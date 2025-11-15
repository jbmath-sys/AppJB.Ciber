
# CU-05: Cobrar

**Actor principal:** Cajero  
**Tipo:** Primario  
**Prioridad:** Alta  
**Iteración:** I1 – Núcleo Cliente + Sesiones  

---

## 1. Objetivo
Registrar el **pago** del consumo (tiempo de juego y/o productos), aceptando **uno o varios métodos de pago**, calculando **cambio** en pagos en efectivo, emitiendo el **comprobante (ticket)** y cerrando la operación de caja de manera consistente.

---

## 2. Descripción breve
Tras cerrar la sesión (CU-04) y tener el **total calculado**, el cajero selecciona el ticket **Pendiente de pago**, elige método de pago en efectivo, confirma el cobro, genera el comprobante e imprime (o emite digital). El sistema marca el ticket como **Pagado** y registra movimientos en caja.

---

## 3. Precondiciones
- Existe un **Ticket** con estado `Pendiente` asociado a la sesión o venta.  
- El **Total**, **Descuento** e **IVA** ya están calculados (desde CU-04 o carrito de venta).  
- El cajero inició sesión y tiene permisos de cobro.  
- La conexión a la base de datos está activa.  
- (Opcional) La impresora de tickets está disponible; si no, se permite ticket digital.

---

## 4. Flujo principal

| Paso | Actor / Sistema | Descripción |
|------|------------------|-------------|
| 1 | Actor | Abre **Caja → Cobrar** y selecciona el ticket `Pendiente`. |
| 2 | Sistema | Muestra el **desglose**: líneas (tiempo y/o productos), subtotal, descuentos, IVA y total. |
| 3 | Actor | Selecciona método de pago: **Efectivo**. |
| 4 | Actor | Ingresa monto(s) recibido(s). |
| 5 | Sistema | Valida que la suma de montos sea **≥ Total**; calcula **cambio** si aplica. |
| 6 | Actor | Confirma **Cobrar**. |
| 7 | Sistema | Registra el pago, marca `Ticket.Estado = Pagado`, y crea movimiento en **Corte de Caja**. |
| 8 | Sistema | Genera **Ticket/Folio** y ofrece **Imprimir** o **Enviar digital**. |
| 9 | Actor | Entrega ticket al cliente y finaliza. |

---

## 5. Flujos alternos / excepciones

| Código | Descripción |
|-------|-------------|
| **A1 – Pago insuficiente** | Si la suma recibida **< Total**, sistema muestra *“Monto insuficiente”* y bloquea el cobro. |
| **A2 – Cambio insuficiente en caja** | Si no hay cambio disponible, se sugiere redondeo o método adicional; el cajero puede **mixto** (efectivo + tarjeta). |
| **A3 – Tarjeta declinada** | Mostrar *“Transacción rechazada”* y permitir reintentar o cambiar de método sin registrar pago. |
| **A4 – Error de conexión** | Si falla al guardar pago, revertir operación y mostrar *“No se pudo registrar el cobro”*. |
| **A5 – Impresora no disponible** | Emitir **ticket digital (PDF/imagen)** y registrar incidente; no bloquear el pago. |
| **A6 – Cancelación antes de confirmar** | El cajero puede cancelar el cobro antes del paso 6; el ticket permanece `Pendiente`. |

---

## 6. Inclusiones (include)
- **CU-04 Cerrar Sesión** (origen del ticket con total calculado).  
- (Futuro) **CU-06 Devolución/Cancelación de venta** (reversos y notas de crédito).

---

## 7. Postcondiciones
- `Ticket.Estado = Pagado`, con **métodos y montos** registrados.  
- Se crea **Movimiento de Caja** (ingresos por método).  
- Se genera **Folio de ticket** y, si aplica, archivo para impresión/digital.  
- (Si era tiempo de juego) La **sesión** ya quedó **Finalizada** desde CU-04.

---

## 8. Reglas de negocio relacionadas
- **RB1:** El **pago puede ser mixto** (varios métodos) siempre que la suma **≥ Total**.  
- **RB2:** Se permite **redondeo** al múltiplo de $0.50 o $1.00 (configurable) para manejo de cambio.  
- **RB3:** El **cambio** se calcula sobre el subtotal de **efectivo**.  
- **RB4:** El ticket pagado no puede editarse; sólo mediante **Devolución/Cancelación** (otra IU y permisos).  
- **RB5:** El **folio** del ticket es único y se asigna al confirmar el cobro.  
- **RB6:** Si falla la impresora, **no bloquea** el registro del pago (ticket digital).

---

## 9. Datos de prueba sugeridos

| Caso | Total | Método(s) | Monto(s) | Cambio | Resultado esperado |
|------|-------|-----------|----------|--------|--------------------|
| 1 | $21.75 | Efectivo | $50.00 | $28.25 | Pagado, folio generado, movimiento de caja (efectivo) |
| 2 | $24.36 | Mixto (Efe+Tj) | $10.00 + $14.36 | $0.00 | Pagado, registra dos métodos |
| 3 | $15.95 | Efectivo | $15.00 | — | Error A1 (monto insuficiente) |
| 4 | $23.00 | Tarjeta | $23.00 | $0.00 | Pagado; si declina → A3 |
| 5 | $40.00 | Efectivo | $100.00 | $60.00 | Pagado; validar **caja con cambio** o sugerir mixto (A2) |

---

## 10. Diagramas relacionados
- `secuencia-cerrar-cobrar.puml` (bloque de cobro)  
- `actividad-cobrar.puml` (flujo con ramas de error)  
- `dominio-v1.puml` (Ticket, LineaVenta, Pago/MovimientoCaja)

---

## 11. Notas técnicas
- **Entidades sugeridas**  
  - `Ticket(Id, SesionId?, Fecha, Subtotal, Descuento, IVA, Total, Estado, Folio)`  
  - `Pago(Id, TicketId, Metodo, Monto, Autorizacion?, Fecha)`  
  - `MovimientoCaja(Id, Tipo, Metodo, Monto, Fecha, TicketId?)`  
- **Servicios**  
  - `CobroService.RegistrarPago(ticketId, IEnumerable<PagoDto>)`  
  - `CajaService.RegistrarMovimiento(...)`  
  - `TicketService.GenerarComprobante(ticketId, formato)`  
- **DTOs**  
  - `PagoDto { Metodo: string; Monto: decimal; Referencia?: string }`  
  - `ComprobanteDto { Folio, Total, QrUrl?, PdfPath? }`  
- **Mensajes UX**  
  - 🟢 *Pago registrado. Folio: JB-2025-000123*  
  - ⚠️ *Monto insuficiente / Tarjeta declinada / Sin cambio suficiente*  
  - ❌ *No se pudo registrar el cobro. Intente de nuevo.*

---

## 12. Ejemplo (de CU-04 → CU-05)
**Ticket**: Total $24.36 (Consola 40 min con 10% frecuente).  
**Pago**: $10.00 efectivo + $14.36 tarjeta → **Mixto**.  
**Cambio**: $0.00.  
**Resultado**: Ticket **Pagado**, Folio generado, ticket PDF disponible, movimientos de caja: Efectivo $10.00, Tarjeta $14.36.

---

**Autor:** Lic. en Matemáticas Juan Bernardo López Acosta— *Sistema de Gestión de Ciber (AppJB.Ciber)*  
**Fecha de redacción:** 19/oct/2025  
**Versión:** v1.0
