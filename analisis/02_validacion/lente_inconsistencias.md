# Lente de inconsistencias del documento maestro (seccion 4.3)

Fecha de analisis: 2026-09-24.

Fuente analizada: `C:\Proyects\PRIV-SV\PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` (documento maestro, hipotesis de producto, no verdad establecida). Los numeros de seccion citados en cada hallazgo (por ejemplo "seccion 22") son los del documento maestro, no de este informe.

Base juridica de contraste: `C:\Proyects\PRIV-SV\analisis\01_legal\matriz_obligaciones.md` / `matriz_obligaciones.json` (105 obligaciones, IDs canonicos OBL-AREA-NN) y `C:\Proyects\PRIV-SV\analisis\01_legal\03_hallazgos_regulatorios.md` (secciones 3, 5, 6, 8 y 9).

Alcance: fase de analisis funcional. Este informe no propone codigo, SQL, APIs, stack ni infraestructura. Toda sugerencia de "resolucion propuesta" es una decision funcional de producto pendiente de validar con el equipo, no una obligacion legal, salvo cuando se cita un OBL-ID expreso.

Metodologia: se releyo el documento maestro completo (secciones 1 a 53) y se contrasto cada modulo, rol y proceso descrito contra la matriz de 105 obligaciones y contra las contradicciones y ambiguedades ya detectadas en la investigacion juridica (seccion 8 de `03_hallazgos_regulatorios.md`). Se identificaron 26 inconsistencias, agrupadas en las cinco categorias solicitadas.

---

## Resumen de hallazgos

| N. | Categoria | Titulo | Secciones del documento maestro |
|---|---|---|---|
| 1 | Modulos solapados | Inventario de datos vs RAT vs Mapa de datos | 13, 14 |
| 2 | Modulos solapados | Contratos/DPA vs Proveedores vs Transferencias | 22, 23, 24 |
| 3 | Modulos solapados | Riesgos/EIPD vs Controles de seguridad | 26, 27 |
| 4 | Modulos solapados | Evidencia (campo transversal) vs Auditoria (log) vs Paquete de evidencias | 16-27, 29, 30 |
| 5 | Modulos solapados | Onboarding vs Diagnostico inicial | 15 |
| 6 | Modulos solapados | Consentimiento vs Documentos/Avisos (version del aviso duplicada) | 19, 20 |
| 7 | Concepto ambiguo | Responsable de privacidad vs Delegado vs Responsable ARCO-POL | 3, 11, 12 |
| 8 | Concepto ambiguo | Contacto ARCO-POL (organizacion) vs rol Responsable ARCO-POL (usuarios) | 11, 12 |
| 9 | Concepto ambiguo | Encargado vs Proveedor vs Tercero/Receptor | 14, 22 |
| 10 | Concepto ambiguo | Transferencia internacional vs acceso del encargado extranjero | 22, 24 |
| 11 | Concepto ambiguo | Evidencia vs Documento vs Log de auditoria | 16, 20, 29, 30 |
| 12 | Proceso incompleto | ARCO-POL sin incompetencia, notificacion a receptores ni reclamo posterior | 17 |
| 13 | Proceso incompleto | Incidentes: computo de las 72 horas y revision interna sin diferenciar | 25 |
| 14 | Proceso incompleto | Revocacion del consentimiento sin flujo de doble plazo | 19 |
| 15 | Proceso incompleto | Retencion sin regla de conflicto entre bases simultaneas | 21 |
| 16 | Proceso incompleto | Aprobacion documental sin cadena configurable por tipo de documento | 20 |
| 17 | Dependencia no contemplada | Calendario de dias habiles tratado como detalle, no como dependencia central | 17, 25 |
| 18 | Dependencia no contemplada | Motor regulatorio y doble estado de la reforma 659 desconectados de los modulos operativos | 3, 40, 41 |
| 19 | Dependencia no contemplada | Catalogo de sistemas sin modulo propietario | 13, 14, 22, 25 |
| 20 | Dependencia no contemplada | Verificacion de identidad del titular no definida | 17, 18 |
| 21 | Dependencia no contemplada | Tramites y contacto ante la ACE no modelados | 11, 24 |
| 22 | Dependencia no contemplada | Principio "core vs regulatory pack" contradicho por reglas salvadorenas ya incrustadas en los modulos | 40 |
| 23 | Contradiccion interna | "No almacenar PII innecesariamente" vs expediente ARCO-POL, Portal, Incidentes y Consentimiento | 17, 18, 19, 25, 37 |
| 24 | Contradiccion interna | "No ser Delegado ni operador de ARCO-POL" vs automatizacion de actos legales del delegado | 3, 17 |
| 25 | Contradiccion interna | Capacitacion tratada como funcionalidad opcional a evaluar vs obligacion legal | 28 |
| 26 | Contradiccion interna | Integridad del log de auditoria (WORM/hash) vs paquete de evidencias exportable sin garantia de integridad | 29, 30 |

---

## A. Modulos repetidos o solapados

### 1. Inventario de datos vs RAT vs Mapa de datos

**Descripcion:** el documento maestro define "Inventario de datos" (seccion 13) y "Registro de Actividades de Tratamiento - RAT/ROPA" (seccion 14) como dos modulos separados que capturan casi los mismos campos por cada actividad: categoria/categorias de datos, origen, finalidad, titulares/categorias de titulares, sistema/sistemas, terceros, pais/paises, sensibilidad/datos sensibles, periodo de conservacion/retencion, medidas de seguridad/controles de seguridad. El documento no explica que informacion vive en Inventario que no viva ya en RAT, ni cual es la relacion entre ambos (uno alimenta al otro, o son bases de datos independientes).

**Donde aparece:** secciones 13 y 14.

**Por que es un problema:** dos modulos que describen la misma entidad conceptual (una actividad de tratamiento) obligan al usuario no especialista a capturar la misma informacion dos veces, con riesgo de que ambas copias diverjan. Ademas, ningun texto de la ley exige un "Inventario de datos" distinto del RAT; la unica exigencia documentada es el RAT (OBL-DOC-02, Art. 4 Medidas Organizativas lit. d, OBLIGATORIO). El "Mapa de datos" que pide el prompt de analisis funcional (origen -> sistema -> area -> proveedor -> pais -> eliminacion) tampoco existe como modulo propio en el documento maestro; el maestro no distingue si el mapa es una tercera base de datos o una vista.

**Resolucion propuesta:** fusionar Inventario de datos dentro del RAT como una unica fuente de verdad por tratamiento. Tratar el "Mapa de datos" como una visualizacion (vista de flujo origen-sistema-area-proveedor-pais-eliminacion) construida sobre los mismos registros del RAT, no como una tercera base de datos independiente. Esto es una decision de producto, no una exigencia legal expresa.

### 2. Contratos/DPA vs Proveedores vs Transferencias

**Descripcion:** el documento maestro define tres modulos separados que comparten el mismo nucleo de informacion. "Proveedores y terceros" (seccion 22) ya pide registrar contrato, DPA, paises, subencargados y evaluacion de riesgo por proveedor. "Contratos/DPA" (seccion 23) se presenta como un modulo aparte que almacena, versiona y genera borradores de los mismos contratos. "Transferencias internacionales" (seccion 24) vuelve a pedir proveedor, pais, contrato y evaluacion.

**Donde aparece:** secciones 22, 23 y 24.

**Fundamento legal relacionado:** OBL-PROV-01 a OBL-PROV-07 (proveedores/encargados, Arts. 33, 34, 36 LPDP) y OBL-TRANSF-01 a OBL-TRANSF-06 (Arts. 40, 41, 44, 45, 54 LPDP) son obligaciones distintas pero relacionadas: un proveedor-encargado no es automaticamente una transferencia (ver hallazgo 10 de este informe).

**Por que es un problema:** el mismo par proveedor-pais-contrato se documentaria en tres lugares distintos, sin que el documento maestro defina cual es la fuente de verdad de "el contrato" cuando Proveedores, Contratos/DPA y Transferencias apuntan al mismo documento. Esto multiplica el trabajo de captura para el usuario no especialista y genera riesgo de contratos desactualizados en un modulo mientras se actualizan en otro.

**Resolucion propuesta:** tratar "Contratos/DPA" como un tipo de documento dentro del modulo Proveedores (no como modulo independiente), y mantener Transferencias como modulo distinto pero enlazado por referencia al proveedor y al contrato ya registrados en Proveedores, sin duplicar los campos.

### 3. Riesgos/EIPD vs Controles de seguridad

**Descripcion:** "Riesgos/EIPD" (seccion 26) genera "medidas" como resultado de la evaluacion de riesgo. "Controles de seguridad" (seccion 27) registra practicamente el mismo tipo de objeto (aplicacion, sistema, responsable, evidencia, revision, vigencia, estado) desde un catalogo separado. El documento maestro no dice si la "medida" que sale de una EIPD es el mismo registro que un "control" del catalogo de seguridad, o si son dos objetos distintos que un usuario debe mantener sincronizados a mano.

**Donde aparece:** secciones 26 y 27.

**Fundamento legal relacionado:** OBL-DOC-03 (EIPD, Art. 4 Medidas Organizativas lit. e, OBLIGATORIO) y OBL-SEG-02/OBL-SEG-03 (medidas organizativas y tecnicas, Art. 4 Politicas ACE, OBLIGATORIO) son obligaciones relacionadas pero el maestro no articula su relacion funcional.

**Por que es un problema:** sin una relacion explicita, el usuario podria registrar una "medida" al cerrar una EIPD y, por separado, tener que volver a dar de alta el mismo control en el catalogo de seguridad para que aparezca en reportes y auditorias, duplicando esfuerzo y arriesgando inconsistencia entre "lo que la EIPD dijo que se haria" y "lo que el catalogo de controles dice que existe".

**Resolucion propuesta:** definir Control como una entidad unica y compartida; el modulo de EIPD selecciona controles existentes del catalogo o crea uno nuevo que queda dado de alta automaticamente en Controles de seguridad, en vez de mantener dos listas independientes de "medidas".

### 4. Evidencia (campo transversal) vs Auditoria (log) vs Paquete de evidencias

**Descripcion:** el documento maestro usa "evidencia" como campo suelto en casi todos los modulos (Centro de tareas seccion 16, ARCO-POL seccion 17, Consentimiento seccion 19, Politicas y documentos seccion 20, Incidentes seccion 25, Controles de seguridad seccion 27). Por separado define "Auditoria y trazabilidad" (seccion 29) como un log de acciones (append-only, WORM), y "Paquete de evidencias" (seccion 30) como una funcion de exportacion que junta RAT, politicas, solicitudes, incidentes, EIPD, proveedores, transferencias, capacitacion, controles, auditorias, logs y aprobaciones en PDF/XLSX/CSV/ZIP. El documento nunca define que es estructuralmente una "evidencia" (un archivo, una referencia, un hash, una entrada de log) ni como se relaciona con el log de auditoria y con el paquete exportable.

**Donde aparece:** secciones 16, 17, 19, 20, 25, 27, 29 y 30.

**Por que es un problema:** hay tres conceptos con el mismo nombre o proposito (evidencia como campo, evidencia como registro de auditoria, evidencia como paquete exportado) sin una definicion unica. Esto complica el diseno de un "Centro de evidencias" transversal (que el prompt de analisis funcional pide en su seccion 25) porque no queda claro sobre que datos deberia consultar: los campos "evidencia" sueltos de cada modulo, el log de auditoria, o ambos.

**Resolucion propuesta:** definir Evidencia como una entidad propia (archivo o referencia con metadatos, vinculada a un registro especifico como prueba de que algo ocurrio), distinta del AuditLog (registro de sistema de quien hizo que y cuando) y distinta del "Paquete de evidencias" (una vista de exportacion sobre Evidencia + AuditLog + Documentos, sin almacenamiento propio).

### 5. Onboarding vs Diagnostico inicial

**Descripcion:** la seccion 15 del documento maestro se titula "Onboarding / Compliance Wizard" pero mezcla dos cosas distintas bajo un mismo nombre: preguntas de configuracion inicial de la cuenta (implicito en el titulo "Onboarding") y un cuestionario regulatorio guiado (¿tiene camaras?, ¿usa biometria?, ¿procesa informacion medica?) que dispara tratamientos, tareas, riesgos, documentos y controles. El prompt de analisis funcional trata este segundo bloque como un modulo propio y mas profundo ("Diagnostico inicial", con arbol de decisiones y dependencias), distinto del registro de la empresa.

**Donde aparece:** seccion 15 (y, por comparacion, seccion 3 sobre el rol de las personas designadas por la empresa).

**Por que es un problema:** fusionar el alta de la cuenta (registrar organizacion, invitar usuarios) con el diagnostico regulatorio en un unico modulo dificulta responder preguntas de diseno basicas: ¿el diagnostico se repite periodicamente o solo una vez al inicio?, ¿se puede volver a ejecutar cuando la empresa cambia de actividad (por ejemplo, empieza a usar biometria)?, ¿el onboarding de un nuevo usuario dispara de nuevo el cuestionario? El documento maestro no distingue estos escenarios porque los trata como el mismo modulo.

**Resolucion propuesta:** separar en dos modulos nombrados de forma distinta: Onboarding (alta de organizacion, usuarios, roles - contenido de las secciones 11 y 12) y Diagnostico de cumplimiento (el cuestionario guiado que genera tratamientos/tareas/plan - contenido de la seccion 15 salvo el marco de alta de cuenta), dejando explicito si el diagnostico es repetible.

### 6. Consentimiento vs Documentos/Avisos (version del aviso duplicada)

**Descripcion:** "Consentimiento" (seccion 19) propone guardar, por cada registro de consentimiento, "version del aviso" y "texto" como campos propios. "Politicas y documentos" (seccion 20) ya gestiona el Aviso de Privacidad con su propio versionado, publicacion y vigencia. El documento maestro no dice si el campo "version del aviso" de Consentimiento es una copia independiente del texto o una referencia a la version publicada en Documentos.

**Donde aparece:** secciones 19 y 20.

**Fundamento legal relacionado:** OBL-CONS-05 (carga de la prueba del consentimiento y del aviso de privacidad, Art. 54 LPDP, OBLIGATORIO) exige poder demostrar exactamente que version del aviso vio el titular al consentir; una copia de texto libre en Consentimiento, separada del documento versionado oficial, debilita esa prueba si ambos textos llegan a divergir.

**Por que es un problema:** si Consentimiento guarda su propia copia del texto del aviso en vez de apuntar a la version exacta publicada en Documentos, existe riesgo de que la "prueba" del consentimiento no coincida con el aviso realmente vigente ese dia, lo que es justo el escenario que el Art. 54 busca evitar.

**Resolucion propuesta:** el registro de consentimiento debe referenciar (no copiar) la version especifica del documento "Aviso de Privacidad" gestionada en el modulo de Documentos, de modo que exista una unica fuente de verdad del texto mostrado.

---

## B. Conceptos ambiguos

### 7. Responsable de privacidad vs Delegado vs Responsable ARCO-POL

**Descripcion:** el modulo de organizacion (seccion 11) incluye "responsable de privacidad" como campo de contacto de la empresa. El modulo de usuarios y roles (seccion 12) define, ademas, "Responsable de privacidad" y "Responsable ARCO-POL" como dos roles distintos del sistema de permisos. En ningun lugar del documento maestro aparece la palabra "Delegado" como rol o campo, pese a que la seccion 3 dice expresamente que el proveedor del software no actuara como "Delegado de Proteccion de Datos del cliente", lo que da a entender que esa figura legal existe y la empresa debe nombrarla.

**Donde aparece:** secciones 3, 11 y 12.

**Fundamento legal relacionado:** OBL-DPO-01 (obligatoriedad de nombrar delegado en el sector privado, Arts. 15 y 17 LPDP, OBLIGATORIO mientras la reforma 659 no entre en vigencia) exige que exista, con nombre propio, la figura de "Delegado". Ademas, buena parte de los actos procedimentales de ARCO-POL (OBL-ARCO-08/09/11, Arts. 18, 19, 21) y del consentimiento (OBL-CONS-03, Art. 30) estan atribuidos por la ley literalmente a "el delegado", no a "el responsable" en general.

**Por que es un problema:** sin un rol explicito llamado "Delegado" mapeado 1 a 1 con los Arts. 15 y 17, el motor de tareas y plazos no tiene a quien asignar automaticamente las obligaciones que la ley atribuye a esa figura especifica (comunicacion a la ACE en 15 dias habiles, reverificacion cada 3 anos, capacitacion anual, confidencialidad de 5 anos tras el cese). "Responsable de privacidad" queda como una etiqueta ambigua que podria ser el Delegado, un coordinador interno distinto, o simplemente un sinonimo mal definido de "Responsable ARCO-POL".

**Resolucion propuesta:** crear un rol explicito "Delegado de Proteccion de Datos" (con campos de certificacion ACE segun los Lineamientos DPO), y mantener "Responsable ARCO-POL" como un rol operativo distinto que puede o no coincidir con la persona del Delegado (relevante sobre todo si la reforma 659 entra en vigencia y el tramite pasa al "sujeto obligado"). Eliminar o redefinir "Responsable de privacidad" para que no se superponga con ninguno de los dos.

### 8. Contacto ARCO-POL (organizacion) vs rol Responsable ARCO-POL (usuarios)

**Descripcion:** la seccion 11 (organizacion) incluye un campo "contacto ARCO-POL" como dato de la empresa, mientras que la seccion 12 (usuarios y roles) define "Responsable ARCO-POL" como un rol del sistema de permisos, con capacidad de accion sobre el modulo. El documento maestro nunca enlaza ambos: no dice si el "contacto ARCO-POL" publicado (por ejemplo, en el aviso de privacidad) debe ser necesariamente la misma persona que tiene asignado el rol operativo, o si son dos cosas independientes (un dato publico de contacto vs un permiso interno de sistema).

**Donde aparece:** secciones 11 y 12.

**Por que es un problema:** si son la misma persona, el sistema deberia sincronizar automaticamente el campo publicado en el aviso con el usuario que tiene el rol asignado (para que un cambio de responsable actualice ambos lugares). Si son conceptos distintos, el documento deberia decirlo para que el diseno no asuma erroneamente que son intercambiables.

**Resolucion propuesta:** definir explicitamente que "contacto ARCO-POL" es el dato publicado de cara al titular y que debe derivarse (no capturarse por separado) del usuario que tenga asignado el rol "Responsable ARCO-POL" activo en cada momento.

### 9. Encargado vs Proveedor vs Tercero/Receptor

**Descripcion:** el modulo "Proveedores y terceros" (seccion 22) agrupa bajo una sola etiqueta dos figuras legales distintas: el encargado del tratamiento (quien procesa datos por instruccion del responsable, Arts. 33-36) y el tercero o receptor (quien recibe datos y puede convertirse en un responsable independiente, Art. 41). El RAT (seccion 14), por su parte, lista "encargados", "terceros" y "destinatarios" como tres campos separados, sin que el documento maestro defina en ningun lugar la diferencia entre ellos ni como se relacionan con el modulo unico de "Proveedores y terceros".

**Donde aparece:** secciones 14 y 22.

**Fundamento legal relacionado:** OBL-PROV-01 a OBL-PROV-03 (Arts. 33, 34, 36, encargado sujeto a instrucciones y a las mismas medidas de seguridad) y OBL-TRANSF-02 (Art. 41, contrato con el responsable receptor) son obligaciones con requisitos distintos segun la figura de que se trate.

**Por que es un problema:** un usuario no especialista no puede saber, a partir del documento maestro, si debe dar de alta a un mismo tercero como "proveedor" o si corresponde otro tratamiento porque es un "receptor" que se convierte en responsable independiente. Esto afecta directamente que obligaciones se activan (por ejemplo, la notificacion a receptores del Art. 21 inc. 3, OBL-ARCO-11, solo aplica a "receptores", no a "encargados").

**Resolucion propuesta:** definir tres tipos de entidad distintos y explicitos (Encargado, Tercero/Receptor, Subencargado) con reglas propias de que obligaciones dispara cada uno, en lugar de un unico modulo "Proveedores y terceros" que los mezcla.

### 10. Transferencia internacional vs acceso del encargado extranjero

**Descripcion:** el modulo Proveedores (seccion 22) ya pide "paises" por proveedor, y el modulo Transferencias internacionales (seccion 24) vuelve a pedir "pais" de forma independiente, sin ninguna regla que distinga cuando un proveedor extranjero (por ejemplo, un encargado de nube fuera de El Salvador) debe registrarse ademas como una transferencia internacional formal.

**Donde aparece:** secciones 22 y 24.

**Fundamento legal relacionado:** esta es una ambiguedad ya identificada en la investigacion juridica (`03_hallazgos_regulatorios.md`, seccion 9, punto 10): la ley define "transferencia" (Art. 4 lit. u) excluyendo expresamente al encargado, pero las definiciones de emisor/receptor de los Arts. 44 y 45 (Art. 4 lit. k y o) si parecen incluirlo, por lo que no esta resuelto si un encargado extranjero (nube, SaaS) debe tratarse como transferencia sujeta a los Arts. 44-45 (consentimiento previo, puesta en conocimiento de la ACE) o solo como un proveedor con pais registrado.

**Por que es un problema:** sin una regla de producto explicita, el sistema podria dejar de activar obligaciones como OBL-TRANSF-04 (consentimiento previo, Art. 44 inciso final, OBLIGATORIO) u OBL-TRANSF-05 (puesta en conocimiento a la ACE, Art. 45, OBLIGATORIO) para relaciones con proveedores extranjeros que en la practica funcionan como flujo transfronterizo de datos.

**Resolucion propuesta (decision de producto, no conclusion juridica):** que todo proveedor/encargado ubicado fuera de El Salvador genere automaticamente un registro vinculado en Transferencias marcado como "pendiente de confirmar", con una nota visible que explique esta ambiguedad legal no resuelta, hasta que la empresa lo confirme con su asesoria juridica.

### 11. Evidencia vs Documento vs Log de auditoria

**Descripcion:** el documento maestro usa "evidencia" como campo de casi todos los modulos operativos (tareas, ARCO-POL, consentimiento, incidentes, controles), "documento" como el objeto versionado del modulo de Politicas y documentos (seccion 20), y "log" como la entrada del modulo de Auditoria (seccion 29, "todo cambio importante debe registrar... documentos" entre sus propios campos). No existe una definicion unica de cada concepto ni una regla de cuando algo es uno u otro.

**Donde aparece:** secciones 16, 20 y 29 (ver tambien hallazgo 4 de este informe).

**Por que es un problema:** al no distinguir estos tres conceptos, el modelo de datos implicito del documento maestro corre el riesgo de que un mismo hecho (por ejemplo, la aprobacion de una politica) se registre tres veces con semantica distinta en tres lugares (como "evidencia" adjunta a una tarea, como nueva version de "documento", y como entrada de "log" de auditoria), sin que quede claro cual es la version autoritativa para efectos de demostrar cumplimiento (OBL-PRIN-03, responsabilidad demostrada, Art. 5 lit. i, OBLIGATORIO).

**Resolucion propuesta:** definir tres entidades separadas y con relaciones claras: Documento (contenido versionado, autoria, aprobacion), Evidencia (artefacto o referencia inmutable vinculada a un registro como prueba de que algo ocurrio) y AuditLog (registro de sistema de acciones, que puede referenciar Documentos o Evidencias pero no es ninguno de los dos).

---

## C. Procesos incompletos

### 12. ARCO-POL sin incompetencia, notificacion a receptores ni reclamo posterior

**Descripcion:** el modulo ARCO-POL (seccion 17) enumera portal publico, solicitud, identificacion, validacion, adjuntos, numero de expediente, clasificacion, asignacion, fechas, plazo legal, prevenciones, suspensiones, prorrogas, notas internas, respuesta, aprobacion, envio, cierre y evidencia. Faltan tres etapas que la ley si contempla y que la matriz de obligaciones cataloga de forma independiente.

**Donde aparece:** seccion 17.

**Fundamento legal relacionado:**
- Devolucion por incompetencia (OBL-ARCO-09, Art. 19, 5 dias habiles, CONDICIONAL): cuando la empresa no es la competente para atender la solicitud, debe comunicarlo y devolverla; el documento maestro no tiene esta rama del flujo.
- Notificacion a receptores tras rectificacion/eliminacion (OBL-ARCO-11, Art. 21 inc. 3, 5 dias habiles, CONDICIONAL): si hubo transferencia previa de esos datos, hay que avisar a quienes los recibieron; no aparece como paso en la seccion 17.
- Reclamo del titular ante la Direccion de Proteccion de Datos de la ACE (OBL-ARCO-14, Art. 33 inc. 4 Lineamientos DPO, 10 dias habiles del titular para reclamar, CONDICIONAL): es un estado posterior al "cierre" que el flujo descrito no contempla, porque termina en "cierre" y no prevé una reapertura por reclamo ante la autoridad.

**Por que es un problema:** son tres obligaciones con plazo legal propio, catalogadas y clasificadas en la matriz, que quedarian sin un lugar donde vivir en el flujo tal como esta descrito en el documento maestro; sin esas ramas, el motor de plazos no podria generar automaticamente los contadores de 5 y 10 dias habiles correspondientes.

**Resolucion propuesta:** anadir al flujo de ARCO-POL tres estados/ramas explicitos: Incompetencia (devolucion), Notificacion a receptores/terceros, y Reclamo posterior ante la ACE (como reapertura del expediente ya cerrado).

### 13. Incidentes: computo de las 72 horas y revision interna sin diferenciar

**Descripcion:** el modulo de Incidentes (seccion 25) pide registrar "fecha de deteccion" y "fecha de conocimiento" como campos separados (correcto), pero solo describe un generico "analisis" dentro de la lista de etapas, sin diferenciar dos plazos de 72 horas distintos que la ley establece: uno para notificar hacia afuera (a la ACE, la Fiscalia y los titulares) y otro para iniciar la revision exhaustiva interna del incidente.

**Donde aparece:** seccion 25 ("Verificar exactamente cuando comienza el plazo" queda como instruccion abierta, sin resolverse en el propio documento).

**Fundamento legal relacionado:** OBL-INC-01 (notificacion en 72 horas, Art. 25, OBLIGATORIO) y OBL-INC-02 (revision exhaustiva dentro de las 72 horas, Art. 25 inc. 2, OBLIGATORIO) son dos obligaciones distintas con el mismo plazo pero objetos diferentes (notificar vs empezar a revisar). Ademas, `03_hallazgos_regulatorios.md` (seccion 9, punto 1) deja explicito que el computo de esas 72 horas en horas corridas u horas habiles es una pregunta sin resolver que requiere criterio de abogado.

**Por que es un problema:** si el documento maestro no separa "notificacion externa en 72h" de "inicio de revision interna en 72h" como dos hitos distintos, el diseno del cronometro/checklist que la misma seccion 25 pide ("cronometro; alertas; escalamiento; checklist; evidencias") no tiene forma de mostrar ambos plazos de manera independiente, y el usuario podria creer que cumplio con notificar cuando en realidad tambien debia haber iniciado formalmente la revision interna, o viceversa.

**Resolucion propuesta:** modelar el incidente con dos hitos de 72 horas visibles por separado (notificacion externa e inicio de revision interna), documentar la diferencia entre fecha de deteccion y fecha de conocimiento cuando no coincidan (exigiendo una justificacion, dado que esa diferencia es en si misma parte de la documentacion obligatoria de OBL-INC-04), y marcar de forma visible en el producto que el criterio de horas corridas vs habiles es una incertidumbre legal pendiente de confirmar con abogado, adoptando por defecto el criterio mas conservador (horas corridas).

### 14. Revocacion del consentimiento sin flujo de doble plazo

**Descripcion:** el modulo de Consentimiento (seccion 19) enumera "retiro" y "fecha de retiro" como simples campos de datos, sin describir ningun flujo o maquina de estados para la revocacion. No hay lugar en el modulo, tal como esta descrito, para modelar dos plazos legales encadenados que exige la ley.

**Donde aparece:** seccion 19.

**Fundamento legal relacionado:** OBL-CONS-02 (revocacion en cualquier momento, Art. 29, OBLIGATORIO) y OBL-CONS-03 (plazo de 5 dias habiles para procesar la revocacion, mas otros 5 dias habiles para informar al encargado, Art. 30, OBLIGATORIO) requieren dos contadores de plazo encadenados y una accion sobre el modulo de Proveedores (avisar al encargado), no solo un campo de fecha.

**Por que es un problema:** sin un flujo propio, no hay forma de que el sistema genere automaticamente ni el contador de 5 dias para dejar de tratar el dato, ni el contador adicional de 5 dias para notificar al encargado, ni de vincular esa notificacion con los encargados realmente asociados a ese tratamiento en el modulo de Proveedores.

**Resolucion propuesta:** modelar la revocacion como un mini flujo (no solo un campo) con dos plazos encadenados, y un enlace automatico que genere una tarea en el modulo de Proveedores cuando existan encargados asociados al tratamiento cuyo consentimiento fue revocado.

### 15. Retencion sin regla de conflicto entre bases simultaneas

**Descripcion:** el modulo de Retencion y eliminacion (seccion 21) define estados (activo, proximo a vencer, retenido por obligacion, listo para eliminar, aprobado para eliminar, eliminado) pero no describe como el sistema resuelve el caso, muy comun, en que un mismo dato esta sujeto a varias obligaciones de retencion con plazos distintos y simultaneos.

**Donde aparece:** seccion 21.

**Fundamento legal relacionado:** la matriz cataloga al menos seis obligaciones de retencion distintas (OBL-RET-01 a OBL-RET-06) con periodos que van de 5 a 15 anos segun el regimen aplicable (Codigo de Comercio, Codigo Tributario, Ley Contra el Lavado de Dinero, aviso de privacidad, expediente ARCO-POL, Ley de Firma Electronica). Es comun que dos o mas de estas bases se apliquen a la vez sobre el mismo registro (por ejemplo, datos de un empleado sujetos a la vez al Codigo de Comercio y a la LCLDA).

**Por que es un problema:** sin una regla explicita de "gana el plazo mas largo aplicable" y sin un campo para registrar cual o cuales bases legales sustentan la retencion de cada registro, el usuario no especialista podria eliminar datos antes de tiempo (incumpliendo la base legal mas larga) o retenerlos indefinidamente por exceso de cautela.

**Resolucion propuesta:** exigir que cada regla de retencion cite explicitamente uno o mas OBL-RET como fundamento, y que el sistema calcule la fecha efectiva de retencion como el maximo entre todos los plazos aplicables, mostrando esa fecha y su fundamento al usuario en vez de dejarlo a su criterio manual.

### 16. Aprobacion documental sin cadena configurable por tipo de documento

**Descripcion:** el modulo de Politicas y documentos (seccion 20) lista "borradores, revision, aprobacion, publicacion, versionado" como estados planos, sin definir quien puede aprobar cada tipo de documento ni si distintos tipos de documento (politica interna, aviso de privacidad, contrato con proveedor) requieren distintos niveles o cadenas de aprobacion. El rol "Aprobador" de la seccion 12 aparece como un unico rol generico, sin vincularse a tipos de documento especificos.

**Donde aparece:** secciones 12 y 20.

**Por que es un problema:** tratar la aprobacion como un unico paso generico no permite modelar escenarios razonables como que un aviso de privacidad requiera aprobacion del responsable de privacidad y ademas de Legal, mientras que una plantilla interna menor solo requiera un aprobador. Sin esa distincion, el producto termina forzando el mismo nivel de control para documentos de riesgo muy distinto, o dejando la cadena de aprobacion sin ninguna regla real.

**Resolucion propuesta:** definir la aprobacion como un flujo configurable por tipo/categoria de documento, con uno o mas roles aprobadores requeridos segun el tipo, en lugar de un unico rol "Aprobador" aplicado de forma uniforme a todo el modulo documental.

---

## D. Dependencias no contempladas

### 17. Calendario de dias habiles tratado como detalle, no como dependencia central

**Descripcion:** el documento maestro menciona la necesidad de un calculo de dias habiles dentro de ARCO-POL (seccion 17: "dias habiles; fines de semana; feriados; asuetos configurables; reglas legales aplicables. Investigar cual debe ser la fuente de calendario oficial.") y de forma similar dentro de Incidentes (seccion 25). Sin embargo, nunca se define un modulo o dependencia propia de "calendario"; el concepto queda enterrado como un detalle interno de otros dos modulos.

**Donde aparece:** secciones 17 y 25 (ausente de la lista de dominios de la seccion 10 y de la lista de entidades candidatas de la seccion 46).

**Fundamento legal relacionado:** casi todos los plazos de la matriz (ARCO-POL, DPO, Sanciones) dependen del computo en dias habiles segun el Art. 82 LPA (OBL-PLAZO-01) y del calendario de dias inhabiles (OBL-PLAZO-02, Art. 190 Codigo de Trabajo y decretos de asuetos). Ademas, `03_hallazgos_regulatorios.md` (seccion 9, puntos 2 y 3) deja abierto si el Art. 82 LPA aplica realmente a la relacion titular-empresa privada, y si el sabado debe tratarse como inhabil para el sector privado: son incertidumbres que afectan a un componente que el documento maestro trata como un simple detalle de implementacion de dos modulos, en vez de como una dependencia compartida por todos los modulos con plazo legal.

**Por que es un problema:** si cada modulo (ARCO-POL, DPO, Incidentes, Sanciones) implementa su propia logica de dias habiles por separado, existe el riesgo de que apliquen reglas distintas o inconsistentes al mismo calendario de asuetos, y de que una correccion futura (por ejemplo, si se aclara si el sabado es habil o no) deba aplicarse en varios lugares en vez de en uno solo.

**Resolucion propuesta:** definir un modulo o dependencia explicita de "Calendario / motor de plazos" (coherente con el "Calendario central" que si menciona el prompt de analisis funcional) que centralice la regla de dias habiles/inhabiles, los asuetos nacionales y la incertidumbre abierta sobre el sabado, y que sea la unica fuente que consulten ARCO-POL, DPO, Incidentes y Sanciones para calcular cualquier plazo.

### 18. Motor regulatorio y doble estado de la reforma 659 desconectados de los modulos operativos

**Descripcion:** las secciones 40 ("Motor regulatorio") y 41 ("Actualizacion normativa") describen, en abstracto, un mecanismo de reglas versionadas con fecha de vigencia, pensado sobre todo para una eventual expansion a otros paises. El documento maestro nunca conecta ese mecanismo generico con el caso concreto y ya conocido que la investigacion juridica identifico: la reforma de septiembre de 2026 (Decreto 659), que deroga la obligatoriedad del delegado en el sector privado y esta hoy "aprobada, pendiente de publicacion".

**Donde aparece:** secciones 3 (menciona la reforma como contexto), 40 y 41 (describen el motor generico sin citar la reforma).

**Fundamento legal relacionado:** `03_hallazgos_regulatorios.md` (seccion 3) recomienda explicitamente un diseno de "doble estado" (ACTUAL vs FUTURO) activado por una bandera administrativa manual, no automatica, ligada a la confirmacion real de publicacion en el Diario Oficial. La matriz marca 17 obligaciones (OBL-DPO-01 a 09, OBL-ARCO-01/08/10/11/14, OBL-CAP-02, OBL-CONS-03, OBL-PLAZO-05, OBL-RET-04) como afectadas por esta reforma.

**Por que es un problema:** sin conectar el motor regulatorio generico con este caso concreto, el equipo de producto podria disenar un mecanismo abstracto de "paquetes regulatorios por pais" sin resolver el requisito practico e inmediato de que el cambio de estado del delegado obligatorio debe activarse manualmente (nunca por la sola aprobacion legislativa) y debe re-etiquetar automaticamente unas 17 obligaciones ya identificadas cuando se active.

**Resolucion propuesta:** documentar la reforma 659 como el primer caso de uso real y concreto del motor regulatorio, con el comportamiento de activacion manual descrito explicitamente en la ficha del modulo (no solo implicito en la arquitectura general), y la lista de obligaciones que cambian de estado al activarse.

### 19. Catalogo de sistemas sin modulo propietario

**Descripcion:** tanto Inventario de datos (seccion 13) como RAT (seccion 14) como Proveedores (seccion 22) piden vincular un tratamiento o proveedor a "sistema"/"sistemas", y el candidato de entidad "System" aparece en la lista de la seccion 46 (modelo de datos). Sin embargo, ningun modulo de las secciones 10 a 31 tiene como responsabilidad crear, editar, deduplicar o dar de baja ese catalogo de sistemas: aparece solo como un campo referenciado desde otros lados.

**Donde aparece:** secciones 13, 14, 22, 25 y 46 (ausente de la lista de dominios de la seccion 10).

**Por que es un problema:** sin un modulo propietario, cada tratamiento o proveedor podria terminar escribiendo el nombre del sistema como texto libre, generando duplicados ("CRM", "Salesforce", "Salesforce CRM" como tres entradas distintas para el mismo sistema) que rompen la trazabilidad que el RAT y el mapa de datos necesitan para responder "donde estan los datos".

**Resolucion propuesta:** anadir un modulo (o submodulo de Organizacion) de "Catalogo de sistemas" que sea la unica fuente de alta/edicion de la entidad Sistema, consultada por referencia desde RAT, Inventario, Proveedores e Incidentes.

### 20. Verificacion de identidad del titular no definida

**Descripcion:** el modulo ARCO-POL (seccion 17) lista "identificacion, validacion" como etapas del flujo, y el Portal de privacidad (seccion 18) propone que los titulares presenten solicitudes ARCO-POL de forma publica en linea. El documento maestro nunca define que metodo o documento de identidad se acepta, ni como se diferencian los tres tipos de solicitante que la ley reconoce.

**Donde aparece:** secciones 17 y 18.

**Fundamento legal relacionado:** Art. 18 lit. b) exige "documentos de identidad" dentro de la solicitud (parte de OBL-ARCO-08, matriz), y OBL-ARCO-01 (Art. 6, matriz) reconoce tres tipos de solicitante con requisitos documentales distintos: el propio titular, su representante con facultades especiales, o (si el titular fallecio) sus herederos o sucesores.

**Por que es un problema:** un portal publico que permite presentar solicitudes ARCO-POL en linea, sin un mecanismo definido de verificacion de identidad, crea un riesgo real de suplantacion (alguien solicitando el acceso, la cancelacion o la portabilidad de los datos de otra persona). El documento maestro pide "analizar seguridad y riesgos de exposicion" del portal (seccion 18) pero no resuelve especificamente este punto.

**Resolucion propuesta:** definir un subproceso explicito de "Verificacion de identidad del titular" dentro de ARCO-POL (referenciado tambien desde el Portal), que distinga los tres tipos de solicitante reconocidos por el Art. 6 y sus requisitos documentales propios.

### 21. Tramites y contacto ante la ACE no modelados

**Descripcion:** el documento maestro no tiene ningun campo, modulo o seccion para gestionar las comunicaciones que la empresa debe enviar hacia la ACE (no solo recibir o cumplir internamente). El modulo de organizacion (seccion 11) solo modela contactos internos (contacto ARCO-POL, contacto de seguridad); no hay lugar para rastrear tramites salientes hacia el regulador.

**Donde aparece:** secciones 11 y 24 (donde deberia aparecer la puesta en conocimiento a la ACE de las transferencias, y no aparece).

**Fundamento legal relacionado:** OBL-DPO-03 (comunicacion del nombramiento del delegado a la ACE en 15 dias habiles, Art. 10 Lineamientos DPO, CONDICIONAL) y OBL-TRANSF-05 (puesta en conocimiento a la ACE del flujo transfronterizo, Art. 45, OBLIGATORIO) son, ambas, obligaciones de enviar informacion hacia la autoridad, no solo de mantenerla documentada internamente.

**Por que es un problema:** sin un lugar que modele estos tramites salientes (que se envio, cuando, con que numero de referencia de la ACE si existe, y que respuesta hubo), el producto no puede generar evidencia de que la empresa efectivamente cumplio con su deber de informar a la autoridad, que es distinto del deber de documentar internamente.

**Resolucion propuesta:** anadir un concepto explicito de "Tramites ante la ACE" (dentro de Organizacion o de un futuro modulo Regulatorio) que registre cada envio saliente (nombramiento del delegado, notificacion de transferencia, solicitud de credencial) con su propio estado, evidencia de envio y referencia de la ACE.

### 22. Principio "core vs regulatory pack" contradicho por reglas salvadorenas ya incrustadas en los modulos

**Descripcion:** la seccion 40 (Motor regulatorio) propone separar un "Core Privacy Engine" generico de un "Regulatory Pack El Salvador" que contendria los plazos, formularios, obligaciones, documentos y reglas especificas del pais, precisamente para permitir expansion futura. Sin embargo, las propias descripciones de los modulos que la seccion 40 lista como parte del "Core" (tratamientos, solicitudes, tareas, incidentes) ya incluyen, en las secciones 14, 17 y 25, terminologia y plazos especificos de la LPDP (ARCO-POL, dias habiles salvadorenos, las seis bases de licitud del Art. 5 lit. g) escritos directamente en la descripcion del modulo "core", no separados en un paquete.

**Donde aparece:** seccion 40 (comparada con 14, 17 y 25).

**Por que es un problema:** el documento maestro se contradice a si mismo: pide una arquitectura funcional donde el nucleo sea agnostico de pais, pero especifica el contenido de ese mismo nucleo usando terminologia y reglas que son propias unicamente de El Salvador. Esto no es un problema tecnico de implementacion (fuera del alcance de esta fase), sino una inconsistencia funcional: el documento no decide, a nivel de diseno de modulos, que partes de ARCO-POL/RAT/Incidentes son genericas y cuales son especificas de El Salvador.

**Resolucion propuesta:** en la ficha de cada modulo, separar explicitamente que campos/reglas son genericos (aplicables a cualquier pais) y cuales son especificos de la LPDP salvadorena, en lugar de dejar la separacion nucleo/paquete como una aspiracion arquitectonica no reflejada en el contenido funcional de los propios modulos.

---

## E. Contradicciones internas

### 23. "No almacenar PII innecesariamente" vs expediente ARCO-POL, Portal, Incidentes y Consentimiento

**Descripcion:** la seccion 37 (Privacy by Design) establece como principio que la plataforma "NO debe copiar o centralizar innecesariamente todos los datos personales de los clientes", y pone como ejemplo no almacenar toda la base de Salesforce, sino solo metadatos (que sistema contiene que categoria de datos, quien es responsable, donde esta, cuanto se retiene). Sin embargo, otros modulos del mismo documento exigen exactamente lo contrario: ARCO-POL (seccion 17) requiere almacenar identificacion, documentos de identidad y adjuntos del titular; Consentimiento (seccion 19) propone guardar "IP si es pertinente" del titular; Incidentes (seccion 25) requiere listar los "titulares" afectados; Portal de privacidad (seccion 18) hace que los titulares carguen documentos y creen cuentas directamente en la plataforma.

**Donde aparece:** secciones 17, 18, 19, 25 y 37.

**Por que es un problema:** el documento maestro presenta un principio general de "no almacenar PII" sin acotar su alcance, cuando en realidad varios de sus propios modulos centrales (ARCO-POL, Portal, Incidentes, Consentimiento) necesitan, de forma legitima e inevitable, almacenar datos personales directos del titular como objeto mismo del proceso (no como copia de un sistema externo). Tal como esta escrito, el principio de la seccion 37 es incompatible, en los hechos, con los requisitos funcionales que el propio documento fija para esos cuatro modulos.

**Resolucion propuesta:** acotar explicitamente el alcance del principio de la seccion 37: aplica al RAT, al Inventario de datos y a Proveedores (que describen sistemas externos del cliente sin replicar su contenido), pero no aplica a ARCO-POL, Portal, Incidentes ni Consentimiento, que por su propia naturaleza procesan y conservan datos personales de primera mano del titular como parte legitima del proceso. Esta excepcion deberia quedar escrita en la ficha de cada modulo afectado.

### 24. "No ser Delegado ni operador de ARCO-POL" vs automatizacion de actos legales del delegado

**Descripcion:** la seccion 3 declara que el proveedor del software no actuara como "Delegado de Proteccion de Datos del cliente" ni como "operador humano de las solicitudes ARCO-POL del cliente". Sin embargo, el modulo ARCO-POL (seccion 17) pide que el "calculo de plazos" del sistema genere ciertos actos que, segun el texto hoy vigente de la ley (Arts. 18, 19, 21, 30), estan atribuidos especificamente a "el delegado", no al "responsable" en general: emitir la prevencion, declarar la incompetencia, notificar a receptores, procesar la revocacion.

**Donde aparece:** secciones 3 y 17.

**Fundamento legal relacionado:** OBL-ARCO-08 (Art. 18, prevencion), OBL-ARCO-09 (Art. 19, incompetencia), OBL-ARCO-11 (Art. 21, notificacion a receptores) y OBL-CONS-03 (Art. 30, revocacion) son, todas, actuaciones que el texto vigente atribuye al delegado.

**Por que es un problema:** el documento maestro no aclara si el software solo calcula/redacta estos actos para que una persona humana (el Delegado, ver hallazgo 7) los revise y emita, o si el sistema los genera y envia de forma automatica. La seccion 17 usa un lenguaje que sugiere automatizacion fuerte ("el motor de plazos debe generar automaticamente la prevencion") sin exigir en ningun punto una aprobacion humana explicita antes del envio, lo cual entra en tension directa con el compromiso de la seccion 3 de no actuar como el "operador humano" de las solicitudes ni sustituir la funcion del delegado.

**Resolucion propuesta:** dejar explicito, en la ficha del modulo ARCO-POL y en la del Delegado, que todo acto legalmente atribuido al delegado es calculado/redactado por el sistema pero requiere una accion explicita de aprobacion por parte de la persona que ocupa el rol Delegado antes de considerarse emitido, cerrando la brecha entre el principio de la seccion 3 y el lenguaje de automatizacion de la seccion 17.

### 25. Capacitacion tratada como funcionalidad opcional a evaluar vs obligacion legal

**Descripcion:** la seccion 28 (Capacitacion) plantea el modulo entero como una pregunta abierta a evaluar ("Evaluar si debe existir: cursos; microlearning; evaluaciones; registros; certificados; recordatorios"), en un tono que lo presenta como una funcionalidad diferenciadora opcional, similar a como se tratan otras funciones claramente no obligatorias del documento.

**Donde aparece:** seccion 28.

**Fundamento legal relacionado:** OBL-CAP-01 (capacitacion del personal como medida organizativa obligatoria, Art. 4 Politicas ACE, OBLIGATORIO) clasifica la capacitacion del personal como una medida organizativa de cumplimiento obligatorio, no como una buena practica opcional (a diferencia de OBL-CAP-02, el plan anual especifico del delegado, que si es CONDICIONAL).

**Por que es un problema:** presentar como "a evaluar si debe existir" algo que la matriz de obligaciones clasifica como OBLIGATORIO para toda empresa genera un riesgo de priorizacion equivocado: un equipo de producto que lea el documento maestro literalmente podria posponer Capacitacion a una version futura por no reconocer que, a diferencia de otras funciones opcionales de la misma seccion (certificados, microlearning), el nucleo de "registrar que el personal fue capacitado" es una obligacion legal minima, no una decision de alcance libre.

**Resolucion propuesta:** separar, dentro de la ficha del modulo, que parte de Capacitacion es obligatoria (el registro minimo de que el personal recibio capacitacion, ligado a OBL-CAP-01) de que parte es opcional o diferenciadora de producto (cursos interactivos, certificados, microlearning), en lugar de presentar el modulo completo como una sola pregunta abierta de alcance.

### 26. Integridad del log de auditoria (WORM/hash) vs paquete de evidencias exportable sin garantia de integridad

**Descripcion:** el modulo de Auditoria y trazabilidad (seccion 29) exige explicitamente mecanismos de integridad fuertes para el log: WORM, append-only logs, hash chaining, integridad criptografica, y establece que "los usuarios normales NO deberian poder borrar logs de auditoria". El modulo de Paquete de evidencias (seccion 30), que exporta esos mismos logs junto con RAT, politicas, incidentes y demas, a formatos como XLSX y CSV, no menciona ningun mecanismo que preserve esa integridad una vez exportado (por ejemplo, una firma o hash del paquete generado).

**Donde aparece:** secciones 29 y 30.

**Fundamento legal relacionado:** OBL-PRIN-03 (principio de responsabilidad demostrada, Art. 5 lit. i, OBLIGATORIO) y, en escenarios de transferencia o de sancion, OBL-TRANSF-06/OBL-CONS-05 (carga de la prueba, Art. 54) dependen de que la evidencia presentada ante la ACE o ante un tercero sea verificablemente integra.

**Por que es un problema:** todo el cuidado que la seccion 29 pone en garantizar que el log no pueda alterarse dentro del sistema pierde valor si, en el momento en que mas importa (presentar el paquete de evidencias ante la ACE o en un procedimiento sancionador), el archivo exportado en XLSX o CSV no lleva ninguna garantia de que no fue modificado despues de exportarlo. El documento maestro no resuelve esta discontinuidad entre la integridad dentro del sistema y la integridad del archivo una vez que sale del sistema.

**Resolucion propuesta:** exigir que todo paquete de evidencias exportado incluya un mecanismo de verificacion de integridad del propio paquete (por ejemplo, un hash o firma que se pueda validar de forma independiente), de modo que la garantia de integridad de la seccion 29 se extienda al artefacto que efectivamente se entrega a la autoridad o se usa como prueba.

---

## Nota final

Todas las "resoluciones propuestas" de este informe son opciones de diseno funcional a validar con el equipo del proyecto; ninguna constituye una obligacion legal en si misma salvo cuando el hallazgo cita expresamente un OBL-ID de la matriz. Las referencias a incertidumbres juridicas (computo de las 72 horas, aplicabilidad del Art. 82 LPA, transferencia vs acceso del encargado, numero exacto del Decreto 659) provienen integramente de `03_hallazgos_regulatorios.md` y requieren confirmacion de abogado antes de fijarse como regla de producto.
