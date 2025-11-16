# CU-VEN-03 – Imprimir ticket

**Actor principal:** Cajero  

## Propósito
Generar e imprimir un ticket con la información de la sesión y la venta de productos.

## Precondiciones
- Existe una venta registrada y confirmada.
- El sistema tiene configurada una impresora o un generador de PDF.

## Postcondiciones
- Se genera un ticket (en papel o PDF) con el detalle de la operación.
- Opcionalmente, se almacena una copia del ticket en el sistema para futuras consultas.

## Flujo principal

1. El cajero selecciona la opción **"Imprimir ticket"** para una venta específica.
2. El sistema obtiene los datos de la sesión, del cliente (si aplica) y de la venta (productos, cantidades, totales).
3. El sistema construye el formato del ticket con base en la plantilla definida (ver `06-mock-ticket.md`).
4. El sistema envía el ticket a la impresora o genera el archivo PDF.
5. El sistema notifica al cajero que el ticket se generó correctamente.

## Flujos alternos

**A1 – Error de impresión**

4a. El sistema detecta un error al enviar el ticket a la impresora.  
4b. Muestra un mensaje indicando que se intente nuevamente o que revise la impresora.  
4c. Permite reintentar la impresión.

## Reglas de negocio relacionadas
- Formato y contenido mínimo del ticket descritos en `06-mock-ticket.md`.
