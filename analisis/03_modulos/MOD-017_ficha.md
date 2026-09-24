# MODULO: Capacitacion

Codigo corto del modulo: MOD-017
Clasificacion global del modulo: MUST HAVE
Obligaciones que cubre: OBL-CAP-01, OBL-CAP-02 (propietarias); OBL-DPO-04, OBL-DPO-05 (colaboradoras, propietario MOD-002), OBL-SEG-02 (colaboradora, propietario MOD-015)

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (sin codigo, sin SQL, sin APIs, sin stack, sin infraestructura).

Fuentes usadas para esta ficha: `00_contexto_para_agentes.md`; `00_prompt_analisis_funcional.md`; `00_plantilla_ficha_modulo.md`; `02_validacion/mapa_modulos.json` (entrada MOD-017); `02_validacion/06_mapa_definitivo_de_modulos.md` (secciones 0, 2, 3, 4, 5, 6.1, 7, 8, 9); `01_legal/matriz_obligaciones.json` (OBL-CAP-01, OBL-CAP-02, OBL-DPO-04, OBL-DPO-05, OBL-SEG-02); `01_legal/03_hallazgos_regulatorios.md` (seccion 4.13, seccion 11); `01_legal/fuentes/lineamientos_dpo_OCR.txt` (Art. 22); `01_legal/fuentes/ace_politicas_protecciondatos.txt` (Art. 4); `02_validacion/02_validacion_de_la_idea.md` (2.3 a 2.7, decision 2.7.23); `02_validacion/04_objetivo_exacto_del_producto.md`; `02_validacion/05_tipos_de_usuario.md` (5.1, 5.3, 5.4); `02_validacion/22_anti_features.md`; `02_validacion/lente_faltantes.md`; `02_validacion/lente_inconsistencias.md` (hallazgo 25); `02_validacion/lente_supuestos.md`; `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` (seccion 28, hipotesis de producto); fichas ya escritas con contrato hacia este modulo: `03_modulos/MOD-002_ficha.md`, `03_modulos/MOD-006_ficha.md`, `03_modulos/MOD-013_ficha.md`, `03_modulos/MOD-016_ficha.md`, `03_modulos/MOD-018_ficha.md`, `03_modulos/MOD-021_ficha.md`.

---

## A. Proposito

- **Por que existe.** Las Politicas de Actuacion y Manejo de Datos Personales de la ACE (N. 001-0309025-DPDP, Art. 4, Medidas Organizativas lit. c) exigen que toda empresa privada sujeta a la LPDP capacite a su personal en proteccion de datos, sin fijar contenido, formato ni periodicidad especifica, salvo la que fije el propio Delegado si existe (OBL-CAP-01, OBLIGATORIO, sin condicion). Por separado, los Lineamientos para el Delegado de Proteccion de Datos Personales (Art. 22, segundo parrafo) exigen que, mientras exista la figura del Delegado, esa persona elabore un plan anual de capacitacion dirigido al personal, que incluya expresamente programas de induccion para el personal nuevo que trate datos personales (OBL-CAP-02, CONDICIONAL a tener Delegado nombrado, afectada por la reforma 659). Ningun otro modulo tiene como funcion propia registrar que el personal fue capacitado ni dar forma al plan anual que el Delegado debe elaborar: esa es la funcion exclusiva de MOD-017.
- **Que problema resuelve para la empresa.** Sin este modulo, "capacitar al personal" queda como una intencion sin registro verificable (quien, cuando, en que), el Delegado no tiene donde elaborar ni versionar el plan anual que la norma le exige, el personal nuevo puede empezar a tratar datos sin induccion, y los roles con exposicion directa a obligaciones especificas (quien atiende ARCO-POL, quien responde incidentes, RRHH, Marketing) no tienen un registro diferenciado de que recibieron la capacitacion que su funcion requiere.
- **Que obligacion u obligaciones cubre (IDs y articulos).**
  - **OBL-CAP-01** (propietaria), Politicas de Actuacion ACE, Art. 4 Medidas Organizativas lit. c): "Capacitacion del Personal: Formacion continua sobre seguridad de datos". OBLIGATORIO, sin condicion, aplica a toda empresa privada sujeta a la LPDP, sin que la norma fije contenido, formato ni periodicidad, salvo la que fije el propio Delegado, si existe (salvedad que el diseno de D.1, campo Periodicidad de renovacion, ya absorbe al dejar la periodicidad editable y en manos de quien administra el programa). Es el nucleo de este modulo: el registro minimo de que el personal recibio capacitacion (decision 2.7.23 de `02_validacion_de_la_idea.md`, que cierra el hallazgo 25 de `lente_inconsistencias.md`: el documento maestro trataba toda la capacitacion como "a evaluar" cuando esta parte tiene una obligacion legal minima y directa).
  - **OBL-CAP-02** (propietaria), Lineamientos para el Delegado, Art. 22, ultimo parrafo: "el Delegado elaborara un plan anual de capacitacion dirigido al personal del ente obligado, el cual tambien incluira programas de induccion para el personal nuevo que desempene funciones relacionadas al tratamiento de datos personales". CONDICIONAL (aplica mientras subsista la figura del Delegado en la empresa), afectada por la reforma 659. Ver la nota de precision sobre esta obligacion mas abajo y en la nota final de esta ficha: no es la capacitacion especifica del propio Delegado (eso es OBL-DPO-05), sino el plan que el Delegado debe elaborar para el resto del personal, incluida la induccion.
  - Colabora con **OBL-DPO-04** (Art. 18 Lineamientos DPO, CONDICIONAL, propietario MOD-002): la reverificacion del perfil del delegado cada 3 anos exige presentar atestados de capacitacion o certificaciones. MOD-017 aporta esa evidencia: cada constancia que esta persona recibe como parte de su propia capacitacion (registrada aqui como cualquier otro TrainingRecord) queda disponible como insumo para el expediente de reverificacion que administra MOD-002, sin que MOD-017 decida ni ejecute la reverificacion en si.
  - Colabora con **OBL-DPO-05** (Art. 22, primer parrafo, Lineamientos DPO, CONDICIONAL, propietario MOD-002): el responsable debe garantizar que el Delegado reciba capacitacion al menos una vez al ano en proteccion de datos y en el ejercicio de los derechos ARCO-POL. MOD-017 es el mecanismo operativo que registra esa capacitacion especifica (un TrainingProgram dirigido al rol Delegado, con su TrainingRecord correspondiente) y notifica a MOD-002 cuando hay una constancia nueva disponible para su campo `fecha_ultima_capacitacion_delegado`; MOD-002 sigue siendo el propietario de la obligacion y de ese campo.
  - Colabora con **OBL-SEG-02** (Art. 4 Politicas ACE, medidas organizativas minimas, OBLIGATORIO, propietario MOD-015 Controles de Seguridad): una de las seis medidas organizativas del catalogo de MOD-015 es literalmente "Capacitacion del Personal". MOD-017 es el modulo que produce la evidencia sustantiva de esa medida (el registro y sus constancias), en el mismo patron que ya documenta la ficha de MOD-018 para su propia colaboracion con OBL-SEG-02.
- **Nota de precision sobre OBL-CAP-02 (ver tambien la nota final de esta ficha).** La ficha resumida de MOD-017 en `06_mapa_definitivo_de_modulos.md` (seccion 3) y el campo `notas_reforma_659` de `mapa_modulos.json` describen OBL-CAP-02 como "capacitacion especifica anual del Delegado". El texto exacto de `matriz_obligaciones.json` y la fuente primaria (`lineamientos_dpo_OCR.txt`, Art. 22, ultimo parrafo) definen algo distinto: el plan anual de capacitacion **dirigido al personal**, que el Delegado **elabora**, incluida la induccion de personal nuevo. Esta ficha disena el modulo segun el texto de la matriz y de la fuente primaria (verificado linea por linea en la seccion de fuentes de esta ficha), no segun la frase abreviada del mapa. La capacitacion especifica y personal del propio Delegado, que si es "anual y del Delegado" en sentido literal, es OBL-DPO-05, propietario MOD-002, colaboradora aqui.
- **Que valor aporta.**
  - Operativo: convierte "hay que capacitar al personal" en un registro concreto por persona, tema y fecha, con recordatorio automatico de renovacion, sin que la empresa tenga que llevar esa cuenta en una hoja de calculo aparte.
  - Probatorio: junto con MOD-019, es la evidencia directa de que la medida organizativa "Capacitacion del Personal" (OBL-SEG-02) existe y de que el Delegado cumplio su deber de elaborar el plan anual (OBL-CAP-02), con constancia individual verificable por persona.
  - De reduccion de riesgo: reduce la exposicion de la empresa a errores evitables (por ejemplo, un empleado de Marketing que no sabe que una campana necesita base juridica, o un encargado de TI que no sabe que un incidente tiene un plazo de 72 horas) mediante capacitacion diferenciada por rol.
- **Que NO hace este modulo (limites explicitos).**
  - No es una plataforma de cursos ni un sistema de aprendizaje (LMS): no ofrece cursos interactivos, microlearning, evaluaciones formales con calificacion ni certificados generados por el sistema en el MVP; esas funciones quedan diferidas a V1/V2 (ver seccion Q), en linea con la resolucion explicita del hallazgo 25 de `lente_inconsistencias.md`: separar el registro minimo obligatorio de las funcionalidades opcionales o diferenciadoras.
  - No evalua ni certifica si el contenido de una capacitacion es correcto, completo o legalmente suficiente; solo registra que existio, quien la recibio y con que material (ver seccion H).
  - No decide si una empresa debe o no tener Delegado, ni si el plan anual sigue siendo obligatorio bajo el estado FUTURO de la reforma 659; eso lo determina la bandera de MOD-024 y el propio registro de MOD-002 (ver "Doble estado" mas abajo).
  - No sustituye ni sobrescribe el expediente laboral del empleado: no es un sistema de RRHH ni de gestion del talento; solo referencia al usuario (MOD-001) y registra los metadatos minimos de la capacitacion recibida (anti-feature 1 y 8 de `22_anti_features.md`).
  - No genera automaticamente el contenido pedagogico de una capacitacion; la empresa aporta o elige el material, el sistema solo lo versiona y lo asocia al registro.

### Doble estado de la reforma 659 en este modulo

De las 17 obligaciones de la matriz marcadas como afectadas por la reforma 659, una es propia de MOD-017: **OBL-CAP-02**. Mientras la bandera `regimen_reforma_659` de MOD-024 este en `ACTUAL` (el vigente al 2026-09-24, con Delegado obligatorio en el sector privado, Arts. 15 y 17 LPDP), el plan anual de capacitacion e induccion que el Delegado debe elaborar sigue siendo CONDICIONAL pero, en la practica, exigible para toda empresa que tenga Delegado nombrado, que hoy es obligatorio para todas. Si la bandera pasa a `FUTURO` (solo cuando el equipo del producto confirme la publicacion del decreto en el Diario Oficial y transcurra la vacatio legis), el plan anual deja de ser exigible como obligacion legal, salvo que la empresa mantenga voluntariamente a su Delegado (`06_mapa_definitivo_de_modulos.md`, seccion 5, punto 7): en ese caso el sistema conserva la funcionalidad completa, solo cambia el texto de ayuda contextual (seccion R) de "obligatorio" a "buena practica recomendada". El registro general de capacitacion del personal (OBL-CAP-01) no depende de la figura del Delegado ni de esta bandera: no cambia bajo ningun escenario de la reforma. Los planes anuales ya publicados antes de un cambio de bandera conservan su version y su caracter de obligatorio en el momento en que se publicaron, sin reescritura retroactiva (mismo principio de preservacion de historial que usan MOD-002 y MOD-016).

---

## B. Usuarios

| Rol estandar | Para que usa este modulo |
|---|---|
| Administrador de la organizacion | Configura los parametros generales (periodicidad por defecto de renovacion, dias de anticipacion de alertas, umbral de doble control); en pyme puede crear programas y registrar capacitaciones cuando no hay RRHH dedicado, con advertencia de autorrevision |
| Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | Usuario principal para OBL-CAP-02: elabora y publica el plan anual de capacitacion e induccion; recibe su propia capacitacion especifica anual (OBL-DPO-05) registrada aqui como cualquier otro TrainingRecord; consulta el estado general del registro de personal |
| Responsable ARCO-POL / Responsable del tramite | Recibe y completa la capacitacion por rol dirigida a quien atiende solicitudes de titulares (verificacion de identidad, causales tasadas, plazos) |
| Responsable Legal / Compliance | Revisa el contenido del plan anual antes de su publicacion cuando co-coordina con el Delegado; puede crear o editar programas generales |
| Responsable de Seguridad / IT | Recibe y completa la capacitacion por rol sobre manejo de incidentes de seguridad y buenas practicas (phishing, contrasenas); puede ademas ser quien registra la capacitacion tecnica de otros usuarios de su area |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | RRHH: gestiona la induccion de personal nuevo y el registro general de su area; Marketing y las demas areas: reciben y completan la capacitacion por rol relacionada con su exposicion especifica (por ejemplo, base juridica de campanas para Marketing) |
| Aprobador | Aprueba la publicacion del plan anual de capacitacion e induccion antes de que quede como version oficial |
| Auditor (interno) | Solo lectura: revisa que cada capacitacion tenga constancia y que el plan anual este publicado y vigente, como verificacion independiente; nunca registra ni aprueba nada aqui |
| Auditor externo (invitado) | Acceso temporal de solo lectura al historico de capacitaciones y al plan anual, durante una auditoria puntual (MOD-018) |
| Usuario de consulta / Colaborador | Autoservicio: ve y confirma las capacitaciones que se le asignaron (induccion, renovacion, por rol) y adjunta su propia constancia o acuse cuando el flujo lo permite |
| Titular (formulario externo) | No aplica: este modulo es informacion organizativa interna sobre la formacion del personal, nunca interactua con titulares de datos |
| Asesor externo invitado | Acceso puntual cuando se le invita a revisar si el contenido de una capacitacion cubre razonablemente un tema en disputa (por ejemplo, tras un hallazgo de auditoria) |

---

## C. Permisos

| Accion | Administrador | Delegado / Resp. interno | Resp. ARCO-POL | Resp. Legal | Resp. Seguridad/IT | Resp. de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Titular | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver programas y registros (alcance segun rol) | Si | Si | Si (solo su capacitacion por rol) | Si | Si (solo tecnica/su area) | Si (solo su area) | Si | Si (solo lectura) | Si (solo lo compartido, invitado) | Si (solo lo propio) | No | Si (caso puntual) |
| Crear programa (General, Induccion, Por rol) | Si (config general) | Si | No | Si | Si (tecnicos) | No | No | No | No | No | No | No |
| Elaborar/editar el Plan anual (tipo Plan anual) | No (salvo pyme, con advertencia de autorrevision) | Si | No | Si (co-edicion) | No | No | No | No | No | No | No | No |
| Publicar el Plan anual | No | Si (propone) | No | No | No | No | Si (aprueba y publica) | No | No | No | No | No |
| Registrar un TrainingRecord (asistencia propia o de terceros) | Si | Si | Si (propia) | Si (propia) | Si (propia o de su area tecnica) | Si (de su area) | No | No | No | Si (solo propia) | No | No |
| Cerrar / marcar Completada una capacitacion | Si (pyme, con advertencia) | Si | Si (propia) | Si (propia) | Si (propia o asignada) | Si (de su area) | No | No | No | Si (propia) | No | No |
| Archivar un programa (nunca eliminar historial) | Si | Si | No | Si | No | No | No | No | No | No | No | No |
| Exportar (listados, plan anual, paquete de evidencia) | Si | Si | No | Si | Si (solo su area) | Si (solo su area) | Si | Si | Si (alcance temporal) | No | No | No |
| Asignar (programar induccion o capacitacion por rol a una persona) | Si | Si | No | Si | Si (tecnicos) | Si (de su area) | No | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | Si | Si (invitado) | Si (propia) | No | Si (caso asignado) |
| Adjuntar evidencia (constancia, acuse, material) | Si | Si | Si (propia) | Si | Si (propia o de su area) | Si (propia o de su area) | No | No | No | Si (propia) | No | No |

**Separacion de funciones.** Elaborar el plan anual (Delegado/Responsable interno o, co-editando, Responsable Legal) y aprobarlo/publicarlo (Aprobador) son acciones separadas: el sistema exige un Aprobador distinto de quien lo elaboro antes de publicarlo, salvo en pyme por debajo del umbral configurable (propuesta inicial 50 empleados, `05_tipos_de_usuario.md` seccion 5.4), donde se permite con advertencia visible de "autorrevision". El rol Auditor (interno o externo) es siempre de solo lectura, nunca registra ni aprueba, para preservar la independencia de su verificacion. Cuando el TrainingRecord corresponde a la propia persona con rol Delegado (su capacitacion especifica anual, OBL-DPO-05), el sistema permite que la misma persona registre su asistencia (autoservicio, igual que cualquier Usuario de consulta), pero la constancia queda igualmente visible para Administrador y Auditor, sin ocultarse por tratarse del Delegado.

---

## D. Informacion de entrada

MOD-017 administra dos entidades, coherentes con `06_mapa_definitivo_de_modulos.md` seccion 7: **TrainingProgram** (el programa o plan que define que se va a ensenar, a quien y con que periodicidad) y **TrainingRecord** (el registro de que una persona concreta recibio, o debe recibir, una instancia de ese programa).

### D.1 Campos de TrainingProgram

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Nombre del programa | Texto | Obligatorio | - | Maximo 140 caracteres; unico dentro de la organizacion por tipo | "Nombre facil de reconocer, por ejemplo: 'Induccion en proteccion de datos - personal nuevo 2027'." | Buena practica |
| Tipo de programa | Seleccion unica | Obligatorio | General (todo el personal) / Induccion de personal nuevo / Por rol especifico / Plan anual (documento agregador) | No editable despues de creado | "Elige que clase de capacitacion es esta." | OBL-CAP-01 (General, Induccion, Por rol); OBL-CAP-02 (Plan anual) |
| Tema | Seleccion multiple | Obligatorio (minimo uno) | Proteccion de datos personales (general); Derechos ARCO-POL; Datos sensibles y consentimiento reforzado; Manejo de incidentes de seguridad; Phishing y buenas practicas de contrasenas; Uso adecuado de la informacion; Induccion general de proteccion de datos; Otro (texto libre) | - | "Elige el tema principal de esta capacitacion." | Catalogo tomado de los temas de la seccion 28 del documento maestro (buena practica; la norma no fija un contenido obligatorio, ver OBL-CAP-01) |
| Rol o publico destinatario | Seleccion multiple | Obligatorio (minimo uno) | Todo el personal, o uno o mas de los 12 roles estandar (tipicamente Responsable ARCO-POL / Responsable del tramite, Responsable de Seguridad/IT, Responsable de area RRHH, Responsable de area Marketing, Delegado de Proteccion de Datos) | - | "A quien va dirigida esta capacitacion." | [Opinion de producto] el enfoque de capacitacion diferenciada por rol no lo fija la norma, pero responde al enfoque especifico de este modulo |
| Modalidad | Seleccion unica | Obligatorio | Presencial / Virtual en vivo / Virtual autogestionada (grabada o material de autoestudio) | - | "Como se va a impartir esta capacitacion." | Buena practica |
| Version del material | Texto o numero de version | Obligatorio | - | Debe incrementar respecto a la version anterior del mismo programa | "Version del contenido usado, para saber exactamente que se enseno en cada fecha." | Buena practica, trazabilidad |
| Material adjunto | Archivo (uno o varios) | Recomendado | - | Formato y tamano segun la politica general de adjuntos del sistema | "Sube la presentacion, video o documento que vas a usar." | Buena practica |
| Periodicidad de renovacion | Seleccion unica + numero si aplica | Obligatorio, salvo Tipo = Induccion | Sin renovacion (induccion unica) / Anual / Cada 2 anos / Personalizada | - | "Cada cuanto debe repetirse esta capacitacion. La ley no fija un plazo para el registro general; el sistema sugiere 'Anual' por defecto, editable." | Buena practica (OBL-CAP-01 sin plazo fijado); para Tipo = Plan anual la periodicidad es fija de 1 ano (ver fila siguiente) |
| Elaborado / propuesto por | Referencia a usuario | Obligatorio si Tipo = Plan anual; opcional en los demas tipos | Usuario con rol Delegado de Proteccion de Datos (o Responsable interno); cualquier rol habilitado en los demas tipos | Si Tipo = Plan anual, el usuario debe tener ese rol activo en MOD-002 | "Quien preparo este programa. El plan anual completo debe ser elaborado por la persona con el rol de Delegado o Responsable interno." | OBL-CAP-02, Art. 22 ultimo parrafo Lineamientos DPO |
| Programas incluidos | Referencia multiple a otros TrainingProgram | Obligatorio si Tipo = Plan anual (minimo uno) | Catalogo de programas Vigente o Borrador de la organizacion | Debe incluir al menos un programa de Tipo = Induccion de personal nuevo | "Selecciona los programas de capacitacion e induccion que este plan anual va a cubrir durante el ano." | OBL-CAP-02 (el plan debe incluir expresamente induccion de personal nuevo) |
| Documento del plan | Referencia a Document (MOD-008) | Obligatorio antes de publicar, solo si Tipo = Plan anual | - | Debe existir un documento en un estado valido de MOD-008 | "El documento formal del plan anual; es el mismo que se muestra por referencia en el expediente del Delegado (MOD-002)." | OBL-CAP-02; enlazado con el campo `plan_capacitacion_personal` de MOD-002 |
| Estado | Seleccion unica | Obligatorio, valor inicial Borrador | Borrador / Vigente / Archivado | Transiciones segun seccion F | "En que etapa esta este programa." | Buena practica |
| Fecha de publicacion / vigencia desde | Fecha | Autogenerado al pasar a Vigente | - | - | "Desde cuando esta vigente este programa." | Buena practica |
| Aplica bajo el regimen (solo Tipo = Plan anual) | Campo calculado, solo lectura | Autogenerado | Obligatorio (regimen ACTUAL) / Buena practica voluntaria (regimen FUTURO sin Delegado voluntario) | Se recalcula al consultar la bandera `regimen_reforma_659` de MOD-024 | "Si la reforma 659 llega a estar vigente, este plan pasa de obligatorio a buena practica recomendada, salvo que su empresa decida mantener un Delegado." | OBL-CAP-02; `06_mapa_definitivo_de_modulos.md`, seccion 5 |

### D.2 Campos de TrainingRecord

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Persona | Referencia a Usuario (MOD-001) | Obligatorio | Usuarios activos de la organizacion | Debe existir y estar Activo | "A quien corresponde este registro." | Buena practica; minimizacion (referencia, no copia del expediente laboral) |
| Programa relacionado | Referencia a TrainingProgram | Obligatorio | Catalogo de programas en estado Vigente | No puede referenciar directamente un programa de Tipo = Plan anual (ese no genera registros individuales, solo agrupa) | "Que capacitacion especifica recibio o debe recibir esta persona." | Buena practica |
| Tema y modalidad planificada (heredados) | Heredado, solo lectura | Autogenerado | - | - | - | Buena practica |
| Fecha en que recibio la capacitacion | Fecha | Obligatorio antes de marcar Completada | - | No puede ser futura | "Cuando realmente recibio la capacitacion." | OBL-CAP-01 (evidencia esperada: constancias de asistencia, `matriz_obligaciones.json`) |
| Modalidad confirmada | Seleccion unica, heredada y editable | Obligatorio antes de Completada | Mismo catalogo del programa | - | "Confirma como la recibio, por si fue distinto de lo planificado." | Buena practica |
| Constancia o acuse | Archivo, o booleano de acuse electronico dentro del sistema | Obligatorio antes de marcar Completada | - | Debe existir al menos un archivo adjunto o un acuse marcado | "Sube la constancia firmada, o si su empresa usa el acuse electronico dentro del sistema, marquelo aqui." | OBL-CAP-01; OBL-PRIN-03 (responsabilidad demostrada) |
| Resultado de evaluacion | Seleccion unica | Opcional (funcionalidad diferida a V1/V2, ver seccion Q) | No evaluado / Aprobado / No aprobado | - | "Si su empresa aplica una evaluacion de conocimientos, registre el resultado aqui. En esta version es opcional." | [Opinion de producto, fuera del MVP] |
| Proxima renovacion | Fecha, calculada | Autogenerado si el programa tiene periodicidad de renovacion distinta de "Sin renovacion" | - | Fecha en que recibio la capacitacion + periodicidad del programa relacionado | "Cuando debe repetir esta capacitacion." | Buena practica |
| Estado | Seleccion unica | Obligatorio, valor inicial Programada | Programada / Completada / No asistio / Proxima a vencer / Vencida | Transiciones segun seccion F | "En que estado esta este registro." | Buena practica |
| Origen del registro | Seleccion unica, autogenerado | Obligatorio | Manual / Induccion automatica al alta (MOD-001) / Renovacion automatica (MOD-023) / Asignacion por cambio de rol (MOD-001) / Sugerido por leccion aprendida de un incidente (MOD-013, via tarea en MOD-021) | No editable | "De donde salio este registro: por ejemplo, del alta de un empleado nuevo o de un recordatorio de renovacion." | Buena practica, trazabilidad |

**Precarga.** El nombre, correo, cargo, area y rol o roles de la Persona (D.2) se precargan por referencia desde MOD-001, nunca se duplican. El tema, modalidad y version del material de un TrainingRecord se precargan desde el TrainingProgram relacionado y son editables solo si la ejecucion real difirio de lo planificado. Cuando un TrainingRecord corresponde a la persona con rol Delegado de Proteccion de Datos (o Responsable interno), el sistema lo marca automaticamente como insumo disponible para los campos `fecha_ultima_capacitacion_delegado` y `atestados_reverificacion` de MOD-002 (ver seccion G, automatizaciones 8 y 9), sin duplicar esos campos: MOD-017 conserva el registro original, MOD-002 solo referencia o adjunta la constancia.

**Minimizacion de datos personales.** TrainingProgram y TrainingRecord son, por diseno, metadatos sobre la formacion del personal interno de la empresa cliente, nunca datos personales de titulares externos. El unico dato de persona natural que aparece es la referencia al usuario capacitado (nombre, correo, area, rol, todos ya administrados por MOD-001) y, cuando aplica, el nombre de quien elaboro el plan anual. El texto de ayuda del campo "Constancia o acuse" advierte explicitamente que no se adjunte el expediente laboral completo, contratos, evaluaciones de desempeno ni otra documentacion de RRHH ajena a la capacitacion: solo la constancia, lista de asistencia o certificado especifico de esa sesion, en linea con el anti-feature 8 de `22_anti_features.md` ("no copiar o centralizar la base de datos completa del cliente") aplicado aqui al expediente de RRHH.

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Tarea "Completar induccion de [persona]" | Referencia al TrainingRecord de tipo Induccion, fecha limite sugerida | Tarea en MOD-021 (tipo Capacitacion) | Al darse de alta un nuevo usuario en MOD-001 | Responsable de area (RRHH), copia a la persona nueva |
| Tarea "Renovar capacitacion: [tema] - [persona]" | Referencia al TrainingRecord vencido o proximo a vencer | Tarea en MOD-021 | Al entrar en estado Proxima a vencer | La persona, copia al Responsable de area |
| Tarea "Elaborar/actualizar el plan anual de capacitacion e induccion" | Recordatorio del ciclo anual, con el plan anterior como referencia si existe | Tarea en MOD-021 | 60 y 30 dias antes del vencimiento del ciclo anual, o si nunca existio un plan publicado | Delegado de Proteccion de Datos (o Responsable interno) |
| Tarea sugerida "Evaluar capacitacion por leccion aprendida" | Referencia al incidente de origen (MOD-013) | Tarea en MOD-021 (tipo Capacitacion, origen MOD-013) | Al cerrarse un incidente con leccion aprendida que senala necesidad de capacitacion | Delegado, Responsable de Seguridad/IT |
| Constancia individual verificable | Persona, tema, fecha, version del material, archivo o acuse | Evidencia en MOD-019 | Al completarse cada TrainingRecord | Centro de Evidencias (consumo interno del sistema) |
| Documento "Plan anual de capacitacion e induccion" publicado | Periodo, programas incluidos, induccion de personal nuevo, elaborado por, fecha | Documento versionado (MOD-008) mas evidencia con verificacion de integridad (MOD-019) | Al publicarse el TrainingProgram de Tipo = Plan anual | Delegado, Gerencia, Legal, Auditor, MOD-002 (por referencia en `plan_capacitacion_personal`) |
| Notificacion a MOD-002 | Aviso de constancia nueva disponible para `fecha_ultima_capacitacion_delegado` o `atestados_reverificacion` | Notificacion (MOD-022) | Al completarse un TrainingRecord de la persona con rol Delegado | Delegado / Responsable interno (via su propio expediente en MOD-002) |
| Indicador "Personal con capacitacion vigente" | Conteo de personas con registro vigente sobre el total activo | Indicador de dashboard (MOD-020) | Recalculado continuamente | Gerencia, Delegado/Legal, Responsable de area, Auditor |
| Indicador "Inducciones pendientes" | Conteo de personal nuevo sin induccion completada | Indicador de dashboard | Recalculado continuamente | RRHH, Delegado, Gerencia |
| Indicador "Vencimientos proximos" | Conteo de TrainingRecord en estado Proxima a vencer | Indicador de dashboard | Recalculado continuamente | Delegado, Responsable de area |
| Evento de auditoria (AuditLog) | Quien hizo que, cuando | Registro tecnico inmutable | En cada creacion, cambio de campo, cambio de estado, aprobacion o exportacion | Consultado por MOD-019 |

---

## F. Workflow

MOD-017 tiene dos ciclos de estados distintos: el del programa (TrainingProgram, F.1) y el de cada registro individual (TrainingRecord, F.2).

### F.1 TrainingProgram

```
        crear programa
              |
              v
      +---------------+   publicar (Plan anual exige       +-----------+
      |   BORRADOR    |-- elaborado_por con rol Delegado -->|  VIGENTE  |
      +---------------+   y, si aplica, documento           +-----------+
              |            adjunto y aprobacion)                  |
              | descartar                                          | nueva version del
              v                                                    | contenido, o fin
      +---------------+                                            | de vigencia
      |  DESCARTADO   |                                            v
      +---------------+                                     +--------------+
                                                              |  ARCHIVADO   |
                                                              +--------------+
```

Tabla de transiciones (TrainingProgram):

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (nuevo) | Crear programa | Nombre, tipo, tema y publico destinatario completos | Borrador | Administrador, Delegado/Resp. interno, Resp. Legal, Resp. Seguridad/IT (tecnicos), Resp. de area | Evento de creacion en AuditLog |
| Borrador | Descartar | Motivo obligatorio si ya tenia TrainingRecord asociados | Descartado | Quien lo creo, Administrador, Delegado/Resp. interno | Evento en AuditLog; los TrainingRecord ya creados quedan huerfanos y se marcan para reasignacion manual |
| Borrador | Publicar (General, Induccion, Por rol) | Version del material y modalidad completas | Vigente | Quien lo creo, con los mismos roles habilitados para crear | Evento en AuditLog; habilita la creacion de TrainingRecord sobre este programa |
| Borrador (Tipo = Plan anual) | Publicar el plan anual | Elaborado_por con rol Delegado/Resp. interno activo; al menos un programa de tipo Induccion incluido; documento adjunto; aprobacion del rol Aprobador | Vigente | Aprobador (distinto de quien elaboro, salvo pyme con advertencia de autorrevision) | Documento queda en MOD-019 con verificacion de integridad; se notifica a MOD-002 (campo `plan_capacitacion_personal`); se recalcula el recordatorio del proximo ciclo anual |
| Vigente | Nueva version del material, o vencimiento de la vigencia (Plan anual: 1 ano) | Segun el tipo de cambio | Archivado (la version anterior) mas un nuevo Borrador editable a partir de ella | Mismos roles que publicaron | Evento en AuditLog; la version anterior se conserva integra para efectos de evidencia |
| Archivado | (ninguna, es terminal para esa version) | - | - | - | Sigue disponible para consulta y para el historico de TrainingRecord que la referencian |

Estados terminales: Descartado (solo si nunca se publico) y Archivado (por version, no por el programa como concepto, que puede tener una nueva version Vigente). Ninguna version publicada se elimina; una version archivada sigue siendo consultable, igual que exige la evidencia de OBL-CAP-01/02.

### F.2 TrainingRecord

```
   se asigna o se programa
   (manual, induccion, renovacion,
    cambio de rol, o sugerido por incidente)
              |
              v
      +---------------+   se registra fecha,          +---------------+
      |  PROGRAMADA   |   constancia y modalidad ----->|  COMPLETADA   |
      +---------------+                                +---------------+
              |                                                |
              | pasa la fecha programada                       | pasa la periodicidad
              | sin registrar asistencia                       | de renovacion del programa
              v                                                v
      +---------------+                                +------------------+
      |  NO ASISTIO   |                                | PROXIMA A VENCER |
      +---------------+                                +------------------+
              |                                                |
              | se reprograma con nuevo motivo                 | vence sin nuevo registro
              v                                                v
      (vuelve a PROGRAMADA)                            +-----------+
                                                        |  VENCIDA  |----> crea automaticamente
                                                        +-----------+      un nuevo TrainingRecord
                                                                            (PROGRAMADA) para la
                                                                            renovacion
```

Tabla de transiciones (TrainingRecord):

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (nuevo) | Asignar o programar | Persona y programa relacionado existen; el programa esta Vigente | Programada | Administrador, Delegado/Resp. interno, Resp. Legal, Resp. de area, o el sistema (automatizaciones G.1, G.2, G.3) | Evento de creacion en AuditLog; tarea en MOD-021 si aplica |
| Programada | Registrar fecha, constancia y modalidad | Constancia o acuse presente | Completada | La propia persona (autoservicio), Resp. de area, Delegado/Resp. interno | Evidencia registrada en MOD-019; si el programa tiene renovacion, se calcula `proxima_renovacion` |
| Programada | Pasa la fecha programada sin registrar asistencia | Automatico | No asistio | Sistema (automatico) | Alerta WARNING; tarea de reprogramacion |
| No asistio | Reprogramar | Motivo obligatorio | Programada | Resp. de area, Delegado/Resp. interno | Evento en AuditLog con el motivo |
| Completada | Se cumplen los dias de anticipacion antes de `proxima_renovacion` | El programa tiene periodicidad distinta de "Sin renovacion" | Proxima a vencer | Sistema (automatico, via MOD-023) | Alerta segun seccion I; tarea de renovacion |
| Proxima a vencer | Se cumple `proxima_renovacion` sin nuevo registro | Automatico | Vencida | Sistema (automatico) | Alerta HIGH; crea automaticamente un nuevo TrainingRecord Programada para el mismo programa y persona (renovacion) |
| Vencida | (ninguna sobre el registro vencido en si, es terminal) | - | - | - | El nuevo TrainingRecord de renovacion sigue su propio ciclo desde Programada |

Estados terminales: Completada (con renovacion posterior si aplica, sobre un nuevo registro, nunca reescribiendo el anterior) y Vencida (terminal para esa instancia especifica; la renovacion es siempre un registro nuevo, para no perder el historial de que hubo un vencimiento). No asistio no es terminal: siempre se reprograma o queda visible como brecha pendiente en el indicador de la seccion M.

---

## G. Automatizaciones

| # | Disparador | Condicion | Accion | Configurable por la empresa |
|---|---|---|---|---|
| 1 | Se da de alta un nuevo usuario en MOD-001 | Siempre | Crea un TrainingRecord Programada de tipo Induccion de personal nuevo, mas una tarea en MOD-021 con fecha limite sugerida (por defecto 30 dias desde el alta) | Si (los dias de plazo; la creacion del registro en si no se puede desactivar) |
| 2 | Un usuario cambia a un rol con capacitacion por rol asociada (Responsable ARCO-POL, Responsable de Seguridad/IT, RRHH, Marketing) | Existe un TrainingProgram Vigente de Tipo = Por rol para ese rol | Crea un TrainingRecord Programada para ese programa y esa persona | Si (la asociacion entre rol y programa es configurable por la empresa) |
| 3 | Se cumple la fecha de proxima renovacion de un TrainingRecord Completada, menos los dias de anticipacion (por defecto 30) | El programa relacionado tiene periodicidad de renovacion distinta de "Sin renovacion" | Cambia el registro a Proxima a vencer; crea tarea de renovacion en MOD-021 | Si (dias de anticipacion) |
| 4 | Pasa la fecha de `proxima_renovacion` sin un nuevo registro Completada | Automatico | Cambia a Vencida; crea automaticamente un nuevo TrainingRecord Programada para el mismo programa y persona | No el disparo en si; si el plazo de anticipacion previo (fila 3) |
| 5 | Se acerca el aniversario del ultimo Plan anual publicado, o nunca existio uno, bajo bandera `regimen_reforma_659` = ACTUAL | Existe un usuario con rol Delegado/Responsable interno activo en MOD-002 | Crea tarea "Elaborar/actualizar el plan anual de capacitacion e induccion" en MOD-021, a esa persona, a los 60 y a los 30 dias antes del vencimiento del ciclo anual | Si (dias de anticipacion) |
| 6 | La bandera `regimen_reforma_659` de MOD-024 pasa a FUTURO | No hay Delegado voluntario activo (`tipo_rol` distinto de DELEGADO en MOD-002) | El Plan anual vigente se marca "buena practica recomendada" en su ayuda contextual y deja de generar la tarea recordatoria obligatoria de la fila 5; el registro general de OBL-CAP-01 continua exactamente igual | No (regla del doble estado, ver `06_mapa_definitivo_de_modulos.md` seccion 5) |
| 7 | Se cierra un incidente de seguridad en MOD-013 con una leccion aprendida que senala necesidad de capacitacion | El usuario que cierra el caso marca esa opcion en MOD-013 | Crea una tarea sugerida en MOD-021 (tipo Capacitacion, origen MOD-013) para que el Delegado o Responsable de Seguridad/IT valore crear o actualizar un TrainingProgram Por rol; nunca crea el programa por si solo | No (la creacion del programa es siempre una decision humana, ver seccion H) |
| 8 | Se completa un TrainingRecord cuyo programa tiene como rol destinatario a Delegado de Proteccion de Datos | Siempre | Notifica a MOD-002 que hay una constancia nueva disponible para el campo `fecha_ultima_capacitacion_delegado` (OBL-DPO-05); no escribe el campo directamente, solo notifica y deja la referencia disponible | No |
| 9 | Se completa cualquier TrainingRecord de la persona con rol Delegado, dentro de la ventana de su ciclo de reverificacion (3 anos, OBL-DPO-04) | Siempre | Queda disponible como adjunto sugerido cuando MOD-002 inicie el flujo de reverificacion del perfil del delegado | No |
| 10 | Se publica el TrainingProgram de Tipo = Plan anual | Siempre | Notifica a MOD-002 para actualizar por referencia su campo `plan_capacitacion_personal`; envia el documento a MOD-019 con verificacion de integridad | No |

---

## H. Decisiones que NO debe automatizar

- **Si el contenido de un programa de capacitacion satisface realmente lo que exige OBL-CAP-01 o el plan anual de OBL-CAP-02 (calidad y suficiencia pedagogica del contenido).** El sistema solo registra que la capacitacion existio, quien la recibio y con que material; nunca evalua si el contenido es correcto o completo. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada."
- **Si una persona queda exenta de la capacitacion general o de la induccion** (por ejemplo, personal temporal de muy corta duracion, o un rol sin acceso real a datos personales). Es una decision de RRHH o del Delegado, con criterio de negocio; el sistema no la infiere ni la aplica por si solo.
- **Si el Plan anual elaborado por el Delegado es suficiente o completo frente al Art. 22.** El sistema solo verifica que existan los campos minimos (al menos un programa de induccion incluido, documento adjunto), no la suficiencia sustantiva del contenido. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada."
- **Si, bajo el estado FUTURO de la reforma 659, la empresa debe seguir tratando el plan anual como obligatorio porque decidio mantener un Delegado voluntario.** Es una decision de la empresa que se documenta explicitamente en MOD-002 (continuidad voluntaria del Delegado); el sistema no la infiere de otros datos.
- **Si un hallazgo de un incidente (leccion aprendida) realmente exige un nuevo programa de capacitacion, o ya esta cubierto por uno existente.** El sistema solo sugiere la tarea (automatizacion G.7); la decision de crear o ajustar el programa es del Delegado o del Responsable de Seguridad/IT.
- **Aceptar una constancia cargada por la propia persona capacitada como prueba suficiente, sin ningun segundo registro, cuando se trata de la capacitacion especifica del propio Delegado.** El sistema no bloquea el autoservicio (es el mismo patron que usa para cualquier otro empleado), pero no es una decision automatizable si la organizacion, por su tamano, decide exigir un segundo control; esa decision de politica interna queda a criterio de la empresa, no es una exigencia legal expresa, por lo que no lleva el texto de advertencia legal.
- **Decidir si la empresa debe contratar un proveedor externo para impartir una capacitacion en vez de hacerla internamente.** Es una decision de negocio y presupuesto; el sistema no la sugiere ni la exige, solo la registra si ocurre. No es una decision juridica, por lo que no lleva el texto de advertencia legal.

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia o repeticion | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Induccion pendiente de nuevo ingreso | Pasan X dias desde el alta (configurable, por defecto 30) sin TrainingRecord Completada de tipo Induccion | WARNING | Responsable de area (RRHH), copia Delegado | Plataforma y correo | Recordatorio cada 5 dias | Si pasan 30 dias adicionales desde que se activo la alerta (60 dias desde el alta) sin completarse, escala a Administrador | Se completa la induccion |
| Capacitacion proxima a vencer | Entra a Proxima a vencer (N dias antes, por defecto 30) | INFO, sube a WARNING a 5 dias del vencimiento | La persona, copia Responsable de area | Plataforma | Una vez al entrar, recordatorio semanal | Escala al Delegado si faltan menos de 5 dias sin accion | Se completa el nuevo registro o cambia de estado |
| Capacitacion vencida | Pasa la fecha de renovacion sin completar | HIGH | La persona, Responsable de area, copia Delegado | Plataforma y correo | Semanal | Escala al Delegado a los 15 dias | Se completa el nuevo TrainingRecord |
| Plan anual de capacitacion proximo a vencer | Faltan 60 o 30 dias para el aniversario del ultimo plan publicado (o nunca hubo uno), bajo bandera ACTUAL | WARNING | Delegado / Responsable interno | Plataforma y correo | Una vez a los 60 dias, recordatorio a los 30 | Escala a Administrador si no se inicia la elaboracion a los 15 dias de vencido el ciclo | Se publica el nuevo plan anual |
| Plan anual vencido | Paso la fecha del ciclo anual sin nuevo plan publicado, bajo regimen ACTUAL | HIGH | Delegado / Responsable interno, Administrador | Plataforma y correo | Semanal | Escala a Gerencia a los 30 dias. El texto de la alerta advierte que la ausencia del plan anual podria leerse como incumplimiento de la medida organizativa de capacitacion (OBL-CAP-01 / OBL-SEG-02, Art. 56 lit. b num. 7); esta lectura no esta establecida expresamente por la matriz para OBL-CAP-02 en si misma y requiere validacion de asesoria juridica | Se publica el nuevo plan |
| Capacitacion por rol faltante tras cambio de rol | Un usuario cambia a un rol con programa asociado y no se completa el TrainingRecord en X dias (configurable, por defecto 15) | WARNING | Responsable de area, Delegado | Plataforma | Recordatorio cada 5 dias | Escala al Delegado a los 15 dias | Se completa el registro |
| Sugerencia de capacitacion por leccion aprendida sin atender | La tarea de la automatizacion G.7 sigue abierta mas de 15 dias | INFO | Delegado, Responsable de Seguridad/IT | Plataforma | Una vez, recordatorio a los 15 dias | No escala automaticamente (es informativa) | Se marca la tarea como atendida o descartada con motivo |

---

## J. Evidencia

| Que genera o conserva | Como | Obligacion que prueba (OBL-ID) | Conservacion |
|---|---|---|---|
| Constancia individual de cada TrainingRecord Completada | Archivo o acuse electronico, con fecha, usuario, version del material y hash | OBL-CAP-01 (evidencia esperada explicita en `matriz_obligaciones.json`: "Constancias de asistencia"); OBL-PRIN-03 | Criterio provisional: duracion de la relacion laboral + 5 anos (alineado con la plantilla de tratamientos de RRHH de MOD-006, fila 21), hasta que el motor de retencion documental de MOD-016 defina una regla especifica para este tipo de registro |
| Documento del Plan anual de capacitacion e induccion, con version y fecha de publicacion | Documento versionado (MOD-008), con verificacion de integridad al exportarse (MOD-019) | OBL-CAP-02 (evidencia esperada: "Plan anual de capacitacion elaborado por el delegado", "Programa de induccion para personal nuevo") | Mismo criterio provisional que la fila anterior; cada version publicada se conserva integra, sin sobrescritura |
| Historial de cambios de estado de cada TrainingProgram y TrainingRecord | AuditLog | OBL-PRIN-03 | Append-only, igual que el resto del sistema |
| Referencia cruzada hacia MOD-002 (constancias que sirven de insumo a la reverificacion y a la capacitacion especifica del Delegado) | Enlace por referencia, sin duplicar el archivo | OBL-DPO-04, OBL-DPO-05 (propietario MOD-002; MOD-017 aporta la evidencia operativa) | Se conserva junto con el TrainingRecord de origen |
| Evento de auditoria de cada exportacion (listado, plan anual, paquete de evidencia) | AuditLog | OBL-PRIN-03 | Append-only |

Toda esta evidencia se expone tambien, de forma consolidada, en el Centro de Evidencias (MOD-019), con verificacion de integridad en cada exportacion (anti-feature 25 de `22_anti_features.md`).

---

## K. Documentos asociados

- **Documentos requeridos como entrada:** material de capacitacion propio de la empresa (presentaciones, videos, manuales, guias); informe o constancia de la firma o consultor externo, si la capacitacion fue impartida por un tercero.
- **Documentos generados:** Plan anual de capacitacion e induccion (documento formal, generado como borrador que agrega los programas del ano y es editable por el Delegado antes de publicarse); constancia individual de asistencia (plantilla simple); listado consolidado de capacitaciones por persona o por area (exportable).
- **Plantillas que el sistema provee:**
  - "Plan anual de capacitacion e induccion" (variables: periodo, programas incluidos, seccion de induccion de personal nuevo, elaborado por, fecha), marcada explicitamente como borrador que requiere revision y aprobacion de la organizacion antes de considerarse el plan oficial, en linea con el texto de descargo estandar de `04_objetivo_exacto_del_producto.md`, seccion 1.3.
  - "Constancia de asistencia" (variables: persona, tema, fecha, modalidad, version del material), que la empresa puede usar cuando no cuenta con una propia.
- **Anexos y evidencias documentales:** material efectivamente presentado, listas de asistencia firmadas si son fisicas (digitalizadas al adjuntarse), informe de un proveedor externo de capacitacion cuando aplique.

---

## L. Dependencias

```
MOD-001 Organizacion y Personas   ---->  +----------------------------+
   (usuarios, altas, cambios              |                            |
    de rol, areas)                        |   MOD-017 Capacitacion     |  ----> MOD-019 Centro de Evidencias
                                           |   (TrainingProgram +       |
MOD-002 Delegado / Responsable   ---->     |    TrainingRecord)         |  ----> MOD-020 Dashboard y Reportes
Interno de Datos                          |                            |
   (quien elabora el plan anual,          +----------------------------+
    capacitacion especifica propia)               |            ^
                                                    | notifica   | consulta
                                                    v            |
                                              MOD-002 (colaboracion OBL-DPO-04/05,
                                              sin dependencia estructural declarada)

     Capa transversal (consultada, nunca consulta al reves):
     MOD-021 Tareas | MOD-022 Notificaciones | MOD-023 Calendario y Motor de Plazos
     MOD-024 Centro Regulatorio (bandera regimen_reforma_659) | MOD-026 Ayuda

     Colaboracion conceptual sin dependencia de datos automatizada declarada en el mapa:
     MOD-015 Controles de Seguridad (OBL-SEG-02, catalogo de medidas organizativas)
     MOD-013 Incidentes de Seguridad (tareas sugeridas por lecciones aprendidas, via MOD-021)
     MOD-006 RAT y Mapa de Datos (referencia de vocabulario: "Sistema de capacitacion
                                    (MOD-017)" en su plantilla de tratamientos de RRHH)
```

- **Entra desde (dependencia estructural declarada en `mapa_modulos.json`):** MOD-001 (identidad de las personas, altas, bajas y cambios de rol que disparan induccion o capacitacion por rol) y MOD-002 (identidad de quien ocupa hoy el rol Delegado o Responsable interno, requisito para elaborar y publicar el Plan anual).
- **Sale hacia (alimenta_a declarado):** MOD-019 (toda la evidencia de constancias y del Plan anual publicado) y MOD-020 (los indicadores de la seccion M).
- **Consumo del patron transversal general (no es una dependencia especifica declarada en el mapa):** MOD-021 (toda tarea de esta ficha), MOD-022 (toda alerta), MOD-023 (calculo de fechas de renovacion y del ciclo anual), MOD-024 (lectura de la bandera `regimen_reforma_659` para saber si el Plan anual sigue siendo obligatorio), MOD-026 (ayuda contextual).
- **Colaboracion conceptual sin flujo de datos automatizado declarado en el mapa:**
  - **MOD-015** (OBL-SEG-02): una de las seis medidas organizativas del catalogo de controles de MOD-015 es literalmente "Capacitacion del Personal"; MOD-017 es quien produce la evidencia sustantiva de esa medida, en el mismo patron que ya documenta la ficha de MOD-018 para su propia colaboracion con la misma obligacion. Ni `mapa_modulos.json` ni esta ficha declaran un flujo de datos automatizado entre MOD-015 y MOD-017; si una siguiente iteracion decide automatizarlo (por ejemplo, que MOD-015 consulte en vivo el estado de capacitacion), deberia reflejarse tambien en el mapa.
  - **MOD-013** (leccion aprendida de un incidente): la ficha de MOD-013 ya documenta que el cierre de un caso "puede generar tareas hacia MOD-015 (nuevo control) o MOD-017 (necesidad de capacitacion)". Esta ficha satisface esa expectativa con la automatizacion G.7: la tarea siempre pasa por MOD-021 (nunca es una escritura directa de MOD-013 sobre MOD-017), igual patron asimetrico que ya usan MOD-004 y MOD-016 para vinculos declarados solo como tarea.
  - **MOD-006** (vocabulario del RAT): la biblioteca de tratamientos tipicos de MOD-006 (fila 21, "Capacitaciones y evaluaciones de personal") ya usa el nombre "Sistema de capacitacion (MOD-017)" como el sistema donde vive ese tratamiento, con retencion sugerida "Duracion de la relacion + 5 anos". Esta ficha confirma que el vocabulario es compatible (ver seccion J) y que no se requiere una dependencia de datos declarada, porque esa fila del RAT es una plantilla editable que el usuario ajusta a su propio caso, no una integracion en vivo entre ambos modulos.
- **Colaboracion con MOD-002 (OBL-DPO-04, OBL-DPO-05).** Sin ser una dependencia estructural declarada en `mapa_modulos.json` mas alla de la ya existente, MOD-017 notifica a MOD-002 (automatizaciones G.8 y G.9) cuando una constancia de la persona con rol Delegado queda disponible como insumo para sus campos `fecha_ultima_capacitacion_delegado` y `atestados_reverificacion`. Es el mismo patron de "notificacion sin dependencia estructural adicional" que ya documenta la ficha de MOD-018 para su vinculo con MOD-002 por OBL-DPO-07.
- **Que ocurre si un modulo dependiente no existe en el MVP.** MOD-001, MOD-002, MOD-019 y MOD-020 son todos MUST HAVE y existen desde el inicio del recorrido, de modo que no hay aqui un escenario de dependencia invertida. El registro general de capacitacion (OBL-CAP-01) puede operar incluso antes de que el expediente de MOD-002 este completo, porque no depende de la existencia de un Delegado; solo el Plan anual (OBL-CAP-02) requiere que exista una persona con ese rol activo en MOD-002 para poder elaborarse y publicarse.

---

## M. Dashboard

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Personal con capacitacion general vigente | Conteo de personas con al menos un TrainingRecord Completada de Tipo = General con `proxima_renovacion` en el futuro, sobre el total de personal activo en MOD-001, mostrado como "X de Y personas con capacitacion general vigente" | Sin semaforo de porcentaje (se muestra el conteo); amarillo si X es menor a Y; rojo si ademas hay registros en Vencida | Gerencia (solo el conteo), Delegado/Legal (detalle completo), Responsable de area (su area), Auditor (historico) |
| Inducciones pendientes | Conteo de personas dadas de alta hace mas de N dias (configurable) sin TrainingRecord Completada de Tipo = Induccion | Rojo si mayor a 0 y fuera del plazo configurado; amarillo si esta dentro del plazo | RRHH/Responsable de area, Delegado, Gerencia (resumen) |
| Vencimientos proximos (30/60 dias) | Conteo de TrainingRecord en estado Proxima a vencer | Amarillo si hay alguno; rojo si hay alguno a menos de 5 dias de vencer | Delegado, Responsable de area |
| Estado del plan anual de capacitacion e induccion | Campo Estado del TrainingProgram de Tipo = Plan anual mas reciente, cruzado con la bandera `regimen_reforma_659` de MOD-024 | Verde si Vigente y publicado dentro del ciclo; amarillo si Proxima a vencer; rojo si Vencida bajo regimen ACTUAL; gris "No aplica bajo el regimen actual" si FUTURO sin Delegado voluntario | Delegado (detalle), Gerencia (solo el semaforo), Auditor (historico de versiones) |
| Capacitacion por rol cubierta | Conteo de personas con un rol destinatario especifico (ARCO-POL, Seguridad/IT, RRHH, Marketing) que tienen al menos un TrainingRecord Completada del programa Por rol correspondiente, sobre el total de personas con ese rol activo | Amarillo si hay brecha; rojo si la brecha supera un umbral configurable | Responsable de area correspondiente, Delegado |

Ningun indicador de este modulo se expresa como "porcentaje de cumplimiento legal"; el lenguaje siempre es "personal con capacitacion vigente", "inducciones pendientes" o "vencimientos proximos", junto con el banner de descargo estandar del sistema (`04_objetivo_exacto_del_producto.md`, seccion 1.3; anti-feature 5 de `22_anti_features.md`).

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Listado de capacitaciones por persona | Todos los TrainingRecord de una persona, con fecha, tema, constancia | Por persona, por rango de fechas | PDF / XLSX | RRHH, Delegado, Auditor | Si |
| Historial de capacitaciones por area o rol | Conteo y detalle de TrainingRecord agrupados por area o por rol destinatario | Por area, por rol, por periodo | XLSX | Responsable de area, Gerencia | Si |
| Plan anual de capacitacion e induccion (version vigente y anteriores) | Contenido completo del documento, con historial de versiones | Por ano | PDF | Delegado, Auditor, ACE si la requiere | Si |
| Vencimientos e inducciones pendientes | Lista de personas con capacitacion vencida o induccion pendiente | Por estado, por area | CSV | RRHH, Delegado | No (es de gestion interna) |

---

## O. Historial

Eventos que quedan en el historial del modulo y en la auditoria transversal (AuditLog):

- Creacion de un TrainingProgram, con tipo y quien lo creo.
- Cambios de campo de un TrainingProgram (tema, publico, modalidad, periodicidad), con valor anterior y nuevo.
- Cambios de estado de un TrainingProgram (Borrador, Vigente, Archivado, Descartado), con quien lo ejecuto.
- Publicacion del Plan anual, con identidad de quien lo elaboro y de quien lo aprobo.
- Creacion de cada TrainingRecord, con su origen (manual, induccion automatica, renovacion, cambio de rol, sugerido por incidente).
- Cambios de estado de cada TrainingRecord (Programada, Completada, No asistio, Proxima a vencer, Vencida), con fecha y usuario.
- Adjunto de constancia o marca de acuse electronico.
- Notificaciones enviadas a MOD-002 (automatizaciones G.8, G.9, G.10), con fecha y referencia.
- Exportaciones de listados, del Plan anual o del paquete de evidencia, con quien la genero y cuando.

---

## P. Riesgos

- **Riesgo legal:** que la empresa o un tercero interprete una capacitacion completada, o el Plan anual publicado, como una declaracion de que la empresa "cumple" la LPDP en general. Mitigacion de diseno: los reportes y el dashboard usan siempre el lenguaje de "personal con capacitacion vigente" y el banner de descargo estandar, nunca "cumplimiento garantizado" (anti-feature 22 de `22_anti_features.md`).
- **Riesgo legal:** aplicar o descartar el Plan anual de forma incorrecta segun el estado de la reforma 659 (por ejemplo, tratarlo como obligatorio despues de confirmarse el estado FUTURO sin Delegado voluntario, o al reves, descartarlo antes de que la reforma se confirme). Mitigacion de diseno: el campo "Aplica bajo el regimen" (D.1) se calcula siempre a partir de la bandera unica de MOD-024, nunca de una copia local del estado normativo.
- **Riesgo de UX:** una pyme (perfil Karla, `05_tipos_de_usuario.md` seccion 5.1) percibe el registro de capacitaciones como una carga administrativa de RRHH y lo abandona. Mitigacion de diseno: la induccion y la renovacion se crean automaticamente (G.1, G.2, G.4), sin que nadie tenga que recordarlo; el formulario de registro es minimo (persona, tema, fecha, constancia).
- **Riesgo de UX:** el Delegado no sabe que debe elaborar un plan anual formal, distinto de simplemente registrar capacitaciones sueltas. Mitigacion de diseno: la tarea recordatoria (G.5) y la ayuda contextual (seccion R, concepto 2) explican la diferencia de forma explicita.
- **Riesgo operativo:** el calculo de renovacion queda mal hecho si el motor de calendario (MOD-023) esta desactualizado, o si el cambio de rol de una persona no dispara la reasignacion del programa correspondiente. Mitigacion de diseno: toda fecha de renovacion se calcula siempre contra MOD-023, nunca con una fecha fija local; la automatizacion G.2 se dispara desde el propio evento de cambio de rol de MOD-001.
- **Riesgo de seguridad y privacidad:** una constancia adjunta contiene datos excesivos, por ejemplo una copia del contrato laboral completo o de una evaluacion de desempeno, en vez de solo la constancia de esa sesion especifica. Mitigacion de diseno: el texto de ayuda del campo "Constancia o acuse" advierte explicitamente no adjuntar expedientes laborales completos (seccion D.2), y la plantilla de constancia sugerida (seccion K) solo captura los metadatos minimos.
- **Riesgo de separacion de funciones en pyme:** la misma persona crea el programa, se autoasigna la capacitacion y marca su propia constancia como completada sin ningun segundo control, riesgo especialmente sensible cuando se trata de la capacitacion del propio Delegado o de la publicacion del Plan anual. Mitigacion de diseno: la publicacion del Plan anual exige un Aprobador distinto de quien lo elaboro (seccion C), con la misma advertencia de autorrevision por debajo del umbral configurable que usa el resto del sistema (`05_tipos_de_usuario.md`, seccion 5.4).

---

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Registro general de capacitacion del personal (quien, cuando, tema, modalidad, version del material, constancia, proxima renovacion) | X | | | | OBL-CAP-01 es OBLIGATORIO sin condicion; es barato de construir (un formulario y un archivo adjunto) frente al riesgo legal de omitirlo; coherente con la clasificacion global MUST HAVE del mapa |
| Induccion automatica de personal nuevo (mismo mecanismo del registro general, disparada al alta en MOD-001) | X | | | | Mismo costo que el registro general; explicitamente incluida en el alcance del MVP por decision de producto para este modulo, y es la unica forma de que el personal nuevo quede cubierto desde el primer dia |
| Capacitacion por rol (catalogo de programas dirigidos a Responsable ARCO-POL, Responsable de Seguridad/IT, RRHH, Marketing) | X | | | | Usa el mismo mecanismo del registro general, solo categorizado por rol destinatario; reduce un riesgo operativo concreto (por ejemplo, Marketing sin nocion de base juridica) a bajo costo adicional |
| Recordatorio y renovacion automatica (calculo de proxima renovacion, alertas, nuevo registro al vencer) | X | | | | Depende del motor de calendario ya MUST HAVE (MOD-023); sin esto el registro general se volveria una lista estatica que nadie revisa |
| Plan anual de capacitacion e induccion en su version minima (agregacion automatica de los programas del ano, elaborado por el Delegado, con aprobacion separada y exportacion como documento) | X | | | | OBL-CAP-02 es CONDICIONAL, pero hoy el Delegado es obligatorio para toda empresa privada (regimen ACTUAL), por lo que la condicion se cumple de facto para el universo completo de clientes del MVP; la version minima (agregar lo ya registrado, sin herramientas de planificacion avanzada) es barata de construir sobre las mismas entidades del registro general |
| Notificacion de constancias hacia MOD-002 para sus campos de capacitacion y reverificacion del Delegado (OBL-DPO-04, OBL-DPO-05) | X | | | | Bajo costo de implementacion; cierra un vinculo real entre dos obligaciones distintas sin duplicar el dato, y depende de entidades que ya existen en el registro general |
| Herramientas avanzadas de planificacion del plan anual (presupuesto, comparativa entre anos, plantillas por sector o tamano de empresa) | | | X | | Mejora de gestion sobre datos que el MVP ya captura; no es indispensable para que el plan anual minimo cumpla su proposito legal |
| Evaluaciones formales de conocimiento con calificacion | | | | X | El documento maestro lo deja como "a evaluar"; ninguna norma exige evaluar el conocimiento adquirido, solo que hubo capacitacion (OBL-CAP-01) |
| Cursos interactivos y microlearning dentro de la plataforma | | | | X | Convertiria el modulo en un LMS, fuera del alcance funcional de este producto (resolucion explicita del hallazgo 25 de `lente_inconsistencias.md`); no aporta valor legal adicional sobre el registro minimo |
| Certificados generados automaticamente por el sistema | | | | X | Ninguna norma exige un certificado formal, solo una constancia; construirlo ahora seria anticipar una funcionalidad diferenciadora sin urgencia regulatoria |
| Integracion con un proveedor externo de e-learning o LMS | | | | X | Fuera del alcance funcional de este analisis (sin stack ni tecnologias); el sistema solo registraria, como hoy, la constancia que ese proveedor externo entregue |

**Version minima vendible del modulo:** el registro general de capacitacion del personal (formulario minimo con constancia), la induccion automatica de personal nuevo y la capacitacion por rol (mismos campos, solo categorizados), el recordatorio y renovacion automatica, y una version minima del Plan anual de capacitacion e induccion (agregacion de lo ya registrado, elaborada por el Delegado y aprobada por un segundo rol, exportable como documento). Esto ya cubre las dos obligaciones propietarias del modulo (OBL-CAP-01 y OBL-CAP-02) desde el primer dia de uso, sin que el producto se convierta en una plataforma de cursos; las herramientas de planificacion avanzada y todo lo relacionado con evaluar, certificar o impartir contenido interactivo pueden iterar despues sin bloquear ese nucleo.

---

## R. Ayuda contextual (complemento obligatorio)

**1. Que es el registro minimo de capacitacion**
- Que es: dejar constancia de que una persona de su equipo recibio una capacitacion concreta (tema, fecha, quien la dio, que material se uso) y guardar la prueba de que asistio.
- Por que tengo que hacer esto: la Agencia de Ciberseguridad del Estado exige que toda empresa capacite a su personal en proteccion de datos, como una de las medidas organizativas minimas que debe tener implementadas.
- Fundamento: OBL-CAP-01, Politicas de Actuacion ACE, Art. 4, Medidas Organizativas lit. c).
- Cuando necesito ayuda juridica: si no esta seguro de si el contenido que va a usar cubre lo minimo que la empresa necesita, consulte con su asesor legal o con su Delegado.

**2. Que es el plan anual de capacitacion e induccion, y quien debe elaborarlo**
- Que es: un documento que la persona con el rol de Delegado (o Responsable interno) prepara una vez al ano, donde organiza que capacitaciones va a dar la empresa durante ese periodo, incluyendo obligatoriamente un programa de induccion para el personal nuevo que trate datos personales.
- Por que tengo que hacer esto: mientras su empresa tenga un Delegado nombrado, la ley le exige a esa persona elaborar este plan, no solo registrar capacitaciones sueltas sin ninguna planificacion.
- Fundamento: OBL-CAP-02, Lineamientos para el Delegado de Proteccion de Datos Personales, Art. 22, ultimo parrafo.
- Cuando necesito ayuda juridica: si tiene dudas sobre si su empresa todavia esta obligada a tener Delegado (por ejemplo, si escucho sobre una reforma reciente a la ley), consulte con su asesor legal antes de dejar de elaborar este plan.

**3. En que se diferencia esto de la capacitacion propia del Delegado**
- Que es: son dos cosas distintas que se registran en el mismo lugar. Una es el plan que el Delegado prepara para el resto del personal (concepto 2, arriba). La otra es la capacitacion que el Delegado mismo debe recibir, al menos una vez al ano, sobre proteccion de datos y derechos ARCO-POL.
- Por que tengo que hacer esto: confundir ambas cosas puede hacer que su empresa crea que ya cumplio con la capacitacion del Delegado cuando en realidad solo elaboro el plan para los demas, o al reves.
- Fundamento: OBL-CAP-02 (plan anual para el personal, elaborado por el Delegado) frente a OBL-DPO-05 (capacitacion anual que el propio Delegado debe recibir, Art. 22 primer parrafo Lineamientos DPO, obligacion que administra el modulo del Delegado).
- Cuando necesito ayuda juridica: no aplica; es una aclaracion sobre como se organiza el sistema, no una pregunta legal.

**4. Que significa la induccion de personal nuevo**
- Que es: la primera capacitacion que recibe una persona apenas se incorpora a su empresa, antes o al mismo tiempo que empieza a tratar datos personales como parte de su trabajo.
- Por que tengo que hacer esto: el plan anual del Delegado debe incluir expresamente un programa de induccion para el personal nuevo; ademas, es la forma mas eficaz de que alguien no cometa un error evitable en sus primeros dias.
- Fundamento: OBL-CAP-02, Art. 22 ultimo parrafo Lineamientos DPO ("programas de induccion para el personal nuevo").
- Cuando necesito ayuda juridica: no suele requerirlo; si tiene dudas sobre a que personal nuevo especifico aplica (por ejemplo, personal externo o subcontratado), consulte con su Delegado o asesor legal.

**5. Por que este modulo no es una plataforma de cursos**
- Que es: este modulo registra que hubo capacitacion y guarda la constancia; no ofrece cursos interactivos, no aplica examenes con calificacion ni emite certificados.
- Por que tengo que hacer esto: la ley exige que la capacitacion exista y quede documentada, no que se imparta de una forma tecnologica especifica; su empresa puede seguir usando el material y el proveedor que ya tiene, este sistema solo lo organiza y lo respalda.
- Fundamento: OBL-CAP-01 y OBL-CAP-02, ninguna de las dos fija un formato de imparticion.
- Cuando necesito ayuda juridica: no aplica; es una aclaracion sobre el alcance de esta version del producto.

**6. Que pasa con el plan anual si la reforma a la ley entra en vigencia**
- Que es: la Asamblea aprobo una reforma que, si se publica oficialmente, eliminaria la obligacion de tener un Delegado en el sector privado. Mientras eso no se confirme, el plan anual sigue siendo obligatorio para toda empresa con Delegado nombrado.
- Por que tengo que hacer esto: si la reforma se confirma, el plan anual pasa de ser obligatorio a ser una buena practica recomendada, a menos que su empresa decida mantener voluntariamente a la persona en ese rol.
- Fundamento: OBL-CAP-02, afectada por la reforma segun `matriz_obligaciones.json`; doble estado documentado en `06_mapa_definitivo_de_modulos.md`, seccion 5.
- Cuando necesito ayuda juridica: si no esta seguro de si la reforma ya esta vigente o de si su empresa deberia mantener un Delegado de forma voluntaria, consulte con su asesor legal antes de dejar de elaborar el plan.

---

## Nota final del agente (desacuerdos y observaciones sobre las fuentes de diseno)

1. **Discrepancia confirmada entre la ficha resumida del mapa y la fuente primaria para OBL-CAP-02.** Tanto el proposito de MOD-017 en la seccion 3 de `06_mapa_definitivo_de_modulos.md` ("capacitacion especifica anual del Delegado / Responsable Interno") como el campo `notas_reforma_659` de `mapa_modulos.json` ("OBL-CAP-02 (capacitacion especifica del Delegado)") describen esta obligacion de forma imprecisa. El texto exacto de `matriz_obligaciones.json` ("El delegado debe elaborar un plan anual de capacitacion dirigido al personal, que incluya programas de induccion para el personal nuevo") y la fuente primaria verificada en esta ficha (`01_legal/fuentes/lineamientos_dpo_OCR.txt`, Art. 22, ultimo parrafo: "el Delegado elaborara un plan anual de capacitacion dirigido al personal del ente obligado, el cual tambien incluira programas de induccion para el personal nuevo") confirman que OBL-CAP-02 es el plan anual **dirigido al personal**, que el Delegado **elabora**, no la capacitacion que el Delegado recibe para si mismo (eso es OBL-DPO-05, Art. 22 primer parrafo, propietario MOD-002, colaboradora aqui). Esta ficha se diseno segun el texto de la matriz y la fuente primaria, no segun la frase abreviada del mapa; se deja esta nota tal como pide la tarea, sin modificar `06_mapa_definitivo_de_modulos.md` ni `mapa_modulos.json` desde esta ficha.
2. **La clasificacion global MUST HAVE del mapa se mantiene sin cambios.** Esta ficha coincide con `06_mapa_definitivo_de_modulos.md` en que el modulo completo es MUST HAVE, sustentado en que OBL-CAP-01 es OBLIGATORIO y sin condicion. Para la tabla de la seccion Q se tomo una decision adicional, no explicita en el mapa: clasificar tambien como MUST HAVE la version minima del Plan anual de capacitacion e induccion (OBL-CAP-02), pese a que esa obligacion es formalmente CONDICIONAL. La justificacion queda registrada en la propia fila de la tabla: bajo el regimen ACTUAL vigente al 2026-09-24, el Delegado es obligatorio para toda empresa privada sujeta a la LPDP, por lo que la condicion de OBL-CAP-02 se cumple de facto para el universo completo de clientes del MVP, y la version minima del plan (agregacion de lo ya registrado) no tiene costo adicional relevante sobre las mismas entidades del registro general. Se deja explicito para que no se lea como una desviacion silenciosa del test de tres condiciones que usa el mapa definitivo (`06_mapa_definitivo_de_modulos.md`, seccion 2, principio 7).
3. **Expectativas de otras fichas ya escritas, y como se satisfacen.**
   - `MOD-002_ficha.md` declara el campo `plan_capacitacion_personal` como "Referencia a documento (MOD-017/MOD-008)" y el campo `fecha_ultima_capacitacion_delegado`, ademas de describir "Sale hacia MOD-017: la capacitacion especifica anual del Delegado y el plan de capacitacion del personal que el mismo elabora (OBL-CAP-02)". Esta ficha satisface ambas expectativas: el Plan anual se modela como un TrainingProgram de Tipo = Plan anual con su Documento asociado (D.1), referenciable desde `plan_capacitacion_personal`; y la capacitacion especifica del Delegado se modela como un TrainingRecord ordinario cuya constancia se notifica hacia MOD-002 (automatizaciones G.8 y G.9) para sus campos `fecha_ultima_capacitacion_delegado` y `atestados_reverificacion`, sin duplicar esos campos.
   - `MOD-006_ficha.md` (fila 21 de su biblioteca de tratamientos tipicos) ya nombra a "Sistema de capacitacion (MOD-017)" como el sistema donde vive el tratamiento de "Capacitaciones y evaluaciones de personal", con retencion sugerida "Duracion de la relacion + 5 anos". Esta ficha confirma ese vocabulario como compatible (seccion J) y no encontro necesidad de cambiarlo.
   - `MOD-013_ficha.md` declara que el cierre de un incidente con leccion aprendida "puede generar tareas hacia MOD-015 (nuevo control) o MOD-017 (necesidad de capacitacion)". Esta ficha lo satisface con la automatizacion G.7, siempre a traves de una tarea en MOD-021, nunca como una escritura directa entre ambos modulos, coherente con que ni el `depende_de` ni el `alimenta_a` de MOD-013 o de MOD-017 en `mapa_modulos.json` declaran esa relacion como estructural.
   - `MOD-016_ficha.md` no menciona a MOD-017 directamente, pero su patron de "colaboracion conceptual sin dependencia de datos declarada" (por ejemplo, con MOD-009 y MOD-015) es el mismo que esta ficha usa para describir la relacion con MOD-015 (OBL-SEG-02) y con MOD-006.
   - `MOD-018_ficha.md` no menciona a MOD-017 de forma directa, pero su tratamiento de OBL-SEG-02 como colaboracion conceptual con MOD-015 (evidencia sustantiva de una medida del catalogo) es el mismo patron que esta ficha replica para su propia colaboracion con esa obligacion.
   - `MOD-021_ficha.md` ya incluye "MOD-017" en el catalogo de "Modulo de origen" de una tarea y "Capacitacion" en el catalogo de "Tipo de tarea"; esta ficha usa exactamente esos valores en las automatizaciones de la seccion G, sin necesidad de proponer cambios en MOD-021.
4. **Ninguna otra discrepancia detectada frente al mapa definitivo.** Las obligaciones asignadas a MOD-017 en esta ficha (dos propietarias, tres colaboradoras) coinciden exactamente con la tabla de cobertura de la seccion 8 de `06_mapa_definitivo_de_modulos.md` (lineas correspondientes a OBL-CAP-01, OBL-CAP-02, OBL-DPO-04, OBL-DPO-05 y OBL-SEG-02) y con las listas `obligaciones_propietarias` y `obligaciones_colaboradoras` de `mapa_modulos.json`. Las entidades principales (TrainingProgram, TrainingRecord) y las dependencias declaradas (`depende_de`: MOD-001, MOD-002; `alimenta_a`: MOD-019, MOD-020) tambien coinciden y se respetaron sin modificacion.
5. **Correccion aplicada tras revision adversarial (fallo grave confirmado).** La fila "Plan anual vencido" de la seccion I atribuia, sin citar OBL-ID, un riesgo de infraccion del Art. 56 lit. b al incumplimiento de OBL-CAP-02. Se verifico en `matriz_obligaciones.json` que el campo `infracciones_asociadas` de OBL-CAP-02 esta vacio y que el Art. 56 lit. b num. 7 solo esta asociado a OBL-CAP-01 y a OBL-SEG-02. Se corrigio la fila para citar los OBL-ID correctos y marcar la lectura como una interpretacion razonable pero no establecida expresamente por la matriz para OBL-CAP-02, que requiere validacion de asesoria juridica. No hay desacuerdo con el mapa definitivo en este punto: la correccion es sobre una cita de la propia ficha, no sobre `mapa_modulos.json` ni `06_mapa_definitivo_de_modulos.md`.
