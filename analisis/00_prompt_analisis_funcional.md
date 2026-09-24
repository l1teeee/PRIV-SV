# PROMPT DE ANALISIS FUNCIONAL DEL CLIENTE (resumen fiel, para agentes)

Fuente: instrucciones del cliente del 2026-09-23. Este archivo condensa los requisitos del entregable. El documento maestro con las hipotesis de producto es `C:\Proyects\PRIV-SV\PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` (leerlo completo; sus modulos son HIPOTESIS, no decisiones).

## Regla absoluta
NO programar. NO frontend, backend, APIs, componentes, migraciones, base de datos, infraestructura, SQL. El entregable es un BLUEPRINT FUNCIONAL: que modulos necesita, que hace cada uno, que informacion pide y produce, que usuarios intervienen, que procesos controla, que decisiones automatiza y cuales no, que documentos y evidencias produce, como se relacionan, que va en MVP y que despues.

## Rol
Equipo multidisciplinario: PM SaaS B2B, business analyst, especialista en proteccion de datos, compliance, investigador juridico salvadoreno, UX corporativo, arquitecto funcional, procesos, seguridad, auditoria, RegTech/LegalTech.

## Objetivo del producto
Una empresa salvadorena obligada por la LPDP, sin abogado ni DPO dedicado, debe poder: adquirir el software, registrar su organizacion, designar personas internas, completar un diagnostico guiado, saber que obligaciones debe atender, recibir tareas concretas, asignarlas, controlar plazos, documentar procesos, mantener evidencias, gestionar ARCO-POL, registrar tratamientos, controlar proveedores, gestionar incidentes, mantener documentos y demostrar lo realizado. El software traduce la regulacion en: procesos + responsabilidades + tareas + plazos + controles + documentos + evidencia + auditoria.

## Principio central
Usable por una persona NO especialista. El sistema no sustituye asesoria juridica, no determina conclusiones legales automaticamente, no garantiza cumplimiento, no sustituye decisiones internas. Debe orientar, explicar, organizar, alertar, calcular, registrar, documentar y generar evidencia. Nunca afirmar "cumplimiento legal X%"; usar estado del programa, controles configurados, tareas pendientes, evidencia disponible.

## Analisis del documento maestro (seccion 4 del prompt)
4.1 Supuestos correctos. 4.2 Supuestos que requieren validacion (legislacion, reglamentos, lineamientos, interpretacion, decisiones de producto, decisiones tecnicas). 4.3 Inconsistencias (modulos repetidos, funcionalidades solapadas, conceptos ambiguos, procesos incompletos, dependencias no contempladas). 4.4 Funciones faltantes (obligaciones o necesidades empresariales no consideradas).

## Modulos (seccion 6)
Los modulos del documento maestro son hipotesis: decidir si se mantienen, fusionan, dividen, eliminan o faltan. Presentar un MAPA DEFINITIVO DE MODULOS en arbol ASCII. Cada modulo se documenta con la ficha A-Q de `00_plantilla_ficha_modulo.md`.

## Areas que deben analizarse como minimo (secciones 8 a 34), reorganizables pero no omitibles
8.1 Configuracion de empresa (empresa, sucursales, unidades, departamentos, responsables, estructura).
8.2 Usuarios, roles y permisos (roles estandar, personalizados, aprobaciones, separacion de funciones).
8.3 Onboarding desde cero (preguntas, flujo, duracion, resultados).
9 Diagnostico inicial: preguntas sencillas (empleados, camaras, curriculums, marketing, CRM, app movil, biometria, informacion medica, cloud, datos fuera del pais...), cada respuesta dispara tratamiento + tarea + documento + evaluacion + riesgo. Disenar arbol de decisiones, preguntas, dependencias, resultados. Documentarlo, no programarlo.
10 Plan de cumplimiento generado tras el diagnostico (acciones con responsable, fecha, fundamento, evidencia, estado; por ejemplo 23 acciones: 7 criticas, 8 importantes, 8 recomendadas).
11 RAT: campos, relaciones, estados, responsables, revisiones, aprobacion, riesgo, documentacion. Evaluar si es el nucleo del sistema.
12 Mapa de datos: modulo separado o visualizacion del RAT. Debe responder donde estan los datos (origen -> sistema -> area -> proveedor -> pais -> eliminacion).
13 ARCO-POL con especial profundidad: portal publico, formulario, identidad, expediente, plazos, prevenciones, prorrogas, responsables, evidencia, respuesta, cierre, auditoria, casos especiales.
14 Centro de tareas transversal (diagnostico, ARCO-POL, incidentes, proveedores, riesgos, documentos, auditoria, controles).
15 Documentos y politicas: documentos, plantillas, versiones, borradores, aprobacion, publicacion, vencimiento, revision; cuando el sistema genera documento, borrador o pide informacion.
16 Consentimiento: si va en MVP; que registra, cuando aplica, evidencia, retiro, sincronizacion.
17 Proveedores: clasificacion, riesgo, contrato, pais, subencargados, datos, servicio, revision.
18 Transferencias internacionales: tratamiento-proveedor-pais-contrato-base-riesgo-evidencia.
19 Incidentes: flujo detallado (reportado, triage, investigacion, contencion, evaluacion, decision, notificacion, remediacion, cierre) con fundamento legal por etapa.
20 EIPD / riesgos: cuando se activa, cuestionario, scoring, revision, mitigacion, aprobacion, riesgo residual; separar calculo de riesgo de conclusion juridica.
21 Controles de seguridad: catalogo (IAM, MFA, cifrado, backups, WAF, firewall, endpoint, logs, pentesting); registrar evidencia, no ejecutar controles.
22 Retencion: periodos, motivos, excepciones, alertas, aprobacion, eliminacion, evidencias.
23 Capacitacion: MVP, integracion o version posterior; nivel funcional minimo.
24 Auditoria transversal: que acciones registrar, quien consulta, periodos, exportacion, integridad.
25 Centro de evidencias: "que evidencia tenemos de esta obligacion" conectando archivos, logs, aprobaciones, documentos, tareas, responsables, fechas.
26 Dashboard principal por perspectiva: Gerencia (vision general), Responsable (pendientes), Legal (riesgos y decisiones), Auditor (evidencias).
27 Notificaciones: canales a evaluar (plataforma, email, Teams, Slack, SMS, WhatsApp) sin asumir todos; trigger, destinatario, prioridad, frecuencia, escalamiento.
28 Reportes: gerencial, ARCO-POL, incidentes, proveedores, RAT, auditoria, seguridad.
29 Busqueda global.
30 Calendario central (revisiones, plazos, auditorias, vencimientos, tareas, ARCO-POL, incidentes).
31 Centro regulatorio / marco normativo consultable, diferenciando VIGENTE, FUTURO, DEROGADO, MODIFICADO.
32 Actualizaciones normativas: experiencia cuando cambia la ley (que cambio, que afecta, que procesos requieren revision).
33 Portal del titular: ARCO-POL, avisos, politica, estado, comunicaciones, archivos; nivel de autenticacion.
34 Centro de ayuda contextual por modulo: que es, por que tengo que registrarlo, fundamento, cuando necesito ayuda juridica.

## Workflows end-to-end obligatorios (seccion 35)
Caso 1 empresa nueva implementa el sistema. Caso 2 empresa registra un nuevo proceso. Caso 3 marketing implementa un nuevo formulario. Caso 4 RRHH comienza a usar biometria. Caso 5 empresa contrata un proveedor cloud. Caso 6 proveedor almacena datos fuera del pais. Caso 7 titular solicita acceso. Caso 8 titular solicita eliminacion. Caso 9 ocurre una brecha de datos. Caso 10 se acerca una auditoria. Caso 11 cambia la normativa.

## Entidades y relaciones (secciones 36 y 37)
Identificar entidades conceptuales (Organization, User, Role, Department, Treatment, Purpose, LegalBasis, DataCategory, Vendor, System, Transfer, PrivacyRequest, Incident, Risk, DPIA, Task, Document, Evidence, Control, AuditEvent, Notification, etc.): que representa y relaciones. Diagrama conceptual ASCII. Sin SQL.

## Priorizacion (secciones 38 a 40)
Matriz: Funcionalidad | Obligacion | Valor | Complejidad | Riesgo | MVP (MUST HAVE, SHOULD HAVE, COULD HAVE, FUTURE). Definir MVP realista: producto minimo vendible a una empresa salvadorena; lo que puede esperar; lo Enterprise; lo que no debe desarrollarse. Seccion ANTI-FEATURES (no ser CRM, no SIEM, no sustituir abogado, no almacenar PII innecesaria, no automatizar decisiones legales delicadas, no resolver todos los paises, y otras).

## UX (seccion 41)
Reducir complejidad para quien no conoce la ley: lenguaje, tooltips, wizards, ejemplos, plantillas, recomendaciones, semaforos, tareas, progresos, dashboards. Evitar lenguaje juridico innecesario.

## Estructura de la salida final (seccion 42), en este orden
1 Resumen ejecutivo. 2 Validacion de la idea. 3 Hallazgos regulatorios. 4 Objetivo exacto del producto. 5 Tipos de usuario. 6 Mapa definitivo de modulos. 7 Explicacion de cada modulo (ficha completa). 8 Workflows end-to-end. 9 Modelo conceptual de informacion. 10 Dependencias entre modulos. 11 Sistema de roles y permisos. 12 Sistema de tareas y alertas. 13 Sistema de evidencia y auditoria. 14 Dashboard y reportes. 15 Propuesta de onboarding. 16 Funcionalidades obligatorias por ley. 17 Funcionalidades recomendadas. 18 Funcionalidades opcionales. 19 MVP. 20 V1. 21 V2 / Enterprise. 22 Funcionalidades que NO deben construirse. 23 Riesgos del producto. 24 Preguntas pendientes. 25 Recomendacion de siguiente etapa.

## Pregunta rectora
Que debe tener exactamente cada modulo para que una persona dentro de una empresa salvadorena pueda gestionar correctamente su programa de proteccion de datos, aunque no sea especialista en privacidad, manteniendo limites claros entre orientacion del software y decisiones juridicas.
