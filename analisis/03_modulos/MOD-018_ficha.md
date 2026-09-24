# MODULO: Auditoria de Cumplimiento

Codigo corto del modulo: MOD-018
Clasificacion global del modulo: SHOULD HAVE
Obligaciones que cubre: OBL-AUD-01 (propietaria); OBL-AUD-02, OBL-DPO-07, OBL-PRIN-03, OBL-SEG-02 (colaboradoras, con propietario en otro modulo)

---

## A. Proposito

- **Por que existe.** Las Politicas de Actuacion y Manejo de Datos Personales de la ACE (N. 001-0309025-DPDP, Art. 8 lit. b) exigen que la empresa realice auditorias anuales para evaluar su propio cumplimiento de esas Politicas. Ningun otro modulo tiene como funcion propia planificar, ejecutar, documentar hallazgos, dar seguimiento a un plan de accion y cerrar formalmente ese ciclo anual: esa es la funcion exclusiva de MOD-018.
- **Distincion clave.** MOD-018 es el programa sustantivo de auditoria (un proceso con alcance, hallazgos, plan de accion y cierre, que ocurre una vez al ano o cuando la empresa decide auditarse), completamente distinto del AuditLog, el registro tecnico e inmutable de acciones del sistema que queda embebido en todos los modulos desde el primer dia de uso. El documento maestro trataba ambas cosas bajo la misma seccion ("29. Auditoria y trazabilidad"); el mapa definitivo las separa de forma explicita (decision 2.7.26 de `02_validacion_de_la_idea.md`, que cierra el faltante de prioridad alta 19: "Programa sustantivo de auditoria anual de cumplimiento... distinto del log tecnico"). MOD-018 consulta el AuditLog como fuente de contexto tecnico, pero nunca lo administra ni lo modifica; el AuditLog no tiene modulo propietario, es una funcion transversal (ver seccion L).
- **Que problema resuelve para la empresa.** Convierte una obligacion legal generica ("hacer una auditoria anual") en un proceso concreto y repetible: cuando toca auditar, que revisar, quien lo hace, que se encontro, que se va a corregir y cuando queda cerrado el ciclo, con el recordatorio automatico anclado a la ultima auditoria registrada para que la empresa nunca pierda de vista cuando le toca la siguiente.
- **Que obligacion u obligaciones cubre (IDs y articulos).**
  - **OBL-AUD-01** (propietaria), Art. 8 lit. b) de las Politicas de Actuacion ACE: obligacion de realizar auditorias anuales para evaluar el cumplimiento de esas Politicas. Nota de precision sobre la fuente: la propia Politica ACE cita como base el Art. 50 lit. l) LPDP, que en realidad faculta a la ACE para auditar las certificaciones que ella misma emite, no para imponer un deber de auditoria interna a las empresas. Esto no invalida la obligacion: el texto expreso del Art. 8 lit. b de la Politica la impone de forma directa como medida organizativa obligatoria, con independencia de si la cita legal que la propia Politica invoca es la mas precisa. El sistema documenta esta precision como una nota de transparencia, nunca como una duda sobre si la obligacion existe.
  - Colabora con **OBL-AUD-02** (Art. 50 lit. j, k, l LPDP, RECOMENDADO), la facultad de la ACE de crear certificaciones o sellos de proteccion de datos para organizaciones y de auditar las que ella misma expida. Al 2026-09-24 la ACE no ha habilitado ningun mecanismo de este tipo para organizaciones (solo un Programa de Certificacion de Delegados, para personas, que tampoco habia entrado en vigencia). MOD-018 no ofrece hoy ninguna funcionalidad de "certificacion", solo deja constancia de que, si la ACE llega a habilitarla en el futuro, el historial de auditorias sustantivas de este modulo seria el insumo natural para solicitarla (ver seccion H y R).
  - Colabora con **OBL-DPO-07** (Art. 30 Lineamientos DPO, CONDICIONAL mientras exista la figura del Delegado, minimo dos veces al ano), el informe periodico del Delegado al responsable. El modulo propietario de ese informe es MOD-002 Delegado / Responsable Interno; MOD-018 le entrega el informe de auditoria cerrado como uno de los insumos que el Delegado o Responsable interno puede citar en su siguiente informe periodico, sin sustituir la obligacion propia de MOD-002 de generar ese informe.
  - Colabora con **OBL-PRIN-03** (Art. 5 lit. i LPDP, responsabilidad demostrada, propietario MOD-019 Centro de Evidencias): el informe y los hallazgos de cada auditoria cerrada son, por si mismos, una de las piezas de evidencia mas fuertes del principio de responsabilidad demostrada, y se registran en MOD-019 al cerrarse la auditoria.
  - Colabora con **OBL-SEG-02** (Art. 4 Politicas ACE, medidas organizativas minimas, propietario MOD-015 Controles de Seguridad): una de las seis medidas organizativas del catalogo de MOD-015 es literalmente "Auditorias de cumplimiento"; MOD-018 es el modulo que produce la evidencia sustantiva de esa medida (el informe de auditoria cerrado, disponible para esa referencia a traves de MOD-019, ver seccion L).
- **Que valor aporta.**
  - Operativo: convierte una obligacion anual abstracta en un proceso con fechas, responsables y checklist, evitando que la primera vez que alguien piense en "la auditoria anual" sea cuando la ACE la pida.
  - Probatorio: es, junto con MOD-019, la pieza mas fuerte de evidencia de responsabilidad demostrada (OBL-PRIN-03) porque documenta una revision propia y periodica del programa completo, no solo evidencia puntual de cada obligacion por separado.
  - De reduccion de riesgo: detecta hallazgos (por ejemplo, controles vencidos en MOD-015 o tratamientos sin base juridica clara en MOD-006) antes de que se conviertan en un incidente o en un hallazgo de una inspeccion de la ACE.
- **Que NO hace este modulo (limites explicitos).**
  - No emite una certificacion ni un sello oficial de la ACE (esa facultad, OBL-AUD-02, es exclusiva de la ACE y hoy no tiene mecanismo habilitado).
  - No sustituye ni actua como el auditor externo del cliente: cuando la auditoria es de tipo Externa, el sistema es la herramienta donde la empresa documenta el ejercicio y adjunta el informe que produjo la firma auditora contratada; MOD-018 no realiza la auditoria por si mismo ni emite una opinion profesional independiente (anti-features 3 y 4 de `22_anti_features.md`).
  - No declara que la empresa "aprobo" o "paso" la auditoria en terminos de cumplimiento legal; solo documenta el alcance revisado, los hallazgos y el estado del plan de accion (anti-feature 5).
  - No decide por si mismo si un hallazgo es grave, si constituye una infraccion sancionable, ni si el plan de accion propuesto es suficiente; esas son decisiones humanas (ver seccion H).
  - No administra el AuditLog: el registro tecnico de acciones del sistema es una funcion transversal embebida en cada modulo, que MOD-018 consulta pero de la que no es propietario (ver `06_mapa_definitivo_de_modulos.md`, seccion 7).

### Nota sobre el doble estado de la reforma 659 en este modulo

Segun el mapa definitivo, la nota de reforma 659 de MOD-018 es "No aplica directamente", y es correcta: OBL-AUD-01 nace de la Politica de Actuacion de la ACE (Art. 8 lit. b), no de los Arts. 15 o 17 LPDP que la reforma modificaria, asi que la obligacion de auditarse cada ano no desaparece ni cambia si la reforma se publica y entra en vigencia. Lo que si cambia, de forma indirecta, es quien aparece por defecto como responsable de coordinar el ciclo de auditoria dentro de la empresa: hoy, en la practica, esa responsabilidad suele recaer en la persona con el rol Delegado de Proteccion de Datos (ver el perfil de Jorge Menendez, `05_tipos_de_usuario.md`, seccion 5.1, que menciona explicitamente "trazabilidad completa para la auditoria anual de cumplimiento" entre sus necesidades). Si el estado FUTURO llega a activarse, ese mismo rol pasa a llamarse "Responsable interno del programa de datos" (`05_tipos_de_usuario.md`, seccion 5.2), sin que el ciclo de auditoria en si mismo cambie de contenido, alcance ni periodicidad. El campo "Responsable de la auditoria" de cada registro de ComplianceAudit conserva el nombre del rol que tenia la persona en el momento de cada auditoria historica, para no reescribir el pasado cuando cambie el estado, el mismo criterio de trazabilidad historica que usa MOD-002.

---

## B. Usuarios

| Rol estandar | Para que usa este modulo |
|---|---|
| Administrador de la organizacion | Planifica el ciclo de auditoria cuando no hay Delegado o Responsable Legal/Compliance designado (tipico en pyme), configura la periodicidad y, en pyme, puede acumular el cierre con advertencia de autorrevision |
| Delegado de Proteccion de Datos (o Responsable interno en estado FUTURO) | Usuario principal del modulo: coordina el ciclo de auditoria, registra o valida hallazgos, da seguimiento al plan de accion, y usa el informe cerrado como insumo de su propio informe periodico al responsable (OBL-DPO-07) |
| Responsable ARCO-POL / Responsable del tramite | No usa este modulo de forma directa; puede recibir una tarea puntual si un hallazgo esta relacionado con el proceso ARCO-POL (por ejemplo, un plazo incumplido detectado en la revision) |
| Responsable Legal / Compliance | Coordina o co-coordina el ciclo junto al Delegado, especialmente en empresa mediana o corporativo; revisa que la calificacion de severidad y la redaccion de la conclusion sean razonables antes del cierre |
| Responsable de Seguridad / IT | Recibe y ejecuta las tareas de correccion de hallazgos relacionados con controles de MOD-015; consulta el checklist de controles precargado para preparar evidencia antes de que inicie la auditoria |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Recibe tareas puntuales de correccion cuando un hallazgo esta relacionado con un tratamiento de su area (por ejemplo, actualizar el RAT de un proceso que cambio) |
| Aprobador | Aprueba el cierre de la auditoria (separado de quien registro los hallazgos) y aprueba cualquier "riesgo aceptado" en vez de correccion |
| Auditor (interno) | Solo lectura: revisa el historico de auditorias cerradas y sus hallazgos como verificacion independiente; nunca registra ni aprueba hallazgos de este modulo, para preservar la independencia de su propia funcion de revision |
| Auditor externo (invitado) | Acceso temporal de solo lectura a la auditoria especifica para la que fue invitado (checklist, hallazgos, evidencia); puede comentar y adjuntar su propio informe como evidencia de esa auditoria puntual |
| Usuario de consulta / Colaborador | Ejecuta unicamente la tarea de correccion que se le asigno desde el plan de accion, sin ver el resto de la auditoria |
| Titular (formulario externo) | No aplica: este modulo no interactua nunca con titulares de datos, es informacion organizativa interna sobre el programa de cumplimiento |
| Asesor externo invitado | Acceso puntual cuando se le invita a dictaminar sobre un hallazgo especifico en disputa (por ejemplo, un abogado externo que opina si un hallazgo sobre una base juridica debil requiere corregirse de inmediato) |

---

## C. Permisos

| Accion | Administrador | Delegado / Resp. interno | Resp. Legal/Compliance | Resp. Seguridad/IT | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Asesor externo invitado |
|---|---|---|---|---|---|---|---|---|---|
| Ver auditorias (lista y detalle) | Si | Si | Si | Si (resumen; detalle de sus hallazgos) | Si | Si (lectura) | Solo la auditoria a la que fue invitado | No (salvo su tarea) | Solo el hallazgo asignado |
| Crear / planificar auditoria | Si | Si | Si | No | No | No | No | No | No |
| Modificar alcance, fechas o tipo (antes de iniciar ejecucion) | Si | Si | Si | No | No | No | No | No | No |
| Registrar o editar un hallazgo | Si (pyme, con advertencia) | Si | Si | No | No | No | No | No | No |
| Aprobar "riesgo aceptado" en vez de corregir un hallazgo | Si (pyme, con advertencia) | No | No | No | Si | No | No | No | No |
| Cerrar auditoria (informe final) | Si (pyme, con advertencia) | No (salvo que tambien tenga rol Aprobador) | No (salvo que tambien tenga rol Aprobador) | No | Si | No | No | No | No |
| Reabrir una auditoria cerrada | Si | Si | No | No | No | No | No | No | No |
| Cancelar una auditoria planificada (nunca eliminar un ciclo ya iniciado) | Si | Si | No | No | No | No | No | No | No |
| Exportar informe o paquete de evidencia | Si | Si | Si | Si (solo lo relacionado con sus controles) | Si | Si | Si (solo lo compartido con el) | No | No |
| Asignar responsable de una accion correctiva | Si | Si | Si | No | No | No | No | No | No |
| Comentar | Si | Si | Si | Si (en hallazgos asignados) | Si | Si | Si (en la auditoria a la que fue invitado) | Si (en su tarea) | Si (en el hallazgo asignado) |
| Adjuntar evidencia | Si | Si | Si | Si (si se le asigna la tarea) | No | No | Si (su propio informe, en la auditoria a la que fue invitado) | Si (en su tarea) | Si (en el hallazgo asignado) |

Separacion de funciones: quien registra los hallazgos de una auditoria (tipicamente Delegado/Responsable interno o Responsable Legal/Compliance) no debe ser la unica persona que aprueba el cierre final del informe, sobre todo si la auditoria encontro hallazgos criticos; por eso "Cerrar auditoria" exige el rol Aprobador, distinto de quien registro los hallazgos, en empresa mediana o corporativo, con la misma advertencia de autorrevision en pyme por debajo del umbral configurable (ver `05_tipos_de_usuario.md`, seccion 5.4). El rol Auditor (interno) es deliberadamente de solo lectura en este modulo, de forma mas estricta que en otros: no puede registrar hallazgos ni aprobar el cierre, porque su valor esta precisamente en revisar de forma independiente lo que otra persona registro, no en autoevaluarse. El Auditor externo (invitado) sigue el mismo patron que en el resto del sistema (acceso de solo lectura al paquete de evidencia, ver `05_tipos_de_usuario.md`, seccion 5.1, perfil 8), con la unica ampliacion de poder adjuntar su propio informe de auditoria como evidencia de la auditoria concreta para la que fue invitado, sin poder editar los hallazgos que la empresa ya registro.

---

## D. Informacion de entrada

Entidad central: **ComplianceAudit**, con dos sub-registros repetibles dentro de cada auditoria: **Hallazgo** y **Accion del plan de accion** (esta ultima referenciada como Task en MOD-021, ver seccion L). El mapa define como entidades principales de este modulo "ComplianceAudit; AuditLog (consultado, embebido en todos los modulos)"; Hallazgo y Accion del plan de accion son sub-estructuras de ComplianceAudit, no entidades independientes con modulo propio.

### D.1 Campos de ComplianceAudit

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Titulo / periodo de la auditoria | Texto corto | Obligatorio | - | No vacio; el sistema sugiere un nombre por defecto | "Ponle un nombre que identifique el periodo, por ejemplo: Auditoria anual 2027." | Buena practica |
| Tipo de auditoria | Seleccion unica | Obligatorio | Interna / Externa (firma contratada) / Mixta | Debe elegir uno | "Interna: la hace tu propio equipo. Externa: la hace una firma que contrataste. Mixta: parte de tu equipo, parte de una firma externa." | Buena practica; la Politica ACE no exige que sea externa (ambiguedad 2, `03_hallazgos_regulatorios.md`, seccion 8) |
| Alcance (obligaciones y modulos revisados) | Seleccion multiple, referencia a OBL-ID y/o modulos | Obligatorio antes de pasar a "En ejecucion" | Catalogo de las 105 obligaciones y de los modulos del sistema | Al menos un elemento | "Elige que partes de tu programa vas a revisar en este ciclo. Si es tu primera auditoria, puedes empezar por las obligaciones marcadas como OBLIGATORIO." | OBL-AUD-01; el alcance exacto no lo fija la Politica, es criterio del producto |
| Periodo cubierto (fecha desde / fecha hasta) | Rango de fechas | Obligatorio | - | Fecha desde anterior a fecha hasta; fecha hasta no futura | "El periodo de tiempo que esta auditoria revisa, normalmente los 12 meses desde la ultima auditoria cerrada." | Buena practica |
| Responsable de la auditoria | Referencia a usuario | Obligatorio | Usuarios con rol Delegado/Responsable interno o Responsable Legal/Compliance | Debe tener uno de esos roles activo | "Quien coordina esta auditoria dentro de tu empresa." | Buena practica |
| Firma auditora externa o auditor invitado | Referencia a usuario con rol Auditor externo (invitado), o texto libre con el nombre de la firma | Obligatorio si Tipo = Externa o Mixta | Usuarios invitados con ese rol | - | "Si contrataste una firma externa, invitala aqui, o anota su nombre si todavia no tiene usuario en el sistema." | Buena practica |
| Checklist base (controles y tratamientos incluidos) | Referencia multiple a Control (MOD-015) y Treatment (MOD-006) | Se precarga automaticamente al iniciar ejecucion, editable | Catalogo vivo de MOD-015 y MOD-006 | - | "Esta es la lista de controles y tratamientos que se van a revisar; el sistema la sugiere a partir de tu catalogo actual, tu puedes ajustarla." | Buena practica |
| Conclusion / resumen ejecutivo | Texto largo | Obligatorio antes de cerrar la auditoria | - | Minimo 50 caracteres | "Resume en pocas lineas que revisaste y que encontraste en general." | Buena practica |
| Informe de auditoria (documento) | Archivo adjunto, o generado por el sistema como borrador | Obligatorio antes de cerrar | - | - | "El informe final de esta auditoria, el que quedaria como evidencia principal ante una revision." | OBL-AUD-01, OBL-PRIN-03 |
| Estado de la auditoria | Seleccion unica | Obligatorio (valor inicial: Planificada) | Planificada / En ejecucion / Hallazgos en revision / Plan de accion en curso / Cerrada / Cancelada | Solo transiciones permitidas por el flujo de la seccion F | "En que etapa del ciclo esta esta auditoria." | Buena practica |
| Fecha de cierre | Fecha (autogenerada al cerrar) | Autogenerado | - | - | "Cuando quedo formalmente cerrada esta auditoria; de aqui se calcula el recordatorio del siguiente ciclo." | OBL-AUD-01 (ancla la periodicidad anual) |

### D.2 Campos de Hallazgo (uno o varios por auditoria)

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Descripcion del hallazgo | Texto largo | Obligatorio | - | Minimo 20 caracteres | "Describe que encontraste, en tus propias palabras." | Buena practica |
| Obligacion o control relacionado | Referencia a OBL-ID, Control (MOD-015) o Tratamiento (MOD-006) | Obligatorio | Catalogo de las 105 obligaciones; catalogo de MOD-015; catalogo de MOD-006 | Al menos una referencia | "A que obligacion, control o tratamiento se relaciona este hallazgo." | OBL-AUD-01 |
| Severidad | Seleccion unica | Obligatorio | Baja / Media / Alta / Critica | El sistema sugiere un valor inicial, la persona puede cambiarlo | "Que tan urgente es corregir esto." | [Opinion de producto] |
| Evidencia del hallazgo | Archivo adjunto o referencia | Opcional (recomendado) | - | - | "Adjunta lo que respalda este hallazgo, por ejemplo una captura del control vencido o del campo faltante en el RAT." | OBL-PRIN-03 |
| Estado del hallazgo | Seleccion unica | Obligatorio (valor inicial: Abierto) | Abierto / En correccion / Corregido / Riesgo aceptado | Solo transiciones permitidas por el flujo de la seccion F | "En que punto esta la solucion de este hallazgo." | Buena practica |

### D.3 Campos de Accion del plan de accion (una o varias por hallazgo)

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Descripcion de la accion correctiva | Texto largo | Obligatorio | - | Minimo 10 caracteres | "Que se va a hacer para corregir el hallazgo." | Buena practica |
| Responsable de la accion | Referencia a usuario | Obligatorio | Usuarios activos de la organizacion | - | "Quien va a ejecutar esta correccion." | Buena practica |
| Fecha limite | Fecha | Obligatorio | - | No puede ser anterior a hoy al crearse | "Para cuando debe estar lista esta correccion." | Buena practica |
| Tarea vinculada en el Centro de Tareas | Referencia automatica a Task (MOD-021) | Autogenerado | - | - | - | Buena practica |

**Campos precargados:** al pasar una auditoria a "En ejecucion", el checklist de controles se precarga desde MOD-015 (estado actual de cada control) y el listado de tratamientos desde MOD-006 (RAT vigente). Si es la primera auditoria de la organizacion, la fecha de "periodo cubierto - desde" se precarga con la fecha de adecuacion inicial registrada durante el diagnostico (MOD-004).

**Minimizacion de datos personales:** ComplianceAudit, Hallazgo y Accion del plan de accion son, por diseno, metadatos sobre el programa de la empresa (que controles, que tratamientos, que obligaciones, que responsables internos), nunca datos personales de titulares externos. El unico dato de persona natural que aparece es el nombre de los usuarios internos responsables (referencia al User de MOD-001, igual que en cualquier otro modulo). El texto de ayuda del campo "Evidencia del hallazgo" advierte explicitamente que no se adjunten capturas ni reportes que contengan datos personales de titulares sin necesidad; por ejemplo, un hallazgo sobre un campo faltante en el RAT no necesita adjuntar una base de datos de clientes, solo la referencia al tratamiento afectado.

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Recordatorio de la proxima auditoria | "Corresponde iniciar la auditoria anual de cumplimiento" | Tarea en MOD-021 y alerta en MOD-022 | Al cumplirse el periodo configurado (por defecto 12 meses) desde el cierre de la ultima auditoria, o desde la fecha de adecuacion inicial si nunca hubo una | Delegado/Responsable interno, Administrador |
| Informe de auditoria cerrado | Alcance, hallazgos, plan de accion y conclusion | PDF | Al cerrar la auditoria | Gerencia, Legal/Delegado, Auditor, Centro de Evidencias (MOD-019) |
| Indicador "Estado de la ultima auditoria" | Planificada / En ejecucion / Hallazgos en revision / Plan de accion en curso / Cerrada / Sin auditoria registrada | Indicador de dashboard (MOD-020) | Recalculado en cada cambio de estado | Gerencia, Legal/Delegado, Auditor |
| Indicador "Hallazgos abiertos" y "Acciones vencidas" | Cuenta por severidad y por vencimiento | Indicador de dashboard | Recalculado en cada cambio | Legal/Delegado, Responsable de Seguridad/IT, Gerencia |
| Tarea de correccion | Una por cada accion del plan de accion | Tarea en MOD-021 | Al registrarse cada accion | Responsable de la accion |
| Evidencia formal del informe | Archivo con hash, version, fecha y responsable | Paquete verificable (MOD-019) | Al cerrar la auditoria | Centro de Evidencias (consumo interno del sistema) |
| Notificacion al Delegado para su informe periodico | Aviso de que hay un informe de auditoria nuevo disponible para citar en el informe periodico (OBL-DPO-07) | Notificacion (MOD-022) | Al cerrar la auditoria | Delegado/Responsable interno |
| Evento de auditoria (AuditLog) | Quien hizo que, cuando | Registro tecnico inmutable | En cada creacion, cambio de campo, cambio de estado, aprobacion o reapertura | Consultado por MOD-019 |

---

## F. Workflow

```
        crear / planificar auditoria
                    |
                    v
          +----------------------+
          |      PLANIFICADA     |
          +----------------------+
             |                |
   iniciar   |                | cancelar (antes de iniciar,
   ejecucion |                | con motivo obligatorio)
             v                v
   +-------------------+   +-----------+
   |   EN EJECUCION    |   | CANCELADA |
   +-------------------+   +-----------+
             |
             | checklist revisado,
             | hallazgos registrados
             v
   +----------------------------+
   |   HALLAZGOS EN REVISION    |
   +----------------------------+
             |
             | hallazgos validados,
             | plan de accion creado
             v
   +----------------------------+
   |  PLAN DE ACCION EN CURSO   | <--------------------------+
   +----------------------------+                            |
             |                                                |
             | todas las acciones en Corregida o              | reabrir (motivo:
             | Riesgo aceptado aprobado; conclusion e          | hallazgo relacionado
             | informe listos; Aprobador confirma el cierre    | posterior, o
             v                                                | requerimiento de la ACE
        +-----------+                                          | sobre ese periodo)
        |  CERRADA  | -----------------------------------------+
        +-----------+
```

Tabla de transiciones:

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (nuevo) | Planificar auditoria | Titulo, tipo, periodo y responsable completos | Planificada | Administrador, Delegado/Resp. interno, Resp. Legal/Compliance | Evento de creacion en AuditLog; si es automatica (recordatorio anual), se crea con fecha sugerida y el alcance del ciclo anterior como plantilla editable |
| Planificada | Iniciar ejecucion | Alcance definido (al menos un elemento) | En ejecucion | Administrador, Delegado/Resp. interno, Resp. Legal/Compliance | Se precarga el checklist desde MOD-015 y MOD-006; evento en AuditLog |
| Planificada | Cancelar | Motivo obligatorio | Cancelada | Administrador, Delegado/Resp. interno | Evento en AuditLog; no cuenta como ciclo cerrado, el recordatorio anual sigue anclado al cierre anterior (o a la adecuacion inicial) |
| En ejecucion | Registrar hallazgos y pasar a revision | Cada elemento del checklist revisado (con o sin hallazgo) | Hallazgos en revision | Delegado/Resp. interno, Resp. Legal/Compliance | Evento en AuditLog por cada hallazgo; el Auditor externo invitado puede comentar y adjuntar su propio informe en esta etapa |
| Hallazgos en revision | Validar hallazgos y crear plan de accion | Cada hallazgo tiene al menos una accion correctiva o un riesgo aceptado justificado | Plan de accion en curso | Delegado/Resp. interno, Resp. Legal/Compliance | Se crea una tarea en MOD-021 por cada accion; alertas segun severidad (seccion I) |
| Plan de accion en curso | Cerrar auditoria | Todas las acciones en Corregida o Riesgo aceptado aprobado; conclusion e informe adjuntos | Cerrada | Aprobador (distinto de quien registro los hallazgos, salvo pyme con advertencia de autorrevision) | Informe queda en MOD-019 con verificacion de integridad; se recalcula el recordatorio del proximo ciclo; notificacion a MOD-002 |
| Cerrada | Reabrir | Motivo obligatorio (por ejemplo, un hallazgo relacionado surgido despues, o un requerimiento de la ACE sobre ese mismo periodo) | Plan de accion en curso | Administrador, Delegado/Resp. interno | Evento de reapertura en AuditLog; el informe anterior se conserva como version historica, no se sobrescribe |

Estados terminales: Cerrada es terminal pero admite reapertura con motivo (el informe anterior no se borra, se versiona, en linea con el anti-feature 19 sobre la bitacora de auditoria); Cancelada es terminal sin reapertura (si la empresa decide auditarse despues de todo, planifica una auditoria nueva). Los hallazgos y acciones vinculados a una auditoria Cancelada quedan archivados como referencia historica, sin generar tareas de plan de accion.

---

## G. Automatizaciones

| Disparador | Condicion | Accion | Configurable por la empresa |
|---|---|---|---|
| Se cierra una auditoria (o, si nunca hubo una, se completa el diagnostico inicial de MOD-004) | Siempre | Crea automaticamente el siguiente registro de ComplianceAudit en estado Planificada, con fecha sugerida = fecha de cierre + periodo configurado, y el mismo alcance del ciclo anterior como plantilla editable | Si (el periodo, hoy 12 meses, es configurable, nunca menor a lo que exige la Politica ACE) |
| Una auditoria pasa a "En ejecucion" | Siempre | Precarga el checklist con los controles de MOD-015 y los tratamientos de MOD-006 vigentes a esa fecha | No |
| Se registra un hallazgo con severidad Alta o Critica | Siempre | Crea automaticamente una tarea de plan de accion en MOD-021, con fecha limite sugerida (15 dias habiles para Critica, 30 para Alta) | Si (los dias sugeridos son configurables) |
| Se registra un hallazgo con severidad Baja o Media | Siempre | Crea la tarea de plan de accion sin fecha limite sugerida automatica; el responsable la define | No |
| Todas las acciones del plan quedan en Corregida o Riesgo aceptado aprobado | Siempre | Habilita el boton "Cerrar auditoria", bloqueado hasta ese momento | No |
| Se cierra la auditoria | Siempre | Genera el informe de auditoria (si no se adjunto uno externo, arma un borrador con conclusion, hallazgos y plan de accion) y lo envia a MOD-019 con verificacion de integridad | No |
| Se cierra la auditoria | Siempre | Notifica al usuario con rol Delegado/Responsable interno que hay un informe nuevo disponible para citar en su proximo informe periodico (OBL-DPO-07) | No |
| Pasan 60 dias desde la fecha sugerida de inicio sin que la auditoria planificada pase a "En ejecucion" | Siempre | Alerta HIGH y escalamiento (ver seccion I) | Si (los dias de tolerancia son configurables) |

---

## H. Decisiones que NO debe automatizar

- **Si un hallazgo constituye o no una infraccion sancionable ante la ACE.** Calificar una conducta como infraccion leve, grave o muy grave del Art. 56 es una facultad exclusiva de la ACE en un procedimiento sancionador; el sistema solo vincula el hallazgo con la obligacion y, si aplica, con el bloque de infraccion asociado en la matriz, pero no declara la calificacion. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada."
- **La severidad final de un hallazgo.** El sistema puede sugerir una severidad inicial a partir de reglas simples (por ejemplo, un hallazgo sobre un control OBLIGATORIO sin evidencia sugiere severidad Alta), pero la persona que registra el hallazgo decide y puede cambiarla, porque el contexto real del negocio no es calculable solo con las reglas del catalogo. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada."
- **Si el alcance de una auditoria es suficiente o adecuado.** El sistema sugiere un alcance por defecto (las obligaciones OBLIGATORIO), pero no puede decidir si eso es lo que la empresa realmente necesita revisar ese ano; eso es un criterio profesional de quien coordina la auditoria, interno o firma externa. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada."
- **Aceptar un riesgo en vez de corregir un hallazgo (estado "Riesgo aceptado").** El sistema nunca cierra automaticamente un hallazgo como riesgo aceptado; siempre requiere que una persona con rol Aprobador lo apruebe explicitamente, porque dejar un hallazgo sin corregir es una decision de negocio con consecuencias legales potenciales. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada."
- **Cerrar la auditoria con hallazgos criticos aun abiertos.** El sistema bloquea el boton de cierre mientras existan hallazgos Criticos sin resolver ni riesgo aceptado aprobado; forzar el cierre en ese estado exige una decision explicita y documentada del Aprobador, nunca ocurre por defecto ni por vencimiento de plazo. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada."
- **Si la empresa deberia contratar una auditoria externa en vez de hacerla internamente.** Es una decision de negocio y de presupuesto de la empresa; el sistema no la sugiere ni la exige, solo la registra si ocurre. No es una decision juridica, por lo que no lleva el texto de advertencia legal.
- **Si el historial de auditorias equivale a una certificacion de la ACE (OBL-AUD-02).** El sistema nunca presenta el cierre de una auditoria interna como si fuera una certificacion o sello oficial; mientras la ACE no habilite ese mecanismo, cualquier mencion a "certificacion" queda fuera del alcance de este modulo. Texto de advertencia (en la ayuda contextual): "La ACE aun no ha habilitado ningun mecanismo de certificacion para organizaciones; esta auditoria es un ejercicio interno de su empresa, no una certificacion oficial."

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia o repeticion | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Recordatorio de proxima auditoria | Faltan 60 dias para la fecha sugerida | INFO | Delegado/Resp. interno, Administrador | Plataforma | Una vez | No escala | Se planifica la auditoria |
| Auditoria proxima a vencer | Faltan 15 dias para la fecha sugerida y sigue sin planificarse | WARNING | Delegado/Resp. interno, Resp. Legal/Compliance | Plataforma y correo | Cada 5 dias | Si no se planifica, escala al Administrador | Se planifica la auditoria |
| Auditoria vencida | Paso la fecha sugerida sin que la auditoria pase a "En ejecucion" | HIGH | Delegado/Resp. interno, Administrador | Plataforma y correo | Semanal | Si sigue sin iniciar a los 60 dias, escala a Gerencia con referencia al riesgo de infraccion grave (Art. 56 lit. b, OBL-AUD-01) | Se inicia la auditoria (pasa a En ejecucion) |
| Hallazgo critico sin plan de accion | Se registra un hallazgo Critico sin accion correctiva | HIGH | Delegado/Resp. interno, Resp. Legal/Compliance | Plataforma y correo | Diaria mientras siga sin accion | Escala a Gerencia a las 72 horas | Se crea la accion correctiva |
| Accion correctiva vencida | La fecha limite de una accion paso sin marcarse Corregida ni Riesgo aceptado | WARNING | Responsable de la accion, Delegado/Resp. interno | Plataforma y correo | Cada 3 dias | Si sigue vencida 15 dias, escala a Legal/Delegado y Gerencia | Se marca Corregida o se aprueba Riesgo aceptado |
| Auditoria abierta mas de 90 dias sin cerrar | La auditoria sigue en Plan de accion en curso mas de 90 dias desde que inicio ejecucion | WARNING | Delegado/Resp. interno, Administrador | Plataforma | Semanal | Escala a Gerencia a los 120 dias | Se cierra la auditoria o se documenta el motivo del retraso |

---

## J. Evidencia

| Que genera o conserva | Como | Obligacion que prueba (OBL-ID) | Conservacion |
|---|---|---|---|
| Informe de auditoria cerrado | Archivo con hash, version, fecha y responsable | OBL-AUD-01, OBL-PRIN-03 | Conservacion indefinida con opcion de archivado manual hasta que el motor de retencion documental (MOD-016) defina un plazo especifico de conservacion documental; mismo criterio provisional que usan otros modulos de evidencia |
| Cada hallazgo con su evidencia adjunta | Registro inmutable con fecha, usuario y referencia a la obligacion o control | OBL-AUD-01 | Igual que el informe asociado |
| Historial de estados de la auditoria (quien cambio que y cuando) | AuditLog | OBL-PRIN-03 | Igual que el informe asociado |
| Aprobacion del cierre | Identidad del Aprobador, fecha, y justificacion de cualquier riesgo aceptado | OBL-AUD-01, OBL-PRIN-03 | Igual que el informe asociado |
| Vinculacion de cada accion correctiva con su tarea y su cierre en MOD-021 | Referencia cruzada | OBL-AUD-01 | Igual que el informe asociado |
| Notificacion enviada al Delegado para su informe periodico | Registro de envio | OBL-DPO-07 (evidencia de que MOD-018 alimento la obligacion de MOD-002, no de que esta se cumplio) | Igual que el informe asociado |

---

## K. Documentos asociados

- **Documentos requeridos como entrada:** informe de la firma auditora externa (si Tipo = Externa o Mixta); checklist previo si la empresa ya tenia uno fuera del sistema (importable como adjunto).
- **Documentos generados:** informe de auditoria (borrador generado automaticamente al cerrar si no se adjunto uno externo, con conclusion, hallazgos y plan de accion); plan de accion exportable (tabla de acciones, responsables y fechas).
- **Plantillas que el sistema provee:** "Informe de auditoria anual de cumplimiento" (variables: periodo, alcance, hallazgos, plan de accion, conclusion), marcada explicitamente como borrador que requiere revision y aprobacion de la organizacion antes de considerarse el informe final, en linea con el texto de descargo estandar de `04_objetivo_exacto_del_producto.md`, seccion 1.3.
- **Anexos y evidencias documentales:** capturas de pantalla, checklist exportado de MOD-015, extractos del RAT (MOD-006) relevantes al alcance de la auditoria, actas de reunion del comite de cumplimiento si la empresa las adjunta, informe de la firma auditora externa cuando aplique.

---

## L. Dependencias

```
MOD-006 RAT y Mapa de Datos --------+
MOD-015 Controles de Seguridad -----+---> MOD-018 Auditoria de Cumplimiento ---> MOD-020 Dashboard y Reportes
MOD-019 Centro de Evidencias -------+              |         ^                        |
        (relacion reciproca,                       |         |                        +--> MOD-021 Centro de Tareas
         ver nota debajo)                          +---------+
                                                (informe y hallazgos cerrados
                                                 se registran como nueva
                                                 evidencia en MOD-019)

     Capa transversal (consultada, nunca consulta al reves):
     MOD-001 Organizacion | MOD-021 Tareas | MOD-022 Notificaciones
     MOD-023 Calendario y Motor de Plazos | MOD-024 Centro Regulatorio | MOD-026 Ayuda

     Vinculo indirecto, sin dependencia estructural:
     MOD-018 --(notificacion)--> MOD-002 Delegado / Responsable Interno (insumo para OBL-DPO-07)
```

- **De que modulos recibe datos:** MOD-006 (tratamientos vigentes del RAT como parte del checklist), MOD-015 (catalogo de controles y su estado, insumo principal de la revision tecnica), MOD-019 (evidencia ya acumulada de otros modulos que la auditoria puede citar como respaldo de un hallazgo o de su ausencia).
- **A que modulos envia datos o eventos:** MOD-019 (el informe cerrado y cada hallazgo con su evidencia, como nueva evidencia del sistema), MOD-020 (indicadores de estado de la ultima auditoria y de hallazgos/acciones abiertos), MOD-021 (una tarea por cada accion del plan de accion). De forma indirecta y sin dependencia estructural, MOD-002 recibe una notificacion (no un dato estructurado obligatorio) para apoyar el informe periodico del Delegado (OBL-DPO-07); este vinculo no aparece como `depende_de` reciproco en `mapa_modulos.json` porque es informativo, no una precondicion de funcionamiento de ninguno de los dos modulos.
- **Catalogos que comparte:** ninguno propio; consume por referencia el catalogo de obligaciones (OBL-ID) de la matriz, el catalogo de controles de MOD-015 y el catalogo de tratamientos de MOD-006.
- **Relacion reciproca con MOD-019.** MOD-018 declara `depende_de` a MOD-019 y MOD-019 declara `depende_de` a MOD-018 en `mapa_modulos.json`; es la unica excepcion de todo el mapa a la regla de que `depende_de` es aciclico (`06_mapa_definitivo_de_modulos.md`, seccion 6.1). No es un error de copia ni un ciclo de orden de construccion: MOD-018 consulta la evidencia ya acumulada en MOD-019 (recibida de MOD-006 a MOD-017 de forma continua) para elaborar sus hallazgos, y el informe y los hallazgos resultantes de MOD-018 se registran a su vez como nueva evidencia en MOD-019. Es una dependencia de datos bidireccional y continua entre los dos modulos de la etapa Demostrar, no una precedencia de inicializacion.
- **Que ocurre si un modulo dependiente no existe en el MVP.** MOD-018 es SHOULD HAVE, y sus dependencias declaradas (MOD-006 y MOD-019, MUST HAVE; MOD-015, tambien MUST HAVE) ya existen para cuando MOD-018 se activa, de modo que no hay aqui un escenario de dependencia invertida como el de MOD-015 con MOD-010 (ver la ficha de MOD-015, seccion L). Mientras el modulo completo no exista todavia, la obligacion OBL-AUD-01 queda cubierta de forma parcial por el mecanismo descrito en la seccion Q: un recordatorio generico anual en el Calendario (MOD-023, MUST HAVE) y la evidencia que el AuditLog ya deja desde el primer dia en cada modulo MUST HAVE, sin el flujo estructurado de hallazgos y plan de accion que describe esta ficha.

---

## M. Dashboard

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Estado de la ultima auditoria | Campo Estado del registro de ComplianceAudit mas reciente | Verde si Cerrada dentro del periodo anual; amarillo si En ejecucion, Hallazgos en revision o Plan de accion en curso; rojo si vencida sin iniciarse o si nunca hubo auditoria y ya paso el plazo esperado | Gerencia: solo el semaforo. Legal/Delegado y Resp. Legal/Compliance: el detalle completo. Auditor: el historico de auditorias cerradas. Resp. Seguridad/IT: solo los hallazgos relacionados con controles de MOD-015 |
| Dias desde el cierre de la ultima auditoria | Hoy menos fecha de cierre de la ultima auditoria en estado Cerrada | Verde si menor a 300 dias, amarillo 300 a 365, rojo mas de 365 [opinion de producto, umbral sin respaldo legal, referenciado a la periodicidad anual de OBL-AUD-01] | Gerencia, Legal/Delegado |
| Hallazgos abiertos por severidad | Cuenta de hallazgos en estado Abierto o En correccion, agrupados por severidad | Rojo si hay al menos un hallazgo Critico abierto | Legal/Delegado, Resp. Seguridad/IT, Gerencia (solo el total) |
| Acciones correctivas vencidas | Cuenta de acciones del plan con fecha limite pasada y estado distinto de Corregida o Riesgo aceptado | Rojo si mayor a 0 | Legal/Delegado, Responsable de la accion, Gerencia |

Ningun indicador de este modulo se expresa como "porcentaje de cumplimiento legal"; el lenguaje siempre es "estado del ciclo de auditoria", "hallazgos abiertos" o "acciones pendientes", junto con el banner de descargo estandar del sistema (`04_objetivo_exacto_del_producto.md`, seccion 1.3).

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Informe de auditoria anual | Alcance, hallazgos, plan de accion, conclusion | Por periodo, por tipo (interna/externa/mixta) | PDF | Gerencia, Auditor externo, ACE si la requiere | Si |
| Plan de accion exportable | Acciones, responsables, fechas y estado | Por auditoria, por severidad | XLSX | Legal/Delegado, Resp. Seguridad/IT | Si |
| Historico de auditorias | Lista de todos los ciclos con fecha, tipo, hallazgos totales y estado | Rango de fechas | CSV | Auditor interno, Gerencia | Si |
| Paquete de evidencia de la auditoria | Informe mas anexos, con verificacion de integridad, generado via MOD-019 | Por auditoria especifica | ZIP con hash o firma | Auditor externo, ACE | Si (es en si mismo un subconjunto del paquete general de evidencias) |

---

## O. Historial

Eventos que quedan en el historial del modulo y en la auditoria transversal (AuditLog):

- Creacion de una auditoria (manual o automatica por el recordatorio), con origen registrado.
- Cambios de alcance, fechas, responsable o tipo antes de iniciar ejecucion, con valor anterior y valor nuevo.
- Cambios de estado de la auditoria, con quien lo ejecuto y cuando.
- Cada hallazgo creado o editado, con valor anterior y nuevo si cambia la severidad o el estado.
- Cada accion del plan creada, reasignada o cerrada.
- Aprobacion del cierre, con identidad del Aprobador y, si hubo riesgo aceptado, su justificacion.
- Reaperturas, con el motivo indicado.
- Exportaciones del informe o del paquete de evidencia, con quien la genero y cuando.
- Accesos de lectura del Auditor externo (invitado) a la auditoria especifica para la que fue invitado.

---

## P. Riesgos

- **Riesgo legal:** que la empresa o un tercero interprete una auditoria en estado "Cerrada" como una declaracion de que la empresa cumple la LPDP. Mitigacion de diseno: el informe y el dashboard incluyen siempre el banner de descargo estandar, mas el texto especifico: "Este informe documenta el alcance revisado y los hallazgos de esta auditoria interna; no constituye una certificacion de cumplimiento legal ni sustituye la facultad de la ACE de evaluar el cumplimiento de la empresa."
- **Riesgo legal:** que se use el historial de auditorias como si fuera la certificacion oficial de la ACE (OBL-AUD-02) cuando esta aun no existe. Mitigacion de diseno: el sistema nunca usa las palabras "certificacion" ni "sello" dentro de este modulo salvo para explicar, en la ayuda contextual, que ese mecanismo todavia no esta habilitado por la ACE.
- **Riesgo de UX:** una pyme (perfil Karla, `05_tipos_de_usuario.md`, seccion 5.1) posterga indefinidamente iniciar su primera auditoria porque le parece un proceso demasiado formal. Mitigacion de diseno: el checklist inicial se precarga automaticamente desde MOD-006 y MOD-015 para que planificar e iniciar tomen minutos, no dias, y el alcance sugerido por defecto son solo las obligaciones OBLIGATORIO.
- **Riesgo operativo:** la fecha del recordatorio anual queda mal calculada si el motor de plazos (MOD-023) no esta actualizado, o si una auditoria queda en estado "Planificada" indefinidamente sin iniciarse. Mitigacion de diseno: las alertas escalonadas de la seccion I, sobre el mismo motor de plazos compartido que usa el resto del sistema.
- **Riesgo de seguridad y privacidad:** un hallazgo puede describir una debilidad de seguridad real (por ejemplo, "el cifrado en transito del sistema de nomina no esta implementado"), informacion sensible desde el punto de vista de seguridad cuya filtracion podria facilitar un ataque. Mitigacion de diseno: acceso a los hallazgos restringido a los roles con necesidad de conocerlos (Delegado/Resp. interno, Resp. Legal/Compliance, Aprobador, Resp. Seguridad/IT solo en los hallazgos que le asignan como tarea, Auditor interno/externo en modo lectura), y el paquete exportado hacia un Auditor externo o hacia la ACE se limita al alcance de esa auditoria especifica, sin exponer hallazgos de otros ciclos o de otras areas fuera del alcance solicitado.
- **Riesgo de separacion de funciones en pyme:** cuando la misma persona acumula Administrador, Delegado y Aprobador (tipico en pyme), esa persona puede registrar un hallazgo, decidir aceptar el riesgo en vez de corregirlo, y cerrar la auditoria sin ningun segundo control real. Mitigacion de diseno: advertencia visible de autorrevision en cada aprobacion de riesgo aceptado y en cada cierre hecho por el mismo usuario que registro los hallazgos, siguiendo la regla general de `05_tipos_de_usuario.md`, seccion 5.4.

---

## Q. MVP

**Cobertura parcial ya disponible antes de que este modulo exista como tal.** Antes de que el registro estructurado de ComplianceAudit este disponible, la empresa ya cuenta con un recordatorio generico de la auditoria anual como evento del Calendario y Motor de Plazos (MOD-023, MUST HAVE), anclado a la fecha de adecuacion inicial registrada en el diagnostico (MOD-004); y el AuditLog tecnico, embebido en todo modulo MUST HAVE, ya deja evidencia verificable desde el primer dia de uso del sistema, sin esperar a que exista el primer ciclo completo de auditoria sustantiva. Solo el flujo estructurado de hallazgos, plan de accion y cierre formal que describe esta ficha se difiere hasta que MOD-018 se active (`06_mapa_definitivo_de_modulos.md`, seccion sobre MOD-018).

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Registro basico de ComplianceAudit (planificar, ejecutar, cerrar) con checklist precargado desde MOD-006 y MOD-015 | | X | | | Cubre OBL-AUD-01 (OBLIGATORIO), pero la primera auditoria formal solo es exigible tras el primer ano de operacion de la empresa; no bloquea a ningun modulo MUST HAVE (test de tres condiciones, `06_mapa_definitivo_de_modulos.md`) |
| Registro de hallazgos con severidad, evidencia y estado | | X | | | Nucleo del valor probatorio del modulo; sin esto la auditoria seria solo una fecha marcada, no un proceso sustantivo |
| Plan de accion con tareas automaticas en MOD-021 | | X | | | Cierra el ciclo entre encontrar un problema y corregirlo; depende del registro de hallazgos, mismo nivel de prioridad |
| Cierre con aprobacion separada (Aprobador distinto de quien registro los hallazgos) | | X | | | Separacion de funciones basica del modulo; sin ella el cierre pierde valor probatorio frente a una autorrevision |
| Informe de auditoria generado automaticamente al cerrar (si no se adjunto uno externo) | | X | | | Reduce la friccion de redaccion manual; el borrador ya usa la informacion capturada durante el ciclo |
| Notificacion al Delegado para su informe periodico (OBL-DPO-07) | | X | | | Bajo costo de implementacion; cierra un vinculo real entre dos obligaciones distintas sin duplicar el informe |
| Recordatorio automatico del siguiente ciclo, anclado al cierre anterior | | X | | | Reemplaza, con datos reales de la auditoria, el recordatorio generico que ya existia via MOD-023 antes de que este modulo se activara |
| Auditoria de tipo Externa o Mixta, con invitacion de Auditor externo y adjunto de su informe | | | X | | Util para empresa mediana o corporativo desde el primer ciclo formal, pero no bloquea el valor central del modulo para una pyme que se audita internamente |
| Plantillas de checklist diferenciadas por sector o tamano de empresa | | | | X | Funcionalidad diferenciadora de producto, sin urgencia regulatoria (la Politica ACE no fija contenido minimo, ver ambiguedad 2 de `03_hallazgos_regulatorios.md`, seccion 8) |
| Integracion con un futuro mecanismo de certificacion de la ACE (OBL-AUD-02) | | | | X | No existe hoy ningun mecanismo habilitado por la ACE (verificado 2026-09-23 y 2026-09-24, sin resultado); construir esto ahora seria especular sobre una facultad sin desarrollo |

**Version minima vendible del modulo:** el registro de ComplianceAudit con su ciclo completo (planificar, ejecutar, registrar hallazgos con severidad y evidencia, generar plan de accion con tareas automaticas, cerrar con aprobacion separada) y el recordatorio automatico del siguiente ciclo. Esto ya permite a una empresa, desde su primer ano de uso del sistema, convertir la obligacion anual de auditarse (OBL-AUD-01) en un proceso documentado con hallazgos y correcciones reales, que es exactamente el nucleo del valor probatorio de este modulo; las variantes de auditoria externa formal y las plantillas por sector pueden iterar despues sin bloquear ese nucleo.

---

## R. Ayuda contextual (complemento obligatorio)

**1. Que es la "auditoria anual de cumplimiento"**
- Que es: una revision propia y periodica de como va su programa de proteccion de datos, en la que se compara lo que la empresa deberia tener (controles, documentos, procesos) contra lo que realmente tiene, y se documentan las diferencias.
- Por que tengo que hacer esto: la Agencia de Ciberseguridad del Estado exige que toda empresa privada sujeta a la ley realice esta revision al menos una vez al ano.
- Fundamento: OBL-AUD-01, Art. 8 lit. b) de las Politicas de Actuacion de la ACE.
- Cuando necesito ayuda juridica: si un hallazgo de la auditoria podria implicar que la empresa ya incumplio una obligacion legal (no solo que un control esta pendiente), consulte con su asesor legal antes de decidir como responder.

**2. Que es un "hallazgo" y en que se diferencia de un incidente de seguridad**
- Que es: un hallazgo es algo que la auditoria encontro mal, incompleto o pendiente dentro de su programa (por ejemplo, un tratamiento sin base juridica registrada, o un control vencido). Un incidente de seguridad (MOD-013) es algo distinto: una vulneracion real que ya ocurrio y afecto datos de personas.
- Por que tengo que hacer esto: separar ambas cosas evita confundir "algo que debo mejorar" con "algo que ya paso y debo notificar en 72 horas"; si un hallazgo revela que ya ocurrio una vulneracion, el sistema le pedira abrir tambien un caso en el modulo de Incidentes.
- Fundamento: OBL-AUD-01 (hallazgo de auditoria) frente a OBL-INC-01 (Art. 25 LPDP, notificacion de vulneraciones).
- Cuando necesito ayuda juridica: si no esta seguro de si lo que encontro es solo una mejora pendiente o ya una vulneracion que debio notificarse, consulte de inmediato con su asesor legal o con la persona responsable de seguridad.

**3. Que significa "riesgo aceptado" en un hallazgo**
- Que es: es la opcion de dejar constancia formal de que, en vez de corregir un hallazgo de inmediato, la empresa decidio conscientemente asumir ese riesgo por ahora, con la aprobacion explicita de una segunda persona.
- Por que tengo que hacer esto: no todos los hallazgos se pueden corregir al instante; dejar uno sin corregir sin ninguna explicacion se ve, ante una revision, igual que no haberlo detectado nunca. Un riesgo aceptado y aprobado demuestra que fue una decision consciente y documentada.
- Fundamento: OBL-PRIN-03 (Art. 5 lit. i LPDP, responsabilidad demostrada).
- Cuando necesito ayuda juridica: si el hallazgo esta relacionado con una obligacion OBLIGATORIO de la matriz, consulte con su asesor legal antes de aceptar el riesgo en vez de corregirlo.

**4. En que se diferencia esta auditoria del registro tecnico que ya guarda todo el sistema (AuditLog)**
- Que es: el AuditLog es un registro automatico de quien hizo que y cuando en cualquier parte del sistema, que existe desde el primer dia sin que nadie lo active. La auditoria de este modulo es un ejercicio distinto: una revision humana, periodica y con conclusiones propias sobre el estado del programa completo.
- Por que tengo que hacer esto: el AuditLog por si solo no le dice si su programa esta bien encaminado, solo deja constancia de acciones; la auditoria de este modulo si analiza y concluye, y por eso requiere su participacion activa una vez al ano.
- Fundamento: OBL-AUD-01 (Art. 8 lit. b Politicas ACE) para la auditoria sustantiva; OBL-PRIN-03 (Art. 5 lit. i LPDP) para el AuditLog como evidencia tecnica de fondo.
- Cuando necesito ayuda juridica: no aplica; esta es una aclaracion sobre que hace cada parte del sistema, no una pregunta legal.

**5. Por que este modulo no emite una certificacion de la ACE**
- Que es: cerrar una auditoria en este sistema es un registro interno de su empresa, no un documento oficial emitido por la Agencia de Ciberseguridad del Estado.
- Por que tengo que hacer esto: la ley le da a la ACE la facultad de crear certificaciones o sellos de proteccion de datos, pero al dia de hoy la ACE no ha habilitado ningun mecanismo de ese tipo para organizaciones; por eso este modulo documenta su propio proceso de revision, sin llamarlo certificacion.
- Fundamento: OBL-AUD-02, Art. 50 lit. j, k y l) LPDP (RECOMENDADO, facultad de la ACE sin desarrollo aun).
- Cuando necesito ayuda juridica: si la ACE llega a anunciar un mecanismo de certificacion en el futuro y quiere saber si le conviene solicitarlo, consulte con su asesor legal; el sistema por si solo no puede evaluar esa conveniencia.

---

## Nota final del agente (posibles observaciones sobre el mapa)

No se detecto ningun error en las decisiones ya tomadas para MOD-018 en `06_mapa_definitivo_de_modulos.md` ni en `mapa_modulos.json`. Las cinco obligaciones asignadas (una propietaria, cuatro colaboradoras) coinciden exactamente con la tabla de cobertura de la seccion 8 de ese documento (lineas correspondientes a OBL-AUD-01, OBL-AUD-02, OBL-DPO-07, OBL-PRIN-03 y OBL-SEG-02), y la relacion reciproca declarada con MOD-019 esta documentada como excepcion intencional y unica del mapa, con explicacion consistente tanto en `notas_dependencia` del JSON como en la seccion 6.1 del documento de mapa. Dos precisiones que esta ficha desarrolla y que conviene dejar explicitas para quien lea el mapa junto a esta ficha:

1. La nota "No aplica directamente" de la reforma 659 para MOD-018 es correcta para la obligacion en si (OBL-AUD-01 nace de la Politica ACE, no de los Arts. 15/17 LPDP), pero el rol que por defecto coordina el ciclo de auditoria si cambia de nombre entre el estado ACTUAL y el estado FUTURO (de Delegado a Responsable interno), en el mismo patron que ya documenta la ficha de MOD-015 para uno de los items de su catalogo. No contradice el mapa, solo lo precisa a nivel de asignacion de responsable dentro del registro de cada auditoria.
2. La cita legal que la propia Politica de Actuacion de la ACE invoca como base de la auditoria anual (Art. 50 lit. l LPDP) no describe con exactitud un deber de auditoria interna de las empresas, sino la facultad de la ACE de auditar sus propias certificaciones. Esto no es un error del mapa ni de la matriz de obligaciones, que ya recogen la obligacion por el texto expreso de la Politica (Art. 8 lit. b); se deja registrado aqui, en la seccion A, como nota de transparencia sobre una imprecision de cita en la fuente normativa misma, sin que afecte la validez ni la clasificacion OBLIGATORIO de OBL-AUD-01.
