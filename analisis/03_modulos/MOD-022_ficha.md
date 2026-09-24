# MODULO: Notificaciones

Codigo corto del modulo: MOD-022
Clasificacion global del modulo: MUST HAVE
Obligaciones que cubre: ninguna obligacion propia ni colaboradora declarada. `mapa_modulos.json` registra para MOD-022 `obligaciones_propietarias: []` y `obligaciones_colaboradoras: []`; a diferencia de MOD-021 Centro de Tareas (que si figura como colaborador expreso de OBL-INC-01, OBL-PLAZO-01, OBL-SANC-03, OBL-SANC-05 y OBL-SANC-06 en ese mismo archivo), MOD-022 no aparece como colaborador de ningun OBL-ID en la matriz. Esto es consistente con `06_mapa_definitivo_de_modulos.md`, seccion 2, principio 5: "los modulos transversales nunca son propietarios de una obligacion de negocio... MOD-021, MOD-022, MOD-025 y MOD-026 no poseen ninguna obligacion propia". MOD-022 sostiene de forma indirecta el cumplimiento de plazo de numerosas obligaciones (entre otras: OBL-INC-01 Art. 25, OBL-ARCO-08 Art. 18, OBL-ARCO-09 Art. 19, OBL-ARCO-10 Art. 20, OBL-ARCO-11 Art. 21 inc. 3, OBL-CONS-03 Art. 30, OBL-DPO-03 Art. 10 Lineamientos DPO, OBL-DPO-07 Art. 30 Lineamientos DPO, OBL-SANC-05 Art. 21 Normativa PAS, OBL-SANC-06 Art. 44 Normativa PAS, OBL-PLAZO-01 y OBL-PLAZO-02) al entregar la alerta que el modulo propietario correspondiente (o MOD-021/MOD-023 en su representacion) genera; el fundamento juridico, el estado del expediente y la decision de fondo siguen perteneciendo siempre a ese modulo propietario, nunca a MOD-022 (ver seccion A).

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (sin codigo, sin SQL, sin APIs, sin stack, sin infraestructura).

Fuentes usadas para esta ficha: `00_contexto_para_agentes.md`; `00_prompt_analisis_funcional.md`; `00_plantilla_ficha_modulo.md`; `02_validacion/mapa_modulos.json` (entrada MOD-022 y las 25 entradas restantes, para el grafo `depende_de`/`alimenta_a`); `02_validacion/06_mapa_definitivo_de_modulos.md` (secciones 1, 2, 3, 4, 6, 6.1 y 7); `01_legal/matriz_obligaciones.json` (registros OBL-INC-01, OBL-ARCO-08, OBL-ARCO-09, OBL-ARCO-10, OBL-ARCO-11, OBL-ARCO-14, OBL-CONS-03, OBL-DPO-03, OBL-DPO-05, OBL-DPO-07, OBL-PLAZO-01, OBL-PLAZO-02, OBL-SANC-05, OBL-SANC-06, OBL-AUD-01, OBL-PRIN-03); `01_legal/03_hallazgos_regulatorios.md` (seccion 9, punto 1, sobre el computo de las 72 horas); `02_validacion/02_validacion_de_la_idea.md` (secciones 2.3, 2.5, 2.6, 2.7, en particular las decisiones 15, 22 y 24); `02_validacion/04_objetivo_exacto_del_producto.md` (secciones 1.1 a 1.3); `02_validacion/05_tipos_de_usuario.md` (secciones 5.1 a 5.4, los 12 roles estandar); `02_validacion/22_anti_features.md` (items 8, 9, 19, 22, 25); `02_validacion/lente_faltantes.md` y `lente_inconsistencias.md` (sin hallazgos especificos adicionales sobre MOD-022 mas alla de lo ya cubierto por la seccion 4 regla 2 del mapa definitivo); `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md`, secciones 16 (Centro de tareas) y 25 (Incidentes: canales de alerta), tratadas como hipotesis, no como decisiones; y las 18 fichas ya redactadas de `03_modulos/` en el momento de escribir esta ficha (MOD-001 a MOD-016, MOD-018, MOD-021; verificado por orden de escritura del sistema de archivos: `MOD-019_ficha.md` y `MOD-025_ficha.md` se redactaron despues de esta ficha, no antes, por lo que no formaban parte de las fuentes disponibles en ese momento), leidas integramente en su seccion I (Alertas) y buscadas con `grep -n "MOD-022"` para relevar sus expectativas hacia este modulo (ver seccion L y Nota final); en una revision posterior de esta misma ficha (correccion adversarial, misma fecha de elaboracion) se incorporo ademas `MOD-019_ficha.md`, ya redactada para entonces, cuya seccion E declara una expectativa expresa hacia MOD-022 (ver seccion I.1 y Nota final, punto 1), y se confirmo que `MOD-025_ficha.md` no aporta alertas adicionales, pues su propia seccion I declara "No aplica" y remite a la clasificacion de MOD-022 como modulo terminal de lectura (linea 359 de esta ficha). Como modelo de estilo y profundidad se usaron completas `MOD-021_ficha.md` y `MOD-013_ficha.md`.

---

## A. Proposito

- **Por que existe.** Es el unico lugar del sistema que decide como, a quien, con que prioridad y con que frecuencia se avisa de un evento que ya ocurrio en otro modulo: una tarea proxima a vencer, un cronometro legal corriendo, una aprobacion pendiente, un documento por publicar, un cambio de regimen normativo. Ningun modulo de recorrido mantiene su propio mecanismo de envio de avisos; todos entregan el evento y MOD-022 resuelve el resto (`06_mapa_definitivo_de_modulos.md`, seccion 4, regla de conexion 2: "MOD-022 Notificaciones solo reacciona a eventos que le entregan MOD-021 y MOD-023; ningun modulo de recorrido envia notificaciones por su cuenta").
- **Que problema resuelve para la empresa.** Sin este modulo, cada plazo legal (los 20 mas 20 dias habiles del Art. 20 para ARCO-POL, las 72 horas del Art. 25 para vulneraciones, los 15 dias habiles del Art. 10 Lineamientos DPO para comunicar el nombramiento del Delegado, y muchos otros) dependeria de que alguien recuerde entrar a mirar el sistema. Esa dependencia de la memoria humana es exactamente el riesgo que `06_mapa_definitivo_de_modulos.md` (seccion 4, tabla "que aportaria si faltara") identifica para este modulo: "los plazos legales... dependerian de que alguien recuerde entrar a mirar". La persona designada (que normalmente no es abogada ni tiene equipo de privacidad dedicado, ver `05_tipos_de_usuario.md`) necesita que el sistema le avise de forma activa, sin tener que revisar cada modulo por separado.
- **Que obligacion u obligaciones cubre.** Ninguna con OBL-ID propio (ver encabezado). MOD-022 es, en cambio, el mecanismo comun por el que se hacen visibles a tiempo los plazos de las obligaciones que otros modulos gobiernan: OBL-INC-01/02 (Art. 25, 72 horas), OBL-ARCO-08 (Art. 18), OBL-ARCO-09 (Art. 19), OBL-ARCO-10 (Art. 20) y OBL-ARCO-11 (Art. 21 inc. 3) de la LPDP (plazos de 5, 10 y 20+20 dias habiles), mas OBL-ARCO-14 (Art. 33 inc. 4 de los Lineamientos para el Delegado de Proteccion de Datos Personales, ACE, norma distinta de la LPDP), OBL-CONS-03 (Art. 30, revocacion 5+5 dias), OBL-DPO-03/05/07 (Lineamientos DPO, 15 dias habiles, capacitacion anual, informe semestral), OBL-SANC-05/06 (Normativa PAS, 5 y 15 dias habiles), OBL-AUD-01 (Art. 8 lit. b Politicas ACE, periodicidad anual) y OBL-PLAZO-01/02 (el motor de plazos que MOD-023 calcula y cuyo vencimiento MOD-022 anuncia).
- **Que valor aporta.**
  - *Operativo*: un unico motor de reglas de aviso (destinatario, canal, frecuencia, escalamiento) en vez de que cada modulo reinvente su propia logica de "a quien le aviso y cuando"; esto evita, ademas, que la misma persona reciba el mismo aviso duplicado por dos vias distintas.
  - *Anti-fatiga*: resumenes, deduplicacion y horario silencioso para todo lo que no sea CRITICAL, para que la bandeja no se vuelva ruido que la persona termine ignorando (riesgo de UX explicito, ver seccion P).
  - *Probatorio*: cada notificacion generada, enviada, entregada, leida, acusada o escalada queda registrada con fecha y hora, lo que sirve como evidencia de que la organizacion fue alertada de un plazo, aunque no pruebe por si sola que la obligacion de fondo se resolvio correctamente (ver seccion J).
  - *Reduccion de riesgo*: el piso minimo de alertas de plazos legales nunca se puede apagar (seccion G y H), de modo que ninguna empresa cliente pueda, por descuido o por configuracion, dejar de recibir el aviso de un plazo OBLIGATORIO.
- **Que NO hace este modulo (limites explicitos).**
  - No decide el fundamento legal, el contenido sustantivo ni el estado de ningun expediente: los hereda siempre del modulo de origen (MOD-011, MOD-013, MOD-002, MOD-021, etc.); MOD-022 nunca interpreta ni resuelve una obligacion.
  - No calcula plazos por si mismo: siempre consulta o recibe el resultado ya calculado por MOD-023 Calendario y Motor de Plazos (regla de conexion 3 del mapa definitivo); MOD-022 nunca implementa su propia cuenta de dias u horas habiles.
  - No crea tareas: si un evento requiere una accion con responsable y fecha, esa tarea vive en MOD-021; MOD-022 solo avisa de lo que ya existe alli (o de lo que MOD-023 calculo), nunca abre un pendiente nuevo por su cuenta.
  - No ejecuta ni redacta la comunicacion formal a un titular, a la ACE o a la Fiscalia General de la Republica: esos actos (por ejemplo, la notificacion de una vulneracion del Art. 25, o la respuesta a una solicitud ARCO-POL) son documentos sustantivos que MOD-011 y MOD-013 generan y controlan por si mismos, con su propio flujo de aprobacion; MOD-022 gestiona unicamente avisos **internos** a usuarios de la organizacion cliente sobre esos eventos (por ejemplo, "faltan 6 horas para el vencimiento del plazo de notificacion"), nunca el envio externo mismo. Esta frontera se detalla en la seccion A.1 y se confirma de forma expresa en `MOD-013_ficha.md`, seccion L: "MOD-022 Notificaciones: alertas internas de cronometro y escalamiento (distinto de la notificacion externa a la ACE/FGR/titulares, que es un acto sustantivo del propio modulo, no una alerta)".
  - No decide si la reforma 659 esta vigente: consulta la bandera unica de MOD-024 solo quien alimenta ese evento (via MOD-021, que a su vez consulta a MOD-024), y solo reacciona a el.
  - No almacena en el cuerpo de un correo o mensaje ningun dato personal de un titular ni el detalle sustantivo de un incidente: el mensaje enviado fuera de la plataforma (correo y, en el futuro, otros canales) contiene solo el aviso generico y un enlace de acceso autenticado a la plataforma, nunca el contenido del caso (`22_anti_features.md`, items 8 y 9; ver seccion D).
  - No es un CRM de mensajeria ni un canal de marketing: solo entrega avisos ligados al programa de proteccion de datos (tareas, plazos, aprobaciones, cambios de estado normativo), nunca comunicacion comercial (`22_anti_features.md`, item 1, por analogia).

### A.1 Frontera entre aviso interno (MOD-022) y comunicacion formal externa (MOD-011 / MOD-013)

Esta frontera es la pieza de diseno mas sensible del modulo y se define de forma expresa porque el documento maestro (secciones 16 y 25) no la traza:

- **MOD-022 gestiona exclusivamente avisos internos** dirigidos a usuarios de la organizacion cliente (los 12 roles estandar de `05_tipos_de_usuario.md`, seccion 5.3, salvo el rol Titular). Ejemplos: "falta 1 dia habil para el vencimiento de la notificacion de la vulneracion", "la respuesta ARCO-POL esta pendiente de aprobacion del Delegado".
- **La comunicacion formal a un titular, a la ACE o a la Fiscalia es un acto sustantivo del modulo propietario del expediente, nunca de MOD-022.** MOD-011 genera y controla la respuesta ARCO-POL al titular (incluida su notificacion de denegatoria, Art. 22) y la notificacion a receptores (Art. 21 inc. 3). MOD-013 genera y controla la notificacion de la vulneracion a la ACE, a la Fiscalia y a los titulares (Art. 25). Ambos actos tienen su propio contenido, su propia Aprobacion (via MOD-021) y su propia evidencia de envio (via MOD-019); MOD-022 nunca los redacta ni los emite, solo avisa internamente de que el plazo para hacerlo se acerca o vencio.
- **Caso ya resuelto por una ficha existente: MOD-012 Portal del Titular.** `MOD-012_ficha.md`, seccion L, deja constancia de una "arista faltante hacia MOD-022": el Portal necesita enviar al titular externo un codigo de verificacion de un solo uso y un aviso de actualizacion de estado de su solicitud, y observa que ni `mapa_modulos.json` ni la ficha resumida de MOD-022 en `06_mapa_definitivo_de_modulos.md` declaran esa arista, preguntando si el envio se modela como evento de MOD-011 o si conviene anadir la arista. Esta ficha resuelve la pregunta: **esos dos correos al titular no son Notification de MOD-022, precisamente porque MOD-022 gestiona solo avisos internos a usuarios de la organizacion, nunca comunicaciones al titular externo.** Se modelan como actos propios de MOD-011 (el expediente ARCO-POL es siempre suyo, incluso cuando el canal de entrada o consulta es el Portal, MOD-012, que depende de MOD-011 segun su propio `depende_de`), ejecutados por el canal que corresponda dentro de MOD-011/MOD-012. No hace falta anadir una arista `depende_de` de MOD-012 hacia MOD-022 en `mapa_modulos.json`: el `depende_de` declarado de MOD-022 (`MOD-021, MOD-023, MOD-011, MOD-013`) ya es correcto tal como esta, y no debe modificarse (ver Nota final, punto 1).

---

## B. Usuarios

Roles estandar segun `02_validacion/05_tipos_de_usuario.md`, seccion 5.3 (los 12 roles del sistema).

| Rol | Para que usa MOD-022 |
|---|---|
| Administrador de la organizacion | Configura las reglas generales del modulo: destinatarios por defecto de cada familia de alerta, tiempos de escalamiento, horario silencioso, resumenes diario/semanal por usuario o por rol; consulta el historial completo de notificaciones enviadas como respaldo de gestion. |
| Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | Recibe las alertas de nivel WARNING, HIGH y CRITICAL relacionadas con los actos que la ley le atribuye hoy (prevencion, incompetencia, notificacion a receptores, revocacion, cronometro de 72 horas, comunicacion a la ACE); es destinatario habitual de escalamiento cuando el responsable original no actua a tiempo. |
| Responsable ARCO-POL / Responsable del tramite | Recibe las alertas de plazo de sus propios expedientes (prevencion, plazo general, notificacion a receptores) generadas a partir de las tareas de MOD-021 y los plazos de MOD-023. |
| Responsable Legal / Compliance | Recibe alertas de nivel HIGH/CRITICAL cuando un plazo legal esta por vencer sin resolucion, y las alertas de cambio de regimen normativo (reforma 659) que requieren revisar documentos o procesos. |
| Responsable de Seguridad / IT | Recibe el nivel mas alto de urgencia del sistema: el cronometro de 72 horas de un incidente en curso (CRITICAL), ademas de alertas de vencimiento de controles de seguridad. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Recibe las alertas ligadas a las tareas y aprobaciones de su propia area (por ejemplo, un consentimiento sensible incompleto, un contrato de proveedor por vencer). |
| Aprobador | Recibe la alerta "Aprobacion pendiente" cuando una tarea u objeto queda esperando su decision, con escalamiento si no responde dentro del plazo configurado. |
| Auditor (interno) | Solo lectura: consulta el historial de notificaciones (enviadas, entregadas, leidas, acusadas, escaladas) como evidencia de que la organizacion fue alertada a tiempo; no puede crear, silenciar ni modificar ninguna regla. |
| Auditor externo (invitado) | Acceso temporal de solo lectura al historial de notificaciones relacionado con el expediente o el periodo de la auditoria puntual para la que fue invitado. |
| Usuario de consulta / Colaborador | Recibe unicamente las notificaciones de las tareas puntuales que se le asignaron; no ve ni configura reglas generales. |
| Titular (formulario externo) | No es destinatario de ninguna Notification de MOD-022 (ver seccion A.1); su comunicacion vive en MOD-011/MOD-012. |
| Asesor externo invitado | Recibe unicamente la notificacion puntual de que se le asigno un caso o tarea especifica para su opinion, sin visibilidad del resto de reglas ni del historial general. |

---

## C. Permisos

Convencion: "Si" = permitido por defecto; "Si*" = permitido solo sobre las notificaciones propias o de su area; "No" = no permitido; "Doble control" = exige una segunda persona distinta (ver `05_tipos_de_usuario.md`, seccion 5.4). Las acciones de la plantilla (crear, modificar, aprobar, cerrar, eliminar/archivar, asignar, comentar, adjuntar evidencia) se adaptan al objeto real de este modulo: la Notification misma (append-only, nunca creada manualmente por un usuario) y la Regla de notificacion (configuracion de destinatarios, canal, escalamiento y resumenes).

| Accion | Administrador | Delegado / Resp. interno | Resp. ARCO-POL | Legal/Compliance | Seguridad/IT | Responsable de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver (sus propias notificaciones) | Si | Si | Si | Si | Si | Si | Si | Si (todas, solo lectura) | Si* (acotado a la auditoria) | Si* (solo las suyas) | Si* (solo la del caso invitado) |
| Ver el historial general de notificaciones de la organizacion | Si | Si* (las de su ambito legal) | No | Si* | No | No | No | Si | Si* (acotado) | No | No |
| Crear una Regla de notificacion (destinatario por rol, canal, escalamiento) | Si | No | No | No | No | No | No | No | No | No | No |
| Modificar una Regla de notificacion no obligatoria (por ejemplo, alertas informativas) | Si | Si* (solo reglas de su ambito) | No | No | No | No | No | No | No | No | No |
| Modificar el piso minimo de alertas de plazos legales (silenciar, alargar umbral por debajo del minimo de producto) | No (bloqueado por diseno, ver seccion H) | No | No | No | No | No | No | No | No | No | No |
| Configurar resumen diario o semanal (frecuencia de agregacion de lo no obligatorio) | Si (para toda la organizacion) | Si* (para si mismo) | Si* (para si mismo) | Si* (para si mismo) | Si* (para si mismo) | Si* (para si mismo) | Si* (para si mismo) | No | No | Si* (para si mismo) | No |
| Silenciar una alerta individual no obligatoria (marcar "no volver a avisar de este caso") | Si | Si* | Si* | Si* | Si* | Si* | Si* | No | No | Si* | No |
| Acusar recibo (obligatorio en notificaciones CRITICAL) | Si* (si es destinatario) | Si* | Si* | Si* | Si* | Si* | Si* | No (solo lectura) | No | Si* | No |
| Reenviar manualmente una notificacion cuya entrega fallo | Si | Si* | Si* | No | No | No | No | No | No | No | No |
| Reasignar el destinatario resuelto de una regla (por ejemplo, activar un suplente) | Si | Si* (para su propio rol) | No | No | No | No | No | No | No | No | No |
| Cerrar/archivar una notificacion (fuera de su ciclo normal) (ver nota 1 debajo de la tabla) | No aplica | No aplica | No aplica | No aplica | No aplica | No aplica | No aplica | No aplica | No aplica | No aplica | No aplica |
| Eliminar una notificacion o su historial | No (solo archivar; ver `22_anti_features.md`, item 19: el historial nunca se borra) | No | No | No | No | No | No | No | No | No | No |
| Exportar (reporte de notificaciones) | Si | Si* | Si* | Si* | Si* | No | No | Si | Si* | No | No |
| Comentar sobre una notificacion (ver nota 2 debajo de la tabla) | No aplica | No aplica | No aplica | No aplica | No aplica | No aplica | No aplica | No aplica | No aplica | No aplica | No aplica |
| Adjuntar evidencia manual de un intento fallido de aviso (por ejemplo, constancia de llamada cuando el correo rebota) | Si | Si* | Si* | No | No | No | No | No | No | No | No |

Nota 1 (fila "Cerrar/archivar una notificacion"): no aplica porque el archivado es automatico al completarse el ciclo (seccion F); ningun rol lo hace manualmente.
Nota 2 (fila "Comentar sobre una notificacion"): no aplica porque MOD-022 no tiene hilo de comentarios propio; el comentario relevante vive en la Tarea de MOD-021 que origino el evento.

**Separacion de funciones y doble control.** El piso minimo de alertas de plazos legales (seccion G y H) no admite excepcion de ningun rol, incluido el Administrador: no es una accion que requiera doble control porque directamente no es una accion disponible en el sistema (no hay boton para desactivarla). La unica accion de este modulo que exige doble control es **ampliar o reducir el umbral de escalamiento de una alerta CRITICAL ya en curso** (por ejemplo, alargar la ventana antes de escalar el cronometro de 72 horas a Legal/Compliance): el Administrador puede proponer el cambio, pero requiere confirmacion de una segunda persona con el rol Delegado/Responsable interno o Legal/Compliance antes de aplicarse, y el cambio queda registrado con ambas identidades. El rol Auditor (interno o externo) es siempre de solo lectura sobre este modulo, igual que en el resto del sistema (`05_tipos_de_usuario.md`, seccion 5.4).

---

## D. Informacion de entrada

MOD-022 administra una entidad principal, **Notificacion** (Notification, segun `mapa_modulos.json` y `06_mapa_definitivo_de_modulos.md`, seccion 7), mas dos catalogos de configuracion que la organizacion mantiene (Regla de notificacion y Preferencia de usuario), descritos al final de esta seccion.

### D.1 Campos de la Notificacion

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda que vera el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Familia de evento | Seleccion unica | Obligatorio | Catalogo cerrado: Tarea proxima a vencer, Tarea vencida, Aprobacion pendiente, Bloqueo prolongado, Cronometro legal critico (72h / 20+20 dias / 10 dias / 5 dias / 15 dias), Documento pendiente o por vencer, Consentimiento pendiente o incompleto, Control de seguridad por vencer, Contrato/proveedor por vencer, Transferencia sin confirmar o sin evaluacion, Riesgo/EIPD pendiente, Retencion/eliminacion pendiente, Auditoria de cumplimiento, Cambio de regimen normativo (reforma 659), Organizacional (estructura, roles, invitaciones), Sistema (fallo de entrega) | Debe existir en el catalogo; cada familia tiene un nivel por defecto (ver seccion I) | "Que tipo de aviso es este, para poder agruparlo y filtrarlo." | Buena practica (usabilidad); ver la tabla consolidada de la seccion I |
| Canal de entrada (via estructural) | Seleccion unica | Obligatorio (autogenerado) | Evento de Tarea (MOD-021), Evento de Plazo (MOD-023), Evento directo ARCO-POL (MOD-011), Evento directo Incidentes (MOD-013) | Debe coincidir con uno de los cuatro modulos declarados en `depende_de` de MOD-022 en `mapa_modulos.json`; ningun otro valor es valido | "Por donde llego este aviso al sistema de notificaciones (dato tecnico, no legal)." | Regla de conexion 2 del mapa definitivo; ver seccion A.1 y Nota final |
| Modulo de origen funcional | Referencia a otra entidad | Obligatorio (autogenerado) | Catalogo abierto: cualquier modulo operativo que definio la regla de negocio de la alerta (por ejemplo, MOD-008 para "Aviso de Privacidad sin publicar", aunque el Canal de entrada tecnico haya sido la Tarea de MOD-021 que ese evento genero) | Debe existir el modulo en el mapa | "De que parte del sistema viene este aviso, para poder ir directo a revisar el caso." | Buena practica (trazabilidad) |
| Objeto de origen | Referencia a otra entidad | Obligatorio | Tarea o Aprobacion de MOD-021, evento de calendario de MOD-023, expediente de MOD-011 o de MOD-013, segun el Canal de entrada | Debe existir el registro referenciado | "El caso exacto al que se refiere este aviso." | Buena practica; minimizacion de datos (ver mas abajo) |
| Obligacion relacionada | Referencia a otra entidad (lista) | Opcional; heredado del objeto de origen cuando este la trae | Lista de OBL-ID de `matriz_obligaciones.json` | Debe existir en la matriz | "El fundamento legal exacto detras de este aviso, si aplica." | OBL-ID correspondiente, mostrado como ayuda contextual (regla de oro de la plantilla) |
| Nivel | Seleccion unica | Obligatorio (autogenerado segun la familia y el disparador especifico) | INFO, WARNING, HIGH, CRITICAL | El nivel de una familia puede subir automaticamente al acercarse el vencimiento (por ejemplo, WARNING a HIGH a 5 dias, HIGH a CRITICAL a 24 horas), nunca bajar salvo que el evento de origen se resuelva | "Que tan urgente es este aviso." | Buena practica; ver seccion I |
| Titulo | Texto | Obligatorio (autogenerado a partir de una plantilla por familia) | Plantilla por familia, sin datos personales del titular | Maximo 140 caracteres | "Resumen corto de que paso." | Buena practica |
| Cuerpo del mensaje (version plataforma) | Texto largo | Obligatorio (autogenerado) | Plantilla por familia; puede incluir referencia al objeto de origen (por ejemplo, numero de expediente), nunca el dato personal del titular ni el detalle sustantivo de un incidente | No contiene datos personales de titulares; validacion automatica bloquea la generacion si la plantilla intenta insertar un campo marcado como dato personal en MOD-006 o MOD-011 | "Lo que vera dentro de la plataforma al abrir el aviso." | `22_anti_features.md`, items 8 y 9; ver seccion A |
| Cuerpo del mensaje (version correo u otro canal externo) | Texto largo | Obligatorio (autogenerado) cuando el canal resuelto incluye correo u otro canal externo | Plantilla reducida: aviso generico mas enlace de acceso autenticado a la plataforma, nunca el contenido del caso | No puede contener datos personales de titulares ni detalle sustantivo del caso; validacion automatica bloquea el envio si se detecta | "Lo que llegara a su correo (u otro canal externo): un aviso y un enlace, nunca el detalle del caso." | Frontera de privacidad de la seccion A; `22_anti_features.md`, items 8 y 9 |
| Destinatario resuelto | Referencia a otra entidad (lista de usuarios) | Obligatorio (autogenerado por la resolucion rol -> personas) | Usuarios activos de la organizacion con el rol configurado para esa familia de evento, mas su suplente si el titular no responde dentro del umbral | Debe existir al menos un destinatario resuelto; si el rol no tiene titular activo, se activa la alerta "Rol critico sin titular" (heredada de MOD-001) | "A quien se le esta avisando de esto." | Buena practica |
| Canal(es) resuelto(s) | Seleccion multiple | Obligatorio (autogenerado) | Plataforma, Correo electronico (MVP); Microsoft Teams, Slack, SMS, WhatsApp (evaluados para V1/V2, ver seccion Q) | El nivel CRITICAL siempre incluye Plataforma + Correo como minimo, sin excepcion configurable | "Por donde le llega este aviso." | Decision de alcance 2.7 de `02_validacion_de_la_idea.md` (canales basicos MUST HAVE) |
| Fecha y hora de generacion | Fecha (autogenerada) | Obligatorio | No aplica | No editable | "Cuando se genero este aviso." | Buena practica (trazabilidad) |
| Fecha y hora de envio por canal | Fecha (autogenerada, una por canal) | Obligatorio en cuanto se envia | No aplica | No editable | "Cuando se envio por cada canal." | Buena practica |
| Estado de entrega por canal | Seleccion unica (autogenerada) | Obligatorio | Pendiente de envio, Enviada, Entregada (si el canal lo confirma), Fallida, Reintentando | Un canal "Fallida" tras el maximo de reintentos configurado dispara la alerta de sistema (ver seccion I) | "Si el aviso realmente llego, cuando el canal puede confirmarlo." | Buena practica |
| Leida (en plataforma) | Booleano mas fecha (autogenerado) | Obligatorio | Si / No, con fecha de primera apertura | No editable manualmente por el usuario mas alla de abrir el aviso | "Si ya entro a ver este aviso dentro de la plataforma." | Buena practica |
| Acuse de recibo | Booleano mas fecha e identidad (autogenerado al confirmar) | Obligatorio para toda notificacion de nivel CRITICAL antes de considerarla resuelta; opcional en los demas niveles | Accion explicita "Confirmar que revise esto" dentro de la plataforma; la sola apertura del correo nunca cuenta como acuse (ver seccion H) | No editable una vez registrado | "Confirme que vio y entendio este aviso urgente. Para los avisos mas criticos, no basta con que el sistema detecte que abrio el correo: debe confirmarlo usted mismo dentro de la plataforma." | OBL-PRIN-03 (responsabilidad demostrada); ejemplo tipico: cronometro de 72 horas de OBL-INC-01 |
| Estado de escalamiento | Seleccion unica (autogenerado) | Obligatorio | No escalada, Escalada nivel 1, Escalada nivel 2, Escalada a Gerencia | Sigue la regla de escalamiento de la familia de evento (seccion I) | "Si este aviso ya se le mando tambien a un superior porque no hubo respuesta a tiempo." | Buena practica |
| Motivo de apagado | Texto (autogenerado) | Obligatorio cuando la notificacion pasa a Resuelta | Generado por el sistema segun la condicion "se apaga cuando" de la familia (seccion I) | No editable | "Por que dejo de repetirse este aviso." | Buena practica |
| Resumen aplicado | Booleano mas referencia al lote (autogenerado) | Obligatorio cuando la Preferencia de usuario agrupa la notificacion en un resumen diario o semanal | Referencia al envio agregado correspondiente | No aplica a notificaciones CRITICAL, que nunca se agrupan (ver seccion G) | "Si este aviso se le envio agrupado con otros en un resumen, en vez de solo." | Decision de alcance 2.7 (reglas anti-fatiga, ver seccion G) |

**Campos precargados desde otros modulos.** Familia de evento, Canal de entrada, Modulo de origen funcional, Objeto de origen, Obligacion relacionada y Nivel llegan siempre precargados desde el evento que dispara la notificacion (una Tarea o Aprobacion de MOD-021, un evento de plazo de MOD-023, o un evento directo de MOD-011/MOD-013). El Destinatario resuelto se calcula automaticamente segun la Regla de notificacion configurada para esa familia (rol por defecto mas suplente); un usuario nunca redacta el contenido de una Notification a mano.

**Minimizacion de datos personales.** La Notificacion nunca contiene el dato personal del titular ni el detalle sustantivo del caso, ni siquiera dentro de la version que se ve en plataforma: guarda una referencia al objeto de origen (por ejemplo, el numero de expediente ARCO-POL o el numero de caso de incidente) y dejar que quien reciba el aviso entre al expediente correspondiente, autenticado, para ver el detalle con los mismos permisos que ya tiene sobre ese modulo. La version enviada por un canal externo (correo y, en el futuro, otros canales) es aun mas restringida: solo el aviso generico y el enlace de acceso, nunca una referencia legible del caso, precisamente porque un canal externo (bandeja de correo, telefono) esta fuera del perimetro de control del sistema (`22_anti_features.md`, items 8 y 9).

### D.2 Catalogos de configuracion

**Regla de notificacion** (una por familia de evento, configurable por la organizacion salvo el piso minimo legal): Familia de evento | Rol(es) destinatario(s) por defecto | Regla de suplencia (a quien avisar si el titular del rol no responde en el umbral) | Canal(es) por nivel | Umbral de escalamiento por nivel | Frecuencia de repeticion | Si el piso minimo aplica (booleano, no editable cuando es Si).

**Preferencia de usuario** (configurable por cada usuario, solo sobre lo que no es obligatorio): Usuario | Resumen diario o semanal para niveles INFO/WARNING (no aplica a HIGH/CRITICAL) | Horario silencioso (rango horario en el que se retrasan los avisos no CRITICAL hasta el fin de ese horario) | Canales habilitados para si mismo, dentro de los que la organizacion tiene activados | Notificaciones individuales silenciadas manualmente (lista, nunca sobre familias con piso minimo legal).

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Notificacion enviada | Registro completo de la seccion D.1 | Registro en el sistema, mas mensaje en plataforma y, segun el canal resuelto, correo u otro canal | Al recibir un evento de MOD-021, MOD-023, MOD-011 o MOD-013 que coincide con una Regla de notificacion activa | Destinatario(s) resuelto(s) |
| Resumen diario o semanal | Lista agrupada de notificaciones INFO/WARNING pendientes o generadas en el periodo, por usuario | Mensaje unico de plataforma y correo | Segun la Preferencia de usuario configurada | El usuario que configuro el resumen |
| Evento de escalamiento | Identificador de la notificacion original, tiempo transcurrido sin respuesta, nuevo destinatario | Nueva Notificacion vinculada a la original | Segun el umbral de escalamiento de la familia (seccion I) | El destinatario de escalamiento (superior de area, Delegado, Administrador o Gerencia, segun la familia) |
| Confirmacion de acuse de recibo | Identidad, fecha y hora de quien confirmo haber visto una notificacion CRITICAL | Registro en el sistema, visible en el historial de la notificacion y del objeto de origen | Al confirmar el usuario dentro de la plataforma | MOD-019 Centro de Evidencias (lectura), el propio modulo de origen (por ejemplo, MOD-013 lo muestra en el expediente del incidente) |
| Alerta de entrega fallida | Notificacion cuyo canal externo (correo u otro) fallo tras el maximo de reintentos | Notificacion de sistema (nivel WARNING o HIGH segun la familia original) | Al agotarse los reintentos configurados | Administrador, y el destinatario original por el canal alternativo (plataforma) |
| Indicador "notificaciones enviadas / leidas / pendientes de acuse / escaladas" | Conteos por familia, por nivel y por destinatario | Datos agregados consumidos por MOD-020 | Actualizacion continua | MOD-020 Dashboard y Reportes, con vista por rol (seccion M) |
| Evento de auditoria | Accion, usuario o sistema, fecha y hora, valor anterior y nuevo | Registro en el AuditLog transversal | En cada generacion, envio, entrega, lectura, acuse, escalamiento o cambio de Regla de notificacion | MOD-019 Centro de Evidencias (lectura) |
| Reporte de notificaciones | Listado filtrable exportable | PDF, XLSX o CSV | Bajo demanda | Administrador, Delegado/Responsable interno, Legal/Compliance, Auditor |

---

## F. Workflow

### F.1 Diagrama de estados de la Notificacion

```
                    +---------------+
                    |   GENERADA    |  (evento recibido, mensaje compuesto)
                    +-------+-------+
                            |
                    se resuelve destinatario, canal y horario
                            v
                    +---------------+
                    |   EN ENVIO    |
                    +-------+-------+
                       /           \
              envio exitoso      falla el canal externo
                    v                   v
            +---------------+   +---------------+
            |   ENVIADA     |   |   FALLIDA      |
            +-------+-------+   +-------+--------+
                    |                   |
         el canal confirma       se reintenta hasta
         entrega (si aplica)     el maximo configurado
                    v                   |
            +---------------+          |  se agotan los reintentos
            |  ENTREGADA    |          v
            +-------+-------+   +----------------------+
                    |            | ALERTA DE SISTEMA    |
      se abre en plataforma      | (ver seccion E)      |
                    v            +----------------------+
            +---------------+
            |    LEIDA      |
            +-------+-------+
                    |
     si el nivel es CRITICAL, requiere accion explicita
                    v
            +---------------+
            |    ACUSADA    |  (obligatorio solo para CRITICAL)
            +-------+-------+
                    |
                    v
            +---------------+
            |   RESUELTA    |  (estado terminal, se archiva, nunca se borra)
            +---------------+

Bandera paralela, no excluyente con los estados anteriores (salvo RESUELTA):
  si transcurre el umbral de escalamiento sin que el destinatario responda
  (leer, acusar, o resolver el objeto de origen), la notificacion se marca
  ESCALADA y se genera una nueva Notificacion vinculada hacia el destinatario
  de escalamiento, sin que la original cambie de estado por eso.
```

### F.2 Tabla de transiciones

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (no existe) | MOD-021, MOD-023, MOD-011 o MOD-013 entregan un evento que coincide con una Regla de notificacion activa | El evento debe traer Familia, Objeto de origen y Nivel validos | Generada | Sistema (automatico) | Se compone el mensaje segun la plantilla de la familia; se registra evento de auditoria |
| Generada | El sistema resuelve destinatario(s) y canal(es) | Debe existir al menos un destinatario resuelto; si no lo hay, se dispara la alerta "Rol critico sin titular" (heredada de MOD-001) en vez de continuar | En envio | Sistema (automatico) | Se aplica horario silencioso si corresponde (se retrasa el envio de niveles no CRITICAL) |
| En envio | El canal confirma el envio | El canal esta disponible | Enviada | Sistema (automatico) | Se registra fecha y hora de envio por canal; evento de auditoria |
| En envio | El canal reporta error | Se reintenta segun politica configurable (por defecto 3 intentos con espera creciente) | Fallida | Sistema (automatico) | Se reintenta; si se agotan los reintentos, se genera la alerta de sistema de la seccion E |
| Enviada | El canal externo confirma entrega (cuando el canal lo permite) | No aplica a Plataforma (se considera entregada al enviarse) | Entregada | Sistema (automatico) | Se registra fecha y hora de entrega |
| Entregada (o Enviada, si el canal no confirma entrega) | El destinatario abre la notificacion dentro de la plataforma | El usuario debe estar autenticado | Leida | Destinatario resuelto | Se registra fecha y hora de primera lectura; evento de auditoria |
| Leida | El destinatario confirma explicitamente "Confirmar que revise esto" | Solo aplica y solo se exige para nivel CRITICAL; la apertura del correo nunca sustituye esta confirmacion (seccion H) | Acusada | Destinatario resuelto | Se registra identidad, fecha y hora del acuse; evento de auditoria; se notifica al modulo de origen (por ejemplo, MOD-013 marca el hito como confirmado internamente) |
| Leida (nivel INFO/WARNING/HIGH) | Ninguna accion adicional requerida | El nivel no exige acuse | Resuelta | Sistema (automatico), al resolverse el objeto de origen o al vencer su ciclo | Se archiva; el historial se conserva |
| Acusada (nivel CRITICAL) | El objeto de origen se resuelve (por ejemplo, la Tarea de notificacion externa de MOD-013 se marca Completada) | El evento de resolucion debe llegar desde el modulo de origen | Resuelta | Sistema (automatico) | Se archiva; el historial se conserva |
| Cualquier estado no terminal | Transcurre el umbral de escalamiento de la familia sin lectura, acuse o resolucion del objeto de origen | Umbral configurable por familia (seccion I); el piso minimo de las familias con plazo legal no puede desactivar el escalamiento | Se mantiene el estado, se agrega la bandera Escalada | Sistema (automatico) | Se genera una nueva Notificacion vinculada hacia el destinatario de escalamiento; evento de auditoria |
| Cualquier estado no terminal | El objeto de origen deja de aplicar (por ejemplo, la Tarea vinculada pasa a "No aplica" por el cambio de regimen de la reforma 659, via MOD-021) | Evento explicito del modulo de origen | Resuelta (con motivo "objeto de origen ya no aplica") | Sistema (automatico) | Se archiva sin mas repeticion; no se borra |

**Registros vinculados.** Ninguna Notificacion se elimina nunca; al llegar a Resuelta queda archivada con su historial completo. Cuando el objeto de origen se reabre (por ejemplo, una Tarea completada que se reabre en MOD-021), el modulo de origen puede disparar una nueva Generacion de Notificacion, pero la anterior conserva su propio historial sin alterarse.

---

## G. Automatizaciones

Todas las reglas siguientes son configurables por la organizacion (activar/desactivar la familia cuando no tiene piso minimo legal, ajustar destinatarios, canales y umbrales), salvo que se indique lo contrario.

| Disparador | Condicion | Accion |
|---|---|---|
| MOD-021 entrega un evento de Tarea o Aprobacion (creacion, proxima a vencer, vencida, bloqueada, aprobacion pendiente) | Existe una Regla de notificacion activa para esa familia | Generar la Notificacion, resolver destinatario(s) por rol y componer el mensaje segun la plantilla |
| MOD-023 entrega un evento de plazo (por ejemplo, "faltan 30 dias para la revision periodica de un contrato") sin que medie necesariamente una Tarea | Existe una Regla de notificacion activa para esa familia | Generar la Notificacion directamente, sin pasar por MOD-021 |
| MOD-011 o MOD-013 entregan un evento directo de cronometro (por ejemplo, "restan 6 horas del plazo de 72 horas") | El evento trae el Nivel ya calculado por el modulo de origen segun su propia tabla de alertas (seccion I de esas fichas) | Generar la Notificacion con Nivel CRITICAL y exigir acuse de recibo al resolverse |
| El rol destinatario resuelto para una notificacion no tiene ningun usuario activo | Se detecta al resolver destinatario | Generar en su lugar la alerta "Rol critico sin titular" (ver `MOD-001_ficha.md`, seccion I) dirigida al Administrador, y suspender el envio de la notificacion original hasta que se asigne el rol |
| El destinatario resuelto no responde (leer o acusar) dentro del umbral de escalamiento de su familia | La familia tiene una regla de escalamiento configurada | Marcar Escalada y generar una nueva Notificacion hacia el destinatario de escalamiento (seccion I) |
| Una notificacion es de nivel CRITICAL | Siempre | Exigir Canal Plataforma + Correo como minimo (no configurable a la baja), y exigir Acuse de recibo explicito antes de considerarla Resuelta |
| Una notificacion pertenece a una familia con piso minimo de plazo legal (ver seccion H) | Siempre | Ignorar cualquier intento de silenciarla o de excluirla de un resumen; se entrega siempre de forma individual e inmediata, nunca agrupada |
| Una notificacion es de nivel INFO o WARNING y el usuario tiene configurado un resumen diario o semanal | La familia no tiene piso minimo de plazo legal | Agregarla al proximo resumen en vez de enviarla de forma individual |
| Dos o mas notificaciones de la misma familia y el mismo objeto de origen se generarian en una ventana corta (por ejemplo, dos eventos de "proxima a vencer" del mismo plazo el mismo dia) | Regla de deduplicacion activa (por defecto, si) | Enviar una sola notificacion consolidada en vez de repetir el mismo aviso |
| Es horario silencioso configurado para el destinatario | La notificacion no es de nivel CRITICAL | Retrasar el envio hasta el fin del horario silencioso; las notificaciones CRITICAL nunca se retrasan por horario silencioso |
| El canal externo (correo u otro) falla al enviar | Se agota el numero de reintentos configurado (por defecto 3) | Generar la alerta de sistema "Entrega fallida" (seccion E) y notificar al Administrador por el canal Plataforma (que no depende de un canal externo) |
| MOD-024 activa el cambio de regimen de la reforma 659 y esa activacion llega como evento desde MOD-021 (que a su vez la recibe de MOD-024) | Existe una Regla de notificacion configurada para la familia "Cambio de regimen normativo" | Generar una Notificacion de nivel INFO hacia Delegado/Responsable interno, Legal/Compliance y Administrador |

---

## H. Decisiones que NO debe automatizar

- **Silenciar o excluir de un resumen cualquier familia de notificacion ligada a un piso minimo de plazo legal**, sin importar quien lo solicite ni el motivo alegado. Texto de advertencia: "Esta alerta corresponde a un plazo legal y no puede desactivarse ni agruparse en un resumen." Razon: el piso minimo existe precisamente para que ninguna empresa cliente pueda, por descuido, configuracion o presion interna, dejar de ser avisada de un plazo OBLIGATORIO (por ejemplo, las 72 horas de OBL-INC-01 o los 20+20 dias de OBL-ARCO-10); permitir una excepcion, aunque sea a pedido del Administrador, anularia el proposito mismo del modulo (`22_anti_features.md`, item 5, por analogia con no declarar cumplimiento legal: tampoco se declara "avisado" cuando no lo estuvo).
- **Decidir por si mismo que la sola apertura de un correo equivale al acuse de recibo exigido para una notificacion CRITICAL.** Texto de advertencia: "La apertura del correo no cuenta como confirmacion. Debe confirmar dentro de la plataforma que vio y entendio este aviso." Razon: el registro de apertura de un correo (cuando el proveedor de correo lo reporta) es una senal tecnica poco confiable y facil de falsear (por ejemplo, un cliente de correo que precarga imagenes automaticamente); la evidencia de que una persona identificada realmente atendio un aviso critico (por ejemplo, el cronometro de 72 horas) exige una accion explicita dentro del sistema, con identidad y fecha verificables (OBL-PRIN-03).
- **Redactar o enviar la comunicacion formal a un titular, a la ACE o a la Fiscalia en nombre de MOD-011 o MOD-013.** Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada." Razon: esos actos tienen su propio contenido sustantivo, su propia aprobacion y su propio fundamento legal (Arts. 21, 22 y 25 LPDP); MOD-022 solo avisa internamente de que el plazo para emitirlos se acerca, nunca sustituye ni acelera esa decision (ver seccion A.1).
- **Decidir por si mismo el destinatario de escalamiento cuando el rol configurado no tiene un suplente definido.** Texto de advertencia: "No hay una persona configurada para recibir este aviso si el responsable original no atiende. Configure un suplente o asignelo manualmente." Razon: elegir automaticamente a "alguien" dentro de la organizacion sin una regla explicita de suplencia podria entregar un aviso sensible (por ejemplo, sobre una vulneracion de seguridad) a una persona sin el rol ni la autorizacion adecuados; esta decision de a quien escalar le corresponde siempre al Administrador o al Delegado/Responsable interno, configurada por adelantado.
- **Interpretar la ausencia de acuse o de lectura de una notificacion CRITICAL como que la organizacion ya incumplio la obligacion subyacente.** Texto de advertencia: "El sistema registra que este aviso no fue confirmado a tiempo, pero no puede determinar si esto ya configura un incumplimiento sancionable. Consulte a su Delegado/Responsable interno o a asesoria especializada." Razon: MOD-022 solo puede constatar que un aviso no fue atendido, no evaluar la consecuencia juridica de esa demora, que depende del expediente completo en el modulo propietario (por ejemplo, MOD-013 para un incidente).
- **Eliminar en forma definitiva una notificacion o su historial**, incluso a pedido del Administrador. Texto de advertencia: "El historial de notificaciones no puede eliminarse; solo puede archivarse al resolverse." Razon: el historial de avisos entregados es parte de la evidencia de que la organizacion fue alertada a tiempo (OBL-PRIN-03) y del principio de no editar ni borrar la bitacora de auditoria (`22_anti_features.md`, item 19).
- **Incluir datos personales de un titular o el detalle sustantivo de un caso en el cuerpo de un mensaje enviado por un canal externo** (correo y, en el futuro, otros canales), aunque el usuario que configura la plantilla lo solicite. El sistema bloquea la generacion en vez de avisar y preguntar. Razon: un canal externo esta fuera del perimetro de control de la plataforma; es una regla de arquitectura de privacidad, no una decision caso por caso (`22_anti_features.md`, items 8 y 9).

---

## I. Alertas

Esta seccion cubre las alertas **propias del funcionamiento del modulo de Notificaciones** (su propia salud operativa), distintas de las decenas de familias de eventos que MOD-022 reenvia por cuenta de otros modulos (esas se documentan de forma consolidada en la seccion I.1, no aqui, porque no son "alertas de MOD-022 sobre si mismo" sino el contenido que MOD-022 entrega).

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia o repeticion | Escalamiento (a quien y cuando) | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Entrega fallida por canal externo | Se agotan los reintentos configurados (por defecto 3) para un canal externo (correo u otro) | WARNING (HIGH si la notificacion original era CRITICAL) | Administrador | Plataforma (el unico canal que no depende de si mismo) | Al agotarse los reintentos | Si la notificacion original era CRITICAL y sigue sin entregarse 1 hora despues, escala a Delegado/Responsable interno | El canal vuelve a confirmar entregas correctamente, o el Administrador reasigna el canal para ese destinatario |
| Rol critico sin titular para una familia con piso minimo legal | Se intenta resolver destinatario y el rol configurado no tiene usuario activo | CRITICAL | Administrador | Plataforma + correo | Inmediata, diaria mientras persista | A la vista de Gerencia del dashboard a las 48 horas | Se asigna un usuario activo a ese rol (coordina con la alerta homologa de `MOD-001_ficha.md`) |
| Notificacion CRITICAL sin acuse dentro del umbral | Transcurre el umbral configurado (por defecto la mitad del tiempo restante del plazo legal asociado) sin que se registre Acuse | HIGH, sube a CRITICAL si el plazo legal asociado esta a menos de 25% de su tiempo total | Destinatario original, mas el destinatario de escalamiento de su familia | Plataforma + correo (mas canal adicional si esta configurado) | Segun el ritmo de la familia de origen (por ejemplo, cada 2 horas para el cronometro de 72 horas) | Automatico segun la regla de escalamiento de la familia origen (ver seccion I.1) | Se registra el Acuse, o el objeto de origen se resuelve |
| Volumen inusual de notificaciones generadas | Se supera un umbral configurable de notificaciones en una ventana corta para la misma organizacion (posible mal funcionamiento de una regla o de un modulo de origen) | WARNING | Administrador | Plataforma | Una vez por evento detectado | A soporte del producto si se repite (fuera del alcance funcional de esta ficha) | El volumen vuelve a un rango normal |
| Regla de notificacion sin destinatario configurado tras un cambio de estructura organizativa | Se elimina o cambia el rol vinculado a una Regla activa | WARNING | Administrador | Plataforma | Una vez al detectarse | A los 7 dias sin corregir, sube a HIGH | Se reconfigura la Regla con un destinatario valido |

### I.1 Tabla consolidada de familias de alertas por modulo emisor

Esta tabla resume, para cada modulo que hoy tiene su propia seccion I de Alertas ya redactada, que familias de evento llegan a MOD-022 y por que canal estructural (Tarea/Aprobacion de MOD-021, evento de plazo de MOD-023, o evento directo de MOD-011/MOD-013, ver seccion D.1). Es el modelo unificado que exige el alcance de esta ficha: mismo tipo de evento, mismo esquema de nivel, misma logica de resolucion de destinatario, mismo criterio de canal por nivel para toda la plataforma, sin que cada modulo de origen reinvente sus propias reglas de aviso.

| Modulo emisor (origen funcional) | Familias de evento tipicas (ver detalle completo en la seccion I de cada ficha) | Niveles usados | Canal de entrada hacia MOD-022 |
|---|---|---|---|
| MOD-001 Organizacion y Personas | Organizacion incompleta, rol critico sin titular, invitacion pendiente, umbral de separacion de funciones, baja de unico titular de rol critico, estructura sin actualizar | INFO a CRITICAL | Evento de Tarea (MOD-021) para las ligadas a onboarding/invitaciones; evento directo de sistema para "rol critico sin titular" (mismo mecanismo que usa MOD-022 para su propia alerta homologa de la seccion I) |
| MOD-002 Delegado / Responsable Interno | Falta nombrar Delegado, notificacion interna (3 dias) y comunicacion a la ACE (15 dias) por vencer o vencidas, reverificacion trienal, capacitacion anual, informe semestral, sustituto no designado tras cese, cambio de regimen 659 | INFO a CRITICAL | Evento de Tarea (MOD-021), que aloja cada uno de estos plazos como Tarea con fecha calculada por MOD-023 |
| MOD-003 Onboarding | Bienvenida, configuracion incompleta, necesidad de resolver si hace falta Delegado, invitacion de usuario pendiente, onboarding abandonado | INFO a CRITICAL | Evento de Tarea (MOD-021) para el seguimiento del wizard; el correo de invitacion inicial es la unica notificacion de este modulo que se dispara directamente al completarse un paso, sin Tarea previa |
| MOD-004 Diagnostico de Cumplimiento | Diagnostico nunca iniciado, sesion estancada, acciones criticas sin asignar, posible incidente o solicitud ARCO-POL no reportada detectada en el cuestionario, re-diagnostico recomendado, cambio de regimen 659 | INFO a CRITICAL | Evento de Tarea (MOD-021); los dos disparadores CRITICAL (incidente o ARCO-POL no reportado) generan primero la tarea urgente en MOD-021 y esta dispara la notificacion inmediata |
| MOD-005 Plan de Cumplimiento | Plan pendiente de aprobacion, accion proxima a vencer o vencida, multiples acciones criticas vencidas, plan desactualizado, accion bloqueada, cambio normativo con impacto en el plan | INFO a CRITICAL | Evento de Tarea o Aprobacion (MOD-021) |
| MOD-006 RAT y Mapa de Datos | Ficha pendiente de completar o de aprobar, revision periodica vencida, transferencia posiblemente no documentada, sistema dado de baja con tratamientos vigentes, dato biometrico sin control enlazado, RAT sin ninguna ficha vigente | INFO a CRITICAL | Evento de Tarea/Aprobacion (MOD-021) para lo ligado a flujo de aprobacion; evento de plazo (MOD-023) para la revision periodica programada |
| MOD-007 Consentimiento | Consentimiento pendiente de captura, consentimiento sensible incompleto, revocacion o notificacion al encargado proxima a vencer o vencida, version de Aviso no disponible, consentimiento biometrico sin alternativa | INFO a CRITICAL | Evento de Tarea (MOD-021) para captura y revocacion (ligadas al doble plazo de 5+5 dias de OBL-CONS-03, calculado por MOD-023) |
| MOD-008 Documentos y Politicas | Aviso de Privacidad sin publicar, documento pendiente de aprobacion o que requiere revision, aviso que no menciona un encargado nuevo, cambio de regimen 659 (revisar avisos), documento proximo a su revision periodica | INFO a CRITICAL | Evento de Tarea/Aprobacion (MOD-021) para los estados de workflow documental; evento de plazo (MOD-023) para la revision periodica programada |
| MOD-009 Proveedores y Encargados | Contrato/DPA proximo a vencer o vencido, revision periodica vencida, proveedor sin evaluacion de riesgo vigente, transferencia sin registro vinculado, incidente grave vinculado, subencargado sin documento de sometimiento | WARNING a CRITICAL | Evento de plazo (MOD-023) para vencimientos de contrato y revisiones periodicas; evento de Tarea (MOD-021) para lo demas; el incidente grave vinculado llega como evento directo desde MOD-013 |
| MOD-010 Transferencias Internacionales | Transferencia detectada sin confirmar, evaluacion de pais incompleta o desactualizada, consentimiento especifico faltante, contrato de transferencia por vencer o vencido, puesta en conocimiento a la ACE pendiente, transferencia huerfana | WARNING a CRITICAL | Evento de Tarea (MOD-021) para los estados de workflow; evento de plazo (MOD-023) para vencimientos de contrato y evaluacion de pais |
| MOD-011 ARCO-POL | Solicitud sin responsable, prevencion o plazo general proximo a vencer o vencido, notificacion a receptores pendiente, denegatoria o incompetencia pendiente de notificar, reclamo ante la ACE, solicitud pendiente de aprobacion del Delegado, bloqueo cautelar prolongado, retencion del expediente proxima a vencer | INFO a CRITICAL | **Evento directo** (declarado en `depende_de` de MOD-022): los cronometros de 20+20, 10, 5 y 3 dias habiles se calculan en MOD-023 pero MOD-011 empuja el evento de alerta el mismo, dada la granularidad fina y la criticidad de sus plazos |
| MOD-012 Portal del Titular | Nueva solicitud recibida, intentos de verificacion fallidos, solicitud sin triage cerca del vencimiento de la prevencion, cambio de version de Aviso/Politica publicados | INFO a HIGH | Evento de Tarea (MOD-021), a traves de MOD-011 (el expediente que el Portal alimenta es siempre de MOD-011; ver seccion A.1). El codigo de verificacion y el aviso de estado al titular NO son Notification de MOD-022 (destinatario externo, fuera de alcance de este modulo, ver seccion A.1) |
| MOD-013 Incidentes de Seguridad | Cronometro de notificacion (aviso temprano, critico, vencido), cronometro de revision interna, documentacion incompleta con riesgo confirmado, incidente en proveedor sin evidencia de aviso, posible operador de infraestructura critica, caso cerrado con notificacion tardia | INFO a CRITICAL | **Evento directo** (declarado en `depende_de` de MOD-022): el cronometro de 72 horas de OBL-INC-01/02 exige alertas por hora, mas finas que un estado de Tarea generico |
| MOD-014 Riesgos y EIPD | Tratamiento de alto riesgo sin EIPD, EIPD con riesgo alto pendiente de mitigacion o de aprobacion, EIPD proxima a vencer, cambio material en tratamiento con EIPD vigente, EIPD rechazada, control pendiente generado desde una EIPD | WARNING a CRITICAL | Evento de Tarea/Aprobacion (MOD-021) |
| MOD-015 Controles de Seguridad | Proxima revision de un control, revision urgente, control vencido, control obligatorio sin evidencia, excepcion pendiente de aprobacion, hallazgo detectado en revision | INFO a HIGH | Evento de plazo (MOD-023) para revisiones programadas; evento de Tarea/Aprobacion (MOD-021) para excepciones y hallazgos |
| MOD-016 Retencion y Eliminacion | Regla proxima a vencer, eliminacion pendiente de aprobacion o aprobada sin ejecutar, intento de eliminar antes del plazo minimo documental, solicitud ARCO-POL que choca con un dato retenido, conflicto de fundamentos con plazos distintos | INFO a CRITICAL | Evento de plazo (MOD-023) para vencimientos de retencion; evento de Tarea/Aprobacion (MOD-021) para el flujo de eliminacion |
| MOD-018 Auditoria de Cumplimiento | Recordatorio y proximidad de la auditoria anual, auditoria vencida, hallazgo critico sin plan de accion, accion correctiva vencida, auditoria abierta mas de 90 dias | INFO a HIGH | Evento de plazo (MOD-023) para la periodicidad anual (OBL-AUD-01); evento de Tarea (MOD-021) para hallazgos y acciones correctivas |
| MOD-019 Centro de Evidencias (ficha redactada despues de esta, incorporada en la revision de correccion, ver Nota final punto 1) | Hueco de evidencia detectado, evidencia por vencer, evidencia vencida, evidencia rechazada, evidencia cargada pendiente de aprobacion, paquete de evidencia pendiente de segundo control | INFO a HIGH | Evento de Tarea (MOD-021) para el flujo de aprobacion y segundo control de evidencia; evento de plazo (MOD-023) para el vencimiento o renovacion programada de una evidencia |
| MOD-021 Centro de Tareas (fuente estructural, no "emisor" en el mismo sentido) | Tarea proxima a vencer o vencida, plazo critico de 72 horas de un incidente en curso, aprobacion pendiente, tarea bloqueada, tarea recurrente proxima a generarse, tareas archivadas por cambio de regimen | WARNING a CRITICAL | Es el canal de entrada mismo para la mayoria de las familias de esta tabla, no un modulo de origen adicional |
| MOD-023 Calendario y Motor de Plazos (fuente estructural) | Cualquier evento puramente calendarico que no requiere que exista antes una Tarea (por ejemplo, revisiones periodicas programadas por fecha) | INFO a WARNING (los niveles altos siempre llegan encapsulados en una Tarea de MOD-021 o en un evento directo de MOD-011/MOD-013) | Es el segundo canal de entrada estructural, no un modulo de origen adicional |
| MOD-024 Centro Regulatorio | Cambio de regimen normativo (activacion de la bandera de la reforma 659) | INFO | Evento de Tarea (MOD-021): MOD-024 activa la bandera, MOD-021 archiva las tareas afectadas y crea la tarea "revisar avisos publicados", y esa tarea es la que dispara la notificacion informativa hacia Delegado/Responsable interno, Legal/Compliance y Administrador |

---

## J. Evidencia

MOD-022 no es propietario de ninguna obligacion, pero es donde queda el registro de que la organizacion fue avisada a tiempo de un plazo o de un pendiente, evidencia que complementa (nunca sustituye) la que genera el modulo propietario del expediente.

- **Registro con fecha y hora de cada cambio de estado de una Notificacion** (generada, en envio, enviada, entregada, leida, acusada, escalada, resuelta): prueba que el aviso existio y en que momento llego a cada canal, distinto de si la obligacion de fondo se resolvio a tiempo.
- **Registro del Acuse de recibo con identidad, fecha y hora**, exigido para toda notificacion CRITICAL: equivale a una constancia de que una persona identificada confirmo haber visto el aviso mas urgente del sistema (por ejemplo, el cronometro de 72 horas de OBL-INC-01). Prueba OBL-PRIN-03 (responsabilidad demostrada, Art. 5 lit. i LPDP) sobre el hecho especifico de que hubo un aviso y una persona lo atendio, sin pronunciarse sobre si la obligacion sustantiva se cumplio.
- **Registro de escalamientos**, con el destinatario original, el destinatario de escalamiento y el tiempo transcurrido sin respuesta: util tanto para mejorar la asignacion de responsables como, ante una auditoria o un requerimiento de la ACE, para mostrar que la organizacion tenia un mecanismo activo de seguimiento, no solo un envio unico sin control de recepcion.
- **Historial de fallos de entrega y de sus reintentos**: evidencia de que un aviso no llego por una causa tecnica (por ejemplo, un correo rebotado) y de que el sistema lo detecto y lo escalo por un canal alternativo, en vez de dejar la falla en silencio.
- **Exportacion firmada o con hash**, delegada al mecanismo unico de integridad que expone MOD-019 Centro de Evidencias: MOD-022 no reinventa su propio formato de exportacion, entrega sus registros a MOD-019 para que el paquete de evidencias sea consistente en todo el sistema (`22_anti_features.md`, item 25).
- **Tiempo de conservacion.** El historial de notificaciones sigue la regla de conservacion documental de cumplimiento propio de MOD-016 Retencion y Eliminacion, alineada con la del objeto de origen que sustenta (expedientes ARCO-POL o de incidentes: 5 anios, segun OBL-RET-05; el resto de familias, segun la politica general de retencion documental de la organizacion). MOD-022 nunca elimina su propio historial de forma independiente: solo lo archiva al llegar a Resuelta, nunca lo borra (`22_anti_features.md`, item 19).

---

## K. Documentos asociados

- **Documentos requeridos como entrada.** MOD-022 no exige ningun documento propio para generar una Notificacion: el contenido siempre proviene de la plantilla de la familia de evento (seccion D.1) mas la referencia al objeto de origen, que vive en el modulo correspondiente.
- **Documentos generados.**
  - Reporte de notificaciones (ver seccion N).
  - Registro de Regla de notificacion vigente por familia (configuracion, no un documento formal, pero exportable como respaldo de la configuracion activa en un momento dado, util ante una auditoria que pregunte "que reglas de aviso tenia configuradas la empresa cuando ocurrio este caso").
- **Plantillas que el sistema provee.**
  - Plantilla de mensaje por familia de evento (version plataforma y version canal externo), con las variables permitidas explicitamente listadas (referencia al objeto de origen, nivel, fecha limite) y las variables prohibidas (cualquier dato personal de titular, cualquier detalle sustantivo de un caso). No requiere validacion de asesoria juridica para su redaccion general (es texto operativo, no un acto legal), pero si requiere revision de producto antes de publicarse, dado que fija el tono y la claridad exigidos por el principio de lenguaje sencillo (Art. 5 lit. e LPDP).
- **Anexos y evidencias documentales.** El unico anexo posible dentro de una Notificacion es la constancia manual de un intento de aviso fallido por un canal no digital (por ejemplo, una nota de que se llamo por telefono cuando el correo rebotaba), cargada por el Administrador o el Delegado/Responsable interno (seccion C).

---

## L. Dependencias

### L.1 Diagrama

```
   MOD-021 Centro de Tareas          MOD-023 Calendario y Motor de Plazos
   (eventos de Tarea/Aprobacion:            (eventos de plazo puro,
    proxima a vencer, vencida,               sin Tarea previa: revision
    bloqueada, aprobacion pendiente)          periodica, vencimiento)
              |                                       |
              |                                       |
              +------------------+--------------------+
                                 |
                                 v
                    MOD-022 NOTIFICACIONES
                                 ^
              +------------------+--------------------+
              |                                       |
   MOD-011 ARCO-POL                          MOD-013 Incidentes de Seguridad
   (eventos directos: cronometros                (eventos directos: cronometro
    de 20+20, 10, 5 y 3 dias habiles)              de 72 horas, por hora)

   Los cuatro modulos anteriores son los unicos declarados en el campo
   `depende_de` de MOD-022 en mapa_modulos.json. Todo modulo de recorrido
   restante (MOD-001 a MOD-018, salvo MOD-011/MOD-013) llega a MOD-022 de
   forma indirecta, siempre a traves de MOD-021 o de MOD-023 (ver seccion I.1
   y Nota final, punto 1): "Notificacion (MOD-022)" en la seccion I de esas
   fichas describe el destino final del aviso, no una arista adicional en el
   grafo `depende_de`/`alimenta_a`.

                    MOD-022 NOTIFICACIONES
                                 |
                       (modulo terminal de lectura,
                        alimenta_a: [] en mapa_modulos.json)
                                 v
                        Destinatario resuelto
                (usuario interno de la organizacion,
                 nunca el Titular externo, ver seccion A.1)
```

### L.2 Lista de dependencias

**Entra desde (le entregan el evento que dispara una Notificacion):** MOD-021 Centro de Tareas (todo evento de Tarea o Aprobacion: creacion, proxima a vencer, vencida, bloqueada, aprobacion pendiente, archivado por cambio de regimen), MOD-023 Calendario y Motor de Plazos (eventos de plazo que no requieren una Tarea previa, por ejemplo revisiones periodicas programadas por fecha), MOD-011 ARCO-POL (eventos directos de cronometro de sus plazos propios: prevencion de 10 dias, plazo general de 20+20, incompetencia y notificacion a receptores de 5 dias, denegatoria de 3 dias) y MOD-013 Incidentes de Seguridad (eventos directos del cronometro de 72 horas de notificacion externa y de inicio de revision interna).

**Sale hacia:** ninguno, segun `mapa_modulos.json` (`alimenta_a: []`). MOD-022 es, junto con MOD-025 Busqueda Global y MOD-026 Centro de Ayuda, un modulo terminal de lectura (`06_mapa_definitivo_de_modulos.md`, seccion 4, regla 5): su unica salida es hacia el destinatario resuelto (un usuario interno de la organizacion, nunca hacia otro modulo). La unica excepcion parcial es el evento de auditoria que MOD-022 entrega a MOD-019 Centro de Evidencias (seccion E), coherente con el patron transversal general que todo modulo del sistema sigue hacia el AuditLog, y que no aparece como arista separada en `mapa_modulos.json` por la misma razon documentada en `06_mapa_definitivo_de_modulos.md`, seccion 6.1, para MOD-001/MOD-023/MOD-024 (una lectura de referencia constante, no una dependencia estructural declarada aparte).

**Que ocurre si un modulo dependiente no existe en el MVP.** MOD-021, MOD-023, MOD-011 y MOD-013 son los cuatro modulos declarados en `depende_de` de MOD-022, y los cuatro son MUST HAVE del MVP segun `06_mapa_definitivo_de_modulos.md` (tabla de la seccion 1). Este riesgo, por lo tanto, no aplica en el MVP: MOD-022 siempre tiene sus cuatro fuentes estructurales disponibles desde el primer lanzamiento. Los modulos de proceso SHOULD HAVE o COULD HAVE (por ejemplo, MOD-012 Portal, MOD-014 Riesgos/EIPD, MOD-016 Retencion, MOD-025 Busqueda Global) pueden generar menos eventos de origen mientras no esten completos, pero eso no afecta el funcionamiento de MOD-022 en si mismo: simplemente hay menos familias de alerta activas hasta que esos modulos maduren, sin que MOD-022 dependa de ellos para operar.

---

## M. Dashboard

Todos los indicadores se expresan como estado del programa (avisos entregados, atendidos, pendientes de acuse), nunca como porcentaje de cumplimiento legal (`04_objetivo_exacto_del_producto.md`, seccion 1.2).

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Notificaciones CRITICAL pendientes de acuse | Conteo de notificaciones en estado Leida o Entregada, nivel CRITICAL, sin Acuse registrado | Rojo si mayor a 0, amarillo si el tiempo restante del plazo asociado es menor al 50% | Gerencia, Delegado/Responsable interno, Legal/Compliance, Auditor |
| Notificaciones escaladas en el periodo | Conteo de notificaciones con bandera Escalada activa, agrupadas por familia | Amarillo si sube respecto del promedio historico, rojo si supera el umbral configurado | Gerencia, Administrador |
| Tasa de entrega fallida | Notificaciones con estado Fallida tras agotar reintentos, dividido entre el total enviado en el periodo | Verde si menor al 1%, amarillo 1 a 5%, rojo mayor a 5% | Administrador |
| Tiempo promedio de acuse en notificaciones CRITICAL | Promedio de tiempo entre Entregada/Leida y Acusada, por familia | Sin semaforo (indicador de tendencia) | Legal, Gerencia, Auditor |
| Notificaciones agrupadas en resumen vs. individuales | Proporcion de notificaciones no obligatorias entregadas en resumen frente al total | Informativo, sin semaforo (mide adopcion de la funcion anti-fatiga) | Administrador |
| Roles criticos sin titular activo | Conteo de roles con una Regla de notificacion activa cuyo destinatario resuelto esta vacio | Rojo si mayor a 0 | Gerencia, Administrador, Auditor |

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Listado de notificaciones | Todas las notificaciones con sus campos principales (familia, nivel, destinatario, estados de entrega, lectura y acuse) | Familia, nivel, destinatario, rango de fechas, modulo de origen | XLSX, CSV | Administrador, Delegado/Responsable interno, Legal/Compliance | Si, como respaldo operativo |
| Notificaciones CRITICAL con su acuse | Todas las notificaciones de nivel CRITICAL del periodo, con fecha y hora de generacion, entrega, lectura y acuse (o su ausencia) | Rango de fechas, familia, modulo de origen | XLSX, PDF | Auditor, Auditor externo, Gerencia | Si, es el insumo principal para demostrar que un plazo critico fue avisado a tiempo |
| Historial de una notificacion especifica | Linea de tiempo completa: generacion, envio por canal, entrega, lectura, acuse, escalamiento | Una notificacion puntual | PDF | Auditor, Auditor externo, Legal/Compliance | Si |
| Entregas fallidas y sus reintentos | Notificaciones que fallaron por canal externo, con motivo y numero de reintentos | Rango de fechas, canal, destinatario | XLSX | Administrador | No (uso interno de gestion) |
| Configuracion vigente de Reglas de notificacion | Foto de las reglas activas por familia (destinatario, canal, escalamiento) en un momento dado | Fecha de corte | PDF | Auditor, Auditor externo | Si, para responder "que reglas de aviso tenia configuradas la empresa" |

---

## O. Historial

Eventos que quedan en el historial de cada Notificacion y que se replican en el AuditLog transversal:

- Generacion de la notificacion (familia, nivel, objeto de origen, modulo de origen funcional, fecha y hora).
- Resolucion de destinatario(s) y canal(es), incluyendo cuando se activa un suplente.
- Cada cambio de estado (Generada, En envio, Enviada, Entregada, Fallida, Leida, Acusada, Resuelta), con fecha y hora exacta.
- Cada reintento de envio por canal externo, con su resultado.
- El acuse de recibo, con identidad, fecha y hora (para notificaciones CRITICAL).
- Cada escalamiento, con el destinatario original, el destinatario de escalamiento y el tiempo transcurrido.
- Cambios a una Regla de notificacion (valor anterior y nuevo), con el usuario que los hizo.
- Cambios a una Preferencia de usuario (resumen, horario silencioso, canales habilitados, notificaciones silenciadas individualmente).
- Cualquier intento de silenciar o modificar una familia con piso minimo de plazo legal, aunque el sistema lo bloquee: queda registrado como intento, con identidad y fecha, para trazabilidad (ver seccion H).
- Exportaciones de reportes que incluyen notificaciones (quien exporto, cuando, que reporte).

---

## P. Riesgos

- **Riesgo legal: que la existencia de una notificacion enviada se confunda con la resolucion de la obligacion de fondo.** Una notificacion "Acusada" prueba que alguien vio el aviso a tiempo, no que la organizacion redacto y envio correctamente la comunicacion formal correspondiente. *Mitigacion de diseno*: los indicadores del dashboard (seccion M) siempre se expresan como "notificaciones entregadas / acusadas / escaladas", nunca como "obligacion cumplida"; el texto de descargo estandar de `04_objetivo_exacto_del_producto.md` (seccion 1.3) se muestra junto a cualquier resumen relacionado con plazos legales.
- **Riesgo legal: que se interprete el acuse tecnico (apertura de correo) como confirmacion valida para un aviso CRITICAL.** *Mitigacion de diseno*: el sistema nunca acepta la apertura de correo como Acuse (seccion H); solo una accion explicita dentro de la plataforma, con identidad y fecha, cuenta como acuse.
- **Riesgo de UX: fatiga de alertas por exceso de avisos no criticos, que lleve a ignorar tambien los criticos.** Es el riesgo central que motiva las reglas anti-fatiga de este modulo (deduplicacion, resumen, horario silencioso). *Mitigacion de diseno*: solo las familias con piso minimo de plazo legal se entregan siempre de forma individual e inmediata; todo lo demas puede agruparse, y el usuario puede ajustar su propia Preferencia sin afectar el piso minimo de nadie mas en la organizacion.
- **Riesgo de UX: que el Administrador configure un destinatario de escalamiento equivocado o inexistente para una familia critica**, dejando un plazo sin nadie que realmente lo reciba a tiempo. *Mitigacion de diseno*: la alerta "Regla de notificacion sin destinatario configurado" (seccion I) avisa de inmediato cuando una Regla queda sin destinatario valido, y la resolucion de destinatario siempre valida contra usuarios activos de MOD-001.
- **Riesgo operativo: que el modulo de origen (MOD-021, MOD-023, MOD-011 o MOD-013) calcule mal la fecha limite y MOD-022 propague un aviso incorrecto.** MOD-022 nunca recalcula el plazo por su cuenta. *Mitigacion de diseno*: el mensaje siempre muestra el objeto de origen y el criterio de computo que ese modulo ya expone (por ejemplo, "criterio de computo mostrado" de MOD-021), para que un error se audite y corrija de forma centralizada en el modulo que realmente calculo el plazo, no en MOD-022.
- **Riesgo de seguridad y privacidad: que una plantilla de mensaje termine incluyendo, por error de configuracion, un dato personal de un titular o el detalle sustantivo de un caso en un canal externo (correo).** *Mitigacion de diseno*: bloqueo tecnico automatico en la generacion del mensaje para canal externo, que impide insertar cualquier campo marcado como dato personal en MOD-006/MOD-011/MOD-013 (seccion D.1 y H); el mensaje externo siempre se limita a un aviso generico mas un enlace de acceso autenticado.
- **Riesgo de seguridad: que un canal externo (correo, y en el futuro SMS o WhatsApp) sea interceptado o llegue a la persona equivocada.** *Mitigacion de diseno*: el contenido sustantivo nunca viaja por el canal externo (mismo punto anterior); el enlace de acceso exige autenticacion propia de la plataforma, de modo que interceptar el correo no equivale a acceder al caso.
- **Riesgo de producto: que canales adicionales (Teams, Slack, SMS, WhatsApp) se incorporen sin evaluar que datos viajan por ellos ni su costo real.** *Mitigacion de diseno*: el MVP se limita a Plataforma y Correo (seccion Q); cualquier canal adicional requiere una evaluacion explicita de demanda, seguridad y costo antes de activarse, documentada como decision de producto, nunca asumida por defecto (ver `06_mapa_definitivo_de_modulos.md`, ficha resumida de MOD-022, seccion 3).

---

## Q. MVP

| Funcionalidad del modulo | Clasificacion | Justificacion |
|---|---|---|
| Notificacion basica por Plataforma y Correo, con resolucion de destinatario por rol | MUST HAVE | Condicion (b) del test de tres condiciones del mapa definitivo: sin esto, ningun modulo MUST HAVE con plazo legal (MOD-002, MOD-011, MOD-013, MOD-021) puede avisar a nadie de un vencimiento. |
| Piso minimo de alertas de plazos legales, no silenciable ni configurable a la baja | MUST HAVE | Es la instrumentacion directa del riesgo identificado en `06_mapa_definitivo_de_modulos.md` (seccion 4): sin este piso, un plazo OBLIGATORIO podria quedar sin aviso por una configuracion equivocada o deliberada. |
| Niveles INFO/WARNING/HIGH/CRITICAL con escalamiento automatico | MUST HAVE | El escalamiento del cronometro de 72 horas (OBL-INC-01) y de los plazos ARCO-POL (OBL-ARCO-10) es el mecanismo central que evita que un plazo critico dependa de una sola persona disponible. |
| Acuse de recibo obligatorio para notificaciones CRITICAL | MUST HAVE | Es la unica forma de que la responsabilidad demostrada (OBL-PRIN-03) sobre un aviso urgente no dependa de una senal tecnica poco confiable (apertura de correo); sin esto, el sistema no puede probar que alguien realmente atendio el aviso mas critico. |
| Historial inmutable de notificaciones (generada, enviada, entregada, leida, acusada, escalada) | MUST HAVE | Es la base minima de evidencia de que la organizacion fue alertada a tiempo, exigida desde el primer dia por el mismo principio que exige MOD-021. |
| Reglas anti-fatiga: deduplicacion y resumen diario/semanal para lo no obligatorio | SHOULD HAVE | Mejora sustancialmente la experiencia de uso sostenido (riesgo de UX de la seccion P), pero el MVP puede operar sin ellas entregando cada notificacion de forma individual, sin bloquear ninguna obligacion legal. |
| Horario silencioso configurable | SHOULD HAVE | Reduce la fatiga fuera de horario laboral, pero no es estructuralmente necesaria para que ningun otro modulo MUST HAVE opere; puede anadirse justo despues del lanzamiento inicial. |
| Reasignacion de destinatario por suplente configurado | SHOULD HAVE | Mejora la cobertura cuando el responsable titular no esta disponible, pero el MVP puede operar con escalamiento directo al Administrador mientras no exista una regla de suplencia explicita. |
| Canales adicionales: Microsoft Teams, Slack, SMS, WhatsApp | FUTURE (V1/V2, sujeto a evaluacion) | Depende de demanda real de los primeros clientes, de seguridad (que datos viajan por cada canal) y de costo, segun la propia clasificacion de MOD-022 en `06_mapa_definitivo_de_modulos.md`, seccion 3: "MUST HAVE con canales basicos... canales adicionales quedan en V1/V2 segun demanda real". |
| Reportes exportables avanzados (configuracion vigente de reglas, entregas fallidas y reintentos) | COULD HAVE | El listado basico de notificaciones (XLSX/CSV) es MUST HAVE; los reportes mas elaborados pueden esperar a la primera necesidad real de auditoria. |
| Panel de analitica de volumen y adopcion de resumenes | COULD HAVE | Mejora de gestion de producto sobre datos que ya existen; no aporta una capacidad legal nueva. |

**Version minima vendible del modulo.** La version minima que ya puede venderse incluye: notificacion por Plataforma y Correo con resolucion de destinatario por rol, el piso minimo de alertas de plazos legales no silenciable, los cuatro niveles con escalamiento automatico, el acuse de recibo obligatorio para CRITICAL, y el historial inmutable de cada notificacion. Esta combinacion ya resuelve el problema central del modulo (que ningun plazo legal dependa de que alguien recuerde entrar a mirar el sistema) y es la unica forma de que MOD-002, MOD-011, MOD-013 y MOD-021 -todos MUST HAVE- puedan avisar de sus plazos desde el primer dia.

---

## R. Ayuda contextual (complemento obligatorio)

**1. Que es una notificacion**
- *Que es*: un aviso que el sistema le envia, dentro de la plataforma y por correo (u otro canal que su empresa active), cuando algo que le corresponde a usted o a su equipo se acerca a su fecha limite o necesita su atencion.
- *Por que tengo que hacer esto*: porque un plazo legal que nadie recuerda revisar termina vencido sin que nadie lo note a tiempo.
- *Fundamento*: no tiene un OBL-ID propio; sostiene el aviso oportuno de las obligaciones con plazo de otros modulos (por ejemplo, OBL-INC-01, Art. 25 LPDP, o OBL-ARCO-10, Art. 20 LPDP).
- *Cuando necesito ayuda juridica*: la notificacion misma nunca requiere ayuda juridica; si tiene dudas sobre que hacer con la obligacion que el aviso menciona, consulte al Delegado/Responsable interno o a asesoria especializada.

**2. Que es el acuse de recibo obligatorio**
- *Que es*: para los avisos mas urgentes (por ejemplo, el cronometro de 72 horas de una vulneracion de seguridad), no basta con que el sistema detecte que abrio el correo: usted debe confirmar dentro de la plataforma que vio y entendio el aviso.
- *Por que tengo que hacer esto*: porque ante una auditoria o la ACE, la empresa necesita poder demostrar que una persona identificada realmente atendio el aviso mas critico, no solo que el sistema lo envio.
- *Fundamento*: Art. 5 lit. i LPDP, principio de responsabilidad demostrada (OBL-PRIN-03).
- *Cuando necesito ayuda juridica*: si no esta seguro de que accion tomar despues de acusar recibo (por ejemplo, si ya se le esta acabando el plazo de 72 horas), consulte de inmediato a su Delegado/Responsable interno o a asesoria especializada; el acuse solo confirma que vio el aviso, no resuelve la obligacion de fondo.

**3. Que es el resumen diario o semanal**
- *Que es*: en vez de recibir cada aviso no urgente por separado, puede configurar que se le entreguen agrupados una vez al dia o una vez a la semana.
- *Por que tengo que hacer esto*: para que la bandeja no se llene de avisos de baja urgencia y usted termine ignorando tambien los importantes.
- *Fundamento*: decision de producto (buena practica de usabilidad), sin base legal especifica; no aplica nunca a los avisos de plazos legales obligatorios, que siempre llegan de inmediato y por separado.
- *Cuando necesito ayuda juridica*: nunca por este concepto en si mismo.

**4. Que es el piso minimo de alertas de plazos legales**
- *Que es*: un conjunto de avisos (los ligados a plazos que la ley fija, como las 72 horas de una vulneracion o los 20 mas 20 dias de una solicitud ARCO-POL) que nadie en su empresa, ni siquiera el Administrador, puede apagar, agrupar en un resumen ni posponer.
- *Por que tengo que hacer esto*: para que ningun plazo obligatorio quede sin aviso por una configuracion equivocada o por comodidad.
- *Fundamento*: sostiene el aviso oportuno de obligaciones OBLIGATORIO de la matriz (por ejemplo, OBL-INC-01, Art. 25 LPDP; OBL-ARCO-10, Art. 20 LPDP; OBL-DPO-03, Art. 10 Lineamientos DPO).
- *Cuando necesito ayuda juridica*: si considera que un plazo especifico no deberia aplicarle a su empresa y por eso quisiera desactivar su aviso, no lo decida usted mismo dentro del sistema: consulte a su Delegado/Responsable interno o a asesoria especializada, porque el sistema no permite esa excepcion por diseno.

**5. Diferencia entre un aviso interno de MOD-022 y una comunicacion formal a un titular o a la autoridad**
- *Que es*: un aviso de MOD-022 solo le informa a usted, dentro de su empresa, que un plazo se acerca; la comunicacion formal (por ejemplo, la notificacion de una vulneracion a la ACE, a la Fiscalia y a los titulares, o la respuesta a una solicitud ARCO-POL) es un documento distinto, con su propio contenido y su propia aprobacion, que gestionan los modulos de Incidentes y de ARCO-POL, nunca este modulo.
- *Por que tengo que hacer esto*: para que quede claro que recibir el aviso interno no significa que la comunicacion formal ya se envio; son dos cosas distintas y ambas quedan registradas por separado.
- *Fundamento*: Art. 25 LPDP (notificacion de vulneraciones) y Arts. 18 a 22 LPDP (respuestas ARCO-POL), gestionados por MOD-013 y MOD-011 respectivamente.
- *Cuando necesito ayuda juridica*: siempre que deba redactar o revisar el contenido de la comunicacion formal misma; el aviso interno de MOD-022 nunca sustituye esa revision.

---

## Nota final del agente (desacuerdos y observaciones sobre las fuentes de diseno)

1. **Reconciliacion de la regla de conexion 2 con el vocabulario de las 18 fichas ya redactadas.** `06_mapa_definitivo_de_modulos.md` (seccion 4, regla 2) dice: "MOD-022 Notificaciones solo reacciona a eventos que le entregan MOD-021 y MOD-023; ningun modulo de recorrido envia notificaciones por su cuenta". El campo `depende_de` de MOD-022 en `mapa_modulos.json` confirma exactamente cuatro entradas: `MOD-021, MOD-023, MOD-011, MOD-013`. Sin embargo, al buscar `MOD-022` en las 18 fichas ya escritas (`grep -n "MOD-022" analisis/03_modulos/*.md`), casi todas (MOD-001, MOD-003, MOD-006, MOD-007, MOD-008, MOD-009, MOD-010, MOD-014, MOD-015, MOD-016, MOD-018, ademas de MOD-011 y MOD-013) citan "Notificacion (MOD-022)" o dibujan una flecha directa hacia MOD-022 en su propia seccion I o en su diagrama de dependencias, como si cada una le entregara el evento por su cuenta. Se verifico contra `mapa_modulos.json` que **ninguno de esos modulos (salvo MOD-011 y MOD-013) declara `MOD-022` en su propio campo `alimenta_a`**: por ejemplo, MOD-008 declara `alimenta_a: [MOD-007, MOD-009, MOD-012, MOD-016, MOD-019]` (sin MOD-022), y MOD-018 declara `alimenta_a: [MOD-019, MOD-020, MOD-021]` (tampoco incluye MOD-022, pese a que su propia ficha dice en la seccion E: "Recordatorio de la proxima auditoria... Tarea en MOD-021 y alerta en MOD-022"). Lo mismo ocurre con `MOD-019_ficha.md` Centro de Evidencias, redactada despues de esta ficha e incorporada en la revision de correccion (ver encabezado): su seccion E declara "Alerta de evidencia vencida o por renovar... Tarea en MOD-021 y alerta en MOD-022", mientras que su `alimenta_a` en `mapa_modulos.json` es `[MOD-018, MOD-020, MOD-024]`, sin arista hacia MOD-021 ni hacia MOD-022; se agrega su fila a la tabla consolidada de la seccion I.1 con el mismo criterio que las demas. Esta ficha resuelve la aparente contradiccion, no como un error a corregir en esas fichas ni en `mapa_modulos.json` (ninguno de los dos se modifica aqui), sino como dos niveles de descripcion compatibles: la prosa de cada ficha describe el **destino final** del aviso (siempre MOD-022, correctamente), mientras que el grafo estructural `depende_de`/`alimenta_a` describe la **via estructural** por la que el evento llega alli, que para esos 17 modulos (los 16 ya citados mas MOD-019) es siempre indirecta, a traves de una Tarea o Aprobacion de MOD-021 o de un evento de plazo de MOD-023 (ver seccion D.1, "Canal de entrada", y la tabla consolidada de la seccion I.1). MOD-019, redactada despues de esta ficha, ya sigue esta misma convencion (cita "alerta en MOD-022" en su prosa sin declarar la arista en `mapa_modulos.json`), por lo que no requiere correccion en `MOD-019_ficha.md`. Se recomienda a quien redacte las fichas restantes (MOD-017, MOD-020, MOD-023, MOD-026) mantener esta misma convencion: citar "Notificacion (MOD-022)" en su seccion I sin que eso implique declarar una arista `depende_de` directa hacia MOD-022 en `mapa_modulos.json`, salvo que el modulo en cuestion tenga, como MOD-011 y MOD-013, cronometros propios de granularidad mas fina que un estado de Tarea generico. **Nota sobre la revision adversarial de esta ficha:** una revision adversarial senalo como fallo grave que MOD-022 omitio a MOD-019 pese a que, segun esa revision, "MOD-019_ficha.md quedo escrito antes que MOD-022_ficha.md" (verificado, segun el revisor, por marca de tiempo del sistema de archivos). Se verifico esa afirmacion contra la marca de tiempo real de ambos archivos y resulto ser exactamente la inversa: `MOD-022_ficha.md` se escribio primero (marca de tiempo mas temprana) y `MOD-019_ficha.md` se escribio despues (marca de tiempo posterior, igual que `MOD-025_ficha.md`). Por lo tanto, el conteo de "18 fichas ya redactadas (MOD-001 a MOD-016, MOD-018, MOD-021)" que esta ficha declaraba en su encabezado era correcto en el momento de escribirla, y no hubo omision negligente de MOD-019: esa ficha simplemente no existia todavia. Se rechaza el fallo grave tal como fue argumentado (la premisa cronologica es incorrecta), pero se acepta y aplica su contenido sustantivo: al momento de esta correccion MOD-019 ya existe y su seccion E declara una expectativa expresa hacia MOD-022 no reflejada hasta ahora en la tabla I.1 ni en esta reconciliacion, por lo que se incorpora aqui y en la seccion I.1 para mantener el modelo unificado completo con el estado actual del repositorio.
2. **Resolucion de la pregunta abierta por `MOD-012_ficha.md` sobre la "arista faltante hacia MOD-022".** Esa ficha (seccion L, nota final) preguntaba si el codigo de verificacion y el aviso de actualizacion de estado que el Portal envia al titular externo deben modelarse como un evento de MOD-011 o si conviene anadir una arista `depende_de` de MOD-012 hacia MOD-022. Esta ficha responde de forma explicita en la seccion A.1: esos dos correos **no son Notification de MOD-022**, porque MOD-022 gestiona exclusivamente avisos internos a usuarios de la organizacion cliente (nunca al Titular externo, que no figura entre los destinatarios de la seccion B); se modelan como actos propios de MOD-011 (dueno del expediente ARCO-POL que el Portal solo canaliza), sin que haga falta modificar el `depende_de` de MOD-012 ni el de MOD-022 en `mapa_modulos.json`.
3. **Clasificacion MVP.** Se mantiene MUST HAVE, identica a la de `mapa_modulos.json` y a `06_mapa_definitivo_de_modulos.md`. No hay discrepancia que reportar: la justificacion de la seccion Q coincide con la razon dada en la ficha resumida del mapa definitivo (condicion (b) del test de tres condiciones: dependencia estructural de todos los modulos MUST HAVE con plazo legal).
4. **Alcance de canales mas alla de Plataforma y Correo.** Esta ficha no asume ninguno de los canales adicionales (Teams, Slack, SMS, WhatsApp) como decidido para V1 o V2; se documentan unicamente como candidatos a evaluar segun demanda, seguridad (que datos viajarian por cada canal) y costo, tal como exige el enfoque especifico de esta tarea y la propia clasificacion de MOD-022 en el mapa definitivo. Ningun campo de esta ficha (por ejemplo, "Canal(es) resuelto(s)" en la seccion D.1) obliga a construir esos canales en el MVP; solo deja el catalogo abierto para cuando se decida incorporarlos.
5. **Nombres y codigos.** Todos los codigos y nombres de modulo usados en esta ficha (MOD-001 a MOD-026) y los 12 roles estandar citados en las secciones B y C corresponden exactamente a los de `mapa_modulos.json` y a `05_tipos_de_usuario.md`, seccion 5.3, respectivamente; no se introdujo ningun nombre alternativo.
6. Ningun otro desacuerdo material se detecto entre esta ficha y las fuentes de diseno ya decididas (`02_validacion_de_la_idea.md`, `04_objetivo_exacto_del_producto.md`, `05_tipos_de_usuario.md`, `22_anti_features.md`, `06_mapa_definitivo_de_modulos.md`, `mapa_modulos.json`). Toda afirmacion juridica de esta ficha cita su OBL-ID y su articulo segun `01_legal/matriz_obligaciones.json`; donde la ley es ambigua (por ejemplo, el computo del plazo de 72 horas que MOD-022 tambien anuncia), esta ficha remite al criterio conservador ya fijado por MOD-013 y MOD-021, sin proponer uno nuevo.

