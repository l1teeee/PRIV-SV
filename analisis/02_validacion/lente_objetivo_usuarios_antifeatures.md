# Lente: objetivo exacto del producto, tipos de usuario y anti-features

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (sin codigo, sin stack, sin base de datos).
Fuentes base: `00_contexto_para_agentes.md`, `00_prompt_analisis_funcional.md`, `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` (hipotesis de producto), `01_legal/matriz_obligaciones.md` / `matriz_obligaciones.json` (105 obligaciones, IDs canonicos OBL-AREA-NN) y `01_legal/03_hallazgos_regulatorios.md` (secciones 3, 5, 6, 8 y 9).

Nota de alcance: donde una afirmacion es una decision u opinion de producto (no una exigencia legal expresa), se marca explicitamente como "[opinion de producto]". Donde una afirmacion es juridica, se cita el OBL-ID canonico de la matriz y el articulo.

---

## 1. Objetivo exacto del producto

### 1.1 Definicion en una pagina

**Que es.** Una plataforma SaaS B2B de autogestion de proteccion de datos personales, hecha para empresas de El Salvador sujetas a la Ley para la Proteccion de Datos Personales (Decreto Legislativo 144, vigente desde el 23 de noviembre de 2024). El sistema convierte las obligaciones de esa ley, sus politicas de actuacion y sus lineamientos en procesos, responsables, tareas, plazos, controles, documentos y evidencia, para que la empresa pueda gestionarlos con su propio personal.

**Para quien.** Para empresas privadas salvadorenas obligadas por la LPDP que no cuentan con un departamento de privacidad dedicado: desde una pyme de alrededor de 30 empleados hasta un grupo corporativo con varias sociedades. El usuario objetivo tipico no es abogado ni especialista en proteccion de datos; es una persona con otro cargo (administracion, RRHH, TI, cumplimiento) a quien la empresa le asigna esta responsabilidad ademas de su trabajo habitual.

**Que hace.** El sistema:
- Traduce el diagnostico de la empresa en la lista de obligaciones que le aplican, citando el OBL-ID y el articulo correspondiente.
- Genera un plan de trabajo con tareas, responsables y fechas.
- Calcula y vigila los plazos legales (por ejemplo, 20 mas 20 dias habiles del Art. 20 para ARCO-POL, OBL-ARCO-10; 72 horas del Art. 25 para vulneraciones, OBL-INC-01; 10 dias habiles de prevencion unica del Art. 18, OBL-ARCO-08).
- Organiza el Registro de Actividades de Tratamiento, el manejo de solicitudes ARCO-POL, la gestion de incidentes, proveedores, riesgos, documentos y controles de seguridad.
- Conserva evidencia y trazabilidad de lo realizado (quien hizo que, cuando, con que fundamento).
- Se adapta a los dos estados normativos vigentes en El Salvador en este momento (ver 1.1.1).

**Que no hace.** No sustituye asesoria juridica, no actua como Delegado de Proteccion de Datos, abogado, auditor externo o responsable del tratamiento de la empresa cliente, no toma decisiones legales por la empresa, no garantiza cumplimiento, no opera como CRM ni como SIEM, y no centraliza innecesariamente los datos personales de los titulares del cliente (ver seccion 3, Anti-features).

**1.1.1 Alineacion con el doble estado de la reforma 659.** El Decreto Legislativo 659, que segun fuentes secundarias derogaria los Arts. 15 y 17 (delegado obligatorio en el sector privado) y reformaria los Arts. 16, 47 y 51, fue aprobado el 17-sep-2026 pero, a la fecha de este documento, su publicacion en el Diario Oficial no esta confirmada (OBL-PLAZO-05; `03_hallazgos_regulatorios.md` seccion 3). El producto debe modelar dos configuraciones activables por fecha de vigencia real, nunca por fecha de aprobacion legislativa:
- **Estado ACTUAL (vigente hoy):** delegado de proteccion de datos obligatorio en el sector privado (OBL-DPO-01, Arts. 15 y 17), con las funciones de recepcion, prevencion, resolucion y notificacion ARCO-POL centralizadas en esa figura.
- **Estado FUTURO (solo si se confirma la publicacion oficial y transcurre la vacatio legis de 8 dias):** delegado no obligatorio para el sector privado; esas funciones pasan a un rol interno configurable ("sujeto obligado" / responsable interno del tramite), sin necesidad de certificacion ACE.
El cambio de estado ACTUAL a FUTURO no debe ser automatico: requiere una bandera de configuracion que el equipo del producto active manualmente al confirmar la publicacion, y el sistema debe registrar la fecha de ese cambio para trazabilidad historica de cada expediente.

**Como se mide el exito** [opinion de producto, no existe metrica legal de "exito"]:
- Cobertura del diagnostico: porcentaje de obligaciones aplicables (segun el diagnostico de esa empresa) con al menos una tarea asignada y en curso.
- Cumplimiento de plazos operativos: porcentaje de solicitudes ARCO-POL resueltas dentro del plazo legal aplicable, y de incidentes documentados dentro de las 72 horas desde su conocimiento (OBL-INC-01).
- Cobertura del RAT: porcentaje de tratamientos identificados en el diagnostico con ficha de Registro de Actividades de Tratamiento completa (OBL-DOC-02).
- Evidencia disponible: porcentaje de obligaciones clasificadas OBLIGATORIO en la matriz con evidencia adjunta verificable.
- Adopcion real: porcentaje de usuarios designados que completan el onboarding y mantienen tareas al dia (no vencidas).
- Retencion comercial: renovacion de la suscripcion y uso sostenido tras el primer diagnostico (senal de que el producto resuelve un problema real y no solo se usa una vez).
El sistema nunca debe expresar estas metricas como "cumplimiento legal", sino como estado del programa, madurez y evidencia disponible (ver 1.2 y 1.3).

### 1.2 El sistema puede / el sistema no debe afirmar

**El sistema puede:**
- Explicar en lenguaje simple que obligacion aplica y por que, citando el OBL-ID y el articulo (por ejemplo: "Su empresa trata datos biometricos (OBL-SENS-06, Art. 4 lit. g); esto requiere consentimiento por escrito y una alternativa no biometrica, OBL-SENS-07, Art. 26 inc. 4 y Art. 37").
- Guiar mediante un diagnostico y un wizard de onboarding.
- Calcular y recordar plazos legales, mostrando el criterio de computo usado (dias habiles, horas corridas u horas habiles) cuando la ley sea ambigua, con una nota visible de esa ambiguedad.
- Registrar, documentar, versionar y conservar evidencia (RAT, incidentes, consentimientos, controles, aprobaciones).
- Generar borradores de documentos (avisos, politicas, contratos, respuestas ARCO-POL) siempre marcados como borrador pendiente de revision.
- Organizar tareas, responsables, dependencias y flujos de aprobacion interna.
- Mostrar el estado del programa (madurez, controles configurados, tareas pendientes, evidencia disponible), nunca un porcentaje de "cumplimiento legal".
- Senalar explicitamente cuando una decision requiere criterio juridico o aprobacion interna, y detener ahi la automatizacion.

**El sistema no debe afirmar automaticamente:**
- Que la empresa esta legal o parcialmente "en cumplimiento" de la LPDP.
- Que una base juridica especifica (consentimiento, interes legitimo u otra de las seis del Art. 5 lit. g) es valida para un tratamiento concreto sin revision humana; la ley no resuelve la tension entre consentimiento como regla general y la pluralidad de bases (`03_hallazgos_regulatorios.md` seccion 8, punto 1).
- Que una transferencia internacional es legal o que un pais tiene "nivel de proteccion adecuado" bajo el Art. 44: la ley no atribuye esa calificacion a ningun organo y la ACE no ha publicado lista ni criterios (incertidumbre 11, seccion 9 hallazgos).
- Que un documento generado por el sistema (aviso, politica, contrato, respuesta ARCO-POL) es valido sin revision y aprobacion de la organizacion.
- Que actua como el Delegado de Proteccion de Datos, abogado, auditor externo o responsable del tratamiento de la empresa cliente.
- Que una solicitud ARCO-POL fue correctamente resuelta por criterio legal automatico; el sistema aporta la causal tasada y el plazo, la decision la toma el responsable interno.
- Que el computo adoptado para un plazo ambiguo (por ejemplo, las 72 horas del Art. 25: corridas u horas habiles, incertidumbre 1, seccion 9 hallazgos) es la unica interpretacion correcta.
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
- **Al activar o mostrar el estado de la reforma 659:** "El Decreto Legislativo 659 fue aprobado por la Asamblea Legislativa pero, a la fecha, no esta confirmada su publicacion en el Diario Oficial. Mientras tanto, aplica el regimen vigente del Delegado de Proteccion de Datos (Arts. 15 y 17 del Decreto 144)."
- **Al cerrar o denegar una solicitud ARCO-POL:** "La resolucion de esta solicitud es responsabilidad de su organizacion. El sistema registro el fundamento y el plazo aplicable; la decision final y su motivacion deben ser revisadas por la persona responsable antes de notificarse al titular."

---

## 2. Tipos de usuario

### 2.1 Personas (perfiles representativos)

Cada perfil incluye: nombre ficticio, cargo real, tipo y tamano de empresa, nivel de conocimiento legal, que necesita del sistema, frecuencia de uso, dispositivos y miedos/objeciones.

#### Pyme (aprox. 30 empleados) - "Ferreteria y Suministros El Roble, S.A. de C.V."

**1. Karla Beatriz Hernandez Mejia - Gerente Administrativa y Financiera**
- Conocimiento legal: bajo-medio. No es abogada; ha leido resumenes de la ley porque le asignaron el tema.
- Rol en el sistema: Administradora de la organizacion y, ademas, Responsable de Privacidad / Delegada interna (acumula roles por ser pyme).
- Necesita: un diagnostico guiado que le diga en lenguaje simple que le aplica, plantillas listas para usar, alertas claras de plazos.
- Frecuencia de uso: 2 a 3 veces por semana; mas intensivo durante el diagnostico inicial.
- Dispositivos: laptop Windows en la oficina, celular Android para notificaciones.
- Miedos y objeciones: teme una multa por desconocimiento y quedar personalmente expuesta al ser la designada; objeta que "esto es cosa de abogados, no mia" y que no tiene tiempo para aprender otra plataforma; el costo mensual le preocupa por el margen ajustado de la pyme.

#### Empresa mediana (aprox. 300 empleados) - "Avicola San Andres, S.A. de C.V."

**2. Jorge Alberto Menendez Rauda - Jefe de Cumplimiento y Riesgo**
- Conocimiento legal: medio-alto; ha llevado cumplimiento de otras normativas (laborales, ambientales), no es abogado litigante.
- Rol en el sistema: Responsable de Privacidad / Delegado interno (en proceso de certificacion ante la ACE bajo el regimen vigente).
- Necesita: un RAT robusto, reportes para la Gerencia y la Junta, trazabilidad completa para la auditoria anual (OBL-AUD-01), coordinacion de plazos ARCO-POL entre varias areas.
- Frecuencia de uso: diaria.
- Dispositivos: laptop corporativa, tablet en reuniones de comite.
- Miedos y objeciones: teme una sancion grave o muy grave por un incidente mal documentado y quedar mal ante la Junta Directiva; pide integraciones con sistemas que ya usa (HRIS, camaras de planta) y le preocupa la curva de aprendizaje de su equipo.

**3. Daniela Patricia Cornejo Lazo - Coordinadora de Recursos Humanos**
- Conocimiento legal: bajo.
- Rol en el sistema: Responsable de area (RRHH); registra el tratamiento de datos biometricos de marcaje y de curriculums recibidos.
- Necesita: saber que debe hacer al implementar un lector biometrico o al recibir CVs (OBL-SENS-06, OBL-SENS-07), plantillas de aviso, tareas simples y accionables.
- Frecuencia de uso: al implementar un proceso nuevo y en consultas puntuales.
- Dispositivos: celular y laptop.
- Miedos y objeciones: teme que su decision de instalar el biometrico genere un problema legal para toda la empresa; objeta que "esto es del area legal, no mia" si el lenguaje del sistema es muy tecnico.

**4. Roberto Antonio Villalta - Gerente de Tecnologia**
- Conocimiento legal: bajo en la ley, alto en seguridad tecnica.
- Rol en el sistema: Responsable de Seguridad / IT; registra controles tecnicos y gestiona incidentes.
- Necesita: catalogo de controles con evidencia, cronometro y checklist para las 72 horas de notificacion de incidentes (OBL-INC-01, OBL-INC-02).
- Frecuencia de uso: constante durante un incidente, mensual en operacion normal.
- Dispositivos: laptop, acceso remoto desde celular durante guardias.
- Miedos y objeciones: teme que un incidente se le escape del plazo de 72 horas sin darse cuenta; no quiere que el sistema le exija instalar software adicional ni acceso amplio a su infraestructura.

#### Corporativo con varias sociedades - "Grupo Financiero Itzalco" (banco, aseguradora y financiera bajo una misma holding)

**5. Licda. Ana Gabriela Reyes Portillo - Directora de Cumplimiento Corporativo**
- Conocimiento legal: alto (abogada interna).
- Rol en el sistema: Responsable Legal / Compliance a nivel de grupo, con visibilidad sobre varias sociedades.
- Necesita: vision consolidada multi-sociedad, comparar el estado entre sociedades, exportar evidencia tanto para la ACE como para el regulador financiero sectorial.
- Frecuencia de uso: diaria o semanal segun la sociedad.
- Dispositivos: laptop, acceso desde la oficina central del grupo.
- Miedos y objeciones: teme que una sociedad del grupo quede desalineada y arrastre riesgo reputacional a todo el grupo; exige separacion estricta de datos entre sociedades y control fino de quien ve que.

**6. Lic. Mauricio Ernesto Aguilar Sandoval - Delegado de Proteccion de Datos certificado ante la ACE (interno, dedicado al banco del grupo)**
- Conocimiento legal: alto, con certificacion del Programa de Certificacion de Delegados de la ACE.
- Rol en el sistema: Responsable de Privacidad / Delegado, dedicado exclusivamente a una sociedad regulada.
- Necesita: gestionar ARCO-POL de esa sociedad, generar el informe periodico al responsable (OBL-DPO-07, minimo dos veces al ano), mantener el enlace con la Direccion de Proteccion de Datos de la ACE (Art. 29 Lineamientos DPO).
- Frecuencia de uso: diaria.
- Dispositivos: laptop, VPN corporativa.
- Miedos y objeciones: le preocupa la incertidumbre de la reforma 659: si se publica, su cargo deja de ser obligatorio y su rol podria diluirse; pide que el sistema distinga claramente lo que hace por obligacion legal de lo que haria de todas formas por buena practica. Vease 2.2 para el efecto detallado de la reforma sobre esta figura.

#### Roles externos (no son personal interno de la empresa cliente)

**7. Sra. Cecilia Marroquin - Titular externo (cliente o ex empleada de una empresa cliente)**
- Conocimiento legal: ninguno o bajo (publico general).
- Rol en el sistema: Titular; usa el Portal del Titular para presentar una solicitud ARCO-POL.
- Necesita: un formulario simple, saber el estado de su solicitud sin tener que crear una cuenta compleja.
- Frecuencia de uso: esporadica, tipicamente una o dos veces.
- Dispositivos: celular, casi siempre.
- Miedos y objeciones: desconfia de entregar su DUI u otros datos de verificacion de identidad en un sitio que no conoce; preferiria llamar o ir en persona.

**8. Ing. Francisco Javier Bonilla - Auditor externo**
- Conocimiento legal: alto en controles y auditoria, no necesariamente abogado.
- Rol en el sistema: Auditor externo (invitado), con acceso temporal de solo lectura al paquete de evidencias de la empresa mediana o corporativa, para la auditoria anual de cumplimiento de las Politicas ACE (OBL-AUD-01).
- Necesita: exportar evidencia en un formato estandar, sin depender de que el cliente le envie archivos sueltos por correo.
- Frecuencia de uso: intensiva durante la semana de la auditoria, nula el resto del ano.
- Dispositivos: laptop propio, acceso temporal por invitacion.
- Miedos y objeciones: necesita garantias de que la evidencia mostrada es integra y no fue editada despues de generada (append-only, trazabilidad verificable).

**9. Lic. Douglas Ivan Quintanilla - Abogado externo ocasional**
- Conocimiento legal: alto.
- Rol en el sistema: Asesor externo invitado, con acceso puntual y acotado a un caso o modulo especifico (por ejemplo, revisar una denegatoria ARCO-POL compleja o dictaminar sobre una base juridica dudosa), no a toda la organizacion.
- Necesita: ver el fundamento normativo que el sistema ya aplico y el expediente completo del caso puntual; dejar su opinion registrada como evidencia.
- Frecuencia de uso: muy baja, por invitacion puntual a un caso concreto.
- Dispositivos: laptop.
- Miedos y objeciones: no quiere opinar sobre un caso sin ver el expediente completo; no quiere una licencia de usuario permanente ni que se le facture como usuario fijo del sistema.

**10. Licda. Silvia Carolina Melendez - Delegada de Proteccion de Datos externa (persona natural contratada por varias empresas, entre ellas la pyme Ferreteria El Roble)**
- Conocimiento legal: alto; atiende a varios clientes al mismo tiempo, cada uno con su propia organizacion en el sistema.
- Rol en el sistema: Responsable de Privacidad / Delegada, en calidad de delegada externa (Art. 13 Lineamientos DPO permite que el delegado externo sea persona natural o juridica).
- Necesita: cambiar entre las organizaciones de sus distintos clientes dentro de una misma cuenta, viendo unicamente los datos del cliente activo en cada momento.
- Frecuencia de uso: variable segun el cliente; algunos dias atiende a varias organizaciones.
- Dispositivos: laptop.
- Miedos y objeciones: la reforma 659, si se publica, eliminaria la base regulatoria de su modelo de negocio como delegada externa obligatoria del sector privado; su servicio tendria que reconvertirse en asesoria voluntaria. Pide que el sistema le permita demostrar a sus clientes que cumplio sus funciones (informes periodicos, Art. 30 Lineamientos DPO) independientemente de si el cargo sigue siendo obligatorio.

**11. Sr. Oscar Rene Handal - Gerente General (perspectiva Gerencia del dashboard)**
- Conocimiento legal: bajo; orientado a negocio y riesgo reputacional y financiero.
- Rol en el sistema: consumidor de la vista de Gerencia del dashboard (no gestiona tareas el mismo).
- Necesita: un resumen ejecutivo simple (semaforos, sin jerga legal), saber si hay algo urgente que decidir.
- Frecuencia de uso: mensual, o inmediata cuando hay una alerta critica (por ejemplo, un incidente en curso).
- Dispositivos: celular para notificaciones, revisa el dashboard en la reunion de comite.
- Miedos y objeciones: teme las multas y el dano reputacional; no quiere aprender el sistema a fondo, solo necesita el resumen.

### 2.2 La figura del Delegado y el efecto de la reforma 659

El Delegado de Proteccion de Datos, bajo el regimen hoy vigente (Arts. 15 y 17 LPDP, Lineamientos para el Delegado de la ACE), puede ser:
- **Interno**, persona natural empleada de la empresa (perfil 2 y 6 arriba).
- **Externo**, persona natural o juridica contratada (Art. 13 Lineamientos DPO; perfil 10 arriba). Cuando el delegado externo es persona juridica, esta debe designar expresamente a una persona natural responsable de atender las funciones (Art. 14 Lineamientos DPO).
- En cualquier caso, debe cumplir requisitos minimos (grado universitario, preferentemente en ciencias juridicas; mayor de 21 anos; experiencia acreditada en materias afines, Art. 5 Lineamientos DPO), someterse al Programa de Certificacion de Delegados de la ACE, y su nombramiento debe comunicarse a la ACE dentro de 15 dias habiles (OBL-DPO-03).

Hoy, el Delegado concentra funciones que el software debe reflejar en un solo rol por defecto: recepcion y resolucion de solicitudes ARCO-POL, prevencion (Art. 18, OBL-ARCO-08), devolucion por incompetencia (Art. 19), notificacion a receptores tras rectificacion o eliminacion (Art. 21, OBL-ARCO-11), tramite de revocacion del consentimiento (Art. 30, OBL-CONS-03), informe periodico al responsable al menos dos veces al ano (OBL-DPO-07), enlace institucional con la Direccion de Proteccion de Datos de la ACE (Art. 29 Lineamientos DPO), y confidencialidad durante 5 anos tras el cese (OBL-DPO-06).

**Si la reforma 659 se publica y entra en vigencia** (estado FUTURO, ver 1.1.1): se derogarian los Arts. 15 y 17, el delegado dejaria de ser obligatorio en el sector privado, y esas funciones pasarian al "sujeto obligado" (la empresa misma), mediante lineamientos internos propios (reforma al Art. 16). Las solicitudes ARCO-POL se presentarian directamente ante la empresa. El sector publico mantendria la figura del delegado (reforma al Art. 47), que podria recaer en el Oficial de Informacion. Segun fuentes secundarias, los plazos (20+20, prevencion de 10 dias, devolucion en 5, notificacion a terceros en 5, revocacion en 5) no cambiarian. Ninguna de estas afirmaciones sobre el contenido articulado de la reforma esta verificada contra el texto oficial del decreto, que no ha sido localizado (OBL-PLAZO-05).

Consecuencia de diseno: el sistema debe modelar un rol "Responsable del tramite ARCO-POL / Responsable de Privacidad" configurable, que hoy se asigna por defecto a quien ocupe el rol Delegado (interno o externo, perfiles 2, 6 y 10), y que el sistema debe permitir reasignar sin friccion el dia que el estado FUTURO se active, sin perder el historial de que version de la regla aplicaba a cada expediente.

### 2.3 Roles estandar del sistema

[opinion de producto para el nombre y alcance exacto de cada rol; el fundamento de la obligatoriedad de la figura Delegado si es legal y esta citado arriba]

| Rol | Proposito | Quien lo suele ocupar | Acumulable en pyme |
|---|---|---|---|
| Administrador de la organizacion | Configura estructura, usuarios, permisos e integraciones; no necesariamente revisa contenido legal en detalle | Dueno o gerente general/administrativo | Si, con casi todos los demas roles |
| Responsable de Privacidad / Delegado (o Responsable interno, si aplica el estado FUTURO) | Concentra hoy las funciones legales del Delegado (ARCO-POL, informes, enlace ACE); en el estado FUTURO coordina la funcion sin investidura legal obligatoria | Persona designada internamente, o Delegado/DPO externo contratado | Si, una sola persona puede ocuparlo junto con Administrador |
| Responsable ARCO-POL / Responsable del tramite | Ejecuta el dia a dia de las solicitudes de titulares dentro de los plazos legales | El mismo Responsable de Privacidad en pyme, o personal de atencion al cliente/legal en empresa mediana | Si |
| Responsable Legal / Compliance | Revisa bases juridicas, documentos, denegatorias y contratos | Abogado interno, o gerente administrativo con apoyo externo en pyme | Si en pyme |
| Responsable de Seguridad / IT | Registra controles tecnicos y evidencia, gestiona incidentes y el cronometro de 72 horas | Jefe de TI, o el proveedor externo de TI si la pyme no tiene TI interno | Si en pyme |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Registra y mantiene actualizados los tratamientos de su area en el RAT, ejecuta las tareas que le asignan | Jefes de cada area | No aplica: por diseno son varios usuarios distintos |
| Aprobador | Aprueba documentos, decisiones de riesgo y cierres de casos sensibles antes de publicarse o enviarse | Gerencia, o el mismo Responsable de Privacidad en pyme | Si en pyme; en mediana/corporativo se recomienda separarlo (ver 2.4) |
| Auditor (interno) | Solo lectura y exportacion de evidencia; no crea ni aprueba nada | Auditoria interna corporativa; en pyme puede recaer en el mismo Responsable de Privacidad con advertencia de autorrevision | Con advertencia visible en pyme |
| Auditor externo (invitado) | Acceso temporal de solo lectura para una auditoria puntual | Firma auditora externa | No aplica, siempre es un tercero |
| Usuario de consulta / Colaborador | Ve y completa unicamente las tareas que se le asignan | Empleados operativos que ejecutan una tarea puntual | Se acumula naturalmente en pyme al ser pocos empleados |
| Titular (portal externo) | Presenta y da seguimiento a su propia solicitud ARCO-POL | Cliente, empleado, ex empleado o candidato de la empresa cliente | No aplica, no es usuario interno de la organizacion |
| Asesor externo invitado | Acceso acotado en tiempo a un caso o modulo especifico | Abogado externo ocasional, consultor de seguridad puntual | No aplica, siempre externo y temporal |

### 2.4 Reglas minimas de separacion de funciones

[mayoria opinion de producto; se indica cuando hay un fundamento legal parcial]

- El rol Auditor (interno o externo) debe ser siempre de solo lectura: nunca debe coincidir con el usuario que carga evidencia o aprueba una accion, para que su verificacion sea independiente. [opinion de producto]
- En organizaciones con areas separadas (a partir de empresa mediana), quien registra o ejecuta una accion sobre datos sensibles o un tratamiento de riesgo alto segun la EIPD no deberia ser la unica persona que la aprueba. [opinion de producto]
- Cuando una solicitud ARCO-POL involucra datos sensibles o existe riesgo de reclamo ante la Direccion de Proteccion de Datos de la ACE (OBL-ARCO-14), el sistema debe permitir escalar la decision de denegatoria a un segundo revisor antes de notificar al titular. [opinion de producto, apoyada en la exigencia de motivacion del Art. 22 y en que la denegatoria indebida es infraccion muy grave segun el catalogo del Art. 56]
- Un mismo usuario no deberia acumular simultaneamente Administrador y Auditor sobre el mismo periodo de evidencia, salvo en pyme, donde el sistema lo permite mostrando siempre una advertencia visible de "autorrevision". [opinion de producto]
- Todo cierre de un incidente de seguridad debe dejar registrada la evidencia de la decision (quien decidio, cuando, con que fundamento), aunque la misma persona haya gestionado todo el caso; esto no exige dos personas distintas por ley, pero si una trazabilidad verificable, en linea con la documentacion obligatoria de toda vulneracion (OBL-INC-04, Art. 25 inciso final) y el principio de responsabilidad demostrada (OBL-PRIN-03, Art. 5 lit. i).
- Umbral configurable de tamano: por debajo de un numero de empleados definido por producto (propuesta inicial: 50), el sistema no exige separacion de funciones, solo la recomienda; por encima de ese umbral, advierte y permite al Administrador activar el bloqueo de la acumulacion Aprobador + Auditor en la misma persona. [opinion de producto, umbral sin respaldo legal]

---

## 3. Anti-features

Lista razonada de lo que el producto no debe ser ni hacer. Cada item indica su razon (legal, de producto, de seguridad o de privacidad) y la alternativa que si se ofrece.

| # | El producto NO debe... | Razon | Alternativa que si se ofrece |
|---|---|---|---|
| 1 | Ser un CRM de los clientes de la empresa que lo usa | Producto | Registrar metadatos del tratamiento (que sistema, quien lo administra, categorias, retencion), sin duplicar la base de clientes del cliente |
| 2 | Ser un SIEM ni una herramienta de monitoreo de seguridad en tiempo real | Seguridad, Producto | Catalogo de controles donde la empresa registra evidencia de que el control existe, su responsable y su vigencia |
| 3 | Sustituir al abogado ni emitir dictamenes juridicos vinculantes | Legal | Mostrar el fundamento normativo (OBL-ID y articulo) y marcar la decision como "requiere validacion de asesoria especializada" cuando sea juridica |
| 4 | Actuar como el Delegado de Proteccion de Datos del cliente ni ejercer sus funciones legales (Arts. 15, 17, 29 Lineamientos DPO) | Legal | Ser la herramienta que usa la persona (interna o externa) designada formalmente como Delegado; el nombramiento y la investidura legal son del cliente, no del proveedor del software |
| 5 | Declarar un porcentaje de cumplimiento legal (0 a 100%) | Legal, Producto | Mostrar estado del programa: controles configurados, tareas pendientes, evidencia disponible (ver 1.2 y 1.3) |
| 6 | Decidir automaticamente si una base juridica es valida para un tratamiento concreto | Legal | Registrar la base elegida por la empresa y mostrar una nota de riesgo cuando exista ambiguedad legal conocida (seccion 8 de `03_hallazgos_regulatorios.md`), dejando la decision al usuario |
| 7 | Resolver automaticamente (aceptar o denegar) solicitudes ARCO-POL sin intervencion humana | Legal | Calcular plazos, mostrar las causales tasadas por la ley y preparar el borrador de respuesta; el responsable interno decide y aprueba |
| 8 | Copiar o centralizar la base de datos completa del cliente (por ejemplo, toda la base de un CRM o un ERP) | Privacidad, Seguridad | Registrar solo metadatos del tratamiento: donde esta el dato, quien lo administra, categorias y retencion |
| 9 | Almacenar dentro del sistema los datos biometricos, de salud u otros datos sensibles de los titulares del cliente | Privacidad, Seguridad | Registrar la existencia del tratamiento, su base legal (OBL-SENS-06, OBL-SENS-07) y su ubicacion, no el dato sensible en si, salvo un adjunto puntual estrictamente necesario para un expediente ARCO-POL, con controles reforzados |
| 10 | Operar como plataforma de videovigilancia ni almacenar las grabaciones de camaras | Seguridad, Producto | Registrar el tratamiento de videovigilancia (OBL-SENS-08), su base legal y su EIPD, nunca las imagenes mismas |
| 11 | Ejecutar controles tecnicos de seguridad en los sistemas del cliente (parchear, cifrar, hacer backups, configurar firewalls) | Seguridad, Producto | Ofrecer el catalogo de controles donde la empresa registra la evidencia de que el control existe y quien lo administra |
| 12 | Emitir la certificacion oficial de Delegado de Proteccion de Datos | Legal | Recordar el tramite y sus plazos (por ejemplo, 15 dias habiles de comunicacion a la ACE) y enlazar al canal oficial de la ACE |
| 13 | Presentar tramites o comunicaciones directamente ante la ACE en nombre de la empresa sin que esta lo autorice y ejecute (por ejemplo, la puesta en conocimiento del Art. 45) | Legal, Seguridad | Preparar el contenido y dejar evidencia del intento de cumplimiento; la empresa presenta el tramite por el canal oficial (que ademas, segun la seccion 8 de hallazgos, la ACE aun no ha habilitado formalmente) |
| 14 | Asumir que la reforma 659 esta vigente antes de que se confirme su publicacion en el Diario Oficial | Legal | Doble estado configurable (ACTUAL / FUTURO) con activacion manual y registro de la fecha del cambio (ver 1.1.1) |
| 15 | Dar consultoria general de seguridad informatica (pentesting, hardening de servidores) | Producto, Seguridad | Recomendar contratar un proveedor especializado y registrar el resultado de ese trabajo como evidencia dentro del catalogo de controles |
| 16 | Ser una plataforma multipais de talla unica que aplique reglas de otras jurisdicciones (por ejemplo GDPR) al caso salvadoreno | Legal, Producto | Motor de reglas separado por pais (nucleo comun mas "paquete regulatorio" de El Salvador), sin mezclar plazos ni catalogos de otra jurisdiccion mientras el analisis se limite a El Salvador |
| 17 | Sustituir la firma o aprobacion formal de un contrato o DPA por parte de las personas legalmente facultadas de la empresa | Legal | Generar el borrador y dejar el flujo de aprobacion interna a cargo del responsable designado por la empresa |
| 18 | Calificar por si mismo si un tercero o un pais representa "nivel de proteccion adecuado" bajo el Art. 44 | Legal | Mostrar un cuestionario de factores de riesgo y dejar la conclusion marcada como "pendiente de validacion por la organizacion o por asesoria legal" |
| 19 | Permitir que un usuario borre o modifique el historial de auditoria | Seguridad | Bitacora de solo escritura por adicion (append-only), visible para Auditor y Administrador, sin funcion de edicion ni borrado para ningun rol |
| 20 | Exponer el portal del titular sin ninguna verificacion minima de identidad | Seguridad, Privacidad | Flujo de verificacion de identidad configurable segun el canal (por ejemplo, adjuntar DUI o verificar por el correo previamente registrado), documentado como parte del expediente |
| 21 | Convertirse en un servicio donde el proveedor administra las solicitudes ARCO-POL del cliente ("outsourcing de privacidad") como parte del producto base | Producto, Legal | Mantenerse como herramienta de autogestion; cualquier servicio de asesoria externa se ofreceria por separado, fuera del software y prestado por terceros claramente identificados como tales |
| 22 | Usar en su comunicacion comercial frases como "cumplimiento garantizado" o "blindaje legal 100%" | Legal, Producto | Comunicar la propuesta de valor como organizacion, evidencia y trazabilidad (documento maestro, seccion 3), nunca como garantia de un resultado legal |
| 23 | Tratar datos de distinta sensibilidad de forma identica dentro de un mismo formulario o tratamiento (por ejemplo, equiparar datos de salud con datos de contacto) | Legal, Privacidad | Catalogo de categorias de datos con el nivel de sensibilidad marcado explicitamente, y reglas de consentimiento reforzado cuando corresponda (OBL-SENS-01 a OBL-SENS-08) |

---

## Resumen de decisiones que quedan como opinion de producto (no exigidas expresamente por la ley)

- El umbral de 50 empleados para activar la exigencia de separacion de funciones.
- El nombre y alcance exacto de los roles estandar (Aprobador, Usuario de consulta, Asesor externo invitado, etc.); la ley solo exige de forma expresa la figura del Delegado (mientras este vigente el regimen actual).
- Las metricas de exito del producto (cobertura, adopcion, retencion comercial).
- Los textos de descargo propuestos en 1.3: la redaccion es una propuesta de producto, no un formato exigido por la ACE.
- El criterio conservador de "horas corridas" para el plazo de 72 horas del Art. 25, mientras no exista pronunciamiento oficial (incertidumbre 1, seccion 9 de `03_hallazgos_regulatorios.md`).
