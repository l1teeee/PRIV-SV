# Backlog del MVP y plan de sprints - PRIV-SV

Fecha: 2026-09-24. Historias de usuario (HU) del MVP derivadas del blueprint funcional (`analisis/05_blueprint/`), con criterios de aceptacion verificables, estimacion en puntos, dependencias y asignacion a sprints.

## Resumen

| Indicador | Valor |
|---|---|
| Epicas | 21 |
| Historias de usuario | 316 |
| Puntos totales | 1322 (R1 749, R2 573) |
| Sprints de desarrollo (velocidad base 40) | 36, mas el Sprint 0 |
| R1 nucleo vendible | fin del Sprint 21 (2027-08-06) |
| R2 MVP completo | fin del Sprint 36 (2028-03-03) |

## Archivos

- [plan_de_sprints.md](plan_de_sprints.md): supuestos, releases, sensibilidad a la velocidad y contenido de cada sprint.
- [contenido_y_validacion_legal.md](contenido_y_validacion_legal.md): contenido legal y de ayuda que cada HU necesita, y HU que requieren validacion de abogado.
- [backlog_mvp.csv](backlog_mvp.csv): todas las HU en una tabla importable (Jira, Azure DevOps, Linear, Trello, hojas de calculo).
- [backlog_mvp.json](backlog_mvp.json): la misma informacion en formato estructurado.
- Carpeta [epicas/](epicas/): una ficha por epica con sus HU completas.

## Epicas

| Epica | Modulo | Release principal | HU | Puntos | Archivo |
|---|---|---|---|---|---|
| EP-000 Plataforma y requisitos transversales | - | R1 | 19 | 74 | [EP-000_plataforma_y_requisitos_transversales.md](epicas/EP-000_plataforma_y_requisitos_transversales.md) |
| EP-001 Organizacion y Personas | MOD-001 | R1 | 14 | 47 | [EP-001_organizacion_y_personas.md](epicas/EP-001_organizacion_y_personas.md) |
| EP-002 Delegado / Responsable Interno de Datos | MOD-002 | R1 | 17 | 76 | [EP-002_delegado_responsable_interno_de_datos.md](epicas/EP-002_delegado_responsable_interno_de_datos.md) |
| EP-003 Onboarding | MOD-003 | R1 | 12 | 45 | [EP-003_onboarding.md](epicas/EP-003_onboarding.md) |
| EP-004 Diagnostico de Cumplimiento | MOD-004 | R1 | 13 | 58 | [EP-004_diagnostico_de_cumplimiento.md](epicas/EP-004_diagnostico_de_cumplimiento.md) |
| EP-005 Plan de Cumplimiento | MOD-005 | R1 | 13 | 62 | [EP-005_plan_de_cumplimiento.md](epicas/EP-005_plan_de_cumplimiento.md) |
| EP-006 RAT y Mapa de Datos | MOD-006 | R1 | 20 | 82 | [EP-006_rat_y_mapa_de_datos.md](epicas/EP-006_rat_y_mapa_de_datos.md) |
| EP-007 Consentimiento | MOD-007 | R2 | 13 | 60 | [EP-007_consentimiento.md](epicas/EP-007_consentimiento.md) |
| EP-008 Documentos y Politicas | MOD-008 | R1 | 18 | 62 | [EP-008_documentos_y_politicas.md](epicas/EP-008_documentos_y_politicas.md) |
| EP-009 Proveedores y Encargados | MOD-009 | R2 | 14 | 67 | [EP-009_proveedores_y_encargados.md](epicas/EP-009_proveedores_y_encargados.md) |
| EP-011 ARCO-POL | MOD-011 | R2 | 20 | 104 | [EP-011_arco_pol.md](epicas/EP-011_arco_pol.md) |
| EP-013 Incidentes de Seguridad | MOD-013 | R2 | 19 | 96 | [EP-013_incidentes_de_seguridad.md](epicas/EP-013_incidentes_de_seguridad.md) |
| EP-015 Controles de Seguridad | MOD-015 | R2 | 14 | 51 | [EP-015_controles_de_seguridad.md](epicas/EP-015_controles_de_seguridad.md) |
| EP-017 Capacitacion | MOD-017 | R2 | 15 | 56 | [EP-017_capacitacion.md](epicas/EP-017_capacitacion.md) |
| EP-019 Centro de Evidencias | MOD-019 | R2 | 14 | 61 | [EP-019_centro_de_evidencias.md](epicas/EP-019_centro_de_evidencias.md) |
| EP-020 Dashboard y Reportes | MOD-020 | R2 | 9 | 41 | [EP-020_dashboard_y_reportes.md](epicas/EP-020_dashboard_y_reportes.md) |
| EP-021 Centro de Tareas | MOD-021 | R1 | 16 | 61 | [EP-021_centro_de_tareas.md](epicas/EP-021_centro_de_tareas.md) |
| EP-022 Notificaciones | MOD-022 | R1 | 14 | 54 | [EP-022_notificaciones.md](epicas/EP-022_notificaciones.md) |
| EP-023 Calendario y Motor de Plazos | MOD-023 | R1 | 11 | 54 | [EP-023_calendario_y_motor_de_plazos.md](epicas/EP-023_calendario_y_motor_de_plazos.md) |
| EP-024 Centro Regulatorio | MOD-024 | R1 | 21 | 79 | [EP-024_centro_regulatorio.md](epicas/EP-024_centro_regulatorio.md) |
| EP-026 Centro de Ayuda | MOD-026 | R1 | 10 | 32 | [EP-026_centro_de_ayuda.md](epicas/EP-026_centro_de_ayuda.md) |

## Como leer una historia de usuario

- **Formato**: "Como <rol>, quiero <capacidad>, para <beneficio u obligacion>". Los roles son los 12 roles estandar del blueprint (seccion 5.3) mas los roles internos del proveedor del software (seccion 11.7).
- **Criterios de aceptacion**: de 3 a 8 por historia, en formato "Dado ..., cuando ..., entonces ...". Son la base de las pruebas de QA y de la demo del sprint.
- **Fundamento**: IDs canonicos de `analisis/01_legal/matriz_obligaciones.json` (formato OBL-AREA-NN) cuando la historia atiende una obligacion legal. La ley obliga a la empresa cliente, no al software: el fundamento indica que obligacion ayuda a atender o demostrar la historia.
- **Referencia**: seccion de la ficha funcional (`analisis/03_modulos/MOD-XXX_ficha.md`) de donde sale la historia; ante cualquier duda de detalle (campos, validaciones, textos de ayuda), manda la ficha.
- **Habilitadora**: historia que otros modulos necesitan (por ejemplo el motor de plazos o la bitacora); se prioriza antes que sus consumidores.

## Estimacion

Puntos de historia en escala Fibonacci. Son relativos: sirven para planificar y se recalibran con la velocidad real de los primeros sprints.

| Puntos | Referencia |
|---|---|
| 1 | Ajuste menor: un campo, un texto, una regla de validacion aislada |
| 2 | Alta, edicion y listado simple de una entidad sin flujo de estados; o una alerta simple |
| 3 | Formulario con varias reglas; listado con filtros; o una automatizacion simple (evento -> tarea) |
| 5 | Flujo con estados, transiciones, permisos por rol e historial; o un calculo con reglas |
| 8 | Flujo complejo: varias ramas, plazos legales calculados, integracion con 3 o mas modulos, o documento con plantilla y aprobacion |

Las estimaciones no incluyen redactar el contenido legal o de ayuda (plantillas, textos, catalogos): ese trabajo esta en `contenido_y_validacion_legal.md` y lo hace el equipo legal y de contenido en paralelo.

## Releases

- **R1 Nucleo vendible** (seccion 19.8 del blueprint): plataforma, organizacion y usuarios, Delegado, onboarding, diagnostico, plan de cumplimiento, RAT, documentos y la infraestructura transversal (tareas, notificaciones, plazos, centro regulatorio y los esqueletos de evidencias y ayuda). Permite vender el diagnostico, el plan con plazos y los documentos base.
- **R2 MVP completo**: consentimiento, proveedores, ARCO-POL, incidentes, controles, capacitacion, evidencias completas, dashboard y ayuda completa. Es el alcance que cumple los criterios de salida a mercado de la seccion 19.6.

## Definicion de listo (para entrar a un sprint)

- La historia tiene criterios de aceptacion verificables y referencia a su ficha.
- Sus dependencias estan terminadas o planificadas antes en el mismo sprint.
- El diseno de pantalla (prototipo) del recorrido esta aprobado por el Product Owner.
- Si requiere contenido o validacion legal, el insumo esta disponible o tiene fecha comprometida antes del cierre del sprint.

## Definicion de terminado

- Cumple todos sus criterios de aceptacion, probados por QA.
- Respeta los permisos de la ficha (incluida la separacion de funciones) y registra sus eventos en la bitacora (AuditLog) cuando corresponde.
- Los textos de pantalla estan en lenguaje sencillo, con su ayuda contextual y sin expresiones de "cumplimiento legal" ni porcentajes de cumplimiento.
- No guarda datos personales que la ficha o las anti-features prohiben.
- Los plazos legales se obtienen del motor de plazos (MOD-023), las tareas se crean en el Centro de Tareas (MOD-021) y los avisos internos los envia Notificaciones (MOD-022).
- Demostrada en la revision del sprint.

## Importar el backlog en una herramienta

`backlog_mvp.csv` esta en UTF-8, con todas las celdas entre comillas y saltos de linea dentro de las celdas de criterios. Mapeo sugerido:

| Columna del CSV | Jira | Azure DevOps | Linear |
|---|---|---|---|
| Titulo | Summary | Title | Title |
| Historia + Criterios de aceptacion | Description | Description + Acceptance Criteria | Description |
| Epica | Epic Link o Parent | Parent (Feature) | Project o Parent |
| Puntos | Story Points | Story Points | Estimate |
| Sprint | Sprint | Iteration | Cycle |
| Release | Fix Version | Tag | Label |
| Depende de (HU) | Link "is blocked by" | Predecessor | Blocked by |
