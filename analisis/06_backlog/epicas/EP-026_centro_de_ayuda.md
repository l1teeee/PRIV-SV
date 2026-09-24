# EP-026 Centro de Ayuda (MOD-026)

**Objetivo.** Ofrecer, en el campo, seccion o paso de cualquier modulo MUST HAVE donde surja una duda, una tarjeta de ayuda de 4 partes (que es, por que tengo que hacer esto, fundamento y cuando necesito ayuda juridica) y un Glosario buscable con descargo estandar siempre visible, con todo el contenido redactado, revisado legalmente, publicado y versionado por el equipo de contenido del producto con separacion de funciones, y con marca manual para revision cuando el equipo de contenido detecta un cambio de regimen en MOD-024, sin que el sistema decida nunca por el usuario si su caso necesita asesoria juridica.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R1 | 10 | 32 | 32 | 0 | [MOD-026](../../03_modulos/MOD-026_ficha.md) |

**Notas de la epica.**

- MOD-026 no es propietario ni colaborador de ninguna obligacion (mapa_modulos.json y matriz_obligaciones.json, verificado por busqueda directa, 0 resultados; asi lo declara el encabezado de MOD-026_ficha.md). Por eso el campo fundamento de las 10 HU de esta epica queda vacio en todas: su valor legal es el Principio de Transparencia (Art. 5 lit. e LPDP), que no tiene registro OBL-PRIN propio en matriz_obligaciones.json (nota final 1 de la ficha), por lo que esta epica no inventa un OBL-ID para citarlo.
- Release: las 10 HU de esta epica quedan en R1. La seccion 19.9 del roadmap ubica a MOD-026 en la capa de infraestructura transversal que se construye desde el inicio como esqueleto completo (estructura de tarjeta de 4 partes), y precisa que el contenido de cada articulo crece con cada modulo de proceso que se libera despues, sin que eso implique construir mecanismo nuevo. Las 5 indicaciones especificas del encargo (tarjeta de 4 partes, ciclo de vida con separacion de funciones, glosario, descargo, marca manual) son integramente ese esqueleto: ninguna depende solo de que existan los modulos de R2 (MOD-007, MOD-009, MOD-011, MOD-013, MOD-015, MOD-017, MOD-019 completo, MOD-020), porque el mecanismo de MOD-026 es generico y no especifico de ningun modulo de contenido. La mencion de MOD-026 completo en R2 (seccion 6 de las instrucciones) se interpreta como el crecimiento del catalogo de articulos especificos de cada modulo (contenido, fuera de esta epica por instruccion expresa del encargo), no como una segunda tanda de HU de mecanismo.
- Rol de las HU de gobernanza de contenido (HU-026-01, 02, 03, 09 y 10): se usa Equipo de contenido del producto (proveedor) para las tres funciones separadas que describe el encargo (redactar, revision legal, publicar/versionar), siguiendo la instruccion literal del encargo y el criterio de 04_secciones/11_roles_y_permisos.md (linea 655), que agrupa autor, revisor legal y responsable de publicacion bajo esa misma etiqueta de rol de proveedor. La lista cerrada de roles de la seccion 4 de las instrucciones no incluye un rol separado de revisor legal, y MOD-026_ficha.md seccion C exige la separacion de funciones como una regla de proceso (quien redacta nunca es quien revisa ni quien publica), no como un catalogo de roles distintos; esa separacion queda modelada en los criterios de aceptacion de HU-026-03 (rechazo si el revisor es la misma persona que el autor), no en el campo rol.
- PP-OPS-04 (04_secciones/24_preguntas_pendientes.md) se cita en HU-026-01, 02, 03, 09 y 10 porque esa pregunta pendiente senala que ninguna ficha detalla en profundidad el proceso operativo continuo de autoria y aprobacion del equipo de contenido del proveedor. No se marca requiere_validacion_legal en ninguna, porque PP-OPS-04 es una pregunta de proceso de producto (dueno: Equipo de producto), no una pregunta juridica de fondo, y su propio hito es V1 (el contenido minimo del MVP ya queda cubierto por el proceso de analisis funcional vigente); no bloquea la construccion de estas HU en el MVP.
- Exclusiones confirmadas contra la tabla Q de la ficha y contra el encargo: sincronizacion automatica con la bandera de MOD-024 (SHOULD HAVE, automatizaciones 1 y 6 de la seccion G de la ficha quedan reemplazadas por la marca manual de HU-026-09); boton necesito ayuda juridica con tarea sugerida en MOD-021 (SHOULD HAVE, automatizacion 4); retroalimentacion fue util / no fue util con metricas de confusion (SHOULD HAVE); niveles Basico, Intermedio y Especialista con navegacion completa (COULD HAVE y anti-feature 24 de 22_anti_features.md); escalamiento formal integrado para invitar a un Asesor externo desde MOD-026 (COULD HAVE); exportacion de Glosario y catalogo por modulo en PDF (COULD HAVE). Ninguna de estas 6 funcionalidades tiene HU en esta epica, ni depende_de_modulos hacia MOD-021 o MOD-022 en ninguna HU, porque la unica automatizacion de esta ficha que los usaba (automatizacion 4) queda fuera de alcance.
- El texto de cada HelpArticle es contenido, no una HU por articulo (instruccion expresa del encargo): el catalogo inicial de 3 a 6 conceptos por cada uno de los modulos MUST HAVE (seccion D.1 de la ficha, hasta 26 catalogos) se declara como requiere_contenido de HU-026-01 y HU-026-03, junto con la redaccion final del descargo estandar (HU-026-07); esta epica construye el mecanismo que permite crear, revisar, publicar y mostrar ese contenido, nunca el contenido en si.
- Los conceptos 1 y 2 de la seccion R de MOD-012_ficha.md (que es el Portal del Titular, que es el codigo de verificacion) se muestran embebidos directamente en la propia interfaz del Portal del Titular, construidos por MOD-012, no por una HU de esta epica (ficha, seccion B, fila Titular); esta epica los deja fuera de alcance de HU-026-05 y HU-026-06 de forma expresa.
- Ninguna HU de gobernanza de contenido (HU-026-01, 02, 03, 09, 10) declara depende_de_modulos hacia MOD-021 o MOD-022: estas acciones ocurren fuera del RBAC de la organizacion cliente (ficha, seccion C) y sus propios avisos usan el canal interno del proveedor (ficha, seccion I), distinto del Centro de Tareas y de Notificaciones que sirven a la organizacion cliente.
- Sin discrepancia entre la tabla Q de la ficha y 19.3 del roadmap: ambas listan de forma identica las 5 funcionalidades MUST HAVE de esta epica y las mismas exclusiones SHOULD HAVE/COULD HAVE, por lo que no aplica la regla de la seccion 3 de las instrucciones sobre seguir la tabla Q en caso de discrepancia.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-026-01 | Crear y editar un articulo de ayuda en borrador | Equipo de contenido del producto (proveedor) | 3 | R1 | 19 | - |
| HU-026-02 | Enviar o reenviar un articulo de ayuda a revision legal | Equipo de contenido del producto (proveedor) | 2 | R1 | 19 | HU-026-01 |
| HU-026-03 | Revisar legalmente un articulo y aprobarlo o rechazarlo | Equipo de contenido del producto (proveedor) | 5 | R1 | 20 | HU-026-02 |
| HU-026-04 | Vincular un articulo publicado a los campos y pantallas del sistema | Equipo de contenido del producto (proveedor) | 3 | R1 | 20 | HU-026-03 |
| HU-026-05 | Mostrar la tarjeta de ayuda contextual de 4 partes | Usuario de consulta / Colaborador | 5 | R1 | 20 | HU-026-04 |
| HU-026-06 | Consultar el Glosario buscable basico | Administrador de la organizacion | 3 | R1 | 20 | HU-026-03 |
| HU-026-07 | Mostrar el descargo estandar en cada articulo y en el Glosario | Usuario de consulta / Colaborador | 1 | R1 | 20 | HU-026-05, HU-026-06 |
| HU-026-08 | Consultar el historial de version y de revision legal de un articulo | Auditor (interno) | 3 | R1 | 20 | HU-026-03 |
| HU-026-09 | Marcar manualmente un articulo publicado para revision | Equipo de contenido del producto (proveedor) | 5 | R1 | 20 | HU-026-03, MOD-024 |
| HU-026-10 | Archivar un articulo marcado para revision cuyo concepto ya no aplica | Equipo de contenido del producto (proveedor) | 2 | R1 | 20 | HU-026-09 |

## Historias

### HU-026-01. Crear y editar un articulo de ayuda en borrador

**Como** Equipo de contenido del producto (proveedor), **quiero** crear y editar un articulo de ayuda con sus 4 textos (que es, por que tengo que hacer esto, fundamento y cuando necesito ayuda juridica), su modulo asociado y sus demas datos, mientras trabajo en el en estado borrador, **para** dejar preparado el contenido que despues pasara por revision legal antes de publicarse.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 19 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el equipo de contenido del producto crea un articulo nuevo, cuando completa Modulo asociado, Titulo del concepto, Tipo de contenido y los 4 textos obligatorios (Que es, Por que tengo que hacer esto, Fundamento, Cuando necesito ayuda juridica), entonces el sistema guarda el HelpArticle en estado BORRADOR con un Codigo del articulo unico y Version 1, y registra el evento de auditoria articulo creado con autor y fecha.
2. Dado un Codigo del articulo que ya existe en el catalogo, cuando el equipo de contenido intenta guardarlo, entonces el sistema rechaza el guardado y exige un codigo distinto.
3. Dado que el texto Fundamento cita un articulo de una norma, cuando se intenta guardar sin completar Fuente primaria citada, entonces el sistema exige completarla antes de guardar.
4. Dado un articulo que cita una de las 17 obligaciones afectadas por la reforma 659, cuando se guarda, entonces el campo Regimen aplicable es obligatorio y debe ser ACTUAL, FUTURO o Ambos regimenes.
5. Dado el campo Nivel de audiencia sugerido, cuando el equipo de contenido lo deja vacio, entonces el sistema permite guardar igual, porque es un metadato opcional y nunca una condicion obligatoria de navegacion.
6. Dado un adjunto ilustrativo, cuando se sube una imagen, entonces el sistema muestra la advertencia de que debe ser generica y sin datos personales reales, sin bloquear automaticamente el archivo.
7. Dado un articulo en estado PUBLICADO o MARCADO_PARA_REVISION, cuando el equipo de contenido edita sus textos, entonces el articulo publicado vigente no cambia para los usuarios de la organizacion cliente hasta que la nueva version complete de nuevo el ciclo de revision legal y se publique.

**Reglas de negocio**

- El Codigo del articulo es unico en todo el catalogo (ficha, seccion D).
- El Nivel de audiencia sugerido es un metadato opcional de filtrado, nunca una condicion obligatoria de navegacion (ficha, secciones D y P; anti-feature 24).
- La Fuente primaria citada es obligatoria cuando el Fundamento cita un articulo de una norma (ficha, seccion D).
- Ningun HelpArticle contiene datos personales de los titulares ni del personal de la empresa cliente; el adjunto ilustrativo es siempre generico (ficha, seccion D, minimizacion de datos personales).
- MOD-026 no precarga ningun campo desde el Diagnostico de la empresa (MOD-004): el contenido es generico y anterior a la existencia de cualquier organizacion cliente (ficha, seccion D).

**Fuera de alcance**

- Escribir el texto final de cada articulo del catalogo D.1 (contenido, ver requiere_contenido)
- Enviar el articulo a revision legal (HU-026-02)
- Sugerencia automatica de coincidencia por palabras clave entre un campo y un articulo, mas alla de guardar Palabras clave o sinonimos como dato del articulo (HU-026-04 exige siempre confirmacion humana)

- Requiere contenido: Catalogo inicial de 3 a 6 articulos de ayuda por cada uno de los modulos MUST HAVE (ver tabla D.1 de la ficha, con los titulos ya propuestos para MOD-001 a MOD-026), con sus 4 textos redactados por el equipo de contenido; Confirmacion o ajuste de los titulos de catalogo de MOD-020, MOD-023 y MOD-024 en la tabla D.1, que la propia ficha marca pendientes de confirmar cuando esas fichas completen su seccion R (nota final 3 de la ficha)
- Preguntas pendientes relacionadas: PP-OPS-04
- Referencia: MOD-026_ficha.md, secciones D y D.1, y tabla F (fila inicio, transicion a BORRADOR)
- Notas: Se fijan 3 puntos porque, pese al numero de campos, la HU no incluye flujo de estados propio (aterriza siempre en BORRADOR); la validacion de completitud total se exige recien al enviar a revision legal (HU-026-02), siguiendo la propia tabla F de la ficha.

### HU-026-02. Enviar o reenviar un articulo de ayuda a revision legal

**Como** Equipo de contenido del producto (proveedor), **quiero** enviar un articulo en borrador, o reenviar uno marcado para revision ya actualizado, al revisor legal asignado, **para** que ningun texto de ayuda llegue a los usuarios sin haber pasado antes por una revision juridica.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 19 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-026-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un articulo en estado BORRADOR con los 4 textos obligatorios, Modulo asociado, Tipo de contenido y Fundamento completos, cuando el equipo de contenido lo envia a revision legal, entonces el sistema cambia su estado a EN_REVISION_LEGAL y notifica al revisor legal asignado.
2. Dado un articulo en estado BORRADOR con al menos un campo obligatorio de la seccion D incompleto, cuando el equipo de contenido intenta enviarlo a revision legal, entonces el sistema rechaza el envio y senala el campo o los campos faltantes.
3. Dado un articulo en estado MARCADO_PARA_REVISION que el equipo de contenido ya actualizo, cuando lo reenvia, entonces el sistema lo pasa de nuevo a EN_REVISION_LEGAL, con el mismo requisito de campos completos que un envio inicial.
4. Dado un articulo en estado PUBLICADO, EN_REVISION_LEGAL u OBSOLETO_ARCHIVADO, cuando el equipo de contenido intenta enviarlo directamente a revision legal, entonces el sistema no ofrece esa accion, porque solo BORRADOR y MARCADO_PARA_REVISION pueden transitar a EN_REVISION_LEGAL.
5. Dado el envio a revision legal, cuando se completa, entonces el sistema registra el evento de auditoria envio a revision legal con autor, fecha y version de trabajo.

**Reglas de negocio**

- Solo BORRADOR y MARCADO_PARA_REVISION pueden transitar a EN_REVISION_LEGAL (ficha, seccion F).
- El envio exige que los campos obligatorios de la seccion D esten completos, incluido el Fundamento (ficha, seccion F).
- El reenvio desde MARCADO_PARA_REVISION pasa de nuevo por revision legal completa, igual que la primera revision (ficha, seccion F).

**Fuera de alcance**

- Revision legal en si, aprobar o rechazar (HU-026-03)

- Preguntas pendientes relacionadas: PP-OPS-04
- Referencia: MOD-026_ficha.md, seccion F (tabla de transiciones, filas BORRADOR a EN_REVISION_LEGAL y MARCADO_PARA_REVISION a EN_REVISION_LEGAL)

### HU-026-03. Revisar legalmente un articulo y aprobarlo o rechazarlo

**Como** Equipo de contenido del producto (proveedor), **quiero** revisar legalmente un articulo enviado a revision y aprobarlo para publicarlo, o rechazarlo con observaciones para que se corrija, **para** asegurar que ningun articulo se publique sin que una persona distinta de quien lo redacto confirme que el texto y su cita legal son correctos.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 20 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-026-02
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un articulo en estado EN_REVISION_LEGAL, cuando el revisor legal confirma el texto, la cita legal y, si aplica, el Regimen aplicable, y aprueba, entonces el sistema cambia el articulo a PUBLICADO, incrementa la Version, registra Fecha de ultima revision legal y revisor, y el articulo queda visible para los roles de la organizacion cliente segun sus permisos.
2. Dado que la persona que intenta aprobar el articulo es la misma persona registrada como autor de esa version, cuando confirma la aprobacion, entonces el sistema rechaza la accion, porque quien redacta nunca puede ser quien aprueba la revision legal de su propio texto.
3. Dado un articulo en estado EN_REVISION_LEGAL, cuando el revisor legal lo rechaza o pide cambios, entonces el sistema exige registrar observaciones y devuelve el articulo a BORRADOR, notificando al autor con esas observaciones.
4. Dado un intento de rechazar sin registrar ninguna observacion, cuando se confirma la accion, entonces el sistema exige el campo de observaciones antes de continuar.
5. Dado un articulo recien publicado, cuando el sistema completa la transicion, entonces registra el evento de auditoria articulo publicado con version anterior, version nueva, revisor y fecha.
6. Dado un articulo en un estado distinto de EN_REVISION_LEGAL, cuando alguien intenta aprobarlo o rechazarlo, entonces el sistema no ofrece esa accion.

**Reglas de negocio**

- Quien redacta un articulo nunca puede ser quien lo revisa legalmente ni quien lo publica (ficha, seccion C, doble control).
- La aprobacion incrementa la Version del articulo y registra Fecha de ultima revision legal y revisor (ficha, secciones D y F).
- El rechazo exige observaciones registradas por el revisor y devuelve el articulo a BORRADOR (ficha, seccion F).
- Solo un articulo PUBLICADO queda visible para los roles de la organizacion cliente, segun sus permisos (ficha, secciones C y F).

**Fuera de alcance**

- Boton necesito ayuda juridica con tarea sugerida (SHOULD HAVE, no se construye en esta epica)
- Retroalimentacion util / no fue util (SHOULD HAVE, no se construye en esta epica)

- Requiere contenido: Confirmacion legal formal (revision y fecha) de cada uno de los articulos del catalogo inicial antes de que puedan considerarse PUBLICADOs
- Preguntas pendientes relacionadas: PP-OPS-04
- Referencia: MOD-026_ficha.md, secciones C (separacion de funciones) y F (filas EN_REVISION_LEGAL a PUBLICADO y EN_REVISION_LEGAL a BORRADOR)
- Notas: Cubre en una sola HU las dos ramas de la revision legal (aprobar y rechazar) porque comparten el mismo punto de decision humana y el mismo conjunto de datos; separarlas en dos HU habria fragmentado un unico evento de revision sin ganar independencia real.

### HU-026-04. Vincular un articulo publicado a los campos y pantallas del sistema

**Como** Equipo de contenido del producto (proveedor), **quiero** vincular un articulo de ayuda ya publicado a los campos, secciones o pasos especificos donde debe mostrarse, **para** que el icono de ayuda aparezca exactamente en la pantalla donde el usuario tiene la duda, sin asociaciones automaticas sin confirmar.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 20 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-026-03
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un HelpArticle en estado PUBLICADO, cuando el equipo de contenido lo vincula a un campo, seccion o paso especifico de un modulo del catalogo, entonces el sistema guarda esa asociacion y queda disponible para mostrarse en esa pantalla.
2. Dado un HelpArticle que no esta en estado PUBLICADO (por ejemplo BORRADOR o EN_REVISION_LEGAL), cuando el equipo de contenido intenta vincularlo a un campo, entonces el sistema rechaza la vinculacion.
3. Dado una coincidencia sugerida por palabra clave entre un campo y un articulo, cuando el sistema la propone, entonces la asociacion queda pendiente de confirmacion humana del equipo de contenido y nunca se activa por si sola.
4. Dado un mismo campo o pantalla, cuando el equipo de contenido lo vincula a mas de un HelpArticle, entonces el sistema permite mas de una asociacion por campo.
5. Dado que el equipo de contenido retira la vinculacion de un articulo a un campo, cuando confirma la accion, entonces el icono de ayuda deja de mostrarse en ese campo sin afectar al HelpArticle ni a su historial.
6. Dado cualquier alta, cambio o retiro de una vinculacion, cuando se guarda, entonces el sistema registra el evento en el historial de gobernanza de contenido con usuario, fecha y campo afectado.

**Reglas de negocio**

- Solo un HelpArticle PUBLICADO puede vincularse a un campo, seccion o paso (ficha, seccion G, automatizacion 2).
- Ninguna asociacion campo-articulo se activa de forma automatica sin confirmacion humana del equipo de contenido, aunque el sistema pueda sugerir una coincidencia por palabra clave (ficha, seccion H, decision 3).
- Un mismo campo puede tener mas de un HelpArticle vinculado.

**Fuera de alcance**

- Asociacion automatica sin confirmacion humana (ficha, seccion H, decision 3)
- Mostrar la tarjeta en pantalla (HU-026-05)

- Referencia: MOD-026_ficha.md, secciones G (automatizacion 2) y H (decision 3)

### HU-026-05. Mostrar la tarjeta de ayuda contextual de 4 partes

**Como** Usuario de consulta / Colaborador, **quiero** ver, junto al campo, seccion o paso donde tengo una duda, la tarjeta de ayuda con sus 4 partes, **para** entender el concepto en lenguaje sencillo, saber por que me lo piden, ver su fundamento y saber cuando debo buscar ayuda juridica, sin interrumpir mi trabajo para preguntarle a otra persona.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 20 | Si |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-026-04
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un campo, seccion o paso vinculado a un HelpArticle PUBLICADO, cuando el usuario abre el icono o enlace de ayuda, entonces el sistema despliega la tarjeta con las 4 partes en este orden: Que es, Por que tengo que hacer esto, Fundamento (con su Clasificacion: OBLIGATORIO, RECOMENDADO, CONDICIONAL, Buena practica o Decision de producto), y Cuando necesito ayuda juridica.
2. Dado un campo sin ningun HelpArticle PUBLICADO vinculado, cuando el usuario revisa la pantalla, entonces el sistema no muestra ningun icono de ayuda en ese campo.
3. Dado un HelpArticle vinculado que esta en estado MARCADO_PARA_REVISION, cuando el usuario abre su tarjeta, entonces el sistema sigue mostrando el contenido completo junto con una nota discreta de contenido en revision, sin ocultar el texto de golpe.
4. Dado el bloque Fundamento de la tarjeta, cuando cita un articulo de una norma, entonces muestra una referencia a la Fuente primaria citada para quien quiera leer el texto legal completo.
5. Dado el bloque Cuando necesito ayuda juridica, cuando se muestra, entonces es siempre texto informativo con una condicion concreta, sin ningun boton ni accion que cree de forma automatica una tarea de asesoria externa, capacidad que queda fuera de esta version.
6. Dado un Titular (formulario externo) que usa el Portal del Titular, cuando navega esa interfaz, entonces no tiene acceso a la tarjeta completa ni al catalogo de MOD-026, salvo los conceptos que MOD-012 embebe directamente en su propia pantalla.

**Reglas de negocio**

- La tarjeta muestra siempre las 4 partes en el mismo orden: que es, por que tengo que hacer esto, fundamento, cuando necesito ayuda juridica (ficha, secciones E y R.1).
- Un articulo MARCADO_PARA_REVISION nunca se oculta de golpe: sigue visible con una nota discreta mientras se actualiza (ficha, seccion F).
- El bloque Cuando necesito ayuda juridica es siempre texto informativo, sin boton ni tarea automatica asociada en esta version (ficha, tabla Q, fila SHOULD HAVE de automatizacion 4, excluida del encargo).
- El Titular (formulario externo) no accede a la tarjeta completa de MOD-026 fuera de los 2 conceptos que MOD-012 embebe en su propia pantalla (ficha, seccion B).

**Fuera de alcance**

- Niveles Basico, Intermedio y Especialista de navegacion (COULD HAVE, anti-feature 24)
- Boton necesito ayuda juridica con tarea sugerida en MOD-021 (SHOULD HAVE)
- Retroalimentacion util / no fue util (SHOULD HAVE)
- Los 2 conceptos que MOD-012 embebe directamente en el Portal del Titular (los construye MOD-012, no esta HU)

- Referencia: MOD-026_ficha.md, secciones E (tarjeta de ayuda contextual), G (automatizaciones 2 y 3) y R.1

### HU-026-06. Consultar el Glosario buscable basico

**Como** Administrador de la organizacion, **quiero** buscar y consultar, en una lista alfabetica, los terminos del Glosario del sistema, **para** confirmar el significado de un termino que encuentro en cualquier parte del sistema, sin tener que ir modulo por modulo.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 20 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-026-03
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado el catalogo de HelpArticle PUBLICADO de Tipo de contenido Termino de glosario, cuando cualquier rol interno con acceso al sistema abre el Glosario, entonces el sistema muestra la lista completa ordenada alfabeticamente por Titulo del concepto.
2. Dado un usuario que escribe una palabra en el buscador del Glosario, cuando la palabra coincide con el Titulo del concepto o con alguna de sus Palabras clave o sinonimos, entonces el sistema muestra el o los terminos correspondientes.
3. Dado una busqueda que no coincide con ningun termino publicado, cuando se ejecuta, entonces el sistema muestra un mensaje de sin resultados, nunca un error tecnico.
4. Dado el rol Titular (formulario externo), cuando intenta acceder al Glosario completo, entonces el sistema no le ofrece esa pantalla, porque su acceso queda limitado a los conceptos que MOD-012 embebe en el Portal del Titular.
5. Dado un termino del Glosario que el usuario selecciona de la lista, cuando lo abre, entonces el sistema le muestra la misma tarjeta de 4 partes y el mismo descargo estandar que en cualquier tarjeta contextual.
6. Dado que se publica una nueva version de un termino de glosario, cuando la publicacion se completa, entonces el Glosario se actualiza para mostrar la version vigente sin intervencion adicional del usuario.

**Reglas de negocio**

- El Glosario solo muestra HelpArticle PUBLICADO de Tipo de contenido Termino de glosario (ficha, secciones D y E).
- La busqueda usa el Titulo del concepto y las Palabras clave o sinonimos del articulo (ficha, seccion D).
- El Titular (formulario externo) no tiene acceso al Glosario completo (ficha, secciones B y C).

**Fuera de alcance**

- Exportacion del Glosario en PDF (COULD HAVE segun tabla Q)
- Busqueda unificada dentro de MOD-025 Busqueda Global (modulo COULD HAVE distinto, que indexa este contenido pero no lo construye esta epica)

- Referencia: MOD-026_ficha.md, secciones D.1, E (Glosario completo) y B (fila Administrador de la organizacion)

### HU-026-07. Mostrar el descargo estandar en cada articulo y en el Glosario

**Como** Usuario de consulta / Colaborador, **quiero** ver siempre, en cualquier articulo de ayuda o entrada del Glosario que consulto, el mismo texto de descargo estandar, **para** tener claro en todo momento que el sistema no me da asesoria legal ni me garantiza que mi empresa cumple con la ley.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 1 | R1 | 20 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-026-05, HU-026-06
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado cualquier HelpArticle PUBLICADO, cuando un usuario abre su tarjeta de ayuda o su entrada en el Glosario, entonces el sistema muestra siempre, junto al contenido, el texto de descargo estandar de la interfaz (el sistema organiza, documenta y da seguimiento a su programa de proteccion de datos; no constituye asesoria legal ni garantiza el cumplimiento de la Ley para la Proteccion de Datos Personales).
2. Dado el descargo estandar, cuando se muestra, entonces su redaccion es identica en todos los articulos y en el Glosario, mantenida como un unico texto centralizado por el equipo de contenido del producto.
3. Dado que el equipo de contenido actualiza la redaccion del descargo estandar, cuando guarda el cambio, entonces se refleja de inmediato en todos los articulos y en el Glosario, sin tener que editar cada HelpArticle de forma individual.
4. Dado cualquier rol de la organizacion cliente, cuando busca una opcion para ocultar de forma permanente el descargo estandar, entonces el sistema no ofrece esa opcion.
5. Dado un articulo en estado MARCADO_PARA_REVISION, cuando se muestra con su nota discreta de contenido en revision, entonces el descargo estandar sigue visible de la misma forma que en un articulo PUBLICADO sin marcar.

**Reglas de negocio**

- El descargo estandar reutiliza la redaccion de 04_objetivo_exacto_del_producto.md, seccion 1.3, y no un texto propio de MOD-026 (ficha, seccion P).
- Ningun rol de la organizacion cliente puede ocultar ni desactivar el descargo estandar.

**Fuera de alcance**

- Redaccion final validada por Legal del texto exacto (contenido, ver requiere_contenido)

- Requiere contenido: Redaccion final, validada por el equipo legal del proveedor, del texto exacto de descargo estandar reutilizado de 04_objetivo_exacto_del_producto.md, seccion 1.3 (banner general), para su uso especifico dentro de MOD-026
- Referencia: MOD-026_ficha.md, seccion P (riesgo 1) y 04_secciones/04_objetivo_exacto_del_producto.md, seccion 1.3

### HU-026-08. Consultar el historial de version y de revision legal de un articulo

**Como** Auditor (interno), **quiero** consultar el historial de version y de revision legal de un articulo de ayuda, **para** verificar que el contenido que vieron los usuarios en una fecha determinada era el vigente en ese momento, y que paso por revision legal antes de publicarse.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R1 | 20 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-026-03
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un HelpArticle publicado al menos una vez, cuando el Auditor (interno) o el equipo de contenido consultan su historial, entonces el sistema muestra cada version con quien la redacto, quien la reviso legalmente, la fecha y el resultado (aprobado u observaciones).
2. Dado un articulo con mas de una version publicada, cuando se consulta el historial, entonces el sistema conserva integras las versiones anteriores, sin permitir editarlas ni eliminarlas.
3. Dado un Auditor (interno), cuando consulta el historial, entonces accede en modo de solo lectura, sin ninguna opcion de aprobar, publicar ni modificar el articulo desde esa vista.
4. Dado un rol de la organizacion cliente distinto de Auditor (interno), cuando intenta abrir el historial de version y revision legal de un articulo, entonces el sistema no le ofrece esa pantalla, porque es informacion de gobernanza interna del contenido.
5. Dado un articulo que aun no salio nunca de BORRADOR, cuando se consulta su historial, entonces el sistema muestra unicamente el evento de creacion, sin ninguna version publicada todavia.

**Reglas de negocio**

- El historial de version conserva quien redacto, quien reviso legalmente, la fecha y el resultado de cada revision (ficha, seccion J).
- El rol Auditor (interno) accede siempre en modo de solo lectura (02_validacion/05_tipos_de_usuario.md, seccion 5.4).
- Ninguna version anterior se edita ni se elimina (ficha, secciones J y O).

**Fuera de alcance**

- Exportacion del Catalogo completo de articulos de ayuda en CSV o PDF (COULD HAVE segun tabla Q)

- Referencia: MOD-026_ficha.md, secciones J (historial de version) y B (fila Auditor interno)

### HU-026-09. Marcar manualmente un articulo publicado para revision

**Como** Equipo de contenido del producto (proveedor), **quiero** marcar manualmente como para revision un articulo ya publicado, cuando el equipo de contenido detecta que un cambio en el Centro Regulatorio (MOD-024) puede haberlo dejado desactualizado, **para** avisar a quien lo consulte que ese contenido esta bajo revision, sin dejarlo desaparecer de golpe mientras se actualiza.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R1 | 20 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-026-03
- Modulos requeridos: MOD-024

**Criterios de aceptacion**

1. Dado que MOD-024 cambia el valor de la bandera regimen_reforma_659 o confirma que se mantiene tras una revision, cuando el equipo de contenido del producto revisa el catalogo, entonces el sistema le permite filtrar los HelpArticle PUBLICADO cuyo campo Regimen aplicable cita una de las 17 obligaciones afectadas y ya no coincide con el valor vigente de la bandera.
2. Dado uno de esos articulos, cuando el equipo de contenido decide marcarlo, entonces registra un motivo (cambio de regimen en MOD-024 o vencimiento de revision periodica) y el sistema cambia su estado a MARCADO_PARA_REVISION.
3. Dado un articulo que no esta en estado PUBLICADO, cuando el equipo de contenido intenta marcarlo para revision, entonces el sistema no ofrece esa accion, porque solo un articulo PUBLICADO puede pasar a MARCADO_PARA_REVISION.
4. Dado un intento de marcar un articulo sin registrar el motivo, cuando se confirma la accion, entonces el sistema exige completarlo antes de continuar.
5. Dado que un articulo queda MARCADO_PARA_REVISION, cuando se completa la transicion, entonces el sistema registra el evento en el historial de gobernanza de contenido con fecha y motivo, y el articulo sigue visible para los usuarios con la nota discreta de contenido en revision.
6. Dado que este marcado es siempre una decision humana del equipo de contenido, cuando MOD-024 cambia su bandera, entonces el sistema nunca marca ningun articulo por su cuenta ni programa la marca de forma automatica, porque la sincronizacion automatica con la bandera queda fuera de esta version.

**Reglas de negocio**

- Solo un articulo PUBLICADO puede pasar a MARCADO_PARA_REVISION (ficha, seccion F).
- El marcado exige un motivo: cambio de regimen en MOD-024 o vencimiento de revision periodica (ficha, secciones F y G).
- El sistema nunca marca un articulo por su cuenta: la decision es siempre humana del equipo de contenido, por instruccion expresa del encargo (sin sincronizacion automatica con la bandera).

**Fuera de alcance**

- Deteccion y marcado automatico cuando cambia la bandera de MOD-024, sin intervencion humana (automatizacion 1 de la ficha, SHOULD HAVE, excluida por el encargo)
- Marcado automatico por sola fecha de vencimiento de revision periodica (automatizacion 6 de la ficha, misma exclusion)

- Preguntas pendientes relacionadas: PP-OPS-04
- Referencia: MOD-026_ficha.md, secciones F (fila PUBLICADO a MARCADO_PARA_REVISION) y G (automatizaciones 1 y 6)
- Notas: Sustituye a las automatizaciones 1 y 6 de la seccion G de la ficha (que las dispara de forma automatica) por una accion manual del equipo de contenido, por instruccion expresa del encargo (sin sincronizacion automatica con la bandera).

### HU-026-10. Archivar un articulo marcado para revision cuyo concepto ya no aplica

**Como** Equipo de contenido del producto (proveedor), **quiero** confirmar, con revision legal, que un articulo marcado para revision ya no aplica y archivarlo, **para** que el catalogo activo no muestre conceptos obsoletos, sin perder nunca su historial.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R1 | 20 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-026-09
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un articulo en estado MARCADO_PARA_REVISION, cuando el equipo de contenido confirma, con revision legal, que el concepto ya no aplica, entonces el sistema cambia su estado a OBSOLETO_ARCHIVADO y deja de mostrarlo en el catalogo activo y en el Glosario.
2. Dado un articulo en estado distinto de MARCADO_PARA_REVISION, cuando alguien intenta archivarlo directamente, entonces el sistema no ofrece esa accion.
3. Dado un articulo ya OBSOLETO_ARCHIVADO, cuando el equipo de contenido busca una opcion para reabrirlo bajo el mismo identificador, entonces el sistema no la ofrece, porque este estado es terminal.
4. Dado un articulo OBSOLETO_ARCHIVADO, cuando el Auditor (interno) o el equipo de contenido consultan su historial, entonces el sistema conserva integro su historial de version y de uso previo, sin eliminar ningun registro.
5. Dado que un articulo pasa a OBSOLETO_ARCHIVADO, cuando se completa la transicion, entonces el sistema registra el evento con quien lo confirmo, fecha y motivo.
6. Dado que el concepto vuelve a ser relevante mas adelante, cuando el equipo de contenido decide retomarlo, entonces debe crear un HelpArticle nuevo, sin reescribir el articulo ya archivado.

**Reglas de negocio**

- Solo un articulo MARCADO_PARA_REVISION puede pasar a OBSOLETO_ARCHIVADO, y siempre con revision legal (ficha, seccion F).
- OBSOLETO_ARCHIVADO es un estado terminal: no existe accion de reabrir un articulo archivado bajo el mismo identificador (ficha, seccion F).
- Ningun cambio de estado borra informacion: el historial completo del articulo se conserva (ficha, seccion F; principio 8 de 06_mapa_definitivo_de_modulos.md, seccion 2).

**Fuera de alcance**

- Reapertura de un articulo obsoleto bajo el mismo identificador (estado terminal, ficha seccion F)

- Preguntas pendientes relacionadas: PP-OPS-04
- Referencia: MOD-026_ficha.md, seccion F (fila MARCADO_PARA_REVISION a OBSOLETO_ARCHIVADO y nota de estados terminales)

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Tarjeta de ayuda contextual de 4 partes, vinculada a los campos y decisiones de los modulos MUST HAVE | HU-026-04, HU-026-05 |
| Catalogo inicial de articulos por modulo (3 a 6 conceptos por modulo MUST HAVE, ver seccion D.1) | HU-026-01, HU-026-02, HU-026-03 |
| Glosario buscable basico (lista alfabetica de terminos de glosario) | HU-026-06 |
| Descargo estandar visible en cada articulo | HU-026-07 |
| Versionado de cada articulo con historial de revision legal | HU-026-03, HU-026-08 |
