# EP-011 ARCO-POL (MOD-011)

**Objetivo.** La empresa puede recibir, verificar, clasificar, resolver y conservar como evidencia toda solicitud de los siete derechos ARCO-POL de un titular dentro de los seis plazos legales que aplican, sin que el sistema apruebe ni deniegue nunca por su cuenta.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R2 | 20 | 104 | 0 | 104 | [MOD-011](../../03_modulos/MOD-011_ficha.md) |

**Notas de la epica.**

- Se siguen las 16 filas MUST HAVE de la tabla Q de la ficha MOD-011 (formulario interno seguro, carga de los 7 formularios oficiales de la ACE, verificacion de identidad de los 3 tipos de solicitante, sub-flujo NNA, prevencion unica con archivo automatico, plazo maestro 20+20 con una sola prorroga, rama de incompetencia, rama de notificacion a receptores con fallback manual, bloqueo cautelar de rectificacion, denegatoria motivada con las 8 causales y notificacion en 3 dias, gratuidad y tabla de costos, informe de acceso sin datos de terceros, portabilidad condicionada, motor de plazos compartido con MOD-023, aprobador segun el doble estado de MOD-002/MOD-024, y evidencia exportable con verificacion de integridad). No se detecto ninguna discrepancia entre esa tabla Q y el bullet de MOD-011 en la seccion 19.3 del roadmap: ambos describen exactamente la misma version minima vendible.
- La fila de la tabla Q Reclamo del titular ante la Direccion de Proteccion de Datos (registro + informe de actuaciones) esta marcada SHOULD HAVE en su columna principal, pero la propia justificacion de esa fila y el parrafo de version minima vendible de la seccion Q, mas el criterio 4 de la seccion 19.6 del roadmap, dicen de forma expresa que el registro basico como texto libre (fecha y contenido) entra en el MVP sin retrasar el lanzamiento, dejando solo la plantilla dedicada del informe de actuaciones para V1. Siguiendo esa indicacion, que ademas el encargo pide de forma explicita, se agrego HU-011-20 para cubrir unicamente ese registro basico; la plantilla estructurada del informe de actuaciones queda fuera de esta epica.
- El formulario interno seguro de HU-011-01 cubre, ademas de las obligaciones propias de MOD-011, las dos obligaciones propietarias de MOD-012 Portal del Titular (OBL-DOC-04 y OBL-PLAZO-04, mecanismos de ejercicio de derechos): la ficha de MOD-011 (seccion L.2) y el roadmap (seccion 19.4) documentan que, mientras MOD-012 no exista en el MVP, ese formulario interno ya satisface ambas obligaciones sin dejar vacio legal.
- HU-011-15 (cerrar el expediente) deja constancia expresa de que ningun rol puede eliminar un expediente Cerrado o Archivado ni su historial: esta es la cobertura pasiva que la seccion 19.4 del roadmap asigna a MOD-011 para una de las obligaciones de MOD-016 Retencion y Eliminacion (los expedientes cerrados se conservan sin borrado por defecto, sin motor de retencion con catalogo sectorial propio).
- Las filas Motor de plazos compartido (consulta a MOD-023) y Doble estado 659: aprobador por defecto segun MOD-002/MOD-024 son transversales a casi todo el modulo, no una pantalla propia: la primera se cubre repartida entre todas las HU que calculan un plazo legal (HU-011-06, 07, 08, 09, 13 y 14, todas via MOD-023); la segunda se resuelve en una unica HU temprana, HU-011-05, que las HU de aprobacion (07, 08, 12, 13) consumen despues.
- Ninguna HU de esta epica resuelve por si sola una solicitud: reconocer o denegar siempre exige la aprobacion explicita del Delegado o Responsable interno (y de un segundo revisor Aprobador cuando hay datos sensibles o riesgo de reclamo ante la ACE), conforme a la anti-feature 7 y a la decision 2.7.22; esto se refleja como criterio negativo explicito en HU-011-07, 08, 11, 12 y 13.
- Quedan fuera de esta epica, por ser SHOULD HAVE, COULD HAVE o FUTURE en la tabla Q: la plantilla dedicada del informe de actuaciones (SHOULD HAVE, salvo el registro basico de HU-011-20), la deteccion automatica de solicitudes masivas o abusivas y de duplicados (COULD HAVE, solo alertas ya descritas en la ficha como fuera de alcance del MVP) y el portal publico con autoregistro del titular (FUTURE, pertenece a MOD-012).
- Todas las HU quedan en release R2, tal como indica el encargo: la secuencia recomendada de la seccion 19.9 del roadmap ubica MOD-011 despues de MOD-006, MOD-007, MOD-008, MOD-009, MOD-015 y MOD-013, y sus dependencias de infraestructura (MOD-002, MOD-023, MOD-024, MOD-021, MOD-022, MOD-019) ya existen desde R1.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-011-01 | Registrar una solicitud ARCO-POL con los datos comunes y los campos especificos del derecho ejercido | Responsable ARCO-POL / Responsable del tramite | 5 | R2 | 23 | MOD-001 |
| HU-011-02 | Cargar un formulario oficial ARCO-POL de la ACE ya diligenciado | Responsable ARCO-POL / Responsable del tramite | 3 | R2 | 27 | HU-011-01 |
| HU-011-03 | Verificar la identidad y la legitimacion del solicitante segun su tipo | Responsable ARCO-POL / Responsable del tramite | 5 | R2 | 23 | HU-011-01 |
| HU-011-04 | Activar el sub-flujo de titular nina, nino o adolescente | Responsable ARCO-POL / Responsable del tramite | 3 | R2 | 27 | HU-011-01, MOD-007 |
| HU-011-05 | Determinar el aprobador por defecto de los actos atribuidos al Delegado | Administrador de la organizacion | 5 | R2 | 23 | MOD-002, MOD-024 |
| HU-011-06 | Admitir automaticamente la solicitud cuando el checklist del Art. 18 esta completo | Responsable ARCO-POL / Responsable del tramite | 5 | R2 | 23 | HU-011-01, HU-011-03, MOD-023, MOD-021 |
| HU-011-07 | Prevenir la solicitud incompleta y archivarla automaticamente si no se subsana | Responsable ARCO-POL / Responsable del tramite | 8 | R2 | 27 | HU-011-01, HU-011-03, HU-011-05, MOD-023, MOD-021, MOD-022 |
| HU-011-08 | Declarar y notificar la incompetencia dentro de 5 dias habiles | Responsable ARCO-POL / Responsable del tramite | 5 | R2 | 27 | HU-011-06, HU-011-05, MOD-023, MOD-021, MOD-022 |
| HU-011-09 | Prorrogar una sola vez el plazo general por causa justificada | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 27 | HU-011-06, MOD-023 |
| HU-011-10 | Activar y liberar el bloqueo cautelar del dato durante la rectificacion | Responsable ARCO-POL / Responsable del tramite | 5 | R2 | 27 | HU-011-06, MOD-006 |
| HU-011-11 | Analizar la procedencia de la solicitud aplicando el checklist tasado de causales | Responsable ARCO-POL / Responsable del tramite | 8 | R2 | 28 | HU-011-06, MOD-006, MOD-016 |
| HU-011-12 | Aprobar y emitir el reconocimiento del derecho ejercido | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 28 | HU-011-11, HU-011-05, MOD-021, MOD-009 |
| HU-011-13 | Redactar, revisar y notificar la denegatoria motivada dentro de 3 dias habiles | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 8 | R2 | 28 | HU-011-11, HU-011-05, MOD-023, MOD-022 |
| HU-011-14 | Notificar a los receptores de los datos dentro de 5 dias habiles | Responsable ARCO-POL / Responsable del tramite | 8 | R2 | 28 | HU-011-12, MOD-023, MOD-009, MOD-021 |
| HU-011-15 | Cerrar el expediente y conservarlo sin posibilidad de borrado | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 28 | HU-011-12, HU-011-13, HU-011-14, MOD-021, MOD-016 |
| HU-011-16 | Aplicar la gratuidad y la tabla de costos de reproduccion o envio | Responsable ARCO-POL / Responsable del tramite | 3 | R2 | 27 | HU-011-01, MOD-008 |
| HU-011-17 | Generar el informe de acceso filtrando los datos de terceros | Responsable ARCO-POL / Responsable del tramite | 5 | R2 | 29 | HU-011-06, MOD-006, MOD-009 |
| HU-011-18 | Habilitar la portabilidad condicionada a la base de consentimiento y al tratamiento automatizado | Responsable ARCO-POL / Responsable del tramite | 5 | R2 | 29 | HU-011-11, MOD-006 |
| HU-011-19 | Exportar el expediente o el paquete de evidencia con verificacion de integridad | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 29 | HU-011-15, MOD-019 |
| HU-011-20 | Registrar el reclamo del titular ante la Direccion de Proteccion de Datos como texto libre | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R2 | 29 | HU-011-15, MOD-021, MOD-024 |

## Historias

### HU-011-01. Registrar una solicitud ARCO-POL con los datos comunes y los campos especificos del derecho ejercido

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** registrar en el formulario interno seguro los datos de la entidad, del solicitante, del derecho ejercido y de la forma de entrega de la respuesta, incluidos los campos propios del derecho seleccionado, sin importar por que canal llego la solicitud, **para** abrir un expediente unico y completo desde el primer contacto, tal como exige el Art. 18 de la LPDP.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 23 | Si |

- Fundamento: OBL-ARCO-08 (Art. 18, Ley para la Proteccion de Datos Personales); OBL-ARCO-01 (Art. 6, Ley para la Proteccion de Datos Personales); OBL-DOC-04 (Art. 61 inc. 2, Ley para la Proteccion de Datos Personales); OBL-PLAZO-04 (Art. 61 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: -
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado que el Responsable ARCO-POL abre una nueva solicitud, cuando el sistema la crea, entonces precarga sin poder editarse el nombre o razon social, el domicilio y el correo de contacto de la entidad responsable desde el modulo Organizacion (MOD-001) y genera un numero de expediente unico con el formato ARCO-[ANIO]-[correlativo].
2. Dado que se completan el nombre del solicitante, su domicilio, el derecho que ejerce y la descripcion de los datos y elementos para localizarlos, cuando el Responsable ARCO-POL guarda el formulario, entonces el expediente pasa al estado Nueva o Recibida con fecha y hora de recepcion y queda un evento en el historial con usuario y fecha.
3. Dado que se selecciona el derecho Rectificacion, cuando se completa la seccion de campos especificos, entonces el sistema exige el campo dato a corregir y valor propuesto antes de permitir avanzar; si se selecciona Cancelacion, exige elegir una causal de la lista tasada de siete opciones y, si elige Otro, exige ademas un texto libre.
4. Dado que se selecciona el derecho Oposicion, cuando se completa el formulario, entonces el sistema exige el motivo de la oposicion y pregunta si se trata de oposicion a mercadotecnia directa o perfilado; si la respuesta es si, el sistema deja registrada esa marca para conectarla despues con la lista de supresion de MOD-007.
5. Dado que la solicitud llego por correo electronico, WhatsApp o de forma presencial, cuando el Responsable ARCO-POL la traslada al formulario interno, entonces el sistema exige adjuntar la captura o transcripcion del mensaje original como evidencia y registra que el plazo corre desde la fecha de recepcion efectiva, no desde la fecha de captura en el sistema.
6. Dado que la empresa habilito el enlace publico del formulario interno seguro, cuando el Titular lo completa y lo envia el mismo sin crear una cuenta, entonces el sistema crea el expediente de la misma forma que si lo hubiera registrado el Responsable ARCO-POL, marcando el canal de recepcion como Formulario interno.
7. Dado que falta el nombre completo del solicitante, la descripcion de los datos o el derecho ejercido, cuando el Responsable ARCO-POL intenta guardar el formulario, entonces el sistema bloquea el guardado y senala los campos obligatorios pendientes sin crear el expediente.

**Reglas de negocio**

- Los cuatro campos de la entidad responsable (D.1) se precargan siempre desde MOD-001 y no se capturan de nuevo por cada solicitud.
- El area que trata los datos y la referencia al Tratamiento del RAT son opcionales y solo ayudan a localizar el dato, nunca sustituyen ni duplican el RAT de MOD-006.
- El formulario interno seguro es, junto con la carga de los formularios oficiales de la ACE (ver HU-011-02), el unico canal del MVP: no existe autoregistro del titular con cuenta persistente, eso pertenece a MOD-012 (SHOULD HAVE).
- El sistema no copia la base de datos completa del cliente para tramitar la solicitud: solo guarda los datos que el propio titular aporta y la referencia al Tratamiento del RAT, nunca una copia del sistema de origen.

**Fuera de alcance**

- Verificacion de identidad y de legitimacion del solicitante (ver HU-011-03).
- Carga de un formulario oficial de la ACE ya diligenciado (ver HU-011-02).
- Evaluacion del checklist de los 7 elementos del Art. 18 y paso a Admitida o Prevenida (ver HU-011-06 y HU-011-07).
- Portal publico con autoregistro y consulta de estado del titular, MOD-012 SHOULD HAVE, fuera del MVP.

- Requiere contenido: Textos de ayuda de cada campo del formulario interno (D.1 a D.10), en lenguaje simple, validados por la organizacion antes de publicarse.
- Preguntas pendientes relacionadas: PP-PROD-06
- Referencia: MOD-011 secciones D.1, D.2, D.6, D.7, D.8, D.9, D.10, F.2 fila ninguno a Nueva/Recibida, F.3 fila Solicitud por WhatsApp/correo/presencial
- Notas: Cubre la fila MUST HAVE Formulario interno seguro con los 7 elementos del Art. 18 de la tabla Q, y cubre de forma parcial las obligaciones propias de MOD-012 (OBL-DOC-04 y OBL-PLAZO-04).

### HU-011-02. Cargar un formulario oficial ARCO-POL de la ACE ya diligenciado

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** adjuntar directamente uno de los 7 formularios oficiales ARCO-POL de la ACE que el titular ya lleno, y que el sistema mapee sus campos a la misma estructura del expediente, **para** aceptar sin poder rechazarlo el formulario oficial que el titular elija usar, tal como exige el Art. 32 de los Lineamientos DPO.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 27 | No |

- Fundamento: OBL-ARCO-15 (Art. 32, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-011-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el titular presento uno de los 7 formularios oficiales ARCO-POL de la ACE version 07-07-2025 ya diligenciado, cuando el Responsable ARCO-POL lo adjunta en el campo Formulario oficial de la ACE adjunto, entonces el sistema acepta el archivo en formato PDF o imagen y no exige llenar de nuevo los mismos campos ya cubiertos por ese formulario.
2. Dado que se adjunta un formulario oficial de la ACE, cuando el sistema lo procesa, entonces mapea sus campos equivalentes de identificacion del solicitante, tipo de legitimacion, derecho ejercido y descripcion de los datos a los campos de D.2, D.6 y D.7 del expediente, dejando visible en el expediente cual de los 7 formularios oficiales se uso.
3. Dado que el formulario oficial adjunto no trae algun campo obligatorio del Art. 18, cuando el Responsable ARCO-POL revisa el expediente, entonces el sistema marca ese elemento como pendiente en el checklist de la seccion Evaluando requisitos del Art. 18, igual que si faltara en el formulario interno.
4. Dado un archivo que no tiene formato PDF o imagen, cuando el Responsable ARCO-POL intenta cargarlo como formulario oficial de la ACE, entonces el sistema rechaza el archivo y muestra el motivo del rechazo sin crear el expediente.
5. Dado un formulario oficial de la ACE cargado, cuando el sistema lo guarda, entonces conserva el archivo original sin modificarlo, con hash de integridad, disponible para el paquete de evidencia exportable.

**Reglas de negocio**

- Los 7 formularios oficiales de la ACE no son modificables por la empresa: deben aceptarse tal cual, aunque la empresa tenga su propio formulario interno (OBL-ARCO-15).
- El expediente creado a partir de un formulario oficial sigue exactamente el mismo workflow de la seccion F que uno creado desde el formulario interno: esta HU solo cubre la carga y el mapeo de campos, no un flujo distinto.

**Fuera de alcance**

- Edicion del contenido de los formularios oficiales de la ACE: el sistema solo los acepta y los mapea, nunca los modifica.
- Verificacion de identidad del solicitante (ver HU-011-03).

- Requiere contenido: Los 7 formularios oficiales ARCO-POL de la ACE version 07-07-2025, con el mapeo de cada campo oficial al campo interno equivalente, validado por Legal.
- Referencia: MOD-011 secciones D introduccion, D.6 fila Formulario oficial de la ACE adjunto, K

### HU-011-03. Verificar la identidad y la legitimacion del solicitante segun su tipo

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** verificar si quien presenta la solicitud es el propio titular, un representante o apoderado, o un heredero o sucesor, exigiendo en cada caso los documentos que acreditan esa calidad, **para** confirmar la legitimacion antes de tramitar cualquier derecho, tal como exige el Art. 6 de la LPDP.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 23 | Si |

- Fundamento: OBL-ARCO-01 (Art. 6, Ley para la Proteccion de Datos Personales)
- Depende de: HU-011-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un expediente en estado Nueva o Recibida con el tipo de solicitante marcado como Titular, cuando el Responsable ARCO-POL adjunta el documento de identidad del solicitante en formato imagen o PDF y confirma la verificacion, entonces el expediente pasa a Verificando identidad y luego a Evaluando requisitos Art. 18, con un evento de auditoria que registra usuario y fecha.
2. Dado que el tipo de solicitante es Representante legal o apoderado, cuando el Responsable ARCO-POL intenta avanzar sin el documento de poder de representacion con facultades especiales, entonces el sistema bloquea el avance y exige ese documento antes de continuar.
3. Dado que el tipo de solicitante es Heredero o sucesor de un titular fallecido, cuando el Responsable ARCO-POL intenta avanzar sin la certificacion de partida de defuncion o sin el documento que acredite el vinculo familiar o la calidad de heredero, entonces el sistema bloquea el avance hasta que ambos documentos esten adjuntos.
4. Dado que el canal usado no permite ningun medio de verificacion de identidad reconocido y no existe firma ni medio equivalente, cuando el Responsable ARCO-POL lo confirma, entonces el expediente pasa al estado Verificacion fallida o Anonima con una advertencia visible, sin archivarse automaticamente, quedando la decision de como proceder a criterio del Responsable ARCO-POL.
5. Dado que la solicitud se presento desde un canal digital verificado por la empresa, por ejemplo el correo previamente registrado del titular en un sistema propio, cuando no hay firma fisica, entonces el sistema acepta la marca de aceptacion electronica como medio equivalente reconocido, sin exigir firma escaneada.
6. Dado un documento de identidad, poder o partida adjunto a la verificacion, cuando cualquier usuario con permiso lo consulta, entonces el sistema registra en el historial quien lo vio y cuando, y ese acceso queda restringido a los roles Responsable ARCO-POL y Delegado o Responsable interno.
7. Dado un rol distinto de Responsable ARCO-POL, por ejemplo Responsable de area o Colaborador, cuando intenta verificar identidad o adjuntar un documento de legitimacion, entonces el sistema deniega la accion.

**Reglas de negocio**

- Ninguna solicitud se admite sin al menos un mecanismo de verificacion aplicado segun el canal usado, con advertencia visible cuando la verificacion no fue completa (anti-feature 20).
- El acceso a los adjuntos de identidad esta restringido a Responsable ARCO-POL y Delegado o Responsable interno, nunca visible para Colaboradores o Responsables de area.
- El derecho se ejerce en nombre del titular fallecido segun el Art. 6: no crea un derecho propio del heredero sobre datos ajenos.

**Fuera de alcance**

- Verificacion biometrica o cualquier confirmacion tecnica de que el documento de identidad corresponde a quien lo presenta: la confirmacion sustantiva queda a criterio humano del Responsable ARCO-POL.
- Sub-flujo de titular NNA (ver HU-011-04).

- Referencia: MOD-011 secciones D.2, D.3, D.4, F.1, F.2 filas Nueva/Recibida a Verificando identidad y Verificando identidad a Verificacion fallida/Evaluando requisitos, F.3 filas Solicitud anonima y Solicitud sin firma, J

### HU-011-04. Activar el sub-flujo de titular nina, nino o adolescente

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** marcar que la solicitud es sobre los datos de una nina, nino o adolescente y que el sistema exija los documentos y muestre el aviso de tension normativa correspondientes, **para** atender la solicitud sin omitir el consentimiento parental que exige la ley y sin ocultar la incertidumbre juridica sobre la edad.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 27 | No |

- Fundamento: OBL-CONS-06 (Art. 56 lit. c num. 3, en relacion con Art. 5 lit. j y Art. 42, Ley para la Proteccion de Datos Personales); OBL-PRIN-04 (Art. 5 lit. j), Ley para la Proteccion de Datos Personales)
- Depende de: HU-011-01
- Modulos requeridos: MOD-007

**Criterios de aceptacion**

1. Dado que se marca Si en Los datos corresponden a un titular de ninez o adolescencia, cuando el Responsable ARCO-POL guarda el formulario, entonces el sistema exige la certificacion de partida de nacimiento del titular y el nombre del progenitor, representante o tutor que consiente o solicita, antes de permitir avanzar a Verificando identidad.
2. Dado que la marca de NNA esta activa, cuando se muestra el expediente, entonces el sistema despliega siempre el banner de solo lectura sobre la tension entre la LPDP (consentimiento parental) y la Ley Crecer Juntos (adolescentes de 12 a 18 anos pueden autorizar ciertas publicaciones de su imagen), con el texto Requiere validacion de la organizacion o asesoria especializada, sin permitir editarlo ni ocultarlo.
3. Dado que la marca de NNA esta activa, cuando el sistema evalua el expediente, entonces lo vincula al sub-flujo de consentimiento parental de MOD-007 sin fijar automaticamente ninguna regla de edad para decidir si el adolescente puede actuar por si mismo.
4. Dado que se adjunta el carne de minoridad, cuando el Responsable ARCO-POL lo carga, entonces el sistema lo guarda como documento opcional adicional sin exigirlo para avanzar.
5. Dado que la marca de NNA esta activa y falta la partida de nacimiento o el nombre del progenitor, representante o tutor, cuando el Responsable ARCO-POL intenta pasar a Verificando identidad, entonces el sistema bloquea el avance y senala los dos campos pendientes.

**Reglas de negocio**

- El sistema nunca decide por si mismo si un titular adolescente de 12 a 18 anos puede ejercer un derecho ARCO-POL sin consentimiento parental: muestra ambas normas y deja la decision marcada como pendiente de criterio juridico.
- La activacion del sub-flujo NNA no cambia el workflow general de la seccion F: solo agrega los campos y el aviso de esta HU antes de continuar con la verificacion de identidad.

**Fuera de alcance**

- Definicion de una edad numerica fija para el consentimiento del adolescente: queda pendiente de asesoria legal (PP-JUR-05), y el sistema mantiene siempre disponible el flujo parental completo como opcion conservadora.
- Ejecucion del consentimiento parental en si: eso ocurre dentro de MOD-007.

- Requiere contenido: Texto legal exacto del banner de tension normativa NNA, validado por Legal.
- Requiere validacion legal: Si (PP-JUR-05)
- Referencia: MOD-011 secciones D.2, D.5, G regla 9

### HU-011-05. Determinar el aprobador por defecto de los actos atribuidos al Delegado

**Como** Administrador de la organizacion, **quiero** que el sistema determine, para cada acto que la ley atribuye hoy a la figura del Delegado, quien debe aprobarlo segun el estado ACTUAL o FUTURO vigente en MOD-024 y el tipo de rol configurado en MOD-002, **para** que la prevencion, la incompetencia, la resolucion final y la notificacion a receptores siempre tengan un aprobador valido, incluso el dia que cambie el regimen de la reforma 659.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 23 | Si |

- Fundamento: OBL-ARCO-01 (Art. 6, Ley para la Proteccion de Datos Personales); OBL-ARCO-08 (Art. 18, Ley para la Proteccion de Datos Personales); OBL-ARCO-10 (Art. 20, Ley para la Proteccion de Datos Personales); OBL-ARCO-11 (Art. 21 inc. 3, Ley para la Proteccion de Datos Personales); OBL-ARCO-14 (Art. 33 inc. 4, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: -
- Modulos requeridos: MOD-002, MOD-024

**Criterios de aceptacion**

1. Dado que la bandera regimen_reforma_659 de MOD-024 esta en ACTUAL, cuando el sistema necesita resolver quien aprueba una prevencion, una incompetencia, una resolucion final o una notificacion a receptores, entonces asigna como aprobador por defecto a la persona con el rol Delegado de Proteccion de Datos registrada en MOD-002.
2. Dado que la bandera regimen_reforma_659 cambia de ACTUAL a FUTURO, cuando se crea un expediente nuevo despues del cambio, entonces el sistema asigna como aprobador por defecto a la persona con el rol Responsable interno vigente en MOD-002, sin exigir que esa persona tenga certificacion ante la ACE.
3. Dado un expediente que ya estaba en curso o ya cerrado cuando la bandera cambio de ACTUAL a FUTURO, cuando el sistema evalua quien debe aprobar sus actos pendientes, entonces conserva la regla que estaba vigente al momento de tramitarse, sin recalcularla de forma retroactiva.
4. Dado que Responsable ARCO-POL y Delegado o Responsable interno recaen en la misma persona ocupando dos roles del sistema, cuando esa persona redacta y luego intenta aprobar el mismo borrador, entonces el sistema exige una segunda confirmacion explicita, separada del guardado del borrador, con advertencia visible de autorrevision.
5. Dado que una solicitud involucra datos sensibles o existe riesgo de reclamo ante la Direccion de Proteccion de Datos de la ACE, cuando el Delegado o Responsable interno revisa una denegatoria, entonces el sistema permite escalar la decision a un segundo revisor con el rol Aprobador antes de notificar al titular.
6. Dado un usuario sin el rol Delegado, Responsable interno ni Aprobador, cuando intenta aprobar y emitir una prevencion, una incompetencia, una resolucion final o una notificacion a receptores, entonces el sistema deniega la accion.

**Reglas de negocio**

- Quien redacta un borrador de prevencion, incompetencia, denegatoria o notificacion nunca es quien lo aprueba y emite, sin excepcion, incluso en pyme donde ambos roles recaigan en la misma persona fisica.
- El Auditor, interno o externo, es siempre de solo lectura y nunca puede coincidir con quien carga evidencia o aprueba una accion en el mismo expediente que audita.
- El cambio de bandera de MOD-024 nunca ocurre por la sola aprobacion legislativa: solo se activa tras confirmacion manual del equipo del producto (anti-feature 14).

**Fuera de alcance**

- Activacion o reversion de la bandera regimen_reforma_659 en si: eso ocurre en MOD-024.
- Decidir si la empresa mantiene voluntariamente al Delegado bajo el estado FUTURO: eso ocurre en MOD-002.

- Referencia: MOD-011 secciones C separacion de funciones, G regla 14, Doble estado de la reforma 659: efecto especifico sobre este modulo
- Notas: Cubre la fila MUST HAVE Doble estado 659: aprobador por defecto segun MOD-002/MOD-024. Se ubica al inicio de la epica, antes de las HU que requieren aprobacion, porque todas ellas consumen esta regla.

### HU-011-06. Admitir automaticamente la solicitud cuando el checklist del Art. 18 esta completo

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** que el sistema evalue automaticamente el checklist de los 7 elementos del Art. 18 apenas la identidad esta verificada, y que arranque el plazo general apenas la solicitud queda completa, **para** empezar a contar el plazo legal desde el momento correcto y no depender de un calculo manual.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 23 | Si |

- Fundamento: OBL-ARCO-08 (Art. 18, Ley para la Proteccion de Datos Personales); OBL-ARCO-10 (Art. 20, Ley para la Proteccion de Datos Personales)
- Depende de: HU-011-01, HU-011-03
- Modulos requeridos: MOD-023, MOD-021

**Criterios de aceptacion**

1. Dado un expediente en Evaluando requisitos Art. 18, cuando todos los campos obligatorios de D.6 y D.7 estan presentes, entonces el sistema lo marca como checklist completo, lo pasa automaticamente a Admitida y pide a MOD-023 el calculo del plazo de 20 dias habiles desde esa fecha.
2. Dado que un expediente pasa a Admitida, cuando el sistema completa la transicion, entonces crea en MOD-021 la tarea Resolver solicitud con fecha limite igual al plazo calculado por MOD-023, asignada por defecto al Responsable ARCO-POL del expediente.
3. Dado el checklist de los 7 elementos del Art. 18, cuando el Responsable ARCO-POL abre el expediente en cualquier momento antes de Admitida, entonces el sistema muestra la marca de cumplido o pendiente de cada uno de los 7 elementos, recalculada con cada edicion.
4. Dado que faltan 5 dias habiles del plazo de 20, o de la prorroga vigente, cuando el sistema evalua las alertas, entonces genera la alerta HIGH Plazo general proximo a vencer al Responsable ARCO-POL y al Delegado o Responsable interno, y la escala a Administrador si faltan 2 dias habiles.
5. Dado que se cumplen los 20 dias habiles, o los 40 con prorroga, sin resolucion, cuando el sistema lo detecta, entonces genera la alerta CRITICAL Plazo general vencido a Delegado o Responsable interno y a Administrador, y ese vencimiento queda registrado de forma permanente en el historial aunque el expediente se cierre despues.
6. Dado que el calendario de dias habiles del ano en curso no esta configurado en MOD-023, cuando el Responsable ARCO-POL intenta admitir una solicitud, entonces el sistema bloquea la admision y muestra la alerta correspondiente.

**Reglas de negocio**

- El plazo legal de 20 dias habiles nunca se calcula dentro de este modulo: siempre se solicita a MOD-023.
- El plazo de admision no es configurable por la empresa; si lo es a quien se asigna por defecto la tarea generada.

**Fuera de alcance**

- Generacion del borrador de prevencion cuando el checklist esta incompleto (ver HU-011-07).
- Prorroga del plazo general (ver HU-011-09).

- Preguntas pendientes relacionadas: PP-JUR-02
- Referencia: MOD-011 secciones E, F.2 filas Evaluando requisitos Art. 18 a Admitida, G reglas 1, 4 y 8, I filas Plazo general proximo a vencer y Plazo general vencido
- Notas: Cubre, junto con HU-011-09, la fila MUST HAVE Plazo general 20+20 dias habiles con una sola prorroga, y cubre en parte la fila MUST HAVE Motor de plazos compartido (consulta a MOD-023).

### HU-011-07. Prevenir la solicitud incompleta y archivarla automaticamente si no se subsana

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** generar el borrador de prevencion cuando falte alguno de los 7 elementos del Art. 18, que el Delegado o Responsable interno lo apruebe y emita, dar 10 dias habiles para subsanar, y que el expediente se archive solo si vence sin subsanacion, **para** cumplir la unica oportunidad de subsanacion que exige la ley antes de poder archivar una solicitud incompleta.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 27 | No |

- Fundamento: OBL-ARCO-08 (Art. 18, Ley para la Proteccion de Datos Personales)
- Depende de: HU-011-01, HU-011-03, HU-011-05
- Modulos requeridos: MOD-023, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado un expediente en Evaluando requisitos Art. 18 al que le falta uno o mas de los 7 elementos, cuando el sistema evalua el checklist, entonces genera el borrador de prevencion con la lista de elementos faltantes y pasa el expediente a Prevenida.
2. Dado un borrador de prevencion listo, cuando el Delegado o Responsable interno lo aprueba y lo emite, entonces el sistema notifica al titular, arranca el contador de 10 dias habiles calculado por MOD-023 y registra el evento de aprobacion por separado de quien redacto el borrador.
3. Dado un expediente en Prevenida, cuando el titular aporta la documentacion o el dato faltante antes de vencer los 10 dias habiles, entonces el contador de 10 dias se detiene, el expediente vuelve a Evaluando requisitos Art. 18, y el computo del plazo general de 20 dias habiles sigue corriendo sin suspenderse, mostrando siempre el texto de advertencia de que la ley no precisa si la prevencion suspende ese plazo y de que el sistema aplica por defecto el criterio mas conservador, remitiendo a asesoria legal si el caso es critico.
4. Dado un expediente en Prevenida, cuando se cumplen los 10 dias habiles sin ninguna subsanacion registrada, entonces el sistema archiva automaticamente el expediente en el estado terminal Archivada, notifica al Responsable ARCO-POL y al Delegado o Responsable interno, y deja evidencia del archivo automatico.
5. Dado un expediente Archivado por falta de subsanacion, cuando el titular quiere continuar el tramite, entonces el sistema no permite reabrir ese expediente: el titular debe presentar una solicitud nueva con un numero de expediente distinto.
6. Dado que faltan 3 dias habiles de los 10, cuando el sistema evalua las alertas, entonces genera la alerta WARNING Prevencion proxima a vencer al Responsable ARCO-POL, escalandola al Delegado o Responsable interno si falta 1 dia habil.
7. Dado un borrador de prevencion, cuando el Responsable ARCO-POL intenta aprobarlo y emitirlo el mismo, entonces el sistema deniega la accion porque quien redacta el borrador nunca es quien lo aprueba y emite.

**Reglas de negocio**

- El plazo de 10 dias habiles no es configurable; si lo es el texto adicional que el Responsable ARCO-POL puede agregar al borrador.
- Un expediente Archivado es terminal: no admite edicion de los campos de fondo, solo anotaciones nuevas y el plazo de retencion.

**Fuera de alcance**

- Redaccion del contenido legal exacto de la plantilla de prevencion: eso es contenido validado por la organizacion.

- Requiere contenido: Plantilla de prevencion validada por la organizacion, ficha MOD-011 seccion K.
- Requiere validacion legal: Si (PP-JUR-04)
- Referencia: MOD-011 secciones E, F.2 filas Evaluando requisitos Art. 18 a Prevenida y Prevenida a Evaluando/Archivada, F.3, G reglas 2 y 3, H prevencion suspende o no el plazo, I fila Prevencion proxima a vencer
- Notas: Cubre la fila MUST HAVE Prevencion unica con archivo automatico. Cierra el vacio de plazo transitorio ya vencido OBL-PLAZO-04 (23-may-2025), por lo que es prioritaria dentro de la epica.

### HU-011-08. Declarar y notificar la incompetencia dentro de 5 dias habiles

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** declarar que la empresa no es competente sobre los datos solicitados, redactar el borrador de devolucion motivada, y que el Delegado o Responsable interno lo apruebe y notifique al titular dentro de 5 dias habiles, **para** devolver correctamente al titular una solicitud que no corresponde a esta empresa, sin dejarla sin respuesta.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 27 | No |

- Fundamento: OBL-ARCO-09 (Art. 19, Ley para la Proteccion de Datos Personales)
- Depende de: HU-011-06, HU-011-05
- Modulos requeridos: MOD-023, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado un expediente en Admitida, cuando el Responsable ARCO-POL determina que la empresa no trata los datos solicitados y redacta el borrador de devolucion motivada, entonces el expediente pasa a Declarada incompetente y el sistema pide a MOD-023 el calculo del plazo de 5 dias habiles desde esa declaracion.
2. Dado un borrador de devolucion listo, cuando el Delegado o Responsable interno lo aprueba y lo emite dentro de los 5 dias habiles, entonces el sistema notifica al titular, el expediente pasa al estado terminal Devuelta al titular, y el evento queda registrado para el reporte de cumplimiento de plazos.
3. Dado que faltan dias de los 5 habiles para devolver, cuando el sistema evalua las alertas, entonces genera la alerta WARNING Incompetencia pendiente de devolver al Responsable ARCO-POL, escalandola al Delegado o Responsable interno si falta 1 dia habil.
4. Dado un expediente en estado Devuelta al titular, cuando cualquier usuario intenta reabrirlo o editar sus campos de fondo, entonces el sistema lo impide porque es un estado terminal.
5. Dado un borrador de devolucion, cuando el mismo Responsable ARCO-POL que lo redacto intenta aprobarlo y emitirlo, entonces el sistema deniega la accion por la regla de separacion de funciones.

**Reglas de negocio**

- El plazo de 5 dias habiles para devolver por incompetencia no es configurable.
- La devolucion motivada por incompetencia orienta al titular, sin que el sistema decida por si mismo si la empresa es o no competente: esa determinacion la hace el Responsable ARCO-POL con criterio humano.

**Fuera de alcance**

- Redaccion del contenido legal exacto de la plantilla de devolucion: contenido validado por la organizacion.

- Requiere contenido: Plantilla de devolucion motivada por incompetencia, validada por la organizacion.
- Referencia: MOD-011 secciones E, F.2 filas Admitida a Declarada incompetente y Declarada incompetente a Devuelta al titular, G regla 7, I fila Incompetencia pendiente de devolver
- Notas: Cubre la fila MUST HAVE Rama de incompetencia (5 dias habiles).

### HU-011-09. Prorrogar una sola vez el plazo general por causa justificada

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** prorrogar el plazo general de 20 dias habiles hasta 20 dias habiles adicionales, dejando registrada la causa justificada, y que el sistema impida una segunda prorroga sobre el mismo expediente, **para** disponer del tiempo adicional que la ley permite sin perder el control del plazo maximo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 27 | No |

- Fundamento: OBL-ARCO-10 (Art. 20, Ley para la Proteccion de Datos Personales)
- Depende de: HU-011-06
- Modulos requeridos: MOD-023

**Criterios de aceptacion**

1. Dado un expediente Admitida sin prorroga previa, cuando el Delegado o Responsable interno registra la causa justificada y solicita la prorroga, entonces el sistema pide a MOD-023 el recalculo del plazo hasta 20 dias habiles adicionales y deja constancia de la causa, la fecha y quien la autorizo.
2. Dado un expediente que ya tiene una prorroga registrada, cuando el Delegado o Responsable interno intenta solicitar una segunda prorroga sobre el mismo expediente, entonces el sistema la deniega porque solo se permite una prorroga.
3. Dado que se registra una prorroga, cuando el sistema recalcula la fecha limite, entonces actualiza la alerta de Plazo general proximo a vencer para que se dispare sobre la nueva fecha, sin reiniciar el conteo de los dias habiles ya corridos.
4. Dado un rol distinto de Delegado o Responsable interno, por ejemplo Responsable ARCO-POL, cuando intenta registrar una prorroga, entonces el sistema deniega la accion.
5. Dado que se registra una prorroga, cuando el sistema completa el registro, entonces queda un evento de auditoria distinto del resto del historial del expediente, con la causa justificada visible para el Auditor.

**Reglas de negocio**

- La prorroga es de hasta 20 dias habiles adicionales, nunca de un plazo distinto ni acumulable mas de una vez.
- El plazo prorrogado sigue calculandose por MOD-023, nunca dentro de este modulo.

**Fuera de alcance**

- Definicion de que cuenta como causa justificada suficiente: queda a criterio del Delegado o Responsable interno, sin catalogo tasado en la ley.

- Referencia: MOD-011 secciones A tabla OBL-ARCO-10, F.1 arranca el plazo de 20 dias habiles, I fila Plazo general proximo a vencer
- Notas: Cubre, junto con HU-011-06, la fila MUST HAVE Plazo general 20+20 dias habiles con una sola prorroga.

### HU-011-10. Activar y liberar el bloqueo cautelar del dato durante la rectificacion

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** que el sistema active automaticamente un bloqueo cautelar sobre la referencia al dato cuando se analiza una solicitud de rectificacion, y que lo libere al reconocerse el derecho o al cerrarse el expediente, **para** cumplir la proteccion que el Art. 9 exige para el titular mientras dura la verificacion del cambio.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 27 | No |

- Fundamento: OBL-ARCO-03 (Art. 9, Ley para la Proteccion de Datos Personales)
- Depende de: HU-011-06
- Modulos requeridos: MOD-006

**Criterios de aceptacion**

1. Dado un expediente de Rectificacion que pasa de Admitida a En analisis de procedencia, cuando el sistema completa la transicion, entonces activa automaticamente el bloqueo cautelar sobre la referencia al Tratamiento del RAT vinculada al expediente y registra la fecha de activacion.
2. Dado un bloqueo cautelar activo, cuando el Delegado o Responsable interno aprueba el reconocimiento de la rectificacion, entonces el sistema libera automaticamente el bloqueo y registra la fecha de liberacion.
3. Dado un bloqueo cautelar activo, cuando el expediente se cierra o se archiva por cualquier via, entonces el sistema libera el bloqueo como parte del cierre, sin dejarlo activo de forma indefinida.
4. Dado que el dato sigue bloqueado despues de vencer el plazo de 20 mas 20 dias habiles sin resolucion, cuando el sistema lo detecta, entonces genera la alerta HIGH Bloqueo cautelar activo por mas del plazo general al Delegado o Responsable interno y al Responsable de area, escalando a Administrador.
5. Dado un expediente que no es de Rectificacion, por ejemplo Cancelacion u Oposicion, cuando pasa a En analisis de procedencia, entonces el sistema no activa ningun bloqueo cautelar automatico, porque esa medida solo esta definida para la rectificacion.

**Reglas de negocio**

- El bloqueo cautelar aplica exclusivamente a solicitudes de Rectificacion: no existe una regla equivalente documentada para cancelacion u olvido.
- La activacion y la liberacion del bloqueo quedan registradas con fecha, como evidencia disponible para el Auditor.

**Fuera de alcance**

- Definir una regla de bloqueo cautelar para cancelacion u olvido: no esta prevista en la ficha y no se inventa aqui.

- Referencia: MOD-011 secciones E fila Constancia de bloqueo cautelar, F.2 fila Admitida a En analisis de procedencia, I fila Bloqueo cautelar activo por mas del plazo general, J
- Notas: Cubre la fila MUST HAVE Bloqueo cautelar durante rectificacion. El Caso 8 de 08c_workflows_casos_07_08.md documenta explicitamente que este bloqueo no existe para cancelacion ni olvido; esta HU respeta ese limite y no lo extiende.

### HU-011-11. Analizar la procedencia de la solicitud aplicando el checklist tasado de causales

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** aplicar, segun el derecho ejercido, el checklist de causales de procedencia e improcedencia que la ley ya tasa, y dejar registrada la decision de reconocer o de denegar para que una persona la apruebe despues, **para** no resolver nunca por cuenta propia si la solicitud procede, dejando esa decision a criterio humano.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 28 | No |

- Fundamento: OBL-ARCO-04 (Art. 10, Ley para la Proteccion de Datos Personales); OBL-ARCO-05 (Art. 12, Ley para la Proteccion de Datos Personales); OBL-ARCO-06 (Art. 13, Ley para la Proteccion de Datos Personales)
- Depende de: HU-011-06
- Modulos requeridos: MOD-006, MOD-016

**Criterios de aceptacion**

1. Dado un expediente de Cancelacion en En analisis de procedencia, cuando el Responsable ARCO-POL revisa el caso, entonces el sistema muestra las 7 causales tasadas de procedencia y los 6 supuestos tasados de improcedencia del Art. 10, sin marcar por si mismo cual aplica, y exige que una persona seleccione la conclusion antes de continuar.
2. Dado un expediente de Oposicion en En analisis de procedencia, cuando el Responsable ARCO-POL lo revisa, entonces el sistema muestra el texto Requiere validacion de la organizacion o asesoria especializada junto a la ponderacion de interes legitimo prevalente, sin calcular ni sugerir un resultado.
3. Dado un expediente de Limitacion en En analisis de procedencia, cuando el Responsable ARCO-POL lo revisa, entonces el sistema muestra los 4 supuestos tasados del Art. 13 para que se seleccione el que corresponde, sin decidir automaticamente.
4. Dado un expediente de Cancelacion u Olvido cuyo Tratamiento vinculado tiene, segun MOD-016, un dato en estado retenido por obligacion, cuando el Responsable ARCO-POL abre el analisis de procedencia, entonces el sistema precarga el borrador de denegatoria parcial motivada que genera MOD-016 con el fundamento de retencion, para que el Responsable ARCO-POL lo revise antes de la aprobacion del Delegado.
5. Dado que el Responsable ARCO-POL concluye que la solicitud procede, cuando registra esa conclusion, entonces el expediente pasa a Pendiente de aprobar reconocimiento; si concluye que no procede o corresponde denegar, debe seleccionar una de las 8 causales tasadas del Art. 22 antes de que el expediente pase a Pendiente de aprobar denegatoria.
6. Dado un expediente de Cancelacion por datos disociados, cuando el Responsable ARCO-POL marca esa causal de improcedencia, entonces el sistema exige una confirmacion humana explicita de que la disociacion es efectiva e irreversible antes de aceptarla.
7. Dado que el Responsable ARCO-POL intenta guardar la conclusion de procedencia o improcedencia sin haber completado el checklist de causales correspondiente al derecho ejercido, entonces el sistema bloquea el guardado.

**Reglas de negocio**

- El sistema nunca decide por si mismo si una causal de cancelacion, oposicion, limitacion o denegatoria aplica a un caso concreto: presenta el checklist tasado y deja la ponderacion a una persona (anti-feature 6, seccion H).
- El contador de 3 dias habiles de la denegatoria arranca cuando se aprueba la decision, no cuando se redacta este analisis (ver HU-011-13).

**Fuera de alcance**

- Aprobacion y emision del reconocimiento (ver HU-011-12) o de la denegatoria (ver HU-011-13).
- Verificacion de la base juridica y del caracter automatizado del tratamiento para portabilidad (ver HU-011-18).

- Requiere validacion legal: Si
- Referencia: MOD-011 secciones D.7, F.2 fila En analisis de procedencia a Pendiente de aprobar reconocimiento/denegatoria, F.3 fila Datos disociados, H
- Notas: Cubre parte de la fila MUST HAVE Denegatoria motivada con las 8 causales tasadas (la parte de analisis; la aprobacion y notificacion viven en HU-011-13). Usa el Caso 8 de 08c_workflows_casos_07_08.md, denegatoria parcial de cancelacion por dato retenido en MOD-016, como criterio de aceptacion 4.

### HU-011-12. Aprobar y emitir el reconocimiento del derecho ejercido

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** aprobar el reconocimiento del derecho que el Responsable ARCO-POL analizo como procedente, y que el sistema ejecute la accion derivada y notifique al titular, **para** que ninguna resolucion favorable salga hacia el titular sin una aprobacion humana explicita.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 28 | No |

- Fundamento: OBL-ARCO-04 (Art. 10, Ley para la Proteccion de Datos Personales); OBL-ARCO-05 (Art. 12, Ley para la Proteccion de Datos Personales); OBL-ARCO-06 (Art. 13, Ley para la Proteccion de Datos Personales); OBL-ARCO-07 (Art. 14, Ley para la Proteccion de Datos Personales)
- Depende de: HU-011-11, HU-011-05
- Modulos requeridos: MOD-021, MOD-009

**Criterios de aceptacion**

1. Dado un expediente en Pendiente de aprobar reconocimiento, cuando el Delegado o Responsable interno aprueba de forma explicita, entonces el expediente pasa a Reconocida, se ejecuta la accion correspondiente, por ejemplo crear en MOD-021 la tarea de eliminacion o de correccion en el area responsable, y se libera el bloqueo cautelar si estaba activo.
2. Dado un expediente en Reconocida, cuando el sistema verifica si el dato ya fue transferido a un receptor previo segun MOD-009 o MOD-010, entonces pasa a Notificando a receptores si existe al menos un receptor vinculado, o a Cerrada si no existe ninguno.
3. Dado un borrador de reconocimiento, cuando el mismo Responsable ARCO-POL que lo redacto intenta aprobarlo, entonces el sistema deniega la accion por la regla de separacion de funciones.
4. Dado un expediente en Pendiente de aprobar reconocimiento, cuando el Delegado o Responsable interno rechaza el borrador en vez de aprobarlo, entonces el expediente vuelve a En analisis de procedencia con el motivo del rechazo registrado, sin considerarse emitido ningun acto.
5. Dado que se aprueba y emite un reconocimiento, cuando el sistema completa el registro, entonces queda un evento de aprobacion con identidad y fecha, distinto del evento de redaccion del borrador, disponible para el Auditor.

**Reglas de negocio**

- El sistema calcula el plazo, presenta las causales tasadas y prepara el borrador; el Delegado o Responsable interno decide y aprueba antes de que cualquier acto se considere emitido (anti-feature 7).
- La ejecucion de la accion derivada nunca implica que este modulo copie o retenga mas datos del sistema de origen que la referencia necesaria para localizar y ejecutar la accion.

**Fuera de alcance**

- Redaccion del contenido del borrador de reconocimiento: se hereda del analisis de procedencia de HU-011-11.

- Referencia: MOD-011 secciones F.2 filas Pendiente de aprobar reconocimiento a Reconocida y Reconocida a Notificando a receptores/Cerrada, O

### HU-011-13. Redactar, revisar y notificar la denegatoria motivada dentro de 3 dias habiles

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** aprobar la denegatoria motivada con la causal tasada seleccionada y sus pruebas, escalarla a un segundo revisor cuando hay datos sensibles o riesgo de reclamo ante la ACE, y notificarla al titular dentro de 3 dias habiles, **para** no denegar nunca una solicitud sin motivacion ni fuera de las 8 causales que permite el Art. 22.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 28 | No |

- Fundamento: OBL-ARCO-12 (Art. 22, Ley para la Proteccion de Datos Personales)
- Depende de: HU-011-11, HU-011-05
- Modulos requeridos: MOD-023, MOD-022

**Criterios de aceptacion**

1. Dado un expediente en Pendiente de aprobar denegatoria con una de las 8 causales tasadas del Art. 22 seleccionada, cuando el Delegado o Responsable interno la aprueba, entonces el expediente pasa a Denegada y el sistema pide a MOD-023 el calculo del plazo de 3 dias habiles desde esa aprobacion, no desde la redaccion del borrador.
2. Dado un expediente con datos sensibles o riesgo de reclamo ante la Direccion de Proteccion de Datos de la ACE, cuando el Delegado o Responsable interno revisa la denegatoria, entonces el sistema exige la aprobacion adicional de un segundo revisor con el rol Aprobador antes de que la denegatoria pueda notificarse.
3. Dado un expediente en Denegada, cuando el Delegado o Responsable interno lo notifica al titular por el medio que este senalo dentro de los 3 dias habiles, entonces el expediente pasa a Cerrada con la fecha de cierre registrada.
4. Dado que faltan dias de los 3 habiles para notificar, cuando el sistema evalua las alertas, entonces genera la alerta HIGH Denegatoria pendiente de notificar al Responsable ARCO-POL, escalandola al Delegado o Responsable interno en el ultimo dia habil.
5. Dado un borrador de denegatoria sin ninguna de las 8 causales tasadas seleccionada, cuando el Delegado o Responsable interno intenta aprobarlo, entonces el sistema bloquea la aprobacion.
6. Dado que el mismo Responsable ARCO-POL que redacto el borrador de denegatoria intenta aprobarlo, entonces el sistema deniega la accion por la regla de separacion de funciones.
7. Dado un expediente denegado en empresa a partir del tamano mediano, cuando el segundo revisor Aprobador rechaza la denegatoria, entonces el expediente vuelve a En analisis de procedencia con el motivo del rechazo registrado.

**Reglas de negocio**

- Denegar sin motivacion o fuera de las 8 causales tasadas es infraccion muy grave segun el catalogo del Art. 56.
- El contador de 3 dias habiles arranca al aprobarse la decision de denegar, nunca al iniciarse el borrador.

**Fuera de alcance**

- Redaccion del contenido del borrador de denegatoria: se hereda del analisis de procedencia de HU-011-11.

- Requiere contenido: Plantilla de denegatoria motivada, validada por la organizacion.
- Requiere validacion legal: Si
- Referencia: MOD-011 secciones C separacion de funciones y segundo revisor, F.2 filas En analisis de procedencia a Pendiente de aprobar denegatoria y Pendiente de aprobar denegatoria a Denegada/Cerrada, G regla 6, I fila Denegatoria pendiente de notificar
- Notas: Cubre, junto con HU-011-11, la fila MUST HAVE Denegatoria motivada con las 8 causales tasadas y notificacion en 3 dias habiles. Usa el Caso 8 de 08c_workflows_casos_07_08.md, segundo revisor por riesgo de reclamo ante la ACE al invocar retencion sectorial, como base del criterio 2.

### HU-011-14. Notificar a los receptores de los datos dentro de 5 dias habiles

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** generar automaticamente la lista de receptores a notificar cuando existe un registro de transferencia o de encargado vinculado, y ejecutar cada notificacion dentro de 5 dias habiles, con una tarea manual cuando no exista ese registro formal, **para** que la rectificacion, la cancelacion o el olvido reconocidos sean efectivos tambien fuera de la empresa.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 28 | No |

- Fundamento: OBL-ARCO-11 (Art. 21 inc. 3, Ley para la Proteccion de Datos Personales)
- Depende de: HU-011-12
- Modulos requeridos: MOD-023, MOD-009, MOD-021

**Criterios de aceptacion**

1. Dado un expediente de Rectificacion, Cancelacion u Olvido que pasa a Reconocida y que tiene un registro de transferencia o de Tercero-Receptor vinculado al Tratamiento en MOD-009 o en MOD-010, cuando el sistema completa la transicion, entonces genera automaticamente la lista de receptores a notificar y pide a MOD-023 el calculo de 5 dias habiles por cada receptor.
2. Dado la lista de receptores generada, cuando el Responsable ARCO-POL ejecuta la notificacion de cada uno dentro del plazo, entonces el sistema deja evidencia de la notificacion individual de cada receptor, con fecha, y cierra esa lista solo cuando todos quedan notificados.
3. Dado que MOD-010 Transferencias Internacionales no esta activo o no existe un registro formal de transferencia para el Tratamiento, cuando el sistema no puede identificar automaticamente a un receptor extranjero, entonces crea en MOD-021 una tarea manual para que el Responsable ARCO-POL identifique a los receptores, sin bloquear el resto del expediente.
4. Dado que no es claro si un encargado, por ejemplo un proveedor de nube, cuenta como receptor a notificar bajo el Art. 21 inciso 3, cuando el sistema construye la lista, entonces aplica por defecto el criterio conservador de tratarlo como receptor, dejando la decision final ajustable por una persona con una nota de riesgo visible.
5. Dado que faltan 2 dias habiles de los 5, cuando el sistema evalua las alertas, entonces genera la alerta WARNING Notificacion a receptores pendiente al Responsable ARCO-POL, escalandola al Delegado o Responsable interno si falta 1 dia habil.
6. Dado que todos los receptores de la lista quedan notificados, cuando el sistema lo detecta, entonces pasa automaticamente el expediente a Cerrada.

**Reglas de negocio**

- El plazo de 5 dias habiles por receptor no es configurable.
- El sistema no decide de forma definitiva y sin posibilidad de ajuste si un encargado extranjero es o no receptor: aplica el criterio conservador por defecto y lo deja siempre visible como ajustable.

**Fuera de alcance**

- Confirmacion de que un encargado extranjero cuenta legalmente como receptor: queda como decision humana ajustable (seccion H).
- Motor de deteccion automatica completo de transferencias internacionales: pertenece a MOD-010 (SHOULD HAVE).

- Requiere contenido: Plantilla de notificacion a receptores, validada por la organizacion.
- Requiere validacion legal: Si (PP-MAPA-05)
- Referencia: MOD-011 secciones E fila Notificacion a receptores, F.2 fila Reconocida a Notificando a receptores, G regla 5, H encargado extranjero como receptor, I fila Notificacion a receptores pendiente, L.2 nota final punto 1
- Notas: Cubre la fila MUST HAVE Rama de notificacion a receptores (5 dias habiles), con fallback manual si MOD-010 aun no esta completo, tal como exige el encargo. Usa el Caso 8 de 08c_workflows_casos_07_08.md, notificacion al proveedor de hosting tras el reconocimiento del olvido, para el criterio 1.

### HU-011-15. Cerrar el expediente y conservarlo sin posibilidad de borrado

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** cerrar el expediente cuando se agotan todas sus ramas activas, marcar como huerfanas las tareas que sigan abiertas, y que ningun rol pueda eliminar despues el expediente ni su historial, **para** dejar constancia final del caso y conservarlo como prueba disponible ante un reclamo o una auditoria.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 28 | No |

- Fundamento: OBL-ARCO-10 (Art. 20, Ley para la Proteccion de Datos Personales); OBL-RET-05 (Art. 47 Normativa PAS; Art. 5 lit. i LPDP (responsabilidad demostrada), Normativa para el Procedimiento Administrativo Sancionador)
- Depende de: HU-011-12, HU-011-13, HU-011-14
- Modulos requeridos: MOD-021, MOD-016

**Criterios de aceptacion**

1. Dado un expediente Reconocida sin transferencia previa, o con todos los receptores ya notificados, o Denegada ya notificada al titular, cuando el sistema completa la transicion correspondiente, entonces pasa a Cerrada con la fecha de cierre registrada y calcula la fecha sugerida de fin de retencion enviandola a MOD-016.
2. Dado que un expediente se cierra o se archiva, cuando existen tareas derivadas en MOD-021 que sigan abiertas, entonces el sistema las marca como huerfanas y notifica al Responsable ARCO-POL para su cierre manual.
3. Dado un expediente en estado Cerrada o Archivada, cuando cualquier rol, incluido el Administrador, intenta eliminarlo o eliminar su historial, entonces el sistema deniega la accion porque esa funcion no existe para ningun rol: la unica salida posible es el archivado por vencimiento de retencion, ejecutado por el sistema con aprobacion del Administrador.
4. Dado un expediente Cerrada, cuando el titular presenta un reclamo ante la Direccion de Proteccion de Datos dentro de los 10 dias habiles siguientes a la notificacion, entonces el sistema abre un sub-registro Reclamo ante la ACE vinculado, sin modificar ningun campo de la resolucion original.
5. Dado que faltan 90 dias para cumplirse el plazo de retencion sugerido de 5 anos, cuando el sistema lo detecta, entonces genera la alerta INFO Retencion del expediente proxima a vencer al Administrador y al Auditor, sin escalar.

**Reglas de negocio**

- Eliminar un expediente o su historial no existe como accion para ningun rol: solo existe archivado por vencimiento de retencion (seccion C).
- El plazo de retencion de 5 anos desde el cierre es el minimo recomendado sin norma expresa (OBL-RET-05, RECOMENDADO); el sistema lo muestra siempre con el texto de que es criterio propio del producto ante ausencia de norma expresa y requiere validacion de asesoria legal, y permite a la empresa configurar un plazo mayor si otra norma lo exige.
- Un expediente Cerrado no se reabre para cambiar la resolucion: el reclamo ante la ACE se anota como evento posterior vinculado, preservando integra la resolucion original.

**Fuera de alcance**

- Motor de retencion con catalogo de fundamentos sectoriales y alertas automaticas: pertenece a MOD-016 (SHOULD HAVE); aqui la conservacion es pasiva, sin boton de eliminar.

- Preguntas pendientes relacionadas: PP-PROD-07
- Referencia: MOD-011 secciones C fila Eliminar un expediente o su historial, F.2 filas Reconocida/Notificando a receptores/Denegada a Cerrada y Cerrada a Reclamo ante la ACE, G regla 11, I fila Retencion del expediente proxima a vencer, seccion Sobre el plazo de retencion
- Notas: Cubre parte de la fila MUST HAVE Evidencia con verificacion de integridad exportable en cuanto a su conservacion, y cubre de forma pasiva la obligacion propia de MOD-016 (los expedientes cerrados se conservan sin borrado), tal como indica el encargo y la seccion 19.4 del roadmap.

### HU-011-16. Aplicar la gratuidad y la tabla de costos de reproduccion o envio

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** que el sistema calcule si la modalidad de entrega elegida tiene costo segun la tabla publicada en la Politica de Privacidad, y que nunca permita cobrar un monto que no este en esa tabla, **para** cumplir la gratuidad general del ejercicio de derechos, cobrando unicamente lo que la ley permite y la empresa publico.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 27 | No |

- Fundamento: OBL-ARCO-13 (Art. 23, Ley para la Proteccion de Datos Personales)
- Depende de: HU-011-01
- Modulos requeridos: MOD-008

**Criterios de aceptacion**

1. Dado que el titular elige una modalidad de entrega sin costo segun la tabla publicada en MOD-008, cuando el sistema calcula la tarifa, entonces registra el monto cobrado en 0 con su fundamento de gratuidad.
2. Dado que el titular elige una modalidad de entrega con costo de reproduccion, certificacion o envio previamente publicado en MOD-008, cuando el sistema calcula la tarifa, entonces registra el monto exacto de la tabla publicada como fundamento del cobro.
3. Dado que una modalidad de entrega no tiene ningun monto publicado en la tabla de MOD-008, cuando el Responsable ARCO-POL intenta registrar un cobro por esa modalidad, entonces el sistema bloquea el cobro porque no puede aplicarse un monto no publicado previamente.
4. Dado un registro de tarifa aplicada, cuando se genera, entonces queda disponible en el reporte de tarifas cobradas y en el paquete de evidencia del expediente, visible para Administrador y Auditor.
5. Dado que la empresa no tiene ninguna tabla de costos publicada en MOD-008, cuando el titular presenta cualquier solicitud, entonces el sistema aplica gratuidad total por defecto, sin bloquear el tramite por la ausencia de tabla.

**Reglas de negocio**

- Solo pueden cobrarse costos de reproduccion, certificacion o envio previamente publicados; el ejercicio de derechos en si mismo es siempre gratuito.
- La tabla de costos se precarga desde la Politica de Privacidad publicada en MOD-008, no se redacta dentro de este modulo.

**Fuera de alcance**

- Redaccion o aprobacion de la tabla de costos: eso ocurre en MOD-008.
- Cobro efectivo del monto al titular por un medio de pago: fuera del alcance del sistema.

- Referencia: MOD-011 secciones D.8, D campos precargados, E fila Registro de tarifa aplicada, N fila Reporte de tarifas cobradas
- Notas: Cubre la fila MUST HAVE Gratuidad y tabla de costos de reproduccion publicados.

### HU-011-17. Generar el informe de acceso filtrando los datos de terceros

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** generar el informe de acceso con quienes consultaron los datos del titular, con que proposito y si hubo intercambio con otras instituciones, filtrando automaticamente cualquier dato de un tercero distinto del titular, **para** responder el derecho de acceso sin revelar nunca datos de otra persona.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 29 | No |

- Fundamento: OBL-ARCO-02 (Art. 8, Ley para la Proteccion de Datos Personales)
- Depende de: HU-011-06
- Modulos requeridos: MOD-006, MOD-009

**Criterios de aceptacion**

1. Dado un expediente de Acceso en En analisis de procedencia, cuando el Responsable ARCO-POL redacta el informe de acceso, entonces el sistema filtra automaticamente cualquier dato identificado como perteneciente a un tercero distinto del titular antes de mostrar el borrador.
2. Dado el borrador del informe de acceso filtrado, cuando el Responsable ARCO-POL lo revisa, entonces el sistema muestra el texto Requiere validacion de la organizacion o asesoria especializada junto a la confirmacion final de que no quedo ningun dato de tercero, dejando esa verificacion como responsabilidad humana antes de aprobar.
3. Dado que el dato del titular involucra una categoria sensible, por ejemplo datos biometricos, cuando el borrador del informe de acceso esta listo, entonces el sistema exige la aprobacion de un segundo revisor con el rol Aprobador antes de que el Delegado o Responsable interno lo apruebe.
4. Dado un informe de acceso aprobado, cuando el Delegado o Responsable interno lo emite, entonces el expediente pasa a Reconocida, se notifica al titular por la modalidad que eligio, y el sistema registra la tarifa aplicada segun HU-011-16.
5. Dado que el informe de acceso incluye el detalle de quienes consultaron los datos del titular, cuando el sistema lo genera, entonces incluye tambien si hubo intercambio con otras instituciones, sin omitir ese elemento exigido por el Art. 8.

**Reglas de negocio**

- El informe de acceso nunca puede revelar datos de un tercero distinto del titular (Art. 8).
- El filtrado automatico de terceros no sustituye la verificacion humana final antes de aprobar.

**Fuera de alcance**

- Extraccion tecnica del dato desde el sistema donde reside: la ejecuta el Responsable de Seguridad o IT como tarea derivada, con apoyo del RAT de MOD-006.

- Requiere contenido: Plantilla de informe de acceso, validada por la organizacion.
- Requiere validacion legal: Si
- Referencia: MOD-011 secciones D.7 fila Modalidad de acceso solicitada, E fila Informe de acceso, F.3 fila Datos de terceros mezclados con los del titular, H verificacion final de terceros
- Notas: Cubre la fila MUST HAVE Informe de acceso sin datos de terceros. Usa el Caso 7 de 08c_workflows_casos_07_08.md, informe de acceso sobre datos biometricos con segundo revisor, como base de los criterios 2 y 3.

### HU-011-18. Habilitar la portabilidad condicionada a la base de consentimiento y al tratamiento automatizado

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** que el sistema verifique en el RAT si la base juridica del tratamiento es consentimiento y si el tratamiento es automatizado antes de generar la exportacion portable, marcando la duda como decision humana cuando no este claro, **para** entregar la portabilidad solo cuando la ley realmente la exige, sin asumir por cuenta propia una base juridica dudosa.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 29 | No |

- Fundamento: OBL-ARCO-07 (Art. 14, Ley para la Proteccion de Datos Personales)
- Depende de: HU-011-11
- Modulos requeridos: MOD-006

**Criterios de aceptacion**

1. Dado un expediente de Portabilidad en En analisis de procedencia, cuando el Responsable ARCO-POL revisa el caso, entonces el sistema consulta en MOD-006 la base juridica y el caracter automatizado del Tratamiento vinculado, mostrando el resultado antes de continuar.
2. Dado que el Tratamiento vinculado tiene base juridica Consentimiento y es automatizado segun el RAT, cuando el Responsable ARCO-POL confirma la procedencia, entonces el sistema genera la exportacion en el formato estructurado que el titular eligio o en el formato por defecto sugerido.
3. Dado que existe duda sobre si la base juridica registrada en el RAT es realmente consentimiento, cuando el Responsable ARCO-POL revisa el caso, entonces el sistema muestra el texto Requiere validacion de la organizacion o asesoria especializada y deja la decision final a una persona, sin generar la exportacion de forma automatica.
4. Dado que el Tratamiento vinculado no tiene base juridica Consentimiento o no es automatizado, cuando el Responsable ARCO-POL lo revisa, entonces el sistema no bloquea el registro del checklist de causales de HU-011-11, permitiendo continuar hacia una denegatoria motivada si corresponde.
5. Dado que se indico un destinatario para el envio directo de los datos portados, cuando el sistema genera la exportacion, entonces deja registrado ese destinatario junto con el formato entregado, disponible en el expediente.

**Reglas de negocio**

- El sistema verifica lo que esta registrado en el RAT, pero si hay duda sobre si esa base es correcta, la decision final es humana (seccion H).
- La portabilidad comparte el mismo formulario de intake, el mismo motor de plazos y el mismo flujo de aprobacion que los demas derechos, sin un modulo separado.

**Fuera de alcance**

- Definicion del catalogo tecnico de formatos estructurados soportados: se resuelve como decision de producto fuera de esta HU.

- Requiere validacion legal: Si
- Referencia: MOD-011 secciones D.7 filas Destinatario de los datos portados y Formato solicitado, H confirmar la base juridica antes de habilitar la portabilidad
- Notas: Cubre la fila MUST HAVE Portabilidad condicionada (verificacion de base + automatizacion).

### HU-011-19. Exportar el expediente o el paquete de evidencia con verificacion de integridad

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** exportar el expediente completo o el paquete de evidencia de una solicitud ARCO-POL con un mecanismo que permita comprobar despues que no fue alterado, **para** entregar una prueba verificable ante una auditoria o ante un requerimiento de la Direccion de Proteccion de Datos de la ACE.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 29 | No |

- Fundamento: OBL-ARCO-01 (Art. 6, Ley para la Proteccion de Datos Personales); OBL-ARCO-02 (Art. 8, Ley para la Proteccion de Datos Personales); OBL-ARCO-08 (Art. 18, Ley para la Proteccion de Datos Personales); OBL-ARCO-10 (Art. 20, Ley para la Proteccion de Datos Personales); OBL-ARCO-13 (Art. 23, Ley para la Proteccion de Datos Personales)
- Depende de: HU-011-15
- Modulos requeridos: MOD-019

**Criterios de aceptacion**

1. Dado un expediente en cualquier estado, cuando el Administrador, el Delegado o Responsable interno, Legal o el Auditor exportan el expediente o su paquete de evidencia, entonces el sistema genera el paquete a traves de MOD-019 con un mecanismo de verificacion de integridad, por ejemplo hash o firma validable de forma independiente.
2. Dado un paquete de evidencia exportado, cuando se genera, entonces incluye el checklist de los 7 elementos del Art. 18 con usuario y fecha de cada marca, el historial completo de estados, las aprobaciones distintas de quien redacto cada borrador, y el registro de tarifa aplicada.
3. Dado que un adjunto de identidad del titular, por ejemplo su DUI, se consulta o se incluye en una exportacion, cuando el sistema completa la operacion, entonces registra en el historial quien accedio al documento y cuando, sin excepcion.
4. Dado un rol sin permiso de exportacion, por ejemplo Responsable de area o Colaborador, cuando intenta exportar el expediente o el paquete de evidencia, entonces el sistema deniega la accion.
5. Dado un Auditor externo invitado con acceso temporal a un expediente puntual, cuando exporta el paquete de evidencia de ese expediente, entonces el sistema limita la exportacion a lo asignado a esa invitacion, sin exponer otros expedientes de la organizacion.

**Reglas de negocio**

- Todo paquete de evidencias exportado incluye un mecanismo propio de verificacion de integridad, sin excepcion (anti-feature 25).
- El Auditor, interno o externo, exporta y consulta, pero nunca aprueba ni carga evidencia sobre el mismo expediente que audita.

**Fuera de alcance**

- Envio del paquete de evidencia o del informe de actuaciones directamente a la ACE: la empresa lo remite por el canal oficial (anti-feature 13).

- Referencia: MOD-011 secciones C fila Exportar expediente, J fila Exportacion del expediente completo, N fila Paquete de evidencia de un expediente individual
- Notas: Cubre la fila MUST HAVE Evidencia con verificacion de integridad exportable.

### HU-011-20. Registrar el reclamo del titular ante la Direccion de Proteccion de Datos como texto libre

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** anotar, dentro del expediente ya Cerrado, la fecha y el contenido del reclamo que el titular presento ante la Direccion de Proteccion de Datos de la ACE, sin modificar la resolucion original, **para** dejar constancia inmediata del reclamo desde el primer dia de uso del sistema, aunque la plantilla completa del informe de actuaciones madure mas adelante.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 29 | No |

- Fundamento: OBL-ARCO-14 (Art. 33 inc. 4, Lineamientos para el Delegado de Proteccion de Datos Personales)
- Depende de: HU-011-15
- Modulos requeridos: MOD-021, MOD-024

**Criterios de aceptacion**

1. Dado un expediente en Cerrada, cuando el titular presenta un reclamo ante la Direccion de Proteccion de Datos dentro de los 10 dias habiles siguientes a la notificacion de la resolucion, entonces el Responsable ARCO-POL o el Delegado registran la fecha del reclamo y su contenido como texto libre, y el sistema abre el sub-registro Reclamo ante la ACE sin alterar ningun campo de la resolucion original.
2. Dado que se registra un reclamo, cuando el sistema completa el registro, entonces genera la alerta CRITICAL Reclamo recibido de la Direccion de Proteccion de Datos al Delegado o Responsable interno, a Legal y al Administrador, de forma inmediata.
3. Dado un reclamo registrado, cuando el sistema crea la tarea derivada, entonces genera en MOD-021 la tarea Preparar informe de actuaciones asignada al Delegado o Responsable interno, sin plantilla dedicada de contenido en el MVP.
4. Dado que se presenta un reclamo fuera de los 10 dias habiles siguientes a la notificacion, cuando el Responsable ARCO-POL intenta registrarlo, entonces el sistema permite igual anotarlo como texto libre, dejando visible que se recibio fuera del plazo de referencia, sin bloquear el registro.
5. Dado un expediente Cerrada con un reclamo registrado, cuando cualquier usuario intenta modificar los campos de fondo de la resolucion original, entonces el sistema lo impide, porque el reclamo es un evento posterior vinculado, nunca una reapertura.

**Reglas de negocio**

- El registro basico del reclamo, con fecha y contenido en texto libre, entra en el MVP; la plantilla dedicada del informe de actuaciones con contenido estructurado madura en V1, segun la version minima vendible de la ficha y la seccion 19.3 del roadmap.
- La Direccion de Proteccion de Datos no tiene facultad de revocar la resolucion del Delegado, solo de requerir informe: por eso el reclamo nunca modifica la resolucion original.

**Fuera de alcance**

- Plantilla dedicada del informe de actuaciones con contenido estructurado: queda para V1.
- Envio real del informe de actuaciones a la ACE: la empresa lo remite por el canal oficial (anti-feature 13).

- Referencia: MOD-011 secciones F.2 fila Cerrada a Reclamo ante la ACE, G regla 12, I fila Reclamo recibido de la Direccion de Proteccion de Datos, Q fila Reclamo del titular ante la Direccion de Proteccion de Datos, version minima vendible
- Notas: La fila de la tabla Q Reclamo del titular ante la Direccion de Proteccion de Datos (registro + informe de actuaciones) esta marcada SHOULD HAVE en su conjunto, pero la propia justificacion de esa fila y el parrafo de version minima vendible de la seccion Q, junto con el criterio 4 de la seccion 19.6 del roadmap, indican de forma expresa que el registro basico como texto libre entra en el MVP sin retrasar el lanzamiento. Esta HU cubre unicamente ese registro basico, tal como lo pide el encargo; la plantilla dedicada del informe de actuaciones queda fuera de esta epica.

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Formulario interno seguro con los 7 elementos del Art. 18 | HU-011-01, HU-011-02, HU-011-06 |
| Carga directa de los 7 formularios oficiales ARCO-POL de la ACE | HU-011-02 |
| Verificacion de identidad para los 3 tipos de solicitante (titular, representante, heredero) | HU-011-03 |
| Sub-flujo de titular NNA (consentimiento parental, aviso de tension normativa) | HU-011-04 |
| Prevencion unica con archivo automatico | HU-011-07 |
| Plazo general 20+20 dias habiles con una sola prorroga | HU-011-06, HU-011-09 |
| Rama de incompetencia (5 dias habiles) | HU-011-08 |
| Rama de notificacion a receptores (5 dias habiles), con fallback manual si MOD-010 aun no esta completo | HU-011-14 |
| Bloqueo cautelar durante rectificacion | HU-011-10 |
| Denegatoria motivada con las 8 causales tasadas y notificacion en 3 dias habiles | HU-011-11, HU-011-13 |
| Gratuidad y tabla de costos de reproduccion publicados | HU-011-16 |
| Informe de acceso sin datos de terceros | HU-011-17 |
| Portabilidad condicionada (verificacion de base + automatizacion) | HU-011-18 |
| Motor de plazos compartido (consulta a MOD-023) | HU-011-06, HU-011-07, HU-011-08, HU-011-09, HU-011-13, HU-011-14 |
| Doble estado 659: aprobador por defecto segun MOD-002/MOD-024 | HU-011-05 |
| Evidencia con verificacion de integridad exportable | HU-011-19 |
| Reclamo del titular ante la Direccion de Proteccion de Datos (registro basico como texto libre, cubierto en el MVP; la plantilla de informe de actuaciones es SHOULD HAVE y queda fuera) | HU-011-20 |
