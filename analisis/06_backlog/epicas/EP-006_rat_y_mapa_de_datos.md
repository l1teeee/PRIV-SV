# EP-006 RAT y Mapa de Datos (MOD-006)

**Objetivo.** La empresa registra, clasifica, aprueba y mantiene vigente su Registro de Actividades de Tratamiento (RAT), con su Catalogo de Sistemas y una biblioteca de tratamientos plantilla, y lo exporta de forma verificable como la fuente unica de verdad que el resto del sistema consulta por referencia.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R1 | 20 | 82 | 74 | 8 | [MOD-006](../../03_modulos/MOD-006_ficha.md) |

**Notas de la epica.**

- La tabla Q de la ficha marca como SHOULD HAVE el calculo automatico del riesgo inicial y la deteccion de transferencia posiblemente no documentada; siguiendo la regla de la seccion 3 de las instrucciones (la tabla Q prevalece sobre la narrativa de otras secciones), esta epica no construye ninguno de los dos motores, aunque las secciones F, G, H e I de la ficha los describan como si ya operaran. El campo Riesgo inicial y la sugerencia automatica de EIPD por riesgo Alto quedan fuera de esta epica.
- Cobertura parcial de la seccion 19.4 asignada a este encargo: el plazo de conservacion vive unicamente como campo de texto estructurado en la ficha de tratamiento (HU-006-09), sin ninguna alerta de vencimiento, mientras MOD-016 (Retencion y Eliminacion) no exista.
- HU-006-19 (vincular encargados) y HU-006-20 (vincular controles de seguridad) quedan en release R2 porque su catalogo de referencia (Proveedores tipo Encargado de MOD-009, Controles de MOD-015) solo existe a partir de R2 segun la seccion 6 de las instrucciones; el resto de la epica (ficha basica, catalogo de sistemas, catalogo de datos sensibles, seis bases de licitud, workflow completo, biblioteca de plantillas, creacion desde el Diagnostico, exportacion y Mapa de Datos tabular) es R1, consistente con que MOD-006 aparece explicitamente en el nucleo vendible de la seccion 19.8. La regla de la seccion 6 sobre HU base en R1 y HU que solo necesitan modulos de R2 se redacto pensando en modulos de infraestructura; se aplica aqui el mismo criterio porque la limitacion es identica: esas dos HU no pueden funcionar sin el catalogo externo correspondiente.
- Se marcan como habilitadoras las HU que crean o mantienen la entidad Tratamiento y la entidad Sistema (HU-006-01, 02, 04, 06, 07, 10, 19, 20), por ser la capacidad base que MOD-007, MOD-009, MOD-011 y MOD-015 consumen por referencia segun la seccion L de la ficha, tal como lo pide el encargo. HU-006-13 (archivar/reactivar) queda fuera de ese grupo porque el aviso que reciben los modulos que referencian una ficha archivada se deja documentado dentro de HU-006-19, cuando el enlace con MOD-009 ya existe.
- El Mapa de Datos se construye solo como vista tabular filtrable sobre el mismo RAT (HU-006-18); el diagrama interactivo navegable que describe la seccion E de la ficha queda fuera de esta epica por ser SHOULD HAVE en la tabla Q.
- La biblioteca de tratamientos plantilla de la ficha (seccion D.6) trae 22 fichas de ejemplo, por encima del minimo de 20 que pide el encargo; el contenido detallado de cada plantilla se deja en requiere_contenido de HU-006-15 porque su redaccion final la produce el equipo legal o de contenido, no el equipo de desarrollo.
- No se crea una HU dedicada para vincular Documentos asociados (Aviso de Privacidad, contrato/DPA) ni para el campo Terceros o destinatarios de la seccion D.1: ambos son opcionales en la ficha y no son condicion de ninguna transicion de estado, asi que quedan como campos menores del alcance general sin criterios propios.
- El acceso de solo lectura del Responsable ARCO-POL (consumido por MOD-011) al RAT completo, y la lectura del Catalogo de Sistemas desde MOD-013, no requieren una HU propia: ya quedan cubiertos por los permisos de lectura descritos en los criterios de HU-006-01, HU-006-02 y HU-006-06, siguiendo la tabla de permisos de la seccion C de la ficha.
- En 02_validacion/mapa_modulos.json, MOD-006 solo declara depende_de MOD-004; esa dependencia se refleja en HU-006-16 (creacion automatica desde el Diagnostico). No se detectaron mas discrepancias entre la tabla Q de la ficha y la seccion 19.3 del roadmap para este modulo: ambas coinciden en el mismo conjunto de 7 filas MUST HAVE.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-006-01 | Crear ficha de tratamiento en Borrador | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R1 | 7 | MOD-001 |
| HU-006-02 | Completar los campos de Borrador y enviar la ficha a revision | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 5 | R1 | 8 | HU-006-01, MOD-021 |
| HU-006-03 | Marcar automaticamente como sensible una categoria de dato del catalogo cerrado | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R1 | 14 | HU-006-02, MOD-021 |
| HU-006-04 | Seleccionar la base de licitud del tratamiento con su justificacion | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 5 | R1 | 8 | HU-006-01 |
| HU-006-05 | Registrar el origen del dato y el analisis de fuente de acceso publico | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R1 | 8 | HU-006-01 |
| HU-006-06 | Dar de alta un sistema en el Catalogo de Sistemas | Responsable de Seguridad / IT | 5 | R1 | 8 | MOD-001, MOD-021 |
| HU-006-07 | Vincular el tratamiento a uno o mas sistemas del catalogo | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R1 | 8 | HU-006-01, HU-006-06 |
| HU-006-08 | Completar la descripcion, el responsable interno y la transferencia internacional | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R1 | 8 | HU-006-01, MOD-001 |
| HU-006-09 | Registrar el plazo de conservacion del tratamiento | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 2 | R1 | 8 | HU-006-01 |
| HU-006-10 | Aprobar una ficha de tratamiento y pasarla a Vigente | Aprobador | 8 | R1 | 8 | HU-006-02, HU-006-04, HU-006-05, HU-006-07, HU-006-08, HU-006-09, MOD-023, MOD-021, MOD-022 |
| HU-006-11 | Rechazar una ficha en revision y devolverla a Borrador | Aprobador | 3 | R1 | 16 | HU-006-02, MOD-021 |
| HU-006-12 | Pasar una ficha Vigente a Requiere revision y confirmarla o actualizarla | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 5 | R1 | 16 | HU-006-10, MOD-023, MOD-021, MOD-022 |
| HU-006-13 | Archivar y reactivar un tratamiento | Administrador de la organizacion | 3 | R1 | 16 | HU-006-10 |
| HU-006-14 | Eliminar definitivamente una ficha en Borrador | Administrador de la organizacion | 2 | R1 | 15 | HU-006-01 |
| HU-006-15 | Crear una ficha desde la biblioteca de tratamientos plantilla | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 5 | R1 | 17 | HU-006-01, MOD-021 |
| HU-006-16 | Crear automaticamente una ficha desde una respuesta del Diagnostico | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 5 | R1 | 17 | HU-006-15, MOD-004, MOD-021 |
| HU-006-17 | Exportar el RAT consolidado y el paquete de evidencia con verificacion de integridad | Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | 8 | R1 | 17 | HU-006-10, EP-000 |
| HU-006-18 | Consultar el Mapa de Datos como vista tabular del RAT | Responsable Legal / Compliance | 3 | R1 | 16 | HU-006-07 |
| HU-006-19 | Vincular los encargados del tratamiento a la ficha | Responsable de area (RRHH, Marketing, Operaciones, etc.) | 3 | R2 | 8 | HU-006-07, HU-006-10, MOD-009 |
| HU-006-20 | Vincular controles de seguridad y bloquear el paso a Vigente sin control en dato sensible | Responsable de Seguridad / IT | 5 | R2 | 9 | HU-006-10, MOD-015 |

## Historias

### HU-006-01. Crear ficha de tratamiento en Borrador

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** crear una ficha nueva de actividad de tratamiento en estado Borrador indicando su nombre y el area responsable, **para** empezar a registrar en el RAT un tratamiento de datos personales que mi area ejecuta.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 7 | Si |

- Fundamento: OBL-DOC-02 (Art. 4 (Medidas Organizativas, lit. d), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: -
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado que estoy creando una ficha nueva, cuando intento guardarla sin nombre ni area responsable, entonces el sistema bloquea el guardado porque ambos campos son obligatorios.
2. Dado que escribo un nombre de tratamiento de menos de 5 caracteres, cuando intento guardar la ficha, entonces el sistema rechaza el guardado y pide un nombre de al menos 5 caracteres.
3. Dado que ya existe una ficha con el mismo nombre en mi organizacion, cuando intento guardar una ficha nueva con ese mismo nombre, entonces el sistema rechaza el guardado por nombre duplicado.
4. Dado que selecciono el area responsable, cuando el area no existe en el catalogo de areas activas de MOD-001, entonces el sistema no me la ofrece como opcion.
5. Dado que completo un nombre y un area responsable validos, cuando guardo la ficha, entonces la ficha queda creada en estado Borrador y el sistema registra en el historial el evento ficha creada, con autor y fecha.
6. Dado que tengo el rol Responsable ARCO-POL, Auditor interno, Usuario de consulta o Titular, cuando intento crear una ficha de tratamiento, entonces el sistema deniega la accion.

**Reglas de negocio**

- El nombre debe ser unico dentro de la organizacion y tener al menos 5 caracteres (seccion D.1).
- Solo Responsable de area, Legal/Compliance, Delegado y Administrador pueden crear una ficha (seccion C).
- La transicion (nuevo) a Borrador exige nombre y area responsable definidos (seccion F.2).

**Fuera de alcance**

- Completar los demas campos obligatorios de Borrador (se hace en HU-006-02)
- Crear la ficha automaticamente desde una plantilla o desde el Diagnostico (HU-006-15 y HU-006-16)

- Referencia: MOD-006 secciones D.1 (Nombre del tratamiento, Area responsable), F.1 y F.2 (fila nuevo a Borrador), C (permisos)

### HU-006-02. Completar los campos de Borrador y enviar la ficha a revision

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** completar la finalidad, las categorias de titulares, si incluye menores de edad y las categorias de datos tratados, y enviar la ficha a revision, **para** que Legal o el Delegado puedan revisar el tratamiento antes de que quede vigente.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 8 | Si |

- Fundamento: OBL-DOC-02 (Art. 4 (Medidas Organizativas, lit. d), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-TRAT-01 (Art. 32, Ley para la Proteccion de Datos Personales); OBL-PRIN-02 (Art. 5 lit. g), Ley para la Proteccion de Datos Personales); OBL-SENS-01 (Art. 4 lit. g), Ley para la Proteccion de Datos Personales)
- Depende de: HU-006-01
- Modulos requeridos: MOD-021

**Criterios de aceptacion**

1. Dado que la ficha esta en Borrador, cuando escribo una finalidad de menos de 15 caracteres o identica a la descripcion breve, entonces el sistema rechaza el campo y explica la regla.
2. Dado que la ficha esta en Borrador, cuando intento enviarla a revision sin marcar al menos una categoria de titulares, entonces el sistema bloquea el envio.
3. Dado que la ficha esta en Borrador, cuando intento enviarla a revision sin marcar al menos una categoria de datos tratados, entonces el sistema bloquea el envio y no permite continuar.
4. Dado que completo Incluye menores de edad y las demas categorias de titulares, categorias de datos y finalidad, cuando envio la ficha a revision, entonces el sistema cambia su estado de Borrador a En revision.
5. Dado que la ficha pasa a En revision, cuando la transicion se completa, entonces el sistema crea una tarea de revision para Legal/Compliance o el Delegado en MOD-021 y registra el evento en el historial.
6. Dado que soy Usuario de consulta o Titular, cuando intento enviar una ficha a revision, entonces el sistema deniega la accion porque no tengo permiso de edicion sobre la ficha.
7. Dado que la ficha ya esta en un estado distinto de Borrador, cuando intento aplicar de nuevo la transicion enviar a revision, entonces el sistema la rechaza porque esa transicion solo aplica desde Borrador.

**Reglas de negocio**

- Finalidad minimo 15 caracteres y distinta de la descripcion breve (seccion D.1).
- Categorias de titulares y categorias de datos tratados exigen al menos una seleccion (seccion D.1).
- La transicion Borrador a En revision exige todos los campos marcados obligatorio desde Borrador completos (seccion F.2).

**Fuera de alcance**

- El calculo automatico del nivel de riesgo (SHOULD HAVE, tabla Q)
- La notificacion al Aprobador por riesgo Alto, que depende de ese calculo diferido

- Referencia: MOD-006 D.1 (Finalidad, Categorias de titulares, Incluye menores de edad, Categorias de datos tratados), F.2 fila Borrador a En revision

### HU-006-03. Marcar automaticamente como sensible una categoria de dato del catalogo cerrado

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** que el sistema marque en rojo y como Dato sensible cualquier categoria de datos que pertenezca al catalogo cerrado (union del Art. 4 lit. g y el Art. 59 lit. b), **para** darme cuenta de inmediato cuando el tratamiento activa el regimen reforzado de datos sensibles.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 14 | No |

- Fundamento: OBL-SENS-01 (Art. 4 lit. g), Ley para la Proteccion de Datos Personales); OBL-SENS-04 (Art. 39, Ley para la Proteccion de Datos Personales); OBL-SENS-06 (Art. 4 lit. g), Ley para la Proteccion de Datos Personales); OBL-SENS-08 (Art. 4 lit. f) y lit. g), Art. 7, Art. 12 lit. b), Art. 16 lit. g), Ley para la Proteccion de Datos Personales)
- Depende de: HU-006-02
- Modulos requeridos: MOD-021

**Criterios de aceptacion**

1. Dado que selecciono una categoria de dato de la lista cerrada de sensibles (por ejemplo Informacion biometrica o Salud fisica y mental), cuando guardo la ficha, entonces el sistema la marca visualmente en rojo y agrega la etiqueta Dato sensible visible en el listado del RAT.
2. Dado que una categoria pertenece al catalogo cerrado de sensibles, cuando intento guardarla como otros ordinarios para ocultarla, entonces el sistema rechaza ese cambio y la mantiene marcada como sensible.
3. Dado que el dato que quiero registrar no esta en ninguna de las categorias cerradas del catalogo, cuando marco la opcion otro dato sensible no listado, entonces el sistema muestra el texto: este dato no esta en el catalogo cerrado de categorias sensibles, requiere validacion de la organizacion o asesoria especializada antes de decidir si aplica el regimen reforzado.
4. Dado que marco Salud fisica y mental y el sector de la empresa registrado en MOD-001 es salud, cuando guardo la ficha, entonces el sistema muestra el aviso de revisar la Ley de Deberes y Derechos de los Pacientes con la nota de que requiere validacion de la organizacion o asesoria especializada.
5. Dado que marco Informacion biometrica, cuando guardo la ficha, entonces el sistema crea la tarea confirmar consentimiento escrito y alternativa no biometrica en MOD-021.
6. Dado que el campo de nacionalidad se declara como un atributo de tratamiento diferenciado y no solo como parte de un documento identificativo, cuando guardo la ficha, entonces el sistema pide confirmacion humana mostrando el texto: el sistema marco este dato como potencialmente sensible por su categoria, confirme con su organizacion si en este caso concreto aplica el regimen reforzado.
7. Dado que ninguna categoria de dato marcada pertenece al catalogo de sensibles, cuando guardo la ficha, entonces el sistema no agrega la etiqueta Dato sensible ni exige el analisis adicional.

**Reglas de negocio**

- El catalogo de sensibles es la union cerrada del Art. 4 lit. g y el Art. 59 lit. b, y no se puede ocultar bajo otra categoria (seccion D.3 y D.4).
- El sistema no puede precalificar la clausula abierta otras informaciones intimas de similar naturaleza (seccion H).

- Requiere contenido: Texto de ayuda de cada categoria del catalogo cerrado de datos sensibles (seccion D.4), validado por asesoria legal
- Referencia: MOD-006 D.3, D.4, G.1, G.2, G.3, seccion H filas 2 y 6

### HU-006-04. Seleccionar la base de licitud del tratamiento con su justificacion

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** elegir una de las seis bases de licitud reconocidas por la ley y escribir la justificacion de por que aplica a este tratamiento, **para** declarar la razon legal por la que mi area puede tratar estos datos personales.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 8 | Si |

- Fundamento: OBL-PRIN-02 (Art. 5 lit. g), Ley para la Proteccion de Datos Personales); OBL-TRAT-02 (Art. 28, Ley para la Proteccion de Datos Personales)
- Depende de: HU-006-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que estoy completando la ficha, cuando intento guardarla sin elegir una de las seis bases de licitud (Consentimiento expreso, Ejecucion de contrato o medidas precontractuales, Cumplimiento de obligacion legal, Proteccion de intereses vitales, Cumplimiento de un fin de interes publico, Intereses legitimos), entonces el sistema bloquea el guardado.
2. Dado que elijo una base distinta de Consentimiento expreso, cuando intento guardar sin escribir al menos 30 caracteres en la justificacion de la base de licitud, entonces el sistema bloquea el guardado.
3. Dado que elijo la base Intereses legitimos, cuando completo la justificacion, entonces el sistema exige que tambien explique por que el tratamiento no afecta de forma desproporcionada al titular, y muestra el texto: la eleccion de esta base requiere el criterio de su organizacion sobre si es defendible para este tratamiento especifico, requiere validacion de la organizacion o asesoria especializada.
4. Dado que la ficha tiene al menos una categoria de dato marcada como sensible, cuando intento guardarla sin completar la justificacion de la base de licitud, entonces el sistema bloquea el guardado aunque la base elegida sea Consentimiento expreso.
5. Dado que marco que el tratamiento invoca una excepcion del Art. 28 en lugar de consentimiento, cuando guardo la ficha, entonces el sistema exige seleccionar una de las 8 opciones de excepcion y no permite dejarla vacia.
6. Dado que guardo una base de licitud con su justificacion, cuando reviso la ficha despues, entonces el sistema nunca marca esa base como valida o invalida por si mismo, solo la deja registrada con su autor y fecha.

**Reglas de negocio**

- El sistema registra la base elegida por la empresa pero nunca decide si es valida o proporcional (seccion H, anti-feature 6).
- Justificacion obligatoria de al menos 30 caracteres si la base no es Consentimiento expreso (seccion D.1).

**Fuera de alcance**

- Cualquier validacion automatica de si la base elegida es correcta para el tratamiento

- Requiere contenido: Pregunta guiada de ponderacion de la base Intereses legitimos frente al derecho del titular (plantilla Analisis de base de interes legitimo, seccion K), validada por asesoria legal
- Referencia: MOD-006 D.1 filas Base de licitud, Justificacion de la base de licitud, Excepcion invocada; seccion H fila 1; anti-feature 6

### HU-006-05. Registrar el origen del dato y el analisis de fuente de acceso publico

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** indicar de donde proviene el dato y, si elijo fuente de acceso publico, documentar el analisis que lo respalda, **para** dejar constancia de por que puedo tratar ese dato sin pedirlo directamente al titular.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 8 | No |

- Fundamento: OBL-TRAT-03 (Art. 4 lit. l), Ley para la Proteccion de Datos Personales)
- Depende de: HU-006-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que estoy completando la ficha, cuando intento enviarla a aprobacion sin elegir el origen del dato, entonces el sistema bloquea el envio.
2. Dado que elijo el origen Fuente de acceso publico, cuando guardo la ficha, entonces el sistema activa el campo obligatorio de analisis con la pregunta guiada: explique por que esta fuente puede consultarse por disposicion de ley por cualquier persona, no basta con que sea publica o abierta en internet.
3. Dado que elijo Fuente de acceso publico y dejo vacio el campo de analisis, cuando intento guardar la ficha, entonces el sistema bloquea el guardado.
4. Dado que completo el analisis de fuente de acceso publico, cuando lo guardo, entonces el sistema muestra el texto: el sistema no determina si esta fuente cumple la definicion legal de acceso publico, requiere validacion de la organizacion o asesoria especializada, y no valida el contenido del analisis.
5. Dado que elijo un origen distinto de Fuente de acceso publico, cuando guardo la ficha, entonces el sistema no muestra el campo de analisis.

**Reglas de negocio**

- El origen del dato es obligatorio para pasar a En revision (seccion D.1).
- Si el origen es Fuente de acceso publico, el analisis documentado es obligatorio y el sistema nunca valida su contenido (seccion D.5).

- Requiere contenido: Plantilla de Analisis de fuente de acceso publico con la pregunta guiada de la seccion D.5, validada por asesoria legal
- Referencia: MOD-006 D.1 fila Origen del dato, D.5, seccion H fila 3

### HU-006-06. Dar de alta un sistema en el Catalogo de Sistemas

**Como** Responsable de Seguridad / IT, **quiero** registrar un sistema nuevo en el Catalogo de Sistemas con su tipo, pais de alojamiento y responsable tecnico, **para** tener una unica lista de sistemas que el RAT y otros modulos puedan referenciar sin duplicar el dato.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 8 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: MOD-001, MOD-021

**Criterios de aceptacion**

1. Dado que quiero registrar un sistema nuevo, cuando dejo vacio el nombre, el tipo de sistema o el pais de alojamiento, entonces el sistema bloquea el guardado.
2. Dado que ya existe un sistema con el mismo nombre en mi organizacion, cuando intento guardar otro con ese mismo nombre, entonces el sistema rechaza el guardado por duplicado.
3. Dado que elijo el tipo de sistema SaaS de un proveedor, cuando guardo el sistema, entonces el campo Proveedor asociado queda disponible para vincularlo al catalogo de Proveedores tipo Encargado de MOD-009, sin bloquear el alta mientras ese catalogo no exista.
4. Dado que no se cual es el pais de alojamiento, cuando elijo la opcion No se sabe / pendiente de confirmar, entonces el sistema guarda el registro y crea una tarea en MOD-021 para averiguar el pais.
5. Dado que dejo vacio el responsable tecnico interno, cuando intento guardar el sistema, entonces el sistema bloquea el guardado porque ese campo es obligatorio.
6. Dado que tengo el rol Responsable de area, Aprobador o Auditor interno, cuando intento dar de alta un sistema en el catalogo, entonces el sistema deniega la accion porque esa alta es exclusiva de Administrador y Responsable de Seguridad/IT.

**Reglas de negocio**

- Nombre unico dentro de la organizacion (seccion D.7).
- Dar de alta un sistema en el catalogo es exclusivo de Administrador y Responsable de Seguridad/IT (seccion C).
- Si el pais de alojamiento queda pendiente de confirmar, el sistema crea una tarea para averiguarlo (seccion D.7).

**Fuera de alcance**

- Verificacion tecnica de que el pais de alojamiento declarado es correcto

- Referencia: MOD-006 D.7, C (nota especifica del modulo)

### HU-006-07. Vincular el tratamiento a uno o mas sistemas del catalogo

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** elegir en que sistema o sistemas del Catalogo de Sistemas se procesa mi tratamiento, o agregar uno nuevo si no esta en la lista, **para** que quede claro donde vive el dato y esa informacion alimente el Mapa de Datos.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 8 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-006-01, HU-006-06
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que estoy completando la ficha, cuando intento enviarla a aprobacion sin vincular al menos un sistema, entonces el sistema bloquea el envio.
2. Dado que el sistema donde vive el dato no esta en el catalogo, cuando elijo Agregar sistema nuevo, entonces el sistema me permite darlo de alta y lo deja disponible para vincularlo a la ficha.
3. Dado que vinculo mas de un sistema a la misma ficha, cuando la guardo, entonces el sistema conserva todos los sistemas vinculados y los muestra en el listado y en el Mapa de Datos.
4. Dado que un sistema vinculado a mi ficha cambia a estado Dado de baja, cuando ese cambio ocurre, entonces mi ficha, si esta Vigente, pasa a Requiere revision con la nota de que el sistema fue dado de baja.
5. Dado que intento vincular como sistema un texto libre que no existe en el catalogo, cuando guardo la ficha, entonces el sistema rechaza el texto libre y solo permite seleccionar del catalogo o crear un sistema nuevo.

**Reglas de negocio**

- Al menos un sistema vinculado es obligatorio para pasar a En revision (seccion D.1).
- Un sistema dado de baja con tratamientos Vigentes que lo referencian los marca Requiere revision (seccion G.8, seccion I).

- Referencia: MOD-006 D.1 fila Sistema o sistemas donde se procesa, G.8, I fila Sistema dado de baja

### HU-006-08. Completar la descripcion, el responsable interno y la transferencia internacional

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** escribir la descripcion breve del tratamiento, asignar su responsable interno y declarar si hay transferencia de datos fuera de El Salvador, **para** dejar la ficha lista con los datos que Legal necesita para aprobarla.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 8 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales); OBL-TRANSF-05 (Art. 45, Ley para la Proteccion de Datos Personales)
- Depende de: HU-006-01
- Modulos requeridos: MOD-001

**Criterios de aceptacion**

1. Dado que estoy completando la ficha, cuando escribo mas de 1000 caracteres en la descripcion breve, entonces el sistema rechaza el exceso de caracteres.
2. Dado que intento enviar la ficha a aprobacion sin asignar un responsable interno, entonces el sistema bloquea el envio.
3. Dado que asigno como responsable interno a un usuario sin el rol Responsable de area o superior, cuando guardo la ficha, entonces el sistema rechaza esa asignacion.
4. Dado que marco Hay transferencia fuera de El Salvador: Si, cuando guardo la ficha, entonces el sistema exige el pais de alojamiento o destino y no permite dejarlo vacio.
5. Dado que marco Hay transferencia fuera de El Salvador: No, cuando guardo la ficha, entonces el sistema no exige el campo de pais de destino.
6. Dado que dejo el campo Hay transferencia fuera de El Salvador sin responder, cuando intento enviar la ficha a aprobacion, entonces el sistema bloquea el envio porque ese campo es obligatorio para pasar a En revision.

**Reglas de negocio**

- Descripcion breve hasta 1000 caracteres (seccion D.1).
- Responsable interno obligatorio para pasar a En revision, con rol Responsable de area o superior (seccion D.1).
- Hay transferencia fuera de El Salvador es obligatorio para pasar a En revision; el pais de destino solo se exige si la respuesta es Si (seccion D.1).

**Fuera de alcance**

- La deteccion automatica de transferencia posiblemente no documentada contra MOD-010 (SHOULD HAVE, tabla Q); esa alerta queda fuera de este modulo mientras MOD-010 no exista

- Referencia: MOD-006 D.1 filas Descripcion breve, Responsable interno del tratamiento, Hay transferencia fuera de El Salvador, Pais de alojamiento o destino

### HU-006-09. Registrar el plazo de conservacion del tratamiento

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** indicar cuanto tiempo se conservan los datos de este tratamiento y, si elijo indefinido, justificarlo, **para** dejar constancia del plazo de conservacion mientras el motor de retencion no exista.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 8 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-006-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que completo el plazo de conservacion, cuando elijo una de las opciones Anios, Meses o Mientras dure la relacion mas N anios adicionales, entonces el sistema guarda el numero y la unidad como texto estructurado del tratamiento.
2. Dado que elijo la opcion Indefinido, cuando intento guardar sin escribir una justificacion, entonces el sistema bloquea el guardado.
3. Dado que elijo Indefinido y completo la justificacion, cuando guardo la ficha, entonces el sistema muestra el texto: un plazo de conservacion indefinido requiere una justificacion legal especifica, requiere validacion de la organizacion o asesoria especializada.
4. Dado que intento enviar la ficha a aprobacion sin completar el plazo de conservacion, entonces el sistema bloquea el envio porque es obligatorio para pasar a En revision.
5. Dado que el plazo de conservacion queda guardado como campo de texto, cuando reviso la ficha mas adelante, entonces el sistema no genera ninguna alerta automatica de vencimiento sobre este campo mientras MOD-016 no exista.

**Reglas de negocio**

- El plazo de conservacion es un campo estructurado (numero y unidad, o Indefinido con justificacion obligatoria), obligatorio para pasar a En revision (seccion D.1).
- Mientras MOD-016 no exista, este campo no dispara ninguna alerta automatica de vencimiento (cobertura parcial, seccion 19.4).

- Referencia: MOD-006 D.1 fila Plazo de conservacion / retencion, seccion H fila 7
- Notas: Cobertura parcial de la seccion 19.4 asignada al encargo: solo campo de texto en el tratamiento, sin alertas, mientras MOD-016 no exista.

### HU-006-10. Aprobar una ficha de tratamiento y pasarla a Vigente

**Como** Aprobador, **quiero** aprobar una ficha que esta En revision cuando todos sus campos obligatorios estan completos, **para** que el tratamiento quede Vigente y sirva como referencia confiable para el resto de la empresa.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 8 | Si |

- Fundamento: OBL-DOC-02 (Art. 4 (Medidas Organizativas, lit. d), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-PRIN-02 (Art. 5 lit. g), Ley para la Proteccion de Datos Personales); OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-006-02, HU-006-04, HU-006-05, HU-006-07, HU-006-08, HU-006-09
- Modulos requeridos: MOD-023, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que la ficha esta En revision con todos los campos obligatorio para pasar a En revision completos, cuando la apruebo, entonces el sistema cambia su estado a Vigente, calcula la fecha de proxima revision a 12 meses por defecto usando el motor de plazos de MOD-023, y registra en el historial mi identidad, la fecha y mi comentario si lo dejo.
2. Dado que la ficha tiene al menos una categoria de dato sensible marcada y el campo de justificacion de la base de licitud esta vacio, cuando intento aprobarla, entonces el sistema bloquea la aprobacion.
3. Dado que soy el mismo usuario que registro una ficha con dato sensible o riesgo alto, cuando intento aprobarla, entonces el sistema deniega la aprobacion porque exige el rol Aprobador o Legal/Compliance distinto de quien la registro, salvo que mi organizacion este por debajo del umbral configurable de tamano (propuesta inicial 50 empleados), en cuyo caso el sistema permite la autoaprobacion mostrando siempre la advertencia visible de autorrevision.
4. Dado que la ficha pasa a Vigente, cuando la transicion se completa, entonces el sistema crea o notifica las tareas correspondientes a traves de MOD-021 y MOD-022 hacia los modulos que la consultan.
5. Dado que la ficha esta Vigente, cuando alguien intenta modificar directamente la finalidad o la base de licitud sin pasar de nuevo por revision, entonces el sistema bloquea la edicion directa de esos campos criticos.
6. Dado que tengo el rol Responsable de area, Usuario de consulta o Auditor interno, cuando intento aprobar una ficha En revision, entonces el sistema deniega la accion porque no tengo el rol Aprobador, Legal/Compliance o Delegado.
7. Dado que la ficha En revision no tiene todos los campos obligatorio para pasar a En revision completos, cuando intento aprobarla, entonces el sistema bloquea la aprobacion y senala los campos faltantes.

**Reglas de negocio**

- Separacion de funciones: quien registra un tratamiento de riesgo alto o con dato sensible no puede aprobarlo, salvo pyme con advertencia visible de autorrevision (seccion C).
- La aprobacion bloquea la edicion directa de campos criticos sin pasar de nuevo por revision (seccion F.2).
- La fecha de proxima revision se calcula con el motor de plazos compartido MOD-023, nunca de forma local (seccion P).

**Fuera de alcance**

- La exigencia de decision explicita sobre EIPD para riesgo Alto, porque el calculo automatico de riesgo es SHOULD HAVE en la tabla Q
- El bloqueo por falta de control de seguridad enlazado en dato biometrico, que se agrega en HU-006-20 cuando MOD-015 este disponible

- Referencia: MOD-006 F.1, F.2 fila En revision a Vigente (Aprobar), seccion C (separacion de funciones), R.6

### HU-006-11. Rechazar una ficha en revision y devolverla a Borrador

**Como** Aprobador, **quiero** rechazar una ficha En revision dejando un comentario obligatorio sobre lo que falta, **para** que el Responsable de area sepa que debe corregir antes de volver a enviarla.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 16 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-006-02
- Modulos requeridos: MOD-021

**Criterios de aceptacion**

1. Dado que la ficha esta En revision, cuando la rechazo sin escribir un comentario, entonces el sistema bloquea el rechazo porque el comentario es obligatorio.
2. Dado que rechazo la ficha con un comentario, cuando la accion se completa, entonces el sistema cambia su estado a Borrador y crea una tarea para el Responsable de area con el motivo del rechazo.
3. Dado que la ficha vuelve a Borrador, cuando reviso su historial, entonces el sistema registra el evento de rechazo con mi identidad, la fecha y el comentario.
4. Dado que tengo el rol Responsable de area o Usuario de consulta, cuando intento rechazar una ficha En revision, entonces el sistema deniega la accion.
5. Dado que la ficha ya esta en Borrador, Vigente, Requiere revision o Archivado, cuando intento aplicar la accion rechazar, entonces el sistema la rechaza porque esa transicion solo aplica desde En revision.

**Reglas de negocio**

- Rechazar exige un comentario obligatorio y crea una tarea para el Responsable de area con el motivo (seccion F.2).

- Referencia: MOD-006 F.2 fila En revision a Borrador (Rechazar / devolver)

### HU-006-12. Pasar una ficha Vigente a Requiere revision y confirmarla o actualizarla

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** que el sistema marque automaticamente como Requiere revision una ficha Vigente cuando vence su fecha de proxima revision o cuando cambia un campo material, y poder confirmarla o actualizarla, **para** mantener el RAT vivo y no dejarlo desactualizado.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 16 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-006-10
- Modulos requeridos: MOD-023, MOD-021, MOD-022

**Criterios de aceptacion**

1. Dado que una ficha Vigente llega a su fecha de proxima revision calculada por MOD-023, cuando esa fecha se cumple, entonces el sistema cambia su estado a Requiere revision y crea una tarea para el Responsable de area con copia a mi.
2. Dado que una ficha Vigente cambia su base de licitud, agrega una categoria sensible nueva o cambia de sistema, cuando guardo ese cambio, entonces el sistema la marca automaticamente como Requiere revision sin bloquear su consulta por otros modulos, mostrando la marca pendiente de reconfirmacion.
3. Dado que una ficha esta Requiere revision y la informacion sigue siendo correcta, cuando la confirmo sin cambios, entonces el sistema la regresa a Vigente y actualiza la fecha de proxima revision.
4. Dado que una ficha esta Requiere revision y hace falta actualizar un campo material, cuando el Responsable de area la actualiza, entonces el sistema la envia de nuevo a En revision y exige repetir el flujo completo de aprobacion.
5. Dado que confirmo o actualizo una ficha Requiere revision, cuando la accion se completa, entonces el sistema registra el evento en el historial con mi identidad y la fecha.
6. Dado que tengo el rol Usuario de consulta, cuando intento confirmar una ficha Requiere revision, entonces el sistema deniega la accion.

**Reglas de negocio**

- Llegar a la fecha de proxima revision o un cambio material pasa la ficha Vigente a Requiere revision de forma automatica (seccion F.2, seccion G.7).
- Confirmar sin cambios regresa la ficha a Vigente; actualizar con cambios materiales exige repetir el flujo de En revision (seccion F.2).

- Referencia: MOD-006 F.2 filas Vigente a Requiere revision y Requiere revision a Vigente/En revision, R.6

### HU-006-13. Archivar y reactivar un tratamiento

**Como** Administrador de la organizacion, **quiero** archivar un tratamiento que dejo de ejecutarse, declarando el motivo, y poder reactivarlo despues si vuelve a ejecutarse, **para** reflejar en el RAT que ese tratamiento ya no esta activo sin perder su historial.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 16 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-006-10
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que una ficha esta Vigente o Requiere revision, cuando la archivo sin declarar el motivo y la fecha de cese, entonces el sistema bloquea la accion.
2. Dado que archivo una ficha con motivo y fecha de cese, cuando la accion se completa, entonces el sistema cambia su estado a Archivado, conserva integro su historial y la deja visible como referencia historica de forma indefinida.
3. Dado que una ficha esta Archivada, cuando la reactivo porque el tratamiento vuelve a ejecutarse, entonces el sistema la envia al estado En revision conservando el historial anterior y abre un nuevo periodo de vigencia.
4. Dado que intento eliminar fisicamente una ficha Archivada, cuando lo intento, entonces el sistema lo rechaza porque el archivado nunca borra el historial ni permite el borrado fisico.
5. Dado que tengo el rol Responsable de area o Usuario de consulta, cuando intento archivar o reactivar una ficha, entonces el sistema deniega la accion porque esa capacidad es de Administrador, Delegado o Legal/Compliance.

**Reglas de negocio**

- Archivar exige motivo y fecha de cese declarados; nunca elimina la ficha ni su historial (seccion F.2).
- Reactivar regresa la ficha a En revision conservando el historial anterior (seccion F.2).
- Archivar y reactivar son exclusivos de Administrador, Delegado y Legal/Compliance (seccion C).

- Referencia: MOD-006 F.2 filas Archivar y Reactivar, seccion C

### HU-006-14. Eliminar definitivamente una ficha en Borrador

**Como** Administrador de la organizacion, **quiero** eliminar de forma fisica una ficha que sigue en Borrador y que nadie mas ha editado, **para** limpiar el RAT de fichas creadas por error sin dejar un registro incompleto.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 15 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-006-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que la ficha esta en Borrador y ningun usuario distinto de quien la creo la ha editado, cuando la elimino, entonces el sistema la borra de forma fisica y no queda registro de ella en el listado del RAT.
2. Dado que la ficha ya paso alguna vez por En revision, cuando intento eliminarla, entonces el sistema rechaza la eliminacion y solo permite archivarla.
3. Dado que otro usuario distinto de quien la creo ya edito la ficha en Borrador, cuando intento eliminarla, entonces el sistema rechaza la eliminacion.
4. Dado que tengo el rol Responsable de area, Delegado o Legal/Compliance, cuando intento eliminar una ficha en Borrador, entonces el sistema deniega la accion porque esa capacidad es exclusiva del Administrador.

**Reglas de negocio**

- Eliminar de forma fisica solo aplica a una ficha en Borrador que nunca paso a En revision y que nadie mas edito (seccion F.2).
- Eliminar es exclusivo del Administrador (seccion C).

- Referencia: MOD-006 F.2 fila Borrador (sin historial) a eliminada, seccion C, seccion O

### HU-006-15. Crear una ficha desde la biblioteca de tratamientos plantilla

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** elegir una plantilla de la biblioteca de al menos 20 tratamientos comunes para crear una ficha nueva ya precargada, **para** no tener que llenar cada campo desde cero para un tratamiento tipico de mi area.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 17 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-006-01
- Modulos requeridos: MOD-021

**Criterios de aceptacion**

1. Dado que abro la biblioteca de tratamientos plantilla, cuando la reviso, entonces el sistema muestra al menos 20 plantillas distintas, cada una con area tipica, finalidad sugerida, base de licitud sugerida, categorias de datos y retencion sugerida.
2. Dado que elijo una plantilla, cuando la selecciono, entonces el sistema copia sus valores sugeridos a una ficha nueva en estado Borrador, editable en todos sus campos.
3. Dado que la ficha se creo desde una plantilla, cuando reviso su historial, entonces el sistema registra que se origino desde esa plantilla especifica, con el nombre de la plantilla.
4. Dado que la ficha se creo desde una plantilla, cuando intento marcarla directamente como Vigente sin pasar por En revision y aprobacion, entonces el sistema rechaza ese cambio de estado directo.
5. Dado que se crea una ficha desde una plantilla, cuando la creacion se completa, entonces el sistema asigna una tarea en MOD-021 al Responsable de area sugerido por la plantilla para completar la ficha.

**Reglas de negocio**

- Elegir una plantilla copia sus valores sugeridos a una ficha nueva en Borrador, editable en su totalidad (seccion D.6).
- El sistema deja constancia en el historial de que la ficha se origino desde una plantilla y cual (seccion D.6).

- Requiere contenido: Contenido completo de al menos 20 tratamientos plantilla (seccion D.6): nombre, area tipica, finalidad sugerida, categorias de titulares y de datos, base de licitud sugerida, origen tipico, sistema tipico, retencion sugerida y riesgo inicial sugerido, validado por el equipo legal o de contenido antes de publicarse
- Referencia: MOD-006 D.6, K, Q fila Biblioteca inicial de tratamientos plantilla

### HU-006-16. Crear automaticamente una ficha desde una respuesta del Diagnostico

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** que el sistema cree automaticamente una ficha en Borrador cuando mi respuesta en el Diagnostico corresponde a una plantilla de la biblioteca, **para** empezar a completar el RAT sin tener que crear la ficha manualmente desde cero.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 17 | No |

- Fundamento: OBL-DOC-02 (Art. 4 (Medidas Organizativas, lit. d), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: HU-006-15
- Modulos requeridos: MOD-004, MOD-021

**Criterios de aceptacion**

1. Dado que respondo el Diagnostico y mi respuesta corresponde a una plantilla de la biblioteca, cuando cierro esa seccion del Diagnostico, entonces el sistema crea automaticamente una ficha en Borrador a partir de esa plantilla.
2. Dado que se crea la ficha automaticamente, cuando la creacion se completa, entonces el sistema asigna una tarea en MOD-021 al Responsable de area sugerido y enlaza el disparador del diagnostico en el historial de la ficha.
3. Dado que mi organizacion desactivo la creacion automatica desde el Diagnostico, cuando respondo una pregunta que normalmente dispara una ficha, entonces el sistema no crea la ficha automaticamente y deja la creacion manual disponible.
4. Dado que ya existe una ficha Vigente o en Borrador para el mismo tratamiento sugerido, cuando respondo de nuevo esa pregunta del Diagnostico, entonces el sistema no duplica la ficha.

**Reglas de negocio**

- Una respuesta del diagnostico que corresponde a una plantilla de la biblioteca crea automaticamente una ficha en Borrador (seccion G.9).
- La empresa puede desactivar la creacion automatica y crear la ficha manualmente (seccion G.9).

- Referencia: MOD-006 G.9, E fila Tarea completar ficha de tratamiento, L

### HU-006-17. Exportar el RAT consolidado y el paquete de evidencia con verificacion de integridad

**Como** Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), **quiero** exportar el listado completo del RAT filtrado por area, estado, base de licitud o riesgo, y generar el paquete de evidencia con un mecanismo de verificacion de integridad, **para** entregar una prueba confiable del cumplimiento de OBL-DOC-02 a un auditor o a la ACE.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 8 | R1 | 17 | No |

- Fundamento: OBL-DOC-02 (Art. 4 (Medidas Organizativas, lit. d), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-006-10
- Modulos requeridos: EP-000

**Criterios de aceptacion**

1. Dado que exporto el RAT consolidado, cuando elijo los filtros de area, estado, base de licitud y sensibilidad, entonces el sistema genera el archivo en PDF y en CSV con solo las fichas que cumplen esos filtros.
2. Dado que exporto el paquete de evidencia del RAT, cuando la exportacion se completa, entonces el sistema entrega un archivo ZIP con el RAT, el historial de cambios y las aprobaciones, mas un archivo de verificacion de integridad que permite comprobar despues que no fue alterado.
3. Dado que exporto el RAT o el paquete de evidencia, cuando la exportacion se completa, entonces el sistema registra en el historial y en el AuditLog transversal mi identidad, la fecha y que se exporto.
4. Dado que tengo el rol Responsable de area o Usuario de consulta, cuando intento exportar el RAT completo o el paquete de evidencia, entonces el sistema deniega la accion porque esa exportacion exige rol Administrador, Delegado o Legal/Compliance.
5. Dado que soy Auditor externo (invitado), cuando intento exportar, entonces el sistema solo me permite exportar lo que se me compartio explicitamente, nunca el RAT completo.

**Reglas de negocio**

- Exportar el RAT completo o el paquete de evidencia exige rol Administrador, Delegado o Legal/Compliance, nunca un Responsable de area por si solo (seccion C).
- Todo paquete de evidencia exportado incluye un mecanismo propio de verificacion de integridad (anti-feature 25).

- Requiere contenido: Texto de descargo estandar del paquete de evidencia y del RAT exportado, validado por el equipo legal o de contenido
- Referencia: MOD-006 E, J, N, C fila Exportar RAT / paquete de evidencia

### HU-006-18. Consultar el Mapa de Datos como vista tabular del RAT

**Como** Responsable Legal / Compliance, **quiero** ver el recorrido de cada tratamiento (origen, sistema, area, proveedor, pais, eliminacion) como una tabla filtrable sobre la misma informacion del RAT, **para** detectar de un vistazo donde esta cada dato sin depender de un diagrama interactivo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 16 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-006-07
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que abro el Mapa de Datos, cuando lo consulto, entonces el sistema muestra una tabla con origen, sistema, area, proveedor si existe, pais y plazo de conservacion de cada ficha, calculada en tiempo real a partir del RAT.
2. Dado que filtro el Mapa de Datos por area, pais o tipo de sistema, cuando aplico el filtro, entonces el sistema muestra solo las filas que cumplen ese filtro.
3. Dado que el Mapa de Datos es una vista tabular en este MVP, cuando lo abro, entonces el sistema no ofrece un diagrama interactivo navegable, solo la tabla y su exportacion como PDF o CSV.
4. Dado que tengo el rol Titular o Usuario de consulta, cuando intento abrir el Mapa de Datos, entonces el sistema deniega el acceso porque nunca es visible desde el Portal del Titular ni para ese rol.
5. Dado que tengo el rol Delegado, Legal/Compliance o Auditor interno, cuando abro el Mapa de Datos, entonces el sistema me permite verlo con los mismos permisos de lectura que tengo sobre el RAT.

**Reglas de negocio**

- El Mapa de Datos se recalcula en tiempo real a partir del RAT, nunca es una base independiente (seccion A).
- Los permisos de lectura del Mapa de Datos siguen exactamente los mismos roles que el RAT (seccion P).

**Fuera de alcance**

- El diagrama interactivo navegable (SHOULD HAVE, tabla Q), que se construye en una version posterior

- Referencia: MOD-006 E fila Mapa de Datos (vista), Q, R.4, seccion P

### HU-006-19. Vincular los encargados del tratamiento a la ficha

**Como** Responsable de area (RRHH, Marketing, Operaciones, etc.), **quiero** enlazar a la ficha el o los proveedores tipo Encargado que procesan estos datos por cuenta de mi empresa, **para** que quede claro que tratamiento delega mi empresa a cada proveedor externo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 8 | Si |

- Fundamento: OBL-PROV-01 (Art. 33 inc. 2, Ley para la Proteccion de Datos Personales)
- Depende de: HU-006-07, HU-006-10
- Modulos requeridos: MOD-009

**Criterios de aceptacion**

1. Dado que uno de los sistemas vinculados a mi ficha es de tipo SaaS externo, cuando guardo la ficha, entonces el sistema sugiere automaticamente el proveedor asociado a ese sistema desde el catalogo de MOD-009.
2. Dado que un sistema vinculado es externo y no enlazo ningun encargado, cuando intento enviar la ficha a aprobacion, entonces el sistema bloquea el envio porque el campo es obligatorio en ese caso.
3. Dado que enlazo un encargado a la ficha, cuando la ficha pasa a Vigente, entonces el sistema notifica a MOD-009 para verificar que exista un contrato o DPA vigente con ese encargado, y crea una tarea si no existe.
4. Dado que la ficha con un encargado enlazado se archiva, cuando el archivado se completa, entonces MOD-009 recibe la alerta de que el tratamiento de origen se archivo, sin que eso borre el enlace historico.
5. Dado que ningun sistema vinculado es externo, cuando guardo la ficha sin enlazar ningun encargado, entonces el sistema lo permite porque el campo es opcional en ese caso.

**Reglas de negocio**

- Encargados del tratamiento es opcional en Borrador y obligatorio si algun sistema vinculado es externo (seccion D.1).
- Si el sistema es SaaS externo, el sistema sugiere automaticamente el proveedor asociado (seccion D.1).

- Referencia: MOD-006 D.1 fila Encargados del tratamiento involucrados, G.10, L
- Notas: Depende del catalogo de Proveedores tipo Encargado de MOD-009 (R2); mientras MOD-009 no exista, el campo Encargados del tratamiento queda deshabilitado en la ficha sin bloquear el resto del flujo R1.

### HU-006-20. Vincular controles de seguridad y bloquear el paso a Vigente sin control en dato sensible

**Como** Responsable de Seguridad / IT, **quiero** enlazar a la ficha los controles de seguridad del catalogo de MOD-015 que protegen ese tratamiento, **para** dejar evidencia de que un dato sensible como la informacion biometrica esta protegido antes de que el tratamiento quede Vigente.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 9 | Si |

- Fundamento: OBL-SEG-02 (Art. 4 (Medidas Organizativas, lit. a-f), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: HU-006-10
- Modulos requeridos: MOD-015

**Criterios de aceptacion**

1. Dado que la ficha tiene marcada la categoria Informacion biometrica y no tiene ningun control de MOD-015 enlazado, cuando alguien intenta aprobarla, entonces el sistema bloquea el paso a Vigente con la alerta Dato biometrico sin control de seguridad enlazado.
2. Dado que enlazo al menos un control de tipo cifrado o control de acceso a una ficha con dato sensible, cuando intento aprobarla despues, entonces el sistema ya no bloquea la aprobacion por falta de control.
3. Dado que la ficha no tiene ninguna categoria de dato sensible marcada, cuando la envio a aprobacion sin enlazar controles de seguridad, entonces el sistema no exige ese campo.
4. Dado que enlazo un control de MOD-015 a la ficha, cuando lo guardo, entonces el sistema registra la fecha del enlace en el historial de la ficha.
5. Dado que tengo el rol Responsable de area, cuando intento enlazar un control de seguridad a la ficha, entonces el sistema me permite proponerlo, pero solo Responsable de Seguridad/IT, Legal/Compliance, Delegado o Administrador pueden confirmarlo como enlazado.

**Reglas de negocio**

- Controles de seguridad es opcional en Borrador y obligatorio para pasar a Vigente; si hay dato sensible, exige al menos un control de tipo cifrado o control de acceso (seccion D.1).
- Sin ese control enlazado, la ficha con dato biometrico no puede pasar a Vigente (seccion I, alerta Dato biometrico sin control de seguridad enlazado).

- Referencia: MOD-006 D.1 fila Controles de seguridad aplicados, seccion I fila Dato biometrico sin control de seguridad enlazado
- Notas: Depende del catalogo de controles de MOD-015 (R2); hasta entonces, la regla de bloqueo de HU-006-10 para dato sensible no incluye esta verificacion especifica de control enlazado.

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Ficha de actividad de tratamiento (campos basicos: nombre, area, finalidad, base de licitud, categorias, sistema) | HU-006-01, HU-006-02, HU-006-04, HU-006-06, HU-006-07 |
| Catalogo cerrado de categorias de datos sensibles (union Art. 4 lit. g / Art. 59 lit. b) con marcado automatico | HU-006-03 |
| Seleccion obligatoria de una de las seis bases de licitud con justificacion | HU-006-04 |
| Workflow de estados (Borrador, En revision, Vigente, Requiere revision, Archivado) con aprobacion | HU-006-02, HU-006-10, HU-006-11, HU-006-12, HU-006-13 |
| Catalogo de sistemas (alta y edicion unica) | HU-006-06 |
| Biblioteca inicial de tratamientos plantilla (minimo 20) | HU-006-15 |
| Exportacion de RAT con verificacion de integridad (hash) | HU-006-17 |
