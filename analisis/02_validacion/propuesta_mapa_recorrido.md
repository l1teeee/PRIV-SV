# Propuesta de mapa de modulos - Angulo recorrido del usuario primero

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (prohibido proponer codigo, SQL, APIs, stack o infraestructura).

Angulo de diseno asignado: RECORRIDO-DEL-USUARIO-PRIMERO. Este documento parte de los 16 pasos del objetivo del producto (`PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md`, seccion 49) y de los 11 casos end-to-end (`00_prompt_analisis_funcional.md`, seccion 35) y disena los modulos como etapas de un recorrido que una persona no especialista pueda seguir de principio a fin: EMPEZAR -> DIAGNOSTICAR -> PLANIFICAR -> REGISTRAR -> OPERAR -> DEMOSTRAR, con un conjunto de modulos transversales visibles en todo momento.

Fuentes base: `01_legal/matriz_obligaciones.md` y `matriz_obligaciones.json` (105 obligaciones, IDs canonicos OBL-AREA-NN, usados en todo este documento), `01_legal/03_hallazgos_regulatorios.md` (secciones 3, 5, 6, 8, 9, 11), `02_validacion/02_validacion_de_la_idea.md` (en particular las 32 decisiones de alcance de la seccion 2.7), y `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md`.

Convencion: toda fila que cita un OBL-ID es una afirmacion verificada contra la matriz. Toda clasificacion MVP y toda decision de fusion/division de modulos es una decision de diseno de producto, marcada explicitamente "[opinion de producto]" cuando no deriva directamente de una obligacion legal o de una decision ya tomada en `02_validacion_de_la_idea.md`.

---

## 0. Resumen de modulos

25 modulos de primer nivel: 19 modulos de recorrido (organizados en 6 etapas) y 6 modulos transversales visibles desde cualquier etapa.

| Codigo | Nombre | Etapa | MVP |
|---|---|---|---|
| MOD-001 | Organizacion y Personas | Empezar | MUST HAVE |
| MOD-002 | Onboarding | Empezar | MUST HAVE |
| MOD-003 | Diagnostico de Cumplimiento | Diagnosticar | MUST HAVE |
| MOD-004 | Plan de Cumplimiento | Planificar | MUST HAVE |
| MOD-005 | RAT y Mapa de Datos | Registrar | MUST HAVE |
| MOD-006 | Consentimiento | Registrar | MUST HAVE |
| MOD-007 | Documentos y Politicas | Registrar | MUST HAVE |
| MOD-008 | Proveedores y Encargados | Registrar | MUST HAVE |
| MOD-009 | Transferencias Internacionales | Registrar | SHOULD HAVE |
| MOD-010 | ARCO-POL | Operar | MUST HAVE |
| MOD-011 | Portal del Titular | Operar | SHOULD HAVE |
| MOD-012 | Incidentes de Seguridad | Operar | MUST HAVE |
| MOD-013 | Riesgos y EIPD | Operar | SHOULD HAVE |
| MOD-014 | Controles de Seguridad | Operar | MUST HAVE |
| MOD-015 | Retencion y Eliminacion | Operar | SHOULD HAVE |
| MOD-016 | Capacitacion | Operar | MUST HAVE (registro minimo) |
| MOD-017 | Auditoria de Cumplimiento | Demostrar | SHOULD HAVE |
| MOD-018 | Centro de Evidencias | Demostrar | MUST HAVE |
| MOD-019 | Dashboard y Reportes | Demostrar | MUST HAVE (dashboard) / SHOULD HAVE (reportes avanzados) |
| MOD-020 | Centro de Tareas | Transversal | MUST HAVE |
| MOD-021 | Notificaciones | Transversal | MUST HAVE (canales basicos) |
| MOD-022 | Calendario y Motor de Plazos | Transversal | MUST HAVE |
| MOD-023 | Centro Regulatorio | Transversal | MUST HAVE (nucleo) / SHOULD HAVE (procedimiento sancionador) |
| MOD-024 | Busqueda Global | Transversal | COULD HAVE |
| MOD-025 | Centro de Ayuda | Transversal | MUST HAVE (basico) |

---

## 1. Arbol ASCII del mapa de modulos

```
PLATAFORMA DE AUTOGESTION DE PROTECCION DE DATOS (El Salvador)
|
|== ETAPA 1: EMPEZAR ==========================================
|    |-- MOD-001 Organizacion y Personas
|    |    |-- Empresa (razon social, sucursales, areas, sector, exclusiones Art. 3)
|    |    |-- Usuarios y Roles (RBAC, roles estandar/personalizados, separacion de funciones)
|    |    v-- Delegado / Responsable Interno de Datos (doble estado, ver seccion 4)
|    v-- MOD-002 Onboarding (alta guiada de organizacion + usuarios + roles)
|
|== ETAPA 2: DIAGNOSTICAR =====================================
|    v-- MOD-003 Diagnostico de Cumplimiento
|         |-- Cuestionario guiado (empleados, camaras, CV, CRM, app movil, biometria,
|         |   salud, cloud, datos fuera del pais, marketing, menores...)
|         |-- Deteccion de exclusiones (Art. 3)
|         v-- Motor de disparo: respuesta -> tratamiento + tarea + documento + riesgo
|
|== ETAPA 3: PLANIFICAR =======================================
|    v-- MOD-004 Plan de Cumplimiento (acciones priorizadas: criticas/importantes/recomendadas)
|
|== ETAPA 4: REGISTRAR ========================================
|    |-- MOD-005 RAT y Mapa de Datos
|    |    |-- Registro de Actividades de Tratamiento (RAT), fuente unica de verdad
|    |    |-- Mapa de datos (vista: origen -> sistema -> area -> proveedor -> pais -> eliminacion)
|    |    v-- Catalogo de sistemas (alta/edicion unica, consultado por referencia)
|    |-- MOD-006 Consentimiento
|    |    |-- Registro de consentimiento (referencia a version del Aviso, nunca copia)
|    |    |-- Revocacion (mini flujo de dos plazos: 5 + 5 dias habiles)
|    |    v-- Sub-flujo titular menor de edad (consentimiento parental)
|    |-- MOD-007 Documentos y Politicas
|    |    |-- Politica de Proteccion de Datos / Politica de Privacidad
|    |    |-- Aviso de Privacidad (versionado, 9 literales del Art. 24)
|    |    v-- Plantillas, borradores, aprobacion configurable por tipo de documento
|    |-- MOD-008 Proveedores y Encargados
|    |    |-- Encargados
|    |    |-- Terceros / Receptores
|    |    |-- Subencargados
|    |    v-- Contratos / DPA (tipo de documento, enlazado a Documentos)
|    v-- MOD-009 Transferencias Internacionales (enlaza por referencia a Proveedores)
|
|== ETAPA 5: OPERAR ===========================================
|    |-- MOD-010 ARCO-POL (formulario interno seguro en MVP)
|    |    |-- Verificacion de identidad del titular (titular/representante/heredero)
|    |    |-- Rama: Incompetencia (devolucion, 5 dias habiles)
|    |    |-- Rama: Notificacion a receptores (5 dias habiles)
|    |    v-- Rama: Reclamo ante la Direccion de Proteccion de Datos (ACE)
|    |-- MOD-011 Portal del Titular (V1/Enterprise: autoregistro publico)
|    |-- MOD-012 Incidentes de Seguridad (dos hitos de 72 horas: notificacion e inicio de revision)
|    |-- MOD-013 Riesgos y EIPD (usa el catalogo de Controles de MOD-014, no uno propio)
|    |-- MOD-014 Controles de Seguridad (catalogo unico de controles con evidencia)
|    |-- MOD-015 Retencion y Eliminacion
|    |    |-- Motor de retencion de datos del titular (por finalidad, maximo entre OBL-RET aplicables)
|    |    v-- Motor de retencion documental de cumplimiento propio (avisos 10 anios, expedientes 5 anios)
|    v-- MOD-016 Capacitacion
|         |-- Capacitacion general del personal (registro minimo, MVP)
|         v-- Capacitacion especifica del Delegado / Responsable Interno
|
|== ETAPA 6: DEMOSTRAR ========================================
|    |-- MOD-017 Auditoria de Cumplimiento (programa anual sustantivo, distinto del log tecnico)
|    |-- MOD-018 Centro de Evidencias (Documento + Evidencia + AuditLog, vista de exportacion con hash)
|    v-- MOD-019 Dashboard y Reportes (por perspectiva: Gerencia/Responsable/Legal/Auditor)
|
v== MODULOS TRANSVERSALES (visibles desde cualquier etapa, ver seccion 3) =====
     |-- MOD-020 Centro de Tareas
     |-- MOD-021 Notificaciones
     |-- MOD-022 Calendario y Motor de Plazos (dias/horas habiles, asuetos)
     |-- MOD-023 Centro Regulatorio
     |    |-- Marco normativo consultable (VIGENTE / FUTURO / DEROGADO / MODIFICADO)
     |    |-- Actualizaciones normativas (funcion transversal, no modulo aparte)
     |    |-- Procedimiento Sancionador (contestacion, pago de multa, medidas adicionales)
     |    v-- Tramites ante la ACE (nombramiento delegado, transferencias, credenciales)
     |-- MOD-024 Busqueda Global
     v-- MOD-025 Centro de Ayuda (contextual por modulo: que es, por que, fundamento)
```

Nota de navegacion [opinion de producto]: para no sobrecargar a un usuario no especialista con 25 entradas de menu, la UI debe agrupar por las 6 etapas (6 grupos colapsables) mas una barra fija de 6 modulos transversales, nunca una lista plana de 25 items. Ver riesgo 1 en la seccion 8.

---

## 2. Ficha resumida de cada modulo

Cada ficha indica: proposito, submodulos (si existen), obligaciones que cubre como propietario (lista completa en la tabla de la seccion 5), areas del prompt que absorbe, decision respecto al documento maestro, clasificacion MVP con justificacion, y dependencias (que modulos consume / a quienes entrega).

### MOD-001 Organizacion y Personas
- Proposito: registrar la identidad legal de la empresa, su estructura interna y las personas responsables. Administra el modelo de roles (RBAC) y aloja el ciclo de vida completo del Delegado / Responsable Interno de Datos, incluido el doble estado de la reforma 659. Es el punto de partida obligatorio antes de usar cualquier otro modulo.
- Submodulos: Empresa; Usuarios y Roles; Delegado / Responsable Interno de Datos.
- Obligaciones que cubre (propietario): OBL-DPO-01 a 08 (8).
- Areas del prompt que absorbe: 8.1 (Configuracion de empresa), 8.2 (Usuarios, roles y permisos).
- Decision respecto al maestro: se fusiona (sec. 11 Modulo de organizacion + sec. 12 Usuarios y roles) y se amplia con el submodulo Delegado, ausente en el maestro (hallazgo estructural principal de `02_validacion_de_la_idea.md`, decision 2.7.7).
- MVP: MUST HAVE. Sin organizacion, usuarios y roles no puede operar ningun otro modulo; ademas el Delegado es OBLIGATORIO hoy (OBL-DPO-01, Arts. 15 y 17 vigentes).
- Dependencias: sale hacia todos los modulos (identidad de organizacion/usuario/rol es prerequisito universal). Entra desde MOD-002 (Onboarding la completa por primera vez) y MOD-023 (bandera de activacion del doble estado).

### MOD-002 Onboarding
- Proposito: guiar a la persona designada, sin conocimiento juridico previo, a travez de la alta inicial de su organizacion, usuarios y roles en la primera sesion. Entrega como salida una organizacion configurada, lista para el Diagnostico.
- Obligaciones que cubre (propietario): ninguna con OBL-ID propio; es un proceso de UX que ejecuta el alta de MOD-001. No se inventa obligacion legal donde no la hay.
- Areas del prompt que absorbe: 8.3 (Onboarding).
- Decision respecto al maestro: se divide de la sec. 15 del maestro ("Onboarding / Compliance Wizard"), separando el alta de organizacion (este modulo) del cuestionario de obligaciones (MOD-003), por decision 2.7.5.
- MVP: MUST HAVE. Es la puerta de entrada del producto; sin el, MOD-001 se llenaria sin guia.
- Dependencias: entra hacia MOD-001 (lo completa). Sale hacia MOD-003 (dispara el diagnostico al finalizar).

### MOD-003 Diagnostico de Cumplimiento
- Proposito: cuestionario guiado y repetible (se puede volver a ejecutar cuando la empresa cambia de actividad) que traduce preguntas sencillas en tratamientos, tareas, documentos y riesgos sugeridos. Detecta ademas las exclusiones del Art. 3 antes de sobre-obligar a la empresa.
- Obligaciones que cubre (propietario): OBL-AMB-01 a 04 (4).
- Areas del prompt que absorbe: 9 (Diagnostico inicial).
- Decision respecto al maestro: se divide de la sec. 15 del maestro (ver MOD-002), decision 2.7.5 y 2.7.27.
- MVP: MUST HAVE. Es el mecanismo concreto para identificar exposicion legal, urgente porque el plazo de adecuacion a las Politicas ACE ya vencio (OBL-PLAZO-03, 2/3-dic-2025).
- Dependencias: entra desde MOD-002. Sale hacia MOD-004 (genera el plan), MOD-005 (siembra tratamientos en el RAT), MOD-013 (dispara EIPD cuando corresponde).

### MOD-004 Plan de Cumplimiento
- Proposito: convierte el resultado del diagnostico en una lista priorizada de acciones (criticas, importantes, recomendadas), cada una con responsable, fecha, fundamento normativo, evidencia esperada y estado. Es la traduccion operativa central de "obligacion legal" a "tarea gestionable".
- Obligaciones que cubre (propietario): OBL-PLAZO-03 (1).
- Areas del prompt que absorbe: 10 (Plan de cumplimiento).
- Decision respecto al maestro: es nuevo como modulo propio; el maestro solo lo menciona implicitamente en la sec. 49 (objetivo final: "Genera un plan de trabajo") sin desarrollarlo como modulo, aunque el area 10 del prompt de analisis funcional si lo exige.
- MVP: MUST HAVE. Es la propuesta de valor central del producto (obligaciones -> procesos + tareas + plazos) y el mecanismo que justifica comercialmente la urgencia de los plazos vencidos (decision 2.7.29).
- Dependencias: entra desde MOD-003. Sale hacia MOD-020 (genera tareas concretas), MOD-019 (alimenta el dashboard).

### MOD-005 RAT y Mapa de Datos
- Proposito: registro de actividades de tratamiento como fuente unica de verdad de que datos trata la empresa, con que finalidad, base juridica, categorias y sistemas. El Mapa de datos es una vista sobre esta misma informacion, no una base de datos aparte.
- Submodulos: Registro de Actividades de Tratamiento (RAT); Mapa de datos (vista); Catalogo de sistemas.
- Obligaciones que cubre (propietario): OBL-PRIN-02; OBL-SENS-01, 04, 06, 08; OBL-TRAT-01, 03; OBL-DOC-02 (8).
- Areas del prompt que absorbe: 11 (RAT), 12 (Mapa de datos, como vista).
- Decision respecto al maestro: se fusiona (sec. 13 Inventario de datos + sec. 14 RAT/ROPA); el Mapa de datos deja de ser modulo separado (decision 2.7.1, inconsistencia 1).
- MVP: MUST HAVE. Es el nucleo operativo identificado en `02_validacion_de_la_idea.md` 2.1, con respaldo normativo directo (OBL-DOC-02, medida organizativa obligatoria de las Politicas ACE).
- Dependencias: entra desde MOD-003 (tratamientos sugeridos). Sale hacia MOD-006, MOD-008, MOD-009, MOD-013, MOD-014, MOD-015 (todos referencian tratamientos del RAT).

### MOD-006 Consentimiento
- Proposito: registrar cuando el consentimiento es la base juridica elegida (no todo tratamiento lo requiere), con evidencia de finalidad, canal, version del aviso mostrado y fecha; gestionar la revocacion como flujo de dos plazos encadenados; dar tratamiento reforzado a datos sensibles, biometria y menores de edad.
- Submodulos: Registro y revocacion de consentimiento; Sub-flujo titular menor de edad.
- Obligaciones que cubre (propietario): OBL-PRIN-01, 04; OBL-CONS-01 a 06 (6); OBL-SENS-02, 03, 07; OBL-TRAT-02 (12).
- Areas del prompt que absorbe: 16 (Consentimiento).
- Decision respecto al maestro: se mantiene (sec. 19), con dos sub-flujos nuevos incorporados (menores de edad, alternativa no biometrica obligatoria) por los faltantes 25 y 27.
- MVP: MUST HAVE. Concentra 4 obligaciones OBLIGATORIO (CONS-01, 02, 03, 04) con riesgo de infraccion muy grave (26 a 40 salarios minimos, seccion 6 de `03_hallazgos_regulatorios.md`); el registro basico se prioriza en el MVP sobre la sincronizacion con sistemas externos, que queda en V1.
- Dependencias: entra desde MOD-005 (tratamiento y base juridica) y MOD-007 (version del aviso vigente, nunca copiada). Sale hacia MOD-008 (notificacion al encargado tras revocacion), MOD-010 (oposicion a marketing directo).

### MOD-007 Documentos y Politicas
- Proposito: gestor documental regulatorio que produce y versiona la Politica de Proteccion de Datos, la Politica de Privacidad y el Aviso de Privacidad, con flujo de aprobacion configurable por tipo de documento. Es el motor documental generico que otros modulos reutilizan por referencia (por ejemplo, Contratos/DPA dentro de Proveedores).
- Obligaciones que cubre (propietario): OBL-AVISO-01 a 05 (5); OBL-DOC-01 (1) (6).
- Areas del prompt que absorbe: 15 (Documentos y politicas).
- Decision respecto al maestro: se mantiene (sec. 20), absorbe Contratos/DPA como tipo de documento (fusion parcial de la sec. 23 del maestro), decision 2.7.2.
- MVP: MUST HAVE. El Aviso de Privacidad (OBL-AVISO-01/02/03/05) es OBLIGATORIO y su mecanismo de publicacion tiene plazo transitorio ya vencido (OBL-PLAZO-04, 23-may-2025).
- Dependencias: entra desde MOD-003, MOD-005. Sale hacia MOD-006 (version del aviso referenciada), MOD-008 (Contratos/DPA), MOD-015 (retencion documental de 10 anios).

### MOD-008 Proveedores y Encargados
- Proposito: registrar a los encargados del tratamiento, terceros/receptores y subencargados de la empresa, con sus contratos/DPA, medidas de seguridad y evaluacion de riesgo, como tres tipos de entidad con obligaciones propias en lugar de un unico modulo generico.
- Submodulos: Encargados; Terceros/Receptores; Subencargados; Contratos/DPA (tipo de documento).
- Obligaciones que cubre (propietario): OBL-PROV-01 a 07 (7).
- Areas del prompt que absorbe: 17 (Proveedores).
- Decision respecto al maestro: se fusiona (sec. 22 Proveedores y terceros + sec. 23 Contratos/DPA como submodulo documental), y se divide internamente en tres tipos de entidad (decision 2.7.2, 2.7.8, inconsistencia 9).
- MVP: MUST HAVE. Identificado como nucleo por `02_validacion_de_la_idea.md` 2.1; concentra obligaciones OBLIGATORIO (PROV-01, 02, 03, 04) y casi toda empresa objetivo tiene al menos un proveedor de tecnologia/cloud.
- Dependencias: entra desde MOD-005 (tratamientos que involucran proveedores). Sale hacia MOD-009 (todo proveedor extranjero genera registro en Transferencias), MOD-007 (contratos como documento).

### MOD-009 Transferencias Internacionales
- Proposito: registrar cada flujo de datos hacia otro pais (tratamiento, proveedor, pais, base juridica, salvaguarda, evidencia de puesta en conocimiento a la ACE), detectando transferencias no documentadas al cruzar Proveedores con el RAT.
- Obligaciones que cubre (propietario): OBL-TRANSF-01 a 06 (6).
- Areas del prompt que absorbe: 18 (Transferencias internacionales).
- Decision respecto al maestro: se mantiene (sec. 24), enlaza por referencia a Proveedores en vez de duplicar campos de contrato (decision 2.7.2).
- MVP: SHOULD HAVE. Las obligaciones son mayormente CONDICIONAL (se activan solo si hay transferencia real); el diagnostico las detecta desde el MVP, pero el modulo completo (evaluacion de pais, tramite ante la ACE) puede madurar en V1 sin bloquear el lanzamiento [opinion de producto].
- Dependencias: entra desde MOD-005, MOD-008 (proveedor/pais). Sale hacia MOD-006 (consentimiento previo), MOD-023 (puesta en conocimiento de la ACE), MOD-018 (carga de la prueba).

### MOD-010 ARCO-POL
- Proposito: gestionar el ciclo de vida completo de una solicitud de un titular (acceso, rectificacion, cancelacion, oposicion, portabilidad, olvido, limitacion), desde la verificacion de identidad hasta el cierre, con las tres ramas que el maestro no contemplaba: incompetencia, notificacion a receptores y reclamo ante la ACE.
- Submodulos: Verificacion de identidad del titular; Rama Incompetencia; Rama Notificacion a receptores; Rama Reclamo ante la ACE.
- Obligaciones que cubre (propietario): OBL-ARCO-01 a 15 (15).
- Areas del prompt que absorbe: 13 (ARCO-POL).
- Decision respecto al maestro: se mantiene y se amplia (sec. 17), con las tres ramas nuevas y el subproceso de verificacion de identidad (decisiones 2.7.10 y 2.7.18, inconsistencia 12, faltantes 8 y 11).
- MVP: MUST HAVE. Concentra la mayor cantidad de obligaciones de toda la matriz (20 candidatas segun el conteo por modulo de `matriz_obligaciones.md`), con plazo transitorio ya vencido para establecer mecanismos (OBL-PLAZO-04); es nucleo segun `02_validacion_de_la_idea.md` 2.1.
- Dependencias: entra desde MOD-011 (canal de recepcion), MOD-006 (oposicion a marketing). Sale hacia MOD-008/MOD-009 (notificacion a receptores), MOD-022 (motor de plazos), MOD-023 (reclamo ante la ACE), MOD-018 (evidencia del expediente).

### MOD-011 Portal del Titular
- Proposito: canal publico opcional para que el titular consulte el aviso y la politica, presente ARCO-POL y consulte el estado de su solicitud de forma autenticada. En el MVP la obligacion legal de "mecanismos" de ejercicio de derechos se satisface con el formulario interno seguro de MOD-010; el portal publico con autoregistro es una capa adicional posterior.
- Obligaciones que cubre (propietario): OBL-DOC-04, OBL-PLAZO-04 (2).
- Areas del prompt que absorbe: 33 (Portal del titular).
- Decision respecto al maestro: se mantiene pero se reduce el alcance en MVP (sec. 18 Portal de privacidad), decision 2.7.30: "el MVP puede satisfacer la obligacion legal con un formulario interno seguro; el portal publico dedicado es V1/Enterprise".
- MVP: SHOULD HAVE (V1). La obligacion legal (OBL-DOC-04, OBL-PLAZO-04) ya esta cubierta por el formulario interno de MOD-010; el portal publico añade superficie de riesgo de identidad y exposicion que conviene madurar despues del lanzamiento.
- Dependencias: entra desde MOD-007 (aviso/politica publicados). Sale hacia MOD-010 (crea solicitudes ARCO-POL), MOD-022 (calendario de estado visible al titular).

### MOD-012 Incidentes de Seguridad
- Proposito: gestionar el ciclo completo de una vulneracion de seguridad (deteccion, contencion, analisis, decision, notificacion, remediacion, cierre) con dos hitos de 72 horas modelados por separado: notificacion externa a la ACE/Fiscalia/titulares e inicio de la revision interna.
- Obligaciones que cubre (propietario): OBL-INC-01 a 05 (5).
- Areas del prompt que absorbe: 19 (Incidentes).
- Decision respecto al maestro: se mantiene (sec. 25), con los dos hitos de 72 horas separados y visibles, criterio conservador por defecto de horas corridas (decision 2.7.11, inconsistencia 13).
- MVP: MUST HAVE. Todas sus 5 obligaciones son OBLIGATORIO, con el plazo mas critico y visible del corpus (72 horas); es nucleo segun `02_validacion_de_la_idea.md` 2.1.
- Dependencias: entra desde MOD-005 (sistemas y datos afectados), MOD-014 (controles vulnerados). Sale hacia MOD-020 (checklist de tareas), MOD-022 (cronometro), MOD-023 (reporte a infraestructura critica si aplica), MOD-018 (evidencia).

### MOD-013 Riesgos y EIPD
- Proposito: evaluar tratamientos de alto riesgo (biometria, salud, menores, monitoreo, transferencias, gran escala) y generar Evaluaciones de Impacto en la Privacidad, seleccionando controles del catalogo unico de MOD-014 en vez de mantener una lista paralela; el resultado siempre requiere aprobacion humana, nunca es una conclusion legal automatica.
- Obligaciones que cubre (propietario): OBL-DOC-03 (1).
- Areas del prompt que absorbe: 20 (EIPD/Riesgos).
- Decision respecto al maestro: se mantiene (sec. 26), comparte la entidad Control con Controles de seguridad en vez de duplicarla (decision 2.7.3, inconsistencia 3).
- MVP: SHOULD HAVE. La EIPD es OBLIGATORIO (OBL-DOC-03) pero solo se activa por disparadores especificos que el diagnostico ya detecta desde el MVP; el flujo completo de scoring/aprobacion puede seguir en V1 sin dejar el disparador sin tarea manual [opinion de producto].
- Dependencias: entra desde MOD-003, MOD-005 (tratamientos de riesgo). Sale hacia MOD-014 (controles), MOD-020 (tareas de mitigacion).

### MOD-014 Controles de Seguridad
- Proposito: catalogo unico de controles tecnicos, organizativos y fisicos (MFA, cifrado, backups, eliminacion segura, etc.) con evidencia de implementacion, responsable, vigencia y estado; registra evidencia, no ejecuta ni sustituye herramientas de seguridad.
- Obligaciones que cubre (propietario): OBL-SEG-01 a 06 (6); OBL-SENS-05 (1) (7).
- Areas del prompt que absorbe: 21 (Controles de seguridad).
- Decision respecto al maestro: se mantiene (sec. 27), entidad Control compartida con Riesgos/EIPD (decision 2.7.3).
- MVP: MUST HAVE. Identificado como nucleo por `02_validacion_de_la_idea.md` 2.1; concentra el bloque de infraccion grave (11 a 25 salarios minimos) por no implementar medidas de la ACE.
- Dependencias: entra desde MOD-005, MOD-009 (sistemas y transferencias que requieren control). Sale hacia MOD-013 (catalogo compartido), MOD-018 (evidencia de controles), MOD-017 (insumo de auditoria).

### MOD-015 Retencion y Eliminacion
- Proposito: dos motores de retencion separados para no arriesgar el dato equivocado: retencion de datos personales del titular (por finalidad, con fecha efectiva igual al maximo entre todos los OBL-RET aplicables al giro del cliente) y retencion documental de cumplimiento propio de la empresa (avisos 10 anios, expedientes ARCO-POL/incidentes 5 anios).
- Submodulos: Motor de retencion de datos del titular; Motor de retencion documental de cumplimiento.
- Obligaciones que cubre (propietario): OBL-RET-01 a 06 (6).
- Areas del prompt que absorbe: 22 (Retencion).
- Decision respecto al maestro: se mantiene (sec. 21), dividido internamente en dos motores (decision 2.7.13, inconsistencia 15).
- MVP: SHOULD HAVE. Dos obligaciones son OBLIGATORIO sin condicion (RET-04, RET-06) y ya deben cubrirse, pero el resto son CONDICIONAL segun el giro del cliente (mercantil, tributario, LCLDA, salud); el motor completo de reglas por sector puede madurar en V1 mientras el MVP cubre el minimo de conservacion documental [opinion de producto].
- Dependencias: entra desde MOD-005, MOD-007 (documentos a retener). Sale hacia MOD-010 (bloqueo/eliminacion de expedientes), MOD-018 (evidencia de eliminacion).

### MOD-016 Capacitacion
- Proposito: dos programas de capacitacion distintos, cada uno con fundamento y periodicidad propios: registro minimo obligatorio de que el personal recibio capacitacion (todo el personal), y capacitacion especifica anual del Delegado / Responsable Interno.
- Submodulos: Capacitacion general del personal; Capacitacion del Delegado.
- Obligaciones que cubre (propietario): OBL-CAP-01, 02 (2).
- Areas del prompt que absorbe: 23 (Capacitacion).
- Decision respecto al maestro: se mantiene (sec. 28), pero el registro minimo pasa de "a evaluar" a MVP explicito (decision 2.7.23, inconsistencia 25).
- MVP: MUST HAVE (solo el registro minimo: quien, cuando, tema). OBL-CAP-01 es OBLIGATORIO sin condicion (medida organizativa de las Politicas ACE); cursos interactivos, microlearning y certificados quedan como funcionalidad diferenciadora en V1/V2.
- Dependencias: entra desde MOD-001 (lista de personal y del Delegado). Sale hacia MOD-018 (evidencia de capacitacion), MOD-019 (indicador de dashboard).

### MOD-017 Auditoria de Cumplimiento
- Proposito: programa sustantivo de auditoria anual (alcance, hallazgos, plan de accion, cierre), distinto del registro tecnico de trazabilidad (AuditLog, funcion transversal descrita en la seccion 3). Genera el recordatorio anual anclado a la ultima auditoria registrada.
- Obligaciones que cubre (propietario): OBL-AUD-01 (1).
- Areas del prompt que absorbe: 24 (Auditoria, en su componente de programa sustantivo).
- Decision respecto al maestro: se divide de la sec. 29 del maestro ("Auditoria y trazabilidad") en este modulo (programa sustantivo) mas la funcion transversal de AuditLog (decision 2.7.26, faltante 19).
- MVP: SHOULD HAVE. Es OBLIGATORIO (OBL-AUD-01, periodicidad anual) pero la primera auditoria formal solo es exigible tras el primer anio de operacion; el modulo debe existir desde el MVP como calendario/checklist, pero su primer ciclo completo puede caer ya en V1 [opinion de producto].
- Dependencias: entra desde MOD-014, MOD-005, MOD-018 (insumos a auditar). Sale hacia MOD-020 (plan de accion como tareas), MOD-019 (indicador de dashboard).

### MOD-018 Centro de Evidencias
- Proposito: responde "que evidencia tenemos de esta obligacion", conectando tres entidades separadas (Documento, Evidencia, registro tecnico AuditLog) sin mezclarlas; el paquete exportable es una vista sobre las tres, sin almacenamiento propio, con mecanismo propio de verificacion de integridad (hash o firma) en cada exportacion.
- Obligaciones que cubre (propietario): OBL-PRIN-03 (1).
- Areas del prompt que absorbe: 25 (Centro de evidencias).
- Decision respecto al maestro: se mantiene (sec. 30 Paquete de evidencias), redefinido como entidad propia mas vista de exportacion (decision 2.7.4, 2.7.24, inconsistencias 4, 11 y 26).
- MVP: MUST HAVE. El principio de responsabilidad demostrada (OBL-PRIN-03, Art. 5 lit. i) es transversal a toda la matriz; sin este modulo ningun otro puede demostrar cumplimiento ante la ACE.
- Dependencias: entra desde todos los modulos operativos (cada uno produce evidencia). Sale hacia MOD-019 (indicadores), MOD-023 (paquete para inspeccion de la ACE).

### MOD-019 Dashboard y Reportes
- Proposito: vista principal por perspectiva (Gerencia: vision general: Responsable: pendientes; Legal: riesgos y decisiones; Auditor: evidencias), mas reportes exportables (gerencial, ARCO-POL, incidentes, proveedores, RAT, auditoria, seguridad). Usa siempre lenguaje de "estado del programa" y "controles configurados", nunca "cumplimiento legal X%".
- Obligaciones que cubre (propietario): ninguna con OBL-ID propio; es una vista de agregacion sobre otros modulos.
- Areas del prompt que absorbe: 26 (Dashboard), 28 (Reportes).
- Decision respecto al maestro: se fusiona (sec. 31 Dashboard del maestro + area 28 del prompt, no desarrollada como modulo propio en el maestro).
- MVP: MUST HAVE el dashboard basico (pendientes, vencidos, tratamientos, solicitudes); SHOULD HAVE los reportes exportables avanzados por area [opinion de producto].
- Dependencias: entra desde todos los modulos (agregador). No entrega datos a otros modulos (es una vista terminal del recorrido).

### MOD-020 Centro de Tareas
- Proposito: modulo transversal que convierte cada obligacion en una accion concreta con titulo, fundamento, responsable, fecha, dependencia, evidencia requerida y estado (Pendiente, En proceso, Bloqueada, En revision, Aprobada, Completada, Vencida). Es alimentado por Diagnostico, ARCO-POL, Incidentes, Proveedores, Riesgos, Documentos y Auditoria.
- Obligaciones que cubre (propietario): ninguna con OBL-ID propio; es la capa de ejecucion compartida de las obligaciones que otros modulos poseen.
- Areas del prompt que absorbe: 14 (Centro de tareas).
- Decision respecto al maestro: se mantiene (sec. 16), confirmado como modulo transversal en vez de exclusivo de un flujo.
- MVP: MUST HAVE. Es el mecanismo operativo central del objetivo del producto (sec. 49 del maestro: "asigna tareas, controla plazos").
- Dependencias: entra desde todos los modulos que generan tareas. Sale hacia MOD-021 (dispara notificaciones), MOD-022 (consume el calendario de plazos), MOD-019 (indicadores).

### MOD-021 Notificaciones
- Proposito: modulo transversal que envia alertas por evento (tarea proxima a vencer, plazo de 72 horas, prevencion ARCO-POL sin resolver, documento por vencer) con destinatario, prioridad, frecuencia y escalamiento configurables, sin asumir de entrada todos los canales posibles (plataforma, email, Teams, Slack, SMS, WhatsApp).
- Obligaciones que cubre (propietario): ninguna con OBL-ID propio; instrumenta los plazos que otros modulos poseen.
- Areas del prompt que absorbe: 27 (Notificaciones).
- Decision respecto al maestro: es nuevo como modulo propio; el maestro lo trata como lista de canales dentro de la sec. 25 (Incidentes) sin modulo transversal dedicado.
- MVP: MUST HAVE con canales basicos (plataforma y email); canales adicionales (Teams, Slack, SMS, WhatsApp) quedan en V1/V2 segun demanda real de los primeros clientes [opinion de producto].
- Dependencias: entra desde MOD-020, MOD-022, MOD-010, MOD-012 (eventos que disparan alertas). No entrega datos a otros modulos.

### MOD-022 Calendario y Motor de Plazos
- Proposito: modulo transversal que centraliza el calculo de dias y horas habiles, asuetos nacionales configurables por anio, y expone un unico servicio de plazos consultado por ARCO-POL, Incidentes, Delegado y Procedimiento sancionador, en vez de que cada modulo implemente su propio calculo.
- Obligaciones que cubre (propietario): OBL-PLAZO-01, 02 (2).
- Areas del prompt que absorbe: 30 (Calendario central).
- Decision respecto al maestro: es nuevo como modulo propio y transversal; el maestro trataba el calculo de dias habiles como detalle disperso dentro de ARCO-POL (sec. 17) e Incidentes (sec. 25) (decision 2.7.15, inconsistencia 17, faltante 31).
- MVP: MUST HAVE. Sin un motor de plazos unico y confiable, ARCO-POL e Incidentes (ambos MUST HAVE) no pueden calcular correctamente sus plazos legales.
- Dependencias: entra desde el equipo del producto (mantiene el calendario de asuetos, fuente no unificada oficialmente, ver `02_validacion_de_la_idea.md` 2.3.1). Sale hacia MOD-010, MOD-012, MOD-001 (Delegado), MOD-023 (Procedimiento sancionador), MOD-020.

### MOD-023 Centro Regulatorio
- Proposito: modulo transversal que muestra el marco normativo aplicable clasificado como VIGENTE, FUTURO, DEROGADO o MODIFICADO, gestiona la bandera de activacion manual del doble estado de la reforma 659 (ver seccion 4), aloja el Procedimiento Sancionador (contestacion de emplazamiento, pago de multa, medidas adicionales, publicidad de resoluciones) y los Tramites ante la ACE (nombramiento del delegado, puesta en conocimiento de transferencias, solicitudes de credencial).
- Submodulos: Marco normativo consultable; Actualizaciones normativas (funcion transversal de este mismo modulo); Procedimiento Sancionador; Tramites ante la ACE.
- Obligaciones que cubre (propietario): OBL-AUD-02; OBL-SANC-01 a 09 (9); OBL-PLAZO-05 (11).
- Areas del prompt que absorbe: 31 (Centro regulatorio), 32 (Actualizaciones normativas, como funcion transversal de este modulo, no modulo aparte).
- Decision respecto al maestro: se fusiona y se amplia (secs. 40 "Motor regulatorio" y 41 "Actualizacion normativa" del maestro, alli tratadas como arquitectura tecnica, aqui convertidas en modulo funcional), mas dos piezas completamente nuevas que el maestro no contemplaba: Procedimiento Sancionador y Tramites ante la ACE (decisiones 2.7.16, 2.7.19, 2.7.25).
- MVP: MUST HAVE el nucleo (marco normativo + bandera de doble estado de la reforma 659, ver seccion 4); SHOULD HAVE el Procedimiento Sancionador completo, porque solo se activa si la empresa efectivamente enfrenta un procedimiento de la ACE, evento poco frecuente en los primeros clientes [opinion de producto].
- Dependencias: entra desde el equipo del producto (mantiene el contenido regulatorio y activa la bandera). Sale hacia MOD-001 (doble estado del Delegado), MOD-010, MOD-006, MOD-016, MOD-014 (obligaciones cuya clasificacion cambia con la reforma), MOD-020 (tareas del procedimiento sancionador).

### MOD-024 Busqueda Global
- Proposito: modulo transversal de busqueda sobre tratamientos, solicitudes ARCO-POL, proveedores, documentos, incidentes y tareas, para que un usuario no especialista encuentre informacion sin memorizar en que modulo vive.
- Obligaciones que cubre (propietario): ninguna con OBL-ID propio; es una capa de UX sobre datos de otros modulos.
- Areas del prompt que absorbe: 29 (Busqueda global).
- Decision respecto al maestro: es nuevo como modulo propio; el maestro no lo desarrolla.
- MVP: COULD HAVE. Mejora de usabilidad valiosa pero no bloquea ninguna obligacion legal; postergable sin riesgo de incumplimiento [opinion de producto].
- Dependencias: entra desde todos los modulos (indice de busqueda). No entrega datos a otros modulos.

### MOD-025 Centro de Ayuda
- Proposito: modulo transversal de ayuda contextual por modulo (que es, por que debo registrarlo, fundamento normativo, cuando necesito asesoria juridica externa), coherente con el principio de lenguaje claro y sin terminologia tecnica innecesaria (Art. 5 lit. e LPDP, ver `02_validacion_de_la_idea.md` 2.2).
- Obligaciones que cubre (propietario): ninguna con OBL-ID propio; instrumenta el principio de transparencia de forma transversal, sin ser el mismo una obligacion catalogable.
- Areas del prompt que absorbe: 34 (Centro de ayuda).
- Decision respecto al maestro: es nuevo como modulo propio; el maestro no lo desarrolla como modulo, solo lo menciona como enfoque de UX de tres niveles en la sec. 32.
- MVP: MUST HAVE (version basica: que es / por que / fundamento / cuando pedir ayuda juridica, por cada modulo MUST HAVE). Es la instrumentacion directa del principio central del producto: usable por alguien que no es especialista en privacidad. Wizards y niveles Intermedio/Especialista completos quedan en V1 (decision 2.3.4, sujeta a pruebas de usabilidad).
- Dependencias: entra desde el equipo del producto (contenido de ayuda por modulo). Sale hacia todos los modulos (widget contextual).

---

## 3. Modulos transversales y como se conectan

Los 6 modulos transversales (MOD-020 a MOD-025) no pertenecen a una etapa del recorrido: aparecen como una barra fija disponible desde cualquier pantalla, porque instrumentan capacidades que TODOS los modulos de recorrido necesitan.

```
                    +-------------------------------------------+
                    |         BARRA TRANSVERSAL (siempre visible)|
                    |  Tareas | Notif. | Calendario | Regulatorio |
                    |         | Busqueda | Ayuda                  |
                    +-------------------------------------------+
                                     ^  |
                     produce eventos |  | consulta / recibe alertas
                                     |  v
   EMPEZAR -> DIAGNOSTICAR -> PLANIFICAR -> REGISTRAR -> OPERAR -> DEMOSTRAR
   (MOD-001,002) (MOD-003)    (MOD-004)   (MOD-005..009)(MOD-010..016)(MOD-017..019)
```

Reglas de conexion:
1. **MOD-020 Centro de Tareas** es el unico lugar donde una obligacion se convierte en una accion con responsable y fecha; todo modulo de recorrido que genera trabajo (Diagnostico, ARCO-POL, Incidentes, Proveedores, Riesgos, Documentos, Auditoria, Procedimiento sancionador) crea tareas alli, en vez de mantener su propia lista de pendientes.
2. **MOD-021 Notificaciones** solo reacciona a eventos que le entregan MOD-020 y MOD-022; ningun modulo de recorrido envia notificaciones por su cuenta.
3. **MOD-022 Calendario y Motor de Plazos** es el unico que calcula dias/horas habiles; ARCO-POL, Incidentes, Delegado (MOD-001) y Procedimiento sancionador (MOD-023) le piden el calculo, nunca lo reimplementan.
4. **MOD-023 Centro Regulatorio** es el unico que decide que version de una regla esta activa (doble estado, ver seccion 4); ningun otro modulo evalua por si mismo si la reforma 659 esta vigente.
5. **MOD-024 Busqueda Global** y **MOD-025 Centro de Ayuda** son de solo lectura sobre el resto de modulos: no generan tareas ni escriben en otras entidades, solo indexan o explican.
6. **MOD-018 Centro de Evidencias**, aunque se ubica en la etapa Demostrar por ser su destino natural en el recorrido, funciona en la practica como semi-transversal: cada modulo operativo (MOD-006 a MOD-016) le entrega evidencia continuamente, no solo al final del recorrido.

---

## 4. Modelado del doble estado de la reforma 659 (sin duplicar modulos)

Principio de diseno: un solo modulo (MOD-001, submodulo Delegado / Responsable Interno) y una sola entidad conceptual ("Responsable del Programa de Datos") sirven tanto para el regimen ACTUAL como para el regimen FUTURO. Lo que cambia no es el modulo ni la entidad, sino dos atributos de esa entidad mas una bandera de activacion global que vive en MOD-023.

1. **Una sola entidad con un atributo de tipo de rol.** La persona designada se registra siempre en MOD-001 con un campo `tipo_rol` que toma el valor `DELEGADO` (regimen ACTUAL, Arts. 15 y 17 vigentes) o `RESPONSABLE_INTERNO` (regimen FUTURO, si la reforma se confirma). El formulario de alta, el historial, las tareas asociadas y la capacitacion (MOD-016) son los mismos campos y las mismas pantallas; solo cambia la etiqueta y el conjunto de obligaciones activas.
2. **Una bandera de activacion global en MOD-023, nunca automatica.** MOD-023 mantiene un interruptor `regimen_reforma_659` con dos valores: `ACTUAL` (por defecto, el vigente al 2026-09-24) y `FUTURO` (activable manualmente solo cuando el equipo del producto confirme la publicacion del decreto en el Diario Oficial y transcurran los 8 dias de vacatio legis). El sistema nunca activa `FUTURO` por la sola fecha de aprobacion legislativa (17-sep-2026); registra la fecha del cambio de bandera para trazabilidad, siguiendo el diseño recomendado en `03_hallazgos_regulatorios.md` seccion 3.
3. **Las 17 obligaciones afectadas cambian de estado, no de modulo.** Cuando la bandera pasa a `FUTURO`, las siguientes obligaciones (todas ya propietarias de MOD-001, MOD-010, MOD-006, MOD-016 o MOD-023 segun la tabla de la seccion 5) actualizan su clasificacion y su "a quien aplica" segun la nota de cada una en `matriz_obligaciones.md`: OBL-DPO-01 a 08 (8, en MOD-001), OBL-ARCO-01, 08, 10, 11, 14 (5, en MOD-010), OBL-CAP-02 (1, en MOD-016), OBL-CONS-03 (1, en MOD-006), OBL-RET-04 (1, en MOD-015) y OBL-PLAZO-05 (1, en MOD-023). Total 17, igual al conteo de `matriz_obligaciones.md`.
4. **Los actos atribuidos hoy al "delegado" (prevencion, incompetencia, notificacion a receptores, revocacion) se redactan igual en MOD-010, MOD-006 y MOD-001, sin importar el regimen; solo cambia quien debe aprobarlos** (la persona con `tipo_rol = DELEGADO` hoy, cualquier persona designada como `RESPONSABLE_INTERNO` despues), conforme a la decision 2.7.22.
5. **El aviso de privacidad (MOD-007) no se reescribe automaticamente al cambiar la bandera.** Dado que el Art. 24 lit. h exige datos de contacto del encargado/responsable del tramite, MOD-023 dispara una tarea en MOD-020 ("revisar avisos publicados tras el cambio de regimen") en vez de sobrescribir documentos ya publicados, siguiendo la ambiguedad documentada en `03_hallazgos_regulatorios.md` seccion 8, punto 4.

Con este diseño no existen dos modulos "Delegado (hoy)" y "Responsable interno (futuro)": existe un unico submodulo con un interruptor de regimen, coherente con el requisito explicito de la tarea de no duplicar modulos.

---

## 5. Tabla de cobertura: OBL-ID -> modulo propietario (105 obligaciones)

Cada obligacion tiene exactamente un modulo propietario; la columna "Colaboradores" lista otros modulos que consumen o alimentan esa obligacion por referencia, sin ser dueños de ella. IDs y agrupacion por area identicos a `matriz_obligaciones.md`.

### AMB (4) - propietario MOD-003 Diagnostico de Cumplimiento

| id | propietario | colaboradores |
|---|---|---|
| OBL-AMB-01 | MOD-003 | MOD-001 |
| OBL-AMB-02 | MOD-003 | - |
| OBL-AMB-03 | MOD-003 | - |
| OBL-AMB-04 | MOD-003 | - |

### PRIN (4)

| id | propietario | colaboradores |
|---|---|---|
| OBL-PRIN-01 | MOD-006 | MOD-005, MOD-004 |
| OBL-PRIN-02 | MOD-005 | MOD-006, MOD-004 |
| OBL-PRIN-03 | MOD-018 | MOD-014, MOD-017 |
| OBL-PRIN-04 | MOD-006 | MOD-010 |

### ARCO (15) - propietario MOD-010 ARCO-POL salvo nota

| id | propietario | colaboradores |
|---|---|---|
| OBL-ARCO-01 | MOD-010 | - |
| OBL-ARCO-02 | MOD-010 | - |
| OBL-ARCO-03 | MOD-010 | MOD-005 |
| OBL-ARCO-04 | MOD-010 | - |
| OBL-ARCO-05 | MOD-010 | MOD-009, MOD-008 |
| OBL-ARCO-06 | MOD-010 | - |
| OBL-ARCO-07 | MOD-010 | - |
| OBL-ARCO-08 | MOD-010 | MOD-022 |
| OBL-ARCO-09 | MOD-010 | MOD-022 |
| OBL-ARCO-10 | MOD-010 | MOD-022 |
| OBL-ARCO-11 | MOD-010 | MOD-009, MOD-008 |
| OBL-ARCO-12 | MOD-010 | - |
| OBL-ARCO-13 | MOD-010 | - |
| OBL-ARCO-14 | MOD-010 | MOD-023 |
| OBL-ARCO-15 | MOD-010 | MOD-011 |

### DPO (8) - propietario MOD-001 Organizacion y Personas (submodulo Delegado)

| id | propietario | colaboradores |
|---|---|---|
| OBL-DPO-01 | MOD-001 | MOD-023 |
| OBL-DPO-02 | MOD-001 | MOD-022 |
| OBL-DPO-03 | MOD-001 | MOD-022 |
| OBL-DPO-04 | MOD-001 | MOD-016 |
| OBL-DPO-05 | MOD-001 | MOD-016 |
| OBL-DPO-06 | MOD-001 | MOD-007 |
| OBL-DPO-07 | MOD-001 | MOD-017 |
| OBL-DPO-08 | MOD-001 | - |

### AVISO (5) - propietario MOD-007 Documentos y Politicas

| id | propietario | colaboradores |
|---|---|---|
| OBL-AVISO-01 | MOD-007 | - |
| OBL-AVISO-02 | MOD-007 | MOD-008 |
| OBL-AVISO-03 | MOD-007 | - |
| OBL-AVISO-04 | MOD-007 | MOD-008 |
| OBL-AVISO-05 | MOD-007 | - |

### CONS (6) - propietario MOD-006 Consentimiento

| id | propietario | colaboradores |
|---|---|---|
| OBL-CONS-01 | MOD-006 | - |
| OBL-CONS-02 | MOD-006 | - |
| OBL-CONS-03 | MOD-006 | MOD-008 |
| OBL-CONS-04 | MOD-006 | - |
| OBL-CONS-05 | MOD-006 | MOD-018 |
| OBL-CONS-06 | MOD-006 | MOD-010 |

### SENS (8)

| id | propietario | colaboradores |
|---|---|---|
| OBL-SENS-01 | MOD-005 | MOD-006 |
| OBL-SENS-02 | MOD-006 | - |
| OBL-SENS-03 | MOD-006 | MOD-005 |
| OBL-SENS-04 | MOD-005 | MOD-006, MOD-013 |
| OBL-SENS-05 | MOD-014 | MOD-005 |
| OBL-SENS-06 | MOD-005 | MOD-006, MOD-013 |
| OBL-SENS-07 | MOD-006 | - |
| OBL-SENS-08 | MOD-005 | MOD-007, MOD-013 |

### TRAT (3)

| id | propietario | colaboradores |
|---|---|---|
| OBL-TRAT-01 | MOD-005 | MOD-006 |
| OBL-TRAT-02 | MOD-006 | MOD-005 |
| OBL-TRAT-03 | MOD-005 | - |

### PROV (7) - propietario MOD-008 Proveedores y Encargados

| id | propietario | colaboradores |
|---|---|---|
| OBL-PROV-01 | MOD-008 | - |
| OBL-PROV-02 | MOD-008 | - |
| OBL-PROV-03 | MOD-008 | MOD-014 |
| OBL-PROV-04 | MOD-008 | MOD-007 |
| OBL-PROV-05 | MOD-008 | - |
| OBL-PROV-06 | MOD-008 | MOD-007 |
| OBL-PROV-07 | MOD-008 | MOD-015 |

### TRANSF (6) - propietario MOD-009 Transferencias Internacionales

| id | propietario | colaboradores |
|---|---|---|
| OBL-TRANSF-01 | MOD-009 | - |
| OBL-TRANSF-02 | MOD-009 | MOD-008 |
| OBL-TRANSF-03 | MOD-009 | - |
| OBL-TRANSF-04 | MOD-009 | MOD-006 |
| OBL-TRANSF-05 | MOD-009 | MOD-023 |
| OBL-TRANSF-06 | MOD-009 | MOD-018 |

### SEG (6) - propietario MOD-014 Controles de Seguridad

| id | propietario | colaboradores |
|---|---|---|
| OBL-SEG-01 | MOD-014 | MOD-023 |
| OBL-SEG-02 | MOD-014 | MOD-005, MOD-013, MOD-016, MOD-017 |
| OBL-SEG-03 | MOD-014 | - |
| OBL-SEG-04 | MOD-014 | MOD-009 |
| OBL-SEG-05 | MOD-014 | MOD-015 |
| OBL-SEG-06 | MOD-014 | MOD-023 |

### DOC (4)

| id | propietario | colaboradores |
|---|---|---|
| OBL-DOC-01 | MOD-007 | MOD-010 |
| OBL-DOC-02 | MOD-005 | - |
| OBL-DOC-03 | MOD-013 | - |
| OBL-DOC-04 | MOD-011 | MOD-010 |

### INC (5) - propietario MOD-012 Incidentes de Seguridad

| id | propietario | colaboradores |
|---|---|---|
| OBL-INC-01 | MOD-012 | MOD-020, MOD-022 |
| OBL-INC-02 | MOD-012 | MOD-022 |
| OBL-INC-03 | MOD-012 | - |
| OBL-INC-04 | MOD-012 | MOD-018 |
| OBL-INC-05 | MOD-012 | MOD-023 |

### CAP (2) - propietario MOD-016 Capacitacion

| id | propietario | colaboradores |
|---|---|---|
| OBL-CAP-01 | MOD-016 | - |
| OBL-CAP-02 | MOD-016 | MOD-001 |

### AUD (2)

| id | propietario | colaboradores |
|---|---|---|
| OBL-AUD-01 | MOD-017 | - |
| OBL-AUD-02 | MOD-023 | MOD-017 |

### SANC (9) - propietario MOD-023 Centro Regulatorio (submodulo Procedimiento Sancionador)

| id | propietario | colaboradores |
|---|---|---|
| OBL-SANC-01 | MOD-023 | - |
| OBL-SANC-02 | MOD-023 | - |
| OBL-SANC-03 | MOD-023 | MOD-020 |
| OBL-SANC-04 | MOD-023 | - |
| OBL-SANC-05 | MOD-023 | MOD-020, MOD-022 |
| OBL-SANC-06 | MOD-023 | MOD-020 |
| OBL-SANC-07 | MOD-023 | MOD-015, MOD-018 |
| OBL-SANC-08 | MOD-023 | - |
| OBL-SANC-09 | MOD-023 | MOD-010 |

### PLAZO (5)

| id | propietario | colaboradores |
|---|---|---|
| OBL-PLAZO-01 | MOD-022 | MOD-020 |
| OBL-PLAZO-02 | MOD-022 | - |
| OBL-PLAZO-03 | MOD-004 | MOD-003 |
| OBL-PLAZO-04 | MOD-011 | MOD-010 |
| OBL-PLAZO-05 | MOD-023 | MOD-001 |

### RET (6) - propietario MOD-015 Retencion y Eliminacion

| id | propietario | colaboradores |
|---|---|---|
| OBL-RET-01 | MOD-015 | MOD-007 |
| OBL-RET-02 | MOD-015 | MOD-007 |
| OBL-RET-03 | MOD-015 | MOD-007 |
| OBL-RET-04 | MOD-015 | MOD-007 |
| OBL-RET-05 | MOD-015 | MOD-018, MOD-010, MOD-012 |
| OBL-RET-06 | MOD-015 | MOD-007 |

**Verificacion de completitud:** 4 (AMB) + 4 (PRIN) + 15 (ARCO) + 8 (DPO) + 5 (AVISO) + 6 (CONS) + 8 (SENS) + 3 (TRAT) + 7 (PROV) + 6 (TRANSF) + 6 (SEG) + 4 (DOC) + 5 (INC) + 2 (CAP) + 2 (AUD) + 9 (SANC) + 5 (PLAZO) + 6 (RET) = 105. Coincide con el total de `matriz_obligaciones.md`.

---

## 6. Tabla de cobertura: 29 areas del prompt -> modulo

| Area del prompt | Modulo | Tipo de asignacion |
|---|---|---|
| 8.1 Configuracion de empresa | MOD-001 | Propia |
| 8.2 Usuarios, roles y permisos | MOD-001 | Propia (submodulo) |
| 8.3 Onboarding | MOD-002 | Propia |
| 9 Diagnostico | MOD-003 | Propia |
| 10 Plan de cumplimiento | MOD-004 | Propia |
| 11 RAT | MOD-005 | Propia |
| 12 Mapa de datos | MOD-005 | Funcion transversal del modulo (vista sobre el RAT) |
| 13 ARCO-POL | MOD-010 | Propia |
| 14 Centro de tareas | MOD-020 | Propia (transversal) |
| 15 Documentos y politicas | MOD-007 | Propia |
| 16 Consentimiento | MOD-006 | Propia |
| 17 Proveedores | MOD-008 | Propia |
| 18 Transferencias internacionales | MOD-009 | Propia |
| 19 Incidentes | MOD-012 | Propia |
| 20 EIPD/Riesgos | MOD-013 | Propia |
| 21 Controles de seguridad | MOD-014 | Propia |
| 22 Retencion | MOD-015 | Propia |
| 23 Capacitacion | MOD-016 | Propia |
| 24 Auditoria | MOD-017 | Propia (programa sustantivo); el registro tecnico (AuditLog) es funcion transversal embebida en todos los modulos, consultable desde MOD-017 y MOD-018 |
| 25 Centro de evidencias | MOD-018 | Propia (transversal) |
| 26 Dashboard | MOD-019 | Propia |
| 27 Notificaciones | MOD-021 | Propia (transversal) |
| 28 Reportes | MOD-019 | Propia (submodulo de Dashboard y Reportes) |
| 29 Busqueda global | MOD-024 | Propia (transversal) |
| 30 Calendario central | MOD-022 | Propia (transversal) |
| 31 Centro regulatorio | MOD-023 | Propia (transversal) |
| 32 Actualizaciones normativas | MOD-023 | Funcion transversal del modulo (no modulo aparte) |
| 33 Portal del titular | MOD-011 | Propia |
| 34 Centro de ayuda | MOD-025 | Propia (transversal) |

Las 29 areas quedan asignadas: 27 como modulo propio y 2 (Mapa de datos, Actualizaciones normativas) declaradas explicitamente como funcion transversal de un modulo ya asignado, tal como exige la tarea.

---

## 7. Entidades conceptuales principales que el mapa implica

Lista de entidades de dominio (sin modelo de datos, sin SQL), agrupadas por dominio funcional, con el modulo que las posee.

**Organizacion y personas**
- Organization (empresa cliente) - MOD-001
- BusinessUnit/Sucursal - MOD-001
- User - MOD-001
- Role (estandar, personalizado) - MOD-001
- ResponsableDelProgramaDeDatos (Delegado o Responsable Interno, con `tipo_rol`) - MOD-001

**Diagnostico y plan**
- DiagnosticoRespuesta - MOD-003
- AccionDelPlan (con responsable, fecha, fundamento, evidencia, estado) - MOD-004

**Tratamiento de datos**
- Treatment (actividad de tratamiento, RAT) - MOD-005
- Purpose (finalidad) - MOD-005
- LegalBasis (una de las seis bases del Art. 5 lit. g) - MOD-005
- DataCategory / DataSubjectCategory - MOD-005
- System (catalogo de sistemas) - MOD-005

**Consentimiento**
- Consent (registro de consentimiento) - MOD-006
- ConsentWithdrawal (revocacion) - MOD-006

**Documentos**
- Document (contenido versionado) - MOD-007
- DocumentVersion - MOD-007
- PrivacyNotice (Aviso de Privacidad) - MOD-007
- PrivacyPolicy (Politica de Privacidad/Proteccion de Datos) - MOD-007

**Proveedores y transferencias**
- Encargado - MOD-008
- TerceroReceptor - MOD-008
- Subencargado - MOD-008
- Contract/DPA (tipo de Document) - MOD-008
- Transfer (flujo transfronterizo) - MOD-009

**Derechos del titular**
- PrivacyRequest (expediente ARCO-POL) - MOD-010
- IdentityVerification - MOD-010
- Titular (persona que ejerce el derecho, no necesariamente usuario del sistema) - MOD-010/MOD-011

**Riesgo y seguridad**
- Incident - MOD-012
- DPIA (EIPD) - MOD-013
- Risk / RiskAssessment - MOD-013
- Control (catalogo unico compartido) - MOD-014
- RetentionRule - MOD-015

**Capacitacion**
- TrainingProgram - MOD-016
- TrainingRecord - MOD-016

**Demostracion**
- ComplianceAudit (auditoria anual sustantiva) - MOD-017
- Evidence (artefacto/referencia inmutable) - MOD-018
- AuditLog (registro tecnico de acciones, entidad transversal, consultada desde MOD-017/MOD-018)
- EvidencePackage (vista de exportacion, sin almacenamiento propio) - MOD-018

**Transversales**
- Task - MOD-020
- Approval - MOD-020 (asociado a Task o Document segun el flujo)
- Notification - MOD-021
- CalendarEvent / HolidayCalendar (calendario de asuetos) - MOD-022
- RegulatoryInstrument (norma, con estado VIGENTE/FUTURO/DEROGADO/MODIFICADO) - MOD-023
- RegulatoryRuleVersion (regla versionada con fecha de vigencia) - MOD-023
- ReformaActivationFlag (bandera de doble estado, ver seccion 4) - MOD-023
- SanctionProcedure (expediente del procedimiento sancionador) - MOD-023
- ACEFiling (tramite saliente hacia la ACE) - MOD-023
- HelpArticle - MOD-025

---

## 8. Riesgos del mapa propuesto

1. **Sobrecarga de navegacion por numero de modulos.** 25 modulos de primer nivel, aunque agrupados en 6 etapas, pueden abrumar a un usuario no especialista si la UI los expone como lista plana. Mitigacion: la agrupacion en 6 etapas colapsables mas una barra transversal fija (seccion 1 y 3) debe ser un requisito de UX vinculante, no solo una sugerencia de este documento [opinion de producto].
2. **Activacion indebida del doble estado de la reforma 659.** Si la bandera de MOD-023 se activa por error o antes de confirmar la publicacion oficial, 17 obligaciones (seccion 4) cambiarian de exigibilidad de forma incorrecta para todos los clientes simultaneamente. Mitigacion: el cambio de bandera debe requerir una accion administrativa explicita y auditable, nunca un job automatico por fecha.
3. **El Centro Regulatorio mezcla contenido informativo con flujo operativo.** MOD-023 aloja a la vez informacion de referencia (marco normativo) y un procedimiento con plazos reales y consecuencias economicas (Procedimiento Sancionador). Si la UI no los separa claramente, un usuario podria confundir "estoy leyendo sobre sanciones" con "tengo un procedimiento sancionador abierto".
4. **Volumen de AuditLog como entidad transversal.** Al registrarse desde todos los modulos, el registro tecnico de auditoria puede crecer rapido; esta fase de analisis funcional no resuelve su arquitectura de almacenamiento, pero el mapa de modulos ya asume que MOD-017/MOD-018 deben poder consultarlo y exportarlo con integridad verificable, lo que debe validarse en la fase de arquitectura tecnica.
5. **Clasificacion MVP con muchos MUST HAVE (15 de 25) puede exceder un "producto minimo vendible".** La urgencia real (obligaciones OBLIGATORIO con plazo ya vencido) justifica una lista amplia, pero esta clasificacion es de producto, no legal; debe validarse contra capacidad real de desarrollo y contra el estudio de disposicion a pagar que `02_validacion_de_la_idea.md` 2.3.4 deja pendiente [opinion de producto].
6. **Dejar Transferencias (MOD-009) y Riesgos/EIPD (MOD-013) en SHOULD HAVE puede exponer a empresas con datos sensibles desde el dia uno.** Si una empresa cliente usa biometria o hace videovigilancia desde su primer diagnostico, el modulo completo de EIPD aun no estaria disponible en el MVP. Mitigacion: el diagnostico (MOD-003, MUST HAVE) debe poder generar una tarea manual de "EIPD pendiente" en el Centro de Tareas incluso si el modulo EIPD completo no esta activo todavia.
7. **RAT como nucleo unico concentra demasiados campos si no se separan bien las vistas.** Fusionar Inventario, RAT y Catalogo de sistemas en un solo modulo (decision 2.7.1) reduce duplicacion, pero si las tres vistas (RAT, Mapa de datos, Catalogo de sistemas) no se disenan como pantallas claramente distintas, el modulo puede volverse un formulario unico sobrecargado, contrario al principio de minima carga cognitiva del angulo asignado.
8. **Incertidumbres juridicas heredadas por multiples modulos.** Las incertidumbres documentadas en `03_hallazgos_regulatorios.md` seccion 9 (computo de 72 horas, aplicabilidad del Art. 82 LPA al sector privado, transferencia vs. encargado extranjero, edad de consentimiento de NNA, numero exacto del Decreto 659) atraviesan varios modulos (MOD-012, MOD-022, MOD-009, MOD-006, MOD-023). Si cada modulo resuelve la ambiguedad de forma distinta, el producto perderia coherencia interna. Mitigacion: el criterio conservador por defecto y su etiqueta de incertidumbre visible deben definirse una sola vez (en MOD-022 y MOD-023 segun corresponda) y heredarse, nunca reimplementarse por modulo.

---

## Nota final

Este mapa es una propuesta de diseno funcional [opinion de producto en su estructura y clasificacion MVP], construida sobre las 105 obligaciones verificadas de `matriz_obligaciones.md` y las 32 decisiones de alcance ya tomadas en `02_validacion_de_la_idea.md`. Ninguna asignacion de modulo reinterpreta un articulo de la ley; donde una obligacion depende de una incertidumbre juridica genuina (seccion 9 de `03_hallazgos_regulatorios.md`), el modulo propietario hereda esa incertidumbre y debe mostrarla, no resolverla. La ficha completa de cada modulo (formato A-Q de `00_plantilla_ficha_modulo.md`) es un entregable posterior, fuera del alcance de este mapa.
