# MODULO: Centro de Evidencias

Codigo corto del modulo: MOD-019
Clasificacion global del modulo: MUST HAVE
Obligaciones que cubre: OBL-PRIN-03 (propietaria); OBL-CONS-05 (colaboradora, propietaria MOD-007 Consentimiento), OBL-INC-04 (colaboradora, propietaria MOD-013 Incidentes de Seguridad), OBL-RET-05 (colaboradora, propietaria MOD-016 Retencion y Eliminacion), OBL-SANC-07 (colaboradora, propietaria MOD-024 Centro Regulatorio), OBL-TRANSF-06 (colaboradora, propietaria MOD-010 Transferencias Internacionales)

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (sin codigo, sin SQL, sin APIs, sin stack, sin infraestructura).

Fuentes usadas para esta ficha: `00_contexto_para_agentes.md`; `00_prompt_analisis_funcional.md`; `00_plantilla_ficha_modulo.md`; `02_validacion/mapa_modulos.json` (entrada MOD-019); `02_validacion/06_mapa_definitivo_de_modulos.md` (secciones 0, 2, 3 ficha de MOD-019, 4, 5, 6, 6.1, 7, 8, 9); `01_legal/matriz_obligaciones.json` (OBL-PRIN-03, OBL-CONS-05, OBL-INC-04, OBL-RET-05, OBL-SANC-07, OBL-TRANSF-06); `01_legal/fuentes/ace_decreto_144.txt` (Art. 5 lit. i, Art. 54); `01_legal/fuentes/normativa_sancionadora_OCR.txt` (Art. 47); `01_legal/03_hallazgos_regulatorios.md`; `02_validacion/02_validacion_de_la_idea.md` (decisiones 2.7.4, 2.7.13, 2.7.24, 2.7.26; inconsistencias 4, 11 y 26; faltante 19); `02_validacion/04_objetivo_exacto_del_producto.md` (secciones 1.2 y 1.3); `02_validacion/05_tipos_de_usuario.md` (secciones 5.3 y 5.4); `02_validacion/22_anti_features.md` (items 1, 5, 8, 9, 13, 19, 25); `02_validacion/lente_faltantes.md` y `02_validacion/lente_inconsistencias.md`; `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` (secciones 29 y 30, hipotesis de producto); secciones J (Evidencia) y O (Historial) de `03_modulos/MOD-001_ficha.md` a `03_modulos/MOD-018_ficha.md` y `03_modulos/MOD-021_ficha.md`; `03_modulos/MOD-018_ficha.md` y `03_modulos/MOD-008_ficha.md` completas, como modelo de estilo y profundidad.

---

## A. Proposito

- **Por que existe.** El principio de responsabilidad demostrada (Art. 5 lit. i LPDP, OBL-PRIN-03) exige que la empresa pueda demostrar, en cualquier momento y ante cualquier requerimiento, que cumple sus obligaciones, no solo que las cumple. Ningun otro modulo tiene como funcion propia responder la pregunta que hace cualquier revision seria del programa: "que evidencia tenemos de esta obligacion". MOD-019 existe exclusivamente para eso: recibe de forma continua la evidencia que generan MOD-007 a MOD-018, la organiza por obligacion (usando el campo `evidencia_esperada` de cada una de las 105 obligaciones de `matriz_obligaciones.json`), muestra los huecos donde falta, y arma paquetes exportables con verificacion de integridad cuando alguien (la propia empresa, un auditor, la ACE) necesita verla junta.
- **Distincion clave (decision de alcance 2.7.4, inconsistencias 4 y 11 de `02_validacion_de_la_idea.md`).** MOD-019 modela tres entidades separadas que nunca se mezclan:
  - **Documento**: contenido versionado (avisos, politicas, contratos, informes). Propiedad de MOD-008 Documentos y Politicas; MOD-019 lo referencia, nunca lo copia.
  - **Evidencia (Evidence)**: propiedad de este modulo. Un artefacto (archivo con hash) o una referencia vinculada a un registro especifico de otro modulo (una aprobacion, un cambio de estado, un envio), que demuestra que algo ocurrio.
  - **AuditLog**: registro tecnico e inmutable de acciones del sistema (quien hizo que, cuando), embebido en todos los modulos desde el primer dia de uso. No tiene modulo propietario unico (cada modulo escribe sus propios eventos); MOD-019 lo consulta como fuente de contexto tecnico, nunca lo administra.
  - **EvidencePackage**: no es una cuarta base de datos. Es una vista de exportacion sobre las tres entidades anteriores, sin almacenamiento propio, con un manifiesto y verificacion de integridad (huella o firma) por archivo y sobre el conjunto (anti-feature 25 de `22_anti_features.md`, decision 2.7.24).
- **Que problema resuelve para la empresa.** Sin este modulo, la evidencia de cumplimiento queda dispersa en 12 modulos distintos (MOD-007 a MOD-018), cada uno con su propio criterio de que guardar y como. Cuando llega una auditoria anual (MOD-018), un requerimiento de la ACE, una diligencia preliminar o un cliente que pide due diligence antes de firmar un contrato, alguien tendria que entrar modulo por modulo a buscar manualmente. MOD-019 responde, para cualquiera de las 105 obligaciones de la matriz, si hay evidencia registrada, si esta vigente, si esta vencida y necesita renovarse, o si simplemente no existe.
- **Que obligacion(es) cubre (IDs y articulos).**
  - **OBL-PRIN-03** (propietaria), Art. 5 lit. i) LPDP: principio de responsabilidad demostrada (accountability). Es la obligacion mas transversal de toda la matriz: cualquier evidencia que otro modulo produzca para probar su propia obligacion especifica es, al mismo tiempo, evidencia parcial de OBL-PRIN-03. MOD-019 es el unico modulo cuya funcion completa es esa obligacion.
  - **Colabora con OBL-CONS-05** (Art. 54 LPDP, carga de la prueba del consentimiento y del aviso de privacidad, propietaria MOD-007 Consentimiento): MOD-019 conserva el conjunto que MOD-007 genera (snapshot del texto, version del aviso, medio, fecha, archivo de firma) accesible por obligacion y exportable con verificacion de integridad, para el momento en que la empresa deba probar ante la ACE o ante un tercero que obtuvo el consentimiento y comunico el aviso.
  - **Colabora con OBL-INC-04** (Art. 25 inc. final LPDP, documentacion obligatoria de toda vulneracion con riesgo, propietaria MOD-013 Incidentes de Seguridad): MOD-019 conserva el expediente completo del incidente (fecha, motivo, hechos, efectos, medidas correctivas) como evidencia consultable por obligacion, y aplica a los archivos adjuntos del incidente el mismo mecanismo de cadena de custodia que describe la seccion siguiente, para que un expediente de incidente no pierda valor probatorio si mas adelante se usa en un procedimiento sancionador.
  - **Colabora con OBL-RET-05** (Art. 47 Normativa PAS por analogia, criterio de retencion del expediente ARCO-POL e incidentes como prueba de descargo, propietaria MOD-016 Retencion y Eliminacion): MOD-019 es quien conserva efectivamente la evidencia sujeta a ese plazo (minimo 5 anos desde el cierre) y quien bloquea su eliminacion o modificacion mientras un procedimiento o un reclamo relacionado siga abierto (ver seccion F). Nota de clasificacion: `matriz_obligaciones.json` clasifica OBL-RET-05 como RECOMENDADO, con la condicion expresa "criterio de diseno recomendado ante ausencia de norma expresa; requiere validacion de abogado" (no existe hoy una norma que fije de forma expresa el plazo de conservacion de este expediente). El plazo de 5 anos y el bloqueo que se describen aqui y en la seccion J son, por tanto, el criterio de diseno por defecto del sistema mientras no exista validacion de asesoria juridica que lo confirme o lo ajuste, no una regla legal cerrada.
  - **Colabora con OBL-SANC-07** (Art. 29 D.L. 143 por remision del Art. 53 LPDP, Art. 47 Normativa PAS, prescripcion de infracciones y sanciones a 5 anos, propietaria MOD-024 Centro Regulatorio): MOD-019 usa ese mismo plazo de 5 anos como horizonte minimo de conservacion para toda la evidencia de cumplimiento que administra, no solo para el expediente ARCO-POL/incidentes (ver seccion J).
  - **Colabora con OBL-TRANSF-06** (Art. 54 inc. 2 LPDP, carga de la prueba en transferencias internacionales, propietaria MOD-010 Transferencias Internacionales): MOD-019 conserva el expediente completo de cada transferencia (tratamiento, receptor, pais, base, contrato, puesta en conocimiento de la ACE) exportable como paquete especifico cuando la empresa deba demostrar que una transferencia concreta se realizo conforme a la ley.
- **Que valor aporta.**
  - Operativo: convierte 12 fuentes de evidencia dispersas en un unico punto de consulta por obligacion, sin que ningun modulo deje de ser dueno de su propio dato.
  - Probatorio: es, junto con MOD-018, la pieza mas fuerte del principio de responsabilidad demostrada, porque muestra no solo evidencia puntual sino el estado completo (que esta, que falta, que vencio) frente a las 105 obligaciones de la matriz.
  - De reduccion de riesgo: detecta huecos de evidencia (una obligacion OBLIGATORIO sin ningun registro) antes de que los detecte la ACE en una diligencia preliminar o un tercero en una due diligence.
- **Que NO hace este modulo (limites explicitos).**
  - No declara "porcentaje de cumplimiento legal" en ningun indicador ni reporte; usa siempre estado de la evidencia (disponible, faltante, vencida, en revision, rechazada) y estado del programa (anti-feature 5 de `22_anti_features.md`).
  - No decide si la evidencia disponible es "suficiente" para una obligacion concreta; esa es una decision humana, de la organizacion o de asesoria juridica (ver seccion H).
  - No copia ni centraliza la base de datos de clientes, empleados o titulares de la empresa; solo conserva metadatos, referencias y, cuando es estrictamente necesario, un adjunto puntual (anti-features 1 y 8 de `22_anti_features.md`).
  - No es el modulo propietario del contenido de los Documentos (eso es MOD-008) ni del AuditLog tecnico (transversal, embebido); consulta ambos, no los sustituye ni los administra.
  - No realiza por si mismo la auditoria sustantiva anual (eso es MOD-018): MOD-019 provee la evidencia que esa auditoria usa, y recibe de vuelta el informe y los hallazgos cerrados como nueva evidencia (relacion reciproca, ver seccion L).
  - No presenta tramites ante la ACE en nombre de la empresa (anti-feature 13); prepara el paquete de evidencia, la empresa decide cuando y como enviarlo.

### Nota sobre el doble estado de la reforma 659 en este modulo

Segun el mapa definitivo, la nota de reforma 659 de MOD-019 es "No aplica directamente; conserva evidencia de ambos regimenes sin alterar retroactivamente expedientes cerrados", y esta ficha la desarrolla asi: ninguna de las 17 obligaciones afectadas por la reforma es propiedad ni colaboradora de este modulo. Lo que si hace MOD-019, de forma consistente con el principio de preservacion de historial de la seccion 5 del mapa definitivo, es conservar cada pieza de evidencia con el regimen (`ACTUAL` o `FUTURO`) vigente en el momento en que se genero, sin reinterpretarla despues. Por ejemplo, un acta de nombramiento del Delegado capturada bajo el regimen `ACTUAL` sigue siendo evidencia valida de OBL-DPO-01 aunque la bandera de MOD-024 cambie mas adelante a `FUTURO`; el paquete de evidencia que incluya ese documento muestra siempre el regimen bajo el que se genero, nunca lo actualiza de forma retroactiva.

---

## B. Usuarios

| Rol estandar | Para que usa este modulo |
|---|---|
| Administrador de la organizacion | Configura el catalogo de tipos de evidencia y los umbrales de doble control para exportaciones externas; consulta el estado general de huecos de evidencia; puede generar paquetes en pyme, con advertencia de autorrevision si tambien es quien aprueba |
| Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | Usuario principal: revisa por obligacion que evidencia existe y cual falta, aprueba evidencia cargada, genera y aprueba paquetes de evidencia (incluido el segundo control en envios externos), da seguimiento a evidencia vencida o por renovar |
| Responsable ARCO-POL / Responsable del tramite | Consulta la evidencia de sus propios expedientes (MOD-011) dentro del Centro de Evidencias, sin poder editarla desde aqui (la edicion ocurre en el modulo de origen); solicita un paquete de evidencia para un reclamo especifico ante la ACE |
| Responsable Legal / Compliance | Revisa huecos de evidencia sobre obligaciones OBLIGATORIO, valida si una evidencia rechazada requiere criterio juridico antes de subsanarse, aprueba paquetes destinados a la ACE o a un procedimiento sancionador (MOD-024) |
| Responsable de Seguridad / IT | Carga y renueva evidencia tecnica con vigencia (por ejemplo, el informe de un pentest anual), recibe las alertas de vencimiento de esa evidencia especifica |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Consulta si la evidencia de un tratamiento de su area esta completa; carga evidencia suelta cuando el modulo estructurado que deberia generarla automaticamente aun no existe en el MVP (por ejemplo, evidencia de una transferencia mientras MOD-010 no esta activo) |
| Aprobador | Aprueba evidencia cargada manualmente antes de que pase a estado Disponible; aprueba, como segundo control, todo paquete de evidencia con destino externo a la organizacion |
| Auditor (interno) | Solo lectura: consulta la evidencia por obligacion y el historial de paquetes generados, como verificacion independiente; nunca carga ni aprueba evidencia desde este modulo |
| Auditor externo (invitado) | Acceso temporal de solo lectura al paquete de evidencia especifico para el que fue invitado, sin ver evidencia de otras obligaciones o periodos fuera del alcance acordado |
| Usuario de consulta / Colaborador | Carga el archivo de evidencia puntual que se le pidio como parte de una tarea (MOD-021), sin ver el resto del catalogo de evidencia de la organizacion |
| Titular (formulario externo) | No aplica: este modulo es informacion organizativa interna sobre el programa de cumplimiento, el titular nunca accede a el |
| Asesor externo invitado | Acceso puntual y acotado a la evidencia de un caso especifico en el que fue invitado a opinar (por ejemplo, si la evidencia disponible sustenta una base juridica en disputa) |

---

## C. Permisos

| Accion | Administrador | Delegado / Resp. interno | Resp. ARCO-POL | Resp. Legal/Compliance | Resp. Seguridad/IT | Resp. de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver evidencia por obligacion, modulo o periodo | Si | Si | Solo la de sus expedientes | Si | Solo la tecnica de sus controles | Solo la de su area | Si | Si (lectura) | Solo el paquete invitado | No | Solo el caso asignado |
| Ver huecos de evidencia (obligaciones sin registro) | Si | Si | No | Si | No | No | Si | Si (lectura) | No | No | No |
| Cargar evidencia suelta (modulo de origen sin cobertura en el MVP) | Si | Si | Si (sus expedientes) | Si | Si (sus controles) | Si (su area) | No | No | No | Si (su tarea) | No |
| Aprobar evidencia cargada manualmente | No (salvo pyme, con advertencia) | Si | No | Si | No | No | Si | No | No | No | No |
| Rechazar evidencia (con motivo) | No (salvo pyme, con advertencia) | Si | No | Si | No | No | Si | No | No | No | No |
| Marcar evidencia como vigente/renovada | No | Si | No | No | Si (la propia) | No | No | No | No | No | No |
| Generar EvidencePackage (borrador) | Si | Si | Si (su expediente) | Si | Si (sus controles) | No | No | No | No | No | No |
| Aprobar exportacion de EvidencePackage con destino interno | Si | Si | No | Si | No | No | Si | No | No | No | No |
| Aprobar exportacion de EvidencePackage con destino externo (doble control) | No (salvo pyme, con advertencia) | Si (primer control) | No | Si (primer control) | No | No | Si (segundo control, obligatorio) | No | No | No | No |
| Exportar / descargar paquete ya aprobado | Si | Si | Si (el suyo) | Si | Si (el suyo) | No | Si | Si | Solo el suyo | No | No |
| Archivar evidencia (nunca eliminar) | Si | Si | No | Si | No | No | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | Si | Si (en su paquete) | Si (en su tarea) | Si (en su caso) |

Separacion de funciones y doble control: quien carga una evidencia manual no debe ser la unica persona que la aprueba antes de que pase a estado Disponible, salvo pyme por debajo del umbral configurable de `05_tipos_de_usuario.md` seccion 5.4, con advertencia visible de autorrevision. Todo paquete de evidencia cuyo destinatario declarado sea externo a la organizacion (la ACE, un auditor externo, un cliente o socio en due diligence) exige doble control obligatorio: quien lo genera propone la exportacion, y una segunda persona con rol Aprobador (o Delegado/Responsable Legal-Compliance cuando ademas actua como primer control) debe aprobarla antes de que el archivo quede disponible para descarga, sin excepcion de pyme para este paso especifico, porque el riesgo de un envio irreversible a un tercero es distinto del riesgo de una autorrevision interna. El rol Auditor (interno y externo) es siempre de solo lectura en este modulo, igual que en MOD-018: su valor esta en verificar de forma independiente, nunca en cargar o aprobar la evidencia que despues revisa.

---

## D. Informacion de entrada

Entidades principales (segun el mapa definitivo, seccion 7): **Evidence** y **EvidencePackage**. El AuditLog es una entidad transversal consultada, sin modulo propietario unico (seccion 7 de `06_mapa_definitivo_de_modulos.md`); MOD-019 la referencia por evento, nunca la duplica.

### D.0 Catalogo consolidado de tipos de evidencia por modulo de origen

Catalogo construido a partir de la seccion J (Evidencia) de las fichas ya redactadas (MOD-001 a MOD-018 y MOD-021) y, para los modulos aun sin ficha propia (MOD-020, MOD-022 a MOD-026), de su ficha resumida en `06_mapa_definitivo_de_modulos.md` seccion 3. Este catalogo es el que alimenta el campo "Tipo de evidencia" y "Modulo de origen" de la seccion D.1: cuando un modulo genera un registro de esta lista, MOD-019 crea automaticamente la Evidencia correspondiente por referencia, sin que el usuario tenga que cargarla a mano.

| Modulo de origen | Tipo de evidencia (ejemplos) | Obligacion(es) que prueba | Forma | Retencion de referencia |
|---|---|---|---|---|
| MOD-001 Organizacion y Personas | Historial de altas/bajas y cambios de rol; exportacion firmada del listado de usuarios y roles vigentes | OBL-PRIN-03 (control de acceso, insumo del catalogo de seguridad de MOD-015) | Registro / archivo | Indefinida mientras la cuenta este activa, luego segun MOD-016 |
| MOD-002 Delegado / Responsable Interno de Datos | Acta de nombramiento; comunicacion a la ACE; declaracion de conflicto de intereses; atestados de reverificacion; informes periodicos; historial de cambio de `tipo_rol` | OBL-DPO-01 a 08, OBL-PRIN-03 | Archivo / registro / aprobacion | Historico indefinido (5 anos minimo tras el cese para la clausula de confidencialidad, OBL-DPO-06) |
| MOD-003 Onboarding | Fotografia del alta de organizacion, usuarios y roles; aceptacion del descargo de responsabilidad | Insumo indirecto de OBL-DPO-02/03 (no propietario) | Registro | Mientras la cuenta este activa, luego segun MOD-016 |
| MOD-004 Diagnostico de Cumplimiento | Registro de cada respuesta con version del cuestionario; resultado del diagnostico al cierre; version comparativa entre diagnosticos | OBL-AMB-01 a 04; colabora con OBL-PRIN-03 | Registro | Igual que el expediente de cumplimiento de la organizacion (MOD-016) |
| MOD-005 Plan de Cumplimiento | Snapshot congelado de cada version Vigente del plan; historial de cambios de estado y prioridad; registro de aprobacion | OBL-PLAZO-03 | Registro / archivo / aprobacion | Vida de la cuenta mas 5 anos [opinion de producto] |
| MOD-006 RAT y Mapa de Datos | Ficha de tratamiento con historial; justificacion de base de licitud; clasificacion de dato sensible; aprobacion de paso a Vigente | OBL-DOC-02, OBL-PRIN-02, OBL-SENS-01/06/08, OBL-PRIN-03 | Registro / aprobacion | 5 anos como minimo por defecto |
| MOD-007 Consentimiento | Snapshot del texto y version del Aviso al momento de capturar; archivo de firma con hash; historial de estados; aprobacion de revocacion | OBL-CONS-01 a 06, OBL-PRIN-01/04, OBL-SENS-02/03/07, OBL-TRAT-02, **OBL-CONS-05** | Registro / archivo / aprobacion | Segun regla de MOD-016 |
| MOD-008 Documentos y Politicas | Contenido de cada version publicada con hash; registro de aprobaciones; checklist de contenido minimo congelado | OBL-AVISO-01 a 05, OBL-DOC-01, OBL-PRIN-03 | Registro / archivo / aprobacion | Minimo 10 anos por version (OBL-RET-04) |
| MOD-009 Proveedores y Encargados | Historial del proveedor; contrato/DPA vinculado con hash; evidencia de seguridad adjunta; aprobacion de activacion; constancia de devolucion/eliminacion al cierre | OBL-PROV-01 a 07, OBL-PRIN-03 | Registro / archivo / aprobacion | Segun MOD-016 |
| MOD-010 Transferencias Internacionales | Expediente completo de la transferencia; estado de puesta en conocimiento de la ACE; salvaguardas tecnicas documentadas | OBL-TRANSF-01 a 05, **OBL-TRANSF-06** | Registro / archivo | 5 anos minimo tras finalizar [opinion de producto, sin norma expresa] |
| MOD-011 ARCO-POL | Expediente completo con checklist del Art. 18; verificacion de identidad; historial de estados; resolucion motivada; aprobacion del Delegado; notificacion a receptores | OBL-ARCO-01 a 15, refuerza OBL-PRIN-03 | Registro / archivo / aprobacion | 5 anos desde el cierre (**OBL-RET-05**) |
| MOD-012 Portal del Titular | Comprobante de recepcion con version del Aviso y del formulario; registro de verificacion de identidad; bitacora de publicacion | OBL-DOC-04, OBL-PLAZO-04, OBL-PRIN-03 | Registro | Alineado al expediente ARCO-POL relacionado (MOD-011) |
| MOD-013 Incidentes de Seguridad | Expediente completo del incidente; bitacora de deteccion y conocimiento; constancia de envio de cada notificacion; aprobacion del Delegado; registro de la decision de cierre | **OBL-INC-04**, OBL-INC-01/02/03/05, OBL-PRIN-03 | Registro / archivo / aprobacion | 5 anos desde el cierre (**OBL-RET-05**), con cadena de custodia (ver seccion F) |
| MOD-014 Riesgos y EIPD | Version del cuestionario al pasar a Evaluado; aprobacion con identidad y fecha; vinculo con obligaciones de dato sensible que dispararon la evaluacion | OBL-DOC-03, OBL-SEG-02, OBL-SENS-04/06/08 | Registro / aprobacion | Tratamiento activo mas 5 anos [opinion de producto] |
| MOD-015 Controles de Seguridad | Archivo de evidencia de implementacion (captura, contrato, certificado, reporte de pentest); aprobacion de excepcion | OBL-SEG-01 a 06, OBL-SENS-05, OBL-PRIN-03 | Archivo / aprobacion | Indefinida hasta que MOD-016 fije un plazo especifico; algunas con vigencia propia (pentest anual, ver seccion G) |
| MOD-016 Retencion y Eliminacion | Registro de cada regla documentado con fundamento; aprobacion de eliminacion (doble control); constancia de eliminacion | OBL-RET-01 a 06, OBL-PRIN-03 | Registro / aprobacion / archivo | Minimo 5 anos tras el cierre del caso relacionado |
| MOD-017 Capacitacion | Registro de capacitacion recibida por persona; plan anual versionado | OBL-CAP-01/02 | Registro / archivo | Segun MOD-016 |
| MOD-018 Auditoria de Cumplimiento | Informe de auditoria cerrado con hash; hallazgos con evidencia adjunta; aprobacion del cierre | OBL-AUD-01/02, OBL-DPO-07, OBL-PRIN-03, OBL-SEG-02 | Registro / archivo / aprobacion | Indefinida con archivado manual hasta que MOD-016 fije plazo especifico |
| MOD-020 Dashboard y Reportes | No genera evidencia propia; consume la de MOD-019 para sus indicadores | No aplica (sin OBL-ID propio) | No aplica | No aplica |
| MOD-021 Centro de Tareas | Historial de cambios de estado de tarea; registro de aprobacion (identidad, fecha, comentario); archivo adjunto con referencia de integridad; historial de comentarios | OBL-PRIN-03 (de forma transversal, para todas las obligaciones que canalizan tareas) | Registro / aprobacion / archivo | Segun la clasificacion del objeto que la tarea sustenta (MOD-016) |
| MOD-022 Notificaciones | Registro de envio de cada alerta critica (por ejemplo, notificacion de incidente enviada a un destinatario) | Colabora con OBL-INC-01, OBL-INC-03, OBL-ARCO-10 (propiedad de esos modulos) | Registro | Igual que el expediente que origino la notificacion |
| MOD-023 Calendario y Motor de Plazos | Registro del criterio de computo aplicado a cada plazo (dias habiles, horas corridas) y su resultado | Colabora con OBL-PLAZO-01/02 (propietario MOD-023) | Registro | Igual que el expediente que consulto el plazo |
| MOD-024 Centro Regulatorio | Historial de cambios de la bandera `regimen_reforma_659`; expediente del procedimiento sancionador; comprobantes de tramites ante la ACE | OBL-SANC-01 a 09, OBL-PLAZO-05, **OBL-SANC-07** | Registro / archivo | 5 anos minimo (**OBL-SANC-07**), o segun se defina para el expediente sancionador especifico |
| MOD-025 Busqueda Global | No genera evidencia, modulo transversal de solo lectura | No aplica (sin OBL-ID propio) | No aplica | No aplica |
| MOD-026 Centro de Ayuda | No genera evidencia (modulo de solo lectura) | No aplica | No aplica | No aplica |

Nota de consistencia: los cinco "tipos de evidencia" marcados en negrita en la columna de obligacion corresponden exactamente a las cinco obligaciones colaboradoras de este modulo, tal como las declara `mapa_modulos.json` (la obligacion propietaria, OBL-PRIN-03, no se marca en negrita en esta tabla porque aparece de forma transversal en casi todas las filas, no como una colaboracion puntual).

### D.1 Campos de Evidence

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Obligacion(es) relacionada(s) | Referencia multiple a OBL-ID | Obligatorio | Catalogo de las 105 obligaciones de la matriz | Al menos una | "A que obligacion de la matriz corresponde esta evidencia." | OBL-PRIN-03 |
| Modulo de origen | Seleccion unica, catalogo de D.0 | Obligatorio (autogenerado si el registro nace de otro modulo) | Catalogo de D.0 (MOD-001 a MOD-018, MOD-021, MOD-024) | Debe existir en el catalogo | "De donde viene esta evidencia dentro del sistema." | Buena practica (trazabilidad) |
| Tipo de evidencia | Seleccion unica, catalogo de D.0 | Obligatorio | Registro / Archivo / Aprobacion / Log | Debe coincidir con la forma declarada en D.0 para ese modulo de origen | "Que clase de prueba es: un registro del sistema, un archivo adjunto, una aprobacion con identidad, o una entrada del historial tecnico." | Buena practica |
| Origen del registro | Seleccion unica | Obligatorio (autogenerado) | Automatico (el modulo estructurado lo genero solo) / Manual (cargado directamente porque el modulo de origen aun no esta disponible en el MVP) | - | "Si esta evidencia llego sola desde otro modulo, o si alguien la subio a mano porque ese modulo todavia no existe en su version del sistema." | Patron de cobertura parcial de `06_mapa_definitivo_de_modulos.md` (por ejemplo, MOD-009 y MOD-010 seccion Q) |
| Entidad de origen (referencia) | Referencia a otra entidad, o vacio si es Manual | Obligatorio si Origen = Automatico | Registro especifico del modulo de origen (por ejemplo, el Consent de MOD-007, el Incident de MOD-013) | Debe existir el registro referenciado | "El registro exacto del otro modulo del que viene esta evidencia; hacer clic aqui abre ese registro." | Buena practica (evita duplicar el dato, regla de direccion unica de `06_mapa_definitivo_de_modulos.md` seccion 4) |
| Archivo adjunto | Archivo, o vacio si la evidencia es solo referencia | Condicional (obligatorio si Tipo de evidencia = Archivo) | Tipos permitidos por politica de seguridad de la organizacion | Verificacion de tipo de archivo; calculo de hash al cargarse | "Adjunte el archivo que sirve de prueba, por ejemplo el certificado, el contrato firmado o el reporte de la firma auditora." | Buena practica |
| Huella de integridad (hash) | Texto (autogenerado) | Autogenerado al cargar el archivo, o heredado del modulo de origen si ya lo calculo alli | - | No editable | "Codigo que permite comprobar despues que este archivo no fue alterado." | Anti-feature 25, decision 2.7.24 |
| Fecha de captura | Fecha y hora (autogenerada) | Autogenerado | - | No editable | "Cuando quedo registrada esta evidencia por primera vez." | Buena practica |
| Fecha de vigencia (si aplica) | Fecha | Opcional (obligatorio si el tipo de control tiene renovacion periodica, por ejemplo un pentest anual) | - | Fecha futura al momento de aprobarse | "Hasta cuando sigue siendo valida esta evidencia antes de necesitar renovarse." | OBL-SEG-03 (colaboradora), buena practica |
| Estado de la evidencia | Seleccion unica | Obligatorio (valor inicial depende de si se detecto un hueco o se cargo evidencia) | Faltante / En revision / Disponible / Vencida / Rechazada / Archivada | Solo transiciones permitidas por el flujo de la seccion F | "En que punto esta esta evidencia: si falta, si esta pendiente de aprobar, si ya esta disponible, si vencio, o si fue rechazada." | Anti-feature 5 (nunca "cumple/no cumple") |
| Responsable de carga | Referencia a usuario (autogenerado) | Autogenerado | Usuario autenticado que carga o que genero el registro en el modulo de origen | No editable | "Quien registro esta evidencia." | OBL-PRIN-03 |
| Aprobador | Referencia a usuario | Obligatorio antes de pasar a Disponible, si el Origen es Manual | Usuario con rol Aprobador o Delegado/Resp. Legal-Compliance, distinto del responsable de carga (salvo pyme) | - | "Quien reviso y confirmo que esta evidencia es correcta." | Separacion de funciones, `05_tipos_de_usuario.md` seccion 5.4 |
| Motivo de rechazo | Texto | Obligatorio si Estado = Rechazada | - | Minimo 10 caracteres | "Por que esta evidencia no se acepto tal como se cargo." | Buena practica |
| Nivel de sensibilidad del contenido | Seleccion unica | Obligatorio | Sin datos personales / Datos personales de identificacion basica / Datos personales sensibles / Informacion tecnica de seguridad sensible | - | "Si este archivo contiene datos de personas o informacion tecnica delicada, para decidir quien puede verlo." | Privacy by design (ver D.3) |
| Bloqueada (procedimiento o reclamo abierto) | Booleano (autogenerado) | Autogenerado | Si / No | No editable directamente por el usuario | "Esta evidencia no se puede archivar ni reemplazar porque esta vinculada a un caso todavia abierto." | OBL-RET-05, OBL-SANC-07 |
| Version | Numero (autogenerado) | Autogenerado | - | Solo se incrementa, nunca se sobrescribe una version anterior | "Cuantas veces se renovo o se reemplazo esta evidencia; las versiones anteriores nunca se borran." | OBL-PRIN-03 |

### D.2 Campos de EvidencePackage

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Nombre del paquete | Texto corto | Obligatorio | - | No vacio; sugerido por defecto segun el tipo | "Ponle un nombre que identifique para que es este paquete, por ejemplo: Paquete para auditoria anual 2027." | Buena practica |
| Tipo de paquete | Seleccion unica | Obligatorio | Auditoria anual (MOD-018) / Requerimiento de la ACE / Procedimiento sancionador (MOD-024) / Due diligence de cliente o socio / Preparacion de inspeccion / Paquete a medida | Debe elegir uno | "Para que va a usar este paquete; el sistema ajusta el contenido sugerido segun el tipo." | Buena practica, faltante 14 de `02_validacion_de_la_idea.md` (preparacion de inspeccion) |
| Filtro por periodo | Rango de fechas | Opcional | - | Fecha desde anterior a fecha hasta | "Limita el paquete a evidencia capturada dentro de este rango de fechas." | Buena practica |
| Filtro por obligacion | Referencia multiple a OBL-ID | Opcional | Catalogo de las 105 obligaciones | - | "Limita el paquete a una o varias obligaciones especificas." | OBL-PRIN-03 |
| Filtro por modulo de origen | Seleccion multiple | Opcional | Catalogo de D.0 | - | "Limita el paquete a la evidencia que viene de ciertos modulos, por ejemplo solo Incidentes." | Buena practica |
| Contenido (evidencias incluidas) | Lista de referencias a Evidence, mas Documentos y eventos de AuditLog relacionados | Autogenerado a partir de los filtros, editable antes de aprobar | - | Al menos un elemento | "Esta es la lista de lo que va a incluir el paquete; puede quitar elementos antes de generarlo." | Decision 2.7.4 |
| Destinatario declarado | Seleccion unica | Obligatorio | Uso interno / ACE / Auditor externo / Cliente o socio (due diligence) / Otro (especificar) | - | "Quien va a recibir este paquete; si es externo, se activa el segundo control de aprobacion." | Doble control, `05_tipos_de_usuario.md` seccion 5.4 |
| Manifiesto | Documento generado (autogenerado) | Autogenerado al generar el paquete | - | No editable | "Lista con el hash de cada archivo incluido y el hash del conjunto, para poder comprobar despues que nada cambio." | Anti-feature 25, decision 2.7.24 |
| Firma o huella del paquete completo | Texto (autogenerado) | Autogenerado al aprobarse la exportacion | - | No editable | "El codigo de verificacion de todo el paquete junto, no solo de cada archivo por separado." | Anti-feature 25 |
| Estado del paquete | Seleccion unica | Obligatorio (valor inicial: Borrador) | Borrador / Pendiente de segundo control / Aprobado / Exportado / Archivado | Solo transiciones permitidas por el flujo de la seccion F | "En que etapa esta este paquete." | Buena practica |
| Formato de exportacion | Seleccion unica | Obligatorio antes de exportar | PDF / XLSX / CSV / ZIP con manifiesto | - | "En que formato quiere descargar el paquete." | Sec. 30 del documento maestro, sin mandato legal de formato (seccion 2.3.5) |
| Aprobador del segundo control | Referencia a usuario | Obligatorio si Destinatario = externo | Usuario con rol Aprobador, distinto de quien genero el paquete | - | "Quien dio el segundo visto bueno antes de que el paquete saliera de la organizacion." | Doble control |

**Campos precargados.** El contenido de un EvidencePackage se precarga automaticamente a partir de los filtros elegidos, consultando en tiempo real la Evidencia ya acumulada de MOD-007 a MOD-018 mas los eventos de AuditLog relacionados; nunca se copian los Documentos de MOD-008 dentro del paquete, se referencian por version exacta y, si el formato lo permite, se adjunta la version congelada que ya existe en ese modulo.

**Minimizacion de datos personales (privacy by design).** La Evidencia de este modulo puede contener, de forma legitima y necesaria, datos personales de titulares externos: un expediente ARCO-POL (MOD-011) incluye documentos de identidad, un expediente de incidente (MOD-013) puede describir a las personas afectadas, un registro de consentimiento (MOD-007) incluye la firma del titular. A diferencia del RAT o del catalogo de proveedores, aqui el principio de minimizacion no significa "no guardar el dato", porque el dato personal es el objeto legitimo de la prueba (decision de alcance 2.7.21 de `02_validacion_de_la_idea.md`, misma logica que MOD-011). Se aplica en su lugar:
- **Control de acceso por nivel de sensibilidad**: el campo "Nivel de sensibilidad del contenido" de cada Evidencia determina quien puede verla (ver seccion C); un Responsable de area nunca ve, por ejemplo, la evidencia de un incidente que no le fue asignado.
- **Guia de minimizacion antes de adjuntar**: el texto de ayuda al cargar evidencia manual advierte explicitamente "no adjunte una base de datos completa ni un listado de clientes; adjunte solo el documento puntual que prueba esta obligacion, y reemplace por una referencia cualquier dato que no sea estrictamente necesario para la prueba" (anti-features 1, 8 y 9 de `22_anti_features.md`).
- **Nunca copiar bases de datos del cliente**: MOD-019 no ofrece ninguna funcionalidad de importacion masiva de bases de datos externas; toda evidencia se carga archivo por archivo o llega por referencia estructurada de otro modulo.
- **Evidencia tecnica sensible** (por ejemplo, un reporte de pentest que detalla vulnerabilidades reales): mismo criterio reforzado que ya aplica MOD-015, acceso restringido a los roles con necesidad de conocerla.

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Vista "que evidencia tenemos de esta obligacion" | Las 105 obligaciones de la matriz, cada una con su evidencia registrada, su estado y su fecha de ultima actualizacion | Vista en pantalla, filtrable por modulo, area o estado | Consulta continua, en tiempo real | Delegado/Resp. interno, Resp. Legal/Compliance, Administrador, Auditor (lectura) |
| Informe de huecos de evidencia | Lista de obligaciones aplicables (segun el diagnostico de MOD-004) sin ninguna evidencia registrada, priorizadas por clasificacion (OBLIGATORIO primero) | Reporte exportable | Bajo demanda, y automaticamente tras cada diagnostico cerrado | Delegado/Resp. interno, Gerencia |
| Alerta de evidencia vencida o por renovar | Evidencia cuya fecha de vigencia esta por cumplirse o ya paso | Tarea en MOD-021 y alerta en MOD-022 | Segun calendario (MOD-023), antes del vencimiento | Responsable de carga original, Delegado/Resp. interno |
| EvidencePackage generado | Manifiesto mas archivos o referencias incluidas, con verificacion de integridad | PDF / XLSX / CSV / ZIP segun el formato elegido | Al completar el flujo de generacion y aprobacion (ver seccion F) | Quien lo solicito, mas el destinatario declarado |
| Indicador "Evidencia disponible por obligacion" | Cuenta y proporcion de obligaciones aplicables con evidencia en estado Disponible | Indicador de dashboard (MOD-020) | Recalculado en cada cambio de estado de Evidence | Gerencia, Legal/Delegado, Auditor |
| Evento de auditoria (AuditLog) | Quien hizo que, cuando, sobre que evidencia o paquete | Registro tecnico inmutable | En cada creacion, cambio de estado, aprobacion, exportacion o acceso de lectura a evidencia sensible | Consultado por MOD-018 |

---

## F. Workflow

### F.1 Workflow de Evidence

```
   se detecta que una obligacion aplica
   (diagnostico, MOD-004) sin evidencia
                    |
                    v
          +--------------------+
          |      FALTANTE      | <----------------------------+
          +--------------------+                               |
             |                                                  |
   se carga   | (manual) o llega automatica-                    | rechazo
   evidencia  | mente desde un modulo de origen                 | (con motivo)
                    |                                            |
                    v                                            |
          +--------------------+                                |
          |    EN REVISION     | ------------------------------>+
          +--------------------+     (si Origen = Manual;
                    |                 si Origen = Automatico,
   se aprueba        |                 pasa directo a DISPONIBLE)
   (o llega ya                       |
   aprobada del modulo de origen)    |
                    v
          +--------------------+
          |     DISPONIBLE     | <----------------------------+
          +--------------------+                               |
             |                |                                 |
   se cumple  |                | se renueva (nueva version,     |
   la fecha   |                | version anterior pasa a         |
   de vigencia|                | HISTORICA, ver abajo)            |
             v                v                                |
   +--------------------+   (vuelve a DISPONIBLE) ---------------+
   |      VENCIDA       |
   +--------------------+
             |
             | la obligacion deja de aplicar (cambio de regimen
             | en MOD-024, o el objeto que documenta se archiva
             | en su modulo de origen)
             v
   +--------------------+
   |     ARCHIVADA      |  (terminal; nunca se elimina, anti-feature 19)
   +--------------------+
```

Tabla de transiciones de Evidence:

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (ninguno) | El diagnostico (MOD-004) confirma que una obligacion aplica | No existe evidencia registrada para esa obligacion | Faltante | Sistema (automatico) | Aparece en el informe de huecos (seccion E); crea tarea sugerida en MOD-021 si la obligacion es OBLIGATORIO |
| Faltante | Cargar evidencia manual | Archivo adjunto o referencia valida | En revision | Responsable de area, Resp. Seguridad/IT, Resp. ARCO-POL, Delegado/Resp. interno, Usuario de consulta (en su tarea) | Evento en AuditLog; notifica al Aprobador configurado |
| Faltante | Un modulo estructurado genera el registro de origen (por ejemplo, MOD-007 aprueba un consentimiento) | Origen = Automatico | Disponible | Sistema (automatico) | Se enlaza por referencia, sin duplicar el dato; evento en AuditLog |
| En revision | Aprobar | El aprobador es distinto de quien cargo (salvo pyme con advertencia) | Disponible | Aprobador, Delegado/Resp. interno, Resp. Legal/Compliance | Evidencia queda inmutable en su version actual (ver nota de integridad); evento en AuditLog |
| En revision | Rechazar | Motivo obligatorio | Faltante (con la nota del motivo visible) | Aprobador, Delegado/Resp. interno, Resp. Legal/Compliance | Notifica a quien cargo la evidencia; evento en AuditLog |
| Disponible | Pasar la fecha de vigencia sin renovar | Solo si el tipo de evidencia tiene fecha de vigencia definida | Vencida | Sistema (automatico) | Alerta segun seccion I; el indicador de dashboard baja de verde a amarillo o rojo |
| Disponible / Vencida | Cargar una renovacion | Nuevo archivo o referencia valida | Disponible (nueva version; la version anterior pasa a Historica, conservada integra) | Mismo criterio que la carga original | Version anterior nunca se sobrescribe; evento en AuditLog |
| Disponible / Vencida | La obligacion deja de aplicar (cambio de regimen en MOD-024) o el objeto de origen se archiva | Ninguna evidencia Bloqueada puede pasar por esta transicion mientras el bloqueo siga activo | Archivada | Sistema (automatico), con confirmacion visible del Administrador | Se marca "no aplica bajo el estado regulatorio actual, ver historial", nunca se elimina (mismo patron de MOD-021, seccion 5 punto 6 del mapa definitivo) |
| Cualquier estado | Se abre un procedimiento sancionador (MOD-024) o un reclamo ante la ACE (MOD-011) que referencia esta evidencia | El expediente relacionado pasa a un estado abierto | (sin cambio de estado visible; se activa el campo Bloqueada = Si) | Sistema (automatico) | Bloquea archivado y reemplazo hasta que el expediente relacionado se cierre; evento en AuditLog |

Estados terminales: Archivada es terminal salvo reapertura del expediente que la origino (en cuyo caso vuelve a Disponible, con el historial intacto). Ninguna evidencia se elimina nunca, solo se archiva (anti-feature 19 de `22_anti_features.md`); lo unico que puede ocurrir con un archivo es su reemplazo por una version nueva, conservando siempre la version anterior.

**Inmutabilidad y cadena de custodia.** Una vez que una Evidencia pasa a Disponible, su contenido (archivo, huella de integridad, fecha, responsable) no puede editarse; solo puede renovarse (nueva version) o archivarse. Para la evidencia que proviene de MOD-013 Incidentes de Seguridad, este mismo mecanismo funciona como cadena de custodia funcional: cada acceso de lectura queda registrado (seccion O), el archivo original nunca se sobrescribe, y cualquier version posterior (por ejemplo, una copia forense adicional) se agrega como una nueva pieza de evidencia enlazada al mismo incidente, nunca reemplazando la anterior, para que el expediente conserve intacta su capacidad probatoria si mas adelante se usa en un procedimiento sancionador (MOD-024) o ante un requerimiento de la ACE.

### F.2 Workflow de EvidencePackage

```
   se solicita un paquete
   (filtros elegidos)
        |
        v
   +-----------+     destino interno,     +-----------+     se exporta      +-----------+
   |  BORRADOR | ----- se aprueba ------> | APROBADO  | ------------------> | EXPORTADO |
   +-----------+                          +-----------+                     +-----------+
        |                                                                        |
        | destino externo declarado                                             | pasa el
        v                                                                        | tiempo de
   +---------------------------+     segundo control      +-----------+          | retencion
   | PENDIENTE DE SEGUNDO      | ------- aprueba -------> | APROBADO  |          v
   | CONTROL                   |                          +-----------+    +-----------+
   +---------------------------+                                           | ARCHIVADO |
        |                                                                  +-----------+
        | segundo control rechaza (motivo obligatorio)
        v
   +-----------+
   |  BORRADOR | (vuelve, con el motivo de rechazo visible)
   +-----------+
```

Tabla de transiciones de EvidencePackage:

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (nuevo) | Elegir tipo y filtros, generar contenido | Al menos un elemento de contenido resultante | Borrador | Delegado/Resp. interno, Resp. Legal/Compliance, Resp. ARCO-POL (su expediente), Resp. Seguridad/IT (sus controles), Administrador | Calcula el manifiesto en borrador; evento en AuditLog |
| Borrador | Aprobar (destino interno) | Destinatario declarado = Uso interno | Aprobado | Aprobador, Delegado/Resp. interno, Resp. Legal/Compliance | Calcula la firma/huella del paquete completo; evento en AuditLog |
| Borrador | Enviar a segundo control (destino externo) | Destinatario declarado distinto de Uso interno | Pendiente de segundo control | Delegado/Resp. interno, Resp. Legal/Compliance, Administrador (pyme, con advertencia) | Notifica al Aprobador designado como segundo control |
| Pendiente de segundo control | Aprobar | El aprobador es distinto de quien genero el paquete (sin excepcion de pyme para este paso) | Aprobado | Aprobador | Calcula la firma/huella del paquete completo; evento en AuditLog |
| Pendiente de segundo control | Rechazar | Motivo obligatorio | Borrador | Aprobador | Notifica a quien genero el paquete; evento en AuditLog |
| Aprobado | Exportar (descargar en el formato elegido) | El paquete debe conservar su firma valida | Exportado | Quien aprobo, o quien genero si el destino es interno | Registro de exportacion con fecha, usuario y destinatario (seccion O); no se puede editar el contenido despues de exportado, solo generar un paquete nuevo |
| Exportado | Cumplir el plazo de retencion de exportaciones | Automatico, sin intervencion humana | Archivado | Sistema (automatico) | El registro de que la exportacion ocurrio se conserva indefinidamente aunque el archivo exportado quede fuera del sistema, igual que en MOD-009 |

Estados terminales: Archivado es terminal; un paquete exportado nunca se modifica, cualquier cambio de alcance requiere generar un paquete nuevo, para que cada exportacion sea individualmente verificable.

---

## G. Automatizaciones

| Disparador | Condicion | Accion | Configurable por la empresa |
|---|---|---|---|
| MOD-004 confirma que una obligacion aplica a la organizacion | No existe evidencia registrada para esa obligacion | Crea el registro Faltante y, si la obligacion es OBLIGATORIO, sugiere una tarea en MOD-021 | No (la deteccion es automatica; el usuario puede posponer la tarea sugerida) |
| Un modulo estructurado (MOD-007 a MOD-018) aprueba, cierra o publica un registro que segun D.0 constituye evidencia | Siempre | Crea automaticamente la Evidencia correspondiente por referencia, estado Disponible, sin pasar por revision manual | No |
| Una Evidencia con fecha de vigencia definida llega a 30 dias de su vencimiento | Siempre | Crea alerta WARNING (ver seccion I) y tarea de renovacion en MOD-021 para el responsable de carga original | Si (los dias de anticipacion son configurables) |
| Una Evidencia con fecha de vigencia definida vence sin renovarse | Siempre | Cambia el estado a Vencida; alerta HIGH; el indicador de dashboard de esa obligacion pasa a amarillo o rojo segun el tiempo transcurrido | No |
| Se activa la bandera `regimen_reforma_659` de MOD-024 | Existe evidencia Disponible o Vencida vinculada a una obligacion afectada por la reforma | No reinterpreta ni archiva automaticamente esa evidencia; solo la marca con el regimen bajo el que se genero para contexto historico | No |
| Se abre un procedimiento sancionador (MOD-024) o un reclamo ante la Direccion de Proteccion de Datos (MOD-011, OBL-ARCO-14) que referencia una o mas Evidencias | Siempre | Marca esas Evidencias como Bloqueada = Si; impide su archivado o reemplazo hasta que el expediente relacionado se cierre | No |
| Se genera un EvidencePackage con destinatario declarado distinto de Uso interno | Siempre | Exige el segundo control antes de habilitar la exportacion, sin excepcion configurable | No |
| Se aprueba (o se aprueba con segundo control) un EvidencePackage | Siempre | Calcula la huella o firma del manifiesto y del paquete completo | No |
| Se exporta un EvidencePackage | Siempre | Registra el evento de exportacion con fecha, usuario, destinatario declarado y formato, de forma permanente e inmutable | No |
| Se completa el diagnostico inicial o un re-diagnostico (MOD-004) | Cambia el conjunto de obligaciones aplicables | Recalcula el informe de huecos de evidencia | No |

---

## H. Decisiones que NO debe automatizar

- **Si la evidencia disponible es suficiente para demostrar cumplimiento de una obligacion.** El sistema muestra que evidencia existe y en que estado esta, nunca concluye "esta obligacion esta cumplida"; esa lectura corresponde siempre a una persona responsable o a asesoria especializada. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada."
- **Si un hueco de evidencia constituye, por si mismo, una infraccion sancionable.** El sistema solo senala la ausencia de registro frente a una obligacion aplicable; calificar esa ausencia como infraccion leve, grave o muy grave del Art. 56 es facultad exclusiva de la ACE. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada."
- **Aprobar evidencia cargada manualmente.** El sistema nunca marca una evidencia manual como Disponible sin la accion explicita de un Aprobador (salvo la excepcion de pyme, siempre con advertencia visible de autorrevision); dejar pasar evidencia sin revision humana anula el valor probatorio de la separacion de funciones. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada."
- **Exportar un paquete de evidencia con destino externo sin el segundo control.** Nunca se habilita la descarga de un paquete destinado a la ACE, a un auditor externo o a un tercero en due diligence sin la aprobacion explicita de una segunda persona; el riesgo de un envio irreversible fuera de la organizacion no admite excepcion automatica, ni siquiera en pyme. No es unicamente una decision juridica, por lo que no siempre lleva el texto de advertencia legal, pero el sistema bloquea el boton de exportar hasta que el segundo control se registre.
- **Decidir si una evidencia rechazada requiere ademas abrir un caso en otro modulo** (por ejemplo, si la evidencia rechazada de un incidente revela en realidad una vulneracion no reportada). El sistema puede sugerir la conexion, pero la persona responsable decide si corresponde abrir el caso correspondiente. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada."
- **Archivar evidencia bloqueada por un procedimiento o reclamo abierto, incluso a peticion del Administrador.** El sistema impide esta accion mientras el bloqueo este activo, sin excepcion manual, porque hacerlo comprometeria la prueba de descargo que el propio procedimiento necesita.

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia o repeticion | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Hueco de evidencia detectado (obligacion OBLIGATORIO) | El diagnostico confirma una obligacion aplicable sin evidencia registrada | WARNING | Delegado/Resp. interno, Resp. Legal/Compliance | Plataforma | Una vez por hueco, mas recordatorio semanal mientras siga abierto | Escala a Gerencia a los 30 dias sin resolver | Se carga y aprueba evidencia, o la obligacion deja de aplicar |
| Evidencia por vencer | Faltan 30 dias para la fecha de vigencia de una evidencia con renovacion periodica | WARNING | Responsable de carga original, Delegado/Resp. interno | Plataforma y correo | Cada 7 dias | Si sigue sin renovarse a los 15 dias, escala al Aprobador correspondiente | Se carga la renovacion y se aprueba |
| Evidencia vencida | Paso la fecha de vigencia sin renovacion | HIGH | Responsable de carga original, Delegado/Resp. interno, Resp. Legal/Compliance | Plataforma y correo | Semanal | Escala a Gerencia a los 30 dias vencida | Se carga la renovacion y se aprueba |
| Evidencia rechazada | Un Aprobador rechaza una evidencia cargada manualmente | INFO | Responsable de carga original | Plataforma | Una vez | No escala | Se vuelve a cargar y se aprueba |
| Evidencia cargada pendiente de aprobacion | Una evidencia manual queda En revision mas de 5 dias habiles | WARNING | Aprobador designado, Delegado/Resp. interno | Plataforma y correo | Cada 3 dias | Escala al Administrador a los 10 dias habiles | Se aprueba o se rechaza |
| Paquete de evidencia pendiente de segundo control | Un EvidencePackage con destino externo queda mas de 3 dias habiles sin el segundo control | WARNING | Aprobador designado como segundo control | Plataforma y correo | Diaria mientras siga pendiente | Escala al Administrador a los 5 dias habiles | Se aprueba o se rechaza el segundo control |
| Exportacion de paquete completada | Se exporta un EvidencePackage | INFO | Quien lo genero, quien aprobo, Auditor (lectura) | Plataforma | Una vez | No escala | No aplica (es informativa) |

---

## J. Evidencia

### J.1 Catalogo consolidado de evidencia por modulo de origen

Ver seccion D.0: esa tabla es, en si misma, el resultado consolidado que exige el enfoque especifico de esta ficha, y es la fuente unica que usa el campo "Tipo de evidencia" de la seccion D.1. No se repite aqui para evitar mantener dos copias del mismo catalogo.

### J.2 Evidencia propia del modulo (sobre sus propias acciones)

MOD-019 no solo conserva la evidencia de los demas modulos: tambien genera evidencia sobre su propia actividad, que a su vez debe poder auditarse.

| Que genera o conserva | Como | Obligacion que prueba (OBL-ID) | Conservacion |
|---|---|---|---|
| Historial completo de cambios de estado de cada Evidence (Faltante, En revision, Disponible, Vencida, Rechazada, Archivada) | AuditLog append-only, con usuario, fecha y motivo cuando aplica | OBL-PRIN-03 | Igual que la Evidencia que documenta |
| Aprobacion de evidencia cargada manualmente, con identidad del aprobador y fecha | Registro inmutable, distinto de quien cargo | OBL-PRIN-03 | Igual que la Evidencia aprobada |
| Manifiesto y firma/huella de cada EvidencePackage generado | Archivo generado con hash, version y fecha | Anti-feature 25, decision 2.7.24; sustenta **OBL-CONS-05** y **OBL-TRANSF-06** cuando el paquete se usa para probar la carga de la prueba ante un tercero | Igual que el registro de exportacion asociado |
| Segundo control de exportacion externa, con identidad de ambos aprobadores y fecha | Registro inmutable | OBL-PRIN-03 | Igual que el paquete exportado |
| Registro de cada exportacion (quien, cuando, destinatario declarado, formato) | Evento de auditoria permanente, aunque el archivo exportado quede fuera del sistema | OBL-PRIN-03, anti-feature 25 | Permanente |
| Accesos de lectura a evidencia con nivel de sensibilidad "Datos personales sensibles" o "Informacion tecnica de seguridad sensible" | Registro de quien la consulto y cuando | Buena practica de seguridad y privacidad, sin OBL-ID propio | Igual que la Evidencia consultada |
| Historial de activaciones y liberaciones del campo Bloqueada por procedimiento o reclamo abierto | Registro con fecha y referencia al expediente que origino el bloqueo | **OBL-RET-05**, **OBL-SANC-07** | Igual que la Evidencia bloqueada |

**Sobre el plazo de conservacion.** MOD-019 no fija un plazo de retencion propio distinto del que ya declara cada obligacion o cada modulo de origen (regla de direccion unica, seccion 4 de `06_mapa_definitivo_de_modulos.md`): conserva cada pieza de evidencia al menos durante el plazo que indique su propio origen (por ejemplo, 5 anos para expedientes ARCO-POL e incidentes segun **OBL-RET-05**, 10 anos para avisos de privacidad segun OBL-RET-04, propiedad de MOD-016, colaboradora MOD-008 (Actualizacion 2026-09-24, fase 3: se corrige el modulo propietario citado, antes atribuido por error a MOD-008; ver `02_validacion/06_mapa_definitivo_de_modulos.md`, seccion 8, y `02_validacion/mapa_modulos.json`, obligaciones_propietarias de MOD-016)). Nota de clasificacion sobre **OBL-RET-05**: `matriz_obligaciones.json` la clasifica RECOMENDADO, con la condicion expresa "criterio de diseno recomendado ante ausencia de norma expresa; requiere validacion de abogado", porque ninguna norma fija hoy de forma expresa el plazo de conservacion del expediente ARCO-POL/incidentes; el plazo de 5 anos que usa este parrafo, y el bloqueo de evidencia de la seccion F que se apoya en el, son el criterio de diseno por defecto del sistema mientras esa validacion de asesoria juridica no lo confirme o lo ajuste. Donde ese plazo no esta definido por el modulo de origen ni por una obligacion especifica, MOD-019 usa como minimo el mismo criterio que **OBL-SANC-07** fija para la prescripcion de infracciones y sanciones (5 anos), por ser el horizonte de retencion mas conservador que ya usa el resto del sistema para evidencia de cumplimiento sin plazo propio (mismo patron que aplican MOD-005, MOD-010 y MOD-014). El registro de que una exportacion ocurrio se conserva siempre de forma permanente, incluso si el archivo exportado en si queda fuera del sistema una vez entregado al destinatario.

---

## K. Documentos asociados

- **Documentos requeridos como entrada.** Ninguno propio: MOD-019 referencia por version exacta los Documentos que administra MOD-008 (avisos, politicas, contratos), sin copiarlos ni mantener una segunda version. Cuando un EvidencePackage incluye un Documento, incluye la version congelada exacta que estaba vigente en el momento relevante, tal como la conserva MOD-008.
- **Documentos generados.** Manifiesto de cada EvidencePackage (lista de contenido con hash por archivo y hash del conjunto); informe de huecos de evidencia (lista de obligaciones aplicables sin evidencia registrada); informe "evidencia por vencer".
- **Plantillas que el sistema provee.** "Manifiesto de paquete de evidencia" (variables: tipo de paquete, filtros aplicados, lista de evidencias y documentos incluidos, hash de cada uno, hash del conjunto, fecha de generacion, aprobadores), marcada como un artefacto tecnico generado automaticamente, no como un documento que requiera redaccion; "Informe de brecha de evidencia" (variables: obligacion, articulo, clasificacion, modulo sugerido, fecha desde que aplica), pensado para que el Delegado/Responsable interno lo revise antes de asignar tareas.
- **Anexos y evidencias documentales.** Todo archivo adjunto a una Evidence conserva su propio hash y queda disponible como anexo de cualquier EvidencePackage que lo incluya; los anexos nunca se duplican fisicamente entre paquetes, cada paquete los referencia con su propia verificacion.

---

## L. Dependencias

```
MOD-007 Consentimiento -----------------+
MOD-008 Documentos y Politicas ---------+
MOD-009 Proveedores y Encargados -------+
MOD-010 Transferencias Internacionales -+
MOD-011 ARCO-POL ------------------------+
MOD-012 Portal del Titular --------------+---> MOD-019 CENTRO DE EVIDENCIAS ---> MOD-020 Dashboard y Reportes
MOD-013 Incidentes de Seguridad --------+              |          ^                  |
MOD-014 Riesgos y EIPD -----------------+              |          |                  +--> MOD-024 Centro Regulatorio
MOD-015 Controles de Seguridad ---------+              |          |                       (procedimiento sancionador,
MOD-016 Retencion y Eliminacion --------+              |          |                        tramites ante la ACE)
MOD-017 Capacitacion --------------------+              |          |
MOD-018 Auditoria de Cumplimiento ------+ (relacion    |          |
     reciproca, ver nota debajo)                       +----------+
                                              (informe y hallazgos cerrados
                                               de MOD-018 se registran como
                                               nueva evidencia en MOD-019)

     Capa transversal (consultada, nunca consulta al reves):
     MOD-001 Organizacion | MOD-021 Tareas | MOD-022 Notificaciones
     MOD-023 Calendario y Motor de Plazos | MOD-024 Centro Regulatorio (bandera) | MOD-026 Ayuda
```

- **De que modulos recibe datos.** MOD-007, MOD-008, MOD-009, MOD-010, MOD-011, MOD-012, MOD-013, MOD-014, MOD-015, MOD-016, MOD-017 y MOD-018, tal como declara `mapa_modulos.json`: cada uno entrega evidencia de forma continua conforme genera, aprueba o cierra sus propios registros, siguiendo el catalogo de la seccion D.0.
- **A que modulos envia datos o eventos.** MOD-018 (evidencia acumulada que la auditoria sustantiva consulta para elaborar sus hallazgos, en relacion reciproca, ver nota debajo), MOD-020 (indicadores de evidencia disponible, huecos y vencimientos para el dashboard), MOD-024 (paquetes de evidencia para el procedimiento sancionador y para los tramites ante la ACE).
- **Catalogos que comparte.** El catalogo de las 105 obligaciones (OBL-ID) de la matriz, que consume por referencia igual que todos los modulos de recorrido; el catalogo de modulos de origen y tipos de evidencia de la seccion D.0, que es propio de este modulo y que otros modulos consultan cuando describen su propia seccion J (Evidencia).
- **Relacion reciproca con MOD-018.** MOD-019 declara `depende_de` a MOD-018 y MOD-018 declara `depende_de` a MOD-019 en `mapa_modulos.json`; es la unica excepcion de todo el mapa a la regla de que `depende_de` es aciclico (`06_mapa_definitivo_de_modulos.md`, seccion 6.1). No es un error de copia: MOD-018 consulta la evidencia ya acumulada en MOD-019 (recibida de MOD-007 a MOD-017 de forma continua) para elaborar sus hallazgos de auditoria, y el informe y los hallazgos resultantes de MOD-018 se registran a su vez como nueva evidencia en MOD-019 (ver seccion D.0, fila MOD-018). Es una dependencia de datos bidireccional y continua entre los dos modulos de la etapa Demostrar, no una precedencia de construccion.
- **Que ocurre si un modulo dependiente no existe en el MVP.** De los doce modulos que alimentan a MOD-019, solo MOD-010 (Transferencias Internacionales), MOD-012 (Portal del Titular), MOD-014 (Riesgos y EIPD), MOD-016 (Retencion y Eliminacion) y MOD-018 (Auditoria de Cumplimiento) son SHOULD HAVE; el resto son MUST HAVE y estan garantizados en el MVP. Mientras alguno de esos cinco modulos SHOULD HAVE no este disponible para una organizacion, el patron de cobertura parcial que ya describen sus propias fichas (por ejemplo, MOD-010 seccion Q, MOD-009 seccion L) aplica de forma simetrica en MOD-019: la evidencia relacionada se registra como "evidencia suelta" con Origen = Manual (campo de la seccion D.1), cargada por un Responsable de area o por el Delegado a partir de la tarea manual que crea MOD-021, en vez de llegar automaticamente por referencia estructurada. El informe de huecos de evidencia (seccion E) sigue funcionando igual en ambos casos, porque no distingue si la evidencia esperada vendria de un modulo estructurado o de una carga manual, solo si existe o no.

---

## M. Dashboard

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Evidencia disponible por obligacion aplicable | Cuenta de obligaciones aplicables (segun el diagnostico) con al menos una Evidence en estado Disponible, dividido entre el total de obligaciones aplicables | Verde si 100% de las OBLIGATORIO tienen evidencia Disponible; amarillo si falta evidencia de al menos una RECOMENDADO o CONDICIONAL; rojo si falta evidencia de al menos una OBLIGATORIO | Gerencia: solo el semaforo, con el texto "evidencia disponible", nunca "cumplimiento". Legal/Delegado y Auditor: el detalle completo por obligacion |
| Huecos de evidencia abiertos | Cuenta de Evidence en estado Faltante, por clasificacion (OBLIGATORIO, RECOMENDADO, CONDICIONAL) | Rojo si hay al menos un hueco de una obligacion OBLIGATORIO | Legal/Delegado, Gerencia (solo el total), Auditor |
| Evidencia vencida o por vencer | Cuenta de Evidence en estado Vencida, mas las que vencen en los proximos 30 dias | Rojo si hay al menos una Vencida; amarillo si hay alguna por vencer en 30 dias | Resp. Seguridad/IT (para su evidencia tecnica), Legal/Delegado, Gerencia |
| Paquetes de evidencia generados en el periodo | Cuenta de EvidencePackage en estado Exportado, por tipo de paquete | Sin semaforo (indicador informativo) | Legal/Delegado, Auditor, Gerencia |
| Tiempo promedio de aprobacion de evidencia manual | Promedio de dias entre En revision y Disponible, sobre las Evidence con Origen = Manual | Verde menor a 5 dias habiles, amarillo 5 a 10, rojo mayor a 10 [opinion de producto, sin respaldo legal] | Legal/Delegado, Administrador |

Ningun indicador de este modulo se expresa como "porcentaje de cumplimiento legal"; el lenguaje siempre es "evidencia disponible", "huecos abiertos" o "evidencia vencida", junto con el banner de descargo estandar del sistema (`04_objetivo_exacto_del_producto.md`, seccion 1.3): "Controles configurados: X%. Tareas pendientes: Y. Este indicador mide el estado de su programa, no equivale a una declaracion de cumplimiento legal."

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Informe de brecha de evidencia | Obligaciones aplicables sin evidencia Disponible, con clasificacion y modulo sugerido | Por clasificacion, por area, por modulo | XLSX, PDF | Delegado/Resp. interno, Gerencia | No es en si mismo parte del paquete, pero orienta que falta antes de generarlo |
| Paquete de evidencia general | Evidencia y Documentos por los filtros elegidos, con manifiesto y verificacion de integridad | Por periodo, por obligacion, por modulo de origen | ZIP con manifiesto, o PDF/XLSX/CSV segun el tipo de paquete | Auditor interno o externo, ACE, cliente en due diligence | Si (es el paquete de evidencia en si) |
| Paquete para auditoria anual (MOD-018) | Evidencia del alcance de la auditoria en curso, mas el checklist de MOD-015 y MOD-006 relacionado | Por auditoria especifica | ZIP con hash o firma | Auditor (interno o externo invitado) | Si |
| Paquete para procedimiento sancionador (MOD-024) | Evidencia relacionada con la obligacion o el hecho investigado, incluida la evidencia bloqueada por el propio expediente | Por expediente sancionador especifico | ZIP con hash o firma | Responsable Legal/Compliance, Delegado/Resp. interno | Si |
| Paquete de preparacion de inspeccion | Evidencia completa por obligacion OBLIGATORIO, generado bajo demanda ante un aviso de diligencia preliminar | Por las 105 obligaciones, priorizando OBLIGATORIO | ZIP con manifiesto | Delegado/Resp. interno, Gerencia | Si |
| Historico de exportaciones | Lista de todos los EvidencePackage exportados, con fecha, tipo, destinatario declarado y aprobadores | Rango de fechas, por tipo de paquete | CSV | Auditor interno, Gerencia | Si |

---

## O. Historial

Eventos que quedan en el historial del modulo y en la auditoria transversal (AuditLog):

- Deteccion de un hueco de evidencia (obligacion aplicable sin registro), con la obligacion y la fecha en que se detecto.
- Carga de evidencia manual, con usuario, fecha y modulo o area de la que proviene.
- Llegada automatica de evidencia desde un modulo estructurado, con referencia al registro de origen.
- Cambios de estado de cada Evidence (En revision, Disponible, Vencida, Rechazada, Archivada), con quien lo ejecuto y cuando.
- Aprobaciones y rechazos de evidencia manual, con identidad y motivo cuando aplica.
- Renovaciones de evidencia con fecha de vigencia, con la version anterior conservada y enlazada.
- Activacion y liberacion del campo Bloqueada, con referencia al expediente (procedimiento sancionador o reclamo) que la origino.
- Generacion, aprobacion, segundo control y exportacion de cada EvidencePackage, con usuario, fecha y destinatario declarado.
- Accesos de lectura a evidencia con nivel de sensibilidad "Datos personales sensibles" o "Informacion tecnica de seguridad sensible", con quien la consulto y cuando.
- Cambios de la bandera `regimen_reforma_659` que MOD-024 activa, registrados como contexto historico sobre la evidencia existente, sin alterarla.

---

## P. Riesgos

- **Riesgo legal:** que se interprete "evidencia disponible" como sinonimo de "cumplimiento legal confirmado". Mitigacion de diseno: ningun texto del modulo usa la palabra "cumplimiento" salvo para explicar, en la ayuda contextual, la diferencia entre ambos conceptos; todo indicador y todo paquete lleva el banner de descargo estandar (`04_objetivo_exacto_del_producto.md`, seccion 1.3).
- **Riesgo legal:** que un paquete de evidencia exportado sin el segundo control llegue a la ACE o a un tercero con contenido que la organizacion no reviso a tiempo. Mitigacion de diseno: el segundo control para destinos externos es obligatorio y no configurable, sin excepcion de pyme (seccion H).
- **Riesgo de UX:** que la vista "que evidencia tenemos de esta obligacion" abrume al usuario no especialista con las 105 obligaciones a la vez. Mitigacion de diseno: la vista se filtra por defecto a las obligaciones que el diagnostico de MOD-004 confirmo como aplicables a esa empresa, y prioriza siempre OBLIGATORIO antes que RECOMENDADO o CONDICIONAL.
- **Riesgo operativo:** que la evidencia con fecha de vigencia (por ejemplo, un pentest anual) venza sin que nadie lo note, dejando un control de seguridad sin respaldo probatorio. Mitigacion de diseno: las alertas escalonadas de la seccion I, sobre el mismo motor de plazos compartido (MOD-023) que usa el resto del sistema.
- **Riesgo operativo:** que la evidencia "suelta" cargada manualmente (mientras un modulo SHOULD HAVE como MOD-010 no existe todavia) se pierda o quede huerfana cuando ese modulo se active mas adelante. Mitigacion de diseno: el campo "Origen del registro" y "Entidad de origen" quedan preparados para reasignarse a la entidad estructurada del modulo nuevo sin perder el historial ya cargado, mismo patron que ya usan MOD-009 y MOD-010 en su propia seccion L.
- **Riesgo de seguridad y privacidad:** que un archivo de evidencia contenga, sin necesidad real, datos personales sensibles de titulares (por ejemplo, un adjunto de un expediente ARCO-POL con mas informacion de la estrictamente necesaria) o informacion tecnica de seguridad delicada (un reporte de pentest). Mitigacion de diseno: control de acceso por nivel de sensibilidad, guia de minimizacion visible al cargar evidencia manual, y prohibicion explicita de importar bases de datos completas del cliente (seccion D.2, anti-features 1, 8 y 9).
- **Riesgo de separacion de funciones en pyme:** que la misma persona cargue, apruebe y exporte una evidencia o un paquete, sin ningun segundo control real. Mitigacion de diseno: advertencia visible de autorrevision en cada aprobacion interna hecha por el mismo usuario que cargo la evidencia (siguiendo `05_tipos_de_usuario.md`, seccion 5.4), y segundo control obligatorio sin excepcion para toda exportacion externa (seccion C).
- **Riesgo probatorio:** que una evidencia bloqueada por un procedimiento sancionador abierto se archive o se pierda por error antes de que el caso se resuelva. Mitigacion de diseno: el campo Bloqueada impide archivar o reemplazar mientras el expediente relacionado siga abierto, sin excepcion manual (seccion H).

---

## Q. MVP

**Cobertura parcial ya disponible antes de que este modulo exista como tal.** Antes de que la vista consolidada de MOD-019 este disponible, cada modulo MUST HAVE (MOD-007, MOD-008, MOD-009, MOD-011, MOD-013, MOD-015, MOD-017) ya conserva su propia evidencia en su propia seccion J, con hash y trazabilidad, segun documenta cada ficha individual; lo que MOD-019 agrega es la vista consolidada por obligacion, el informe de huecos y el mecanismo unico de paquete exportable con verificacion de integridad.

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Vista "que evidencia tenemos de esta obligacion" por las 105 obligaciones, con estados Faltante/En revision/Disponible/Vencida/Rechazada | X | | | | Es la tercera condicion del test de tres condiciones del mapa definitivo (capacidad probatoria desde el primer dia); sin esto ningun modulo puede demostrar responsabilidad demostrada de forma consolidada |
| Recepcion automatica de evidencia por referencia desde MOD-007 a MOD-018 (segun cada modulo se active) | X | | | | Nucleo de la separacion Documento/Evidencia/AuditLog (decision 2.7.4); sin esto la vista consolidada no tiene datos que mostrar |
| Informe de huecos de evidencia, priorizado por clasificacion OBLIGATORIO | X | | | | Bajo costo, alto valor: convierte el diagnostico de MOD-004 en una lista accionable de que evidencia falta |
| Carga manual de evidencia suelta con aprobacion (para cubrir modulos SHOULD HAVE aun no activos) | X | | | | Necesario desde el primer dia porque MOD-010, MOD-012, MOD-014, MOD-016 y MOD-018 son SHOULD HAVE; sin esto esas obligaciones quedarian sin ninguna forma de registrar evidencia mientras tanto |
| EvidencePackage con manifiesto y verificacion de integridad, destino interno | X | | | | Cierra el anti-feature 25: sin esto ningun paquete exportado del sistema es verificable |
| Doble control obligatorio para exportacion con destino externo | X | | | | Mismo nivel de urgencia que el mecanismo de integridad: un envio externo sin segundo control anula el valor probatorio del paquete |
| Alertas de evidencia vencida o por renovar (por ejemplo, pentest anual) | X | | | | Sin esto, un control critico de seguridad puede quedar sin evidencia vigente sin que nadie lo note |
| Bloqueo de evidencia vinculada a un procedimiento o reclamo abierto | X | | | | Depende de que MOD-011 (OBL-ARCO-14) y MOD-024 (procedimiento sancionador) existan como referencia; ambos MUST HAVE el nucleo necesario desde el MVP |
| Paquetes especializados por tipo (auditoria MOD-018, procedimiento sancionador MOD-024, due diligence, preparacion de inspeccion) con contenido sugerido automatico | | X | | | El mecanismo generico de EvidencePackage ya cubre estos casos con filtros manuales; la sugerencia automatica de contenido por tipo es una mejora de UX, no un requisito para que el paquete exista |
| Indicadores de dashboard (evidencia disponible, huecos, vencimientos) integrados en MOD-020 | X | | | | Bajo costo de implementacion una vez que existe el resto del modulo; MOD-020 es MUST HAVE y depende de estos datos |
| Tiempo promedio de aprobacion de evidencia como indicador de dashboard | | | X | | Metrica de mejora continua, sin urgencia regulatoria ni dependencia de otro modulo MUST HAVE |

**Version minima vendible del modulo:** la vista consolidada de evidencia por obligacion (con sus cinco estados), la recepcion automatica de evidencia desde los modulos ya activos, el informe de huecos priorizado, la carga manual con aprobacion para las obligaciones cuyo modulo estructurado aun no existe, y el EvidencePackage con manifiesto, verificacion de integridad y doble control para destinos externos. Esto ya permite a una empresa, desde su primer dia de uso del sistema, responder con evidencia verificable la pregunta que motiva todo el modulo: que evidencia tenemos de esta obligacion. Los paquetes especializados por tipo y las metricas de eficiencia interna pueden iterar despues sin bloquear ese nucleo.

---

## R. Ayuda contextual (complemento obligatorio)

**1. Que es la "evidencia" y en que se diferencia de un "documento"**
- Que es: un documento (por ejemplo, un aviso de privacidad o un contrato) es el contenido en si, versionado, que administra el modulo de Documentos y Politicas. La evidencia es la prueba de que algo ocurrio con ese documento o con cualquier otro proceso: que se publico, que alguien lo aprobo, que un titular lo acepto, en que fecha y por quien.
- Por que tengo que hacer esto: si solo guarda el documento pero no la prueba de lo que paso con el, no puede demostrar despues, por ejemplo, que version del aviso vio realmente un titular cuando dio su consentimiento.
- Fundamento: OBL-PRIN-03 (Art. 5 lit. i LPDP, responsabilidad demostrada); OBL-CONS-05 (Art. 54, carga de la prueba del consentimiento y del aviso).
- Cuando necesito ayuda juridica: si necesita decidir que tan detallada debe ser una evidencia especifica para un caso en disputa, consulte con su asesor legal.

**2. Que es el registro tecnico (AuditLog) y por que no es lo mismo que la evidencia de este modulo**
- Que es: el AuditLog es un registro automatico de quien hizo que y cuando en cualquier parte del sistema, que existe desde el primer dia sin que nadie lo active. La evidencia de este modulo es distinta: son las pruebas concretas (documentos, aprobaciones, registros) que respaldan cada obligacion especifica.
- Por que tengo que hacer esto: el AuditLog por si solo no le dice si tiene evidencia de una obligacion de la ley; solo deja constancia tecnica de acciones. El Centro de Evidencias si organiza esa informacion por obligacion, para que usted pueda responder directamente "que evidencia tengo de esto".
- Fundamento: OBL-PRIN-03 (Art. 5 lit. i LPDP) para ambos conceptos, aplicados de forma distinta.
- Cuando necesito ayuda juridica: no aplica; es una aclaracion sobre que hace cada parte del sistema.

**3. Que es un "hueco de evidencia" y que debo hacer cuando aparece uno**
- Que es: un hueco de evidencia es una obligacion que la ley le exige (segun su propio diagnostico) para la cual todavia no hay ningun registro, archivo ni aprobacion guardada en el sistema.
- Por que tengo que hacer esto: un hueco en una obligacion OBLIGATORIO es el mayor riesgo del programa: significa que, si la ACE preguntara hoy, la empresa no tendria nada que mostrar sobre esa obligacion especifica.
- Fundamento: OBL-PRIN-03 (Art. 5 lit. i LPDP); la clasificacion OBLIGATORIO/RECOMENDADO/CONDICIONAL de cada obligacion viene de `matriz_obligaciones.json`.
- Cuando necesito ayuda juridica: si no esta seguro de que tipo de evidencia serviria para cerrar un hueco especifico, consulte con su asesor legal o revise la ayuda contextual del modulo que deberia generar esa evidencia.

**4. Que es un "paquete de evidencia" (EvidencePackage) y por que no puedo editarlo despues de exportado**
- Que es: un paquete de evidencia es una seleccion de evidencia y documentos, empaquetados juntos con un mecanismo que permite comprobar despues que nada fue alterado (un "manifiesto" con la huella de cada archivo).
- Por que tengo que hacer esto: si alguien pudiera editar un paquete despues de exportado, perderia todo su valor como prueba; por eso cualquier cambio de contenido exige generar un paquete nuevo, nunca modificar uno ya exportado.
- Fundamento: Anti-feature 25 (todo paquete de evidencias exportado debe permitir verificar despues que no fue alterado); decision de alcance 2.7.24.
- Cuando necesito ayuda juridica: si el paquete va dirigido a la ACE o forma parte de un procedimiento sancionador, consulte con su asesor legal sobre que contenido incluir antes de aprobarlo.

**5. Por que un envio a la ACE, a un auditor externo o a un cliente exige un segundo control**
- Que es: el segundo control es la aprobacion de una segunda persona, distinta de quien preparo el paquete, antes de que un paquete de evidencia pueda salir de la organizacion hacia un destinatario externo.
- Por que tengo que hacer esto: una vez que un paquete sale de la organizacion, ya no se puede corregir ni retirar; el segundo control es la ultima oportunidad de revisar que el contenido sea el correcto antes de que eso ocurra.
- Fundamento: [opinion de producto, buena practica de seguridad y control interno, alineada con la exigencia general de separacion de funciones de `05_tipos_de_usuario.md`, seccion 5.4].
- Cuando necesito ayuda juridica: si el destinatario es la ACE en el marco de un procedimiento sancionador o una diligencia preliminar, consulte con su asesor legal antes de aprobar el envio.

**6. Que significa que una evidencia este "bloqueada"**
- Que es: una evidencia bloqueada es aquella que esta vinculada a un caso todavia abierto (un procedimiento sancionador o un reclamo de un titular ante la Direccion de Proteccion de Datos), por lo que el sistema no permite archivarla ni reemplazarla mientras ese caso siga abierto.
- Por que tengo que hacer esto: si esa evidencia se archivara o se reemplazara antes de que el caso se resuelva, la empresa podria perder justo la prueba que necesita para defenderse.
- Fundamento: OBL-RET-05 (retencion del expediente ARCO-POL e incidentes como prueba de descargo); OBL-SANC-07 (prescripcion de infracciones y sanciones a 5 anos).
- Cuando necesito ayuda juridica: si no esta seguro de si un caso relacionado sigue abierto o ya se cerro, consulte con su asesor legal antes de intentar archivar la evidencia vinculada.

---

## Nota final del agente (desacuerdos y observaciones sobre las fuentes de diseno)

**Sobre el mapa definitivo.** No se detecto ningun error en las decisiones ya tomadas para MOD-019 en `06_mapa_definitivo_de_modulos.md` ni en `mapa_modulos.json`. Las seis obligaciones asignadas (una propietaria, cinco colaboradoras) coinciden exactamente con la tabla de cobertura de la seccion 8 de ese documento (lineas de OBL-PRIN-03, OBL-CONS-05, OBL-TRANSF-06, OBL-INC-04, OBL-SANC-07 y OBL-RET-05), la lista de doce modulos en `depende_de` coincide con la seccion D.0 de esta ficha, y la relacion reciproca con MOD-018 esta documentada de forma consistente tanto en `notas_dependencia` del JSON como en la seccion 6.1 del mapa y en la propia ficha de MOD-018 (seccion L), sin que esta ficha necesite anadir ninguna precision adicional a esa excepcion ya explicada. La clasificacion MUST HAVE se mantiene sin cambios.

**Expectativas de otras fichas encontradas y como se resolvieron.** El `grep -n "MOD-019" analisis/03_modulos/*.md` sobre las 18 fichas ya redactadas (MOD-001 a MOD-018, MOD-021) muestra un vocabulario y unas expectativas consistentes entre si, que esta ficha adopta literalmente en vez de introducir terminologia nueva:
1. Todas esas fichas describen a MOD-019 como el destino de su propia evidencia "por referencia", nunca como quien la genera o la copia; esta ficha lo modela exactamente asi en la seccion D.0 (columna "Forma": registro, archivo, aprobacion o log, nunca una cuarta copia del dato).
2. Varias fichas (MOD-002, MOD-007, MOD-008, MOD-010, MOD-011, MOD-014, MOD-015, MOD-016, MOD-021) dan por hecho que "todo paquete de evidencia exportado incluye un mecanismo propio de verificacion de integridad (hash o firma)" conforme a la decision 2.7.24 y el anti-feature 25; esta ficha satisface esa expectativa con el manifiesto y la firma del EvidencePackage (secciones D.2 y F.2), y precisa ademas que el hash de cada archivo individual normalmente ya lo calculo el modulo de origen al capturarlo (por ejemplo, MOD-007 o MOD-013), mientras que MOD-019 anade la firma o huella del manifiesto y del paquete completo al momento de exportar.
3. MOD-021 (seccion J) da por hecho que MOD-019 "define el mecanismo de integridad para todo el sistema"; esta ficha lo recoge explicitamente en la seccion D.1 (campo "Huella de integridad") y D.2 (campos "Manifiesto" y "Firma o huella del paquete completo"), sin contradecir que cada modulo de origen siga calculando su propio hash al capturar el archivo.
4. Varias fichas (MOD-009, MOD-010) describen el patron de "tarea manual en MOD-021 con evidencia suelta en MOD-019" para cuando un modulo SHOULD HAVE (MOD-010) todavia no esta disponible; esta ficha lo satisface con el campo "Origen del registro" (Automatico / Manual) de la seccion D.1 y lo desarrolla en la seccion L ("que ocurre si un modulo dependiente no existe en el MVP"), generalizando el mismo patron a los cinco modulos SHOULD HAVE que alimentan a MOD-019 (MOD-010, MOD-012, MOD-014, MOD-016, MOD-018).
5. MOD-016 (seccion J) senala que "toda esta evidencia se expone tambien, de forma consolidada, en el Centro de Evidencias"; esta ficha construye esa consolidacion en la seccion D.0 a partir precisamente de la seccion J de MOD-016 y de las otras 17 fichas existentes, mas la ficha resumida de los modulos sin ficha propia.
6. Ninguna ficha existente contradice o pide de MOD-019 algo que esta ficha no pueda satisfacer con el diseno de las secciones D a J; no fue necesario resolver ninguna expectativa incorrecta o contradictoria.

**Precision propia de esta ficha, no presente de forma explicita en el mapa ni en las fichas ya redactadas.** El mapa definitivo y las fichas existentes documentan con detalle el mecanismo de integridad por archivo y por paquete, pero ninguna fuente leida fija de forma expresa un mecanismo de "doble control obligatorio y no configurable" para toda exportacion con destinatario externo a la organizacion, mas alla de la separacion de funciones general de `05_tipos_de_usuario.md` seccion 5.4. Esta ficha lo introduce como diseno propio (seccion C, F.2 y H) porque el enfoque especifico de la tarea lo exige explicitamente ("doble control para envios externos") y porque es coherente con el resto del sistema: se marca en la seccion R, concepto 5, como "[opinion de producto]" en su fundamento, no como una exigencia legal expresa, y no contradice ninguna decision de alcance ya tomada en `02_validacion_de_la_idea.md`.
