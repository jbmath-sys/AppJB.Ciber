# 04. Backlog inicial

Después de definir el modelo de dominio y los supuestos del sistema, se procede a construir el **backlog inicial**, donde se plasman las **épicas** y **primeras historias de usuario** que guiarán el desarrollo del sistema “Videojuegos El Profe 3.0”.  
Este backlog servirá como punto de partida para priorizar las funcionalidades de mayor valor y riesgo dentro del proyecto.

---

## 4.1 Épicas del sistema

Cada épica agrupa un conjunto de funcionalidades relacionadas con un objetivo general del negocio.

| ID | Épica | Descripción |
|----|-------|--------------|
| EP-01 | Gestión de sesiones | Permitir iniciar, pausar y finalizar sesiones de juego en PC o consola con registro automático del tiempo y costo. |
| EP-02 | Ventas rápidas | Registrar la venta de productos (snacks, bebidas, impresiones) de forma ágil desde una interfaz sencilla. |
| EP-03 | Control de caja | Calcular y registrar los ingresos, generar reportes diarios y realizar el cierre de caja. |
| EP-04 | Administración de clientes | Registrar y consultar clientes frecuentes, manteniendo su historial de consumo. |
| EP-05 | Gestión de promociones | Definir promociones y descuentos válidos en fechas específicas. |
| EP-06 | Emisión de tickets | Generar e imprimir comprobantes de venta de forma automática y con detalle de consumos. |

---

## 4.2 Historias de usuario

A partir de las épicas, se redactan las primeras **historias de usuario** en formato ágil utilizando la estructura “Como / Quiero / Para”.

| ID | Historia de usuario | Criterios de aceptación (Dado–Cuando–Entonces) |
|----|----------------------|-----------------------------------------------|
| HU-01 | **Como cajero**, quiero iniciar una sesión de PC o consola, **para** registrar el tiempo de uso y su costo automático. | **Dado** que un cliente solicita tiempo de juego, **cuando** selecciono la estación y duración, **entonces** el sistema debe iniciar una sesión activa con hora de inicio y cálculo de tarifa. |
| HU-02 | **Como cliente**, quiero recibir un ticket con los detalles de mi consumo, **para** conocer el desglose de mis gastos. | **Dado** que se completa una venta, **cuando** el cajero confirma el cobro, **entonces** el sistema debe generar e imprimir un ticket con productos, tiempo y total pagado. |
| HU-03 | **Como administrador**, quiero visualizar el reporte diario de ventas, **para** conocer los ingresos totales y diferencias de caja. | **Dado** que el día laboral termina, **cuando** se realiza el cierre de caja, **entonces** el sistema debe mostrar los totales y permitir exportar el reporte. |
| HU-04 | **Como administrador**, quiero crear y editar promociones, **para** aplicar descuentos automáticos a productos o sesiones durante un periodo específico. | **Dado** que existe una promoción activa, **cuando** se registra una venta, **entonces** el sistema aplica el descuento correspondiente antes del IVA. |
| HU-05 | **Como cajero**, quiero registrar ventas de snacks o bebidas, **para** agilizar la atención al cliente. | **Dado** que un cliente solicita un producto, **cuando** selecciono el artículo y cantidad, **entonces** el sistema debe calcular el total e incluirlo en la venta. |
| HU-06 | **Como administrador**, quiero gestionar los clientes frecuentes, **para** ofrecer descuentos o promociones personalizadas. | **Dado** que se registra un cliente, **cuando** realiza varias compras, **entonces** el sistema debe identificarlo como frecuente y guardar su historial. |

---

## 4.3 Priorización por valor y riesgo

Las historias se ordenan según el **valor que aportan al negocio** y el **riesgo técnico** asociado a su implementación.

| Prioridad | Historia | Valor | Riesgo | Comentario |
|------------|-----------|--------|---------|-------------|
| 🔴 Alta | HU-01 – Iniciar sesión | Alto | Medio | Núcleo del negocio, depende del control de estaciones. |
| 🟠 Alta | HU-02 – Generar ticket | Alto | Bajo | Directamente ligada a la satisfacción del cliente. |
| 🟢 Media | HU-03 – Reporte diario | Medio | Medio | Necesaria para la gestión del negocio, pero no urgente para MVP. |
| 🟢 Media | HU-05 – Ventas rápidas | Medio | Bajo | Incrementa ingresos y agiliza atención. |
| 🔵 Baja | HU-04 – Promociones | Medio | Alto | Implementación más compleja, se puede dejar para iteración siguiente. |
| 🔵 Baja | HU-06 – Clientes frecuentes | Bajo | Bajo | Complementa fidelización; no bloquea operaciones principales. |

---

Con este backlog inicial se establecen las bases funcionales del proyecto, priorizando las historias que entregan **mayor valor comercial** en menor tiempo.  
