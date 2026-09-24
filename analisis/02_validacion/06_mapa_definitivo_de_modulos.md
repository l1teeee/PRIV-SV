# Mapa definitivo de modulos - PRIV-SV

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (prohibido proponer codigo, SQL, APIs, stack o infraestructura). Este documento es el MAPA DEFINITIVO DE MODULOS de la fase de validacion: parte de la propuesta ganadora (`propuesta_mapa_recorrido.md`, angulo RECORRIDO-DEL-USUARIO-PRIMERO) e injerta las ideas recomendadas por los tres jueces sobre las otras dos propuestas (`propuesta_mapa_obligaciones.md`, `propuesta_mapa_mvp.md`). Sustituye a las tres propuestas para todo efecto posterior.

Fuentes: `01_legal/matriz_obligaciones.md` y `matriz_obligaciones.json` (105 obligaciones, IDs canonicos OBL-AREA-NN), `01_legal/03_hallazgos_regulatorios.md` (secciones 3, 5, 6, 8, 9, 11), `02_validacion/02_validacion_de_la_idea.md`, las tres propuestas de `02_validacion/propuesta_mapa_*.md`, y los veredictos de los tres jueces que evaluaron esas propuestas (resumidos en la seccion 12).

Convencion: toda fila que cita un OBL-ID es una afirmacion verificada contra la matriz (105/105 confirmados por script contra `matriz_obligaciones.json`, ver seccion 8). Toda clasificacion MVP, fusion, division o injerto de idea de un juez es una decision de diseno de producto y se marca como tal; se cita explicitamente de que documento o de que juez proviene cada injerto.

---

## 0. Resumen de modulos

26 modulos de primer nivel: 20 modulos de recorrido (organizados en 6 etapas) y 6 modulos transversales visibles desde cualquier etapa. Uno mas que la propuesta ganadora original (25), por la elevacion de MOD-002 Delegado a modulo propio (ver seccion 12).

| Codigo | Nombre | Etapa | Transversal | MVP |
|---|---|---|---|---|
| MOD-001 | Organizacion y Personas | Empezar | No | MUST HAVE |
| MOD-002 | Delegado / Responsable Interno de Datos | Empezar | No | MUST HAVE |
| MOD-003 | Onboarding | Empezar | No | MUST HAVE |
| MOD-004 | Diagnostico de Cumplimiento | Diagnosticar | No | MUST HAVE |
| MOD-005 | Plan de Cumplimiento | Planificar | No | MUST HAVE |
| MOD-006 | RAT y Mapa de Datos | Registrar | No | MUST HAVE |
| MOD-007 | Consentimiento | Registrar | No | MUST HAVE |
| MOD-008 | Documentos y Politicas | Registrar | No | MUST HAVE |
| MOD-009 | Proveedores y Encargados | Registrar | No | MUST HAVE |
| MOD-010 | Transferencias Internacionales | Registrar | No | SHOULD HAVE |
| MOD-011 | ARCO-POL | Operar | No | MUST HAVE |
| MOD-012 | Portal del Titular | Operar | No | SHOULD HAVE |
| MOD-013 | Incidentes de Seguridad | Operar | No | MUST HAVE |
| MOD-014 | Riesgos y EIPD | Operar | No | SHOULD HAVE |
| MOD-015 | Controles de Seguridad | Operar | No | MUST HAVE |
| MOD-016 | Retencion y Eliminacion | Operar | No | SHOULD HAVE |
| MOD-017 | Capacitacion | Operar | No | MUST HAVE |
| MOD-018 | Auditoria de Cumplimiento | Demostrar | No | SHOULD HAVE |
| MOD-019 | Centro de Evidencias | Demostrar | No | MUST HAVE |
| MOD-020 | Dashboard y Reportes | Demostrar | No | MUST HAVE |
| MOD-021 | Centro de Tareas | Transversal | Si | MUST HAVE |
| MOD-022 | Notificaciones | Transversal | Si | MUST HAVE |
| MOD-023 | Calendario y Motor de Plazos | Transversal | Si | MUST HAVE |
| MOD-024 | Centro Regulatorio | Transversal | Si | MUST HAVE |
| MOD-025 | Busqueda Global | Transversal | Si | COULD HAVE |
| MOD-026 | Centro de Ayuda | Transversal | Si | MUST HAVE |

---

## 1. Arbol ASCII definitivo

```
PLATAFORMA DE AUTOGESTION DE PROTECCION DE DATOS (El Salvador)
|
|== ETAPA 1: EMPEZAR ==========================================
|    |-- MOD-001 Organizacion y Personas
|    |    |-- Empresa (razon social, sucursales, areas, sector, exclusiones Art. 3)
|    |    v-- Usuarios y Roles (RBAC, roles estandar/personalizados, separacion de funciones)
|    |-- MOD-002 Delegado / Responsable Interno de Datos  [elevado, ver seccion 12]
|    |    |-- Nombramiento y ciclo de vida (comunicacion ACE, reverificacion, informes)
|    |    v-- Doble estado de la reforma 659 (ver seccion 5)
|    v-- MOD-003 Onboarding (alta guiada de organizacion + usuarios + roles + delegado)
|
|== ETAPA 2: DIAGNOSTICAR =====================================
|    v-- MOD-004 Diagnostico de Cumplimiento
|         |-- Cuestionario guiado (empleados, camaras, CV, CRM, app movil, biometria,
|         |   salud, cloud, datos fuera del pais, marketing, menores...)
|         |-- Deteccion de exclusiones (Art. 3)
|         v-- Motor de disparo: respuesta -> tratamiento + tarea + documento + riesgo
|
|== ETAPA 3: PLANIFICAR =======================================
|    v-- MOD-005 Plan de Cumplimiento (acciones priorizadas: criticas/importantes/recomendadas)
|
|== ETAPA 4: REGISTRAR ========================================
|    |-- MOD-006 RAT y Mapa de Datos
|    |    |-- Registro de Actividades de Tratamiento (RAT), fuente unica de verdad
|    |    |-- Mapa de datos (vista: origen -> sistema -> area -> proveedor -> pais -> eliminacion)
|    |    v-- Catalogo de sistemas (alta/edicion unica, consultado por referencia)
|    |-- MOD-007 Consentimiento
|    |    |-- Registro de consentimiento (referencia a version del Aviso, nunca copia)
|    |    |-- Revocacion (mini flujo de dos plazos: 5 + 5 dias habiles)
|    |    v-- Sub-flujo titular menor de edad (consentimiento parental)
|    |-- MOD-008 Documentos y Politicas
|    |    |-- Politica de Proteccion de Datos / Politica de Privacidad
|    |    |-- Aviso de Privacidad (versionado, 9 literales del Art. 24)
|    |    v-- Plantillas, borradores, aprobacion configurable por tipo de documento
|    |-- MOD-009 Proveedores y Encargados
|    |    |-- Encargados
|    |    |-- Terceros / Receptores
|    |    |-- Subencargados
|    |    v-- Contratos / DPA (tipo de documento, enlazado a Documentos)
|    v-- MOD-010 Transferencias Internacionales (enlaza por referencia a Proveedores)
|
|== ETAPA 5: OPERAR (subdividida en 3 grupos tematicos, ver seccion 2) ========
|    |-- [Relacion con el titular]
|    |    |-- MOD-011 ARCO-POL (formulario interno seguro en MVP)
|    |    |    |-- Verificacion de identidad del titular (titular/representante/heredero)
|    |    |    |-- Rama: Incompetencia (devolucion, 5 dias habiles)
|    |    |    |-- Rama: Notificacion a receptores (5 dias habiles)
|    |    |    v-- Rama: Reclamo ante la Direccion de Proteccion de Datos (ACE)
|    |    v-- MOD-012 Portal del Titular (V1/Enterprise: autoregistro publico)
|    |-- [Riesgo y seguridad]
|    |    |-- MOD-013 Incidentes de Seguridad (dos hitos de 72 horas: notificacion e inicio de revision)
|    |    |-- MOD-014 Riesgos y EIPD (usa el catalogo de Controles de MOD-015, no uno propio)
|    |    v-- MOD-015 Controles de Seguridad (catalogo unico de controles con evidencia)
|    v-- [Ciclo de vida y personas]
|         |-- MOD-016 Retencion y Eliminacion
|         |    |-- Motor de retencion de datos del titular (por finalidad)
|         |    v-- Motor de retencion documental de cumplimiento propio (avisos 10 anios, expedientes 5 anios)
|         v-- MOD-017 Capacitacion
|              |-- Capacitacion general del personal (registro minimo, MVP)
|              v-- Capacitacion especifica del Delegado / Responsable Interno (MOD-002)
|
|== ETAPA 6: DEMOSTRAR ========================================
|    |-- MOD-018 Auditoria de Cumplimiento (programa anual sustantivo, distinto del log tecnico)
|    |-- MOD-019 Centro de Evidencias (Documento + Evidencia + AuditLog, vista de exportacion con hash)
|    v-- MOD-020 Dashboard y Reportes (por perspectiva: Gerencia/Responsable/Legal-Delegado/Auditor)
|
v== MODULOS TRANSVERSALES (visibles desde cualquier etapa, ver seccion 4) =====
     |-- MOD-021 Centro de Tareas
     |-- MOD-022 Notificaciones
     |-- MOD-023 Calendario y Motor de Plazos (dias/horas habiles, asuetos)
     |-- MOD-024 Centro Regulatorio
     |    |-- Marco normativo consultable (VIGENTE / FUTURO / DEROGADO / MODIFICADO)
     |    |-- Actualizaciones normativas (funcion transversal, no modulo aparte)
     |    |-- Procedimiento Sancionador (contestacion, pago de multa, medidas adicionales)
     |    v-- Tramites ante la ACE (nombramiento delegado, transferencias, credenciales)
     |-- MOD-025 Busqueda Global
     v-- MOD-026 Centro de Ayuda (contextual por modulo: que es, por que, fundamento)
```

Nota de navegacion [opinion de producto, heredada de la propuesta ganadora]: para no sobrecargar a un usuario no especialista, la UI debe agrupar por las 6 etapas (6 grupos colapsables, con OPERAR subdividido en 3 sub-grupos tematicos) mas una barra fija de 6 modulos transversales, nunca una lista plana de 26 items.

---

## 2. Principios de organizacion (por que asi)

1. **El recorrido del usuario ordena las etapas, no la taxonomia juridica.** Los modulos se agrupan en 6 etapas (EMPEZAR, DIAGNOSTICAR, PLANIFICAR, REGISTRAR, OPERAR, DEMOSTRAR) que coinciden con el orden real en que una persona sin abogado ni DPO dedicado usaria el software, en vez de por dominio legal (contra lo cual competia la propuesta obligacion-primero). Es el criterio que gano la validacion de los tres jueces (ver seccion 12).
2. **Cada obligacion tiene exactamente un modulo propietario.** Las 105 obligaciones de `matriz_obligaciones.json` estan asignadas una sola vez como propietarias (verificado por script, seccion 8); otros modulos pueden ser colaboradores (consumen o alimentan la obligacion por referencia) pero nunca dueños compartidos.
3. **El hallazgo estructural mas importante de la validacion se hace visible como modulo propio.** El Delegado / Responsable Interno de Datos (MOD-002) deja de ser un submodulo de tercer nivel dentro de Organizacion (como en la propuesta ganadora original) y pasa a ser un modulo de primer nivel, por injerto explicito de dos de los tres jueces (ver seccion 12, idea comun a los jueces 1 y 2).
4. **El doble estado de la reforma 659 se modela con una sola entidad y una sola bandera, nunca con dos modulos paralelos.** Ver seccion 5. Esto se mantiene sin cambios respecto de la propuesta ganadora: ningun injerto de los jueces propuso duplicar modulos por el cambio normativo, todos refuerzan el modelo de bandera unica.
5. **Los modulos transversales nunca son propietarios de una obligacion de negocio, salvo que la obligacion describa literalmente al motor transversal mismo.** MOD-023 Calendario (OBL-PLAZO-01/02) es la unica excepcion real; MOD-021, MOD-022, MOD-025 y MOD-026 no poseen ninguna obligacion propia. MOD-024 Centro Regulatorio es un caso especial: es transversal en el sentido de que ningun modulo de proceso mantiene su propia copia del estado normativo, pero a la vez es propietario de 11 obligaciones reales (Procedimiento Sancionador + Auditoria de la reforma), por lo que se ubica en la barra transversal pero se declara explicitamente no binario (injerto del juez 3, ver seccion 12).
6. **Direccion unica: todo modulo de proceso escribe hacia los transversales, nunca al reves; y las referencias entre modulos de proceso son lectura, no escritura duplicada.** Regla ya presente en la propuesta ganadora (seccion 3 original) y reforzada aqui con la formulacion explicita de la propuesta obligacion-primero, injertada por el juez 3: un modulo de proceso (por ejemplo MOD-006 RAT) puede ser leido por referencia por otro (MOD-009 Proveedores, MOD-016 Retencion) sin que eso implique que ese otro modulo pueda escribir o duplicar el dato original.
7. **El MVP se decide con un test explicito de tres condiciones, no por intuicion.** Injertado de `propuesta_mapa_mvp.md` (recomendado por los jueces 1 y 2): un modulo entra al MVP si (a) cubre una obligacion OBLIGATORIO cuyo plazo transitorio ya vencio (OBL-PLAZO-03, OBL-PLAZO-04), (b) es una dependencia estructural sin la cual otro modulo MUST HAVE no puede operar, o (c) es la unica forma de que el producto sea probatorio desde el primer dia (Centro de Evidencias, AuditLog). Todo modulo SHOULD HAVE o COULD HAVE de este mapa declara ademas su mecanismo de cobertura parcial (ver fichas de la seccion 3 y seccion 12).
8. **Ningun cambio de estado normativo borra informacion; todo queda versionado con su historial.** Aplica tanto a documentos (MOD-008, MOD-024) como a tareas dependientes del Delegado (MOD-002, MOD-021): se marcan como "no aplica bajo el estado regulatorio actual, ver historial" en vez de eliminarse. Principio injertado de `propuesta_mapa_mvp.md` (ver seccion 5).

---

## 3. Ficha resumida de cada modulo

Cada ficha indica: proposito, submodulos (si existen), obligaciones que cubre como propietario, areas del prompt que absorbe, decision respecto al documento maestro y a la propuesta ganadora, clasificacion MVP con justificacion (y mecanismo de cobertura parcial si es SHOULD/COULD HAVE), y dependencias.

### MOD-001 Organizacion y Personas (Empezar)
- Proposito: Registra la identidad legal de la empresa cliente, su estructura interna (sucursales, unidades, departamentos) y administra el modelo de roles y permisos (RBAC) que usan todos los demas modulos. Es el punto de partida obligatorio antes de usar cualquier otro modulo. No incluye al Delegado / Responsable Interno de Datos, elevado a modulo propio (MOD-002).
- Submodulos: Empresa (razon social, sucursales, areas, sector, exclusiones Art. 3); Usuarios y Roles (RBAC, roles estandar/personalizados, separacion de funciones).
- Obligaciones que cubre (propietario): ninguna con OBL-ID propio.
- Areas del prompt que absorbe: 8.1, 8.2.
- Decision respecto al documento maestro y a la propuesta ganadora: Se fusiona (sec. 11 Modulo de organizacion + sec. 12 Usuarios y roles del maestro). Se retira el submodulo Delegado que traia en la propuesta ganadora original (propuesta_mapa_recorrido.md), elevado ahora a MOD-002 por injerto de los jueces 1 y 2 (ver seccion 12).
- MVP: MUST HAVE. Justificacion: Sin organizacion, usuarios y roles no puede operar ningun otro modulo; es el registro fundacional de toda cuenta.
- Dependencias: entra desde MOD-003. Sale hacia MOD-002, MOD-003, MOD-004, MOD-005, MOD-006, MOD-007, MOD-008, MOD-009, MOD-010, MOD-011, MOD-012, MOD-013, MOD-014, MOD-015, MOD-016, MOD-017, MOD-018, MOD-019, MOD-020, MOD-021, MOD-022, MOD-023, MOD-024, MOD-025, MOD-026.
- Notas reforma 659: No posee obligaciones afectadas directamente; conserva la identidad de organizacion y usuarios sin cambios entre regimenes.

### MOD-002 Delegado / Responsable Interno de Datos (Empezar)
- Proposito: Gestiona el ciclo de vida completo de la figura que hoy la ley llama Delegado de Proteccion de Datos (Arts. 15 y 17 vigentes) y que la reforma 659 renombraria a responsable interno / sujeto obligado: nombramiento, comunicacion a la ACE, reverificacion periodica, informes, capacitacion especifica y confidencialidad post-cese. Modela el doble estado de la reforma 659 con una sola entidad y un atributo de tipo de rol. Se eleva de submodulo de Organizacion a modulo propio de primer nivel: concentra 8 obligaciones OBLIGATORIO vigentes hoy y es, segun 02_validacion_de_la_idea.md (decision 2.7.7), el hallazgo estructural mas importante de toda la validacion; enterrarlo como bullet reducia su visibilidad para el usuario no especialista.
- Submodulos: Nombramiento y ciclo de vida (comunicacion a la ACE, reverificacion, informes); Doble estado de la reforma 659 (tipo_rol: DELEGADO | RESPONSABLE_INTERNO).
- Obligaciones que cubre (propietario): OBL-DPO-01, OBL-DPO-02, OBL-DPO-03, OBL-DPO-04, OBL-DPO-05, OBL-DPO-06, OBL-DPO-07, OBL-DPO-08 (8).
- Areas del prompt que absorbe: ninguna area especifica de las 29 (es un hallazgo estructural de la validacion, ver seccion 12).
- Decision respecto al documento maestro y a la propuesta ganadora: NUEVO como modulo de primer nivel. En el maestro no existia como rol ni modulo (hallazgo estructural principal de 02_validacion_de_la_idea.md, decision 2.7.7). En la propuesta ganadora (recorrido) vivia como submodulo de tercer nivel dentro de MOD-001; se eleva a modulo propio por injerto explicito de dos de los tres jueces (idea 4 del juez 1 y del juez 2), que senalan que enterrarlo como bullet reduce su visibilidad para el usuario no especialista pese a ser, en palabras de 02_validacion_de_la_idea.md, "el hallazgo estructural mas importante de toda la validacion".
- MVP: MUST HAVE. Justificacion: El Delegado es OBLIGATORIO hoy (Arts. 15 y 17 vigentes) con plazos ya en curso (comunicacion a la ACE en 15 dias habiles, OBL-DPO-03); concentra 8 obligaciones OBLIGATORIO completas.
- Dependencias: entra desde MOD-001, MOD-024. Sale hacia MOD-007, MOD-008, MOD-011, MOD-017, MOD-018, MOD-021, MOD-023, MOD-024.
- Notas reforma 659: Modulo directamente regido por el doble estado: aloja las 8 obligaciones DPO (OBL-DPO-01 a 08), afectadas en su totalidad por la reforma 659. Ver seccion 5 del documento principal.

### MOD-003 Onboarding (Empezar)
- Proposito: Guia a la persona designada, sin conocimiento juridico previo, a traves de la alta inicial de organizacion, usuarios y roles en la primera sesion. Entrega como salida una organizacion configurada, lista para el Diagnostico. No posee obligaciones legales propias: ejecuta el alta de MOD-001.
- Obligaciones que cubre (propietario): ninguna con OBL-ID propio.
- Areas del prompt que absorbe: 8.3.
- Decision respecto al documento maestro y a la propuesta ganadora: Se divide de la sec. 15 del maestro ("Onboarding / Compliance Wizard"), separando el alta de organizacion (este modulo) del cuestionario de obligaciones (MOD-004), decision 2.7.5 de 02_validacion_de_la_idea.md.
- MVP: MUST HAVE. Justificacion: Es la puerta de entrada del producto; sin el, MOD-001 y MOD-002 se llenarian sin guia.
- Dependencias: entra desde ninguno (punto de entrada o configuracion mantenida por el equipo del producto). Sale hacia MOD-001, MOD-002, MOD-004.
- Notas reforma 659: No aplica directamente.

### MOD-004 Diagnostico de Cumplimiento (Diagnosticar)
- Proposito: Cuestionario guiado y repetible que traduce preguntas sencillas (empleados, camaras, CV, CRM, app movil, biometria, salud, cloud, datos fuera del pais, marketing, menores) en tratamientos, tareas, documentos y riesgos sugeridos. Detecta las exclusiones del Art. 3 antes de sobre-obligar a la empresa.
- Submodulos: Cuestionario guiado; Deteccion de exclusiones (Art. 3); Motor de disparo: respuesta -> tratamiento + tarea + documento + riesgo.
- Obligaciones que cubre (propietario): OBL-AMB-01, OBL-AMB-02, OBL-AMB-03, OBL-AMB-04 (4).
- Areas del prompt que absorbe: 9.
- Decision respecto al documento maestro y a la propuesta ganadora: Se divide de la sec. 15 del maestro (ver MOD-003), decisiones 2.7.5 y 2.7.27.
- MVP: MUST HAVE. Justificacion: Es el mecanismo concreto para identificar exposicion legal, urgente porque el plazo de adecuacion a las Politicas ACE ya vencio (OBL-PLAZO-03, 2/3-dic-2025).
- Dependencias: entra desde MOD-003. Sale hacia MOD-005, MOD-006, MOD-008, MOD-014, MOD-021.
- Notas reforma 659: No aplica directamente.

### MOD-005 Plan de Cumplimiento (Planificar)
- Proposito: Convierte el resultado del diagnostico en una lista priorizada de acciones (criticas, importantes, recomendadas), cada una con responsable, fecha, fundamento normativo, evidencia esperada y estado.
- Obligaciones que cubre (propietario): OBL-PLAZO-03 (1).
- Areas del prompt que absorbe: 10.
- Decision respecto al documento maestro y a la propuesta ganadora: Nuevo como modulo propio; el maestro solo lo menciona implicitamente en su objetivo final (sec. 49), sin desarrollarlo, aunque el area 10 del prompt de analisis funcional si lo exige.
- MVP: MUST HAVE. Justificacion: Es la propuesta de valor central del producto (obligaciones -> procesos + tareas + plazos) y el mecanismo que justifica comercialmente la urgencia de los plazos vencidos (decision 2.7.29).
- Dependencias: entra desde MOD-004. Sale hacia MOD-021, MOD-020.
- Notas reforma 659: No aplica directamente.

### MOD-006 RAT y Mapa de Datos (Registrar)
- Proposito: Registro de actividades de tratamiento como fuente unica de verdad de que datos trata la empresa, con que finalidad, base juridica, categorias y sistemas. El Mapa de datos es una vista sobre esta misma informacion. Incluye el catalogo de sistemas.
- Submodulos: Registro de Actividades de Tratamiento (RAT), fuente unica de verdad; Mapa de datos (vista: origen -> sistema -> area -> proveedor -> pais -> eliminacion); Catalogo de sistemas.
- Obligaciones que cubre (propietario): OBL-DOC-02, OBL-PRIN-02, OBL-SENS-01, OBL-SENS-04, OBL-SENS-06, OBL-SENS-08, OBL-TRAT-01, OBL-TRAT-03 (8).
- Areas del prompt que absorbe: 11, 12.
- Decision respecto al documento maestro y a la propuesta ganadora: Se fusiona (sec. 13 Inventario de datos + sec. 14 RAT/ROPA del maestro); el Mapa de datos deja de ser modulo separado (decision 2.7.1, inconsistencia 1).
- MVP: MUST HAVE. Justificacion: Es el nucleo operativo identificado en 02_validacion_de_la_idea.md 2.1, con respaldo normativo directo (OBL-DOC-02, medida organizativa obligatoria de las Politicas ACE).
- Dependencias: entra desde MOD-004. Sale hacia MOD-007, MOD-008, MOD-009, MOD-010, MOD-013, MOD-014, MOD-015, MOD-016, MOD-018.
- Notas reforma 659: No aplica directamente.

### MOD-007 Consentimiento (Registrar)
- Proposito: Registra el consentimiento cuando es la base juridica elegida, con evidencia de finalidad, canal, version del aviso mostrado y fecha; gestiona la revocacion como flujo de dos plazos encadenados (5 + 5 dias habiles); refuerza datos sensibles, biometria y menores de edad.
- Submodulos: Registro y revocacion de consentimiento; Sub-flujo titular menor de edad.
- Obligaciones que cubre (propietario): OBL-CONS-01, OBL-CONS-02, OBL-CONS-03, OBL-CONS-04, OBL-CONS-05, OBL-CONS-06, OBL-PRIN-01, OBL-PRIN-04, OBL-SENS-02, OBL-SENS-03, OBL-SENS-07, OBL-TRAT-02 (12).
- Areas del prompt que absorbe: 16.
- Decision respecto al documento maestro y a la propuesta ganadora: Se mantiene (sec. 19 del maestro), con dos sub-flujos nuevos (menores de edad, alternativa no biometrica obligatoria) por los faltantes 25 y 27 de 02_validacion_de_la_idea.md.
- MVP: MUST HAVE. Justificacion: Concentra 4 obligaciones OBLIGATORIO (CONS-01 a 04) con riesgo de infraccion muy grave (26 a 40 salarios minimos, seccion 6 de 03_hallazgos_regulatorios.md).
- Dependencias: entra desde MOD-006, MOD-008. Sale hacia MOD-009, MOD-011, MOD-019.
- Notas reforma 659: OBL-CONS-03 (revocacion) esta afectada: el destinatario de la notificacion de revocacion depende del estado vigente del responsable del tramite (MOD-002).

### MOD-008 Documentos y Politicas (Registrar)
- Proposito: Gestor documental regulatorio que produce y versiona la Politica de Proteccion de Datos, la Politica de Privacidad y el Aviso de Privacidad, con flujo de aprobacion configurable por tipo de documento. Motor documental generico reutilizado por referencia (por ejemplo, Contratos/DPA dentro de Proveedores).
- Obligaciones que cubre (propietario): OBL-AVISO-01, OBL-AVISO-02, OBL-AVISO-03, OBL-AVISO-04, OBL-AVISO-05, OBL-DOC-01 (6).
- Areas del prompt que absorbe: 15.
- Decision respecto al documento maestro y a la propuesta ganadora: Se mantiene (sec. 20 del maestro), absorbe Contratos/DPA como tipo de documento (fusion parcial de la sec. 23), decision 2.7.2.
- MVP: MUST HAVE. Justificacion: El Aviso de Privacidad (OBL-AVISO-01/02/03/05) es OBLIGATORIO y su mecanismo de publicacion tiene plazo transitorio ya vencido (OBL-PLAZO-04, 23-may-2025, propietaria de MOD-012).
- Dependencias: entra desde MOD-004, MOD-006. Sale hacia MOD-007, MOD-009, MOD-012, MOD-016, MOD-019.
- Notas reforma 659: No aplica directamente; el Aviso de Privacidad puede requerir revision tras un cambio de estado (ver seccion 5, punto 5 del documento principal).

### MOD-009 Proveedores y Encargados (Registrar)
- Proposito: Registra encargados del tratamiento, terceros/receptores y subencargados, con sus contratos/DPA, medidas de seguridad y evaluacion de riesgo, como tres tipos de entidad con obligaciones propias.
- Submodulos: Encargados; Terceros / Receptores; Subencargados; Contratos / DPA (tipo de documento, enlazado a MOD-008).
- Obligaciones que cubre (propietario): OBL-PROV-01, OBL-PROV-02, OBL-PROV-03, OBL-PROV-04, OBL-PROV-05, OBL-PROV-06, OBL-PROV-07 (7).
- Areas del prompt que absorbe: 17.
- Decision respecto al documento maestro y a la propuesta ganadora: Se fusiona (sec. 22 Proveedores y terceros + sec. 23 Contratos/DPA como submodulo documental), dividido en tres tipos de entidad (decision 2.7.2, 2.7.8, inconsistencia 9).
- MVP: MUST HAVE. Justificacion: Identificado como nucleo por 02_validacion_de_la_idea.md 2.1; concentra obligaciones OBLIGATORIO (PROV-01 a 04) y casi toda empresa objetivo tiene al menos un proveedor de tecnologia/cloud.
- Dependencias: entra desde MOD-006. Sale hacia MOD-008, MOD-010, MOD-019.
- Notas reforma 659: No aplica directamente.

### MOD-010 Transferencias Internacionales (Registrar)
- Proposito: Registra cada flujo de datos hacia otro pais (tratamiento, proveedor, pais, base juridica, salvaguarda, evidencia de puesta en conocimiento a la ACE), detectando transferencias no documentadas al cruzar Proveedores con el RAT.
- Obligaciones que cubre (propietario): OBL-TRANSF-01, OBL-TRANSF-02, OBL-TRANSF-03, OBL-TRANSF-04, OBL-TRANSF-05, OBL-TRANSF-06 (6).
- Areas del prompt que absorbe: 18.
- Decision respecto al documento maestro y a la propuesta ganadora: Se mantiene (sec. 24 del maestro), enlaza por referencia a Proveedores en vez de duplicar campos de contrato (decision 2.7.2).
- MVP: SHOULD HAVE. Justificacion: Test de tres condiciones (injerto del juez 1 y 2 desde propuesta_mapa_mvp.md, ver seccion 4): no cubre una obligacion OBLIGATORIO con plazo ya vencido, no es dependencia estructural de otro MUST HAVE, y el diagnostico ya detecta el caso desde el MVP sin este modulo completo. Queda SHOULD HAVE.
- Cobertura parcial en el MVP (modulo SHOULD/COULD HAVE): El diagnostico (MOD-004) marca "datos fuera de El Salvador: si" y crea una tarea manual en MOD-021 para que el responsable documente la transferencia como evidencia suelta en MOD-019, sin motor de deteccion automatica ni registro formal "pendiente de confirmar" (patron injertado de propuesta_mapa_mvp.md, ficha de su MOD-016).
- Dependencias: entra desde MOD-006, MOD-009. Sale hacia MOD-007, MOD-015, MOD-019, MOD-024.
- Notas reforma 659: No aplica directamente.

### MOD-011 ARCO-POL (Operar)
- Proposito: Gestiona el ciclo de vida completo de una solicitud de un titular (acceso, rectificacion, cancelacion, oposicion, portabilidad, olvido, limitacion), desde la verificacion de identidad hasta el cierre, con tres ramas: incompetencia, notificacion a receptores y reclamo ante la ACE.
- Submodulos: Verificacion de identidad del titular; Rama Incompetencia; Rama Notificacion a receptores; Rama Reclamo ante la ACE.
- Obligaciones que cubre (propietario): OBL-ARCO-01, OBL-ARCO-02, OBL-ARCO-03, OBL-ARCO-04, OBL-ARCO-05, OBL-ARCO-06, OBL-ARCO-07, OBL-ARCO-08, OBL-ARCO-09, OBL-ARCO-10, OBL-ARCO-11, OBL-ARCO-12, OBL-ARCO-13, OBL-ARCO-14, OBL-ARCO-15 (15).
- Areas del prompt que absorbe: 13.
- Decision respecto al documento maestro y a la propuesta ganadora: Se mantiene y se amplia (sec. 17 del maestro), con las tres ramas nuevas y el subproceso de verificacion de identidad (decisiones 2.7.10 y 2.7.18, inconsistencia 12, faltantes 8 y 11).
- MVP: MUST HAVE. Justificacion: Concentra la mayor cantidad de obligaciones de toda la matriz (15 propias + 3 colaboradoras); tiene plazo transitorio ya vencido (OBL-PLAZO-04, propietaria de MOD-012); es nucleo segun 02_validacion_de_la_idea.md 2.1.
- Dependencias: entra desde MOD-012, MOD-007, MOD-002. Sale hacia MOD-009, MOD-010, MOD-019, MOD-021, MOD-022, MOD-023, MOD-024.
- Notas reforma 659: 5 obligaciones afectadas (OBL-ARCO-01, 08, 10, 11, 14): la resolucion y aprobacion de casos depende del estado vigente del responsable del tramite en MOD-002.

### MOD-012 Portal del Titular (Operar)
- Proposito: Canal publico opcional para que el titular consulte el aviso y la politica, presente ARCO-POL y consulte el estado de su solicitud de forma autenticada. En el MVP la obligacion legal de mecanismos de ejercicio de derechos ya se satisface con el formulario interno seguro de MOD-011; el portal publico con autoregistro es una capa adicional posterior.
- Obligaciones que cubre (propietario): OBL-DOC-04, OBL-PLAZO-04 (2).
- Areas del prompt que absorbe: 33.
- Decision respecto al documento maestro y a la propuesta ganadora: Se mantiene pero se reduce el alcance en MVP (sec. 18 del maestro, "Portal de privacidad"), decision 2.7.30: el MVP satisface la obligacion legal con un formulario interno seguro; el portal publico dedicado es V1/Enterprise.
- MVP: SHOULD HAVE. Justificacion: Test de tres condiciones: la obligacion legal (OBL-DOC-04, OBL-PLAZO-04) ya esta cubierta por el formulario interno de MOD-011 desde el MVP; el portal publico anade superficie de riesgo de identidad que conviene madurar despues. Queda SHOULD HAVE.
- Cobertura parcial en el MVP (modulo SHOULD/COULD HAVE): OBL-DOC-04 y OBL-PLAZO-04 (mecanismos de ejercicio de derechos) ya estan cubiertas en el MVP por el formulario interno seguro de MOD-011; no hay vacio legal, solo un canal adicional diferido.
- Dependencias: entra desde MOD-008. Sale hacia MOD-011, MOD-019, MOD-023.
- Notas reforma 659: No aplica directamente.

### MOD-013 Incidentes de Seguridad (Operar)
- Proposito: Gestiona el ciclo completo de una vulneracion de seguridad (deteccion, contencion, analisis, decision, notificacion, remediacion, cierre) con dos hitos de 72 horas modelados por separado: notificacion externa a la ACE/Fiscalia/titulares e inicio de la revision interna.
- Obligaciones que cubre (propietario): OBL-INC-01, OBL-INC-02, OBL-INC-03, OBL-INC-04, OBL-INC-05 (5).
- Areas del prompt que absorbe: 19.
- Decision respecto al documento maestro y a la propuesta ganadora: Se mantiene (sec. 25 del maestro), con los dos hitos de 72 horas separados y visibles, criterio conservador por defecto de horas corridas (decision 2.7.11, inconsistencia 13).
- MVP: MUST HAVE. Justificacion: Las 5 obligaciones son OBLIGATORIO, con el plazo mas critico y visible del corpus (72 horas); es nucleo segun 02_validacion_de_la_idea.md 2.1.
- Dependencias: entra desde MOD-006, MOD-015. Sale hacia MOD-019, MOD-021, MOD-022, MOD-023, MOD-024.
- Notas reforma 659: No aplica directamente.

### MOD-014 Riesgos y EIPD (Operar)
- Proposito: Evalua tratamientos de alto riesgo (biometria, salud, menores, monitoreo, transferencias, gran escala) y genera Evaluaciones de Impacto en la Privacidad, seleccionando controles del catalogo unico de MOD-015. El resultado siempre requiere aprobacion humana, nunca es una conclusion legal automatica.
- Obligaciones que cubre (propietario): OBL-DOC-03 (1).
- Areas del prompt que absorbe: 20.
- Decision respecto al documento maestro y a la propuesta ganadora: Se mantiene (sec. 26 del maestro), comparte la entidad Control con MOD-015 en vez de duplicarla (decision 2.7.3, inconsistencia 3).
- MVP: SHOULD HAVE. Justificacion: Test de tres condiciones: OBL-DOC-03 es OBLIGATORIO pero solo se activa por disparadores especificos que el diagnostico ya detecta desde el MVP; no tiene plazo transitorio vencido propio ni es dependencia estructural de otro MUST HAVE. Queda SHOULD HAVE.
- Cobertura parcial en el MVP (modulo SHOULD/COULD HAVE): Cuando el diagnostico (MOD-004) detecta biometria, salud, menores o camaras, crea una tarea en MOD-021 ("elaborar EIPD") con una plantilla generica en MOD-008, llenada manualmente, sin el motor de scoring (patron injertado de propuesta_mapa_mvp.md, ficha de su MOD-018).
- Dependencias: entra desde MOD-004, MOD-006. Sale hacia MOD-015, MOD-019, MOD-021.
- Notas reforma 659: No aplica directamente.

### MOD-015 Controles de Seguridad (Operar)
- Proposito: Catalogo unico de controles tecnicos, organizativos y fisicos (MFA, cifrado, backups, eliminacion segura) con evidencia de implementacion, responsable, vigencia y estado. Registra evidencia, no ejecuta ni sustituye herramientas de seguridad.
- Obligaciones que cubre (propietario): OBL-SEG-01, OBL-SEG-02, OBL-SEG-03, OBL-SEG-04, OBL-SEG-05, OBL-SEG-06, OBL-SENS-05 (7).
- Areas del prompt que absorbe: 21.
- Decision respecto al documento maestro y a la propuesta ganadora: Se mantiene (sec. 27 del maestro), entidad Control compartida con MOD-014 (decision 2.7.3).
- MVP: MUST HAVE. Justificacion: Identificado como nucleo por 02_validacion_de_la_idea.md 2.1; concentra el bloque de infraccion grave (11 a 25 salarios minimos) por no implementar medidas de la ACE; su plazo transitorio ya vencio (OBL-PLAZO-03, MOD-005).
- Dependencias: entra desde MOD-006, MOD-010. Sale hacia MOD-013, MOD-014, MOD-018, MOD-019.
- Notas reforma 659: No aplica directamente.

### MOD-016 Retencion y Eliminacion (Operar)
- Proposito: Dos motores de retencion separados: retencion de datos personales del titular (por finalidad, con fecha efectiva igual al maximo entre todos los OBL-RET aplicables) y retencion documental de cumplimiento propio (avisos 10 anios, expedientes ARCO-POL/incidentes 5 anios).
- Submodulos: Motor de retencion de datos del titular; Motor de retencion documental de cumplimiento.
- Obligaciones que cubre (propietario): OBL-RET-01, OBL-RET-02, OBL-RET-03, OBL-RET-04, OBL-RET-05, OBL-RET-06 (6).
- Areas del prompt que absorbe: 22.
- Decision respecto al documento maestro y a la propuesta ganadora: Se mantiene (sec. 21 del maestro), dividido internamente en dos motores (decision 2.7.13, inconsistencia 15).
- MVP: SHOULD HAVE. Justificacion: Test de tres condiciones: dos obligaciones (RET-04, RET-06) son OBLIGATORIO sin condicion, pero el resto son CONDICIONAL segun el giro del cliente; no hay plazo transitorio vencido especifico ni es dependencia estructural. Queda SHOULD HAVE.
- Cobertura parcial en el MVP (modulo SHOULD/COULD HAVE): OBL-RET-04 (aviso 10 anios) y OBL-RET-06 ya se cubren directamente como conservacion dentro de MOD-008 Documentos y de los expedientes de MOD-011/MOD-013 desde el MVP; el campo "plazo de conservacion" vive como texto dentro del RAT (MOD-006) sin alertas automaticas ni flujo de aprobacion de eliminacion (patron injertado de propuesta_mapa_mvp.md, ficha de su MOD-017).
- Dependencias: entra desde MOD-006, MOD-008. Sale hacia MOD-011, MOD-019.
- Notas reforma 659: OBL-RET-04 (conservacion del aviso 10 anios) esta afectada: el contenido del aviso a conservar puede versionar segun el estado vigente al momento de su publicacion.

### MOD-017 Capacitacion (Operar)
- Proposito: Dos programas de capacitacion: registro minimo obligatorio de que el personal recibio capacitacion (todo el personal), y capacitacion especifica anual del Delegado / Responsable Interno (MOD-002).
- Submodulos: Capacitacion general del personal; Capacitacion del Delegado / Responsable Interno (MOD-002).
- Obligaciones que cubre (propietario): OBL-CAP-01, OBL-CAP-02 (2).
- Areas del prompt que absorbe: 23.
- Decision respecto al documento maestro y a la propuesta ganadora: Se mantiene (sec. 28 del maestro), pero el registro minimo pasa de "a evaluar" a MVP explicito (decision 2.7.23, inconsistencia 25).
- MVP: MUST HAVE. Justificacion: OBL-CAP-01 es OBLIGATORIO sin condicion (medida organizativa de las Politicas ACE); cursos interactivos, microlearning y certificados quedan como funcionalidad diferenciadora en V1/V2.
- Dependencias: entra desde MOD-001, MOD-002. Sale hacia MOD-019, MOD-020.
- Notas reforma 659: OBL-CAP-02 (capacitacion especifica del Delegado) esta afectada: se mantiene mientras el estado sea ACTUAL; en estado FUTURO pasa a buena practica voluntaria si la empresa mantiene al Responsable Interno.

### MOD-018 Auditoria de Cumplimiento (Demostrar)
- Proposito: Programa sustantivo de auditoria anual (alcance, hallazgos, plan de accion, cierre), distinto del registro tecnico de trazabilidad (AuditLog, funcion transversal embebida en todos los modulos). Genera el recordatorio anual anclado a la ultima auditoria registrada.
- Obligaciones que cubre (propietario): OBL-AUD-01 (1).
- Areas del prompt que absorbe: 24.
- Decision respecto al documento maestro y a la propuesta ganadora: Se divide de la sec. 29 del maestro ("Auditoria y trazabilidad") en este modulo (programa sustantivo) mas la funcion transversal de AuditLog, embebida en todos los modulos (decision 2.7.26, faltante 19).
- MVP: SHOULD HAVE. Justificacion: Test de tres condiciones: OBL-AUD-01 es OBLIGATORIO pero la primera auditoria formal solo es exigible tras el primer anio de operacion; no cubre un plazo ya vencido ni es dependencia estructural de otro MUST HAVE. Queda SHOULD HAVE.
- Cobertura parcial en el MVP (modulo SHOULD/COULD HAVE): El calendario/checklist de la auditoria anual existe desde el MVP (vinculado a MOD-023), y el AuditLog tecnico (funcion transversal embebida en todo modulo MUST HAVE) ya deja evidencia desde el primer dia; solo el primer ciclo completo de auditoria sustantiva se difiere.
- Dependencias: entra desde MOD-015, MOD-006, MOD-019. Sale hacia MOD-019, MOD-020, MOD-021. La entrada desde MOD-019 y la salida hacia MOD-019 son una relacion reciproca intencional, no un ciclo de orden de construccion: ver seccion 6.1.
- Notas reforma 659: No aplica directamente.

### MOD-019 Centro de Evidencias (Demostrar)
- Proposito: Responde que evidencia tenemos de esta obligacion, conectando tres entidades separadas (Documento, Evidencia, AuditLog) sin mezclarlas; el paquete exportable es una vista sobre las tres, con verificacion de integridad (hash o firma) en cada exportacion. Funciona de forma semi-transversal (recibe evidencia de MOD-007 a MOD-017 de forma continua) aunque se ubica en la etapa Demostrar por ser su destino natural en el recorrido.
- Obligaciones que cubre (propietario): OBL-PRIN-03 (1).
- Areas del prompt que absorbe: 25.
- Decision respecto al documento maestro y a la propuesta ganadora: Se mantiene (sec. 30 del maestro, "Paquete de evidencias"), redefinido como entidad propia mas vista de exportacion (decision 2.7.4, 2.7.24, inconsistencias 4, 11 y 26).
- MVP: MUST HAVE. Justificacion: El principio de responsabilidad demostrada (OBL-PRIN-03, Art. 5 lit. i) es transversal a toda la matriz; sin este modulo ningun otro puede demostrar cumplimiento ante la ACE. Es la tercera condicion del test de tres condiciones (capacidad probatoria desde el primer dia).
- Dependencias: entra desde MOD-007, MOD-008, MOD-009, MOD-010, MOD-011, MOD-012, MOD-013, MOD-014, MOD-015, MOD-016, MOD-017, MOD-018. Sale hacia MOD-018, MOD-020, MOD-024. La entrada desde MOD-018 y la salida hacia MOD-018 son una relacion reciproca intencional, no un ciclo de orden de construccion: ver seccion 6.1.
- Notas reforma 659: No aplica directamente; conserva evidencia de ambos regimenes sin alterar retroactivamente expedientes cerrados.

### MOD-020 Dashboard y Reportes (Demostrar)
- Proposito: Vista principal por perspectiva (Gerencia: vision general; Responsable: pendientes; Legal/Delegado: riesgos y decisiones; Auditor: evidencias), mas reportes exportables. La perspectiva Legal/Delegado puede filtrar por los ocho clusters legales (Nucleo organizativo, Entrada y hoja de ruta, Registro y gobernanza, Relacion con el titular, Relacion con terceros, Gestion de crisis y control, Documentacion, Relacion con la autoridad) como vista alternativa a las 6 etapas del recorrido. Usa siempre lenguaje de estado del programa, nunca cumplimiento legal X%.
- Submodulos: Dashboard por perspectiva (Gerencia, Responsable, Legal/Delegado, Auditor); Reportes exportables.
- Obligaciones que cubre (propietario): ninguna con OBL-ID propio.
- Areas del prompt que absorbe: 26, 28.
- Decision respecto al documento maestro y a la propuesta ganadora: Se fusiona (sec. 31 Dashboard del maestro + area 28 del prompt, no desarrollada como modulo propio en el maestro). Se anade, por injerto del juez 3 (idea 5, desde propuesta_mapa_obligaciones.md), que la perspectiva Legal/Delegado puede filtrar por los 8 clusters legales de esa propuesta como vista alternativa.
- MVP: MUST HAVE. Justificacion: Dashboard basico (pendientes, vencidos, tratamientos, solicitudes) MUST HAVE; reportes exportables avanzados por area SHOULD HAVE dentro del mismo modulo.
- Dependencias: entra desde MOD-005, MOD-019, MOD-021. Sale hacia ninguno (es un modulo terminal de lectura).
- Notas reforma 659: No aplica directamente.

### MOD-021 Centro de Tareas (Transversal, transversal)
- Proposito: Convierte cada obligacion en una accion concreta con titulo, fundamento, responsable, fecha, dependencia, evidencia requerida y estado (Pendiente, En proceso, Bloqueada, En revision, Aprobada, Completada, Vencida). Alimentado por Diagnostico, ARCO-POL, Incidentes, Proveedores, Riesgos, Documentos y Auditoria.
- Obligaciones que cubre (propietario): ninguna con OBL-ID propio.
- Areas del prompt que absorbe: 14.
- Decision respecto al documento maestro y a la propuesta ganadora: Se mantiene (sec. 16 del maestro), confirmado como modulo transversal.
- MVP: MUST HAVE. Justificacion: Es el mecanismo operativo central del objetivo del producto (sec. 49 del maestro: "asigna tareas, controla plazos"). Condicion (b) del test de tres condiciones: dependencia estructural de todos los modulos MUST HAVE.
- Dependencias: entra desde MOD-004, MOD-005, MOD-011, MOD-013, MOD-002. Sale hacia MOD-022, MOD-023, MOD-020.
- Notas reforma 659: No aplica directamente; las tareas dependientes de MOD-002 se marcan "no aplica bajo el estado regulatorio actual, ver historial" en vez de eliminarse cuando cambia el estado (ver seccion 4).

### MOD-022 Notificaciones (Transversal, transversal)
- Proposito: Envia alertas por evento (tarea proxima a vencer, plazo de 72 horas, prevencion ARCO-POL sin resolver, documento por vencer) con destinatario, prioridad, frecuencia y escalamiento configurables, sin asumir todos los canales posibles.
- Obligaciones que cubre (propietario): ninguna con OBL-ID propio.
- Areas del prompt que absorbe: 27.
- Decision respecto al documento maestro y a la propuesta ganadora: Nuevo como modulo propio; el maestro lo trata como lista de canales dentro de la sec. 25 (Incidentes) sin modulo transversal dedicado.
- MVP: MUST HAVE. Justificacion: MUST HAVE con canales basicos (plataforma y email); canales adicionales (Teams, Slack, SMS, WhatsApp) quedan en V1/V2 segun demanda real de los primeros clientes.
- Dependencias: entra desde MOD-021, MOD-023, MOD-011, MOD-013. Sale hacia ninguno (es un modulo terminal de lectura).
- Notas reforma 659: No aplica directamente.

### MOD-023 Calendario y Motor de Plazos (Transversal, transversal)
- Proposito: Centraliza el calculo de dias y horas habiles y asuetos nacionales configurables por anio, y expone un unico servicio de plazos consultado por ARCO-POL, Incidentes, Delegado y Procedimiento sancionador.
- Obligaciones que cubre (propietario): OBL-PLAZO-01, OBL-PLAZO-02 (2).
- Areas del prompt que absorbe: 30.
- Decision respecto al documento maestro y a la propuesta ganadora: Nuevo como modulo propio y transversal; el maestro trataba el calculo de dias habiles como detalle disperso dentro de ARCO-POL (sec. 17) e Incidentes (sec. 25), decision 2.7.15, inconsistencia 17, faltante 31.
- MVP: MUST HAVE. Justificacion: Condicion (b) del test de tres condiciones: sin un motor de plazos unico y confiable, ARCO-POL e Incidentes (ambos MUST HAVE) no pueden calcular correctamente sus plazos legales.
- Dependencias: entra desde ninguno (punto de entrada o configuracion mantenida por el equipo del producto). Sale hacia MOD-002, MOD-011, MOD-013, MOD-021, MOD-022, MOD-024.
- Notas reforma 659: No aplica directamente; el motor de plazos es el mismo en ambos regimenes.

### MOD-024 Centro Regulatorio (Transversal, transversal)
- Proposito: Muestra el marco normativo aplicable clasificado como VIGENTE, FUTURO, DEROGADO o MODIFICADO, gestiona la bandera de activacion manual del doble estado de la reforma 659, y aloja el Procedimiento Sancionador y los Tramites ante la ACE. El contenido informativo y el flujo operativo con dinero y plazos reales deben separarse visualmente en la UI.
- Submodulos: Marco normativo consultable; Actualizaciones normativas (funcion transversal de este mismo modulo); Procedimiento Sancionador; Tramites ante la ACE.
- Obligaciones que cubre (propietario): OBL-AUD-02, OBL-PLAZO-05, OBL-SANC-01, OBL-SANC-02, OBL-SANC-03, OBL-SANC-04, OBL-SANC-05, OBL-SANC-06, OBL-SANC-07, OBL-SANC-08, OBL-SANC-09 (11).
- Areas del prompt que absorbe: 31, 32.
- Decision respecto al documento maestro y a la propuesta ganadora: Se fusiona y se amplia (secs. 40 "Motor regulatorio" y 41 "Actualizacion normativa" del maestro, alli tratadas como arquitectura tecnica, aqui convertidas en modulo funcional), mas dos piezas nuevas: Procedimiento Sancionador y Tramites ante la ACE (decisiones 2.7.16, 2.7.19, 2.7.25).
- MVP: MUST HAVE. Justificacion: MUST HAVE el nucleo (marco normativo + bandera de doble estado de la reforma 659, condicion (b): MOD-002 y MOD-011 dependen de esta bandera); SHOULD HAVE el Procedimiento Sancionador completo, porque sus obligaciones son mayormente CONDICIONAL (solo se activan si la ACE abre un caso).
- Cobertura parcial en el MVP (modulo SHOULD/COULD HAVE): El catalogo de infracciones (informativo, OBL-SANC-01) se muestra desde el MVP dentro del nucleo de MOD-024; solo el flujo operativo completo del Procedimiento Sancionador (contestacion, pago, medidas) se difiere.
- Dependencias: entra desde ninguno (punto de entrada o configuracion mantenida por el equipo del producto). Sale hacia MOD-002, MOD-011, MOD-007, MOD-017, MOD-015, MOD-021.
- Notas reforma 659: Aloja la bandera de activacion del doble estado (regimen_reforma_659) y OBL-PLAZO-05 (afectada). Es el unico modulo que decide que estado esta vigente.

### MOD-025 Busqueda Global (Transversal, transversal)
- Proposito: Busqueda sobre tratamientos, solicitudes ARCO-POL, proveedores, documentos, incidentes y tareas, para que un usuario no especialista encuentre informacion sin memorizar en que modulo vive.
- Obligaciones que cubre (propietario): ninguna con OBL-ID propio.
- Areas del prompt que absorbe: 29.
- Decision respecto al documento maestro y a la propuesta ganadora: Nuevo como modulo propio; el maestro no lo desarrolla.
- MVP: COULD HAVE. Justificacion: Mejora de usabilidad valiosa pero no bloquea ninguna obligacion legal; postergable sin riesgo de incumplimiento.
- Dependencias: entra desde ninguno (punto de entrada o configuracion mantenida por el equipo del producto). Sale hacia ninguno (es un modulo terminal de lectura).
- Notas reforma 659: No aplica directamente.

### MOD-026 Centro de Ayuda (Transversal, transversal)
- Proposito: Ayuda contextual por modulo (que es, por que debo registrarlo, fundamento normativo, cuando necesito asesoria juridica externa), coherente con el principio de lenguaje claro (Art. 5 lit. e LPDP).
- Obligaciones que cubre (propietario): ninguna con OBL-ID propio.
- Areas del prompt que absorbe: 34.
- Decision respecto al documento maestro y a la propuesta ganadora: Nuevo como modulo propio; el maestro no lo desarrolla como modulo, solo lo menciona como enfoque de UX en la sec. 32.
- MVP: MUST HAVE. Justificacion: Es la instrumentacion directa del principio central del producto: usable por alguien que no es especialista en privacidad. Wizards y niveles Intermedio/Especialista completos quedan en V1.
- Dependencias: entra desde ninguno (punto de entrada o configuracion mantenida por el equipo del producto). Sale hacia ninguno (es un modulo terminal de lectura).
- Notas reforma 659: No aplica directamente.

---

## 4. Modulos transversales y como se conectan

Los 6 modulos de la barra transversal (MOD-021 a MOD-026) no pertenecen a una etapa del recorrido: aparecen como una barra fija disponible desde cualquier pantalla, porque instrumentan capacidades que todos los modulos de recorrido necesitan. Esto coincide con los 7 modulos transversales que el propio enunciado de la tarea nombra explicitamente (tareas, evidencias, auditoria, notificaciones, calendario, regulatorio, ayuda), con una diferencia deliberada, injertada del juez 1 (idea 5, ver seccion 12): MOD-018 Auditoria y MOD-019 Evidencias NO estan en la barra transversal, sino en la etapa Demostrar, porque son su destino natural en el recorrido del usuario, aunque funcionan de forma semi-transversal (reciben datos de todos los modulos operativos de forma continua, no solo al final). Los otros modulos que este mapa agrega a la barra por el mismo criterio de soporte (Dashboard/Reportes en MOD-020, Busqueda en MOD-025, Usuarios/roles como submodulo de MOD-001) no estan nombrados explicitamente en el prompt de analisis, pero surgen del mismo principio de diseno (distincion tambien injertada del juez 1, idea 5, desde `propuesta_mapa_obligaciones.md`).

```
                    +-------------------------------------------------+
                    |            BARRA TRANSVERSAL (siempre visible)  |
                    |  Tareas | Notif. | Calendario | Regulatorio     |
                    |         | Busqueda | Ayuda                     |
                    +-------------------------------------------------+
                                     ^  |
                     produce eventos |  | consulta / recibe alertas
                                     |  v
   EMPEZAR -> DIAGNOSTICAR -> PLANIFICAR -> REGISTRAR -> OPERAR -> DEMOSTRAR
   (001,002,003) (004)      (005)       (006..010)  (011..017) (018,019,020)
```

Reglas de conexion:
1. **MOD-021 Centro de Tareas** es el unico lugar donde una obligacion se convierte en una accion con responsable y fecha; todo modulo de recorrido que genera trabajo crea tareas alli, en vez de mantener su propia lista de pendientes.
2. **MOD-022 Notificaciones** solo reacciona a eventos que le entregan MOD-021 y MOD-023; ningun modulo de recorrido envia notificaciones por su cuenta.
3. **MOD-023 Calendario y Motor de Plazos** es el unico que calcula dias/horas habiles; ARCO-POL, Incidentes, Delegado y Procedimiento sancionador le piden el calculo, nunca lo reimplementan.
4. **MOD-024 Centro Regulatorio** es el unico que decide que version de una regla esta activa (doble estado, ver seccion 5); ningun otro modulo evalua por si mismo si la reforma 659 esta vigente.
5. **MOD-025 Busqueda Global** y **MOD-026 Centro de Ayuda** son de solo lectura sobre el resto de modulos: no generan tareas ni escriben en otras entidades, solo indexan o explican.
6. **MOD-019 Centro de Evidencias**, aunque se ubica en la etapa Demostrar, funciona en la practica como semi-transversal: cada modulo operativo (MOD-007 a MOD-017) le entrega evidencia continuamente, no solo al final del recorrido. Con MOD-018 Auditoria de Cumplimiento la relacion es ademas reciproca (MOD-018 consulta la evidencia de MOD-019 para elaborar sus hallazgos, y esos hallazgos vuelven a MOD-019 como nueva evidencia): es el unico par de modulos del mapa cuyo `depende_de` es mutuo, detallado en la seccion 6.1.
7. **Direccion unica entre modulos de proceso** (injerto del juez 3 desde `propuesta_mapa_obligaciones.md`): cuando MOD-009 Proveedores o MOD-016 Retencion referencian datos de MOD-006 RAT, o cuando MOD-007 Consentimiento referencia la version del aviso de MOD-008 Documentos, esa referencia es de lectura; el modulo que crea el dato original (RAT, Documentos) sigue siendo su unico propietario y nunca hay dos copias del mismo campo mutandose por separado.

Tabla "que aportaria si faltara / quien lo consume" para los 6 modulos transversales (injerto de los jueces 1 y 2, patron tomado de `propuesta_mapa_mvp.md` seccion 3):

| Modulo | Que aportaria si faltara (riesgo de no tenerlo) | Quien lo consume |
|---|---|---|
| MOD-021 Centro de Tareas | Las obligaciones detectadas quedarian como texto sin responsable ni fecha | Todos los modulos operativos |
| MOD-022 Notificaciones | Los plazos legales (20+20 dias, 72 horas, 5 dias, 15 dias del Delegado) dependerian de que alguien recuerde entrar a mirar | MOD-011, MOD-013, MOD-021, MOD-002 |
| MOD-023 Calendario y Motor de Plazos | Cada modulo con plazo legal calcularia dias habiles por su cuenta, con riesgo de resultados distintos para el mismo caso | MOD-011, MOD-013, MOD-002, MOD-024, MOD-021 |
| MOD-024 Centro Regulatorio | No existiria un lugar unico donde saber si la reforma 659 ya aplica o no, y cada modulo tendria que decidirlo por separado | MOD-002, MOD-011, MOD-007, MOD-017, MOD-015 |
| MOD-025 Busqueda Global | El usuario no especialista tendria que memorizar en que modulo vive cada registro | Todos los modulos con contenido indexable |
| MOD-026 Centro de Ayuda | El usuario no especialista quedaria solo frente a terminologia juridica, rompiendo el principio central del producto | Todos los modulos operativos |

---

## 5. Explicacion del doble estado de la reforma 659 (sin duplicar modulos)

Contexto juridico (ver `00_contexto_para_agentes.md` seccion 3 y `01_legal/03_hallazgos_regulatorios.md` secciones 3 y 9): el Decreto Legislativo 659 fue aprobado el 17-sep-2026 pero al 24-sep-2026 no esta confirmada su publicacion en el Diario Oficial. Mientras no se publique, el texto vigente del Decreto 144 (Arts. 15 y 17) exige delegado obligatorio en el sector privado. Segun fuentes secundarias, la reforma eliminaria esa obligatoriedad y trasladaria las funciones al "sujeto obligado" (responsable interno, sin nombramiento formal ante la ACE). 17 obligaciones de la matriz quedan marcadas como afectadas por esta reforma (verificado contra `matriz_obligaciones.json`, campo `afectada_por_reforma_659.afectada = true`: OBL-DPO-01 a 08, OBL-ARCO-01/08/10/11/14, OBL-CONS-03, OBL-CAP-02, OBL-RET-04, OBL-PLAZO-05).

Principio de diseno (heredado sin cambios de la propuesta ganadora): un solo modulo (ahora MOD-002, antes submodulo de MOD-001) y una sola entidad conceptual ("Responsable del Programa de Datos") sirven tanto para el regimen ACTUAL como para el regimen FUTURO. Lo que cambia no es el modulo ni la entidad, sino dos atributos de esa entidad mas una bandera de activacion global que vive en MOD-024.

1. **Una sola entidad con un atributo de tipo de rol.** La persona designada se registra siempre en MOD-002 con un campo `tipo_rol` que toma el valor `DELEGADO` (regimen ACTUAL, Arts. 15 y 17 vigentes) o `RESPONSABLE_INTERNO` (regimen FUTURO, si la reforma se confirma). El formulario de alta, el historial, las tareas asociadas y la capacitacion (MOD-017) son los mismos campos y las mismas pantallas; solo cambia la etiqueta y el conjunto de obligaciones activas.
2. **Una bandera de activacion global en MOD-024, nunca automatica.** MOD-024 mantiene un interruptor `regimen_reforma_659` con dos valores: `ACTUAL` (por defecto, el vigente al 2026-09-24) y `FUTURO` (activable manualmente solo cuando el equipo del producto confirme la publicacion del decreto en el Diario Oficial y transcurran los 8 dias de vacatio legis). El sistema nunca activa `FUTURO` por la sola fecha de aprobacion legislativa (17-sep-2026); registra la fecha del cambio de bandera para trazabilidad.
3. **Las 17 obligaciones afectadas cambian de estado, no de modulo.** Cuando la bandera pasa a `FUTURO`: OBL-DPO-01 a 08 (8, en MOD-002), OBL-ARCO-01, 08, 10, 11, 14 (5, en MOD-011), OBL-CAP-02 (1, en MOD-017), OBL-CONS-03 (1, en MOD-007), OBL-RET-04 (1, en MOD-016) y OBL-PLAZO-05 (1, en MOD-024) actualizan su clasificacion y su "a quien aplica", sin cambiar de modulo propietario. Total 17, igual al conteo verificado de `matriz_obligaciones.json`.
4. **Los actos atribuidos hoy al "delegado" (prevencion, incompetencia, notificacion a receptores, revocacion) se redactan igual en MOD-011, MOD-007 y MOD-002, sin importar el regimen; solo cambia quien debe aprobarlos** (la persona con `tipo_rol = DELEGADO` hoy, cualquier persona designada como `RESPONSABLE_INTERNO` despues).
5. **El aviso de privacidad (MOD-008) no se reescribe automaticamente al cambiar la bandera.** Dado que el Art. 24 lit. h exige datos de contacto del encargado/responsable del tramite, MOD-024 dispara una tarea en MOD-021 ("revisar avisos publicados tras el cambio de regimen") en vez de sobrescribir documentos ya publicados.
6. **Preservacion de historial, en vez de borrado [injerto de los jueces 1 y 2, tomado de `propuesta_mapa_mvp.md` seccion 4].** Cuando la bandera pasa de `ACTUAL` a `FUTURO`, las tareas y registros de MOD-021 que dependian de pasos exclusivos del regimen `ACTUAL` (reverificacion cada 3 anios, informes semestrales, comunicacion formal a la ACE) no se eliminan: se marcan "no aplica bajo el estado regulatorio actual, ver historial", preservando el rastro de auditoria (coherente con OBL-PRIN-03, responsabilidad demostrada, propietaria de MOD-019). Un expediente ARCO-POL o un registro del Delegado ya cerrado antes del cambio de bandera conserva las reglas vigentes en el momento de su cierre; MOD-002 y MOD-024 versionan sus propios formularios y checklists igual que versionan las reglas normativas, de modo que un nombramiento certificado bajo `ACTUAL` no se reinterpreta retroactivamente.
7. **Continuidad voluntaria del Delegado [injerto de los jueces 1 y 2, tomado de `propuesta_mapa_mvp.md` seccion 4].** Una empresa que ya nombro Delegado certificado bajo el regimen `ACTUAL` puede mantenerlo voluntariamente bajo `FUTURO`; el sistema no fuerza el cese. MOD-002 deja de exigir los pasos que la reforma volveria opcionales, pero conserva la opcion de seguir usandolos si la empresa lo decide como buena practica.

Con este diseno no existen dos modulos "Delegado (hoy)" y "Responsable interno (futuro)": existe un unico modulo (MOD-002) con un interruptor de regimen (alojado en MOD-024), coherente con el requisito explicito de la tarea de no duplicar modulos. Los tres jueces evaluaron el modelo de bandera unica de las tres propuestas como tecnicamente equivalente; los injertos de esta seccion (puntos 6 y 7) enriquecen el detalle operativo sin cambiar el principio de diseno.

---

## 6. Diagrama ASCII de dependencias

Vista de flujo principal (etapas 1 a 6), con los transversales como capa de soporte consultada por toda etapa. Las flechas indican "escribe hacia" / "es consultado por"; ninguna flecha va de un modulo transversal hacia un modulo de proceso (regla 1 de la seccion 4).

```
MOD-003 Onboarding
     |
     v
MOD-001 Organizacion  ---->  MOD-002 Delegado
     |                            |
     v                            v
MOD-004 Diagnostico  <------------+
     |
     v
MOD-005 Plan de Cumplimiento
     |
     v
MOD-006 RAT y Mapa de Datos
     |------------------+------------------+------------------+
     v                  v                  v                  v
MOD-007 Consent.   MOD-008 Docs.     MOD-009 Proveed.   MOD-014 Riesgos/EIPD
     |                  |                  |                  |
     |                  +---> MOD-016 Retencion             v
     |                  |                  |            MOD-015 Controles
     |                  v                  v                  |
     +----------->  MOD-010 Transferencias -----------------> +
                         |
                         v
MOD-011 ARCO-POL <---- MOD-012 Portal del Titular
     |
     +---> MOD-013 Incidentes de Seguridad
     |
     v
MOD-017 Capacitacion
     |
     v
MOD-018 Auditoria ---> MOD-019 Centro de Evidencias ---> MOD-020 Dashboard y Reportes
```

```
           +----------------------------------------------------------+
           |   CAPA TRANSVERSAL (consultada, nunca consulta al reves) |
           |  MOD-021 Tareas | MOD-022 Notif. | MOD-023 Calendario     |
           |  MOD-024 Regulatorio | MOD-025 Busqueda | MOD-026 Ayuda   |
           +----------------------------------------------------------+
                 ^ escriben eventos/tareas/plazos     | consultan/alertan
                 |                                    v
     MOD-001..020 (todos los modulos de las 6 etapas del recorrido)
```

---

### 6.1 Convencion de los campos depende_de y alimenta_a, y la excepcion MOD-018/MOD-019

En `mapa_modulos.json` cada modulo declara dos listas: `depende_de` (de que modulos necesita datos o servicios; es la lista usada para el diagrama de esta seccion y para el arbol ASCII de la seccion 1) y `alimenta_a` (a que modulos entrega datos). Regla de consistencia verificada mecanicamente sobre los 26 modulos: si el modulo Y aparece en el `depende_de` de X, entonces X aparece siempre en el `alimenta_a` de Y, sin excepciones. `alimenta_a` puede ademas listar destinatarios adicionales que no tienen una entrada `depende_de` reciproca explicita en el modulo consumidor (por ejemplo MOD-001, MOD-023 y MOD-024 alimentan a practicamente todos los modulos porque proveen identidad de organizacion, plazos o el estado normativo vigente, sin que cada consumidor declare esa lectura de referencia constante como una dependencia estructural propia). Esa asimetria en un solo sentido es intencional: `alimenta_a` es la lista, mas amplia por diseno, de "quien consume esto"; `depende_de` registra solo la dependencia estructural minima que ordena el recorrido y los diagramas de esta seccion.

Excepcion unica del mapa: leido como grafo de orden estricto de construccion/inicializacion, `depende_de` es aciclico en todos los modulos salvo un solo par. MOD-018 Auditoria de Cumplimiento y MOD-019 Centro de Evidencias se declaran mutuamente en su `depende_de` (MOD-018 depende_de incluye MOD-019 y MOD-019 depende_de incluye MOD-018). Esto es intencional, no un error de copia (ver seccion 4 regla 6, y el campo `notas_dependencia` de ambos modulos en `mapa_modulos.json`): MOD-018 consulta la evidencia acumulada en MOD-019 para elaborar sus hallazgos de auditoria, y el informe y los hallazgos resultantes de MOD-018 se registran a su vez como nueva evidencia en MOD-019. Es una dependencia de datos bidireccional y continua entre dos modulos semi-transversales, no una precedencia de construccion; ningun otro par de modulos del mapa tiene esta relacion reciproca.

---

## 7. Entidades conceptuales principales

Lista de entidades de dominio (sin modelo de datos, sin SQL), agrupadas por dominio funcional, con el modulo que las posee.

- **MOD-001 Organizacion y Personas**: Organization; BusinessUnit/Sucursal; User; Role.
- **MOD-002 Delegado / Responsable Interno de Datos**: ResponsableDelProgramaDeDatos (tipo_rol: DELEGADO | RESPONSABLE_INTERNO).
- **MOD-004 Diagnostico de Cumplimiento**: DiagnosticoRespuesta.
- **MOD-005 Plan de Cumplimiento**: AccionDelPlan.
- **MOD-006 RAT y Mapa de Datos**: Treatment; Purpose; LegalBasis; DataCategory; System.
- **MOD-007 Consentimiento**: Consent; ConsentWithdrawal.
- **MOD-008 Documentos y Politicas**: Document; DocumentVersion; PrivacyNotice; PrivacyPolicy.
- **MOD-009 Proveedores y Encargados**: Encargado; TerceroReceptor; Subencargado; Contrato/DPA.
- **MOD-010 Transferencias Internacionales**: Transfer.
- **MOD-011 ARCO-POL**: PrivacyRequest; IdentityVerification.
- **MOD-012 Portal del Titular**: Titular.
- **MOD-013 Incidentes de Seguridad**: Incident.
- **MOD-014 Riesgos y EIPD**: DPIA; Risk/RiskAssessment.
- **MOD-015 Controles de Seguridad**: Control.
- **MOD-016 Retencion y Eliminacion**: RetentionRule.
- **MOD-017 Capacitacion**: TrainingProgram; TrainingRecord.
- **MOD-018 Auditoria de Cumplimiento**: ComplianceAudit; AuditLog (consultado, embebido en todos los modulos).
- **MOD-019 Centro de Evidencias**: Evidence; EvidencePackage.
- **MOD-021 Centro de Tareas**: Task; Approval.
- **MOD-022 Notificaciones**: Notification.
- **MOD-023 Calendario y Motor de Plazos**: CalendarEvent/HolidayCalendar.
- **MOD-024 Centro Regulatorio**: RegulatoryInstrument; RegulatoryRuleVersion; ReformaActivationFlag; SanctionProcedure; ACEFiling.
- **MOD-026 Centro de Ayuda**: HelpArticle.

Entidad transversal adicional: **AuditLog** (registro tecnico e inmutable de acciones del sistema), embebida en todos los modulos, consultada desde MOD-018 (programa de auditoria) y MOD-019 (Centro de Evidencias); no tiene un modulo propietario unico porque cada modulo registra sus propios eventos en ella.

---

## 8. Tabla completa de cobertura: OBL-ID -> modulo propietario (105 obligaciones)

Cada obligacion tiene exactamente un modulo propietario; la columna "Colaboradores" lista otros modulos que consumen o alimentan esa obligacion por referencia, sin ser dueños de ella. IDs y agrupacion por area identicos a `matriz_obligaciones.md`. Tabla generada por transformacion mecanica (script) de la tabla equivalente de la propuesta ganadora, renumerando cada modulo (+1 a partir de MOD-002, con las 8 obligaciones DPO reasignadas de MOD-001 a MOD-002 por la elevacion del Delegado) y verificada por segundo script contra `matriz_obligaciones.json`: 105/105 IDs, sin duplicados ni huecos, cada uno con propietario unico (ver seccion 10 para el detalle de la transformacion).

### AMB (4)

| id | propietario | colaboradores |
|---|---|---|
| OBL-AMB-01 | MOD-004 | MOD-001 |
| OBL-AMB-02 | MOD-004 | - |
| OBL-AMB-03 | MOD-004 | - |
| OBL-AMB-04 | MOD-004 | - |

### PRIN (4)

| id | propietario | colaboradores |
|---|---|---|
| OBL-PRIN-01 | MOD-007 | MOD-006, MOD-005 |
| OBL-PRIN-02 | MOD-006 | MOD-007, MOD-005 |
| OBL-PRIN-03 | MOD-019 | MOD-015, MOD-018 |
| OBL-PRIN-04 | MOD-007 | MOD-011 |

### ARCO (15)

| id | propietario | colaboradores |
|---|---|---|
| OBL-ARCO-01 | MOD-011 | - |
| OBL-ARCO-02 | MOD-011 | - |
| OBL-ARCO-03 | MOD-011 | MOD-006 |
| OBL-ARCO-04 | MOD-011 | - |
| OBL-ARCO-05 | MOD-011 | MOD-010, MOD-009 |
| OBL-ARCO-06 | MOD-011 | - |
| OBL-ARCO-07 | MOD-011 | - |
| OBL-ARCO-08 | MOD-011 | MOD-023 |
| OBL-ARCO-09 | MOD-011 | MOD-023 |
| OBL-ARCO-10 | MOD-011 | MOD-023 |
| OBL-ARCO-11 | MOD-011 | MOD-010, MOD-009 |
| OBL-ARCO-12 | MOD-011 | - |
| OBL-ARCO-13 | MOD-011 | - |
| OBL-ARCO-14 | MOD-011 | MOD-024 |
| OBL-ARCO-15 | MOD-011 | MOD-012 |

### DPO (8)

| id | propietario | colaboradores |
|---|---|---|
| OBL-DPO-01 | MOD-002 | MOD-024 |
| OBL-DPO-02 | MOD-002 | MOD-023 |
| OBL-DPO-03 | MOD-002 | MOD-023 |
| OBL-DPO-04 | MOD-002 | MOD-017 |
| OBL-DPO-05 | MOD-002 | MOD-017 |
| OBL-DPO-06 | MOD-002 | MOD-008 |
| OBL-DPO-07 | MOD-002 | MOD-018 |
| OBL-DPO-08 | MOD-002 | - |

### AVISO (5)

| id | propietario | colaboradores |
|---|---|---|
| OBL-AVISO-01 | MOD-008 | - |
| OBL-AVISO-02 | MOD-008 | MOD-009 |
| OBL-AVISO-03 | MOD-008 | - |
| OBL-AVISO-04 | MOD-008 | MOD-009 |
| OBL-AVISO-05 | MOD-008 | - |

### CONS (6)

| id | propietario | colaboradores |
|---|---|---|
| OBL-CONS-01 | MOD-007 | - |
| OBL-CONS-02 | MOD-007 | - |
| OBL-CONS-03 | MOD-007 | MOD-009 |
| OBL-CONS-04 | MOD-007 | - |
| OBL-CONS-05 | MOD-007 | MOD-019 |
| OBL-CONS-06 | MOD-007 | MOD-011 |

### SENS (8)

| id | propietario | colaboradores |
|---|---|---|
| OBL-SENS-01 | MOD-006 | MOD-007 |
| OBL-SENS-02 | MOD-007 | - |
| OBL-SENS-03 | MOD-007 | MOD-006 |
| OBL-SENS-04 | MOD-006 | MOD-007, MOD-014 |
| OBL-SENS-05 | MOD-015 | MOD-006 |
| OBL-SENS-06 | MOD-006 | MOD-007, MOD-014 |
| OBL-SENS-07 | MOD-007 | - |
| OBL-SENS-08 | MOD-006 | MOD-008, MOD-014 |

### TRAT (3)

| id | propietario | colaboradores |
|---|---|---|
| OBL-TRAT-01 | MOD-006 | MOD-007 |
| OBL-TRAT-02 | MOD-007 | MOD-006 |
| OBL-TRAT-03 | MOD-006 | - |

### PROV (7)

| id | propietario | colaboradores |
|---|---|---|
| OBL-PROV-01 | MOD-009 | - |
| OBL-PROV-02 | MOD-009 | - |
| OBL-PROV-03 | MOD-009 | MOD-015 |
| OBL-PROV-04 | MOD-009 | MOD-008 |
| OBL-PROV-05 | MOD-009 | - |
| OBL-PROV-06 | MOD-009 | MOD-008 |
| OBL-PROV-07 | MOD-009 | MOD-016 |

### TRANSF (6)

| id | propietario | colaboradores |
|---|---|---|
| OBL-TRANSF-01 | MOD-010 | - |
| OBL-TRANSF-02 | MOD-010 | MOD-009 |
| OBL-TRANSF-03 | MOD-010 | - |
| OBL-TRANSF-04 | MOD-010 | MOD-007 |
| OBL-TRANSF-05 | MOD-010 | MOD-024 |
| OBL-TRANSF-06 | MOD-010 | MOD-019 |

### SEG (6)

| id | propietario | colaboradores |
|---|---|---|
| OBL-SEG-01 | MOD-015 | MOD-024 |
| OBL-SEG-02 | MOD-015 | MOD-006, MOD-014, MOD-017, MOD-018 |
| OBL-SEG-03 | MOD-015 | - |
| OBL-SEG-04 | MOD-015 | MOD-010 |
| OBL-SEG-05 | MOD-015 | MOD-016 |
| OBL-SEG-06 | MOD-015 | MOD-024 |

### DOC (4)

| id | propietario | colaboradores |
|---|---|---|
| OBL-DOC-01 | MOD-008 | MOD-011 |
| OBL-DOC-02 | MOD-006 | - |
| OBL-DOC-03 | MOD-014 | - |
| OBL-DOC-04 | MOD-012 | MOD-011 |

### INC (5)

| id | propietario | colaboradores |
|---|---|---|
| OBL-INC-01 | MOD-013 | MOD-021, MOD-023 |
| OBL-INC-02 | MOD-013 | MOD-023 |
| OBL-INC-03 | MOD-013 | - |
| OBL-INC-04 | MOD-013 | MOD-019 |
| OBL-INC-05 | MOD-013 | MOD-024 |

### CAP (2)

| id | propietario | colaboradores |
|---|---|---|
| OBL-CAP-01 | MOD-017 | - |
| OBL-CAP-02 | MOD-017 | MOD-002 |

### AUD (2)

| id | propietario | colaboradores |
|---|---|---|
| OBL-AUD-01 | MOD-018 | - |
| OBL-AUD-02 | MOD-024 | MOD-018 |

### SANC (9)

| id | propietario | colaboradores |
|---|---|---|
| OBL-SANC-01 | MOD-024 | - |
| OBL-SANC-02 | MOD-024 | - |
| OBL-SANC-03 | MOD-024 | MOD-021 |
| OBL-SANC-04 | MOD-024 | - |
| OBL-SANC-05 | MOD-024 | MOD-021, MOD-023 |
| OBL-SANC-06 | MOD-024 | MOD-021 |
| OBL-SANC-07 | MOD-024 | MOD-016, MOD-019 |
| OBL-SANC-08 | MOD-024 | - |
| OBL-SANC-09 | MOD-024 | MOD-011 |

### PLAZO (5)

| id | propietario | colaboradores |
|---|---|---|
| OBL-PLAZO-01 | MOD-023 | MOD-021 |
| OBL-PLAZO-02 | MOD-023 | - |
| OBL-PLAZO-03 | MOD-005 | MOD-004 |
| OBL-PLAZO-04 | MOD-012 | MOD-011 |
| OBL-PLAZO-05 | MOD-024 | MOD-002 |

### RET (6)

| id | propietario | colaboradores |
|---|---|---|
| OBL-RET-01 | MOD-016 | MOD-008 |
| OBL-RET-02 | MOD-016 | MOD-008 |
| OBL-RET-03 | MOD-016 | MOD-008 |
| OBL-RET-04 | MOD-016 | MOD-008 |
| OBL-RET-05 | MOD-016 | MOD-019, MOD-011, MOD-013 |
| OBL-RET-06 | MOD-016 | MOD-008 |

**Verificacion de completitud:** 4 (AMB) + 4 (PRIN) + 15 (ARCO) + 8 (DPO) + 5 (AVISO) + 6 (CONS) + 8 (SENS) + 3 (TRAT) + 7 (PROV) + 6 (TRANSF) + 6 (SEG) + 4 (DOC) + 5 (INC) + 2 (CAP) + 2 (AUD) + 9 (SANC) + 5 (PLAZO) + 6 (RET) = 105. Coincide con el total verificado de `matriz_obligaciones.json` (105 IDs unicos, confirmado por script).

---

## 9. Tabla de cobertura: 29 areas del prompt -> modulo

| Area del prompt | Modulo | Tipo de asignacion |
|---|---|---|
| 8.1 Configuracion de empresa | MOD-001 | Propia |
| 8.2 Usuarios, roles y permisos | MOD-001 | Propia (submodulo) |
| 8.3 Onboarding | MOD-003 | Propia |
| 9 Diagnostico | MOD-004 | Propia |
| 10 Plan de cumplimiento | MOD-005 | Propia |
| 11 RAT | MOD-006 | Propia |
| 12 Mapa de datos | MOD-006 | Funcion transversal del modulo (vista sobre el RAT) |
| 13 ARCO-POL | MOD-011 | Propia |
| 14 Centro de tareas | MOD-021 | Propia (transversal) |
| 15 Documentos y politicas | MOD-008 | Propia |
| 16 Consentimiento | MOD-007 | Propia |
| 17 Proveedores | MOD-009 | Propia |
| 18 Transferencias internacionales | MOD-010 | Propia |
| 19 Incidentes | MOD-013 | Propia |
| 20 EIPD/Riesgos | MOD-014 | Propia |
| 21 Controles de seguridad | MOD-015 | Propia |
| 22 Retencion | MOD-016 | Propia |
| 23 Capacitacion | MOD-017 | Propia |
| 24 Auditoria | MOD-018 | Propia (programa sustantivo); el registro tecnico (AuditLog) es funcion transversal embebida en todos los modulos |
| 25 Centro de evidencias | MOD-019 | Propia (semi-transversal, ver seccion 4) |
| 26 Dashboard | MOD-020 | Propia |
| 27 Notificaciones | MOD-022 | Propia (transversal) |
| 28 Reportes | MOD-020 | Propia (submodulo de Dashboard y Reportes) |
| 29 Busqueda global | MOD-025 | Propia (transversal) |
| 30 Calendario central | MOD-023 | Propia (transversal) |
| 31 Centro regulatorio | MOD-024 | Propia (transversal, no binario: ver seccion 12) |
| 32 Actualizaciones normativas | MOD-024 | Funcion transversal del modulo (no modulo aparte) |
| 33 Portal del titular | MOD-012 | Propia |
| 34 Centro de ayuda | MOD-026 | Propia (transversal) |

Verificacion: 29 filas cubren las 29 areas del prompt (8.1/8.2/8.3 cuentan como 3, mas 9 a 34 = 26; total 29). 27 se asignan como modulo propio y 2 (Mapa de datos, Actualizaciones normativas) se declaran explicitamente como funcion transversal de un modulo ya asignado, igual que en la propuesta ganadora original.

---

## 10. Que se fusiono, dividio, elimino y por que

### 10.1 Respecto al documento maestro (`PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md`)

Heredado sin cambios de la propuesta ganadora (`propuesta_mapa_recorrido.md`); el detalle completo esta en el campo "Decision respecto al documento maestro" de cada ficha (seccion 3). Resumen:

| Fusiones | Divisiones | Nuevo (sin equivalente en el maestro) | Eliminado / redefinido |
|---|---|---|---|
| Inventario de datos + RAT -> MOD-006. Usuarios y roles + Organizacion -> MOD-001. Proveedores + Contratos/DPA -> MOD-009. Motor regulatorio + Actualizacion normativa -> MOD-024. Dashboard + Reportes -> MOD-020. | Onboarding (sec. 15) -> MOD-003 (alta) + MOD-004 (diagnostico). Auditoria y trazabilidad (sec. 29) -> MOD-018 (programa sustantivo) + AuditLog (funcion transversal embebida). Retencion (sec. 21) -> dos motores dentro de MOD-016 (titular / documental propio). | MOD-002 Delegado (hallazgo estructural, decision 2.7.7). MOD-005 Plan de Cumplimiento. MOD-021 Notificaciones. MOD-023 Calendario y Motor de Plazos. MOD-024 Procedimiento Sancionador y Tramites ACE. MOD-025 Busqueda Global. MOD-026 Centro de Ayuda. | Mapa de datos deja de ser modulo aparte (pasa a vista de MOD-006). "Motor regulatorio" y "Actualizacion normativa" dejan de tratarse como arquitectura tecnica y pasan a modulo funcional (MOD-024). |

### 10.2 Respecto a las tres propuestas de validacion (este mapa vs. `propuesta_mapa_recorrido.md`, `_obligaciones.md`, `_mvp.md`)

Este mapa parte integramente de la estructura de 6 etapas + 6 transversales de `propuesta_mapa_recorrido.md` (25 modulos originales) y le injerta 8 cambios recomendados por los tres jueces, tomados de las otras dos propuestas. Ningun modulo de la propuesta ganadora se elimino; uno se dividio (elevacion del Delegado).

| # | Cambio | Tipo | Tomado de | Recomendado por | Efecto en el mapa |
|---|---|---|---|---|---|
| 1 | Delegado / Responsable Interno de Datos deja de ser submodulo de MOD-001 y se eleva a modulo propio (MOD-002) | Division | `propuesta_mapa_mvp.md` (su MOD-003) | Juez 1 (idea 4) y Juez 2 (idea 4) | 25 -> 26 modulos; las 8 obligaciones DPO cambian de propietario (MOD-001 -> MOD-002) |
| 2 | Etapa OPERAR se subdivide en 3 grupos tematicos (Relacion con el titular / Riesgo y seguridad / Ciclo de vida y personas) en vez de una lista plana de 7 modulos | Reorganizacion visual, sin cambio de modulos | `propuesta_mapa_obligaciones.md` (clusters D, E, F), adaptado a la composicion real de la etapa Operar de recorrido | Juez 2 (idea 1) | Arbol ASCII (seccion 1) y nota de navegacion actualizados |
| 3 | Test explicito de tres condiciones para MVP, aplicado a cada modulo SHOULD/COULD HAVE con su mecanismo de cobertura parcial documentado | Criterio de clasificacion + contenido nuevo en cada ficha | `propuesta_mapa_mvp.md` (introduccion y fichas de sus MOD-016/017/018/019/020) | Juez 1 (idea 1) y Juez 2 (idea 3) | Fichas de MOD-010, MOD-012, MOD-014, MOD-016, MOD-018 y el submodulo Procedimiento Sancionador de MOD-024 (seccion 3) |
| 4 | Preservacion de historial ("no aplica bajo el estado regulatorio actual, ver historial") en vez de borrar tareas al cambiar la bandera de la reforma 659; continuidad voluntaria del Delegado | Regla de negocio nueva | `propuesta_mapa_mvp.md` (seccion 4, puntos 2 y 5) | Juez 1 (idea 2) | Seccion 5, puntos 6 y 7 |
| 5 | Tabla "que aportaria si faltara / quien lo consume" para los 6 modulos transversales | Documentacion nueva | `propuesta_mapa_mvp.md` (seccion 3) | Juez 1 (idea 3) | Seccion 4 de este documento |
| 6 | Riesgo de posible subutilizacion de MOD-024 (mezcla marco normativo + doble estado + procedimiento sancionador) declarado explicitamente, con exigencia de separacion visual en la UI | Riesgo documentado + regla de UX | `propuesta_mapa_obligaciones.md` (su riesgo 4 sobre MOD-REG) | Juez 1 (idea 4) y Juez 2 (idea 5) | Ficha de MOD-024 (seccion 3) y riesgo 3 de la seccion 11 |
| 7 | Distincion explicita, citada por codigo, entre los 7 modulos transversales que el prompt nombra y los que este mapa agrega por su propio criterio de diseno (Dashboard/Reportes, Busqueda, Usuarios/roles) | Aclaracion documentada | `propuesta_mapa_obligaciones.md` (seccion 3) | Juez 1 (idea 5) | Seccion 4, primer parrafo |
| 8 | Regla de "direccion unica" entre modulos de proceso (no solo hacia los transversales) hecha explicita, y perspectiva Legal/Delegado del Dashboard puede filtrar por los 8 clusters legales de la propuesta obligacion-primero | Aclaracion + funcionalidad nueva en ficha existente | `propuesta_mapa_obligaciones.md` (seccion 3 y arbol de clusters A-H) | Juez 3 (ideas 3 y 5) | Seccion 4 regla 7; ficha de MOD-020 (seccion 3) |

Ideas de los jueces evaluadas y **no injertadas**, con la razon:
- Elevar MOD-USR/Usuarios-roles o MOD-CAL/Calendario a modulos con obligaciones propias mas amplias (sugerido implicitamente al discutir el riesgo 2 de `propuesta_mapa_obligaciones.md`): no se injerta porque la propuesta ganadora ya declara MOD-023 Calendario con sus 2 obligaciones propias (OBL-PLAZO-01/02) sin ambigüedad, y Usuarios/roles (submodulo de MOD-001) no posee ninguna obligacion propia en ninguna de las tres propuestas.
- Separar Onboarding del Diagnostico en un tercer nivel de sub-flujo adicional (mencionado en `propuesta_mapa_obligaciones.md`): no se injerta porque la propuesta ganadora ya los separa como dos modulos de primer nivel (MOD-003 y MOD-004), un nivel de separacion mayor al de las otras dos propuestas.
- Renombrar el criterio de capas de construccion (Capa 0 a 5 de `propuesta_mapa_mvp.md`) como estructura primaria por encima de las 6 etapas: no se injerta como estructura visible porque el propio juez 3 lo propone como capa interna "montada sobre" el recorrido, no como reemplazo; el orden de dependencia real ya queda expresado en la numeracion secuencial MOD-001 a MOD-026 (que sigue, en la practica, el mismo orden de capas) y en el diagrama de la seccion 6.

---

## 11. Riesgos del mapa definitivo

1. **Sobrecarga de navegacion por numero de modulos.** 26 modulos de primer nivel (uno mas que la propuesta ganadora original), aunque agrupados en 6 etapas y OPERAR subdividida en 3 grupos tematicos, pueden abrumar a un usuario no especialista si la UI los expone como lista plana. Mitigacion: la agrupacion en 6 etapas colapsables, con OPERAR en 3 sub-grupos, mas una barra transversal fija, debe ser un requisito de UX vinculante [opinion de producto].
2. **Activacion indebida del doble estado de la reforma 659.** Si la bandera de MOD-024 se activa por error o antes de confirmar la publicacion oficial, 17 obligaciones cambiarian de exigibilidad de forma incorrecta para todos los clientes simultaneamente. Mitigacion: el cambio de bandera debe requerir una accion administrativa explicita y auditable, nunca un job automatico por fecha (seccion 5, punto 2).
3. **MOD-024 Centro Regulatorio mezcla contenido informativo con flujo operativo, con riesgo de subutilizacion del Procedimiento Sancionador [riesgo injertado de `propuesta_mapa_obligaciones.md`, ver seccion 10.2 fila 6].** Aloja a la vez informacion de referencia (marco normativo), el interruptor del doble estado y un procedimiento con plazos reales y consecuencias economicas (Procedimiento Sancionador). Si la UI no los separa claramente, un usuario podria confundir "estoy leyendo sobre sanciones" con "tengo un procedimiento sancionador abierto"; y si pocos clientes enfrentan realmente un caso de la ACE, esa capacidad especifica queda subutilizada dentro de un modulo mas grande. Se mantuvo unido porque las tres capacidades comparten la misma relacion (interaccion formal con la ACE) y dividirlas incrementaria el numero de modulos sin una obligacion adicional que lo justifique.
4. **Volumen de AuditLog como entidad transversal embebida.** Al registrarse desde todos los modulos, el registro tecnico de auditoria puede crecer rapido; esta fase de analisis funcional no resuelve su arquitectura de almacenamiento, pero el mapa ya asume que MOD-018/MOD-019 deben poder consultarlo y exportarlo con integridad verificable, lo que debe validarse en la fase de arquitectura tecnica.
5. **Clasificacion MVP con muchos MUST HAVE (20 de 26) puede exceder un "producto minimo vendible".** La urgencia real (obligaciones OBLIGATORIO con plazo ya vencido) justifica una lista amplia, pero esta clasificacion es de producto, no legal; el test de tres condiciones (seccion 2, principio 7) documenta la razon de cada inclusion, pero debe validarse contra capacidad real de desarrollo y contra el estudio de disposicion a pagar que `02_validacion_de_la_idea.md` 2.3.4 deja pendiente [opinion de producto].
6. **MOD-002 (Delegado) es, tras su elevacion, un modulo casi transversal aunque se clasifica como modulo de proceso [clasificacion no binaria, injerto del juez 3 desde `propuesta_mapa_obligaciones.md`].** MOD-011 ARCO-POL, MOD-007 Consentimiento, MOD-017 Capacitacion y MOD-024 Centro Regulatorio consultan "quien es hoy el responsable del tramite" en MOD-002 de forma constante, mas parecido al patron de consulta de un modulo transversal que al de un modulo de proceso ordinario. Se mantiene en la etapa Empezar (no en la barra transversal) porque, a diferencia de Tareas o Calendario, si posee 8 obligaciones propias completas y un ciclo de vida propio (nombramiento, reverificacion, cese) que un usuario debe completar una sola vez al inicio del recorrido.
7. **Dejar Transferencias (MOD-010), Portal (MOD-012), Riesgos/EIPD (MOD-014), Retencion (MOD-016) y Auditoria (MOD-018) en SHOULD HAVE puede exponer a empresas con datos sensibles desde el dia uno.** Si una empresa cliente usa biometria o hace videovigilancia desde su primer diagnostico, el modulo completo de EIPD aun no estaria disponible en el MVP. Mitigacion ya incorporada: cada uno de estos 5 modulos declara su mecanismo de cobertura parcial en su ficha (seccion 3), injertado de `propuesta_mapa_mvp.md` por recomendacion de los jueces 1 y 2.
8. **RAT (MOD-006) como nucleo unico concentra demasiados campos si no se separan bien las vistas.** Fusionar Inventario, RAT y Catalogo de sistemas en un solo modulo reduce duplicacion, pero si las tres vistas no se disenan como pantallas claramente distintas, el modulo puede volverse un formulario unico sobrecargado, contrario al principio de minima carga cognitiva.
9. **Incertidumbres juridicas heredadas por multiples modulos.** Las incertidumbres documentadas en `03_hallazgos_regulatorios.md` seccion 9 (computo de 72 horas, aplicabilidad del Art. 82 LPA al sector privado, transferencia vs. encargado extranjero, edad de consentimiento de NNA, numero exacto del Decreto 659) atraviesan varios modulos (MOD-013, MOD-023, MOD-010, MOD-007, MOD-024). Mitigacion: el criterio conservador por defecto y su etiqueta de incertidumbre visible deben definirse una sola vez (en MOD-023 y MOD-024 segun corresponda) y heredarse, nunca reimplementarse por modulo.

---

## 12. Resumen de los veredictos de los jueces

Tres jueces independientes puntuaron las tres propuestas (`propuesta_mapa_obligaciones.md`, `propuesta_mapa_recorrido.md`, `propuesta_mapa_mvp.md`) en 5 criterios (cobertura, simplicidad, MVP realista, dependencias, extensibilidad, sobre 50 puntos totales).

| Juez | Obligacion-primero | Recorrido | MVP-primero | Ganador de este juez |
|---|---|---|---|---|
| Juez 1 | 38.0 | 44.5 | 39.5 | Recorrido |
| Juez 2 | 36.5 | 41.0 | 36.5 | Recorrido |
| Juez 3 | 34.0 | 39.0 | 40.0 | MVP-primero |
| **Total agregado** | **108.5** | **124.5** | **116.0** | **Recorrido** |

**Ganadora por mayoria (2 de 3 jueces) y por puntaje agregado: `propuesta_mapa_recorrido.md`.** Los jueces 1 y 2 la eligen explicitamente por su angulo de navegacion (6 etapas que responden "por donde empiezo"), su MVP mas ajustado en numero absoluto (15/25 modulos MUST HAVE en la propuesta original) y su tratamiento mas detallado del doble estado de la reforma 659 (tarea de revision de avisos en vez de reescritura automatica). El juez 3, aunque prefiere `propuesta_mapa_mvp.md` por su disciplina de MVP mas rigurosa (criterio de tres condiciones y patron de cobertura parcial explicito por modulo diferido), reconoce a recorrido como segunda opcion muy cercana (39.0 vs 40.0) y recomienda montar la capa de navegacion de recorrido SOBRE la estructura de capas de mvp, no reemplazarla.

Razones principales citadas por cada juez para elegir recorrido (jueces 1 y 2):
- Unica propuesta organizada explicitamente como recorrido de 6 etapas (EMPEZAR -> DIAGNOSTICAR -> PLANIFICAR -> REGISTRAR -> OPERAR -> DEMOSTRAR) que responde de forma directa a la pregunta "por donde empiezo" de un usuario no especialista.
- Unica que impone, como requisito de UX vinculante, agrupar los modulos en grupos colapsables por etapa mas una barra transversal fija, en vez de una lista plana.
- Cobertura completa e identica en rigor a las otras dos (105/105 obligaciones, 29/29 areas del prompt).
- MVP mas ajustado en numero absoluto de las tres propuestas originales (15 de 25 MUST HAVE).
- Es la unica que cita y usa realmente `03_hallazgos_regulatorios.md` en las secciones que la tarea senalo como mas utiles (3, 5, 6, 8, 9, 11), resolviendo explicitamente la ambiguedad de la seccion 8 punto 4 (aviso de privacidad tras la reforma 659) con una tarea en vez de sobrescribir documentos.

Debilidades de recorrido senaladas por los jueces, y como se resolvieron en este mapa definitivo:
| Debilidad senalada | Juez(es) | Resolucion en este mapa |
|---|---|---|
| El Delegado queda enterrado como submodulo de tercer nivel dentro de MOD-001, pese a ser el hallazgo estructural mas importante de la validacion | Jueces 1 y 2 | Elevado a MOD-002, modulo de primer nivel (fila 1 de la tabla de injertos, seccion 10.2) |
| Sin patron de cobertura parcial explicito para los modulos SHOULD HAVE | Jueces 1 y 2 | Cada modulo SHOULD/COULD HAVE declara su cobertura parcial en su ficha (seccion 3) |
| Sin criterio explicito y verificable de que hace a un modulo MUST HAVE | Jueces 1 y 2 | Test de tres condiciones adoptado como principio de organizacion (seccion 2, punto 7) |
| La etapa OPERAR agrupa 7 modulos heterogeneos sin subdivision interna | Juez 2 | OPERAR subdividida en 3 grupos tematicos (seccion 1) |
| MOD-024 (antes MOD-023) mezcla contenido informativo con flujo operativo real, sin separacion visual exigida | Jueces 1 y 2 | Exigencia de separacion visual anadida a la ficha de MOD-024 y al riesgo 3 (seccion 11) |
| Sin tratamiento de preservacion de historial ni continuidad voluntaria del Delegado al cambiar de regimen | Juez 1 | Incorporado en la seccion 5, puntos 6 y 7 |

Razones del juez 3 para preferir `propuesta_mapa_mvp.md` (no adoptadas como estructura primaria, pero si sus ideas de fondo, ver seccion 10.2):
- Test de disciplina de MVP mas riguroso y explicito de las tres propuestas (tres condiciones objetivas).
- Documenta una cobertura parcial concreta para cada modulo diferido a V1.
- Separa Delegado y Catalogo de sistemas como modulos propios de primer nivel, dando mayor visibilidad al hallazgo estructural mas importante de la validacion.

Estas tres razones del juez 3 quedan incorporadas en este mapa definitivo: la primera y la segunda mediante el test de tres condiciones y las fichas de cobertura parcial (principio 7, seccion 2); la tercera mediante la elevacion de MOD-002 Delegado (que ademas coincide con la recomendacion explicita de los jueces 1 y 2). El catalogo de sistemas no se eleva a modulo propio: se mantiene como submodulo de MOD-006 RAT, porque ningun juez lo senala como hallazgo estructural comparable al del Delegado, y separarlo anadiria un modulo sin una obligacion propia que lo justifique.

---

## 13. Nota final

Este mapa definitivo es una propuesta de diseño funcional [opinion de producto en su estructura, clasificacion MVP e injertos de los jueces], construida sobre las 105 obligaciones verificadas de `matriz_obligaciones.json` (verificacion automatica: 105/105 IDs unicos, cada uno con propietario unico, ver seccion 8) y sobre la propuesta ganadora de la validacion de tres jueces (`propuesta_mapa_recorrido.md`), enriquecida con 8 injertos explicitos recomendados por esos mismos jueces desde las otras dos propuestas (seccion 10.2). Ninguna asignacion de modulo reinterpreta un articulo de la ley; donde una obligacion depende de una incertidumbre juridica genuina (seccion 9 de `03_hallazgos_regulatorios.md`), el modulo propietario hereda esa incertidumbre y debe mostrarla, no resolverla. La ficha completa de cada modulo (formato A-Q de `00_plantilla_ficha_modulo.md`) es un entregable posterior, fuera del alcance de este mapa.

Archivo de datos estructurados equivalente: `mapa_modulos.json` (26 modulos, mismos campos que esta tabla mas dependencias, entidades y notas de la reforma 659 en formato maquina).