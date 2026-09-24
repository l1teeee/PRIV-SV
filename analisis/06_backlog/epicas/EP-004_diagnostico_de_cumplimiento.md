# EP-004 Diagnostico de Cumplimiento (MOD-004)

**Objetivo.** Que la empresa complete un cuestionario guiado de 47 preguntas en 11 bloques que traduzca cada aspecto real de su operacion en un analisis inicial de aplicabilidad de la ley, detecte posibles exclusiones del Art. 3 con confirmacion humana, genere automaticamente al cerrar los tratamientos, tareas, documentos y evaluaciones de riesgo sugeridos hacia el resto del sistema, calcule un nivel de madurez inicial sin porcentaje de cumplimiento, y pueda repetirse conservando el historial completo de versiones anteriores

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R1 | 13 | 58 | 58 | 0 | [MOD-004](../../03_modulos/MOD-004_ficha.md) |

**Notas de la epica.**

- La asignacion de bloques a distintos responsables de area (seccion D.1, permiso P de Seguridad/IT y Responsable de area en la seccion C) es SHOULD HAVE segun la tabla Q; por eso estas HU limitan Iniciar y Responder a Administrador y Delegado en este MVP, igual que el escenario pyme de 04_secciones/15_onboarding.md seccion 15.6.1. La asignacion por bloques queda para cuando esa funcionalidad se construya.
- Comentar en una pregunta (COULD HAVE, fila propia de la tabla Q) y Adjuntar evidencia a una respuesta (fila de la tabla de permisos C sin desarrollo propio en las secciones D, F, G ni J de la ficha) no se convirtieron en HU de este MVP.
- La seccion G.1 dice en su encabezado que sus reglas no generan tarea, pero su propia fila P-EMP-07 si crea una tarea en MOD-021; HU-004-04 sigue la fila, mas especifica, sobre el encabezado general.
- 04_secciones/08b_workflows_casos_04_06.md reclasifica la EIPD de P-PER-04 (biometria laboral) de recomendada, texto literal de MOD-004 seccion G.2, a obligatoria, apoyandose en que matriz_obligaciones.json marca OBL-DOC-03 como OBLIGATORIO sin umbral de riesgo definido. Esta epica sigue el texto literal de la ficha (G.2: recomendada) porque el encargo pide usar la ficha como fuente principal; se deja constancia para que un revisor legal decida cual version debe prevalecer.
- El mecanismo de cobertura parcial de MOD-014 (HU-004-13) sigue el texto de la seccion 19.4 del roadmap y del encargo recibido (biometria, salud, menores o camaras), que es mas amplio que la propia tabla G.2 de la ficha: G.2 no asigna ninguna evaluacion de riesgo a P-MEN-01 (menores) ni a P-VID-01 (camara base sin reconocimiento facial). Se amplio la cobertura a esas dos preguntas siguiendo el encargo de forma literal, y se deja constancia del vacio para revision legal.
- Fuera de las dos coberturas parciales asignadas en el encargo, quedan sin tarea propia en MOD-021 los disparadores EIPD recomendada de P-SEN-01 (categorias sensibles generales) y evaluacion de base juridica de P-CLI-04, que la tabla G.2 marca como riesgo sin texto de tarea propio y que no entran en las cuatro categorias del encargo (biometria, salud, menores, camaras); no se crearon HU adicionales para no exceder el encargo recibido, y se deja como hueco documentado para una revision posterior.
- P-PER-07 (verificacion de antecedentes penales o crediticios) cita OBL-PROV-01 en la seccion D.2 pero no tiene fila propia en la tabla de disparadores G.2; este hueco ya esta documentado en 04_secciones/15_onboarding.md y esta epica no inventa un disparador para esa pregunta.
- La exportacion del resultado en PDF con verificacion de integridad y la asignacion de bloques a responsables de area son SHOULD HAVE (tabla Q); el historial comparativo entre diagnosticos sucesivos y los comentarios en una pregunta son COULD HAVE (tabla Q). Los cuatro quedan fuera de esta epica.
- HU-004-07 cita la pregunta pendiente PP-JUR-05 (tension entre la LPDP y la Ley Crecer Juntos para el consentimiento de adolescentes, P-MEN-02) porque el MVP ya activa el flujo parental completo por defecto, dejando la resolucion final para asesoria legal, segun 04_secciones/24_preguntas_pendientes.md.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-004-01 | Iniciar una sesion de diagnostico de cumplimiento | Administrador de la organizacion | 3 | R1 | 5 | MOD-003, MOD-001 |
| HU-004-02 | Responder las preguntas de un bloque respetando sus dependencias | Administrador de la organizacion | 8 | R1 | 12 | HU-004-01, MOD-001 |
| HU-004-03 | Guardar el avance del cuestionario y continuar despues | Administrador de la organizacion | 3 | R1 | 12 | HU-004-01, HU-004-02 |
| HU-004-04 | Detectar posibles exclusiones del Art. 3 y exigir confirmacion humana | Responsable Legal / Compliance | 5 | R1 | 12 | HU-004-02, MOD-021 |
| HU-004-05 | Calcular y mostrar el resultado del diagnostico | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R1 | 13 | HU-004-02, HU-004-04 |
| HU-004-06 | Cerrar la sesion de diagnostico con confirmacion simple o doble control | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R1 | 13 | HU-004-05 |
| HU-004-07 | Generar tratamientos, tareas, documentos y riesgos sugeridos al cerrar la sesion | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 8 | R1 | 14 | HU-004-05, HU-004-06, MOD-006, MOD-021, MOD-008, MOD-022 |
| HU-004-08 | Iniciar un re-diagnostico y archivar la sesion anterior | Administrador de la organizacion | 5 | R1 | 14 | HU-004-06 |
| HU-004-09 | Archivar manualmente una sesion de diagnostico | Administrador de la organizacion | 2 | R1 | 9 | HU-004-01 |
| HU-004-10 | Consultar en solo lectura el resultado y el historial de sesiones cerradas | Auditor (interno) | 3 | R1 | 14 | HU-004-06 |
| HU-004-11 | Alertar sobre el ciclo de vida de la sesion de diagnostico | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R1 | 14 | HU-004-01, HU-004-03, HU-004-06, HU-004-08, MOD-022, MOD-024, MOD-021 |
| HU-004-12 | Crear tarea manual para documentar una transferencia internacional detectada | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R1 | 14 | HU-004-02, HU-004-06, MOD-021, MOD-019 |
| HU-004-13 | Crear tarea de elaborar EIPD con plantilla generica cuando se detecta biometria, salud, menores o camaras | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R1 | 14 | HU-004-02, HU-004-06, MOD-021, MOD-008 |

## Historias

### HU-004-01. Iniciar una sesion de diagnostico de cumplimiento

**Como** Administrador de la organizacion, **quiero** iniciar una nueva sesion de diagnostico de cumplimiento para mi organizacion, con la version vigente del cuestionario y los datos de cabecera precargados, **para** que la empresa comience a identificar que le exige la ley sin tener que descubrirlo por su cuenta.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 5 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: MOD-003, MOD-001

**Criterios de aceptacion**

1. Dado que la organizacion completo el Onboarding (MOD-003), cuando el Administrador o el Delegado inician una sesion de diagnostico, entonces el sistema crea la sesion en estado EN PROGRESO con la organizacion precargada, el responsable de la sesion y la version vigente del cuestionario asignada automaticamente
2. Dado que la organizacion no ha completado el Onboarding, cuando se intenta iniciar una sesion de diagnostico, entonces el sistema impide la creacion y explica que debe completarse el Onboarding primero
3. Dado que la organizacion no tiene ninguna sesion de diagnostico cerrada previa, cuando se crea la sesion, entonces el campo Motivo de la sesion permite elegir Diagnostico inicial
4. Dado que la organizacion ya tiene al menos una sesion de diagnostico cerrada, cuando se crea una nueva sesion, entonces el campo Motivo de la sesion no permite elegir Diagnostico inicial y exige elegir Re-diagnostico por cambio de actividad o Re-diagnostico periodico
5. Dado un usuario sin permiso de iniciar sesion, por ejemplo Responsable de area o Usuario de consulta, cuando intenta crear una sesion de diagnostico, entonces el sistema deniega la accion
6. Dado que se crea la sesion, cuando se guarda, entonces el sistema registra un evento de historial con la organizacion, el usuario, la fecha, la version del cuestionario y el motivo de la sesion

**Reglas de negocio**

- La organizacion, el responsable de la sesion y la version del cuestionario se precargan y no se piden de nuevo (seccion D.1)
- Solo Administrador y Delegado pueden iniciar una sesion (seccion C)
- El motivo Diagnostico inicial solo esta disponible si es la primera sesion cerrada de la organizacion (seccion D.1)

**Fuera de alcance**

- Asignacion de bloques a distintos responsables de area al momento de crear la sesion (SHOULD HAVE, tabla Q)

- Requiere contenido: Catalogo y textos de las tres opciones de Motivo de la sesion; Texto de ayuda contextual de que es el Diagnostico de Cumplimiento (seccion R)
- Referencia: MOD-004 secciones D.1 y F (transicion No iniciado a En progreso)

### HU-004-02. Responder las preguntas de un bloque respetando sus dependencias

**Como** Administrador de la organizacion, **quiero** responder las preguntas de cada bloque del cuestionario, viendo solo las preguntas que corresponden segun mis respuestas anteriores y con los datos ya conocidos de mi organizacion precargados, **para** declarar como opera realmente mi empresa sin repetir datos ni responder preguntas que no le aplican.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 12 | No |

- Fundamento: OBL-AMB-01 (Art. 2 inc. 1, Ley para la Proteccion de Datos Personales); OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-004-01
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado que una pregunta obligatoria de un bloque no tiene respuesta, cuando el usuario intenta avanzar al siguiente bloque, entonces el sistema bloquea el avance y exige elegir una opcion antes de continuar
2. Dado que P-PER-01, tiene personal en planilla, se responde No, cuando se muestra el Bloque 2, entonces las preguntas P-PER-03, P-PER-05 y P-PER-06, que dependen de P-PER-01 igual a Si, no se muestran y no se exigen como obligatorias
3. Dado que P-PER-03, usa sistema de control de asistencia, se responde Si, cuando se muestra el Bloque 2, entonces aparece la pregunta P-PER-04 sobre biometria y se vuelve obligatoria antes de avanzar
4. Dado que la organizacion ya tiene registrados en MOD-001 su sector, su cantidad de empleados y si tiene mas de una sucursal, cuando se abre el Bloque 1, entonces esos valores aparecen prellenados en P-EMP-01, P-EMP-02 y P-EMP-08, listos para confirmarse o corregirse sin volver a capturarlos
5. Dado que una pregunta ya tenia una respuesta guardada y la sesion sigue abierta, cuando el usuario cambia esa respuesta antes del cierre, entonces el sistema conserva el valor anterior y el nuevo en el historial, con usuario y fecha, sin sobrescribir el dato anterior
6. Dado un usuario sin permiso de responder, por ejemplo Auditor interno o Usuario de consulta, cuando intenta responder una pregunta, entonces el sistema deniega la accion
7. Dado que P-TEC-02, proveedor con servidores fuera de El Salvador, ya fue respondida, cuando se muestra el Bloque 9, entonces P-TRF-01 aparece sugerida prellenada con esa respuesta, pero puede confirmarse o corregirse de forma independiente
8. Dado que se guarda una respuesta, cuando se guarda, entonces el sistema registra un evento de historial con la pregunta, el valor, el usuario, la fecha y la version del cuestionario

**Reglas de negocio**

- Todas las preguntas se muestran en lenguaje simple; el fundamento normativo, OBL-ID y articulo, solo aparece en la ayuda contextual de segundo nivel (seccion D.2)
- Ninguna pregunta pide nombre, DUI, correo u otro dato identificativo de un titular concreto; todas las preguntas son sobre la existencia de un tipo de tratamiento (seccion D.3)
- El cuestionario tiene 47 preguntas en 11 bloques, con las dependencias documentadas en la ficha seccion D.2 y en 04_secciones/15_onboarding.md seccion 15.3.2

**Fuera de alcance**

- Asignacion de bloques a distintos responsables de area (SHOULD HAVE, tabla Q)
- Comentarios en una pregunta especifica (COULD HAVE, tabla Q)
- Adjuntar evidencia a una respuesta (no desarrollado en las secciones D, F, G ni J de la ficha mas alla del permiso)

- Requiere contenido: Banco completo de las 47 preguntas de los 11 bloques con su texto en lenguaje simple, opciones, dependencias y ayuda contextual de segundo nivel (OBL-ID y articulo), validado por el equipo legal y de contenido antes de publicarse
- Referencia: MOD-004 secciones D.2, D.3, F (transicion Responder una pregunta), G.3 (cambio de respuesta) y C (permisos Responder y modificar respuestas)

### HU-004-03. Guardar el avance del cuestionario y continuar despues

**Como** Administrador de la organizacion, **quiero** guardar mi avance del cuestionario en cualquier punto y retomarlo despues en la ultima pregunta sin responder, **para** no perder lo ya respondido ni tener que completar las 47 preguntas en una sola sesion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 12 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-004-01, HU-004-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el usuario esta respondiendo una sesion en EN PROGRESO, cuando selecciona Guardar y continuar, entonces la sesion pasa a GUARDADO PARCIAL conservando exactamente el avance, sin calcular ningun resultado todavia
2. Dado una sesion en GUARDADO PARCIAL, cuando el mismo usuario la reanuda, entonces la sesion vuelve a EN PROGRESO y se posiciona en la ultima pregunta sin responder
3. Dado una sesion en GUARDADO PARCIAL, cuando el Administrador o el Delegado la reanudan aunque no la hayan iniciado ellos, entonces el sistema permite continuar respondiendo
4. Dado un usuario sin permiso de responder, cuando intenta reanudar una sesion en GUARDADO PARCIAL, entonces el sistema deniega la accion
5. Dado que la sesion cambia entre EN PROGRESO y GUARDADO PARCIAL, cuando ocurre el cambio, entonces el sistema registra un evento de historial con el estado anterior, el estado nuevo, el usuario y la fecha

**Reglas de negocio**

- Guardar y continuar no genera resultado ni cierra la sesion (seccion F)
- Reanudar posiciona al usuario en la ultima pregunta sin responder (tabla de transiciones, seccion F)

- Referencia: MOD-004 seccion F (transiciones Guardar y continuar, Reanudar) y seccion P (riesgo de abandono por extension del cuestionario)

### HU-004-04. Detectar posibles exclusiones del Art. 3 y exigir confirmacion humana

**Como** Responsable Legal / Compliance, **quiero** que el sistema me muestre una advertencia clara cuando una respuesta sugiera una posible exclusion del ambito de la ley, y que me pida confirmarla antes de descartar cualquier tratamiento, **para** no sobre obligar a la empresa con tareas que no le corresponden, pero tampoco asumir por error que esta exenta de la ley.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 12 | No |

- Fundamento: OBL-AMB-02 (Art. 3 lit. a), Ley para la Proteccion de Datos Personales); OBL-AMB-03 (Art. 3 lit. b), Ley para la Proteccion de Datos Personales); OBL-AMB-04 (Art. 3 lit. c) y d), Ley para la Proteccion de Datos Personales); OBL-INC-05 (Art. 6 lit. f-g, en relacion con Art. 2 y Art. 8 lit. f-g, Ley de Ciberseguridad y Seguridad de la Informacion)
- Depende de: HU-004-02
- Modulos requeridos: MOD-021

**Criterios de aceptacion**

1. Dado que P-EMP-03, entidad supervisada por la SSF, es Si y P-EMP-04, reporta historial crediticio, es Si, cuando se guardan ambas respuestas, entonces el sistema muestra la advertencia de posible exclusion parcial del reporte de historial crediticio y exige la confirmacion de Legal/Compliance antes de continuar sin generar tareas para esa actividad especifica
2. Dado que P-EMP-05, tratamiento exclusivamente domestico, es Si, cuando se guarda la respuesta, entonces el sistema muestra la advertencia de que una empresa registrada formalmente rara vez cumple esa condicion y exige la confirmacion explicita del Administrador antes de continuar
3. Dado que P-EMP-06, objeto es seguridad publica o registro publico oficial, es Si, cuando se guarda la respuesta, entonces el sistema muestra la advertencia de que esta exclusion no se extiende a seguridad privada ni a prevencion de fraude de empresas privadas y exige la confirmacion de Legal/Compliance
4. Dado que P-EMP-07, la ACE notifico infraestructura critica, es Si o No lo se, cuando se guarda la respuesta, entonces el sistema crea en el Centro de Tareas, MOD-021, la tarea de confirmar ante la ACE si la empresa esta calificada como operador de infraestructura critica, sin concluir por si mismo esa calificacion
5. Dado que ninguna de las cuatro condiciones anteriores se cumple, cuando se completa el Bloque 1, entonces el sistema no muestra ninguna advertencia de exclusion ni marca ningun tratamiento como excluido del alcance del diagnostico
6. Dado que un usuario confirma o rechaza una advertencia de posible exclusion, cuando responde, entonces el sistema registra un evento de historial con la decision, el usuario y la fecha

**Reglas de negocio**

- El sistema nunca concluye por si mismo que una empresa esta o no esta sujeta a la ley; solo marca la posibilidad y exige confirmacion humana (seccion H)
- La calificacion de operador de infraestructura critica es facultad exclusiva de la ACE (seccion G.1, OBL-INC-05)
- Toda advertencia de exclusion muestra el texto Requiere validacion de la organizacion o asesoria especializada (seccion H)

**Fuera de alcance**

- Decidir de forma definitiva si una exclusion del Art. 3 aplica, es una decision humana (seccion H)

- Requiere contenido: Los cuatro textos de advertencia de exclusion del Art. 3, seccion G.1, validados por el equipo legal antes de publicarse
- Requiere validacion legal: Si
- Referencia: MOD-004 seccion G.1 y seccion H (primera decision que el sistema no automatiza)

### HU-004-05. Calcular y mostrar el resultado del diagnostico

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** ver el nivel de madurez inicial de mi organizacion y el conteo de acciones criticas, importantes y recomendadas apenas se completan los bloques obligatorios, **para** saber que tan urgente es actuar sin necesitar que alguien me traduzca 105 obligaciones legales.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 13 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-004-02, HU-004-04
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que todas las preguntas obligatorias visibles segun las dependencias quedan respondidas, cuando se completa el ultimo bloque pendiente, entonces el sistema calcula el resultado preliminar y la sesion pasa a PENDIENTE DE CIERRE
2. Dado que no existe Delegado designado, P-GOB-01 es No, o no existe Aviso de Privacidad publicado, P-GOB-03 es No, o existe al menos una accion CRITICA de datos sensibles, menores o un incidente no reportado, cuando se calcula el resultado, entonces el nivel de madurez es INICIAL
3. Dado que existen Delegado y Aviso de Privacidad pero quedan acciones CRITICAS de otro origen o acciones IMPORTANTES sin asignar, cuando se calcula el resultado, entonces el nivel de madurez es EN DESARROLLO
4. Dado que solo quedan acciones RECOMENDADAS o ninguna accion pendiente, cuando se calcula el resultado, entonces el nivel de madurez es EN CONSOLIDACION
5. Dado el conteo de acciones criticas, importantes y recomendadas de la sesion, cuando se muestra el panel de resultado, entonces se presenta como X acciones criticas, Y importantes, Z recomendadas junto con el texto fijo que aclara que es un calculo de apoyo interno basado en lo registrado y no una declaracion de cumplimiento legal
6. Dado un usuario sin permiso de ver el resultado completo, por ejemplo Usuario de consulta o Titular, cuando intenta abrir el panel de resultado, entonces el sistema deniega el acceso
7. Dado el calculo del nivel de madurez o el conteo de acciones, cuando se muestra en cualquier pantalla, entonces el sistema nunca lo expresa como un porcentaje de cumplimiento legal

**Reglas de negocio**

- El nivel de madurez es un estado del programa, nunca un porcentaje de cumplimiento (seccion E.1)
- Cuando dos o mas preguntas distintas disparan una accion sobre el mismo tratamiento u obligacion, se fusionan en una sola antes de contarla (seccion E.1)

**Fuera de alcance**

- Exportacion del resultado en PDF con verificacion de integridad (SHOULD HAVE, tabla Q)
- Historial comparativo entre diagnosticos sucesivos (COULD HAVE, tabla Q)

- Requiere contenido: Texto fijo de descargo del resultado, validado por legal; Redaccion de los tres niveles de madurez, INICIAL, EN DESARROLLO, EN CONSOLIDACION, y su explicacion en lenguaje simple
- Referencia: MOD-004 secciones E y E.1

### HU-004-06. Cerrar la sesion de diagnostico con confirmacion simple o doble control

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** confirmar el cierre de la sesion de diagnostico, con una segunda confirmacion cuando el resultado tenga alguna accion critica, **para** que el resultado quede formalmente generado con la revision que corresponde segun su riesgo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 13 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-004-05
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado una sesion en PENDIENTE DE CIERRE sin ninguna accion CRITICA, cuando el Delegado o el Administrador confirman el cierre, entonces la sesion pasa a CERRADO - RESULTADO GENERADO con una sola confirmacion
2. Dado una sesion en PENDIENTE DE CIERRE con al menos una accion CRITICA, cuando el Delegado confirma el cierre, entonces el sistema exige una segunda confirmacion de Legal/Compliance o de Aprobador, distinta de quien respondio el cuestionario, antes de generar el resultado
3. Dado que la organizacion esta por debajo del umbral de tamano configurable, propuesta inicial 50 empleados, cuando existe una accion CRITICA, entonces el sistema solo recomienda la segunda confirmacion sin bloquear el cierre con una sola
4. Dado una sesion en PENDIENTE DE CIERRE, cuando quien inicio la sesion o el Administrador la reabren para corregir una respuesta antes de la confirmacion final, entonces la sesion vuelve a EN PROGRESO, se habilita la edicion y se registra el motivo de la reapertura
5. Dado una sesion en CERRADO - RESULTADO GENERADO, cuando cualquier usuario intenta modificar una respuesta, entonces el sistema deniega la edicion
6. Dado un usuario sin permiso para cerrar la sesion, por ejemplo Responsable de area, cuando intenta confirmar el cierre, entonces el sistema deniega la accion
7. Dado que se confirma el cierre, cuando ocurre, entonces el sistema registra un evento de historial con la identidad y la fecha de cada confirmacion, incluida la segunda cuando aplique

**Reglas de negocio**

- Cualquier respuesta clasificada como CRITICA no cierra la sesion sin la segunda confirmacion (seccion H)
- El cierre bloquea la edicion de respuestas (seccion F)
- Eliminar o archivar una sesion es exclusivo del Administrador y no forma parte de esta confirmacion de cierre (seccion C)

- Referencia: MOD-004 seccion F (transiciones Completar bloques obligatorios, Confirmar cierre, Reabrir) y seccion C (separacion de funciones)

### HU-004-07. Generar tratamientos, tareas, documentos y riesgos sugeridos al cerrar la sesion

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que al confirmarse el cierre el sistema genere automaticamente, en un solo paso, los tratamientos sugeridos, las tareas, los documentos sugeridos y las evaluaciones de riesgo que correspondan segun las respuestas del cuestionario, **para** saber de inmediato que debe hacer la empresa primero, sin tener que deducir por mi cuenta que obligacion dispara cada respuesta.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 14 | No |

- Fundamento: OBL-DOC-02 (Art. 4 (Medidas Organizativas, lit. d), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-AVISO-01 (Art. 24, Ley para la Proteccion de Datos Personales); OBL-SENS-06 (Art. 4 lit. g), Ley para la Proteccion de Datos Personales); OBL-SENS-07 (Art. 26 inc. 4 y Art. 37, Ley para la Proteccion de Datos Personales); OBL-CONS-04 (Art. 26 inc. 4, Ley para la Proteccion de Datos Personales); OBL-DOC-03 (Art. 4 (Medidas Organizativas, lit. e), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-SENS-04 (Art. 39, Ley para la Proteccion de Datos Personales); OBL-INC-01 (Art. 25, Ley para la Proteccion de Datos Personales); OBL-INC-02 (Art. 25 inc. 2, Ley para la Proteccion de Datos Personales); OBL-INC-04 (Art. 25 inc. final, Ley para la Proteccion de Datos Personales); OBL-ARCO-08 (Art. 18, Ley para la Proteccion de Datos Personales); OBL-ARCO-10 (Art. 20, Ley para la Proteccion de Datos Personales); OBL-DOC-01 (Art. 33 inc. 1, Ley para la Proteccion de Datos Personales)
- Depende de: HU-004-05, HU-004-06
- Modulos requeridos: MOD-006, MOD-021, MOD-008, MOD-022

**Criterios de aceptacion**

1. Dado que la sesion se cierra con P-PER-04, biometria de personal, igual a Si, cuando se confirma el cierre, entonces el sistema crea en el RAT, MOD-006, el tratamiento sugerido de control de acceso biometrico de personal, crea en el Centro de Tareas, MOD-021, la tarea de registrar consentimiento por escrito y ofrecer alternativa no biometrica, y sugiere en Documentos, MOD-008, el aviso especifico de biometria laboral
2. Dado que la sesion se cierra con P-CLI-01, registra datos de clientes, igual a Si, cuando se confirma el cierre, entonces el sistema crea el tratamiento sugerido de gestion de datos de clientes en MOD-006, la tarea de completar la ficha de RAT en MOD-021, y sugiere el Aviso de Privacidad de clientes en MOD-008
3. Dado que la sesion se cierra con P-SEN-02, datos geneticos, igual a Si, cuando se confirma el cierre, entonces el sistema crea en MOD-021 la tarea de elaborar EIPD para el tratamiento de datos geneticos, con prioridad CRITICA
4. Dado que dos o mas preguntas distintas de la misma sesion apuntan al mismo tratamiento u obligacion, por ejemplo P-PER-04 y P-VID-03, ambas sobre biometria, cuando se confirma el cierre, entonces el sistema fusiona ambos disparadores en una sola accion antes de crearla, sin duplicar tareas
5. Dado que la sesion se cierra con P-SEG-04, acceso no autorizado, perdida o fuga en el ultimo ano, igual a Si, cuando se confirma el cierre, entonces el sistema solicita de inmediato una alerta CRITICAL a Delegado y a Responsable de Seguridad/IT ademas de crear la tarea de evaluar si activa el flujo de Incidentes
6. Dado que la sesion se cierra con P-GOB-04, solicitud de un titular en el ultimo ano, igual a Si, cuando se confirma el cierre, entonces el sistema solicita de inmediato una alerta CRITICAL a Delegado y a Responsable ARCO-POL ademas de crear la tarea de revisar si existe una solicitud ARCO-POL pendiente fuera de plazo
7. Dado que una pregunta de la tabla de disparadores nunca se mostro en la sesion porque su dependencia no se cumplio, cuando se confirma el cierre, entonces el sistema no genera ningun tratamiento, tarea, documento ni riesgo asociado a esa pregunta
8. Dado que se genera cualquier tratamiento, tarea, documento o riesgo sugerido, cuando se crea, entonces el sistema registra en el historial la lista completa de lo generado, con referencia a cada registro creado en el modulo destino

**Reglas de negocio**

- El Diagnostico no escribe directamente en MOD-002, MOD-009, MOD-010, MOD-013, MOD-015 ni MOD-017; su unica salida transversal es siempre una tarea en el Centro de Tareas, MOD-021, y esa tarea describe en su texto en que modulo se completa el registro final (seccion G.2, nota de dependencias)
- La tension entre la LPDP y la Ley Crecer Juntos para P-MEN-02 se marca como nota de advertencia que requiere asesoria legal, sin que el sistema la resuelva (seccion H)
- Cuando MOD-014 Riesgos y EIPD no esta disponible, la evaluacion de riesgo sugerida se limita a lo que ya define esta HU en las filas de la tabla G.2 que crean una tarea propia de EIPD, por ejemplo P-SEN-02 y P-VID-02; el resto de la cobertura de riesgo sin MOD-014 se cubre con la HU-004-13

**Fuera de alcance**

- Registro directo en MOD-014 Riesgos y EIPD, el modulo no existe en este MVP, ver HU-004-13
- Registro directo en MOD-010 Transferencias Internacionales, el modulo no existe en este MVP, ver HU-004-12
- Determinar de forma definitiva si una EIPD es obligatoria mas alla de los disparadores tasados de la tabla G.2, decision humana, seccion H

- Requiere contenido: Tabla completa de disparadores de la seccion G.2, pregunta, tratamiento, tarea, documento, riesgo, OBL-ID y prioridad, validada por el equipo legal y de contenido, incluida su carga como configuracion mantenible; Textos de las tareas, nombres de tratamientos y documentos sugeridos de cada fila de la tabla
- Requiere validacion legal: Si (PP-JUR-05)
- Referencia: MOD-004 secciones G.2, G.3 (cierre confirmado) y E.1 (fusion de disparadores duplicados)

### HU-004-08. Iniciar un re-diagnostico y archivar la sesion anterior

**Como** Administrador de la organizacion, **quiero** abrir una nueva sesion de diagnostico cuando cambia algo relevante en mi operacion o vence el ciclo periodico, partiendo de las respuestas anteriores, **para** mantener actualizado el analisis de mi empresa sin perder el historial de lo que ya se respondio antes.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 14 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-004-06
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado una sesion en CERRADO - RESULTADO GENERADO, cuando el Administrador o el Delegado declaran un cambio relevante de actividad o se cumple el ciclo periodico configurado, entonces el sistema crea una nueva sesion en RE-DIAGNOSTICO ABIERTO con la version N mas 1 del cuestionario vigente
2. Dado que se crea la nueva sesion, cuando se genera, entonces la sesion cerrada anterior pasa a estado Archivado, sigue visible en el historial y no se elimina
3. Dado que la nueva sesion se abre, cuando el usuario continua respondiendo, entonces las respuestas de la sesion anterior se muestran precargadas como punto de partida y quedan editables
4. Dado un usuario sin permiso para iniciar sesion, por ejemplo Responsable de area, cuando intenta iniciar un re-diagnostico, entonces el sistema deniega la accion
5. Dado que se crea la nueva sesion de re-diagnostico, cuando se genera, entonces el sistema registra un evento de historial con el motivo del re-diagnostico, la version archivada y el usuario

**Reglas de negocio**

- Ninguna sesion cerrada se elimina; el re-diagnostico archiva, nunca borra (seccion F y O, principio de historial append-only)
- El motivo de la nueva sesion debe ser Re-diagnostico por cambio de actividad o Re-diagnostico periodico (seccion D.1)

- Referencia: MOD-004 seccion F (transicion Iniciar re-diagnostico) y seccion D.1 (version del cuestionario)

### HU-004-09. Archivar manualmente una sesion de diagnostico

**Como** Administrador de la organizacion, **quiero** archivar una sesion de diagnostico que ya no debe seguir activa, **para** mantener ordenado el listado de sesiones sin que nadie pueda borrar el registro subyacente.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 9 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-004-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado una sesion en cualquier estado distinto de Archivado, cuando el Administrador selecciona archivar la sesion, entonces la sesion pasa a estado Archivado y deja de aparecer en las vistas de sesiones activas
2. Dado que una sesion se archiva, cuando ocurre, entonces ningun registro de respuestas ni de historial subyacente se elimina
3. Dado un usuario distinto del Administrador, incluido el Delegado, cuando intenta archivar o eliminar una sesion, entonces el sistema deniega la accion
4. Dado que una sesion queda Archivada, cuando el Administrador o el Auditor interno consultan el historial, entonces la sesion archivada sigue siendo visible en modo lectura
5. Dado que se archiva una sesion, cuando ocurre, entonces el sistema registra un evento de historial con el usuario, la fecha y el motivo del archivado

**Reglas de negocio**

- Archivar es exclusivo del Administrador, nunca del Delegado, para que quien participa en el contenido del diagnostico no pueda hacerlo desaparecer del historial (seccion C)
- Archivar nunca borra el registro subyacente (secciones C y O)

- Referencia: MOD-004 seccion C (fila Eliminar / archivar una sesion) y seccion O (archivado de una sesion)

### HU-004-10. Consultar en solo lectura el resultado y el historial de sesiones cerradas

**Como** Auditor (interno), **quiero** consultar en modo lectura el historial de diagnosticos completados de la organizacion, **para** usarlo como evidencia en la auditoria anual de cumplimiento sin poder alterarlo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 14 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-004-06
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado el rol Auditor interno, cuando accede al historial de sesiones de diagnostico cerradas o archivadas de la organizacion, entonces puede consultarlo en modo lectura sin poder crear, responder, aprobar ni archivar ninguna sesion
2. Dado el rol Auditor externo invitado con una invitacion puntual vigente, cuando accede al resultado de una sesion cerrada, entonces solo puede consultarlo en modo lectura dentro del alcance de su invitacion
3. Dado el rol Asesor externo invitado con acceso acotado a un bloque o pregunta marcada como que requiere asesoria legal, cuando consulta esa respuesta, entonces solo ve el bloque o pregunta autorizados, en modo lectura
4. Dado que un Auditor externo invitado o un Asesor externo invitado accede a un resultado o a una respuesta, cuando ocurre el acceso, entonces el sistema registra un evento de historial reforzado con identidad, fecha y alcance del acceso, por tratarse de un rol externo
5. Dado el rol Titular, formulario externo, cuando intenta acceder a cualquier pantalla del diagnostico, entonces el sistema no le expone ninguna pantalla del modulo

**Reglas de negocio**

- El Auditor, interno o externo, siempre es de solo lectura, nunca puede coincidir con quien carga evidencia o aprueba una accion (05_tipos_de_usuario.md seccion 5.4)
- El acceso de un rol externo queda registrado con un refuerzo especifico frente al de un rol interno (seccion O)

**Fuera de alcance**

- Exportacion del resultado con verificacion de integridad (SHOULD HAVE, seccion N)

- Referencia: MOD-004 secciones B y C (filas Ver resultado completo, Exportar) y O (accesos externos reforzados)

### HU-004-11. Alertar sobre el ciclo de vida de la sesion de diagnostico

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** recibir avisos cuando el diagnostico nunca se inicia, cuando una sesion queda estancada, cuando el cierre deja acciones criticas sin asignar, cuando el diagnostico envejece sin repetirse, o cuando cambia el estado regulatorio, **para** actuar a tiempo sin depender de revisar manualmente cada sesion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 14 | No |

- Fundamento: OBL-DPO-01 (Art. 15 y 17, Ley para la Proteccion de Datos Personales); OBL-DPO-03 (Art. 10, Lineamientos para el Delegado de Proteccion de Datos Personales); OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-004-01, HU-004-03, HU-004-06, HU-004-08
- Modulos requeridos: MOD-022, MOD-024, MOD-021

**Criterios de aceptacion**

1. Dado que el Onboarding se completo hace mas de 7 dias sin que se haya iniciado una sesion de diagnostico, cuando se cumple el plazo, entonces el sistema solicita a Notificaciones, MOD-022, avisar con nivel WARNING al Administrador, y escala a Delegado a los 21 dias si sigue sin iniciarse
2. Dado que una sesion en GUARDADO PARCIAL no tiene actividad por mas del umbral configurable, por defecto 15 dias, cuando se cumple el umbral, entonces el sistema solicita avisar con nivel WARNING a quien tiene el bloque asignado y al Administrador, escalando a Delegado a los 30 dias
3. Dado que una sesion se cierra con al menos una accion CRITICA sin tarea asignada con responsable en el Centro de Tareas, MOD-021, cuando ocurre, entonces el sistema solicita avisar con nivel HIGH a diario al Delegado hasta que todas las acciones criticas queden asignadas, escalando a Administrador a los 5 dias
4. Dado que una sesion cerrada tiene mas de 12 meses, configurable, sin re-diagnostico, cuando se cumple el plazo, entonces el sistema solicita avisar con nivel INFO al Administrador y al Delegado sugiriendo iniciar un re-diagnostico
5. Dado que el Centro Regulatorio, MOD-024, activa el estado FUTURO y existe una sesion cerrada con P-GOB-01 respondida bajo el estado ACTUAL, cuando ocurre el cambio, entonces el sistema marca las tareas relacionadas con la designacion del Delegado como revisar bajo el nuevo estado regulatorio, sin eliminarlas, y solicita avisar con nivel WARNING al Delegado escalando a Administrador a los 10 dias

**Reglas de negocio**

- Los avisos internos siempre los envia Notificaciones, MOD-022; este modulo solo define la condicion y el destinatario (seccion I)
- Ningun cambio de estado normativo elimina una tarea; solo la marca para revision (seccion G.3, principio 8 de 06_mapa_definitivo_de_modulos.md)

- Requiere contenido: Textos de asunto y cuerpo de cada alerta para los canales plataforma y correo, validados por el equipo de contenido
- Referencia: MOD-004 seccion I (tabla de alertas) y G.3 (ultima fila, cambio de estado regulatorio)

### HU-004-12. Crear tarea manual para documentar una transferencia internacional detectada

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** recibir una tarea para documentar como evidencia suelta la transferencia internacional que el diagnostico detecto, mientras el modulo de Transferencias Internacionales no exista, **para** dejar constancia de la transferencia aunque el sistema todavia no tenga un registro formal para ella.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 14 | No |

- Fundamento: OBL-TRANSF-01 (Art. 40, Ley para la Proteccion de Datos Personales); OBL-TRANSF-03 (Art. 44 inc. 1, Ley para la Proteccion de Datos Personales)
- Depende de: HU-004-02, HU-004-06
- Modulos requeridos: MOD-021, MOD-019

**Criterios de aceptacion**

1. Dado que la sesion se cierra con P-TRF-01, datos almacenados o procesados fuera de El Salvador, igual a Si, o con P-TEC-02, proveedor con servidores fuera de El Salvador, igual a Si o No lo se, cuando se confirma el cierre y el modulo de Transferencias Internacionales no esta disponible en el sistema, entonces el sistema crea en el Centro de Tareas, MOD-021, una tarea manual dirigida al Responsable de area para documentar la transferencia detectada como evidencia suelta, en vez de crear una ficha formal de transferencia
2. Dado que esa tarea se completa, cuando el Responsable de area adjunta la documentacion de la transferencia, entonces el sistema la registra como evidencia suelta pendiente de aprobacion en el Centro de Evidencias, MOD-019
3. Dado que P-TRF-01 y P-TEC-02 se responden ambas No, cuando se cierra la sesion, entonces el sistema no crea esta tarea de cobertura parcial
4. Dado que P-TRF-02, comparte datos con sociedades del grupo en otros paises, o P-TRF-03, le han pedido enviar datos al extranjero, se responden Si, cuando se cierra la sesion, entonces el sistema aplica el mismo mecanismo de tarea manual de evidencia suelta mientras el modulo de Transferencias Internacionales no exista
5. Dado que se crea la tarea de esta cobertura parcial, cuando se genera, entonces el sistema registra un evento de historial que indica que el mecanismo usado fue la cobertura parcial de Transferencias Internacionales, referenciando OBL-TRANSF-01 y OBL-TRANSF-03

**Reglas de negocio**

- Mientras MOD-010 Transferencias Internacionales no exista en el sistema, el diagnostico crea el registro pendiente de confirmar como tarea manual en MOD-021 en vez de una ficha formal de transferencia (seccion L de la ficha y seccion 19.4 del roadmap)
- Este mecanismo no sustituye al flujo formal de MOD-010; solo evita que la obligacion quede sin ninguna forma de cumplirse mientras el modulo completo no se construya (seccion 19.4)

**Fuera de alcance**

- Ficha formal de transferencia con estados propios, queda para cuando exista MOD-010, fuera de este MVP

- Requiere contenido: Texto de la tarea manual de documentar la transferencia como evidencia suelta, validado por el equipo legal mientras MOD-010 no exista
- Referencia: MOD-004 seccion L (que ocurre si MOD-010 no existe) y 04_secciones/19_21_roadmap_mvp_v1_v2.md seccion 19.4, fila MOD-010

### HU-004-13. Crear tarea de elaborar EIPD con plantilla generica cuando se detecta biometria, salud, menores o camaras

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** recibir una tarea de elaborar EIPD con una plantilla generica cuando el diagnostico detecte biometria, salud, menores o camaras, mientras el modulo de Riesgos y EIPD no exista, **para** empezar a documentar el riesgo del tratamiento aunque el sistema todavia no tenga un motor de calculo de riesgo propio.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 14 | No |

- Fundamento: OBL-SENS-06 (Art. 4 lit. g), Ley para la Proteccion de Datos Personales); OBL-SENS-07 (Art. 26 inc. 4 y Art. 37, Ley para la Proteccion de Datos Personales); OBL-SENS-04 (Art. 39, Ley para la Proteccion de Datos Personales); OBL-PRIN-04 (Art. 5 lit. j), Ley para la Proteccion de Datos Personales)
- Depende de: HU-004-02, HU-004-06
- Modulos requeridos: MOD-021, MOD-008

**Criterios de aceptacion**

1. Dado que la sesion detecta biometria, P-PER-04, P-VID-02 o P-VID-03 igual a Si, salud, P-PER-05 igual a Si o P-EMP-01 igual a Salud, menores, P-MEN-01 igual a Si, o camaras de videovigilancia, P-VID-01 igual a Si, cuando se confirma el cierre de la sesion y el modulo de Riesgos y EIPD no esta disponible en el sistema, entonces el sistema crea en el Centro de Tareas, MOD-021, la tarea elaborar EIPD para el tratamiento detectado, dirigida al Delegado o Responsable interno
2. Dado que se crea la tarea elaborar EIPD, cuando se genera, entonces el sistema sugiere en Documentos y Politicas, MOD-008, la plantilla generica de EIPD, de llenado manual y sin motor de calculo de riesgo
3. Dado que dos o mas de esas condiciones se detectan sobre el mismo tratamiento, por ejemplo biometria de personal y camaras con reconocimiento facial, cuando se confirma el cierre, entonces el sistema fusiona ambos disparadores en una sola tarea elaborar EIPD, sin duplicarla
4. Dado que ninguna de las cuatro condiciones se detecto en la sesion, cuando se confirma el cierre, entonces el sistema no crea la tarea elaborar EIPD de esta cobertura parcial
5. Dado que se crea la tarea de esta cobertura parcial, cuando se genera, entonces el sistema registra un evento de historial que referencia el OBL-ID del tratamiento detectado y deja constancia de que se uso la plantilla generica de MOD-008 en vez de una evaluacion nativa de MOD-014

**Reglas de negocio**

- Mientras MOD-014 Riesgos y EIPD no exista en el sistema, el diagnostico igual crea la tarea elaborar EIPD en MOD-021 con una plantilla generica en MOD-008, sin motor de scoring (seccion L de la ficha y seccion 19.4 del roadmap)
- La conclusion juridica sobre si una EIPD es realmente obligatoria siempre requiere aprobacion humana; esta tarea solo abre el expediente, no lo resuelve (seccion H)

**Fuera de alcance**

- Motor de calculo o puntaje de riesgo, queda para cuando exista MOD-014, fuera de este MVP
- Determinacion final de si la EIPD es obligatoria u obligatoria por escala, decision humana, seccion H

- Requiere contenido: Plantilla generica de EIPD en MOD-008, validada por el equipo legal, para uso mientras MOD-014 no exista; Texto de la tarea elaborar EIPD
- Requiere validacion legal: Si
- Referencia: MOD-004 seccion L (que ocurre si MOD-014 no existe) y 04_secciones/19_21_roadmap_mvp_v1_v2.md seccion 19.4, fila MOD-014

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Cuestionario completo de 11 bloques y 47 preguntas, con dependencias | HU-004-01, HU-004-02 |
| Deteccion de exclusiones del Art. 3 (seccion G.1) | HU-004-04 |
| Motor de disparo (tratamiento + tarea + documento + riesgo, seccion G.2) | HU-004-07 |
| Guardar y continuar | HU-004-03 |
| Calculo de nivel de madurez inicial y conteo de acciones por prioridad | HU-004-05 |
| Diagnostico repetible (re-diagnostico por cambio de actividad) | HU-004-08 |
