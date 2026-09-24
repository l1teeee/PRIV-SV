# 2. Validacion de la idea

Fecha de consolidacion: 2026-09-24. Fase: analisis funcional (prohibido proponer codigo, SQL, APIs, stack o infraestructura).

Este documento consolida los cuatro informes de validacion elaborados en paralelo:
- `lente_supuestos.md` (supuestos correctos y supuestos que requieren validacion).
- `lente_inconsistencias.md` (26 inconsistencias del documento maestro).
- `lente_faltantes.md` (31 funciones faltantes).
- `lente_objetivo_usuarios_antifeatures.md` (objetivo del producto, tipos de usuario, anti-features), cuyas tres piezas se publican ademas como documentos separados: `04_objetivo_exacto_del_producto.md`, `05_tipos_de_usuario.md` y `22_anti_features.md`.

Fuente evaluada: `C:\Proyects\PRIV-SV\PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` (documento maestro, hipotesis de producto, no verdad establecida), contrastado contra `01_legal\matriz_obligaciones.md` / `matriz_obligaciones.json` (105 obligaciones, IDs canonicos OBL-AREA-NN) y `01_legal\03_hallazgos_regulatorios.md`.

Convencion de este documento: toda fila que cita un OBL-ID o un articulo es una afirmacion juridica verificada contra el corpus local. Toda fila marcada "[opinion de producto]" es una decision de negocio o de diseno sin mandato legal expreso. Donde una pregunta requiere criterio de abogado, se dice explicitamente "requiere validacion de asesoria juridica externa"; este documento no resuelve esas preguntas.

---

## 2.1 Veredicto general sobre la idea

**Viabilidad funcional: SI, con ajustes de alcance, no de direccion.** El nucleo operativo que el documento maestro propone (RAT, ARCO-POL, Incidentes, Proveedores, Consentimiento, Controles de seguridad) esta bien orientado: corresponde a los modulos con mas obligaciones OBLIGATORIO de la matriz y a los procesos que una empresa sin equipo de privacidad dedicado necesita primero. El problema no es la eleccion de modulos sino su delimitacion: se detectaron 26 inconsistencias (seccion 2.5), la mayoria por solapamiento entre modulos que describen la misma entidad conceptual dos o tres veces (Inventario/RAT/Mapa de datos; Contratos-DPA/Proveedores/Transferencias; Evidencia/Auditoria/Paquete de evidencias). Ninguna de estas inconsistencias exige rediseñar el objetivo del producto; todas se resuelven fusionando modulos, definiendo entidades compartidas o separando responsabilidades, es decir, con decisiones de producto (ver seccion 2.7).

**Viabilidad regulatoria: SI, pero el documento maestro tiene un vacio estructural que debe corregirse antes de pasar a diseno de modulos.** El hallazgo mas importante de toda la validacion es que el mapa de roles y el modulo de Organizacion del maestro nunca incluyen la figura de "Delegado de Proteccion de Datos" como rol o campo propio, pese a que los Arts. 15 y 17 LPDP la exigen hoy (OBL-DPO-01 a 08) y seguiran exigiendola mientras el Decreto Legislativo 659 (aprobado el 17-sep-2026, con 57 votos) no se publique en el Diario Oficial. El documento maestro ya disena, en varios lugares, como si el escenario post-reforma fuera el vigente. Esto no invalida la idea: al contrario, confirma que el producto tiene una razon de ser concreta e inmediata (traducir obligaciones legales reales en tareas), pero exige incorporar el rol Delegado y su ciclo de vida completo desde el primer diseno de modulos, no como un anadido posterior.

**Urgencia comercial validada por plazos ya vencidos.** La matriz registra 58 obligaciones OBLIGATORIO, dos de ellas con plazo transitorio ya vencido a la fecha de este analisis: la adecuacion a las Politicas de Actuacion de la ACE (OBL-PLAZO-03, vencio el 2/3-dic-2025) y el establecimiento de mecanismos de ejercicio de derechos ARCO-POL (OBL-PLAZO-04, vencio el 23-may-2025). Esto significa que buena parte del universo objetivo del producto esta hoy, a 2026-09-24, en incumplimiento de obligaciones con plazo ya cumplido, lo que valida la urgencia comercial de la idea y debe orientar la priorizacion del MVP (decision 2.7.29).

**Gaps estructurales que si son bloqueantes para el diseno de modulos (no para la idea en si).** Dos areas completas de la matriz de obligaciones no tienen ningun lugar funcional en el documento maestro: el procedimiento sancionador (area SANC, 9 obligaciones) y buena parte del ciclo de vida del Delegado mas alla de un campo de contacto (area DPO, 8 obligaciones). El tramite de puesta en conocimiento a la ACE para transferencias internacionales (Art. 45, OBL-TRANSF-05, OBLIGATORIO) tampoco tiene campo ni evidencia asociada. Estos tres vacios, junto con 28 funciones faltantes adicionales (seccion 2.6), deben cerrarse antes de considerar completo el blueprint funcional.

**Incertidumbres juridicas genuinas que el producto debe mostrar, no resolver por si solo.** Varias preguntas quedan abiertas en el propio corpus juridico (no son errores del documento maestro sino ambiguedades reales de la ley o de sus reglamentos): el computo de las 72 horas de notificacion de incidentes (horas corridas u habiles), si la prevencion del Art. 18 suspende el plazo de 20 dias del Art. 20, si un encargado extranjero (nube) debe tratarse como transferencia internacional, y la tension entre la LPDP y la Ley Crecer Juntos sobre la edad de consentimiento de menores. Para estos casos, el producto debe adoptar un criterio conservador por defecto donde sea posible (por ejemplo, horas corridas para las 72 horas) y mostrar siempre la incertidumbre de forma visible, nunca ocultarla ni resolverla como si fuera un hecho cerrado.

**Conclusion.** La idea es funcionalmente viable y responde a una necesidad regulatoria real, urgente y bien documentada. El documento maestro, tal como esta redactado, no requiere cambiar de objetivo ni de segmento de cliente; requiere: (a) incorporar explicitamente el rol Delegado y su ciclo de vida, (b) fusionar los pares de modulos duplicados identificados en la seccion 2.5, (c) anadir los modulos y funciones faltantes de la seccion 2.6 (en particular Delegado operativo y Procedimiento sancionador), y (d) fijar las decisiones de alcance de la seccion 2.7 antes de redactar la ficha de cada modulo. Ninguno de los 68 supuestos revisados en la seccion 2.2 y 2.3, ni las 26 inconsistencias, ni los 31 hallazgos de funciones faltantes, cuestionan la premisa central del producto: que una empresa salvadorena sin equipo de privacidad dedicado puede gestionar su programa de proteccion de datos con procesos, responsables, tareas, plazos, controles, documentos y evidencia, sin que el software sustituya asesoria juridica ni actue como Delegado, abogado o auditor del cliente.

---

## 2.2 Supuestos correctos

Afirmaciones del documento maestro que coinciden con la ley vigente o con una buena practica verificable, con su fundamento y su implicacion para el diseno del blueprint.

| Seccion del maestro | Afirmacion o hipotesis | Fundamento (OBL-ID / articulo) | Implicacion para el diseno |
|---|---|---|---|
| Sec. 3 | El proveedor del software no actua como Delegado, abogado, auditor externo ni responsable del tratamiento del cliente | Art. 34 LPDP; Art. 5 lit. i) (OBL-PRIN-03) | Ningun modulo debe dar a entender que el proveedor asume responsabilidad legal del cliente; es herramienta de gestion, no outsourcing |
| Sec. 7 | La reforma de septiembre de 2026 se describe como "aprobada", no como "vigente" | Decreto Legislativo 659, aprobado 17-sep-2026, estado APROBADA-PENDIENTE-PUBLICACION al 24-sep-2026 | Las reglas deben anclarse en la fecha de vigencia real, no en la de aprobacion legislativa |
| Sec. 8.2 | No asumir que una reforma aprobada esta vigente hasta verificar publicacion | Diseno de doble estado recomendado (ACTUAL vigente Arts. 15/17 vs FUTURO condicionado a publicacion confirmada) | El motor regulatorio necesita una bandera de activacion manual, nunca automatica por fecha de aprobacion |
| Sec. 8.3 | Determinar dias habiles vs. calendario para ARCO-POL | Art. 20 LPDP (OBL-ARCO-10); Art. 82 LPA (OBL-PLAZO-01) | El motor de plazos calcula en dias habiles, no en dias calendario |
| Sec. 8.4 | Verificar expresamente cualquier plazo de 72 horas en incidentes | Art. 25 LPDP (OBL-INC-01) | Cronometro y alertas especificas de 72 horas, distintas del resto de plazos en dias habiles |
| Sec. 8.6 | Consentimiento, contrato, obligacion legal, intereses vitales, interes publico e interes legitimo como bases juridicas a investigar | Art. 5 lit. g) LPDP (OBL-PRIN-02) | El RAT exige seleccionar una de seis bases de licitud por tratamiento, sin asumir que el consentimiento es la unica valida |
| Sec. 8.7 | Biometria y salud requieren consentimiento reforzado | Art. 4 lit. g) y Art. 39 LPDP (OBL-SENS-01, OBL-SENS-04, OBL-SENS-06) | El intake de datos sensibles fuerza el flujo de consentimiento escrito reforzado al marcar biometria o salud |
| Sec. 8.9 | MFA/2FA, cifrado, control de acceso, backups, firewall, IDS/IPS y pentesting como controles a investigar | Politicas de Actuacion ACE, medidas tecnicas (OBL-SEG-03); Art. 5 lit. f) LPDP | El catalogo de controles se alinea con este listado y con la referencia cruzada a ISO 27001 de las Politicas ACE |
| Sec. 8.10 | Politica de Proteccion de Datos, RAT y EIPD como documentos que la ley podria exigir | Politicas ACE, medidas organizativas lit. d) y e) (OBL-DOC-02, OBL-DOC-03); Art. 5 lit. i) | RAT y EIPD son modulos nucleo con respaldo normativo directo, no accesorios |
| Sec. 8.11 | Periodicidad anual de auditoria como algo a investigar | Politicas ACE, Art. 8 lit. b) (OBL-AUD-01) | El modulo de Auditoria genera el recordatorio anual anclado a la ultima auditoria registrada |
| Sec. 9 | El producto no debe afirmar "cumplimiento legal 100%" | Coherente con Art. 5 lit. i) LPDP (responsabilidad demostrada) | El dashboard usa "estado del programa" o "controles configurados", nunca un porcentaje de cumplimiento juridico |
| Sec. 13 / 14 | Biometria y salud como categorias especiales en inventario y RAT | Art. 4 lit. g) LPDP (OBL-SENS-01, OBL-SENS-06) | El campo "categoria de dato" marca automaticamente estas categorias como sensibles y dispara consentimiento reforzado |
| Sec. 14 | El RAT incluye base juridica, finalidad e historial de modificaciones | Art. 5 lit. g) (OBL-PRIN-02); Politicas ACE, medida lit. d) (OBL-DOC-02) | Confirma al RAT como modulo nucleo; el historial de cambios demuestra el principio de responsabilidad demostrada |
| Sec. 15 | "Tiene camaras" dispara tratamiento, tarea, documento y evaluacion de riesgo | OBL-SENS-08 (Arts. 4, 7, 12, 16) | El diagnostico enlaza esta respuesta con Riesgos/EIPD, no solo con el RAT |
| Sec. 15 | "Utiliza biometria" dispara consentimiento reforzado y evaluacion de riesgo | OBL-SENS-06, OBL-SENS-07 (Art. 26 inc. 4, Art. 37) | Debe ademas ofrecer una alternativa no biometrica, exigida por la propia obligacion |
| Sec. 15 | "Procesa informacion medica" activa un regimen especial | OBL-SENS-04 (Art. 39) | El diagnostico marca automaticamente a la empresa como tratante de datos de salud y sugiere EIPD |
| Sec. 15 | "Los datos se alojan fuera de El Salvador" activa el modulo de transferencias | OBL-TRANSF-03, OBL-TRANSF-04, OBL-TRANSF-05 (Arts. 44 y 45) | Debe encadenarse con el registro de proveedores cloud para no duplicar el alta de la misma transferencia |
| Sec. 17 | Plazo de respuesta ARCO-POL de 20 dias habiles con posibilidad de prorroga | Art. 20 LPDP (OBL-ARCO-10) | Confirma el plazo maestro del motor de calendario (ver 2.3 sobre el numero de prorrogas) |
| Sec. 19 | No asumir que todo tratamiento requiere consentimiento | Art. 5 lit. g) (OBL-PRIN-02); Art. 28 (OBL-TRAT-02, excepciones) | Consentimiento se activa solo cuando la base elegida en el RAT sea consentimiento |
| Sec. 20 | Politica de Proteccion de Datos y Politica de Privacidad como documentos distintos | Politicas ACE (medida organizativa) vs. Art. 24 LPDP (OBL-AVISO-01) | El gestor documental modela dos tipos de documento con publico y contenido minimo distintos |
| Sec. 21 | Reglas de retencion por categoria/tratamiento con estados "proximo a vencer" y "eliminado" | Art. 5 lit. h) LPDP (principio de temporalidad) | Motor de retencion basado en finalidad, no solo en fecha fija (ver 2.3 sobre plazos sectoriales simultaneos) |
| Sec. 23 | No asumir que el sistema puede sustituir revision juridica en contratos/DPA | Consistente con Art. 34 LPDP | Todo contrato generado por plantilla se marca como borrador sujeto a revision legal antes de firma |
| Sec. 24 | El sistema debe poder detectar transferencias no documentadas | OBL-TRANSF-05 (Art. 45); OBL-TRANSF-06 (carga de la prueba, Art. 54 inc. 2) | Cruza proveedores/paises con el RAT para senalar tratamientos con destino extranjero sin ficha de transferencia |
| Sec. 25 | Motor condicional de 72 horas para incidentes | Art. 25 LPDP (OBL-INC-01, OBL-INC-02) | Valida el cronometro de 72 horas como funcionalidad obligatoria (ver 2.3 sobre horas corridas/habiles) |
| Sec. 26 | No convertir automaticamente el resultado de la EIPD en conclusion legal definitiva | Consistente con Art. 5 lit. i) LPDP | El resultado de la EIPD es insumo para una decision humana, nunca aprobacion/rechazo automatico |
| Sec. 27 | Catalogo de controles sin convertir el producto en SIEM ni antivirus | OBL-SEG-02, OBL-SEG-03, OBL-SEG-05; Art. 5 lit. f) LPDP | El limite funcional correcto: registrar evidencia de controles, no ejecutarlos |
| Sec. 28 | Capacitacion del personal como funcionalidad a evaluar | Politicas ACE, medida organizativa lit. c) (OBL-CAP-01) | La capacitacion general tiene respaldo normativo directo (ver 2.5, inconsistencia 25, sobre su caracter obligatorio) |
| Sec. 29 | Los usuarios normales no deberian poder borrar logs de auditoria | Art. 5 lit. i) LPDP (responsabilidad demostrada) | Requiere control de integridad de logs especifico, no solo un permiso mas del RBAC generico |
| Sec. 31 | Dashboard con "controles configurados X%" en vez de "cumplimiento legal X%" | Coherente con Art. 5 lit. i) LPDP | Toda metrica visible describe el estado del programa, nunca un porcentaje de cumplimiento juridico |
| Sec. 32 y 42 | La UX debe evitar lenguaje juridico innecesario, textos extensos y terminologia tecnica | Art. 5 lit. e) LPDP, principio de transparencia (prohibe expresamente textos extensos, terminologia tecnica y letra pequena) | Todo texto de cara al titular (avisos, formularios ARCO-POL, portal) se audita contra este articulo, no solo contra buenas practicas de UX |
| Sec. 33 | Reconocer el stack propuesto como hipotesis pendiente de comparacion tecnica | Consistente con la regla de fase de `00_contexto_para_agentes.md` | Esta fase de analisis no se pronuncia sobre stack; correctamente diferido a la fase de arquitectura tecnica |
| Sec. 37 | Privacy by design: no copiar o centralizar innecesariamente todos los datos personales de los clientes | Art. 5 lit. d) LPDP, principio de minimizacion (sin OBL-ID propio en la matriz; se sugiere incorporarlo al area PRIN) | Existe mandato legal expreso, no solo argumento tecnico, que limita lo que el propio producto puede almacenar de sus clientes (ver 2.5, inconsistencia 23, sobre el alcance de este principio) |
| Sec. 40 | Separar "Core Privacy Engine" de "Regulatory Packs" versionables por jurisdiccion y fecha de vigencia | Diseno de doble estado exigido por la reforma 659 | Unica forma de modelar que un mismo articulo tenga dos versiones vigentes en momentos distintos (ver 2.5, inconsistencia 22) |
| Sec. 41 | Versionado de reglas con fecha de vigencia y trazabilidad historica por expediente | Aplicable a la reforma 659 y a cualquier reforma futura | Un expediente ARCO-POL resuelto antes de la publicacion de la reforma conserva las reglas vigentes en ese momento |
| Sec. 42 | Usar la frase "requiere validacion de la organizacion o asesoria especializada" para separar software y asesoria juridica | Consistente con todo el corpus revisado | Debe ser un estado o etiqueta reutilizable en toda la plataforma (EIPD, bases juridicas, transferencias, denegatorias ARCO-POL) |
| Sec. 49 | La empresa sigue siendo responsable de sus decisiones | Art. 34 LPDP; Art. 5 lit. i) LPDP | Ninguna accion del sistema se ejecuta sin una aprobacion humana identificable dentro de la empresa cliente |
| Sec. 6 | Bancos, seguros, clinicas, hospitales, laboratorios y empresas con biometria, videovigilancia o marketing directo como segmentos de mayor necesidad | OBL-AMB-02 (sujetos SSF); OBL-SENS-04 (salud); OBL-SENS-06/08 (biometria, videovigilancia); OBL-ARCO-05 (oposicion a marketing directo) | Valida la priorizacion comercial hacia estos sectores con una razon juridica concreta, no solo intuicion de mercado |

---

## 2.3 Supuestos que requieren validacion

Afirmaciones cuya certeza depende de legislacion aun no publicada, de un reglamento o lineamiento sin desarrollo suficiente, de una interpretacion juridica no resuelta, o de una decision de producto o tecnica que el corpus juridico no puede zanjar por si solo. Agrupadas por tipo de validacion pendiente.

### 2.3.1 Legislacion

| Seccion del maestro | Afirmacion o hipotesis | Pregunta concreta pendiente | Implicacion para el diseno |
|---|---|---|---|
| Sec. 7 / 8.1 | El numero de decreto de la reforma se cita como "659" sin nota de incertidumbre | Busquedas y fuentes secundarias devuelven numeros distintos (659 y 660) para la misma reforma; el numero correcto se confirma solo con el texto que publique el Diario Oficial | Toda referencia a "Decreto 659" en el producto debe marcarse como "segun fuentes secundarias, pendiente de confirmar" (ver decision 2.7.32) |
| Sec. 17 | Investigar la fuente de calendario oficial para dias habiles | OBL-PLAZO-02 se apoya en el Art. 190 del Codigo de Trabajo mas dos decretos de asuetos especificos; no hay un calendario unico y consolidado publicado por una sola fuente oficial | El calendario de dias inhabiles es un dato configurable y versionado por ano, mantenido manualmente por el equipo del producto hasta que exista fuente oficial unificada |
| Sec. 21 | Estados de retencion definidos solo por categoria, tratamiento o finalidad | Tension entre el principio de temporalidad (Art. 5 lit. h) y plazos minimos de otras leyes (OBL-RET-01 mercantil 10 anos, OBL-RET-02 tributario 10 anos, OBL-RET-03 LCLDA hasta 15 anos); depende del giro de cada empresa cliente | El motor de retencion permite marcar un dato "retenido por obligacion legal distinta a la LPDP", con fundamento especifico, y genera automaticamente el escenario de denegatoria parcial motivada (Art. 22, OBL-ARCO-06) |

### 2.3.2 Reglamentos y lineamientos de la ACE

| Seccion del maestro | Afirmacion o hipotesis | Pregunta concreta pendiente | Implicacion para el diseno |
|---|---|---|---|
| Sec. 8.5 / 22 | "Subencargados" listado como concepto a investigar y registrar en el registro de proveedores | OBL-PROV-05 esta marcada `verificada: false`; es interpretacion extensiva del Art. 33 inc. 2, sin lineamiento ACE especifico al 24-sep-2026 | El campo "subencargados" se marca como practica recomendada, no bloqueante, hasta que exista base legal expresa o criterio de abogado |
| Sec. 8.8 / 24 | Un "registro" formal como parte de la documentacion necesaria para transferencias | El Art. 45 exige poner en conocimiento el "registro de banco de datos", pero la ACE no ha creado ningun registro general ni canal para cumplirlo | El sistema registra internamente la gestion del aviso a la ACE (fecha, medio, acuse si existe) como evidencia de buena fe, sin bloquear la operacion por falta de un canal que la propia autoridad no ha habilitado |
| Sec. 8.12 | "Criterios de graduacion" y "reincidencia" como elementos a determinar sobre las sanciones | El Art. 57 LPDP solo fija rangos fijos de multa por clasificacion, sin mencionar reincidencia; falta confirmar si la Normativa PAS (D.O. 11-ago-2026) contiene criterios de graduacion dentro del rango | El modulo Regulatorio muestra a lo sumo el rango legal aplicable segun clasificacion, con nota de que el monto final depende de criterios de la ACE aun no confirmados |

### 2.3.3 Interpretacion juridica (requiere validacion de asesoria juridica externa)

| Seccion del maestro | Afirmacion o hipotesis | Pregunta concreta pendiente | Implicacion para el diseno |
|---|---|---|---|
| Sec. 8.5 / 23 | "Instrucciones documentadas" y "devolucion/eliminacion de datos" modeladas como obligaciones contractuales del encargado | OBL-PROV-06 y OBL-PROV-07 estan marcadas `verificada: false`, RECOMENDADO; se apoyan por analogia en Art. 34 y Art. 5 lit. h) e i), sin articulo expreso | Las plantillas de DPA distinguen visualmente las clausulas con base legal expresa (Art. 36) de las clausulas de buena practica sin articulo especifico |
| Sec. 8.8 / 24 | "Autorizaciones" como requisito de las transferencias internacionales | El Art. 45 exige "poner en conocimiento", no crea un tramite de autorizacion o aprobacion previa de la ACE | El modulo de Transferencias no modela un estado "aprobado por la ACE" bloqueante, sino "puesto en conocimiento de la ACE" mas la opinion previa opcional |
| Sec. 15 | Una sola pregunta de onboarding ("procesa informacion de menores") para todo el tratamiento de NNA | Tension no resuelta entre el Art. 5 lit. j) LPDP (ejercicio progresivo de facultades, sin edad numerica) y el Art. 77 de la Ley Crecer Juntos (adolescentes de 12 a 18 anos pueden consentir solos ciertas publicaciones) | El diagnostico marca el tratamiento de NNA como "requiere criterio juridico" y muestra informacion de ambas normas en conflicto, sin fijar una regla automatica de edad |
| Sec. 17 | "Suspensiones si legalmente aplican" durante el plazo de 20 dias habiles | No esta resuelto si la prevencion del Art. 18 suspende el computo del Art. 20 por analogia con el Art. 90.1 LPA | El motor de plazos permite configurar ambos criterios (con nota de riesgo visible) hasta que un abogado fije el criterio aplicable |
| Sec. 25 | Contenido de la notificacion de incidente descrito de forma unica, sin diferenciar destinatario | El Art. 25 exige contenido minimo distinto: literales a) a e) para ACE y Fiscalia, pero solo a), b), d) y e) para los titulares (OBL-INC-03) | El generador de notificaciones produce dos plantillas distintas (autoridad frente a titular) a partir del mismo expediente de incidente |
| Sec. 25 | Computo de las 72 horas del plazo de notificacion de incidentes | No esta resuelto si son horas corridas u horas habiles; la LPA (Art. 82) no distingue expresamente para plazos en horas | El cronometro de 72 horas se implementa por defecto en horas corridas (criterio conservador), con nota de incertidumbre visible (ver decision 2.7.11) |

### 2.3.4 Decision de producto

| Seccion del maestro | Afirmacion o hipotesis | Pregunta concreta pendiente | Implicacion para el diseno |
|---|---|---|---|
| Sec. 4 | Empresas salvadorenas "pueden estar usando Excel, Word, correos, carpetas compartidas" como hipotesis de mercado | Sin respaldo en el corpus juridico; requiere investigacion de mercado directa (encuestas, entrevistas) | No debe usarse como dato de dimensionamiento sin validacion directa; el diagnostico inicial puede capturar esta informacion de cada cliente real |
| Sec. 5 | Modelo comercial (SaaS mensual/anual, licencia por modulos, Basic/Professional/Enterprise, on-premise) como abanico abierto | Decision estrictamente comercial; requiere estudio de disposicion a pagar y de practicas de mercado local | Fuera del alcance de esta fase de analisis funcional; requiere estudio de mercado separado |
| Sec. 8.5 / 23 | Clausulas de "instrucciones documentadas" y "devolucion/eliminacion de datos" del DPA | Se documentan explicitamente como "practica recomendada del producto" para no dar la impresion de mandato legal directo | Ver tambien 2.3.3; el etiquetado visual de la clausula es decision de producto |
| Sec. 17 | "Portal publico" asumido como la arquitectura de ARCO-POL | OBL-PLAZO-04 y OBL-DOC-04 exigen "mecanismos" de ejercicio de derechos, sin mandar un portal publico especifico | El MVP puede satisfacer la obligacion legal con un formulario interno seguro; el portal publico dedicado es V1/Enterprise (ver decision 2.7.30) |
| Sec. 17 | "Prorrogas" (en plural) del plazo de respuesta ARCO-POL | El Art. 20 (OBL-ARCO-10) permite una unica prorroga de hasta 20 dias habiles adicionales, no prorrogas sucesivas | El motor de plazos limita a una sola prorroga por expediente |
| Sec. 26 | El sistema "debe generar nivel de riesgo" (scoring de la EIPD) sin metodologia especificada | Las Politicas ACE exigen EIPD sin fijar formato, contenido minimo ni umbral de riesgo | El resultado de la EIPD lleva visible la leyenda "metodologia propia del producto, no un formato oficial de la ACE" |
| Sec. 28 | Un unico modulo de "Capacitacion" para todos los temas y publicos | OBL-CAP-01 (general, todo el personal) y OBL-DPO-05 (especifica del Delegado, condicional a la reforma 659) tienen bases y periodicidad distintas | Dos programas de capacitacion distintos en el modelo de informacion, cada uno con fundamento y periodicidad propios |
| Sec. 32 | Enfoque de UX de tres niveles (Basico/Intermedio/Especialista) | Mas alla del mandato de lenguaje claro del Art. 5 lit. e), la segmentacion en tres niveles es decision de diseno sin respaldo normativo especifico | Validar con pruebas de usabilidad antes de comprometer el diseno de navegacion a tres niveles fijos |
| Sec. 38 | Integraciones futuras con M365, Salesforce, HubSpot, SAP listadas de forma generica | Sin evidencia de que integraciones usan realmente las empresas salvadorenas objetivo | Priorizar integraciones segun el diagnostico real de los primeros clientes piloto |
| Sec. 43 | OneTrust, TrustArc, DataGrail, Securiti listados como competencia internacional de referencia directa | Ninguna fuente confirma que estas plataformas tengan adaptacion especifica a la LPDP salvadorena | Su valor es de referencia de funcionalidades maduras, no evidencia de que resuelven el mercado local; requiere investigacion competitiva separada |
| Sec. 45 | Lista de 11 modulos de MVP planteada como hipotesis | La matriz registra 58 obligaciones OBLIGATORIO, varias con plazo transitorio ya vencido (OBL-PLAZO-03, OBL-PLAZO-04) | El MVP se justifica explicitamente contra esas obligaciones vencidas primero (ver decision 2.7.29) |

### 2.3.5 Decision tecnica

| Seccion del maestro | Afirmacion o hipotesis | Pregunta concreta pendiente | Implicacion para el diseno |
|---|---|---|---|
| Sec. 18 | El portal de privacidad publico requiere "analizar seguridad y riesgos de exposicion" | Sin regla legal especifica sobre el nivel de controles exigido a un portal publico, mas alla del deber general de seguridad (Art. 5 lit. f, OBL-SEG-02/03) | El portal se trata como un sistema que procesa datos personales del titular y recibe el mismo catalogo de controles que los sistemas internos, no un estandar reducido |
| Sec. 21 | "Investigar como manejar backups" ante una solicitud de eliminacion | Ninguna norma del corpus regula la eliminacion de datos dentro de copias de respaldo | Se documenta como criterio propio del producto (purga inmediata, en el siguiente ciclo de rotacion, o excepcion aceptada) y se comunica asi al cliente |
| Sec. 29 | WORM, append-only logs y hash chaining propuestos como requisitos de auditoria | Ninguna tecnica esta exigida expresamente por la LPDP ni por las Politicas ACE, que solo mencionan "logs" de forma generica | Se documentan como estandar propio de ingenieria, distinguiendolos claramente de los controles exigidos por norma |
| Sec. 30 | Formatos de exportacion PDF/XLSX/CSV/ZIP para el paquete de evidencias | Ningun articulo ni la Normativa PAS especifica un formato obligatorio de entrega de evidencia | Se mantienen como decision de producto; el generador de evidencia debe poder adaptarse si la ACE llega a exigir un formato especifico |
| Sec. 33 a 39 | Comparaciones de frontend, backend, base de datos, cloud, multi-tenancy e integraciones | `00_contexto_para_agentes.md` y `00_prompt_analisis_funcional.md` prohiben decidir stack, APIs, base de datos o infraestructura en esta fase | Ningun modulo del blueprint funcional queda condicionado a una eleccion de stack; se difiere integramente a la fase de arquitectura tecnica |

---

## 2.4 Supuestos incorrectos o desactualizados

Afirmaciones que contradicen el texto vigente o que describen una categoria/tramite que la ley no reconoce tal como esta redactado.

| Seccion del maestro | Afirmacion o hipotesis | Por que es incorrecta o esta desactualizada | Correccion |
|---|---|---|---|
| Sec. 11 y 12 | El modulo de Organizacion no incluye un campo "Delegado de Proteccion de Datos" y la lista de roles no incluye "Delegado", solo "Responsable de privacidad" generico | Mientras el Decreto 659 no se publique, los Arts. 15 y 17 LPDP obligan a nombrar un Delegado con requisitos, certificacion ante la ACE y funciones propias (OBL-DPO-01 a OBL-DPO-08); el maestro ya disena como si esa figura no existiera | Agregar el rol "Delegado de Proteccion de Datos" al modulo de roles desde el primer diseno, mapeandolo despues al "sujeto obligado" cuando se confirme la publicacion de la reforma (ver decision 2.7.7) |
| Sec. 8.7 y 13 | "Datos laborales" listado junto a biometria y salud como categoria que requiere "consentimiento reforzado" | El Art. 4 lit. g) y el Art. 59 lit. b) LPDP no reconocen "datos laborales" como categoria generica de dato sensible; solo son sensibles subconjuntos especificos (salud, afiliacion sindical o gremial, datos biometricos, convicciones) que pueden aparecer dentro de un expediente laboral | El inventario y el RAT no marcan automaticamente "toda la categoria RRHH/laboral" como sensible; el diagnostico desagrega preguntas especificas (salud ocupacional, afiliacion sindical, biometria de control de acceso) (ver decision 2.7.27) |

---

## 2.5 Inconsistencias detectadas y resolucion propuesta

26 inconsistencias del documento maestro, agrupadas en cinco categorias. Toda "resolucion propuesta" es una decision de diseno funcional a validar con el equipo, no una obligacion legal en si misma, salvo cuando se cita un OBL-ID expreso.

### A. Modulos repetidos o solapados

| # | Titulo | Secciones del maestro | Resolucion propuesta |
|---|---|---|---|
| 1 | Inventario de datos vs RAT vs Mapa de datos | 13, 14 | Fusionar Inventario dentro del RAT como fuente unica de verdad; el Mapa de datos es una vista sobre el RAT, no una tercera base de datos |
| 2 | Contratos/DPA vs Proveedores vs Transferencias | 22, 23, 24 | Contratos/DPA como tipo de documento dentro de Proveedores; Transferencias enlaza por referencia al proveedor y contrato ya registrados, sin duplicar campos |
| 3 | Riesgos/EIPD vs Controles de seguridad | 26, 27 | Control como entidad unica y compartida; la EIPD selecciona controles existentes del catalogo o crea uno nuevo que queda dado de alta en Controles de seguridad |
| 4 | Evidencia (campo transversal) vs Auditoria (log) vs Paquete de evidencias | 16-27, 29, 30 | Evidencia como entidad propia distinta de AuditLog (registro de sistema) y del Paquete de evidencias (vista de exportacion sin almacenamiento propio) |
| 5 | Onboarding vs Diagnostico inicial | 15 | Separar en Onboarding (alta de organizacion, usuarios, roles) y Diagnostico de cumplimiento (cuestionario guiado), dejando explicito si el diagnostico es repetible |
| 6 | Consentimiento vs Documentos/Avisos (version del aviso duplicada) | 19, 20 | El registro de consentimiento referencia, no copia, la version especifica del Aviso de Privacidad gestionada en Documentos (fundamento: OBL-CONS-05, Art. 54) |

### B. Conceptos ambiguos

| # | Titulo | Secciones del maestro | Resolucion propuesta |
|---|---|---|---|
| 7 | Responsable de privacidad vs Delegado vs Responsable ARCO-POL | 3, 11, 12 | Crear rol explicito "Delegado de Proteccion de Datos" (OBL-DPO-01, Arts. 15 y 17); mantener "Responsable ARCO-POL" como rol operativo distinto; eliminar o redefinir "Responsable de privacidad" |
| 8 | Contacto ARCO-POL (organizacion) vs rol Responsable ARCO-POL (usuarios) | 11, 12 | El "contacto ARCO-POL" publicado se deriva automaticamente del usuario con el rol "Responsable ARCO-POL" activo, no se captura por separado |
| 9 | Encargado vs Proveedor vs Tercero/Receptor | 14, 22 | Definir tres tipos de entidad distintos (Encargado, Tercero/Receptor, Subencargado) con reglas propias de que obligaciones dispara cada uno (OBL-PROV-01 a 03, OBL-TRANSF-02) |
| 10 | Transferencia internacional vs acceso del encargado extranjero | 22, 24 | Todo proveedor/encargado fuera de El Salvador genera automaticamente un registro en Transferencias marcado "pendiente de confirmar", con nota de la ambiguedad legal (Arts. 44-45 vs Art. 4 lit. u) |
| 11 | Evidencia vs Documento vs Log de auditoria | 16, 20, 29 | Tres entidades separadas: Documento (contenido versionado), Evidencia (artefacto/referencia inmutable) y AuditLog (registro de sistema), sin superponerse |

### C. Procesos incompletos

| # | Titulo | Secciones del maestro | Resolucion propuesta |
|---|---|---|---|
| 12 | ARCO-POL sin incompetencia, notificacion a receptores ni reclamo posterior | 17 | Anadir tres ramas al flujo: Incompetencia (devolucion, OBL-ARCO-09, 5 dias habiles), Notificacion a receptores (OBL-ARCO-11, 5 dias habiles) y Reclamo ante la ACE (OBL-ARCO-14, reapertura del expediente cerrado) |
| 13 | Incidentes: computo de las 72 horas y revision interna sin diferenciar | 25 | Modelar dos hitos de 72 horas separados (notificacion externa OBL-INC-01, inicio de revision interna OBL-INC-02); adoptar por defecto horas corridas mientras la incertidumbre no se resuelva |
| 14 | Revocacion del consentimiento sin flujo de doble plazo | 19 | Modelar la revocacion como mini flujo con dos plazos encadenados (5 dias para dejar de tratar, 5 dias adicionales para informar al encargado, OBL-CONS-03, Art. 30), con tarea automatica hacia Proveedores |
| 15 | Retencion sin regla de conflicto entre bases simultaneas | 21 | Exigir que cada regla cite uno o mas OBL-RET como fundamento; la fecha efectiva de retencion es el maximo entre todos los plazos aplicables |
| 16 | Aprobacion documental sin cadena configurable por tipo de documento | 12, 20 | Aprobacion como flujo configurable por tipo/categoria de documento, con uno o mas roles aprobadores segun el tipo, en vez de un unico rol "Aprobador" uniforme |

### D. Dependencias no contempladas

| # | Titulo | Secciones del maestro | Resolucion propuesta |
|---|---|---|---|
| 17 | Calendario de dias habiles tratado como detalle, no como dependencia central | 17, 25 | Definir un motor de plazos/calendario transversal que centralice dias habiles/inhabiles y asuetos, consultado por ARCO-POL, Incidentes, Delegado y Procedimiento sancionador |
| 18 | Motor regulatorio y doble estado de la reforma 659 desconectados de los modulos operativos | 3, 40, 41 | Documentar la reforma 659 como primer caso de uso concreto del motor regulatorio, con activacion manual explicita y la lista de las 17 obligaciones que cambian de estado al activarse |
| 19 | Catalogo de sistemas sin modulo propietario | 13, 14, 22, 25 | Anadir un submodulo "Catalogo de sistemas" como unica fuente de alta/edicion, consultado por referencia desde RAT, Inventario, Proveedores e Incidentes |
| 20 | Verificacion de identidad del titular no definida | 17, 18 | Definir un subproceso explicito de "Verificacion de identidad del titular" dentro de ARCO-POL, referenciado tambien desde el Portal, que distinga los tres tipos de solicitante del Art. 6 |
| 21 | Tramites y contacto ante la ACE no modelados | 11, 24 | Anadir el concepto "Tramites ante la ACE" (envios salientes: nombramiento del delegado, puesta en conocimiento de transferencias) con estado, evidencia de envio y referencia de la ACE |
| 22 | Principio "core vs regulatory pack" contradicho por reglas salvadorenas ya incrustadas en los modulos | 40 | En la ficha de cada modulo, separar explicitamente que campos/reglas son genericos y cuales son especificos de la LPDP salvadorena |

### E. Contradicciones internas

| # | Titulo | Secciones del maestro | Resolucion propuesta |
|---|---|---|---|
| 23 | "No almacenar PII innecesariamente" vs expediente ARCO-POL, Portal, Incidentes y Consentimiento | 17, 18, 19, 25, 37 | Acotar el principio de minimizacion (Art. 5 lit. d) a RAT, Inventario y Proveedores; no aplica a ARCO-POL, Portal, Incidentes ni Consentimiento, que procesan datos del titular como objeto legitimo del proceso |
| 24 | "No ser Delegado ni operador de ARCO-POL" vs automatizacion de actos legales del delegado | 3, 17 | Todo acto atribuido legalmente al Delegado (prevencion, incompetencia, notificacion a receptores, revocacion) es calculado/redactado por el sistema pero requiere aprobacion explicita del Delegado antes de emitirse |
| 25 | Capacitacion tratada como funcionalidad opcional a evaluar vs obligacion legal | 28 | Separar el registro minimo obligatorio (ligado a OBL-CAP-01) de las funcionalidades opcionales/diferenciadoras (cursos interactivos, certificados, microlearning) |
| 26 | Integridad del log de auditoria (WORM/hash) vs paquete de evidencias exportable sin garantia de integridad | 29, 30 | Todo paquete de evidencias exportado incluye un mecanismo de verificacion de integridad propio (hash o firma validable de forma independiente) |

---

## 2.6 Funciones faltantes priorizadas

31 hallazgos de funciones u obligaciones sin cobertura en el documento maestro, ordenados por prioridad (alta primero). "Obligacion sin cobertura" cita un OBL-ID de la matriz; "necesidad empresarial" se marca explicitamente cuando no hay OBL-ID canonico, sin que eso implique que se inventa una obligacion legal.

### Prioridad alta

| # | Que falta | Obligacion / necesidad | Modulo sugerido |
|---|---|---|---|
| 1 | Nombramiento del Delegado y su comunicacion a la ACE (15 dias habiles) mas notificacion interna (3 dias habiles) | OBL-DPO-02, OBL-DPO-03 | Organizacion, sub-flujo "Delegado de Proteccion de Datos" |
| 6 | Doble estado del rol responsable de ARCO-POL ante la reforma 659, con interruptor de activacion manual | OBL-PLAZO-05 y 17 obligaciones afectadas por la reforma | Centro regulatorio + Actualizacion normativa |
| 7 | Constancia y bloqueo cautelar del dato durante una rectificacion en tramite | OBL-ARCO-03 (Art. 9, 20 dias habiles) | ARCO-POL, nuevo estado "en revision - dato bloqueado" |
| 8 | Notificacion a receptores en 5 dias habiles cuando procede rectificacion/eliminacion y los datos ya fueron transferidos | OBL-ARCO-11 (Art. 21 inc. 3) | ARCO-POL, tarea derivada del cierre, cruzada con Proveedores/Transferencias |
| 10 | Adopcion de los formularios oficiales ARCO-POL de la ACE y un canal de disponibilidad fisica ademas del portal en linea | OBL-ARCO-15, OBL-DOC-04 (plazo transitorio vencido el 23-may-2025) | Portal de privacidad |
| 12 | Tramite y evidencia de puesta en conocimiento a la ACE de cada flujo transfronterizo | OBL-TRANSF-05 (Art. 45) | Transferencias internacionales, nuevo campo "puesta en conocimiento de la ACE" |
| 15 | Contestacion del emplazamiento del procedimiento sancionador en 5 dias habiles | OBL-SANC-05 (Art. 21 Normativa PAS) | Nuevo sub-modulo "Procedimiento sancionador" |
| 19 | Programa sustantivo de auditoria anual de cumplimiento (alcance, hallazgos, plan de accion, cierre), distinto del log tecnico | OBL-AUD-01 (Art. 8 lit. b Politicas ACE) | Nuevo sub-modulo "Auditoria de cumplimiento", separado del AuditLog |
| 25 | Flujo especifico para tratamiento de datos de menores: consentimiento parental, verificacion de la relacion, lenguaje adaptado | OBL-CONS-06, OBL-PRIN-04 (Art. 5 lit. j, Art. 42) | Consentimiento, sub-flujo "titular menor de edad" |
| 26 | Flujo especifico para videovigilancia y reconocimiento facial: senalizacion, EIPD obligatoria, retencion de grabaciones | OBL-SENS-08 (Arts. 4, 7, 12, 16) | Inventario de datos + Riesgos/EIPD |
| 31 | Motor de plazos habiles como servicio transversal compartido por todos los modulos con plazo legal, no solo una vista de calendario | OBL-PLAZO-01, OBL-PLAZO-02 | Capa compartida referenciada desde ARCO-POL, Incidentes, Delegado, Procedimiento sancionador |

### Prioridad media

| # | Que falta | Obligacion / necesidad | Modulo sugerido |
|---|---|---|---|
| 2 | Reverificacion del perfil del Delegado cada 3 anos | OBL-DPO-04 | Organizacion + Capacitacion, tarea recurrente |
| 3 | Informes periodicos del Delegado al responsable (minimo dos veces al ano) | OBL-DPO-07 | Organizacion + Politicas y documentos |
| 4 | Control de la confidencialidad del Delegado durante 5 anos tras el cese | OBL-DPO-06 | Organizacion, evento de baja de un responsable |
| 5 | Deber de asistencia de las demas areas y proveedores al Delegado | OBL-DPO-08 (Art. 17) | Usuarios y roles, responsabilidad transversal del rol Delegado |
| 9 | Tarifario de costos de reproduccion/envio y registro de cobros efectivamente realizados | OBL-ARCO-13 (Art. 23) | Portal de privacidad + ARCO-POL |
| 11 | Reclamo del titular ante la Direccion de Proteccion de Datos de la ACE | OBL-ARCO-14 (10 dias habiles del titular) | ARCO-POL, estado "reclamo ante ACE" |
| 13 | Requerimientos de informacion que la ACE puede solicitar a la empresa | Art. 50 lit. t) LPDP (sin OBL-ID en la matriz) | Nuevo sub-modulo "Procedimiento sancionador" |
| 14 | Preparacion para inspecciones y diligencias preliminares de la ACE | Art. 12 Normativa PAS (sin OBL-ID en la matriz) | Paquete de evidencias, modo "preparacion de inspeccion" |
| 16 | Pago de la multa en 15 dias habiles y seguimiento de medidas adicionales ordenadas | OBL-SANC-06, OBL-SANC-03 | Procedimiento sancionador, enlazado al Centro de tareas |
| 20 | Plan anual de capacitacion e induccion, como documento propio con periodicidad anual | OBL-CAP-02 (condicional a tener Delegado) | Capacitacion, documento versionado enlazado con Politicas y documentos |
| 21 | Conservacion de la documentacion del aviso de privacidad por minimo 10 anos, como evidencia de cumplimiento (no dato del titular) | OBL-RET-04 (Art. 31 Lineamientos DPO) | Politicas y documentos, plazo de conservacion de cumplimiento distinto del motor de retencion de datos |
| 22 | Retencion del expediente ARCO-POL y de incidentes como prueba de descargo (minimo 5 anos) | OBL-RET-05 (Art. 47 Normativa PAS) | ARCO-POL e Incidentes, plazo de retencion post-cierre enlazado al paquete de evidencias |
| 23 | Preguntas del diagnostico que detecten las exclusiones del Art. 3 | OBL-AMB-02 a 04 | Onboarding / Diagnostico de cumplimiento |
| 27 | Alternativa no biometrica obligatoria cuando se usa biometria | OBL-SENS-07 (Art. 26 inc. 4, Art. 37) | Consentimiento, campo obligatorio "alternativa no biometrica ofrecida" |
| 28 | WhatsApp Business como posible transferencia internacional implicita | OBL-TRANSF-01/03/04 (conexion; sin OBL-ID exclusivo) | Onboarding, regla que conecte con Transferencias y con el aviso de privacidad |
| 29 | Supresion/opt-out de marketing directo enlazado con la oposicion ARCO-POL | OBL-ARCO-05 (Art. 12) | Consentimiento, lista de supresion enlazada con ARCO-POL |
| 30 | Gestion de grupos empresariales con varias sedes o razones sociales y delegado comun | Necesidad de negocio (conecta OBL-DPO-01, OBL-AMB-01, sin OBL-ID propio) | Organizacion; definir si el MVP soporta multi-sucursal, dejando multi-empresa/grupo para V1/Enterprise |

### Prioridad baja

| # | Que falta | Obligacion / necesidad | Modulo sugerido |
|---|---|---|---|
| 17 | Registro y monitoreo de la publicidad de resoluciones sancionatorias (version publica) | OBL-SANC-08 (Art. 55) | Centro regulatorio, referencia vinculada al expediente sancionador |
| 18 | Historial propio de infracciones y sanciones recibidas | Necesidad de negocio (sin base legal expresa de reincidencia) | Riesgos/EIPD o Procedimiento sancionador, campo de historial declarado explicitamente como buena practica |
| 24 | Deteccion de operador de infraestructura critica, para activar reporte de incidentes de ciberseguridad adicional | OBL-INC-05 (Art. 6 lit. f-g Ley de Ciberseguridad) | Onboarding (pregunta sectorial) + Incidentes (flujo adicional condicionado) |

---

## 2.7 Decisiones de alcance que se toman para el blueprint

Decisiones de producto adoptadas a partir de las secciones 2.2 a 2.6, para que el diseno de cada modulo (parte 6 en adelante del entregable final) parta de un alcance ya resuelto. Cada decision indica su razon; ninguna reinterpreta un articulo de la ley, salvo cuando se declara explicitamente un criterio conservador por defecto sobre una ambiguedad ya documentada.

1. **Fusionar Inventario de datos dentro del RAT** como fuente unica por actividad de tratamiento; el Mapa de datos es una vista (origen -> sistema -> area -> proveedor -> pais -> eliminacion) sobre el RAT, no una base de datos independiente. Razon: evita capturar la misma actividad dos veces (inconsistencia 1).
2. **Tratar Contratos/DPA como un tipo de documento dentro de Proveedores**, y mantener Transferencias como modulo aparte enlazado por referencia al proveedor y al contrato ya registrados. Razon: evita que el mismo contrato se documente en tres lugares (inconsistencia 2).
3. **Definir Control como entidad unica compartida** entre Riesgos/EIPD y Controles de seguridad; la EIPD selecciona o crea controles del catalogo, nunca mantiene una lista paralela. Razon: evita divergencia entre lo que la EIPD promete y lo que el catalogo de seguridad realmente tiene (inconsistencia 3).
4. **Modelar tres entidades distintas y relacionadas**: Documento (contenido versionado), Evidencia (artefacto o referencia vinculada a un registro especifico) y AuditLog (registro tecnico de acciones); el Paquete de evidencias es una vista de exportacion sobre las tres, sin almacenamiento propio. Razon: sin esta separacion el Centro de evidencias transversal no tiene sobre que datos consultar (inconsistencias 4 y 11).
5. **Separar Onboarding de Diagnostico de cumplimiento**, declarando el diagnostico como repetible (se puede volver a ejecutar cuando la empresa cambia de actividad, por ejemplo al empezar a usar biometria). Razon: onboarding y diagnostico responden preguntas de diseno distintas que el maestro mezcla (inconsistencia 5).
6. **El registro de consentimiento referencia, nunca copia, la version especifica del Aviso de Privacidad** gestionada en Documentos. Razon: la carga de la prueba del Art. 54 (OBL-CONS-05) exige que el texto mostrado al titular y el texto conservado como prueba sean exactamente el mismo (inconsistencia 6).
7. **Incorporar el rol "Delegado de Proteccion de Datos" de forma explicita** en Organizacion y en el catalogo de roles desde el primer diseno, distinto de "Responsable ARCO-POL"; el campo "contacto ARCO-POL" publicado se deriva automaticamente del usuario con ese rol activo. Razon: es el hallazgo estructural mas importante de toda la validacion; sin este rol el motor de tareas no tiene a quien asignar las obligaciones que la ley atribuye especificamente al Delegado (OBL-DPO-01 a 08; inconsistencias 7 y 8; supuesto incorrecto de la seccion 2.4).
8. **Definir tres tipos de entidad distintos con reglas propias**: Encargado, Tercero/Receptor y Subencargado, en lugar de un unico modulo "Proveedores y terceros" que los mezcla. Razon: activan obligaciones distintas (por ejemplo, la notificacion a receptores del Art. 21 solo aplica a receptores, no a encargados) (inconsistencia 9).
9. **Todo proveedor o encargado fuera de El Salvador genera automaticamente un registro "pendiente de confirmar" en Transferencias**, con nota visible de que la distincion legal entre transferencia y acceso del encargado extranjero no esta resuelta. Razon: evita que el sistema deje de activar obligaciones de los Arts. 44/45 por una laguna de definicion legal (inconsistencia 10).
10. **Ampliar el flujo de ARCO-POL con tres ramas explicitas**: Incompetencia (devolucion en 5 dias habiles), Notificacion a receptores (5 dias habiles) y Reclamo posterior ante la ACE (reapertura del expediente cerrado). Razon: son tres obligaciones con plazo legal propio que el flujo descrito en el maestro no contempla (inconsistencia 12; faltantes 8 y 11).
11. **En Incidentes, modelar dos hitos de 72 horas separados y visibles** (notificacion externa a ACE/Fiscalia/titulares e inicio de revision interna), adoptando por defecto el criterio conservador de horas corridas mientras no exista pronunciamiento oficial. Razon: son dos obligaciones distintas con el mismo plazo (OBL-INC-01 y OBL-INC-02) y la ambiguedad del computo exige un default explicito y visible (inconsistencia 13).
12. **Modelar la revocacion del consentimiento como un mini flujo con dos plazos encadenados** (5 dias para dejar de tratar, 5 dias adicionales para notificar al encargado), con tarea automatica hacia Proveedores. Razon: hoy es solo un campo de fecha sin maquina de estados (inconsistencia 14).
13. **Separar dos motores de retencion**: retencion de datos personales del titular (por finalidad, con fecha efectiva igual al maximo entre todos los OBL-RET aplicables) y retencion documental de cumplimiento propio de la empresa (aviso 10 anos OBL-RET-04, expediente ARCO-POL/incidentes 5 anos OBL-RET-05). Razon: usar el mismo motor para ambos arriesga eliminar un aviso de privacidad junto con los datos de un titular especifico, o eliminar datos del titular antes de tiempo por una obligacion documental ajena (inconsistencia 15; faltantes 21 y 22).
14. **Definir la aprobacion documental como flujo configurable por tipo de documento**, con uno o mas roles aprobadores segun el tipo, en lugar de un unico rol "Aprobador" aplicado de forma uniforme. Razon: un aviso de privacidad y una plantilla interna menor no requieren el mismo nivel de control (inconsistencia 16).
15. **Definir un motor de plazos habiles transversal** (calendario de dias/horas habiles y asuetos nacionales configurables por ano) como unica fuente consultada por ARCO-POL, Incidentes, Delegado y Procedimiento sancionador. Razon: evita que cada modulo implemente su propio calculo con riesgo de reglas inconsistentes (inconsistencia 17; faltante 31).
16. **Documentar la reforma 659 como el primer caso de uso concreto del motor regulatorio de doble estado** (ACTUAL/FUTURO), con activacion manual explicita -nunca automatica por la sola aprobacion legislativa- y la lista de las 17 obligaciones que cambian de estado al activarse. Razon: sin esto, el motor regulatorio quedaria como un mecanismo abstracto que no resuelve el requisito practico e inmediato de la reforma (inconsistencia 18; faltante 6).
17. **Anadir un submodulo "Catalogo de sistemas"** como unica fuente de alta/edicion de la entidad Sistema, consultada por referencia desde RAT, Inventario, Proveedores e Incidentes. Razon: evita duplicados de texto libre que rompen la trazabilidad del RAT y del mapa de datos (inconsistencia 19).
18. **Definir un subproceso explicito de "Verificacion de identidad del titular"** dentro de ARCO-POL (y referenciado desde el Portal), que distinga los tres tipos de solicitante del Art. 6 (titular, representante, herederos/sucesores). Razon: un portal publico sin este subproceso crea riesgo real de suplantacion (inconsistencia 20; faltante 10).
19. **Anadir el concepto "Tramites ante la ACE"** (envios salientes: nombramiento del delegado, puesta en conocimiento de transferencias, solicitudes de credencial) con estado propio, evidencia de envio y referencia de la ACE. Razon: es distinto del deber de documentar internamente; sin el, el producto no puede demostrar que la empresa informo a la autoridad cuando correspondia (inconsistencia 21; faltante 12).
20. **En la ficha de cada modulo, separar explicitamente los campos/reglas genericos de los especificos de la LPDP salvadorena**, en vez de dejar la separacion "Core Privacy Engine / Regulatory Pack" como una aspiracion de arquitectura no reflejada en el contenido funcional. Razon: el maestro hoy escribe terminologia salvadorena directamente en la descripcion del "core" (inconsistencia 22).
21. **Acotar el principio de minimizacion de datos (privacy by design) al RAT, Inventario y Proveedores**; declarar explicitamente que NO aplica a ARCO-POL, Portal, Incidentes ni Consentimiento, que por naturaleza procesan datos personales directos del titular como objeto legitimo del proceso. Razon: tal como esta escrito en el maestro, el principio es incompatible con los propios requisitos funcionales de esos cuatro modulos (inconsistencia 23).
22. **Todo acto legalmente atribuido al Delegado** (prevencion, incompetencia, notificacion a receptores, revocacion) es calculado y redactado por el sistema, pero requiere una accion explicita de aprobacion de la persona con el rol Delegado antes de considerarse emitido; el sistema nunca lo envia de forma automatica. Razon: cierra la brecha entre el compromiso del maestro de no actuar como operador humano de ARCO-POL y el lenguaje de automatizacion fuerte de la seccion 17 (inconsistencia 24).
23. **En Capacitacion, separar el registro minimo obligatorio** (que el personal recibio capacitacion, OBL-CAP-01) de las funcionalidades opcionales o diferenciadoras (cursos interactivos, microlearning, certificados); el registro minimo va en MVP, no "a evaluar". Razon: el maestro lo presenta como pregunta abierta de alcance cuando en realidad tiene una obligacion legal minima (inconsistencia 25).
24. **Todo paquete de evidencias exportado incluye un mecanismo propio de verificacion de integridad** (hash o firma validable de forma independiente). Razon: sin esto, la integridad que el log de auditoria garantiza dentro del sistema se pierde en el momento en que mas importa, cuando el archivo sale del sistema hacia la ACE (inconsistencia 26).
25. **Anadir dos modulos completos que el maestro no desarrolla**: "Delegado de Proteccion de Datos" (nombramiento, tramite ante la ACE en 15 dias, reverificacion cada 3 anos, informes semestrales, confidencialidad post-cese) y "Procedimiento sancionador / requerimientos ACE" (contestacion de emplazamiento en 5 dias, pago de multa, medidas adicionales, publicidad de resoluciones). Razon: son las dos areas completas de la matriz de obligaciones (8 y 9 obligaciones respectivamente) sin ningun lugar funcional propio (faltantes, secciones A y D de `lente_faltantes.md`).
26. **Separar "Auditoria de cumplimiento" (programa anual sustantivo) del log tecnico de trazabilidad (AuditLog)**; son dos cosas distintas que el maestro confunde bajo el mismo nombre de seccion. Razon: faltante 19, de prioridad alta, con fundamento en OBL-AUD-01.
27. **El diagnostico inicial incluye preguntas de exclusion del Art. 3** antes de generar el plan de cumplimiento, y desagrega la pregunta generica de "datos laborales" en preguntas especificas (salud ocupacional, afiliacion sindical, biometria de control de acceso), sin marcar automaticamente toda la categoria RRHH como sensible. Razon: evita sobre-obligar a empresas parcialmente excluidas y corrige el supuesto incorrecto de "datos laborales" como categoria sensible generica (faltante 23; seccion 2.4).
28. **Dar flujo propio a cuatro tratamientos de alto riesgo** en lugar de tratarlos como preguntas sueltas del diagnostico: menores de edad (consentimiento parental diferenciado, con aviso de la tension LPDP/Ley Crecer Juntos), videovigilancia/reconocimiento facial (EIPD automatica y retencion de grabaciones), biometria (alternativa no biometrica obligatoria) y marketing directo (lista de supresion enlazada a la oposicion ARCO-POL). Razon: hoy son solo banderas del diagnostico sin modulo que traduzca la respuesta en obligaciones especificas (faltantes 25 a 29).
29. **El MVP se prioriza explicitamente alrededor de las obligaciones OBLIGATORIO con plazo transitorio ya vencido** (adecuacion a Politicas ACE, vencida 2/3-dic-2025; mecanismos ARCO-POL, vencidos 23-may-2025), y no solo alrededor de una lista intuitiva de "modulos centrales". Razon: valida la urgencia comercial real y corrige el supuesto REQUIERE VALIDACION sobre los 11 modulos hipoteticos de MVP del maestro (seccion 2.3.4).
30. **El ARCO-POL del MVP se satisface con un formulario interno seguro**, sin portal publico dedicado; el portal publico con autoregistro del titular queda como funcionalidad V1/Enterprise. Razon: la ley exige "mecanismos" de ejercicio de derechos, no un portal publico especifico, y el portal implica mayor superficie de riesgo (identidad, exposicion) que conviene madurar despues del MVP (seccion 2.3.4).
31. **La gestion de grupos empresariales con varias sociedades y delegado comun queda fuera del MVP** (V1/Enterprise); el MVP soporta una organizacion con varias sucursales de la misma razon social. Razon: el propio maestro la deja pendiente sin desarrollo y no hay urgencia regulatoria que la fuerce al MVP (faltante 30).
32. **Toda referencia al numero del decreto de reforma se escribe como "Decreto Legislativo 659, segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado"**, nunca como un hecho cerrado, hasta que el Diario Oficial publique el texto. Razon: el numero de decreto tiene fuentes contradictorias (659 y 660) en la investigacion juridica (seccion 2.3.1).

---

## Nota final sobre alcance de este documento

Ninguna de las decisiones de la seccion 2.7 resuelve por si sola una incertidumbre juridica genuina (computo de las 72 horas, aplicabilidad del Art. 82 LPA, transferencia vs. acceso del encargado extranjero, edad de consentimiento de menores, numero exacto del Decreto 659); donde se fija un criterio conservador por defecto (por ejemplo, horas corridas), el producto debe mostrarlo siempre como una eleccion explicita y visible, no como una interpretacion legal cerrada, y remitir a asesoria juridica externa cuando el caso concreto lo amerite.
