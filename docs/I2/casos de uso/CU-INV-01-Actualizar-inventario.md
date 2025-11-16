# CU-INV-01 – Actualizar inventario

**Actor principal:** Sistema  
**Actor secundario:** Administrador (consulta y mantiene configuraciones)

## Propósito
Actualizar el inventario de productos como consecuencia de una venta, entrada de mercancía u otros movimientos.

## Precondiciones
- Existe una venta confirmada o un movimiento de inventario registrado.
- Cada producto tiene un registro de existencias.

## Postcondiciones
- El stock de cada producto se actualiza.
- Se registra un movimiento de inventario para trazabilidad.

## Flujo principal (caso disparado por una venta)

1. El sistema recibe la confirmación de una venta (desde **CU-VEN-01**).
2. Para cada producto en el detalle de la venta:
   1. Consulta el stock actual.
   2. Resta la cantidad vendida.
   3. Actualiza el stock en la tabla de existencias.
   4. Registra un movimiento de inventario de tipo "Salida".
3. Si algún producto queda por debajo del punto de reorden, el sistema lo marca como "bajo stock" para reportes futuros.

## Flujos alternos

**A1 – Stock negativo**

2b1. Si al restar la cantidad la existencia quedara negativa, el sistema registra un error en bitácora y evita la actualización.  
2b2. Se genera una alerta para que el administrador revise el caso.

## Reglas de negocio relacionadas
- Definición de stock mínimo y punto de reorden en `04-modelo-datos.md` y `05-reglas-negocio.md`.
