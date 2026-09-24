# EP-017 Capacitacion (MOD-017)

**Objetivo.** Dejar constancia verificable de que el personal recibio capacitacion en proteccion de datos (general, induccion de personal nuevo y por rol), con renovacion automatica sin que nadie tenga que llevar la cuenta a mano, y permitir que el Delegado de Proteccion de Datos elabore y publique el plan anual de capacitacion e induccion que la norma le exige mientras la empresa tenga esa figura activa.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R2 | 15 | 56 | 0 | 56 | [MOD-017](../../03_modulos/MOD-017_ficha.md) |

**Notas de la epica.**

- La tabla Q de MOD-017_ficha.md y la seccion 19.3 del roadmap coinciden en el alcance minimo (registro general, induccion automatica, capacitacion por rol, recordatorio y renovacion automatica, notificacion hacia MOD-002, version minima del plan anual); no se detecto discrepancia entre ambas fuentes para este modulo.
- OBL-CAP-02 es CONDICIONAL (aplica mientras exista Delegado nombrado), pero la propia ficha clasifica como MUST HAVE tambien la version minima del Plan anual porque, bajo el regimen ACTUAL vigente al 2026-09-24, el Delegado es obligatorio para toda empresa privada sujeta a la LPDP: la condicion se cumple de facto para el universo completo de clientes del MVP. Las HU-017-09 a HU-017-12 heredan esa misma lectura.
- La ficha de MOD-017 (seccion A y nota final punto 1, y PP-MAPA-09 de 24_preguntas_pendientes.md) documenta y corrige una descripcion imprecisa de OBL-CAP-02 en 06_mapa_definitivo_de_modulos.md y en el campo notas_reforma_659 de mapa_modulos.json (la describen como 'capacitacion especifica anual del Delegado'). El texto exacto de matriz_obligaciones.json y de los Lineamientos DPO (Art. 22, ultimo parrafo) confirma que OBL-CAP-02 es el plan anual de capacitacion e induccion dirigido al personal, que el Delegado elabora, distinto de OBL-DPO-05 (la capacitacion que el propio Delegado recibe, propietario MOD-002). Este backlog sigue la definicion de la ficha (matriz y fuente primaria), consistente con HU-017-09/10/11/12 (plan dirigido al personal) frente a HU-017-08 (notificacion de la capacitacion propia del Delegado hacia MOD-002 para OBL-DPO-04/05). No es una discrepancia pendiente de resolver, ya esta resuelta en la ficha; se deja la nota por transparencia.
- Se agrego HU-017-15 (sugerencia de capacitacion por leccion aprendida de un incidente, automatizacion G.7 de la ficha) aunque el encargo no la enumero de forma expresa entre las indicaciones especificas: es comportamiento MVP ya documentado en las secciones G, H e I de la ficha (y en la seccion 12.2.17/12.3.17 del documento de tareas y alertas), por lo que la regla general de cobertura completa del MUST HAVE (seccion 3 de INSTRUCCIONES_HU.md) exige incluirla. Es la HU mas pequena y de menor prioridad de la epica (2 puntos, no habilitadora); si el encargo prefiere excluirla, puede eliminarse sin afectar la cobertura de la tabla Q.
- La minimizacion de datos de empleados (indicacion especifica del encargo) no se modelo como una HU aparte porque la ficha la resuelve como una regla de validacion y un texto de ayuda sobre un campo ya existente (Constancia o acuse, seccion D.2: solo la constancia especifica, nunca el expediente laboral completo), no como una capacidad nueva: quedo como regla_negocio de HU-017-03 y HU-017-04.
- La exclusion de cursos interactivos, evaluaciones formales con calificacion, certificados automaticos e integracion con un LMS externo (indicacion especifica del encargo, y filas SHOULD/COULD/FUTURE de la tabla Q) no genero ninguna HU; se dejo registrada como fuera_de_alcance en las HU de registro (HU-017-02, HU-017-03) y no se repite fila por fila.
- El umbral configurable de separacion de funciones (propuesta inicial 50 empleados, autorrevision Aprobador/Elaborador del plan anual) es un parametro transversal de la plataforma (02_validacion/05_tipos_de_usuario.md, seccion 5.4), consumido por HU-017-10 pero no reconfigurado dentro de MOD-017; por eso HU-017-01 (configuracion propia del modulo) solo cubre periodicidad de renovacion por defecto y dias de anticipacion de alertas/plazos, que si son parametros propios de esta ficha (seccion G, columna Configurable por la empresa).
- Ninguna HU de esta epica quedo con 13 puntos; el flujo mas complejo (HU-017-10, aprobar y publicar el plan anual) se estimo en 8 por integrar doble control, generacion de documento con plantilla y notificacion simultanea hacia MOD-002, MOD-008 y MOD-019.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-017-01 | Configurar los parametros generales de capacitacion | Administrador de la organizacion | 2 | R2 | 28 | - |
| HU-017-02 | Crear y versionar programas de capacitacion general, de induccion y por rol | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 31 | - |
| HU-017-03 | Asignar y dar seguimiento a la asistencia de una persona a una capacitacion | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 5 | R2 | 31 | HU-017-02 |
| HU-017-04 | Confirmar mi propia asistencia a una capacitacion asignada | Usuario de consulta / Colaborador | 3 | R2 | 32 | HU-017-02, HU-017-03 |
| HU-017-05 | Crear automaticamente la induccion de un usuario nuevo dado de alta | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R2 | 32 | HU-017-02, HU-017-03, MOD-001, MOD-021, MOD-022 |
| HU-017-06 | Asignar automaticamente la capacitacion por rol al cambiar de rol un usuario | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R2 | 32 | HU-017-02, HU-017-03, MOD-001, MOD-021, MOD-022 |
| HU-017-07 | Calcular y ejecutar la renovacion automatica de una capacitacion | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 32 | HU-017-03, MOD-023, MOD-021, MOD-022 |
| HU-017-08 | Notificar a MOD-002 la constancia de capacitacion del Delegado | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R2 | 32 | HU-017-03, MOD-002, MOD-022 |
| HU-017-09 | Elaborar el borrador del plan anual de capacitacion e induccion | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 32 | HU-017-02, MOD-002, MOD-008 |
| HU-017-10 | Aprobar y publicar el plan anual de capacitacion e induccion | Aprobador | 8 | R2 | 32 | HU-017-09, MOD-002, MOD-008, MOD-019 |
| HU-017-11 | Recibir recordatorio para elaborar o actualizar el plan anual antes de su vencimiento | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R2 | 32 | HU-017-09, HU-017-10, MOD-023, MOD-021, MOD-022, MOD-002 |
| HU-017-12 | Aplicar el efecto de la bandera de la reforma 659 sobre el plan anual | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R2 | 33 | HU-017-09, HU-017-10, HU-017-11, MOD-024, MOD-002 |
| HU-017-13 | Consultar los indicadores de capacitacion del personal | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R2 | 33 | HU-017-02, HU-017-03, HU-017-05, HU-017-06, HU-017-07, HU-017-09, HU-017-10, MOD-020, MOD-001 |
| HU-017-14 | Exportar reportes y listados de capacitacion del personal | Responsable Legal / Compliance | 3 | R2 | 33 | HU-017-03, HU-017-09, HU-017-10, MOD-019 |
| HU-017-15 | Recibir sugerencia de capacitacion a partir de una leccion aprendida de un incidente | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 2 | R2 | 33 | HU-017-02, MOD-013, MOD-021 |

## Historias

### HU-017-01. Configurar los parametros generales de capacitacion

**Como** Administrador de la organizacion, **quiero** configurar la periodicidad de renovacion por defecto y los dias de anticipacion de las alertas de induccion, capacitacion por rol y renovacion, **para** que el registro general de capacitacion del personal use plazos ajustados a la realidad de mi empresa sin depender de un valor fijo del sistema.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R2 | 28 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que soy Administrador de la organizacion, cuando abro la configuracion general de Capacitacion, entonces puedo ver y editar la periodicidad de renovacion por defecto (Anual, Cada 2 anos o Personalizada), los dias de anticipacion de la alerta de renovacion (por defecto 30), los dias de plazo para completar la induccion de personal nuevo (por defecto 30) y los dias de plazo para completar la capacitacion por rol tras un cambio de rol (por defecto 15).
2. Dado que cambio alguno de estos valores, cuando guardo la configuracion, entonces el sistema aplica el nuevo valor solo a los TrainingRecord que se creen o recalculen desde ese momento, sin modificar retroactivamente los plazos ya calculados de registros existentes.
3. Dado que un usuario no tiene el rol Administrador de la organizacion, cuando intenta abrir esta configuracion, entonces el sistema le deniega el acceso.
4. Dado que dejo un campo de dias en blanco o con un valor no numerico o negativo, cuando intento guardar, entonces el sistema rechaza el cambio y muestra un mensaje de validacion, conservando el ultimo valor valido.
5. Dado que se guarda un cambio de configuracion, cuando reviso el historial del modulo, entonces encuentro un evento de auditoria con el valor anterior, el valor nuevo y quien hizo el cambio.

**Reglas de negocio**

- La periodicidad de renovacion por defecto es editable y se sugiere Anual (seccion D.1); la norma no fija una periodicidad para OBL-CAP-01.
- Los dias de anticipacion de alertas y los dias de plazo de induccion y de capacitacion por rol son configurables por la empresa (seccion G, filas 1, 2 y 3).

**Fuera de alcance**

- Configurar el umbral de doble control para autorrevision, que es un parametro transversal de la plataforma administrado fuera de este modulo.
- Configurar el catalogo de temas o el catalogo de roles destinatarios, que son catalogos fijos del sistema.

- Referencia: MOD-017 seccion B (fila Administrador) y seccion G, filas 1, 2 y 3 (columna Configurable por la empresa)

### HU-017-02. Crear y versionar programas de capacitacion general, de induccion y por rol

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** crear y versionar programas de capacitacion (TrainingProgram) de tipo General, Induccion de personal nuevo o Por rol especifico, con su tema, modalidad, version del material y periodicidad de renovacion, **para** dejar organizado que se va a ensenar, a quien y con que material, como base del registro de capacitacion que exige OBL-CAP-01.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 31 | Si |

- Fundamento: OBL-CAP-01 (Art. 4 (Medidas Organizativas, lit. c), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que creo un programa nuevo, cuando completo nombre, tipo de programa (General, Induccion de personal nuevo o Por rol especifico), al menos un tema y al menos un rol o publico destinatario, entonces el programa queda en estado Borrador y registra el evento de creacion en el historial.
2. Dado un programa en Borrador, cuando intento publicarlo, entonces el sistema exige que la modalidad y la version del material esten completas antes de permitir el cambio a Vigente.
3. Dado un programa de tipo distinto de Induccion de personal nuevo, cuando lo publico sin haber elegido una periodicidad de renovacion, entonces el sistema no permite publicarlo porque la periodicidad de renovacion es obligatoria salvo para el tipo Induccion.
4. Dado un programa ya Vigente, cuando registro una nueva version del material y la publico, entonces la version anterior pasa a Archivado conservandose integra para consulta, y la nueva version exige un numero o texto de version mayor que el anterior del mismo programa.
5. Dado un programa en Borrador que ya tiene TrainingRecord asociados, cuando intento descartarlo, entonces el sistema exige un motivo obligatorio antes de pasarlo a Descartado, y los TrainingRecord ya creados quedan marcados para reasignacion manual.
6. Dado que el tipo de programa ya fue elegido al crearlo, cuando intento cambiarlo despues, entonces el sistema no permite editar ese campo.
7. Dado un usuario con rol Responsable de area o Usuario de consulta, cuando intenta crear un programa, entonces el sistema le deniega la accion porque no esta entre los roles habilitados para crear programas.

**Reglas de negocio**

- Tipo de programa no es editable despues de creado (seccion D.1).
- Version del material debe incrementar respecto a la version anterior del mismo programa (seccion D.1).
- Periodicidad de renovacion es obligatoria salvo cuando Tipo = Induccion de personal nuevo (seccion D.1).
- Transiciones de TrainingProgram segun la tabla F.1: Borrador a Vigente exige version del material y modalidad completas; Vigente a Archivado ocurre por nueva version o fin de vigencia; Descartado y Archivado son estados terminales para esa version.
- Pueden crear programas: Administrador (configuracion general), Delegado o Responsable interno, Responsable Legal, y Responsable de Seguridad/IT solo para programas tecnicos (seccion C).

**Fuera de alcance**

- Programas de Tipo = Plan anual, cubiertos en HU-017-09 y HU-017-10.
- Asignacion de un programa a una persona concreta (TrainingRecord), cubierta en HU-017-03.
- Cursos interactivos, microlearning, evaluaciones formales con calificacion o certificados automaticos: este modulo no es un LMS.

- Referencia: MOD-017 seccion D.1, seccion F.1 y su tabla de transiciones de TrainingProgram, seccion C

### HU-017-03. Asignar y dar seguimiento a la asistencia de una persona a una capacitacion

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** asignar manualmente una capacitacion vigente a una persona de mi area y registrar su asistencia con la fecha, la modalidad y la constancia, **para** dejar evidencia verificable de que esa persona recibio la capacitacion, tal como exige OBL-CAP-01.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 31 | Si |

- Fundamento: OBL-CAP-01 (Art. 4 (Medidas Organizativas, lit. c), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-SEG-02 (Art. 4 (Medidas Organizativas, lit. a-f), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: HU-017-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un TrainingProgram en estado Vigente, cuando lo asigno a una persona activa de mi area, entonces se crea un TrainingRecord en estado Programada referenciando esa persona y ese programa, con el tema y la modalidad heredados del programa.
2. Dado un TrainingRecord en Programada, cuando registro la fecha en que la persona recibio la capacitacion, confirmo la modalidad y adjunto la constancia o marco el acuse electronico, entonces el registro pasa a Completada.
3. Dado que intento marcar un TrainingRecord como Completada sin haber adjuntado ningun archivo de constancia ni marcado el acuse electronico, cuando confirmo la accion, entonces el sistema la rechaza porque la constancia o el acuse es obligatorio antes de Completada.
4. Dado que intento registrar una fecha de capacitacion posterior al dia de hoy, cuando guardo el registro, entonces el sistema rechaza la fecha porque no puede ser futura.
5. Dado un TrainingRecord en Programada cuya fecha programada ya paso sin registrar asistencia, cuando el sistema revisa los registros vencidos, entonces lo cambia automaticamente a No asistio y genera una alerta de nivel WARNING.
6. Dado un TrainingRecord en No asistio, cuando lo reprogramo indicando un motivo obligatorio, entonces vuelve a Programada y el motivo queda en el historial.
7. Dado que intento asignar o registrar una capacitacion de una persona de un area distinta a la mia, cuando confirmo la accion, entonces el sistema me la deniega porque mi alcance como Responsable de area se limita a mi propia area.

**Reglas de negocio**

- Constancia o acuse es obligatorio antes de marcar Completada (seccion D.2); el texto de ayuda advierte no adjuntar el expediente laboral completo, solo la constancia de esa sesion.
- Fecha en que recibio la capacitacion no puede ser futura (seccion D.2).
- Transiciones de TrainingRecord segun la tabla F.2: Programada a Completada exige constancia; Programada a No asistio es automatico al pasar la fecha; No asistio a Programada exige motivo.
- Persona debe existir y estar Activa en MOD-001 (seccion D.2), y se referencia por nombre, correo, cargo, area y rol, nunca se duplica su expediente laboral.
- El campo Origen del registro se marca automaticamente como Manual cuando la asignacion la hace una persona (seccion D.2).

**Fuera de alcance**

- Confirmacion de la propia asistencia por la persona capacitada (autoservicio), cubierta en HU-017-04.
- Creacion automatica del registro por induccion, cambio de rol o renovacion, cubiertas en HU-017-05, HU-017-06 y HU-017-07.
- Evaluacion de si el contenido de la capacitacion es correcto o suficiente: el sistema solo registra que existio.

- Requiere contenido: Plantilla de constancia de asistencia, para las empresas que no cuenten con una propia (seccion K).
- Referencia: MOD-017 seccion D.2, seccion F.2 y su tabla de transiciones de TrainingRecord, seccion C

### HU-017-04. Confirmar mi propia asistencia a una capacitacion asignada

**Como** Usuario de consulta / Colaborador, **quiero** ver las capacitaciones que se me asignaron y confirmar mi propia asistencia adjuntando mi constancia, **para** dejar constancia de que recibi la capacitacion sin depender de que otra persona lo registre por mi.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 32 | No |

- Fundamento: OBL-CAP-01 (Art. 4 (Medidas Organizativas, lit. c), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: HU-017-02, HU-017-03
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que tengo TrainingRecord asignados, cuando entro a mi vista de capacitaciones, entonces veo unicamente los registros que me corresponden a mi, con su tema, modalidad y estado.
2. Dado un TrainingRecord propio en Programada, cuando confirmo la fecha en que recibi la capacitacion y adjunto mi constancia o marco el acuse electronico, entonces el registro pasa a Completada.
3. Dado que intento confirmar mi asistencia sin adjuntar constancia ni marcar el acuse electronico, cuando guardo, entonces el sistema rechaza la accion porque la constancia o el acuse es obligatorio.
4. Dado que intento ver o completar un TrainingRecord que no me pertenece, cuando abro esa pantalla, entonces el sistema me lo deniega.
5. Dado que mi TrainingRecord corresponde a la capacitacion especifica del rol Delegado de Proteccion de Datos, cuando lo completo por autoservicio, entonces la constancia queda igualmente visible para Administrador y Auditor, sin ocultarse por tratarse del Delegado.

**Reglas de negocio**

- Autoservicio: la propia persona puede registrar y cerrar su TrainingRecord (seccion C).
- Constancia o acuse obligatorio antes de Completada (seccion D.2).
- El autoservicio del Delegado no oculta la constancia a Administrador ni Auditor (seccion C, nota de separacion de funciones).

**Fuera de alcance**

- Asignacion de la capacitacion a la persona, que la crea otro rol o una automatizacion (HU-017-03, HU-017-05, HU-017-06).
- Reprogramar un registro en No asistio, que corresponde a Responsable de area o Delegado.

- Referencia: MOD-017 seccion C (fila Usuario de consulta / Colaborador) y nota de separacion de funciones

### HU-017-05. Crear automaticamente la induccion de un usuario nuevo dado de alta

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** que se cree automaticamente un TrainingRecord de induccion y una tarea con fecha limite cuando se da de alta un usuario nuevo en MOD-001, **para** que ninguna persona nueva empiece a tratar datos personales sin que su induccion quede programada desde el primer dia.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 32 | No |

- Fundamento: OBL-CAP-01 (Art. 4 (Medidas Organizativas, lit. c), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: HU-017-02, HU-017-03
- Modulos requeridos: MOD-001, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que se da de alta un usuario nuevo en MOD-001, cuando el alta se confirma, entonces el sistema crea automaticamente un TrainingRecord en Programada de tipo Induccion de personal nuevo para esa persona, con Origen del registro Induccion automatica al alta (MOD-001).
2. Dado que se creo ese TrainingRecord, cuando el sistema lo procesa, entonces crea en MOD-021 una tarea Completar induccion de [persona] con fecha limite igual a la fecha de alta mas los dias configurados (30 por defecto), dirigida al Responsable de area (RRHH) con copia a la persona nueva.
3. Dado que pasan los dias configurados desde el alta sin que la induccion este Completada, cuando el sistema revisa los pendientes, entonces genera la alerta Induccion pendiente de nuevo ingreso de nivel WARNING hacia el Responsable de area con copia al Delegado, con recordatorio cada 5 dias.
4. Dado que la alerta de induccion pendiente sigue activa 30 dias mas (60 dias desde el alta) sin completarse, cuando se cumple ese plazo, entonces la alerta escala al Administrador de la organizacion.
5. Dado que no existe ningun TrainingProgram Vigente de tipo Induccion de personal nuevo en la organizacion, cuando se da de alta un usuario nuevo, entonces el sistema no puede crear el TrainingRecord de induccion y genera una alerta hacia el Delegado y el Administrador para que publiquen un programa de induccion.
6. Dado que se completa la induccion antes del plazo, cuando el TrainingRecord pasa a Completada, entonces la alerta de induccion pendiente se apaga.

**Reglas de negocio**

- La creacion del TrainingRecord de induccion al alta no se puede desactivar; solo los dias de plazo son configurables (seccion G, fila 1).
- La alerta de induccion pendiente escala a Administrador a los 60 dias desde el alta si no se completa (seccion I).

**Fuera de alcance**

- Registrar la asistencia en si (marcar Completada), cubierta en HU-017-03 y HU-017-04.
- Crear o publicar el programa de Induccion de personal nuevo, cubierta en HU-017-02.

- Referencia: MOD-017 seccion G automatizacion 1; seccion I fila Induccion pendiente de nuevo ingreso; seccion E

### HU-017-06. Asignar automaticamente la capacitacion por rol al cambiar de rol un usuario

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** que se asigne automaticamente el programa de capacitacion por rol correspondiente cuando una persona de mi area cambia a un rol con capacitacion asociada, **para** que quien asume Responsable ARCO-POL, Responsable de Seguridad/IT, RRHH o Marketing quede cubierto por la capacitacion que su nueva funcion requiere sin tener que recordarlo manualmente.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 32 | No |

- Fundamento: OBL-CAP-01 (Art. 4 (Medidas Organizativas, lit. c), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: HU-017-02, HU-017-03
- Modulos requeridos: MOD-001, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que un usuario cambia a un rol que tiene un TrainingProgram Vigente de tipo Por rol especifico asociado, cuando el cambio de rol se confirma en MOD-001, entonces el sistema crea automaticamente un TrainingRecord en Programada para esa persona y ese programa, con Origen del registro Asignacion por cambio de rol (MOD-001).
2. Dado que el rol nuevo no tiene ningun TrainingProgram Vigente de tipo Por rol asociado, cuando ocurre el cambio de rol, entonces el sistema no crea ningun TrainingRecord.
3. Dado que la asociacion entre un rol y un programa es configurable por la empresa, cuando el Administrador o el Delegado la definen, entonces el sistema usa esa asociacion para decidir si dispara la creacion automatica.
4. Dado que pasan los dias configurados (15 por defecto) desde el cambio de rol sin completar el TrainingRecord, cuando el sistema revisa los pendientes, entonces genera la alerta Capacitacion por rol faltante tras cambio de rol de nivel WARNING hacia el Responsable de area y el Delegado, con recordatorio cada 5 dias y escalamiento al Delegado a los 15 dias.
5. Dado que se completa el TrainingRecord antes del plazo, cuando pasa a Completada, entonces la alerta de capacitacion por rol faltante se apaga.

**Reglas de negocio**

- La asociacion entre rol y programa por rol es configurable por la empresa (seccion G, fila 2).
- La alerta de capacitacion por rol faltante escala al Delegado a los 15 dias (seccion I).

**Fuera de alcance**

- Crear o publicar el programa Por rol especifico, cubierta en HU-017-02.
- Registrar la asistencia en si, cubierta en HU-017-03 y HU-017-04.

- Referencia: MOD-017 seccion G automatizacion 2; seccion I fila Capacitacion por rol faltante tras cambio de rol

### HU-017-07. Calcular y ejecutar la renovacion automatica de una capacitacion

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que el sistema calcule la proxima renovacion de cada capacitacion completada, avise antes de que venza y cree automaticamente un nuevo registro si vence sin renovarse, **para** que ninguna capacitacion con periodicidad de renovacion quede vencida sin que nadie lo note.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 32 | No |

- Fundamento: OBL-CAP-01 (Art. 4 (Medidas Organizativas, lit. c), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: HU-017-03
- Modulos requeridos: MOD-023, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado un TrainingRecord que pasa a Completada y cuyo programa relacionado tiene una periodicidad de renovacion distinta de Sin renovacion, cuando se completa, entonces el sistema calcula el campo Proxima renovacion como la fecha de la capacitacion mas la periodicidad del programa, usando el motor de calendario de MOD-023.
2. Dado un TrainingRecord Completada, cuando faltan los dias de anticipacion configurados (30 por defecto) para su Proxima renovacion, entonces el sistema lo cambia a Proxima a vencer y crea en MOD-021 una tarea de renovacion para la persona, con alerta INFO que sube a WARNING a 5 dias del vencimiento.
3. Dado un TrainingRecord en Proxima a vencer, cuando se cumple la fecha de Proxima renovacion sin un nuevo registro Completada, entonces el sistema lo cambia a Vencida, genera la alerta HIGH hacia la persona, el Responsable de area y el Delegado, y crea automaticamente un nuevo TrainingRecord en Programada para el mismo programa y persona.
4. Dado un TrainingRecord en Proxima a vencer o Vencida, cuando se registra un nuevo TrainingRecord Completada para el mismo programa y persona, entonces la alerta correspondiente se apaga y el registro vencido conserva su estado historico sin reescribirse.
5. Dado un TrainingRecord Vencida cuya alerta HIGH sigue activa 15 dias, cuando se cumple ese plazo, entonces la alerta escala al Delegado.
6. Dado un programa cuya periodicidad de renovacion es Sin renovacion, cuando su TrainingRecord pasa a Completada, entonces el sistema no calcula ninguna Proxima renovacion ni genera ningun ciclo de vencimiento.

**Reglas de negocio**

- Proxima renovacion se calcula siempre contra MOD-023, nunca con una fecha fija local (seccion P riesgos).
- La renovacion es siempre un TrainingRecord nuevo, nunca reescribe el registro vencido anterior (seccion F.2).
- Vencida es terminal para esa instancia especifica; el nuevo registro de renovacion sigue su propio ciclo desde Programada (seccion F.2).

**Fuera de alcance**

- Registrar la asistencia del nuevo TrainingRecord de renovacion en si, cubierta en HU-017-03 y HU-017-04.

- Referencia: MOD-017 seccion G automatizaciones 3 y 4; seccion F.2; seccion I fila Capacitacion proxima a vencer / vencida

### HU-017-08. Notificar a MOD-002 la constancia de capacitacion del Delegado

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que cada vez que complete mi propia capacitacion especifica el sistema avise al expediente del Delegado en MOD-002, **para** que esa constancia quede disponible como insumo de mi capacitacion anual (OBL-DPO-05) y de mi reverificacion cada 3 anos (OBL-DPO-04), sin tener que cargarla dos veces.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 32 | No |

- Fundamento: OBL-DPO-04 (Art. 18, Lineamientos para el Delegado de Proteccion de Datos Personales); OBL-DPO-05 (Art. 22, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-017-03
- Modulos requeridos: MOD-002, MOD-022

**Criterios de aceptacion**

1. Dado que se completa un TrainingRecord cuyo programa tiene como rol destinatario a Delegado de Proteccion de Datos, cuando el registro pasa a Completada, entonces el sistema notifica a MOD-002 que hay una constancia nueva disponible para el campo fecha_ultima_capacitacion_delegado, sin escribir ese campo directamente.
2. Dado que la persona con rol Delegado completa cualquier TrainingRecord dentro de la ventana de su ciclo de reverificacion de 3 anos, cuando el registro pasa a Completada, entonces esa constancia queda disponible como adjunto sugerido para cuando MOD-002 inicie el flujo de reverificacion del perfil del delegado.
3. Dado que se envia la notificacion hacia MOD-002, cuando reviso el historial del modulo, entonces encuentro el evento con fecha y referencia al TrainingRecord de origen.
4. Dado un TrainingRecord Completada cuyo programa no tiene como rol destinatario a Delegado de Proteccion de Datos, cuando se completa, entonces el sistema no genera ninguna notificacion hacia MOD-002.
5. Dado que la notificacion ya se envio para un TrainingRecord, cuando ese mismo registro se consulta de nuevo, entonces el sistema no la duplica ni la reenvia.

**Reglas de negocio**

- MOD-017 conserva el registro original; MOD-002 solo referencia o adjunta la constancia, sin duplicar el campo (seccion D.2, precarga).
- MOD-017 nunca escribe directamente los campos fecha_ultima_capacitacion_delegado ni atestados_reverificacion de MOD-002, solo notifica (seccion G, automatizaciones 8 y 9).

**Fuera de alcance**

- Escribir o aprobar los campos de MOD-002, que sigue siendo el propietario de esa obligacion y de esos campos.
- El flujo de reverificacion del perfil del delegado en si, que administra MOD-002.

- Referencia: MOD-017 seccion G automatizaciones 8 y 9; seccion D.2 precarga; seccion E

### HU-017-09. Elaborar el borrador del plan anual de capacitacion e induccion

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** elaborar el borrador del plan anual de capacitacion e induccion agregando los programas del ano y el documento formal del plan, **para** cumplir con el deber de elaborar ese plan mientras exista la figura del Delegado en la empresa.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 32 | No |

- Fundamento: OBL-CAP-02 (Art. 22, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-017-02
- Modulos requeridos: MOD-002, MOD-008

**Criterios de aceptacion**

1. Dado que soy Delegado de Proteccion de Datos o Responsable interno activo en MOD-002, cuando creo un TrainingProgram de Tipo Plan anual, entonces el sistema exige que el campo Elaborado / propuesto por sea un usuario con ese rol activo.
2. Dado que elaboro el plan anual, cuando selecciono los Programas incluidos, entonces el sistema exige al menos un programa y valida que incluya al menos un programa de Tipo Induccion de personal nuevo antes de permitir publicarlo.
3. Dado que el plan esta en Borrador, cuando adjunto o referencio el Documento del plan, entonces el sistema lo vincula al mismo documento por referencia que se muestra en el campo plan_capacitacion_personal de MOD-002, sin duplicarlo.
4. Dado que el Responsable Legal / Compliance co-edita el borrador del plan, cuando guarda sus cambios, entonces el sistema los registra en el historial igual que los del Delegado.
5. Dado que intento publicar el plan anual sin haber incluido ningun programa de Tipo Induccion de personal nuevo, cuando confirmo la publicacion, entonces el sistema la rechaza y muestra que falta ese programa obligatorio.
6. Dado que un usuario sin el rol Delegado, Responsable interno o Responsable Legal intenta elaborar o editar el plan anual, cuando lo intenta, entonces el sistema le deniega la accion, salvo el Administrador en una organizacion pyme, que puede hacerlo con una advertencia visible de autorrevision.

**Reglas de negocio**

- Elaborado / propuesto por es obligatorio y debe tener rol Delegado o Responsable interno activo en MOD-002 cuando Tipo = Plan anual (seccion D.1).
- Programas incluidos debe tener al menos un programa y al menos uno de Tipo Induccion de personal nuevo (seccion D.1).
- Documento del plan se enlaza por referencia con el campo plan_capacitacion_personal de MOD-002, sin duplicarse (seccion D.1 y nota final punto 3).
- Periodicidad del plan anual es fija de 1 ano (seccion D.1).

**Fuera de alcance**

- Aprobar y publicar el plan (cambio de Borrador a Vigente), cubierta en HU-017-10.
- Creacion de programas General, Induccion o Por rol individuales, cubierta en HU-017-02.

- Referencia: MOD-017 seccion D.1 (filas Elaborado/propuesto por, Programas incluidos, Documento del plan); seccion C; seccion F.1

### HU-017-10. Aprobar y publicar el plan anual de capacitacion e induccion

**Como** Aprobador, **quiero** aprobar y publicar el plan anual de capacitacion e induccion elaborado por el Delegado, **para** que el plan quede como version oficial solo despues de una revision separada de quien lo elaboro.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 32 | No |

- Fundamento: OBL-CAP-02 (Art. 22, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-017-09
- Modulos requeridos: MOD-002, MOD-008, MOD-019

**Criterios de aceptacion**

1. Dado un plan anual en Borrador con Elaborado por, Programas incluidos con induccion y Documento del plan completos, cuando lo apruebo y publico, entonces el sistema exige que yo, como Aprobador, sea una persona distinta de quien lo elaboro.
2. Dado que la organizacion esta por debajo del umbral configurable de separacion de funciones, cuando la misma persona que elaboro el plan intenta tambien aprobarlo, entonces el sistema lo permite pero muestra una advertencia visible de autorrevision.
3. Dado que publico el plan anual, cuando la publicacion se confirma, entonces el TrainingProgram pasa a Vigente, el documento queda enviado a MOD-019 con verificacion de integridad, y se notifica a MOD-002 para actualizar por referencia su campo plan_capacitacion_personal.
4. Dado que se publica una nueva version del plan anual, cuando la version anterior deja de ser la vigente, entonces esa version anterior pasa a Archivado y se conserva integra para consulta, sin reescritura retroactiva de su caracter de obligatorio en el momento en que se publico.
5. Dado que intento publicar el plan anual sin que exista el Documento del plan referenciado, cuando confirmo la publicacion, entonces el sistema la rechaza.
6. Dado que se publica el plan anual, cuando reviso el historial, entonces encuentro el evento de publicacion con la identidad de quien lo elaboro y de quien lo aprobo.
7. Dado un usuario sin el rol Aprobador, cuando intenta aprobar o publicar el plan anual, entonces el sistema le deniega la accion.

**Reglas de negocio**

- Publicar el plan anual exige un Aprobador distinto de quien lo elaboro, salvo pyme por debajo del umbral configurable, con advertencia de autorrevision (seccion C, separacion de funciones).
- Al publicarse, el documento queda en MOD-019 con verificacion de integridad y se notifica a MOD-002 (seccion F.1; seccion G automatizacion 10).
- Ninguna version publicada se elimina; una version archivada sigue siendo consultable (seccion F.1).

**Fuera de alcance**

- Elaborar o editar el contenido del borrador, cubierta en HU-017-09.

- Requiere contenido: Plantilla Plan anual de capacitacion e induccion, marcada como borrador que requiere revision y aprobacion de la organizacion antes de considerarse el plan oficial (seccion K).
- Requiere validacion legal: Si
- Referencia: MOD-017 seccion F.1 (transicion Borrador a Vigente del Plan anual); seccion C separacion de funciones; seccion G automatizacion 10; seccion K

### HU-017-11. Recibir recordatorio para elaborar o actualizar el plan anual antes de su vencimiento

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** recibir una tarea y una alerta antes de que se cumpla el aniversario del plan anual publicado, **para** no dejar vencer el ciclo anual del plan de capacitacion e induccion que debo elaborar.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 32 | No |

- Fundamento: OBL-CAP-02 (Art. 22, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-017-09, HU-017-10
- Modulos requeridos: MOD-023, MOD-021, MOD-022, MOD-002

**Criterios de aceptacion**

1. Dado que existe un usuario con rol Delegado o Responsable interno activo en MOD-002 y falta 60 dias para el aniversario del ultimo plan anual publicado (o nunca existio uno), bajo la bandera regimen_reforma_659 en ACTUAL, cuando el sistema revisa los ciclos anuales, entonces crea en MOD-021 la tarea Elaborar/actualizar el plan anual de capacitacion e induccion dirigida a esa persona, calculando la fecha con MOD-023.
2. Dado que la tarea ya se creo a los 60 dias, cuando faltan 30 dias para el vencimiento del ciclo, entonces el sistema genera un recordatorio adicional de la misma tarea.
3. Dado que pasa la fecha del ciclo anual sin que se publique un nuevo plan, cuando el sistema revisa el vencimiento, entonces genera la alerta Plan anual vencido de nivel HIGH hacia el Delegado y el Administrador, con repeticion semanal.
4. Dado que la alerta de plan anual vencido sigue activa 15 dias sin iniciarse la elaboracion, cuando se cumple ese plazo, entonces escala al Administrador; y si siguen sin iniciarla 30 dias, escala ademas a Gerencia.
5. Dado que la alerta de plan anual vencido esta activa, cuando se muestra al usuario, entonces incluye el texto de advertencia de que la ausencia del plan anual podria leerse como incumplimiento de la medida organizativa de capacitacion, aclarando que esta lectura requiere validacion de asesoria juridica.
6. Dado que se publica el nuevo plan anual, cuando la publicacion se confirma, entonces tanto la tarea recordatoria como la alerta de plan anual vencido se apagan.

**Reglas de negocio**

- El recordatorio se crea a los 60 y a los 30 dias antes del vencimiento del ciclo anual, o si nunca existio un plan publicado (seccion G automatizacion 5).
- La alerta de plan anual vencido no atribuye una infraccion especifica a OBL-CAP-02 sin advertencia de validacion legal (seccion I, correccion de la nota final punto 5).

**Fuera de alcance**

- El efecto de la bandera regimen_reforma_659 en FUTURO sobre esta tarea recordatoria, cubierto en HU-017-12.

- Requiere validacion legal: Si
- Referencia: MOD-017 seccion G automatizacion 5; seccion I filas Plan anual proximo a vencer y Plan anual vencido

### HU-017-12. Aplicar el efecto de la bandera de la reforma 659 sobre el plan anual

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que el caracter obligatorio o de buena practica del plan anual se ajuste automaticamente segun la bandera regimen_reforma_659 de MOD-024, **para** no seguir tratando el plan anual como obligatorio, o dejar de elaborarlo, por error cuando cambia el regimen normativo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 33 | No |

- Fundamento: OBL-CAP-02 (Art. 22, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-017-09, HU-017-10, HU-017-11
- Modulos requeridos: MOD-024, MOD-002

**Criterios de aceptacion**

1. Dado que la bandera regimen_reforma_659 de MOD-024 esta en ACTUAL, cuando consulto un TrainingProgram de Tipo Plan anual, entonces el campo calculado Aplica bajo el regimen muestra Obligatorio (regimen ACTUAL).
2. Dado que la bandera regimen_reforma_659 pasa a FUTURO y no hay ningun usuario con tipo_rol Delegado activo en MOD-002 (ningun Delegado voluntario), cuando el sistema procesa el cambio, entonces el Plan anual vigente se marca Buena practica voluntaria (regimen FUTURO sin Delegado voluntario) en su ayuda contextual, y deja de generar la tarea recordatoria obligatoria de la automatizacion 5.
3. Dado que la bandera pasa a FUTURO pero la empresa mantiene un Delegado voluntario activo, cuando el sistema procesa el cambio, entonces el Plan anual sigue funcionando con la misma funcionalidad completa, cambiando solo el texto de ayuda contextual de obligatorio a buena practica recomendada.
4. Dado que la bandera cambia de ACTUAL a FUTURO o se revierte, cuando el sistema recalcula el campo Aplica bajo el regimen, entonces el registro general de capacitacion del personal (OBL-CAP-01) continua exactamente igual, sin cambio de estado ni de comportamiento.
5. Dado un plan anual que ya fue publicado antes de un cambio de bandera, cuando la bandera cambia despues, entonces esa version publicada conserva su version y su caracter de obligatorio del momento en que se publico, sin reescritura retroactiva.
6. Dado que el sistema no puede inferir por si solo si la empresa decidio mantener un Delegado voluntario, cuando procesa el cambio de bandera, entonces se apoya siempre en el dato de continuidad voluntaria que documenta MOD-002, nunca en una deduccion propia.

**Reglas de negocio**

- El campo Aplica bajo el regimen se recalcula siempre contra la bandera unica de MOD-024, nunca contra una copia local (seccion D.1; seccion P riesgos).
- El cambio de bandera no es el disparador de un nuevo estado del TrainingProgram, solo cambia una etiqueta y el disparo de la tarea recordatoria (seccion G automatizacion 6).
- OBL-CAP-01 nunca cambia bajo ningun escenario de la reforma 659 (seccion A, doble estado).

**Fuera de alcance**

- Decidir si la empresa mantiene o no un Delegado voluntario, decision que documenta y ejecuta MOD-002.
- Activar o revertir la bandera regimen_reforma_659 en si, que administra MOD-024.

- Requiere validacion legal: Si
- Referencia: MOD-017 seccion Doble estado de la reforma 659; seccion D.1 fila Aplica bajo el regimen; seccion G automatizacion 6; seccion H

### HU-017-13. Consultar los indicadores de capacitacion del personal

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** ver los indicadores de personal con capacitacion vigente, inducciones pendientes, vencimientos proximos, estado del plan anual y capacitacion por rol cubierta, **para** saber de un vistazo el estado del programa de capacitacion sin recorrer registro por registro.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 33 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-017-02, HU-017-03, HU-017-05, HU-017-06, HU-017-07, HU-017-09, HU-017-10
- Modulos requeridos: MOD-020, MOD-001

**Criterios de aceptacion**

1. Dado que consulto el indicador Personal con capacitacion general vigente, cuando lo abro, entonces veo el conteo de personas con al menos un TrainingRecord Completada de Tipo General con Proxima renovacion en el futuro, sobre el total de personal activo en MOD-001.
2. Dado que consulto el indicador Inducciones pendientes, cuando lo abro, entonces veo el conteo de personas dadas de alta hace mas del plazo configurado sin TrainingRecord Completada de tipo Induccion.
3. Dado que consulto el indicador Vencimientos proximos, cuando lo abro, entonces veo el conteo de TrainingRecord en estado Proxima a vencer, en amarillo si hay alguno y en rojo si alguno vence en menos de 5 dias.
4. Dado que consulto el indicador Estado del plan anual, cuando lo abro, entonces veo el semaforo cruzado con la bandera regimen_reforma_659: verde si esta Vigente y publicado dentro del ciclo, amarillo si esta Proxima a vencer, rojo si esta Vencida bajo regimen ACTUAL, o gris No aplica bajo el regimen actual si esta en FUTURO sin Delegado voluntario.
5. Dado que consulto el indicador Capacitacion por rol cubierta, cuando lo abro, entonces veo el conteo de personas con un rol destinatario especifico que tienen al menos un TrainingRecord Completada del programa Por rol correspondiente, sobre el total de personas con ese rol activo.
6. Dado un usuario con rol Responsable de area, cuando consulta estos indicadores, entonces solo ve el detalle de su propia area, nunca el agregado de otras areas.
7. Dado que ningun indicador de este modulo debe expresarse como porcentaje de cumplimiento legal, cuando reviso cualquiera de ellos, entonces el texto usa siempre personal con capacitacion vigente, inducciones pendientes o vencimientos proximos, junto con el banner de descargo estandar del sistema.

**Reglas de negocio**

- Ningun indicador se expresa como porcentaje de cumplimiento legal (seccion M).
- Responsable de area ve solo el detalle de su propia area (seccion M, columna Vista por rol).

**Fuera de alcance**

- El calculo de riesgo o de cumplimiento juridico: el modulo nunca lo declara.

- Referencia: MOD-017 seccion M

### HU-017-14. Exportar reportes y listados de capacitacion del personal

**Como** Responsable Legal / Compliance, **quiero** exportar el listado de capacitaciones por persona, el historial por area o rol, el plan anual con su historial de versiones y el listado de vencimientos e inducciones pendientes, **para** entregar evidencia verificable de la capacitacion del personal a Gerencia, a un Auditor o a la ACE si la requiere.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 33 | No |

- Fundamento: OBL-CAP-01 (Art. 4 (Medidas Organizativas, lit. c), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-CAP-02 (Art. 22, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-017-03, HU-017-09, HU-017-10
- Modulos requeridos: MOD-019

**Criterios de aceptacion**

1. Dado que exporto el Listado de capacitaciones por persona, cuando elijo una persona y un rango de fechas, entonces obtengo un archivo en PDF o XLSX con fecha, tema y constancia de cada TrainingRecord de esa persona.
2. Dado que exporto el Historial de capacitaciones por area o rol, cuando elijo un area, un rol o un periodo, entonces obtengo un archivo XLSX con el conteo y detalle de TrainingRecord agrupados segun ese filtro.
3. Dado que exporto el Plan anual de capacitacion e induccion, cuando elijo un ano, entonces obtengo un PDF con el contenido completo de la version vigente y el historial de versiones anteriores.
4. Dado que exporto el listado de Vencimientos e inducciones pendientes, cuando elijo un estado y un area, entonces obtengo un archivo CSV con las personas en capacitacion vencida o induccion pendiente.
5. Dado que genero cualquiera de estas exportaciones, cuando la exportacion se completa, entonces el sistema registra en el historial quien la genero y cuando, y la deja disponible como parte del paquete de evidencia en MOD-019, salvo el listado de vencimientos e inducciones pendientes, que es de gestion interna.
6. Dado un usuario con rol Responsable de area, cuando exporta estos reportes, entonces solo puede hacerlo con el alcance de su propia area.
7. Dado un usuario con rol Usuario de consulta / Colaborador o Aprobador, cuando intenta exportar cualquiera de estos reportes, entonces el sistema le deniega la accion porque no esta entre los roles habilitados para exportar.

**Reglas de negocio**

- El listado de Vencimientos e inducciones pendientes no forma parte del paquete de evidencia, es de gestion interna (seccion N).
- Toda exportacion queda registrada en el historial con quien la genero y cuando (seccion O).

**Fuera de alcance**

- El paquete de evidencia consolidado por obligacion, que administra MOD-019 directamente.

- Referencia: MOD-017 seccion N; seccion C fila Exportar

### HU-017-15. Recibir sugerencia de capacitacion a partir de una leccion aprendida de un incidente

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** recibir una tarea sugerida cuando se cierra un incidente de seguridad con una leccion aprendida que senala necesidad de capacitacion, **para** valorar si hace falta crear o actualizar un programa de capacitacion por rol, sin que el sistema lo cree por si solo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R2 | 33 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-017-02
- Modulos requeridos: MOD-013, MOD-021

**Criterios de aceptacion**

1. Dado que se cierra un incidente en MOD-013 y la persona que lo cierra marca que la leccion aprendida senala necesidad de capacitacion, cuando el cierre se confirma, entonces el sistema crea en MOD-021 una tarea sugerida Evaluar capacitacion por leccion aprendida de tipo Capacitacion con origen MOD-013, dirigida al Delegado y al Responsable de Seguridad/IT.
2. Dado que se crea esa tarea sugerida, cuando reviso el catalogo de TrainingProgram, entonces confirmo que el sistema no creo ni modifico ningun programa por si solo.
3. Dado que la tarea sugerida sigue abierta mas de 15 dias, cuando el sistema revisa las tareas pendientes, entonces genera la alerta INFO Sugerencia de capacitacion por leccion aprendida sin atender con un recordatorio a los 15 dias, sin escalar automaticamente.
4. Dado que marco la tarea como atendida o la descarto con un motivo, cuando confirmo la accion, entonces la alerta se apaga y el motivo queda en el historial.
5. Dado que se cierra un incidente sin marcar la opcion de leccion aprendida que senala necesidad de capacitacion, cuando el cierre se confirma, entonces el sistema no crea ninguna tarea sugerida de capacitacion.

**Reglas de negocio**

- La tarea siempre pasa por MOD-021, nunca es una escritura directa entre MOD-013 y MOD-017 (seccion L).
- Crear o ajustar el programa a partir de esta sugerencia es siempre una decision humana del Delegado o del Responsable de Seguridad/IT (seccion H).

**Fuera de alcance**

- Crear o versionar el programa de capacitacion resultante, cubierta en HU-017-02 si el Delegado decide hacerlo.

- Referencia: MOD-017 seccion G automatizacion 7; seccion H; seccion I fila Sugerencia de capacitacion por leccion aprendida sin atender

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Registro general de capacitacion del personal (quien, cuando, tema, modalidad, version del material, constancia, proxima renovacion) | HU-017-02, HU-017-03, HU-017-04 |
| Induccion automatica de personal nuevo (mismo mecanismo del registro general, disparada al alta en MOD-001) | HU-017-02, HU-017-05 |
| Capacitacion por rol (catalogo de programas dirigidos a Responsable ARCO-POL, Responsable de Seguridad/IT, RRHH, Marketing) | HU-017-02, HU-017-06 |
| Recordatorio y renovacion automatica (calculo de proxima renovacion, alertas, nuevo registro al vencer) | HU-017-07 |
| Plan anual de capacitacion e induccion en su version minima (agregacion automatica de los programas del ano, elaborado por el Delegado, con aprobacion separada y exportacion como documento) | HU-017-09, HU-017-10, HU-017-11 |
| Notificacion de constancias hacia MOD-002 para sus campos de capacitacion y reverificacion del Delegado (OBL-DPO-04, OBL-DPO-05) | HU-017-08 |
