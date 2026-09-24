# MODULO: Centro de Ayuda

Codigo corto del modulo: MOD-026
Clasificacion global del modulo: MUST HAVE
Obligaciones que cubre: ninguna obligacion propia ni colaboradora declarada. `mapa_modulos.json` registra para MOD-026 `obligaciones_propietarias: []` y `obligaciones_colaboradoras: []`, y una busqueda directa de "MOD-026" sobre las 105 obligaciones de `matriz_obligaciones.json` no arroja ninguna coincidencia (verificado por busqueda mecanica, 0 resultados). Esto es consistente con `06_mapa_definitivo_de_modulos.md`, seccion 2, principio 5: "los modulos transversales nunca son propietarios de una obligacion de negocio... MOD-021, MOD-022, MOD-025 y MOD-026 no poseen ninguna obligacion propia". El respaldo legal de este modulo no es una obligacion con OBL-ID sino un principio rector: el Principio de Transparencia del Art. 5 lit. e) de la Ley para la Proteccion de Datos Personales (Decreto Legislativo 144), verificado contra la fuente primaria (`01_legal/fuentes/ace_decreto_144.txt`, pagina 5): "informar al titular... en forma concisa, de facil acceso y con un lenguaje claro y sencillo. Se prohibe recurrir a textos extensos, terminologias tecnicas o legales y/o letra pequena". Ese literal e) no tiene, sin embargo, un registro OBL-PRIN propio en `matriz_obligaciones.json` (que si registra OBL-PRIN-01 a 04 para los literales c, g, i y j): se trata de un principio que este modulo instrumenta de forma transversal para todos los demas, no de una obligacion que MOD-026 posea o que otro modulo le delegue como colaborador (ver Nota final, punto 3).

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (sin codigo, sin SQL, sin APIs, sin stack, sin infraestructura).

Fuentes usadas para esta ficha: `00_contexto_para_agentes.md`; `00_prompt_analisis_funcional.md` (area 34 del prompt, seccion "Areas que deben analizarse"); `00_plantilla_ficha_modulo.md`; `02_validacion/mapa_modulos.json` (entrada MOD-026 y las 25 entradas restantes, para verificar el grafo `depende_de`/`alimenta_a` y construir el catalogo D.1); `02_validacion/06_mapa_definitivo_de_modulos.md` (secciones 0, 1, 2, 3 -ficha resumida de MOD-026 y de los 25 modulos restantes-, 4, 5, 6, 6.1, 7 y 9); `01_legal/matriz_obligaciones.json` (verificacion de ausencia de MOD-026 como propietario o colaborador; clasificacion OBLIGATORIO/RECOMENDADO/CONDICIONAL reutilizada en la seccion D); `01_legal/fuentes/ace_decreto_144.txt` (Art. 5, verificacion directa del Principio de Transparencia, literal e); `02_validacion/02_validacion_de_la_idea.md` (seccion 2.3.4, fila sobre el enfoque de UX de tres niveles; seccion 2.7); `02_validacion/04_objetivo_exacto_del_producto.md` (secciones 1.2 y 1.3, limites del sistema y textos de descargo estandar); `02_validacion/05_tipos_de_usuario.md` (secciones 5.1 a 5.4, los 12 roles estandar); `02_validacion/22_anti_features.md` (items 3, 5, 6, 21 y 24 en particular); `02_validacion/lente_faltantes.md` y `lente_inconsistencias.md` (sin hallazgos especificos sobre este modulo o "Centro de Ayuda"/"HelpArticle", verificado por busqueda directa); `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md`, secciones 32 (UX, niveles Basico/Intermedio/Especialista) y 42 (Separacion entre software y asesoria juridica), tratadas como hipotesis de producto, no como decisiones; y las 24 fichas ya redactadas de `03_modulos/` (MOD-001 a MOD-019, MOD-021 a MOD-025), leidas integramente en su seccion R mediante `awk '/^## R[.]/,/^## Nota/'` y buscadas con `grep -n "MOD-026"` para relevar sus expectativas hacia este modulo (ver seccion L y Nota final). Como modelo de estilo y profundidad se leyeron completas `MOD-003_ficha.md` y `MOD-004_ficha.md`. Antes de cerrar esta ficha se volvio a listar `03_modulos/` dos veces para confirmar que fichas nuevas se incorporaran (MOD-017_ficha.md aparecio durante la redaccion y su seccion R ya quedo integrada en el catalogo D.1; MOD-020_ficha.md aparecio en el segundo listado, ya avanzada esta ficha, pero al cierre solo llegaba hasta su seccion K, sin seccion R todavia, por lo que su catalogo se derivo de su ficha resumida en `06_mapa_definitivo_de_modulos.md`, igual que MOD-023 y MOD-024).

---

## A. Proposito

- **Por que existe.** Es la instrumentacion directa del principio central del producto: el sistema debe ser usable por una persona que no es especialista en proteccion de datos, sin que eso signifique que el software decide cuestiones juridicas por ella (`00_prompt_analisis_funcional.md`, "Principio central"; documento maestro, seccion 42). MOD-026 es el modulo que concentra, en un solo lugar y con un formato repetible, la explicacion en lenguaje sencillo de cada concepto, campo y decision que el resto de los modulos le presenta al usuario, con el fundamento normativo siempre en un segundo nivel, tal como lo exige la "Regla de oro" de `00_plantilla_ficha_modulo.md`.
- **Que problema resuelve para la empresa.** Sin este modulo, cada pantalla tendria que explicar por su cuenta terminos como ARCO-POL, RAT, EIPD, base de licitud, encargado o transferencia internacional, con el riesgo de que cada modulo lo haga con una redaccion distinta, o de que el usuario abandone un formulario por no entender que le estan pidiendo. MOD-026 evita esa dispersion: es la unica fuente de verdad del texto de ayuda, aunque cada modulo decide en que pantalla y junto a que campo mostrarlo (regla de dependencia unica, ver seccion L).
- **Que obligacion cubre.** Ninguna con OBL-ID propio (ver encabezado). Su valor legal es indirecto y masivo: sostiene, para las 105 obligaciones de la matriz, el cumplimiento practico del Principio de Transparencia (Art. 5 lit. e) que ningun modulo de negocio posee en solitario porque es un principio transversal de redaccion, no una obligacion puntual con plazo o evidencia propia.
- **Que valor aporta.**
  - Operativo: reduce la dependencia de que alguien mas (un colega, un consultor, el equipo de soporte) tenga que explicar en el momento que significa un campo o un boton; la ayuda esta siempre disponible en la misma pantalla donde surge la duda.
  - Probatorio: de forma indirecta y agregada (nunca por si sola como evidencia de una obligacion, ver seccion J), deja constancia de que la organizacion tuvo acceso permanente a explicaciones y advertencias claras antes de tomar cada decision, lo que respalda el principio general de responsabilidad demostrada (OBL-PRIN-03, Art. 5 lit. i, propietario MOD-019) sin que MOD-026 sea su dueno.
  - De reduccion de riesgo: al catalogar de forma sistematica las "senales de que se necesita asesoria juridica" (ver seccion G y R) en un formato identico en los 26 modulos, reduce el riesgo de que una persona interprete por su cuenta una zona gris de la ley (por ejemplo, si un dato es sensible o si un proveedor cuenta como transferencia) sin darse cuenta de que ese es exactamente el punto donde el sistema le pide detenerse y consultar.
- **Que NO hace este modulo (limites explicitos).**
  - No brinda asesoria juridica ni emite una opinion sobre el caso concreto del usuario: los articulos de ayuda son generales, escritos antes de conocer la situacion especifica de cada empresa (anti-feature 3 de `22_anti_features.md`).
  - No sustituye al Delegado/Responsable interno, a la Responsable Legal/Compliance ni a un asesor externo: cuando el contenido no alcanza, el modulo escala la solicitud (seccion G), nunca la resuelve por su cuenta.
  - No decide ni afirma cumplimiento legal: ningun articulo de este modulo puede contener, ni directa ni indirectamente, una frase equivalente a "su empresa esta en regla" (04_objetivo_exacto_del_producto.md, seccion 1.2).
  - No escribe ni modifica registros de otros modulos: es de solo lectura sobre el resto del sistema, igual que MOD-025 (`06_mapa_definitivo_de_modulos.md`, seccion 4, regla 5).
  - No recopila ni conserva datos personales de los titulares con los que trata la empresa cliente; el unico contenido que administra es texto de referencia generico y, cuando existe, retroalimentacion agregada y anonima de uso (ver seccion D y P).
  - No compromete la navegacion del sistema a un modelo fijo de tres niveles (Basico, Intermedio, Especialista) sin haberlo validado con usuarios reales (anti-feature 24); en esta version, el nivel es una etiqueta opcional de cada articulo, no una arquitectura de navegacion obligatoria (ver seccion D, Q y P).

---

## B. Usuarios

MOD-026 esta disponible, en mayor o menor medida, para los 12 roles estandar de `02_validacion/05_tipos_de_usuario.md`, seccion 5.3, porque es una capa transversal consultada desde cualquier pantalla (`06_mapa_definitivo_de_modulos.md`, seccion 4). Ningun rol de la organizacion cliente autoriza contenido: la autoria y la aprobacion de cada `HelpArticle` son responsabilidad del equipo del producto con revision juridica (ver seccion C), siguiendo el mismo patron de gobernanza centralizada que ya usa MOD-024 para su contenido normativo.

| Rol | Como usa MOD-026 |
|---|---|
| Administrador de la organizacion | Consulta la ayuda contextual mientras configura la organizacion, usuarios y roles (MOD-001, MOD-003); es tipicamente quien mas usa el Glosario completo al inicio, antes de que el resto del equipo tenga cuentas activas. |
| Delegado de Proteccion de Datos (o Responsable interno) | Consulta los articulos vinculados a sus propias funciones (MOD-002) y a los modulos que aprueba (ARCO-POL, Incidentes); es el destinatario tipico de la tarea sugerida "evaluar necesidad de asesoria externa" (seccion G, automatizacion 4). |
| Responsable ARCO-POL / Responsable del tramite | Consulta con frecuencia los articulos de MOD-011 (prevencion, bloqueo cautelar, denegatoria motivada) durante la gestion de un expediente. |
| Responsable Legal / Compliance | Es, junto con el Delegado, quien mas usa el boton "necesito ayuda juridica" como punto de partida para decidir si el caso amerita invitar a un Asesor externo; no edita el contenido (ver seccion C). |
| Responsable de Seguridad / IT | Consulta los articulos de MOD-013 (incidentes) y MOD-015 (controles), sobre todo durante el cronometro de 72 horas, donde la rapidez para entender que se le exige importa tanto como el contenido mismo. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Es el perfil que mas depende de la ayuda contextual: consulta el significado de conceptos (dato sensible, base de licitud) al registrar un tratamiento nuevo en su area, sin conocimiento juridico previo. |
| Aprobador | Consulta la ayuda de un documento o decision antes de aprobarla, en particular el fundamento del articulo citado por el campo que esta revisando. |
| Auditor (interno) | Usa el Glosario y el reporte "Catalogo completo de articulos de ayuda" (seccion N) para verificar que el contenido mostrado al personal esta alineado con el estado vigente de la normativa, sin poder modificarlo. |
| Auditor externo (invitado) | Acceso de solo lectura al Glosario y a los articulos publicados, si la organizacion lo incluye como referencia dentro del paquete que revisa; nunca puede dejar retroalimentacion. |
| Usuario de consulta / Colaborador | Es quien mas usa la tarjeta de ayuda de 4 partes al completar una tarea puntual asignada, sin necesitar el resto del sistema. |
| Titular (formulario externo) | Acceso limitado e indirecto: solo ve, dentro del Portal del Titular (MOD-012), los dos conceptos que ese modulo embebe directamente en su propia interfaz (que es el Portal, que es el codigo de verificacion); los conceptos 3 a 5 de la seccion R de MOD-012 se muestran al personal interno "a traves de MOD-026" segun la propia ficha de MOD-012, es decir, el Titular externo nunca navega el catalogo completo de este modulo ni su Glosario. |
| Asesor externo invitado | Acceso de solo lectura, acotado al caso o modulo para el que fue invitado (por ejemplo, la ayuda de MOD-014 si revisa una EIPD), igual que su acceso al resto del sistema. |

---

## C. Permisos

MOD-026 no tiene, dentro de la organizacion cliente, ningun rol que cree o apruebe contenido: la autoria de cada `HelpArticle` es responsabilidad del equipo de contenido del producto, con revision juridica antes de publicarse, exactamente el mismo patron de gobernanza que `06_mapa_definitivo_de_modulos.md` ya establece para el contenido normativo de MOD-024 ("activable manualmente solo cuando el equipo del producto confirme..."). La tabla siguiente refleja eso explicitamente en las columnas de los 12 roles, que son consumidores de este modulo, nunca sus autores.

| Accion | Adm. | Delegado/Resp. interno | Resp. ARCO-POL | Legal/Compliance | Seg./IT | Resp. de area | Aprobador | Auditor interno | Auditor externo | Usuario consulta | Titular externo | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver (tarjeta de ayuda y Glosario) | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si | Limitado (solo los 2 conceptos embebidos en MOD-012) | Si, acotado al caso de su invitacion |
| Buscar dentro del Centro de Ayuda | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si | No | Si, acotado |
| Crear un articulo nuevo | No | No | No | No | No | No | No | No | No | No | No | No |
| Modificar un articulo publicado | No | No | No | No | No | No | No | No | No | No | No | No |
| Aprobar (publicar tras revision legal) | No | No | No | No | No | No | No | No | No | No | No | No |
| Cerrar | No aplica (este modulo no tiene expedientes propios que cerrar; ver seccion F) | | | | | | | | | | | |
| Eliminar / archivar un articulo | No | No | No | No | No | No | No | No | No | No | No | No |
| Exportar (Glosario o catalogo por modulo en PDF) | Si | Si | Si | Si | Si | Si | Si | Si | Si, solo lectura | Si | No aplica | Si, acotado |
| Asignar | No aplica (no hay articulos asignables a un responsable dentro de la organizacion cliente) | | | | | | | | | | | |
| Comentar (retroalimentacion "fue util / no fue util" + comentario opcional) | Si | Si | Si | Si | Si | Si | Si | No (para no comprometer su independencia de revision, ver `05_tipos_de_usuario.md` 5.4) | No | Si | No | Si, acotado |
| Adjuntar evidencia | No aplica (este modulo no gestiona evidencia legal; ver seccion J) | | | | | | | | | | | |

**Crear, modificar y aprobar contenido (fuera del RBAC de la organizacion cliente).** Estas tres acciones las ejecuta el equipo de contenido del producto, con separacion de funciones y doble control propios: (1) quien redacta un articulo (autor de contenido) nunca es la misma persona que (2) lo revisa juridicamente (revisor legal, interno o contratado por el proveedor) ni que (3) lo publica (responsable de contenido, quien confirma que la revision quedo completa antes de que el articulo pase a estado PUBLICADO, ver seccion F). Esta separacion es analoga, pero no identica, a la que `05_tipos_de_usuario.md` seccion 5.4 exige dentro de la organizacion cliente: aqui protege al usuario final de recibir un texto sin revisar, no protege a la empresa cliente de un fraude interno.

**Separacion de funciones dentro de la organizacion cliente.** El rol Auditor (interno) puede ver y exportar, pero nunca dejar retroalimentacion ("comentar"), para mantener su funcion de revision independiente sin mezclarla con la de usuario operativo (mismo criterio que `05_tipos_de_usuario.md`, seccion 5.4, primer punto).

---

## D. Informacion de entrada

La entidad principal de este modulo es `HelpArticle` (unica entidad que le asigna `06_mapa_definitivo_de_modulos.md`, seccion 7). Ningun campo se precarga desde el Diagnostico de la empresa (MOD-004): el contenido es generico y se define antes de que exista ninguna organizacion cliente. Dos campos si se precargan desde otros modulos transversales: "Modulo asociado" desde el catalogo de 26 modulos de `mapa_modulos.json`, y "Regimen aplicable" desde la bandera `regimen_reforma_659` de MOD-024, para los articulos vinculados a una de las 17 obligaciones afectadas por la reforma.

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda que vera el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Codigo del articulo | Texto | Obligatorio desde la creacion | No aplica (formato interno HELP-MOD0XX-NN) | Unico en todo el catalogo | No visible al usuario final; identificador interno del equipo de contenido | Buena practica |
| Modulo asociado | Referencia a otra entidad (Modulo) | Obligatorio | Catalogo cerrado de los 26 modulos de `mapa_modulos.json`, mas la opcion "Transversal / general" para conceptos que no pertenecen a un solo modulo (por ejemplo, "que es un OBL-ID") | Debe existir en el catalogo | "En que pantalla del sistema debe aparecer este texto de ayuda" | Buena practica |
| Titulo del concepto | Texto | Obligatorio | No aplica | No vacio, longitud recomendada breve | "El nombre corto que vera el usuario en el indice o en el titulo de la tarjeta" | Buena practica |
| Tipo de contenido | Seleccion unica | Obligatorio | Concepto de modulo, Termino de glosario, Senal de alerta juridica, Guia de paso a paso (onboarding o wizard), Pregunta frecuente | Debe pertenecer al catalogo | Organiza el indice y alimenta los filtros de busqueda | Buena practica |
| Nivel de audiencia sugerido | Seleccion multiple | Opcional (metadato informativo, no una puerta de navegacion obligatoria; ver seccion P) | Basico, Intermedio, Especialista | Ninguna especifica | "Le ayuda a decidir si necesita mas o menos detalle" | PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md, seccion 32 [hipotesis de producto, anti-feature 24, pendiente de validar con usuarios reales] |
| Texto "Que es" | Texto largo | Obligatorio | No aplica | Longitud maxima recomendada (evitar textos extensos, Art. 5 lit. e) | Explicacion sencilla del concepto, sin jerga legal | Buena practica; Art. 5 lit. e LPDP (Principio de Transparencia) |
| Texto "Por que tengo que hacer esto" | Texto largo | Obligatorio | No aplica | Misma longitud recomendada | Por que le importa a su empresa, no solo que dice la ley | Buena practica |
| Texto "Fundamento" | Texto largo | Obligatorio | No aplica | Debe citar un OBL-ID y articulo, o "buena practica"/"decision de producto" si no existe OBL-ID | El respaldo legal o de diseno, mostrado en segundo nivel | Regla de oro de `00_plantilla_ficha_modulo.md` |
| Clasificacion del fundamento | Seleccion unica | Obligatorio | OBLIGATORIO, RECOMENDADO, CONDICIONAL (identico a `matriz_obligaciones.json`), Buena practica, Decision de producto | Debe pertenecer al catalogo | Distingue lo que la ley exige de lo que es un consejo del producto | `matriz_obligaciones.json` |
| Texto "Cuando necesito ayuda juridica" | Texto largo | Obligatorio | No aplica | Debe describir una condicion concreta (nunca un generico "consulte siempre a un abogado", ver seccion H) | Cuando debe buscar a alguien mas antes de decidir | Buena practica |
| Fuente primaria citada | Referencia o texto | Obligatorio si el "Fundamento" cita un articulo | Catalogo de fuentes de `01_legal/fuentes/` o URL oficial (ACE, Asamblea Legislativa, Diario Oficial) | Debe existir el archivo o la URL citada | Para quien quiera leer el texto legal original completo | `00_contexto_para_agentes.md`, seccion 2 |
| Version del articulo | Numero | Obligatorio, autogenerado | No aplica | Incrementa en cada republicacion | No visible al usuario final | Buena practica |
| Estado del contenido | Seleccion unica | Obligatorio | Borrador, En revision legal, Publicado, Marcado para revision, Obsoleto/archivado | Solo "Publicado" es visible para los roles de la organizacion cliente (ver seccion F) | No aplica (campo de gobernanza interna) | Buena practica |
| Regimen aplicable (reforma 659) | Seleccion unica | Obligatorio solo si el articulo cita una de las 17 obligaciones afectadas (`matriz_obligaciones.json`, campo `afectada_por_reforma_659`) | ACTUAL, FUTURO, Ambos regimenes | Debe coincidir con el campo `afectada_por_reforma_659` del OBL-ID citado | "En que estado de la reforma aplica este texto" | `06_mapa_definitivo_de_modulos.md`, seccion 5 |
| Fecha de ultima revision legal y revisor | Fecha + texto | Obligatorio antes de publicar | No aplica | La fecha no puede ser futura | No visible al usuario final; visible al equipo de contenido y a Auditor en el reporte de la seccion N | Buena practica |
| Palabras clave o sinonimos | Lista de texto | Opcional | No aplica | Ninguna especifica | Terminos en lenguaje cotidiano que un usuario podria escribir al buscar (por ejemplo, "borrar mis datos" para Cancelacion) | Alimenta la Busqueda Global (MOD-025, ver seccion L) |
| Articulos relacionados ("ver tambien") | Referencia multiple a otro `HelpArticle` | Opcional | No aplica | Deben existir en el catalogo | Enlaces a conceptos relacionados | Buena practica |
| Adjunto ilustrativo | Archivo (imagen) | Opcional | No aplica | Formato de imagen estandar; nunca debe contener datos personales de titulares ni de empleados de la empresa cliente | Una captura de pantalla de ejemplo, generica y sin datos reales | Buena practica; privacidad por diseno |

**Minimizacion de datos personales.** `HelpArticle` no contiene, en su diseno, ningun dato personal de los titulares con los que trata la empresa cliente ni del personal de esa empresa: es contenido de referencia generico, autorizado y mantenido por el proveedor. El unico dato personal tangencial es el nombre del revisor legal (personal del propio proveedor, no del cliente) y, cuando el usuario decide dejarlo, un comentario de texto libre de retroalimentacion; ese comentario se trata como texto anonimo agregado por rol, nunca vinculado de forma expuesta a la identidad de quien lo escribio (ver seccion P, riesgo de seguridad y privacidad), siguiendo el mismo criterio de minimizacion que MOD-025 ya aplica a los terminos de busqueda que un usuario escribe.

### D.1 Catalogo inicial de articulos por modulo

Catalogo construido a partir de la seccion R (Ayuda contextual) de las fichas ya redactadas (MOD-001 a MOD-019, MOD-021 a MOD-025) y, para los modulos cuya ficha aun no llega a su seccion R (MOD-020, MOD-023, MOD-024, todas incompletas al cierre de esta ficha, ver Nota final), derivado del proposito resumido de cada uno en `06_mapa_definitivo_de_modulos.md`, seccion 3. Esta tabla solo lista los titulos de los conceptos, no reproduce su texto completo (que ya vive, palabra por palabra, en la seccion R de cada ficha de origen); MOD-026 no duplica ese contenido como fuente independiente, solo lo cataloga y lo sirve en el lugar correcto (regla de "direccion unica" entre modulos de proceso, `06_mapa_definitivo_de_modulos.md`, seccion 4, regla 7).

| Modulo | Articulos iniciales (titulos) | Fuente |
|---|---|---|
| MOD-001 Organizacion y Personas | Organizacion; Sucursal; Rol; Separacion de funciones; Usuario invitado vs usuario activo; Rol Delegado de Proteccion de Datos/Responsable interno (dentro del catalogo de roles) | Seccion R de MOD-001_ficha.md |
| MOD-002 Delegado / Responsable Interno de Datos | Delegado de Proteccion de Datos/Responsable interno; Comunicacion del nombramiento a la ACE; Reverificacion del perfil; Confidencialidad despues del cese; Doble estado (reforma 659); Declaracion jurada de conflicto de intereses | Seccion R de MOD-002_ficha.md |
| MOD-003 Onboarding | Que es la "organizacion" en este sistema; Que es el Delegado de Proteccion de Datos; Que son los roles y por que debo asignarlos desde ahora; Por que tengo que aceptar el aviso sobre lo que este sistema no hace; Que pasa despues de terminar esta configuracion inicial | Seccion R de MOD-003_ficha.md |
| MOD-004 Diagnostico de Cumplimiento | Que es el Diagnostico de Cumplimiento; Que es una exclusion del Art. 3; Que es un dato personal sensible; Que es una transferencia internacional de datos; Por que me preguntan sobre menores, biometria o videovigilancia | Seccion R de MOD-004_ficha.md |
| MOD-005 Plan de Cumplimiento | Que es el Plan de Cumplimiento; Por que las acciones tienen distinta prioridad (Critica, Importante, Recomendada); Que significa que una accion este vencida; Por que tengo que justificar si marco una accion como "No aplica"; Cuando se recalcula el plan; Que es el "Plan de adecuacion" y por que se me pide como evidencia | Seccion R de MOD-005_ficha.md |
| MOD-006 RAT y Mapa de Datos | Que es el RAT (Registro de Actividades de Tratamiento); Que es una base de licitud; Que es un dato personal sensible; Que es el Mapa de Datos; Que es el Catalogo de Sistemas; Que significa "requiere revision periodica" | Seccion R de MOD-006_ficha.md |
| MOD-007 Consentimiento | Que es el consentimiento; Revocacion del consentimiento; Datos sensibles y consentimiento reforzado; Alternativa no biometrica; Consentimiento de menores de edad (NNA); Cuando no se necesita consentimiento | Seccion R de MOD-007_ficha.md |
| MOD-008 Documentos y Politicas | Aviso de Privacidad; Politica de Privacidad; Version vigente frente a version historica; Cadena de aprobacion; Checklist del Articulo 24; Documento requiere revision | Seccion R de MOD-008_ficha.md |
| MOD-009 Proveedores y Encargados | Encargado del tratamiento; Tercero/Receptor; Subencargado; Contrato o DPA (documento de sometimiento); Evaluacion de riesgo del proveedor; Pais fuera de El Salvador y transferencia | Seccion R de MOD-009_ficha.md |
| MOD-010 Transferencias Internacionales | Que es una transferencia internacional de datos; Nivel de proteccion del pais receptor; Puesta en conocimiento a la ACE; Encargado extranjero frente a transferencia internacional; Base juridica de la transferencia | Seccion R de MOD-010_ficha.md |
| MOD-011 ARCO-POL | Que es una solicitud ARCO-POL; Que es la prevencion; Que es el bloqueo cautelar; Que es la denegatoria motivada; Que es la notificacion a receptores; Que es el reclamo ante la Agencia de Ciberseguridad del Estado (ACE) | Seccion R de MOD-011_ficha.md |
| MOD-012 Portal del Titular | Que es el Portal del Titular; Que es el codigo de verificacion (embebidos en el propio Portal); Por que se pide un documento de identidad al presentar la solicitud; Diferencia entre el Portal y el formulario interno de la empresa; Que significa que mi solicitud este "en revision" en el Portal (estos 3 ultimos se muestran al personal interno a traves de MOD-026, no al titular) | Seccion R de MOD-012_ficha.md |
| MOD-013 Incidentes de Seguridad | Vulneracion de seguridad de datos personales; Las 72 horas (dos cronometros distintos); Fecha de conocimiento; Contenido de la notificacion; Documentacion obligatoria del expediente; Operador de infraestructura critica | Seccion R de MOD-013_ficha.md |
| MOD-014 Riesgos y EIPD | Que es una EIPD (Evaluacion de Impacto en la Privacidad); Que es el nivel de riesgo; Que es el riesgo residual; Por que el sistema no decide si mi tratamiento es legal; Que es un tratamiento de alto riesgo | Seccion R de MOD-014_ficha.md |
| MOD-015 Controles de Seguridad | Que es un "control de seguridad" en este sistema; Por que debo adjuntar evidencia; Que significa que un control este "vencido"; Que pasa si un control no aplica a mi empresa; Por que este modulo no es un antivirus ni un SIEM; Que es la "infraccion grave" vinculada a estos controles | Seccion R de MOD-015_ficha.md |
| MOD-016 Retencion y Eliminacion | Que es una regla de retencion; Que es la fecha efectiva de retencion; Diferencia entre el motor de datos del titular y el motor de retencion documental; Que significa que un dato quede "retenido por obligacion"; Eliminacion segura; Por que este modulo no cambia de nombre ni de estructura con la reforma 659 | Seccion R de MOD-016_ficha.md |
| MOD-017 Capacitacion | Que es el registro minimo de capacitacion; Que es el plan anual de capacitacion e induccion, y quien debe elaborarlo; En que se diferencia esto de la capacitacion propia del Delegado; Que significa la induccion de personal nuevo; Por que este modulo no es una plataforma de cursos; Que pasa con el plan anual si la reforma a la ley entra en vigencia | Seccion R de MOD-017_ficha.md |
| MOD-018 Auditoria de Cumplimiento | Que es la "auditoria anual de cumplimiento"; Que es un "hallazgo" y en que se diferencia de un incidente de seguridad; Que significa "riesgo aceptado" en un hallazgo; En que se diferencia de esta auditoria del AuditLog; Por que este modulo no emite una certificacion de la ACE | Seccion R de MOD-018_ficha.md |
| MOD-019 Centro de Evidencias | Que es la "evidencia" y en que se diferencia de un "documento"; Que es el registro tecnico (AuditLog) y por que no es lo mismo que la evidencia de este modulo; Que es un "hueco de evidencia"; Que es un "paquete de evidencia" y por que no se puede editar despues de exportado; Por que un envio externo exige un segundo control; Que significa que una evidencia este "bloqueada" | Seccion R de MOD-019_ficha.md |
| MOD-020 Dashboard y Reportes | Que es el Dashboard; Que significa "estado del programa" (y por que nunca vera un porcentaje de cumplimiento legal); Que son los 8 clusters legales (vista alternativa a las 6 etapas); Que es una foto periodica (cierre mensual); Diferencia entre el Dashboard y un Reporte; Por que un indicador puede decir "no disponible en esta version" | Seccion R de MOD-020_ficha.md (Actualizacion 2026-09-24, fase 3: se reemplaza el catalogo provisional de 3 conceptos por los 6 titulos reales de la seccion R, ya redactada) |
| MOD-021 Centro de Tareas | Que es una tarea; Que es una aprobacion; Que significa que una tarea este vencida; Que es el motor de plazos (por que la fecha no se puede editar a mano); Que pasa cuando cambia el regimen del Delegado (reforma 659); Diferencia entre una tarea y una evidencia | Seccion R de MOD-021_ficha.md |
| MOD-022 Notificaciones | Que es una notificacion; Que es el acuse de recibo obligatorio; Que es el resumen diario o semanal; Que es el piso minimo de alertas de plazos legales; Diferencia entre un aviso interno de MOD-022 y una comunicacion formal a un titular o a la autoridad | Seccion R de MOD-022_ficha.md |
| MOD-023 Calendario y Motor de Plazos | Que es un dia habil; Que es el motor de plazos (por que el mismo servicio calcula todos los plazos del sistema); Que es un recalculo y por que una fecha limite puede cambiar; Diferencia entre un plazo frente al titular y un plazo frente a la Agencia de Ciberseguridad del Estado (ACE); Que significa que el sistema aplique un "criterio conservador" cuando la ley no es clara; Que es la vista de calendario central | Seccion R de MOD-023_ficha.md (Actualizacion 2026-09-24, fase 3: se reemplaza el catalogo provisional de 3 conceptos por los 6 titulos reales de la seccion R, ya redactada) |
| MOD-024 Centro Regulatorio | Marco normativo consultable; Actualizaciones normativas; Doble estado de la reforma 659; Procedimiento Sancionador; Multas orientativas; Tramites ante la ACE | Seccion R de MOD-024_ficha.md (Actualizacion 2026-09-24, fase 3: se reemplaza el catalogo provisional de 3 conceptos por los 6 titulos reales de la seccion R, ya redactada) |
| MOD-025 Busqueda Global | Que es la Busqueda Global; Que significa buscar "en lenguaje sencillo" (sinonimos); Por que a veces la busqueda no muestra nada, aunque el registro exista; Por que el sistema a veces no guarda el termino exacto que usted escribio; Diferencia entre la Busqueda Global y el buscador propio de cada modulo | Seccion R de MOD-025_ficha.md |
| MOD-026 Centro de Ayuda (este mismo modulo) | Ver seccion R de esta misma ficha | Seccion R de esta ficha |

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Tarjeta de ayuda contextual (4 partes) | "Que es", "Por que tengo que hacer esto", "Fundamento" y "Cuando necesito ayuda juridica" del `HelpArticle` vinculado al campo o pantalla | Panel desplegable dentro de la pantalla de origen | Cada vez que el usuario abre el icono de ayuda de un campo, seccion o paso de un wizard | El usuario que esta en esa pantalla, filtrado segun los permisos que ya tiene en el modulo de origen |
| Glosario completo | Lista alfabetica de todos los `HelpArticle` de tipo "Termino de glosario" | Pagina buscable dentro de MOD-026 | Siempre disponible; se actualiza con cada publicacion | Todos los roles internos con acceso al sistema (ver seccion C) |
| Catalogo inicial por modulo | Ver seccion D.1 | Tabla de referencia | Definido en el diseno funcional; se actualiza cuando el equipo de contenido agrega o retira articulos | Equipo de contenido del producto; Auditor, para verificar cobertura |
| Tarea sugerida "Evaluar necesidad de asesoria externa" | Referencia al caso o modulo de origen y a la senal de alerta que la disparo | Tarea en el Centro de Tareas | Cuando se cumple el disparador de la automatizacion 4 (seccion G) | MOD-021, asignada al Delegado/Responsable interno o a Responsable Legal/Compliance |
| Metrica agregada de uso y utilidad | Vistas por articulo, votos "util"/"no fue util", sin identificar a la persona individual en el reporte | Indicador de dashboard (seccion M) y reporte (seccion N) | Se recalcula periodicamente (por ejemplo, a diario) | Equipo de contenido, Gerencia, Legal/Delegado (segun el indicador, ver seccion M) |
| Evento de auditoria de contenido | Creacion, envio a revision legal, publicacion, marcado para revision, archivado de un `HelpArticle` | Evento en el registro tecnico (AuditLog) | En cada cambio de estado del articulo (seccion F) | Consultable por MOD-019 como historial tecnico interno, nunca como evidencia de una obligacion (ver seccion J) |
| Exportacion de Glosario o guia por modulo | PDF con los articulos publicados de un modulo, o el Glosario completo | PDF | Bajo demanda | Quien lo solicite, segun su permiso de exportar (seccion C) |

---

## F. Workflow

El "workflow" de este modulo no es un expediente del usuario final (MOD-026 no tiene casos propios que un usuario de la organizacion cliente abra o cierre), sino el ciclo de vida de gobernanza de contenido de cada `HelpArticle`, ejecutado por el equipo de contenido del producto con revision juridica.

```
                    +-----------+
                    | BORRADOR  |
                    +-----------+
                          |
                enviar a revision legal
                          v
              +-----------------------+
              |   EN_REVISION_LEGAL   |
              +-----------------------+
                 |                 |
             aprobar         rechazar / pedir cambios
                 v                 v
          +-----------+      +-----------+
          | PUBLICADO |      | BORRADOR  |
          +-----------+      +-----------+
                 |
      cambia el regimen (MOD-024) o
      vence la fecha de revision periodica
                 v
      +---------------------------+
      |   MARCADO_PARA_REVISION   |
      +---------------------------+
           |                      \
   se actualiza y se           se confirma que
   vuelve a publicar           el concepto ya no aplica
           v                          v
     +-----------+          +------------------------+
     | PUBLICADO |          | OBSOLETO_ARCHIVADO      |
     +-----------+          | (terminal, solo lectura, |
                             |  version conservada)     |
                             +------------------------+
```

### Tabla de transiciones

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (inicio) | Se redacta un articulo nuevo | Modulo asociado, tipo de contenido y los 4 textos obligatorios completos | BORRADOR | Autor de contenido (equipo del producto) | Evento de auditoria "articulo creado" |
| BORRADOR | Enviar a revision legal | Los campos obligatorios de la seccion D estan completos, incluido el "Fundamento" | EN_REVISION_LEGAL | Autor de contenido | Notifica al revisor legal asignado |
| EN_REVISION_LEGAL | Aprobar | El revisor confirma el texto, la cita legal y, si aplica, el regimen (ACTUAL/FUTURO/Ambos) | PUBLICADO | Revisor legal (persona distinta del autor; doble control) | La version incrementa; el articulo queda visible para los roles de la organizacion cliente segun seccion C; evento de auditoria "articulo publicado" |
| EN_REVISION_LEGAL | Rechazar o pedir cambios | Observaciones registradas por el revisor | BORRADOR | Revisor legal | Notifica al autor con las observaciones; no queda visible para ningun rol del cliente |
| PUBLICADO | Cambia la bandera `regimen_reforma_659` en MOD-024, y el articulo cita una de las 17 obligaciones afectadas; o vence la fecha de revision periodica configurada por el equipo del producto | El campo "Regimen aplicable" del articulo no coincide ya con la bandera vigente, o se cumplio el plazo de revision | MARCADO_PARA_REVISION | Automatizacion (seccion G, regla 1) | El articulo sigue visible, con una nota discreta "contenido en revision" (nunca se oculta de golpe, para no dejar a mitad de un tramite a quien lo estaba leyendo); crea tarea interna para el equipo de contenido |
| MARCADO_PARA_REVISION | Actualizar el texto y reenviar | Pasa de nuevo por revision legal completa | EN_REVISION_LEGAL | Autor de contenido | Igual que la primera revision |
| MARCADO_PARA_REVISION | Confirmar que el concepto ya no aplica | Decision humana del equipo de contenido, con revision legal | OBSOLETO_ARCHIVADO | Equipo de contenido (con revision legal) | El articulo deja de mostrarse en el catalogo activo; se conserva integro en el historial, nunca se elimina (principio 8 de `06_mapa_definitivo_de_modulos.md`, seccion 2: "ningun cambio de estado normativo borra informacion") |
| Cualquier estado PUBLICADO o MARCADO_PARA_REVISION | Un articulo acumula retroalimentacion "no fue util" por encima del umbral configurable | Umbral superado en el periodo (seccion G, regla 5) | (no cambia de estado por si solo) | Automatizacion | Genera alerta de calidad de contenido (seccion I) dirigida al equipo de contenido, sin forzar una transicion de estado |

**Estados terminales.** OBSOLETO_ARCHIVADO es terminal: no existe una accion de "reabrir" un articulo archivado bajo el mismo identificador. Si el concepto vuelve a ser relevante (por ejemplo, si la reforma 659 se revierte o se aclara de otra forma), se publica un articulo nuevo o se retoma conscientemente el anterior como un evento nuevo de creacion, sin reescribir el historico ya archivado.

**Reapertura y registros vinculados.** Los registros de uso y retroalimentacion de un articulo archivado se conservan junto con el, para que el historial de "cuantas veces se consulto este concepto mientras estuvo vigente" no se pierda; no se transfieren automaticamente a un articulo nuevo que lo reemplace.

---

## G. Automatizaciones

| # | Disparador | Condicion | Accion | Configurable por la empresa |
|---|---|---|---|---|
| 1 | MOD-024 activa el estado FUTURO de la bandera `regimen_reforma_659` (o confirma que sigue en ACTUAL tras una revision) | El articulo cita una obligacion de la lista de 17 afectadas y su campo "Regimen aplicable" ya no coincide | Marca el articulo como MARCADO_PARA_REVISION y crea una tarea interna para el equipo de contenido (seccion F) | No (gobernanza del proveedor, no de la empresa cliente) |
| 2 | Un modulo de negocio abre un campo, seccion o paso cuyo "Fundamento" cita un OBL-ID o un concepto del catalogo | Existe un `HelpArticle` PUBLICADO vinculado a ese campo, seccion o modulo | Muestra el icono o enlace de ayuda contextual junto al campo, listo para desplegar la tarjeta de 4 partes | No (mecanismo estructural del sistema, no un ajuste de la empresa) |
| 3 | El onboarding (MOD-003) llega a un paso especifico del wizard (por ejemplo, el Paso 4, Delegado) | Existe un articulo vinculado a ese paso | Muestra automaticamente el articulo contextual asociado, sin que el usuario tenga que buscarlo | No |
| 4 | El usuario hace clic explicito en "necesito ayuda juridica" de un articulo marcado como senal de alerta, o abre 3 o mas articulos de ese tipo relacionados con el mismo caso en una misma sesion | Umbral configurable por el equipo del producto | Crea la tarea sugerida "Evaluar necesidad de asesoria externa para [caso/modulo]" en MOD-021, asignada al Delegado/Responsable interno o a Responsable Legal/Compliance; nunca invita por su cuenta a un Asesor externo (esa decision y esa invitacion las ejecuta la organizacion, en el modulo del caso correspondiente) | Si, el umbral de repeticion lo ajusta el equipo del producto; no es una opcion visible para la empresa cliente en el MVP |
| 5 | Un articulo acumula votos "no fue util" por encima de un umbral en un periodo | Umbral configurable | Genera una alerta de calidad de contenido (seccion I) dirigida al equipo de contenido, sin alterar la visibilidad del articulo para los usuarios mientras tanto | No (gobernanza del proveedor) |
| 6 | Un articulo PUBLICADO alcanza su fecha de revision periodica configurada (por ejemplo, revision anual, igual que el resto del contenido normativo) | Ninguna adicional | Lo marca MARCADO_PARA_REVISION aunque no haya habido ningun cambio normativo detectado, para forzar una relectura periodica | No |

---

## H. Decisiones que NO debe automatizar

1. **Determinar si la situacion especifica de una empresa realmente requiere asesoria juridica.** El sistema solo muestra la senal generica ("Cuando necesito ayuda juridica") y, en su caso, sugiere una tarea de evaluacion (automatizacion 4); nunca concluye "usted no necesita abogado" ni "esto ya es legal". Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada." Razon: la necesidad real de asesoria depende de hechos concretos de cada empresa que ningun catalogo generico puede evaluar por si solo.
2. **Redactar o interpretar el contenido de un articulo como un dictamen vinculante sobre el caso concreto del usuario.** Los articulos son generales y se escriben antes de conocer la situacion de ninguna empresa en particular; nunca se generan ni se ajustan de forma automatica en funcion de los datos que una empresa cargo en otro modulo. Razon: seria funcionalmente indistinguible de emitir asesoria juridica personalizada, prohibido por el anti-feature 3 de `22_anti_features.md`.
3. **Vincular de forma automatica un campo o pantalla nueva a un `HelpArticle` existente sin que el equipo de contenido confirme la relacion.** Aunque el sistema puede sugerir una coincidencia por palabras clave, la asociacion definitiva "este campo muestra este articulo" siempre requiere confirmacion humana del equipo de contenido. Razon: una asociacion automatica erronea podria mostrar una ayuda que no corresponde exactamente a lo que el campo realmente pide.
4. **Tratar la retroalimentacion agregada de los usuarios ("fue util"/"no fue util") como una validacion legal del contenido.** Esa retroalimentacion es una senal de calidad de redaccion y de UX, nunca un sustituto de la revision juridica que exige la seccion F antes de publicar o de mantener un articulo vigente. Razon: la correccion legal de un texto no la determina su popularidad, sino la revision de una persona con criterio juridico.
5. **Marcar un articulo como OBSOLETO_ARCHIVADO de forma automatica a partir de un cambio normativo detectado.** El sistema puede proponer MARCADO_PARA_REVISION automaticamente (automatizacion 1), pero archivar un concepto por completo siempre exige una decision humana del equipo de contenido, con revision legal (seccion F). Razon: mismo criterio que ya aplica MOD-024 para su propia bandera de regimen, que "nunca activa FUTURO por la sola fecha de aprobacion legislativa": ningun modulo de este sistema retira contenido normativo por si solo sin confirmacion humana.

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia o repeticion | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Contenido marcado para revision por cambio de regimen o vencimiento | Automatizacion 1 o 6 (seccion G) | WARNING | Equipo de contenido del producto (fuera del RBAC de la empresa cliente) | Canal interno del proveedor | Al disparo | Si no se resuelve en 30 dias, escala al responsable de contenido senior | El articulo se actualiza y vuelve a PUBLICADO, o se archiva conscientemente |
| Sugerencia de evaluar asesoria juridica externa | Automatizacion 4 (seccion G) | INFO | Delegado / Responsable interno, o Responsable Legal/Compliance | Tarea en MOD-021 y notificacion via MOD-022 | Una vez por caso o sesion que cumple el disparador | Ninguno automatico (es una sugerencia, no una obligacion) | La tarea se marca como atendida o descartada por la persona destinataria |
| Articulo con alto volumen de retroalimentacion "no fue util" | Automatizacion 5 (seccion G) | WARNING | Equipo de contenido del producto | Canal interno del proveedor | Al superar el umbral configurable | Revision de contenido prioritaria | Se publica una nueva version del articulo con mejor redaccion |
| Solicitud de escalamiento a soporte del producto sin resolver | Usuario indica que la ayuda disponible no resolvio su duda de uso del sistema (distinto de una duda juridica) | INFO | Equipo de soporte del producto (canal comercial/postventa, fuera del alcance funcional de este analisis) | Canal de soporte del proveedor | Al disparo | Segun la politica de soporte del proveedor (fuera de esta ficha) | El equipo de soporte marca la consulta como atendida |

---

## J. Evidencia

MOD-026 **no genera evidencia** que pruebe el cumplimiento de ninguna obligacion, consistente con la propia tabla de MOD-019 (`MOD-019_ficha.md`, seccion E.1): "MOD-026 Centro de Ayuda: No genera evidencia (modulo de solo lectura). No aplica. No aplica. No aplica." Esto es intencional, no una omision: MOD-026 explica y orienta, nunca prueba por si solo que una obligacion especifica quedo atendida (esa evidencia la genera siempre el modulo dueno de la obligacion: MOD-011 para ARCO-POL, MOD-013 para incidentes, y asi sucesivamente).

Lo que este modulo si conserva, como **registro operativo de gobernanza de contenido** (distinto de la evidencia legal descrita arriba):

- **Historial de version de cada `HelpArticle`**, con quien lo redacto, quien lo reviso legalmente, en que fecha y con que resultado (aprobado o con observaciones). Sirve para que el equipo de contenido y, si lo solicita, un Auditor puedan verificar que el texto que vio un usuario en una fecha determinada era el vigente en ese momento.
- **Registro de cambios de estado del articulo** (BORRADOR, EN_REVISION_LEGAL, PUBLICADO, MARCADO_PARA_REVISION, OBSOLETO_ARCHIVADO), con fecha de cada transicion.
- **Metricas agregadas de uso y de retroalimentacion**, sin identificar a la persona individual (ver seccion P).
- **Conservacion.** Al no ser evidencia legal de una obligacion, este modulo no fija un plazo de retencion propio ligado a un OBL-ID; el historial de version de cada articulo se conserva mientras el articulo exista en el catalogo (incluido en estado OBSOLETO_ARCHIVADO, que nunca se elimina, solo deja de mostrarse activamente), siguiendo el mismo principio general de preservacion de historial que ya aplica `06_mapa_definitivo_de_modulos.md`, seccion 2, principio 8.

---

## K. Documentos asociados

- **Documentos requeridos como entrada.** Ninguno formal por parte de la organizacion cliente. El contenido se redacta a partir de las fuentes juridicas primarias (`01_legal/fuentes/`), de `matriz_obligaciones.json` y de las secciones R ya redactadas de cada ficha de modulo (ver seccion D.1).
- **Documentos generados.** Ninguno con valor legal para la empresa cliente (MOD-026 no genera avisos, politicas ni contratos). Genera unicamente material de referencia: el Glosario completo y las guias exportables por modulo (ver seccion N).
- **Plantillas que el sistema provee.**
  - Plantilla de `HelpArticle` para el equipo de contenido (los 4 campos obligatorios: Que es, Por que, Fundamento, Cuando necesito ayuda juridica), identica en estructura a la que ya exige la seccion R de `00_plantilla_ficha_modulo.md` para cada modulo. No requiere validacion de la organizacion cliente, porque no es un documento con contenido especifico de esa empresa, sino contenido de referencia generico y ya revisado legalmente antes de publicarse.
  - Plantilla de correo o aviso interno cuando un articulo relevante para una tarea en curso queda MARCADO_PARA_REVISION (variables: nombre del articulo, modulo asociado, motivo de la marca).
- **Anexos y evidencias documentales.** Capturas de pantalla ilustrativas por articulo (campo "Adjunto ilustrativo" de la seccion D), siempre genericas y sin datos reales de ninguna empresa cliente ni de sus titulares.

---

## L. Dependencias

```
   MOD-001 (roles y permisos)      MOD-002 (conceptos del Delegado)
   MOD-024 (bandera regimen_659,          |
   catalogo normativo y OBL-ID)           |
              |                           |
              v                           v
      +-------------------------------------------+
      |          MOD-026 CENTRO DE AYUDA           |
      |   (autoria y revision: equipo del producto) |
      +-------------------------------------------+
              |                    |                 \
      tarjeta de ayuda      palabras clave/        evento de auditoria
      en cada pantalla      catalogo indexable        (AuditLog)
              |                    |                 \
              v                    v                  v
   MOD-001..MOD-025          MOD-025 Busqueda      MOD-019 Centro de
   (todos los modulos          Global (indexa el     Evidencias (solo
   operativos, lectura)        contenido de MOD-026,  historial tecnico,
                                ver su propia ficha)   nunca evidencia legal)
```

- **De que modulos recibe datos.** Segun `mapa_modulos.json`, el campo `depende_de` de MOD-026 esta vacio, igual que MOD-025 (`"depende_de": []`). En la practica funcional, MOD-026 si consulta dos fuentes de referencia constante: MOD-001 (catalogo de roles y permisos, para filtrar que puede ver cada usuario, igual que ya hace MOD-025 segun su propia ficha) y MOD-024 (la bandera `regimen_reforma_659` y el catalogo de OBL-ID/articulos, para saber cuando un articulo queda MARCADO_PARA_REVISION, seccion G). Ademas, el equipo de contenido redacta cada articulo a partir del contenido ya publicado en la seccion R de las demas fichas de modulo (MOD-001 a MOD-025), sin que eso implique una dependencia de datos en tiempo de ejecucion: es una fuente editorial, no una lectura en vivo.
- **A que modulos envia datos o eventos.** El campo `alimenta_a` de MOD-026 tambien esta vacio en `mapa_modulos.json`, consistente con ser, junto con MOD-025, un modulo terminal de solo lectura (`06_mapa_definitivo_de_modulos.md`, seccion 4, regla 5): nunca crea tareas de negocio por su cuenta (la tarea de la automatizacion 4 es una sugerencia hacia MOD-021, no una escritura sobre otro modulo de negocio) y nunca modifica un registro de otro modulo. Sin embargo, tal como la propia ficha de MOD-025 ya senala para si misma en su Nota final, esta declaracion de dependencia estructural vacia es incompleta como descripcion funcional: MOD-026 es, segun la propia tabla "que aportaria si faltara" de `06_mapa_definitivo_de_modulos.md`, seccion 4 ("el usuario no especialista quedaria solo frente a terminologia juridica"), consumido por "todos los modulos operativos", y en la practica alimenta directamente a MOD-025 Busqueda Global, que indexa "el contenido del Centro de Ayuda (MOD-026)" segun la propia ficha de MOD-025 (seccion L.2), y a MOD-003, MOD-006, MOD-008, MOD-009, MOD-012, MOD-014, MOD-015, MOD-018 y MOD-019, que ya citan explicitamente a MOD-026 como su fuente de ayuda contextual en sus propias secciones L (ver Nota final, punto 2, para el detalle de esta asimetria).
- **Que catalogos comparte.** El catalogo de OBL-ID y articulos (campo "Fundamento" de la seccion D) se construye por referencia a `matriz_obligaciones.json` y al indice normativo de MOD-024, igual que ya hace MOD-025 con su propio catalogo de sinonimos; MOD-026 no mantiene una copia editable independiente de esas fuentes, solo la cita.
- **Que pasa si un modulo dependiente no existe en el MVP.** No aplica como escenario real: MOD-026 esta clasificado MUST HAVE (igual que la enorme mayoria de los modulos operativos que consume su contenido) y no depende, para poder operar de forma minima, de ningun otro modulo transversal COULD HAVE (como MOD-025): si la Busqueda Global no existe en una version del producto, MOD-026 sigue funcionando por completo a traves de sus tarjetas de ayuda contextual y su Glosario navegable, solo pierde el canal adicional de busqueda unificada.

---

## M. Dashboard

MOD-026 aporta indicadores de uso y calidad de su contenido, nunca un porcentaje de "cumplimiento legal", consistente con `04_objetivo_exacto_del_producto.md`, seccion 1.2.

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Articulos de ayuda consultados en el periodo | Conteo de aperturas de la tarjeta de ayuda o del Glosario, agregado por modulo | Sin semaforo (dato informativo de adopcion, no de riesgo) | Responsable (Administrador), Gerencia |
| Articulos marcados para revision pendientes | Conteo de `HelpArticle` en estado MARCADO_PARA_REVISION | Verde si 0; amarillo si 1 a 3; rojo si mas de 3 | Legal/Delegado, Auditor |
| Utilidad percibida del contenido | Votos "util" dividido entre el total de votos "util" + "no fue util", por cien; se muestra siempre acompanado de la aclaracion "mide la claridad del texto de ayuda, no el cumplimiento legal de su empresa" | Verde si 80% o mas; amarillo si 60 a 79%; rojo si menos de 60% | Responsable (Administrador), Gerencia |
| Casos con sugerencia de asesoria juridica en el periodo | Conteo de tareas "Evaluar necesidad de asesoria externa" creadas por la automatizacion 4 | Sin semaforo (dato informativo de riesgo acumulado, util para planificar presupuesto de asesoria) | Legal/Delegado, Gerencia |

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Catalogo completo de articulos de ayuda | Todos los `HelpArticle` publicados, con modulo asociado, version, fecha y revisor de la ultima revision legal | Por modulo, por estado, por regimen aplicable | CSV o PDF | Equipo de contenido; Auditor, para verificar que el contenido esta alineado con la version vigente de la normativa | No; per seccion J, MOD-026 no genera evidencia de una obligacion, por lo que este reporte no forma parte del paquete formal de evidencias de MOD-019, aunque puede adjuntarse como material de referencia complementario si la organizacion lo decide |
| Reporte de retroalimentacion y confusion | Articulos con mas votos "no fue util", agrupados por modulo, sin identificar usuarios individuales | Rango de fechas, modulo | CSV o PDF | Equipo de contenido del producto | No |
| Uso de la ayuda por modulo | Vistas agregadas de la tarjeta de ayuda y del Glosario, por modulo y por periodo | Rango de fechas, modulo | CSV o PDF | Gerencia, Responsable (Administrador) | No |

---

## O. Historial

Eventos que deben quedar en el historial propio del modulo (gobernanza de contenido) y, de forma tecnica, en el AuditLog transversal:

- Creacion de un `HelpArticle` (autor, fecha, modulo asociado).
- Envio a revision legal.
- Aprobacion o rechazo de la revision legal (revisor, fecha, resultado, observaciones si las hubo).
- Publicacion de una nueva version (version anterior y version nueva).
- Cambio a MARCADO_PARA_REVISION (motivo: cambio de regimen o vencimiento de revision periodica).
- Archivado a OBSOLETO_ARCHIVADO (quien lo confirmo, fecha, motivo).
- Registro agregado de vistas y de votos de retroalimentacion (sin identificar a la persona individual en el historial expuesto a roles de la organizacion cliente).
- Creacion de una tarea sugerida de evaluacion de asesoria externa (caso o modulo de origen, fecha).
- Exportacion del Glosario o de un catalogo por modulo (quien lo exporto, cuando).

Todos los eventos quedan con usuario (del equipo del producto, cuando aplique), fecha y hora, y el motivo cuando corresponda.

---

## P. Riesgos

| Riesgo | Tipo | Mitigacion de diseno |
|---|---|---|
| Un texto de ayuda mal redactado se interpreta como asesoria legal vinculante o como una garantia de cumplimiento | Legal | Estructura obligatoria de 4 partes en todo articulo, con el "Fundamento" siempre en segundo nivel y la parte "Cuando necesito ayuda juridica" siempre presente; revision legal obligatoria antes de publicar (seccion F); descargo estandar reutilizado de `04_objetivo_exacto_del_producto.md`, seccion 1.3 |
| Sobrecarga de informacion: el usuario ignora la ayuda porque hay demasiado texto, o porque no encuentra el articulo relevante | UX | Longitud maxima recomendada por parte (Art. 5 lit. e, prohibicion de textos extensos); catalogo inicial acotado a 3-6 conceptos centrales por modulo (seccion D.1), no una enciclopedia completa de la ley; palabras clave y sinonimos para que la Busqueda Global encuentre el articulo aunque el usuario no use el termino tecnico |
| El contenido queda desactualizado frente a un cambio de la reforma 659 o frente a un cambio funcional en otro modulo cuya ayuda no se actualizo al mismo tiempo | Operativo | Automatizaciones 1 y 6 (seccion G) marcan el contenido afectado para revision de forma automatica; versionado obligatorio de cada articulo (seccion D); el articulo nunca se oculta de golpe mientras esta en revision, para no dejar a un usuario a mitad de un tramite sin ninguna ayuda visible |
| Un comentario de retroalimentacion libre termina conteniendo, sin querer, datos personales de un titular o de un empleado (por ejemplo, "mi empleado con datos biometricos tuvo un problema con...") | Seguridad y privacidad | Advertencia visible junto al campo de comentario ("no incluya datos personales de terceros en este comentario"); el comentario se trata y se muestra siempre de forma agregada y anonima en los reportes (seccion N), nunca vinculado a la identidad de quien lo escribio en las vistas de los roles de la organizacion cliente, mismo criterio de minimizacion que ya aplica MOD-025 a los terminos de busqueda |
| Comprometer la navegacion del sistema a un modelo fijo de tres niveles (Basico, Intermedio, Especialista) sin haberlo validado con usuarios reales no juristas | Producto | Anti-feature 24 de `22_anti_features.md`: el campo "Nivel de audiencia sugerido" de la seccion D es un metadato opcional de filtrado, no una arquitectura de navegacion obligatoria; la experiencia completa de tres niveles con wizards propios queda diferida a V1, sujeta a pruebas de usabilidad (ver seccion Q) |

---

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Tarjeta de ayuda contextual de 4 partes, vinculada a los campos y decisiones de los modulos MUST HAVE | X | | | | Es la instrumentacion directa del principio central del producto (seccion A); sin esto, el resto del sistema ya no cumple su propio requisito de "regla de oro" de `00_plantilla_ficha_modulo.md` |
| Catalogo inicial de articulos por modulo (3 a 6 conceptos por modulo MUST HAVE, ver seccion D.1) | X | | | | Contenido minimo indispensable para que la tarjeta de ayuda tenga algo que mostrar desde el primer dia |
| Glosario buscable basico (lista alfabetica de terminos de glosario) | X | | | | Sostiene el principio de lenguaje claro de forma transversal, no solo pantalla por pantalla |
| Descargo estandar visible en cada articulo | X | | | | Requisito transversal de todo el producto (`04_objetivo_exacto_del_producto.md`, secciones 1.2 y 1.3); debe existir desde el primer articulo publicado |
| Versionado de cada articulo con historial de revision legal | X | | | | Evita que un texto sin revisar "parezca" ayuda vigente y sostiene la trazabilidad de contenido descrita en la seccion F |
| Sincronizacion automatica con la bandera de MOD-024 (marca contenido "para revision" cuando cambia el regimen) | | X | | | Mejora critica de confiabilidad del contenido, pero un primer lanzamiento podria sostenerse, de forma mas costosa, con revision periodica manual del equipo de contenido mientras se termina de construir la automatizacion |
| Boton "necesito ayuda juridica" que crea una tarea sugerida de evaluacion de asesoria externa | | X | | | Valor alto para reducir el riesgo de que una zona gris legal pase desapercibida, pero el texto de advertencia ya presente en cada tarjeta (MUST HAVE) cumple el limite minimo de no decidir por el usuario, aunque sin el empujon activo de crear la tarea |
| Retroalimentacion "fue util / no fue util" con metricas agregadas de confusion | | X | | | Mejora de calidad de contenido valiosa para detectar que esta confundiendo a los usuarios, pero el catalogo puede operar y cumplir su proposito sin ella en una primera version |
| Niveles Basico, Intermedio y Especialista con navegacion completa a tres niveles fijos | | | X | | Anti-feature 24: requiere validarse con usuarios reales antes de comprometer el diseno de navegacion; el metadato de nivel puede existir como filtro opcional sin construir la experiencia completa de tres niveles |
| Escalamiento formal integrado (formulario propio dentro de MOD-026 para invitar a un Asesor externo) | | | X | | El rol y el flujo de invitacion de un Asesor externo ya existen en los modulos de caso (por ejemplo, MOD-011, MOD-014); un atajo directo desde el Centro de Ayuda es una mejora de conveniencia, no una funcionalidad estructural nueva |
| Exportacion de Glosario y catalogo por modulo en PDF | | | X | | Util como material de referencia descargable, pero no bloquea el proposito central del modulo, que ya se cumple con la tarjeta contextual en pantalla |

**Version minima vendible del modulo.** Las cinco funcionalidades MUST HAVE de esta tabla (tarjeta de ayuda de 4 partes, catalogo inicial por modulo, glosario basico, descargo estandar y versionado con revision legal) ya constituyen, por si solas, la version minima util: garantizan que ninguna pantalla del sistema exponga a un usuario no especialista a un concepto sin explicarlo en lenguaje sencillo y sin marcar cuando esa explicacion no basta y hace falta asesoria especializada, que es exactamente el proposito que `06_mapa_definitivo_de_modulos.md` le asigna a este modulo. Las funcionalidades SHOULD HAVE y COULD HAVE mejoran la deteccion temprana de riesgo y la calidad del contenido, pero su ausencia no impide vender ni operar el modulo.

---

## R. Ayuda contextual (complemento obligatorio)

**1. Que es el Centro de Ayuda**
- Que es: es el icono o enlace de ayuda que encuentra junto a casi cualquier campo, pantalla o decision del sistema, que le explica en pocas palabras que es ese concepto, por que tiene que completarlo, en que norma se basa y cuando conviene consultar a alguien mas.
- Por que tengo que hacer esto: para que pueda usar el sistema sin tener que memorizar terminos legales de antemano ni interrumpir su trabajo para preguntarle a otra persona cada vez que aparece una palabra que no conoce.
- Fundamento: decision de producto, instrumentacion del Principio de Transparencia (Art. 5 lit. e de la Ley para la Proteccion de Datos Personales, Decreto Legislativo 144: "lenguaje claro y sencillo... se prohibe recurrir a textos extensos, terminologias tecnicas o legales"). No corresponde a una obligacion con un OBL-ID propio (ver encabezado de esta ficha).
- Cuando necesito ayuda juridica: nunca por consultar la ayuda en si misma; si el texto que lee le indica "requiere validacion de la organizacion o asesoria especializada", es momento de acudir a su Delegado, a Responsable Legal/Compliance o a un asesor externo, segun el caso.

**2. Que es el Glosario**
- Que es: la lista completa y ordenada alfabeticamente de los terminos que mas se repiten en el sistema (ARCO-POL, RAT, EIPD, responsable, encargado, subencargado, transferencia, dato sensible, base de licitud, consentimiento, vulneracion de seguridad, Delegado, Responsable interno, dias habiles, entre otros), explicados en lenguaje sencillo.
- Por que tengo que hacer esto: le sirve como punto de referencia rapido cuando encuentra un termino en cualquier parte del sistema (o en un documento que redacto con ayuda del sistema) y quiere confirmar que significa, sin tener que ir modulo por modulo.
- Fundamento: buena practica de producto, apoyada en el mismo Principio de Transparencia del Art. 5 lit. e).
- Cuando necesito ayuda juridica: si, despues de leer la definicion sencilla del Glosario, todavia no esta seguro de como aplica ese termino a su caso concreto (por ejemplo, si un dato especifico de su empresa cuenta o no como "dato sensible"), consulte al Delegado/Responsable interno o a asesoria especializada; el Glosario explica el concepto en general, no decide su caso.

**3. Que significa que un articulo este "marcado para revision"**
- Que es: es un aviso discreto que aparece sobre un texto de ayuda cuando algo cambio (por ejemplo, la reforma a la ley) y el equipo que mantiene este contenido todavia esta confirmando si el texto sigue siendo correcto tal como esta escrito.
- Por que tengo que hacer esto: para que usted sepa que ese texto en particular esta bajo revision y no deba tomarse, mientras tanto, como la ultima palabra sobre ese tema.
- Fundamento: decision de producto (gobernanza del contenido, seccion F de esta ficha); no corresponde a un articulo especifico de la ley.
- Cuando necesito ayuda juridica: si el articulo marcado para revision es central para una decision que debe tomar de forma inmediata (por ejemplo, sobre la figura del Delegado mientras la reforma 659 sigue sin publicarse), consulte directamente con su asesoria legal en vez de esperar a que el contenido termine de actualizarse.

**4. Por que este modulo no me da asesoria legal**
- Que es: los textos de este Centro de Ayuda son generales, escritos de antemano para cualquier empresa, sin conocer los detalles concretos de la suya; nunca son una respuesta personalizada a su situacion.
- Por que tengo que hacer esto: para que usted distinga con claridad entre "el sistema me explico el concepto" y "un profesional evaluo mi caso especifico y me dio una recomendacion"; son dos cosas distintas, y solo la segunda es asesoria legal.
- Fundamento: `04_objetivo_exacto_del_producto.md`, secciones 1.2 y 1.3 (limites del sistema); anti-feature 3 de `22_anti_features.md` ("sustituir al abogado ni emitir dictamenes juridicos vinculantes").
- Cuando necesito ayuda juridica: siempre que el texto de ayuda le indique explicitamente "requiere validacion de la organizacion o asesoria especializada", o siempre que su situacion concreta no coincida exactamente con el ejemplo generico que el articulo describe.

**5. Que es el boton "necesito ayuda juridica"**
- Que es: un boton que puede usar cuando la explicacion disponible no le resuelve la duda, y que crea una tarea para que el Delegado/Responsable interno o Responsable Legal/Compliance de su empresa evalue si conviene consultar a un asesor externo.
- Por que tengo que hacer esto: para que su duda quede registrada y asignada a alguien con la autoridad y el criterio para decidir el siguiente paso, en vez de quedar sin resolver o de que usted mismo tenga que decidir, sin apoyo, si el tema amerita un abogado.
- Fundamento: decision de producto, coherente con el anti-feature 21 de `22_anti_features.md` (el sistema no se convierte en un servicio de asesoria externa integrado; solo facilita que la organizacion decida invitar a uno, si lo necesita).
- Cuando necesito ayuda juridica: es precisamente lo que este boton le ayuda a activar; una vez creada la tarea, la decision de invitar o no a un Asesor externo la toma la persona responsable dentro de su empresa, no el sistema.

---

## Nota final del agente (desacuerdos y observaciones sobre las fuentes de diseno)

1. **El Principio de Transparencia (Art. 5 lit. e) no tiene un registro OBL-PRIN propio en `matriz_obligaciones.json`.** La matriz registra OBL-PRIN-01 (lit. c, consentimiento y finalidad), OBL-PRIN-02 (lit. g, licitud), OBL-PRIN-03 (lit. i, responsabilidad demostrada) y OBL-PRIN-04 (lit. j, interes superior de NNA), pero ningun OBL-PRIN cubre expresamente el literal e (transparencia y lenguaje claro), verificado por busqueda directa contra la fuente primaria (`01_legal/fuentes/ace_decreto_144.txt`). Esta ficha no inventa un OBL-ID para llenar ese vacio, porque la instruccion del encargo prohibe expresamente inventar obligaciones; en su lugar, cita el articulo directamente como principio rector transversal, sin asignarle un OBL-ID. Se deja esta observacion para quien mantenga `matriz_obligaciones.json`: podria valorarse si el literal e merece su propio registro de principio (con clasificacion RECOMENDADO o similar) en una siguiente iteracion del corpus juridico, dado que es precisamente el fundamento legal mas citado por esta ficha y, de forma implicita, por la seccion R de las 24 fichas de modulo ya redactadas.
2. **La asimetria del campo `alimenta_a` vacio de MOD-026 en `mapa_modulos.json` merece la misma precision que MOD-025 ya se hizo a si misma.** El JSON declara correctamente que MOD-026 no tiene una dependencia estructural de construccion hacia ningun otro modulo (ningun modulo necesita que MOD-026 exista para poder operar en su forma minima, coherente con que el propio catalogo de ayuda pueda crecer de forma incremental). Sin embargo, como descripcion funcional completa, MOD-026 si es consumido activamente por practicamente todos los modulos operativos: MOD-003, MOD-006, MOD-008, MOD-009, MOD-012, MOD-014, MOD-015, MOD-018 y MOD-019 ya lo citan explicitamente en sus propias secciones L o R como su fuente de ayuda contextual (ver seccion L de esta ficha), y MOD-025 lo indexa como contenido de busqueda. Esta ficha no propone cambiar `mapa_modulos.json` (seria incorrecto declarar alli una dependencia estructural de construccion que no existe), pero dejar esta nota junto a la que ya dejo MOD-025 sobre si misma ayuda a que una futura revision de `mapa_modulos.json` documente esta misma distincion (dependencia de datos por consumo frente a dependencia estructural de construccion) tambien para los transversales de solo lectura MOD-025 y MOD-026, con el mismo criterio que la seccion 6.1 del mapa definitivo ya aplica para MOD-001, MOD-023 y MOD-024.
3. **MOD-020_ficha.md, MOD-023_ficha.md y MOD-024_ficha.md existen pero terminan de forma incompleta**, sin llegar a su seccion R. Al cierre de esta ficha: MOD-020 llega hasta la seccion K, MOD-023 hasta la seccion K y MOD-024 hasta la seccion L. La carpeta `03_modulos/` se volvio a listar dos veces durante la redaccion de esta ficha (MOD-017_ficha.md aparecio en el primer listado adicional y su seccion R ya quedo integrada en el catalogo D.1; MOD-020_ficha.md aparecio en el segundo listado, ya incompleta como se describe aqui). Para los tres modulos sin seccion R todavia, esta ficha deriva un catalogo minimo de 3 conceptos directamente del proposito resumido de cada uno en `06_mapa_definitivo_de_modulos.md`, seccion 3, y deja marcado expresamente en la tabla D.1 que ese catalogo queda "pendiente de confirmar" cuando esas fichas incorporen su seccion R completa. No se trata de una contradiccion con el mapa ni con esas fichas, sino de una limitacion factual del estado del repositorio al momento de escribir esta ficha (2026-09-24, con otros agentes del mismo workflow redactando esas fichas en paralelo); se recomienda revisar el catalogo de MOD-020, MOD-023 y MOD-024 en esta misma ficha (seccion D.1) tan pronto esas tres fichas incorporen su seccion R completa.
4. **Ningun rol de la organizacion cliente (los 12 roles estandar de `05_tipos_de_usuario.md`, seccion 5.3) crea, modifica o aprueba contenido de este modulo.** Esta ficha modela esa gobernanza como responsabilidad exclusiva del equipo de contenido del proveedor, con revision juridica y separacion de funciones internas propias (seccion C), siguiendo el mismo precedente que el propio mapa definitivo ya establece para el contenido normativo de MOD-024 ("activable manualmente solo cuando el equipo del producto confirme..."). No se trata de una desviacion del catalogo de 12 roles estandar, sino de una consecuencia directa de que MOD-026, igual que MOD-024, es contenido curado centralmente y distribuido a todas las organizaciones clientes por igual, no un registro que cada empresa redacte por si misma (a diferencia, por ejemplo, de sus propios documentos en MOD-008). Se deja esta observacion explicita porque ninguna otra ficha hasta ahora habia necesitado modelar un flujo de autoria fuera del RBAC de la empresa cliente con este nivel de detalle.
5. **La clasificacion global MUST HAVE coincide exactamente con `mapa_modulos.json` y con `06_mapa_definitivo_de_modulos.md`**, sin discrepancia: esta ficha comparte integramente la justificacion del mapa ("es la instrumentacion directa del principio central del producto") y no encontro razones, durante la investigacion de las fuentes obligatorias, para proponer una clasificacion distinta.
