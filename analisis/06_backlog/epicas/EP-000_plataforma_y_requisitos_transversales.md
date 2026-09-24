# EP-000 Plataforma y requisitos transversales

**Objetivo.** La organizacion cliente puede acceder de forma segura y aislada de las demas organizaciones, confiar en una bitacora de auditoria inalterable y en exportaciones con integridad verificable, aceptar los terminos de uso y el contrato de encargo de tratamiento con el proveedor, y usar el sistema en espanol con la hora y el formato de fecha de El Salvador, desde que el equipo del producto aprovisiona su cuenta hasta que el contrato termina y sus datos se exportan y se eliminan con constancia.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R1 | 19 | 74 | 61 | 13 | No aplica (epica transversal) |

**Notas de la epica.**

- EP-000 no tiene ficha propia en 03_modulos (no existe MOD-000_ficha.md), por eso el campo modulo queda vacio y, en vez de una tabla Q, cobertura_q usa como filas los 14 bloques que lista el encargo (inicio de sesion y recuperacion; doble factor; cierre de sesion por inactividad; aislamiento; AuditLog; servicio comun de exportacion con integridad; descargo legal y terminos de uso; aprovisionamiento; contrato de encargo de tratamiento; aviso de privacidad del producto; acceso de soporte; exportacion y eliminacion al terminar el contrato; zona horaria y formato de fecha; interfaz en espanol).
- El aprovisionamiento de una organizacion cliente nueva (HU-000-05) es distinto del alta que hace el propio Administrador dentro de MOD-003 Onboarding: aqui el equipo del producto crea la cuenta vacia e invita al primer Administrador; MOD-003 es la sesion guiada que esa persona completa despues, y MOD-001 es donde la organizacion pasa de BORRADOR a ACTIVA. La facturacion y el plan comercial contratado quedan fuera del MVP y se gestionan fuera del sistema, tal como declara la propia ficha de MOD-001 seccion A (No gestiona facturacion, suscripcion comercial ni planes de pago de la cuenta SaaS).
- El alcance de doble factor obligatorio (HU-000-08) se fijo, como decision de esta epica y no como un hecho literal de ninguna ficha, para los roles Administrador de la organizacion, Delegado de Proteccion de Datos (o Responsable interno), Responsable ARCO-POL / Responsable del tramite, Responsable Legal / Compliance, Responsable de Seguridad / IT y Auditor (interno), por ser quienes acceden a datos de titulares o de administracion segun la matriz de permisos de 04_secciones/11_roles_y_permisos.md seccion 11.2; el resto de roles puede activarlo de forma voluntaria. Esta lista de roles queda sujeta a validacion del equipo de producto.
- El contrato de encargo de tratamiento (HU-000-12) se fundamenta, segun indica el encargo, en los Arts. 34, 36 y 41 LPDP. Los OBL-ID mas cercanos de la matriz son OBL-PROV-01, OBL-PROV-02 y OBL-PROV-03, redactados en las fichas para el proveedor que la organizacion cliente contrata (propietario MOD-009), no para el proveedor del software mismo; se citan aqui por analogia, porque ninguna obligacion de la matriz modela de forma literal al proveedor del software como encargado de su organizacion cliente. El Art. 41 esta indexado en la matriz como OBL-TRANSF-02, dentro del capitulo de transferencias de datos; se invoca en esta epica solo como fundamento adicional de que la ley exige un contrato con obligaciones equivalentes cuando un responsable entrega datos a otro, no porque este flujo sea una transferencia internacional.
- El acceso del equipo de soporte del proveedor a una cuenta cliente (HU-000-14 y HU-000-15) es una propuesta de 04_secciones/11_roles_y_permisos.md seccion 11.7, marcada ahi mismo como propuesta de esa seccion, no presente en las fichas: la propia ficha de MOD-026 declara el alcance de soporte fuera del alcance funcional de ese analisis. Ambas historias quedan sujetas a validacion del equipo de producto y, en lo referente a datos personales, de asesoria legal, antes de tratarse como regla definitiva del producto.
- La exportacion completa y la eliminacion con constancia de los datos de una organizacion al terminar el contrato (HU-000-16 y HU-000-17) usan por analogia el criterio de OBL-PROV-07 (devolucion o eliminacion de datos por el encargado al finalizar la relacion, RECOMENDADO), aplicado aqui al propio proveedor del software frente a su cliente. Ninguna ficha fija el plazo comercial exacto tras el cual se ejecuta la eliminacion; ese plazo es una decision contractual pendiente, fuera del alcance funcional de este documento, y se deja como parametro configurable.
- El periodo de inactividad que cierra la sesion (HU-000-09, propuesto en 15 minutos) y el umbral de intentos fallidos de inicio de sesion antes del bloqueo temporal (HU-000-06) son opinion de producto sin respaldo legal expreso, con el mismo estilo de los valores por defecto que ya propone MOD-001 (30 dias de vigencia de invitacion, umbral de 50 empleados); quedan sujetos a validacion del equipo de producto.
- Todas las historias de esta epica se clasifican en release R1 porque son condicion de uso seguro del sistema desde el primer cliente, sin importar si los modulos de negocio que ese cliente use ya estan en R1 o llegan en R2.
- Release ajustado de R1 a R2 en la planificacion: la exportacion y eliminacion al terminar el contrato se necesitan antes del primer vencimiento de contrato, no para la primera venta.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-000-01 | Aislar los datos entre organizaciones clientes | Administrador de la organizacion | 8 | R1 | 1 | - |
| HU-000-02 | Registrar cada accion relevante en la bitacora de auditoria | Auditor (interno) | 8 | R1 | 1 | - |
| HU-000-03 | Consultar la bitacora de auditoria | Auditor (interno) | 3 | R1 | 20 | HU-000-02 |
| HU-000-04 | Generar huella de integridad y manifiesto al exportar | Auditor (interno) | 5 | R1 | 2 | HU-000-02 |
| HU-000-05 | Aprovisionar una organizacion cliente nueva | Equipo del producto (proveedor) | 3 | R1 | 20 | HU-000-02 |
| HU-000-06 | Iniciar sesion con credenciales propias | Usuario de consulta / Colaborador | 3 | R1 | 2 | HU-000-02 |
| HU-000-07 | Recuperar el acceso cuando se olvida la contrasena | Usuario de consulta / Colaborador | 3 | R1 | 20 | HU-000-06, HU-000-02 |
| HU-000-08 | Exigir doble factor de autenticacion en roles sensibles | Responsable de Seguridad / IT | 5 | R1 | 21 | HU-000-06, HU-000-02 |
| HU-000-09 | Cerrar la sesion automaticamente por inactividad | Usuario de consulta / Colaborador | 3 | R1 | 21 | HU-000-06 |
| HU-000-10 | Mostrar el descargo legal del sistema | Usuario de consulta / Colaborador | 1 | R1 | 5 | - |
| HU-000-11 | Aceptar los terminos de uso | Usuario de consulta / Colaborador | 3 | R1 | 21 | HU-000-02 |
| HU-000-12 | Aceptar el contrato de encargo de tratamiento | Administrador de la organizacion | 3 | R1 | 21 | HU-000-02, HU-000-05 |
| HU-000-13 | Consultar el aviso de privacidad del producto | Usuario de consulta / Colaborador | 2 | R1 | 19 | - |
| HU-000-14 | Autorizar un acceso temporal de soporte | Administrador de la organizacion | 3 | R1 | 21 | HU-000-02 |
| HU-000-15 | Usar el acceso temporal de soporte autorizado | Equipo de soporte del producto (proveedor) | 5 | R1 | 21 | HU-000-14, HU-000-02, HU-000-01 |
| HU-000-16 | Exportar todos los datos de la organizacion al finalizar el contrato | Administrador de la organizacion | 8 | R2 | 36 | HU-000-04, HU-000-02 |
| HU-000-17 | Eliminar los datos de una organizacion tras finalizar el contrato | Equipo del producto (proveedor) | 5 | R2 | 36 | HU-000-16, HU-000-02 |
| HU-000-18 | Ver fechas y horas en el huso horario de El Salvador | Usuario de consulta / Colaborador | 2 | R1 | 21 | - |
| HU-000-19 | Usar el sistema en espanol | Usuario de consulta / Colaborador | 1 | R1 | 6 | - |

## Historias

### HU-000-01. Aislar los datos entre organizaciones clientes

**Como** Administrador de la organizacion, **quiero** que ningun usuario de otra organizacion cliente pueda ver, buscar, listar ni exportar datos de mi organizacion, y que mi organizacion tampoco pueda ver los de otra, **para** tener la certeza de que la informacion de mi empresa esta separada por completo de la de otros clientes que usan la misma plataforma.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 1 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un usuario autenticado con sesion activa en la Organizacion A, cuando consulta cualquier listado, expediente, tarea, alerta, reporte o resultado de busqueda dentro del sistema, entonces el resultado nunca incluye registros que pertenecen a la Organizacion B.
2. Dado que un usuario de la Organizacion A conoce o adivina el identificador de un expediente, documento o registro que pertenece a la Organizacion B, cuando intenta abrirlo de forma directa, entonces el sistema responde como si ese registro no existiera, sin confirmar ni negar su existencia.
3. Dado un reporte o un paquete exportado por un usuario de la Organizacion A, cuando el archivo se genera, entonces su contenido nunca incluye registros de otra organizacion, aunque los filtros elegidos coincidan con datos de otra organizacion.
4. Dado un evento generado por cualquier otro modulo (una tarea, una alerta, una notificacion o un evento de la bitacora de auditoria), cuando el sistema lo crea, entonces ese evento queda asociado a exactamente una organizacion y solo es visible para los usuarios de esa organizacion.
5. Dado un Auditor externo (invitado) o un Asesor externo invitado con acceso vigente a la Organizacion A, cuando consulta el sistema dentro de su ventana de invitacion, entonces solo ve informacion de la Organizacion A, incluso si la misma persona tiene otra invitacion vigente en una Organizacion C distinta.
6. Dado que el equipo de soporte del producto (proveedor) no tiene un acceso temporal autorizado y vigente sobre la Organizacion A, cuando cualquiera de sus integrantes intenta consultar informacion de esa organizacion, entonces el sistema deniega el acceso de la misma forma que a cualquier otro usuario ajeno a esa organizacion.

**Reglas de negocio**

- Toda entidad de negocio (tratamiento, expediente, tarea, evidencia, documento, evento de auditoria) pertenece a exactamente una organizacion cliente, sin excepcion (principio de propietario unico aplicado a nivel de organizacion, 04_secciones/09_modelo_conceptual.md seccion 9.6).
- El sistema no ofrece en el MVP una vista consolidada que fusione registros de varias organizaciones: una vista de ese tipo, si existe, seria una capa de agregacion de solo lectura fuera de esta epica, nunca una fusion de registros.
- Negar el acceso a un registro de otra organizacion nunca revela si ese registro existe o no.

**Fuera de alcance**

- Permitir que una misma persona cambie entre varias organizaciones no relacionadas entre si dentro de una misma cuenta (perfil de Delegado externo que atiende a varios clientes): es un hueco documentado en 04_secciones/09_modelo_conceptual.md, sin mecanismo definido, pendiente de validacion de producto
- Vision consolidada de un grupo corporativo con varias razones sociales: fuera del MVP (decision de alcance 2.7.31)
- La arquitectura tecnica concreta que garantiza el aislamiento (fuera del alcance funcional de este blueprint)

- Referencia: 04_secciones/09_modelo_conceptual.md seccion 9.6; 04_secciones/23_riesgos_del_producto.md RIESGO-SEG-01 y RIESGO-SEG-07; 04_secciones/11_roles_y_permisos.md seccion 11.5
- Notas: 04_secciones/23_riesgos_del_producto.md (RIESGO-SEG-07) marca la validacion final del aislamiento como una decision de arquitectura tecnica fuera del alcance de este blueprint; esta historia fija el comportamiento observable que esa arquitectura debe cumplir, sin nombrar como se implementa.

### HU-000-02. Registrar cada accion relevante en la bitacora de auditoria

**Como** Auditor (interno), **quiero** que el sistema registre automaticamente, en una bitacora unica de solo adicion, toda creacion, cambio de estado, aprobacion, rechazo, exportacion, intento bloqueado y lectura de informacion sensible que ocurra en cualquier modulo, **para** poder demostrar en cualquier momento quien hizo que, cuando y con que resultado, sin que nadie pueda alterar ese registro despues.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 1 | Si |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que en cualquier modulo ocurre una creacion, un cambio de estado, una aprobacion, un rechazo, una exportacion o un intento bloqueado o rechazado, cuando ese evento ocurre, entonces la bitacora de auditoria (AuditLog) agrega una entrada nueva con la marca de tiempo, el usuario o Sistema, el modulo y la entidad afectada, el tipo de evento y, cuando aplique, el valor anterior y el valor nuevo.
2. Dado que una automatizacion del sistema ejecuta una accion sin que una persona la dispare directamente, cuando esa accion ocurre, entonces la bitacora registra el evento con Sistema como usuario, en vez de dejarlo sin registrar.
3. Dado que alguien consulta una Evidencia marcada con nivel de sensibilidad Datos personales sensibles o Informacion tecnica de seguridad sensible, cuando abre esa Evidencia, entonces la bitacora registra quien la consulto y cuando, ademas de cualquier otro evento sobre ella.
4. Dado un evento ya registrado en la bitacora, cuando cualquier rol, incluido el Administrador de la organizacion, intenta editarlo o eliminarlo, entonces el sistema rechaza la accion sin excepcion, porque la bitacora es de solo escritura por adicion.
5. Dado que un modulo de negocio queda deshabilitado, archivado o dado de baja, cuando eso ocurre, entonces los eventos que ya existen en la bitacora para ese modulo permanecen intactos y consultables.
6. Dado que se activa o revierte la bandera del doble estado de la reforma 659, cuando ese cambio ocurre, entonces la bitacora registra el evento con quien lo autorizo y la fecha, igual que cualquier otro cambio de estado relevante.

**Reglas de negocio**

- El AuditLog es una bitacora de solo escritura por adicion (append-only), sin funcion de edicion ni borrado para ningun rol, ni siquiera el Administrador (02_validacion/22_anti_features.md item 19; 04_secciones/13_evidencia_y_auditoria.md seccion 13.3.4).
- El AuditLog no tiene modulo propietario unico: cada modulo escribe sus propios eventos (04_secciones/13_evidencia_y_auditoria.md seccion 13.3.1).
- Los campos minimos de cada evento son marca de tiempo, usuario o Sistema, modulo y entidad de origen, tipo de evento, valor anterior y nuevo cuando aplique, y motivo cuando la accion de origen lo exige (04_secciones/13_evidencia_y_auditoria.md seccion 13.3.3, propuesta de esa seccion a partir del patron repetido en las fichas).
- Cada evento se conserva, como minimo, el mismo plazo que el registro o expediente al que pertenece (04_secciones/13_evidencia_y_auditoria.md seccion 13.3.6).

**Fuera de alcance**

- Definir la estructura de campos como una entidad formal con pantalla propia de edicion: no existe, porque el AuditLog no se edita
- El plazo de purga o retencion definitivo del AuditLog cuando el registro de origen no tiene todavia un plazo propio: hueco documentado en 04_secciones/09_modelo_conceptual.md, pendiente de que MOD-016 lo defina

- Referencia: 04_secciones/13_evidencia_y_auditoria.md secciones 13.1.3, 13.3.1 a 13.3.8; 02_validacion/22_anti_features.md item 19; 04_secciones/09_modelo_conceptual.md seccion 9.1.5

### HU-000-03. Consultar la bitacora de auditoria

**Como** Auditor (interno), **quiero** consultar y filtrar la bitacora de auditoria de todos los modulos por modulo, usuario, tipo de evento y periodo, **para** poder revisar quien hizo que y cuando durante una revision interna o una auditoria, sin depender de pedirlo modulo por modulo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 20 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-000-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el Auditor (interno) abre la consulta de la bitacora de auditoria, cuando aplica un filtro por modulo, por usuario, por tipo de evento o por un rango de fechas, entonces el sistema muestra solo los eventos de su propia organizacion que cumplen esos filtros.
2. Dado que el Administrador de la organizacion abre la misma consulta, cuando la usa, entonces tambien puede ver y filtrar la bitacora completa de su organizacion, en modo de solo lectura.
3. Dado un usuario que no tiene el rol Auditor (interno) ni el rol Administrador de la organizacion, cuando intenta abrir la consulta general de la bitacora de auditoria, entonces el sistema deniega el acceso a esa vista general.
4. Dado que el Auditor (interno) o el Administrador consulta un evento de la bitacora, cuando revisa la pantalla, entonces no encuentra ninguna opcion para editar, anotar sobre, ocultar o eliminar ese evento.
5. Dado que el Auditor externo (invitado) tiene una invitacion vigente y acotada a un caso o modulo especifico, cuando consulta la bitacora, entonces solo ve los eventos relacionados con ese caso o modulo, no la bitacora completa de la organizacion.

**Reglas de negocio**

- El AuditLog es visible para Auditor y Administrador (02_validacion/22_anti_features.md item 19; 04_secciones/13_evidencia_y_auditoria.md seccion 13.3.5).
- El rol Auditor, interno o externo, es siempre de solo lectura sobre la bitacora (04_secciones/13_evidencia_y_auditoria.md seccion 13.3.5).
- Cada ficha de modulo tambien muestra, dentro de su propio historial, los eventos que le corresponden a los roles que ya tienen acceso a ese expediente; esta consulta transversal no reemplaza esa vista propia de cada modulo.

**Fuera de alcance**

- Una exportacion del AuditLog completo sin acotarlo a una obligacion o a un expediente: hueco documentado en 04_secciones/13_evidencia_y_auditoria.md seccion 13.3.7; toda exportacion pasa por el servicio comun de exportacion (HU-000-04) dentro de un paquete de un modulo especifico
- El historial propio de cada modulo (por ejemplo el historial de altas y bajas de usuarios de MOD-001): sigue viviendo dentro de cada ficha

- Referencia: 04_secciones/13_evidencia_y_auditoria.md secciones 13.3.5 y 13.3.7

### HU-000-04. Generar huella de integridad y manifiesto al exportar

**Como** Auditor (interno), **quiero** que todo modulo que exporte un paquete de archivos obtenga, del mismo servicio comun, una huella de integridad por archivo y un manifiesto del conjunto completo, **para** poder demostrar despues, ante la organizacion, un cliente o la ACE, que un paquete exportado no fue alterado tras su salida del sistema.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 2 | Si |

- Fundamento: OBL-RET-06 (Art. 13-A, Ley de Firma Electronica)
- Depende de: HU-000-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que un modulo solicita exportar uno o varios archivos como un paquete, cuando el servicio comun de exportacion procesa la solicitud, entonces calcula una huella de integridad individual para cada archivo incluido.
2. Dado que ya se calculo la huella de cada archivo del paquete, cuando el servicio termina de procesarlos, entonces genera ademas un manifiesto unico que lista cada archivo con su huella y una huella global del conjunto completo.
3. Dado un archivo exportado junto con su huella y su manifiesto, cuando alguien recalcula la huella de ese archivo mas adelante, entonces la huella coincide con la original si el archivo no cambio, y no coincide si el archivo fue alterado.
4. Dado que el calculo de la huella de alguno de los archivos del paquete falla o queda incompleto, cuando el servicio comun termina de procesar la solicitud, entonces el paquete no queda disponible para descarga hasta que todas las huellas y el manifiesto se completen correctamente.
5. Dado que un paquete ya fue exportado con su manifiesto, cuando alguien intenta modificar su contenido despues de exportado, entonces el sistema no ofrece ninguna forma de editar ese paquete ya exportado: cualquier cambio de alcance exige generar un paquete nuevo.
6. Dado que el servicio comun de exportacion genera un paquete para cualquier modulo, cuando el paquete se genera, entonces la bitacora de auditoria registra quien lo solicito, cuando y de que modulo u organizacion.

**Reglas de negocio**

- Todo paquete de evidencias exportado incluye un mecanismo propio de verificacion de integridad, obligatorio y no configurable para destinos externos (02_validacion/22_anti_features.md item 25).
- El paquete calcula un manifiesto con la huella de cada archivo incluido y la huella del conjunto; al aprobarse, calcula ademas una huella o firma del paquete completo (04_secciones/13_evidencia_y_auditoria.md seccion 13.5.2).
- Un paquete ya exportado nunca se modifica: cualquier cambio de alcance exige generar un paquete nuevo (04_secciones/13_evidencia_y_auditoria.md seccion 13.5.3).
- Este servicio es agnostico del contenido: no decide que se exporta ni aplica reglas de aprobacion o de doble control propias de un modulo, eso lo define cada modulo que lo usa (por ejemplo, el doble control para destinos externos de MOD-019).

**Fuera de alcance**

- Los tipos de paquete, sus filtros y el doble control para destinos externos: son reglas propias de cada modulo consumidor, por ejemplo el EvidencePackage de MOD-019 (R2)
- El formato final de descarga del archivo exportado

- Referencia: 04_secciones/13_evidencia_y_auditoria.md seccion 13.5.2 y 13.5.4; 02_validacion/22_anti_features.md item 25; 04_secciones/23_riesgos_del_producto.md RIESGO-SEG-05
- Notas: Este servicio es la capacidad comun que MOD-001 (exportacion firmada de usuarios), MOD-019 (EvidencePackage) y cualquier otro modulo con exportacion reutilizan; cada modulo consumidor declara esta dependencia con depende_de_modulos: ["EP-000"] en su propia epica.

### HU-000-05. Aprovisionar una organizacion cliente nueva

**Como** Equipo del producto (proveedor), **quiero** dar de alta la cuenta de una organizacion cliente nueva e invitar a la persona que sera su primer Administrador de la organizacion, **para** que esa empresa pueda empezar a usar el sistema sin depender de una tarea tecnica manual, sin registrar todavia ningun dato de facturacion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 20 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-000-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el equipo del producto (proveedor) recibe un cliente nuevo con su razon social y el correo de la persona que sera su primer Administrador, cuando registra el alta, entonces el sistema crea una cuenta de organizacion vacia y envia una invitacion unica a esa persona.
2. Dado que ya existe una organizacion registrada previamente con la misma razon social o la misma identificacion tributaria, cuando el equipo del producto intenta darla de alta otra vez, entonces el sistema rechaza el alta duplicada y muestra la organizacion existente en vez de crear una nueva.
3. Dado que la invitacion al primer Administrador no se acepta dentro de 30 dias, cuando se cumple ese plazo, entonces la invitacion queda vencida y el equipo del producto puede reenviarla sin tener que dar de alta la organizacion otra vez.
4. Dado que la persona invitada acepta la invitacion, cuando confirma sus datos, entonces esa persona queda activa con el rol Administrador de la organizacion y la organizacion queda disponible para completar su alta en el modulo de Organizacion y Personas.
5. Dado que el equipo del producto completa el aprovisionamiento de una organizacion, cuando lo hace, entonces el sistema no pide ni guarda ningun dato de plan comercial, precio o facturacion, porque esa gestion se hace fuera del sistema.
6. Dado que se aprovisiona una organizacion nueva, cuando el alta se registra, entonces la bitacora de auditoria guarda quien la creo dentro del equipo del producto, la fecha y la organizacion afectada.

**Reglas de negocio**

- El aprovisionamiento de la cuenta es un acto del equipo del producto (proveedor), distinto y anterior al asistente de onboarding que completa el Administrador dentro de MOD-003.
- La facturacion, el plan comercial y la suscripcion de la cuenta SaaS quedan fuera del alcance funcional del sistema (03_modulos/MOD-001_ficha.md seccion A).
- Una organizacion aprovisionada sin que su primer Administrador acepte la invitacion no puede operar ningun otro modulo.

**Fuera de alcance**

- Completar el resto de la ficha de organizacion (sucursales, unidades, numero de empleados): eso ocurre en MOD-003 Onboarding y MOD-001
- Cualquier dato de facturacion, plan contratado o forma de pago
- La gestion de grupos multi-sociedad (fuera del MVP)

- Requiere contenido: Texto del correo de invitacion inicial al primer Administrador de una organizacion nueva
- Referencia: 03_modulos/MOD-001_ficha.md seccion A (limites) y seccion L (Entra desde MOD-003); 04_secciones/19_21_roadmap_mvp_v1_v2.md seccion 19.9

### HU-000-06. Iniciar sesion con credenciales propias

**Como** Usuario de consulta / Colaborador, **quiero** iniciar sesion con mi correo y mi contrasena, **para** acceder al sistema con los permisos de mi rol o roles asignados.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 2 | No |

- Fundamento: OBL-SEG-03 (Art. 4 (Medidas Tecnicas), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: HU-000-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un usuario en estado Activo que ingresa su correo y su contrasena correctos, cuando confirma el inicio de sesion, entonces el sistema le da acceso con los permisos de su rol o roles asignados.
2. Dado un usuario que ingresa un correo o una contrasena incorrectos, cuando confirma el inicio de sesion, entonces el sistema deniega el acceso con un mensaje generico, sin indicar si el correo existe o si el campo equivocado fue el correo o la contrasena.
3. Dado un usuario en estado Suspendido o Dado de baja que ingresa credenciales correctas, cuando intenta iniciar sesion, entonces el sistema deniega el acceso con un mensaje generico, sin revelar el estado exacto de la cuenta.
4. Dado que un mismo correo acumula varios intentos fallidos consecutivos de inicio de sesion, cuando se supera el limite definido, entonces el sistema bloquea temporalmente los intentos desde ese correo antes de permitir uno nuevo.
5. Dado un intento de inicio de sesion, exitoso o fallido, cuando ocurre, entonces la bitacora de auditoria registra el correo utilizado, el resultado y la fecha y hora.

**Reglas de negocio**

- El estado del usuario (Invitado, Activo, Suspendido, Dado de baja) lo administra MOD-001; esta historia solo consulta ese estado para decidir si permite el acceso.
- El sistema nunca revela, en un mensaje de error de inicio de sesion, si el correo ingresado existe o cual campo especifico fallo.
- Las Politicas de Actuacion de la ACE exigen control de acceso como medida tecnica minima (00_contexto_para_agentes.md seccion 3).

**Fuera de alcance**

- Gestionar el estado del usuario (invitar, suspender, dar de baja): eso lo define MOD-001
- El segundo factor de autenticacion para roles sensibles: ver HU-000-08
- El cierre de sesion por inactividad: ver HU-000-09

- Referencia: 00_contexto_para_agentes.md seccion 3 (Politicas ACE, medidas tecnicas); 03_modulos/MOD-001_ficha.md seccion F.2 (estados de Usuario)

### HU-000-07. Recuperar el acceso cuando se olvida la contrasena

**Como** Usuario de consulta / Colaborador, **quiero** solicitar un enlace para restablecer mi contrasena cuando la olvido, **para** recuperar el acceso a mi cuenta sin depender de que el Administrador me reinvite.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 20 | No |

- Fundamento: OBL-SEG-03 (Art. 4 (Medidas Tecnicas), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: HU-000-06, HU-000-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un usuario que ya no recuerda su contrasena, cuando solicita restablecerla con su correo registrado, entonces el sistema envia un enlace de un solo uso a ese correo.
2. Dado que se solicita restablecer la contrasena de un correo que no esta registrado en el sistema, cuando se envia la solicitud, entonces el sistema muestra el mismo mensaje generico de confirmacion que si el correo existiera, sin revelar si esta registrado.
3. Dado un enlace de restablecimiento vigente, cuando el usuario lo abre y define una contrasena nueva, entonces el sistema actualiza la contrasena y cierra cualquier sesion anterior de esa cuenta que siguiera activa.
4. Dado un enlace de restablecimiento ya usado o vencido por el paso del tiempo, cuando alguien intenta abrirlo de nuevo, entonces el sistema lo rechaza y pide solicitar uno nuevo.
5. Dado un usuario en estado Suspendido o Dado de baja, cuando solicita restablecer su contrasena, entonces el sistema no le entrega acceso, sin revelar el estado exacto de la cuenta.
6. Dado que se solicita o se completa un restablecimiento de contrasena, cuando ocurre cualquiera de los dos eventos, entonces la bitacora de auditoria lo registra con el correo, el resultado y la fecha y hora.

**Reglas de negocio**

- El enlace de restablecimiento es de un solo uso y tiene una vigencia corta y definida.
- Restablecer la contrasena cierra cualquier sesion previa de esa cuenta, para que un tercero que hubiera accedido antes pierda el acceso.
- El sistema nunca revela, en la respuesta a una solicitud de recuperacion, si un correo especifico existe en la cuenta.

**Fuera de alcance**

- Reactivar una cuenta Suspendida o Dada de baja: eso lo decide el Administrador en MOD-001
- El segundo factor de autenticacion, si el usuario tiene un rol que lo exige (ver HU-000-08)

- Requiere contenido: Texto del correo con el enlace de restablecimiento de contrasena
- Referencia: 00_contexto_para_agentes.md seccion 3 (Politicas ACE, medidas tecnicas)

### HU-000-08. Exigir doble factor de autenticacion en roles sensibles

**Como** Responsable de Seguridad / IT, **quiero** que el sistema exija un segundo factor de autenticacion, ademas de la contrasena, a los roles con acceso a datos de titulares o de administracion, **para** reforzar el control de acceso tecnico que exigen las Politicas de Actuacion de la ACE para la informacion mas sensible de cada organizacion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 21 | No |

- Fundamento: OBL-SEG-03 (Art. 4 (Medidas Tecnicas), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: HU-000-06, HU-000-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un usuario al que se le asigna por primera vez uno de los roles con acceso a datos de titulares o de administracion (Administrador de la organizacion, Delegado de Proteccion de Datos o Responsable interno, Responsable ARCO-POL, Responsable Legal / Compliance, Responsable de Seguridad / IT o Auditor interno), cuando inicia sesion despues de esa asignacion, entonces el sistema le exige configurar un segundo factor antes de continuar.
2. Dado un usuario que ya configuro su segundo factor y tiene asignado alguno de esos roles, cuando inicia sesion con su correo y su contrasena correctos, entonces el sistema le exige ademas verificar el segundo factor antes de dar acceso.
3. Dado que el segundo factor ingresado no es valido, cuando el usuario lo confirma, entonces el sistema deniega el acceso y permite reintentar dentro de un limite de intentos.
4. Dado un usuario con uno de los roles sensibles al que se le retira ese rol y no le queda ningun otro rol sensible asignado, cuando inicia sesion despues del cambio, entonces el sistema deja de exigirle el segundo factor, sin borrar su configuracion previa.
5. Dado un Administrador de la organizacion, cuando intenta desactivar la exigencia de segundo factor para su propio usuario o para otro usuario que mantiene un rol sensible, entonces el sistema no permite desactivarla mientras ese rol sensible siga asignado.
6. Dado que un usuario pierde el acceso a su segundo factor, cuando usa un codigo de respaldo de un solo uso entregado al momento de configurarlo, entonces el sistema le permite iniciar sesion y le pide configurar un segundo factor nuevo.

**Reglas de negocio**

- Las Politicas de Actuacion de la ACE incluyen, dentro de las medidas tecnicas minimas, control de acceso con autenticacion en dos pasos (2FA) (00_contexto_para_agentes.md seccion 3; 01_legal/fuentes/ace_politicas_protecciondatos.txt).
- El conjunto de roles obligados a segundo factor es una decision de esta epica (ver notas_epica), no un listado literal de ninguna ficha.
- El segundo factor no se puede desactivar de forma administrativa mientras el usuario mantenga asignado un rol dentro del conjunto obligado.

**Fuera de alcance**

- El mecanismo tecnico concreto del segundo factor
- Extender la exigencia a roles fuera del conjunto obligado: la organizacion puede activarlo de forma voluntaria, pero no es parte de esta historia

- Referencia: 00_contexto_para_agentes.md seccion 3 (Politicas ACE, medidas tecnicas); 04_secciones/11_roles_y_permisos.md seccion 11.2 (matriz de permisos por rol)
- Notas: La lista de roles obligados (ver notas_epica) es una interpretacion de esta epica a partir de OBL-SEG-03 y de la matriz de 11.2; queda sujeta a validacion del equipo de producto.

### HU-000-09. Cerrar la sesion automaticamente por inactividad

**Como** Usuario de consulta / Colaborador, **quiero** que mi sesion se cierre sola despues de un periodo sin actividad, con un aviso previo, **para** que nadie mas pueda usar el sistema con mi acceso si dejo mi sesion abierta sin vigilancia.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 21 | No |

- Fundamento: OBL-SEG-03 (Art. 4 (Medidas Tecnicas), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: HU-000-06
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un usuario con sesion activa que no realiza ninguna accion durante el periodo de inactividad configurado (15 minutos, propuesta inicial), cuando se cumple ese periodo, entonces el sistema cierra la sesion de forma automatica.
2. Dado que se acerca el limite de inactividad, cuando faltan los ultimos instantes antes del cierre automatico, entonces el sistema muestra un aviso previo que permite continuar la sesion con una sola confirmacion.
3. Dado que el usuario confirma el aviso previo o realiza cualquier accion dentro del sistema, cuando lo hace, entonces el contador de inactividad se reinicia y la sesion sigue activa.
4. Dado que la sesion se cerro por inactividad, cuando el usuario quiere seguir usando el sistema, entonces debe autenticarse de nuevo con sus credenciales, incluido el segundo factor si su rol lo exige.
5. Dado un usuario que esta completando un formulario largo y sigue interactuando con la pantalla antes de guardar, cuando transcurre el periodo de inactividad configurado sin que haya guardado nada, entonces el sistema aplica el mismo cierre automatico, sin excepcion por el tipo de pantalla abierta.

**Reglas de negocio**

- El periodo de inactividad por defecto (15 minutos) es opinion de producto sin respaldo legal expreso, ajustable por el equipo del producto dentro de un rango predefinido.
- Cerrar la sesion por inactividad es una medida tecnica de control de acceso alineada con las Politicas de Actuacion de la ACE (00_contexto_para_agentes.md seccion 3).

**Fuera de alcance**

- Guardar de forma automatica el contenido de un formulario antes de cerrar la sesion: cada modulo decide si ofrece guardado progresivo (por ejemplo, el estado Borrador de varios modulos)
- El bloqueo temporal por intentos fallidos de inicio de sesion: ver HU-000-06

- Referencia: 00_contexto_para_agentes.md seccion 3 (Politicas ACE, medidas tecnicas)

### HU-000-10. Mostrar el descargo legal del sistema

**Como** Usuario de consulta / Colaborador, **quiero** ver siempre visible un descargo que aclare que el sistema organiza y documenta mi programa de proteccion de datos, pero no constituye asesoria legal ni garantiza el cumplimiento de la ley, **para** entender desde el primer momento los limites de lo que el sistema hace y no confundirlo con asesoria juridica.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 1 | R1 | 5 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado cualquier usuario con sesion activa, cuando navega por el sistema, entonces encuentra siempre visible o alcanzable en un solo paso el texto de descargo general del producto.
2. Dado el texto de descargo visible, cuando el usuario quiere leerlo completo, entonces puede abrir su version completa sin salir del sistema.
3. Dado cualquier rol, incluido el Administrador de la organizacion, cuando intenta quitar el descargo de forma permanente para toda la organizacion, entonces el sistema no ofrece esa opcion.
4. Dado que el equipo de contenido del producto (proveedor) publica una version nueva del texto de descargo, cuando la publica, entonces el sistema muestra la version vigente a todos los usuarios sin que cada organizacion deba activarla.

**Reglas de negocio**

- El sistema no debe afirmar que la empresa esta en cumplimiento de la ley ni actuar como si sustituyera asesoria juridica (02_validacion/04_objetivo_exacto_del_producto.md secciones 1.2 y 1.3).
- El texto de descargo es una propuesta de redaccion de producto, no un formato exigido por la ACE (02_validacion/04_objetivo_exacto_del_producto.md seccion 1.3).

**Fuera de alcance**

- Los descargos especificos de un modulo o de un resultado concreto (por ejemplo, al generar un documento o al calcular un plazo ambiguo): esos los define cada modulo de negocio
- La aceptacion formal de terminos de uso: ver HU-000-11

- Requiere contenido: Texto exacto del descargo legal general del producto (banner y version completa)
- Referencia: 02_validacion/04_objetivo_exacto_del_producto.md secciones 1.2 y 1.3; 02_validacion/22_anti_features.md item 22

### HU-000-11. Aceptar los terminos de uso

**Como** Usuario de consulta / Colaborador, **quiero** aceptar los terminos de uso del sistema antes de usarlo por primera vez, **para** dejar constancia de que conozco y acepto las condiciones bajo las que uso la plataforma.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 21 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-000-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un usuario que inicia sesion por primera vez, cuando entra al sistema, entonces el sistema le muestra los terminos de uso vigentes y no le permite continuar hasta que los acepte.
2. Dado que el usuario acepta los terminos de uso, cuando confirma la aceptacion, entonces el sistema registra su identidad, la fecha y hora, y la version exacta del texto aceptado.
3. Dado un usuario que no acepta los terminos de uso, cuando intenta continuar sin aceptarlos, entonces el sistema le permite unicamente cerrar sesion, sin darle acceso a ningun otro modulo.
4. Dado que se publica una version nueva de los terminos de uso, cuando un usuario que ya habia aceptado una version anterior vuelve a iniciar sesion, entonces el sistema le pide aceptar la version nueva antes de continuar, sin borrar el registro de su aceptacion anterior.
5. Dado que se acepta una version de los terminos de uso, cuando ocurre, entonces la bitacora de auditoria registra el evento con el usuario, la version y la fecha y hora.

**Reglas de negocio**

- Nada que ya se acepto se sobrescribe: cada aceptacion queda con su propia version y fecha (04_secciones/09_modelo_conceptual.md seccion 9.1.4, principio de versionado).

**Fuera de alcance**

- El contrato de encargo de tratamiento entre el proveedor y la organizacion cliente: ver HU-000-12
- El aviso de privacidad del propio producto: ver HU-000-13

- Requiere contenido: Texto completo de los terminos de uso del producto, redactado y validado por asesoria legal del proveedor
- Requiere validacion legal: Si
- Referencia: 02_validacion/04_objetivo_exacto_del_producto.md seccion 1.1 (que el sistema no hace); 04_secciones/09_modelo_conceptual.md seccion 9.1.4

### HU-000-12. Aceptar el contrato de encargo de tratamiento

**Como** Administrador de la organizacion, **quiero** aceptar, en nombre de mi organizacion, el contrato de encargo de tratamiento con el proveedor del software, **para** dejar constancia de que el proveedor trata los datos que mi organizacion registra en el sistema como encargado, bajo las mismas obligaciones de la LPDP que le corresponden a esa figura.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 21 | No |

- Fundamento: OBL-PROV-01 (Art. 33 inc. 2, Ley para la Proteccion de Datos Personales); OBL-PROV-02 (Art. 34, Ley para la Proteccion de Datos Personales); OBL-PROV-03 (Art. 36, Ley para la Proteccion de Datos Personales)
- Depende de: HU-000-02, HU-000-05
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que la organizacion todavia no acepto el contrato de encargo de tratamiento vigente, cuando el Administrador de la organizacion intenta avanzar mas alla del aprovisionamiento inicial, entonces el sistema le exige revisar y aceptar ese contrato antes de continuar.
2. Dado que el Administrador de la organizacion acepta el contrato, cuando confirma la aceptacion, entonces el sistema registra su identidad, la fecha y hora, la organizacion y la version exacta del texto aceptado.
3. Dado que el Administrador de la organizacion no acepta el contrato, cuando intenta continuar sin aceptarlo, entonces la organizacion permanece sin poder operar los demas modulos del sistema.
4. Dado que el proveedor publica una version nueva del contrato de encargo de tratamiento, cuando una organizacion que ya habia aceptado una version anterior inicia sesion, entonces el sistema le pide aceptar la version nueva, conservando sin cambios el registro de la aceptacion anterior.
5. Dado que se acepta una version del contrato de encargo de tratamiento, cuando ocurre, entonces la bitacora de auditoria registra el evento con el Administrador que acepto, la organizacion, la version y la fecha y hora.
6. Dado que el Auditor (interno) de la organizacion quiere confirmar que el contrato esta aceptado, cuando consulta la evidencia de la organizacion, entonces encuentra el registro de aceptacion vigente con su version y su fecha.

**Reglas de negocio**

- El proveedor del software es encargado del tratamiento de los datos que la organizacion cliente registra en el sistema, bajo las mismas obligaciones que la LPDP impone al encargado (Arts. 34, 36 y 41 LPDP; ver notas_epica sobre la correspondencia con OBL-PROV-01 a 03).
- El contrato se acepta por organizacion, no por cada usuario individual, porque obliga a la organizacion como responsable del tratamiento frente al proveedor.

**Fuera de alcance**

- La redaccion juridica del contrato: la produce el equipo legal del proveedor
- Los terminos de uso de la plataforma: ver HU-000-11
- Los contratos de encargo entre la organizacion cliente y sus propios proveedores (encargados): eso es MOD-009, modulo de negocio distinto

- Requiere contenido: Plantilla del contrato de encargo de tratamiento entre el proveedor y la organizacion cliente, validada por asesoria legal, con las clausulas minimas de los Arts. 34, 36 y 41 LPDP
- Requiere validacion legal: Si
- Referencia: 01_legal/fuentes/ace_decreto_144.txt Arts. 34, 36 y 41; 04_secciones/13_evidencia_y_auditoria.md tabla PROV (seccion 13.2)
- Notas: Los Arts. 34 y 36 corresponden en la matriz a OBL-PROV-02 y OBL-PROV-03; el Art. 41 esta indexado como OBL-TRANSF-02 (contrato con el receptor en una transferencia). Se citan los tres por instruccion del encargo, con la aclaracion de analogia que detalla notas_epica.

### HU-000-13. Consultar el aviso de privacidad del producto

**Como** Usuario de consulta / Colaborador, **quiero** consultar el aviso de privacidad del propio producto, sobre como el proveedor trata mis datos como usuario de la plataforma, **para** conocer mis derechos frente al proveedor del software, de forma separada del aviso de privacidad que mi propia organizacion publica para sus titulares.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 19 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado cualquier usuario del sistema, cuando busca el aviso de privacidad del producto, entonces lo encuentra alcanzable desde cualquier pantalla, sin que la consulta exija ninguna aprobacion previa.
2. Dado el aviso de privacidad del producto, cuando el usuario lo abre, entonces ve la version vigente con su fecha de publicacion y puede ver que dice sobre el tratamiento de sus datos como usuario de la plataforma.
3. Dado el aviso de privacidad del producto y el Aviso de Privacidad que la organizacion cliente publica para sus propios titulares en el modulo de Documentos y Politicas, cuando un usuario ve cualquiera de los dos, entonces el sistema los presenta de forma distinguible, sin mezclarlos en la misma pantalla.
4. Dado que el proveedor publica una version nueva del aviso de privacidad del producto, cuando la publica, entonces el sistema muestra la version vigente a todos los usuarios y conserva las versiones anteriores disponibles para consulta.

**Reglas de negocio**

- El aviso de privacidad del producto describe el tratamiento que el proveedor hace de los datos personales de los usuarios de la plataforma (nombre, correo, cargo); es distinto del Aviso de Privacidad que cada organizacion cliente publica para sus propios titulares (propiedad de MOD-008).
- Consultar este aviso es informativo: no exige ninguna aceptacion ni bloquea el uso del sistema.

**Fuera de alcance**

- El Aviso de Privacidad de la organizacion cliente hacia sus propios titulares: eso es MOD-008
- Los terminos de uso: ver HU-000-11
- El contrato de encargo de tratamiento: ver HU-000-12

- Requiere contenido: Texto del aviso de privacidad del propio producto (tratamiento de datos de los usuarios de la plataforma por el proveedor), validado por asesoria legal
- Requiere validacion legal: Si
- Referencia: 04_secciones/09_modelo_conceptual.md seccion 9.1.4 (versionado); 02_validacion/04_objetivo_exacto_del_producto.md seccion 1.1

### HU-000-14. Autorizar un acceso temporal de soporte

**Como** Administrador de la organizacion, **quiero** revisar y autorizar, o rechazar, una solicitud de acceso temporal del equipo de soporte del producto a mi organizacion, con una duracion definida, **para** mantener el control de quien entra a los datos de mi organizacion, incluso cuando necesito ayuda del proveedor.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 21 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-000-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el equipo de soporte del producto (proveedor) solicita acceso temporal a una organizacion con un motivo y una duracion propuesta, cuando el Administrador de la organizacion revisa la solicitud, entonces puede aprobarla o rechazarla, y ajustar la duracion antes de aprobarla.
2. Dado que el Administrador de la organizacion aprueba la solicitud, cuando la aprueba, entonces el sistema habilita el acceso de soporte unicamente por la duracion definida, sin posibilidad de que el propio equipo de soporte la extienda por su cuenta.
3. Dado que el Administrador de la organizacion rechaza la solicitud, cuando la rechaza, entonces el equipo de soporte del producto no obtiene ningun acceso a esa organizacion.
4. Dado un acceso de soporte ya aprobado y todavia vigente, cuando el Administrador de la organizacion decide revocarlo antes de tiempo, entonces el sistema termina el acceso de inmediato.
5. Dado que se solicita, aprueba, rechaza o revoca un acceso temporal de soporte, cuando cualquiera de esos eventos ocurre, entonces la bitacora de auditoria lo registra con quien lo hizo, la organizacion afectada, la duracion y la fecha y hora.

**Reglas de negocio**

- Todo acceso de una persona del equipo de soporte a una cuenta cliente especifica requiere autorizacion explicita y registrada del Administrador de esa cuenta (04_secciones/11_roles_y_permisos.md seccion 11.7, propuesta de esa seccion, a validar).
- El acceso queda acotado en el tiempo y se registra en el historial de la organizacion cliente, visible para su Administrador y su Auditor interno (04_secciones/11_roles_y_permisos.md seccion 11.7).

**Fuera de alcance**

- Lo que el equipo de soporte hace durante el acceso ya autorizado: ver HU-000-15
- El acceso del Editor de contenido regulatorio o del Equipo de contenido del producto al contenido normativo o de ayuda compartido: ninguno de los dos entra a datos de una organizacion cliente (04_secciones/11_roles_y_permisos.md seccion 11.7)

- Requiere contenido: Politica interna de soporte del proveedor que defina motivos validos y duracion maxima del acceso temporal (propuesta a validar por el equipo de producto)
- Referencia: 04_secciones/11_roles_y_permisos.md seccion 11.7 (propuesta de esa seccion, no presente en las fichas)
- Notas: Propuesta de la seccion 11.7 del blueprint, marcada ahi mismo como no presente en ninguna ficha; sujeta a validacion del equipo de producto y de asesoria legal antes de tratarse como regla definitiva.

### HU-000-15. Usar el acceso temporal de soporte autorizado

**Como** Equipo de soporte del producto (proveedor), **quiero** usar, solo dentro de la ventana de tiempo que el Administrador autorizo, un acceso acotado a la organizacion que pidio ayuda, **para** resolver su consulta de soporte sin acceder sin autorizacion y dejando registrado todo lo que revise.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 21 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-000-14, HU-000-02, HU-000-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un acceso temporal aprobado y vigente sobre una organizacion, cuando un integrante del equipo de soporte del producto lo usa, entonces solo puede consultar esa organizacion, nunca otra distinta de la autorizada.
2. Dado que la ventana de tiempo autorizada vence, cuando eso ocurre, entonces el acceso se cierra de inmediato, incluso si el integrante del equipo de soporte tenia una sesion abierta en ese momento.
3. Dado que el equipo de soporte del producto usa un acceso autorizado, cuando intenta ejecutar un acto que la ley atribuye a un rol de la organizacion cliente (por ejemplo, aprobar o denegar una solicitud ARCO-POL, aprobar un documento o activar el doble estado de la reforma 659), entonces el sistema no permite esa accion.
4. Dado cualquier accion que el equipo de soporte realice dentro de la ventana autorizada, cuando la realiza, entonces queda registrada en la bitacora de auditoria de esa organizacion, visible para su Administrador y su Auditor (interno).
5. Dado que no existe ningun acceso temporal aprobado y vigente para una organizacion, cuando un integrante del equipo de soporte intenta consultarla, entonces el sistema deniega el acceso de la misma forma que a cualquier otro usuario ajeno a esa organizacion.

**Reglas de negocio**

- El acceso de soporte nunca sustituye ni ejecuta un acto que la ley atribuye a un rol de la organizacion cliente (04_secciones/11_roles_y_permisos.md seccion 11.7).
- Todo lo que el equipo de soporte hace durante su acceso queda registrado y visible para el Administrador y el Auditor interno de la organizacion (04_secciones/11_roles_y_permisos.md seccion 11.7).

**Fuera de alcance**

- Solicitar y aprobar el acceso: ver HU-000-14
- Cualquier accion legalmente atribuida a un rol de la organizacion cliente

- Referencia: 04_secciones/11_roles_y_permisos.md seccion 11.7 (propuesta de esa seccion, no presente en las fichas)
- Notas: Propuesta de la seccion 11.7 del blueprint, marcada ahi mismo como no presente en ninguna ficha; sujeta a validacion del equipo de producto y de asesoria legal antes de tratarse como regla definitiva.

### HU-000-16. Exportar todos los datos de la organizacion al finalizar el contrato

**Como** Administrador de la organizacion, **quiero** solicitar y recibir una exportacion completa de todos los datos que mi organizacion registro en el sistema, cuando termina mi contrato con el proveedor, **para** conservar la informacion de mi programa de proteccion de datos sin depender de que siga usando la plataforma.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 36 | No |

- Fundamento: OBL-PROV-07 (Art. 34 lit. a), en relacion con Art. 5 lit. h), Ley para la Proteccion de Datos Personales)
- Depende de: HU-000-04, HU-000-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que la organizacion finaliza su contrato con el proveedor, cuando el Administrador de la organizacion o el equipo del producto (proveedor) solicita la exportacion completa, entonces el sistema arma un paquete con los registros de todos los modulos que la organizacion uso (organizacion y usuarios, tratamientos, ARCO-POL, incidentes, consentimientos, documentos, evidencia, controles, entre otros).
2. Dado que el paquete de exportacion completa se genera, cuando el servicio comun de exportacion lo procesa, entonces incluye la huella de integridad de cada archivo y el manifiesto del conjunto.
3. Dado que la exportacion de algun modulo con datos de la organizacion queda incompleta o falla, cuando el sistema procesa la solicitud, entonces no marca la exportacion completa como terminada hasta que todos los modulos con datos de esa organizacion queden incluidos.
4. Dado que el paquete de exportacion completa queda disponible, cuando el Administrador de la organizacion lo descarga, entonces el sistema deja constancia de quien lo descargo y cuando.
5. Dado que se solicita o se entrega la exportacion completa de una organizacion, cuando ocurre cualquiera de los dos eventos, entonces la bitacora de auditoria lo registra con quien lo solicito o lo recibio, la organizacion y la fecha y hora.

**Reglas de negocio**

- La exportacion completa usa el mismo servicio comun de exportacion con verificacion de integridad que el resto del sistema (HU-000-04), no un mecanismo separado.
- La devolucion de los datos al finalizar la relacion con el encargado es una practica recomendada bajo la LPDP, aplicada aqui al propio proveedor frente a su cliente (ver notas_epica sobre OBL-PROV-07).

**Fuera de alcance**

- La eliminacion de los datos despues de entregada la exportacion: ver HU-000-17
- El formato exacto de entrega del archivo final

- Referencia: 04_secciones/13_evidencia_y_auditoria.md tabla PROV (OBL-PROV-07); 04_secciones/09_modelo_conceptual.md seccion 9.6
- Notas: OBL-PROV-07 esta redactada en la matriz para el proveedor que la organizacion cliente contrata (propietario MOD-009); se usa aqui por analogia para el proveedor del software frente a la organizacion cliente, segun explica notas_epica. Release ajustado de R1 a R2 en la planificacion: la exportacion y eliminacion al terminar el contrato se necesitan antes del primer vencimiento de contrato, no para la primera venta.

### HU-000-17. Eliminar los datos de una organizacion tras finalizar el contrato

**Como** Equipo del producto (proveedor), **quiero** eliminar los datos de una organizacion cliente despues de confirmar que recibio su exportacion completa y de que se cumple el plazo pactado, dejando constancia de la eliminacion, **para** cerrar la relacion con esa organizacion sin conservar sus datos mas alla de lo pactado.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 36 | No |

- Fundamento: OBL-PROV-07 (Art. 34 lit. a), en relacion con Art. 5 lit. h), Ley para la Proteccion de Datos Personales); OBL-SEG-05 (Art. 4, Medidas Fisicas lit. e), Politicas de Actuacion ACE)
- Depende de: HU-000-16, HU-000-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que una organizacion finalizo su contrato, cuando el equipo del producto (proveedor) intenta iniciar la eliminacion de sus datos, entonces el sistema exige confirmar primero que la exportacion completa de la organizacion (HU-000-16) ya fue entregada.
2. Dado que la organizacion tiene un procedimiento sancionador o un reclamo ante la Direccion de Proteccion de Datos de la ACE todavia abierto que referencia sus datos, cuando el equipo del producto intenta eliminarlos, entonces el sistema bloquea la eliminacion mientras ese procedimiento siga abierto.
3. Dado que se cumplen las condiciones para eliminar (exportacion entregada, plazo pactado cumplido, sin procedimiento abierto), cuando el equipo del producto confirma la eliminacion con el metodo usado y su propia identidad, entonces el sistema elimina los datos de esa organizacion y genera una constancia de la eliminacion.
4. Dado que los datos de la organizacion ya fueron eliminados, cuando alguien busca la constancia de esa eliminacion, entonces la encuentra disponible aunque los datos originales ya no existan.
5. Dado que se confirma la eliminacion de los datos de una organizacion, cuando ocurre, entonces la bitacora de auditoria registra quien la ejecuto, el metodo, la fecha y hora.

**Reglas de negocio**

- La eliminacion nunca ocurre antes de confirmar que la exportacion completa fue entregada.
- Un procedimiento abierto que referencia los datos de la organizacion bloquea la eliminacion, sin excepcion, igual que el mismo criterio que aplica MOD-016 a la evidencia bloqueada por un procedimiento abierto (04_secciones/13_evidencia_y_auditoria.md seccion 13.6.2).
- La eliminacion siempre deja una constancia (metodo, responsable, fecha) que sigue disponible incluso despues de eliminados los datos originales, con el mismo criterio de evidencia de eliminacion que usa MOD-016 (04_secciones/13_evidencia_y_auditoria.md seccion 13.6.3).

**Fuera de alcance**

- El plazo comercial exacto que debe transcurrir antes de eliminar: es una decision de contrato, fuera del alcance funcional de este documento
- La exportacion previa: ver HU-000-16

- Referencia: 04_secciones/13_evidencia_y_auditoria.md secciones 13.6.2 y 13.6.3 (por analogia); tabla PROV (OBL-PROV-07)
- Notas: El plazo exacto tras el cual procede la eliminacion queda como parametro configurable, pendiente de decision comercial (ver notas_epica). Release ajustado de R1 a R2 en la planificacion: la exportacion y eliminacion al terminar el contrato se necesitan antes del primer vencimiento de contrato, no para la primera venta.

### HU-000-18. Ver fechas y horas en el huso horario de El Salvador

**Como** Usuario de consulta / Colaborador, **quiero** que toda fecha y hora que el sistema muestra use el huso horario y el formato de fecha de El Salvador, **para** interpretar correctamente los plazos, las alertas y la bitacora de auditoria sin hacer conversiones manuales.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 21 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado cualquier fecha u hora que el sistema muestra en una pantalla, un reporte o un documento generado, cuando el usuario la consulta, entonces aparece en el huso horario de El Salvador y en el formato de fecha usado en el pais, sin importar desde donde se conecte.
2. Dado que otro modulo calcula una fecha limite o un plazo legal (por ejemplo, a traves del motor de plazos), cuando el resultado se muestra al usuario, entonces se presenta en ese mismo huso horario y formato.
3. Dado un usuario cuyo dispositivo o navegador esta configurado con otro huso horario, cuando consulta cualquier fecha dentro del sistema, entonces la fecha mostrada no cambia por la configuracion de su dispositivo.
4. Dado un evento registrado en la bitacora de auditoria, cuando alguien lo consulta, entonces la marca de tiempo se muestra en el huso horario de El Salvador.

**Reglas de negocio**

- El huso horario y el formato de fecha de El Salvador se aplican de forma uniforme en todo el sistema, sin depender de la configuracion del dispositivo de cada usuario.

**Fuera de alcance**

- El calculo de plazos legales en dias u horas habiles: eso lo hace el motor de plazos (MOD-023)
- El calendario de dias inhabiles: tambien es MOD-023

- Referencia: 00_contexto_para_agentes.md seccion 1 (contexto de El Salvador)

### HU-000-19. Usar el sistema en espanol

**Como** Usuario de consulta / Colaborador, **quiero** que todas las pantallas, mensajes, textos de ayuda y documentos que el sistema genera esten en espanol, **para** poder usar el sistema completo sin depender de otro idioma.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 1 | R1 | 6 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado cualquier pantalla del sistema, cuando un usuario la abre, entonces todas las etiquetas, botones, mensajes de error y textos de ayuda estan en espanol.
2. Dado un modulo nuevo que se libera a los usuarios, cuando se publica, entonces no contiene texto residual sin traducir en otro idioma.
3. Dado un documento o un correo que el sistema genera de forma automatica (por ejemplo, una invitacion o una notificacion), cuando se genera, entonces su contenido esta en espanol.
4. Dado el estilo de redaccion en espanol sin lenguaje juridico innecesario que exige el principio de transparencia, cuando el equipo de contenido revisa un texto de cara al usuario, entonces el texto evita terminologia tecnica y letra pequena para un usuario no especialista.

**Reglas de negocio**

- Idioma unico del producto: espanol, con registro profesional y claro para un usuario no especialista (00_contexto_para_agentes.md seccion 4).

**Fuera de alcance**

- El contenido normativo o de ayuda especifico de cada modulo: cada modulo redacta su propio contenido en espanol dentro de su propio alcance

- Referencia: 00_contexto_para_agentes.md seccion 4 (reglas de redaccion); 02_validacion/04_objetivo_exacto_del_producto.md

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Inicio de sesion y recuperacion de acceso | HU-000-06, HU-000-07 |
| Doble factor obligatorio al menos para los roles con acceso a datos de titulares o de administracion | HU-000-08 |
| Cierre de sesion por inactividad | HU-000-09 |
| Aislamiento total entre organizaciones clientes | HU-000-01 |
| Bitacora (AuditLog) de solo adicion, sin edicion ni borrado para ningun rol, consultable por Auditor y Administrador, habilitadora para todos los modulos | HU-000-02, HU-000-03 |
| Servicio comun de exportacion con verificacion de integridad (huella por archivo y manifiesto), reutilizado por los modulos, habilitadora | HU-000-04 |
| Descargo legal visible y aceptacion de terminos de uso | HU-000-10, HU-000-11 |
| Alta de una organizacion cliente por el equipo del producto (aprovisionamiento); la facturacion queda fuera del MVP y se hace fuera del sistema | HU-000-05 |
| Contrato de encargo de tratamiento entre el proveedor del software y la organizacion cliente (Arts. 34, 36 y 41 LPDP) | HU-000-12 |
| Aviso de privacidad del propio producto | HU-000-13 |
| Acceso del equipo de soporte del proveedor solo con autorizacion del Administrador, acotado en tiempo y registrado (propuesta de la seccion 11.7, a validar) | HU-000-14, HU-000-15 |
| Exportacion completa de los datos de la organizacion al terminar el contrato y eliminacion posterior con constancia | HU-000-16, HU-000-17 |
| Zona horaria y formato de fecha de El Salvador | HU-000-18 |
| Interfaz en espanol | HU-000-19 |
