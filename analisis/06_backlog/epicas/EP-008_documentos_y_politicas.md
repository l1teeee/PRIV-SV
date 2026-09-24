# EP-008 Documentos y Politicas (MOD-008)

**Objetivo.** La empresa puede redactar, aprobar, publicar y versionar su Politica de Proteccion de Datos, su Politica de Privacidad y su Aviso de Privacidad con el checklist legal completo, y cualquier otro modulo puede reutilizar el mismo motor documental para sus propios tipos de documento.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R1 | 18 | 62 | 62 | 0 | [MOD-008](../../03_modulos/MOD-008_ficha.md) |

**Notas de la epica.**

- La tabla Q clasifica como SHOULD HAVE tanto la deteccion automatica de encargado no mencionado (regla G-2) como la tarea automatica tras el cambio de regimen 659 (regla G-3). Se excluye G-2 de esta epica porque ademas depende de que MOD-009 (release R2) este operativo con datos reales; se incluye G-3 (HU-008-13) porque el encargo de esta epica lo pide de forma explicita y el modulo del que depende, MOD-024, se construye en el mismo release R1 que MOD-008 (seccion 19.8 del roadmap), lo que satisface la condicion que la propia justificacion de la tabla Q pone para incluirla. Se deja constancia de esta discrepancia con la clasificacion literal de la tabla Q.
- Se excluyen de esta epica, por ser SHOULD HAVE, COULD HAVE o FUTURE en la tabla Q: el wizard guiado con ejemplo por literal del Art. 24, el paquete de exportacion con verificacion de integridad (hash o firma), las plantillas para documentos internos no regulatorios, el multi-idioma y la firma electronica avanzada.
- El literal h) del checklist del Art. 24 (datos de contacto del encargado) usa en esta epica el campo de texto libre que describe la seccion L de la ficha, porque MOD-009 (que aportaria la referencia formal al catalogo de Encargados) se construye en el release R2, posterior a MOD-008 (R1).
- La regla de conservacion de 10 anios sin borrado (cobertura de OBL-RET-04 y OBL-RET-06, obligaciones colaboradoras propiedad de MOD-016 segun la seccion 19.4 del roadmap) queda incorporada de forma nativa en el ciclo de vida del documento (HU-008-07 Publicar y HU-008-08 Archivar, con los estados terminales HISTORICO y ARCHIVADO de solo lectura), sin necesitar una historia separada.
- HU-008-18 entrega la plantilla generica de Evaluacion de Impacto (EIPD) que cubre parcialmente a MOD-014 segun la seccion 19.4 del roadmap. La tarea elaborar EIPD que consume esa plantilla la crea el Diagnostico de Cumplimiento (MOD-004), fuera de esta epica.
- Los campos especificos del tipo de documento Contrato/DPA (partes, plazo del contrato, clausulas exigidas al encargado) no se incluyen en esta epica: son propiedad de la ficha de MOD-009, que reutiliza el motor generico construido aqui (HU-008-01, 02, 05, 06, 07, 08, 09, 14 y 15, marcadas habilitadora). Por esa misma razon ninguna historia de esta epica declara depende_de_modulos hacia MOD-009: la dependencia estructural corre en sentido inverso.
- El indicador de estado de documentos regulatorios (seccion M de la ficha) y su presentacion en el dashboard se consideran responsabilidad de la epica de MOD-020 (Dashboard y Reportes, release R2); esta epica ya deja disponibles, a traves de sus historias de flujo, los estados y conteos que ese indicador necesita, sin requerir una historia propia.
- PP-MAPA-03 (seccion 24.7 de 04_secciones/24_preguntas_pendientes.md) senala que el mapa definitivo agrupa OBL-AVISO-01/02/03/05 como si las cuatro fueran OBLIGATORIO sin condicion. La propia ficha de MOD-008 y esta epica ya reflejan correctamente que OBL-AVISO-02 y OBL-AVISO-03 son CONDICIONAL (HU-008-03), por lo que esa discrepancia de documentacion del mapa no bloquea ninguna historia de esta epica.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-008-01 | Configurar el catalogo de tipos de documento y la cadena de aprobacion por tipo | Administrador de la organizacion | 3 | R1 | 12 | MOD-001 |
| HU-008-02 | Crear y editar el borrador de un documento a partir de la plantilla de su tipo | Responsable Legal / Compliance | 3 | R1 | 13 | MOD-001, MOD-002 |
| HU-008-03 | Completar el checklist de los nueve literales del Art. 24 en el Aviso de Privacidad | Responsable Legal / Compliance | 3 | R1 | 17 | HU-008-02 |
| HU-008-04 | Completar el checklist de los cinco elementos del Art. 7 en la Politica de Privacidad y el Aviso de Privacidad | Responsable Legal / Compliance | 2 | R1 | 17 | HU-008-02 |
| HU-008-05 | Enviar un documento a revision y registrar su rechazo con motivo | Responsable Legal / Compliance | 5 | R1 | 13 | HU-008-01, HU-008-02, MOD-021, MOD-022 |
| HU-008-06 | Aprobar un documento en revision segun la cadena configurada | Aprobador | 5 | R1 | 13 | HU-008-05, MOD-001, MOD-019 |
| HU-008-07 | Publicar la version aprobada de un documento | Administrador de la organizacion | 8 | R1 | 13 | HU-008-06, MOD-019 |
| HU-008-08 | Archivar un documento descontinuado con doble aprobacion cuando aplica | Administrador de la organizacion | 5 | R1 | 14 | HU-008-07 |
| HU-008-09 | Iniciar una nueva version de un documento que requiere revision | Responsable Legal / Compliance | 3 | R1 | 14 | HU-008-07 |
| HU-008-10 | Pasar el Aviso de Privacidad vigente a Requiere revision cuando el RAT registra una finalidad nueva | Responsable Legal / Compliance | 3 | R1 | 17 | HU-008-07, MOD-006, MOD-021, MOD-022 |
| HU-008-11 | Pasar un documento vigente a Requiere revision al vencer su intervalo de revision periodica | Responsable Legal / Compliance | 5 | R1 | 17 | HU-008-07, MOD-023, MOD-021, MOD-022 |
| HU-008-12 | Alertar cuando no exista un Aviso de Privacidad publicado pese a tratamientos activos | Administrador de la organizacion | 2 | R1 | 17 | MOD-022, MOD-023 |
| HU-008-13 | Crear una tarea de revision de avisos publicados cuando cambia el regimen de la reforma 659 | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R1 | 17 | HU-008-07, MOD-024, MOD-021, MOD-022 |
| HU-008-14 | Adjuntar evidencia de publicacion de un documento | Responsable Legal / Compliance | 2 | R1 | 13 | HU-008-07, MOD-019 |
| HU-008-15 | Exportar la version vigente de un documento a PDF | Responsable Legal / Compliance | 2 | R1 | 14 | HU-008-07 |
| HU-008-16 | Consultar el inventario de documentos regulatorios y el historial de versiones | Auditor (interno) | 3 | R1 | 17 | HU-008-07 |
| HU-008-17 | Invitar a un asesor externo a comentar un documento especifico en revision | Administrador de la organizacion | 3 | R1 | 18 | HU-008-05 |
| HU-008-18 | Proveer la plantilla generica de Evaluacion de Impacto (EIPD) en el catalogo de documentos | Equipo de contenido del producto (proveedor) | 2 | R1 | 13 | HU-008-02 |

## Historias

### HU-008-01. Configurar el catalogo de tipos de documento y la cadena de aprobacion por tipo

**Como** Administrador de la organizacion, **quiero** configurar, para cada tipo de documento del catalogo, la lista de roles que deben aprobarlo antes de publicarse, y ampliar el catalogo con tipos adicionales cuando mi empresa los necesite, **para** que ningun documento se publique sin pasar por los revisores que mi empresa decidio, y que el catalogo se adapte a los documentos internos que mi empresa quiera gestionar.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 12 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado que reviso el catalogo de tipos de documento, cuando lo abro, entonces veo los cuatro tipos fijos (Politica de Proteccion de Datos, Politica de Privacidad, Aviso de Privacidad, Procedimiento ARCO-POL) mas los tipos que haya agregado, sin poder eliminar ni renombrar los cuatro tipos fijos.
2. Dado que agrego un tipo nuevo al catalogo extensible (Plantilla interna u Otro documento regulatorio), cuando indico un nombre, entonces el sistema lo agrega a la lista de tipos disponibles para crear documentos, sin afectar los documentos ya creados de otros tipos.
3. Dado que configuro la cadena de aprobacion de un tipo de documento, cuando selecciono uno o varios roles disponibles en MOD-001 como aprobadores, entonces el sistema guarda esa cadena y la aplica a toda version futura de ese tipo de documento.
4. Dado que el tipo es Aviso de Privacidad o Politica de Privacidad, cuando intento guardar una cadena de aprobacion vacia, entonces el sistema no permite guardar y muestra que ese tipo exige al menos un rol aprobador distinto del autor.
5. Dado que edito la cadena de aprobacion de un tipo de documento, cuando guardo el cambio, entonces el sistema registra en el historial quien la modifico, el valor anterior y el nuevo valor, y la nueva cadena aplica solo a partir de ese momento.
6. Dado que un usuario con un rol distinto de Administrador intenta abrir la configuracion del catalogo o de la cadena de aprobacion, cuando lo intenta, entonces el sistema deniega el acceso.

**Reglas de negocio**

- El catalogo fijo de 4 tipos no es editable ni eliminable.
- La cadena de aprobacion de Aviso de Privacidad y Politica de Privacidad exige al menos un rol aprobador distinto del autor.
- Los cambios de cadena de aprobacion quedan en el historial con el valor anterior y el nuevo.

**Fuera de alcance**

- La accion de aprobar o rechazar una version especifica (ver HU-008-05 y HU-008-06).
- El umbral configurable de separacion de funciones en si mismo, que vive en MOD-001.

- Referencia: MOD-008 secciones C, D (fila Cadena de aprobacion aplicable) y F

### HU-008-02. Crear y editar el borrador de un documento a partir de la plantilla de su tipo

**Como** Responsable Legal / Compliance, **quiero** crear un documento nuevo eligiendo su tipo y editar su contenido a partir de la plantilla precargada con las variables de mi organizacion, **para** iniciar cada documento regulatorio sin partir de una pagina en blanco y sin volver a escribir a mano los datos que ya existen en el sistema.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 13 | Si |

- Fundamento: OBL-AVISO-01 (Art. 24, Ley para la Proteccion de Datos Personales); OBL-AVISO-05 (Art. 24 inc. 1, Ley para la Proteccion de Datos Personales); OBL-DOC-01 (Art. 33 inc. 1, Ley para la Proteccion de Datos Personales)
- Depende de: -
- Modulos requeridos: MOD-001, MOD-002

**Criterios de aceptacion**

1. Dado que elijo un tipo de documento del catalogo y un nombre entre 3 y 120 caracteres que no este en uso por otro documento vigente del mismo tipo, cuando confirmo la creacion, entonces el sistema crea el documento en BORRADOR con su primera DocumentVersion, precargada con la plantilla del tipo elegido y con la razon social, los datos de contacto y el nombre del Delegado o Responsable interno vigente resueltos automaticamente.
2. Dado que intento crear un documento con un nombre ya usado por otro documento vigente del mismo tipo, o con menos de 3 o mas de 120 caracteres, cuando confirmo, entonces el sistema no crea el documento y muestra el error correspondiente.
3. Dado que el documento esta en BORRADOR, cuando modifico su contenido, entonces el sistema guarda el cambio sobre la version en curso y registra en el historial que el contenido se modifico, con usuario y fecha.
4. Dado que reviso las variables precargadas (razon social, contacto, Delegado o Responsable interno), cuando intento editarlas directamente en el documento, entonces el sistema no lo permite y me indica que se corrigen en Organizacion o en Delegado.
5. Dado que adjunto un archivo de respaldo en PDF o DOCX de hasta 10 MB, cuando lo subo, entonces el sistema lo guarda vinculado a la version en curso.
6. Dado que intento adjuntar un archivo de mas de 10 MB o de un formato distinto de PDF o DOCX, cuando lo subo, entonces el sistema rechaza el archivo y muestra el error.
7. Dado que un usuario con rol Responsable de area, Auditor o Usuario de consulta intenta crear o editar un documento, cuando lo intenta, entonces el sistema deniega la accion.

**Reglas de negocio**

- El nombre es unico dentro del mismo tipo mientras el documento este vigente.
- Las variables precargadas son de solo lectura dentro del documento.
- El archivo adjunto es opcional, PDF o DOCX, maximo 10 MB.
- Editar el contenido de un borrador no crea una version formal nueva.

**Fuera de alcance**

- El checklist de Aviso de Privacidad (HU-008-03) y el de Politica de Privacidad/Aviso (HU-008-04).
- Enviar el documento a revision (HU-008-05).

- Requiere contenido: Plantilla de Politica de Proteccion de Datos validada por abogado; Plantilla de Politica de Privacidad validada por abogado; Plantilla de Aviso de Privacidad validada por abogado, con el checklist de los 9 literales integrado; Plantilla de Procedimiento ARCO-POL validada por abogado
- Requiere validacion legal: Si
- Referencia: MOD-008 secciones D, E, F (transiciones Crear documento y Editar contenido) y G regla 6

### HU-008-03. Completar el checklist de los nueve literales del Art. 24 en el Aviso de Privacidad

**Como** Responsable Legal / Compliance, **quiero** marcar, para cada uno de los nueve literales del Art. 24, si el Aviso de Privacidad los cubre, y justificar los que no apliquen, **para** verificar que el Aviso no omita ninguno de los puntos que la ley exige antes de enviarlo a revision.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 17 | No |

- Fundamento: OBL-AVISO-01 (Art. 24, Ley para la Proteccion de Datos Personales); OBL-AVISO-02 (Art. 24 lit. h), Ley para la Proteccion de Datos Personales); OBL-AVISO-03 (Art. 24 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-008-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que abro el checklist de un documento tipo Aviso de Privacidad, cuando lo veo, entonces encuentro las nueve casillas de los literales a) a i) del Art. 24, todas sin marcar en un documento recien creado.
2. Dado que intento marcar como no aplica alguno de los literales a), b), c), d), e) o f), cuando lo intento, entonces el sistema no lo permite porque esos seis literales son siempre exigidos.
3. Dado que marco el literal h) (datos del encargado) como no aplica, cuando lo guardo sin escribir una justificacion breve, entonces el sistema no permite guardar el checklist como completo.
4. Dado que marco el literal h) como aplicable, cuando no indico al menos un encargado (por referencia a MOD-009 si esta disponible, o como texto libre con nombre y contacto mientras no lo este), entonces el sistema no permite guardar el checklist como completo.
5. Dado que marco el literal i) (cookies) como no aplica sin escribir una justificacion breve, cuando lo guardo, entonces el sistema no permite guardar el checklist como completo.
6. Dado que las nueve casillas quedan en un estado valido, cuando reviso el checklist, entonces el sistema lo muestra como completo y habilita enviar el documento a revision.
7. Dado que intento enviar el documento a revision con el checklist incompleto, cuando lo intento, entonces el sistema no permite la transicion y me indica que literales faltan.

**Reglas de negocio**

- Los literales a) a f) son siempre obligatorios, sin opcion de no aplica.
- Los literales h) e i) admiten no aplica solo con una justificacion breve obligatoria.
- El checklist completo es condicion para enviar el Aviso de Privacidad a revision.

**Fuera de alcance**

- El wizard guiado con ejemplo por literal (SHOULD HAVE, ver notas_epica).
- El checklist de los cinco elementos del Art. 7 (HU-008-04).

- Requiere contenido: Textos de ayuda por literal del Art. 24, validados por abogado, para la tarjeta de ayuda contextual de MOD-026
- Requiere validacion legal: Si
- Referencia: MOD-008 seccion D, fila Checklist de contenido minimo Art. 24; seccion L
- Notas: El literal h no depende de que MOD-009 este operativo (release R2); mientras tanto se usa el campo de texto libre que describe la seccion L de la ficha.

### HU-008-04. Completar el checklist de los cinco elementos del Art. 7 en la Politica de Privacidad y el Aviso de Privacidad

**Como** Responsable Legal / Compliance, **quiero** marcar, para la Politica de Privacidad y para el Aviso de Privacidad, si cada uno de los cinco elementos del Art. 7 esta cubierto, **para** verificar que ambos documentos informen correctamente el derecho de informacion en la recoleccion antes de enviarlos a revision.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 17 | No |

- Fundamento: OBL-AVISO-04 (Art. 7, Ley para la Proteccion de Datos Personales)
- Depende de: HU-008-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que abro el checklist de un documento tipo Politica de Privacidad o Aviso de Privacidad, cuando lo veo, entonces encuentro las cinco casillas (proposito y destinatarios; existencia de la base de datos, respaldos y sitios de contingencia; identidad y contacto de responsable y encargado; contenido de los derechos ARCO-POL y mecanismos para ejercerlos; medidas de seguridad activas), todas sin marcar en un documento recien creado.
2. Dado que intento marcar el checklist como completo con alguna de las cinco casillas sin marcar, cuando lo intento, entonces el sistema no lo permite.
3. Dado que marco las cinco casillas, cuando reviso el checklist, entonces el sistema lo muestra como completo y habilita enviar el documento a revision.
4. Dado que intento enviar a revision un documento tipo Politica de Privacidad o Aviso de Privacidad con este checklist incompleto, cuando lo intento, entonces el sistema no permite la transicion.
5. Dado que el documento es del tipo Politica de Proteccion de Datos o Procedimiento ARCO-POL, cuando reviso su ficha, entonces el sistema no exige este checklist porque solo aplica a Politica de Privacidad y Aviso de Privacidad.

**Reglas de negocio**

- Las cinco casillas son siempre obligatorias, sin opcion de no aplica.
- El checklist aplica solo a Politica de Privacidad y Aviso de Privacidad.

**Fuera de alcance**

- El checklist de los nueve literales del Art. 24 (HU-008-03).

- Requiere contenido: Textos de ayuda de los cinco elementos del Art. 7, validados por abogado
- Requiere validacion legal: Si
- Referencia: MOD-008 seccion D, fila Cinco elementos del Art. 7

### HU-008-05. Enviar un documento a revision y registrar su rechazo con motivo

**Como** Responsable Legal / Compliance, **quiero** enviar un documento en BORRADOR a revision y, si un revisor lo rechaza, ver el motivo para corregirlo, **para** que el documento pase por la cadena de aprobacion configurada antes de poder publicarse.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 13 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-008-01, HU-008-02
- Modulos requeridos: MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que el documento esta en BORRADOR con contenido no vacio, y si es Aviso de Privacidad o Politica de Privacidad tiene sus checklists completos, cuando lo envio a revision, entonces el sistema lo pasa a EN_REVISION, crea una tarea de revision en MOD-021 para cada rol de la cadena de aprobacion configurada y envia la alerta correspondiente por MOD-022.
2. Dado que el documento esta en BORRADOR con el contenido vacio, cuando intento enviarlo a revision, entonces el sistema no permite la transicion.
3. Dado que el documento es Aviso de Privacidad o Politica de Privacidad con algun checklist incompleto, cuando intento enviarlo a revision, entonces el sistema no permite la transicion.
4. Dado que el documento esta en EN_REVISION, cuando un rol de la cadena de aprobacion lo rechaza sin escribir un comentario, entonces el sistema no permite registrar el rechazo.
5. Dado que un rol de la cadena de aprobacion rechaza el documento con un comentario de hasta 1000 caracteres, cuando lo registra, entonces el sistema pasa el documento a BORRADOR, notifica al autor con el motivo por MOD-022 y registra el evento en el historial con el comentario.
6. Dado que un usuario que no pertenece a la cadena de aprobacion configurada para ese tipo de documento intenta aprobar o rechazar, cuando lo intenta, entonces el sistema deniega la accion.

**Reglas de negocio**

- El contenido no vacio y los checklists completos son condicion para enviar a revision.
- El comentario es obligatorio al rechazar.
- Solo los roles de la cadena configurada pueden aprobar o rechazar.

**Fuera de alcance**

- La aprobacion final cuando todos los roles de la cadena aprueban (HU-008-06).

- Referencia: MOD-008 seccion F, tabla de transiciones, filas Enviar a revision y Rechazar

### HU-008-06. Aprobar un documento en revision segun la cadena configurada

**Como** Aprobador, **quiero** aprobar un documento en EN_REVISION cuando todos los roles de la cadena configurada lo hayan aprobado, **para** que el contenido quede congelado con un hash de integridad y listo para publicarse.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 13 | Si |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-008-05
- Modulos requeridos: MOD-001, MOD-019

**Criterios de aceptacion**

1. Dado que el documento esta en EN_REVISION y todavia falta que uno o mas roles de la cadena aprueben, cuando yo apruebo, entonces el sistema registra mi aprobacion con mi identidad y fecha, pero el documento permanece en EN_REVISION.
2. Dado que el documento esta en EN_REVISION y ya aprobaron todos los roles de la cadena configurada, cuando el ultimo rol aprueba, entonces el sistema pasa el documento a APROBADO, congela el contenido de la version, calcula su hash de integridad y registra la evidencia de cada aprobacion en MOD-019.
3. Dado que el documento es Aviso de Privacidad o Politica de Privacidad y la empresa esta por encima del umbral configurable de separacion de funciones de MOD-001, cuando el autor del borrador intenta aprobar su propia version, entonces el sistema deniega la accion.
4. Dado que el documento es Aviso de Privacidad o Politica de Privacidad y la empresa esta por debajo del umbral configurable, cuando el autor aprueba su propia version, entonces el sistema lo permite mostrando una advertencia visible de autorrevision.
5. Dado que el checklist de contenido minimo del documento no esta completo, cuando se intenta pasar el documento a APROBADO, entonces el sistema no permite la transicion.
6. Dado que el documento pasa a APROBADO, cuando reviso su historial, entonces encuentro la identidad de cada aprobador, la fecha y el hash calculado.

**Reglas de negocio**

- Todos los roles de la cadena configurada deben aprobar antes de pasar a APROBADO.
- El contenido se congela y se calcula el hash al completarse la aprobacion.
- Separacion de funciones con umbral configurable en MOD-001 y advertencia de autorrevision por debajo del umbral.

**Fuera de alcance**

- Publicar la version aprobada (HU-008-07).
- Enviar a revision y rechazar (HU-008-05).

- Referencia: MOD-008 seccion F, tabla de transiciones, fila Aprobar; seccion C, Separacion de funciones; seccion G regla 4

### HU-008-07. Publicar la version aprobada de un documento

**Como** Administrador de la organizacion, **quiero** publicar una version APROBADA fijando su fecha de vigencia, **para** que el documento quede como la version vigente y la version anterior quede conservada como historica.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 13 | Si |

- Fundamento: OBL-AVISO-01 (Art. 24, Ley para la Proteccion de Datos Personales); OBL-AVISO-05 (Art. 24 inc. 1, Ley para la Proteccion de Datos Personales); OBL-RET-04 (Art. 31, Lineamientos para el Delegado de Proteccion de Datos Personales); OBL-RET-06 (Art. 13-A, Ley de Firma Electronica)
- Depende de: HU-008-06
- Modulos requeridos: MOD-019

**Criterios de aceptacion**

1. Dado que el documento esta en APROBADO y defino una fecha de vigencia no anterior a la fecha de aprobacion, cuando publico, entonces el sistema pasa el documento a PUBLICADO / VIGENTE, genera la evidencia de publicacion (fecha, hora, usuario, hash) en MOD-019 y registra el evento en el historial.
2. Dado que ya existia una version PUBLICADO / VIGENTE del mismo documento, cuando publico la nueva version, entonces el sistema pasa automaticamente la version anterior a HISTORICO sin eliminarla.
3. Dado que intento publicar sin definir la fecha de vigencia, o con una fecha anterior a la fecha de aprobacion, cuando lo intento, entonces el sistema no permite la publicacion.
4. Dado que el tipo del documento es Aviso de Privacidad, cuando la publicacion se completa, entonces el sistema notifica que existe una nueva version de referencia disponible para nuevas capturas de consentimiento.
5. Dado que un rol que la cadena configurada no habilita para publicar intenta publicar, cuando lo intenta, entonces el sistema deniega la accion.
6. Dado que una version esta en HISTORICO, cuando cualquier usuario intenta editarla o eliminarla, entonces el sistema lo deniega porque el registro de solo lectura se conserva un minimo de 10 anios.

**Reglas de negocio**

- La fecha de vigencia no puede ser anterior a la fecha de aprobacion.
- La version anterior PUBLICADO / VIGENTE pasa automaticamente a HISTORICO al publicar la nueva.
- HISTORICO es un estado terminal de solo lectura que no se elimina.

**Fuera de alcance**

- Archivar un documento (HU-008-08).
- El registro del consentimiento en si, que gestiona MOD-007.

- Referencia: MOD-008 seccion F, tabla de transiciones, fila Publicar; seccion G regla 7; seccion J

### HU-008-08. Archivar un documento descontinuado con doble aprobacion cuando aplica

**Como** Administrador de la organizacion, **quiero** archivar un documento PUBLICADO / VIGENTE que la empresa descontinua, con una justificacion y, si es Aviso de Privacidad o Politica de Privacidad, con una segunda aprobacion, **para** dejar constancia de por que el documento dejo de estar vigente sin perder su contenido.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 14 | Si |

- Fundamento: OBL-AVISO-01 (Art. 24, Ley para la Proteccion de Datos Personales); OBL-AVISO-05 (Art. 24 inc. 1, Ley para la Proteccion de Datos Personales); OBL-RET-04 (Art. 31, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-008-07
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que solicito archivar un documento que no es Aviso de Privacidad ni Politica de Privacidad, cuando escribo la justificacion, entonces el sistema pasa el documento a ARCHIVADO y registra el evento con la justificacion en el historial.
2. Dado que solicito archivar un Aviso de Privacidad o una Politica de Privacidad, cuando escribo la justificacion, entonces el sistema deja la solicitud pendiente de una segunda aprobacion de un rol Delegado de Proteccion de Datos (o Responsable interno) o Administrador distinto de quien solicito.
3. Dado que la segunda persona aprueba la solicitud de archivo, cuando lo hace, entonces el sistema pasa el documento a ARCHIVADO y registra ambas identidades y fechas en el historial.
4. Dado que intento archivar un Aviso de Privacidad o una Politica de Privacidad sin escribir una justificacion, cuando lo intento, entonces el sistema no permite la solicitud.
5. Dado que la misma persona que solicito el archivo de un Aviso de Privacidad o una Politica de Privacidad intenta dar la segunda aprobacion, cuando lo intenta, entonces el sistema deniega la accion.
6. Dado que un documento esta en ARCHIVADO, cuando cualquier usuario intenta editarlo, eliminarlo o reabrirlo, entonces el sistema lo deniega; para retomar el tipo de documento se debe crear uno nuevo.

**Reglas de negocio**

- La doble aprobacion es obligatoria solo para Aviso de Privacidad y Politica de Privacidad.
- La justificacion es siempre obligatoria al archivar.
- ARCHIVADO es un estado terminal de solo lectura que no se elimina ni se reabre.

**Fuera de alcance**

- Crear el documento de reemplazo (HU-008-02).

- Referencia: MOD-008 seccion C, Separacion de funciones; seccion F, tabla de transiciones, fila Archivar

### HU-008-09. Iniciar una nueva version de un documento que requiere revision

**Como** Responsable Legal / Compliance, **quiero** iniciar una nueva version de un documento que esta en REQUIERE_REVISION, **para** redactar la actualizacion sin dejar de mostrar la version vigente mientras la nueva version se revisa y aprueba.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 14 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-008-07
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el documento esta en REQUIERE_REVISION, cuando inicio una nueva version, entonces el sistema crea una nueva DocumentVersion en BORRADOR con el contenido de la version vigente como punto de partida, y me pide un motivo de la nueva version de hasta 300 caracteres.
2. Dado que la nueva version esta en BORRADOR, cuando la reviso, entonces la version anterior sigue mostrandose como PUBLICADO / VIGENTE hasta que la nueva complete el ciclo completo hasta Publicar.
3. Dado que intento crear la nueva version sin escribir el motivo, cuando lo intento, entonces el sistema no permite continuar.
4. Dado que el documento no esta en REQUIERE_REVISION, cuando intento iniciar una nueva version por esta via, entonces el sistema no ofrece la accion.

**Reglas de negocio**

- La version vigente permanece vigente hasta que la nueva version se publique.
- El motivo de la nueva version es obligatorio a partir de la segunda version del documento.

**Fuera de alcance**

- Los disparadores que llevan a REQUIERE_REVISION (HU-008-10, HU-008-11, HU-008-13).

- Referencia: MOD-008 seccion F, tabla de transiciones, fila Iniciar nueva version; seccion D, fila Motivo de la nueva version

### HU-008-10. Pasar el Aviso de Privacidad vigente a Requiere revision cuando el RAT registra una finalidad nueva

**Como** Responsable Legal / Compliance, **quiero** que el Aviso de Privacidad vigente pase automaticamente a Requiere revision cuando el RAT registra una finalidad de tratamiento nueva sobre datos ya recolectados, **para** no dejar pasar por alto un cambio que el Aviso podria no estar informando todavia.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 17 | No |

- Fundamento: OBL-AVISO-04 (Art. 7, Ley para la Proteccion de Datos Personales); OBL-AVISO-01 (Art. 24, Ley para la Proteccion de Datos Personales)
- Depende de: HU-008-07
- Modulos requeridos: MOD-006, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que existe un Aviso de Privacidad en PUBLICADO / VIGENTE y el RAT (MOD-006) registra una finalidad de tratamiento nueva, cuando el evento llega, entonces el sistema pasa ese Aviso a REQUIERE_REVISION, crea la tarea Actualizar Aviso de Privacidad: nueva finalidad detectada en MOD-021 dirigida a Legal/Compliance (configurable) y envia la alerta correspondiente por MOD-022.
2. Dado que no existe ningun Aviso de Privacidad en PUBLICADO / VIGENTE, cuando el RAT registra una finalidad nueva, entonces el sistema no genera esta tarea especifica porque ya existe la alerta de Aviso sin publicar de HU-008-12.
3. Dado que este disparador se activa, cuando reviso su configuracion, entonces no encuentro forma de desactivarlo, aunque si puedo cambiar el rol destinatario de la tarea.
4. Dado que la tarea Actualizar Aviso de Privacidad: nueva finalidad detectada se crea, cuando la reviso, entonces el sistema muestra el texto de advertencia de que se detecto un posible cambio de finalidad y que debo evaluar si el Aviso requiere actualizarse, sin decidir por si mismo si el cambio exige republicar.

**Reglas de negocio**

- El disparo no es desactivable.
- El sistema no evalua si el cambio de finalidad es sustancial, solo alerta y crea la tarea.

**Fuera de alcance**

- Decidir si la nueva finalidad ya esta cubierta por el texto vigente del Aviso, que es una decision humana segun la seccion H de la ficha.

- Referencia: MOD-008 seccion G regla 1; seccion H; seccion I

### HU-008-11. Pasar un documento vigente a Requiere revision al vencer su intervalo de revision periodica

**Como** Responsable Legal / Compliance, **quiero** que el sistema marque un documento vigente como Requiere revision cuando se cumple el intervalo de revision configurado, y me avise antes de que llegue la fecha, **para** revisar cada documento con la periodicidad que mi empresa definio, aunque nada mas haya cambiado.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 17 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-008-07
- Modulos requeridos: MOD-023, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que configuro un intervalo de revision periodica para un tipo de documento (por defecto 12 meses si no elijo otro valor), cuando se publica una version, entonces el sistema calcula la fecha de proxima revision con el motor de plazos de MOD-023 a partir de esa fecha y el intervalo.
2. Dado que faltan 30 dias para la fecha de proxima revision de un documento PUBLICADO / VIGENTE, cuando se llega a esa marca, entonces el sistema envia la alerta INFO correspondiente al autor original y a Legal/Compliance, y la repite semanalmente en la ultima semana.
3. Dado que se cumple la fecha de proxima revision de un documento PUBLICADO / VIGENTE, cuando llega esa fecha, entonces el sistema lo pasa a REQUIERE_REVISION, crea la tarea de revision en MOD-021 y envia la alerta WARNING correspondiente por MOD-022.
4. Dado que la fecha de proxima revision se pospone con una justificacion registrada, cuando la reviso, entonces el sistema no pasa el documento a REQUIERE_REVISION hasta la nueva fecha.
5. Dado que un documento pasa a REQUIERE_REVISION y transcurren 15 dias sin que se cree una version nueva en BORRADOR, cuando se cumple ese plazo, entonces el sistema escala la alerta al Administrador.

**Reglas de negocio**

- El intervalo es configurable por tipo de documento, con 12 meses como valor por defecto.
- El plazo lo calcula MOD-023, nunca el propio modulo.
- Escalamiento al Administrador a los 15 dias sin avance.

**Fuera de alcance**

- La creacion de la nueva version en si (HU-008-09).

- Referencia: MOD-008 seccion D, fila Fecha de proxima revision; seccion G regla 5; seccion I

### HU-008-12. Alertar cuando no exista un Aviso de Privacidad publicado pese a tratamientos activos

**Como** Administrador de la organizacion, **quiero** recibir una alerta critica cuando mi empresa ya tenga tratamientos activos registrados pero ningun Aviso de Privacidad publicado, **para** no dejar a mi empresa operando sin el documento que la ley exige tener siempre vigente.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 17 | No |

- Fundamento: OBL-AVISO-01 (Art. 24, Ley para la Proteccion de Datos Personales)
- Depende de: -
- Modulos requeridos: MOD-022, MOD-023

**Criterios de aceptacion**

1. Dado que el Diagnostico o el RAT ya registraron tratamientos activos y no existe ninguna DocumentVersion de tipo Aviso de Privacidad en PUBLICADO / VIGENTE, cuando el sistema evalua esta condicion, entonces envia la alerta CRITICAL Aviso de Privacidad sin publicar al Administrador y al Delegado de Proteccion de Datos por plataforma y correo.
2. Dado que la alerta ya se envio y la condicion sigue sin resolverse, cuando pasa un dia, entonces el sistema la repite diariamente.
3. Dado que transcurren 5 dias habiles sin que exista una version publicada, cuando se cumple ese plazo calculado por MOD-023, entonces el sistema escala la alerta al Aprobador designado.
4. Dado que se publica una version PUBLICADO / VIGENTE de tipo Aviso de Privacidad, cuando esto ocurre, entonces el sistema deja de emitir esta alerta.

**Reglas de negocio**

- La alerta no es desactivable.
- El escalamiento a los 5 dias habiles se calcula con MOD-023.

**Fuera de alcance**

- La creacion y publicacion del Aviso en si (HU-008-02 a HU-008-07).

- Referencia: MOD-008 seccion I, fila Aviso de Privacidad sin publicar

### HU-008-13. Crear una tarea de revision de avisos publicados cuando cambia el regimen de la reforma 659

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** recibir una tarea para revisar los avisos de privacidad publicados cuando el Centro Regulatorio cambia la bandera del regimen de ACTUAL a FUTURO, **para** confirmar si los avisos vigentes siguen mencionando correctamente al Delegado o al Responsable interno, sin que el sistema los reescriba por su cuenta.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 17 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-008-07
- Modulos requeridos: MOD-024, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que existe al menos un Aviso de Privacidad en PUBLICADO / VIGENTE y MOD-024 cambia la bandera regimen_reforma_659 de ACTUAL a FUTURO, cuando el evento llega, entonces el sistema crea la tarea Revisar avisos publicados tras el cambio de regimen en MOD-021 dirigida al Delegado de Proteccion de Datos (o Responsable interno) y envia la alerta WARNING correspondiente por MOD-022.
2. Dado que se crea esta tarea, cuando la reviso, entonces el sistema nunca reescribe ni republica ningun Aviso de Privacidad por si solo.
3. Dado que transcurren 30 dias sin avance sobre la tarea, cuando se cumple ese plazo, entonces el sistema escala la alerta al Administrador.
4. Dado que todos los avisos PUBLICADO / VIGENTE quedan marcados como revisados, con evidencia de confirmacion o de una nueva version publicada, cuando esto ocurre, entonces el sistema deja de emitir esta alerta.
5. Dado que no existe ningun Aviso de Privacidad en PUBLICADO / VIGENTE cuando la bandera cambia, cuando el evento llega, entonces el sistema no crea esta tarea.

**Reglas de negocio**

- El disparo no es desactivable cuando existe un Aviso de Privacidad vigente.
- El sistema nunca republica automaticamente, solo crea la tarea de revision.

**Fuera de alcance**

- Decidir si el aviso sigue siendo valido tras el cambio de regimen, que es una decision humana segun la seccion H de la ficha.
- Republicar el aviso, que sigue el ciclo normal de HU-008-09 a HU-008-07.

- Referencia: MOD-008 seccion G regla 3; seccion H; seccion I, fila Cambio de regimen 659
- Notas: La tabla Q de la ficha clasifica esta automatizacion (regla G-3) como SHOULD HAVE, condicionada a que MOD-024 ya exista. El encargo de esta epica pide incluirla de forma explicita y, dado que MOD-024 se construye en el mismo release R1 que MOD-008 (seccion 19.8 del roadmap), se adelanta a R1 en vez de diferirla; se deja constancia de esta discrepancia con la tabla Q tambien en notas_epica.

### HU-008-14. Adjuntar evidencia de publicacion de un documento

**Como** Responsable Legal / Compliance, **quiero** adjuntar la evidencia de que un documento publicado quedo efectivamente disponible, por ejemplo la referencia de la URL donde se coloco el Aviso, **para** reforzar la prueba de que el documento no solo se aprobo, sino que la empresa lo puso a disposicion de los titulares.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 13 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-008-07
- Modulos requeridos: MOD-019

**Criterios de aceptacion**

1. Dado que un documento esta en PUBLICADO / VIGENTE o en HISTORICO, cuando adjunto una referencia o un archivo como evidencia de publicacion, entonces el sistema la guarda vinculada a esa version junto con la evidencia de publicacion que ya genero automaticamente (fecha, hora, usuario, hash).
2. Dado que adjunto esta evidencia, cuando reviso el historial del documento, entonces encuentro el evento registrado con usuario y fecha.
3. Dado que un usuario con rol Responsable de area, Seguridad/IT, Auditor o Usuario de consulta intenta adjuntar esta evidencia, cuando lo intenta, entonces el sistema deniega la accion.
4. Dado que el documento todavia no alcanzo el estado PUBLICADO / VIGENTE, cuando intento adjuntar evidencia de publicacion, entonces el sistema no ofrece la accion.

**Reglas de negocio**

- La evidencia adjunta complementa, nunca sustituye, la evidencia de publicacion que el sistema genera automaticamente al publicar.

**Fuera de alcance**

- La generacion automatica de la evidencia de publicacion en si (HU-008-07).

- Referencia: MOD-008 seccion C, fila Adjuntar evidencia de publicacion; seccion E

### HU-008-15. Exportar la version vigente de un documento a PDF

**Como** Responsable Legal / Compliance, **quiero** exportar a PDF la version vigente de un documento, o una version historica especifica, **para** entregar el documento fuera del sistema cuando mi empresa lo necesite, por ejemplo para una auditoria.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 14 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-008-07
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que elijo un documento y su version PUBLICADO / VIGENTE, cuando exporto, entonces el sistema genera un PDF con el contenido completo de esa version y registra el evento de exportacion en el historial con usuario, fecha y version exportada.
2. Dado que elijo una version HISTORICO o ARCHIVADO, cuando exporto, entonces el sistema genera el PDF de esa version exacta, sin mezclarla con el contenido de otra version.
3. Dado que un usuario con rol Administrador, Legal/Compliance, Delegado o Auditor exporta un documento, cuando lo hace, entonces el sistema lo permite segun lo que ese rol puede ver.
4. Dado que un usuario con rol Responsable de area o Usuario de consulta intenta exportar, cuando lo intenta, entonces el sistema deniega la accion.
5. Dado que reviso el PDF exportado en el MVP, cuando lo verifico, entonces el sistema no lo presenta como un paquete con integridad verificable porque esta version incluye solo la exportacion simple a PDF.

**Reglas de negocio**

- La exportacion del MVP es un PDF simple, sin el paquete de verificacion de integridad.
- Toda exportacion queda registrada en el historial.

**Fuera de alcance**

- El paquete de exportacion con hash o firma verificable (SHOULD HAVE, ver notas_epica).
- El reporte de inventario y de historial completo (HU-008-16).

- Referencia: MOD-008 seccion C, fila Exportar; seccion E, fila Paquete de exportacion; seccion Q
- Notas: La verificacion de integridad exportable (hash o firma independiente del paquete) es SHOULD HAVE segun la tabla Q y queda fuera de esta HU; el hash de integridad de la propia version ya se calcula al aprobar (HU-008-06). Esta HU solo exporta el contenido a PDF.

### HU-008-16. Consultar el inventario de documentos regulatorios y el historial de versiones

**Como** Auditor (interno), **quiero** consultar la lista de documentos regulatorios con su estado y version vigente, y el historial completo de versiones de cualquiera de ellos, **para** verificar, de forma independiente y sin poder modificar nada, que evidencia documental existe para una auditoria.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 17 | No |

- Fundamento: OBL-AVISO-01 (Art. 24, Ley para la Proteccion de Datos Personales); OBL-DOC-01 (Art. 33 inc. 1, Ley para la Proteccion de Datos Personales)
- Depende de: HU-008-07
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que abro el inventario de documentos regulatorios, cuando lo consulto con filtros de tipo de documento, estado y sucursal, entonces el sistema muestra el nombre, tipo, version vigente, fecha de publicacion, proxima revision y estado de cada uno.
2. Dado que abro el historial de un documento especifico, cuando lo consulto, entonces el sistema muestra todas sus versiones, incluidas HISTORICO y ARCHIVADO, con autores, aprobadores, fechas y el hash de cada una.
3. Dado que consulto este inventario o este historial, cuando reviso mis permisos, entonces el sistema me los muestra en modo de solo lectura, sin opcion de crear, editar, aprobar, publicar ni archivar.
4. Dado que soy Auditor externo invitado con acceso acotado a un periodo o a un tipo de documento, cuando consulto el inventario, entonces el sistema me muestra unicamente lo que mi invitacion autoriza.
5. Dado que un Auditor externo invitado accede a una version especifica, cuando lo hace, entonces el sistema registra ese acceso en el historial, aunque el contenido no sea un dato personal sensible.

**Reglas de negocio**

- El acceso es siempre de solo lectura para Auditor interno y externo.
- El Auditor externo esta acotado a la ventana o alcance de su invitacion.
- Todo acceso de un Auditor externo queda registrado en el historial.

**Fuera de alcance**

- La exportacion a PDF (HU-008-15).

- Referencia: MOD-008 seccion N, filas Inventario de documentos e Historial de versiones; seccion C; seccion O

### HU-008-17. Invitar a un asesor externo a comentar un documento especifico en revision

**Como** Administrador de la organizacion, **quiero** invitar a un asesor externo con acceso temporal acotado a un documento especifico en EN_REVISION, **para** recibir su opinion juridica puntual sobre ese documento sin darle acceso a toda la organizacion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 18 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-008-05
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que un documento esta en EN_REVISION, cuando invito a un asesor externo indicando ese documento, entonces el sistema le da acceso de solo ese documento, en modo de solo lectura mas comentarios.
2. Dado que el asesor externo invitado tiene acceso al documento, cuando escribe un comentario de hasta 1000 caracteres, entonces el sistema lo guarda vinculado a esa version y lo notifica a Legal/Compliance.
3. Dado que el asesor externo invitado intenta editar el contenido, aprobar, rechazar o publicar el documento, cuando lo intenta, entonces el sistema deniega la accion.
4. Dado que el asesor externo invitado accede al documento, cuando lo hace, entonces el sistema registra ese acceso en el historial.
5. Dado que reviso el acceso concedido y ya no lo necesito, cuando lo revoco, entonces el sistema deja de mostrarle el documento de inmediato.

**Reglas de negocio**

- El acceso queda acotado a un unico documento y a su estado de revision.
- El acceso es de solo lectura mas comentarios, nunca de edicion ni aprobacion.
- El acceso es revocable en cualquier momento.

**Fuera de alcance**

- Dar acceso del asesor externo a mas de un documento o a toda la organizacion.

- Referencia: MOD-008 seccion B, fila Asesor externo invitado; seccion C

### HU-008-18. Proveer la plantilla generica de Evaluacion de Impacto (EIPD) en el catalogo de documentos

**Como** Equipo de contenido del producto (proveedor), **quiero** cargar y mantener, dentro del tipo de documento Otro documento regulatorio, una plantilla generica de Evaluacion de Impacto en la Privacidad (EIPD), **para** que exista un documento donde completar manualmente la evaluacion cuando el Diagnostico (MOD-004) cree la tarea de elaborarla, mientras el modulo de Riesgos y EIPD (MOD-014) no este disponible.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 13 | Si |

- Fundamento: OBL-DOC-03 (Art. 4 (Medidas Organizativas, lit. e), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: HU-008-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que reviso el catalogo de tipos de documento, cuando busco entre las plantillas disponibles de Otro documento regulatorio, entonces encuentro la plantilla Evaluacion de Impacto en la Privacidad (EIPD), version generica, con las secciones minimas de descripcion del tratamiento, riesgos identificados, medidas de mitigacion y conclusion.
2. Dado que un Responsable Legal / Compliance crea un documento a partir de esta plantilla, cuando lo hace, entonces el documento sigue exactamente el mismo ciclo BORRADOR, EN_REVISION, APROBADO, PUBLICADO / VIGENTE que cualquier otro documento del modulo.
3. Dado que esta plantilla se actualiza, cuando se publica una nueva version de la plantilla, entonces los documentos EIPD ya creados a partir de la version anterior no se modifican de forma retroactiva.
4. Dado que el modulo de Riesgos y EIPD (MOD-014) no esta activo en el MVP, cuando se completa esta EIPD generica, entonces el sistema no calcula ningun nivel de riesgo automatico, solo aloja el texto que la persona responsable redacto.

**Reglas de negocio**

- La plantilla generica no sustituye el motor de scoring de MOD-014 cuando ese modulo exista.
- Los documentos EIPD ya creados conservan la version de plantilla con la que se crearon.

**Fuera de alcance**

- La creacion de la tarea elaborar EIPD en si, que crea MOD-004.
- El motor de scoring de riesgo de MOD-014.

- Requiere contenido: Plantilla generica de EIPD validada por abogado, con las secciones minimas de descripcion del tratamiento, riesgos identificados, medidas de mitigacion y conclusion
- Requiere validacion legal: Si
- Referencia: 04_secciones/19_21_roadmap_mvp_v1_v2.md seccion 19.4, fila MOD-014; MOD-008_ficha.md seccion D, fila Tipo de documento (catalogo extensible)
- Notas: Mecanismo de cobertura parcial de la seccion 19.4: cubre parcialmente a MOD-014 (Riesgos y EIPD, SHOULD HAVE) mientras ese modulo no exista. La tarea que consume esta plantilla la crea MOD-004, fuera de esta epica.

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Gestor de Politica de Proteccion de Datos (plantilla, versionado, aprobacion) | HU-008-01, HU-008-02, HU-008-05, HU-008-06, HU-008-07, HU-008-08, HU-008-09 |
| Gestor de Politica de Privacidad | HU-008-01, HU-008-02, HU-008-04, HU-008-05, HU-008-06, HU-008-07, HU-008-08, HU-008-09 |
| Gestor de Aviso de Privacidad con checklist de 9 literales (Art. 24) y 5 elementos (Art. 7) | HU-008-01, HU-008-02, HU-008-03, HU-008-04, HU-008-05, HU-008-06, HU-008-07, HU-008-08, HU-008-09, HU-008-10, HU-008-11, HU-008-12 |
| Flujo de aprobacion configurable por tipo de documento | HU-008-01, HU-008-05, HU-008-06 |
| Versionado con historial inmutable y regla simple de no-borrado antes de 10 anios | HU-008-02, HU-008-07, HU-008-08, HU-008-09, HU-008-16 |
| Motor documental generico reutilizable por referencia (usado por MOD-009 para Contrato/DPA) | HU-008-01, HU-008-02, HU-008-05, HU-008-06, HU-008-07, HU-008-08, HU-008-09, HU-008-14, HU-008-15 |
