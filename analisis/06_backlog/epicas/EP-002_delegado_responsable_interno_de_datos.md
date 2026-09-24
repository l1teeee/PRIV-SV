# EP-002 Delegado / Responsable Interno de Datos (MOD-002)

**Objetivo.** La empresa puede nombrar y mantener al Delegado de Proteccion de Datos o Responsable Interno durante todo su ciclo de vida (nombramiento, contadores legales de notificacion interna, comunicacion a la ACE y designacion de sustituto, checklist de perfil, declaracion jurada, reverificacion trienal, capacitacion anual, cese y confidencialidad post-cese), con el estado normativo de la reforma 659 leido desde el Centro Regulatorio y un responsable del tramite siempre identificado para ARCO-POL y Consentimiento.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R1 | 17 | 76 | 74 | 2 | [MOD-002](../../03_modulos/MOD-002_ficha.md) |

**Notas de la epica.**

- Se excluyen del MVP, por ser SHOULD HAVE o superior en la tabla Q de la ficha: registro de informes periodicos semestrales con estadisticas ARCO-POL (SHOULD HAVE), bitacora de peticiones internas atendidas por otras areas OBL-DPO-08 (SHOULD HAVE), paquete de evidencia exportable con hash de integridad (SHOULD HAVE, depende de MOD-019), delegado comun para grupos de sociedades (FUTURE) y multiples delegados propietarios simultaneos (COULD). No hay discrepancia entre la tabla Q y 19.3: ambas fuentes coinciden en dejar fuera estos elementos del MVP, y el encargo confirma de forma explicita sin informes semestrales automaticos.
- HU-002-11 (recepcion por referencia de la constancia generada en MOD-017) se clasifica en R2 porque depende de que MOD-017 Capacitacion, clasificado en R2 segun la seccion 6 de las instrucciones, exista y notifique la constancia; el registro manual de la capacitacion anual (HU-002-10) ya satisface OBL-DPO-05 desde R1 sin depender de MOD-017, de modo que el nucleo vendible de R1 no queda incompleto.
- El campo certificacion_ace_estado (Art. 5 lit. e, 20 y 21 Lineamientos DPO) no se construye como HU propia en este backlog: la ficha indica que ese requisito aplica desde que la Agencia lo habilite formalmente, lo cual aun no ocurre (decision H.4, anti-feature 12); queda como extension futura del modulo cuando la ACE habilite el Programa de Certificacion.
- El fundamento del contador de 10 dias habiles para designar sustituto tras el cese (HU-002-12 y HU-002-13) no tiene un OBL-ID propio distinto en la matriz: se apoya en OBL-DPO-01 y en su campo nota_actualizacion_fase3 (la continuidad de la figura incluye designar un nuevo Delegado dentro de los 10 dias habiles siguientes a su cese o suspension, Art. 19 Lineamientos DPO), tal como indica el encargo.
- Se preserva la asimetria de depende_de senalada por la propia ficha entre MOD-002 y MOD-023 (mapa_modulos.json no declara la entrada de MOD-023 hacia MOD-002 pese a que la decision 2.7.15 nombra al Delegado como consumidor del motor de plazos unico): este backlog declara MOD-023 en depende_de_modulos de toda HU que calcula un plazo, siguiendo la ficha propietaria (MOD-002, seccion L) sobre el mapa, sin modificar mapa_modulos.json.
- La gestion de grupos empresariales con delegado comun y de multiples delegados propietarios simultaneos (Art. 16 y 17 Lineamientos DPO) queda fuera de este backlog por ser FUTURE/COULD en la tabla Q y por la decision de alcance 2.7.31 (V1/Enterprise, seccion 21.1 del roadmap); el MVP soporta un unico responsable activo mas un historico de sustituciones secuenciales.
- Las HU que dependen de la lectura de la bandera regimen_reforma_659 (HU-002-01, HU-002-15, HU-002-16) y del envio del tramite a la ACE (HU-002-05) heredan la incertidumbre juridica documentada en las preguntas pendientes PP-JUR-13, PP-JUR-14, PP-REG-01, PP-REG-02 y PP-REG-06 sobre el numero de decreto, su contenido articulado exacto y el destino del registro transitorio de la ACE; el sistema nunca activa el estado FUTURO ni certifica la recepcion del tramite por si mismo (anti-features 13 y 14).

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-002-01 | Registrar el nombramiento inicial del responsable del programa de datos | Administrador de la organizacion | 3 | R1 | 9 | MOD-001, MOD-024 |
| HU-002-02 | Completar el checklist de perfil y avanzar el nombramiento a pendiente de aceptacion | Administrador de la organizacion | 5 | R1 | 9 | HU-002-01 |
| HU-002-03 | Aceptar el cargo mediante la declaracion jurada de conflicto de intereses | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R1 | 9 | HU-002-02, MOD-023, MOD-021 |
| HU-002-04 | Registrar la notificacion interna del nombramiento dentro del plazo legal | Administrador de la organizacion | 3 | R1 | 9 | HU-002-03, MOD-023, MOD-021, MOD-022 |
| HU-002-05 | Preparar y registrar la comunicacion del nombramiento a la ACE | Administrador de la organizacion | 8 | R1 | 10 | HU-002-04, MOD-023, MOD-021, MOD-024, MOD-022 |
| HU-002-06 | Registrar el rechazo de inscripcion de la ACE y reabrir el nombramiento | Administrador de la organizacion | 5 | R1 | 11 | HU-002-05, HU-002-01, MOD-023, MOD-021, MOD-022 |
| HU-002-07 | Activar el registro tras recibir la credencial o agotarse el plazo de emision | Administrador de la organizacion | 3 | R1 | 10 | HU-002-05, MOD-023 |
| HU-002-08 | Editar los datos de contacto o modalidad de un registro activo | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R1 | 11 | HU-002-07, MOD-023, MOD-021, MOD-022 |
| HU-002-09 | Reverificar el perfil del responsable cada tres anos | Aprobador | 8 | R1 | 11 | HU-002-07, MOD-023, MOD-021, MOD-022 |
| HU-002-10 | Registrar la capacitacion anual del propio responsable | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R1 | 11 | HU-002-07, MOD-021, MOD-023, MOD-022 |
| HU-002-11 | Recibir por referencia la constancia de capacitacion anual generada en MOD-017 | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 2 | R2 | 36 | HU-002-10, MOD-017, MOD-022 |
| HU-002-12 | Registrar el cese y disparar la designacion de sustituto en 10 dias habiles | Administrador de la organizacion | 5 | R1 | 11 | HU-002-07, MOD-023, MOD-021, MOD-022 |
| HU-002-13 | Vigilar el plazo de 10 dias habiles para designar sustituto tras el cese | Administrador de la organizacion | 5 | R1 | 12 | HU-002-12, HU-002-01, MOD-023, MOD-022 |
| HU-002-14 | Mantener la clausula y el contador de confidencialidad post-cese de 5 anos | Responsable Legal / Compliance | 5 | R1 | 12 | HU-002-01, HU-002-12, MOD-023, MOD-022 |
| HU-002-15 | Reaccionar automaticamente cuando cambia el regimen normativo de la reforma 659 | Administrador de la organizacion | 5 | R1 | 10 | HU-002-07, MOD-024, MOD-021, MOD-022 |
| HU-002-16 | Decidir con doble control si mantener al Delegado de forma voluntaria o migrar a Responsable Interno | Aprobador | 5 | R1 | 10 | HU-002-15, MOD-024 |
| HU-002-17 | Exportar el expediente y la bitacora de plazos del responsable del programa de datos | Auditor (interno) | 3 | R1 | 12 | HU-002-01, MOD-023 |

## Historias

### HU-002-01. Registrar el nombramiento inicial del responsable del programa de datos

**Como** Administrador de la organizacion, **quiero** crear el registro de nombramiento del Delegado o Responsable Interno con sus datos basicos, modalidad y contacto institucional, con el tipo_rol precargado segun el regimen normativo vigente, **para** dejar constancia formal de quien ejerce esta funcion, como exige OBL-DPO-01, desde el primer dia de uso del sistema.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 9 | No |

- Fundamento: OBL-DPO-01 (Art. 15 y 17, Ley para la Proteccion de Datos Personales)
- Depende de: -
- Modulos requeridos: MOD-001, MOD-024

**Criterios de aceptacion**

1. Dado que no existe ningun registro de nombramiento en la organizacion, cuando el Administrador de la organizacion o el Responsable Legal inician el alta, entonces el sistema crea un registro en estado BORRADOR sin generar todavia ningun plazo legal
2. Dado que la bandera regimen_reforma_659 de MOD-024 esta en ACTUAL, cuando se crea el registro, entonces el campo tipo_rol se precarga como DELEGADO, editable solo con aprobacion de doble control
3. Dado que la persona a designar ya existe como usuario en MOD-001, cuando se selecciona en el alta, entonces nombre_completo, correo_electronico_institucional y telefono_institucional se precargan desde su perfil de usuario y quedan editables
4. Dado que se selecciona modalidad EXTERNO_PERSONA_JURIDICA, cuando se intenta guardar el registro, entonces el sistema exige completar razon_social_persona_juridica, nit_persona_juridica y persona_natural_responsable antes de continuar
5. Dado que se completa fecha_nombramiento, cuando se ingresa una fecha futura, entonces el sistema rechaza el valor con un mensaje de validacion
6. Dado un usuario con un rol distinto de Administrador de la organizacion o Responsable Legal, cuando intenta crear el registro, entonces el sistema deniega el permiso
7. Dado que se completa el registro en BORRADOR, cuando se guarda cualquier cambio, entonces el sistema registra el evento en el historial del modulo con usuario y fecha

**Reglas de negocio**

- tipo_rol se precarga desde la bandera regimen_reforma_659 de MOD-024 y toma los valores DELEGADO o RESPONSABLE_INTERNO (ficha MOD-002, seccion D)
- El numero de documento de identidad se guarda como dato de referencia, nunca como imagen escaneada, salvo un adjunto puntual de evidencia con acceso restringido (seccion D, minimizacion de datos)
- Crear el registro de nombramiento esta permitido solo a Administrador de la organizacion y a Responsable Legal / Compliance (seccion C)

**Fuera de alcance**

- El checklist de perfil y la declaracion jurada de conflicto de intereses, cubiertos en HU-002-02 y HU-002-03
- La redaccion con fuerza legal del acuerdo o acta de nombramiento ante la maxima autoridad de la empresa, que sigue siendo responsabilidad de la organizacion (seccion H, decision 5)

- Requiere contenido: Modelo de acta de nombramiento de Delegado o Responsable Interno, validado por asesoria legal, para adjuntar como documento_acta_nombramiento
- Referencia: MOD-002 secciones D, F (fila inicial) y H decision 5

### HU-002-02. Completar el checklist de perfil y avanzar el nombramiento a pendiente de aceptacion

**Como** Administrador de la organizacion, **quiero** marcar cada requisito del perfil del Art. 5 de los Lineamientos DPO como cumplido o no cumplido, y que el registro avance a PENDIENTE_ACEPTACION solo cuando todos los campos obligatorios y el checklist esten completos, **para** dejar evidencia de la diligencia de la organizacion sobre el perfil de la persona designada, sin que el sistema certifique su idoneidad.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 9 | No |

- Fundamento: OBL-DPO-01 (Art. 15 y 17, Ley para la Proteccion de Datos Personales)
- Depende de: HU-002-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un registro en BORRADOR con el checklist de requisitos_perfil sin completar, cuando el Administrador de la organizacion intenta avanzarlo a PENDIENTE_ACEPTACION, entonces el sistema bloquea la transicion mientras quede alguna casilla sin marcar explicitamente Si o No
2. Dado que se muestra el checklist de perfil, cuando se presenta en pantalla, entonces el sistema muestra el texto Requiere validacion de la organizacion o asesoria especializada junto a cada requisito
3. Dado un registro en BORRADOR con todos los campos obligatorios de la seccion D completos y el checklist de requisitos_perfil totalmente marcado, cuando el Administrador de la organizacion confirma, entonces el registro pasa a PENDIENTE_ACEPTACION
4. Dado que falta algun campo obligatorio distinto del checklist, por ejemplo documento_identidad o numero_acuerdo_acta, cuando se intenta avanzar el registro, entonces el sistema lista los campos faltantes y no permite la transicion
5. Dado que el registro pasa a PENDIENTE_ACEPTACION, entonces el sistema registra el evento de cambio de estado en el historial del modulo con usuario y fecha
6. Dado un usuario con rol distinto de Administrador de la organizacion, cuando intenta completar el checklist, entonces el sistema deniega el permiso

**Reglas de negocio**

- El checklist de requisitos_perfil incluye grado universitario, mayor de 21 anos, experiencia acreditada, ausencia de sentencia firme por delitos dolosos relacionados y ausencia de sancion firme por infracciones a la LPDP (seccion D)
- El sistema no verifica por si mismo el cumplimiento del perfil; es responsabilidad de la organizacion confirmarlo con la documentacion de respaldo (seccion H, decision 1)

**Fuera de alcance**

- La validacion de que la persona cumple realmente los requisitos del Art. 5, que sigue siendo responsabilidad de la organizacion o de asesoria especializada

- Referencia: MOD-002 secciones D (fila requisitos_perfil), F (transicion BORRADOR a PENDIENTE_ACEPTACION) y H decision 1

### HU-002-03. Aceptar el cargo mediante la declaracion jurada de conflicto de intereses

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** firmar digitalmente la declaracion jurada de conflicto de intereses y aceptar el cargo, **para** formalizar mi nombramiento y cumplir la diligencia previa que exige el Art. 9 de los Lineamientos DPO antes de ejercer la funcion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 9 | No |

- Fundamento: OBL-DPO-01 (Art. 15 y 17, Ley para la Proteccion de Datos Personales)
- Depende de: HU-002-02
- Modulos requeridos: MOD-023, MOD-021

**Criterios de aceptacion**

1. Dado un registro en PENDIENTE_ACEPTACION, cuando la persona designada marca sin conflicto declarado y confirma la aceptacion, entonces el registro pasa a NOMBRADO y se fija fecha_nombramiento con la fecha de la confirmacion
2. Dado que la persona designada marca con situacion declarada, cuando intenta confirmar sin adjuntar la medida correctiva adoptada, entonces el sistema bloquea la aceptacion hasta que se complete ese campo
3. Dado que el registro pasa a NOMBRADO, cuando se completa la transicion, entonces el sistema solicita a MOD-023 la fecha limite de 3 dias habiles para la notificacion interna y crea en MOD-021 la tarea Notificar al Delegado su nombramiento asignada a Administrador de la organizacion
4. Dado que se registra la declaracion jurada, cuando se muestra en pantalla, entonces el sistema presenta el texto Requiere validacion de la organizacion o asesoria especializada junto a la advertencia sobre conflicto de intereses
5. Dado un usuario distinto de la persona designada en el registro, cuando intenta aceptar el cargo en su nombre, entonces el sistema deniega el permiso
6. Dado que la aceptacion se completa, entonces el sistema registra la declaracion jurada firmada, con fecha y contenido declarado, como evidencia del expediente

**Reglas de negocio**

- La aceptacion del cargo exige que la persona designada firme o acepte digitalmente la declaracion jurada antes de pasar a NOMBRADO (seccion F)
- El sistema registra la declaracion y advierte sobre cargos tipicamente incompatibles, pero no decide si el caso concreto configura conflicto de intereses (seccion H, decision 2)

**Fuera de alcance**

- La valoracion de si la situacion declarada configura un conflicto de intereses real, potencial o aparente, que corresponde a la organizacion o a asesoria juridica

- Requiere contenido: Modelo de declaracion jurada de conflicto de intereses, validado por asesoria legal
- Referencia: MOD-002 secciones D (declaracion_jurada_conflicto_intereses), F (PENDIENTE_ACEPTACION a NOMBRADO), G.1 y H decision 2

### HU-002-04. Registrar la notificacion interna del nombramiento dentro del plazo legal

**Como** Administrador de la organizacion, **quiero** adjuntar la constancia de que se notifico internamente a la persona designada su nombramiento, dentro del plazo de 3 dias habiles, **para** cumplir el Art. 8 de los Lineamientos DPO y dejar disparado el plazo de comunicacion a la ACE.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 9 | No |

- Fundamento: OBL-DPO-02 (Art. 8, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-002-03
- Modulos requeridos: MOD-023, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado un registro en NOMBRADO con la fecha limite de 3 dias habiles calculada por MOD-023, cuando el Administrador de la organizacion adjunta la constancia de notificacion interna y confirma, entonces el registro pasa a NOTIFICADO_INTERNAMENTE
2. Dado que el registro pasa a NOTIFICADO_INTERNAMENTE, cuando se completa la transicion, entonces el sistema solicita a MOD-023 la fecha limite de 15 dias habiles para comunicar el nombramiento a la ACE, contada desde el dia siguiente a fecha_nombramiento, y crea en MOD-021 la tarea Comunicar el nombramiento a la ACE
3. Dado que falta 1 dia habil para vencer el plazo de 3 dias habiles sin que la notificacion se haya registrado, entonces el sistema dispara la alerta WARNING Notificacion interna por vencer hacia Administrador de la organizacion
4. Dado que vence el plazo de 3 dias habiles sin registrar la notificacion, entonces el sistema dispara la alerta HIGH Notificacion interna vencida hacia Administrador de la organizacion y Aprobador, con frecuencia diaria hasta que se complete
5. Dado que se intenta registrar la notificacion sin adjuntar la constancia, cuando se confirma, entonces el sistema bloquea la transicion
6. Dado un usuario con rol distinto de Administrador de la organizacion, cuando intenta registrar la notificacion interna, entonces el sistema deniega el permiso

**Reglas de negocio**

- El plazo de notificacion interna es de 3 dias habiles desde fecha_nombramiento y lo calcula siempre MOD-023 (seccion F, G.1)
- MOD-002 nunca calcula plazos por su cuenta; si el calendario de dias habiles del ano no esta configurado, el sistema bloquea la creacion de la fecha limite y alerta al Administrador (seccion P, riesgos operativos)

**Fuera de alcance**

- El envio de la alerta por correo o plataforma, que ejecuta MOD-022
- La creacion y el seguimiento tecnico de la tarea en si, que administra MOD-021

- Referencia: MOD-002 secciones F (NOMBRADO a NOTIFICADO_INTERNAMENTE), G.1, G.2 e I

### HU-002-05. Preparar y registrar la comunicacion del nombramiento a la ACE

**Como** Administrador de la organizacion, **quiero** preparar el contenido de la comunicacion del nombramiento a la ACE, adjuntar el acta y registrarla como tramite pendiente hacia el Centro Regulatorio, dentro del plazo de 15 dias habiles, **para** cumplir el Art. 10 de los Lineamientos DPO y dejar evidencia verificable del intento de comunicacion, sin que el sistema presente el tramite ni certifique su recepcion por la ACE.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 10 | Si |

- Fundamento: OBL-DPO-03 (Art. 10, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-002-04
- Modulos requeridos: MOD-023, MOD-021, MOD-024, MOD-022

**Criterios de aceptacion**

1. Dado un registro en NOTIFICADO_INTERNAMENTE, cuando el Administrador de la organizacion o el Responsable Legal intentan enviar la comunicacion sin tener adjunto documento_acta_nombramiento, entonces el sistema bloquea la accion
2. Dado un registro en NOTIFICADO_INTERNAMENTE con requisitos_perfil incompleto, cuando se intenta enviar la comunicacion, entonces el sistema bloquea la accion hasta que el checklist este completo
3. Dado un registro con documento_acta_nombramiento adjunto y requisitos_perfil completo, cuando se confirma el envio, entonces el registro pasa a COMUNICADO_A_ACE, se fija fecha_comunicacion_ace y el sistema genera un evento saliente hacia el submodulo Tramites ante la ACE de MOD-024 con estado Preparado
4. Dado que se genera el evento hacia MOD-024, cuando se muestra en pantalla, entonces el sistema presenta el texto el sistema deja evidencia del intento de envio, fecha y documento remitido, y no certifica que la ACE lo haya recibido o aceptado mientras el canal oficial de la ACE no este plenamente operativo
5. Dado que faltan 3 dias habiles para vencer el plazo de 15 dias habiles sin haberse enviado la comunicacion, entonces el sistema dispara la alerta WARNING hacia Administrador de la organizacion y Delegado
6. Dado que vence el plazo de 15 dias habiles sin enviarse la comunicacion, entonces el sistema dispara la alerta CRITICAL hacia Administrador de la organizacion, Aprobador y Responsable Legal, visible en el dashboard de Gerencia
7. Dado que la comunicacion se registra como enviada, entonces el sistema conserva el comprobante de envio, con fecha y documento remitido, como evidencia del expediente

**Reglas de negocio**

- El sistema nunca presenta tramites ante la ACE en nombre de la empresa sin que esta lo autorice y ejecute; solo prepara el contenido y deja evidencia del intento (anti-feature 13)
- El plazo de comunicacion es de 15 dias habiles contados desde el dia siguiente a fecha_nombramiento y lo calcula MOD-023 (seccion G.2)

**Fuera de alcance**

- La presentacion efectiva del tramite ante el canal oficial de la ACE, que ejecuta la propia empresa
- La confirmacion de que la ACE recibio o acepto el tramite, que se registra en MOD-024 cuando la empresa la reporte

- Requiere contenido: Modelo u oficio de comunicacion de nombramiento a la ACE, validado por asesoria legal
- Requiere validacion legal: Si (PP-REG-06)
- Referencia: MOD-002 secciones F (NOTIFICADO_INTERNAMENTE a COMUNICADO_A_ACE), G.2, H decision 7 y anti-feature 13

### HU-002-06. Registrar el rechazo de inscripcion de la ACE y reabrir el nombramiento

**Como** Administrador de la organizacion, **quiero** registrar cuando la ACE notifica que no inscribe a la persona designada, y volver a iniciar un nombramiento con otra persona dentro del plazo legal, **para** no dejar a la empresa sin un responsable del tramite valido ante la ACE.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 11 | No |

- Fundamento: OBL-DPO-01 (Art. 15 y 17, Ley para la Proteccion de Datos Personales); OBL-DPO-03 (Art. 10, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-002-05, HU-002-01
- Modulos requeridos: MOD-023, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado un registro en COMUNICADO_A_ACE, cuando el Administrador de la organizacion registra la notificacion formal de incumplimiento de requisitos de la ACE, entonces el registro pasa a RECHAZADO_ACE y el sistema dispara la alerta CRITICAL correspondiente
2. Dado que el registro pasa a RECHAZADO_ACE, entonces el sistema solicita a MOD-023 la cuenta atras de 10 dias habiles para nombrar a otra persona
3. Dado un registro en RECHAZADO_ACE, cuando el Administrador de la organizacion inicia un nuevo nombramiento, entonces el sistema crea un nuevo registro en BORRADOR y archiva el registro anterior con el motivo rechazado por la ACE, sin eliminarlo
4. Dado que el registro anterior queda archivado, cuando se consulta el historial, entonces sigue siendo visible con su motivo de cierre
5. Dado que vencen los 10 dias habiles sin que exista un nuevo registro que llegue a NOMBRADO, entonces el sistema mantiene la alerta CRITICAL visible en el dashboard de Gerencia
6. Dado un usuario con rol distinto de Administrador de la organizacion, cuando intenta registrar el rechazo de la ACE, entonces el sistema deniega el permiso

**Reglas de negocio**

- El registro rechazado nunca se elimina, solo se archiva con motivo (seccion F, anti-feature 19)
- Iniciar un nuevo nombramiento sigue las mismas reglas de alta que HU-002-01

**Fuera de alcance**

- La causa por la que la ACE rechaza la inscripcion, que es decision exclusiva de la Direccion de Proteccion de Datos de la ACE

- Referencia: MOD-002 seccion F (COMUNICADO_A_ACE a RECHAZADO_ACE, y RECHAZADO_ACE a BORRADOR) e I

### HU-002-07. Activar el registro tras recibir la credencial o agotarse el plazo de emision

**Como** Administrador de la organizacion, **quiero** registrar la credencial recibida de la ACE, o que el sistema reconozca automaticamente que el plazo de emision se agoto sin observaciones, para que el registro pase a ACTIVO, **para** que el contacto del responsable del tramite quede disponible para el resto del sistema desde que la designacion queda firme.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 10 | Si |

- Fundamento: OBL-DPO-03 (Art. 10, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-002-05
- Modulos requeridos: MOD-023

**Criterios de aceptacion**

1. Dado un registro en COMUNICADO_A_ACE, cuando el Administrador de la organizacion registra numero_registro_ace o credencial_ace, entonces el registro pasa a ACTIVO
2. Dado un registro en COMUNICADO_A_ACE, cuando transcurren 15 dias habiles desde fecha_comunicacion_ace sin que se haya registrado una observacion de la ACE, entonces el sistema pasa automaticamente el registro a ACTIVO
3. Dado que el registro pasa a ACTIVO, entonces el contacto ARCO-POL derivado, nombre, correo y telefono institucional, queda disponible por referencia para MOD-007, MOD-008 y MOD-011
4. Dado que el registro pasa a ACTIVO, entonces el indicador Estado del nombramiento del dashboard pasa a Verde, salvo que exista otro plazo vencido
5. Dado un usuario con rol distinto de Administrador de la organizacion, cuando intenta registrar la credencial recibida, entonces el sistema deniega el permiso
6. Dado que el registro pasa a ACTIVO, entonces el sistema registra el evento en el historial con la fecha y el mecanismo de activacion, credencial registrada o plazo agotado

**Reglas de negocio**

- El contacto ARCO-POL derivado se inserta en otros modulos como variable de plantilla, por referencia, sin duplicarlo (seccion G.9)

**Fuera de alcance**

- La certificacion de que la ACE efectivamente recibio o proceso el tramite, cubierta como limite en HU-002-05

- Referencia: MOD-002 secciones F (COMUNICADO_A_ACE a ACTIVO), E y M

### HU-002-08. Editar los datos de contacto o modalidad de un registro activo

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** editar mis propios datos de contacto institucional o de modalidad mientras mi registro esta ACTIVO, **para** mantener actualizada la informacion que se publica en el aviso de privacidad y se comunica a la ACE.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 11 | No |

- Fundamento: OBL-DPO-03 (Art. 10, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-002-07
- Modulos requeridos: MOD-023, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado un registro ACTIVO, cuando la persona designada o el Administrador de la organizacion editan correo_electronico_institucional, telefono_institucional, direccion_institucional o modalidad, entonces el sistema guarda el cambio y lo registra en el historial con el valor anterior y el nuevo
2. Dado un registro ACTIVO que ya fue comunicado a la ACE, cuando se edita un campo de contacto o modalidad, entonces el sistema solicita a MOD-023 la fecha limite de 10 dias habiles para actualizar el tramite ante la ACE y crea en MOD-021 la tarea Actualizar el tramite ante la ACE
3. Dado que faltan 2 dias habiles para vencer el plazo de actualizacion de 10 dias habiles, entonces el sistema dispara la alerta WARNING hacia Administrador de la organizacion
4. Dado que se edita el correo_electronico_institucional, cuando se guarda con un formato invalido, entonces el sistema rechaza el cambio
5. Dado un usuario con rol distinto de Administrador de la organizacion o de la propia persona designada, cuando intenta editar estos datos, entonces el sistema deniega el permiso
6. Dado que se marca el tramite de actualizacion como enviado, entonces la alerta de actualizacion pendiente se apaga

**Reglas de negocio**

- Editar un registro ACTIVO ya comunicado dispara el plazo de actualizacion del Art. 10 inciso final de los Lineamientos DPO (seccion G.3)
- Modificar datos de perfil o contacto esta permitido a Administrador de la organizacion y a la persona designada sobre su propio registro (seccion C)

**Fuera de alcance**

- El cambio de tipo_rol, que exige doble control y se cubre en HU-002-16

- Referencia: MOD-002 secciones G.3, C y D

### HU-002-09. Reverificar el perfil del responsable cada tres anos

**Como** Aprobador, **quiero** aprobar la reverificacion periodica del perfil del responsable del programa de datos, respaldada por los atestados de capacitacion o certificacion que la persona designada adjunta, **para** cumplir la reverificacion trienal que exige el Art. 18 de los Lineamientos DPO.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 11 | No |

- Fundamento: OBL-DPO-04 (Art. 18, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-002-07
- Modulos requeridos: MOD-023, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado un registro ACTIVO, cuando faltan 30 dias para cumplir 3 anos desde fecha_nombramiento o desde fecha_ultima_reverificacion, entonces el sistema crea en MOD-021 la tarea Reverificar perfil del Delegado y mueve el registro a EN_REVERIFICACION si la fecha limite llega sin completarse
2. Dado un registro en EN_REVERIFICACION, cuando la persona designada adjunta los atestados_reverificacion y reconfirma el checklist de requisitos_perfil, entonces el registro queda listo para la aprobacion
3. Dado un registro en EN_REVERIFICACION con atestados adjuntos, cuando el Aprobador confirma la reverificacion, entonces el registro vuelve a ACTIVO y se actualiza fecha_ultima_reverificacion
4. Dado que vence la fecha de 3 anos sin completarse la reverificacion, entonces el registro permanece ACTIVO pero el indicador de dashboard pasa a Rojo y el sistema dispara la alerta HIGH hacia Administrador de la organizacion, Aprobador y Responsable Legal
5. Dado un usuario con rol distinto de Aprobador, cuando intenta aprobar la reverificacion, entonces el sistema deniega el permiso
6. Dado que se aprueba la reverificacion, entonces el sistema conserva los atestados de esa reverificacion como evidencia versionada, sin sobrescribir los de reverificaciones anteriores

**Reglas de negocio**

- El plazo de reverificacion es de 3 anos desde el nombramiento o la ultima reverificacion y lo calcula MOD-023, con margen de aviso configurable de 30 dias (seccion G.4)
- El vencimiento sin completar no bloquea el registro porque la ley no lo exige, solo mantiene la alerta activa (seccion F)

**Fuera de alcance**

- La emision o la validez de las certificaciones o constancias de capacitacion presentadas como atestados

- Referencia: MOD-002 secciones F (ACTIVO a EN_REVERIFICACION y de regreso), G.4 e I

### HU-002-10. Registrar la capacitacion anual del propio responsable

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** registrar la fecha y la constancia de mi capacitacion anual en proteccion de datos, **para** cumplir la capacitacion anual que exige el Art. 22 de los Lineamientos DPO.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 11 | No |

- Fundamento: OBL-DPO-05 (Art. 22, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-002-07
- Modulos requeridos: MOD-021, MOD-023, MOD-022

**Criterios de aceptacion**

1. Dado un registro ACTIVO, cuando faltan 30 dias para cumplir 1 ano desde fecha_ultima_capacitacion_delegado, entonces el sistema crea en MOD-021 la tarea Renovar capacitacion anual del Delegado asignada a la persona designada
2. Dado la tarea creada, cuando la persona designada registra fecha_ultima_capacitacion_delegado y adjunta la constancia correspondiente, entonces el sistema guarda el registro como evidencia y marca la tarea como completada
3. Dado que faltan 10 dias para vencer el ciclo anual sin registrar la capacitacion, entonces el sistema dispara la alerta WARNING hacia la persona designada
4. Dado que se intenta registrar la capacitacion sin adjuntar constancia, cuando se confirma, entonces el sistema bloquea el registro
5. Dado un usuario distinto de la persona designada o de Administrador de la organizacion, cuando intenta registrar esta capacitacion, entonces el sistema deniega el permiso

**Reglas de negocio**

- El plazo de capacitacion anual del propio responsable es de 1 ano desde el nombramiento o la ultima capacitacion registrada y lo calcula MOD-023 (seccion G.5)

**Fuera de alcance**

- El plan anual de capacitacion dirigido al resto del personal, OBL-CAP-02, que administra MOD-017
- La recepcion automatica de la constancia desde MOD-017, cubierta en HU-002-11

- Referencia: MOD-002 secciones D (fecha_ultima_capacitacion_delegado), G.5 e I

### HU-002-11. Recibir por referencia la constancia de capacitacion anual generada en MOD-017

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que, cuando complete en MOD-017 una capacitacion dirigida a mi rol, el expediente del responsable del programa de datos reciba automaticamente la referencia a esa constancia, **para** no tener que cargar dos veces la misma constancia de capacitacion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R2 | 36 | No |

- Fundamento: OBL-DPO-05 (Art. 22, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-002-10
- Modulos requeridos: MOD-017, MOD-022

**Criterios de aceptacion**

1. Dado que en MOD-017 se completa un registro de capacitacion cuyo publico destinatario incluye al rol Delegado de Proteccion de Datos, cuando ese registro se completa, entonces MOD-002 recibe la notificacion y ofrece la constancia como referencia disponible para fecha_ultima_capacitacion_delegado, sin duplicar el archivo
2. Dado la referencia recibida, cuando la persona designada la acepta, entonces el sistema actualiza fecha_ultima_capacitacion_delegado con la fecha de esa constancia
3. Dado un registro de capacitacion en MOD-017 dentro de la ventana de reverificacion trienal, cuando se completa, entonces queda disponible como adjunto sugerido para el flujo de reverificacion del perfil descrito en HU-002-09
4. Dado que MOD-017 aun no existe o no esta activo para la organizacion, cuando se necesita registrar la capacitacion anual, entonces el sistema sigue permitiendo el registro manual descrito en HU-002-10 sin bloquear el modulo

**Reglas de negocio**

- MOD-017 conserva el registro original de la capacitacion; MOD-002 solo referencia o adjunta la constancia, sin duplicar el campo (ficha MOD-017, secciones D.4 e I)

**Fuera de alcance**

- La creacion, edicion o aprobacion del programa de capacitacion en si, que es responsabilidad exclusiva de MOD-017

- Referencia: MOD-002 seccion D (plan_capacitacion_personal y fecha_ultima_capacitacion_delegado); MOD-017 secciones D.4, G.8 y G.9
- Notas: Se clasifica en R2 porque depende de que MOD-017 Capacitacion, clasificado en R2 segun la seccion 6 de las instrucciones, exista y notifique la constancia; el registro manual de HU-002-10 ya satisface OBL-DPO-05 desde R1 sin esta pieza

### HU-002-12. Registrar el cese y disparar la designacion de sustituto en 10 dias habiles

**Como** Administrador de la organizacion, **quiero** registrar la fecha y el motivo de cese de la persona designada, y que el sistema exija designar un sustituto dentro de 10 dias habiles, **para** no dejar a la empresa sin responsable del tramite mientras haya solicitudes ARCO-POL activas.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 11 | No |

- Fundamento: OBL-DPO-01 (Art. 15 y 17, Ley para la Proteccion de Datos Personales)
- Depende de: HU-002-07
- Modulos requeridos: MOD-023, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado un registro ACTIVO, cuando el Administrador de la organizacion o el Aprobador registran fecha_cese y motivo_cese, entonces el registro pasa a CESADO
2. Dado que fecha_cese es anterior a fecha_nombramiento, cuando se intenta guardar, entonces el sistema rechaza el valor
3. Dado que motivo_cese no encaja claramente en renuncia, fallecimiento, terminacion de contrato o ausencia temporal, cuando se selecciona la opcion Otra, entonces el sistema exige un texto libre explicando la causal, sin inferirla por si mismo
4. Dado que el registro pasa a CESADO, entonces el sistema solicita a MOD-023 la fecha limite de 10 dias habiles y crea en MOD-021 la tarea Designar sustituto asignada a Administrador de la organizacion
5. Dado que el registro pasa a CESADO, entonces el contacto ARCO-POL derivado queda vacante y el sistema marca esa condicion para que MOD-011 muestre su advertencia
6. Dado que existen tareas pendientes que dependian de la persona cesada, cuando el registro pasa a CESADO, entonces esas tareas se marcan pendiente de reasignar y quedan visibles para el Administrador de la organizacion, sin eliminarse
7. Dado un usuario con rol distinto de Administrador de la organizacion o Aprobador, cuando intenta registrar el cese, entonces el sistema deniega el permiso

**Reglas de negocio**

- El plazo de designacion de sustituto es de 10 dias habiles desde fecha_cese, fundamentado en la continuidad de la figura (OBL-DPO-01, campo nota_actualizacion_fase3 de la matriz de obligaciones) y en el Art. 19 de los Lineamientos DPO (seccion F, automatizacion 7)
- Las tareas pendientes que dependian de la persona cesada nunca se eliminan; se marcan pendientes de reasignar (seccion F, Registros vinculados)

**Fuera de alcance**

- La designacion en si del sustituto, que reutiliza el alta descrita en HU-002-01
- El seguimiento del plazo de 10 dias y su escalamiento, cubiertos en HU-002-13

- Referencia: MOD-002 secciones F (ACTIVO a CESADO), G.7, D (motivo_cese) y H decision 6; OBL-DPO-01 campo nota_actualizacion_fase3 de 01_legal/matriz_obligaciones.json

### HU-002-13. Vigilar el plazo de 10 dias habiles para designar sustituto tras el cese

**Como** Administrador de la organizacion, **quiero** ver el conteo de dias habiles restantes para designar un sustituto tras un cese, y recibir la alerta correspondiente si el plazo vence, **para** no perder de vista la obligacion de continuidad de la figura mientras gestiono otras tareas urgentes.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 12 | No |

- Fundamento: OBL-DPO-01 (Art. 15 y 17, Ley para la Proteccion de Datos Personales)
- Depende de: HU-002-12, HU-002-01
- Modulos requeridos: MOD-023, MOD-022

**Criterios de aceptacion**

1. Dado un registro en CESADO con la tarea Designar sustituto activa, cuando se consulta el registro, entonces el sistema muestra los dias habiles restantes calculados por MOD-023 hasta el limite de 10 dias habiles
2. Dado que un nuevo registro llega a NOMBRADO dentro del plazo de 10 dias habiles, entonces la tarea Designar sustituto se marca completada y la cuenta atras se detiene
3. Dado que vencen los 10 dias habiles sin que exista un nuevo registro en NOMBRADO, entonces el sistema dispara la alerta CRITICAL Sustituto no designado tras cese hacia Administrador de la organizacion y Aprobador, con frecuencia diaria
4. Dado que la alerta CRITICAL esta activa, entonces el indicador queda visible en el dashboard de Gerencia hasta que se resuelva
5. Dado un registro CESADO con un sustituto ya designado, cuando se consulta el historial, entonces el sistema muestra el registro CESADO archivado junto con la referencia al nuevo registro que lo sucede

**Reglas de negocio**

- El registro CESADO queda archivado, visible en el historial, mientras corre el periodo de confidencialidad (seccion F)

**Fuera de alcance**

- El formulario de alta del sustituto en si, cubierto en HU-002-01

- Referencia: MOD-002 secciones F (CESADO a nuevo BORRADOR), I y M

### HU-002-14. Mantener la clausula y el contador de confidencialidad post-cese de 5 anos

**Como** Responsable Legal / Compliance, **quiero** confirmar que el contrato o acta de nombramiento incluye la clausula de confidencialidad post-cese, y que el sistema archive el registro automaticamente cuando se cumplan 5 anos del cese, **para** cumplir el deber de confidencialidad que exige el Art. 36 de los Lineamientos DPO.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 12 | No |

- Fundamento: OBL-DPO-06 (Art. 36, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-002-01, HU-002-12
- Modulos requeridos: MOD-023, MOD-022

**Criterios de aceptacion**

1. Dado un registro en BORRADOR o NOMBRADO, cuando se intenta avanzarlo sin marcar clausula_confidencialidad_postcontractual y su referencia al documento, entonces el sistema bloquea la transicion
2. Dado un registro CESADO, cuando se registra fecha_cese, entonces el sistema inicia el contador de 5 anos de confidencialidad sobre el historial de ese registro
3. Dado que faltan 60 dias para cumplir 5 anos desde fecha_cese, entonces el sistema dispara la alerta INFO hacia Responsable Legal / Compliance y Administrador de la organizacion
4. Dado que transcurren 5 anos desde fecha_cese, entonces el sistema mueve automaticamente el registro a ARCHIVADO y cierra la obligacion de confidencialidad activa, sin eliminar el registro
5. Dado un registro en ARCHIVADO, cuando se consulta, entonces sigue disponible como historico para Delegado, Aprobador, Legal y Auditor
6. Dado un usuario con rol distinto de Administrador de la organizacion o Responsable Legal / Compliance, cuando intenta editar clausula_confidencialidad_postcontractual, entonces el sistema deniega el permiso

**Reglas de negocio**

- El periodo de confidencialidad post-cese es de 5 anos desde fecha_cese y lo calcula MOD-023 (seccion G.7)
- El registro archivado nunca se elimina, permanece disponible como historico (seccion F, anti-feature 19)

**Fuera de alcance**

- La redaccion definitiva de la clausula de confidencialidad para el contrato, que requiere validacion de la organizacion o asesoria especializada

- Requiere contenido: Modelo de clausula de confidencialidad post-cese para incorporar al contrato o acta, validado por asesoria legal o especializada
- Referencia: MOD-002 secciones D (clausula_confidencialidad_postcontractual), F (CESADO a ARCHIVADO) e I

### HU-002-15. Reaccionar automaticamente cuando cambia el regimen normativo de la reforma 659

**Como** Administrador de la organizacion, **quiero** que, cuando la bandera regimen_reforma_659 de MOD-024 cambie de ACTUAL a FUTURO, reciba una tarea de revision y vea que las tareas de pasos exclusivos del regimen actual quedan marcadas como no aplicables, sin perder su historial, **para** saber de inmediato que cambio el marco normativo aplicable a la figura del responsable del programa de datos.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 10 | No |

- Fundamento: OBL-DPO-02 (Art. 8, Lineamientos para el Delegado de Proteccion de Datos Personales); OBL-DPO-03 (Art. 10, Lineamientos para el Delegado de Proteccion de Datos Personales); OBL-DPO-04 (Art. 18, Lineamientos para el Delegado de Proteccion de Datos Personales); OBL-DPO-05 (Art. 22, Lineamientos para el Delegado de Proteccion de Datos Personales); OBL-DPO-06 (Art. 36, Lineamientos para el Delegado de Proteccion de Datos Personales); OBL-DPO-07 (Art. 30, Lineamientos para el Delegado de Proteccion de Datos Personales); OBL-DPO-08 (Art. 17, Ley para la Proteccion de Datos Personales)
- Depende de: HU-002-07
- Modulos requeridos: MOD-024, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado un registro ACTIVO, cuando la bandera regimen_reforma_659 de MOD-024 cambia de ACTUAL a FUTURO, entonces el sistema crea la tarea Revisar si mantiene esta figura de forma voluntaria asignada a Administrador de la organizacion, sin cambiar tipo_rol de forma automatica
2. Dado el cambio de bandera, entonces el sistema dispara la alerta INFO Cambio de estado regulatorio, reforma 659, hacia Administrador de la organizacion, la persona designada y Responsable Legal / Compliance, una unica vez
3. Dado el cambio de bandera, entonces el sistema actualiza la etiqueta de clasificacion visible de OBL-DPO-02 a OBL-DPO-08 de OBLIGATORIO o CONDICIONAL a opcional bajo el estado regulatorio actual, preservando la clasificacion anterior en el historial
4. Dado que existen tareas recurrentes de tipos exclusivos del regimen ACTUAL, por ejemplo la reverificacion trienal o la comunicacion a la ACE, cuando la bandera pasa a FUTURO y no hay una persona con tipo_rol DELEGADO mantenida de forma voluntaria, entonces esas tareas dejan de generarse y las instancias abiertas se marcan no aplica bajo el estado regulatorio actual, ver historial, sin eliminarse
5. Dado un registro cerrado antes del cambio de bandera, cuando se consulta su historial, entonces conserva integras las reglas y la clasificacion vigentes en el momento de su cierre
6. Dado que la bandera regresa de FUTURO a ACTUAL por reversion, entonces el sistema restaura la generacion de las tareas del regimen ACTUAL sin reinterpretar los registros ya cerrados bajo FUTURO

**Reglas de negocio**

- El cambio de bandera nunca lo activa MOD-002; el modulo solo lo lee y reacciona a el (seccion G.8, ficha MOD-024)
- Ninguna tarea ni alerta se recalcula retroactivamente; la clasificacion vigente al momento de generarse cada registro queda preservada (06_mapa_definitivo_de_modulos.md, seccion 5, punto 6)

**Fuera de alcance**

- La activacion o reversion de la bandera regimen_reforma_659 en si, que es exclusiva de MOD-024
- La decision de mantener voluntariamente al Delegado o migrar a Responsable Interno, cubierta en HU-002-16

- Referencia: MOD-002 secciones F (nota de diseno), G.8; 06_mapa_definitivo_de_modulos.md seccion 5, puntos 6 y 7; 12_tareas_y_alertas.md seccion 12.7

### HU-002-16. Decidir con doble control si mantener al Delegado de forma voluntaria o migrar a Responsable Interno

**Como** Aprobador, **quiero** confirmar, junto con quien propone el cambio, si la organizacion mantiene voluntariamente al Delegado certificado bajo el regimen ACTUAL o migra a la figura de Responsable Interno sin certificacion ante la ACE, una vez que la bandera regimen_reforma_659 este en FUTURO, **para** que el cambio de tipo_rol quede respaldado por una decision explicita y con doble control, nunca automatica.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 10 | Si |

- Fundamento: OBL-DPO-01 (Art. 15 y 17, Ley para la Proteccion de Datos Personales); OBL-DPO-02 (Art. 8, Lineamientos para el Delegado de Proteccion de Datos Personales); OBL-DPO-03 (Art. 10, Lineamientos para el Delegado de Proteccion de Datos Personales); OBL-DPO-04 (Art. 18, Lineamientos para el Delegado de Proteccion de Datos Personales); OBL-DPO-05 (Art. 22, Lineamientos para el Delegado de Proteccion de Datos Personales); OBL-DPO-06 (Art. 36, Lineamientos para el Delegado de Proteccion de Datos Personales); OBL-DPO-07 (Art. 30, Lineamientos para el Delegado de Proteccion de Datos Personales); OBL-DPO-08 (Art. 17, Ley para la Proteccion de Datos Personales)
- Depende de: HU-002-15
- Modulos requeridos: MOD-024

**Criterios de aceptacion**

1. Dado que la bandera regimen_reforma_659 esta en FUTURO y existe la tarea Revisar si mantiene esta figura de forma voluntaria, cuando Administrador de la organizacion o la persona designada proponen mantener o migrar, entonces el sistema exige una segunda confirmacion de un usuario con rol Aprobador o Responsable Legal / Compliance antes de aplicar el cambio
2. Dado que quien propone el cambio es la unica persona disponible con rol Aprobador, cuando intenta autoaprobar su propia propuesta, entonces el sistema bloquea la confirmacion y exige un segundo usuario distinto
3. Dado que se confirma con doble control mantener la figura, cuando se aplica la decision, entonces tipo_rol permanece DELEGADO y el registro conserva sus tareas de regimen ACTUAL como buena practica voluntaria
4. Dado que se confirma con doble control migrar a Responsable Interno, cuando se aplica la decision, entonces tipo_rol cambia a RESPONSABLE_INTERNO y el sistema muestra el texto requiere validacion de la organizacion o asesoria especializada antes de la confirmacion final
5. Dado que se aplica cualquiera de las dos decisiones, entonces el sistema registra en el historial quien propuso el cambio, quien lo aprobo y la fecha, sin reinterpretar los registros ya cerrados bajo el regimen anterior
6. Dado que no se ha tomado ninguna decision, cuando se consulta el registro, entonces tipo_rol permanece sin cambios hasta que exista la confirmacion explicita

**Reglas de negocio**

- Aprobar el cambio de tipo_rol exige doble control siempre: quien lo propone no puede ser la unica firma; se requiere ademas Aprobador o Responsable Legal (seccion C, Separacion de funciones)
- El sistema no ejecuta el cambio de tipo_rol sin aprobacion explicita (seccion H, decision 3)

**Fuera de alcance**

- La valoracion del impacto reputacional o de riesgo de mantener o no la figura, que es decision estrategica de la empresa

- Requiere contenido: Texto explicativo de las diferencias entre mantener el Delegado o migrar a Responsable Interno, validado por asesoria legal
- Requiere validacion legal: Si (PP-JUR-14)
- Referencia: MOD-002 secciones C (separacion de funciones), F (nota de diseno), H decision 3; 11_roles_y_permisos.md seccion 11.9

### HU-002-17. Exportar el expediente y la bitacora de plazos del responsable del programa de datos

**Como** Auditor (interno), **quiero** exportar la ficha vigente del responsable del programa de datos y la bitacora de los plazos calculados para este modulo, **para** usar esa evidencia en el programa de auditoria de cumplimiento sin tener que reconstruir manualmente el expediente.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 12 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-002-01
- Modulos requeridos: MOD-023

**Criterios de aceptacion**

1. Dado un registro ACTIVO o su historico, cuando Auditor interno, Responsable Legal / Compliance o Administrador de la organizacion exportan la ficha del responsable, entonces el sistema genera un documento en PDF con los datos vigentes y el resumen del historico
2. Dado que se exporta la bitacora de plazos, cuando se filtra por rango de fechas o por tipo de plazo, entonces el sistema entrega el archivo en XLSX o CSV con todos los plazos calculados por MOD-023 para este modulo, cumplidos y vencidos
3. Dado un Auditor externo invitado con acceso temporal a un expediente especifico, cuando exporta, entonces el sistema limita la exportacion al alcance temporal autorizado
4. Dado un usuario con rol Usuario de consulta / Colaborador, cuando intenta exportar el expediente completo, entonces el sistema deniega el permiso y solo muestra el dato publico de contacto
5. Dado que se completa una exportacion, entonces el sistema registra en el historial quien exporto, que reporte y con que alcance

**Reglas de negocio**

- El rol Auditor, interno o externo, es siempre de solo lectura y no puede comentar, aprobar ni adjuntar evidencia (seccion C, Separacion de funciones)
- El documento de identidad de la persona designada nunca se incluye en estas exportaciones basicas por ser un dato de acceso restringido (seccion D, minimizacion de datos)

**Fuera de alcance**

- El paquete de evidencia con manifiesto y verificacion de integridad, que depende de que MOD-019 este disponible y queda fuera del MVP de este modulo
- El informe de gestion periodico con estadisticas ARCO-POL, que depende de los informes periodicos semestrales excluidos del MVP

- Referencia: MOD-002 secciones C (Exportar), N (Reportes) y J

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Alta y edicion del nombramiento (datos basicos, perfil, modalidad) | HU-002-01, HU-002-06, HU-002-07, HU-002-08 |
| Contador y tarea de notificacion interna (3 dias habiles) | HU-002-03, HU-002-04 |
| Contador, tarea y registro del tramite de comunicacion a la ACE (15 dias habiles) | HU-002-04, HU-002-05, HU-002-07 |
| Declaracion jurada de conflicto de intereses | HU-002-03 |
| Checklist de perfil como autoevaluacion (Art. 5) | HU-002-02 |
| Contador y tarea de reverificacion cada 3 anos | HU-002-09 |
| Contador y tarea de capacitacion anual del propio Delegado | HU-002-10, HU-002-11 |
| Gestion de cese y disparo del plazo de 10 dias para sustituto | HU-002-12, HU-002-13 |
| Clausula y contador de confidencialidad post-cese (5 anos) | HU-002-14 |
| Interruptor de doble estado (lectura de la bandera de MOD-024) | HU-002-01, HU-002-15, HU-002-16 |
