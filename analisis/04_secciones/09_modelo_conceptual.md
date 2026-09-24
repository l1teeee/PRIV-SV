# 9. Modelo conceptual de informacion

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (prohibido codigo, SQL, APIs, endpoints, esquemas de base de datos, nombres de tecnologias, stack o infraestructura).

Esta seccion consolida y cruza lo ya decidido en `02_validacion/06_mapa_definitivo_de_modulos.md` (seccion 7, "Entidades conceptuales principales", y seccion 5, doble estado de la reforma 659), en `02_validacion/mapa_modulos.json` (campo `entidades_principales` de cada uno de los 26 modulos) y en las secciones D (Informacion de entrada), E (Informacion generada), F (Workflow) y L (Dependencias) de las 26 fichas funcionales de `03_modulos/MOD-001_ficha.md` a `MOD-026_ficha.md`, que son la fuente principal de detalle de cada entidad, su ciclo de vida y sus reglas de minimizacion de datos personales. No inventa entidades ni funcionalidades que ninguna ficha define; donde el prompt del cliente (`00_prompt_analisis_funcional.md`, seccion "Entidades y relaciones") exige algo que ninguna ficha cubre, se marca explicitamente "propuesta de esta seccion, no presente en las fichas".

Jerarquia usada para resolver cualquier discrepancia entre fuentes, identica a la de las secciones 10 y 11 de este mismo blueprint: fuente legal primaria y `01_legal/matriz_obligaciones.json` sobre `02_validacion/mapa_modulos.json` y `06_mapa_definitivo_de_modulos.md`, estos sobre `02_validacion/05_tipos_de_usuario.md` para lo relativo a roles, y estos sobre la ficha del modulo propietario de la entidad, y esta sobre cualquier otra ficha que la referencie de forma colaboradora. Las contradicciones detectadas al aplicar esta jerarquia y los huecos (piezas que ninguna ficha define) se listan al final, en "Contradicciones y huecos detectados", con el archivo, lo que dice cada fuente, cual se adopto y por que.

Convencion de identificadores: todo OBL-ID citado es el identificador canonico de `01_legal/matriz_obligaciones.json` (formato OBL-AREA-NN, 105 obligaciones), nunca los IDs preliminares de `01_legal/03_hallazgos_regulatorios.md` (su equivalencia esta en la seccion 11 de ese documento). Los 12 roles citados son los de `02_validacion/05_tipos_de_usuario.md`, seccion 5.3, con su nombre exacto. Ninguna tabla de esta seccion usa tipos de dato tecnicos, claves, indices ni nombres de tabla: la columna "Atributos funcionales clave" describe que informacion administra cada entidad en lenguaje de negocio, no un modelo de base de datos.

---

## 9.1 Principios del modelo de informacion

Estos seis principios ya estan aplicados, de forma dispersa, en las 26 fichas y en `06_mapa_definitivo_de_modulos.md`; esta subseccion los declara de forma explicita y unica porque son la base de lectura de todo el catalogo de entidades que sigue.

### 9.1.1 Entidad unica por concepto

Cada concepto de negocio vive en una sola entidad, aunque varios modulos lo consulten. El caso mas visible es el Delegado de Proteccion de Datos: en vez de modelar "Delegado (regimen actual)" y "Responsable interno (regimen futuro)" como dos entidades o dos modulos distintos, existe una sola entidad, `ResponsableDelProgramaDeDatos`, con un atributo `tipo_rol` que distingue el regimen (ver 9.7). El mismo principio aplica al catalogo de controles de seguridad: MOD-014 (Riesgos y EIPD) no mantiene una lista propia de controles, sino que selecciona o crea controles dentro del unico catalogo `Control` que administra MOD-015 (decision 2.7.3 de `02_validacion_de_la_idea.md`).

### 9.1.2 Propietario unico

Toda entidad tiene exactamente un modulo propietario, igual que toda obligacion de `matriz_obligaciones.json` tiene exactamente un modulo propietario segun la seccion 8 de `06_mapa_definitivo_de_modulos.md`. El propietario es quien crea, edita y decide el ciclo de vida del registro; cualquier otro modulo que lo necesite lo consulta por referencia (9.1.3), nunca lo duplica ni lo edita desde fuera. La columna "Modulo propietario" del catalogo de la seccion 9.2 es, en consecuencia, siempre un unico valor.

### 9.1.3 Referencias en vez de copias

Cuando un modulo de proceso necesita un dato que otro modulo ya administra, lo enlaza por referencia (un identificador de registro), nunca copia el valor. Ejemplos verificados en las fichas: el Centro de Tareas (MOD-021) nunca copia el contenido de un expediente ARCO-POL, solo guarda su numero de expediente como referencia; el Centro de Evidencias (MOD-019) nunca copia un Documento de MOD-008 dentro de un paquete de evidencia, lo referencia por version exacta; un Consentimiento (MOD-007) nunca copia el texto del Aviso de Privacidad vigente, guarda la referencia a esa version exacta de MOD-008. Esta regla es la misma "Regla 3: direccion unica entre modulos de proceso" que documenta la seccion 10.1 de este blueprint (Dependencias entre modulos), aplicada aqui al modelo de datos en vez de al flujo de eventos.

### 9.1.4 Versionado

Nada que ya se publico o se conservo como prueba se sobrescribe: se crea una version nueva y la anterior queda disponible con sus propias fechas de vigencia. Ejemplos: `DocumentVersion` (MOD-008) nunca se edita despues de publicada, un cambio siempre abre una version nueva; `RegulatoryRuleVersion` (MOD-024) conserva la version anterior de una regla con su `fecha_vigencia_hasta`, sin sobrescribirla nunca, para poder reconstruir que regla aplicaba a un caso en una fecha pasada; el texto exacto de un Consentimiento (MOD-007) es un "snapshot inmutable"; el calendario de dias inhabiles (`HolidayCalendar`, MOD-023) se versiona por anio y capa (Borrador, Publicado, Vigente, Actualizado, Historico).

### 9.1.5 Historial inmutable y append-only

El registro tecnico transversal `AuditLog`, embebido en todos los modulos (seccion 7 de `06_mapa_definitivo_de_modulos.md`), es de solo escritura por adicion: ningun rol, ni siquiera Administrador, puede editarlo ni borrarlo (anti-feature 19 de `22_anti_features.md`). El mismo principio de "no borrar, marcar" aplica a registros de negocio: cuando el regimen de la reforma 659 cambia, las tareas del regimen anterior no se eliminan, se marcan "no aplica bajo el estado regulatorio actual, ver historial" (seccion 5, punto 6 de `06_mapa_definitivo_de_modulos.md`); un `Evidence` (MOD-019) incrementa su version en cada renovacion, nunca sobrescribe la version anterior.

### 9.1.6 Minimizacion de datos personales de los titulares

Regla general: el sistema registra metadatos del tratamiento (que sistema, quien lo administra, categorias de dato, retencion), nunca copia ni centraliza la base de datos de titulares del cliente (anti-features 1 y 8 de `22_anti_features.md`). Esta regla general tiene cuatro excepciones declaradas de forma expresa por decision de alcance (`02_validacion_de_la_idea.md`, seccion 2.7, punto 21): Consentimiento (MOD-007), ARCO-POL (MOD-011), Portal del Titular (MOD-012) e Incidentes (MOD-013) procesan datos personales directos del titular porque identificarlo, verificarlo o describir el impacto sobre el es el objeto legitimo de esos procesos. Incluso en esas cuatro excepciones, el sistema minimiza en el sentido correcto: guarda solo el dato minimo necesario para la prueba (por ejemplo, nombre e identificador de referencia en Consentimiento, nunca el perfil completo del CRM del cliente), nunca el dato sensible en si (por ejemplo, nunca la plantilla biometrica, solo la evidencia de que se pidio consentimiento para tratarla), y aplica control de acceso reforzado por nivel de sensibilidad. La seccion 9.8 desarrolla esta regla con el detalle exigido por el contenido minimo 8 de esta tarea.

---

## 9.2 Catalogo de entidades

El catalogo agrupa las entidades en nueve dominios funcionales para facilitar la lectura; los diagramas de la seccion 9.4 usan una agrupacion ligeramente distinta (los siete dominios que exige el contenido minimo 4 de esta tarea), con una nota de equivalencia al inicio de 9.4. Convenciones de las tablas: la columna "Datos personales" usa las etiquetas "No (metadato/institucional)", "Si - personal interno" (de empleados o colaboradores de la empresa cliente, nunca de sus titulares externos), "Si - titular externo (objeto legitimo)" (una de las cuatro excepciones de 9.1.6) y "Si - referenciado, no almacenado" (el dato sensible existe en el mundo real pero el sistema solo guarda su categoria o una evidencia puntual, nunca el valor). La columna "Retencion aplicable" cita el OBL-ID cuando existe un plazo legal o recomendado propio; en su defecto, indica el criterio de producto y senala si es un hueco (ver seccion final).

### 9.2.1 Organizacion, personas y gobierno del programa (MOD-001, MOD-002, MOD-003, MOD-017)

| Entidad | Que representa | Modulo propietario | Atributos funcionales clave | Estados del ciclo de vida | Datos personales y como se minimiza | Retencion aplicable |
|---|---|---|---|---|---|---|
| `Organization` | La empresa cliente que usa el sistema: identidad legal, giro, sucursales y unidades | MOD-001 | Razon social, nombre comercial, NIT, sector/giro, rango de empleados, paises donde opera, sucursales, unidades o departamentos, contacto ARCO-POL derivado, contacto de seguridad | Activa (unico estado en el MVP; no existe alta de sociedades adicionales de un mismo grupo, ver 9.6) | No (datos societarios, no personales) | Mientras la cuenta este activa; despues, segun regla que fije MOD-016 [opinion de producto, hueco parcial: MOD-016 no define hoy una regla propia para el expediente de organizacion] |
| `BusinessUnit` / Sucursal | Una sede o area funcional dentro de la misma organizacion | MOD-001 | Nombre, direccion, pais, area funcional, responsable por defecto | Activa / Inactiva (uso implicito, sin catalogo de estados propio en la ficha) | No | Igual que `Organization` |
| `User` | Una persona con cuenta dentro del sistema, interna a la empresa cliente o invitada | MOD-001 | Nombre completo, correo corporativo, cargo, area, rol o roles asignados, telefono | Invitado, Activo, Suspendido, Dado de baja | Si - personal interno (nombre, correo, cargo, telefono; nunca documento de identidad, fecha de nacimiento ni direccion personal, excepcion intencional y acotada a este modulo segun decision 2.7.21) | Mientras la cuenta este activa; historial de altas/bajas y cambios de rol conservado como evidencia (OBL-PRIN-03), luego segun MOD-016 |
| `Role` / Rol personalizado | Un conjunto de permisos por modulo y por accion que se asigna a uno o varios `User` | MOD-001 | Nombre del rol, rol estandar del que parte (si aplica), matriz de permisos por modulo y accion (ver, crear, modificar, aprobar, eliminar/archivar, exportar, asignar), descripcion | Activo (los 12 roles estandar no se eliminan; un rol personalizado puede archivarse) | No | Igual que `Organization` |
| `ResponsableDelProgramaDeDatos` | La persona (o persona juridica con un responsable natural) designada como Delegado de Proteccion de Datos hoy, o Responsable interno si se activa el regimen FUTURO; una sola entidad para ambos regimenes (ver 9.7) | MOD-002 | `tipo_rol` (DELEGADO / RESPONSABLE_INTERNO), modalidad (interno/externo persona natural/externo persona juridica), datos de contacto institucional, fecha de nombramiento, checklist de requisitos del perfil, declaracion de conflicto de intereses, estado de certificacion ACE, fecha de ultima reverificacion, informes periodicos, delegado sustituto, fecha y motivo de cese | Implicitos por los campos de fecha: Designado -> Nombrado (comunicado a la ACE) -> Reverificado (periodico) -> Cesado; en cualquier momento puede haber un Delegado sustituto activo | Si - personal interno (o de la persona natural responsable si es persona juridica externa); numero de documento de identidad como dato de referencia, nunca copia escaneada salvo adjunto puntual de evidencia con acceso restringido | Historico indefinido; la clausula de confidencialidad post-cese exige conservar el expediente al menos 5 anos tras el cese (OBL-DPO-06) |
| `TrainingProgram` | El plan o programa que define que se ensena, a quien y con que periodicidad (general, induccion, por rol, o el plan anual agregador) | MOD-017 | Nombre, tipo de programa, tema(s), publico destinatario, modalidad, version del material, periodicidad de renovacion, elaborado por (Delegado, si es plan anual), programas incluidos (si es plan anual) | Borrador, Vigente, Archivado | No (metadato de formacion del personal interno) | Segun regla que fije MOD-016; sin plazo legal propio (OBL-CAP-01 no fija plazo de conservacion del programa en si) |
| `TrainingRecord` | La constancia de que una persona concreta recibio, o debe recibir, una instancia de un `TrainingProgram` | MOD-017 | Persona, programa relacionado, fecha en que recibio la capacitacion, modalidad confirmada, constancia o acuse, resultado de evaluacion (opcional, fuera de MVP), proxima renovacion, origen del registro | Programada, Completada, No asistio, Proxima a vencer, Vencida | Si - personal interno (referencia al `User` capacitado; la constancia nunca debe incluir el expediente laboral completo, contratos ni evaluaciones de desempeno, solo la constancia especifica de esa sesion) | Segun regla que fije MOD-016; evidencia esperada de OBL-CAP-01 y OBL-CAP-02 |

### 9.2.2 Diagnostico y plan de cumplimiento (MOD-004, MOD-005)

| Entidad | Que representa | Modulo propietario | Atributos funcionales clave | Estados del ciclo de vida | Datos personales y como se minimiza | Retencion aplicable |
|---|---|---|---|---|---|---|
| `DiagnosticoRespuesta` | Una sesion completa del cuestionario guiado de 47 preguntas en 11 bloques, mas cada respuesta individual | MOD-004 | Organizacion, responsable de la sesion, version del cuestionario, motivo de la sesion (inicial/re-diagnostico por cambio/periodico), bloques asignados por responsable, y por cada respuesta: pregunta, valor elegido, dependencias activadas | Sesion en curso -> Sesion cerrada (una organizacion puede tener varias sesiones historicas, nunca se sobrescribe una anterior) | No (todas las preguntas son sobre la existencia de un tipo de tratamiento, nunca sobre datos de un titular concreto) | Igual que el expediente de cumplimiento de la organizacion (MOD-016) |
| `AccionDelPlan` | Una accion priorizada (critica, importante o recomendada) que el sistema deriva del resultado del diagnostico | MOD-005 | Titulo, descripcion, obligacion relacionada (OBL-ID), modulo de ejecucion, origen del disparo, nivel de prioridad, responsable asignado, fecha objetivo, evidencia esperada y adjunta, justificacion de repriorizacion o de descarte, dependencias con otras acciones | Pendiente, En curso, Bloqueada, Vencida, Completada, Descartada, Archivada | Si - personal interno (referencia al responsable asignado, ya administrado por MOD-001; ningun campo admite adjuntar un dato personal de un titular, toda evidencia se referencia al modulo de ejecucion) | Vida de la cuenta mas 5 anos [opinion de producto, sin plazo legal propio; evidencia de OBL-PLAZO-03] |

### 9.2.3 Registro de tratamientos (MOD-006)

| Entidad | Que representa | Modulo propietario | Atributos funcionales clave | Estados del ciclo de vida | Datos personales y como se minimiza | Retencion aplicable |
|---|---|---|---|---|---|---|
| `Treatment` | Una actividad de tratamiento de datos personales que realiza la empresa (por ejemplo, "Nomina y pago de salarios"); fuente unica de verdad del RAT | MOD-006 | Nombre, descripcion, area y responsable interno, finalidad, base de licitud (con justificacion), excepcion invocada (si aplica), categorias de titulares, incluye menores, categorias de datos (con marca automatica de sensibilidad), origen del dato, sistema(s), encargados involucrados, terceros/destinatarios, transferencia fuera de El Salvador (booleano), plazo de conservacion, controles de seguridad aplicados, riesgo inicial estimado, requiere EIPD (sugerido), fecha de proxima revision | Borrador -> En revision -> Vigente -> (marcado "requiere revision" al vencer la fecha de proxima revision) -> Archivado | No (metadatos y referencias del tratamiento; nunca copia el dato del titular ni la base de clientes del cliente) | 5 anos como minimo por defecto [opinion de producto]; alimenta OBL-DOC-02, OBL-PRIN-02, OBL-SENS-01/04/06/08, OBL-TRAT-01/03 |
| `Purpose` (finalidad) y `LegalBasis` (base de licitud) | La razon declarada para tratar el dato y el fundamento juridico elegido de las seis bases del Art. 5 lit. g) | MOD-006 | Ver nota de contradiccion en la seccion final: se documentan como atributos catalogados de `Treatment` (campos "Finalidad" y "Base de licitud" con su justificacion), no como registros con ciclo de vida propio | No tienen ciclo de vida independiente del `Treatment` que los contiene | No | Igual que `Treatment` |
| `DataCategory` (categoria de datos) | Un tipo de dato personal del catalogo compartido (ordinario o sensible) que un `Treatment`, `Consent`, `Transfer` o `Incident` puede referenciar | MOD-006 (catalogo maestro, ver 9.5) | Nombre de la categoria, si es sensible (union de los catalogos del Art. 4 lit. g y el Art. 59 lit. b), fuente normativa | Catalogo estable, mantenido por el equipo del producto (ver 9.5) | No (es el nombre de una categoria, no el dato en si) | No aplica (contenido de referencia) |
| `System` (catalogo de sistemas) | Un sistema, aplicacion, archivo fisico u hoja de calculo donde vive un dato personal | MOD-006 | Nombre, tipo (interno/SaaS/fisico/hoja de calculo/otro), proveedor asociado (si es SaaS), pais de alojamiento, responsable tecnico interno | Activo / En baja / Dado de baja | No (metadato tecnico-organizativo) | Igual que `Treatment` |

### 9.2.4 Relacion con el titular (MOD-007, MOD-011, MOD-012)

| Entidad | Que representa | Modulo propietario | Atributos funcionales clave | Estados del ciclo de vida | Datos personales y como se minimiza | Retencion aplicable |
|---|---|---|---|---|---|---|
| `Consent` | El consentimiento de un titular para un `Treatment` cuya base de licitud es "Consentimiento" | MOD-007 | Tratamiento asociado, finalidad(es) cubiertas, categorias de datos heredadas, tipo (general/sensible reforzado/biometrico/parental), identificacion minima del titular, medio de captura, texto exacto presentado (snapshot inmutable), version del Aviso de Privacidad referenciada, firma o evidencia de aceptacion, excepcion invocada (si aplica) | Presentado, No otorgado, Vigente, Revocado, Expirado, Sustituido | Si - titular externo (objeto legitimo, OBL-CONS-05): solo nombre y un identificador de referencia, nunca el perfil completo del CRM; el dato sensible en si (por ejemplo la plantilla biometrica) nunca se guarda, solo la evidencia de que se pidio consentimiento para tratarlo | Segun regla que fije MOD-016 |
| `ConsentWithdrawal` | La revocacion de un `Consent` vigente, con el flujo de dos plazos encadenados (5+5 dias habiles) | MOD-007 | Consentimiento de origen, fecha y canal de recepcion de la revocacion, fecha limite de ejecucion (calculada), fecha de ejecucion real, encargados a notificar, fecha limite de notificacion al encargado, persona que aprueba y ejecuta (segun el `tipo_rol` vigente, ver 9.7) | Recibida, Ejecutada, Encargado notificado, Cerrada, Vencida | Igual que `Consent` (hereda la identificacion minima del titular por referencia) | Segun regla que fije MOD-016 |
| `PrivacyRequest` | Una solicitud ARCO-POL de un titular (acceso, rectificacion, cancelacion, oposicion, portabilidad, limitacion u olvido) | MOD-011 | Numero de expediente, tipo de solicitante (titular/representante/heredero), datos del solicitante, documento de identidad adjunto, derecho ejercido, descripcion de los datos, canal de recepcion, campos especificos por derecho (por ejemplo causal de cancelacion o supuesto de limitacion), modalidad y lugar de entrega de la respuesta, marca de solicitud anonima o potencialmente masiva | Recibida -> Verificacion de identidad -> (Prevencion/subsanacion o Devolucion por incompetencia) -> En tramite -> Resuelta (Aprobada/Denegada motivada) -> Notificacion a receptores (si aplica) -> Cerrada; rama alterna: Reclamo ante la Direccion de Proteccion de Datos (ACE) | Si - titular externo (objeto legitimo, decision 2.7.21): nombre, documento de identidad, domicilio, contacto y el contenido de la solicitud; adjuntos de identidad cifrados y de acceso restringido a Responsable ARCO-POL y Delegado/Responsable interno | 5 anos desde el cierre (OBL-RET-05, RECOMENDADO) |
| `IdentityVerification` | El resultado de verificar la identidad del solicitante de una `PrivacyRequest`, distinguiendo los tres tipos de solicitante del Art. 6 | MOD-011 | Tipo de solicitante, documento verificado, acreditacion de representacion o de calidad de heredero (si aplica), resultado de la verificacion | Pendiente, Verificada, Rechazada (sub-registro de `PrivacyRequest`, no tiene ciclo de vida propio fuera de ella) | Si - titular externo (documento de identidad y, si aplica, acreditacion de representacion o partida de defuncion/nacimiento) | Igual que `PrivacyRequest` |
| `Titular` | La persona externa (cliente, empleado, ex empleado o candidato de la empresa cliente) que consulta el Aviso, presenta una solicitud ARCO-POL o consulta su estado a traves del Portal | MOD-012 | Identificacion minima (nombre, documento, contacto), sesion de verificacion por codigo, referencia al expediente de MOD-011 | No es una entidad con ciclo de vida propio de negocio en el MVP: es la referencia al `PrivacyRequest` correspondiente mas los metadatos propios de cada sesion de consulta (codigo, fecha, resultado de verificacion); la cuenta persistente del titular es funcionalidad COULD HAVE fuera del nucleo del MVP | Si - titular externo (objeto legitimo); el Portal no duplica el expediente ni el documento de identidad, solo referencia el expediente de `PrivacyRequest` que vive en MOD-011 | Alineado al expediente ARCO-POL relacionado (MOD-011) |

### 9.2.5 Documentos y politicas (MOD-008)

| Entidad | Que representa | Modulo propietario | Atributos funcionales clave | Estados del ciclo de vida | Datos personales y como se minimiza | Retencion aplicable |
|---|---|---|---|---|---|---|
| `Document` / `DocumentVersion` | Un documento regulatorio de la empresa (Politica de Proteccion de Datos, Politica de Privacidad, Aviso de Privacidad, Procedimiento ARCO-POL u otro tipo extensible), y cada version que produce | MOD-008 | Tipo de documento, nombre, sucursal/unidad aplicable, contenido con plantilla, checklist de los 9 literales del Art. 24 (solo Aviso), checklist de los 5 elementos del Art. 7, encargados mencionados, variables precargadas (razon social, contacto del Delegado/Responsable interno), motivo de la nueva version, fecha de vigencia y de proxima revision, cadena de aprobacion aplicable | Borrador -> En revision -> Aprobado -> Publicado (vigente) -> Vencido/Historico (al publicarse una version nueva) | No de forma estructurada (el contenido es institucional); unico dato personal estructurado es el del Delegado/Responsable interno vigente, precargado por referencia desde MOD-002, nunca copiado a mano | Minimo 10 anos por version del Aviso de Privacidad (OBL-RET-04); otros tipos, segun regla que fije MOD-016 |
| `PrivacyNotice` / `PrivacyPolicy` | Las dos subclases de `Document` con contenido minimo legal propio (los 9 literales del Art. 24 y los 5 elementos del Art. 7, respectivamente) | MOD-008 | Ver `Document`/`DocumentVersion`: no son entidades separadas en la implementacion de la ficha, son el `tipo_documento` = "Aviso de Privacidad" o "Politica de Privacidad" dentro de la misma entidad | Igual que `Document` | Igual que `Document` | Igual que `Document` |

### 9.2.6 Terceros y transferencias (MOD-009, MOD-010)

| Entidad | Que representa | Modulo propietario | Atributos funcionales clave | Estados del ciclo de vida | Datos personales y como se minimiza | Retencion aplicable |
|---|---|---|---|---|---|---|
| `Encargado` | Un proveedor que trata datos personales siguiendo instrucciones de la empresa cliente | MOD-009 | Nombre comercial y razon social, servicio prestado, area responsable, sistemas relacionados, tratamientos del RAT vinculados, categorias de datos a las que accede (heredadas), pais(es) donde trata los datos, nivel de riesgo, medidas de seguridad declaradas, contrato/DPA vinculado, datos de contacto para el Aviso de Privacidad | En evaluacion -> Activo -> (revision periodica) -> Relacion finalizada -> Cerrado | No (metadatos del proveedor como entidad; unico dato de persona natural es el contacto de enlace del proveedor, no un titular) | Segun regla que fije MOD-016 |
| `TerceroReceptor` | Un tercero al que la empresa entrega datos para que los use con una finalidad propia distinta (no un encargado) | MOD-009 | Mismos atributos que `Encargado`, con "Tipo de entidad" = Tercero/Receptor | Igual que `Encargado` | Igual que `Encargado` | Igual que `Encargado` |
| `Subencargado` | Un proveedor contratado por un `Encargado` de la empresa, no directamente por la empresa cliente | MOD-009 | Mismos atributos que `Encargado`, mas la referencia al `Encargado` del que depende | Igual que `Encargado` | Igual que `Encargado` | Igual que `Encargado` |
| `Contrato/DPA` | El documento contractual que respalda la relacion con un `Encargado`, `TerceroReceptor` o `Subencargado`, o una `Transfer` | MOD-009 (tipo de `Document` de MOD-008, reutilizado por referencia) | Documento vinculado, fecha de vigencia e inicio, fecha de vencimiento, clausula de devolucion/eliminacion pactada | Igual que `Document` (MOD-008) | No | Igual que `Document` |
| `Transfer` | Un flujo de datos personales de un `Treatment` hacia un receptor, nacional o internacional | MOD-010 | Nombre, tratamiento de origen, tipo (nacional/internacional), receptor y su rol (encargado/responsable independiente/subencargado), pais(es) de destino, categorias de datos, finalidad, base juridica de la transferencia, evidencia de consentimiento especifico (si aplica), evaluacion del nivel de proteccion del pais receptor, salvaguardas tecnicas y contractuales, contrato de transferencia, puesta en conocimiento a la ACE (referencia a `ACEFiling`), solicitud de opinion previa (opcional) | Borrador -> En evaluacion de pais -> Pendiente de aprobacion -> Activa -> (revision periodica) | No (metadatos y referencias; el unico dato de persona natural incidental es el contacto comercial del proveedor extranjero) | 5 anos minimo tras finalizar [opinion de producto, sin norma expresa]; evidencia de OBL-TRANSF-01 a 06 |

### 9.2.7 Riesgo, seguridad, incidentes y retencion (MOD-013, MOD-014, MOD-015, MOD-016)

| Entidad | Que representa | Modulo propietario | Atributos funcionales clave | Estados del ciclo de vida | Datos personales y como se minimiza | Retencion aplicable |
|---|---|---|---|---|---|---|
| `Incident` | Una vulneracion de seguridad de datos personales, desde la deteccion hasta el cierre | MOD-013 | Titulo, fecha de deteccion, fecha de conocimiento (dispara los dos cronometros de 72 horas), origen, proveedor/encargado relacionado, sistema y tratamiento(s) afectados, tipo de vulneracion, causa raiz, categorias de datos afectadas, cantidad estimada de titulares afectados, impacto estimado, acciones de contencion, hallazgos de la revision exhaustiva, medidas correctivas, contenido diferenciado de la notificacion a ACE/FGR frente a titulares, criterio de computo de las 72 horas aplicado, decision final y justificacion | Registrado -> Triage -> Investigacion -> Contencion -> Evaluacion -> Decision -> Notificacion -> Remediacion -> Cerrado | Si - referenciado, no almacenado (categorias y cantidades estimadas de titulares afectados; nunca una copia de la base comprometida; un adjunto puntual solo cuando es indispensable, con cifrado y acceso restringido al equipo del incidente) | 5 anos desde el cierre (OBL-RET-05), con cadena de custodia |
| `DPIA` / `Risk` (RiskAssessment) | La evaluacion de impacto en la privacidad de un `Treatment` de alto riesgo, y el nivel de riesgo calculado | MOD-014 | Tratamiento evaluado, motivo(s) de apertura, volumen estimado de titulares, categorias de datos (heredadas), monitoreo/perfilado, uso de nuevas tecnologias, transferencia internacional asociada, encargados involucrados, cuestionario de factores de riesgo, medidas de seguridad existentes (referencia a `Control`), nivel de riesgo calculado, riesgo residual estimado, conclusion (siempre una decision humana, nunca automatica) | Abierta -> Cuestionario en curso -> Evaluada (riesgo calculado) -> Aprobada/Vigente -> (marcada para revision al vencer la fecha de proxima revision) | No de forma directa (referencias al tratamiento y categorias, nunca el dato del titular; la ayuda del campo de evidencia advierte no subir datos reales de las personas afectadas) | Tratamiento activo mas 5 anos [opinion de producto]; evidencia de OBL-DOC-03 |
| `Control` | Una medida de seguridad tecnica, organizativa o fisica, con su evidencia de implementacion; catalogo unico compartido con MOD-014 | MOD-015 | Nombre, categoria (organizativa/tecnica/fisica), tipo, ambito de aplicacion, responsable, evidencia de implementacion, fecha de implementacion, periodicidad y proxima fecha de revision, proveedor externo asociado, justificacion de no implementacion (si aplica), aprobador de la excepcion | Pendiente de implementar, Implementado, Implementado con hallazgo, Vencido, No aplica - Exceptuado, Archivado | No (informacion organizativa y tecnica; unico dato de persona natural es el responsable interno del control, por referencia a `User`) | Indefinida hasta que MOD-016 fije un plazo especifico; algunos controles con vigencia propia (por ejemplo, pentest anual) |
| `RetentionRule` | Una regla que fija cuanto tiempo se conserva un dato del titular por finalidad (motor 1), o un documento/expediente de cumplimiento propio (motor 2) | MOD-016 | Motor 1: tratamiento vinculado, categoria de datos, finalidad heredada, fundamento(s) de retencion (OBL-RET-01/02/03 o "sin norma especifica" con justificacion), plazo por cada fundamento, fecha efectiva (maximo entre todos los fundamentos activos), accion al vencer, aprobacion requerida. Motor 2: tipo de documento de cumplimiento, documento/expediente de origen, fecha de inicio del computo, plazo minimo, bloqueo de eliminacion anticipada | Activo -> Proximo a vencer -> (Listo para eliminar o Retenido por obligacion, si se agrega un nuevo fundamento) -> Aprobado para eliminar -> Eliminado | No de forma directa: guarda referencias (tratamiento, categoria, sistema) y metadatos de plazo, nunca el dato del titular en si (anti-feature 8); el motor 2 referencia el expediente sin duplicar su contenido | La propia regla no vence; su historial se conserva de forma indefinida por trazabilidad (evidencia de OBL-RET-01 a 06) |

### 9.2.8 Gobierno y evidencia (MOD-018, MOD-019, AuditLog)

| Entidad | Que representa | Modulo propietario | Atributos funcionales clave | Estados del ciclo de vida | Datos personales y como se minimiza | Retencion aplicable |
|---|---|---|---|---|---|---|
| `ComplianceAudit` | Un ciclo de auditoria anual sustantiva de cumplimiento de las Politicas ACE | MOD-018 | Titulo/periodo, tipo (interna/externa/mixta), alcance (obligaciones y modulos), periodo cubierto, responsable, firma auditora externa (si aplica), checklist base (controles y tratamientos incluidos), conclusion/resumen ejecutivo, informe de auditoria | Planificada, En ejecucion, Hallazgos en revision, Plan de accion en curso, Cerrada, Cancelada | No (metadatos del programa de la empresa: que controles, que tratamientos, que obligaciones, que responsables internos, nunca datos de titulares externos) | Indefinida con archivado manual hasta que MOD-016 fije un plazo especifico; evidencia de OBL-AUD-01 |
| `Hallazgo` | Un hallazgo concreto detectado dentro de una `ComplianceAudit`, con su severidad y estado de correccion | MOD-018 (sub-registro de `ComplianceAudit`) | Descripcion, obligacion/control/tratamiento relacionado, severidad, evidencia del hallazgo, estado | Abierto, En correccion, Corregido, Riesgo aceptado | No (misma logica que `ComplianceAudit`; la ayuda del campo advierte no adjuntar datos de titulares sin necesidad) | Igual que `ComplianceAudit` |
| `Evidence` | Un elemento de prueba de que una obligacion se cumplio (registro, archivo, aprobacion o log), generado automaticamente por el modulo de origen o cargado manualmente | MOD-019 | Obligacion(es) relacionada(s), modulo de origen, tipo de evidencia, origen del registro (automatico/manual), entidad de origen (referencia), archivo adjunto (si aplica), huella de integridad (hash), fecha de captura y de vigencia, estado, responsable de carga, aprobador, nivel de sensibilidad del contenido, version | Faltante, En revision, Disponible, Vencida, Rechazada, Archivada | Si - titular externo cuando el registro de origen lo exige por naturaleza (por ejemplo, un expediente ARCO-POL o de incidente); nunca una base de datos completa, solo el archivo o registro puntual, con control de acceso por nivel de sensibilidad | Igual que el registro que la origina (ver columna "Retencion de referencia" del catalogo D.0 de MOD-019, replicada por modulo de origen en esta misma tabla 9.2) |
| `EvidencePackage` | Un paquete exportable que reune varias `Evidence`, `Document` y eventos de `AuditLog` filtrados, con verificacion de integridad | MOD-019 | Nombre, tipo de paquete (auditoria/requerimiento ACE/procedimiento sancionador/due diligence/inspeccion/a medida), filtros (periodo, obligacion, modulo de origen), contenido, destinatario declarado, manifiesto con hash, firma del paquete completo, formato de exportacion, aprobador del segundo control (si el destinatario es externo) | Borrador, Pendiente de segundo control, Aprobado, Exportado, Archivado | Igual que `Evidence` (el contenido puede incluir datos de titulares por ser el objeto legitimo de la prueba); nunca se ofrece importacion masiva de bases externas | Igual que la evidencia mas restrictiva que agrupa |
| `AuditLog` | El registro tecnico e inmutable de toda accion relevante en cualquier modulo (creacion, edicion, cambio de estado, aprobacion, exportacion) | Transversal, sin modulo propietario unico (cada modulo registra sus propios eventos); consultado por MOD-018 y MOD-019 | Accion, usuario o sistema, fecha y hora, modulo y registro afectado, valor anterior y nuevo | Registrado (append-only; ningun rol puede editarlo ni borrarlo, anti-feature 19) | Puede referenciar indirectamente a un titular cuando el registro afectado es un expediente que lo contiene, nunca el dato en si (solo el identificador del registro) | Indefinida por diseno (append-only); ninguna ficha fija un plazo de purga (ver "Contradicciones y huecos detectados") |

### 9.2.9 Capa transversal (MOD-021 a MOD-026)

| Entidad | Que representa | Modulo propietario | Atributos funcionales clave | Estados del ciclo de vida | Datos personales y como se minimiza | Retencion aplicable |
|---|---|---|---|---|---|---|
| `Task` | Una accion concreta asignada a un responsable, generada por cualquier modulo de proceso o creada manualmente | MOD-021 | Titulo, descripcion, modulo de origen, obligacion relacionada, tipo de tarea, prioridad, responsable, area, fecha limite (calculada por MOD-023 cuando hay plazo legal), criterio de computo mostrado, dependencia (tarea previa), evidencia requerida, archivos adjuntos, comentarios (bitacora inmutable), es recurrente/periodicidad, nivel de confidencialidad | Pendiente, En proceso, Bloqueada, En revision, Aprobada, Completada, No aplica ("Vencida" no es un estado adicional del ciclo de vida: es una bandera visual paralela que se activa cuando la fecha limite se cumple sin llegar a Completada o No aplica, ver MOD-021_ficha.md secciones F.1 y F.2 y 12_tareas_y_alertas.md seccion 12.1.3) | Si - referenciado, no almacenado (nunca copia el dato del titular; referencia el expediente de origen; el campo "Nivel de confidencialidad" evita tratar igual una tarea administrativa y una que toca datos sensibles) | Segun la clasificacion del objeto que la tarea sustenta (regla de MOD-016) |
| `Approval` | La aprobacion o rechazo formal de una `Task` en revision, por el rol que corresponda segun el tipo de acto | MOD-021 | Tarea relacionada, tipo de aprobacion, rol requerido, aprobador asignado, fecha de solicitud y de resolucion, decision (Aprobada/Devuelta con cambios/Rechazada), comentario de la decision, identidad del aprobador, version del objeto aprobado | Pendiente -> Aprobada / Devuelta con cambios / Rechazada | Igual que `Task` | Igual que `Task` |
| `Notification` | Un aviso generado por un evento de `Task`, de plazo (MOD-023) o directo de ARCO-POL/Incidentes, entregado por uno o varios canales | MOD-022 | Familia de evento, canal de entrada, modulo de origen funcional, objeto de origen (referencia), obligacion relacionada, nivel (INFO/WARNING/HIGH/CRITICAL), titulo y cuerpo (version plataforma y version canal externo, sin datos personales del titular), destinatario(s) resuelto(s), canal(es) resuelto(s), estado de entrega por canal, leida, acuse de recibo (obligatorio en CRITICAL), estado de escalamiento, resumen aplicado | Pendiente de envio, Enviada, Entregada, Fallida, Reintentando (mas los atributos de lectura/acuse/escalamiento) | No de forma directa: nunca contiene el dato personal del titular ni el detalle sustantivo del caso, solo una referencia al objeto de origen; la version enviada por canal externo (correo) es aun mas restringida | Igual que el expediente que la origino |
| `CalendarEvent` | Una solicitud de calculo de plazo que un modulo consumidor hace a MOD-023 (modulo solicitante, obligacion relacionada, evento de inicio, tipo de computo, duracion, capa de calendario aplicable, es suspendible, criterio ante ambiguedad juridica) | MOD-023 | Ver descripcion; no tiene ciclo de vida propio, es un calculo bajo demanda que devuelve una fecha limite y un desglose | No aplica (calculo, no un registro persistente con estados propios; el resultado se referencia desde la `Task` u otro registro que lo solicito) | No (solo referencia el expediente de origen, nunca el dato del titular) | Igual que el expediente que consulto el plazo |
| `HolidayCalendar` | El calendario de dias inhabiles organizado en 6 capas (fin de semana, calendario nacional, asuetos ad hoc, asuetos locales por sede, calendario propio de la empresa, calendario de la autoridad/ACE) | MOD-023 | Anio calendario, capa, fecha, nombre del asueto, alcance, sede/municipio (capa 3), fuente de la fecha, fecha de verificacion | Borrador, Publicado, Vigente, Actualizado, Historico | No (fechas, nombres de asuetos y fuentes documentales publicas) | Historico conservado sin plazo de purga definido |
| `RegulatoryInstrument` / `RegulatoryRuleVersion` | El marco normativo consultable (leyes, normativa ACE, lineamientos, politicas de actuacion, buena practica) y cada version de una regla operativa que ese instrumento define | MOD-024 | Nombre, tipo de instrumento, clasificacion de exigibilidad (OBLIGATORIO/RECOMENDADO/CONDICIONAL), numero y fecha de emision, fecha de publicacion en el Diario Oficial, fecha de entrada en vigencia, estado (VIGENTE/FUTURO/DEROGADO/MODIFICADO), estado de verificacion, fuente oficial, obligaciones relacionadas, version de regla con fechas de vigencia | Contenido vivo mantenido por el Editor de contenido regulatorio del proveedor; de solo lectura para la organizacion cliente | No (contenido normativo, no un dato de la empresa cliente ni de sus titulares) | Sin plazo (contenido de referencia vivo; las versiones historicas se conservan para reconstruir que regla aplicaba en el pasado) |
| `ReformaActivationFlag` | La bandera unica de activacion manual del doble estado de la reforma 659 (ver 9.7) | MOD-024 | `regimen_reforma_659` (ACTUAL/FUTURO), fecha de aprobacion legislativa, estado interno de verificacion (campo tecnico de workflow del proveedor), fecha de publicacion en el Diario Oficial de la reforma, validacion juridica del texto oficial, fecha de cumplimiento de la vacatio legis, fecha de activacion, motivo de reversion (si aplica) | Instancia unica y global: ACTUAL (por defecto) -> FUTURO (activacion manual, nunca automatica por la sola fecha de aprobacion legislativa); reversion posible con motivo obligatorio | No | Historico de cambios de bandera conservado de forma indefinida (trazabilidad) |
| `SanctionProcedure` | Un procedimiento administrativo sancionador de la ACE contra la empresa cliente | MOD-024 | Origen del caso, fecha de notificacion recibida, via (simplificada/ordinaria), infracciones imputadas (catalogo Art. 56), escrito de contestacion, decision de allanamiento, pruebas propuestas, resultado de la resolucion final, monto de la multa, medidas adicionales, comprobante de pago, recurso interpuesto, fecha de firmeza y de prescripcion | Emplazamiento recibido -> Contestacion -> (Via simplificada u ordinaria) -> Resolucion (sin sancion/leve/grave/muy grave) -> Pago/Recurso -> Firme | Si - personal interno puntual (nombre de la persona que firma la contestacion o que la ACE identifique como presunto responsable; referenciado, no duplicado del RAT ni de MOD-001) | 5 anos minimo (OBL-SANC-07) |
| `ACEFiling` | Un tramite formal de la empresa ante la ACE (comunicacion de nombramiento del Delegado, actualizacion de sus datos, puesta en conocimiento de una transferencia, solicitud de opinion previa, solicitud de certificacion/sello) | MOD-024 | Tipo de tramite, modulo de origen, contenido del tramite (precargado por referencia), estado del tramite, canal de envio, documento adjunto, acuse o respuesta de la ACE | Borrador, Pendiente de envio, Enviado, Confirmado, Rechazado, No aplica | No de forma directa (tramite institucional; puede referenciar al `ResponsableDelProgramaDeDatos` por su nombre institucional) | Segun el expediente especifico que lo origina (MOD-002 o MOD-010) |
| `HelpArticle` | Un articulo de ayuda contextual por modulo, con su fundamento normativo en segundo nivel | MOD-026 | Codigo del articulo, modulo asociado, titulo, tipo de contenido, texto "que es"/"por que"/"fundamento"/"cuando necesito ayuda juridica", clasificacion del fundamento, fuente primaria citada, version, estado del contenido, regimen aplicable (si cita una obligacion afectada por la reforma 659), palabras clave, articulos relacionados | Borrador, En revision legal, Publicado, Marcado para revision, Obsoleto/archivado | No (contenido de referencia generico del proveedor); unico dato personal tangencial es el nombre del revisor legal, personal del proveedor, no del cliente | Sin plazo (contenido de referencia vivo) |
| `Search Log` [propuesta de esta seccion a partir de la seccion D.3 de MOD-025_ficha.md, que no lo nombra como entidad del catalogo de `06_mapa_definitivo_de_modulos.md` seccion 7 pero si lo define como registro propio] | El registro tecnico de cada consulta de Busqueda Global, con minimizacion reforzada en ambito sensible | MOD-025 | Usuario, fecha y hora, tipos de contenido filtrados, indicador booleano "ambito sensible"; el termino exacto solo se conserva fuera de ambito sensible | Registrado (append-only, no editable) | Si - referenciado, no almacenado en ambito sensible: si la consulta cae en ARCO-POL, Incidentes, Riesgos/EIPD o coincide con una categoria sensible del diccionario de sinonimos, el termino exacto se descarta tras procesar la consulta, conservando solo que hubo busqueda, en que ambito, quien y cuando | Sin plazo de purga definido para el registro fuera de ambito sensible (ver "Contradicciones y huecos detectados") |

---

## 9.3 Relaciones entre entidades

La tabla usa cardinalidad conceptual (uno a uno, uno a muchos, muchos a muchos), sin claves ni indices. "Modulo que crea la relacion" es siempre el modulo propietario de la entidad origen o destino que la instancia (regla de "direccion unica", 9.1.3).

| Entidad origen | Relacion (verbo) | Entidad destino | Cardinalidad conceptual | Modulo que crea la relacion | Nota |
|---|---|---|---|---|---|
| `Organization` | tiene | `BusinessUnit` | Uno a muchos | MOD-001 | Una organizacion, varias sucursales/unidades; ver 9.6 sobre el limite de una sola razon social en el MVP |
| `Organization` | tiene | `User` | Uno a muchos | MOD-001 | - |
| `User` | ocupa | `Role` | Muchos a muchos | MOD-001 | Un usuario puede acumular varios roles (comun en pyme, 5.3 de `05_tipos_de_usuario.md`) |
| `Organization` | designa | `ResponsableDelProgramaDeDatos` | Uno a muchos en el tiempo, uno vigente a la vez (mas suplente opcional) | MOD-002 | Puede haber un historico de designaciones sucesivas; solo una vigente, mas un `delegado_sustituto` opcional |
| `User` | es | `ResponsableDelProgramaDeDatos` | Uno a uno (si el usuario ya existe en MOD-001) | MOD-002 | Precarga de nombre/correo/telefono desde el perfil de usuario |
| `Organization` | ejecuta | `DiagnosticoRespuesta` | Uno a muchos | MOD-004 | Varias sesiones historicas, nunca se sobrescriben (9.1.4) |
| `DiagnosticoRespuesta` | genera | `Treatment` (sugerido) | Uno a muchos | MOD-004 (siembra la biblioteca de MOD-006) | El diagnostico sugiere tratamientos; la empresa los confirma en el RAT |
| `DiagnosticoRespuesta` | genera | `AccionDelPlan` | Uno a muchos | MOD-005 | El plan se deriva del resultado del diagnostico |
| `AccionDelPlan` | se ejecuta en | (modulo de ejecucion, por ejemplo `Treatment`, `Document`, `Control`) | Uno a uno con el registro concreto de ese modulo | MOD-005 (referencia), el modulo de ejecucion (contenido real) | El plan organiza y da seguimiento; el trabajo real vive en el modulo de ejecucion |
| `Treatment` | tiene | `System` | Uno a muchos | MOD-006 | - |
| `Treatment` | involucra | `Encargado` | Muchos a muchos | MOD-006 (referencia), MOD-009 (propietario del `Encargado`) | Un tratamiento puede tener varios encargados; un encargado puede servir a varios tratamientos |
| `Treatment` | fundamenta | `Consent` | Uno a muchos | MOD-007 | Solo si la base de licitud del tratamiento es "Consentimiento" |
| `Consent` | se revoca mediante | `ConsentWithdrawal` | Uno a uno (por revocacion) | MOD-007 | Un `Consent` vigente puede tener a lo sumo una `ConsentWithdrawal` activa |
| `Consent` | referencia | `DocumentVersion` (Aviso de Privacidad) | Muchos a uno | MOD-007 (referencia), MOD-008 (propietario) | Nunca copia el texto, referencia la version exacta vigente al momento de la captura |
| `Treatment` | se documenta en | `Document` (Aviso/Politica) | Muchos a muchos | MOD-006/MOD-008 | Un aviso puede cubrir varios tratamientos; un tratamiento puede citarse en varios documentos |
| `Encargado` / `TerceroReceptor` / `Subencargado` | se respalda en | `Contrato/DPA` | Uno a uno (contrato vigente) | MOD-009 | Puede generarse un borrador desde la plantilla de MOD-008 |
| `Subencargado` | depende de | `Encargado` | Muchos a uno | MOD-009 | Un encargado puede tener varios subencargados |
| `Treatment` | se transfiere mediante | `Transfer` | Uno a muchos | MOD-010 | - |
| `Transfer` | tiene como receptor a | `Encargado` / `TerceroReceptor` / `Subencargado` | Muchos a uno | MOD-010 (referencia), MOD-009 (propietario) | - |
| `Transfer` | se acredita con | `Consent` | Muchos a uno (opcional) | MOD-010 (referencia), MOD-007 (propietario) | Solo si la base juridica de la transferencia es "Consentimiento previo" |
| `Transfer` | se comunica mediante | `ACEFiling` | Uno a uno | MOD-024 | Puesta en conocimiento a la ACE (OBL-TRANSF-05) |
| `Titular` | presenta | `PrivacyRequest` | Uno a muchos | MOD-011 (o MOD-012 como canal) | - |
| `PrivacyRequest` | incluye | `IdentityVerification` | Uno a uno | MOD-011 | - |
| `PrivacyRequest` | notifica a | `Encargado` | Uno a muchos (si el tratamiento tiene encargados) | MOD-011 (dispara), MOD-009 (destinatario referenciado) | Notificacion a receptores tras rectificacion/eliminacion (OBL-ARCO-11) |
| `Incident` | afecta a | `Treatment` | Muchos a muchos | MOD-013 (referencia), MOD-006 (propietario) | Un incidente puede afectar varios tratamientos |
| `Incident` | involucra a | `Encargado` | Muchos a uno (opcional) | MOD-013 (referencia), MOD-009 (propietario) | Cuando el origen es "Proveedor/Encargado" |
| `Treatment` | se evalua mediante | `DPIA` | Uno a muchos | MOD-014 | Un tratamiento de alto riesgo puede tener varias EIPD historicas |
| `DPIA` | selecciona | `Control` | Muchos a muchos | MOD-014 (referencia), MOD-015 (propietario del catalogo) | Catalogo unico, nunca duplicado (9.1.1) |
| `Treatment` / `Encargado` / `Transfer` | aplica | `Control` | Muchos a muchos | MOD-015 (propietario), referenciado desde MOD-006/MOD-009/MOD-010 | El ambito de un control puede ser un sistema, un tratamiento o "toda la organizacion" |
| `Treatment` | tiene | `RetentionRule` (motor 1) | Uno a muchos | MOD-016 | Una o varias reglas segun categoria de dato |
| `Document` (Aviso publicado) / `PrivacyRequest` (cerrada) / `Incident` (cerrado) | se protege con | `RetentionRule` (motor 2) | Uno a uno | MOD-016 | Bloqueo de eliminacion anticipada por defecto |
| `TrainingProgram` | genera | `TrainingRecord` | Uno a muchos | MOD-017 | Un registro por persona capacitada |
| `TrainingRecord` (del Delegado) | alimenta a | `ResponsableDelProgramaDeDatos` | Muchos a uno | MOD-017 (origen), MOD-002 (referencia) | Insumo de `fecha_ultima_capacitacion_delegado` y `atestados_reverificacion`, sin duplicar el registro |
| `ComplianceAudit` | produce | `Hallazgo` | Uno a muchos | MOD-018 | - |
| `Hallazgo` | genera | `Task` (accion correctiva) | Uno a muchos | MOD-018 (dispara), MOD-021 (propietario de `Task`) | - |
| `ComplianceAudit` | consulta | `Evidence` | Muchos a muchos | MOD-018 (consulta), MOD-019 (propietario) | Dependencia de datos bidireccional y continua: MOD-018 consulta evidencia de MOD-019 para sus hallazgos, y sus hallazgos se registran de vuelta como nueva `Evidence` en MOD-019 (unica excepcion de ciclo en el mapa, seccion 6.1 de `06_mapa_definitivo_de_modulos.md`) |
| (todo modulo de proceso, MOD-002 a MOD-018 y MOD-021) | genera | `Evidence` | Uno a muchos | El modulo de origen (ver catalogo D.0 de MOD-019) | Automatico cuando el modulo de origen ya existe; manual si el modulo de origen aun no cubre esa evidencia en el MVP |
| `Evidence` | se agrupa en | `EvidencePackage` | Muchos a muchos | MOD-019 | Un paquete filtra evidencia por periodo, obligacion o modulo de origen |
| (todo modulo) | escribe evento en | `AuditLog` | Muchos a uno (destino compartido) | Cada modulo escribe sus propios eventos | Entidad transversal sin propietario unico (9.2.8) |
| (todo modulo de proceso) | genera | `Task` | Uno a muchos | El modulo de origen (referenciado en el campo "Modulo de origen" de `Task`) | MOD-021 recibe eventos de generacion de tarea de practicamente todo modulo de proceso (ver nota de asimetria en "Contradicciones y huecos detectados") |
| `Task` | requiere | `Approval` | Uno a uno (cuando el tipo de tarea lo exige) | MOD-021 | No toda tarea genera una aprobacion |
| `Task` / `Approval` / `CalendarEvent` (plazo) | dispara | `Notification` | Uno a muchos | MOD-022 (propietario de `Notification`), MOD-021/MOD-023/MOD-011/MOD-013 (origen del evento) | Canal de entrada restringido a esos cuatro modulos segun `depende_de` de MOD-022 en `mapa_modulos.json` |
| `Task` (con plazo legal) | consulta | `CalendarEvent` | Uno a uno por calculo | MOD-023 | El modulo solicitante nunca calcula el plazo por su cuenta |
| `ReformaActivationFlag` | condiciona a | `ResponsableDelProgramaDeDatos`, `PrivacyRequest`, `Consent`, `TrainingProgram`, `RetentionRule` (documental) | Uno a muchos (afecta a las 17 obligaciones de la seccion 5 de `06_mapa_definitivo_de_modulos.md`) | MOD-024 | Ver 9.7 |
| `SanctionProcedure` | consulta | `CalendarEvent` | Muchos a uno | MOD-023 | Plazos de contestacion, pago y prescripcion |
| `HelpArticle` | se asocia a | (cualquier modulo) | Muchos a uno | MOD-026 | Un articulo se asocia a un modulo o a "Transversal/general" |
| `Search Log` | referencia | (cualquier entidad indexada) | Muchos a uno | MOD-025 | Nunca copia el contenido del registro, solo su metadato buscable |

---

## 9.4 Diagramas conceptuales ASCII

Los siete diagramas de dominio corresponden exactamente a los siete dominios exigidos por esta tarea; equivalen a los nueve grupos de la seccion 9.2 asi: "Organizacion y personas" une 9.2.1; "Registro de tratamientos" une 9.2.2 y 9.2.3 (el diagnostico y el plan preceden y alimentan al RAT); "Relacion con el titular" es 9.2.4; "Terceros y transferencias" es 9.2.6; "Riesgo, seguridad e incidentes" es 9.2.7; "Gobierno y evidencia" une 9.2.5 y 9.2.8 (los documentos institucionales se gobiernan junto con la auditoria y la evidencia); "Capa transversal" es 9.2.9.

### 9.4.0 Diagrama general

```
                              +-------------------+
                              |   Organization    |
                              | (BusinessUnit,     |
                              |  User, Role)       |
                              +-------------------+
                                       |
                                       v
                         +----------------------------+
                         | ResponsableDelPrograma      |<--- ReformaActivationFlag
                         | DeDatos (tipo_rol)          |     (MOD-024, ver 9.7)
                         +----------------------------+
                                       |
                                       v
                   +---------------------------------------+
                   |     DiagnosticoRespuesta / AccionDelPlan|
                   +---------------------------------------+
                                       |
                                       v
     +------------------------------------------------------------------+
     |                        Treatment (RAT)                            |
     |  System | DataCategory | Purpose/LegalBasis (embebidos)           |
     +------------------------------------------------------------------+
        |            |                |                 |
        v            v                v                 v
   +---------+  +-----------+   +------------+   +-----------------+
   | Consent |  | Document/ |   | Encargado/ |   |  DPIA / Control  |
   | Consent |  | DocVersion|   | Tercero/   |   |  (riesgo/seg.)   |
   |Withdrawal| |(Aviso,Pol)|   | Subenc.    |   +-----------------+
   +---------+  +-----------+   +------------+           |
        |                             |                   v
        v                             v            +-------------+
  +---------------+            +-------------+      |  Incident   |
  | PrivacyRequest|            |  Transfer   |      +-------------+
  | (ARCO-POL)    |            +-------------+
  +---------------+                   |
        |                             v
        v                       +-----------+
   +----------+                 | ACEFiling |
   |  Titular |                 +-----------+
   +----------+

     Todo lo anterior escribe y es consultado por la
     CAPA TRANSVERSAL: Task | Approval | Notification |
     CalendarEvent/HolidayCalendar | RegulatoryInstrument/
     RegulatoryRuleVersion | HelpArticle | Search Log

     Todo lo anterior alimenta a
     GOBIERNO Y EVIDENCIA: Evidence | EvidencePackage |
     ComplianceAudit/Hallazgo | AuditLog (transversal)
```

### 9.4.1 Organizacion y personas

```
+--------------+        1..N        +---------------+
| Organization |------------------->| BusinessUnit   |
+--------------+                    | / Sucursal     |
      |                             +---------------+
      | 1..N
      v
+--------------+      M..N      +---------+
|    User      |<-------------->|  Role   |
+--------------+                +---------+
      |
      | 0..1 (un usuario puede ser tambien el Responsable)
      v
+------------------------------+       depende de la
| ResponsableDelProgramaDeDatos |<----- bandera de MOD-024
| (tipo_rol: DELEGADO |         |       (ver 9.7)
|  RESPONSABLE_INTERNO)         |
+------------------------------+
      |
      v
+------------------+       +------------------+
|  TrainingProgram |------>|  TrainingRecord   |
+------------------+  1..N +------------------+
```

### 9.4.2 Registro de tratamientos

```
+---------------------+      +-------------------+
| DiagnosticoRespuesta |----->|   AccionDelPlan   |
+---------------------+      +-------------------+
          | sugiere                    | organiza y da
          v                             | seguimiento a
+---------------------------------------------------+
|                     Treatment                       |
|  (Purpose y LegalBasis embebidos como catalogo)     |
+---------------------------------------------------+
      |            |                |
      v            v                v
 +--------+   +-----------+   +--------------+
 | System |   | DataCategory|  | (referencias  |
 +--------+   | (catalogo)  |  | a Consent,    |
              +-----------+   | Encargado,    |
                               | Transfer,     |
                               | Control, DPIA)|
                               +--------------+
```

### 9.4.3 Relacion con el titular

```
+----------+   presenta    +------------------+   incluye   +---------------------+
| Titular  |-------------->|  PrivacyRequest   |------------>| IdentityVerification|
+----------+               +------------------+             +---------------------+
     ^                            |
     | consulta estado            | notifica a
     | (Portal, MOD-012)          v
     |                     +--------------+
     |                     |  Encargado    |
     |                     +--------------+
     |
     |  otorga / revoca
     v
+---------+   revoca    +------------------+
| Consent |------------>| ConsentWithdrawal|
+---------+             +------------------+
     |
     | referencia version vigente
     v
+------------------+
| DocumentVersion   |
| (Aviso Privacidad)|
+------------------+
```

### 9.4.4 Terceros y transferencias

```
+--------------+   1..N   +---------------+
|  Treatment   |--------->|   Encargado    |------+
+--------------+          +---------------+      |
       |                          ^                | depende de
       |                          | subcontrata     v
       |                   +---------------+  +--------------+
       |                   | TerceroReceptor|  | Subencargado |
       |                   +---------------+  +--------------+
       |                          |
       v                          v
+--------------+          +---------------+
|   Transfer   |<---------|  Contrato/DPA |
+--------------+          +---------------+
       |
       v
+--------------+
|  ACEFiling    |
+--------------+
```

### 9.4.5 Riesgo, seguridad e incidentes

```
+--------------+    se evalua con    +----------+   selecciona   +---------+
|  Treatment   |-------------------->|   DPIA   |--------------->| Control |
+--------------+                     +----------+   (catalogo    +---------+
       |                                                unico)        ^
       | puede sufrir                                                  |
       v                                                                | aplica a
+--------------+                                                        |
|   Incident   |------------------------------------------------------->
+--------------+
       |
       v
+------------------------+
| RetentionRule (motor 1 |
| y motor 2)              |
+------------------------+
```

### 9.4.6 Gobierno y evidencia

```
+-----------+      versiona      +----------------+
| Document  |------------------->| DocumentVersion|
+-----------+                    +----------------+
                                          |
                                          v (referenciado, nunca copiado)
+------------------------------------------------------------+
|                        Evidence                              |
|  (generada por todo modulo de proceso, MOD-002 a MOD-018,   |
|   MOD-021, ver catalogo D.0 de MOD-019)                      |
+------------------------------------------------------------+
       |                                    ^
       | se agrupa en                       | consulta y alimenta
       v                                    |
+------------------+              +-------------------+
|  EvidencePackage |              |  ComplianceAudit /  |
+------------------+              |  Hallazgo           |
                                   +-------------------+
                                          ^
                                          | escribe/lee
                                          |
                              +----------------------+
                              |      AuditLog          |
                              | (transversal, append-  |
                              |  only, sin propietario  |
                              |  unico)                 |
                              +----------------------+
```

### 9.4.7 Capa transversal

```
                    +--------------------------------------------+
                    |         CAPA TRANSVERSAL (consultada,       |
                    |         nunca consulta al reves)             |
                    +--------------------------------------------+
                              |          |          |
                              v          v          v
 +--------+   requiere   +----------+  genera   +---------------+
 |  Task  |------------->| Approval |<----------| (modulo de     |
 +--------+              +----------+           |  proceso)      |
     |                                            +---------------+
     | dispara
     v
 +--------------+     consulta      +------------------------+
 | Notification |<------------------|  CalendarEvent /        |
 +--------------+                   |  HolidayCalendar         |
                                    +------------------------+
                                              ^
                                              |
                          +---------------------------------------+
                          | RegulatoryInstrument / RegulatoryRule   |
                          | Version / ReformaActivationFlag /       |
                          | SanctionProcedure / ACEFiling            |
                          +---------------------------------------+
                                              ^
                                              |
                          +---------------------------------------+
                          |  HelpArticle   |   Search Log            |
                          +---------------------------------------+
```

---

## 9.5 Catalogos maestros

Un catalogo maestro es un conjunto de valores de referencia que varios modulos comparten por consulta, nunca por copia. La columna "Quien lo mantiene" distingue el equipo del producto (contenido que viene precargado y solo el proveedor edita) de la organizacion cliente (contenido que la empresa configura para su propio caso).

| Catalogo | Contenido | Quien lo mantiene | Modulo donde vive | Nota |
|---|---|---|---|---|
| Categorias de datos (`DataCategory`) | Catalogo de datos ordinarios y sensibles (union del Art. 4 lit. g y el Art. 59 lit. b) | Equipo del producto (la union de ambas listas es una decision de diseno documentada en MOD-006, seccion D.4); la organizacion solo marca cuales aplican a cada tratamiento | MOD-006 | No editable por la organizacion cliente en su definicion legal; si en su uso por tratamiento |
| Bases de licitud (`LegalBasis`) | Las seis bases del Art. 5 lit. g mas las excepciones del Art. 28 y Art. 37/38 | Equipo del producto (fijo, deriva directamente de la ley) | MOD-006 (embebido en `Treatment`), MOD-007 (excepciones) | No editable |
| Paises | Catalogo ISO de paises, con "El Salvador" preseleccionado y no removible | Equipo del producto | MOD-001 (paises donde opera), MOD-009 y MOD-010 (pais del proveedor/receptor) | Compartido entre los tres modulos, nunca una lista propia por modulo |
| Tipos de documento de identidad | DUI, Pasaporte, Carnet de residente, Partida de nacimiento (herederos) | Equipo del producto | MOD-011, MOD-012, MOD-002 | - |
| Catalogo de controles (`Control`) | Lista inicial de controles organizativos, tecnicos y fisicos (Art. 4 de las Politicas ACE) | Equipo del producto crea la plantilla inicial al completar el diagnostico; la organizacion agrega, edita estado y evidencia de los suyos | MOD-015 (propietario), MOD-014 (consume el mismo catalogo) | Catalogo unico, nunca duplicado (9.1.1) |
| Calendario de asuetos (`HolidayCalendar`) | 6 capas: fin de semana, calendario nacional, asuetos ad hoc, asuetos locales por sede, calendario propio de la empresa, calendario de la ACE | Equipo del producto mantiene las capas 0, 1, 2 y 5; la organizacion mantiene las capas 3 y 4 | MOD-023 | Ver 9.2.9 |
| Reglas normativas (`RegulatoryInstrument` / `RegulatoryRuleVersion`) | Leyes, normativa ACE, lineamientos, politicas de actuacion, buena practica, con su estado VIGENTE/FUTURO/DEROGADO/MODIFICADO | Equipo del producto (Editor de contenido regulatorio); de solo lectura para la organizacion cliente | MOD-024 | Incluye la bandera unica `regimen_reforma_659` (ver 9.7) |
| Plantillas de documentos | Plantillas de Politica de Proteccion de Datos, Politica de Privacidad, Aviso de Privacidad, Procedimiento ARCO-POL, Contrato/DPA | Equipo del producto | MOD-008 | La organizacion edita el contenido, no la plantilla base |
| Biblioteca de tratamientos plantilla | 22 fichas de tratamiento comunes (nomina, reclutamiento, CRM, videovigilancia, biometria, etc., ver MOD-006 seccion D.6) | Equipo del producto | MOD-006 | La organizacion copia y edita, nunca queda en Vigente sin revision humana |
| Articulos de ayuda (`HelpArticle`) | Contenido de "que es / por que / fundamento / cuando necesito ayuda juridica" por modulo, mas diccionario de sinonimos de busqueda | Equipo del producto | MOD-026 (articulos), MOD-025 (diccionario de sinonimos) | - |
| Catalogo de infracciones y multas | Las 26 infracciones del Art. 56 con su rango de multa en salarios minimos | Equipo del producto (deriva directamente de la ley) | MOD-024 | Informativo, no calcula la sancion real, solo el rango legal |
| Roles estandar | Los 12 roles de `05_tipos_de_usuario.md`, seccion 5.3, y su matriz de permisos por defecto | Equipo del producto define los 12 estandar; la organizacion crea roles personalizados sobre esa base | MOD-001 | Ver seccion 11 de este blueprint para el detalle de permisos |

---

## 9.6 Multi-organizacion

`Organization` (9.2.1) representa, en el MVP, una sola razon social con una o varias `BusinessUnit`/sucursales bajo el mismo NIT: decision de alcance 2.7.31 de `02_validacion_de_la_idea.md`, confirmada en MOD-001_ficha.md seccion D.1 ("el MVP soporta una organizacion con varias sucursales, no multiples razones sociales/grupos"). Todo el resto del modelo de esta seccion (Treatment, PrivacyRequest, Evidence, etc.) cuelga de una unica `Organization` activa a la vez; no existe en el MVP una entidad "Holding" o "Grupo corporativo" que agrupe varias `Organization` bajo una misma cuenta con vision consolidada.

El caso de "Grupo Financiero Itzalco" (perfil 5 de `05_tipos_de_usuario.md`, seccion 5.1: banco, aseguradora y financiera bajo una misma holding) es, de forma explicita, funcionalidad V1/Enterprise, no MVP: la Directora de Cumplimiento Corporativo necesita "comparar el estado entre sociedades" y exige "separacion estricta de datos entre sociedades", pero el propio perfil aclara que esa vision consolidada multi-sociedad "es funcionalidad V1/Enterprise, no MVP" (decision 2.7.31). Tres senales adicionales, ya presentes en las fichas, confirman que el sistema se prepara para esa evolucion sin construirla todavia:

- MOD-002 (Delegado) incluye el campo `delegado_comun_grupo_societario` ("marque si esta misma persona es Delegado de otras sociedades de su mismo grupo empresarial"), pero documentado como "Opcional (fuera del MVP, ver seccion Q)".
- MOD-020 (Dashboard) reserva el filtro "Sociedad (grupo empresarial)", pero aclara que "no aplicable mientras el MVP no soporte multi-sociedad" y que ese filtro "queda listo pero inactivo hasta que exista esa capacidad".
- El perfil 10 de `05_tipos_de_usuario.md` (Delegada externa que atiende a varios clientes, cada uno con su propia organizacion) es un caso distinto del grupo corporativo: no es una sola empresa con varias sociedades, sino un profesional externo con cuentas en varias organizaciones no relacionadas entre si, "cambiando entre las organizaciones de sus distintos clientes dentro de una misma cuenta, viendo unicamente los datos del cliente activo en cada momento". Ninguna ficha define el mecanismo de entidad que resuelve este segundo caso (ver "Contradicciones y huecos detectados").

Cuando la funcionalidad de grupo corporativo se construya (fuera del alcance de este blueprint de MVP), el principio de este modelo que debe preservarse es el mismo de 9.1.2 (propietario unico) aplicado a nivel de organizacion: cada `Treatment`, `PrivacyRequest`, `Incident`, etc. debe seguir perteneciendo a exactamente una `Organization` (una sociedad), sin mezclar datos entre sociedades del mismo grupo; una vista consolidada (la que pediria la Directora de Cumplimiento Corporativo) se construiria como una capa de agregacion de solo lectura sobre varias `Organization`, nunca fusionando sus registros en una sola.

---

## 9.7 Doble estado de la reforma 659 en el modelo de informacion

Esta subseccion aplica al modelo de datos el diseno ya decidido y detallado en la seccion 5 de `06_mapa_definitivo_de_modulos.md` ("Explicacion del doble estado de la reforma 659, sin duplicar modulos"); no repite su fundamento juridico completo, solo la traduccion al catalogo de entidades de 9.2.

**Una sola entidad.** `ResponsableDelProgramaDeDatos` (9.2.1) es la unica entidad para el Delegado de Proteccion de Datos, hoy obligatorio (Arts. 15 y 17 LPDP vigentes), y para el eventual Responsable interno si la reforma 659 entra en vigencia. El atributo `tipo_rol` (DELEGADO / RESPONSABLE_INTERNO) distingue el regimen sin crear una segunda entidad ni un segundo modulo.

**Una bandera unica, ajena a la entidad que regula.** `ReformaActivationFlag` (9.2.9) es una instancia unica y global que vive en MOD-024, no dentro de `ResponsableDelProgramaDeDatos`: el campo `regimen_reforma_659` (ACTUAL/FUTURO) se activa manualmente, nunca por la sola fecha de aprobacion legislativa (17-sep-2026), y solo cuando el equipo del producto confirme la publicacion del decreto en el Diario Oficial y transcurran los 8 dias de vacatio legis (por analogia con el Art. 64 LPDP). Al 24-sep-2026, la bandera permanece en ACTUAL.

**Las entidades afectadas cambian de estado, no de estructura.** Las 17 obligaciones marcadas `afectada_por_reforma_659.afectada = true` en `matriz_obligaciones.json` (OBL-DPO-01 a 08, OBL-ARCO-01/08/10/11/14, OBL-CONS-03, OBL-CAP-02, OBL-RET-04, OBL-PLAZO-05) recaen sobre cinco entidades del catalogo de 9.2, sin que ninguna de ellas cambie de modulo propietario ni de campos cuando la bandera cambia:

| Entidad | Que cambia cuando la bandera pasa a FUTURO |
|---|---|
| `ResponsableDelProgramaDeDatos` (MOD-002) | El atributo `tipo_rol` pasa a RESPONSABLE_INTERNO para los nuevos nombramientos; deja de exigirse la comunicacion formal a la ACE, la reverificacion trienal y los informes semestrales como obligacion, aunque la entidad y sus campos siguen existiendo (continuidad voluntaria, punto 7 de la seccion 5 del mapa) |
| `PrivacyRequest` (MOD-011) | El campo "persona que aprueba y ejecuta" deja de requerir el rol vigente segun MOD-024 con el significado de "Delegado obligatorio"; las solicitudes se presentan directamente ante la empresa |
| `ConsentWithdrawal` (MOD-007) | El destinatario de la notificacion de revocacion (campo "persona que aprueba y ejecuta") depende del `tipo_rol` vigente |
| `TrainingProgram` de tipo Plan anual (MOD-017) | El campo calculado "Aplica bajo el regimen" pasa de "Obligatorio (regimen ACTUAL)" a "Buena practica voluntaria (regimen FUTURO sin Delegado voluntario)" |
| `Document`/`DocumentVersion` del Aviso de Privacidad (MOD-008) | No se reescribe automaticamente: MOD-024 dispara una `Task` ("revisar avisos publicados tras el cambio de regimen") en vez de sobrescribir un documento ya publicado |

**Preservacion de historial.** Cuando la bandera cambia, las `Task` de MOD-021 que dependian de pasos exclusivos del regimen ACTUAL no se eliminan: se marcan "no aplica bajo el estado regulatorio actual, ver historial" (9.1.5). Un `PrivacyRequest` o un expediente del Delegado ya cerrado antes del cambio conserva las reglas vigentes en el momento de su cierre, porque `RegulatoryRuleVersion` (MOD-024) versiona sus propias reglas igual que MOD-002 versiona sus formularios y checklists (9.1.4).

**Version de reglas.** `RegulatoryRuleVersion` es el mecanismo generico que permite reconstruir, para cualquier expediente, que version de una regla (un plazo, un formulario, un checklist) aplicaba en la fecha en que ese expediente se abrio o se cerro, sin importar cuantas veces cambie despues el marco normativo.

---

## 9.8 Datos personales: que guarda el sistema y que no debe guardar nunca

Esta subseccion aplica el principio 9.1.6 con el detalle de `22_anti_features.md` y de las secciones de minimizacion de cada ficha ya citadas en el catalogo de 9.2.

### 9.8.1 Lo que el sistema nunca debe guardar (privacidad por diseno)

| Nunca almacenar | Por que | Que si se guarda en su lugar | Fuente |
|---|---|---|---|
| La base de datos completa de clientes, empleados o cualquier titular del cliente (CRM, ERP, nomina completa) | Anti-feature 1 y 8: el sistema no es un CRM ni un repositorio central de datos del cliente | Metadatos del tratamiento en `Treatment`: que sistema, quien lo administra, categorias de dato, retencion | `22_anti_features.md`, items 1 y 8 |
| El dato biometrico, de salud u otro dato sensible en si (por ejemplo, la plantilla de huella digital, el expediente clinico completo) | Anti-feature 9: riesgo de seguridad y de privacidad desproporcionado | La existencia del tratamiento, su base legal (`Treatment`, `Consent`) y su ubicacion (`System`); solo un adjunto puntual y estrictamente necesario para un expediente ARCO-POL o de incidente, con controles reforzados | `22_anti_features.md`, item 9 |
| Las grabaciones de videovigilancia | Anti-feature 10: el sistema no opera como plataforma de videovigilancia | El tratamiento de videovigilancia (`Treatment`), su base legal y su `DPIA`, nunca las imagenes | `22_anti_features.md`, item 10 |
| El contenido de una `Notification` con el dato personal del titular o el detalle sustantivo de un caso, en cualquier canal (plataforma o correo) | Frontera de privacidad de MOD-022: un canal externo (bandeja de correo) esta fuera del perimetro de control del sistema | Una referencia al objeto de origen (numero de expediente); quien recibe el aviso entra al expediente, autenticado, con sus propios permisos | `22_anti_features.md`, items 8 y 9; MOD-022_ficha.md seccion D |
| El termino exacto de una busqueda que cae en ambito sensible (Search Log) | Evitar conservar por escrito, de forma permanente, un nombre o dato sensible que un usuario escribio para buscar | Que hubo una busqueda, en que ambito, quien la hizo, cuando y si obtuvo resultados | MOD-025_ficha.md, seccion D.3 |
| Documento de identidad, fecha de nacimiento o direccion personal de los `User` internos de la empresa cliente | El control de acceso interno no necesita ese nivel de dato personal (a diferencia de los titulares externos, que si lo requieren como objeto legitimo de otros procesos) | Nombre, correo corporativo, cargo, area y rol, lo estrictamente necesario para operar el RBAC | MOD-001_ficha.md, seccion D.4 |
| Expediente laboral completo, contratos o evaluaciones de desempeno como respaldo de una capacitacion | Anti-feature 8 aplicado al expediente de RRHH | Solo la constancia, lista de asistencia o certificado especifico de esa sesion (`TrainingRecord`) | MOD-017_ficha.md, seccion D.2 |
| Una copia paralela de un `Document` o su contenido dentro de otro modulo (por ejemplo, dentro de `Task`, `Notification` o `EvidencePackage`) | Regla de "direccion unica" (9.1.3): el modulo que crea el dato sigue siendo su unico propietario | Una referencia a la version exacta del documento | Regla 3, seccion 10.1 de este blueprint |

### 9.8.2 Lo que el sistema si guarda, como objeto legitimo del proceso, y como se minimiza incluso ahi

| Modulo / entidad | Dato personal que si guarda | Minimizacion aplicada |
|---|---|---|
| `Consent` (MOD-007) | Nombre e identificador de referencia del titular, texto exacto presentado, firma o evidencia de aceptacion | Nunca copia el perfil completo del CRM del cliente; nunca guarda el dato sensible en si, solo la evidencia de que se pidio consentimiento para tratarlo |
| `PrivacyRequest` / `IdentityVerification` (MOD-011) | Nombre, documento de identidad, domicilio, contacto y contenido de la solicitud del titular (o de su representante o heredero) | Adjuntos de identidad cifrados, acceso restringido a Responsable ARCO-POL y Delegado/Responsable interno; el acceso de lectura queda registrado en el historial |
| `Titular` (Portal, MOD-012) | Los mismos datos de identidad que exige `PrivacyRequest`, sin duplicarlos: el Portal solo referencia el expediente y guarda metadatos propios de cada sesion de consulta | La duplicacion que se evita no es la del dato personal en si (que es legitimo), sino la de guardarlo dos veces en dos modulos distintos |
| `Incident` (MOD-013) | Categorias y cantidades estimadas de titulares afectados; un adjunto puntual solo cuando es indispensable para el caso | Nunca la extraccion masiva de la base afectada; el adjunto queda cifrado y con acceso restringido al equipo del incidente |
| `Evidence` / `EvidencePackage` (MOD-019) | Puede contener, de forma legitima, documentos de identidad (via `PrivacyRequest`), descripciones de personas afectadas (via `Incident`) o firmas (via `Consent`) | Control de acceso por el campo "Nivel de sensibilidad del contenido"; la guia de minimizacion antes de adjuntar advierte explicitamente no subir una base de datos completa; nunca se ofrece importacion masiva |
| `SanctionProcedure` (MOD-024) | El nombre de la persona que firma la contestacion, o la que la ACE identifique como presunto responsable | Se referencia por lo estrictamente necesario para el expediente, sin duplicar el RAT ni el inventario de personas de MOD-001 |

---

## Contradicciones y huecos detectados

### Contradicciones

1. **`06_mapa_definitivo_de_modulos.md` seccion 7 / `mapa_modulos.json` (campo `entidades_principales` de MOD-006) frente a `MOD-006_ficha.md` seccion D.1.** El mapa y el JSON listan `Purpose` y `LegalBasis` como entidades conceptuales independientes de `Treatment`. La ficha propietaria (MOD-006), que es la fuente de detalle, las modela como campos catalogados dentro de `Treatment` ("Finalidad" y "Base de licitud", con su justificacion), sin ciclo de vida ni formulario propio. Se adopta la version de la ficha propietaria para el nivel de detalle funcional de esta seccion (9.2.3): `Purpose` y `LegalBasis` se documentan como atributos catalogados de `Treatment`, conservando sus nombres conceptuales de `mapa_modulos.json` para no romper la trazabilidad del catalogo de entidades citado en otras secciones del blueprint. Motivo de la eleccion: la jerarquia de esta tarea situa `mapa_modulos.json` por encima de la ficha propietaria solo para resolver una discrepancia de fondo (por ejemplo, a que modulo pertenece una obligacion); aqui no hay discrepancia de fondo sobre a quien pertenecen estos conceptos (MOD-006 en ambas fuentes), sino solo de nivel de modelado, y en ese nivel la ficha es, por definicion de esta misma tarea, "la fuente principal de detalle".
2. **`MOD-013_ficha.md` seccion D.1 frente a `MOD-009_ficha.md` seccion D.1 y `06_mapa_definitivo_de_modulos.md` seccion 7.** El campo "Proveedor/Encargado relacionado" de un `Incident` se describe como "Referencia a entidad Vendor (MOD-009)". Ni la ficha propietaria de MOD-009 ni el mapa definitivo usan el nombre "Vendor": MOD-009 modela tres subtipos distintos (`Encargado`, `TerceroReceptor`, `Subencargado`), sin una entidad generica unificadora con ese nombre. Se adopta el modelo de la ficha propietaria (MOD-009): en el catalogo de 9.2.6 y en las relaciones de 9.3, "Vendor" se trata como una etiqueta informal que MOD-013 usa para referirse a cualquiera de los tres subtipos, nunca como una cuarta entidad independiente.
3. **`MOD-010_ficha.md` seccion D frente a `MOD-024_ficha.md` seccion D.4.** El campo de `Transfer` que muestra el estado de la puesta en conocimiento a la ACE lista solo cuatro valores de lectura ("Borrador / Pendiente de envio / Enviado -sin canal oficial confirmado- / No aplica"), mientras que `ACEFiling`, cuyo propietario es MOD-024, define seis estados (agrega CONFIRMADO y RECHAZADO). La propia ficha de MOD-024 aclara que esto no es un error sino una simplificacion de lectura deliberada para el usuario de Transferencias, y deja como recomendacion para una revision futura de MOD-010 incorporar los dos estados faltantes a su vista de solo lectura. Se adopta el modelo completo de seis estados de `ACEFiling` (MOD-024, modulo propietario de la entidad) como el ciclo de vida canonico en el catalogo de 9.2.9; la vista de cuatro estados de MOD-010 se documenta como una proyeccion simplificada de esa misma entidad, no como una entidad distinta.

### Huecos

1. **Un mismo usuario (por ejemplo, un Delegado externo) con acceso a varias organizaciones no relacionadas entre si.** El perfil 10 de `05_tipos_de_usuario.md` (Licda. Silvia Melendez) necesita "cambiar entre las organizaciones de sus distintos clientes dentro de una misma cuenta, viendo unicamente los datos del cliente activo en cada momento". Ninguna ficha de MOD-001 ni de ningun otro modulo define la entidad o el mecanismo que permite a un mismo `User` pertenecer, con una sola cuenta, a varias `Organization` no relacionadas entre si (a diferencia del grupo corporativo de 9.6, que es una sola holding con varias sociedades relacionadas). Requiere validacion de producto antes de construirse.
2. **Una entidad conceptual para "grupo corporativo" u "holding" que relacione varias `Organization`.** El perfil 5 de `05_tipos_de_usuario.md` y el filtro reservado en MOD-020 confirman que esta capacidad es V1/Enterprise, pero ninguna ficha propone la estructura de datos (por ejemplo, si es una entidad nueva que agrupa `Organization`, o un atributo de `Organization` que apunta a una holding). Ver 9.6.
3. **Politica de retencion o purga para `AuditLog`.** El registro tecnico transversal se documenta de forma consistente en varias fichas (MOD-016, MOD-019) como de conservacion "indefinida hasta que MOD-016 fije un plazo especifico"; ninguna ficha, incluida la propia MOD-016 (cuyo motor documental de retencion en su seccion D.2 solo cubre tres tipos de documento: aviso publicado, expediente ARCO-POL cerrado y expediente de incidente cerrado), define una regla de retencion para `AuditLog`, ni tampoco para `Evidence`/`EvidencePackage` en general, `ComplianceAudit`, `DPIA` o `Control` fuera de esos tres tipos. Esto ya esta senalado, de forma parcial y dispersa, dentro de la propia tabla D.0 de `MOD-019_ficha.md` ("indefinida hasta que MOD-016 fije un plazo especifico" se repite para varios modulos de origen); esta seccion lo consolida como un unico hueco del modelo de retencion.
4. **Politica de retencion para `Search Log` fuera de ambito sensible.** MOD-025_ficha.md define con detalle que el termino de busqueda se descarta cuando la consulta cae en ambito sensible, pero no fija un plazo de conservacion para el registro de consultas que no caen en ese ambito (por ejemplo, buscar "plantilla de aviso de privacidad").
5. **Retencion propia del expediente de `Organization` y de `HolidayCalendar`.** Ninguna ficha (MOD-001, MOD-023) fija cuanto tiempo se conserva el historial de una organizacion dada de baja, ni si el calendario historico de anios pasados se archiva o purga en algun momento; ambos se documentan en esta seccion como "conservado sin plazo de purga definido" (9.2.1 y 9.2.9), a falta de una regla explicita en MOD-016.
6. **Estados del ciclo de vida de `RetentionRule` documentados fuera del diagrama de workflow.** El catalogo de entidades de MOD-016 (seccion D) no nombra los seis estados de la regla (ACTIVO, PROXIMO A VENCER, LISTO PARA ELIMINAR, RETENIDO POR OBLIGACION, APROBADO PARA ELIMINAR, ELIMINADO) como una lista cerrada; solo aparecen dentro del diagrama ASCII de la seccion F (Workflow) de esa ficha. Esta seccion los reproduce en 9.2.7 tomandolos de ese diagrama; se deja constancia de que la seccion D de esa ficha, a diferencia de casi todas las demas, no repite el catalogo de estados junto a los campos de la entidad.
