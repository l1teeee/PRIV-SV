# EP-022 Notificaciones (MOD-022)

**Objetivo.** Que la empresa cuente con un unico motor de avisos por plataforma y correo, con destinatario resuelto por rol, niveles INFO a CRITICAL con escalamiento automatico, acuse de recibo obligatorio para lo mas urgente y un historial inmutable, para que ningun plazo legal de otro modulo dependa de que alguien recuerde entrar a revisar el sistema

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R1 | 14 | 54 | 48 | 6 | [MOD-022](../../03_modulos/MOD-022_ficha.md) |

**Notas de la epica.**

- El alcance MUST HAVE se tomo literal de la tabla Q de MOD-022_ficha.md (5 filas): notificacion basica por Plataforma y Correo con resolucion de destinatario por rol, piso minimo de alertas de plazos legales no silenciable, niveles INFO/WARNING/HIGH/CRITICAL con escalamiento automatico, acuse de recibo obligatorio para CRITICAL, e historial inmutable. Esto coincide exactamente con la version minima de 19.3, sin discrepancia entre ambas fuentes.
- El encargo pide resolucion de destinatarios por rol con suplente. La tabla Q de la ficha clasifica la Reasignacion de destinatario por suplente configurado como SHOULD HAVE, y justifica que el MVP puede operar con escalamiento directo (por ejemplo al Administrador de la organizacion o al Delegado/Responsable interno) mientras no exista una regla de suplencia explicita. Se siguio la tabla Q: esta epica construye el escalamiento automatico hacia un destinatario de escalamiento configurado (HU-022-06, MUST HAVE), pero no una pantalla de suplente configurable por rol especifico, que queda para una version posterior junto con el resumen y el horario silencioso.
- La fila Q Reportes exportables avanzados esta clasificada COULD HAVE, pero su propia justificacion dice que el listado basico de notificaciones en XLSX o CSV es MUST HAVE, y la seccion N ya describe ese listado con sus filtros. Se agrego una historia pequena (HU-022-12) solo para ese listado basico; se dejaron fuera la exportacion de la configuracion vigente de Reglas y el reporte de entregas fallidas y reintentos, que siguen COULD HAVE.
- Se excluyeron del todo, por instruccion expresa del encargo y porque la tabla Q las clasifica SHOULD HAVE o FUTURE, las reglas anti-fatiga (deduplicacion, resumen diario o semanal, horario silencioso, silenciar un caso puntual no obligatorio) y los canales adicionales (Microsoft Teams, Slack, SMS, WhatsApp).
- Dos historias (HU-022-13 y HU-022-14) solo pueden construirse cuando existe un evento directo de MOD-011 o de MOD-013 respectivamente. La seccion 6 de las instrucciones clasifica MOD-011 y MOD-013 como modulos de R2, mientras que MOD-022 es infraestructura base de R1; por eso esas dos historias quedaron en release R2, y las otras 12 (que solo necesitan MOD-021, MOD-023 o son internas de MOD-022) quedaron en R1.
- MOD-022 no tiene ninguna obligacion propia ni colaboradora declarada en mapa_modulos.json (obligaciones_propietarias y obligaciones_colaboradoras vacias, ver encabezado de la ficha), por lo que casi todas las historias dejan fundamento vacio. La unica excepcion es HU-022-08 (acuse de recibo obligatorio), donde la propia ficha atribuye ese campo especifico a OBL-PRIN-03 (responsabilidad demostrada, Art. 5 lit. i LPDP) en las secciones D.1 y J.
- Ninguna pregunta pendiente de 24_preguntas_pendientes.md queda abierta para MOD-022: la unica que lo menciona (PP-MAPA-06, sobre una arista entre MOD-012 y MOD-022) ya esta resuelta por la propia ficha en su seccion A.1, y por eso ninguna historia cita un ID de pregunta pendiente.
- La frontera con MOD-011 y MOD-013 (avisos internos de MOD-022 frente a la comunicacion formal a titulares, a la ACE o a la Fiscalia) se dejo como fuera de alcance explicito en las historias de generacion (HU-022-02, 03, 13 y 14): MOD-022 nunca redacta ni envia esa comunicacion, solo el aviso interno de que el plazo se acerca o vencio.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-022-01 | Configurar la regla de notificacion por familia de evento | Administrador de la organizacion | 5 | R1 | 3 | MOD-001 |
| HU-022-02 | Generar notificacion desde un evento de tarea o aprobacion de MOD-021 | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 5 | R1 | 3 | HU-022-01, MOD-021, MOD-001 |
| HU-022-03 | Generar notificacion desde un evento de plazo directo de MOD-023 | Responsable Legal / Compliance | 3 | R1 | 3 | HU-022-01, MOD-023 |
| HU-022-04 | Bloquear la desactivacion del piso minimo de alertas de plazos legales | Administrador de la organizacion | 3 | R1 | 7 | HU-022-01 |
| HU-022-05 | Subir automaticamente el nivel de urgencia de una notificacion activa | Responsable Legal / Compliance | 5 | R1 | 7 | HU-022-02, HU-022-03, MOD-023 |
| HU-022-06 | Escalar automaticamente una notificacion sin respuesta dentro del umbral | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R1 | 7 | HU-022-01, HU-022-02, MOD-001 |
| HU-022-07 | Ajustar con doble control el umbral de escalamiento de una alerta CRITICAL en curso | Administrador de la organizacion | 3 | R1 | 7 | HU-022-06 |
| HU-022-08 | Exigir acuse de recibo explicito para notificaciones CRITICAL | Responsable de Seguridad / IT | 5 | R1 | 7 | HU-022-05 |
| HU-022-09 | Mantener el historial inmutable de cada notificacion | Auditor (interno) | 3 | R1 | 7 | HU-022-02 |
| HU-022-10 | Reintentar el envio fallido por canal externo y alertar el agotamiento | Administrador de la organizacion | 5 | R1 | 7 | HU-022-02 |
| HU-022-11 | Bloquear datos personales en el cuerpo del mensaje externo | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R1 | 9 | HU-022-02, MOD-006 |
| HU-022-12 | Exportar el listado de notificaciones en XLSX o CSV | Administrador de la organizacion | 3 | R1 | 9 | HU-022-09 |
| HU-022-13 | Generar notificacion critica desde el cronometro directo de MOD-011 | Responsable ARCO-POL / Responsable del tramite | 3 | R2 | 34 | HU-022-01, HU-022-08, MOD-011 |
| HU-022-14 | Generar notificacion critica desde el cronometro directo de MOD-013 | Responsable de Seguridad / IT | 3 | R2 | 35 | HU-022-01, HU-022-08, MOD-013 |

## Historias

### HU-022-01. Configurar la regla de notificacion por familia de evento

**Como** Administrador de la organizacion, **quiero** crear y editar, para cada familia de evento del catalogo, el rol o roles destinatarios por defecto, el canal por nivel, el umbral de escalamiento y la frecuencia de repeticion de la Regla de notificacion, **para** que el sistema sepa a quien avisar, por que canal y con que urgencia sin que cada modulo reinvente su propia logica de aviso.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 3 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado el catalogo cerrado de familias de evento de la seccion D.1, cuando el Administrador de la organizacion crea una Regla de notificacion para una familia, entonces debe indicar rol o roles destinatarios por defecto, canal por nivel, umbral de escalamiento y frecuencia de repeticion antes de guardarla
2. Dado que una familia de evento no tiene piso minimo de plazo legal, cuando el Administrador de la organizacion modifica su Regla de notificacion, entonces el cambio se guarda y queda registrado en el historial con el valor anterior, el valor nuevo y el usuario que lo hizo
3. Dado que una familia de evento tiene el piso minimo de plazo legal marcado como Si, cuando el Administrador de la organizacion intenta editar ese indicador, entonces el sistema no permite el cambio porque el campo no es editable cuando es Si
4. Dado un usuario con rol distinto de Administrador de la organizacion, cuando intenta crear una Regla de notificacion, entonces el sistema deniega la accion
5. Dado el rol Delegado de Proteccion de Datos, cuando modifica una Regla de notificacion, entonces solo puede modificar reglas de su propio ambito legal y nunca el indicador de piso minimo
6. Dado que se elimina o se cambia el rol vinculado a una Regla de notificacion activa por un cambio de estructura organizativa, cuando el sistema detecta que la Regla quedo sin destinatario valido, entonces genera una alerta de nivel WARNING hacia el Administrador de la organizacion, que sube a HIGH si no se corrige en 7 dias
7. Dado que no existe ningun usuario activo con el rol configurado en una Regla de notificacion, cuando el Administrador de la organizacion consulta esa Regla, entonces el sistema muestra que el destinatario resuelto esta vacio y remite a la alerta Rol critico sin titular

**Reglas de negocio**

- Una Regla de notificacion existe una por familia de evento (seccion D.2)
- El indicador de piso minimo no es editable cuando su valor es Si (secciones D.2 y H)
- Solo el Administrador de la organizacion crea una Regla de notificacion; el Delegado o Responsable interno solo edita las de su propio ambito legal (seccion C)

**Fuera de alcance**

- Bloquear en tiempo de ejecucion los intentos de silenciar una notificacion de una familia con piso minimo: eso se cubre en HU-022-04

- Referencia: MOD-022 secciones C, D.2, G y O
- Notas: El piso minimo se profundiza en HU-022-04; esta historia cubre el alta, la edicion y el bloqueo de edicion de ese indicador dentro de la Regla

### HU-022-02. Generar notificacion desde un evento de tarea o aprobacion de MOD-021

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** recibir automaticamente, en Plataforma y por correo, un aviso cuando una tarea o aprobacion mia entregada por el Centro de Tareas esta proxima a vencer, vencida, bloqueada o pendiente de aprobacion, **para** poder atenderla a tiempo sin depender de que alguien recuerde revisar el sistema por su cuenta.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 3 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-022-01
- Modulos requeridos: MOD-021, MOD-001

**Criterios de aceptacion**

1. Dado que MOD-021 entrega un evento de Tarea o Aprobacion con Familia de evento, Objeto de origen y Nivel validos, cuando existe una Regla de notificacion activa para esa familia, entonces se genera una Notificacion en estado Generada con el mensaje compuesto segun la plantilla de la familia
2. Dado una Notificacion en estado Generada, cuando el sistema resuelve destinatario y canal, entonces asigna como Destinatario resuelto a los usuarios activos con el rol configurado para esa familia y pasa la Notificacion a En envio
3. Dado que el rol configurado para una familia no tiene ningun usuario activo, cuando el sistema intenta resolver el destinatario, entonces suspende el envio de esa Notificacion y genera en su lugar la alerta Rol critico sin titular dirigida al Administrador de la organizacion
4. Dado un Nivel INFO, cuando la Notificacion se envia, entonces el canal resuelto es unicamente Plataforma
5. Dado un Nivel WARNING, HIGH o CRITICAL, cuando la Notificacion se envia, entonces el canal resuelto incluye Plataforma y Correo electronico como minimo
6. Dado el Canal de entrada de una Notificacion generada por este mecanismo, cuando se compone, entonces su valor es siempre Evento de Tarea (MOD-021), y el Modulo de origen funcional muestra el modulo que origino la regla de negocio aunque sea distinto de MOD-021
7. Dado que el evento entregado por MOD-021 no trae Familia de evento, Objeto de origen o Nivel validos, cuando el sistema lo recibe, entonces no genera ninguna Notificacion

**Reglas de negocio**

- MOD-022 nunca calcula el plazo por su cuenta: siempre lo recibe ya resuelto en el evento (seccion A)
- El Destinatario resuelto son los usuarios activos con el rol configurado para la familia (seccion D.1)
- El Nivel CRITICAL siempre exige Plataforma y Correo como minimo (seccion G)

**Fuera de alcance**

- Redactar o enviar la comunicacion formal a un titular, a la ACE o a la Fiscalia General de la Republica: ese acto pertenece siempre a MOD-011 o a MOD-013
- Calcular la fecha limite de la tarea o de la aprobacion: ese calculo lo hace siempre MOD-023

- Requiere contenido: Plantillas de mensaje por familia de evento, version plataforma y version correo, en lenguaje sencillo y con las variables permitidas listadas, redactadas y revisadas por el equipo de contenido del producto
- Referencia: MOD-022 secciones D.1, F.1, F.2 y G
- Notas: Historia base: todo modulo de recorrido MUST HAVE que no tiene cronometro propio de granularidad fina llega a MOD-022 por este canal, segun la tabla I.1

### HU-022-03. Generar notificacion desde un evento de plazo directo de MOD-023

**Como** Responsable Legal / Compliance, **quiero** recibir un aviso automatico cuando un plazo puramente calendarico, por ejemplo una revision periodica programada, se acerca a su vencimiento aunque no exista una Tarea previa en el Centro de Tareas, **para** no depender de que exista una tarea para enterarme de un vencimiento.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 3 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-022-01
- Modulos requeridos: MOD-023

**Criterios de aceptacion**

1. Dado que MOD-023 entrega un evento de plazo con Familia de evento, Objeto de origen y Nivel validos y sin Tarea previa, cuando existe una Regla de notificacion activa para esa familia, entonces se genera una Notificacion en estado Generada directamente, sin pasar por MOD-021
2. Dado el Canal de entrada de una Notificacion generada por este mecanismo, cuando se compone, entonces su valor es siempre Evento de Plazo (MOD-023)
3. Dado un evento de plazo con Nivel INFO o WARNING, cuando se genera la Notificacion, entonces el canal resuelto sigue la tabla de canales por nivel: Plataforma para INFO, Plataforma y Correo para WARNING
4. Dado que el evento de MOD-023 no trae un Objeto de origen valido, cuando el sistema lo recibe, entonces no genera ninguna Notificacion
5. Dado un evento de revision periodica programada de un tratamiento de MOD-006 sin Tarea previa, cuando llega a MOD-022 por este canal, entonces el Modulo de origen funcional registrado es MOD-006 aunque el Canal de entrada tecnico sea Evento de Plazo (MOD-023)
6. Dado que no existe Regla de notificacion activa para la familia del evento, cuando MOD-023 entrega el evento, entonces no se genera ninguna Notificacion y no se avisa a nadie

**Reglas de negocio**

- El evento de plazo puro de MOD-023 genera la Notificacion sin pasar por MOD-021 (secciones F.2 y L.1)
- El Modulo de origen funcional puede ser distinto del Canal de entrada tecnico (seccion D.1)

**Fuera de alcance**

- Calcular el propio plazo o su fecha limite: siempre lo calcula MOD-023
- Deduplicar o consolidar dos avisos de la misma familia y el mismo objeto de origen: es una regla anti-fatiga fuera de esta version

- Requiere contenido: Plantillas de mensaje para las familias de evento que llegan por este canal, por ejemplo revision periodica, version plataforma y version correo
- Referencia: MOD-022 secciones D.1, F.2, G y I.1 (filas MOD-006, MOD-008, MOD-015, MOD-016, MOD-018)
- Notas: Segundo canal de entrada estructural del modulo junto con MOD-021, segun el diagrama de la seccion L.1

### HU-022-04. Bloquear la desactivacion del piso minimo de alertas de plazos legales

**Como** Administrador de la organizacion, **quiero** que el sistema me impida desactivar, silenciar o reducir el canal obligatorio de cualquier familia de notificacion marcada con piso minimo de plazo legal, y que deje registro de cualquier intento, **para** que ningun plazo OBLIGATORIO quede sin aviso por una configuracion equivocada o deliberada.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 7 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-022-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado una Regla de notificacion cuyo indicador Si el piso minimo aplica es Si, cuando cualquier usuario intenta desactivarla, silenciarla o excluirla de un resumen, entonces el sistema no lo permite y muestra el texto Esta alerta corresponde a un plazo legal y no puede desactivarse ni agruparse en un resumen
2. Dado ese mismo intento bloqueado, cuando ocurre, entonces queda registrado en el historial como intento, con la identidad de quien lo intento y la fecha, aunque el sistema lo haya bloqueado
3. Dado una familia de evento con piso minimo, cuando se genera una Notificacion de esa familia, entonces se entrega siempre de forma individual e inmediata, nunca agrupada con otras
4. Dado una Notificacion de Nivel CRITICAL, cuando se genera, entonces el canal resuelto incluye Plataforma y Correo electronico sin excepcion configurable, sin importar la preferencia del usuario destinatario
5. Dado el Administrador de la organizacion, cuando intenta cambiar el indicador Si el piso minimo aplica de Si a No para reducir el nivel de una familia, entonces el sistema no expone ninguna accion para hacerlo
6. Dado un Auditor (interno), cuando consulta el historial de una Regla de notificacion con piso minimo, entonces puede ver todos los intentos bloqueados de desactivarla, con identidad y fecha, en modo de solo lectura

**Reglas de negocio**

- El piso minimo aplica a toda familia ligada a un plazo que la ley fija, y no admite excepcion de ningun rol, incluido el Administrador (seccion H)
- Todo intento de silenciar una familia con piso minimo queda registrado aunque el sistema lo bloquee (seccion O)

**Fuera de alcance**

- Permitir cualquier excepcion al piso minimo, incluso a pedido del Administrador de la organizacion o de cualquier otro rol

- Referencia: MOD-022 secciones C, G, H (decision 1) y O

### HU-022-05. Subir automaticamente el nivel de urgencia de una notificacion activa

**Como** Responsable Legal / Compliance, **quiero** que el nivel de una notificacion suba automaticamente de WARNING a HIGH y de HIGH a CRITICAL a medida que se acerca el vencimiento del plazo asociado, **para** darme cuenta de la urgencia real sin tener que calcular yo mismo cuanto tiempo queda.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 7 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-022-02, HU-022-03
- Modulos requeridos: MOD-023

**Criterios de aceptacion**

1. Dado una Notificacion en Nivel WARNING cuyo plazo asociado llega a 5 dias habiles de vencer, cuando el sistema evalua el tiempo restante que le entrega MOD-023, entonces sube el Nivel a HIGH
2. Dado una Notificacion en Nivel HIGH cuyo plazo asociado llega a 24 horas de vencer, cuando el sistema evalua el tiempo restante, entonces sube el Nivel a CRITICAL
3. Dado que el Nivel de una Notificacion sube, cuando eso ocurre, entonces el cambio queda registrado en el historial con fecha y hora, y se recompone el canal resuelto segun el nuevo Nivel
4. Dado un Nivel ya subido a HIGH o CRITICAL, cuando el objeto de origen aun no se resuelve, entonces el Nivel nunca baja por si solo
5. Dado un Nivel subido, cuando el objeto de origen se resuelve, por ejemplo la Tarea o Aprobacion se completa, entonces la Notificacion pasa a Resuelta sin que el Nivel se reduzca antes de eso
6. Dado que un evento directo de MOD-011 o de MOD-013 ya trae el Nivel calculado por su propio modulo de origen, cuando MOD-022 lo recibe, entonces no vuelve a calcular ni a modificar ese Nivel por su cuenta

**Reglas de negocio**

- El Nivel de una familia puede subir automaticamente al acercarse el vencimiento, nunca baja salvo que el evento de origen se resuelva (seccion D.1)
- Los eventos directos de MOD-011 y MOD-013 llegan con el Nivel ya calculado por su propio modulo de origen (seccion G)

**Fuera de alcance**

- Calcular por si mismo el tiempo restante del plazo: ese calculo siempre lo entrega MOD-023
- Recalcular el Nivel de eventos directos de MOD-011 o MOD-013, que llegan con el Nivel ya calculado por su propio modulo

- Referencia: MOD-022 secciones D.1 (campo Nivel) y G

### HU-022-06. Escalar automaticamente una notificacion sin respuesta dentro del umbral

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** recibir automaticamente una notificacion de escalamiento cuando el destinatario original de una alerta no la lee, no la acusa ni resuelve el objeto de origen dentro del umbral configurado de su familia, **para** poder intervenir a tiempo en un plazo critico que de otro modo dependeria de una sola persona disponible.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 7 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-022-01, HU-022-02
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado que transcurre el umbral de escalamiento configurado para la familia de una Notificacion sin que el Destinatario resuelto la lea, la acuse o resuelva el Objeto de origen, cuando el sistema lo detecta, entonces marca el Estado de escalamiento como Escalada nivel 1 y genera una nueva Notificacion vinculada hacia el destinatario de escalamiento configurado
2. Dado que la Notificacion original queda marcada Escalada, cuando eso ocurre, entonces su propio Estado, sea Generada, En envio, Enviada, Entregada, Leida, Acusada o Resuelta, no cambia por el solo hecho de escalar
3. Dado que transcurre un nuevo umbral sin respuesta despues de Escalada nivel 1, cuando el sistema lo detecta, entonces sube el Estado de escalamiento a Escalada nivel 2, y si vuelve a transcurrir sin respuesta, a Escalada a Gerencia
4. Dado una familia sin un destinatario de escalamiento configurado, cuando el sistema necesita escalar, entonces no elige a nadie por su cuenta y muestra el texto No hay una persona configurada para recibir este aviso si el responsable original no atiende. Configure un suplente o asignelo manualmente
5. Dado un escalamiento generado, cuando ocurre, entonces queda registrado en el historial con el destinatario original, el destinatario de escalamiento y el tiempo transcurrido sin respuesta
6. Dado un escalamiento hacia un destinatario adicional, cuando se genera, entonces nunca reasigna automaticamente la Tarea o la Aprobacion de origen a otra persona, solo copia el aviso

**Reglas de negocio**

- Ningun escalamiento reasigna automaticamente la Tarea o la Aprobacion de origen a otra persona, solo copia el aviso (seccion 12.4.3 de 12_tareas_y_alertas.md)
- El destinatario de escalamiento debe estar configurado por adelantado; el sistema nunca lo elige por su cuenta (seccion H)

**Fuera de alcance**

- Reasignar automaticamente la Tarea o la Aprobacion de origen a otra persona
- Elegir por su cuenta un destinatario de escalamiento cuando ninguno esta configurado

- Referencia: MOD-022 secciones D.1 (Estado de escalamiento), F.1, F.2, G, H (decision 4)

### HU-022-07. Ajustar con doble control el umbral de escalamiento de una alerta CRITICAL en curso

**Como** Administrador de la organizacion, **quiero** proponer ampliar o reducir el umbral de escalamiento de una notificacion CRITICAL que ya esta en curso, y que el cambio solo se aplique con la confirmacion de una segunda persona, **para** poder ajustar un caso puntual sin que una sola persona pueda relajar por si sola el escalamiento de un plazo legal critico.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 7 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-022-06
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado una Notificacion de Nivel CRITICAL en curso, cuando el Administrador de la organizacion propone un nuevo umbral de escalamiento, entonces el cambio queda pendiente de confirmacion y no se aplica todavia
2. Dado un cambio de umbral pendiente, cuando lo confirma una segunda persona con el rol Delegado de Proteccion de Datos o Responsable Legal / Compliance, entonces el nuevo umbral se aplica y queda registrado con ambas identidades y la fecha
3. Dado un cambio de umbral pendiente, cuando lo intenta confirmar la misma persona que lo propuso, entonces el sistema no lo permite
4. Dado un cambio de umbral pendiente, cuando ningun usuario con el rol requerido lo confirma, entonces el umbral original sigue vigente y el escalamiento automatico de la Notificacion sigue su curso sin modificarse
5. Dado un usuario con rol distinto de Administrador de la organizacion, cuando intenta proponer el cambio de umbral, entonces el sistema deniega la accion

**Reglas de negocio**

- La unica accion de este modulo con doble control es ampliar o reducir el umbral de escalamiento de una alerta CRITICAL en curso (seccion C)

**Fuera de alcance**

- Cambiar el umbral de escalamiento de familias sin piso minimo por este mecanismo: ese ajuste ya esta cubierto por la edicion normal de la Regla de notificacion en HU-022-01

- Referencia: MOD-022 seccion C (nota de doble control)

### HU-022-08. Exigir acuse de recibo explicito para notificaciones CRITICAL

**Como** Responsable de Seguridad / IT, **quiero** confirmar dentro de la plataforma, con una accion explicita, que vi y entendi una notificacion CRITICAL, sin que la sola apertura del correo cuente como esa confirmacion, **para** que la organizacion pueda demostrar que una persona identificada realmente atendio el aviso mas urgente del sistema.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 7 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-022-05
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado una Notificacion de Nivel CRITICAL en estado Leida, cuando el Destinatario resuelto usa la accion Confirmar que revise esto dentro de la plataforma, entonces la Notificacion pasa a Acusada con identidad, fecha y hora registradas
2. Dado que el proveedor de correo reporta que el Destinatario resuelto abrio el mensaje externo, cuando eso ocurre, entonces el sistema nunca lo interpreta como Acuse y muestra el texto La apertura del correo no cuenta como confirmacion. Debe confirmar dentro de la plataforma que vio y entendio este aviso
3. Dado una Notificacion de Nivel CRITICAL en estado Acusada, cuando el Objeto de origen se resuelve, entonces la Notificacion pasa a Resuelta; mientras el Objeto de origen no se resuelva, la Notificacion no llega a Resuelta aunque ya este Acusada
4. Dado un Auditor (interno), cuando abre una Notificacion CRITICAL para revisarla, entonces puede verla pero el sistema no le ofrece la accion Confirmar que revise esto porque su rol es de solo lectura
5. Dado una Notificacion de Nivel INFO, WARNING o HIGH, cuando llega a Leida, entonces no exige ningun Acuse antes de poder pasar a Resuelta
6. Dado una Notificacion CRITICAL sin Acuse registrado transcurrido el umbral configurado, cuando el Auditor (interno) o el Delegado consultan el caso, entonces el sistema muestra que el aviso no fue confirmado a tiempo con el texto El sistema registra que este aviso no fue confirmado a tiempo, pero no puede determinar si esto ya configura un incumplimiento sancionable. Consulte a su Delegado o Responsable interno o a asesoria especializada, sin afirmar por si mismo que hubo incumplimiento

**Reglas de negocio**

- La apertura de un correo nunca sustituye el Acuse de recibo exigido para CRITICAL (seccion H)
- El Acuse se registra con identidad, fecha y hora, y se notifica al modulo de origen (secciones F.2 y E)

**Fuera de alcance**

- Decidir si la ausencia de acuse ya configura un incumplimiento sancionable: esa evaluacion es siempre del Delegado, del Responsable interno o de asesoria especializada

- Referencia: MOD-022 secciones D.1 (Acuse de recibo), F.2, H (decisiones 2 y 5) y J

### HU-022-09. Mantener el historial inmutable de cada notificacion

**Como** Auditor (interno), **quiero** consultar, en modo de solo lectura, el historial completo de cada notificacion con la fecha y hora de cada cambio de estado, Generada, En envio, Enviada, Fallida, Entregada, Leida, Acusada, Escalada y Resuelta, **para** usarlo como evidencia de que la organizacion fue alertada a tiempo de un plazo o de un pendiente.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 7 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-022-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado cualquier cambio de Estado de una Notificacion, cuando ocurre, entonces queda registrado en su historial con fecha y hora exactas, y se replica en el AuditLog transversal
2. Dado el Auditor (interno), cuando consulta el historial general de notificaciones de la organizacion, entonces puede verlo completo en modo de solo lectura, sin poder crear, silenciar ni modificar ninguna Regla
3. Dado un Auditor externo (invitado), cuando consulta el historial, entonces solo ve el acotado al expediente o al periodo de la auditoria puntual para la que fue invitado
4. Dado cualquier rol, incluido el Administrador de la organizacion, cuando intenta editar o eliminar un registro del historial de una Notificacion, entonces el sistema no lo permite y muestra el texto El historial de notificaciones no puede eliminarse; solo puede archivarse al resolverse
5. Dado una Notificacion que llega a Resuelta, cuando eso ocurre, entonces se archiva conservando su historial completo, sin que nadie pueda borrarlo
6. Dado que el Objeto de origen de una Notificacion Resuelta se reabre, cuando el modulo de origen dispara una nueva Generacion, entonces la Notificacion anterior conserva su propio historial sin alterarse

**Reglas de negocio**

- El historial de una Notificacion nunca se borra, solo se archiva al llegar a Resuelta (anti-features item 19)
- Toda Notificacion Resuelta conserva su historial aunque el Objeto de origen se reabra despues (seccion F.2)

**Fuera de alcance**

- Ofrecer alguna funcion de edicion o borrado del historial para cualquier rol, incluido el Administrador de la organizacion

- Referencia: MOD-022 secciones C, F.2, J y O

### HU-022-10. Reintentar el envio fallido por canal externo y alertar el agotamiento

**Como** Administrador de la organizacion, **quiero** que el sistema reintente automaticamente el envio de una notificacion por un canal externo que fallo, y que me avise cuando se agoten los reintentos, **para** enterarme de que un aviso no llego por una causa tecnica en vez de que la falla quede en silencio.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 7 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-022-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el canal externo de una Notificacion en En envio reporta un error, cuando eso ocurre, entonces la Notificacion pasa a Fallida y el sistema reintenta el envio segun la politica configurada, por defecto 3 intentos con espera creciente
2. Dado que se agotan los reintentos configurados, cuando eso ocurre, entonces el sistema genera la alerta de sistema Entrega fallida de Nivel WARNING dirigida al Administrador de la organizacion por el canal Plataforma
3. Dado que la Notificacion original que fallo era de Nivel CRITICAL, cuando se agotan los reintentos, entonces la alerta de sistema Entrega fallida se genera en Nivel HIGH en vez de WARNING
4. Dado una alerta de Entrega fallida sobre una Notificacion CRITICAL, cuando pasa 1 hora sin que el canal externo confirme una entrega correcta, entonces escala hacia el Delegado de Proteccion de Datos
5. Dado cada reintento de envio por canal externo, cuando ocurre, entonces queda registrado en el historial con su resultado
6. Dado que el canal externo vuelve a confirmar entregas correctamente, cuando eso ocurre, entonces la alerta Entrega fallida se apaga

**Reglas de negocio**

- Por defecto se reintenta 3 veces con espera creciente antes de marcar Fallida en definitiva (secciones F.2 y G)
- Una Notificacion CRITICAL sin entregar 1 hora despues de agotar los reintentos escala al Delegado o Responsable interno (seccion I)

**Fuera de alcance**

- Reasignar automaticamente el canal para el destinatario: ese reenvio manual es una accion humana, no una automatizacion de esta historia

- Referencia: MOD-022 secciones D.1, E, F.2, G y I (fila Entrega fallida)

### HU-022-11. Bloquear datos personales en el cuerpo del mensaje externo

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que el sistema impida que el cuerpo del mensaje enviado por un canal externo como el correo contenga un dato personal de un titular o el detalle sustantivo de un caso, dejando solo un aviso generico y un enlace de acceso autenticado a la plataforma, **para** confiar en que ningun canal externo, que esta fuera del perimetro de control de la plataforma, expone datos de titulares.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 9 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-022-02
- Modulos requeridos: MOD-006

**Criterios de aceptacion**

1. Dado el Cuerpo del mensaje version correo u otro canal externo de una Notificacion, cuando se compone, entonces solo puede incluir el aviso generico, la referencia al Objeto de origen si la plantilla lo permite, y el enlace de acceso autenticado a la plataforma
2. Dado que la plantilla de una familia intenta insertar un campo marcado como dato personal en MOD-006, cuando el sistema compone el Cuerpo del mensaje para un canal externo, entonces bloquea la generacion de ese mensaje en vez de enviarlo o de preguntar
3. Dado el Cuerpo del mensaje version plataforma de una Notificacion, cuando se compone, entonces tampoco incluye el dato personal del titular ni el detalle sustantivo de un incidente, aunque se vea dentro de la plataforma autenticada
4. Dado un enlace de acceso incluido en el mensaje externo, cuando alguien lo abre sin autenticarse, entonces no puede ver el detalle del caso: la autenticacion de la plataforma sigue exigiendose igual que para cualquier otro acceso
5. Dado un Titulo de Notificacion, cuando se genera, entonces respeta el maximo de 140 caracteres y no incluye ningun dato personal del titular

**Reglas de negocio**

- Ninguna plantilla de canal externo puede incluir un dato personal de titular ni el detalle sustantivo de un caso; el sistema bloquea, no pregunta (seccion H y anti-features items 8 y 9)
- El mensaje externo se limita siempre a un aviso generico mas un enlace de acceso autenticado (seccion D.1)

**Fuera de alcance**

- Permitir alguna excepcion configurable a esta regla, aunque el usuario que configura la plantilla lo solicite

- Requiere contenido: Lista de variables permitidas y prohibidas por plantilla de mensaje, revisada por el equipo de contenido del producto antes de publicarse
- Referencia: MOD-022 secciones D.1, H (decision 7) y K

### HU-022-12. Exportar el listado de notificaciones en XLSX o CSV

**Como** Administrador de la organizacion, **quiero** exportar el listado de notificaciones filtrando por familia, nivel, destinatario, rango de fechas y modulo de origen, **para** usarlo como respaldo operativo o para responder a una auditoria sin tener que revisar notificacion por notificacion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 9 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-022-09
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado el listado de notificaciones, cuando el Administrador de la organizacion aplica filtros por familia, nivel, destinatario, rango de fechas o modulo de origen, cualquiera de ellos o combinados, entonces el listado exportado respeta esos filtros
2. Dado el listado filtrado, cuando el Administrador de la organizacion lo exporta, entonces puede elegir formato XLSX o CSV
3. Dado un Auditor (interno), cuando exporta el listado, entonces obtiene el mismo reporte en modo de solo lectura sobre todas las notificaciones de la organizacion
4. Dado un Auditor externo (invitado), cuando exporta el listado, entonces solo puede hacerlo acotado al expediente o periodo de su auditoria puntual
5. Dado un Usuario de consulta / Colaborador, cuando intenta exportar el listado de notificaciones, entonces el sistema deniega la accion
6. Dado cualquier exportacion de este reporte, cuando ocurre, entonces queda registrada en el historial con quien exporto, cuando y que filtros uso

**Reglas de negocio**

- El listado exportable respeta los mismos permisos de lectura que ya tiene cada rol sobre las notificaciones (seccion C)
- Toda exportacion queda registrada en el historial (seccion O)

**Fuera de alcance**

- Exportar el reporte de configuracion vigente de Reglas de notificacion o el de entregas fallidas y reintentos: ambos siguen clasificados COULD HAVE y quedan fuera de esta version

- Referencia: MOD-022 seccion N (fila Listado de notificaciones) y seccion Q (fila Reportes exportables avanzados)
- Notas: La fila Q Reportes exportables avanzados esta clasificada COULD HAVE, pero su propia justificacion dice que el listado basico de notificaciones en XLSX o CSV es MUST HAVE; esta historia cubre solo ese listado basico

### HU-022-13. Generar notificacion critica desde el cronometro directo de MOD-011

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** recibir una notificacion critica automatica cuando el cronometro de un plazo propio de una solicitud ARCO-POL, sea prevencion, plazo general, incompetencia, notificacion a receptores o denegatoria, se acerca a su vencimiento, **para** actuar a tiempo sobre un plazo legal sin depender de revisar el expediente por mi cuenta.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 34 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-022-01, HU-022-08
- Modulos requeridos: MOD-011

**Criterios de aceptacion**

1. Dado que MOD-011 entrega un evento directo de cronometro con Familia de evento, Objeto de origen y Nivel ya calculados por su propia tabla de alertas, cuando existe una Regla de notificacion activa para esa familia, entonces MOD-022 genera la Notificacion con el Nivel que MOD-011 ya calculo, sin recalcularlo
2. Dado el Canal de entrada de una Notificacion generada por este mecanismo, cuando se compone, entonces su valor es siempre Evento directo ARCO-POL (MOD-011)
3. Dado que el evento directo de MOD-011 llega en Nivel CRITICAL, cuando se genera la Notificacion, entonces exige Acuse de recibo antes de considerarse Resuelta, igual que cualquier otra Notificacion CRITICAL
4. Dado el Responsable ARCO-POL / Responsable del tramite como Destinatario resuelto, cuando la Regla de notificacion de esa familia no tiene ningun usuario activo con ese rol, entonces se genera la alerta Rol critico sin titular en vez de la Notificacion
5. Dado que el evento directo de MOD-011 no trae un Nivel valido, cuando el sistema lo recibe, entonces no genera ninguna Notificacion

**Reglas de negocio**

- MOD-022 gestiona solo el aviso interno del cronometro; la respuesta ARCO-POL y sus notificaciones formales siguen siendo actos propios de MOD-011 (seccion A.1)

**Fuera de alcance**

- Redactar o enviar la respuesta ARCO-POL, la notificacion de denegatoria o la notificacion a receptores: esos actos son siempre de MOD-011

- Referencia: MOD-022 secciones D.1, G, I.1 (fila MOD-011) y L.2
- Notas: Release R2 porque depende exclusivamente de MOD-011, que la seccion 6 de las instrucciones clasifica en R2; las demas historias de esta epica solo necesitan MOD-021, MOD-023 o son internas de MOD-022 y por eso quedan en R1

### HU-022-14. Generar notificacion critica desde el cronometro directo de MOD-013

**Como** Responsable de Seguridad / IT, **quiero** recibir una notificacion critica automatica cuando el cronometro de 72 horas de un incidente de seguridad en curso se acerca a su vencimiento, **para** actuar de inmediato sobre el aviso mas urgente del sistema.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 35 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-022-01, HU-022-08
- Modulos requeridos: MOD-013

**Criterios de aceptacion**

1. Dado que MOD-013 entrega un evento directo de cronometro con Familia de evento, Objeto de origen y Nivel ya calculados por su propia tabla de alertas, cuando existe una Regla de notificacion activa para esa familia, entonces MOD-022 genera la Notificacion con el Nivel que MOD-013 ya calculo, sin recalcularlo
2. Dado el Canal de entrada de una Notificacion generada por este mecanismo, cuando se compone, entonces su valor es siempre Evento directo Incidentes (MOD-013)
3. Dado que el evento directo de MOD-013 llega en Nivel CRITICAL, cuando se genera la Notificacion, entonces exige Acuse de recibo antes de considerarse Resuelta y el canal resuelto incluye Plataforma y Correo sin excepcion
4. Dado el Responsable de Seguridad / IT como Destinatario resuelto, cuando la Regla de notificacion de esa familia no tiene ningun usuario activo con ese rol, entonces se genera la alerta Rol critico sin titular en vez de la Notificacion
5. Dado que el evento directo de MOD-013 no trae un Objeto de origen valido, cuando el sistema lo recibe, entonces no genera ninguna Notificacion
6. Dado que la Notificacion CRITICAL de este cronometro no se acusa dentro del umbral y el plazo legal asociado esta a menos del 25 por ciento de su tiempo total, cuando el sistema lo detecta, entonces sube la alerta de Nivel HIGH a CRITICAL

**Reglas de negocio**

- MOD-022 gestiona solo el aviso interno del cronometro de 72 horas; la notificacion de la vulneracion a la ACE, a la Fiscalia y a los titulares sigue siendo un acto propio de MOD-013 (seccion A.1)

**Fuera de alcance**

- Redactar o enviar la notificacion de la vulneracion a la ACE, a la Fiscalia General de la Republica o a los titulares: ese acto es siempre de MOD-013

- Referencia: MOD-022 secciones D.1, G, I (fila Notificacion CRITICAL sin acuse), I.1 (fila MOD-013) y L.2
- Notas: Release R2 por la misma razon que HU-022-13: depende exclusivamente de MOD-013, clasificado R2 en la seccion 6 de las instrucciones

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Notificacion basica por Plataforma y Correo, con resolucion de destinatario por rol | HU-022-01, HU-022-02, HU-022-03, HU-022-10, HU-022-11, HU-022-13, HU-022-14 |
| Piso minimo de alertas de plazos legales, no silenciable ni configurable a la baja | HU-022-04 |
| Niveles INFO/WARNING/HIGH/CRITICAL con escalamiento automatico | HU-022-05, HU-022-06, HU-022-07 |
| Acuse de recibo obligatorio para notificaciones CRITICAL | HU-022-08 |
| Historial inmutable de notificaciones (generada, enviada, entregada, leida, acusada, escalada) | HU-022-09 |
| Listado basico de notificaciones exportable en XLSX o CSV (la fila Q Reportes exportables avanzados esta clasificada COULD HAVE, pero su propia justificacion reconoce este listado basico como MUST HAVE) | HU-022-12 |
