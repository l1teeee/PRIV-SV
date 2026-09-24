# MODULO: Diagnostico de Cumplimiento

Codigo corto del modulo: MOD-004
Clasificacion global del modulo: MUST HAVE
Obligaciones que cubre (propietarias): OBL-AMB-01, OBL-AMB-02, OBL-AMB-03, OBL-AMB-04
Obligaciones colaboradoras que este modulo detecta y deriva hacia su modulo propietario (ver tabla completa de disparadores en la seccion G): OBL-PLAZO-03, OBL-PLAZO-04, OBL-SENS-01, OBL-SENS-04, OBL-SENS-06, OBL-SENS-07, OBL-SENS-08, OBL-PRIN-02, OBL-PRIN-04, OBL-CONS-04, OBL-CONS-06, OBL-AVISO-01, OBL-AVISO-03, OBL-AVISO-04, OBL-AVISO-05, OBL-DOC-01, OBL-DOC-02, OBL-DOC-03, OBL-DPO-01, OBL-DPO-03, OBL-PROV-01, OBL-PROV-02, OBL-PROV-03, OBL-PROV-05, OBL-TRANSF-01, OBL-TRANSF-02, OBL-TRANSF-03, OBL-TRANSF-04, OBL-TRANSF-05, OBL-TRANSF-06, OBL-SEG-02, OBL-SEG-03, OBL-INC-01, OBL-INC-02, OBL-INC-04, OBL-INC-05, OBL-ARCO-05, OBL-ARCO-08, OBL-ARCO-10.

---

## A. Proposito

- **Por que existe.** Una persona sin formacion juridica no puede leer los 64 articulos de la Ley para la Proteccion de Datos Personales (Decreto Legislativo 144), sus Politicas de Actuacion ni sus Lineamientos y deducir por si misma que le aplica a su empresa. El Diagnostico de Cumplimiento traduce esa lectura en un cuestionario guiado, en lenguaje sencillo, organizado en 11 bloques tematicos que reflejan como una empresa realmente opera (su gente, sus clientes, su marketing, su tecnologia), no como esta organizada la ley.
- **Que problema resuelve para la empresa.** Sin este modulo, la empresa no sabe por donde empezar ni que modulos del resto del sistema activar. El diagnostico es la puerta de entrada operativa: convierte cada respuesta relevante en un tratamiento sugerido para el Registro de Actividades de Tratamiento (MOD-006), una tarea concreta en el Centro de Tareas (MOD-021), un documento sugerido en Documentos y Politicas (MOD-008) y, cuando corresponde, una evaluacion de riesgo en Riesgos y EIPD (MOD-014).
- **Que obligacion u obligaciones cubre.** Como propietario: OBL-AMB-01 (Art. 2 inc. 1, ambito universal de la ley), OBL-AMB-02 (Art. 3 lit. a, exclusion de historial crediticio), OBL-AMB-03 (Art. 3 lit. b, exclusion domestica) y OBL-AMB-04 (Art. 3 lit. c y d, exclusiones de seguridad publica y registros publicos). Estas cuatro obligaciones son el analisis de aplicabilidad de la ley al caso concreto de la empresa, y este modulo es el unico lugar del sistema donde ese analisis se documenta de forma estructurada. Como colaborador, detecta las condiciones que activan decenas de obligaciones adicionales cuyo dueno funcional es otro modulo (ver seccion G).
- **Que valor aporta.** Operativo: evita que la empresa tenga que decidir por su cuenta que modulos usar. Probatorio: deja evidencia fechada de que la empresa analizo su propia exposicion legal (fundamento de OBL-PRIN-03, responsabilidad demostrada, Art. 5 lit. i, propietario MOD-019) antes de que la ACE se lo pida. De reduccion de riesgo: prioriza explicitamente para el usuario que accion es critica, importante o recomendada, en lugar de entregarle 105 obligaciones sin orden.
- **Que NO hace este modulo (limites explicitos).** No decide si una exclusion del Art. 3 aplica de forma definitiva: marca la posibilidad y exige confirmacion humana (ver seccion H). No redacta documentos legales, solo sugiere cual falta y en que modulo crearlo. No calcula ni afirma un porcentaje de "cumplimiento legal": calcula un nivel de madurez del programa y un conteo de acciones pendientes (ver seccion E). No sustituye la calificacion oficial de "operador de infraestructura critica" que solo la ACE puede otorgar (OBL-INC-05). No es el lugar donde se registra el detalle final de un tratamiento, un proveedor, un incidente o una EIPD: solo los siembra como sugerencia en el modulo que es su dueno.

---

## B. Usuarios

| Rol estandar | Para que lo usa en este modulo |
|---|---|
| Administrador de la organizacion | Inicia la sesion de diagnostico despues del Onboarding (MOD-003), decide si se responde en bloque unico o se asigna por areas, y ve el resultado global. |
| Delegado de Proteccion de Datos / Responsable interno (MOD-002) | Revisa el resultado completo, prioriza las acciones criticas, y es quien por defecto debe confirmar el cierre de la sesion antes de que el resultado alimente el Plan de Cumplimiento (MOD-005). |
| Responsable ARCO-POL / Responsable del tramite | Consulta el bloque de gobernanza (historial de solicitudes previas) cuando existe, pero no suele responder el cuestionario. |
| Responsable Legal / Compliance | Revisa y confirma las respuestas marcadas como "requiere validacion de la organizacion o asesoria especializada" (exclusiones del Art. 3, base juridica, transferencias). |
| Responsable de Seguridad / IT | Responde los bloques de tecnologia y proveedores, seguridad, y la parte tecnica de videovigilancia/biometria. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Responde el bloque correspondiente a su area cuando el Administrador asigna bloques por responsable (por ejemplo RRHH responde Personas, Marketing responde Marketing y Web). |
| Aprobador | Aprueba el cierre del resultado cuando la organizacion activa doble control para sesiones con acciones criticas (rol configurable, ver seccion C). |
| Auditor (interno) | Consulta en solo lectura el historial de diagnosticos completados, como evidencia para la auditoria anual de cumplimiento (OBL-AUD-01, propietario MOD-018). |
| Auditor externo (invitado) | Accede en solo lectura, por invitacion puntual, al resultado exportado como parte del paquete de evidencias de una auditoria. |
| Usuario de consulta / Colaborador | No interactua con el diagnostico en si; recibe y completa las tareas puntuales que el diagnostico genero en el Centro de Tareas (MOD-021). |
| Titular (formulario externo) | No aplica. El diagnostico es una herramienta interna de la empresa, el titular externo nunca lo ve ni participa en el. |
| Asesor externo invitado | Revisa puntualmente, por invitacion acotada a un bloque o pregunta, una respuesta marcada como "requiere asesoria legal" (por ejemplo la tension entre LPDP y Ley Crecer Juntos en el bloque Menores). |

---

## C. Permisos

Leyenda: X = permitido sin restriccion. P = permitido solo sobre el bloque que tiene asignado. A = permitido solo si la organizacion activa la aprobacion en paralelo (doble control). L = solo lectura. - = no permitido.

| Accion | Adm. | Delegado / Resp. interno | Resp. ARCO-POL | Legal / Compliance | Seg. / IT | Resp. de area | Aprobador | Auditor interno | Auditor externo | Usuario consulta | Titular | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver resultado completo | X | X | - | X | P | P | X | L | L | - | - | L |
| Iniciar / crear sesion | X | X | - | - | - | - | - | - | - | - | - | - |
| Responder / modificar respuestas | X | X | - | - | P | P | - | - | - | - | - | - |
| Aprobar cierre del resultado | X | X | - | A | - | - | A | - | - | - | - | - |
| Cerrar la sesion (generar resultado) | X | X | - | - | - | - | - | - | - | - | - | - |
| Eliminar / archivar una sesion | X | - | - | - | - | - | - | - | - | - | - | - |
| Exportar resultado | X | X | - | X | - | - | - | L | L | - | - | - |
| Asignar bloques a responsables | X | X | - | - | - | - | - | - | - | - | - | - |
| Comentar en una pregunta | X | X | - | X | P | P | - | - | - | - | - | L |
| Adjuntar evidencia a una respuesta | X | X | - | - | P | P | - | - | - | - | - | - |

Separacion de funciones: cuando el resultado contiene al menos una accion CRITICA, el cierre de la sesion exige una segunda confirmacion (Legal/Compliance o Aprobador) distinta de quien respondio el cuestionario, siguiendo el mismo criterio de umbral configurable descrito en `05_tipos_de_usuario.md` seccion 5.4 (por debajo del umbral de tamano, la doble confirmacion se recomienda pero no se bloquea). Eliminar o archivar una sesion es exclusivo del Administrador (nunca del Delegado) para que quien participa en el contenido del diagnostico no pueda tambien hacerlo desaparecer del historial; en la practica archivar nunca borra el registro subyacente (ver seccion O, principio de historial append-only).

---

## D. Informacion de entrada

### D.1 Campos de la sesion de diagnostico (nivel de cabecera, no son preguntas)

| Campo | Tipo | Obligatorio | Opciones o catalogo | Validacion | Ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|
| Organizacion | Referencia a Organization | Obligatorio | - | Debe existir una organizacion creada en MOD-001/MOD-003 | Se precarga automaticamente de la organizacion activa, no se pide de nuevo | Buena practica |
| Responsable de la sesion | Referencia a User | Obligatorio | Usuarios activos de la organizacion | Debe tener un rol con permiso de "iniciar sesion" (ver seccion C) | Quien queda como responsable de que el diagnostico se complete | Buena practica |
| Version del cuestionario | Texto corto, calculado | Obligatorio, automatico | - | Se asigna al crear la sesion y no cambia durante ella | Indica que version de las preguntas se uso, por si el catalogo cambia despues (por ejemplo al activarse el estado FUTURO de la reforma 659) | Principio 8 de `06_mapa_definitivo_de_modulos.md`: nada se borra, todo se versiona |
| Motivo de la sesion | Seleccion unica | Obligatorio | Diagnostico inicial / Re-diagnostico por cambio de actividad / Re-diagnostico periodico | Solo puede ser "Diagnostico inicial" si es la primera sesion cerrada de la organizacion | Explica por que se repite el diagnostico; ayuda a comparar resultados entre sesiones | Decision 2.7.5 de `02_validacion_de_la_idea.md`: el diagnostico es repetible |
| Bloques asignados por responsable | Lista de referencias (bloque, usuario) | Opcional | Los 11 bloques de la seccion D.2 | Un bloque solo puede asignarse a un usuario con permiso "responder" | Permite que cada area responda solo lo que le corresponde en vez de que una sola persona conteste todo | Buena practica (reduce el riesgo de abandono, ver seccion P) |

### D.2 Catalogo de preguntas del diagnostico, por bloque

El cuestionario tiene 47 preguntas organizadas en 11 bloques. Cada pregunta se muestra siempre en modo lenguaje simple; el fundamento normativo (OBL-ID y articulo) solo aparece en la ayuda contextual de segundo nivel, nunca en el texto principal de la pregunta, siguiendo la regla de oro de la plantilla. Salvo que se indique lo contrario, el tipo es "seleccion unica" con opciones Si / No, y la validacion es "debe elegirse una opcion antes de avanzar al siguiente bloque".

**Bloque 1: Empresa (aplicabilidad de la ley)**

| ID | Pregunta (texto simplificado que ve el usuario) | Tipo | Obligatorio | Opciones / catalogo | Depende de | Ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|---|
| P-EMP-01 | Cual es el giro o sector principal de su empresa | Seleccion unica | Obligatorio | Comercio, Servicios, Industria/Manufactura, Salud, Financiero/Seguros, Tecnologia/Software, Educacion, Agroindustria, Otro | Ninguna | Se precarga desde el registro de la organizacion (MOD-001); puede confirmarse o corregirse aqui | OBL-AMB-01, Art. 2 |
| P-EMP-02 | Cuantas personas tiene aproximadamente contratadas | Numero | Obligatorio | - | Ninguna | Se precarga desde MOD-001; se usa para sugerir si conviene activar separacion de funciones mas estricta | Buena practica, `05_tipos_de_usuario.md` 5.4 |
| P-EMP-03 | Su empresa es parte del Sistema Financiero y esta supervisada por la Superintendencia del Sistema Financiero (SSF) | Si/No | Obligatorio | Si, No | Ninguna | Por ejemplo bancos, aseguradoras o financieras reguladas. Si no esta segura, responda No y confirme despues con su area legal | OBL-AMB-02, Art. 3 lit. a |
| P-EMP-04 | Su empresa reporta historial crediticio de personas bajo la ley especial de burós de credito | Si/No | Obligatorio | Si, No | Ninguna | Esta exclusion es muy especifica: solo aplica al reporte de historial crediticio en si, no a toda su operacion | OBL-AMB-02, Art. 3 lit. a |
| P-EMP-05 | El unico tratamiento de datos personales de su empresa es para uso familiar o domestico, sin ningun fin comercial | Si/No | Obligatorio | Si, No | Ninguna | Casi ninguna empresa registrada cumple esta condicion; se pregunta para descartarla explicitamente, no para sugerirla | OBL-AMB-03, Art. 3 lit. b |
| P-EMP-06 | El objeto de su actividad es la seguridad publica, la defensa, la persecucion del delito, o es usted un registro publico oficial (registro del estado familiar, DUI) | Si/No | Obligatorio | Si, No | Ninguna | Aplica solo a entidades con ese objeto exacto, no a empresas privadas que usan camaras o contratan seguridad privada | OBL-AMB-04, Art. 3 lit. c y d |
| P-EMP-07 | Le ha notificado la Agencia de Ciberseguridad del Estado (ACE) que su empresa es operador de infraestructura critica | Si/No/No lo se | Obligatorio | Si, No, No lo se | Ninguna | Esta calificacion la otorga unicamente la ACE; si no esta segura, responda "No lo se" | OBL-INC-05, Art. 6 lit. f-g Ley de Ciberseguridad |
| P-EMP-08 | Su empresa opera con mas de una sucursal o sede | Si/No | Obligatorio | Si, No | Ninguna | Se precarga desde MOD-001 | Buena practica |

**Bloque 2: Personas (RRHH)**

| ID | Pregunta | Tipo | Obligatorio | Opciones | Depende de | Ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|---|
| P-PER-01 | Tiene personal contratado en planilla | Si/No | Obligatorio | Si, No | Ninguna | Incluye planilla permanente y temporal | OBL-DOC-02 (siembra RAT) |
| P-PER-02 | Recibe curriculums o solicitudes de empleo, en fisico o por correo/plataforma | Si/No | Obligatorio | Si, No | Ninguna | Aplica aunque no contrate a la persona | OBL-DOC-02 |
| P-PER-03 | Usa algun sistema de control de asistencia o marcaje del personal | Si/No | Obligatorio si P-PER-01=Si | Si, No | P-PER-01 = Si | Por ejemplo tarjeta, codigo o reloj biometrico | OBL-DOC-02 |
| P-PER-04 | Ese sistema de marcaje usa huella digital, reconocimiento facial, iris u otro dato biometrico | Si/No | Obligatorio si P-PER-03=Si | Si, No | P-PER-03 = Si | La huella digital y el reconocimiento facial son datos biometricos y se tratan como dato sensible | OBL-SENS-06, Art. 4 lit. g |
| P-PER-05 | Realiza examenes medicos ocupacionales o conserva expedientes de salud del personal | Si/No | Obligatorio si P-PER-01=Si | Si, No | P-PER-01 = Si | Incluye incapacidades, examenes preempleo o de retiro | OBL-SENS-04, Art. 39 |
| P-PER-06 | Registra la afiliacion sindical de las personas empleadas | Si/No | Obligatorio si P-PER-01=Si | Si, No | P-PER-01 = Si | No se refiere a la nomina general, solo al dato especifico de pertenencia a un sindicato | OBL-SENS-01, Art. 4 lit. g y Art. 59 lit. b |
| P-PER-07 | Contrata servicios externos de verificacion de antecedentes penales o crediticios de candidatos o personal | Si/No | Opcional | Si, No | Ninguna | Por ejemplo un proveedor que verifica antecedentes antes de contratar | OBL-PROV-01 |

**Bloque 3: Clientes**

| ID | Pregunta | Tipo | Obligatorio | Opciones | Depende de | Ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|---|
| P-CLI-01 | Registra datos personales de sus clientes (nombre, contacto, direccion, etc.) | Si/No | Obligatorio | Si, No | Ninguna | Casi toda empresa con clientes identificados responde Si | OBL-DOC-02, OBL-AVISO-01 |
| P-CLI-02 | Usa un sistema CRM o similar para gestionar a sus clientes | Si/No | Obligatorio si P-CLI-01=Si | Si, No | P-CLI-01 = Si | Por ejemplo Salesforce, HubSpot, o una hoja de calculo dedicada cuenta tambien | OBL-DOC-02 |
| P-CLI-03 | Tiene programa de fidelizacion, puntos o membresias | Si/No | Opcional | Si, No | Ninguna | - | OBL-DOC-02 |
| P-CLI-04 | Ofrece financiamiento directo, credito o evalua la capacidad de pago de sus clientes | Si/No | Opcional | Si, No | Ninguna | No confundir con reportar a un buro de credito (eso es la pregunta P-EMP-04) | OBL-AMB-02, OBL-PRIN-02 |

**Bloque 4: Marketing y web**

| ID | Pregunta | Tipo | Obligatorio | Opciones | Depende de | Ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|---|
| P-MKT-01 | Tiene sitio web propio | Si/No | Obligatorio | Si, No | Ninguna | - | OBL-AVISO-01 |
| P-MKT-02 | El sitio web usa cookies u otras tecnologias de rastreo (analytics, pixeles) | Si/No | Obligatorio si P-MKT-01=Si | Si, No | P-MKT-01 = Si | Si usa Google Analytics, Meta Pixel u otra herramienta similar, la respuesta es Si | OBL-AVISO-03, Art. 24 lit. i |
| P-MKT-03 | Tiene formularios de captura de datos en el sitio web o en redes sociales (contacto, registro, boletin, concursos) | Si/No | Opcional | Si, No | Ninguna | - | OBL-AVISO-04, Art. 7 |
| P-MKT-04 | Realiza email marketing o campanas publicitarias digitales dirigidas | Si/No | Opcional | Si, No | Ninguna | - | OBL-ARCO-05, Art. 12 |
| P-MKT-05 | Usa WhatsApp Business u otra plataforma de mensajeria para atencion al cliente o marketing | Si/No | Opcional | Si, No | Ninguna | - | OBL-TRANSF-01, OBL-TRANSF-03 (conexion) |
| P-MKT-06 | Tiene aplicacion movil propia | Si/No | Opcional | Si, No | Ninguna | - | OBL-AVISO-01, OBL-PRIN-02 |

**Bloque 5: Tecnologia y proveedores**

| ID | Pregunta | Tipo | Obligatorio | Opciones | Depende de | Ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|---|
| P-TEC-01 | Usa servicios en la nube para almacenar o procesar datos personales (correo, ERP, CRM, respaldo) | Si/No | Obligatorio | Si, No | Ninguna | Por ejemplo Google Workspace, Microsoft 365, AWS | OBL-DOC-02 |
| P-TEC-02 | Alguno de esos proveedores tecnologicos tiene sus servidores fuera de El Salvador | Si/No/No lo se | Obligatorio si P-TEC-01=Si | Si, No, No lo se | P-TEC-01 = Si | La mayoria de servicios cloud globales almacenan datos fuera del pais; si no lo sabe, responda "No lo se" | OBL-TRANSF-01, OBL-TRANSF-03 |
| P-TEC-03 | Contrata proveedores externos con acceso a datos personales de su empresa (contabilidad, nomina, soporte TI, mensajeria) | Si/No | Obligatorio | Si, No | Ninguna | - | OBL-PROV-01, OBL-PROV-02, OBL-PROV-03 |
| P-TEC-04 | Sabe si alguno de esos proveedores subcontrata a su vez a otro proveedor con acceso a esos mismos datos | Si/No/No lo se | Obligatorio si P-TEC-03=Si | Si, No, No lo se | P-TEC-03 = Si | Por ejemplo su proveedor de nomina usa a su vez un servicio de nube externo | OBL-PROV-05, Art. 33 inc. 2 |

**Bloque 6: Datos sensibles**

| ID | Pregunta | Tipo | Obligatorio | Opciones | Depende de | Ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|---|
| P-SEN-01 | Ademas de lo ya indicado, su empresa trata alguno de estos datos sobre clientes, personal u otras personas | Seleccion multiple | Opcional | Origen etnico o racial, Opiniones politicas, Convicciones religiosas o filosoficas, Orientacion sexual o vida sexual, Nacionalidad como dato sensible especifico, Ninguno de los anteriores | Ninguna | Marque todas las que apliquen; si ninguna aplica, marque "Ninguno de los anteriores" | OBL-SENS-01, Art. 4 lit. g y Art. 59 lit. b |
| P-SEN-02 | Su empresa trata datos geneticos de alguna persona | Si/No | Opcional | Si, No | Ninguna | Por ejemplo pruebas de laboratorio con fines de salud o de identificacion | OBL-SENS-01, OBL-SENS-04 |

**Bloque 7: Menores**

| ID | Pregunta | Tipo | Obligatorio | Opciones | Depende de | Ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|---|
| P-MEN-01 | Su empresa recopila o trata datos de ninas, ninos o adolescentes (menores de 18 anos) | Si/No | Obligatorio | Si, No | Ninguna | Por ejemplo en formularios, redes sociales, programas de fidelizacion o servicios educativos | OBL-PRIN-04, Art. 5 lit. j |
| P-MEN-02 | Esos menores pueden registrarse, crear una cuenta o usar directamente sus servicios digitales sin la intervencion de una persona adulta | Si/No | Obligatorio si P-MEN-01=Si | Si, No | P-MEN-01 = Si | Por ejemplo si un adolescente puede comprar en linea sin que un adulto confirme la compra | OBL-CONS-06, Art. 56 lit. c num. 3 |

**Bloque 8: Videovigilancia y biometria**

| ID | Pregunta | Tipo | Obligatorio | Opciones | Depende de | Ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|---|
| P-VID-01 | Tiene camaras de videovigilancia en sus instalaciones | Si/No | Obligatorio | Si, No | Ninguna | - | OBL-SENS-08, Art. 4 lit. f |
| P-VID-02 | Esas camaras usan reconocimiento facial u otro identificador biometrico | Si/No | Obligatorio si P-VID-01=Si | Si, No | P-VID-01 = Si | La mayoria de camaras convencionales de vigilancia NO hacen esto; solo responda Si si el sistema identifica personas automaticamente | OBL-SENS-06, OBL-SENS-08 |
| P-VID-03 | Aparte del control de acceso del personal (pregunta anterior sobre marcaje), usa biometria para identificar o autenticar clientes o publico general | Si/No | Opcional | Si, No | Ninguna | Por ejemplo huella para acceder a instalaciones abiertas al publico | OBL-SENS-06, OBL-SENS-07 |

**Bloque 9: Transferencias**

| ID | Pregunta | Tipo | Obligatorio | Opciones | Depende de | Ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|---|
| P-TRF-01 | Los datos personales que trata su empresa se almacenan, respaldan o procesan en servidores fuera de El Salvador (incluidos los de sus proveedores) | Si/No | Obligatorio | Si, No | Se sugiere prellenado con la respuesta de P-TEC-02, pero es confirmable de forma independiente | Incluye respaldos en la nube fuera del pais, no solo el sistema principal | OBL-TRANSF-01, OBL-TRANSF-03 |
| P-TRF-02 | Su empresa forma parte de un grupo corporativo con sociedades en otros paises con las que comparte datos personales | Si/No | Opcional | Si, No | Ninguna | - | OBL-TRANSF-01, OBL-TRANSF-02 |
| P-TRF-03 | Alguna autoridad, cliente corporativo o casa matriz en el extranjero le ha pedido enviar datos personales fuera de El Salvador | Si/No | Opcional | Si, No | Ninguna | - | OBL-TRANSF-04, Art. 44 |

**Bloque 10: Seguridad**

| ID | Pregunta | Tipo | Obligatorio | Opciones | Depende de | Ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|---|
| P-SEG-01 | Hay una persona o area responsable de administrar los permisos de acceso a los sistemas con datos personales | Si/No | Obligatorio | Si, No | Ninguna | - | OBL-SEG-02, Art. 4 Medidas Organizativas |
| P-SEG-02 | Los sistemas con datos personales usan autenticacion de dos factores (2FA/MFA) | Si/No/No lo se | Obligatorio | Si, No, No lo se | Ninguna | Si no administra usted mismo estos sistemas, consulte con su proveedor de TI antes de responder | OBL-SEG-03, Art. 4 Medidas Tecnicas |
| P-SEG-03 | La informacion de sus sistemas se respalda (backup) de forma periodica | Si/No/No lo se | Obligatorio | Si, No, No lo se | Ninguna | - | OBL-SEG-03 |
| P-SEG-04 | En el ultimo ano, ha identificado algun acceso no autorizado, perdida o fuga de datos personales, se haya reportado formalmente o no | Si/No | Obligatorio | Si, No | Ninguna | Responda Si aunque el hecho no se haya documentado o comunicado en su momento | OBL-INC-01, OBL-INC-04 |

**Bloque 11: Gobernanza**

| ID | Pregunta | Tipo | Obligatorio | Opciones | Depende de | Ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|---|
| P-GOB-01 | Su empresa ya cuenta con una persona designada formalmente como Delegado de Proteccion de Datos o responsable interno | Si/No | Obligatorio | Si, No | Ninguna | - | OBL-DPO-01, Art. 15 y 17 |
| P-GOB-02 | Su empresa ya cuenta con una Politica de Proteccion de Datos o Politica de Privacidad redactada | Si/No | Obligatorio | Si, No | Ninguna | - | OBL-AVISO-05, OBL-SEG-02 |
| P-GOB-03 | Su empresa ya publico un Aviso de Privacidad | Si/No | Obligatorio | Si, No | Ninguna | - | OBL-AVISO-01, OBL-PLAZO-04 |
| P-GOB-04 | En el ultimo ano, ha recibido alguna solicitud de una persona para ejercer sus derechos sobre sus datos (acceso, correccion, eliminacion, etc.), la haya gestionado formalmente o no | Si/No | Obligatorio | Si, No | Ninguna | Responda Si aunque la solicitud haya llegado por correo, telefono o en persona y no se haya tramitado en ningun sistema | OBL-ARCO-08, OBL-ARCO-10 |

### D.3 Precarga y minimizacion de datos

Los campos P-EMP-01, P-EMP-02 y P-EMP-08 se precargan desde MOD-001 (Organizacion y Personas) a traves de MOD-003 (Onboarding) y solo se confirman o corrigen aqui, nunca se capturan por segunda vez. Ninguna pregunta del diagnostico pide el nombre, DUI, correo o cualquier otro dato identificativo de una persona titular concreta (cliente, empleado o menor): todas las preguntas son sobre la existencia de un tipo de tratamiento, nunca sobre datos de titulares especificos. El propio diagnostico, por diseno, no almacena datos personales de terceros; solo almacena metadatos sobre la actividad de la empresa (privacy by design, acotado segun decision 2.7.21 de `02_validacion_de_la_idea.md`).

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Registro de respuestas (DiagnosticoRespuesta) | Una fila por pregunta respondida, con valor, usuario, fecha y version del cuestionario | Registro interno | En cada respuesta guardada | Historial del modulo (seccion O) |
| Tratamientos sugeridos | Lista de actividades de tratamiento detectadas (por ejemplo "Control de acceso biometrico de personal") | Prellenado de ficha en RAT | Al cerrar la sesion | MOD-006 (RAT y Mapa de Datos) |
| Tareas sugeridas | Lista de acciones con titulo, fundamento (OBL-ID) y prioridad sugerida | Prellenado de tarea | Al cerrar la sesion | MOD-021 (Centro de Tareas) |
| Documentos sugeridos | Lista de plantillas de documento a iniciar (por ejemplo "Aviso de Privacidad", "Clausula de cookies") | Prellenado de borrador | Al cerrar la sesion | MOD-008 (Documentos y Politicas) |
| Evaluaciones de riesgo sugeridas | Lista de tratamientos que requieren EIPD obligatoria o recomendada | Prellenado de evaluacion | Al cerrar la sesion | MOD-014 (Riesgos y EIPD) |
| Resultado del diagnostico | Nivel de madurez inicial y conteo de acciones criticas, importantes y recomendadas (ver seccion E.1) | Panel de resultado + reporte descargable | Al cerrar la sesion | Administrador, Delegado, Legal/Compliance; alimenta el ordenamiento inicial de MOD-005 |
| Evento de auditoria | Creacion, respuesta, cierre y reapertura de la sesion, con usuario y fecha | Registro interno inmutable | En cada evento | MOD-019 (Centro de Evidencias, por referencia) |

### E.1 Calculo del resultado

**Nivel de madurez inicial.** Es un estado del programa, nunca un porcentaje de cumplimiento legal (regla explicita de `04_objetivo_exacto_del_producto.md`, seccion 1.2). Se calcula por reglas simples, no por una formula ponderada:

| Nivel | Condicion |
|---|---|
| INICIAL | No existe Delegado/responsable interno (P-GOB-01 = No), o no existe Aviso de Privacidad publicado (P-GOB-03 = No), o existe al menos una accion CRITICA relacionada con datos sensibles, menores o un incidente no reportado (ver seccion G) |
| EN DESARROLLO | Existen Delegado y Aviso de Privacidad, pero quedan abiertas una o mas acciones CRITICAS de otro origen (RAT incompleto, proveedor sin contrato, transferencia sin documentar) o acciones IMPORTANTES sin asignar |
| EN CONSOLIDACION | Solo quedan abiertas acciones RECOMENDADAS, o ninguna accion pendiente |

**Conteo de acciones criticas, importantes y recomendadas.** Es la suma de las filas de la tabla de disparadores (seccion G.2) cuya condicion se cumplio con las respuestas de esta sesion, agrupadas por la columna Prioridad. Cuando dos o mas preguntas distintas disparan una tarea que apunta al mismo tratamiento u obligacion (por ejemplo P-PER-04 y P-VID-03, ambas sobre biometria), el sistema fusiona ambos disparadores en una sola accion antes de contarla, para no inflar el numero con tareas duplicadas. El resultado se muestra como "X acciones criticas, Y importantes, Z recomendadas", junto con el texto fijo: "Este resultado es un calculo de apoyo interno basado en lo que usted registro, no una declaracion de cumplimiento legal" (mismo texto de descargo que define `04_objetivo_exacto_del_producto.md`, seccion 1.3).

---

## F. Workflow

```
                    [NO INICIADO]
                          |
                          | Administrador o Responsable de area
                          | inicia la sesion (tras completar Onboarding)
                          v
        +-------->  [EN PROGRESO]
        |                 |    |
        |  Guardar y      |    | Responde una pregunta de un bloque
        |  continuar      |    v
        +-----------------+  [BLOQUE COMPLETADO] (se repite bloque a bloque)
        |
   [GUARDADO PARCIAL]
        |
        | El mismo usuario u otro con el bloque asignado retoma la sesion
        +----------------> vuelve a [EN PROGRESO]

   [EN PROGRESO]
        |
        | Todos los bloques obligatorios quedan respondidos
        v
   [PENDIENTE DE CIERRE]
        |
        | Delegado / responsable interno confirma
        | (o Legal/Compliance + Aprobador si hay accion CRITICA, doble control)
        v
   [CERRADO - RESULTADO GENERADO] -----> siembra MOD-005, MOD-006, MOD-008, MOD-014
        |                                y crea tareas en MOD-021
        |
        | Cambio relevante de actividad (nuevo tratamiento, nueva sede,
        | nueva tecnologia) o vencimiento del ciclo periodico configurado
        v
   [RE-DIAGNOSTICO ABIERTO] (nueva sesion, version N+1; la sesion anterior
        |                     queda archivada con su fecha, nunca se borra)
        v
   [EN PROGRESO]  (vuelve al ciclo)
```

### Tabla de transiciones

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| No iniciado | Iniciar sesion | Debe existir organizacion con Onboarding completado (MOD-003) | En progreso | Administrador, Delegado | Crea la sesion con version del cuestionario vigente; evento de auditoria |
| En progreso | Responder una pregunta | La pregunta debe estar visible segun sus dependencias (seccion D.2) | En progreso (bloque avanza) | Quien tiene asignado el bloque, o Administrador/Delegado si no hay asignacion | Guarda la respuesta con usuario y fecha; evalua si dispara una regla de la seccion G |
| En progreso | Guardar y continuar | Ninguna | Guardado parcial | Quien esta respondiendo | Conserva el avance exacto; no genera resultado todavia |
| Guardado parcial | Reanudar | Ninguna | En progreso | Quien tiene asignado el bloque, Administrador, Delegado | Retoma en la ultima pregunta sin respuesta |
| En progreso | Completar todos los bloques obligatorios | Toda pregunta marcada Obligatorio (o Obligatorio condicional que se activo) tiene respuesta | Pendiente de cierre | Sistema (automatico al cumplirse la condicion) | Calcula el resultado preliminar (seccion E.1) para revision |
| Pendiente de cierre | Confirmar cierre | Sin accion CRITICA: un solo confirmante. Con accion CRITICA: doble confirmacion (ver seccion C) | Cerrado - resultado generado | Delegado / responsable interno (y Legal/Compliance o Aprobador si aplica doble control) | Genera tratamientos, tareas, documentos y evaluaciones sugeridas (seccion E); evento de auditoria; bloquea edicion de respuestas |
| Pendiente de cierre | Reabrir para corregir una respuesta | Solo antes de la confirmacion final | En progreso | Quien inicio la sesion, Administrador | Vuelve a habilitar edicion; queda registrado el motivo |
| Cerrado - resultado generado | Iniciar re-diagnostico | La organizacion declara un cambio de actividad, o vence el ciclo periodico configurado (opinion de producto, sin plazo legal fijo) | Re-diagnostico abierto | Administrador, Delegado | Crea una nueva sesion (version N+1); la sesion cerrada anterior pasa a estado Archivado, visible en el historial, nunca eliminada |
| Cerrado - resultado generado | Exportar resultado | Ninguna | Sin cambio de estado | Administrador, Delegado, Legal/Compliance, Auditor (lectura) | Genera el reporte descargable con verificacion de integridad (ver seccion N) |
| Re-diagnostico abierto | Continuar respondiendo | Igual que "En progreso" | En progreso | Igual que "En progreso" | Las respuestas anteriores se muestran precargadas como punto de partida, editables |

No existe un estado de eliminacion definitiva: "Eliminar/archivar" (seccion C) mueve la sesion a Archivado, visible solo para Administrador y Auditor, pero conserva el registro completo para la trazabilidad exigida por el principio de responsabilidad demostrada (OBL-PRIN-03).

---

## G. Automatizaciones

### G.1 Reglas de deteccion de exclusiones del Art. 3 (no generan tarea, generan advertencia)

| Disparador | Condicion | Accion | OBL-ID | Automatizable |
|---|---|---|---|---|
| P-EMP-03 y P-EMP-04 | SSF = Si y reporta historial crediticio = Si | Marca "posible exclusion parcial: solo el reporte de historial crediticio bajo su ley especial queda fuera de la LPDP; el resto de datos que trata la entidad supervisada por la SSF sigue sujeto a la ley" | OBL-AMB-02 | No, requiere confirmacion de Legal/Compliance antes de excluir cualquier tratamiento del alcance del diagnostico (ver seccion H) |
| P-EMP-05 | Si | Marca advertencia: "una empresa registrada formalmente rara vez cumple la condicion de fin exclusivamente domestico"; exige confirmacion explicita del Administrador antes de continuar sin generar tareas para esa actividad | OBL-AMB-03 | No |
| P-EMP-06 | Si | Marca advertencia: "esta exclusion no se extiende por analogia a seguridad privada ni a prevencion de fraude de empresas privadas"; exige confirmacion de Legal/Compliance | OBL-AMB-04 | No |
| P-EMP-07 | Si o No lo se | Crea tarea en MOD-021: "confirmar ante la ACE si la empresa esta calificada como operador de infraestructura critica"; si se confirma, se activa una pregunta adicional del flujo de Incidentes (propietario MOD-013) | OBL-INC-05 | No, la calificacion es exclusiva de la ACE |

### G.2 Tabla completa de disparadores (tratamiento + tarea + documento + riesgo)

Cada fila se activa unicamente si la sesion llega a esa pregunta segun las dependencias de la seccion D.2. La columna Prioridad alimenta el conteo de la seccion E.1.

| Pregunta | Respuesta que dispara | Tratamiento sugerido (a MOD-006) | Tarea creada (a MOD-021) | Documento sugerido (a MOD-008) | Riesgo/evaluacion (a MOD-014) | OBL-ID | Prioridad |
|---|---|---|---|---|---|---|---|
| P-PER-01 | Si | Gestion de datos de personal (nomina, expediente laboral) | Completar la ficha de RAT del tratamiento de personal | - | - | OBL-DOC-02 | CRITICA (plazo OBL-PLAZO-03 vencido) |
| P-PER-03 | Si | Control de asistencia del personal | Completar la ficha de RAT | - | - | OBL-DOC-02 | RECOMENDADA |
| P-PER-04 | Si | Control de acceso biometrico de personal (dato sensible) | Registrar consentimiento por escrito y ofrecer alternativa no biometrica a cada persona empleada | Aviso especifico de biometria laboral | EIPD recomendada | OBL-SENS-06, OBL-SENS-07, OBL-CONS-04 | CRITICA |
| P-PER-05 | Si | Gestion de expedientes de salud ocupacional | Definir base juridica y medidas reforzadas para datos de salud | Clausula de datos de salud en el aviso de RRHH | EIPD recomendada | OBL-SENS-01, OBL-SENS-04 | IMPORTANTE |
| P-PER-06 | Si | Registro de afiliacion sindical | Confirmar base juridica y consentimiento reforzado para este dato sensible | - | Evaluacion de riesgo basica | OBL-SENS-01 | IMPORTANTE |
| P-CLI-01 | Si | Gestion de datos de clientes | Completar la ficha de RAT del tratamiento de clientes | Aviso de Privacidad (clientes) | - | OBL-DOC-02, OBL-AVISO-01 | CRITICA (plazo OBL-PLAZO-03 y OBL-PLAZO-04 vencidos) |
| P-CLI-02 | Si | Gestion de clientes via CRM | Registrar el CRM en el Catalogo de sistemas y, si es externo, en Proveedores | - | - | OBL-DOC-02, OBL-PROV-01 | RECOMENDADA |
| P-CLI-03 | Si | Programa de fidelizacion | Completar la ficha de RAT | - | - | OBL-DOC-02 | RECOMENDADA |
| P-CLI-04 | Si | Evaluacion de capacidad de pago / financiamiento | Confirmar la base juridica (contrato) para este tratamiento | - | Evaluacion de base juridica | OBL-PRIN-02 | RECOMENDADA |
| P-MKT-01 | Si | Sitio web con captura de datos | Verificar que el sitio muestre el Aviso de Privacidad de forma accesible | - | - | OBL-AVISO-01 | IMPORTANTE |
| P-MKT-02 | Si | Uso de cookies en sitio web | Incluir seccion de cookies en el Aviso de Privacidad | Clausula de cookies | - | OBL-AVISO-03 | IMPORTANTE |
| P-MKT-03 | Si | Captura de datos via formularios web | Verificar que cada formulario muestre el aviso antes de enviar datos | - | - | OBL-AVISO-04 | IMPORTANTE |
| P-MKT-04 | Si | Marketing directo por correo o campanas | Habilitar mecanismo de baja/oposicion enlazado a ARCO-POL (lista de supresion) | - | - | OBL-ARCO-05 | IMPORTANTE |
| P-MKT-05 | Si | Atencion o marketing via WhatsApp Business | Confirmar con el proveedor si los datos se procesan fuera de El Salvador; registrar como transferencia "pendiente de confirmar" | - | - | OBL-TRANSF-01, OBL-TRANSF-03 | RECOMENDADA |
| P-MKT-06 | Si | Aplicacion movil propia | Verificar los permisos del dispositivo solicitados y su justificacion en el aviso | - | - | OBL-AVISO-01, OBL-PRIN-02 | IMPORTANTE |
| P-TEC-01 | Si | Uso de servicios en la nube | Completar el Catalogo de sistemas con cada proveedor cloud usado | - | - | OBL-DOC-02 | IMPORTANTE |
| P-TEC-02 | Si | Registro "pendiente de confirmar" en Transferencias | Confirmar el pais donde el proveedor almacena los datos y documentar la transferencia | - | - | OBL-TRANSF-01, OBL-TRANSF-03, OBL-TRANSF-05 | CRITICA |
| P-TEC-02 | No lo se | Registro "pendiente de confirmar" en Transferencias | Solicitar al proveedor confirmacion escrita de la ubicacion de sus servidores | - | - | OBL-TRANSF-01, OBL-TRANSF-03 | IMPORTANTE |
| P-TEC-03 | Si | Encargados del tratamiento | Registrar el proveedor en Proveedores y Encargados y verificar contrato/DPA vigente | Plantilla de DPA | - | OBL-PROV-01, OBL-PROV-02, OBL-PROV-03 | CRITICA |
| P-TEC-04 | Si o No lo se | - | Confirmar con el proveedor si subcontrata a otros proveedores (subencargados) y documentar la cadena | - | - | OBL-PROV-05 | RECOMENDADA |
| P-SEN-01 | Cualquier categoria marcada | Tratamiento de dato sensible especifico (categoria marcada) | Confirmar base juridica reforzada (consentimiento por escrito) para cada categoria marcada | - | EIPD recomendada | OBL-SENS-01, OBL-CONS-04 | CRITICA |
| P-SEN-02 | Si | Tratamiento de datos geneticos | Elaborar EIPD para el tratamiento de datos geneticos | - | EIPD obligatoria (alto riesgo) | OBL-DOC-03, OBL-SENS-04 | CRITICA |
| P-MEN-01 | Si | Tratamiento de datos de ninas, ninos o adolescentes | Activar el subflujo de consentimiento parental (MOD-007) | Aviso adaptado a menores | - | OBL-PRIN-04, OBL-CONS-06 | CRITICA |
| P-MEN-02 | Si | - | Revisar con asesoria legal el mecanismo de verificacion de edad y consentimiento parental aplicable | - | Nota de advertencia: tension LPDP / Ley Crecer Juntos, requiere asesoria legal | OBL-CONS-06 | CRITICA |
| P-VID-01 | Si | Videovigilancia | Verificar senalizacion visible y aviso de privacidad de videovigilancia | - | - | OBL-SENS-08, OBL-AVISO-04 | IMPORTANTE |
| P-VID-02 | Si | Videovigilancia con reconocimiento facial (dato sensible biometrico) | Elaborar EIPD para el reconocimiento facial | - | EIPD obligatoria | OBL-SENS-06, OBL-SENS-08, OBL-DOC-03 | CRITICA |
| P-VID-03 | Si | Biometria de clientes o publico general | Registrar consentimiento por escrito y ofrecer alternativa no biometrica al publico | - | EIPD recomendada | OBL-SENS-06, OBL-SENS-07 | CRITICA |
| P-TRF-01 | Si | Registro de transferencia internacional | Registrar la transferencia (o como pendiente de confirmar en el MVP) con base juridica y evidencia de puesta en conocimiento a la ACE | - | - | OBL-TRANSF-01, OBL-TRANSF-03, OBL-TRANSF-04, OBL-TRANSF-05, OBL-TRANSF-06 | CRITICA |
| P-TRF-02 | Si | Transferencia intragrupo | Documentar la transferencia igual que a un tercero, salvo excepcion de integracion economica centroamericana | - | - | OBL-TRANSF-01, OBL-TRANSF-02, OBL-TRANSF-03 | IMPORTANTE |
| P-TRF-03 | Si | - | No enviar datos personales al extranjero sin verificar primero base juridica y consentimiento previo del titular | - | Alerta de riesgo alto | OBL-TRANSF-04 | CRITICA |
| P-SEG-01 | No | - | Definir un responsable de administracion de accesos a los sistemas con datos personales | - | - | OBL-SEG-02 | IMPORTANTE |
| P-SEG-02 | No o No lo se | - | Evaluar la implementacion de autenticacion de dos factores en sistemas con datos personales | - | - | OBL-SEG-03 | IMPORTANTE |
| P-SEG-03 | No o No lo se | - | Confirmar y documentar la politica de respaldo de informacion | - | - | OBL-SEG-03 | IMPORTANTE |
| P-SEG-04 | Si | - | Evaluar de inmediato, con apoyo del Delegado, si el hecho declarado activa el flujo de Incidentes y sus plazos de notificacion | - | Alerta CRITICAL inmediata (posible plazo de 72 horas ya vencido) | OBL-INC-01, OBL-INC-02, OBL-INC-04 | CRITICA |
| P-GOB-01 | No | - | Designar formalmente un Delegado de Proteccion de Datos o responsable interno y comunicarlo a la ACE en 15 dias habiles | - | - | OBL-DPO-01, OBL-DPO-03 | CRITICA |
| P-GOB-02 | No | - | Elaborar la Politica de Proteccion de Datos / Politica de Privacidad | Plantilla de Politica de Privacidad | - | OBL-AVISO-05, OBL-SEG-02 | CRITICA (plazo OBL-PLAZO-03 vencido) |
| P-GOB-03 | No | - | Elaborar y publicar el Aviso de Privacidad con los 9 literales del Art. 24 | Plantilla de Aviso de Privacidad | - | OBL-AVISO-01, OBL-PLAZO-04 | CRITICA (plazo vencido 23-may-2025) |
| P-GOB-04 | Si | - | Revisar de inmediato si existe una solicitud ARCO-POL pendiente fuera de plazo y regularizarla con apoyo de asesoria legal | - | Alerta CRITICAL | OBL-ARCO-08, OBL-ARCO-10, OBL-DOC-01 | CRITICA |
| P-EMP-01 | Salud | Prestacion de servicios de salud | - | - | EIPD recomendada | OBL-SENS-04 | IMPORTANTE |
| P-EMP-08 | Si | - | Confirmar si cada sucursal comparte el mismo Aviso de Privacidad o requiere uno propio | - | - | Buena practica | RECOMENDADA |
| P-PER-02 | Mayor o igual al umbral configurado (propuesta inicial 50) | - | Activar la recomendacion de separacion de funciones (Aprobador distinto de Auditor) | - | - | Buena practica, `05_tipos_de_usuario.md` 5.4 | RECOMENDADA |

Nota de dependencias: aunque varias tareas de esta tabla mencionan Proveedores (MOD-009), Transferencias (MOD-010), Incidentes (MOD-013), Controles de Seguridad (MOD-015), Delegado (MOD-002), Capacitacion (MOD-017) o Centro Regulatorio (MOD-024), el Diagnostico no escribe directamente en esos modulos: su unica salida transversal de "tarea" es siempre hacia el Centro de Tareas (MOD-021), y es la persona que completa esa tarea quien, al entrar al modulo correspondiente, deja el registro final alli. Esto respeta exactamente la lista de dependencias declarada en `06_mapa_definitivo_de_modulos.md` y en `mapa_modulos.json` (el diagnostico solo alimenta a MOD-005, MOD-006, MOD-008, MOD-014 y MOD-021) sin inventar enlaces directos adicionales.

### G.3 Automatizaciones generales de la sesion

| Disparador | Condicion | Accion | Configurable por la empresa |
|---|---|---|---|
| Cambio de respuesta antes del cierre | La pregunta ya tenia una respuesta previa | Guarda ambos valores en el historial (anterior y nuevo), no sobrescribe silenciosamente | No |
| Todos los bloques obligatorios completos | - | Calcula el resultado preliminar y pasa a Pendiente de cierre | No |
| Cierre confirmado | - | Genera en un solo paso todos los tratamientos, tareas, documentos y evaluaciones de la seccion G.2 que aplican | No |
| Sesion en Guardado parcial por mas de 15 dias | Configurable | Envia recordatorio (ver seccion I) | Si, el numero de dias |
| Diagnostico cerrado hace mas de 12 meses sin re-diagnostico | Configurable | Sugiere iniciar un re-diagnostico periodico | Si, la periodicidad |
| Activacion del estado FUTURO de la reforma 659 en MOD-024 | La organizacion tiene un diagnostico cerrado con P-GOB-01 respondida bajo el estado ACTUAL | Marca las tareas relacionadas con OBL-DPO-01/03 como "revisar bajo el nuevo estado regulatorio, ver historial", nunca las elimina | No (principio 8 de `06_mapa_definitivo_de_modulos.md`) |

---

## H. Decisiones que NO debe automatizar

- **Si una exclusion del Art. 3 aplica de forma definitiva.** El sistema solo marca la posibilidad (seccion G.1); confirmar que una empresa realmente esta fuera del ambito de la ley es una conclusion juridica. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada". Razon: excluir por error a un tratamiento del alcance del diagnostico deja a la empresa sin las tareas que en realidad necesitaba.
- **Si una base juridica distinta del consentimiento (contrato, obligacion legal, interes legitimo, etc.) es defendible para un tratamiento concreto detectado en el diagnostico.** El sistema solo registra la base elegida y muestra la nota de riesgo cuando existe ambiguedad conocida (por ejemplo la tension entre el Art. 5 lit. c y el Art. 5 lit. g descrita en `03_hallazgos_regulatorios.md`, seccion 8.1). Razon: es una decision de la empresa, expresamente reservada por decision 2.7.6 de `02_validacion_de_la_idea.md`.
- **Si un proveedor o servicio fuera de El Salvador constituye "transferencia" o "flujo transfronterizo del encargado".** La propia investigacion juridica deja esta distincion sin resolver (incertidumbre 10 de `03_hallazgos_regulatorios.md`, seccion 9); el sistema aplica por defecto la lectura conservadora (tratarlo como transferencia, ver decision 2.7.9), pero la clasificacion final requiere confirmacion humana.
- **Si la calificacion de "operador de infraestructura critica" aplica a la empresa.** Es una facultad exclusiva de la ACE (Art. 8 lit. f Decreto 143); el sistema solo crea la tarea de confirmarlo.
- **La determinacion final de si un tratamiento requiere EIPD obligatoria u obligatoria por escala/alto riesgo, mas alla de los disparadores tasados de la seccion G.2.** El calculo de riesgo lo hace MOD-014, pero la conclusion juridica sobre la necesidad de la evaluacion siempre requiere aprobacion humana, nunca es automatica (`04_objetivo_exacto_del_producto.md`, seccion 1.2).
- **Si la tension entre la LPDP (consentimiento parental, Art. 56 lit. c num. 3) y la Ley Crecer Juntos (adolescentes de 12 a 18 anos pueden consentir solos ciertas publicaciones de imagen) se resuelve de una forma u otra para el caso de la empresa (P-MEN-02).** Es la incertidumbre 8 de `03_hallazgos_regulatorios.md`, seccion 9; requiere criterio de abogado.
- **Cualquier respuesta que el sistema clasifique como CRITICA no cierra automaticamente el diagnostico sin la segunda confirmacion descrita en la seccion C.** El cierre en si mismo (que las tareas se activen) es automatico una vez confirmado, pero la confirmacion humana previa nunca se omite cuando hay una accion CRITICA.

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Diagnostico nunca iniciado tras onboarding | Onboarding (MOD-003) completado hace mas de 7 dias sin sesion iniciada | WARNING | Administrador | Plataforma + correo | Una vez, luego semanal | A Delegado si pasan 21 dias | Se inicia la sesion |
| Sesion en Guardado parcial estancada | Sin actividad en la sesion por mas del umbral configurado (por defecto 15 dias) | WARNING | Quien tiene el bloque asignado, Administrador | Plataforma + correo | Semanal | A Delegado a los 30 dias | Se retoma o se cierra la sesion |
| Resultado con acciones criticas pendientes de asignar | Sesion cerrada con al menos una accion CRITICA sin tarea asignada en MOD-021 | HIGH | Delegado / responsable interno | Plataforma + correo | Diaria mientras persista | A Administrador a los 5 dias | Todas las acciones criticas quedan asignadas con responsable y fecha en MOD-021 |
| Posible incidente no reportado detectado (P-SEG-04 = Si) | Cierre de sesion con esa respuesta | CRITICAL | Delegado, Responsable de Seguridad/IT | Plataforma + correo inmediato | Inmediata, una vez | A Administrador de forma inmediata (no espera plazo) | Se crea y avanza el expediente correspondiente en Incidentes de Seguridad (MOD-013) |
| Solicitud ARCO-POL previa sin gestionar (P-GOB-04 = Si) | Cierre de sesion con esa respuesta | CRITICAL | Delegado, Responsable ARCO-POL | Plataforma + correo inmediato | Inmediata, una vez | A Legal/Compliance de forma inmediata | Se registra formalmente el caso en ARCO-POL (MOD-011) o se documenta por que no aplica |
| Re-diagnostico recomendado por antiguedad | Diagnostico cerrado hace mas de 12 meses (configurable) sin re-diagnostico | INFO | Administrador, Delegado | Plataforma | Una vez al cumplirse el plazo | No escala | Se inicia un re-diagnostico |
| Cambio de estado regulatorio (reforma 659) con diagnostico cerrado bajo el estado anterior | MOD-024 activa el estado FUTURO | WARNING | Delegado / responsable interno | Plataforma + correo | Una vez | A Administrador a los 10 dias | Las tareas afectadas se revisan y quedan marcadas segun el nuevo estado |

---

## J. Evidencia

| Evidencia | Como se genera | Que prueba (OBL-ID) | Retencion |
|---|---|---|---|
| Registro de cada respuesta (pregunta, valor, usuario, fecha, version del cuestionario) | Automatico en cada respuesta guardada | OBL-AMB-01 a 04 (analisis de aplicabilidad documentado); colabora con OBL-PRIN-03 (responsabilidad demostrada, propietario MOD-019) | Igual que el expediente de cumplimiento de la organizacion; el criterio de retencion documental lo fija MOD-016 |
| Historial de cambios de una respuesta (valor anterior, valor nuevo, quien, cuando, motivo si se reabre) | Automatico cuando se reabre y corrige una sesion | OBL-PRIN-03 | Igual que el registro de respuestas, nunca se sobrescribe |
| Confirmacion de cierre con identidad y fecha (y segunda confirmacion cuando aplica doble control) | Automatico al confirmar el cierre | OBL-PRIN-03 | Igual que el registro de respuestas |
| Resultado del diagnostico en el momento del cierre (nivel de madurez y conteo, "fotografia" de ese momento) | Automatico al cerrar | OBL-AMB-01 a 04; base de partida de MOD-005 | Se conserva junto con cada version de la sesion, incluidas las archivadas por re-diagnostico |
| Version comparativa entre diagnosticos sucesivos | Automatico cuando existe mas de una sesion cerrada | Apoya OBL-PRIN-03 al mostrar evolucion del programa | Igual que las sesiones que compara |

Todo lo anterior se consulta desde el Centro de Evidencias (MOD-019) por referencia, sin duplicar el dato: MOD-019 no copia las respuestas del diagnostico, solo enlaza al registro que vive en MOD-004.

---

## K. Documentos asociados

- **Documentos requeridos como entrada:** ninguno. El diagnostico no exige adjuntar ningun documento externo para completarse; es un cuestionario de autoevaluacion.
- **Documentos generados directamente por este modulo:** ninguno. El diagnostico nunca redacta un documento legal por si mismo; solo sugiere cual falta y en que modulo iniciarlo (columna "Documento sugerido" de la seccion G.2).
- **Plantillas que el sistema provee (viven y se editan en MOD-008, el diagnostico solo las sugiere):**
  - "Aviso de Privacidad" (variables: razon social, finalidades detectadas, encargados detectados, canal ARCO-POL). Requiere validacion de la organizacion antes de publicarse.
  - "Politica de Proteccion de Datos / Politica de Privacidad" (variables: alcance, roles designados). Requiere validacion de la organizacion.
  - "Clausula de cookies" (variable: lista de herramientas de rastreo detectadas). Requiere validacion de la organizacion.
  - "Aviso especifico de biometria laboral" y "Aviso adaptado a menores" (variables segun el tratamiento detectado). Requieren validacion de la organizacion y, en el caso de menores, nota explicita de asesoria legal (ver seccion H).
- **Anexos y evidencias documentales:** el reporte de resultado exportado (ver seccion N) puede adjuntarse como anexo a la primera version del expediente de cumplimiento de la organizacion.

---

## L. Dependencias

```
   MOD-003 Onboarding
        |
        v
   MOD-004 Diagnostico de Cumplimiento  <-- (precarga sector/sucursales desde MOD-001, via MOD-003)
        |         |          |            |
        v         v          v            v
   MOD-005    MOD-006    MOD-008      MOD-014
   Plan de    RAT y      Documentos   Riesgos
   Cumpl.     Mapa       y Politicas  y EIPD
        \         \__________|____________/
         \                   |
          \                  v
           +------------> MOD-021 Centro de Tareas
```

- **Entra desde:** MOD-003 Onboarding (dispara el diagnostico al finalizar el alta de organizacion, usuarios y roles). De forma indirecta, MOD-001 (sector, sucursales) llega ya precargado a traves de MOD-003.
- **Sale hacia:** MOD-005 Plan de Cumplimiento (el resultado siembra el ordenamiento inicial de acciones), MOD-006 RAT y Mapa de Datos (siembra tratamientos), MOD-008 Documentos y Politicas (sugiere documentos a iniciar), MOD-014 Riesgos y EIPD (sugiere evaluaciones), MOD-021 Centro de Tareas (crea las tareas concretas).
- **Catalogos que comparte:** el catalogo de sectores/giro (P-EMP-01) es el mismo catalogo que usa MOD-001; el catalogo de categorias de datos sensibles (P-SEN-01) es el mismo catalogo compartido con MOD-006 y MOD-015 descrito en el anti-feature 23.
- **Que ocurre si un modulo dependiente no existe todavia en el MVP:** MOD-014 (Riesgos y EIPD) es SHOULD HAVE; mientras no este activo, el diagnostico igual crea la tarea "elaborar EIPD" en MOD-021 con una plantilla generica en MOD-008, sin motor de scoring (patron ya documentado en la ficha resumida de MOD-014, seccion 3 de `06_mapa_definitivo_de_modulos.md`). Lo mismo aplica a MOD-010 Transferencias Internacionales (tambien SHOULD HAVE): mientras no este completo, el diagnostico crea el registro "pendiente de confirmar" como tarea manual en MOD-021 en vez de una ficha formal de transferencia.

---

## M. Dashboard

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Diagnosticos completados vs. organizaciones activas | Sesiones en estado Cerrado / total de organizaciones con Onboarding completo | Verde si 100%, amarillo si hay sesiones en Guardado parcial, rojo si hay organizaciones sin iniciar | Gerencia (vision general), Administrador |
| Avance del diagnostico en curso | Preguntas respondidas / preguntas obligatorias visibles segun dependencias | Barra de progreso, sin semaforo | Responsable (quien esta completando su bloque) |
| Acciones criticas abiertas generadas por el diagnostico | Conteo de la seccion E.1 con estado distinto de Completada en MOD-021 | Rojo si mayor a 0, verde si 0 | Legal/Delegado, Gerencia |
| Acciones importantes y recomendadas abiertas | Igual que el anterior, para esas dos categorias | Amarillo / gris | Responsable, Legal/Delegado |
| Nivel de madurez inicial de la organizacion | Regla de la seccion E.1 | Rojo (Inicial), amarillo (En desarrollo), verde (En consolidacion) | Gerencia, Legal/Delegado |
| Dias desde el ultimo diagnostico cerrado | Fecha actual menos fecha de cierre de la ultima sesion | Verde si menor al ciclo configurado, amarillo si se acerca, rojo si lo supero | Administrador, Delegado |

Todos los indicadores usan el lenguaje de estado del programa definido en `04_objetivo_exacto_del_producto.md` (madurez, controles configurados, tareas pendientes, evidencia disponible); ninguno se expresa como "porcentaje de cumplimiento legal".

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Resultado del diagnostico | Respuestas por bloque, nivel de madurez, conteo de acciones por prioridad, fecha y responsables | Por sesion, por bloque | PDF | Administrador, Delegado, Gerencia | Si, con mecanismo de verificacion de integridad (hash) al exportarse, siguiendo la decision 2.7.24 |
| Historial comparativo de diagnosticos | Evolucion del nivel de madurez y del conteo de acciones entre sesiones sucesivas de la misma organizacion | Por rango de fechas | PDF, XLSX | Delegado, Auditor interno | Si |
| Detalle de disparadores activados | Lista completa de las filas de la seccion G.2 que se activaron en una sesion, con su OBL-ID y modulo de destino | Por sesion, por prioridad | XLSX, CSV | Legal/Compliance, Auditor externo (en auditoria puntual) | Si |

---

## O. Historial

Eventos que quedan en el historial del modulo (y se reflejan en la auditoria transversal, propietaria de MOD-018/MOD-019):

- Creacion de la sesion (organizacion, usuario, fecha, version del cuestionario, motivo).
- Cada respuesta guardada (pregunta, valor, usuario, fecha).
- Cada cambio de una respuesta antes del cierre (valor anterior, valor nuevo, usuario, fecha, motivo si se reabrio).
- Asignacion de un bloque a un responsable (quien asigna, a quien, fecha).
- Cambios de estado (En progreso, Guardado parcial, Pendiente de cierre, Cerrado, Re-diagnostico abierto, Archivado), con usuario y fecha.
- Confirmaciones de cierre (identidad, fecha, y segunda confirmacion cuando aplica doble control).
- Generacion de tratamientos, tareas, documentos y evaluaciones sugeridas al cerrar (lista completa de lo generado, con referencia a cada registro creado en el modulo destino).
- Exportaciones del resultado (quien, cuando, formato).
- Accesos de lectura al resultado por parte de Auditor externo o Asesor externo invitado (registro reforzado por tratarse de un rol externo).
- Archivado de una sesion por re-diagnostico (nunca eliminacion; motivo del re-diagnostico).

Todo el historial es de solo escritura por adicion (append-only): ningun rol, incluido Administrador, puede editar o borrar un evento ya registrado (anti-feature 19 de `22_anti_features.md`).

---

## P. Riesgos

- **Riesgo legal: dar por valida una exclusion del Art. 3 sin suficiente analisis.** Mitigacion de diseno: las reglas de exclusion (seccion G.1) nunca cierran el diagnostico automaticamente ni desactivan preguntas por si solas; siempre generan una advertencia visible y exigen confirmacion de Legal/Compliance antes de excluir cualquier tratamiento del alcance.
- **Riesgo legal: que una empresa interprete el nivel de madurez o el conteo de acciones como una certificacion de cumplimiento.** Mitigacion de diseno: todo panel de resultado incluye el texto de descargo fijo de `04_objetivo_exacto_del_producto.md`, seccion 1.3, y el modulo nunca usa la palabra "cumplimiento" seguida de un porcentaje.
- **Riesgo de UX: abandono del cuestionario por su extension (47 preguntas en 11 bloques).** Mitigacion de diseno: guardar y continuar en cualquier punto, asignacion de bloques por responsable de area (para que ninguna persona conteste sola las 47 preguntas), lenguaje simple con ejemplos en cada pregunta, y barra de progreso por bloque en vez de un formulario unico largo.
- **Riesgo de UX: que una pregunta de dependencia condicional quede oculta y la empresa nunca declare un tratamiento relevante (por ejemplo P-PER-04 sobre biometria, que solo aparece si P-PER-03 fue Si).** Mitigacion de diseno: las preguntas base de cada bloque (P-PER-03, P-VID-01, P-TEC-01, P-TEC-03, etc.) estan formuladas de forma amplia a proposito, para minimizar el riesgo de que una empresa responda "No" a la pregunta base cuando en realidad si aplica.
- **Riesgo operativo: que el catalogo de preguntas quede desactualizado frente a un cambio normativo (por ejemplo la reforma 659) y el bloque Gobernanza siga preguntando por un Delegado obligatorio cuando ya no lo es.** Mitigacion de diseno: la version del cuestionario queda registrada en cada sesion (seccion D.1) y el cambio de estado en MOD-024 dispara la automatizacion de la seccion G.3 que revisa, sin eliminar, las tareas afectadas.
- **Riesgo operativo: doble conteo de acciones cuando dos preguntas distintas apuntan al mismo tratamiento (por ejemplo biometria de personal y biometria de publico general).** Mitigacion de diseno: la regla de fusion de disparadores descrita en la seccion E.1.
- **Riesgo de seguridad y privacidad: que las respuestas del bloque Datos sensibles, Menores o Seguridad (que revelan informacion operativa sensible de la propia empresa, no de un titular, pero igual delicada) queden visibles para roles que no las necesitan.** Mitigacion de diseno: la tabla de permisos de la seccion C limita la vista completa a Administrador, Delegado y Legal/Compliance, y restringe a los demas roles a solo su bloque asignado (marca P en la tabla).
- **Riesgo de seguridad: exportacion del resultado sin garantia de integridad.** Mitigacion de diseno: todo reporte exportado incluye el mecanismo de verificacion de integridad exigido por la decision 2.7.24 (ver seccion N).

---

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Cuestionario completo de 11 bloques y 47 preguntas, con dependencias | X | | | | Es el mecanismo concreto para identificar exposicion legal; el plazo de adecuacion a las Politicas ACE ya vencio (OBL-PLAZO-03) |
| Deteccion de exclusiones del Art. 3 (seccion G.1) | X | | | | Evita sobre-obligar a empresas parcialmente excluidas; decision 2.7.27 |
| Motor de disparo (tratamiento + tarea + documento + riesgo, seccion G.2) | X | | | | Es la propuesta de valor central del producto: convierte obligacion en accion gestionable |
| Guardar y continuar | X | | | | Sin esto el riesgo de abandono (seccion P) compromete la adopcion del diagnostico completo |
| Calculo de nivel de madurez inicial y conteo de acciones por prioridad | X | | | | Es la salida que alimenta directamente a MOD-005 (dependencia estructural de un modulo MUST HAVE) |
| Diagnostico repetible (re-diagnostico por cambio de actividad) | X | | | | Es una propiedad estructural del modelo de datos, no una capa adicional (decision 2.7.5) |
| Asignacion de bloques a distintos responsables de area | | X | | | Mejora la adopcion en empresa mediana/corporativa; en pyme una sola persona puede responder todo sin esta funcion |
| Exportacion del resultado en PDF con verificacion de integridad | | X | | | Necesaria para auditoria y ACE, pero no bloquea el primer uso del diagnostico |
| Historial comparativo entre diagnosticos sucesivos | | | X | | Utilidad de seguimiento, no bloquea ninguna obligacion legal mientras exista al menos una sesion cerrada |
| Comentarios en una pregunta especifica | | | X | | Mejora de colaboracion interna, postergable sin riesgo |
| Recomendaciones dinamicas basadas en benchmarking por sector | | | | X | Requiere una base de datos de multiples clientes por sector, no existe en el lanzamiento inicial |
| Reabrir automaticamente preguntas relacionadas cuando cambia una respuesta ya cerrada (recalculo retroactivo) | | | | X | Complejidad alta frente al valor incremental sobre el re-diagnostico manual ya disponible en MVP |

**Version minima vendible del modulo:** el cuestionario completo de 11 bloques con sus dependencias, la deteccion de exclusiones, el motor de disparo completo (seccion G.2), guardar y continuar, y el calculo de resultado. Esta combinacion ya resuelve la pregunta rectora del producto (que le aplica a esta empresa y que debe hacer primero) sin depender de ninguna funcionalidad SHOULD HAVE o posterior. Asignar bloques por responsable y exportar con integridad pueden llegar en una iteracion inmediatamente posterior sin bloquear el primer diagnostico de un cliente real.

---

## R. Ayuda contextual (complemento obligatorio)

**Que es el Diagnostico de Cumplimiento**
- Que es: un cuestionario guiado que le pregunta, en lenguaje simple, como opera su empresa (si tiene empleados, camaras, sitio web, proveedores, etc.) para saber que le exige la ley de proteccion de datos.
- Por que tengo que hacer esto: sin este paso, el sistema no sabe que modulos activar para su empresa ni que tareas asignarle.
- Fundamento: analisis de aplicabilidad de la Ley para la Proteccion de Datos Personales, OBL-AMB-01 a 04, Art. 2 y 3 del Decreto Legislativo 144.
- Cuando necesito ayuda juridica: cuando el sistema le muestre una advertencia de posible exclusion (por ejemplo por ser una entidad supervisada por la SSF o por seguridad publica), consulte a su area legal antes de dar por cerrado ese tema.

**Que es una exclusion del Art. 3**
- Que es: son los pocos casos donde la ley misma dice que no aplica: reporte de historial crediticio bajo su ley especial, uso estrictamente domestico sin fin comercial, o actividades de seguridad publica y registros oficiales.
- Por que tengo que hacer esto: para que el sistema no le pida cumplir con obligaciones que realmente no le corresponden, pero tambien para no asumir por error que su empresa esta exenta cuando no lo esta.
- Fundamento: OBL-AMB-02, OBL-AMB-03, OBL-AMB-04, Art. 3 lit. a, b, c y d.
- Cuando necesito ayuda juridica: siempre que el sistema marque una posible exclusion; ninguna exclusion se confirma sin que su area legal o un asesor externo la revise.

**Que es un dato personal sensible**
- Que es: un tipo de dato que, por su naturaleza, tiene proteccion reforzada: salud, biometria (huella, reconocimiento facial), origen etnico, opiniones politicas, convicciones religiosas, orientacion sexual, afiliacion sindical y datos geneticos, entre otros.
- Por que tengo que hacer esto: la ley exige un consentimiento reforzado (por escrito) para tratar estos datos, y su omision es una de las infracciones mas graves del catalogo.
- Fundamento: OBL-SENS-01, Art. 4 lit. g y Art. 59 lit. b; OBL-CONS-04, Art. 26 inc. 4.
- Cuando necesito ayuda juridica: cuando su empresa trata datos geneticos, de salud o biometria de forma habitual; el sistema le sugerira una evaluacion de impacto (EIPD), pero la decision final de como implementarla requiere asesoria especializada.

**Que es una transferencia internacional de datos**
- Que es: cuando los datos personales que su empresa trata se envian, almacenan o procesan fuera de El Salvador, incluso si es solo un respaldo en la nube de un proveedor extranjero.
- Por que tengo que hacer esto: la ley exige informar al titular, obtener su consentimiento previo (salvo excepciones) y poner el flujo en conocimiento de la ACE.
- Fundamento: OBL-TRANSF-01 a 06, Art. 40, 41, 44 y 45.
- Cuando necesito ayuda juridica: cuando no este segura de si su proveedor tecnologico cuenta como "transferencia" o como "encargado extranjero"; esta distincion no esta resuelta de forma expresa en la ley (ver `03_hallazgos_regulatorios.md`, seccion 9, incertidumbre 10) y el sistema aplica por defecto el criterio mas conservador.

**Por que me preguntan sobre menores, biometria o videovigilancia**
- Que es: son tres de los tratamientos que la ley y las autoridades consideran de mayor riesgo, con reglas especiales propias (consentimiento parental, alternativa no biometrica, senalizacion y evaluacion de impacto).
- Por que tengo que hacer esto: si su empresa hace alguno de estos tratamientos sin las medidas reforzadas correspondientes, el riesgo de una infraccion grave o muy grave es mayor que en un tratamiento ordinario.
- Fundamento: OBL-PRIN-04 y OBL-CONS-06 (menores, Art. 5 lit. j y Art. 56 lit. c num. 3); OBL-SENS-06 y OBL-SENS-07 (biometria, Art. 4 lit. g, Art. 26 inc. 4 y Art. 37); OBL-SENS-08 (videovigilancia, Art. 4 lit. f y g, Art. 7, Art. 12 lit. b).
- Cuando necesito ayuda juridica: en menores, siempre que el sistema le indique la tension entre la LPDP y la Ley Crecer Juntos; en biometria y videovigilancia con reconocimiento facial, antes de implementar el tratamiento si aun no lo tiene en marcha.

---

## Nota final: observaciones y posibles desacuerdos con las fuentes de diseno

1. **Numero de preguntas.** El instructivo pide un minimo de 40 preguntas; esta ficha define 47, agrupadas en los 11 bloques exigidos. No se detecto contradiccion con `06_mapa_definitivo_de_modulos.md` ni con `mapa_modulos.json`: ambos documentos dejan el contenido detallado del cuestionario como pendiente de que la ficha del modulo lo desarrolle.
2. **Aclaracion de dependencias, no error.** Varias filas de la tabla de disparadores (seccion G.2) mencionan modulos que no aparecen en la lista oficial de "alimenta_a" de MOD-004 (por ejemplo MOD-002, MOD-009, MOD-010, MOD-013, MOD-015, MOD-017, MOD-024). Esto no contradice el mapa: en todos los casos la salida real del diagnostico sigue siendo exclusivamente una tarea en MOD-021 (que si esta en la lista); esa tarea simplemente describe, en su texto, en que otro modulo debera completarse el registro final cuando la persona responsable la ejecute. Se deja explicito en la nota al pie de la seccion G.2 para que no se lea como una desviacion del mapa definitivo.
3. **Posible falta menor detectada.** `02_validacion_de_la_idea.md`, hallazgo de prioridad baja 24, senala la deteccion de "operador de infraestructura critica" como necesidad de negocio ligada a OBL-INC-05, sugerida para el bloque de Onboarding. Esta ficha la ubica en el bloque Empresa del Diagnostico (pregunta P-EMP-07) en lugar de en MOD-003 Onboarding, porque el Diagnostico es el modulo que ya concentra todas las preguntas de aplicabilidad normativa y porque MOD-003, segun su propia ficha en `06_mapa_definitivo_de_modulos.md`, no tiene obligaciones propias ni esta disenado para preguntas de fondo. Se senala aqui por transparencia, no como un error de las fuentes, sino como una decision de ubicacion que un revisor podria querer confirmar.
4. **Ninguna obligacion de la matriz fue inventada.** Todos los OBL-ID citados en este documento fueron verificados contra `01_legal/matriz_obligaciones.json` antes de usarse; donde una obligacion es CONDICIONAL o RECOMENDADA, la tabla de disparadores lo refleja en la columna Prioridad (RECOMENDADA) en vez de tratarla como si fuera OBLIGATORIO.
