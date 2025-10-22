# CU-02: Iniciar Sesión de Juego

**Actor principal:** Cajero  
**Tipo:** Primario  
**Prioridad:** Alta  
**Iteración:** I1 – Núcleo Cliente + Sesiones  

---

## 1. Objetivo
Permitir al cajero iniciar una nueva sesión de juego en una estación (PC o Consola) para un cliente, registrando la hora de inicio y el tipo de estación para el cálculo posterior del tiempo y del costo.

---

## 2. Descripción breve
El actor selecciona al cliente y la estación disponible.  
El sistema valida que la estación esté libre, registra la hora de inicio y crea una sesión con estado **“En curso”**.  
Esta sesión servirá para calcular el tiempo consumido, aplicar promociones y generar el ticket al finalizar.

---

## 3. Precondiciones
- El actor ha iniciado sesión en el sistema.  
- Existen estaciones registradas con estado “Disponible”.  
- El cliente está registrado (o puede ser un invitado).  
- La conexión con la base de datos está activa.

---

## 4. Flujo principal

| Paso | Actor / Sistema | Descripción |
|------|------------------|--------------|
| 1 | Actor | Selecciona **Iniciar Sesión de juego** desde el menú de Caja. |
| 2 | Sistema | Muestra lista de estaciones disponibles y clientes registrados. |
| 3 | Actor | Elige un cliente y una estación. |
| 4 | Sistema | Verifica que la estación esté libre y el cliente no tenga otra sesión activa. |
| 5 | Sistema | Registra la hora de inicio (`Inicio = Now()`), el tipo de estación (PC o Consola) y el estado “En curso”. |
| 6 | Sistema | Cambia el estado de la estación a “Ocupada”. |
| 7 | Sistema | Muestra al cajero la pantalla **Sesión en curso** con cronómetro activo. |
| 8 | Actor | Confirma visualmente que la sesión ha iniciado correctamente. |

---

## 5. Flujos alternos / extensiones

| Código | Descripción |
|---------|--------------|
| **A1** | **Estación ocupada:** Si la estación no está disponible, el sistema muestra mensaje *“Estación en uso”* y cancela la operación. |
| **A2** | **Cliente con sesión activa:** Si el cliente ya tiene una sesión abierta, muestra *“Cliente ya en sesión”* y ofrece opción para reanudar o cerrar la anterior. |
| **A3** | **Invitado:** Si el cliente no está registrado, el cajero puede crear un *Cliente tipo Invitado* (ver CU-01-A4). |
| **A4** | **Error de conexión:** Si ocurre un fallo al guardar, muestra *“No se pudo iniciar la sesión”* y no cambia el estado de la estación. |

---

## 6. Inclusiones (include)
- CU-01 Registrar Cliente (si el cliente es nuevo o invitado).  
- CU-00 Iniciar Sesión del Sistema (precondición general).  

---

## 7. Postcondiciones
- Se crea un registro en la entidad `Sesion` con:
  - `Estado = EnCurso`
  - `FechaInicio = actual`
  - `EstacionId` y `ClienteId` válidos.  
- La estación pasa a estado **Ocupada**.  
- El cronómetro o temporizador comienza a correr para medir el tiempo.  

---

## 8. Reglas de negocio relacionadas
- **RB1:** Una estación solo puede tener **una sesión activa** a la vez.  
- **RB2:** Un cliente no puede tener **más de una sesión abierta** simultáneamente.  
- **RB3:** La **tarifa por hora** depende del tipo de estación (`PC`, `Consola`).  
- **RB4:** La **hora de inicio** se registra automáticamente desde el reloj del sistema.  
- **RB5:** La sesión pasa a estado *Pausada*, *Finalizada* o *Cancelada* según el flujo posterior.  

---

## 9. Datos de prueba sugeridos

| Cliente | Estación | Tipo | Hora inicio | Resultado esperado |
|----------|-----------|------|-------------|--------------------|
| Ana Torres | PC-01 | PC | 16:00 | Sesión iniciada (estado EnCurso) |
| Luis Pérez | XBX-01 | Consola | 17:30 | Sesión iniciada (estado EnCurso) |
| Ana Torres | XBX-02 | Consola | 16:10 | Error (cliente ya tiene sesión activa) |
| — (Invitado) | PC-02 | PC | 18:00 | Sesión iniciada como cliente invitado |

---

## 10. Diagramas relacionados
- `actividad-iniciar-sesion.puml`  
- `secuencia-iniciar-sesion.puml`  
- `dominio-v1.puml` (relación *Cliente–Estación–Sesión*)  

---

## 11. Notas técnicas
- **Entidad:** `Sesion(Id, ClienteId, EstacionId, Inicio, Fin, Estado)`  
- **Estados posibles:** `EnCurso`, `Pausada`, `Finalizada`.  
- **Servicios involucrados:**  
  - `SesionService.StartSession(dto)`  
  - `EstacionService.UpdateEstado("Ocupada")`  
- **Mensajes UX:**  
  - ✔️ *Sesión iniciada correctamente.*  
  - ⚠️ *Estación ocupada o cliente activo.*  
  - ❌ *Error al crear sesión.*

---

**Autor:** Lic. en Matematicas Juan Bernardo Lopez Acosta— *Sistema de Gestión de Ciber (AppJB.Ciber)*  
**Fecha de redacción:** 18/oct/2025  
**Versión:** v1.0  

