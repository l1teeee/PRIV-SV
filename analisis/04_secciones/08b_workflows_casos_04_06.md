## Caso 4. RRHH comienza a usar biometria (control de asistencia con huella o rostro)

Fuentes principales: `03_modulos/MOD-004_ficha.md` (Diagnostico, disparador P-PER-04), `03_modulos/MOD-006_ficha.md` (RAT y Mapa de Datos), `03_modulos/MOD-007_ficha.md` (Consentimiento), `03_modulos/MOD-014_ficha.md` (Riesgos y EIPD), `03_modulos/MOD-015_ficha.md` (Controles de Seguridad), `03_modulos/MOD-009_ficha.md` (Proveedores y Encargados, si el equipo biometrico tiene acceso remoto), `03_modulos/MOD-008_ficha.md` (Documentos y Politicas) y `01_legal/matriz_obligaciones.json` (area SENS).

### Situacion de partida

Avicola San Andres, S.A. de C.V. (empresa mediana, aprox. 300 empleados) decide instalar lectores de huella dactilar en sus dos plantas para reemplazar el marcaje en papel del personal operativo. Daniela Patricia Cornejo Lazo, Coordinadora de Recursos Humanos (perfil 3 de `05_tipos_de_usuario.md`, seccion 5.1), es quien impulsa el cambio y no tiene formacion legal. Jorge Alberto Menendez Rauda, Jefe de Cumplimiento y Riesgo, ejerce el rol de Delegado de Proteccion de Datos interno (perfil 2) y esta en proceso de certificacion ante la ACE. Roberto Antonio Villalta, Gerente de Tecnologia, ejerce el rol de Responsable de Seguridad / IT (perfil 4).

### Disparador

Daniela responde "Si" a la pregunta P-PER-04 del Diagnostico (MOD-004): "su empresa usa o planea usar control de acceso o de asistencia con huella, rostro u otro dato biometrico". Si el diagnostico ya estaba cerrado antes de decidir instalar el lector, el disparador alternativo es que Daniela o Roberto den de alta directamente el tratamiento en el RAT (MOD-006) marcando la categoria de dato "Informacion biometrica".

### Actores y modulos que intervienen

| Rol estandar (05_tipos_de_usuario.md 5.3) | Participacion en este caso |
|---|---|
| Responsable de area (RRHH) | Impulsa el tratamiento, completa la ficha de RAT, captura el consentimiento de cada persona empleada, publica el aviso especifico |
| Delegado de Proteccion de Datos (o Responsable interno) | Revisa y aprueba el paso de la ficha de RAT a Vigente, aprueba la EIPD junto con el Aprobador, resuelve dudas de base juridica |
| Responsable de Seguridad / IT | Evalua y registra el proveedor del equipo biometrico si tiene acceso remoto, vincula el control de seguridad del lector antes de aprobar la ficha |
| Responsable Legal / Compliance | Co-revisa la justificacion de la base de licitud y la suficiencia de la alternativa no biometrica |
| Aprobador | Aprueba, distinto de quien evaluo, la EIPD y la excepcion si se llegara a invocar (Avicola supera el umbral configurable de 50 empleados) |
| Usuario de consulta / Colaborador | Cada persona empleada de planta: recibe el aviso, decide si presta o no el consentimiento biometrico |

| Modulo | Codigo | Papel en este caso |
|---|---|---|
| Diagnostico de Cumplimiento | MOD-004 | Detecta la intencion de usar biometria y dispara tratamiento, tarea, documento y evaluacion |
| RAT y Mapa de Datos | MOD-006 | Registra y clasifica el tratamiento como dato sensible biometrico |
| Consentimiento | MOD-007 | Captura el consentimiento por escrito (o equivalente) y la alternativa no biometrica ofrecida |
| Riesgos y EIPD | MOD-014 | Evalua el riesgo del tratamiento biometrico y su mitigacion |
| Controles de Seguridad | MOD-015 | Registra el control tecnico/organizativo vinculado al lector antes de aprobar el RAT |
| Proveedores y Encargados | MOD-009 | Registra al proveedor del equipo o del software de asistencia, si tiene acceso remoto o aloja las plantillas biometricas |
| Documentos y Politicas | MOD-008 | Publica el aviso especifico de biometria laboral, informa a los empleados |
| Centro de Tareas | MOD-021 | Aloja todas las tareas generadas por el diagnostico y por las automatizaciones de los modulos anteriores |
| Notificaciones | MOD-022 | Canal de las alertas descritas en la seccion siguiente |
| Centro de Evidencias | MOD-019 | Recibe la evidencia de cada modulo con verificacion de integridad |
| Retencion y Eliminacion | MOD-016 | Colaboradora: fija (cuando este activo) el plazo de conservacion del dato biometrico segun la finalidad declarada en el RAT |

### Diagrama ASCII del recorrido de extremo a extremo

```
Daniela (RRHH)              MOD-004            MOD-006 / MOD-007        Roberto (Seg/IT)      Jorge (Delegado)
      |                        |                       |                        |                     |
      | responde Si a          |                       |                        |                     |
      | P-PER-04 (biometria)   |                       |                        |                     |
      +----------------------->|                       |                        |                     |
      |                cierra diagnostico              |                        |                     |
      |                (Cerrado - resultado)            |                        |                     |
      |                        |---------------------->|                        |                     |
      |                        |  crea ficha RAT        |                        |                     |
      |                        |  Borrador; tarea       |                        |                     |
      |                        |  "consentimiento +      |                        |                     |
      |                        |   alternativa"          |                        |                     |
      |                        |                       [RAT: Informacion         |                     |
      |                        |                        biometrica marcada]      |                     |
      |                        |                       |------------------------>|                     |
      |                        |                       | exige control MOD-015   |                     |
      |                        |                       | antes de Vigente        |                     |
      |                        |                       |                 [Control creado          |
      |                        |                       |                  e Implementado]              |
      |                        |                       |<------------------------|                     |
      |                        |                       |                                              |
      |                        |         [MOD-014: EIPD DETECTADO -> ABIERTO -> EVALUADO             |
      |                        |          -> EN_MITIGACION -> PENDIENTE_DE_APROBACION]---------------->|
      |                        |                       |                              aprueba (Aprobador
      |                        |                       |                              distinto, VIGENTE)
      |                        |                       |<---------------------------------------------|
      |                        |             RAT pasa de En revision a Vigente
      |                        |                       |
      |            [MOD-008: Aviso especifico de biometria laboral, Borrador->Vigente]
      |                        |                       |
      | recibe aviso, decide   |                       |
      +----------------------->|  [MOD-007: Consent Presentado -> Vigente (firma) o No otorgado]
      |                                                |
      |                                                v
      |                                    MOD-019 Centro de Evidencias
      |                                    (RAT + Consent + EIPD + Control,
      |                                     cada uno con su propia evidencia)
```

### Paso a paso

| Paso | Quien | Modulo | Que hace en el sistema | Que genera | Plazo y como se calcula | Fundamento |
|---|---|---|---|---|---|---|
| 1 | Daniela (RRHH) | MOD-004 | Responde "Si" a P-PER-04 dentro de la sesion de diagnostico en curso o de un re-diagnostico | Tratamiento sugerido "Control de acceso biometrico de personal (dato sensible)"; tarea "registrar consentimiento por escrito y ofrecer alternativa no biometrica"; documento sugerido "Aviso especifico de biometria laboral"; evaluacion "EIPD recomendada" (ver Contradicciones y huecos, se adopta como obligatoria) | Sin plazo legal propio; prioridad interna CRITICA (regla G.2 de MOD-004) | OBL-SENS-06, OBL-SENS-07, OBL-CONS-04 |
| 2 | Sistema (automatico) | MOD-006 | Al cerrar el diagnostico, crea la ficha de tratamiento en Borrador a partir de la plantilla correspondiente | Ficha con categoria "Informacion biometrica" marcada; etiqueta "Dato sensible" visible en todo listado | Sin plazo | OBL-SENS-01, OBL-SENS-06 (Art. 4 lit. g) |
| 3 | Sistema (automatico) | MOD-006 | Al marcarse "Informacion biometrica", sugiere automaticamente "Requiere EIPD: Si" y crea la tarea "confirmar consentimiento escrito y alternativa no biometrica" enlazada a MOD-007 | Tarea en MOD-021; apertura simultanea de una EIPD en MOD-014 en estado DETECTADO | Sin plazo propio | OBL-SENS-06, OBL-SENS-07 |
| 4 | Daniela (RRHH) | MOD-006 | Completa la ficha (finalidad: control de asistencia del personal; base de licitud); envia a revision | Pasa de Borrador a En revision; crea tarea de revision para Legal/Delegado; si el riesgo es Alto, notifica al Aprobador | Sin plazo legal; buena practica de revision oportuna | OBL-PRIN-02, OBL-PRIN-03 |
| 5 | Jorge (Delegado) o Legal/Compliance | MOD-006 | Revisa la ficha; el sistema exige una justificacion escrita de la base legal porque hay dato sensible (bloqueo si el campo queda vacio) | Justificacion registrada; alerta HIGH si se intenta guardar sin ella | Sin plazo propio, bloqueo inmediato en pantalla | OBL-SENS-01 |
| 6 | Roberto (Seguridad/IT) | MOD-015 | Antes de que la ficha pueda pasar a Vigente, crea o vincula un control de seguridad para el lector biometrico (por ejemplo, cifrado de las plantillas en el dispositivo, control de acceso fisico al equipo) y registra evidencia de su implementacion | Control en estado Implementado con evidencia adjunta y hash | Sin plazo legal propio | OBL-SEG-01 a 06 (colaboradoras), regla de bloqueo "dato biometrico sin control de seguridad enlazado" de MOD-006 |
| 7 | Roberto (Seguridad/IT) | MOD-009 | Si el lector o el software de asistencia tiene acceso remoto a las plantillas biometricas o las aloja en la nube del fabricante, da de alta al proveedor como Encargado del tratamiento, vincula el tratamiento del RAT y evalua el nivel de riesgo (Alto, por tratarse de dato sensible) | Proveedor en Borrador -> En_evaluacion; si aplica, registro "pendiente de confirmar" en MOD-010 si el pais del proveedor no es El Salvador (desarrollado en el Caso 6) | Sin plazo legal propio; se bloquea el paso a Activo sin Contrato/DPA vigente | OBL-PROV-01 (Art. 33 inc. 2), OBL-PROV-02, OBL-PROV-03 |
| 7b | Roberto (Seguridad/IT) | MOD-009 | Si el lector es un dispositivo local que solo guarda las plantillas dentro del equipo, sin conexion a un tercero, confirma explicitamente que no existe encargado que registrar | Nota en la ficha de RAT: "sin proveedor con acceso a datos biometricos"; queda como decision documentada, no automatica (ver seccion siguiente) | Sin plazo | Decision no automatizable, ver "Decisiones que el sistema NO toma" |
| 8 | Sistema (automatico) | MOD-014 | Abre la EIPD en DETECTADO (por el disparo del diagnostico) y crea la tarea "completar cuestionario de riesgo" | Tarea con plazo por defecto de 15 dias habiles (configurable) para el responsable de area | 15 dias habiles por defecto (MOD-023) | OBL-DOC-03 |
| 9 | Roberto o Jorge | MOD-014 | Completa el cuestionario de riesgo; el sistema calcula el nivel (tipicamente Alto, por biometria en relacion laboral) | Pasa a EVALUADO y, por ser Alto, a EN_MITIGACION (bloquea el paso directo a aprobacion) | Sin plazo propio | OBL-DOC-03 |
| 10 | Roberto | MOD-014 | Registra la mitigacion: el control de seguridad del paso 6 y la alternativa no biometrica ofrecida | Pasa a PENDIENTE_DE_APROBACION; recalcula el riesgo residual | Sin plazo propio | OBL-DOC-03 |
| 11 | Aprobador (distinto de quien evaluo) + Jorge | MOD-014 | Aprueban la EIPD | Pasa a VIGENTE; se calcula la fecha de proxima revision (12 meses); evidencia formal con identidad y fecha | Avicola supera el umbral de 50 empleados: aprobador obligatoriamente distinto (05_tipos_de_usuario.md 5.4) | OBL-DOC-03, OBL-PRIN-03 |
| 12 | Jorge (Delegado) o Legal/Compliance | MOD-006 | Aprueba el paso de la ficha de RAT de En revision a Vigente, ya con el control de MOD-015 enlazado y la EIPD vigente | Ficha Vigente; dispara alertas a MOD-007, MOD-008, MOD-014, MOD-015 segun corresponda | Sin plazo legal propio | OBL-DOC-02, OBL-PRIN-03 |
| 13 | Daniela (RRHH) | MOD-008 | Redacta y publica el "Aviso especifico de biometria laboral" (tipo de documento "Otro documento regulatorio", ver Contradicciones y huecos), con la advertencia del derecho a no proporcionar el dato y la existencia de una alternativa | Documento Borrador -> En revision -> Aprobado -> Publicado/Vigente | Sin plazo legal propio para la instalacion del lector | OBL-SENS-02 (Art. 37 inc. 1), OBL-AVISO-04 |
| 14 | Daniela (RRHH) | MOD-007 | Para cada persona empleada, crea el registro de consentimiento en Presentado con el snapshot del aviso vigente; el empleado acepta y firma (firma autografa o equivalente) o declina | Si acepta: Vigente, con archivo de firma adjunto obligatorio. Si declina: No otorgado, conservando la evidencia de que se le advirtio el derecho a no darlo, sin guardar el dato biometrico | Sin plazo legal propio | OBL-SENS-06, OBL-SENS-07 (Art. 26 inc. 4, Art. 37), OBL-CONS-04 |
| 15 | Daniela (RRHH) | MOD-007 | Registra si se ofrecio una alternativa no biometrica (tarjeta o PIN); si marca "No", el sistema no bloquea pero deja una alerta WARNING permanente en el registro | Campo "alternativa no biometrica ofrecida" completado; nota de riesgo si es "No" | Sin plazo | OBL-SENS-07; decision de si el consentimiento sigue siendo libre queda fuera del automatismo (ver seccion siguiente) |
| 16 | Sistema (automatico) | MOD-019 | Consolida la ficha de RAT, el consentimiento, la EIPD y el control de seguridad como evidencia con verificacion de integridad | Paquete de evidencia disponible para Auditor y para una eventual auditoria anual | Se genera con cada aprobacion | OBL-PRIN-03; anti-feature 25 |

### Decisiones que el sistema NO toma

El sistema muestra siempre el texto "Requiere validacion de la organizacion o asesoria especializada" (o su variante especifica) junto a cada una de estas decisiones:

1. Si el consentimiento sigue siendo "libre" en una relacion de subordinacion laboral (por ejemplo, biometria de marcaje). El sistema solo registra si se ofrecio una alternativa no biometrica; no concluye si eso hace al consentimiento valido (MOD-007, seccion H, punto 6; este punto requiere confirmacion de abogado segun la propia matriz de obligaciones, OBL-SENS-07).
2. Si el proveedor del equipo o del software de asistencia biometrica debe registrarse como Encargado del tratamiento (porque tiene acceso remoto a las plantillas) o si es un simple proveedor de hardware sin acceso a datos: el sistema aplica el criterio general del campo "Tipo de entidad" de MOD-009, pero la calificacion final del caso concreto la confirma la persona responsable.
3. Si el nivel de riesgo calculado automaticamente por la EIPD (Alto, en este caso) refleja el riesgo real del tratamiento, y si la mitigacion registrada es suficiente para aceptar el riesgo residual: el campo de conclusion siempre lo completa una persona (Delegado o Legal), nunca el sistema (MOD-014, seccion H, puntos 1 y 3).
4. Si el control de seguridad implementado (por ejemplo, el cifrado del lector) es tecnicamente suficiente o esta bien configurado: exige criterio de un especialista en seguridad informatica (MOD-015, seccion H).
5. Si un dato de reconocimiento facial adicional (si la empresa optara por esa modalidad en vez de huella) activa ademas el regimen de videovigilancia del Art. 4 lit. f): el sistema no decide por si mismo, remite a la clasificacion conjunta OBL-SENS-06/OBL-SENS-08.

El sistema nunca almacena la huella dactilar, el rostro ni ningun otro dato biometrico de las personas empleadas (anti-feature 9, `22_anti_features.md`): solo registra que el tratamiento existe, su base legal, el consentimiento y, si la persona declina, la constancia de la negativa.

### Alertas y escalamientos

| Alerta | Disparador | Nivel | Destinatario | Escalamiento |
|---|---|---|---|---|
| Tratamiento con dato sensible sin justificacion de base | Se intenta guardar la ficha de RAT con "Informacion biometrica" marcada y el campo de justificacion vacio | HIGH (bloqueante) | Responsable de area | No aplica, es bloqueo en pantalla |
| Dato biometrico sin control de seguridad enlazado | La ficha de RAT intenta pasar a Vigente sin al menos un control de MOD-015 enlazado | HIGH (bloqueante) | Responsable de area, Seguridad/IT | No aplica, es bloqueo |
| Consentimiento sensible incompleto | Registro en Presentado con tipo Biometrico sin firma adjunta por mas de 2 dias | WARNING | Responsable de area, Delegado | A Administrador tras 5 dias |
| Consentimiento biometrico sin alternativa ofrecida | Se guarda un consentimiento tipo Biometrico con "alternativa no biometrica ofrecida = No" | WARNING | Responsable de area, Responsable Legal | A Delegado si se repite en el mismo tratamiento |
| EIPD con riesgo Alto o Critico pendiente de mitigacion | La EIPD entra en EN_MITIGACION | HIGH | Seguridad/IT o de area, Delegado | A Aprobador/Gerencia tras 10 dias habiles sin mitigacion |
| Control obligatorio sin evidencia | Un control del catalogo base permanece en Pendiente de implementar mas de 30 dias | HIGH | Seguridad/IT, Delegado | A Gerencia a los 60 dias, con referencia al riesgo de infraccion grave |
| Pais fuera de El Salvador sin registro vinculado en Transferencias | El proveedor del equipo tiene pais distinto de El Salvador y la creacion automatica en MOD-010 falla o se pierde | HIGH | Delegado, Legal/Compliance | A Administrador si persiste 5 dias |

### Evidencia resultante

- Ficha de tratamiento en el RAT, con la categoria "Informacion biometrica" marcada, la justificacion de la base legal y el historial completo de cambios: prueba OBL-DOC-02, OBL-SENS-01 y OBL-SENS-06; vive en MOD-006 y se conserva mientras el tratamiento este activo, y de forma indefinida tras archivarse.
- Registro de consentimiento (o de la negativa) de cada persona empleada, con snapshot del aviso, medio, fecha y archivo de firma con hash: prueba OBL-SENS-02, OBL-SENS-07 y OBL-CONS-04; vive en MOD-007, con el plazo de conservacion que fije MOD-016 cuando este activo.
- Expediente de EIPD con el cuestionario, el calculo de riesgo, la mitigacion y la aprobacion: prueba OBL-DOC-03; vive en MOD-014, conservado mientras el tratamiento este activo mas un minimo adicional de 5 anos desde su archivo (criterio propuesto por el producto, sin norma expresa).
- Control de seguridad del lector, con evidencia adjunta, responsable y vigencia: prueba las obligaciones colaboradoras OBL-SEG-01 a 06; vive en MOD-015.
- Aviso especifico de biometria laboral, version publicada con hash de integridad: prueba OBL-SENS-02 y OBL-AVISO-04; vive en MOD-008, conservado minimo 10 anos (OBL-RET-04, colaboradora).
- Todo lo anterior queda ademas en el AuditLog transversal de solo escritura por adicion, y se exporta con verificacion de integridad hacia MOD-019.

### Variantes y casos borde

- **Pyme con una persona en varios roles.** En Ferreteria y Suministros El Roble (aprox. 30 empleados, por debajo del umbral de 50), si decidiera instalar un lector biometrico, Karla Beatriz Hernandez Mejia (Administradora y Delegada) podria aprobar la ficha de RAT y la EIPD sin una segunda persona, pero el sistema muestra siempre la advertencia visible de "autorrevision"; la captura del consentimiento de cada empleado y la advertencia del derecho a no proporcionar el dato no cambian.
- **Reconocimiento facial en vez de huella.** El mismo tratamiento se marca ademas con OBL-SENS-08 (videovigilancia y reconocimiento facial); se agrega la exigencia de aviso visible del dispositivo y la EIPD pasa a "obligatoria" sin ambiguedad, porque MOD-004 (P-VID-02) ya la etiqueta asi para esta modalidad especifica (a diferencia de la huella, ver Contradicciones y huecos).
- **Grupo corporativo.** En Grupo Financiero Itzalco, si una sociedad instala biometria de acceso a una boveda o area restringida, el mismo flujo aplica dentro de esa sociedad especifica; la vision consolidada de las tres sociedades es funcionalidad V1/Enterprise, no MVP (`02_validacion_de_la_idea.md`, decision 2.7.31).
- **Doble estado de la reforma 659.** El Art. 37 y el Art. 26 inc. 4 (consentimiento por escrito para datos sensibles) no estan entre las 17 obligaciones afectadas por la reforma. Lo que si cambia, si el estado FUTURO se activa, es quien aprueba y ejecuta la revocacion de un consentimiento biometrico (pasa del Delegado al Responsable interno configurable en MOD-002), sin alterar el contenido ni los plazos del consentimiento en si (MOD-007, seccion G, regla 9).
- **La persona empleada se niega y no existia alternativa no biometrica.** El registro queda en No otorgado con la advertencia mostrada; la empresa debe decidir, con apoyo legal, si mantiene el marcaje en papel para esa persona o suspende el requisito, decision que el sistema no toma por ella.

### Cobertura por version

| Funcionalidad | MVP | V1 / V2 |
|---|---|---|
| Ficha de RAT con catalogo de datos sensibles y bloqueo de justificacion | MUST HAVE | - |
| Registro de consentimiento reforzado (biometrico, con firma) y su revocacion | MUST HAVE | - |
| Catalogo de controles de seguridad (MOD-015) con bloqueo de aprobacion sin evidencia | MUST HAVE | - |
| Apertura automatica de la EIPD desde el diagnostico, cuestionario y aprobacion formal | MUST HAVE dentro de MOD-014 (aunque el modulo completo es SHOULD HAVE a nivel global) | Calculo ponderado de riesgo residual y doble control configurable por tipo de tratamiento quedan como mejora (SHOULD HAVE) |
| Registro del proveedor del equipo biometrico como Encargado, con Contrato/DPA obligatorio | MUST HAVE (MOD-009) | Deteccion automatica hacia Transferencias si el proveedor esta fuera de El Salvador (MOD-010) es SHOULD/COULD HAVE |
| Plazo de conservacion del dato biometrico | Campo de texto libre dentro de la ficha del RAT (MVP) | Motor de retencion completo con alertas y flujo de aprobacion de eliminacion (MOD-016, SHOULD HAVE) |
| Plantillas de cuestionario de EIPD especificas para biometria | Plantilla generica unica | Plantilla especializada por tipo de disparador (COULD HAVE) |

### Riesgos especificos del caso y su mitigacion

| Riesgo | Mitigacion de diseno |
|---|---|
| Que Daniela, sin formacion legal, no sepa que instalar un lector biometrico requiere EIPD y consentimiento reforzado | Disparo automatico desde el diagnostico (MOD-004) y desde el RAT (MOD-006), sin que ella tenga que saber de antemano que reglas aplican; Centro de Ayuda (MOD-026) contextual en cada pantalla |
| Que el consentimiento laboral se capture sin ofrecer alternativa no biometrica, debilitando su libertad | Campo obligatorio "alternativa no biometrica ofrecida" y alerta permanente si se marca "No", visible en cualquier revision posterior |
| Que el propio software termine siendo un segundo repositorio de datos biometricos | Anti-feature 9: el sistema nunca almacena la huella o el rostro, solo el registro del tratamiento, su base legal y el consentimiento |
| Que el proveedor del lector tenga acceso remoto a las plantillas sin contrato ni medidas de seguridad verificadas | Bloqueo de MOD-009 para pasar a Activo sin Contrato/DPA vigente; catalogo de controles compartido con MOD-015 |
| Que la ficha de RAT quede aprobada sin que exista realmente un control de seguridad implementado para el dispositivo | Alerta bloqueante "dato biometrico sin control de seguridad enlazado" antes de permitir el paso a Vigente |

---

## Caso 5. La empresa contrata un proveedor cloud

Fuentes principales: `03_modulos/MOD-009_ficha.md` (Proveedores y Encargados), `03_modulos/MOD-008_ficha.md` (Documentos y Politicas, Contrato/DPA y Aviso de Privacidad), `03_modulos/MOD-015_ficha.md` (Controles de Seguridad), `03_modulos/MOD-006_ficha.md` (RAT), `03_modulos/MOD-004_ficha.md` (Diagnostico, disparadores P-TEC-01 y P-TEC-03).

### Situacion de partida

Ferreteria y Suministros El Roble, S.A. de C.V. (pyme, aprox. 30 empleados) decide migrar su sistema de facturacion y contabilidad a un proveedor de servicios en la nube (un ERP/contabilidad como servicio). Karla Beatriz Hernandez Mejia, Gerente Administrativa y Financiera, ejerce a la vez los roles de Administradora de la organizacion y Delegada de Proteccion de Datos interna (perfil 1 de `05_tipos_de_usuario.md`, seccion 5.1); la ferreteria no tiene personal de TI dedicado, por lo que apoya en la evaluacion tecnica un proveedor externo de soporte informatico, actuando bajo el rol Responsable de Seguridad / IT.

### Disparador

Karla responde "Si" a P-TEC-01 ("uso de servicios en la nube") y a P-TEC-03 ("Encargados del tratamiento") en el Diagnostico (MOD-004), o bien da de alta directamente al proveedor en MOD-009 cuando firma la propuesta comercial, sin esperar a un re-diagnostico.

### Actores y modulos que intervienen

| Rol estandar | Participacion en este caso |
|---|---|
| Administrador de la organizacion | Da de alta al proveedor, gestiona el contrato y las alertas de vencimiento |
| Delegado de Proteccion de Datos (o Responsable interno) | Confirma la clasificacion del proveedor como Encargado, aprueba la activacion |
| Responsable de Seguridad / IT | Evalua el riesgo y las medidas de seguridad del proveedor (rol ejercido por soporte externo en esta pyme) |
| Responsable de area | Vincula el tratamiento del RAT que usara el nuevo sistema (por ejemplo, gestion de clientes o de nomina) |
| Aprobador | En pyme, puede coincidir con Karla (autorrevision con advertencia visible) |

| Modulo | Codigo | Papel en este caso |
|---|---|---|
| Diagnostico de Cumplimiento | MOD-004 | Detecta el uso de servicios en la nube y de encargados del tratamiento |
| RAT y Mapa de Datos | MOD-006 | Aporta el o los tratamientos a los que se vincula el proveedor |
| Proveedores y Encargados | MOD-009 | Propietario del caso: clasifica, evalua y activa al proveedor |
| Documentos y Politicas | MOD-008 | Aloja el Contrato/DPA como tipo de documento y actualiza el Aviso de Privacidad |
| Controles de Seguridad | MOD-015 | Catalogo compartido de medidas de seguridad que declara el proveedor |
| Transferencias Internacionales | MOD-010 | Recibe automaticamente el registro "pendiente de confirmar" si el pais del proveedor no es El Salvador (desarrollado en el Caso 6) |
| Centro de Tareas | MOD-021 | Aloja las tareas de evaluacion, vinculacion de contrato y revision periodica |
| Notificaciones | MOD-022 | Alertas de vencimiento de contrato y de revision |
| Calendario y Motor de Plazos | MOD-023 | Calcula la fecha de la proxima revision periodica del proveedor |
| Centro de Evidencias | MOD-019 | Recibe el expediente del proveedor con verificacion de integridad |

### Diagrama ASCII del recorrido de extremo a extremo

```
Karla (Admin/Delegada)          MOD-006          MOD-009                         MOD-008        MOD-010
      |                            |                 |                              |              |
      | responde Si a P-TEC-01/03  |                 |                              |              |
      | (MOD-004)                  |                 |                              |              |
      +---------------------------------------------->|                              |              |
      | vincula tratamiento         |<---------------|                              |              |
      | (RAT ya vigente)            |                 |                              |              |
      |                            |          [BORRADOR]                            |              |
      |                            |                 | envia a evaluacion            |              |
      |                            |                 v                              |              |
      |                            |          [EN_EVALUACION] --pais != SV--------->|-------------->|
      |                            |                 |                              |     DETECTADA_
      |     evalua riesgo y        |                 |                              |     PENDIENTE_DE_
      |     medidas de MOD-015     |                 |                              |     CONFIRMAR
      |                            |                 v                              |     (ver Caso 6)
      |                            |          [PENDIENTE_DE_CONTRATO]                |
      |                            |                 |                              |
      | genera borrador de         |                 |                              |
      | Contrato/DPA               |                 |<-----------------------------|
      +---------------------------------------------->|  vincula contrato firmado    |
      |                            |                 v                              |
      |                            |          [ACTIVO] --habilita datos de contacto->| actualiza Aviso
      |                            |                 |    del encargado             | de Privacidad
      |                            |                 |                              |
      |                            |          llega fecha de revision                |
      |                            |                 v                              |
      |                            |          [EN_REVISION] --confirma sin cambios--> vuelve a ACTIVO
      |                            |                                                |
      |                            |                                                v
      |                                                                    MOD-019 Centro de Evidencias
```

### Paso a paso

| Paso | Quien | Modulo | Que hace en el sistema | Que genera | Plazo y como se calcula | Fundamento |
|---|---|---|---|---|---|---|
| 1 | Karla | MOD-004 | Responde "Si" a P-TEC-01 (uso de la nube) y P-TEC-03 (encargados del tratamiento) | Tarea "registrar el proveedor en Proveedores y Encargados y verificar contrato/DPA vigente"; plantilla de DPA sugerida | Sin plazo legal propio; prioridad interna CRITICA | OBL-PROV-01, OBL-PROV-02, OBL-PROV-03 |
| 2 | Karla | MOD-006 | Verifica que el tratamiento que usara el nuevo sistema (por ejemplo, "Gestion de datos de clientes") ya este Vigente en el RAT; si no existe, lo completa primero | Ficha de RAT Vigente disponible para vincular | Sin plazo | OBL-DOC-02 |
| 3 | Karla | MOD-009 | Da de alta al proveedor: nombre comercial, razon social, Tipo de entidad = Encargado del tratamiento, servicio que presta, area responsable, tratamiento del RAT vinculado, pais o paises donde trata los datos (incluye donde aloja sus servidores en la nube) | Registro en Borrador; evento de auditoria "alta creada" | Sin plazo | OBL-PROV-01 (Art. 33 inc. 2) |
| 4 | Karla | MOD-009 | Envia a evaluacion (campos obligatorios de D.1 completos, incluido el pais) | Pasa a EN_EVALUACION; crea tarea para el Responsable de Seguridad/IT; si el pais es distinto de El Salvador, crea automaticamente el registro "pendiente de confirmar" en MOD-010 | Sin plazo legal propio | OBL-PROV-01; regla de deteccion automatica de MOD-009/MOD-010 |
| 5 | Responsable de Seguridad/IT (soporte externo) | MOD-009 | Completa el cuestionario de apoyo, asigna Nivel de riesgo (tipicamente Medio o Alto, por tratarse de un ERP en la nube) y declara medidas de seguridad tomadas del catalogo de MOD-015 (cifrado en transito y reposo, control de acceso, respaldos, certificaciones si el proveedor las tiene) | Evaluacion aprobada; crea tarea "vincular contrato/DPA" | Sin plazo legal propio | OBL-PROV-03 (Art. 36) |
| 6 | Aprobador (Karla, con advertencia de autorrevision en esta pyme) | MOD-009 | Aprueba la evaluacion de riesgo y seguridad | Pasa a PENDIENTE_DE_CONTRATO | Doble control exigido si el riesgo es Alto o el pais es distinto de El Salvador; en esta pyme, por debajo del umbral de 50 empleados, se permite con advertencia visible (ver Contradicciones y huecos) | OBL-PRIN-03; 05_tipos_de_usuario.md 5.4 |
| 7 | Karla | MOD-008 | Genera el borrador del Contrato/DPA desde la plantilla del sistema, lo completa con los datos del proveedor y lo envia fuera del sistema para la firma de las personas facultadas | Documento tipo Contrato/DPA en Borrador -> revision -> Aprobado; el sistema no sustituye la firma (anti-feature 17) | Sin plazo legal propio | OBL-PROV-01, OBL-PROV-02 |
| 8 | Karla | MOD-009 | Adjunta el contrato firmado con sus fechas de vigencia e inicio/vencimiento | Documento vinculado y vigente en D.3 | Sin plazo | OBL-PROV-01 |
| 9 | Aprobador | MOD-009 | Aprueba la activacion (vincular contrato/DPA y aprobar activacion) | Pasa a ACTIVO; se programa la proxima revision en MOD-023 (Anual); se habilitan los campos de contacto del encargado | El sistema bloquea el paso a ACTIVO sin documento de sometimiento vinculado y vigente | OBL-PROV-01 (Art. 33 inc. 2, bloqueo automatico) |
| 10 | Karla | MOD-008 | Actualiza el Aviso de Privacidad: agrega al proveedor a la lista de "Encargados mencionados" (literal h del Art. 24) con su nombre y contacto | El aviso pasa a REQUIERE_REVISION -> nueva version -> Publicado/Vigente; la version anterior pasa a Historico | Se dispara automaticamente al registrar o modificar un Encargado en MOD-009 sin que el aviso publicado lo liste | OBL-AVISO-02 (Art. 24 lit. h); evita la infraccion leve de OBL-PROV-04 |
| 11 | Responsable de Seguridad/IT | MOD-009 | Llegada la fecha de revision periodica (Anual, configurable), confirma que la evaluacion sigue vigente sin cambios materiales, o detecta un cambio (nuevo pais, nueva categoria de dato) | Si no hay cambios: vuelve a ACTIVO. Si hay cambios: vuelve a EN_EVALUACION conservando el historial anterior | Periodicidad configurada en D.2 (Anual/Semestral) | Buena practica; OBL-PRIN-03 |
| 12 | Sistema (automatico) | MOD-019 | Consolida el expediente del proveedor (evaluacion, contrato, aprobaciones) con verificacion de integridad | Paquete de evidencia disponible para una auditoria | Se genera con cada aprobacion o exportacion | Anti-feature 25 |

### Decisiones que el sistema NO toma

1. Si el nivel de riesgo asignado al proveedor es el correcto: el cuestionario de apoyo sugiere un nivel, pero la calificacion final la fija una persona con el rol Responsable de Seguridad/IT o Delegado (MOD-009, seccion H).
2. Si las clausulas del Contrato/DPA vinculado cumplen realmente el Art. 34 y el Art. 36: el sistema solo verifica que existe un documento vinculado, vigente y del tipo correcto (MOD-009, seccion H; anti-feature 17).
3. Si el pais donde el proveedor trata los datos tiene "nivel de proteccion adecuado" (Art. 44): la ley no atribuye esa calificacion a ningun organo y la ACE no ha publicado lista ni criterios; el sistema solo marca el registro "pendiente de confirmar" en MOD-010 (anti-feature 18, desarrollado en el Caso 6).
4. Si las instrucciones documentadas y la clausula de devolucion/eliminacion pactadas son suficientes o exigibles en el caso concreto: son RECOMENDADO (OBL-PROV-06, OBL-PROV-07), sin articulo expreso que las exija; se muestran siempre como buena practica.
5. Si el contenido del Aviso de Privacidad actualizado es juridicamente suficiente: el checklist verifica presencia de los literales del Art. 24, no la calidad juridica de la redaccion (MOD-008, seccion H).

### Alertas y escalamientos

| Alerta | Disparador | Nivel | Destinatario | Escalamiento |
|---|---|---|---|---|
| Contrato/DPA proximo a vencer (30 dias) | Faltan 30 dias para el vencimiento | WARNING | Responsable de area, Delegado | A Aprobador si faltan 7 dias sin gestion |
| Contrato/DPA proximo a vencer (7 dias) | Faltan 7 dias | HIGH | Responsable de area, Delegado, Aprobador | A Administrador si vence sin renovar |
| Contrato/DPA vencido sin renovar | Fecha de vencimiento superada | CRITICAL | Delegado, Administrador | Diaria hasta resolver |
| Proveedor activo sin evaluacion de riesgo vigente | Periodo maximo configurable superado desde la ultima evaluacion | WARNING | Delegado | Sin escalamiento adicional definido |
| Pais fuera de El Salvador sin registro vinculado en Transferencias | La creacion automatica en MOD-010 falla o el vinculo se pierde | HIGH | Delegado, Legal/Compliance | A Administrador si persiste 5 dias |
| Revision periodica vencida | Fecha de proxima revision superada sin registro nuevo | WARNING | Responsable de area, Delegado | A Aprobador a los 15 dias sin revisar |

### Evidencia resultante

- Historial completo de creacion y cambios del proveedor (quien, cuando, campo anterior y nuevo): prueba OBL-PRIN-03; vive en MOD-009 con salida al AuditLog transversal.
- Documento de sometimiento (Contrato/DPA), con version y hash de integridad: prueba OBL-PROV-01 y OBL-PROV-02; vive referenciado desde MOD-008.
- Evidencia de seguridad adjunta (certificaciones, autoevaluaciones): prueba OBL-PROV-03; vive en MOD-009.
- Aprobacion de la evaluacion de riesgo y de la activacion, con identidad y fecha: prueba OBL-PROV-02 y OBL-PROV-03.
- Datos de contacto del encargado que aparecen publicados en el aviso vigente: prueba OBL-AVISO-02 y descarta la infraccion leve de OBL-PROV-04.
- Todo lo anterior se exporta con verificacion de integridad hacia MOD-019; retencion segun la retencion documental de MOD-016 (SHOULD HAVE); mientras ese motor no este activo, MOD-009 no elimina evidencia por si solo, solo permite archivar manualmente con justificacion.

### Variantes y casos borde

- **Empresa mediana.** En Avicola San Andres (300 empleados, sobre el umbral de 50), la aprobacion de la activacion exige obligatoriamente un Aprobador distinto de quien evaluo el riesgo, sin la advertencia de autorrevision que si aplica a la ferreteria.
- **Grupo corporativo.** En Grupo Financiero Itzalco, cada sociedad (banco, aseguradora, financiera) registra su propio proveedor cloud por separado; no existe todavia una vista consolidada de proveedores a nivel de grupo (funcionalidad V1/Enterprise, decision 2.7.31 de `02_validacion_de_la_idea.md`).
- **Proveedor rechazado en la evaluacion.** Si el Responsable de Seguridad/IT o el Delegado rechazan la evaluacion (por ejemplo, el proveedor no ofrece cifrado en reposo), el registro vuelve a Borrador con el motivo documentado.
- **El proveedor subcontrata a su vez (subencargado).** Si el ERP en la nube usa a su vez otro proveedor de infraestructura, ese subencargado se registra en MOD-009 con su Encargado padre vinculado; si no tiene su propio documento de sometimiento, el sistema muestra alerta CRITICAL sin bloquear automaticamente, porque OBL-PROV-05 es una lectura extensiva del Art. 33 inc. 2 sin verificar contra un lineamiento especifico de la ACE.

### Cobertura por version

| Funcionalidad | MVP | V1 / V2 |
|---|---|---|
| Alta y ficha de Encargado, vinculacion de Contrato/DPA, workflow de aprobacion con doble control en riesgo alto | MUST HAVE | - |
| Alertas de vencimiento de contrato y de revision periodica | MUST HAVE | - |
| Datos de contacto del encargado integrados al Aviso de Privacidad | MUST HAVE | - |
| Paquete de evidencia exportable por proveedor con verificacion de integridad | MUST HAVE | - |
| Creacion automatica del registro "pendiente de confirmar" en Transferencias | SHOULD HAVE (depende de que MOD-010 exista) | Motor de deteccion automatica completo |
| Modelado de cadenas de subcontratacion (subencargados de segundo nivel) | SHOULD HAVE | - |
| Motor de scoring automatizado de riesgo de proveedores | No incluido | FUTURE |

### Riesgos especificos del caso y su mitigacion

| Riesgo | Mitigacion de diseno |
|---|---|
| Activar un proveedor sin contrato firmado | Bloqueo automatico del paso a ACTIVO sin documento de sometimiento vinculado y vigente |
| Que una pyme sin personal de TI no sepa evaluar el riesgo del proveedor | Cuestionario de apoyo simple; el rol puede recaer en el mismo Administrador o en soporte externo, con advertencia de autorrevision cuando aplique |
| Que el Aviso de Privacidad quede desactualizado tras contratar al proveedor | Automatizacion que crea la tarea de revision del aviso en cuanto se registra o modifica un Encargado sin que el aviso publicado lo mencione |
| Que se copie o centralice la base de datos completa del cliente en el registro del proveedor | El modulo solo registra metadatos del tratamiento (categorias, sistema, retencion), nunca los datos de los clientes en si (anti-feature 1 y 8) |

---

## Caso 6. Un proveedor almacena datos fuera del pais

Fuentes principales: `03_modulos/MOD-010_ficha.md` (Transferencias Internacionales, leida completa), `03_modulos/MOD-009_ficha.md` (Proveedores y Encargados), `03_modulos/MOD-024_ficha.md` (Centro Regulatorio, tramites ante la ACE), `03_modulos/MOD-007_ficha.md` (Consentimiento), `03_modulos/MOD-006_ficha.md` (RAT).

### Situacion de partida

Grupo Financiero Itzalco (corporativo con banco, aseguradora y financiera bajo una misma holding) tiene, en su sociedad aseguradora, un contrato de reaseguro con una companiia reaseguradora con sede fuera de El Salvador, a la que debe enviar periodicamente datos de polizas y siniestros de sus asegurados (identificacion y, en polizas de vida y salud, categoria de salud) para que la reaseguradora evalue y asuma su parte del riesgo por cuenta propia. Licda. Ana Gabriela Reyes Portillo, Directora de Cumplimiento Corporativo (perfil 5 de `05_tipos_de_usuario.md`, seccion 5.1), coordina el caso junto con el Delegado de Proteccion de Datos designado especificamente para la aseguradora (cada sociedad regulada del grupo mantiene su propio Delegado, en el mismo esquema que el perfil 6, Lic. Mauricio Ernesto Aguilar Sandoval, dedicado al banco).

### Disparador

Al registrar a la reaseguradora en Proveedores y Encargados (MOD-009) con Tipo de entidad = Tercero/Receptor (recibe los datos para usarlos con su propia finalidad de suscripcion de reaseguro, no siguiendo instrucciones de la aseguradora) y pais distinto de El Salvador, el sistema crea automaticamente el registro de transferencia en MOD-010 en estado DETECTADA_PENDIENTE_DE_CONFIRMAR.

### Actores y modulos que intervienen

| Rol estandar | Participacion en este caso |
|---|---|
| Responsable Legal / Compliance | Ana Gabriela Reyes Portillo: redacta y completa la evaluacion de pais, la base juridica y las salvaguardas |
| Delegado de Proteccion de Datos (o Responsable interno) | El Delegado de la aseguradora: recibe la notificacion para su informe periodico, revisa la nota de riesgo |
| Aprobador | Persona distinta de quien redacto el registro; aprueba el paso a ACTIVA (corporativo, sin excepcion de pyme) |
| Responsable de area | Area de reaseguros/suscripcion: aporta la finalidad y las categorias de datos exactas que se envian |
| Titular (formulario externo) | El asegurado, cuyo consentimiento especifico puede requerirse segun la base juridica elegida |

| Modulo | Codigo | Papel en este caso |
|---|---|---|
| Transferencias Internacionales | MOD-010 | Propietario del caso: registra, evalua y aprueba la transferencia |
| Proveedores y Encargados | MOD-009 | Registra a la reaseguradora como Tercero/Receptor y dispara la deteccion automatica |
| RAT y Mapa de Datos | MOD-006 | Aporta el tratamiento de origen (gestion de polizas y siniestros) |
| Consentimiento | MOD-007 | Vincula el consentimiento especifico del asegurado si esa es la base juridica elegida |
| Controles de Seguridad | MOD-015 | Recibe la evidencia de las salvaguardas tecnicas (cifrado en transito) |
| Centro Regulatorio | MOD-024 | Genera y tramita el borrador de puesta en conocimiento a la ACE (Art. 45) |
| Centro de Tareas | MOD-021 | Aloja las tareas de confirmacion, evaluacion y revision periodica |
| Notificaciones | MOD-022 | Alertas de la seccion siguiente |
| Calendario y Motor de Plazos | MOD-023 | Calcula la fecha de la revision periodica de la transferencia |
| Centro de Evidencias | MOD-019 | Recibe el expediente completo con verificacion de integridad |

### Diagrama ASCII del recorrido de extremo a extremo

```
MOD-009 (alta receptor,          MOD-010                              MOD-007          MOD-024
 pais != El Salvador)               |                                    |                |
      |                             |                                    |                |
      +--------------------------->[DETECTADA_PENDIENTE_DE_CONFIRMAR]    |                |
                                     |                                    |                |
                        Ana Gabriela confirma que es real                |                |
                                     v                                    |                |
                                [BORRADOR]                                |                |
                                     |                                    |                |
                        completa receptor, pais, categorias, finalidad   |                |
                        (tipo = Internacional)                            |                |
                                     v                                    |                |
                          [EN_EVALUACION_DE_PAIS]                         |                |
                                     |                                    |                |
                   cuestionario de factores del pais (sin calificar       |                |
                   "adecuado"); elige base juridica                      |                |
                                     |                                    |                |
                    base = Consentimiento previo, sin Consent vinculado -->| bloquea hasta  |
                                     |                                    | capturar Consent|
                                     |<-----------------------------------|                |
                                     v                                    |                |
                         [PENDIENTE_DE_APROBACION] --genera borrador ACEFiling------------->|
                                     |                                                      |
                        Aprobador (distinto) aprueba                                        |
                                     v                                                      |
                                 [ACTIVA] <---------------------------- notifica al Delegado |
                                     |                                    para su informe    |
                        llega fecha de revision periodica                 periodico          |
                                     v                                                       |
                          [EN_REVISION_PERIODICA] --confirma o detecta riesgo--> ACTIVA o     |
                                                                                  SUSPENDIDA   |
                                                                                               v
                                                                              [BORRADOR]->[PENDIENTE_
                                                                               DE_ENVIO]->[ENVIADO]
                                                                               (constancia de intento,
                                                                                sin canal oficial ACE)
```

### Paso a paso

| Paso | Quien | Modulo | Que hace en el sistema | Que genera | Plazo y como se calcula | Fundamento |
|---|---|---|---|---|---|---|
| 1 | Sistema (automatico) | MOD-009 / MOD-010 | Al registrar a la reaseguradora con pais distinto de El Salvador, crea el registro de transferencia en DETECTADA_PENDIENTE_DE_CONFIRMAR, con nota de riesgo visible | Tarea en MOD-021 para el area de reaseguros, con copia a Legal/Compliance; alerta WARNING | Sin plazo legal propio; recordatorio semanal mientras siga pendiente | Regla de deteccion automatica de MOD-009/MOD-010 |
| 2 | Ana Gabriela (Legal/Compliance) | MOD-010 | Confirma que es una transferencia real, completando al menos tratamiento de origen y finalidad | Pasa a BORRADOR, conservando el origen "detectada automaticamente" en el historial | A los 15 dias habiles sin confirmar, escala al Delegado | Buena practica |
| 3 | Ana Gabriela | MOD-010 | Completa receptor (heredado de MOD-009), tipo de transferencia = Internacional, pais(es) de destino, categorias de datos (identificacion, salud si aplica), finalidad | Al guardar con tipo Internacional, pasa a EN_EVALUACION_DE_PAIS | Sin plazo legal propio | OBL-TRANSF-01 (Art. 40) |
| 4 | Ana Gabriela | MOD-010 | Completa el cuestionario de evaluacion del pais receptor (existencia de ley de proteccion de datos, autoridad de control, certificaciones del reasegurador, clausulas contractuales adicionales) | Evaluacion documentada; el sistema muestra: "El sistema no decide si el pais es adecuado; esa conclusion la debe tomar su organizacion, con apoyo de asesoria legal si el caso es dudoso" | Sin plazo legal propio; alerta HIGH si el estado supera 10 dias habiles | OBL-TRANSF-03 (Art. 44 inc. 1); anti-feature 18 |
| 5 | Ana Gabriela | MOD-010 | Selecciona la base juridica: Consentimiento previo del titular (regla general) o, si aplica, la excepcion de integracion economica centroamericana (nunca preseleccionada, exige confirmacion adicional) | Si la base no es consentimiento ni la excepcion centroamericana, se muestra nota de riesgo obligatoria de reconocer antes de continuar | Sin plazo legal propio | OBL-TRANSF-04 (Art. 44 inciso final y 4) |
| 6 | Area de reaseguros (Responsable de area) | MOD-007 | Si la base elegida es Consentimiento previo, captura o vincula el consentimiento especifico del asegurado para esta transferencia internacional (distinto del consentimiento general de la poliza) | Registro Consent vinculado y vigente; si no existe, el sistema bloquea el paso a PENDIENTE_DE_APROBACION y crea la tarea "capturar consentimiento especifico" | Sin plazo legal propio | OBL-TRANSF-04 |
| 7 | Ana Gabriela | MOD-010 | Marca las salvaguardas tecnicas y contractuales (cifrado en transito SSL/TLS, clausulas contractuales de transferencia, certificacion del reasegurador) y vincula el contrato de transferencia | Al menos una salvaguarda marcada; contrato vinculado y vigente | Obligatorio antes de pasar a ACTIVA | OBL-SEG-04 (colaboradora); OBL-TRANSF-02 (Art. 41), aplicable porque el receptor es un responsable independiente (Tercero/Receptor), no un encargado (ver Contradicciones y huecos) |
| 8 | Sistema (automatico) | MOD-010 / MOD-024 | Con la evaluacion de pais, base juridica y salvaguardas completas, el registro pasa a PENDIENTE_DE_APROBACION y genera automaticamente el borrador de "puesta en conocimiento a la ACE" (ACEFiling) en MOD-024, precargado con los datos ya registrados | Registro ACEFiling en Borrador dentro de MOD-024 | Sin plazo legal definido para este tramite (el Art. 45 no fija plazo especifico) | OBL-TRANSF-05 (Art. 45) |
| 9 | Aprobador (distinto de quien redacto el registro) | MOD-010 | Aprueba el paso a ACTIVA | Se registra identidad y fecha de aprobacion; entra al Centro de Evidencias; se notifica al Delegado de la aseguradora para su informe periodico (OBL-DPO-07) | Sin excepcion de pyme en este caso: Grupo Financiero Itzalco es corporativo | OBL-PRIN-03 |
| 10 | Ana Gabriela o Administrador de la organizacion | MOD-024 | Completa el documento_adjunto y el canal_de_envio del ACEFiling, y lo envia a un segundo Responsable Legal o Aprobador para su confirmacion (doble control) | Pasa de Borrador a Pendiente_de_envio y luego a Enviado; se deja constancia del intento de cumplimiento | A los 15 dias habiles sin marcar Enviado, alerta WARNING; a los 30 dias, escala al Administrador | OBL-TRANSF-05; anti-feature 13 (la ACE aun no habilita canal oficial confirmado para este tramite) |
| 11 | Sistema (automatico) | MOD-010 | Con la periodicidad configurada (Cada 12 meses), pasa la transferencia de ACTIVA a EN_REVISION_PERIODICA | Tarea de revision en MOD-021; alerta INFO | Cada 12 meses desde la ultima confirmacion | Buena practica; OBL-TRANSF-06 (carga de la prueba continua) |
| 12 | Ana Gabriela | MOD-010 | Confirma que la transferencia sigue vigente sin cambios, o detecta un riesgo (contrato vencido, evaluacion de pais desactualizada) y la suspende hasta corregirlo | Vuelve a ACTIVA, o pasa a SUSPENDIDA con alerta CRITICAL | Evaluacion de pais desactualizada a partir de 24 meses sin actualizar (configurable) | OBL-TRANSF-03, OBL-TRANSF-06 |
| 13 | Sistema (automatico) | MOD-019 | Consolida el expediente completo (evaluacion de pais, consentimiento, contrato, ACEFiling) con verificacion de integridad | Paquete de evidencia central para sostener la carga de la prueba | Se genera al pasar a ACTIVA y en cada revision periodica cerrada | OBL-TRANSF-06 (Art. 54 inc. 2); anti-feature 25 |

### Decisiones que el sistema NO toma

1. Calificar si el pais receptor tiene "nivel de proteccion adecuado" bajo el Art. 44: el sistema muestra el cuestionario de factores y el texto "Requiere validacion de la organizacion o asesoria especializada", nunca produce una etiqueta de "pais adecuado" o "pais de riesgo" (MOD-010, seccion H; anti-feature 18).
2. Decidir si un encargado extranjero (por ejemplo, un proveedor cloud que sigue instrucciones) es una "transferencia" o solo "acceso del encargado": es una ambiguedad genuina entre el Art. 4 lit. u y los Arts. 44-45; el sistema aplica el criterio conservador (tratarlo como flujo transfronterizo) pero lo muestra siempre como decision pendiente de confirmar (MOD-010, seccion H, incertidumbre 10).
3. Decidir si aplica la excepcion de integracion economica centroamericana: no existe reglamento que la desarrolle para datos personales; el sistema no la activa nunca de forma automatica, exige marcarla expresamente.
4. Certificar que el contrato de transferencia cumple con "al menos las mismas obligaciones" del Art. 41: el sistema ofrece un checklist de clausulas usuales, pero no verifica el contenido juridico real del contrato cargado (anti-feature 17).
5. Decidir el contenido, el momento y la forma exactos de "poner en conocimiento" a la ACE (Art. 45 inc. 2), ni certificar que la ACE efectivamente lo recibio: a la fecha de este analisis la ACE no ha habilitado formulario ni procedimiento oficial (anti-feature 13).
6. Aprobar automaticamente la activacion de una transferencia internacional de datos sensibles (en este caso, datos de salud de asegurados): siempre requiere la aprobacion explicita de una persona con el rol Aprobador, dado que esa infraccion esta clasificada como muy grave (Art. 56, Art. 57).

### Alertas y escalamientos

| Alerta | Disparador | Nivel | Destinatario | Escalamiento |
|---|---|---|---|---|
| Transferencia detectada automaticamente sin confirmar | Alta de proveedor con pais distinto de El Salvador | WARNING | Responsable de area, Legal/Compliance | A los 15 dias habiles sin confirmar, escala al Delegado |
| Transferencia internacional sin evaluacion de pais completa | Estado EN_EVALUACION_DE_PAIS por mas de 10 dias habiles | HIGH | Legal/Compliance, Delegado | A los 20 dias habiles, escala al Administrador |
| Transferencia internacional sin consentimiento especifico vinculado | Base = Consentimiento previo sin Consent enlazado | HIGH | Legal/Compliance, Responsable de area | A los 10 dias habiles, escala al Delegado |
| Base juridica distinta de consentimiento sin excepcion documentada | Nota de riesgo sin justificacion adicional adjunta | HIGH | Legal/Compliance, Aprobador | Requiere cierre manual de la nota |
| Contrato de transferencia proximo a vencer / vencido | Faltan 30 dias, o venció la fecha | WARNING / CRITICAL | Legal/Compliance, Seguridad/IT, Delegado, Aprobador | A los 7 dias, escala al Aprobador; vencido, al Administrador |
| Puesta en conocimiento a la ACE pendiente de envio | Borrador en MOD-024 sin marcar como enviado, 15 dias habiles despues de creado | WARNING | Delegado | A los 30 dias habiles, escala al Administrador |
| Revision periodica vencida | Fecha de proxima revision alcanzada sin confirmar | INFO, sube a WARNING a los 15 dias | Legal/Compliance, Delegado | A los 30 dias, escala al Aprobador |
| Transferencia con evaluacion de pais desactualizada | Mas de 24 meses sin actualizar | WARNING | Legal/Compliance | A los 60 dias, escala al Delegado |

### Evidencia resultante

- Registro completo de la transferencia (tratamiento, receptor, pais, base, contrato), con fecha, hora y usuario de cada cambio: prueba OBL-TRANSF-01, OBL-TRANSF-02, OBL-TRANSF-03 y OBL-TRANSF-04; vive en MOD-010.
- Registro del estado de la puesta en conocimiento a la ACE (Borrador, Pendiente de envio, Enviado, o constancia de imposibilidad por falta de canal habilitado): prueba el intento de cumplimiento de OBL-TRANSF-05; vive en MOD-024.
- Expediente completo con todos sus adjuntos e historial de cambios: evidencia central para sostener la carga de la prueba de OBL-TRANSF-06 (Art. 54 inc. 2) ante una fiscalizacion de la ACE.
- Consentimiento especifico del asegurado vinculado, con snapshot del aviso: prueba OBL-TRANSF-04, vive en MOD-007.
- Salvaguardas tecnicas documentadas: prueba OBL-SEG-04 (colaboradora, propiedad MOD-015).
- Todo lo anterior se exporta con verificacion de integridad hacia MOD-019. Conservacion: mientras la transferencia este ACTIVA y, como minimo, 5 anos adicionales despues de pasar a FINALIZADA o DESCARTADA (criterio propuesto por el producto, por analogia con OBL-RET-05; sin norma expresa de retencion especifica para este expediente).

### Variantes y casos borde

- **El receptor es un Encargado (no un Tercero/Receptor), por ejemplo el mismo proveedor cloud del Caso 5.** Si la ferreteria de ese caso confirma que el proveedor cloud aloja los datos fuera de El Salvador, MOD-010 igual crea el registro de transferencia (criterio conservador, ver "Decisiones que el sistema NO toma", punto 2), pero el contrato exigido de forma directa por la ley para un encargado es el del Art. 33/34/36 (ya cubierto en MOD-009), no el contrato del Art. 41 (OBL-TRANSF-02), cuya propia condicion en `matriz_obligaciones.json` la excluye expresamente ("no aplica a la relacion con un encargado"). El campo "Contrato de transferencia" de MOD-010 puede entonces referenciar el mismo Contrato/DPA de MOD-009 como salvaguarda, sin que eso implique que el Art. 41 se aplique a ese caso.
- **Pyme con una persona en varios roles.** Si Ferreteria y Suministros El Roble transfiere datos a un tercero independiente fuera del pais, Karla puede redactar y evaluar el registro, pero el sistema exige que el aprobador sea distinto de quien lo redacto, salvo advertencia visible de autorrevision (unica excepcion de pyme explicita en MOD-010, seccion F).
- **Doble estado de la reforma 659.** Ninguna de las seis obligaciones propietarias de MOD-010 esta entre las 17 afectadas por la reforma; lo unico que cambia es quien recibe, por defecto, la notificacion de que la transferencia quedo ACTIVA para su informe periodico (Delegado hoy, Responsable interno en el estado FUTURO).
- **Riesgo detectado tras la aprobacion.** Si durante la revision periodica se detecta que el contrato vencio o la evaluacion de pais quedo desactualizada, la transferencia se SUSPENDE hasta corregir el riesgo, sin eliminarse ni perder su historial.
- **Cobertura parcial si MOD-010 no esta disponible en la version del producto.** El Diagnostico (MOD-004) igual detecta la senal "datos fuera de El Salvador: si" (P-TRF-01, P-TEC-02) y crea una tarea manual en el Centro de Tareas (MOD-021) para documentar la transferencia como evidencia suelta en el Centro de Evidencias (MOD-019), sin motor de deteccion automatica ni estados de workflow propios.

### Cobertura por version

MOD-010 completo es SHOULD HAVE a nivel de todo el mapa de modulos (no cubre una obligacion OBLIGATORIO con plazo ya vencido, no es dependencia estructural de otro MUST HAVE, y el Diagnostico ya detecta el caso desde el MVP sin el modulo completo).

| Funcionalidad | MVP (si el modulo se construye) | V1 / V2 |
|---|---|---|
| Registro manual de una transferencia (tratamiento, receptor, pais, base, finalidad) y workflow de aprobacion de dos pasos | SHOULD HAVE | - |
| Cuestionario de evaluacion de pais receptor y vinculacion de consentimiento especifico | SHOULD HAVE | - |
| Exportacion del expediente con verificacion de integridad | SHOULD HAVE | - |
| Deteccion automatica de transferencias no documentadas al dar de alta un proveedor extranjero | No en la version minima | COULD HAVE |
| Generacion automatica del borrador de puesta en conocimiento a la ACE (integracion con MOD-024) | No en la version minima | COULD HAVE |
| Revision periodica automatizada con calendario y alertas escalonadas | No en la version minima | COULD HAVE |
| Solicitud de opinion previa a la ACE | No incluida | FUTURE (es facultad opcional, RECOMENDADO) |
| Panel comparativo de transferencias por pais o proveedor a nivel de grupo corporativo | No incluido | FUTURE (util solo para Grupo Financiero Itzalco, Enterprise) |
| Cobertura parcial mientras el modulo no exista | Diagnostico (MOD-004, MUST HAVE) + tarea manual en MOD-021 (MUST HAVE) + evidencia suelta en MOD-019 (MUST HAVE) | Se reemplaza por el flujo completo al activarse MOD-010 |

### Riesgos especificos del caso y su mitigacion

| Riesgo | Mitigacion de diseno |
|---|---|
| Que el sistema de la impresion de estar calificando el pais receptor como "adecuado" | El cuestionario de evaluacion de pais nunca produce una etiqueta tipo "Pais adecuado" o "Pais de riesgo"; solo muestra los factores marcados y el texto de advertencia en todo momento en que se consulta |
| Tratar la excepcion de integracion centroamericana como una casilla mas, sin friccion | Nunca aparece preseleccionada, exige confirmacion explicita adicional y muestra siempre la advertencia de que no existe desarrollo reglamentario |
| Confundir el regimen de un Encargado extranjero con el de un Tercero/Receptor extranjero, aplicando el contrato o la obligacion equivocada | El campo "Rol del receptor" se hereda de MOD-009 (Encargado / Responsable independiente / Subencargado) y determina que obligaciones colaboradoras aplican; el sistema deja la clasificacion final a la organizacion cuando el caso es ambiguo |
| Que la deteccion automatica genere ruido con falsos positivos (proveedores extranjeros sin tratamiento real de datos) | La accion "Descartar" en DETECTADA_PENDIENTE_DE_CONFIRMAR es rapida (un clic mas motivo breve) y el sistema no vuelve a alertar sobre el mismo proveedor una vez descartado |
| Que la puesta en conocimiento a la ACE quede indefinidamente pendiente por falta de canal oficial habilitado | El intento documentado (fecha, documento, canal) se trata como evidencia suficiente de cumplimiento de buena fe, sin que el sistema simule una confirmacion que no existe |
| Exposicion de informacion contractual sensible del receptor (montos, penalizaciones) a roles que no la necesitan | El contrato en si vive en MOD-009 con sus propios permisos; MOD-010 solo referencia su existencia y vigencia |

---

## Contradicciones y huecos detectados

- **Archivo:** `03_modulos/MOD-004_ficha.md`, seccion G.2 (tabla de disparadores), filas P-PER-04, P-PER-05, P-PER-06 y P-EMP-01, frente a las filas P-SEN-02 y P-VID-02, y frente a `01_legal/matriz_obligaciones.json` (OBL-DOC-03). Que dice cada fuente: la fila P-PER-04 (biometria de personal, la usada en el Caso 4) etiqueta la evaluacion resultante como "EIPD recomendada", igual que P-PER-05, P-PER-06 y P-EMP-01, mientras que P-SEN-02 y P-VID-02 (datos geneticos y videovigilancia con reconocimiento facial, ambos tambien bajo la categoria de dato sensible del Art. 4 lit. g) la etiquetan como "EIPD obligatoria". `matriz_obligaciones.json` clasifica OBL-DOC-03 como OBLIGATORIO, "sin que exista umbral de riesgo definido que determine cuando es obligatoria una EIPD especifica", y MOD-006 (seccion G, regla 2) trata el disparo de biometria como automatico y no opcional. Cual se adopto y por que: en el Caso 4 se trato la EIPD como obligatoria (no meramente recomendada) para el tratamiento de biometria de personal, porque `matriz_obligaciones.json` (fuente de mayor jerarquia que la ficha de un modulo) no distingue ese supuesto de los demas disparadores de dato sensible con el mismo fundamento legal (OBL-SENS-06).
- **Archivo:** `03_modulos/MOD-009_ficha.md`, seccion F (tabla de transiciones, fila "Aprobar evaluacion de riesgo y seguridad" y automatizacion 10 de la seccion G), frente a `02_validacion/05_tipos_de_usuario.md` seccion 5.4 y frente a `03_modulos/MOD-006_ficha.md`, `MOD-010_ficha.md`, `MOD-015_ficha.md` y `MOD-016_ficha.md`. Que dice cada fuente: MOD-009 exige "doble control" (aprobador distinto de quien evaluo) cuando el riesgo es Alto o el pais es distinto de El Salvador, sin mencionar ninguna excepcion para pyme; MOD-006, MOD-010, MOD-015 y MOD-016 si repiten explicitamente, cada uno en su propia regla de separacion de funciones, la formula "salvo pyme con advertencia visible". `05_tipos_de_usuario.md` (seccion 5.4) fija el principio general: por debajo del umbral configurable de tamano (propuesta inicial 50 empleados) el sistema "no exige separacion de funciones, solo la recomienda". Cual se adopto y por que: en el Caso 5 (Ferreteria y Suministros El Roble, pyme) se permitio que Karla apruebe la activacion del proveedor cloud ella misma, con advertencia visible de autorrevision, porque `05_tipos_de_usuario.md` tiene mayor jerarquia que la ficha de un modulo especifico para las reglas de separacion de funciones, y el mismo principio ya se aplica de forma explicita en otros cuatro modulos.
- **Archivo:** `03_modulos/MOD-008_ficha.md`, seccion D (catalogo de "Tipo de documento"), frente a `03_modulos/MOD-004_ficha.md`, seccion G.2, fila P-PER-04. Que dice cada fuente: MOD-004 sugiere generar, al detectar biometria de personal, un documento llamado "Aviso especifico de biometria laboral"; el catalogo cerrado de MOD-008 solo define como tipos fijos "Politica de Proteccion de Datos, Politica de Privacidad, Aviso de Privacidad, Procedimiento ARCO-POL", con dos tipos extensibles genericos ("Plantilla interna", "Otro documento regulatorio") que el Administrador puede usar, pero ninguna ficha dice expresamente cual de los dos usar para este caso. Que se adopto: en el Caso 4 se uso el tipo extensible "Otro documento regulatorio" para el aviso especifico de biometria laboral, por ser la opcion mas cercana a un documento de cumplimiento formal (distinto de una plantilla puramente interna). **Hueco:** ninguna ficha define expresamente bajo cual de los dos tipos extensibles de MOD-008 debe crearse un aviso especifico de este tipo; se marca "hueco: no definido en la ficha de MOD-008".
- **Hueco:** ninguna ficha de modulo (MOD-006, MOD-009 ni MOD-015) define un criterio explicito para decidir si el proveedor o fabricante de un lector biometrico debe registrarse como Encargado del tratamiento en MOD-009 (por tener acceso remoto o alojar las plantillas biometricas en su nube) o si, al ser un dispositivo local sin conexion externa, no requiere registro alguno como proveedor con acceso a datos. El Caso 4 (paso 7 y 7b) resuelve el caso aplicando el criterio general del campo "Tipo de entidad" de MOD-009 (D.1), pero deja expresamente la calificacion del caso concreto a la persona responsable, marcada como decision no automatizable. Se marca "hueco: no definido de forma especifica en la ficha de MOD-009" para el caso particular de equipos biometricos.
