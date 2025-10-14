## Actores, Glosario y Reglas de Negocio

En esta sección se identifican los principales actores que interactúan con el sistema, los términos clave del dominio y las primeras reglas de negocio que servirán como base para la siguiente iteración del proyecto.

---

### Actores

Los actores que interactúan con el Sistema de Gestión de sala de Videojuegos (Videojuegos El Profe 3.0). Se distinguen actores primarios (buscan objetivos propios con el sistema) y secundarios (dan soporte o proveen servicios externos).
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


### Glosario de Términos

El glosario define los conceptos fundamentales del dominio de negocio que se usarán durante el análisis y diseño del sistema.  
Estos términos garantizan un lenguaje común entre los miembros del equipo y los interesados.

A continuación se enlistan cada uno de los terminos con su definición clara y precisas, los cuales son:

| Término | Definición |
|----------|------------|
| **Sesión** | Periodo de tiempo en el que un cliente utiliza una PC o consola. Se inicia al registrar el tiempo y finaliza al concluir el servicio o agotarse el saldo. |
| **PC** | Equipo de cómputo destinado al uso individual de los clientes dentro del ciber. Cada PC tiene una tarifa por hora. |
| **Consola** | Dispositivo de videojuegos disponible para renta por tiempo. Se maneja de manera similar a una PC pero con tarifas y reglas diferentes. |
| **Ticket** | Comprobante impreso que contiene los detalles del servicio: cliente, tiempo, total pagado y fecha. |
| **Promoción** | Oferta especial o descuento temporal aplicado a servicios o productos para incentivar las ventas. |
| **Inventario** | Conjunto de productos disponibles para la venta (bebidas, snacks, accesorios). Se actualiza automáticamente tras cada venta. |
| **Cierre de caja** | Proceso final del día en el cual se calcula el total de ventas, efectivo disponible y se genera el reporte diario. |
| **Descuento** | Reducción en el precio de un servicio o producto, autorizada únicamente por el administrador. |
| **Saldo** | Monto de dinero disponible en una cuenta de cliente para consumir en el sistema. |
| **Tiempo restante** | Cantidad de minutos o segundos disponibles en una sesión antes de que finalice. |
| **Reporte diario** | Documento o resumen que muestra todas las operaciones realizadas durante la jornada laboral. |
| **Usuario** | Persona registrada que puede iniciar sesión en el sistema con credenciales. Puede tener roles como Administrador o Cajero. |
