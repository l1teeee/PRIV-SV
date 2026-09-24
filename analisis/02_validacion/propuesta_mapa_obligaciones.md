# Propuesta de mapa de modulos - PRIV-SV (angulo obligacion-primero)

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (prohibido proponer codigo, SQL, APIs, stack o infraestructura).

Angulo de diseno asignado: OBLIGACION-PRIMERO. Se parte de las 105 obligaciones de `01_legal/matriz_obligaciones.md` (IDs canonicos OBL-AREA-NN) y se agrupan por proceso de negocio de forma que cada obligacion tenga exactamente un modulo propietario. Ningun modulo de este mapa existe sin al menos una obligacion propia o una necesidad probatoria/operativa explicita detras (los modulos sin obligacion propia son, por diseno, los siete modulos transversales que el propio enunciado de la tarea identifica: Centro de tareas, Centro de evidencias, Auditoria, Notificaciones, Calendario, Centro regulatorio y Centro de ayuda; a estos se suman Usuarios/roles, Dashboard, Reportes y Busqueda global, tambien transversales por naturaleza).

Fuentes usadas: `01_legal/matriz_obligaciones.md` (105 obligaciones, columna "modulos candidatos" como punto de partida de la agrupacion), `02_validacion/02_validacion_de_la_idea.md` (32 decisiones de alcance de la seccion 2.7, que este documento sigue salvo indicacion explicita en contrario), `00_prompt_analisis_funcional.md` (29 areas obligatorias 8.1 a 34) y el documento maestro (hipotesis de modulos de sus secciones 11 a 31).

Convencion: toda fila que cita un OBL-ID es una obligacion real de la matriz. Toda decision de agrupacion sin OBL-ID detras (por ejemplo, que Onboarding y Diagnostico compartan modulo) es una decision de producto de este documento, no un mandato legal, y se marca como tal.

---

## 1. Arbol de modulos (ASCII)

```
PLATAFORMA PRIV-SV
|
+-- A. NUCLEO ORGANIZATIVO
|     |
|     +-- MOD-ORG    Organizacion y Delegado de Proteccion de Datos
|     |     +-- Empresa, sucursales, unidades, departamentos
|     |     +-- Ciclo de vida del Delegado / Responsable interno (doble estado reforma 659)
|     |
|     +-- MOD-USR    Usuarios, roles y permisos
|           +-- Catalogo de roles (incluye rol Delegado)
|           +-- Aprobaciones y separacion de funciones
|
+-- B. ENTRADA Y HOJA DE RUTA
|     |
|     +-- MOD-DIAG   Onboarding y Diagnostico de cumplimiento
|     |     +-- Asistente de incorporacion (una vez, alta guiada)
|     |     +-- Cuestionario de diagnostico (repetible)
|     |
|     +-- MOD-PLAN   Plan de cumplimiento
|           +-- Acciones priorizadas (responsable, fecha, fundamento, evidencia, estado)
|
+-- C. REGISTRO Y GOBERNANZA DE DATOS
|     |
|     +-- MOD-RAT    RAT y Mapa de datos
|     |     +-- Registro de actividades de tratamiento (fuente unica de verdad)
|     |     +-- Mapa de datos (vista: origen -> sistema -> area -> proveedor -> pais -> eliminacion)
|     |     +-- Catalogo de sistemas
|     |
|     +-- MOD-CONS   Consentimiento
|     |     +-- Sub-flujo titular menor de edad
|     |     +-- Sub-flujo biometria (alternativa no biometrica obligatoria)
|     |     +-- Lista de supresion de marketing directo
|     |
|     +-- MOD-EIPD   Riesgos y Evaluaciones de Impacto (EIPD)
|     |
|     +-- MOD-RET    Retencion y eliminacion
|           +-- Motor de retencion de datos del titular (por finalidad)
|           +-- Motor de retencion documental de cumplimiento propio
|
+-- D. RELACION CON EL TITULAR
|     |
|     +-- MOD-ARCO   ARCO-POL y Portal del titular
|           +-- Motor de casos ARCO-POL (formulario interno seguro, MVP)
|           +-- Verificacion de identidad del solicitante
|           +-- Ramas: incompetencia, notificacion a receptores, reclamo ante la ACE
|           +-- Portal publico del titular (canal externo, V1/Enterprise)
|
+-- E. RELACION CON TERCEROS
|     |
|     +-- MOD-PROV    Proveedores, encargados y contratos (DPA)
|     |     +-- Encargado / Tercero-receptor / Subencargado (tipos distintos)
|     |     +-- Contratos y DPA (tipo de documento dentro de Proveedores)
|     |
|     +-- MOD-TRANSF  Transferencias internacionales
|           +-- Auto-alta "pendiente de confirmar" desde Proveedores en el extranjero
|
+-- F. GESTION DE CRISIS Y CONTROL
|     |
|     +-- MOD-INC    Incidentes de seguridad
|     +-- MOD-CTRL   Controles de seguridad (catalogo compartido con EIPD)
|     +-- MOD-CAP    Capacitacion
|
+-- G. DOCUMENTACION
|     |
|     +-- MOD-DOC    Documentos y politicas (avisos, politicas, plantillas)
|
+-- H. RELACION CON LA AUTORIDAD (ACE)
|     |
|     +-- MOD-REG    Centro regulatorio, actualizaciones normativas y procedimiento sancionador
|           +-- Marco normativo consultable (VIGENTE / FUTURO / DEROGADO / MODIFICADO)
|           +-- Motor de doble estado de la reforma 659
|           +-- Procedimiento sancionador / requerimientos de la ACE
|
+-- I. MODULOS TRANSVERSALES (sin obligacion propia exclusiva; dan soporte a todos los anteriores)
      |
      +-- MOD-TASK   Centro de tareas
      +-- MOD-CAL    Calendario y motor de plazos habiles
      +-- MOD-AUD    Auditoria (registro tecnico AuditLog + programa anual de cumplimiento)
      +-- MOD-EVID   Centro de evidencias
      +-- MOD-NOTIF  Notificaciones
      +-- MOD-DASH   Dashboard
      +-- MOD-REP    Reportes
      +-- MOD-SEARCH Busqueda global
      +-- MOD-HELP   Centro de ayuda contextual
```

25 modulos en total: 16 modulos "de proceso" con al menos una obligacion propia (clusters A a H) y 9 modulos transversales de soporte (cluster I), de los cuales MOD-USR, MOD-AUD y MOD-CAL si tienen obligaciones propias (ver seccion 5) aunque funcionan de forma transversal. Esto es menos de los 29 items que enumera el prompt de analisis porque varias areas se absorben como submodulos o vistas de otro modulo (ver seccion 6), y menos que los 21 "modulos" que sugiere el documento maestro en sus secciones 11 a 31, pese a cubrir mas obligaciones y mas areas que el maestro.

---

## 2. Fichas de modulo

Cada ficha resume: proposito, obligaciones que cubre como propietario (lista completa de OBL-ID; "colaborador" indica obligaciones donde el modulo participa sin ser el dueno), areas del prompt que absorbe, decision respecto al documento maestro, clasificacion MVP con justificacion y dependencias principales. La ficha extendida A-Q de `00_plantilla_ficha_modulo.md` es un entregable posterior; esto es la base para redactarla.

### MOD-ORG - Organizacion y Delegado de Proteccion de Datos

- Proposito: registra la identidad legal y estructura de la empresa cliente (sucursales, unidades, departamentos, responsables). Administra el ciclo de vida completo de la figura que hoy la ley llama "Delegado de Proteccion de Datos" y que la reforma 659 renombraria a "sujeto obligado" / responsable interno, sin duplicar esa figura en dos modulos. Es el punto de partida de todo el resto de la plataforma.
- Obligaciones propias: OBL-DPO-01, OBL-DPO-02, OBL-DPO-03, OBL-DPO-04, OBL-DPO-05, OBL-DPO-06, OBL-DPO-07, OBL-DPO-08 (8).
- Colaborador en: OBL-AMB-01 (contexto de sujecion), OBL-CAP-02 (capacitacion del propio Delegado, ejecutada en MOD-CAP), OBL-SANC-* (quien responde por la empresa ante la ACE).
- Areas del prompt que absorbe: 8.1 Configuracion de empresa (propia). Funcion transversal para 8.2 (perfil del Delegado dentro del catalogo de roles).
- Decision vs. documento maestro: se mantiene y se amplia. El maestro (seccion 11) no incluia el rol Delegado; es la correccion estructural mas importante identificada en `02_validacion` (seccion 2.4 y decision 2.7.7).
- MVP: MUST HAVE. Sin empresa ni Delegado registrado no hay sujeto que asuma ninguna obligacion; ademas el Delegado es obligatorio hoy (Arts. 15 y 17 LPDP vigentes) con plazos ya en curso (comunicacion a la ACE en 15 dias habiles).
- Dependencias: entra desde MOD-USR (personas disponibles para asignar como Delegado) y MOD-REG (bandera de activacion del estado FUTURO de la reforma 659). Alimenta a MOD-DIAG, MOD-ARCO, MOD-TASK, MOD-CAP, MOD-EVID (todos necesitan saber quien es el Delegado/responsable interno vigente).

### MOD-USR - Usuarios, roles y permisos

- Proposito: administra personas, roles estandar y personalizados, y las reglas de aprobacion y separacion de funciones que exige operar el resto de la plataforma. No posee ninguna obligacion legal propia; es infraestructura habilitante para todos los demas modulos.
- Obligaciones propias: ninguna (0).
- Colaborador en: OBL-PRIN-03 (responsabilidad demostrada exige trazar quien hizo que, con que rol), decision 2.7.22 de `02_validacion` (todo acto atribuido al Delegado requiere su aprobacion explicita antes de emitirse, lo que exige un motor de aprobacion por rol).
- Areas del prompt que absorbe: 8.2 Usuarios, roles y permisos (propia, integra).
- Decision vs. documento maestro: se mantiene (seccion 12 del maestro), con el rol "Delegado de Proteccion de Datos" agregado explicitamente al catalogo (decision 2.7.7).
- MVP: MUST HAVE. Ningun modulo puede asignar tareas, aprobar documentos ni separar funciones sin este modulo.
- Dependencias: entra desde MOD-ORG (estructura sobre la que se asignan roles). Alimenta a todos los demas modulos (quien puede ver/editar/aprobar que).

### MOD-DIAG - Onboarding y Diagnostico de cumplimiento

- Proposito: incorpora a una empresa nueva (alta guiada de organizacion y usuarios) y ejecuta el cuestionario de diagnostico que traduce respuestas simples (empleados, camaras, biometria, informacion medica, cloud, datos fuera del pais) en tratamientos, tareas, documentos y evaluaciones de riesgo. El diagnostico es repetible; el onboarding no.
- Obligaciones propias: OBL-AMB-01, OBL-AMB-02, OBL-AMB-03, OBL-AMB-04 (4).
- Colaborador en: dispara altas en MOD-RAT, MOD-CONS, MOD-EIPD, MOD-TRANSF, MOD-PLAN segun cada respuesta (decision 2.7.27 y 2.7.28).
- Areas del prompt que absorbe: 8.3 Onboarding y 9 Diagnostico inicial (ambas, como dos submodulos de un mismo modulo).
- Decision vs. documento maestro: se fusiona. El maestro trataba Onboarding (seccion 15, "Compliance Wizard") como una sola cosa; `02_validacion` decision 2.7.5 separa el concepto de Onboarding (una vez) del de Diagnostico (repetible), pero ambos se agrupan aqui en un solo modulo con dos submodulos para minimizar el numero de modulos sin perder esa distincion.
- MVP: MUST HAVE. Es el punto de entrada de todo el producto; sin diagnostico no hay plan, ni RAT inicial, ni activacion de sub-flujos de riesgo.
- Dependencias: entra desde MOD-ORG y MOD-USR (que se esta dando de alta). Alimenta a MOD-PLAN, MOD-RAT, MOD-CONS, MOD-EIPD, MOD-TRANSF, MOD-TASK.

### MOD-PLAN - Plan de cumplimiento

- Proposito: convierte el resultado del diagnostico en una lista priorizada de acciones concretas, cada una con responsable, fecha, fundamento legal (OBL-ID), evidencia esperada y estado. Es la promesa comercial central del producto: "sepa que debe hacer".
- Obligaciones propias: OBL-PLAZO-03 (1).
- Colaborador en: referencia (sin duplicar) obligaciones de todos los demas modulos al generar cada accion.
- Areas del prompt que absorbe: 10 Plan de cumplimiento (propia, integra).
- Decision vs. documento maestro: es nuevo como modulo explicito. El maestro no lo desarrollaba como pieza separada de Onboarding; se hace explicito porque el prompt de analisis lo exige (area 10) y porque decision 2.7.29 de `02_validacion` ancla la urgencia comercial del producto justo a la obligacion que este modulo posee (adecuacion a las Politicas ACE, con plazo transitorio ya vencido el 2/3-dic-2025).
- MVP: MUST HAVE. Sin plan de accion priorizado, el diagnostico es solo un cuestionario sin salida util para un usuario no especialista.
- Dependencias: entra desde MOD-DIAG (respuestas), MOD-RAT/MOD-CONS/MOD-CTRL/etc. (gaps detectados). Alimenta a MOD-TASK (cada accion del plan genera tareas) y MOD-DASH.

### MOD-RAT - RAT y Mapa de datos

- Proposito: es la fuente unica de verdad de cada actividad de tratamiento (que dato, con que finalidad, con que base legal, en que sistema, con que proveedor). El "Mapa de datos" es una vista sobre este registro, no una base independiente. Es el modulo con mas obligaciones propias despues de ARCO-POL.
- Obligaciones propias: OBL-PRIN-01, OBL-PRIN-02, OBL-SENS-01, OBL-SENS-03, OBL-SENS-04, OBL-SENS-05, OBL-SENS-06, OBL-TRAT-01, OBL-TRAT-02, OBL-TRAT-03, OBL-DOC-02 (11).
- Colaborador en: OBL-SENS-02, OBL-SENS-07 (marca categorias sensibles que Consentimiento debe reforzar), OBL-TRANSF-* (detecta tratamientos con destino extranjero sin ficha de transferencia, decision 2.7 seccion 2.2).
- Areas del prompt que absorbe: 11 RAT (propia) y 12 Mapa de datos (vista/submodulo, sin base de datos propia).
- Decision vs. documento maestro: se fusiona. El maestro tenia "13 Inventario de datos" y "14 RAT" como secciones separadas que describian la misma entidad dos veces; decision 2.7.1 las fusiona.
- MVP: MUST HAVE. Es el registro obligatorio central (OBL-DOC-02, medida organizativa de las Politicas ACE) y la base de la que dependen Consentimiento, EIPD, Transferencias y Retencion.
- Dependencias: entra desde MOD-DIAG (altas iniciales), MOD-PROV (sistemas/proveedores referenciados). Alimenta a MOD-CONS, MOD-EIPD, MOD-RET, MOD-TRANSF, MOD-PLAN, MOD-EVID.

### MOD-ARCO - ARCO-POL y Portal del titular

- Proposito: gestiona el ciclo de vida completo de una solicitud de un titular (acceso, rectificacion, cancelacion, oposicion, portabilidad, olvido, limitacion): identidad, prevencion, plazos, prorroga, denegatoria, notificacion a receptores, y las vias de escalamiento del titular (reclamo ante la Direccion de Proteccion de Datos, denuncia ante la ACE). En el MVP el canal es un formulario interno seguro; el portal publico con autoregistro es el mismo motor expuesto hacia afuera en V1/Enterprise.
- Obligaciones propias: OBL-ARCO-01 a OBL-ARCO-15 (15), mas OBL-DOC-04, OBL-PLAZO-04, OBL-SANC-09 (18 en total).
- Colaborador en: OBL-CONS-03 (revocacion, ejecutada en MOD-CONS pero enlazada aqui como via de contacto), OBL-TRANSF-* (notificacion a receptores transferidos).
- Areas del prompt que absorbe: 13 ARCO-POL (propia, con profundidad especial) y 33 Portal del titular (submodulo/canal del mismo motor).
- Decision vs. documento maestro: se fusiona y se amplia. El maestro tenia "17 ARCO-POL" y "18 Portal de privacidad" como secciones separadas; se integran en un solo modulo porque el portal no es mas que el canal publico del mismo motor de casos (decision de minimizacion de este documento). Se amplia con tres ramas que el maestro no contemplaba: incompetencia, notificacion a receptores y reclamo ante la ACE (decision 2.7.10).
- MVP: MUST HAVE. Tiene el mayor numero de obligaciones propias de todo el mapa, incluye el mecanismo de ejercicio de derechos con plazo transitorio ya vencido (OBL-PLAZO-04, OBL-DOC-04) y es el area que el prompt pide tratar "con especial profundidad". El portal publico (canal externo con autoregistro) es SHOULD HAVE/V1 dentro de este mismo modulo (decision 2.7.30): el MVP satisface la obligacion con el formulario interno.
- Dependencias: entra desde MOD-ORG/MOD-USR (quien resuelve el caso segun el estado de la reforma 659), MOD-CAL (computo de plazos), MOD-DOC (version del aviso vigente). Alimenta a MOD-TASK, MOD-NOTIF, MOD-EVID, MOD-PROV (notificacion a receptores).

### MOD-TASK - Centro de tareas

- Proposito: orquesta la creacion, asignacion, seguimiento y cierre de toda tarea que se origina en otro modulo (diagnostico, plan, ARCO-POL, incidentes, proveedores, riesgos, documentos, auditoria, controles). No decide ninguna obligacion por si mismo; es el mecanismo compartido que convierte "una obligacion con plazo" en "una tarea con responsable".
- Obligaciones propias: ninguna (0).
- Colaborador en: prácticamente todas las obligaciones con plazo (OBL-ARCO-*, OBL-INC-01/02, OBL-DPO-02/03, OBL-SANC-05/06, OBL-CONS-03, etc.), en las que aparece como "modulo candidato" secundario en la matriz (8 apariciones explicitas).
- Areas del prompt que absorbe: 14 Centro de tareas (propia, transversal por diseno segun el propio enunciado de la tarea).
- Decision vs. documento maestro: se mantiene (seccion 16 del maestro), ahora declarado explicitamente transversal y sin obligaciones propias.
- MVP: MUST HAVE. Sin este modulo ningun otro puede asignar responsable ni fecha limite a una obligacion.
- Dependencias: entra desde todos los modulos de proceso (A a H). Alimenta a MOD-NOTIF (alertas de vencimiento), MOD-DASH (pendientes por responsable), MOD-EVID (tarea cerrada como evidencia).

### MOD-DOC - Documentos y politicas

- Proposito: gestiona el ciclo de vida de documentos versionados de cara al titular y de uso interno (aviso de privacidad, politica de privacidad, politica de proteccion de datos, plantillas): borrador, aprobacion configurable por tipo, publicacion, vencimiento, revision.
- Obligaciones propias: OBL-AVISO-01, OBL-AVISO-02, OBL-AVISO-03, OBL-AVISO-04, OBL-AVISO-05, OBL-DOC-01 (6).
- Colaborador en: OBL-CONS-05 (el registro de consentimiento referencia, no copia, la version del aviso gestionada aqui, decision 2.7.6), OBL-PROV-04 (no publicar datos del encargado).
- Areas del prompt que absorbe: 15 Documentos y politicas (propia, integra).
- Decision vs. documento maestro: se mantiene (seccion 20 del maestro), con la distincion explicita entre Politica de Proteccion de Datos y Politica de Privacidad que el maestro ya intuia correctamente.
- MVP: MUST HAVE. El aviso de privacidad (OBL-AVISO-01) es obligatorio desde el dia uno y es prerequisito de Consentimiento y de ARCO-POL.
- Dependencias: entra desde MOD-USR (aprobadores por tipo de documento). Alimenta a MOD-CONS, MOD-ARCO, MOD-PROV, MOD-EVID.

### MOD-CONS - Consentimiento

- Proposito: registra el consentimiento cuando la base juridica elegida en el RAT es consentimiento, con los refuerzos que exige la ley para datos sensibles, biometria y menores de edad; gestiona la revocacion con su doble plazo encadenado y la lista de supresion de marketing directo.
- Obligaciones propias: OBL-PRIN-04, OBL-CONS-01, OBL-CONS-02, OBL-CONS-03, OBL-CONS-04, OBL-CONS-05, OBL-CONS-06, OBL-SENS-02, OBL-SENS-07 (9).
- Colaborador en: OBL-ARCO-05 (oposicion/marketing directo, decision 2.7 faltante 29), OBL-TRANSF-04 (consentimiento previo para transferencias internacionales).
- Areas del prompt que absorbe: 16 Consentimiento (propia, integra).
- Decision vs. documento maestro: se mantiene (seccion 19 del maestro), ampliado con los sub-flujos de menores (decision 2.7.28) y de alternativa no biometrica obligatoria (decision 2.7 faltante 27), que el maestro no contemplaba.
- MVP: MUST HAVE. Seis de sus nueve obligaciones propias son OBLIGATORIO sin condicion (area CONS completa).
- Dependencias: entra desde MOD-RAT (que tratamientos usan consentimiento) y MOD-DOC (version del aviso vigente). Alimenta a MOD-ARCO (revocacion como via de contacto), MOD-EVID (carga de la prueba del Art. 54).

### MOD-PROV - Proveedores, encargados y contratos (DPA)

- Proposito: administra a todo tercero que trata datos por cuenta de la empresa o que los recibe (encargado, tercero/receptor, subencargado), con el contrato/DPA como tipo de documento dentro del proveedor, no como modulo aparte.
- Obligaciones propias: OBL-PROV-01, OBL-PROV-02, OBL-PROV-03, OBL-PROV-04, OBL-PROV-05, OBL-PROV-06, OBL-PROV-07 (7).
- Colaborador en: dispara automaticamente un registro "pendiente de confirmar" en MOD-TRANSF cuando el proveedor esta fuera de El Salvador (decision 2.7.9).
- Areas del prompt que absorbe: 17 Proveedores (propia). Absorbe tambien la seccion 23 "Contratos/DPA" del documento maestro como submodulo.
- Decision vs. documento maestro: se fusiona. El maestro tenia "22 Proveedores y terceros" y "23 Contratos/DPA" separados; decision 2.7.2 los une para que el mismo contrato no se documente en tres lugares.
- MVP: MUST HAVE. Casi toda empresa salvadorena usa al menos un proveedor cloud (correo, RRHH, marketing); sin este modulo el RAT queda incompleto y no se puede activar Transferencias.
- Dependencias: entra desde MOD-RAT (que tratamientos usan que proveedor). Alimenta a MOD-TRANSF, MOD-DOC (contrato como documento), MOD-CTRL (medidas de seguridad exigidas al encargado).

### MOD-TRANSF - Transferencias internacionales

- Proposito: gestiona cada flujo de datos hacia otro responsable o fuera de El Salvador: base juridica, contrato, nivel de proteccion del pais destino y evidencia de la puesta en conocimiento a la ACE.
- Obligaciones propias: OBL-TRANSF-01, OBL-TRANSF-02, OBL-TRANSF-03, OBL-TRANSF-04, OBL-TRANSF-05, OBL-TRANSF-06 (6).
- Colaborador en: recibe altas automaticas desde MOD-PROV; OBL-ARCO-11 (notificacion a receptores transferidos, ejecutada desde ARCO-POL).
- Areas del prompt que absorbe: 18 Transferencias internacionales (propia, integra).
- Decision vs. documento maestro: se mantiene (seccion 24 del maestro), con la regla nueva de auto-alta "pendiente de confirmar" que el maestro no tenia (decision 2.7.9, cierra inconsistencia 10).
- MVP: SHOULD HAVE. La deteccion basica (proveedor extranjero = bandera pendiente) vive ya en MOD-PROV desde el MVP; la gestion completa de nivel de proteccion, contrato especifico y evidencia de aviso a la ACE puede incorporarse inmediatamente despues sin bloquear el lanzamiento.
- Dependencias: entra desde MOD-PROV (altas automaticas), MOD-CONS (consentimiento previo si aplica). Alimenta a MOD-REG (puesta en conocimiento a la ACE), MOD-EVID.

### MOD-INC - Incidentes de seguridad

- Proposito: cubre el flujo completo de una vulneracion (reportado, triage, investigacion, contencion, evaluacion, decision, notificacion, remediacion, cierre), con dos cronometros de 72 horas separados y visibles (notificacion externa e inicio de revision interna).
- Obligaciones propias: OBL-INC-01, OBL-INC-02, OBL-INC-03, OBL-INC-04, OBL-INC-05 (5).
- Colaborador en: OBL-RET-05 (retencion del expediente como prueba de descargo).
- Areas del prompt que absorbe: 19 Incidentes (propia, con flujo detallado exigido por el prompt).
- Decision vs. documento maestro: se mantiene (seccion 25 del maestro), con los dos hitos de 72 horas separados de forma explicita (decision 2.7.11, cierra inconsistencia 13).
- MVP: MUST HAVE. El plazo de 72 horas (Art. 25) es de los mas estrictos de toda la ley y de mayor exposicion sancionatoria; ninguna empresa puede operar el producto sin este modulo desde el dia uno.
- Dependencias: entra desde MOD-CAL (computo de las 72 horas), MOD-ORG (quien decide/firma la notificacion). Alimenta a MOD-TASK, MOD-NOTIF (alerta critica), MOD-EVID, MOD-RET (retencion del expediente).

### MOD-EIPD - Riesgos y Evaluaciones de Impacto (EIPD)

- Proposito: ejecuta el cuestionario de evaluacion de impacto cuando un tratamiento de alto riesgo lo dispara (biometria, videovigilancia, salud, menores), calcula un nivel de riesgo con metodologia propia del producto (nunca un formato oficial de la ACE) y selecciona o crea controles del catalogo compartido con MOD-CTRL, sin mantener una lista de controles propia.
- Obligaciones propias: OBL-SENS-08, OBL-DOC-03 (2).
- Colaborador en: OBL-SENS-01/04/06 (RAT marca la categoria que dispara la EIPD).
- Areas del prompt que absorbe: 20 EIPD/Riesgos (propia, integra).
- Decision vs. documento maestro: se mantiene (seccion 26 del maestro), pero deja de mantener un catalogo de controles paralelo al de Controles de seguridad (decision 2.7.3, cierra inconsistencia 3).
- MVP: SHOULD HAVE. La obligacion de tener EIPD (OBL-DOC-03) es OBLIGATORIO como medida organizativa, pero su activacion es condicional (solo tratamientos de alto riesgo) y no tiene un plazo transitorio ya vencido como ARCO-POL o Controles; puede incorporarse inmediatamente despues del nucleo del MVP.
- Dependencias: entra desde MOD-RAT (categorias que disparan EIPD), MOD-DIAG (respuestas de alto riesgo). Alimenta a MOD-CTRL (controles seleccionados), MOD-TASK, MOD-EVID.

### MOD-CTRL - Controles de seguridad

- Proposito: mantiene el catalogo unico de controles tecnicos, organizativos y fisicos (IAM, MFA, cifrado, backups, firewall, logs, pentesting, eliminacion segura) y registra evidencia de que cada control esta implementado. No ejecuta los controles, solo documenta su existencia y evidencia.
- Obligaciones propias: OBL-SEG-01, OBL-SEG-02, OBL-SEG-03, OBL-SEG-04, OBL-SEG-05, OBL-SEG-06 (6).
- Colaborador en: OBL-PROV-03 (medidas de seguridad tambien obligatorias para el encargado), OBL-EIPD (controles seleccionados desde la EIPD).
- Areas del prompt que absorbe: 21 Controles de seguridad (propia, integra).
- Decision vs. documento maestro: se mantiene (seccion 27 del maestro).
- MVP: MUST HAVE. Las seis obligaciones del area SEG son OBLIGATORIO sin excepcion y son exactamente la adecuacion a las Politicas de Actuacion de la ACE cuyo plazo transitorio ya vencio (OBL-PLAZO-03); es la razon de mayor urgencia comercial identificada en `02_validacion`.
- Dependencias: entra desde MOD-EIPD (controles requeridos por un riesgo detectado), MOD-PROV (controles exigidos a un encargado). Alimenta a MOD-EVID, MOD-DASH, MOD-PLAN.

### MOD-RET - Retencion y eliminacion

- Proposito: mantiene dos motores separados dentro de un mismo modulo: retencion de datos personales del titular (por finalidad, con fecha efectiva igual al maximo entre todas las normas aplicables) y retencion documental de cumplimiento propio de la empresa (aviso de privacidad, expedientes ARCO-POL/incidentes). Genera alertas, aprobacion y evidencia de eliminacion.
- Obligaciones propias: OBL-RET-01, OBL-RET-02, OBL-RET-03, OBL-RET-04, OBL-RET-05, OBL-RET-06, OBL-SANC-07 (7).
- Colaborador en: OBL-PROV-07 (devolucion/eliminacion de datos por el encargado), OBL-ARCO-06 (denegatoria parcial motivada por retencion legal distinta a la LPDP).
- Areas del prompt que absorbe: 22 Retencion (propia, integra).
- Decision vs. documento maestro: se divide conceptualmente en dos motores dentro del mismo modulo (decision 2.7.13, cierra inconsistencia 15); el maestro (seccion 21) trataba la retencion como un unico motor, lo que arriesgaba eliminar un aviso de privacidad junto con los datos de un titular o al reves.
- MVP: SHOULD HAVE. El campo basico "plazo de retencion y fundamento" puede vivir dentro del RAT desde el MVP; el motor completo (alertas automaticas, workflow de aprobacion de eliminacion, purga de backups) se incorpora inmediatamente despues sin bloquear el lanzamiento.
- Dependencias: entra desde MOD-RAT (finalidad de cada tratamiento), MOD-ARCO/MOD-INC (retencion de expedientes). Alimenta a MOD-TASK (alertas de vencimiento), MOD-EVID.

### MOD-CAP - Capacitacion

- Proposito: registra que el personal (y el Delegado en particular) recibio la capacitacion que exige la ley como medida organizativa minima, con periodicidad anual. El registro minimo obligatorio es una obligacion legal, no una funcionalidad opcional a evaluar.
- Obligaciones propias: OBL-CAP-01, OBL-CAP-02 (2).
- Colaborador en: OBL-DPO-05 (capacitacion anual especifica del Delegado).
- Areas del prompt que absorbe: 23 Capacitacion (propia, integra).
- Decision vs. documento maestro: se mantiene (seccion 28 del maestro), corregido de "funcionalidad a evaluar" a obligacion con registro minimo en MVP (decision 2.7.23, cierra inconsistencia 25).
- MVP: MUST HAVE, con alcance minimo (registro de quien, cuando y que capacitacion recibio). Funcionalidades diferenciadoras (cursos interactivos, microlearning, certificados) son COULD HAVE/FUTURE dentro del mismo modulo.
- Dependencias: entra desde MOD-ORG/MOD-USR (a quien capacitar, incluido el Delegado). Alimenta a MOD-EVID, MOD-PLAN.

### MOD-AUD - Auditoria (registro tecnico + programa anual)

- Proposito: mantiene dos cosas distintas dentro de un mismo modulo: el AuditLog (registro tecnico inmutable de acciones del sistema, que sustenta la evidencia de todos los demas modulos) y el programa sustantivo de auditoria de cumplimiento anual (alcance, hallazgos, plan de accion, cierre) que exigen las Politicas de la ACE.
- Obligaciones propias: OBL-AUD-01 (1).
- Colaborador en: OBL-PRIN-03 (responsabilidad demostrada es la razon de ser del AuditLog).
- Areas del prompt que absorbe: 24 Auditoria (propia, integra).
- Decision vs. documento maestro: se divide conceptualmente en dos submodulos (decision 2.7.26, cierra faltante 19); el maestro (seccion 29 "Auditoria y trazabilidad") los trataba como una sola cosa.
- MVP: MUST HAVE. El AuditLog tecnico es infraestructura que toda accion de todo modulo necesita desde el primer dia para poder demostrar despues lo que se hizo; el programa sustantivo de auditoria anual completo (hallazgos, plan de accion) puede madurar en V1.
- Dependencias: entra desde todos los modulos (cada accion se registra aqui). Alimenta a MOD-EVID, MOD-REP.

### MOD-EVID - Centro de evidencias

- Proposito: responde "que evidencia tenemos de esta obligacion", conectando por referencia archivos, aprobaciones, documentos, tareas y responsables de todos los demas modulos. Es la materializacion funcional del principio de responsabilidad demostrada (Art. 5 lit. i); no almacena una copia propia de cada dato, solo referencias y su verificacion de integridad.
- Obligaciones propias: OBL-PRIN-03 (1).
- Colaborador en: todo OBL-ID cuya columna "evidencia esperada" (en el JSON de la matriz) apunte a un artefacto de otro modulo.
- Areas del prompt que absorbe: 25 Centro de evidencias (propia, transversal por diseno segun el propio enunciado de la tarea).
- Decision vs. documento maestro: se mantiene y se redefine. El maestro (seccion 30, "Paquete de evidencias") lo trataba como un exportable; aqui se separan tres entidades distintas y relacionadas -Documento, Evidencia y AuditLog- y el paquete de evidencias pasa a ser solo una vista de exportacion sin almacenamiento propio (decision 2.7.4, cierra inconsistencias 4 y 11). Todo paquete exportado incluye verificacion de integridad propia (decision 2.7.24, cierra inconsistencia 26).
- MVP: MUST HAVE. Es la pieza que cumple la promesa central del producto ("mantener evidencias"); sin ella, ARCO-POL, Incidentes, Consentimiento y Controles no pueden demostrar lo actuado ante una auditoria o inspeccion.
- Dependencias: entra desde todos los modulos de proceso y de MOD-AUD (log tecnico) y MOD-TASK (tareas cerradas). Alimenta a MOD-REP (exportacion), MOD-DASH.

### MOD-DASH - Dashboard

- Proposito: presenta el estado del programa de proteccion de datos por perspectiva (Gerencia: vision general; Responsable: pendientes propios; Delegado/Legal: riesgos y decisiones; Auditor: evidencias), usando siempre lenguaje de "estado del programa" y nunca un porcentaje de cumplimiento legal.
- Obligaciones propias: ninguna (0).
- Colaborador en: OBL-PRIN-03 (el dashboard es la vitrina de la responsabilidad demostrada, sin afirmar cumplimiento).
- Areas del prompt que absorbe: 26 Dashboard (propia, transversal de visualizacion).
- Decision vs. documento maestro: se mantiene (seccion 31 del maestro), con la restriccion explicita de lenguaje que exige `02_validacion` (nunca "cumplimiento legal X%").
- MVP: MUST HAVE, en version basica (una vista por rol con pendientes, plazos proximos y estado de modulos clave). Widgets avanzados (tendencias historicas, comparativas) son SHOULD HAVE/V1.
- Dependencias: entra desde MOD-TASK, MOD-PLAN, MOD-EVID, MOD-CAL. No alimenta a otros modulos (es una vista de solo lectura).

### MOD-NOTIF - Notificaciones

- Proposito: entrega alertas de vencimiento, asignacion y escalamiento por el canal que corresponda (plataforma como minimo; email, Teams, Slack, SMS o WhatsApp como canales adicionales evaluables, sin asumir que todos se implementan). Es el mecanismo que convierte un plazo calculado en una accion humana a tiempo.
- Obligaciones propias: ninguna (0).
- Colaborador en: toda obligacion con plazo (ARCO-POL 20+20/10/5/3 dias, Incidentes 72 horas, DPO 15/3 dias, Sancionador 5/15 dias).
- Areas del prompt que absorbe: 27 Notificaciones (propia, integra).
- Decision vs. documento maestro: es nuevo como modulo propio. El maestro no lo trataba como modulo separado.
- MVP: MUST HAVE, con alcance minimo de dos canales (plataforma y correo electronico). Canales adicionales (Teams, Slack, SMS, WhatsApp) son SHOULD HAVE/COULD HAVE segun demanda de los primeros clientes.
- Dependencias: entra desde MOD-CAL (cuando avisar) y MOD-TASK/MOD-ARCO/MOD-INC (que avisar y a quien). No alimenta a otros modulos.

### MOD-REP - Reportes

- Proposito: genera reportes predefinidos (gerencial, ARCO-POL, incidentes, proveedores, RAT, auditoria, seguridad) a partir de los datos ya capturados en los demas modulos, sin duplicar su almacenamiento.
- Obligaciones propias: ninguna (0).
- Colaborador en: OBL-CONS-05, OBL-TRANSF-06 (carga de la prueba, materializada como reporte exportable).
- Areas del prompt que absorbe: 28 Reportes (propia, integra).
- Decision vs. documento maestro: es nuevo como modulo propio. El maestro no lo desarrollaba mas alla de menciones sueltas.
- MVP: SHOULD HAVE. El Centro de evidencias y el Dashboard ya cubren la necesidad minima de mostrar y exportar informacion en el MVP; los reportes predefinidos y programables se incorporan inmediatamente despues.
- Dependencias: entra desde MOD-EVID, MOD-AUD, MOD-RAT, MOD-ARCO, MOD-INC, MOD-PROV, MOD-CTRL. No alimenta a otros modulos.

### MOD-SEARCH - Busqueda global

- Proposito: permite ubicar rapidamente cualquier registro (tratamiento, caso ARCO-POL, proveedor, documento, tarea) desde un unico punto de entrada, sin necesidad de saber en que modulo vive.
- Obligaciones propias: ninguna (0).
- Colaborador en: ninguna obligacion especifica; su necesidad es de usabilidad para un usuario no especialista, que crece con el volumen de datos capturado por los demas modulos.
- Areas del prompt que absorbe: 29 Busqueda global (propia, integra).
- Decision vs. documento maestro: es nuevo. El maestro no lo menciona.
- MVP: COULD HAVE. Con el volumen de datos de un cliente nuevo, la navegacion por modulo es suficiente; gana valor real cuando ya hay historial acumulado (V1/Enterprise).
- Dependencias: entra desde todos los modulos (indice de lectura). No alimenta a otros modulos.

### MOD-CAL - Calendario y motor de plazos habiles

- Proposito: es el motor de plazos legales compartido (dias y horas habiles, asuetos nacionales configurables por ano) que ARCO-POL, Incidentes, el Delegado y el Procedimiento sancionador consultan para calcular cada fecha limite, evitando que cada modulo implemente su propio calculo con riesgo de reglas inconsistentes.
- Obligaciones propias: OBL-PLAZO-01, OBL-PLAZO-02 (2).
- Colaborador en: toda obligacion con plazo en dias/horas habiles de la matriz (mas de 20 obligaciones referencian este motor de forma indirecta).
- Areas del prompt que absorbe: 30 Calendario (propia, integra).
- Decision vs. documento maestro: es nuevo como modulo explicito. El maestro trataba el calendario de dias habiles como un detalle disperso en cada seccion; decision 2.7.15 de `02_validacion` lo convierte en motor transversal propio (cierra inconsistencia 17).
- MVP: MUST HAVE. Sin un unico calculo de dias habiles, cada modulo con plazo legal (ARCO-POL, Incidentes, DPO) arriesga calcular una fecha limite distinta para el mismo hecho.
- Dependencias: entra de forma manual (mantenimiento del calendario de asuetos por el equipo del producto, hasta que exista fuente oficial unificada). Alimenta a MOD-ARCO, MOD-INC, MOD-ORG (plazos del Delegado), MOD-REG (plazos del procedimiento sancionador), MOD-NOTIF.

### MOD-REG - Centro regulatorio, actualizaciones normativas y procedimiento sancionador

- Proposito: mantiene el marco normativo consultable (clasificado VIGENTE, FUTURO, DEROGADO, MODIFICADO), es el unico lugar donde vive el motor de doble estado de la reforma 659 (ver seccion 4), y gestiona el procedimiento sancionador cuando la ACE abre un caso contra la empresa (emplazamiento, alegatos, pago de multa, medidas adicionales, publicidad de resoluciones).
- Obligaciones propias: OBL-SANC-01, OBL-SANC-02, OBL-SANC-03, OBL-SANC-04, OBL-SANC-05, OBL-SANC-06, OBL-SANC-08, OBL-AUD-02, OBL-PLAZO-05 (9).
- Colaborador en: OBL-TRANSF-05 (puesta en conocimiento a la ACE), OBL-DPO-03 (comunicacion del nombramiento del Delegado a la ACE).
- Areas del prompt que absorbe: 31 Centro regulatorio y 32 Actualizaciones normativas (mismo motor de reglas versionadas, dos vistas de una misma capacidad).
- Decision vs. documento maestro: es nuevo. El "motor regulatorio" de la seccion 40 del maestro era una idea de arquitectura tecnica sin contraparte funcional; aqui se convierte en el modulo funcional "Centro regulatorio", y se le anade el "Procedimiento sancionador" que decision 2.7.25 identifica como una de las dos areas completas de la matriz sin ningun lugar funcional en el maestro (la otra es el Delegado, ya cubierta en MOD-ORG).
- MVP: SHOULD HAVE. El estado del Delegado (vigente hoy) puede mostrarse desde MOD-ORG con un campo simple desde el MVP; el motor de doble estado con activacion manual, el marco normativo consultable completo y el procedimiento sancionador (que solo se activa si la ACE abre un caso) se incorporan inmediatamente despues, antes de la primera renovacion anual del cliente.
- Dependencias: entra desde MOD-CAL (plazos del procedimiento sancionador). Alimenta a MOD-ORG (bandera de activacion del estado FUTURO), MOD-ARCO (quien resuelve casos segun el estado vigente), MOD-DASH, MOD-NOTIF.

### MOD-HELP - Centro de ayuda contextual

- Proposito: explica, en cada modulo, que es, por que hay que registrarlo, cual es su fundamento legal (OBL-ID) y cuando se necesita asesoria juridica externa. Es la materializacion funcional del principio de transparencia y lenguaje claro (Art. 5 lit. e) y del principio central del producto: usable por alguien que no es especialista en privacidad.
- Obligaciones propias: ninguna (0).
- Colaborador en: ninguna obligacion especifica de forma directa; su necesidad se sostiene en el principio de transparencia (Art. 5 lit. e) y en el objetivo exacto del producto (`04_objetivo_exacto_del_producto.md`).
- Areas del prompt que absorbe: 34 Centro de ayuda (propia, transversal).
- Decision vs. documento maestro: es nuevo como modulo propio. El maestro solo mencionaba tooltips dispersos dentro de la seccion 32 (UX).
- MVP: SHOULD HAVE. Textos de ayuda minimos (tooltips, un parrafo por campo) son MUST HAVE y viven dentro de cada modulo desde el dia uno; un Centro de ayuda buscable y centralizado, con contenido curado por modulo, es SHOULD HAVE/V1.
- Dependencias: entra desde todos los modulos (contenido de ayuda por pantalla). No alimenta a otros modulos.

---

## 3. Modulos transversales y como se conectan

El propio enunciado de esta tarea identifica siete modulos transversales: tareas, evidencias, auditoria, notificaciones, calendario, regulatorio y ayuda. Este mapa confirma los siete y agrega dos mas por el mismo criterio (ningun modulo de proceso deberia reimplementar su propia busqueda ni su propio panel de indicadores): Busqueda global y Dashboard. En total, 9 de los 25 modulos son transversales: MOD-TASK, MOD-CAL, MOD-AUD, MOD-EVID, MOD-NOTIF, MOD-REG, MOD-HELP, MOD-DASH, MOD-REP, mas MOD-USR y MOD-SEARCH (11 en total si se cuenta con criterio amplio; los 7 nombrados explicitamente por la tarea mas Dashboard, Reportes, Usuarios/roles y Busqueda por el mismo criterio de "dan soporte a todos, ninguno los posee en exclusiva").

Regla de conexion: un modulo transversal nunca es dueno de una obligacion de negocio (salvo la excepcion puntual de MOD-USR con 0, MOD-CAL con OBL-PLAZO-01/02 y MOD-AUD con OBL-AUD-01, que son las tres obligaciones que literalmente describen al motor transversal mismo, no un proceso de negocio). Todo modulo de proceso (cluster A a H) escribe hacia los transversales, nunca al reves:

```
Modulo de proceso (ORG, DIAG, PLAN, RAT, ARCO, PROV, TRANSF, INC,
EIPD, CTRL, RET, CAP, DOC, CONS, REG)
        |
        | escribe evento/tarea/plazo/registro
        v
+-------------------------------------------------------------+
| MOD-TASK (que hacer)  MOD-CAL (para cuando)                 |
| MOD-AUD (que paso)    MOD-EVID (con que prueba)              |
| MOD-NOTIF (a quien avisar)                                    |
+-------------------------------------------------------------+
        |
        | se consulta desde
        v
   MOD-DASH / MOD-REP / MOD-SEARCH / MOD-HELP
   (leen, nunca escriben en los modulos de proceso)
```

MOD-REG es un caso especial: es transversal en el sentido de que ningun modulo de proceso deberia mantener su propia copia del estado normativo, pero a la vez es propietario de obligaciones reales (Procedimiento sancionador), por lo que se clasifica como modulo de proceso en el arbol (cluster H) aunque su capacidad de "motor de reglas versionadas" sea consumida de forma transversal por MOD-ORG (ver seccion 4).

---

## 4. Modelado del doble estado de la reforma 659 (sin duplicar modulos)

La reforma (Decreto Legislativo 659, aprobado 17-sep-2026, APROBADA-PENDIENTE-PUBLICACION al 24-sep-2026) no genera un modulo nuevo ni una copia de ningun modulo existente. Se modela como un unico atributo de estado sobre una unica entidad ya descrita en MOD-ORG, mas una unica bandera de activacion que vive en MOD-REG:

1. La entidad "Responsable del tramite" vive solo en MOD-ORG. Tiene un campo `estado_normativo` con dos valores posibles: `DELEGADO_ACE` (hoy: persona certificada por la ACE conforme a los Arts. 15 y 17 vigentes, con las 8 obligaciones OBL-DPO-01 a 08) o `SUJETO_OBLIGADO_INTERNO` (futuro: cualquier persona interna designada por la empresa, sin certificacion ACE, segun la reforma). Nunca existen dos registros simultaneos para la misma empresa.
2. La bandera de activacion (`reforma_659_vigente = si/no`) vive en MOD-REG, no se activa por la sola fecha de aprobacion legislativa, y solo la activa manualmente el equipo del producto cuando se confirme la publicacion en el Diario Oficial y transcurran los 8 dias de vacatio legis (decision 2.7.16 de `02_validacion`).
3. Todo modulo que hoy atribuye un acto al "Delegado" en sentido literal (MOD-ARCO para prevencion, incompetencia y notificacion a receptores; MOD-CONS para la revocacion) no codifica el nombre "Delegado": codifica el rol logico "responsable del tramite ARCO-POL", que hoy se resuelve automaticamente hacia la persona con `estado_normativo = DELEGADO_ACE` y que, tras la activacion, se resuelve hacia la persona designada como `SUJETO_OBLIGADO_INTERNO`. Ningun modulo aparte de MOD-ORG necesita saber cual es el estado vigente; solo consulta "quien es hoy el responsable del tramite".
4. Las 17 obligaciones afectadas por la reforma (listadas en `matriz_obligaciones.md`, seccion "Obligaciones afectadas por la reforma 659") no cambian de modulo propietario cuando se activa la bandera: OBL-DPO-01 a 08 siguen siendo propiedad de MOD-ORG, OBL-ARCO-01/08/10/11 siguen siendo propiedad de MOD-ARCO, OBL-CONS-03 sigue siendo propiedad de MOD-CONS, OBL-CAP-02 sigue siendo propiedad de MOD-CAP y OBL-PLAZO-05/OBL-RET-04 siguen siendo propiedad de MOD-REG/MOD-RET respectivamente. Lo unico que cambia es el contenido de la regla que cada modulo aplica (por ejemplo, si la obligatoriedad de nombrar Delegado sigue vigente o no), nunca el modulo que la aplica.
5. Un expediente ARCO-POL o un registro DPO ya cerrado antes de la activacion conserva las reglas vigentes en el momento de su cierre (decision 2.7 seccion 41 del maestro, confirmada por `02_validacion`), por lo que el modulo debe versionar la regla aplicada, no solo el estado actual.

Este diseno evita exactamente el riesgo que señalaba `02_validacion` (inconsistencia 18): que el motor regulatorio quede desconectado de los modulos operativos. Con este modelo, activar la bandera en MOD-REG es la unica accion administrativa necesaria; ningun modulo de proceso requiere una migracion de datos ni una nueva pantalla.

---

## 5. Tabla de cobertura: OBL-ID -> modulo propietario (105 obligaciones)

Fuente: `01_legal/matriz_obligaciones.md`. Un OBL-ID aparece una sola vez en esta tabla (propietario unico); donde el modulo participa sin ser dueno se indico como "colaborador" en la ficha correspondiente de la seccion 2, no aqui.

### AMB (4) - propietario: MOD-DIAG

OBL-AMB-01, OBL-AMB-02, OBL-AMB-03, OBL-AMB-04.

### PRIN (4)

| OBL-ID | Modulo propietario |
|---|---|
| OBL-PRIN-01 | MOD-RAT |
| OBL-PRIN-02 | MOD-RAT |
| OBL-PRIN-03 | MOD-EVID |
| OBL-PRIN-04 | MOD-CONS |

### ARCO (15) - propietario: MOD-ARCO

OBL-ARCO-01, OBL-ARCO-02, OBL-ARCO-03, OBL-ARCO-04, OBL-ARCO-05, OBL-ARCO-06, OBL-ARCO-07, OBL-ARCO-08, OBL-ARCO-09, OBL-ARCO-10, OBL-ARCO-11, OBL-ARCO-12, OBL-ARCO-13, OBL-ARCO-14, OBL-ARCO-15.

### DPO (8) - propietario: MOD-ORG

OBL-DPO-01, OBL-DPO-02, OBL-DPO-03, OBL-DPO-04, OBL-DPO-05, OBL-DPO-06, OBL-DPO-07, OBL-DPO-08.

### AVISO (5) - propietario: MOD-DOC

OBL-AVISO-01, OBL-AVISO-02, OBL-AVISO-03, OBL-AVISO-04, OBL-AVISO-05.

### CONS (6) - propietario: MOD-CONS

OBL-CONS-01, OBL-CONS-02, OBL-CONS-03, OBL-CONS-04, OBL-CONS-05, OBL-CONS-06.

### SENS (8)

| OBL-ID | Modulo propietario |
|---|---|
| OBL-SENS-01 | MOD-RAT |
| OBL-SENS-02 | MOD-CONS |
| OBL-SENS-03 | MOD-RAT |
| OBL-SENS-04 | MOD-RAT |
| OBL-SENS-05 | MOD-RAT |
| OBL-SENS-06 | MOD-RAT |
| OBL-SENS-07 | MOD-CONS |
| OBL-SENS-08 | MOD-EIPD |

### TRAT (3) - propietario: MOD-RAT

OBL-TRAT-01, OBL-TRAT-02, OBL-TRAT-03.

### PROV (7) - propietario: MOD-PROV

OBL-PROV-01, OBL-PROV-02, OBL-PROV-03, OBL-PROV-04, OBL-PROV-05, OBL-PROV-06, OBL-PROV-07.

### TRANSF (6) - propietario: MOD-TRANSF

OBL-TRANSF-01, OBL-TRANSF-02, OBL-TRANSF-03, OBL-TRANSF-04, OBL-TRANSF-05, OBL-TRANSF-06.

### SEG (6) - propietario: MOD-CTRL

OBL-SEG-01, OBL-SEG-02, OBL-SEG-03, OBL-SEG-04, OBL-SEG-05, OBL-SEG-06.

### DOC (4)

| OBL-ID | Modulo propietario |
|---|---|
| OBL-DOC-01 | MOD-DOC |
| OBL-DOC-02 | MOD-RAT |
| OBL-DOC-03 | MOD-EIPD |
| OBL-DOC-04 | MOD-ARCO |

### INC (5) - propietario: MOD-INC

OBL-INC-01, OBL-INC-02, OBL-INC-03, OBL-INC-04, OBL-INC-05.

### CAP (2) - propietario: MOD-CAP

OBL-CAP-01, OBL-CAP-02.

### AUD (2)

| OBL-ID | Modulo propietario |
|---|---|
| OBL-AUD-01 | MOD-AUD |
| OBL-AUD-02 | MOD-REG |

### SANC (9)

| OBL-ID | Modulo propietario |
|---|---|
| OBL-SANC-01 | MOD-REG |
| OBL-SANC-02 | MOD-REG |
| OBL-SANC-03 | MOD-REG |
| OBL-SANC-04 | MOD-REG |
| OBL-SANC-05 | MOD-REG |
| OBL-SANC-06 | MOD-REG |
| OBL-SANC-07 | MOD-RET |
| OBL-SANC-08 | MOD-REG |
| OBL-SANC-09 | MOD-ARCO |

### PLAZO (5)

| OBL-ID | Modulo propietario |
|---|---|
| OBL-PLAZO-01 | MOD-CAL |
| OBL-PLAZO-02 | MOD-CAL |
| OBL-PLAZO-03 | MOD-PLAN |
| OBL-PLAZO-04 | MOD-ARCO |
| OBL-PLAZO-05 | MOD-REG |

### RET (6) - propietario: MOD-RET

OBL-RET-01, OBL-RET-02, OBL-RET-03, OBL-RET-04, OBL-RET-05, OBL-RET-06.

### Verificacion de cobertura

Total de filas de esta seccion: 105 (coincide con el total de la matriz). Conteo por modulo propietario: MOD-ARCO 18, MOD-RAT 11, MOD-ORG 8, MOD-REG 9, MOD-PROV 7, MOD-RET 7, MOD-CONS 9, MOD-DOC 6, MOD-TRANSF 6, MOD-CTRL 6, MOD-INC 5, MOD-DIAG 4, MOD-EIPD 2, MOD-CAP 2, MOD-CAL 2, MOD-EVID 1, MOD-AUD 1, MOD-PLAN 1; MOD-USR, MOD-TASK, MOD-DASH, MOD-NOTIF, MOD-REP, MOD-SEARCH, MOD-HELP: 0 obligaciones propias cada uno (justificados como transversales en la seccion 3). Suma: 18+11+8+9+7+7+9+6+6+6+5+4+2+2+2+1+1+1 = 105.

---

## 6. Tabla de cobertura: 29 areas del prompt -> modulo

| Area del prompt | Modulo | Tipo de asignacion |
|---|---|---|
| 8.1 Configuracion de empresa | MOD-ORG | Propia |
| 8.2 Usuarios, roles y permisos | MOD-USR | Propia |
| 8.3 Onboarding | MOD-DIAG | Submodulo (fusionado con Diagnostico) |
| 9 Diagnostico | MOD-DIAG | Propia |
| 10 Plan de cumplimiento | MOD-PLAN | Propia |
| 11 RAT | MOD-RAT | Propia |
| 12 Mapa de datos | MOD-RAT | Vista (sin base de datos propia) |
| 13 ARCO-POL | MOD-ARCO | Propia |
| 14 Centro de tareas | MOD-TASK | Propia, transversal |
| 15 Documentos y politicas | MOD-DOC | Propia |
| 16 Consentimiento | MOD-CONS | Propia |
| 17 Proveedores | MOD-PROV | Propia |
| 18 Transferencias internacionales | MOD-TRANSF | Propia |
| 19 Incidentes | MOD-INC | Propia |
| 20 EIPD/Riesgos | MOD-EIPD | Propia |
| 21 Controles de seguridad | MOD-CTRL | Propia |
| 22 Retencion | MOD-RET | Propia |
| 23 Capacitacion | MOD-CAP | Propia |
| 24 Auditoria | MOD-AUD | Propia |
| 25 Centro de evidencias | MOD-EVID | Propia, transversal |
| 26 Dashboard | MOD-DASH | Propia, transversal |
| 27 Notificaciones | MOD-NOTIF | Propia, transversal |
| 28 Reportes | MOD-REP | Propia, transversal |
| 29 Busqueda global | MOD-SEARCH | Propia, transversal |
| 30 Calendario | MOD-CAL | Propia, transversal |
| 31 Centro regulatorio | MOD-REG | Propia |
| 32 Actualizaciones normativas | MOD-REG | Submodulo (mismo motor de reglas) |
| 33 Portal del titular | MOD-ARCO | Submodulo/canal |
| 34 Centro de ayuda | MOD-HELP | Propia, transversal |

Las 29 areas quedan asignadas sin excepcion; 6 de ellas (12, 8.3, 32, 33) se absorben como vista o submodulo de otro modulo en vez de tener codigo propio, lo que explica por que el mapa tiene 25 modulos y no 29.

---

## 7. Entidades conceptuales principales que implica el mapa

Lista conceptual (sin modelo relacional ni SQL); cada entidad se ubica en el modulo que la administra como fuente de verdad, aunque otros modulos la referencien.

| Entidad | Modulo que la administra | Que representa |
|---|---|---|
| Organizacion | MOD-ORG | La empresa cliente y sus sucursales/unidades |
| ResponsableDelTramite (Delegado / SujetoObligado) | MOD-ORG | Persona con las funciones del Art. 15/17, con estado_normativo |
| Usuario | MOD-USR | Persona con acceso al sistema |
| Rol | MOD-USR | Conjunto de permisos, incluye rol Delegado |
| RespuestaDiagnostico | MOD-DIAG | Respuesta a una pregunta del cuestionario y sus disparadores |
| AccionDelPlan | MOD-PLAN | Item priorizado del plan de cumplimiento |
| ActividadDeTratamiento | MOD-RAT | Fila del RAT: dato, finalidad, base legal, sistema |
| CategoriaDeDato | MOD-RAT | Clasificacion, incluye marca de dato sensible |
| BaseJuridica | MOD-RAT | Una de las seis bases del Art. 5 lit. g |
| Sistema | MOD-RAT | Catalogo de sistemas/aplicaciones que procesan datos |
| RegistroDeConsentimiento | MOD-CONS | Evidencia de un consentimiento otorgado o revocado |
| ListaDeSupresion | MOD-CONS | Titulares que se opusieron a marketing directo |
| Encargado / TerceroReceptor / Subencargado | MOD-PROV | Tipos distintos de tercero con obligaciones propias |
| Contrato/DPA | MOD-PROV | Documento contractual entre responsable y encargado |
| Transferencia | MOD-TRANSF | Flujo de datos hacia otro responsable o fuera del pais |
| SolicitudARCOPOL | MOD-ARCO | Expediente de un titular, con estado y plazos |
| Incidente | MOD-INC | Vulneracion de seguridad y su ciclo de vida |
| EIPD | MOD-EIPD | Evaluacion de impacto de un tratamiento de alto riesgo |
| Control | MOD-CTRL | Medida de seguridad del catalogo, compartida con EIPD |
| ReglaDeRetencion | MOD-RET | Plazo y fundamento de conservacion o eliminacion |
| RegistroDeCapacitacion | MOD-CAP | Evidencia de que una persona recibio una capacitacion |
| Documento | MOD-DOC | Contenido versionado (aviso, politica, plantilla) |
| Tarea | MOD-TASK | Unidad de trabajo con responsable, plazo y origen |
| DiaHabil/Asueto | MOD-CAL | Calendario que resuelve el computo de plazos |
| Evidencia | MOD-EVID | Artefacto o referencia inmutable vinculada a un registro |
| AuditLog | MOD-AUD | Registro tecnico de acciones del sistema |
| ProgramaDeAuditoria | MOD-AUD | Ciclo anual de auditoria de cumplimiento |
| Notificacion | MOD-NOTIF | Alerta enviada por un canal a un destinatario |
| ReglaRegulatoria | MOD-REG | Version de una obligacion con fecha de vigencia y estado |
| CasoSancionador | MOD-REG | Expediente abierto por la ACE contra la empresa |
| ReporteExportable | MOD-REP | Vista de exportacion sobre datos de otros modulos |
| ArticuloDeAyuda | MOD-HELP | Texto explicativo asociado a un modulo/campo |

---

## 8. Riesgos del mapa propuesto

1. **MOD-ARCO concentra 18 de las 105 obligaciones (17 porciento del total).** Es el modulo mas denso del mapa; si su alcance crece sin control (portal publico, verificacion de identidad, tres ramas nuevas) puede volverse dificil de mantener como una sola unidad. Mitigacion sugerida (opinion de producto, no obligacion legal): tratar el "motor de casos" y el "canal Portal" como dos componentes internos con contratos de datos claros desde el diseno tecnico, aunque compartan un mismo modulo funcional.
2. **La linea entre "modulo transversal sin obligacion propia" y "modulo de proceso" no es binaria en todos los casos.** MOD-USR, MOD-CAL y MOD-AUD tienen caracter transversal pero si poseen (o en el caso de USR, no poseen pero sustentan) obligaciones reales; una lectura distinta de la matriz podria reasignar OBL-PLAZO-01/02 a MOD-ARCO en vez de a un modulo de calendario separado. Este documento eligio la lectura que minimiza numero de modulos evitando duplicar el calculo de plazos en cada modulo de proceso, pero es una decision de diseno, no un hecho legal.
3. **La fusion de ARCO-POL y Portal del titular en un solo modulo (decision de este documento, no de `02_validacion`) puede no reflejar la separacion de equipos o de release que el negocio finalmente decida** (por ejemplo, si el portal publico requiere un release y una superficie de riesgo de seguridad claramente distintos del motor interno). Se documenta explicitamente como submodulo/canal para que una decision tecnica posterior pueda separarlos sin romper la propiedad de las obligaciones (que seguirian siendo de MOD-ARCO).
4. **MOD-REG absorbe tres capacidades distintas** (marco normativo consultable, motor de doble estado de la reforma 659, procedimiento sancionador). Si el volumen de trabajo real del procedimiento sancionador resulta bajo (depende de cuantas empresas clientes reciban un caso de la ACE), esta capacidad podria quedar subutilizada dentro de un modulo mas grande; se mantuvo unido aqui porque las tres comparten la misma relacion (interaccion formal con la ACE) y porque dividirlas incrementaria el numero de modulos sin una obligacion adicional que lo justifique.
5. **La clasificacion MVP resultante es mas amplia (18 de 25 modulos en MUST HAVE) que la hipotesis de 11 modulos del documento maestro.** Esto es una consecuencia directa del angulo obligacion-primero (58 de 105 obligaciones son OBLIGATORIO) y de la decision 2.7.29 de `02_validacion` de anclar el MVP a los plazos transitorios ya vencidos, no una recomendacion de que el primer release deba construir los 18 modulos completos de una sola vez; cada ficha de la seccion 2 ya distingue, dentro del modulo, que alcance minimo es MUST HAVE y que enriquecimiento es SHOULD/COULD/FUTURE. La priorizacion fina de secuencia de construccion (que modulo primero, cuales en paralelo) es una decision de producto posterior a este mapa, no resuelta aqui.
6. **El modelo de doble estado de la reforma 659 (seccion 4) depende de un solo campo de bandera manual.** Si esa bandera no se activa a tiempo tras la publicacion oficial (o se activa antes de tiempo), toda obligacion de MOD-ORG, MOD-ARCO, MOD-CONS, MOD-CAP y MOD-REG que dependa del estado normativo quedaria calculando el escenario equivocado; requiere un procedimiento operativo claro de quien activa la bandera y cuando, que este documento no resuelve por tratarse de un proceso interno del equipo del producto, no una obligacion legal.
7. **La acotacion del principio de minimizacion de datos (decision 2.7.21 de `02_validacion`) a solo RAT/Proveedores/Retencion, excluyendo ARCO-POL/Portal/Incidentes/Consentimiento, es una decision de producto que este mapa hereda sin cuestionar.** Si el criterio cambia en una fase posterior, afecta directamente el diseno de campos de MOD-ARCO, MOD-INC y MOD-CONS.
8. **Ocho modulos de este mapa (MOD-PLAN, MOD-NOTIF, MOD-REP, MOD-SEARCH, MOD-CAL, MOD-REG, MOD-HELP, mas la fusion Onboarding/Diagnostico en MOD-DIAG) son nuevos o fusionados respecto del documento maestro, sin equivalente 1 a 1 en su seccion 6 de modulos.** Esto responde a los gaps identificados en `02_validacion` (secciones 2.5 y 2.6), pero implica que la ficha extendida A-Q de cada uno de estos ocho debera redactarse desde cero, sin una seccion previa del maestro de la cual partir.
