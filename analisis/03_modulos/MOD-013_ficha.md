# MODULO: Incidentes de Seguridad

Codigo corto del modulo: MOD-013
Clasificacion global del modulo: MUST HAVE (para el MVP)
Obligaciones que cubre: OBL-INC-01, OBL-INC-02, OBL-INC-03, OBL-INC-04, OBL-INC-05 (propietarias); OBL-RET-05 (colaboradora, propietaria de MOD-016 Retencion y Eliminacion)

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (prohibido codigo, SQL, APIs, stack o infraestructura tecnica).

Fuentes base: `00_contexto_para_agentes.md`, `00_prompt_analisis_funcional.md`, `02_validacion/06_mapa_definitivo_de_modulos.md`, `02_validacion/mapa_modulos.json`, `02_validacion/02_validacion_de_la_idea.md` (seccion 2.7, decisiones 11 y 24; inconsistencia 13), `02_validacion/04_objetivo_exacto_del_producto.md`, `02_validacion/05_tipos_de_usuario.md`, `02_validacion/22_anti_features.md`, `01_legal/matriz_obligaciones.md` / `matriz_obligaciones.json`, `01_legal/03_hallazgos_regulatorios.md` (secciones 3, 5, 6, 8, 9), `01_legal/sweep_encargados_transferencias.md` (seccion 5.6, clausula de incidentes en el contrato con el encargado), y `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` (secciones 8.4 y 25, hipotesis de producto).

Nota de alcance: donde una afirmacion es decision u opinion de producto (no exigencia legal expresa), se marca explicitamente "[opinion de producto]". Donde una afirmacion es juridica, se cita el OBL-ID canonico (de `matriz_obligaciones.json`) y el articulo.

---

## A. Proposito

**Por que existe.** Una vulneracion de seguridad de datos personales es el evento de mayor riesgo legal, reputacional y operativo de todo el programa de proteccion de datos: la ley exige actuar en horas, no en dias, y una empresa sin abogado ni DPO dedicado no tiene forma de saber, sin ayuda, que debe hacer en las primeras 72 horas desde que se entera de lo ocurrido. Este modulo existe para que esa persona (tipicamente el Responsable de Seguridad / IT, ver perfil 4 de `05_tipos_de_usuario.md`) tenga un procedimiento guiado, con cronometro visible, checklist y plantillas, en lugar de enfrentar el Art. 25 de la ley sin apoyo.

**Que problema resuelve para la empresa.** Convierte un articulo de ley denso (Art. 25 LPDP, cuatro incisos con contenido distinto para cada destinatario) en un flujo paso a paso: que registrar, a quien notificar, que debe decir cada notificacion, cuando empieza a correr el plazo y que evidencia debe quedar. Evita el escenario mas comun de incumplimiento: que el incidente se resuelva tecnicamente (el sistema se restaura, el acceso se corrige) pero nadie documente ni notifique, porque nadie tenia claro que existia una obligacion legal separada de la respuesta tecnica.

**Que obligacion u obligaciones cubre.**
- OBL-INC-01 (Art. 25, primer inciso) - notificar a la ACE, a la Fiscalia General de la Republica (FGR) y a los titulares afectados en un plazo maximo de 72 horas desde que se tuvo conocimiento de la vulneracion. Clasificacion: OBLIGATORIO. Sin excepcion expresa identificada en la ley.
- OBL-INC-02 (Art. 25 inciso 2) - dentro del mismo plazo de 72 horas, iniciar (no necesariamente concluir) un proceso de revision exhaustiva para determinar la magnitud de la afectacion y las medidas correctivas y preventivas, incluida la actualizacion de las politicas de seguridad. Clasificacion: OBLIGATORIO.
- OBL-INC-03 (Art. 25 incisos 3 y 4) - contenido minimo diferenciado de la notificacion: a la ACE y a la FGR, cinco elementos (naturaleza del incidente, datos comprometidos, acciones correctivas inmediatas, recomendaciones al titular, medios de contacto); a los titulares afectados, solo cuatro (se omiten las acciones correctivas internas). Clasificacion: OBLIGATORIO.
- OBL-INC-04 (Art. 25 inciso final) - documentar toda vulneracion, en cualquier fase del tratamiento, que ocasione un riesgo en la seguridad de los datos personales, con fecha, motivo, hechos, efectos o implicaciones y medidas correctivas inmediatas y definitivas, a disposicion de la autoridad. Clasificacion: OBLIGATORIO.
- OBL-INC-05 (Ley de Ciberseguridad y Seguridad de la Informacion, Decreto Legislativo 143, Art. 6 lit. f-g en relacion con Art. 2 y Art. 8 lit. f-g) - reporte de incidentes de ciberseguridad a la ACE para entidades privadas calificadas formalmente por la ACE como operadores de infraestructura critica, sin plazo numerico fijo (exige actuar "de manera inmediata y eficaz" y "de forma oportuna, expedita y eficiente"). Clasificacion: CONDICIONAL, solo si la empresa tiene esa calificacion formal.
- OBL-RET-05 (colaboradora, propiedad de MOD-016; Art. 47 Normativa para el Procedimiento Administrativo Sancionador de la ACE, por analogia) - el expediente de cada incidente debe conservarse un minimo recomendado de 5 anos desde su cierre, como prueba de descargo ante una eventual investigacion de la ACE. Clasificacion: RECOMENDADO (no existe norma expresa; criterio de diseno que requiere validacion de abogado).

**Que valor aporta.**
- Operativo: convierte un plazo de horas en un cronometro visible con checklist, para que nadie descubra el incumplimiento despues de que ya vencio.
- Probatorio: el expediente documentado (OBL-INC-04) y la evidencia de envio de cada notificacion (OBL-INC-01, OBL-INC-03) son, junto con el Centro de Evidencias (MOD-019), la defensa de la empresa si la ACE abre una investigacion.
- Reduccion de riesgo: la infraccion de no notificar una vulneracion esta tipificada como leve (Art. 56 lit. a num. 3, multa de 1 a 10 salarios minimos, ver `03_hallazgos_regulatorios.md` seccion 6), pero el riesgo real mas alto no es la multa por si sola sino la exposicion adicional (denegar, ocultar o tratar datos sin base legal durante el manejo del incidente son infracciones muy graves, 26 a 40 salarios minimos) que se dispara cuando un incidente mal gestionado deriva en otras faltas.

**Que NO hace este modulo (limites explicitos).**
- No es un SIEM, un antivirus ni una herramienta de deteccion de amenazas en tiempo real; no detecta el incidente, solo lo gestiona desde que un humano lo registra (anti-feature 2 de `22_anti_features.md`).
- No decide por si mismo si un evento constituye una "vulneracion de seguridad de datos personales" bajo el Art. 25, ni si existe "riesgo" a efectos de OBL-INC-04; ambas son decisiones humanas (ver seccion H).
- No envia la notificacion a la ACE, a la FGR ni a los titulares de forma automatica: prepara el borrador y exige aprobacion explicita antes de marcarlo como enviado.
- No presenta el reporte de infraestructura critica del Decreto 143 en nombre de la empresa sin su calificacion formal por la ACE, ni asume que la empresa tiene esa calificacion; el campo correspondiente (ver seccion D) queda vacio hasta que la organizacion confirme una resolucion de la ACE.
- No resuelve por si mismo la incertidumbre juridica sobre si las 72 horas se cuentan en horas corridas o en horas habiles (ver seccion 9 de `03_hallazgos_regulatorios.md`); aplica un criterio conservador por defecto (horas corridas) y lo muestra siempre de forma visible, nunca como un hecho legal cerrado (decision 2.7.11 de `02_validacion_de_la_idea.md`).

---

## B. Usuarios

Roles estandar segun `05_tipos_de_usuario.md`, seccion 5.3 (12 roles del sistema). Para MOD-013:

| Rol | Para que lo usa en este modulo |
|---|---|
| Responsable de Seguridad / IT | Usuario principal y operativo del modulo. Registra el incidente, ejecuta triage, investigacion y contencion, adjunta evidencia tecnica, propone medidas correctivas y vigila los dos cronometros de 72 horas (perfil 4 de `05_tipos_de_usuario.md`, "Roberto Antonio Villalta"). |
| Delegado de Proteccion de Datos (o Responsable interno, segun el estado de la reforma 659) | Aprueba el contenido y el envio de las notificaciones a la ACE, a la FGR y a los titulares antes de que salgan del sistema; es el enlace institucional con la Direccion de Proteccion de Datos de la ACE (Art. 29 Lineamientos DPO, aplicable mientras la figura sea obligatoria). Revisa si el incidente activa una EIPD (hacia MOD-014). |
| Responsable Legal / Compliance | Revisa el contenido de las notificaciones desde el angulo de riesgo legal, valida (junto con el Delegado) si corresponde documentacion reforzada por existir "riesgo" (OBL-INC-04), y participa en la decision de cierre en casos sensibles. |
| Administrador de la organizacion | Ve el estado de todos los incidentes de la organizacion en el dashboard (perspectiva Gerencia), recibe las alertas criticas de plazo, y configura parametros del modulo (por ejemplo, el criterio de computo de las 72 horas o la bandera de "operador de infraestructura critica" a nivel de organizacion, en MOD-001). No gestiona el caso dia a dia salvo en una pyme donde acumula roles. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Reporta un incidente que se origino o se detecto en su area (por ejemplo, un equipo con datos de curriculums extraviado), y ejecuta las tareas puntuales que se le asignan (por ejemplo, avisar a un proveedor o recolectar informacion de los titulares afectados). No tiene acceso al expediente completo salvo que se le asigne. |
| Aprobador | En organizaciones que superan el umbral configurable de separacion de funciones (propuesta inicial 50 empleados, `05_tipos_de_usuario.md` 5.4), aprueba formalmente el cierre del incidente cuando quien lo cerraria es la misma persona que lo investigo, dejando una segunda firma registrada. |
| Auditor (interno) | Solo lectura sobre expedientes cerrados y en curso, y sobre la evidencia de notificaciones enviadas, para la auditoria anual de cumplimiento (OBL-AUD-01, Politicas ACE Art. 8 lit. b). No crea ni aprueba nada. |
| Auditor externo (invitado) | Acceso temporal de solo lectura, por invitacion, al paquete de evidencias de incidentes de un periodo especifico, durante una auditoria externa puntual. |
| Usuario de consulta / Colaborador | Ejecuta unicamente la tarea puntual que se le asigna desde el incidente (por ejemplo, "verificar si el servidor X fue accedido"), sin ver el expediente completo. |
| Asesor externo invitado | Acceso acotado en tiempo a un incidente especifico cuando la empresa contrata a un abogado o a un consultor de seguridad externo para dictaminar sobre ese caso; deja su opinion registrada como evidencia (perfil 9 de `05_tipos_de_usuario.md`). |
| Titular (formulario externo) | No aplica como usuario de este modulo. El titular no accede a Incidentes: solo recibe la notificacion externa (OBL-INC-03) por el canal que corresponda. Si el titular quiere ejercer un derecho ARCO-POL a raiz del incidente (por ejemplo, pedir informacion adicional), lo hace por MOD-011, no por aqui. |

---

## C. Permisos

Acciones = ver, crear, modificar, aprobar (notificacion), cerrar, eliminar/archivar, exportar, asignar, comentar, adjuntar evidencia. La columna Titular no aparece: no tiene acceso a este modulo (ver seccion B).

| Accion | Resp. Seguridad/IT | Delegado / Resp. interno | Legal/Compliance | Administrador | Resp. de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|
| Ver (expediente propio o asignado) | Si | Si | Si | Si (todos) | Solo si reporto o le asignaron tarea | Solo si le corresponde aprobar | Solo lectura, todos | Solo lectura, invitado a un periodo | Solo la tarea asignada | Solo el caso invitado |
| Crear (reportar incidente) | Si | Si | Si | Si | Si | No | No | No | No | No |
| Modificar (datos del expediente) | Si | Si (campos de decision/notificacion) | Si (campos de evaluacion legal) | No directamente | No | No | No | No | No | No |
| Aprobar notificacion (ACE/FGR/titulares) | No (prepara el borrador) | Si | Puede co-revisar segun politica interna | No | No | No | No | No | No | No |
| Cerrar caso | Si (si esta bajo el umbral de separacion de funciones) | Si | Si | No directamente | No | Si (por encima del umbral, como segunda firma) | No | No | No | No |
| Eliminar/archivar | No (nunca se elimina; solo se archiva tras conservacion vencida, automatizado desde MOD-016) | No | No | No | No | No | No | No | No | No |
| Exportar (paquete de evidencia) | Si | Si | Si | Si | No | No | Si | Si (solo lo compartido con el) | No | Si (solo su caso) |
| Asignar tareas dentro del incidente | Si | Si | Si | Si | No | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | Si (si tiene acceso) | Si | No (serian observaciones de auditoria, via reporte, no comentario en el caso) | No | Si (en su tarea) | Si (en su caso) |
| Adjuntar evidencia | Si | Si | Si | No directamente | Si (si tiene acceso) | No | No | No | Si (en su tarea) | Si (en su caso) |

**Separacion de funciones.**
- Ninguna norma de la LPDP exige que dos personas distintas gestionen y cierren un incidente; pero toda decision de cierre debe dejar registrada la evidencia de quien decidio, cuando y con que fundamento (OBL-INC-04, Art. 25 inciso final; principio de responsabilidad demostrada OBL-PRIN-03, Art. 5 lit. i), aunque haya sido la misma persona de principio a fin. [fundamento legal parcial, ver `05_tipos_de_usuario.md` 5.4]
- La aprobacion de la notificacion externa (a la ACE, a la FGR o a los titulares) exige siempre una accion explicita del Delegado / Responsable interno, distinta de quien redacto el borrador; el sistema nunca envia una notificacion externa sin esa aprobacion, en linea con la decision de que todo acto atribuido a esa figura queda calculado y redactado por el sistema pero pendiente de aprobacion humana antes de emitirse (decision 22, `02_validacion_de_la_idea.md`). [opinion de producto sobre el mecanismo; el fundamento de que la decision de notificar exige criterio humano es legal, ver seccion H]
- Por encima del umbral configurable de separacion de funciones (propuesta inicial 50 empleados), el cierre de un incidente que investigo y gestiono una sola persona requiere una segunda firma del rol Aprobador. Por debajo del umbral, el sistema lo permite pero muestra una advertencia visible de "autorrevision". [opinion de producto, umbral sin respaldo legal, `05_tipos_de_usuario.md` 5.4]
- El rol Auditor (interno o externo) es siempre de solo lectura sobre este modulo: nunca coincide con quien investigo, aprobo o cerro el mismo caso que audita. [opinion de producto]

---

## D. Informacion de entrada

Convencion de la columna Fundamento: se cita el OBL-ID cuando el campo existe porque la ley lo exige (directa o indirectamente, como contenido minimo de la notificacion o del expediente); se marca "buena practica" cuando el campo no tiene respaldo legal expreso pero ayuda a gestionar el caso; se marca "[opinion de producto]" cuando ademas es una decision de diseno discutible.

Minimizacion de datos personales (privacy by design): este modulo es una excepcion declarada al principio general de minimizacion de MOD-006/MOD-009 (decision 2.7.21, inconsistencia 23 de `02_validacion_de_la_idea.md`), porque por su naturaleza debe describir que datos personales de que titulares resultaron afectados. Aun asi, el sistema NO almacena una copia de la base de datos comprometida ni el dato personal en si (nombre completo, numero de tarjeta, expediente clinico, etc.): registra categorias, cantidades estimadas y, cuando es indispensable para el caso, un adjunto puntual con controles reforzados (cifrado, acceso restringido al equipo del incidente), nunca la extraccion masiva de la base afectada (anti-feature 9 de `22_anti_features.md`).

### D.1 Identificacion y deteccion

| Campo | Tipo | Obligatorio/opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Titulo del incidente | Texto | Obligatorio desde el registro | - | Minimo 5 caracteres | "Un nombre corto para identificar el caso, por ejemplo: Acceso no autorizado al servidor de RRHH." | Buena practica |
| Fecha y hora de deteccion | Fecha y hora | Obligatorio desde el registro | - | No puede ser futura | "El momento en que alguien de la empresa noto por primera vez que algo raro pasaba (una alerta, un reclamo, un hallazgo tecnico). Puede ser distinto del momento en que se confirmo que era una vulneracion de datos." | Buena practica (base para calcular la fecha de conocimiento) |
| Fecha y hora de conocimiento (dispara ambos cronometros de 72 horas) | Fecha y hora | Obligatorio antes de pasar a Triage | - | No puede ser futura; si es posterior a la fecha de deteccion, exige un campo de justificacion obligatorio (ver seccion R.3 para la definicion operativa) | "El momento exacto en que la persona responsable en su empresa confirmo, con certeza razonable, que ocurrio una vulneracion de datos personales. Desde aqui empiezan a correr las 72 horas. Si tiene dudas de cual es ese momento, use el mas temprano posible: es el criterio mas seguro." | OBL-INC-01, OBL-INC-02 (Art. 25, "desde que se tuvo conocimiento") |
| Quien reporta | Referencia a Usuario | Obligatorio, autocompletado | Usuarios de la organizacion | - | "La persona que esta registrando el caso ahora mismo." | Buena practica |
| Origen del incidente | Seleccion unica | Obligatorio desde Triage | Interno (empleado, sistema propio); Proveedor/Encargado; Terceros/Receptor; Desconocido/en investigacion | - | "De donde vino el problema: de un sistema o persona de su empresa, de un proveedor que trata datos por usted, o aun no lo sabe." | Buena practica; si es Proveedor/Encargado, enlaza con MOD-009 (ver seccion L) |
| Proveedor/Encargado relacionado | Referencia a entidad Vendor (MOD-009) | Obligatorio si origen = Proveedor/Encargado | Catalogo de proveedores de MOD-009 | Debe existir en MOD-009; si no existe, exige darlo de alta primero | "Si el incidente ocurrio en un proveedor que trata datos por usted (por ejemplo, su proveedor de nube), selecciónelo aqui." | Buena practica; contenido minimo recomendado del DPA/contrato (`sweep_encargados_transferencias.md` seccion 5.6) |
| Sistema o proceso afectado | Referencia a Sistema (catalogo unico de MOD-006) o texto libre si aun no esta en el catalogo | Obligatorio desde Triage | Catalogo de sistemas de MOD-006 | - | "Que sistema, archivo o proceso se vio afectado (por ejemplo: nomina en la nube, expedientes fisicos de RRHH)." | Buena practica; conecta con el RAT (MOD-006) |
| Tratamiento(s) relacionado(s) del RAT | Referencia multiple a Treatment (MOD-006) | Recomendado desde Investigacion | RAT de MOD-006 | - | "A que actividad de tratamiento de su Registro de Actividades de Tratamiento pertenecen los datos afectados." | Buena practica; permite saber si el tratamiento ya tenia base legal, EIPD o categoria sensible marcada |

### D.2 Clasificacion y alcance (Triage / Investigacion)

| Campo | Tipo | Obligatorio/opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Es una vulneracion de datos personales bajo el Art. 25 | Booleano con justificacion | Obligatorio antes de salir de Triage | Si / No, aun no se sabe (mantener en Triage) | Si se marca "No", exige un campo de justificacion obligatorio y visible en el historial | "¿Este evento afecto datos personales de personas identificadas o identificables? Si no esta seguro, mantengalo en investigacion; no lo descarte todavia." | Decision que NO se automatiza, ver seccion H |
| Tipo de vulneracion | Seleccion multiple | Obligatorio desde Investigacion | Dano; Perdida; Alteracion; Destruccion; Acceso ilegitimo; Uso ilicito o no autorizado (incluye accidental) | Al menos una opcion | "Que tipo de afectacion sufrieron los datos. La ley cubre cualquiera de estas, incluso si fue accidental." | OBL-INC-01 (Art. 25, definicion de vulneracion) |
| Causa raiz (preliminar / confirmada) | Seleccion unica + texto libre | Preliminar opcional en Triage; obligatorio en Investigacion | Error humano; Falla tecnica; Ataque externo (ejemplo: ransomware, phishing); Perdida/robo de dispositivo o documento fisico; Falla de un proveedor; Otro | - | "Que causo la vulneracion, hasta donde se sepa. Puede actualizarlo conforme avanza la investigacion." | OBL-INC-02, OBL-INC-04 |
| Categorias de datos afectadas | Seleccion multiple (catalogo compartido con MOD-006) | Obligatorio desde Investigacion | Identificacion basica; Contacto; Laboral; Financiera; Ubicacion; Biometrica; Salud; Afiliacion sindical/religiosa/politica; Datos de NNA; Otra | Al menos una opcion | "Que tipos de datos personales estuvieron expuestos." | OBL-INC-03 (contenido de la notificacion), OBL-SENS-01 a 08 (union del catalogo de datos sensibles, ver `03_hallazgos_regulatorios.md` seccion 8.6) |
| Incluye datos sensibles | Booleano, calculado a partir de categorias de datos, editable con justificacion | Automatico, editable | Si/No | - | "El sistema marca esto automaticamente segun las categorias que eligio arriba; puede corregirlo si es necesario, explicando por que." | OBL-SENS-01 a 08 |
| Cantidad estimada de titulares afectados | Numero (rango si no hay certeza) | Obligatorio antes de Evaluacion | Rango libre o numero exacto | Numero entero positivo | "Cuantas personas se vieron afectadas, aunque sea un estimado (por ejemplo: entre 50 y 100)." | OBL-INC-04 |
| Listado o referencia de titulares afectados | Lista de referencias (nunca copia de la base) | Opcional, recomendado si el numero es manejable | - | No debe convertirse en una carga masiva de la base completa | "Si puede identificar a las personas afectadas, registre una referencia (por ejemplo, un identificador interno), no copie aqui toda la base de datos." | Minimizacion [opinion de producto]; necesario para poder notificar a los titulares (OBL-INC-01) |
| Impacto estimado para los titulares | Texto largo | Obligatorio antes de Evaluacion | - | - | "Que le podria pasar a las personas afectadas por esto (por ejemplo: riesgo de suplantacion, exposicion de datos de salud)." | OBL-INC-04 |
| Existe riesgo en la seguridad de los datos personales | Booleano con justificacion (decision humana) | Obligatorio antes de Evaluacion | Si / No | Si es "No", exige justificacion visible en el historial y queda marcado para revision del Delegado | "¿Este incidente crea un riesgo real para la seguridad de los datos de las personas afectadas? De esto depende el nivel de documentacion exigido." | OBL-INC-04 (el deber reforzado de documentacion aplica a vulneraciones "que ocasionen un riesgo"); decision que NO se automatiza, ver seccion H |
| Severidad interna | Seleccion unica | Obligatorio desde Triage | Baja; Media; Alta; Critica | - | "Que tan grave es este caso para priorizar la atencion interna." | Buena practica [opinion de producto; sin equivalente legal directo] |

### D.3 Contencion, revision exhaustiva y remediacion

| Campo | Tipo | Obligatorio/opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Acciones de contencion inmediata | Texto largo, con fecha por cada entrada (bitacora) | Obligatorio al menos una entrada antes de Contencion completada | - | - | "Que hizo de inmediato para detener o limitar el dano (por ejemplo: se desconecto el servidor, se cambiaron las contrasenas)." | OBL-INC-03 lit. c) (acciones correctivas inmediatas, parte del contenido de la notificacion a la ACE) |
| Fecha de inicio de la revision exhaustiva | Fecha y hora, autocompletada al pasar a Investigacion | Obligatorio | - | Debe registrarse dentro de las 72 horas desde la fecha de conocimiento; si se registra despues, el sistema marca el hito como vencido en el historial, sin bloquear el avance del caso | "El momento en que formalmente inicio la revision a fondo del incidente. La ley exige que esta revision inicie (no que termine) dentro de las 72 horas desde que supo del caso." | OBL-INC-02 |
| Hallazgos de la revision exhaustiva | Texto largo, versionable | Obligatorio antes de Decision | - | - | "Que encontro al investigar a fondo: alcance real, sistemas comprometidos, vulnerabilidad explotada." | OBL-INC-02 |
| Medidas correctivas definitivas propuestas | Texto largo, enlazable a Control (MOD-015) | Obligatorio antes de Remediacion | Catalogo de controles de MOD-015 o texto libre para un control nuevo | - | "Que va a cambiar de forma permanente para que esto no vuelva a pasar (por ejemplo: activar 2FA, cambiar un proceso, capacitar al equipo)." | OBL-INC-02 ("medidas correctivas y preventivas... incluyendo la actualizacion de las politicas de seguridad") |
| Actualizacion de politicas de seguridad requerida | Booleano | Obligatorio antes de cierre | Si/No | Si es "Si", crea tarea hacia MOD-008/MOD-015 | "¿Este incidente exige actualizar alguna politica o procedimiento de seguridad?" | OBL-INC-02 |

### D.4 Decision, notificacion externa y Decreto 143

| Campo | Tipo | Obligatorio/opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Naturaleza del incidente (redaccion final) | Texto largo | Obligatorio antes de generar las notificaciones | - | - | "Una explicacion clara y breve de que paso, para incluir en la notificacion oficial." | OBL-INC-03 lit. a) |
| Datos personales comprometidos (redaccion final) | Texto largo (a partir de las categorias de D.2) | Obligatorio antes de generar las notificaciones | - | - | "Que datos se vieron comprometidos, redactado para que lo entienda quien lo reciba." | OBL-INC-03 lit. b) |
| Acciones correctivas inmediatas (redaccion final, solo para ACE/FGR) | Texto largo | Obligatorio antes de notificar a la ACE/FGR | - | - | "Que hizo su empresa de inmediato. Este contenido NO se incluye en la notificacion a los titulares; la ley solo lo exige para la ACE y la Fiscalia." | OBL-INC-03 (contenido diferenciado: presente para ACE/FGR, ausente para titulares) |
| Recomendaciones al titular | Texto largo | Obligatorio antes de generar las notificaciones | - | - | "Que le recomienda a las personas afectadas hacer (por ejemplo: cambiar su contrasena, estar alerta a mensajes sospechosos)." | OBL-INC-03 lit. d) |
| Medios de contacto para mas informacion | Texto | Obligatorio antes de generar las notificaciones | - | Debe incluir al menos un canal valido | "Como puede la persona (o la ACE) pedir mas informacion sobre este caso." | OBL-INC-03 lit. e) |
| Criterio de computo del plazo de 72 horas aplicado | Seleccion unica, con valor por defecto | Automatico (horas corridas), editable con justificacion y advertencia | Horas corridas (por defecto); Horas habiles (alternativa, marcada como criterio no verificado) | Cambiar el valor exige un campo de justificacion visible en el historial y muestra la advertencia de incertidumbre | "La ley no aclara si las 72 horas se cuentan de corrido o solo en horas habiles. El sistema usa por defecto el criterio mas exigente (horas corridas) para protegerlo. Si cambia este criterio, dejelo justificado." | Ambiguedad documentada en `03_hallazgos_regulatorios.md` seccion 9.1; decision 2.7.11 de `02_validacion_de_la_idea.md` |
| Notificacion a la ACE y a la FGR enviada | Booleano + fecha/hora + canal + adjunto | Obligatorio para cerrar el hito de notificacion | Canal: correo oficial / plataforma de la ACE (cuando este disponible) / otro medio documentado | Requiere aprobacion previa del Delegado (ver seccion F) | "Marque esto cuando ya envio la notificacion oficial. El sistema guarda una copia y la hora exacta." | OBL-INC-01, OBL-INC-03 |
| Notificacion a titulares enviada | Booleano + fecha/hora + canal + adjunto, por lote o individual | Obligatorio para cerrar el hito de notificacion | Canal: correo; carta fisica; comunicado dentro de un portal si existe; otro documentado | Requiere aprobacion previa del Delegado | "Marque esto cuando ya avisó a las personas afectadas." | OBL-INC-01, OBL-INC-03 |
| La organizacion esta calificada como operador de infraestructura critica (Decreto 143) | Booleano, configurado a nivel de organizacion en MOD-001, referenciado aqui | Condicional; visible siempre, obligatorio de responder solo si es Si | Si (con referencia a la resolucion de la ACE) / No / No aplica | Si es "Si", exige adjuntar la resolucion de calificacion de la ACE | "Si la ACE calificó formalmente a su empresa como operador de infraestructura critica, este incidente puede tener un deber adicional de reporte bajo la Ley de Ciberseguridad." | OBL-INC-05 |
| Reporte adicional a la ACE bajo el Decreto 143 realizado | Booleano + fecha + evidencia | Obligatorio solo si el campo anterior es "Si" | - | - | "Si aplica el deber adicional, marque cuando lo cumplio. La ley no fija un numero de horas para este reporte, pero exige actuar de inmediato." | OBL-INC-05 |

### D.5 Decision de cierre

| Campo | Tipo | Obligatorio/opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Decision final del caso | Seleccion unica | Obligatorio para cerrar | Resuelto con notificacion enviada; Resuelto sin obligacion de notificar (justificado); Descartado en Triage (no era vulneracion de datos personales); Transferido a otro proceso | - | "Como termino el caso." | OBL-INC-04, OBL-PRIN-03 (responsabilidad demostrada) |
| Justificacion de la decision de cierre | Texto largo | Obligatorio para cerrar | - | Minimo 20 caracteres | "Por que se tomo esta decision, en sus propias palabras." | OBL-INC-04 |
| Responsable de la decision de cierre | Referencia a Usuario, autocompletada | Obligatorio, automatico | - | - | "Queda registrado quien tomo la decision final y cuando." | OBL-PRIN-03, `05_tipos_de_usuario.md` 5.4 |
| Lecciones aprendidas | Texto largo | Opcional, recomendado | - | - | "Que aprendio su empresa de este caso, para evitar que se repita." | Buena practica (deriva de OBL-INC-02, actualizacion de politicas) |

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Borrador de notificacion a la ACE y a la FGR | Los cinco elementos de OBL-INC-03 lit. a) a e), a partir de los campos de D.4 | Documento de texto, plantilla del sistema | Automaticamente al completar los campos obligatorios de D.4, antes de la aprobacion | Delegado / Responsable interno (para aprobar) |
| Borrador de notificacion a titulares | Los cuatro elementos de OBL-INC-03 (a, b, d, e; se omite c) | Documento de texto, plantilla del sistema, version simplificada para publico no especialista | Automaticamente junto con la anterior | Delegado / Responsable interno (para aprobar); luego se envia a los titulares |
| Constancia de envio de cada notificacion | Fecha, hora, canal, destinatario, version del contenido enviado, quien aprobo | Registro interno con adjunto, con verificacion de integridad (hash) | Al marcar la notificacion como enviada | Centro de Evidencias (MOD-019); visible para Auditor |
| Tareas automaticas | Por ejemplo: "iniciar revision exhaustiva antes de [fecha limite]", "enviar notificacion antes de [fecha limite]", "documentar medidas correctivas definitivas", "evaluar si corresponde EIPD" | Tarea en el Centro de Tareas, con responsable, fecha y fundamento | Al cambiar de estado (ver seccion F) o al activarse una regla de la seccion G | Responsable de Seguridad/IT, Delegado, Responsable de area asignado |
| Alertas de cronometro | Ver seccion I | Notificacion en plataforma y por correo (y otros canales configurados) | Segun los umbrales de tiempo restante de cada cronometro | Responsable de Seguridad/IT, Delegado, Administrador (escalamiento) |
| Expediente documentado del incidente | Todos los campos de la seccion D mas la bitacora de acciones e historial de estados | Vista consolidada, exportable a PDF | Se actualiza en tiempo real; el expediente final queda fijo al cerrar el caso | Auditor, Delegado, Responsable Legal, y la ACE si la solicita |
| Indicador para el dashboard | Estado del programa frente a incidentes (ver seccion M) | Panel visual, sin porcentaje de "cumplimiento legal" | Al vencer o cumplirse cada cronometro, y al cerrar cada caso | Gerencia, Responsable, Legal, Auditor |
| Evento de creacion de EIPD (si aplica) | Referencia al tratamiento afectado y al incidente que la origino | Tarea/registro hacia MOD-014 | Cuando el incidente involucra datos sensibles o un tratamiento de alto riesgo aun no evaluado | Delegado, Responsable Legal |
| Registro de conservacion del expediente | Fecha de cierre + plazo minimo recomendado de conservacion (5 anos, OBL-RET-05) | Registro hacia el motor de retencion documental de MOD-016 | Al cerrar el caso | MOD-016 (motor de retencion); visible para Administrador y Auditor |

---

## F. Workflow

Profundidad especial de este modulo: el flujo completo, con los dos hitos de 72 horas (notificacion externa e inicio de la revision interna) corriendo en paralelo desde el mismo momento de conocimiento, tal como lo fija la decision 11 de `02_validacion_de_la_idea.md` (inconsistencia 13).

### F.1 Diagrama ASCII de estados

```
                 (fecha de conocimiento registrada)
                              |
                              v
                      +---------------+
                      |   REPORTADO   |
                      +---------------+
                              |
                    inicia clasificacion
                              v
                      +---------------+
                      |    TRIAGE     |<---------------------+
                      +---------------+                       |
                        |            |                        |
             es vulneracion?     no es vulneracion             |
             (decision humana)   de datos personales           |
                        |            |                        |
                        v            v                        |
              +----------------+  +------------------------+  |
              | INVESTIGACION  |  | DESCARTADO (terminal)  |  |
              +----------------+  +------------------------+  |
                        |                                     |
        (arranca el cronometro de revision:                   |
         debe iniciar <= 72h desde conocimiento)               |
                        |                                     |
                        v                                     |
              +----------------+                              |
              |  CONTENCION    |------ (accion continua, puede |
              +----------------+        empezar desde REPORTADO)
                        |
                        v
              +----------------+
              |  EVALUACION    |  <- hay riesgo? cantidad de titulares?
              +----------------+     activa EIPD? aplica Decreto 143?
                        |
                        v
              +----------------+
              |   DECISION     |  <- decision humana no automatizable
              +----------------+     (ver seccion H)
                   |         |
        requiere        no requiere
        notificar        notificar
        externa          externa (caso raro, justificado)
                   |         |
                   v         v
          +----------------+  +---------------------------+
          | NOTIFICACION   |  | CIERRE SIN NOTIFICACION    |
          +----------------+  | EXTERNA (justificado)      |
                   |          +---------------------------+
       (envio <= 72h desde              |
        conocimiento; aprobado                    |
        por el Delegado)                          |
                   |                               |
                   v                               |
          +----------------+                       |
          | REMEDIACION    |                       |
          +----------------+                       |
                   |                                |
                   v                                |
          +----------------+                        |
          |    CIERRE      |<-----------------------+
          +----------------+
                   |
                   v
          +----------------+
          |   LECCIONES    |  (estado terminal informativo,
          |  APRENDIDAS    |   no bloquea el cierre legal)
          +----------------+
                   |
          (si aparece informacion nueva)
                   v
          +----------------+
          |   REABIERTO    |----> vuelve a INVESTIGACION o EVALUACION
          +----------------+       segun el motivo de reapertura
```

Nota de lectura: "CONTENCION" no es estrictamente secuencial. Las acciones de contencion inmediata (por ejemplo, desconectar un servidor) pueden y deben registrarse desde el momento de REPORTADO o TRIAGE si la urgencia lo exige; el estado formal "CONTENCION" marca el punto en que el sistema exige al menos una accion documentada antes de avanzar a EVALUACION, no que la contencion solo pueda ocurrir en ese momento.

### F.2 Tabla de transiciones

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos (tareas, alertas, evidencia, auditoria) |
|---|---|---|---|---|---|
| (ninguno) | Reportar un incidente | Debe existir al menos titulo, fecha de deteccion y quien reporta | Reportado | Cualquier rol con permiso de crear (ver seccion C) | Crea el expediente; evento de auditoria "incidente creado"; si no hay fecha de conocimiento aun, el sistema advierte que los cronometros no han iniciado |
| Reportado | Confirmar fecha de conocimiento | Fecha de conocimiento registrada (D.1) | Triage | Responsable de Seguridad/IT, Delegado | Arrancan ambos cronometros de 72 horas (notificacion y revision); se crean las tareas "iniciar revision antes de..." y "notificar antes de..." en MOD-021; alerta INFO de inicio de plazo |
| Triage | Marcar "Es vulneracion de datos personales = No", con justificacion | Justificacion obligatoria (D.2) | Descartado | Responsable de Seguridad/IT, Delegado, Legal | Detiene ambos cronometros; evento de auditoria con la justificacion completa, visible para Auditor; el caso queda accesible para reapertura |
| Triage | Marcar "Es vulneracion de datos personales = Si" | Categorias de datos y tipo de vulneracion registrados (D.2) | Investigacion | Responsable de Seguridad/IT, Delegado | Se habilita el registro de "fecha de inicio de la revision exhaustiva"; si ya paso mas de 72h desde el conocimiento sin haber marcado el inicio, el sistema marca el hito de revision como vencido en el historial (no bloquea el avance) |
| Investigacion | Registrar hallazgos y avanzar | Fecha de inicio de revision registrada; al menos una accion de contencion documentada | Contencion (si aun no hay acciones) o Evaluacion (si ya hay) | Responsable de Seguridad/IT | Actualiza el indicador de dashboard "revision iniciada dentro/fuera de plazo"; evidencia de la bitacora de hallazgos |
| Contencion | Registrar al menos una accion de contencion y completar hallazgos minimos | Campos D.3 completos | Evaluacion | Responsable de Seguridad/IT | Habilita los campos de D.2 relativos a riesgo, cantidad de titulares e impacto |
| Evaluacion | Registrar "existe riesgo" y cantidad/impacto estimado | Campos D.2 (riesgo, cantidad, impacto) completos | Decision | Responsable de Seguridad/IT, Delegado, Legal | Si "existe riesgo = Si", bloquea el cierre posterior hasta completar todos los campos de OBL-INC-04 (D.5); si el tratamiento afectado no tenia EIPD y corresponde por datos sensibles, crea tarea hacia MOD-014 |
| Decision | Decidir si corresponde notificacion externa, con justificacion si la respuesta es "No" | Decision explicita y documentada (ver seccion H, no automatizable) | Notificacion o Cierre sin notificacion externa (justificado) | Delegado, Responsable Legal (co-revision) | Evento de auditoria de la decision; si se elige "No notificar", la justificacion queda visible para cualquier auditoria posterior de la ACE |
| Decision | Generar los borradores de notificacion (ACE/FGR y titulares) | Campos de D.4 completos | Notificacion | Responsable de Seguridad/IT (prepara), Delegado (aprueba) | Genera los dos documentos de la seccion E; quedan marcados "borrador pendiente de aprobacion" |
| Notificacion | Aprobar y marcar como enviada cada notificacion | Aprobacion explicita del Delegado; registro de fecha, hora y canal | Remediacion (cuando ambas notificaciones, ACE/FGR y titulares, estan enviadas) | Delegado | Constancia de envio con verificacion de integridad; si el envio ocurre despues de las 72 horas desde el conocimiento, el sistema no bloquea el envio pero marca el hito como vencido en el historial, visible de forma permanente |
| Remediacion | Registrar medidas correctivas definitivas y confirmar actualizacion de politicas si corresponde | Campos D.3 (medidas definitivas, actualizacion de politicas) completos | Cierre | Responsable de Seguridad/IT, Delegado | Enlaza o crea Control(es) en MOD-015; si hay tarea de actualizacion de politica, se crea en MOD-021 |
| Cierre sin notificacion externa (justificado) | Completar justificacion y decision de cierre | Campos D.5 completos | Cierre | Delegado, Legal | Mismo efecto que un cierre ordinario, pero queda marcado explicitamente como "sin notificacion externa" en el historial y en los reportes |
| Remediacion / Cierre sin notificacion | Cerrar el caso | Campos D.5 completos; si esta por encima del umbral de separacion de funciones, requiere aprobacion adicional del rol Aprobador | Cierre | Responsable de Seguridad/IT o Delegado (segun quien gestione); Aprobador si aplica el umbral | Calcula la fecha de conservacion del expediente (cierre + minimo recomendado de 5 anos, OBL-RET-05) y la envia a MOD-016; el expediente queda de solo lectura salvo reapertura |
| Cierre | Registrar lecciones aprendidas | Opcional | Lecciones aprendidas | Cualquier rol con acceso al caso | Informativo; puede generar tareas hacia MOD-015 (nuevo control) o MOD-017 (necesidad de capacitacion) |
| Cierre / Lecciones aprendidas | Reabrir el caso (por ejemplo, nueva informacion, reclamo de un titular, requerimiento de la ACE) | Justificacion obligatoria del motivo de reapertura | Reabierto (vuelve a Investigacion o Evaluacion segun el motivo) | Delegado, Responsable Legal, Administrador | El expediente conserva integramente el historial anterior; se abre una nueva linea de tiempo dentro del mismo caso, nunca se sobrescribe lo ya cerrado |

**Estados terminales:** Descartado (si nunca fue una vulneracion de datos personales) y Cierre (con o sin notificacion externa, con lecciones aprendidas opcionales). Ambos son reabribles con justificacion.

**Reapertura:** nunca borra ni sobrescribe el expediente original; agrega una nueva linea de tiempo dentro del mismo caso, preservando integramente la version anterior para efectos de evidencia (OBL-INC-04, OBL-PRIN-03).

**Archivado:** no es una accion manual del usuario; ocurre automaticamente cuando el motor de retencion documental de MOD-016 determina que se cumplio el plazo de conservacion (minimo recomendado 5 anos desde el cierre, OBL-RET-05) y no hay una obligacion legal mayor que lo extienda (por ejemplo, una investigacion abierta de la ACE).

**Registros vinculados:** las tareas creadas en MOD-021 a partir de este incidente quedan enlazadas por referencia; si el incidente se reabre, las tareas cerradas no se reabren automaticamente, se crean tareas nuevas para el nuevo motivo.

---

## G. Automatizaciones

Todas las reglas de tiempo (72 horas, umbrales de alerta) son configurables por la empresa dentro de los limites que marca cada regla; el criterio de computo por defecto (horas corridas) y los umbrales de alerta se explican como configuracion visible, nunca oculta.

| # | Disparador | Condicion | Accion | Configurable |
|---|---|---|---|---|
| 1 | Se registra la fecha de conocimiento | Siempre | Inicia el cronometro de notificacion (72h) y el cronometro de revision exhaustiva (72h), en paralelo, con el criterio de computo por defecto (horas corridas) | Si, el criterio de computo (con advertencia visible al cambiarlo) |
| 2 | Cronometro de notificacion llega al 50% del tiempo restante consumido (24h transcurridas por defecto) | Notificacion aun no enviada | Alerta WARNING a Responsable de Seguridad/IT y Delegado (ver seccion I) | Si, el umbral de horas |
| 3 | Cronometro de notificacion llega a 6 horas restantes | Notificacion aun no enviada | Alerta CRITICAL, escalada a Administrador y Aprobador; repite cada hora | Si, el umbral y la frecuencia |
| 4 | Cronometro de notificacion llega a 0 (72h cumplidas) | Notificacion aun no enviada | Marca el hito "notificacion" como vencido en el historial (de forma permanente e irreversible); alerta CRITICAL a Administrador, Delegado y Legal; no bloquea el envio posterior | No (el registro del vencimiento no es desactivable, para preservar la evidencia) |
| 5 | Cronometro de revision llega a 70 horas transcurridas | Estado aun no paso a Investigacion (fecha de inicio de revision no registrada) | Alerta HIGH a Responsable de Seguridad/IT, escalada al Delegado | Si, el umbral |
| 6 | Se marca "existe riesgo = Si" (D.2) | Al entrar a Evaluacion | Bloquea el avance a Decision hasta completar los campos obligatorios de OBL-INC-04 (D.5 parcial: cantidad, impacto, medidas) | No (la exigencia legal de documentar no es opcional cuando hay riesgo) |
| 7 | Se completan los campos de D.4 (naturaleza, datos comprometidos, acciones correctivas, recomendaciones, medios de contacto) | En estado Decision | Genera automaticamente los dos borradores de notificacion (ACE/FGR y titulares), con el contenido diferenciado de OBL-INC-03, marcados "pendiente de aprobacion" | No en el contenido minimo legal; si en el formato/plantilla visual |
| 8 | El Delegado aprueba una notificacion | Borrador existente | Bloquea la edicion de esa version, registra el envio con fecha, hora, canal y hash de integridad; crea el evento de auditoria correspondiente | No |
| 9 | Se marcan categorias de datos = Biometrica o Salud, o el tratamiento relacionado no tiene EIPD registrada en MOD-014 | Durante Evaluacion o Investigacion | Crea tarea "evaluar si corresponde EIPD" hacia MOD-014, con referencia al incidente como origen | No en la creacion de la tarea; si en a quien se asigna |
| 10 | Se marca "organizacion calificada como operador de infraestructura critica = Si" en MOD-001 y el incidente es de tipo ciberseguridad | Al entrar a Evaluacion | Muestra el campo condicional de reporte adicional bajo el Decreto 143 (OBL-INC-05) con alerta de "actuar de inmediato", sin cronometro numerico | No en la activacion del campo; si en el texto de la alerta |
| 11 | El incidente tiene origen = Proveedor/Encargado | Al registrar el origen | Muestra, si existe, el plazo de aviso pactado en el contrato/DPA de MOD-009 (por ejemplo, 24 horas), y calcula cuanto de ese plazo ya se consumio dentro de las 72 horas totales | No (es informativo) |
| 12 | Se cierra el caso | Estado Cierre alcanzado | Calcula la fecha de conservacion del expediente (cierre + minimo recomendado, ver OBL-RET-05) y la envia a MOD-016; genera el evento de auditoria de cierre con responsable y justificacion | Si, el periodo minimo de conservacion (dentro del rango recomendado por MOD-016), no la obligacion de calcularlo |
| 13 | El caso permanece en "Lecciones aprendidas" con medidas correctivas nuevas propuestas | Al registrar una medida nueva | Crea o actualiza el Control correspondiente en MOD-015 | No en la creacion del vinculo, si en si se crea un Control nuevo o se enlaza uno existente |

---

## H. Decisiones que NO debe automatizar

1. **Calificar si un evento es una "vulneracion de seguridad de datos personales" bajo el Art. 25.** De esta calificacion depende si se activan las 72 horas legales. El sistema no puede inferir esto de forma automatica a partir de un ticket tecnico; exige que una persona lo confirme o lo descarte con justificacion. Advertencia mostrada: "Requiere validacion de la organizacion o asesoria especializada."
2. **Determinar si existe "riesgo en la seguridad de los datos personales" para efectos del deber reforzado de documentacion (OBL-INC-04).** La ley usa un termino abierto ("riesgo") sin definirlo numericamente; el sistema no asigna un score automatico que sustituya este juicio. Advertencia mostrada: "Requiere validacion de la organizacion o asesoria especializada."
3. **Decidir el contenido final y el momento exacto de envio de cada notificacion**, especialmente cuando la investigacion no ha concluido al llegar a las 72 horas. El sistema genera el borrador con la informacion disponible, pero no decide si esa informacion es suficiente para notificar o si conviene esperar (con el riesgo de vencer el plazo). Advertencia mostrada: "Requiere validacion de la organizacion o asesoria especializada."
4. **Cambiar el criterio de computo del plazo de 72 horas** (de horas corridas al criterio alternativo de horas habiles). El sistema aplica un valor conservador por defecto, pero cambiarlo para un caso especifico es una decision de riesgo legal que exige criterio humano informado. Advertencia mostrada: "La ley no precisa si este plazo se cuenta en horas corridas u horas habiles. El sistema aplica por defecto el criterio mas conservador. Verifique este criterio con asesoria legal si el caso es critico."
5. **Confirmar si la empresa califica como "operador de infraestructura critica" bajo el Decreto 143.** Esta calificacion es un acto formal de la ACE (resolucion fundada, ratificada por el Presidente), nunca una autodeclaracion ni una inferencia del sistema a partir del giro de la empresa. Advertencia mostrada: "Requiere validacion de la organizacion o asesoria especializada."
6. **Aprobar el envio de cualquier notificacion externa** (a la ACE, a la FGR o a los titulares). El sistema prepara el borrador; el envio siempre requiere una aprobacion explicita y trazable del Delegado / Responsable interno. Advertencia mostrada: junto al boton de aprobacion, "Documento generado como borrador a partir de la informacion registrada. Requiere revision y aprobacion de su organizacion antes de usarse, y puede requerir validacion de asesoria legal especializada" (texto estandar de `04_objetivo_exacto_del_producto.md` seccion 1.3).
7. **Decidir la decision final de cierre del caso y si las medidas correctivas fueron suficientes.** El sistema no cierra un caso por si mismo ni evalua la suficiencia de las medidas tomadas; solo bloquea el cierre si faltan campos obligatorios. Advertencia mostrada: "Requiere validacion de la organizacion o asesoria especializada."
8. **Determinar si un proveedor o encargado incumplio su obligacion contractual de aviso oportuno del incidente.** Esto es una cuestion contractual y comercial entre la empresa y su proveedor que el sistema no puede resolver; solo muestra los tiempos registrados. Advertencia mostrada: "Requiere validacion de la organizacion o asesoria especializada."

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia/repeticion | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Cronometro de notificacion - aviso temprano | 50% del plazo de 72h consumido sin notificacion enviada | WARNING | Responsable de Seguridad/IT, Delegado | Plataforma + correo | Una vez | A Administrador si no hay accion en 6 horas | La notificacion se marca como enviada, o el caso se marca Descartado |
| Cronometro de notificacion - critico | 6 horas restantes sin notificacion enviada | CRITICAL | Delegado, Administrador, Aprobador | Plataforma + correo (+ SMS si el canal esta configurado) | Cada hora hasta el vencimiento | Inmediato a Gerencia (perspectiva Administrador del dashboard) | La notificacion se marca como enviada |
| Plazo de notificacion vencido | 72 horas cumplidas sin notificacion enviada | CRITICAL | Administrador, Delegado, Legal | Plataforma + correo | Diaria hasta que se resuelva | Gerencia General | Nunca se apaga del todo: la notificacion enviada tardiamente registra el incumplimiento de forma permanente en el historial, aunque la alerta activa deje de repetirse |
| Cronometro de revision - inicio pendiente | 60 horas transcurridas sin marcar inicio de la revision exhaustiva | WARNING | Responsable de Seguridad/IT | Plataforma + correo | Una vez | A Delegado a las 70 horas | El estado pasa a Investigacion con fecha de inicio registrada |
| Documentacion incompleta con riesgo confirmado | Se intenta avanzar a Decision con "existe riesgo = Si" y campos de OBL-INC-04 incompletos | HIGH (bloqueante, no solo informativa) | Responsable de Seguridad/IT | Plataforma | Cada intento de avance | No aplica (es un bloqueo, no un escalamiento) | Se completan los campos obligatorios |
| Incidente en proveedor sin evidencia de aviso | Origen = Proveedor/Encargado y no hay registro de aviso del proveedor dentro del plazo pactado en el contrato (si existe) | WARNING | Responsable de Seguridad/IT, Responsable de Proveedores (MOD-009) | Plataforma + correo | Una vez | A Legal si transcurre el 80% del plazo total de 72h | Se registra el aviso del proveedor, o el caso avanza sin el dato (con nota visible) |
| Posible operador de infraestructura critica no confirmado | El incidente es de tipo ciberseguridad y el sector de la organizacion coincide con los sectores tipicos de infraestructura critica, pero el campo de calificacion (D.4) esta vacio | INFO | Administrador | Plataforma | Una vez por incidente | No aplica | Se completa el campo con Si/No/No aplica |
| Caso cerrado con notificacion tardia | Se cierra un caso que tiene el hito de notificacion marcado como vencido en el historial | INFO (registro para auditoria, no requiere accion) | Auditor interno, Legal | Plataforma | Una vez | No aplica | No se apaga; queda como marca permanente visible en reportes |

---

## J. Evidencia

| Evidencia | Como se genera y conserva | Obligacion que prueba | Retencion |
|---|---|---|---|
| Expediente completo del incidente (todos los campos de la seccion D) | Registro versionado con fecha y hora de cada cambio, usuario que lo hizo, valor anterior y nuevo | OBL-INC-04 (documentacion obligatoria de toda vulneracion con riesgo) | Minimo recomendado 5 anos desde el cierre (OBL-RET-05); referenciar politica de MOD-016 |
| Bitacora de deteccion y conocimiento (fecha de deteccion, fecha de conocimiento y su justificacion si difieren) | Registro inmutable de solo adicion (append-only) | OBL-INC-01, OBL-INC-02 (inicio del computo de ambos plazos de 72 horas) | Igual que el expediente |
| Constancia de envio de cada notificacion (ACE/FGR y titulares) | Registro con fecha, hora, canal, destinatario, contenido enviado (version fija) y hash de integridad verificable | OBL-INC-01, OBL-INC-03 | Igual que el expediente |
| Registro de aprobacion del Delegado / Responsable interno para cada notificacion | Identidad del aprobador, fecha y hora, version aprobada | OBL-INC-01 (acto atribuido a quien concentra hoy las funciones del Delegado); responsabilidad demostrada, OBL-PRIN-03 | Igual que el expediente |
| Bitacora de acciones de contencion y hallazgos de la revision exhaustiva | Entradas con fecha, hora y usuario, no editables retroactivamente sin dejar rastro | OBL-INC-02 | Igual que el expediente |
| Registro de la decision de cierre (quien decidio, cuando, con que fundamento) | Campo obligatorio de justificacion, vinculado a identidad del usuario | OBL-INC-04, OBL-PRIN-03; `05_tipos_de_usuario.md` 5.4 | Igual que el expediente |
| Historial de vencimientos (notificacion y/o revision fuera de plazo) | Marca permanente, visible en reportes y en el expediente, nunca eliminable | OBL-INC-01, OBL-INC-02 (evidencia honesta del propio incumplimiento, mejor que ocultarlo) | Igual que el expediente |
| Evidencia del reporte adicional bajo el Decreto 143 (si aplica) | Fecha, canal, adjunto | OBL-INC-05 | Igual que el expediente |

Todo paquete de evidencias exportado desde este modulo (por ejemplo, para una auditoria o para responder a un requerimiento de la ACE) incluye un mecanismo de verificacion de integridad (hash o firma validable de forma independiente), en linea con el anti-feature 25 de `22_anti_features.md`.

---

## K. Documentos asociados

**Documentos requeridos como entrada:**
- Contrato o DPA con el proveedor/encargado (de MOD-009), cuando el origen del incidente es un proveedor, para conocer el plazo pactado de aviso y las obligaciones de cooperacion (ver `sweep_encargados_transferencias.md` seccion 5.6).
- Politica de seguridad de la informacion vigente (de MOD-008), como referencia para saber si el incidente exige actualizarla (OBL-INC-02).

**Documentos generados:**
- Notificacion formal a la ACE y a la FGR (borrador, luego version enviada fija).
- Notificacion formal a los titulares afectados (borrador, luego version enviada fija; puede generarse en lote si hay muchos titulares).
- Informe de cierre del incidente (resumen del expediente, para uso interno o para entregar a un auditor).
- Reporte adicional a la ACE bajo el Decreto 143, si la organizacion esta calificada como operador de infraestructura critica.

**Plantillas que el sistema provee:**
- Plantilla de notificacion a la ACE/FGR (variables: naturaleza, datos comprometidos, acciones correctivas, recomendaciones, medios de contacto; requiere validacion de la organizacion antes de enviarse).
- Plantilla de notificacion a titulares (mismas variables salvo acciones correctivas; lenguaje simplificado para publico no especialista; requiere validacion de la organizacion).
- Checklist de las 72 horas (lista de verificacion de los pasos minimos exigidos, ver seccion R).
- Plantilla de informe de cierre.

**Anexos y evidencias documentales:** capturas de pantalla, logs tecnicos puntuales, comunicaciones con el proveedor, resolucion de calificacion de infraestructura critica (si aplica); todos como adjuntos con hash de integridad, nunca como copia de la base de datos comprometida.

---

## L. Dependencias

### L.1 Diagrama ASCII

```
   MOD-006 RAT y Mapa de Datos --------\
   (que tratamiento/sistema fue         \
    afectado, si el dato es sensible)    v
                                   +----------------+
   MOD-015 Controles de Seguridad |                |
   (catalogo de controles para   -->  MOD-013      |
    contencion/remediacion;         Incidentes de  |
    que control existia)             Seguridad     |
                                   |                |
   MOD-009 Proveedores y Encargados-->  (relacion   |
   (referencia informativa, ver     informativa,    |
    nota al final de esta ficha)    no dependencia  |
                                    formal del mapa) |
                                   +----------------+
                                    |    |    |    |
                    +---------------+    |    |    +-----------------+
                    v                    v    v                      v
           MOD-021 Centro de    MOD-022      MOD-023 Calendario   MOD-024 Centro
           Tareas               Notificaciones  y Motor de Plazos  Regulatorio
           (tareas: iniciar     (alertas         (calculo de las   (marco Decreto 143,
            revision, notificar, internas de      72 horas;         bandera doble estado
            documentar)          cronometro)       criterio horas    659 aunque no aplica
                                                    corridas)         directamente aqui)
                    |
                    v
           MOD-019 Centro de Evidencias  (expediente, constancias de envio)
                    |
                    v
           MOD-016 Retencion y Eliminacion  (colaboradora, OBL-RET-05: plazo
                                             de conservacion del expediente cerrado)
```

### L.2 Lista de dependencias

**Recibe datos de:**
- MOD-006 RAT y Mapa de Datos: identifica el tratamiento y el sistema afectado, y si el tratamiento ya tenia categorias de datos sensibles marcadas.
- MOD-015 Controles de Seguridad: catalogo de controles existentes, para referenciar cuales fallaron y cuales se crean o refuerzan como medida correctiva.

**Envia datos o eventos a:**
- MOD-019 Centro de Evidencias: el expediente completo y las constancias de envio de notificacion.
- MOD-021 Centro de Tareas: tareas de investigacion, notificacion, remediacion y documentacion.
- MOD-022 Notificaciones: alertas internas de cronometro y escalamiento (distinto de la notificacion externa a la ACE/FGR/titulares, que es un acto sustantivo del propio modulo, no una alerta).
- MOD-023 Calendario y Motor de Plazos: consulta el servicio de calculo de plazos para las 72 horas (con el criterio de horas corridas por defecto).
- MOD-024 Centro Regulatorio: el campo condicional del Decreto 143 (OBL-INC-05) se apoya en la bandera de "operador de infraestructura critica" que administra MOD-001, visible tambien desde MOD-024 como parte del marco normativo.
- MOD-016 Retencion y Eliminacion (colaboradora en OBL-RET-05): al cerrar el caso, envia la fecha de cierre para que el motor de retencion documental calcule y vigile el plazo minimo recomendado de conservacion del expediente (5 anos).
- MOD-014 Riesgos y EIPD: crea una tarea de evaluacion de EIPD cuando el incidente revela un tratamiento de alto riesgo sin evaluar.

**Catalogos que comparte:** catalogo de sistemas (con MOD-006), catalogo de categorias de datos sensibles (con MOD-006, MOD-007), catalogo de controles (con MOD-014, MOD-015).

**Que ocurre si un modulo dependiente no existe en el MVP:**
- MOD-006 y MOD-015 son ambos MUST HAVE, por lo que estan disponibles desde el MVP; no hay escenario de ausencia que resolver.
- MOD-014 (Riesgos y EIPD) es SHOULD HAVE. Si aun no esta disponible, la tarea "evaluar si corresponde EIPD" se crea igual en MOD-021, pero como una tarea generica sin el cuestionario de scoring (mismo patron de cobertura parcial descrito en la ficha de MOD-014).
- MOD-012 (Portal del Titular) es SHOULD HAVE y no es una dependencia de este modulo: la notificacion a titulares no depende de que exista un portal publico; se envia por el canal disponible (correo, carta, u otro documentado) desde el MVP.

**Nota sobre MOD-009 (Proveedores y Encargados):** `mapa_modulos.json` no lista a MOD-009 dentro de `depende_de` ni de `alimenta_a` de MOD-013. Esta ficha modela de todas formas una referencia informativa desde el incidente hacia el proveedor de origen (campo D.1 "Proveedor/Encargado relacionado"), porque la ley exige documentar la causa del incidente (OBL-INC-04) y el contenido minimo recomendado del contrato con el encargado incluye una clausula especifica de aviso de incidentes (`sweep_encargados_transferencias.md` seccion 5.6). Se marca esta observacion tambien en la nota final de esta ficha, para que quede visible al equipo que mantiene el mapa de modulos.

---

## M. Dashboard

Nunca se expresa como "porcentaje de cumplimiento legal"; siempre como estado del programa, controles configurados, tareas pendientes o evidencia disponible (ver `04_objetivo_exacto_del_producto.md` seccion 1.2).

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Incidentes abiertos por severidad | Conteo de casos en estados Reportado a Remediacion, agrupados por severidad interna | Verde: sin casos Alta/Critica abiertos; Amarillo: 1 o mas Alta; Rojo: 1 o mas Critica | Gerencia (resumen), Responsable (detalle) |
| Cronometros de 72h por vencer | Conteo de casos con menos de 24 horas restantes en cualquiera de los dos cronometros | Amarillo bajo 24h; Rojo bajo 6h | Responsable, Gerencia (alerta destacada) |
| Casos con notificacion enviada dentro de plazo (ultimos 12 meses) | (Casos con notificacion enviada antes de vencer el cronometro) / (total de casos con notificacion requerida) | Sin umbral de "cumplimiento"; se muestra como dato de estado del programa | Legal, Auditor |
| Tiempo promedio de cierre | Promedio de dias entre Reportado y Cierre, ultimos 12 meses | Informativo, sin semaforo | Responsable, Gerencia |
| Incidentes por origen (interno / proveedor / terceros) | Conteo agrupado por el campo "Origen del incidente" | Informativo | Legal, Auditor |
| Expedientes con documentacion incompleta (OBL-INC-04) | Conteo de casos con "existe riesgo = Si" y campos de D.5 incompletos, aun abiertos | Rojo si hay alguno con mas de 72 horas de antiguedad en ese estado | Responsable, Legal |

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Listado de incidentes del periodo | Titulo, fechas clave, severidad, estado, si hubo notificacion y si fue dentro de plazo | Rango de fechas, severidad, estado, origen | PDF, XLSX, CSV | Gerencia, Legal | No (es un reporte gerencial) |
| Expediente individual de un incidente | Todos los campos de la seccion D, bitacora completa, constancias de notificacion | Un incidente especifico | PDF, ZIP (con adjuntos) | Auditor, la ACE si lo requiere | Si |
| Reporte de cumplimiento de plazos de notificacion | Cuantos casos vencieron el plazo de 72 horas, cuanto tiempo de exceso, justificacion registrada | Rango de fechas | PDF, XLSX | Legal, Auditor, Gerencia | Si |
| Reporte de incidentes por proveedor | Incidentes cuyo origen fue un proveedor/encargado, con el tiempo de aviso del proveedor frente al plazo pactado | Rango de fechas, proveedor especifico | PDF, XLSX | Responsable de Proveedores, Legal | Si |
| Paquete de evidencia para auditoria anual (OBL-AUD-01) | Todos los expedientes cerrados del periodo, con constancias de notificacion y hash de integridad | Rango de fechas | ZIP firmado | Auditor externo | Si |

---

## O. Historial

Eventos que quedan en el historial del modulo y en la auditoria transversal (MOD-018), todos con fecha, hora, usuario y, cuando corresponda, valor anterior y nuevo:

- Creacion del incidente (quien lo reporto, con que datos iniciales).
- Registro y cualquier cambio posterior de la fecha de conocimiento, siempre con la justificacion si se modifica despues del registro inicial (es el dato que dispara ambos plazos legales, ver OBL-INC-01 y OBL-INC-02).
- Cambios de estado (cada transicion de la seccion F, con quien la ejecuto).
- Cambios de cualquier campo de la seccion D (valor anterior y nuevo), en particular los campos que alimentan el contenido de la notificacion (D.4).
- Asignaciones de tareas relacionadas con el incidente.
- Aprobaciones de cada notificacion (quien aprobo, cuando, que version).
- Envios de notificacion (fecha, hora, canal, si fue dentro o fuera del plazo de 72 horas).
- Adjuntos agregados o removidos, con el hash de cada archivo.
- Exportaciones del expediente o de cualquier paquete de evidencia (quien exporto, cuando, con que filtro).
- Accesos de lectura de roles con acceso temporal (Auditor externo, Asesor externo invitado) a datos sensibles del expediente.
- Decision de cierre, con la justificacion completa y el responsable.
- Reaperturas, con el motivo.
- Vencimientos de cualquiera de los dos cronometros de 72 horas (evento permanente, no editable ni eliminable).

---

## P. Riesgos

| Riesgo | Tipo | Mitigacion de diseno |
|---|---|---|
| Confundir "fecha de deteccion" con "fecha de conocimiento", retrasando el inicio real del cronometro y generando un incumplimiento no detectado a tiempo | Legal | Dos campos separados y obligatorios, con texto de ayuda que da ejemplos concretos; si la fecha de conocimiento es posterior a la de deteccion, exige justificacion visible; el sistema recomienda usar la fecha mas temprana disponible como criterio conservador |
| Enviar a los titulares el mismo contenido reservado para la ACE/FGR (por ejemplo, incluir las acciones correctivas internas) | Legal | Generacion automatica de dos plantillas separadas a partir de los mismos campos base, con el contenido de "acciones correctivas inmediatas" excluido por diseno de la plantilla de titulares (OBL-INC-03) |
| Que el sistema, o un usuario apurado, trate el criterio de horas corridas como si fuera la unica interpretacion legal correcta | Legal | El criterio se muestra siempre con la advertencia de incertidumbre (texto estandar de `04_objetivo_exacto_del_producto.md` 1.3); cambiarlo exige justificacion visible en el historial |
| Abandono del formulario de registro del incidente por su extension y complejidad, justo cuando la urgencia es maxima | UX | El registro inicial (estado Reportado) exige solo 3 campos minimos (titulo, fecha de deteccion, quien reporta); el resto de los campos se piden progresivamente conforme avanza el estado, no todos de una vez |
| Calcular mal el plazo de 72 horas por usar un calendario de dias/horas habiles desactualizado o incorrecto | Operativo | El cronometro de 72 horas usa por defecto horas corridas (no depende de dias habiles ni asuetos); si la empresa cambia el criterio a horas habiles, consulta el mismo servicio central de MOD-023 que usan ARCO-POL y el Procedimiento Sancionador, evitando un calculo propio inconsistente |
| Exposicion de datos personales sensibles de los titulares afectados dentro del propio expediente del incidente (el lugar donde mas se concentra el riesgo, porque describe exactamente que se filtro) | Seguridad y privacidad | El expediente registra categorias, cantidades y referencias, no una copia de la base de datos comprometida; los adjuntos puntuales llevan controles reforzados (cifrado, acceso restringido al equipo del incidente, ver seccion D) |
| Que un usuario cierre un incidente sin dejar constancia de por que se decidio no notificar, dificultando la defensa de la empresa ante una investigacion posterior de la ACE | Legal / operativo | Campo de justificacion obligatorio para el estado "Cierre sin notificacion externa (justificado)", con el responsable de la decision identificado de forma automatica (D.5) |
| Que el sistema decida por si mismo si hubo o no una vulneracion de datos personales, dejando a la empresa sin margen de revision | Legal | Toda calificacion de "es vulneracion" y de "existe riesgo" es una decision humana explicita con justificacion obligatoria (seccion H); el sistema nunca la infiere ni la cierra automaticamente |
| Que la relacion con el proveedor de origen del incidente quede documentada de forma incompleta, dificultando saber si el proveedor cumplio su plazo contractual de aviso | Operativo | Campo de referencia al proveedor (D.1) y alerta especifica si no hay evidencia de aviso del proveedor dentro del plazo pactado (seccion I); marcado como relacion informativa, no como dependencia estructural del modulo (ver nota de la seccion L) |

---

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Registro del incidente y flujo completo de estados (Reportado a Cierre) | X | | | | Nucleo del modulo; sin esto no existe gestion de incidentes. Modulo clasificado MUST HAVE en `mapa_modulos.json` |
| Dos cronometros de 72 horas en paralelo (notificacion e inicio de revision), con criterio de horas corridas por defecto | X | | | | Cubre OBL-INC-01 y OBL-INC-02, el plazo mas critico y visible de todo el corpus juridico (`02_validacion_de_la_idea.md` 2.1) |
| Plantillas diferenciadas de notificacion a ACE/FGR y a titulares | X | | | | Cubre OBL-INC-03 de forma directa; sin diferenciacion, la empresa arriesga incluir contenido indebido en la notificacion a titulares |
| Documentacion obligatoria del expediente con bloqueo si hay riesgo y faltan campos | X | | | | Cubre OBL-INC-04, obligacion sin condicion; es la base probatoria del modulo |
| Checklist de las 72 horas | X | | | | Herramienta operativa central para el usuario no especialista, alineada con el objetivo del producto (`04_objetivo_exacto_del_producto.md`) |
| Vinculo con el catalogo de controles de MOD-015 para medidas correctivas | X | | | | MOD-015 es MUST HAVE y comparte la entidad Control; el vinculo evita duplicar el registro de controles |
| Constancia de envio con verificacion de integridad (hash) | X | | | | Alineado con el anti-feature 25 de `22_anti_features.md`; sin esto, la evidencia de notificacion es impugnable |
| Alertas de cronometro (WARNING, CRITICAL, vencido) por plataforma y correo | X | | | | Canales basicos MUST HAVE segun la clasificacion general de MOD-022 en `06_mapa_definitivo_de_modulos.md` |
| Referencia informativa al proveedor/encargado de origen y su plazo pactado de aviso | | X | | | Util pero no bloqueante para el MVP: la mayoria de incidentes en el primer ano de un cliente pyme son de origen interno; se puede operar sin este enlace al inicio |
| Creacion automatica de tarea de EIPD hacia MOD-014 | | X | | | Depende de que MOD-014 exista con su cuestionario de scoring, y MOD-014 mismo es SHOULD HAVE; mientras tanto, la tarea se crea igual mas generica (ver seccion L) |
| Flujo condicional completo del Decreto 143 (reporte adicional de infraestructura critica) | | X | | | OBL-INC-05 es CONDICIONAL y solo aplica a un subconjunto muy pequeno de clientes calificados formalmente por la ACE; el campo esta disponible desde el MVP, pero el flujo operativo completo (evidencia especifica, plantilla propia) puede madurar despues |
| Alertas por canales adicionales (SMS, WhatsApp, Teams, Slack) para escalamiento critico | | | X | | Depende de la disponibilidad de esos canales en MOD-022, que los deja para V1/V2 segun demanda real de los primeros clientes |
| Dashboard comparativo de incidentes por proveedor a lo largo del tiempo | | | X | | Analitica de valor agregado, no bloqueante para operar un caso individual |
| Reapertura con flujo guiado especifico (por ejemplo, distinto segun el motivo de reapertura) | | | X | | La reapertura basica (con justificacion, sin sobrescribir el historial) ya cubre la necesidad legal minima desde el MVP |
| Integracion bidireccional con el canal oficial de la ACE (cuando la ACE lo habilite formalmente) | | | | X | La ACE aun no tiene un canal formal habilitado para esto, segun `22_anti_features.md` item 13; hoy la notificacion se documenta como envio por el medio disponible |

**Version minima vendible del modulo:** el MVP de MOD-013 es el flujo completo de un incidente con origen interno (sin dependencia obligatoria de Proveedores ni de Decreto 143), con los dos cronometros de 72 horas, las plantillas diferenciadas de notificacion, la documentacion obligatoria del expediente y las alertas basicas por plataforma y correo. Esto ya cubre, de forma completa, las cinco obligaciones propietarias del modulo (OBL-INC-01 a 05, la ultima solo si aplica) y es suficiente para que una empresa sin abogado ni DPO dedicado pueda gestionar un incidente real desde el primer dia de uso del sistema.

---

## R. Ayuda contextual (complemento obligatorio)

### R.1 Vulneracion de seguridad de datos personales

**Que es:** cualquier dano, perdida, alteracion, destruccion, acceso no autorizado o uso indebido de datos personales, incluso si fue accidental (por ejemplo, un empleado que pierde una laptop con datos de clientes, o alguien que entra sin permiso a un sistema).

**Por que tengo que hacer esto:** porque la ley le da a su empresa solo 72 horas desde que se entera para avisar a la autoridad y a las personas afectadas; entre mas rapido lo registre y clasifique, menos riesgo de que se le pase el plazo.

**Fundamento:** Art. 25 de la Ley para la Proteccion de Datos Personales (Decreto Legislativo 144); OBL-INC-01.

**Cuando necesito ayuda juridica:** cuando no esta seguro si lo que paso realmente cuenta como una vulneracion de datos personales, o cuando el caso involucra datos muy sensibles (salud, biometria, menores de edad).

### R.2 Las 72 horas (dos cronometros distintos)

**Que es:** la ley le exige dos cosas dentro de las mismas 72 horas desde que supo del incidente: (1) notificar a la ACE, a la Fiscalia y a las personas afectadas, y (2) empezar (no necesariamente terminar) una revision a fondo de lo que paso. El sistema los muestra como dos cronometros separados porque son dos obligaciones distintas.

**Por que tengo que hacer esto:** porque si se le pasa cualquiera de los dos plazos, su empresa queda expuesta a una infraccion, aunque haya resuelto el problema tecnico rapidamente.

**Fundamento:** Art. 25, primer y segundo inciso; OBL-INC-01 y OBL-INC-02.

**Cuando necesito ayuda juridica:** si a las 72 horas todavia no tiene toda la informacion necesaria para notificar con certeza, o si duda si el plazo se cuenta en horas corridas o solo en horas habiles (esto no esta resuelto de forma clara en la ley).

### R.3 Fecha de conocimiento (cuando empieza a correr el plazo)

**Que es:** el momento en que la persona responsable de su empresa confirmo, con certeza razonable, que ocurrio una vulneracion de datos personales. No es necesariamente el mismo momento en que alguien noto por primera vez que algo raro pasaba (eso es la "fecha de deteccion"). [Definicion operativa propuesta por el producto: la ley no define expresamente el momento de "conocimiento"; el sistema recomienda usar el momento mas temprano en que una persona con responsabilidad sobre el caso pudo razonablemente concluir que se trataba de una vulneracion, no el momento en que se termino de investigar a fondo.]

**Por que tengo que hacer esto:** porque de esta fecha depende cuando vencen las 72 horas; si la registra mas tarde de lo real, corre el riesgo de que el plazo ya haya vencido sin que su empresa lo supiera.

**Fundamento:** Art. 25 ("desde que se tuvo conocimiento de la vulneracion"); OBL-INC-01, OBL-INC-02. La definicion operativa de "conocimiento" usada por el sistema es una decision de producto, no un criterio fijado expresamente por la ley.

**Cuando necesito ayuda juridica:** siempre que exista duda razonable sobre cuando su empresa "supo" del incidente, especialmente si hay varias fechas posibles (por ejemplo, una alerta automatica versus la confirmacion humana de que era real).

### R.4 Contenido de la notificacion (diferente para la ACE/Fiscalia y para las personas afectadas)

**Que es:** la ley exige que la notificacion a la ACE y a la Fiscalia incluya cinco elementos (que paso, que datos se vieron afectados, que hizo su empresa de inmediato, que le recomienda a las personas afectadas, y como contactarlos para mas informacion), pero a las personas afectadas solo se les debe dar cuatro de esos cinco elementos: se omite el detalle de las acciones correctivas internas de su empresa.

**Por que tengo que hacer esto:** para no compartir con el publico informacion que la ley reserva para la autoridad, y para asegurarse de que la autoridad reciba todo lo que exige la ley.

**Fundamento:** Art. 25, incisos 3 y 4; OBL-INC-03.

**Cuando necesito ayuda juridica:** si no esta seguro de como redactar alguno de los cinco elementos sin comprometer informacion sensible de su empresa o sin minimizar el riesgo real para las personas afectadas.

### R.5 Documentacion obligatoria del expediente

**Que es:** su empresa debe guardar un registro escrito de toda vulneracion que genere un riesgo para la seguridad de los datos personales, aunque decida que no era necesario notificarla externamente. Ese registro debe tener, al menos, fecha, motivo, hechos, efectos y las medidas correctivas que tomo.

**Por que tengo que hacer esto:** porque la ACE puede pedirle este expediente en cualquier momento, incluso anos despues, y sin el no puede demostrar que actuo correctamente.

**Fundamento:** Art. 25, inciso final; OBL-INC-04.

**Cuando necesito ayuda juridica:** si duda de si el caso concreto "genera un riesgo" o no, porque de esa calificacion depende si el expediente completo es obligatorio.

### R.6 Operador de infraestructura critica (Decreto 143 de Ciberseguridad)

**Que es:** una categoria especial que la Agencia de Ciberseguridad del Estado (ACE) asigna formalmente, mediante resolucion, a ciertas entidades cuya operacion es considerada critica para el pais. Si su empresa tiene esa calificacion, un incidente de ciberseguridad puede generarle un deber adicional de reporte, distinto del deber de notificar la vulneracion de datos personales.

**Por que tengo que hacer esto:** porque este deber adicional no depende de que haya datos personales involucrados, sino de la calificacion de su empresa como infraestructura critica; si aplica, es independiente del cronometro de 72 horas de este modulo.

**Fundamento:** Ley de Ciberseguridad y Seguridad de la Informacion (Decreto Legislativo 143), Art. 6 lit. f-g, en relacion con Art. 2 y Art. 8 lit. f-g; OBL-INC-05.

**Cuando necesito ayuda juridica:** siempre, para confirmar si su empresa efectivamente tiene esta calificacion (el sistema nunca se la asigna por su cuenta) y que debe reportar exactamente.

---

## Notas finales y desacuerdos con el mapa

1. **Relacion con MOD-009 Proveedores y Encargados.** `mapa_modulos.json` no lista a MOD-009 dentro de `depende_de` ni de `alimenta_a` de MOD-013, pero esta ficha modela una referencia informativa desde el incidente hacia el proveedor de origen (campo "Proveedor/Encargado relacionado", seccion D.1; alerta especifica, seccion I), porque: (a) la documentacion obligatoria del expediente (OBL-INC-04) exige registrar la causa y los hechos relacionados, que con frecuencia incluyen a un proveedor; y (b) el contenido minimo recomendado del contrato con el encargado (`sweep_encargados_transferencias.md` seccion 5.6) incluye especificamente una clausula de aviso de incidentes con un plazo interno sugerido de 24 horas para que la empresa aun pueda cumplir sus propias 72 horas. Se recomienda al equipo que mantiene `06_mapa_definitivo_de_modulos.md` y `mapa_modulos.json` evaluar si esta relacion informativa debe elevarse a una entrada formal en `depende_de` (entrada, de solo lectura, sin bloquear el flujo si MOD-009 no esta disponible) en una proxima revision del mapa.

2. **Doble estado de la reforma 659.** Se confirma la nota de `mapa_modulos.json` ("No aplica directamente"): el Art. 25 LPDP, base legal de todas las obligaciones propietarias de este modulo, atribuye el deber de notificar al "responsable" del tratamiento (la empresa), no literalmente al "delegado" como si lo hacen los Arts. 18, 19, 21 y 30. Por eso este modulo no depende de la bandera de doble estado de MOD-024 para sus obligaciones sustantivas. Se mantiene, sin embargo, una dependencia de producto (no legal) en el rol que aprueba y envia la notificacion (hoy, tipicamente el Delegado, por ser el enlace institucional con la Direccion de Proteccion de Datos de la ACE segun el Art. 29 de los Lineamientos DPO); si el estado FUTURO de la reforma se activa, ese rol pasaria al "Responsable interno" configurable de MOD-002, sin que cambie ninguna de las cinco obligaciones propietarias de este modulo.

3. **Definicion operativa de "conocimiento" (seccion R.3).** No existe en el corpus juridico revisado (LPDP, Politicas ACE, Lineamientos DPO, Normativa Sancionadora) una definicion expresa de cuando se considera que el responsable "tuvo conocimiento" de una vulneracion. La definicion operativa propuesta en esta ficha (el momento mas temprano en que una persona con responsabilidad sobre el caso pudo razonablemente concluir que se trataba de una vulneracion) es una decision de producto que reduce el riesgo de la empresa al adoptar el criterio mas conservador, coherente con el mismo enfoque ya adoptado para el computo en horas corridas (decision 2.7.11 de `02_validacion_de_la_idea.md`), pero requiere validacion de asesoria legal antes de presentarse como un criterio definitivo del producto.

4. **Alcance de la "revision exhaustiva" del proveedor.** El plazo interno sugerido de 24 horas para que un proveedor avise a la empresa de un incidente (para que esta aun pueda cumplir sus 72 horas) proviene de `sweep_encargados_transferencias.md`, una fuente de analisis juridico (RECOMENDADO, sin norma expresa que fije ese numero). Esta ficha lo usa solo como referencia informativa en la alerta de la seccion I, nunca como un plazo legal exigible por si mismo; el contrato especifico de cada proveedor es el que fija el plazo real aplicable.

Ninguna de las notas anteriores contradice una obligacion legal ya verificada en `matriz_obligaciones.json`; son observaciones de coherencia entre documentos de la fase de validacion y precisiones sobre los limites de lo que la ley resuelve expresamente frente a lo que queda como decision de producto.
