# CU-04: Cerrar Sesión

**Actor principal:** Cajero  
**Tipo:** Primario  
**Prioridad:** Alta  
**Iteración:** I1 – Núcleo Cliente + Sesiones  

---

## 1. Objetivo
Permitir al cajero **cerrar una sesión de juego** en curso o pausada, calcular el **tiempo total jugado**, aplicar las **promociones y el IVA** correspondientes, y **generar el ticket de venta** asociado al cobro final.

---

## 2. Descripción breve
Cuando el cliente finaliza su tiempo de juego, el cajero selecciona la sesión activa y elige **Cerrar Sesión**.  
El sistema detiene el cronómetro, calcula el tiempo total cobrado, aplica promociones, calcula impuestos y genera un ticket con el monto final.  
Finalmente, cambia el estado de la sesión a *Finalizada* y la estación vuelve a *Disponible*.

---

## 3. Precondiciones
- Existe una sesión con `Estado = EnCurso` o `Pausada`.  
- La estación asociada está registrada en el sistema.  
- El cajero tiene permisos de cierre y cobro.  
- Conexión con la base de datos activa.

---

## 4. Flujo principal

| Paso | Actor / Sistema | Descripción |
|------|------------------|--------------|
| 1 | Actor | Desde la vista “Sesión en curso”, selecciona **Cerrar Sesión**. |
| 2 | Sistema | Solicita confirmación de cierre. |
| 3 | Actor | Confirma la acción. |
| 4 | Sistema | Registra `HoraFin = Now()`. |
| 5 | Sistema | Calcula el **tiempo total** sumando todos los intervalos (inicio–pausas–reanudaciones). |
| 6 | Sistema | Obtiene **tarifa por hora** según tipo de estación (PC o Consola). |
| 7 | Sistema | Aplica promociones activas (por cliente o rango horario). |
| 8 | Sistema | Calcula **subtotal, descuento, IVA y total a cobrar**. |
| 9 | Sistema | Genera registro `Ticket` y `LineaVenta` con el detalle. |
| 10 | Sistema | Cambia `EstadoSesion = Finalizada` y `EstadoEstacion = Disponible`. |
| 11 | Sistema | Muestra desglose en pantalla con opción **Cobrar / Imprimir Ticket**. |
| 12 | Actor | Confirma cobro y entrega ticket al cliente. |

---

## 5. Flujos alternos / excepciones

| Código | Descripción |
|---------|--------------|
| **A1** | **Sesión ya finalizada:** Si el cajero intenta cerrar una sesión ya cerrada, el sistema muestra *“Sesión finalizada previamente”*. |
| **A2** | **Sesión sin tiempo jugado:** Si el tiempo total es cero, muestra *“No se puede cerrar una sesión sin consumo”*. |
| **A3** | **Error de conexión:** Si ocurre un fallo al guardar el ticket, muestra *“No se pudo registrar el cobro”*. |
| **A4** | **Impresora no disponible:** Si falla la impresora, se genera ticket digital (PDF o imagen). |
| **A5 (Extend)** | **Aplicar descuento manual:** El cajero autorizado puede aplicar un descuento adicional antes del cierre. |

---

## 6. Inclusiones (include)
- CU-03 Pausar / Reanudar Sesión (si hubo pausas intermedias).  
- CU-05 Cobrar (para la operación de pago, si se implementa aparte).  

---

## 7. Postcondiciones
- Se registra `HoraFin` y `TiempoTotal` en la tabla `Sesion`.  
- Se genera un `Ticket` con su respectiva `LineaVenta`.  
- La estación queda **disponible** para un nuevo cliente.  
- El monto total queda registrado en la base de datos para reportes de ventas.  

---

## 8. Reglas de negocio relacionadas
- **RB1:** El tiempo total se calcula sumando los tramos efectivamente jugados (inicio–pausa–reanudar–fin).  
- **RB2:** Las promociones se aplican **antes del IVA**.  
- **RB3:** El IVA se calcula sobre el subtotal neto (tras descuentos).  
- **RB4:** Cada sesión cerrada genera exactamente **un ticket**.  
- **RB5:** La tarifa depende del tipo de estación (`PC = 25 $/h`, `Consola = 35 $/h` por defecto).  
- **RB6:** Se pueden aplicar descuentos por cliente frecuente o promoción activa.  

---

## 9. Datos de prueba sugeridos

| Caso | Tipo estación | Tiempo total | Promoción | Resultado esperado |
|-------|----------------|---------------|-------------|--------------------|
| 1 | PC | 45 min | Ninguna | Total $21.75 (IVA incluido) |
| 2 | Consola | 40 min | Frecuente 10% | Total $24.36 |
| 3 | PC | 45 min | Hora Feliz −$5 | Total $15.95 |
| 4 | Consola | 0 min | — | Error “sin consumo” |
| 5 | PC | 60 min | Descuento manual −$3 | Total $23.00 aprox. |

---

## 10. Diagramas relacionados
- `actividad-cerrar-sesion.puml`  
- `secuencia-cerrar-cobrar.puml`  
- `dominio-v1.puml` (relaciones `Sesion–Ticket–LineaVenta`)  

---

## 11. Notas técnicas
- **Entidades:**  
  - `Sesion(Id, ClienteId, EstacionId, Inicio, Fin, Estado, MinutosAcumulados)`  
  - `Ticket(Id, SesionId, Fecha, Subtotal, Descuento, IVA, Total)`  
  - `LineaVenta(Id, TicketId, Concepto, Cantidad, PrecioUnit, Importe)`  
- **Servicios involucrados:**  
  - `SesionService.CloseSession(sessionId)`  
  - `PrecioService.CalcularTotal(sessionId)`  
  - `TicketService.GenerarTicket(sessionId)`  
- **Mensajes UX:**  
  - 🟢 *Sesión cerrada correctamente.*  
  - ⚠️ *Tiempo insuficiente para cerrar.*  
  - ❌ *Error al registrar ticket o conexión fallida.*  

---

## 12. Ejemplo de cálculo (escenario real)

**Cliente:** Ana Torres  
**Estación:** XBOX-01 (Consola)  
**Tiempo total:** 40 min  
**Tarifa:** $35/h → 35 × (40/60) = $23.33  
**Descuento (Frecuente 10%)** = −$2.33  
**Subtotal** = $21.00  
**IVA 16%** = $3.36  
**Total** = $24.36  
✅ Ticket generado y sesión finalizada.

---

**Autor:** Lic en Matemáticas Juan Bernardo López Acosta — *Sistema de Gestión de Ciber (AppJB.Ciber)*  
**Fecha de redacción:** 22/oct/2025  
**Versión:** v1.0  

