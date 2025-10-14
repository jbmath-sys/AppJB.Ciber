## Actores, Glosario y Reglas de Negocio

En esta sección se identifican los principales actores que interactúan con el sistema, los términos clave del dominio y las primeras reglas de negocio que servirán como base para la siguiente iteración del proyecto.

---

### Actores

En esta sección se identifican los actores que interactúan con el Sistema de Gestión de sala de Videojuegos (Videojuegos El Profe 3.0). Se distinguen actores primarios (buscan objetivos propios con el sistema) y secundarios (dan soporte o proveen servicios externos).
Esta definición permitirá delimitar responsabilidades, permisos y fronteras del sistema para el análisis posterior (clases de dominio y diagramas de secuencia).
A continuación, se presenta una tabla resumen de los actores que intervienen en el sistema, indicando su tipo y una breve descripción de sus objetivos principales.  

| Actor | Tipo | Descripción breve / Objetivo principal |
|--------|------|----------------------------------------|
| **Administrador (Dueño)** | Primario | Configura precios, define tiempo y tarifas de PCs o consolas, gestiona usuarios, inventario, promociones y reportes. Busca tener control total sobre la operación y la rentabilidad. |
| **Cajero** | Primario | Registra sesiones en PC o consola, ventas de snacks o bebidas, genera tickets, cobra y aplica descuentos autorizados. Busca rapidez, precisión y facilidad en el manejo de caja. |
| **Cliente (Jugador)** | Primario | Utiliza las PCs o consolas, solicita servicios de impresión y compra productos. Busca un servicio rápido, económico y confiable. |
| **Invitado (Cliente ocasional)** | Primario | Usuario no registrado que realiza consumos sin historial de cliente frecuente. Busca un servicio ágil y sin necesidad de registro. |
| **Sistema de Tickets / Impresora** | Secundario | Dispositivo externo encargado de imprimir comprobantes de venta y registros de consumo. Interactúa con el sistema para recibir la información del ticket. |
| **Proveedor** | Secundario | Suministra snacks, insumos de impresión y refacciones; requiere órdenes de compra y recepciones|

---
