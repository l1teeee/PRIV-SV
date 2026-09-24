# MODULO: Centro de Tareas

Codigo corto del modulo: MOD-021
Clasificacion global del modulo: MUST HAVE
Obligaciones que cubre: ninguna obligacion propia (ningun OBL-ID lo tiene como modulo propietario, por diseno: ver seccion A). Colaborador de OBL-INC-01, OBL-PLAZO-01, OBL-SANC-03, OBL-SANC-05, OBL-SANC-06 (colaboradoras declaradas en `mapa_modulos.json`; el modulo aloja la tarea con fecha y responsable, pero el fundamento juridico y el estado del expediente los define el modulo propietario correspondiente).

---

## A. Proposito

- **Por que existe.** Es el unico lugar del sistema donde una obligacion detectada, un paso de un flujo o un hallazgo de auditoria se convierte en una accion concreta: titulo, fundamento, responsable, fecha limite, dependencia, evidencia requerida y estado (`06_mapa_definitivo_de_modulos.md`, seccion 4, regla de conexion 1). Ningun otro modulo mantiene su propia lista de pendientes; todos escriben aqui.
- **Que problema resuelve para la empresa.** La persona designada (que normalmente no es abogada ni tiene un equipo de privacidad dedicado) necesita una sola bandeja de trabajo donde ver que le toca hacer, para cuando, con que respaldo legal y que evidencia debe dejar, sin tener que recorrer 20 modulos distintos para saber que esta pendiente. Sin este modulo, las obligaciones detectadas por el Diagnostico (MOD-004) o el Plan de Cumplimiento (MOD-005) quedarian como texto informativo, sin dueño ni fecha, y se perderian (riesgo identificado explicitamente en la tabla "que aportaria si faltara" del mapa definitivo).
- **Que obligacion u obligaciones cubre.** MOD-021 no es propietario de ninguna obligacion: es una regla de diseno explicita (seccion 2, principio 5, y seccion 4, regla 5 de `06_mapa_definitivo_de_modulos.md`) que los modulos transversales no posean obligaciones de negocio, salvo la unica excepcion real (MOD-023 Calendario, que si posee OBL-PLAZO-01 y OBL-PLAZO-02 por describir literalmente al motor de plazos). MOD-021 es colaborador de:
  - **OBL-INC-01** (Art. 25 LPDP, notificacion de vulneraciones de seguridad en un plazo maximo de 72 horas desde que se tuvo conocimiento; propietario MOD-013 Incidentes de Seguridad): MOD-021 crea y vigila la tarea "notificar la vulneracion a la ACE, la Fiscalia y los titulares", pero el fundamento, el contenido y el cierre del caso los gobierna MOD-013.
  - **OBL-PLAZO-01** (Art. 82 de la Ley de Procedimientos Administrativos, D.L. 856, aplicable de forma supletoria por el Art. 62 LPDP; regla de computo de dias y horas habiles; propietario MOD-023 Calendario y Motor de Plazos): MOD-021 nunca calcula el plazo por si mismo, siempre lo pide a MOD-023 y muestra la fecha limite resultante en cada tarea.
  - **OBL-SANC-03** (Art. 58 LPDP, medidas adicionales que la ACE puede ordenar tras una sancion firme; propietario MOD-024 Centro Regulatorio): MOD-021 aloja el plan de accion correctiva como una o varias tareas encadenadas.
  - **OBL-SANC-05** (Art. 21 de la Normativa para el Procedimiento Administrativo Sancionador de la ACE, contestacion del emplazamiento en 5 dias habiles; propietario MOD-024): MOD-021 aloja la tarea con el plazo ya calculado por MOD-023.
  - **OBL-SANC-06** (Art. 44 de la misma Normativa, pago de la multa en 15 dias habiles desde la notificacion de la resolucion; propietario MOD-024): MOD-021 aloja la tarea de pago y su evidencia (comprobante).
- **Que valor aporta.**
  - *Operativo*: una sola bandeja de trabajo por persona, con prioridad, fecha y dependencias visibles, en vez de que cada modulo tenga su propia lista dispersa.
  - *Probatorio*: cada tarea completada, con su evidencia adjunta y su historial de cambios, alimenta el principio de responsabilidad demostrada (OBL-PRIN-03, Art. 5 lit. i LPDP, propietario MOD-019 Centro de Evidencias); MOD-021 es la fuente donde se genera ese rastro dia a dia.
  - *Reduccion de riesgo*: ninguna obligacion detectada queda "flotando" sin dueño ni fecha, y toda tarea vencida es visible antes de convertirse en un incumplimiento silencioso.
- **Que NO hace este modulo (limites explicitos).**
  - No decide el fundamento legal de una tarea: lo hereda siempre del modulo de origen (MOD-004, MOD-005, MOD-011, MOD-013, MOD-002, MOD-014, MOD-018, MOD-024, etc.); MOD-021 nunca inventa ni reinterpreta una obligacion.
  - No calcula plazos habiles por si mismo: siempre consulta a MOD-023 Calendario y Motor de Plazos (regla de conexion 3 del mapa definitivo).
  - No envia notificaciones directamente al usuario: emite el evento y delega el envio a MOD-022 Notificaciones (regla de conexion 2).
  - No aprueba nada por si mismo: la Aprobacion siempre requiere una persona identificada con el rol que corresponda; el sistema nunca marca "Aprobada" una tarea de forma automatica.
  - No decide si la reforma 659 esta vigente: consulta la bandera unica de MOD-024 Centro Regulatorio (regla de conexion 4) y solo reacciona a ella.
  - No es un gestor de proyectos generico ni un CRM de tareas comerciales: solo aloja tareas ligadas a una obligacion, un flujo de cumplimiento o un hallazgo de auditoria, nunca tareas ajenas al programa de proteccion de datos (ver `22_anti_features.md`, item 1).

---

## B. Usuarios

Roles estandar segun `02_validacion/05_tipos_de_usuario.md`, seccion 5.3 (los 12 roles del sistema).

| Rol | Para que usa MOD-021 |
|---|---|
| Administrador de la organizacion | Ve todas las tareas de la organizacion, reasigna responsables, configura reglas de escalamiento y el umbral de separacion de funciones (seccion 5.4). No aprueba por defecto contenido juridico salvo que tambien ocupe el rol correspondiente. |
| Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | Recibe las tareas que la ley atribuye hoy al "delegado" (prevencion ARCO-POL, incompetencia, notificacion a receptores, revocacion, informes periodicos, comunicacion a la ACE); aprueba los actos que el sistema calculo o redacto antes de que se emitan. |
| Responsable ARCO-POL / Responsable del tramite | Ejecuta el dia a dia de las tareas de solicitudes de titulares dentro de los plazos calculados por MOD-023. |
| Responsable Legal / Compliance | Revisa y aprueba tareas que involucran una base juridica, un documento o una denegatoria; puede reasignar tareas legales entre areas. |
| Responsable de Seguridad / IT | Ejecuta y cierra las tareas del cronometro de 72 horas de un incidente y las tareas de controles de seguridad. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Ve y ejecuta unicamente las tareas que le fueron asignadas dentro de su area (por ejemplo, completar el RAT de un tratamiento nuevo o registrar un control). |
| Aprobador | Recibe tareas en estado "En revision" que requieren su aprobacion (documentos, cierres de incidente, EIPD, respuestas ARCO-POL sensibles, plan de accion correctiva sancionador) y decide aprobar o devolver con comentarios. |
| Auditor (interno) | Solo lectura: consulta el historial completo de tareas y aprobaciones como evidencia de gestion, sin poder crear, editar ni aprobar nada. |
| Auditor externo (invitado) | Acceso temporal de solo lectura al conjunto de tareas y su evidencia asociada durante una auditoria puntual, nunca a datos personales de titulares dentro de la tarea. |
| Usuario de consulta / Colaborador | Ve y completa unicamente las tareas puntuales que se le asignaron, sin visibilidad del resto del Centro de Tareas. |
| Titular (formulario externo) | No usa este modulo directamente; ve el estado de su propia solicitud a traves de MOD-011 (ARCO-POL), que internamente esta respaldado por tareas de MOD-021. |
| Asesor externo invitado | Recibe, por invitacion puntual y acotada, una tarea especifica (por ejemplo, opinar sobre una denegatoria compleja) sin visibilidad del resto de tareas de la organizacion. |

---

## C. Permisos

Convencion: "Si" = permitido por defecto; "Si*" = permitido solo sobre las tareas propias o asignadas; "No" = no permitido; "Doble control" = exige una segunda persona distinta de quien ejecuto la accion previa (ver `05_tipos_de_usuario.md`, seccion 5.4).

| Accion | Administrador | Delegado / Resp. interno | Resp. ARCO-POL | Legal/Compliance | Seguridad/IT | Responsable de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver | Si | Si | Si* | Si* | Si* | Si* | Si* | Si (solo lectura) | Si* (solo lectura, temporal) | Si* | Si* (acotado) |
| Crear tarea manual | Si | Si | Si* | Si | Si* | Si* | No | No | No | No | No |
| Modificar (titulo, fecha, responsable) | Si | Si* | Si* | Si* | Si* | Si* (solo campos no legales) | No | No | No | No | No |
| Cambiar de estado (iniciar, bloquear) | Si | Si* | Si* | Si* | Si* | Si* | No | No | No | Si* (solo su tarea) | No |
| Enviar a revision | Si | Si* | Si* | Si* | Si* | Si* | No | No | No | Si* | No |
| Aprobar (Approval) | Doble control | Si* (solo actos DPO) | No | Si* | No | No | Si* | No | No | No | Si* (solo el caso invitado) |
| Cerrar/completar | Si | Si* | Si* | Si* | Si* | Si* | No | No | No | Si* | No |
| Reabrir tarea completada | Si | Si* | No | Si* | No | No | No | No | No | No | No |
| Archivar como "no aplica" (cambio de regimen) | Solo automatico por MOD-024, con confirmacion de Administrador | No | No | No | No | No | No | No | No | No | No |
| Eliminar | No (solo archivar; ver `22_anti_features.md` item 19: el historial nunca se borra) | No | No | No | No | No | No | No | No | No | No |
| Exportar (reporte) | Si | Si* | Si* | Si* | Si* | No | No | Si | Si* | No | No |
| Asignar / reasignar | Si | Si* | Si* | Si* | Si* | No | No | No | No | No | No |
| Comentar | Si | Si | Si* | Si | Si* | Si* | Si* | No | No | Si* | Si* |
| Adjuntar evidencia | Si | Si | Si* | Si | Si* | Si* | Si* | No | No | Si* | Si* |

**Separacion de funciones.** Quien crea o ejecuta una tarea nunca puede aprobarla a si mismo cuando esa tarea tiene una Aprobacion asociada: el sistema bloquea la accion "Aprobar" si el usuario conectado es el mismo que dejo la tarea en "En revision", salvo en organizaciones por debajo del umbral configurable (propuesta inicial: 50 empleados, `05_tipos_de_usuario.md` seccion 5.4), donde se permite con una advertencia visible de "autorrevision". El rol Auditor (interno o externo) es siempre de solo lectura, nunca puede aprobar ni cerrar una tarea, para que su verificacion posterior sea independiente (misma seccion 5.4). Las aprobaciones que corresponden hoy al Delegado (prevencion, incompetencia, notificacion a receptores, revocacion) exigen doble control cuando la organizacion supera el umbral: quien redacto el borrador (el sistema o un colaborador) no es la misma persona investida como Delegado que lo aprueba.

---

## D. Informacion de entrada

MOD-021 administra dos entidades: **Tarea** (Task) y **Aprobacion** (Approval), coherentes con `06_mapa_definitivo_de_modulos.md`, seccion 7.

### D.1 Campos de la Tarea

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Titulo | Texto | Obligatorio siempre | Libre, sugerido por el modulo de origen | Maximo 140 caracteres | "Escriba en pocas palabras que hay que hacer, por ejemplo: 'Responder solicitud de acceso de Juan Perez'." | Buena practica (usabilidad, principio de transparencia Art. 5 lit. e) |
| Descripcion | Texto largo | Opcional al crear; obligatorio antes de pasar a "En revision" | Libre | Maximo 2000 caracteres | "Explique brevemente en que consiste la tarea, como si se la explicara a un companero nuevo." | Buena practica |
| Modulo de origen | Referencia a otra entidad | Obligatorio (autogenerado si la tarea nace de otro modulo) | Catalogo: MOD-002, MOD-004, MOD-005, MOD-006 (excepcional, ver nota de la seccion L), MOD-008, MOD-009, MOD-011, MOD-013, MOD-014, MOD-016, MOD-017, MOD-018, MOD-024, "Manual" (creada directamente en MOD-021) | Si el origen no es "Manual", el registro de origen debe existir | "Indica de donde salio esta tarea: por ejemplo, del Diagnostico o de una solicitud ARCO-POL." | Buena practica (trazabilidad) |
| Obligacion relacionada | Referencia a otra entidad (lista) | Opcional; obligatorio si el modulo de origen la trae | Lista de OBL-ID de `matriz_obligaciones.json` | Debe existir en la matriz; puede tener cero, uno o varios IDs (una tarea puede sustentar mas de una obligacion) | "Aqui vera el fundamento legal exacto (articulo y numero de obligacion) si esta tarea proviene de una exigencia de la ley." | OBL-ID correspondiente, mostrado como ayuda contextual, no en el lenguaje principal (regla de oro de la plantilla) |
| Tipo de tarea | Seleccion unica | Obligatorio | Catalogo: Diagnostico, Plan de cumplimiento, ARCO-POL, Incidente, Documento, Proveedor, Riesgo/EIPD, Retencion, Capacitacion, Auditoria, Delegado/Responsable interno, Procedimiento sancionador, Regulatorio (cambio de regimen), Otra (manual) | Debe coincidir con el modulo de origen | "Clasifica la tarea para poder filtrarla y para calcular los indicadores del panel." | Buena practica |
| Prioridad | Seleccion unica | Obligatorio | Baja, Media, Alta, Critica | Las tareas con plazo legal en curso de menos de 5 dias habiles se sugieren automaticamente como Alta o Critica (configurable) | "Que tan urgente es esta tarea. Las tareas con un plazo legal proximo a vencer se marcan automaticamente como prioritarias." | Buena practica |
| Responsable | Referencia a otra entidad (usuario) | Obligatorio antes de pasar a "En proceso" | Usuarios activos de la organizacion, filtrados por rol compatible con el tipo de tarea | Debe tener un rol habilitado para ese tipo de tarea (ver seccion C) | "Quien va a hacer el trabajo. Puede ser usted mismo o alguien de su equipo." | Buena practica |
| Area o unidad responsable | Referencia a otra entidad | Opcional (obligatorio en empresa mediana o corporativo con estructura de areas) | Catalogo de sucursales/areas de MOD-001 | Debe existir en MOD-001 | "A que area de la empresa pertenece esta tarea, si su organizacion tiene varias areas." | Buena practica |
| Fecha de creacion | Fecha | Obligatorio (autogenerado) | No aplica | No editable | "Cuando se genero esta tarea." | Buena practica (trazabilidad) |
| Fecha limite | Fecha | Obligatorio si la tarea tiene plazo legal o interno; opcional en tareas sin plazo | Calculada por MOD-023 cuando hay un plazo legal (por ejemplo, 20+20 dias habiles del Art. 20, 72 horas del Art. 25); editable manualmente solo en tareas sin plazo legal | No puede ser anterior a la fecha de creacion; si el plazo es legal, el campo se bloquea para edicion manual y solo MOD-023 puede recalcularlo | "Fecha limite para completar la tarea. Si esta fecha viene de un plazo legal, el sistema la calculo por usted y no se puede cambiar a mano." | OBL-PLAZO-01 (Art. 82 LPA supletorio) cuando la fecha proviene de un plazo legal |
| Criterio de computo mostrado | Texto (solo lectura, generado) | Automatico cuando la fecha limite proviene de un plazo ambiguo | "Dias habiles", "Horas corridas (criterio conservador)", "Horas habiles" | No aplica | "Le mostramos como se calculo el plazo, porque en algunos casos la ley no aclara si se cuenta en horas corridas u horas habiles." | OBL-PLAZO-01; nota de incertidumbre de `01_legal/03_hallazgos_regulatorios.md`, seccion 9, punto 1 |
| Dependencia (tarea previa) | Referencia a otra entidad (lista) | Opcional | Otras tareas de la misma organizacion | No puede crear un ciclo de dependencias | "Si esta tarea no puede empezar hasta que termine otra, enlacela aqui." | Buena practica |
| Evidencia requerida | Seleccion multiple | Obligatorio antes de pasar a "En revision" en tareas de tipo Incidente, ARCO-POL, Delegado o Procedimiento sancionador; opcional en el resto | Catalogo: Documento adjunto, Captura de pantalla, Comprobante de envio/notificacion, Comprobante de pago, Acta de aprobacion, Otro | Debe coincidir con al menos un archivo cargado antes de completar | "Que prueba necesita dejar de que hizo esto. Por ejemplo, el comprobante de haber enviado la respuesta al titular." | OBL-PRIN-03 (responsabilidad demostrada), a traves de MOD-019 |
| Archivos adjuntos | Archivo (lista) | Condicional (ver Evidencia requerida) | Tipos de archivo permitidos por politica de seguridad de la organizacion | Tamano maximo configurable; verificacion de tipo de archivo | "Adjunte aqui los archivos que sirven de evidencia de que completo la tarea." | OBL-PRIN-03, via MOD-019 |
| Comentarios | Texto largo (lista, tipo bitacora) | Opcional | Libre | Cada comentario queda con autor y fecha, no editable ni borrable | "Deje notas para usted o para quien reciba la tarea despues." | Buena practica (trazabilidad) |
| Estado | Seleccion unica | Obligatorio (autogenerado en "Pendiente" al crear) | Pendiente, En proceso, Bloqueada, En revision, Aprobada, Completada, Vencida, No aplica | Transiciones segun la tabla de la seccion F | "En que paso del proceso esta la tarea." | Buena practica |
| Motivo de bloqueo | Texto | Obligatorio si el estado es "Bloqueada" | Libre, con sugerencias: "Esperando informacion del titular", "Esperando respuesta del proveedor", "Esperando aprobacion de otra tarea" | No aplica | "Explique brevemente por que no puede avanzar esta tarea ahora." | Buena practica |
| Motivo de archivado ("no aplica") | Texto (autogenerado) | Obligatorio si el estado es "No aplica" | Generado por el sistema: "No aplica bajo el estado regulatorio actual, ver historial" mas la referencia al cambio de bandera de MOD-024 | No editable | "Esta tarea dejo de aplicar porque cambio el regimen legal del Delegado. Queda guardada, no se borra." | Seccion 5, punto 6 de `06_mapa_definitivo_de_modulos.md` |
| Es recurrente | Booleano | Obligatorio (por defecto "No") | Si / No | Si es "Si", exige el campo Periodicidad | "Marque esta opcion si esta tarea se repite (por ejemplo, la reverificacion del Delegado cada 3 anios)." | Buena practica; ejemplos concretos en `02_validacion_de_la_idea.md`, decision 2.7 puntos 2 y 3 (reverificacion cada 3 anios OBL-DPO-04, informes semestrales OBL-DPO-07) |
| Periodicidad | Seleccion unica | Obligatorio si Es recurrente = Si | Mensual, Trimestral, Semestral, Anual, Cada 3 anios, Personalizada | Debe tener una fecha base de referencia | "Cada cuanto se debe repetir esta tarea." | Buena practica |
| Nivel de confidencialidad | Seleccion unica | Obligatorio | Normal, Sensible (datos de titular involucrados), Muy sensible (datos de salud, biometricos o de menores) | Determina quien puede verla ademas del responsable y el rol correspondiente | "Marque si esta tarea involucra datos personales delicados, para limitar quien puede verla." | OBL-SENS-01 a OBL-SENS-08 (minimizacion y confidencialidad reforzada) |

**Campos precargados desde otros modulos.** Titulo, Descripcion, Modulo de origen, Obligacion relacionada, Tipo de tarea y, cuando aplica, Fecha limite (via MOD-023) llegan precargados desde el modulo que genera la tarea (por ejemplo, MOD-004 Diagnostico al detectar biometria, MOD-011 ARCO-POL al recibir una solicitud, MOD-013 Incidentes al abrir un caso). El Responsable sugerido se precarga segun el rol por defecto de ese tipo de tarea (por ejemplo, Responsable de Seguridad/IT para tareas de Incidentes), pero el Administrador o el propio responsable pueden reasignarla.

**Minimizacion de datos personales.** La Tarea nunca almacena el dato personal del titular en si (por ejemplo, no copia el contenido de una identificacion o un dato de salud): guarda una referencia al expediente correspondiente (por ejemplo, el numero de expediente ARCO-POL en MOD-011, o el numero de caso en MOD-013) y, cuando el proceso exige un adjunto puntual (por ejemplo, un comprobante de identidad dentro de un expediente ARCO-POL), ese adjunto vive en el expediente de origen y la Tarea solo referencia su existencia, nunca lo duplica. El campo "Nivel de confidencialidad" existe precisamente para no tratar por igual una tarea administrativa (por ejemplo, "actualizar el catalogo de sistemas") y una tarea que toca datos sensibles de un titular (por ejemplo, "resolver solicitud de cancelacion de datos de salud"), en linea con `22_anti_features.md`, item 23.

### D.2 Campos de la Aprobacion

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Tarea relacionada | Referencia a otra entidad | Obligatorio | Una Tarea en estado "En revision" | Debe existir y estar en el estado correcto | "A que tarea corresponde esta aprobacion." | Buena practica |
| Tipo de aprobacion | Seleccion unica | Obligatorio | Documento, Acto del Delegado/Responsable interno (prevencion, incompetencia, notificacion a receptores, revocacion), Cierre de incidente, Resultado de EIPD/riesgo, Respuesta ARCO-POL sensible, Plan de accion correctiva sancionador, Otra | Debe coincidir con el tipo de la Tarea | "Que tipo de decision se esta pidiendo aprobar." | Buena practica |
| Rol requerido | Seleccion unica | Obligatorio (autogenerado segun el tipo) | Delegado/Responsable interno, Legal/Compliance, Aprobador, Administrador (doble control) | Determina quien puede resolverla | "Que rol debe dar el visto bueno." | `05_tipos_de_usuario.md`, secciones 5.2 y 5.4 |
| Aprobador asignado | Referencia a otra entidad (usuario) | Obligatorio antes de notificar | Usuarios con el rol requerido | No puede coincidir con el usuario que dejo la tarea en "En revision" (salvo pyme bajo el umbral, con advertencia) | "Quien va a dar el visto bueno." | `05_tipos_de_usuario.md`, seccion 5.4 |
| Fecha de solicitud | Fecha (autogenerada) | Obligatorio | No aplica | No editable | "Cuando se pidio la aprobacion." | Buena practica |
| Fecha de resolucion | Fecha (autogenerada) | Obligatorio al resolver | No aplica | No editable | "Cuando se aprobo o se devolvio." | Buena practica |
| Decision | Seleccion unica | Obligatorio al resolver | Aprobada, Devuelta con cambios, Rechazada | No aplica | "El resultado de la revision." | Buena practica |
| Comentario de la decision | Texto largo | Obligatorio si la decision es "Devuelta" o "Rechazada"; opcional si es "Aprobada" | Libre | No aplica | "Explique por que devuelve o rechaza, para que quien hizo el trabajo sepa que corregir." | Buena practica |
| Identidad del aprobador | Texto (autogenerado) | Obligatorio (autogenerado) | Usuario autenticado que ejecuta la accion, con marca de fecha y hora | No editable | "Queda registrado quien aprobo, exactamente como si firmara." | OBL-PRIN-03, via MOD-019 |
| Version del objeto aprobado | Referencia a otra entidad | Obligatorio cuando el tipo es "Documento" | Version especifica del documento en MOD-008 | Debe existir esa version exacta | "Que version exacta del documento se aprobo, para no confundirla con una version posterior." | Buena practica (integridad de la evidencia) |

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Tarea creada | Registro completo de la seccion D.1 | Registro en el sistema, visible en pantalla | Al recibir un evento de un modulo de origen, o al crearla manualmente | Responsable asignado; visible para su area y para Administrador |
| Fecha limite calculada | Fecha exacta y criterio de computo usado (dias habiles, horas corridas, horas habiles) | Campo de la tarea, mas nota de ayuda visible | Al crear una tarea con plazo legal, y cada vez que MOD-023 actualiza su calendario de dias inhabiles | Responsable, Delegado/Responsable interno, Administrador |
| Evento "tarea proxima a vencer" / "tarea vencida" | Identificador de la tarea, dias restantes o dias de atraso, responsable | Evento interno entregado a MOD-022 | Segun las reglas de la seccion I | MOD-022 (que decide el canal y el destinatario final) |
| Aprobacion pendiente | Registro de la seccion D.2 | Registro en el sistema mas evento a MOD-022 | Al pasar una tarea a "En revision" con un tipo que requiere aprobacion | Aprobador asignado |
| Indicador "tareas pendientes / vencidas / completadas" | Conteos por estado, por tipo, por area y por responsable | Datos agregados consumidos por MOD-020 | Actualizacion continua | MOD-020 Dashboard y Reportes, con vista por rol |
| Evento de auditoria | Accion, usuario, fecha y hora, valor anterior y nuevo | Registro en el AuditLog transversal | En cada creacion, cambio de campo, cambio de estado, asignacion, aprobacion, adjunto o archivado | MOD-019 Centro de Evidencias (lectura), MOD-018 Auditoria de Cumplimiento |
| Reporte de tareas | Listado filtrable exportable | PDF, XLSX o CSV | Bajo demanda | Administrador, Delegado/Responsable interno, Legal/Compliance, Auditor |
| Tarea "revisar avisos publicados tras el cambio de regimen" | Tarea generada automaticamente cuando MOD-024 activa la bandera FUTURO | Registro estandar de tarea, tipo "Regulatorio" | Al activarse manualmente el cambio de regimen en MOD-024 | Delegado/Responsable interno, Legal/Compliance |
| Archivado "no aplica bajo el estado regulatorio actual" | Cambio de estado de una tarea existente, con nota explicativa, sin borrar el registro | Actualizacion de estado mas nota en el historial | Al activarse el cambio de regimen, sobre las tareas exclusivas del regimen anterior (por ejemplo, reverificacion trienal del Delegado) | Delegado/Responsable interno, Administrador, Auditor (como consulta historica) |

---

## F. Workflow

### F.1 Diagrama de estados de la Tarea

```
                         +-------------+
              +--------->|  PENDIENTE  |
              |          +------+------+
              |                 |
              | reapertura      | responsable inicia el trabajo
              |                 v
              |          +-------------+      falta un insumo      +-------------+
              |          | EN PROCESO  |-------------------------->|  BLOQUEADA  |
              |          +------+------+                           +------+------+
              |                 |                                          |
              |     listo para revision                     se resuelve el bloqueo
              |                 v                                          |
              |          +-------------+<---------------------------------+
              |          | EN REVISION |
              |          +------+------+
              |            /          \
              |   aprobador aprueba    aprobador devuelve o rechaza
              |          v                          \
              |   +-------------+                    v
              |   |  APROBADA   |             (regresa a EN PROCESO)
              |   +------+------+
              |          |
              |  se confirma evidencia final
              |          v
              |   +-------------+
              +---| COMPLETADA  |  (estado terminal, puede reabrirse)
                  +------+------+
                         |
          la obligacion deja de aplicar (cambio de regimen en MOD-024)
                         v
                  +-------------+
                  |  NO APLICA  |  (estado terminal archivado, nunca se borra)
                  +-------------+

Bandera paralela, no excluyente con los estados anteriores (salvo COMPLETADA y NO APLICA):
  si la fecha limite se cumple sin que la tarea llegue a COMPLETADA o NO APLICA,
  la tarea se marca visualmente VENCIDA (se muestra en rojo, sigue su flujo normal
  desde el estado en que estaba).
```

### F.2 Tabla de transiciones

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (no existe) | El modulo de origen dispara la creacion, o un usuario crea la tarea manualmente | Debe existir un Responsable sugerido o asignable | Pendiente | Sistema (automatico) o rol con permiso "Crear tarea manual" (seccion C) | Se calcula la fecha limite si hay plazo legal (via MOD-023); se registra evento de auditoria; se notifica al responsable (via MOD-022) |
| Pendiente | El responsable marca "iniciar" | Debe tener responsable y, si aplica, area asignada | En proceso | Responsable asignado, Administrador | Evento de auditoria; si la tarea tenia prioridad Critica, se refuerza la alerta (seccion I) |
| En proceso | El responsable marca "bloqueada" | Debe indicar Motivo de bloqueo | Bloqueada | Responsable asignado, su superior de area, Administrador | Se pausa el conteo de "tiempo activo" del indicador de dashboard; se notifica a quien depende de esta tarea (si otra tarea la tiene como dependencia) |
| Bloqueada | Se resuelve el impedimento | El usuario confirma que el impedimento ya no existe | En proceso | Responsable asignado, Administrador | Evento de auditoria; se reanuda el conteo de tiempo activo |
| En proceso | El responsable marca "lista para revision" | Debe tener Evidencia requerida cargada cuando el tipo de tarea la exige (seccion D.1); debe tener Descripcion completa | En revision | Responsable asignado | Se crea el registro de Aprobacion si el tipo de tarea lo requiere; se notifica al Aprobador asignado |
| En revision | El aprobador aprueba | El usuario que aprueba no puede ser el mismo que envio a revision (salvo pyme bajo el umbral, con advertencia) | Aprobada | Aprobador asignado (segun Rol requerido) | Se registra la Aprobacion con identidad y fecha; evento de auditoria |
| En revision | El aprobador devuelve con comentarios o rechaza | Debe registrar Comentario de la decision | En proceso | Aprobador asignado | Se notifica al responsable original con el motivo; evento de auditoria; el ciclo de revision puede repetirse las veces que sea necesario |
| Aprobada | El responsable o el sistema confirma que la evidencia final quedo registrada | Debe existir al menos un archivo o referencia de evidencia si el tipo de tarea lo exige | Completada | Responsable asignado, Administrador | Se cierra el conteo de tiempo; se envia evento a MOD-019 (evidencia) y a MOD-020 (indicador); evento de auditoria |
| Completada | Un usuario autorizado solicita reabrir, con justificacion | Debe registrar el motivo de reapertura como comentario | Pendiente (o En proceso, segun el motivo) | Administrador, Delegado/Responsable interno, Legal/Compliance (segun el tipo de tarea) | Evento de auditoria con el motivo; la version anterior de la evidencia se conserva, no se sobrescribe |
| Cualquier estado no terminal | MOD-024 activa el cambio de regimen y esta tarea pertenece a un paso exclusivo del regimen anterior | Regla configurada por tipo de tarea (por ejemplo, reverificacion trienal solo bajo regimen ACTUAL) | No aplica | Sistema (automatico), con confirmacion visible del Administrador | Se registra la nota "no aplica bajo el estado regulatorio actual, ver historial"; el registro nunca se borra (seccion 5, punto 6 del mapa definitivo) |
| Cualquier estado no terminal | La fecha limite se cumple sin llegar a Completada o No aplica | Automatico, no requiere accion humana | (se mantiene el estado, se agrega la bandera Vencida) | Sistema (automatico) | Se dispara la alerta de vencimiento (seccion I); el indicador de "tareas vencidas" del dashboard sube |

**Registros vinculados.** Cuando una Tarea pasa a "No aplica" o se archiva, cualquier Aprobacion asociada conserva su historial tal como quedo, sin reabrirse ni recalcularse; y cualquier otra tarea que la tuviera como dependencia recibe una alerta para que su responsable decida si tambien deja de aplicar o si necesita una tarea de reemplazo (esa decision no se automatiza, ver seccion H).

---

## G. Automatizaciones

Todas las reglas siguientes son configurables por la organizacion (activar/desactivar, ajustar umbrales de dias), salvo que se indique lo contrario.

| Disparador | Condicion | Accion |
|---|---|---|
| Un modulo de origen genera un hecho que exige una accion (por ejemplo, el Diagnostico detecta biometria, o ARCO-POL recibe una solicitud) | El hecho esta mapeado a una plantilla de tarea | Crear automaticamente la Tarea con los campos precargados de la seccion D.1 |
| La Tarea tiene un plazo legal asociado | El modulo de origen indica el articulo y el hito de inicio del computo | Pedir a MOD-023 el calculo de la fecha limite (dias u horas habiles segun corresponda) y mostrarla en la tarea, con el criterio de computo visible |
| Faltan N dias habiles (configurable) para la fecha limite de una tarea | La tarea no esta en Completada ni No aplica | Elevar la Prioridad a Alta o Critica (segun el umbral) y disparar la alerta correspondiente (seccion I) |
| Una tarea con plazo legal se marca Completada | El registro de evidencia esta presente | Actualizar el indicador de "cumplimiento de plazos operativos" del dashboard (MOD-020), sin usar la palabra "cumplimiento legal" |
| Una tarea pasa a En revision y su tipo requiere Aprobacion | El tipo de tarea esta en el catalogo de tipos que exigen aprobacion (documento, acto del Delegado, cierre de incidente, EIPD, ARCO-POL sensible, plan de accion sancionador) | Crear el registro de Aprobacion, asignar el Rol requerido y notificar al Aprobador (via MOD-022) |
| Una tarea recurrente (Es recurrente = Si) llega a Completada | Existe una Periodicidad configurada | Crear automaticamente la siguiente instancia de la tarea, con nueva fecha limite calculada a partir de la fecha base y la periodicidad |
| MOD-024 activa la bandera de regimen FUTURO | Existen tareas activas de tipos exclusivos del regimen ACTUAL (reverificacion trienal, informe semestral, comunicacion formal a la ACE) | Archivar esas tareas como "No aplica bajo el estado regulatorio actual, ver historial"; crear la tarea "Revisar avisos publicados tras el cambio de regimen" |
| Una tarea de tipo Documento pasa a Aprobada | El documento asociado en MOD-008 existe | Notificar a MOD-008 que la version aprobada puede publicarse (la publicacion misma la ejecuta una persona en MOD-008, no MOD-021) |
| Una tarea queda Bloqueada mas de N dias habiles (configurable) | La tarea no se desbloquea en ese plazo | Escalar la alerta al superior del responsable o al Administrador (seccion I) |
| Se cierra un incidente de seguridad en MOD-013 | El incidente tenia tareas asociadas en curso | Verificar que todas las tareas asociadas al incidente esten Completadas antes de permitir el cierre del expediente en MOD-013; si falta alguna, se muestra un bloqueo informativo |

---

## H. Decisiones que NO debe automatizar

- **Aprobar automaticamente una tarea sin intervencion humana**, sin importar cuan rutinaria parezca. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada." Razon: la Aprobacion existe precisamente para que una persona con el rol correspondiente revise antes de que un acto (documento, respuesta ARCO-POL, cierre de incidente) salga del sistema; automatizarla eliminaria el unico control humano previsto por diseno (ver `04_objetivo_exacto_del_producto.md`, seccion 1.2).
- **Decidir por si mismo si una tarea "ya no aplica" fuera del caso expresamente configurado del cambio de regimen 659.** Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada." Razon: solo el cambio de bandera de MOD-024, activado manualmente por el equipo del producto tras confirmar la publicacion oficial, puede disparar el archivado automatico; cualquier otro motivo de "ya no aplica" (por ejemplo, que la empresa dejo de tratar cierto tipo de dato) exige que una persona lo evalue y lo registre con su propio motivo.
- **Reasignar automaticamente una Aprobacion a otra persona cuando el aprobador original no responde**, mas alla de escalar la alerta. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada." Razon: reasignar quien aprueba un acto legal (por ejemplo, un acto atribuido hoy al Delegado) es una decision organizativa que le corresponde al Administrador o al propio Delegado, no un ajuste tecnico del sistema.
- **Calcular por si mismo un plazo legal sin pasar por MOD-023.** No es propiamente una decision "juridica" sino una regla de arquitectura, pero se lista aqui porque el riesgo de saltarsela es el mismo: dos calculos distintos para el mismo caso. MOD-021 siempre delega el computo a MOD-023 (regla de conexion 3 del mapa definitivo).
- **Decidir si la ambiguedad del plazo de 72 horas del Art. 25 (horas corridas u horas habiles) se resuelve de una forma u otra para un caso concreto.** Texto de advertencia: "La ley no precisa si este plazo se cuenta en horas corridas u horas habiles. El sistema aplica por defecto el criterio mas conservador (horas corridas). Verifique este criterio con asesoria legal si el caso es critico" (texto estandar de `04_objetivo_exacto_del_producto.md`, seccion 1.3). Razon: es una incertidumbre juridica documentada (`01_legal/03_hallazgos_regulatorios.md`, seccion 9, punto 1), no una decision tecnica.
- **Eliminar en forma definitiva una tarea o su historial**, incluso a pedido del Administrador. Texto de advertencia: "El historial de tareas no puede eliminarse; solo puede archivarse." Razon: el historial de tareas es parte de la evidencia de responsabilidad demostrada (OBL-PRIN-03) y del principio de no editar ni borrar la bitacora de auditoria (`22_anti_features.md`, item 19).
- **Decidir por si mismo la prioridad final de una tarea cuando dos plazos legales compiten por los mismos recursos** (por ejemplo, dos solicitudes ARCO-POL y un incidente de seguridad vencen la misma semana). El sistema sugiere prioridad segun cercania de la fecha limite, pero la decision final de a que dedicar el tiempo primero queda con el responsable o su superior.

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia o repeticion | Escalamiento (a quien y cuando) | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Tarea proxima a vencer | Faltan N dias habiles (configurable, por defecto 5 para plazos largos, 12 horas para plazos de 72 horas) para la fecha limite | WARNING | Responsable asignado | Plataforma + correo | Una vez al activarse el umbral, luego diaria hasta que cambie de estado o venza | A los 2 dias habiles (o 6 horas si el plazo es de 72 horas) sin avance, se copia al Delegado/Responsable interno o al superior de area | La tarea pasa a Completada o No aplica |
| Tarea vencida | La fecha limite se cumplio sin llegar a Completada ni No aplica | HIGH | Responsable asignado, Administrador | Plataforma + correo | Diaria mientras siga vencida | A las 24 horas de vencida sin actividad, escala a Delegado/Responsable interno y a Legal/Compliance | La tarea pasa a Completada o No aplica |
| Plazo critico de 72 horas de un incidente en curso | Restan menos de 12 horas para el vencimiento de la notificacion externa (OBL-INC-01) | CRITICAL | Responsable de Seguridad/IT, Delegado/Responsable interno | Plataforma + correo (mas canal adicional si la organizacion lo configura) | Cada 2 horas mientras el plazo siga corriendo | Inmediato al Administrador y a Legal/Compliance en cuanto se activa el nivel CRITICAL | La tarea de notificacion externa se marca Completada con evidencia de envio |
| Aprobacion pendiente por mas de N dias habiles (configurable, por defecto 3) | Una Aprobacion sigue sin decision | WARNING | Aprobador asignado | Plataforma + correo | Cada 2 dias habiles mientras siga pendiente | A los 5 dias habiles, se copia al Administrador | La Aprobacion se resuelve (Aprobada, Devuelta o Rechazada) |
| Tarea bloqueada por mas de N dias habiles (configurable, por defecto 5) | El estado se mantiene en Bloqueada mas alla del umbral | WARNING | Responsable asignado y su superior de area | Plataforma + correo | Semanal mientras siga bloqueada | A los 10 dias habiles, escala al Administrador | La tarea sale del estado Bloqueada |
| Tarea recurrente proxima a generarse | Faltan 15 dias (configurable) para la fecha base de la siguiente instancia (por ejemplo, reverificacion trienal del Delegado) | INFO | Delegado/Responsable interno, Administrador | Plataforma | Una vez | No aplica | Se genera la siguiente instancia de la tarea |
| Tareas archivadas por cambio de regimen | MOD-024 activa la bandera FUTURO y se archivan tareas exclusivas del regimen ACTUAL | INFO | Delegado/Responsable interno, Administrador | Plataforma + correo | Una vez por cada lote de archivado | No aplica | No aplica (es informativa) |

---

## J. Evidencia

MOD-021 no es propietario de ninguna obligacion, pero es donde se genera, dia a dia, buena parte de la evidencia que otros modulos (sobre todo MOD-019 Centro de Evidencias) exponen despues como prueba de responsabilidad demostrada (OBL-PRIN-03, Art. 5 lit. i LPDP).

- **Registro con fecha y hora de cada cambio de estado de una tarea**, con el usuario que lo ejecuto: prueba que existio una gestion activa, no solo una obligacion detectada y olvidada.
- **Registro de la Aprobacion con identidad del aprobador, fecha y comentario**: equivale a una firma dentro del sistema para actos que la ley atribuye hoy al Delegado (prevencion, incompetencia, notificacion a receptores, revocacion) y para cualquier documento u otro objeto que requiera visto bueno interno. Prueba OBL-PRIN-03 y, de forma indirecta, sostiene la evidencia de plazo de OBL-INC-01, OBL-SANC-05 y OBL-SANC-06 (que se cumplio a tiempo, con quien y con que respaldo).
- **Archivo adjunto con referencia de integridad** (verificable de forma independiente, segun el mecanismo que defina MOD-019 para todo el sistema): cada evidencia cargada en una tarea queda enlazada a esa verificacion, para que un paquete de evidencias exportado despues no pueda alegarse como alterado (`22_anti_features.md`, item 25).
- **Historial inmutable de comentarios**, sin edicion ni borrado, con autor y fecha: sirve como bitacora de coordinacion interna que tambien puede usarse como evidencia de buena fe (por ejemplo, ante la incertidumbre del "registro de banco de datos" del Art. 45, `01_legal/03_hallazgos_regulatorios.md`, seccion 8, punto 3, cuando la empresa documenta el intento de cumplimiento aunque la ACE no tenga canal habilitado).
- **Exportacion firmada o con hash**, delegada al mecanismo unico de integridad que expone MOD-019: MOD-021 no reinventa su propio formato de exportacion, entrega sus registros a MOD-019 para que el paquete de evidencias sea consistente en todo el sistema.
- **Tiempo de conservacion.** El historial de tareas y aprobaciones sigue la regla de conservacion documental de cumplimiento propio de MOD-016 Retencion y Eliminacion (expedientes relacionados con ARCO-POL o incidentes: 5 anios; avisos y politicas: 10 anios, segun la clasificacion del objeto que la tarea sustenta). MOD-021 nunca elimina su propio historial de forma independiente: solo lo archiva o lo marca "No aplica", nunca lo borra (`22_anti_features.md`, item 19).

---

## K. Documentos asociados

- **Documentos requeridos como entrada.** MOD-021 no exige documentos propios para crear una tarea: los documentos (contrato con un proveedor, borrador de un aviso, expediente ARCO-POL) viven en su modulo de origen (MOD-008, MOD-009, MOD-011) y la tarea solo los referencia.
- **Documentos generados.**
  - Acta de aprobacion (registro interno, no un PDF separado por defecto): resume la decision, quien la tomo y cuando, generada a partir del registro de Aprobacion.
  - Reporte de tareas (ver seccion N).
  - Nota automatica "Tareas archivadas por cambio de regimen", que enumera cada tarea afectada y el motivo (ver seccion E).
- **Plantillas que el sistema provee.**
  - Plantilla de tarea por tipo (por ejemplo, "Responder solicitud ARCO-POL", "Notificar vulneracion de seguridad", "Renovar contrato de encargado"), con campos precargados y evidencia requerida sugerida segun el tipo. Requiere validacion de la organizacion antes de usarse tal cual, porque el contenido de la descripcion es un punto de partida, no un texto legal cerrado.
  - Plantilla de plan de accion correctiva sancionador (para OBL-SANC-03), con las tareas encadenadas sugeridas (contestar emplazamiento, adjuntar prueba, pagar multa si corresponde, ejecutar medida ordenada). Requiere validacion de asesoria especializada, dado que deriva de una resolucion de la ACE.
- **Anexos y evidencias documentales.** Los archivos adjuntos de la seccion D.1 (comprobantes de envio, comprobantes de pago, capturas, actas) quedan enlazados a la tarea y disponibles para exportacion via MOD-019.

---

## L. Dependencias

### L.1 Diagrama

```
   MOD-002 Delegado         MOD-004 Diagnostico       MOD-005 Plan de Cumplimiento
        |                          |                           |
        |                          |                           |
   MOD-011 ARCO-POL          MOD-013 Incidentes         MOD-014 Riesgos/EIPD
        |                          |                           |
        |                          |                           |
   MOD-018 Auditoria -------> MOD-021 CENTRO DE TAREAS <------- MOD-024 Regulatorio
                                    |        ^                  (bandera de regimen)
                                    |        |
                          consulta plazos    | consulta identidad/estructura
                                    |        |
                                    v        |
                            MOD-023 Calendario y Motor de Plazos
                                    |
                                    v
                       MOD-022 Notificaciones (recibe eventos)
                                    |
                                    v
                       MOD-020 Dashboard y Reportes (recibe indicadores)
```

### L.2 Lista de dependencias

**Entra desde (crean o alimentan tareas):** MOD-002 (Delegado / Responsable Interno: reverificacion, informes, comunicacion a la ACE), MOD-004 (Diagnostico: tareas iniciales tras cada respuesta que dispara obligacion), MOD-005 (Plan de Cumplimiento: acciones criticas/importantes/recomendadas), MOD-011 (ARCO-POL: prevencion, respuesta, notificacion a receptores), MOD-013 (Incidentes: cronometro de 72 horas y pasos del ciclo del incidente), MOD-014 (Riesgos/EIPD: tarea "elaborar EIPD" cuando el diagnostico detecta un disparador de riesgo), MOD-018 (Auditoria de Cumplimiento: plan de accion tras hallazgos de la auditoria anual), MOD-024 (Centro Regulatorio: tareas derivadas de la activacion de la bandera de regimen y del procedimiento sancionador).

**Consulta (servicios, no crea tareas por si mismo):** MOD-023 (Calendario y Motor de Plazos, para toda fecha limite con plazo legal), MOD-024 (Centro Regulatorio, para saber si el regimen vigente es ACTUAL o FUTURO antes de decidir que tareas archivar), MOD-001 (Organizacion y Personas, para el catalogo de usuarios, roles y areas).

**Sale hacia:** MOD-022 (Notificaciones, que recibe los eventos de la seccion I y decide el canal final), MOD-023 (Calendario, al que le pide cada calculo de plazo), MOD-020 (Dashboard y Reportes, que recibe los indicadores agregados de la seccion M).

**Que ocurre si un modulo dependiente no existe en el MVP.** Todos los modulos que crean tareas hacia MOD-021 (MOD-002, MOD-004, MOD-005, MOD-011, MOD-013, MOD-024) son MUST HAVE del MVP, de modo que este riesgo no aplica en el MVP. MOD-014 (Riesgos/EIPD) y MOD-018 (Auditoria de Cumplimiento) son SHOULD HAVE con cobertura parcial documentada en `06_mapa_definitivo_de_modulos.md`: mientras no tengan su version completa, generan igualmente una tarea manual simplificada en MOD-021 (por ejemplo, "elaborar EIPD" con plantilla generica), de modo que el Centro de Tareas nunca depende de que esos dos modulos esten completos para funcionar.

**Nota de desacuerdo con el mapa (a reportar, no corregido unilateralmente aqui).** La lista `depende_de` de MOD-021 en `mapa_modulos.json` solo declara `["MOD-004", "MOD-005", "MOD-011", "MOD-013", "MOD-002"]`. Sin embargo, al revisar la ficha resumida de cada modulo en `06_mapa_definitivo_de_modulos.md` (seccion 3), tanto MOD-014 Riesgos y EIPD (linea 282: "Sale hacia MOD-015, MOD-019, MOD-021") como MOD-018 Auditoria de Cumplimiento (linea 322: "Sale hacia MOD-019, MOD-020, MOD-021") declaran explicitamente que entregan tareas a MOD-021, y la propia ficha de MOD-021 en ese documento dice en su proposito que esta "alimentado por Diagnostico, ARCO-POL, Incidentes, Proveedores, Riesgos, Documentos y Auditoria" (linea 345), una lista mas amplia que la de `mapa_modulos.json` y que tampoco coincide del todo con las declaraciones "Sale hacia" de cada modulo individual (por ejemplo, MOD-009 Proveedores y MOD-008 Documentos no declaran "Sale hacia MOD-021" en sus propias fichas, pese a estar mencionados en el proposito de MOD-021). La regla de conexion 1 de la seccion 4 del mismo documento ("todo modulo de recorrido que genera trabajo crea tareas alli") sugiere ademas que, en algun momento, modulos como MOD-008 (revision de documentos antes de vencer), MOD-009 (renovacion de contratos con proveedores) y MOD-016 (aprobacion de eliminacion por retencion) tambien deberian declarar esta relacion de forma explicita. Esta ficha modela MOD-021 conforme al principio general de la regla de conexion 1 (cualquier modulo operativo puede crear una tarea aqui, ver el catalogo del campo "Modulo de origen" en la seccion D.1), pero se deja constancia de que el campo `depende_de` de `mapa_modulos.json` para MOD-021 esta incompleto frente a las propias fichas de MOD-014 y MOD-018, y de que la prosa de la ficha resumida de MOD-021 no coincide en su totalidad con las relaciones declaradas modulo por modulo. Se recomienda a quien consolide el mapa final actualizar `depende_de` de MOD-021 para incluir al menos MOD-014 y MOD-018.

---

## M. Dashboard

Todos los indicadores se expresan como estado del programa (tareas, plazos, evidencia), nunca como porcentaje de cumplimiento legal (`04_objetivo_exacto_del_producto.md`, seccion 1.2).

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Tareas pendientes | Conteo de tareas en Pendiente + En proceso + Bloqueada | Verde si esta bajo el promedio historico de la organizacion; amarillo si sube; rojo si supera el umbral configurado | Responsable (las suyas), Gerencia (total de la organizacion), Legal (por tipo de tarea) |
| Tareas vencidas | Conteo de tareas con bandera Vencida activa | Rojo si mayor a 0, amarillo si son de prioridad Baja/Media unicamente | Gerencia, Responsable, Legal, Auditor |
| Aprobaciones pendientes | Conteo de Aprobaciones sin Decision, agrupadas por dias en espera | Amarillo si hay alguna con mas de 3 dias habiles, rojo si hay alguna con mas de 5 | Aprobador, Delegado/Responsable interno, Gerencia |
| Tiempo promedio de cierre por tipo de tarea | Promedio de dias entre Fecha de creacion y Fecha de Completada, por Tipo de tarea | Sin semaforo (indicador de tendencia) | Legal, Gerencia |
| Cumplimiento de plazos operativos con plazo legal | Porcentaje de tareas con plazo legal completadas dentro de la fecha limite (metrica de producto, ver `04_objetivo_exacto_del_producto.md`) | Verde >= 95%, amarillo 80 a 94%, rojo < 80% | Gerencia, Legal, Auditor |
| Tareas archivadas por cambio de regimen | Conteo acumulado desde la activacion de la bandera FUTURO | Informativo, sin semaforo | Delegado/Responsable interno, Legal, Auditor |
| Carga de trabajo por responsable | Conteo de tareas activas por usuario | Amarillo si un usuario concentra mas del umbral configurado de tareas activas | Administrador, Gerencia |

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Listado de tareas | Todas las tareas con sus campos principales | Estado, tipo, responsable, area, rango de fechas, obligacion relacionada | XLSX, CSV | Administrador, Delegado/Responsable interno, Legal/Compliance | Si, como respaldo operativo |
| Tareas vencidas | Tareas con bandera Vencida activa o historica, con dias de atraso | Rango de fechas, tipo, area | XLSX, PDF | Gerencia, Auditor | Si |
| Historial de una tarea especifica | Linea de tiempo completa: creacion, cambios de estado, comentarios, adjuntos, aprobacion | Una tarea puntual | PDF | Auditor, Auditor externo, Legal/Compliance | Si, es el insumo principal para demostrar una obligacion puntual |
| Historial de aprobaciones | Todas las Aprobaciones resueltas, con identidad del aprobador y fecha | Rango de fechas, tipo de aprobacion, rol | XLSX, PDF | Auditor, Auditor externo, Delegado/Responsable interno | Si |
| Carga de trabajo por area o responsable | Conteo de tareas activas, completadas y vencidas por persona o area | Rango de fechas, area | XLSX | Gerencia, Administrador | No (uso interno de gestion) |
| Paquete de tareas archivadas por cambio de regimen | Listado completo de tareas marcadas "No aplica" tras el cambio de bandera, con motivo | Rango de fechas | ZIP (incluye PDF resumen mas anexos) | Delegado/Responsable interno, Auditor | Si, para demostrar trazabilidad del cambio de regimen |

---

## O. Historial

Eventos que quedan en el historial de cada Tarea y de cada Aprobacion, y que se replican en el AuditLog transversal:

- Creacion de la tarea (usuario o modulo de origen, fecha y hora, campos iniciales).
- Cada cambio de campo relevante (valor anterior y nuevo): Responsable, Fecha limite, Prioridad, Estado, Area.
- Cada cambio de estado, con el usuario que lo ejecuto y la fecha y hora exacta.
- Asignaciones y reasignaciones de Responsable.
- Solicitud de Aprobacion y su resolucion (Aprobada, Devuelta, Rechazada), con identidad del aprobador.
- Adjuntos cargados o eliminados (el sistema no permite eliminar un adjunto que ya forma parte de una tarea Completada; solo se pueden agregar versiones nuevas, la anterior se conserva).
- Comentarios agregados (no editables ni borrables).
- Exportaciones de reportes que incluyen esta tarea (quien exporto, cuando, que reporte).
- Accesos de lectura a tareas marcadas con Nivel de confidencialidad "Sensible" o "Muy sensible" por un rol distinto del Responsable, el Delegado/Responsable interno o el Administrador (por ejemplo, un Auditor externo consultando el historial durante una auditoria).
- Archivado como "No aplica" (motivo, fecha, referencia al cambio de bandera de MOD-024).
- Reapertura de una tarea Completada (motivo, usuario, fecha).

---

## P. Riesgos

- **Riesgo legal: dar por resuelta una obligacion solo porque la tarea esta Completada.** Una tarea marcada Completada no equivale a que la decision juridica de fondo sea correcta (por ejemplo, que la base juridica elegida sea defendible). *Mitigacion de diseno*: el estado de la tarea nunca se traduce en el dashboard como "obligacion cumplida", sino como "tarea completada, con evidencia disponible"; los textos de descargo de `04_objetivo_exacto_del_producto.md` (seccion 1.3) se muestran junto a cada indicador relacionado con tareas legales.
- **Riesgo legal: usar la fecha limite calculada como si fuera la unica interpretacion correcta del plazo.** Sobre todo en el plazo de 72 horas del Art. 25, donde existe una ambiguedad documentada (horas corridas u horas habiles). *Mitigacion de diseno*: el "criterio de computo mostrado" (seccion D.1) siempre es visible en la tarea, con el texto de advertencia estandar de la seccion H.
- **Riesgo de UX: sobrecarga de tareas para una persona que ocupa varios roles a la vez (tipico en pyme).** Karla, del perfil pyme de `05_tipos_de_usuario.md`, puede terminar viendo decenas de tareas de tipos muy distintos en una sola bandeja. *Mitigacion de diseno*: vista "Mis tareas de hoy" priorizada por fecha limite y prioridad, agrupacion por tipo, y la posibilidad de posponer tareas sin plazo legal sin que eso oculte las que si lo tienen.
- **Riesgo de UX: abandono del flujo de aprobacion por fricción excesiva.** Si cada documento menor exige el mismo nivel de aprobacion que un acto legal del Delegado, el usuario puede empezar a aprobar sin leer. *Mitigacion de diseno*: el catalogo de "Tipo de aprobacion" distingue actos de alto impacto legal (que siempre exigen revision detallada) de aprobaciones administrativas menores, y el sistema no permite "aprobar en lote" actos del tipo Delegado/Responsable interno o respuestas ARCO-POL sensibles.
- **Riesgo operativo: fechas limite mal calculadas por un calendario de dias inhabiles desactualizado en MOD-023.** Como MOD-021 nunca calcula el plazo por si mismo, hereda cualquier error del calendario compartido. *Mitigacion de diseno*: MOD-021 muestra siempre la fecha de origen del calculo (version del calendario usada) para que un error se pueda auditar y corregir de forma centralizada en MOD-023, sin tener que revisar tarea por tarea.
- **Riesgo operativo: dependencias circulares entre tareas que bloquean el flujo sin que nadie lo note.** *Mitigacion de diseno*: la validacion de la seccion D.1 impide crear una dependencia que forme un ciclo; el sistema advierte antes de guardar.
- **Riesgo de seguridad y privacidad: exposicion de datos del titular dentro de una tarea.** Por ejemplo, si un responsable pega el DUI completo de un titular en la Descripcion de una tarea de ARCO-POL en lugar de referenciarlo desde el expediente de MOD-011. *Mitigacion de diseno*: el campo Nivel de confidencialidad activa una advertencia visible al crear o editar una tarea marcada Sensible o Muy sensible, recordando no copiar datos personales dentro del texto libre y usar siempre la referencia al expediente de origen; el acceso a esas tareas queda restringido y su lectura por un rol no habitual queda registrada en el historial (seccion O).
- **Riesgo de seguridad: que un usuario se apruebe a si mismo un acto que deberia revisar otra persona.** *Mitigacion de diseno*: bloqueo tecnico de autorrevision (seccion C), salvo bajo el umbral configurable de pyme, siempre con advertencia visible.

---

## Q. MVP

| Funcionalidad del modulo | Clasificacion | Justificacion |
|---|---|---|
| Creacion, edicion y estados basicos de la Tarea (Pendiente, En proceso, Bloqueada, Completada) | MUST HAVE | Condicion (b) del test de tres condiciones del mapa definitivo: sin esto, ningun otro modulo MUST HAVE (MOD-004, MOD-005, MOD-011, MOD-013, MOD-002) puede operar. |
| Fecha limite calculada a partir de MOD-023 (plazos legales) | MUST HAVE | Es la instrumentacion directa de los plazos ya en curso (20+20 dias, 72 horas, 10 dias de prevencion, 15 dias del Delegado); sin fecha limite calculada, el producto no cumple su promesa central. |
| Estado "En revision" y entidad Aprobacion, con bloqueo de autorrevision | MUST HAVE | Los actos atribuidos hoy al Delegado (prevencion, incompetencia, notificacion a receptores, revocacion) exigen aprobacion explicita desde el primer dia (`04_objetivo_exacto_del_producto.md`, seccion 1.2); sin esto, el sistema estaria emitiendo actos legales sin control humano, contra el principio central del producto. |
| Alertas de tarea proxima a vencer y tarea vencida (niveles WARNING y HIGH) | MUST HAVE | Es la unica forma de que los plazos legales no dependan de que alguien recuerde entrar a mirar (riesgo explicito de la tabla de la seccion 4 del mapa definitivo). |
| Escalamiento automatico de alertas criticas (72 horas de incidentes) | MUST HAVE | El plazo mas critico y visible del corpus legal (Art. 25); un escalamiento tardio puede convertir una infraccion leve en una omitida por completo. |
| Historial inmutable de cambios de estado y comentarios | MUST HAVE | Es la base minima de evidencia de responsabilidad demostrada (OBL-PRIN-03) desde el primer dia. |
| Tareas recurrentes con periodicidad configurable | SHOULD HAVE | Util desde el inicio (reverificacion trienal, informes semestrales del Delegado), pero el mismo resultado puede lograrse en el MVP creando manualmente la siguiente instancia; no es dependencia estructural de otro MUST HAVE. |
| Archivado automatico "No aplica" por cambio de regimen 659 | SHOULD HAVE, con cobertura minima en MVP | El disparador (la bandera de MOD-024) es MUST HAVE por si mismo, pero mientras la reforma no se publique, esta automatizacion no se ejercita; el MVP debe tener el campo de estado "No aplica" listo, aunque el disparador automatico pueda entregarse justo antes de que la bandera se active en produccion. |
| Reportes exportables avanzados (historial de aprobaciones, paquete de tareas archivadas) | SHOULD HAVE | El listado basico de tareas (XLSX/CSV) es MUST HAVE; los reportes mas elaborados pueden esperar a la primera necesidad real de auditoria. |
| Dependencias entre tareas con validacion de ciclos | SHOULD HAVE | Mejora la calidad del plan de trabajo, pero una version inicial puede operar sin bloquear dependencias, solo mostrandolas como texto libre. |
| Vista tipo tablero (kanban) o calendario visual de tareas | COULD HAVE | Mejora de experiencia sobre la misma informacion que ya existe en la lista y el dashboard; no aporta una capacidad nueva. |
| Checklist de subtareas dentro de una tarea | COULD HAVE | Util para tareas complejas (por ejemplo, un plan de accion sancionador con varios pasos), pero se puede resolver en el MVP con varias tareas encadenadas por Dependencia. |
| Reglas de SLA distintas por tipo de obligacion, configurables por la empresa | COULD HAVE | Los umbrales por defecto (5 dias habiles, 12 horas, etc.) cubren el caso general; la personalizacion fina es una mejora posterior. |
| Vista consolidada de tareas entre varias sociedades de un mismo grupo corporativo | FUTURE | Coincide con la decision 2.7.31 de `02_validacion_de_la_idea.md`: la vision consolidada multi-sociedad es funcionalidad V1/Enterprise, no MVP. |
| Integraciones de notificacion con Teams, Slack, SMS o WhatsApp para tareas | FUTURE | Depende de que MOD-022 incorpore esos canales; el MVP de MOD-022 solo cubre plataforma y correo. |
| Reasignacion automatica de tareas por balanceo de carga entre responsables | FUTURE | Es una optimizacion de gestion de equipo, no una necesidad del cumplimiento legal ni una dependencia estructural de otro modulo. |

**Version minima vendible del modulo.** La version minima que ya puede venderse incluye: creacion y estados basicos de la Tarea, fecha limite calculada por MOD-023, la entidad Aprobacion con bloqueo de autorrevision, las alertas de vencimiento con escalamiento para el caso critico de 72 horas, y el historial inmutable. Esta combinacion ya resuelve el problema central del producto (que una obligacion detectada se convierta en una accion con responsable, fecha y control humano) y es la unica forma de que MOD-004, MOD-005, MOD-011, MOD-013 y MOD-002 -todos MUST HAVE- puedan operar como fueron disenados.

---

## R. Ayuda contextual (complemento obligatorio)

**1. Que es una tarea**
- *Que es*: una accion concreta, con un responsable y una fecha, que representa algo que su empresa debe hacer para proteger los datos personales que maneja.
- *Por que tengo que hacer esto*: porque cada obligacion de la ley, si no se convierte en una accion con dueño y fecha, tiende a quedarse en el olvido.
- *Fundamento*: principio de responsabilidad demostrada, Art. 5 lit. i LPDP (OBL-PRIN-03); el fundamento especifico de cada tarea se muestra en el campo "Obligacion relacionada".
- *Cuando necesito ayuda juridica*: cuando no entienda por que una tarea es obligatoria o que pasa si no la completa a tiempo, especialmente si tiene un plazo legal.

**2. Que es una aprobacion**
- *Que es*: el visto bueno formal de una persona autorizada (por ejemplo, el Delegado de Proteccion de Datos) antes de que algo salga del sistema: un documento, una respuesta a un titular, el cierre de un incidente.
- *Por que tengo que hacer esto*: porque la ley atribuye ciertas decisiones a una persona especifica, y el sistema nunca decide ni emite nada en su lugar.
- *Fundamento*: Arts. 15, 17, 18, 19, 21 y 30 LPDP (funciones atribuidas hoy al Delegado, mientras el regimen ACTUAL este vigente); Art. 5 lit. i (responsabilidad demostrada).
- *Cuando necesito ayuda juridica*: cuando la aprobacion implica elegir una base juridica, redactar una denegatoria o decidir el contenido de una notificacion a la ACE.

**3. Que significa que una tarea este vencida**
- *Que es*: la fecha limite calculada para esa tarea ya paso y la tarea no se completo ni se archivo.
- *Por que tengo que hacer esto*: porque un plazo vencido sin gestion puede convertirse en una infraccion sancionable (por ejemplo, no notificar una vulneracion dentro de las 72 horas).
- *Fundamento*: depende de la tarea; por ejemplo, Art. 25 LPDP y OBL-INC-01 para incidentes, Art. 20 LPDP y OBL-ARCO-10 para solicitudes ARCO-POL.
- *Cuando necesito ayuda juridica*: si una tarea con plazo legal ya vencio y no sabe que consecuencia tiene, consulte de inmediato al Delegado/Responsable interno o a asesoria especializada; el sistema no puede decirle si esa demora ya configura una infraccion.

**4. Que es el motor de plazos (por que la fecha no se puede editar a mano)**
- *Que es*: el servicio unico (MOD-023) que calcula cada fecha limite en dias u horas habiles, considerando fines de semana y dias no laborables.
- *Por que tengo que hacer esto*: para que todas las tareas de la empresa calculen el mismo plazo de la misma forma, sin que cada persona haga su propia cuenta.
- *Fundamento*: Art. 82 de la Ley de Procedimientos Administrativos (D.L. 856), aplicable de forma supletoria por el Art. 62 LPDP (OBL-PLAZO-01).
- *Cuando necesito ayuda juridica*: si tiene dudas sobre si un plazo se cuenta en dias corridos u habiles, o en horas corridas u horas habiles, en un caso donde la ley no es clara (por ejemplo, las 72 horas del Art. 25).

**5. Que pasa cuando cambia el regimen del Delegado (reforma 659)**
- *Que es*: si la reforma legislativa aprobada en septiembre de 2026 se publica oficialmente y entra en vigencia, algunas tareas dejan de ser obligatorias bajo el nuevo regimen y se archivan como "No aplica bajo el estado regulatorio actual, ver historial", sin borrarse.
- *Por que tengo que hacer esto*: para que su historial refleje siempre las reglas que estaban vigentes en cada momento, sin reescribir el pasado.
- *Fundamento*: Decreto Legislativo 659 (numero pendiente de confirmar contra el texto oficial), aprobado el 17 de septiembre de 2026, publicacion en el Diario Oficial pendiente de confirmar al 24 de septiembre de 2026; mientras tanto aplica el regimen vigente de los Arts. 15 y 17 del Decreto 144.
- *Cuando necesito ayuda juridica*: siempre que el sistema le muestre un cambio de regimen; verifique con su Delegado/Responsable interno o con asesoria especializada si su empresa debe actuar de inmediato o puede esperar la confirmacion oficial.

**6. Diferencia entre una tarea y una evidencia**
- *Que es*: la tarea es la accion que se hizo o se esta haciendo; la evidencia es la prueba de que se hizo (un archivo, un comprobante, una aprobacion registrada). Una tarea puede estar completada y aun asi carecer de evidencia suficiente si no se adjunto nada.
- *Por que tengo que hacer esto*: porque ante la ACE o una auditoria, lo que cuenta no es solo haber hecho el trabajo, sino poder demostrarlo.
- *Fundamento*: Art. 5 lit. i LPDP, principio de responsabilidad demostrada (OBL-PRIN-03).
- *Cuando necesito ayuda juridica*: si no esta seguro de que tipo de evidencia es suficiente para una obligacion especifica (por ejemplo, cuanto detalle debe tener el comprobante de notificacion de una vulneracion).

---

## Nota final del agente (desacuerdos y observaciones sobre las fuentes de diseno)

1. **Inconsistencia en `depende_de` de MOD-021 dentro de `mapa_modulos.json`.** Ya detallada en la seccion L.2: el campo solo lista `MOD-004, MOD-005, MOD-011, MOD-013, MOD-002`, pero las fichas individuales de MOD-014 (Riesgos y EIPD) y MOD-018 (Auditoria de Cumplimiento) en `06_mapa_definitivo_de_modulos.md` declaran explicitamente "Sale hacia... MOD-021". Se recomienda corregir `depende_de` de MOD-021 para incluir al menos esas dos entradas, o bien aclarar en el mapa que esa asimetria es intencional (lo cual, a diferencia del caso de MOD-001/MOD-023/MOD-024 explicado en la seccion 6.1 del mismo documento, no esta declarado como excepcion para MOD-014 ni MOD-018).
2. **La prosa del proposito de MOD-021 en `06_mapa_definitivo_de_modulos.md` (linea 345) menciona "Proveedores" y "Documentos" como fuentes que alimentan al Centro de Tareas**, pero ni MOD-009 (Proveedores y Encargados) ni MOD-008 (Documentos y Politicas) declaran "Sale hacia MOD-021" en sus propias fichas de la seccion 3 del mismo documento. Esta ficha no contradice esa mencion (la modela de forma generica a traves del campo "Modulo de origen" con catalogo abierto), pero deja constancia de que, tal como esta redactado hoy el mapa definitivo, esa relacion no tiene respaldo explicito en las fichas individuales de MOD-008 y MOD-009. Se recomienda que, cuando se redacten las fichas de esos dos modulos, se decida y declare expresamente si generan tareas hacia MOD-021 (por ejemplo, revision de un documento antes de su vencimiento, o renovacion de un contrato con un proveedor) y se actualicen ambos lados de la relacion.
3. Ningun otro desacuerdo material se detecto entre esta ficha y las fuentes de diseno ya decididas (`02_validacion_de_la_idea.md`, `04_objetivo_exacto_del_producto.md`, `05_tipos_de_usuario.md`, `22_anti_features.md`, `06_mapa_definitivo_de_modulos.md`, `mapa_modulos.json`). Todas las afirmaciones juridicas de esta ficha citan su OBL-ID y su articulo segun `01_legal/matriz_obligaciones.json` y `01_legal/03_hallazgos_regulatorios.md`; donde la ley es ambigua (por ejemplo, el computo del plazo de 72 horas), esta ficha lo senala explicitamente en vez de asumir una interpretacion como cierta.
