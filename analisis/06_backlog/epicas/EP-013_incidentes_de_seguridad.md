# EP-013 Incidentes de Seguridad (MOD-013)

**Objetivo.** Permitir que la empresa gestione un incidente de seguridad de datos personales de principio a fin, desde que alguien lo reporta hasta su cierre y conservacion, con los dos cronometros de 72 horas del Articulo 25 siempre visibles, las notificaciones diferenciadas a la ACE, a la Fiscalia General de la Republica y a los titulares, y el expediente documentado como prueba de descargo.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R2 | 19 | 96 | 0 | 96 | [MOD-013](../../03_modulos/MOD-013_ficha.md) |

**Notas de la epica.**

- Se sigue la tabla Q de la ficha (8 filas MUST HAVE, ver cobertura_q): registro y flujo completo de estados, los dos cronometros de 72 horas en paralelo con criterio de horas corridas por defecto, plantillas diferenciadas de notificacion, documentacion obligatoria con bloqueo, checklist de las 72 horas, vinculo con el catalogo de MOD-015, constancia de envio con hash y alertas de cronometro. No se construyen las filas SHOULD HAVE ni COULD HAVE de la misma tabla: referencia informativa completa al proveedor/encargado de origen, creacion de tarea de Evaluacion de Impacto con cuestionario de scoring, flujo condicional completo del Decreto 143, alertas por canales adicionales, flujo guiado de reapertura por motivo y dashboard comparativo por proveedor. La seccion 19.3 del roadmap describe la misma version minima (flujo de origen interno, sin dependencia obligatoria de Proveedores ni de Decreto 143) y no discrepa con la tabla Q.
- Discrepancia relevante 1 (criterio de las 72 horas): la ficha de MOD-013 (seccion D.4) describe el campo Criterio de computo del plazo de 72 horas aplicado como editable con justificacion dentro del cuerpo principal, sin marcarlo por si solo como SHOULD HAVE en la tabla Q de este modulo. Sin embargo, la ficha de MOD-023 (seccion Q) clasifica la configurabilidad de ese cambio, con el mecanismo de doble control entre Delegado y Legal, como SHOULD HAVE, y el roadmap (04_secciones/19_21_roadmap_mvp_v1_v2.md, seccion 20, area de Calendario mas fino) la ubica en V1. Se siguio el criterio mas restrictivo: HU-013-02 y HU-013-11 solo aplican y muestran el criterio conservador por defecto (horas corridas); cambiar el criterio a horas habiles queda fuera de esta epica hasta que MOD-023 construya esa pieza.
- Discrepancia relevante 2 (proveedor de origen): la tabla Q de MOD-013 y el caso 9 (04_secciones/08d_workflows_casos_09_11.md, tabla Cobertura por version) clasifican como SHOULD HAVE, no bloqueante, la referencia informativa al proveedor/encargado de origen y su plazo pactado de aviso, y el parrafo de version minima vendible de la propia ficha aclara que el MVP cubre el flujo completo de un incidente de origen interno sin dependencia obligatoria de Proveedores. Sin embargo, el campo D.1 Proveedor/Encargado relacionado se describe con una validacion que exige que el proveedor exista en MOD-009. Se siguio la tabla Q: HU-013-03 registra el origen del incidente (incluida la opcion Proveedor/Encargado) pero no exige ni valida el vinculo con un registro especifico de MOD-009, y la alerta de proveedor sin evidencia de aviso queda fuera de alcance.
- Discrepancia relevante 3 (modulos SHOULD HAVE referenciados por la ficha): MOD-014 (Riesgos y EIPD) y MOD-016 (Retencion y Eliminacion) son SHOULD HAVE y no aparecen en la lista de modulos de R1 ni de R2 que dan las instrucciones de esta tarea (seccion 6), aunque la ficha de MOD-013 los menciona como destino de una tarea y de un envio, respectivamente. Siguiendo el mecanismo de cobertura parcial que documentan la seccion 19.4 del roadmap y las propias fichas de MOD-014 y MOD-016 (seccion Q y notas finales de cada una), HU-013-07 crea la tarea de Evaluacion de Impacto de forma generica hacia el Centro de Tareas (MOD-021), sin cuestionario de scoring y sin depender de MOD-014; y HU-013-14 calcula la fecha de conservacion y protege el expediente cerrado contra el borrado de forma pasiva, sin depender de que MOD-016 exista como modulo construido.
- El campo condicional de operador de infraestructura critica (Decreto 143, OBL-INC-05) se mantiene visible en modo lectura dentro de la Evaluacion (HU-013-07), tal como permite la propia justificacion de la tabla Q (el campo esta disponible desde el MVP), pero el flujo operativo completo de ese reporte adicional, marcado SHOULD HAVE en la misma tabla, queda fuera de esta epica.
- Dos preguntas juridicas pendientes (PP-JUR-01 y PP-JUR-02, 04_secciones/24_preguntas_pendientes.md) afectan directamente el computo de las 72 horas; mientras no se resuelvan, el modulo aplica siempre el criterio conservador de horas corridas con la advertencia de incertidumbre visible, segun la decision 2.7.11 que cita la propia ficha. Ambas preguntas se citan en HU-013-02.
- OBL-RET-05 (retencion del expediente cerrado) es de clasificacion RECOMENDADO en la matriz de obligaciones, sin norma expresa que fije el plazo de 5 anos, y requiere validacion de abogado; HU-013-14 se marca en consecuencia con requiere_validacion_legal en verdadero.
- No se redacta ninguna HU de ayuda contextual dedicada: el encargo de esta epica no la señalo como indicacion especifica, y el contenido de ayuda de la ficha (seccion R) se referencia solo como texto de apoyo dentro de los criterios de aceptacion y como requiere_contenido de HU-013-17.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-013-01 | Reportar un incidente de seguridad | Responsable de Seguridad / IT | 3 | R2 | 23 | - |
| HU-013-02 | Confirmar la fecha de conocimiento y arrancar los dos cronometros de 72 horas | Responsable de Seguridad / IT | 8 | R2 | 29 | HU-013-01, MOD-023, MOD-021, MOD-022 |
| HU-013-03 | Clasificar el incidente en Triage | Responsable de Seguridad / IT | 5 | R2 | 29 | HU-013-02, MOD-006 |
| HU-013-04 | Descartar un incidente en Triage por no ser una vulneracion de datos personales | Responsable de Seguridad / IT | 3 | R2 | 29 | HU-013-02 |
| HU-013-05 | Registrar el inicio de la revision exhaustiva del incidente | Responsable de Seguridad / IT | 5 | R2 | 29 | HU-013-03, MOD-023 |
| HU-013-06 | Registrar acciones de contencion inmediata | Responsable de Seguridad / IT | 3 | R2 | 27 | HU-013-01 |
| HU-013-07 | Evaluar el alcance, impacto y riesgo del incidente con bloqueo de documentacion obligatoria | Responsable de Seguridad / IT | 8 | R2 | 30 | HU-013-05, HU-013-06, MOD-021 |
| HU-013-08 | Decidir si corresponde la notificacion externa del incidente | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 30 | HU-013-07 |
| HU-013-09 | Completar el contenido y generar los borradores diferenciados de notificacion | Responsable de Seguridad / IT | 8 | R2 | 30 | HU-013-08 |
| HU-013-10 | Aprobar y marcar como enviada cada notificacion externa | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 8 | R2 | 30 | HU-013-09, MOD-019, MOD-023 |
| HU-013-11 | Recibir alertas y escalamiento de los dos cronometros de 72 horas | Responsable de Seguridad / IT | 8 | R2 | 30 | HU-013-02, MOD-022, MOD-023 |
| HU-013-12 | Registrar las medidas correctivas definitivas y la actualizacion de politicas | Responsable de Seguridad / IT | 5 | R2 | 31 | HU-013-10, MOD-015, MOD-021 |
| HU-013-13 | Completar la decision final de cierre del incidente | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 8 | R2 | 31 | HU-013-08, HU-013-12, MOD-001 |
| HU-013-14 | Enviar el expediente cerrado a conservacion sin borrado | Administrador de la organizacion | 3 | R2 | 31 | HU-013-13 |
| HU-013-15 | Reabrir un incidente cerrado o descartado | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 31 | HU-013-13, HU-013-04, MOD-021 |
| HU-013-16 | Registrar lecciones aprendidas tras el cierre | Responsable de Seguridad / IT | 2 | R2 | 31 | HU-013-13, MOD-015, MOD-017, MOD-021 |
| HU-013-17 | Consultar el checklist de las 72 horas del incidente | Responsable de Seguridad / IT | 3 | R2 | 30 | HU-013-02, MOD-023 |
| HU-013-18 | Consultar el listado de incidentes con filtros | Responsable Legal / Compliance | 3 | R2 | 31 | HU-013-01 |
| HU-013-19 | Exportar el expediente de un incidente como paquete de evidencia verificable | Auditor (interno) | 3 | R2 | 32 | HU-013-13, MOD-019 |

## Historias

### HU-013-01. Reportar un incidente de seguridad

**Como** Responsable de Seguridad / IT, **quiero** registrar un nuevo incidente de seguridad con los datos minimos iniciales (titulo, fecha y hora de deteccion, quien reporta), **para** dejar abierto el expediente desde el primer momento en que alguien nota algo anormal, sin esperar a tener toda la informacion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 23 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que no existe un incidente previo para este caso, cuando registro un titulo de al menos 5 caracteres, la fecha y hora de deteccion y confirmo quien reporta, entonces el sistema crea el expediente en estado Reportado y registra un evento de auditoria de incidente creado.
2. Dado que estoy registrando el incidente, cuando dejo el titulo con menos de 5 caracteres, entonces el sistema no permite guardar y muestra que el titulo es obligatorio con minimo 5 caracteres.
3. Dado que estoy registrando el incidente, cuando indico una fecha de deteccion posterior al momento actual, entonces el sistema rechaza el valor porque la fecha de deteccion no puede ser futura.
4. Dado que acabo de crear el expediente, cuando aun no he registrado la fecha y hora de conocimiento, entonces el sistema muestra una advertencia visible de que los dos cronometros de 72 horas todavia no han iniciado.
5. Dado un incidente recien creado en estado Reportado, cuando reviso el expediente, entonces el campo quien reporta aparece autocompletado con mi usuario y no puede quedar vacio.
6. Dado que soy un rol sin permiso de crear incidentes, por ejemplo Titular, Auditor interno, Auditor externo, Aprobador, Usuario de consulta o Asesor externo, cuando intento reportar un incidente, entonces el sistema deniega la accion.

**Reglas de negocio**

- El campo Origen del incidente y el resto de campos de clasificacion no son obligatorios en este paso; se piden progresivamente en estados posteriores, no todos a la vez.
- Nunca se elimina un incidente; solo se archiva o se descarta con justificacion.

**Fuera de alcance**

- Clasificacion del incidente (origen, tipo de vulneracion, categorias de datos), que se cubre en la HU de Triage.
- Arranque de los cronometros de 72 horas, que depende de registrar la fecha de conocimiento (HU aparte).

- Referencia: MOD-013 secciones D.1, F.1 y F.2 (transicion inicial), P (riesgo de abandono del formulario), Q

### HU-013-02. Confirmar la fecha de conocimiento y arrancar los dos cronometros de 72 horas

**Como** Responsable de Seguridad / IT, **quiero** registrar la fecha y hora exacta en que se tuvo conocimiento de la vulneracion, **para** que arranquen en paralelo el cronometro de notificacion y el de inicio de la revision exhaustiva, tal como exige el Articulo 25.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 29 | No |

- Fundamento: OBL-INC-01 (Art. 25, Ley para la Proteccion de Datos Personales); OBL-INC-02 (Art. 25 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-013-01
- Modulos requeridos: MOD-023, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado un incidente en estado Reportado, cuando registro la fecha y hora de conocimiento y no es futura, entonces el sistema pasa el incidente a Triage y arrancan en paralelo el cronometro de notificacion de 72 horas y el cronometro de revision exhaustiva de 72 horas, ambos calculados por el motor de plazos en horas corridas por defecto.
2. Dado que confirmo la fecha de conocimiento, cuando el sistema arranca ambos cronometros, entonces se crean automaticamente en el Centro de Tareas las tareas iniciar revision antes de la fecha limite y notificar antes de la fecha limite, cada una con responsable y fecha limite calculada por el motor de plazos.
3. Dado que confirmo la fecha de conocimiento, cuando el sistema arranca los cronometros, entonces se envia una alerta de nivel INFO al Responsable de Seguridad/IT y al Delegado informando el inicio del plazo.
4. Dado que intento registrar una fecha de conocimiento futura, cuando confirmo el valor, entonces el sistema rechaza el dato porque la fecha de conocimiento no puede ser futura.
5. Dado que la fecha de conocimiento que registro es posterior a la fecha de deteccion ya guardada, cuando intento guardar, entonces el sistema exige un campo de justificacion obligatorio antes de aceptar el valor.
6. Dado un incidente sin fecha de conocimiento registrada, cuando intento avanzar el estado a Triage sin completar este campo, entonces el sistema no permite el avance.
7. Dado que el criterio de computo aplicado es horas corridas por defecto, cuando visualizo cualquiera de los dos cronometros, entonces el sistema muestra siempre el texto de advertencia de que la ley no precisa si el plazo se cuenta en horas corridas u horas habiles y que se aplica el criterio mas conservador.

**Reglas de negocio**

- La fecha de conocimiento es el dato que dispara ambos plazos legales (OBL-INC-01 y OBL-INC-02); no se calcula ningun plazo mientras no se registre.
- El calculo del plazo lo realiza siempre el motor de plazos (MOD-023), nunca una logica propia de este modulo.
- El criterio de computo por defecto es horas corridas; es el criterio conservador que el sistema aplica mientras la organizacion no lo cambie con el mecanismo de doble control correspondiente.

**Fuera de alcance**

- Cambiar el criterio de computo de horas corridas a horas habiles para un caso especifico (mecanismo de doble control entre Delegado y Legal que administra MOD-023).

- Requiere validacion legal: Si (PP-JUR-01, PP-JUR-02)
- Referencia: MOD-013 secciones D.1, F.2 (transicion Reportado a Triage), G regla 1, I
- Notas: El cambio del criterio por defecto a horas habiles depende de la configurabilidad con doble control que la ficha de MOD-023 clasifica como SHOULD HAVE (seccion Q) y que el roadmap ubica en V1 (04_secciones/19_21_roadmap_mvp_v1_v2.md, seccion 20); esta HU solo aplica y muestra el criterio conservador por defecto, ver notas_epica.

### HU-013-03. Clasificar el incidente en Triage

**Como** Responsable de Seguridad / IT, **quiero** registrar el origen del incidente y el sistema o proceso afectado, y confirmar que se trata de una vulneracion de datos personales con su tipo y categorias de datos, **para** que el expediente avance a Investigacion con la informacion base que exige el Articulo 25.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 29 | No |

- Fundamento: OBL-INC-01 (Art. 25, Ley para la Proteccion de Datos Personales); OBL-SENS-01 (Art. 4 lit. g), Ley para la Proteccion de Datos Personales)
- Depende de: HU-013-02
- Modulos requeridos: MOD-006

**Criterios de aceptacion**

1. Dado un incidente en Triage, cuando registro el origen del incidente entre Interno, Proveedor/Encargado, Terceros/Receptor o Desconocido/en investigacion, y el sistema o proceso afectado, entonces el sistema guarda ambos datos como obligatorios para continuar.
2. Dado un incidente en Triage, cuando marco Es una vulneracion de datos personales bajo el Articulo 25 en Si y registro al menos un tipo de vulneracion y al menos una categoria de datos afectada, entonces el sistema muestra el texto Requiere validacion de la organizacion o asesoria especializada junto a la decision y pasa el incidente a Investigacion.
3. Dado que las categorias de datos afectadas incluyen Biometrica o Salud, cuando guardo la clasificacion, entonces el sistema marca automaticamente incluye datos sensibles en Si, editable solo con una justificacion registrada en el historial.
4. Dado un incidente en Triage, cuando intento marcar Es una vulneracion de datos personales en Si sin haber seleccionado ningun tipo de vulneracion ni ninguna categoria de datos, entonces el sistema no permite avanzar a Investigacion.
5. Dado un incidente cuyo origen es Proveedor/Encargado, cuando lo registro, entonces el sistema acepta el dato sin exigir vincularlo a un proveedor especifico del catalogo de MOD-009 ni bloquear el avance por esa falta de vinculo.
6. Dado un incidente ya clasificado como vulneracion con datos sensibles marcados automaticamente, cuando un usuario habilitado edita ese valor a No, entonces el sistema exige una justificacion visible antes de aceptar el cambio.

**Reglas de negocio**

- La calificacion de si el evento es una vulneracion de datos personales es una decision humana que el sistema nunca infiere ni cierra automaticamente.
- El catalogo de categorias de datos es el mismo compartido con MOD-006 y MOD-007.

**Fuera de alcance**

- Vincular el incidente a un proveedor especifico del catalogo de MOD-009, validar su existencia y mostrar su plazo pactado de aviso (funcionalidad SHOULD HAVE segun la tabla Q de la ficha y la version minima vendible del modulo).
- La alerta de incidente en proveedor sin evidencia de aviso dentro del plazo pactado (misma cobertura parcial que el punto anterior).

- Referencia: MOD-013 secciones D.1, D.2, F.2 (transicion Triage a Investigacion), H punto 1, Q
- Notas: La referencia a un proveedor especifico de MOD-009 se excluye porque la ficha (seccion Q y el parrafo de version minima vendible) marca esa pieza como SHOULD HAVE y aclara que el MVP cubre el flujo completo de un incidente de origen interno sin dependencia obligatoria de Proveedores; ver discrepancia en notas_epica.

### HU-013-04. Descartar un incidente en Triage por no ser una vulneracion de datos personales

**Como** Responsable de Seguridad / IT, **quiero** marcar en Triage que el evento reportado no es una vulneracion de datos personales, con una justificacion obligatoria, **para** cerrar de forma trazable los casos que no activan las obligaciones del Articulo 25, dejando constancia de quien lo decidio y por que.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 29 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-013-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un incidente en Triage, cuando marco Es una vulneracion de datos personales en No y registro una justificacion, entonces el sistema pasa el incidente a Descartado y detiene ambos cronometros de 72 horas.
2. Dado que intento marcar Es una vulneracion de datos personales en No, cuando dejo vacio el campo de justificacion, entonces el sistema no permite el cambio de estado.
3. Dado un incidente que paso a Descartado, cuando reviso su historial, entonces veo el evento de auditoria con la justificacion completa, visible para el rol Auditor interno.
4. Dado un incidente en estado Descartado, cuando un rol distinto de Responsable de Seguridad/IT, Delegado o Responsable Legal/Compliance intenta ejecutar esta transicion, entonces el sistema deniega la accion.
5. Dado un incidente en Descartado, cuando alguien intenta editar los campos ya guardados antes del descarte, entonces el sistema no lo permite: el expediente queda de solo lectura salvo la creacion de una nueva linea de tiempo por reapertura.

**Reglas de negocio**

- Ninguna norma exige dos personas distintas para descartar un caso, pero la justificacion siempre queda visible para cualquier auditoria posterior.
- Descartado es un estado terminal, reabribile con justificacion.

**Fuera de alcance**

- El flujo de reapertura en si mismo (HU aparte).

- Referencia: MOD-013 secciones D.2, F.1, F.2 (transicion Triage a Descartado), H punto 1

### HU-013-05. Registrar el inicio de la revision exhaustiva del incidente

**Como** Responsable de Seguridad / IT, **quiero** registrar formalmente la fecha y hora en que inicia la revision exhaustiva del caso, **para** dejar evidencia de que la obligacion de iniciar la revision dentro de las 72 horas se cumplio o, si no fue asi, que quede marcada honestamente como vencida.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 29 | No |

- Fundamento: OBL-INC-02 (Art. 25 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-013-03
- Modulos requeridos: MOD-023

**Criterios de aceptacion**

1. Dado un incidente en Investigacion sin fecha de inicio de revision registrada, cuando la registro dentro de las 72 horas desde la fecha de conocimiento, entonces el sistema la guarda y actualiza el indicador de dashboard de revision iniciada dentro de plazo.
2. Dado un incidente en Investigacion, cuando registro la fecha de inicio de la revision exhaustiva despues de cumplidas las 72 horas desde el conocimiento, entonces el sistema guarda el dato pero marca el hito de revision como vencido en el historial de forma permanente, sin bloquear el avance del caso.
3. Dado que aun no he registrado ninguna accion de contencion, cuando registro hallazgos y confirmo el inicio de la revision, entonces el sistema exige al menos una accion de contencion documentada antes de pasar a Evaluacion, y en su ausencia el caso pasa a Contencion.
4. Dado que ya existe al menos una accion de contencion documentada, cuando registro hallazgos y confirmo el inicio de la revision, entonces el sistema pasa el incidente directamente a Evaluacion.
5. Dado un incidente en Investigacion, cuando intento pasar a Evaluacion sin haber registrado la fecha de inicio de la revision exhaustiva, entonces el sistema no permite el avance.
6. Dado un hito de revision marcado como vencido, cuando cualquier usuario con acceso revisa el expediente, entonces esa marca de vencimiento permanece visible de forma permanente y no puede eliminarse ni editarse.

**Reglas de negocio**

- La ley exige que la revision inicie, no que concluya, dentro de las 72 horas.
- El vencimiento del hito de revision nunca bloquea el avance del caso; solo queda documentado.

- Referencia: MOD-013 secciones D.3, F.1 (nota de Contencion), F.2 (transicion Investigacion a Contencion o Evaluacion), G regla 5

### HU-013-06. Registrar acciones de contencion inmediata

**Como** Responsable de Seguridad / IT, **quiero** registrar en una bitacora cada accion de contencion inmediata que se ejecuta, con fecha y usuario, **para** demostrar que se actuo de inmediato para detener o limitar el dano, como exige el contenido minimo de la notificacion a la ACE y a la Fiscalia General de la Republica.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 27 | No |

- Fundamento: OBL-INC-03 (Art. 25 inc. 3-4, Ley para la Proteccion de Datos Personales)
- Depende de: HU-013-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un incidente en cualquier estado desde Reportado en adelante, cuando registro una accion de contencion con su descripcion, entonces el sistema la guarda en la bitacora con fecha, hora y el usuario que la registro.
2. Dado que intento avanzar el incidente al estado Evaluacion, cuando no existe ninguna entrada de contencion registrada, entonces el sistema no permite el avance.
3. Dado una entrada ya guardada en la bitacora de contencion, cuando intento editarla despues de guardada, entonces el sistema no permite modificarla retroactivamente sin dejar rastro del cambio.
4. Dado un incidente con varias entradas de contencion, cuando reviso el expediente, entonces veo todas las entradas ordenadas por fecha, cada una con su autor.
5. Dado que soy un rol sin permiso para modificar el expediente, por ejemplo Auditor interno o Usuario de consulta sin tarea asignada, cuando intento agregar una entrada de contencion, entonces el sistema deniega la accion.

**Reglas de negocio**

- Las acciones de contencion pueden y deben registrarse desde Reportado o Triage si la urgencia lo exige; el estado formal Contencion solo marca el punto en que se exige al menos una entrada antes de avanzar.

- Referencia: MOD-013 seccion D.3, F.1 (nota de lectura de Contencion), F.2

### HU-013-07. Evaluar el alcance, impacto y riesgo del incidente con bloqueo de documentacion obligatoria

**Como** Responsable de Seguridad / IT, **quiero** registrar la cantidad estimada de titulares afectados, el impacto estimado y si existe riesgo en la seguridad de los datos personales, y que el sistema bloquee el avance si faltan los campos obligatorios cuando hay riesgo, **para** cumplir con la documentacion obligatoria de toda vulneracion con riesgo antes de decidir sobre la notificacion externa.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 30 | No |

- Fundamento: OBL-INC-04 (Art. 25 inc. final, Ley para la Proteccion de Datos Personales)
- Depende de: HU-013-05, HU-013-06
- Modulos requeridos: MOD-021

**Criterios de aceptacion**

1. Dado un incidente en Evaluacion, cuando registro la cantidad estimada de titulares afectados y el impacto estimado para los titulares, entonces el sistema los guarda como obligatorios para continuar.
2. Dado un incidente en Evaluacion, cuando marco Existe riesgo en la seguridad de los datos personales en Si, entonces el sistema muestra el texto Requiere validacion de la organizacion o asesoria especializada junto a la decision.
3. Dado que marco Existe riesgo en Si, cuando intento avanzar a Decision sin haber completado cantidad de titulares, impacto estimado y medidas correctivas propuestas, entonces el sistema bloquea el avance con una alerta de nivel HIGH y no permite continuar hasta completarlos.
4. Dado que marco Existe riesgo en No, cuando guardo el valor, entonces el sistema exige una justificacion visible en el historial y marca el caso para revision del Delegado.
5. Dado un tratamiento relacionado sin Evaluacion de Impacto registrada y con categorias Biometrica o Salud marcadas, cuando guardo la evaluacion, entonces el sistema crea una tarea evaluar si corresponde EIPD en el Centro de Tareas, con referencia al incidente como origen y sin cuestionario de scoring propio.
6. Dado que la organizacion tiene marcada la bandera de operador de infraestructura critica, cuando reviso la Evaluacion de un incidente de tipo ciberseguridad, entonces el sistema muestra ese campo condicional en modo lectura, sin bloquear el flujo ni exigir el reporte adicional del Decreto 143.
7. Dado que intento registrar el listado o referencia de titulares afectados, cuando cargo una lista de identificadores internos, entonces el sistema la acepta; cuando el contenido equivale a una extraccion masiva de la base de datos completa, entonces el texto de ayuda advierte que no debe convertirse en una copia masiva de la base afectada.

**Reglas de negocio**

- El bloqueo por documentacion incompleta con riesgo confirmado no es configurable ni desactivable.
- El sistema nunca calcula un puntaje automatico de riesgo; la decision es siempre humana.
- El expediente nunca almacena una copia de la base de datos comprometida ni el dato personal en si, solo categorias, cantidades y referencias.

**Fuera de alcance**

- El cuestionario de scoring de la Evaluacion de Impacto (depende de MOD-014, SHOULD HAVE).
- El reporte adicional a la ACE bajo el Decreto 143 y su evidencia especifica (SHOULD HAVE segun la tabla Q).

- Referencia: MOD-013 secciones D.2, D.3, F.2 (transicion Evaluacion a Decision), G reglas 6, 9 y 10, H punto 2, I
- Notas: Se incluye aqui, de forma generica y sin cuestionario propio, la tarea de Evaluacion de Impacto que la ficha (seccion L.2) confirma que se crea igual aunque MOD-014 (SHOULD HAVE) no este activo; por eso esta HU depende de MOD-021 y no de MOD-014.

### HU-013-08. Decidir si corresponde la notificacion externa del incidente

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** decidir, junto con Responsable Legal/Compliance, si el incidente requiere notificar externamente a la ACE, a la Fiscalia General de la Republica y a los titulares, dejando justificacion si la respuesta es que no corresponde, **para** dar cumplimiento a la decision que la ley nunca deja en manos del sistema, antes de generar cualquier notificacion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 30 | No |

- Fundamento: OBL-INC-01 (Art. 25, Ley para la Proteccion de Datos Personales)
- Depende de: HU-013-07
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un incidente en Decision con la evaluacion de riesgo completa, cuando decido que si corresponde notificar externamente, entonces el sistema muestra el texto Requiere validacion de la organizacion o asesoria especializada, registra el evento de auditoria de la decision y pasa el incidente a Notificacion.
2. Dado un incidente en Decision, cuando decido que no corresponde notificar externamente, entonces el sistema exige una justificacion obligatoria antes de pasar el caso a Cierre sin notificacion externa justificado.
3. Dado que intento guardar la decision de no notificar sin justificacion, cuando confirmo, entonces el sistema no permite el cambio de estado.
4. Dado que soy Responsable de Seguridad/IT o Responsable de area, cuando intento ejecutar esta decision, entonces el sistema deniega la accion porque solo el Delegado, con co-revision de Responsable Legal/Compliance segun la politica interna, puede decidirla.
5. Dado una decision de no notificar ya registrada, cuando el Auditor interno revisa el historial, entonces la justificacion completa queda visible para cualquier auditoria posterior de la ACE.
6. Dado un incidente cuya evaluacion de riesgo aun no esta completa, cuando intento tomar esta decision, entonces el sistema no permite avanzar hasta que la evaluacion este completa.

**Reglas de negocio**

- La decision de notificar o no notificar nunca la toma el sistema; solo la registra con su justificacion.
- El corevisor Responsable Legal/Compliance participa segun la politica interna de la organizacion, pero la aprobacion formal siempre requiere la accion explicita del Delegado.

- Requiere validacion legal: Si
- Referencia: MOD-013 secciones D.5 parcial, F.2 (transicion Decision), H punto 3

### HU-013-09. Completar el contenido y generar los borradores diferenciados de notificacion

**Como** Responsable de Seguridad / IT, **quiero** completar la naturaleza del incidente, los datos comprometidos, las acciones correctivas inmediatas, las recomendaciones al titular y los medios de contacto, y que el sistema genere automaticamente los dos borradores de notificacion diferenciados, **para** preparar el contenido minimo que exige el Articulo 25 sin arriesgarme a compartir con los titulares informacion reservada a la autoridad.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 30 | No |

- Fundamento: OBL-INC-03 (Art. 25 inc. 3-4, Ley para la Proteccion de Datos Personales)
- Depende de: HU-013-08
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un incidente en Notificacion, cuando completo naturaleza del incidente, datos comprometidos, acciones correctivas inmediatas, recomendaciones al titular y medios de contacto, entonces el sistema genera automaticamente el borrador de notificacion a la ACE y a la Fiscalia General de la Republica con los cinco elementos naturaleza, datos comprometidos, acciones correctivas, recomendaciones y medios de contacto, y el borrador de notificacion a titulares con los cuatro elementos, omitiendo las acciones correctivas inmediatas.
2. Dado que los dos borradores se generan, cuando los reviso, entonces ambos quedan marcados como borrador pendiente de aprobacion y no pueden marcarse como enviados sin la aprobacion del Delegado.
3. Dado que falta cualquiera de los cinco campos de contenido, cuando intento generar los borradores, entonces el sistema no los genera hasta completarlos.
4. Dado el borrador de notificacion a titulares ya generado, cuando lo comparo con el borrador a la ACE y a la Fiscalia, entonces verifico que el contenido de acciones correctivas inmediatas nunca aparece en la version de titulares.
5. Dado que los medios de contacto para mas informacion no incluyen al menos un canal valido, cuando intento guardar el campo, entonces el sistema no lo acepta.
6. Dado cualquiera de los dos borradores generados, cuando lo visualizo, entonces el sistema muestra el texto Documento generado como borrador a partir de la informacion registrada, requiere revision y aprobacion de su organizacion antes de usarse, y puede requerir validacion de asesoria legal especializada.

**Reglas de negocio**

- Las dos plantillas se generan siempre por separado a partir de los mismos campos base; nunca es una sola plantilla editada a mano.
- El contenido minimo legal de cada plantilla no es configurable; solo el formato o la plantilla visual lo es.

**Fuera de alcance**

- La aprobacion y el marcado de enviado de cada notificacion (HU aparte).
- El contenido especifico del reporte adicional del Decreto 143 (SHOULD HAVE).

- Requiere contenido: Plantilla de notificacion a la ACE y a la Fiscalia General de la Republica con los cinco elementos del Articulo 25, validada por abogado.; Plantilla de notificacion a titulares con los cuatro elementos, sin acciones correctivas, en lenguaje simplificado para publico no especialista, validada por abogado.
- Requiere validacion legal: Si
- Referencia: MOD-013 secciones D.4, E, F.2 (transicion Decision a Notificacion), G regla 7, K

### HU-013-10. Aprobar y marcar como enviada cada notificacion externa

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** aprobar y marcar como enviada cada notificacion, a la ACE y a la Fiscalia General de la Republica, y a los titulares, registrando fecha, hora, canal y una constancia con verificacion de integridad, **para** dejar prueba fehaciente de que la empresa cumplio, o de que no cumplio a tiempo, su obligacion de notificar dentro de las 72 horas.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 30 | No |

- Fundamento: OBL-INC-01 (Art. 25, Ley para la Proteccion de Datos Personales); OBL-INC-03 (Art. 25 inc. 3-4, Ley para la Proteccion de Datos Personales); OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-013-09
- Modulos requeridos: MOD-019, MOD-023

**Criterios de aceptacion**

1. Dado un borrador de notificacion pendiente de aprobacion, cuando lo apruebo y registro fecha, hora y canal de envio, entonces el sistema bloquea la edicion de esa version, genera una constancia de envio con hash de integridad verificable y la envia al Centro de Evidencias.
2. Dado que ambas notificaciones, a la ACE y a la Fiscalia, y a los titulares, quedan marcadas como enviadas, cuando se completa la segunda, entonces el sistema pasa el incidente a Remediacion.
3. Dado que soy Responsable de Seguridad/IT, cuando intento aprobar o marcar como enviada una notificacion, entonces el sistema deniega la accion porque ese rol solo prepara el borrador, nunca aprueba.
4. Dado que el envio ocurre despues de cumplidas las 72 horas desde la fecha de conocimiento, cuando marco la notificacion como enviada, entonces el sistema no bloquea el envio pero marca el hito de notificacion como vencido de forma permanente e irreversible en el historial.
5. Dado una notificacion ya marcada como enviada, cuando reviso su constancia, entonces veo fecha, hora, canal, destinatario, la version exacta del contenido enviado y un hash verificable de forma independiente.
6. Dado que apruebo una notificacion a titulares en lote para varios destinatarios, cuando confirmo el envio, entonces el sistema genera la constancia por lote con el mismo mecanismo de integridad.
7. Dado un caso cerrado que tiene el hito de notificacion marcado como vencido en su historial, cuando el Auditor interno o Responsable Legal/Compliance lo consultan, entonces la marca de vencimiento permanece visible de forma permanente en los reportes.

**Reglas de negocio**

- El sistema nunca envia una notificacion externa por si mismo; siempre exige la aprobacion explicita y trazable del Delegado.
- El vencimiento del plazo de notificacion no se apaga nunca del todo: el incumplimiento queda registrado de forma permanente aunque la notificacion se envie despues.

- Referencia: MOD-013 secciones E, F.2 (transicion Notificacion a Remediacion), G regla 8, H punto 6, I, J

### HU-013-11. Recibir alertas y escalamiento de los dos cronometros de 72 horas

**Como** Responsable de Seguridad / IT, **quiero** recibir alertas automaticas por plataforma y correo cuando cualquiera de los dos cronometros de 72 horas se acerca a su limite o lo vence, con escalamiento y acuse de recibo cuando son criticas, **para** que ningun plazo legal dependa de que alguien recuerde revisar el sistema.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 30 | No |

- Fundamento: OBL-INC-01 (Art. 25, Ley para la Proteccion de Datos Personales); OBL-INC-02 (Art. 25 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-013-02
- Modulos requeridos: MOD-022, MOD-023

**Criterios de aceptacion**

1. Dado un incidente con el cronometro de notificacion activo, cuando se consume el 50 por ciento del plazo de 72 horas sin notificacion enviada, entonces el sistema envia una alerta WARNING al Responsable de Seguridad/IT y al Delegado por plataforma y correo, y la escala al Administrador si no hay accion en 6 horas.
2. Dado un incidente con el cronometro de notificacion activo, cuando faltan 6 horas para vencer sin notificacion enviada, entonces el sistema envia una alerta CRITICAL al Delegado, al Administrador y al Aprobador cada hora hasta el vencimiento, y exige acuse de recibo obligatorio de quien la recibe.
3. Dado un incidente cuyo cronometro de notificacion llega a cero sin notificacion enviada, cuando se cumplen las 72 horas, entonces el sistema marca el hito de notificacion como vencido de forma permanente y envia una alerta CRITICAL diaria al Administrador, al Delegado y a Legal hasta que se resuelva.
4. Dado un incidente cuyo cronometro de revision llega a 60 horas transcurridas sin haber marcado el inicio de la revision exhaustiva, cuando se alcanza ese umbral, entonces el sistema envia una alerta WARNING al Responsable de Seguridad/IT, escalada al Delegado a las 70 horas.
5. Dado que la notificacion se marca como enviada o el caso pasa a Descartado, cuando esto ocurre, entonces las alertas activas del cronometro de notificacion dejan de repetirse.
6. Dado que una alerta CRITICAL fue enviada, cuando el destinatario no confirma el acuse de recibo dentro de la plataforma, entonces el sistema no la considera atendida y la sigue mostrando como pendiente.
7. Dado un incidente cuyo cronometro de revision ya paso a Investigacion con fecha de inicio registrada, cuando reviso las alertas, entonces la alerta de inicio de revision pendiente ya no se genera para ese caso.

**Reglas de negocio**

- El registro del vencimiento de cualquiera de los dos cronometros no es desactivable, para preservar la evidencia.

**Fuera de alcance**

- Canales de alerta adicionales a plataforma y correo, como SMS, WhatsApp, Teams o Slack.

- Referencia: MOD-013 seccion I completa, G reglas 2 a 5

### HU-013-12. Registrar las medidas correctivas definitivas y la actualizacion de politicas

**Como** Responsable de Seguridad / IT, **quiero** registrar las medidas correctivas definitivas, enlazarlas con el catalogo de Controles de MOD-015 y confirmar si se requiere actualizar la politica de seguridad, **para** dejar constancia de que el incidente genero una mejora permanente, como exige la revision exhaustiva del Articulo 25.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 31 | No |

- Fundamento: OBL-INC-02 (Art. 25 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-013-10
- Modulos requeridos: MOD-015, MOD-021

**Criterios de aceptacion**

1. Dado un incidente en Remediacion, cuando registro una medida correctiva definitiva y la enlazo a un Control existente del catalogo de MOD-015, entonces el sistema guarda el vinculo en el expediente.
2. Dado que la medida correctiva definitiva no tiene un Control equivalente en el catalogo de MOD-015, cuando la registro como texto libre, entonces el sistema crea un Control nuevo en MOD-015 referenciando este incidente como origen.
3. Dado un incidente en Remediacion, cuando marco Actualizacion de politicas de seguridad requerida en Si, entonces el sistema crea una tarea de actualizacion de politica en el Centro de Tareas.
4. Dado un incidente en Remediacion, cuando intento avanzar a Cierre sin haber registrado al menos una medida correctiva definitiva, entonces el sistema no permite el avance.
5. Dado que marco Actualizacion de politicas de seguridad requerida en No, cuando guardo el valor, entonces el sistema no crea ninguna tarea de politica y permite continuar.

**Reglas de negocio**

- El catalogo de controles compartido es el mismo que usan MOD-014 y MOD-015; no se duplica.

- Referencia: MOD-013 secciones D.3, F.2 (transicion Remediacion a Cierre), G regla 6

### HU-013-13. Completar la decision final de cierre del incidente

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** completar la decision final del caso y su justificacion y, si la organizacion supera el umbral de separacion de funciones, obtener la segunda firma del Aprobador, **para** cerrar el expediente dejando registrada la evidencia de quien decidio, cuando y con que fundamento.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 31 | No |

- Fundamento: OBL-INC-04 (Art. 25 inc. final, Ley para la Proteccion de Datos Personales); OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-013-08, HU-013-12
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado un incidente en Remediacion o en Cierre sin notificacion externa justificado, cuando completo la decision final del caso entre Resuelto con notificacion enviada, Resuelto sin obligacion de notificar, Descartado en Triage o Transferido a otro proceso, y una justificacion de al menos 20 caracteres, entonces el sistema registra el responsable de la decision de forma automatica.
2. Dado que la organizacion esta por encima del umbral configurable de separacion de funciones y quien cierra es la misma persona que investigo y gestiono todo el caso, cuando intento cerrar, entonces el sistema exige una segunda firma del rol Aprobador antes de completar el cierre.
3. Dado que la organizacion esta por debajo del umbral configurable, cuando la misma persona investiga y cierra el caso, entonces el sistema permite el cierre pero muestra una advertencia visible de autorrevision.
4. Dado que intento cerrar el caso con una justificacion de menos de 20 caracteres, cuando confirmo, entonces el sistema no permite el cierre.
5. Dado que el incidente tiene Existe riesgo en Si y los campos de documentacion obligatoria estan incompletos, cuando intento cerrar, entonces el sistema no permite el cierre hasta completarlos.
6. Dado un incidente cerrado, cuando cualquier usuario intenta editar sus campos, entonces el sistema no lo permite: el expediente queda de solo lectura salvo reapertura.
7. Dado que el Aprobador registra la segunda firma, cuando confirma, entonces el sistema deja constancia de su identidad, fecha y hora junto a la del responsable original de la decision.

**Reglas de negocio**

- Ninguna norma exige dos personas distintas para cerrar un incidente, pero la decision de cierre siempre deja registrada la evidencia de quien decidio, cuando y con que fundamento.
- El umbral de separacion de funciones, con propuesta inicial de 50 empleados, se configura a nivel de organizacion en MOD-001.

- Referencia: MOD-013 secciones D.5, F.2 (transiciones a Cierre), H punto 7

### HU-013-14. Enviar el expediente cerrado a conservacion sin borrado

**Como** Administrador de la organizacion, **quiero** que al cerrarse un incidente el sistema calcule automaticamente su fecha de conservacion recomendada y proteja el expediente de cualquier eliminacion, **para** poder demostrarlo ante una eventual investigacion de la ACE, incluso anos despues del cierre.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 31 | No |

- Fundamento: OBL-RET-05 (Art. 47 Normativa PAS; Art. 5 lit. i LPDP (responsabilidad demostrada), Normativa para el Procedimiento Administrativo Sancionador)
- Depende de: HU-013-13
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un incidente que pasa a Cierre, cuando el sistema calcula la fecha de conservacion, entonces la establece como la fecha de cierre mas el minimo recomendado configurable de 5 anos por defecto y la registra en el expediente.
2. Dado un incidente cerrado, cuando cualquier rol, incluido el Administrador, intenta eliminarlo, entonces el sistema no ofrece ninguna accion de borrado: el expediente solo puede archivarse cuando se cumpla el plazo de conservacion.
3. Dado un incidente cerrado, cuando el Administrador o el Auditor interno consultan el expediente, entonces ven la fecha de conservacion recomendada junto con la fecha de cierre.
4. Dado que el motor de retencion documental completo, con alertas de vencimiento y archivado automatico activo, aun no existe como modulo propio, cuando se cumple el plazo de conservacion, entonces el expediente permanece protegido de borrado de forma pasiva, sin alerta automatica de vencimiento ni archivado automatico.
5. Dado un incidente cerrado, cuando reviso el evento de auditoria de cierre, entonces veo tambien la fecha de conservacion calculada junto con el responsable y la justificacion del cierre.

**Reglas de negocio**

- El periodo minimo de conservacion es ajustable por el Responsable Legal dentro del rango recomendado, pero nunca acortable sin excepcion documentada.
- Mientras el motor de retencion documental completo no exista, la proteccion contra el borrado es la unica cobertura activa; no hay alertas de vencimiento ni archivado automatico real.

**Fuera de alcance**

- El archivado automatico activo y las alertas de vencimiento del expediente, que dependen del motor de retencion documental completo, SHOULD HAVE y diferido a V1.

- Requiere validacion legal: Si (PP-MAPA-08)
- Referencia: MOD-013 secciones E, F.2 (nota de Archivado), G regla 12, J
- Notas: OBL-RET-05 es RECOMENDADO, sin norma expresa que fije el plazo de 5 anos, y requiere validacion de abogado. MOD-016 (motor de retencion completo) es SHOULD HAVE y no aparece en la lista de modulos de R1 ni de R2 de las instrucciones de esta tarea; por eso esta HU no depende de MOD-016 como modulo construido, solo calcula la fecha y aplica la proteccion pasiva contra el borrado, tal como documentan la ficha de MOD-013 (seccion L.2) y la propia ficha de MOD-016 (seccion Q y notas finales). Ver notas_epica.

### HU-013-15. Reabrir un incidente cerrado o descartado

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** reabrir un incidente que ya esta en Cierre, en Lecciones aprendidas o en Descartado, con un motivo justificado, **para** incorporar informacion nueva, por ejemplo un reclamo de un titular o un requerimiento de la ACE, sin perder el expediente original.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 31 | No |

- Fundamento: OBL-INC-04 (Art. 25 inc. final, Ley para la Proteccion de Datos Personales); OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-013-13, HU-013-04
- Modulos requeridos: MOD-021

**Criterios de aceptacion**

1. Dado un incidente en Cierre, en Lecciones aprendidas o en Descartado, cuando registro un motivo de reapertura obligatorio, entonces el sistema pasa el caso a Reabierto y lo dirige a Investigacion o a Evaluacion segun el motivo indicado.
2. Dado que intento reabrir un caso sin registrar el motivo, cuando confirmo la accion, entonces el sistema no permite la reapertura.
3. Dado un incidente reabierto, cuando reviso su historial, entonces el expediente conserva integramente la version anterior, y se abre una nueva linea de tiempo dentro del mismo caso sin sobrescribir lo ya cerrado.
4. Dado que soy Responsable de Seguridad/IT sin el rol Delegado, Responsable Legal/Compliance o Administrador, cuando intento reabrir un caso, entonces el sistema deniega la accion.
5. Dado un incidente reabierto, cuando reviso las tareas asociadas al motivo original, entonces las tareas ya cerradas no se reabren automaticamente: el sistema crea tareas nuevas para el nuevo motivo.

**Reglas de negocio**

- La reapertura nunca borra ni sobrescribe el expediente original.
- Solo Delegado, Responsable Legal/Compliance o Administrador pueden reabrir un caso.

**Fuera de alcance**

- Un flujo guiado distinto segun cada motivo de reapertura, funcionalidad COULD HAVE segun la tabla Q.

- Referencia: MOD-013 secciones F.1, F.2 (transicion a Reabierto), O

### HU-013-16. Registrar lecciones aprendidas tras el cierre

**Como** Responsable de Seguridad / IT, **quiero** registrar de forma opcional las lecciones aprendidas de un incidente ya cerrado, **para** dejar constancia de lo que la empresa aprendio y facilitar que no se repita.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R2 | 31 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-013-13
- Modulos requeridos: MOD-015, MOD-017, MOD-021

**Criterios de aceptacion**

1. Dado un incidente en Cierre, cuando registro el texto de lecciones aprendidas, entonces el sistema lo guarda y pasa el caso al estado informativo Lecciones aprendidas sin reabrir ni afectar el cierre legal ya realizado.
2. Dado un incidente en Cierre, cuando decido no registrar lecciones aprendidas, entonces el sistema permite que el caso permanezca en Cierre sin exigir este campo.
3. Dado que registro una medida correctiva nueva dentro de las lecciones aprendidas, cuando la guardo, entonces el sistema crea o actualiza un Control en MOD-015.
4. Dado que las lecciones aprendidas senalan una necesidad de capacitacion, cuando lo registro, entonces el sistema puede generar una tarea hacia MOD-017.

**Reglas de negocio**

- Lecciones aprendidas es un estado terminal informativo; no bloquea el cierre legal ya alcanzado.

- Referencia: MOD-013 secciones D.5, F.2 (transicion Cierre a Lecciones aprendidas), G regla 13

### HU-013-17. Consultar el checklist de las 72 horas del incidente

**Como** Responsable de Seguridad / IT, **quiero** ver dentro del expediente un checklist con los pasos minimos exigidos por el Articulo 25 y su estado, **para** no perder de vista, en medio de la urgencia, ningun paso obligatorio de las 72 horas.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 30 | No |

- Fundamento: OBL-INC-01 (Art. 25, Ley para la Proteccion de Datos Personales); OBL-INC-02 (Art. 25 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-013-02
- Modulos requeridos: MOD-023

**Criterios de aceptacion**

1. Dado un incidente con la fecha de conocimiento registrada, cuando abro el checklist de las 72 horas, entonces veo cada paso minimo, entre ellos confirmar la vulneracion, iniciar la revision, evaluar el riesgo, decidir la notificacion, generar y enviar las notificaciones, y documentar las medidas correctivas, cada uno con su estado pendiente, completado o vencido.
2. Dado un paso ya completado en el expediente, por ejemplo la fecha de inicio de revision ya registrada, cuando reviso el checklist, entonces ese paso aparece marcado como completado sin necesidad de marcarlo manualmente.
3. Dado un paso cuyo plazo ya vencio, por ejemplo la notificacion no enviada a las 72 horas, cuando reviso el checklist, entonces aparece marcado como vencido, en linea con el historial del cronometro correspondiente.
4. Dado un incidente sin fecha de conocimiento registrada todavia, cuando abro el checklist, entonces el sistema muestra que los pasos con plazo aun no aplican porque los cronometros no han iniciado.
5. Dado el checklist de un incidente, cuando lo consulto, entonces cada paso muestra su fundamento legal en segundo nivel, nunca como texto principal de la pantalla.

**Reglas de negocio**

- El checklist refleja el estado real de los campos y transiciones del expediente; no es una lista aparte que haya que llenar dos veces.

- Requiere contenido: Contenido del checklist de las 72 horas con los pasos minimos exigidos, revisado por el equipo legal.
- Referencia: MOD-013 secciones E, K, R.2

### HU-013-18. Consultar el listado de incidentes con filtros

**Como** Responsable Legal / Compliance, **quiero** consultar el listado de incidentes del periodo, con filtros por fecha, severidad, estado y origen, **para** darle seguimiento gerencial al estado de todos los incidentes, incluidos los que estan por vencer sus cronometros.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 31 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-013-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que existen incidentes registrados en la organizacion, cuando abro el listado del periodo, entonces veo, para cada incidente, titulo, fechas clave, severidad, estado, si hubo notificacion y si fue dentro de plazo.
2. Dado el listado de incidentes, cuando aplico un filtro por rango de fechas, severidad, estado u origen, entonces el sistema muestra solo los incidentes que cumplen ese filtro.
3. Dado que soy Responsable de area sin incidentes asignados, cuando abro el listado, entonces solo veo los incidentes que reporte o que me fueron asignados, nunca el listado completo de la organizacion.
4. Dado el listado filtrado, cuando lo exporto, entonces el sistema lo genera en PDF, XLSX o CSV segun elija.
5. Dado el listado de incidentes, cuando lo reviso, entonces el sistema nunca muestra un porcentaje de cumplimiento legal, solo estado del programa, severidad y plazos.

**Reglas de negocio**

- El listado nunca usa la expresion cumplimiento legal ni un porcentaje de cumplimiento.
- El acceso respeta los permisos de visibilidad por rol ya definidos en la ficha.

- Referencia: MOD-013 seccion N, fila Listado de incidentes del periodo

### HU-013-19. Exportar el expediente de un incidente como paquete de evidencia verificable

**Como** Auditor (interno), **quiero** exportar el expediente completo de un incidente, con su bitacora y sus constancias de notificacion, como un paquete verificable, **para** usarlo como evidencia en una auditoria interna o ante un requerimiento de la ACE.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 32 | No |

- Fundamento: OBL-INC-04 (Art. 25 inc. final, Ley para la Proteccion de Datos Personales)
- Depende de: HU-013-13
- Modulos requeridos: MOD-019

**Criterios de aceptacion**

1. Dado un incidente cerrado, cuando exporto su expediente, entonces el sistema genera un archivo en PDF o ZIP que incluye todos los campos del expediente, la bitacora completa y las constancias de notificacion.
2. Dado el paquete exportado, cuando lo recibo, entonces incluye un mecanismo de verificacion de integridad, hash o firma validable de forma independiente, que permite comprobar despues que no fue alterado.
3. Dado que soy Auditor interno, cuando exporto un expediente, entonces el sistema registra el evento en el historial con quien exporto, cuando y con que filtro.
4. Dado que soy Responsable de area sin acceso al expediente completo, cuando intento exportarlo, entonces el sistema deniega la accion.
5. Dado un incidente aun abierto y no cerrado, cuando lo exporto, entonces el sistema genera igualmente el paquete con el estado actual del expediente, dejando claro que el caso sigue en curso.

**Reglas de negocio**

- Todo paquete de evidencias exportado incluye verificacion de integridad, sin excepcion.

**Fuera de alcance**

- El paquete consolidado de evidencia para la auditoria anual, que se genera desde MOD-019 combinando varios modulos.

- Referencia: MOD-013 secciones E, J, N, fila Expediente individual de un incidente

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Registro del incidente y flujo completo de estados (Reportado a Cierre) | HU-013-01, HU-013-02, HU-013-03, HU-013-04, HU-013-05, HU-013-06, HU-013-07, HU-013-08, HU-013-12, HU-013-13, HU-013-15 |
| Dos cronometros de 72 horas en paralelo (notificacion e inicio de revision), con criterio de horas corridas por defecto | HU-013-02, HU-013-11 |
| Plantillas diferenciadas de notificacion a ACE/FGR y a titulares | HU-013-09, HU-013-10 |
| Documentacion obligatoria del expediente con bloqueo si hay riesgo y faltan campos | HU-013-07, HU-013-13 |
| Checklist de las 72 horas | HU-013-17 |
| Vinculo con el catalogo de controles de MOD-015 para medidas correctivas | HU-013-12 |
| Constancia de envio con verificacion de integridad (hash) | HU-013-10 |
| Alertas de cronometro (WARNING, CRITICAL, vencido) por plataforma y correo | HU-013-11 |
