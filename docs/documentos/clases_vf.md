## 🟩 Cliente
| **Atributo / Método** | **Descripción** |
|------------------------|-----------------|
| `id` | Identificador único del cliente. |
| `nombre` | Nombre del cliente. |
| `telefono` | Teléfono registrado. |
| `esFrecuente` | Indica si es cliente frecuente. |
| `actualizarContacto(nuevoTelefono)` | Modifica el número telefónico. |
| `marcarComoFrecuente()` | Marca al cliente como frecuente. |
| `esElegibleParaPromoción()` | Determina si puede recibir promociones. |

## 🟩 Usuario
| **Atributo / Método** | **Descripción** |
|------------------------|-----------------|
| `id` | Identificador del usuario del sistema. |
| `nombre` | Nombre del empleado. |
| `rol` | Cajero o Administrador. |
| `esAdministrador()` | Verifica si el usuario tiene rol administrador. |
| `esCajero()` | Verifica si el usuario es cajero. |
| `puedeAplicarDescuento()` | Determina si puede aplicar promociones. |

## 🟩 Estación
| **Atributo / Método** | **Descripción** |
|------------------------|-----------------|
| `id` | Identifica la estación. |
| `tipo` | PC o Consola. |
| `tarifaPorHora` | Costo por hora de uso. |
| `activa` | Indica si está disponible para operar. |
| `activar()` | Habilita la estación. |
| `desactivar()` | Deshabilita la estación. |
| `marcarOcupada()` | Indica que la estación está en uso. |
| `marcarDisponible()` | Libera la estación. |
| `estaDisponible()` | Retorna si está lista para usarse. |

## 🟩 Sesión
| **Atributo / Método** | **Descripción** |
|------------------------|-----------------|
| `id` | Identificador único de la sesión. |
| `clienteId` | Cliente asociado. |
| `estacionId` | Estación utilizada. |
| `inicio` | Hora de inicio. |
| `fin` | Hora de finalización. |
| `finalizar(fin)` | Cierra la sesión. |
| `calcularMinutosConsumidos()` | Calcula la duración total. |
| `calcularMonto(tarifaPorHora)` | Calcula el precio final según minutos. |
| `estaActiva()` | Indica si la sesión sigue en curso. |

## 🟩 Producto
| **Atributo / Método** | **Descripción** |
|------------------------|-----------------|
| `id` | Identificador del producto. |
| `nombre` | Nombre o descripción. |
| `categoria` | Tipo de producto (snack, bebida…). |
| `precioUnitario` | Precio por unidad. |
| `stock` | Existencia actual. |
| `actualizarPrecio(nuevoPrecio)` | Cambia el precio unitario. |
| `ajustarStock(cantidad)` | Incrementa o reduce existencias. |
| `hayStockRequerido(cantidad)` | Verifica si hay stock suficiente. |

## 🟩 Promoción
| **Atributo / Método** | **Descripción** |
|------------------------|-----------------|
| `id` | Identificador de la promoción. |
| `nombre` | Nombre promocional. |
| `descripcion` | Detalles de la promoción. |
| `tipo` | Porcentaje o cantidad fija. |
| `valor` | Cantidad que descuenta. |
| `inicio` | Inicio de vigencia. |
| `fin` | Fin de vigencia. |
| `activa` | Indica si puede aplicarse. |
| `estaVigente(fecha)` | Valida si la promo está dentro de la vigencia. |
| `calcularDescuento(montoBase)` | Aplica el descuento al monto dado. |
| `activar()` | Activa la promoción. |
| `desactivar()` | Desactiva la promoción. |

## 🟩 Venta
| **Atributo / Método** | **Descripción** |
|------------------------|-----------------|
| `id` | Identificador único de la venta. |
| `fecha` | Fecha y hora de la transacción. |
| `clienteId` | Cliente asociado (opcional). |
| `usuarioId` | Usuario que registró la venta. |
| `agregarLinea(linea)` | Añade una línea de venta. |
| `calcularSubtotal()` | Suma todos los importes de líneas. |
| `calcularIva(porcentajeIva)` | Calcula el IVA. |
| `calcularTotal(porcentajeIva)` | Calcula el total final. |
| `tieneClienteAsociado()` | Indica si la venta se ligó a un cliente. |

## 🟩 LíneaVenta
| **Atributo / Método** | **Descripción** |
|------------------------|-----------------|
| `id` | Identificador de la línea. |
| `ventaId` | Venta a la que pertenece. |
| `tipoItem` | Sesión o Producto. |
| `referenciaId` | ID del producto o sesión. |
| `cantidad` | Cantidad vendida. |
| `precioUnitario` | Precio por unidad. |
| `calcularImporte()` | Retorna cantidad × precio. |

## 🟩 Ticket
| **Atributo / Método** | **Descripción** |
|------------------------|-----------------|
| `id` | Identificador del ticket. |
| `ventaId` | Venta asociada. |
| `folio` | Folio único del ticket. |
| `emitidoEn` | Fecha y hora de emisión. |
| `generarFolio()` | Crea un folio único. |
| `esValido()` | Verifica que el ticket corresponda a una venta existente. |
