# Blueprint funcional PRIV-SV - indice

Plataforma SaaS B2B de autogestion de proteccion de datos personales para empresas de El Salvador. Fase: analisis funcional (sin codigo ni arquitectura tecnica). Fecha: 2026-09-24.

Documento completo en un solo archivo: [BLUEPRINT_FUNCIONAL_PRIV-SV.md](BLUEPRINT_FUNCIONAL_PRIV-SV.md) (unos 3,4 MB; GitHub no lo muestra en pantalla por su tamano, se lee descargandolo o en un editor Markdown). Las mismas secciones, navegables una por una:

| Seccion | Titulo | Archivo(s) fuente |
|---|---|---|
| 1 | Resumen ejecutivo | [01_resumen_ejecutivo.md](../04_secciones/01_resumen_ejecutivo.md) |
| 2 | Validacion de la idea | [02_validacion_de_la_idea.md](../02_validacion/02_validacion_de_la_idea.md) |
| 3 | Hallazgos regulatorios | [03_hallazgos_regulatorios.md](../01_legal/03_hallazgos_regulatorios.md) |
| 4 | Objetivo exacto del producto | [04_objetivo_exacto_del_producto.md](../02_validacion/04_objetivo_exacto_del_producto.md) |
| 5 | Tipos de usuario | [05_tipos_de_usuario.md](../02_validacion/05_tipos_de_usuario.md) |
| 6 | Mapa definitivo de modulos | [06_mapa_definitivo_de_modulos.md](../02_validacion/06_mapa_definitivo_de_modulos.md) |
| 7 | Explicacion de cada modulo (26 fichas) | [03_modulos/](../03_modulos/) |
| 8 | Workflows end-to-end (11 casos) | [08a_workflows_casos_01_03.md](../04_secciones/08a_workflows_casos_01_03.md), [08b_workflows_casos_04_06.md](../04_secciones/08b_workflows_casos_04_06.md), [08c_workflows_casos_07_08.md](../04_secciones/08c_workflows_casos_07_08.md), [08d_workflows_casos_09_11.md](../04_secciones/08d_workflows_casos_09_11.md) |
| 9 | Modelo conceptual de informacion | [09_modelo_conceptual.md](../04_secciones/09_modelo_conceptual.md) |
| 10 | Dependencias entre modulos | [10_dependencias_entre_modulos.md](../04_secciones/10_dependencias_entre_modulos.md) |
| 11 | Sistema de roles y permisos | [11_roles_y_permisos.md](../04_secciones/11_roles_y_permisos.md) |
| 12 | Sistema de tareas y alertas | [12_tareas_y_alertas.md](../04_secciones/12_tareas_y_alertas.md) |
| 13 | Sistema de evidencia y auditoria | [13_evidencia_y_auditoria.md](../04_secciones/13_evidencia_y_auditoria.md) |
| 14 | Dashboard y reportes | [14_dashboard_y_reportes.md](../04_secciones/14_dashboard_y_reportes.md) |
| 15 | Propuesta de onboarding | [15_onboarding.md](../04_secciones/15_onboarding.md) |
| 16-18 | Funcionalidades obligatorias por ley, recomendadas y opcionales | [16_18_funcionalidades_por_origen.md](../04_secciones/16_18_funcionalidades_por_origen.md) |
| 19-21 | MVP, V1 y V2 / Enterprise | [19_21_roadmap_mvp_v1_v2.md](../04_secciones/19_21_roadmap_mvp_v1_v2.md) |
| 22 | Funcionalidades que NO deben construirse | [22_anti_features.md](../02_validacion/22_anti_features.md) |
| 23 | Riesgos del producto | [23_riesgos_del_producto.md](../04_secciones/23_riesgos_del_producto.md) |
| 24 | Preguntas pendientes | [24_preguntas_pendientes.md](../04_secciones/24_preguntas_pendientes.md) |
| 25 | Recomendacion de siguiente etapa | [25_siguiente_etapa.md](../04_secciones/25_siguiente_etapa.md) |

## Fichas de modulo (seccion 7)

| Codigo | Modulo | Etapa | MVP |
|---|---|---|---|
| [MOD-001](../03_modulos/MOD-001_ficha.md) | Organizacion y Personas | Empezar | MUST HAVE |
| [MOD-002](../03_modulos/MOD-002_ficha.md) | Delegado / Responsable Interno de Datos | Empezar | MUST HAVE |
| [MOD-003](../03_modulos/MOD-003_ficha.md) | Onboarding | Empezar | MUST HAVE |
| [MOD-004](../03_modulos/MOD-004_ficha.md) | Diagnostico de Cumplimiento | Diagnosticar | MUST HAVE |
| [MOD-005](../03_modulos/MOD-005_ficha.md) | Plan de Cumplimiento | Planificar | MUST HAVE |
| [MOD-006](../03_modulos/MOD-006_ficha.md) | RAT y Mapa de Datos | Registrar | MUST HAVE |
| [MOD-007](../03_modulos/MOD-007_ficha.md) | Consentimiento | Registrar | MUST HAVE |
| [MOD-008](../03_modulos/MOD-008_ficha.md) | Documentos y Politicas | Registrar | MUST HAVE |
| [MOD-009](../03_modulos/MOD-009_ficha.md) | Proveedores y Encargados | Registrar | MUST HAVE |
| [MOD-010](../03_modulos/MOD-010_ficha.md) | Transferencias Internacionales | Registrar | SHOULD HAVE |
| [MOD-011](../03_modulos/MOD-011_ficha.md) | ARCO-POL | Operar | MUST HAVE |
| [MOD-012](../03_modulos/MOD-012_ficha.md) | Portal del Titular | Operar | SHOULD HAVE |
| [MOD-013](../03_modulos/MOD-013_ficha.md) | Incidentes de Seguridad | Operar | MUST HAVE |
| [MOD-014](../03_modulos/MOD-014_ficha.md) | Riesgos y EIPD | Operar | SHOULD HAVE |
| [MOD-015](../03_modulos/MOD-015_ficha.md) | Controles de Seguridad | Operar | MUST HAVE |
| [MOD-016](../03_modulos/MOD-016_ficha.md) | Retencion y Eliminacion | Operar | SHOULD HAVE |
| [MOD-017](../03_modulos/MOD-017_ficha.md) | Capacitacion | Operar | MUST HAVE |
| [MOD-018](../03_modulos/MOD-018_ficha.md) | Auditoria de Cumplimiento | Demostrar | SHOULD HAVE |
| [MOD-019](../03_modulos/MOD-019_ficha.md) | Centro de Evidencias | Demostrar | MUST HAVE |
| [MOD-020](../03_modulos/MOD-020_ficha.md) | Dashboard y Reportes | Demostrar | MUST HAVE |
| [MOD-021](../03_modulos/MOD-021_ficha.md) | Centro de Tareas | Transversal | MUST HAVE |
| [MOD-022](../03_modulos/MOD-022_ficha.md) | Notificaciones | Transversal | MUST HAVE |
| [MOD-023](../03_modulos/MOD-023_ficha.md) | Calendario y Motor de Plazos | Transversal | MUST HAVE |
| [MOD-024](../03_modulos/MOD-024_ficha.md) | Centro Regulatorio | Transversal | MUST HAVE |
| [MOD-025](../03_modulos/MOD-025_ficha.md) | Busqueda Global | Transversal | COULD HAVE |
| [MOD-026](../03_modulos/MOD-026_ficha.md) | Centro de Ayuda | Transversal | MUST HAVE |

## Anexos

- [Anexo A. Control de calidad de la fase 3](anexo_control_de_calidad.md): revision adversarial de las fichas y critica de coherencia global con el resultado de cada correccion.
- Anexo B. Archivos fuente y huella SHA-256: al final de [BLUEPRINT_FUNCIONAL_PRIV-SV.md](BLUEPRINT_FUNCIONAL_PRIV-SV.md).
- Matriz de obligaciones (105 obligaciones canonicas): [matriz_obligaciones.md](../01_legal/matriz_obligaciones.md) y [matriz_obligaciones.json](../01_legal/matriz_obligaciones.json).
