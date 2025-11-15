# CU-00: Iniciar Sesión (Administrador / Cajero)

**Actor principal:** Administrador o Cajero  
**Tipo:** Soporte (precondición para CU-01…CU-05)  
**Prioridad:** Crítica  
**Iteración:** I1 – Núcleo Cliente + Sesiones  

---

## 1. Objetivo
Permitir que un usuario autorizado (Administrador o Cajero) acceda al sistema mediante credenciales válidas, estableciendo su **rol y permisos** para operar funciones de caja, clientes y sesiones.

---

## 2. Descripción breve
El actor ingresa **usuario** y **contraseña**.  
El sistema valida credenciales, verifica estado del usuario (activo/no bloqueado), determina **rol** y crea una **sesión de aplicación** con tiempo de expiración.  
Si falla, informa el motivo (credenciales inválidas, bloqueado, sin permisos).

---

## 3. Precondiciones
- El sistema está en línea y la conexión a base de datos es funcional.  
- El usuario existe, está **Activo** y cuenta con **rol** asignado (Administrador o Cajero).  
- La política de contraseñas y bloqueo está configurada (intentos máximos 3 y tiempo de bloqueo 5 minutos).

---

## 4. Flujo principal

| Paso | Actor / Sistema | Descripción |
|---|---|---|
| 1 | Actor | Abre la pantalla **Iniciar Sesión**. |
| 2 | Sistema | Presenta campos *Usuario*, *Contraseña*. |
| 3 | Actor | Ingresa credenciales y confirma **Acceder**. |
| 4 | Sistema | Valida usuario/contraseña (hash), estado **Activo** y **no bloqueado**. |
| 5 | Sistema | Determina **Rol** y **Permisos**; crea **SesiónApp** con expiración e ID. |
| 6 | Sistema | Redirige a **Elegir consola/pc** (rol Cajero) o **Panel Admin** (rol Administrador). |
| 7 | Actor | Visualiza acceso concedido y continúa con operaciones. |

---

## 5. Flujos alternos / excepciones

| Código | Descripción |
|---|---|
| **A1 – Credenciales inválidas** | Muestra *“Usuario o contraseña incorrectos”* e incrementa contador de intentos fallidos. |
| **A2 – Usuario bloqueado** | Si supera **3** intentos fallidos, marca **Bloqueado** (por 5 minutos o hasta desbloqueo admin). |
| **A3 – Usuario inactivo** | Si `Activo = false`, muestra *“Usuario inactivo, contacte al administrador”*. |
| **A4 – Error de conexión** | Muestra *“No fue posible validar credenciales. Intente más tarde”*. |
| **A5 – Cambio obligatorio de contraseña** | Si es primer login/expiración, redirige a **Cambiar Contraseña** antes de acceder. |

---

## 6. Inclusiones (include)
- **CU-___: Cerrar Sesión** (logout por menú o inactividad).  
- **CU-___: Recuperar/Restablecer Contraseña** (si aplica).

---

## 7. Postcondiciones
- Se crea una **sesión de aplicación** con: `UsuarioId`, `Rol`, `HoraInicio`, `ExpiraEn`.  
- El sistema habilita menús y acciones según **permisos del rol**.  
- Se registra en bitácora **login exitoso** (usuario, IP/equipo, fecha/hora).

---

## 8. Reglas de negocio relacionadas
- **RB1:** Política de contraseña (longitud 10 caracteres, minusculas, mayusculas y numeros).  
- **RB2:** **Bloqueo** tras `3` intentos fallidos durante `5` minutos.  
- **RB3:** **Timeout** de sesión por inactividad es de 15 min.  
- **RB4:** Auditoría obligatoria de **intentos fallidos** y **logins**.  

---

## 9. Datos de prueba sugeridos

| Caso | Usuario | Contraseña | 2FA | Estado esperado |
|---|---|---|---|---|
| 1 | admin | Correcta | Válido | Acceso a Panel Admin |
| 2 | cajero01 | Correcta | — | Acceso a Caja |
| 3 | cajero01 | Incorrecta | — | Error A1; +1 intento fallido |
| 4 | cajero01 | Incorrecta (N veces) | — | A2: Usuario bloqueado |
| 5 | cajero02(inactivo) | Correcta | — | A3: Usuario inactivo |

---

## 10. Diagramas relacionados
- `actividad-login.puml`  
- `secuencia-login.puml`  

---

## 11. Notas técnicas
- **Modelo sugerido**  
  - `Usuario(Id, Username, Hash, Activo, Rol, IntentosFallidos, BloqueadoHasta, RequiereCambioPwd)`  
  - `SesionApp(Id, UsuarioId, Inicio, Expira, UltimoMovimiento, Estado)`  
- **Seguridad**  
  - Contraseñas con **hash + salt** (p. ej., PBKDF2/Argon2).  
  - Almacenar solo **hash**; nunca texto plano.  
  - Registrar `IP/host` en bitácora de acceso.  
- **UX Mensajes**  
  - 🟢 *Bienvenido, {Usuario}.*  
  - ⚠️ *Usuario o contraseña incorrectos.*  
  - 🔒 *Usuario bloqueado por seguridad.*  
  - 🔁 *Debe cambiar su contraseña para continuar.*  

---

**Autor:** Lic. en Matemáticas Juan Bernardo Lopez Acosta — *Sistema de Gestión de Ciber (AppJB.Ciber)*  
**Fecha de redacción:** 22/oct/2025  
**Versión:** v1.0
