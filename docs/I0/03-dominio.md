# 03. Dominio

Después de identificar los actores, el glosario de términos y las reglas de negocio, el siguiente paso consiste en modelar el **dominio del sistema**, es decir, representar las **entidades principales** que forman parte del negocio y las **relaciones** entre ellas.  
Este modelo conceptual servirá como base para construir los casos de uso y los diagramas de secuencia en las próximas iteraciones.

En esta sección se propone un primer **modelo del dominio (v0)** con las **entidades del negocio** para “Videojuegos El Profe 3.0”. Se incluyen **clases candidatas con atributos mínimos**, un **diagrama de clases** y un listado de **supuestos y restricciones** que guían el alcance técnico inicial.

---

## 3.1 Clases candidatas y atributos mínimos

Para comprender mejor la estructura del negocio, se identifican las **clases candidatas** que representan los principales conceptos del dominio.  
Cada clase incluye un conjunto mínimo de **atributos esenciales** que describen su información básica y permiten modelar las relaciones más relevantes entre las entidades.

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
| **Promocion** | Regla comercial temporal. | `id`, `nombre`, `descripcion`, `tipo: {Porcentaje, Fijo}`, `valor: decimal`, `inicio: datetime`, `fin: datetime`, `activa: bool` | Puede afectar Sesiones/Productos (aplicación en lógica) |

A continuación, se detallan los **atributos mínimos** de cada clase, especificando su tipo de dato y propósito dentro del modelo.  
Esta descripción complementa la tabla anterior y servirá como referencia para el diseño lógico y la futura implementación en código.

**Atributos mínimos detallados**  
- **Cliente:** `id:string`, `nombre:string`, `telefono?:string`, `esFrecuente:bool`  
- **Usuario:** `id:string`, `nombre:string`, `rol:string` (valores: *Administrador*, *Cajero*)  
- **Estacion:** `id:string`, `tipo:string` (*PC*, *Consola*), `tarifaPorHora:decimal`, `activa:bool`  
- **Sesion:** `id:string`, `clienteId?:string`, `estacionId:string`, `inicio:datetime`, `fin?:datetime`  
- **Producto:** `id:string`, `nombre:string`, `categoria:string`, `precioUnitario:decimal`, `stock?:int`  
- **Venta:** `id:string`, `fecha:datetime`, `clienteId?:string`, `usuarioId:string`  
- **LineaVenta:** `id:string`, `ventaId:string`, `tipoItem:string` (*Sesion* | *Producto*), `referenciaId:string`, `cantidad:int`, `precioUnitario:decimal`  
- **Ticket:** `id:string`, `ventaId:string`, `folio:string`, `emitidoEn:datetime`  
- **Promocion:** `id:string`, `nombre:string`, `descripcion:string`, `tipo:string` (*Porcentaje* | *Fijo*), `valor:decimal`, `inicio:datetime`, `fin:datetime`, `activa:bool`
  
---

## 3.2 Diagrama de clases

Una vez definidas las clases candidatas y sus atributos mínimos, se representa gráficamente su estructura mediante un **diagrama de clases**.  
Este diagrama permite visualizar cómo se relacionan las entidades del negocio entre sí y facilita la comprensión de la información que manejará el sistema.

Nuestro diagrama es:

![Diagrama de clases](../imagenes/i0/Diagrama_de_Clases.png)

---

## 3.3 Supuestos y restricciones

Después de representar el modelo de clases del dominio, es importante documentar los **supuestos** que se tomaron durante su elaboración y las **restricciones técnicas u operativas** que podrían afectar el funcionamiento del sistema.  
Estos elementos ayudan a mantener la coherencia entre el modelo conceptual y las condiciones reales del entorno donde será implementado el sistema “Videojuegos El Profe 3.0”.

---

### Supuestos de negocio

1. Un **Invitado** se maneja como `Cliente` sin teléfono y con `esFrecuente = false`.  
2. Una **Venta** puede incluir **tiempo de juego (Sesión)** y **productos** en el mismo ticket.  
3. La **tarifa por hora** depende del tipo de **Estación** (PC/Consola) y se calcula de forma proporcional al tiempo consumido.  
4. Las **Promociones** se aplican **antes del IVA** y pueden ser por **porcentaje** o **monto fijo**.  
5. El **Ticket** tiene relación **1 a 1** con la **Venta** y se genera al momento del cobro.  

---

### Restricciones técnicas / operativas

1. La **impresora de tickets** debe estar disponible localmente; si falla, el sistema podrá emitir un **ticket digital** (PDF o imagen).  
2. **NAT / Red Xbox:** para consolas, se asume una configuración de **NAT abierto**; en caso de **NAT estricto**, algunas funciones en línea podrían no estar disponibles.  
3. El **inventario** de productos se descuenta automáticamente en cada **Línea de Venta** de tipo *Producto*.  
4. Las **integraciones externas** (pagos en línea, sistemas de lealtad, etc.) quedan fuera del alcance del **v0**.  
5. El cálculo de **minutosConsumidos** y **monto** en la **Sesión** se realiza al cerrarla (o en tiempo real, sin guardar cada actualización).  

---

Con estos supuestos y restricciones se establecen los límites operativos del modelo de dominio.  
Esta información será clave para definir las **épicas e historias de usuario** que compondrán el **backlog inicial** en la siguiente jornada de trabajo.

