# MODULO: Documentos y Politicas

Codigo corto del modulo: MOD-008
Clasificacion global del modulo: MUST HAVE (para el MVP)
Obligaciones que cubre:
- Propietarias (6): OBL-AVISO-01, OBL-AVISO-02, OBL-AVISO-03, OBL-AVISO-04, OBL-AVISO-05, OBL-DOC-01
- Colaboradoras, es decir obligaciones propiedad de otro modulo que MOD-008 ayuda a probar o a ejecutar (9): OBL-DPO-06 (propietario MOD-002), OBL-PROV-04 y OBL-PROV-06 (propietario MOD-009), OBL-RET-01, OBL-RET-02, OBL-RET-03, OBL-RET-04 y OBL-RET-06 (propietario MOD-016), OBL-SENS-08 (propietario MOD-006)

Fuente: `02_validacion/mapa_modulos.json` y `02_validacion/06_mapa_definitivo_de_modulos.md`, seccion "MOD-008 Documentos y Politicas". Todas las obligaciones se citan con el ID canonico de `01_legal/matriz_obligaciones.json` (105 obligaciones); no se usa la numeracion alternativa de `01_legal/03_hallazgos_regulatorios.md`, que emplea prefijos distintos (OBL-CONSENT, OBL-ENC) para los mismos hechos juridicos.

---

## A. Proposito

**Por que existe.** Toda empresa que trata datos personales en El Salvador necesita, como minimo, tres documentos regulatorios (Politica de Proteccion de Datos, Politica de Privacidad y Aviso de Privacidad) redactados de forma consistente entre si, mantenidos al dia y con evidencia de cuando se aprobaron y publicaron. Sin un lugar unico para producir, versionar y aprobar esos documentos, cada area de la empresa termina con su propia copia desactualizada en una carpeta compartida, sin control de version ni prueba de que el titular vio exactamente ese texto en un momento dado. MOD-008 es ese lugar unico.

**Que problema resuelve para la empresa.** Una persona sin formacion juridica (el usuario objetivo del producto, ver `02_validacion/04_objetivo_exacto_del_producto.md`) no sabe redactar un aviso de privacidad desde cero, no sabe que el aviso debe contener exactamente nueve elementos, y no tiene forma de probar despues que la version que un titular vio en marzo es distinta de la que se publico en octubre. MOD-008 responde con plantillas guiadas, una lista de verificacion del contenido minimo legal, un flujo de aprobacion configurable y un historial de versiones que nunca se sobrescribe.

**Que obligacion u obligaciones cubre (propietario, con articulo).**
- OBL-AVISO-01, contenido minimo del aviso de privacidad, Art. 24 inc. 1 LPDP. OBLIGATORIO.
- OBL-AVISO-02, datos de contacto del encargado subcontratado en el aviso, Art. 24 lit. h) LPDP. CONDICIONAL (solo si la empresa subcontrata un encargado).
- OBL-AVISO-03, informar el uso de cookies, Art. 24 lit. i) LPDP. CONDICIONAL (solo si la empresa usa sitios o apps con cookies).
- OBL-AVISO-04, derecho de informacion en la recoleccion, Art. 7 LPDP. OBLIGATORIO.
- OBL-AVISO-05, elaboracion de la politica de privacidad, Art. 24 inc. 1 LPDP y Politicas ACE Art. 4 lit. a. OBLIGATORIO.
- OBL-DOC-01, establecer y documentar los procedimientos ARCO-POL, Art. 33 inc. 1 LPDP. OBLIGATORIO (el procedimiento como documento vive en MOD-008; su ejecucion operativa es propiedad de MOD-011 ARCO-POL, que es colaborador de esta obligacion segun la tabla de cobertura del mapa definitivo).

**Que valor aporta.**
- Operativo: un unico lugar donde redactar, aprobar y publicar los documentos regulatorios, reutilizado por referencia desde otros modulos (por ejemplo, MOD-009 Proveedores usa el mismo motor documental para el tipo de documento Contrato/DPA).
- Probatorio: cada version publicada queda fechada, con quien la aprobo y con un hash de integridad, de modo que si un titular reclama "no se me informo correctamente", la empresa puede mostrar exactamente que aviso estaba vigente ese dia.
- De reduccion de riesgo: el checklist de los nueve literales del Art. 24 impide publicar un aviso incompleto por descuido, que es la infraccion mas facil de cometer por simple omision.

**Que NO hace este modulo (limites explicitos).**
- No decide si el contenido redactado es juridicamente suficiente; solo valida que las secciones minimas exigidas por la ley esten presentes en la estructura del documento (ver seccion H).
- No es el modulo que ejecuta el tramite operativo de ARCO-POL (eso es MOD-011); solo aloja y versiona el documento "Procedimiento ARCO-POL" que MOD-011 sigue.
- No es el modulo que registra el consentimiento del titular ni decide si una base juridica es valida (eso es MOD-007); solo produce y versiona el Aviso de Privacidad que MOD-007 referencia por version exacta, nunca por copia (decision 2.7.6 de `02_validacion/02_validacion_de_la_idea.md`).
- No almacena la base de datos de clientes de la empresa ni datos personales reales de titulares dentro de una plantilla; las plantillas usan variables (`{{razon_social}}`, `{{finalidad}}`), nunca datos reales precargados (antifeature 8 de `02_validacion/22_anti_features.md`).
- No calcula plazos habiles por su cuenta; cuando un documento tiene fecha de revision programada, consulta el calendario de MOD-023 (principio de organizacion 5 del mapa definitivo).
- No define ni aplica las reglas de cuanto tiempo se conserva cada categoria de dato del titular (eso es MOD-016 Retencion); solo aplica, sobre sus propios documentos, la regla fija de conservacion documental de 10 anios (OBL-RET-04, OBL-RET-04 propietario MOD-016, MOD-008 colaborador) descrita en la seccion J.

---

## B. Usuarios

Roles estandar de `02_validacion/05_tipos_de_usuario.md`, seccion 5.3, y para que usa cada uno este modulo:

| Rol | Para que usa MOD-008 |
|---|---|
| Administrador de la organizacion | Configura el catalogo de tipos de documento, la cadena de aprobacion por tipo, y publica documentos cuando la configuracion se lo permite |
| Delegado de Proteccion de Datos (o Responsable interno, segun el estado de la reforma 659) | Revisa y aprueba la Politica de Privacidad y el Aviso de Privacidad; recibe las tareas de revision cuando el RAT o Proveedores detectan un cambio que afecta al aviso; aprueba la revision de avisos tras un cambio de regimen |
| Responsable ARCO-POL / Responsable del tramite | Consulta y usa el documento "Procedimiento ARCO-POL" como guia operativa dentro de MOD-011; no suele redactar documentos en MOD-008, solo los consulta |
| Responsable Legal / Compliance | Redacta y edita el contenido de los documentos regulatorios; completa el checklist de contenido minimo del Aviso; suele ser aprobador en la cadena configurada |
| Responsable de Seguridad / IT | Aporta el contenido de las medidas de seguridad que el Aviso de Privacidad debe mencionar (Art. 7, OBL-AVISO-04, OBL-AVISO-05); no suele tener permiso de aprobacion en este modulo |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Solicita al Administrador o al Legal la creacion de una plantilla interna cuando su area la necesita; aporta informacion puntual (por ejemplo, uso de cookies en el sitio de Marketing) pero no suele redactar documentos regulatorios |
| Aprobador | Aprueba o rechaza una version en revision segun la cadena configurada para ese tipo de documento; puede coincidir con el Delegado/Responsable interno o el Legal segun el tamano de la empresa |
| Auditor (interno) | Consulta y exporta el historial de versiones y las aprobaciones como evidencia; nunca crea, edita, aprueba ni publica documentos |
| Auditor externo (invitado) | Igual que el Auditor interno, con acceso temporal acotado a un periodo o a un tipo de documento durante una auditoria puntual |
| Usuario de consulta / Colaborador | Consulta documentos publicados que le fueron asignados como tarea de lectura (por ejemplo, confirmar que leyo la Politica de Proteccion de Datos interna) |
| Titular (formulario externo) | No usa MOD-008 directamente; consume el Aviso de Privacidad publicado a traves del sitio de la empresa o, cuando exista, del Portal del Titular (MOD-012) |
| Asesor externo invitado | Acceso temporal para revisar o comentar un documento especifico en estado En revision, por ejemplo un abogado externo contratado puntualmente para validar el Aviso |

---

## C. Permisos

Acciones evaluadas: ver, crear (nuevo documento o nueva version), editar borrador, enviar a revision, aprobar/rechazar, publicar, archivar, exportar, asignar (tarea de revision), comentar, adjuntar evidencia (por ejemplo, captura de la publicacion en el sitio web).

| Accion | Administrador | Delegado / Resp. interno | Legal / Compliance | Seguridad / IT | Resp. de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Asesor externo invitado |
|---|---|---|---|---|---|---|---|---|---|---|
| Ver documentos publicados | Si | Si | Si | Si | Si | Si | Si | Si (acotado) | Si (los asignados) | Si (el asignado) |
| Ver borradores e historial completo | Si | Si | Si | Solo lo que le compete | No | Si (los que revisa) | Si (solo lectura) | Si (acotado, solo lectura) | No | Solo el documento asignado |
| Crear documento / nueva version | Si | Si | Si | No | No (solicita) | No | No | No | No | No |
| Editar borrador | Si | Si | Si | No | No | No | No | No | No | No (solo comenta) |
| Enviar a revision | Si | Si | Si | No | No | No | No | No | No | No |
| Aprobar / rechazar | Segun cadena | Segun cadena | Segun cadena | No | No | Si | No | No | No | No |
| Publicar | Si | Si (si la cadena lo habilita) | No, salvo que la cadena lo asigne | No | No | No | No | No | No | No |
| Archivar documento | Si | Si (con doble aprobacion si es Aviso o Politica de Privacidad) | No | No | No | No | No | No | No | No |
| Exportar (paquete con hash) | Si | Si | Si | No | No | No | Si | Si (acotado) | No | No |
| Asignar tarea de revision | Si | Si | Si | No | No | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | Si | Si | No | No | No | Si |
| Adjuntar evidencia de publicacion | Si | Si | Si | No | No | No | No | No | No | No |

**Separacion de funciones.**
- Quien redacta o edita el borrador de un Aviso de Privacidad o de una Politica de Privacidad no debe ser la unica persona que lo aprueba; para estos dos tipos de documento la cadena de aprobacion exige como minimo un aprobador distinto del autor, salvo en pyme por debajo del umbral configurable (propuesta inicial 50 empleados, ver `02_validacion/05_tipos_de_usuario.md` seccion 5.4), donde se permite con advertencia visible de autorrevision.
- El rol Auditor (interno o externo) es siempre de solo lectura sobre este modulo: nunca puede crear, editar, aprobar, publicar ni archivar un documento, para que su verificacion posterior sea independiente.
- Archivar un Aviso de Privacidad o una Politica de Privacidad exige doble aprobacion (quien lo solicita y una segunda persona con rol Delegado/Responsable interno o Administrador), porque descontinuar estos dos tipos de documento sin sustituirlos deja a la empresa sin el documento que la ley exige tener siempre vigente.

---

## D. Informacion de entrada

Convenciones: "OBL-ID" es fundamento legal; "buena practica" es una decision de producto sin mandato legal expreso, marcada segun `02_validacion/22_anti_features.md` y `02_validacion/02_validacion_de_la_idea.md` seccion 2.7.

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Tipo de documento | Seleccion unica | Obligatorio desde la creacion | Catalogo fijo: Politica de Proteccion de Datos, Politica de Privacidad, Aviso de Privacidad, Procedimiento ARCO-POL; catalogo extensible por el Administrador: Plantilla interna, Otro documento regulatorio | No editable despues de creado el documento (crear uno nuevo si se necesita cambiar de tipo) | "Elija que clase de documento va a crear. Si no esta seguro, use el Centro de Ayuda de este modulo (MOD-026) para ver un ejemplo de cada uno." | Politica de Proteccion de Datos y Politica de Privacidad: OBL-AVISO-05, Art. 24 inc. 1. Aviso de Privacidad: OBL-AVISO-01, Art. 24. Procedimiento ARCO-POL: OBL-DOC-01, Art. 33 inc. 1 |
| Nombre del documento | Texto | Obligatorio | - | Entre 3 y 120 caracteres; unico dentro del mismo tipo mientras este vigente | "Un nombre corto que identifique este documento, por ejemplo 'Aviso de Privacidad - Clientes'." | Buena practica |
| Sucursal o unidad aplicable | Referencia a MOD-001 (BusinessUnit) | Opcional; obligatorio solo si la empresa tiene mas de una razon social o linea de negocio con avisos distintos | Catalogo de MOD-001 | Debe existir en MOD-001 | "Si este documento aplica solo a una sucursal o linea de negocio especifica, indiquelo aqui. Si aplica a toda la empresa, dejelo en blanco." | Buena practica |
| Descripcion / proposito | Texto largo | Opcional | - | Maximo 500 caracteres | "Una o dos frases que expliquen para que sirve este documento internamente." | Buena practica |
| Contenido del documento | Texto largo con formato (plantilla) | Obligatorio para pasar a Enviar a revision | Plantilla precargada segun el tipo de documento | No puede quedar vacio; para Aviso de Privacidad, el checklist del campo siguiente debe estar completo | "Redacte el contenido usando la plantilla como base. Las palabras entre llaves, por ejemplo {{razon_social}}, se completan solas con los datos de su empresa." | OBL-AVISO-01, OBL-AVISO-05, OBL-DOC-01 |
| Checklist de contenido minimo Art. 24 (solo Aviso de Privacidad) | Lista de 9 casillas booleanas, una por literal a) a i) del Art. 24 | Obligatorio completarlo antes de Enviar a revision, si el tipo es Aviso de Privacidad | Literales a) identidad y contacto del responsable, b) finalidades, c) destinatarios, d) derechos ARCO-POL y como ejercerlos, e) caracter obligatorio u opcional de los datos, f) consecuencias de no proporcionarlos, g) transferencias previstas, h) datos de contacto del encargado subcontratado (si existe), i) uso de cookies (si aplica) | El sistema no permite marcar b, c, d, e o f como "no aplica"; h e i pueden marcarse "no aplica" solo si no existe encargado o no se usan cookies, respectivamente, con un campo de justificacion breve obligatorio en ese caso | "Verifique que su aviso mencione cada uno de estos nueve puntos que exige la ley. Si alguno no aplica a su caso, explique brevemente por que." | OBL-AVISO-02 (literal h), OBL-AVISO-03 (literal i), OBL-AVISO-01 (conjunto de los nueve literales) |
| Cinco elementos del Art. 7 (Politica de Privacidad y Aviso de Privacidad) | Lista de 5 casillas booleanas | Obligatorio completarlo antes de Enviar a revision | Proposito y destinatarios; existencia de la base de datos, respaldos y sitios de contingencia; identidad y contacto de responsable y encargado; contenido de los derechos ARCO-POL y mecanismos para ejercerlos; medidas de seguridad activas | No puede quedar ninguna casilla sin marcar | "Estos cinco puntos son independientes de los nueve del Aviso; verifiquelos por separado." | OBL-AVISO-04, Art. 7 |
| Encargados mencionados | Referencia multiple a MOD-009 (Encargado) | Condicional: obligatorio si el checklist marca el literal h) como aplicable | Lista de encargados registrados en MOD-009 | Debe existir al menos un encargado seleccionado si el literal h) esta marcado como aplicable | "Seleccione los proveedores que tratan datos por cuenta de su empresa y que deben mencionarse en el aviso." | OBL-AVISO-02, OBL-PROV-04 |
| Variables precargadas | Lista de solo lectura | Se muestra automaticamente, no se captura | Razon social y datos de contacto (MOD-001), nombre y contacto del Delegado/Responsable interno vigente (MOD-002) | No editable directamente; se actualiza si cambia el dato de origen, pero solo al crear una version nueva, nunca sobre una version ya publicada | "Estos datos se completan solos a partir de la informacion de su organizacion. Si estan mal, corrijalos en Organizacion (MOD-001) o en Delegado (MOD-002), no aqui." | Buena practica, evita duplicar datos ya capturados en otro modulo |
| Motivo de la nueva version | Texto | Obligatorio al crear una version distinta de la primera | - | Maximo 300 caracteres | "Explique brevemente que cambio respecto de la version anterior, por ejemplo 'se agrego un nuevo proveedor de nube'." | Buena practica, apoya la trazabilidad exigida por OBL-PRIN-03 (colaboradora de MOD-019) |
| Fecha de vigencia | Fecha | Obligatorio al aprobar, antes de publicar | - | No puede ser anterior a la fecha de aprobacion | "Desde que fecha este documento sera el vigente. Normalmente es la fecha de hoy." | Buena practica |
| Fecha de proxima revision | Fecha | Opcional; si se deja en blanco, el sistema propone un intervalo por defecto configurable (por ejemplo 12 meses) | - | Debe ser posterior a la fecha de vigencia | "Cuando quiere que el sistema le recuerde revisar este documento, aunque nada haya cambiado antes." | Buena practica |
| Cadena de aprobacion aplicable | Referencia (configuracion por tipo de documento) | Se precarga desde la configuracion del Administrador; editable por el Administrador para un documento especifico si hay una razon documentada | Roles disponibles en MOD-001 | Debe incluir al menos un rol distinto del autor para Aviso de Privacidad y Politica de Privacidad | "Quienes deben aprobar este documento antes de publicarse. Se define una vez por tipo de documento y se aplica a todas sus versiones." | Decision de producto 2.7.14 de `02_validacion/02_validacion_de_la_idea.md` |
| Archivo adjunto (opcional) | Archivo | Opcional | PDF, DOCX | Maximo 10 MB | "Si ya tiene un documento firmado fuera del sistema, adjuntelo aqui como respaldo." | Buena practica |
| Comentarios de revision | Texto largo | Opcional, obligatorio al rechazar | - | Maximo 1000 caracteres | "Explique que debe corregirse antes de volver a enviarlo a revision." | Buena practica |

**Campos que contienen o podrian contener datos personales, y como se minimizan.** El contenido de los documentos de este modulo es, por diseno, texto institucional (politicas, avisos, procedimientos) dirigido a describir practicas de tratamiento, no a almacenar datos de titulares concretos. El unico dato personal que aparece de forma estructurada es el del Delegado o Responsable interno vigente (nombre y contacto de una persona designada por la empresa, precargado desde MOD-002 por referencia, nunca copiado a mano) y el de los usuarios internos que redactan y aprueban (metadato de autoria, ya minimo por naturaleza). El archivo adjunto opcional es el unico punto donde un usuario podria, por error, subir un documento que contenga datos de un tercero; el sistema no impide tecnicamente ese adjunto, pero el texto de ayuda advierte que el adjunto es solo para el documento institucional firmado, no para expedientes de titulares, y las plantillas nunca precargan datos reales de clientes o empleados, solo variables.

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| DocumentVersion (registro de version) | Contenido completo del documento en ese momento, autor, fecha, estado, hash de integridad una vez aprobada | Registro interno + exportable a PDF | Al crear o editar un borrador (version en curso) y al aprobar (se congela el contenido y se calcula el hash) | Consultable por todos los roles con permiso de ver (seccion C) |
| Tarea de revision o aprobacion | Nombre del documento, tipo de tarea (redactar, revisar, aprobar), fecha limite sugerida | Tarea en MOD-021 | Al enviar a revision, al pasar a Requiere revision, o al detectar un disparador automatico (seccion G) | Rol asignado segun la cadena de aprobacion o la regla del disparador |
| Alerta | Ver tabla completa en la seccion I | Notificacion en MOD-022 | Segun cada disparador de la seccion I | Rol destinatario de cada alerta |
| Borrador de documento generado desde plantilla | Contenido precargado con variables resueltas (razon social, contacto del Delegado/Responsable interno) y estructura minima por tipo de documento | Documento en estado Borrador, marcado "generado automaticamente, pendiente de revision" | Al crear un documento nuevo de un tipo del catalogo fijo | Autor que crea el documento |
| Evidencia de publicacion | Version publicada, fecha y hora, usuario que publico, hash | Entrada en MOD-019 (Centro de Evidencias) | Al publicar una version | Consultable por Auditor, Administrador, Delegado/Responsable interno |
| Evento de auditoria | Accion realizada, usuario, fecha y hora, documento y version afectados | Entrada en el AuditLog transversal | En cada transicion de estado de la seccion F | Consultable por Auditor y Administrador |
| Paquete de exportacion con integridad verificable | PDF de la version vigente (o de un rango de versiones historicas) mas archivo de verificacion de hash | ZIP o PDF firmado | Bajo demanda, al usar la accion Exportar | Quien exporta; tipicamente Auditor o Administrador, para una auditoria (MOD-018) o para un requerimiento de la ACE |
| Indicador de estado de documentos regulatorios | Cuenta de documentos vigentes, en revision, requieren revision, sin publicar, por tipo | Indicador en el dashboard (MOD-020) | Se recalcula cada vez que cambia el estado de un documento | Vistas por rol, ver seccion M |

---

## F. Workflow

### Diagrama de estados

```
                    crear documento
                          |
                          v
                     +----------+
                     | BORRADOR |<---------------------------+
                     +----------+                             |
                          |                                    | rechazar
                          | enviar a revision                  | (con motivo)
                          v                                    |
                    +-------------+                            |
                    | EN_REVISION |--------------------------->+
                    +-------------+
                          |
                          | aprueban todos los roles
                          | de la cadena configurada
                          v
                    +----------+
                    | APROBADO |
                    +----------+
                          |
                          | publicar
                          v
              +----------------------+     se publica una version nueva    +-----------+
              | PUBLICADO / VIGENTE  |------------------------------------>| HISTORICO |
              +----------------------+     (esta version queda reemplazada) +-----------+
                    |        ^
                    |        | se publica la nueva version
     llega fecha de |        | (repite el ciclo desde BORRADOR,
     revision, o    |        |  ver paso "iniciar nueva version")
     RAT/Proveedores|        |
     detectan cambio,|       |
     o cambia el     v       |
     regimen 659  +--------------------+
                   | REQUIERE_REVISION  |
                   +--------------------+
                          |
                          | iniciar nueva version
                          | (la version actual sigue
                          |  PUBLICADO/VIGENTE mientras tanto)
                          v
                     +----------+
                     | BORRADOR | (nueva version del mismo documento)
                     +----------+

              +----------------------+   documento descontinuado,   +-----------+
              | PUBLICADO / VIGENTE  |-- justificado y con doble --> | ARCHIVADO |
              +----------------------+   aprobacion si es Aviso     +-----------+
                                          o Politica de Privacidad
```

Estados terminales: HISTORICO y ARCHIVADO. Ninguno de los dos se elimina ni se reabre: ambos se conservan como registro de solo lectura durante el plazo de conservacion documental aplicable (minimo 10 anios, OBL-RET-04 y OBL-RET-06, colaboradoras propiedad de MOD-016). Para volver a tener un documento vigente de un tipo Archivado, se crea un documento nuevo, no se reabre el archivado.

### Tabla de transiciones

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (ninguno) | Crear documento | Tipo de documento seleccionado; nombre unico dentro del tipo mientras este vigente | BORRADOR | Administrador, Delegado/Responsable interno, Legal/Compliance | Crea la primera DocumentVersion; precarga plantilla y variables (seccion E); evento de auditoria "documento creado" |
| BORRADOR | Editar contenido | El documento no esta publicado | BORRADOR | Autor original, Legal/Compliance, Administrador | Actualiza el contenido de la version en curso; no crea una version formal nueva; evento de auditoria "contenido modificado" |
| BORRADOR | Enviar a revision | Contenido no vacio; si el tipo es Aviso de Privacidad, checklist Art. 24 y checklist Art. 7 completos (seccion D) | EN_REVISION | Autor con permiso de crear/editar | Crea tarea de revision en MOD-021 para cada rol de la cadena de aprobacion configurada; alerta a los revisores (MOD-022); evento de auditoria |
| EN_REVISION | Rechazar | Comentario de revision obligatorio | BORRADOR | Cualquier rol de la cadena de aprobacion | Notifica al autor con el motivo (MOD-022); evento de auditoria con el comentario |
| EN_REVISION | Aprobar | Todos los roles de la cadena configurada han aprobado; checklist de contenido minimo verificado | APROBADO | Rol(es) de la cadena de aprobacion | Congela el contenido de la version; calcula el hash de integridad; registra identidad y fecha de cada aprobacion como evidencia (MOD-019); evento de auditoria |
| APROBADO | Publicar | Fecha de vigencia definida | PUBLICADO / VIGENTE | Administrador, o el rol que la cadena configurada habilite para publicar | Si existia una version anterior PUBLICADO/VIGENTE del mismo documento, esa version pasa automaticamente a HISTORICO; genera evidencia de publicacion (fecha, hora, usuario, hash) en MOD-019; actualiza el indicador del dashboard (MOD-020); si el tipo es Aviso de Privacidad, notifica a MOD-007 (Consentimiento) de que existe una nueva version de referencia disponible para nuevas capturas de consentimiento |
| PUBLICADO / VIGENTE | Disparador automatico de revision (fecha programada, cambio detectado en RAT o Proveedores, o cambio de regimen 659; ver seccion G) | Ninguna condicion manual; la regla dispara sola | REQUIERE_REVISION | El sistema (regla automatica, seccion G) | Crea tarea en MOD-021 para el rol responsable; alerta (MOD-022); el documento sigue siendo el vigente mientras se redacta la nueva version |
| REQUIERE_REVISION | Iniciar nueva version | Documento aun vigente mientras se redacta la nueva version | BORRADOR (nueva version) | Legal/Compliance, Delegado/Responsable interno, Administrador | La version actual permanece PUBLICADO/VIGENTE hasta que la version nueva complete el ciclo hasta Publicar |
| PUBLICADO / VIGENTE | Archivar (documento descontinuado) | Justificacion obligatoria; para Aviso de Privacidad o Politica de Privacidad, exige doble aprobacion (quien solicita y un segundo rol Delegado/Responsable interno o Administrador) | ARCHIVADO | Administrador (con la doble aprobacion cuando aplica) | El documento deja de mostrarse como vigente; se conserva integro; evento de auditoria con la justificacion |
| HISTORICO / ARCHIVADO | (ninguna transicion manual disponible) | - | Permanece, sin cambios | N/A, solo lectura | Se conserva minimo 10 anios (OBL-RET-04) o el plazo mayor que resulte aplicable segun OBL-RET-01, OBL-RET-02 o OBL-RET-03 si el contenido tambien tiene relevancia mercantil, tributaria o de prevencion de lavado de dinero; consultable y exportable por Auditor |

**Reapertura.** No existe una accion de "reabrir" un documento HISTORICO o ARCHIVADO. Si se necesita retomar el contenido de un tipo de documento archivado, se crea un documento nuevo del mismo tipo, partiendo de la ultima version disponible como referencia de lectura.

**Registros vinculados.** Cuando una version de un documento pasa a HISTORICO, cualquier otro modulo que la haya referenciado en el pasado (por ejemplo, un registro de consentimiento en MOD-007 que muestra que Aviso de Privacidad vio el titular) sigue apuntando a esa version historica exacta, nunca se actualiza para apuntar a la version vigente actual. Esto es intencional: es la unica forma de que la carga de la prueba del Art. 54 (OBL-CONS-05, propiedad de MOD-007) se pueda sostener despues de que el aviso cambie.

---

## G. Automatizaciones

| # | Disparador | Condicion | Accion | Configurable por la empresa |
|---|---|---|---|---|
| 1 | MOD-006 (RAT) registra una finalidad de tratamiento nueva sobre datos ya recolectados | El Aviso de Privacidad vigente no menciona esa finalidad | Crea tarea "Actualizar Aviso de Privacidad: nueva finalidad detectada" en MOD-021; pasa el documento a REQUIERE_REVISION | El disparo en si no es desactivable (OBL-AVISO-04, Art. 7); el destinatario de la tarea si es configurable |
| 2 | MOD-009 (Proveedores) registra o modifica un Encargado del tratamiento | El Aviso de Privacidad publicado no lista ese encargado en el checklist del literal h) | Crea tarea de revision del aviso; pasa el documento a REQUIERE_REVISION | El disparo no es desactivable (OBL-AVISO-02, OBL-PROV-04); el destinatario si es configurable |
| 3 | MOD-024 (Centro Regulatorio) cambia la bandera `regimen_reforma_659` de ACTUAL a FUTURO | Existe al menos un Aviso de Privacidad en estado PUBLICADO/VIGENTE | Crea tarea "Revisar avisos publicados tras el cambio de regimen" en MOD-021, dirigida al Delegado/Responsable interno; el sistema nunca reescribe ni republica el documento por si solo | No desactivable (decision 2.7 del mapa definitivo, seccion 5, punto 5) |
| 4 | Se completa la aprobacion de una version (todos los roles de la cadena aprobaron) | Checklist de contenido minimo verificado | Calcula el hash de integridad del contenido final; registra la evidencia de aprobacion en MOD-019; habilita la accion Publicar | No desactivable |
| 5 | Transcurre el intervalo de revision periodica configurado desde la ultima publicacion | El documento esta en PUBLICADO/VIGENTE | Pasa a REQUIERE_REVISION; crea tarea y alerta | El intervalo (por ejemplo 12 meses) es configurable por tipo de documento; el disparo en si no se puede desactivar por completo para Aviso de Privacidad y Politica de Privacidad |
| 6 | Se crea un documento de tipo Aviso de Privacidad o Politica de Privacidad | Ninguna | Precarga la plantilla con el checklist correspondiente (Art. 24 o Art. 7) y las variables de MOD-001 y MOD-002 | No aplica (parte de la creacion) |
| 7 | Se publica una nueva version de un documento que ya tenia una version PUBLICADO/VIGENTE | Publicacion exitosa | La version anterior pasa automaticamente a HISTORICO; nunca se elimina | No desactivable |

---

## H. Decisiones que NO debe automatizar

- **Suficiencia juridica del contenido.** El sistema no decide si el texto redactado en un Aviso o una Politica de Privacidad es legalmente adecuado mas alla de que el checklist estructural (presencia de los literales del Art. 24 y de los cinco elementos del Art. 7) este completo. El checklist verifica presencia, nunca calidad juridica del texto. Texto mostrado: "Este documento incluye las secciones minimas exigidas por la ley. Su contenido especifico requiere validacion de la organizacion o asesoria especializada." Por que: la ley exige contenido minimo, no un formato certificado; solo una persona con criterio legal puede evaluar si la redaccion concreta protege a la empresa frente a un caso especifico.
- **Publicacion sin accion humana.** El sistema nunca aprueba ni publica un documento por si solo, aunque el borrador haya sido generado automaticamente a partir de una plantilla y de datos del RAT. Publicar exige siempre una accion explicita de una persona con el rol habilitado. Por que: cierra la brecha entre el compromiso de no actuar como Delegado del cliente (antifeature 4) y la automatizacion del contenido (decision 2.7.22 de `02_validacion/02_validacion_de_la_idea.md`).
- **Si un cambio de finalidad es "sustancial".** Cuando el RAT declara una finalidad nueva, el sistema no decide si ese cambio exige republicar el aviso o si basta con una nota interna; solo alerta y crea la tarea, dejando la decision a la persona responsable. Texto mostrado: "Se detecto un posible cambio de finalidad en el Registro de Actividades de Tratamiento. Evalue si el Aviso de Privacidad requiere actualizarse. Requiere validacion de la organizacion o asesoria especializada."
- **Validez del Aviso tras un cambio de regimen de la reforma 659.** El sistema no determina si el Aviso de Privacidad vigente sigue siendo valido despues de que la bandera de MOD-024 pase a FUTURO; solo crea la tarea de revision (ver seccion G, regla 3) y deja la decision, y la eventual republicacion, a la organizacion.
- **Valor probatorio de una version historica en un caso ya cerrado.** El sistema no decide si una version historica especifica sigue siendo defendible como prueba (por ejemplo, frente a un consentimiento capturado bajo un aviso anterior); solo conserva y referencia la version exacta usada en su momento, dejando la valoracion probatoria a la organizacion o a su asesoria legal.

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia o repeticion | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Aviso de Privacidad sin publicar | No existe ninguna version PUBLICADO/VIGENTE de tipo Aviso de Privacidad, pese a que el diagnostico (MOD-004) o el RAT (MOD-006) ya registraron tratamientos activos | CRITICAL | Administrador, Delegado/Responsable interno | Plataforma + correo | Diaria hasta resolverse | Escala al Aprobador designado tras 5 dias habiles sin avance | Existe una version PUBLICADO/VIGENTE de Aviso de Privacidad |
| Documento pendiente de aprobacion | Una version lleva mas de N dias habiles (configurable, por defecto 5) en EN_REVISION | WARNING | Rol(es) aprobador(es) asignados | Plataforma + correo | Al vencer el plazo, luego cada 2 dias habiles | Escala al Administrador tras 10 dias habiles sin avance | Se aprueba o se rechaza la version |
| Documento requiere revision | El documento pasa a REQUIERE_REVISION (fecha programada, RAT, Proveedores o cambio de regimen) | WARNING | Legal/Compliance, Delegado/Responsable interno | Plataforma + correo | Una vez al dispararse; recordatorio semanal | Escala al Administrador tras 15 dias sin que se cree una nueva version en BORRADOR | Se publica la nueva version, o el documento se archiva con justificacion |
| Aviso de Privacidad no menciona un encargado nuevo | MOD-009 registra un encargado y el Aviso vigente no lo lista en el literal h) | HIGH | Delegado/Responsable interno, Legal/Compliance | Plataforma + correo | Una vez al dispararse | Escala al Administrador tras 5 dias habiles sin avance | Se publica una version que incluye al encargado, o se marca "no aplica" con justificacion en el checklist |
| Cambio de regimen 659: revisar avisos publicados | MOD-024 activa la bandera FUTURO | WARNING | Delegado/Responsable interno, Administrador | Plataforma + correo | Una vez al dispararse | Escala si no hay avance en 30 dias | Todos los avisos PUBLICADO/VIGENTE quedan marcados como revisados (con evidencia de confirmacion o de republicacion) |
| Documento vigente proximo a su revision periodica | Faltan 30 dias para la fecha de proxima revision configurada | INFO | Autor original, Legal/Compliance | Plataforma | Una vez; luego semanal en los ultimos 7 dias | Si no hay avance al llegar la fecha, se convierte en la alerta "Documento requiere revision" | Se publica una nueva version, o se pospone la fecha con justificacion registrada |

---

## J. Evidencia

| Evidencia | Como se conserva | Obligacion que prueba | Conservacion minima |
|---|---|---|---|
| Contenido de cada version publicada, con hash de integridad | Registro inmutable de DocumentVersion, con fecha, hora y usuario que publico | OBL-AVISO-01, OBL-AVISO-05, OBL-DOC-01 | 10 anios desde la publicacion (OBL-RET-04); si el documento tambien tiene relevancia mercantil o tributaria, el plazo mayor entre OBL-RET-01, OBL-RET-02 y OBL-RET-04 aplica |
| Registro de aprobaciones | Identidad de cada aprobador, fecha y hora, comentarios; nunca editable despues de registrado | Cadena de aprobacion configurada (decision de producto 2.7.14); apoya OBL-PRIN-03 (responsabilidad demostrada, colaboradora de MOD-019) | Igual que la version que aprueba |
| Checklist de contenido minimo completado al momento de cada aprobacion | Copia congelada del estado de cada casilla en el momento de aprobar, distinta del checklist en curso de versiones posteriores | OBL-AVISO-02, OBL-AVISO-03, OBL-AVISO-04 | Igual que la version que aprueba |
| Historial de versiones, nunca sobrescrito | Cada version HISTORICO permanece accesible integra, con su propio hash | OBL-RET-04 (conservacion del aviso), OBL-RET-06 (integridad de la conservacion electronica, Ley de Firma Electronica Art. 13-A) | Minimo 10 anios por version |
| Registro de la tarea "revisar avisos tras cambio de regimen" y su cierre | Tarea en MOD-021 con su historial de estado y comentarios | Evidencia de diligencia ante el cambio normativo (colaboradora de OBL-PRIN-03 via MOD-019) | Igual que la version del documento asociado |
| Paquete de exportacion con verificacion de integridad | PDF o ZIP con hash o firma validable de forma independiente | Antifeature 25 de `02_validacion/22_anti_features.md`: todo paquete exportado debe permitir verificar despues que no fue alterado | No se elimina; se puede regenerar en cualquier momento a partir del historial |

---

## K. Documentos asociados

**Documentos requeridos como entrada.** Ninguno de forma estricta para crear un documento nuevo; sin embargo, el diagnostico (MOD-004) y el RAT (MOD-006) alimentan las variables y disparan la necesidad de redactar o actualizar un Aviso de Privacidad, y MOD-009 alimenta la lista de encargados a mencionar.

**Documentos generados por este modulo.**
- Politica de Proteccion de Datos (medida organizativa reconocida por las Politicas ACE).
- Politica de Privacidad (OBL-AVISO-05, Art. 24 inc. 1).
- Aviso de Privacidad (OBL-AVISO-01 a 04, Art. 24 y Art. 7), con checklist de nueve literales y cinco elementos.
- Procedimiento ARCO-POL (OBL-DOC-01, Art. 33 inc. 1), seguido operativamente por MOD-011.

**Plantillas que el sistema provee.**
- Plantilla de Politica de Proteccion de Datos: variables de organizacion (razon social, sector); requiere validacion de la organizacion.
- Plantilla de Politica de Privacidad: variables de organizacion y de contacto del Delegado/Responsable interno; requiere validacion de la organizacion.
- Plantilla de Aviso de Privacidad: variables de organizacion, contacto del Delegado/Responsable interno, checklist de nueve literales integrado; requiere validacion de la organizacion.
- Plantilla de Procedimiento ARCO-POL: pasos base alineados con los plazos de MOD-011 y MOD-023; requiere validacion de la organizacion.

**Anexos y evidencias documentales.** Version en PDF exportada con hash de cada version publicada; evidencia de publicacion (por ejemplo, referencia de la URL publica donde se coloco el aviso, si la empresa lo hace fuera del sistema); archivo adjunto opcional cuando existe un documento firmado fuera del sistema.

**Motor documental generico reutilizado por referencia.** MOD-008 aloja tambien la entidad generica Document/DocumentVersion y el flujo de aprobacion configurable que MOD-009 Proveedores reutiliza para su propio tipo de documento Contrato/DPA. Los campos especificos de Contrato/DPA (partes, plazo del contrato, clausulas de proteccion de datos exigidas al encargado) se documentan en la ficha de MOD-009, no en esta ficha; aqui solo se documenta el motor compartido (estados, aprobacion, versionado, evidencia).

---

## L. Dependencias

```
MOD-004 Diagnostico ---\
                         \
MOD-006 RAT y Mapa ------>---- MOD-008 Documentos y Politicas ----> MOD-007 Consentimiento
de Datos                /  |                                  \---> MOD-009 Proveedores (motor
                        /   |                                       documental para Contrato/DPA)
MOD-009 Proveedores ---/    |                                  \---> MOD-012 Portal del Titular
(encargados a listar)       |                                        (publica el Aviso vigente)
                             \---> MOD-016 Retencion (aplica OBL-RET-04/06
                                    sobre los propios documentos de MOD-008)
                             \---> MOD-019 Centro de Evidencias

Consultado desde la capa transversal: MOD-001 (datos de organizacion), MOD-002 (contacto del
Delegado/Responsable interno), MOD-021 (tareas), MOD-022 (notificaciones), MOD-023 (calendario
para fechas de revision), MOD-024 (bandera del regimen 659), MOD-025 (busqueda), MOD-026 (ayuda).
```

**Entra desde:** MOD-004 (dispara la necesidad de documentos tras el diagnostico), MOD-006 (finalidades y cambios que exigen revisar el Aviso), MOD-009 (lista de encargados a mencionar en el literal h).

**Sale hacia:** MOD-007 (referencia por version exacta al Aviso de Privacidad vigente en el momento de cada consentimiento), MOD-009 (reutiliza el motor documental para Contrato/DPA), MOD-012 (publica el Aviso vigente al titular cuando ese modulo exista), MOD-016 (las reglas de retencion documental de cumplimiento se aplican sobre los documentos de este modulo), MOD-019 (evidencia continua de cada version, aprobacion y publicacion).

**Que ocurre si un modulo dependiente no existe en el MVP.**
- Si MOD-012 Portal del Titular (SHOULD HAVE) no esta disponible, el Aviso de Privacidad se sigue redactando, aprobando y publicando igual dentro de MOD-008; la empresa lo publica por otro medio (su sitio web, un lugar visible en sus instalaciones), ya que la decision de alcance 2.7.30 fija que el MVP de ARCO-POL usa un formulario interno, no un portal publico. MOD-008 no depende de MOD-012 para cumplir su propia obligacion.
- Si MOD-016 Retencion (SHOULD HAVE) no esta disponible en el MVP, MOD-008 cubre directamente, con una regla simple de no-borrado antes de 10 anios sobre sus propios documentos (sin el motor completo de retencion por finalidad), las obligaciones OBL-RET-04 y OBL-RET-06 que le corresponden como colaborador; esto esta declarado explicitamente como mecanismo de cobertura parcial en `02_validacion/06_mapa_definitivo_de_modulos.md`, seccion 3, ficha de MOD-016.
- Si MOD-009 Proveedores aun no esta operativo, el checklist del literal h) se completa manualmente con el nombre y contacto del encargado capturados como texto libre dentro del propio Aviso, en vez de por referencia; el sistema muestra una nota de que esa mencion no esta sincronizada automaticamente con un registro de Proveedores y podria quedar desactualizada.

---

## M. Dashboard

| Indicador | Formula | Semaforo | Vista |
|---|---|---|---|
| Documentos regulatorios obligatorios vigentes | Conteo de los 3 tipos obligatorios (Politica de Proteccion de Datos, Politica de Privacidad, Aviso de Privacidad) que tienen una version PUBLICADO/VIGENTE, sobre el total de 3 | Verde: 3 de 3. Amarillo: 1 o 2 de 3, o alguno en REQUIERE_REVISION. Rojo: 0 de 3, o el Aviso de Privacidad sin publicar | Gerencia (resumen de 3), Responsable/Legal (detalle por tipo con estado), Auditor (fecha y version exacta) |
| Documentos con revision pendiente | Conteo de documentos en estado REQUIERE_REVISION | Amarillo si hay al menos uno; rojo si alguno lleva mas de 30 dias sin nueva version en curso | Responsable/Legal (lista con antiguedad), Gerencia (solo el conteo) |
| Tiempo promedio de aprobacion | Promedio de dias habiles entre EN_REVISION y APROBADO de las ultimas versiones aprobadas | Sin semaforo, es un indicador de eficiencia interna | Gerencia, Legal |
| Ultima publicacion del Aviso de Privacidad | Fecha de la version PUBLICADO/VIGENTE actual y dias transcurridos desde entonces | Amarillo si supera el intervalo de revision configurado; verde en caso contrario | Responsable/Legal, Auditor |

El dashboard nunca muestra un porcentaje de "cumplimiento legal"; los indicadores de esta seccion describen el estado del programa documental (documentos vigentes, pendientes, tiempos internos), conforme al principio de `02_validacion/04_objetivo_exacto_del_producto.md`, seccion 1.2.

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia para auditoria o ACE |
|---|---|---|---|---|---|
| Inventario de documentos regulatorios | Nombre, tipo, version vigente, fecha de publicacion, proxima revision, estado | Tipo de documento, estado, sucursal | PDF, XLSX | Gerencia, Auditor | Si |
| Historial de versiones de un documento | Todas las versiones (incluidas HISTORICO y ARCHIVADO), autores, aprobadores, fechas, hash de cada una | Documento especifico, rango de fechas | PDF, CSV | Auditor, requerimiento de la ACE | Si |
| Paquete de evidencia documental | PDF firmado de cada documento vigente mas verificacion de integridad de cada uno | Tipo de documento, fecha de corte | ZIP | Auditoria de Cumplimiento (MOD-018), requerimiento de la ACE | Si |
| Checklist de contenido minimo por Aviso de Privacidad | Estado de cada literal del Art. 24 y de cada elemento del Art. 7 en la version vigente | Version especifica | PDF | Legal/Compliance, Delegado/Responsable interno | Si |

---

## O. Historial

Eventos que deben quedar en el historial del modulo y en la auditoria transversal (MOD-018/AuditLog):
- Creacion de un documento (tipo, nombre, autor, fecha).
- Cada edicion del contenido de un borrador (usuario, fecha; se registra que el contenido cambio, no necesariamente un diff campo a campo del texto libre).
- Cambios en el checklist de contenido minimo (que literal se marco o desmarco, usuario, fecha).
- Envio a revision (usuario, fecha, destinatarios de la tarea generada).
- Rechazo, con el motivo registrado.
- Aprobacion, con identidad de cada aprobador y fecha.
- Publicacion (usuario, fecha, hora, hash resultante).
- Paso automatico a HISTORICO de la version reemplazada.
- Paso a REQUIERE_REVISION, con el disparador que lo origino (fecha programada, RAT, Proveedores, cambio de regimen 659).
- Archivado, con la justificacion y, cuando aplique, la segunda aprobacion.
- Cada exportacion (usuario, fecha, version exportada, si incluyo verificacion de integridad).
- Accesos de lectura de un Auditor externo invitado a una version especifica (por ser un acceso temporal de un tercero, se registra aunque el contenido no sea un dato personal sensible).
- Cambios en la cadena de aprobacion configurada por tipo de documento (quien la modifico, valor anterior y nuevo).

---

## P. Riesgos

- **Riesgo legal: dar por valida la suficiencia juridica de un documento solo porque el checklist estructural esta completo.** Mitigacion de diseno: el checklist valida presencia de secciones, nunca calidad del contenido; todo documento generado o aprobado muestra el texto de descargo "requiere validacion de la organizacion o asesoria especializada" (seccion H).
- **Riesgo de UX: abandono del formulario de redaccion del Aviso de Privacidad por la complejidad de los nueve literales del Art. 24.** Mitigacion de diseno: wizard paso a paso con un ejemplo por literal y ayuda contextual de MOD-026 accesible sin salir del formulario.
- **Riesgo operativo: la version vigente queda desactualizada porque nadie ejecuta la tarea de revision generada automaticamente.** Mitigacion de diseno: alerta con escalamiento definido (seccion I) y semaforo visible en el dashboard (seccion M) que se pone en rojo si la tarea no avanza.
- **Riesgo de seguridad y privacidad: que un usuario pegue por error datos reales de un titular dentro del contenido de una plantilla (por ejemplo, un ejemplo con un nombre y DUI reales en vez de datos ficticios).** Mitigacion de diseno: las plantillas usan solo variables y ejemplos ficticios marcados como tales; el modulo no ofrece funcion de importar bases de datos ni de pegar tablas masivas de registros, alineado con el antifeature 8.
- **Riesgo probatorio: que la version equivocada de un documento se cite como prueba en un caso ARCO-POL o de consentimiento ya cerrado, despues de que el documento se actualice.** Mitigacion de diseno: toda referencia externa (MOD-007, MOD-011) apunta siempre a la version historica exacta usada en su momento, nunca a "la version actual" (decision 2.7.6 de `02_validacion/02_validacion_de_la_idea.md`; ver tambien seccion F de esta ficha, "Registros vinculados").
- **Riesgo regulatorio: que el cambio de regimen de la reforma 659 deje avisos publicados con menciones desactualizadas (por ejemplo, al Delegado en vez de al Responsable interno) sin que nadie lo note.** Mitigacion de diseno: tarea automatica obligatoria de revision al activarse la bandera FUTURO (seccion G, regla 3), sin republicacion automatica, y alerta con escalamiento a 30 dias (seccion I).

---

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Gestor de Politica de Proteccion de Datos (plantilla, versionado, aprobacion) | X | | | | Obligacion OBLIGATORIO (OBL-AVISO-05) sin condicion; complejidad baja; sin ella la empresa no tiene ni siquiera el documento base que las Politicas ACE exigen |
| Gestor de Politica de Privacidad | X | | | | Mismo fundamento, OBL-AVISO-05, Art. 24 inc. 1 |
| Gestor de Aviso de Privacidad con checklist de 9 literales (Art. 24) y 5 elementos (Art. 7) | X | | | | OBL-AVISO-01 a 04 OBLIGATORIO/CONDICIONAL; el plazo transitorio de mecanismos ARCO-POL asociado (OBL-PLAZO-04, propietaria MOD-012) ya vencio el 23-may-2025, lo que hace urgente tener el Aviso publicable desde el dia uno |
| Flujo de aprobacion configurable por tipo de documento | X | | | | Sin control de aprobacion, publicar un Aviso incompleto es trivial; decision de producto 2.7.14; complejidad media, valor alto |
| Versionado con historial inmutable y regla simple de no-borrado antes de 10 anios | X | | | | Cobertura directa de OBL-RET-04 y OBL-RET-06 declarada como mecanismo de cobertura del MVP en el mapa definitivo, sin depender del motor completo de MOD-016 |
| Motor documental generico reutilizable por referencia (usado por MOD-009 para Contrato/DPA) | X | | | | Dependencia estructural: sin este motor, MOD-009 no tiene donde alojar el tipo de documento Contrato/DPA; cumple la condicion (b) del test de tres condiciones del mapa definitivo |
| Exportacion con hash de integridad verificable | | X | | | Valor probatorio alto pero se puede lanzar el MVP con exportacion simple a PDF primero y anadir la verificacion de hash en una iteracion muy cercana, antes de exportar hacia la ACE (antifeature 25) |
| Wizard guiado con ejemplo por literal del Art. 24 | | X | | | Mejora de UX que reduce el riesgo de abandono (seccion P), pero el valor legal minimo ya se cubre con el checklist obligatorio sin el wizard |
| Deteccion automatica de encargado no mencionado en el Aviso (regla G-2) | | X | | | Depende de que MOD-009 Proveedores ya este operativo con datos reales; mientras tanto se cubre con el campo de texto libre descrito en la seccion L |
| Tarea automatica de revision de avisos tras cambio de regimen 659 (regla G-3) | | X | | | Logica simple y de bajo costo, pero solo se activa si la reforma efectivamente se publica y MOD-024 existe; se recomienda incluirla junto con el lanzamiento de MOD-024 |
| Plantillas para documentos internos no regulatorios (por ejemplo, manuales internos sin relacion con proteccion de datos) | | | X | | Valor de producto (retener al cliente reutilizando el mismo motor), pero fuera del alcance legal estricto de este modulo |
| Multi-idioma de documentos | | | | X | Sin obligacion legal que lo exija hoy; el mercado objetivo del MVP es exclusivamente salvadoreno |
| Firma electronica avanzada integrada dentro del flujo de aprobacion | | | | X | La Ley de Firma Electronica exige integridad verificable (OBL-RET-06), que ya se cubre con hash y versionado; una firma electronica avanzada embebida es una mejora, no una obligacion, y tiene complejidad alta |

**Version minima vendible del modulo.** Politica de Proteccion de Datos, Politica de Privacidad y Aviso de Privacidad (con su checklist de contenido minimo), mas el flujo de aprobacion configurable y el versionado con conservacion minima de 10 anios. Esta version cubre las 6 obligaciones propietarias de MOD-008, todas con plazo transitorio ya vencido o sin plazo transitorio pendiente, y es dependencia estructural directa de MOD-009 (motor documental) y de MOD-007 (referencia de version del Aviso), por lo que no puede diferirse mas alla del MVP.

---

## R. Ayuda contextual (complemento obligatorio)

**1. Aviso de Privacidad**
- Que es: un documento breve que la empresa entrega a las personas para explicarles que datos personales recolecta, para que los usa y que derechos tienen sobre ellos.
- Por que tengo que hacer esto: la ley obliga a comunicarlo por escrito en el momento en que se pide el consentimiento, no despues.
- Fundamento: OBL-AVISO-01 y OBL-AVISO-03, Art. 24 y Art. 24 inciso final de la Ley para la Proteccion de Datos Personales (Decreto 144).
- Cuando necesito ayuda juridica: si duda si el contenido que redacto cubre correctamente su caso especifico, o si esta cambiando la finalidad de un tratamiento ya existente.

**2. Politica de Privacidad**
- Que es: un documento interno mas extenso que sirve de base para el Aviso de Privacidad y debe ser consistente con el.
- Por que tengo que hacer esto: es una medida organizativa que la Agencia de Ciberseguridad del Estado (ACE) exige tener elaborada.
- Fundamento: OBL-AVISO-05, Art. 24 inc. 1 de la Ley, y Politicas de Actuacion de la ACE, Art. 4 lit. a.
- Cuando necesito ayuda juridica: al definir el alcance de la politica si su empresa tiene varias sucursales, marcas o lineas de negocio distintas.

**3. Version vigente frente a version historica**
- Que es: cada documento de este modulo tiene, en todo momento, una unica version vigente; las versiones anteriores quedan guardadas para siempre y nunca se editan.
- Por que tengo que hacer esto: para poder demostrar despues, si alguien lo pregunta, exactamente que texto vio cada persona en cada momento.
- Fundamento: OBL-CONS-05 (Art. 54, carga de la prueba, propietaria de MOD-007) y OBL-RET-04 (Art. 31 de los Lineamientos del Delegado, colaboradora de MOD-016).
- Cuando necesito ayuda juridica: si necesita usar una version historica como prueba frente a un reclamo o una inspeccion.

**4. Cadena de aprobacion**
- Que es: la lista de personas que deben revisar y aprobar un documento antes de que se pueda publicar, que usted mismo configura segun el tipo de documento.
- Por que tengo que hacer esto: para que ningun documento se publique sin que al menos otra persona lo haya revisado.
- Fundamento: decision de producto (`02_validacion/02_validacion_de_la_idea.md`, seccion 2.7, decision 14); no existe un articulo que exija especificamente esta cadena, aunque se apoya en el deber general de responsabilidad demostrada (Art. 5 lit. i de la Ley).
- Cuando necesito ayuda juridica: al decidir cuantos aprobadores debe tener un documento de alto riesgo, como el Aviso de Privacidad de una empresa que trata datos sensibles.

**5. Checklist del Articulo 24**
- Que es: una lista de nueve elementos que todo Aviso de Privacidad debe contener segun la ley.
- Por que tengo que hacer esto: la ley los exige a todas las empresas por igual, sin excepcion en cuanto a los primeros siete.
- Fundamento: OBL-AVISO-02 (literal h, datos del encargado) y OBL-AVISO-03 (literal i, cookies), Art. 24 lit. a) a i).
- Cuando necesito ayuda juridica: si un literal no le parece claramente aplicable a su caso (por ejemplo, no usa cookies) y no esta seguro de como justificarlo.

**6. Documento requiere revision**
- Que es: un estado que indica que el documento vigente probablemente quedo desactualizado por algo que cambio (una nueva finalidad, un nuevo proveedor, o un cambio en la ley del Delegado).
- Por que tengo que hacer esto: para que el aviso o la politica se mantengan alineados con lo que su empresa realmente hace.
- Fundamento: OBL-AVISO-04 y OBL-AVISO-05, Art. 7 (derecho de informacion, incluido el cambio de finalidad).
- Cuando necesito ayuda juridica: si no esta seguro de si el cambio detectado exige republicar el documento o si basta con una nota interna de seguimiento.

---

## Notas finales (desacuerdos y observaciones sobre el mapa definitivo)

1. **Precision sobre la clasificacion legal de OBL-AVISO-02 y OBL-AVISO-03.** La ficha resumida de MOD-008 en `02_validacion/06_mapa_definitivo_de_modulos.md` (linea "MVP: MUST HAVE. Justificacion: El Aviso de Privacidad (OBL-AVISO-01/02/03/05) es OBLIGATORIO...") agrupa las cuatro obligaciones como si todas fueran OBLIGATORIO. Segun `01_legal/matriz_obligaciones.json`, OBL-AVISO-01 y OBL-AVISO-05 si son OBLIGATORIO sin condicion, pero OBL-AVISO-02 (datos de contacto del encargado, literal h) y OBL-AVISO-03 (uso de cookies, literal i) estan clasificadas como CONDICIONAL: aplican solo si la empresa efectivamente subcontrata un encargado o efectivamente usa cookies. Esto no cambia la clasificacion MVP del modulo (que sigue siendo correcta por OBL-AVISO-01 y OBL-AVISO-05 solos), pero el checklist de esta ficha (seccion D) si refleja la distincion correctamente: los literales h) e i) pueden marcarse "no aplica" con justificacion, mientras que los demas literales del Art. 24 y los cinco elementos del Art. 7 no admiten esa salida. Se recomienda ajustar la redaccion de esa linea en el mapa definitivo para no dar a entender que las cuatro obligaciones son igualmente incondicionales.
2. **Relacion entre OBL-RET-04 y el doble estado de la reforma 659.** `01_legal/matriz_obligaciones.json` marca OBL-RET-04 (conservacion del aviso por 10 anios) como afectada por la reforma 659, con la nota: "si la reforma 659 elimina el delegado obligatorio en el sector privado, deberia confirmarse si la obligacion de conservacion documental subsiste bajo otra norma". Como OBL-RET-04 nace de los Lineamientos para el Delegado (un instrumento vinculado a la figura que la reforma modificaria), existe una incertidumbre genuina, ya documentada en `01_legal/03_hallazgos_regulatorios.md` seccion 9, punto 14, sobre si ese plazo de 10 anios sigue teniendo el mismo fundamento normativo despues del cambio de regimen. Esta ficha no resuelve esa incertidumbre: mientras no se aclare, MOD-008 aplica la regla de conservacion de 10 anios de forma conservadora, sin excepcion automatica por el cambio de bandera de MOD-024, y esa continuidad deberia mencionarse explicitamente en la ficha de MOD-016 (Retencion), que es la propietaria de OBL-RET-04.
3. **Alcance del "motor documental generico".** El proposito de MOD-008 en `mapa_modulos.json` lo describe como "motor documental generico reutilizado por referencia (por ejemplo, Contratos/DPA dentro de Proveedores)". Esta ficha documenta el motor compartido (estados, aprobacion, versionado, evidencia) pero deja explicitamente fuera los campos especificos del tipo Contrato/DPA, que corresponden a la ficha de MOD-009, para no duplicar contenido entre ambas fichas ni invadir la propiedad de esa obligacion (OBL-PROV-04 y OBL-PROV-06 son colaboradoras aqui, propietarias en MOD-009). No se detecto ninguna inconsistencia en esta division, solo se deja constancia del limite para quien redacte la ficha de MOD-009 a continuacion.

No se identificaron desacuerdos adicionales con `02_validacion/02_validacion_de_la_idea.md`, `02_validacion/04_objetivo_exacto_del_producto.md`, `02_validacion/05_tipos_de_usuario.md` ni `02_validacion/22_anti_features.md` respecto del alcance asignado a MOD-008.
