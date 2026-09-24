# EP-021 Centro de Tareas (MOD-021)

**Objetivo.** Convertir cualquier obligacion detectada, paso de un flujo o hallazgo de auditoria en una tarea con responsable, fecha limite y estado, con aprobacion humana obligatoria antes de cerrarla y con historial inmutable, para que la empresa tenga una sola bandeja de trabajo por persona en vez de pendientes dispersos por modulo.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R1 | 16 | 61 | 56 | 5 | [MOD-021](../../03_modulos/MOD-021_ficha.md) |

**Notas de la epica.**

- MOD-021 no es propietaria de ningun OBL-ID (es colaboradora de OBL-INC-01, OBL-PLAZO-01, OBL-SANC-03, OBL-SANC-05 y OBL-SANC-06, seccion A de la ficha). Por eso la mayoria de las HU dejan fundamento vacio; solo se cita un OBL-ID cuando la HU implementa directamente el comportamiento que sostiene esa obligacion (fecha limite via MOD-023, escalamiento de 72 horas, identidad del aprobador, historial, evidencia).
- Discrepancia entre el encargo y la tabla Q: la fila Archivado automatico No aplica por cambio de regimen 659 esta clasificada SHOULD HAVE, con cobertura minima en MVP, y no aparece en la version minima vendible que la propia seccion Q describe al final (esa lista solo incluye estados basicos, fecha limite, Aprobacion con bloqueo de autorrevision, alertas con escalamiento de 72 horas e historial). El encargo especifico de esta epica pide igualmente cubrir el estado No aplica, asi que se incluyo como HU-021-16, dejandola en release R2 y dejando constancia de que no forma parte del nucleo vendible de 19.8 ni de la version minima vendible de la ficha.
- El listado basico de tareas exportable en XLSX o CSV (HU-021-14) no tiene fila propia MUST HAVE en la tabla Q: la fila con esa clasificacion es Reportes exportables avanzados (SHOULD HAVE), pero su propia columna de justificacion aclara en texto que el listado basico de tareas (XLSX/CSV) es MUST HAVE. Se incluyo la HU por esa aclaracion explicita, acotada solo al listado simple sin filtros avanzados de aprobaciones ni paquetes archivados.
- Se excluyen del MVP de esta epica, por ser SHOULD HAVE, COULD HAVE o FUTURE en la tabla Q y por instruccion explicita del encargo: tareas recurrentes automaticas con Periodicidad (en este MVP la siguiente instancia se crea manualmente), vista tipo tablero o calendario visual, dependencias entre tareas con validacion tecnica de ciclos (el campo Motivo de bloqueo admite texto libre de referencia a otra tarea, sin bloqueo automatico de ciclos), reportes exportables avanzados (historial de aprobaciones, paquete de tareas archivadas) y vista consolidada multi-sociedad.
- El campo depende_de de MOD-021 en mapa_modulos.json esta incompleto frente a las propias fichas de MOD-014 y MOD-018 (ambas declaran Sale hacia MOD-021) y frente a la prosa de proposito del mapa definitivo, que tambien menciona Proveedores y Documentos como fuentes. La propia ficha de MOD-021 (seccion L.2 y nota final) y 24_preguntas_pendientes.md (PP-MAPA-11, PP-MAPA-12) ya dejan constancia de esta asimetria. No se modifico ningun archivo del mapa desde este backlog; el catalogo abierto del campo Modulo de origen (seccion D.1) ya modela cualquier origen sin depender de que se corrija el mapa.
- MOD-021 necesita de MOD-001 el catalogo de usuarios activos, roles y areas/sucursales para resolver los campos Responsable y Area o unidad responsable; se declaro MOD-001 en depende_de_modulos solo en las HU donde ese campo especifico interviene (creacion automatica, creacion manual y bandeja), no en todas.
- Todas las HU de esta epica se ubicaron en R1 salvo HU-021-16 (estado No aplica), consistente con 19.8 y 19.9, que construyen MOD-021 completo como infraestructura transversal desde el inicio del nucleo vendible.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-021-01 | Generar automaticamente una tarea desde un evento de otro modulo | Administrador de la organizacion | 3 | R1 | 3 | MOD-001 |
| HU-021-02 | Crear manualmente una tarea en el Centro de Tareas | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R1 | 5 | MOD-001 |
| HU-021-03 | Avanzar una tarea por sus estados basicos | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 5 | R1 | 5 | HU-021-01, HU-021-02 |
| HU-021-04 | Consultar la bandeja de tareas propia por persona | Usuario de consulta / Colaborador | 3 | R1 | 5 | HU-021-01, HU-021-02, MOD-001 |
| HU-021-05 | Adjuntar y gestionar evidencia de una tarea | Responsable ARCO-POL / Responsable del tramite | 3 | R1 | 5 | HU-021-01, HU-021-02 |
| HU-021-06 | Registrar comentarios en la bitacora de una tarea | Asesor externo invitado | 2 | R1 | 6 | HU-021-01, HU-021-02 |
| HU-021-07 | Mostrar la fecha limite calculada por el motor de plazos con su desglose | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R1 | 6 | HU-021-01, HU-021-02, MOD-023 |
| HU-021-08 | Marcar automaticamente una tarea como vencida | Administrador de la organizacion | 3 | R1 | 6 | HU-021-03, HU-021-07 |
| HU-021-09 | Enviar una tarea a revision y generar la Aprobacion correspondiente | Responsable ARCO-POL / Responsable del tramite | 5 | R1 | 6 | HU-021-03, HU-021-05, MOD-022 |
| HU-021-10 | Resolver una Aprobacion con bloqueo de autorrevision | Aprobador | 5 | R1 | 6 | HU-021-09, MOD-022 |
| HU-021-11 | Emitir alertas de tarea proxima a vencer y tarea vencida | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R1 | 6 | HU-021-07, HU-021-08, MOD-022, MOD-023 |
| HU-021-12 | Escalar automaticamente la alerta critica de 72 horas | Responsable de Seguridad / IT | 5 | R1 | 6 | HU-021-11, MOD-022, MOD-023 |
| HU-021-13 | Mantener el historial inmutable de la tarea y la aprobacion | Auditor (interno) | 5 | R1 | 7 | HU-021-03, HU-021-09, HU-021-10 |
| HU-021-14 | Exportar el listado de tareas | Responsable Legal / Compliance | 3 | R1 | 6 | HU-021-04 |
| HU-021-15 | Alojar la tarea generica de cobertura parcial del Diagnostico | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R1 | 7 | HU-021-01, MOD-004 |
| HU-021-16 | Archivar una tarea como No aplica tras el cambio de regimen | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 35 | HU-021-03, HU-021-13, MOD-024 |

## Historias

### HU-021-01. Generar automaticamente una tarea desde un evento de otro modulo

**Como** Administrador de la organizacion, **quiero** que el sistema cree automaticamente una tarea en el Centro de Tareas cuando un modulo de origen detecte un hecho que exige una accion, **para** que ninguna obligacion detectada por otro modulo quede sin responsable ni fecha.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 3 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado que un modulo de origen del catalogo (MOD-002, MOD-004, MOD-005, MOD-006, MOD-008, MOD-009, MOD-011, MOD-013, MOD-014, MOD-016, MOD-017, MOD-018 o MOD-024) genera un hecho mapeado a una plantilla de tarea, cuando el hecho ocurre, entonces el sistema crea una Tarea en estado Pendiente con el campo Modulo de origen igual a ese modulo, sin intervencion manual.
2. Dado que el modulo de origen entrega Titulo, Descripcion, Obligacion relacionada, Tipo de tarea y el Responsable sugerido, cuando se crea la tarea, entonces esos campos quedan precargados y el sistema registra la Fecha de creacion de forma automatica y no editable.
3. Dado que el modulo de origen indica una Obligacion relacionada, cuando se guarda la tarea, entonces el sistema valida que cada OBL-ID exista en la matriz de obligaciones antes de guardarlo, y la tarea puede quedar con cero, uno o varios OBL-ID.
4. Dado que la tarea creada corresponde a un Tipo de tarea con evidencia requerida definida en el catalogo (Incidente, ARCO-POL, Delegado/Responsable interno o Procedimiento sancionador), cuando se crea, entonces el sistema precarga el catalogo de Evidencia requerida sugerido para ese tipo, sin exigirla todavia en este paso.
5. Dado que el modulo de origen indicado no existe o el registro de origen referenciado no existe, cuando se intenta crear la tarea, entonces el sistema rechaza la creacion automatica porque el campo Modulo de origen exige que el registro de origen exista.
6. Dado que se crea una tarea nueva, cuando se guarda, entonces el sistema registra un evento de auditoria (creacion, modulo de origen, fecha y hora) y notifica al Responsable asignado a traves de MOD-022.
7. Dado que el Responsable sugerido no coincide con ningun usuario activo con un rol compatible con el Tipo de tarea, cuando se crea la tarea, entonces el sistema la deja sin Responsable asignado en firme y la muestra como pendiente de asignacion, sin bloquear su creacion.

**Reglas de negocio**

- El Modulo de origen es obligatorio y, si no es Manual, el registro de origen debe existir (seccion D.1).
- Titulo, Descripcion, Modulo de origen, Obligacion relacionada, Tipo de tarea y Responsable sugerido llegan precargados desde el modulo que genera la tarea (seccion D.1, nota de campos precargados).
- MOD-021 nunca decide el fundamento legal de una tarea, siempre lo hereda del modulo de origen (seccion A).

**Fuera de alcance**

- El calculo de la fecha limite legal, que se pide a MOD-023 (HU-021-07).
- La creacion manual de una tarea sin evento de origen (HU-021-02).

- Requiere contenido: Plantilla de tarea por tipo (por ejemplo Responder solicitud ARCO-POL, Notificar vulneracion de seguridad, Renovar contrato de encargado), con evidencia requerida sugerida segun el tipo, validada por la organizacion antes de usarse tal cual (seccion K).
- Referencia: MOD-021 secciones A, D.1, F.2 (fila no existe -> Pendiente), G (fila 1); 12_tareas_y_alertas.md 12.2
- Notas: Es la capacidad habilitadora que MOD-002, MOD-004, MOD-005, MOD-011 y MOD-013 (todos MUST HAVE) necesitan para operar (19.2, condicion b).

### HU-021-02. Crear manualmente una tarea en el Centro de Tareas

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** registrar manualmente una tarea con su titulo, tipo, responsable y prioridad, **para** dejar constancia de un pendiente de mi area que no proviene de ningun otro modulo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 5 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado que tengo el permiso Crear tarea manual, cuando completo Titulo (maximo 140 caracteres), Tipo de tarea y guardo, entonces el sistema crea la tarea con Modulo de origen Manual y Estado Pendiente.
2. Dado que dejo el Titulo vacio o supero 140 caracteres, cuando intento guardar, entonces el sistema rechaza el guardado y senala el campo Titulo como invalido.
3. Dado que mi rol no tiene el permiso Crear tarea manual (por ejemplo Usuario de consulta / Colaborador o Auditor (interno)), cuando intento crear una tarea, entonces el sistema deniega la accion.
4. Dado que asigno un Responsable, cuando lo selecciono, entonces el sistema solo permite elegir usuarios activos de la organizacion cuyo rol sea compatible con el Tipo de tarea elegido.
5. Dado que faltan menos de 5 dias habiles (umbral configurable) para el vencimiento de un plazo legal en curso vinculado a la tarea, cuando el sistema evalua la Prioridad, entonces la sugiere automaticamente como Alta o Critica, pero deja que el responsable o su superior decidan la prioridad final sin imponerla de forma definitiva.
6. Dado que marco Es recurrente en Si, cuando intento guardar sin indicar Periodicidad, entonces el sistema exige el campo Periodicidad antes de guardar.
7. Dado que la tarea creada manualmente queda guardada, cuando se guarda, entonces el sistema registra un evento de auditoria de creacion con el usuario que la creo y notifica al Responsable asignado via MOD-022.

**Reglas de negocio**

- El campo Titulo es obligatorio siempre, maximo 140 caracteres (seccion D.1).
- El catalogo de Tipo de tarea es cerrado: Diagnostico, Plan de cumplimiento, ARCO-POL, Incidente, Documento, Proveedor, Riesgo/EIPD, Retencion, Capacitacion, Auditoria, Delegado/Responsable interno, Procedimiento sancionador, Regulatorio, Otra (seccion D.1).
- El sistema nunca decide por si mismo la prioridad final cuando compiten varios plazos legales por los mismos recursos: solo la sugiere (seccion H).

**Fuera de alcance**

- Tareas recurrentes automaticas mas alla de exigir el campo Periodicidad: la siguiente instancia se crea manualmente en este MVP (tabla Q, fila SHOULD HAVE).

- Referencia: MOD-021 secciones C, D.1, F.2, H (ultimo punto)

### HU-021-03. Avanzar una tarea por sus estados basicos

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** iniciar, bloquear, desbloquear, completar y reabrir una tarea segun su flujo de estados, **para** reflejar en todo momento en que paso del trabajo esta cada tarea.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 5 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-021-01, HU-021-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que una tarea esta en Pendiente y tiene Responsable asignado, cuando el responsable marca iniciar, entonces la tarea pasa a En proceso y el sistema registra el evento de auditoria correspondiente.
2. Dado que una tarea esta en En proceso, cuando el responsable la marca como Bloqueada sin indicar el Motivo de bloqueo, entonces el sistema rechaza el cambio de estado porque ese campo es obligatorio en ese estado.
3. Dado que una tarea esta en En proceso, cuando el responsable la marca como Bloqueada con un Motivo de bloqueo valido, entonces la tarea pasa a Bloqueada, se pausa el conteo de tiempo activo, y si otra tarea la tiene como Dependencia, se notifica a esa tarea dependiente.
4. Dado que una tarea Bloqueada tiene resuelto su impedimento, cuando el usuario confirma que el impedimento ya no existe, entonces la tarea vuelve a En proceso y se reanuda el conteo de tiempo activo.
5. Dado que una tarea esta Completada, cuando un Administrador, un Delegado/Responsable interno o un Responsable Legal/Compliance solicita reabrirla sin registrar un motivo de reapertura, entonces el sistema rechaza la reapertura porque ese motivo es obligatorio.
6. Dado que una tarea Completada se reabre con motivo registrado, cuando se confirma, entonces la tarea vuelve a Pendiente o a En proceso segun el motivo, se registra el evento de auditoria con ese motivo, y la version anterior de la evidencia se conserva sin sobrescribirse.
7. Dado que un rol sin permiso para cambiar de estado (por ejemplo Auditor (interno) o Aprobador) intenta iniciar, bloquear o completar una tarea, cuando lo intenta, entonces el sistema deniega la accion.

**Reglas de negocio**

- Tabla de transiciones de la seccion F.2: Pendiente a En proceso a Bloqueada a En proceso a En revision a Aprobada a Completada, con reapertura posible desde Completada.
- El Motivo de bloqueo es obligatorio siempre que el Estado sea Bloqueada (seccion D.1).
- Eliminar una tarea no existe para ningun rol: solo se puede archivar (seccion C, nota especifica).

- Referencia: MOD-021 secciones F.1, F.2, C

### HU-021-04. Consultar la bandeja de tareas propia por persona

**Como** Usuario de consulta / Colaborador, **quiero** ver en un solo lugar unicamente las tareas que se me asignaron, filtradas por estado, tipo y fecha limite, **para** saber que me toca hacer sin recorrer otros modulos.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 5 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-021-01, HU-021-02
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado que inicio sesion como Usuario de consulta / Colaborador, cuando abro el Centro de Tareas, entonces solo veo las tareas puntuales que se me asignaron, sin visibilidad del resto de tareas de la organizacion.
2. Dado que soy Administrador de la organizacion, cuando abro el Centro de Tareas, entonces veo todas las tareas de la organizacion, con la opcion de filtrar por Estado, Tipo de tarea, Responsable, Area y rango de Fecha limite.
3. Dado que soy Responsable de area, cuando filtro mi bandeja, entonces solo veo las tareas de mi propia area o sucursal, nunca el agregado de otras areas.
4. Dado que una tarea tiene Nivel de confidencialidad Sensible o Muy sensible, cuando un usuario que no es el Responsable, el Delegado/Responsable interno ni el Administrador intenta verla en la bandeja, entonces el sistema no la muestra y ese acceso queda restringido.
5. Dado que ordeno mi bandeja por Fecha limite, cuando la reviso, entonces las tareas con plazo legal en curso quedan distinguibles de las tareas internas sin plazo legal, sin que las internas oculten a las que si tienen plazo.
6. Dado que soy Auditor (interno), cuando abro el Centro de Tareas, entonces veo todas las tareas de la organizacion en modo solo lectura, sin poder crear, editar ni aprobar ninguna.

**Reglas de negocio**

- Permisos de Ver: Si para Administrador y Delegado, Si* (solo lo propio o asignado) para el resto de roles operativos, Si de solo lectura para Auditor interno (seccion C).
- Responsable de area ve solo su propia area, nunca el agregado de otras (11_roles_y_permisos.md, seccion 11.2).
- El Nivel de confidencialidad limita quien puede ver la tarea ademas del responsable y el rol correspondiente (seccion D.1).

**Fuera de alcance**

- Vista tipo tablero (kanban) o calendario visual de tareas: clasificacion COULD HAVE, no se construye en este MVP.

- Referencia: MOD-021 secciones B, C, P (riesgo de UX, vista Mis tareas de hoy)

### HU-021-05. Adjuntar y gestionar evidencia de una tarea

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** adjuntar los archivos que prueban que complete una tarea, **para** dejar evidencia verificable de que la ejecute.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 5 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-021-01, HU-021-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el Tipo de tarea es Incidente, ARCO-POL, Delegado/Responsable interno o Procedimiento sancionador, cuando intento pasar la tarea a En revision sin ningun archivo que corresponda a la Evidencia requerida marcada, entonces el sistema rechaza la transicion.
2. Dado que adjunto un archivo, cuando lo cargo, entonces el sistema verifica el tipo de archivo permitido por la politica de seguridad de la organizacion y el tamano maximo configurado, y rechaza el archivo si no cumple.
3. Dado que una tarea esta Completada, cuando intento eliminar un adjunto que ya forma parte de ella, entonces el sistema no lo permite; solo puedo agregar una version nueva y la anterior se conserva.
4. Dado que adjunto o elimino un archivo de una tarea que no esta Completada, cuando lo hago, entonces el sistema registra el evento en el historial con quien lo hizo y cuando.
5. Dado que mi rol no tiene permiso de Adjuntar evidencia (por ejemplo Auditor (interno) o Auditor externo (invitado)), cuando intento adjuntar un archivo, entonces el sistema deniega la accion.

**Reglas de negocio**

- La Tarea nunca almacena el dato personal del titular en si, solo una referencia al expediente de origen (seccion D.1, Minimizacion de datos personales).
- No se permite eliminar un adjunto que ya forma parte de una tarea Completada, solo agregar versiones nuevas (seccion O).

- Referencia: MOD-021 secciones D.1 (Evidencia requerida, Archivos adjuntos), O, J

### HU-021-06. Registrar comentarios en la bitacora de una tarea

**Como** Asesor externo invitado, **quiero** dejar un comentario en la tarea especifica que se me asigno, **para** coordinar con quien retome el trabajo despues sin tener visibilidad del resto de tareas.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 6 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-021-01, HU-021-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que tengo acceso a una tarea especifica por invitacion puntual, cuando escribo un comentario y lo guardo, entonces queda registrado con mi identidad y la fecha, sin poder editarlo ni borrarlo despues.
2. Dado que un comentario ya fue guardado, cuando cualquier usuario intenta editarlo o borrarlo, entonces el sistema no lo permite para ningun rol.
3. Dado que mi rol es Auditor (interno) o Auditor externo (invitado), cuando intento comentar una tarea, entonces el sistema deniega la accion porque esos roles son de solo lectura.
4. Dado que agrego un comentario, cuando lo guardo, entonces el sistema lo agrega al historial de la tarea, visible para quienes tienen permiso de Ver esa tarea.

**Reglas de negocio**

- Los comentarios quedan con autor y fecha, no editables ni borrables (seccion D.1).
- El rol Auditor (interno o externo) es siempre de solo lectura, nunca comenta ni aprueba (seccion C).

- Referencia: MOD-021 secciones D.1 (Comentarios), C, O

### HU-021-07. Mostrar la fecha limite calculada por el motor de plazos con su desglose

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** ver la fecha limite de una tarea con plazo legal calculada por el motor de plazos y su desglose, **para** confiar en un unico calculo de plazos en toda la organizacion, sin que cada tarea lo calcule por su cuenta.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 6 | No |

- Fundamento: OBL-PLAZO-01 (Art. 82 LPA, Ley de Procedimientos Administrativos)
- Depende de: HU-021-01, HU-021-02
- Modulos requeridos: MOD-023

**Criterios de aceptacion**

1. Dado que una tarea tiene un plazo legal asociado, cuando se crea o se necesita su Fecha limite, entonces el sistema nunca la calcula dentro de MOD-021 y siempre se la pide a MOD-023, mostrando la fecha resultante en la tarea.
2. Dado que la Fecha limite proviene de un plazo legal, cuando intento editarla a mano, entonces el sistema bloquea la edicion manual de ese campo; solo MOD-023 puede recalcularla.
3. Dado que la tarea no tiene plazo legal (tarea interna), cuando edito su Fecha limite, entonces el sistema permite el cambio siempre que registre una justificacion y la nueva fecha no sea anterior a la Fecha de creacion.
4. Dado que la fecha limite tiene una ambiguedad juridica documentada (por ejemplo el plazo de 72 horas del Art. 25), cuando se muestra la fecha, entonces el sistema muestra tambien el Criterio de computo mostrado (por ejemplo Horas corridas, criterio conservador) junto con el texto La ley no precisa si este plazo se cuenta en horas corridas u horas habiles. El sistema aplica por defecto el criterio mas conservador (horas corridas). Verifique este criterio con asesoria legal si el caso es critico.
5. Dado que abro la vista expandible del calculo, cuando la consulto, entonces veo el dia 1 del computo, cada dia u hora excluido con su motivo, la fecha resultante y la version del calendario usada para ese calculo especifico.
6. Dado que MOD-023 recalcula la Fecha limite porque cambio el calendario de dias inhabiles mientras el plazo seguia abierto, cuando ocurre el recalculo, entonces el sistema conserva el valor anterior en el historial de la tarea y notifica el cambio via MOD-022, sin mover la fecha en silencio.

**Reglas de negocio**

- MOD-021 nunca calcula un plazo legal por su cuenta, siempre lo pide a MOD-023 (secciones A, H y L.2).
- El campo Fecha limite se bloquea para edicion manual cuando proviene de un plazo legal (seccion D.1).
- El criterio de computo ambiguo se muestra siempre junto a la fecha, con el texto de advertencia estandar (seccion H).

**Fuera de alcance**

- El calculo mismo de dias y horas habiles, que es capacidad propia de MOD-023.

- Requiere validacion legal: Si (PP-JUR-02, PP-JUR-03)
- Referencia: MOD-021 secciones D.1 (Fecha limite, Criterio de computo mostrado), H, P; 12_tareas_y_alertas.md 12.1.6, 12.5
- Notas: El calculo mismo (dias u horas habiles) es capacidad de MOD-023 (EP-023); esta HU cubre como MOD-021 lo solicita, lo bloquea para edicion manual y lo muestra con su desglose.

### HU-021-08. Marcar automaticamente una tarea como vencida

**Como** Administrador de la organizacion, **quiero** que el sistema marque visualmente como vencida cualquier tarea cuya fecha limite se cumplio sin completarse, **para** ver de inmediato que plazos ya se pasaron, sin que queden ocultos.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 6 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-021-03, HU-021-07
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que una tarea no terminal (no esta en Completada ni en No aplica) llega a su Fecha limite sin cambiar de estado, cuando se cumple esa fecha, entonces el sistema activa la bandera Vencida en Si de forma automatica, sin intervencion humana.
2. Dado que la bandera Vencida se activa, cuando se muestra la tarea, entonces se ve en rojo y sigue su flujo normal desde el estado en que estaba, sin que Vencida reemplace ni excluya el valor del campo Estado.
3. Dado que una tarea con la bandera Vencida en Si finalmente se completa fuera de tiempo, cuando se marca Completada, entonces el registro de que estuvo vencida permanece visible de forma permanente en su historial, sin ocultarse ni borrarse.
4. Dado que una tarea pasa a Completada o a No aplica antes de cumplirse la Fecha limite, cuando eso ocurre, entonces la bandera Vencida nunca se activa para esa tarea.
5. Dado que la bandera Vencida se activa, cuando ocurre, entonces el indicador de tareas vencidas del dashboard sube y se dispara la alerta correspondiente hacia MOD-022.

**Reglas de negocio**

- Vencida es un campo booleano paralelo, no excluyente con los estados salvo Completada y No aplica (seccion D.1, actualizacion fase 3; seccion F.1).
- Ninguna vista del sistema permite borrar, editar o disimular un vencimiento ya ocurrido (22_anti_features.md item 19; 12_tareas_y_alertas.md 12.5.3).

- Referencia: MOD-021 secciones D.1 (Vencida bandera), F.1, F.2 (ultima fila), M; 12_tareas_y_alertas.md 12.1.3, 12.5.3

### HU-021-09. Enviar una tarea a revision y generar la Aprobacion correspondiente

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** marcar mi tarea como lista para revision cuando termine el trabajo, **para** que la persona con el rol correspondiente la apruebe antes de darla por cerrada.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 6 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-021-03, HU-021-05
- Modulos requeridos: MOD-022

**Criterios de aceptacion**

1. Dado que una tarea esta En proceso y su Tipo de tarea exige Evidencia requerida, cuando intento marcarla lista para revision sin al menos un archivo cargado de esa evidencia, entonces el sistema rechaza la transicion.
2. Dado que una tarea esta En proceso sin Descripcion completa, cuando intento marcarla lista para revision, entonces el sistema rechaza la transicion porque la Descripcion es obligatoria antes de pasar a En revision.
3. Dado que una tarea cumple sus validaciones, cuando la marco lista para revision, entonces pasa a En revision y, si su Tipo de tarea esta en el catalogo que exige aprobacion (Documento, Acto del Delegado/Responsable interno, Cierre de incidente, Resultado de EIPD/riesgo, Respuesta ARCO-POL sensible, Plan de accion correctiva sancionador), el sistema crea automaticamente el registro de Aprobacion.
4. Dado que se crea la Aprobacion, cuando se genera, entonces el sistema autocompleta el Rol requerido segun el Tipo de aprobacion y sugiere un Aprobador asignado con ese rol, distinto de quien envio la tarea a revision.
5. Dado que se crea la Aprobacion, cuando queda creada, entonces el sistema notifica al Aprobador asignado a traves de MOD-022 y registra el evento de auditoria de la solicitud.
6. Dado que el Tipo de tarea no requiere Aprobacion (por ejemplo una tarea Otra sin acto legal asociado), cuando la tarea pasa a En revision, entonces el sistema no crea un registro de Aprobacion y permite cerrarla segun su propio flujo.

**Reglas de negocio**

- De En proceso a En revision exige Evidencia requerida cargada cuando el tipo la exige y Descripcion completa (seccion F.2).
- El catalogo de tipos que exige Aprobacion es fijo: Documento, Acto del Delegado/Responsable interno, Cierre de incidente, Resultado de EIPD/riesgo, Respuesta ARCO-POL sensible, Plan de accion correctiva sancionador, Otra (seccion D.2).

- Referencia: MOD-021 secciones D.2, F.2 (fila En proceso -> En revision), G

### HU-021-10. Resolver una Aprobacion con bloqueo de autorrevision

**Como** Aprobador, **quiero** aprobar, devolver con comentarios o rechazar una tarea que esta en revision, **para** dar el visto bueno formal antes de que el trabajo se de por cerrado.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 6 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-021-09
- Modulos requeridos: MOD-022

**Criterios de aceptacion**

1. Dado que una Aprobacion esta pendiente y el usuario conectado es el mismo que dejo la tarea en En revision, cuando intenta aprobarla, entonces el sistema bloquea la accion Aprobar y muestra la advertencia de autorrevision, salvo que la organizacion este por debajo del umbral configurable de separacion de funciones (propuesta inicial 50 empleados).
2. Dado que la organizacion esta por debajo del umbral configurable, cuando la misma persona aprueba su propio trabajo, entonces el sistema lo permite pero muestra siempre una advertencia visible de autorrevision y la deja marcada como tal en el historial.
3. Dado que el Aprobador aprueba, cuando registra la Decision Aprobada, entonces la tarea pasa a Aprobada, se registra la Identidad del aprobador con fecha y hora, y ningun caso pasa a Aprobada sin esa accion humana explicita, mostrando el texto Requiere validacion de la organizacion o asesoria especializada si algo intenta forzar una aprobacion automatica.
4. Dado que el Aprobador devuelve con cambios o rechaza sin registrar el Comentario de la decision, cuando intenta guardar, entonces el sistema rechaza el guardado porque ese comentario es obligatorio en esos dos casos.
5. Dado que el Aprobador devuelve con cambios o rechaza con comentario, cuando lo guarda, entonces la tarea regresa a En proceso y se notifica al responsable original con el motivo via MOD-022.
6. Dado que una Aprobacion sigue sin Decision durante mas de 3 dias habiles (umbral configurable), cuando se cumple ese plazo, entonces el sistema copia el aviso al Administrador a los 5 dias habiles, pero nunca reasigna automaticamente la Aprobacion a otra persona.
7. Dado que el Tipo de aprobacion es Documento, cuando se resuelve, entonces la Aprobacion exige registrar la Version del objeto aprobado, que debe ser una version existente en MOD-008.

**Reglas de negocio**

- Bloqueo tecnico de autorrevision salvo pyme bajo el umbral, con advertencia visible (seccion C).
- El sistema nunca marca Aprobada una tarea de forma automatica (seccion H).
- El escalamiento de una Aprobacion pendiente nunca reasigna automaticamente a otra persona, solo copia el aviso (seccion H).

- Referencia: MOD-021 secciones C (separacion de funciones), D.2, F.2, H, I (fila Aprobacion pendiente)

### HU-021-11. Emitir alertas de tarea proxima a vencer y tarea vencida

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** recibir un aviso cuando mi tarea este por vencer o cuando ya haya vencido, **para** reaccionar a tiempo sin tener que revisar el sistema todo el dia.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 6 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-021-07, HU-021-08
- Modulos requeridos: MOD-022, MOD-023

**Criterios de aceptacion**

1. Dado que faltan 5 dias habiles (umbral configurable) para la Fecha limite de una tarea que no esta Completada ni No aplica, cuando se cumple ese umbral, entonces el sistema emite hacia MOD-022 el evento de tarea proxima a vencer, nivel WARNING, dirigido al Responsable asignado.
2. Dado que la tarea tiene un plazo de 72 horas, cuando faltan 12 horas para su vencimiento, entonces el sistema emite el mismo tipo de evento con el umbral especifico de 12 horas en lugar de 5 dias habiles.
3. Dado que la Fecha limite de una tarea se cumple sin que llegue a Completada ni a No aplica, cuando eso ocurre, entonces el sistema emite hacia MOD-022 el evento de tarea vencida, nivel HIGH, dirigido al Responsable asignado y al Administrador.
4. Dado que una tarea proxima a vencer sigue sin avance 2 dias habiles despues de emitida la primera alerta, cuando se cumple ese plazo, entonces el sistema copia el aviso al Delegado/Responsable interno o al superior de area.
5. Dado que una tarea vencida sigue sin actividad 24 horas despues de vencida, cuando se cumple ese plazo, entonces el sistema escala el aviso a Delegado/Responsable interno y a Responsable Legal/Compliance.
6. Dado que una tarea pasa a Completada o a No aplica, cuando eso ocurre, entonces el sistema deja de emitir el evento de tarea proxima a vencer o tarea vencida para esa tarea.

**Reglas de negocio**

- MOD-021 nunca envia notificaciones directamente al usuario: emite el evento y delega el envio a MOD-022 (seccion A).
- El umbral por defecto es 5 dias habiles para plazos largos y 12 horas para plazos de 72 horas, ambos configurables (seccion I).

- Referencia: MOD-021 seccion I (filas Tarea proxima a vencer, Tarea vencida); 12_tareas_y_alertas.md 12.3, 12.4

### HU-021-12. Escalar automaticamente la alerta critica de 72 horas

**Como** Responsable de Seguridad / IT, **quiero** que el sistema escale automaticamente el aviso cuando el plazo de notificacion de un incidente este por vencer, **para** no dejar pasar el plazo mas critico de la ley sin que alguien reaccione a tiempo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 6 | No |

- Fundamento: OBL-INC-01 (Art. 25, Ley para la Proteccion de Datos Personales)
- Depende de: HU-021-11
- Modulos requeridos: MOD-022, MOD-023

**Criterios de aceptacion**

1. Dado que una tarea de notificacion externa de un incidente tiene menos de 12 horas restantes para su vencimiento, cuando se cumple ese umbral, entonces el sistema emite hacia MOD-022 el evento de plazo critico de 72 horas, nivel CRITICAL, dirigido al Responsable de Seguridad/IT y al Delegado/Responsable interno.
2. Dado que el plazo critico de 72 horas sigue corriendo, cuando pasa el tiempo, entonces el sistema repite el evento cada 2 horas mientras la tarea de notificacion no se complete.
3. Dado que se activa el nivel CRITICAL de esta alerta, cuando se activa, entonces el sistema escala de inmediato al Administrador y a Responsable Legal/Compliance, sin esperar un umbral adicional.
4. Dado que la tarea de notificacion externa se marca Completada con evidencia de envio adjunta, cuando eso ocurre, entonces el sistema deja de emitir esta alerta para esa tarea.
5. Dado que el plazo de 72 horas se cumple sin que la tarea de notificacion se complete, cuando eso ocurre, entonces el incumplimiento queda registrado de forma permanente en el historial, aunque la alerta activa deje de repetirse.
6. Dado que se muestra esta alerta o la fecha limite asociada, cuando se muestra, entonces el sistema indica el Criterio de computo mostrado (Horas corridas, criterio conservador) con el texto de advertencia estandar sobre la ambiguedad del Art. 25.

**Reglas de negocio**

- El escalamiento a Administrador y a Responsable Legal/Compliance es inmediato al activarse CRITICAL, sin umbral adicional (seccion I).
- Un vencimiento ya ocurrido nunca se apaga del todo: queda registrado de forma permanente aunque la alerta activa deje de repetirse (12_tareas_y_alertas.md 12.5.3).

- Requiere validacion legal: Si (PP-JUR-01)
- Referencia: MOD-021 seccion I (fila Plazo critico de 72 horas de un incidente en curso); 12_tareas_y_alertas.md 12.3.13, 12.5.3
- Notas: El conteo de las 72 horas lo calcula MOD-013/MOD-023; esta HU cubre el escalamiento de la alerta dentro de MOD-021/MOD-022, que es la fila propia de MOD-021 en la tabla Q.

### HU-021-13. Mantener el historial inmutable de la tarea y la aprobacion

**Como** Auditor (interno), **quiero** consultar el historial completo de una tarea y sus aprobaciones, **para** verificar la gestion realizada sin poder alterarla.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 7 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-021-03, HU-021-09, HU-021-10
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que ocurre la creacion de una tarea, un cambio de campo relevante (Responsable, Fecha limite, Prioridad, Estado, Area), una asignacion, una solicitud o resolucion de Aprobacion, un adjunto cargado o un archivado, cuando ocurre cada uno de esos hechos, entonces el sistema agrega un evento al historial de la tarea con usuario, fecha y hora, y lo replica en el AuditLog transversal.
2. Dado que un Auditor (interno) o un Auditor externo (invitado) consulta el historial, cuando lo hace, entonces lo ve completo en modo solo lectura, sin poder crear, editar ni borrar ningun evento.
3. Dado que cualquier usuario, incluido el Administrador de la organizacion, intenta eliminar un evento del historial o la tarea misma, cuando lo intenta, entonces el sistema no lo permite y muestra el texto El historial de tareas no puede eliminarse; solo puede archivarse.
4. Dado que un rol distinto del Responsable, el Delegado/Responsable interno o el Administrador consulta una tarea marcada con Nivel de confidencialidad Sensible o Muy sensible, cuando accede a su historial, entonces el sistema registra ese acceso de lectura como un evento propio del historial.
5. Dado que se exporta un reporte que incluye una tarea, cuando se exporta, entonces el sistema registra en el historial quien exporto, cuando y que reporte.
6. Dado que una Aprobacion se resuelve, cuando se resuelve, entonces el historial registra la Identidad del aprobador, la fecha y el Comentario de la decision de forma no editable.

**Reglas de negocio**

- Bitacora de solo escritura por adicion (append-only), sin funcion de edicion ni borrado para ningun rol (22_anti_features.md item 19).
- El Auditor (interno o externo) es siempre de solo lectura (seccion C).

- Referencia: MOD-021 secciones O, J, C; 22_anti_features.md item 19

### HU-021-14. Exportar el listado de tareas

**Como** Responsable Legal / Compliance, **quiero** exportar el listado de tareas con sus campos principales, **para** llevar un respaldo operativo fuera del sistema o entregarlo a una auditoria.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 6 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-021-04
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que tengo el permiso Exportar, cuando pido el listado de tareas, entonces el sistema genera el archivo en XLSX o CSV con Estado, Tipo de tarea, Responsable, Area, Fecha limite y Obligacion relacionada de cada tarea.
2. Dado que aplico filtros de Estado, Tipo, Responsable, Area o rango de fechas, cuando genero la exportacion, entonces el archivo solo incluye las tareas que cumplen esos filtros.
3. Dado que mi rol no tiene permiso de Exportar (por ejemplo Responsable de area o Usuario de consulta / Colaborador), cuando intento exportar, entonces el sistema deniega la accion.
4. Dado que genero una exportacion, cuando se genera, entonces el sistema registra en el historial de cada tarea incluida quien exporto, cuando y que reporte.
5. Dado que exporto tareas siendo Auditor externo (invitado), cuando genero la exportacion, entonces el sistema respeta el mismo acotamiento de acceso que tengo para verlas, sin incluir tareas que no puedo consultar.

**Reglas de negocio**

- El listado basico de tareas exportable en XLSX o CSV es la version minima de reportes de este modulo (seccion Q, justificacion de la fila Reportes exportables avanzados).
- Toda exportacion queda registrada en el historial (seccion O).

**Fuera de alcance**

- Reporte de tareas vencidas, historial de aprobaciones y paquete de tareas archivadas por cambio de regimen: reportes exportables avanzados, clasificacion SHOULD HAVE.

- Referencia: MOD-021 secciones N (fila Listado de tareas), C (Exportar), Q
- Notas: La tabla Q clasifica Reportes exportables avanzados como SHOULD HAVE, pero su propia columna de justificacion aclara que el listado basico de tareas en XLSX/CSV es MUST HAVE; esta HU cubre solo ese listado basico, sin filtros avanzados de aprobaciones ni paquetes archivados.

### HU-021-15. Alojar la tarea generica de cobertura parcial del Diagnostico

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** recibir en el Centro de Tareas una tarea generica cuando el Diagnostico detecte una senal que hoy no tiene modulo especializado propio, **para** dejar evidencia del pendiente mientras Transferencias Internacionales o Riesgos y EIPD no esten completos.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 7 | No |

- Fundamento: OBL-DOC-03 (Art. 4 (Medidas Organizativas, lit. e), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-TRANSF-01 (Art. 40, Ley para la Proteccion de Datos Personales)
- Depende de: HU-021-01
- Modulos requeridos: MOD-004

**Criterios de aceptacion**

1. Dado que el Diagnostico (MOD-004) marca datos fuera de El Salvador: si para un tratamiento, cuando dispara ese hecho, entonces el sistema crea una tarea con Modulo de origen MOD-004 para documentar la transferencia como evidencia suelta, dirigida al Responsable de area con copia a Responsable Legal/Compliance.
2. Dado que el Diagnostico detecta biometria, salud, menores de edad o camaras de seguridad sin una EIPD registrada, cuando dispara ese hecho, entonces el sistema crea una tarea de Tipo de tarea Riesgo/EIPD con el titulo Elaborar EIPD para el tratamiento, dirigida al Delegado/Responsable interno.
3. Dado que se crea cualquiera de estas dos tareas, cuando se crea, entonces queda con Evidencia requerida marcada como Documento adjunto y sin motor de deteccion automatica ni estados de flujo propios de Transferencias o de Riesgos/EIPD, solo el flujo generico de estados de la Tarea.
4. Dado que estas tareas existen mientras MOD-010 o MOD-014 completos no estan disponibles, cuando el Diagnostico se ejecuta de nuevo, entonces el mecanismo sigue creando la tarea generica sin bloquear la operacion del Diagnostico.
5. Dado que una de estas tareas se completa, cuando se marca Completada, entonces la evidencia adjunta queda disponible para el Centro de Evidencias (MOD-019) como evidencia suelta con aprobacion manual.

**Reglas de negocio**

- Mecanismo de cobertura parcial documentado en 19_21_roadmap_mvp_v1_v2.md 19.4: MOD-004 (disparo) + MOD-021 (tarea) + MOD-019 (evidencia suelta con aprobacion manual).
- MOD-021 no inventa un flujo de estados propio de Transferencias ni de Riesgos/EIPD: usa el flujo generico de la Tarea (seccion A, limites explicitos del modulo).

**Fuera de alcance**

- El flujo completo de Transferencias Internacionales (MOD-010) y de Riesgos y EIPD (MOD-014): ambos SHOULD HAVE, quedan fuera de esta epica.

- Requiere contenido: Plantilla generica de EIPD para llenado manual mientras MOD-014 no este completo (19_21_roadmap_mvp_v1_v2.md 19.4).; Plantilla de evidencia suelta para documentar una transferencia internacional mientras MOD-010 no este completo (19_21_roadmap_mvp_v1_v2.md 19.4).
- Referencia: 19_21_roadmap_mvp_v1_v2.md 19.4; 08b_workflows_casos_04_06.md (caso de transferencia de reaseguradora); MOD-021 seccion D.1 (Modulo de origen, Tipo de tarea)

### HU-021-16. Archivar una tarea como No aplica tras el cambio de regimen

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que las tareas exclusivas del regimen ACTUAL se archiven como No aplica cuando MOD-024 confirme el cambio de regimen, sin que se borren, **para** que mi historial refleje siempre las reglas vigentes en cada momento.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 35 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-021-03, HU-021-13
- Modulos requeridos: MOD-024

**Criterios de aceptacion**

1. Dado que MOD-024 activa la bandera regimen_reforma_659 a FUTURO, cuando el evento llega a MOD-021, entonces el sistema identifica las tareas activas de tipos exclusivos del regimen ACTUAL (por ejemplo reverificacion trienal del Delegado, informe semestral, comunicacion formal a la ACE) y las pasa al estado No aplica con confirmacion visible del Administrador.
2. Dado que una tarea pasa a No aplica, cuando pasa, entonces el sistema genera el Motivo de archivado autogenerado No aplica bajo el estado regulatorio actual, ver historial, con referencia al cambio de bandera de MOD-024, y ese motivo no es editable.
3. Dado que una tarea pasa a No aplica, cuando pasa, entonces el registro no se borra, y cualquier Aprobacion asociada conserva su historial tal como quedo, sin reabrirse ni recalcularse.
4. Dado que otra tarea tenia como Dependencia una tarea que paso a No aplica, cuando eso ocurre, entonces el sistema envia una alerta a su responsable para que decida si esa tarea tambien deja de aplicar o si necesita una tarea de reemplazo, sin automatizar esa decision.
5. Dado que un Administrador intenta marcar una tarea como No aplica por un motivo distinto del cambio de bandera de MOD-024, cuando lo intenta, entonces el sistema no lo permite de forma automatica y muestra el texto Requiere validacion de la organizacion o asesoria especializada, dejando esa decision fuera de esta transicion automatica.
6. Dado que la bandera regimen_reforma_659 vuelve a ACTUAL, cuando eso ocurre, entonces las tareas ya archivadas como No aplica no se reabren automaticamente ni se recalculan de forma retroactiva; su clasificacion historica queda preservada.

**Reglas de negocio**

- El paso a No aplica solo lo dispara, de forma automatica, el cambio de bandera regimen_reforma_659 de MOD-024, con confirmacion visible del Administrador; ningun otro motivo de No aplica se automatiza (secciones F.2 y H).
- Nunca se elimina una tarea ni su historial: solo se archiva o se marca No aplica (22_anti_features.md item 19).
- Ninguna alerta ni tarea relacionada con las obligaciones afectadas se recalcula retroactivamente (12_tareas_y_alertas.md 12.7, punto 8).

**Fuera de alcance**

- La activacion misma de la bandera regimen_reforma_659, que es capacidad de MOD-024.
- La creacion de la tarea Revisar el impacto del cambio de regimen normativo, ya cubierta por HU-021-01 (creacion desde evento de otro modulo).

- Preguntas pendientes relacionadas: PP-REG-01
- Referencia: MOD-021 secciones F.2, G, H, Q (fila Archivado automatico No aplica); 12_tareas_y_alertas.md 12.7
- Notas: La tabla Q clasifica esta fila como SHOULD HAVE, con cobertura minima en MVP (el campo de estado No aplica debe estar listo, pero el disparador automatico puede entregarse justo antes de activar la bandera en produccion); la version minima vendible de la seccion Q no la incluye. Se construye en R2 porque el regimen aun no cambio (bandera en ACTUAL, PP-REG-01 sin resolver) y porque el encargo especifico de esta epica pide cubrirla; ver notas_epica.

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Creacion, edicion y estados basicos de la Tarea (Pendiente, En proceso, Bloqueada, Completada) | HU-021-01, HU-021-02, HU-021-03, HU-021-04 |
| Fecha limite calculada a partir de MOD-023 (plazos legales) | HU-021-07 |
| Estado "En revision" y entidad Aprobacion, con bloqueo de autorrevision | HU-021-09, HU-021-10 |
| Alertas de tarea proxima a vencer y tarea vencida (niveles WARNING y HIGH) | HU-021-08, HU-021-11 |
| Escalamiento automatico de alertas criticas (72 horas de incidentes) | HU-021-12 |
| Historial inmutable de cambios de estado y comentarios | HU-021-06, HU-021-13 |
