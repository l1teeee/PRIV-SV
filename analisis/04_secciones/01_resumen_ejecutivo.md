# 1. Resumen ejecutivo

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (prohibido codigo, SQL, APIs, endpoints, esquemas de base de datos, nombres de tecnologias, stack o infraestructura). Este documento es la seccion 1 del blueprint funcional del proyecto PRIV-SV y consolida, sin inventar contenido nuevo, lo que las secciones 2 a 25 y las 26 fichas de `03_modulos/` ya definieron. Cada cifra de este resumen fue verificada contra el archivo fuente que se cita junto a ella (`matriz_obligaciones.json`, `mapa_modulos.json` y los documentos de `02_validacion/` y `04_secciones/`), no estimada. Toda obligacion legal se cita con su ID canonico de `01_legal/matriz_obligaciones.json` (formato OBL-AREA-NN, 105 obligaciones); los IDs preliminares de `01_legal/03_hallazgos_regulatorios.md` (OBL-AMBITO-xx, OBL-CONSENT-xx y similares) no se usan en este documento.

Destinatarios de esta seccion: la direccion de la empresa cliente que encargo este analisis y el equipo de producto que construira el sistema a partir de el.

---

## 1.1 Que es el producto, para quien y que no es

**Que es.** Una plataforma SaaS B2B de autogestion de proteccion de datos personales para empresas privadas de El Salvador sujetas a la Ley para la Proteccion de Datos Personales (Decreto Legislativo 144, vigente desde el 23 de noviembre de 2024). El sistema convierte las obligaciones de esa ley, sus politicas de actuacion y sus lineamientos en procesos, responsables, tareas, plazos, controles, documentos y evidencia, para que la empresa los gestione con su propio personal, sin equipo de privacidad dedicado (fuente: `02_validacion/04_objetivo_exacto_del_producto.md`, seccion 1.1).

**Para quien.** Empresas privadas salvadorenas obligadas por la LPDP sin departamento de privacidad dedicado, desde una pyme de alrededor de 30 empleados (perfil "Karla Hernandez", Ferreteria y Suministros El Roble) hasta una empresa mediana de una sola sociedad (perfil "Jorge Menendez", Avicola San Andres). El perfil de grupo corporativo con varias sociedades (perfil "Ana Gabriela Reyes Portillo", Grupo Financiero Itzalco) es cliente objetivo de V2/Enterprise, no del producto minimo vendible (decision de alcance 2.7.31 de `02_validacion/02_validacion_de_la_idea.md`). El usuario tipico no es abogado ni especialista en proteccion de datos: es una persona con otro cargo (administracion, RRHH, TI o cumplimiento) a quien la empresa le asigna esta responsabilidad ademas de su trabajo habitual.

**Que hace.** Orienta, explica, organiza, alerta, calcula, registra, documenta y genera evidencia: traduce el diagnostico de la empresa en la lista de obligaciones que le aplican (con su OBL-ID y articulo), genera un plan de trabajo con tareas y fechas, calcula y vigila los plazos legales mediante un motor de dias y horas habiles compartido por todos los modulos con plazo legal, organiza el Registro de Actividades de Tratamiento, el manejo de ARCO-POL, la gestion de incidentes, proveedores, riesgos, documentos, controles de seguridad y el ciclo de vida completo del Delegado de Proteccion de Datos, y conserva evidencia con integridad verificable.

**Que NO es y que NO hace** (fuente: `02_validacion/04_objetivo_exacto_del_producto.md`, seccion 1.2, y `02_validacion/22_anti_features.md`, 25 items razonados):

- No sustituye asesoria juridica, ni actua como Delegado de Proteccion de Datos, abogado, auditor externo o responsable del tratamiento de la empresa cliente.
- No garantiza cumplimiento legal ni declara un porcentaje de cumplimiento (0 a 100%): toda metrica visible se expresa como estado del programa, controles configurados, tareas pendientes o evidencia disponible.
- No decide automaticamente cuestiones juridicas: no resuelve por si solo si una base juridica es valida, no resuelve automaticamente una solicitud ARCO-POL, no califica si un pais tiene "nivel de proteccion adecuado", y no convierte el resultado de una evaluacion de riesgo en una conclusion legal.
- No opera como CRM ni como SIEM: no centraliza la base de clientes del cliente ni ejecuta controles tecnicos de seguridad; registra metadatos y evidencia de que un control existe, no lo ejecuta.
- No presenta tramites ante la ACE en nombre de la empresa sin su autorizacion y ejecucion explicita, ni emite la certificacion oficial del Delegado.

## 1.2 Veredicto de la validacion de la idea

**Viabilidad funcional: SI, con ajustes de alcance, no de direccion.** El nucleo operativo que planteaba el documento maestro (RAT, ARCO-POL, Incidentes, Proveedores, Consentimiento, Controles de seguridad) esta bien orientado: corresponde a los modulos con mas obligaciones OBLIGATORIO de la matriz. El hallazgo estructural mas importante de toda la validacion es que el documento maestro nunca incluia la figura del Delegado de Proteccion de Datos como rol o campo propio, pese a que los Arts. 15 y 17 LPDP la exigen hoy (OBL-DPO-01 a 08) mientras el Decreto Legislativo 659 no se publique en el Diario Oficial. Esto no invalida la idea: confirma que el producto responde a una necesidad regulatoria real e inmediata (fuente: `02_validacion/02_validacion_de_la_idea.md`, seccion 2.1).

**Urgencia comercial validada por plazos ya vencidos.** De las 105 obligaciones de la matriz, 58 estan clasificadas OBLIGATORIO, 42 CONDICIONAL y 5 RECOMENDADO (conteo verificado contra `01_legal/matriz_obligaciones.json`). Dos de las OBLIGATORIO tienen plazo transitorio ya vencido a la fecha de este analisis: la adecuacion a las Politicas de Actuacion de la ACE (OBL-PLAZO-03, vencio el 2/3-dic-2025) y el establecimiento de mecanismos de ejercicio de derechos ARCO-POL (OBL-PLAZO-04, vencio el 23-may-2025). Esto valida la urgencia comercial de la idea y orienta la priorizacion del MVP.

**Cifras de la validacion** (conteo verificado fila por fila contra `02_validacion/02_validacion_de_la_idea.md`; el documento califica su propio total como "68 supuestos revisados en la seccion 2.2 y 2.3", pero la suma verificada de las filas de sus propias tablas da 65 -37 mas 28-, discrepancia que se deja registrada aqui, no corregida por esta seccion):

| Categoria | Cantidad verificada | Detalle |
|---|---|---|
| Supuestos correctos (2.2) | 37 | Confirman la ley vigente o buena practica verificable |
| Supuestos que requieren validacion (2.3) | 28 | Legislacion: 3. Reglamentos y lineamientos ACE: 3. Interpretacion juridica (requiere abogado): 6. Decision de producto: 11. Decision tecnica: 5 |
| Supuestos incorrectos o desactualizados (2.4) | 2 | "Datos laborales" como categoria sensible generica; ausencia del rol Delegado |
| Inconsistencias detectadas y resueltas (2.5) | 26 | A. Modulos solapados: 6. B. Conceptos ambiguos: 5. C. Procesos incompletos: 5. D. Dependencias no contempladas: 6. E. Contradicciones internas: 4 |
| Funciones faltantes priorizadas (2.6) | 31 | Prioridad alta: 11. Prioridad media: 17. Prioridad baja: 3 |
| Decisiones de alcance adoptadas para el blueprint (2.7) | 32 | Cada una con su razon; ninguna reinterpreta un articulo de la ley salvo donde fija un criterio conservador explicito ante una ambiguedad ya documentada |

Ninguno de estos supuestos, inconsistencias o funciones faltantes cuestiona la premisa central del producto. Las decisiones de alcance resuelven las inconsistencias fusionando modulos (por ejemplo, Inventario se fusiona dentro del RAT), incorporando el rol Delegado desde el primer diseno, y separando lo que es mandato legal expreso de lo que es decision de producto marcada "[opinion de producto]".

## 1.3 Hallazgos regulatorios clave

Fuente: `01_legal/03_hallazgos_regulatorios.md`, secciones 1 a 3, y `01_legal/matriz_obligaciones.json`.

- **Ley vigente:** Ley para la Proteccion de Datos Personales, Decreto Legislativo 144, publicada en el Diario Oficial 219, Tomo 445, el 15 de noviembre de 2024, vigente desde el 23 de noviembre de 2024 (Art. 64: ocho dias despues de su publicacion).
- **Autoridad rectora:** la Agencia de Ciberseguridad del Estado (ACE), a traves de su Director/Direccion de Proteccion de Datos Personales (Arts. 50 a 52 LPDP).
- **Plazos transitorios ya vencidos:** el plazo de tres meses para que los sujetos obligados se adecuaran a las Politicas de Actuacion de la ACE vencio el 2/3 de diciembre de 2025 (OBL-PLAZO-03); el plazo de seis meses para establecer mecanismos de ejercicio de derechos ARCO-POL vencio el 23 de mayo de 2025 (OBL-PLAZO-04). Ambos siguen exigibles y OBLIGATORIO en la matriz.
- **Politicas de Actuacion de la ACE** (N. 001-0309025-DPDP, vigentes segun prensa desde el 3-sep-2025): declaran de cumplimiento obligatorio medidas organizativas (Politica de Proteccion de Datos, Delegado, capacitacion, Registro de Actividades de Tratamiento, EIPD, auditorias anuales), tecnicas (control de acceso, cifrado, backups, analisis de vulnerabilidades) y de transferencia.
- **Lineamientos para el Delegado de Proteccion de Datos y Normativa para el Procedimiento Administrativo Sancionador**, ambos de la ACE, publicados en el Diario Oficial 146, Tomo 452, el 11 de agosto de 2026, vigentes desde el 19 de agosto de 2026.
- **Reforma de septiembre de 2026 (Decreto Legislativo 659, segun fuentes secundarias, numero pendiente de confirmar):** aprobada por la Asamblea Legislativa el 17 de septiembre de 2026 con 57 votos, pero sin publicacion confirmada en el Diario Oficial al 24 de septiembre de 2026 (estado APROBADA-PENDIENTE-PUBLICACION). Segun fuentes secundarias, derogaria la obligatoriedad del Delegado en el sector privado (Arts. 15 y 17) y trasladaria sus funciones al "sujeto obligado" (Art. 16), sin cambiar los plazos existentes (20+20 dias, prevencion de 10, devolucion en 5, notificacion a terceros en 5, revocacion en 5).
- **Modelo de doble estado:** el producto modela una sola entidad (MOD-002) con un atributo `tipo_rol` (DELEGADO o RESPONSABLE_INTERNO) y una bandera manual `regimen_reforma_659` (ACTUAL o FUTURO) alojada en MOD-024, activada solo cuando el equipo del producto confirme la publicacion oficial y transcurra la vacatio legis de 8 dias, nunca por la sola fecha de aprobacion legislativa. 17 obligaciones de la matriz quedan marcadas como afectadas por este cambio (OBL-DPO-01 a 08, OBL-ARCO-01/08/10/11/14, OBL-CONS-03, OBL-CAP-02, OBL-RET-04, OBL-PLAZO-05; conteo verificado contra `matriz_obligaciones.json`, campo `afectada_por_reforma_659`).

Toda incertidumbre juridica genuina identificada en el corpus (computo de las 72 horas del Art. 25 en horas corridas u habiles, aplicabilidad del Art. 82 LPA al sector privado, si un encargado extranjero es transferencia internacional, edad de consentimiento de menores, numero exacto del decreto de reforma) se muestra siempre al usuario como una eleccion explicita con un criterio conservador por defecto, nunca como un hecho legal cerrado, y se marca "requiere validacion de asesoria juridica" cuando corresponde.

## 1.4 Mapa de modulos: 26 modulos en 6 etapas mas barra transversal

Fuente: `02_validacion/mapa_modulos.json` (105/105 obligaciones verificadas por script) y `02_validacion/06_mapa_definitivo_de_modulos.md`. El recorrido del usuario, no la taxonomia juridica, ordena las 6 etapas; los 6 modulos transversales son una barra fija visible desde cualquier pantalla.

```
PLATAFORMA DE AUTOGESTION DE PROTECCION DE DATOS (El Salvador)
|
|== EMPEZAR ==========  |== DIAGNOSTICAR ==  |== PLANIFICAR ====
|  MOD-001 Organizacion |  MOD-004 Diagnos-  |  MOD-005 Plan de
|  MOD-002 Delegado     |  tico de Cumpli-   |  Cumplimiento
|  MOD-003 Onboarding   |  miento            |
v                       v                    v
|== REGISTRAR ============================================
|  MOD-006 RAT y Mapa de Datos | MOD-007 Consentimiento
|  MOD-008 Documentos y Politicas | MOD-009 Proveedores
|  MOD-010 Transferencias Internacionales
v
|== OPERAR ================================================
|  MOD-011 ARCO-POL | MOD-012 Portal del Titular
|  MOD-013 Incidentes | MOD-014 Riesgos y EIPD
|  MOD-015 Controles | MOD-016 Retencion | MOD-017 Capacitacion
v
|== DEMOSTRAR ==============================================
|  MOD-018 Auditoria | MOD-019 Centro de Evidencias
|  MOD-020 Dashboard y Reportes
v
+----------------------------------------------------------+
|  BARRA TRANSVERSAL: MOD-021 Tareas, MOD-022 Notificaciones,|
|  MOD-023 Calendario y Motor de Plazos, MOD-024 Centro      |
|  Regulatorio, MOD-025 Busqueda Global, MOD-026 Ayuda        |
+----------------------------------------------------------+
```

**Conteo por clasificacion** (verificado contra `mapa_modulos.json`, campo `mvp`): 20 modulos MUST HAVE, 5 SHOULD HAVE, 1 COULD HAVE, 0 FUTURE a nivel de modulo completo. 26 modulos en total: uno mas que la propuesta ganadora original de 25, por la elevacion de MOD-002 (Delegado) de submodulo a modulo de primer nivel.

| Cod | Modulo | Etapa | Clasificacion | Que hace, en una linea |
|---|---|---|---|---|
| MOD-001 | Organizacion y Personas | Empezar | MUST HAVE | Identidad legal de la empresa, sucursales y el modelo de roles y permisos que usan todos los demas modulos |
| MOD-002 | Delegado / Responsable Interno de Datos | Empezar | MUST HAVE | Ciclo de vida completo del Delegado (nombramiento, comunicacion a la ACE, reverificacion, informes) y el doble estado de la reforma 659 |
| MOD-003 | Onboarding | Empezar | MUST HAVE | Alta guiada de organizacion, primer usuario y siembra del Delegado en la primera sesion |
| MOD-004 | Diagnostico de Cumplimiento | Diagnosticar | MUST HAVE | Cuestionario guiado y repetible que traduce respuestas en tratamientos, tareas, documentos y riesgos |
| MOD-005 | Plan de Cumplimiento | Planificar | MUST HAVE | Convierte el diagnostico en acciones priorizadas con responsable, fecha y fundamento normativo |
| MOD-006 | RAT y Mapa de Datos | Registrar | MUST HAVE | Registro de Actividades de Tratamiento como fuente unica de verdad, con mapa de datos y catalogo de sistemas |
| MOD-007 | Consentimiento | Registrar | MUST HAVE | Registro y revocacion del consentimiento, con sub-flujo reforzado para datos sensibles y menores de edad |
| MOD-008 | Documentos y Politicas | Registrar | MUST HAVE | Gestor documental que versiona Politica de Proteccion de Datos, Politica de Privacidad y Aviso de Privacidad |
| MOD-009 | Proveedores y Encargados | Registrar | MUST HAVE | Registra encargados, terceros/receptores y subencargados, con sus contratos/DPA |
| MOD-010 | Transferencias Internacionales | Registrar | SHOULD HAVE | Registra cada flujo de datos hacia otro pais y su puesta en conocimiento de la ACE |
| MOD-011 | ARCO-POL | Operar | MUST HAVE | Ciclo completo de una solicitud del titular, con verificacion de identidad y tres ramas (incompetencia, notificacion a receptores, reclamo) |
| MOD-012 | Portal del Titular | Operar | SHOULD HAVE | Canal publico opcional para presentar ARCO-POL y consultar su estado, adicional al formulario interno del MVP |
| MOD-013 | Incidentes de Seguridad | Operar | MUST HAVE | Ciclo completo de una vulneracion, con dos cronometros de 72 horas separados |
| MOD-014 | Riesgos y EIPD | Operar | SHOULD HAVE | Evalua tratamientos de alto riesgo y genera Evaluaciones de Impacto en la Privacidad |
| MOD-015 | Controles de Seguridad | Operar | MUST HAVE | Catalogo unico de controles tecnicos, organizativos y fisicos con evidencia de implementacion |
| MOD-016 | Retencion y Eliminacion | Operar | SHOULD HAVE | Dos motores de retencion: datos del titular por finalidad, y documentacion propia de cumplimiento |
| MOD-017 | Capacitacion | Operar | MUST HAVE | Registro minimo obligatorio de capacitacion del personal, mas la capacitacion especifica del Delegado |
| MOD-018 | Auditoria de Cumplimiento | Demostrar | SHOULD HAVE | Programa sustantivo de auditoria anual, distinto del registro tecnico de trazabilidad |
| MOD-019 | Centro de Evidencias | Demostrar | MUST HAVE | Vista de que evidencia existe por cada obligacion, con paquete exportable e integridad verificable |
| MOD-020 | Dashboard y Reportes | Demostrar | MUST HAVE | Vista por perspectiva (Gerencia, Responsable, Legal/Delegado, Auditor) del estado del programa |
| MOD-021 | Centro de Tareas | Transversal | MUST HAVE | Convierte cada obligacion detectada en una accion con responsable, fecha y estado |
| MOD-022 | Notificaciones | Transversal | MUST HAVE | Alertas por evento con destinatario, prioridad y escalamiento, sin fatiga de notificacion |
| MOD-023 | Calendario y Motor de Plazos | Transversal | MUST HAVE | Unico calculo de dias y horas habiles y asuetos, consultado por todos los modulos con plazo legal |
| MOD-024 | Centro Regulatorio | Transversal | MUST HAVE | Marco normativo consultable, bandera del doble estado de la reforma 659, Procedimiento Sancionador y Tramites ante la ACE |
| MOD-025 | Busqueda Global | Transversal | COULD HAVE | Busqueda agregada entre modulos de negocio |
| MOD-026 | Centro de Ayuda | Transversal | MUST HAVE | Ayuda contextual por modulo con fundamento legal en segundo nivel |

## 1.5 El MVP: que hace y que no

Fuente: `04_secciones/19_21_roadmap_mvp_v1_v2.md`, secciones 19.2, 19.8 y 19.9. Un modulo entra al MVP si cumple al menos una de tres condiciones: (a) cubre una obligacion OBLIGATORIO con plazo transitorio ya vencido (OBL-PLAZO-03, OBL-PLAZO-04); (b) es dependencia estructural de otro modulo MUST HAVE; o (c) es la unica forma de que el producto sea probatorio desde el primer dia (Centro de Evidencias, AuditLog).

Un producto minimo vendible, bajo este test, permite a una empresa sin abogado ni Delegado dedicado, con su propio personal: registrar su organizacion y designar responsables; saber que le aplica; recibir un plan de trabajo con plazos; registrar que datos trata; gestionar sus bases legales y documentos regulatorios; controlar a sus proveedores; resolver una solicitud de un titular dentro del plazo legal; reaccionar a una vulneracion de seguridad dentro de las 72 horas; demostrar que tiene controles de seguridad; capacitar a su personal; y ver el estado de su programa con evidencia verificable.

Ningun modulo SHOULD HAVE o COULD HAVE (MOD-010, MOD-012, MOD-014, MOD-016, MOD-018, MOD-025) deja una obligacion sin ninguna forma de cumplirse: cada uno tiene un mecanismo de cobertura parcial ya activo en el MVP (por ejemplo, el diagnostico crea una tarea manual para documentar una transferencia internacional mientras MOD-010 completo no exista).

Ante el riesgo de que 20 de 26 modulos MUST HAVE exceda la capacidad real de un primer lanzamiento, la seccion 19.8 propone, sin reclasificar ningun modulo, una secuencia de entrega en dos grupos:

- **Nucleo vendible (primer lanzamiento comercial), 10 modulos:** MOD-003, MOD-001, MOD-002 (alta y responsable designado); MOD-023, MOD-021, MOD-022, MOD-024 (motor de plazos, tareas, alertas y estado normativo); MOD-004, MOD-005 (diagnostico y plan, la propuesta de valor comercial mas directa contra los dos plazos ya vencidos); MOD-006, MOD-008 (RAT y documentos regulatorios).
- **Segundo grupo (completa el MUST HAVE en las semanas siguientes), 10 modulos:** MOD-007 (consentimiento), MOD-009 (proveedores), MOD-011 (ARCO-POL), MOD-013 (incidentes), MOD-015 (controles), MOD-017 (capacitacion), MOD-019 (evidencias), MOD-020 (dashboard), MOD-026 (ayuda).

## 1.6 Los 11 casos end-to-end

Fuente: `04_secciones/08a_workflows_casos_01_03.md` a `08d_workflows_casos_09_11.md`, seccion 8, indice de la parte 08a. Cada caso protagoniza una de tres empresas de ejemplo (Ferreteria y Suministros El Roble, pyme; Avicola San Andres, empresa mediana; Grupo Financiero Itzalco, corporativo) y cruza varios modulos, roles, plazos y evidencias de principio a fin.

1. **Una empresa nueva implementa el sistema:** alta guiada de organizacion, Delegado y diagnostico inicial en la primera sesion.
2. **La empresa registra un nuevo proceso:** alta de una actividad de tratamiento en el RAT con su base juridica y sus disparadores.
3. **Marketing implementa un nuevo formulario:** captura de datos con consentimiento, aviso de privacidad y lista de supresion.
4. **RRHH comienza a usar biometria:** consentimiento reforzado, alternativa no biometrica obligatoria y EIPD.
5. **La empresa contrata un proveedor cloud:** alta de encargado, Contrato/DPA y evaluacion de riesgo.
6. **Un proveedor almacena datos fuera del pais:** registro en Transferencias Internacionales y puesta en conocimiento de la ACE.
7. **Un titular solicita acceso a sus datos:** verificacion de identidad, plazo de 20+20 dias habiles y respuesta con evidencia.
8. **Un titular solicita la eliminacion de sus datos:** cancelacion, bloqueo cautelar, y notificacion a receptores en 5 dias habiles.
9. **Ocurre una brecha de datos:** los dos cronometros de 72 horas (notificacion externa e inicio de revision interna) en paralelo.
10. **Se acerca una auditoria:** ciclo sustantivo de auditoria anual con hallazgos, plan de accion y cierre.
11. **Cambia la normativa:** activacion manual, auditable y trazable de la bandera `regimen_reforma_659` en MOD-024.

## 1.7 Riesgos principales, preguntas bloqueantes y recomendacion de siguiente etapa

**Los seis riesgos que mas importan para la direccion** (de un registro consolidado de 52 riesgos en `04_secciones/23_riesgos_del_producto.md`, seccion 23.3, seleccionados por severidad Critica o Alta con alcance transversal a todos los clientes):

1. Activar la bandera del doble estado de la reforma 659 en el momento equivocado cambia 17 obligaciones para todos los clientes a la vez; se mantiene contenido porque la activacion nunca es automatica.
2. Que el cliente entienda el software como sustituto del abogado, del Delegado o del auditor, exponiendo al proveedor a una responsabilidad que su modelo no contempla.
3. Que el propio producto se convierta en un blanco de alto valor por concentrar datos de muchos clientes a la vez (requiere decision de arquitectura tecnica fuera de esta fase).
4. Que un error en el motor de plazos habiles se propague a todos los clientes que dependen de ARCO-POL, Incidentes, Delegado o Procedimiento sancionador al mismo tiempo.
5. Que el modelo comercial no encaje con lo que el mercado salvadoreno esta dispuesto a pagar, pese a que la urgencia legal ya esta validada.
6. Que en una pyme una sola persona cree, apruebe y audite su propio trabajo sin ningun segundo control real.

**Preguntas bloqueantes del MVP** (de `04_secciones/24_preguntas_pendientes.md`, seccion 24.8; todas ya tienen un criterio conservador operativo mientras tanto): 7 juridicas (computo de las 72 horas, aplicabilidad del Art. 82 LPA, si un encargado extranjero es transferencia, numero del decreto 659, entre otras), 4 regulatorias (confirmar la publicacion de la reforma 659 y la fecha oficial de las Politicas ACE), 4 de producto (hipotesis de herramientas actuales, suficiencia del formulario interno de ARCO-POL, necesidad de multi-sociedad desde el MVP), 4 de UX, 3 comerciales y 3 de operacion del contenido normativo (gobernanza de la bandera 659, monitoreo del Diario Oficial, mantenimiento del calendario de dias habiles).

**Recomendacion de siguiente etapa** (de `04_secciones/25_siguiente_etapa.md`): una secuencia de seis pasos, donde los pasos 1 y 2 corren en paralelo, alimentan el paso 3, del cual dependen los pasos 4 y 5, y el paso 6 cierra la secuencia.

```
PASO 1 Validaciones bloqueantes  ->  PASO 3 PRD por modulo  -> PASO 4 Arquitectura
(juridica externa, reforma 659,          del MVP (20 MUST         tecnica (solo se
piloto de decisiones de producto)        HAVE)                    nombra)
PASO 2 Prototipo de UX de los    ->                          -> PASO 5 Plan de
recorridos criticos                                              contenido normativo
                                          |                       y de ayuda
                                          v
                                     PASO 6 Plan de pilotos y criterios
                                     funcionales de salida a mercado
```

Puntos de decision que el cliente debe tomar ahora (seccion 25.8): (1) gobernanza de quien autoriza el cambio de la bandera `regimen_reforma_659` (recomendado: comite de al menos dos personas); (2) alcance del primer lanzamiento comercial (recomendado: nucleo vendible de 10 modulos primero); (3) modelo comercial y empaquetado (recomendado: fijar la estructura de paquetes antes del PRD, dejar el precio final para despues de los pilotos); (4) segmento de cliente piloto a priorizar (pyme o sector regulado de alto riesgo); (5) adopcion de la segmentacion de navegacion en tres niveles (recomendado: mantenerla como hipotesis hasta el prototipo de UX); (6) continuidad de la asesoria juridica externa (recomendado: contrato continuo, no solo consulta puntual).

## 1.8 Indice del blueprint funcional

Estructura de la salida final exigida por `00_prompt_analisis_funcional.md`, seccion 42, en 25 secciones:

1. Resumen ejecutivo (este documento).
2. Validacion de la idea: veredicto, supuestos, inconsistencias, funciones faltantes y decisiones de alcance.
3. Hallazgos regulatorios: marco normativo, linea de tiempo y catalogo de 105 obligaciones.
4. Objetivo exacto del producto: que hace, que no debe afirmar, y textos de descargo estandar.
5. Tipos de usuario: 11 perfiles representativos y los 12 roles estandar del sistema.
6. Mapa definitivo de modulos: los 26 modulos en 6 etapas mas barra transversal.
7. Explicacion de cada modulo: ficha completa de los 26 modulos en `03_modulos/`.
8. Workflows end-to-end: los 11 casos de uso completos, de disparador a cierre.
9. Modelo conceptual de informacion: entidades de dominio y sus relaciones.
10. Dependencias entre modulos: quien consulta a quien y en que direccion.
11. Sistema de roles y permisos: RBAC y reglas de separacion de funciones.
12. Sistema de tareas y alertas: como una obligacion se convierte en accion.
13. Sistema de evidencia y auditoria: Documento, Evidencia y AuditLog como entidades distintas.
14. Dashboard y reportes: vista por perspectiva de usuario.
15. Propuesta de onboarding: alta guiada de la primera sesion.
16. Funcionalidades obligatorias por ley.
17. Funcionalidades recomendadas.
18. Funcionalidades opcionales.
19. MVP: producto minimo vendible, nucleo vendible y secuencia de construccion.
20. V1: lo que llega en la siguiente version, sin dejar obligaciones sin cobertura.
21. V2 / Enterprise: multi-sociedad, integraciones y funcionalidades de demanda no validada.
22. Funcionalidades que NO deben construirse: 25 anti-features razonados.
23. Riesgos del producto: 52 riesgos consolidados en 7 categorias.
24. Preguntas pendientes: juridicas, regulatorias, de producto, de UX, comerciales y de operacion del contenido normativo.
25. Recomendacion de siguiente etapa: seis pasos y seis puntos de decision.
