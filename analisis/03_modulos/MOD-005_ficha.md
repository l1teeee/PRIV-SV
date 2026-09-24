# MODULO: Plan de Cumplimiento

Codigo corto del modulo: MOD-005
Clasificacion global del modulo: MUST HAVE (para el MVP)
Obligaciones que cubre: OBL-PLAZO-03 (propietaria); OBL-PRIN-01, OBL-PRIN-02 (colaboradoras, obligaciones propias de MOD-006 RAT y MOD-007 Consentimiento que este modulo ayuda a convertir en trabajo concreto)

Fecha de esta ficha: 2026-09-24. Fase: analisis funcional (sin codigo, sin stack, sin base de datos).

Fuentes base de esta ficha: `00_contexto_para_agentes.md`, `00_prompt_analisis_funcional.md`, `02_validacion\06_mapa_definitivo_de_modulos.md`, `02_validacion\mapa_modulos.json`, `02_validacion\02_validacion_de_la_idea.md` (seccion 2.7), `02_validacion\04_objetivo_exacto_del_producto.md`, `02_validacion\05_tipos_de_usuario.md`, `02_validacion\22_anti_features.md`, `01_legal\matriz_obligaciones.md` / `matriz_obligaciones.json`, `01_legal\03_hallazgos_regulatorios.md` (secciones 3, 5, 6, 8, 9) y las secciones del documento maestro `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` relacionadas con el objetivo final del producto (el maestro no desarrolla este modulo como seccion propia; ver nota al final).

---

## A. Proposito

- **Por que existe.** MOD-005 es la bisagra entre "ya sabemos que le aplica a esta empresa" (resultado de MOD-004 Diagnostico de Cumplimiento) y "esto es lo que hay que hacer, quien lo hace y para cuando". Sin este modulo, el diagnostico queda como un cuestionario respondido sin traduccion a trabajo real; es el mecanismo concreto que convierte la ley en tareas, tal como exige el area 10 del prompt de analisis funcional (`00_prompt_analisis_funcional.md`).
- **Que problema resuelve para la empresa.** Una pyme o empresa mediana sin equipo de privacidad dedicado no sabe por donde empezar entre decenas de obligaciones. MOD-005 ordena ese universo en una lista priorizada (critica, importante, recomendada), con responsable, fecha y evidencia esperada por cada accion, para que una persona no especialista pueda ejecutar sin tener que leer la ley articulo por articulo.
- **Obligacion que cubre como propietario.** OBL-PLAZO-03 (Art. 60 inc. 2 LPDP): los sujetos obligados debian adecuarse a las Politicas de Actuacion de la ACE en 3 meses desde su emision; ese plazo transitorio vencio el 2 o 3 de diciembre de 2025, pero la obligacion de adecuacion en si permanece vigente y exigible de forma continua. El Plan de Cumplimiento es, funcionalmente, el instrumento con el que la empresa demuestra que esta ejecutando esa adecuacion; por eso esta obligacion se asigna como propia de este modulo y no de MOD-004 (que solo diagnostica) ni de MOD-019 (que solo archiva evidencia).
- **Obligaciones que cubre como colaborador.** OBL-PRIN-01 (Art. 5 lit. c, consentimiento libre, especifico, informado, expreso e individualizado) y OBL-PRIN-02 (Art. 5 lit. g, seis bases de licitud): MOD-005 no ejecuta estos principios (eso lo hacen MOD-006 RAT y MOD-007 Consentimiento, que los tienen como obligaciones propias), pero garantiza que exista una accion concreta, con responsable y fecha, que obligue a la empresa a documentar la base juridica y el consentimiento de cada tratamiento identificado en el diagnostico. Sin este modulo esos dos principios quedarian como texto legal sin ningun mecanismo que fuerce su ejecucion ordenada.
- **Que valor aporta.**
  - Operativo: convierte una lista de obligaciones abstractas en una lista de tareas concretas, priorizadas y asignadas, ejecutable por personal no especialista.
  - Probatorio: cada version aprobada del plan queda congelada como evidencia fechada de que la organizacion actuo, insumo central del paquete de evidencia para la auditoria anual de cumplimiento de las Politicas ACE (OBL-AUD-01) y para un eventual requerimiento de la ACE.
  - De reduccion de riesgo: prioriza primero las obligaciones con plazo transitorio ya vencido y las de mayor riesgo de infraccion grave o muy grave (ver seccion 6 de `03_hallazgos_regulatorios.md`), en lugar de dejar que la empresa las atienda en el orden en que se le ocurra.
- **Que NO hace este modulo (limites explicitos).**
  - No ejecuta las acciones por si mismo: cada accion se trabaja en su modulo de ejecucion propio (RAT, Documentos, Consentimiento, Proveedores, ARCO-POL, Incidentes, Controles de Seguridad, etc.); MOD-005 solo organiza, prioriza y da seguimiento.
  - No decide si una obligacion aplica a la empresa: esa determinacion la hace el diagnostico guiado de MOD-004 a partir de las respuestas del usuario; MOD-005 solo traduce el resultado ya calculado en acciones.
  - No declara "cumplimiento legal" ni un porcentaje de cumplimiento; solo muestra avance del plan y evidencia disponible (ver seccion M y `04_objetivo_exacto_del_producto.md`, seccion 1.2).
  - No redacta ni aprueba el contenido juridico de los documentos que cada accion dispara (eso es de MOD-008 Documentos y Politicas); MOD-005 solo enlaza la tarea con el documento que debe producirse.
  - No sustituye la asesoria juridica para decidir si una accion puede descartarse como "no aplica"; siempre exige justificacion y, en obligaciones OBLIGATORIO de alto riesgo, una segunda validacion humana (ver seccion H).
- **Doble estado de la reforma 659 en este modulo.** Segun `mapa_modulos.json`, la nota de reforma 659 para MOD-005 es "No aplica directamente": este modulo no tiene contenido propio especifico del Decreto Legislativo 659 (a diferencia de MOD-002 Delegado, que si lo tiene). MOD-005 no decide ni interpreta el estado de la reforma; solo refleja, a traves de las obligaciones que recibe de MOD-004, cualquier cambio de aplicabilidad que el Centro Regulatorio (MOD-024) confirme. En terminos practicos: si el estado FUTURO de la reforma se activa alguna vez, una accion como "Nombrar Delegado de Proteccion de Datos" (ligada a OBL-DPO-01) podria pasar de critica a recomendada u obsoleta, y el sistema la marca para revision humana en lugar de archivarla automaticamente (ver seccion G, regla de recalculo por normativa). El mecanismo de recalculo es generico (sirve para cualquier cambio normativo futuro), no una logica especial de la reforma 659.

## B. Usuarios

Se usan los 12 roles estandar de `02_validacion\05_tipos_de_usuario.md`, seccion 5.3.

| Rol | Para que usa MOD-005 |
|---|---|
| Administrador de la organizacion | Ve el plan completo, dispara la generacion o el recalculo manual, asigna o reasigna responsables, configura los parametros de generacion del plan (seccion D), archiva versiones cuando corresponde. |
| Delegado de Proteccion de Datos (o Responsable interno en estado FUTURO) | Revisa el plan generado antes de que se publique, propone reclasificaciones de prioridad con justificacion, ejecuta y cierra las acciones que la ley le atribuye directamente (por ejemplo, nombrar y comunicar su propio nombramiento), valida los descartes de acciones ligadas a obligaciones OBLIGATORIO. |
| Responsable ARCO-POL / Responsable del tramite | Recibe y ejecuta las acciones relacionadas con establecer o mantener el mecanismo de ejercicio de derechos (por ejemplo, publicar el formulario ARCO-POL). |
| Responsable Legal / Compliance | Revisa el fundamento normativo de cada accion, valida la priorizacion cuando hay ambiguedad legal, aprueba o rechaza justificaciones de descarte de obligaciones OBLIGATORIO. |
| Responsable de Seguridad / IT | Recibe y ejecuta las acciones tecnicas (medidas minimas de las Politicas ACE, catalogo de controles, procedimiento de notificacion de incidentes). |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Recibe las acciones especificas de su area detectadas por el diagnostico (por ejemplo, RRHH recibe la accion de registrar el tratamiento de curriculums; Marketing recibe la de registrar consentimiento de campañas). |
| Aprobador | Aprueba formalmente una version del plan antes de que pase a estado Vigente y genere tareas; sin esta aprobacion el plan queda como borrador interno. |
| Auditor (interno) | Consulta de solo lectura el plan vigente y su historial de versiones, como parte de la auditoria anual de cumplimiento (OBL-AUD-01). |
| Auditor externo (invitado) | Acceso temporal de solo lectura al plan y a la evidencia enlazada, durante la semana de una auditoria puntual. |
| Usuario de consulta / Colaborador | Ve y completa unicamente las acciones que se le asignaron, sin visibilidad del plan completo. |
| Titular (formulario externo) | No aplica: el Plan de Cumplimiento es un instrumento interno de gestion de la empresa; el titular externo no tiene visibilidad ni interaccion con este modulo. |
| Asesor externo invitado | Consulta puntual, acotada a un caso concreto para el que fue invitado, del fundamento normativo y del estado de una accion especifica (por ejemplo, para dictaminar sobre una base juridica dudosa antes de marcarla como completada). |

## C. Permisos

Acciones: ver, generar/recalcular, modificar, reclasificar prioridad, aprobar version, cerrar/completar accion propia, descartar accion, archivar version, exportar, asignar responsable, comentar, adjuntar o referenciar evidencia.

| Accion | Admin. org. | Delegado / Resp. interno | Resp. ARCO-POL | Legal / Compliance | Seguridad / IT | Resp. de area | Aprobador | Auditor interno | Auditor externo | Colaborador | Titular externo | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver plan completo | Si | Si | Solo sus acciones | Si | Solo sus acciones | Solo sus acciones | Si | Si (solo lectura) | Si (temporal, solo lectura) | Solo sus acciones | No aplica | Solo el caso puntual |
| Generar o recalcular el plan | Si | Si | No | No | No | No | No | No | No | No | No aplica | No |
| Modificar campos de una accion (fecha, descripcion, responsable) | Si | Si | No | Si (fundamento y prioridad) | No | No | No | No | No | No | No aplica | No |
| Reclasificar prioridad manualmente | No | Si (con justificacion) | No | Si (con justificacion) | No | No | No | No | No | No | No aplica | No |
| Aprobar version del plan (publicar como Vigente) | No | Propone, no aprueba | No | No | No | No | Si | No | No | No | No aplica | No |
| Cerrar / completar una accion propia con evidencia | No | Si (sus acciones) | Si (sus acciones) | Si (sus acciones) | Si (sus acciones) | Si (sus acciones) | No | No | No | Si (sus acciones) | No aplica | No |
| Descartar accion ("no aplica") | Si (con justificacion) | Si (con justificacion) | No | Si (con justificacion; valida descartes ajenos si la obligacion es OBLIGATORIO) | No (propone, requiere validacion Legal si es critica) | No (propone, requiere validacion Legal si es critica) | No | No | No | No | No aplica | No |
| Archivar version del plan | Si (con motivo) | No | No | No | No | No | No | No | No | No | No aplica | No |
| Exportar plan o reportes | Si | Si | No | Si | No | No | Si | Si | Si (solo lo autorizado) | No | No aplica | No (solo consulta) |
| Asignar o reasignar responsable | Si | Si | No | Si (por criterio legal) | No | No | No | No | No | No | No aplica | No |
| Comentar en una accion | Si | Si | Si (sus acciones) | Si | Si (sus acciones) | Si (sus acciones) | Si | Si (solo lectura de comentarios) | No | Si (sus acciones) | No aplica | Si (en su caso) |
| Adjuntar o referenciar evidencia | Si | Si | Si (sus acciones) | Si | Si (sus acciones) | Si (sus acciones) | No | No | No | Si (sus acciones) | No aplica | No |

**Separacion de funciones y doble control.**

- Quien genera o propone el plan (Administrador, Delegado) nunca es quien lo aprueba como version Vigente: eso exige siempre el rol Aprobador, incluso en pyme donde la misma persona puede ocupar Administrador y Delegado; el sistema no permite que el mismo usuario que propuso el borrador confirme su propia aprobacion sin mostrar la advertencia de "autorrevision" si ademas ocupa el rol Aprobador (consistente con `05_tipos_de_usuario.md`, seccion 5.4).
- Descartar una accion ligada a una obligacion clasificada OBLIGATORIO en la matriz exige doble control: quien la propone (responsable o Delegado) y quien la valida (Legal o Delegado, si el Delegado no fue quien la propuso).
- El rol Auditor (interno o externo) es siempre de solo lectura: nunca puede aprobar, cerrar, descartar ni adjuntar evidencia, para que su verificacion sea independiente.
- Ninguna version del plan se elimina; solo se archiva, con motivo obligatorio, preservando el historial completo (alineado con el anti-feature 19: nadie puede borrar el historial de auditoria).

## D. Informacion de entrada

Entidad principal: **AccionDelPlan** (una fila por cada tarea del plan).

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Titulo de la accion | Texto corto | Obligatorio | - | Maximo 120 caracteres | "Nombre breve de lo que hay que hacer, por ejemplo: Publicar el Aviso de Privacidad en el sitio web." | Buena practica; se redacta a partir de la plantilla de accion asociada a la obligacion |
| Descripcion | Texto largo | Obligatorio | - | Minimo 20 caracteres | "Explica en detalle que hay que hacer y por que, en lenguaje simple, sin tecnicismos legales." | Buena practica |
| Obligacion relacionada | Referencia a otra entidad (catalogo de obligaciones) | Obligatorio | Catalogo de 105 obligaciones OBL-ID de `matriz_obligaciones.json` | Debe existir en el catalogo vigente y estar clasificada como aplicable por el diagnostico | "Indica en que articulo de la ley o de las politicas de la ACE se basa esta tarea." | OBL-ID correspondiente (toda el area del catalogo, segun la obligacion que origino la accion) |
| Modulo de ejecucion | Seleccion unica | Obligatorio, precargado | RAT, Documentos y Politicas, Consentimiento, Proveedores y Encargados, Transferencias Internacionales, ARCO-POL, Incidentes de Seguridad, Riesgos y EIPD, Controles de Seguridad, Retencion y Eliminacion, Capacitacion, Delegado de Proteccion de Datos, Auditoria de Cumplimiento, Organizacion y Personas | Debe ser un modulo existente del sistema | "Indica en que parte del sistema se hace el trabajo real de esta tarea; aqui solo se organiza y se da seguimiento." | Buena practica (enrutamiento funcional entre modulos) |
| Origen del disparo | Seleccion unica | Obligatorio, precargado por el sistema, solo lectura | Respuesta de diagnostico, obligacion con plazo transitorio ya vencido, cambio normativo, resultado de auditoria, alta manual | No editable tras la creacion | "Explica por que esta accion aparecio en su plan." | Buena practica (trazabilidad del origen) |
| Nivel de prioridad | Seleccion unica | Obligatorio, calculado por el sistema, editable con justificacion | Critica, Importante, Recomendada | Si se cambia manualmente, exige diligenciar el campo "Justificacion de repriorizacion" | "Que tan urgente es. Critica: atender de inmediato, riesgo alto o plazo legal ya vencido. Importante: atender en las proximas semanas. Recomendada: buena practica, sin urgencia inmediata." | Motor de priorizacion, ver seccion G |
| Responsable asignado | Referencia a Usuario (catalogo de MOD-001) | Obligatorio antes de pasar a "En curso" | Usuarios activos de la organizacion | Debe tener acceso al modulo de ejecucion correspondiente | "Quien en su empresa va a hacer esta tarea." | Buena practica; el rol sugerido por defecto sigue la matriz de responsabilidades de `05_tipos_de_usuario.md` |
| Fecha objetivo / limite | Fecha | Obligatorio, calculado automaticamente, editable con justificacion si se aparta mucho del default | - | No puede ser anterior a la fecha de generacion del plan | "Para cuando deberia estar lista esta tarea." | Motor de plazos habiles (dependencia operativa con el calendario compartido del sistema); ver seccion G |
| Fecha de inicio real | Fecha | Opcional, se registra automaticamente al pasar a "En curso" | - | No puede ser futura | "Cuando empezo realmente el trabajo." | Buena practica |
| Estado | Seleccion unica | Obligatorio, gestionado por el flujo | Pendiente, En curso, Bloqueada, Vencida, Completada, Descartada, Archivada | Solo se permiten las transiciones de la seccion F | "En que punto va esta tarea." | Buena practica |
| Evidencia esperada | Texto largo | Obligatorio, precargado, editable | Se precarga desde el campo "evidencia_esperada" de la obligacion en la matriz | - | "Que prueba deberia guardar cuando termine, por ejemplo una captura del aviso publicado o el contrato firmado." | Campo `evidencia_esperada` de `matriz_obligaciones.json` |
| Evidencia adjunta o referenciada | Referencia a Evidencia (Centro de Evidencias) | Obligatorio para pasar a "Completada" si la obligacion es OBLIGATORIO | Referencia a un archivo o registro ya cargado en el modulo de ejecucion | Debe existir y estar vinculado a un registro real, no un archivo suelto | "Enlace a la prueba de que se hizo la tarea, guardada donde corresponde; aqui no se sube el archivo otra vez." | OBL-PLAZO-03 (evidencia del plan de adecuacion) |
| Justificacion de repriorizacion manual | Texto largo | Obligatorio solo si se cambio el nivel calculado | - | Minimo 20 caracteres | "Explique por que esta tarea es mas o menos urgente de lo que el sistema calculo." | Buena practica; refuerza la decision H |
| Justificacion de descarte | Texto largo | Obligatorio solo si Estado = Descartada | - | Minimo 20 caracteres; si la obligacion es OBLIGATORIO exige ademas validacion de un segundo usuario | "Explique por que esta obligacion no le aplica a su empresa o por que no se va a ejecutar esta tarea." | Buena practica, apoya la responsabilidad demostrada que exige la ley de forma general |
| Dependencias con otras acciones | Referencia multiple a otra AccionDelPlan | Opcional | Otras acciones del mismo plan | No se permiten dependencias circulares | "Si esta tarea necesita que otra se termine primero, marquela aqui." | Buena practica |
| Notas internas | Texto largo | Opcional | - | - | "Espacio libre para anotaciones de su equipo." | Buena practica |
| Version del plan | Referencia a Plan (version), solo lectura | Obligatorio, generado por el sistema | - | - | "A que version de su plan pertenece esta tarea." | Buena practica (trazabilidad) |
| Fecha de ultima revision | Fecha, solo lectura | Generado por el sistema | - | - | "Ultima vez que alguien reviso o cambio esta tarea." | Buena practica |

**Configuracion de generacion del plan** (parametros a nivel de organizacion, no por accion; todos editables solo por el Administrador y con valores por defecto de producto):

| Campo | Tipo | Obligatorio u opcional | Valor por defecto | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|
| Dias habiles por defecto para accion Critica | Numero | Opcional | 10 dias habiles | "En cuantos dias habiles se sugiere cerrar una accion critica si la ley no fija un plazo propio." | Opinion de producto |
| Dias habiles por defecto para accion Importante | Numero | Opcional | 30 dias habiles | Idem, para acciones importantes | Opinion de producto |
| Dias habiles por defecto para accion Recomendada | Numero | Opcional | 90 dias habiles | Idem, para acciones recomendadas | Opinion de producto |
| Umbral de dias vencida para escalar (Critica) | Numero | Opcional | 5 dias habiles | "Despues de cuantos dias de vencida se avisa a un nivel superior." | Opinion de producto |
| Umbral de acciones criticas vencidas para alerta maxima | Numero | Opcional | 3 acciones | "Cuantas acciones criticas vencidas a la vez disparan la alerta mas alta." | Opinion de producto |

**Precarga.** Los campos Titulo, Descripcion, Obligacion relacionada, Modulo de ejecucion, Origen del disparo y Evidencia esperada se precargan automaticamente a partir del resultado del diagnostico (MOD-004) y del catalogo de obligaciones (`matriz_obligaciones.json`). El campo Responsable asignado sugiere un valor por defecto segun el rol tipicamente responsable de esa obligacion (por ejemplo, las obligaciones del area DPO sugieren al Delegado), tomado del catalogo de roles de MOD-001 y de la matriz de responsabilidades de `05_tipos_de_usuario.md`; el usuario puede reasignarlo. El campo Nivel de prioridad se calcula, no se precarga de otra fuente (ver seccion G).

**Minimizacion de datos.** AccionDelPlan no almacena datos personales de titulares externos (clientes, empleados de clientes, solicitantes ARCO-POL). El unico dato personal presente es la referencia al usuario interno responsable (empleado de la empresa cliente), que ya existe como registro en MOD-001 Organizacion y Personas y aqui solo se guarda como referencia, no se duplica. Ningun campo de este modulo admite adjuntar directamente un dato personal de un titular; toda evidencia se referencia por enlace al modulo de ejecucion donde el control de minimizacion propio de ese modulo ya aplica (por ejemplo, un expediente ARCO-POL vive y se minimiza en MOD-011, el Plan solo apunta a el).

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Plan de Cumplimiento (version vigente) | Lista estructurada de AccionDelPlan con estado, prioridad, responsable y fecha | Vista interactiva en pantalla | Al completar el diagnostico por primera vez y en cada recalculo aprobado | Todos los roles internos, segun su alcance de visibilidad (seccion C) |
| Tareas en el Centro de Tareas (MOD-021) | Una tarea por cada accion en estado Pendiente, con el mismo responsable y fecha limite, enlazada de vuelta al plan | Registro de tarea | Al aprobar una version del plan como Vigente | El responsable asignado a cada accion |
| Alertas de vencimiento y escalamiento | Ver tabla de la seccion I | Notificacion en plataforma y correo (canal por defecto) | Segun el calendario de vencimientos de cada accion | Responsable, Delegado, Administrador, Gerencia (segun nivel) |
| Indicadores para el Dashboard (MOD-020) | Avance del plan, acciones criticas pendientes o vencidas, ultima fecha de recalculo, distribucion por modulo de ejecucion | Indicadores numericos y semaforos | En tiempo real, a partir del estado de las acciones | Gerencia, Responsable, Legal, Auditor, segun su vista (seccion M) |
| Reporte "Plan de Cumplimiento vigente" | Listado completo exportable con fundamento, estado y evidencia esperada de cada accion | PDF / XLSX | Bajo demanda o al aprobar una version | Administrador, Delegado, Legal, Auditor |
| Reporte "Plan de adecuacion" (evidencia OBL-PLAZO-03) | Version historica congelada del plan aprobado en una fecha determinada, con hash de integridad | PDF firmado / ZIP con hash | Al aprobar cada version, o bajo demanda para una auditoria | Auditor interno o externo, ACE (si se requiere) |
| Evento de auditoria (AuditLog transversal) | Registro tecnico de cada creacion, cambio de estado, aprobacion o exportacion, con usuario y fecha | Registro interno, no editable | En cada accion relevante sobre el modulo | MOD-018 Auditoria de Cumplimiento, MOD-019 Centro de Evidencias |

## F. Workflow

MOD-005 tiene dos maquinas de estado relacionadas: la del **Plan** como version completa, y la de cada **AccionDelPlan** dentro de esa version.

### F.1 Estados del Plan (version)

```
  DIAGNOSTICO COMPLETADO (MOD-004)
            |
            v
       [GENERADO] (borrador, v1)
            |
            | enviar a revision (Administrador o Delegado)
            v
      [EN REVISION]
            |
            |-- aprobar (Aprobador) ------------------> [VIGENTE]
            |                                                |
            `-- rechazar, con motivo (Aprobador)              | cambia el diagnostico o
                     |                                        | cambia el estado normativo
                     v                                        v
              [GENERADO] (ajustado)                    [RECALCULANDO]
                                                                |
                                                                | nueva version generada
                                                                v
                                                        [GENERADO] (v+1)
                                                                |
                                             la version VIGENTE anterior pasa a
                                                                v
                                                          [ARCHIVADA]
```

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (ninguno) | Diagnostico completado por primera vez | El diagnostico de MOD-004 llega a estado "completado" | Generado (v1) | Sistema (automatico) | Crea todas las AccionDelPlan calculadas; evento de auditoria "plan generado" |
| Generado | Enviar a revision | El borrador tiene al menos una accion por cada obligacion aplicable | En revision | Administrador, Delegado | Notifica al Aprobador |
| En revision | Aprobar | El Aprobador confirma el contenido | Vigente | Aprobador | Congela snapshot con hash de integridad; crea tareas en MOD-021; notifica a cada responsable; evento de auditoria "plan aprobado" |
| En revision | Rechazar / pedir ajustes | El Aprobador registra el motivo | Generado (mismo borrador editable) | Aprobador | Notifica a quien lo genero, con el motivo visible |
| Vigente | El diagnostico cambia (respuestas modificadas) | Evento recibido desde MOD-004 | Recalculando | Sistema (automatico) | Congela la version Vigente actual como referencia antes de recalcular |
| Vigente | Cambia el estado normativo de una obligacion afectada (por ejemplo, activacion futura de la reforma 659) | El Centro Regulatorio (MOD-024) confirma el cambio y MOD-004 actualiza la aplicabilidad de esa obligacion | Recalculando | Sistema (automatico) | Idem; solo se recalculan las acciones ligadas a la obligacion afectada |
| Vigente | Recalculo manual | Un usuario con permiso lo solicita | Recalculando | Administrador, Delegado | Idem |
| Recalculando | Nueva version generada | El motor de priorizacion terminó de aplicar reglas | Generado (v+1) | Sistema (automatico) | La version Vigente anterior pasa a Archivada; las acciones ya completadas cuya obligacion sigue vigente se preservan y se re-vinculan a la nueva version, no se pierden ni se duplican |
| Generado / En revision / Vigente | Archivar manualmente | Justificacion obligatoria (caso excepcional) | Archivada | Administrador | Evento de auditoria; el plan deja de generar tareas nuevas |

No existe transicion de "eliminar": ninguna version del plan se borra, solo se archiva, preservando el historial completo.

### F.2 Estados de una AccionDelPlan

```
[PENDIENTE] --inicia el responsable--> [EN CURSO] --adjunta evidencia y completa--> [COMPLETADA]
     |                                      |
     | vence la fecha limite                | depende de otra accion no terminada
     v                                      v
 [VENCIDA]                             [BLOQUEADA] --se completa la accion de la que depende--> [EN CURSO]
     |
     | se completa despues de vencida
     v
[COMPLETADA] (marcada con retraso)

[PENDIENTE] o [EN CURSO] o [VENCIDA] --se marca "no aplica" con justificacion--> [DESCARTADA]

[COMPLETADA] o [DESCARTADA] --se archiva la version del plan a la que pertenece--> [ARCHIVADA]
```

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| Pendiente | Iniciar trabajo | El responsable esta asignado | En curso | Responsable, Colaborador | Registra fecha de inicio real |
| En curso | Completar | Adjunta o referencia evidencia; si la obligacion es OBLIGATORIO de alto riesgo, declara explicitamente que la evidencia satisface la tarea | Completada | Responsable (segun el modulo de ejecucion) | Evento de auditoria; actualiza el indicador de avance; si estaba vencida, queda marcada "completada con retraso" |
| En curso | Se detecta dependencia no resuelta | Otra accion de la que depende no esta Completada | Bloqueada | Sistema (automatico) | Alerta al responsable de la accion bloqueada y al de la bloqueante |
| Bloqueada | La dependencia se resuelve | La accion bloqueante pasa a Completada | En curso | Sistema (automatico) | Notifica al responsable que puede continuar |
| Pendiente / En curso | Vence la fecha limite | Fecha actual mayor a la fecha limite y el estado no es terminal | Vencida | Sistema (automatico, motor de plazos) | Alerta segun nivel de prioridad (seccion I); posible escalamiento |
| Pendiente / En curso / Vencida | Marcar "no aplica" | Justificacion obligatoria; si la obligacion es OBLIGATORIO, exige ademas validacion de Legal o Delegado | Descartada | Responsable, con validacion adicional cuando corresponda | Evento de auditoria con el motivo; alerta a Legal si la obligacion queda sin ninguna accion viva |
| Completada / Descartada | Se archiva la version del plan | Automatico al aprobar una version recalculada | Archivada (vinculada a la version archivada) | Sistema (automatico) | Se conserva integramente como evidencia historica |

## G. Automatizaciones

### G.1 Motor de priorizacion (reglas de generacion)

El nivel de prioridad de cada accion se calcula automaticamente al generarse o recalcularse el plan, combinando tres senales que ya existen en la matriz de obligaciones y en el diagnostico. Los umbrales exactos son una decision de producto (marcados [opinion de producto]); los datos de entrada (clasificacion, plazo, infraccion asociada) son juridicos y estan verificados en `matriz_obligaciones.json` y en la seccion 6 de `03_hallazgos_regulatorios.md`.

**Nivel CRITICA** si se cumple alguna condicion:
- (a) La obligacion tiene un plazo transitorio ya vencido (por ejemplo OBL-PLAZO-03, OBL-PLAZO-04); o
- (b) La obligacion esta clasificada OBLIGATORIO en la matriz y su incumplimiento esta asociado a una infraccion GRAVE o MUY GRAVE del Art. 56/57 (ver tabla de la seccion 6 de `03_hallazgos_regulatorios.md`); o
- (c) La obligacion es condicion previa para que otras obligaciones legales puedan cumplirse (por ejemplo, nombrar Delegado o publicar el Aviso de Privacidad, sin los cuales el mecanismo ARCO-POL no puede operar). [opinion de producto en el criterio (c); (a) y (b) usan datos juridicos verificados]

**Nivel IMPORTANTE** si no califica como Critica y se cumple alguna condicion:
- (a) La obligacion esta clasificada OBLIGATORIO pero su infraccion asociada es LEVE, o es una obligacion organizativa sin infraccion directa asociada; o
- (b) La obligacion es CONDICIONAL y el diagnostico confirmo que la condicion aplica a esta empresa (por ejemplo, usa camaras de seguridad, entonces la videovigilancia aplica), sin llegar a los criterios de Critica. [opinion de producto]

**Nivel RECOMENDADA** si no califica como Critica ni Importante:
- (a) La obligacion esta clasificada RECOMENDADO en la matriz; o
- (b) Es una buena practica sin obligacion legal directa mas alla del minimo ya cubierto por otra accion; o
- (c) Es una obligacion CONDICIONAL de plazo lejano o bajo impacto declarado (por ejemplo, la reverificacion del perfil del Delegado a 3 anos). [opinion de producto]

### G.2 Reglas de automatizacion (disparador -> condicion -> accion)

| # | Disparador | Condicion | Accion | Configurable |
|---|---|---|---|---|
| 1 | Diagnostico completado (MOD-004) | No existe una version previa del plan | Generar la primera version del plan aplicando el motor de priorizacion a cada obligacion aplicable | No |
| 2 | Nueva version del plan aprobada como Vigente | Existen acciones en estado Pendiente | Calcular la fecha limite de cada accion con el motor de plazos habiles compartido: si la obligacion tiene plazo legal propio ya vencido, usar fecha de generacion + dias por defecto de su nivel (configuracion de la seccion D); si no tiene plazo legal propio, usar los dias por defecto segun prioridad | Si (dias por defecto por nivel) |
| 3 | Version aprobada como Vigente | Accion en estado Pendiente | Crear una tarea equivalente en el Centro de Tareas (MOD-021), con el mismo responsable y fecha limite, enlazada de vuelta a la accion | No |
| 4 | Fecha actual llega a (fecha limite menos umbral de aviso: 5 dias habiles para Critica, 10 para Importante o Recomendada) | La accion no esta Completada ni Descartada | Enviar alerta WARNING al responsable | Si (umbral de aviso) |
| 5 | Fecha actual supera la fecha limite | La accion no esta Completada ni Descartada | Cambiar estado a Vencida; enviar alerta HIGH (Critica) o WARNING (Importante/Recomendada) | No (el cambio de estado); Si (nivel de alerta asociado) |
| 6 | Accion Critica en estado Vencida por mas del umbral configurado (default 5 dias habiles) | Sigue sin completarse | Escalar alerta a Delegado y Administrador | Si (umbral) |
| 7 | Numero de acciones Criticas Vencidas simultaneas alcanza el umbral configurado (default 3) | - | Enviar alerta CRITICAL a Gerencia (via Aprobador) y marcar el indicador de Dashboard en rojo | Si (umbral) |
| 8 | MOD-004 marca que cambiaron las respuestas del diagnostico y el conjunto de obligaciones aplicables cambio | Existe una version Vigente del plan | Pasar el plan a Recalculando: mantener sin cambios las acciones cuya obligacion sigue aplicando; crear acciones nuevas para obligaciones recien aplicables; marcar como "obligacion ya no aplica, revisar" (nunca archivar automaticamente) las acciones cuya obligacion dejo de aplicar segun el diagnostico | Parcial (el disparo es automatico; el archivado final exige confirmacion humana) |
| 9 | El Centro Regulatorio (MOD-024) confirma un cambio de estado de vigencia sobre una obligacion que ya tiene acciones en el plan Vigente (por ejemplo, activacion del estado FUTURO de la reforma 659) | MOD-004 recalcula la aplicabilidad o los atributos de esa obligacion y emite el evento correspondiente | MOD-005 recalcula unicamente las acciones ligadas a la obligacion afectada, deja el resto de la version Vigente intacta, y notifica a Delegado y Legal para revision antes de publicar la version recalculada | No (el disparo es automatico; la publicacion siempre requiere aprobacion humana, ver seccion H) |
| 10 | Un usuario cambia manualmente el nivel de prioridad calculado | El usuario diligencia la justificacion obligatoria | Registrar el cambio con el nivel anterior, el nuevo y la justificacion en el historial | No |
| 11 | Se detecta que una accion tiene una dependencia declarada que aun no esta Completada | La accion dependiente pasa a estado En curso | Cambiar la accion a Bloqueada y notificar a ambos responsables | No |
| 12 | Accion Bloqueada por mas de 10 dias habiles | Sigue bloqueada | Enviar alerta WARNING al Administrador | Si (umbral) |

## H. Decisiones que NO debe automatizar

Cada una de estas decisiones muestra en pantalla el texto: **"Requiere validacion de la organizacion o asesoria especializada"**.

1. **Confirmar que una obligacion realmente aplica a la empresa** mas alla de lo que el diagnostico automatico detecto, en particular en casos limite de exclusion (Art. 3 LPDP). El sistema no reinterpreta el resultado del diagnostico por su cuenta; si hay duda, la accion queda marcada para revision de Responsable Legal o Delegado antes de descartarse.
2. **Aprobar una version del plan como Vigente.** El sistema nunca publica automaticamente un plan generado o recalculado; siempre requiere la accion explicita del rol Aprobador. Razon: publicar el plan equivale a fijar el compromiso oficial de la organizacion frente a una eventual auditoria, y esa decision no puede quedar en manos de un calculo automatico.
3. **Declarar que una accion "Completada" efectivamente satisface la obligacion legal.** El sistema no infiere cumplimiento por la sola presencia de un archivo adjunto; el responsable debe declarar explicitamente que la evidencia cargada satisface la tarea, con el texto de advertencia visible. Razon: solo una persona de la organizacion puede valorar si el contenido de un documento o control es realmente adecuado para el caso concreto.
4. **Descartar ("no aplica") una accion ligada a una obligacion OBLIGATORIO.** Exige justificacion escrita y, si la obligacion tiene infraccion GRAVE o MUY GRAVE asociada, una segunda validacion de Legal o Delegado. Razon: descartar sin control una obligacion de alto riesgo es la forma mas facil de dejar una exposicion legal real sin que nadie la vea.
5. **Resolver un conflicto entre criterios de priorizacion** (por ejemplo, una obligacion con plazo legal vencido pero que la empresa considera de bajo riesgo real). El algoritmo propone un nivel; reclasificarlo a un nivel distinto siempre exige que una persona (Delegado, Legal o Aprobador) registre el motivo. Razon: el algoritmo usa reglas generales de producto, no conoce el contexto especifico de cada empresa.
6. **Declarar que el plan satisface la obligacion de adecuacion del Art. 60 inc. 2 (OBL-PLAZO-03).** El sistema organiza y evidencia el trabajo realizado; no puede declarar en nombre de la empresa que esta "ya se adecuo" en terminos legales frente a la ACE.

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia o repeticion | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Plan pendiente de aprobacion | Version en estado Generado o En revision por mas de 2 dias habiles | INFO, sube a WARNING tras 2 dias habiles | Aprobador, Administrador | Plataforma + correo | Recordatorio cada 3 dias habiles | A Gerencia tras 5 dias habiles sin aprobar | Al aprobar o rechazar la version |
| Accion proxima a vencer | Fecha limite menos 5 dias habiles (Critica) o menos 10 dias habiles (Importante/Recomendada) | WARNING | Responsable asignado | Plataforma + correo | Diaria hasta vencer o completar | A Delegado si es Critica y quedan 2 dias habiles o menos | Al completar, descartar o cambiar la fecha con justificacion |
| Accion critica vencida | Fecha actual supera la fecha limite y estado no es Completada ni Descartada, obligacion prioridad Critica | HIGH | Responsable, Delegado | Plataforma + correo | Diaria mientras siga vencida | A Administrador/Gerencia tras 5 dias habiles vencida; sube a CRITICAL tras 15 dias habiles | Al completar o descartar con justificacion |
| Multiples acciones criticas vencidas | Conteo de acciones Critica en estado Vencida alcanza el umbral configurado (default 3) | CRITICAL | Administrador, Gerencia (vista Aprobador) | Plataforma + correo | Al cruzar el umbral, luego semanal | No escala mas alla de Gerencia | Cuando el conteo vuelve a estar bajo el umbral |
| Plan desactualizado | Cambiaron respuestas del diagnostico o la normativa aplicable y no se ha recalculado en 5 dias habiles | WARNING | Administrador, Delegado | Plataforma | Recordatorio cada 5 dias habiles | A Legal tras 15 dias habiles sin recalcular | Al recalcular el plan |
| Accion bloqueada por mucho tiempo | Estado Bloqueada por mas de 10 dias habiles | WARNING | Responsable de la accion bloqueada y de la bloqueante | Plataforma | Una vez, luego semanal | A Administrador tras 20 dias habiles | Al resolverse la dependencia |
| Cambio normativo con impacto en el plan | Centro Regulatorio (MOD-024) confirma un cambio de estado sobre una obligacion con acciones activas en el plan | HIGH | Delegado, Legal | Plataforma + correo | Una vez por evento | A Administrador si no se revisa en 10 dias habiles | Al revisar y publicar (o descartar) el recalculo derivado |

## J. Evidencia

| Evidencia | Como se genera | OBL-ID que prueba | Retencion sugerida |
|---|---|---|---|
| Snapshot congelado de cada version Vigente del plan (con hash de integridad) | Automatico al aprobar una version | OBL-PLAZO-03 | Mientras la organizacion sea cliente del sistema, mas 5 anos adicionales tras dar de baja el modulo [opinion de producto, criterio conservador por analogia con el plazo de OBL-RET-05; sin plazo legal especifico propio para el plan en si] |
| Historial de cambios de estado y de prioridad de cada accion (usuario, fecha, valor anterior y nuevo) | Automatico (evento de auditoria transversal) | OBL-PLAZO-03 | Igual que el snapshot del plan al que pertenece |
| Justificaciones de descarte y de repriorizacion manual | Registrado por el usuario al ejecutar la accion | OBL-PLAZO-03 | Igual |
| Registro de aprobacion de cada version (usuario, rol, fecha) | Automatico al aprobar | OBL-PLAZO-03 | Igual |
| Exportacion firmada del plan (PDF/XLSX con hash validable de forma independiente) | Bajo demanda, o automatico al aprobar si la organizacion lo configura | OBL-PLAZO-03 | El archivo exportado conserva su propio hash indefinidamente; sigue ademas la politica de retencion del snapshot del que proviene |

MOD-005 no genera evidencia propia sobre OBL-PRIN-01 y OBL-PRIN-02: esas obligaciones se prueban con la evidencia que MOD-006 (RAT) y MOD-007 (Consentimiento) producen cuando la accion correspondiente del plan se completa; el plan solo referencia esa evidencia, nunca la duplica.

## K. Documentos asociados

- **Documentos requeridos como entrada.** Ninguno directo; el modulo consume el resultado ya calculado del diagnostico (MOD-004) y el catalogo de obligaciones del sistema.
- **Documentos generados.**
  - "Plan de Cumplimiento vigente": listado completo exportable de todas las acciones de la version Vigente.
  - "Plan de adecuacion": version historica congelada de una aprobacion especifica, usada como evidencia puntual de OBL-PLAZO-03 ante una auditoria o un requerimiento de la ACE.
- **Plantillas que el sistema provee.**
  - Plantilla de exportacion "Plan de Cumplimiento": variables `nombre_organizacion`, `fecha_generacion`, `numero_de_version`, `lista_de_acciones` (titulo, obligacion, articulo, prioridad, responsable, fecha limite, estado, evidencia esperada) y el texto de descargo estandar del banner general (ver `04_objetivo_exacto_del_producto.md`, seccion 1.3). No requiere validacion juridica de contenido nuevo (es un reflejo del estado ya registrado en el sistema), pero si requiere el flujo normal de aprobacion (rol Aprobador) antes de considerarse la version oficial vigente.
  - Plantilla de accion por obligacion: texto base de Titulo, Descripcion y Evidencia esperada, precargado desde la ficha de cada obligacion en `matriz_obligaciones.json`, editable por el usuario.
- **Anexos y evidencias documentales.** Ninguno propio; toda evidencia especifica de una accion vive y se adjunta en su modulo de ejecucion, y el plan solo la referencia (ver seccion D).

## L. Dependencias

```
MOD-001 Organizacion y Personas               MOD-004 Diagnostico de Cumplimiento
   (catalogo de usuarios, areas y roles)          (obligaciones aplicables segun
              |                                    las respuestas de la empresa)
              |                                              |
              +----------------------+-----------------------+
                                     |
                                     v
                     [ MOD-005 Plan de Cumplimiento ]
                                     |
                 +-------------------+-------------------+
                 |                                       |
                 v                                       v
     MOD-021 Centro de Tareas                 MOD-020 Dashboard y Reportes
   (una tarea por cada accion Pendiente)      (indicadores de avance del plan)
```

- **Entra desde:**
  - **MOD-004 Diagnostico de Cumplimiento** (dependencia declarada en `mapa_modulos.json`): entrega el conjunto de obligaciones aplicables a la empresa, ya calculado a partir de sus respuestas; es la unica fuente que determina que obligaciones generan una accion.
  - **MOD-001 Organizacion y Personas** (dependencia declarada, ya que MOD-001 alimenta a todos los modulos): entrega el catalogo de usuarios, areas y roles disponibles para asignar como responsables.
  - Catalogo de obligaciones (`matriz_obligaciones.json`): dato de referencia compartido por todo el sistema, no un modulo con interfaz propia; se usa para el fundamento, el articulo y la evidencia esperada de cada accion.
- **Sale hacia (dependencias declaradas en `mapa_modulos.json`):**
  - **MOD-021 Centro de Tareas:** recibe una tarea por cada accion en estado Pendiente de una version Vigente.
  - **MOD-020 Dashboard y Reportes:** recibe los indicadores de avance del plan (seccion M).
- **Relaciones operativas adicionales, sin flecha propia en el mapa definitivo** (se apoyan en las dependencias ya declaradas, no la contradicen): el calculo de fechas limite usa el calendario de dias habiles compartido por todo el sistema; el recalculo por cambio normativo llega a traves de MOD-004 (que si esta declarado como entrada), nunca de forma directa desde el Centro Regulatorio; la evidencia de cada accion completada se consulta despues por MOD-019 Centro de Evidencias y por MOD-018 Auditoria de Cumplimiento a traves del modulo de ejecucion de cada accion, no por una integracion directa de MOD-005 con esos dos modulos.
- **Que ocurre si un modulo dependiente no existe en el MVP.** MOD-004, MOD-001, MOD-021 y MOD-020 estan clasificados MUST HAVE en `mapa_modulos.json`, igual que MOD-005; ninguno de ellos falta en el MVP, por lo que este modulo no necesita un modo degradado. Como salvaguarda operativa, si en algun momento el disparo automatico de recalculo por cambio normativo (regla G.9) no estuviera aun conectado, el recalculo siempre puede dispararse manualmente (regla G del permiso "Generar o recalcular el plan", seccion C).

## M. Dashboard

Nunca se expresa como "porcentaje de cumplimiento legal"; siempre como avance del plan, controles configurados o evidencia disponible (`04_objetivo_exacto_del_producto.md`, seccion 1.2).

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Avance del plan | Acciones en estado Completada / total de acciones de la version Vigente | Verde si mayor a 80%, amarillo entre 50% y 80%, rojo si menor a 50% | Gerencia (resumen), Responsable (su propio avance), Legal (avance por obligacion), Auditor (solo lectura, con fecha de corte) |
| Acciones criticas pendientes o vencidas | Conteo de acciones con prioridad Critica en estado distinto de Completada o Descartada | Rojo si mayor a 0 y alguna esta Vencida; amarillo si hay Pendientes sin vencer; verde si 0 | Gerencia, Responsable, Legal |
| Dias promedio de retraso de acciones vencidas | Promedio de (fecha actual menos fecha limite) sobre las acciones en estado Vencida | Verde si 0, amarillo si menor a 10 dias habiles, rojo si mayor o igual a 10 | Legal, Auditor |
| Acciones por modulo de ejecucion | Conteo de acciones agrupado por el campo Modulo de ejecucion | Sin semaforo, vista de distribucion | Legal, Responsable de area (filtrado a su area) |
| Vigencia de la version actual del plan | Fecha de aprobacion de la version Vigente y numero de version | Amarillo si han pasado mas de 90 dias sin recalculo y hay obligaciones aplicables nuevas segun el diagnostico | Administrador, Delegado, Auditor |

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Plan de Cumplimiento vigente | Listado completo de acciones de la version Vigente, con fundamento, estado y evidencia esperada | Por prioridad, por modulo de ejecucion, por responsable, por estado | PDF, XLSX | Administrador, Delegado, Legal | Si |
| Plan de adecuacion | Version historica congelada de una version aprobada especifica, con hash de integridad | Por version o por rango de fechas de aprobacion | PDF firmado, ZIP con hash | Auditor interno o externo, ACE si se requiere | Si (es el instrumento central de evidencia de OBL-PLAZO-03) |
| Acciones vencidas | Listado de acciones en estado Vencida, con dias de retraso | Por responsable, por modulo, por prioridad | CSV, XLSX | Administrador, Delegado, Legal | Si, como anexo de seguimiento |
| Historial de recalculos del plan | Lista de todas las versiones generadas, con fecha, motivo del recalculo y version anterior archivada | Por rango de fechas | PDF | Auditor, Legal | Si |

## O. Historial

Eventos que quedan registrados en el historial del modulo y en la auditoria transversal (AuditLog):

- Creacion de la primera version del plan (fecha, obligaciones incluidas).
- Cada recalculo (fecha, motivo: cambio de diagnostico o cambio normativo, version anterior archivada).
- Cambios de campo en una AccionDelPlan (valor anterior y nuevo), en particular: cambio de estado, cambio de nivel de prioridad, cambio de responsable, cambio de fecha limite.
- Asignaciones y reasignaciones de responsable.
- Aprobacion o rechazo de una version del plan (usuario, rol, fecha, motivo si fue rechazo).
- Justificaciones de descarte y de repriorizacion manual, con el usuario que las registro y, cuando aplica, el usuario que las valido.
- Adjuntos o referencias de evidencia vinculados a una accion (sin duplicar el archivo, solo el evento de vinculacion).
- Exportaciones del plan o de cualquier reporte (usuario, fecha, formato).
- Accesos de lectura de un Auditor externo invitado (fecha, alcance concedido).
- Archivado de una version del plan (usuario, motivo).

Todos estos eventos prueban principalmente OBL-PLAZO-03 (evidencia continua de la adecuacion) y, de forma colaboradora, sirven de respaldo operativo para que MOD-006 y MOD-007 puedan a su vez evidenciar OBL-PRIN-01 y OBL-PRIN-02 cuando la accion vinculada se completa.

## P. Riesgos

| Riesgo | Tipo | Mitigacion de diseno |
|---|---|---|
| La empresa entiende la priorizacion automatica como una decision legal cerrada, no como apoyo | Legal | Banner de descargo estandar en el plan y en cada exportacion ("Documento generado... requiere revision y aprobacion de su organizacion", `04_objetivo_exacto_del_producto.md` seccion 1.3); texto de ayuda contextual en cada nivel de prioridad (seccion R) |
| Se descarta una accion ligada a una obligacion OBLIGATORIO sin justificacion real, dejando una obligacion sin cobertura | Legal | Justificacion obligatoria y doble validacion para obligaciones OBLIGATORIO de alto riesgo (seccion H, decision 4); alerta a Legal cuando una obligacion queda sin ninguna accion viva |
| Abandono del plan por sobrecarga visual al mostrar 23 o mas acciones de una vez | UX | Agrupacion por prioridad, mostrando primero las acciones Criticas; progresividad (mostrar Importantes y Recomendadas en pestanas separadas); lenguaje simple en titulo y descripcion (seccion D) |
| Fechas limite mal calculadas por un calendario de dias habiles desactualizado | Operativo | Uso obligatorio del motor de plazos habiles compartido por todo el sistema, actualizado anualmente con los asuetos nacionales, nunca un calculo local propio de este modulo |
| El campo "Responsable asignado" expone la estructura organizativa interna a un Auditor externo mas alla de lo necesario para su auditoria puntual | Seguridad y privacidad | El acceso de Auditor externo se concede por invitacion acotada en tiempo y alcance; solo ve nombre y rol del responsable, sin otros datos de contacto personal |
| La empresa percibe el "avance del plan" como garantia de cumplimiento legal | Legal, de producto | El indicador nunca se llama "cumplimiento"; siempre "avance del plan" o "estado del programa", con la nota de descargo visible junto a cualquier metrica (`04_objetivo_exacto_del_producto.md`, seccion 1.3) |
| Una version del plan se pierde o se sobrescribe sin dejar rastro | Operativo, de auditoria | Ninguna version se elimina, solo se archiva; el historial de versiones es de solo adicion (append-only), igual que el resto del AuditLog transversal (anti-feature 19) |

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Generacion automatica del plan tras el diagnostico | X | | | | Es la propuesta de valor central del modulo (seccion A); sin esto el diagnostico no se traduce en trabajo |
| Motor de priorizacion Critica / Importante / Recomendada | X | | | | Necesario para que una empresa sin especialista sepa por donde empezar; obligacion OBL-PLAZO-03 con plazo ya vencido exige orden claro |
| Asignacion de responsable y fecha limite por accion | X | | | | Sin responsable y fecha, el plan es solo una lista, no un plan de trabajo |
| Estados basicos de la accion (Pendiente, En curso, Completada, Vencida) | X | | | | Minimo para dar seguimiento y generar las alertas exigidas por la urgencia comercial (seccion 2.1 de `02_validacion_de_la_idea.md`) |
| Creacion automatica de tareas en el Centro de Tareas (MOD-021) | X | | | | MOD-021 es MUST HAVE y depende de MOD-005; sin esta integracion el responsable no ve su trabajo en un solo lugar |
| Exportacion del plan con hash de integridad ("Plan de adecuacion") | X | | | | Es el instrumento concreto de evidencia de OBL-PLAZO-03 ante una auditoria (decision 2.7.24, integridad verificable) |
| Recalculo manual bajo demanda | X | | | | Complejidad baja, riesgo alto de no tenerlo (plan desactualizado sin forma de corregirlo) |
| Descarte de accion con justificacion y validacion reforzada | X | | | | Evita que una obligacion critica quede sin cobertura silenciosamente (seccion H, decision 4) |
| Recalculo automatico al cambiar respuestas del diagnostico | | X | | | Alto valor pero mayor complejidad de deteccion de cambios; en el MVP el recalculo manual cubre el caso, el automatico reduce friccion despues |
| Recalculo automatico al confirmarse un cambio normativo (Centro Regulatorio) | | X | | | Depende de la madurez de MOD-024; en el MVP el Administrador puede recalcular manualmente al enterarse del cambio |
| Estado Bloqueada por dependencias entre acciones | | | X | | Util en planes grandes (empresa mediana o corporativo); una pyme de 23 acciones puede operar sin dependencias explicitas |
| Historial de versiones completo navegable en pantalla (no solo exportable) | | X | | | Valioso para Auditor y Legal, pero el reporte exportable ya cubre la necesidad minima de evidencia |
| Indicadores avanzados de Dashboard (dias promedio de retraso, distribucion por modulo) | | | X | | Mejora la gestion pero no es indispensable para el primer uso del producto |
| Ponderacion configurable de los criterios de priorizacion por la propia empresa | | | | X | Anadir configurabilidad fina del algoritmo es una mejora de producto madura, no una necesidad del primer cliente |
| Comparacion visual entre versiones del plan (diff) | | | | X | Funcionalidad de conveniencia; el historial exportable ya permite reconstruir la diferencia manualmente |
| Plan consolidado multi-sociedad (grupo corporativo) | | | | X | Coherente con la decision 2.7.31: la gestion de varios sujetos con delegado comun queda fuera del MVP |

**Version minima vendible del modulo.** Generacion automatica del plan, motor de priorizacion de tres niveles, asignacion de responsable y fecha, estados basicos de seguimiento, creacion automatica de tareas y exportacion con integridad verificable. Sin este conjunto minimo, el sistema entrega un diagnostico sin ningun mecanismo que lo convierta en trabajo real, y la empresa pierde exactamente el valor que justifica la urgencia comercial descrita en `02_validacion_de_la_idea.md` (obligaciones con plazo transitorio ya vencido, seccion 2.1).

## R. Ayuda contextual (complemento obligatorio)

**1. Que es el Plan de Cumplimiento**
- Que es: es la lista de tareas que su empresa debe hacer para atender la Ley de Proteccion de Datos, ordenada por urgencia, con quien la hace y para cuando.
- Por que tengo que hacer esto: sin un plan ordenado es facil olvidar obligaciones importantes o dejarlas para despues sin darse cuenta del riesgo.
- Fundamento: Art. 60 inc. 2 LPDP, OBL-PLAZO-03 (adecuacion a las Politicas de Actuacion de la ACE).
- Cuando necesito ayuda juridica: si no esta seguro de si una obligacion listada realmente le aplica a su empresa, o si el plan le parece incompleto frente a su actividad especifica.

**2. Por que las acciones tienen distinta prioridad (Critica, Importante, Recomendada)**
- Que es: el sistema ordena las tareas segun que tan urgentes y riesgosas son, para que usted sepa por donde empezar.
- Por que tengo que hacer esto: atender primero lo critico reduce el riesgo de una multa grave o muy grave y resuelve primero los plazos que ya vencieron.
- Fundamento: clasificacion OBLIGATORIO/RECOMENDADO/CONDICIONAL de `matriz_obligaciones.json` y tabla de infracciones del Art. 56/57 (`03_hallazgos_regulatorios.md`, seccion 6).
- Cuando necesito ayuda juridica: si usted cree que una accion marcada como Critica en realidad no representa un riesgo real para su empresa, antes de reclasificarla consulte con su Delegado o con asesoria legal.

**3. Que significa que una accion este vencida**
- Que es: la fecha sugerida para terminar esa tarea ya paso y la tarea sigue sin completarse.
- Por que tengo que hacer esto: una accion vencida, sobre todo si es Critica, aumenta el riesgo de que la empresa no pueda demostrar que actuo a tiempo si la ACE lo pide.
- Fundamento: buena practica de gestion de plazos; en el caso de OBL-PLAZO-03, el plazo legal original ya vencio (2/3-dic-2025), por lo que la fecha del sistema es una meta interna de recuperacion, no el plazo legal en si.
- Cuando necesito ayuda juridica: si tiene varias acciones criticas vencidas a la vez y no sabe como priorizar entre ellas.

**4. Por que tengo que justificar si marco una accion como "No aplica"**
- Que es: es la forma de decir que esa tarea no corresponde a su empresa, sin simplemente borrarla de la vista.
- Por que tengo que hacer esto: si la obligacion es de las que la ley exige siempre (OBLIGATORIO), descartarla sin explicacion deja una obligacion sin cubrir y sin que nadie lo note despues.
- Fundamento: principio general de responsabilidad demostrada de la LPDP (Art. 5 lit. i); no es una obligacion propia de este modulo, pero orienta por que se exige la justificacion.
- Cuando necesito ayuda juridica: siempre que este descartando una obligacion clasificada como OBLIGATORIO; el sistema le pedira ademas la validacion de otra persona (Legal o Delegado) en esos casos.

**5. Cuando se recalcula el plan**
- Que es: el plan se vuelve a generar cuando cambian las respuestas de su diagnostico (por ejemplo, empieza a usar camaras nuevas) o cuando cambia la normativa aplicable.
- Por que tengo que hacer esto: si su empresa cambia como trata datos personales, las obligaciones que le aplican tambien pueden cambiar, y el plan debe reflejarlo.
- Fundamento: buena practica de mantenimiento del programa de proteccion de datos; no existe un articulo especifico que obligue a "recalcular" un plan, pero si existe la obligacion continua de mantener la adecuacion (OBL-PLAZO-03).
- Cuando necesito ayuda juridica: si un cambio normativo (por ejemplo, la eventual entrada en vigencia de la reforma 659) le genera dudas sobre que obligaciones siguen o dejan de aplicarle.

**6. Que es el "Plan de adecuacion" y por que se me pide como evidencia**
- Que es: es una copia congelada y firmada de una version aprobada de su plan, en una fecha especifica, que usted puede mostrar como prueba de que estaba trabajando en su adecuacion.
- Por que tengo que hacer esto: si la ACE o un auditor le pide evidencia de que su empresa se adecuo a las Politicas de Actuacion, este documento es la prueba concreta y verificable (no editable despues de generado).
- Fundamento: Art. 60 inc. 2 LPDP, OBL-PLAZO-03.
- Cuando necesito ayuda juridica: si recibe un requerimiento formal de la ACE y no sabe que alcance de informacion debe entregar.

---

## Anexo: ejemplo completo de plan para una pyme (23 acciones)

Ejemplo ilustrativo basado en el perfil "Ferreteria y Suministros El Roble, S.A. de C.V." (pyme de aprox. 30 empleados, ver `02_validacion\05_tipos_de_usuario.md`, seccion 5.1), con un diagnostico que detecta: personal en planilla, camaras de seguridad en la tienda, recepcion de curriculums, marketing por WhatsApp y redes sociales, un sistema de facturacion en la nube operado por un proveedor externo, sin biometria y sin transferencias internacionales conocidas. Las fechas se expresan como plazo relativo a la fecha de aprobacion del plan (dia 0), calculado con los valores por defecto de la seccion D.

### 7 acciones CRITICAS

| # | Accion | Obligacion (Art.) | Modulo de ejecucion | Responsable sugerido | Fecha limite | Evidencia esperada |
|---|---|---|---|---|---|---|
| 1 | Adecuarse a las Politicas de Actuacion de la ACE (medidas organizativas y tecnicas minimas) | OBL-PLAZO-03 (Art. 60 inc. 2) | Plan de Cumplimiento (transversal) | Administradora de la organizacion | Dia 0 + 10 dias habiles | Registro del avance de adecuacion y de las demas acciones criticas completadas |
| 2 | Habilitar y publicar un mecanismo operativo para recibir solicitudes ARCO-POL | OBL-PLAZO-04 (Art. 61 inc. 2) | ARCO-POL | Administradora / futura Delegada | Dia 0 + 10 dias habiles | Formulario interno publicado y accesible, con fecha de puesta en marcha |
| 3 | Nombrar formalmente al Delegado de Proteccion de Datos interno | OBL-DPO-01 (Art. 15 y 17) | Delegado de Proteccion de Datos | Administradora de la organizacion | Dia 0 + 10 dias habiles | Acta o resolucion interna de nombramiento |
| 4 | Elaborar y publicar el Aviso de Privacidad con el contenido minimo del Art. 24 | OBL-AVISO-01 (Art. 24) | Documentos y Politicas | Delegada de Proteccion de Datos | Dia 0 + 10 dias habiles | Aviso publicado en el sitio web y en el punto de venta, con version y fecha |
| 5 | Completar el Registro de Actividades de Tratamiento (RAT) de los tratamientos identificados en el diagnostico | OBL-DOC-02 (Politicas ACE, Art. 4, Medidas Organizativas lit. d) | RAT y Mapa de Datos | Delegada de Proteccion de Datos | Dia 0 + 10 dias habiles | RAT con todas las actividades del diagnostico registradas |
| 6 | Implementar las medidas tecnicas minimas de las Politicas ACE (control de acceso, cifrado basico, respaldo de informacion) | OBL-SEG-03 (Politicas ACE) | Controles de Seguridad | Gerente de Tecnologia / proveedor de TI | Dia 0 + 10 dias habiles | Checklist de medidas tecnicas con evidencia adjunta por cada control |
| 7 | Establecer el procedimiento y el canal interno para detectar y notificar vulneraciones de seguridad dentro de 72 horas | OBL-INC-01 (Art. 25) | Incidentes de Seguridad | Gerente de Tecnologia | Dia 0 + 10 dias habiles | Procedimiento documentado y cronometro de 72 horas configurado |

### 8 acciones IMPORTANTES

| # | Accion | Obligacion (Art.) | Modulo de ejecucion | Responsable sugerido | Fecha limite | Evidencia esperada |
|---|---|---|---|---|---|---|
| 8 | Elaborar la Politica de Privacidad interna, consistente con el Aviso de Privacidad publicado | OBL-AVISO-05 (Art. 24, consistencia) | Documentos y Politicas | Delegada de Proteccion de Datos | Dia 0 + 30 dias habiles | Politica de Privacidad aprobada y versionada |
| 9 | Documentar por escrito el procedimiento interno de atencion de solicitudes ARCO-POL | OBL-DOC-01 (Art. 33 inc. 1) | Documentos y Politicas | Delegada de Proteccion de Datos | Dia 0 + 30 dias habiles | Procedimiento documentado con roles y plazos |
| 10 | Registrar y controlar el consentimiento de los clientes que reciben marketing por WhatsApp y redes sociales | OBL-CONS-01 (Art. 26 y 27) | Consentimiento | Encargado de Marketing | Dia 0 + 30 dias habiles | Registro de consentimiento por campana, con fecha y canal |
| 11 | Elaborar el aviso de videovigilancia y registrar la base legal de las camaras de seguridad | OBL-SENS-08 (Art. 4 lit. g) | RAT y Mapa de Datos | Gerente de Tecnologia | Dia 0 + 30 dias habiles | Aviso de videovigilancia visible y registro en el RAT |
| 12 | Firmar contrato o adenda de tratamiento de datos con el proveedor del sistema de facturacion en la nube | OBL-PROV-01 y OBL-PROV-02 (Art. 33 inc. 2, Art. 34) | Proveedores y Encargados | Administradora de la organizacion | Dia 0 + 30 dias habiles | Contrato o adenda firmada con clausulas de proteccion de datos |
| 13 | Impartir la capacitacion inicial en proteccion de datos a todo el personal | OBL-CAP-01 (Politicas ACE) | Capacitacion | Delegada de Proteccion de Datos | Dia 0 + 30 dias habiles | Lista de asistencia o constancia de capacitacion recibida |
| 14 | Definir y registrar el periodo de conservacion del Aviso de Privacidad (10 anos) | OBL-RET-04 (buena practica de retencion documental) | Retencion y Eliminacion | Delegada de Proteccion de Datos | Dia 0 + 30 dias habiles | Politica de retencion documental registrada |
| 15 | Comunicar el nombramiento del Delegado a la ACE dentro de 15 dias habiles desde su designacion | OBL-DPO-03 (Art. 10 Lineamientos DPO) | Delegado de Proteccion de Datos | Delegada de Proteccion de Datos | Dia 0 + 15 dias habiles desde el nombramiento (accion 3) | Constancia de comunicacion enviada a la ACE |

### 8 acciones RECOMENDADAS

| # | Accion | Obligacion (Art.) | Modulo de ejecucion | Responsable sugerido | Fecha limite | Evidencia esperada |
|---|---|---|---|---|---|---|
| 16 | Elaborar un plan anual de capacitacion en proteccion de datos, mas alla del registro minimo | OBL-CAP-02 (buena practica) | Capacitacion | Delegada de Proteccion de Datos | Dia 0 + 90 dias habiles | Plan anual de capacitacion aprobado |
| 17 | Preparar el primer informe periodico del Delegado a la Administradora (minimo dos veces al ano) | OBL-DPO-07 (Art. 30 Lineamientos DPO) | Delegado de Proteccion de Datos | Delegada de Proteccion de Datos | Dia 0 + 90 dias habiles | Informe periodico entregado y registrado |
| 18 | Documentar instrucciones formales al proveedor del sistema de facturacion sobre como debe tratar los datos | OBL-PROV-06 (buena practica) | Proveedores y Encargados | Administradora de la organizacion | Dia 0 + 90 dias habiles | Instrucciones documentadas anexas al contrato |
| 19 | Revisar y documentar el procedimiento de eliminacion segura de documentos fisicos con datos de clientes y empleados | OBL-SEG-05 (Politicas ACE) | Controles de Seguridad | Gerente de Tecnologia | Dia 0 + 90 dias habiles | Procedimiento de eliminacion segura documentado |
| 20 | Realizar una evaluacion de riesgo simplificada para el tratamiento de videovigilancia | OBL-DOC-03 (buena practica, EIPD) | Riesgos y EIPD | Delegada de Proteccion de Datos | Dia 0 + 90 dias habiles | Evaluacion de riesgo registrada con nivel de riesgo residual |
| 21 | Configurar el calendario de dias inhabiles del ano en curso para el motor de plazos | OBL-PLAZO-02 (buena practica operativa) | Calendario y Motor de Plazos | Administradora de la organizacion | Dia 0 + 90 dias habiles | Calendario de asuetos nacionales cargado y vigente |
| 22 | Agendar la reverificacion del perfil del Delegado a 3 anos desde su nombramiento | OBL-DPO-04 (Art. 18 Lineamientos DPO) | Delegado de Proteccion de Datos | Delegada de Proteccion de Datos | Dia 0 + 90 dias habiles (agenda a 3 anos) | Recordatorio programado con fecha de reverificacion |
| 23 | Preparar la carpeta base de evidencia para la primera auditoria anual de cumplimiento de las Politicas ACE | OBL-AUD-01 (Politicas ACE, Art. 8 lit. b) | Auditoria de Cumplimiento | Delegada de Proteccion de Datos | Dia 0 + 90 dias habiles | Indice de evidencia organizado por obligacion |

---

## Nota final: desacuerdos o senalamientos frente al mapa definitivo

- **Recalculo por cambio normativo sin arista directa en el mapa.** `mapa_modulos.json` no declara una dependencia directa entre MOD-024 Centro Regulatorio y MOD-005; el `alimenta_a` de MOD-024 no incluye MOD-005. Para cumplir el requisito explicito de la tarea ("como se recalcula cuando cambian... la normativa") sin contradecir el mapa, esta ficha modela el recalculo como un evento que llega a traves de MOD-004 (que si esta declarado como entrada de MOD-005 y como salida de ningun cambio normativo directo tampoco, pero es el modulo natural donde vive "que obligaciones aplican"). Se recomienda a quien mantenga `06_mapa_definitivo_de_modulos.md` confirmar explicitamente esta cadena (MOD-024 -> MOD-004 -> MOD-005) o, si se prefiere, anadir una arista directa MOD-024 -> MOD-005 en una proxima revision del mapa, para que quede documentada en el nivel transversal y no solo en esta ficha.
- **Coherencia confirmada, no contradicha.** El resto del contenido de esta ficha (proposito, obligaciones propietarias y colaboradoras, clasificacion MVP, notas de reforma 659) es consistente con `mapa_modulos.json` y con `06_mapa_definitivo_de_modulos.md`; no se detectaron errores adicionales que senalar.
