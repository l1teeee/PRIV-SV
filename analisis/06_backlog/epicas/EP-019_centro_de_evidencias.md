# EP-019 Centro de Evidencias (MOD-019)

**Objetivo.** Con esta epica la empresa puede ver, para cualquiera de las 105 obligaciones de la matriz, que evidencia tiene y en que estado esta (Faltante, En revision, Disponible, Vencida o Rechazada), recibir automaticamente la evidencia que ya generan los demas modulos, cargar a mano la evidencia suelta mientras un modulo aun no existe, y armar paquetes de evidencia verificables (con doble control si el destinatario es externo) para una auditoria, un requerimiento de la ACE o una due diligence, sin que el sistema declare nunca si la obligacion se cumple o no se cumple.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R2 | 14 | 61 | 21 | 40 | [MOD-019](../../03_modulos/MOD-019_ficha.md) |

**Notas de la epica.**

- El encargo pide en R1 solo tres capacidades (vista por obligacion, recepcion automatica y carga manual con aprobacion); el resto de las filas MUST HAVE de la tabla Q (informe de huecos, EvidencePackage, doble control, alertas de vigencia, control por sensibilidad, bloqueo de evidencia por caso abierto e indicadores de Dashboard) se asigna a R2. Dos de esas filas (bloqueo de evidencia; indicadores de Dashboard) no aparecen mencionadas en el resumen de la seccion 19.3 ni en la lista de indicaciones del encargo, pero si estan marcadas MUST HAVE en la tabla Q de la ficha; siguiendo la seccion 3 de las instrucciones (la tabla Q manda sobre el resumen de 19.3), esta epica las incluye igual y las ubica en R2.
- La carga manual de evidencia suelta (HU-019-04) se limita, segun el encargo, a los modulos MOD-010, MOD-014, MOD-016 y MOD-018. No se incluye MOD-012 en ese mecanismo, en linea con la seccion 19.4 del roadmap: las dos obligaciones propias de MOD-012 (OBL-DOC-04, OBL-PLAZO-04) ya quedan cubiertas de forma automatica por el formulario interno de MOD-011 (MUST HAVE), por lo que no existe alli un vacio de evidencia que MOD-019 deba llenar a mano mientras MOD-012 no exista.
- El bloqueo de evidencia por procedimiento sancionador o reclamo abierto (HU-019-12) depende tanto de MOD-024 (R1) como de MOD-011 (R2), asi que la HU completa se ubica en R2 para no partir un mismo mecanismo entre dos releases; el disparador de MOD-024 por si solo ya existiria desde R1, pero se prefiere entregar el mecanismo completo de una sola vez.
- La HU de EvidencePackage (HU-019-07) declara depende_de_modulos con EP-000 para el calculo de la huella de integridad del manifiesto, siguiendo la indicacion explicita del encargo de usar el servicio comun de EP-000; ningun documento del corpus de analisis leido para esta epica describe ese servicio en detalle, asi que esta HU asume que existe como capacidad transversal de la plataforma y no repite el calculo de hash por su cuenta.
- Se excluyen del alcance, por instruccion expresa del encargo y porque la propia tabla Q de la ficha las clasifica SHOULD HAVE o COULD HAVE: los paquetes especializados automaticos por tipo (auditoria, procedimiento sancionador, due diligence, preparacion de inspeccion) con contenido sugerido automatico, y el indicador de tiempo promedio de aprobacion de evidencia manual.
- Ninguna HU de esta epica usa las palabras cumple o no cumple, ni declara un porcentaje de cumplimiento legal; todas usan el estado de la evidencia (Faltante, En revision, Disponible, Vencida, Rechazada, Archivada) o el estado del programa (evidencia disponible, huecos abiertos, evidencia vencida), siguiendo la instruccion especifica del encargo y el anti-feature 5 de 22_anti_features.md.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-019-01 | Recibir automaticamente evidencia generada por otros modulos | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R1 | 13 | - |
| HU-019-02 | Detectar automaticamente un hueco de evidencia | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R1 | 19 | HU-019-01, MOD-004, MOD-021 |
| HU-019-03 | Consultar el catalogo de evidencia por obligacion | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R1 | 19 | HU-019-01, HU-019-02 |
| HU-019-04 | Cargar evidencia suelta manualmente | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R1 | 19 | HU-019-01 |
| HU-019-05 | Aprobar o rechazar evidencia cargada manualmente | Aprobador | 5 | R1 | 19 | HU-019-04, MOD-022, MOD-023 |
| HU-019-06 | Restringir y auditar el acceso a evidencia por nivel de sensibilidad | Responsable Legal / Compliance | 5 | R2 | 33 | HU-019-01, HU-019-03, HU-019-04 |
| HU-019-07 | Generar un paquete de evidencia con manifiesto verificable | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 8 | R2 | 33 | HU-019-01, HU-019-03, HU-019-06, EP-000, MOD-008 |
| HU-019-08 | Exigir doble control para exportar evidencia a un destinatario externo | Aprobador | 5 | R2 | 33 | HU-019-07, MOD-022, MOD-023 |
| HU-019-09 | Exportar el paquete de evidencia aprobado | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R2 | 33 | HU-019-07, HU-019-08 |
| HU-019-10 | Vencer y renovar evidencia con vigencia | Responsable de Seguridad / IT | 5 | R2 | 33 | HU-019-01 |
| HU-019-11 | Alertar sobre evidencia por vencer o vencida | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R2 | 33 | HU-019-10, MOD-022, MOD-021, MOD-023 |
| HU-019-12 | Archivar evidencia respetando el bloqueo por caso abierto | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 34 | HU-019-01, HU-019-10, MOD-024, MOD-011 |
| HU-019-13 | Generar el informe de huecos de evidencia | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R2 | 34 | HU-019-02, MOD-004, MOD-022, MOD-023 |
| HU-019-14 | Exponer los indicadores de evidencia para el Dashboard | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R2 | 34 | HU-019-02, HU-019-03, HU-019-10, HU-019-13 |

## Historias

### HU-019-01. Recibir automaticamente evidencia generada por otros modulos

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que el sistema cree automaticamente el registro de Evidencia, por referencia y en estado Disponible, cada vez que un modulo estructurado (MOD-007 a MOD-018) aprueba, cierra o publica un registro que el catalogo de tipos de evidencia clasifica como prueba de una obligacion, **para** tener organizada por obligacion, desde el primer dia, la evidencia que ya se genera en el resto del sistema, sin cargarla ni duplicarla a mano.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 13 | Si |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales); OBL-CONS-05 (Art. 54, Ley para la Proteccion de Datos Personales); OBL-INC-04 (Art. 25 inc. final, Ley para la Proteccion de Datos Personales)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que un modulo estructurado (por ejemplo MOD-007 o MOD-013) aprueba, cierra o publica un registro que el catalogo de tipos de evidencia clasifica como prueba de una obligacion, cuando el evento ocurre, entonces el sistema crea automaticamente una Evidencia en estado Disponible, con Origen del registro = Automatico y Entidad de origen enlazada al registro exacto que la origino, sin pedir ninguna accion manual.
2. Dado que la Evidencia se crea de forma automatica, cuando el modulo de origen ya calculo su propia huella de integridad (hash) del archivo, entonces el sistema la hereda tal cual, sin recalcularla ni pedir que se adjunte de nuevo.
3. Dado que una misma obligacion tiene mas de un registro de origen posible (por ejemplo, dos consentimientos distintos que prueban la misma obligacion), cuando cada uno se aprueba, entonces el sistema crea una Evidencia por cada registro de origen, sin fusionarlas ni sobrescribir una con otra.
4. Dado que se crea una Evidencia de forma automatica, cuando la creacion ocurre, entonces queda un evento en el historial (AuditLog) con el modulo de origen, el registro enlazado y la fecha, visible para el Auditor (interno).
5. Dado un registro de un modulo que no figura en el catalogo de tipos de evidencia de la seccion D.0 de la ficha (por ejemplo un evento sin valor probatorio), cuando ese registro se genera, entonces el sistema no crea ninguna Evidencia automatica para el.
6. Dado que la Evidencia ya existe por referencia para un registro de origen especifico, cuando alguien intenta cargar de nuevo el mismo archivo o dato a mano para la misma obligacion y el mismo registro, entonces el sistema no permite duplicarla y muestra la Evidencia ya existente.

**Reglas de negocio**

- La Evidencia es propiedad de MOD-019; nunca copia el Documento de MOD-008 ni administra el AuditLog, solo los referencia.
- El campo Tipo de evidencia debe coincidir con la forma declarada en el catalogo D.0 para ese modulo de origen (Registro, Archivo, Aprobacion o Log).
- Toda Evidencia automatica nace en estado Disponible, sin pasar por revision manual.

**Fuera de alcance**

- La vista consolidada por obligacion (HU aparte).
- La carga manual de evidencia cuando el modulo de origen todavia no existe en el MVP (HU aparte).

- Referencia: MOD-019 secciones D.0, D.1, F.1 (fila Faltante/ninguno -> Disponible por Automatico) y G (fila 2)
- Notas: Esta HU es la capacidad base (habilitadora) que MOD-007 a MOD-018 consumen una vez existen; no depende de que esos modulos ya esten construidos, solo deja lista la via de recepcion, segun la seccion 19.9 del roadmap.

### HU-019-02. Detectar automaticamente un hueco de evidencia

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que el sistema marque automaticamente como Faltante toda obligacion que el diagnostico confirma como aplicable y que todavia no tiene ninguna Evidencia registrada, y sugiera una tarea de carga cuando la obligacion es OBLIGATORIO, **para** saber de inmediato, sin revisar modulo por modulo, donde tengo un vacio de evidencia.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 19 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-019-01
- Modulos requeridos: MOD-004, MOD-021

**Criterios de aceptacion**

1. Dado que el diagnostico (MOD-004) confirma que una obligacion de la matriz aplica a la organizacion, cuando todavia no existe ninguna Evidencia registrada para esa obligacion, entonces el sistema crea automaticamente un registro en estado Faltante.
2. Dado que la obligacion recien marcada Faltante tiene clasificacion OBLIGATORIO, cuando se crea el registro Faltante, entonces el sistema sugiere una tarea de carga de evidencia en el Centro de Tareas (MOD-021), asignada al Responsable de area correspondiente.
3. Dado que la obligacion recien marcada Faltante tiene clasificacion RECOMENDADO o CONDICIONAL, cuando se crea el registro Faltante, entonces el sistema no sugiere ninguna tarea de forma automatica.
4. Dado que se repite el diagnostico (re-diagnostico) y el conjunto de obligaciones aplicables cambia, cuando el nuevo resultado se confirma, entonces el sistema recalcula los registros Faltante sin duplicar los que ya existian.
5. Dado que una obligacion ya tiene al menos una Evidencia en un estado distinto de Faltante, cuando el diagnostico se repite, entonces el sistema no crea un nuevo registro Faltante para esa obligacion.
6. Dado que se crea un registro Faltante, cuando la creacion ocurre, entonces queda un evento en el historial con la obligacion y la fecha en que se detecto, visible para Delegado, Responsable Legal/Compliance y Auditor.

**Reglas de negocio**

- El estado Faltante nunca lo crea una persona a mano; solo nace de la confirmacion de aplicabilidad de MOD-004.
- La tarea sugerida se pospone o se descarta desde MOD-021, sin que MOD-019 decida por la persona.

**Fuera de alcance**

- La alerta periodica de seguimiento del hueco (semanal, con escalamiento a Gerencia a los 30 dias), que se resuelve junto con el informe de huecos.

- Referencia: MOD-019 secciones F.1 (fila ninguno -> Faltante), G (fila 1) y E (fila 1)

### HU-019-03. Consultar el catalogo de evidencia por obligacion

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** consultar en una sola vista las 105 obligaciones de la matriz, cada una con el estado de su evidencia (Faltante, En revision, Disponible, Vencida o Rechazada) y la fecha de su ultima actualizacion, filtrable por modulo de origen, area o estado, **para** responder en cualquier momento, sin entrar modulo por modulo, que evidencia tengo de cada obligacion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 19 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-019-01, HU-019-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el Delegado abre la vista de evidencia por obligacion, cuando la pantalla carga, entonces se listan las 105 obligaciones de la matriz, cada una con su estado de evidencia y la fecha de ultima actualizacion.
2. Dado que una obligacion no tiene ninguna Evidencia registrada, cuando aparece en la vista, entonces su estado se muestra como Faltante, nunca como cumple, no cumple, ni con un porcentaje de cumplimiento legal.
3. Dado que el Delegado aplica un filtro por modulo de origen, por area o por estado de la evidencia, cuando el filtro se aplica, entonces la vista muestra solo las obligaciones que cumplen ese filtro.
4. Dado que un Responsable de area consulta la vista, cuando la pantalla carga, entonces solo ve la evidencia de tratamientos de su propia area, nunca la de otras areas.
5. Dado que un Responsable ARCO-POL consulta la vista, cuando la pantalla carga, entonces solo ve la evidencia de sus propios expedientes, sin poder editarla desde aqui.
6. Dado que un Usuario de consulta / Colaborador intenta abrir la vista completa del catalogo de evidencia, cuando lo intenta, entonces el sistema le niega el acceso, porque su alcance se limita a la evidencia de su propia tarea asignada.
7. Dado que se muestra el estado de una obligacion, cuando el Delegado se pregunta si la evidencia disponible alcanza para esa obligacion, entonces el sistema nunca concluye eso por si mismo y muestra el texto Requiere validacion de la organizacion o asesoria especializada junto a esa pregunta.

**Reglas de negocio**

- Los estados posibles de una Evidencia son Faltante, En revision, Disponible, Vencida, Rechazada y Archivada.
- Ningun texto de este modulo usa cumple o no cumple; el lenguaje es siempre estado de la evidencia.

**Fuera de alcance**

- El filtrado por defecto a solo obligaciones aplicables segun MOD-004 (mejora de UX que puede iterar despues).
- El informe de huecos priorizado (HU aparte).

- Referencia: MOD-019 secciones B, C, D.1 (campo Estado de la evidencia), E (fila 1), H y P (riesgo de UX)

### HU-019-04. Cargar evidencia suelta manualmente

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** cargar un archivo o registrar una referencia como evidencia suelta para una obligacion cuyo modulo estructurado (MOD-010, MOD-014, MOD-016 o MOD-018) todavia no esta activo en mi version del sistema, **para** dejar constancia de esa obligacion mientras el modulo que deberia generarla automaticamente no existe.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 19 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales); OBL-TRANSF-06 (Art. 54 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-019-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que una obligacion esta en estado Faltante porque su modulo estructurado (MOD-010, MOD-014, MOD-016 o MOD-018) todavia no esta activo, cuando el Responsable de area adjunta un archivo o registra una referencia, entonces el sistema crea la Evidencia con Origen del registro = Manual y la pasa a En revision.
2. Dado que se carga un archivo como evidencia, cuando el archivo se guarda, entonces el sistema calcula automaticamente su huella de integridad (hash) y registra la fecha de captura, sin que la persona pueda editar ninguno de los dos despues.
3. Dado que se carga evidencia manual, cuando el formulario se completa, entonces es obligatorio indicar al menos una obligacion relacionada y el nivel de sensibilidad del contenido (Sin datos personales, Datos personales de identificacion basica, Datos personales sensibles o Informacion tecnica de seguridad sensible).
4. Dado que el Responsable de area intenta guardar evidencia manual sin adjuntar archivo y sin registrar ninguna referencia, cuando lo intenta, entonces el sistema no permite guardar y senala el campo faltante.
5. Dado que se va a adjuntar el archivo, cuando se muestra el formulario de carga, entonces el sistema muestra el texto de guia: no adjunte una base de datos completa ni un listado de clientes, adjunte solo el documento puntual que prueba esta obligacion, y reemplace por una referencia cualquier dato que no sea estrictamente necesario para la prueba.
6. Dado que se completa la carga, cuando el registro se guarda, entonces queda un evento en el historial con el usuario, la fecha y el area de origen, y se notifica al Aprobador configurado.

**Reglas de negocio**

- Nunca se ofrece importacion masiva de bases de datos externas; toda carga es archivo por archivo o referencia puntual.
- El campo Entidad de origen queda vacio cuando Origen del registro = Manual.

**Fuera de alcance**

- La aprobacion o el rechazo de la evidencia cargada (HU aparte).

- Referencia: MOD-019 secciones D.1, D.2 (minimizacion de datos), F.1 (fila Faltante -> En revision, manual), L y Q
- Notas: Cubre el patron de cobertura parcial de la seccion 19.4 para MOD-010, MOD-014, MOD-016 y MOD-018, segun el alcance especifico del encargo; no incluye MOD-012 (ver notas_epica).

### HU-019-05. Aprobar o rechazar evidencia cargada manualmente

**Como** Aprobador, **quiero** aprobar o rechazar, con motivo, una evidencia que alguien cargo manualmente antes de que pase a estado Disponible, **para** que ninguna evidencia manual quede disponible sin que una persona distinta de quien la cargo la revise.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 19 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-019-04
- Modulos requeridos: MOD-022, MOD-023

**Criterios de aceptacion**

1. Dado que una Evidencia esta En revision porque se cargo manualmente, cuando el Aprobador la revisa y la aprueba, entonces el sistema la pasa a Disponible y deja la aprobacion con la identidad del Aprobador y la fecha.
2. Dado que quien carga la evidencia es la misma persona que intenta aprobarla, cuando lo intenta, entonces el sistema no lo permite, salvo que la organizacion este por debajo del umbral pyme configurado, en cuyo caso lo permite mostrando una advertencia visible de autorrevision.
3. Dado que el Aprobador rechaza una evidencia, cuando registra el rechazo, entonces es obligatorio escribir un motivo de al menos 10 caracteres, y el sistema regresa la Evidencia a Faltante mostrando ese motivo.
4. Dado que se rechaza una evidencia, cuando el rechazo se guarda, entonces el sistema notifica a quien la cargo originalmente.
5. Dado que una Evidencia cargada manualmente lleva mas de 5 dias habiles En revision sin decision, cuando se cumple ese plazo, entonces el sistema genera una alerta WARNING al Aprobador designado y al Delegado, repetida cada 3 dias, escalando al Administrador a los 10 dias habiles.
6. Dado que una Evidencia esta En revision, cuando nadie con rol Aprobador, Delegado o Responsable Legal/Compliance la ha aprobado todavia, entonces el sistema nunca la pasa a Disponible por si solo, y la accion de aprobar siempre muestra el texto Requiere validacion de la organizacion o asesoria especializada.

**Reglas de negocio**

- El aprobador debe ser distinto de quien cargo, salvo pyme con advertencia visible (05_tipos_de_usuario.md, seccion 5.4).
- El motivo de rechazo es obligatorio y de minimo 10 caracteres.

**Fuera de alcance**

- Decidir si una evidencia rechazada amerita abrir un caso en otro modulo (el sistema solo puede sugerirlo, la persona decide).

- Referencia: MOD-019 secciones C, F.1 (fila En revision -> Disponible/Faltante), H (aprobar evidencia cargada manualmente) e I

### HU-019-06. Restringir y auditar el acceso a evidencia por nivel de sensibilidad

**Como** Responsable Legal / Compliance, **quiero** que el acceso a la evidencia con datos personales sensibles o informacion tecnica de seguridad sensible se restrinja segun su nivel, y que cada lectura quede registrada, **para** minimizar el riesgo de exposicion innecesaria de datos de titulares o de informacion tecnica delicada.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 33 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-019-01, HU-019-03, HU-019-04
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que una Evidencia tiene Nivel de sensibilidad del contenido igual a Datos personales sensibles o Informacion tecnica de seguridad sensible, cuando un usuario sin necesidad de conocerla intenta abrirla, entonces el sistema le niega el acceso.
2. Dado que un Responsable de area consulta el catalogo de evidencia, cuando la evidencia pertenece a un incidente o expediente que no le fue asignado, entonces no la ve, aunque sea de su misma area.
3. Dado que alguien con permiso abre una Evidencia con Nivel de sensibilidad igual a Datos personales sensibles o Informacion tecnica de seguridad sensible, cuando la abre, entonces el sistema registra quien la consulto y cuando, visible despues para el Auditor (interno).
4. Dado que una Evidencia tiene Nivel de sensibilidad igual a Sin datos personales o Datos personales de identificacion basica, cuando se consulta, entonces el sistema no exige el registro reforzado de acceso que si exige para los dos niveles mas sensibles.
5. Dado que se carga evidencia manual o llega evidencia automatica, cuando el registro se crea, entonces el campo Nivel de sensibilidad del contenido es obligatorio desde ese momento.
6. Dado que un Auditor externo (invitado) accede al paquete de evidencia para el que fue invitado, cuando ese paquete incluye evidencia sensible fuera del alcance acordado, entonces el sistema no se la muestra.

**Reglas de negocio**

- El nivel de sensibilidad se fija al crear la Evidencia y determina desde ese momento quien puede verla, segun la tabla de permisos de la seccion C.
- El acceso de lectura a evidencia sensible siempre queda registrado, sin excepcion de rol.

**Fuera de alcance**

- La clasificacion automatica del nivel de sensibilidad por analisis de contenido (siempre la elige una persona al cargar, o la hereda el modulo de origen).

- Referencia: MOD-019 secciones C, D.1 (campo Nivel de sensibilidad del contenido), D.2 (minimizacion de datos personales), J.2 y O

### HU-019-07. Generar un paquete de evidencia con manifiesto verificable

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** elegir un tipo de paquete y unos filtros (periodo, obligacion, modulo de origen), generar un EvidencePackage en borrador con su contenido precargado y su manifiesto de integridad, y aprobarlo cuando el destinatario declarado es de uso interno, **para** reunir en un solo paquete verificable la evidencia que necesito mostrar, sin que nadie pueda alterarla despues sin que se note.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 33 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales); OBL-CONS-05 (Art. 54, Ley para la Proteccion de Datos Personales); OBL-TRANSF-06 (Art. 54 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-019-01, HU-019-03, HU-019-06
- Modulos requeridos: EP-000, MOD-008

**Criterios de aceptacion**

1. Dado que el Delegado elige un tipo de paquete (Auditoria anual, Requerimiento de la ACE, Procedimiento sancionador, Due diligence de cliente o socio, Preparacion de inspeccion o Paquete a medida) y aplica filtros de periodo, obligacion o modulo de origen, cuando confirma, entonces el sistema precarga el contenido (Evidencia y eventos de AuditLog relacionados, mas los Documentos de MOD-008 referenciados por su version exacta) en un EvidencePackage en estado Borrador.
2. Dado que el contenido se precargo, cuando el Delegado lo revisa antes de aprobar, entonces puede quitar elementos de la lista, pero el paquete debe conservar al menos un elemento para poder continuar.
3. Dado que el EvidencePackage se genera, cuando el sistema arma el manifiesto, entonces calcula, usando el servicio comun de verificacion de integridad de la plataforma (EP-000), la huella de cada archivo incluido y la huella del conjunto, sin que la persona pueda editar ese calculo.
4. Dado que el Destinatario declarado del paquete es Uso interno, cuando el Delegado, el Responsable Legal/Compliance o un Aprobador lo aprueba, entonces el sistema pasa el paquete a Aprobado y calcula ademas la firma del paquete completo.
5. Dado que el Destinatario declarado es distinto de Uso interno (ACE, Auditor externo, Cliente o socio, u Otro), cuando se intenta aprobar desde esta misma accion, entonces el sistema no lo permite y exige el segundo control.
6. Dado que se elige un tipo de paquete, cuando el contenido se precarga, entonces el sistema no sugiere ni completa automaticamente un contenido distinto del que resulta de los filtros elegidos por la persona, sin paquetes especializados automaticos por tipo.
7. Dado que un EvidencePackage no tiene ningun elemento de contenido despues de aplicar los filtros, cuando se intenta generarlo, entonces el sistema no permite pasar de Borrador y senala que no hay contenido.

**Reglas de negocio**

- Los Documentos de MOD-008 nunca se copian dentro del paquete, se referencian por version exacta.
- Un EvidencePackage nunca duplica fisicamente un archivo entre paquetes distintos.

**Fuera de alcance**

- La sugerencia automatica de contenido segun el tipo de paquete elegido (auditoria, procedimiento sancionador, due diligence, inspeccion); el usuario configura manualmente los filtros en todos los casos.
- El segundo control para destino externo y la exportacion o descarga del archivo (HU aparte).

- Referencia: MOD-019 secciones D.2, F.2 (fila nuevo -> Borrador -> Aprobado interno), K y Q (fila Paquetes especializados, excluida)
- Notas: Se excluye de forma explicita el contenido sugerido automatico por tipo de paquete (fila SHOULD HAVE de la tabla Q), siguiendo la indicacion especifica del encargo.

### HU-019-08. Exigir doble control para exportar evidencia a un destinatario externo

**Como** Aprobador, **quiero** dar el segundo control obligatorio, distinto de quien genero el paquete, antes de que un EvidencePackage con destinatario declarado externo a la organizacion quede disponible para descarga, **para** que ningun envio irreversible a la ACE, a un auditor externo o a un cliente salga sin que una segunda persona lo revise.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 33 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-019-07
- Modulos requeridos: MOD-022, MOD-023

**Criterios de aceptacion**

1. Dado que un EvidencePackage en Borrador tiene Destinatario declarado distinto de Uso interno, cuando quien lo genero lo envia a control, entonces el sistema lo pasa a Pendiente de segundo control y notifica al Aprobador designado.
2. Dado que el paquete esta Pendiente de segundo control, cuando el Aprobador designado lo aprueba, entonces el sistema lo pasa a Aprobado y calcula la firma del paquete completo, dejando constancia de la identidad de ambos aprobadores y la fecha.
3. Dado que el Aprobador designado es la misma persona que genero el paquete, cuando intenta dar el segundo control, entonces el sistema no lo permite, sin ninguna excepcion de empresa pequena para este paso.
4. Dado que el Aprobador rechaza el paquete en el segundo control, cuando registra el rechazo con motivo obligatorio, entonces el sistema regresa el paquete a Borrador y notifica a quien lo genero.
5. Dado que un paquete con destino externo lleva mas de 3 dias habiles Pendiente de segundo control, cuando se cumple ese plazo, entonces el sistema genera una alerta WARNING diaria al Aprobador designado, escalando al Administrador a los 5 dias habiles.
6. Dado que el Administrador de una organizacion pyme es quien genero el paquete y el destinatario es externo, cuando intenta aprobar el mismo el segundo control, entonces el sistema no lo permite, sin la excepcion de autorrevision que si aplica a otras aprobaciones internas del modulo.

**Reglas de negocio**

- El segundo control para destino externo no tiene excepcion de pyme, a diferencia de otras aprobaciones internas del modulo.

**Fuera de alcance**

- La exportacion o descarga del archivo ya aprobado (HU aparte).

- Referencia: MOD-019 secciones C, F.2 (fila Borrador -> Pendiente de segundo control -> Aprobado/Borrador), H (exportar sin segundo control) e I

### HU-019-09. Exportar el paquete de evidencia aprobado

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** descargar en el formato elegido (PDF, XLSX, CSV o ZIP con manifiesto) un EvidencePackage ya Aprobado, y consultar despues el historico de todas las exportaciones realizadas, **para** entregar la evidencia en el formato que necesito y poder demostrar despues cuando se exporto, quien lo hizo y a quien iba dirigida.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 33 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-019-07, HU-019-08
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que un EvidencePackage esta Aprobado y conserva su firma valida, cuando quien aprobo (o quien genero, si el destino es interno) elige el formato de exportacion y descarga el paquete, entonces el sistema lo pasa a Exportado y registra la fecha, el usuario y el destinatario declarado.
2. Dado que un paquete ya paso a Exportado, cuando alguien intenta cambiar su contenido, entonces el sistema no lo permite; cualquier cambio de alcance exige generar un paquete nuevo.
3. Dado que se completa una exportacion, cuando el evento ocurre, entonces el sistema genera una alerta INFO, una sola vez, para quien lo genero, quien lo aprobo y el Auditor (interno).
4. Dado que un Auditor (interno) o Gerencia consulta el Historico de exportaciones, cuando lo abre, entonces ve, para cada EvidencePackage exportado, la fecha, el tipo, el destinatario declarado y los aprobadores, filtrable por rango de fechas o por tipo de paquete.
5. Dado que se cumple el plazo de retencion de una exportacion, cuando el plazo se cumple, entonces el sistema pasa el paquete a Archivado de forma automatica, conservando de forma permanente el registro de que la exportacion ocurrio, aunque el archivo exportado en si quede fuera del sistema.
6. Dado que alguien intenta descargar un EvidencePackage que todavia esta en Borrador o Pendiente de segundo control, cuando lo intenta, entonces el sistema no permite la descarga.

**Reglas de negocio**

- Un paquete Exportado es terminal salvo su paso automatico a Archivado; nunca se edita.
- El registro de que una exportacion ocurrio se conserva de forma permanente.

- Preguntas pendientes relacionadas: PP-REG-07, PP-PROD-09
- Referencia: MOD-019 secciones D.2, F.2 (fila Aprobado -> Exportado -> Archivado), I (exportacion completada) y N (Historico de exportaciones)
- Notas: Los formatos PDF/XLSX/CSV/ZIP son decision de producto (PP-PROD-09); si la ACE llega a exigir un formato especifico (PP-REG-07) el generador tendria que adaptarse.

### HU-019-10. Vencer y renovar evidencia con vigencia

**Como** Responsable de Seguridad / IT, **quiero** que la evidencia con fecha de vigencia definida (por ejemplo el informe de un pentest anual) pase automaticamente a Vencida cuando se cumple esa fecha sin renovarse, y poder cargar la renovacion sin perder la version anterior, **para** que un control critico nunca quede sin respaldo probatorio vigente y sin que nadie lo note.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 33 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-019-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que una Evidencia Disponible tiene Fecha de vigencia definida, cuando esa fecha se cumple sin que se cargue una renovacion, entonces el sistema la pasa automaticamente a Vencida.
2. Dado que una Evidencia esta Disponible o Vencida y tiene Fecha de vigencia, cuando el responsable correspondiente carga una renovacion valida, entonces el sistema crea una nueva version en Disponible y conserva la version anterior como Historica, sin sobrescribirla.
3. Dado que se carga una renovacion, cuando se guarda, entonces el numero de Version solo se incrementa, nunca se reutiliza ni se borra una version previa.
4. Dado que un tipo de evidencia no tiene fecha de vigencia definida (por ejemplo un expediente ARCO-POL cerrado), cuando pasa el tiempo, entonces el sistema nunca la marca Vencida por vigencia.
5. Dado que una Evidencia pasa a Vencida, cuando el cambio ocurre, entonces queda un evento en el historial con la fecha del vencimiento, visible para Responsable Legal/Compliance y para el Auditor.
6. Dado que alguien intenta registrar una Fecha de vigencia anterior o igual a la fecha en que la evidencia se aprueba, cuando lo intenta, entonces el sistema no lo permite porque la fecha de vigencia debe ser futura al momento de aprobarse.

**Reglas de negocio**

- El contenido de una Evidencia Disponible nunca se edita; solo se renueva (nueva version) o se archiva.
- La version anterior siempre queda enlazada y consultable como Historica.

**Fuera de alcance**

- El envio de la alerta de vencimiento (HU aparte).

- Referencia: MOD-019 secciones D.1 (campos Fecha de vigencia y Version), F.1 (fila Disponible -> Vencida y renovacion) y G

### HU-019-11. Alertar sobre evidencia por vencer o vencida

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** recibir una alerta cuando falten 30 dias para que venza una evidencia con vigencia, y una alerta de mayor nivel cuando ya haya vencido, con escalamiento si nadie la renueva, **para** no depender de acordarme de revisar yo mismo cada fecha de vigencia una por una.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 33 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-019-10
- Modulos requeridos: MOD-022, MOD-021, MOD-023

**Criterios de aceptacion**

1. Dado que a una Evidencia Disponible con vigencia le faltan 30 dias para vencer, cuando se cumple ese plazo, entonces el sistema genera una alerta WARNING al responsable de carga original y al Delegado, por plataforma y correo, repetida cada 7 dias.
2. Dado que una alerta de evidencia por vencer sigue sin atenderse a los 15 dias, cuando se cumple ese plazo, entonces el sistema escala la alerta al Aprobador correspondiente.
3. Dado que una Evidencia pasa a Vencida, cuando el cambio ocurre, entonces el sistema genera una alerta HIGH al responsable de carga original, al Delegado y al Responsable Legal/Compliance, por plataforma y correo, repetida semanalmente.
4. Dado que una Evidencia sigue Vencida a los 30 dias de haber vencido, cuando se cumple ese plazo, entonces el sistema escala la alerta a Gerencia.
5. Dado que se carga y se aprueba la renovacion de una Evidencia, cuando la aprobacion se registra, entonces todas las alertas de vencimiento de esa Evidencia se apagan.
6. Dado que una Evidencia no tiene fecha de vigencia definida, cuando pasa el tiempo, entonces el sistema nunca genera para ella ninguna alerta de vencimiento.

**Reglas de negocio**

- Los dias de anticipacion de la primera alerta son configurables por la empresa; el resto del esquema de escalamiento no lo es.

- Referencia: MOD-019 seccion I (filas Evidencia por vencer y Evidencia vencida) y G

### HU-019-12. Archivar evidencia respetando el bloqueo por caso abierto

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** archivar una Evidencia cuando la obligacion que prueba deja de aplicar o el objeto que documenta se archiva en su modulo de origen, y que el sistema bloquee ese archivado mientras un procedimiento sancionador o un reclamo ante la Direccion de Proteccion de Datos siga abierto y la referencie, **para** no perder nunca la prueba de descargo que un caso abierto todavia necesita, y no eliminar evidencia por error.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 34 | No |

- Fundamento: OBL-RET-05 (Art. 47 Normativa PAS; Art. 5 lit. i LPDP (responsabilidad demostrada), Normativa para el Procedimiento Administrativo Sancionador); OBL-SANC-07 (Art. 29 D.L. 143; Art. 47 Normativa PAS, Ley de Ciberseguridad y Seguridad de la Informacion); OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-019-01, HU-019-10
- Modulos requeridos: MOD-024, MOD-011

**Criterios de aceptacion**

1. Dado que una Evidencia Disponible o Vencida corresponde a una obligacion que deja de aplicar (cambio de regimen en MOD-024) o a un objeto que se archiva en su modulo de origen, cuando eso ocurre, entonces el sistema la pasa a Archivada con confirmacion visible del Administrador, sin eliminarla nunca.
2. Dado que se abre un procedimiento sancionador (MOD-024) o un reclamo ante la Direccion de Proteccion de Datos (MOD-011) que referencia una o mas Evidencias, cuando el caso se abre, entonces el sistema marca esas Evidencias con Bloqueada = Si, sin cambiar su estado visible.
3. Dado que una Evidencia esta Bloqueada, cuando alguien, incluido el Administrador, intenta archivarla o reemplazarla, entonces el sistema no lo permite mientras el caso relacionado siga abierto, sin ninguna excepcion manual.
4. Dado que el procedimiento o el reclamo que origino el bloqueo se cierra, cuando el cierre se registra, entonces el sistema libera el campo Bloqueada de las Evidencias relacionadas.
5. Dado que se activa o se libera el campo Bloqueada, cuando el cambio ocurre, entonces queda un evento en el historial con la fecha y la referencia al expediente que lo origino.
6. Dado que una Evidencia Archivada corresponde a un expediente que se reabre, cuando la reapertura se registra, entonces el sistema la regresa a Disponible conservando intacto su historial.

**Reglas de negocio**

- Ninguna evidencia se elimina nunca, solo se archiva.
- El bloqueo no admite excepcion manual, ni siquiera del Administrador.

- Requiere validacion legal: Si
- Referencia: MOD-019 secciones D.1 (campo Bloqueada), F.1 (filas Archivada y bloqueo), G, H (archivar evidencia bloqueada) y J.2
- Notas: El horizonte de 5 anos y el bloqueo se apoyan en OBL-RET-05; la propia matriz de obligaciones clasifica esa obligacion como RECOMENDADO con la condicion expresa de que requiere validacion de abogado, por eso esta HU marca requiere_validacion_legal en true.

### HU-019-13. Generar el informe de huecos de evidencia

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** generar un informe con las obligaciones aplicables que todavia no tienen ninguna evidencia registrada, priorizado por clasificacion OBLIGATORIO primero, **para** saber en que orden atender los huecos de evidencia mas urgentes, en vez de revisarlos uno por uno.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 34 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-019-02
- Modulos requeridos: MOD-004, MOD-022, MOD-023

**Criterios de aceptacion**

1. Dado que existen obligaciones en estado Faltante, cuando el Delegado genera el informe de huecos, entonces la lista muestra primero las obligaciones OBLIGATORIO, despues las RECOMENDADO y por ultimo las CONDICIONAL.
2. Dado que se cierra el diagnostico inicial o un re-diagnostico (MOD-004), cuando el cierre ocurre, entonces el sistema recalcula automaticamente el informe de huecos sin que nadie lo pida.
3. Dado que una obligacion OBLIGATORIO aparece en el informe de huecos, cuando el hueco sigue abierto, entonces el sistema mantiene una alerta WARNING semanal al Delegado y al Responsable Legal/Compliance, escalando a Gerencia a los 30 dias.
4. Dado que una obligacion deja de estar en Faltante porque se cargo y se aprobo evidencia, o porque dejo de aplicar, cuando eso ocurre, entonces el informe de huecos deja de listarla y la alerta correspondiente se apaga.
5. Dado que el informe de huecos se exporta, cuando se genera el archivo, entonces se muestra junto con el texto Requiere validacion de la organizacion o asesoria especializada para la pregunta de si un hueco constituye por si mismo una infraccion sancionable.
6. Dado que un Usuario de consulta / Colaborador intenta generar el informe de huecos, cuando lo intenta, entonces el sistema le niega el acceso, porque el informe esta reservado a Delegado, Responsable Legal/Compliance, Aprobador y Auditor.
7. Dado que Gerencia consulta el informe de huecos, cuando lo abre, entonces ve el total de huecos por clasificacion, sin ningun porcentaje de cumplimiento legal ni las palabras cumple o no cumple.

**Reglas de negocio**

- El informe nunca declara una obligacion como incumplida, solo como sin evidencia registrada.

- Referencia: MOD-019 secciones E (fila 2), G (filas 1 y ultima), H (hueco como infraccion) e I

### HU-019-14. Exponer los indicadores de evidencia para el Dashboard

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que el Centro de Evidencias entregue al Dashboard (MOD-020) los indicadores de evidencia disponible por obligacion, huecos abiertos y evidencia vencida o por vencer, **para** que cualquier perspectiva del Dashboard pueda mostrar el estado de la evidencia sin que yo tenga que calcularlo aparte.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 34 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-019-02, HU-019-03, HU-019-10, HU-019-13
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el Dashboard (MOD-020) solicita el indicador de evidencia disponible por obligacion aplicable, cuando el Centro de Evidencias lo calcula, entonces entrega la cuenta de obligaciones aplicables con al menos una Evidencia Disponible sobre el total de obligaciones aplicables, sin usar la palabra cumplimiento ni un porcentaje etiquetado como legal.
2. Dado que cambia el estado de cualquier Evidence, cuando el cambio se guarda, entonces los indicadores de evidencia disponible, huecos abiertos y evidencia vencida o por vencer se recalculan antes de la siguiente consulta del Dashboard.
3. Dado que la perspectiva Gerencia del Dashboard consulta el indicador, cuando lo muestra, entonces no ve el detalle por obligacion, solo el semaforo con el texto evidencia disponible.
4. Dado que la perspectiva Legal/Delegado o Auditor del Dashboard consulta el indicador, cuando lo muestra, entonces ve el detalle completo por obligacion, no solo el semaforo.
5. Dado que existe al menos una obligacion OBLIGATORIO en estado Faltante, cuando se calcula el semaforo de evidencia disponible, entonces el resultado es rojo, nunca verde ni amarillo.
6. Dado que se calcula cualquiera de estos indicadores, cuando el resultado se muestra en pantalla, entonces siempre aparece junto al texto de descargo estandar del sistema sobre que el indicador mide el estado del programa, no una declaracion de cumplimiento legal.

**Reglas de negocio**

- MOD-020 es de solo lectura sobre estos indicadores; MOD-019 nunca consulta ni depende de MOD-020 para calcularlos.

**Fuera de alcance**

- El tiempo promedio de aprobacion de evidencia manual como indicador (funcionalidad COULD HAVE, fuera del MVP).

- Preguntas pendientes relacionadas: PP-UX-05
- Referencia: MOD-019 secciones E (fila 5), M y P (riesgo legal)

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Vista "que evidencia tenemos de esta obligacion" por las 105 obligaciones, con estados Faltante/En revision/Disponible/Vencida/Rechazada | HU-019-03 |
| Recepcion automatica de evidencia por referencia desde MOD-007 a MOD-018 (segun cada modulo se active) | HU-019-01 |
| Informe de huecos de evidencia, priorizado por clasificacion OBLIGATORIO | HU-019-13 |
| Carga manual de evidencia suelta con aprobacion (para cubrir modulos SHOULD HAVE aun no activos) | HU-019-04, HU-019-05 |
| EvidencePackage con manifiesto y verificacion de integridad, destino interno | HU-019-07 |
| Doble control obligatorio para exportacion con destino externo | HU-019-08 |
| Alertas de evidencia vencida o por renovar (por ejemplo, pentest anual) | HU-019-10, HU-019-11 |
| Bloqueo de evidencia vinculada a un procedimiento o reclamo abierto | HU-019-12 |
| Indicadores de dashboard (evidencia disponible, huecos, vencimientos) integrados en MOD-020 | HU-019-14 |
