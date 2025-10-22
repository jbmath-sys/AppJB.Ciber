# CU-03: Pausar / Reanudar Sesión

**Actor principal:** Cajero  
**Tipo:** Primario  
**Prioridad:** Alta  
**Iteración:** I1 – Núcleo Cliente + Sesiones  

---

## 1. Objetivo
Permitir al cajero **pausar temporalmente** una sesión de juego (PC o Consola) y **reanudarla posteriormente**, sin perder el tiempo ya acumulado, asegurando que el cálculo final sea proporcional al tiempo efectivamente jugado.

---

## 2. Descripción breve
Durante una sesión en curso, el cliente puede solicitar una pausa (por salida momentánea, cambio de jugador o problema técnico).  
El cajero puede pausar la sesión, quedando el cronómetro detenido y la estación libre.  
Cuando el cliente regresa, el cajero puede reanudar la sesión, continuando el conteo desde el tiempo acumulado.

---

## 3. Precondiciones
- Existe una sesión activa con `Estado = EnCurso`.  
- El actor (cajero) tiene permisos de control sobre sesiones.  
- La conexión con la base de datos está activa.  

---

## 4. Flujo principal (Pausar)

| Paso | Actor / Sistema | Descripción |
|------|------------------|--------------|
| 1 | Actor | Desde la pantalla “Sesión en curso”, selecciona **Pausar**. |
| 2 | Sistema | Muestra diálogo de confirmación. |
| 3 | Actor | Confirma la acción. |
| 4 | Sistema | Registra la hora de pausa (`HoraPausa = Now()`). |
| 5 | Sistema | Calcula tiempo transcurrido desde el último inicio o reanudación y lo suma al campo `MinutosAcumulados`. |
| 6 | Sistema | Cambia el estado de la sesión a **Pausada**. |
| 7 | Sistema | Cambia el estado de la estación a **Disponible** (temporalmente). |
| 8 | Sistema | Muestra mensaje *“Sesión pausada correctamente”*. |

---

## 5. Flujo alterno: Reanudar

| Paso | Actor / Sistema | Descripción |
|------|------------------|--------------|
| 1 | Actor | Desde la lista de sesiones pausadas, selecciona **Reanudar**. |
| 2 | Sistema | Verifica que la estación asociada esté disponible. |
| 3 | Sistema | Registra hora de reanudación (`HoraReanudacion = Now()`). |
| 4 | Sistema | Cambia estado de la sesión a **EnCurso**. |
| 5 | Sistema | Cambia la estación a estado **Ocupada**. |
| 6 | Sistema | Muestra nuevamente la vista “Sesión en curso” con cronómetro activo. |

---

## 6. Flujos alternos / excepciones

| Código | Descripción |
|---------|--------------|
| **A1** | **Sesión ya pausada:** Si intenta pausar una sesión que no está en curso, muestra *“Sesión no activa”*. |
| **A2** | **Reanudar sin pausa:** Si intenta reanudar una sesión que no está pausada, muestra *“No se puede reanudar, sesión en curso o finalizada”*. |
| **A3** | **Estación ocupada:** Si la estación está ocupada al intentar reanudar, muestra *“Estación actualmente en uso”*. |
| **A4** | **Error de conexión:** Si no se puede guardar el cambio de estado, muestra *“Error al actualizar sesión”*. |

---

## 7. Inclusiones (include)
- CU-02 Iniciar Sesión de Juego (precondición).  
- CU-04 Cerrar Sesión (flujo posterior).  

---

## 8. Postcondiciones
- Al pausar:  
  - Se registra la hora de pausa.  
  - Se actualiza `MinutosAcumulados`.  
  - Estado de la sesión = **Pausada**.  
  - Estación = **Disponible**.  
- Al reanudar:  
  - Se registra hora de reanudación.  
  - Estado de la sesión = **EnCurso**.  
  - Estación = **Ocupada**.  

---

## 9. Reglas de negocio relacionadas
- **RB1:** El tiempo total se calcula sumando cada intervalo *entre inicio–pausa–reanudar–fin*.  
- **RB2:** Una sesión pausada puede permanecer inactiva un máximo de *5 minutos* (configurable).  
- **RB3:** Solo una sesión activa puede estar asociada a una estación en un momento dado.  
- **RB4:** La pausa no genera costo adicional; solo se cobra el tiempo efectivamente jugado.  
- **RB5:** Si una sesión supera el tiempo límite en pausa, el sistema puede cerrarla automáticamente (en futuras iteraciones).

---

## 10. Datos de prueba sugeridos

| Caso | Hora inicio | Hora pausa | Hora reanudación | Minutos cobrables | Resultado esperado |
|-------|--------------|-------------|------------------|--------------------|--------------------|
| 1 | 16:00 | 16:20 | 16:30 | 20 + 30 = 50 | Sesión reanudada, tiempo acumulado correcto |
| 2 | 17:10 | 17:40 | — | 30 | Sesión pausada (sin reanudar aún) |
| 3 | 18:00 | 18:10 | 18:12 | 2 + (reanudado activo) | Reanuda correctamente |
| 4 | 19:00 | — | — | — | Error: no se puede pausar sesión inactiva |

---

## 11. Diagramas relacionados
- `actividad-pausar-reanudar.puml`  
- `secuencia-pausar-reanudar.puml`  
- `dominio-v1.puml` (atributos `Inicio`, `Fin`, `MinutosAcumulados`, `Estado`)  

---

## 12. Notas técnicas
- **Entidad:** `Sesion(Id, ClienteId, EstacionId, Inicio, Fin?, Estado, MinutosAcumulados)`  
- **Servicios involucrados:**  
  - `SesionService.PauseSession(sessionId)`  
  - `SesionService.ResumeSession(sessionId)`  
  - `EstacionService.UpdateEstado("Disponible"/"Ocupada")`  
- **DTOs usados:**  
  - `PauseSessionRequest`  
  - `ResumeSessionRequest`  
- **Mensajes UX:**  
  - 🟡 *Sesión pausada correctamente.*  
  - 🟢 *Sesión reanudada correctamente.*  
  - ⚠️ *No se puede reanudar, estación ocupada.*  
  - ❌ *Error al actualizar sesión.*

---

**Autor:** Lic. en Matematicas Juan Bernardo López Acosta — *Sistema de Gestión de Ciber (AppJB.Ciber)*  
**Fecha de redacción:** 22/oct/2025  
**Versión:** v1.0  

