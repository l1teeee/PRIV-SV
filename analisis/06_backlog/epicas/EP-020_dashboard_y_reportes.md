# EP-020 Dashboard y Reportes (MOD-020)

**Objetivo.** Dar a cada rol de la organizacion, desde el nucleo vendible, una vista de solo lectura de en que estado esta su programa de proteccion de datos (pendientes, vencidos, evidencia disponible), diferenciada por perspectiva (Gerencia, Responsable, Legal/Delegado, Auditor), con filtro por sucursal o unidad, drill-down que respeta permisos y acceso directo a los reportes minimos ya construidos por cada modulo de origen, sin declarar nunca un porcentaje de cumplimiento legal ni exponer datos personales de titulares.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R2 | 9 | 41 | 3 | 38 | [MOD-020](../../03_modulos/MOD-020_ficha.md) |

**Notas de la epica.**

- MOD-020 no es propietario ni colaborador de ninguna obligacion (verificado en el encabezado de MOD-020_ficha.md contra las 105 obligaciones de 01_legal/matriz_obligaciones.json, sin resultados). Por eso el campo fundamento de las 9 HU de esta epica queda vacio: el valor probatorio del modulo es indirecto (agrega evidencia disponible que MOD-019 si sostiene contra OBL-PRIN-03 en su propio modulo).
- Excepcion de release autorizada por el encargo: HU-020-01 se propone en R1 porque el nucleo vendible de la seccion 19.8 (10 modulos: MOD-001, MOD-002, MOD-003, MOD-004, MOD-005, MOD-006, MOD-008, MOD-021, MOD-022, MOD-023, MOD-024) necesita mostrar avance del Plan de Cumplimiento y de las tareas antes de que exista el Dashboard completo por perspectivas, que se entrega en R2 junto con el resto del segundo grupo de modulos MUST HAVE (seccion 19.9). HU-020-01 es un panel muy reducido (sin perspectivas, sin filtros, solo MOD-005 y MOD-021) y no un prerequisito tecnico de las demas HU: no se declara depende_de_hu entre HU-020-01 y las HU de R2.
- Discrepancia detectada y resuelta: la propia tabla Q de MOD-020_ficha.md clasifica 'Estado del programa por etapa y por cluster (seccion M.3, sintesis de alto nivel)' como una sola fila SHOULD HAVE (no distingue version por etapa frente a version por cluster). El documento 04_secciones/14_dashboard_y_reportes.md, seccion 14.8, en cambio, propone separarla (por etapa: MVP; por cluster: V1), sin que ninguna otra fuente resuelva la discrepancia. Siguiendo la regla de la seccion 3 de las instrucciones (si la tabla Q y otra fuente discrepan, sigue la tabla Q de tu ficha), esta epica excluye por completo la sintesis de 5 niveles (Sin iniciar / En configuracion / Operando / Con evidencia / Revisado), tanto por etapa como por cluster, de R1 y de R2. La indicacion especifica del encargo sobre un 'modelo de estado del programa sin porcentaje de cumplimiento legal' se satisface, dentro del alcance MUST HAVE, con el aviso de descargo y la prohibicion de lenguaje de cumplimiento (HU-020-03) y con la regla de que ningun indicador individual de las HU de perspectiva (HU-020-05 a 08) se expresa como cumplimiento legal.
- Exclusiones expresas del encargo, confirmadas contra las fuentes: vista alternativa por los 8 clusters legales (Q, SHOULD HAVE/V1), fotos periodicas o historicas / cierres mensuales (Q, SHOULD HAVE/V1) e Informe para Junta Directiva (Q, SHOULD HAVE/V1, tambien excluido de forma literal por 19.3). Por la misma clasificacion V1 de N.1/14.5.1, tampoco se incluyen en esta epica el Informe gerencial consolidado propio de MOD-020, el enlace al paquete de evidencia para la ACE, el reporte comparativo de tendencia ni la exportacion en PDF de la vista vigente del Dashboard: los cinco reportes propios de MOD-020 (seccion N.1 de la ficha y 14.5.1) estan clasificados Version V1 en su totalidad.
- Reportes minimos del MVP (indicacion especifica del encargo): la tabla N.2 de la ficha exige un unico punto de entrada a 7 reportes minimos del area 28. De esos 7, 5 ya existen como reporte MUST HAVE de su propio modulo de origen (ARCO-POL de MOD-011, Incidentes de MOD-013, Proveedores de MOD-009, RAT de MOD-006, Seguridad de MOD-015); los otros 2 (Gerencial y Auditoria) dependen de piezas V1 (el Informe gerencial propio de MOD-020, y MOD-018 completo, que es SHOULD HAVE). HU-020-09 construye el catalogo/directorio para los 5 disponibles, marcando los otros 2 como no disponibles en esta version, y satisface la exigencia de la fila MUST HAVE de la tabla Q ('toda exportacion queda en el AuditLog, con verificacion de integridad via MOD-019') reusando el mismo mecanismo de auditoria e integridad que cada modulo de origen ya implementa en su propia epica, en vez de que MOD-020 reinvente uno propio.
- Los meta-indicadores propios del Dashboard como herramienta (seccion M.2 de la ficha: cobertura de indicadores activos, fotos periodicas generadas a tiempo, reportes exportados por tipo, perspectiva mas consultada) quedan fuera de esta epica: la tabla Q no les asigna una fila propia, la mayoria depende de capacidades V1 (fotos periodicas, reportes propios de MOD-020) y el encargo especifico no los menciona. Se deja como observacion para una revision futura de la tabla Q que los clasifique de forma explicita.
- El filtro por sociedad (D.1) y la vision consolidada multi-sociedad no se modelan en esta epica: el MVP no soporta grupos multi-sociedad (decision de alcance 2.7.31 de 02_validacion_de_la_idea.md; MOD-001, seccion Q, marca esa capacidad FUTURE/Enterprise). El filtro por etapa del recorrido y por modulo de origen (tambien en D.1) tampoco se incluyen en HU-020-02: no estan en la lista de indicaciones especificas del encargo (que solo pide sucursal o unidad) y su ausencia no deja ninguna obligacion sin cobertura, porque los mismos indicadores siguen visibles agrupados por perspectiva.
- Se cita PP-UX-05 (04_secciones/24_preguntas_pendientes.md) en HU-020-03 porque esa pregunta pendiente, clasificada MVP, pide validar con clientes piloto que el diseno visual del aviso de estado del programa no contradiga el texto de descargo; no es una pregunta juridica, por lo que ninguna HU de esta epica marca requiere_validacion_legal en true.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-020-01 | Mostrar un panel inicial de pendientes del plan y de tareas | Administrador de la organizacion | 3 | R1 | 20 | MOD-005, MOD-021 |
| HU-020-02 | Elegir la perspectiva del Dashboard y aplicar filtros de sucursal, unidad y periodo | Administrador de la organizacion | 3 | R2 | 34 | MOD-001 |
| HU-020-03 | Mostrar el aviso de estado del programa, nunca cumplimiento legal | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 2 | R2 | 34 | HU-020-02 |
| HU-020-04 | Bajar al registro fuente de un indicador respetando permisos | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 5 | R2 | 34 | HU-020-02 |
| HU-020-05 | Ver el Dashboard en la perspectiva Gerencia | Administrador de la organizacion | 5 | R2 | 34 | HU-020-02, HU-020-03, HU-020-04, MOD-001, MOD-005, MOD-011, MOD-013, MOD-019, MOD-021, MOD-024 |
| HU-020-06 | Ver el Dashboard en la perspectiva Responsable | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 5 | R2 | 34 | HU-020-02, HU-020-03, HU-020-04, MOD-006, MOD-009, MOD-011, MOD-013, MOD-021 |
| HU-020-07 | Ver el Dashboard en la perspectiva Legal/Delegado | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R2 | 34 | HU-020-02, HU-020-03, HU-020-04, MOD-002, MOD-011, MOD-019, MOD-024 |
| HU-020-08 | Ver el Dashboard en la perspectiva Auditor | Auditor (interno) | 5 | R2 | 35 | HU-020-02, HU-020-03, HU-020-04, MOD-011, MOD-015, MOD-019, MOD-023 |
| HU-020-09 | Consultar el catalogo de reportes minimos por modulo de origen | Auditor (interno) | 8 | R2 | 35 | HU-020-02, HU-020-04, HU-020-08, MOD-006, MOD-009, MOD-011, MOD-013, MOD-015, MOD-019 |

## Historias

### HU-020-01. Mostrar un panel inicial de pendientes del plan y de tareas

**Como** Administrador de la organizacion, **quiero** ver, apenas tengo el sistema del nucleo vendible funcionando, cuantas acciones de mi Plan de Cumplimiento y cuantas tareas del Centro de Tareas tengo pendientes, en proceso y vencidas, **para** mostrar avance real del programa desde el primer dia, sin esperar a que exista el Dashboard completo por perspectivas.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 20 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: MOD-005, MOD-021

**Criterios de aceptacion**

1. Dado que la organizacion tiene un Plan de Cumplimiento en estado Vigente (MOD-005) y tareas creadas en el Centro de Tareas (MOD-021), cuando el Administrador abre el panel inicial, entonces ve el conteo de acciones del plan Pendiente, En proceso, Completada y Vencida, y el conteo de tareas Pendiente, En proceso, Bloqueada y Vencida.
2. Dado que existe al menos una accion del plan o una tarea en estado Vencida, cuando se calcula el panel, entonces el indicador correspondiente se muestra en rojo con su conteo exacto.
3. Dado que no existe ninguna accion ni tarea vencida, cuando se calcula el panel, entonces el indicador correspondiente se muestra en verde.
4. Dado que el usuario hace clic en el conteo de acciones o de tareas, cuando se ejecuta el enlace, entonces el sistema lo redirige a la lista correspondiente de MOD-005 o MOD-021, respetando los permisos que ese usuario ya tiene en el modulo de destino.
5. Dado un usuario cuyo rol no es Administrador de la organizacion ni Delegado de Proteccion de Datos, cuando intenta abrir el panel inicial, entonces el sistema le deniega el acceso, porque el panel esta acotado a esos dos roles mientras el Dashboard completo no exista.
6. Dado que aun no existe ningun Plan de Cumplimiento Vigente, cuando se abre el panel, entonces el sistema muestra el conteo de acciones en cero, sin mostrar un mensaje de error.
7. Dado que el usuario abre o refresca el panel, cuando el sistema recalcula los conteos, entonces la vista se actualiza en tiempo real sin generar un evento de auditoria, por tratarse de una consulta de solo lectura.
8. Dado cualquier conteo mostrado en este panel, cuando el usuario lo revisa, entonces el texto de pantalla nunca usa la palabra cumplimiento junto a un numero o un porcentaje.

**Reglas de negocio**

- MOD-020 nunca recalcula ni reinterpreta el valor de un indicador: lo muestra tal como su modulo fuente lo define (ficha, seccion M.1).
- MOD-020 no crea tareas ni modifica ningun otro modulo: es un modulo terminal de lectura (ficha, seccion A).
- Todo indicador es un conteo agregado, nunca un dato de negocio individual (ficha, seccion D.4).
- El enlace de detalle respeta siempre los permisos del modulo de destino (ficha, seccion D.4, punto 2).

**Fuera de alcance**

- Filtro por sucursal, unidad o periodo
- Las 4 perspectivas completas del Dashboard (Gerencia, Responsable, Legal/Delegado, Auditor)
- Indicadores de modulos distintos de MOD-005 y MOD-021
- Exportacion de este panel

- Referencia: MOD-020_ficha.md, secciones A, E y L.2; 04_secciones/19_21_roadmap_mvp_v1_v2.md, seccion 19.8
- Notas: Version muy reducida y temporal, autorizada de forma expresa por el encargo para que el nucleo vendible de 19.8 pueda mostrar avance antes de que el Dashboard completo (HU-020-02 a HU-020-09, en R2) este disponible; no es un prerequisito tecnico de esas HU.

### HU-020-02. Elegir la perspectiva del Dashboard y aplicar filtros de sucursal, unidad y periodo

**Como** Administrador de la organizacion, **quiero** que el Dashboard preseleccione la perspectiva que corresponde a mi rol, poder cambiar de perspectiva cuando mi rol lo permite, y filtrar la informacion por sucursal o unidad y por periodo, **para** ver siempre la informacion relevante a mi rol y acotada al alcance de la organizacion que necesito revisar.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 34 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado un usuario que abre el Dashboard por primera vez en la sesion, cuando el sistema carga la pantalla, entonces preselecciona la perspectiva que corresponde a su rol (Gerencia, Responsable, Legal/Delegado o Auditor) segun la tabla de perspectiva por defecto de la ficha.
2. Dado un usuario con mas de un rol asignado, cuando el sistema preselecciona la perspectiva, entonces usa la de mayor alcance entre las que le correspondan.
3. Dado un rol sin permiso para cambiar de perspectiva (por ejemplo, Responsable de area o Aprobador), cuando el usuario abre el selector de perspectiva, entonces el sistema no le ofrece ninguna perspectiva distinta de la suya.
4. Dado un Administrador de la organizacion, cuando aplica el filtro de sucursal o unidad, entonces puede elegir una, varias o Todas del catalogo vigente de MOD-001.
5. Dado un Responsable de area, cuando aplica el filtro de sucursal o unidad, entonces el sistema solo le permite elegir su propia area, nunca el agregado de otra area.
6. Dado un filtro de periodo con fecha desde posterior a fecha hasta, cuando el usuario intenta aplicarlo, entonces el sistema rechaza el filtro y muestra el mensaje de validacion correspondiente, sin recalcular la vista.
7. Dado cualquier cambio de perspectiva o de filtro, cuando el usuario lo confirma, entonces el sistema recalcula los indicadores visibles en tiempo real sin generar un evento de auditoria, por tratarse de una consulta de solo lectura.
8. Dado un usuario con el rol Usuario de consulta / Colaborador, cuando intenta abrir el Dashboard principal, entonces el sistema lo redirige a su vista personal reducida de tareas en vez de mostrarle el selector de perspectivas.

**Reglas de negocio**

- Las 4 perspectivas son una capa de presentacion sobre los 12 roles estandar del sistema, no una quinta categoria de rol (ficha, seccion B).
- Un Responsable de area nunca ve el agregado de otra area (ficha, seccion C, nota de separacion de funciones).
- El filtro de sucursal o unidad usa el catalogo compartido de MOD-001 (ficha, seccion L.2).
- Toda vista respeta primero el filtro de permisos del rol y despues el filtro de perspectiva, sucursal o periodo elegido (ficha, seccion M.1).

**Fuera de alcance**

- Vista alternativa por los 8 clusters legales
- Filtro por etapa del recorrido
- Filtro por modulo de origen
- Filtro por sociedad (inactivo mientras el MVP no soporte multi-sociedad)
- Seleccion de una foto periodica (cierre mensual) como punto de comparacion

- Referencia: MOD-020_ficha.md, secciones B, C y D.1
- Notas: El filtro por sociedad se excluye por decision expresa del encargo y porque el MVP no soporta multi-sociedad (decision de alcance 2.7.31 de 02_validacion_de_la_idea.md).

### HU-020-03. Mostrar el aviso de estado del programa, nunca cumplimiento legal

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que el Dashboard muestre siempre, en sus 4 perspectivas, un aviso de que los indicadores reflejan el estado del programa y nunca un porcentaje de cumplimiento legal, **para** que ningun usuario de mi organizacion interprete un indicador como una conclusion juridica sobre si cumplimos o no con la ley.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R2 | 34 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-020-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado cualquier perspectiva del Dashboard (Gerencia, Responsable, Legal/Delegado o Auditor), cuando el usuario la abre, entonces ve visible el aviso de que el panel muestra el estado del programa (controles configurados, tareas pendientes, evidencia disponible), no una medicion de cumplimiento legal, y que debe consultar a su Delegado o a asesoria especializada antes de afirmar que su empresa cumple con la ley.
2. Dado un indicador que usa una escala verde, amarillo o rojo, cuando se muestra en pantalla, entonces su etiqueta usa siempre alguno de los terminos estado del programa, controles configurados, tareas pendientes o evidencia disponible, nunca la palabra cumplimiento junto a un numero o un porcentaje.
3. Dado un indicador que si expresa un porcentaje (por ejemplo, cobertura del RAT), cuando se muestra, entonces su texto de ayuda aclara que mide una magnitud operativa concreta y acotada, no el cumplimiento legal de la empresa en abstracto.
4. Dado que el usuario cierra o recarga el Dashboard, cuando vuelve a entrar, entonces el aviso de descargo vuelve a mostrarse, sin opcion de desactivarlo de forma permanente.
5. Dado un indicador mostrado en rojo, cuando el usuario consulta su ayuda contextual, entonces el texto aclara que un indicador en rojo senala una tarea, un control o una evidencia pendiente, y no es por si mismo una conclusion sobre si existe una infraccion.
6. Dado un Administrador de la organizacion, cuando busca alguna opcion para configurar o desactivar el aviso de descargo desde cualquier pantalla del Dashboard, entonces el sistema no ofrece esa opcion.

**Reglas de negocio**

- Anti-feature 5: declarar un porcentaje de cumplimiento legal de 0 a 100 por ciento no debe hacerse; en su lugar se muestra estado del programa, controles configurados, tareas pendientes o evidencia disponible.
- Anti-feature 22: no usar en la comunicacion frases como cumplimiento garantizado o blindaje legal 100 por ciento.
- Decision que el sistema no automatiza (ficha, seccion H): traducir un indicador o una combinacion de indicadores en una afirmacion de cumplimiento legal, con o sin porcentaje.

**Fuera de alcance**

- Calculo de cualquier indicador (cubierto por HU-020-05 a HU-020-08)

- Requiere contenido: Validacion, con clientes piloto, de que el texto y el diseno visual (semaforos, barras) del aviso no contradicen el descargo de cumplimiento legal (ver PP-UX-05)
- Preguntas pendientes relacionadas: PP-UX-05
- Referencia: MOD-020_ficha.md, seccion H; 04_secciones/14_dashboard_y_reportes.md, seccion 14.1

### HU-020-04. Bajar al registro fuente de un indicador respetando permisos

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** bajar desde un indicador del Dashboard hasta el registro fuente en su modulo de origen (drill-down), **para** poder actuar directamente sobre lo que esta pendiente o vencido, sin tener que buscarlo de nuevo por mi cuenta.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 34 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-020-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un indicador con enlace de detalle, cuando el usuario hace clic y conserva el permiso de ver ese registro en su modulo de origen, entonces el sistema lo redirige a la pantalla correspondiente de ese modulo, ya filtrada al registro o al listado que originaba el indicador.
2. Dado un usuario cuyo rol no tiene permiso para ver el registro en su modulo de origen, cuando hace clic en el enlace de detalle, entonces el sistema no revela si el registro existe: el enlace no se muestra, o redirige a un mensaje neutro de sin acceso.
3. Dado un Responsable de area, cuando baja al detalle de un indicador de su propia area, entonces accede al registro; cuando el mismo tipo de indicador pertenece a otra area, entonces el sistema nunca le ofrece el enlace de detalle.
4. Dado un Auditor (interno) o un Auditor externo invitado, cuando baja al detalle de cualquier registro por drill-down, entonces solo puede verlo en modo de solo lectura, sin opcion de crear, aprobar, modificar ni eliminar nada desde esa pantalla.
5. Dado que el usuario pierde el permiso sobre un registro en su modulo de origen despues de haber visto el indicador (por ejemplo, se le retira el rol), cuando vuelve a intentar el mismo drill-down, entonces el sistema evalua el permiso vigente en ese momento, no el que tenia antes.
6. Dado cualquier enlace de detalle, cuando el usuario hace clic, entonces la accion sobre el registro queda gobernada por los permisos y por el historial del modulo de destino, sin que MOD-020 cree, apruebe ni modifique ningun registro por su cuenta.
7. Dado un Asesor externo invitado o un Auditor externo invitado, cuando intenta bajar al detalle de un registro fuera del alcance temporal o de modulos habilitado para su caso, entonces el sistema le deniega el acceso de la misma forma que si el registro no existiera.

**Reglas de negocio**

- El filtro de permisos se aplica siempre antes que el filtro de perspectiva, con la misma regla de no revelar existencia que usa la Busqueda Global (04_secciones/14_dashboard_y_reportes.md, seccion 14.7.2).
- El Dashboard nunca permite completar, aprobar ni cerrar nada directamente: siempre redirige al modulo de origen (ficha, seccion C, ultima fila).
- El rol Auditor, interno o externo, debe ser siempre de solo lectura (02_validacion/05_tipos_de_usuario.md, seccion 5.4).

**Fuera de alcance**

- Crear, aprobar, modificar o eliminar un registro desde el Dashboard
- Definir permisos nuevos: usa siempre los que ya existen en el modulo de origen

- Referencia: MOD-020_ficha.md, secciones C, D.4 punto 2, F.3 y P; 04_secciones/14_dashboard_y_reportes.md, seccion 14.7.2
- Notas: Mecanismo generico que consumen las HU de perspectiva (HU-020-05 a HU-020-08); no declara depende_de_modulos especifico porque se apoya en el modelo de permisos que cada modulo de destino ya construye en su propia epica, no en una capacidad nueva de MOD-020.

### HU-020-05. Ver el Dashboard en la perspectiva Gerencia

**Como** Administrador de la organizacion, **quiero** ver, en la perspectiva Gerencia del Dashboard, los indicadores criticos de toda la organizacion: avance del plan, evidencia disponible, tareas y solicitudes vencidas, incidentes abiertos y roles criticos sin titular, **para** responder de un vistazo como vamos, sin abrir cada modulo por separado.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 34 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-020-02, HU-020-03, HU-020-04
- Modulos requeridos: MOD-001, MOD-005, MOD-011, MOD-013, MOD-019, MOD-021, MOD-024

**Criterios de aceptacion**

1. Dado un Administrador de la organizacion que entra al Dashboard, cuando el sistema muestra la perspectiva Gerencia, entonces ve el avance del Plan de Cumplimiento (MOD-005), la evidencia disponible por obligacion aplicable (MOD-019), las tareas vencidas (MOD-021), las solicitudes ARCO-POL vencidas (MOD-011), los incidentes abiertos por severidad (MOD-013) y los roles criticos sin titular (MOD-001).
2. Dado que el avance del Plan de Cumplimiento es mayor a 80 por ciento, cuando se muestra el indicador, entonces aparece en verde; si esta entre 50 y 80 por ciento aparece en amarillo; si es menor a 50 por ciento aparece en rojo.
3. Dado que existe al menos una tarea o una accion del plan en estado Vencida, cuando se calcula el indicador correspondiente, entonces se muestra en rojo con su conteo exacto.
4. Dado un indicador cuyo modulo fuente es SHOULD HAVE o COULD HAVE y aun no existe en esta version (por ejemplo Riesgos y EIPD o Transferencias Internacionales), cuando se muestra en la perspectiva Gerencia, entonces aparece como no disponible en esta version, nunca como un valor en cero.
5. Dado un Delegado de Proteccion de Datos o un Responsable Legal / Compliance, cuando accede a la perspectiva Gerencia, entonces la ve en modo de solo lectura, sin las acciones exclusivas del Administrador.
6. Dado un rol sin permiso para ver la perspectiva Gerencia (por ejemplo Responsable de area o Aprobador), cuando intenta seleccionarla, entonces el sistema no la ofrece como opcion.
7. Dado el badge de regimen normativo vigente, cuando se muestra en la perspectiva Gerencia, entonces refleja el estado ACTUAL o FUTURO tal como lo define MOD-024, sin que MOD-020 lo calcule por su cuenta.
8. Dado cualquier indicador de esta perspectiva que cuente expedientes individuales (por ejemplo solicitudes ARCO-POL o incidentes), cuando se muestra en pantalla, entonces solo se ve el conteo agregado, nunca el nombre, el documento de identidad ni cualquier otro dato del titular al que pertenece un expediente.

**Reglas de negocio**

- MOD-020 nunca recalcula ni reinterpreta el valor de un indicador: lo muestra tal como su modulo fuente lo define (ficha, seccion M.1).
- Cuando un modulo fuente aun no existe en el MVP vigente, su indicador se muestra como no disponible en esta version (ficha, seccion G).
- Todo indicador es un conteo, un porcentaje, una fecha o un estado agregado, nunca un dato individual del titular (ficha, seccion D.4).
- El badge de regimen se lee siempre de MOD-024, nunca se calcula ni se duplica en MOD-020 (ficha, seccion L.2).

**Fuera de alcance**

- Informe gerencial consolidado exportable
- Informe para Junta Directiva
- Estado del programa por etapa o por cluster (sintesis de 5 niveles)
- Enlace al paquete de evidencia para la ACE

- Referencia: MOD-020_ficha.md, seccion M.3.1; 04_secciones/14_dashboard_y_reportes.md, seccion 14.2.1
- Notas: La sintesis estado del programa por etapa (5 niveles) que la maqueta de 14.2.1 incluye como bloque 1 se excluye de esta HU por la discrepancia de clasificacion documentada en notas_epica (la tabla Q de la ficha la marca SHOULD HAVE en conjunto); el encargo especifico se satisface con HU-020-03 y con indicadores individuales no porcentuales.

### HU-020-06. Ver el Dashboard en la perspectiva Responsable

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** ver, en la perspectiva Responsable del Dashboard, mis propias tareas pendientes y vencidas, mis aprobaciones pendientes si soy Aprobador, mis solicitudes ARCO-POL por vencer si soy Responsable del tramite, y los indicadores de mi propia area, **para** saber que tengo pendiente hoy sin revisar cada modulo por separado, y sin ver nunca el agregado de otra area.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 34 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-020-02, HU-020-03, HU-020-04
- Modulos requeridos: MOD-006, MOD-009, MOD-011, MOD-013, MOD-021

**Criterios de aceptacion**

1. Dado un Responsable de area que entra al Dashboard, cuando el sistema muestra la perspectiva Responsable, entonces ve sus tareas Pendiente, En proceso y Vencida (MOD-021) y los indicadores de su propia area, por ejemplo fichas del RAT pendientes de revision periodica (MOD-006), si su area administra tratamientos.
2. Dado ese mismo usuario, cuando revisa el panel, entonces el sistema nunca le ofrece el indicador equivalente de otra area: solo ve el conteo de su propia sucursal o area.
3. Dado un Aprobador, cuando entra a la perspectiva Responsable, entonces ve el conteo de aprobaciones pendientes asignadas a el (MOD-021), en amarillo si llevan mas de 3 dias en espera y en rojo si llevan 5 dias o mas.
4. Dado un Responsable ARCO-POL / Responsable del tramite, cuando entra a la perspectiva Responsable, entonces ve sus propias solicitudes ARCO-POL proximas a vencer o vencidas (MOD-011), nunca las de otro responsable.
5. Dado un Responsable de Seguridad / IT, cuando entra a la perspectiva Responsable, entonces ve sus controles e incidentes propios (MOD-015, MOD-013), incluidos los cronometros de 72 horas por vencer.
6. Dado que el usuario no tiene ninguna tarea, aprobacion ni solicitud pendiente, cuando se calcula el panel, entonces todos los indicadores se muestran en cero y en verde, sin mensaje de error.
7. Dado el indicador de proveedores sin contrato o DPA vigente vinculado (MOD-009) de la propia area del usuario, cuando su conteo es mayor a cero, entonces se muestra en rojo.
8. Dado cualquier indicador de esta perspectiva que cuente expedientes o fichas, cuando se muestra, entonces expone unicamente el conteo agregado, nunca el detalle de un expediente individual ni un dato personal del titular.

**Reglas de negocio**

- Un Responsable de area nunca ve el agregado de otra area (ficha, seccion C, nota de separacion de funciones).
- Ve unicamente los indicadores y tareas de su propia area (ficha, seccion B, tabla).
- Todo indicador es un conteo agregado, nunca un dato individual del titular (ficha, seccion D.4).

**Fuera de alcance**

- Vista personal reducida de Usuario de consulta / Colaborador, ya cubierta por MOD-021
- Configuracion de umbrales de semaforo

- Referencia: MOD-020_ficha.md, secciones B y C; 04_secciones/14_dashboard_y_reportes.md, seccion 14.2.2

### HU-020-07. Ver el Dashboard en la perspectiva Legal/Delegado

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** ver, en la perspectiva Legal/Delegado del Dashboard, los riesgos y decisiones legales pendientes, el estado de mi propio nombramiento e informes periodicos, y la evidencia disponible por obligacion aplicable, **para** priorizar que atender primero sin tener que revisar cada modulo legal por separado.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 34 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-020-02, HU-020-03, HU-020-04
- Modulos requeridos: MOD-002, MOD-011, MOD-019, MOD-024

**Criterios de aceptacion**

1. Dado un Delegado de Proteccion de Datos que entra al Dashboard, cuando el sistema muestra la perspectiva Legal/Delegado, entonces ve el estado de su propio nombramiento y el conteo de informes periodicos entregados frente al minimo legal de 2 (MOD-002).
2. Dado que existe al menos un reclamo ante la Direccion de Proteccion de Datos abierto (MOD-011), cuando se calcula el indicador, entonces se muestra en rojo.
3. Dado el badge de regimen normativo vigente, cuando se muestra en esta perspectiva, entonces indica si el regimen es ACTUAL o FUTURO, leido siempre de MOD-024 sin recalculo propio de MOD-020.
4. Dado el indicador de huecos de evidencia abiertos (MOD-019), cuando existe al menos un hueco clasificado OBLIGATORIO, entonces se muestra en rojo.
5. Dado que Riesgos y EIPD (MOD-014) o Transferencias Internacionales (MOD-010) aun no existen en esta version, cuando se muestran sus indicadores en esta perspectiva, entonces aparecen como no disponible en esta version.
6. Dado un Responsable Legal / Compliance, cuando entra a esta perspectiva, entonces ve el mismo panel que el Delegado, con foco en base juridica, documentos y procedimiento sancionador.
7. Dado un usuario en esta perspectiva, cuando intenta activar la vista alternativa por los 8 clusters legales, entonces el sistema no ofrece esa opcion en esta version.
8. Dado cualquier indicador de riesgos o reclamos, cuando se muestra, entonces expone solo el conteo agregado, nunca el nombre del titular ni el contenido del reclamo.

**Reglas de negocio**

- Ve riesgos y decisiones pendientes de su rol, con foco en base juridica y procedimiento sancionador (ficha, seccion B).
- El badge de regimen se lee siempre de MOD-024, nunca se calcula ni se duplica en MOD-020 (ficha, seccion L.2).
- La vista alternativa por los 8 clusters legales esta clasificada version SHOULD HAVE/V1 (ficha, tabla Q).

**Fuera de alcance**

- Vista alternativa por los 8 clusters legales
- Enlace al paquete de evidencia para la ACE
- Exportar el Informe para Junta Directiva

- Referencia: MOD-020_ficha.md, seccion M.3.1; 04_secciones/14_dashboard_y_reportes.md, seccion 14.2.3
- Notas: Los indicadores de MOD-014 y MOD-010 (ambos SHOULD HAVE) se muestran como no disponibles en esta version; no se declaran como depende_de_modulos porque su ausencia no bloquea la HU.

### HU-020-08. Ver el Dashboard en la perspectiva Auditor

**Como** Auditor (interno), **quiero** ver, en la perspectiva Auditor del Dashboard, la evidencia disponible y los huecos por obligacion aplicable, los vencimientos de controles y contratos, y elegir una fecha de corte para mi alcance de auditoria, **para** preparar mi revision de solo lectura sin necesitar acceso de edicion a ningun modulo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 35 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-020-02, HU-020-03, HU-020-04
- Modulos requeridos: MOD-011, MOD-015, MOD-019, MOD-023

**Criterios de aceptacion**

1. Dado un Auditor (interno) que entra al Dashboard, cuando el sistema muestra la perspectiva Auditor, entonces ve la evidencia disponible por obligacion aplicable clasificada OBLIGATORIO, RECOMENDADO o CONDICIONAL (MOD-019) y los huecos de evidencia abiertos.
2. Dado que existe al menos un hueco de evidencia clasificado OBLIGATORIO, cuando se calcula el indicador, entonces se muestra en rojo.
3. Dado el indicador de controles obligatorios sin evidencia o vencidos (MOD-015), cuando su conteo es mayor a cero, entonces se muestra en rojo.
4. Dado un Auditor externo invitado, cuando entra a esta perspectiva, entonces ve unicamente los indicadores y el alcance de modulos habilitado para su auditoria puntual, nunca el panel general de la organizacion.
5. Dado el indicador de estado de la ultima auditoria (MOD-018), cuando se muestra en esta perspectiva, entonces aparece como no disponible en esta version, porque MOD-018 es SHOULD HAVE y no existe en esta epica.
6. Dado que el Auditor selecciona una fecha de corte distinta de hoy dentro del rango permitido, cuando aplica el filtro, entonces los indicadores se recalculan en tiempo real a esa fecha, sin generar ni consultar una foto periodica de cierre mensual, porque esa capacidad no forma parte de esta version.
7. Dado cualquier accion sobre un indicador o su drill-down, cuando el Auditor la ejecuta, entonces solo puede consultar en modo de solo lectura, sin ninguna opcion de crear, aprobar, modificar o eliminar.
8. Dado un indicador que cuenta expedientes con evidencia completa o incompleta (por ejemplo ARCO-POL), cuando se muestra, entonces expone solo el porcentaje o el conteo agregado, nunca el contenido de un expediente individual.

**Reglas de negocio**

- El rol Auditor, interno o externo, debe ser siempre de solo lectura (02_validacion/05_tipos_de_usuario.md, seccion 5.4).
- Un Auditor externo invitado ve unicamente los indicadores y reportes del alcance temporal y de modulos habilitado para su auditoria puntual (ficha, seccion B).
- Cuando un modulo fuente aun no existe en el MVP vigente, su indicador se muestra como no disponible en esta version (ficha, seccion G).

**Fuera de alcance**

- Seleccion de una foto periodica (cierre mensual) como fecha de corte
- Exportar el paquete de evidencia de la auditoria desde MOD-020 (MOD-019 lo hace desde su propio modulo)

- Referencia: MOD-020_ficha.md, seccion M.3.1; 04_secciones/14_dashboard_y_reportes.md, seccion 14.2.4

### HU-020-09. Consultar el catalogo de reportes minimos por modulo de origen

**Como** Auditor (interno), **quiero** consultar, desde el Dashboard, un catalogo de los reportes minimos ya disponibles (ARCO-POL, incidentes, proveedores, RAT, seguridad) organizado por modulo de origen, y abrir cada uno desde ahi, **para** encontrar en un solo lugar los reportes que ya existen en cada modulo, con la garantia de que cada exportacion queda registrada y es verificable.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R2 | 35 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-020-02, HU-020-04, HU-020-08
- Modulos requeridos: MOD-006, MOD-009, MOD-011, MOD-013, MOD-015, MOD-019

**Criterios de aceptacion**

1. Dado un Auditor (interno) que abre el catalogo de reportes desde el Dashboard, cuando el sistema lo calcula, entonces ve, para su alcance, los reportes ya disponibles de MOD-006 (RAT consolidado y RAT de datos sensibles), MOD-009 (listado de proveedores y reporte de vencimientos), MOD-011 (reporte de solicitudes ARCO-POL), MOD-013 (listado de incidentes del periodo) y MOD-015 (checklist de controles de seguridad).
2. Dado un reporte del catalogo, cuando el usuario lo selecciona, entonces el sistema lo abre en la pantalla de exportacion de su modulo de origen, sin duplicar ni regenerar el reporte dentro de MOD-020.
3. Dado el reporte gerencial consolidado o el reporte del ciclo de auditoria, que dependen del Informe gerencial propio de MOD-020 y de MOD-018 (ambos fuera de esta version), cuando se muestran en el catalogo, entonces aparecen como no disponible en esta version.
4. Dado que el usuario exporta un reporte alcanzado desde este catalogo, cuando la exportacion se completa, entonces queda registrada en el AuditLog transversal con usuario, fecha, hora, reporte, filtros aplicados y formato, y su archivo incluye la verificacion de integridad que expone MOD-019, igual que si el usuario hubiera exportado ese reporte entrando de forma directa a su modulo de origen.
5. Dado un rol sin permiso para exportar un reporte especifico (por ejemplo Responsable de area), cuando revisa el catalogo, entonces ese reporte no aparece como opcion para el.
6. Dado un Auditor externo invitado o un Asesor externo invitado, cuando consulta el catalogo, entonces solo ve los reportes del alcance de modulos habilitado para su caso puntual.
7. Dado que el usuario abre el catalogo sin exportar nada, cuando solo navega la lista, entonces el sistema no genera un evento de auditoria de exportacion, porque la sola consulta del catalogo es una lectura, no una exportacion.
8. Dado cualquier reporte del catalogo, cuando el usuario lo abre, entonces el contenido y las reglas de minimizacion de datos personales del titular siguen siendo las que ya define su propio modulo de origen, sin que MOD-020 las modifique.

**Reglas de negocio**

- Toda exportacion queda en el AuditLog, con verificacion de integridad via MOD-019 (ficha, tabla Q, fila MUST HAVE).
- MOD-020 no reinventa su propio formato de hash o firma: entrega sus reportes al mecanismo unico que expone MOD-019 (ficha, seccion J).
- El rol de MOD-020 es ofrecer un unico punto de entrada donde encontrar los reportes ya existentes de cada modulo de origen (ficha, seccion N.2).
- Anti-feature 25: todo archivo exportado incluye un mecanismo propio de verificacion de integridad, hash o firma validable de forma independiente.

**Fuera de alcance**

- Informe gerencial consolidado propio de MOD-020
- Informe para Junta Directiva
- Enlace al paquete de evidencia para la ACE
- Reporte comparativo de tendencia con fotos periodicas
- Exportacion de la vista de Dashboard vigente (fotografia en PDF de la pantalla)

- Referencia: MOD-020_ficha.md, secciones J, N.1, N.2 y Q (fila 5); 04_secciones/14_dashboard_y_reportes.md, secciones 14.5 y 14.6
- Notas: De los 7 reportes minimos del area 28 que exige la seccion N.2, esta HU cubre los 5 que ya existen en un modulo MUST HAVE (ARCO-POL, incidentes, proveedores, RAT, seguridad); Gerencial y Auditoria se muestran como no disponibles hasta que existan el Informe gerencial propio de MOD-020 y MOD-018 (ambos V1), conforme a la propia tabla N.3/14.5.1 de la ficha.

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Dashboard basico por perspectiva (Gerencia, Responsable, Legal/Delegado, Auditor) con los indicadores de pendientes, vencidos, tratamientos, solicitudes | HU-020-01, HU-020-05, HU-020-06, HU-020-07, HU-020-08 |
| Indicadores agregados desde MOD-005, MOD-019 y MOD-021 (dependencia estructural minima) | HU-020-01, HU-020-05, HU-020-06, HU-020-07, HU-020-08 |
| Filtro por sucursal o unidad, y drill-down al registro fuente respetando permisos | HU-020-02, HU-020-04 |
| Regla de minimizacion (nunca datos personales de titulares en el Dashboard) y prohibicion de lenguaje de cumplimiento legal | HU-020-03, HU-020-05, HU-020-06, HU-020-07, HU-020-08 |
| Toda exportacion queda en el AuditLog, con verificacion de integridad via MOD-019 | HU-020-09 |
| Catalogo consolidado de indicadores de los modulos MUST HAVE (seccion M.3.1, filas de MOD-001 a MOD-009, MOD-011, MOD-013, MOD-015, MOD-017, MOD-019, MOD-021 a MOD-024, MOD-026) | HU-020-05, HU-020-06, HU-020-07, HU-020-08 |
