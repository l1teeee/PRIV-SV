# MODULO: Busqueda Global

Codigo corto del modulo: MOD-025
Clasificacion global del modulo: COULD HAVE
Obligaciones que cubre: ninguna obligacion propia (ningun OBL-ID de `matriz_obligaciones.json` lo tiene como modulo propietario). Ninguna obligacion colaboradora tampoco: MOD-025 no aparece en el campo `modulos_candidatos` de ningun registro de la matriz (verificado por busqueda directa sobre las 105 obligaciones), consistente con el principio de diseno de que los modulos transversales de solo lectura no poseen obligaciones de negocio (`02_validacion/06_mapa_definitivo_de_modulos.md`, seccion 2, principio 5).
Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (sin codigo, sin SQL, sin APIs, sin stack, sin infraestructura).
Fuentes usadas para esta ficha: `analisis/00_contexto_para_agentes.md`, `analisis/00_prompt_analisis_funcional.md`, `analisis/00_plantilla_ficha_modulo.md`, `analisis/02_validacion/mapa_modulos.json` (entrada MOD-025), `analisis/02_validacion/06_mapa_definitivo_de_modulos.md` (secciones 2, 3, 4, 5, 6, 6.1, 7, 9), `analisis/01_legal/matriz_obligaciones.json` (verificacion de ausencia de obligaciones propias o colaboradoras), `analisis/02_validacion/05_tipos_de_usuario.md` (seccion 5.3, roles estandar), `analisis/02_validacion/22_anti_features.md` (items 1, 8, 9, 23), `analisis/02_validacion/04_objetivo_exacto_del_producto.md` (secciones 1.2 y 1.3, textos de descargo estandar), `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` (seccion 32, contexto de UX; el maestro no desarrolla busqueda global como modulo), y las fichas ya redactadas `analisis/03_modulos/MOD-021_ficha.md`, `MOD-012_ficha.md`, `MOD-006_ficha.md` y `MOD-008_ficha.md` (contrato de expectativas, ver Nota final).

---

## A. Proposito

- **Por que existe.** Es la unica caja de busqueda del sistema: permite encontrar, desde cualquier pantalla, un tratamiento, una solicitud ARCO-POL, un proveedor, un documento, un incidente, una tarea, un control, un riesgo, una evidencia o un articulo del Centro Regulatorio y del Centro de Ayuda, sin tener que saber de antemano en que modulo vive ese registro (`06_mapa_definitivo_de_modulos.md`, seccion 4, tabla "que aportaria si faltara").
- **Que problema resuelve para la empresa.** Una persona no especialista (por ejemplo Karla, del perfil pyme de `05_tipos_de_usuario.md`) no conoce la estructura de 26 modulos del sistema ni la terminologia legal exacta. Sin una busqueda global, tendria que memorizar que "cancelacion" vive en ARCO-POL y que "Art. 25" vive en Incidentes; con ella, escribe lo que recuerda en lenguaje comun y el sistema la dirige al lugar correcto.
- **Que obligacion u obligaciones cubre.** Ninguna. MOD-025 no es propietario ni colaborador de ningun OBL-ID (ver encabezado). Es una capacidad de usabilidad, no una instrumentacion de una exigencia legal especifica; por eso su clasificacion MVP es COULD HAVE y no MUST HAVE, a diferencia de los otros cinco modulos de la barra transversal (`06_mapa_definitivo_de_modulos.md`, seccion 0 y seccion 3, ficha resumida de MOD-025).
- **Que valor aporta.**
  - *Operativo*: reduce el tiempo de encontrar informacion y el numero de clics para llegar a un registro conocido (por ejemplo, retomar el expediente ARCO-POL "EXP-2026-00147" sin recordar en que pestana quedo).
  - *Probatorio*: ninguno directo; MOD-025 no genera evidencia de cumplimiento por si mismo (ver seccion J), aunque su propio registro de consultas puede usarse como evidencia de buena practica de minimizacion (seccion J).
  - *De reduccion de riesgo*: reduce el riesgo de que un usuario cree un registro duplicado (por ejemplo, un proveedor o una tarea) por no encontrar el que ya existia.
- **Que NO hace este modulo (limites explicitos).**
  - No crea, modifica, aprueba ni elimina ningun registro de otro modulo: es de solo lectura (`06_mapa_definitivo_de_modulos.md`, seccion 4, regla de conexion 5). Un resultado de busqueda siempre abre el registro en su modulo de origen para cualquier accion.
  - No decide ni interpreta nada juridicamente: no resuelve si un termino buscado corresponde a una obligacion aplicable a la empresa, solo ayuda a localizar donde esta esa informacion.
  - No expone la existencia ni el conteo de registros que el usuario que busca no tiene permiso de ver (seccion C); nunca es una via alterna para eludir los permisos definidos en el modulo de origen.
  - No es un motor de analitica ni de reportes: para eso existen MOD-020 Dashboard y Reportes (indicadores agregados) y los reportes propios de cada modulo (seccion N de cada ficha).
  - No sustituye los filtros y buscadores propios de cada modulo de negocio, que siguen existiendo y son, de hecho, el unico mecanismo de busqueda disponible mientras MOD-025 no este en el alcance vendido (ver seccion Q, cobertura parcial del MVP).
  - No es un buscador de texto libre sin control de acceso sobre expedientes de titulares (evita el riesgo que `22_anti_features.md`, item 20, senala para el canal ARCO-POL): la busqueda por nombre de una persona titular esta restringida (seccion C y seccion D).

---

## B. Usuarios

Roles estandar segun `02_validacion/05_tipos_de_usuario.md`, seccion 5.3 (los 12 roles del sistema). MOD-025 esta disponible desde cualquier pantalla para todo usuario interno autenticado; lo que cambia entre roles no es el acceso al modulo, sino que resultados puede ver cada quien (seccion C).

| Rol | Para que usa MOD-025 |
|---|---|
| Administrador de la organizacion | Encuentra rapidamente cualquier configuracion, usuario, area o registro de cualquier modulo para resolver una duda operativa o de soporte interno. |
| Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | Busca por OBL-ID o por articulo ("Art. 25") para ubicar de inmediato el modulo, el registro o el articulo del Centro Regulatorio relacionado con un caso que esta atendiendo. |
| Responsable ARCO-POL / Responsable del tramite | Busca por codigo de expediente o por nombre de titular (si su rol tiene acceso al expediente, ver seccion C) para retomar una solicitud en curso. |
| Responsable Legal / Compliance | Busca en lenguaje sencillo ("borrar mis datos", "vulneracion de seguridad") para ubicar el modulo o el articulo aplicable antes de asesorar internamente. |
| Responsable de Seguridad / IT | Busca por codigo de incidente o por nombre de un control de seguridad para verificar su estado sin recorrer el catalogo completo. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Busca un tratamiento o un documento de su area por nombre comun, sin conocer el nombre tecnico del campo en el RAT. |
| Aprobador | Busca una tarea o un documento pendiente de su aprobacion por nombre o por fecha aproximada. |
| Auditor (interno) | Busca evidencia, controles o eventos de auditoria de un tema puntual durante una revision, siempre en modo de solo lectura. |
| Auditor externo (invitado) | Busca dentro del alcance acotado que le fue habilitado para su auditoria puntual; nunca ve resultados fuera de ese alcance ni de otros clientes. |
| Usuario de consulta / Colaborador | Busca la tarea puntual que le asignaron cuando no la encuentra en su bandeja. |
| Titular (formulario externo) | No usa este modulo: el Portal del Titular (MOD-012) tiene su propio buscador acotado por codigo de expediente (ver seccion Q y `MOD-012_ficha.md`), no la busqueda global interna. |
| Asesor externo invitado | Busca, dentro del caso puntual y acotado para el que fue invitado, el expediente o documento que necesita revisar; nunca ve resultados fuera de ese caso. |

---

## C. Permisos

Convencion: "Si" = permitido por defecto; "Si*" = permitido solo dentro del alcance de visibilidad que el usuario ya tiene en el modulo de origen de cada resultado; "No" = no permitido.

| Accion | Administrador | Delegado / Resp. interno | Resp. ARCO-POL | Legal/Compliance | Seguridad/IT | Responsable de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Titular | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver (ejecutar una busqueda) | Si | Si | Si | Si | Si | Si | Si | Si | Si* (acotado a su auditoria) | Si | No (usa MOD-012) | Si* (acotado a su caso) |
| Ver resultados de tratamientos (RAT) | Si | Si | Si* | Si | Si* | Si* (solo su area) | Si* | Si | Si* | No | No | Si* |
| Ver resultados de expedientes ARCO-POL por codigo de expediente | Si | Si | Si | Si* | No | No | Si* | Si | Si* | No | No | Si* |
| Ver resultados de expedientes ARCO-POL por nombre del titular | Si | Si | Si | Si* | No | No | No | No | No | No | No | No |
| Ver resultados de incidentes de seguridad | Si | Si | Si* | Si* | Si | No | Si* | Si | Si* | No | No | Si* |
| Ver resultados de proveedores, documentos, controles, riesgos | Si | Si | Si* | Si | Si* | Si* | Si* | Si | Si* | Si* (solo lo asignado) | No | Si* |
| Ver resultados del Centro Regulatorio y del Centro de Ayuda | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si | No | Si |
| Crear, modificar o eliminar un registro desde un resultado | No (siempre redirige al modulo de origen) | No | No | No | No | No | No | No | No | No | No | No |
| Exportar un listado de resultados de busqueda | No (no existe exportacion propia; se exporta desde el modulo de origen) | No | No | No | No | No | No | No | No | No | No | No |
| Configurar sinonimos y catalogo de busqueda | Si | No | No | No | No | No | No | No | No | No | No | No |
| Consultar el registro de consultas de busqueda (seccion J) | Si* (con justificacion) | No | No | No | No | No | No | Si (solo lectura, como evidencia de minimizacion) | No | No | No | No |

**Separacion de funciones.** MOD-025 no crea, aprueba ni cierra nada, por lo que la separacion de funciones y el doble control no aplican a sus acciones propias (regla de conexion 5 de `06_mapa_definitivo_de_modulos.md`, seccion 4): toda separacion de funciones relevante ya esta resuelta en el modulo de origen del resultado (por ejemplo, quien puede ver un expediente ARCO-POL sensible se decide en MOD-011, no aqui). La unica accion que exige control especial es la exportacion o consulta del propio registro de consultas de MOD-025 (fila final de la tabla), que queda restringida al Administrador con justificacion registrada y al Auditor interno en modo de solo lectura, para que el propio mecanismo de minimizacion (seccion D.3) no se convierta en una nueva via de exposicion de datos personales.

---

## D. Informacion de entrada

MOD-025 no administra entidades de negocio propias (no aparece en la lista de entidades por modulo de `06_mapa_definitivo_de_modulos.md`, seccion 7): indexa, por referencia y en tiempo cercano al real, el contenido ya existente de los modulos de origen. Lo unico que MOD-025 recibe como entrada directa del usuario es la consulta de busqueda, y lo unico que registra de forma propia es el evento de esa consulta (seccion D.3), nunca una copia del dato original.

### D.1 Campo de consulta (lo que escribe el usuario)

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda que vera el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Termino de busqueda | Texto | Obligatorio | Libre | Minimo 2 caracteres; maximo 200 caracteres | "Escriba lo que busca: un nombre, una palabra clave (por ejemplo 'borrar mis datos'), un numero de expediente o un articulo de la ley (por ejemplo 'Art. 25')." | Buena practica (usabilidad) |
| Filtro por tipo de contenido | Seleccion multiple | Opcional | Tratamientos, Solicitudes ARCO-POL, Proveedores, Documentos, Incidentes, Tareas, Controles, Riesgos, Evidencias, Centro Regulatorio, Centro de Ayuda | Si no se marca ninguno, se busca en todos los tipos permitidos para el rol del usuario | "Marque en que partes del sistema quiere buscar, si ya sabe donde podria estar." | Buena practica |
| Filtro por rango de fechas | Fecha (rango) | Opcional | Fecha desde / fecha hasta | Fecha desde no puede ser posterior a fecha hasta | "Limite la busqueda a un periodo, si recuerda mas o menos cuando ocurrio." | Buena practica |

### D.2 Catalogo de equivalencias de busqueda (mantenido por el sistema, no por el usuario)

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda que vera el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Diccionario de sinonimos en lenguaje sencillo | Lista (par termino comun -> termino tecnico o modulo, con bandera propia "categoria sensible: si/no" por entrada, ver nota debajo de la tabla) | Obligatorio para que la busqueda en lenguaje sencillo funcione | Ejemplos minimos: "borrar mis datos" / "olvidar mis datos" -> Cancelacion u Olvido (MOD-011), categoria sensible: no; "me estan vigilando con camaras" -> Videovigilancia (MOD-006, MOD-008, MOD-014), categoria sensible: no (salvo reconocimiento facial, OBL-SENS-08); "hackeo" / "me robaron datos" / "se filtraron datos" -> Incidente de seguridad (MOD-013), categoria sensible: no; "el que me representa ante la ACE" -> Delegado de Proteccion de Datos o Responsable interno, segun el `tipo_rol` vigente en MOD-002 o la bandera `regimen_reforma_659` de MOD-024 (MOD-002), categoria sensible: no; "mi contrato con el proveedor de nube" -> Encargado, Transferencia internacional (MOD-009, MOD-010), categoria sensible: no; "tengo vih" / "mi enfermedad" -> categoria de dato de salud (MOD-006, OBL-SENS-01), categoria sensible: si | Cada entrada debe apuntar a un modulo o a un registro tipo existente; sin entradas huerfanas; toda entrada que corresponda a una categoria sensible (salud, biometria, afiliacion sindical, preferencias sexuales, origen etnico, creencias religiosas, ideologia politica, situacion moral y familiar, habitos personales, segun OBL-SENS-01) debe llevar la bandera "categoria sensible: si" | No aplica directamente al usuario (es configuracion interna), pero explica por que una busqueda en palabras simples encuentra resultados tecnicos | Buena practica (principio de lenguaje claro, Art. 5 lit. e LPDP, aplicado como buena practica de UX, no como obligacion propia de este modulo) |
| Catalogo de OBL-ID | Referencia (las 105 obligaciones de `matriz_obligaciones.json`) | Obligatorio | Todos los OBL-ID vigentes de la matriz, con su articulo y su modulo propietario | Debe existir en la matriz; se actualiza automaticamente si la matriz cambia | "Puede buscar directamente por el codigo de obligacion, por ejemplo OBL-INC-01, si ya lo conoce." | Consistencia con la regla de citar siempre el ID canonico (`00_contexto_para_agentes.md`, seccion 4) |
| Catalogo de articulos | Referencia (articulos de la LPDP, normativa ACE, lineamientos y politicas indexados por MOD-024) | Obligatorio | Por ejemplo "Art. 25", "Art. 18 inc. 2" | Debe existir en el indice normativo de MOD-024; si el articulo no existe, se muestra "no encontrado" en vez de un resultado inventado | "Puede escribir 'Art. 25' para ir directo al articulo y a los modulos que lo instrumentan." | Regla de no inventar articulos ni obligaciones (`00_contexto_para_agentes.md`, seccion 4) |
| Catalogo de codigos de expediente | Referencia (codigos de MOD-011 ARCO-POL, MOD-013 Incidentes y otros modulos con numero de caso) | Obligatorio | Formato de codigo definido por cada modulo de origen (por ejemplo el formato de expediente de MOD-011) | Debe existir el expediente exacto en el modulo de origen | "Puede escribir el numero de expediente o de caso que le dieron, tal como aparece en su comprobante." | Consistente con el campo equivalente ya definido en `MOD-012_ficha.md` (busqueda por codigo de expediente en el Portal del Titular) |

**Bandera de categoria sensible del diccionario de sinonimos.** Cada entrada del diccionario de sinonimos lleva asociado un indicador booleano "categoria sensible: si/no", mantenido por el Administrador junto con el resto del catalogo (seccion C, fila "Configurar sinonimos y catalogo de busqueda"). Esa bandera, no un analisis semantico del texto libre, es la que la seccion D.3 punto 3 usa para decidir si una consulta cae en ambito sensible por la via del catalogo de sinonimos (a diferencia del ambito sensible que se activa por el filtro de tipo de contenido, que no depende del catalogo).

### D.3 Campo generado por el sistema (registro de la consulta, no de entrada del usuario)

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda que vera el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Registro de consulta (Search Log) | Registro tecnico (ver seccion J) | Obligatorio (autogenerado en cada busqueda) | Usuario, fecha y hora, tipos de contenido filtrados, indicador booleano "ambito sensible" | Ver regla de minimizacion mas abajo | No visible como formulario; se explica en la ayuda contextual (seccion R) | Buena practica de minimizacion (privacy by design), alineada con `22_anti_features.md`, item 8 (no centralizar datos innecesarios) |

**Campos precargados desde el diagnostico, plantillas u otros modulos.** MOD-025 no precarga campos de un formulario propio: su unico "campo de entrada" real es el termino de busqueda, escrito por el usuario en el momento. Todo lo demas (resultados, catalogo de sinonimos, catalogo de OBL-ID, catalogo de articulos) proviene por referencia de otros modulos (MOD-024 para el indice normativo, cada modulo de negocio para sus propios registros).

**Que campos contienen o podrian contener datos personales, y como se minimizan.** El unico lugar donde MOD-025 podria acumular datos personales por su cuenta es el propio termino de busqueda cuando el usuario escribe, por ejemplo, el nombre de un titular. Regla de minimizacion (privacy by design, definida y justificada para este modulo):

1. **El indice de busqueda nunca copia el contenido de un registro sensible.** MOD-025 no duplica el expediente, el documento ni el dato del titular: indexa unicamente metadatos ya pensados para ser buscables (titulo, codigo, tipo, fecha, area, OBL-ID relacionado) que cada modulo de origen expone para ese fin, igual que el resto de modulos ya evita centralizar la base de datos completa del cliente (`22_anti_features.md`, items 1 y 8). Un resultado de busqueda muestra el metadato y un enlace al registro completo en su modulo de origen; nunca reproduce el contenido integro del expediente dentro de MOD-025.
2. **La busqueda por nombre de un titular esta restringida a los roles con acceso al expediente correspondiente** (seccion C): un Responsable de area sin acceso a ARCO-POL no puede localizar un expediente escribiendo el nombre de la persona, aunque ese nombre exista en el sistema; el resultado simplemente no aparece (ver regla de "no revelar existencia" mas abajo).
3. **El registro de la consulta (Search Log) no conserva el termino de busqueda cuando ese termino cae en un ambito sensible.** Se considera ambito sensible una consulta que: (a) se ejecuta con el filtro de tipo de contenido limitado a Solicitudes ARCO-POL, Incidentes o Riesgos/EIPD, o (b) el sistema detecta, por la bandera "categoria sensible" del catalogo de sinonimos (seccion D.2), que el termino corresponde a una categoria de dato sensible (salud, informacion biometrica y genetica, origen etnico, creencias religiosas, ideologia politica, afiliacion sindical, preferencias sexuales, situacion moral y familiar, habitos personales, segun OBL-SENS-01, Art. 4 lit. g, y `22_anti_features.md` item 9). En ese caso, el Search Log guarda unicamente: que hubo una busqueda, en que ambito (por ejemplo "ARCO-POL"), quien la hizo, cuando, y si obtuvo o no resultados, pero descarta el texto exacto del termino de inmediato tras procesar la consulta. Justificacion: permite auditar que existio actividad de busqueda en zonas sensibles (util si se investiga un uso indebido) sin conservar por escrito, de forma permanente, el nombre o dato personal que un usuario escribio para buscar. Para consultas fuera de ambito sensible (por ejemplo, buscar "plantilla de aviso de privacidad" o "Art. 25"), el termino si se conserva en el Search Log, porque no supone un riesgo de minimizacion.
4. **Nunca se revela la existencia ni el conteo de registros que el usuario no puede ver.** Si una busqueda coincidiria con un expediente fuera del alcance de permisos del usuario, el resultado no aparece, y el sistema no distingue entre "no existe" y "existe pero no tiene permiso": ambos casos se muestran igual (por ejemplo, "no se encontraron resultados" o, cuando hay resultados visibles de otros tipos, simplemente la ausencia de esa categoria en la lista), para no filtrar informacion por la sola forma de la respuesta.

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Lista de resultados de busqueda | Metadato de cada coincidencia (tipo, titulo, codigo, fecha, modulo de origen, fragmento de contexto) con enlace al registro completo en su modulo de origen | Lista en pantalla, agrupada por tipo de contenido | Al ejecutar una busqueda | El usuario que busco, filtrado siempre por sus permisos (seccion C) |
| Sugerencia de sinonimo aplicado | Aviso visible de que "borrar mis datos" se interpreto como "Cancelacion u Olvido" (o el equivalente que corresponda) | Nota breve sobre la lista de resultados | Cuando el termino coincide con una entrada del catalogo de sinonimos (seccion D.2) | El usuario que busco |
| Mensaje "no se encontraron resultados" | Mensaje neutro, igual para "no existe" y para "existe pero sin permiso" (regla de minimizacion, seccion D.3) | Mensaje en pantalla | Cuando ninguna coincidencia visible para ese usuario existe | El usuario que busco |
| Evento de auditoria de la consulta | Usuario, fecha y hora, tipos de contenido filtrados, indicador de ambito sensible, termino (solo si no es ambito sensible) | Registro en el AuditLog transversal (Search Log, seccion J) | En cada consulta ejecutada | MOD-019 Centro de Evidencias (lectura), Auditor interno (solo lectura, seccion C) |

MOD-025 no genera tareas, alertas de negocio, calculos de plazo, documentos ni indicadores de dashboard propios: es coherente con su caracter de modulo terminal de solo lectura (`06_mapa_definitivo_de_modulos.md`, seccion 4, regla de conexion 5), y por eso las secciones G, I, K y M de esta ficha son mas breves que las de un modulo de negocio.

---

## F. Workflow

MOD-025 no administra un ciclo de vida de expedientes con estados de negocio (Pendiente, Aprobada, Completada, etc.): su unico "workflow" es el ciclo de una consulta puntual, que siempre termina en el mismo turno de uso.

### F.1 Diagrama de estados de una consulta de busqueda

```
   +-----------+    el usuario escribe un termino    +------------+
   | INACTIVA  | ----------------------------------> | EJECUTANDO |
   +-----------+    de al menos 2 caracteres          +------------+
         ^           y confirma                            |    |
         |                                      hay >=1     |    |  ninguna coincidencia
         |                                  coincidencia    |    |  visible para el rol
         |                                  visible (v)     v    v
         |                          +----------------+    +----------------+
         |                          | CON_RESULTADOS |    | SIN_RESULTADOS |
         |                          +----------------+    +----------------+
         |                            |   ^      |             |    ^
         |    el usuario hace clic    |   |      | el usuario modifica el
         |    en un resultado         |   |      | termino o los filtros
         |    (sale de MOD-025 hacia  |   |      | (vuelve a EJECUTANDO)
         |    el modulo de origen)    |   +------+----------------------+
         |                            v                                |
         |                    (fuera del diagrama: gobernado por        |
         |                     el modulo de origen, no por MOD-025)     |
         |                                                              |
         +--------------------------------------------------------------+
           el usuario cierra la busqueda o navega a otra pantalla sin elegir
           un resultado (desde CON_RESULTADOS o desde SIN_RESULTADOS)
```

### F.2 Tabla de transiciones

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| Inactiva | El usuario escribe un termino de al menos 2 caracteres y confirma (o la busqueda incremental se activa) | Ninguna adicional | Ejecutando | Cualquier usuario interno autenticado con permiso de ver el modulo (seccion C) | Se crea el registro de consulta (seccion D.3) |
| Ejecutando | El motor de busqueda encuentra al menos una coincidencia visible para el rol del usuario | Se aplica el filtro de permisos por tipo de contenido (seccion C) antes de mostrar cualquier resultado | Con resultados | Sistema (automatico) | Se muestra la lista de resultados (seccion E); se completa el registro de auditoria de la consulta |
| Ejecutando | Ninguna coincidencia es visible para el rol del usuario (exista o no el registro para otros roles) | Regla de no revelar existencia (seccion D.3, punto 4) | Sin resultados | Sistema (automatico) | Se muestra el mensaje neutro "no se encontraron resultados"; se completa igual el registro de auditoria de la consulta |
| Con resultados | El usuario hace clic en un resultado | El usuario debe conservar el permiso de ver ese registro en su modulo de origen en el momento del clic | (sale de MOD-025 hacia el modulo de origen) | Usuario que busco | Ninguno adicional: la accion sobre el registro (ver, editar, aprobar) queda gobernada por los permisos de ese modulo de origen, no por MOD-025 |
| Con resultados / Sin resultados | El usuario modifica el termino o los filtros | Ninguna | Ejecutando (nueva consulta) | Usuario que busco | Se crea un nuevo registro de consulta independiente; no se sobrescribe el anterior |
| Con resultados / Sin resultados | El usuario cierra la busqueda o navega a otra pantalla sin elegir un resultado | Ninguna | Inactiva | Usuario que busco | Ninguno; el registro de consulta ya quedo escrito |

**Estados terminales, reapertura y archivado.** No aplica en el sentido de un expediente de negocio: cada consulta es un evento puntual que concluye en el mismo turno de uso (Con resultados o Sin resultados), sin reapertura posible ni necesidad de archivado, porque MOD-025 no posee un registro editable que deba conservarse mas alla del propio Search Log (seccion J). Los registros a los que la busqueda apunta siguen su propio ciclo de vida en su modulo de origen, sin relacion con el estado de la consulta que los encontro.

---

## G. Automatizaciones

Todas las reglas siguientes son configurables por la organizacion salvo que se indique lo contrario.

| Disparador | Condicion | Accion |
|---|---|---|
| El usuario escribe un termino que coincide con una entrada del catalogo de sinonimos (seccion D.2) | El termino esta mapeado (por ejemplo "borrar mis datos") | Traducir la busqueda al termino tecnico o al modulo correspondiente (Cancelacion u Olvido, MOD-011) y mostrar el sinonimo aplicado como nota visible |
| El termino coincide con el formato de un OBL-ID o de un articulo ("Art. NN") | El OBL-ID o el articulo existe en la matriz o en el indice normativo de MOD-024 | Mostrar como primer resultado la ficha de esa obligacion o ese articulo, con el modulo propietario, antes que otras coincidencias de texto libre |
| El termino coincide con el formato de un codigo de expediente | El codigo existe en el modulo de origen correspondiente | Mostrar ese expediente como resultado directo, sujeto siempre al filtro de permisos de la seccion C |
| Se ejecuta cualquier consulta | No aplica | Registrar el evento de consulta en el Search Log (seccion D.3 y J); no configurable, es la base de la regla de minimizacion |
| La consulta cae en ambito sensible (filtro ARCO-POL, Incidentes, Riesgos/EIPD, o el sinonimo indica categoria sensible) | Ver definicion de ambito sensible en seccion D.3, punto 3 | Descartar el termino exacto del Search Log tras procesar la consulta, conservando solo el ambito, el resultado booleano y los metadatos de quien y cuando; no configurable, es una regla de privacidad por diseno |
| Un modulo de origen publica, cierra o archiva un registro indexable | El registro tiene contenido indexable segun su propio catalogo (por ejemplo, un documento publicado en MOD-008, una tarea creada en MOD-021) | Actualizar el indice de MOD-025 con el metadato correspondiente; MOD-025 nunca escribe de vuelta al modulo de origen (regla de conexion 5 y 6 de `06_mapa_definitivo_de_modulos.md`, seccion 4) |
| Un registro se elimina o archiva en su modulo de origen | El modulo de origen marca el registro como archivado, "no aplica" o eliminado | Retirar o marcar como archivado el metadato correspondiente en el indice de MOD-025, para no mostrar como resultado activo algo que ya no existe en su origen |

---

## H. Decisiones que NO debe automatizar

- **Decidir por si mismo que un resultado es "el correcto" cuando el termino es ambiguo entre varios modulos** (por ejemplo, "retencion" podria referirse a MOD-016 Retencion y Eliminacion o a un concepto distinto dentro de otro modulo). Texto de advertencia: "Revise los resultados agrupados por tipo; el sistema no elige por usted cual es el que necesita." Razon: elegir el resultado relevante para la tarea que la persona tiene en mente es una decision del usuario, no algo que el sistema pueda inferir de forma confiable sin contexto adicional.
- **Ampliar automaticamente el acceso de un usuario para mostrarle un resultado que su rol no deberia ver**, aunque el termino buscado sea muy especifico y parezca indicar que "ya sabe" del caso. Texto de advertencia: (no aplica advertencia visible; el resultado simplemente no aparece, siguiendo la regla de no revelar existencia de la seccion D.3). Razon: los permisos del modulo de origen son la unica fuente de verdad sobre quien puede ver que; MOD-025 nunca debe convertirse en un atajo que eluda esa regla.
- **Decidir si un termino de busqueda "es" un dato personal sensible con certeza absoluta para aplicar la regla de minimizacion de la seccion D.3.** El sistema aplica una regla objetiva y configurable (filtro de tipo de contenido mas catalogo de sinonimos), no un analisis semantico exhaustivo del texto escrito. Texto de advertencia: (no aplica advertencia visible al usuario final; nota para quien configure el catalogo) "El catalogo de sinonimos que activa la minimizacion debe revisarse periodicamente por una persona responsable; el sistema no garantiza detectar toda posible categoria sensible que un usuario podria escribir en lenguaje libre." Razon: es una regla tecnica de privacidad por diseno con un limite conocido (no interpreta lenguaje libre de forma perfecta), y ese limite debe quedar explicito para quien mantiene el catalogo.
- **Interpretar automaticamente el resultado de una busqueda como una conclusion sobre el estado de cumplimiento de la empresa** (por ejemplo, "no aparecen incidentes, entonces la empresa esta al dia"). Texto de advertencia: "Esta busqueda solo localiza registros existentes; no es una medicion del estado de su programa de proteccion de datos. Consulte el Dashboard (MOD-020) para ese indicador." Razon: ausencia de resultados no equivale a ausencia de riesgo ni a cumplimiento, y afirmar lo contrario violaria el principio de no declarar cumplimiento legal (`22_anti_features.md`, item 5).

---

## I. Alertas

No aplica: MOD-025 no genera alertas de negocio ni notificaciones propias hacia ningun usuario ni hacia ningun otro modulo. Esto es consistente con tres reglas ya establecidas en las fuentes de diseno: la regla de conexion 5 de `06_mapa_definitivo_de_modulos.md`, seccion 4 ("MOD-025 Busqueda Global... son de solo lectura sobre el resto de modulos: no generan tareas ni escriben en otras entidades, solo indexan o explican"); la regla de conexion 2 de la misma seccion ("MOD-022 Notificaciones solo reacciona a eventos que le entregan MOD-021 y MOD-023; ningun modulo de recorrido envia notificaciones por su cuenta"), que excluye a MOD-025 como fuente directa de eventos hacia MOD-022; y la seccion L.2 de esta misma ficha, que declara que "MOD-025 nunca crea tareas, nunca dispara notificaciones de negocio y nunca modifica un registro de otro modulo". `MOD-022_ficha.md` (linea 359) confirma esta misma lectura al declarar a MOD-025, junto con MOD-022 y MOD-026, como "un modulo terminal de lectura" cuya unica salida es hacia el destinatario resuelto, nunca hacia otro modulo.

La senal de volumen inusual de consultas en ambito sensible, que una version anterior de esta ficha modelaba de forma incorrecta como una alerta con notificacion al Administrador y escalamiento al Auditor interno, se traslada integramente al indicador de dashboard de solo lectura de la seccion M ("Volumen de consultas en ambito sensible por usuario"). El Administrador revisa ese indicador por iniciativa propia, desde el Dashboard, sin que MOD-025 dispare ningun evento, tarea ni notificacion: el mecanismo queda asi alineado con la regla de conexion 5 en vez de contradecirla.

---

## J. Evidencia

- **Registro de consulta (Search Log), embebido en el AuditLog transversal** (la misma entidad transversal declarada en `06_mapa_definitivo_de_modulos.md`, seccion 7, "embebida en todos los modulos"): cada consulta deja un evento con usuario, fecha y hora, tipos de contenido filtrados, indicador de ambito sensible, y el termino exacto solo cuando la consulta no cae en ambito sensible (regla de minimizacion, seccion D.3).
- **Que obligacion prueba esta evidencia.** Ninguna obligacion de la matriz (MOD-025 no tiene obligaciones propias ni colaboradoras). El Search Log no se presenta como evidencia de cumplimiento ante la ACE ni se incluye en un paquete de evidencias de auditoria por defecto; su unico proposito es servir de respaldo interno de buena practica de minimizacion de datos y, si fuera necesario, de rastro para investigar un uso indebido del buscador (ver indicador de volumen inusual de la seccion M).
- **Historial inmutable.** Igual que el resto de eventos del AuditLog transversal, el Search Log no se edita ni se borra por un usuario; solo el Administrador puede consultarlo agregando una justificacion (seccion C), y el Auditor interno puede consultarlo en modo de solo lectura como evidencia de que la regla de minimizacion efectivamente opera.
- **Cuanto tiempo se conserva.** El Search Log sigue la regla general de conservacion de eventos tecnicos de auditoria que define MOD-016 Retencion y Eliminacion para el AuditLog transversal (no una regla propia de MOD-025); mientras MOD-016 no fije un plazo especifico para este tipo de evento tecnico, se aplica por defecto un periodo corto (propuesta inicial: 90 dias) dado que su valor es principalmente operativo (detectar un patron de uso inusual reciente), no probatorio de una obligacion legal especifica. [opinion de producto, sin obligacion legal que fije este plazo]

---

## K. Documentos asociados

- **Documentos requeridos como entrada.** Ninguno. MOD-025 no exige ningun documento para funcionar; todo documento que aparece como resultado (por ejemplo, una version de un Aviso de Privacidad en MOD-008) es propiedad de su modulo de origen.
- **Documentos generados.** Ninguno. MOD-025 no genera documentos, borradores ni resoluciones; su unica salida es la lista de resultados en pantalla (seccion E), que no se exporta ni se archiva como documento propio.
- **Plantillas que el sistema provee.** No aplica: MOD-025 no tiene plantillas de documento. Lo unico configurable es el catalogo de sinonimos (seccion D.2), que no es una plantilla sino una tabla de equivalencias de busqueda mantenida por el Administrador.
- **Anexos y evidencias documentales.** No aplica: MOD-025 no adjunta ni conserva archivos; cualquier archivo que un resultado referencie (por ejemplo, un adjunto de una tarea) vive y se descarga desde su modulo de origen.

---

## L. Dependencias

### L.1 Diagrama

```
   Todos los modulos con contenido indexable (MOD-002, MOD-004 a MOD-020)
   escriben metadatos hacia el indice, MOD-025 nunca escribe hacia ellos
                              |
                              v
                    +-------------------+
                    |  MOD-025 BUSQUEDA |
                    |      GLOBAL       |
                    +-------------------+
                       ^             |
                       |             | filtra siempre por permisos
        consulta el indice           | del modulo de origen antes
        normativo y de ayuda         | de mostrar un resultado
                       |             v
             MOD-024 Regulatorio    MOD-001 Organizacion y Personas
             MOD-026 Centro de Ayuda (catalogo de roles/permisos)
```

### L.2 Lista de dependencias

- **De que modulos recibe datos.** Segun `mapa_modulos.json`, el campo `depende_de` de MOD-025 esta vacio (ver Nota final sobre esta declaracion). En la practica funcional, MOD-025 lee metadatos indexables de todos los modulos de negocio y transversales mencionados explicitamente en el enunciado de esta ficha: tratamientos (MOD-006), solicitudes ARCO-POL (MOD-011), proveedores (MOD-009), documentos (MOD-008), incidentes (MOD-013), tareas (MOD-021), controles (MOD-015), riesgos (MOD-014), evidencias (MOD-019), contenido del Centro Regulatorio (MOD-024) y del Centro de Ayuda (MOD-026); ademas consulta a MOD-001 para resolver el catalogo de roles y permisos que filtra cada resultado (seccion C).
- **A que modulos envia datos o eventos.** Ninguno (`alimenta_a` vacio en `mapa_modulos.json`, consistente con ser un modulo terminal de solo lectura, regla de conexion 5 de la seccion 4 del mapa definitivo). MOD-025 nunca crea tareas, nunca dispara notificaciones de negocio y nunca modifica un registro de otro modulo; su unica salida hacia otro modulo transversal es el evento de auditoria de sus propias consultas, que va al AuditLog (consultado por MOD-019, seccion J).
- **Que catalogos comparte.** El catalogo de sinonimos y el catalogo de OBL-ID/articulos (seccion D.2) son propios de MOD-025, pero se construyen por referencia a `matriz_obligaciones.json` y al indice normativo de MOD-024; MOD-025 no mantiene una copia editable independiente de esas fuentes, solo una vista de busqueda sobre ellas.
- **Que ocurre si el modulo dependiente no existe en el MVP.** MOD-025 es COULD HAVE: mientras no se desarrolle, ningun otro modulo depende de el para operar (ninguna ficha existente lo declara como una dependencia estructural en su seccion L, ver Nota final), y su ausencia no bloquea ninguna obligacion legal (`06_mapa_definitivo_de_modulos.md`, seccion 3, ficha resumida de MOD-025). Si alguno de los modulos que MOD-025 indexa no existe todavia (por ejemplo, MOD-010 Transferencias Internacionales o MOD-014 Riesgos/EIPD, ambos SHOULD HAVE), la busqueda simplemente no encuentra resultados de ese tipo hasta que el modulo exista; no es un bloqueo, es una cobertura parcial del indice (ver seccion Q).

---

## M. Dashboard

MOD-025 no aporta indicadores propios al Dashboard principal (MOD-020): no mide "cumplimiento" ni "actividad legal", solo uso del buscador. Los tres indicadores siguientes son de gestion interna del producto, no del programa de proteccion de datos de la empresa, y por eso se muestran unicamente al Administrador, nunca en las vistas de Gerencia, Responsable, Legal o Auditor del dashboard principal. Ninguno de los tres dispara una notificacion: el Administrador los revisa por iniciativa propia (ver seccion I).

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Consultas ejecutadas en el periodo | Conteo de eventos del Search Log en el periodo seleccionado | Informativo, sin semaforo | Administrador |
| Proporcion de consultas sin resultados | Consultas en estado Sin resultados / total de consultas del periodo | Amarillo si supera un umbral configurable (propuesta inicial 40%), indicando que el catalogo de sinonimos podria necesitar revision | Administrador |
| Volumen de consultas en ambito sensible por usuario | Conteo de consultas en ambito sensible (ARCO-POL, Incidentes, Riesgos/EIPD) ejecutadas por un mismo usuario dentro de un periodo corto (configurable, propuesta inicial 1 hora), agrupado por usuario | Amarillo si algun usuario supera un umbral configurable (propuesta inicial 20 consultas) dentro del periodo corto, para que el Administrador decida si corresponde revisar el detalle agregado (sin termino exacto conservado, seccion D.3) | Administrador |

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Registro agregado de consultas en ambito sensible | Conteo de consultas por usuario, por ambito y por resultado (con/sin coincidencias), sin el termino exacto conservado | Rango de fechas, usuario, ambito | XLSX | Administrador, Auditor interno | No forma parte del paquete de evidencia de cumplimiento por defecto; puede exportarse como respaldo puntual si se investiga un uso indebido del buscador |
| Catalogo de sinonimos vigente | Lista completa de equivalencias termino comun -> termino tecnico o modulo | Ninguno | CSV | Administrador, equipo de producto | No |

---

## O. Historial

Eventos que quedan en el registro tecnico de MOD-025 (Search Log, embebido en el AuditLog transversal):

- Cada consulta ejecutada: usuario, fecha y hora, tipos de contenido filtrados, indicador de ambito sensible, resultado (con/sin coincidencias visibles).
- El termino exacto de la consulta, unicamente cuando esa consulta no cae en ambito sensible (regla de minimizacion, seccion D.3).
- Cambios al catalogo de sinonimos (quien agrego, modifico o elimino una entrada, y cuando).
- Consultas del propio Administrador o del Auditor interno al Search Log (acceso de segundo nivel, registrado igual que cualquier acceso de lectura a un registro de nivel de confidencialidad reforzado, siguiendo el mismo criterio que MOD-021 aplica a sus tareas "Sensible" o "Muy sensible").
- Revision del indicador de volumen inusual de consultas en ambito sensible por el Administrador (cuando lo consulto en el Dashboard), si el Administrador deja constancia de esa revision (seccion M).

MOD-025 no tiene historial de "cambios de campo" de un registro de negocio (no posee ese tipo de entidad), por lo que esta seccion se limita a los eventos tecnicos propios del modulo.

---

## P. Riesgos

- **Riesgo legal: que un resultado de busqueda se interprete como una conclusion sobre el estado legal de la empresa.** Por ejemplo, que la ausencia de resultados para "incidente" se lea como "no hay incidentes que reportar" cuando en realidad el incidente existe pero el usuario no tiene permiso para verlo, o el termino usado no coincide con el catalogo. *Mitigacion de diseno*: el mensaje de "sin resultados" es siempre neutro (seccion D.3, punto 4) y la ayuda contextual (seccion R) advierte explicitamente que la busqueda no es una medicion de cumplimiento (ver tambien seccion H, ultima decision no automatizable).
- **Riesgo de UX: el usuario no encuentra nada porque el catalogo de sinonimos no cubrio su forma particular de decir algo.** Por ejemplo, alguien escribe "quiero que dejen de mandarme publicidad" y el catalogo solo cubre "borrar mis datos". *Mitigacion de diseno*: el catalogo de sinonimos es revisable y ampliable por el Administrador, y el indicador de "proporcion de consultas sin resultados" (seccion M) sirve para detectar patrones de busqueda no cubiertos y priorizar que sinonimos agregar.
- **Riesgo de UX: sobrecarga de resultados irrelevantes cuando el termino es muy generico** (por ejemplo, buscar "datos"). *Mitigacion de diseno*: agrupacion de resultados por tipo de contenido (seccion E), con los resultados que coinciden con un OBL-ID, un articulo o un codigo de expediente exacto mostrados primero (seccion G), antes que coincidencias de texto libre.
- **Riesgo operativo: el indice queda desactualizado frente a un registro que ya se archivo o elimino en su modulo de origen**, mostrando un resultado que ya no existe o que cambio de estado. *Mitigacion de diseno*: la regla de actualizacion del indice (seccion G, ultima fila) retira o marca como archivado el metadato correspondiente en cuanto el modulo de origen cambia ese estado; mientras esa sincronizacion no sea instantanea, el enlace al modulo de origen siempre muestra el estado real y actual del registro, nunca una copia desactualizada de su contenido.
- **Riesgo de seguridad y privacidad: que la busqueda se convierta en un atajo para encontrar informacion de un titular sin pasar por los controles de acceso del expediente.** Por ejemplo, un Responsable de area sin acceso a ARCO-POL intenta localizar un expediente escribiendo el nombre de una persona conocida. *Mitigacion de diseno*: la restriccion de la busqueda por nombre de titular a roles con acceso al expediente (seccion C) y la regla de no revelar existencia (seccion D.3, punto 4) son controles de diseno explicitos para este riesgo especifico, y coinciden con el motivo por el cual `22_anti_features.md`, item 20, exige verificacion de identidad minima en el canal ARCO-POL: la busqueda global nunca debe ser una puerta lateral a ese mismo canal.
- **Riesgo de seguridad y privacidad: acumulacion silenciosa de datos personales dentro del propio Search Log.** Si el registro de consultas guardara siempre el termino exacto, con el tiempo el Search Log terminaria siendo una base paralela de nombres y datos de titulares, contraria al principio de minimizacion. *Mitigacion de diseno*: la regla de descarte del termino en ambito sensible (seccion D.3, punto 3) existe precisamente para evitar esta acumulacion, y el propio acceso al Search Log queda restringido y auditado (seccion C y O).

---

## Q. MVP

| Funcionalidad del modulo | Clasificacion | Justificacion |
|---|---|---|
| Filtros y buscadores propios de cada modulo de negocio (por ejemplo, filtrar tratamientos por area en MOD-006, o buscar un expediente por codigo en MOD-011 y en el Portal del Titular MOD-012) | MUST HAVE, pero como parte de la ficha de cada modulo, no de MOD-025 | Es la cobertura parcial que sustituye a la busqueda global mientras esta no exista: cada modulo de negocio ya necesita su propio filtro y su propio buscador acotado para ser usable por si solo, independientemente de si MOD-025 llega a construirse. |
| Busqueda por codigo exacto (OBL-ID, articulo, codigo de expediente) sobre un unico modulo a la vez, con enlace directo al registro | COULD HAVE (primera version de MOD-025 si se decide construirlo) | Es la version mas simple de MOD-025: no requiere el catalogo de sinonimos ni la busqueda agregada entre modulos, y ya resuelve el caso de uso mas frecuente (retomar un expediente conocido). |
| Busqueda agregada entre todos los tipos de contenido, con filtro de permisos y agrupacion por tipo | COULD HAVE | Es el valor completo de la busqueda global (encontrar sin saber en que modulo esta), pero exige que el indice cubra la mayoria de los modulos de negocio, por lo que tiene sentido despues de que esos modulos ya existan. |
| Diccionario de sinonimos en lenguaje sencillo (seccion D.2) | COULD HAVE | Mejora sustancial de usabilidad para el usuario no especialista, pero requiere mantenimiento continuo (revisar que terminos usa la gente realmente) y puede iniciarse con un catalogo minimo o crecer despues del lanzamiento del resto de la busqueda agregada. |
| Regla de minimizacion del Search Log en ambito sensible (seccion D.3, punto 3) | MUST HAVE en cuanto exista cualquier version de MOD-025 (no postergable dentro del propio modulo) | Si se construye MOD-025, aunque sea en su version minima, esta regla debe estar presente desde el primer dia: no existe una version "sin minimizacion" que sea aceptable, dado el riesgo de acumulacion de datos personales que describe la seccion P. |
| Indicador de dashboard de volumen inusual de consultas en ambito sensible (seccion M) | FUTURE | Es una mejora de monitoreo interno sobre una funcionalidad que en si misma ya es COULD HAVE; tiene sentido una vez que exista suficiente volumen de uso real del buscador para calibrar el umbral. |
| Busqueda por voz, autocompletado predictivo o busqueda semantica avanzada | FUTURE | Mejoras de experiencia sobre la misma capacidad ya cubierta por la busqueda de texto y el catalogo de sinonimos; no aportan una capacidad nueva de cumplimiento ni de usabilidad critica. |

**Version minima vendible del modulo.** Si la organizacion decide construir MOD-025 dentro del horizonte COULD HAVE, la version minima que ya aporta valor es la busqueda por codigo exacto (OBL-ID, articulo, codigo de expediente) con enlace directo al registro y con la regla de minimizacion del Search Log activa desde el primer dia. Mientras esa version no exista, el producto sigue siendo completo y vendible sin MOD-025: cada modulo de negocio resuelve su propia busqueda con sus filtros propios (fila 1 de esta tabla), que es la cobertura parcial explicita del MVP para este modulo.

---

## R. Ayuda contextual (complemento obligatorio)

**1. Que es la Busqueda Global**
- *Que es*: la caja de busqueda disponible desde cualquier pantalla del sistema, que le permite encontrar un tratamiento, una solicitud, un proveedor, un documento, un incidente, una tarea o un articulo de la ley sin tener que saber en que modulo esta.
- *Por que tengo que hacer esto*: para no perder tiempo recorriendo modulo por modulo cuando ya sabe mas o menos que esta buscando, aunque no recuerde el nombre tecnico exacto.
- *Fundamento*: no tiene un fundamento legal propio; es una funcionalidad de usabilidad (COULD HAVE en el MVP), alineada con el principio de lenguaje claro del Art. 5 lit. e LPDP, aplicado aqui como buena practica de diseno.
- *Cuando necesito ayuda juridica*: nunca por usar el buscador en si; si un resultado que encontro le genera una duda legal, esa duda se resuelve en el modulo de origen del resultado, no aqui.

**2. Que significa buscar "en lenguaje sencillo" (sinonimos)**
- *Que es*: puede escribir frases comunes, como "borrar mis datos" o "hackeo", y el sistema las traduce a los terminos tecnicos correspondientes (por ejemplo, Cancelacion u Olvido, o Incidente de seguridad).
- *Por que tengo que hacer esto*: para no obligarlo a conocer de antemano la terminologia legal exacta antes de poder buscar algo.
- *Fundamento*: buena practica de UX, coherente con el principio de lenguaje claro (Art. 5 lit. e LPDP); no es en si mismo una obligacion de la matriz.
- *Cuando necesito ayuda juridica*: si el resultado que la busqueda le mostro no coincide con lo que en realidad necesita, consulte al Delegado/Responsable interno para confirmar en cual modulo o proceso corresponde su caso.

**3. Por que a veces la busqueda no muestra nada, aunque usted sepa que el registro existe**
- *Que es*: si busca algo para lo que su rol no tiene permiso de ver (por ejemplo, el expediente ARCO-POL de otra area, o un incidente reservado a Seguridad/IT), el sistema muestra "no se encontraron resultados", sin distinguir si el registro no existe o si simplemente usted no puede verlo.
- *Por que tengo que hacer esto*: para proteger la privacidad de los titulares y la confidencialidad de los expedientes; la busqueda nunca puede ser una forma de saltarse los permisos que ya protegen esa informacion en su modulo de origen.
- *Fundamento*: buena practica de seguridad y privacidad por diseno, coherente con la restriccion de acceso minimo que ya aplican MOD-011 (ARCO-POL) y MOD-013 (Incidentes) a sus propios expedientes.
- *Cuando necesito ayuda juridica*: no aplica; si cree que deberia tener acceso a algo que no encuentra, la solicitud de acceso se resuelve con el Administrador de la organizacion, no con asesoria legal.
- *Aviso de la interfaz*: "Este buscador solo localiza registros existentes dentro de lo que su rol puede ver; no es una medicion del estado de su programa de proteccion de datos. Consulte el Dashboard (MOD-020) para ese indicador." (texto de descargo derivado del formato estandar de `04_objetivo_exacto_del_producto.md`, seccion 1.3).

**4. Por que el sistema a veces no guarda el termino exacto que usted escribio**
- *Que es*: cuando busca algo relacionado con una solicitud ARCO-POL, un incidente, un riesgo/EIPD, o una categoria de dato sensible, el sistema registra que hubo una busqueda en esa area, pero no conserva por escrito la palabra o el nombre exacto que usted tecleo.
- *Por que tengo que hacer esto*: para que el propio buscador no termine acumulando, sin necesidad, nombres de personas o datos sensibles que usted escribio solo para encontrar algo, evitando crear una base de datos paralela dentro de la busqueda.
- *Fundamento*: regla de minimizacion de datos definida para este modulo (seccion D.3, punto 3); no corresponde a un OBL-ID especifico, es una decision de privacidad por diseno.
- *Cuando necesito ayuda juridica*: no aplica directamente; si tiene dudas sobre que datos personales deberia o no escribir en cualquier campo de texto libre del sistema (incluida la busqueda), consulte la ayuda contextual del modulo donde esta trabajando.

**5. Diferencia entre la Busqueda Global y el buscador propio de cada modulo**
- *Que es*: cada modulo de negocio (por ejemplo, ARCO-POL o el RAT) tiene su propio filtro o buscador acotado a su propio contenido; la Busqueda Global, cuando este disponible, busca a la vez en todos los modulos que su rol puede ver.
- *Por que tengo que hacer esto*: mientras la Busqueda Global no forme parte de su version del sistema (es una funcionalidad COULD HAVE), siga usando el buscador propio de cada modulo: sigue siendo la forma normal y completa de encontrar informacion dentro de ese modulo.
- *Fundamento*: clasificacion MVP de este modulo (COULD HAVE, seccion Q); no existe obligacion legal que exija una busqueda agregada entre modulos.
- *Cuando necesito ayuda juridica*: no aplica.

---

## Nota final del agente (desacuerdos y observaciones sobre las fuentes de diseno)

1. **El campo `depende_de` vacio de MOD-025 en `mapa_modulos.json` es tecnicamente correcto pero puede inducir a error si se lee de forma aislada.** El JSON declara `depende_de: []` y `alimenta_a: []`, y la ficha resumida de la seccion 3 de `06_mapa_definitivo_de_modulos.md` describe esto como "entra desde ninguno... sale hacia ninguno (es un modulo terminal de lectura)". Esa declaracion es correcta en el sentido estricto de dependencia estructural de construccion (MOD-025 no necesita que ningun otro modulo exista para poder lanzarse, y ningun otro modulo necesita que MOD-025 exista para operar, coherente con su clasificacion COULD HAVE), pero es incompleta como descripcion funcional: un buscador global, por definicion, lee metadatos de practicamente todos los modulos con contenido indexable (MOD-002, MOD-004 a MOD-020, mas MOD-024 y MOD-026), tal como la propia seccion 4 del mapa definitivo reconoce en su tabla "que aportaria si faltara" ("todos los modulos con contenido indexable" lo consumirian) y como ya declaran explicitamente MOD-006 y MOD-008 en sus propias fichas ("consultado desde la capa transversal... MOD-025 (busqueda)"). Esta ficha modela esa lectura de referencia en la seccion L.2 sin proponer cambiar el campo `depende_de` de `mapa_modulos.json` (seria incorrecto declarar alli una dependencia estructural que MOD-025 no tiene para poder funcionar de forma minima), pero se recomienda que, si se revisa `mapa_modulos.json` en una siguiente iteracion, se documente esta distincion (dependencia de datos por consumo vs. dependencia estructural de construccion) tambien para MOD-025, con el mismo criterio que la seccion 6.1 del mapa definitivo ya aplica para explicar la asimetria de `alimenta_a` de MOD-001, MOD-023 y MOD-024.
2. **Correccion sobre el contrato de expectativas (ver instruccion 7 de la tarea): el `grep -n "MOD-025" analisis/03_modulos/*.md` citado en una version anterior de esta nota estaba incompleto.** Ese grep, reejecutado ahora sobre los 22 ficheros realmente existentes en `analisis/03_modulos/` (MOD-001 a MOD-016, MOD-018, MOD-019, MOD-021 a MOD-024; no existen aun MOD-017, MOD-020 ni MOD-026), encuentra cinco menciones, no dos: `MOD-006_ficha.md` linea 372 y `MOD-008_ficha.md` linea 296 (ambas en la forma "consultado desde la capa transversal... MOD-025 (busqueda)"), y tres en `MOD-022_ficha.md` (lineas 5, 359 y 361). La mencion de la linea 359 de `MOD-022_ficha.md` no es trivial: declara expresamente que "MOD-022 es, junto con MOD-025 Busqueda Global y MOD-026 Centro de Ayuda, un modulo terminal de lectura... su unica salida es hacia el destinatario resuelto... nunca hacia otro modulo". Esa expectativa es la que expuso la contradiccion, ya corregida en esta version, entre la alerta que la seccion I definia originalmente (notificacion al Administrador con escalamiento al Auditor interno) y el caracter de modulo terminal de solo lectura que esta misma ficha y el mapa definitivo (seccion 4, reglas de conexion 2 y 5) le asignan a MOD-025: ver la seccion I corregida, que ahora traslada esa senal a un indicador de dashboard (seccion M) sin notificacion ni escalamiento. Fuera de esa mencion, ninguna ficha existente exige un evento, un campo o un servicio adicional concreto de MOD-025 mas alla de consumirlo como capa transversal de solo lectura; esta ficha sigue modelando a MOD-025 como consumidor de solo lectura de metadatos indexables, sin que ningun modulo de origen deba escribir hacia el de forma especial (la actualizacion del indice es responsabilidad del propio MOD-025, seccion G).
3. **Discrepancia menor de redaccion entre el proposito de MOD-025 en `mapa_modulos.json` y en `06_mapa_definitivo_de_modulos.md`.** El JSON describe el alcance como "tratamientos, solicitudes ARCO-POL, proveedores, documentos, incidentes y tareas" (sin mencionar controles, riesgos, evidencias, Centro Regulatorio ni Centro de Ayuda), mientras que el enunciado de esta tarea y la seccion 4 del mapa definitivo (tabla "que aportaria si faltara": "todos los modulos con contenido indexable") sugieren un alcance mas amplio. Esta ficha adopta el alcance mas amplio indicado en el enunciado de la tarea (tratamientos, solicitudes ARCO-POL, proveedores, documentos, incidentes, tareas, controles, riesgos, evidencias, Centro Regulatorio y Centro de Ayuda), por ser la fuente mas especifica y mas reciente para este modulo; se recomienda actualizar el campo `proposito` de `mapa_modulos.json` para que coincida con este alcance ampliado, en vez de dejar dos descripciones de alcance ligeramente distintas para el mismo modulo.
4. **Clasificacion MVP.** Esta ficha conserva la clasificacion COULD HAVE del mapa definitivo sin modificarla, tal como exige la tarea. Coincide con esa clasificacion: MOD-025 no cubre ninguna obligacion OBLIGATORIO con plazo vencido, no es una dependencia estructural de ningun modulo MUST HAVE (punto 1 de esta nota), y no es indispensable para que el producto sea probatorio desde el primer dia (ese papel lo cumplen MOD-019 y MOD-021, no MOD-025); los tres criterios del test de tres condiciones de la seccion 2 del mapa definitivo apuntan en la misma direccion que la clasificacion ya asignada.
5. No se detecto ninguna otra inconsistencia material entre esta ficha y las fuentes de diseno ya decididas (`02_validacion_de_la_idea.md`, `04_objetivo_exacto_del_producto.md`, `05_tipos_de_usuario.md`, `22_anti_features.md`, `06_mapa_definitivo_de_modulos.md`, `mapa_modulos.json`). El documento maestro (`PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md`) no desarrolla la busqueda global como modulo en ninguna seccion (se confirmo por busqueda de texto "busqueda" sobre el documento completo, sin resultados fuera del indice de areas del prompt de analisis funcional), por lo que esta ficha se construyo a partir del mapa definitivo y del enfoque especifico dado en el enunciado de la tarea, sin una hipotesis previa del maestro que contrastar.
6. **Correccion aplicada tras revision adversarial: la seccion I (Alertas) de una version anterior de esta ficha contradecia, sin declararlo, su propia seccion L.2 y las reglas de conexion 2 y 5 de `06_mapa_definitivo_de_modulos.md`, seccion 4.** Esa version definia una alerta que exigia que MOD-025 notificara al Administrador (canal "Plataforma") y escalara al Auditor interno a las 24 horas, es decir, que MOD-025 disparara una notificacion de negocio, cuando la seccion L.2 de la propia ficha, la regla de conexion 5 ("MOD-025... son de solo lectura sobre el resto de modulos: no generan tareas ni escriben en otras entidades") y la regla de conexion 2 ("MOD-022 Notificaciones solo reacciona a eventos que le entregan MOD-021 y MOD-023") excluyen a MOD-025 como fuente directa de una notificacion o de un evento hacia MOD-022. Esta version corrige el mecanismo (no el criterio de deteccion, que se conserva sin cambios): la senal de volumen inusual de consultas en ambito sensible ya no se modela como alerta con notificacion y escalamiento (seccion I), sino como un indicador de dashboard de solo lectura que el Administrador revisa por iniciativa propia (seccion M), con los ajustes de referencia correspondientes en J, O y Q. No hay desacuerdo con el mapa definitivo: la correccion alinea la ficha con las reglas de conexion 2 y 5 ya vigentes en `06_mapa_definitivo_de_modulos.md`, sin proponer ningun cambio a ese documento.
