# EP-001 Organizacion y Personas (MOD-001)

**Objetivo.** Una empresa registra su organizacion (una razon social) con sus sucursales y unidades, invita y gestiona el ciclo de vida completo de sus usuarios sobre el catalogo de los 12 roles estandar, y opera con las reglas minimas de continuidad y separacion de funciones que el resto de los modulos necesitan para funcionar.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R1 | 14 | 47 | 47 | 0 | [MOD-001](../../03_modulos/MOD-001_ficha.md) |

**Notas de la epica.**

- MOD-001 no es propietaria de ningun OBL-ID; solo colabora en OBL-AMB-01 (propietaria MOD-004), citado unicamente en HU-001-01 porque la ficha define la ficha de organizacion como su evidencia esperada.
- Los datos relevantes para las exclusiones del Art. 3 (sector o giro economico, numero de empleados, paises donde opera) no forman un conjunto separado en la ficha: son los mismos campos minimos de D.1 que ya cubre HU-001-01; la conclusion sobre exclusiones la entrega MOD-004, nunca este modulo.
- Se incluyo una HU de exportacion simple del listado de usuarios y roles (HU-001-14) sin mecanismo de hash, apoyada en la propia justificacion de la fila Exportacion firmada con verificacion de integridad del listado de usuarios de la tabla Q, que describe esa version simple como la cobertura parcial mientras se construye el mecanismo de hash compartido con MOD-019; la version CON hash es SHOULD HAVE y queda fuera de esta epica.
- El Auditor externo y el Asesor externo invitado se pueden invitar con el mismo mecanismo generico de HU-001-05 (invitacion con vigencia de 30 dias); el acotamiento automatico a una ventana de auditoria o de caso distinta de ese plazo generico es la fila SHOULD HAVE Auditor externo con acceso temporal por invitacion de la tabla Q y queda fuera de esta epica, consistente con los huecos que documenta 04_secciones/11_roles_y_permisos.md en 11.5.1 y 11.5.2.
- Se excluyeron explicitamente, por indicacion del encargo y por ser SHOULD HAVE en la tabla Q de la ficha: roles personalizados (seccion D.3), bloqueo automatico configurable de separacion de funciones mas alla de la advertencia visible de autorrevision, organigrama visual grafico, y toda gestion de grupo multi-sociedad.
- El umbral de 50 empleados y el plazo de 30 dias de vigencia de la invitacion son opinion de producto sin respaldo legal expreso, pendientes de validacion (PP-PROD-04 y PP-PROD-05 de 24_preguntas_pendientes.md); se usaron como valores de referencia en los criterios de aceptacion tal como los propone la ficha.
- La fila de permisos Comentar en una solicitud de alta o cambio de rol y la distincion entre solicitar y ejecutar que hace la seccion C para el Delegado sin rol Administrador se cubrieron como criterios dentro de HU-001-05 y HU-001-08, sin crear una entidad Solicitud separada, porque la seccion F de la ficha no define estados ni campos propios para esa solicitud.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-001-01 | Registrar y mantener los datos basicos de la organizacion | Administrador de la organizacion | 5 | R1 | 1 | - |
| HU-001-02 | Gestionar las sucursales de la organizacion | Administrador de la organizacion | 3 | R1 | 1 | HU-001-01 |
| HU-001-03 | Gestionar el catalogo de unidades o departamentos | Administrador de la organizacion | 3 | R1 | 2 | HU-001-01 |
| HU-001-04 | Consultar el catalogo de los 12 roles estandar | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 2 | R1 | 2 | HU-001-01 |
| HU-001-05 | Invitar usuarios y gestionar el ciclo de la invitacion | Administrador de la organizacion | 5 | R1 | 2 | HU-001-01, HU-001-04, MOD-021, MOD-022 |
| HU-001-06 | Suspender y reactivar usuarios | Administrador de la organizacion | 5 | R1 | 2 | HU-001-05, MOD-022 |
| HU-001-07 | Dar de baja usuarios con reemplazo de rol critico | Administrador de la organizacion | 5 | R1 | 3 | HU-001-05, HU-001-06, MOD-022 |
| HU-001-08 | Editar los datos y el rol de un usuario | Administrador de la organizacion | 5 | R1 | 2 | HU-001-04, HU-001-05 |
| HU-001-09 | Actualizar el contacto ARCO-POL derivado al cambiar su titular | Administrador de la organizacion | 3 | R1 | 3 | HU-001-08, MOD-021 |
| HU-001-10 | Alertar y registrar la decision sobre el umbral de separacion de funciones | Administrador de la organizacion | 3 | R1 | 3 | HU-001-01, HU-001-08, MOD-022 |
| HU-001-11 | Alertar cuando ningun usuario activo tiene un rol critico | Administrador de la organizacion | 2 | R1 | 3 | HU-001-04, HU-001-07, MOD-022 |
| HU-001-12 | Alertar sobre estructura sin actualizar y registrar la revision de accesos | Responsable de Seguridad / IT | 2 | R1 | 3 | HU-001-01, HU-001-08, MOD-022 |
| HU-001-13 | Crear una tarea de revision al declarar operacion fuera de El Salvador | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 2 | R1 | 3 | HU-001-01, HU-001-02, MOD-021 |
| HU-001-14 | Exportar el listado de usuarios y roles vigentes | Auditor (interno) | 2 | R1 | 3 | HU-001-05, HU-001-08 |

## Historias

### HU-001-01. Registrar y mantener los datos basicos de la organizacion

**Como** Administrador de la organizacion, **quiero** registrar y mantener actualizados los datos basicos de mi organizacion (razon social, identificacion tributaria, sector o giro economico, numero de empleados, paises donde opera, direccion y sucursales iniciales), **para** que el resto del sistema tenga una identidad de organizacion confiable desde la cual operar y que quede constancia de la ficha de organizacion que la evaluacion del ambito de aplicacion de la ley necesita como evidencia.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 1 | Si |

- Fundamento: OBL-AMB-01 (Art. 2 inc. 1, Ley para la Proteccion de Datos Personales)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que la organizacion esta en estado BORRADOR, cuando el Administrador completa Razon social, Identificacion tributaria (NIT/NRC), Sector o giro economico, Numero de empleados y al menos un pais en Paises donde opera, entonces el sistema cambia el estado de la organizacion a ACTIVA y registra el evento organizacion lista con fecha y hora.
2. Dado que el Administrador intenta guardar la organizacion sin haber completado Razon social, Identificacion tributaria, Sector o giro economico, Numero de empleados o Paises donde opera, cuando confirma el guardado, entonces el sistema rechaza el avance a ACTIVA, muestra que campos faltan y la organizacion permanece en BORRADOR.
3. Dado que el Administrador ingresa una Razon social o una Identificacion tributaria ya registrada por otra cuenta dentro del sistema, cuando intenta guardarla, entonces el sistema rechaza el guardado por duplicidad y muestra el error correspondiente.
4. Dado que el pais El Salvador viene preseleccionado en Paises donde opera, cuando el Administrador intenta quitarlo de la lista, entonces el sistema no permite removerlo.
5. Dado que la organizacion esta en estado ACTIVA, cuando el Administrador edita cualquier campo de los datos basicos, entonces el sistema conserva el estado ACTIVA, guarda el valor anterior y el valor nuevo, y registra en el historial quien hizo el cambio y cuando.
6. Dado que el Administrador adjunta un documento opcional de respaldo (por ejemplo acta de constitucion o poder del representante legal), cuando lo sube, entonces el sistema lo guarda como anexo de la organizacion sin exigirlo como campo obligatorio.
7. Dado que la organizacion completa los datos de Sector o giro economico y Paises donde opera, cuando el Administrador guarda el formulario, entonces el sistema no muestra ninguna conclusion sobre si la Ley para la Proteccion de Datos Personales aplica a la organizacion ni ningun texto de exclusion del Art. 3, porque esa determinacion es exclusiva del Diagnostico de Cumplimiento.
8. Dado que han pasado 3 dias desde el alta de la organizacion sin completar los campos minimos, cuando se cumple ese plazo, entonces el sistema genera la alerta Organizacion incompleta de nivel WARNING hacia el Administrador, con un segundo recordatorio a los 7 dias, y la alerta se apaga cuando la organizacion pasa a ACTIVA.

**Reglas de negocio**

- La organizacion pasa de BORRADOR a ACTIVA solo cuando estan presentes razon social, NIT/NRC, sector, pais y numero de empleados.
- El Salvador queda preseleccionado y no removible en Paises donde opera.
- Los datos societarios (razon social, NIT, sucursales) no son datos personales; los datos personales viven unicamente en el modulo de usuarios.
- Solo el Administrador puede crear o modificar los datos societarios.

**Fuera de alcance**

- Determinar si la LPDP aplica a la organizacion o si corresponde alguna exclusion del Art. 3 (lo hace MOD-004)
- Gestion de grupos multi-sociedad con varias razones sociales (fuera del MVP)

- Referencia: MOD-001 secciones D.1, F.1, F.3, G fila 1, H, I (Organizacion incompleta), J, R.1
- Notas: El alta inicial tipicamente se dispara desde el asistente de MOD-003 Onboarding, pero la entidad Organizacion, sus validaciones y su transicion BORRADOR a ACTIVA son propiedad de MOD-001.

### HU-001-02. Gestionar las sucursales de la organizacion

**Como** Administrador de la organizacion, **quiero** dar de alta, archivar y reactivar las sucursales de mi organizacion, **para** reflejar donde opera mi empresa y poder asociar responsables y tratamientos a cada sede.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 1 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-001-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que la organizacion esta en estado ACTIVA o BORRADOR, cuando el Administrador agrega una sucursal con nombre, entonces el sistema la crea en estado ACTIVA y la incluye en el listado de sucursales activas.
2. Dado que el Administrador intenta agregar una sucursal sin nombre, cuando confirma el guardado, entonces el sistema rechaza el guardado y exige el campo Nombre.
3. Dado que una sucursal esta en estado ACTIVA, cuando el Administrador la archiva, entonces el sistema la pasa a estado ARCHIVADA, deja de mostrarla en los listados activos y conserva su historial.
4. Dado que la sucursal que se intenta archivar es la unica registrada y existen tratamientos activos que la referencian desde el modulo de tratamientos, cuando el Administrador confirma el archivado, entonces el sistema muestra una advertencia de que existen tratamientos que la referencian, pero permite continuar porque esta validacion es una advertencia y no un bloqueo automatico.
5. Dado que una sucursal esta en estado ARCHIVADA, cuando el Administrador la reactiva, entonces el sistema la regresa a estado ACTIVA y vuelve a mostrarla en los listados activos, sin perder su historial previo.
6. Dado que el Administrador agrega o edita una sucursal con un pais distinto a El Salvador, cuando guarda el cambio, entonces el sistema registra el evento en el historial de la organizacion con el campo, el valor anterior, el valor nuevo, quien lo hizo y cuando.

**Reglas de negocio**

- El MVP soporta varias sucursales de una misma razon social, nunca varias razones sociales.
- Archivar o reactivar una sucursal nunca elimina su historial.
- Solo el Administrador puede crear, archivar o reactivar sucursales.

**Fuera de alcance**

- Bloquear automaticamente el archivado de una sucursal con tratamientos activos (la ficha lo define como advertencia, no como bloqueo)
- Gestion de sucursales de una sociedad distinta (multi-empresa)

- Referencia: MOD-001 secciones D.1 (Sucursales), F.1, F.3, R.2

### HU-001-03. Gestionar el catalogo de unidades o departamentos

**Como** Administrador de la organizacion, **quiero** definir las unidades o departamentos de mi organizacion y asignarles un responsable por defecto, **para** poder organizar el trabajo y asignar tareas por area desde el primer dia.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 2 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-001-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que la organizacion existe, cuando el Administrador crea una unidad con nombre y area funcional del catalogo (RRHH, Marketing, TI, Legal/Compliance, Operaciones, Finanzas, Atencion al cliente u Otro), entonces el sistema la agrega al catalogo de unidades de la organizacion.
2. Dado que el Administrador intenta crear una unidad sin nombre, cuando confirma el guardado, entonces el sistema rechaza el guardado y exige el campo Nombre.
3. Dado que el Administrador quiere asignar un Responsable por defecto a una unidad, cuando selecciona una persona que aun no ha sido invitada al sistema, entonces el sistema no permite seleccionarla porque el responsable debe ser un usuario ya invitado.
4. Dado que no existia ninguna unidad registrada, cuando el Administrador registra la primera unidad, entonces el sistema habilita el selector de area en la pantalla de invitar usuarios, que antes solo permitia invitar sin area asignada.
5. Dado que una unidad ya tiene usuarios asociados en su area, cuando el Administrador edita el nombre o el area funcional de esa unidad, entonces el sistema conserva la asociacion existente y registra el cambio en el historial con valor anterior y valor nuevo.

**Reglas de negocio**

- El area funcional de cada unidad se elige del catalogo fijo (RRHH, Marketing, TI, Legal/Compliance, Operaciones, Finanzas, Atencion al cliente, Otro).
- El responsable por defecto de una unidad debe ser un usuario ya invitado.
- Registrar unidades es opcional en el alta pero se recomienda antes de invitar usuarios.

**Fuera de alcance**

- Organigrama visual grafico (COULD HAVE, fuera del MVP)

- Referencia: MOD-001 secciones D.1 (Unidades o departamentos), G fila 7

### HU-001-04. Consultar el catalogo de los 12 roles estandar

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** consultar el catalogo de los 12 roles estandar disponibles en mi organizacion, incluyendo quienes los ocupan hoy, **para** saber a quien puedo asignar las tareas que la ley me atribuye y a quien escalar un caso.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 2 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-001-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que la organizacion fue creada, cuando cualquier usuario con permiso de ver el catalogo de roles lo abre, entonces el sistema muestra los 12 roles estandar (Administrador de la organizacion, Delegado de Proteccion de Datos o Responsable interno, Responsable ARCO-POL o Responsable del tramite, Responsable Legal o Compliance, Responsable de Seguridad o IT, Responsable de area, Aprobador, Auditor interno, Auditor externo invitado, Usuario de consulta o Colaborador, Titular formulario externo, Asesor externo invitado) disponibles desde el alta.
2. Dado que el catalogo de roles se muestra, cuando el Delegado lo consulta, entonces el sistema muestra, para cada rol, que usuarios activos lo tienen asignado actualmente.
3. Dado que la reforma 659 puede cambiar de estado ACTUAL a FUTURO, cuando el Delegado consulta el rol de Delegado de Proteccion de Datos, entonces el sistema muestra ambas etiquetas (Delegado de Proteccion de Datos y Responsable interno) como dos nombres visibles de un mismo rol configurable.
4. Dado que Administrador de la organizacion, Delegado de Proteccion de Datos/Responsable interno y Responsable de Seguridad/IT estan marcados como roles criticos, cuando se muestra el catalogo, entonces el sistema identifica visualmente cuales de los 12 roles son criticos.
5. Dado que el MVP no incluye roles personalizados, cuando un Administrador busca una opcion para crear o editar los permisos de uno de los 12 roles estandar, entonces el sistema no ofrece ninguna accion de edicion de permisos sobre el catalogo estandar.
6. Dado que un Usuario de consulta / Colaborador abre el catalogo de roles, cuando intenta ver el listado completo de usuarios por rol, entonces el sistema le deniega esa vista y solo le muestra su propio rol y su propio equipo.

**Reglas de negocio**

- El catalogo de los 12 roles estandar es fijo y se siembra automaticamente al crear la organizacion.
- Los roles Administrador de la organizacion, Delegado/Responsable interno y Responsable de Seguridad/IT se marcan como criticos para las alertas y bloqueos de continuidad.
- El rol Delegado de Proteccion de Datos y el rol Responsable interno son la misma entidad de rol con dos etiquetas segun el estado de la reforma 659.

**Fuera de alcance**

- Creacion de roles personalizados con permisos granulares (SHOULD HAVE, fuera del MVP)

- Requiere contenido: Descripcion breve de cada uno de los 12 roles estandar para mostrar en el catalogo (la ficha solo desarrolla el texto de ayuda general de Rol y el especifico del Delegado/Responsable interno en la seccion R)
- Referencia: MOD-001 secciones B, C, nota final; R.3 y R.6

### HU-001-05. Invitar usuarios y gestionar el ciclo de la invitacion

**Como** Administrador de la organizacion, **quiero** invitar usuarios a mi organizacion asignandoles al menos un rol, y gestionar la aceptacion, el vencimiento y el reenvio de esa invitacion, **para** dar acceso controlado al sistema a las personas de mi equipo desde el primer dia.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 2 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-001-01, HU-001-04
- Modulos requeridos: MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que el Administrador invita a un usuario con un correo electronico valido y no duplicado dentro de la cuenta y al menos un rol seleccionado del catalogo de 12 roles estandar, cuando confirma la invitacion, entonces el sistema crea el usuario en estado INVITADO, envia la notificacion de invitacion y crea la tarea Completar perfil para ese usuario.
2. Dado que el Administrador intenta invitar a un usuario con un correo ya registrado en la cuenta o sin seleccionar ningun rol, cuando confirma la invitacion, entonces el sistema rechaza la invitacion y muestra el error correspondiente.
3. Dado que un usuario esta en estado INVITADO, cuando usa el enlace de invitacion vigente y confirma la aceptacion, entonces el sistema cambia su estado a ACTIVO y registra el evento usuario activado con fecha y hora.
4. Dado que un usuario en estado INVITADO no acepta la invitacion dentro de los 30 dias siguientes, cuando se cumple ese plazo, entonces el sistema cambia su estado a EXPIRADO y genera la alerta Invitacion pendiente de aceptar de nivel INFO hacia el Administrador a los 15 y a los 30 dias.
5. Dado que un usuario esta en estado EXPIRADO, cuando el Administrador reenvia la invitacion, entonces el sistema genera un nuevo enlace, reinicia el plazo de 30 dias y regresa al usuario a estado INVITADO.
6. Dado que el Delegado de Proteccion de Datos no tiene ademas asignado el rol Administrador de la organizacion, cuando intenta invitar directamente a un usuario, entonces el sistema le deniega la ejecucion directa y solo le permite registrar una solicitud de alta para que el Administrador la ejecute.
7. Dado que existe una solicitud de alta de usuario pendiente, cuando Administrador, Delegado, Responsable ARCO-POL, Responsable Legal/Compliance, Responsable de Seguridad/IT, Responsable de area o Aprobador la consultan, entonces el sistema les permite comentarla, y a Auditor interno, Auditor externo, Usuario de consulta y Titular no les permite comentarla.
8. Dado que la empresa desactivo el envio de la notificacion de bienvenida, cuando el Administrador invita a un usuario, entonces el sistema crea igualmente el usuario en estado INVITADO y la tarea Completar perfil, pero no envia la notificacion de bienvenida.

**Reglas de negocio**

- El alta de usuario exige correo valido y no duplicado, y al menos un rol.
- La invitacion vence a los 30 dias; el Administrador puede reenviarla desde EXPIRADO.
- El Delegado o Responsable interno solo puede invitar directamente si ademas tiene asignado el rol Administrador; si no, solo puede solicitar el alta.
- Dar de baja no reasigna ni elimina identidades; este flujo solo cubre invitar y activar.

**Fuera de alcance**

- Mecanica de autenticacion e inicio de sesion del enlace de invitacion (EP-000)
- Acceso temporal acotado a una ventana de auditoria distinta del plazo generico de 30 dias para Auditor externo o Asesor externo invitado (SHOULD HAVE)

- Preguntas pendientes relacionadas: PP-PROD-05
- Referencia: MOD-001 secciones D.2, F.2, F.3, G fila 2, I (Invitacion pendiente de aceptar), C (Crear/invitar usuario, Comentar), R.5
- Notas: La aceptacion de la invitacion por parte del usuario invitado se describe aqui solo como transicion de estado; el mecanismo de autenticacion del enlace pertenece a EP-000.

### HU-001-06. Suspender y reactivar usuarios

**Como** Administrador de la organizacion, **quiero** suspender temporalmente el acceso de un usuario declarando un motivo, y reactivarlo cuando corresponda, **para** bloquear el acceso de alguien sin perder su historial ni su identidad dentro del sistema.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 2 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-001-05
- Modulos requeridos: MOD-022

**Criterios de aceptacion**

1. Dado que un usuario esta en estado ACTIVO, cuando el Administrador lo suspende declarando un motivo, entonces el sistema cambia su estado a SUSPENDIDO, bloquea su acceso de inmediato y registra el motivo, quien lo hizo y cuando.
2. Dado que el Administrador intenta suspender a un usuario sin declarar un motivo, cuando confirma la suspension, entonces el sistema rechaza la accion y exige el campo de motivo.
3. Dado que el usuario que se intenta suspender es el unico usuario activo con un rol critico (Administrador de la organizacion, Delegado de Proteccion de Datos/Responsable interno o Responsable de Seguridad/IT) y no hay otro usuario activo con ese rol, cuando el Administrador confirma la suspension, entonces el sistema exige asignar un reemplazo o confirmar explicitamente con el texto Esta decision requiere la confirmacion de un responsable de su organizacion antes de completar la suspension.
4. Dado que se confirma la suspension de un usuario que es el unico titular de un rol critico sin reemplazo, cuando se completa la accion, entonces el sistema genera la alerta Baja de unico titular de un rol critico sin reemplazo de nivel CRITICAL hacia Administrador y Delegado de forma inmediata.
5. Dado que un usuario esta en estado SUSPENDIDO, cuando el Administrador lo reactiva, entonces el sistema cambia su estado a ACTIVO y restaura su acceso segun el rol o roles que ya tenia asignados.
6. Dado que un Responsable de area intenta suspender a un usuario de su propia unidad, cuando lo intenta, entonces el sistema le deniega la accion porque suspender usuarios es una accion exclusiva del Administrador.

**Reglas de negocio**

- Suspender exige siempre un motivo declarado.
- No se puede dejar sin reemplazo al unico titular activo de un rol critico sin una confirmacion explicita registrada.
- Suspender bloquea el acceso de inmediato sin perder el historial.

**Fuera de alcance**

- Reasignacion automatica del rol critico vacante a otro usuario (el sistema nunca la ejecuta por su cuenta)

- Referencia: MOD-001 secciones F.2, F.3, G fila 5, H, I (Baja de unico titular de un rol critico sin reemplazo), C

### HU-001-07. Dar de baja usuarios con reemplazo de rol critico

**Como** Administrador de la organizacion, **quiero** dar de baja de forma definitiva a un usuario declarando un motivo, exigiendo un reemplazo cuando es el unico titular de un rol critico, **para** cerrar el acceso de quien ya no debe tenerlo sin perder la trazabilidad de lo que hizo mientras estuvo activo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 3 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-001-05, HU-001-06
- Modulos requeridos: MOD-022

**Criterios de aceptacion**

1. Dado que un usuario esta en estado ACTIVO o SUSPENDIDO, cuando el Administrador lo da de baja declarando un motivo, entonces el sistema cambia su estado a DADO DE BAJA como estado terminal, y el usuario deja de poder iniciar sesion.
2. Dado que el Administrador intenta dar de baja a un usuario sin declarar un motivo, cuando confirma la baja, entonces el sistema rechaza la accion y exige el campo de motivo.
3. Dado que el usuario a dar de baja es el unico usuario activo con un rol critico (Administrador de la organizacion, Delegado de Proteccion de Datos/Responsable interno o Responsable de Seguridad/IT), cuando el Administrador intenta completar la baja sin asignar un reemplazo, entonces el sistema bloquea la accion hasta que se asigne un reemplazo o se confirme explicitamente con el texto Esta decision requiere la confirmacion de un responsable de su organizacion.
4. Dado que un usuario fue dado de baja, cuando se completa la transicion, entonces el sistema conserva integramente su historial de acciones pasadas vinculado a su identidad, sin eliminarlo ni reasignarlo a otra persona.
5. Dado que un usuario dado de baja tenia tareas asignadas o evidencia adjunta en otros modulos, cuando se consulta ese historial despues de la baja, entonces el sistema sigue mostrando esos registros enlazados a la identidad historica del usuario dado de baja.
6. Dado que se completa la baja de un usuario que no era el unico titular de ningun rol critico, cuando se registra el evento, entonces el sistema no genera la alerta CRITICAL de baja de unico titular sin reemplazo.
7. Dado que un Auditor interno consulta el historial de un usuario dado de baja, cuando lo abre, entonces el sistema le permite verlo en modo de solo lectura, sin ninguna opcion de reactivarlo.

**Reglas de negocio**

- Dar de baja es un estado terminal: no existe transicion de reactivacion desde DADO DE BAJA.
- No se puede dar de baja al unico titular activo de un rol critico sin asignar reemplazo o confirmar explicitamente.
- El historial de un usuario dado de baja nunca se elimina ni se reasigna a otra persona.

**Fuera de alcance**

- Reapertura del estado DADO DE BAJA (no existe en este modulo)

- Referencia: MOD-001 secciones F.2, F.3, G fila 5, H, I (Baja de unico titular de un rol critico sin reemplazo), O

### HU-001-08. Editar los datos y el rol de un usuario

**Como** Administrador de la organizacion, **quiero** editar los datos basicos de un usuario y modificar el rol o roles que tiene asignados, con las reglas de doble control y de advertencia de autorrevision que correspondan, **para** mantener el control de acceso actualizado sin que una sola persona pueda aprobarse a si misma un cambio sensible.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 2 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-001-04, HU-001-05
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que un usuario existe en el sistema, cuando el Administrador edita su cargo, su area o unidad, o su telefono, entonces el sistema guarda los cambios y registra en el historial el valor anterior, el valor nuevo, quien lo hizo y cuando.
2. Dado que el Administrador asigna uno o mas roles del catalogo de 12 roles estandar a un usuario, cuando guarda el cambio, entonces el sistema exige que quede al menos un rol seleccionado y registra el rol anterior y el rol nuevo en el historial.
3. Dado que el cambio de rol es sobre el propio rol del Administrador que lo esta ejecutando, cuando intenta guardarlo, entonces el sistema le deniega aprobar ese cambio el mismo y exige que lo apruebe un segundo Administrador o, si no existe otro, el Responsable Legal/Compliance.
4. Dado que se asigna el rol Aprobador o Auditor a un usuario y la organizacion esta por debajo del umbral configurable de separacion de funciones (valor propuesto: 50 empleados), cuando quien crea o modifica ese rol es la misma persona que lo aprobaria, entonces el sistema permite completar la accion pero muestra una advertencia visible de autorrevision y la marca como autorrevision en el historial.
5. Dado que la organizacion supera el umbral configurable de separacion de funciones, cuando se detecta que quien crea o modifica un rol Aprobador o Auditor seria la misma persona que lo aprobaria, entonces el sistema bloquea unicamente esa accion especifica y nunca reasigna o retira el rol de nadie por su cuenta; la resolucion queda siempre a cargo del Administrador o del Responsable Legal/Compliance.
6. Dado que un Usuario de consulta / Colaborador abre su propio perfil, cuando lo consulta, entonces el sistema le muestra unicamente sus propios datos y no le permite ver el listado completo de usuarios de la organizacion.
7. Dado que el Delegado de Proteccion de Datos no tiene ademas asignado el rol Administrador de la organizacion, cuando intenta modificar directamente el rol de otro usuario, entonces el sistema le deniega la ejecucion directa y solo le permite dejar registrada una solicitud de cambio de rol.

**Reglas de negocio**

- El Administrador nunca puede aprobarse a si mismo un cambio de su propio rol, sin excepcion de tamano de empresa.
- Por debajo del umbral configurable, la acumulacion de roles Aprobador o Auditor con quien los crea se permite con advertencia visible de autorrevision; por encima del umbral, esa accion especifica se bloquea.
- El rol Auditor (interno o externo) es siempre de solo lectura y nunca coincide con quien carga evidencia o aprueba la misma accion que audita.
- Un usuario debe conservar siempre al menos un rol asignado.

**Fuera de alcance**

- Bloqueo automatico configurable de la separacion de funciones por umbral de tamano mas alla de la combinacion Aprobador/Auditor (SHOULD HAVE)
- Roles personalizados (SHOULD HAVE)

- Preguntas pendientes relacionadas: PP-PROD-04
- Referencia: MOD-001 secciones D.2, C, F.3 (Cambio de rol asignado), H, R.4
- Notas: El umbral y la advertencia de autorrevision son opinion de producto (05_tipos_de_usuario.md 5.4); el bloqueo automatico configurable completo es SHOULD HAVE y queda fuera de esta HU.

### HU-001-09. Actualizar el contacto ARCO-POL derivado al cambiar su titular

**Como** Administrador de la organizacion, **quiero** que el contacto ARCO-POL que se muestra en pantalla y en los documentos se actualice automaticamente cuando cambia quien tiene asignado el rol Responsable ARCO-POL, **para** no dejar informacion de contacto desactualizada sin que nadie se entere.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 3 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-001-08
- Modulos requeridos: MOD-021

**Criterios de aceptacion**

1. Dado que el rol Responsable ARCO-POL queda activo en exactamente un usuario, cuando se asigna o se retira ese rol a alguien, entonces el sistema actualiza automaticamente el contacto ARCO-POL derivado que se muestra en pantalla.
2. Dado que existen documentos publicados que citan el contacto ARCO-POL por variable, cuando el contacto derivado se actualiza, entonces el sistema crea una tarea de revision de esos documentos, en vez de reescribirlos o republicarlos automaticamente.
3. Dado que ningun usuario activo tiene asignado el rol Responsable ARCO-POL, cuando el sistema muestra el contacto ARCO-POL derivado, entonces indica que no hay contacto asignado en vez de mostrar un nombre.
4. Dado que se actualiza el contacto ARCO-POL derivado, cuando ocurre el cambio, entonces el sistema registra el evento en el historial de la organizacion con el valor anterior, el valor nuevo, quien ejecuto el cambio de rol y cuando.

**Reglas de negocio**

- El contacto ARCO-POL nunca se captura como campo independiente; siempre se deriva del usuario activo con el rol Responsable ARCO-POL.
- El sistema nunca reescribe automaticamente un documento ya publicado; solo crea una tarea de revision.

**Fuera de alcance**

- Reescritura o republicacion automatica de documentos ya publicados

- Referencia: MOD-001 secciones D.1 (Contacto ARCO-POL publicado), G fila 3, H

### HU-001-10. Alertar y registrar la decision sobre el umbral de separacion de funciones

**Como** Administrador de la organizacion, **quiero** recibir una alerta cuando el numero de empleados declarado supera el umbral configurable de separacion de funciones, y poder dejar registrada mi decision, **para** decidir de forma informada si activo el bloqueo de acumulacion de roles o si mantengo mi decision de no activarlo por ahora.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 3 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-001-01, HU-001-08
- Modulos requeridos: MOD-022

**Criterios de aceptacion**

1. Dado que el numero de empleados declarado de la organizacion supera el umbral configurable (valor propuesto: 50) y la separacion de funciones no esta activada, cuando se cruza ese umbral, entonces el sistema genera la alerta Umbral de separacion de funciones alcanzado de nivel WARNING hacia el Administrador por plataforma y correo.
2. Dado que la alerta de umbral ya se genero y sigue sin atenderse, cuando pasa un mes sin que el Administrador actue, entonces el sistema repite la alerta mensualmente y la escala al Responsable Legal/Compliance a los 30 dias.
3. Dado que se muestra la alerta de umbral, cuando el Administrador decide activar el bloqueo de acumulacion de Aprobador y Auditor en la misma persona, entonces el sistema activa esa configuracion y apaga la alerta.
4. Dado que se muestra la alerta de umbral, cuando el Administrador decide mantenerla desactivada por ahora, entonces el sistema exige una confirmacion explicita, registra esa decision en el historial con quien la tomo y cuando, y apaga la alerta hasta el proximo ciclo.
5. Dado que el numero de empleados declarado esta por debajo del umbral configurable, cuando se consulta el estado de separacion de funciones, entonces el sistema lo muestra como no aplica y no genera la alerta de umbral.

**Reglas de negocio**

- El umbral es configurable dentro de un rango predefinido por el equipo de producto (propuesta inicial: 50 empleados).
- Decidir mantener la separacion de funciones desactivada siempre queda registrado como una decision explicita del Administrador.

**Fuera de alcance**

- El mecanismo de bloqueo en si mismo (cubierto como una de las reglas de HU-001-08); esta HU cubre la alerta y el registro de la decision

- Preguntas pendientes relacionadas: PP-PROD-04
- Referencia: MOD-001 secciones G fila 4, I (Umbral de separacion de funciones alcanzado), M

### HU-001-11. Alertar cuando ningun usuario activo tiene un rol critico

**Como** Administrador de la organizacion, **quiero** recibir una alerta cuando ningun usuario activo tenga asignado alguno de los roles criticos, **para** no quedarme sin capacidad de administrar el sistema por una vacante no atendida.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 3 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-001-04, HU-001-07
- Modulos requeridos: MOD-022

**Criterios de aceptacion**

1. Dado que ningun usuario activo tiene asignado el rol Administrador de la organizacion, Delegado de Proteccion de Datos/Responsable interno o Responsable de Seguridad/IT, cuando se detecta esa condicion, entonces el sistema genera la alerta Rol critico sin titular de nivel HIGH hacia el Administrador restante o quien quede con acceso.
2. Dado que la alerta de rol critico sin titular sigue activa, cuando pasan 15 dias sin que se asigne el rol, entonces el sistema la escala a la vista de Gerencia del dashboard.
3. Dado que la alerta de rol critico sin titular esta activa, cuando se repite el ciclo semanal, entonces el sistema la reenvia por plataforma y correo mientras persista la condicion.
4. Dado que se asigna el rol critico faltante a un usuario activo, cuando se completa esa asignacion, entonces el sistema apaga la alerta Rol critico sin titular.
5. Dado que al menos un usuario activo tiene asignado cada uno de los tres roles criticos, cuando se evalua la condicion, entonces el sistema no genera esta alerta.

**Reglas de negocio**

- Los roles criticos son Administrador de la organizacion, Delegado de Proteccion de Datos/Responsable interno y Responsable de Seguridad/IT.
- El sistema solo alerta; nunca asigna un rol critico a un usuario por su cuenta.

- Referencia: MOD-001 secciones I (Rol critico sin titular), H, M

### HU-001-12. Alertar sobre estructura sin actualizar y registrar la revision de accesos

**Como** Responsable de Seguridad / IT, **quiero** recibir un aviso cuando la estructura de usuarios, roles o sucursales no ha cambiado en un periodo prolongado, y poder dejar constancia de que se reviso, **para** usarlo como evidencia de que la organizacion revisa periodicamente sus accesos vigentes.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 3 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-001-01, HU-001-08
- Modulos requeridos: MOD-022

**Criterios de aceptacion**

1. Dado que no hubo ningun cambio de usuarios, roles o sucursales en un periodo prolongado (por ejemplo, 6 meses), cuando se cumple ese periodo, entonces el sistema genera la alerta Estructura sin actualizar de nivel INFO hacia Administrador y Responsable de Seguridad/IT.
2. Dado que se muestra la alerta Estructura sin actualizar, cuando el Administrador realiza cualquier cambio de usuarios, roles o sucursales, entonces el sistema apaga la alerta.
3. Dado que se muestra la alerta Estructura sin actualizar y no hay cambios pendientes que hacer, cuando el Administrador confirma explicitamente que reviso los accesos vigentes y no hay cambios pendientes, entonces el sistema registra esa confirmacion en el historial con quien la hizo y cuando, y apaga la alerta.
4. Dado que se registro una confirmacion de revision de accesos, cuando el Auditor interno o el Responsable de Seguridad/IT consultan el historial del modulo, entonces pueden ver esa confirmacion como parte de la evidencia de control de acceso.
5. Dado que hubo un cambio de estructura dentro del periodo vigente, cuando se evalua la condicion de la alerta, entonces el sistema no genera la alerta Estructura sin actualizar.

**Reglas de negocio**

- El sistema no ejecuta por si mismo una revision periodica de accesos; solo la sugiere mediante esta alerta.
- La confirmacion de revision queda registrada en el historial como evidencia.

**Fuera de alcance**

- Periodicidad exacta o checklist formal de la revision de accesos (hueco documentado en 04_secciones/11_roles_y_permisos.md, 11.4.4, sin definir en la ficha)

- Referencia: MOD-001 secciones I (Estructura sin actualizar), M, O
- Notas: La ficha no define una periodicidad recomendada ni un checklist propio de esta revision; solo la alerta y la confirmacion registrada.

### HU-001-13. Crear una tarea de revision al declarar operacion fuera de El Salvador

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** recibir una tarea sugerida de revision cuando la organizacion declara un pais distinto a El Salvador o una sucursal en el exterior, **para** evaluar a tiempo si esa operacion implica una transferencia internacional de datos.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 3 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-001-01, HU-001-02
- Modulos requeridos: MOD-021

**Criterios de aceptacion**

1. Dado que el Administrador agrega un pais distinto a El Salvador en Paises donde opera, cuando guarda el cambio, entonces el sistema crea la tarea sugerida Revisar si esto implica una transferencia internacional de datos para el Delegado, con un enlace de referencia al modulo de transferencias internacionales.
2. Dado que el Administrador da de alta una sucursal en el exterior, cuando guarda el cambio, entonces el sistema crea la misma tarea sugerida para el Delegado.
3. Dado que la empresa desactivo esta sugerencia, cuando se agrega un pais distinto a El Salvador o una sucursal en el exterior, entonces el sistema no crea la tarea.
4. Dado que se crea la tarea sugerida, cuando se registra el evento, entonces el sistema no crea por si mismo ningun registro de transferencia internacional, solo la tarea de revision.
5. Dado que el Administrador solo agrega o edita sucursales dentro de El Salvador, cuando guarda esos cambios, entonces el sistema no crea la tarea sugerida de transferencia internacional.

**Reglas de negocio**

- La empresa puede desactivar esta sugerencia.
- El sistema nunca concluye por si mismo que existe una transferencia internacional; solo sugiere revisarla.

**Fuera de alcance**

- Registro formal de la transferencia internacional (MOD-010, SHOULD HAVE)

- Referencia: MOD-001 secciones D.1 (Paises donde opera), G fila 6

### HU-001-14. Exportar el listado de usuarios y roles vigentes

**Como** Auditor (interno), **quiero** exportar el listado de usuarios y roles vigentes a una fecha de corte, **para** usarlo como evidencia de control de acceso dentro de una revision o auditoria.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 3 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-001-05, HU-001-08
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el Auditor interno tiene acceso al modulo, cuando solicita exportar el listado de usuarios y roles vigentes, entonces el sistema genera un archivo en PDF, XLSX o CSV con nombre, correo, cargo, area, rol o roles, estado y fecha de alta de cada usuario a la fecha de corte.
2. Dado que se genera la exportacion, cuando se completa, entonces el sistema registra en el historial quien exporto, cuando y con que filtro.
3. Dado que un Responsable de area sin permiso de exportacion intenta exportar el listado completo, cuando lo intenta, entonces el sistema le deniega la exportacion.
4. Dado que el Auditor interno filtra el listado por area, por rol o por estado antes de exportar, cuando confirma la exportacion, entonces el archivo generado respeta esos filtros.
5. Dado que la exportacion generada en esta version no incluye un mecanismo de verificacion de integridad (hash o firma), cuando se entrega a un tercero, entonces el sistema no la presenta como un EvidencePackage con verificacion de integridad, porque ese mecanismo es una capacidad posterior.

**Reglas de negocio**

- Pueden exportar el listado Administrador, Delegado, Responsable Legal/Compliance, Responsable de Seguridad/IT, Auditor interno y Auditor externo (este ultimo acotado a su ventana de invitacion).
- La version con hash de integridad queda fuera de esta HU (SHOULD HAVE).

**Fuera de alcance**

- Exportacion firmada con verificacion de integridad (hash o firma validable), que es SHOULD HAVE segun la tabla Q de la ficha

- Referencia: MOD-001 secciones E, N, Q (fila Exportacion firmada con verificacion de integridad del listado de usuarios), C (Exportar)
- Notas: La ficha marca la version CON hash de integridad como SHOULD HAVE; esta HU cubre la version simple del MVP, cobertura parcial descrita en la propia justificacion de esa fila de la tabla Q, y se declara como discrepancia en notas_epica.

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Alta de organizacion (datos societarios minimos) | HU-001-01 |
| Gestion de sucursales de una misma razon social | HU-001-02 |
| Gestion de usuarios (invitar, activar, suspender, dar de baja) | HU-001-05, HU-001-06, HU-001-07, HU-001-08 |
| Catalogo de los 12 roles estandar | HU-001-04, HU-001-08 |
| Unidades o departamentos | HU-001-03 |
