### Reglas de Negocio 

Después de identificar los actores y definir los conceptos clave del sistema, es necesario establecer un conjunto de reglas que guíen su comportamiento.  
Las **reglas de negocio** representan las políticas, restricciones y condiciones que deben cumplirse para garantizar la correcta operación del sistema de gestión del ciber.  
Estas reglas permiten mantener la coherencia de la información, estandarizar procesos como el registro de sesiones, ventas o descuentos, y asegurar que las decisiones del sistema se alineen con los objetivos del negocio.

Las reglas de negocio seran:

| ID | Regla de Negocio | Descripción |
|----|------------------|--------------|
| **RN-01** | IVA incluido | Todos los precios visibles incluyen IVA del 16%. |
| **RN-02** | Redondeo de precios | Los montos totales se redondean al múltiplo de $0.50 más cercano. |
| **RN-03** | Autorización de descuentos | Solo el Administrador puede aprobar o aplicar descuentos a clientes o productos. |
| **RN-04** | Expiración de promociones | Toda promoción debe tener una fecha de inicio y fin. Una vez vencida, el sistema la desactiva automáticamente. |
| **RN-05** | Registro de sesiones | Toda sesión de PC o consola debe registrarse con hora de inicio y fin para calcular el monto. |
| **RN-06** | Impresión obligatoria | Cada venta o servicio debe generar un ticket impreso o digital. |
| **RN-07** | Control de inventario | El sistema debe disminuir automáticamente la cantidad disponible de cada producto vendido. |
| **RN-08** | Cierre de caja diario | No se puede iniciar un nuevo día sin haber cerrado la caja anterior. |
| **RN-09** | Política de reembolso | Solo el Administrador puede autorizar reembolsos o cancelaciones. |
| **RN-10** | Seguridad de acceso | Los usuarios deben ingresar con credenciales válidas para acceder al sistema. |

Con la definición de estas reglas de negocio se establece una base sólida para el desarrollo del sistema.  
Cada regla busca reflejar las políticas reales del negocio y garantizar que las operaciones del sistema —como la venta, el registro de sesiones, los descuentos y el control de inventario— se realicen de manera uniforme y confiable.  
Estas reglas servirán como referencia en las siguientes iteraciones, especialmente al diseñar los casos de uso y modelar la lógica del dominio.

---
