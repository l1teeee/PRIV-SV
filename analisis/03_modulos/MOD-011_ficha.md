# MODULO: ARCO-POL

Codigo corto del modulo: MOD-011
Clasificacion global del modulo: MUST HAVE (para el MVP)
Obligaciones que cubre:
- Propietarias: OBL-ARCO-01, OBL-ARCO-02, OBL-ARCO-03, OBL-ARCO-04, OBL-ARCO-05, OBL-ARCO-06, OBL-ARCO-07, OBL-ARCO-08, OBL-ARCO-09, OBL-ARCO-10, OBL-ARCO-11, OBL-ARCO-12, OBL-ARCO-13, OBL-ARCO-14, OBL-ARCO-15 (15 obligaciones, la mayor concentracion de toda la matriz).
- Colaboradoras (el modulo participa pero no es el propietario): OBL-CONS-06, OBL-DOC-01, OBL-DOC-04, OBL-PLAZO-04, OBL-PRIN-04, OBL-RET-05, OBL-SANC-09.

---

## A. Proposito

**Por que existe.** La Ley para la Proteccion de Datos Personales (Decreto Legislativo 144, en adelante LPDP) reconoce siete derechos del titular agrupados bajo la sigla ARCO-POL (Acceso, Rectificacion, Cancelacion, Oposicion, Portabilidad, Olvido, Limitacion; Art. 4 lit. i y Arts. 6 a 14) y obliga expresamente a la empresa a "establecer y documentar procedimientos" para atenderlos (Art. 33 inc. 1, OBL-DOC-01). Sin un modulo dedicado, cada solicitud de un titular se atenderia de forma manual (correo, papel, hoja de calculo), sin verificacion de identidad consistente, sin control de los seis plazos legales distintos que aplican segun la etapa del tramite, y sin la evidencia que la empresa necesitaria para defenderse ante un reclamo del titular o un requerimiento de la Agencia de Ciberseguridad del Estado (ACE).

**Que problema resuelve para la empresa.** Convierte una obligacion legal compleja, con siete derechos distintos y hasta seis plazos que corren en paralelo o en cadena, en un unico flujo operativo: intake, verificacion de identidad, clasificacion del derecho, calculo automatico de plazos, generacion de borradores de respuesta, aprobacion humana antes de notificar, cierre y conservacion del expediente como evidencia.

**Que obligacion u obligaciones cubre (IDs y articulos).**

| OBL-ID | Articulo / fuente | Contenido resumido |
|---|---|---|
| OBL-ARCO-01 | Art. 6 LPDP | Legitimacion para presentar la solicitud: el propio titular, su representante con facultades especiales, o -si el titular fallecio- sus herederos o sucesores acreditando esa calidad |
| OBL-ARCO-02 | Art. 8 LPDP | Contenido obligatorio de la respuesta al derecho de acceso: quienes consultaron los datos, con que proposito, si hubo intercambio con otras instituciones; nunca puede revelar datos de un tercero distinto del titular |
| OBL-ARCO-03 | Art. 9 LPDP | Rectificacion: 20 dias habiles, gratuita, con bloqueo cautelar del dato mientras se verifica |
| OBL-ARCO-04 | Art. 10 LPDP | Cancelacion: procede solo en 7 causales tasadas y no procede en 6 supuestos tasados |
| OBL-ARCO-05 | Art. 12 LPDP | Oposicion, incluida la oposicion a perfilado con fines de mercadotecnia directa; no procede si hay interes publico o interes legitimo prevalente |
| OBL-ARCO-06 | Art. 13 LPDP | Limitacion del tratamiento: procede solo en 4 supuestos tasados |
| OBL-ARCO-07 | Art. 14 LPDP | Portabilidad: exige que la base sea consentimiento y que el tratamiento sea automatizado |
| OBL-ARCO-08 | Art. 18 LPDP | Los 7 requisitos de toda solicitud, y la prevencion unica con 10 dias habiles para subsanar (archivo automatico si no se subsana) |
| OBL-ARCO-09 | Art. 19 LPDP | Devolucion por incompetencia dentro de 5 dias habiles |
| OBL-ARCO-10 | Art. 20 LPDP | Plazo general de respuesta: 20 dias habiles, prorrogables por causa justificada hasta 20 dias habiles adicionales (una sola prorroga) |
| OBL-ARCO-11 | Art. 21 inc. 3 LPDP | Notificacion a los receptores de los datos, dentro de 5 dias habiles desde que se determina la procedencia |
| OBL-ARCO-12 | Art. 22 LPDP | Denegatoria total o parcial: solo en 8 supuestos tasados, motivada, con pruebas, notificada en 3 dias habiles |
| OBL-ARCO-13 | Art. 23 LPDP | Gratuidad; solo pueden cobrarse costos de reproduccion, certificacion o envio previamente publicados |
| OBL-ARCO-14 | Lineamientos DPO (ACE), Art. 33 inc. 4 | Reclamo del titular ante la Direccion de Proteccion de Datos Personales de la ACE, dentro de 10 dias habiles desde la notificacion de la resolucion |
| OBL-ARCO-15 | Lineamientos DPO (ACE), Art. 32 | Obligacion de aceptar los formularios oficiales ARCO-POL de la ACE, aunque la empresa tenga formulario propio |

Colaboradoras que este modulo consulta o alimenta sin ser su propietario: OBL-CONS-06 y OBL-PRIN-04 (consentimiento y ejercicio progresivo de facultades de ninas, ninos y adolescentes, propiedad de MOD-007), OBL-DOC-01 (procedimiento documentado, propiedad de MOD-008), OBL-DOC-04 y OBL-PLAZO-04 (mecanismos de ejercicio de derechos, propiedad de MOD-012 Portal del Titular, pero satisfechas en el MVP por el formulario interno seguro de este modulo), OBL-RET-05 (retencion del expediente, propiedad de MOD-016) y OBL-SANC-09 (denuncia del titular ante la ACE por incumplimiento de plazos, propiedad de MOD-024).

**Que valor aporta.**
- Operativo: un solo lugar donde se reciben, clasifican, asignan y resuelven las siete solicitudes, con plazos calculados automaticamente por el motor compartido (MOD-023).
- Probatorio: cada expediente queda como evidencia verificable (quien hizo que, cuando, con que fundamento) para un reclamo del titular ante la ACE (OBL-ARCO-14) o para la auditoria anual de cumplimiento.
- De reduccion de riesgo: evita las dos infracciones mas costosas del catalogo relacionadas con este modulo: no atender solicitudes en tiempo y forma (infraccion grave, 11 a 25 salarios minimos) y denegar solicitudes en contravencion de la ley (infraccion muy grave, 26 a 40 salarios minimos, Art. 56).

**Que NO hace este modulo (limites explicitos).**
- No resuelve automaticamente (acepta o deniega) una solicitud sin intervencion humana; calcula el plazo, presenta las causales tasadas y prepara el borrador de respuesta, pero la persona con el rol Delegado (o Responsable interno, ver seccion de doble estado mas abajo) decide y aprueba antes de que cualquier acto salga hacia el titular (anti-feature 7 de `22_anti_features.md`; decision 2.7.22 de `02_validacion_de_la_idea.md`).
- No actua como el Delegado de Proteccion de Datos del cliente ni ejerce sus funciones legales; es la herramienta que usa la persona designada, no un sustituto de su investidura legal (anti-feature 4).
- No es el portal publico con autoregistro del titular. En el MVP, el canal es un formulario interno seguro operado por personal de la empresa (con opcion de que el titular lo complete el mismo si la empresa habilita un enlace), sin cuenta de titular ni autoregistro; el portal publico dedicado con consulta de estado autenticada por el propio titular es el modulo MOD-012 (SHOULD HAVE, capa adicional posterior, decision 2.7.30).
- No presenta tramites ante la ACE en nombre de la empresa sin que esta lo autorice y ejecute: en el reclamo del Art. 33 inc. 4 de los Lineamientos DPO, el sistema prepara el informe de actuaciones, pero la empresa es quien lo remite por el canal oficial (anti-feature 13).
- No decide por si mismo si una causal de cancelacion, de oposicion o de denegatoria aplica a un caso concreto cuando la ley exige ponderacion (por ejemplo, "interes legitimo prevalente" del Art. 12); presenta el checklist tasado y deja la ponderacion a una persona.
- No almacena copias de la base de datos completa del cliente para tramitar una solicitud (anti-feature 8); solo conserva los datos del titular solicitante y las referencias necesarias para localizar y ejecutar la accion (por ejemplo, referencia al Tratamiento del RAT, no una copia del sistema de origen). A diferencia de RAT, Inventario y Proveedores (donde si aplica minimizacion estricta), en ARCO-POL los datos del titular SI se procesan de forma directa porque son el objeto legitimo del proceso (decision 2.7.21); la minimizacion aqui significa no pedir ni conservar mas de lo que el expediente requiere, no evitar el dato del titular por completo.

---

## B. Usuarios

| Rol estandar | Para que usa este modulo |
|---|---|
| Administrador de la organizacion | Configura el canal de recepcion (formulario interno, correo habilitado, disponibilidad presencial), la tabla de costos de reproduccion/envio publicada, y ve reportes agregados de volumen y cumplimiento de plazos; no interviene en la resolucion de casos individuales salvo que tambien ocupe otro rol (comun en pyme) |
| Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO de la reforma 659) | Aprueba, antes de que se emitan, todos los actos que la ley atribuye a esta figura: la prevencion, la declaracion de incompetencia, la resolucion (reconocimiento o denegatoria) y la notificacion a receptores; firma la resolucion final; atiende el reclamo del titular ante la Direccion de Proteccion de Datos de la ACE (OBL-ARCO-14) |
| Responsable ARCO-POL / Responsable del tramite | Ejecuta el dia a dia: recibe la solicitud, verifica la identidad y la representacion, clasifica el derecho ejercido, redacta los borradores de prevencion, resolucion y notificaciones, coordina con las areas que deben ejecutar la accion (por ejemplo, RRHH para eliminar un CV) |
| Responsable Legal / Compliance | Revisa denegatorias complejas, pondera el interes legitimo en una oposicion, revisa el borrador del informe de actuaciones ante un reclamo de la ACE, y decide si un caso amerita opinion de asesor externo |
| Responsable de Seguridad / IT | Apoya en la ejecucion tecnica del derecho de acceso y de portabilidad (localizar y extraer los datos del sistema donde realmente residen, con apoyo del RAT/Mapa de datos de MOD-006) |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Ejecuta las tareas derivadas de una solicitud que afecta a su area, por ejemplo dar de baja a un titular de una lista de marketing tras una oposicion, o eliminar un curriculum tras una cancelacion |
| Aprobador | En organizaciones a partir de empresa mediana, actua como segundo revisor de una denegatoria que involucra datos sensibles o riesgo de reclamo ante la ACE, antes de que se notifique al titular (regla de separacion de funciones de `05_tipos_de_usuario.md`, seccion 5.4) |
| Auditor (interno) | Solo lectura del expediente y de su historial, para verificar el cumplimiento de los seis plazos legales durante la auditoria anual de cumplimiento (OBL-AUD-01) |
| Auditor externo (invitado) | Acceso temporal de solo lectura al paquete de expedientes exportado, durante la semana de auditoria de una firma externa |
| Usuario de consulta / Colaborador | Completa unicamente la tarea puntual que se le asigna, por ejemplo "confirmar si el sistema X tiene datos del titular Y" |
| Titular (formulario externo) | Presenta su propia solicitud y da seguimiento a su estado; en el MVP lo hace mediante el formulario interno seguro de este modulo (sin necesidad de crear una cuenta), directamente o asistido por la empresa (canal presencial, telefonico, WhatsApp o correo, ver seccion F.1 casos especiales) |
| Asesor externo invitado | Revisa un caso puntual complejo (por ejemplo, una denegatoria dudosa o una solicitud de un titular menor de edad con tension normativa) con acceso acotado a ese expediente, y deja su opinion registrada como evidencia, sin licencia permanente |

---

## C. Permisos

| Accion | Administrador | Delegado / Resp. interno | Resp. ARCO-POL | Legal | IT/Seguridad | Resp. de area | Aprobador | Auditor interno | Auditor externo | Colaborador | Titular | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver expediente propio (solo el suyo) | - | - | - | - | - | - | - | - | - | - | Si | - |
| Ver todos los expedientes de la organizacion | Si | Si | Si | Si | Solo lectura | No | Solo lectura | Solo lectura | Solo lectura (invitacion) | No | No | Solo el asignado |
| Recibir/registrar una solicitud nueva | Si | Si | Si | No | No | No | No | No | No | No | Si (la presenta) | No |
| Verificar identidad y representacion | No | Si | Si | No | No | No | No | No | No | No | No | No |
| Enviar prevencion (borrador) | No | No | Si | No | No | No | No | No | No | No | No | No |
| Aprobar y emitir la prevencion | No | Si | No | No | No | No | No | No | No | No | No | No |
| Declarar incompetencia (borrador) | No | No | Si | No | No | No | No | No | No | No | No | No |
| Aprobar y emitir la incompetencia | No | Si | No | No | No | No | No | No | No | No | No | No |
| Redactar borrador de resolucion (reconocimiento o denegatoria) | No | No | Si | Si (revision) | No | No | No | No | No | No | No | No |
| Aprobar y emitir la resolucion final | No | Si | No | No | No | No | Si (segundo revisor si aplica) | No | No | No | No | No |
| Notificar a receptores | No | Si (aprueba el envio) | Si (ejecuta) | No | No | No | No | No | No | No | No | No |
| Cerrar expediente | No | Si | Si (propone) | No | No | No | No | No | No | No | No | No |
| Reabrir por reclamo ante la ACE | No | Si | No | Si | No | No | No | No | No | No | No | No |
| Asignar responsable / reasignar | Si | Si | No | No | No | No | No | No | No | No | No | No |
| Comentar internamente en el expediente | Si | Si | Si | Si | Si | Si | Si | No | No | Si (si tiene tarea asignada) | No | Si (en su caso) |
| Adjuntar evidencia | Si | Si | Si | Si | Si | Si (en su tarea) | No | No | No | Si (en su tarea) | Si (en su solicitud) | No |
| Archivar por falta de subsanacion | Sistema (automatico) | - | - | - | - | - | - | - | - | - | - | - |
| Exportar expediente / paquete de evidencia | Si | Si | Si | Si | No | No | No | Si | Si (lo asignado) | No | No | No |
| Eliminar un expediente o su historial | Nadie. No existe esta accion para ningun rol; solo existe archivado por vencimiento de retencion, ejecutado por el sistema con aprobacion del Administrador (ver seccion J) | | | | | | | | | | | |

**Separacion de funciones.** Quien redacta un borrador de prevencion, incompetencia, denegatoria o notificacion (Responsable ARCO-POL) nunca es quien lo aprueba y emite (Delegado o Responsable interno): esto aplica a todo acto legalmente atribuido a esa figura, sin excepcion, incluso en pyme donde ambos roles puedan recaer en la misma persona fisica ocupando dos roles del sistema (en ese caso, el sistema exige una segunda confirmacion explicita separada del guardado del borrador, con advertencia de autorrevision, siguiendo la regla general de `05_tipos_de_usuario.md` seccion 5.4). Cuando la solicitud involucra datos sensibles o existe riesgo de reclamo ante la ACE (por ejemplo, una denegatoria total), el sistema permite escalar la decision a un segundo revisor (Aprobador) antes de notificar al titular. El rol Auditor (interno o externo) es siempre de solo lectura y nunca puede coincidir con quien carga evidencia o aprueba una accion en el mismo expediente que audita.

---

## D. Informacion de entrada

Los campos del formulario de intake replican, como estandar minimo, los elementos de los 7 formularios oficiales ARCO-POL de la ACE (version 07-07-2025: acceso, rectificacion, cancelacion, oposicion, portabilidad, limitacion, olvido), que la empresa debe aceptar sin poder rechazarlos aunque tenga formulario propio (OBL-ARCO-15, Art. 32 Lineamientos DPO). El sistema permite ademas cargar directamente un formulario oficial ya diligenciado por el titular, mapeando sus campos a esta misma estructura.

### D.1 Datos de la entidad responsable (precargados)

| Campo | Tipo | Obligatorio/opcional | Opciones/catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Nombre o razon social | Texto | Obligatorio, precargado | - | No vacio | "Es el nombre legal de su empresa, ya registrado en Organizacion." | OBL-ARCO-08, Art. 18 (formulario debe identificar al responsable) |
| Domicilio | Texto | Obligatorio, precargado | - | No vacio | Se toma del modulo Organizacion (MOD-001) | OBL-ARCO-08 |
| Correo electronico de contacto | Texto | Obligatorio, precargado | - | Formato de correo | Correo publicado para consultas | OBL-ARCO-08 |
| Telefono de contacto | Texto | Opcional, precargado | - | - | - | Buena practica |

Estos cuatro campos se precargan siempre desde el modulo Organizacion (MOD-001) y no se capturan de nuevo por cada solicitud.

### D.2 Identificacion del solicitante y del tipo de legitimacion

| Campo | Tipo | Obligatorio/opcional | Opciones/catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Tipo de solicitante | Seleccion unica | Obligatorio desde el inicio | Titular; Representante legal o apoderado; Heredero o sucesor (titular fallecido) | Determina que documentos adicionales se piden mas abajo | "Indique si usted es la persona duena de los datos, alguien que la representa legalmente, o un familiar de una persona fallecida." | OBL-ARCO-01, Art. 6 |
| Nombre completo del solicitante | Texto | Obligatorio | - | No vacio | "Nombre completo de quien presenta la solicitud (puede ser distinto del titular si es representante o heredero)." | OBL-ARCO-08, Art. 18 lit. a |
| Documento de identidad del solicitante (DUI o equivalente) | Archivo (imagen o PDF) | Obligatorio antes de admitir | - | Formato imagen/PDF, tamano maximo configurable | "Suba una foto o escaneo legible de su Documento Unico de Identidad (DUI)." | OBL-ARCO-08, Art. 18 lit. b |
| Domicilio del solicitante | Texto | Obligatorio | - | No vacio | - | OBL-ARCO-08, Art. 18 lit. a |
| Correo electronico del solicitante | Texto | Obligatorio si elige notificacion por correo | - | Formato de correo | - | OBL-ARCO-08 |
| Telefono del solicitante | Texto | Opcional | - | - | - | Buena practica |
| Los datos corresponden a un titular de ninez o adolescencia | Booleano | Obligatorio (checkbox) | Si/No | Si es "Si", activa el sub-flujo de menores (ver D.5) | "Marque esta opcion si la solicitud es sobre los datos de una nina, nino o adolescente." | OBL-CONS-06, OBL-PRIN-04, Art. 5 lit. j, Art. 42, Art. 56 lit. c num. 3 |
| Los datos corresponden a una persona fallecida | Booleano | Obligatorio (checkbox) | Si/No | Si es "Si", activa los campos de D.4 | "Marque esta opcion si la solicitud es sobre los datos de alguien que ya fallecio." | OBL-ARCO-01, Art. 6 |

### D.3 Si el tipo de solicitante es Representante legal o apoderado

| Campo | Tipo | Obligatorio/opcional | Opciones/catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Nombre completo del titular representado | Texto | Obligatorio | - | No vacio | - | OBL-ARCO-01, Art. 6 |
| Documento de poder de representacion | Archivo | Obligatorio, no se puede admitir la solicitud sin este archivo | - | Formato imagen/PDF | "Adjunte el poder notarial u otro documento que acredite que usted puede actuar en nombre del titular, con facultades especiales para este tramite." | OBL-ARCO-01, Art. 6 (facultades especiales) |

### D.4 Si el tipo de solicitante es Heredero o sucesor (titular fallecido)

| Campo | Tipo | Obligatorio/opcional | Opciones/catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Certificacion de partida de defuncion del titular | Archivo | Obligatorio, no se puede admitir sin este archivo | - | Formato imagen/PDF | "Adjunte la partida de defuncion del titular." | OBL-ARCO-01, Art. 6 |
| Documento que acredite el vinculo familiar o la calidad de heredero/sucesor | Archivo | Obligatorio, no se puede admitir sin este archivo | - | Formato imagen/PDF | "Adjunte el documento que demuestre su parentesco o su calidad de heredero (por ejemplo, partida de nacimiento, declaratoria de herederos)." | OBL-ARCO-01, Art. 6 |

### D.5 Si el titular es nina, nino o adolescente

| Campo | Tipo | Obligatorio/opcional | Opciones/catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Certificacion de partida de nacimiento del titular | Archivo | Obligatorio si se marco NNA | - | Formato imagen/PDF | "Adjunte la partida de nacimiento del nino, nina o adolescente." | OBL-CONS-06, Art. 5 lit. j, Art. 42 |
| Carne de minoridad (si existe) | Archivo | Opcional | - | Formato imagen/PDF | - | Buena practica, documento de la ACE |
| Nombre del progenitor, representante o tutor que consiente/solicita | Texto | Obligatorio si se marco NNA | - | No vacio | "Nombre de la madre, padre, representante o tutor que autoriza o presenta esta solicitud en nombre del nino, nina o adolescente." | OBL-CONS-06, Art. 56 lit. c num. 3 |
| Aviso visible: tension normativa NNA | Solo lectura (banner) | Automatico, no editable | - | - | "Existe una tension entre la LPDP (consentimiento parental) y la Ley Crecer Juntos (adolescentes de 12 a 18 anos pueden autorizar ciertas publicaciones de su imagen). Requiere validacion de la organizacion o asesoria especializada." | Incertidumbre 8 de `03_hallazgos_regulatorios.md`; OBL-PRIN-04 |

### D.6 Datos sobre la solicitud (comunes a todos los derechos)

| Campo | Tipo | Obligatorio/opcional | Opciones/catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Derecho que se ejerce | Seleccion unica | Obligatorio | Acceso; Rectificacion; Cancelacion o supresion; Oposicion; Portabilidad; Limitacion; Olvido | Determina que campos adicionales de D.7 se muestran | "Elija el derecho que quiere ejercer. Si tiene dudas, revise la ayuda contextual de cada uno (seccion R)." | OBL-ARCO-08, Art. 18 lit. e |
| Area que trata los datos (si se conoce) | Seleccion unica o texto libre | Opcional | Catalogo de areas de MOD-001, o "no lo se" | - | "Si sabe que area de la empresa maneja sus datos (por ejemplo Recursos Humanos o Marketing), indiquelo; si no lo sabe, deje esta casilla en blanco." | OBL-ARCO-08, Art. 18 lit. c |
| Descripcion de los datos y elementos para localizarlos | Texto largo | Obligatorio | - | No vacio, minimo de caracteres configurable | "Describa que datos personales quiere consultar/corregir/eliminar, y cualquier informacion que ayude a encontrarlos (por ejemplo, fecha aproximada de cuando los entrego, o el numero de cliente)." | OBL-ARCO-08, Art. 18 lit. d y f |
| Canal de recepcion | Seleccion unica | Obligatorio, se marca automaticamente segun donde se registro | Formulario interno; Correo electronico; WhatsApp; Presencial; Formulario oficial ACE cargado | - | - | OBL-DOC-04, OBL-PLAZO-04 (mecanismos de ejercicio de derechos) |
| Formulario oficial de la ACE adjunto (si el titular lo uso) | Archivo | Opcional | - | Formato PDF/imagen | "Si usted ya lleno uno de los formularios oficiales de la ACE, adjuntelo aqui en vez de repetir los datos." | OBL-ARCO-15, Art. 32 Lineamientos DPO |
| Firma o medio equivalente | Archivo o marca electronica | Obligatorio, salvo canal que la ley reconozca sin firma fisica (ver F.1) | Firma escaneada; firma electronica simple del formulario; marca de aceptacion en el canal digital verificado | - | "Firme el documento o, si presenta la solicitud desde un canal digital verificado (por ejemplo, el correo previamente registrado por usted), acepte la casilla de confirmacion." | OBL-ARCO-08, Art. 18 lit. g |

### D.7 Campos especificos por derecho ejercido

| Campo | Aplica a | Tipo | Obligatorio/opcional | Opciones/catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|---|
| Modalidad de acceso solicitada | Acceso | Seleccion unica | Obligatorio | Consulta directa; Copia simple; Correo electronico; Copia certificada; Dispositivo de almacenamiento | - | "Elija como quiere recibir la informacion." | OBL-ARCO-02, Art. 8 |
| Dato a corregir y valor propuesto | Rectificacion | Texto largo | Obligatorio | - | No vacio | "Indique cual dato esta incorrecto y cual deberia ser el valor correcto." | OBL-ARCO-03, Art. 9 |
| Causal de cancelacion invocada | Cancelacion | Seleccion unica | Obligatorio | 1) Datos ya no necesarios; 2) Retiro de consentimiento; 3) Oposicion sin motivo legitimo prevalente; 4) Datos obtenidos o tratados ilicitamente; 5) Obligacion legal de suprimir; 6) Oferta directa dirigida a ninos; 7) Otro (especificar) | Si elige "Otro", exige texto libre | "Elija la razon principal de su solicitud." | OBL-ARCO-04, Art. 10 incisos 1 y 2 |
| Motivo de la oposicion | Oposicion | Texto largo | Obligatorio | - | No vacio | "Explique por que se opone a que sigamos usando sus datos." | OBL-ARCO-05, Art. 12 |
| Es oposicion a mercadotecnia directa / perfilado | Oposicion | Booleano | Obligatorio (checkbox) | Si/No | Si es "Si", conecta con la lista de supresion de MOD-007 | "Marque esta opcion si su solicitud es para dejar de recibir publicidad o dejar de ser incluido en perfiles de mercadeo." | OBL-ARCO-05, Art. 12 |
| Destinatario de los datos portados (si aplica) | Portabilidad | Texto | Opcional | - | - | "Si quiere que enviemos sus datos directamente a otra empresa, indique cual." | OBL-ARCO-07, Art. 14 |
| Formato solicitado | Portabilidad | Seleccion unica | Opcional (se sugiere un formato por defecto) | Formato estructurado de uso comun (segun catalogo tecnico del producto) | - | "El sistema le entregara sus datos en un formato que pueda abrirse facilmente y transferirse a otra empresa." | OBL-ARCO-07, Art. 14 |
| Supuesto de limitacion invocado | Limitacion | Seleccion unica | Obligatorio | 1) Impugna la exactitud del dato mientras se verifica; 2) Tratamiento ilicito, se opone a la supresion; 3) Necesita los datos para una reclamacion propia; 4) Oposicion pendiente de ponderacion | - | "Elija la situacion que corresponde a su caso." | OBL-ARCO-06, Art. 13 |
| Los datos objeto de olvido estan publicados en internet | Olvido | Booleano | Obligatorio (checkbox) | Si/No | Si es "Si", dispara la lista de terceros a notificar (ver E y G) | "Marque esta opcion si sus datos aparecen publicados en algun sitio web o red social." | OBL-ARCO-04, Art. 10 inciso final |

### D.8 Forma de entrega de la respuesta

| Campo | Tipo | Obligatorio/opcional | Opciones/catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Modalidad de entrega de la respuesta | Seleccion unica | Obligatorio | Copia simple; Correo electronico; Copia certificada; Dispositivo de almacenamiento | - | - | Estandar formularios ACE |
| Lugar o medio para recibir notificaciones | Seleccion unica | Obligatorio | Correo electronico registrado; Acudir con el Delegado/Responsable del tramite (presencial) | - | "Elija como quiere que le avisemos sobre su solicitud." | OBL-ARCO-12, Art. 22 (notificar por el medio senalado por el titular) |

### D.9 Documentacion adjunta (catalogo comun)

| Campo | Tipo | Obligatorio/opcional | Opciones/catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Pruebas o documentos adicionales que respalden la solicitud | Archivo (multiple) | Opcional | - | Formato imagen/PDF | "Adjunte cualquier documento que ayude a sustentar su solicitud." | Buena practica, formularios ACE |

### D.10 Campos internos (no visibles para el titular)

| Campo | Tipo | Obligatorio/opcional | Opciones/catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Numero de expediente | Texto (generado) | Automatico | Formato ARCO-[ANIO]-[correlativo] | Unico | - | Buena practica, trazabilidad |
| Fecha y hora de recepcion | Fecha/hora | Automatico | - | - | - | OBL-ARCO-10 (inicio del computo del plazo) |
| Responsable ARCO-POL asignado | Referencia a Usuario | Obligatorio antes de avanzar de "Recibida" | Usuarios con rol Responsable ARCO-POL | - | - | Buena practica |
| Marca de solicitud anonima | Booleano | Automatico/manual | Si/No | - | "Se marca cuando no fue posible verificar completamente la identidad del solicitante por el canal usado." | Ver F.1 casos especiales |
| Marca de solicitud potencialmente masiva o abusiva | Booleano | Automatico (por regla, ver G) | Si/No | - | "Se marca cuando el sistema detecta un volumen inusual de solicitudes del mismo remitente en poco tiempo." | Ver F.1 casos especiales |
| Referencia al Tratamiento del RAT (si se identifico) | Referencia | Opcional | Catalogo de Tratamientos de MOD-006 | - | - | Ayuda a localizar el dato sin duplicar el RAT |

**Campos precargados.** Los datos de la entidad responsable (D.1) se precargan desde MOD-001 Organizacion. El area sugerida (D.6) puede precargarse desde el RAT de MOD-006 si el titular o el Responsable ARCO-POL identifican el Tratamiento relacionado. La tabla de costos de reproduccion (si la empresa cobra algo) se precarga desde la Politica de Privacidad publicada en MOD-008.

**Datos personales que contiene este modulo y como se minimizan.** A diferencia de RAT, Inventario y Proveedores, este modulo SI procesa datos personales directos del titular (nombre, documento de identidad, domicilio, contacto, y el contenido mismo de su solicitud), porque son el objeto legitimo del proceso (decision 2.7.21 de `02_validacion_de_la_idea.md`). La minimizacion se aplica asi: (a) no se copian bases de datos completas del cliente para tramitar la solicitud, solo se referencia el Tratamiento del RAT donde corresponda; (b) los documentos de identidad (DUI, partidas, poderes) se guardan como adjuntos cifrados con acceso restringido a los roles Responsable ARCO-POL y Delegado/Responsable interno, nunca visibles para Colaboradores o Responsables de area; (c) el acceso de lectura a esos adjuntos queda registrado en el historial (seccion O); (d) al cerrar el expediente, el plazo de conservacion (OBL-RET-05, ver J) es el unico periodo en que se conservan estos datos, salvo que otra obligacion legal exija un plazo mayor.

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Numero de expediente | Identificador unico correlativo | Texto | Al registrar la solicitud | Responsable ARCO-POL, Titular (como referencia de seguimiento) |
| Checklist de los 7 elementos del Art. 18 | Marca de cumplido/pendiente por cada elemento | Vista en pantalla | Al registrar la solicitud, se recalcula con cada edicion | Responsable ARCO-POL |
| Calculo de plazos legales | Fecha limite de cada plazo aplicable (prevencion, general 20+20, incompetencia, notificacion a receptores, denegatoria, reclamo del titular) | Vista en pantalla + eventos en MOD-023 | Al admitir la solicitud, y se recalcula en cada evento relevante | Responsable ARCO-POL, Delegado, Notificaciones (MOD-022) |
| Tareas derivadas | Por ejemplo "localizar el dato en el Sistema X", "eliminar el CV del candidato", "dar de baja de la lista de marketing" | Registro en MOD-021 con responsable y fecha | Al clasificar el derecho y determinar las acciones necesarias | Responsable de area asignado, Responsable ARCO-POL |
| Borrador de prevencion | Lista de elementos faltantes del Art. 18, con plazo de 10 dias habiles | Documento (borrador) | Cuando la solicitud esta incompleta | Delegado (para aprobar), luego Titular (al notificarse) |
| Borrador de devolucion por incompetencia | Motivo de la incompetencia y orientacion al titular | Documento (borrador) | Cuando el Responsable ARCO-POL declara incompetencia | Delegado (para aprobar), luego Titular |
| Informe de acceso | Datos del titular, quienes los consultaron y con que proposito, intercambios con otras instituciones, sin datos de terceros | Documento | Al resolver una solicitud de Acceso | Delegado (para aprobar), luego Titular |
| Resolucion de reconocimiento (rectificacion, cancelacion, oposicion, portabilidad, limitacion, olvido) | Decision favorable, causal aplicada, accion ejecutada | Documento (borrador, luego version final) | Al concluir el analisis de procedencia | Delegado (para aprobar), luego Titular |
| Resolucion de denegatoria motivada | Causal tasada seleccionada, motivacion, pruebas | Documento (borrador, luego version final) | Cuando procede denegar total o parcialmente | Delegado y, si aplica, Aprobador (segundo revisor), luego Titular |
| Constancia de bloqueo cautelar | Fecha de activacion y de liberacion del bloqueo sobre el dato en revision | Registro | Al admitir una solicitud de rectificacion | Responsable ARCO-POL, Auditor |
| Notificacion a receptores | Lista de receptores/terceros que recibieron el dato y evidencia de cada notificacion enviada | Documento + registro | Al determinarse la procedencia de una rectificacion, cancelacion u olvido que ya fue transferido | Cada receptor identificado en MOD-009/MOD-010; copia en el expediente |
| Informe de actuaciones ante la ACE | Resumen de lo actuado en el expediente, en respuesta al requerimiento de la Direccion de Proteccion de Datos | Documento (borrador) | Cuando se registra un reclamo del titular ante la ACE | Delegado (para revisar antes de que la empresa lo remita) |
| Registro de tarifa aplicada | Monto cobrado (si hubo) y su fundamento en la tabla publicada | Registro | Al elegir una modalidad de entrega con costo | Titular (en la respuesta), Auditor |
| Evidencia del expediente | Ver seccion J | - | Continua durante todo el ciclo de vida | Centro de Evidencias (MOD-019) |
| Indicadores para el dashboard | Ver seccion M | Vista agregada | Actualizacion continua | Dashboard (MOD-020) |
| Eventos de auditoria | Ver seccion O | Registro append-only | Cada accion relevante | AuditLog transversal, Auditor |

---

## F. Workflow

### F.1 Diagrama de estados

```
                              +-----------------------+
                              |  NUEVA / RECIBIDA      |
                              |  (numero de expediente |
                              |   asignado)            |
                              +-----------+-----------+
                                          |
                                          v
                         +----------------+----------------+
                         |  VERIFICANDO IDENTIDAD           |
                         |  (tipo de solicitante,           |
                         |   documentos de D.2 a D.4)       |
                         +----------------+----------------+
                                          |
                    identidad no verificable (ver F.2 caso "sin firma / anonima")
                                          |
                              +-----------v-----------+
                              | VERIFICACION FALLIDA / |
                              | ANONIMA (advertencia)  |
                              +-----------+-----------+
                                          |  identidad verificada
                                          v
                         +----------------+----------------+
                         |  EVALUANDO REQUISITOS ART. 18    |
                         |  (checklist de 7 elementos)      |
                         +----+----------------------+-----+
                    incompleta|                       |completa
                              v                       v
                    +---------+--------+     +--------+---------+
                    | PREVENIDA         |     | ADMITIDA          |
                    | (10 dias habiles  |     | (arranca el plazo |
                    |  para subsanar)   |     |  de 20 dias        |
                    +----+---------+---+     |  habiles, MOD-023) |
           subsana dentro |         | vence sin  +----+-----------+
              del plazo   |         | subsanar        |
                    v     |         v                 v
          (vuelve a       |  +------+------+   +------+-------------------+
    EVALUANDO REQUISITOS) |  | ARCHIVADA    |   | EVALUANDO COMPETENCIA     |
                          |  | (terminal)   |   +------+-------------------+
                          |  +--------------+          |
                          |                    no competente | si competente
                          |                             v            v
                          |                  +----------+---+  +----+---------------+
                          |                  | DECLARADA     |  | EN ANALISIS DE     |
                          |                  | INCOMPETENTE  |  | PROCEDENCIA        |
                          |                  | (5 dias       |  | (segun el derecho   |
                          |                  |  habiles para |  |  ejercido)          |
                          |                  |  devolver)    |  +--+---------------+--+
                          |                  +-------+-------+     |               |
                          |                          v         procede      no procede /
                          |                  +-------+-------+   |          causal de
                          |                  | DEVUELTA AL   |   |          improcedencia
                          |                  | TITULAR       |   |               |
                          |                  | (terminal)    |   v               v
                          |                  +---------------+ +-+-----------+ +-+------------+
                          |                                    | PENDIENTE   | | PENDIENTE     |
                          |                                    | DE APROBAR  | | DE APROBAR    |
                          |                                    | RECONOCI-   | | DENEGATORIA   |
                          |                                    | MIENTO      | | (Delegado +   |
                          |                                    | (Delegado)  | | Aprobador si  |
                          |                                    +-+-----------+ | aplica)       |
                          |                                      |            +-+-------------+
                          |                                      v              |
                          |                            +---------+---------+    |
                          |                            | RECONOCIDA         |    |
                          |                            | (bloqueo cautelar  |    |
                          |                            |  si es             |    |
                          |                            |  rectificacion)    |    |
                          |                            +---------+---------+    |
                          |                                      |              |
                          |                        hubo transfer.|              |
                          |                        previa         v             |
                          |                            +---------+---------+    |
                          |                            | NOTIFICANDO A     |    |
                          |                            | RECEPTORES        |    |
                          |                            | (5 dias habiles)  |    |
                          |                            +---------+---------+    |
                          |                                      |              v
                          |                                      |      +-------+-------+
                          |                                      |      | DENEGADA       |
                          |                                      |      | (notificada en |
                          |                                      |      |  3 dias habiles)|
                          |                                      |      +-------+--------+
                          |                                      |              |
                          |                                      v              v
                          |                              +-------+--------------+---+
                          |                              |        CERRADA            |
                          |                              |  (retencion OBL-RET-05)   |
                          |                              +-------+--------------+---+
                          |                                      |
                          |                      reclamo del titular dentro de
                          |                      10 dias habiles (OBL-ARCO-14)
                          |                                      |
                          |                                      v
                          |                          +-----------+-----------+
                          |                          | RECLAMO ANTE LA ACE    |
                          |                          | (registrado, informe   |
                          |                          |  de actuaciones en     |
                          |                          |  preparacion)          |
                          |                          +-----------+-----------+
                          |                                      |
                          |                                      v
                          |                          +-----------+-----------+
                          |                          | INFORME REMITIDO       |
                          |                          | (la CERRADA original   |
                          |                          |  no se modifica;       |
                          |                          |  queda anotacion)      |
                          |                          +-----------------------+
                          |
                          v
                (cualquier estado activo puede pasar a
                 EN REVISION INTERNA si Legal o el Delegado
                 detecta un error antes del cierre, sin
                 reiniciar los plazos legales ya corridos)
```

### F.2 Tabla de transiciones

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (ninguno) | Se recibe una solicitud por cualquier canal | Ninguna | Nueva / Recibida | Sistema (automatico al registrar) o Titular (si usa el formulario) | Se genera el numero de expediente; evento de auditoria; alerta si no hay responsable asignado |
| Nueva / Recibida | Verificar identidad | El tipo de solicitante y sus documentos (D.2 a D.4) estan completos | Verificando identidad | Responsable ARCO-POL | Evento de auditoria con usuario y fecha |
| Verificando identidad | No es posible verificar por el canal usado | Ver F.3 caso "sin firma/anonima" | Verificacion fallida / Anonima | Responsable ARCO-POL | Advertencia visible; no se archiva automaticamente, requiere decision humana sobre como proceder |
| Verificando identidad | Identidad y representacion confirmadas | Documentos validos segun tipo de solicitante | Evaluando requisitos Art. 18 | Responsable ARCO-POL | Evento de auditoria |
| Evaluando requisitos Art. 18 | Checklist completo (7 elementos) | Todos los campos obligatorios de D.6 y D.7 presentes | Admitida | Sistema (automatico) | Arranca el contador de 20 dias habiles (MOD-023); tarea "Resolver solicitud" creada en MOD-021 |
| Evaluando requisitos Art. 18 | Checklist incompleto | Falta uno o mas de los 7 elementos | Prevenida | Sistema genera el borrador; Delegado aprueba y emite | Contador de 10 dias habiles (MOD-023); notificacion al titular; evento de auditoria |
| Prevenida | Titular subsana dentro del plazo | Documentacion o dato faltante recibido antes de vencer los 10 dias habiles | Evaluando requisitos Art. 18 | Titular (aporta), Responsable ARCO-POL (registra) | El contador de 10 dias se detiene; el computo del plazo general de 20 dias sigue el criterio conservador configurado (no suspende, ver G y H) |
| Prevenida | Vencen los 10 dias habiles sin subsanacion | Ninguna subsanacion registrada | Archivada (terminal) | Sistema (automatico) | Evidencia del archivo automatico; notificacion al Responsable ARCO-POL y al Delegado; no se puede reabrir con el mismo numero de expediente, el titular debe presentar una nueva solicitud |
| Admitida | Declarar incompetencia | El Responsable ARCO-POL determina que la empresa no es quien trata esos datos | Evaluando competencia -> Declarada incompetente | Responsable ARCO-POL redacta, Delegado aprueba | Contador de 5 dias habiles; borrador de devolucion motivada |
| Declarada incompetente | Notificar devolucion al titular | Dentro de los 5 dias habiles | Devuelta al titular (terminal) | Delegado (emite) | Evento de auditoria; se cuenta para el reporte de plazos |
| Admitida | Analizar procedencia segun el derecho ejercido | Ninguna adicional | En analisis de procedencia | Responsable ARCO-POL | Si es rectificacion, activa bloqueo cautelar sobre el dato referenciado en el RAT |
| En analisis de procedencia | Se determina que procede (cumple causal tasada, no hay causal de improcedencia) | Checklist de causales de D.7 completado | Pendiente de aprobar reconocimiento | Responsable ARCO-POL redacta | Advertencia "Requiere validacion de la organizacion o asesoria especializada" si hay ambiguedad marcada |
| En analisis de procedencia | Se determina que no procede o corresponde denegar total/parcialmente | Debe seleccionarse una de las 8 causales tasadas del Art. 22 | Pendiente de aprobar denegatoria | Responsable ARCO-POL redacta; Aprobador revisa si aplica escalamiento | Contador de 3 dias habiles arranca al aprobarse la decision, no al iniciar el borrador. Si la solicitud es de cancelacion u olvido y el dato consultado en MOD-016 esta en estado "retenido por obligacion", el sistema precarga en este paso el borrador de denegatoria parcial motivada que genera MOD-016, para revision del Responsable ARCO-POL y aprobacion del Delegado (ver seccion L.2 y `03_modulos/MOD-016_ficha.md`, seccion G, automatizacion 10) |
| Pendiente de aprobar reconocimiento | Delegado/Responsable interno aprueba | Aprobacion explicita registrada (decision 2.7.22) | Reconocida | Delegado / Responsable interno | Se ejecuta la accion (por ejemplo, se crea la tarea de eliminacion en el area correspondiente); libera el bloqueo cautelar si corresponde |
| Reconocida | El dato ya fue transferido a un receptor previamente | Existe un registro de transferencia/receptor vinculado en MOD-009/MOD-010 para ese Tratamiento | Notificando a receptores | Responsable ARCO-POL (ejecuta), Delegado (aprueba el envio) | Contador de 5 dias habiles por cada receptor pendiente |
| Notificando a receptores | Todos los receptores notificados | Evidencia de notificacion de cada uno | Cerrada | Sistema (automatico al completar la lista) | Fecha de cierre; arranca el plazo de retencion del expediente (OBL-RET-05) |
| Reconocida | No hubo transferencia previa | Ninguna | Cerrada | Delegado (cierra) | Igual que arriba |
| Pendiente de aprobar denegatoria | Delegado/Responsable interno (y Aprobador si aplica) aprueban | Aprobacion explicita de ambos si el caso requiere segundo revisor | Denegada | Delegado / Responsable interno | Contador de 3 dias habiles para notificar |
| Denegada | Se notifica al titular por el medio que este senalo | Dentro de los 3 dias habiles | Cerrada | Delegado (emite) | Fecha de cierre; arranca retencion |
| Cerrada | El titular presenta reclamo ante la Direccion de Proteccion de Datos de la ACE | Dentro de los 10 dias habiles desde la notificacion de la resolucion | Reclamo ante la ACE | Responsable ARCO-POL registra, Delegado gestiona | El expediente original no se modifica; se abre un sub-registro de reclamo |
| Reclamo ante la ACE | Se remite el informe de actuaciones que la ACE solicito | Informe revisado y autorizado por la empresa antes del envio | Informe remitido | Delegado (prepara), Administrador o Delegado (autoriza el envio real fuera del sistema, anti-feature 13) | Evidencia del informe conservada junto al expediente |
| Cualquier estado activo (no terminal) | Legal o el Delegado detecta un error material antes del cierre | Justificacion registrada | En revision interna -> vuelve al estado anterior corregido | Legal, Delegado | No reinicia los contadores de plazo ya corridos; queda evidencia del ajuste |

**Estados terminales:** Archivada, Devuelta al titular, Cerrada (con o sin reclamo posterior), Informe remitido (sub-estado de Cerrada). Ningun estado terminal admite edicion de los campos de fondo del expediente; solo admite anotaciones nuevas (por ejemplo, el registro de un reclamo posterior) y la aplicacion del plazo de retencion.

**Reapertura.** Un expediente Archivado por falta de subsanacion no se reabre: el titular debe presentar una solicitud nueva con numero de expediente distinto (evita alterar el computo del plazo original). Un expediente Cerrado no se reabre para cambiar la resolucion; solo se anota el reclamo ante la ACE como un evento posterior vinculado, preservando integra la resolucion original (Art. 33 inc. 4 Lineamientos DPO no da a la Direccion de Proteccion de Datos facultad de revocar la resolucion del delegado, solo de requerir informe).

**Registros vinculados al cerrar o archivar.** Al cerrarse o archivarse un expediente, las tareas derivadas en MOD-021 que sigan abiertas se marcan como huerfanas y se notifican al Responsable ARCO-POL para su cierre manual; el bloqueo cautelar, si estaba activo, se libera; la referencia al Tratamiento del RAT permanece sin cambios (el expediente solo referencia, nunca modifica, el RAT).

### F.3 Casos especiales

| Caso | Tratamiento en el modulo |
|---|---|
| Solicitud anonima (no es posible verificar identidad) | Se marca "Verificacion fallida / Anonima"; el sistema no la rechaza automaticamente (no hay causal legal expresa de improcedencia por anonimato en el Art. 10, y el Art. 18 exige identidad pero no prejuzga la consecuencia de no lograrla); el Responsable ARCO-POL decide como proceder con advertencia visible; anti-feature 20 exige que exista siempre algun mecanismo minimo de verificacion configurable por canal |
| Solicitud masiva o abusiva | El sistema detecta automaticamente un patron (mismo remitente, mismo documento de identidad o mismo correo, varias solicitudes en un periodo corto) y marca el expediente con una bandera informativa; no existe en la ley una causal tasada de "solicitud abusiva" para el sector privado salvadoreno, por lo que el sistema NO deniega automaticamente ni acelera el archivo; solo alerta al Delegado para que decida con criterio humano |
| Solicitud sin firma | Se acepta si el canal usado permite un medio equivalente reconocido (por ejemplo, aceptacion desde el correo previamente registrado del titular en un sistema de la empresa); si no hay medio equivalente disponible, se trata igual que el caso "anonima" |
| Solicitud por WhatsApp, correo electronico o presencial | El canal se registra en el campo "Canal de recepcion" (D.6); en todos los casos el Responsable ARCO-POL traslada la informacion al mismo formulario interno (D.1 a D.10), adjuntando la captura o transcripcion del mensaje original como evidencia; el plazo corre desde la recepcion efectiva, no desde su transcripcion al sistema |
| Datos en poder de un encargado (proveedor) | El expediente referencia el Encargado de MOD-009 vinculado al Tratamiento; la tarea de ejecutar la accion (por ejemplo, eliminar el dato) se asigna al Responsable de area con copia al contrato/DPA de ese encargado; el plazo legal de 20+20 dias corre igual frente al titular, sin extenderse por la gestion con el encargado |
| Datos disociados | El Art. 10 inciso 2 excluye de la cancelacion los datos disociados; el checklist de causales de improcedencia de D.7 incluye esta opcion; requiere criterio humano para confirmar que la disociacion es efectiva (no reversible), ver seccion H |
| Datos de terceros mezclados con los del titular (por ejemplo, en un correo o en un expediente compartido) | El informe de acceso (OBL-ARCO-02) filtra automaticamente cualquier dato identificado como perteneciente a un tercero antes de generar el borrador, pero la verificacion final de que no quedo ningun dato de tercero es responsabilidad humana antes de aprobar |
| Titular fallecido | Ver D.4; requiere partida de defuncion y prueba de vinculo antes de admitir; el derecho se ejerce en nombre del titular fallecido segun el Art. 6, no crea un derecho propio del heredero sobre datos ajenos |
| Titular menor de edad | Ver D.5; conecta con el sub-flujo de consentimiento parental de MOD-007 (OBL-CONS-06, OBL-PRIN-04) |
| Solicitud duplicada (mismo titular, mismo derecho, dentro de un expediente ya abierto o recien cerrado) | El sistema alerta al registrar una nueva solicitud si detecta coincidencia de documento de identidad y derecho ejercido con un expediente abierto o cerrado en los ultimos 20 dias habiles; no la bloquea automaticamente (el titular tiene derecho a insistir o aclarar), pero facilita vincular ambos expedientes para evitar respuestas contradictorias |
| Solicitud recibida durante un incidente de seguridad activo (MOD-013) | Si el Tratamiento o sistema referenciado en la solicitud coincide con el que esta bajo investigacion en un incidente abierto, el sistema muestra una nota cruzada al Responsable ARCO-POL y al responsable del incidente; el plazo de la solicitud ARCO-POL sigue corriendo igual, sin suspenderse por el incidente, salvo decision expresa y documentada de la organizacion |

---

## G. Automatizaciones

| # | Disparador | Condicion | Accion | Configurable por la empresa |
|---|---|---|---|---|
| 1 | Se completa el registro de una solicitud | Los 7 elementos del Art. 18 estan presentes | Pasa automaticamente a Admitida y arranca el contador de 20 dias habiles en MOD-023 | No (el plazo legal no es configurable; si lo es el destinatario de la tarea generada) |
| 2 | Se completa el registro de una solicitud | Falta uno o mas de los 7 elementos | Genera el borrador de prevencion y el contador de 10 dias habiles | No en el plazo; si en el texto adicional que puede agregar el Responsable ARCO-POL |
| 3 | Vence el plazo de prevencion | No se registro subsanacion | Archiva automaticamente el expediente y notifica al Responsable ARCO-POL y al Delegado | No |
| 4 | Se admite una solicitud | Ninguna adicional | Crea la tarea "Resolver solicitud" en MOD-021 con fecha limite igual al plazo de 20 dias habiles | Si, en cuanto a quien se asigna por defecto |
| 5 | Se determina la procedencia de rectificacion, cancelacion u olvido | Existe registro de transferencia o receptor vinculado al Tratamiento en MOD-009/MOD-010 | Genera automaticamente la lista de receptores a notificar y el contador de 5 dias habiles por cada uno | No en el plazo |
| 6 | Se aprueba una denegatoria | Ninguna adicional | Arranca el contador de 3 dias habiles para notificar | No |
| 7 | Se declara incompetencia | Ninguna adicional | Genera el borrador de devolucion y el contador de 5 dias habiles | No |
| 8 | Faltan X dias habiles para vencer cualquiera de los plazos del modulo | X configurable (por defecto: 5 dias para el plazo general, 3 dias para prevencion, 2 dias para incompetencia/notificacion/denegatoria) | Genera alerta (ver seccion I) | Si, el umbral de dias de aviso |
| 9 | Se marca "Los datos corresponden a un titular de ninez o adolescencia" | Ninguna adicional | Vincula el expediente al sub-flujo de consentimiento parental de MOD-007 y muestra el aviso de tension normativa (D.5) | No en el contenido del aviso; si en a quien se notifica |
| 10 | Se marca "Los datos corresponden a una persona fallecida" | Ninguna adicional | Exige partida de defuncion y prueba de vinculo antes de permitir avanzar a Verificando identidad -> completada | No |
| 11 | El expediente pasa a Cerrada | Ninguna adicional | Calcula la fecha sugerida de fin de retencion (cierre + 5 anos, OBL-RET-05, criterio recomendado) y la envia a MOD-016 | Si, si la empresa tiene otro plazo mayor aplicable por otra norma (por ejemplo mercantil, 10 anos) |
| 12 | Se registra un reclamo del titular ante la Direccion de Proteccion de Datos dentro de los 10 dias habiles de notificada la resolucion | Ninguna adicional | Crea la tarea "preparar informe de actuaciones" para el Delegado, sin reabrir ni modificar la resolucion original | No |
| 13 | Se marca "Es oposicion a mercadotecnia directa / perfilado" y se reconoce la oposicion | Ninguna adicional | Envia el dato del titular a la lista de supresion de MOD-007/Consentimiento | Si, el canal de sincronizacion con la lista |
| 14 | La bandera de doble estado de la reforma 659 en MOD-024 cambia de ACTUAL a FUTURO | Cambio confirmado manualmente por el equipo del producto (nunca automatico por la sola aprobacion legislativa) | Para expedientes nuevos, el aprobador por defecto de todo acto atribuido a "el Delegado" pasa a ser la persona con el rol Responsable interno vigente; los expedientes ya cerrados o en curso bajo el estado ACTUAL conservan su regla original en el historial | No en la regla de negocio (viene del Centro Regulatorio); si en quien ocupa cada rol |
| 15 | Se detecta el mismo documento de identidad o correo con varias solicitudes en un periodo corto | Umbral configurable (por defecto: 3 solicitudes en 30 dias) | Marca el expediente como "potencialmente masiva/abusiva" (ver F.3); solo alerta, nunca deniega ni archiva automaticamente | Si, el umbral |
| 16 | Se detecta un documento de identidad o correo coincidente con un expediente abierto o cerrado en los ultimos 20 dias habiles, mismo derecho | Ninguna adicional | Muestra alerta de posible duplicado y ofrece vincular ambos expedientes | No en la deteccion; si en el umbral de dias |

---

## H. Decisiones que NO debe automatizar

- **Si una solicitud de cancelacion cumple realmente una causal tasada de procedencia y no cae en ninguna de las 6 causales de improcedencia (Art. 10).** El sistema presenta el checklist y ambas listas tasadas, pero la valoracion de si el caso concreto encaja es de una persona. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada."
- **La ponderacion de interes legitimo prevalente para negar una oposicion (Art. 12).** No existe formula ni umbral legal para "prevalencia"; requiere criterio humano, con posible consulta a Legal o a un asesor externo.
- **Confirmar que la base juridica del tratamiento realmente sea consentimiento y que el tratamiento sea automatizado, antes de habilitar la portabilidad (Art. 14).** El sistema verifica lo que esta registrado en el RAT (MOD-006), pero si hay duda sobre si esa base es correcta, la decision es humana.
- **Determinar si un encargado extranjero (por ejemplo, un proveedor de nube) cuenta como "receptor" que debe notificarse bajo el Art. 21 inc. 3, o si es un encargado sin esa obligacion.** Es una de las incertidumbres documentadas (tension entre el Art. 4 lit. u, que excluye al encargado de la definicion de transferencia, y los Arts. 44-45); el sistema aplica el criterio conservador de tratarlo como receptor a notificar por defecto, pero deja la decision final visible como ajustable por una persona con nota de riesgo.
- **Resolver la solicitud en si misma (reconocer o denegar).** El sistema calcula el plazo, presenta las causales tasadas aplicables y prepara el borrador; el Delegado o Responsable interno decide y aprueba antes de que cualquier acto se considere emitido (decision 2.7.22; anti-feature 7).
- **Determinar si aplica alguna exclusion del Art. 3 al caso concreto** (por ejemplo, si el dato objeto de la solicitud es historial crediticio bajo ley especial, o dato de ambito estrictamente domestico).
- **Decidir si la prevencion suspende o no el computo del plazo general de 20 dias habiles.** Es una incertidumbre juridica no resuelta (incertidumbre 16 de `03_hallazgos_regulatorios.md`, por analogia con el Art. 90.1 de la Ley de Procedimientos Administrativos). El sistema aplica por defecto el criterio conservador configurado por el producto (no suspende: los dias de prevencion cuentan dentro de los 20), mostrando siempre el texto: "La ley no precisa si la prevencion suspende este plazo. El sistema aplica por defecto el criterio mas conservador (no suspende). Verifique este criterio con asesoria legal si el caso es critico."
- **Determinar si un titular adolescente (12 a 18 anos) puede ejercer un derecho ARCO-POL por si mismo sin consentimiento parental**, ante la tension entre el Art. 5 lit. j LPDP (ejercicio progresivo de facultades) y el Art. 77 de la Ley Crecer Juntos. El sistema muestra ambas normas y la marca como pendiente de criterio juridico, sin fijar una regla automatica de edad.
- **Autorizar el envio real del informe de actuaciones a la Direccion de Proteccion de Datos de la ACE.** El sistema prepara el borrador; la empresa (Delegado o Administrador) revisa y ejecuta el envio por el canal oficial (anti-feature 13).
- **Confirmar que una disociacion de datos es efectiva e irreversible** antes de aplicarla como causal de improcedencia de una cancelacion (Art. 10 inciso 2).

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Solicitud nueva sin responsable asignado | Se recibe la solicitud y no tiene Responsable ARCO-POL asignado | WARNING | Administrador, Delegado | Plataforma + correo | Inmediata, se repite cada 24 horas | Escala al Delegado si sigue sin asignar 24 horas despues | Se asigna un responsable |
| Prevencion proxima a vencer | Faltan 3 dias habiles de los 10 | WARNING | Responsable ARCO-POL | Plataforma + correo | Diaria mientras dure | Escala al Delegado si falta 1 dia habil | Se subsana o se archiva |
| Plazo general proximo a vencer | Faltan 5 dias habiles de los 20 (o de la prorroga) | HIGH | Responsable ARCO-POL, Delegado | Plataforma + correo | Diaria | Escala a Administrador si faltan 2 dias habiles | Se cierra o se resuelve |
| Plazo general vencido | Transcurrieron los 20 (o 40 con prorroga) dias habiles sin resolucion | CRITICAL | Delegado, Administrador | Plataforma + correo | Inmediata al vencer, luego diaria | Escala a la vista de Gerencia del dashboard | Se cierra el expediente (el vencimiento queda registrado permanentemente en el historial) |
| Notificacion a receptores pendiente | Procedencia declarada con receptores por notificar, faltan 2 dias habiles de los 5 | WARNING | Responsable ARCO-POL | Plataforma | Diaria | Escala al Delegado si falta 1 dia habil | Todos los receptores quedan notificados |
| Denegatoria pendiente de notificar | Denegatoria aprobada, faltan dias de los 3 habiles | HIGH | Responsable ARCO-POL | Plataforma + correo | Diaria | Escala al Delegado si falta el ultimo dia habil | Se notifica al titular |
| Incompetencia pendiente de devolver | Declarada, faltan dias de los 5 habiles | WARNING | Responsable ARCO-POL | Plataforma + correo | Diaria | Escala al Delegado si falta 1 dia habil | Se notifica la devolucion |
| Reclamo recibido de la Direccion de Proteccion de Datos de la ACE | Se registra un reclamo dentro del expediente | CRITICAL | Delegado, Legal, Administrador | Plataforma + correo | Inmediata | Escala a Gerencia | Se remite el informe de actuaciones |
| Solicitud pendiente de aprobacion del Delegado | Borrador listo, sin aprobacion en X dias | WARNING | Delegado / Responsable interno | Plataforma + correo | Diaria | Escala a Administrador si pasan 2 dias sin aprobar | Se aprueba o se rechaza el borrador |
| Bloqueo cautelar activo por mas del plazo general | El dato sigue bloqueado despues de vencer el plazo de 20+20 dias sin resolucion | HIGH | Delegado, Responsable de area | Plataforma | Diaria | Escala a Administrador | Se libera el bloqueo al cerrar el expediente |
| Solicitud potencialmente masiva o abusiva detectada | Umbral configurable superado (ver G.15) | INFO | Delegado | Plataforma | Unica por deteccion | No escala automaticamente | El Delegado revisa y descarta o actua la alerta |
| Retencion del expediente proxima a vencer | Faltan 90 dias para cumplirse el plazo de retencion sugerido (5 anos) | INFO | Administrador, Auditor | Plataforma | Unica | No escala | Se decide conservar (por otra obligacion) o se ejecuta la purga documentada |

---

## J. Evidencia

| Evidencia que genera o conserva el modulo | Como se registra | OBL-ID que prueba | Retencion |
|---|---|---|---|
| Expediente con fecha/hora de recepcion, canal usado y version del formulario (propio o ACE) | Registro con timestamp, usuario, hash del archivo si el titular cargo el formulario oficial | OBL-ARCO-15, OBL-DOC-04, OBL-PLAZO-04 | 5 anos desde el cierre (minimo recomendado, OBL-RET-05) |
| Checklist de verificacion de los 7 elementos del Art. 18, con usuario y fecha de cada marca | Registro inmutable | OBL-ARCO-08 | 5 anos desde el cierre |
| Registro de verificacion de identidad y representacion (tipo de solicitante, documentos adjuntos con hash de integridad) | Adjunto cifrado + hash | OBL-ARCO-01 | 5 anos desde el cierre |
| Historial completo de estados con fecha/hora y usuario (creacion, prevencion, admision, aprobaciones, notificaciones, cierre) | AuditLog append-only, sin edicion ni borrado para ningun rol | OBL-ARCO-10 (trazabilidad del plazo maestro) | 5 anos desde el cierre |
| Version de la prevencion enviada y constancia de su notificacion | Documento versionado + registro de envio | OBL-ARCO-08 | 5 anos desde el cierre |
| Registro de activacion y liberacion del bloqueo cautelar, con fecha | Registro con timestamp | OBL-ARCO-03 | 5 anos desde el cierre |
| Resolucion motivada de denegatoria, con la causal tasada seleccionada y la aprobacion del Delegado (identidad y fecha) | Documento version final + firma de aprobacion en el sistema | OBL-ARCO-12 | 5 anos desde el cierre |
| Constancia de notificacion al titular (fecha, medio efectivamente usado, coincidencia con el medio que el titular senalo) | Registro | OBL-ARCO-12 | 5 anos desde el cierre |
| Lista de receptores notificados, con fecha de cada notificacion individual | Registro por receptor | OBL-ARCO-11 | 5 anos desde el cierre |
| Informe de acceso generado, version final entregada | Documento versionado | OBL-ARCO-02 | 5 anos desde el cierre |
| Registro de tarifa aplicada o de gratuidad | Registro | OBL-ARCO-13 | 5 anos desde el cierre |
| Registro de declaracion de incompetencia y de la devolucion notificada | Documento + registro de envio | OBL-ARCO-09 | 5 anos desde el cierre |
| Registro del reclamo recibido de la Direccion de Proteccion de Datos y del informe de actuaciones preparado/remitido | Documento + registro | OBL-ARCO-14 | 5 anos desde el cierre del expediente principal |
| Aprobacion explicita del Delegado/Responsable interno antes de cada acto emitido | Registro de aprobacion con identidad y fecha, distinto del registro de quien redacto el borrador | Refuerza todas las OBL-ARCO anteriores y el principio de responsabilidad demostrada (propiedad de MOD-019) | 5 anos desde el cierre |
| Registro de accesos de lectura a documentos de identidad del titular (quien vio el DUI, cuando) | AuditLog | Buena practica de seguridad, sin OBL-ID propio | 5 anos desde el cierre |
| Exportacion del expediente completo con verificacion de integridad (hash o firma) | Paquete exportable a traves de MOD-019 | Anti-feature 25, decision 2.7.24 | Igual que el expediente |

**Sobre el plazo de retencion.** No existe en la LPDP, la Normativa Sancionadora, los Lineamientos DPO ni las Politicas ACE una norma expresa que fije cuanto debe conservarse el expediente de una solicitud ARCO-POL. OBL-RET-05 es una obligacion clasificada RECOMENDADO (no OBLIGATORIO) que usa por analogia el plazo de prescripcion de infracciones y sanciones (5 anos, Art. 47 Normativa PAS) como minimo razonable. El sistema aplica este minimo por defecto, mostrando siempre la leyenda "criterio propio del producto ante ausencia de norma expresa, requiere validacion de asesoria legal", y permite a la empresa configurar un plazo mayor si otra norma aplicable al dato especifico lo exige (por ejemplo, retencion mercantil o tributaria de 10 anos si el expediente ademas contiene un comprobante fiscal).

---

## K. Documentos asociados

**Documentos requeridos como entrada.**
- Documento Unico de Identidad (DUI) del solicitante.
- Poder de representacion (si el solicitante es representante o apoderado).
- Certificacion de partida de nacimiento y, si existe, carne de minoridad (si el titular es NNA).
- Certificacion de partida de defuncion y documento de vinculo familiar (si el titular fallecio y solicita un heredero o sucesor).
- Formulario oficial ARCO-POL de la ACE ya diligenciado (si el titular opto por usarlo en vez del formulario interno; OBL-ARCO-15).
- Pruebas o documentos adicionales que el titular aporte para sustentar su solicitud.

**Documentos generados por el sistema (todos como borrador, requieren revision y aprobacion de la organizacion, banner de `04_objetivo_exacto_del_producto.md` seccion 1.3).**
- Prevencion (Art. 18 inciso final).
- Devolucion motivada por incompetencia (Art. 19).
- Resolucion de reconocimiento del derecho ejercido (rectificacion, cancelacion, oposicion, portabilidad, limitacion u olvido).
- Resolucion de denegatoria motivada (Art. 22), con la causal tasada y las pruebas.
- Informe de acceso (Art. 8), sin datos de terceros.
- Constancia de bloqueo cautelar (Art. 9).
- Notificacion a receptores (Art. 21 inc. 3).
- Informe de actuaciones para responder al requerimiento de la Direccion de Proteccion de Datos de la ACE (Art. 33 inc. 4 Lineamientos DPO).

**Plantillas que el sistema provee.**

| Plantilla | Variables principales | Requiere validacion de la organizacion |
|---|---|---|
| Los 7 formularios oficiales ARCO-POL de la ACE (version 07-07-2025), cargables directamente | Datos de la entidad, del solicitante, del derecho | No modificable: son formularios oficiales que deben aceptarse tal cual (OBL-ARCO-15) |
| Formulario interno equivalente (D.1 a D.10 de este documento) | Los mismos campos, en lenguaje simplificado | Si, en su redaccion inicial por parte del Administrador |
| Plantilla de prevencion | Elementos faltantes, plazo, expediente | Si, antes de emitirse (aprobacion del Delegado) |
| Plantilla de denegatoria motivada | Causal tasada, motivacion, pruebas, expediente | Si, siempre (aprobacion del Delegado y, si aplica, del Aprobador) |
| Plantilla de notificacion a receptores | Lista de receptores, dato afectado, accion tomada | Si |
| Plantilla de informe de acceso | Datos del titular, consultas registradas, proposito, intercambios | Si |
| Plantilla de informe de actuaciones ante la ACE | Resumen del expediente, actos realizados, fechas | Si, y ademas requiere autorizacion expresa de envio fuera del sistema |

**Anexos y evidencias documentales.** Todos los archivos adjuntos por el titular o generados por el sistema quedan vinculados al expediente con hash de integridad y disponibles para el paquete de evidencias exportable de MOD-019.

---

## L. Dependencias

### L.1 Diagrama

```
         MOD-002 Delegado/            MOD-007            MOD-012 Portal
         Resp. Interno                Consentimiento      del Titular
              |                            |                    |
              | (aprobador por defecto     | (sub-flujo NNA,    | (canal publico
              |  de los actos legales)     |  lista supresion)  |  adicional, SHOULD)
              v                            v                    v
         +---------------------------------------------------------+
         |                    MOD-011 ARCO-POL                      |
         |  PrivacyRequest ; IdentityVerification                   |
         +--------+--------+---------+---------+---------+----------+
                  |        |         |         |         |
                  v        v         v         v         v
             MOD-009    MOD-010   MOD-019   MOD-021   MOD-022
             Proveed.   Transfer. Evidencias Tareas    Notific.
                  |        |
                  v        v
             (receptores a notificar,
              lectura de referencia)

         MOD-023 Calendario/Motor de Plazos ---> (consultado por MOD-011
                                                    para calcular todos
                                                    los plazos habiles)
         MOD-024 Centro Regulatorio ---> (consultado por MOD-011 para
                                            saber si aplica el estado
                                            ACTUAL o FUTURO del doble
                                            estado de la reforma 659)
```

### L.2 Lista

**De que modulos recibe datos (depende_de, segun `mapa_modulos.json`):**
- MOD-012 Portal del Titular: si esta activo, alimenta solicitudes recibidas por el canal publico; si no existe en el MVP, este modulo funciona igual usando solo el formulario interno seguro (decision 2.7.30), sin que se pierda cobertura legal.
- MOD-007 Consentimiento: referencia la version del aviso mostrado, el sub-flujo de consentimiento parental (NNA) y la lista de supresion de marketing directo.
- MOD-002 Delegado / Responsable Interno de Datos: determina quien ocupa el rol de aprobador por defecto de todo acto legalmente atribuido al "Delegado", segun el estado ACTUAL o FUTURO vigente.

**Lecturas de referencia adicionales (no listadas como `depende_de` estructural en el mapa, pero necesarias funcionalmente, siguiendo la convencion de la seccion 6.1 de `06_mapa_definitivo_de_modulos.md`):**
- MOD-001 Organizacion y Personas: datos de la entidad responsable (D.1) y catalogo de usuarios/roles.
- MOD-006 RAT y Mapa de Datos: para sugerir el area que trata los datos y para referenciar el Tratamiento relacionado con la solicitud, sin duplicar el RAT.
- MOD-009 Proveedores y Encargados / MOD-010 Transferencias Internacionales: para construir automaticamente la lista de receptores a notificar (OBL-ARCO-11) y para saber si un tratamiento de marketing directo tiene proveedores externos vinculados. Ver nota al final de este documento sobre una posible correccion al mapa de dependencias en este punto.
- MOD-016 Retencion y Eliminacion: al resolver una solicitud de cancelacion u olvido, se consulta si el dato esta en estado "retenido por obligacion" y, de ser asi, se recibe el borrador de denegatoria parcial motivada que genera MOD-016 (Art. 22, OBL-ARCO-06), para revision del Responsable ARCO-POL y aprobacion del Delegado antes de enviarse (ver seccion F.2, fila "En analisis de procedencia" -> "Pendiente de aprobar denegatoria", y `03_modulos/MOD-016_ficha.md`, secciones B, E y G automatizacion 10).
- MOD-023 Calendario y Motor de Plazos: unico servicio consultado para calcular los seis plazos habiles de este modulo.
- MOD-024 Centro Regulatorio: unico origen de la bandera de doble estado (ACTUAL/FUTURO) de la reforma 659.

**A que modulos envia datos o eventos (alimenta_a, segun `mapa_modulos.json`):**
- MOD-009 Proveedores y Encargados / MOD-010 Transferencias Internacionales: notificaciones salientes a receptores y terceros identificados durante una solicitud.
- MOD-019 Centro de Evidencias: toda la evidencia descrita en la seccion J.
- MOD-021 Centro de Tareas: cada tarea derivada de una solicitud.
- MOD-022 Notificaciones: cada alerta descrita en la seccion I.
- MOD-023 Calendario y Motor de Plazos: cada solicitud de calculo de plazo (relacion de consulta continua).
- MOD-024 Centro Regulatorio: eventos relacionados con el reclamo del titular ante la ACE (OBL-ARCO-14, colaborador de OBL-SANC-09) y con el cambio de estado de la reforma 659.

**Que ocurre si un modulo dependiente no existe en el MVP.**
- Si MOD-012 Portal del Titular no esta disponible (es SHOULD HAVE): el modulo sigue cumpliendo la obligacion legal de mecanismos de ejercicio de derechos (OBL-DOC-04, OBL-PLAZO-04) con el formulario interno seguro; el titular presenta su solicitud de forma asistida por la empresa.
- Si MOD-010 Transferencias Internacionales no esta completo (es SHOULD HAVE): la notificacion a receptores (OBL-ARCO-11) se apoya solo en el registro de MOD-009 (Proveedores/Terceros-Receptores, que si es MUST HAVE) y, cuando no exista un registro formal de transferencia, el Responsable ARCO-POL debe identificar manualmente a los receptores extranjeros, con una tarea manual en MOD-021, sin el motor de deteccion automatica completo (mismo patron de cobertura parcial documentado en la ficha de MOD-010).

---

## M. Dashboard

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Solicitudes abiertas por estado | Conteo de expedientes activos agrupados por estado del workflow | Sin semaforo, vista de distribucion | Gerencia (resumen), Responsable (su cola) |
| Solicitudes proximas a vencer | Expedientes con menos de X dias habiles para su plazo aplicable | Amarillo si falta menos del 25% del plazo, rojo si falta menos del 10% | Responsable, Legal/Delegado |
| Solicitudes vencidas | Expedientes cuyo plazo legal aplicable ya paso sin resolucion | Rojo siempre que exista al menos una | Gerencia, Legal/Delegado, Auditor |
| Tiempo promedio de resolucion | Promedio de dias habiles entre admision y cierre, de los expedientes cerrados en el periodo | Verde si es menor al plazo general, amarillo si se acerca, rojo si lo supera en promedio | Legal/Delegado, Auditor |
| Solicitudes resueltas dentro del plazo legal aplicable | (Cerradas dentro de plazo) / (Total cerradas en el periodo) x 100, mostrado como "estado del programa", nunca como "cumplimiento legal" | Verde/amarillo/rojo segun umbral configurable | Gerencia, Legal/Delegado |
| Solicitudes con prevencion activa | Conteo de expedientes en estado Prevenida | Sin semaforo | Responsable, Legal/Delegado |
| Reclamos ante la Direccion de Proteccion de Datos abiertos | Conteo de expedientes con reclamo registrado sin informe remitido | Rojo si hay al menos uno | Gerencia, Legal/Delegado, Auditor |
| Expedientes con evidencia completa vs. incompleta (checklist de la seccion J) | (Expedientes con todos los items de evidencia esperada) / (Total cerrados) | Verde/amarillo/rojo | Auditor, Legal/Delegado |

Todo indicador se presenta como "estado del programa" (por ejemplo "Solicitudes dentro de plazo: 92%. Solicitudes vencidas: 1.") y nunca como un porcentaje de "cumplimiento legal", conforme a la regla transversal de `04_objetivo_exacto_del_producto.md`.

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Reporte de solicitudes ARCO-POL | Listado de expedientes con estado, derecho ejercido, fechas y cumplimiento de plazo | Periodo, estado, derecho, responsable | PDF, XLSX | Delegado, Gerencia | Si |
| Estadisticas ARCO-POL para el informe periodico del Delegado (semestral) | Volumen por derecho, tiempo promedio de resolucion, incidencias de plazo vencido | Periodo (semestral) | PDF | Delegado (para su informe al responsable, OBL-DPO-07 de MOD-002) | Si |
| Paquete de evidencia de un expediente individual | Todo el contenido de la seccion J, con verificacion de integridad | Numero de expediente | ZIP con hash/firma | Auditor, ACE (si la empresa lo entrega ante un requerimiento) | Si |
| Reporte de reclamos ante la Direccion de Proteccion de Datos | Listado de reclamos, estado del informe de actuaciones | Periodo, estado | PDF, XLSX | Delegado, Legal | Si |
| Reporte de tarifas cobradas | Listado de cobros de reproduccion/envio efectivamente realizados, con su fundamento en la tabla publicada | Periodo | XLSX | Administrador, Auditor | Si |

---

## O. Historial

Eventos que quedan registrados en el historial del expediente y en el AuditLog transversal (MOD-019), todos con fecha, hora y usuario, de forma append-only (sin edicion ni borrado para ningun rol, anti-feature 19):

- Creacion de la solicitud y canal de recepcion.
- Cada cambio de campo relevante (valor anterior y nuevo), por ejemplo la correccion de un dato de contacto del solicitante.
- Cada cambio de estado del workflow (seccion F).
- Asignacion y reasignacion del Responsable ARCO-POL.
- Envio de la prevencion y recepcion de la subsanacion (si ocurre).
- Declaracion de incompetencia y su devolucion.
- Activacion y liberacion del bloqueo cautelar.
- Aprobaciones del Delegado/Responsable interno en cada acto (prevencion, incompetencia, resolucion, notificacion a receptores), como evento separado de la redaccion del borrador.
- Notificaciones enviadas al titular (medio, fecha, contenido referenciado).
- Cada notificacion individual a un receptor.
- Registro del reclamo ante la Direccion de Proteccion de Datos y del informe de actuaciones remitido.
- Adjuntos cargados (quien, cuando, hash del archivo).
- Accesos de lectura a documentos de identidad del titular (DUI, partidas, poder).
- Exportaciones del expediente o del paquete de evidencia (quien, cuando, para que finalidad declarada).
- Archivado por falta de subsanacion, con el motivo automatico.
- Cierre del expediente, con el motivo (reconocimiento o denegatoria).
- Cualquier ajuste registrado desde "En revision interna" (seccion F.2), con el motivo y sin alterar los contadores de plazo ya corridos.

---

## P. Riesgos

| Riesgo | Tipo | Mitigacion de diseno |
|---|---|---|
| Dar por valida automaticamente una causal de cancelacion, oposicion o denegatoria sin criterio humano suficiente | Legal | Checklist obligatorio de causales tasadas + aprobacion explicita del Delegado/Responsable interno antes de emitir cualquier acto (seccion H) |
| Abandono del formulario por su extension (7 elementos obligatorios mas documentos segun el tipo de solicitante) | UX | Wizard por pasos que muestra solo los campos relevantes segun el tipo de solicitante y el derecho elegido; guardado de borrador; lenguaje simple con ejemplos, conforme al Art. 5 lit. e (principio de transparencia) |
| Plazos mal calculados por un calendario de dias habiles desactualizado o mal configurado | Operativo | Un unico motor de plazos (MOD-023) consultado por todo el modulo, con alerta si el calendario del ano en curso no esta configurado antes de admitir una solicitud |
| Exposicion de documentos de identidad o datos sensibles del titular a usuarios sin necesidad de verlos | Seguridad y privacidad | Acceso a los adjuntos de identidad restringido a Responsable ARCO-POL y Delegado/Responsable interno; todo acceso de lectura queda registrado (seccion O) |
| Solicitud anonima o sin firma que compromete la verificacion de identidad y abre la puerta a suplantacion | Seguridad y privacidad | Verificacion minima configurable por canal (anti-feature 20); ninguna solicitud se admite sin al menos un mecanismo de verificacion aplicado, con advertencia visible cuando la verificacion no fue completa |
| Solicitudes masivas o presuntamente abusivas saturan al Responsable ARCO-POL o se usan para extraer informacion sensible de forma fraudulenta | Operativo, seguridad | Deteccion de patron con alerta (no bloqueo automatico, porque no hay causal legal de "abuso" en el Art. 10); el Delegado decide con criterio humano en cada caso |
| Confundir el reclamo del titular ante la Direccion de Proteccion de Datos (Art. 33 inc. 4 Lineamientos DPO) con una reapertura que modifica la resolucion original | Legal | El workflow separa explicitamente "Cerrada" de "Reclamo ante la ACE" como sub-registro que no altera la resolucion original (seccion F.2) |
| Enviar en nombre de la empresa el informe de actuaciones a la ACE sin autorizacion humana | Legal | El sistema prepara el borrador; el envio real queda fuera del sistema y requiere autorizacion expresa de la empresa (anti-feature 13) |
| Vencimiento de un plazo por falta de asignacion del expediente a un responsable | Operativo | Alerta CRITICAL desde el primer dia sin asignacion (seccion I) |
| Perdida de integridad del expediente al exportarlo para una auditoria o para la ACE | Seguridad | Todo paquete exportado incluye verificacion de integridad (hash o firma), a traves de MOD-019 (decision 2.7.24) |

---

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Formulario interno seguro con los 7 elementos del Art. 18 | X | | | | Obligacion OBLIGATORIO con plazo transitorio ya vencido (OBL-ARCO-08, OBL-PLAZO-04) |
| Carga directa de los 7 formularios oficiales ARCO-POL de la ACE | X | | | | OBL-ARCO-15, obligacion OBLIGATORIO sin excepcion |
| Verificacion de identidad para los 3 tipos de solicitante (titular, representante, heredero) | X | | | | OBL-ARCO-01, base de legitimacion de todo el modulo |
| Sub-flujo de titular NNA (consentimiento parental, aviso de tension normativa) | X | | | | Riesgo de infraccion muy grave si se omite (OBL-CONS-06, Art. 56 lit. c num. 3) |
| Prevencion unica con archivo automatico | X | | | | OBL-ARCO-08, obligacion OBLIGATORIO |
| Plazo general 20+20 dias habiles con una sola prorroga | X | | | | OBL-ARCO-10, plazo maestro del modulo |
| Rama de incompetencia (5 dias habiles) | X | | | | OBL-ARCO-09; inconsistencia 12 del maestro corregida por decision 2.7.10 |
| Rama de notificacion a receptores (5 dias habiles), con fallback manual si MOD-010 aun no esta completo | X | | | | OBL-ARCO-11; funciona con cobertura parcial si MOD-010 (SHOULD HAVE) no esta disponible |
| Bloqueo cautelar durante rectificacion | X | | | | OBL-ARCO-03, exigencia expresa del Art. 9 |
| Denegatoria motivada con las 8 causales tasadas y notificacion en 3 dias habiles | X | | | | OBL-ARCO-12, riesgo de infraccion muy grave (26 a 40 salarios minimos) |
| Gratuidad y tabla de costos de reproduccion publicados | X | | | | OBL-ARCO-13, riesgo de infraccion leve pero facil de evitar desde el MVP |
| Informe de acceso sin datos de terceros | X | | | | OBL-ARCO-02, control automatico de filtrado |
| Portabilidad condicionada (verificacion de base + automatizacion) | X | | | | OBL-ARCO-07 es CONDICIONAL pero de uso bajo; se incluye igual porque forma parte del mismo formulario unico de intake, sin costo adicional relevante de construir el modulo por separado |
| Motor de plazos compartido (consulta a MOD-023) | X | | | | Condicion estructural para que todo el modulo funcione |
| Doble estado 659: aprobador por defecto segun MOD-002/MOD-024 | X | | | | Es uno de los cinco OBL-ARCO afectados; sin esto el modulo quedaria inconsistente el dia que el estado cambie |
| Evidencia con verificacion de integridad exportable | X | | | | Decision 2.7.24, anti-feature 25 |
| Reclamo del titular ante la Direccion de Proteccion de Datos (registro + informe de actuaciones) | | X | | | OBL-ARCO-14 es CONDICIONAL y de baja frecuencia esperada; el registro basico (fecha, contenido) puede ir en MVP minimo, pero el flujo completo de preparacion de informe con plantilla dedicada puede madurar en V1 sin dejar un vacio legal (el sistema igual permite anotar el reclamo como texto libre desde el primer dia) |
| Deteccion automatica de solicitudes potencialmente masivas o abusivas | | | X | | No hay obligacion legal que lo exija; mejora operativa que reduce carga del Responsable ARCO-POL |
| Deteccion automatica de solicitudes duplicadas | | | X | | Mejora operativa sin respaldo legal directo |
| Portal publico con autoregistro del titular (consulta de estado autenticada por el propio titular) | | | | X | Pertenece a MOD-012 (SHOULD HAVE en si mismo), decision 2.7.30; el MVP de ARCO-POL ya cumple la obligacion legal sin el |
| Integraciones de sincronizacion automatica de la lista de supresion de marketing con sistemas externos del cliente (CRM, plataformas de envio de correo) | | | X | | Mejora de integracion sin obligacion legal especifica en la LPDP; la obligacion se cumple con el registro interno |
| Omnicanalidad automatizada (bot de WhatsApp, IVR telefonico) para recibir solicitudes | | | | X | El MVP cumple con canales manuales (correo, presencial, WhatsApp transcrito); la automatizacion de canal es mejora de producto, no obligacion legal |

**Version minima vendible.** La version minima de este modulo que ya puede venderse a una empresa salvadorena incluye: el formulario interno seguro con los 7 elementos del Art. 18 y aceptacion de los formularios oficiales ACE; verificacion de identidad para los 3 tipos de solicitante; las tres ramas completas (incompetencia, notificacion a receptores, denegatoria motivada); el plazo maestro de 20+20 dias con prorroga unica; la prevencion unica con archivo automatico; el bloqueo cautelar de rectificacion; la gratuidad con tabla de costos publicada; el informe de acceso filtrado; y la evidencia exportable con verificacion de integridad. Esta version ya cierra el vacio de plazo transitorio vencido (OBL-PLAZO-04, 23-may-2025) y cubre el nucleo de obligaciones OBLIGATORIO del modulo (OBL-ARCO-02, 03, 08, 09, 10, 12, 13, 15) mas las CONDICIONAL de mayor frecuencia esperada (04, 05, 06, 07, 11). El registro basico del reclamo ante la ACE (OBL-ARCO-14) puede entrar como texto libre desde el MVP sin retrasar el lanzamiento, dejando su plantilla dedicada para V1.

---

## R. Ayuda contextual

**1. Que es una solicitud ARCO-POL**
- Que es: es un pedido formal que una persona (el titular de los datos, o alguien que la representa legalmente) le hace a su empresa para ejercer uno de siete derechos sobre su informacion personal: acceder a ella, corregirla, eliminarla, oponerse a su uso, llevarsela a otra empresa, limitar su uso, o pedir que se olvide de datos publicados en internet.
- Por que tengo que hacer esto: porque la ley le da a toda persona estos siete derechos sobre su propia informacion, y su empresa tiene la obligacion de atenderlos dentro de plazos especificos.
- Fundamento: Art. 4 lit. i y Arts. 6 a 14 de la Ley para la Proteccion de Datos Personales (Decreto Legislativo 144); OBL-ARCO-01 a OBL-ARCO-07.
- Cuando necesito ayuda juridica: cuando la solicitud es ambigua sobre que derecho exactamente se esta ejerciendo, cuando involucra datos de un menor de edad, cuando hay varios titulares mezclados en la misma informacion, o cuando la empresa considera que corresponde denegar la solicitud.

**2. Que es la prevencion**
- Que es: es un aviso unico que se le envia al titular cuando su solicitud llego incompleta, para que en 10 dias habiles complete la informacion o los documentos que faltan.
- Por que tengo que hacer esto: la ley exige dar esta oportunidad antes de poder rechazar o dejar de tramitar una solicitud incompleta; si el titular no completa la informacion en ese plazo, la solicitud se archiva automaticamente sin mas tramite.
- Fundamento: Art. 18 inciso final de la LPDP; OBL-ARCO-08.
- Cuando necesito ayuda juridica: si tiene dudas sobre si un elemento realmente falta o si ya esta cubierto de otra forma en la solicitud.

**3. Que es el bloqueo cautelar**
- Que es: es una medida temporal que se aplica al dato que esta siendo corregido, para que mientras se verifica el cambio, ese dato no se use de forma normal y quede marcado como "en revision".
- Por que tengo que hacer esto: la ley lo exige especificamente para las solicitudes de rectificacion, como proteccion al titular mientras dura el analisis.
- Fundamento: Art. 9 de la LPDP; OBL-ARCO-03.
- Cuando necesito ayuda juridica: si el dato bloqueado se usa en un proceso critico del negocio (por ejemplo, un contrato en curso) y no esta claro como manejar esa excepcion sin incumplir el bloqueo.

**4. Que es la denegatoria motivada**
- Que es: es la decision formal de rechazar, total o parcialmente, una solicitud ARCO-POL, explicando por escrito la razon legal exacta (de una lista cerrada de ocho razones posibles) y aportando las pruebas que la respaldan.
- Por que tengo que hacer esto: la ley no permite negar una solicitud sin explicar el motivo exacto; hacerlo sin motivacion, o inventar una razon fuera de la lista permitida, es una infraccion muy grave.
- Fundamento: Art. 22 de la LPDP; OBL-ARCO-12.
- Cuando necesito ayuda juridica: siempre que este por denegar una solicitud, especialmente si involucra datos sensibles o si el titular ya presento un reclamo antes.

**5. Que es la notificacion a receptores**
- Que es: cuando se corrige, elimina o retira informacion de un titular, y esa informacion ya habia sido compartida antes con otra empresa (un proveedor, un socio comercial), hay que avisarle a esa otra empresa del cambio.
- Por que tengo que hacer esto: para que la correccion o eliminacion sea efectiva de verdad, no solo dentro de su empresa, y la otra empresa tambien actualice su copia del dato.
- Fundamento: Art. 21 inciso 3 de la LPDP; OBL-ARCO-11.
- Cuando necesito ayuda juridica: si no esta claro si un proveedor externo (por ejemplo, un servicio de nube) cuenta como "receptor" a quien avisar, o simplemente como alguien que procesa el dato en su nombre.

**6. Que es el reclamo ante la Agencia de Ciberseguridad del Estado (ACE)**
- Que es: si el titular no esta de acuerdo con la resolucion que su empresa dio a su solicitud, puede presentar un escrito ante la Direccion de Proteccion de Datos Personales de la ACE, dentro de los 10 dias habiles siguientes a que se le notifico la respuesta; cuando eso pasa, la ACE puede pedirle a la empresa un informe de lo actuado.
- Por que tengo que hacer esto: porque la empresa esta obligada a atender ese requerimiento de la autoridad y demostrar que actuo correctamente en el expediente.
- Fundamento: Art. 33 inciso 4 de los Lineamientos para el Delegado de Proteccion de Datos Personales (ACE); OBL-ARCO-14.
- Cuando necesito ayuda juridica: en cuanto se registra un reclamo, conviene que Legal o un asesor externo revise el informe de actuaciones antes de que la empresa lo remita a la ACE.

---

## Doble estado de la reforma 659: efecto especifico sobre este modulo

Bajo el **estado ACTUAL (vigente hoy)**: los Arts. 15 y 17 LPDP obligan a que exista un Delegado de Proteccion de Datos, y los articulos operativos de ARCO-POL (18, 19, 21, 30) atribuyen literalmente la prevencion, la declaracion de incompetencia, la notificacion a receptores y la revocacion del consentimiento a esa figura. En este modulo, el aprobador por defecto de todo acto de ese tipo es la persona con el rol Delegado, tomado de MOD-002.

Bajo el **estado FUTURO (activable solo cuando el Centro Regulatorio, MOD-024, confirme la publicacion oficial de la reforma y transcurra la vacatio legis de 8 dias)**: segun fuentes secundarias, el Delegado dejaria de ser obligatorio en el sector privado y esas mismas funciones pasarian a un rol interno configurable ("sujeto obligado" / Responsable interno), designado por la empresa sin necesidad de certificacion ante la ACE. Las solicitudes ARCO-POL se presentarian directamente ante la empresa. Segun las mismas fuentes secundarias, los seis plazos legales de este modulo (10, 5, 20+20, 5, 3 y 10 dias habiles) no cambiarian.

Las 5 obligaciones de este modulo marcadas como afectadas por la reforma en `mapa_modulos.json` son OBL-ARCO-01, OBL-ARCO-08, OBL-ARCO-10, OBL-ARCO-11 y OBL-ARCO-14: no porque su contenido legal cambie, sino porque la resolucion y aprobacion de los casos dependen de quien ocupe, en cada momento, el rol vigente en MOD-002. Ningun expediente cambia retroactivamente de regla al activarse el estado FUTURO: cada expediente conserva en su historial la regla que estaba vigente cuando se tramito (decision 2.7.16 de `02_validacion_de_la_idea.md`). Toda referencia al numero y contenido exacto de esta reforma debe citarse siempre como "Decreto Legislativo 659, segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado" (decision 2.7.32), incluyendo dentro de los textos de ayuda de este mismo modulo.

---

## Notas finales (desacuerdos o precisiones respecto al mapa)

1. **Posible ajuste de direccion en `depende_de`/`alimenta_a` respecto a MOD-009 y MOD-010.** El mapa (`mapa_modulos.json`) declara que MOD-011 `alimenta_a` MOD-009 y MOD-010 (es decir, MOD-011 entrega datos a Proveedores y a Transferencias), pero no declara la relacion inversa. Sin embargo, la propia tabla de obligaciones colaboradoras de `06_mapa_definitivo_de_modulos.md` (lineas correspondientes a OBL-ARCO-05 y OBL-ARCO-11) y la implicacion funcional documentada en `03_hallazgos_regulatorios.md` ("El modulo de solicitudes debe cruzar con el registro de transferencias/receptores para generar automaticamente la lista de notificaciones pendientes") dejan claro que MOD-011 tambien necesita LEER el catalogo de receptores/encargados de MOD-009 y el registro de transferencias de MOD-010 para construir esa lista (seccion G.5 de esta ficha). Esta ficha documenta esa lectura como "consulta de referencia" en la seccion L.2, siguiendo la misma convencion que ya usa el mapa para MOD-001/MOD-023/MOD-024 (seccion 6.1 del documento maestro de mapeo), pero senala que valdria la pena que una futura revision de `mapa_modulos.json` agregue explicitamente MOD-011 a la lista `alimenta_a` de MOD-009 y de MOD-010 (o, alternativamente, agregue MOD-009 y MOD-010 al `depende_de` de MOD-011), para que el grafo de dependencias documente tambien este sentido de la relacion y no solo el opuesto.
2. **Portabilidad (OBL-ARCO-07) clasificada MUST HAVE pese a ser CONDICIONAL y de baja frecuencia esperada.** Esta ficha decidio incluirla en el MUST HAVE del MVP (seccion Q) porque comparte el mismo formulario de intake, el mismo motor de plazos y el mismo flujo de aprobacion que los demas derechos, sin costo adicional relevante de construirla por separado; se deja constancia de que, si en una revision posterior del mapa se prefiere tratarla como SHOULD HAVE por su baja frecuencia esperada, no habria vacio legal grave en diferirla, ya que sigue siendo CONDICIONAL segun la propia matriz de obligaciones.
3. **Sin desacuerdos de fondo con el resto de `06_mapa_definitivo_de_modulos.md`, `mapa_modulos.json` ni `02_validacion_de_la_idea.md`.** El resto del contenido de esta ficha (proposito, submodulos, obligaciones propietarias y colaboradoras, clasificacion MVP MUST HAVE, dependencias `depende_de`/`alimenta_a` declaradas, y notas de la reforma 659) sigue exactamente lo ya decidido en esas fuentes, sin contradecirlas.
