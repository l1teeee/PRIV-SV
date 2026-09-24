# Lente 4.4 - Funciones faltantes

Fecha de este informe: 2026-09-24. Fase: analisis funcional (sin propuestas de codigo, SQL, API, stack ni infraestructura).

Rol: business analyst y especialista en proteccion de datos.

## 1. Objetivo y metodo

Este informe cruza las 105 obligaciones de `matriz_obligaciones.md` / `matriz_obligaciones.json` (IDs canonicos OBL-AREA-NN) contra los modulos propuestos en el documento maestro `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md`, secciones 11 a 32 (dominios funcionales) y 45 (hipotesis de MVP). Para cada obligacion se verifico si algun modulo del documento maestro la menciona de forma explicita (campo, flujo, plazo o documento) o si solo queda cubierta de forma generica o implicita. Tambien se revisaron `03_hallazgos_regulatorios.md` (secciones 3, 5, 6, 8, 9 y 11) para identificar necesidades de negocio que la investigacion juridica ya detecto pero que el documento maestro no traduce en ningun modulo.

Se aplican dos categorias de hallazgo:
- **Obligacion sin cobertura**: existe un OBL-ID en la matriz y el documento maestro no tiene ningun modulo, campo o flujo que lo mencione.
- **Necesidad empresarial**: funcionalidad util para operar el programa de cumplimiento que no corresponde a un OBL-ID especifico de la matriz (o que se apoya en un articulo identificado en la investigacion juridica pero sin ID canonico todavia). En estos casos se aclara expresamente que es opinion de producto y no una obligacion legal expresa.

Ningun hallazgo de este informe inventa un articulo o una obligacion. Cuando no hay OBL-ID canonico se cita el articulo directamente y se indica el origen (por ejemplo, `03_hallazgos_regulatorios.md` seccion 11.14).

## 2. Resumen (10 lineas)

El documento maestro cubre bien el nucleo operativo (RAT, ARCO-POL generico, incidentes, proveedores, consentimiento, controles), pero dos areas completas de la matriz no tienen modulo propio: SANC (procedimiento sancionador, 9 obligaciones) y buena parte de DPO (delegado, 8 obligaciones) quedan sin un lugar funcional que las desarrolle mas alla de un campo de contacto. La auditoria de cumplimiento (OBL-AUD-01) se confunde en el maestro con el log tecnico de trazabilidad, que es un concepto distinto. El tramite del Art. 45 ante la ACE para flujos transfronterizos no tiene ningun campo ni evidencia asociada, pese a ser OBLIGATORIO. La retencion documental de cumplimiento (aviso 10 anos, expediente ARCO-POL 5 anos) se confunde con la retencion de datos del titular. El diagnostico inicial no pregunta por las exclusiones del Art. 3, lo que puede sobre-obligar a empresas parcialmente excluidas. Tratamientos de alto riesgo mencionados solo como preguntas sueltas del onboarding (menores, videovigilancia, biometria, WhatsApp, marketing) no tienen un flujo propio que traduzca la respuesta en obligaciones especificas. La gestion de grupos empresariales con varias sedes y delegado comun se deja expresamente para "despues" sin desarrollo. El calculo de plazos habiles se trata como una vista de calendario y no como un motor compartido por todos los modulos con plazo legal. Se listan 31 hallazgos (minimo pedido: 25), 12 de prioridad alta.

## 3. Como leer la tabla de hallazgos

Cada hallazgo tiene: que falta, la obligacion o necesidad con su ID (o articulo si no hay ID canonico), por que importa, el modulo del documento maestro al que deberia sumarse (usando la numeracion de secciones 11 a 32 y 45), y prioridad (alta, media, baja) segun: alta = obligacion OBLIGATORIO sin ningun modulo, o riesgo sancionatorio directo; media = obligacion CONDICIONAL sin modulo, o necesidad empresarial con respaldo legal indirecto; baja = obligacion RECOMENDADO, caso de baja frecuencia, o mejora de gestion sin base legal expresa.

---

## A. Delegado de Proteccion de Datos (area DPO de la matriz)

El documento maestro (seccion 11, Modulo de organizacion) solo pide un campo "responsable de privacidad" y un "contacto ARCO-POL". No existe ningun modulo que desarrolle el ciclo de vida del delegado mientras la LPDP vigente lo exige (Arts. 15 y 17, hasta que se publique y entre en vigencia la reforma 659).

### Hallazgo 1 (prioridad alta)
- **Que falta**: nombramiento formal del delegado y su comunicacion a la ACE dentro de 15 dias habiles, mas la notificacion interna en 3 dias habiles.
- **Obligacion**: OBL-DPO-02 (Art. 8 Lineamientos DPO, notificacion interna, 3 dias habiles) y OBL-DPO-03 (Art. 10 Lineamientos DPO, comunicacion a la ACE, 15 dias habiles).
- **Por que importa**: mientras la reforma 659 no este vigente (ver seccion 3 de `03_hallazgos_regulatorios.md`), el delegado sigue siendo obligatorio en el sector privado; omitir el tramite ante la ACE deja a la empresa sin delegado certificado.
- **Modulo sugerido**: ampliar seccion 11 (Organizacion) con un sub-flujo "Delegado de Proteccion de Datos" (nombramiento, tramite ACE, certificacion, vigencia).
- **Prioridad**: alta.

### Hallazgo 2 (prioridad media)
- **Que falta**: recordatorio y registro de la reverificacion periodica del perfil del delegado.
- **Obligacion**: OBL-DPO-04 (Art. 18 Lineamientos DPO, cada 3 anos).
- **Por que importa**: sin este control la empresa puede mantener un delegado cuyo perfil ya no cumple los requisitos de los Lineamientos, sin darse cuenta.
- **Modulo sugerido**: seccion 11 (Organizacion) junto con seccion 28 (Capacitacion), como tarea recurrente ligada al perfil del delegado.
- **Prioridad**: media.

### Hallazgo 3 (prioridad media)
- **Que falta**: generacion y archivo de los informes periodicos del delegado al responsable (minimo dos veces al ano).
- **Obligacion**: OBL-DPO-07 (Art. 30 Lineamientos DPO).
- **Por que importa**: es la evidencia principal de que el delegado esta ejerciendo su funcion de supervision interna; sin plantilla ni recordatorio es facil que se omita.
- **Modulo sugerido**: seccion 11 (Organizacion) + seccion 20 (Politicas y documentos), como documento periodico con plantilla y recordatorio semestral.
- **Prioridad**: media.

### Hallazgo 4 (prioridad media)
- **Que falta**: control de la obligacion de confidencialidad del delegado durante 5 anos despues de su cese.
- **Obligacion**: OBL-DPO-06 (Art. 36 Lineamientos DPO).
- **Por que importa**: la empresa necesita saber, ante una salida del delegado (renuncia, despido, fin de contrato externo), que el deber de confidencialidad sigue vigente y debe documentarse (por ejemplo, en la carta de salida).
- **Modulo sugerido**: seccion 11 (Organizacion), evento de baja de un responsable con plazo de confidencialidad asociado.
- **Prioridad**: media.

### Hallazgo 5 (prioridad media)
- **Que falta**: registro del deber de las demas dependencias, empleados y proveedores de prestar asistencia al delegado.
- **Obligacion**: OBL-DPO-08 (Art. 17 LPDP).
- **Por que importa**: sin este deber explicito en el sistema, areas como IT o Marketing pueden no saber que estan obligadas a responder a requerimientos del delegado dentro de la empresa.
- **Modulo sugerido**: seccion 12 (Usuarios y roles), como responsabilidad transversal asociada al rol "Delegado" frente a los demas roles.
- **Prioridad**: media.

### Hallazgo 6 (prioridad alta)
- **Que falta**: diseno de doble estado del rol responsable de los tramites ARCO-POL (delegado mientras la LPDP vigente lo exige; "sujeto obligado" o responsable interno si la reforma 659 entra en vigencia), con un interruptor administrativo que el equipo del producto active manualmente cuando se confirme la publicacion en el Diario Oficial.
- **Obligacion**: OBL-PLAZO-05 (seguimiento de la reforma 659) y las obligaciones marcadas `afectada_por_reforma_659.afectada = true` en el JSON (17 en total, entre ellas OBL-DPO-01 a 03, OBL-ARCO-01/08/10/11, OBL-CONS-03, OBL-CAP-02, OBL-RET-04).
- **Por que importa**: sin este diseno, el software quedaria desactualizado automaticamente el dia que la reforma entre en vigencia, o peor, aplicaria la reforma antes de tiempo por error de configuracion; el hallazgo esta explicitamente recomendado en `03_hallazgos_regulatorios.md` seccion 3 ("diseno de doble estado recomendado para el software").
- **Modulo sugerido**: seccion 31 (Centro regulatorio) + seccion 41/seccion 32 del maestro (Actualizacion normativa), como caso concreto del motor de versionado de reglas, no solo el ejemplo generico "Regla ARCO-001 version 1/2" que hoy trae la seccion 41.
- **Prioridad**: alta.

---

## B. ARCO-POL: pasos y evidencia no desarrollados

La seccion 17 del maestro describe el ciclo general de una solicitud, pero varios pasos con obligacion legal expresa no aparecen en su lista de campos.

### Hallazgo 7 (prioridad alta)
- **Que falta**: constancia de "en revision o actualizacion" y bloqueo cautelar del dato mientras se tramita una rectificacion.
- **Obligacion**: OBL-ARCO-03 (Art. 9 LPDP, 20 dias habiles).
- **Por que importa**: la ley exige expresamente que el responsable bloquee el dato en revision y lo haga constar; sin este estado especifico el sistema no puede demostrar que cumplio ese paso si la ACE lo requiere.
- **Modulo sugerido**: seccion 17 (ARCO-POL), nuevo estado de expediente "en revision - dato bloqueado" con constancia generada automaticamente.
- **Prioridad**: alta.

### Hallazgo 8 (prioridad alta)
- **Que falta**: notificacion a los receptores de los datos dentro de 5 dias habiles cuando procede una rectificacion, actualizacion o eliminacion y esos datos ya fueron transferidos a un tercero.
- **Obligacion**: OBL-ARCO-11 (Art. 21 inc. 3 LPDP).
- **Por que importa**: es un paso posterior al cierre del expediente que depende del modulo de Proveedores/Transferencias (secciones 22 y 24); si ARCO-POL no dispara automaticamente esta tarea, el plazo de 5 dias puede vencer sin que nadie lo note.
- **Modulo sugerido**: seccion 17 (ARCO-POL) como tarea derivada del cierre del expediente, cruzada con seccion 22 (Proveedores) y seccion 24 (Transferencias) para saber a quienes se transfirieron esos datos.
- **Prioridad**: alta.

### Hallazgo 9 (prioridad media)
- **Que falta**: publicacion de un tarifario de costos de reproduccion, certificacion o envio (el unico cobro permitido) y registro de los cobros efectivamente realizados.
- **Obligacion**: OBL-ARCO-13 (Art. 23 LPDP).
- **Por que importa**: cobrar sin tarifario publicado, o cobrar de mas, es infraccion leve segun la tabla de infracciones de `03_hallazgos_regulatorios.md` seccion 6 ("Exigir pago por solicitudes que deben ser gratuitas").
- **Modulo sugerido**: seccion 18 (Portal de privacidad) para la publicacion, y seccion 17 (ARCO-POL) para el registro de cobros por expediente.
- **Prioridad**: media.

### Hallazgo 10 (prioridad alta)
- **Que falta**: adopcion de los formularios oficiales ARCO-POL de la ACE como estandar minimo del sistema, y un canal de disponibilidad fisica (no solo el portal en linea) para presentar solicitudes.
- **Obligacion**: OBL-ARCO-15 (Art. 32 Lineamientos DPO) y OBL-DOC-04 (Art. 61 inc. 2 LPDP, plazo transitorio ya vencido el 23-may-2025).
- **Por que importa**: la LPDP y los Lineamientos DPO dan por hecho un canal fisico ademas del digital; un portal exclusivamente en linea (seccion 18 del maestro) podria dejar fuera a titulares sin acceso a internet y no cumplir el minimo exigido por los formularios oficiales, que ya existen en el corpus local (`ace_form_acceso.txt`, `ace_form_cancelacion.txt`, `ace_form_portabilidad.txt`).
- **Modulo sugerido**: seccion 18 (Portal de privacidad), agregar explicitamente los campos de los formularios oficiales de la ACE como plantilla base, y documentar un canal de recepcion fisica/presencial o por correo.
- **Prioridad**: alta.

### Hallazgo 11 (prioridad media)
- **Que falta**: gestion del reclamo que el titular puede presentar ante la Direccion de Proteccion de Datos de la ACE cuando no esta conforme con la resolucion del delegado.
- **Obligacion**: OBL-ARCO-14 (Art. 33 inc. 4 Lineamientos DPO, 10 dias habiles de plazo del titular para reclamar).
- **Por que importa**: es la segunda instancia del ciclo ARCO-POL; sin un estado de expediente para "reclamo ante la ACE" la empresa pierde visibilidad de que su caso escalo a la autoridad.
- **Modulo sugerido**: seccion 17 (ARCO-POL), estado adicional de expediente "reclamo ante ACE", enlazado con seccion 31 (Centro regulatorio) para el seguimiento de la respuesta de la autoridad.
- **Prioridad**: media.

---

## C. Transferencias internacionales: el tramite del Art. 45

### Hallazgo 12 (prioridad alta)
- **Que falta**: tramite y evidencia de haber puesto en conocimiento de la ACE cada flujo transfronterizo de datos, incluyendo la informacion de la transferencia y el "registro de banco de datos" que exige el Art. 45 inciso 2.
- **Obligacion**: OBL-TRANSF-05 (Art. 45 LPDP).
- **Por que importa**: es OBLIGATORIO y no tiene ningun campo asociado en la seccion 24 (Transferencias internacionales) del maestro, que solo pide registrar tratamiento, proveedor, pais, contrato y evidencia interna, sin el paso especifico de notificacion a la autoridad. `03_hallazgos_regulatorios.md` seccion 8, punto 3, advierte que la ACE no ha habilitado ningun canal o formulario para esto: el software debe al menos registrar el intento de cumplimiento (o su imposibilidad) como evidencia de buena fe, dato que hoy no tiene donde guardarse.
- **Modulo sugerido**: seccion 24 (Transferencias internacionales), nuevo campo "puesta en conocimiento de la ACE" (fecha, medio usado, evidencia, o motivo de imposibilidad si la ACE no tiene canal habilitado).
- **Prioridad**: alta.

---

## D. Procedimiento sancionador: sin modulo propio

La matriz tiene 9 obligaciones en el area SANC. El documento maestro no tiene ningun modulo dedicado a gestionar un procedimiento sancionador activo contra la empresa; la seccion 31 (Centro regulatorio) es solo material de consulta sobre la norma vigente, no un expediente de defensa administrativa.

### Hallazgo 13 (prioridad media)
- **Que falta**: gestion de requerimientos de informacion que la ACE puede solicitar a la empresa sobre antecedentes, documentos o programas de tratamiento de datos.
- **Necesidad/obligacion**: Art. 50 lit. t) LPDP. No tiene OBL-ID propio en `matriz_obligaciones.json`; identificada en `03_hallazgos_regulatorios.md` seccion 11.14 como obligacion de hallazgos sin equivalente en la matriz (facultad de la ACE, de bajo riesgo de omision practica segun esa nota, pero util para el diseno del producto).
- **Por que importa**: sin un lugar para registrar y responder este tipo de requerimiento, la empresa no tiene forma de demostrar que respondio a tiempo ni de centralizar la evidencia entregada.
- **Modulo sugerido**: nuevo sub-modulo "Procedimiento sancionador / requerimientos ACE", enlazado con seccion 25 (Centro de evidencias) y seccion 16 (Centro de tareas).
- **Prioridad**: media.

### Hallazgo 14 (prioridad media)
- **Que falta**: preparacion para inspecciones y diligencias preliminares de investigacion de la ACE.
- **Necesidad/obligacion**: Art. 12 Normativa PAS (90 dias habiles para las diligencias preliminares, ver `03_hallazgos_regulatorios.md` seccion 5). No tiene OBL-ID propio en la matriz; conecta con OBL-SANC-01 (catalogo de infracciones) y OBL-AUD-01 (auditorias anuales) como necesidad de "estar listo para mostrar evidencia en cualquier momento".
- **Por que importa**: una inspeccion puede llegar sin aviso previo prolongado; si la empresa no tiene forma de generar rapido un paquete de evidencia por obligacion, la diligencia preliminar puede agravarse en procedimiento sancionador formal.
- **Modulo sugerido**: seccion 30 (Paquete de evidencias), agregar un modo "preparacion de inspeccion" que arme el paquete completo por obligacion bajo demanda.
- **Prioridad**: media.

### Hallazgo 15 (prioridad alta)
- **Que falta**: contestacion del emplazamiento del procedimiento sancionador dentro de 5 dias habiles.
- **Obligacion**: OBL-SANC-05 (Art. 21 Normativa PAS).
- **Por que importa**: si la empresa no comparece, los hechos se tienen por contestados negativamente segun la tabla de plazos de `03_hallazgos_regulatorios.md` seccion 5; es el paso con mayor riesgo de perdida de defensa si no hay una tarea con plazo y alerta.
- **Modulo sugerido**: nuevo sub-modulo "Procedimiento sancionador" (mismo del hallazgo 13), con tarea de plazo fijo de 5 dias habiles y escalamiento automatico.
- **Prioridad**: alta.

### Hallazgo 16 (prioridad media)
- **Que falta**: pago de la multa impuesta dentro de 15 dias habiles y seguimiento de las medidas adicionales que ordene la ACE para restablecer la legalidad.
- **Obligacion**: OBL-SANC-06 (Art. 44 Normativa PAS, matriz) y OBL-SANC-03 (Art. 58 LPDP, medidas adicionales).
- **Por que importa**: sin tarea con plazo, el vencimiento del pago puede generar recargos o agravar la situacion frente a la ACE; las medidas adicionales (por ejemplo, corregir un tratamiento) necesitan convertirse en tareas de cumplimiento igual que cualquier otra obligacion.
- **Modulo sugerido**: mismo sub-modulo "Procedimiento sancionador", con tarea de pago y tareas derivadas de las medidas ordenadas, enlazadas al Centro de tareas (seccion 16).
- **Prioridad**: media.

### Hallazgo 17 (prioridad baja)
- **Que falta**: registro y monitoreo de la publicidad de resoluciones sancionatorias (version publica que la ACE publica segun el Art. 55).
- **Obligacion**: OBL-SANC-08 (Art. 55 LPDP).
- **Por que importa**: una empresa sancionada puede necesitar saber que su caso fue publicado y en que terminos, para gestionar reputacion y para tener registro propio de precedentes que le afectan.
- **Modulo sugerido**: seccion 31 (Centro regulatorio), como referencia vinculada al expediente sancionador propio.
- **Prioridad**: baja.

### Hallazgo 18 (prioridad baja)
- **Que falta**: historial propio de infracciones y sanciones recibidas, util para valorar el riesgo de la empresa ante nuevos hallazgos.
- **Necesidad empresarial (opinion de producto, no obligacion legal expresa)**: el Art. 57 LPDP fija rangos de multa por categoria de infraccion pero no menciona reincidencia ni fija criterios de graduacion en el texto revisado (`ace_decreto_144.txt`, Art. 57); la Normativa Sancionadora OCR tampoco menciona el termino. No existe por tanto una obligacion legal expresa de "registrar reincidencia": esta es una recomendacion de diseno para gestion de riesgo interno, no un mandato normativo.
- **Por que importa**: aunque no sea obligacion legal, sirve como senal de riesgo para priorizar controles y como evidencia de mejora continua ante una eventual sancion futura.
- **Modulo sugerido**: seccion 26 (Riesgos/EIPD) o el mismo sub-modulo "Procedimiento sancionador", como campo de historial, dejando explicito en el propio sistema que no es un requisito legal sino buena practica.
- **Prioridad**: baja.

---

## E. Auditoria de cumplimiento: confundida con el log tecnico

### Hallazgo 19 (prioridad alta)
- **Que falta**: un programa sustantivo de auditoria anual de cumplimiento (alcance, hallazgos, plan de accion, cierre), distinto del log tecnico de auditoria y trazabilidad.
- **Obligacion**: OBL-AUD-01 (Art. 8 lit. b Politicas de Actuacion ACE, periodicidad anual).
- **Por que importa**: la seccion 29 del maestro ("Auditoria y trazabilidad") describe exclusivamente el log inmutable de acciones del sistema (WORM, append-only, hash chaining), que es un mecanismo tecnico de trazabilidad, no la obligacion sustantiva de realizar y documentar una auditoria de cumplimiento cada ano. Son dos cosas distintas y el documento maestro solo desarrolla la primera.
- **Modulo sugerido**: nuevo sub-modulo "Auditoria de cumplimiento" dentro o junto a la seccion 29, con planificacion anual, alcance, hallazgos, responsables de correccion y evidencia de cierre, separado conceptualmente del log de sistema.
- **Prioridad**: alta.

---

## F. Capacitacion: falta el plan anual formal

### Hallazgo 20 (prioridad media)
- **Que falta**: plan anual de capacitacion del personal e induccion de personas nuevas, como documento propio con periodicidad anual.
- **Obligacion**: OBL-CAP-02 (Art. 22 Lineamientos DPO, condicional a tener delegado; se aplica mientras la LPDP vigente lo exija).
- **Por que importa**: la seccion 28 del maestro habla de cursos, microlearning y certificados en terminos generales, pero no pide un plan anual formal ni distingue la induccion de personal nuevo del reentrenamiento periodico; sin esa distincion la empresa no puede demostrar que cumplio con el plan como documento (no solo como actividad suelta).
- **Modulo sugerido**: seccion 28 (Capacitacion), agregar el "Plan anual de capacitacion e induccion" como documento versionado (enlazado con seccion 20, Politicas y documentos).
- **Prioridad**: media.

---

## G. Retencion documental de cumplimiento (distinta de la retencion de datos del titular)

La seccion 21 del maestro modela la retencion de **datos personales por tratamiento** (categoria, sistema, obligacion, finalidad). No modela la retencion de la **documentacion de cumplimiento propia de la empresa**, que tiene plazos distintos y motivos distintos.

### Hallazgo 21 (prioridad media)
- **Que falta**: conservacion de la documentacion del aviso de privacidad por un minimo de 10 anos, como evidencia de cumplimiento y no como dato personal del titular.
- **Obligacion**: OBL-RET-04 (Art. 31 Lineamientos DPO).
- **Por que importa**: si se aplica el mismo motor de retencion de datos personales (seccion 21) a este documento, se corre el riesgo de eliminarlo quinamente junto con los datos de un titular especifico, cuando en realidad el aviso debe conservarse por su propio plazo, independiente de cualquier titular individual.
- **Modulo sugerido**: seccion 20 (Politicas y documentos), campo de "plazo de conservacion de cumplimiento" (10 anos minimo) distinto del motor de retencion de datos personales de la seccion 21.
- **Prioridad**: media.

### Hallazgo 22 (prioridad media)
- **Que falta**: retencion del expediente ARCO-POL y de incidentes como prueba de descargo, minimo recomendado de 5 anos.
- **Obligacion**: OBL-RET-05 (Art. 47 Normativa PAS, en relacion con Art. 5 lit. i LPDP, principio de responsabilidad demostrada).
- **Por que importa**: la seccion 30 (Paquete de evidencias) del maestro reune evidencia pero no fija cuanto tiempo debe conservarse un expediente cerrado antes de poder eliminarlo; sin esta regla, un expediente clave para defenderse en un procedimiento sancionador podria borrarse antes de que prescriba la infraccion asociada (5 anos, Art. 47 Normativa PAS).
- **Modulo sugerido**: seccion 17 (ARCO-POL) y seccion 25 (Incidentes), agregar plazo de retencion post-cierre del expediente, enlazado con seccion 30.
- **Prioridad**: media.

---

## H. Diagnostico inicial: faltan preguntas de exclusion y de aplicabilidad especial

### Hallazgo 23 (prioridad media)
- **Que falta**: preguntas del diagnostico/onboarding que detecten las exclusiones del Art. 3 LPDP (historial crediticio bajo ley especial, ambito domestico, seguridad publica y registros publicos).
- **Obligacion**: OBL-AMB-02, OBL-AMB-03, OBL-AMB-04 (Art. 3 lit. a, b, c y d).
- **Por que importa**: la seccion 15 (Onboarding) del maestro lista preguntas sobre empleados, camaras, CRM, biometria, etc., pero ninguna pregunta detecta si parte de la actividad de la empresa esta excluida del ambito de la ley; sin esto el sistema puede generar obligaciones sobre tratamientos que en realidad estan fuera del alcance de la LPDP (por ejemplo, reporte de buro de credito bajo su ley especial).
- **Modulo sugerido**: seccion 15 (Onboarding / Compliance Wizard), agregar preguntas de exclusion antes de generar el plan de cumplimiento de la seccion 10 del prompt de analisis funcional.
- **Prioridad**: media.

### Hallazgo 24 (prioridad baja)
- **Que falta**: deteccion de si la empresa es operador de infraestructura critica, para activar el reporte de incidentes de ciberseguridad a la ACE ademas de la notificacion de vulneraciones de datos personales.
- **Obligacion**: OBL-INC-05 (Art. 6 lit. f-g Ley de Ciberseguridad, en relacion con Art. 2 y Art. 8 lit. f-g).
- **Por que importa**: es una obligacion condicional que aplica a un subconjunto pequeno pero critico de clientes (por ejemplo, bancos, telecomunicaciones); sin una pregunta de diagnostico que la detecte, el modulo de Incidentes (seccion 25) trataria toda vulneracion igual, sin activar el reporte adicional que corresponde a ese perfil de empresa.
- **Modulo sugerido**: seccion 15 (Onboarding), pregunta de clasificacion sectorial; seccion 25 (Incidentes), flujo adicional condicionado a esa respuesta.
- **Prioridad**: baja.

---

## I. Tratamientos de alto riesgo: preguntas sueltas sin flujo propio

El maestro incluye preguntas de onboarding sobre menores, camaras, biometria y WhatsApp (seccion 15), pero no define que hace el sistema con esas respuestas mas alla de "sugerir tratamientos, tareas, riesgos, documentos". Cada uno de estos temas tiene obligaciones especificas en la matriz que necesitan un flujo propio, no solo una bandera activada en el diagnostico.

### Hallazgo 25 (prioridad alta)
- **Que falta**: flujo especifico para tratamiento de datos de menores (ninez y adolescencia): consentimiento parental, verificacion de la relacion parental, ejercicio progresivo de facultades y lenguaje adaptado al informar al menor.
- **Obligacion**: OBL-CONS-06 (Art. 56 lit. c num. 3, en relacion con Art. 5 lit. j y Art. 42) y OBL-PRIN-04 (Art. 5 lit. j).
- **Por que importa**: `03_hallazgos_regulatorios.md` seccion 9, punto 8, senala una tension no resuelta entre la LPDP y la Ley Crecer Juntos sobre la edad de consentimiento digital; sin un flujo propio que capture consentimiento parental de forma diferenciada, la empresa no tiene como demostrar que trato datos de un menor conforme a la ley, y el sistema tampoco puede alertar sobre la incertidumbre legal para que la empresa pida asesoria.
- **Modulo sugerido**: seccion 19 (Consentimiento), sub-flujo "titular menor de edad" con captura de consentimiento parental y aviso de incertidumbre legal.
- **Prioridad**: alta.

### Hallazgo 26 (prioridad alta)
- **Que falta**: flujo especifico para videovigilancia y reconocimiento facial: senalizacion, evaluacion de riesgo obligatoria y plazo de conservacion de las grabaciones.
- **Obligacion**: OBL-SENS-08 (Arts. 4, 7, 12 y 16 LPDP).
- **Por que importa**: la videovigilancia con reconocimiento facial trata datos biometricos, que son sensibles (OBL-SENS-06); el maestro solo la menciona como una pregunta de onboarding ("Tiene camaras?") sin conectarla con el modulo de Riesgos/EIPD (seccion 26) ni con un periodo de retencion propio de las grabaciones.
- **Modulo sugerido**: seccion 13 (Inventario de datos) + seccion 26 (Riesgos/EIPD), plantilla de tratamiento "videovigilancia" que dispare automaticamente la evaluacion de riesgo y el plazo de retencion de grabaciones.
- **Prioridad**: alta.

### Hallazgo 27 (prioridad media)
- **Que falta**: obligacion de ofrecer una alternativa no biometrica cuando se usa biometria (por ejemplo, control de asistencia con huella) y de obtener consentimiento por escrito para ese tratamiento.
- **Obligacion**: OBL-SENS-07 (Art. 26 inc. 4 y Art. 37 LPDP).
- **Por que importa**: no basta con registrar el consentimiento biometrico; la ley exige que exista una alternativa no biometrica disponible para quien no quiera dar su dato biometrico, y el maestro no menciona ese requisito en ningun lugar.
- **Modulo sugerido**: seccion 19 (Consentimiento), campo obligatorio "alternativa no biometrica ofrecida" para cualquier tratamiento marcado como biometrico.
- **Prioridad**: media.

### Hallazgo 28 (prioridad media)
- **Que falta**: tratamiento especifico del canal WhatsApp Business como posible transferencia internacional implicita (los datos pueden alojarse en servidores fuera de El Salvador) y su propio consentimiento de canal.
- **Necesidad empresarial (opinion de producto)**: no hay un OBL-ID exclusivo para "WhatsApp"; la necesidad conecta con OBL-TRANSF-01, OBL-TRANSF-03 y OBL-TRANSF-04 (transferencias nacionales e internacionales) si el proveedor del canal aloja datos fuera del pais, y con el principio de informacion en la recoleccion (OBL-AVISO-04, Art. 7).
- **Por que importa**: el maestro incluye la pregunta "Utiliza WhatsApp empresarial?" en el onboarding (seccion 15) pero no explica que hace el sistema con esa respuesta; sin conectarla al modulo de Transferencias (seccion 24), la empresa podria no darse cuenta de que ese canal implica una transferencia internacional de datos.
- **Modulo sugerido**: seccion 15 (Onboarding), regla que conecte la respuesta "usa WhatsApp Business" con una entrada sugerida en seccion 24 (Transferencias) y seccion 20 (Documentos, mencion en el aviso de privacidad).
- **Prioridad**: media.

### Hallazgo 29 (prioridad media)
- **Que falta**: modulo de supresion/opt-out de marketing directo, diferenciado del consentimiento general y enlazado con la oposicion ARCO-POL.
- **Obligacion**: OBL-ARCO-05 (Art. 12 LPDP, oposicion al tratamiento, incluido marketing directo).
- **Por que importa**: el maestro menciona "email marketing" y "campanas digitales" solo como preguntas de onboarding (seccion 15); no define una lista de supresion especifica para marketing que se alimente automaticamente cuando un titular ejerce oposicion via ARCO-POL, lo que podria hacer que la empresa siga contactando a alguien que ya se opuso.
- **Modulo sugerido**: seccion 19 (Consentimiento), lista de supresion de marketing enlazada con seccion 17 (ARCO-POL, oposicion).
- **Prioridad**: media.

---

## J. Estructura corporativa: grupos empresariales y multiples sedes

### Hallazgo 30 (prioridad media)
- **Que falta**: gestion de grupos empresariales con varias sedes o varias razones sociales que comparten un mismo delegado o responsable interno, con vision consolidada de RAT, tareas y evidencia por entidad y a nivel de grupo.
- **Necesidad empresarial (opinion de producto)**: no hay un OBL-ID especifico para "grupo empresarial"; la necesidad se apoya en OBL-DPO-01 (obligatoriedad del delegado, que podria ser una sola persona para varias empresas del mismo grupo) y OBL-AMB-01 (ambito universal, aplicable a cada persona juridica del grupo por separado).
- **Por que importa**: el maestro (seccion 11) menciona sucursales dentro de una misma organizacion, pero deja expresamente para despues la posibilidad de "multiples organizaciones por cuenta" bajo una "modalidad corporativa o partner", sin desarrollarla; empresas salvadorenas con varias razones sociales bajo un mismo grupo (frecuente en retail, financieras y conglomerados) necesitan saber si el producto los sirve desde el MVP o no.
- **Modulo sugerido**: seccion 11 (Organizacion), definir si el MVP soporta una organizacion con varias sucursales de la misma razon social, y dejar explicito en la seccion 45 (MVP) que el soporte multi-empresa/grupo con delegado comun es V1 o Enterprise, no MVP.
- **Prioridad**: media.

---

## K. Motor de plazos habiles: falta como servicio transversal

### Hallazgo 31 (prioridad alta)
- **Que falta**: un motor de computo de dias y horas habiles (con el calendario de asuetos nacionales) que sea un servicio compartido por todos los modulos con plazo legal (ARCO-POL, incidentes de 72 horas, DPO, procedimiento sancionador), y no solo una vista de calendario para el usuario.
- **Obligacion**: OBL-PLAZO-01 (Art. 82 LPA, regla de computo) y OBL-PLAZO-02 (Art. 190 Codigo de Trabajo y D.L. 339/2016, D.L. 208/2012, calendario de asuetos).
- **Por que importa**: el maestro trata el calculo de plazos dentro de la seccion 17 (ARCO-POL, "el calculo de plazos debe considerar dias habiles, fines de semana, feriados, asuetos configurables") y la seccion 30 del prompt de analisis funcional describe un "calendario central", pero ninguno de los dos se plantea explicitamente como el unico punto de verdad que deben usar TODOS los plazos legales del sistema (20+20 dias ARCO-POL, 72 horas de incidentes, 15/3/10 dias del delegado, 5/15 dias del procedimiento sancionador). Si cada modulo implementa su propio calculo de dias habiles, un cambio en el calendario de asuetos (por ejemplo, un asueto decretado a ultima hora) tendria que actualizarse en varios lugares con riesgo de inconsistencia entre modulos.
- **Modulo sugerido**: definir el "motor de plazos habiles" como una funcion transversal (no un modulo visible aparte, sino una capa compartida), documentada junto con la seccion 30 del prompt de analisis funcional (Calendario central) y referenciada desde ARCO-POL (17), Incidentes (25), Organizacion/Delegado (11) y el nuevo sub-modulo de Procedimiento sancionador (hallazgos 13 a 18).
- **Prioridad**: alta.

---

## 4. Tabla resumen de los 31 hallazgos

| # | Que falta (resumen) | Obligacion / necesidad | Prioridad |
|---|---|---|---|
| 1 | Nombramiento y comunicacion del delegado a la ACE (15 dias) | OBL-DPO-02, OBL-DPO-03 | Alta |
| 2 | Reverificacion del perfil del delegado cada 3 anos | OBL-DPO-04 | Media |
| 3 | Informes semestrales del delegado | OBL-DPO-07 | Media |
| 4 | Confidencialidad del delegado tras el cese (5 anos) | OBL-DPO-06 | Media |
| 5 | Deber de asistencia al delegado | OBL-DPO-08 | Media |
| 6 | Doble estado del rol ARCO-POL ante la reforma 659 | OBL-PLAZO-05 y obligaciones afectadas | Alta |
| 7 | Constancia y bloqueo cautelar en rectificacion | OBL-ARCO-03 | Alta |
| 8 | Notificacion a receptores en 5 dias | OBL-ARCO-11 | Alta |
| 9 | Tarifario de costos de reproduccion | OBL-ARCO-13 | Media |
| 10 | Formularios oficiales ACE y canal fisico | OBL-ARCO-15, OBL-DOC-04 | Alta |
| 11 | Reclamo del titular ante la Direccion de Proteccion de Datos | OBL-ARCO-14 | Media |
| 12 | Tramite/evidencia del Art. 45 ante la ACE | OBL-TRANSF-05 | Alta |
| 13 | Requerimientos de informacion de la ACE | Art. 50 lit. t (sin OBL-ID en matriz) | Media |
| 14 | Preparacion para inspecciones/diligencias preliminares | Art. 12 Normativa PAS (sin OBL-ID en matriz) | Media |
| 15 | Contestacion de emplazamiento en 5 dias | OBL-SANC-05 | Alta |
| 16 | Pago de multa y medidas adicionales | OBL-SANC-06, OBL-SANC-03 | Media |
| 17 | Publicidad de resoluciones sancionatorias | OBL-SANC-08 | Baja |
| 18 | Historial propio de infracciones/sanciones | Necesidad de negocio (sin base legal expresa de reincidencia) | Baja |
| 19 | Programa de auditoria anual de cumplimiento | OBL-AUD-01 | Alta |
| 20 | Plan anual de capacitacion e induccion | OBL-CAP-02 | Media |
| 21 | Conservacion de la documentacion del aviso (10 anos) | OBL-RET-04 | Media |
| 22 | Retencion del expediente ARCO-POL/incidentes (5 anos) | OBL-RET-05 | Media |
| 23 | Preguntas de exclusion del Art. 3 en el diagnostico | OBL-AMB-02 a 04 | Media |
| 24 | Deteccion de operador de infraestructura critica | OBL-INC-05 | Baja |
| 25 | Flujo de tratamiento de datos de menores | OBL-CONS-06, OBL-PRIN-04 | Alta |
| 26 | Flujo de videovigilancia y reconocimiento facial | OBL-SENS-08 | Alta |
| 27 | Alternativa no biometrica obligatoria | OBL-SENS-07 | Media |
| 28 | WhatsApp Business como transferencia implicita | OBL-TRANSF-01/03/04 (conexion) | Media |
| 29 | Supresion/opt-out de marketing directo | OBL-ARCO-05 | Media |
| 30 | Grupos empresariales con delegado comun | Necesidad de negocio (conecta OBL-DPO-01, OBL-AMB-01) | Media |
| 31 | Motor transversal de plazos habiles | OBL-PLAZO-01, OBL-PLAZO-02 | Alta |

Total: 31 hallazgos (12 alta, 15 media, 4 baja).

## 5. Limitaciones de este informe

- No se evaluo aqui si estos modulos deben ir en MVP, V1 o Enterprise; esa priorizacion corresponde a la seccion 19 a 21 del prompt de analisis funcional (fuera del alcance de este lente).
- Los hallazgos 13, 14, 18, 28 y 30 no tienen OBL-ID canonico en `matriz_obligaciones.json`; se marcan explicitamente como necesidad empresarial u obligacion identificada solo en `03_hallazgos_regulatorios.md`, para no mezclarlos con las 105 obligaciones catalogadas formalmente.
- Este informe no valida si los modulos que "si" cubren cada obligacion lo hacen de forma suficiente en su diseno interno (ficha A-Q); eso corresponde a la fase de diseno de cada modulo, no a este lente de faltantes.
- Cualquier conclusion sobre el alcance exacto del Art. 45 (banco de datos) o sobre la vigencia de la reforma 659 requiere confirmacion de abogado, conforme a las incertidumbres ya documentadas en `03_hallazgos_regulatorios.md` seccion 9.
