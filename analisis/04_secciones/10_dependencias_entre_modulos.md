# 10. Dependencias entre modulos

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (prohibido codigo, SQL, APIs, esquemas de base de datos, nombres de tecnologias, stack o infraestructura).

Esta seccion consolida y cruza lo ya decidido en `02_validacion/mapa_modulos.json`, `02_validacion/06_mapa_definitivo_de_modulos.md` y la seccion L (Dependencias) y G (Automatizaciones) de las 26 fichas de `03_modulos/`. No inventa funcionalidades que ninguna ficha defina: cuando algo falta y el prompt del cliente lo exige, se marca explicitamente "propuesta de esta seccion, no presente en las fichas". Cuando una ficha ya senalo una diferencia entre `mapa_modulos.json` y su propio diseno, esta seccion no repite ambas versiones en el cuerpo del documento: adopta la version verificada por la ficha (que en estos casos coincide con otra ficha independiente, nunca es una opinion aislada) y dejala anotada en la seccion final "Contradicciones y huecos detectados", con la correccion propuesta al mapa.

Convencion de identificadores: todo OBL-ID citado es el identificador canonico de `01_legal/matriz_obligaciones.json` (formato OBL-AREA-NN, 105 obligaciones), nunca los IDs preliminares de `01_legal/03_hallazgos_regulatorios.md`. Los 12 roles citados son los de `02_validacion/05_tipos_de_usuario.md`, seccion 5.3, con su nombre exacto.

---

## 10.1 Reglas de dependencia

Estas reglas ya estan decididas en `06_mapa_definitivo_de_modulos.md` (secciones 4 y 6.1); esta seccion las enuncia de forma operativa porque son la base de lectura de la matriz y de los diagramas que siguen.

**Regla 1. Dos listas, no una: `depende_de` y `alimenta_a`.** Cada modulo declara en `mapa_modulos.json` de que modulos necesita datos o servicios (`depende_de`, dependencia estructural minima de construccion, la que ordena el recorrido y los diagramas de esta seccion) y a que modulos entrega datos (`alimenta_a`, lista mas amplia por diseno: "quien consume esto"). Regla de consistencia verificada mecanicamente: si Y aparece en el `depende_de` de X, entonces X aparece siempre en el `alimenta_a` de Y, sin excepciones. La implicacion inversa no es obligatoria: `alimenta_a` puede listar destinatarios adicionales sin que el modulo consumidor declare esa lectura como dependencia estructural propia.

**Regla 2. Asimetria intencional de las tres fuentes transversales de referencia constante.** MOD-001 (identidad de organizacion, usuarios y roles), MOD-023 (calendario y plazos) y MOD-024 (estado normativo vigente) alimentan a practicamente todos los modulos sin que cada consumidor declare esa lectura como dependencia estructural propia, porque son servicios de referencia constante, no eventos puntuales de negocio. Esta seccion (10.2, nota final) documenta que el mismo patron aplica en sentido inverso a MOD-021 Centro de Tareas, que recibe eventos de generacion de tarea de practicamente todo modulo de proceso, aunque el mapa definitivo no declaro explicitamente esta asimetria como excepcion para un modulo receptor (ver "Contradicciones y huecos detectados").

**Regla 3. Direccion unica entre modulos de proceso.** Cuando un modulo de proceso (por ejemplo MOD-009 Proveedores, MOD-016 Retencion) referencia un dato de otro (MOD-006 RAT, MOD-008 Documentos), esa referencia es de lectura; el modulo que crea el dato original sigue siendo su unico propietario y nunca hay dos copias del mismo campo mutandose por separado.

**Regla 4. Capa transversal: consultada, nunca consulta al reves.** Ningun modulo de la barra transversal (MOD-021 a MOD-026) escribe hacia un modulo de recorrido (MOD-001 a MOD-020); todo modulo de recorrido escribe hacia los transversales, nunca al reves. Dentro de la barra: MOD-021 es el unico lugar donde una obligacion se vuelve tarea con responsable y fecha; MOD-022 solo reacciona a eventos que le entregan MOD-021 y MOD-023, nunca a un modulo de recorrido de forma directa (con la excepcion puntual de MOD-011 y MOD-013, que le entregan directamente sus propios cronometros de grano mas fino, ver 10.3); MOD-023 es el unico que calcula dias u horas habiles; MOD-024 es el unico que decide que version de una regla o que estado del regimen de la reforma 659 esta activo; MOD-025 y MOD-026 son de solo lectura, nunca generan tareas ni escriben en otro modulo.

**Regla 5. Excepcion reciproca unica: MOD-018 / MOD-019.** Leido como grafo de orden estricto de construccion, `depende_de` es aciclico en los 26 modulos salvo un solo par: MOD-018 Auditoria de Cumplimiento y MOD-019 Centro de Evidencias se declaran mutuamente en su `depende_de`. No es un error de copia: MOD-018 consulta la evidencia acumulada en MOD-019 (recibida de MOD-007 a MOD-017 de forma continua) para elaborar sus hallazgos de auditoria, y el informe y los hallazgos resultantes de MOD-018 se registran a su vez como nueva evidencia en MOD-019. Es una dependencia de datos bidireccional y continua entre los dos modulos de la etapa Demostrar, no una precedencia de inicializacion; ningun otro par del mapa tiene esta relacion.

**Regla 6. El doble estado de la reforma 659 no crea aristas nuevas de negocio, solo un evento de bandera.** MOD-024 aloja la bandera manual `regimen_reforma_659` (ACTUAL | FUTURO). El cambio de bandera no es un flujo de datos de negocio: es un evento de sistema que MOD-024 emite hacia los modulos cuyas obligaciones estan afectadas (ver 10.4), sin que ningun modulo evalue por si mismo si la reforma esta vigente.

---

## 10.2 Matriz de dependencias de los 26 modulos

Fuente primaria de las columnas `depende_de` y `alimenta_a`: `02_validacion/mapa_modulos.json` (verificado 105/105 contra `01_legal/matriz_obligaciones.json`, seccion 8 de `06_mapa_definitivo_de_modulos.md`). Las columnas "Recibe" y "Entrega" resumen la seccion L (Dependencias) de cada ficha de `03_modulos/`, que detalla que dato o evento concreto viaja por cada arista. La columna "Diferencia detectada" marca, con el codigo Dn, cada caso en que una ficha ya escrita declara una relacion que el JSON no refleja (o al reves); el detalle y la correccion propuesta para cada Dn estan en la seccion "Contradicciones y huecos detectados", al final de este documento.

| Cod | Nombre | depende_de (JSON) | alimenta_a (JSON) | Recibe (resumen, seccion L de la ficha) | Entrega (resumen, seccion L de la ficha) | Dif. |
|---|---|---|---|---|---|---|
| MOD-001 | Organizacion y Personas | MOD-003 | MOD-002 a MOD-026 (todos) | De MOD-003: alta inicial de organizacion, usuarios y roles | A casi todos: identidad de organizacion, catalogo de usuarios, catalogo de roles (RBAC), consultados por referencia constante (regla 2) | - |
| MOD-002 | Delegado / Responsable Interno de Datos | MOD-001, MOD-024 | MOD-007, MOD-008, MOD-011, MOD-017, MOD-018, MOD-021, MOD-023, MOD-024 | De MOD-001: identidad y estructura; de MOD-024: bandera `regimen_reforma_659`; de MOD-023 (no declarado en `depende_de`, ver D1): calculo de dias/horas habiles para sus contadores de 3, 10 y 15 dias y 1, 3 y 5 anos | A MOD-007: destinatario de revocacion; a MOD-008: contacto publicado; a MOD-011: responsable del tramite; a MOD-017: capacitacion especifica; a MOD-018: informes periodicos; a MOD-021: tareas; a MOD-024: tramite de nombramiento (ACEFiling) | D1 |
| MOD-003 | Onboarding | (ninguno, punto de entrada) | MOD-001, MOD-002, MOD-004 | De un evento externo al analisis funcional (alta comercial de la cuenta) | A MOD-001: datos de empresa y usuarios; a MOD-002: registro inicial del Delegado si aplica; a MOD-004: disparo de inicio del diagnostico | - |
| MOD-004 | Diagnostico de Cumplimiento | MOD-003 | MOD-005, MOD-006, MOD-008, MOD-014, MOD-021 | De MOD-003: disparo de inicio; de MOD-001 (indirecto, via MOD-003): sector y sucursales | A MOD-005: obligaciones aplicables que siembran el plan; a MOD-006: tratamientos borrador; a MOD-008: documentos sugeridos; a MOD-014: EIPD sugeridas; a MOD-021: tareas | - |
| MOD-005 | Plan de Cumplimiento | MOD-004 | MOD-021, MOD-020 | De MOD-004: obligaciones aplicables ya calculadas; de MOD-001: catalogo de usuarios/areas/roles para asignar responsables | A MOD-021: una tarea por accion Pendiente; a MOD-020: indicadores de avance del plan | D2 |
| MOD-006 | RAT y Mapa de Datos | MOD-004 | MOD-007, MOD-008, MOD-009, MOD-010, MOD-013, MOD-014, MOD-015, MOD-016, MOD-018 | De MOD-004: tratamientos borrador; de MOD-001: catalogo de areas/usuarios; de MOD-009: catalogo de proveedores tipo Encargado; de MOD-015: catalogo de controles | A los nueve modulos del `alimenta_a`, todos por lectura de referencia (tratamiento, base juridica, categoria de dato, finalidad, catalogo de sistemas) | - |
| MOD-007 | Consentimiento | MOD-006, MOD-008 | MOD-009, MOD-011, MOD-019 | De MOD-006: tratamiento, base juridica, categoria de dato, finalidad; de MOD-008: version vigente del Aviso | A MOD-009: tarea de notificacion de revocacion; a MOD-011: lista de supresion y verificacion de identidad compartida; a MOD-019: evidencia continua | - |
| MOD-008 | Documentos y Politicas | MOD-004, MOD-006 | MOD-007, MOD-009, MOD-012, MOD-016, MOD-019 | De MOD-004: necesidad de documentos; de MOD-006: finalidades y cambios que exigen revisar el Aviso; de MOD-009: lista de encargados (literal h); de MOD-024 (no declarado en `alimenta_a` de MOD-024, ver D3): evento "cambio de bandera" que dispara la tarea de revision de avisos | A MOD-007: version exacta del Aviso; a MOD-009: motor documental para Contrato/DPA; a MOD-012: Aviso publicado; a MOD-016: reglas de retencion documental; a MOD-019: evidencia de version, aprobacion y publicacion | D3 |
| MOD-009 | Proveedores y Encargados | MOD-006 | MOD-008, MOD-010, MOD-019 | De MOD-006: tratamientos, categorias de datos, catalogo de sistemas (solo lectura); eventos puntuales de MOD-007 (revocacion), MOD-011 (rectificacion/eliminacion), MOD-013 (incidente grave) | A MOD-008: Contrato/DPA como tipo de documento; a MOD-010: registro "pendiente de confirmar" si el pais no es El Salvador; a MOD-019: evidencia continua; a MOD-021 (no declarado en `alimenta_a`, ver D6): tareas de vencimiento de contrato, revision periodica, notificacion a encargado/receptor y verificacion de devolucion/eliminacion | D6 |
| MOD-010 | Transferencias Internacionales | MOD-006, MOD-009 | MOD-007, MOD-015, MOD-019, MOD-024 | De MOD-001: estructura de la organizacion; de MOD-006: tratamiento de origen; de MOD-009: receptor, rol, contrato; de MOD-004: senal "datos fuera de El Salvador" | A MOD-007: consentimiento especifico exigido; a MOD-015: evidencia de salvaguardas tecnicas; a MOD-019: expediente; a MOD-024: borrador de puesta en conocimiento a la ACE (ACEFiling); MOD-011 lee (no escribe) sus transferencias activas | - |
| MOD-011 | ARCO-POL | MOD-012, MOD-007, MOD-002 | MOD-009, MOD-010, MOD-019, MOD-021, MOD-022, MOD-023, MOD-024 | De MOD-012: solicitudes del canal publico (si existe); de MOD-007: version del aviso, sub-flujo NNA, lista de supresion; de MOD-002: aprobador por defecto del acto legal; lecturas de referencia de MOD-001 y MOD-006 (no declaradas como `depende_de` estructural, coherente con la regla 2) | A MOD-009/MOD-010: lista de receptores a notificar; a MOD-019: expediente completo; a MOD-021: tareas; a MOD-022: alertas de cronometro propio; a MOD-023: calculo de todos sus plazos habiles; a MOD-024: reclamo ante la Direccion de Proteccion de Datos | - |
| MOD-012 | Portal del Titular | MOD-008 | MOD-011, MOD-019, MOD-023 | De MOD-008: Aviso y Politica vigentes (solo lectura) | A MOD-011: crea la Solicitud (nunca resuelve ni modifica el expediente); a MOD-019: comprobantes, bitacora de accesos; a MOD-023: lectura del plazo aplicable para mostrar al titular | - |
| MOD-013 | Incidentes de Seguridad | MOD-006, MOD-015 | MOD-019, MOD-021, MOD-022, MOD-023, MOD-024 | De MOD-006: tratamiento y sistema afectado, si el dato es sensible; de MOD-015: catalogo de controles existentes; referencia informativa de MOD-009 (proveedor de origen, sin arista formal) | A MOD-019: expediente y constancias de envio; a MOD-021: tareas de investigacion/notificacion/remediacion; a MOD-022: alertas de cronometro propio; a MOD-023: calculo de las 72 horas; a MOD-024: bandera de infraestructura critica (Decreto 143); a MOD-016 (no declarado en `alimenta_a`, ver D4): fecha de cierre para la regla de retencion del expediente | D4 |
| MOD-014 | Riesgos y EIPD | MOD-004, MOD-006 | MOD-015, MOD-019, MOD-021 | De MOD-004: deteccion automatica de tratamiento de alto riesgo; de MOD-006: ficha del tratamiento, categorias, base juridica | A MOD-015: seleccion o creacion de controles del catalogo unico; a MOD-019: expediente y paquete exportado; a MOD-021: tareas de cuestionario, mitigacion y aprobacion | - |
| MOD-015 | Controles de Seguridad | MOD-006, MOD-010 | MOD-013, MOD-014, MOD-018, MOD-019 | De MOD-006: catalogo de sistemas y tratamientos a los que vincular un control; de MOD-010: contexto de transferencias para el bloque OBL-SEG-04 | A MOD-013: contexto de que controles existian sobre el sistema afectado; a MOD-014: entidad Control compartida; a MOD-018: checklist e insumo de la auditoria; a MOD-019: evidencia con hash, version y fecha | - |
| MOD-016 | Retencion y Eliminacion | MOD-006, MOD-008 | MOD-011, MOD-019 | De MOD-006: tratamientos, categorias, finalidad; de MOD-008: avisos publicados y sus versiones; de MOD-011 y MOD-013 (no declarado en `depende_de`, ver D4): fecha de cierre de expediente ARCO-POL o de incidente, necesaria para la automatizacion G.3 (OBL-RET-05) | A MOD-011: consulta si un dato esta retenido antes de resolver cancelacion u olvido; a MOD-019: evidencia de reglas y eliminaciones | D4 |
| MOD-017 | Capacitacion | MOD-001, MOD-002 | MOD-019, MOD-020 | De MOD-001: altas, bajas y cambios de rol que disparan induccion; de MOD-002: identidad de quien ocupa hoy el rol Delegado/Responsable interno | A MOD-019: evidencia de constancias y del Plan anual; a MOD-020: indicadores; colaboracion conceptual sin arista declarada con MOD-002 (notifica constancia nueva) y con MOD-013 (leccion aprendida sugiere capacitacion) | - |
| MOD-018 | Auditoria de Cumplimiento | MOD-006, MOD-015, MOD-019 | MOD-019, MOD-020, MOD-021 | De MOD-006: tratamientos vigentes del checklist; de MOD-015: catalogo de controles y su estado; de MOD-019: evidencia ya acumulada (relacion reciproca, regla 5) | A MOD-019: informe y hallazgos como nueva evidencia; a MOD-020: indicadores; a MOD-021: tarea por cada accion del plan de accion; vinculo indirecto sin arista declarada hacia MOD-002 (insumo de OBL-DPO-07) | - |
| MOD-019 | Centro de Evidencias | MOD-007 a MOD-018 (los 12) | MOD-018, MOD-020, MOD-024 | De MOD-007 a MOD-018: evidencia entregada de forma continua conforme cada modulo aprueba, cierra o publica un registro (relacion reciproca con MOD-018, regla 5) | A MOD-018: evidencia acumulada para sus hallazgos; a MOD-020: indicadores de evidencia disponible, huecos y vencimientos; a MOD-024: paquetes de evidencia para procedimiento sancionador y tramites ante la ACE | - |
| MOD-020 | Dashboard y Reportes | MOD-005, MOD-019, MOD-021 | (ninguno, modulo terminal de lectura) | Dependencia estructural minima: MOD-005 (avance del plan), MOD-019 (evidencia disponible), MOD-021 (pendientes y vencidos); consumo real mas amplio (no estructural, ver D5): indicadores y reportes de los 24 modulos restantes por su propia seccion M/N | Ninguno hacia otro modulo (drill-down hacia el modulo de origen no es escritura) | D5 |
| MOD-021 | Centro de Tareas | MOD-004, MOD-005, MOD-011, MOD-013, MOD-002 | MOD-022, MOD-023, MOD-020 | De los cinco declarados, mas MOD-014 y MOD-018 (declarados como "Sale hacia MOD-021" en sus propias fichas pero ausentes del `depende_de` de MOD-021, ver D6); consulta (no crea tareas) a MOD-023 y MOD-001 | A MOD-022: eventos de tarea/aprobacion; a MOD-023: solicitud de calculo de plazo; a MOD-020: indicadores agregados | D6 |
| MOD-022 | Notificaciones | MOD-021, MOD-023, MOD-011, MOD-013 | (ninguno, modulo terminal de lectura) | De MOD-021: eventos de tarea/aprobacion; de MOD-023: eventos de plazo sin tarea previa; de MOD-011 y MOD-013: cronometros propios de grano fino (unica excepcion a la regla 4) | Ninguno hacia otro modulo; su unica salida es el destinatario resuelto (usuario interno) | - |
| MOD-023 | Calendario y Motor de Plazos | (ninguno) | MOD-002, MOD-011, MOD-013, MOD-021, MOD-022, MOD-024 | Ninguna dependencia estructural; su unica entrada es la configuracion del equipo del producto y de la empresa (calendario nacional y propio) | A los seis declarados, mas consumo adicional documentado por otras 9 fichas (MOD-006 a MOD-010, MOD-012, MOD-014 a MOD-016, MOD-018) segun la asimetria de la regla 2 | - |
| MOD-024 | Centro Regulatorio | (ninguno) | MOD-002, MOD-007, MOD-008, MOD-011, MOD-015, MOD-017, MOD-021 | De MOD-023 (broad source, sin declarar): calculo de plazos del procedimiento sancionador; de MOD-002 y MOD-010 (no declarados en `depende_de`, ver D7): eventos de tramite de nombramiento y de puesta en conocimiento de transferencia; de MOD-011 y MOD-013 (consulta informativa, sin arista de negocio): reclamos e infraestructura critica | A los siete del `alimenta_a` (incluye MOD-008 pese a no estar declarado explicitamente en el JSON de MOD-024, ver D3): bandera de doble estado, eventos de cambio normativo y del procedimiento sancionador | D3, D7 |
| MOD-025 | Busqueda Global | (ninguno) | (ninguno) | Ninguna dependencia estructural declarada; en la practica lee metadatos indexables de MOD-002, MOD-004 a MOD-020, MOD-024 y MOD-026 (consumo de solo lectura, ver D5 y Regla 2) | Ninguno (modulo terminal de solo lectura) | - |
| MOD-026 | Centro de Ayuda | (ninguno) | (ninguno) | Ninguna dependencia estructural declarada; en la practica consulta MOD-001 (roles/permisos) y MOD-024 (bandera y catalogo OBL-ID) | Ninguno declarado en el JSON; en la practica alimenta el contenido indexable de MOD-025 y la ayuda contextual de MOD-003, MOD-006, MOD-008, MOD-009, MOD-012, MOD-014, MOD-015, MOD-018, MOD-019 (ver D5) | D5 |

Nota de lectura de la columna "Dif.": los codigos Dn remiten a la seccion final de este documento, donde se detalla que dice cada fuente, cual version adopta este documento y por que. Ningun Dn implica que el diseno funcional descrito en la ficha este equivocado: en todos los casos la ficha propietaria y al menos otra ficha independiente coinciden entre si; lo que difiere es el registro de esa relacion en `mapa_modulos.json`.

---

## 10.3 Catalogo de eventos entre modulos

Tomado de la seccion G (Automatizaciones) y L (Dependencias) de cada ficha de `03_modulos/`. Se listan los eventos que cruzan de un modulo a otro (no las validaciones internas de un solo modulo). La columna "Efecto" usa siempre uno de: tarea, alerta, calculo de plazo, evidencia, cambio de estado (nunca "cumplimiento legal X%", regla no negociable 5). La columna "Fundamento" cita OBL-ID y articulo cuando el evento instrumenta una obligacion legal; queda en blanco cuando es una regla operativa sin fundamento legal directo (opinion de producto).

### 10.3.1 Etapas Empezar a Planificar

| Evento | Modulo emisor | Modulo(s) receptor(es) | Efecto | Fundamento |
|---|---|---|---|---|
| Organizacion pasa a ACTIVA | MOD-001 | MOD-003, MOD-004 | Cambio de estado; habilita el paso siguiente | - |
| Alta de usuario con rol Delegado, o respuesta "ya designado/designarlo ahora" en el wizard | MOD-003 | MOD-002, MOD-023 | Cambio de estado (registro "designacion en curso"); calculo de plazo (siembra el contador de 15 dias habiles) | OBL-DPO-03, Art. 15/17 |
| Onboarding pasa a COMPLETADO | MOD-003 | MOD-004, MOD-021 | Tarea ("Completar el Diagnostico") | - |
| Registro del Delegado pasa a NOMBRADO | MOD-002 | MOD-021, MOD-023 | Tarea ("Notificar al Delegado su nombramiento"); calculo de plazo (fecha_nombramiento + 3 dias habiles) | Art. 15/17 |
| Registro del Delegado pasa a NOTIFICADO_INTERNAMENTE | MOD-002 | MOD-021, MOD-024 | Tarea ("Comunicar el nombramiento a la ACE"); evidencia (tramite pendiente ACEFiling en MOD-024) | OBL-DPO-03 |
| Se registra fecha_cese del Delegado | MOD-002 | MOD-021 | Tarea ("Designar sustituto", 10 dias habiles) | Art. 19 |
| Cuestionario del Diagnostico se cierra | MOD-004 | MOD-006, MOD-008, MOD-014, MOD-021, MOD-005 | Cambio de estado (tratamientos en Borrador); tarea (por cada disparador de la tabla G.2); evidencia (registro de respuestas) | OBL-DOC-02, OBL-AVISO-01, OBL-PLAZO-03/04 (segun la fila) |
| Detecta senal "trata datos fuera de El Salvador" | MOD-004 | MOD-021 (tarea manual, cobertura parcial mientras MOD-010 no este completo) | Tarea ("registrar la transferencia como pendiente de confirmar") | OBL-TRANSF-01, OBL-TRANSF-03 |
| Diagnostico completado, primera version del plan | MOD-004 | MOD-005 | Cambio de estado (plan generado) | - |
| Version del plan aprobada como Vigente | MOD-005 | MOD-021, MOD-020 | Tarea por cada accion Pendiente; indicador de avance | - |
| Cambio en el conjunto de obligaciones aplicables (re-diagnostico) | MOD-004 | MOD-005 | Cambio de estado (plan pasa a Recalculando) | - |

### 10.3.2 Etapa Registrar

| Evento | Modulo emisor | Modulo(s) receptor(es) | Efecto | Fundamento |
|---|---|---|---|---|
| Se marca categoria de dato sensible en una ficha del RAT | MOD-006 | MOD-014 (sugerencia EIPD), MOD-008 (aviso especifico) | Alerta; tarea | OBL-SENS-01, Art. 4 lit. g |
| Se marca "Informacion biometrica" | MOD-006 | MOD-007, MOD-014 | Tarea ("confirmar consentimiento escrito y alternativa no biometrica") | OBL-SENS-06, OBL-SENS-07 |
| Ficha de tratamiento pasa a Vigente con transferencia no documentada | MOD-006 | MOD-010, MOD-021 | Alerta ("transferencia posiblemente no documentada"); tarea | OBL-TRANSF-01 |
| Ficha de tratamiento pasa a Vigente con "Requiere EIPD: Si" | MOD-006 | MOD-014 | Tarea ("elaborar EIPD") | OBL-DOC-03 |
| RAT marca tratamiento con base juridica = Consentimiento | MOD-006 | MOD-007 | Tarea ("capturar consentimiento") | - |
| Se otorga un nuevo consentimiento para una finalidad ya vigente | MOD-007 | MOD-007 (interno, no cruza modulo) | Cambio de estado (archiva el anterior como Sustituido) | - |
| Se registra una revocacion de consentimiento | MOD-007 | MOD-023, MOD-021 | Calculo de plazo (5 dias habiles); tarea al Responsable ARCO-POL y al Delegado | Art. 30 |
| Revocacion ejecutada con encargado registrado | MOD-007 | MOD-009 | Calculo de plazo (5 dias habiles adicionales); tarea de notificacion | OBL-CONS-03, Art. 30 |
| Revocacion sobre finalidad de marketing directo | MOD-007 | MOD-011 (lista de supresion) | Cambio de estado (titular anadido a lista de supresion) | - |
| MOD-006 registra finalidad nueva sobre datos ya recolectados | MOD-006 | MOD-008 | Tarea ("Actualizar Aviso de Privacidad"); cambio de estado (REQUIERE_REVISION) | OBL-AVISO-04, Art. 7 |
| MOD-009 registra o modifica un Encargado | MOD-009 | MOD-008 | Tarea de revision del aviso (literal h); cambio de estado | OBL-AVISO-02, OBL-PROV-04 |
| Version de documento con todas las aprobaciones completas | MOD-008 | MOD-019 | Evidencia (hash de integridad, evidencia de aprobacion) | - |
| Pais del proveedor distinto de El Salvador | MOD-009 | MOD-010 | Cambio de estado (registro DETECTADA_PENDIENTE_DE_CONFIRMAR); tarea | Incertidumbre 10 (encargado extranjero vs. transferencia) |
| Fecha de vencimiento de contrato de proveedor a 30/7 dias | MOD-009 | MOD-021 | Alerta WARNING/HIGH; tarea | - |
| MOD-013 vincula incidente Alto/Critico a un proveedor | MOD-013 | MOD-009 | Cambio de estado (proveedor pasa a SUSPENDIDO); alerta | - |
| Transferencia pasa a PENDIENTE_DE_APROBACION (tipo Internacional) | MOD-010 | MOD-024 | Evidencia/tramite (borrador de ACEFiling precargado) | Art. 45 |
| Base juridica de transferencia = Consentimiento previo sin registro vinculado | MOD-010 | MOD-007 | Bloqueo de estado; tarea ("capturar consentimiento especifico") | OBL-TRANSF-04, Art. 40 |
| Rectificacion/cancelacion/oposicion/portabilidad/olvido/limitacion aprobada con transferencias activas | MOD-011 | MOD-010, MOD-009 | Tarea ("notificar al receptor", 5 dias habiles) | OBL-ARCO-11, Art. 21 inc. 3 |

### 10.3.3 Etapa Operar: relacion con el titular, seguridad y ciclo de vida

| Evento | Modulo emisor | Modulo(s) receptor(es) | Efecto | Fundamento |
|---|---|---|---|---|
| Formulario del Portal completo con identidad adjunta | MOD-012 | MOD-011 | Cambio de estado (Solicitud creada, estado Recibida) | Art. 18 |
| Solicitud ARCO-POL con los 7 elementos del Art. 18 completos | MOD-011 | MOD-023, MOD-021 | Calculo de plazo (20 dias habiles); cambio de estado (Admitida) | OBL-ARCO-01, Art. 18/20 |
| Solicitud incompleta | MOD-011 | MOD-023, MOD-021 | Calculo de plazo (10 dias habiles de prevencion); tarea | Art. 18 |
| Vence prevencion sin subsanacion | MOD-011 | MOD-021, MOD-022 | Cambio de estado (Archivada); alerta | Art. 18 |
| Se determina procedencia de rectificacion/cancelacion/olvido con receptor vinculado | MOD-011 | MOD-009, MOD-010, MOD-023 | Calculo de plazo (5 dias habiles); tarea de notificacion | OBL-ARCO-11, Art. 21 |
| Se declara incompetencia | MOD-011 | MOD-023, MOD-021 | Calculo de plazo (5 dias habiles); tarea | Art. 19 |
| Expediente ARCO-POL pasa a Cerrada | MOD-011 | MOD-016, MOD-019 | Calculo de plazo (fecha de retencion sugerida, cierre + 5 anos); evidencia | OBL-RET-05 |
| Reclamo del titular ante la Direccion de Proteccion de Datos | MOD-011 | MOD-024, MOD-021 | Cambio de estado (enlace en panel de Denuncias); tarea ("preparar informe de actuaciones") al Delegado | OBL-ARCO-14 |
| Oposicion a mercadotecnia directa reconocida | MOD-011 | MOD-007 | Cambio de estado (titular a lista de supresion) | - |
| Se registra fecha de conocimiento de una vulneracion | MOD-013 | MOD-023, MOD-021, MOD-022 | Calculo de plazo (cronometro de 72h de notificacion y de revision, en paralelo); tarea; alerta | Art. 25 |
| Cronometro de notificacion llega a 0 (72h) sin notificacion enviada | MOD-013 | MOD-021, MOD-022 | Alerta CRITICAL; marca el hito vencido de forma permanente | Art. 25 |
| Se marca "existe riesgo = Si" en un incidente | MOD-013 | MOD-013 (bloqueo interno hasta completar campos) | Cambio de estado (bloqueo de avance) | OBL-INC-04, Art. 25 inc. final |
| Categorias de datos del incidente = Biometrica o Salud, sin EIPD registrada | MOD-013 | MOD-014 | Tarea ("evaluar si corresponde EIPD") | - |
| Se cierra un incidente | MOD-013 | MOD-016, MOD-019, MOD-017 (leccion aprendida, sin arista estructural) | Calculo de plazo (fecha de conservacion del expediente); evidencia (cierre con responsable y justificacion); tarea sugerida de capacitacion | OBL-RET-05, OBL-PRIN-03 |
| Medida correctiva nueva propuesta en "Lecciones aprendidas" | MOD-013 | MOD-015 | Cambio de estado (crea o actualiza un Control) | - |
| Riesgo calculado Alto o Critico sin mitigacion | MOD-014 | MOD-015, MOD-021 | Bloqueo de estado; tarea de mitigacion | - |
| EIPD aprobada (pasa a VIGENTE) | MOD-014 | MOD-019, MOD-023 | Evidencia de aprobacion; calculo de plazo (proxima revision, 12 meses) | - |
| Tratamiento vinculado a una EIPD se marca inactivo en el RAT | MOD-006 | MOD-014 | Cambio de estado (EIPD pasa a ARCHIVADA) | - |
| Se marca Implementado un control | MOD-015 | MOD-023 | Calculo de plazo (proxima fecha de revision) | - |
| Vence la fecha de revision de un control sin accion | MOD-015 | MOD-021, MOD-020 (indicador de riesgo sancionador) | Cambio de estado (Vencido); alerta | - |
| Se publica nueva version del Aviso de Privacidad | MOD-008 | MOD-016 | Cambio de estado (crea regla de retencion documental, 10 anos) | OBL-RET-04 |
| Expediente ARCO-POL o de incidente cambia a "cerrado" | MOD-011, MOD-013 | MOD-016 | Cambio de estado (crea/actualiza regla de retencion documental, cierre + 5 anos) | OBL-RET-05 |
| Se cumple la fecha efectiva de una regla de retencion | MOD-016 | MOD-021, MOD-022 | Cambio de estado (LISTO PARA ELIMINAR); alerta HIGH; tarea de aprobacion | - |
| Solicitud de cancelacion u olvido sobre dato RETENIDO POR OBLIGACION | MOD-016 | MOD-011 | Evidencia (borrador de denegatoria parcial motivada para revision del Delegado) | Art. 22, OBL-ARCO-06 |
| Alta de usuario nuevo en MOD-001 | MOD-001 | MOD-017, MOD-021 | Tarea (induccion de personal nuevo, TrainingRecord Programada) | OBL-CAP-01 |
| TrainingRecord del Delegado completado | MOD-017 | MOD-002 | Evidencia (notificacion de constancia disponible para `fecha_ultima_capacitacion_delegado`) | OBL-DPO-05 |

### 10.3.4 Etapa Demostrar y capa transversal

| Evento | Modulo emisor | Modulo(s) receptor(es) | Efecto | Fundamento |
|---|---|---|---|---|
| Modulo estructurado (MOD-007 a MOD-018) aprueba, cierra o publica un registro con evidencia segun el catalogo D.0 | MOD-007 a MOD-018 | MOD-019 | Evidencia (registro automatico, estado Disponible) | OBL-PRIN-03 |
| Evidencia con vigencia definida llega a 30 dias de vencer | MOD-019 | MOD-021, MOD-022 | Alerta WARNING; tarea de renovacion | - |
| Se abre procedimiento sancionador o reclamo ante la Direccion de Proteccion de Datos que referencia evidencia | MOD-024, MOD-011 | MOD-019 | Cambio de estado (Evidencia bloqueada, no archivable) | OBL-ARCO-14 |
| Se cierra una auditoria (o no existe ninguna previa, tras el primer diagnostico) | MOD-018, MOD-004 | MOD-021 | Tarea (siguiente ComplianceAudit Planificada) | OBL-AUD-01 |
| Hallazgo de auditoria con severidad Alta o Critica | MOD-018 | MOD-021 | Tarea de plan de accion (15/30 dias habiles sugeridos) | - |
| Se cierra la auditoria | MOD-018 | MOD-019, MOD-002 (notificacion, sin arista estructural) | Evidencia (informe cerrado); aviso de informe nuevo disponible para OBL-DPO-07 | OBL-AUD-01, OBL-DPO-07 |
| Se registra `fecha_notificacion_recibida` de un expediente sancionador | MOD-024 | MOD-023, MOD-021, MOD-022 | Calculo de plazo (5 dias habiles de contestacion); tarea urgente; alerta CRITICAL | OBL-SANC-05, Art. 62 (LPA supletoria) |
| MOD-002 completa "Enviar comunicacion a la ACE", o MOD-010 activa una transferencia | MOD-002, MOD-010 | MOD-024 | Cambio de estado (crea ACEFiling en BORRADOR) | OBL-DPO-03, Art. 45 |
| Expediente sancionador llega a RESUELTO con sancion | MOD-024 | MOD-021, MOD-016 | Calculo de plazo (pago 15 dias habiles, prescripcion 5 anos); tarea por cada medida adicional | OBL-SANC-06, OBL-SANC-07 |
| Bandera `regimen_reforma_659` cambia de ACTUAL a FUTURO | MOD-024 | MOD-002, MOD-007, MOD-008, MOD-011, MOD-015, MOD-017, MOD-021 | Cambio de estado (ver 10.4, diagrama de doble estado); tarea de revision en cada uno | OBL-DPO-01 a 08, OBL-ARCO-01/08/10/11/14, OBL-CONS-03, OBL-CAP-02, OBL-RET-04, OBL-PLAZO-05 |
| Evento de Tarea o Aprobacion (creacion, proxima a vencer, vencida, bloqueada, aprobacion pendiente) | MOD-021 | MOD-022 | Alerta (segun nivel de la tarea) | - |
| Evento de plazo sin tarea previa (por ejemplo revision periodica programada por fecha) | MOD-023 | MOD-022 | Alerta | - |
| Cronometro propio de MOD-011 o MOD-013 (unica excepcion a la regla 4) | MOD-011, MOD-013 | MOD-022 | Alerta CRITICAL con acuse de recibo exigido | Art. 20, Art. 25 |
| Calendario se actualiza (asueto ad hoc) mientras hay calculos abiertos afectados | MOD-023 | modulo de origen del calculo, MOD-022 | Cambio de estado (recalculo, nunca mover el plazo en silencio); alerta | - |
| Consulta de busqueda | Usuario, via MOD-025 | MOD-025 (registro interno) | Evidencia (Search Log, con minimizacion en ambito sensible) | - |
| Articulo del Centro de Ayuda vinculado a un OBL-ID afectado por el cambio de bandera | MOD-024 | MOD-026 | Cambio de estado (articulo MARCADO_PARA_REVISION); tarea interna del equipo del producto | - |

Nota: los eventos de esta tabla no agotan la seccion G de cada ficha (que ademas documenta validaciones puramente internas, sin cruce de modulo); recogen los que cruzan de un modulo a otro y por lo tanto son relevantes para leer la matriz de 10.2 y los diagramas de 10.4.

---

## 10.4 Diagramas ASCII

### 10.4.1 Flujo principal por etapas

Adaptado de `06_mapa_definitivo_de_modulos.md`, seccion 6, con las direcciones confirmadas por la seccion L de cada ficha (10.2).

```
MOD-003 Onboarding
     |
     v
MOD-001 Organizacion  ---->  MOD-002 Delegado / Responsable Interno
     |                            |
     v                            v
MOD-004 Diagnostico de Cumplimiento  <----------------+
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
     |                  +---> MOD-016 Retencion              v
     |                  |                  |             MOD-015 Controles
     |                  v                  v                  |
     +----------->  MOD-010 Transferencias ------------------>+
                         |
                         v
MOD-012 Portal del Titular ----> MOD-011 ARCO-POL
                                       |
                                       +---> MOD-013 Incidentes de Seguridad
                                       |
                                       v
                                  MOD-017 Capacitacion
                                       |
                                       v
MOD-018 Auditoria <----------------> MOD-019 Centro de Evidencias ---> MOD-020 Dashboard y Reportes
   (excepcion reciproca, regla 5)
```

### 10.4.2 Capa transversal

```
           +----------------------------------------------------------+
           |   CAPA TRANSVERSAL (consultada, nunca consulta al reves) |
           |  MOD-021 Tareas | MOD-022 Notif. | MOD-023 Calendario     |
           |  MOD-024 Regulatorio | MOD-025 Busqueda | MOD-026 Ayuda   |
           +----------------------------------------------------------+
                 ^ escriben eventos/tareas/plazos     | consultan/alertan
                 |                                    v
     MOD-001 a MOD-020 (los 20 modulos de las 6 etapas del recorrido)
```

Dentro de la barra: MOD-021 recibe eventos de generacion de tarea de practicamente todo modulo de proceso (10.3) y entrega a MOD-022 y MOD-023; MOD-022 solo reacciona a MOD-021 y MOD-023 (salvo la excepcion puntual de los cronometros propios de MOD-011 y MOD-013); MOD-023 y MOD-024 son fuentes de referencia constante (regla 2) sin depender de ningun otro modulo; MOD-025 y MOD-026 son de solo lectura sobre el resto, sin escribir en ninguno.

### 10.4.3 Cadena critica: ARCO-POL (MOD-011)

```
MOD-023 Calendario -----> [calcula 20+20, 10, 5, 3 dias habiles] -----> MOD-011
MOD-021 Centro de Tareas <---------------------------------------------- MOD-011
MOD-022 Notificaciones   <---------------------------------------------- MOD-011
   (cronometro propio, excepcion a la regla 4)

MOD-008 Documentos  ---(version del Aviso vigente)--->  MOD-011
MOD-006 RAT         ---(tratamiento relacionado, referencia)--->  MOD-011
MOD-009 Proveedores ---(receptores a notificar)--->  MOD-011  ---(rectif./elim. a notificar)--->  MOD-009
MOD-016 Retencion   ---(bloquea cancelacion/olvido si RETENIDO POR OBLIGACION)--->  MOD-011
MOD-019 Centro de Evidencias  <---(expediente completo)---  MOD-011
```

Lectura: MOD-011 es el modulo con mas obligaciones propietarias del mapa (15) y el que mas cadenas cruza en Operar; su ciclo de vida completo (identidad -> tramite -> cierre) no puede completarse sin los cuatro transversales (MOD-021 a MOD-023, mas MOD-024 para la bandera del aprobador por defecto) mas MOD-008, MOD-006, MOD-009 y MOD-016 (esta ultima solo si existe, ver 10.5).

### 10.4.4 Cadena critica: Incidentes de Seguridad (MOD-013)

```
MOD-023 Calendario -----> [calcula el cronometro de 72 horas, paralelo: notificacion / revision] -----> MOD-013
MOD-021 Centro de Tareas <---------------------------------------------------------------------------- MOD-013
MOD-022 Notificaciones   <---------------------------------------------------------------------------- MOD-013
   (cronometro propio, excepcion a la regla 4)

MOD-006 RAT           ---(tratamiento/sistema afectado, dato sensible)--->  MOD-013
MOD-015 Controles     ---(catalogo de controles existentes)--->  MOD-013  ---(medida correctiva nueva)--->  MOD-015
MOD-009 Proveedores   <---(suspension si severidad Alta/Critica)---  MOD-013
MOD-019 Centro de Evidencias  <---(expediente y constancias de envio)---  MOD-013
```

Lectura: MOD-013 comparte con MOD-011 la dependencia de los tres transversales de plazo/tarea/alerta, y ademas cruza con MOD-006, MOD-015, MOD-009 y MOD-019; es el modulo con el plazo mas critico y visible del corpus (72 horas, Art. 25).

### 10.4.5 Doble estado de la reforma 659: propagacion de la bandera

```
                         MOD-024 Centro Regulatorio
                    (bandera regimen_reforma_659: ACTUAL | FUTURO)
                                    |
        cambia solo por confirmacion manual del equipo del producto
                                    |
        +----------+----------+----------+----------+----------+----------+
        v          v          v          v          v          v          v
     MOD-002    MOD-007    MOD-008    MOD-011    MOD-015    MOD-017    MOD-021
   (tipo_rol   (aprobador  (tarea de   (aprobador (item de   (Plan anual (tarea generica
    DELEGADO /  de la      revision de  por        catalogo   pasa a      "Revisar el
    RESPONSABLE revocacion) avisos      defecto     "Delegado  buena       impacto del
    _INTERNO)              publicados) del acto     designado" practica    cambio de
                                        legal)       obligatorio  voluntaria  regimen")
                                                     /opcional)   si aplica)
```

Aclaracion importante sobre esta cadena: `MOD-024_ficha.md` (seccion G, regla 1) declara de forma explicita que el evento de cambio de bandera se emite hacia estos siete modulos (los seis del `alimenta_a` declarado en `mapa_modulos.json` mas MOD-008, ver D3), y que **MOD-016 Retencion y Eliminacion no recibe este evento**, aunque OBL-RET-04 (propiedad de MOD-016) es una de las 17 obligaciones afectadas por la reforma 659. La razon, verificada contra la propia ficha de MOD-016: la relacion de MOD-016 con la bandera es una consulta de referencia bajo demanda (para decidir que texto de ayuda contextual mostrar sobre el aviso conservado), nunca una automatizacion propia disparada por el evento push. Por eso este diagrama no incluye a MOD-016 como receptor del evento, a diferencia de una lectura superficial de la lista de 17 obligaciones afectadas que podria sugerir lo contrario.

Las 17 obligaciones afectadas cambian de estado, nunca de modulo propietario: OBL-DPO-01 a 08 (MOD-002), OBL-ARCO-01/08/10/11/14 (MOD-011), OBL-CAP-02 (MOD-017), OBL-CONS-03 (MOD-007), OBL-RET-04 (MOD-016, por consulta, no por evento) y OBL-PLAZO-05 (MOD-024). Ningun registro se borra: las tareas y expedientes ya cerrados bajo el estado ACTUAL conservan la regla vigente en el momento de su cierre (principio 8 de `06_mapa_definitivo_de_modulos.md`, seccion 2).

---

## 10.5 Orden funcional de construccion

Basado en las secciones L y Q de cada ficha y en el test de tres condiciones de `06_mapa_definitivo_de_modulos.md` (seccion 2, principio 7): un modulo entra al MVP si (a) cubre una obligacion OBLIGATORIO con plazo transitorio ya vencido, (b) es dependencia estructural de otro MUST HAVE, o (c) es la unica forma de que el producto sea probatorio desde el primer dia.

### 10.5.1 Orden de los MUST HAVE (20 modulos, disponibles desde el primer lanzamiento)

```
Nivel 0 (sin dependencia de otro modulo de proceso, disponibles desde el arranque):
   MOD-003 Onboarding | MOD-023 Calendario y Motor de Plazos | MOD-024 Centro Regulatorio

Nivel 1 (dependen solo de Nivel 0):
   MOD-001 Organizacion y Personas (de MOD-003)

Nivel 2:
   MOD-002 Delegado / Responsable Interno (de MOD-001, MOD-024; consulta MOD-023)
   MOD-021 Centro de Tareas (recibe de casi todos; consulta MOD-023, MOD-001)
   MOD-022 Notificaciones (de MOD-021, MOD-023)

Nivel 3:
   MOD-004 Diagnostico de Cumplimiento (de MOD-003; precarga de MOD-001)

Nivel 4:
   MOD-005 Plan de Cumplimiento (de MOD-004, MOD-001)
   MOD-006 RAT y Mapa de Datos (de MOD-004)

Nivel 5 (todos dependen de MOD-006, algunos entre si):
   MOD-008 Documentos y Politicas (de MOD-004, MOD-006)
   MOD-009 Proveedores y Encargados (de MOD-006)

Nivel 6:
   MOD-007 Consentimiento (de MOD-006, MOD-008)
   MOD-015 Controles de Seguridad (de MOD-006; de MOD-010 si existe, SHOULD HAVE)

Nivel 7:
   MOD-011 ARCO-POL (de MOD-007, MOD-002; de MOD-012 si existe, SHOULD HAVE)
   MOD-013 Incidentes de Seguridad (de MOD-006, MOD-015)

Nivel 8:
   MOD-016 Retencion y Eliminacion (de MOD-006, MOD-008; SHOULD HAVE, ver 10.5.2)
   MOD-017 Capacitacion (de MOD-001, MOD-002)

Nivel 9:
   MOD-019 Centro de Evidencias (de MOD-007 a MOD-018, los 12 modulos operativos)

Nivel 10:
   MOD-018 Auditoria de Cumplimiento (de MOD-006, MOD-015, MOD-019; relacion reciproca con MOD-019, regla 5)
   MOD-020 Dashboard y Reportes (de MOD-005, MOD-019, MOD-021)
```

MOD-025 (Busqueda Global, COULD HAVE) y MOD-026 (Centro de Ayuda, MUST HAVE) no tienen dependencia estructural de construccion (`depende_de: []`), pero MOD-026 debe tener contenido redactado antes de que cada pantalla lo consuma (regla operativa, no de datos: la ayuda contextual es "complemento obligatorio" de cada ficha, seccion R de la plantilla), y MOD-025 solo aporta valor una vez que existe contenido indexable en los demas modulos.

### 10.5.2 Que pasa si un modulo del que se depende no entra en el MVP (SHOULD HAVE / COULD HAVE)

Cobertura parcial documentada en la seccion L y Q de cada ficha (ninguna es una invencion de esta seccion):

| Modulo ausente (clasificacion) | Quien depende de el | Cobertura parcial mientras no existe |
|---|---|---|
| MOD-010 Transferencias Internacionales (SHOULD HAVE) | MOD-006, MOD-009, MOD-007, MOD-015, MOD-011 (lectura), MOD-024 | El Diagnostico (MOD-004) y el RAT (MOD-006) detectan la senal "datos fuera de El Salvador: si" y crean una tarea manual en MOD-021 para documentar la transferencia como evidencia suelta en MOD-019, sin motor de deteccion automatica de proveedores extranjeros ni estados de workflow propios |
| MOD-012 Portal del Titular (SHOULD HAVE) | MOD-011, MOD-008 | El MVP de ARCO-POL usa el formulario interno seguro de MOD-011 (decision 2.7.30); el Aviso de Privacidad se publica por otro medio (sitio web, lugar visible); no hay vacio legal, OBL-DOC-04 y OBL-PLAZO-04 ya estan cubiertas |
| MOD-014 Riesgos y EIPD (SHOULD HAVE) | MOD-006, MOD-015, MOD-021 | El Diagnostico detecta biometria, salud, menores o camaras y crea la tarea generica "elaborar EIPD" en MOD-021 con una plantilla generica de documento en MOD-008, llenada manualmente, sin motor de scoring |
| MOD-016 Retencion y Eliminacion (SHOULD HAVE) | MOD-006, MOD-008, MOD-011 (bloqueo de cancelacion/olvido) | MOD-008, MOD-011 y MOD-013 no permiten borrar sus propios registros de cumplimiento antes de 10/5 anos (regla de no-borrado nativa); el motor de retencion de datos del titular con calculo del maximo entre bases no existe, la resolucion de conflictos queda como nota manual en el campo "plazo de conservacion" del RAT |
| MOD-018 Auditoria de Cumplimiento (SHOULD HAVE) | MOD-019 (relacion reciproca), MOD-021, MOD-020 | Los informes periodicos del Delegado (MOD-002) se generan y archivan igual de forma autonoma como evidencia, disponibles para cuando MOD-018 se active, sin perdida de historial |
| MOD-025 Busqueda Global (COULD HAVE) | Ningun modulo declara una dependencia estructural hacia el | Ninguna: su ausencia no bloquea ninguna obligacion legal; el usuario navega por los menus de cada modulo en vez de buscar de forma centralizada |

Ningun modulo MUST HAVE queda sin sus dependencias estructurales en el MVP: los 20 modulos de nivel 0 a 10 de 10.5.1 son todos MUST HAVE o forman parte del nucleo transversal MUST HAVE (MOD-021 a MOD-024, MOD-026), de modo que el riesgo real de "modulo ausente" solo aplica a los 5 SHOULD HAVE y a MOD-010, MOD-012, MOD-014, MOD-016, MOD-018 y MOD-025 listados arriba.

---

## 10.6 Riesgos de acoplamiento y mitigacion

Los cuatro modulos de los que dependen mas modulos (directa o indirectamente, segun la matriz de 10.2 y la regla 2 de asimetria de fuentes constantes) son MOD-001, MOD-021, MOD-023 y MOD-024. Una falla funcional o un retraso en cualquiera de los cuatro se propaga a la mayoria del sistema.

| Modulo | Por que concentra riesgo | Mitigacion funcional |
|---|---|---|
| MOD-001 Organizacion y Personas | Fuente unica de identidad de organizacion, usuarios y roles; sin el, ningun otro modulo MUST HAVE puede operar (regla del mapa definitivo: "ningun modulo de proceso escribe su propia copia de la identidad de organizacion") | Validacion de integridad minima (G, regla 5): bloquear la baja de un usuario unico titular de un rol critico sin reemplazo; catalogo de roles versionado y no editable a mitad de un flujo en curso; la separacion de funciones (5.4) evita que un solo usuario concentre Aprobador y Auditor sin advertencia visible |
| MOD-021 Centro de Tareas | Todo modulo de proceso que genera trabajo crea tareas alli (regla 1 de conexion, seccion 4 del mapa); es el receptor de facto mas amplio del sistema, de forma simetrica a como MOD-001, MOD-023 y MOD-024 son las fuentes mas amplias (ver D6, no declarado explicitamente como excepcion en el mapa) | Preservacion de historial en vez de borrado cuando cambia el regimen normativo (nunca se pierde una tarea, solo se marca "no aplica, ver historial"); el catalogo de tipos de tarea es abierto y extensible sin tocar otros modulos; cada tarea conserva su "modulo de origen" para trazabilidad si MOD-021 debe reconstruirse |
| MOD-023 Calendario y Motor de Plazos | Unico servicio de calculo de dias/horas habiles; ARCO-POL, Incidentes, Delegado y Procedimiento sancionador dependen de el para no calcular plazos por su cuenta con riesgo de resultados distintos para el mismo caso | Recalculo automatico y trazado cuando cambia el calendario (nunca mueve un plazo en silencio, regla 4 de su propia ficha); capas de calendario independientes (nacional, autoridad, sucursal) que se pueden corregir sin afectar calculos ya cerrados; alerta explicita si falta el calendario del ano siguiente (1 de noviembre) |
| MOD-024 Centro Regulatorio | Unico modulo que decide que version de una regla o que estado del regimen de la reforma 659 esta activo; siete modulos MUST HAVE reciben directamente su evento de cambio de bandera (10.4.5) | La bandera nunca cambia de forma automatica por la sola aprobacion legislativa, solo por confirmacion manual del equipo del producto (mitiga el riesgo de un cambio de estado prematuro o de una fuente secundaria equivocada); cada modulo receptor consulta por referencia, nunca copia el estado (regla 9 de la seccion G de MOD-024), de modo que una correccion posterior de la bandera se refleja de inmediato sin tener que sincronizar copias distribuidas |

Riesgo adicional no ligado a un modulo individual sino al patron de acoplamiento en si: la mayoria de estas dependencias amplias (MOD-001, MOD-023, MOD-024 como fuentes; MOD-021 como receptor) no estan declaradas como aristas `depende_de`/`alimenta_a` explicitas modulo por modulo en `mapa_modulos.json`, sino que se documentan como excepcion narrativa en la seccion 6.1 del mapa definitivo (para las tres fuentes) o quedan sin declarar como tal (para MOD-021, ver "Contradicciones y huecos detectados", D6). Esto es funcionalmente correcto (evita una matriz saturada de aristas triviales) pero implica que cualquier cambio futuro en el comportamiento de estos cuatro modulos exige revisar el texto de cada ficha, no solo el JSON, porque el JSON por si solo subestima cuantos modulos realmente dependen de ellos.

---

## Propuestas de esta seccion, no presentes en las fichas

Las dos piezas siguientes responden a exigencias explicitas del prompt del cliente (`00_prompt_analisis_funcional.md`, seccion 10 de la estructura final) que ninguna ficha individual consolida por si sola, porque cada ficha describe su propio modulo, no el conjunto. Se marcan como propuesta de esta seccion porque no hay una tabla o diagrama equivalente ya redactado en `03_modulos/` ni en `06_mapa_definitivo_de_modulos.md`.

1. **La tabla de orden de construccion de 10.5.1 y la tabla de cobertura parcial de 10.5.2** son una consolidacion nueva: cada ficha individual dice de que depende y que ocurre si su propia dependencia falta, pero ninguna arma la secuencia completa de los 20 MUST HAVE en niveles. Se construyo exclusivamente a partir de los `depende_de` ya declarados (mas las correcciones D1 a D7 de abajo), sin agregar ninguna dependencia nueva no sustentada en una ficha o en el JSON.
2. **Un runbook funcional consolidado para la secuencia de revision cuando cambia la bandera de la reforma 659** (mas alla del diagrama de propagacion de 10.4.5). Cada una de las siete fichas receptoras (MOD-002, MOD-007, MOD-008, MOD-011, MOD-015, MOD-017, MOD-021) describe su propia reaccion al evento, pero ninguna fija un orden recomendado entre ellas para la revision humana posterior (por ejemplo, revisar primero MOD-002 para confirmar quien queda como responsable del tramite, antes de revisar MOD-011 y MOD-007, que dependen de esa misma persona como aprobador por defecto). Se propone el orden: (1) MOD-002, porque define quien es hoy el aprobador de todo acto atribuido "al Delegado"; (2) MOD-011 y MOD-007, que usan ese aprobador; (3) MOD-008, que revisa avisos publicados; (4) MOD-015 y MOD-017, que actualizan catalogo y plan de capacitacion; (5) MOD-021, que archiva las tareas exclusivas del regimen anterior una vez resueltos los pasos 1 a 4. Esta secuencia es una recomendacion operativa de esta seccion, no una regla que ninguna ficha imponga; el sistema no la fuerza, solo la sugiere como guia de uso.

---

## Contradicciones y huecos detectados

### Contradicciones (diferencias entre `mapa_modulos.json` y las fichas, o entre fichas)

Para cada una: que dice cada fuente, cual version adopta este documento, y por que. En todos los casos la version adoptada es la que declaran, de forma coincidente, la ficha propietaria del modulo receptor y (cuando existe) la ficha del modulo emisor; ninguna de estas correcciones contradice `matriz_obligaciones.json` ni el texto legal, solo el registro de aristas de `mapa_modulos.json`.

- **D1 (MOD-002 / MOD-023).** `mapa_modulos.json` declara `depende_de` de MOD-002 = [MOD-001, MOD-024], sin MOD-023. `MOD-002_ficha.md` (seccion L) declara explicitamente que consulta a MOD-023 para todos sus contadores de plazo (3, 10, 15 dias habiles; 1, 3, 5 anos), y `06_mapa_definitivo_de_modulos.md` (decision 2.7.15) nombra a "Delegado" como uno de los cuatro consumidores del motor de plazos unico; el `alimenta_a` de MOD-023 ya incluye a MOD-002. Se adopta la version de la ficha: MOD-002 si depende de MOD-023. Correccion propuesta: agregar "MOD-023" al `depende_de` de MOD-002 en `mapa_modulos.json`.
- **D2 (MOD-005 / MOD-024, recalculo por cambio normativo).** El prompt de analisis exige documentar como se recalcula un plan cuando cambia la normativa; `mapa_modulos.json` no declara una arista directa MOD-024 -> MOD-005, y el `alimenta_a` de MOD-024 tampoco incluye a MOD-005. `MOD-005_ficha.md` y `MOD-024_ficha.md` (notas finales) coinciden en modelar el recalculo como una cadena indirecta MOD-024 -> MOD-004 -> MOD-005 (MOD-004 si es una entrada declarada de MOD-005) en vez de crear una arista nueva no sustentada. Se adopta esa cadena indirecta como la version correcta de este documento (10.3.1, fila "Cambio en el conjunto de obligaciones aplicables"); no se propone agregar una arista directa MOD-024 -> MOD-005 al mapa, siguiendo la misma decision que ya tomaron ambas fichas para no introducir una discrepancia adicional no solicitada.
- **D3 (MOD-024 -> MOD-008).** `mapa_modulos.json` declara `alimenta_a` de MOD-024 = [MOD-002, MOD-007, MOD-011, MOD-015, MOD-017, MOD-021], sin MOD-008. `MOD-008_ficha.md` (seccion G, regla 3) declara una automatizacion propia disparada exactamente por "MOD-024 cambia la bandera regimen_reforma_659 de ACTUAL a FUTURO"; `MOD-024_ficha.md` (seccion G, regla 1) confirma la misma relacion y senala la misma discrepancia de forma independiente. Se adopta la version coincidente de ambas fichas: MOD-024 si alimenta a MOD-008. Correccion propuesta: agregar "MOD-008" al `alimenta_a` de MOD-024 y "MOD-024" al `depende_de` de MOD-008 en `mapa_modulos.json`. Precision relacionada, sin corregir: `mapa_modulos.json` no incluye a MOD-016 en esta lista pese a que OBL-RET-04 (propiedad de MOD-016) es una de las 17 obligaciones afectadas; `MOD-016_ficha.md` confirma que su relacion con la bandera es una consulta bajo demanda, no un evento push, por lo que aqui no hay discrepancia que corregir (ver tambien la aclaracion de 10.4.5).
- **D4 (MOD-016 / MOD-011 y MOD-013).** `mapa_modulos.json` declara `depende_de` de MOD-016 = [MOD-006, MOD-008], y el `alimenta_a` de MOD-011 y de MOD-013 no incluye a MOD-016. `MOD-016_ficha.md` (seccion G, regla 3, y nota de coherencia al final de la seccion L) declara que su automatizacion de OBL-RET-05 necesita leer la fecha de cierre de un expediente de MOD-011 o de MOD-013. Se adopta la version de la ficha: MOD-016 si depende de MOD-011 y de MOD-013 para esa automatizacion especifica. Correccion propuesta: agregar "MOD-011" y "MOD-013" al `depende_de` de MOD-016, y "MOD-016" al `alimenta_a` de ambos, en `mapa_modulos.json`.
- **D5 (MOD-020, MOD-025 y MOD-026: consumo real mas amplio que `depende_de`/`alimenta_a`).** `mapa_modulos.json` declara `depende_de` de MOD-020 = [MOD-005, MOD-019, MOD-021] (dependencia estructural minima correcta para el "dashboard basico") y `alimenta_a`/`depende_de` vacios para MOD-025 y MOD-026 (correcto para su clasificacion COULD HAVE / sin dependencia de construccion). Las propias fichas de MOD-020, MOD-025 y MOD-026 (notas finales) verifican por `grep` que consumen datos de 24, de "MOD-002 y MOD-004 a MOD-020 mas MOD-024/MOD-026" y de "practicamente todos los modulos operativos" respectivamente, sin que eso sea una dependencia estructural de construccion. Se adopta la distincion que las tres fichas proponen (la misma que la seccion 6.1 del mapa definitivo ya aplica a MOD-001, MOD-023 y MOD-024 como fuentes amplias): no se cambia el `depende_de`/`alimenta_a` de estos tres modulos en `mapa_modulos.json` (seria incorrecto declarar alli una dependencia estructural que no tienen para funcionar en su version minima), pero se recomienda documentar esta misma distincion tambien para ellos en una proxima revision de la seccion 6.1.
- **D6 (MOD-021 como receptor amplio: MOD-014, MOD-018, MOD-008, MOD-009).** `mapa_modulos.json` declara `depende_de` de MOD-021 = [MOD-004, MOD-005, MOD-011, MOD-013, MOD-002]. `MOD-014_ficha.md` y `MOD-018_ficha.md` declaran "Sale hacia MOD-021" en su propia seccion L, y sus respectivos `alimenta_a` en el JSON ya incluyen a MOD-021; `MOD-021_ficha.md` (nota final, punto 1) senala esta asimetria de forma explicita y recomienda corregirla o declararla como excepcion. Ademas, `MOD-008_ficha.md` y `MOD-009_ficha.md` (seccion G) muestran varias reglas que crean tareas en MOD-021 (por ejemplo, revision de aviso, vencimiento de contrato, verificacion de devolucion/eliminacion), sin que sus propios `alimenta_a` en el JSON incluyan a MOD-021 (`MOD-021_ficha.md`, nota final, punto 2, deja constancia de esta segunda asimetria). Se adopta la version de las cuatro fichas de origen: los cuatro si alimentan a MOD-021. Correccion propuesta: agregar "MOD-014" y "MOD-018" al `depende_de` de MOD-021 (sus `alimenta_a` ya son correctos); y agregar "MOD-021" al `alimenta_a` de MOD-008 y de MOD-009, mas "MOD-008" y "MOD-009" al `depende_de` de MOD-021, en `mapa_modulos.json`. Se recomienda ademas que una proxima revision de la seccion 6.1 del mapa definitivo declare a MOD-021 como el equivalente receptor de la excepcion de asimetria que hoy solo se documenta para MOD-001, MOD-023 y MOD-024 como fuentes (ver 10.6).
- **D7 (MOD-024 / MOD-002 y MOD-010).** `mapa_modulos.json` declara `depende_de` de MOD-024 = [] (vacio), mientras que su propio `alimenta_a` y el de MOD-002 y de MOD-010 ya reflejan correctamente que ambos alimentan a MOD-024. `MOD-002_ficha.md` y `MOD-010_ficha.md` (seccion L) declaran de forma coincidente que envian, respectivamente, el evento "tramite de nombramiento" y el borrador de "puesta en conocimiento a la ACE" (ACEFiling) hacia MOD-024; `MOD-024_ficha.md` (seccion L y nota final) confirma la misma relacion desde el lado receptor y senala la misma discrepancia. Se adopta la version coincidente de las tres fichas. Correccion propuesta: agregar "MOD-002" y "MOD-010" al `depende_de` de MOD-024 en `mapa_modulos.json` (el `alimenta_a` de ambos ya es correcto, no requiere cambio).

### Huecos (pasos o piezas que ninguna ficha define)

- **H1. Continuidad operativa si un modulo transversal MUST HAVE falla por un incidente propio (no por ausencia en el MVP).** Las fichas y el mapa definitivo documentan que pasa si un modulo SHOULD HAVE/COULD HAVE aun no existe (10.5.2), pero ninguna ficha de MOD-021, MOD-022, MOD-023 o MOD-024 describe un comportamiento funcional degradado si el propio servicio transversal deja de estar disponible operativamente (por ejemplo, que hace MOD-011 si el servicio de calculo de plazos de MOD-023 no responde durante el computo de las 20 dias habiles). Requiere validacion de producto: no es una decision juridica, pero ninguna ficha la resuelve hoy.
- **H2. Orden de revision humana tras el cambio de bandera de la reforma 659 entre los siete modulos receptores.** Cada ficha describe su propia reaccion al evento (10.4.5), pero ninguna fija una secuencia recomendada de revision entre MOD-002, MOD-007, MOD-008, MOD-011, MOD-015, MOD-017 y MOD-021. Se cubre como propuesta de esta seccion (ver arriba), no como hallazgo en una ficha existente.
- **H3. Que ocurre con una tarea de MOD-021 cuyo modulo de origen (por ejemplo MOD-014 o MOD-018) todavia no esta en el MVP, mas alla de "crear una tarea generica".** Las fichas de MOD-014 y MOD-018 (con cobertura parcial, 10.5.2) describen que la tarea se crea en MOD-021 con una plantilla generica, pero ninguna ficha de MOD-021 describe si esa tarea "generica" queda marcada de forma distinta en el listado (por ejemplo, con una etiqueta "cobertura parcial, modulo completo no disponible") para que el responsable sepa que no esta usando el flujo completo. Requiere una decision de producto que ninguna ficha toma hoy.
- **H4. Verificacion tecnica de la excepcion de asimetria de MOD-021 como receptor amplio (D6) contra el resto de fichas no citadas aqui.** Esta seccion verifico la relacion de MOD-021 con MOD-014, MOD-018, MOD-008 y MOD-009 porque son las que sus propias fichas ya declaran de forma expresa; no se verifico exhaustivamente si otras fichas (por ejemplo MOD-010, MOD-012, MOD-016) tienen la misma asimetria no declarada, porque hacerlo requeriria releer la seccion G completa de las 26 fichas linea por linea, mas alla del alcance de esta seccion. Queda como verificacion pendiente para quien mantenga `mapa_modulos.json`.
