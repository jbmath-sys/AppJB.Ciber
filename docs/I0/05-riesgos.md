# 05. Riesgos

Tras definir el backlog inicial, se realiza un análisis de **riesgos potenciales**, se documentan las **convenciones de trabajo** que se seguirán en el proyecto y se efectúa una **revisión final de la Iteración 0 (Incepción)**.  
Esta fase garantiza que toda la documentación esté alineada, completa y lista para dar inicio al desarrollo incremental del sistema.

---

## 5.1 Matriz de riesgos

Los riesgos se evaluaron según su **probabilidad (P)** y **impacto (I)** en una escala del 1 al 5.  
El nivel de prioridad se obtiene de la multiplicación **P × I**, y se propone una **estrategia de respuesta** para cada uno.

| ID | Riesgo | P | I | Nivel | Estrategia / Respuesta |
|----|--------|---|---|--------|------------------------|
| R-01 | Fallo en la impresora de tickets durante la operación diaria | 4 | 4 | 🔴 16 | Implementar opción de ticket digital (PDF o imagen) como respaldo. |
| R-02 | Errores en el cálculo del tiempo de sesión o tarifas | 3 | 5 | 🔴 15 | Validar fórmula y pruebas unitarias del cálculo de tiempo y costo. |
| R-03 | Pérdida de datos por cortes eléctricos o cierres inesperados | 3 | 4 | 🟠 12 | Guardado automático de sesiones y ventas cada 2 minutos. |
| R-04 | Sobrecarga del sistema si hay muchas sesiones simultáneas | 2 | 4 | 🟡 8 | Limitar sesiones concurrentes y optimizar acceso a base de datos. |
| R-05 | Confusión entre roles de usuario (cajero/administrador) | 3 | 3 | 🟡 9 | Definir roles y permisos claramente desde el modelo de seguridad. |
| R-06 | Retrasos en la documentación o subida de archivos al repo | 4 | 2 | 🟠 8 | Establecer entregas diarias y commits por día de trabajo. |
| R-07 | Dificultades con red NAT en consolas Xbox | 2 | 3 | 🟢 6 | Mantener NAT moderado o abierto mediante configuración del router. |

---

