# EP-009 Proveedores y Encargados (MOD-009)

**Objetivo.** La empresa registra, evalua, contrata en firme y da seguimiento a cada Encargado, Tercero-Receptor y Subencargado que trata datos personales por su cuenta, con doble control en los casos de riesgo alto, alertas de vencimiento y revision, las notificaciones legales de 5 dias habiles hacia encargados y receptores, y un paquete de evidencia exportable por proveedor.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R2 | 14 | 67 | 0 | 67 | [MOD-009](../../03_modulos/MOD-009_ficha.md) |

**Notas de la epica.**

- Se siguio la tabla Q de MOD-009_ficha.md como fuente de alcance. Las 8 filas MUST HAVE de esa tabla quedan cubiertas: alta y ficha de los 3 tipos de entidad (bloques D.1 y D.2), vinculacion de Contrato/DPA, flujo de estados con doble control en riesgo alto, alertas de vencimiento de contrato y de revision periodica, las dos notificaciones legales de 5 dias habiles, datos de contacto para el aviso, y el paquete de evidencia exportable.
- Fuera de alcance por ser SHOULD HAVE, COULD HAVE o FUTURE en la tabla Q (no se redactaron HU para esto), conforme a la seccion 3 de INSTRUCCIONES_HU.md: (a) creacion automatica del registro pendiente de confirmar en Transferencias Internacionales cuando el pais es distinto de El Salvador (depende de MOD-010, SHOULD HAVE; el campo pais si se captura en HU-009-03, pero la automatizacion hacia MOD-010 y su alerta asociada quedan fuera, sin construir tampoco la tarea manual de respaldo porque el encargo no la incluyo en las indicaciones especificas); (b) modelado de cadenas de subcontratacion de segundo nivel o mas y la alerta de subencargado sin documento de sometimiento propio (el encargo excluye expresamente cadenas de segundo nivel; el registro de un Subencargado de primer nivel con su Encargado padre si queda incluido en HU-009-01 por ser parte de la fila 1 de la tabla Q); (c) la tarea automatica y la alerta de verificar devolucion o eliminacion de datos al finalizar la relacion (fila propia SHOULD HAVE de la tabla Q); se mantiene en HU-009-12 la exigencia basica de adjuntar la constancia antes de pasar a CERRADO cuando la clausula de devolucion/eliminacion fue pactada, por ser parte del flujo de estados MUST HAVE (fila 3); (d) suspension automatica al vincular un incidente de seguridad grave desde MOD-013 (fila propia COULD HAVE); se mantiene la suspension y reactivacion manual en HU-009-11 por ser parte del flujo de estados MUST HAVE; (e) motor de scoring automatizado de riesgo (FUTURE); (f) reportes exportables adicionales y dashboard completo (SHOULD HAVE), mas alla del listado con filtros y el paquete de evidencia por proveedor que si son MUST HAVE.
- No se redacto una historia de ayuda contextual (seccion R de la ficha, articulos de MOD-026) porque el encargo no la incluyo en sus indicaciones especificas; la regla 3 de INSTRUCCIONES_HU.md condiciona esa cobertura a que el encargo la indique.
- El paquete de evidencia por proveedor (HU-009-14) reutiliza el servicio comun de generacion de huella o firma de integridad de la plataforma (EP-000), como indica el encargo; por eso no se declaro EP-000 en depende_de_modulos de ninguna HU (no es un codigo MOD-NNN y la seccion 6 de INSTRUCCIONES_HU.md ya establece esa dependencia como implicita para toda epica), y se dejo la referencia explicita en el campo notas de esa historia.
- El campo pais o paises donde trata los datos (D.1) queda dentro de HU-009-03 porque es un dato obligatorio para enviar el proveedor a evaluacion segun la tabla de transiciones de la seccion F; la pregunta pendiente PP-JUR-06 (si un encargado extranjero es transferencia internacional o queda excluido por el Art. 4 lit. u) se cita en esa historia porque la captura del pais es lo que en el futuro disparara esa clasificacion, aunque la automatizacion en si (hacia MOD-010) no se construye en esta epica.
- La automatizacion 6 de la seccion G (notificacion al Encargado tras revocacion de consentimiento) depende de quien ocupe el rol aprobador segun el regimen de la reforma 659 vigente en MOD-024 (Delegado en el regimen ACTUAL, rol configurado como responsable interno en el regimen FUTURO); HU-009-09 declara esa dependencia y exige que el sistema deje registrada en el historial la version de la regla bajo la que se aprobo, tal como exige la seccion A de la ficha.
- Todas las historias quedan en release R2 porque MOD-009 pertenece al segundo grupo del nucleo vendible descrito en 19.8 y a la etapa Registrar de la secuencia de 19.9, construido en paralelo con MOD-008 y MOD-015 tras cerrar MOD-006; ninguna HU de esta epica es habilitadora de un modulo transversal de R1, salvo HU-009-01, que se marca habilitadora porque MOD-007 y MOD-011 (ambos tambien R2) necesitan el catalogo base de Encargados/Receptores de MOD-009 para sus propias notificaciones de 5 dias habiles (OBL-CONS-03 y OBL-ARCO-11).

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-009-01 | Dar de alta y editar los datos generales de un Encargado, Tercero-Receptor o Subencargado | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R2 | 22 | MOD-001, MOD-006 |
| HU-009-02 | Listar y consultar la ficha de proveedores con filtros y visibilidad segun el rol | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R2 | 22 | HU-009-01 |
| HU-009-03 | Vincular tratamientos del RAT y pais, y enviar el proveedor a evaluacion | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 5 | R2 | 22 | HU-009-01, MOD-006, MOD-021 |
| HU-009-04 | Registrar la evaluacion de riesgo y seguridad, y aprobarla o rechazarla | Responsable de Seguridad / IT | 5 | R2 | 22 | HU-009-03, MOD-015, MOD-021 |
| HU-009-05 | Vincular el Contrato/DPA y aprobar la activacion del proveedor con doble control | Aprobador | 8 | R2 | 22 | HU-009-04, MOD-008, MOD-023 |
| HU-009-06 | Registrar los datos de contacto del Encargado para el aviso de privacidad | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 2 | R2 | 22 | HU-009-05, MOD-008 |
| HU-009-07 | Recibir alertas y tareas de vencimiento del Contrato/DPA | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 3 | R2 | 22 | HU-009-05, MOD-021, MOD-022 |
| HU-009-08 | Ejecutar la revision periodica programada de un proveedor | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 5 | R2 | 22 | HU-009-05, MOD-021, MOD-022 |
| HU-009-09 | Notificar al Encargado la revocacion de un consentimiento dentro del plazo legal | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 8 | R2 | 23 | HU-009-05, MOD-007, MOD-023, MOD-021, MOD-024, MOD-008 |
| HU-009-10 | Notificar a un Tercero/Receptor tras una rectificacion, actualizacion o eliminacion | Responsable ARCO-POL / Responsable del tramite | 8 | R2 | 23 | HU-009-05, MOD-011, MOD-023, MOD-021, MOD-008 |
| HU-009-11 | Suspender manualmente a un proveedor por un incidente de seguridad y reactivarlo o finalizar la relacion | Responsable de Seguridad / IT | 5 | R2 | 24 | HU-009-05, MOD-013, MOD-022 |
| HU-009-12 | Finalizar y cerrar la relacion con un proveedor | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 24 | HU-009-05, HU-009-08, MOD-021 |
| HU-009-13 | Archivar un registro de proveedor duplicado, cancelado o creado por error | Administrador de la organizacion | 2 | R2 | 24 | HU-009-01 |
| HU-009-14 | Exportar el paquete de evidencia de un proveedor con verificacion de integridad | Auditor (interno) | 5 | R2 | 24 | HU-009-01, HU-009-05, MOD-008 |

## Historias

### HU-009-01. Dar de alta y editar los datos generales de un Encargado, Tercero-Receptor o Subencargado

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** registrar un nuevo proveedor clasificandolo como Encargado del tratamiento, Tercero-Receptor o Subencargado, con sus datos generales, y editar esos datos mientras el registro este en estado Borrador o En_evaluacion, **para** mantener un inventario unico y confiable de los proveedores que tratan datos personales por cuenta o para mi empresa, como exige la Ley para la Proteccion de Datos Personales.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 22 | Si |

- Fundamento: OBL-PROV-01 (Art. 33 inc. 2, Ley para la Proteccion de Datos Personales); OBL-PROV-05 (Art. 33 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: -
- Modulos requeridos: MOD-001, MOD-006

**Criterios de aceptacion**

1. Dado que no existe un registro previo, cuando el Responsable de area captura nombre comercial, razon social, tipo de entidad, servicio que presta y area o responsable interno que lo contrata, entonces el sistema crea el proveedor en estado BORRADOR y registra el evento de auditoria alta creada con usuario y fecha
2. Dado que se intenta guardar el alta sin el nombre comercial, la razon social, el tipo de entidad o el area responsable, cuando se confirma el guardado, entonces el sistema rechaza la operacion y senala como obligatorios los campos faltantes
3. Dado que el tipo de entidad seleccionado es Subencargado, cuando el usuario intenta guardar sin indicar el Encargado del que depende, entonces el sistema bloquea el guardado hasta que se vincule un Encargado que este en estado ACTIVO o EN_EVALUACION
4. Dado que el tipo de entidad seleccionado es Subencargado y el Encargado del que depende ya fue vinculado, cuando el registro se guarda, entonces el sistema muestra el texto Requiere validacion de la organizacion o asesoria especializada, indicando que si ese subencargado queda sometido a la LPDP no lo decide el sistema
5. Dado un proveedor en estado BORRADOR o EN_EVALUACION, cuando un usuario con permiso de modificar edita el nombre comercial, la razon social, el servicio que presta o los sistemas relacionados, entonces el sistema guarda el cambio y registra en el historial el valor anterior y el nuevo, con usuario y fecha
6. Dado un proveedor en estado ACTIVO, SUSPENDIDO, RELACION_FINALIZADA, CERRADO o ARCHIVADO, cuando cualquier usuario intenta editar el nombre comercial, la razon social o el tipo de entidad, entonces el sistema rechaza la edicion porque esos campos ya no son editables en ese estado
7. Dado un usuario con el rol Auditor (interno) o Auditor externo (invitado), cuando intenta crear o modificar un proveedor, entonces el sistema deniega la accion porque esos roles son de solo lectura
8. Dado un campo Sistemas relacionados o Area o responsable interno que lo contrata, cuando el usuario selecciona un valor, entonces el sistema lo toma por referencia de un catalogo existente y no permite digitarlo como texto libre nuevo

**Reglas de negocio**

- Para crear el registro en BORRADOR basta con nombre comercial, razon social, tipo de entidad, servicio que presta y area responsable
- Si Tipo de entidad = Subencargado, el Encargado del que depende es obligatorio y debe estar ACTIVO o EN_EVALUACION
- La edicion de datos generales solo esta permitida en BORRADOR o EN_EVALUACION
- El Auditor interno y el Auditor externo nunca crean, modifican ni aprueban

**Fuera de alcance**

- Modelado de cadenas de subcontratacion de mas de un nivel (un Subencargado que a su vez tenga su propio Subencargado)
- La alerta de Subencargado sin documento de sometimiento propio
- El calculo o sugerencia automatica del nivel de riesgo

- Requiere validacion legal: Si
- Referencia: MOD-009 secciones D.1, F (tabla de transiciones, fila de alta), H
- Notas: El texto de advertencia para Subencargado corresponde a la decision de la seccion H sobre OBL-PROV-05 (lectura extensiva del Art. 33 inc. 2, no verificada); se muestra siempre, incluso para un Subencargado de primer nivel.

### HU-009-02. Listar y consultar la ficha de proveedores con filtros y visibilidad segun el rol

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** ver el listado de proveedores de la organizacion filtrado por tipo de entidad, estado, pais y nivel de riesgo, y abrir la ficha completa de cualquiera de ellos, **para** dar seguimiento a todos los proveedores y encargados registrados sin depender de correos o carpetas dispersas.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 22 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-009-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que existen proveedores en distintos estados, cuando el Delegado abre el listado, entonces el sistema muestra nombre comercial, tipo de entidad, pais, estado de la relacion y nivel de riesgo de cada uno, ordenable y filtrable por esos mismos campos
2. Dado un filtro por Tipo de entidad = Subencargado, cuando se aplica, entonces el listado muestra unicamente los registros de ese tipo junto con el Encargado del que dependen
3. Dado un usuario con rol Responsable de area sin ningun rol de alcance global, cuando abre el listado, entonces el sistema muestra unicamente los proveedores de su propia area
4. Dado un usuario con rol Responsable ARCO-POL / Responsable del tramite, cuando abre el listado, entonces el sistema muestra en modo de solo lectura unicamente los proveedores vinculados al tratamiento de un caso ARCO-POL que tiene asignado
5. Dado un usuario con rol Auditor externo (invitado), cuando intenta abrir el listado, entonces el sistema restringe la vista a los proveedores que la organizacion incluyo de forma explicita en su invitacion de auditoria puntual
6. Dado un proveedor en estado ARCHIVADO, cuando el Administrador o el Auditor (interno) abren el listado, entonces el registro se muestra marcado como archivado y no se cuenta en los indicadores de proveedores activos
7. Dado un registro CERRADO, cuando un usuario con permiso de ver lo abre, entonces el sistema muestra su ficha completa en modo de solo lectura, incluida la referencia al registro historico anterior si el proveedor fue recontratado

**Reglas de negocio**

- Visibilidad por area salvo roles de alcance global (Administrador, Delegado, Legal/Compliance, Auditor)
- Responsable ARCO-POL ve solo lo vinculado a su caso
- Auditor externo ve solo lo incluido en su invitacion
- CERRADO y ARCHIVADO son consultables pero no editables

**Fuera de alcance**

- Reportes exportables en PDF, XLSX o CSV (se cubren, para el paquete probatorio, en HU-009-14)
- Busqueda global entre modulos (MOD-025)

- Referencia: MOD-009 secciones C, D.1, F (estados terminales)

### HU-009-03. Vincular tratamientos del RAT y pais, y enviar el proveedor a evaluacion

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** vincular al menos un tratamiento del RAT, ver las categorias de datos que se calculan solas, indicar el pais o paises donde el proveedor trata los datos, y enviar el proveedor a evaluacion, **para** dejar trazabilidad de con que actividad de tratamiento se relaciona el proveedor antes de que alguien evalue su riesgo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 22 | No |

- Fundamento: OBL-TRAT-01 (Art. 32, Ley para la Proteccion de Datos Personales)
- Depende de: HU-009-01
- Modulos requeridos: MOD-006, MOD-021

**Criterios de aceptacion**

1. Dado un proveedor en BORRADOR sin tratamientos del RAT vinculados, cuando se intenta enviarlo a evaluacion, entonces el sistema bloquea la transicion y exige vincular al menos un tratamiento del RAT
2. Dado que se vincula uno o mas tratamientos del RAT, cuando se guarda el vinculo, entonces el sistema calcula y muestra de forma automatica y de solo lectura las categorias de datos a las que accede el proveedor, tomadas de esos tratamientos
3. Dado un proveedor sin ningun pais capturado en Pais o paises donde trata los datos, cuando se intenta enviar a evaluacion, entonces el sistema exige al menos un pais antes de permitir la transicion
4. Dado un proveedor con nombre comercial, razon social, tipo de entidad, area responsable, al menos un tratamiento del RAT vinculado y al menos un pais capturado, cuando el Responsable de area o el Delegado envian el proveedor a evaluacion, entonces el sistema cambia el estado de BORRADOR a EN_EVALUACION y crea una tarea en el Centro de Tareas para el Responsable de Seguridad/IT
5. Dado un proveedor con un pais distinto de El Salvador, cuando pasa a EN_EVALUACION, entonces el sistema deja constancia en el historial de ese dato, sin generar el registro de transferencia internacional porque esa automatizacion pertenece a MOD-010 y queda fuera del alcance de esta historia
6. Dado un proveedor en EN_EVALUACION, cuando el Responsable de Seguridad/IT o el Delegado registran un motivo de rechazo, entonces el sistema regresa el proveedor a BORRADOR, notifica a quien creo el registro y conserva el motivo en el historial
7. Dado un usuario sin el rol Responsable de area ni Delegado, cuando intenta ejecutar la transicion de enviar a evaluacion, entonces el sistema deniega la accion

**Reglas de negocio**

- Enviar a evaluacion exige al menos un tratamiento del RAT y al menos un pais capturado
- Las categorias de datos se calculan solas desde los tratamientos vinculados y no se editan de forma directa
- El rechazo de la evaluacion regresa el proveedor a BORRADOR con motivo obligatorio

**Fuera de alcance**

- Creacion automatica de un registro pendiente de confirmar en Transferencias Internacionales (MOD-010, SHOULD HAVE)
- Determinar si el pais donde el proveedor trata los datos tiene nivel de proteccion adecuado

- Preguntas pendientes relacionadas: PP-JUR-06
- Referencia: MOD-009 secciones D.1, F (transicion Enviar a evaluacion), G (automatizacion 1, excluida de esta epica)
- Notas: PP-JUR-06 se cita porque el campo pais que aqui se captura es el dato que en el futuro (cuando MOD-010 exista) disparara la clasificacion de transferencia internacional; esta historia no resuelve esa pregunta, solo registra el dato.

### HU-009-04. Registrar la evaluacion de riesgo y seguridad, y aprobarla o rechazarla

**Como** Responsable de Seguridad / IT, **quiero** asignar el nivel de riesgo del proveedor, declarar las medidas de seguridad y adjuntar evidencia, para que un Aprobador o el Delegado aprueben o rechacen la evaluacion, **para** verificar que el proveedor cumple medidas de seguridad equivalentes a las de mi empresa antes de contratarlo en firme.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 22 | No |

- Fundamento: OBL-PROV-02 (Art. 34, Ley para la Proteccion de Datos Personales); OBL-PROV-03 (Art. 36, Ley para la Proteccion de Datos Personales)
- Depende de: HU-009-03
- Modulos requeridos: MOD-015, MOD-021

**Criterios de aceptacion**

1. Dado un proveedor en EN_EVALUACION, cuando el Responsable de Seguridad/IT asigna un Nivel de riesgo de Bajo, Medio o Alto, entonces el sistema deja esa decision como una eleccion humana y no la fija por si solo a partir del cuestionario de apoyo
2. Dado un nivel de riesgo Medio o Alto, cuando se intenta guardar la evaluacion sin al menos una medida de seguridad del catalogo de MOD-015, entonces el sistema bloquea el guardado
3. Dado una evaluacion completa con nivel de riesgo asignado y, si aplica, medidas de seguridad declaradas, cuando el Aprobador o el Delegado la aprueban, entonces el sistema cambia el estado de EN_EVALUACION a PENDIENTE_DE_CONTRATO, registra el evento de auditoria evaluacion aprobada y crea la tarea vincular contrato/DPA
4. Dado que la misma persona con rol Responsable de Seguridad/IT ejecuto la evaluacion tecnica de un proveedor de riesgo Alto, cuando esa misma persona intenta aprobarla, entonces el sistema deniega la aprobacion, salvo que la organizacion este por debajo del umbral configurable de tamano, en cuyo caso permite la aprobacion mostrando una advertencia visible de autorrevision
5. Dado un archivo adjuntado como Evidencia de seguridad del proveedor, cuando el usuario intenta subir algo distinto de certificaciones, autoevaluaciones o reportes, entonces el texto de ayuda advierte no subir bases de datos completas del proveedor
6. Dado un usuario con el rol Responsable de area, cuando intenta aprobar una evaluacion de riesgo, entonces el sistema deniega la accion porque ese rol solo completa datos operativos, no aprueba evaluaciones
7. Dado un proveedor cuya evaluacion se aprueba, cuando se consulta su historial, entonces el sistema muestra quien evaluo, quien aprobo y en que fecha

**Reglas de negocio**

- El nivel de riesgo siempre lo decide una persona, nunca un calculo automatico
- Medidas de seguridad obligatorias si el riesgo es Medio o Alto
- Separacion de funciones entre quien evalua y quien aprueba, salvo pyme bajo el umbral configurable, con advertencia visible
- La evidencia de seguridad se limita a certificaciones, autoevaluaciones o reportes

**Fuera de alcance**

- Motor de scoring automatizado de riesgo de proveedores
- Plantilla dedicada para las instrucciones documentadas de tratamiento (queda como campo de texto simple, sin plantilla propia)

- Referencia: MOD-009 secciones D.2, F (transicion Aprobar evaluacion de riesgo y seguridad), H, C (separacion de funciones)

### HU-009-05. Vincular el Contrato/DPA y aprobar la activacion del proveedor con doble control

**Como** Aprobador, **quiero** verificar que el proveedor tiene un Contrato o DPA vigente vinculado y aprobar su paso a estado ACTIVO, con un segundo control cuando el riesgo es Alto o el pais es distinto de El Salvador, **para** asegurar que ningun proveedor empiece a tratar datos personales sin haberse sometido de forma expresa a la ley.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 22 | No |

- Fundamento: OBL-PROV-01 (Art. 33 inc. 2, Ley para la Proteccion de Datos Personales); OBL-PROV-02 (Art. 34, Ley para la Proteccion de Datos Personales)
- Depende de: HU-009-04
- Modulos requeridos: MOD-008, MOD-023

**Criterios de aceptacion**

1. Dado un proveedor en PENDIENTE_DE_CONTRATO sin ningun documento tipo Contrato/DPA vinculado y vigente, cuando alguien intenta pasarlo a ACTIVO, entonces el sistema bloquea la transicion y muestra el mensaje que cita OBL-PROV-01 y el Art. 33 inc. 2
2. Dado un documento tipo Contrato/DPA de MOD-008 vinculado con fecha de vigencia de inicio y fecha de vencimiento, cuando la fecha de inicio es posterior a la fecha de vencimiento, entonces el sistema rechaza el guardado de esas fechas
3. Dado un proveedor con Nivel de riesgo Alto o con un pais distinto de El Salvador, cuando se intenta aprobar la activacion, entonces el sistema exige que quien aprueba sea una persona distinta de quien registro o evaluo al proveedor
4. Dado un proveedor con Contrato/DPA vigente vinculado, cuando el Aprobador o el Delegado aprueban la activacion, entonces el sistema cambia el estado a ACTIVO, programa la proxima revision periodica segun el calendario de MOD-023 y la periodicidad configurada, y registra el evento de auditoria proveedor activado
5. Dado un proveedor de Tipo de entidad Encargado que pasa a ACTIVO, cuando la transicion se completa, entonces el sistema habilita los campos de contacto del encargado para el aviso de privacidad
6. Dado un Contrato/DPA vinculado y vigente generado desde la plantilla del sistema, cuando un usuario consulta la ficha del proveedor, entonces el sistema muestra el texto documento generado como borrador, pendiente de revision, junto con la advertencia de que la suficiencia de sus clausulas frente al Art. 34 y al Art. 36 requiere revision de la organizacion o de su asesoria legal
7. Dado un proveedor en una organizacion por debajo del umbral configurable de tamano, cuando la misma persona que evaluo intenta tambien aprobar la activacion de un proveedor de riesgo Alto, entonces el sistema lo permite mostrando una advertencia visible de autorrevision
8. Dado un usuario con el rol Responsable de Seguridad/IT, cuando intenta aprobar el paso a ACTIVO, entonces el sistema deniega la accion porque ese rol evalua pero no aprueba

**Reglas de negocio**

- Bloqueo automatico del paso a ACTIVO sin Contrato/DPA vigente y vinculado
- Doble control obligatorio si el riesgo es Alto o el pais es distinto de El Salvador, salvo pyme bajo el umbral con advertencia visible
- Un solo Contrato/DPA vigente por proveedor a la vez
- Los campos de contacto de D.5 solo se habilitan para Encargado activo

**Fuera de alcance**

- Revisar o certificar el contenido legal del contrato: el sistema solo verifica que existe, esta vigente y es del tipo correcto
- Registrar la transferencia internacional del proveedor en MOD-010

- Requiere contenido: Plantilla de Contrato/DPA estandar (Encargado) validada por asesoria legal antes de publicarse en el catalogo de MOD-008; Plantilla de Documento de sometimiento a la LPDP (Tercero/Receptor) validada por asesoria legal
- Requiere validacion legal: Si
- Referencia: MOD-009 secciones D.3, F (transicion Vincular contrato/DPA y aprobar activacion), G (automatizaciones 2 y 10), H

### HU-009-06. Registrar los datos de contacto del Encargado para el aviso de privacidad

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** capturar el nombre de contacto y el correo o telefono de un Encargado activo, **para** que esos datos puedan publicarse en el aviso de privacidad de mi empresa, como exige la ley.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R2 | 22 | No |

- Fundamento: OBL-AVISO-02 (Art. 24 lit. h), Ley para la Proteccion de Datos Personales); OBL-PROV-04 (Art. 56 lit. a num. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-009-05
- Modulos requeridos: MOD-008

**Criterios de aceptacion**

1. Dado un proveedor con Tipo de entidad Encargado y Estado ACTIVO, cuando se intenta guardar la ficha sin el nombre de contacto o sin el correo/telefono, entonces el sistema exige ambos campos como obligatorios
2. Dado un valor capturado en Correo o telefono de contacto, cuando no tiene formato valido de correo electronico ni de telefono, entonces el sistema rechaza el guardado y senala el formato esperado
3. Dado un proveedor de Tipo de entidad Tercero/Receptor o Subencargado, cuando se abre su ficha, entonces el sistema no muestra los campos de contacto porque son exclusivos de Encargado
4. Dado que se guardan o modifican los datos de contacto de un Encargado activo, cuando el cambio se confirma, entonces el sistema conserva el historial de versiones de ese dato, con usuario y fecha
5. Dado un Encargado activo cuyos datos de contacto ya existen, cuando el aviso de privacidad vigente en MOD-008 todavia no lo lista en el literal h del Art. 24, entonces el sistema deja disponible la referencia de este Encargado para que MOD-008 la incluya en su siguiente version
6. Dado un usuario con el rol Auditor (interno), cuando intenta modificar los datos de contacto de un Encargado, entonces el sistema deniega la accion por tratarse de un rol de solo lectura

**Reglas de negocio**

- Nombre de contacto y correo/telefono obligatorios solo si Tipo = Encargado y Estado = ACTIVO
- Validacion de formato de correo o telefono
- Historial de version del dato de contacto

**Fuera de alcance**

- La publicacion del aviso de privacidad en si (funcionalidad de MOD-008)
- La alerta Aviso no menciona un encargado nuevo (disparo y propiedad de MOD-008)

- Referencia: MOD-009 seccion D.5

### HU-009-07. Recibir alertas y tareas de vencimiento del Contrato/DPA

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** recibir una alerta cuando falten 30 y 7 dias para que venza el contrato o DPA de un proveedor, y otra si ya vencio sin renovarse, **para** renovar a tiempo la relacion y no dejar a un proveedor activo sin documento de sometimiento vigente.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 22 | No |

- Fundamento: OBL-PROV-01 (Art. 33 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-009-05
- Modulos requeridos: MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado un proveedor ACTIVO cuya fecha de vencimiento del contrato esta a 30 dias, cuando el sistema detecta esa fecha, entonces genera una alerta de nivel WARNING para el Responsable de area y el Delegado, por plataforma y correo, y crea una tarea en el Centro de Tareas
2. Dado la alerta WARNING sin ninguna accion siete dias despues, cuando transcurre esa semana, entonces el sistema la repite
3. Dado un proveedor ACTIVO cuya fecha de vencimiento esta a 7 dias, cuando el sistema detecta esa fecha, entonces genera una alerta de nivel HIGH diaria para el Responsable de area, el Delegado y el Aprobador
4. Dado un proveedor cuya fecha de vencimiento del contrato ya paso sin que se haya vinculado un nuevo Contrato/DPA vigente, cuando el sistema evalua las alertas pendientes, entonces genera una alerta CRITICAL diaria para el Delegado y el Administrador hasta que se resuelva
5. Dado un proveedor con la alerta HIGH activa, cuando pasan 7 dias sin gestion, entonces el sistema la escala al Administrador
6. Dado que se vincula un nuevo Contrato/DPA vigente o se cierra formalmente la relacion con el proveedor, cuando eso ocurre, entonces el sistema apaga todas las alertas de vencimiento asociadas a ese contrato
7. Dado un proveedor en estado distinto de ACTIVO, cuando se calculan las alertas de vencimiento, entonces el sistema no genera ninguna alerta de vencimiento de contrato para ese registro

**Reglas de negocio**

- Tres niveles de alerta: WARNING a 30 dias, HIGH a 7 dias, CRITICAL si ya vencio
- Los dias de anticipacion son configurables
- Las alertas y tareas usan los servicios comunes de Notificaciones y Centro de Tareas

**Fuera de alcance**

- Calculo del plazo en dias habiles (no aplica: es un plazo contractual pactado por las partes, no un plazo legal)
- Creacion del registro de transferencia en MOD-010

- Referencia: MOD-009 seccion G (automatizaciones 4 y 4b), seccion I

### HU-009-08. Ejecutar la revision periodica programada de un proveedor

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** que el sistema me cree una tarea de revision cuando llegue la fecha programada, y poder registrar el resultado de esa revision, **para** confirmar de forma periodica que la evaluacion de riesgo de cada proveedor sigue vigente.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 22 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-009-05
- Modulos requeridos: MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado un proveedor ACTIVO cuya fecha de proxima revision calculada segun la periodicidad configurada llega, cuando el sistema la detecta, entonces crea la tarea revisar proveedor X y cambia el estado a EN_REVISION
2. Dado un proveedor en EN_REVISION, cuando se registra que la revision no encontro cambios materiales, entonces el sistema regresa el estado a ACTIVO y actualiza el campo Fecha de ultima revision
3. Dado un proveedor en EN_REVISION, cuando se detecta un cambio material de nuevo pais, nueva categoria de dato o cambio de nivel de riesgo y se registra el motivo, entonces el sistema mueve el proveedor a EN_EVALUACION conservando integro el historial anterior
4. Dado un proveedor ACTIVO cuya fecha de revision programada ya paso sin que se haya registrado una revision nueva, cuando el sistema evalua las alertas, entonces genera una alerta WARNING semanal para el Responsable de area y el Delegado
5. Dado que la alerta de revision vencida sigue activa 15 dias despues, cuando transcurre ese plazo, entonces el sistema la escala al Aprobador
6. Dado un usuario sin el rol Responsable de area, Delegado o Responsable de Seguridad/IT, cuando intenta registrar el resultado de una revision, entonces el sistema deniega la accion
7. Dado que se completa una revision, cuando se guarda, entonces el sistema deja evidencia en el historial con fecha, usuario y resultado

**Reglas de negocio**

- La periodicidad de revision es Anual, Semestral o un numero de meses configurable
- La revision sin cambios no reinicia el flujo de evaluacion
- La revision con cambios materiales reinicia el proveedor a EN_EVALUACION conservando su historial

**Fuera de alcance**

- La alerta mensual proveedor activo sin evaluacion de riesgo vigente, distinta de la revision periodica programada aqui descrita

- Referencia: MOD-009 seccion F (transiciones desde ACTIVO y EN_REVISION), G (automatizacion 5), I

### HU-009-09. Notificar al Encargado la revocacion de un consentimiento dentro del plazo legal

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que el sistema cree una tarea para notificar al Encargado activo cuando MOD-007 marque la revocacion de un consentimiento vinculado, con el plazo legal calculado, y poder aprobar el envio de esa notificacion, **para** cumplir el plazo de 5 dias habiles del Art. 30 y dejar evidencia de que el encargado fue informado.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 23 | No |

- Fundamento: OBL-CONS-03 (Art. 30, Ley para la Proteccion de Datos Personales)
- Depende de: HU-009-05
- Modulos requeridos: MOD-007, MOD-023, MOD-021, MOD-024, MOD-008

**Criterios de aceptacion**

1. Dado que MOD-007 marca la revocacion de un consentimiento vinculado a un tratamiento con un Encargado en estado ACTIVO, cuando el evento llega a MOD-009, entonces el sistema crea la tarea notificar la revocacion a [Encargado] con la fecha limite de 5 dias habiles calculada por MOD-023
2. Dado que el regimen normativo vigente en MOD-024 es ACTUAL, cuando se crea la tarea de notificacion, entonces queda pendiente de aprobacion de quien ocupe el rol Delegado de Proteccion de Datos antes de poder enviarse
3. Dado que el regimen normativo vigente en MOD-024 cambia a FUTURO, cuando se crea una tarea nueva de este tipo, entonces queda pendiente de aprobacion de quien ocupe el rol configurado como responsable interno, y el sistema registra en el historial bajo que version de la regla se aprobo
4. Dado la tarea de notificacion pendiente de aprobacion, cuando el Delegado la aprueba, entonces el sistema genera la carta de notificacion desde la plantilla del sistema y permite marcarla como enviada, adjuntando la constancia de envio
5. Dado que faltan 2 dias habiles para que venza el plazo de 5 dias habiles de la notificacion al Encargado, cuando el sistema lo detecta, entonces genera una alerta WARNING que escala a CRITICAL si el plazo vence sin enviarse
6. Dado un Encargado que no esta en estado ACTIVO cuando ocurre la revocacion, cuando el sistema evalua la condicion, entonces no crea la tarea de notificacion para ese Encargado
7. Dado que la notificacion se envia y se adjunta la constancia, cuando se consulta el expediente, entonces el sistema muestra la evidencia con fecha, usuario y verificacion del plazo cumplido
8. Dado un usuario sin el rol Delegado ni el rol configurado como responsable interno segun el regimen vigente, cuando intenta aprobar el envio de esta notificacion, entonces el sistema deniega la accion

**Reglas de negocio**

- El plazo de 5 dias habiles siempre se calcula en MOD-023, nunca dentro de MOD-009
- La tarea queda pendiente de aprobacion del Delegado o del rol configurado como responsable interno segun el regimen vigente en MOD-024
- El texto de la notificacion es configurable, el plazo no

**Fuera de alcance**

- La ejecucion misma de la revocacion del consentimiento (ocurre en MOD-007)
- El calculo del plazo en si (ocurre en MOD-023)

- Requiere contenido: Plantilla de notificacion de revocacion de consentimiento al Encargado, validada por asesoria legal antes de usarse
- Requiere validacion legal: Si
- Referencia: MOD-009 secciones A, G (automatizacion 6), I, J, K

### HU-009-10. Notificar a un Tercero/Receptor tras una rectificacion, actualizacion o eliminacion

**Como** Responsable ARCO-POL / Responsable del tramite, **quiero** que el sistema cree una tarea para notificar a cada Tercero/Receptor vinculado cuando MOD-011 cierre un caso de rectificacion, actualizacion o eliminacion, con el plazo legal calculado, y dejar evidencia del envio, **para** cumplir el plazo de 5 dias habiles del Art. 21 inciso 3 con cada receptor que recibio los datos del titular.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 23 | No |

- Fundamento: OBL-ARCO-11 (Art. 21 inc. 3, Ley para la Proteccion de Datos Personales)
- Depende de: HU-009-05
- Modulos requeridos: MOD-011, MOD-023, MOD-021, MOD-008

**Criterios de aceptacion**

1. Dado que MOD-011 cierra un caso de rectificacion, actualizacion o eliminacion sobre un tratamiento con al menos un Tercero/Receptor vinculado, cuando el evento llega a MOD-009, entonces el sistema crea una tarea notificar a [Receptor] por cada receptor vinculado, con la fecha limite de 5 dias habiles calculada por MOD-023
2. Dado un tratamiento sin ningun Tercero/Receptor vinculado en MOD-009, cuando MOD-011 cierra el caso, entonces el sistema no crea ninguna tarea de notificacion a receptores
3. Dado la tarea de notificacion a un receptor, cuando el Responsable ARCO-POL genera la carta desde la plantilla del sistema y la marca como enviada, entonces el sistema adjunta la constancia de la comunicacion enviada como evidencia del expediente
4. Dado que faltan 2 dias habiles para que venza el plazo de notificacion a un receptor, cuando el sistema lo detecta, entonces genera una alerta que escala segun la configuracion de MOD-022 si el plazo vence sin enviarse
5. Dado un proveedor registrado como Tipo de entidad Encargado en vez de Tercero/Receptor para el mismo tratamiento, cuando el caso de rectificacion se cierra, entonces el sistema no genera la tarea de notificacion a receptor para ese registro
6. Dado que se notifico a todos los receptores vinculados a un caso, cuando se consulta el expediente en MOD-009, entonces el sistema muestra el registro y la evidencia de cada notificacion enviada, con fecha y verificacion del plazo
7. Dado un usuario con el rol Usuario de consulta / Colaborador al que se le asigno la tarea de subir la constancia de envio, cuando la adjunta, entonces el sistema la acepta como evidencia sin darle permisos adicionales sobre el resto del proveedor

**Reglas de negocio**

- El plazo de 5 dias habiles se calcula en MOD-023
- Se crea una tarea de notificacion por cada Tercero/Receptor vinculado al tratamiento afectado
- El texto de la notificacion es configurable, el plazo no

**Fuera de alcance**

- La determinacion de procedencia de la rectificacion, actualizacion o eliminacion (ocurre en MOD-011)
- El registro formal de transferencia internacional en MOD-010

- Requiere contenido: Plantilla de notificacion a Receptor tras rectificacion, actualizacion o eliminacion, validada por asesoria legal
- Requiere validacion legal: Si
- Referencia: MOD-009 secciones A, G (automatizacion 7), I, J, K

### HU-009-11. Suspender manualmente a un proveedor por un incidente de seguridad y reactivarlo o finalizar la relacion

**Como** Responsable de Seguridad / IT, **quiero** vincular un incidente de seguridad grave a un proveedor activo y suspenderlo, y despues reactivarlo si las medidas correctivas se verifican o finalizar la relacion si la empresa decide terminarla, **para** dejar de exponer datos a un proveedor mientras no se confirme que el riesgo esta controlado.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 24 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-009-05
- Modulos requeridos: MOD-013, MOD-022

**Criterios de aceptacion**

1. Dado un proveedor ACTIVO al que se vincula un incidente de seguridad grave registrado en MOD-013, cuando el Responsable de Seguridad/IT o el Delegado ejecutan la suspension, entonces el sistema cambia el estado a SUSPENDIDO y notifica al Responsable de area
2. Dado un proveedor recien SUSPENDIDO, cuando se consulta su ficha, entonces el sistema muestra la advertencia operativa de no enviar nuevos datos a ese proveedor hasta resolver el incidente, dejando claro que el sistema no ejecuta ningun bloqueo tecnico
3. Dado un proveedor SUSPENDIDO con evidencia de cierre del incidente vinculado, cuando el Delegado o el Aprobador verifican que las medidas correctivas fueron confirmadas, entonces el sistema permite reactivarlo a ACTIVO y registra el evento de auditoria reactivado tras suspension
4. Dado un proveedor SUSPENDIDO, cuando la empresa decide terminar la relacion tras el incidente y se registra el motivo de cierre, entonces el sistema lo mueve a RELACION_FINALIZADA
5. Dado que el sistema sugiere un cambio de estado a partir de la severidad reportada por MOD-013, cuando se evalua reactivar, terminar o mantener suspendido a un proveedor, entonces exige que una persona con el rol Delegado o Aprobador confirme la decision final, sin aplicarla de forma automatica
6. Dado un usuario con el rol Responsable de area, cuando intenta reactivar un proveedor suspendido, entonces el sistema deniega la accion porque ese rol no esta habilitado para esta transicion
7. Dado un proveedor SUSPENDIDO, cuando se consulta su historial, entonces el sistema muestra quien vinculo el incidente, quien decidio la reactivacion o el cierre, y en que fecha

**Reglas de negocio**

- La suspension y la reactivacion siempre requieren una decision humana
- El sistema no bloquea tecnicamente el envio de datos, solo advierte
- La reactivacion exige evidencia de cierre del incidente vinculado

**Fuera de alcance**

- La suspension automatica disparada por la severidad del incidente sin intervencion humana (integracion COULD HAVE con MOD-013)
- El registro y flujo completo del incidente de seguridad en si (MOD-013)

- Referencia: MOD-009 seccion F (transiciones ACTIVO-SUSPENDIDO), G (automatizacion 11, parcial), H, I

### HU-009-12. Finalizar y cerrar la relacion con un proveedor

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** registrar el fin natural del contrato o la decision de no renovar con un proveedor, y despues cerrar el expediente dejandolo como evidencia, **para** dejar constancia clara de cuando y por que termino cada relacion con un proveedor.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 24 | No |

- Fundamento: OBL-PROV-07 (Art. 34 lit. a), en relacion con Art. 5 lit. h), Ley para la Proteccion de Datos Personales)
- Depende de: HU-009-05, HU-009-08
- Modulos requeridos: MOD-021

**Criterios de aceptacion**

1. Dado un proveedor ACTIVO cuyo contrato termina o cuya empresa decide no renovarlo, cuando se registra el Motivo de cierre entre Contrato vencido, Terminacion anticipada, Cambio de proveedor u Otro, entonces el sistema cambia el estado a RELACION_FINALIZADA
2. Dado un intento de pasar a RELACION_FINALIZADA sin capturar el Motivo de cierre, cuando se confirma la accion, entonces el sistema rechaza la transicion por falta de ese dato obligatorio
3. Dado un proveedor en RELACION_FINALIZADA cuya clausula de devolucion/eliminacion pactada es Si, cuando el Delegado o el Administrador intentan cerrarlo, entonces el sistema exige adjuntar la constancia de devolucion o eliminacion de datos antes de permitir el paso a CERRADO
4. Dado un proveedor en RELACION_FINALIZADA cuya clausula de devolucion/eliminacion pactada es No o No aplica, cuando se cierra, entonces el sistema permite el paso a CERRADO dejando registrada esa condicion, sin exigir el archivo adjunto
5. Dado un proveedor que pasa a CERRADO, cuando la transicion se completa, entonces el sistema registra el evento de auditoria final y deja el registro en solo lectura, aunque sigue siendo consultable como evidencia
6. Dado que existian tareas abiertas en el Centro de Tareas que dependian de este proveedor, cuando el proveedor se cierra, entonces esas tareas se marcan proveedor cerrado, verificar si la tarea sigue aplicando en vez de cerrarse de forma automatica
7. Dado un proveedor ya CERRADO, cuando la empresa vuelve a contratarlo, entonces el sistema no reactiva ese registro, sino que se crea un nuevo registro de proveedor que lo referencia como historico

**Reglas de negocio**

- El motivo de cierre siempre es obligatorio
- La constancia de devolucion/eliminacion es obligatoria solo si la clausula pactada lo exige
- CERRADO es un estado terminal de solo lectura
- Un proveedor CERRADO nunca se reactiva

**Fuera de alcance**

- La tarea automatica en el Centro de Tareas que recuerda verificar la devolucion o eliminacion de datos, y su alerta asociada (funcionalidad SHOULD HAVE segun la tabla Q de la ficha)

- Referencia: MOD-009 seccion F (transiciones RELACION_FINALIZADA y CERRADO, estados terminales, reapertura), D.4

### HU-009-13. Archivar un registro de proveedor duplicado, cancelado o creado por error

**Como** Administrador de la organizacion, **quiero** archivar un proveedor en Borrador o En_evaluacion que se creo por error o esta duplicado, dejando la justificacion en el historial, **para** mantener limpio el catalogo de proveedores sin borrar informacion que pueda servir de evidencia.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R2 | 24 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-009-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un proveedor en BORRADOR o EN_EVALUACION, cuando se intenta archivar sin escribir una justificacion, entonces el sistema rechaza la accion porque la justificacion es obligatoria
2. Dado un proveedor en BORRADOR o EN_EVALUACION con justificacion capturada, cuando el Administrador confirma el archivado, entonces el sistema cambia el estado a ARCHIVADO y registra el evento con usuario, fecha y motivo
3. Dado un proveedor ARCHIVADO, cuando se calculan los indicadores de proveedores activos del dashboard, entonces el sistema lo excluye de esos indicadores
4. Dado un proveedor ARCHIVADO, cuando el Auditor (interno) consulta el modulo, entonces el registro permanece visible para el
5. Dado un proveedor en ACTIVO, PENDIENTE_DE_CONTRATO, SUSPENDIDO, RELACION_FINALIZADA o CERRADO, cuando cualquier usuario intenta archivarlo, entonces el sistema deniega la accion porque archivar solo esta permitido desde BORRADOR o EN_EVALUACION
6. Dado un usuario con un rol distinto de Administrador, cuando intenta archivar un proveedor, entonces el sistema deniega la accion
7. Dado un proveedor ARCHIVADO, cuando cualquier usuario intenta eliminarlo por completo del sistema, entonces el sistema no ofrece esa opcion porque nunca existe un borrado real de un registro con contenido

**Reglas de negocio**

- Archivar exige justificacion obligatoria
- Solo el Administrador puede archivar
- Archivar solo aplica desde BORRADOR o EN_EVALUACION
- Nunca hay eliminacion real de un registro con contenido

**Fuera de alcance**

- Archivado de proveedores en estados posteriores a EN_EVALUACION

- Referencia: MOD-009 seccion F (transicion Archivar), C (separacion de funciones)

### HU-009-14. Exportar el paquete de evidencia de un proveedor con verificacion de integridad

**Como** Auditor (interno), **quiero** generar y descargar el paquete de evidencia de un proveedor especifico, con su ficha completa, el contrato vinculado, las evaluaciones de riesgo, las revisiones y las notificaciones enviadas, verificable con una huella de integridad, **para** presentar esa evidencia en la auditoria anual de cumplimiento o ante la ACE si la empresa lo requiere.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 24 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales); OBL-PROV-01 (Art. 33 inc. 2, Ley para la Proteccion de Datos Personales); OBL-PROV-02 (Art. 34, Ley para la Proteccion de Datos Personales); OBL-PROV-03 (Art. 36, Ley para la Proteccion de Datos Personales)
- Depende de: HU-009-01, HU-009-05
- Modulos requeridos: MOD-008

**Criterios de aceptacion**

1. Dado un proveedor con ficha completa, contrato vinculado, evaluaciones de riesgo y revisiones registradas, cuando el Auditor (interno) solicita el paquete de evidencia de ese proveedor, entonces el sistema genera un archivo en PDF y ZIP firmado que incluye esos elementos usando el servicio comun de generacion de huella o firma de integridad de la plataforma
2. Dado un paquete de evidencia generado, cuando se descarga, entonces el sistema registra el evento de exportacion con quien lo exporto, cuando y que version del registro del proveedor se exporto
3. Dado un proveedor con notificaciones enviadas a un Encargado o a un Receptor, cuando se genera su paquete de evidencia, entonces el sistema incluye esas notificaciones con su constancia adjunta
4. Dado un proveedor sin ningun Contrato/DPA vinculado todavia, cuando se solicita su paquete de evidencia, entonces el sistema lo genera igual mostrando de forma explicita que ese elemento esta pendiente, sin fallar la exportacion
5. Dado un usuario con el rol Auditor externo (invitado), cuando solicita el paquete de evidencia, entonces el sistema lo limita a los proveedores que la organizacion incluyo en su invitacion de auditoria puntual
6. Dado un paquete de evidencia ya exportado, cuando alguien intenta modificar su contenido, entonces el sistema no lo permite porque el paquete exportado queda fijo
7. Dado un usuario con el rol Usuario de consulta / Colaborador, cuando intenta exportar el paquete de evidencia de un proveedor, entonces el sistema deniega la accion porque ese rol no tiene permiso de exportar

**Reglas de negocio**

- La huella o firma de integridad se genera con el servicio comun de la plataforma, no con un mecanismo propio de MOD-009
- El evento de exportacion se registra de forma permanente aunque el archivo exportado salga del sistema
- El Auditor externo queda acotado a los proveedores incluidos en su invitacion

**Fuera de alcance**

- La vista consolidada de evidencia por las 105 obligaciones y el informe de huecos (funcionalidad propia de MOD-019)

- Referencia: MOD-009 secciones E, J, N
- Notas: La generacion de la huella o firma de integridad y el formato del paquete (PDF/ZIP) reutilizan el servicio comun de exportacion verificable de EP-000, segun indica el encargo; MOD-009 no construye su propio motor de huella o firma.

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Alta y ficha de Encargado / Tercero-Receptor / Subencargado (bloques D.1 y D.2) | HU-009-01, HU-009-03, HU-009-04 |
| Vinculacion de Contrato/DPA (referencia a MOD-008) | HU-009-05 |
| Flujo de estados con aprobacion de activacion y doble control en riesgo alto | HU-009-04, HU-009-05, HU-009-08, HU-009-11, HU-009-12 |
| Alertas de vencimiento de contrato y de revision periodica | HU-009-07, HU-009-08 |
| Notificacion automatica a Encargado tras revocacion de consentimiento (integracion con MOD-007) | HU-009-09 |
| Notificacion automatica a Receptor tras rectificacion/eliminacion (integracion con MOD-011) | HU-009-10 |
| Datos de contacto del encargado para el aviso de privacidad (integracion con MOD-008) | HU-009-06 |
| Paquete de evidencia exportable por proveedor, con verificacion de integridad | HU-009-14 |
