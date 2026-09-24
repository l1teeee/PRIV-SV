# MODULO: Transferencias Internacionales

Codigo corto del modulo: MOD-010
Clasificacion global del modulo: SHOULD HAVE (para el MVP; ver mapa_modulos.json y 06_mapa_definitivo_de_modulos.md, seccion 3)
Obligaciones que cubre:
- Propietarias: OBL-TRANSF-01, OBL-TRANSF-02, OBL-TRANSF-03, OBL-TRANSF-04, OBL-TRANSF-05, OBL-TRANSF-06 (matriz_obligaciones.json, area Transferencias, 6 obligaciones).
- Colaboradoras (el modulo consume o alimenta, no es propietario): OBL-ARCO-05 (oposicion, incluye marketing directo, propietario MOD-011), OBL-ARCO-11 (notificacion a receptores tras rectificacion o eliminacion, propietario MOD-011), OBL-SEG-04 (medidas de seguridad especificas para transferencias, propietario MOD-015).

Nota de correlacion de IDs: `01_legal/03_hallazgos_regulatorios.md` seccion 4.9 numera 8 obligaciones (OBL-TRANSF-01 a 08) para esta misma area, pero esta ficha usa exclusivamente la numeracion canonica de `matriz_obligaciones.json` (6 obligaciones), que es la que exige seguir la instruccion de agentes. La tabla de equivalencia esta en `03_hallazgos_regulatorios.md`, seccion 11.9: OBL-TRANSF-07 (hallazgos) = OBL-TRANSF-06 (matriz, carga de la prueba); OBL-TRANSF-08 (hallazgos, medidas tecnicas) quedo fusionado dentro de OBL-SEG-04 (matriz, propietario MOD-015).

---

## A. Proposito

- **Por que existe.** Cuando una empresa salvadorena envia datos personales a otra empresa, a un proveedor o a un pais distinto de El Salvador, la ley le exige varias cosas a la vez (consentimiento, informacion al titular, identificacion del receptor, evaluacion del pais destino, contrato con el receptor y aviso a la autoridad). Sin un lugar unico donde registrar todo esto, cada area de la empresa (TI, Marketing, RRHH) contrata herramientas o proveedores extranjeros sin darse cuenta de que esta activando estas obligaciones. Este modulo existe para que cada flujo de datos hacia otro responsable (dentro o fuera de El Salvador) quede identificado, documentado y vigilado en un solo lugar, y para detectar los que nadie registro.
- **Que problema resuelve para la empresa.** Evita el escenario mas comun en pymes y empresas medianas: contratar un servicio cloud, un CRM o una herramienta de RRHH con sede en el extranjero (o simplemente con datos alojados fuera de El Salvador) sin documentar que eso constituye, segun la lectura conservadora recomendada por el analisis juridico, un flujo transfronterizo de datos personales sujeto a los Arts. 44 y 45 de la LPDP.
- **Que obligacion u obligaciones cubre.**
  - OBL-TRANSF-01 (Art. 40): consentimiento previo, informacion de la finalidad e identificacion del cesionario en toda transferencia de datos a otro responsable.
  - OBL-TRANSF-02 (Art. 41): contrato con el responsable receptor, con al menos las mismas obligaciones que tiene el transferente.
  - OBL-TRANSF-03 (Art. 44 inc. 1): nivel de proteccion exigido al pais receptor en transferencias internacionales.
  - OBL-TRANSF-04 (Art. 44 inc. final): consentimiento previo especifico para la transferencia internacional, salvo excepcion por instrumento internacional reciproco.
  - OBL-TRANSF-05 (Art. 45): puesta en conocimiento de la ACE de todo flujo transfronterizo.
  - OBL-TRANSF-06 (Art. 54 inc. 2): la carga de la prueba de que la transferencia se realizo conforme a la ley recae en el responsable.
- **Que valor aporta.**
  - Operativo: un solo lugar donde ver todos los flujos de datos hacia otro responsable, en vez de que la informacion viva dispersa en contratos de proveedores y correos sueltos.
  - Probatorio: ante una fiscalizacion de la ACE o un litigio, la empresa puede mostrar, transferencia por transferencia, que consentimiento tuvo, que contrato firmo y que evaluacion hizo del pais destino (responde directamente a OBL-TRANSF-06).
  - De reduccion de riesgo: detecta transferencias que nadie documento (por ejemplo, un proveedor de nomina con servidores en otro pais que se dio de alta en Proveedores sin pasar por este modulo), antes de que se conviertan en un hallazgo de auditoria o en una infraccion muy grave (Art. 56 lit. c num. 5 y 6).
- **Que NO hace este modulo (limites explicitos).**
  - No decide si un pais tiene "nivel de proteccion adecuado" bajo el Art. 44: ningun organo esta facultado por la ley para calificarlo y la ACE no ha publicado lista ni criterios (incertidumbre 11 de `03_hallazgos_regulatorios.md`, seccion 9; anti-feature 18). El modulo ofrece un cuestionario de factores de riesgo y deja la conclusion marcada como pendiente de validacion.
  - No presenta ni tramita ante la ACE la puesta en conocimiento del flujo transfronterizo en nombre de la empresa sin que esta lo autorice y ejecute; prepara el contenido y dispara el tramite dentro de MOD-024 (Tramites ante la ACE), pero el envio final por el canal oficial (a la fecha, no habilitado por la ACE) es un acto de la empresa (anti-feature 13).
  - No copia ni centraliza los datos personales de los titulares afectados por la transferencia: registra metadatos (que categorias de datos, que tratamiento, que proveedor, que pais), nunca el dato personal en si (ver seccion D, minimizacion).
  - No decide si un encargado extranjero (por ejemplo, un proveedor cloud) debe tratarse como "transferencia" o como simple "acceso del encargado a los datos" (incertidumbre 10 de `03_hallazgos_regulatorios.md`, seccion 9, Art. 4 lit. u frente a Arts. 44-45): aplica por defecto el criterio conservador acordado en la validacion (tratarlo como flujo transfronterizo, decision 2.7.9 de `02_validacion_de_la_idea.md`) y lo marca siempre como pendiente de confirmar por la organizacion.
  - No sustituye el contrato de transferencia ni la firma de las personas facultadas de la empresa; genera el borrador y dejar el resto a la organizacion (anti-feature 17).
  - No es el registro de proveedores ni de contratos: esos viven en MOD-009 y se referencian aqui, nunca se duplican (decision 2.7.2 de `02_validacion_de_la_idea.md`).

## B. Usuarios

Se usan los 12 roles estandar de `05_tipos_de_usuario.md`, seccion 5.3.

| Rol | Para que usa este modulo |
|---|---|
| Administrador de la organizacion | Configura el catalogo de paises, los umbrales de revision periodica y quien recibe las alertas por defecto de este modulo; normalmente no opera transferencias una por una. |
| Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | Revisa y aprueba, hoy, cada acto atribuido legalmente a esa figura dentro del ciclo de una transferencia (ver seccion G): la puesta en conocimiento a la ACE y la clasificacion de una transferencia detectada automaticamente. Recibe el resumen de transferencias activas para su informe periodico (OBL-DPO-07, MOD-002). |
| Responsable ARCO-POL / Responsable del tramite | Consulta este modulo cuando una solicitud de rectificacion, cancelacion o eliminacion involucra datos que ya fueron transferidos, para completar la notificacion a receptores dentro de los 5 dias habiles (OBL-ARCO-11, colaboradora). |
| Responsable Legal / Compliance | Usuario principal del modulo: registra o revisa la base juridica de cada transferencia, completa el cuestionario de evaluacion del pais receptor, decide si documenta la excepcion de integracion centroamericana y redacta o revisa el contrato de transferencia junto con MOD-009. |
| Responsable de Seguridad / IT | Registra o confirma las salvaguardas tecnicas (cifrado en transito, protocolos seguros) que alimentan la evidencia de OBL-SEG-04 (colaboradora, propietario MOD-015), y suele ser quien da de alta el proveedor extranjero en MOD-009 que dispara la deteccion automatica de este modulo. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Quien contrata o usa el servicio con destino extranjero (por ejemplo, Marketing con una plataforma de envio de correos alojada fuera de El Salvador); recibe la tarea automatica cuando su area genera una transferencia detectada y aporta el detalle de finalidad y categorias de datos. |
| Aprobador | Aprueba el paso de una transferencia a estado ACTIVA cuando la evaluacion de pais o la base juridica generan una nota de riesgo, y aprueba antes de que se envie la puesta en conocimiento a la ACE. |
| Auditor (interno) | Solo lectura sobre el listado completo de transferencias y su expediente de evidencia, para la auditoria anual de cumplimiento (OBL-AUD-01). |
| Auditor externo (invitado) | Acceso temporal de solo lectura, tipicamente durante la semana de una auditoria, al paquete de evidencia exportado de este modulo. |
| Usuario de consulta / Colaborador | Ve y completa unicamente la tarea puntual que se le asigno (por ejemplo, "confirma si el proveedor X aloja datos fuera de El Salvador"), sin ver el resto del modulo. |
| Titular (formulario externo) | No usa este modulo de forma directa. Puede recibir, de forma indirecta, informacion sobre transferencias en el aviso de privacidad (MOD-008) o en la respuesta a una solicitud de acceso (MOD-011), que puede citar el registro de este modulo como fuente. |
| Asesor externo invitado | Acceso puntual y acotado a una transferencia concreta cuando el caso es juridicamente dudoso (por ejemplo, si aplica la excepcion centroamericana o si un encargado extranjero cuenta como transferencia), para dejar su opinion registrada como evidencia. |

## C. Permisos

| Accion | Administrador | Delegado / Responsable interno | Resp. ARCO-POL | Legal / Compliance | Seguridad / IT | Responsable de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Titular | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver listado y expediente | Si | Si | Si (solo transferencias vinculadas a un ARCO-POL) | Si | Si | Solo las de su area | Si | Si (solo lectura) | Si, temporal (solo lectura) | No | No | Solo el caso asignado |
| Crear transferencia (manual) | No | Si | No | Si | Si (registro tecnico) | Si (borrador) | No | No | No | No | No | No |
| Modificar campos | No | Si | No | Si | Solo campos tecnicos | Solo su borrador antes de enviarlo a revision | No | No | No | No | No | No |
| Confirmar o descartar una transferencia detectada automaticamente | No | Si | No | Si | No | No (solo aporta informacion) | No | No | No | No | No | No |
| Aprobar paso a ACTIVA | No | No (ejecuta, no aprueba lo que el mismo redacto salvo pyme, ver nota) | No | No (mismo motivo) | No | No | Si | No | No | No | No | No |
| Aprobar y enviar puesta en conocimiento a la ACE (via MOD-024) | Si (ver nota) | No (genera y revisa el borrador del ACEFiling, pero la aprobacion y el envio se rigen por la cadena de MOD-024) | No | Si | No | No | Si, doble control en empresa mediana/corporativo | No | No | No | No | No |
| Cerrar o suspender transferencia | No | Si | No | Si | No | No | Si | No | No | No | No | No |
| Eliminar / archivar | No | Si (archivar, nunca eliminar el historial) | No | No | No | No | No | No | No | No | No | No |
| Exportar paquete de evidencia | Si | Si | No | Si | No | No | No | Si | Si (solo el paquete compartido con ella) | No | No | No |
| Asignar tarea | Si | Si | No | Si | No | No | No | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | No (solo lectura) | No | Si, sobre su tarea | No | Si |
| Adjuntar evidencia | Si | Si | No | Si | Si | Si, sobre su tarea | No | No | No | Si, sobre su tarea | No | Si |

**Separacion de funciones.** Quien crea o redacta una transferencia (Legal/Compliance o el Delegado) no deberia ser la unica persona que la aprueba para pasar a ACTIVA ni para autorizar el envio de la puesta en conocimiento a la ACE; esa aprobacion recae en el rol Aprobador. En pyme, donde Administrador, Delegado y Aprobador suelen acumularse en la misma persona (ver `05_tipos_de_usuario.md`, seccion 5.4), el sistema permite la acumulacion pero muestra siempre la advertencia visible de autorrevision. A partir del umbral configurable de tamano de empresa, el sistema bloquea que la misma persona redacte y apruebe la misma transferencia. El rol Auditor (interno o externo) es siempre de solo lectura y nunca coincide con quien carga evidencia o aprueba una accion en este modulo.

## D. Informacion de entrada

Los campos marcados "referencia" no duplican datos: guardan el identificador de un registro que vive en otro modulo (principio de minimizacion, ver nota final de esta seccion).

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Nombre o identificador de la transferencia | Texto | Obligatorio desde BORRADOR | Libre, con sugerencia automatica "Tratamiento + Receptor" | Minimo 5 caracteres | "Un nombre corto que le ayude a reconocer esta transferencia despues, por ejemplo: Nomina - proveedor de planillas en Guatemala." | Buena practica |
| Tratamiento de origen | Referencia a Treatment (MOD-006, RAT) | Obligatorio desde BORRADOR | Lista de tratamientos ya registrados en el RAT de la empresa | Debe existir en el RAT activo | "Elija de que actividad de tratamiento salen los datos que se van a transferir. Si no aparece en la lista, primero debe registrarla en el Registro de Actividades de Tratamiento." | OBL-DOC-02 (MOD-006), consistencia con OBL-TRANSF-01 |
| Tipo de transferencia | Seleccion unica | Obligatorio desde BORRADOR | Nacional a otro responsable / Internacional / Pendiente de confirmar (valor de sistema, no seleccionable manualmente) | - | "Nacional: el receptor esta en El Salvador. Internacional: el receptor esta fuera de El Salvador, o los datos se alojaran fuera del pais aunque el receptor tenga oficina local." | OBL-TRANSF-01 (Art. 40, aplica a toda transferencia) y OBL-TRANSF-03/04 (Art. 44, solo si es internacional) |
| Receptor | Referencia a Encargado, Tercero/Receptor o Subencargado (MOD-009) | Obligatorio desde BORRADOR | Lista de entidades ya registradas en Proveedores y Encargados | Debe existir en MOD-009; si no existe, el sistema ofrece crearlo alli primero | "Elija a quien le va a enviar los datos. Si es la primera vez que trabaja con esta empresa, debe registrarla primero en Proveedores." | OBL-TRANSF-01 (identificacion del cesionario) |
| Rol del receptor | Seleccion unica (heredado de MOD-009, solo lectura aqui) | Se calcula automaticamente al elegir el receptor | Encargado del tratamiento / Responsable independiente (tercero o receptor) / Subencargado | - | "Este dato viene de como registro a este proveedor en el modulo de Proveedores. Si el receptor procesa los datos siguiendo sus instrucciones, es un encargado; si decide por su cuenta que hacer con los datos, es un responsable independiente." | Distincion relevante para Art. 40/41 frente a Arts. 33-36 (encargados) |
| Pais o paises de destino | Seleccion multiple sobre catalogo de paises | Obligatorio desde BORRADOR | Catalogo de paises (ISO), sin marcar ninguno como "adecuado" por el sistema | Debe incluir El Salvador solo si el tipo es Nacional | "Indique en que pais o paises quedaran los datos, no solo donde tiene su sede el proveedor. Por ejemplo, un proveedor con oficina en El Salvador puede alojar los datos en servidores en otro pais." | OBL-TRANSF-03 (Art. 44 inc. 1) |
| Categorias de datos transferidas | Seleccion multiple, referencia al catalogo de DataCategory (MOD-006) | Obligatorio desde BORRADOR | Catalogo compartido de categorias de datos (incluye marcado de sensibilidad heredado del RAT) | Al menos una categoria | "Elija que tipos de datos personales se envian (por ejemplo: datos de contacto, datos de nomina, datos biometricos). No describa aqui los datos de una persona en concreto, solo el tipo de dato." | OBL-TRANSF-01, minimizacion (instruccion 8 de la tarea) |
| Finalidad de la transferencia | Texto largo | Obligatorio desde BORRADOR | - | Minimo 20 caracteres, precargado desde la finalidad del tratamiento de origen si existe | "Explique en una frase para que se envian estos datos, por ejemplo: procesar la planilla mensual de sueldos." | OBL-TRANSF-01 (informacion de la finalidad) |
| Base juridica de la transferencia | Seleccion unica | Obligatorio antes de pasar a EN_EVALUACION_DE_PAIS o PENDIENTE_DE_APROBACION | Consentimiento previo del titular / Excepcion por instrumento internacional reciproco (Integracion Economica Centroamericana) / Otra base registrada en el tratamiento de origen (ver nota de riesgo) | Si el tipo es Internacional y la base no es "Consentimiento previo" ni la excepcion centroamericana, el sistema muestra nota de riesgo obligatoria de leer antes de continuar | "La ley exige, por regla general, el consentimiento especifico del titular para transferir sus datos a otro pais. Solo hay una excepcion expresa (tratados de integracion centroamericana) y no esta desarrollada en ningun reglamento todavia." | OBL-TRANSF-04 (Art. 44 inciso final y 4) |
| Evidencia de consentimiento especifico | Referencia a Consent (MOD-007) | Obligatorio si la base elegida es "Consentimiento previo" | Lista de consentimientos ya registrados para el titular o el tratamiento correspondiente | Debe existir y estar vigente (no revocado) | "Vincule aqui el registro de consentimiento que cubre especificamente esta transferencia, no un consentimiento general del tratamiento." | OBL-TRANSF-04 |
| Evaluacion del nivel de proteccion del pais receptor | Cuestionario de factores (seleccion multiple + texto) mas archivo adjunto opcional | Obligatorio si el tipo es Internacional, antes de pasar a PENDIENTE_DE_APROBACION | Catalogo de factores (por ejemplo: existencia de ley de proteccion de datos en el pais destino, existencia de autoridad de control, certificaciones del proveedor, clausulas contractuales adicionales) | Al menos un factor documentado | "Esta lista de preguntas le ayuda a reunir informacion sobre el pais destino. El sistema no decide si el pais es adecuado; esa conclusion la debe tomar su organizacion, con apoyo de asesoria legal si el caso es dudoso." | OBL-TRANSF-03; anti-feature 18 (el sistema no califica el nivel de proteccion) |
| Salvaguardas tecnicas y contractuales | Seleccion multiple | Recomendado desde BORRADOR, obligatorio antes de ACTIVA | Cifrado en transito (SSL/TLS) / Contrato de confidencialidad / Clausulas contractuales de transferencia / Certificacion del proveedor / Otra (especificar) | Al menos una salvaguarda marcada antes de ACTIVA | "Marque que medidas de proteccion existen para este envio de datos, por ejemplo si la conexion esta cifrada o si el contrato incluye clausulas de confidencialidad." | OBL-SEG-04 (colaboradora, propietario MOD-015) |
| Contrato de transferencia | Referencia a documento tipo Contrato/DPA (MOD-009 / MOD-008) | Obligatorio antes de ACTIVA | Lista de contratos ya vinculados al receptor en MOD-009, o generar borrador desde plantilla | Debe existir un contrato vigente vinculado al mismo receptor | "Vincule el contrato firmado con este proveedor o genere un borrador a partir de la plantilla si todavia no existe." | OBL-TRANSF-02 (Art. 41) |
| Puesta en conocimiento a la ACE | Referencia a ACEFiling (MOD-024), mas estado de solo lectura en este modulo | Se genera automaticamente al pasar a ACTIVA si el tipo es Internacional | Estados heredados de MOD-024: Borrador / Pendiente de envio / Enviado (sin canal oficial confirmado) / No aplica | - | "El sistema prepara la informacion que la ley pide poner en conocimiento de la ACE. El envio final lo gestiona su organizacion desde el Centro Regulatorio, porque a la fecha la ACE no tiene un canal oficial habilitado para recibir este aviso." | OBL-TRANSF-05 (Art. 45); decision 19 de `02_validacion_de_la_idea.md` |
| Solicitud de opinion previa a la ACE | Booleano + referencia a ACEFiling (MOD-024) | Opcional, siempre | Si / No | - | "Puede pedir, de forma voluntaria, la opinion de la ACE sobre si esta transferencia cumple con la ley. No es obligatorio hacerlo." | OBL-TRANSF-06 (hallazgos 4.9, "puede" no "debe"; RECOMENDADO) |
| Fecha de inicio de la transferencia | Fecha | Obligatorio antes de ACTIVA | - | No puede ser anterior a la fecha de creacion del registro salvo justificacion (transferencia ya existente que se esta regularizando) | "Indique desde cuando se realiza o se realizara este envio de datos." | Buena practica, soporte de OBL-TRANSF-06 |
| Periodicidad de revision | Seleccion unica | Obligatorio antes de ACTIVA | Cada 6 meses / Cada 12 meses / Cada 24 meses, configurable por la empresa | - | "Cada cuanto quiere que el sistema le recuerde revisar si esta transferencia sigue vigente y si las condiciones del pais o del proveedor cambiaron." | Buena practica, apoya OBL-TRANSF-06 (carga de la prueba continua) |
| Estado de la transferencia | Seleccion de sistema (no editable directamente) | Se calcula por el workflow | Ver seccion F | - | - | - |
| Notas de riesgo generadas por el sistema | Texto largo, solo lectura | Se genera automaticamente | - | - | "Estas notas son generadas por el sistema para llamar su atencion sobre un punto que requiere revision; no son una conclusion legal." | Anti-feature 5, 6, 18, 22 |
| Adjuntos de evidencia | Archivo (uno o varios) | Opcional, recomendado antes de ACTIVA | PDF, imagen, correo exportado | Tamano maximo configurable, hash calculado al subir | "Adjunte aqui cualquier documento que respalde esta transferencia: capturas del acuse de envio a la ACE, correos de confirmacion del proveedor, certificaciones." | OBL-TRANSF-06 |

**Campos precargados.** Tratamiento de origen, finalidad y categorias de datos se precargan desde el RAT (MOD-006) cuando el usuario elige el tratamiento. El receptor y su rol (encargado/responsable independiente/subencargado) se precargan desde MOD-009. El pais de destino se sugiere a partir del pais registrado en la ficha del proveedor en MOD-009, editable porque el proveedor puede alojar los datos en un pais distinto al de su sede. Cuando el registro nace por deteccion automatica (ver seccion G), el sistema precarga tratamiento, receptor, rol y pais, y deja el resto en blanco para que el responsable lo complete.

**Minimizacion de datos personales.** Este modulo no almacena datos personales de los titulares afectados por la transferencia: todos los campos son metadatos (categorias, no valores) o referencias a otros registros (tratamiento, proveedor, consentimiento, contrato). El unico dato personal que puede aparecer de forma incidental es informacion de contacto de personas de la empresa receptora (por ejemplo, nombre y correo del responsable de privacidad del proveedor extranjero), que se trata como dato de contacto comercial, no como dato del titular final, y se limita a lo estrictamente necesario para gestionar la relacion contractual. Los adjuntos de evidencia deben evitar incluir datos personales de titulares finales salvo que sea estrictamente necesario (por ejemplo, un correo de confirmacion que por error incluya un fragmento de datos); el texto de ayuda de ese campo advierte de esto.

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Registro de transferencia | Ficha completa con todos los campos de la seccion D y su historial de estados | Registro interno, exportable a PDF | Al crear o confirmar una transferencia | Legal/Compliance, Delegado, Auditor |
| Tarea de confirmacion (transferencia detectada) | "Confirme si esta transferencia hacia [pais] es correcta" | Tarea en MOD-021 | Al detectar automaticamente un proveedor o encargado fuera de El Salvador (ver G) | Responsable de area que dio de alta el proveedor, con copia a Legal |
| Nota de riesgo | Texto de advertencia sobre un punto que requiere revision (base juridica distinta de consentimiento, pais sin evaluar, excepcion centroamericana invocada) | Texto dentro del registro, visible en el listado | Al guardar el registro si se cumple la condicion | Legal/Compliance, Aprobador |
| Borrador de puesta en conocimiento a la ACE | Datos de la transferencia en el formato que MOD-024 usa para tramites salientes | Registro ACEFiling en MOD-024, exportable a PDF | Al pasar la transferencia a ACTIVA, si es internacional | Delegado, Aprobador |
| Entrada en el Centro de Evidencias | Copia de referencia del expediente completo de la transferencia, con hash de cada adjunto | Paquete de evidencia (MOD-019) | Al pasar a ACTIVA y en cada revision periodica cerrada | Auditor, Legal/Compliance |
| Indicador de dashboard | Numero de transferencias por estado, numero de transferencias detectadas sin confirmar, numero de evaluaciones de pais vencidas | Tarjetas y semaforos (MOD-020) | Se recalcula en cada cambio relevante | Gerencia, Responsable, Legal, Auditor (vistas distintas, ver seccion M) |
| Evento de auditoria | Quien hizo que cambio, cuando, sobre que registro | Entrada en AuditLog transversal | En cada creacion, cambio de campo, cambio de estado, aprobacion o exportacion | Auditor, Administrador |
| Reporte de transferencias | Listado filtrable de todas las transferencias con su estado y evidencia asociada | PDF / XLSX | Bajo demanda, o programado mensualmente | Gerencia, Legal, Auditor externo |

## F. Workflow

```
                    (deteccion automatica: proveedor/encargado con pais != El Salvador)
                                        |
                                        v
   [alta manual] ---------------> DETECTADA_PENDIENTE_DE_CONFIRMAR
        |                                |
        |                                | confirmar que es una transferencia real
        v                                v
     BORRADOR  <--------------------------
        |
        | completar campos minimos (D) y guardar
        v
   EN_EVALUACION_DE_PAIS  (solo si Tipo = Internacional; si Tipo = Nacional, se salta este estado)
        |
        | evaluacion de pais documentada + base juridica valida + salvaguardas marcadas
        v
   PENDIENTE_DE_APROBACION
        |
        |-- aprobada por Aprobador -----------------> ACTIVA
        |
        v (rechazada, requiere corregir)
     BORRADOR

   ACTIVA -------- llega fecha de revision periodica --------> EN_REVISION_PERIODICA
     ^                                                                  |
     |                                                                  |
     |------------------ revision confirma que sigue vigente -----------|
     |
     |-- ya no se realiza la transferencia -------------------------> FINALIZADA
     |
     |-- riesgo detectado, se pausa mientras se corrige -------------> SUSPENDIDA
                                                                          |
                                                     se corrige el riesgo |
                                                                          v
                                                                       ACTIVA

   DETECTADA_PENDIENTE_DE_CONFIRMAR -- se determina que no es una transferencia real --> DESCARTADA

   FINALIZADA, DESCARTADA: estados terminales (archivados, nunca se eliminan)
```

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (ninguno) | Se crea un proveedor o encargado en MOD-009 con pais distinto de El Salvador | Automatico, ver seccion G | DETECTADA_PENDIENTE_DE_CONFIRMAR | Sistema | Crea tarea en MOD-021, notificacion en MOD-022, nota de riesgo visible, evento de auditoria |
| (ninguno) | Un usuario da de alta manualmente una transferencia | Ninguna | BORRADOR | Delegado, Legal/Compliance, Seguridad/IT (registro tecnico) | Evento de auditoria de creacion |
| DETECTADA_PENDIENTE_DE_CONFIRMAR | Confirmar que es una transferencia real | El usuario completa al menos tratamiento de origen y finalidad | BORRADOR | Delegado, Legal/Compliance | Evento de auditoria, se conserva el origen "detectada automaticamente" en el historial |
| DETECTADA_PENDIENTE_DE_CONFIRMAR | Descartar (no es una transferencia real, por ejemplo el proveedor no trata datos personales) | El usuario debe registrar un motivo | DESCARTADA | Delegado, Legal/Compliance | Evento de auditoria con el motivo; el registro queda archivado, consultable, nunca se borra |
| BORRADOR | Guardar con campos minimos completos, tipo = Nacional | Receptor, categorias, finalidad y contrato completos | PENDIENTE_DE_APROBACION | Legal/Compliance, Delegado | Evento de auditoria |
| BORRADOR | Guardar con campos minimos completos, tipo = Internacional | Receptor, categorias, finalidad completos | EN_EVALUACION_DE_PAIS | Legal/Compliance, Delegado | Evento de auditoria, tarea de "completar evaluacion de pais" si queda pendiente |
| EN_EVALUACION_DE_PAIS | Completar evaluacion de pais, base juridica y salvaguardas | Evaluacion con al menos un factor documentado; si la base no es consentimiento ni excepcion centroamericana, se debe reconocer expresamente la nota de riesgo | PENDIENTE_DE_APROBACION | Legal/Compliance, Delegado | Genera borrador de puesta en conocimiento a la ACE en MOD-024 (queda en estado Borrador dentro de ese modulo) |
| PENDIENTE_DE_APROBACION | Aprobar | El aprobador no puede ser la misma persona que redacto el registro, salvo pyme con advertencia visible | ACTIVA | Aprobador | Evento de auditoria con identidad y fecha, entrada en Centro de Evidencias, notificacion al Delegado para su informe periodico |
| PENDIENTE_DE_APROBACION | Rechazar y devolver | El aprobador registra el motivo | BORRADOR | Aprobador | Evento de auditoria, notificacion a quien redacto |
| ACTIVA | Llega la fecha de revision periodica (motor de plazos, MOD-023) | Automatico | EN_REVISION_PERIODICA | Sistema | Tarea de revision en MOD-021, alerta INFO |
| EN_REVISION_PERIODICA | Confirmar que sigue vigente sin cambios | Ninguna adicional | ACTIVA | Legal/Compliance, Delegado | Evento de auditoria, se reinicia el contador de la proxima revision |
| EN_REVISION_PERIODICA | Confirmar que ya no se realiza | Ninguna adicional | FINALIZADA | Legal/Compliance, Delegado, Aprobador | Evento de auditoria, entrada final en Centro de Evidencias, se conserva el expediente completo |
| ACTIVA o EN_REVISION_PERIODICA | Suspender por riesgo detectado (contrato vencido, evaluacion de pais desactualizada, incidente relacionado) | Debe registrarse el motivo | SUSPENDIDA | Delegado, Legal/Compliance, Aprobador | Alerta CRITICAL, notificacion al Responsable de area involucrado, evento de auditoria |
| SUSPENDIDA | Corregir el riesgo y reactivar | Debe registrarse evidencia de la correccion | ACTIVA | Aprobador | Evento de auditoria |
| SUSPENDIDA | No se corrige, se decide terminar la transferencia | Debe registrarse el motivo | FINALIZADA | Aprobador | Evento de auditoria, se conserva el expediente |

**Reapertura y registros vinculados.** Un registro FINALIZADO o DESCARTADO puede reabrirse solo mediante la creacion de un nuevo registro que referencia al anterior como "sustituye a", nunca editando el estado terminal directamente, para no perder la trazabilidad historica (principio 8 de `06_mapa_definitivo_de_modulos.md`). Si el tratamiento de origen (MOD-006) o el receptor (MOD-009) al que apunta una transferencia se elimina o se archiva, la transferencia no se elimina: queda marcada como "huerfana, requiere revision" con una alerta al Delegado y a Legal, y conserva su historial completo.

## G. Automatizaciones

Todas las reglas de esta seccion son configurables por la empresa (activar/desactivar, cambiar destinatario, ajustar periodicidad) desde la configuracion del modulo, salvo donde se indique lo contrario.

| Disparador | Condicion | Accion |
|---|---|---|
| Se crea o edita un proveedor, encargado o tercero/receptor en MOD-009 | El pais registrado para ese receptor es distinto de El Salvador, o se marca "datos alojados fuera de El Salvador" | Crear automaticamente un registro de transferencia en estado DETECTADA_PENDIENTE_DE_CONFIRMAR, con nota de riesgo visible que explica la incertidumbre 10 (encargado extranjero vs. transferencia), crear tarea en MOD-021 asignada al responsable de area que dio de alta el proveedor, con copia a Legal/Compliance |
| El diagnostico inicial (MOD-004) marca "trata datos fuera de El Salvador: si" para algun tratamiento | El tratamiento no tiene todavia ninguna transferencia vinculada | Crear tarea en MOD-021 para registrar la transferencia correspondiente; no crea el registro completo por si solo (el diagnostico solo detecta la senal, ver nota de cobertura parcial en el mapa de modulos) |
| Una transferencia pasa a EN_EVALUACION_DE_PAIS | El tipo es Internacional y la base juridica elegida no es "Consentimiento previo" ni la excepcion centroamericana | Mostrar nota de riesgo obligatoria de reconocer antes de continuar, y marcar el registro con indicador visual de riesgo en el listado |
| Una transferencia pasa a PENDIENTE_DE_APROBACION con tipo Internacional | Siempre | Generar automaticamente el borrador de "puesta en conocimiento a la ACE" en MOD-024 (ACEFiling), precargado con los datos ya registrados |
| Se marca la base juridica como "Consentimiento previo" | No existe ningun registro de Consent (MOD-007) vinculado al titular o al tratamiento | Bloquear el paso a PENDIENTE_DE_APROBACION y crear tarea "capturar consentimiento especifico para esta transferencia" |
| Llega la fecha configurada de revision periodica de una transferencia ACTIVA | Automatico, segun periodicidad elegida en el campo correspondiente (D) | Crear tarea de revision en MOD-021, cambiar estado a EN_REVISION_PERIODICA, enviar alerta INFO |
| El contrato de transferencia vinculado (MOD-009) llega a su fecha de vencimiento | Faltan menos de 30 dias para el vencimiento (umbral configurable) | Alerta WARNING; si vence sin renovar, alerta CRITICAL y bloqueo del paso a ACTIVA para nuevas transferencias con ese mismo receptor |
| Se aprueba una solicitud ARCO-POL de rectificacion, cancelacion, oposicion, portabilidad, olvido o limitacion (MOD-011) sobre un tratamiento que tiene transferencias ACTIVAS vinculadas | Automatico | Crear tarea de "notificar la rectificacion/eliminacion al receptor" con el plazo de 5 dias habiles calculado por MOD-023 (soporta OBL-ARCO-11, colaboradora) |
| Se cierra la puesta en conocimiento a la ACE en MOD-024 como "enviada" | Automatico | Actualizar el estado visible en este modulo, adjuntar la constancia como evidencia del registro |
| La evaluacion de pais de una transferencia ACTIVA supera la antiguedad configurada (por ejemplo, 24 meses) sin actualizarse | Automatico | Alerta WARNING de "evaluacion de pais desactualizada", tarea de revision anticipada |

## H. Decisiones que NO debe automatizar

- **Calificar si el pais receptor tiene "nivel de proteccion adecuado".** La ley (Art. 44) exige que el pais cumpla como minimo los principios de la LPDP, pero no atribuye a ningun organo la facultad de declarar esa adecuacion, y la ACE no ha publicado lista ni criterios (incertidumbre 11, `03_hallazgos_regulatorios.md` seccion 9). El sistema muestra el cuestionario de factores y el texto "Requiere validacion de la organizacion o asesoria especializada" antes de dejar avanzar la transferencia.
- **Decidir si un encargado extranjero (por ejemplo, un proveedor cloud) es una "transferencia" o solo "acceso del encargado".** Es una ambiguedad genuina entre el Art. 4 lit. u (que excluye al encargado de la definicion de transferencia) y los Arts. 44-45 (cuyas definiciones de emisor/receptor si lo incluyen). El sistema aplica el criterio conservador por defecto (tratarlo como flujo transfronterizo) pero lo muestra siempre como una decision pendiente de confirmar, nunca como un hecho cerrado, con el texto de advertencia estandar.
- **Decidir si aplica la excepcion de integracion economica centroamericana (Art. 44 inc. 4).** No existe reglamento o resolucion de COMIECO/SICA/SIECA que la desarrolle para datos personales; el sistema no la activa de forma automatica en ningun caso, exige que un usuario la marque expresamente y muestra la advertencia de que requiere criterio de abogado.
- **Certificar que el contrato de transferencia cumple con "al menos las mismas obligaciones" que tiene el transferente (Art. 41).** El sistema puede ofrecer un checklist de clausulas usuales, pero no puede verificar el contenido juridico real de un contrato cargado como archivo; la conclusion de suficiencia queda a cargo de Legal/Compliance o de un asesor externo.
- **Decidir el contenido, el momento y la forma exactos de "poner en conocimiento" a la ACE (Art. 45 inc. 2).** La ACE no ha habilitado formulario, plataforma ni procedimiento (incertidumbre 12, `03_hallazgos_regulatorios.md` seccion 9); el sistema prepara el contenido y deja constancia del intento, pero no puede inventar un canal ni garantizar que la ACE lo reciba.
- **Aprobar la activacion de una transferencia internacional de datos sensibles.** Dado que la infraccion "transferencia internacional a pais sin nivel de proteccion adecuado" y "transferencia sin consentimiento del titular" estan clasificadas como muy graves (Art. 56, Art. 57), el sistema nunca activa automaticamente una transferencia de esta categoria sin la aprobacion explicita de una persona con el rol Aprobador.

En todos los casos anteriores, el sistema muestra el texto estandar: "Requiere validacion de la organizacion o asesoria especializada."

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia o repeticion | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Transferencia detectada automaticamente sin confirmar | Alta de proveedor/encargado con pais distinto de El Salvador (G) | WARNING | Responsable de area, con copia a Legal/Compliance | Plataforma + correo | Al crearse; recordatorio semanal mientras siga pendiente | A los 15 dias habiles sin confirmar, escala al Delegado | Se confirma como BORRADOR o se DESCARTA |
| Transferencia internacional sin evaluacion de pais completa | Estado EN_EVALUACION_DE_PAIS por mas de 10 dias habiles | HIGH | Legal/Compliance, Delegado | Plataforma + correo | Diaria mientras siga pendiente | A los 20 dias habiles, escala al Administrador de la organizacion | La evaluacion queda registrada |
| Transferencia internacional sin consentimiento especifico vinculado | Base = Consentimiento previo sin registro de Consent enlazado (G) | HIGH | Legal/Compliance, Responsable de area | Plataforma + correo | Al intentar avanzar de estado; recordatorio cada 5 dias habiles | A los 10 dias habiles, escala al Delegado | Se vincula un Consent vigente |
| Base juridica distinta de consentimiento sin excepcion documentada | Nota de riesgo generada en G, sin justificacion adicional adjunta | HIGH | Legal/Compliance, Aprobador | Plataforma | Al guardar; persiste visible mientras la transferencia este activa | No escala automaticamente, requiere cierre manual de la nota | Se adjunta justificacion o se cambia la base |
| Contrato de transferencia proximo a vencer | Faltan menos de 30 dias para el vencimiento del contrato vinculado (MOD-009) | WARNING | Legal/Compliance, Responsable de Seguridad/IT | Plataforma + correo | Unica al cruzar el umbral, luego semanal | A los 7 dias antes del vencimiento sin renovar, escala al Aprobador | Se registra un contrato vigente |
| Contrato de transferencia vencido | Fecha de vencimiento del contrato alcanzada sin renovacion | CRITICAL | Legal/Compliance, Delegado, Aprobador | Plataforma + correo + notificacion push si esta configurada | Diaria mientras siga vencido | Inmediato al Administrador de la organizacion | Se registra un contrato vigente o se suspende la transferencia |
| Puesta en conocimiento a la ACE pendiente de envio | Borrador generado en MOD-024 sin marcar como enviado, 15 dias habiles despues de creado | WARNING | Delegado | Plataforma + correo | Semanal | A los 30 dias habiles, escala al Administrador de la organizacion | Se marca como enviada (o se documenta la imposibilidad por falta de canal, ver seccion H) |
| Revision periodica vencida | Fecha de proxima revision alcanzada sin que el estado pase a EN_REVISION_PERIODICA confirmada | INFO, sube a WARNING a los 15 dias | Legal/Compliance, Delegado | Plataforma | Al vencer, luego semanal | A los 30 dias, escala al Aprobador | Se completa la revision |
| Transferencia con evaluacion de pais desactualizada | Evaluacion de pais con mas de 24 meses (configurable) sin actualizar, en transferencia ACTIVA | WARNING | Legal/Compliance | Plataforma + correo | Mensual mientras siga desactualizada | A los 60 dias, escala al Delegado | Se actualiza la evaluacion |
| Transferencia huerfana (tratamiento o receptor eliminado) | Se elimina o archiva el tratamiento o el receptor vinculado | HIGH | Delegado, Legal/Compliance | Plataforma + correo | Inmediata, luego semanal | A los 10 dias habiles, escala al Administrador de la organizacion | Se revincula a un tratamiento/receptor vigente o se pasa a FINALIZADA |

## J. Evidencia

- **Registro con fecha y hora, usuario y version.** Cada creacion, edicion de campo, cambio de estado, aprobacion o rechazo queda registrado con marca de tiempo, identidad del usuario y version anterior/nueva del campo modificado (historial inmutable, ver seccion O).
- **Archivo adjunto con hash.** Todo documento adjunto (contrato, constancia de puesta en conocimiento a la ACE, capturas de evaluacion de pais) se guarda con un hash calculado al momento de subirlo, para poder verificar despues que no fue alterado.
- **Aprobacion con identidad y fecha.** El paso de PENDIENTE_DE_APROBACION a ACTIVA queda registrado con la identidad de quien aprobo, la fecha y, si existia, la nota de riesgo que reconocio antes de aprobar.
- **Exportacion firmada.** El paquete de evidencia exportado desde este modulo hacia el Centro de Evidencias (MOD-019) incluye un mecanismo de verificacion de integridad (hash o firma validable de forma independiente), conforme al anti-feature 25.
- **Que obligacion prueba cada evidencia.**
  - El registro completo de la transferencia (tratamiento, receptor, pais, base, contrato) prueba OBL-TRANSF-01, OBL-TRANSF-02, OBL-TRANSF-03 y OBL-TRANSF-04.
  - El registro del estado de la puesta en conocimiento a la ACE (borrador, pendiente de envio, enviado, o constancia de la imposibilidad por falta de canal habilitado) prueba el intento de cumplimiento de OBL-TRANSF-05.
  - El expediente completo, con todos sus adjuntos y su historial de cambios, es la evidencia central para sostener la carga de la prueba de OBL-TRANSF-06 (Art. 54 inc. 2) ante una fiscalizacion de la ACE.
  - Las salvaguardas tecnicas marcadas y su documentacion de soporte alimentan la evidencia de OBL-SEG-04 (colaboradora, propietario MOD-015).
- **Tiempo de conservacion.** No existe una regla expresa de retencion para el expediente de transferencias en la LPDP ni en las Politicas ACE. Por analogia con OBL-RET-05 (criterio de retencion del expediente ARCO-POL e incidentes como prueba de descargo, 5 anos minimo recomendado, fundado en el principio de responsabilidad demostrada del Art. 5 lit. i), se recomienda conservar el expediente completo de cada transferencia mientras esta permanezca ACTIVA y, como minimo, 5 anos adicionales despues de pasar a FINALIZADA o DESCARTADA [opinion de producto, sin norma expresa de retencion para este expediente en particular; el periodo exacto debe confirmarse con las reglas globales de retencion documental de MOD-016].

## K. Documentos asociados

- **Documentos requeridos como entrada.**
  - Contrato de transferencia o DPA con el receptor, ya registrado en MOD-009 (tipo de documento "Contrato/DPA", decision 2.7.2 de `02_validacion_de_la_idea.md`).
  - Aviso de privacidad vigente del tratamiento de origen (MOD-008), para verificar que menciona la posibilidad de transferencia si corresponde.
- **Documentos generados por este modulo.**
  - Borrador de "puesta en conocimiento a la ACE" (se materializa como registro ACEFiling dentro de MOD-024, pero el contenido nace en este modulo).
  - Ficha de evaluacion del pais receptor (resumen de los factores marcados en el cuestionario, exportable a PDF).
  - Solicitud opcional de opinion previa a la ACE (tambien materializada en MOD-024).
  - Expediente de transferencia completo, exportable como paquete de evidencia (MOD-019).
- **Plantillas que el sistema provee.**
  - Plantilla de contrato de transferencia internacional, con variables (nombre del receptor, pais, categorias de datos, finalidad, salvaguardas), marcada siempre como borrador que requiere validacion de la organizacion antes de firmarse (anti-feature 17).
  - Plantilla del cuestionario de evaluacion de pais receptor.
  - Plantilla del contenido de puesta en conocimiento a la ACE.
- **Anexos y evidencias documentales.** Capturas de pantalla o acuses de envio a la ACE (mientras no exista canal formal), correos de confirmacion del proveedor receptor, certificaciones de seguridad del proveedor (por ejemplo, ISO 27001), evidencia de cifrado en transito.

## L. Dependencias

```
MOD-001 (Organizacion)  --------\
                                  v
MOD-006 (RAT) ------------------> MOD-010 (Transferencias) -----> MOD-007 (Consentimiento)
MOD-009 (Proveedores) ----------> MOD-010                   -----> MOD-015 (Controles: evidencia SSL/TLS)
MOD-004 (Diagnostico, senal parcial en MVP) -> tarea en MOD-021    -----> MOD-019 (Centro de Evidencias)
                                                                    -----> MOD-024 (Tramites ante la ACE)
                                                                    -----> MOD-021 (Tareas)
                                                                    -----> MOD-022 (Notificaciones)
                                                                    -----> MOD-023 (Calendario, revision periodica)
MOD-011 (ARCO-POL) <----- lectura de transferencias activas para notificar a receptores (OBL-ARCO-11)
```

- **Entra desde (lee por referencia, nunca escribe en esos modulos):** MOD-001 (estructura de la organizacion), MOD-006 (tratamiento de origen, categorias de datos), MOD-009 (receptor, rol del receptor, contrato), MOD-004 (senal del diagnostico "datos fuera de El Salvador").
- **Sale hacia (alimenta con datos o eventos):** MOD-007 (vincula el consentimiento especifico exigido por OBL-TRANSF-04), MOD-015 (aporta evidencia de salvaguardas tecnicas para OBL-SEG-04), MOD-019 (entrega su expediente al paquete de evidencia), MOD-024 (genera el borrador de puesta en conocimiento a la ACE y, opcionalmente, la solicitud de opinion previa), MOD-021 (crea tareas), MOD-022 (dispara notificaciones), MOD-023 (usa el motor de calendario para la revision periodica). MOD-011 lee (no escribe) las transferencias activas de un tratamiento cuando gestiona la notificacion a receptores tras una rectificacion o eliminacion (OBL-ARCO-11).
- **Que ocurre si un modulo dependiente no existe en el MVP.** Segun `06_mapa_definitivo_de_modulos.md`, MOD-001, MOD-004, MOD-006, MOD-007, MOD-009, MOD-011, MOD-015, MOD-019, MOD-021, MOD-022, MOD-023 y el nucleo de MOD-024 son todos MUST HAVE: estan garantizados en el MVP. El unico modulo que puede faltar en el MVP es este mismo (MOD-010, SHOULD HAVE). Cuando MOD-010 no esta disponible, la cobertura parcial documentada en el mapa de modulos aplica: el Diagnostico (MOD-004) detecta la senal "datos fuera de El Salvador: si" y crea una tarea manual en el Centro de Tareas (MOD-021) para que el responsable documente la transferencia como evidencia suelta en el Centro de Evidencias (MOD-019), sin motor de deteccion automatica de proveedores extranjeros ni estados de workflow propios.

## M. Dashboard

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Transferencias activas registradas | Conteo de registros en estado ACTIVA | No aplica (informativo) | Gerencia (numero total), Responsable/Legal (listado), Auditor (listado con expediente) |
| Transferencias pendientes de confirmar | Conteo de registros en DETECTADA_PENDIENTE_DE_CONFIRMAR | Verde: 0. Amarillo: 1-4. Rojo: 5 o mas, o alguna con mas de 15 dias habiles sin confirmar | Responsable (su area), Legal (toda la organizacion), Gerencia (solo el numero) |
| Transferencias internacionales sin evaluacion de pais completa | Conteo de registros en EN_EVALUACION_DE_PAIS con mas de 10 dias habiles en ese estado | Verde: 0. Amarillo: 1-2. Rojo: 3 o mas | Legal, Auditor |
| Puestas en conocimiento a la ACE pendientes de envio | Conteo de ACEFiling de tipo transferencia en estado distinto de "enviado" | Verde: 0. Amarillo: 1-2. Rojo: 3 o mas, o alguna con mas de 30 dias habiles pendiente | Delegado, Legal |
| Contratos de transferencia vencidos o por vencer | Conteo de transferencias ACTIVAS con contrato vencido o a menos de 30 dias de vencer | Verde: 0. Amarillo: contratos por vencer. Rojo: al menos un contrato vencido | Legal, Responsable de Seguridad/IT, Gerencia |
| Cobertura de evidencia de transferencias | Porcentaje de transferencias ACTIVAS con expediente completo (evaluacion de pais, contrato, salvaguardas y, si aplica, consentimiento, todos presentes) | Verde: 90-100%. Amarillo: 70-89%. Rojo: menos de 70% | Auditor, Legal, Gerencia (texto: "estado del expediente de transferencias", nunca "cumplimiento legal") |

Conforme a la regla del sistema, ningun indicador de este modulo se expresa como "porcentaje de cumplimiento legal"; todos describen estado del registro, tareas pendientes o evidencia disponible.

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia para auditoria/ACE |
|---|---|---|---|---|---|
| Listado de transferencias | Todas las transferencias con estado, pais, receptor, base juridica y fecha de ultima revision | Estado, tipo (nacional/internacional), pais, receptor, rango de fechas | XLSX, CSV | Legal, Gerencia | No, es de uso interno de gestion |
| Expediente individual de transferencia | Ficha completa de una transferencia con su historial de estados y adjuntos | Una transferencia especifica | PDF | Auditor, Delegado, asesor externo invitado sobre el caso | Si |
| Paquete de evidencia de transferencias | Conjunto de expedientes de todas las transferencias ACTIVAS o del periodo solicitado, con hash de integridad | Rango de fechas, estado | ZIP (con PDF y adjuntos originales) | Auditor externo, para la auditoria anual (OBL-AUD-01) | Si |
| Transferencias pendientes o con riesgo abierto | Registros en DETECTADA_PENDIENTE_DE_CONFIRMAR, con nota de riesgo abierta, o con contrato vencido | Tipo de pendiente | PDF, XLSX | Delegado, Gerencia | No |
| Registro de puestas en conocimiento a la ACE | Historial de todos los intentos de notificacion a la ACE por transferencia, con su estado | Rango de fechas, estado | PDF | Delegado, Auditor externo | Si |

## O. Historial

Eventos que quedan en el historial del modulo y se replican en la auditoria transversal (AuditLog, MOD-019/MOD-021 segun corresponda):

- Creacion de un registro (manual o por deteccion automatica), con el origen indicado.
- Cambio de cualquier campo, con el valor anterior y el nuevo, quien lo hizo y cuando.
- Cambio de estado (ver tabla de transiciones en F), con quien lo ejecuto y el motivo cuando el flujo lo exige (suspension, descarte, rechazo).
- Confirmacion o descarte de una transferencia detectada automaticamente, con el motivo si fue descartada.
- Asignacion o reasignacion de la tarea de confirmacion o de revision periodica.
- Aprobacion o rechazo del paso a ACTIVA, con identidad y fecha.
- Adjuntos agregados o eliminados, con hash de cada archivo.
- Exportaciones del expediente o del paquete de evidencia, con quien exporto y para que destinatario (por ejemplo, "exportado para auditor externo Ing. Francisco Bonilla, periodo 2026").
- Accesos de lectura de un auditor externo o un asesor externo invitado al expediente (registro de quien vio que y cuando, dado el caracter temporal y acotado de esos roles).
- Vinculacion o desvinculacion de un consentimiento, un contrato o una evaluacion de pais.
- Marcado de un registro como huerfano (tratamiento o receptor eliminado) y su resolucion posterior.
- Archivado (paso a FINALIZADA o DESCARTADA), nunca eliminacion: el sistema no permite borrar un registro de transferencia ni su historial (anti-feature 19, bitacora de solo escritura por adicion).

## P. Riesgos

- **Riesgo legal: que el sistema, sin querer, de la impresion de estar calificando el pais receptor como "adecuado".** Mitigacion de diseno: el cuestionario de evaluacion de pais nunca produce una etiqueta tipo "Pais adecuado" o "Pais de riesgo"; solo muestra los factores marcados y el texto "Requiere validacion de la organizacion o asesoria especializada" en todo momento en que se consulta la evaluacion.
- **Riesgo legal: tratar la excepcion de integracion centroamericana como una casilla mas, sin friccion.** Mitigacion: esa opcion nunca aparece preseleccionada, exige una confirmacion explicita adicional y muestra siempre la advertencia de que no existe desarrollo reglamentario de la excepcion.
- **Riesgo de UX: que el responsable de area abandone la tarea de confirmar una transferencia detectada automaticamente por no entender por que se le pide algo que el no origino (solo contrato un proveedor).** Mitigacion: el texto de la tarea explica en una frase simple por que se genero (ver seccion R) y ofrece la opcion de reasignarla a Legal/Compliance si el usuario no tiene la informacion necesaria, sin poder simplemente ignorarla.
- **Riesgo de UX: sobrecarga del formulario de alta con demasiados campos legales a la vez.** Mitigacion: el flujo se divide en pasos (datos basicos -> tipo y receptor -> base juridica -> evaluacion de pais si aplica -> salvaguardas y contrato), y solo los campos minimos son obligatorios para guardar un BORRADOR; el resto se completa antes de pasar a los estados siguientes.
- **Riesgo operativo: que la deteccion automatica genere demasiado ruido (falsos positivos) si la empresa tiene proveedores extranjeros sin tratamiento real de datos personales (por ejemplo, un proveedor de papeleria con sede en otro pais que no procesa datos).** Mitigacion: la accion de "Descartar" en DETECTADA_PENDIENTE_DE_CONFIRMAR es rapida (un clic mas motivo breve) y el sistema aprende a no volver a alertar sobre el mismo proveedor una vez descartado, salvo que cambien sus datos en MOD-009.
- **Riesgo operativo: plazos de revision periodica mal calculados si el calendario de dias habiles (MOD-023) no esta actualizado con los asuetos vigentes.** Mitigacion: este modulo consume el motor de plazos compartido de MOD-023 en vez de calcular fechas por su cuenta, para que cualquier correccion del calendario se aplique automaticamente a todas las revisiones pendientes.
- **Riesgo de seguridad y privacidad: que un usuario adjunte, por error, un documento con datos personales de titulares finales (por ejemplo, un archivo exportado de nomina) como "evidencia" de la transferencia.** Mitigacion: el texto de ayuda del campo de adjuntos advierte explicitamente de esto, y el campo de categorias de datos exige tipo de dato (metadato), no el dato en si, reduciendo la tentacion de adjuntar el archivo real.
- **Riesgo de seguridad y privacidad: exposicion de informacion contractual sensible del proveedor (precios, clausulas de penalizacion) a roles que no la necesitan.** Mitigacion: el contrato en si vive en MOD-009 con sus propios permisos; este modulo solo referencia su existencia y vigencia, no reproduce su contenido completo en la vista de Transferencias.

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Registro manual basico de una transferencia (tratamiento, receptor, pais, base, finalidad) | | X | | | Es el nucleo minimo del modulo cuando este se construye; sin el, el modulo no existe. No es MUST HAVE del producto global porque el modulo completo es SHOULD HAVE (no cubre una obligacion OBLIGATORIO con plazo ya vencido ni es dependencia estructural de otro MUST HAVE, test de tres condiciones de `06_mapa_definitivo_de_modulos.md`). |
| Workflow de estados (BORRADOR -> EN_EVALUACION_DE_PAIS -> PENDIENTE_DE_APROBACION -> ACTIVA) | | X | | | Necesario para que el registro basico tenga control de aprobacion y no quede como una simple lista plana; viaja junto con el registro basico. |
| Cuestionario de evaluacion de pais receptor | | X | | | Exigido por OBL-TRANSF-03; sin el, el registro basico no cubre la obligacion internacional principal. |
| Vinculacion de consentimiento especifico (MOD-007) | | X | | | Exigido por OBL-TRANSF-04, condicion para activar una transferencia internacional. |
| Deteccion automatica de transferencias no documentadas al dar de alta un proveedor extranjero | | | X | | Mejora significativa de riesgo, pero la cobertura parcial del MVP (tarea manual desde el Diagnostico) ya cubre la senal minima sin este motor; se construye despues del registro manual basico. |
| Generacion automatica del borrador de puesta en conocimiento a la ACE (integracion con MOD-024) | | | X | | Depende de que MOD-024 tenga ya su pieza de Tramites ante la ACE madura; se puede operar en su version inicial con un registro manual mas simple. |
| Solicitud de opinion previa a la ACE | | | | X | Es una facultad opcional del Art. 45 LPDP, sin OBL-ID propio en la matriz, no una obligacion; se deja para una version posterior sin que eso deje ninguna obligacion sin cubrir. |
| Revision periodica automatizada con calendario y alertas escalonadas | | | X | | Mejora de mantenimiento del registro; el registro basico puede operar inicialmente con revision manual sin recordatorio automatico. |
| Reportes y paquete de evidencia exportable con hash | | X | | | Es lo que hace probatorio al modulo (OBL-TRANSF-06); sin exportacion verificable, el registro no sirve ante una auditoria o una fiscalizacion. |
| Panel comparativo de transferencias por pais o por proveedor a nivel de grupo corporativo | | | | X | Util solo para el perfil de grupo corporativo con varias sociedades (Enterprise, decision 2.7.31 de `02_validacion_de_la_idea.md`), fuera del alcance de una empresa individual del MVP. |

**Version minima del modulo que ya puede venderse.** La version minima vendible de MOD-010, cuando se construya, es: registro manual de transferencias con sus campos esenciales, workflow de aprobacion de dos pasos (evaluacion de pais mas aprobacion), vinculacion de consentimiento y de contrato por referencia, y exportacion de expediente con evidencia verificable. Esta version ya cubre las seis obligaciones propietarias (OBL-TRANSF-01 a 06) de forma operativa, aunque de forma manual en vez de automatica; la deteccion automatica de transferencias no documentadas, la integracion completa con el tramite de la ACE y la solicitud de opinion previa son mejoras que se agregan despues sin dejar ninguna obligacion legal sin una forma de cumplirse.

## R. Ayuda contextual (complemento obligatorio)

**1. Que es una transferencia internacional de datos**
- Que es: Enviar datos personales de una persona (por ejemplo, un cliente o un empleado) a una empresa, proveedor o servidor que esta fuera de El Salvador, aunque sea solo para guardarlos.
- Por que tengo que hacer esto: Porque la ley le pide a su empresa, antes de enviar esos datos a otro pais, avisar al titular, pedirle su consentimiento y verificar que el pais de destino ofrezca una proteccion razonable a esos datos.
- Fundamento: Arts. 44 y 45 de la Ley para la Proteccion de Datos Personales (OBL-TRANSF-03, OBL-TRANSF-04, OBL-TRANSF-05).
- Cuando necesito ayuda juridica: Si no esta seguro de si un proveedor cloud o una herramienta con servidores en otro pais cuenta como transferencia, o si quiere invocar la excepcion de integracion centroamericana.

**2. Nivel de proteccion del pais receptor**
- Que es: Un conjunto de preguntas que le ayudan a reunir informacion sobre que tan protegidos estan los datos en el pais al que los va a enviar (si tiene su propia ley de proteccion de datos, si el proveedor tiene certificaciones de seguridad, si existen clausulas contractuales adicionales).
- Por que tengo que hacer esto: Porque la ley exige que el pais de destino cumpla como minimo los mismos principios que exige El Salvador, y su empresa es quien debe poder demostrar que lo evaluo.
- Fundamento: Art. 44 inciso 1 (OBL-TRANSF-03).
- Cuando necesito ayuda juridica: Siempre que el resultado del cuestionario no sea claro, o si el pais de destino no tiene una ley de proteccion de datos reconocida; el sistema nunca le dira si el pais es "adecuado" o no, esa conclusion la debe validar su organizacion o su asesor legal.

**3. Puesta en conocimiento a la ACE**
- Que es: Un aviso que, segun la ley, su empresa debe darle a la Agencia de Ciberseguridad del Estado (ACE) cada vez que envia datos personales a otro pais.
- Por que tengo que hacer esto: Es un requisito legal independiente del consentimiento del titular; aplica siempre que exista un flujo de datos hacia el extranjero.
- Fundamento: Art. 45 de la ley (OBL-TRANSF-05).
- Cuando necesito ayuda juridica: La ACE todavia no ha habilitado un canal oficial para recibir este aviso (a la fecha de este analisis). El sistema deja constancia de que su empresa intento cumplir, pero le recomendamos consultar con su asesoria legal como manejar esta situacion mientras la autoridad no defina el mecanismo.

**4. Encargado extranjero frente a transferencia internacional**
- Que es: La diferencia entre "transferir" datos a otra empresa que decide por su cuenta que hacer con ellos, y simplemente usar un proveedor (como un servicio de nube) que solo sigue sus instrucciones, pero que esta fisicamente fuera de El Salvador.
- Por que tengo que hacer esto: La ley no es clara sobre si el segundo caso cuenta como "transferencia" con todas sus obligaciones (consentimiento, evaluacion de pais, aviso a la ACE), o si se rige por reglas distintas (las de los encargados del tratamiento).
- Fundamento: Art. 4 lit. u (definicion de transferencia, que excluye al encargado) frente a los Arts. 44 y 45 (cuyas definiciones de emisor y receptor si lo incluyen); ver `03_hallazgos_regulatorios.md`, seccion 9, incertidumbre 10.
- Cuando necesito ayuda juridica: Siempre que contrate un proveedor de nube o de software fuera de El Salvador. El sistema aplica por defecto el criterio mas prudente (tratarlo como transferencia), pero esta es una de las preguntas legales genuinamente abiertas de la ley salvadorena; su asesoria legal puede darle un criterio mas especifico para su caso.

**5. Base juridica de la transferencia**
- Que es: La razon legal que justifica que su empresa envie esos datos a otro pais. La mas comun, y casi la unica prevista de forma expresa por la ley, es el consentimiento especifico del titular para esa transferencia en particular.
- Por que tengo que hacer esto: Sin una base juridica valida y documentada, la transferencia internacional se considera indebida y puede dar lugar a una sancion muy grave.
- Fundamento: Art. 44 inciso final (OBL-TRANSF-04).
- Cuando necesito ayuda juridica: Si considera que el consentimiento no es viable para su caso (por ejemplo, porque el titular no tiene forma de negarse sin afectar el servicio) y quiere explorar si existe alguna excepcion aplicable.

---

## Nota final: observaciones y posible desacuerdo con el mapa de modulos

1. **El nombre del modulo ("Transferencias Internacionales") es mas estrecho que las obligaciones que posee como propietario.** OBL-TRANSF-01 (Art. 40) y OBL-TRANSF-02 (Art. 41) hablan de "toda transferencia de datos personales" y de un "contrato con el responsable receptor", sin limitarse a transferencias internacionales; el propio texto de la obligacion no distingue nacional de internacional, y solo a partir de OBL-TRANSF-03 (Art. 44) la ley empieza a hablar especificamente de transferencias internacionales. El proposito del modulo en `mapa_modulos.json` ("Registra cada flujo de datos hacia otro pais") tambien es mas estrecho que esas dos obligaciones. Esta ficha resuelve la tension incluyendo un campo "Tipo de transferencia" (Nacional a otro responsable / Internacional) para que el modulo cubra de forma completa OBL-TRANSF-01 y OBL-TRANSF-02 sin dejar sin dueño las transferencias domesticas a otro responsable (que no tienen otro modulo propietario en el mapa). Se recomienda que el equipo de producto confirme si el nombre visible del modulo en la interfaz deberia ser mas neutro (por ejemplo, "Transferencias de Datos") para no sugerir que solo cubre casos internacionales, sin que esto implique cambiar su codigo (MOD-010) ni su ubicacion en el arbol de modulos.
2. **No se detecto ningun otro desacuerdo con las fuentes de diseno ya decididas** (mapa definitivo de modulos, `mapa_modulos.json`, validacion de la idea seccion 2.7, objetivo exacto del producto, tipos de usuario, anti-features). Las decisiones de alcance citadas en esta ficha (2.7.2 sobre Contratos/DPA como documento de Proveedores, 2.7.9 sobre encargado extranjero pendiente de confirmar, 2.7.19 sobre Tramites ante la ACE) se aplicaron tal como estan descritas en `02_validacion_de_la_idea.md`, sin contradecirlas.
