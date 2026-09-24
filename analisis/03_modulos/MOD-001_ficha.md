# MODULO: Organizacion y Personas

Codigo corto del modulo: MOD-001
Clasificacion global del modulo: MUST HAVE
Obligaciones que cubre: ninguna como propietario. Colabora en OBL-AMB-01 (propietaria: MOD-004 Diagnostico de Cumplimiento).

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (sin codigo, sin SQL, sin APIs, sin stack, sin infraestructura).

Fuentes usadas para esta ficha: `02_validacion/mapa_modulos.json` (entrada MOD-001), `02_validacion/06_mapa_definitivo_de_modulos.md` (secciones 0, 1, 2, 3, 6.1, 7, 8, 9, 10, 11), `02_validacion/02_validacion_de_la_idea.md` (secciones 2.4, 2.5, 2.6, 2.7, decisiones 5, 7, 30, 31), `02_validacion/04_objetivo_exacto_del_producto.md`, `02_validacion/05_tipos_de_usuario.md` (secciones 5.1 a 5.4), `02_validacion/22_anti_features.md`, `01_legal/matriz_obligaciones.md` y `matriz_obligaciones.json` (OBL-AMB-01), `01_legal/03_hallazgos_regulatorios.md`, y las secciones 11 y 12 (hipotesis) de `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md`.

---

## A. Proposito

- **Por que existe.** MOD-001 es el registro fundacional de toda cuenta: la identidad legal de la empresa cliente, su estructura interna (sucursales, unidades, departamentos) y el modelo de roles y permisos (RBAC) que usan los demas 25 modulos del sistema. Es el punto de partida obligatorio: ningun otro modulo puede operar sin una organizacion registrada y sin al menos un usuario con un rol asignado.
- **Que problema resuelve para la empresa.** Hoy, en una empresa salvadorena sin departamento de privacidad dedicado, la identidad de la empresa, quien es responsable de que area y quien tiene acceso a que informacion suele vivir dispersa (hojas de calculo, correos, memoria del gerente). MOD-001 le da a esa informacion un lugar unico, con historial y trazabilidad, del que dependen todas las tareas, alertas, documentos y evidencia que genera el resto del sistema.
- **Que obligacion cubre.** MOD-001 no es propietario de ninguna obligacion con OBL-ID propio (verificado en `mapa_modulos.json`, campo `obligaciones_propietarias: []`, y en la tabla de cobertura de la seccion 8 de `06_mapa_definitivo_de_modulos.md`). Es colaborador de OBL-AMB-01 (Art. 2 inc. 1 LPDP, "Ambito de aplicacion universal de la LPDP", clasificacion OBLIGATORIO), cuya propietaria es MOD-004 Diagnostico de Cumplimiento: la matriz de obligaciones exige como evidencia esperada una "Ficha de organizacion con giro y tipos de tratamiento", y esa ficha es exactamente el registro que MOD-001 mantiene. MOD-001 provee el dato (razon social, sector, giro, paises de operacion); MOD-004 es quien concluye y documenta si la ley aplica y en que medida.
- **Que valor aporta.**
  - Operativo: sin organizacion, usuarios y roles no puede operar ningun otro modulo (dependencia estructural, criterio (b) del test de tres condiciones de MVP, seccion 2 principio 7 de `06_mapa_definitivo_de_modulos.md`).
  - Probatorio: deja constancia de quien existia, con que rol, desde cuando y hasta cuando, insumo directo del control de acceso que las Politicas de Actuacion de la ACE (N. 001-0309025-DPDP) exigen como medida tecnica organizativa.
  - De reduccion de riesgo: permite separar funciones (quien crea no siempre puede aprobar) antes de que la empresa crezca y ese riesgo se vuelva mas dificil de corregir.
- **Que NO hace este modulo (limites explicitos).**
  - No determina si la Ley para la Proteccion de Datos Personales aplica a la empresa ni si alguna exclusion del Art. 3 le corresponde: eso lo concluye y documenta el Diagnostico de Cumplimiento (MOD-004), usando los datos que MOD-001 le entrega.
  - No gestiona el nombramiento legal del Delegado de Proteccion de Datos ni del Responsable Interno, su comunicacion a la ACE, su reverificacion cada 3 anos ni su confidencialidad post-cese: esas 8 obligaciones (OBL-DPO-01 a OBL-DPO-08) y ese ciclo de vida completo son propiedad de MOD-002 Delegado / Responsable Interno de Datos, elevado a modulo de primer nivel en el mapa definitivo. MOD-001 solo mantiene el rol dentro del catalogo de RBAC (quien esta asignado hoy a ese rol), no la investidura legal de esa persona.
  - No gestiona facturacion, suscripcion comercial ni planes de pago de la cuenta SaaS: es informacion comercial, fuera del alcance funcional de proteccion de datos que cubre esta ficha.
  - No es un directorio completo de recursos humanos: solo captura los campos minimos necesarios para operar el sistema (nombre, correo corporativo, cargo, area, rol); no reemplaza al sistema de nomina o de gestion de personal de la empresa.
  - No decide por si mismo si dos sociedades de un mismo grupo empresarial deben tratarse como una organizacion con sucursales o como organizaciones separadas: en el MVP, esa decision queda fuera de alcance porque el MVP solo soporta una razon social con varias sucursales (decision de alcance 2.7.31 de `02_validacion_de_la_idea.md`); la gestion de grupos multi-sociedad con delegado comun es funcionalidad V1/Enterprise.

**Nota sobre el doble estado de la reforma 659.** MOD-001 no cambia entre el estado ACTUAL y el estado FUTURO de la reforma (campo `notas_reforma_659` de `mapa_modulos.json`: "No posee obligaciones afectadas directamente; conserva la identidad de organizacion y usuarios sin cambios entre regimenes"). La organizacion, sus sucursales, sus usuarios y el catalogo de roles siguen siendo exactamente los mismos registros en ambos regimenes; lo unico que cambia con la activacion de la bandera de MOD-024 Centro Regulatorio es cual rol concentra las funciones legales hoy atribuidas al Delegado, y ese cambio se documenta y ejecuta dentro de MOD-002, no aqui. MOD-001 solo debe garantizar que el catalogo de roles incluya, sin friccion, tanto la etiqueta "Delegado de Proteccion de Datos" (estado ACTUAL) como "Responsable Interno" (estado FUTURO) como dos nombres visibles de un mismo rol configurable.

---

## B. Usuarios

Roles estandar usados (los 12 de `02_validacion/05_tipos_de_usuario.md`, seccion 5.3):

| Rol | Para que usa MOD-001 |
|---|---|
| Administrador de la organizacion | Crea y edita los datos societarios, da de alta sucursales y unidades, invita usuarios, asigna y modifica roles, activa o desactiva la separacion de funciones. Es el unico rol con acceso de escritura completo al modulo. |
| Delegado de Proteccion de Datos / Responsable interno | Consulta la estructura y el catalogo de usuarios para saber a quien puede asignar las tareas que la ley le atribuye a el o ella; puede solicitar el alta o el cambio de un rol relacionado con privacidad, pero no lo ejecuta el mismo salvo que tambien tenga asignado el rol Administrador (caso tipico de pyme, ver perfil 1 de `05_tipos_de_usuario.md`). |
| Responsable ARCO-POL / Responsable del tramite | Consulta la estructura para saber a que area o sucursal pertenece un tratamiento cuando gestiona un caso concreto en MOD-011; no administra usuarios ni roles. |
| Responsable Legal / Compliance | Consulta el catalogo de roles y las reglas de separacion de funciones configuradas para validar que una cadena de aprobacion sea valida antes de publicarla en otro modulo (por ejemplo, aprobacion de un documento en MOD-008). |
| Responsable de Seguridad / IT | Consulta el listado de usuarios activos e inactivos como parte de la evidencia de control de acceso que despues registra en el catalogo de controles de MOD-015; puede solicitar una revision de accesos. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Ve su propia ficha de usuario y la de su equipo dentro de su area o unidad; no administra la estructura global de la organizacion ni el catalogo global de roles. |
| Aprobador | No administra MOD-001 directamente; su capacidad de aprobar en otros modulos depende de que este rol le haya sido asignado aqui. |
| Auditor (interno) | Consulta de solo lectura el listado de usuarios, roles vigentes e historico de cambios de estructura; no puede crear, modificar ni aprobar nada en este modulo. |
| Auditor externo (invitado) | Igual que el Auditor interno, pero con acceso temporal por invitacion y acotado a lo que el paquete de evidencias exponga durante la ventana de auditoria. |
| Usuario de consulta / Colaborador | Ve unicamente su propio perfil y el organigrama basico necesario para saber a quien escalar una tarea o una duda. |
| Titular (formulario externo) | No usa este modulo. El titular externo no tiene visibilidad de la estructura interna de la empresa; su relacion es exclusivamente con MOD-011 ARCO-POL y MOD-012 Portal del Titular. |
| Asesor externo invitado | Ve solo la porcion de estructura o roles relevante al caso puntual para el que fue invitado (por ejemplo, quien es hoy el Responsable Legal a cargo de un expediente); no ve el resto del catalogo de usuarios. |

---

## C. Permisos

Abreviaturas de rol usadas en la tabla: ADM = Administrador de la organizacion, DEL = Delegado / Responsable interno, ARC = Responsable ARCO-POL, LEG = Responsable Legal/Compliance, SEG = Responsable de Seguridad/IT, ARE = Responsable de area, APR = Aprobador, AUI = Auditor interno, AUE = Auditor externo, COL = Usuario de consulta/Colaborador, TIT = Titular externo, ASE = Asesor externo invitado.

Simbologia: X = permitido siempre. X* = permitido con condicion (ver notas debajo de la tabla). - = no permitido.

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver datos de la organizacion | X | X | X | X | X | X | X | X | X* | X* | - | X* |
| Ver listado completo de usuarios y roles | X | X | - | X | X | - | - | X | X* | - | - | - |
| Ver solo su propio perfil y su equipo | X | X | X | X | X | X | X | X | X | X | - | - |
| Crear organizacion (alta inicial) | X | - | - | - | - | - | - | - | - | - | - | - |
| Modificar datos societarios (razon social, sector, sucursales) | X | - | - | - | - | - | - | - | - | - | - | - |
| Crear/invitar usuario | X | X* | - | - | - | - | - | - | - | - | - | - |
| Modificar rol de un usuario | X | - | - | - | - | - | - | - | - | - | - | - |
| Aprobar cambio de rol sensible (doble control) | X* | - | - | X* | - | - | - | - | - | - | - | - |
| Suspender o dar de baja usuario | X | - | - | - | - | - | - | - | - | - | - | - |
| Archivar sucursal o unidad | X | - | - | - | - | - | - | - | - | - | - | - |
| Eliminar registro (solo borrador no publicado) | X | - | - | - | - | - | - | - | - | - | - | - |
| Exportar listado de usuarios y roles | X | X | - | X | X | - | - | X | X* | - | - | - |
| Asignar rol personalizado | X | - | - | - | - | - | - | - | - | - | - | - |
| Comentar en una solicitud de alta o cambio de rol | X | X | X | X | X | X | X | - | - | - | - | - |
| Adjuntar evidencia (por ejemplo, acta o poder del Administrador) | X | - | - | X | - | - | - | - | - | - | - | - |

Notas de separacion de funciones:
- El Administrador no puede aprobarse a si mismo un cambio de su propio rol: ese cambio siempre exige un segundo Administrador o, si no existe otro, al Responsable Legal (X* en la fila "Aprobar cambio de rol sensible").
- El Delegado o Responsable interno puede invitar usuarios solo si ademas tiene asignado el rol Administrador (caso pyme); si no lo tiene, solo puede solicitar el alta, no ejecutarla (X* en "Crear/invitar usuario").
- El acceso del Auditor externo y del Asesor externo invitado esta siempre acotado en el tiempo (ventana de invitacion) y, para el Asesor, ademas acotado al caso o modulo para el que fue invitado (X* en "Ver datos de la organizacion", "Ver listado" y "Exportar").
- Por encima del umbral configurable de tamano de empresa (propuesta inicial: 50 empleados, opinion de producto sin respaldo legal expreso, ver `05_tipos_de_usuario.md` seccion 5.4), el sistema exige que quien crea o modifica un rol de tipo Aprobador o Auditor no sea la misma persona que lo aprueba; por debajo del umbral, el sistema solo lo recomienda con una advertencia visible de "autorrevision".
- El rol Auditor (interno o externo) es siempre de solo lectura en este modulo, sin excepcion: nunca puede coincidir con quien carga evidencia o aprueba una accion (regla heredada de `05_tipos_de_usuario.md` seccion 5.4).

---

## D. Informacion de entrada

### D.1 Organizacion (empresa)

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Razon social | Texto | Obligatorio desde el alta | - | No vacio; unico dentro de la cuenta | "Escriba el nombre legal completo de su empresa, tal como aparece en su documento de constitucion." | Buena practica; base identificatoria para la ficha de organizacion que exige OBL-AMB-01 |
| Nombre comercial | Texto | Opcional | - | - | "Si su empresa usa un nombre distinto al legal para atender al publico, escribalo aqui." | Buena practica |
| Identificacion tributaria (NIT/NRC) | Texto | Obligatorio antes de completar el onboarding | - | Formato numerico salvadoreno; unico dentro de la cuenta | "Ingrese el NIT de su empresa. Lo usamos para identificar su organizacion, no para hacer tramites tributarios." | Buena practica |
| Sector o giro economico | Seleccion unica | Obligatorio desde el alta | Catalogo: Comercio, Industria/Manufactura, Servicios financieros, Salud, Educacion, Tecnologia, Agroindustria, Construccion, Turismo, Gobierno/sector publico, Otro | Debe elegir un valor del catalogo | "Elija el giro principal de su empresa. Esta informacion la usamos para adaptar las preguntas del diagnostico a su actividad." | OBL-AMB-01 (Art. 2 inc. 1): la matriz exige como evidencia esperada una "ficha de organizacion con giro y tipos de tratamiento" |
| Numero de empleados (rango) | Seleccion unica | Obligatorio desde el alta | 1-10, 11-50, 51-250, 251 o mas | Debe elegir un rango | "Elija el rango que mejor describe el tamano de su empresa. Lo usamos para sugerir cuando activar controles adicionales, como la separacion de funciones." | Opinion de producto: umbral de separacion de funciones, `05_tipos_de_usuario.md` seccion 5.4 |
| Direccion principal | Texto largo | Opcional | - | - | "Direccion de la oficina principal o casa matriz." | Buena practica |
| Paises donde opera | Seleccion multiple | Obligatorio desde el alta | Catalogo de paises, con "El Salvador" preseleccionado y no removible | Al menos un pais seleccionado | "Marque todos los paises donde su empresa tiene operaciones. Si marca un pais distinto a El Salvador, el sistema le sugerira revisar si eso implica una transferencia internacional de datos." | Dispara evaluacion de referencia en MOD-010 (Transferencias Internacionales); no concluye por si mismo que exista una transferencia |
| Fecha de inicio de operaciones en El Salvador | Fecha | Opcional | - | No puede ser fecha futura | "Fecha desde la que su empresa opera en El Salvador. Nos ayuda a calcular plazos transitorios si aplican a su caso." | Buena practica |
| Sucursales | Lista de sub-registros (nombre, direccion, pais) | Opcional en el alta, editable despues | - | Cada sucursal requiere nombre | "Agregue cada sucursal o sede adicional de su empresa. El MVP soporta varias sucursales de una misma razon social." | Decision de alcance 2.7.31: el MVP soporta una organizacion con varias sucursales, no multiples razones sociales/grupos |
| Unidades o departamentos | Lista (nombre, area funcional) | Opcional, recomendado antes de invitar usuarios | Catalogo de area funcional: RRHH, Marketing, TI, Legal/Compliance, Operaciones, Finanzas, Atencion al cliente, Otro | - | "Defina las areas o departamentos de su empresa para poder asignar responsables y organizar el trabajo." | Buena practica |
| Responsable por defecto de cada unidad | Referencia a Usuario | Opcional | - | Debe ser un usuario ya invitado | "Elija quien es la persona responsable de esta area. Podra cambiarlo despues." | Buena practica |
| Contacto ARCO-POL publicado | Derivado automaticamente | No se captura como campo independiente | - | - | (no aplica, es un campo calculado, se muestra solo como referencia de lectura) | Decision de alcance 2.7.8: el contacto ARCO-POL se deriva del usuario con el rol "Responsable ARCO-POL" activo, no se captura por separado |
| Contacto de seguridad | Referencia a Usuario con rol Responsable de Seguridad/IT | Opcional | - | - | "Persona a quien contactar internamente ante un problema de seguridad de la informacion." | Buena practica |

### D.2 Usuario

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Nombre completo | Texto | Obligatorio | - | No vacio | "Nombre completo de la persona que usara el sistema." | Necesario para identificacion y trazabilidad de auditoria |
| Correo electronico corporativo | Texto | Obligatorio | - | Formato de correo valido; unico dentro de la cuenta | "Correo con el que esta persona iniciara sesion. Recomendamos usar su correo corporativo, no uno personal." | Necesario para invitacion y notificaciones |
| Cargo | Texto | Opcional | - | - | "Puesto que ocupa dentro de la empresa (por ejemplo, Gerente de RRHH)." | Buena practica |
| Area o departamento | Referencia a Unidad | Opcional | Catalogo de unidades de D.1 | - | "Area a la que pertenece esta persona." | Buena practica |
| Rol o roles asignados | Seleccion multiple | Obligatorio, al menos uno | Catalogo de los 12 roles estandar mas roles personalizados activos | Debe elegir al menos un rol | "Elija que puede hacer esta persona dentro del sistema. Puede asignar mas de un rol si en su empresa una sola persona cumple varias funciones (comun en pymes)." | RBAC, base de todo el sistema de permisos |
| Telefono | Texto | Opcional | - | Formato de numero telefonico | "Numero para recibir notificaciones por SMS o WhatsApp cuando ese canal este disponible." | Buena practica, preparacion para MOD-022 Notificaciones |
| Estado | Seleccion unica, gestionada por el sistema | No editable directamente por el usuario final | Invitado, Activo, Suspendido, Dado de baja | Transiciones controladas por el workflow (seccion F) | (no aplica, es un campo de sistema) | Necesario para control de acceso |

### D.3 Rol personalizado (cuando la empresa necesita mas granularidad que los 12 roles estandar)

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Nombre del rol | Texto | Obligatorio | - | No vacio; unico dentro de la cuenta | "Nombre de este rol personalizado, por ejemplo Coordinador de Marketing Digital." | Opinion de producto |
| Basado en rol estandar | Referencia opcional a uno de los 12 roles | Opcional | Catalogo de los 12 roles estandar | - | "Si este rol se parece a uno de los roles estandar, eliguelo aqui como punto de partida." | Opinion de producto |
| Permisos por modulo y por accion | Matriz de seleccion | Obligatorio | Modulos disponibles x acciones (ver, crear, modificar, aprobar, eliminar/archivar, exportar, asignar) | Debe tener al menos un permiso marcado | "Marque exactamente que puede ver y hacer esta persona en cada modulo." | Opinion de producto |
| Descripcion | Texto largo | Opcional | - | - | "Explique brevemente para que se usa este rol." | Buena practica |

### D.4 Precarga y minimizacion de datos personales

- Que campos se precargan desde otros modulos: MOD-003 Onboarding precarga los campos minimos de D.1 (razon social, NIT, sector, pais, numero de empleados) durante la primera sesion guiada; el resto de la ficha de organizacion y todos los usuarios adicionales se completan despues, directamente en MOD-001.
- Que campos contienen datos personales: unicamente los campos de D.2 (nombre, correo, cargo, telefono) contienen datos personales, y son datos del personal interno de la empresa cliente (no de los titulares externos que la empresa atiende). Los campos de D.1 (razon social, NIT, sector, sucursales) son datos societarios, no datos personales.
- Como se minimizan: el modulo no pide documento de identidad, fecha de nacimiento ni direccion personal de los usuarios internos; solo los campos estrictamente necesarios para operar el control de acceso (nombre, correo corporativo, cargo, rol). Esta es una excepcion intencional y acotada al principio general de minimizacion (decision de alcance 2.7.21 de `02_validacion_de_la_idea.md`, que acota la minimizacion estricta a RAT, Inventario y Proveedores): un modulo de identidad y acceso necesita datos reales de personas reales para funcionar, a diferencia del RAT, que solo necesita metadatos de un tratamiento ajeno.

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Ficha de organizacion consolidada | Razon social, NIT, sector, tamano, sucursales, estructura | Vista en pantalla, exportable a PDF | Se actualiza en tiempo real con cada cambio; se "cierra" logicamente cuando pasa a estado ACTIVA | Administrador, Delegado, Legal, Auditor; consumida automaticamente por MOD-004 Diagnostico como evidencia de OBL-AMB-01 |
| Organigrama o vista de estructura | Sucursales, unidades y responsables por unidad | Vista jerarquica en pantalla | Se recalcula con cada cambio de estructura | Todos los roles internos, segun su alcance de visibilidad (seccion C) |
| Catalogo de roles activo | Los 12 roles estandar mas los roles personalizados que la empresa haya creado, con sus permisos | Vista consultable por otros modulos (referencia, no duplicado) | Disponible desde el alta; se actualiza con cada cambio | Consumido por referencia por los 25 modulos restantes para resolver permisos |
| Historial de altas, bajas y cambios de rol | Evento, usuario afectado, valor anterior/nuevo, quien lo ejecuto, fecha y hora | Registro de auditoria, exportable | En cada evento | Auditor, Administrador; insumo de MOD-018/MOD-019 |
| Alertas de estructura incompleta o rol critico sin titular | Texto de alerta, nivel, modulo/campo afectado | Notificacion en plataforma, email | Segun disparadores de la seccion I | Administrador, y segun escalamiento, Delegado o Gerencia |
| Evento "organizacion lista" | Bandera booleana mas fecha | Evento interno de sistema | Cuando los campos minimos de D.1 quedan completos | Habilita el siguiente paso de MOD-003 Onboarding y el inicio de MOD-004 Diagnostico |
| Exportacion firmada de usuarios y roles vigentes | Listado completo a una fecha de corte, con hash de integridad | PDF o CSV con verificacion de integridad | A solicitud, tipicamente antes de una auditoria | Auditor interno o externo, Gerencia, Centro de Evidencias (MOD-019) |

---

## F. Workflow

MOD-001 gestiona dos ciclos de vida relacionados: el de la Organizacion (y sus sucursales) y el de cada Usuario. Ambos se muestran por separado porque tienen disparadores y responsables distintos, aunque comparten el mismo modulo.

### F.1 Ciclo de vida de la Organizacion

```
   [alta desde MOD-003 Onboarding]
              |
              v
        +-----------+     completar campos minimos      +----------+
        | BORRADOR  | ---------------------------------> |  ACTIVA  |
        +-----------+          (D.1: razon social,       +----------+
              |                 NIT, sector, pais,              |
              |                 numero de empleados)             |
              |                                                  | edicion continua
              |  abandono (sin completar)                        | (no cambia de estado,
              v                                                  |  solo actualiza campos
        +-----------+                                            |  y registra historial)
        | DESCARTADA|                                            v
        +-----------+                                     +-----------+
                                                            |  ACTIVA   |
                                                            | (estable) |
                                                            +-----------+
```

Las sucursales tienen un ciclo propio, mas simple, anidado dentro de una Organizacion en estado ACTIVA:

```
   +----------+   archivar    +-----------+
   | ACTIVA   | ------------> | ARCHIVADA |
   +----------+               +-----------+
        ^                            |
        |______ reactivar ___________|
        (el Administrador puede reactivar sin perder historial)
```

### F.2 Ciclo de vida del Usuario

```
   [Administrador invita]
            |
            v
      +-----------+   acepta invitacion   +----------+
      | INVITADO  | ---------------------> |  ACTIVO  |
      +-----------+                        +----------+
            |                                  |    ^
            | vence invitacion (30 dias)        |    |
            v                                  |    | reactivar
      +-----------+                             |    |
      | EXPIRADO  |                             v    |
      +-----------+                       +------------+
      (Administrador puede reenviar)       | SUSPENDIDO |
                                            +------------+
                                                  |
                                                  | dar de baja
                                                  v
                                          +----------------+
                                          | DADO DE BAJA   |  (estado terminal,
                                          +----------------+   historial preservado)
```

### F.3 Tabla de transiciones

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (nueva) | Alta de organizacion desde Onboarding | Ninguna | BORRADOR | Administrador (via MOD-003) | Crea registro; evento de auditoria "organizacion creada" |
| BORRADOR | Completar campos minimos de D.1 | Razon social, NIT, sector, pais y numero de empleados presentes | ACTIVA | Administrador | Dispara evento "organizacion lista"; habilita MOD-004; alerta se apaga |
| BORRADOR | Abandono sin completar (inactividad prolongada) | Ninguna accion en X dias, umbral configurable [opinion de producto] | DESCARTADA | Sistema, con aviso previo | No se elimina informacion, queda archivada con historial |
| ACTIVA | Editar cualquier campo de D.1 | Ninguna, salvo validaciones de campo | ACTIVA (sin cambio de estado) | Administrador | Registra valor anterior/nuevo en historial; evento de auditoria |
| ACTIVA (sucursal) | Archivar sucursal | La sucursal no puede ser la unica registrada si hay tratamientos activos referenciandola desde MOD-006 (advertencia, no bloqueo automatico) | ARCHIVADA | Administrador | Deja de aparecer en listas activas; conserva historial; MOD-006 mantiene la referencia como historica |
| ARCHIVADA (sucursal) | Reactivar sucursal | Ninguna | ACTIVA | Administrador | Vuelve a aparecer en listas activas |
| (nuevo) | Administrador invita usuario | Correo valido y no duplicado; al menos un rol seleccionado | INVITADO | Administrador (o Delegado si tambien es Administrador) | Envia notificacion de invitacion; crea tarea "completar perfil" en MOD-021 |
| INVITADO | Usuario acepta la invitacion | Enlace de invitacion valido y vigente | ACTIVO | El propio usuario invitado | Habilita acceso segun su rol; evento de auditoria "usuario activado" |
| INVITADO | Vencimiento de la invitacion (30 dias, opinion de producto) | Sin accion del usuario en el plazo | EXPIRADO | Sistema | Genera alerta INFO al Administrador |
| EXPIRADO | Reenviar invitacion | Ninguna | INVITADO | Administrador | Nuevo enlace, nuevo plazo |
| ACTIVO | Suspender usuario | Motivo declarado obligatorio | SUSPENDIDO | Administrador | Bloquea acceso inmediatamente; conserva historial; si el usuario es titular unico de un rol critico, exige confirmacion explicita (ver seccion G) |
| SUSPENDIDO | Reactivar usuario | Ninguna | ACTIVO | Administrador | Restaura acceso |
| ACTIVO o SUSPENDIDO | Dar de baja usuario | Motivo declarado obligatorio; si es titular unico de un rol critico, exige asignar reemplazo o confirmar advertencia explicita | DADO DE BAJA | Administrador | Estado terminal; el usuario deja de poder iniciar sesion; su historial de acciones pasadas permanece intacto y vinculado a su identidad, nunca se elimina ni se reasigna a otra persona |
| Cualquier estado de Usuario | Cambio de rol asignado | Si el nuevo rol es sensible (Aprobador, Auditor) y la empresa supera el umbral de separacion de funciones, requiere aprobacion de un segundo Administrador o del Responsable Legal | (sin cambio de estado del usuario) | Administrador, con aprobacion condicional | Registra rol anterior y nuevo en historial; puede disparar la alerta de "contacto ARCO-POL actualizado" si el rol afectado es Responsable ARCO-POL |

No existen estados de "reapertura" propios de MOD-001 mas alla de reactivar un usuario suspendido o una sucursal archivada: al ser un modulo de identidad y no de expedientes, no tiene un concepto de "caso cerrado" que deba reabrirse. Los registros vinculados (tareas asignadas, evidencia adjunta, aprobaciones firmadas por un usuario dado de baja) nunca se eliminan ni se reasignan automaticamente a otra persona: quedan enlazados a la identidad historica de ese usuario, tal como lo exige la regla general de preservacion de historial del mapa definitivo (seccion 2, principio 8).

---

## G. Automatizaciones

| # | Disparador | Condicion | Accion | Configurable |
|---|---|---|---|---|
| 1 | Se completan los campos minimos de D.1 en una organizacion en BORRADOR | Razon social, NIT, sector, pais y numero de empleados presentes | Cambia el estado a ACTIVA; dispara el evento "organizacion lista"; habilita el paso siguiente de MOD-003 y el inicio de MOD-004 | No |
| 2 | Se invita a un usuario | Correo valido, rol seleccionado | Se crea automaticamente una tarea "Completar perfil" en MOD-021 Centro de Tareas para ese usuario; se envia una notificacion de bienvenida via MOD-022 | Si, la empresa puede desactivar el envio de la notificacion de bienvenida |
| 3 | Se asigna o retira el rol "Responsable ARCO-POL" a un usuario | El rol queda activo en exactamente una persona | Se actualiza automaticamente el "contacto ARCO-POL" derivado que se muestra en pantalla y en los documentos que lo referencian por variable; se crea una tarea de revision en los documentos publicados que citan ese contacto (no se reescriben automaticamente, ver seccion H) | No |
| 4 | El numero de empleados declarado supera el umbral configurable (propuesta inicial: 50) | Separacion de funciones aun no activada | Se genera una alerta WARNING y se ofrece al Administrador activar el bloqueo de acumulacion Aprobador + Auditor en la misma persona | Si, el umbral es ajustable por el equipo del producto dentro de un rango predefinido |
| 5 | Se intenta dar de baja o suspender a un usuario que es el unico titular de un rol critico (Delegado, Responsable de Seguridad, Administrador) sin reemplazo asignado | No existe otro usuario activo con ese mismo rol | Se bloquea la accion hasta que se asigne un reemplazo, o se exige una confirmacion explicita con advertencia visible si la empresa decide continuar sin reemplazo inmediato | No, es una validacion de integridad minima |
| 6 | Se agrega un pais distinto de El Salvador en "paises donde opera", o se da de alta una sucursal en el exterior | Ninguna adicional | Se crea una tarea sugerida "Revisar si esto implica una transferencia internacional de datos" visible para el Delegado, con enlace de referencia a MOD-010; no se crea un registro de transferencia automaticamente | Si, la empresa puede desactivar esta sugerencia |
| 7 | Se completa el catalogo minimo de unidades/departamentos | Al menos una unidad registrada | Se habilita, en la invitacion de usuarios, el selector de area (antes solo se puede invitar sin area asignada) | No |

Todas estas reglas son sugerencias operativas o validaciones de integridad del propio modulo; ninguna decide por si sola una cuestion juridica. El catalogo de reglas disponibles lo fija el equipo del producto; la empresa puede activar, desactivar o ajustar el umbral de cada regla dentro de los rangos predefinidos [opinion de producto].

---

## H. Decisiones que NO debe automatizar

- **Determinar si la empresa esta dentro del ambito de aplicacion de la LPDP (Art. 2) o si le corresponde alguna exclusion del Art. 3.** MOD-001 solo registra el giro, el sector y los paises de operacion; la conclusion sobre aplicabilidad y exclusiones la entrega exclusivamente el Diagnostico de Cumplimiento (MOD-004), con el texto "Requiere validacion de la organizacion o asesoria especializada" cuando corresponda. Razon: la aplicabilidad de la ley es una calificacion juridica sobre hechos, no un dato de formulario.
- **Decidir automaticamente que persona debe ocupar un rol critico** (Delegado, Administrador, Responsable de Seguridad). El sistema solo alerta cuando un rol critico queda sin titular; nunca asigna un rol a un usuario por su cuenta. Razon: es una decision de gobierno interno de la empresa, no una funcion del software.
- **Resolver por si mismo un conflicto de separacion de funciones reasignando o eliminando un rol.** El sistema solo bloquea la accion que genera el conflicto y muestra la advertencia; la resolucion (a quien se le retira o se le asigna el rol) la decide siempre el Administrador o el Responsable Legal. Razon: reasignar automaticamente el acceso de una persona sin intervencion humana es en si mismo un riesgo de seguridad y de gobierno, no solo un riesgo legal.
- **Decidir si dos sociedades de un mismo grupo empresarial deben tratarse como una sola organizacion (con sucursales) o como organizaciones separadas.** El MVP no ofrece esta decision porque no soporta grupos multi-sociedad (decision de alcance 2.7.31); cuando esa funcionalidad exista en V1/Enterprise, la decision seguira siendo administrativa de la empresa, nunca automatica del sistema. Razon: tiene efectos sobre como se reparte la responsabilidad legal entre sociedades del grupo, algo que el software no puede calificar.
- **Actualizar de forma automatica y retroactiva documentos ya publicados que citan al "contacto ARCO-POL" cuando ese rol cambia de titular.** El sistema actualiza la referencia viva (la variable), pero no reescribe ni republica por su cuenta un documento ya emitido; crea una tarea de revision para que una persona decida si corresponde emitir una nueva version. Razon: un documento publicado (por ejemplo, un Aviso de Privacidad ya comunicado a titulares) no debe cambiar de contenido sin que alguien lo revise y apruebe explicitamente.

Cada uno de estos casos muestra, segun corresponda, el texto "Requiere validacion de la organizacion o asesoria especializada" cuando la decision es de naturaleza juridica, o una advertencia equivalente de gobierno interno ("Esta decision requiere la confirmacion de un responsable de su organizacion") cuando es administrativa mas no juridica, pero que igualmente el sistema no debe tomar por si solo.

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia o repeticion | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Organizacion incompleta | Han pasado 3 dias desde el alta sin completar los campos minimos de D.1 | WARNING | Administrador | Plataforma + email | Recordatorio a los 3 y a los 7 dias | No escala (es informativo, el modulo es autoservicio) | Se completan los campos minimos y la organizacion pasa a ACTIVA |
| Rol critico sin titular | Ningun usuario activo tiene asignado un rol critico (Administrador, Delegado, Responsable de Seguridad) | HIGH | Administrador (o quien quede) | Plataforma + email | Semanal mientras persista | Escala a Gerencia (vista dashboard) a los 15 dias | Se asigna el rol a un usuario activo |
| Invitacion pendiente de aceptar | Un usuario invitado no ha activado su cuenta | INFO | Administrador | Plataforma | Una vez a los 15 dias, otra a los 30 dias (antes de expirar) | No escala | El usuario acepta la invitacion, o el Administrador cancela la invitacion |
| Umbral de separacion de funciones alcanzado | El numero de empleados declarado supera el umbral configurable (50 por defecto) sin que la separacion de funciones este activada | WARNING | Administrador | Plataforma + email | Una vez al cruzar el umbral; repite mensualmente si no se atiende | Escala al Responsable Legal a los 30 dias | Se activa la separacion de funciones, o el Administrador confirma explicitamente que decide mantenerla desactivada (queda registrado como decision) |
| Baja de unico titular de un rol critico sin reemplazo | Se intenta dar de baja o suspender al unico usuario con un rol critico y no hay reemplazo asignado | CRITICAL | Administrador y Delegado | Plataforma + email (mas SMS si esta configurado) | Inmediato | Escala a la vista de Gerencia del dashboard en 24 horas si no se resuelve | Se asigna un reemplazo, o la accion se cancela |
| Estructura sin actualizar | Ningun cambio de usuarios, roles o sucursales en un periodo prolongado (por ejemplo, 6 meses), sugiere revisar accesos vigentes | INFO | Administrador, Responsable de Seguridad | Plataforma | Una vez por periodo | No escala | Se realiza cualquier cambio o el Administrador confirma que revizo y no hay cambios pendientes |

---

## J. Evidencia

| Evidencia | Como se registra | Que obligacion o control prueba | Conservacion |
|---|---|---|---|
| Ficha de organizacion con giro y tipos de tratamiento | Registro con fecha y hora de creacion, historial de cada edicion (valor anterior y nuevo, usuario, fecha) | Evidencia esperada explicitamente por OBL-AMB-01 (Art. 2 inc. 1), segun `matriz_obligaciones.json` | Mientras la cuenta este activa; tras la baja de la cuenta, segun la regla general de retencion documental que define MOD-016 (MOD-001 no es propietario de ninguna obligacion de retencion propia) |
| Historial de altas, bajas y cambios de rol de cada usuario | Evento de auditoria por cada transicion de la seccion F.3, con identidad de quien ejecuto el cambio, fecha, hora y motivo declarado | Prueba de control de acceso, insumo indirecto de la evidencia tecnica que la empresa registra en el catalogo de controles de seguridad (MOD-015), alineado con las medidas tecnicas de control de acceso de las Politicas de Actuacion de la ACE | Igual que el registro anterior; nunca se elimina, ni siquiera si el usuario es dado de baja |
| Registro de aprobaciones de cambios de rol sensible | Identidad del aprobador, fecha, resultado (aprobado/rechazado), motivo si fue rechazado | Prueba de que la separacion de funciones configurada realmente se aplico | Igual que el registro anterior |
| Exportacion firmada del listado de usuarios y roles vigentes a una fecha | Archivo exportado con mecanismo de verificacion de integridad (hash o firma validable de forma independiente) | Insumo del paquete de evidencia que arma MOD-019 Centro de Evidencias para auditorias internas o externas (por ejemplo, la auditoria anual de cumplimiento, OBL-AUD-01, propiedad de MOD-018) | La copia exportada conserva su propia fecha de corte; el registro vivo sigue las reglas anteriores |
| Accesos de lectura del Auditor externo o del Asesor externo invitado | Cada acceso queda registrado (quien, cuando, que vio) durante la ventana de invitacion | Prueba de que el acceso externo estuvo acotado en tiempo y alcance | Igual que el historial general |

---

## K. Documentos asociados

- **Documentos requeridos como entrada.** Ninguno es obligatorio para completar el alta basica de la organizacion. Opcionalmente, la empresa puede adjuntar el acta de constitucion o el poder del representante legal como respaldo de identidad de quien se registra como Administrador inicial; es una buena practica, no una exigencia de esta ficha.
- **Documentos generados.** "Ficha de organizacion" exportable en PDF, que resume razon social, NIT, sector, estructura y roles vigentes a la fecha de exportacion. No es en si mismo un documento con efectos legales; es un insumo de evidencia y de otros documentos del sistema (por ejemplo, el Aviso de Privacidad de MOD-008 puede citar por referencia los datos societarios registrados aqui, nunca copiarlos como texto fijo).
- **Plantillas que el sistema provee.** Plantilla opcional de organigrama simple. No requiere validacion de la organizacion antes de usarse porque no genera ningun compromiso legal ni se envia a un tercero por si sola.
- **Anexos y evidencias documentales.** El sistema permite adjuntar el acta de constitucion, el poder del representante legal, o cualquier otro respaldo que la empresa decida conservar como evidencia del alta, siempre a criterio de la empresa, nunca como campo obligatorio.

---

## L. Dependencias

```
   MOD-003 Onboarding
        |
        v
   MOD-001 Organizacion y Personas
        |
        |------------------------------------------------------------+
        v  (alimenta identidad de organizacion, catalogo de usuarios |
        |   y catalogo de roles, consultados por referencia          |
        |   constante desde todos los demas modulos)                 |
        v                                                             v
   MOD-002 .. MOD-026
   (Delegado, Diagnostico, Plan, RAT, Consentimiento, Documentos,
    Proveedores, Transferencias, ARCO-POL, Portal, Incidentes,
    Riesgos/EIPD, Controles, Retencion, Capacitacion, Auditoria,
    Evidencias, Dashboard, Tareas, Notificaciones, Calendario,
    Regulatorio, Busqueda, Ayuda)
```

- **Entra desde:** MOD-003 Onboarding, que es el flujo guiado a traves del cual una organizacion nueva completa su alta inicial en MOD-001. Una vez creada, la organizacion tambien se edita directamente dentro de MOD-001 (pantallas de administracion), sin pasar de nuevo por el wizard de onboarding.
- **Sale hacia:** practicamente todos los demas modulos (MOD-002 a MOD-026). Segun la convencion de `mapa_modulos.json` explicada en la seccion 6.1 de `06_mapa_definitivo_de_modulos.md`, MOD-001 aparece en el `alimenta_a` de casi todos los modulos porque provee la identidad de organizacion, el catalogo de usuarios y el catalogo de roles que se consultan por referencia constante, sin que cada modulo consumidor tenga que declarar esa lectura como una dependencia estructural propia.
- **Que catalogos comparte:** catalogo de Roles (RBAC, los 12 estandar mas los personalizados que la empresa cree), catalogo de Unidades/Departamentos, catalogo de Sucursales.
- **Que ocurre si el modulo dependiente no existe en el MVP:** no aplica en ese sentido; MOD-001 es la dependencia estructural de la que dependen los demas, no al reves. El riesgo real es el inverso: si MOD-001 no estuviera disponible o incompleto, ningun otro modulo MUST HAVE podria operar, porque ninguno tiene su propio catalogo de usuarios o de roles (regla del mapa definitivo: "ningun modulo de proceso escribe su propia copia de la identidad de organizacion").

---

## M. Dashboard

| Indicador | Formula o definicion | Semaforo | Vista por rol |
|---|---|---|---|
| Usuarios activos vs invitados pendientes | Conteo de usuarios en estado ACTIVO sobre el total invitado | Verde si no hay invitaciones vencidas; amarillo si hay 1 o mas invitaciones a mas de 15 dias sin aceptar; rojo si hay invitaciones expiradas sin reenviar | Gerencia (resumen), Administrador (detalle completo) |
| Roles criticos sin titular | Conteo de roles marcados como criticos (Administrador, Delegado, Responsable de Seguridad) sin ningun usuario activo asignado | Verde si es 0; amarillo si es 1; rojo si es 2 o mas | Gerencia, Legal, Administrador |
| Sucursales registradas | Conteo de sucursales en estado ACTIVA | Sin semaforo, es informativo | Gerencia, Responsable de area |
| Separacion de funciones | Estado: activada / recomendada no activada / no aplica (por debajo del umbral) | Verde si esta activada o si la empresa esta por debajo del umbral; amarillo si esta por encima del umbral y no activada | Legal, Auditor, Gerencia |
| Ultimo cambio de estructura | Fecha del ultimo evento de alta, baja o cambio de rol | Sin semaforo, es informativo, util para saber que tan actualizado esta el control de acceso | Auditor, Responsable de Seguridad |

Ningun indicador de este modulo se expresa como porcentaje de "cumplimiento legal"; todos muestran estado del programa (usuarios activos, roles cubiertos, estructura configurada), en linea con el principio general del producto (`04_objetivo_exacto_del_producto.md`, seccion 1.2).

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Listado de usuarios y roles vigentes | Nombre, correo, cargo, area, rol(es), estado, fecha de alta | Por area, por rol, por estado | PDF, XLSX, CSV | Auditor interno o externo, Administrador | Si, forma parte del paquete de evidencia de auditoria (control de acceso) |
| Ficha de organizacion | Razon social, NIT, sector, tamano, sucursales, estructura | Ninguno (reporte de una sola organizacion) | PDF | Uso interno, Gerencia, y como insumo para MOD-004 | Complementario: se cita como evidencia de OBL-AMB-01 dentro del paquete general, no como reporte independiente para la ACE |
| Historial de cambios de estructura | Cada evento de alta, baja o cambio de rol, con fecha, usuario y motivo | Por rango de fechas, por tipo de evento, por usuario | CSV, PDF | Auditor, Responsable de Seguridad | Si, forma parte del paquete de evidencia de control de acceso |

---

## O. Historial

Eventos que deben quedar registrados en el historial de este modulo y en la auditoria transversal (AuditLog):

- Creacion de la organizacion (fecha, usuario que la creo).
- Cada cambio de campo de la organizacion (campo, valor anterior, valor nuevo, usuario, fecha y hora).
- Alta de una sucursal o unidad; archivado y reactivacion de una sucursal.
- Invitacion de un usuario (correo, rol inicial asignado, quien invito).
- Aceptacion o expiracion de una invitacion.
- Cambio de rol de un usuario (rol anterior, rol nuevo, quien lo ejecuto, aprobacion asociada si aplico).
- Suspension y reactivacion de un usuario (motivo declarado).
- Baja definitiva de un usuario (motivo declarado, si se asigno reemplazo de rol critico).
- Aprobaciones de cambios de rol sensible (identidad del aprobador, resultado).
- Exportaciones del listado de usuarios y roles (quien exporto, cuando, con que filtro).
- Accesos de lectura del Auditor externo o del Asesor externo invitado (quien, cuando, que vio, dentro de que ventana de invitacion).
- Activacion o desactivacion de la separacion de funciones, y quien tomo esa decision.

---

## P. Riesgos

- **Riesgo legal.** Que la empresa (o el propio equipo de producto) trate el campo "sector/giro" de la ficha de organizacion como si ya resolviera la aplicabilidad de la LPDP, sin pasar por el Diagnostico. Mitigacion de diseno: la ficha de organizacion nunca muestra un texto del tipo "la ley le aplica" o "esta excluido"; solo alimenta a MOD-004, que es el unico lugar donde aparece esa conclusion, siempre con el texto de advertencia correspondiente.
- **Riesgo de UX.** Un formulario de alta demasiado largo desalienta a un usuario no especialista y provoca abandono durante el onboarding (perfil tipico: Karla, Gerente Administrativa de una pyme, `05_tipos_de_usuario.md` perfil 1). Mitigacion de diseno: solo 5 campos son obligatorios en el alta minima (razon social, NIT, sector, pais, numero de empleados); el resto de la ficha (sucursales, unidades, contactos adicionales) se completa progresivamente despues, sin bloquear el avance al Diagnostico.
- **Riesgo operativo.** Estructura desactualizada: un usuario que ya no trabaja en la empresa sigue teniendo acceso activo porque nadie lo dio de baja. Mitigacion de diseno: la alerta "Estructura sin actualizar" (seccion I) y la revision periodica sugerida de accesos, ademas de que toda baja exige un motivo declarado y queda en el historial.
- **Riesgo de seguridad y privacidad.** Exposicion innecesaria de datos personales del personal interno (nombre, correo, cargo) a usuarios que no lo necesitan para su trabajo. Mitigacion de diseno: el listado completo de usuarios solo es visible para Administrador, Delegado, Legal, Seguridad y Auditor (seccion C); un Responsable de area solo ve su propio equipo, y un Colaborador solo ve su propio perfil.
- **Riesgo de continuidad.** Que un rol critico (por ejemplo, Administrador o Responsable de Seguridad) quede sin ningun titular activo, por ejemplo tras una renuncia no gestionada, y la empresa pierda la capacidad de administrar el sistema. Mitigacion de diseno: la alerta CRITICAL de "baja de unico titular sin reemplazo" (seccion I) y el bloqueo de la baja hasta confirmar explicitamente esa situacion (seccion F.3, regla de automatizacion 5 de la seccion G).

---

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Alta de organizacion (datos societarios minimos) | X | | | | Dependencia estructural absoluta: sin ella no puede operar ningun otro modulo MUST HAVE (test de tres condiciones, criterio b, seccion 2 de `06_mapa_definitivo_de_modulos.md`) |
| Gestion de sucursales de una misma razon social | X | | | | El MVP soporta explicitamente multi-sucursal (decision de alcance 2.7.31) |
| Gestion de usuarios (invitar, activar, suspender, dar de baja) | X | | | | Sin control de acceso basico no hay forma segura de operar ningun modulo |
| Catalogo de los 12 roles estandar | X | | | | Es el RBAC minimo que consumen los 25 modulos restantes |
| Unidades o departamentos | X | | | | Necesario para asignar tareas por area desde el primer dia (Diagnostico y Plan de Cumplimiento ya lo requieren) |
| Roles personalizados con permisos granulares por modulo/accion | | X | | | Valor real para empresas medianas y corporativas, pero los 12 roles estandar ya permiten operar el primer tramo de clientes (pyme y empresa mediana); cobertura parcial en MVP: la empresa puede pedir ajustes de alcance al equipo del producto mientras no exista el editor de permisos |
| Separacion de funciones configurable con umbral por tamano | | X | | | Opinion de producto de valor real (05_tipos_de_usuario.md 5.4), pero no bloquea la operacion de una pyme pequena; cobertura parcial en MVP: el sistema ya muestra la advertencia de "autorrevision", solo falta el bloqueo automatico configurable |
| Auditor externo con acceso temporal por invitacion | | X | | | Valioso para la auditoria anual de cumplimiento (OBL-AUD-01, propiedad de MOD-018), pero no imprescindible desde el primer dia de uso; cobertura parcial en MVP: el Auditor interno ya cubre la necesidad basica de solo lectura |
| Organigrama visual grafico | | | X | | Mejora de experiencia, no bloquea ninguna obligacion ni ningun otro modulo |
| Exportacion firmada con verificacion de integridad del listado de usuarios | | X | | | Necesaria para el paquete de evidencia de auditoria, pero puede cubrirse en una primera version con una exportacion simple sin firma, mientras se construye el mecanismo de integridad compartido con MOD-019 |
| Gestion de grupo empresarial multi-sociedad (holding con varias razones sociales y delegado comun) | | | | X | Explicitamente fuera del MVP por decision de alcance 2.7.31; el propio documento maestro tampoco la desarrolla |
| Vision consolidada multi-sociedad en el dashboard | | | | X | Depende de la funcionalidad anterior; perfil "Ana Gabriela Reyes Portillo" de `05_tipos_de_usuario.md` (Directora de Cumplimiento Corporativo) la necesita, pero es V1/Enterprise por decision explicita |

**Version minima que ya puede venderse.** Una organizacion (una razon social) con una o varias sucursales, el catalogo completo de los 12 roles estandar, invitacion y gestion basica de usuarios (invitar, activar, suspender, dar de baja) y el catalogo minimo de unidades/departamentos. Sin roles personalizados, sin separacion de funciones automatica (solo advertencia visible), sin multi-empresa y sin exportacion firmada con hash. Esta version ya permite operar con seguridad razonable a una pyme o a una empresa mediana de una sola sociedad, que es el segmento de entrada declarado en `04_objetivo_exacto_del_producto.md`.

---

## R. Ayuda contextual

**1. Organizacion**
- Que es: el registro de su empresa dentro del sistema, con sus datos basicos (nombre legal, NIT, sector) y su estructura (sucursales, areas).
- Por que tengo que hacer esto: todo lo demas que el sistema hace (diagnostico, tareas, plazos, documentos) parte de saber quien es su empresa y como esta organizada.
- Fundamento: la ficha de organizacion es la evidencia que la ley pide como parte de determinar si le aplica la Ley para la Proteccion de Datos Personales (OBL-AMB-01, Art. 2 inc. 1 del Decreto Legislativo 144).
- Cuando necesito ayuda juridica: si tiene dudas sobre si su actividad esta total o parcialmente excluida de la ley (por ejemplo, por manejar unicamente historial crediticio bajo su ley especial), consulte con asesoria especializada; el sistema muestra esa conclusion en el Diagnostico, no aqui.

**2. Sucursal**
- Que es: una sede adicional de su misma empresa (misma razon social), en un lugar distinto a su oficina principal.
- Por que tengo que hacer esto: le permite saber, mas adelante, en que sucursal ocurre cada tratamiento de datos o cada incidente, y organizar responsables por sede.
- Fundamento: buena practica de organizacion interna; no existe un articulo especifico que exija registrar sucursales.
- Cuando necesito ayuda juridica: si sus sucursales pertenecen a razones sociales distintas (por ejemplo, sociedades separadas de un mismo grupo), consulte con su equipo legal como manejar esa estructura, ya que el sistema, en esta version, solo soporta una razon social con sucursales, no varias sociedades independientes.

**3. Rol**
- Que es: lo que una persona puede ver y hacer dentro del sistema (por ejemplo, el rol Aprobador puede aprobar documentos; el rol Auditor solo puede consultar).
- Por que tengo que hacer esto: asignar el rol correcto evita que alguien vea o modifique informacion que no le corresponde, y permite que el sistema sepa a quien asignarle cada tarea.
- Fundamento: buena practica de control de acceso, alineada con las medidas tecnicas y organizativas que las Politicas de Actuacion de la ACE (N. 001-0309025-DPDP) esperan de toda empresa que trata datos personales; el unico rol que la ley exige de forma expresa es el de Delegado de Proteccion de Datos (Arts. 15 y 17 del Decreto 144, mientras ese regimen siga vigente).
- Cuando necesito ayuda juridica: no suele requerirse para asignar roles operativos; si tiene dudas sobre quien debe ser designado formalmente Delegado de Proteccion de Datos, consulte la ficha de MOD-002.

**4. Separacion de funciones**
- Que es: la regla de que una misma persona no deberia, a la vez, crear y aprobar la misma accion, sobre todo cuando la empresa crece.
- Por que tengo que hacer esto: reduce el riesgo de errores o abusos que nadie mas revisa; es una practica de control interno recomendada, especialmente util cuando la empresa tiene mas de un area separada.
- Fundamento: es una decision de producto (05_tipos_de_usuario.md, seccion 5.4), no una exigencia expresa de la ley salvadorena, salvo en lo relacionado con la exigencia de motivacion de ciertas decisiones (por ejemplo, la denegatoria de una solicitud ARCO-POL, Art. 22).
- Cuando necesito ayuda juridica: normalmente no; es una decision de gobierno interno de su empresa, no una calificacion juridica.

**5. Usuario invitado vs usuario activo**
- Que es: "invitado" es alguien a quien ya se le envio acceso pero todavia no lo acepto; "activo" es alguien que ya puede usar el sistema.
- Por que tengo que hacer esto: le permite saber quien realmente esta usando el sistema y quien todavia no, para poder dar seguimiento.
- Fundamento: buena practica operativa; no tiene un fundamento legal especifico.
- Cuando necesito ayuda juridica: no aplica.

**6. Rol Delegado de Proteccion de Datos / Responsable interno (dentro del catalogo de roles)**
- Que es: la etiqueta del rol que hoy la ley llama "Delegado de Proteccion de Datos" y que, si la reforma 659 se publica y entra en vigencia, pasaria a llamarse "Responsable interno".
- Por que tengo que hacer esto: asignar este rol a la persona correcta es el primer paso para que el sistema le asigne, mas adelante en MOD-002, todas las tareas y plazos que la ley le atribuye a esa figura.
- Fundamento: OBL-DPO-01 (Arts. 15 y 17 del Decreto 144), mientras el regimen actual siga vigente; si la reforma se publica, el fundamento cambia al articulo reformado (16) sobre el "sujeto obligado", segun fuentes secundarias pendientes de confirmar contra el texto oficial.
- Cuando necesito ayuda juridica: si tiene dudas sobre quien puede o debe ocupar este rol (por ejemplo, si puede ser una persona externa, o si su empresa realmente necesita nombrar uno), consulte la ficha de MOD-002 y, si persiste la duda, a asesoria especializada.

---

## Nota final del autor de esta ficha

- No se detecto ninguna contradiccion entre esta ficha y las fuentes de diseno ya decididas (`mapa_modulos.json`, `06_mapa_definitivo_de_modulos.md`, `02_validacion_de_la_idea.md` seccion 2.7). La ausencia de obligaciones propias de MOD-001 (solo colabora en OBL-AMB-01) es consistente entre el JSON, el mapa definitivo y la matriz de obligaciones.
- Aclaracion de trazabilidad: la lista de roles usada en las secciones B y C es la de los 12 roles estandar de `02_validacion/05_tipos_de_usuario.md` (seccion 5.3), tal como pide la tarea. Esta lista sustituye, para esta ficha y para todo el blueprint, a la lista de ejemplo mas corta y desactualizada que aparece en la seccion B de `00_plantilla_ficha_modulo.md` ("Administrador de organizacion, Responsable de privacidad, Gestor ARCO-POL..."), que no incluye separadamente al Delegado, al Auditor externo, al Titular ni al Asesor externo invitado. No se trata de un error de la plantilla que deba corregirse aqui, sino de una version mas antigua que el catalogo de roles valido y mas reciente ya la reemplaza.
- Excepcion de minimizacion de datos declarada explicitamente: a diferencia del RAT o del Inventario de proveedores, MOD-001 si almacena datos personales reales de personas reales (nombre, correo, cargo de los usuarios internos de la empresa cliente), porque es el modulo de identidad y control de acceso del propio sistema. Esta excepcion esta amparada por la decision de alcance 2.7.21 de `02_validacion_de_la_idea.md`, que acota el principio de minimizacion estricta a RAT, Inventario y Proveedores, y no la extiende a modulos que por naturaleza deben manejar identidades reales para funcionar.
- Punto abierto para el equipo de producto, no un error de diseno: el umbral de 50 empleados para activar la separacion de funciones y el plazo de 30 dias para expirar una invitacion son valores propuestos en esta ficha como opinion de producto, sin respaldo legal expreso; quedan sujetos a validacion por el equipo antes de fijarse como parametros por defecto del sistema.
