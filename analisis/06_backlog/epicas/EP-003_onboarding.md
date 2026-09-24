# EP-003 Onboarding (MOD-003)

**Objetivo.** Que una empresa pueda, en una sola sesion guiada, dar de alta su organizacion, su primer Administrador y usuarios adicionales, dejar declarada la situacion de su Delegado de Proteccion de Datos, aceptar el descargo de responsabilidad, y llegar lista al Diagnostico de Cumplimiento.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R1 | 12 | 45 | 45 | 0 | [MOD-003](../../03_modulos/MOD-003_ficha.md) |

**Notas de la epica.**

- Contradiccion de obligatoriedad del campo NIT en el Paso 1: la seccion D de la ficha lo marca opcional, pero la seccion P de la misma ficha y la seccion P de MOD-001 lo tratan como parte de los 5 campos obligatorios del alta minima. Se adopto NIT como obligatorio en HU-003-02, siguiendo la resolucion ya documentada en 04_secciones/15_onboarding.md (Contradicciones, punto 1), que da prioridad a MOD-001 por ser la propietaria de la entidad Organizacion.
- Nombre de la tarea automatica de cierre del onboarding: la seccion E de la ficha la llama 'Iniciar el Diagnostico de Cumplimiento' y 04_secciones/15_onboarding.md usa el mismo nombre, mientras que la seccion G (automatizacion 5) y 04_secciones/12_tareas_y_alertas.md (12.2.3) la llaman 'Completar el Diagnostico de Cumplimiento'. Se adopto 'Iniciar el Diagnostico de Cumplimiento' en HU-003-08 por coincidir entre dos fuentes independientes.
- Momento exacto de creacion del registro del Delegado en MOD-002: la seccion G (automatizacion 2) se puede leer como que ocurre ya al completar el Paso 4, pero la seccion F (tabla de transiciones, la fuente especifica de estados) la ubica como efecto de 'Confirmar y finalizar' (transicion a COMPLETADO). HU-003-05 sigue la seccion F como version autoritativa.
- La advertencia de 'combinacion de roles riesgosa' del Paso 3 (seccion C) se redacto siguiendo el texto literal de la ficha (HU-003-04, criterio 7). El propio Paso 3 asigna un solo rol por usuario invitado, por lo que ninguna fuente precisa la mecanica exacta de deteccion de una 'combinacion' dentro de una sola alta inicial; se deja como detalle de diseno tecnico, fiel al texto de la ficha.
- Se excluyeron de esta epica, por indicacion directa del encargo y por ser SHOULD HAVE o FUTURE en la tabla Q de la ficha: la sugerencia automatica de rol segun el cargo declarado (automatizacion 9), la verificacion de dominio de correo con DNS real, la estructura detallada de sucursales o areas dentro del wizard, y la carga de documentos para verificacion tipo KYB.
- Se agregaron HU-003-10, HU-003-11 y HU-003-12 (historial, exportacion de reportes y gestion de invitaciones) que no son filas literales de la tabla Q, pero si son comportamiento explicito de las funcionalidades MUST HAVE (permisos de Ver/Exportar de la seccion C, reportes de la seccion N, automatizacion 7 de la seccion G), conforme al alcance de cobertura completa que pide la seccion 3 de las instrucciones comunes.
- Los indicadores del Dashboard (seccion M de la ficha) no se modelaron como HU propias de esta epica: son datos que MOD-003 ya deja disponibles (estado del onboarding, aceptacion de invitaciones, estado heredado de la designacion del Delegado) para que el Dashboard (MOD-020, fuera de este encargo) los consuma y visualice.
- El umbral de 50 empleados para la bandera de separacion de funciones (HU-003-02) y los plazos de recordatorio y vencimiento de invitacion de 5, 10 y 30 dias (HU-003-12) son decisiones de producto sin respaldo legal, ya senaladas como pendientes de validar en PP-PROD-04 y PP-PROD-05 de 04_secciones/24_preguntas_pendientes.md.
- Las acciones 'Comentar' y 'Adjuntar evidencia' de la tabla de permisos (seccion C) no generan HU porque la propia ficha declara que no aplican a ningun rol en este modulo (el wizard no admite hilos de comentarios ni adjuntos de archivos).

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-003-01 | Iniciar la sesion guiada de configuracion inicial | Administrador de la organizacion | 3 | R1 | 5 | MOD-021, MOD-022 |
| HU-003-02 | Completar los datos basicos de la organizacion | Administrador de la organizacion | 3 | R1 | 9 | HU-003-01, MOD-001 |
| HU-003-03 | Registrar al primer usuario Administrador de la organizacion | Administrador de la organizacion | 2 | R1 | 9 | HU-003-02, MOD-001 |
| HU-003-04 | Invitar usuarios adicionales con su rol propuesto | Administrador de la organizacion | 3 | R1 | 9 | HU-003-03, MOD-001 |
| HU-003-05 | Responder si la organizacion ya tiene o va a designar un Delegado, y sembrar su registro | Administrador de la organizacion | 5 | R1 | 10 | HU-003-04, MOD-002, MOD-023 |
| HU-003-06 | Registrar que la empresa no esta segura sobre el Delegado y crear la tarea critica de seguimiento | Administrador de la organizacion | 3 | R1 | 10 | HU-003-04, MOD-021, MOD-022, MOD-023 |
| HU-003-07 | Aceptar el descargo de responsabilidad y confirmar la finalizacion de la configuracion inicial | Administrador de la organizacion | 8 | R1 | 10 | HU-003-02, HU-003-03, HU-003-05, HU-003-06, MOD-001, MOD-022 |
| HU-003-08 | Crear automaticamente la tarea de iniciar el Diagnostico y redirigir a MOD-004 | Administrador de la organizacion | 3 | R1 | 10 | HU-003-07, MOD-021, MOD-004 |
| HU-003-09 | Guardar automaticamente el avance y reanudar la configuracion inicial tras un periodo de inactividad | Administrador de la organizacion | 5 | R1 | 11 | HU-003-02, MOD-022 |
| HU-003-10 | Consultar el historial de la configuracion inicial | Administrador de la organizacion | 2 | R1 | 11 | HU-003-07 |
| HU-003-11 | Exportar el resumen de configuracion inicial y el historial de invitaciones | Administrador de la organizacion | 3 | R1 | 11 | HU-003-07, HU-003-10 |
| HU-003-12 | Gestionar el estado de las invitaciones enviadas | Administrador de la organizacion | 5 | R1 | 11 | HU-003-07, MOD-022 |

## Historias

### HU-003-01. Iniciar la sesion guiada de configuracion inicial

**Como** Administrador de la organizacion, **quiero** que al crearse la cuenta de mi empresa el sistema me reciba con una alerta de bienvenida y pueda iniciar de inmediato el wizard de configuracion, **para** comenzar a organizar el programa de proteccion de datos de mi empresa desde el primer contacto con el sistema.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 5 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que se crea la cuenta de la organizacion (alta comercial) con el correo de contacto verificado, cuando el proceso externo de alta finaliza, entonces el onboarding queda en estado NO_INICIADO, se crea la tarea Completar configuracion inicial en el Centro de Tareas y se envia la alerta INFO Bienvenida configure su organizacion por correo y en plataforma al Administrador.
2. Dado que el onboarding esta en NO_INICIADO y no se ha iniciado la configuracion en 48 horas, cuando se cumple ese plazo, entonces el sistema envia un recordatorio de la alerta de bienvenida.
3. Dado que el Administrador esta autenticado con correo verificado y el onboarding esta en NO_INICIADO, cuando selecciona Iniciar configuracion, entonces el estado cambia a EN_PROGRESO, se abre el Paso 1 del wizard y se registra el evento de auditoria onboarding iniciado con usuario y fecha.
4. Dado que el onboarding aun esta en NO_INICIADO, cuando se consulta el Centro de Tareas, entonces la tarea Completar configuracion inicial aparece asignada al Administrador y sigue pendiente hasta que el wizard avanza.
5. Dado que un usuario no autenticado o sin correo verificado intenta acceder a Iniciar configuracion, cuando lo intenta, entonces el sistema no permite el acceso al wizard.

**Reglas de negocio**

- El onboarding es un proceso lineal de una sola pasada por organizacion, no repetible (seccion F).
- El alta comercial de la cuenta es un evento externo, fuera del alcance funcional de este modulo (seccion L).

**Fuera de alcance**

- El proceso comercial de venta y creacion de la cuenta en si.
- El contenido del Paso 1, cubierto en HU-003-02.

- Referencia: MOD-003 seccion F tabla de transiciones filas (inicio) y NO_INICIADO a EN_PROGRESO; seccion I fila Bienvenida

### HU-003-02. Completar los datos basicos de la organizacion

**Como** Administrador de la organizacion, **quiero** registrar los datos basicos de mi empresa (razon social, NIT, sector, cantidad de empleados y paises donde opero) en el Paso 1 del wizard, **para** dejar identificada mi organizacion con lo minimo indispensable para que el resto del sistema pueda operar.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 9 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-003-01
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado que el onboarding esta en EN_PROGRESO en el Paso 1, cuando el Administrador completa razon social (minimo 3 caracteres), NIT, sector o industria (una opcion del catalogo), cantidad aproximada de empleados (numero entero positivo) y al menos un pais (con El Salvador preseleccionado) y confirma Guardar y continuar, entonces el sistema guarda el paso automaticamente y avanza al Paso 2.
2. Dado que el Administrador deja vacia la razon social, el NIT, no selecciona sector, no indica cantidad de empleados o no selecciona ningun pais, cuando confirma Guardar y continuar, entonces el sistema no avanza de paso y muestra el error especifico del campo faltante.
3. Dado que el Administrador escribe una cantidad de empleados que no es un numero entero positivo, cuando intenta guardar, entonces el sistema rechaza el valor y muestra el error de validacion.
4. Dado que el Administrador completa el sitio web con un formato que no es una URL valida, cuando intenta guardar, entonces el sistema muestra el error de formato sin bloquear los demas campos opcionales.
5. Dado que el nombre comercial, la direccion principal y el sitio web quedan vacios, cuando el Administrador guarda el paso, entonces el sistema permite avanzar porque son opcionales.
6. Dado que el Administrador consulta la ayuda contextual del Paso 1, cuando la abre, entonces ve el texto Que es la organizacion en este sistema (que es, por que, fundamento, cuando necesito ayuda juridica) de la seccion R de la ficha.
7. Dado que se confirma el Paso 1 con la cantidad de empleados registrada, cuando el sistema guarda el paso, entonces calcula si la empresa supera el umbral de 50 empleados y marca la bandera de separacion de funciones recomendada o exigida que MOD-001 usara despues, sin bloquear el avance del wizard en ningun caso.

**Reglas de negocio**

- Razon social obligatoria, minimo 3 caracteres.
- NIT tratado como obligatorio en el Paso 1 (ver discrepancia con la seccion D de la ficha en notas_epica).
- Sector o industria obligatorio, catalogo cerrado (Comercio, Manufactura, Servicios financieros, Salud, Tecnologia, Educacion, Construccion, Agroindustria, Otro).
- Cantidad de empleados obligatoria, entero positivo.
- Pais o paises obligatorio, seleccion multiple, El Salvador preseleccionado.
- El sistema no precarga ningun campo de este paso porque MOD-003 no tiene dependencias de entrada (seccion L).
- El umbral de 50 empleados para la bandera de separacion de funciones es configurable solo por el equipo del producto, sin respaldo legal (seccion G automatizacion 1; 05_tipos_de_usuario.md seccion 5.4).

**Fuera de alcance**

- Verificacion documental del NIT o del acta de constitucion (KYB), excluida de este modulo (seccion Q, FUTURE).
- Estructura detallada de sucursales o areas mas alla del pais (seccion Q, COULD HAVE).
- El bloqueo duro de separacion de funciones al superar el umbral, que es responsabilidad de MOD-001, no de este modulo.

- Preguntas pendientes relacionadas: PP-PROD-04
- Referencia: MOD-003 seccion D Paso 1; seccion G automatizacion 1; seccion R punto 1
- Notas: El campo NIT se trata como obligatorio siguiendo la resolucion de 04_secciones/15_onboarding.md sobre la contradiccion entre la seccion D y la seccion P de la propia ficha; ver notas_epica.

### HU-003-03. Registrar al primer usuario Administrador de la organizacion

**Como** Administrador de la organizacion, **quiero** registrarme como el primer usuario con el rol Administrador de la organizacion en el Paso 2 del wizard, **para** quedar habilitado desde el primer momento para configurar usuarios, permisos y el resto del sistema.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 9 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-003-02
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado que el onboarding esta en el Paso 2, cuando el Administrador completa nombre completo y correo electronico validos y confirma Guardar y continuar, entonces el sistema guarda el paso, le asigna el rol Administrador de la organizacion y avanza al Paso 3.
2. Dado que el correo ingresado ya esta registrado en el sistema, cuando el Administrador intenta guardar el Paso 2, entonces el sistema rechaza el valor y muestra el error de correo no disponible.
3. Dado que el nombre completo queda vacio, cuando se intenta guardar el paso, entonces el sistema no permite avanzar.
4. Dado que el Administrador selecciona un cargo del catalogo (Gerente General, Gerente Administrativo, Jefe de TI, Jefe de RRHH, Jefe Legal o Compliance, Otro) o lo deja vacio, cuando guarda el paso, entonces el sistema lo acepta porque el cargo es opcional.
5. Dado que el Paso 2 quedo guardado, cuando el onboarding todavia no llega a COMPLETADO, entonces la cuenta del Administrador existe pero no queda formalmente activa hasta que se confirme el Paso 5.

**Reglas de negocio**

- Nombre completo y correo son obligatorios; el cargo es opcional.
- El correo debe tener formato valido y ser unico en el sistema.
- La cuenta del Administrador se activa formalmente al cerrar el Paso 5, no al guardar el Paso 2 (seccion E).

**Fuera de alcance**

- Activacion formal de la cuenta y envio de accesos, cubiertos por HU-003-07.
- Alta de usuarios adicionales, cubierta por HU-003-04.

- Referencia: MOD-003 seccion D Paso 2; seccion E fila Cuenta y rol del Administrador

### HU-003-04. Invitar usuarios adicionales con su rol propuesto

**Como** Administrador de la organizacion, **quiero** agregar en el Paso 3 del wizard, de forma opcional, a otras personas de mi empresa con su rol propuesto y area, **para** que mi equipo minimo pueda empezar a usar el sistema desde la primera sesion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 9 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-003-03
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado que el onboarding esta en el Paso 3, cuando el Administrador no agrega ninguna fila y confirma Guardar y continuar, entonces el sistema permite avanzar al Paso 4 porque el paso completo es opcional.
2. Dado que el Administrador agrega una fila con nombre, correo y rol propuesto validos, cuando confirma la fila, entonces el sistema la guarda con estado pendiente de invitacion y permite agregar otra fila o continuar.
3. Dado que el Administrador agrega una fila y deja vacio el nombre, el correo o el rol propuesto, cuando intenta guardar esa fila, entonces el sistema no la acepta y muestra el error del campo faltante.
4. Dado que el correo de una fila ya fue usado en otra fila o ya pertenece a un usuario de la misma organizacion, cuando se intenta guardar, entonces el sistema rechaza el correo duplicado.
5. Dado que el catalogo de Rol propuesto se muestra en una fila, cuando el Administrador lo abre, entonces solo puede elegir entre los roles estandar de 05_tipos_de_usuario.md seccion 5.3, sin incluir Titular (formulario externo), Auditor externo (invitado) ni Asesor externo invitado.
6. Dado que el correo de una fila tiene un dominio distinto al de los correos ya registrados en la misma organizacion, cuando el Administrador confirma la fila, entonces el sistema muestra en pantalla, de forma no bloqueante, la advertencia de que el correo no coincide con el dominio de los demas usuarios de su organizacion y que verifique antes de continuar.
7. Dado que el conjunto de roles asignados en el Paso 3 incluye una combinacion marcada como riesgosa en 05_tipos_de_usuario.md seccion 5.4 (por ejemplo Aprobador y Auditor), cuando el Administrador guarda el paso, entonces el sistema muestra una advertencia no bloqueante y permite continuar de todas formas.
8. Dado que el area o departamento de una fila queda vacia, cuando se guarda la fila, entonces el sistema la acepta porque el area es opcional.

**Reglas de negocio**

- El Paso 3 admite de 0 a N filas y es opcional en su totalidad.
- Si se agrega una fila, nombre, correo y rol propuesto son obligatorios; el area es opcional.
- El catalogo de rol propuesto excluye Titular externo, Auditor externo y Asesor externo invitado.
- El sistema nunca bloquea el cierre del onboarding por una combinacion de roles riesgosa, solo advierte, porque la organizacion todavia no esta activa (seccion C).

**Fuera de alcance**

- Sugerencia automatica de rol a partir del cargo declarado (SHOULD HAVE, excluida de este encargo).
- Envio real de la invitacion por correo, que ocurre al confirmar el Paso 5 (HU-003-07).

- Referencia: MOD-003 seccion D Paso 3; seccion G automatizacion 8; seccion C nota de separacion de funciones; seccion P riesgo 3
- Notas: La advertencia de combinacion de roles riesgosa (criterio 7) sigue el texto de la seccion C de la ficha; la ficha no precisa el mecanismo exacto de deteccion cuando cada fila solo permite un rol por persona, ver notas_epica.

### HU-003-05. Responder si la organizacion ya tiene o va a designar un Delegado, y sembrar su registro

**Como** Administrador de la organizacion, **quiero** indicar en el Paso 4 si mi empresa ya tiene un Delegado de Proteccion de Datos designado o si quiero designarlo ahora, con su nombre, correo y tipo interno o externo, **para** que el sistema siembre el registro inicial en el modulo del Delegado desde el primer contacto, en vez de dejarlo para despues.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 10 | No |

- Fundamento: OBL-DPO-01 (Art. 15 y 17, Ley para la Proteccion de Datos Personales); OBL-DPO-03 (Art. 10, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-003-04
- Modulos requeridos: MOD-002, MOD-023

**Criterios de aceptacion**

1. Dado que el onboarding esta en el Paso 4, cuando el Administrador selecciona Si ya esta designado o No quiero designarlo ahora y completa nombre, correo y tipo (interno, externo persona natural o externo persona juridica), entonces el sistema guarda el paso y permite avanzar al Paso 5.
2. Dado que el Administrador elige Si ya esta designado o No quiero designarlo ahora pero deja vacio el nombre, el correo o el tipo del Delegado, cuando intenta guardar el paso, entonces el sistema no permite avanzar y muestra el error del campo faltante.
3. Dado que el Paso 4 se completo con una de esas dos opciones, cuando el Administrador confirma el Paso 5 y el onboarding pasa a COMPLETADO, entonces el sistema crea el registro inicial del Delegado en MOD-002 en estado designacion en curso con el nombre, correo y tipo capturados.
4. Dado que el registro inicial del Delegado se crea en MOD-002, cuando eso ocurre, entonces el sistema siembra en MOD-023 el conteo del plazo de 15 dias habiles de comunicacion a la ACE, sin calcular ese plazo dentro de este modulo; el conteo real inicia cuando MOD-002 confirme el nombramiento, no en este paso.
5. Dado que el Administrador completa el Paso 4 con cualquiera de las tres opciones, cuando la pantalla se muestra, entonces incluye el texto Requiere validacion de la organizacion o asesoria especializada y el sistema nunca concluye por si mismo si la empresa necesita o no un Delegado.
6. Dado que el correo del Delegado no tiene formato valido, cuando se intenta guardar el paso, entonces el sistema rechaza el valor.

**Reglas de negocio**

- La pregunta del Paso 4 es obligatoria; debe elegirse una de las tres opciones.
- Nombre, correo y tipo interno o externo del Delegado son obligatorios si la respuesta no fue No estoy seguro.
- El sistema nunca decide si la empresa necesita Delegado ni que tipo de vinculo le conviene (seccion H, decision 1).
- El calculo del plazo de 15 dias habiles lo hace el motor de plazos MOD-023, nunca este modulo.

**Fuera de alcance**

- Verificacion de que el Delegado cumple los requisitos legales del Art. 5 Lineamientos DPO, que corresponde a MOD-002 (seccion H, decision 4).
- Aceptacion del cargo por parte del Delegado y el resto de su expediente, que ocurre dentro de MOD-002.

- Requiere validacion legal: Si
- Referencia: MOD-003 seccion D Paso 4; seccion G automatizacion 2; seccion F tabla de transiciones fila Confirmar y finalizar; seccion H decision 1
- Notas: La seccion G automatizacion 2 podria leerse como que la creacion del registro en MOD-002 ocurre ya al completar el Paso 4; esta HU sigue la seccion F (tabla de transiciones), que la ubica como efecto de Confirmar y finalizar (COMPLETADO). Ver notas_epica.

### HU-003-06. Registrar que la empresa no esta segura sobre el Delegado y crear la tarea critica de seguimiento

**Como** Administrador de la organizacion, **quiero** poder responder No estoy seguro, necesito ayuda para decidir en el Paso 4 sin que eso bloquee mi avance, **para** que el sistema no me deje olvidar este tema y me cree un recordatorio critico hasta que lo resuelva.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 10 | No |

- Fundamento: OBL-DPO-01 (Art. 15 y 17, Ley para la Proteccion de Datos Personales)
- Depende de: HU-003-04
- Modulos requeridos: MOD-021, MOD-022, MOD-023

**Criterios de aceptacion**

1. Dado que el onboarding esta en el Paso 4, cuando el Administrador selecciona No estoy seguro, necesito ayuda para decidir y confirma Guardar y continuar, entonces el sistema guarda la respuesta sin exigir nombre, correo ni tipo del Delegado, y permite avanzar al Paso 5.
2. Dado que se guarda la respuesta No estoy seguro, cuando eso ocurre, entonces el sistema crea de inmediato la tarea CRITICAL Resolver si su empresa necesita designar un Delegado de Proteccion de Datos en el Centro de Tareas, asignada al Administrador, con ayuda contextual de los Arts. 15 y 17, sin importar si el resto del wizard se completa despues.
3. Dado que la tarea CRITICAL sigue sin resolverse, cuando pasan 7 dias desde su creacion, entonces el sistema repite la alerta CRITICAL al Administrador, y al Delegado si ya fue invitado por otra via, por plataforma y correo.
4. Dado que la tarea CRITICAL sigue sin resolverse, cuando pasan 15 dias habiles calculados por MOD-023, entonces la alerta se hace visible en el dashboard de Gerencia.
5. Dado que la tarea CRITICAL esta activa, cuando se muestra al Administrador, entonces incluye el texto Requiere validacion de la organizacion o asesoria especializada.
6. Dado que mas adelante MOD-002 registra un Delegado confirmado, o queda documentada una decision explicita de la organizacion sobre por que no aplica, cuando eso ocurre, entonces la alerta CRITICAL se apaga.

**Reglas de negocio**

- La opcion No estoy seguro nunca cierra el tema ni se interpreta como que no aplica (seccion H, decision 1; seccion P riesgo 1).
- El plazo de 15 dias habiles para la escalada visible en el dashboard de Gerencia lo calcula MOD-023, no este modulo.
- La tarea CRITICAL se crea al guardar la respuesta del Paso 4, no al finalizar todo el wizard (seccion G automatizacion 3; seccion I).

**Fuera de alcance**

- Decidir si la empresa realmente necesita un Delegado o que tipo de vinculo le conviene (seccion H, decision 1).
- El registro del Delegado en MOD-002, que solo se crea cuando la respuesta es ya designado o designarlo ahora (HU-003-05).

- Requiere validacion legal: Si
- Referencia: MOD-003 seccion D Paso 4; seccion G automatizacion 3; seccion I fila Debe resolver si necesita un Delegado; seccion H decision 1

### HU-003-07. Aceptar el descargo de responsabilidad y confirmar la finalizacion de la configuracion inicial

**Como** Administrador de la organizacion, **quiero** aceptar explicitamente el aviso de que el sistema no sustituye asesoria legal y confirmar el cierre del wizard, **para** activar mi organizacion y mis usuarios invitados, y dejar constancia formal de como quedo configurado mi programa desde el primer dia.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 10 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-003-02, HU-003-03, HU-003-05, HU-003-06
- Modulos requeridos: MOD-001, MOD-022

**Criterios de aceptacion**

1. Dado que el onboarding esta en el Paso 5 con los campos obligatorios de los Pasos 1, 2 y 4 completos, cuando el Administrador marca la casilla Acepto el aviso de que este sistema no sustituye asesoria legal y selecciona Confirmar y finalizar, entonces el sistema muestra el texto completo Confirmo que entiendo que este sistema organiza y documenta el programa de proteccion de datos de mi empresa, pero no sustituye asesoria legal ni garantiza cumplimiento y pasa el onboarding a COMPLETADO.
2. Dado que la casilla del descargo no esta marcada, cuando el Administrador intenta Confirmar y finalizar, entonces el sistema no permite finalizar y muestra el error de casilla obligatoria.
3. Dado que falta un campo obligatorio de los Pasos 1, 2 o 4, cuando el Administrador intenta confirmar el Paso 5, entonces el sistema no permite finalizar y senala el paso incompleto.
4. Dado que el onboarding pasa a COMPLETADO, cuando eso ocurre, entonces se activa la Organizacion en MOD-001 con los datos del Paso 1, y se activan formalmente la cuenta del Administrador y las cuentas de los usuarios agregados en el Paso 3 en estado invitado con su rol propuesto.
5. Dado que el onboarding pasa a COMPLETADO, cuando eso ocurre, entonces se envia, via MOD-022, una invitacion por correo a cada usuario agregado en el Paso 3, con un enlace de activacion de un solo uso y con vencimiento.
6. Dado que el onboarding pasa a COMPLETADO, cuando eso ocurre, entonces se registra el evento de auditoria onboarding completado con una fotografia de todos los valores capturados en los 5 pasos, la fecha y el usuario.
7. Dado que el onboarding ya esta en COMPLETADO, cuando alguien intenta reabrir el wizard, entonces el sistema no lo permite porque es un estado terminal; cualquier cambio posterior a organizacion, usuarios o roles se hace directamente en MOD-001.

**Reglas de negocio**

- La casilla del descargo es obligatoria para poder finalizar (seccion D Paso 5).
- COMPLETADO exige todos los campos obligatorios de los Pasos 1, 2 y 5 completos, la casilla marcada y al menos un usuario Administrador activo (seccion F).
- COMPLETADO es un estado terminal del wizard; no existe accion de reabrirlo (seccion F).
- La creacion del registro del Delegado en MOD-002, cuando aplica, esta cubierta por HU-003-05 y no se repite aqui.

**Fuera de alcance**

- La creacion del registro del Delegado en MOD-002 (HU-003-05) y la tarea CRITICAL del Paso 4 (HU-003-06), que no dependen de este cierre para crearse.
- La creacion de la tarea de inicio del Diagnostico y la redireccion a MOD-004 (HU-003-08).

- Referencia: MOD-003 seccion D Paso 5; seccion F tabla de transiciones fila Confirmar y finalizar; seccion G automatizacion 4; seccion J evidencia de aceptacion del descargo

### HU-003-08. Crear automaticamente la tarea de iniciar el Diagnostico y redirigir a MOD-004

**Como** Administrador de la organizacion, **quiero** que al terminar la configuracion inicial el sistema me cree de inmediato la tarea de iniciar el Diagnostico de Cumplimiento y me lleve directamente a el, **para** no abandonar el producto justo antes de llegar al valor real, que son el Diagnostico y el Plan de Cumplimiento.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 10 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-003-07
- Modulos requeridos: MOD-021, MOD-004

**Criterios de aceptacion**

1. Dado que el onboarding pasa a COMPLETADO, cuando eso ocurre siempre, entonces el sistema crea la tarea Iniciar el Diagnostico de Cumplimiento en el Centro de Tareas, asignada al Administrador o a quien este designe.
2. Dado que se crea esa tarea, cuando el Administrador termina el Paso 5, entonces el sistema lo redirige automaticamente a MOD-004 Diagnostico de Cumplimiento.
3. Dado que la tarea ya fue creada, cuando el Administrador consulta el Centro de Tareas, entonces la ve con un enlace directo hacia MOD-004.
4. Dado que el onboarding todavia esta en EN_PROGRESO o ABANDONADO, cuando se consulta el Centro de Tareas, entonces la tarea Iniciar el Diagnostico de Cumplimiento todavia no existe.
5. Dado que pasan mas de 7 dias desde el onboarding COMPLETADO sin que se inicie ninguna sesion del Diagnostico, cuando se cumple ese plazo, entonces se dispara la alerta WARNING Diagnostico nunca iniciado tras onboarding, gestionada por MOD-004.

**Reglas de negocio**

- La tarea se crea siempre al completarse el onboarding, sin condicion adicional (seccion G automatizacion 5).
- El nombre de la tarea usado en esta HU es Iniciar el Diagnostico de Cumplimiento, tomado de la seccion E de la ficha y de 04_secciones/15_onboarding.md; ver discrepancia de nombre en notas_epica.

**Fuera de alcance**

- El contenido y el flujo del propio Diagnostico de Cumplimiento (MOD-004).
- La alerta Diagnostico nunca iniciado, que pertenece a MOD-004 y solo se cita aqui como referencia.

- Referencia: MOD-003 seccion E fila Tarea Iniciar el Diagnostico; seccion G automatizacion 5
- Notas: La seccion G (automatizacion 5) y 04_secciones/12_tareas_y_alertas.md nombran esta tarea Completar el Diagnostico de Cumplimiento, mientras que la seccion E de la misma ficha y 04_secciones/15_onboarding.md la nombran Iniciar el Diagnostico de Cumplimiento. Se adopto este segundo nombre por coincidir entre dos fuentes independientes; ver notas_epica.

### HU-003-09. Guardar automaticamente el avance y reanudar la configuracion inicial tras un periodo de inactividad

**Como** Administrador de la organizacion, **quiero** que mi avance en el wizard se guarde solo despues de cada paso y poder continuar exactamente donde quede si me alejo varios dias, **para** no perder lo ya capturado ni tener que empezar de nuevo si no puedo terminar la configuracion en una sola sesion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 11 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-003-02
- Modulos requeridos: MOD-022

**Criterios de aceptacion**

1. Dado que el Administrador confirma Guardar y continuar en cualquier paso con los campos obligatorios validos, cuando el sistema guarda, entonces el onboarding permanece en EN_PROGRESO, se actualiza el indicador de progreso (paso X de 5), se conserva una fotografia de los valores de ese paso para el historial, incluidos los cambios de un campo con su valor anterior y nuevo si se corrigio antes de avanzar, y lo guardado no se pierde aunque el Administrador cierre sesion.
2. Dado que el onboarding esta en EN_PROGRESO y pasan 5 dias, valor por defecto configurable solo por el equipo del producto y no por la empresa, sin completar un paso nuevo, cuando se cumple ese plazo, entonces el sistema envia la alerta WARNING Configuracion inicial incompleta por correo y en plataforma, y repite el recordatorio cada 5 dias hasta un maximo de 3 veces.
3. Dado que transcurren los mismos dias de inactividad configurados sin completar un paso nuevo, cuando se cumple ese plazo, entonces el estado cambia de EN_PROGRESO a ABANDONADO sin eliminar el avance ya guardado, y se envia la alerta WARNING Onboarding abandonado una vez al entrar al estado y luego semanalmente.
4. Dado que el onboarding esta en ABANDONADO, cuando el Administrador, ya autenticado, reingresa al wizard, entonces el estado vuelve a EN_PROGRESO y continua exactamente en el ultimo paso guardado, sin pedir de nuevo los datos ya capturados.
5. Dado que el onboarding esta en NO_INICIADO, EN_PROGRESO o ABANDONADO, cuando un proceso externo de baja comercial cancela la cuenta antes de completar el onboarding, entonces el registro pasa a ARCHIVADO con el motivo de la cancelacion cuando el proceso comercial lo proporcione, se conserva como historico sin eliminarse, y las invitaciones pendientes de usuarios que no habian aceptado quedan revocadas automaticamente.
6. Dado que el onboarding ya esta en COMPLETADO o en ARCHIVADO, cuando alguien intenta modificar cualquiera de sus pasos, entonces el sistema lo impide porque ambos son estados terminales de solo lectura para este modulo.
7. Dado que una organizacion reactiva su cuenta despues de haber quedado ARCHIVADA sin completar el onboarding, cuando vuelve a acceder, entonces el sistema le presenta un onboarding nuevo y no reutiliza el registro archivado.

**Reglas de negocio**

- El autoguardado ocurre al final de cada paso, no a nivel de campo individual (seccion F).
- El numero de dias de inactividad es configurable solo por el equipo del producto, nunca por la empresa (seccion G automatizacion 6).
- COMPLETADO y ARCHIVADO son estados terminales; no existe reapertura del wizard (seccion F).
- Ningun cambio de estado borra informacion; todo queda versionado con su historial (seccion F, principio del mapa definitivo citado ahi).

**Fuera de alcance**

- El contenido especifico de cada paso, cubierto por las HU de cada Paso.
- La decision comercial de cancelar o reactivar una cuenta, que es un proceso externo a este modulo.

- Referencia: MOD-003 seccion F completa (workflow y tabla de transiciones); seccion I filas Configuracion inicial incompleta y Onboarding abandonado; seccion O

### HU-003-10. Consultar el historial de la configuracion inicial

**Como** Administrador de la organizacion, **quiero** ver el historial completo de como se configuro mi organizacion, paso por paso, **para** verificar en cualquier momento que se declaro y cuando, incluso despues de terminado el onboarding.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 11 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-003-07
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el onboarding esta COMPLETADO, cuando el Administrador abre el historial, entonces ve cada paso guardado con la fotografia de los valores capturados en ese momento, fecha y usuario, incluidos los cambios de campo corregidos antes de avanzar.
2. Dado que el onboarding esta COMPLETADO, cuando el Administrador abre el historial, entonces tambien ve la respuesta elegida en el Paso 4, la evidencia de aceptacion del descargo (texto, version, fecha y usuario) y el evento onboarding completado.
3. Dado que un usuario con rol Auditor (interno) abre el historial del onboarding ya completado, cuando lo consulta, entonces accede en modo de solo lectura, sin poder modificar ningun dato.
4. Dado que un usuario con un rol distinto de Administrador o Auditor (interno) intenta ver el wizard en curso o su historial, cuando lo intenta, entonces el sistema le niega el acceso.
5. Dado que el onboarding todavia esta EN_PROGRESO o ABANDONADO, cuando el Administrador lo consulta, entonces ve el wizard en su punto actual, no un historial cerrado.

**Reglas de negocio**

- Solo Administrador (total) y Auditor interno (solo lectura del historial ya completado) pueden ver el wizard o su historial (seccion C).
- El historial es inmutable y queda con usuario, fecha y hora, y el motivo cuando aplique (seccion O).

**Fuera de alcance**

- La exportacion del historial en PDF o CSV/XLSX, cubierta por HU-003-11.

- Referencia: MOD-003 seccion C tabla de permisos fila Ver; seccion J; seccion O

### HU-003-11. Exportar el resumen de configuracion inicial y el historial de invitaciones

**Como** Administrador de la organizacion, **quiero** exportar un resumen en PDF de como quedo configurada mi organizacion y un listado del historial de invitaciones, **para** usarlos como insumo del paquete de evidencias de auditoria y para dar seguimiento a quien acepto su invitacion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 11 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-003-07, HU-003-10
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el onboarding esta COMPLETADO, cuando el Administrador solicita el reporte Resumen de configuracion inicial, entonces el sistema genera un PDF con los datos de la organizacion del Paso 1, la lista de usuarios y roles asignados, el estado de la designacion del Delegado al cierre, y la fecha de finalizacion y el usuario que lo completo.
2. Dado que el onboarding esta COMPLETADO, cuando el Administrador o el Auditor (interno) solicitan el Historial de invitaciones y aceptaciones, entonces el sistema genera un archivo CSV o XLSX con cada invitacion enviada, su fecha de envio, su fecha de aceptacion o de vencimiento, y el rol asignado.
3. Dado que se solicita el historial de invitaciones, cuando el usuario aplica un filtro por rango de fechas o por estado (pendiente, aceptada, vencida), entonces el listado exportado respeta ese filtro.
4. Dado que un usuario con un rol distinto de Administrador o Auditor (interno) intenta exportar cualquiera de estos dos reportes, cuando lo intenta, entonces el sistema le niega el permiso.
5. Dado que el onboarding todavia no esta COMPLETADO, cuando se intenta exportar el Resumen de configuracion inicial, entonces el sistema no genera el reporte porque el onboarding aun no tiene fecha de cierre.
6. Dado que se exporta cualquiera de los dos reportes, cuando la exportacion se genera, entonces el sistema registra en el historial quien lo exporto y cuando.

**Reglas de negocio**

- El Resumen de configuracion inicial es un reporte unico por organizacion, no un listado filtrable (seccion N).
- El historial de invitaciones admite filtro por rango de fechas y por estado (seccion N).
- Solo Administrador y Auditor (interno) pueden exportar (seccion C).

**Fuera de alcance**

- El calculo de hash o firma de integridad sobre estos reportes, no descrito para este modulo a diferencia de otros modulos con exportacion con hash.

- Referencia: MOD-003 seccion N; seccion C fila Exportar; seccion O ultima fila

### HU-003-12. Gestionar el estado de las invitaciones enviadas

**Como** Administrador de la organizacion, **quiero** recibir recordatorios automaticos de las invitaciones que no se han aceptado, y poder reenviarlas o retirarlas, **para** asegurar que mi equipo minimo realmente pueda acceder al sistema sin quedar con invitaciones olvidadas.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 11 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-003-07
- Modulos requeridos: MOD-022

**Criterios de aceptacion**

1. Dado que una invitacion enviada al confirmar el Paso 5 sigue sin aceptarse, cuando pasan 5 dias, entonces el sistema envia un recordatorio por correo y en plataforma al usuario invitado y alerta al Administrador; el nivel de la alerta pasa de INFO a WARNING a los 10 dias.
2. Dado que una invitacion sigue sin aceptarse, cuando pasan 30 dias desde su envio, entonces el sistema la marca como vencida y notifica al Administrador para que la reenvie o la retire.
3. Dado que una invitacion esta pendiente, no vencida ni aceptada, cuando el Administrador elige retirarla, entonces el sistema la retira y deja de enviar recordatorios sobre ella.
4. Dado que una invitacion ya fue aceptada y el usuario ya creo su cuenta, cuando el Administrador intenta retirarla, entonces el sistema no lo permite porque solo puede retirar invitaciones pendientes.
5. Dado que una invitacion quedo marcada como vencida, cuando el Administrador elige reenviarla, entonces el sistema genera un nuevo enlace de activacion de un solo uso con su propio vencimiento y reinicia el conteo de recordatorios.
6. Dado que un usuario invitado acepta su invitacion, cuando lo hace, entonces el sistema registra en el historial quien acepto y cuando, y detiene cualquier recordatorio pendiente sobre esa invitacion.

**Reglas de negocio**

- Los plazos de recordatorio de 5, 10 y 30 dias son configurables por el equipo del producto, no por la empresa (seccion G automatizacion 7).
- El Administrador solo puede retirar invitaciones pendientes, nunca eliminar el registro del onboarding ya completado (seccion C).
- El enlace de activacion es de un solo uso y con vencimiento (seccion P riesgo de seguridad).

**Fuera de alcance**

- El envio de la primera invitacion al confirmar el Paso 5, cubierto por HU-003-07.
- La creacion de la cuenta del usuario invitado una vez acepta, que es responsabilidad de MOD-001.

- Preguntas pendientes relacionadas: PP-PROD-05
- Referencia: MOD-003 seccion G automatizacion 7; seccion I fila Invitacion de usuario pendiente; seccion C fila Eliminar/archivar
- Notas: El plazo de vencimiento de 30 dias y los recordatorios a 5 y 10 dias son valores de producto sin respaldo legal, sujetos a PP-PROD-05.

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Alta guiada de los datos basicos de la organizacion (razon social, sector, tamano, paises) | HU-003-01, HU-003-02 |
| Alta del primer usuario Administrador e invitacion de usuarios adicionales con rol propuesto | HU-003-03, HU-003-04, HU-003-07, HU-003-12 |
| Pregunta inicial sobre la existencia o designacion del Delegado, con siembra del registro en MOD-002 | HU-003-05, HU-003-06 |
| Texto de descargo de responsabilidad con aceptacion explicita | HU-003-07 |
| Creacion automatica de la tarea de inicio del Diagnostico y redireccion | HU-003-08 |
