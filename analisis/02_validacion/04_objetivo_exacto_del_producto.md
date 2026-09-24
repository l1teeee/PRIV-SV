# 4. Objetivo exacto del producto

Fecha: 2026-09-24. Fase: analisis funcional (sin codigo, sin stack, sin base de datos).

Fuentes base: `00_contexto_para_agentes.md`, `00_prompt_analisis_funcional.md`, `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` (hipotesis de producto), `01_legal\matriz_obligaciones.md` / `matriz_obligaciones.json` (105 obligaciones, IDs canonicos OBL-AREA-NN) y `01_legal\03_hallazgos_regulatorios.md`. Alineado con las decisiones de alcance de `02_validacion_de_la_idea.md`, seccion 2.7.

Nota de alcance: donde una afirmacion es decision u opinion de producto (no exigencia legal expresa), se marca explicitamente "[opinion de producto]". Donde una afirmacion es juridica, se cita el OBL-ID canonico y el articulo.

---

## 1.1 Definicion en una pagina

**Que es.** Una plataforma SaaS B2B de autogestion de proteccion de datos personales, hecha para empresas de El Salvador sujetas a la Ley para la Proteccion de Datos Personales (Decreto Legislativo 144, vigente desde el 23 de noviembre de 2024). El sistema convierte las obligaciones de esa ley, sus politicas de actuacion y sus lineamientos en procesos, responsables, tareas, plazos, controles, documentos y evidencia, para que la empresa pueda gestionarlos con su propio personal.

**Para quien.** Para empresas privadas salvadorenas obligadas por la LPDP que no cuentan con un departamento de privacidad dedicado: desde una pyme de alrededor de 30 empleados hasta un grupo corporativo con varias sociedades. El usuario objetivo tipico no es abogado ni especialista en proteccion de datos; es una persona con otro cargo (administracion, RRHH, TI, cumplimiento) a quien la empresa le asigna esta responsabilidad ademas de su trabajo habitual.

**Que hace.** El sistema:
- Traduce el diagnostico de la empresa en la lista de obligaciones que le aplican, citando el OBL-ID y el articulo correspondiente.
- Genera un plan de trabajo con tareas, responsables y fechas.
- Calcula y vigila los plazos legales (por ejemplo, 20 mas 20 dias habiles del Art. 20 para ARCO-POL, OBL-ARCO-10; 72 horas del Art. 25 para vulneraciones, OBL-INC-01; 10 dias habiles de prevencion unica del Art. 18, OBL-ARCO-08) mediante un motor de plazos habiles compartido por todos los modulos con plazo legal.
- Organiza el Registro de Actividades de Tratamiento (RAT), el manejo de solicitudes ARCO-POL, la gestion de incidentes, proveedores, riesgos, documentos y controles de seguridad, incluyendo el ciclo de vida completo del Delegado de Proteccion de Datos y del procedimiento sancionador mientras estos aplican.
- Conserva evidencia y trazabilidad de lo realizado (quien hizo que, cuando, con que fundamento), con integridad verificable en todo paquete de evidencia que sale del sistema.
- Se adapta a los dos estados normativos vigentes en El Salvador en este momento (ver 1.1.1).

**Que no hace.** No sustituye asesoria juridica, no actua como Delegado de Proteccion de Datos, abogado, auditor externo o responsable del tratamiento de la empresa cliente, no toma decisiones legales por la empresa, no garantiza cumplimiento, no opera como CRM ni como SIEM, y no centraliza innecesariamente los datos personales de los titulares del cliente (ver `22_anti_features.md`).

### 1.1.1 Alineacion con el doble estado de la reforma 659

El Decreto Legislativo 659, que segun fuentes secundarias derogaria los Arts. 15 y 17 (delegado obligatorio en el sector privado) y reformaria los Arts. 16, 47 y 51, fue aprobado el 17-sep-2026 pero, a la fecha de este documento, su publicacion en el Diario Oficial no esta confirmada (OBL-PLAZO-05). El numero de decreto mismo tiene fuentes contradictorias (659 y 660) y debe citarse siempre como "segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado".

El producto modela dos configuraciones activables por fecha de vigencia real, nunca por fecha de aprobacion legislativa:
- **Estado ACTUAL (vigente hoy):** Delegado de Proteccion de Datos obligatorio en el sector privado (OBL-DPO-01, Arts. 15 y 17), con las funciones de recepcion, prevencion, resolucion y notificacion ARCO-POL centralizadas en esa figura.
- **Estado FUTURO (solo si se confirma la publicacion oficial y transcurre la vacatio legis de 8 dias):** Delegado no obligatorio para el sector privado; esas funciones pasan a un rol interno configurable ("sujeto obligado" / responsable interno del tramite), sin necesidad de certificacion ACE.

El cambio de estado ACTUAL a FUTURO no es automatico: requiere una bandera de configuracion que el equipo del producto active manualmente al confirmar la publicacion, y el sistema registra la fecha de ese cambio para trazabilidad historica de cada expediente. Este mecanismo de doble estado se documenta como el primer caso de uso concreto del motor regulatorio del producto (motor "Core Privacy Engine" mas "Regulatory Pack" por jurisdiccion), y cubre las 17 obligaciones de la matriz marcadas como afectadas por la reforma.

### 1.2 El sistema puede / el sistema no debe afirmar

**El sistema puede:**
- Explicar en lenguaje simple que obligacion aplica y por que, citando el OBL-ID y el articulo (por ejemplo: "Su empresa trata datos biometricos, OBL-SENS-06, Art. 4 lit. g; esto requiere consentimiento por escrito y una alternativa no biometrica, OBL-SENS-07, Art. 26 inc. 4 y Art. 37").
- Guiar mediante un diagnostico de cumplimiento repetible y un wizard de onboarding, separados como dos pasos distintos.
- Calcular y recordar plazos legales, mostrando el criterio de computo usado (dias habiles, horas corridas u horas habiles) cuando la ley sea ambigua, con una nota visible de esa ambiguedad.
- Registrar, documentar, versionar y conservar evidencia (RAT, incidentes, consentimientos, controles, aprobaciones), con Documento, Evidencia y AuditLog como entidades distintas y relacionadas.
- Generar borradores de documentos (avisos, politicas, contratos, respuestas ARCO-POL) siempre marcados como borrador pendiente de revision.
- Organizar tareas, responsables, dependencias y flujos de aprobacion interna configurables por tipo de documento o de decision.
- Mostrar el estado del programa (madurez, controles configurados, tareas pendientes, evidencia disponible), nunca un porcentaje de "cumplimiento legal".
- Senalar explicitamente cuando una decision requiere criterio juridico o aprobacion interna, y detener ahi la automatizacion; en particular, todo acto legalmente atribuido al Delegado (prevencion, incompetencia, notificacion a receptores, revocacion) queda calculado y redactado por el sistema pero pendiente de aprobacion explicita de esa persona antes de emitirse.

**El sistema no debe afirmar automaticamente:**
- Que la empresa esta legal o parcialmente "en cumplimiento" de la LPDP.
- Que una base juridica especifica (consentimiento, interes legitimo u otra de las seis del Art. 5 lit. g) es valida para un tratamiento concreto sin revision humana.
- Que una transferencia internacional es legal o que un pais tiene "nivel de proteccion adecuado" bajo el Art. 44: la ley no atribuye esa calificacion a ningun organo y la ACE no ha publicado lista ni criterios.
- Que un documento generado por el sistema (aviso, politica, contrato, respuesta ARCO-POL) es valido sin revision y aprobacion de la organizacion.
- Que actua como el Delegado de Proteccion de Datos, abogado, auditor externo o responsable del tratamiento de la empresa cliente.
- Que una solicitud ARCO-POL fue correctamente resuelta por criterio legal automatico; el sistema aporta la causal tasada y el plazo, la decision la toma el responsable interno.
- Que el computo adoptado para un plazo ambiguo (por ejemplo, las 72 horas del Art. 25: corridas u horas habiles) es la unica interpretacion correcta.
- Que garantiza la seguridad de la informacion de la empresa: no es un SIEM ni un antivirus, solo registra evidencia de que un control existe.
- Que sustituye la certificacion oficial del Delegado ante la ACE (facultad exclusiva de la Direccion de Proteccion de Datos, Art. 12 Lineamientos DPO).

### 1.3 Textos de descargo estandar de la interfaz

[opinion de producto: redaccion propuesta, no un formato exigido por la ACE]

- **Banner general (visible en todo momento o en el dashboard principal):** "Este sistema organiza, documenta y da seguimiento a su programa de proteccion de datos. No constituye asesoria legal ni garantiza el cumplimiento de la Ley para la Proteccion de Datos Personales (Decreto Legislativo 144)."
- **Al generar cualquier documento (aviso, politica, contrato, respuesta):** "Documento generado como borrador a partir de la informacion registrada. Requiere revision y aprobacion de su organizacion antes de usarse, y puede requerir validacion de asesoria legal especializada."
- **Al mostrar un resultado de riesgo o de una Evaluacion de Impacto (EIPD):** "Este resultado es un calculo de apoyo interno basado en los factores que usted registro. No es una conclusion juridica sobre la legalidad del tratamiento."
- **En el dashboard, junto a cualquier metrica de avance:** "Controles configurados: X%. Tareas pendientes: Y. Este indicador mide el estado de su programa, no equivale a una declaracion de cumplimiento legal."
- **Al elegir una base juridica distinta del consentimiento para un tratamiento:** "La eleccion de esta base requiere el criterio de su organizacion sobre si es defendible para este tratamiento especifico. En caso de duda, consulte asesoria legal."
- **Al calcular un plazo con criterio ambiguo (por ejemplo, las 72 horas de notificacion de incidentes):** "La ley no precisa si este plazo se cuenta en horas corridas u horas habiles. El sistema aplica por defecto el criterio mas conservador (horas corridas). Verifique este criterio con asesoria legal si el caso es critico."
- **Al activar o mostrar el estado de la reforma 659:** "El Decreto Legislativo 659 (numero pendiente de confirmar contra el texto oficial) fue aprobado por la Asamblea Legislativa pero, a la fecha, no esta confirmada su publicacion en el Diario Oficial. Mientras tanto, aplica el regimen vigente del Delegado de Proteccion de Datos (Arts. 15 y 17 del Decreto 144)."
- **Al cerrar o denegar una solicitud ARCO-POL:** "La resolucion de esta solicitud es responsabilidad de su organizacion. El sistema registro el fundamento y el plazo aplicable; la decision final y su motivacion deben ser revisadas por la persona responsable antes de notificarse al titular."

### Como se mide el exito [opinion de producto, no existe metrica legal de "exito"]

- Cobertura del diagnostico: porcentaje de obligaciones aplicables (segun el diagnostico de esa empresa) con al menos una tarea asignada y en curso.
- Cumplimiento de plazos operativos: porcentaje de solicitudes ARCO-POL resueltas dentro del plazo legal aplicable, y de incidentes documentados dentro de las 72 horas desde su conocimiento (OBL-INC-01).
- Cobertura del RAT: porcentaje de tratamientos identificados en el diagnostico con ficha de Registro de Actividades de Tratamiento completa (OBL-DOC-02).
- Evidencia disponible: porcentaje de obligaciones clasificadas OBLIGATORIO en la matriz con evidencia adjunta verificable.
- Adopcion real: porcentaje de usuarios designados que completan el onboarding y mantienen tareas al dia (no vencidas).
- Retencion comercial: renovacion de la suscripcion y uso sostenido tras el primer diagnostico (senal de que el producto resuelve un problema real y no solo se usa una vez).

El sistema nunca debe expresar estas metricas como "cumplimiento legal", sino como estado del programa, madurez y evidencia disponible.
