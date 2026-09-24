# EP-023 Calendario y Motor de Plazos (MOD-023)

**Objetivo.** Toda obligacion con plazo legal del sistema (ARCO-POL, Delegado, Incidentes y Procedimiento sancionador) se calcula una sola vez con el mismo calendario de dias habiles salvadoreno, con desglose verificable, suspension, prorroga y recalculo siempre notificado, y se consulta en una vista de calendario central unica.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R1 | 11 | 54 | 54 | 0 | [MOD-023](../../03_modulos/MOD-023_ficha.md) |

**Notas de la epica.**

- MOD-023 es 100% R1: el modulo no depende de ningun otro (seccion L.2 de la ficha, depende_de vacio) y es infraestructura consumida desde el primer dia por MOD-002, MOD-011 y MOD-013, todos MUST HAVE; ademas figura de forma explicita en el nucleo vendible de la seccion 19.8. Las 11 HU de esta epica se marcan release R1.
- Se excluyen del alcance, por estar clasificadas SHOULD HAVE o COULD HAVE en la tabla Q de la ficha: la capa 5 diferenciada de calendario de la autoridad (SHOULD HAVE; el MVP aplica las capas 0 a 2 tambien a los plazos frente a la ACE, criterio mas generoso, nunca mas corto); la capa 3 de asuetos locales por sede (SHOULD HAVE); la configurabilidad del criterio de las 72 horas hacia horas habiles con doble control (SHOULD HAVE); y la configuracion de horario habil propio o sabado habil para metas internas (COULD HAVE, capa 4). El encargo pedia incluir la opcion configurable del criterio de las 72 horas, pero se sigue la clasificacion de la tabla Q (regla de la seccion 3 de INSTRUCCIONES_HU.md): el MVP calcula siempre con el criterio conservador (horas corridas), mostrado con su advertencia, sin la interfaz de cambio con doble control. Por el mismo motivo tampoco se construye la interfaz para activar la causal de que la prevencion del Art. 18 suspenda el plazo de 20 dias: la mecanica generica de suspension si se construye (HU-023-06), pero ese interruptor especifico permanece en su valor conservador por defecto (No suspende).
- La tabla Q no tiene una fila propia para prorroga, pero la ficha (secciones D.2, F.3, F.4 y O) la describe como parte intrinseca del ciclo de vida del calculo, y OBL-ARCO-10 (plazo de 20 mas 20 dias habiles, propietario MOD-011, MUST HAVE) la exige desde el primer dia. Se incluye como HU MUST HAVE inferida por necesidad estructural de un modulo MUST HAVE dependiente (HU-023-07), con el mismo criterio que la propia ficha ya aplica a la suspension. Se recomienda agregar esta fila a la tabla Q en una proxima revision de la ficha.
- La cobertura parcial de MOD-018 (seccion 19.4 del roadmap) se construye dentro de esta epica (HU-023-11) porque el mecanismo mismo, un recordatorio generico anclado a la fecha de adecuacion inicial del diagnostico, vive en MOD-023 y no en MOD-018 (que todavia no existe como modulo en R1). Usa el cierre de la primera sesion de Diagnostico inicial (MOD-004) como fecha de adecuacion inicial, crea una tarea generica en MOD-021 y una alerta INFO en MOD-022, sin el flujo estructurado de hallazgos y plan de accion que solo existira cuando MOD-018 se active.
- No se incluye una HU de reportes o exportaciones (seccion N de la ficha) porque ninguna fila de la tabla Q clasifica un reporte de MOD-023 como MUST HAVE; el historial y el desglose que un reporte exportaria ya quedan cubiertos como parte de las HU de calculo, suspension, prorroga y recalculo.
- Se documenta, sin corregirlo (la tarea no autoriza modificar otros archivos), el desacuerdo que la propia ficha ya senala en su nota final: el campo obligaciones_colaboradoras de MOD-023 en mapa_modulos.json no incluye OBL-ARCO-11, OBL-ARCO-12, OBL-ARCO-14, OBL-CONS-03, OBL-DPO-04 ni OBL-SANC-06, aunque la ficha (seccion D.4) confirma que MOD-023 tambien calcula esos plazos para sus mismos modulos propietarios.
- Los cuatro criterios legales conservadores por defecto que aplica este motor (aplicabilidad del Art. 82 LPA, sabado inhabil, 72 horas en horas corridas, y que la prevencion no suspende el plazo de 20 dias) dependen de PP-JUR-02, PP-JUR-03, PP-JUR-01 y PP-JUR-04 (04_secciones/24_preguntas_pendientes.md), las cuatro marcadas como bloqueantes del MVP. Las HU que aplican esos criterios (HU-023-02, HU-023-04, HU-023-06) exigen mostrar la advertencia de la seccion H y quedan marcadas requiere_validacion_legal.
- Se incluyen fechas reales de asuetos salvadorenos en los criterios de aceptacion, verificadas contra 01_legal/sweep_plazos_calendario_retencion.md (secciones 3.1, 3.2 y 3.5): los asuetos fijos del Art. 190 del Codigo de Trabajo, el 10 de mayo (D.L. 339/2016) y el 17 de junio (D.L. 208/2012), la Semana Santa de 2026 calculada por el algoritmo de Pascua (jueves 2 y viernes 3 de abril), y los asuetos ad hoc ya decretados por la Asamblea Legislativa el 16 de septiembre de 2022, el 26 de diciembre de 2022, el 2 de enero de 2023 y el 18 de junio de 2024.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-023-01 | Mantener y publicar el calendario anual de asuetos nacionales y ad hoc | Equipo del producto (proveedor) | 8 | R1 | 4 | - |
| HU-023-02 | Calcular una fecha limite en dias habiles | Responsable ARCO-POL / Responsable del tramite | 8 | R1 | 4 | HU-023-01 |
| HU-023-03 | Ver el desglose verificable de un calculo de plazo | Auditor (interno) | 3 | R1 | 4 | HU-023-02 |
| HU-023-04 | Calcular el vencimiento de las 72 horas en horas corridas | Responsable de Seguridad / IT | 5 | R1 | 3 | - |
| HU-023-05 | Calcular una fecha de vencimiento periodica de fecha a fecha | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R1 | 4 | HU-023-01 |
| HU-023-06 | Suspender y reanudar un calculo de plazo por causal declarada | Responsable ARCO-POL / Responsable del tramite | 5 | R1 | 4 | HU-023-02 |
| HU-023-07 | Aplicar una prorroga a un plazo abierto | Responsable ARCO-POL / Responsable del tramite | 3 | R1 | 4 | HU-023-02 |
| HU-023-08 | Recalcular y notificar un plazo abierto cuando se agrega un asueto ad hoc | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 8 | R1 | 4 | HU-023-01, HU-023-02, MOD-021, MOD-022 |
| HU-023-09 | Alertar cuando el calendario del proximo anio no esta cargado | Equipo del producto (proveedor) | 3 | R1 | 5 | HU-023-01 |
| HU-023-10 | Ver la vista de calendario central | Administrador de la organizacion | 5 | R1 | 5 | HU-023-02, HU-023-04, HU-023-05, HU-023-06, HU-023-07, MOD-001, MOD-021 |
| HU-023-11 | Generar el recordatorio de la auditoria anual mientras el modulo de Auditoria no este activo | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R1 | 5 | HU-023-05, MOD-004, MOD-021, MOD-022 |

## Historias

### HU-023-01. Mantener y publicar el calendario anual de asuetos nacionales y ad hoc

**Como** Equipo del producto (proveedor), **quiero** cargar, verificar la fuente y publicar cada anio la version del calendario de dias inhabiles con el calendario nacional base (capa 1) y los asuetos ad hoc que decrete la Asamblea Legislativa (capa 2), y que el sistema la active automaticamente el 1 de enero y la archive como historico al terminar el anio, **para** que exista siempre una unica fuente de dias inhabiles vigente y verificable, en vez de que cada modulo con plazo legal mantenga su propio calendario.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 4 | No |

- Fundamento: OBL-PLAZO-02 (Art. 190 Codigo de Trabajo, y D.L. 339/2016, D.L. 208/2012, Codigo de Trabajo y decretos legislativos de asueto)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el Equipo del producto inicia la carga del calendario de un anio nuevo, cuando registra cada fecha de la Capa 1 (calendario nacional) con su Alcance, su Fuente y su Fecha de verificacion, por ejemplo el 1 de enero, el 1 y el 10 de mayo, el 17 de junio, el 6 de agosto, el 15 de septiembre, el 2 de noviembre, el 25 de diciembre, y el jueves y el viernes de Semana Santa calculados por el algoritmo de Pascua para el 2 y el 3 de abril de 2026, entonces la version queda en estado Borrador.
2. Dado una version en Borrador con al menos una fecha sin Fuente documentada o sin Fecha de verificacion, cuando el Equipo del producto intenta pasarla a Publicado, entonces el sistema rechaza la transicion y senala cual fecha esta incompleta.
3. Dado una version en Borrador cuyas fechas de las capas 1 y 2 tienen todas Fuente y Fecha de verificacion, cuando el Equipo del producto confirma la version, entonces pasa a Publicado y queda disponible para revision, sin ser todavia la version aplicada por defecto a ningun calculo nuevo.
4. Dado una version Publicada cuyo Anio calendario llega al 1 de enero, cuando el sistema evalua la fecha, entonces la version pasa automaticamente a Vigente y se convierte en la aplicada por defecto para todo calculo nuevo de ese anio.
5. Dado una version Vigente, cuando el Equipo del producto confirma y publica un asueto ad hoc adicional con su fuente y su alcance por sector, por ejemplo un asueto con el mismo alcance de sector publico y privado que el confirmado por la Asamblea Legislativa el 18 de junio de 2024, entonces la version pasa a Actualizada con un numero de revision incrementado.
6. Dado una version Vigente o Actualizada cuyo Anio calendario termina, cuando inicia el 1 de enero del anio siguiente, entonces la version pasa automaticamente a Historico, deja de aplicarse a calculos nuevos y se conserva integra para auditar los calculos ya cerrados de ese anio.
7. Dado cualquier version de calendario en cualquier estado, cuando cualquier usuario intenta eliminarla, entonces el sistema no ofrece esa accion para ningun rol: una version solo se archiva como Historico.

**Reglas de negocio**

- Solo el Equipo del producto (proveedor) puede configurar el calendario nacional base y los asuetos ad hoc (seccion C); ningun rol de la organizacion cliente edita estas capas.
- Toda fecha exige Fuente documental mas archivo o enlace verificable y Fecha de verificacion, salvo la fecha movil de Semana Santa, calculada por el algoritmo de Pascua gregoriana (seccion D.1).
- Historico es estado terminal y no se reabre; una version nunca se elimina (anti-feature 19).

**Fuera de alcance**

- La capa 3 (asuetos locales por sede) y la capa 5 (calendario de la autoridad, ACE), fuera del alcance asignado a esta epica.
- La capa 4 (calendario propio de la empresa, horario habil y sabado habil), clasificada COULD HAVE en la tabla Q.
- La aplicacion automatica de un asueto anunciado por prensa antes de que el Equipo del producto confirme su fuente y alcance (decision de la seccion H, ver HU-023-08).

- Requiere contenido: Verificacion primaria de la fuente oficial de cada asueto nacional y ad hoc del anio (decreto legislativo, Diario Oficial o aviso del Ministerio de Trabajo) antes de publicar cada version anual.
- Preguntas pendientes relacionadas: PP-OPS-03
- Referencia: MOD-023 secciones D.1, F.1 y F.2
- Notas: El listado de fechas nacionales fijas y su base legal (Art. 190 Codigo de Trabajo, D.L. 339/2016, D.L. 208/2012) esta verificado en 01_legal/sweep_plazos_calendario_retencion.md, secciones 3.1 y 3.2.

### HU-023-02. Calcular una fecha limite en dias habiles

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** que el sistema calcule automaticamente la fecha limite de un plazo en dias habiles, aplicando el fin de semana, el calendario nacional y los asuetos ad hoc, y la regla de computo del Art. 82 LPA, **para** saber con certeza cuando vence un plazo legal, por ejemplo el plazo general de 20 dias habiles de una solicitud ARCO-POL, sin calcularlo a mano ni arriesgarme a un error de conteo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 4 | Si |

- Fundamento: OBL-PLAZO-01 (Art. 82 LPA, Ley de Procedimientos Administrativos)
- Depende de: HU-023-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que un modulo consumidor entrega un Evento de inicio, un Tipo de computo Dias habiles, una Duracion y una Capa de calendario aplicable, cuando MOD-023 recibe la solicitud, entonces calcula la fecha limite contando desde el dia siguiente al Evento de inicio y excluyendo sabados, domingos, los asuetos de la Capa 1 vigente y los asuetos ad hoc de la Capa 2 vigente.
2. Dado un plazo de 5 dias habiles con Evento de inicio el 12 de septiembre de un anio en que el 15 de septiembre cae entre semana, cuando MOD-023 calcula la fecha limite, entonces el 15 de septiembre no cuenta como dia habil y la fecha limite se corre en esa misma medida.
3. Dado un calculo cuyo ultimo dia contado cae en un dia inhabil, ya sea fin de semana o asueto, cuando MOD-023 determina la fecha limite, entonces la traslada al primer dia habil siguiente, conforme al Art. 82 LPA.
4. Dado que a la solicitud le falta el Evento de inicio, el Tipo de computo o la Duracion, cuando el modulo consumidor la envia, entonces MOD-023 no ejecuta el calculo y devuelve el campo faltante.
5. Dado un calculo con Capa de calendario aplicable igual a Empresa frente a la autoridad, cuando MOD-023 lo procesa en esta version del MVP, entonces aplica las mismas capas 0 a 2 que a un plazo frente al titular, nunca un resultado mas corto, mientras la diferenciacion fina de la capa 5 no este construida.
6. Dado cualquier calculo en dias habiles, cuando MOD-023 devuelve la fecha limite, entonces muestra junto a ella el texto: La aplicacion de esta regla de computo a su empresa se basa en la remision del Art. 62 de la Ley para la Proteccion de Datos Personales. Existe un argumento en contra, el Art. 2 de la Ley de Procedimientos Administrativos limita su ambito a la Administracion Publica. Requiere validacion de asesoria juridica.
7. Dado que la empresa no configuro el sabado como habil para sus propias metas internas, cuando MOD-023 calcula cualquier plazo frente al titular, entonces trata siempre el sabado como dia inhabil, sin excepcion configurable en esta version.

**Reglas de negocio**

- El computo inicia el dia siguiente al evento de inicio y los plazos por dias se cuentan solo en dias habiles (OBL-PLAZO-01, Art. 82 LPA).
- MOD-023 nunca decide que plazo aplica ni por que articulo: solo calcula la fecha con los datos que entrega el modulo de origen (seccion A).
- El snapshot de la version del calendario usada en el calculo se conserva de forma inmutable aunque el calendario cambie despues (seccion J).

**Fuera de alcance**

- La diferenciacion fina de la capa 5 (vacaciones colectivas de la Ley de Asuetos de los Empleados Publicos), clasificada SHOULD HAVE en la tabla Q.
- La configuracion de horario habil propio y de sabado habil para metas internas (capa 4), clasificada COULD HAVE.
- El desglose expandible completo del calculo, cubierto por HU-023-03.

- Requiere validacion legal: Si (PP-JUR-02, PP-JUR-03)
- Referencia: MOD-023 secciones D.2, G (automatizaciones 1 y 2) y H
- Notas: El criterio de dias habiles conservador (Art. 82 LPA supletorio, sabado inhabil) es el mismo que documentan las incertidumbres 1 y 3 de 01_legal/sweep_plazos_calendario_retencion.md, seccion 9.

### HU-023-03. Ver el desglose verificable de un calculo de plazo

**Como** Auditor (interno), **quiero** ver, junto a cada fecha limite calculada, el desglose completo con el dia 1 del computo, cada dia excluido con su motivo, la fecha resultante y la version del calendario usada, **para** poder verificar y demostrar, ante una fiscalizacion o mucho tiempo despues, exactamente como el sistema llego a esa fecha.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 4 | No |

- Fundamento: OBL-PLAZO-01 (Art. 82 LPA, Ley de Procedimientos Administrativos)
- Depende de: HU-023-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un calculo de plazo ya realizado, cuando un rol con permiso de ver desglose lo abre, entonces el sistema muestra primero la fecha limite en lenguaje simple, por ejemplo responder antes del [fecha], y como vista expandible aparte el desglose tecnico completo.
2. Dado que se abre el desglose expandible, cuando el sistema lo construye, entonces incluye el dia 1 del computo, cada dia u hora excluido con su motivo (fin de semana, asueto nacional, asueto ad hoc), la fecha resultante y el identificador de la version de HolidayCalendar usada.
3. Dado un calculo cuyo tipo de computo tiene una ambiguedad juridica documentada, cuando se muestra el desglose, entonces el criterio de computo mostrado aparece junto con su advertencia estandar de la seccion H.
4. Dado que el calendario cambia despues de realizado un calculo, cuando el Auditor consulta el desglose de ese calculo ya cerrado, entonces sigue mostrando la version del calendario vigente en el momento del calculo, no la version actual.
5. Dado el rol Titular (formulario externo), cuando intenta ver el desglose tecnico de su propia solicitud, entonces el sistema no se lo muestra: solo ve el numero de dias restantes a traves de MOD-012.

**Reglas de negocio**

- El fundamento legal y el desglose tecnico van siempre en segundo nivel, nunca en el texto principal de la pantalla (regla de oro de la plantilla).
- El snapshot de calendario usado en cada calculo es inmutable, aunque el calendario cambie despues (seccion J).

**Fuera de alcance**

- El calculo mismo de la fecha limite, cubierto por HU-023-02, HU-023-04 y HU-023-05.

- Referencia: MOD-023 secciones E, C y Q (desglose visible)

### HU-023-04. Calcular el vencimiento de las 72 horas en horas corridas

**Como** Responsable de Seguridad / IT, **quiero** que el sistema calcule el vencimiento de las 72 horas de un incidente en horas corridas por defecto y muestre siempre el criterio de computo aplicado, **para** saber con exactitud cuanto tiempo queda para notificar la vulneracion y para iniciar la revision exhaustiva, sin depender de un calculo manual bajo presion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 3 | Si |

- Fundamento: OBL-PLAZO-01 (Art. 82 LPA, Ley de Procedimientos Administrativos); OBL-INC-01 (Art. 25, Ley para la Proteccion de Datos Personales); OBL-INC-02 (Art. 25 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que MOD-013 entrega el momento en que se tuvo conocimiento de la vulneracion con Tipo de computo Horas corridas y Duracion 72, cuando MOD-023 recibe la solicitud, entonces calcula el vencimiento sumando 72 horas de reloj continuo, sin excluir fines de semana ni asuetos.
2. Dado que se solicitan en paralelo el cronometro de notificacion (OBL-INC-01) y el de inicio de la revision exhaustiva (OBL-INC-02) desde el mismo momento de conocimiento, cuando MOD-023 los calcula, entonces ambos vencimientos quedan disponibles de forma independiente, cada uno con su propio desglose.
3. Dado cualquier calculo de las 72 horas, cuando MOD-023 devuelve el vencimiento, entonces muestra junto a el el texto: La ley no precisa si este plazo se cuenta en horas corridas u horas habiles. El sistema aplica por defecto el criterio mas conservador, horas corridas. Verifique este criterio con asesoria legal si el caso es critico.
4. Dado un calculo de las 72 horas ya realizado, cuando se consulta despues, entonces el criterio de computo aplicado en ese momento, horas corridas, queda conservado de forma inmutable junto al calculo, aunque la configuracion de la empresa cambie con posterioridad.
5. Dado que a la solicitud le falta el momento de conocimiento de la vulneracion, cuando MOD-013 la envia, entonces MOD-023 no ejecuta el calculo y devuelve el campo faltante.

**Reglas de negocio**

- El criterio por defecto de las 72 horas es horas corridas, el mas conservador, y su cambio a horas habiles exige doble control (seccion D.3); esa capacidad de cambio queda fuera de esta epica (ver notas_epica).
- MOD-023 nunca decide si un vencimiento ya configura una infraccion sancionable: esa evaluacion es siempre del Delegado o de asesoria especializada (seccion H).

**Fuera de alcance**

- El cambio del criterio de horas corridas a horas habiles con doble control, clasificado SHOULD HAVE en la tabla Q.
- El esquema de alertas intermedias de las 72 horas, que define y ejecuta MOD-013, no MOD-023 (seccion I).

- Requiere validacion legal: Si (PP-JUR-01)
- Referencia: MOD-023 secciones D.2, D.3, G (automatizacion 1) y H

### HU-023-05. Calcular una fecha de vencimiento periodica de fecha a fecha

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que el sistema calcule una fecha de vencimiento contando meses o anios de fecha a fecha desde un evento de origen, por ejemplo mi reverificacion trienal, **para** no perder de vista una obligacion periodica que no se cuenta en dias habiles sino en el calendario comun.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 4 | Si |

- Fundamento: OBL-PLAZO-01 (Art. 82 LPA, Ley de Procedimientos Administrativos); OBL-DPO-04 (Art. 18, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-023-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que un modulo consumidor entrega un Evento de inicio con Tipo de computo Anios de fecha a fecha y una Duracion en anios, cuando MOD-023 recibe la solicitud, entonces calcula la fecha de vencimiento como esa misma fecha del calendario, el anio de origen mas la Duracion, conforme al Art. 82 LPA.
2. Dado un plazo de 3 anios con Evento de inicio el 15 de marzo de un anio, cuando MOD-023 calcula el vencimiento, entonces devuelve el 15 de marzo del anio de origen mas 3, sin contar dias habiles ni excluir asuetos en el trayecto.
3. Dado que la fecha resultante de un computo de meses o anios cae en un dia inhabil segun la version de calendario vigente, cuando MOD-023 determina la fecha final, entonces la traslada al primer dia habil siguiente, igual que para un computo en dias habiles.
4. Dado un Evento de inicio marcado como una fecha futura sin que el modulo de origen lo declare como una prorroga o suspension programada, cuando se envia la solicitud, entonces MOD-023 la rechaza.
5. Dado un calculo con Tipo de computo Meses de fecha a fecha, cuando MOD-023 lo procesa, entonces aplica la misma regla de fecha a fecha que para anios, ajustada a la unidad de meses.

**Reglas de negocio**

- Los plazos por meses o anios van de fecha a fecha, conforme al Art. 82 LPA (OBL-PLAZO-01).
- MOD-023 nunca calcula un plazo por su cuenta sin que un modulo de origen entregue el evento de inicio, la duracion y el tipo de computo (seccion A).

**Fuera de alcance**

- El calculo en dias u horas habiles, cubierto por HU-023-02 y HU-023-04.

- Referencia: MOD-023 secciones D.2, D.4 y G (automatizacion 1)
- Notas: Ejemplo tomado del catalogo consolidado de la ficha (seccion D.4): reverificacion trienal del perfil del Delegado, OBL-DPO-04, Art. 18 Lineamientos DPO.

### HU-023-06. Suspender y reanudar un calculo de plazo por causal declarada

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** que el modulo de origen pueda declarar una causal de suspension configurada sobre un plazo abierto y que el conteo se detenga hasta que la causal cese, **para** que el tiempo que el titular tarda en subsanar una prevencion, o cualquier otra causa prevista, no cuente en mi contra dentro del plazo legal.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 4 | Si |

- Fundamento: OBL-PLAZO-01 (Art. 82 LPA, Ley de Procedimientos Administrativos); OBL-ARCO-08 (Art. 18, Ley para la Proteccion de Datos Personales)
- Depende de: HU-023-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un calculo en estado Abierto cuyo campo Es plazo suspendible es Si, cuando el modulo de origen declara la causal de suspension configurada, por ejemplo la prevencion del Art. 18 mientras esa regla este activa, entonces el calculo pasa a Suspendido y se detiene el conteo del plazo.
2. Dado un calculo Suspendido, cuando el modulo de origen informa que la causal ceso, por ejemplo el titular subsano su solicitud, entonces el calculo vuelve a Abierto y el conteo se reanuda desde donde quedo, sin perder los dias u horas ya transcurridos antes de la suspension.
3. Dado que un modulo de origen intenta declarar una causal de suspension sobre un calculo cuyo campo Es plazo suspendible es No, cuando envia la solicitud, entonces MOD-023 la rechaza.
4. Dado un calculo Suspendido cuyo criterio de fondo, por ejemplo si la prevencion suspende o no el plazo general, sigue siendo una incertidumbre juridica no resuelta por la organizacion, cuando se muestra el calculo, entonces se ve tambien la fecha que resultaria sin la suspension, como referencia mas exigente.
5. Dado que un calculo pasa de Suspendido a Abierto, cuando MOD-023 registra el evento, entonces queda en el historial la duracion exacta de la suspension.

**Reglas de negocio**

- MOD-023 nunca suspende ni reanuda un plazo por iniciativa propia: solo ejecuta la suspension o la reanudacion cuando el modulo propietario se la solicita de forma explicita, con el fundamento que ese modulo declare (seccion A).
- La causal de suspension solo aplica si la organizacion la tiene habilitada en su configuracion (seccion D.3); en esta version del MVP ese valor permanece en su default conservador, No suspende (ver notas_epica).

**Fuera de alcance**

- El cambio del valor por defecto de la causal de suspension mediante doble control entre Delegado y Legal/Compliance, fuera de esta epica (ver notas_epica).

- Preguntas pendientes relacionadas: PP-JUR-04
- Referencia: MOD-023 secciones D.2, F.3, F.4 y G (automatizacion 6)

### HU-023-07. Aplicar una prorroga a un plazo abierto

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** que el modulo de origen pueda solicitar una prorroga sobre un plazo abierto antes de su vencimiento y que MOD-023 calcule la nueva fecha limite conservando la fecha original, **para** poder extender el plazo general de una solicitud, por ejemplo los 20 dias habiles adicionales del Art. 20 LPDP, cuando la motivacion ya quedo registrada en mi propio expediente.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 4 | Si |

- Fundamento: OBL-PLAZO-01 (Art. 82 LPA, Ley de Procedimientos Administrativos); OBL-ARCO-10 (Art. 20, Ley para la Proteccion de Datos Personales)
- Depende de: HU-023-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un calculo en estado Abierto, cuando el modulo de origen solicita una prorroga con una extension declarada antes de que se cumpla la fecha limite ordinaria, entonces MOD-023 calcula la nueva fecha limite sumando la extension y el calculo pasa a Prorrogado.
2. Dado un calculo que pasa a Prorrogado, cuando MOD-023 registra el evento, entonces conserva la fecha limite original en el historial, visible junto a la nueva.
3. Dado que el modulo de origen solicita la prorroga despues de que ya se cumplio la fecha limite ordinaria, cuando envia la solicitud, entonces MOD-023 la rechaza, porque la prorroga debe pedirse antes del vencimiento.
4. Dado un calculo Prorrogado, cuando se alcanza la nueva fecha limite sin que el modulo de origen marque el caso resuelto, entonces se activa la bandera Vencido, igual que en un calculo Abierto.
5. Dado una solicitud de prorroga con la extension declarada, cuando MOD-023 la procesa, entonces no evalua ni valida el fondo de la motivacion del modulo de origen: solo verifica que la solicitud llegue a tiempo.

**Reglas de negocio**

- La prorroga se pide dentro del plazo ordinario y con motivacion registrada en el expediente del modulo de origen, por analogia con el Art. 83 LPA; MOD-023 no valida el fondo de esa motivacion (seccion F.4).
- MOD-023 nunca decide por si mismo si procede una prorroga: solo la ejecuta cuando el modulo propietario se la solicita de forma explicita (seccion A).

**Fuera de alcance**

- La decision y la motivacion de fondo de la prorroga, que corresponden siempre al modulo propietario del plazo, por ejemplo MOD-011 para el Art. 20 LPDP.

- Referencia: MOD-023 secciones D.2, F.3 y F.4
- Notas: La tabla Q no incluye una fila propia para prorroga; se documenta como MUST HAVE inferido en notas_epica, porque OBL-ARCO-10 (MOD-011, MUST HAVE) la exige desde el primer dia.

### HU-023-08. Recalcular y notificar un plazo abierto cuando se agrega un asueto ad hoc

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que, cuando se confirma un asueto ad hoc dentro de la ventana de un plazo ya en curso, el sistema recalcule automaticamente la fecha limite, conserve la fecha anterior en el historial y me notifique el cambio, **para** nunca perder de vista que un plazo se movio, ni actuar con una fecha ya desactualizada.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 4 | No |

- Fundamento: OBL-PLAZO-02 (Art. 190 Codigo de Trabajo, y D.L. 339/2016, D.L. 208/2012, Codigo de Trabajo y decretos legislativos de asueto); OBL-PLAZO-01 (Art. 82 LPA, Ley de Procedimientos Administrativos)
- Depende de: HU-023-01, HU-023-02
- Modulos requeridos: MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que el Equipo del producto publica una nueva fecha en la Capa 2 de asueto ad hoc y esa fecha cae entre el evento de inicio y la fecha limite actual de un calculo en estado Abierto, Suspendido o Prorrogado, cuando MOD-023 detecta la coincidencia, entonces recalcula automaticamente la fecha limite de ese calculo.
2. Dado un calculo recalculado, cuando MOD-023 registra el evento, entonces conserva la fecha limite anterior en el historial junto con el motivo, por ejemplo un asueto ad hoc confirmado con el mismo alcance que el del 18 de junio de 2024 para el sector publico y privado, y notifica al modulo de origen y a MOD-022.
3. Dado que el recalculo deja menos de 1 dia habil para el vencimiento, cuando MOD-023 aplica el recalculo, entonces escala de inmediato la notificacion al Administrador de la organizacion, ademas del aviso normal al responsable del expediente.
4. Dado un asueto anunciado por un medio de prensa pero que el Equipo del producto todavia no confirmo con su fuente oficial y su alcance por sector, cuando el sistema evalua los calculos abiertos, entonces no aplica ningun recalculo y muestra el texto: Este posible asueto esta pendiente de confirmacion oficial y no se aplica todavia a ningun calculo.
5. Dado un calculo ya Cerrado, cuando se confirma despues un asueto ad hoc que hubiera caido dentro de su ventana original, entonces MOD-023 no lo recalcula: el recalculo automatico solo aplica a calculos Abiertos, Suspendidos o Prorrogados.
6. Dado cualquier recalculo aplicado, cuando un usuario consulta el calculo despues, entonces ninguna vista permite editar ni ocultar el valor anterior: el historial completo del recalculo queda siempre visible.

**Reglas de negocio**

- Ningun recalculo ocurre en silencio: siempre se notifica, se conserva el valor anterior y se deja registrado el motivo (secciones F y G, automatizacion 4).
- El recalculo automatico no es opcional para la organizacion; solo el canal de la notificacion puede variar (seccion G, automatizacion 4).

**Fuera de alcance**

- La confirmacion de la fuente oficial del asueto ad hoc en si, cubierta por HU-023-01.

- Referencia: MOD-023 secciones F.3, F.4, G (automatizacion 4) y H

### HU-023-09. Alertar cuando el calendario del proximo anio no esta cargado

**Como** Equipo del producto (proveedor), **quiero** recibir una alerta escalonada si al 1 de noviembre del anio en curso no existe una version Publicada del calendario del anio siguiente, **para** publicar el calendario a tiempo y que ningun cliente quede, el 1 de enero, sin un calendario valido para calcular sus plazos.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 5 | No |

- Fundamento: OBL-PLAZO-02 (Art. 190 Codigo de Trabajo, y D.L. 339/2016, D.L. 208/2012, Codigo de Trabajo y decretos legislativos de asueto)
- Depende de: HU-023-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que llega el 1 de noviembre del anio en curso, por ejemplo el 1 de noviembre de 2026, sin que exista una version Publicada del calendario del anio siguiente para las capas 1 y 2, cuando el sistema evalua la condicion, entonces dispara la alerta Calendario del proximo anio no cargado en nivel WARNING para el Equipo del producto.
2. Dado que la alerta sigue activa, cuando pasa una semana sin que se publique la version, entonces el sistema repite el aviso semanalmente.
3. Dado que la alerta lleva 15 dias sin resolverse, cuando el sistema evalua el tiempo transcurrido, entonces escala el nivel a CRITICAL para el Equipo del producto.
4. Dado que faltan 30 dias para el 1 de enero del anio que cubre la version y esta sigue en Borrador, cuando el sistema evalua la condicion, entonces dispara ademas la alerta Version del calendario aun en Borrador en nivel HIGH, diaria, con escalamiento inmediato a nivel CRITICAL interno del proveedor.
5. Dado que el Equipo del producto publica la version pendiente, cuando el sistema vuelve a evaluar la condicion, entonces ambas alertas se apagan.
6. Dado que la version del anio siguiente ya esta Publicada antes del 1 de noviembre, cuando llega esa fecha, entonces el sistema no dispara ninguna de las dos alertas.

**Reglas de negocio**

- El canal por defecto de estas alertas es la plataforma interna del proveedor, no un aviso al cliente (seccion I).
- El Administrador de la organizacion recibe copia informativa de la alerta, sin ser el destinatario principal (seccion E).

**Fuera de alcance**

- La alerta de sucursal sin fiesta patronal local documentada, fuera del alcance asignado porque la capa 3 esta excluida.

- Referencia: MOD-023 secciones G (automatizacion 5) e I
- Notas: El 1 de noviembre de 2026, fecha de referencia del primer criterio, es la proxima fecha real en que se evalua esta condicion para el calendario 2027.

### HU-023-10. Ver la vista de calendario central

**Como** Administrador de la organizacion, **quiero** ver en una sola pantalla todos los plazos legales, revisiones periodicas, vencimientos y tareas de mi organizacion, filtrables por modulo, responsable o sucursal, **para** no tener que entrar a cada modulo por separado para saber que fecha vence cuando.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 5 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-023-02, HU-023-04, HU-023-05, HU-023-06, HU-023-07
- Modulos requeridos: MOD-001, MOD-021

**Criterios de aceptacion**

1. Dado que el Administrador abre la vista de calendario central, cuando el sistema la construye, entonces muestra los plazos legales en curso, las revisiones periodicas programadas, las tareas asignadas y las fechas de recalculo, con el modulo de origen y el responsable de cada evento.
2. Dado que el Administrador aplica un filtro por modulo, por responsable o por sucursal, cuando el sistema actualiza la vista, entonces solo muestra los eventos que coinciden con el filtro elegido.
3. Dado un Responsable de area, cuando abre la vista de calendario central, entonces solo ve los eventos de su area o sucursal, sin poder ampliar el filtro al resto de la organizacion.
4. Dado el rol Usuario de consulta / Colaborador, cuando abre la vista, entonces solo ve las tareas puntuales que tiene asignadas, sin acceso a la configuracion del calendario.
5. Dado el rol Titular (formulario externo), cuando intenta acceder a la vista de calendario central, entonces el sistema se la niega: el Titular solo ve el numero de dias restantes de su propia solicitud a traves de MOD-012.
6. Dado un Auditor interno o externo, cuando abre la vista de calendario central, entonces la consulta en modo de solo lectura, sin poder editar ningun evento.

**Reglas de negocio**

- La vista de calendario central es la instrumentacion del area 30 del prompt de analisis funcional; no es una agenda de reuniones ni una herramienta de disponibilidad de personas (seccion A).
- Cada rol ve la vista con el alcance que le corresponde segun la seccion C de la ficha.

**Fuera de alcance**

- La sincronizacion con la aplicacion de calendario personal del usuario, clasificada FUTURE.
- La vista consolidada de calendario entre varias sociedades de un mismo grupo corporativo, clasificada FUTURE.

- Referencia: MOD-023 seccion Q; 04_secciones/12_tareas_y_alertas.md seccion 12.6

### HU-023-11. Generar el recordatorio de la auditoria anual mientras el modulo de Auditoria no este activo

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** recibir un recordatorio automatico para iniciar la auditoria anual de cumplimiento, anclado a la fecha de adecuacion inicial de mi primer diagnostico, **para** no perder de vista la obligacion de auditarse cada anio mientras el modulo estructurado de Auditoria de Cumplimiento todavia no este activo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 5 | No |

- Fundamento: OBL-AUD-01 (Art. 8 lit. b), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: HU-023-05
- Modulos requeridos: MOD-004, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que MOD-004 registra el cierre de la primera sesion de Diagnostico inicial de la organizacion, cuando ese cierre ocurre, entonces MOD-023 toma esa fecha como fecha de adecuacion inicial para el recordatorio anual de la auditoria.
2. Dado la fecha de adecuacion inicial ya registrada, cuando se cumplen 12 meses desde esa fecha sin que se haya generado un recordatorio previo, entonces MOD-023 genera el evento Corresponde iniciar la auditoria anual de cumplimiento, con una tarea en MOD-021 y una alerta INFO en MOD-022.
3. Dado que ya se genero un recordatorio anterior, cuando se cumplen 12 meses desde ese recordatorio, entonces MOD-023 genera el siguiente recordatorio anclado a esa fecha, no a la adecuacion inicial original.
4. Dado que la organizacion todavia no completo ninguna sesion de Diagnostico inicial, cuando el sistema evalua si corresponde generar el recordatorio, entonces no lo genera, porque no existe todavia una fecha de adecuacion inicial de la cual anclarlo.
5. Dado el recordatorio ya generado como tarea en MOD-021, cuando el Delegado o Responsable interno lo consulta, entonces ve que se trata de un recordatorio generico, sin el flujo estructurado de hallazgos y plan de accion que solo existira cuando MOD-018 este activo.

**Reglas de negocio**

- Esta HU cubre de forma parcial la obligacion OBL-AUD-01 mientras MOD-018, SHOULD HAVE, no se construya, sin sustituir su flujo estructurado de hallazgos y plan de accion (04_secciones/19_21_roadmap_mvp_v1_v2.md, seccion 19.4).
- El periodo del recordatorio es de 12 meses, el minimo que exige la Politica de Actuacion ACE, Art. 8 lit. b (seccion D.4 de la ficha).

**Fuera de alcance**

- El registro estructurado de hallazgos, severidad y plan de accion de una auditoria, que pertenece a MOD-018 y queda fuera de esta epica.
- El recalculo del recordatorio cuando MOD-018 exista y reemplace este mecanismo generico.

- Referencia: MOD-023 seccion D.4; 04_secciones/19_21_roadmap_mvp_v1_v2.md seccion 19.4; 04_secciones/08d_workflows_casos_09_11.md caso 10
- Notas: Cobertura parcial asignada del encargo: cubre MOD-018 (SHOULD HAVE) mientras no se construya, segun la seccion 19.4 del roadmap.

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Calculo de dias y horas habiles con las capas 0, 1 y 2 (fin de semana, calendario nacional, asuetos ad hoc) | HU-023-02, HU-023-04 |
| Regla de computo del Art. 82 LPA (inicio al dia siguiente, meses/anios de fecha a fecha, ultimo dia inhabil se traslada al siguiente habil) | HU-023-02, HU-023-05 |
| Calendario de asuetos nacionales del Codigo de Trabajo y de los decretos D.L. 339/2016 y D.L. 208/2012 | HU-023-01 |
| Desglose visible de cada calculo (dia 1, dias excluidos y motivo, fecha resultante) | HU-023-03 |
| Suspension y reanudacion de un calculo por causal declarada por el modulo de origen | HU-023-06 |
| Recalculo automatico, notificado y con historial, cuando cambia el calendario mientras un plazo sigue abierto | HU-023-08 |
| Alerta de calendario del proximo anio no cargado | HU-023-09 |
| Vista de calendario central (area 30) con filtros por modulo, responsable y sucursal | HU-023-10 |
