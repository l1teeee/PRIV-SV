# 19. MVP

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (prohibido codigo, SQL, APIs, esquemas de base de datos, nombres de tecnologias, stack o infraestructura).

Esta seccion consolida y cruza lo ya decidido en `02_validacion/mapa_modulos.json`, `02_validacion/06_mapa_definitivo_de_modulos.md` (secciones 2 principio 7, 4, 5 y 11), `01_legal/matriz_obligaciones.json` (105 obligaciones) y la seccion Q ("MVP") de las 26 fichas funcionales de `03_modulos/MOD-001_ficha.md` a `MOD-026_ficha.md`. No inventa funcionalidades que ninguna ficha define: cuando el prompt del cliente exige un contenido que ninguna ficha ni el mapa cubren, se marca explicitamente "propuesta de esta seccion, no presente en las fichas". La clasificacion MVP de cada modulo (MUST HAVE, SHOULD HAVE, COULD HAVE) es siempre la de `mapa_modulos.json`; esta seccion no la modifica en ningun caso, solo la ordena, la agrupa y propone una secuencia de entrega dentro de ella.

Convencion de identificadores: todo OBL-ID citado es el identificador canonico de `01_legal/matriz_obligaciones.json` (formato OBL-AREA-NN, 105 obligaciones), nunca los IDs preliminares de `01_legal/03_hallazgos_regulatorios.md` (OBL-AMBITO-xx, OBL-CONSENT-xx y similares); la equivalencia entre unos y otros esta en la seccion 11 de ese documento. Los 12 roles citados son los de `02_validacion/05_tipos_de_usuario.md`, seccion 5.3, con su nombre exacto. Toda obligacion se clasifica OBLIGATORIO, RECOMENDADO o CONDICIONAL, igual que `matriz_obligaciones.json`. El sistema orienta, explica, organiza, alerta, calcula, registra, documenta y genera evidencia; nunca decide cuestiones juridicas ni afirma cumplimiento legal: por eso ningun indicador de esta seccion se expresa como "porcentaje de cumplimiento", solo como estado del programa, controles configurados, tareas pendientes o evidencia disponible.

Jerarquia usada para resolver cualquier discrepancia entre fuentes: fuente legal primaria y `matriz_obligaciones.json` sobre `mapa_modulos.json` y `06_mapa_definitivo_de_modulos.md`, estos sobre `05_tipos_de_usuario.md` para lo relativo a roles, y estos sobre la ficha del modulo propietario de la obligacion, y esta sobre cualquier otra ficha que mencione el mismo tema de forma colaboradora. Las contradicciones detectadas al aplicar esta jerarquia y los huecos (piezas que ninguna ficha define) se listan al final del documento, en "Contradicciones y huecos detectados".

---

## 19.1 Matriz de priorizacion consolidada (seccion 38 del prompt del cliente)

### 19.1.1 Criterio de Valor, Complejidad y Riesgo

El prompt del cliente (seccion 38 de `00_prompt_analisis_funcional.md`) exige una matriz Funcionalidad | Obligacion | Valor | Complejidad | Riesgo | Clasificacion. Esta seccion la construye a nivel de modulo (26 filas), consolidando las funcionalidades individuales que cada ficha ya prioriza en su propia seccion Q; el detalle fila por fila de cada funcionalidad interna del modulo (con su propia columna MUST/SHOULD/COULD/FUTURE) no se repite aqui y sigue viviendo en la seccion Q de cada ficha. Los tres criterios se califican en escala Alta / Media / Baja, definidos asi para todo el documento:

- **Valor** (que tanto reduce el riesgo legal y operativo de la empresa cliente si el modulo existe): Alta si el modulo cubre una o mas obligaciones OBLIGATORIO con plazo transitorio ya vencido, o es la unica forma de que el producto sea probatorio desde el primer dia (condiciones (a) y (c) del test de tres condiciones, seccion 2 principio 7 de `06_mapa_definitivo_de_modulos.md`), o es dependencia estructural de varios modulos MUST HAVE (condicion (b)). Media si cubre obligaciones OBLIGATORIO o RECOMENDADO sin plazo vencido, o si su ausencia ya tiene una cobertura parcial documentada que evita un vacio legal. Baja si es una mejora de usabilidad o de gestion sin obligacion propia y sin dependencia estructural.
- **Complejidad** (esfuerzo funcional relativo, no tecnico): Alta si el modulo tiene varias ramas o submodulos con reglas propias, un motor de calculo propio (plazos, riesgo, retencion) o depende de varios modulos a la vez para operar. Media si tiene un flujo principal con dos o tres variantes. Baja si es un registro simple con pocos estados.
- **Riesgo** (que pasa si el modulo falta o esta mal disenado): Alta si su ausencia deja un plazo legal sin vigilancia, una obligacion con infraccion grave o muy grave sin evidencia, o rompe la operacion de otro modulo MUST HAVE. Media si su ausencia es cubierta por un mecanismo parcial ya documentado en el mapa o en la ficha. Baja si su ausencia no genera exposicion legal ni bloquea a otro modulo.

### 19.1.2 Matriz consolidada (26 modulos)

Fuente de la columna Obligacion: campo `obligaciones_propietarias` de `mapa_modulos.json`, cruzado con la seccion Q de cada ficha. Fuente de Valor/Complejidad/Riesgo: la justificacion de la seccion Q de cada ficha, resumida con el criterio de 19.1.1. La columna Clasificacion es siempre la de `mapa_modulos.json` (nunca una opinion nueva de esta seccion).

| Cod | Modulo (funcionalidad nucleo del MVP) | Obligacion (OBL-ID propietaria) | Valor | Complejidad | Riesgo | Clasificacion |
|---|---|---|---|---|---|---|
| MOD-001 | Organizacion y Personas: alta de empresa, sucursales, usuarios y los 12 roles estandar | Ninguna propia (colabora OBL-AMB-01) | Alta | Media | Alta | MUST HAVE |
| MOD-002 | Delegado / Responsable Interno de Datos: nombramiento, contadores legales, doble estado 659 | OBL-DPO-01 a 08 (8) | Alta | Alta | Alta | MUST HAVE |
| MOD-003 | Onboarding: alta guiada de organizacion + primer usuario + siembra del Delegado | Ninguna propia | Alta | Media | Media | MUST HAVE |
| MOD-004 | Diagnostico de Cumplimiento: cuestionario de 11 bloques, exclusiones Art. 3, motor de disparo | OBL-AMB-01 a 04 (4) | Alta | Alta | Alta | MUST HAVE |
| MOD-005 | Plan de Cumplimiento: acciones priorizadas Critica/Importante/Recomendada con responsable y fecha | OBL-PLAZO-03 (1) | Alta | Media | Alta | MUST HAVE |
| MOD-006 | RAT y Mapa de Datos: ficha de tratamiento, catalogo de datos sensibles, catalogo de sistemas | OBL-DOC-02, OBL-PRIN-02, OBL-SENS-01/04/06/08, OBL-TRAT-01/03 (8) | Alta | Alta | Alta | MUST HAVE |
| MOD-007 | Consentimiento: registro general y reforzado, revocacion 5+5 dias, sub-flujo NNA | OBL-CONS-01 a 06, OBL-PRIN-01/04, OBL-SENS-02/03/07, OBL-TRAT-02 (12) | Alta | Alta | Alta | MUST HAVE |
| MOD-008 | Documentos y Politicas: Politica de Datos, Politica de Privacidad, Aviso de Privacidad versionado | OBL-AVISO-01 a 05, OBL-DOC-01 (6) | Alta | Media | Alta | MUST HAVE |
| MOD-009 | Proveedores y Encargados: alta de los 3 tipos de entidad, Contrato/DPA, notificaciones de 5 dias | OBL-PROV-01 a 07 (7) | Alta | Alta | Alta | MUST HAVE |
| MOD-010 | Transferencias Internacionales: registro manual de flujo hacia otro pais | OBL-TRANSF-01 a 06 (6) | Media | Media | Media | SHOULD HAVE |
| MOD-011 | ARCO-POL: formulario interno seguro, verificacion de identidad, 3 ramas, plazo 20+20 | OBL-ARCO-01 a 15 (15) | Alta | Alta | Alta | MUST HAVE |
| MOD-012 | Portal del Titular: canal publico de intake y consulta de estado sin cuenta persistente | OBL-DOC-04, OBL-PLAZO-04 (ya cubiertas por MOD-011) | Media | Media | Baja | SHOULD HAVE |
| MOD-013 | Incidentes de Seguridad: flujo completo, dos cronometros de 72 horas en paralelo | OBL-INC-01 a 05 (5) | Alta | Alta | Alta | MUST HAVE |
| MOD-014 | Riesgos y EIPD: disparo automatico, cuestionario, controles del catalogo unico, aprobacion | OBL-DOC-03 (1) | Media | Alta | Media | SHOULD HAVE |
| MOD-015 | Controles de Seguridad: catalogo unico de controles con evidencia, excepciones aprobadas | OBL-SEG-01 a 06, OBL-SENS-05 (7) | Alta | Media | Alta | MUST HAVE |
| MOD-016 | Retencion y Eliminacion: motor de datos del titular y motor documental de cumplimiento | OBL-RET-01 a 06 (6) | Media | Alta | Media | SHOULD HAVE |
| MOD-017 | Capacitacion: registro general, induccion automatica, capacitacion por rol, plan anual minimo | OBL-CAP-01, OBL-CAP-02 (2) | Alta | Media | Media | MUST HAVE |
| MOD-018 | Auditoria de Cumplimiento: ciclo sustantivo de ComplianceAudit con hallazgos y cierre | OBL-AUD-01 (1) | Media | Media | Media | SHOULD HAVE |
| MOD-019 | Centro de Evidencias: vista "que evidencia tenemos" por las 105 obligaciones, paquete con hash | OBL-PRIN-03 (1, transversal) | Alta | Alta | Alta | MUST HAVE |
| MOD-020 | Dashboard y Reportes: vision por perspectiva (Gerencia/Responsable/Legal/Auditor) | Ninguna propia | Alta | Media | Media | MUST HAVE |
| MOD-021 | Centro de Tareas: obligacion convertida en accion con responsable, fecha y estado | Ninguna propia (colabora varias) | Alta | Media | Alta | MUST HAVE |
| MOD-022 | Notificaciones: alertas por evento, niveles y escalamiento, canales plataforma y correo | Ninguna propia | Alta | Media | Alta | MUST HAVE |
| MOD-023 | Calendario y Motor de Plazos: calculo unico de dias/horas habiles y asuetos nacionales | OBL-PLAZO-01, 02 (2) | Alta | Alta | Alta | MUST HAVE |
| MOD-024 | Centro Regulatorio: marco normativo, bandera de doble estado 659, catalogo de infracciones | OBL-AUD-02, OBL-PLAZO-05, OBL-SANC-01 a 09 (11) | Alta | Alta | Alta | MUST HAVE |
| MOD-025 | Busqueda Global: busqueda agregada entre modulos de negocio | Ninguna propia | Baja | Media | Baja | COULD HAVE |
| MOD-026 | Centro de Ayuda: tarjeta contextual de 4 partes, glosario, descargo, versionado | Ninguna propia | Alta | Media | Media | MUST HAVE |

Nota de lectura: 20 filas MUST HAVE, 5 SHOULD HAVE, 1 COULD HAVE, 0 FUTURE a nivel de modulo completo; esto coincide exactamente con el resumen de `mapa_modulos.json` y con la fila "0. Resumen de modulos" de `06_mapa_definitivo_de_modulos.md`. Ningun modulo completo queda en FUTURE porque el mapa definitivo no elimina ningun modulo de primer nivel del producto: lo que se difiere a V1 o V2/Enterprise son funcionalidades especificas dentro de cada modulo (ver 19.4, seccion 20 y seccion 21), documentadas fila por fila en la seccion Q de cada ficha.

---

## 19.2 Definicion del producto minimo vendible

**Test de tres condiciones** (injertado de `propuesta_mapa_mvp.md`, adoptado como principio 7 de la seccion 2 de `06_mapa_definitivo_de_modulos.md`): un modulo entra al MVP si cumple al menos una de estas tres condiciones, no por intuicion de que "suena importante":

- (a) Cubre una obligacion OBLIGATORIO cuyo plazo transitorio ya vencio: adecuacion a las Politicas de Actuacion de la ACE (OBL-PLAZO-03, vencido 2/3-dic-2025, propietaria MOD-005) y establecimiento de mecanismos de ejercicio de derechos ARCO-POL (OBL-PLAZO-04, vencido 23-may-2025, propietaria MOD-012 pero ya satisfecha por el formulario interno de MOD-011 desde el MVP).
- (b) Es una dependencia estructural sin la cual otro modulo MUST HAVE no puede operar (por ejemplo MOD-023 Calendario para MOD-011 y MOD-013; MOD-021 Centro de Tareas para MOD-004, MOD-005, MOD-011, MOD-013 y MOD-002).
- (c) Es la unica forma de que el producto sea probatorio desde el primer dia (MOD-019 Centro de Evidencias, y el AuditLog tecnico embebido en todo modulo MUST HAVE).

Un producto minimo vendible a una empresa salvadorena, bajo este test, es aquel que le permite completar, sin abogado ni DPO dedicado y con su propio personal: registrar su organizacion y designar responsables (MOD-001, 002, 003); saber que le aplica (MOD-004); recibir un plan de trabajo con plazos (MOD-005); dejar constancia de que datos trata (MOD-006); gestionar las bases legales de ese tratamiento (MOD-007, si aplica consentimiento) y sus documentos regulatorios obligatorios (MOD-008); controlar a sus proveedores de tratamiento (MOD-009); resolver una solicitud de un titular dentro del plazo legal (MOD-011); reaccionar a una vulneracion de seguridad dentro de las 72 horas (MOD-013); demostrar que tiene controles de seguridad (MOD-015); capacitar a su personal (MOD-017); y, en todo momento, ver el estado de su programa (MOD-020) y exportar evidencia verificable de lo anterior (MOD-019), con el soporte transversal de tareas, notificaciones, plazos, marco regulatorio y ayuda contextual (MOD-021 a MOD-024, MOD-026).

---

## 19.3 Alcance por modulo: la version minima de cada modulo MUST HAVE

Resumen de la "version minima vendible" que cada ficha ya declara en su propia seccion Q. El detalle exhaustivo fila por fila de cada funcionalidad (con su propia justificacion) vive en `03_modulos/MOD-0NN_ficha.md`, seccion Q; esta subseccion no lo repite integro, lo agrupa por etapa del recorrido para que se lea como un solo producto.

### Etapa Empezar

- **MOD-001 Organizacion y Personas.** Una organizacion (una razon social) con una o varias sucursales, el catalogo completo de los 12 roles estandar, invitacion y gestion basica de usuarios (invitar, activar, suspender, dar de baja) y el catalogo minimo de unidades/departamentos. Sin roles personalizados, sin bloqueo automatico de separacion de funciones (solo advertencia visible), sin grupo multi-sociedad.
- **MOD-002 Delegado / Responsable Interno de Datos.** Alta y edicion del nombramiento, los tres contadores legales de nombramiento (notificacion interna 3 dias, comunicacion a la ACE 15 dias, sustituto por cese 10 dias), declaracion jurada de conflicto de intereses, checklist de perfil, reverificacion trienal, capacitacion anual, confidencialidad post-cese, e interruptor de doble estado (lectura de la bandera de MOD-024). Sin informes semestrales automaticos ni paquete de evidencia con hash propio (se apoyan en MOD-019 cuando este exista).
- **MOD-003 Onboarding.** Alta guiada de datos basicos de la organizacion, alta del primer usuario Administrador con invitacion de usuarios adicionales, pregunta inicial sobre el Delegado con siembra del registro en MOD-002, texto de descargo con aceptacion explicita, y creacion automatica de la tarea de inicio del Diagnostico. Sin sugerencia automatica de rol ni verificacion KYB.

### Etapa Diagnosticar y Planificar

- **MOD-004 Diagnostico de Cumplimiento.** Cuestionario completo de 11 bloques y 47 preguntas con dependencias, deteccion de exclusiones del Art. 3, motor de disparo completo (respuesta -> tratamiento + tarea + documento + riesgo), guardar y continuar, calculo de madurez inicial, y diagnostico repetible. Sin asignacion de bloques por responsable de area ni exportacion con hash (llegan en la primera iteracion posterior, ver seccion 20).
- **MOD-005 Plan de Cumplimiento.** Generacion automatica del plan tras el diagnostico, motor de priorizacion de tres niveles, asignacion de responsable y fecha, estados basicos, creacion automatica de tareas en MOD-021, exportacion con hash de integridad, recalculo manual bajo demanda y descarte de accion con justificacion. Sin recalculo automatico por cambio de respuestas o de norma.

### Etapa Registrar

- **MOD-006 RAT y Mapa de Datos.** Ficha completa de tratamiento (nombre, area, finalidad, base de licitud, categorias, sistema), catalogo cerrado de datos sensibles con marcado automatico, seis bases de licitud con justificacion obligatoria, workflow de aprobacion, catalogo de sistemas, biblioteca de al menos 20 tratamientos plantilla, y exportacion con hash. Sin mapa de datos como diagrama interactivo (la misma informacion ya es consultable en tabla).
- **MOD-007 Consentimiento.** Registro de consentimiento general y reforzado (firma para datos sensibles y biometricos), revocacion con flujo de dos plazos encadenados (5+5 dias habiles), sub-flujo de consentimiento parental para NNA, snapshot inmutable de la version del aviso, y reportes exportables basicos. Sin catalogo de excepciones al consentimiento ni sincronizacion con sistemas externos de marketing.
- **MOD-008 Documentos y Politicas.** Gestor de Politica de Proteccion de Datos, Politica de Privacidad y Aviso de Privacidad con checklist de los 9 literales del Art. 24 y los 5 elementos del Art. 7, flujo de aprobacion configurable por tipo de documento, versionado con no-borrado antes de 10 anos, y motor documental generico reutilizado por MOD-009. Sin exportacion con hash propio en esta primera version (exportacion simple a PDF) ni wizard guiado por literal.
- **MOD-009 Proveedores y Encargados.** Alta y ficha de Encargado, Tercero-Receptor y Subencargado, vinculacion obligatoria de Contrato/DPA, flujo de aprobacion con doble control en riesgo alto, alertas de vencimiento y revision, las dos notificaciones legales de 5 dias (a Encargado por revocacion, a Receptor por rectificacion/eliminacion), datos de contacto para el Aviso, y paquete de evidencia exportable por proveedor. Sin motor de scoring de riesgo ni modelado de cadenas de subcontratacion de segundo nivel.

### Etapa Operar

- **MOD-011 ARCO-POL.** Formulario interno seguro con los 7 elementos del Art. 18, carga de los 7 formularios oficiales ACE, verificacion de identidad para los 3 tipos de solicitante, sub-flujo NNA, prevencion unica con archivo automatico, plazo maestro de 20+20 dias con una prorroga, las tres ramas completas (incompetencia, notificacion a receptores con fallback manual si MOD-010 no esta activo, denegatoria motivada), bloqueo cautelar de rectificacion, gratuidad con tabla de costos publicada, informe de acceso filtrado, motor de plazos compartido con MOD-023, resolucion del aprobador segun el estado de MOD-002/MOD-024, y evidencia exportable con hash. El registro basico del reclamo ante la Direccion de Proteccion de Datos entra como texto libre desde el MVP; su plantilla dedicada llega en V1.
- **MOD-013 Incidentes de Seguridad.** Registro del incidente con flujo completo de estados, los dos cronometros de 72 horas en paralelo (notificacion e inicio de revision, criterio conservador de horas corridas por defecto), plantillas diferenciadas de notificacion a ACE/FGR y a titulares, documentacion obligatoria del expediente con bloqueo si faltan campos, checklist de las 72 horas, vinculo con el catalogo de MOD-015, constancia de envio con hash, y alertas basicas por plataforma y correo. Cubre el flujo completo de un incidente de origen interno sin depender de que MOD-009 o MOD-014 esten activos.
- **MOD-015 Controles de Seguridad.** Catalogo base de controles organizativos, tecnicos y fisicos con estado y evidencia adjunta, registro de excepciones con aprobacion de un segundo usuario, vinculacion con Sistema/Tratamiento de MOD-006, e indicadores de dashboard (evidencia vigente, controles obligatorios sin evidencia). Sin alertas automatizadas de vencimiento (dependen de que MOD-023 este maduro para ese uso especifico) ni vinculacion estructurada con MOD-010.
- **MOD-017 Capacitacion.** Registro general de capacitacion del personal, induccion automatica al alta en MOD-001, capacitacion por rol (mismo mecanismo, categorizado), recordatorio y renovacion automatica, notificacion de constancias hacia MOD-002, y una version minima del Plan anual de capacitacion (agregacion de lo ya registrado, aprobado por un segundo rol, exportable). Sin herramientas avanzadas de planificacion ni evaluaciones formales de conocimiento.

### Etapa Demostrar

- **MOD-019 Centro de Evidencias.** Vista consolidada "que evidencia tenemos de esta obligacion" por las 105 obligaciones con sus cinco estados (Faltante/En revision/Disponible/Vencida/Rechazada), recepcion automatica de evidencia desde los modulos ya activos, informe de huecos priorizado por OBLIGATORIO, carga manual de evidencia suelta con aprobacion para cubrir los modulos SHOULD HAVE aun no activos, EvidencePackage con manifiesto y verificacion de integridad, doble control para exportacion externa, y alertas de evidencia vencida. Sin paquetes especializados automaticos por tipo (auditoria, procedimiento sancionador).
- **MOD-020 Dashboard y Reportes.** Dashboard basico por las 4 perspectivas (Gerencia, Responsable, Legal/Delegado, Auditor) con los indicadores de MOD-005, MOD-019 y MOD-021 mas los de los demas modulos MUST HAVE, filtro por sucursal/unidad con drill-down respetando permisos, regla de minimizacion (nunca datos personales de titulares en el Dashboard) y prohibicion de lenguaje de cumplimiento legal, y toda exportacion verificable via MOD-019. Sin vista alternativa por los 8 clusters legales ni informes para Junta Directiva.

### Barra transversal

- **MOD-021 Centro de Tareas.** Creacion, edicion y estados basicos de la Tarea (Pendiente, En proceso, Bloqueada, Completada), fecha limite calculada desde MOD-023, estado "En revision" con entidad Aprobacion y bloqueo de autorrevision, alertas de tarea proxima a vencer y vencida, escalamiento automatico para el caso critico de 72 horas, e historial inmutable. Sin tareas recurrentes automaticas (se crean manualmente) ni vista tipo tablero.
- **MOD-022 Notificaciones.** Notificacion basica por Plataforma y Correo con resolucion de destinatario por rol, piso minimo de alertas de plazos legales no silenciable, niveles INFO/WARNING/HIGH/CRITICAL con escalamiento automatico, acuse de recibo obligatorio para CRITICAL, e historial inmutable. Sin reglas anti-fatiga ni canales adicionales (Teams, Slack, SMS, WhatsApp).
- **MOD-023 Calendario y Motor de Plazos.** Calculo de dias y horas habiles con las capas de fin de semana, calendario nacional y asuetos ad hoc, regla de computo del Art. 82 LPA, calendario de asuetos nacionales, desglose visible de cada calculo, suspension/reanudacion por causal declarada, recalculo notificado con historial, alerta de calendario no cargado, y vista de calendario central (area 30 del prompt). Sin la capa diferenciada de calendario de la autoridad ni asuetos locales por sede.
- **MOD-024 Centro Regulatorio.** Marco normativo consultable con los cuatro estados (VIGENTE/FUTURO/DEROGADO/MODIFICADO), bandera `regimen_reforma_659` con interruptor manual y notificacion a cada organizacion, catalogo informativo de infracciones y multas, registro basico de tramites ante la ACE (incluida recepcion automatica desde MOD-002 y MOD-010), y tarea automatica de revision ante cualquier cambio normativo. El flujo operativo completo del Procedimiento Sancionador queda en V1 (ver seccion 20); el registro manual basico ya permite documentar un expediente real si se presenta.
- **MOD-026 Centro de Ayuda.** Tarjeta de ayuda contextual de 4 partes vinculada a los campos de los modulos MUST HAVE, catalogo inicial de 3 a 6 articulos por modulo MUST HAVE, glosario buscable basico, descargo estandar visible en cada articulo, y versionado con historial de revision legal. Sin sincronizacion automatica con la bandera de MOD-024 (revision manual mientras tanto) ni niveles Basico/Intermedio/Especialista (anti-feature 24: requiere validarse con usuarios reales).

---

## 19.4 Cobertura parcial de los modulos SHOULD HAVE y COULD HAVE dentro del MVP

Ninguno de estos cinco modulos SHOULD HAVE, ni el unico COULD HAVE, deja un vacio legal sin cubrir mientras el modulo completo no se construye: cada uno tiene un mecanismo de cobertura parcial ya documentado en su propia ficha y en `06_mapa_definitivo_de_modulos.md`, seccion 3.

| Modulo (clasificacion) | Mecanismo de cobertura parcial ya activo en el MVP | Donde vive ese mecanismo |
|---|---|---|
| MOD-010 Transferencias Internacionales (SHOULD HAVE) | El Diagnostico (MOD-004) marca "datos fuera de El Salvador: si" y crea una tarea manual para que el responsable documente la transferencia como evidencia suelta, sin motor de deteccion automatica ni registro formal | MOD-004 (disparo) + MOD-021 (tarea) + MOD-019 (evidencia suelta con aprobacion manual) |
| MOD-012 Portal del Titular (SHOULD HAVE) | Las dos obligaciones propias (OBL-DOC-04, OBL-PLAZO-04, mecanismos de ejercicio de derechos) ya estan cubiertas por el formulario interno seguro; no hay vacio legal, solo falta el canal publico adicional | MOD-011 (formulario interno) |
| MOD-014 Riesgos y EIPD (SHOULD HAVE) | Cuando el Diagnostico detecta biometria, salud, menores o camaras, crea una tarea "elaborar EIPD" con una plantilla generica de documento, llenada manualmente y sin motor de scoring | MOD-004 (disparo) + MOD-021 (tarea) + MOD-008 (plantilla generica) |
| MOD-016 Retencion y Eliminacion (SHOULD HAVE) | OBL-RET-04 (aviso 10 anios) y OBL-RET-06 se cubren de forma pasiva como conservacion dentro de MOD-008 y de los expedientes cerrados de MOD-011/MOD-013 (no se borran por defecto); el plazo de conservacion vive como campo de texto dentro del RAT, sin alertas automaticas | MOD-008 + MOD-011 + MOD-013 (conservacion pasiva) + MOD-006 (campo de texto) |
| MOD-018 Auditoria de Cumplimiento (SHOULD HAVE) | Un recordatorio generico de la auditoria anual ya existe como evento del Calendario (MOD-023), anclado a la fecha de adecuacion inicial del diagnostico; y el AuditLog tecnico, embebido en todo modulo MUST HAVE, ya deja evidencia verificable desde el primer dia | MOD-023 (recordatorio) + AuditLog transversal (todo modulo MUST HAVE) |
| MOD-025 Busqueda Global (COULD HAVE) | Cada modulo de negocio ya resuelve su propia busqueda con sus filtros y buscadores propios (por ejemplo, filtrar tratamientos por area en MOD-006, o buscar un expediente por codigo en MOD-011); el producto es completo y vendible sin este modulo | Filtros y buscadores propios de cada ficha de modulo |

---

## 19.5 Lo que el MVP NO incluye

Esta lista agrupa, por tema, las funcionalidades SHOULD HAVE, COULD HAVE y FUTURE que las 26 fichas ya excluyen del MVP (columna de la seccion Q distinta de MUST HAVE); no repite la enumeracion completa de cada ficha, que queda como fuente de detalle.

- **Modulos completos diferidos a V1**: Transferencias Internacionales (MOD-010), Portal del Titular (MOD-012), Riesgos y EIPD (MOD-014), Retencion y Eliminacion (MOD-016), Auditoria de Cumplimiento como programa estructurado (MOD-018). Ver seccion 20.
- **Multi-sociedad y grupo corporativo**: gestion de grupo empresarial con varias razones sociales y delegado comun, vision consolidada multi-sociedad del Dashboard, del Plan de Cumplimiento, del RAT, del Centro de Tareas y del Calendario (MOD-001, MOD-002, MOD-005, MOD-006, MOD-020, MOD-021, MOD-023). Decision de alcance 2.7.31 de `02_validacion_de_la_idea.md`: el MVP soporta una organizacion con varias sucursales de la misma razon social, no varias sociedades distintas. Ver seccion 21.
- **Roles y permisos avanzados**: roles personalizados con permisos granulares por modulo/accion, bloqueo automatico configurable de separacion de funciones por umbral de tamano (MOD-001).
- **Automatizacion de calculo de riesgo**: motor de calculo ponderado de riesgo del RAT (MOD-006), motor de scoring de EIPD (MOD-014), motor de scoring de riesgo de proveedores (MOD-009).
- **Canales de notificacion adicionales**: Microsoft Teams, Slack, SMS, WhatsApp (MOD-022); el MVP cubre plataforma y correo.
- **Reportes y analitica avanzada**: vista por los 8 clusters legales, fotos periodicas y tendencia, informe para Junta Directiva (MOD-020); reportes exportables avanzados por modulo con filtros (MOD-007, MOD-009, MOD-019, MOD-021, MOD-022).
- **Procedimiento Sancionador operativo completo**: vias simplificada/ordinaria, medidas provisionales, recursos (MOD-024); el MVP solo tiene el registro manual basico del expediente y el catalogo informativo de infracciones.
- **Portal del titular enriquecido**: cuenta persistente, marca personalizada, multi-idioma, descarga de resolucion, mensajeria (MOD-012).
- **Ayuda contextual dinamica**: sincronizacion automatica con la bandera de la reforma 659, boton "necesito ayuda juridica" con tarea sugerida, retroalimentacion util/no util (MOD-026); niveles Basico/Intermedio/Especialista, explicitamente pendientes de validar con usuarios reales (anti-feature 24).

Lo que el producto no debe construir nunca (no solo diferir) esta en `02_validacion/22_anti_features.md` y no se repite aqui; esta seccion 19 no incluye ninguna de esas 25 funcionalidades ni en el MVP ni en ninguna version posterior.

---

## 19.6 Criterios funcionales de salida a mercado

**[Propuesta de esta seccion, no presente en las fichas: ningun documento del corpus define un checklist de "listo para vender" a nivel de producto completo; cada ficha define su propia version minima vendible por modulo, seccion 19.3, pero no existe una condicion de cierre transversal.]** Se propone que el MVP este listo para su primer cliente real cuando se cumplan, a la vez, las siguientes condiciones:

1. Los 20 modulos MUST HAVE de 19.1 estan disponibles en su version minima descrita en 19.3, con sus obligaciones OBLIGATORIO propietarias operativas de principio a fin (no solo como pantalla, sino con el flujo completo de estados que describe la seccion F de cada ficha).
2. Los seis mecanismos de cobertura parcial de 19.4 estan activos, de modo que ningun modulo SHOULD HAVE o COULD HAVE deja una obligacion sin ninguna forma de cumplirse mientras el modulo completo no exista.
3. Al menos los casos 1 (empresa nueva implementa el sistema), 2 (registra un nuevo proceso), 3 (marketing implementa un formulario), 7 (titular solicita acceso), 8 (titular solicita eliminacion) y 9 (ocurre una brecha de datos) de los workflows end-to-end obligatorios (seccion 35 del prompt del cliente) se pueden completar de inicio a fin sin salir del sistema ni requerir una intervencion manual fuera de el.
4. Los dos plazos transitorios ya vencidos (OBL-PLAZO-03, OBL-PLAZO-04) tienen, cada uno, un modulo operativo que permite documentar la adecuacion retroactiva (MOD-005 y MOD-015 para el primero; MOD-011 para el segundo), de modo que un cliente que se registre despues del vencimiento pueda demostrar que actuo tan pronto tuvo la herramienta.
5. El interruptor de doble estado de la reforma 659 (MOD-024) existe y esta fijado en `ACTUAL`, con el mecanismo de cambio de bandera probado (aunque no activado) antes del primer cliente, para no depender de una implementacion de urgencia el dia que se confirme la publicacion en el Diario Oficial.
6. Todo texto de cara al usuario que aparece en los 20 modulos MUST HAVE tiene su tarjeta de ayuda contextual (MOD-026) y su fundamento legal en segundo nivel, nunca en el texto principal de la pantalla.
7. Ningun modulo MUST HAVE usa la expresion "cumplimiento legal" ni un porcentaje de cumplimiento; todos usan estado del programa, controles configurados, tareas pendientes o evidencia disponible (anti-feature 5).

---

## 19.7 Perfil de cliente objetivo del MVP

Fuente primaria: `02_validacion/04_objetivo_exacto_del_producto.md`, seccion 1.1 ("Para quien"). El perfil general del producto va "desde una pyme de alrededor de 30 empleados hasta un grupo corporativo con varias sociedades"; el perfil especifico del MVP (no desarrollado como tal en ningun documento del corpus, **[propuesta de esta seccion]**) es mas acotado, porque la decision de alcance 2.7.31 deja fuera del MVP la gestion de grupos con varias sociedades:

- Empresa privada salvadorena sujeta a la LPDP, de una sola razon social, con una o varias sucursales dentro del pais.
- Sin departamento de privacidad dedicado ni abogado interno especializado; la persona que administra el sistema tiene otro cargo principal (administracion, RRHH, TI o cumplimiento general).
- Tamano tipico de pyme (alrededor de 30 empleados, perfil "Karla Hernandez" de `05_tipos_de_usuario.md`) hasta empresa mediana de una sola sociedad (varios cientos de empleados, perfil "Jorge Menendez"); el perfil de grupo corporativo con varias sociedades ("Ana Gabriela Reyes Portillo", Directora de Cumplimiento Corporativo) es cliente objetivo de V2/Enterprise, no del MVP (ver seccion 21).
- Empresa que hoy esta, con alta probabilidad, en incumplimiento de al menos una de las dos obligaciones OBLIGATORIO con plazo transitorio ya vencido (adecuacion a Politicas ACE, mecanismos ARCO-POL), lo que valida la urgencia comercial de venderle el MVP primero a este segmento (decision 2.7.29 de `02_validacion_de_la_idea.md`).
- Empresa que ya tiene, o esta en proceso de nombrar, un Delegado de Proteccion de Datos (obligatorio hoy bajo el regimen ACTUAL, Arts. 15 y 17), interno o externo.

---

## 19.8 El riesgo de "20 de 26 modulos MUST HAVE" y un nucleo vendible propuesto

El riesgo 5 de la seccion 11 de `06_mapa_definitivo_de_modulos.md` senala explicitamente: "Clasificacion MVP con muchos MUST HAVE (20 de 26) puede exceder un producto minimo vendible", y deja pendiente de validar contra capacidad real de desarrollo y disposicion a pagar (seccion 2.3.4 de `02_validacion_de_la_idea.md`). Esta seccion no cambia la clasificacion de `mapa_modulos.json` (los 20 modulos siguen siendo MUST HAVE del producto): propone, **[propuesta de esta seccion, no presente en las fichas ni en el mapa]**, subdividir esos 20 modulos en un nucleo vendible mas pequeno que ya resuelve, por si solo, la propuesta de valor central, y un segundo grupo que completa el MUST HAVE poco despues, sin que el cliente perciba una version incompleta.

- **Nucleo vendible (primer lanzamiento comercial).** MOD-003, MOD-001, MOD-002 (alta y responsable designado); MOD-023, MOD-021, MOD-022, MOD-024 (motor de plazos, tareas, alertas y estado normativo, construidos como infraestructura desde el dia uno); MOD-004, MOD-005 (diagnostico y plan, la propuesta de valor comercial mas directa contra los dos plazos ya vencidos); MOD-006, MOD-008 (RAT y documentos regulatorios, base de todo lo demas). Con este subconjunto (10 de los 20), una empresa ya puede completar el diagnostico, ver su plan de accion priorizado con plazos, y tener sus documentos regulatorios base, que es exactamente el nucleo que valida la urgencia comercial de `02_validacion_de_la_idea.md` (decision 2.7.29).
- **Segundo grupo (completa el MUST HAVE, se entrega en las semanas siguientes sin reabrir el nucleo).** MOD-007 (consentimiento), MOD-009 (proveedores), MOD-011 (ARCO-POL), MOD-013 (incidentes), MOD-015 (controles), MOD-017 (capacitacion), MOD-019 (evidencias), MOD-020 (dashboard), MOD-026 (ayuda). Estos diez modulos son los que convierten el nucleo vendible en el producto MUST HAVE completo que exige el mapa definitivo; ninguno se degrada a SHOULD HAVE, solo se secuencia despues del nucleo (ver 19.9).

Esta subdivision no reclasifica ningun modulo: los 20 siguen siendo MUST HAVE del producto final. Lo que cambia es que el nucleo vendible permite, si la capacidad real de desarrollo lo exige, ofrecer una primera version comercial mas acotada sin abandonar el compromiso de completar el MUST HAVE completo poco despues, en vez de diferir modulos completos a SHOULD HAVE sin respaldo del test de tres condiciones.

---

## 19.9 Secuencia funcional recomendada de construccion del MVP

**[Propuesta de esta seccion, no presente en las fichas ni en el mapa: ningun documento define un orden de construccion; `mapa_modulos.json` solo declara `depende_de` como dependencia de datos y servicios, no como secuencia de desarrollo, segun aclara explicitamente la seccion 6.1 de `06_mapa_definitivo_de_modulos.md`.]** Esta secuencia usa esa misma distincion: separa la capa de infraestructura transversal (que debe existir desde el inicio, aunque varios modulos de proceso la "requieran" segun el JSON) de la cadena real de dependencia estructural entre los modulos de recorrido. Ningun paso de esta secuencia cambia la clasificacion MVP de ningun modulo; es un orden de entrega, no una lista distinta de modulos.

```
CAPA DE INFRAESTRUCTURA TRANSVERSAL (se construye primero, en paralelo, sin
esperar a los modulos de proceso que la consumiran)
   MOD-023 Calendario y Motor de Plazos  (sin dependencias)
   MOD-024 Centro Regulatorio            (sin dependencias)
   MOD-021 Centro de Tareas              (esqueleto: crear/editar/estado de Tarea)
   MOD-022 Notificaciones                (esqueleto: plataforma y correo)
   MOD-019 Centro de Evidencias          (esqueleto: vista por obligacion + carga manual)
   MOD-026 Centro de Ayuda               (esqueleto: estructura de tarjeta de 4 partes;
                                           el contenido de cada articulo crece con cada
                                           modulo de proceso que se libera despues)
        |
        v
CADENA DE MODULOS DE RECORRIDO (dependencia estructural real, seccion depende_de)

MOD-003 Onboarding
     |
     v
MOD-001 Organizacion y Personas --------> MOD-002 Delegado / Responsable Interno
     |                                          |
     v                                          v
MOD-004 Diagnostico de Cumplimiento <-----------+
     |
     v
MOD-005 Plan de Cumplimiento
     |
     v
MOD-006 RAT y Mapa de Datos
     |----------------+------------------+
     v                v                  v
MOD-008 Documentos  MOD-009 Proveedores  MOD-015 Controles de Seguridad
     |                                          |
     v                                          v
MOD-007 Consentimiento                   MOD-013 Incidentes de Seguridad
     |                                          |
     +--------------------+---------------------+
                           v
                    MOD-011 ARCO-POL
                           |
                           v
                    MOD-017 Capacitacion
                           |
                           v
              MOD-019 (version completa) -> MOD-020 Dashboard y Reportes
```

Notas de lectura de la secuencia:

- **MOD-021, MOD-022 y MOD-019 se construyen como infraestructura desde el inicio**, aunque `mapa_modulos.json` liste su `depende_de` apuntando a varios modulos de proceso (MOD-004, MOD-005, MOD-011, MOD-013, MOD-002 para MOD-021; MOD-007 a MOD-018 para MOD-019): esa lista describe de que modulos reciben datos una vez existen, no una condicion para que el propio motor de tareas, de notificaciones o de evidencias pueda empezar a operar. Un Centro de Tareas vacio, un Centro de Evidencias vacio o un canal de notificaciones sin eventos aun no tienen valor por si mismos, pero deben estar listos para recibir el primer evento del primer modulo de proceso que se libere (MOD-003/MOD-001), en vez de anadirse como una capa posterior.
- **MOD-011 no requiere que MOD-012 (Portal del Titular) exista** para construirse ni para operar, pese a que `mapa_modulos.json` declara `MOD-012` en el `depende_de` de MOD-011: la decision de alcance 2.7.30 satisface la obligacion legal con el formulario interno seguro desde el MVP; MOD-012 es SHOULD HAVE y se construye despues (ver seccion 20).
- **MOD-015 no requiere que MOD-010 (Transferencias Internacionales) exista** para su version minima: la ficha de MOD-015 documenta que OBL-SEG-04 se cubre en el MVP con un campo generico dentro del propio catalogo de controles mientras MOD-010 no este activo.
- El orden dentro de "Etapa Registrar" (MOD-008, MOD-009, MOD-015 en paralelo tras MOD-006) puede variar segun capacidad de equipo, porque los tres dependen solo de MOD-006 y no entre si de forma estructural (MOD-007 si depende de MOD-008 para la version del aviso, por lo que MOD-007 debe cerrarse despues de MOD-008).
- MOD-017 Capacitacion se ubica al final de la cadena de proceso porque depende de MOD-001 y MOD-002, ambos ya construidos desde el inicio; en la practica puede liberarse en paralelo con MOD-011 o MOD-013 sin reordenar la secuencia.
- MOD-020 Dashboard es, por diseno, un modulo terminal de solo lectura (no tiene `alimenta_a`): se construye al final porque necesita que MOD-005, MOD-019 y MOD-021 ya tengan datos reales que mostrar, aunque su esqueleto de pantallas por perspectiva puede empezar a construirse en paralelo desde el inicio.

---

# 20. V1

Esta seccion agrupa, por modulo y por tema, lo que llega despues del MVP porque el analisis de demanda, riesgo o dependencia de la propia ficha lo ubica ahi, sin que ninguna obligacion legal quede sin una forma de cumplirse mientras tanto (ver 19.4). A diferencia del MVP, las 26 fichas no distinguen de forma explicita "V1" de "V2/Enterprise" dentro de su columna SHOULD HAVE, COULD HAVE o FUTURE (salvo excepciones puntuales que se citan de forma literal, como MOD-016); esta distincion es, por tanto, **[propuesta de esta seccion, no presente en las fichas, ver "Contradicciones y huecos detectados"]**, construida con el mismo criterio de demanda, riesgo y dependencia que pide el enfoque de esta tarea: V1 es lo que un cliente pyme o empresa mediana de una sola sociedad va a necesitar en su primer o segundo ano de uso; V2/Enterprise (seccion 21) es lo que solo tiene sentido para un grupo corporativo, para integraciones externas o para canales que dependen de demanda validada.

## 20.1 Modulos completos que se incorporan en V1

| Modulo | Que llega en V1 | Razon dominante |
|---|---|---|
| MOD-010 Transferencias Internacionales | Registro manual de la transferencia (tratamiento, receptor, pais, base, finalidad), workflow de dos pasos (evaluacion de pais + aprobacion), cuestionario de evaluacion de pais receptor, vinculacion de consentimiento especifico, y exportacion de expediente con evidencia verificable | Riesgo: la cobertura parcial del MVP (tarea manual del diagnostico) ya es funcional pero no escala bien si la empresa tiene varios proveedores en el extranjero; demanda: casi toda empresa con proveedores de tecnologia/cloud tiene al menos un flujo hacia otro pais |
| MOD-012 Portal del Titular (version base) | Consulta publica del Aviso y la Politica vigentes, formulario de presentacion de solicitud ARCO-POL sin cuenta persistente, verificacion basica de identidad por documento adjunto, y consulta de estado por codigo de expediente | Demanda: reduce la carga operativa del Responsable ARCO-POL al evitar llamadas y correos de seguimiento; riesgo bajo porque la obligacion legal ya esta cubierta desde el MVP por el formulario interno (decision 2.7.30) |
| MOD-014 Riesgos y EIPD | Apertura automatica desde disparadores del Diagnostico y del RAT, cuestionario estructurado, seleccion de controles del catalogo compartido con MOD-015, flujo de aprobacion formal, con clasificacion de riesgo cualitativa simple (sin motor de calculo ponderado todavia) | Riesgo: el riesgo 7 de la seccion 11 del mapa senala que una empresa con biometria o videovigilancia desde el primer diagnostico queda sin este modulo en el MVP; dependencia: usa el catalogo de MOD-015 (ya MUST HAVE), por lo que su costo incremental es menor una vez ese catalogo existe |
| MOD-016 Retencion y Eliminacion | Motor de retencion de datos del titular con calculo de la fecha efectiva como maximo entre los fundamentos aplicables, mas el estado y la alerta basica; la propia ficha de MOD-016 concluye textualmente que esta es "la version minima de MOD-016 que justifica construirlo como modulo propio, para V1" | Dependencia: exige combinar catalogos legales fuera de la LPDP (Codigo de Comercio, Codigo Tributario, LCLDA) que hoy no viven en ningun otro modulo; riesgo medio porque OBL-RET-04 y OBL-RET-06 ya se cumplen de forma pasiva desde el MVP |
| MOD-018 Auditoria de Cumplimiento | Registro estructurado de ComplianceAudit (planificar, ejecutar, cerrar), registro de hallazgos con severidad y evidencia, plan de accion con tareas automaticas en MOD-021, cierre con aprobacion separada, e informe generado automaticamente al cerrar | Dependencia de tiempo: la primera auditoria formal (OBL-AUD-01) solo es exigible tras el primer anio de operacion de cada cliente, por lo que coincide de forma natural con el ciclo de vida de los primeros clientes del MVP |

## 20.2 Funcionalidades diferidas dentro de modulos MUST HAVE que llegan en V1

Agrupadas por tema, con el modulo de origen entre parentesis; el detalle fila por fila y su justificacion individual estan en la seccion Q de cada ficha citada.

- **Roles y permisos mas finos.** Roles personalizados con permisos granulares por modulo/accion, separacion de funciones con bloqueo automatico configurable por umbral de tamano, auditor externo con acceso temporal por invitacion (MOD-001).
- **Automatizacion de calculo de riesgo (primer nivel).** Calculo automatico de riesgo inicial del RAT (bajo/medio/alto) una vez exista suficiente base de tratamientos (MOD-006); deteccion de transferencia posiblemente no documentada por cruce RAT-Catalogo de Sistemas, una vez MOD-010 este activo (MOD-006); vinculacion estructurada de MOD-015 con MOD-010 para OBL-SEG-04; entidad Control compartida en tiempo real entre MOD-015 y MOD-014.
- **Cierre del ciclo de aprobacion y recalculo.** Recalculo automatico del Plan de Cumplimiento al cambiar respuestas del diagnostico o al confirmarse un cambio normativo (MOD-005); historial de versiones del plan navegable en pantalla, no solo exportable (MOD-005); asignacion de bloques del diagnostico a distintos responsables de area, con exportacion en PDF con hash (MOD-004).
- **Profundidad documental y de proveedores.** Exportacion con hash de integridad y wizard guiado por literal del Aviso de Privacidad (MOD-008); deteccion automatica de encargado no mencionado en el Aviso, y tarea automatica de revision de avisos tras el cambio de regimen de la reforma 659 (MOD-008); modelado de cadenas de subcontratacion de segundo nivel o mas, y tarea de verificacion de devolucion/eliminacion de datos al finalizar la relacion con un proveedor (MOD-009).
- **Profundidad de consentimiento.** Catalogo de excepciones al consentimiento (Art. 28 y Arts. 37-38), enlace automatico con la lista de supresion de marketing desde la oposicion ARCO-POL, reportes exportables avanzados con filtros (MOD-007).
- **Profundidad de ARCO-POL e incidentes.** Registro con plantilla dedicada para el reclamo ante la Direccion de Proteccion de Datos, mas alla del texto libre del MVP (MOD-011); referencia informativa al proveedor de origen y su plazo pactado de aviso, creacion automatica de tarea de EIPD hacia MOD-014, y flujo condicional completo del Decreto 143 para infraestructura critica (MOD-013).
- **Auditoria sustantiva y reportes.** Vinculo formal entre el cierre de MOD-018 y el informe periodico del Delegado (MOD-002, OBL-DPO-07); reportes exportables avanzados de MOD-015 (checklist, paquete de evidencia con verificacion de integridad).
- **Dashboard mas rico.** Estado del programa por etapa y por cluster (sintesis de alto nivel), vista alternativa por los 8 clusters legales, fotos periodicas de cierre mensual y reporte comparativo de tendencia, reportes exportables avanzados consolidados por area (MOD-020).
- **Notificaciones sin fatiga.** Reglas anti-fatiga (deduplicacion, resumen diario/semanal), horario silencioso configurable, reasignacion de destinatario por suplente (MOD-022).
- **Calendario mas fino.** Capa 5 (calendario propio de la autoridad, diferenciado del de la empresa frente al titular), capa 3 (asuetos locales por sede), configurabilidad del criterio de computo de las 72 horas (MOD-023).
- **Procedimiento Sancionador operativo.** Flujo operativo completo (vias simplificada/ordinaria, medidas provisionales, recursos, seguimiento de medidas adicionales), mas alla del registro manual del MVP (MOD-024).
- **Ayuda contextual mas confiable.** Sincronizacion automatica del contenido con la bandera de MOD-024, boton "necesito ayuda juridica" con tarea sugerida de evaluacion de asesoria externa, retroalimentacion "fue util / no fue util" con metricas de confusion (MOD-026).
- **Tareas mas flexibles.** Tareas recurrentes con periodicidad configurable, reportes exportables avanzados (historial de aprobaciones, paquete de tareas archivadas), dependencias entre tareas con validacion de ciclos (MOD-021).

## 20.3 Por que estas piezas, y no otras, entran primero

El criterio compartido en toda la seccion 20 es el mismo que separa V1 de V2/Enterprise en la seccion 21: demanda ya visible en el primer tramo de clientes del MVP (empresa privada de una sola sociedad, con o sin datos sensibles desde el primer diagnostico), riesgo de dejar una obligacion OBLIGATORIO o CONDICIONAL de alta severidad sin ninguna herramienta especializada, y dependencia de otro modulo que en el MVP todavia no tenia suficiente madurez (por ejemplo MOD-014 y MOD-015, o MOD-016 y el resto del sistema de documentos). Ninguna de las piezas de esta seccion depende de que exista una segunda sociedad, una integracion con un sistema externo del cliente, o un canal de comunicacion que hoy no forma parte del MVP: esas piezas, por definicion, pertenecen a la seccion 21.

---

# 21. V2 / Enterprise

Esta seccion agrupa lo que solo tiene sentido para un cliente corporativo con varias sociedades, para integraciones con sistemas externos al producto, o para canales y funcionalidades que dependen de una demanda que los primeros clientes del MVP y de V1 todavia no han validado. Fuente: las columnas COULD HAVE y FUTURE de la seccion Q de las 26 fichas, mas el perfil "Ana Gabriela Reyes Portillo" (Directora de Cumplimiento Corporativo) de `02_validacion/05_tipos_de_usuario.md`, seccion 5.1.

## 21.1 Multi-sociedad avanzada

Decision de alcance 2.7.31 de `02_validacion_de_la_idea.md`: la gestion de grupos empresariales con varias sociedades y delegado comun queda fuera del MVP y de V1 por completo; es la funcionalidad que define este nivel Enterprise.

- Gestion de grupo empresarial multi-sociedad (holding con varias razones sociales y delegado comun), y vision consolidada multi-sociedad del Dashboard (MOD-001, MOD-020).
- Delegado comun para grupos de sociedades (Art. 16 Lineamientos DPO) y multiples delegados propietarios simultaneos por especializacion (Art. 17 Lineamientos DPO) (MOD-002).
- Version multi-sociedad del RAT (comparar RAT entre varias empresas de un mismo grupo) (MOD-006).
- Plan de Cumplimiento consolidado multi-sociedad (MOD-005).
- Panel comparativo de transferencias por pais o por proveedor a nivel de grupo corporativo (MOD-010).
- Mapa de calor de riesgo consolidado multi-tratamiento o multi-sociedad (MOD-014).
- Vista consolidada de tareas y de calendario entre varias sociedades de un mismo grupo (MOD-021, MOD-023).
- Onboarding multi-sociedad o de grupo corporativo, en una sola sesion (MOD-003).

## 21.2 Integraciones

Las integraciones de este nivel se disenan siempre respetando los anti-features del producto (nunca ejecutar controles tecnicos, nunca actuar como SIEM ni como CRM): son integraciones de solo lectura o de sincronizacion de metadatos, nunca de ejecucion.

- Sincronizacion con sistemas externos de marketing o CRM (webhook) para reflejar la revocacion de consentimiento o la oposicion ARCO-POL en la lista de supresion del cliente (MOD-007); se disena con cuidado para no acercarse al anti-feature 1 (no ser un CRM).
- Integracion bidireccional con el canal oficial de la ACE, una vez la ACE lo habilite formalmente (hoy no existe, anti-feature 13) (MOD-013, MOD-024); mientras tanto, la empresa sigue confirmando y ejecutando cada envio.
- Integracion de solo lectura con herramientas reales de seguridad (por ejemplo, para autocompletar evidencia de un control ya existente) (MOD-015); debe disenarse con cuidado para no convertir el producto en un SIEM (anti-feature 2): el sistema sigue sin ejecutar ni monitorear en tiempo real, solo lee evidencia que otra herramienta ya genero.
- Integracion con un proveedor externo de e-learning o LMS (MOD-017): el sistema seguiria, como hoy, solo registrando la constancia que ese proveedor externo entrega; no se convierte en una plataforma de cursos (resolucion explicita del hallazgo 25 de `lente_inconsistencias.md`).

## 21.3 Portal del titular avanzado

Sobre la version base de MOD-012 que ya llega en V1 (seccion 20.1):

- Cuenta persistente del titular con historial de sus propias solicitudes.
- Marca visible personalizada por organizacion (logo, colores) y portal en mas de un idioma.
- Descarga de la resolucion final desde el Portal, con revision previa del Responsable Legal por posibles datos de terceros.
- Notificacion por correo de cambios de estado relevantes.
- Mensajeria o chat con el Responsable ARCO-POL dentro del Portal (exige disenar con cuidado la conservacion de evidencia de esas conversaciones).
- Verificacion de identidad biometrica o KYC electronico de terceros, siempre mediante un proveedor externo (anti-feature 9: el sistema no almacena datos biometricos de los titulares).
- Aplicacion movil nativa del Portal y kiosco fisico de autoservicio en sucursal.

## 21.4 Canales adicionales

- Notificaciones por Microsoft Teams, Slack, SMS o WhatsApp, ademas de plataforma y correo (MOD-022), sujeto a evaluacion de demanda real, seguridad de los datos que viajan por cada canal, y costo.
- Omnicanalidad automatizada para recibir solicitudes ARCO-POL (bot de WhatsApp, IVR telefonico), mas alla de los canales manuales ya cubiertos desde el MVP (correo, presencial, WhatsApp transcrito) (MOD-011).

## 21.5 Automatizaciones avanzadas

- Recalculo dinamico de riesgo del RAT con factores de volumen y ponderacion configurable por la propia empresa (MOD-006).
- Motor de scoring automatizado de riesgo de proveedores, mas alla del campo manual con cuestionario de apoyo (MOD-009).
- Reasignacion automatica de tareas por balanceo de carga entre responsables (MOD-021).
- Personalizacion completa de umbrales de semaforo del Dashboard para cada indicador del catalogo (MOD-020).
- Ponderacion configurable de los criterios de priorizacion del Plan de Cumplimiento por la propia empresa (MOD-005).
- Herramientas avanzadas de planificacion del Plan anual de Capacitacion (presupuesto, comparativa entre anios, plantillas por sector o tamano) (MOD-017).

Dos automatizaciones citadas por las fichas quedan senaladas aqui como bloqueadas por incertidumbre juridica, no solo diferidas por demanda, y no deben construirse hasta que esa base exista, conforme a la regla de "requiere validacion de asesoria juridica" de este blueprint:

- Integracion de scoring especifico de transferencias internacionales con un factor de riesgo propio del pais destino (MOD-014): depende de que exista un criterio o catalogo de "nivel de proteccion adecuado" bajo el Art. 44 que hoy no existe (incertidumbre 11 de `01_legal/03_hallazgos_regulatorios.md`); construirlo antes arriesga dar una falsa sensacion de calificacion legal, contra el anti-feature 18.
- Sugerencia automatica de riesgo del RAT por aprendizaje sobre el historico de tratamientos de la industria (MOD-006): la propia ficha la califica de "funcionalidad especulativa sin base normativa ni de producto validada"; no se adopta como compromiso de ninguna version, se menciona solo por completitud de la seccion Q de esa ficha.

## 21.6 Lo que no debe desarrollarse nunca

Remite integramente a `02_validacion/22_anti_features.md` (25 items razonados, con su alternativa funcional); esta seccion no repite esa lista. Un caso puntual detectado al escribir esta seccion se resuelve en favor de ese documento y se deja registrado en "Contradicciones y huecos detectados": la integracion tecnica que descubriera automaticamente sistemas y bases de datos de la empresa mediante escaneo de red o de esquemas (fila de `MOD-006_ficha.md`, seccion Q) no forma parte de esta seccion 21 ni de ninguna version futura del producto, porque su propia justificacion la describe como equivalente a un SIEM (anti-feature 2) y a una herramienta de descubrimiento tecnico que este producto no debe ejecutar.

---

## Contradicciones y huecos detectados

### Contradicciones

1. **`03_modulos/MOD-006_ficha.md`, seccion Q, fila "Integracion tecnica que descubra automaticamente sistemas y bases de datos de la empresa (escaneo de red o de esquemas)"** marca esta funcionalidad como FUTURE (columna con X), pero su propia justificacion dice textualmente que esta "fuera del alcance funcional de la fase actual y del principio de no ejecutar herramientas tecnicas de descubrimiento (mas cercano a un SIEM que a este producto, ver anti-feature 2)". Esto es inconsistente con el patron que el mismo corpus usa en otros casos identicos: `03_modulos/MOD-016_ficha.md`, seccion Q, fila "Integracion tecnica que ejecute la eliminacion real en los sistemas del cliente (purga automatizada)" describe una situacion equivalente (una funcionalidad prohibida por un anti-feature permanente, no solo diferida) y, coherente con eso, no marca ninguna columna (ni MUST, ni SHOULD, ni COULD, ni FUTURE), con la justificacion explicita "Fuera de alcance permanente (no es una fase futura, es un limite de producto)". Se adopta el criterio de `02_validacion/22_anti_features.md` (items 2 y 11) y el patron de MOD-016 por estar mas arriba en la jerarquia de fuentes (anti-features del producto sobre el detalle de una sola ficha): la funcionalidad de escaneo automatico de MOD-006 se trata en esta seccion como anti-feature permanente, no como elemento de V2/Enterprise (ver 21.6), y se recomienda corregir la columna de esa fila en `MOD-006_ficha.md` de FUTURE a ninguna columna marcada, para que quede consistente con MOD-016.
2. **Ningun otro caso de discrepancia sustantiva** se detecto entre las 26 fichas y `mapa_modulos.json` respecto de la clasificacion MVP a nivel de modulo completo: las 26 conclusiones de la seccion Q de cada ficha (el parrafo "Version minima vendible"/"Conclusion MVP") coinciden en el nombre exacto de la clasificacion (MUST HAVE, SHOULD HAVE o COULD HAVE) con el campo `mvp` de su entrada en `mapa_modulos.json`, verificado fila por fila para este documento.

### Huecos (piezas que ninguna ficha ni el mapa definen)

1. Las 26 fichas usan una sola columna "FUTURE" en su seccion Q, sin distinguir V1 de V2/Enterprise (salvo excepciones puntuales donde el texto lo dice literalmente, como la conclusion de `MOD-016_ficha.md`, "para V1"). La seccion 20 y la seccion 21 de este documento asignan cada funcionalidad diferida a V1 o a V2/Enterprise segun demanda, riesgo y dependencia (criterio propio de esta seccion, declarado en 20 y en el encabezado de 21), no segun una etiqueta que ya existiera en el corpus.
2. Ningun documento del corpus define un checklist de "criterios funcionales de salida a mercado" del producto completo (cada ficha define su propia version minima vendible por modulo, pero no existe una condicion de cierre transversal). La seccion 19.6 de este documento es una propuesta nueva, marcada como tal.
3. Ninguna ficha ni `06_mapa_definitivo_de_modulos.md` proponen un orden de construccion explicito entre los 20 modulos MUST HAVE: `depende_de` es, segun aclara la propia seccion 6.1 de ese documento, un grafo de dependencia de datos y servicios, no de secuencia de desarrollo. La secuencia de la seccion 19.9 (incluyendo la decision de construir MOD-021, MOD-022 y MOD-019 como infraestructura desde el inicio, pese a que su `depende_de` liste modulos de proceso posteriores) es una propuesta de esta seccion.
4. El riesgo 5 de la seccion 11 de `06_mapa_definitivo_de_modulos.md` senala como pendiente de validar la relacion entre 20 modulos MUST HAVE y un "producto minimo vendible" real, pero ningun documento propone una subdivision concreta en un nucleo vendible mas pequeno. La propuesta de la seccion 19.8 (nucleo vendible de 10 modulos mas un segundo grupo de otros 10) es nueva y no reclasifica ningun modulo.
5. El perfil de cliente objetivo especifico del MVP (distinto del perfil general del producto, que si incluye grupos corporativos) no esta definido como tal en ningun documento; se deriva en la seccion 19.7 de `04_objetivo_exacto_del_producto.md` seccion 1.1 mas la exclusion de multi-sociedad de la decision 2.7.31 de `02_validacion_de_la_idea.md`.
6. Ninguna ficha desarrolla que sucede con la ayuda contextual (MOD-026) de un modulo SHOULD HAVE o COULD HAVE mientras ese modulo no esta activo (por ejemplo, el contenido de ayuda de MOD-010 o MOD-014 antes de que existan como modulo propio en una version dada del producto); esta seccion asume, sin que ninguna ficha lo diga de forma expresa, que el catalogo de MOD-026 crece junto con cada modulo cuando este se libera (ver nota de la capa de infraestructura transversal en 19.9), lo cual queda marcado aqui como supuesto propio, no como decision ya tomada por la ficha de MOD-026.
