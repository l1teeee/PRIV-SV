# MODULO: Consentimiento

Codigo corto del modulo: MOD-007
Clasificacion global del modulo: MUST HAVE
Obligaciones que cubre:

- Propias (12): OBL-CONS-01, OBL-CONS-02, OBL-CONS-03, OBL-CONS-04, OBL-CONS-05, OBL-CONS-06, OBL-PRIN-01, OBL-PRIN-04, OBL-SENS-02, OBL-SENS-03, OBL-SENS-07, OBL-TRAT-02
- Colaboradoras (6, propietario en otro modulo, este modulo las usa o refuerza): OBL-PRIN-02 (propietario MOD-006), OBL-SENS-01 (propietario MOD-006), OBL-SENS-04 (propietario MOD-006), OBL-SENS-06 (propietario MOD-006), OBL-TRANSF-04 (propietario MOD-010), OBL-TRAT-01 (propietario MOD-006)

Fecha de referencia: 2026-09-24. Fuentes: `mapa_modulos.json` (entrada MOD-007), `06_mapa_definitivo_de_modulos.md`, `01_legal\matriz_obligaciones.json`, `01_legal\03_hallazgos_regulatorios.md`, `02_validacion_de_la_idea.md` (seccion 2.7), `04_objetivo_exacto_del_producto.md`, `05_tipos_de_usuario.md`, `22_anti_features.md`.

---

## A. Proposito

- **Por que existe.** La LPDP exige que, cuando una empresa elige el consentimiento como base juridica para tratar datos de una persona, ese consentimiento cumpla requisitos precisos (expreso, libre, especifico, informado, individualizado, Arts. 26 y 27, OBL-CONS-01) y que la empresa pueda demostrarlo despues, porque la carga de la prueba es suya (Art. 54, OBL-CONS-05). Sin un registro estructurado, la empresa solo tiene "confio en que alguien lo pidio", lo cual no sirve como evidencia ante la Agencia de Ciberseguridad del Estado (ACE) ni ante un reclamo del titular.
- **Que problema resuelve para la empresa.** Convierte un acto que hoy suele quedar disperso (una casilla marcada en un formulario web, una hoja firmada en papel, una grabacion de call center) en un registro unico, con fecha, medio, texto exacto y version del aviso vigente en ese momento, y en un flujo de revocacion con plazos calculados automaticamente en vez de un correo suelto que nadie cronometra.
- **Que obligacion u obligaciones cubre.** Ver la lista de OBL-ID al inicio de esta ficha. Las de mayor riesgo son OBL-CONS-01 a OBL-CONS-04 (Arts. 26, 27, 29 y 30 LPDP), clasificadas como infraccion muy grave (26 a 40 salarios minimos, Art. 56 lit. c num. 1, 9 y 10) segun la tabla de infracciones de `03_hallazgos_regulatorios.md` seccion 6.
- **Que valor aporta.**
  - Operativo: convierte la captura y la revocacion del consentimiento en un flujo con pasos y plazos, en vez de un campo de fecha suelto (decision 2.7 punto 12 de `02_validacion_de_la_idea.md`).
  - Probatorio: conserva el texto exacto mostrado, la version del aviso y el medio de captura, que es exactamente lo que exige la carga de la prueba del Art. 54 (OBL-CONS-05).
  - De reduccion de riesgo: fuerza el regimen reforzado (firma, advertencia, alternativa no biometrica) cuando el dato es sensible o biometrico, y el sub-flujo parental cuando el titular es nino, nina o adolescente (NNA), evitando la infraccion muy grave del Art. 56 lit. c num. 3.
- **Que NO hace este modulo (limites explicitos).**
  - No decide si el consentimiento es la base juridica correcta para un tratamiento: esa eleccion se hace en el Registro de Actividades de Tratamiento (RAT, MOD-006); este modulo solo se activa cuando esa base ya fue elegida alli (Art. 5 lit. g, seis bases de licitud, OBL-PRIN-02, decision de que "no todo tratamiento requiere consentimiento", area 16 y 19 del documento maestro).
  - No redacta ni versiona el Aviso de Privacidad; solo referencia, sin copiar, la version vigente que administra MOD-008 (regla de "direccion unica", seccion 4 punto 7 de `06_mapa_definitivo_de_modulos.md`).
  - No juzga si el consentimiento fue realmente "libre" en una relacion de subordinacion (por ejemplo, biometria de marcaje laboral); solo deja constancia de que se ofrecio una alternativa no biometrica (ver seccion H).
  - No ejecuta tecnicamente la baja del titular en sistemas externos de marketing o CRM del cliente; solo registra la revocacion y crea la tarea correspondiente (el producto no es un CRM, anti-feature 1 de `22_anti_features.md`).
  - No emite ni envia por si mismo la notificacion al encargado tras una revocacion: la calcula, la redacta y la deja pendiente de aprobacion de la persona con el rol "responsable del tramite" (ver seccion H).

## B. Usuarios

Roles segun los 12 estandar de `05_tipos_de_usuario.md`, seccion 5.3:

| Rol | Para que usa este modulo |
|---|---|
| Administrador de la organizacion | Activa el modulo, configura si aplica el sub-flujo de menores de edad (segun lo detectado en el diagnostico), revisa el resumen general |
| Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | Aprueba cada notificacion de revocacion antes de que se emita (al encargado o al titular), revisa los casos de consentimiento sensible, biometrico o parental, es el enlace institucional si la ACE consulta un caso |
| Responsable ARCO-POL / Responsable del tramite | Recibe y da seguimiento a las solicitudes de revocacion que llegan por el canal ARCO-POL o por otro canal habilitado, coordina el cronometro de 5 mas 5 dias habiles |
| Responsable Legal / Compliance | Revisa si una excepcion al consentimiento (Art. 28, o Arts. 37 a 38 para sensibles) esta bien invocada, resuelve dudas sobre el sub-flujo NNA, aprueba el texto juridico de las plantillas de consentimiento antes de publicarlas |
| Responsable de Seguridad / IT | Registra el consentimiento biometrico asociado a sistemas de control de acceso o de asistencia, coordina con Proveedores cuando el sistema biometrico lo opera un tercero |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Captura el consentimiento en el punto donde ocurre (por ejemplo, RRHH al instalar un lector biometrico, Marketing al recolectar datos para boletines), y recibe revocaciones que le llegan directamente por su canal |
| Aprobador | Aprueba el texto de una plantilla de consentimiento reforzado (sensible, biometrico, parental) antes de que quede activa para su uso |
| Auditor (interno) | Consulta, sin poder editar, el registro de consentimientos y revocaciones como parte de la auditoria anual de cumplimiento (OBL-AUD-01) |
| Auditor externo (invitado) | Accede en modo lectura, por invitacion temporal, al paquete de evidencia de consentimientos durante una auditoria puntual |
| Usuario de consulta / Colaborador | Completa la tarea puntual que se le asigna (por ejemplo, "recolectar la firma del formulario en papel y adjuntarla") sin ver el resto del modulo |
| Titular (formulario externo) | En el MVP no tiene una pantalla propia dentro de este modulo; presenta su solicitud de revocacion por el formulario interno seguro de MOD-011 o por el mismo canal donde otorgo el consentimiento, y el personal interno la registra aqui (no existe portal publico dedicado en el MVP, decision 2.7.30) |
| Asesor externo invitado | Accede de forma puntual y acotada a un caso especifico (por ejemplo, para dictaminar si una excepcion al consentimiento aplica a un tratamiento concreto), nunca a todo el modulo |

## C. Permisos

Leyenda de columnas: ADM = Administrador de la organizacion; DPO = Delegado / Responsable interno; ARCO = Responsable ARCO-POL; LEG = Responsable Legal/Compliance; SEG = Responsable de Seguridad/IT; AREA = Responsable de area; APR = Aprobador; AUDI = Auditor interno; AUDE = Auditor externo; COL = Usuario de consulta/Colaborador; TIT = Titular; ASE = Asesor externo.

| Accion | ADM | DPO | ARCO | LEG | SEG | AREA | APR | AUDI | AUDE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver | Si | Si | Si | Si | Si (lo propio) | Si (lo propio) | Si | Si (solo lectura) | Si (solo lectura, temporal) | Solo lo asignado | No (no hay pantalla propia en MVP) | Si (solo el caso invitado) |
| Crear (registrar consentimiento) | No | Si | Si | No | Si (lo propio) | Si (lo propio) | No | No | No | No | No | No |
| Modificar (antes de vigente) | No | Si | Si | No | Si (lo propio) | Si (lo propio) | No | No | No | No | No | No |
| Aprobar (plantilla o notificacion) | No | Si | No | Si (plantillas) | No | No | Si (plantillas) | No | No | No | No | No |
| Cerrar (revocacion) | No | Si | Si | No | No | No | No | No | No | No | No | No |
| Eliminar / archivar | No | No | No | No | No | No | No | No | No | No | No | No |
| Exportar | Si (resumen) | Si | Si | Si | No | No | No | Si | Si (su caso) | No | No | No |
| Asignar (tarea de captura o revocacion) | Si | Si | Si | No | No | No | No | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | No | No | No | No | Si (su caso) |
| Adjuntar evidencia (firma, documento) | No | Si | Si | No | Si | Si | No | No | No | Si (si se le asigna) | No | No |

Separacion de funciones:
- Quien captura un consentimiento sensible o biometrico (Responsable de area, IT) no puede ser quien apruebe la plantilla que uso para capturarlo (Aprobador); son roles distintos por diseno.
- El registro de consentimientos y revocaciones es de solo escritura por adicion (append-only): ningun rol, incluido Administrador, puede eliminar un registro ya creado, solo archivarlo por sustitucion (ver seccion F), en linea con el anti-feature 19 de `22_anti_features.md`.
- Auditor (interno y externo) nunca puede crear, modificar ni aprobar, solo ver y exportar, para que su verificacion sea independiente (regla de `05_tipos_de_usuario.md`, seccion 5.4).
- El cierre de una revocacion que involucra datos sensibles o un reclamo potencial ante la Direccion de Proteccion de Datos de la ACE exige la aprobacion explicita del Delegado o Responsable interno antes de notificar al titular o al encargado; el sistema nunca la emite de forma automatica (ver seccion H).

## D. Informacion de entrada

Este modulo tiene dos entidades principales: **Consent** (el consentimiento otorgado) y **ConsentWithdrawal** (la revocacion). A diferencia de RAT, Inventario y Proveedores, el principio de minimizacion de datos por diseno (Art. 5 lit. d) no se acota aqui a metadatos: por decision expresa de alcance (`02_validacion_de_la_idea.md`, seccion 2.7, punto 21), Consentimiento procesa datos del titular como objeto legitimo del proceso, igual que ARCO-POL e Incidentes, porque sin identificar minimamente al titular y conservar el texto que acepto no se puede probar el Art. 54 (OBL-CONS-05). Aun asi, el modulo minimiza en el sentido correcto: guarda solo el dato de identificacion necesario para esa prueba (nombre y un identificador de referencia), nunca copia el perfil completo del titular desde el CRM o el sistema del cliente (anti-feature 1 y 8 de `22_anti_features.md`), y nunca almacena el dato sensible en si (por ejemplo, la plantilla biometrica), solo la evidencia de que se pidio consentimiento para tratarlo (anti-feature 9).

### D.1 Consent (registro de consentimiento)

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Tratamiento asociado | Referencia (a Treatment de MOD-006) | Obligatorio desde el alta | Lista de tratamientos del RAT cuya base juridica = "Consentimiento" | Debe existir en el RAT con esa base juridica; si el tratamiento cambia de base, el sistema advierte y no permite nuevos consentimientos bajo ese tratamiento | "Elija el tratamiento para el que esta pidiendo el consentimiento. Solo aparecen los que su RAT ya marco como basados en consentimiento." | OBL-PRIN-02 (Art. 5 lit. g), propietario MOD-006 |
| Finalidad(es) cubiertas | Seleccion multiple (de las finalidades declaradas en el tratamiento) | Obligatorio | Catalogo heredado del tratamiento en RAT | Al menos una finalidad seleccionada; no se permite anadir una finalidad que no este en el RAT | "Marque para que fin especifico esta pidiendo permiso, por ejemplo enviar boletines o verificar identidad." | OBL-PRIN-01 (Art. 5 lit. c), OBL-CONS-01 (Art. 26-27) |
| Categorias de datos cubiertas | Lista (heredada del RAT) | Se precarga, no editable aqui | Catalogo de categorias del RAT (incluye marca "sensible"/"biometrico" heredada) | Solo lectura | "Estas son las categorias de datos que su RAT ya declaro para este tratamiento." | OBL-SENS-01, OBL-SENS-06 (propietario MOD-006) |
| Tipo de consentimiento | Seleccion unica | Obligatorio | General / Sensible reforzado / Biometrico / Parental (NNA) | Se calcula automaticamente a partir de las categorias de datos heredadas; el usuario puede confirmarlo pero no bajar el nivel de refuerzo | "El sistema detecto que categoria de dato aplica y ajusto los campos siguientes; no puede tratarse un dato sensible con el formulario general." | OBL-CONS-04, OBL-SENS-07 |
| Titular (identificacion minima) | Texto (nombre) + referencia (identificador externo del cliente, por ejemplo correo o ID de su propio sistema) | Obligatorio | Libre, con formato de correo o identificador valido | No se permite copiar campos adicionales del titular (direccion, telefono, etc.) salvo que el canal de captura los incluya como parte del propio texto aceptado | "Registre solo el nombre y un identificador con el que usted reconoce a esta persona en sus propios sistemas; no copie aqui su ficha completa de cliente o empleado." | OBL-CONS-05 (Art. 54); decision de alcance 2.7.21 |
| Titular es NNA | Booleano | Obligatorio | Si / No | Si es "Si", activa el sub-flujo parental (campos siguientes) | "Marque si la persona es nina, nino o adolescente segun la informacion que usted tiene." | OBL-CONS-06, OBL-PRIN-04 (Art. 5 lit. j, Art. 42) |
| Nombre del padre, madre o tutor que consiente | Texto | Obligatorio si Titular es NNA = Si | Libre | No vacio | "Registre el nombre de quien esta autorizando en nombre del menor." | OBL-CONS-06 (Art. 56 lit. c num. 3) |
| Relacion o parentesco declarado | Seleccion unica | Obligatorio si Titular es NNA = Si | Padre / Madre / Tutor legal / Representante legal | - | "Indique la relacion de quien autoriza con el menor." | OBL-CONS-06 |
| Evidencia de la relacion | Archivo | Recomendado si Titular es NNA = Si | PDF, imagen | Tamano y formato validos | "Adjunte, si lo tiene, un documento que respalde la relacion (por ejemplo partida de nacimiento). Si no lo tiene, puede continuar dejando constancia de que no se adjunto." | OBL-CONS-06; buena practica |
| Medio o canal de captura | Seleccion unica | Obligatorio | Formulario web / Casilla en aplicacion / Documento fisico firmado / Verbal grabado / Otro (especificar) | - | "Elija como la persona dio su consentimiento." | OBL-CONS-01 (Art. 26, medios verbal/escrito/signos inequivocos) |
| Fecha y hora de captura | Fecha y hora | Obligatorio, se genera automaticamente al guardar | - | No puede ser futura | "Se registra automaticamente el momento exacto en que se guardo este consentimiento." | OBL-CONS-01, OBL-CONS-05 |
| Texto exacto presentado al titular | Texto largo (snapshot inmutable) | Obligatorio | - | No editable despues de guardado; se conserva version por version si el texto cambia | "Este es el texto exacto que la persona vio y acepto. Una vez guardado no se puede modificar, solo crear una version nueva." | OBL-CONS-01, OBL-CONS-05 |
| Version del Aviso de Privacidad vigente | Referencia (a documento versionado de MOD-008) | Obligatorio | Version publicada mas reciente al momento de la captura | Debe existir una version publicada del Aviso; si no existe, el sistema bloquea la captura y crea alerta | "El sistema toma automaticamente la version del Aviso de Privacidad que estaba vigente en el momento de este consentimiento; nunca se sustituye por versiones posteriores." | OBL-CONS-05 (Art. 54); decision 2.7 punto 6 (referencia, nunca copia) |
| Firma o evidencia de aceptacion | Archivo (firma escaneada o electronica) o booleano con sello de tiempo (clic con IP) segun el canal | Obligatorio si tipo = Sensible, Biometrico o Parental; opcional si tipo = General y canal es digital con registro de clic | Firma autografa escaneada / firma electronica valida / registro de aceptacion digital con fecha e IP | Para tipo Sensible/Biometrico/Parental, el sistema no permite guardar sin un archivo de firma adjunto | "Para datos sensibles o biometricos la ley exige firma; adjunte la firma en papel escaneada o utilice la firma electronica disponible. Un simple clic no es suficiente para estos casos." | OBL-CONS-04 (Art. 26 inc. 4) |
| Direccion IP / dispositivo | Texto | Opcional (solo si el canal es digital y es pertinente) | - | Formato de IP valido si se captura | "Si el consentimiento se dio por un medio digital, el sistema puede guardar esta informacion tecnica como respaldo adicional." | Buena practica, mencionada en documento maestro seccion 19 |
| Advertencia de derecho a no proporcionar el dato mostrada | Booleano | Obligatorio si tipo = Sensible o Biometrico | Si / No | El sistema no permite continuar sin marcar este campo cuando el tipo lo exige | "Confirme que se le informo a la persona que puede negarse a dar este dato sensible sin que eso la perjudique de forma indebida." | OBL-SENS-02 (Art. 37 inc. 1) |
| Alternativa no biometrica ofrecida | Booleano + texto breve (descripcion de la alternativa) | Obligatorio si tipo = Biometrico | Si / No + descripcion | Si es "No", el sistema muestra advertencia de riesgo (ver seccion H), pero permite continuar dejando constancia | "Indique si ademas del metodo biometrico se ofrecio una forma alternativa de identificarse (por ejemplo tarjeta o PIN)." | OBL-SENS-07 (Art. 26 inc. 4, Art. 37); recomendacion de diseno, no mandato legal expreso |
| Excepcion invocada en lugar de consentimiento | Seleccion unica (catalogo) | Condicional: solo si este registro documenta una excepcion en vez de un consentimiento otorgado | 8 supuestos del Art. 28 (fuente de acceso publico, contrato, obligacion legal, etc.) o 3 excepciones de datos sensibles (Arts. 37-38: salvaguarda de vida, secreto profesional de salud, interes general por ley) | Si se selecciona, el campo "firma" y "advertencia" quedan opcionales, pero se exige campo "justificacion" | "Si no se necesita consentimiento porque aplica una excepcion legal, selecciónela aqui y explique por que aplica a este caso." | OBL-TRAT-02 (Art. 28), OBL-SENS-03 (Art. 37-38) |
| Justificacion de la excepcion | Texto largo | Obligatorio si se selecciono una excepcion | - | No vacio | "Explique en sus palabras por que este caso concreto cae dentro de la excepcion seleccionada." | OBL-TRAT-02, OBL-SENS-03; recuerda que "requiere validacion de la organizacion o asesoria especializada" (ver seccion H) |
| Estado | Seleccion (gestionado por el sistema) | Se genera automaticamente | Presentado / No otorgado / Vigente / Revocado / Expirado / Sustituido | No editable manualmente, solo por transiciones de workflow (ver seccion F) | "Aqui ve en que etapa esta este consentimiento." | Control interno |
| Notas internas | Texto largo | Opcional | - | - | "Espacio libre para anotaciones internas, no visible para el titular." | Buena practica |

### D.2 ConsentWithdrawal (revocacion)

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Consentimiento de origen | Referencia (a Consent) | Obligatorio | Consentimientos en estado Vigente del mismo titular | Debe estar en estado Vigente al momento de crear la revocacion | "Seleccione el consentimiento que la persona quiere retirar." | OBL-CONS-02 (Art. 29) |
| Fecha y hora de recepcion de la solicitud | Fecha y hora | Obligatorio, se precarga con la fecha de creacion del registro pero es editable si la solicitud se recibio antes por otro canal (por ejemplo una carta fisica) | - | No puede ser futura | "Registre cuando la persona pidio la revocacion, aunque el registro en el sistema se haga despues." | OBL-CONS-03 (Art. 30), inicia el contador de 5 dias habiles |
| Canal de la revocacion | Seleccion unica | Obligatorio | Mismo canal del consentimiento original / Formulario ARCO-POL / Correo / Presencial / Otro | - | "La ley exige que revocar sea tan facil como otorgar; indique por donde llego la solicitud." | OBL-CONS-02 (mecanismo expedito, sencillo y gratuito) |
| Motivo declarado por el titular | Texto largo | Opcional | - | - | "Si la persona explico por que retira su consentimiento, puede anotarlo aqui; no es obligatorio pedirlo." | Buena practica |
| Fecha limite para ejecutar (calculada) | Fecha (calculada por MOD-023) | Se genera automaticamente | - | Recepcion + 5 dias habiles, segun calendario de MOD-023 | "El sistema calculo esta fecha limite usando el calendario de dias habiles vigente." | OBL-CONS-03 (Art. 30) |
| Fecha de ejecucion real | Fecha | Obligatorio al cerrar el paso de ejecucion | - | No puede ser posterior a mas de la fecha limite sin quedar marcada en alerta de vencido | "Fecha en la que efectivamente se dejo de tratar el dato para la finalidad revocada." | OBL-CONS-03 |
| Encargados a notificar | Referencia multiple (a Proveedores/Encargados de MOD-009 vinculados al tratamiento) | Obligatorio si el tratamiento tiene al menos un encargado registrado en MOD-009; si no tiene, el sistema lo marca "no aplica" y lo justifica automaticamente | Lista de encargados de MOD-009 asociados al mismo tratamiento | El sistema no permite cerrar la revocacion si hay encargados asociados al tratamiento y ninguno fue marcado como notificado o "no aplica" justificado | "Si un proveedor tambien trata estos datos por encargo suyo, debe avisarle de esta revocacion." | OBL-CONS-04 (Art. 30, segundo tramo) |
| Fecha limite de notificacion al encargado (calculada) | Fecha (calculada por MOD-023) | Se genera automaticamente cuando hay encargados | - | Fecha de resolucion/ejecucion + 5 dias habiles | "El sistema calculo esta segunda fecha limite para avisar a su proveedor." | OBL-CONS-03, OBL-CONS-04 |
| Persona que aprueba y ejecuta | Referencia (a usuario con rol Delegado/Responsable interno segun el estado vigente de MOD-024) | Obligatorio antes de pasar a Ejecutada | Usuarios con el rol vigente segun la bandera de MOD-024 | El sistema solo ofrece usuarios con el rol correcto para el estado regulatorio activo | "Esta accion debe quedar aprobada por la persona que hoy tiene la funcion legal de tramitar revocaciones en su organizacion." | Art. 30 (atribuido hoy al Delegado); notas_reforma_659 de MOD-007 |
| Evidencia de ejecucion | Archivo (opcional) | Opcional | - | - | "Si tiene una constancia de que se detuvo el tratamiento (por ejemplo una captura de pantalla de la baja en un sistema), adjuntela aqui." | OBL-CONS-05 (Art. 54) |
| Estado | Seleccion (gestionado por el sistema) | Se genera automaticamente | Recibida / Ejecutada / Encargado notificado / Cerrada / Vencida | No editable manualmente | "Aqui ve en que etapa esta esta revocacion." | Control interno |

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Registro de consentimiento (Consent) | Todos los campos de D.1, con estado actualizado | Registro interno con historial | Al guardar el formulario de captura | Queda disponible para ARCO-POL, Proveedores y Centro de Evidencias |
| Registro de revocacion (ConsentWithdrawal) | Todos los campos de D.2, con historial de estados y fechas | Registro interno con historial | Al recibir una solicitud de revocacion | Responsable ARCO-POL, Delegado/Responsable interno, Proveedores (tarea) |
| Tarea "capturar consentimiento" | Tratamiento, finalidad, tipo requerido (general/reforzado/biometrico/parental), fecha limite si aplica | Tarea en MOD-021 | Cuando el RAT marca un tratamiento con base = consentimiento y aun no existe registro Consent vigente para ese titular/finalidad | Responsable de area asignado al tratamiento |
| Tarea "procesar revocacion" | Consentimiento de origen, fecha limite (5 dias habiles) | Tarea en MOD-021 | Al crear un registro ConsentWithdrawal | Responsable ARCO-POL, con copia a Delegado/Responsable interno |
| Tarea "notificar a encargado" | Encargado(s), fecha limite (5 dias habiles adicionales) | Tarea en MOD-021, dirigida a MOD-009 | Al ejecutar la revocacion, si hay encargados asociados | Responsable de Proveedores / Responsable de Seguridad-IT |
| Alertas de plazo | Ver tabla de la seccion I | Notificacion (plataforma / correo) | Segun disparadores de la seccion I | Rol correspondiente, con escalamiento |
| Indicador "consentimientos vigentes por finalidad" | Conteo por finalidad y tipo | Dato de dashboard | Actualizacion continua | Vistas Gerencia, Responsable, Legal, Auditor (seccion M) |
| Indicador "revocaciones en curso" | Conteo por estado y dias restantes | Dato de dashboard, con semaforo | Actualizacion continua | Vistas Responsable y Legal |
| Snapshot inmutable de evidencia | Texto exacto + version del aviso + archivo de firma + hash | Paquete de evidencia | Al capturar el consentimiento y en cada exportacion | Centro de Evidencias (MOD-019) |
| Evento de auditoria | Cada creacion, cambio de estado, aprobacion, exportacion, acceso de lectura a un archivo de firma | Entrada en AuditLog (append-only) | En cada accion relevante | Auditoria transversal, Auditor |
| Entrada en la lista de supresion de marketing | Titular, finalidad de marketing revocada | Referencia enlazada con MOD-011 | Cuando la revocacion cubre una finalidad de marketing directo | Responsable de Marketing, ARCO-POL |

## F. Workflow

Este modulo tiene dos maquinas de estados independientes pero enlazadas: la del consentimiento (Consent) y la de su revocacion (ConsentWithdrawal).

### F.1 Estados del consentimiento (Consent)

```
[Tratamiento con base = Consentimiento en el RAT, sin registro vigente]
                         |
                         v
                  +-------------+
                  | PRESENTADO  |   (texto y version del aviso mostrados al titular)
                  +-------------+
                    |          |
          titular   |          |  titular declina
          acepta     v          v
          y firma  +--------+  +---------------+
          si aplica| VIGENTE|  | NO_OTORGADO   |  (terminal; sirve para probar OBL-SENS-02)
                    +--------+  +---------------+
                      |    |
        titular       |    | vence la finalidad
        revoca        |    | (si el RAT declara plazo)
                       v    v
                +-----------+  +-----------+
                | REVOCADO  |  | EXPIRADO  |
                +-----------+  +-----------+
                       |              |
                       +------+-------+
                              |
                se otorga un nuevo consentimiento
                para la misma finalidad
                              |
                              v
                     (nuevo registro VIGENTE;
                      este registro pasa a SUSTITUIDO,
                      archivado, nunca borrado)
```

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (sin registro) | Se crea el borrador de captura | El tratamiento debe existir en el RAT con base = Consentimiento | Presentado | Responsable ARCO-POL, Responsable de area, Delegado/Responsable interno | Se toma el snapshot del texto y de la version vigente del Aviso |
| Presentado | El titular acepta (y firma si el tipo lo exige) | Si tipo = Sensible, Biometrico o Parental, debe existir archivo de firma adjunto (D.1) | Vigente | El mismo rol que capturo | Se genera evidencia inmutable; se crea evento de auditoria; si es NNA, exige campos parentales completos |
| Presentado | El titular declina | - | No otorgado | El mismo rol que capturo | Se conserva como evidencia de que se advirtio el derecho a no dar el dato (OBL-SENS-02); no se guarda el dato sensible en si |
| Vigente | Se recibe y ejecuta una revocacion (ver F.2) | La revocacion asociada debe llegar al estado Ejecutada | Revocado | Automatico, disparado por el cierre del paso "Ejecutada" en F.2 | Se detiene el uso de ese consentimiento para nuevas finalidades; queda visible en el historial |
| Vigente | Vence la finalidad declarada en el RAT (si tiene plazo) | El RAT debe tener una fecha de vigencia declarada para esa finalidad | Expirado | Automatico (motor de plazos, MOD-023) | Se crea tarea de revision al Responsable de area |
| Revocado / Expirado | Se otorga un nuevo consentimiento para la misma finalidad | Debe pasar por el flujo completo de Presentado -> Vigente | Sustituido (el registro anterior) / Vigente (el nuevo registro) | Responsable ARCO-POL, Responsable de area | El registro anterior queda archivado, enlazado al nuevo por referencia; nunca se edita ni se borra |

Estados terminales: No otorgado, Sustituido. Reapertura: no existe reapertura de un registro cerrado; cualquier nuevo consentimiento crea un registro nuevo, preservando el historial completo (append-only, anti-feature 19). Si el tratamiento asociado se elimina o se archiva en el RAT, los registros de Consent quedan archivados junto con el, sin eliminarse, para conservar evidencia historica.

### F.2 Estados de la revocacion (ConsentWithdrawal)

```
[Solicitud de revocacion recibida por cualquier canal habilitado]
                         |
                         v
                  +--------------+
                  | RECIBIDA     |   inicia contador de 5 dias habiles (MOD-023)
                  +--------------+
                         |
        Delegado/Responsable interno valida y aprueba
                         v
                  +--------------+
                  | EJECUTADA    |   se deja de tratar el dato para esa finalidad
                  +--------------+
                         |
              hay encargados registrados en MOD-009
              para ese tratamiento?
                    si  |   | no
                        v   v
             +-----------------+   +-----------+
             | ENCARGADO       |   | CERRADA   |
             | NOTIFICADO      |   +-----------+
             +-----------------+
                         |
       (otros 5 dias habiles desde la fecha de ejecucion)
                         v
                  +-----------+
                  | CERRADA   |
                  +-----------+

  En cualquier estado antes de Cerrada, si se supera la fecha limite
  sin avanzar: -> VENCIDA (no bloquea la ejecucion, pero queda marcada
  en el historial y dispara alerta CRITICAL, ver seccion I)
```

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (sin registro) | Se registra la solicitud de revocacion | Debe existir un Consent en estado Vigente para ese titular/finalidad | Recibida | Responsable ARCO-POL, Responsable de area | Se calcula fecha limite (recepcion + 5 dias habiles); se crea tarea y evento de auditoria |
| Recibida | Se valida y se deja de tratar el dato | Requiere aprobacion del Delegado/Responsable interno vigente (ver seccion H) | Ejecutada | Delegado/Responsable interno | Actualiza el Consent origen a Revocado; registra fecha de ejecucion |
| Ejecutada | Se notifica al encargado registrado | Solo si existen encargados asociados al tratamiento en MOD-009 | Encargado notificado | Delegado/Responsable interno (aprueba el envio) | Crea tarea en MOD-009; calcula fecha limite (ejecucion + 5 dias habiles) |
| Ejecutada (sin encargados) | Se verifica que no existen encargados asociados | El sistema no permite cerrar sin esta verificacion explicita si el tratamiento tiene proveedores en general | Cerrada | Automatico, con confirmacion del Responsable ARCO-POL | Cierra el expediente de revocacion |
| Encargado notificado | Se confirma la notificacion (evidencia de envio) | - | Cerrada | Responsable ARCO-POL, Delegado/Responsable interno | Cierra el expediente; queda evidencia completa para MOD-019 |
| Recibida / Ejecutada / Encargado notificado | Se supera la fecha limite correspondiente sin avanzar | Automatico por el motor de plazos | Vencida (marca adicional, no bloquea el avance posterior) | Automatico | Genera alerta CRITICAL y escalamiento (ver seccion I); queda registrado en el historial como incumplimiento de plazo |

Estado terminal: Cerrada. No existe "reapertura" de una revocacion cerrada: si el titular vuelve a otorgar consentimiento despues, se crea un nuevo registro Consent (ver F.1), enlazado por referencia al expediente de revocacion anterior para trazabilidad, nunca reescribiendolo.

## G. Automatizaciones

Todas las reglas siguientes son configurables por la empresa en el alcance que se indica (activar/desactivar el sub-flujo, ajustar umbrales de alerta), nunca en el calculo del plazo legal en si, que siempre usa el motor central de MOD-023.

| # | Disparador | Condicion | Accion | Configurable |
|---|---|---|---|---|
| 1 | El RAT marca un tratamiento con base juridica = Consentimiento | No existe un registro Consent vigente para ese tratamiento y ese titular | Crear tarea "capturar consentimiento" en MOD-021, asignada al Responsable de area del tratamiento | Si, el responsable por defecto es configurable |
| 2 | Se inicia la captura de un consentimiento | La categoria de dato heredada del RAT es sensible o biometrica | Bloquear el guardado hasta que se adjunte firma y se marque la advertencia del Art. 37 (campos obligatorios de D.1) | No (es una validacion legal minima) |
| 3 | Se marca "Titular es NNA = Si" | - | Activar los campos del sub-flujo parental y exigirlos antes de guardar | No (activacion condicional por dato, no desactivable si el diagnostico detecto tratamiento de menores) |
| 4 | Se registra una solicitud de revocacion | - | Calcular la fecha limite de ejecucion (recepcion + 5 dias habiles, via MOD-023) y crear tarea al Responsable ARCO-POL y al Delegado/Responsable interno | No en el calculo del plazo; si en el destinatario de la tarea |
| 5 | Se ejecuta una revocacion | El tratamiento tiene al menos un encargado registrado en MOD-009 | Calcular la fecha limite de notificacion (ejecucion + 5 dias habiles) y crear tarea hacia Proveedores | No en el calculo del plazo |
| 6 | Falta 1 dia habil para vencer un plazo de revocacion (5 o 5+5) | El expediente sigue en Recibida, Ejecutada o Encargado notificado | Generar alerta WARNING; si vence sin avanzar, escalar a CRITICAL (ver seccion I) | Si, el umbral de dias de anticipacion es configurable |
| 7 | Se otorga un nuevo consentimiento para una finalidad que ya tenia uno vigente | - | Archivar el registro anterior como Sustituido y enlazarlo al nuevo; nunca sobrescribir ni borrar | No |
| 8 | Se revoca un consentimiento cuya finalidad incluye marketing directo | - | Anadir al titular a la lista de supresion de marketing enlazada con la oposicion de MOD-011 (faltante 29 de `02_validacion_de_la_idea.md`) | Si, activable por tipo de finalidad |
| 9 | Cambia la bandera de estado regulatorio en MOD-024 (reforma 659) | Hay una revocacion pendiente de aprobacion | El campo "persona que aprueba y ejecuta" (D.2) se recalcula segun el rol vigente (Delegado o Responsable interno); los expedientes ya cerrados conservan el rol que aplicaba cuando se cerraron | No (regla estructural del doble estado, ver seccion 5 de `06_mapa_definitivo_de_modulos.md`) |
| 10 | El RAT declara una fecha de vigencia para la finalidad de un tratamiento y esa fecha se cumple | El consentimiento sigue en estado Vigente | Marcarlo Expirado y crear tarea de revision al Responsable de area | Si, activable si la empresa usa vigencias por finalidad |

## H. Decisiones que NO debe automatizar

Cada una de estas decisiones muestra en pantalla el texto: **"Requiere validacion de la organizacion o asesoria especializada"**.

1. **Si una base juridica distinta al consentimiento es defendible para un tratamiento concreto.** El Art. 5 lit. g ofrece seis bases alternativas y el propio corpus juridico documenta una contradiccion abierta entre el consentimiento como "regla general" (Arts. 5 lit. c y 27) y su caracter de base entre varias (03_hallazgos_regulatorios.md, seccion 8, punto 1). El sistema registra la base elegida, nunca la valida.
2. **Si un adolescente (12 a 18 anos) puede autoconsentir bajo la Ley Crecer Juntos en vez de requerir consentimiento parental bajo la LPDP.** Es una tension normativa expresamente documentada como incertidumbre juridica (03_hallazgos_regulatorios.md, seccion 9, punto 8): el sistema siempre pide el flujo parental completo por defecto (criterio conservador) y muestra la tension como nota visible, nunca como una regla de edad cerrada.
3. **Si una excepcion invocada (Art. 28 o Arts. 37-38) aplica realmente al caso concreto.** El sistema solo ofrece el catalogo y pide la justificacion escrita; la validez de esa justificacion la evalua la persona responsable o su asesoria legal.
4. **Si el texto de consentimiento cumple los cinco atributos exigidos (libre, especifico, informado, expreso, individualizado).** El sistema verifica que los campos esten completos, no la calidad juridica de la redaccion; el Aprobador y Legal revisan el contenido antes de publicar una plantilla.
5. **Si un encargado ubicado fuera de El Salvador debe tratarse como transferencia internacional (Arts. 44-45) o como simple encargo de tratamiento.** Es una incertidumbre juridica documentada (03_hallazgos_regulatorios.md, seccion 9, punto 10); el sistema deja la clasificacion a criterio de la organizacion y remite al modulo de Transferencias cuando corresponda.
6. **Si el consentimiento sigue siendo "libre" en una relacion de subordinacion laboral** (por ejemplo, biometria de marcaje). El sistema solo registra si se ofrecio una alternativa no biometrica (campo de D.1); no concluye si eso hace al consentimiento valido.
7. **La aprobacion final de toda notificacion de revocacion**, tanto al encargado como, si corresponde, al titular. El sistema calcula el plazo y redacta el contenido, pero la emision queda pendiente de la aprobacion explicita de la persona con el rol Delegado o Responsable interno, segun el estado vigente de la reforma 659 (ver seccion G, regla 9).

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Consentimiento pendiente de captura | Tratamiento con base = Consentimiento sin registro vigente, X dias despues de creado en el RAT | INFO | Responsable de area | Plataforma | Una vez, recordatorio semanal si sigue pendiente | A Delegado/Responsable interno tras 15 dias sin captura | Se crea el registro Consent en estado Vigente o No otorgado |
| Consentimiento sensible incompleto | Registro en Presentado con tipo Sensible/Biometrico/Parental sin firma adjunta por mas de 2 dias | WARNING | Responsable de area, Delegado/Responsable interno | Plataforma y correo | Diaria mientras persista | A Administrador tras 5 dias | Se adjunta la firma o se marca No otorgado |
| Revocacion proxima a vencer (primer plazo) | Faltan 2 dias habiles para el limite de 5 dias habiles de ejecucion | WARNING | Responsable ARCO-POL, Delegado/Responsable interno | Plataforma y correo | Diaria los ultimos 2 dias | A Administrador si falta 1 dia | Se ejecuta la revocacion |
| Revocacion vencida (primer plazo) | Se supero el plazo de 5 dias habiles sin ejecutar | CRITICAL | Delegado/Responsable interno, Administrador | Plataforma, correo, resumen en dashboard Gerencia | Diaria hasta resolverse | Inmediato a Administrador y a Gerencia | Se ejecuta la revocacion (queda registrado el incumplimiento del plazo en el historial) |
| Notificacion a encargado proxima a vencer (segundo plazo) | Faltan 2 dias habiles para el limite de 5 dias habiles de notificacion | WARNING | Responsable de Proveedores/IT, Delegado/Responsable interno | Plataforma y correo | Diaria los ultimos 2 dias | A Administrador si falta 1 dia | Se notifica al encargado |
| Notificacion a encargado vencida (segundo plazo) | Se supero el plazo de 5 dias habiles de notificacion al encargado | CRITICAL | Delegado/Responsable interno, Administrador | Plataforma, correo | Diaria hasta resolverse | Inmediato a Administrador | Se notifica al encargado |
| Version de Aviso de Privacidad no disponible | Se intenta capturar un consentimiento y MOD-008 no tiene una version publicada del Aviso | CRITICAL | Delegado/Responsable interno, Administrador | Plataforma | Al momento del intento | Inmediato | Existe una version publicada del Aviso |
| Consentimiento biometrico sin alternativa ofrecida | Se guarda un consentimiento tipo Biometrico con "alternativa no biometrica ofrecida = No" | WARNING | Responsable de area, Responsable Legal | Plataforma | Una vez, al guardar | A Delegado/Responsable interno si se repite en el mismo tratamiento | Es informativa; no bloquea, queda como nota de riesgo permanente en el registro |

## J. Evidencia

- **Registro con fecha y hora, usuario y version del formulario:** cada Consent y cada ConsentWithdrawal guarda quien lo creo, cuando, y que version de los campos del formulario estaba activa, para poder explicar por que un registro antiguo tiene menos campos que uno nuevo.
- **Snapshot inmutable del texto y de la version del Aviso:** el texto exacto presentado y la version del Aviso de Privacidad quedan congelados en el momento de la captura; nunca se sustituyen aunque el Aviso cambie despues (evidencia directa de OBL-CONS-05, Art. 54).
- **Archivo adjunto con hash:** toda firma o documento adjunto (firma autografa escaneada, documento de relacion parental, evidencia de ejecucion de una revocacion) se guarda con un hash de integridad verificable, para poder demostrar que no fue alterado despues.
- **Historial de estados con marca de tiempo:** cada transicion de la seccion F queda registrada con fecha, hora, usuario y motivo cuando aplica (por ejemplo, "revocado por solicitud del titular, recibida el...").
- **Aprobacion con identidad y fecha:** la aprobacion del Delegado/Responsable interno antes de ejecutar o notificar una revocacion queda registrada con su identidad, fecha y el estado regulatorio vigente en ese momento (Delegado o Responsable interno).
- **Exportacion firmada:** todo paquete de evidencia que sale de este modulo hacia el Centro de Evidencias (MOD-019) incluye verificacion de integridad, para cumplir el anti-feature 25 de `22_anti_features.md`.

Que evidencia prueba cada obligacion:

| OBL-ID | Evidencia que la prueba |
|---|---|
| OBL-CONS-01 (Art. 26-27) | Registro con medio, texto exacto y fecha de captura |
| OBL-CONS-02 (Art. 29) | Existencia y facilidad del canal de revocacion, registro de revocaciones recibidas |
| OBL-CONS-03 (Art. 30) | Fecha de recepcion, fecha limite calculada y fecha de ejecucion real de cada revocacion |
| OBL-CONS-04 (Art. 30, segundo tramo) | Fecha de notificacion al encargado y evidencia de esa notificacion |
| OBL-CONS-05 (Art. 54) | El conjunto: snapshot del texto, version del aviso, medio, fecha, archivo de firma |
| OBL-CONS-06 (Art. 56 lit. c num. 3) | Registro del sub-flujo parental completo (nombre, relacion, evidencia si existe) |
| OBL-PRIN-01 (Art. 5 lit. c) | Finalidad y periodo declarados en el consentimiento, heredados del RAT |
| OBL-PRIN-04 (Art. 5 lit. j) | Marca de titular NNA y aplicacion del sub-flujo diferenciado |
| OBL-SENS-02 (Art. 37 inc. 1) | Campo "advertencia mostrada" en cada registro sensible o biometrico, incluidos los No otorgado |
| OBL-SENS-03 (Art. 37-38) | Excepcion seleccionada y justificacion escrita |
| OBL-SENS-07 (Art. 26 inc. 4, Art. 37) | Campo "alternativa no biometrica ofrecida" en cada consentimiento biometrico |
| OBL-TRAT-02 (Art. 28) | Excepcion seleccionada del catalogo de 8 supuestos y su justificacion |

Retencion: este modulo no define su propio plazo de conservacion, por la regla de "direccion unica" (un dato lo posee un solo modulo, seccion 4 punto 7 de `06_mapa_definitivo_de_modulos.md`); el plazo de conservacion del registro de consentimiento y de sus revocaciones lo fija MOD-016 Retencion, y este modulo solo aplica lo que ese modulo indique.

## K. Documentos asociados

- **Documentos requeridos como entrada:** version vigente del Aviso de Privacidad (de MOD-008), y, cuando aplica, la Politica de Privacidad publicada.
- **Documentos generados por este modulo:**
  - Snapshot del texto de consentimiento presentado (registro interno, no es un documento para publicar).
  - Constancia o acuse de revocacion (documento breve, si el canal lo requiere, para entregar al titular).
  - Borrador de notificacion al encargado tras una revocacion (dirigido a MOD-009, pendiente de aprobacion segun seccion H).
- **Plantillas que el sistema provee** (alojadas y versionadas como tipo de documento en MOD-008, usadas por referencia aqui, nunca copiadas):
  - Plantilla de clausula de consentimiento general (variables: nombre de la empresa, finalidad, periodo). Requiere validacion de la organizacion.
  - Plantilla de consentimiento sensible/biometrico (incluye advertencia del Art. 37, espacio de firma, campo de alternativa no biometrica). Requiere validacion de la organizacion y de asesoria legal.
  - Plantilla de consentimiento parental para NNA (lenguaje adaptado a la edad, Art. 42). Requiere validacion de la organizacion y de asesoria legal.
  - Plantilla de notificacion de revocacion al encargado. Requiere validacion de la organizacion.
- **Anexos y evidencias documentales:** firma escaneada o archivo de firma electronica, documento de relacion parental, evidencia de ejecucion de la revocacion.

## L. Dependencias

```
MOD-006 RAT y Mapa de Datos -----> MOD-007 CONSENTIMIENTO -----> MOD-009 Proveedores y Encargados
   (tratamiento, base juridica,        |        |                    (notificacion de revocacion)
    categoria de dato, finalidad)      |        |
                                       |        +---------------> MOD-011 ARCO-POL
MOD-008 Documentos y Politicas --------+        |                    (lista de supresion de marketing,
   (version vigente del Aviso)                  |                     consulta de consentimientos vigentes)
                                                 |
                                                 +---------------> MOD-019 Centro de Evidencias
                                                                      (evidencia de consentimientos
                                                                       y revocaciones)

Consultado de forma transversal (no es una entrada/salida de datos de negocio, es un servicio comun):
  MOD-002 Delegado / Responsable interno  -> quien aprueba cada revocacion, segun el estado vigente
  MOD-023 Calendario y Motor de Plazos    -> calculo de los plazos de 5 y 5+5 dias habiles
  MOD-021 Centro de Tareas                -> aloja las tareas que este modulo crea
  MOD-022 Notificaciones                  -> envia las alertas de la seccion I
  MOD-024 Centro Regulatorio              -> bandera de estado ACTUAL/FUTURO de la reforma 659
```

- **Entra desde:** MOD-006 (tratamiento, base juridica, categoria de dato, finalidad y su posible vigencia), MOD-008 (version del Aviso de Privacidad vigente, por referencia, nunca copiada).
- **Sale hacia:** MOD-009 (tarea de notificacion de revocacion a encargados), MOD-011 (enlace con la lista de supresion de marketing y con la verificacion de identidad ya hecha para un titular que tambien presenta una solicitud ARCO-POL), MOD-019 (evidencia continua).
- **Que ocurre si un modulo dependiente no existe en el MVP:** MOD-006 y MOD-008 son ambos MUST HAVE, por lo que esta dependencia esta cubierta desde el primer dia. Si MOD-009 no tuviera aun registrado un encargado para un tratamiento con proveedores reales, el modulo no bloquea la revocacion: la marca como "sin encargados registrados, verificar manualmente" y crea una tarea de alta en MOD-009 antes de permitir cerrar el expediente como completo.

## M. Dashboard

| Indicador | Formula | Semaforo | Vista |
|---|---|---|---|
| Consentimientos vigentes por finalidad | Conteo de Consent en estado Vigente, agrupado por finalidad | No aplica (informativo) | Gerencia (resumen), Responsable (detalle por su area), Legal (detalle completo) |
| Cobertura de captura | Tratamientos con base = Consentimiento en el RAT que ya tienen al menos un Consent vigente / total de tratamientos con esa base | Verde si 100%, amarillo si hay pendientes recientes, rojo si hay pendientes con mas de 15 dias | Responsable, Gerencia |
| Revocaciones dentro de plazo | ConsentWithdrawal cerradas dentro del plazo legal / total cerradas en el periodo | Verde si 100%, amarillo si hubo 1 caso vencido, rojo si hay mas de 1 en el periodo o alguna sigue abierta y vencida | Legal, Auditor, Gerencia |
| Consentimientos sensibles/biometricos incompletos | Conteo de registros en Presentado con tipo Sensible/Biometrico/Parental sin firma por mas de 2 dias | Rojo si mayor a 0 | Responsable, Legal |
| Evidencia disponible | Consent y ConsentWithdrawal con snapshot y archivo adjunto completos / total de registros aplicables | Verde/amarillo/rojo segun umbral configurado por producto | Auditor, Legal |

Todos los indicadores se muestran como "estado del programa" (cobertura, tareas pendientes, evidencia disponible), nunca como un porcentaje de "cumplimiento legal", conforme a `04_objetivo_exacto_del_producto.md`, seccion 1.2.

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Consentimientos vigentes | Lista de Consent vigentes con finalidad, tipo, fecha y version del aviso | Por tratamiento, finalidad, tipo, rango de fechas | XLSX, CSV | Responsable, Legal, Gerencia | Si |
| Revocaciones procesadas | Lista de ConsentWithdrawal con fechas de recepcion, ejecucion y notificacion, y si cumplieron el plazo | Por rango de fechas, por estado (a tiempo/vencida) | XLSX, CSV | Legal, Auditor (auditoria anual OBL-AUD-01) | Si |
| Expediente individual de consentimiento | Snapshot del texto, version del aviso, archivo de firma, historial de estados, hash de integridad | Por Consent especifico | PDF firmado/hash | Delegado/Responsable interno, respuesta a un reclamo o a la ACE | Si |
| Consentimientos sensibles y biometricos | Lista filtrada de registros tipo Sensible/Biometrico/Parental, con estado de la alternativa no biometrica ofrecida | Por tipo, por area | XLSX | Legal, Riesgos/EIPD (MOD-014) | Si |

## O. Historial

Eventos que quedan en el historial del modulo y en la auditoria transversal:

- Creacion de un Consent o de un ConsentWithdrawal (usuario, fecha, hora).
- Cambios de estado en cualquiera de las dos maquinas de estados (valor anterior y nuevo, usuario, fecha, motivo cuando aplique).
- Captura o reemplazo del texto de consentimiento (con la version anterior conservada, nunca sobrescrita).
- Adjuntos: alta de una firma o documento (usuario, fecha, hash del archivo).
- Aprobaciones (Delegado/Responsable interno aprobando una ejecucion o una notificacion): identidad, fecha, rol vigente en ese momento.
- Asignaciones de tareas relacionadas (a quien, cuando, por quien).
- Accesos de lectura a datos sensibles del registro (por ejemplo, quien abrio el archivo de firma o el documento de relacion parental de un caso NNA), con fecha y hora.
- Exportaciones de reportes o de un expediente individual (quien, cuando, para que caso).
- Archivado por sustitucion (un Consent que pasa a Sustituido: fecha, y referencia al nuevo registro que lo reemplaza).
- Vencimientos de plazo detectados por el motor de plazos (queda marcado permanentemente, aunque el expediente se resuelva despues).

## P. Riesgos

| Riesgo | Tipo | Mitigacion de diseno |
|---|---|---|
| Dar por valida automaticamente la calidad de un consentimiento (que sea realmente libre, especifico, informado) | Legal | El sistema nunca certifica la validez juridica del texto; solo verifica que los campos obligatorios existan (seccion H, punto 4) |
| Computar mal el plazo de revocacion (5 o 5+5 dias habiles) por no usar el calendario correcto | Operativo | El calculo nunca se reimplementa en este modulo; siempre se pide a MOD-023, el unico que conoce los dias inhabiles configurados |
| Formulario de consentimiento sensible o biometrico demasiado largo, con abandono del titular | UX | Mostrar solo los campos que aplican segun el tipo detectado automaticamente desde el RAT (regla 2 de la seccion G), sin exponer todos los campos posibles de una vez |
| La version del Aviso referenciada queda desactualizada si Documentos publica una version nueva despues de la captura | Operativo | El campo "version del Aviso" es un snapshot inmutable tomado en el momento de la captura, nunca un enlace que se actualiza solo (decision 2.7 punto 6) |
| Exposicion de la firma o del documento de identidad del titular a personas sin necesidad de verlo | Seguridad, privacidad | Acceso a archivos adjuntos sensibles restringido por rol, con registro obligatorio de todo acceso de lectura en el historial (seccion O) |
| Revocacion cerrada sin notificar a un encargado real porque no estaba registrado en Proveedores | Legal, operativo | El sistema bloquea el cierre de una revocacion si el tratamiento tiene encargados sin evaluar en MOD-009, exigiendo registrarlos primero |
| Uso del rol equivocado (Delegado en vez de Responsable interno, o viceversa) tras un cambio del estado de la reforma 659 | Regulatorio | El campo "persona que aprueba" (D.2) se calcula consultando la bandera de MOD-024 en cada revocacion nueva, nunca se guarda en cache |
| Datos de menores de edad capturados sin evidencia suficiente de la relacion parental | Legal, seguridad de la infraccion muy grave (Art. 56 lit. c num. 3) | El sub-flujo parental es obligatorio en cuanto se marca Titular NNA = Si; no se puede omitir aunque no se adjunte documento de respaldo (queda constancia de que no se adjunto) |

## Q. MVP

| Funcionalidad del modulo | MUST | SHOULD | COULD | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Registro de consentimiento general (formulario simple, sin refuerzo) | X | | | | Cubre OBL-CONS-01 y OBL-PRIN-01, base de todo el modulo; complejidad baja, valor alto |
| Registro de consentimiento reforzado (sensible/biometrico con firma) | X | | | | Cubre OBL-CONS-04 y OBL-SENS-02/07, riesgo de infraccion muy grave si falta (Art. 56 lit. c num. 1) |
| Revocacion con flujo de dos plazos (5 + 5 dias habiles) | X | | | | Cubre OBL-CONS-02, 03 y 04, tambien infraccion muy grave (Art. 56 lit. c num. 9 y 10) |
| Sub-flujo de consentimiento parental para NNA | X | | | | Cubre OBL-CONS-06 y OBL-PRIN-04, infraccion muy grave especifica (Art. 56 lit. c num. 3); faltante 25 identificado en `02_validacion_de_la_idea.md` |
| Catalogo de excepciones al consentimiento (Art. 28 y Arts. 37-38) | | X | | | Clasificacion CONDICIONAL en la matriz (OBL-TRAT-02, OBL-SENS-03); util pero no bloquea el flujo principal si se lanza primero solo con consentimiento explicito |
| Enlace automatico con la lista de supresion de marketing (oposicion ARCO-POL) | | X | | | Mejora operativa de un faltante identificado (numero 29), depende de que MOD-011 este disponible; no es en si una obligacion OBLIGATORIO independiente |
| Snapshot inmutable y version del aviso referenciada | X | | | | Es la base de la carga de la prueba (OBL-CONS-05, Art. 54); sin esto ningun otro campo sirve como evidencia |
| Reportes exportables de consentimientos y revocaciones | X (basico) | X (avanzado con filtros) | | | Version basica MUST HAVE para la auditoria anual (OBL-AUD-01); filtros avanzados y analitica quedan como mejora posterior |
| Sincronizacion con sistemas externos (webhook a CRM o plataforma de marketing) | | | X | | Mencionado como "posible dato" en el documento maestro, seccion 19, pero no exigido por ley; riesgo de acercarse al anti-feature 1 (no ser CRM) si se hace mal, por eso se pospone y se disena con cuidado |
| Portal publico de autogestion del consentimiento para el titular | | | | X | Depende de MOD-012 Portal del Titular, que es V1/Enterprise (decision 2.7.30); en el MVP el titular usa el formulario interno seguro existente |
| Analitica de tendencias de consentimiento (tasas de aceptacion por canal, por finalidad) | | | X | | Valor de negocio pero no de cumplimiento; util cuando ya hay volumen suficiente de datos |

**Version minima vendible del modulo:** registro de consentimiento general y reforzado (con firma para datos sensibles y biometricos), revocacion con el flujo completo de dos plazos encadenados, sub-flujo parental para NNA, y el snapshot inmutable del texto y la version del aviso. Esta combinacion cubre las cuatro obligaciones OBLIGATORIO de mayor riesgo de la matriz (OBL-CONS-01 a 04) mas la obligacion CONDICIONAL de mayor severidad (OBL-CONS-06, infraccion muy grave si aplica y no se cumple), sin necesidad de sincronizacion externa ni de portal publico.

## R. Ayuda contextual (complemento obligatorio)

**1. Que es el consentimiento**
- Que es: es el permiso claro y especifico que una persona da para que su informacion se use con un fin concreto que usted le explico antes.
- Por que tengo que hacer esto: porque si su empresa eligio el consentimiento como la razon legal para usar ese dato, la ley le exige poder demostrar despues que la persona realmente lo dio, no solo que "probablemente" lo dio.
- Fundamento: OBL-CONS-01, Arts. 26 y 27 de la Ley para la Proteccion de Datos Personales.
- Cuando necesito ayuda juridica: si no esta seguro de que el consentimiento sea la base correcta para un tratamiento (existen otras cinco bases posibles), consulte a su asesoria legal antes de apoyarse solo en el consentimiento.

**2. Revocacion del consentimiento**
- Que es: el derecho de la persona a retirar, en cualquier momento, el permiso que dio antes, sin que eso afecte lo que ya se hizo con sus datos hasta ese momento.
- Por que tengo que hacer esto: la ley obliga a que retirar el consentimiento sea tan facil como darlo, y le da a su empresa solo 5 dias habiles para dejar de usar el dato, y otros 5 dias habiles para avisarle a cualquier proveedor que tambien lo estuviera usando por encargo suyo.
- Fundamento: OBL-CONS-02, OBL-CONS-03, OBL-CONS-04, Arts. 29 y 30.
- Cuando necesito ayuda juridica: si la revocacion afecta un contrato ya en ejecucion o genera dudas sobre que datos concretos deben dejar de tratarse, consulte a su asesoria legal.

**3. Datos sensibles y consentimiento reforzado**
- Que es: cuando el dato es especialmente delicado (salud, biometria, afiliacion sindical, entre otros), la ley exige un consentimiento mas estricto, con firma, no solo un clic de aceptacion.
- Por que tengo que hacer esto: porque tratar datos sensibles sin este consentimiento reforzado es una de las infracciones mas graves de la ley.
- Fundamento: OBL-CONS-04, OBL-SENS-02, Art. 26 inc. 4 y Art. 37.
- Cuando necesito ayuda juridica: si no esta seguro de si un dato concreto (por ejemplo, "datos laborales" en general) es sensible o no, consulte a su asesoria legal; no todos los datos de un expediente de recursos humanos son sensibles por igual.

**4. Alternativa no biometrica**
- Que es: ofrecer a la persona una forma distinta a la huella o el rostro para identificarse (por ejemplo una tarjeta o un PIN), ademas del metodo biometrico.
- Por que tengo que hacer esto: aunque la ley no lo exige de forma literal, es una recomendacion de diseno fuerte, especialmente en el trabajo, donde la relacion de subordinacion puede poner en duda que el consentimiento fue realmente libre.
- Fundamento: OBL-SENS-07, Art. 26 inc. 4 y Art. 37 (recomendacion de diseno, no mandato legal expreso).
- Cuando necesito ayuda juridica: si su empresa quiere usar solo biometria, sin alternativa, para un proceso laboral, consulte a su asesoria legal antes de implementarlo.

**5. Consentimiento de menores de edad (NNA)**
- Que es: cuando la persona titular de los datos es nina, nino o adolescente, el consentimiento normalmente lo debe dar su padre, madre o tutor, en lugar del menor por si solo.
- Por que tengo que hacer esto: usar datos de menores sin ese consentimiento es una infraccion muy grave.
- Fundamento: OBL-CONS-06, OBL-PRIN-04, Art. 56 lit. c num. 3, Art. 5 lit. j, Art. 42.
- Cuando necesito ayuda juridica: existe una tension no resuelta entre esta ley y la Ley Crecer Juntos sobre si un adolescente puede autoconsentir ciertas publicaciones; consulte siempre a su asesoria legal en casos de adolescentes de 12 a 18 anos.

**6. Cuando no se necesita consentimiento**
- Que es: hay situaciones en las que la ley permite usar un dato sin pedir consentimiento, porque existe otra razon legal valida (por ejemplo, un contrato, una obligacion legal, o el dato viene de una fuente publica).
- Por que tengo que hacer esto: si su empresa se apoya en una de estas excepciones, debe dejar constancia de cual es y por que aplica, en vez de simplemente no pedir permiso sin explicacion.
- Fundamento: OBL-TRAT-02 (Art. 28, ocho supuestos), OBL-SENS-03 (Arts. 37-38, tres excepciones para datos sensibles).
- Cuando necesito ayuda juridica: la decision de si una excepcion aplica realmente a su caso siempre requiere el criterio de su organizacion o de asesoria legal; el sistema solo le muestra las opciones, no decide por usted.

---

## Nota final del arquitecto funcional (desacuerdos y observaciones sobre el mapa)

No se detecto ningun error o inconsistencia material entre `mapa_modulos.json`, `06_mapa_definitivo_de_modulos.md` y la matriz de obligaciones respecto de este modulo; las 12 obligaciones propias y las 6 colaboradoras asignadas a MOD-007 coinciden exactamente con lo verificado en `matriz_obligaciones.json`. Se dejan registradas tres observaciones, ninguna de ellas una discrepancia:

1. **Dependencias formales vs. consultas transversales.** El campo `depende_de` de `mapa_modulos.json` solo lista MOD-006 y MOD-008 como entradas de datos de negocio. Esta ficha ademas modela a MOD-002 (Delegado/Responsable interno), MOD-023 (Calendario) y MOD-024 (Centro Regulatorio) como consultas de servicio transversal (aprobacion, calculo de plazos, bandera de estado), no como flechas de dependencia de datos. Esto es coherente con la regla explicita de la seccion 4 de `06_mapa_definitivo_de_modulos.md` (los modulos transversales se consultan desde cualquier pantalla, no se enumeran como dependencias de recorrido), por lo que no se trata de un error del mapa sino de una precision necesaria para que el flujo de aprobacion de revocaciones (Art. 30) quede completo en esta ficha.
2. **Alcance del principio de minimizacion.** Se aplico de forma literal la decision 2.7, punto 21, de `02_validacion_de_la_idea.md`, que excluye explicitamente a Consentimiento (junto con ARCO-POL, Portal e Incidentes) del principio de minimizacion estricta que si aplica a RAT, Inventario y Proveedores. Esto es consistente con la instruccion de la tarea de minimizar "salvo donde el proceso lo exige"; se documenta aqui para que quede explicito que la identificacion minima del titular en el registro de consentimiento (seccion D.1) es una excepcion deliberada y ya decidida, no un vacio de diseno.
3. **Incertidumbres heredadas, no resueltas por este modulo.** Dos incertidumbres juridicas documentadas en `03_hallazgos_regulatorios.md` (seccion 9, puntos 8 y 10: edad de consentimiento de NNA frente a la Ley Crecer Juntos, y si un encargado extranjero debe tratarse como transferencia) atraviesan este modulo. Se modelaron con el criterio conservador por defecto (flujo parental completo siempre disponible; remision a Transferencias cuando el encargado esta fuera del pais) y con la advertencia visible correspondiente en la seccion H, sin intentar resolverlas, tal como exige la regla de redaccion del proyecto.
