# EP-007 Consentimiento (MOD-007)

**Objetivo.** La empresa puede registrar el consentimiento general y reforzado de sus titulares (con firma cuando el dato es sensible o biometrico), activar el sub-flujo parental para menores de edad, procesar una revocacion dentro del plazo legal de 5 mas 5 dias habiles, y exportar evidencia basica de todo ello.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R2 | 13 | 60 | 0 | 60 | [MOD-007](../../03_modulos/MOD-007_ficha.md) |

**Notas de la epica.**

- Se sigue la tabla Q de la ficha (6 filas MUST HAVE): registro de consentimiento general, registro reforzado sensible/biometrico, revocacion con dos plazos de 5 dias habiles, sub-flujo parental para NNA, snapshot inmutable con version del aviso referenciada, y reportes exportables basicos. No se construyen las filas SHOULD HAVE o COULD HAVE de la misma tabla: catalogo de excepciones al consentimiento (Art 28 y Arts 37-38), enlace automatico con la lista de supresion de marketing, sincronizacion con sistemas externos de marketing o CRM, portal publico de autogestion del titular, ni analitica de tendencias, conforme a las indicaciones del encargo.
- La aprobacion de las plantillas de consentimiento (general, sensible/biometrico, parental) no se modela como HU propia de este modulo: la ficha, seccion K, declara que esas plantillas se alojan, se versionan y se aprueban como tipo de documento dentro de MOD-008, y que este modulo solo las usa por referencia, nunca las copia. La necesidad de ese contenido validado queda registrada en el campo requiere_contenido de cada HU de captura que las usa.
- Los dos plazos de la revocacion (5 dias habiles para ejecutar y 5 dias habiles adicionales para notificar al encargado) se fundamentan en OBL-CONS-03, Art 30, y nunca en OBL-CONS-04, que corresponde solo al consentimiento por escrito de datos sensibles; esto sigue la correccion que la propia ficha ya incorporo (actualizacion 2026-09-24, fase 3) sobre un error anterior que atribuia el segundo tramo a OBL-CONS-04.
- Los indicadores de la seccion M de la ficha (cobertura de captura, revocaciones dentro de plazo, evidencia disponible) no se modelan como una pantalla propia de dashboard dentro de esta epica: se calculan sobre los mismos datos que ya exponen los reportes basicos (HU-007-12) y los consume el dashboard transversal de MOD-020, que pertenece a otra epica.
- Minimizacion de datos: siguiendo la decision de alcance citada en la ficha (seccion D), este modulo si identifica minimamente al titular (nombre e identificador de referencia) porque sin eso no se puede probar el consentimiento (OBL-CONS-05); en ningun caso guarda el dato sensible o biometrico en si, solo la constancia de que se pidio, se acepto, se declino o se ofrecio una alternativa.
- Las 13 HU de esta epica quedan en release R2: MOD-007 completo depende de que MOD-006 (RAT) y MOD-008 (version del aviso) ya existan, y ambos son R1, segun la secuencia recomendada de la ficha de roadmap, seccion 19.9.
- No se detecto ninguna discrepancia entre la tabla Q de la ficha y la seccion 19.3 del roadmap: ambas describen la misma version minima vendible del modulo (registro general y reforzado, revocacion de dos plazos, sub-flujo parental, snapshot inmutable y reportes basicos).

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-007-01 | Registrar el consentimiento general de un titular para una finalidad del RAT | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 5 | R2 | 22 | MOD-006, MOD-008, MOD-022 |
| HU-007-02 | Generar la tarea de captura de consentimiento cuando el RAT declara la base Consentimiento | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R2 | 25 | HU-007-01, MOD-006, MOD-021, MOD-022 |
| HU-007-03 | Registrar un consentimiento reforzado para datos sensibles con firma | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 5 | R2 | 25 | HU-007-01 |
| HU-007-04 | Registrar un consentimiento biometrico con firma y alternativa no biometrica | Responsable de Seguridad / IT | 5 | R2 | 26 | HU-007-01, HU-007-03 |
| HU-007-05 | Ejecutar el sub-flujo de consentimiento parental para titulares NNA | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 5 | R2 | 26 | HU-007-01 |
| HU-007-06 | Archivar automaticamente el consentimiento sustituido al otorgarse uno nuevo vigente | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R2 | 25 | HU-007-01 |
| HU-007-07 | Marcar como Expirado un consentimiento cuando vence la vigencia declarada en el RAT | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R2 | 26 | HU-007-01, MOD-006, MOD-023, MOD-021 |
| HU-007-08 | Registrar la solicitud de revocacion y calcular el plazo de ejecucion | Responsable ARCO-POL / Responsable del tramite | 5 | R2 | 26 | HU-007-01, MOD-023, MOD-021, MOD-022 |
| HU-007-09 | Validar y ejecutar la revocacion con aprobacion del Delegado o Responsable interno | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 26 | HU-007-08, MOD-002, MOD-024 |
| HU-007-10 | Notificar la revocacion al encargado o cerrar el expediente cuando no aplica | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 8 | R2 | 26 | HU-007-09, MOD-009, MOD-023, MOD-021 |
| HU-007-11 | Marcar como Vencida una revocacion que supera su plazo sin avanzar | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 26 | HU-007-08, HU-007-09, HU-007-10, MOD-023, MOD-022 |
| HU-007-12 | Exportar los listados basicos de consentimientos y de revocaciones | Responsable Legal / Compliance | 3 | R2 | 26 | HU-007-01, HU-007-08, MOD-019 |
| HU-007-13 | Exportar el expediente individual de un consentimiento con verificacion de integridad | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 27 | HU-007-01, MOD-019 |

## Historias

### HU-007-01. Registrar el consentimiento general de un titular para una finalidad del RAT

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** presentar el aviso vigente y registrar el consentimiento de un titular para una finalidad de tratamiento que el RAT ya declaro con base Consentimiento, dejando un registro con el snapshot del texto y de la version del aviso, **para** poder demostrar despues que la persona acepto de forma expresa e informada, tal como exige la carga de la prueba de la ley.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 22 | Si |

- Fundamento: OBL-CONS-01 (Art. 26 y 27, Ley para la Proteccion de Datos Personales); OBL-PRIN-01 (Art. 5 lit. c), Ley para la Proteccion de Datos Personales); OBL-CONS-05 (Art. 54, Ley para la Proteccion de Datos Personales)
- Depende de: -
- Modulos requeridos: MOD-006, MOD-008, MOD-022

**Criterios de aceptacion**

1. Dado un tratamiento Vigente en el RAT con base juridica Consentimiento y al menos una finalidad declarada, cuando el Responsable de area inicia una nueva captura, entonces el sistema muestra unicamente los tratamientos y finalidades que el RAT ya marco con esa base juridica.
2. Dado que el sistema toma el texto exacto presentado y la version del Aviso de Privacidad publicada en MOD-008 en el momento de la captura, cuando el registro pasa a estado Vigente, entonces ambos quedan guardados como snapshot inmutable, por referencia a esa version de MOD-008 y nunca como copia editable, sin sustituirse aunque MOD-008 publique una version posterior.
3. Dado que el titular acepta el consentimiento presentado, cuando el Responsable de area guarda el registro, entonces el estado cambia de Presentado a Vigente y se registra fecha, hora y usuario en el historial.
4. Dado que el titular declina el consentimiento presentado, cuando el Responsable de area lo registra, entonces el estado cambia de Presentado a No otorgado y el sistema conserva unicamente la constancia de que se le informo el derecho a no dar el dato, sin guardar el dato del formulario.
5. Dado que el tratamiento seleccionado no tiene ninguna version publicada del Aviso de Privacidad en MOD-008, cuando el Responsable de area intenta iniciar la captura, entonces el sistema bloquea el guardado y genera la alerta CRITICAL Version de Aviso de Privacidad no disponible, dirigida al Delegado o Responsable interno y al Administrador.
6. Dado que el usuario completo los campos obligatorios del formulario, cuando intenta guardarlo, entonces el sistema verifica unicamente que los campos esten completos, nunca la calidad juridica de la redaccion (libre, especifico, informado, expreso, individualizado), y muestra el texto Requiere validacion de la organizacion o asesoria especializada junto al campo del texto de consentimiento.
7. Dado un rol sin permiso de creacion en este modulo, por ejemplo Auditor interno o Usuario de consulta sin tarea asignada, cuando intenta abrir el formulario de captura, entonces el sistema deniega el acceso.

**Reglas de negocio**

- El tipo de consentimiento se calcula automaticamente segun las categorias de datos heredadas del tratamiento; el usuario no puede bajar el nivel de refuerzo detectado.
- El titular se identifica solo con nombre y un identificador de referencia; no se copian otros campos de su perfil desde el sistema del cliente.
- Las categorias de datos cubiertas se precargan del RAT y no son editables en este modulo.
- El registro es de solo escritura por adicion (append-only); ningun rol puede eliminarlo, solo archivarlo por sustitucion (ver HU-007-06).

**Fuera de alcance**

- Consentimiento reforzado para datos sensibles o biometricos con firma (ver HU-007-03 y HU-007-04).
- Sub-flujo de consentimiento parental para NNA (ver HU-007-05).
- Catalogo de excepciones al consentimiento de los Art 28 y Arts 37-38: no se construye en el MVP.

- Requiere contenido: Plantilla de clausula de consentimiento general (variables de empresa, finalidad y periodo), validada por la organizacion, ficha MOD-007 seccion K.
- Requiere validacion legal: Si
- Referencia: MOD-007 secciones D.1, F.1 fila Presentado, G regla 2, H punto 4, I fila Version de Aviso de Privacidad no disponible
- Notas: Version minima vendible del modulo segun la seccion Q de la ficha; capacidad base de la que dependen las demas HU de esta epica.

### HU-007-02. Generar la tarea de captura de consentimiento cuando el RAT declara la base Consentimiento

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** que el sistema me cree automaticamente una tarea de captura cuando el RAT marque un tratamiento de mi area con base juridica Consentimiento y aun no exista un registro vigente, **para** no depender de recordar manualmente que falta pedir el consentimiento de ese tratamiento.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 25 | No |

- Fundamento: OBL-CONS-01 (Art. 26 y 27, Ley para la Proteccion de Datos Personales)
- Depende de: HU-007-01
- Modulos requeridos: MOD-006, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que una ficha de tratamiento pasa a Vigente en el RAT con base juridica Consentimiento, cuando no existe todavia un registro Consent en estado Vigente para ese tratamiento y ese titular, entonces el sistema crea en MOD-021 la tarea Capturar consentimiento asignada al Responsable de area del tratamiento, con el tipo de consentimiento requerido segun la categoria de dato heredada.
2. Dado que ya existe un registro Consent en estado Vigente para ese tratamiento y ese titular, cuando el RAT vuelve a confirmar la misma base juridica, entonces el sistema no crea una tarea duplicada.
3. Dado que pasan varios dias desde la creacion del tratamiento sin que exista un registro Consent Vigente ni No otorgado, cuando se cumple el umbral configurado, entonces el sistema genera la alerta INFO Consentimiento pendiente de captura al Responsable de area, con recordatorio semanal mientras siga pendiente.
4. Dado que la alerta INFO sigue activa 15 dias despues de creada, cuando se cumple ese plazo, entonces el sistema la escala al Delegado o Responsable interno.
5. Dado que el Responsable de area registra el consentimiento como Vigente o deja constancia de que el titular declino como No otorgado, cuando guarda ese registro, entonces la tarea y la alerta asociadas se cierran automaticamente.

**Reglas de negocio**

- El responsable por defecto de la tarea es configurable por la empresa, pero el disparo de la tarea en si no lo es.
- La tarea siempre vive en el Centro de Tareas de MOD-021, nunca dentro de este modulo.

- Referencia: MOD-007 secciones E fila Tarea capturar consentimiento, G regla 1, I fila Consentimiento pendiente de captura

### HU-007-03. Registrar un consentimiento reforzado para datos sensibles con firma

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** registrar el consentimiento de un titular cuando el tratamiento involucra datos sensibles, exigiendo firma y la advertencia del derecho a no proporcionar el dato, **para** cumplir el requisito reforzado que la ley exige para datos sensibles y poder probarlo despues.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 25 | No |

- Fundamento: OBL-CONS-04 (Art. 26 inc. 4, Ley para la Proteccion de Datos Personales); OBL-SENS-02 (Art. 37 inc. 1, Ley para la Proteccion de Datos Personales)
- Depende de: HU-007-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que la categoria de dato heredada del tratamiento esta marcada como sensible, cuando se inicia la captura, entonces el sistema calcula automaticamente el Tipo de consentimiento como Sensible reforzado y el usuario no puede cambiarlo a General.
2. Dado un registro en estado Presentado con Tipo Sensible reforzado, cuando el Responsable de area intenta guardarlo como Vigente sin un archivo de firma adjunto, entonces el sistema bloquea el guardado.
3. Dado un registro en estado Presentado con Tipo Sensible reforzado, cuando el Responsable de area intenta guardarlo sin marcar el campo Advertencia de derecho a no proporcionar el dato mostrada, entonces el sistema bloquea el guardado.
4. Dado que el Responsable de area adjunta la firma, autografa escaneada o firma electronica valida, y marca la advertencia, cuando guarda el registro, entonces el estado cambia a Vigente, el archivo queda con hash de integridad, y el evento queda en el historial con usuario y fecha.
5. Dado un registro en Presentado con Tipo Sensible reforzado sin firma adjunta por mas de 2 dias, cuando se cumple ese plazo, entonces el sistema genera la alerta WARNING Consentimiento sensible incompleto al Responsable de area y al Delegado, escalando a Administrador a los 5 dias.
6. Dado que un usuario con permiso de ver un registro sensible abre su archivo de firma, cuando lo consulta, entonces el sistema registra ese acceso de lectura en el historial con usuario, fecha y hora.
7. Dado un rol sin permiso de creacion en este modulo, por ejemplo Aprobador o Auditor interno, cuando intenta registrar un consentimiento sensible, entonces el sistema deniega la accion.

**Reglas de negocio**

- El nivel de refuerzo detectado automaticamente no puede bajarse a General.
- El sistema nunca guarda el dato sensible en si, solo la constancia de que se pidio y se acepto o declino el consentimiento.

**Fuera de alcance**

- Catalogo de excepciones de los Art 37 y 38 para datos sensibles: no se construye en el MVP.

- Requiere contenido: Plantilla de consentimiento sensible con la advertencia del Art 37 y espacio de firma, validada por la organizacion y por asesoria legal, ficha MOD-007 seccion K.
- Referencia: MOD-007 secciones D.1 campos Tipo de consentimiento, Firma, Advertencia; F.1 fila Presentado a Vigente; G regla 2; I fila Consentimiento sensible incompleto; J; O

### HU-007-04. Registrar un consentimiento biometrico con firma y alternativa no biometrica

**Como** Responsable de Seguridad / IT, **quiero** registrar el consentimiento biometrico de un titular exigiendo firma y advertencia, y dejar constancia de si se ofrecio una alternativa no biometrica, **para** cumplir el regimen reforzado de datos biometricos y dejar evidencia de la alternativa ofrecida.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 26 | No |

- Fundamento: OBL-CONS-04 (Art. 26 inc. 4, Ley para la Proteccion de Datos Personales); OBL-SENS-02 (Art. 37 inc. 1, Ley para la Proteccion de Datos Personales); OBL-SENS-07 (Art. 26 inc. 4 y Art. 37, Ley para la Proteccion de Datos Personales)
- Depende de: HU-007-01, HU-007-03
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que la categoria de dato heredada del tratamiento esta marcada como biometrica, cuando se inicia la captura, entonces el sistema calcula automaticamente el Tipo de consentimiento como Biometrico.
2. Dado un registro en Presentado con Tipo Biometrico, cuando el Responsable de Seguridad / IT intenta guardarlo como Vigente sin archivo de firma adjunto o sin marcar la advertencia del Art 37, entonces el sistema bloquea el guardado.
3. Dado un registro en Presentado con Tipo Biometrico, cuando el Responsable de Seguridad / IT lo guarda, entonces el sistema exige completar antes el campo Alternativa no biometrica ofrecida, con su descripcion breve cuando aplica.
4. Dado que se guarda un consentimiento Biometrico con Alternativa no biometrica ofrecida en No, cuando el registro pasa a Vigente, entonces el sistema no bloquea el guardado, pero genera la alerta WARNING Consentimiento biometrico sin alternativa ofrecida al Responsable de area y a Legal, deja una nota de riesgo permanente y visible en el registro, y muestra el texto Requiere validacion de la organizacion o asesoria especializada, porque el sistema no concluye si el consentimiento sigue siendo libre en una relacion de subordinacion.
5. Dado que esa misma alerta se repite para otro registro del mismo tratamiento, cuando se guarda ese segundo caso, entonces el sistema la escala al Delegado o Responsable interno.
6. Dado que se guarda un consentimiento Biometrico, cuando el sistema lo registra, entonces guarda unicamente la constancia de que se pidio el consentimiento, medio, fecha, firma y alternativa ofrecida, nunca la plantilla o el dato biometrico en si.

**Reglas de negocio**

- La advertencia y la firma para el Tipo Biometrico siguen la misma regla de bloqueo que el Tipo Sensible reforzado.
- La alerta por no ofrecer alternativa no biometrica es informativa, no bloquea el guardado del registro.

**Fuera de alcance**

- Catalogo de excepciones de los Art 37 y 38 para datos sensibles: no se construye en el MVP.

- Requiere validacion legal: Si
- Referencia: MOD-007 secciones D.1 campo Alternativa no biometrica ofrecida, F.1, G regla 2, H punto 6, I fila Consentimiento biometrico sin alternativa ofrecida, D parrafo de minimizacion
- Notas: El sistema deja constancia de la alternativa ofrecida; nunca certifica si el consentimiento fue realmente libre, segun la seccion H de la ficha.

### HU-007-05. Ejecutar el sub-flujo de consentimiento parental para titulares NNA

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** activar y completar el sub-flujo parental cuando el titular sea nina, nino o adolescente, registrando quien autoriza en su nombre, **para** cumplir el requisito de consentimiento parental antes de tratar datos de un menor de edad.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 26 | No |

- Fundamento: OBL-CONS-06 (Art. 56 lit. c num. 3, en relacion con Art. 5 lit. j y Art. 42, Ley para la Proteccion de Datos Personales); OBL-PRIN-04 (Art. 5 lit. j), Ley para la Proteccion de Datos Personales); OBL-CONS-04 (Art. 26 inc. 4, Ley para la Proteccion de Datos Personales)
- Depende de: HU-007-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el usuario marca Titular es NNA en Si durante la captura, cuando continua el formulario, entonces el sistema activa y exige los campos Nombre del padre, madre o tutor que consiente y Relacion o parentesco declarado antes de permitir guardar.
2. Dado el sub-flujo parental activo, cuando el usuario intenta guardar el registro sin el campo Nombre del padre, madre o tutor completo, entonces el sistema bloquea el guardado por dato obligatorio faltante.
3. Dado el sub-flujo parental activo, cuando el usuario adjunta o no adjunta la Evidencia de la relacion, por ejemplo una partida de nacimiento, entonces el sistema permite continuar en ambos casos, dejando constancia explicita de si se adjunto o no.
4. Dado un consentimiento con Titular es NNA en Si, cuando se guarda como Vigente, entonces el sistema exige el mismo archivo de firma obligatorio que en los tipos Sensible reforzado y Biometrico.
5. Dado el sub-flujo parental activo, cuando el sistema muestra el formulario, entonces incluye de forma visible la nota sobre la tension entre la LPDP y la Ley Crecer Juntos respecto de si un adolescente puede autoconsentir, junto con el texto Requiere validacion de la organizacion o asesoria especializada, sin fijar una regla automatica de edad.
6. Dado que el diagnostico de la organizacion detecto tratamiento de menores de edad, cuando un usuario intenta desactivar el sub-flujo parental para ese tratamiento, entonces el sistema no lo permite, porque esa activacion condicional por dato no es desactivable en ese caso.
7. Dado que el consentimiento parental se guarda, cuando el registro pasa a Vigente, entonces el sistema deja constancia en el historial del nombre y la relacion de quien autorizo, junto con la fecha y el usuario que lo registro.

**Reglas de negocio**

- El flujo parental completo se pide siempre por criterio conservador, sin una regla automatica de edad.
- La evidencia de la relacion parental es recomendada, no obligatoria, pero su ausencia queda registrada.

- Requiere contenido: Plantilla de consentimiento parental para NNA con lenguaje adaptado a la edad, Art 42, validada por la organizacion y por asesoria legal, ficha MOD-007 seccion K.
- Requiere validacion legal: Si (PP-JUR-05, PP-UX-03)
- Referencia: MOD-007 secciones D.1 campos Titular es NNA y campos parentales, F.1, G regla 3, H punto 2, P riesgo de datos de menores sin evidencia suficiente
- Notas: Criterio conservador por defecto: el flujo parental completo se pide siempre, sin regla automatica de edad, ver PP-JUR-05.

### HU-007-06. Archivar automaticamente el consentimiento sustituido al otorgarse uno nuevo vigente

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** que al registrarse un nuevo consentimiento vigente para una finalidad que ya tenia uno, el sistema archive el anterior como Sustituido y lo enlace al nuevo, **para** conservar el historial completo sin duplicar registros activos ni borrar evidencia.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 25 | No |

- Fundamento: OBL-CONS-05 (Art. 54, Ley para la Proteccion de Datos Personales)
- Depende de: HU-007-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un consentimiento en estado Revocado o Expirado para una finalidad, cuando el titular otorga un nuevo consentimiento vigente para esa misma finalidad, entonces el sistema pasa el registro anterior a estado Sustituido y lo enlaza por referencia al nuevo registro Vigente.
2. Dado un registro que paso a Sustituido, cuando cualquier rol, incluido Administrador, intenta editarlo o eliminarlo, entonces el sistema lo deniega, porque el registro es de solo escritura por adicion.
3. Dado un registro Sustituido, cuando un usuario con permiso de ver consulta el historial del nuevo consentimiento, entonces puede ver la referencia al registro anterior y la fecha en la que quedo archivado.
4. Dado un consentimiento en estado Vigente para una finalidad, cuando el titular otorga un nuevo consentimiento para una finalidad distinta del mismo tratamiento, entonces el sistema crea un registro independiente sin afectar el consentimiento Vigente existente.
5. Dado que un registro paso a Sustituido, cuando se genera ese evento, entonces queda registrado en el historial con fecha y la referencia al registro que lo reemplaza.

**Reglas de negocio**

- Nunca se sobrescribe ni se borra un registro anterior; solo se archiva por sustitucion.
- El enlace entre el registro Sustituido y el nuevo Vigente debe poder consultarse desde ambos lados.

- Referencia: MOD-007 seccion F.1 fila Revocado o Expirado a Sustituido, G regla 7, C separacion de funciones

### HU-007-07. Marcar como Expirado un consentimiento cuando vence la vigencia declarada en el RAT

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** que el sistema marque automaticamente como Expirado un consentimiento Vigente cuando se cumple la fecha de vigencia que el RAT declaro para esa finalidad, y me cree una tarea de revision, **para** no seguir tratando datos bajo un consentimiento cuya vigencia declarada ya vencio.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 26 | No |

- Fundamento: OBL-PRIN-01 (Art. 5 lit. c), Ley para la Proteccion de Datos Personales)
- Depende de: HU-007-01
- Modulos requeridos: MOD-006, MOD-023, MOD-021

**Criterios de aceptacion**

1. Dado un tratamiento con una fecha de vigencia declarada para una finalidad en el RAT, cuando esa fecha se cumple segun el calendario de MOD-023 y el consentimiento sigue en estado Vigente, entonces el sistema lo marca automaticamente como Expirado.
2. Dado que un consentimiento pasa a Expirado, cuando ocurre esa transicion, entonces el sistema crea en MOD-021 una tarea de revision asignada al Responsable de area del tratamiento.
3. Dado un tratamiento sin fecha de vigencia declarada en el RAT para esa finalidad, cuando pasa el tiempo, entonces el sistema no marca ningun consentimiento como Expirado por esta regla.
4. Dado que la empresa no activo la funcion de vigencias por finalidad, cuando un tratamiento no tiene vigencia declarada, entonces esta automatizacion permanece desactivada para ese tratamiento.
5. Dado un consentimiento que paso a Expirado, cuando un usuario intenta revertirlo manualmente a Vigente, entonces el sistema lo deniega; solo un nuevo consentimiento otorgado por el titular puede sustituirlo.

**Reglas de negocio**

- La activacion de esta regla por vigencias declaradas por finalidad es configurable por la empresa.
- El calculo de la fecha de vigencia siempre lo hace MOD-023, nunca este modulo.

- Referencia: MOD-007 seccion F.1 fila Vigente a Expirado, G regla 10

### HU-007-08. Registrar la solicitud de revocacion y calcular el plazo de ejecucion

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** registrar la solicitud de revocacion de un consentimiento vigente y que el sistema calcule la fecha limite de 5 dias habiles para ejecutarla, **para** cumplir el plazo legal desde el momento en que la persona pide retirar su consentimiento.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 26 | No |

- Fundamento: OBL-CONS-02 (Art. 29, Ley para la Proteccion de Datos Personales); OBL-CONS-03 (Art. 30, Ley para la Proteccion de Datos Personales)
- Depende de: HU-007-01
- Modulos requeridos: MOD-023, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado un consentimiento en estado Vigente del titular, cuando el Responsable ARCO-POL registra una solicitud de revocacion indicando el canal por el que llego, entonces el sistema crea un registro ConsentWithdrawal en estado Recibida.
2. Dado que se crea el registro en Recibida, cuando se guarda, entonces el sistema calcula la Fecha limite para ejecutar como la fecha de recepcion mas 5 dias habiles, usando el calendario de MOD-023.
3. Dado que se crea el registro en Recibida, cuando se guarda, entonces el sistema crea en MOD-021 la tarea de ejecucion de la revocacion asignada al Responsable ARCO-POL, con copia al Delegado o Responsable interno.
4. Dado que la solicitud se recibio antes por otro canal, por ejemplo una carta fisica, cuando el Responsable ARCO-POL registra el caso, entonces puede editar la Fecha y hora de recepcion de la solicitud para que coincida con el momento real, siempre que no sea una fecha futura.
5. Dado un titular sin ningun consentimiento en estado Vigente, cuando el Responsable ARCO-POL intenta registrar una revocacion para el, entonces el sistema no permite crear el registro.
6. Dado que faltan 2 dias habiles para el limite de los 5 dias habiles, cuando se cumple esa condicion, entonces el sistema genera la alerta WARNING Revocacion proxima a vencer al Responsable ARCO-POL y al Delegado o Responsable interno.

**Reglas de negocio**

- La revocacion no tiene efecto retroactivo sobre lo ya tratado antes de recibirse.
- El canal de revocacion debe ser tan expedito, sencillo y gratuito como el canal usado para otorgar el consentimiento.

**Fuera de alcance**

- Ejecucion de la revocacion, ver HU-007-09.
- Notificacion al encargado, ver HU-007-10.

- Referencia: MOD-007 secciones D.2 campos Fecha de recepcion y Fecha limite, F.2 fila Recibida, G regla 4, I fila Revocacion proxima a vencer

### HU-007-09. Validar y ejecutar la revocacion con aprobacion del Delegado o Responsable interno

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** aprobar y ejecutar una solicitud de revocacion recibida, dejando de tratar el dato para esa finalidad, **para** cumplir el plazo de 5 dias habiles y dejar constancia de quien autorizo el cierre del tratamiento.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 26 | No |

- Fundamento: OBL-CONS-03 (Art. 30, Ley para la Proteccion de Datos Personales)
- Depende de: HU-007-08
- Modulos requeridos: MOD-002, MOD-024

**Criterios de aceptacion**

1. Dado un registro ConsentWithdrawal en estado Recibida, cuando el Delegado o Responsable interno vigente segun MOD-024 valida y aprueba la ejecucion, entonces el sistema cambia el estado a Ejecutada, registra la Fecha de ejecucion real y actualiza el Consent de origen a Revocado.
2. Dado que el sistema arma la lista de posibles aprobadores, cuando la muestra, entonces solo incluye usuarios con el rol vigente segun la bandera regimen_reforma_659 de MOD-024, Delegado si esta en ACTUAL, Responsable interno si esta en FUTURO.
3. Dado un rol distinto de Delegado o Responsable interno, por ejemplo Responsable ARCO-POL o Responsable de area, cuando intenta ejecutar la revocacion sin la aprobacion correspondiente, entonces el sistema deniega la accion.
4. Dado que la revocacion involucra datos sensibles o un posible reclamo ante la Direccion de Proteccion de Datos de la ACE, cuando el Delegado o Responsable interno revisa el caso, entonces el sistema exige su aprobacion explicita antes de continuar y nunca ejecuta ni notifica el cierre de forma automatica.
5. Dado que la Fecha de ejecucion real se registra despues de la Fecha limite para ejecutar, cuando se guarda, entonces el sistema conserva el registro del incumplimiento del plazo en el historial, ademas de la marca Vencida que corresponda.
6. Dado que un expediente de revocacion ya fue cerrado antes de un cambio de la bandera de MOD-024, cuando se consulta despues de ese cambio, entonces conserva el rol que aprobo, Delegado o Responsable interno, segun estaba vigente al momento del cierre, sin recalcularlo con la bandera nueva.

**Reglas de negocio**

- Quien captura el consentimiento no es, por este solo hecho, quien aprueba su revocacion; la aprobacion siempre es del Delegado o Responsable interno vigente.
- El campo Persona que aprueba y ejecuta nunca se guarda en cache; se recalcula en cada revocacion nueva segun la bandera de MOD-024.

- Requiere validacion legal: Si
- Referencia: MOD-007 secciones D.2 campo Persona que aprueba y ejecuta, F.2 fila Recibida a Ejecutada, G regla 9, H punto 7, C separacion de funciones

### HU-007-10. Notificar la revocacion al encargado o cerrar el expediente cuando no aplica

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** aprobar el envio de la notificacion de revocacion a cada encargado asociado al tratamiento, o confirmar que no aplica cuando no hay encargados, dentro del segundo plazo de 5 dias habiles, **para** cumplir el segundo tramo del plazo legal y cerrar el expediente con evidencia completa.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 26 | No |

- Fundamento: OBL-CONS-03 (Art. 30, Ley para la Proteccion de Datos Personales)
- Depende de: HU-007-09
- Modulos requeridos: MOD-009, MOD-023, MOD-021

**Criterios de aceptacion**

1. Dado un registro ConsentWithdrawal en estado Ejecutada cuyo tratamiento tiene al menos un encargado registrado en MOD-009, cuando se identifica esa condicion, entonces el sistema calcula la Fecha limite de notificacion como la fecha de ejecucion mas 5 dias habiles y crea en MOD-021 la tarea Notificar la revocacion al encargado.
2. Dado el borrador de notificacion al encargado ya redactado por el sistema, cuando el Delegado o Responsable interno no ha dado su aprobacion explicita, entonces el sistema no envia la notificacion, porque la emision final requiere esa aprobacion humana.
3. Dado que el Delegado o Responsable interno aprueba el envio y se registra la evidencia de esa notificacion, cuando se confirma, entonces el estado cambia de Ejecutada a Encargado notificado y despues a Cerrada.
4. Dado un registro ConsentWithdrawal en Ejecutada cuyo tratamiento no tiene ningun encargado registrado en MOD-009, cuando el sistema lo detecta, entonces marca el campo Encargados a notificar como no aplica de forma automatica y justificada, y permite cerrar el expediente con la confirmacion del Responsable ARCO-POL, sin pasar por Encargado notificado.
5. Dado un tratamiento con encargados asociados en MOD-009, cuando el Responsable ARCO-POL o el Delegado intentan cerrar el expediente sin marcar cada encargado como notificado o como no aplica justificado, entonces el sistema bloquea el cierre.
6. Dado que faltan 2 dias habiles para el limite de los 5 dias habiles adicionales, cuando se cumple esa condicion, entonces el sistema genera la alerta WARNING Notificacion a encargado proxima a vencer al Responsable de Seguridad / IT y al Delegado o Responsable interno.
7. Dado que el expediente se cierra, cuando se completa el ultimo paso aplicable, entonces el sistema deja la evidencia completa, constancia de notificacion o de no aplicabilidad, disponible para MOD-019.

**Reglas de negocio**

- Si MOD-009 aun no tiene registrado un encargado real del tratamiento, el sistema no bloquea la revocacion: la marca para verificar manualmente y crea una tarea de alta en MOD-009 antes de permitir cerrar el expediente como completo.
- La emision de la notificacion al encargado nunca es automatica; siempre requiere la aprobacion explicita del Delegado o Responsable interno.

- Requiere contenido: Plantilla de notificacion de revocacion al encargado, validada por la organizacion, ficha MOD-007 seccion K.
- Referencia: MOD-007 secciones D.2 campos Encargados a notificar y Fecha limite de notificacion, F.2 filas Ejecutada a Encargado notificado a Cerrada y Ejecutada sin encargados a Cerrada, G regla 5, H punto 7, I filas de notificacion a encargado, L cuando MOD-009 no tiene el encargado registrado
- Notas: Fundamento OBL-CONS-03, Art 30 segundo tramo; no se atribuye a OBL-CONS-04, que corresponde solo al consentimiento por escrito de datos sensibles, segun la actualizacion de la ficha, fase 3.

### HU-007-11. Marcar como Vencida una revocacion que supera su plazo sin avanzar

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que el sistema marque automaticamente como Vencida una revocacion que supero el plazo de ejecucion o el de notificacion al encargado sin avanzar de estado, y escale la alerta, **para** intervenir de inmediato y dejar constancia del incumplimiento del plazo legal.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 26 | No |

- Fundamento: OBL-CONS-03 (Art. 30, Ley para la Proteccion de Datos Personales)
- Depende de: HU-007-08, HU-007-09, HU-007-10
- Modulos requeridos: MOD-023, MOD-022

**Criterios de aceptacion**

1. Dado un registro ConsentWithdrawal en Recibida, Ejecutada o Encargado notificado, cuando se supera la fecha limite correspondiente, de ejecucion o de notificacion al encargado, sin que el expediente avance de estado, entonces el sistema anade la marca Vencida sin bloquear que el expediente siga avanzando despues.
2. Dado que se supera el plazo de 5 dias habiles de ejecucion sin ejecutar, cuando se cumple esa condicion, entonces el sistema genera la alerta CRITICAL Revocacion vencida al Delegado o Responsable interno y al Administrador, con resumen en el dashboard de Gerencia.
3. Dado que se supera el plazo de 5 dias habiles adicionales de notificacion al encargado, cuando se cumple esa condicion, entonces el sistema genera la alerta CRITICAL Notificacion a encargado vencida al Delegado o Responsable interno y al Administrador.
4. Dado un expediente marcado Vencida, cuando finalmente se ejecuta la revocacion o se notifica al encargado, entonces la alerta CRITICAL se apaga, pero la marca Vencida permanece visible de forma permanente en el historial del expediente.
5. Dado un expediente marcado Vencida, cuando cualquier rol, incluido Administrador, intenta quitar esa marca manualmente, entonces el sistema lo deniega, porque solo se genera y se conserva de forma automatica.
6. Dado un expediente que avanza de estado dentro del plazo correspondiente, cuando se evalua la condicion de vencimiento, entonces el sistema no genera la marca Vencida ni la alerta CRITICAL para ese expediente.

**Reglas de negocio**

- El calculo de ambos plazos siempre lo hace MOD-023; este modulo nunca reimplementa el calendario de dias habiles.
- La marca Vencida es acumulativa e historica: no desaparece aunque el expediente se resuelva despues.

- Referencia: MOD-007 secciones F.2 nota de Vencida, G regla 6, I filas Revocacion vencida y Notificacion a encargado vencida

### HU-007-12. Exportar los listados basicos de consentimientos y de revocaciones

**Como** Responsable Legal / Compliance, **quiero** exportar el listado de consentimientos vigentes, el de revocaciones procesadas y el de consentimientos sensibles o biometricos, con filtros basicos, **para** usarlos como evidencia en la auditoria anual y en la respuesta a un reclamo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 26 | No |

- Fundamento: OBL-CONS-05 (Art. 54, Ley para la Proteccion de Datos Personales)
- Depende de: HU-007-01, HU-007-08
- Modulos requeridos: MOD-019

**Criterios de aceptacion**

1. Dado que existen registros Consent, cuando el Responsable Legal / Compliance exporta el reporte Consentimientos vigentes, entonces el sistema genera un archivo XLSX o CSV con finalidad, tipo, fecha y version del aviso, filtrable por tratamiento, finalidad, tipo y rango de fechas.
2. Dado que existen registros ConsentWithdrawal, cuando se exporta el reporte Revocaciones procesadas, entonces el sistema genera un archivo XLSX o CSV con las fechas de recepcion, ejecucion y notificacion, e indica si cada una cumplio su plazo, filtrable por rango de fechas y por estado, a tiempo o vencida.
3. Dado registros con Tipo Sensible reforzado, Biometrico o Parental, cuando se exporta el reporte Consentimientos sensibles y biometricos, entonces el sistema genera un archivo XLSX filtrable por tipo y por area, con el estado de la Alternativa no biometrica ofrecida cuando aplica.
4. Dado un rol sin permiso de exportar en este modulo, por ejemplo Responsable de area o Responsable de Seguridad / IT, cuando intenta exportar cualquiera de estos reportes, entonces el sistema lo deniega.
5. Dado que se genera cualquiera de estos tres reportes, cuando se completa la exportacion, entonces el sistema registra el evento en el historial, quien, cuando y que reporte, y lo deja disponible para el paquete de evidencia de MOD-019.
6. Dado que el Auditor interno exporta cualquiera de estos reportes, cuando lo hace, entonces el sistema lo permite en modo de solo lectura, sin habilitarle ninguna accion de creacion o modificacion.

**Reglas de negocio**

- Esta es la version basica del reporte; los filtros avanzados y la analitica de tendencias quedan fuera del MVP.
- Todo indicador que resuma estos datos se muestra como estado del programa, nunca como porcentaje de cumplimiento legal.

**Fuera de alcance**

- Filtros avanzados y analitica de tendencias de consentimiento: quedan fuera del MVP.

- Referencia: MOD-007 seccion N filas Consentimientos vigentes, Revocaciones procesadas y Consentimientos sensibles y biometricos; seccion C fila Exportar
- Notas: Version basica del reporte segun la tabla Q; los filtros avanzados quedan fuera del MVP.

### HU-007-13. Exportar el expediente individual de un consentimiento con verificacion de integridad

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** exportar el expediente completo de un consentimiento especifico, con su snapshot, version del aviso, archivo de firma, historial de estados y verificacion de integridad, **para** responder con evidencia verificable a un reclamo del titular o a una consulta de la ACE.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 27 | No |

- Fundamento: OBL-CONS-05 (Art. 54, Ley para la Proteccion de Datos Personales)
- Depende de: HU-007-01
- Modulos requeridos: MOD-019

**Criterios de aceptacion**

1. Dado un registro Consent especifico, cuando el Delegado o Responsable interno exporta su expediente individual, entonces el sistema genera un documento con el texto exacto presentado, la version del Aviso de Privacidad referenciada, el archivo de firma o evidencia de aceptacion, y el historial completo de estados con fecha, hora y usuario.
2. Dado que se genera el expediente individual, cuando se completa el archivo, entonces incluye un hash o firma verificable de integridad, para poder demostrar despues que no fue alterado.
3. Dado un registro Consent en estado Presentado sin snapshot de texto ni version de aviso completos, cuando se intenta exportar su expediente individual, entonces el sistema no genera un expediente valido, porque los datos probatorios minimos aun no existen.
4. Dado que se genera un expediente individual, cuando se completa la exportacion, entonces el sistema registra el evento en el historial, quien lo exporto, cuando y para que caso, y lo deja disponible para el Centro de Evidencias de MOD-019.
5. Dado un rol sin permiso de exportar en este modulo, por ejemplo Responsable de area o Titular, cuando intenta exportar un expediente individual, entonces el sistema lo deniega.
6. Dado que el expediente incluye el archivo de firma o el documento de relacion parental de un caso NNA, cuando el Delegado o Responsable interno lo consulta antes de exportar, entonces el sistema registra ese acceso de lectura en el historial, por tratarse de un adjunto sensible.

**Reglas de negocio**

- El expediente exportado es parte del paquete de evidencia hacia MOD-019.
- La verificacion de integridad debe poder validarse de forma independiente, sin depender de este modulo.

- Referencia: MOD-007 seccion N fila Expediente individual de consentimiento, J evidencia y exportacion firmada, O accesos de lectura y exportaciones

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Registro de consentimiento general (formulario simple, sin refuerzo) | HU-007-01, HU-007-02, HU-007-06 |
| Registro de consentimiento reforzado (sensible/biometrico con firma) | HU-007-03, HU-007-04 |
| Revocacion con flujo de dos plazos (5+5 dias habiles) | HU-007-08, HU-007-09, HU-007-10, HU-007-11 |
| Sub-flujo de consentimiento parental para NNA | HU-007-05 |
| Snapshot inmutable y version del aviso referenciada | HU-007-01, HU-007-13 |
| Reportes exportables de consentimientos y revocaciones (basico) | HU-007-12, HU-007-13 |
