# 03. Dominio v0 

En esta sección se propone un primer **modelo del dominio (v0)** con las **entidades del negocio** para “Videojuegos El Profe 3.0”. Se incluyen **clases candidatas con atributos mínimos**, un **diagrama de clases** y un listado de **supuestos y restricciones** que guían el alcance técnico inicial.

---

## 3.1 Clases candidatas y atributos mínimos

> Nota: Solo entidades del **negocio** (sin UI ni infraestructura). Tipos sugeridos: `string`, `int`, `decimal`, `datetime`, `bool`.

| Clase | Propósito (negocio) | Atributos mínimos (v0) | Relación clave |
|---|---|---|---|
| **Cliente** | Identifica a quien consume servicios/productos. | `id`, `nombre`, `telefono?`, `esFrecuente: bool` | Tiene **0..*** Sesiones y **0..*** Ventas |
| **Usuario** | Personal que opera el sistema. | `id`, `nombre`, `rol: {Administrador, Cajero}` | Registra Sesiones/Ventas |
| **Estacion** | Punto de consumo: PC o Consola. | `id`, `tipo: {PC, Consola}`, `tarifaPorHora: decimal`, `activa: bool` | Relacionada con Sesiones |
| **Sesion** | Consumo de tiempo en una Estación. | `id`, `clienteId?`, `estacionId`, `inicio: datetime`, `fin?`, `minutosConsumidos (calc)`, `monto (calc)` | 1 Estación, opcional 1 Cliente |
| **Producto** | Snack/bebida/impresión con precio. | `id`, `nombre`, `categoria`, `precioUnitario: decimal`, `stock?: int` | Aparece en Líneas de Venta |
| **Venta** | Transacción de cobro (tiempo y/o productos). | `id`, `fecha: datetime`, `clienteId?`, `usuarioId`, `subtotal (calc)`, `iva (calc)`, `total (calc)` | Tiene **1..*** Líneas de Venta y 0..1 Ticket |
| **LineaVenta** | Ítem con cantidad y precio. | `id`, `ventaId`, `tipoItem: {Sesion, Producto}`, `referenciaId`, `cantidad: int`, `precioUnitario: decimal`, `importe (calc)` | Pertenece a 1 Venta |
| **Ticket** | Comprobante de la Venta. | `id`, `ventaId (único)`, `folio`, `emitidoEn: datetime` | 1–1 con Venta |


**Atributos mínimos detallados**  
- **Cliente:** `id:string`, `nombre:string`, `telefono?:string`, `esFrecuente:bool`  
- **Usuario:** `id:string`, `nombre:string`, `rol:string` (valores: *Administrador*, *Cajero*)  
- **Estacion:** `id:string`, `tipo:string` (*PC*, *Consola*), `tarifaPorHora:decimal`, `activa:bool`  
- **Sesion:** `id:string`, `clienteId?:string`, `estacionId:string`, `inicio:datetime`, `fin?:datetime`  
- **Producto:** `id:string`, `nombre:string`, `categoria:string`, `precioUnitario:decimal`, `stock?:int`  
- **Venta:** `id:string`, `fecha:datetime`, `clienteId?:string`, `usuarioId:string`  
- **LineaVenta:** `id:string`, `ventaId:string`, `tipoItem:string` (*Sesion* | *Producto*), `referenciaId:string`, `cantidad:int`, `precioUnitario:decimal`  
- **Ticket:** `id:string`, `ventaId:string`, `folio:string`, `emitidoEn:datetime`  


---

## 3.2 Diagrama de clases v0 (PlantUML)

