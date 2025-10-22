# CU-01: Registrar Cliente

**Actor principal:** Administrador (o Cajero autorizado)  
**Tipo:** Primario  
**Prioridad:** Alta  
**Iteración:** I1 – Núcleo Cliente + Sesiones  

---

## 1. Objetivo
Permitir al administrador o cajero registrar un nuevo cliente en el sistema con sus datos básicos, para identificarlo en futuras sesiones, ventas o promociones frecuentes.

---

## 2. Descripción breve
El actor ingresa los datos del cliente (nombre, teléfono, correo opcional y foto opcional).  
El sistema valida que el nombre no esté vacío y que el número telefónico no esté registrado previamente.  
Si la validación es correcta, guarda los datos en la base y confirma el registro.

---

## 3. Precondiciones
- El actor ha iniciado sesión en el sistema.  
- La conexión con la base de datos está activa.  
- El actor tiene permisos para registrar clientes.

---

## 4. Flujo principal

| Paso | Actor / Sistema | Descripción |
|------|------------------|--------------|
| 1 | Actor | Selecciona la opción **Registrar Cliente** desde el menú principal. |
| 2 | Sistema | Muestra el formulario de registro con campos: *Nombre*, *Teléfono*, *Correo*, *Foto*. |
| 3 | Actor | Ingresa los datos solicitados. |
| 4 | Sistema | Valida que los campos obligatorios estén completos y que el teléfono no exista previamente. |
| 5 | Sistema | Crea un nuevo registro en la tabla `Cliente` con estado activo. |
| 6 | Sistema | Muestra mensaje de confirmación y genera un identificador único (IdCliente). |
| 7 | Actor | Visualiza mensaje de éxito y puede proceder a iniciar sesión de juego o registrar otro cliente. |

---

## 5. Flujos alternos / extensiones

| Código | Descripción |
|---------|--------------|
| **A1** | **Teléfono duplicado:** Si el número ya está registrado, el sistema muestra mensaje *“Cliente existente”* y ofrece opción de buscarlo. |
| **A2** | **Campos incompletos:** Si faltan datos obligatorios, muestra advertencia *“Complete los campos requeridos”*. |
| **A3** | **Error de conexión:** Si hay problema con la base, muestra *“No se pudo guardar el cliente. Intente más tarde”*. |
| **A4 (Extend)** | **Registrar como invitado:** Si no se proporciona teléfono ni correo, el sistema marca `esFrecuente=false` y `tipo=Invitado`. |

---

## 6. Inclusiones (include)
- CU-00 Iniciar Sesión (precondición).  
- CU-02 Iniciar Sesión de Juego (posible flujo posterior).

---

## 7. Postcondiciones
- Se crea un registro válido en la entidad `Cliente`.  
- El sistema puede listar el nuevo cliente en las búsquedas.  
- Si se trata de un invitado, queda registrado con datos mínimos.

---

## 8. Reglas de negocio relacionadas
- **RB1:** Un *Invitado* es un cliente sin teléfono y con `esFrecuente=false`.  
- **RB2:** El *Nombre* es obligatorio.  
- **RB3:** El *Teléfono* es único en el sistema.  
- **RB4:** El registro se marca con fecha de alta (`FechaRegistro`).

---

## 9. Datos de prueba sugeridos

| Nombre | Teléfono | Correo | Resultado esperado |
|---------|-----------|--------|--------------------|
| Ana Torres | 4921012233 | ana@gmail.com | Registro exitoso |
| Luis Pérez | 4921012233 | — | Error (teléfono duplicado) |
| Invitado — | — | — | Registro exitoso como cliente tipo *Invitado* |

---

## 10. Diagramas relacionados
- `actividad-registrar-cliente.puml`  
- `dominio-v1.puml` (entidades *Cliente* y *Sesion* conectadas)  

---

## 11. Notas técnicas
- **Entidad:** `Cliente(Id, Nombre, Telefono?, Correo?, EsFrecuente, FechaRegistro, Tipo)`  
- **Validaciones UI:** campos requeridos, formato de teléfono, correo válido.  
- **Mensajes UX:**  
  - ✔️ *Cliente registrado correctamente.*  
  - ⚠️ *El número ingresado ya existe.*  
  - ❌ *Error al guardar, intente más tarde.*

---

**Autor:** Profe JB — *Sistema de Gestión de Ciber (AppJB.Ciber)*  
**Fecha de redacción:** 18/oct/2025  
**Versión:** v1.0  
