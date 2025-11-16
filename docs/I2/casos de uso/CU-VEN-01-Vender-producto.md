# CU-VEN-01 – Vender producto

**Actor principal:** Cajero  
**Actores secundarios:** Administrador (configura productos y precios)  

## Propósito
Registrar la venta de uno o varios productos (snacks, bebidas, etc.) asociados a una sesión o cliente, calculando el importe correspondiente.

## Precondiciones
- El cajero ha iniciado sesión en el sistema.
- Existen productos registrados y con stock disponible.
- Existe una sesión activa o un cliente seleccionado (según diseño del sistema).

## Postcondiciones
- La venta queda registrada en el sistema.
- El detalle de la venta queda disponible para generar ticket.
- El inventario se actualiza (mediante el caso de uso **CU-INV-01 – Actualizar inventario**).

## Flujo principal

1. El cajero selecciona el cliente o la sesión de juego asociada a la venta.
2. El sistema muestra la lista de productos disponibles con su precio y stock.
3. El cajero selecciona uno o más productos e indica la cantidad de cada uno.
4. El sistema valida que la cantidad solicitada no supere el stock disponible.
5. El sistema incluye el caso de uso **CU-COM-01 – Calcular total** para obtener subtotal, IVA y total.
6. El cajero revisa el resumen de la venta (productos, cantidades, subtotal, IVA, total).
7. El cajero confirma la venta.
8. El sistema registra la venta y el detalle de productos.
9. El sistema incluye el caso de uso **CU-INV-01 – Actualizar inventario** para descontar el stock.
10. El sistema deja disponible la información para **CU-VEN-03 – Imprimir ticket**.

## Flujos alternos

**A1 – Stock insuficiente**

4a. El sistema detecta que la cantidad de uno o más productos supera el stock disponible.  
4b. El sistema muestra un mensaje de error indicando el producto afectado y el stock actual.  
4c. El cajero ajusta la cantidad o elimina el producto.  
4d. Vuelve al paso 3 del flujo principal.

**A2 – Cancelación de la venta**

7a. El cajero decide cancelar la venta.  
7b. El sistema descarta los datos capturados y retorna a la pantalla principal de ventas.  
7c. No se registra ninguna venta.

## Reglas de negocio relacionadas
- Ver documento `05-reglas-negocio.md` en la raíz de la iteración 2.
