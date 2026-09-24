# EP-024 Centro Regulatorio (MOD-024)

**Objetivo.** La empresa consulta el marco normativo vigente con sus cuatro estados y su fuente, sabe si aplica el regimen actual o el de la reforma 659 y se entera cuando cambia, revisa el catalogo informativo de infracciones y multas, deja registro de cada tramite que pone en conocimiento de la ACE con su acuse, y puede documentar de forma basica un procedimiento sancionador si la ACE le abre un caso.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R1 | 21 | 79 | 52 | 27 | [MOD-024](../../03_modulos/MOD-024_ficha.md) |

**Notas de la epica.**

- Alcance MUST HAVE segun tabla Q de MOD-024_ficha.md: las 5 filas marcadas MUST (marco normativo consultable, bandera regimen_reforma_659, catalogo de infracciones y multas, registro basico de tramites ante la ACE, tarea automatica de revision) quedan cubiertas entre HU-024-01 y HU-024-15, con el detalle exacto en cobertura_q.
- Discrepancia entre la tabla Q y el encargo/roadmap, resuelta siguiendo el encargo: la fila de tabla Q 'Registro manual de un expediente de Procedimiento Sancionador (datos basicos, contestacion, resultado) con contadores de plazo' esta marcada SHOULD HAVE en la ficha (no MUST), pero la seccion 19.3 del roadmap describe la version minima de MOD-024 diciendo textualmente que 'el registro manual basico ya permite documentar un expediente real si se presenta', y el encargo de esta epica pide expresamente ese registro basico. Se sigue el encargo y el roadmap: HU-024-16 a HU-024-21 cubren un registro basico y lineal del expediente (creacion, contestacion, resolucion, pago, cierre, acceso restringido y exportacion), usando los nombres de estado reales de la ficha (EMPLAZADO, EN_CONTESTACION, EN_PRUEBA, EN_RESOLUCION, RESUELTO, FIRME, PAGADO, EN_COBRO_EJECUTIVO_FGR, CERRADO, PRESCRITO_ARCHIVADO) para la ruta simplificada por defecto (via_procedimiento = SIMPLIFICADA), sin modelar la via ORDINARIA, alegatos finales, recursos, medidas provisionales, decision de allanamiento, solicitud de inspeccion o peritaje, ni el registro repetible de requerimientos de informacion de la ACE fuera de un expediente abierto: esas piezas forman el 'flujo operativo completo' que la seccion 20.2 del roadmap ubica en V1, fuera de esta version del producto, y que el propio encargo pide dejar fuera.
- No se redacta ninguna historia para la recepcion automatica de tramites ACEFiling desde MOD-010 (Transferencias Internacionales), pese a que el encargo la menciona 'cuando exista': MOD-010 es SHOULD HAVE y, segun 19_21_roadmap_mvp_v1_v2.md seccion 20.1, se incorpora en V1, fuera de las release R1 y R2 de esta version del MVP; no existe ninguna otra epica de MOD-010 en esta ronda de backlog contra la cual esta epica pudiera declarar depende_de_modulos. HU-024-11 (creacion manual de un tramite) ya cubre el vacio mientras tanto, exactamente como describe la seccion L de MOD-024_ficha.md para el caso en que MOD-010 no este activo.
- Todas las historias quedan en release R1 porque MOD-024 es infraestructura transversal declarada en el nucleo vendible completo (19.8) y en la lista R1 de convenciones.md; ninguna historia depende de un modulo cuya propia epica sea R2, salvo el evento de entrada de MOD-002 (R1) y el consumo por MOD-021/MOD-022 (R1); no hay historias R2 en esta epica.
- El catalogo de infracciones y multas (HU-024-08 y HU-024-09) se modela con el mismo gobierno de contenido que el marco normativo (Editor de contenido regulatorio del proveedor) porque la seccion D de la ficha describe ambos como 'contenido del proveedor, no datos personales de la empresa cliente'; la ficha no detalla una tabla de campos propia para el catalogo como si lo hace para D.1, D.2, D.3 y D.4, asi que el alcance de HU-024-08 se acoto a lo que si describen las secciones E, G (regla 10) y K sobre ese catalogo.
- El numero exacto y la fecha de publicacion oficial del Decreto Legislativo 659 no estan confirmados a la fecha de este analisis (PP-JUR-13, PP-REG-01, PP-REG-02); HU-024-04 y HU-024-05 heredan esa incertidumbre y no se pueden dar por terminadas sin la confirmacion oficial, aunque el mecanismo tecnico de activacion y reversion si se puede construir y probar antes de esa confirmacion, tal como exige el criterio de salida a mercado 19.6 punto 5.
- Release ajustado de R1 a R2 en la planificacion: el registro basico del expediente sancionador solo se usa si la ACE abre un caso y no forma parte del nucleo vendible (seccion 19.8).

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-024-01 | Mantener el marco normativo con versionado | Editor de contenido regulatorio (proveedor) | 5 | R1 | 18 | - |
| HU-024-02 | Consultar el marco normativo vigente | Usuario de consulta / Colaborador | 3 | R1 | 18 | HU-024-01 |
| HU-024-03 | Exponer el estado del regimen normativo a otros modulos | Equipo del producto (proveedor) | 3 | R1 | 9 | - |
| HU-024-04 | Activar el regimen FUTURO de la reforma 659 | Editor de contenido regulatorio (proveedor) | 8 | R1 | 18 | HU-024-03, MOD-021, MOD-022 |
| HU-024-05 | Revertir el regimen a ACTUAL | Editor de contenido regulatorio (proveedor) | 5 | R1 | 18 | HU-024-04, MOD-021, MOD-022 |
| HU-024-06 | Notificar y confirmar el cambio de regimen normativo | Administrador de la organizacion | 3 | R1 | 18 | HU-024-04, HU-024-05, MOD-022 |
| HU-024-07 | Generar tarea de revision ante un cambio normativo | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R1 | 18 | HU-024-01, HU-024-04, MOD-021, MOD-022 |
| HU-024-08 | Mantener el catalogo de infracciones y multas | Editor de contenido regulatorio (proveedor) | 3 | R1 | 18 | - |
| HU-024-09 | Consultar el catalogo de infracciones y multas | Usuario de consulta / Colaborador | 2 | R1 | 18 | HU-024-08 |
| HU-024-10 | Recibir automaticamente el tramite de nombramiento del Delegado | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R1 | 19 | MOD-002 |
| HU-024-11 | Crear manualmente un tramite ante la ACE | Administrador de la organizacion | 2 | R1 | 19 | - |
| HU-024-12 | Completar un tramite ante la ACE para su envio | Responsable Legal / Compliance | 3 | R1 | 19 | HU-024-10, HU-024-11, MOD-021 |
| HU-024-13 | Aprobar y enviar un tramite ante la ACE | Aprobador | 3 | R1 | 19 | HU-024-12 |
| HU-024-14 | Registrar el acuse o rechazo de un tramite ante la ACE | Administrador de la organizacion | 3 | R1 | 19 | HU-024-13 |
| HU-024-15 | Consultar y exportar el registro de tramites ante la ACE | Responsable Legal / Compliance | 3 | R1 | 19 | HU-024-11, HU-024-13, MOD-022 |
| HU-024-16 | Registrar el expediente basico de un procedimiento sancionador | Administrador de la organizacion | 8 | R2 | 35 | MOD-023, MOD-021, MOD-022 |
| HU-024-17 | Contestar el emplazamiento de un procedimiento sancionador | Responsable Legal / Compliance | 5 | R2 | 35 | HU-024-16, MOD-023 |
| HU-024-18 | Registrar la resolucion final del procedimiento sancionador | Administrador de la organizacion | 5 | R2 | 35 | HU-024-17, MOD-023, MOD-021, MOD-022 |
| HU-024-19 | Registrar el pago de la multa impuesta | Administrador de la organizacion | 3 | R2 | 36 | HU-024-18, MOD-023, MOD-022 |
| HU-024-20 | Cerrar el expediente del procedimiento sancionador | Responsable Legal / Compliance | 3 | R2 | 36 | HU-024-19, MOD-023 |
| HU-024-21 | Consultar en solo lectura y exportar el expediente sancionador para auditoria | Auditor (interno) | 3 | R2 | 36 | HU-024-16, MOD-019 |

## Historias

### HU-024-01. Mantener el marco normativo con versionado

**Como** Editor de contenido regulatorio (proveedor), **quiero** dar de alta y editar cada instrumento normativo (ley, normativa ACE, lineamiento, politica de actuacion o buena practica) con su tipo, su estado, su fuente y su fecha de verificacion, y versionar cada regla operativa sin sobrescribir la version anterior, **para** que todas las organizaciones clientes consulten siempre el marco normativo vigente con su fundamento y su procedencia.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 18 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el Editor de contenido regulatorio da de alta un instrumento normativo, cuando completa nombre_instrumento, tipo_instrumento, clasificacion_exigibilidad, numero_y_fecha_emision, estado_instrumento, estado_verificacion y fuente_oficial, entonces el sistema guarda el instrumento y registra fecha_ultima_consulta.
2. Dado un instrumento sin fecha_publicacion_diario_oficial, cuando el Editor intenta guardar una fecha posterior al dia de hoy, entonces el sistema rechaza el valor y muestra que la fecha de publicacion no puede ser futura.
3. Dado un instrumento con estado_instrumento VIGENTE, cuando el Editor lo cambia a DEROGADO o MODIFICADO, entonces el sistema exige fuente_oficial y fecha_ultima_consulta actualizadas antes de guardar el cambio.
4. Dado que una regla operativa (RegulatoryRuleVersion) de un instrumento existente cambia, cuando el Editor publica la nueva version, entonces el sistema conserva la version anterior con su fecha_vigencia_hasta cerrada, sin sobrescribirla, y crea la version nueva con su fecha_vigencia_desde.
5. Dado que se publica una nueva version de una regla, cuando la operacion se completa, entonces el sistema registra en el historial del modulo quien publico la version, cuando, y que obligaciones_relacionadas cita.
6. Dado un usuario con un rol de la organizacion cliente, cuando intenta editar estado_instrumento o cualquier otro campo del marco normativo, entonces el sistema deniega la accion porque esa edicion es exclusiva del Editor de contenido regulatorio del proveedor.

**Reglas de negocio**

- El marco normativo y su versionado no son datos de la organizacion cliente; los mantiene exclusivamente el Editor de contenido regulatorio del proveedor, rol fuera del catalogo de roles de cliente (seccion B).
- estado_instrumento admite unicamente VIGENTE, FUTURO, DEROGADO o MODIFICADO.
- La version anterior de una regla siempre conserva su fecha_vigencia_hasta; nunca se sobrescribe (seccion D.1).
- Ningun rol de la organizacion cliente tiene permiso de edicion sobre este contenido (seccion C).

**Fuera de alcance**

- Redaccion juridica del contenido de cada instrumento (trabajo del equipo legal y de contenido, ver requiere_contenido)
- Vista de consulta para las organizaciones clientes (HU-024-02)

- Requiere contenido: Catalogo inicial de instrumentos normativos verificados (Decreto 144, Normativa PAS, Politicas de Actuacion ACE, Lineamientos DPO) con fuente oficial y estado de verificacion, redactado por el equipo legal y de contenido antes del lanzamiento
- Preguntas pendientes relacionadas: PP-OPS-04, PP-REG-03
- Referencia: MOD-024 secciones B, D.1 y O
- Notas: El rol Editor de contenido regulatorio no pertenece a los 12 roles estandar de la organizacion cliente (seccion B); ninguna de sus acciones se ejecuta dentro de una cuenta de cliente.

### HU-024-02. Consultar el marco normativo vigente

**Como** Usuario de consulta / Colaborador, **quiero** consultar el listado del marco normativo con filtros por tipo de instrumento y por estado, ver el detalle de cada uno con su fuente y su estado de verificacion, y exportarlo, **para** saber en cualquier momento que version de la ley debe seguir mi empresa sin rastrear el Diario Oficial por mi cuenta.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 18 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-024-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un usuario autenticado de la organizacion cliente distinto de Titular externo, cuando abre el marco normativo consultable, entonces ve el listado de instrumentos con su tipo_instrumento, estado_instrumento (VIGENTE, FUTURO, DEROGADO o MODIFICADO), fuente_oficial y fecha_ultima_consulta.
2. Dado el listado del marco normativo, cuando el usuario filtra por tipo_instrumento o por estado_instrumento, entonces el sistema muestra unicamente los instrumentos que cumplen el filtro elegido.
3. Dado un instrumento con estado_verificacion igual a OCR_PENDIENTE_DE_VERIFICAR, cuando el usuario abre su detalle, entonces el sistema muestra de forma visible que el texto proviene de un escaneo pendiente de verificar contra la fuente oficial.
4. Dado el marco normativo consultable, cuando el usuario solicita exportarlo, entonces el sistema genera el reporte en PDF o XLSX con los mismos datos visibles en pantalla.
5. Dado un Titular (formulario externo) que intenta acceder al marco normativo consultable, cuando lo intenta, entonces el sistema le deniega el acceso porque este modulo no es parte de su alcance.

**Reglas de negocio**

- El marco normativo es de solo lectura para toda la organizacion cliente (seccion D.1).
- Ningun texto de esta vista usa lenguaje de porcentaje de cumplimiento legal.

**Fuera de alcance**

- Edicion del contenido normativo (HU-024-01)

- Referencia: MOD-024 secciones C, D.1, E y N

### HU-024-03. Exponer el estado del regimen normativo a otros modulos

**Como** Equipo del producto (proveedor), **quiero** que el valor vigente de la bandera regimen_reforma_659 (ACTUAL o FUTURO) quede disponible para que cualquier otro modulo lo consulte por referencia, **para** que ningun otro modulo evalue por su cuenta si la reforma 659 esta vigente y nunca existan dos modulos mostrando estados normativos contradictorios el mismo dia.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 9 | Si |

- Fundamento: OBL-PLAZO-05 (Segun fuentes secundarias: deroga Arts. 15 y 17; reforma Arts. 16, 47 y 51, Decreto Legislativo N. 659)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que la organizacion aun no ha registrado ningun cambio de regimen, cuando cualquier modulo consulta regimen_reforma_659, entonces recibe el valor ACTUAL por defecto.
2. Dado que otro modulo (por ejemplo MOD-002, MOD-007, MOD-008, MOD-011, MOD-015 o MOD-017) consulta si el estado normativo vigente afecta a una obligacion propia, cuando existe una RegulatoryRuleVersion vigente para esa obligacion, entonces el sistema responde con el estado vigente por referencia, sin copiar el dato hacia el modulo consultante.
3. Dado que regimen_reforma_659 cambia de valor, cuando un modulo vuelve a consultarlo, entonces recibe siempre el valor mas reciente, sin necesidad de que ese modulo mantenga su propia copia.
4. Dado un modulo consultante, cuando pide el valor de regimen_reforma_659, entonces el sistema nunca expone un tercer valor distinto de ACTUAL o FUTURO, ni siquiera durante el paso interno de verificacion.

**Reglas de negocio**

- regimen_reforma_659 conserva unicamente los valores ACTUAL y FUTURO; el campo tecnico estado_interno_verificacion_659 es un paso interno del proveedor, nunca un tercer valor visible para otros modulos (seccion D.2).
- La consulta es siempre por referencia; ningun modulo consumidor duplica el valor como su propia copia de negocio (seccion G, regla 9).

**Fuera de alcance**

- Activacion o reversion del regimen (HU-024-04 y HU-024-05)

- Referencia: MOD-024 secciones D.2, G (regla 9) y L
- Notas: Historia habilitadora: MOD-002, MOD-007, MOD-008, MOD-011, MOD-015 y MOD-017 (todos MUST HAVE de R1 o R2) dependen de este mecanismo desde su propia primera version.

### HU-024-04. Activar el regimen FUTURO de la reforma 659

**Como** Editor de contenido regulatorio (proveedor), **quiero** cambiar regimen_reforma_659 de ACTUAL a FUTURO solo cuando se confirme la publicacion oficial, se cumpla la vacatio legis y se valide juridicamente el texto oficial, **para** que ninguna organizacion cliente deje de cumplir una obligacion que la ley todavia exige por activar un regimen legal que aun no esta vigente.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 18 | No |

- Fundamento: OBL-PLAZO-05 (Segun fuentes secundarias: deroga Arts. 15 y 17; reforma Arts. 16, 47 y 51, Decreto Legislativo N. 659)
- Depende de: HU-024-03
- Modulos requeridos: MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que regimen_reforma_659 esta en ACTUAL, cuando fecha_publicacion_diario_oficial_reforma esta vacia, entonces el sistema no permite activar FUTURO bajo ninguna condicion, ni siquiera si fecha_aprobacion_legislativa ya esta completa.
2. Dado que fecha_publicacion_diario_oficial_reforma ya esta completa, cuando aun no transcurrieron los 8 dias de fecha_cumplimiento_vacatio_legis, entonces el sistema no permite activar FUTURO.
3. Dado que fecha_publicacion_diario_oficial_reforma y fecha_cumplimiento_vacatio_legis ya se cumplieron, cuando validacion_juridica_texto_oficial no esta marcada en Si, entonces el sistema no permite activar FUTURO.
4. Dado que las tres condiciones (publicacion, vacatio legis y validacion juridica) estan completas, cuando el Editor de contenido regulatorio confirma la activacion, entonces regimen_reforma_659 pasa a FUTURO, se registra fecha_activacion_bandera, y se emite el evento de cambio de bandera hacia MOD-002, MOD-007, MOD-008, MOD-011, MOD-015 y MOD-017.
5. Dado que la bandera pasa a FUTURO, cuando la activacion se confirma, entonces el sistema actualiza el estado_instrumento de cada una de las 17 obligaciones afectadas por la reforma, preservando su clasificacion anterior en el historial en vez de sobrescribirla.
6. Dado que el sistema nunca activa FUTURO por si mismo, cuando solo transcurre el tiempo o solo se completa fecha_aprobacion_legislativa sin las otras tres condiciones, entonces el sistema mantiene ACTUAL y muestra el texto: Decreto Legislativo 659, segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado.

**Reglas de negocio**

- Nunca se activa FUTURO por la sola fecha de aprobacion legislativa, por el paso del tiempo o por una fecha calculada (anti-feature 14, seccion H decision 1).
- Ningun rol de la organizacion cliente puede activar este cambio; Responsable Legal / Compliance solo puede recomendarlo, de forma consultiva y no vinculante (seccion B y C).
- Las tres condiciones (publicacion, vacatio legis, validacion juridica) son acumulativas, no alternativas (seccion D.2 y F.1).

**Fuera de alcance**

- Notificacion a cada organizacion y confirmacion de toma de conocimiento (HU-024-06)
- Gobernanza interna de quien autoriza al Editor de contenido regulatorio a ejecutar la activacion (PP-OPS-01, fuera del alcance de esta ficha)

- Requiere validacion legal: Si (PP-REG-01, PP-REG-02, PP-JUR-13, PP-OPS-01)
- Referencia: MOD-024 secciones D.2, F.1 (fila EN_VERIFICACION a FUTURO), G (regla 1) y H (decision 1)
- Notas: El numero exacto del decreto (659 u otro) y su publicacion oficial no estan confirmados a la fecha de este analisis (PP-JUR-13, PP-REG-01, PP-REG-02); toda referencia se redacta como fuentes secundarias hasta la confirmacion.

### HU-024-05. Revertir el regimen a ACTUAL

**Como** Editor de contenido regulatorio (proveedor), **quiero** revertir regimen_reforma_659 de FUTURO a ACTUAL cuando el decreto no se publique, sea impugnado o su texto oficial difiera de lo reportado, dejando registrado el motivo, **para** que ninguna organizacion cliente quede operando bajo un regimen legal que ya no corresponde a la realidad juridica.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 18 | No |

- Fundamento: OBL-PLAZO-05 (Segun fuentes secundarias: deroga Arts. 15 y 17; reforma Arts. 16, 47 y 51, Decreto Legislativo N. 659)
- Depende de: HU-024-04
- Modulos requeridos: MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que regimen_reforma_659 esta en FUTURO, cuando el Editor de contenido regulatorio intenta revertirlo sin completar motivo_reversion, entonces el sistema rechaza la reversion y exige el motivo.
2. Dado que el Editor completa motivo_reversion con una de las opciones DECRETO_NO_PUBLICADO, DECRETO_IMPUGNADO, TEXTO_DIFIERE_DE_LO_REPORTADO u OTRO, cuando confirma la reversion, entonces regimen_reforma_659 pasa a ACTUAL y se emite el evento de reversion hacia los mismos seis modulos que recibieron el evento de activacion.
3. Dado que la reversion se ejecuta, cuando las tareas y registros que dependian de pasos exclusivos del regimen FUTURO existen, entonces el sistema las marca no aplica bajo el estado regulatorio actual, ver historial, sin eliminarlas.
4. Dado un expediente u otro registro ya cerrado mientras regimen_reforma_659 estaba en FUTURO, cuando ocurre la reversion, entonces ese registro conserva la regla que le aplicaba en el momento de su cierre, sin modificarse de forma retroactiva.
5. Dado que la reversion se confirma, cuando la operacion se completa, entonces el sistema registra en el historial la fecha, el motivo y el responsable de la reversion, de forma permanente.

**Reglas de negocio**

- La reversion es siempre una accion manual y explicita del Editor de contenido regulatorio del proveedor, nunca automatica (seccion F.1).
- El cambio de bandera nunca modifica retroactivamente un expediente, un registro de MOD-002 o un aviso de privacidad ya publicado (seccion F.1, Registros vinculados).

- Requiere validacion legal: Si (PP-JUR-13)
- Referencia: MOD-024 secciones D.2, F.1 (fila FUTURO a ACTUAL) y O

### HU-024-06. Notificar y confirmar el cambio de regimen normativo

**Como** Administrador de la organizacion, **quiero** ver el estado vigente del regimen de la reforma 659 con su advertencia mientras sea ACTUAL, recibir la notificacion cuando cambie, y confirmar que tome conocimiento, **para** saber en todo momento que obligaciones sigue vigentes mi empresa y dejar constancia de que me entere del cambio.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 18 | No |

- Fundamento: OBL-PLAZO-05 (Segun fuentes secundarias: deroga Arts. 15 y 17; reforma Arts. 16, 47 y 51, Decreto Legislativo N. 659); OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-024-04, HU-024-05
- Modulos requeridos: MOD-022

**Criterios de aceptacion**

1. Dado que regimen_reforma_659 esta en ACTUAL, cuando el Administrador de la organizacion consulta el estado regulatorio vigente, entonces ve el badge ACTUAL junto con el texto: Decreto Legislativo 659, segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado.
2. Dado que regimen_reforma_659 cambia de valor (activacion o reversion), cuando el cambio se confirma, entonces el sistema registra a la organizacion en organizaciones_notificadas y envia la notificacion por plataforma y correo, a traves de MOD-022, a Administrador, Delegado/Responsable interno, Responsable Legal y Responsable de area.
3. Dado una notificacion de cambio de regimen pendiente de confirmar, cuando el Administrador, el Delegado/Responsable interno, Responsable ARCO-POL, Responsable Legal, Responsable de Seguridad/IT, Responsable de area o Aprobador la abre y confirma, entonces el sistema registra la confirmacion de toma de conocimiento con fecha y usuario.
4. Dado un Auditor (interno) o un Auditor externo (invitado), cuando intenta confirmar toma de conocimiento de un cambio normativo, entonces el sistema deniega la accion porque ese permiso no esta disponible para su rol.
5. Dado que el cambio de regimen ya se notifico, cuando ningun usuario confirma la lectura dentro de los primeros dias, entonces la alerta permanece activa en la plataforma hasta que se confirme.

**Reglas de negocio**

- La notificacion interna siempre la envia MOD-022; este modulo solo genera el evento y registra a quien se notifico (seccion D.2, campo organizaciones_notificadas).
- Confirmar toma de conocimiento no equivale a aprobar ni a recomendar el cambio; es solo una constancia de lectura (seccion C).

**Fuera de alcance**

- Activacion y reversion del regimen (HU-024-04 y HU-024-05)

- Preguntas pendientes relacionadas: PP-UX-01
- Referencia: MOD-024 secciones B, C, D.2, I y O

### HU-024-07. Generar tarea de revision ante un cambio normativo

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que se cree automaticamente una tarea de revision cuando se publique una nueva version de una regla normativa o cuando cambie regimen_reforma_659, **para** no perder de vista ninguna actualizacion normativa que afecte a mi empresa.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 18 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-024-01, HU-024-04
- Modulos requeridos: MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que el Editor de contenido regulatorio publica una nueva RegulatoryRuleVersion sobre un instrumento existente, cuando la publicacion se completa, entonces el sistema crea en MOD-021 la tarea Revisar cambio normativo: [nombre del instrumento], dirigida a Administrador, Delegado/Responsable interno y Responsable Legal.
2. Dado que regimen_reforma_659 cambia de ACTUAL a FUTURO o se revierte, cuando el cambio se confirma, entonces el sistema crea en MOD-021, para cada organizacion, una unica tarea Revisar el impacto del cambio de regimen normativo, dirigida al Administrador de la organizacion.
3. Dado una tarea de revision de cambio normativo creada, cuando pasan 10 dias habiles sin que se complete, entonces el sistema escala la alerta a Aprobador.
4. Dado que un cambio normativo es puramente editorial (por ejemplo, corregir una fecha de consulta), cuando se publica, entonces el sistema no genera una tarea de revision ni una alerta WARNING, y el cambio queda solo en el historial de versiones.

**Reglas de negocio**

- Las tareas se crean siempre en MOD-021, nunca dentro de este modulo (regla de plataforma, seccion 4 de las instrucciones comunes).
- El plazo interno de revision no es un plazo legal; es configurable por el proveedor (seccion G, regla 2).

- Referencia: MOD-024 secciones E, G (reglas 1 y 2) e I

### HU-024-08. Mantener el catalogo de infracciones y multas

**Como** Editor de contenido regulatorio (proveedor), **quiero** mantener el catalogo de las infracciones leves, graves y muy graves del Art. 56 con su rango de multa del Art. 57 en salarios minimos, junto con la tabla de salarios minimos vigente por fecha, **para** que el catalogo informativo este siempre actualizado sin que ninguna organizacion cliente pueda alterarlo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 18 | No |

- Fundamento: OBL-SANC-01 (Art. 56, Ley para la Proteccion de Datos Personales)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado el catalogo de infracciones, cuando el Editor de contenido regulatorio lo mantiene, entonces cada infraccion queda clasificada como leve, grave o muy grave, con su rango de multa correspondiente en salarios minimos.
2. Dado que el salario minimo vigente cambia, cuando el Editor actualiza la tabla de salarios minimos, entonces el sistema conserva el valor anterior con su periodo de vigencia, sin sobrescribirlo, para poder mostrar ambos valores cuando corresponda.
3. Dado un usuario con un rol de la organizacion cliente, cuando intenta editar el catalogo de infracciones o la tabla de salarios minimos, entonces el sistema deniega la accion.
4. Dado el catalogo mantenido, cuando el Editor lo revisa, entonces el sistema no incluye ningun campo de calculo de probabilidad ni de monto exacto de una sancion para un caso concreto.

**Reglas de negocio**

- El catalogo es contenido del proveedor, identico para todas las organizaciones clientes (seccion D, introduccion).
- El catalogo nunca predice ni gradua una sancion para un caso concreto (anti-feature 5; seccion H, decision 3).

**Fuera de alcance**

- Consulta del catalogo por la organizacion cliente (HU-024-09)
- Graduacion o prediccion de una multa para un expediente concreto (seccion H)

- Requiere contenido: Catalogo verificado de las 26 infracciones del Art. 56 (9 leves, 7 graves, 10 muy graves) y de los rangos de multa del Art. 57, con la tabla de salarios minimos vigente, redactado por el equipo legal y de contenido
- Requiere validacion legal: Si (PP-JUR-10, PP-REG-04)
- Referencia: MOD-024 secciones D (introduccion), E, G (regla 10) y K

### HU-024-09. Consultar el catalogo de infracciones y multas

**Como** Usuario de consulta / Colaborador, **quiero** consultar el catalogo de infracciones leves, graves y muy graves con su rango de multa orientativo, filtrado por categoria, y exportarlo en PDF, **para** entender el marco sancionador aplicable sin que el sistema prediga ni determine una sancion para mi empresa.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 18 | No |

- Fundamento: OBL-SANC-01 (Art. 56, Ley para la Proteccion de Datos Personales)
- Depende de: HU-024-08
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un usuario autenticado de la organizacion cliente distinto de Titular externo, cuando abre el catalogo de infracciones y multas, entonces ve las infracciones agrupadas por categoria (leve, grave, muy grave) con su rango de multa en salarios minimos y su equivalente orientativo en dolares.
2. Dado el catalogo abierto, cuando el usuario filtra por categoria, entonces el sistema muestra unicamente las infracciones de esa categoria.
3. Dado el catalogo abierto, cuando el usuario lo consulta, entonces el sistema muestra junto al rango el texto: informacion orientativa, no una determinacion de la sancion; la graduacion es facultad exclusiva de la ACE, y remite a asesoria juridica.
4. Dado el catalogo abierto, cuando el usuario solicita exportarlo, entonces el sistema genera el catalogo descargable en PDF, sin variables propias de la organizacion.

**Reglas de negocio**

- El catalogo se presenta siempre como material de consulta general; la calificacion de un hecho propio como infraccion exige el texto Requiere validacion de la organizacion o asesoria especializada (seccion H, decision 2).

**Fuera de alcance**

- Mantenimiento del contenido del catalogo (HU-024-08)

- Preguntas pendientes relacionadas: PP-REG-04
- Referencia: MOD-024 secciones C, E, H (decisiones 2 y 3), K y N

### HU-024-10. Recibir automaticamente el tramite de nombramiento del Delegado

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que se genere automaticamente un registro de tramite ante la ACE cuando complete el paso de comunicar mi nombramiento en MOD-002, **para** no volver a capturar los mismos datos ni perder de vista ese tramite.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 19 | No |

- Fundamento: OBL-DPO-03 (Art. 10, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: -
- Modulos requeridos: MOD-002

**Criterios de aceptacion**

1. Dado que MOD-002 completa el paso Enviar comunicacion a la ACE de su propio workflow de nombramiento, cuando ese evento llega a este modulo, entonces el sistema crea automaticamente un registro ACEFiling en estado BORRADOR con tipo_tramite COMUNICACION_NOMBRAMIENTO_DELEGADO y modulo_origen MOD-002.
2. Dado el registro ACEFiling creado automaticamente, cuando se consulta contenido_del_tramite, entonces el sistema lo muestra precargado por referencia desde el registro de MOD-002, sin duplicar el dato en un campo propio.
3. Dado que el registro se crea, cuando la operacion se completa, entonces el sistema deja un evento de auditoria y el registro queda visible dentro de MOD-002 como estado de solo lectura.
4. Dado que MOD-002 no ha completado el paso Enviar comunicacion a la ACE, cuando se revisa este modulo, entonces no existe ningun registro ACEFiling de tipo COMUNICACION_NOMBRAMIENTO_DELEGADO para esa organizacion.

**Reglas de negocio**

- La generacion automatica no duplica datos: contenido_del_tramite es una referencia al registro que lo origino, nunca una copia (regla de direccion unica, seccion D.4).
- El registro nace siempre en BORRADOR (seccion F.2).

**Fuera de alcance**

- Completar el borrador para enviarlo (HU-024-12)

- Referencia: MOD-024 secciones D.4, F.2 (fila ninguno a BORRADOR) y L

### HU-024-11. Crear manualmente un tramite ante la ACE

**Como** Administrador de la organizacion, **quiero** crear manualmente un registro de tramite ante la ACE cuando no se origine de forma automatica desde otro modulo, **para** dejar constancia de tramites como una solicitud de certificacion o sello, o cualquier otro que mi empresa deba poner en conocimiento de la ACE.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 19 | No |

- Fundamento: OBL-AUD-02 (Art. 50 lit. j, k, l, Ley para la Proteccion de Datos Personales); OBL-TRANSF-05 (Art. 45, Ley para la Proteccion de Datos Personales)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que un tramite no se origina en MOD-002, cuando el Administrador de la organizacion lo crea manualmente, entonces el sistema exige seleccionar tipo_tramite entre COMUNICACION_NOMBRAMIENTO_DELEGADO, ACTUALIZACION_DATOS_DELEGADO, PUESTA_EN_CONOCIMIENTO_TRANSFERENCIA, SOLICITUD_OPINION_PREVIA_TRANSFERENCIA, SOLICITUD_CERTIFICACION_O_SELLO u OTRO, y guarda modulo_origen como Manual.
2. Dado un tramite con modulo_origen Manual, cuando se crea, entonces el sistema lo guarda en estado BORRADOR y registra fecha_generado de forma automatica.
3. Dado que se crea un tramite de tipo SOLICITUD_CERTIFICACION_O_SELLO, cuando el Administrador lo revisa, entonces el sistema muestra que la ACE aun no ha habilitado un mecanismo de certificacion, y que este registro solo deja constancia del intento, sin emitir ninguna certificacion oficial.
4. Dado que la organizacion aun no cuenta con MOD-010 activo, cuando necesita registrar la puesta en conocimiento de una transferencia internacional, entonces puede crear el tramite manualmente con tipo_tramite PUESTA_EN_CONOCIMIENTO_TRANSFERENCIA y modulo_origen Manual, en vez de recibirlo de forma automatica.
5. Dado un Usuario de consulta / Colaborador, cuando intenta crear un tramite ante la ACE, entonces el sistema deniega la accion porque su rol no tiene ese permiso.

**Reglas de negocio**

- Si el origen no es Manual, el registro de origen debe existir antes de crear el tramite (seccion D.4).
- Este modulo nunca emite la certificacion oficial de Delegado ni ningun sello de proteccion de datos; solo recuerda el tramite y enlaza al canal oficial cuando exista (anti-feature 12, seccion H decision 7).

**Fuera de alcance**

- Recepcion automatica de tramites desde MOD-010: mientras ese modulo no forme parte de esta version del producto, la unica via para registrar sus tramites es la creacion manual descrita en esta historia

- Preguntas pendientes relacionadas: PP-JUR-08, PP-REG-05
- Referencia: MOD-024 secciones C, D.4, F.2 (fila ninguno a BORRADOR), H (decision 7) y L
- Notas: La recepcion automatica desde MOD-010 no se modela como historia propia en esta version porque MOD-010 es SHOULD HAVE y queda fuera de esta version del producto (ver notas_epica); esta historia ya cubre el vacio mientras tanto, igual que describe la seccion L de la ficha.

### HU-024-12. Completar un tramite ante la ACE para su envio

**Como** Responsable Legal / Compliance, **quiero** completar el documento final y el canal de envio de un tramite en BORRADOR, **para** dejarlo listo para su aprobacion y envio.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 19 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-024-10, HU-024-11
- Modulos requeridos: MOD-021

**Criterios de aceptacion**

1. Dado un tramite ACEFiling en BORRADOR, cuando Responsable Legal, Delegado/Responsable interno o Administrador de la organizacion completan documento_adjunto y canal_de_envio, entonces el sistema pasa el tramite a PENDIENTE_DE_ENVIO.
2. Dado un tramite en BORRADOR, cuando se intenta pasarlo a PENDIENTE_DE_ENVIO sin documento_adjunto o sin canal_de_envio, entonces el sistema rechaza el cambio y exige ambos campos.
3. Dado que canal_de_envio se completa, cuando el usuario elige la opcion, entonces el sistema muestra las opciones correo institucional, formulario web de contacto de la ACE, plataforma de la ACE, o presencial, con la nota de que la ACE aun no habilita un canal oficial dedicado para varios de estos tramites.
4. Dado que el tramite pasa a PENDIENTE_DE_ENVIO, cuando la operacion se completa, entonces el sistema crea en MOD-021 la tarea Aprobar y enviar tramite ante la ACE.

**Reglas de negocio**

- Completar el borrador no equivale a aprobarlo ni enviarlo; esa es una accion separada por doble control (HU-024-13, seccion C).

**Fuera de alcance**

- Aprobacion y envio (HU-024-13)

- Referencia: MOD-024 secciones C, D.4, F.2 (fila BORRADOR a PENDIENTE_DE_ENVIO) y G (regla 5)

### HU-024-13. Aprobar y enviar un tramite ante la ACE

**Como** Aprobador, **quiero** aprobar y marcar como enviado un tramite en PENDIENTE_DE_ENVIO redactado por otra persona, **para** cumplir el doble control exigido antes de un acto con efecto ante la autoridad, dejando evidencia del intento de cumplimiento.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 19 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-024-12
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un tramite en PENDIENTE_DE_ENVIO, cuando el Aprobador o un segundo Responsable Legal distinto de quien completo el borrador lo aprueba, entonces el sistema lo pasa a ENVIADO y registra fecha_envio.
2. Dado un tramite en PENDIENTE_DE_ENVIO, cuando el mismo usuario que completo el borrador intenta aprobarlo, entonces el sistema rechaza la aprobacion por no cumplir el doble control, salvo que la organizacion este por debajo del umbral de 50 empleados, en cuyo caso permite que Administrador de la organizacion apruebe mostrando siempre la advertencia visible de autorrevision.
3. Dado un tramite marcado como ENVIADO, cuando cualquier usuario lo consulta, entonces el sistema muestra que este registro deja constancia del intento de cumplimiento, sin certificar que la ACE lo recibio, porque la ACE aun no habilita un canal oficial confirmado para varios de estos tramites.
4. Dado que el tramite pasa a ENVIADO, cuando la operacion se completa, entonces el sistema notifica al modulo de origen para actualizar su estado visible de solo lectura.

**Reglas de negocio**

- Aprobar el envio de cualquier tramite ante la ACE exige doble control: quien redacta no puede ser la unica firma (seccion C, separacion de funciones).
- El sistema nunca certifica que un tramite fue efectivamente recibido y aceptado por la ACE mientras no exista un canal oficial habilitado (anti-feature 13, seccion H decision 5).

**Fuera de alcance**

- Registro del acuse de recepcion (HU-024-14)

- Preguntas pendientes relacionadas: PP-JUR-08, PP-REG-05
- Referencia: MOD-024 secciones C, F.2 (fila PENDIENTE_DE_ENVIO a ENVIADO) y H (decision 5)

### HU-024-14. Registrar el acuse o rechazo de un tramite ante la ACE

**Como** Administrador de la organizacion, **quiero** registrar el acuse de recepcion cuando la ACE lo confirme, o marcar el tramite como rechazado o ya no aplicable, **para** mantener actualizado el estado real del tramite frente a la autoridad.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 19 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-024-13
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un tramite en ENVIADO, cuando el Administrador de la organizacion adjunta acuse_o_respuesta_ace, entonces el sistema pasa el tramite a CONFIRMADO y cierra la alerta de seguimiento.
2. Dado un tramite en ENVIADO, cuando la ACE rechaza el tramite o transcurre un plazo razonable sin canal oficial habilitado para confirmar la recepcion, entonces el Administrador lo marca RECHAZADO sin que eso bloquee al modulo de origen, que ya dejo constancia del intento.
3. Dado un tramite en BORRADOR, PENDIENTE_DE_ENVIO o ENVIADO, cuando el tramite deja de ser necesario por un evento automatico (por ejemplo una reversion de regimen_reforma_659), entonces el sistema lo marca NO_APLICA de forma automatica, con nota visible, sin eliminar el registro.
4. Dado un tramite en CONFIRMADO, RECHAZADO o NO_APLICA, cuando cualquier usuario intenta eliminarlo, entonces el sistema lo impide porque un registro ACEFiling nunca se borra.

**Reglas de negocio**

- CONFIRMADO y RECHAZADO son estados propios de este modulo (seccion D.4, nota sobre MOD-010).
- Ningun registro ACEFiling se elimina; solo cambia de estado (seccion O).

- Referencia: MOD-024 secciones D.4, F.2 (filas ENVIADO a CONFIRMADO/RECHAZADO/NO_APLICA) y O

### HU-024-15. Consultar y exportar el registro de tramites ante la ACE

**Como** Responsable Legal / Compliance, **quiero** consultar el listado de tramites ante la ACE con filtros por tipo y por modulo de origen, exportarlo, y recibir una alerta cuando un tramite quede pendiente de envio demasiado tiempo, **para** dar seguimiento a que ningun tramite quede olvidado sin evidencia de intento de cumplimiento.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 19 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-024-11, HU-024-13
- Modulos requeridos: MOD-022

**Criterios de aceptacion**

1. Dado el listado de tramites ante la ACE, cuando Responsable Legal, Delegado/Responsable interno o Administrador lo consultan, entonces ven cada registro con su tipo_tramite, modulo_origen, estado_tramite y fecha_generado, con filtros por tipo y por modulo de origen.
2. Dado el listado de tramites, cuando el usuario solicita exportarlo, entonces el sistema genera el reporte en XLSX o CSV con todos los campos visibles.
3. Dado un tramite en BORRADOR o PENDIENTE_DE_ENVIO por mas de 15 dias habiles desde su creacion, cuando se cumple ese umbral, entonces el sistema emite una alerta WARNING semanal a Administrador, Responsable Legal y Delegado/Responsable interno.
4. Dado un tramite en BORRADOR o PENDIENTE_DE_ENVIO por mas de 30 dias habiles, cuando se cumple ese umbral, entonces el sistema escala la alerta a Administrador de la organizacion.
5. Dado que el tramite se marca ENVIADO, cuando ocurre, entonces la alerta de tramite pendiente de envio se apaga.

**Reglas de negocio**

- El umbral de dias es configurable; la existencia de la alerta no lo es (seccion G, regla 5).

- Referencia: MOD-024 secciones E, G (regla 5), I y N

### HU-024-16. Registrar el expediente basico de un procedimiento sancionador

**Como** Administrador de la organizacion, **quiero** registrar el expediente basico de un procedimiento sancionador cuando mi empresa recibe un emplazamiento de la ACE, con la fecha de notificacion y la resolucion de inicio adjunta, **para** dejar constancia inmediata del caso y saber cuanto tiempo tengo para contestar.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 35 | No |

- Fundamento: OBL-SANC-05 (Art. 21, Normativa para el Procedimiento Administrativo Sancionador)
- Depende de: -
- Modulos requeridos: MOD-023, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que Administrador de la organizacion o Responsable Legal / Compliance inician el registro, cuando completan origen_del_caso, fecha_notificacion_recibida y adjuntan documento_resolucion_inicio, entonces el sistema crea el expediente en estado EMPLAZADO.
2. Dado que fecha_notificacion_recibida se completa, cuando el expediente se guarda, entonces el sistema pide a MOD-023 la fecha limite de contestacion (fecha de notificacion mas 1 dia mas 5 dias habiles) y la muestra en el expediente.
3. Dado que fecha_notificacion_recibida es una fecha futura, cuando el usuario intenta guardarla, entonces el sistema rechaza el valor porque esa fecha no puede ser futura.
4. Dado que el expediente se crea, cuando la operacion se completa, entonces el sistema crea en MOD-021 la tarea urgente Contestar emplazamiento de la ACE con prioridad maxima, y emite una alerta CRITICAL inmediata visible en el dashboard de Gerencia desde el primer dia.
5. Dado que se seleccionan infracciones_imputadas del catalogo del Art. 56, cuando el usuario las registra, entonces el sistema las guarda como referencia informativa de lo que la ACE atribuye, sin calificar por si mismo si esos hechos constituyen una infraccion.
6. Dado un Responsable de area, Usuario de consulta / Colaborador o Auditor, cuando intenta crear un expediente de procedimiento sancionador, entonces el sistema deniega la accion porque su rol no tiene ese permiso.

**Reglas de negocio**

- via_procedimiento se registra por defecto como SIMPLIFICADA (seccion D.3); esta historia no modela el cambio a ORDINARIA ni sus efectos (ver fuera_de_alcance).
- El plazo legal se calcula siempre en MOD-023, nunca dentro de este modulo (regla de plazos, instrucciones comunes seccion 4).
- El expediente nunca se elimina, solo cambia de estado o se archiva con motivo (seccion F, introduccion).

**Fuera de alcance**

- Cambio de via_procedimiento a ORDINARIA y sus efectos (alegatos finales, recursos): forma parte del flujo operativo completo, fuera de esta version del producto
- Registro de diligencia preliminar como estado propio con su plazo de 90 dias prorrogables
- Registro de medidas provisionales y de requerimientos de informacion de la ACE fuera de un expediente ya abierto

- Referencia: MOD-024 secciones C, D.3, F.3 (filas ninguno a EMPLAZADO), G (regla 3) e I
- Notas: Release ajustado de R1 a R2 en la planificacion: el registro basico del expediente sancionador solo se usa si la ACE abre un caso y no forma parte del nucleo vendible (seccion 19.8).

### HU-024-17. Contestar el emplazamiento de un procedimiento sancionador

**Como** Responsable Legal / Compliance, **quiero** redactar o adjuntar el escrito de contestacion dentro del plazo de 5 dias habiles, con aprobacion de un segundo firmante antes de enviarlo, **para** responder a tiempo al emplazamiento y dejar evidencia verificable de que mi empresa reacciono dentro del plazo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 35 | No |

- Fundamento: OBL-SANC-05 (Art. 21, Normativa para el Procedimiento Administrativo Sancionador)
- Depende de: HU-024-16
- Modulos requeridos: MOD-023

**Criterios de aceptacion**

1. Dado un expediente en EMPLAZADO, cuando Responsable Legal completa escrito_de_contestacion dentro del plazo calculado por MOD-023, entonces el sistema pasa el expediente a EN_CONTESTACION y luego a EN_PRUEBA una vez aprobado el envio.
2. Dado un escrito_de_contestacion completo, cuando un segundo Responsable Legal o el Aprobador distinto de quien lo redacto lo aprueba, entonces el sistema registra el envio con fecha cierta, salvo que la organizacion este por debajo del umbral de 50 empleados, en cuyo caso Administrador de la organizacion puede aprobar mostrando siempre la advertencia visible de autorrevision.
3. Dado que el mismo usuario que redacto el escrito intenta aprobarlo en una organizacion por encima del umbral de 50 empleados, cuando lo intenta, entonces el sistema rechaza la aprobacion por no cumplir la separacion de funciones.
4. Dado que vence el plazo de 5 dias habiles sin que se envie el escrito_de_contestacion, cuando el plazo se cumple, entonces el sistema deja constancia de que los hechos se tienen por contestados negativamente y el expediente continua igual hacia EN_PRUEBA, mientras la alerta de contestacion vencida se muestra en el dashboard de Gerencia.
5. Dado un expediente en EN_PRUEBA, cuando el usuario lo consulta antes de la resolucion, entonces el sistema muestra el conteo esperado de hasta 8 dias habiles para la remision del expediente por el delegado instructor de la ACE, como informacion, sin accion propia de la empresa.
6. Dado que Asesor externo invitado participa en el caso asignado, cuando colabora en la redaccion del escrito, entonces el sistema le permite comentar y aportar contenido, pero nunca aprobar el envio.

**Reglas de negocio**

- Quien redacta la contestacion no deberia ser el unico que aprueba y envia, salvo pyme por debajo de 50 empleados con advertencia visible de autorrevision (seccion C, separacion de funciones).
- Esta historia no modela alegatos finales ni via ORDINARIA (seccion D.3, fuera_de_alcance de HU-024-16).

**Fuera de alcance**

- Decision de allanamiento y de solicitud de inspeccion o peritaje
- Alegatos finales de la via ORDINARIA

- Requiere contenido: Modelo de escrito de contestacion de emplazamiento, validado por asesoria juridica antes de usarse
- Referencia: MOD-024 secciones C, D.3, F.3 (filas EMPLAZADO a EN_PRUEBA), I y K
- Notas: Release ajustado de R1 a R2 en la planificacion: el registro basico del expediente sancionador solo se usa si la ACE abre un caso y no forma parte del nucleo vendible (seccion 19.8).

### HU-024-18. Registrar la resolucion final del procedimiento sancionador

**Como** Administrador de la organizacion, **quiero** registrar el resultado de la resolucion final, incluido el monto de la multa si la hay, mostrando siempre el rango legal como informacion orientativa, **para** dejar constancia del resultado real que impuso la ACE y saber el plazo para pagar.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 35 | No |

- Fundamento: OBL-SANC-02 (Art. 57, Ley para la Proteccion de Datos Personales); OBL-SANC-03 (Art. 58, Ley para la Proteccion de Datos Personales)
- Depende de: HU-024-17
- Modulos requeridos: MOD-023, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado un expediente en EN_RESOLUCION, cuando Administrador de la organizacion o Responsable Legal completan resultado_resolucion_final con una de las opciones SIN_SANCION_ARCHIVADO, SANCION_LEVE, SANCION_GRAVE o SANCION_MUY_GRAVE, entonces el sistema pasa el expediente a RESUELTO.
2. Dado un resultado distinto de SIN_SANCION_ARCHIVADO, cuando se completa, entonces el sistema exige monto_multa_impuesta en salarios minimos y calcula su equivalente en dolares con el salario minimo vigente en la fecha de la resolucion, mostrando tambien el vigente en la fecha del hecho si ambos difieren.
3. Dado que se completa monto_multa_impuesta, cuando se guarda, entonces el sistema muestra ademas el rango orientativo completo de esa categoria de infraccion junto con el texto: informacion orientativa, no una determinacion de la sancion; la graduacion es facultad exclusiva de la ACE, sin calcular ni predecir el monto exacto por su cuenta.
4. Dado que existen medidas_adicionales_ordenadas, cuando se registran, entonces el sistema crea en MOD-021 una tarea por cada medida, dirigida al Responsable de area que corresponda.
5. Dado que el resultado tiene sancion, cuando se guarda, entonces el sistema pide a MOD-023 la fecha limite de pago (15 dias habiles) y emite una alerta HIGH visible en el dashboard de Gerencia.
6. Dado que resultado_resolucion_final es SIN_SANCION_ARCHIVADO, cuando se guarda, entonces el sistema no exige monto_multa_impuesta ni calcula plazo de pago.

**Reglas de negocio**

- El sistema nunca gradua la multa ni predice su monto exacto para un caso concreto; solo muestra el rango legal como informacion (seccion H, decision 3).
- El plazo de pago se calcula siempre en MOD-023 (seccion G, regla 6).

**Fuera de alcance**

- Interposicion de recursos contra la resolucion (via ORDINARIA)

- Preguntas pendientes relacionadas: PP-REG-04
- Referencia: MOD-024 secciones D.3, F.3 (fila EN_RESOLUCION a RESUELTO), G (regla 6, 10) y H (decision 3)
- Notas: Release ajustado de R1 a R2 en la planificacion: el registro basico del expediente sancionador solo se usa si la ACE abre un caso y no forma parte del nucleo vendible (seccion 19.8).

### HU-024-19. Registrar el pago de la multa impuesta

**Como** Administrador de la organizacion, **quiero** adjuntar el comprobante de pago de la multa dentro del plazo de 15 dias habiles, o dejar constancia informativa si el plazo vence sin pago, **para** cerrar la obligacion de pago con evidencia verificable o documentar el paso al cobro ejecutivo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 36 | No |

- Fundamento: OBL-SANC-06 (Art. 44, Normativa para el Procedimiento Administrativo Sancionador)
- Depende de: HU-024-18
- Modulos requeridos: MOD-023, MOD-022

**Criterios de aceptacion**

1. Dado un expediente en FIRME con multa, cuando Administrador de la organizacion adjunta comprobante_pago_multa dentro del plazo de 15 dias habiles calculado por MOD-023, entonces el sistema pasa el expediente a PAGADO y cierra la alerta de pago.
2. Dado que comprobante_pago_multa tiene una fecha posterior al plazo de 15 dias habiles, cuando se intenta guardar, entonces el sistema lo acepta como comprobante pero mantiene visible que el pago se realizo fuera del plazo.
3. Dado que vencen los 15 dias habiles sin comprobante_pago_multa, cuando el plazo se cumple, entonces el sistema pasa el expediente a EN_COBRO_EJECUTIVO_FGR de forma informativa y emite una alerta CRITICAL persistente, sin ejecutar ni simular ningun cobro por su cuenta.
4. Dado que faltan 3 dias habiles para el vencimiento del plazo de pago, cuando se cumple ese umbral, entonces el sistema emite una alerta WARNING a Administrador de la organizacion.

**Reglas de negocio**

- El sistema nunca ejecuta ni simula el cobro ejecutivo; solo documenta que el plazo establecido por la Normativa PAS vencio (seccion F.3, fila FIRME a EN_COBRO_EJECUTIVO_FGR).
- El plazo de pago se calcula siempre en MOD-023.

- Referencia: MOD-024 secciones D.3, F.3 (filas RESUELTO a FIRME a PAGADO/EN_COBRO_EJECUTIVO_FGR) e I
- Notas: Release ajustado de R1 a R2 en la planificacion: el registro basico del expediente sancionador solo se usa si la ACE abre un caso y no forma parte del nucleo vendible (seccion 19.8).

### HU-024-20. Cerrar el expediente del procedimiento sancionador

**Como** Responsable Legal / Compliance, **quiero** cerrar el expediente cuando se completen las medidas adicionales ordenadas, y que el sistema calcule la fecha limite de prescripcion, **para** dejar el caso disponible como historico completo sin perder ninguna evidencia.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 36 | No |

- Fundamento: OBL-SANC-07 (Art. 29 D.L. 143; Art. 47 Normativa PAS, Ley de Ciberseguridad y Seguridad de la Informacion)
- Depende de: HU-024-19
- Modulos requeridos: MOD-023

**Criterios de aceptacion**

1. Dado un expediente en PAGADO o en EN_COBRO_EJECUTIVO_FGR, cuando todas las tareas de MOD-021 ligadas a medidas_adicionales_ordenadas estan completadas, entonces Administrador de la organizacion o Responsable Legal pueden pasar el expediente a CERRADO.
2. Dado que el expediente pasa a CERRADO, cuando la operacion se completa, entonces el sistema pide a MOD-023 la fecha_limite_prescripcion a 5 anos desde la firmeza de la sancion o desde el ultimo hecho de la infraccion, segun corresponda.
3. Dado que transcurren los 5 anos de fecha_limite_prescripcion, cuando el plazo se cumple, entonces el sistema pasa el expediente a PRESCRITO_ARCHIVADO de forma automatica, y cierra el requisito de retencion minima de evidencia.
4. Dado un expediente en cualquier estado, cuando un usuario intenta eliminarlo, entonces el sistema lo impide porque el expediente permanece disponible como historico y nunca se elimina.
5. Dado que faltan 90 dias para cumplir los 5 anos de fecha_limite_prescripcion, cuando se cumple ese umbral, entonces el sistema emite una alerta INFO a Responsable Legal / Compliance y a Auditor (interno).

**Reglas de negocio**

- El expediente nunca se elimina; solo pasa a CERRADO y luego a PRESCRITO_ARCHIVADO (anti-feature 19, seccion O).
- El plazo de prescripcion se calcula siempre en MOD-023 (seccion G, regla 6).

- Referencia: MOD-024 secciones D.3, F.3 (filas PAGADO a CERRADO a PRESCRITO_ARCHIVADO), G (regla 6) e I
- Notas: Release ajustado de R1 a R2 en la planificacion: el registro basico del expediente sancionador solo se usa si la ACE abre un caso y no forma parte del nucleo vendible (seccion 19.8).

### HU-024-21. Consultar en solo lectura y exportar el expediente sancionador para auditoria

**Como** Auditor (interno), **quiero** consultar en solo lectura el expediente de un procedimiento sancionador cerrado y exportar su paquete de evidencia con verificacion de integridad, **para** alimentar el programa de auditoria de cumplimiento sin poder alterar ningun dato del expediente.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 36 | No |

- Fundamento: OBL-SANC-07 (Art. 29 D.L. 143; Art. 47 Normativa PAS, Ley de Ciberseguridad y Seguridad de la Informacion)
- Depende de: HU-024-16
- Modulos requeridos: MOD-019

**Criterios de aceptacion**

1. Dado un expediente de procedimiento sancionador, cuando Auditor (interno) lo consulta, entonces el sistema le muestra el expediente completo en solo lectura, sin permitirle comentar, aprobar ni adjuntar evidencia.
2. Dado el numero de expediente y los datos de la persona natural del presunto infractor, cuando Administrador, Responsable Legal, Aprobador o Auditor los consultan, entonces el sistema registra ese acceso en el historial, porque esa informacion es de acceso restringido a esos cuatro roles.
3. Dado un expediente, cuando Auditor (interno) o Auditor externo (invitado) solicitan exportar el paquete de evidencia, entonces el sistema genera el ZIP con manifiesto y un mecanismo propio de verificacion de integridad (hash o firma).
4. Dado un Auditor externo (invitado), cuando accede a un expediente para el que no fue invitado, entonces el sistema le deniega el acceso porque su alcance es acotado al caso o al periodo para el que se le invito.
5. Dado un Responsable de area o un Usuario de consulta / Colaborador, cuando intentan abrir un expediente de procedimiento sancionador, entonces el sistema les deniega el acceso porque su rol no lo tiene habilitado.

**Reglas de negocio**

- El rol Auditor es siempre de solo lectura, para preservar la independencia de su verificacion (seccion C, separacion de funciones).
- Toda exportacion hacia el paquete de evidencias incluye un mecanismo propio de verificacion de integridad (anti-feature 25, nota final de la ficha).

- Referencia: MOD-024 secciones C, E, J y O
- Notas: Release ajustado de R1 a R2 en la planificacion: el registro basico del expediente sancionador solo se usa si la ACE abre un caso y no forma parte del nucleo vendible (seccion 19.8).

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Marco normativo consultable (instrumentos con estado VIGENTE/FUTURO/DEROGADO/MODIFICADO, fuente y fecha de consulta) | HU-024-01, HU-024-02 |
| Bandera regimen_reforma_659 con interruptor manual, registro de fecha y notificacion a cada organizacion | HU-024-03, HU-024-04, HU-024-05, HU-024-06 |
| Catalogo de infracciones y multas (Art. 56 y 57), informativo | HU-024-08, HU-024-09 |
| Registro basico de tramites ante la ACE (ACEFiling), incluida la recepcion automatica de eventos desde MOD-002 y MOD-010 | HU-024-10, HU-024-11, HU-024-12, HU-024-13, HU-024-14, HU-024-15 |
| Tarea automatica de revision al publicarse una actualizacion normativa o al cambiar la bandera | HU-024-07 |
| Registro manual de un expediente de Procedimiento Sancionador (datos basicos, contestacion, resultado) con contadores de plazo. Alcance parcial incorporado al MVP por indicacion expresa del encargo y de la seccion 19.3 del roadmap: solo el registro basico y lineal, sin el flujo operativo completo (vias, medidas provisionales, recursos), que permanece SHOULD HAVE fuera de esta version | HU-024-16, HU-024-17, HU-024-18, HU-024-19, HU-024-20, HU-024-21 |
