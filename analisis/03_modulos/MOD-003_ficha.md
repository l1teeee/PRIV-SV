# MODULO: Onboarding

Codigo corto del modulo: MOD-003
Clasificacion global del modulo: MUST HAVE
Obligaciones que cubre: ninguna con OBL-ID propio (ver nota en seccion A)

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (prohibido codigo, SQL, APIs, stack o infraestructura).

Fuentes usadas para esta ficha: `00_contexto_para_agentes.md`, `00_prompt_analisis_funcional.md`, `00_plantilla_ficha_modulo.md`, `02_validacion/06_mapa_definitivo_de_modulos.md` (seccion MOD-003 y MOD-001, MOD-002, MOD-004), `02_validacion/mapa_modulos.json` (entrada MOD-003), `02_validacion/02_validacion_de_la_idea.md` (decision de alcance 2.7.5 y filas 23, 24, 28 de la tabla de faltantes), `02_validacion/04_objetivo_exacto_del_producto.md`, `02_validacion/05_tipos_de_usuario.md` (roles estandar, secciones 5.2 a 5.4), `02_validacion/22_anti_features.md`, `01_legal/matriz_obligaciones.md` / `.json`, y `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` secciones 8.3, 11, 12, 15, 32 y 45 (hipotesis de producto, no decisiones).

---

## A. Proposito

- **Por que existe.** Es la puerta de entrada del producto. Una persona designada por la empresa, sin conocimiento juridico previo y muchas veces sin experiencia previa en este tipo de plataformas, necesita poder crear el espacio de trabajo de su empresa, dar de alta su estructura minima y a las primeras personas que van a usar el sistema, en una sola sesion, sin sentirse perdida. El mapa definitivo de modulos describe su proposito asi: "Guia a la persona designada, sin conocimiento juridico previo, a traves de la alta inicial de organizacion, usuarios y roles en la primera sesion. Entrega como salida una organizacion configurada, lista para el Diagnostico" (`06_mapa_definitivo_de_modulos.md`, seccion 3, ficha MOD-003).
- **Que problema resuelve para la empresa.** Evita que la empresa llegue a un formulario largo y generico de "configuracion de cuenta" sin guia. En vez de eso, ordena en pasos cortos lo minimo indispensable para que el resto del sistema pueda funcionar: identidad de la organizacion, quien va a administrar el sistema, quien mas necesita acceso y si la empresa ya tiene resuelta (o no) la figura del Delegado de Proteccion de Datos, cuyo plazo legal ya esta corriendo desde el momento en que la empresa queda sujeta a la ley.
- **Que obligacion u obligaciones cubre.** MOD-003 no es propietario de ninguna obligacion con OBL-ID propio, segun confirma `mapa_modulos.json` (`"obligaciones_propietarias": []`, `"obligaciones_colaboradoras": []`) y la ficha resumida del mapa definitivo ("No posee obligaciones legales propias: ejecuta el alta de MOD-001"). Su valor legal es indirecto: siembra, desde el primer contacto, los datos que MOD-001 (Organizacion y Personas) y MOD-002 (Delegado / Responsable Interno de Datos) necesitan para empezar a vigilar sus propias obligaciones, entre ellas OBL-DPO-01 a 03 (Arts. 15, 17, 8 y 10 LPDP, nombramiento y comunicacion del Delegado) y OBL-AMB-01 (Art. 2 inc. 1, ambito de aplicacion universal de la LPDP, que el Diagnostico terminara de resolver).
- **Que valor aporta.**
  - Operativo: reduce el tiempo entre "la empresa compra el software" y "la empresa tiene datos utiles registrados" a una sola sesion guiada, en vez de dejar que cada usuario descubra por si mismo donde registrar cada cosa.
  - Probatorio: deja evidencia con fecha y usuario de cuando se constituyo el programa dentro del sistema (quien lo configuro, que organizacion se declaro, que personas se dieron de alta desde el inicio), que sirve de linea base historica para auditorias posteriores.
  - De reduccion de riesgo: la pregunta sobre el Delegado se hace en el primer contacto con el sistema, no se deja para "despues", lo que reduce el riesgo de que una empresa pequena olvide por completo esta obligacion mientras el plazo de comunicacion a la ACE (15 dias habiles, OBL-DPO-03) sigue corriendo.
- **Que NO hace este modulo (limites explicitos).**
  - No decide si la empresa esta sujeta a la LPDP ni cuales tratamientos realiza: eso es exclusivo del Diagnostico de Cumplimiento (MOD-004), que ademas es repetible y MOD-003 no lo es (decision de alcance 2.7.5, `02_validacion_de_la_idea.md`).
  - No completa el expediente legal del Delegado (requisitos del Art. 5 Lineamientos DPO, certificacion ante la ACE, reverificacion periodica): solo recoge el dato minimo para sembrar el registro en MOD-002, donde ese expediente se completa y se vigila.
  - No genera documentos legales (aviso de privacidad, politica de proteccion de datos, contratos): eso corresponde a MOD-008, despues del diagnostico y del plan.
  - No es un formulario de verificacion de identidad legal de la empresa (no exige documento de constitucion, DUI del representante ni NIT verificado contra un registro oficial); esa validacion documental queda fuera del alcance de este modulo (ver seccion Q, funcionalidad FUTURE).
  - No vuelve a ejecutarse como wizard una vez completado: los cambios posteriores a la organizacion, usuarios o roles se hacen directamente en MOD-001 (ver seccion F).

---

## B. Usuarios

MOD-003 tiene el universo de usuarios mas acotado de todo el sistema, porque ocurre antes de que la mayoria de los roles exista formalmente en la organizacion. Se usan los 12 roles estandar de `02_validacion/05_tipos_de_usuario.md`, seccion 5.3.

| Rol | Como usa MOD-003 |
|---|---|
| Administrador de la organizacion | Es quien ejecuta el wizard completo: crea la organizacion, completa el Paso 1 (datos de empresa), se autoasigna como Administrador en el Paso 2, invita a los primeros usuarios en el Paso 3, responde la pregunta sobre el Delegado en el Paso 4 y confirma el cierre en el Paso 5. Es, en la practica, el unico rol que "opera" este modulo. |
| Delegado de Proteccion de Datos (o Responsable interno) | No configura el wizard. Si el Administrador lo declara en el Paso 4, recibe una invitacion para crear su cuenta y aceptar la designacion; esa aceptacion ya ocurre dentro de MOD-002, no dentro de MOD-003 (ver seccion L). |
| Responsable ARCO-POL / Responsable del tramite | Puede ser uno de los usuarios invitados en el Paso 3 si el Administrador ya sabe quien va a ocupar ese rol; su participacion se limita a aceptar la invitacion y crear su cuenta. |
| Responsable Legal / Compliance | Igual que el anterior: puede recibir invitacion en el Paso 3 si la empresa ya lo tiene identificado; no interactua con la logica del wizard. |
| Responsable de Seguridad / IT | Igual: candidato tipico a invitacion temprana (por ejemplo, el Gerente de Tecnologia de una empresa mediana), sin interaccion adicional con el modulo. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Puede invitarse desde el Paso 3, aunque en la practica muchas empresas prefieren invitar solo al equipo minimo en el onboarding y sumar responsables de area despues, directamente desde MOD-001, sin reabrir el wizard. |
| Aprobador | No participa en el onboarding salvo que el Administrador decida invitarlo desde ya; el modulo no tiene flujo de aprobacion propio (ver seccion C). |
| Auditor (interno) | No participa en el onboarding. Su primer contacto con este modulo suele ser de solo lectura, meses despues, cuando consulta el historial de cuando y como se configuro la organizacion (ver seccion C, accion Ver). |
| Auditor externo (invitado) | No aplica en este modulo: los auditores externos se invitan puntualmente desde MOD-001/MOD-019 para una auditoria concreta, nunca durante el alta inicial. |
| Usuario de consulta / Colaborador | Puede ser invitado desde el Paso 3 si la empresa ya sabe que necesitara colaboradores operativos desde el primer dia; de lo contrario se agrega despues en MOD-001. |
| Titular (formulario externo) | No aplica: el titular de datos externo a la empresa nunca participa en el onboarding de la organizacion. |
| Asesor externo invitado | No aplica en el onboarding: se invita puntualmente a un caso concreto desde el modulo correspondiente (por ejemplo, ARCO-POL), nunca durante el alta inicial. |

---

## C. Permisos

MOD-003 no tiene flujo de aprobacion propio: es un autoservicio de una sola persona (el Administrador) en su primera sesion. La tabla de acciones refleja eso explicitamente en vez de forzar columnas que no aplican.

| Accion | Administrador de la organizacion | Delegado / Responsable interno | Responsable ARCO-POL | Responsable Legal | Responsable Seguridad/IT | Responsable de area | Aprobador | Auditor (interno) | Auditor externo | Usuario de consulta | Titular externo | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver (el wizard en curso o su historial) | Si, total | No aplica | No aplica | No aplica | No aplica | No aplica | No aplica | Si, solo lectura del historial ya completado | No | No | No aplica | No |
| Crear (organizacion, usuarios, respuestas del wizard) | Si | No | No | No | No | No | No | No | No | No | No aplica | No |
| Modificar (mientras el estado es EN_PROGRESO) | Si | No | No | No | No | No | No | No | No | No | No aplica | No |
| Aprobar | No aplica (el modulo no tiene flujo de aprobacion) | | | | | | | | | | | |
| Cerrar (confirmar y finalizar) | Si | No | No | No | No | No | No | No | No | No | No aplica | No |
| Eliminar / archivar | Solo puede retirar una invitacion pendiente; no puede eliminar el registro del onboarding ya completado (ver seccion F) | No | No | No | No | No | No | No | No | No | No aplica | No |
| Exportar (resumen de configuracion inicial) | Si | No | No | No | No | No | No | Si | No | No | No aplica | No |
| Asignar (rol a un usuario invitado) | Si | No | No | No | No | No | No | No | No | No | No aplica | No |
| Comentar | No aplica (el wizard no tiene hilos de comentarios; opinion de producto para mantenerlo simple) | | | | | | | | | | | |
| Adjuntar evidencia | No aplica (este modulo no admite adjuntos; ver seccion K) | | | | | | | | | | | |

**Separacion de funciones.** Este modulo, a diferencia de la mayoria, no exige doble control porque no toma ninguna decision legal sustantiva: solo recoge datos administrativos y de contacto. La unica regla de separacion de funciones que aplica aqui, heredada de `05_tipos_de_usuario.md` seccion 5.4, es una advertencia (no un bloqueo) cuando el Administrador intenta asignar a un mismo usuario invitado, ya en este primer paso, una combinacion de roles marcada como riesgosa por ese documento (por ejemplo, Aprobador y Auditor sobre el mismo periodo de evidencia). El bloqueo duro de esa combinacion, cuando la empresa supera el umbral configurable de tamano (propuesta inicial 50 empleados), es responsabilidad de MOD-001, no de este modulo; MOD-003 solo advierte porque en ese momento la estructura de la organizacion todavia no esta activa.

---

## D. Informacion de entrada

El wizard se organiza en 5 pasos cortos. Ningun campo de este modulo se precarga desde el Diagnostico ni desde plantillas, porque MOD-003 es el primer modulo que se usa (no tiene dependencias de entrada, ver seccion L); en sentido inverso, varios de sus campos si se reutilizan como precarga de otros modulos (lo indica la columna "Fundamento" y las notas al pie de cada paso).

### Paso 1: Datos de la empresa

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Razon social | Texto | Obligatorio desde el inicio | No aplica | No vacio, minimo 3 caracteres | "Escriba el nombre legal completo de su empresa, tal como aparece en su documento de constitucion. Ejemplo: Ferreteria y Suministros El Roble, S.A. de C.V." | Buena practica (PROMPT_BASE, seccion 11, hipotesis de producto) |
| Nombre comercial | Texto | Opcional | No aplica | Ninguna especifica | "El nombre con el que sus clientes conocen a la empresa, si es distinto de la razon social. Ejemplo: Ferreteria El Roble." | Buena practica |
| Identificacion tributaria (NIT) | Texto | Opcional en el onboarding (se puede pedir como obligatorio mas adelante, en MOD-008, para generar ciertos documentos formales) | No aplica | Formato numerico segun patron de NIT de El Salvador, si se llena | "Su Numero de Identificacion Tributaria. Puede completarlo despues si no lo tiene a la mano ahora." | Buena practica |
| Sector o industria | Seleccion unica | Obligatorio | Catalogo: Comercio, Manufactura, Servicios financieros, Salud, Tecnologia, Educacion, Construccion, Agroindustria, Otro | Debe seleccionar una opcion del catalogo | "Elija el sector que mejor describe la actividad principal de su empresa. Esto ayuda a personalizar las preguntas del siguiente paso, el Diagnostico." | Buena practica; precarga contexto para MOD-004 |
| Cantidad aproximada de empleados | Numero | Obligatorio | No aplica | Entero positivo | "Un numero aproximado basta. Esto ayuda al sistema a sugerir mas adelante si conviene separar funciones entre distintas personas, por ejemplo que quien aprueba no sea la misma persona que audita." | 05_tipos_de_usuario.md, seccion 5.4 [opinion de producto, umbral de 50 empleados sin respaldo legal] |
| Pais o paises donde opera | Seleccion multiple | Obligatorio | Catalogo de paises, con El Salvador preseleccionado | Al menos un pais seleccionado | "Marque todos los paises donde su empresa tiene operaciones u oficinas. Si sus datos se almacenan o procesan fuera de El Salvador, el Diagnostico se lo preguntara con mas detalle." | Buena practica; conecta con Arts. 44 y 45, que se resuelven en MOD-004/MOD-010, no aqui |
| Direccion principal | Texto largo | Opcional | No aplica | Ninguna especifica | "Direccion de la oficina principal o casa matriz." | Buena practica |
| Sitio web (si tiene) | Texto | Opcional | No aplica | Formato de URL valido, si se llena | "Si su empresa tiene pagina web, indiquela; ayuda a identificar canales digitales en el Diagnostico." | Buena practica |

### Paso 2: Primer usuario (Administrador)

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Nombre completo | Texto | Obligatorio | No aplica | No vacio | "La persona que va a configurar el sistema y podra administrar usuarios y permisos. Normalmente es quien esta completando este formulario." | Buena practica; dato personal minimo necesario para crear la cuenta |
| Correo electronico | Texto (correo) | Obligatorio | No aplica | Formato de correo valido, unico en el sistema | "Se usara para iniciar sesion y para recibir alertas importantes, como plazos que estan por vencer." | Buena practica |
| Cargo dentro de la empresa | Seleccion de catalogo o texto libre | Opcional | Catalogo: Gerente General, Gerente Administrativo, Jefe de TI, Jefe de RRHH, Jefe Legal/Compliance, Otro | Ninguna especifica | "Su cargo dentro de la empresa; ayuda a sugerir que otros roles podria necesitar asignar." | Buena practica |

### Paso 3: Usuarios adicionales (tabla repetible, de 0 a N filas, opcional en su totalidad)

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Nombre completo | Texto | Obligatorio si se agrega una fila | No aplica | No vacio | "Nombre de la persona que tendra acceso al sistema." | Buena practica; dato personal minimo del personal de la empresa cliente |
| Correo electronico | Texto (correo) | Obligatorio si se agrega una fila | No aplica | Formato valido, no duplicado dentro de la misma organizacion | "A esta direccion llegara la invitacion para crear su propia cuenta." | Buena practica |
| Rol propuesto | Seleccion unica | Obligatorio si se agrega una fila | Catalogo de roles estandar (05_tipos_de_usuario.md, 5.3), sin incluir Titular externo, Auditor externo ni Asesor externo, que no se asignan en el alta inicial | Debe pertenecer al catalogo | "Que podra hacer esta persona en el sistema. Puede cambiarlo despues desde Organizacion y Personas." | 05_tipos_de_usuario.md, seccion 5.3. El sistema puede sugerir un rol a partir del cargo, pero la confirmacion final la hace el Administrador (ver seccion H) |
| Area o departamento | Seleccion unica o texto libre | Opcional | Catalogo de areas capturadas en este mismo paso, o "Otra" | Ninguna especifica | "El area donde trabaja esta persona, si ya la tiene definida. Puede omitirlo y completarlo despues." | Buena practica |

### Paso 4: Delegado de Proteccion de Datos

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Su empresa, tiene ya una persona designada como Delegado de Proteccion de Datos | Seleccion unica | Obligatorio | "Si, ya esta designado" / "No, quiero designarlo ahora" / "No estoy seguro, necesito ayuda para decidir" | Debe elegir una opcion | "El Delegado es la persona responsable de atender las solicitudes de las personas sobre sus datos y de mantener contacto con la autoridad (la ACE). Hoy la ley exige tener uno en la mayoria de empresas privadas." | OBL-DPO-01, Arts. 15 y 17 LPDP (fundamento ampliado en MOD-002) |
| Nombre del Delegado | Texto | Obligatorio si la respuesta anterior no fue "No estoy seguro" | No aplica | No vacio | "Nombre completo de la persona designada o que planea designar." | Buena practica; dato personal minimo, referencia hacia MOD-002 |
| Correo del Delegado | Texto (correo) | Obligatorio si la respuesta anterior no fue "No estoy seguro" | No aplica | Formato valido | "Se usara para invitarlo a completar su propio perfil en el modulo del Delegado." | Buena practica |
| El Delegado es interno o externo | Seleccion unica | Obligatorio si se completo el nombre | "Interno (empleado de la empresa)" / "Externo, persona natural" / "Externo, persona juridica" | Debe seleccionar una opcion | "Indique si es alguien de su planilla o un tercero contratado para esta funcion." | Art. 13 y 14 Lineamientos DPO (se profundiza en MOD-002) |

### Paso 5: Confirmacion

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Acepto el aviso de que este sistema no sustituye asesoria legal | Booleano (casilla) | Obligatorio para poder finalizar | No aplica | Debe estar marcado | "Confirmo que entiendo que este sistema organiza y documenta el programa de proteccion de datos de mi empresa, pero no sustituye asesoria legal ni garantiza cumplimiento." | 04_objetivo_exacto_del_producto.md, secciones 1.2 y 1.3 |

**Minimizacion de datos personales.** Los unicos campos de este modulo que contienen datos personales son los nombres y correos electronicos de personas identificadas: el Administrador (Paso 2), los usuarios invitados (Paso 3) y el Delegado (Paso 4), todos ellos personal o colaboradores de la propia empresa cliente, no titulares finales. Es el minimo indispensable para crear cuentas de acceso y enviar invitaciones. El modulo no solicita documentos de identidad, fecha de nacimiento, fotografias, datos sensibles ni ningun dato de los titulares con los que la empresa trata datos (clientes, empleados, candidatos); esos se registran mas adelante, y solo como metadatos, en MOD-004 y MOD-006 (privacy by design, consistente con el anti-feature 8 de `22_anti_features.md`: nunca copiar bases de datos completas del cliente).

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Registro de Organizacion activo | Los campos del Paso 1 (razon social, sector, tamano, paises, etc.) | Registro estructurado en MOD-001 | Al confirmar el Paso 5 | MOD-001; visible para todos los roles internos segun sus permisos alli definidos |
| Cuenta y rol del Administrador | Nombre, correo, cargo, rol "Administrador de la organizacion" | Cuenta de usuario activa | Al confirmar el Paso 2 dentro del wizard (activa formalmente al cerrar el Paso 5) | MOD-001; el propio Administrador (ya esta autenticado) |
| Cuentas y roles de los usuarios adicionales | Nombre, correo, rol propuesto, area | Cuenta de usuario en estado "invitado", mas correo de invitacion | Al confirmar el Paso 5 | MOD-001 (registro de usuarios); MOD-022 Notificaciones (envio del correo); el propio usuario invitado |
| Registro inicial del Delegado | Nombre, correo, tipo interno/externo, estado "designacion en curso" o "por confirmar" | Registro en MOD-002 | Al confirmar el Paso 5, solo si la respuesta del Paso 4 fue "ya designado" o "designarlo ahora" | MOD-002; la persona designada, via invitacion |
| Tarea "Resolver la designacion del Delegado" | Recordatorio con ayuda contextual del Art. 15 y 17 | Tarea en el Centro de Tareas | Al confirmar el Paso 5, solo si la respuesta del Paso 4 fue "no estoy seguro" | MOD-021, asignada al Administrador |
| Tarea "Iniciar el Diagnostico de Cumplimiento" | Enlace directo a MOD-004 | Tarea en el Centro de Tareas | Siempre, al completar el onboarding | MOD-021, asignada al Administrador o a quien este designe |
| Evento de auditoria "onboarding completado" | Fotografia (snapshot) de todos los valores capturados en los 5 pasos, con fecha y usuario | Evento inmutable de auditoria | Al confirmar el Paso 5 | MOD-019 Centro de Evidencias; consultable por Auditor y Administrador |
| Reporte "Resumen de configuracion inicial" | Ver seccion N | PDF | Bajo demanda, despues de completar el onboarding | Administrador; insumo para el paquete de evidencias de auditoria |
| Alertas y recordatorios | Ver seccion I | Notificacion en plataforma y/o correo | Segun cada disparador | Administrador (principalmente) |

---

## F. Workflow

MOD-003 es, por diseno, un proceso lineal de una sola pasada por organizacion: no es repetible como el Diagnostico (decision de alcance 2.7.5).

```
                    +----------------+
                    | NO_INICIADO    |
                    +----------------+
                            |
                     iniciar wizard
                            v
        +-------------------------------------+
        |           EN_PROGRESO                |
        |  (Paso 1 -> Paso 2 -> Paso 3 ->       |
        |   Paso 4 -> Paso 5, con autoguardado) |
        +-------------------------------------+
              |  ^                        |
   inactividad|  | reingresar al wizard   | confirmar y finalizar
   prolongada |  |                        | (Paso 5)
              v  |                        v
        +----------------+          +----------------+
        |  ABANDONADO    |          |  COMPLETADO    |
        +----------------+          +----------------+
                                       |  (terminal para el wizard;
                                       |   cambios futuros -> MOD-001)
                                       v
                              organizacion operativa,
                              redirige a MOD-004
                              Diagnostico de Cumplimiento

   (desde NO_INICIADO, EN_PROGRESO o ABANDONADO)
              |
   cancelacion de la cuenta antes de completar
              v
        +----------------+
        |  ARCHIVADO     |  (terminal, historico, solo lectura)
        +----------------+
```

### Tabla de transiciones

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (inicio) | Se crea la cuenta de la organizacion (alta comercial, fuera del alcance funcional de este modulo) | Correo de contacto verificado | NO_INICIADO | Proceso externo de alta comercial | Se crea la tarea "Completar configuracion inicial" en MOD-021; se envia la alerta de bienvenida (seccion I) |
| NO_INICIADO | "Iniciar configuracion" | Usuario autenticado con correo verificado | EN_PROGRESO | Administrador (usuario que se registro) | Se abre el Paso 1; evento de auditoria "onboarding iniciado" |
| EN_PROGRESO | "Guardar y continuar" en cualquier paso | Campos obligatorios del paso valido | EN_PROGRESO (avanza al siguiente paso) | Administrador | Autoguardado del paso; se actualiza el indicador de progreso (paso X de 5) |
| EN_PROGRESO | Responder la pregunta del Delegado (Paso 4) | Seleccion obligatoria entre las 3 opciones | EN_PROGRESO | Administrador | Segun la respuesta: crea o no el registro inicial en MOD-002, o crea la tarea CRITICAL de la seccion I (regla detallada en seccion G) |
| EN_PROGRESO | Inactividad sin completar ningun paso nuevo durante N dias (configurable, por defecto 5) | Ningun paso avanzado en el periodo | ABANDONADO | Automatizacion del sistema | Alerta WARNING al Administrador (seccion I); no se pierde el avance ya guardado |
| ABANDONADO | Reingresar al wizard | Usuario autenticado | EN_PROGRESO | Administrador | Continua desde el ultimo paso guardado |
| EN_PROGRESO | "Confirmar y finalizar" (Paso 5) | Todos los campos obligatorios de los pasos 1, 2 y 5 completos; casilla del descargo marcada; al menos un usuario Administrador activo | COMPLETADO | Administrador | Se activa la Organizacion en MOD-001; se crean/activan los usuarios y roles; se envian las invitaciones (MOD-022); se crea el registro del Delegado en MOD-002 si aplica; evento de auditoria "onboarding completado"; se crea la tarea "Iniciar el Diagnostico" y se redirige a MOD-004 |
| COMPLETADO | (no hay reapertura del wizard) | No aplica | COMPLETADO (terminal para este modulo) | No aplica | Cualquier cambio posterior a organizacion, usuarios o roles se hace directamente en MOD-001; el registro del onboarding queda archivado como evidencia de solo lectura, consultable pero no editable |
| NO_INICIADO / EN_PROGRESO / ABANDONADO | Cancelacion de la cuenta antes de completar el onboarding | Decision de cancelacion tomada fuera de este modulo (proceso comercial) | ARCHIVADO | Proceso externo de baja comercial | El registro EN_PROGRESO se conserva como historico sin eliminarse; las invitaciones no aceptadas quedan revocadas automaticamente |

**Estados terminales.** COMPLETADO y ARCHIVADO son terminales para este modulo. No existe una accion de "reabrir el onboarding": esto es deliberado, porque una vez que la organizacion existe, cualquier ajuste (agregar una sucursal, cambiar un rol, dar de baja a un usuario) debe quedar en el historial propio de MOD-001, con su propia trazabilidad de "quien cambio que", en vez de mezclarse con el registro fundacional del onboarding.

**Reapertura y registros vinculados.** No hay reapertura del wizard en si. Si la organizacion cancela su suscripcion antes de completar el onboarding, el registro pasa a ARCHIVADO sin eliminarse (principio 8 del mapa definitivo: "ningun cambio de estado normativo borra informacion; todo queda versionado con su historial", aplicado aqui tambien a la baja de una cuenta); las invitaciones pendientes de usuarios que no habian aceptado quedan revocadas automaticamente, y si la empresa reactiva su cuenta despues, se le presenta un onboarding nuevo (no se reutiliza el registro archivado, que queda solo como historico).

---

## G. Automatizaciones

| # | Disparador | Condicion | Accion | Configurable por la empresa |
|---|---|---|---|---|
| 1 | Se confirma el Paso 1 (datos de la empresa) | Cantidad de empleados registrada | Calcula si la empresa supera el umbral de 50 empleados y marca la bandera "separacion de funciones recomendada / exigida" que MOD-001 usara despues | No (umbral fijado por el producto; ver 05_tipos_de_usuario.md 5.4) |
| 2 | Se agrega un usuario con rol "Delegado de Proteccion de Datos" en el Paso 3, o se completa el Paso 4 con "ya designado" / "designarlo ahora" | Rol = Delegado, o respuesta del Paso 4 distinta de "no estoy seguro" | Crea automaticamente el registro inicial del Delegado en MOD-002 en estado "designacion en curso"; siembra en MOD-023 (Calendario y Motor de Plazos) el conteo del plazo de comunicacion a la ACE, 15 dias habiles (OBL-DPO-03), a partir de la fecha en que MOD-002 confirme el nombramiento | No |
| 3 | Se responde "no estoy seguro" en el Paso 4 | Ninguna adicional | Crea la tarea CRITICAL "Resolver si su empresa necesita designar un Delegado de Proteccion de Datos" en MOD-021, con ayuda contextual de los Arts. 15 y 17 | No |
| 4 | Se completa el Paso 5 (confirmar y finalizar) | Todos los campos obligatorios validos | Activa la Organizacion en MOD-001; envia las invitaciones por correo (via MOD-022) a cada usuario agregado, con un enlace de activacion de un solo uso y con vencimiento | No |
| 5 | El onboarding pasa a COMPLETADO | Siempre | Crea la tarea "Completar el Diagnostico de Cumplimiento" en MOD-021 y redirige automaticamente a MOD-004 | No |
| 6 | Transcurren N dias sin actividad en EN_PROGRESO | Ningun paso nuevo completado en el periodo | Envia un recordatorio (MOD-022) y marca el estado ABANDONADO | Si, el numero de dias es configurable por el equipo del producto (por defecto 5); no es una opcion visible para la empresa en el MVP |
| 7 | Un usuario invitado no acepta su invitacion | Estado de la invitacion = pendiente, transcurridos 5 y 10 dias | Envia recordatorios automaticos y alerta al Administrador; a los 30 dias marca la invitacion como "vencida" | Si, los plazos de recordatorio son configurables por el equipo del producto |
| 8 | Se ingresa un correo de usuario invitado con un dominio distinto al de correos ya registrados en la misma organizacion | Dominio del correo distinto | Muestra una advertencia en pantalla, no bloqueante: "el correo no coincide con el dominio de los demas usuarios de su organizacion, verifique antes de continuar" | No (advertencia fija; opinion de producto, medida de seguridad basica) |
| 9 | Se selecciona un cargo del catalogo en el Paso 2 o Paso 3 que coincide con un rol del catalogo de roles | Coincidencia exacta cargo-rol (por ejemplo, "Jefe de TI" sugiere el rol Responsable de Seguridad/IT) | Sugiere automaticamente ese rol en el campo "Rol propuesto", dejandolo editable | Si, en el sentido de que la sugerencia siempre puede sobrescribirse manualmente; ver limite en seccion H |

---

## H. Decisiones que NO debe automatizar

1. **Decidir si la empresa realmente necesita un Delegado de Proteccion de Datos y que tipo de vinculo (interno o externo) le conviene.** El sistema solo registra la respuesta del Paso 4 y crea la tarea correspondiente; nunca concluye "su empresa no necesita Delegado" ni "le conviene contratar uno externo". Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada." Razon: la ley (Arts. 15 y 17) exige la figura hoy para la generalidad del sector privado, con excepciones que dependen de un analisis caso por caso que el sistema no puede resolver con una sola pregunta.
2. **Asignar de forma definitiva el rol de cada usuario invitado a partir de su cargo declarado.** El sistema sugiere un rol (automatizacion 9 de la seccion G), pero nunca lo fija sin que el Administrador lo confirme, y nunca sugiere de forma automatica los roles sensibles Aprobador o Auditor. Texto de advertencia visible junto a la sugerencia: "Esta es una sugerencia; confirme el rol antes de continuar. Requiere validacion de la organizacion." Razon: un rol mal asignado desde el primer dia puede romper la separacion de funciones antes de que la organizacion siquiera empiece a operar.
3. **Determinar si la empresa esta excluida del ambito de la LPDP (exclusiones del Art. 3).** Esa evaluacion pertenece exclusivamente al Diagnostico de Cumplimiento (MOD-004, obligaciones OBL-AMB-02 a 04); el onboarding nunca afirma, a partir del sector o el tamano declarados en el Paso 1, que la empresa "esta" o "no esta" sujeta a la ley. Razon: los datos del Paso 1 son insuficientes para esa determinacion; solo el cuestionario detallado del Diagnostico puede acercarse a ella, y siempre con la advertencia de que requiere criterio juridico.
4. **Confirmar que la persona designada como Delegado cumple los requisitos legales** (grado universitario, mayor de 21 anos, experiencia acreditada, certificacion ante la ACE, Art. 5 y 12 Lineamientos DPO). El onboarding solo captura nombre, correo y tipo interno/externo; esa verificacion completa vive en MOD-002 y nunca se da por cumplida automaticamente por haber pasado por este paso. Texto de advertencia en MOD-002 al recibir el registro: "Requiere validacion de la organizacion o asesoria especializada."
5. **Decidir la estructura definitiva de sucursales, areas o sociedades relacionadas de una organizacion compleja.** El onboarding solo captura la estructura inicial minima declarada (pais y, opcionalmente, area por usuario); cualquier reorganizacion societaria o multi-sociedad (por ejemplo, un grupo corporativo con varias razones sociales) requiere confirmacion posterior y criterio interno en MOD-001, y la vision consolidada multi-sociedad queda fuera del MVP (ver `05_tipos_de_usuario.md`, decision 2.7.31, y seccion Q de esta ficha).

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia o repeticion | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Bienvenida: configure su organizacion | Cuenta creada, onboarding en NO_INICIADO | INFO | Administrador (usuario que se registro) | Correo + notificacion en plataforma | Una vez, con un recordatorio a las 48 horas si no se inicia | Ninguno (todavia no existe otro usuario al que escalar) | El wizard entra a EN_PROGRESO |
| Configuracion inicial incompleta | Onboarding en EN_PROGRESO sin avance por 5 dias (configurable) | WARNING | Administrador | Correo + plataforma | Cada 5 dias, hasta 3 recordatorios | Ninguno | Se completa el siguiente paso, o el onboarding finaliza |
| Debe resolver si necesita un Delegado de Proteccion de Datos | Respuesta "no estoy seguro" en el Paso 4 | CRITICAL | Administrador (y el Delegado, si ya fue invitado por otra via) | Plataforma + correo | Persistente, reaparece cada 7 dias hasta resolverse | A los 15 dias habiles sin resolver, se hace visible en el dashboard de Gerencia (referencia al plazo de OBL-DPO-03) | MOD-002 registra un Delegado confirmado, o queda documentada una decision explicita de la organizacion sobre por que no aplica |
| Invitacion de usuario pendiente de aceptar | Se envia una invitacion y no se acepta | INFO, pasa a WARNING a los 10 dias | Administrador | Correo + plataforma | Recordatorios a los 5 y 10 dias | A los 30 dias se marca "invitacion vencida" y se notifica al Administrador para reenviarla o retirarla | El usuario invitado acepta y crea su cuenta |
| Onboarding abandonado | El estado pasa a ABANDONADO | WARNING | Administrador | Correo | Una vez al entrar al estado, luego semanal | Ninguno | El Administrador reingresa al wizard |
| El correo no coincide con el dominio de la organizacion | Validacion de dominio en el Paso 2 o 3 | INFO | Administrador (en pantalla, en el momento) | En pantalla, sin notificacion asincrona | Una vez por intento | No aplica | Se corrige el campo o se confirma explicitamente que es correcto |

---

## J. Evidencia

MOD-003 no es propietario de ninguna obligacion (seccion A), por lo que su evidencia no "prueba" directamente ningun OBL-ID por si sola; funciona como respaldo indirecto, registrando el momento y el modo en que se sembraron los datos que despues prueban obligaciones concretas en MOD-001 y, sobre todo, en MOD-002.

- **Registro con fecha y hora de creacion de la organizacion**, con el usuario que la creo (siempre el Administrador que ejecuto el wizard). Sirve de linea base historica: si mas adelante se audita cuando empezo a operar el programa de proteccion de datos de la empresa dentro del sistema, este es el primer evento verificable.
- **Historial inmutable de cada paso completado**, con una fotografia (snapshot) de los valores capturados en ese paso, fecha y usuario. Permite reconstruir exactamente que informacion se declaro en el momento del alta, incluso si despues cambia en MOD-001.
- **Evidencia de aceptacion del descargo de responsabilidad**: el texto exacto mostrado en el Paso 5, la fecha y el usuario que lo acepto. Es evidencia de que la empresa fue informada, desde el primer uso, de los limites del sistema (seccion 1.2 y 1.3 de `04_objetivo_exacto_del_producto.md`).
- **Registro de las invitaciones enviadas y su aceptacion**: quien invito, a quien, cuando, y cuando (o si) cada usuario acepto. Alimenta la trazabilidad de asignacion de roles que despues gestiona MOD-001.
- **Evento de auditoria "onboarding completado"**, con la fotografia final de la organizacion, usuarios y roles al cierre del wizard. Es especialmente relevante como insumo indirecto para OBL-DPO-02 y OBL-DPO-03 (Arts. 8 y 10 LPDP): la fecha en que se sembro el registro del Delegado en el Paso 4 es el punto de partida que MOD-002 usa para calcular y vigilar esos plazos legales, aunque el calculo y el cumplimiento formal de esas obligaciones sean responsabilidad de MOD-002 y MOD-023, no de este modulo.
- **Conservacion.** Este modulo no define un plazo de retencion propio (no aplica el plazo de 5 o 10 anos de expedientes ARCO-POL o de documentacion del aviso de privacidad, que corresponden a otro tipo de evidencia). El registro del onboarding se conserva mientras la organizacion mantenga su cuenta activa, y despues, si la cuenta se cancela, segun la politica de retencion documental de cumplimiento propio que administra MOD-016 (Retencion y Eliminacion), sin que MOD-003 fije aqui un numero de anos autoritativo.

---

## K. Documentos asociados

- **Documentos requeridos como entrada.** Ninguno es obligatorio para completar el onboarding. No se exige subir el documento de constitucion de la empresa, el NIT verificado ni ningun otro documento formal en este paso (ver seccion Q, funcionalidad FUTURE de verificacion documental tipo KYB).
- **Documentos generados.** El onboarding no genera documentos legales (eso ocurre en MOD-008, despues del diagnostico y del plan). Genera unicamente el reporte operativo "Resumen de configuracion inicial" (ver seccion N), que no tiene valor legal por si mismo distinto del evento de auditoria descrito en la seccion J.
- **Plantillas que el sistema provee.**
  - Correo de invitacion a usuarios nuevos (variables: nombre del invitado, nombre de la organizacion, rol asignado, enlace de activacion de un solo uso). No requiere validacion de la organizacion: es texto operativo, no un documento con contenido legal.
  - Correo de bienvenida al Administrador que acaba de crear la cuenta.
- **Anexos y evidencias documentales.** No aplica: este modulo no admite adjuntos de archivos (ver seccion C, accion "Adjuntar evidencia").

---

## L. Dependencias

```
              (alta comercial / compra de la suscripcion,
               evento externo fuera de este modulo)
                            |
                            v
                    MOD-003 Onboarding
                    /        |         \
                   v         v          v
              MOD-001    MOD-002     MOD-004
           Organizacion  Delegado /  Diagnostico
           y Personas    Resp. Int.  de Cumplimiento
                    \        |         /
                     v       v        v
        MOD-021 Centro de Tareas | MOD-022 Notificaciones |
        MOD-023 Calendario (solo si hay Delegado declarado) |
        MOD-026 Centro de Ayuda (ayuda contextual del wizard)
```

- **Entra desde:** ninguno. MOD-003 es el punto de entrada funcional del producto; el unico disparador previo es un evento externo al analisis funcional (el alta comercial de la cuenta), tal como lo confirma `mapa_modulos.json` (`"depende_de": []`).
- **Sale hacia:**
  - **MOD-001 Organizacion y Personas:** recibe los datos de la empresa (Paso 1) y las cuentas y roles de los usuarios (Pasos 2 y 3); MOD-003 "ejecuta el alta de MOD-001", segun la propia definicion del mapa definitivo.
  - **MOD-002 Delegado / Responsable Interno de Datos:** recibe el registro inicial del Delegado, si el Paso 4 concluyo en "ya designado" o "designarlo ahora".
  - **MOD-004 Diagnostico de Cumplimiento:** recibe el disparo de inicio (la tarea "Iniciar el Diagnostico") y el contexto de sector, tamano y paises capturado en el Paso 1, que el Diagnostico puede usar para priorizar sus propias preguntas.
- **Toca ademas, de forma transversal:** MOD-021 Centro de Tareas (crea las tareas iniciales), MOD-022 Notificaciones (envia invitaciones y recordatorios), MOD-023 Calendario y Motor de Plazos (si ya se declaro un Delegado, siembra el conteo del plazo de 15 dias habiles que MOD-002 vigilara) y MOD-026 Centro de Ayuda (provee los textos de ayuda contextual del wizard, ver seccion R).
- **Que pasa si un modulo dependiente no existe en el MVP.** No aplica como escenario real: MOD-001, MOD-002 y MOD-004 estan clasificados MUST HAVE en el mapa definitivo y siempre existen desde el primer lanzamiento del producto. Los transversales MOD-021, MOD-022, MOD-023 y MOD-026 tambien son MUST HAVE. Por lo tanto, MOD-003 nunca opera en un escenario donde alguno de sus destinos no exista.

---

## M. Dashboard

MOD-003 aporta indicadores de "estado de configuracion inicial", nunca un porcentaje de cumplimiento legal, consistente con `04_objetivo_exacto_del_producto.md` seccion 1.2.

| Indicador | Formula | Semaforo | Vista |
|---|---|---|---|
| Configuracion inicial completada | Estado del onboarding de la organizacion (NO_INICIADO / EN_PROGRESO / ABANDONADO / COMPLETADO) | Verde si COMPLETADO; amarillo si EN_PROGRESO o ABANDONADO dentro de los primeros 5 dias; rojo si ABANDONADO por mas de 5 dias | Gerencia, Responsable (Administrador) |
| Aceptacion de invitaciones | Usuarios que aceptaron su invitacion, dividido entre usuarios invitados, por 100 | Verde si 100%; amarillo si hay invitaciones pendientes dentro del plazo normal (menos de 10 dias); rojo si hay invitaciones vencidas | Responsable (Administrador), Auditor |
| Estado de la designacion del Delegado | Estado heredado de MOD-002 a partir de la semilla sembrada en el Paso 4 del onboarding (confirmado / en curso / pendiente de resolver) | Verde si confirmado; amarillo si en curso; rojo si pendiente de resolver | Legal / Delegado, Gerencia |
| Fecha y usuario de creacion de la organizacion | Dato directo del evento de auditoria "onboarding completado" | No aplica semaforo, es un dato informativo | Auditor |

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Resumen de configuracion inicial | Datos de la organizacion (Paso 1), lista de usuarios y roles asignados, estado de la designacion del Delegado al cierre, fecha de finalizacion y usuario que lo completo | Ninguno (reporte unico por organizacion, no es un listado filtrable) | PDF | Administrador | Si; sirve como primera pieza del paquete de evidencias de MOD-019, para mostrar cuando y como se constituyo el programa dentro del sistema |
| Historial de invitaciones y aceptaciones | Cada invitacion enviada, con fecha de envio, fecha de aceptacion o de vencimiento, rol asignado | Rango de fechas, estado (pendiente / aceptada / vencida) | CSV o XLSX | Administrador, Auditor | Si, como respaldo de la trazabilidad de asignacion de accesos desde el origen |

---

## O. Historial

Eventos que deben quedar en el historial propio del modulo y en la auditoria transversal (MOD-019):

- Creacion de la cuenta de la organizacion e inicio del onboarding (usuario, fecha y hora).
- Cada paso guardado, con el valor capturado en ese momento (fotografia del paso).
- Cambios de campo dentro de un mismo paso, si el usuario corrige un dato antes de avanzar al siguiente (valor anterior y valor nuevo).
- Envio de cada invitacion (a quien, con que rol propuesto, cuando).
- Reenvio de una invitacion.
- Aceptacion de una invitacion (usuario, fecha).
- Vencimiento de una invitacion no aceptada.
- Respuesta a la pregunta del Delegado en el Paso 4 (que opcion se eligio).
- Creacion del registro inicial del Delegado en MOD-002 (evento cruzado, referenciado desde ambos modulos).
- Aceptacion del descargo de responsabilidad (texto mostrado, version, fecha, usuario).
- Cambio de estado: EN_PROGRESO a ABANDONADO, y de vuelta a EN_PROGRESO al reingresar.
- Finalizacion del onboarding (evento "completado", con la fotografia final).
- Archivado del registro por cancelacion de la cuenta antes de completar, con el motivo.
- Exportacion del "Resumen de configuracion inicial" (quien lo exporto, cuando).

Todos los eventos quedan con usuario, fecha y hora, y el motivo cuando aplique (por ejemplo, el motivo de la cancelacion, si el proceso comercial lo captura).

---

## P. Riesgos

| Riesgo | Tipo | Mitigacion de diseno |
|---|---|---|
| El sistema parece "decidir" que la empresa no necesita Delegado con solo la respuesta rapida del Paso 4 | Legal | La opcion "no estoy seguro" (y, de forma mas amplia, cualquier respuesta que no confirme una designacion ya hecha) nunca cierra el tema: genera una tarea CRITICAL persistente (seccion I) y muestra siempre el texto "requiere validacion de la organizacion o asesoria especializada"; el sistema nunca asume "no aplica" por defecto |
| Abandono del wizard por percibirse largo, o por pedir informacion que el usuario no tiene a mano en ese momento (por ejemplo, el NIT exacto o la lista completa de sucursales) | UX | Solo un numero minimo de campos es obligatorio para poder finalizar (razon social, sector, cantidad de empleados, pais, datos del Administrador, respuesta sobre el Delegado, aceptacion del descargo); el resto queda marcado como opcional y completable despues desde MOD-001; el progreso se guarda automaticamente en cada paso |
| El Administrador asigna mal el rol de un usuario desde el primer momento (por ejemplo, le da Auditor a quien tambien va a aprobar documentos), rompiendo la separacion de funciones desde el origen | Operativo | El wizard muestra una advertencia (no un bloqueo duro, dado que en este momento la organizacion todavia no esta activa) cuando detecta una combinacion de roles marcada como riesgosa en `05_tipos_de_usuario.md` seccion 5.4 |
| Se invita a usuarios con correos incorrectos o de dominios ajenos a la empresa, dando acceso potencial a personas equivocadas | Seguridad y privacidad | Validacion de formato de correo, advertencia de dominio distinto (automatizacion 8, seccion G), enlace de invitacion de un solo uso con vencimiento, verificacion del correo antes de activar la cuenta |
| La organizacion depende de una sola cuenta de Administrador, sin respaldo; si esa persona deja la empresa antes de invitar a alguien mas con permisos administrativos, la organizacion queda sin nadie que pueda gestionarla | Seguridad, operativo | El wizard recomienda (no obliga, en el MVP) invitar al menos a un segundo usuario con rol administrativo en el Paso 3; la recomendacion queda registrada como tal, sin bloquear el cierre del onboarding [opinion de producto] |

---

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Alta guiada de los datos basicos de la organizacion (razon social, sector, tamano, paises) | X | | | | Sin esto no puede operar ningun otro modulo; es una dependencia estructural de todo el sistema (principio 7b del mapa definitivo) |
| Alta del primer usuario Administrador e invitacion de usuarios adicionales con rol propuesto | X | | | | Dependencia estructural para el RBAC de MOD-001; sin usuarios no hay a quien asignar tareas |
| Pregunta inicial sobre la existencia o designacion del Delegado, con siembra del registro en MOD-002 | X | | | | El Delegado es OBLIGATORIO hoy (OBL-DPO-01, Arts. 15 y 17) con plazos ya corriendo; sembrar el registro desde el primer contacto reduce el riesgo de que la empresa lo olvide por completo |
| Texto de descargo de responsabilidad con aceptacion explicita | X | | | | Requisito transversal de todo el producto (04_objetivo_exacto_del_producto.md, secciones 1.2 y 1.3); debe mostrarse desde el primer uso |
| Creacion automatica de la tarea de inicio del Diagnostico y redireccion | X | | | | Sin esto el usuario podria completar el alta y abandonar el producto antes de llegar al valor real (Diagnostico y Plan) |
| Sugerencia automatica de rol segun el cargo declarado | | X | | | Mejora de velocidad y UX; si no existe, el Administrador simplemente selecciona el rol manualmente, sin bloquear el flujo |
| Estructura detallada de sucursales o areas dentro del propio wizard, mas alla del pais | | | X | | Se puede completar despues directamente en MOD-001 sin bloquear el cierre del onboarding; util pero no critico para el primer valor entregado |
| Verificacion de dominio corporativo de correo con validacion DNS real (mas alla de la advertencia visual) | | | X | | Mejora de seguridad razonable, pero no critica para que el onboarding funcional cumpla su proposito |
| Carga de documento de constitucion o de identificacion tributaria para verificacion tipo KYB | | | | X | No es exigido por la ley para operar el software; anadiria friccion y una capa de verificacion documental fuera del alcance de un producto de autogestion (relacionado con el anti-feature de no convertirse en un tramite adicional no solicitado) |
| Onboarding multi-sociedad o de grupo corporativo (una sola sesion que de de alta varias razones sociales relacionadas) | | | | X | La vision consolidada multi-sociedad es funcionalidad V1/Enterprise, segun la decision de alcance 2.7.31 de `05_tipos_de_usuario.md` |

**Version minima vendible.** Las cinco funcionalidades MUST HAVE de esta tabla ya constituyen, por si solas, la version minima util del modulo: permiten a una pyme de una sola sucursal completar su alta, dejar declarada (o al menos abierta y con tarea de seguimiento) la situacion de su Delegado, y llegar en la misma sesion al Diagnostico de Cumplimiento, que es exactamente el proposito que el mapa definitivo le asigna a este modulo ("guiar a la persona designada... a traves de la alta inicial... en la primera sesion... lista para el Diagnostico"). Las funcionalidades SHOULD HAVE y COULD HAVE mejoran la experiencia pero su ausencia no impide vender ni operar el modulo.

---

## R. Ayuda contextual (complemento obligatorio)

**1. Que es la "organizacion" en este sistema**
- Que es: es el espacio de trabajo unico de su empresa dentro del sistema, donde se guarda toda la informacion de su programa de proteccion de datos.
- Por que tengo que hacer esto: todo lo demas que va a usar (usuarios, tareas, diagnostico, documentos) depende de que esta informacion basica este completa y correcta desde el inicio.
- Fundamento: decision de diseno de producto (PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md, seccion "Modulo de organizacion"); no corresponde a un articulo especifico de la LPDP.
- Cuando necesito ayuda juridica: si tiene dudas sobre cual es la razon social correcta o si su empresa opera bajo varias sociedades relacionadas, consulte a su area legal o contable antes de continuar.

**2. Que es el Delegado de Proteccion de Datos**
- Que es: la persona, de su empresa o contratada externamente, responsable de atender las solicitudes de las personas sobre sus datos y de mantener el enlace con la autoridad reguladora (la ACE).
- Por que tengo que hacer esto: hoy la ley exige que la mayoria de empresas privadas tengan una persona en este rol. Si la reforma que fue aprobada por la Asamblea Legislativa llega a publicarse y entrar en vigencia, esta figura podria volverse opcional y sus funciones pasarian a un responsable interno designado por la empresa.
- Fundamento: OBL-DPO-01, Arts. 15 y 17 de la Ley para la Proteccion de Datos Personales (Decreto 144). Ver el modulo Delegado / Responsable Interno de Datos para el detalle completo.
- Cuando necesito ayuda juridica: para decidir quien debe ocupar este rol, o si su empresa puede prescindir de el en este momento, consulte asesoria especializada; el sistema no puede decidirlo por usted, solo dejar constancia de su respuesta y recordarselo.

**3. Que son los roles y por que debo asignarlos desde ahora**
- Que es: cada persona que use el sistema necesita un rol que defina que puede ver, crear o aprobar dentro de la plataforma.
- Por que tengo que hacer esto: evita que una sola persona controle todo el proceso sin ningun tipo de revision, y ordena desde el primer dia quien hace que dentro de su empresa.
- Fundamento: decision de producto (02_validacion/05_tipos_de_usuario.md, secciones 5.3 y 5.4); no es una exigencia expresa de la LPDP, salvo en el caso especifico del rol Delegado.
- Cuando necesito ayuda juridica: si tiene dudas sobre si una persona externa, por ejemplo un consultor, deberia tener acceso al sistema, consultelo con su area legal antes de invitarla.

**4. Por que tengo que aceptar el aviso sobre lo que este sistema no hace**
- Que es: un texto breve que explica que este sistema organiza y documenta el programa de proteccion de datos de su empresa, pero no sustituye asesoria legal ni garantiza que su empresa este cumpliendo la ley.
- Por que tengo que hacer esto: para evitar que usted o su empresa asuman, por error, que usar este sistema por si solo equivale a estar "en regla" con la Ley para la Proteccion de Datos Personales.
- Fundamento: decision de producto (02_validacion/04_objetivo_exacto_del_producto.md, secciones 1.2 y 1.3), apoyada en el principio general de que el software orienta, explica y organiza, pero nunca decide cuestiones juridicas por la empresa.
- Cuando necesito ayuda juridica: siempre que el sistema le muestre, en cualquier modulo, un texto que diga "requiere validacion de la organizacion o asesoria especializada".

**5. Que pasa despues de terminar esta configuracion inicial**
- Que es: al terminar estos 5 pasos, su empresa queda lista para el Diagnostico de Cumplimiento, el siguiente paso, donde se identifican en detalle los tratamientos de datos que su empresa realmente hace.
- Por que tengo que hacer esto: esta configuracion inicial solo prepara el terreno (quien es su empresa, quien va a usar el sistema); el Diagnostico es el que realmente descubre que obligaciones concretas le aplican a usted.
- Fundamento: decision de alcance 2.7.5 (02_validacion/02_validacion_de_la_idea.md): separar el alta de organizacion del cuestionario de obligaciones en dos pasos distintos.
- Cuando necesito ayuda juridica: no aplica en este punto especifico; es un paso operativo de configuracion, no una decision con contenido juridico.

---

## Nota final del agente (posibles desacuerdos o precisiones frente al mapa)

No se detecto ninguna contradiccion real frente a las fuentes de diseno ya decididas (`06_mapa_definitivo_de_modulos.md` y `mapa_modulos.json`). Una precision que vale la pena dejar registrada para quien lea esta ficha junto con `02_validacion_de_la_idea.md`:

- Las filas 23, 24 y 28 de la tabla de "faltantes" de `02_validacion_de_la_idea.md` (deteccion de las exclusiones del Art. 3, deteccion de operador de infraestructura critica, y WhatsApp Business como transferencia internacional implicita) mencionan "Onboarding" como modulo sugerido, junto con Diagnostico de Cumplimiento en el primer caso. Esta ficha sigue la version mas reciente y mas especifica de la decision, la del mapa definitivo: esas tres preguntas son parte del cuestionario del Diagnostico (MOD-004, area del prompt 9), no del alta de MOD-003 (area del prompt 8.3), porque `mapa_modulos.json` fija a MOD-003 sin ninguna obligacion colaboradora y con `"areas_prompt": ["8.3"]` exclusivamente, mientras que la propia ficha de MOD-004 en `06_mapa_definitivo_de_modulos.md` ya incluye explicitamente "biometria, salud, cloud, datos fuera del pais" dentro de su cuestionario guiado. No se trata de un error del mapa sino de una evolucion normal entre un documento de hallazgos preliminares (`02_validacion_de_la_idea.md`) y el mapa definitivo que lo sustituye para todo efecto posterior; se deja esta nota solo para que quien redacte la ficha de MOD-004 confirme que esas tres preguntas quedan efectivamente dentro de su cuestionario guiado, y no se pierdan entre ambos modulos.
