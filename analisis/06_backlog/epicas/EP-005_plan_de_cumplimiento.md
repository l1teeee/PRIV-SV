# EP-005 Plan de Cumplimiento (MOD-005)

**Objetivo.** La empresa recibe automaticamente, al cerrar su diagnostico, un plan de acciones priorizadas (Critica, Importante, Recomendada) con responsable, fecha limite y evidencia esperada, les da seguimiento hasta completarlas o descartarlas con justificacion, y puede exportar el plan con verificacion de integridad como prueba de su adecuacion.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R1 | 13 | 62 | 62 | 0 | [MOD-005](../../03_modulos/MOD-005_ficha.md) |

**Notas de la epica.**

- Sin recalculo automatico por cambio de respuestas del diagnostico ni por cambio normativo (ambos SHOULD HAVE segun la tabla Q y 19.3); el MVP solo cubre el recalculo manual bajo demanda (HU-005-12), conforme lo indica expresamente el encargo.
- El estado Bloqueada y el campo Dependencias con otras acciones quedan fuera del MVP (COULD HAVE en la tabla Q); los estados basicos cubiertos son Pendiente, En curso, Completada y Vencida (fila propia de la tabla Q) mas Descartada (su propia fila MUST HAVE) y Archivada (consecuencia automatica de archivar la version del plan, necesaria para que ninguna version se elimine).
- El historial de versiones completo navegable en pantalla es SHOULD HAVE (tabla Q); el MVP deja la trazabilidad de versiones en los eventos de historial y en la exportacion (HU-005-13), sin una pantalla dedicada de comparacion entre versiones.
- El servicio de exportacion con verificacion de integridad se declara como dependencia de EP-000 (plataforma) solo en HU-005-13, tal como lo indica el encargo; ningun modulo MOD-0NN de las 26 fichas lo declara como propio.
- No se detectaron discrepancias entre la tabla Q de la ficha y la seccion 19.3 del roadmap para este modulo: ambas coinciden en el mismo conjunto de 8 filas MUST HAVE.
- Los indicadores del Dashboard (seccion M de la ficha) y los reportes Acciones vencidas e Historial de recalculos (seccion N) no tienen HU propia en esta epica porque ninguno de los dos aparece como fila MUST HAVE de la tabla Q; MOD-020 los consume directamente de los datos que estas HU ya producen.
- La accion Comentar en una accion (seccion C de la ficha) tampoco tiene HU propia por la misma razon: no es una fila de la tabla Q.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-005-01 | Generar automaticamente la primera version del plan al cerrar el diagnostico | Administrador de la organizacion | 5 | R1 | 15 | MOD-004 |
| HU-005-02 | Configurar los parametros de generacion del plan de cumplimiento | Administrador de la organizacion | 2 | R1 | 4 | - |
| HU-005-03 | Calcular el nivel de prioridad de cada accion y permitir su reclasificacion manual justificada | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R1 | 15 | HU-005-01 |
| HU-005-04 | Asignar el responsable y calcular la fecha limite de cada accion del plan | Administrador de la organizacion | 5 | R1 | 15 | HU-005-01, HU-005-03, MOD-023, MOD-001 |
| HU-005-05 | Consultar el plan de cumplimiento agrupado por prioridad y filtrable | Administrador de la organizacion | 3 | R1 | 15 | HU-005-01, HU-005-03, HU-005-04 |
| HU-005-06 | Enviar una version del plan a revision | Administrador de la organizacion | 3 | R1 | 15 | HU-005-01, MOD-022 |
| HU-005-07 | Aprobar o rechazar una version del plan como Vigente | Aprobador | 8 | R1 | 15 | HU-005-06, MOD-001, MOD-022 |
| HU-005-08 | Archivar manualmente una version del plan | Administrador de la organizacion | 2 | R1 | 15 | HU-005-01 |
| HU-005-09 | Crear automaticamente una tarea por cada accion pendiente al aprobar el plan | Administrador de la organizacion | 3 | R1 | 15 | HU-005-07, MOD-021 |
| HU-005-10 | Avanzar el estado de una accion entre Pendiente, En curso, Completada y Vencida | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 8 | R1 | 16 | HU-005-04, HU-005-07, MOD-023, MOD-022 |
| HU-005-11 | Descartar una accion como no aplica con justificacion y validacion reforzada | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R1 | 16 | HU-005-10, MOD-001 |
| HU-005-12 | Recalcular manualmente el plan bajo demanda | Administrador de la organizacion | 8 | R1 | 16 | HU-005-07, HU-005-09, HU-005-10, MOD-004 |
| HU-005-13 | Exportar el plan con verificacion de integridad | Administrador de la organizacion | 5 | R1 | 16 | HU-005-07, EP-000 |

## Historias

### HU-005-01. Generar automaticamente la primera version del plan al cerrar el diagnostico

**Como** Administrador de la organizacion, **quiero** que el sistema genere automaticamente la primera version del plan de cumplimiento en cuanto el diagnostico de mi empresa se cierra, **para** recibir de inmediato una lista de acciones concretas y priorizadas en lugar de un cuestionario respondido sin ninguna traduccion a trabajo real.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 15 | No |

- Fundamento: OBL-PLAZO-03 (Art. 60 inc. 2, Ley para la Proteccion de Datos Personales); OBL-PRIN-01 (Art. 5 lit. c), Ley para la Proteccion de Datos Personales); OBL-PRIN-02 (Art. 5 lit. g), Ley para la Proteccion de Datos Personales)
- Depende de: -
- Modulos requeridos: MOD-004

**Criterios de aceptacion**

1. Dado que el diagnostico de mi empresa (MOD-004) llega a estado completado por primera vez, cuando el sistema procesa ese cierre, entonces crea automaticamente la version 1 del plan en estado Generado, con una AccionDelPlan por cada obligacion que el diagnostico marco como aplicable.
2. Dado que se crea una AccionDelPlan a partir de una obligacion aplicable, cuando el sistema la precarga, entonces completa los campos Titulo, Descripcion, Obligacion relacionada, Modulo de ejecucion y Evidencia esperada a partir de la plantilla de esa obligacion en el catalogo, y deja el campo Origen del disparo en Respuesta de diagnostico, de solo lectura.
3. Dado que ya existe una version previa del plan para mi organizacion, cuando el diagnostico se completa de nuevo, entonces el sistema no crea una segunda version de forma automatica por este evento, porque la regla de generacion automatica solo aplica cuando no existe ninguna version previa.
4. Dado que el diagnostico de mi empresa todavia no llego a estado completado, cuando intento abrir el plan de cumplimiento, entonces el sistema me indica que aun no existe ninguna version generada, sin crear un plan vacio por su cuenta.
5. Dado que la version 1 del plan termina de generarse, cuando reviso el historial del modulo, entonces encuentro el evento plan generado con la fecha y las obligaciones incluidas, registrado tambien en el AuditLog transversal.
6. Dado que una obligacion aplicable no tiene plantilla de accion cargada en el catalogo, cuando el sistema genera su AccionDelPlan, entonces la crea igual con la Obligacion relacionada visible y marca Descripcion y Evidencia esperada como pendientes de completar, sin bloquear la generacion del resto del plan.

**Reglas de negocio**

- El cierre del diagnostico dispara la generacion de la primera version del plan (v1, estado Generado) solo cuando no existe una version previa (seccion F.1 y G.2 regla 1).
- Los campos Titulo, Descripcion, Obligacion relacionada, Modulo de ejecucion, Origen del disparo y Evidencia esperada se precargan automaticamente desde el resultado del diagnostico y el catalogo de obligaciones (seccion D, Precarga).
- El campo Origen del disparo no es editable tras la creacion (seccion D).

**Fuera de alcance**

- Recalculo automatico por un nuevo cierre de diagnostico o por cambio normativo (SHOULD HAVE; el recalculo manual se cubre en HU-005-12)
- Envio a revision y aprobacion de la version generada (ver HU-005-06 y HU-005-07)

- Requiere contenido: Plantilla de accion por obligacion (titulo, descripcion y evidencia esperada) para cada obligacion del catalogo de matriz_obligaciones.json, redactada en lenguaje simple y validada por el equipo legal o de contenido
- Referencia: MOD-005 secciones A, D (Precarga), F.1, G.2 regla 1

### HU-005-02. Configurar los parametros de generacion del plan de cumplimiento

**Como** Administrador de la organizacion, **quiero** definir los dias habiles por defecto de cada nivel de prioridad y los umbrales de alerta por vencimiento, **para** adaptar los tiempos y las alertas del plan a la forma de operar de mi empresa sin depender de un cambio del equipo del producto.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 4 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que soy Administrador de la organizacion, cuando abro la configuracion de generacion del plan, entonces veo los cinco parametros de la seccion D con su valor por defecto: Dias habiles por defecto para accion Critica en 10, Importante en 30, Recomendada en 90, Umbral de dias vencida para escalar (Critica) en 5, y Umbral de acciones criticas vencidas para alerta maxima en 3.
2. Dado que cambio el valor de un parametro por un numero entero positivo, cuando guardo el cambio, entonces el sistema lo aplica desde ese momento a los calculos de fecha limite y de alertas, sin recalcular las fechas ya asignadas a acciones existentes.
3. Dado que intento guardar un parametro con un valor negativo, en cero o no numerico, cuando confirmo el cambio, entonces el sistema rechaza el guardado, muestra el motivo y conserva el valor anterior.
4. Dado que no soy Administrador de la organizacion, cuando intento abrir la configuracion de generacion del plan, entonces el sistema me niega el acceso, porque segun la seccion C solo el Administrador puede modificarla.
5. Dado que un parametro de configuracion se modifica, cuando reviso el historial del modulo, entonces encuentro el registro del cambio con el usuario, la fecha, el valor anterior y el nuevo.

**Reglas de negocio**

- La configuracion de generacion del plan es un conjunto de parametros a nivel de organizacion, editables solo por el Administrador, con valores por defecto de producto (seccion D).

**Fuera de alcance**

- Ponderacion configurable de los criterios de priorizacion por la propia empresa (FUTURE, fuera del MVP)

- Referencia: MOD-005 seccion D, tabla Configuracion de generacion del plan

### HU-005-03. Calcular el nivel de prioridad de cada accion y permitir su reclasificacion manual justificada

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que cada accion del plan reciba automaticamente un nivel de prioridad (Critica, Importante o Recomendada) segun reglas verificables, y poder cambiarlo manualmente cuando no refleje el riesgo real, dejando constancia del motivo, **para** saber por donde empezar sin tener que leer la ley articulo por articulo, sin perder la posibilidad de aplicar mi propio criterio cuando el algoritmo no conoce el contexto especifico de mi empresa.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 15 | No |

- Fundamento: OBL-PLAZO-03 (Art. 60 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-005-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que se genera o recalcula el plan, cuando el motor de priorizacion evalua una accion cuya obligacion tiene un plazo transitorio ya vencido (por ejemplo OBL-PLAZO-03 u OBL-PLAZO-04), entonces le asigna el nivel Critica.
2. Dado que se genera o recalcula el plan, cuando el motor evalua una accion cuya obligacion esta clasificada OBLIGATORIO en la matriz y su incumplimiento esta asociado a una infraccion GRAVE o MUY GRAVE, entonces le asigna el nivel Critica.
3. Dado que una accion no califica como Critica, cuando su obligacion esta clasificada OBLIGATORIO con infraccion LEVE, o es una obligacion CONDICIONAL que el diagnostico confirmo aplicable a la empresa, entonces el sistema le asigna el nivel Importante.
4. Dado que una accion no califica como Critica ni como Importante, cuando el motor la evalua, entonces le asigna el nivel Recomendada.
5. Dado que soy Delegado de Proteccion de Datos o Responsable Legal / Compliance, cuando cambio manualmente el Nivel de prioridad calculado de una accion sin diligenciar el campo Justificacion de repriorizacion manual, entonces el sistema no permite guardar el cambio y exige un texto de al menos 20 caracteres.
6. Dado que reclasifico manualmente el nivel de una accion con la justificacion diligenciada, cuando confirmo el cambio, entonces el sistema muestra el texto Requiere validacion de la organizacion o asesoria especializada, y guarda en el historial de la accion el nivel anterior, el nuevo y la justificacion.
7. Dado que soy Administrador de la organizacion, cuando intento reclasificar manualmente el nivel de prioridad de una accion, entonces el sistema no me lo permite, porque segun la seccion C esa accion esta reservada a Delegado de Proteccion de Datos y a Responsable Legal / Compliance.
8. Dado que soy Responsable de area (RRHH, Marketing, Operaciones, etc.), Responsable ARCO-POL / Responsable del tramite, Responsable de Seguridad / IT o Usuario de consulta / Colaborador, cuando abro una accion que se me asigno, entonces puedo ver su Nivel de prioridad pero el sistema no me ofrece la opcion de reclasificarla.

**Reglas de negocio**

- Motor de priorizacion: reglas de Nivel CRITICA (a, b, c), Nivel IMPORTANTE (a, b) y Nivel RECOMENDADA (a, b, c) de la seccion G.1.
- El campo Nivel de prioridad es editable solo con justificacion (seccion D); reclasificar es una decision que siempre exige que una persona registre el motivo (seccion H, decision 5).

**Fuera de alcance**

- Ponderacion configurable de los criterios de priorizacion por la propia empresa (FUTURE, fuera del MVP)

- Referencia: MOD-005 seccion G.1, seccion D (Nivel de prioridad, Justificacion de repriorizacion manual), seccion H decision 5

### HU-005-04. Asignar el responsable y calcular la fecha limite de cada accion del plan

**Como** Administrador de la organizacion, **quiero** asignar o reasignar quien ejecuta cada accion del plan y que el sistema calcule automaticamente su fecha limite con el motor de plazos habiles, **para** convertir cada accion en un compromiso de trabajo real, con alguien especifico y una fecha concreta, en lugar de una lista sin dueno de tarea asignado.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 15 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-005-01, HU-005-03
- Modulos requeridos: MOD-023, MOD-001

**Criterios de aceptacion**

1. Dado que se crea una AccionDelPlan, cuando el sistema la precarga, entonces sugiere un Responsable asignado por defecto segun el rol tipicamente responsable de esa obligacion, tomado del catalogo de usuarios activos de MOD-001.
2. Dado que quiero reasignar el Responsable asignado de una accion, cuando selecciono un usuario que no tiene acceso al Modulo de ejecucion de esa accion, entonces el sistema no permite guardar la asignacion y me indica el motivo.
3. Dado que una version del plan pasa a Vigente, cuando el sistema calcula la Fecha objetivo / limite de cada accion Pendiente, entonces usa el motor de plazos habiles compartido (MOD-023): si la obligacion tiene un plazo legal propio ya vencido, cuenta desde la fecha de generacion mas los dias habiles por defecto del nivel de la accion; si no tiene plazo legal propio, usa igualmente los dias habiles por defecto de su nivel.
4. Dado que edito manualmente la Fecha objetivo / limite de una accion, cuando la fecha que ingreso es anterior a la fecha de generacion del plan, entonces el sistema rechaza el cambio y muestra el motivo.
5. Dado que cambio el Responsable asignado o la Fecha objetivo / limite de una accion, cuando guardo el cambio, entonces el sistema actualiza el campo Fecha de ultima revision y registra en el historial el valor anterior y el nuevo.
6. Dado que soy Responsable Legal / Compliance, cuando reasigno el responsable de una accion por un criterio legal, entonces el sistema permite el cambio, igual que a Administrador de la organizacion y a Delegado de Proteccion de Datos, segun la seccion C.
7. Dado que una accion no tiene Responsable asignado, cuando intento pasarla a En curso, entonces el sistema no permite la transicion, porque ese campo es obligatorio antes de llegar a ese estado.

**Reglas de negocio**

- Responsable asignado obligatorio antes de pasar a En curso, con sugerencia de valor por defecto (seccion D).
- Fecha objetivo / limite calculada por el motor de plazos habiles compartido, nunca por un calculo local del modulo (seccion D, seccion G.2 regla 2, seccion P riesgo de calendario).

**Fuera de alcance**

- Dependencias entre acciones y estado Bloqueada (COULD HAVE, fuera del MVP)

- Referencia: MOD-005 seccion D (Responsable asignado, Fecha objetivo / limite), seccion G.2 regla 2, seccion C

### HU-005-05. Consultar el plan de cumplimiento agrupado por prioridad y filtrable

**Como** Administrador de la organizacion, **quiero** ver todas las acciones del plan vigente agrupadas por Nivel de prioridad y poder filtrarlas por modulo de ejecucion, responsable y estado, **para** dar seguimiento al avance sin perderme entre docenas de acciones ni tener que revisarlas una por una.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 15 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-005-01, HU-005-03, HU-005-04
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que existe una version Vigente del plan, cuando la abro como Administrador de la organizacion, entonces veo primero las acciones en nivel Critica, luego Importante y luego Recomendada, cada grupo en su propia vista.
2. Dado que estoy viendo el plan, cuando aplico un filtro por Modulo de ejecucion, por Responsable asignado o por Estado, entonces la lista muestra unicamente las acciones que cumplen ese filtro, combinables entre si.
3. Dado que soy Responsable de area (RRHH, Marketing, Operaciones, etc.), Responsable ARCO-POL / Responsable del tramite, Responsable de Seguridad / IT o Usuario de consulta / Colaborador, cuando abro el plan, entonces veo unicamente las acciones que tengo asignadas, sin acceso al resto del plan, segun la seccion C.
4. Dado que soy Auditor (interno), cuando abro el plan, entonces puedo ver el plan completo y su version, pero el sistema no me ofrece ninguna accion de crear, modificar, aprobar, descartar o adjuntar evidencia.
5. Dado que soy Auditor externo (invitado), cuando se me concede acceso, entonces veo el plan y la evidencia enlazada solo mientras dura la invitacion y dentro del alcance concedido.
6. Dado que soy Asesor externo invitado, cuando abro el modulo, entonces solo veo el fundamento normativo y el estado de la accion puntual para la que fui invitado, no el resto del plan.
7. Dado que no existe todavia ninguna version del plan para mi organizacion, cuando intento abrirlo, entonces el sistema me indica que aun no hay un plan generado, en lugar de mostrar una lista vacia sin explicacion.
8. Dado que la vista del plan muestra cualquier indicador de avance, cuando se presenta ese indicador, entonces el sistema lo expresa siempre como avance del plan o evidencia disponible, y nunca como un porcentaje de cumplimiento legal.

**Reglas de negocio**

- Permisos de Ver plan completo por rol (seccion C).
- Mitigacion de sobrecarga visual: agrupacion por prioridad mostrando primero las Criticas, con Importantes y Recomendadas en vistas separadas (seccion P).
- El indicador de avance nunca se expresa como porcentaje de cumplimiento legal (seccion M, apertura).

**Fuera de alcance**

- Historial de versiones completo navegable en pantalla (SHOULD HAVE); esta historia solo muestra la version Vigente

- Referencia: MOD-005 seccion C (Ver plan completo), seccion P (sobrecarga visual), seccion M (apertura)

### HU-005-06. Enviar una version del plan a revision

**Como** Administrador de la organizacion, **quiero** enviar el borrador del plan a revision cuando considere que esta completo, **para** que el Aprobador pueda confirmarlo formalmente antes de que se convierta en el compromiso oficial de mi empresa.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 15 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-005-01
- Modulos requeridos: MOD-022

**Criterios de aceptacion**

1. Dado que una version del plan esta en estado Generado y tiene al menos una AccionDelPlan por cada obligacion aplicable, cuando la envio a revision como Administrador de la organizacion o como Delegado de Proteccion de Datos, entonces el sistema cambia su estado a En revision y notifica al Aprobador.
2. Dado que a una version del plan en estado Generado le falta una accion para alguna obligacion aplicable, cuando intento enviarla a revision, entonces el sistema no permite el cambio de estado y me indica que obligacion quedo sin accion.
3. Dado que no soy Administrador de la organizacion ni Delegado de Proteccion de Datos, cuando intento enviar el plan a revision, entonces el sistema me niega la accion, segun la seccion C.
4. Dado que una version del plan pasa a En revision, cuando reviso el historial, entonces encuentro el evento con el usuario y la fecha del envio.
5. Dado que una version del plan lleva mas de 2 dias habiles en estado Generado o En revision, cuando se cumple ese plazo, entonces el sistema solicita a MOD-022 la alerta Plan pendiente de aprobacion hacia el Aprobador y el Administrador, sin bloquear el envio ni la aprobacion.

**Reglas de negocio**

- Transicion Generado a En revision: el borrador debe tener al menos una accion por cada obligacion aplicable (seccion F.1).
- Alerta Plan pendiente de aprobacion tras 2 dias habiles en Generado o En revision (seccion I).

- Referencia: MOD-005 seccion F.1, seccion I (Plan pendiente de aprobacion)

### HU-005-07. Aprobar o rechazar una version del plan como Vigente

**Como** Aprobador, **quiero** aprobar formalmente una version del plan que esta en revision, o rechazarla con un motivo, con doble control frente a quien la propuso, **para** que el plan solo se convierta en el compromiso oficial de la empresa cuando una persona con esa responsabilidad lo confirme de forma explicita, nunca de manera automatica.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 15 | No |

- Fundamento: OBL-PLAZO-03 (Art. 60 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-005-06
- Modulos requeridos: MOD-001, MOD-022

**Criterios de aceptacion**

1. Dado que una version del plan esta En revision, cuando la apruebo como Aprobador, entonces el sistema la cambia a Vigente, congela un snapshot con hash de integridad, y registra el evento de auditoria plan aprobado con mi usuario, mi rol y la fecha.
2. Dado que soy la misma persona que genero o envio a revision el borrador y ademas ocupo el rol Aprobador, cuando voy a confirmar la aprobacion, entonces el sistema muestra una advertencia visible de autorrevision antes de permitirme continuar.
3. Dado que estoy a punto de aprobar una version como Vigente, cuando el sistema me presenta la confirmacion, entonces incluye el texto Requiere validacion de la organizacion o asesoria especializada, porque publicar el plan nunca ocurre de forma automatica.
4. Dado que una version del plan esta En revision, cuando la rechazo registrando un motivo, entonces el sistema la regresa a estado Generado como borrador editable y notifica a quien la genero, con el motivo visible.
5. Dado que intento rechazar una version sin registrar un motivo, cuando confirmo el rechazo, entonces el sistema no permite guardar la accion.
6. Dado que no ocupo el rol Aprobador, cuando intento aprobar o rechazar una version del plan, entonces el sistema me niega la accion aunque sea Administrador de la organizacion o Delegado de Proteccion de Datos, segun la seccion C.
7. Dado que una version del plan pasa a Vigente, cuando reviso la evidencia del modulo, entonces encuentro el registro de aprobacion (usuario, rol, fecha) disponible para la auditoria anual de cumplimiento.

**Reglas de negocio**

- Aprobar congela snapshot con hash, crea tareas en MOD-021 y notifica a cada responsable (seccion F.1).
- Quien genera o propone el plan nunca es quien lo aprueba; advertencia de autorrevision cuando la misma persona ocupa ambos roles (seccion C, separacion de funciones).
- Aprobar una version como Vigente nunca es automatico (seccion H, decision 2).

**Fuera de alcance**

- Creacion de las tareas en MOD-021 (ver HU-005-09)

- Referencia: MOD-005 seccion F.1, seccion H decision 2, seccion J

### HU-005-08. Archivar manualmente una version del plan

**Como** Administrador de la organizacion, **quiero** archivar una version del plan en un caso excepcional, registrando el motivo, **para** retirarla de circulacion sin perder nunca su historial, cuando una situacion fuera de lo normal lo justifique.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 15 | No |

- Fundamento: OBL-PLAZO-03 (Art. 60 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-005-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que una version del plan esta en estado Generado, En revision o Vigente, cuando la archivo como Administrador de la organizacion sin registrar un motivo, entonces el sistema no permite guardar la accion.
2. Dado que archivo una version registrando el motivo, cuando confirmo la accion, entonces el sistema la cambia a Archivada, deja de generar tareas nuevas a partir de ella, y registra el evento de auditoria con mi usuario, la fecha y el motivo.
3. Dado que no soy Administrador de la organizacion, cuando intento archivar una version del plan, entonces el sistema me niega la accion, segun la seccion C.
4. Dado que una version pasa a Archivada, cuando busco una opcion para eliminarla, entonces el sistema no ofrece ninguna, porque ninguna version del plan se borra.
5. Dado que una version Vigente se archiva manualmente, cuando reviso sus AccionDelPlan en estado Completada o Descartada, entonces el sistema las conserva vinculadas a esa version archivada como evidencia historica, sin perderlas ni duplicarlas.

**Reglas de negocio**

- Archivar manualmente exige justificacion obligatoria y es exclusivo del Administrador (seccion F.1, seccion C).
- Ninguna version del plan se elimina, solo se archiva, preservando el historial completo (seccion C, seccion P).

- Referencia: MOD-005 seccion F.1 (Archivar manualmente), seccion C

### HU-005-09. Crear automaticamente una tarea por cada accion pendiente al aprobar el plan

**Como** Administrador de la organizacion, **quiero** que cada accion en estado Pendiente de la version recien aprobada genere automaticamente su tarea equivalente en el Centro de Tareas (MOD-021), **para** que cada responsable vea su trabajo pendiente en un solo lugar, sin tener que capturarlo de nuevo a mano.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 15 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-005-07
- Modulos requeridos: MOD-021

**Criterios de aceptacion**

1. Dado que una version del plan pasa a Vigente, cuando el sistema procesa esa aprobacion, entonces crea en MOD-021 una tarea por cada AccionDelPlan en estado Pendiente, con el mismo Responsable asignado y la misma Fecha objetivo / limite, enlazada de vuelta a la accion.
2. Dado que una AccionDelPlan de la version aprobada no esta en estado Pendiente (por ejemplo ya esta Descartada), cuando el sistema crea las tareas de esa version, entonces no genera ninguna tarea para esa accion.
3. Dado que la creacion de tareas termina, cuando reviso el plan, entonces cada accion Pendiente muestra el enlace a su tarea equivalente en MOD-021.
4. Dado que una version ya aprobada anteriormente vuelve a aprobarse tras un recalculo (v+1), cuando el sistema crea las tareas de la nueva version, entonces no duplica una tarea para una accion que se preservo sin cambios desde la version anterior y que ya tenia su tarea activa.
5. Dado que se crearon las tareas de una version, cuando reviso el historial del plan, entonces encuentro el numero de tareas creadas junto con el evento de aprobacion de esa version.

**Reglas de negocio**

- Version aprobada como Vigente, accion en estado Pendiente: crear una tarea equivalente en MOD-021 con el mismo responsable y fecha limite, enlazada de vuelta (seccion G.2 regla 3, seccion E).

**Fuera de alcance**

- Edicion o gestion posterior de la tarea dentro de MOD-021 (responsabilidad de esa ficha)

- Referencia: MOD-005 seccion E, seccion G.2 regla 3, seccion F.1

### HU-005-10. Avanzar el estado de una accion entre Pendiente, En curso, Completada y Vencida

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** iniciar el trabajo de una accion asignada a mi area, completarla con evidencia cuando termine, y que quede marcada si se vence, **para** dar seguimiento real al trabajo que me corresponde dentro del plan de cumplimiento.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 16 | No |

- Fundamento: OBL-PLAZO-03 (Art. 60 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-005-04, HU-005-07
- Modulos requeridos: MOD-023, MOD-022

**Criterios de aceptacion**

1. Dado que una accion esta en estado Pendiente y tiene Responsable asignado, cuando inicio el trabajo, entonces el sistema la cambia a En curso y registra la Fecha de inicio real.
2. Dado que una accion esta En curso, cuando la completo adjuntando o referenciando la Evidencia adjunta o referenciada exigida, entonces el sistema la cambia a Completada y actualiza el indicador de avance del plan.
3. Dado que la obligacion relacionada de la accion esta clasificada OBLIGATORIO, cuando intento completarla sin ninguna Evidencia adjunta o referenciada, entonces el sistema no permite el cambio a Completada.
4. Dado que estoy a punto de marcar una accion como Completada, cuando confirmo la evidencia, entonces el sistema me exige declarar explicitamente que la evidencia cargada satisface la tarea y muestra el texto Requiere validacion de la organizacion o asesoria especializada.
5. Dado que una accion Pendiente o En curso llega a su Fecha objetivo / limite sin llegar a Completada ni a Descartada, cuando el sistema evalua la fecha, entonces la cambia automaticamente a Vencida y solicita a MOD-022 la alerta correspondiente (WARNING para Importante o Recomendada, HIGH para Critica).
6. Dado que una accion Vencida se completa despues de su fecha limite, cuando la marco Completada, entonces el sistema la deja registrada como completada con retraso, sin perder la fecha limite original.
7. Dado que el numero de acciones en nivel Critica y estado Vencida alcanza el umbral configurado, cuando se cruza ese umbral, entonces el sistema solicita a MOD-022 la alerta CRITICAL hacia Administrador de la organizacion y Gerencia (via Aprobador).
8. Dado que una accion cambia de estado, cuando el cambio se guarda (manual o automatico), entonces el sistema lo registra en el historial con el estado anterior, el nuevo, el usuario o Sistema, y la fecha.

**Reglas de negocio**

- Transiciones de estado de AccionDelPlan (seccion F.2): Pendiente a En curso, En curso a Completada, Pendiente/En curso a Vencida.
- Declarar Completada exige declaracion explicita de que la evidencia satisface la tarea; el sistema no lo infiere solo por adjuntar un archivo (seccion H, decision 3).
- Alertas de vencimiento y escalamiento por nivel de prioridad (seccion I, seccion G.2 reglas 4 a 7).

**Fuera de alcance**

- Estado Bloqueada por dependencias entre acciones (COULD HAVE, fuera del MVP)
- Envio del correo o de la notificacion en si (responsabilidad de MOD-022)

- Referencia: MOD-005 seccion F.2, seccion H decision 3, seccion G.2 reglas 4 a 7, seccion I

### HU-005-11. Descartar una accion como no aplica con justificacion y validacion reforzada

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** marcar una accion como Descartada cuando no aplique a mi empresa, registrando el motivo y, si la obligacion es OBLIGATORIO, con la validacion de una segunda persona, **para** dejar constancia de por que esa obligacion no se ejecuta, sin que desaparezca del plan sin que nadie lo note.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 16 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-005-10
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado que una accion esta en estado Pendiente, En curso o Vencida, cuando la marco como Descartada sin diligenciar la Justificacion de descarte, entonces el sistema no permite guardar el cambio y exige un texto de al menos 20 caracteres.
2. Dado que la obligacion relacionada de la accion no esta clasificada OBLIGATORIO en la matriz, cuando registro la justificacion de descarte como Delegado de Proteccion de Datos o como Administrador de la organizacion, entonces el sistema cambia la accion a Descartada de inmediato.
3. Dado que la obligacion relacionada de la accion si esta clasificada OBLIGATORIO, cuando propongo el descarte con justificacion, entonces el sistema exige ademas la validacion de un segundo usuario (Responsable Legal / Compliance o Delegado de Proteccion de Datos, distinto de quien propuso) antes de cambiar la accion a Descartada, y muestra el texto Requiere validacion de la organizacion o asesoria especializada.
4. Dado que soy la misma persona que propuso el descarte de una accion ligada a una obligacion OBLIGATORIO, cuando intento validarlo yo mismo, entonces el sistema no lo permite.
5. Dado que una accion queda Descartada y su obligacion relacionada no tiene ninguna otra accion viva en el plan, cuando el sistema detecta esa situacion, entonces alerta a Responsable Legal / Compliance.
6. Dado que soy Responsable de area (RRHH, Marketing, Operaciones, etc.) o Responsable de Seguridad / IT, cuando propongo el descarte de una accion, entonces el sistema exige la validacion de Responsable Legal / Compliance antes de completarlo si la obligacion es OBLIGATORIO, segun la seccion C.
7. Dado que una accion queda Descartada, cuando reviso su historial, entonces encuentro el evento de auditoria con el motivo, quien lo registro y, cuando aplica, quien lo valido.
8. Dado que soy Auditor (interno) o Auditor externo (invitado), cuando reviso el plan, entonces no tengo ninguna opcion de descartar una accion, porque ese rol es siempre de solo lectura.

**Reglas de negocio**

- Transicion a Descartada: justificacion obligatoria y, si la obligacion es OBLIGATORIO, validacion de un segundo usuario (seccion F.2, seccion C).
- Descartar una accion ligada a una obligacion OBLIGATORIO nunca es una decision de una sola persona (seccion H, decision 4).

- Referencia: MOD-005 seccion F.2, seccion C, seccion H decision 4, seccion D (Justificacion de descarte)

### HU-005-12. Recalcular manualmente el plan bajo demanda

**Como** Administrador de la organizacion, **quiero** solicitar un recalculo del plan cuando lo considere necesario, sin perder el trabajo ya completado, **para** mantener el plan actualizado aunque el recalculo automatico por cambio de diagnostico o de normativa todavia no exista en esta version del producto.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 16 | No |

- Fundamento: OBL-PLAZO-03 (Art. 60 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-005-07, HU-005-09, HU-005-10
- Modulos requeridos: MOD-004

**Criterios de aceptacion**

1. Dado que existe una version Vigente del plan, cuando solicito su recalculo como Administrador de la organizacion o como Delegado de Proteccion de Datos, entonces el sistema la pasa a estado Recalculando.
2. Dado que el plan esta en Recalculando, cuando el motor de priorizacion termina de aplicar sus reglas sobre las obligaciones aplicables vigentes segun MOD-004, entonces el sistema genera una nueva version en estado Generado (v+1).
3. Dado que se genera la nueva version (v+1), cuando el sistema la crea, entonces cambia la version Vigente anterior a Archivada.
4. Dado que una AccionDelPlan ya esta Completada o Descartada y su obligacion sigue aplicando, cuando el plan se recalcula, entonces esa accion se preserva y se re-vincula a la nueva version, sin perderse ni duplicarse.
5. Dado que no soy Administrador de la organizacion ni Delegado de Proteccion de Datos, cuando intento solicitar el recalculo del plan, entonces el sistema me niega la accion, segun la seccion C.
6. Dado que solicito el recalculo del plan, cuando confirmo la accion, entonces el sistema registra en el historial el motivo del recalculo y la version anterior archivada.
7. Dado que la nueva version (v+1) queda en estado Generado, cuando la reviso, entonces todavia no genera tareas nuevas en MOD-021 ni es el compromiso oficial de la empresa, hasta que se repita el flujo de envio a revision y aprobacion.

**Reglas de negocio**

- Recalculo manual: un usuario con permiso lo solicita; la version Vigente pasa a Recalculando y luego a Generado (v+1); la version Vigente anterior pasa a Archivada (seccion F.1).
- El mantenimiento continuo de la adecuacion no tiene un articulo especifico que obligue a recalcular, pero si respalda la obligacion continua de OBL-PLAZO-03 (seccion R.5).

**Fuera de alcance**

- Recalculo automatico al cambiar respuestas del diagnostico (SHOULD HAVE)
- Recalculo automatico al confirmarse un cambio normativo del Centro Regulatorio (SHOULD HAVE)

- Referencia: MOD-005 seccion F.1, seccion C (Generar o recalcular el plan), seccion R.5

### HU-005-13. Exportar el plan con verificacion de integridad

**Como** Administrador de la organizacion, **quiero** exportar la version vigente del plan o una version archivada como Plan de adecuacion, con un hash de integridad verificable de forma independiente, **para** contar con la prueba concreta y verificable de que mi empresa esta ejecutando su adecuacion, lista para una auditoria o un requerimiento de la ACE.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 16 | No |

- Fundamento: OBL-PLAZO-03 (Art. 60 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-005-07
- Modulos requeridos: EP-000

**Criterios de aceptacion**

1. Dado que existe una version Vigente o una version Archivada del plan, cuando la exporto como Administrador de la organizacion, Delegado de Proteccion de Datos, Responsable Legal / Compliance o Aprobador, entonces el sistema genera el documento usando el servicio comun de exportacion con verificacion de integridad de EP-000 y produce un archivo con hash validable de forma independiente.
2. Dado que genero la exportacion Plan de adecuacion de una version aprobada especifica, cuando el archivo se genera, entonces incluye el numero de version, la fecha de aprobacion, y el listado completo de acciones con su fundamento (obligacion y articulo), Nivel de prioridad, Estado y Evidencia esperada.
3. Dado que genero cualquier exportacion del plan, cuando se produce el archivo, entonces incluye el texto de descargo Documento generado como borrador a partir de la informacion registrada. Requiere revision y aprobacion de su organizacion antes de usarse, y puede requerir validacion de asesoria legal especializada.
4. Dado que el servicio comun de EP-000 no puede verificar la integridad del archivo generado, cuando intento completar la exportacion, entonces el sistema no entrega el archivo como valido y me informa del error, en lugar de entregar un documento sin hash.
5. Dado que soy Auditor externo (invitado), cuando exporto el plan o su evidencia, entonces solo puedo hacerlo dentro de lo autorizado por mi invitacion, segun la seccion C.
6. Dado que soy Responsable de area (RRHH, Marketing, Operaciones, etc.), Responsable ARCO-POL / Responsable del tramite, Responsable de Seguridad / IT o Usuario de consulta / Colaborador, cuando busco exportar el plan, entonces el sistema no me ofrece esa opcion, porque segun la seccion C esos roles no tienen permiso de exportar.
7. Dado que se completa una exportacion del plan, cuando reviso el historial del modulo, entonces encuentro el evento registrado con el usuario, la fecha y el formato exportado.

**Reglas de negocio**

- Reporte Plan de adecuacion: version historica congelada con hash de integridad, evidencia central de OBL-PLAZO-03 (seccion E, K, N, J).
- Toda exportacion queda registrada en el historial (usuario, fecha, formato) (seccion O).

**Fuera de alcance**

- Reporte Acciones vencidas e Historial de recalculos del plan (no estan en la tabla Q como MUST HAVE de este modulo)

- Requiere contenido: Plantilla de exportacion Plan de Cumplimiento (variables nombre_organizacion, fecha_generacion, numero_de_version, lista_de_acciones) con el texto de descargo estandar del banner general, validada por el equipo legal o de contenido
- Referencia: MOD-005 seccion E, K, N, J

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Generacion automatica del plan tras el diagnostico | HU-005-01 |
| Motor de priorizacion Critica / Importante / Recomendada | HU-005-03 |
| Asignacion de responsable y fecha limite por accion | HU-005-04 |
| Estados basicos de la accion (Pendiente, En curso, Completada, Vencida) | HU-005-10 |
| Creacion automatica de tareas en el Centro de Tareas (MOD-021) | HU-005-09 |
| Exportacion del plan con hash de integridad ("Plan de adecuacion") | HU-005-13 |
| Recalculo manual bajo demanda | HU-005-12 |
| Descarte de accion con justificacion y validacion reforzada | HU-005-11 |
