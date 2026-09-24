# Plan de sprints del MVP - PRIV-SV

Fecha: 2026-09-24. Plan generado a partir del backlog (`backlog_mvp.json`) respetando las dependencias entre historias y modulos, la secuencia de construccion de la seccion 19.9 del blueprint y la capacidad de cada sprint. Las fechas son tentativas: se recalculan con la velocidad real del equipo.

## 1. Supuestos

| Supuesto | Valor |
|---|---|
| Duracion del sprint | 2 semanas (10 dias habiles) |
| Inicio del Sprint 0 | 2026-10-05 |
| Velocidad base | 40 puntos por sprint completo |
| Rampa de arranque | Sprint 1 al 60%, Sprint 2 al 80%, desde el Sprint 3 al 100% |
| Asuetos descontados | 2026-11-02, 2026-12-24, 2026-12-25, 2026-12-31, 2027-01-01, 2027-03-25, 2027-03-26, 2027-05-10, 2027-06-17, 2027-08-03, 2027-08-04, 2027-08-05, 2027-08-06, 2027-09-15, 2027-11-02, 2027-12-24, 2027-12-31 |
| Equipo de referencia | EQUIPO POR DEFINIR |

## 2. Releases e hitos

| Release | Contenido | Ultimo sprint | Fecha estimada |
|---|---|---|---|
| R1 | Nucleo vendible (seccion 19.8): plataforma, organizacion, Delegado, onboarding, diagnostico, plan, RAT, documentos e infraestructura transversal | Sprint 21 | 2027-08-06 |
| R2 | MVP completo: consentimiento, proveedores, ARCO-POL, incidentes, controles, capacitacion, evidencias completas, dashboard y ayuda completa | Sprint 36 | 2028-03-03 |

## 3. Sensibilidad a la velocidad del equipo

| Velocidad (puntos por sprint) | Sprints totales | R1 listo al final del sprint | Fecha R1 | R2 listo al final del sprint | Fecha R2 |
|---|---|---|---|---|---|
| 30 | 47 | 28 | 2027-11-12 | 47 | 2028-08-04 |
| 40 | 36 | 21 | 2027-08-06 | 36 | 2028-03-03 |
| 50 | 29 | 17 | 2027-06-11 | 29 | 2027-11-26 |
| 60 | 25 | 14 | 2027-04-30 | 25 | 2027-10-01 |
| 80 | 19 | 11 | 2027-03-19 | 19 | 2027-07-09 |

## 4. Sprint 0 (preparacion, sin historias de desarrollo)

PENDIENTE DE REDACCION

## 5. Sprints

### Sprint 1 (2026-10-19 a 2026-10-30)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 24 puntos. Comprometido: 24 puntos en 4 historias. Epicas: EP-000 Plataforma y requisitos transversales (16 pts); EP-001 Organizacion y Personas (8 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-000-01 | Aislar los datos entre organizaciones clientes | EP-000 | 8 | R1 |
| HU-001-01 | Registrar y mantener los datos basicos de la organizacion | EP-001 | 5 | R1 |
| HU-000-02 | Registrar cada accion relevante en la bitacora de auditoria | EP-000 | 8 | R1 |
| HU-001-02 | Gestionar las sucursales de la organizacion | EP-001 | 3 | R1 |

### Sprint 2 (2026-11-02 a 2026-11-13)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 28 puntos (descuenta asuetos: 2026-11-02). Comprometido: 28 puntos en 7 historias. Epicas: EP-001 Organizacion y Personas (20 pts); EP-000 Plataforma y requisitos transversales (8 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-001-03 | Gestionar el catalogo de unidades o departamentos | EP-001 | 3 | R1 |
| HU-000-04 | Generar huella de integridad y manifiesto al exportar | EP-000 | 5 | R1 |
| HU-001-04 | Consultar el catalogo de los 12 roles estandar | EP-001 | 2 | R1 |
| HU-000-06 | Iniciar sesion con credenciales propias | EP-000 | 3 | R1 |
| HU-001-05 | Invitar usuarios y gestionar el ciclo de la invitacion | EP-001 | 5 | R1 |
| HU-001-08 | Editar los datos y el rol de un usuario | EP-001 | 5 | R1 |
| HU-001-06 | Suspender y reactivar usuarios | EP-001 | 5 | R1 |

### Sprint 3 (2026-11-16 a 2026-11-27)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 40 puntos en 12 historias. Epicas: EP-001 Organizacion y Personas (19 pts); EP-022 Notificaciones (13 pts); EP-021 Centro de Tareas (3 pts); EP-023 Calendario y Motor de Plazos (5 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-001-07 | Dar de baja usuarios con reemplazo de rol critico | EP-001 | 5 | R1 |
| HU-001-09 | Actualizar el contacto ARCO-POL derivado al cambiar su titular | EP-001 | 3 | R1 |
| HU-022-01 | Configurar la regla de notificacion por familia de evento | EP-022 | 5 | R1 |
| HU-022-02 | Generar notificacion desde un evento de tarea o aprobacion de MOD-021 | EP-022 | 5 | R1 |
| HU-022-03 | Generar notificacion desde un evento de plazo directo de MOD-023 | EP-022 | 3 | R1 |
| HU-001-10 | Alertar y registrar la decision sobre el umbral de separacion de funciones | EP-001 | 3 | R1 |
| HU-001-11 | Alertar cuando ningun usuario activo tiene un rol critico | EP-001 | 2 | R1 |
| HU-001-12 | Alertar sobre estructura sin actualizar y registrar la revision de accesos | EP-001 | 2 | R1 |
| HU-021-01 | Generar automaticamente una tarea desde un evento de otro modulo | EP-021 | 3 | R1 |
| HU-001-13 | Crear una tarea de revision al declarar operacion fuera de El Salvador | EP-001 | 2 | R1 |
| HU-001-14 | Exportar el listado de usuarios y roles vigentes | EP-001 | 2 | R1 |
| HU-023-04 | Calcular el vencimiento de las 72 horas en horas corridas | EP-023 | 5 | R1 |

### Sprint 4 (2026-11-30 a 2026-12-11)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 40 puntos en 8 historias. Epicas: EP-023 Calendario y Motor de Plazos (38 pts); EP-005 Plan de Cumplimiento (2 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-023-01 | Mantener y publicar el calendario anual de asuetos nacionales y ad hoc | EP-023 | 8 | R1 |
| HU-023-02 | Calcular una fecha limite en dias habiles | EP-023 | 8 | R1 |
| HU-023-03 | Ver el desglose verificable de un calculo de plazo | EP-023 | 3 | R1 |
| HU-023-05 | Calcular una fecha de vencimiento periodica de fecha a fecha | EP-023 | 3 | R1 |
| HU-023-06 | Suspender y reanudar un calculo de plazo por causal declarada | EP-023 | 5 | R1 |
| HU-023-07 | Aplicar una prorroga a un plazo abierto | EP-023 | 3 | R1 |
| HU-023-08 | Recalcular y notificar un plazo abierto cuando se agrega un asueto ad hoc | EP-023 | 8 | R1 |
| HU-005-02 | Configurar los parametros de generacion del plan de cumplimiento | EP-005 | 2 | R1 |

### Sprint 5 (2026-12-14 a 2026-12-25)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 32 puntos (descuenta asuetos: 2026-12-24, 2026-12-25). Comprometido: 32 puntos en 10 historias. Epicas: EP-023 Calendario y Motor de Plazos (11 pts); EP-003 Onboarding (3 pts); EP-004 Diagnostico de Cumplimiento (3 pts); EP-021 Centro de Tareas (14 pts); EP-000 Plataforma y requisitos transversales (1 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-023-09 | Alertar cuando el calendario del proximo anio no esta cargado | EP-023 | 3 | R1 |
| HU-023-10 | Ver la vista de calendario central | EP-023 | 5 | R1 |
| HU-003-01 | Iniciar la sesion guiada de configuracion inicial | EP-003 | 3 | R1 |
| HU-004-01 | Iniciar una sesion de diagnostico de cumplimiento | EP-004 | 3 | R1 |
| HU-023-11 | Generar el recordatorio de la auditoria anual mientras el modulo de Auditoria no este activo | EP-023 | 3 | R1 |
| HU-021-02 | Crear manualmente una tarea en el Centro de Tareas | EP-021 | 3 | R1 |
| HU-021-03 | Avanzar una tarea por sus estados basicos | EP-021 | 5 | R1 |
| HU-021-04 | Consultar la bandeja de tareas propia por persona | EP-021 | 3 | R1 |
| HU-021-05 | Adjuntar y gestionar evidencia de una tarea | EP-021 | 3 | R1 |
| HU-000-10 | Mostrar el descargo legal del sistema | EP-000 | 1 | R1 |

### Sprint 6 (2026-12-28 a 2027-01-08)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 32 puntos (descuenta asuetos: 2026-12-31, 2027-01-01). Comprometido: 32 puntos en 9 historias. Epicas: EP-021 Centro de Tareas (31 pts); EP-000 Plataforma y requisitos transversales (1 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-021-06 | Registrar comentarios en la bitacora de una tarea | EP-021 | 2 | R1 |
| HU-021-07 | Mostrar la fecha limite calculada por el motor de plazos con su desglose | EP-021 | 5 | R1 |
| HU-021-08 | Marcar automaticamente una tarea como vencida | EP-021 | 3 | R1 |
| HU-021-09 | Enviar una tarea a revision y generar la Aprobacion correspondiente | EP-021 | 5 | R1 |
| HU-021-10 | Resolver una Aprobacion con bloqueo de autorrevision | EP-021 | 5 | R1 |
| HU-021-11 | Emitir alertas de tarea proxima a vencer y tarea vencida | EP-021 | 3 | R1 |
| HU-021-12 | Escalar automaticamente la alerta critica de 72 horas | EP-021 | 5 | R1 |
| HU-021-14 | Exportar el listado de tareas | EP-021 | 3 | R1 |
| HU-000-19 | Usar el sistema en espanol | EP-000 | 1 | R1 |

### Sprint 7 (2027-01-11 a 2027-01-22)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 40 puntos en 10 historias. Epicas: EP-021 Centro de Tareas (8 pts); EP-022 Notificaciones (29 pts); EP-006 RAT y Mapa de Datos (3 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-021-13 | Mantener el historial inmutable de la tarea y la aprobacion | EP-021 | 5 | R1 |
| HU-021-15 | Alojar la tarea generica de cobertura parcial del Diagnostico | EP-021 | 3 | R1 |
| HU-022-04 | Bloquear la desactivacion del piso minimo de alertas de plazos legales | EP-022 | 3 | R1 |
| HU-022-05 | Subir automaticamente el nivel de urgencia de una notificacion activa | EP-022 | 5 | R1 |
| HU-022-06 | Escalar automaticamente una notificacion sin respuesta dentro del umbral | EP-022 | 5 | R1 |
| HU-022-07 | Ajustar con doble control el umbral de escalamiento de una alerta CRITICAL en curso | EP-022 | 3 | R1 |
| HU-022-08 | Exigir acuse de recibo explicito para notificaciones CRITICAL | EP-022 | 5 | R1 |
| HU-022-09 | Mantener el historial inmutable de cada notificacion | EP-022 | 3 | R1 |
| HU-022-10 | Reintentar el envio fallido por canal externo y alertar el agotamiento | EP-022 | 5 | R1 |
| HU-006-01 | Crear ficha de tratamiento en Borrador | EP-006 | 3 | R1 |

### Sprint 8 (2027-01-25 a 2027-02-05)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 40 puntos en 10 historias. Epicas: EP-006 RAT y Mapa de Datos (37 pts); EP-015 Controles de Seguridad (3 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-006-02 | Completar los campos de Borrador y enviar la ficha a revision | EP-006 | 5 | R1 |
| HU-006-04 | Seleccionar la base de licitud del tratamiento con su justificacion | EP-006 | 5 | R1 |
| HU-006-05 | Registrar el origen del dato y el analisis de fuente de acceso publico | EP-006 | 3 | R1 |
| HU-006-06 | Dar de alta un sistema en el Catalogo de Sistemas | EP-006 | 5 | R1 |
| HU-006-07 | Vincular el tratamiento a uno o mas sistemas del catalogo | EP-006 | 3 | R1 |
| HU-006-08 | Completar la descripcion, el responsable interno y la transferencia internacional | EP-006 | 3 | R1 |
| HU-006-09 | Registrar el plazo de conservacion del tratamiento | EP-006 | 2 | R1 |
| HU-006-10 | Aprobar una ficha de tratamiento y pasarla a Vigente | EP-006 | 8 | R1 |
| HU-006-19 | Vincular los encargados del tratamiento a la ficha | EP-006 | 3 | R2 |
| HU-015-01 | Crear un control de seguridad en el catalogo | EP-015 | 3 | R2 |

### Sprint 9 (2027-02-08 a 2027-02-19)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 40 puntos en 12 historias. Epicas: EP-006 RAT y Mapa de Datos (5 pts); EP-022 Notificaciones (6 pts); EP-003 Onboarding (8 pts); EP-024 Centro Regulatorio (3 pts); EP-002 Delegado / Responsable Interno de Datos (16 pts); EP-004 Diagnostico de Cumplimiento (2 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-006-20 | Vincular controles de seguridad y bloquear el paso a Vigente sin control en dato sensible | EP-006 | 5 | R2 |
| HU-022-11 | Bloquear datos personales en el cuerpo del mensaje externo | EP-022 | 3 | R1 |
| HU-022-12 | Exportar el listado de notificaciones en XLSX o CSV | EP-022 | 3 | R1 |
| HU-003-02 | Completar los datos basicos de la organizacion | EP-003 | 3 | R1 |
| HU-003-03 | Registrar al primer usuario Administrador de la organizacion | EP-003 | 2 | R1 |
| HU-003-04 | Invitar usuarios adicionales con su rol propuesto | EP-003 | 3 | R1 |
| HU-024-03 | Exponer el estado del regimen normativo a otros modulos | EP-024 | 3 | R1 |
| HU-002-01 | Registrar el nombramiento inicial del responsable del programa de datos | EP-002 | 3 | R1 |
| HU-002-02 | Completar el checklist de perfil y avanzar el nombramiento a pendiente de aceptacion | EP-002 | 5 | R1 |
| HU-002-03 | Aceptar el cargo mediante la declaracion jurada de conflicto de intereses | EP-002 | 5 | R1 |
| HU-002-04 | Registrar la notificacion interna del nombramiento dentro del plazo legal | EP-002 | 3 | R1 |
| HU-004-09 | Archivar manualmente una sesion de diagnostico | EP-004 | 2 | R1 |

### Sprint 10 (2027-02-22 a 2027-03-05)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 40 puntos en 8 historias. Epicas: EP-002 Delegado / Responsable Interno de Datos (21 pts); EP-003 Onboarding (19 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-002-05 | Preparar y registrar la comunicacion del nombramiento a la ACE | EP-002 | 8 | R1 |
| HU-002-07 | Activar el registro tras recibir la credencial o agotarse el plazo de emision | EP-002 | 3 | R1 |
| HU-002-15 | Reaccionar automaticamente cuando cambia el regimen normativo de la reforma 659 | EP-002 | 5 | R1 |
| HU-002-16 | Decidir con doble control si mantener al Delegado de forma voluntaria o migrar a Responsable Interno | EP-002 | 5 | R1 |
| HU-003-05 | Responder si la organizacion ya tiene o va a designar un Delegado, y sembrar su registro | EP-003 | 5 | R1 |
| HU-003-06 | Registrar que la empresa no esta segura sobre el Delegado y crear la tarea critica de seguimiento | EP-003 | 3 | R1 |
| HU-003-07 | Aceptar el descargo de responsabilidad y confirmar la finalizacion de la configuracion inicial | EP-003 | 8 | R1 |
| HU-003-08 | Crear automaticamente la tarea de iniciar el Diagnostico y redirigir a MOD-004 | EP-003 | 3 | R1 |

### Sprint 11 (2027-03-08 a 2027-03-19)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 39 puntos en 9 historias. Epicas: EP-003 Onboarding (15 pts); EP-002 Delegado / Responsable Interno de Datos (24 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-003-09 | Guardar automaticamente el avance y reanudar la configuracion inicial tras un periodo de inactividad | EP-003 | 5 | R1 |
| HU-003-10 | Consultar el historial de la configuracion inicial | EP-003 | 2 | R1 |
| HU-003-11 | Exportar el resumen de configuracion inicial y el historial de invitaciones | EP-003 | 3 | R1 |
| HU-003-12 | Gestionar el estado de las invitaciones enviadas | EP-003 | 5 | R1 |
| HU-002-06 | Registrar el rechazo de inscripcion de la ACE y reabrir el nombramiento | EP-002 | 5 | R1 |
| HU-002-08 | Editar los datos de contacto o modalidad de un registro activo | EP-002 | 3 | R1 |
| HU-002-09 | Reverificar el perfil del responsable cada tres anos | EP-002 | 8 | R1 |
| HU-002-10 | Registrar la capacitacion anual del propio responsable | EP-002 | 3 | R1 |
| HU-002-12 | Registrar el cese y disparar la designacion de sustituto en 10 dias habiles | EP-002 | 5 | R1 |

### Sprint 12 (2027-03-22 a 2027-04-02)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 32 puntos (descuenta asuetos: 2027-03-25, 2027-03-26). Comprometido: 32 puntos en 7 historias. Epicas: EP-002 Delegado / Responsable Interno de Datos (13 pts); EP-004 Diagnostico de Cumplimiento (16 pts); EP-008 Documentos y Politicas (3 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-002-13 | Vigilar el plazo de 10 dias habiles para designar sustituto tras el cese | EP-002 | 5 | R1 |
| HU-002-14 | Mantener la clausula y el contador de confidencialidad post-cese de 5 anos | EP-002 | 5 | R1 |
| HU-002-17 | Exportar el expediente y la bitacora de plazos del responsable del programa de datos | EP-002 | 3 | R1 |
| HU-004-02 | Responder las preguntas de un bloque respetando sus dependencias | EP-004 | 8 | R1 |
| HU-004-03 | Guardar el avance del cuestionario y continuar despues | EP-004 | 3 | R1 |
| HU-004-04 | Detectar posibles exclusiones del Art. 3 y exigir confirmacion humana | EP-004 | 5 | R1 |
| HU-008-01 | Configurar el catalogo de tipos de documento y la cadena de aprobacion por tipo | EP-008 | 3 | R1 |

### Sprint 13 (2027-04-05 a 2027-04-16)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 40 puntos en 9 historias. Epicas: EP-004 Diagnostico de Cumplimiento (10 pts); EP-008 Documentos y Politicas (25 pts); EP-019 Centro de Evidencias (5 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-004-05 | Calcular y mostrar el resultado del diagnostico | EP-004 | 5 | R1 |
| HU-004-06 | Cerrar la sesion de diagnostico con confirmacion simple o doble control | EP-004 | 5 | R1 |
| HU-008-02 | Crear y editar el borrador de un documento a partir de la plantilla de su tipo | EP-008 | 3 | R1 |
| HU-008-05 | Enviar un documento a revision y registrar su rechazo con motivo | EP-008 | 5 | R1 |
| HU-008-18 | Proveer la plantilla generica de Evaluacion de Impacto (EIPD) en el catalogo de documentos | EP-008 | 2 | R1 |
| HU-019-01 | Recibir automaticamente evidencia generada por otros modulos | EP-019 | 5 | R1 |
| HU-008-06 | Aprobar un documento en revision segun la cadena configurada | EP-008 | 5 | R1 |
| HU-008-07 | Publicar la version aprobada de un documento | EP-008 | 8 | R1 |
| HU-008-14 | Adjuntar evidencia de publicacion de un documento | EP-008 | 2 | R1 |

### Sprint 14 (2027-04-19 a 2027-04-30)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 40 puntos en 10 historias. Epicas: EP-008 Documentos y Politicas (10 pts); EP-004 Diagnostico de Cumplimiento (27 pts); EP-006 RAT y Mapa de Datos (3 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-008-08 | Archivar un documento descontinuado con doble aprobacion cuando aplica | EP-008 | 5 | R1 |
| HU-008-09 | Iniciar una nueva version de un documento que requiere revision | EP-008 | 3 | R1 |
| HU-008-15 | Exportar la version vigente de un documento a PDF | EP-008 | 2 | R1 |
| HU-004-07 | Generar tratamientos, tareas, documentos y riesgos sugeridos al cerrar la sesion | EP-004 | 8 | R1 |
| HU-004-08 | Iniciar un re-diagnostico y archivar la sesion anterior | EP-004 | 5 | R1 |
| HU-004-10 | Consultar en solo lectura el resultado y el historial de sesiones cerradas | EP-004 | 3 | R1 |
| HU-004-11 | Alertar sobre el ciclo de vida de la sesion de diagnostico | EP-004 | 5 | R1 |
| HU-004-12 | Crear tarea manual para documentar una transferencia internacional detectada | EP-004 | 3 | R1 |
| HU-004-13 | Crear tarea de elaborar EIPD con plantilla generica cuando se detecta biometria, salud, menores o camaras | EP-004 | 3 | R1 |
| HU-006-03 | Marcar automaticamente como sensible una categoria de dato del catalogo cerrado | EP-006 | 3 | R1 |

### Sprint 15 (2027-05-03 a 2027-05-14)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 36 puntos (descuenta asuetos: 2027-05-10). Comprometido: 36 puntos en 9 historias. Epicas: EP-005 Plan de Cumplimiento (34 pts); EP-006 RAT y Mapa de Datos (2 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-005-01 | Generar automaticamente la primera version del plan al cerrar el diagnostico | EP-005 | 5 | R1 |
| HU-005-03 | Calcular el nivel de prioridad de cada accion y permitir su reclasificacion manual justificada | EP-005 | 5 | R1 |
| HU-005-04 | Asignar el responsable y calcular la fecha limite de cada accion del plan | EP-005 | 5 | R1 |
| HU-005-05 | Consultar el plan de cumplimiento agrupado por prioridad y filtrable | EP-005 | 3 | R1 |
| HU-005-06 | Enviar una version del plan a revision | EP-005 | 3 | R1 |
| HU-005-07 | Aprobar o rechazar una version del plan como Vigente | EP-005 | 8 | R1 |
| HU-005-08 | Archivar manualmente una version del plan | EP-005 | 2 | R1 |
| HU-005-09 | Crear automaticamente una tarea por cada accion pendiente al aprobar el plan | EP-005 | 3 | R1 |
| HU-006-14 | Eliminar definitivamente una ficha en Borrador | EP-006 | 2 | R1 |

### Sprint 16 (2027-05-17 a 2027-05-28)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 40 puntos en 8 historias. Epicas: EP-005 Plan de Cumplimiento (26 pts); EP-006 RAT y Mapa de Datos (14 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-005-10 | Avanzar el estado de una accion entre Pendiente, En curso, Completada y Vencida | EP-005 | 8 | R1 |
| HU-005-11 | Descartar una accion como no aplica con justificacion y validacion reforzada | EP-005 | 5 | R1 |
| HU-005-12 | Recalcular manualmente el plan bajo demanda | EP-005 | 8 | R1 |
| HU-005-13 | Exportar el plan con verificacion de integridad | EP-005 | 5 | R1 |
| HU-006-11 | Rechazar una ficha en revision y devolverla a Borrador | EP-006 | 3 | R1 |
| HU-006-12 | Pasar una ficha Vigente a Requiere revision y confirmarla o actualizarla | EP-006 | 5 | R1 |
| HU-006-13 | Archivar y reactivar un tratamiento | EP-006 | 3 | R1 |
| HU-006-18 | Consultar el Mapa de Datos como vista tabular del RAT | EP-006 | 3 | R1 |

### Sprint 17 (2027-05-31 a 2027-06-11)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 39 puntos en 10 historias. Epicas: EP-006 RAT y Mapa de Datos (18 pts); EP-008 Documentos y Politicas (21 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-006-15 | Crear una ficha desde la biblioteca de tratamientos plantilla | EP-006 | 5 | R1 |
| HU-006-16 | Crear automaticamente una ficha desde una respuesta del Diagnostico | EP-006 | 5 | R1 |
| HU-006-17 | Exportar el RAT consolidado y el paquete de evidencia con verificacion de integridad | EP-006 | 8 | R1 |
| HU-008-03 | Completar el checklist de los nueve literales del Art. 24 en el Aviso de Privacidad | EP-008 | 3 | R1 |
| HU-008-04 | Completar el checklist de los cinco elementos del Art. 7 en la Politica de Privacidad y el Aviso de Privacidad | EP-008 | 2 | R1 |
| HU-008-10 | Pasar el Aviso de Privacidad vigente a Requiere revision cuando el RAT registra una finalidad nueva | EP-008 | 3 | R1 |
| HU-008-11 | Pasar un documento vigente a Requiere revision al vencer su intervalo de revision periodica | EP-008 | 5 | R1 |
| HU-008-12 | Alertar cuando no exista un Aviso de Privacidad publicado pese a tratamientos activos | EP-008 | 2 | R1 |
| HU-008-13 | Crear una tarea de revision de avisos publicados cuando cambia el regimen de la reforma 659 | EP-008 | 3 | R1 |
| HU-008-16 | Consultar el inventario de documentos regulatorios y el historial de versiones | EP-008 | 3 | R1 |

### Sprint 18 (2027-06-14 a 2027-06-25)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 36 puntos (descuenta asuetos: 2027-06-17). Comprometido: 35 puntos en 9 historias. Epicas: EP-008 Documentos y Politicas (3 pts); EP-024 Centro Regulatorio (32 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-008-17 | Invitar a un asesor externo a comentar un documento especifico en revision | EP-008 | 3 | R1 |
| HU-024-01 | Mantener el marco normativo con versionado | EP-024 | 5 | R1 |
| HU-024-02 | Consultar el marco normativo vigente | EP-024 | 3 | R1 |
| HU-024-04 | Activar el regimen FUTURO de la reforma 659 | EP-024 | 8 | R1 |
| HU-024-05 | Revertir el regimen a ACTUAL | EP-024 | 5 | R1 |
| HU-024-06 | Notificar y confirmar el cambio de regimen normativo | EP-024 | 3 | R1 |
| HU-024-07 | Generar tarea de revision ante un cambio normativo | EP-024 | 3 | R1 |
| HU-024-08 | Mantener el catalogo de infracciones y multas | EP-024 | 3 | R1 |
| HU-024-09 | Consultar el catalogo de infracciones y multas | EP-024 | 2 | R1 |

### Sprint 19 (2027-06-28 a 2027-07-09)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 40 puntos en 13 historias. Epicas: EP-024 Centro Regulatorio (17 pts); EP-019 Centro de Evidencias (16 pts); EP-026 Centro de Ayuda (5 pts); EP-000 Plataforma y requisitos transversales (2 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-024-10 | Recibir automaticamente el tramite de nombramiento del Delegado | EP-024 | 3 | R1 |
| HU-024-11 | Crear manualmente un tramite ante la ACE | EP-024 | 2 | R1 |
| HU-024-12 | Completar un tramite ante la ACE para su envio | EP-024 | 3 | R1 |
| HU-024-13 | Aprobar y enviar un tramite ante la ACE | EP-024 | 3 | R1 |
| HU-024-14 | Registrar el acuse o rechazo de un tramite ante la ACE | EP-024 | 3 | R1 |
| HU-024-15 | Consultar y exportar el registro de tramites ante la ACE | EP-024 | 3 | R1 |
| HU-019-02 | Detectar automaticamente un hueco de evidencia | EP-019 | 3 | R1 |
| HU-019-03 | Consultar el catalogo de evidencia por obligacion | EP-019 | 5 | R1 |
| HU-019-04 | Cargar evidencia suelta manualmente | EP-019 | 3 | R1 |
| HU-019-05 | Aprobar o rechazar evidencia cargada manualmente | EP-019 | 5 | R1 |
| HU-026-01 | Crear y editar un articulo de ayuda en borrador | EP-026 | 3 | R1 |
| HU-026-02 | Enviar o reenviar un articulo de ayuda a revision legal | EP-026 | 2 | R1 |
| HU-000-13 | Consultar el aviso de privacidad del producto | EP-000 | 2 | R1 |

### Sprint 20 (2027-07-12 a 2027-07-23)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 39 puntos en 12 historias. Epicas: EP-026 Centro de Ayuda (27 pts); EP-020 Dashboard y Reportes (3 pts); EP-000 Plataforma y requisitos transversales (9 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-026-03 | Revisar legalmente un articulo y aprobarlo o rechazarlo | EP-026 | 5 | R1 |
| HU-026-04 | Vincular un articulo publicado a los campos y pantallas del sistema | EP-026 | 3 | R1 |
| HU-026-05 | Mostrar la tarjeta de ayuda contextual de 4 partes | EP-026 | 5 | R1 |
| HU-026-06 | Consultar el Glosario buscable basico | EP-026 | 3 | R1 |
| HU-026-07 | Mostrar el descargo estandar en cada articulo y en el Glosario | EP-026 | 1 | R1 |
| HU-026-08 | Consultar el historial de version y de revision legal de un articulo | EP-026 | 3 | R1 |
| HU-026-09 | Marcar manualmente un articulo publicado para revision | EP-026 | 5 | R1 |
| HU-026-10 | Archivar un articulo marcado para revision cuyo concepto ya no aplica | EP-026 | 2 | R1 |
| HU-020-01 | Mostrar un panel inicial de pendientes del plan y de tareas | EP-020 | 3 | R1 |
| HU-000-03 | Consultar la bitacora de auditoria | EP-000 | 3 | R1 |
| HU-000-05 | Aprovisionar una organizacion cliente nueva | EP-000 | 3 | R1 |
| HU-000-07 | Recuperar el acceso cuando se olvida la contrasena | EP-000 | 3 | R1 |

### Sprint 21 (2027-07-26 a 2027-08-06)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 24 puntos (descuenta asuetos: 2027-08-03, 2027-08-04, 2027-08-05, 2027-08-06). Comprometido: 24 puntos en 7 historias. Epicas: EP-000 Plataforma y requisitos transversales (24 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-000-08 | Exigir doble factor de autenticacion en roles sensibles | EP-000 | 5 | R1 |
| HU-000-09 | Cerrar la sesion automaticamente por inactividad | EP-000 | 3 | R1 |
| HU-000-11 | Aceptar los terminos de uso | EP-000 | 3 | R1 |
| HU-000-12 | Aceptar el contrato de encargo de tratamiento | EP-000 | 3 | R1 |
| HU-000-14 | Autorizar un acceso temporal de soporte | EP-000 | 3 | R1 |
| HU-000-15 | Usar el acceso temporal de soporte autorizado | EP-000 | 5 | R1 |
| HU-000-18 | Ver fechas y horas en el huso horario de El Salvador | EP-000 | 2 | R1 |

### Sprint 22 (2027-08-09 a 2027-08-20)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 39 puntos en 9 historias. Epicas: EP-009 Proveedores y Encargados (34 pts); EP-007 Consentimiento (5 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-009-01 | Dar de alta y editar los datos generales de un Encargado, Tercero-Receptor o Subencargado | EP-009 | 3 | R2 |
| HU-009-02 | Listar y consultar la ficha de proveedores con filtros y visibilidad segun el rol | EP-009 | 3 | R2 |
| HU-009-03 | Vincular tratamientos del RAT y pais, y enviar el proveedor a evaluacion | EP-009 | 5 | R2 |
| HU-009-04 | Registrar la evaluacion de riesgo y seguridad, y aprobarla o rechazarla | EP-009 | 5 | R2 |
| HU-009-05 | Vincular el Contrato/DPA y aprobar la activacion del proveedor con doble control | EP-009 | 8 | R2 |
| HU-009-06 | Registrar los datos de contacto del Encargado para el aviso de privacidad | EP-009 | 2 | R2 |
| HU-009-07 | Recibir alertas y tareas de vencimiento del Contrato/DPA | EP-009 | 3 | R2 |
| HU-009-08 | Ejecutar la revision periodica programada de un proveedor | EP-009 | 5 | R2 |
| HU-007-01 | Registrar el consentimiento general de un titular para una finalidad del RAT | EP-007 | 5 | R2 |

### Sprint 23 (2027-08-23 a 2027-09-03)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 39 puntos en 7 historias. Epicas: EP-009 Proveedores y Encargados (16 pts); EP-011 ARCO-POL (20 pts); EP-013 Incidentes de Seguridad (3 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-009-09 | Notificar al Encargado la revocacion de un consentimiento dentro del plazo legal | EP-009 | 8 | R2 |
| HU-011-01 | Registrar una solicitud ARCO-POL con los datos comunes y los campos especificos del derecho ejercido | EP-011 | 5 | R2 |
| HU-011-03 | Verificar la identidad y la legitimacion del solicitante segun su tipo | EP-011 | 5 | R2 |
| HU-011-05 | Determinar el aprobador por defecto de los actos atribuidos al Delegado | EP-011 | 5 | R2 |
| HU-011-06 | Admitir automaticamente la solicitud cuando el checklist del Art. 18 esta completo | EP-011 | 5 | R2 |
| HU-009-10 | Notificar a un Tercero/Receptor tras una rectificacion, actualizacion o eliminacion | EP-009 | 8 | R2 |
| HU-013-01 | Reportar un incidente de seguridad | EP-013 | 3 | R2 |

### Sprint 24 (2027-09-06 a 2027-09-17)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 36 puntos (descuenta asuetos: 2027-09-15). Comprometido: 36 puntos en 10 historias. Epicas: EP-009 Proveedores y Encargados (17 pts); EP-015 Controles de Seguridad (19 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-009-11 | Suspender manualmente a un proveedor por un incidente de seguridad y reactivarlo o finalizar la relacion | EP-009 | 5 | R2 |
| HU-009-12 | Finalizar y cerrar la relacion con un proveedor | EP-009 | 5 | R2 |
| HU-009-13 | Archivar un registro de proveedor duplicado, cancelado o creado por error | EP-009 | 2 | R2 |
| HU-009-14 | Exportar el paquete de evidencia de un proveedor con verificacion de integridad | EP-009 | 5 | R2 |
| HU-015-02 | Editar los datos de un control existente | EP-015 | 2 | R2 |
| HU-015-03 | Consultar y filtrar el catalogo de controles segun el rol | EP-015 | 5 | R2 |
| HU-015-04 | Vincular un control al Sistema o Tratamiento que protege | EP-015 | 3 | R2 |
| HU-015-05 | Registrar pais y proveedor de una transferencia en un control SSL/TLS | EP-015 | 2 | R2 |
| HU-015-06 | Marcar un control como Implementado adjuntando evidencia | EP-015 | 5 | R2 |
| HU-015-14 | Consultar el historial de cambios de un control | EP-015 | 2 | R2 |

### Sprint 25 (2027-09-20 a 2027-10-01)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 40 puntos en 10 historias. Epicas: EP-015 Controles de Seguridad (29 pts); EP-007 Consentimiento (11 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-015-07 | Exigir un segundo aprobador para implementar un control critico | EP-015 | 5 | R2 |
| HU-015-08 | Registrar una excepcion de control con justificacion | EP-015 | 3 | R2 |
| HU-015-09 | Aprobar o rechazar una excepcion de control | EP-015 | 5 | R2 |
| HU-015-10 | Archivar y reactivar un control | EP-015 | 3 | R2 |
| HU-015-11 | Precargar el catalogo base de controles al completar el diagnostico | EP-015 | 5 | R2 |
| HU-015-12 | Mostrar el indicador de controles con evidencia vigente | EP-015 | 5 | R2 |
| HU-015-13 | Mostrar el indicador de controles obligatorios sin evidencia | EP-015 | 3 | R2 |
| HU-007-02 | Generar la tarea de captura de consentimiento cuando el RAT declara la base Consentimiento | EP-007 | 3 | R2 |
| HU-007-03 | Registrar un consentimiento reforzado para datos sensibles con firma | EP-007 | 5 | R2 |
| HU-007-06 | Archivar automaticamente el consentimiento sustituido al otorgarse uno nuevo vigente | EP-007 | 3 | R2 |

### Sprint 26 (2027-10-04 a 2027-10-15)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 39 puntos en 8 historias. Epicas: EP-007 Consentimiento (39 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-007-04 | Registrar un consentimiento biometrico con firma y alternativa no biometrica | EP-007 | 5 | R2 |
| HU-007-05 | Ejecutar el sub-flujo de consentimiento parental para titulares NNA | EP-007 | 5 | R2 |
| HU-007-07 | Marcar como Expirado un consentimiento cuando vence la vigencia declarada en el RAT | EP-007 | 3 | R2 |
| HU-007-08 | Registrar la solicitud de revocacion y calcular el plazo de ejecucion | EP-007 | 5 | R2 |
| HU-007-09 | Validar y ejecutar la revocacion con aprobacion del Delegado o Responsable interno | EP-007 | 5 | R2 |
| HU-007-10 | Notificar la revocacion al encargado o cerrar el expediente cuando no aplica | EP-007 | 8 | R2 |
| HU-007-11 | Marcar como Vencida una revocacion que supera su plazo sin avanzar | EP-007 | 5 | R2 |
| HU-007-12 | Exportar los listados basicos de consentimientos y de revocaciones | EP-007 | 3 | R2 |

### Sprint 27 (2027-10-18 a 2027-10-29)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 40 puntos en 9 historias. Epicas: EP-007 Consentimiento (5 pts); EP-011 ARCO-POL (32 pts); EP-013 Incidentes de Seguridad (3 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-007-13 | Exportar el expediente individual de un consentimiento con verificacion de integridad | EP-007 | 5 | R2 |
| HU-011-02 | Cargar un formulario oficial ARCO-POL de la ACE ya diligenciado | EP-011 | 3 | R2 |
| HU-011-04 | Activar el sub-flujo de titular nina, nino o adolescente | EP-011 | 3 | R2 |
| HU-011-07 | Prevenir la solicitud incompleta y archivarla automaticamente si no se subsana | EP-011 | 8 | R2 |
| HU-011-08 | Declarar y notificar la incompetencia dentro de 5 dias habiles | EP-011 | 5 | R2 |
| HU-011-09 | Prorrogar una sola vez el plazo general por causa justificada | EP-011 | 5 | R2 |
| HU-011-10 | Activar y liberar el bloqueo cautelar del dato durante la rectificacion | EP-011 | 5 | R2 |
| HU-011-16 | Aplicar la gratuidad y la tabla de costos de reproduccion o envio | EP-011 | 3 | R2 |
| HU-013-06 | Registrar acciones de contencion inmediata | EP-013 | 3 | R2 |

### Sprint 28 (2027-11-01 a 2027-11-12)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 36 puntos (descuenta asuetos: 2027-11-02). Comprometido: 36 puntos en 6 historias. Epicas: EP-011 ARCO-POL (34 pts); EP-017 Capacitacion (2 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-011-11 | Analizar la procedencia de la solicitud aplicando el checklist tasado de causales | EP-011 | 8 | R2 |
| HU-011-12 | Aprobar y emitir el reconocimiento del derecho ejercido | EP-011 | 5 | R2 |
| HU-011-13 | Redactar, revisar y notificar la denegatoria motivada dentro de 3 dias habiles | EP-011 | 8 | R2 |
| HU-011-14 | Notificar a los receptores de los datos dentro de 5 dias habiles | EP-011 | 8 | R2 |
| HU-011-15 | Cerrar el expediente y conservarlo sin posibilidad de borrado | EP-011 | 5 | R2 |
| HU-017-01 | Configurar los parametros generales de capacitacion | EP-017 | 2 | R2 |

### Sprint 29 (2027-11-15 a 2027-11-26)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 39 puntos en 8 historias. Epicas: EP-011 ARCO-POL (18 pts); EP-013 Incidentes de Seguridad (21 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-011-17 | Generar el informe de acceso filtrando los datos de terceros | EP-011 | 5 | R2 |
| HU-011-18 | Habilitar la portabilidad condicionada a la base de consentimiento y al tratamiento automatizado | EP-011 | 5 | R2 |
| HU-011-19 | Exportar el expediente o el paquete de evidencia con verificacion de integridad | EP-011 | 5 | R2 |
| HU-011-20 | Registrar el reclamo del titular ante la Direccion de Proteccion de Datos como texto libre | EP-011 | 3 | R2 |
| HU-013-02 | Confirmar la fecha de conocimiento y arrancar los dos cronometros de 72 horas | EP-013 | 8 | R2 |
| HU-013-03 | Clasificar el incidente en Triage | EP-013 | 5 | R2 |
| HU-013-04 | Descartar un incidente en Triage por no ser una vulneracion de datos personales | EP-013 | 3 | R2 |
| HU-013-05 | Registrar el inicio de la revision exhaustiva del incidente | EP-013 | 5 | R2 |

### Sprint 30 (2027-11-29 a 2027-12-10)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 40 puntos en 6 historias. Epicas: EP-013 Incidentes de Seguridad (40 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-013-07 | Evaluar el alcance, impacto y riesgo del incidente con bloqueo de documentacion obligatoria | EP-013 | 8 | R2 |
| HU-013-08 | Decidir si corresponde la notificacion externa del incidente | EP-013 | 5 | R2 |
| HU-013-09 | Completar el contenido y generar los borradores diferenciados de notificacion | EP-013 | 8 | R2 |
| HU-013-10 | Aprobar y marcar como enviada cada notificacion externa | EP-013 | 8 | R2 |
| HU-013-11 | Recibir alertas y escalamiento de los dos cronometros de 72 horas | EP-013 | 8 | R2 |
| HU-013-17 | Consultar el checklist de las 72 horas del incidente | EP-013 | 3 | R2 |

### Sprint 31 (2027-12-13 a 2027-12-24)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 36 puntos (descuenta asuetos: 2027-12-24). Comprometido: 36 puntos en 8 historias. Epicas: EP-013 Incidentes de Seguridad (26 pts); EP-017 Capacitacion (10 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-013-12 | Registrar las medidas correctivas definitivas y la actualizacion de politicas | EP-013 | 5 | R2 |
| HU-013-13 | Completar la decision final de cierre del incidente | EP-013 | 8 | R2 |
| HU-013-14 | Enviar el expediente cerrado a conservacion sin borrado | EP-013 | 3 | R2 |
| HU-013-15 | Reabrir un incidente cerrado o descartado | EP-013 | 5 | R2 |
| HU-017-02 | Crear y versionar programas de capacitacion general, de induccion y por rol | EP-017 | 5 | R2 |
| HU-017-03 | Asignar y dar seguimiento a la asistencia de una persona a una capacitacion | EP-017 | 5 | R2 |
| HU-013-16 | Registrar lecciones aprendidas tras el cierre | EP-013 | 2 | R2 |
| HU-013-18 | Consultar el listado de incidentes con filtros | EP-013 | 3 | R2 |

### Sprint 32 (2027-12-27 a 2028-01-07)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 36 puntos (descuenta asuetos: 2027-12-31). Comprometido: 36 puntos en 9 historias. Epicas: EP-013 Incidentes de Seguridad (3 pts); EP-017 Capacitacion (33 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-013-19 | Exportar el expediente de un incidente como paquete de evidencia verificable | EP-013 | 3 | R2 |
| HU-017-04 | Confirmar mi propia asistencia a una capacitacion asignada | EP-017 | 3 | R2 |
| HU-017-05 | Crear automaticamente la induccion de un usuario nuevo dado de alta | EP-017 | 3 | R2 |
| HU-017-06 | Asignar automaticamente la capacitacion por rol al cambiar de rol un usuario | EP-017 | 3 | R2 |
| HU-017-07 | Calcular y ejecutar la renovacion automatica de una capacitacion | EP-017 | 5 | R2 |
| HU-017-08 | Notificar a MOD-002 la constancia de capacitacion del Delegado | EP-017 | 3 | R2 |
| HU-017-09 | Elaborar el borrador del plan anual de capacitacion e induccion | EP-017 | 5 | R2 |
| HU-017-10 | Aprobar y publicar el plan anual de capacitacion e induccion | EP-017 | 8 | R2 |
| HU-017-11 | Recibir recordatorio para elaborar o actualizar el plan anual antes de su vencimiento | EP-017 | 3 | R2 |

### Sprint 33 (2028-01-10 a 2028-01-21)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 40 puntos en 10 historias. Epicas: EP-017 Capacitacion (11 pts); EP-019 Centro de Evidencias (29 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-017-12 | Aplicar el efecto de la bandera de la reforma 659 sobre el plan anual | EP-017 | 3 | R2 |
| HU-017-13 | Consultar los indicadores de capacitacion del personal | EP-017 | 3 | R2 |
| HU-017-14 | Exportar reportes y listados de capacitacion del personal | EP-017 | 3 | R2 |
| HU-017-15 | Recibir sugerencia de capacitacion a partir de una leccion aprendida de un incidente | EP-017 | 2 | R2 |
| HU-019-06 | Restringir y auditar el acceso a evidencia por nivel de sensibilidad | EP-019 | 5 | R2 |
| HU-019-07 | Generar un paquete de evidencia con manifiesto verificable | EP-019 | 8 | R2 |
| HU-019-08 | Exigir doble control para exportar evidencia a un destinatario externo | EP-019 | 5 | R2 |
| HU-019-09 | Exportar el paquete de evidencia aprobado | EP-019 | 3 | R2 |
| HU-019-10 | Vencer y renovar evidencia con vigencia | EP-019 | 5 | R2 |
| HU-019-11 | Alertar sobre evidencia por vencer o vencida | EP-019 | 3 | R2 |

### Sprint 34 (2028-01-24 a 2028-02-04)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 39 puntos en 10 historias. Epicas: EP-019 Centro de Evidencias (11 pts); EP-020 Dashboard y Reportes (25 pts); EP-022 Notificaciones (3 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-019-12 | Archivar evidencia respetando el bloqueo por caso abierto | EP-019 | 5 | R2 |
| HU-019-13 | Generar el informe de huecos de evidencia | EP-019 | 3 | R2 |
| HU-019-14 | Exponer los indicadores de evidencia para el Dashboard | EP-019 | 3 | R2 |
| HU-020-02 | Elegir la perspectiva del Dashboard y aplicar filtros de sucursal, unidad y periodo | EP-020 | 3 | R2 |
| HU-020-03 | Mostrar el aviso de estado del programa, nunca cumplimiento legal | EP-020 | 2 | R2 |
| HU-020-04 | Bajar al registro fuente de un indicador respetando permisos | EP-020 | 5 | R2 |
| HU-020-05 | Ver el Dashboard en la perspectiva Gerencia | EP-020 | 5 | R2 |
| HU-020-06 | Ver el Dashboard en la perspectiva Responsable | EP-020 | 5 | R2 |
| HU-020-07 | Ver el Dashboard en la perspectiva Legal/Delegado | EP-020 | 5 | R2 |
| HU-022-13 | Generar notificacion critica desde el cronometro directo de MOD-011 | EP-022 | 3 | R2 |

### Sprint 35 (2028-02-07 a 2028-02-18)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 39 puntos en 7 historias. Epicas: EP-020 Dashboard y Reportes (13 pts); EP-021 Centro de Tareas (5 pts); EP-022 Notificaciones (3 pts); EP-024 Centro Regulatorio (18 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-020-08 | Ver el Dashboard en la perspectiva Auditor | EP-020 | 5 | R2 |
| HU-020-09 | Consultar el catalogo de reportes minimos por modulo de origen | EP-020 | 8 | R2 |
| HU-021-16 | Archivar una tarea como No aplica tras el cambio de regimen | EP-021 | 5 | R2 |
| HU-022-14 | Generar notificacion critica desde el cronometro directo de MOD-013 | EP-022 | 3 | R2 |
| HU-024-16 | Registrar el expediente basico de un procedimiento sancionador | EP-024 | 8 | R2 |
| HU-024-17 | Contestar el emplazamiento de un procedimiento sancionador | EP-024 | 5 | R2 |
| HU-024-18 | Registrar la resolucion final del procedimiento sancionador | EP-024 | 5 | R2 |

### Sprint 36 (2028-02-21 a 2028-03-03)

Objetivo: POR DEFINIR

Demo al cierre: POR DEFINIR

Capacidad: 40 puntos. Comprometido: 24 puntos en 6 historias. Epicas: EP-024 Centro Regulatorio (9 pts); EP-002 Delegado / Responsable Interno de Datos (2 pts); EP-000 Plataforma y requisitos transversales (13 pts).

| HU | Titulo | Epica | Puntos | Release |
|---|---|---|---|---|
| HU-024-19 | Registrar el pago de la multa impuesta | EP-024 | 3 | R2 |
| HU-024-20 | Cerrar el expediente del procedimiento sancionador | EP-024 | 3 | R2 |
| HU-024-21 | Consultar en solo lectura y exportar el expediente sancionador para auditoria | EP-024 | 3 | R2 |
| HU-002-11 | Recibir por referencia la constancia de capacitacion anual generada en MOD-017 | EP-002 | 2 | R2 |
| HU-000-16 | Exportar todos los datos de la organizacion al finalizar el contrato | EP-000 | 8 | R2 |
| HU-000-17 | Eliminar los datos de una organizacion tras finalizar el contrato | EP-000 | 5 | R2 |

## 6. Trabajo en paralelo al desarrollo (legal, contenido y UX)

PENDIENTE DE REDACCION

## 7. Riesgos del plan y como recalcularlo

PENDIENTE DE REDACCION
