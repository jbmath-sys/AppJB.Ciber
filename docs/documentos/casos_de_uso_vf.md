## CU-01 Registrar Cliente

| Campo                                   | Descripción |
|-----------------------------------------|-------------|
| **ID**                                  | CU-01 |
| **Nombre del Caso de Uso**              | Registrar Cliente |
| **Alcance**                             | Sistema de Gestión de Ciber |
| **Nivel**                               | Usuario (meta-usuario) |
| **Actor Principal**                     | Administrador |
| **Stakeholders e Intereses**            | El administrador desea registrar nuevos clientes para mantener actualizada la base de datos y facilitar el seguimiento de consumo. |
| **Precondiciones**                      | El administrador debe estar autenticado en el sistema. |
| **Éxito Garantizado (Postcondiciones)** | El nuevo cliente queda registrado correctamente en la base de datos. |
| **Principal Escenario de Éxito**        | <ol><li>El administrador selecciona la opción “Registrar cliente”.</li><li>El sistema muestra un formulario de registro.</li><li>El administrador introduce los datos del cliente.</li><li>El administrador confirma el registro.</li><li>El sistema guarda la información y confirma la operación.</li></ol> |
| **Extensiones**                         | Si los datos están incompletos o incorrectos, el sistema muestra un mensaje de error. |


## CU-02 Eliminar Cliente

| Campo                                   | Descripción |
|-----------------------------------------|-------------|
| **ID**                                  | CU-02 |
| **Nombre del Caso de Uso**              | Eliminar Cliente |
| **Alcance**                             | Sistema de Gestión de Ciber |
| **Nivel**                               | Usuario |
| **Actor Principal**                     | Administrador |
| **Stakeholders e Intereses**            | El administrador desea eliminar registros obsoletos o inactivos para mantener limpia la base de datos. |
| **Precondiciones**                      | El cliente debe estar registrado. |
| **Éxito Garantizado (Postcondiciones)** | El registro del cliente se elimina del sistema. |
| **Principal Escenario de Éxito**        | <ol><li>El administrador selecciona “Eliminar cliente”.</li><li>El sistema muestra la lista de clientes.</li><li>El administrador selecciona al cliente a eliminar.</li><li>El sistema solicita confirmación.</li><li>El administrador confirma la eliminación.</li><li>El sistema elimina al cliente y muestra un mensaje de éxito.</li></ol> |
| **Extensiones**                         | Si el cliente tiene sesiones activas, el sistema no permite su eliminación. |


## CU-03 Consultar Historial de Cliente

| Campo                                   | Descripción |
|-----------------------------------------|-------------|
| **ID**                                  | CU-03 |
| **Nombre del Caso de Uso**              | Consultar Historial de Cliente |
| **Alcance**                             | Sistema de Gestión de Ciber |
| **Nivel**                               | Subfunción |
| **Actor Principal**                     | Administrador |
| **Stakeholders e Intereses**            | El administrador busca analizar hábitos de consumo de los clientes frecuentes. |
| **Precondiciones**                      | El cliente debe estar registrado en el sistema. |
| **Éxito Garantizado (Postcondiciones)** | El historial se muestra correctamente en pantalla. |
| **Principal Escenario de Éxito**        | <ol><li>El administrador selecciona “Consultar historial”.</li><li>El sistema muestra la lista de clientes.</li><li>El administrador elige un cliente.</li><li>El sistema muestra el historial de consumo.</li></ol> |
| **Extensiones**                         | Si no existe historial, el sistema lo indica. |


## CU-04 Iniciar Sesión de Juego

| Campo                                   | Descripción |
|-----------------------------------------|-------------|
| **ID**                                  | CU-04 |
| **Nombre del Caso de Uso**              | Iniciar Sesión de Juego |
| **Alcance**                             | Sistema de Gestión de Ciber |
| **Nivel**                               | Meta-usuario |
| **Actor Principal**                     | Cajero / Cliente |
| **Stakeholders e Intereses**            | El cliente desea acceder a una PC o consola; el cajero necesita registrar la sesión y contabilizar el tiempo de uso. |
| **Precondiciones**                      | El equipo debe estar disponible. |
| **Éxito Garantizado (Postcondiciones)** | La sesión se inicia y comienza a contabilizarse el tiempo. |
| **Principal Escenario de Éxito**        | <ol><li>El cajero selecciona “Iniciar sesión de juego”.</li><li>El sistema muestra las estaciones disponibles.</li><li>El cajero asigna al cliente una PC o consola.</li><li>El sistema inicia la sesión y registra el tiempo.</li></ol> |
| **Extensiones**                         | Si no hay equipos disponibles, el sistema muestra aviso de espera. |


## CU-05 Finalizar Sesión de Juego

| Campo                                   | Descripción |
|-----------------------------------------|-------------|
| **ID**                                  | CU-05 |
| **Nombre del Caso de Uso**              | Finalizar Sesión de Juego |
| **Alcance**                             | Sistema de Gestión de Ciber |
| **Nivel**                               | Meta-usuario |
| **Actor Principal**                     | Cajero |
| **Stakeholders e Intereses**            | El cajero necesita cerrar correctamente las sesiones para calcular el tiempo y monto a pagar; el cliente desea pagar justo por el tiempo utilizado. |
| **Precondiciones**                      | Debe existir una sesión activa. |
| **Éxito Garantizado (Postcondiciones)** | La sesión queda finalizada, y el sistema registra el pago correspondiente. |
| **Principal Escenario de Éxito**        | <ol><li>El cajero selecciona “Finalizar sesión”.</li><li>El sistema calcula el tiempo total y el monto a pagar.</li><li>El cajero cobra al cliente.</li><li>El sistema registra el pago y cierra la sesión.</li></ol> |
| **Extensiones**                         | Si el cliente tiene saldo a favor, el sistema aplica el descuento automáticamente. |


## CU-06 Registrar Venta de Snack

| Campo                                   | Descripción |
|-----------------------------------------|-------------|
| **ID**                                  | CU-06 |
| **Nombre del Caso de Uso**              | Registrar Venta de Snack |
| **Alcance**                             | Sistema de Gestión de Ciber |
| **Nivel**                               | Subfunción |
| **Actor Principal**                     | Cajero |
| **Stakeholders e Intereses**            | El cajero desea registrar ventas de productos para mantener actualizado el inventario y la caja; el cliente recibe el producto solicitado. |
| **Precondiciones**                      | El snack debe estar disponible en inventario. |
| **Éxito Garantizado (Postcondiciones)** | El producto se descuenta del inventario y la venta queda registrada. |
| **Principal Escenario de Éxito**        | <ol><li>El cajero selecciona “Venta de snack”.</li><li>El sistema muestra el listado de productos disponibles.</li><li>El cajero elige el snack vendido.</li><li>El sistema descuenta el producto del inventario y registra el costo.</li></ol> |
| **Extensiones**                         | Si el stock es insuficiente, el sistema muestra un mensaje de advertencia. |


## CU-07 Registrar Venta de Bebida

| Campo                                   | Descripción |
|-----------------------------------------|-------------|
| **ID**                                  | CU-07 |
| **Nombre del Caso de Uso**              | Registrar Venta de Bebida |
| **Alcance**                             | Sistema de Gestión de Ciber |
| **Nivel**                               | Subfunción |
| **Actor Principal**                     | Cajero |
| **Stakeholders e Intereses**            | El cajero registra la venta para actualizar el inventario y caja; el cliente recibe la bebida solicitada. |
| **Precondiciones**                      | La bebida debe estar disponible en inventario. |
| **Éxito Garantizado (Postcondiciones)** | La venta se registra y el inventario se actualiza. |
| **Principal Escenario de Éxito**        | <ol><li>El cajero selecciona “Venta de bebida”.</li><li>El sistema muestra el listado de bebidas.</li><li>El cajero selecciona la bebida vendida.</li><li>El sistema descuenta la cantidad y registra la venta.</li></ol> |
| **Extensiones**                         | Si no hay stock, el sistema bloquea la venta y notifica la falta del producto. |


## CU-08 Registrar Impresión

| Campo                                   | Descripción |
|-----------------------------------------|-------------|
| **ID**                                  | CU-08 |
| **Nombre del Caso de Uso**              | Registrar Impresión |
| **Alcance**                             | Sistema de Gestión de Ciber |
| **Nivel**                               | Subfunción |
| **Actor Principal**                     | Cajero |
| **Stakeholders e Intereses**            | El cajero desea controlar las impresiones realizadas para registrar ingresos adicionales; el cliente paga por el servicio recibido. |
| **Precondiciones**                      | La impresora debe estar disponible y con insumos suficientes. |
| **Éxito Garantizado (Postcondiciones)** | La impresión queda registrada junto con el cobro correspondiente. |
| **Principal Escenario de Éxito**        | <ol><li>El cliente solicita una impresión.</li><li>El cajero ingresa el número de páginas.</li><li>El sistema calcula el costo.</li><li>El cajero cobra y confirma la impresión.</li></ol> |
| **Extensiones**                         | Si la impresora presenta error o falta de insumo, el sistema muestra una alerta. |


## CU-09 Aplicar Descuento

| Campo                                   | Descripción |
|-----------------------------------------|-------------|
| **ID**                                  | CU-09 |
| **Nombre del Caso de Uso**              | Aplicar Descuento |
| **Alcance**                             | Sistema de Gestión de Ciber |
| **Nivel**                               | Subfunción |
| **Actor Principal**                     | Cajero (con autorización del Administrador) |
| **Stakeholders e Intereses**            | El cajero aplica descuentos para fidelizar clientes o corregir cargos; el administrador mantiene el control mediante autorización. |
| **Precondiciones**                      | Debe existir una autorización válida del administrador. |
| **Éxito Garantizado (Postcondiciones)** | El descuento se aplica y queda registrado en el sistema. |
| **Principal Escenario de Éxito**        | <ol><li>El cajero selecciona “Aplicar descuento”.</li><li>El sistema solicita código o autorización.</li><li>El cajero ingresa el porcentaje de descuento.</li><li>El sistema recalcula el monto y guarda la operación.</li></ol> |
| **Extensiones**                         | Si no se valida la autorización, el sistema no permite aplicar el descuento. |


## CU-10 Cerrar Caja

| Campo                                   | Descripción |
|-----------------------------------------|-------------|
| **ID**                                  | CU-10 |
| **Nombre del Caso de Uso**              | Cerrar Caja |
| **Alcance**                             | Sistema de Gestión de Ciber |
| **Nivel**                               | Meta-usuario |
| **Actor Principal**                     | Cajero |
| **Stakeholders e Intereses**            | El cajero desea cerrar correctamente la jornada y registrar el balance final; el administrador usa la información para control financiero. |
| **Precondiciones**                      | Deben existir ventas y sesiones registradas. |
| **Éxito Garantizado (Postcondiciones)** | El sistema guarda el registro del cierre de caja y genera el reporte del día. |
| **Principal Escenario de Éxito**        | <ol><li>El cajero selecciona “Cerrar caja”.</li><li>El sistema muestra el resumen de ventas.</li><li>El cajero verifica el efectivo.</li><li>El sistema genera y guarda el reporte de cierre.</li></ol> |
| **Extensiones**                         | Si hay diferencia entre efectivo y sistema, se genera una alerta y se solicita revisión. |


## CU-11 Generar Reportes

| Campo                                   | Descripción |
|-----------------------------------------|-------------|
| **ID**                                  | CU-11 |
| **Nombre del Caso de Uso**              | Generar Reportes |
| **Alcance**                             | Sistema de Gestión de Ciber |
| **Nivel**                               | Meta-usuario |
| **Actor Principal**                     | Administrador |
| **Stakeholders e Intereses**            | El administrador desea obtener reportes para análisis de rendimiento, ventas y control de operaciones. |
| **Precondiciones**                      | Deben existir datos registrados. |
| **Éxito Garantizado (Postcondiciones)** | El sistema genera el reporte solicitado para su consulta o exportación. |
| **Principal Escenario de Éxito**        | <ol><li>El administrador selecciona “Generar reporte”.</li><li>El sistema solicita el tipo de reporte (ventas, sesiones, caja).</li><li>El administrador confirma.</li><li>El sistema genera el reporte y lo muestra en pantalla.</li></ol> |
| **Extensiones**                         | Si no hay datos, el sistema notifica que no se puede generar el reporte. |


## CU-12 Administrar Inventario

| Campo                                   | Descripción |
|-----------------------------------------|-------------|
| **ID**                                  | CU-12 |
| **Nombre del Caso de Uso**              | Administrar Inventario |
| **Alcance**                             | Sistema de Gestión de Ciber |
| **Nivel**                               | Meta-usuario |
| **Actor Principal**                     | Administrador |
| **Stakeholders e Intereses**            | El administrador necesita mantener actualizado el inventario para garantizar la disponibilidad de productos y servicios. |
| **Precondiciones**                      | El administrador debe estar autenticado. |
| **Éxito Garantizado (Postcondiciones)** | El inventario se actualiza correctamente en la base de datos. |
| **Principal Escenario de Éxito**        | <ol><li>El administrador selecciona “Inventario”.</li><li>El sistema muestra la lista de productos registrados.</li><li>El administrador agrega, edita o elimina productos.</li><li>El sistema guarda los cambios y actualiza los datos.</li></ol> |
| **Extensiones**                         | Si un producto tiene ventas activas, el sistema bloquea su eliminación. |
