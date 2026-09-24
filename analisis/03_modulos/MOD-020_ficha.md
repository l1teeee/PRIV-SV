# MODULO: Dashboard y Reportes

Codigo corto del modulo: MOD-020
Clasificacion global del modulo: MUST HAVE (dashboard basico por perspectiva: pendientes, vencidos, tratamientos, solicitudes). Dentro del mismo modulo, los reportes exportables avanzados por area y la vista alternativa por los 8 clusters legales son SHOULD HAVE (ver seccion Q); esta ficha no cambia la clasificacion global MUST HAVE que trae `mapa_modulos.json`, solo documenta el desglose interno que la propia entrada del mapa ya anticipa en su campo `mvp`.
Obligaciones que cubre: ninguna obligacion propia (ningun OBL-ID de `analisis/01_legal/matriz_obligaciones.json` lo tiene como modulo propietario; verificado por busqueda directa de "MOD-020" sobre el archivo completo de las 105 obligaciones, sin resultados). Ninguna obligacion colaboradora tampoco: MOD-020 no aparece en el campo `modulos_candidatos` de ningun registro de la matriz. Esto es consistente con el principio de diseno de que los modulos transversales o de solo lectura no poseen obligaciones de negocio propias (`analisis/02_validacion/06_mapa_definitivo_de_modulos.md`, seccion 2, principio 5) y con la propia entrada de MOD-020 en `mapa_modulos.json` (`"obligaciones_propietarias": []`, `"obligaciones_colaboradoras": []`). MOD-020 es, en cambio, el punto de consumo declarado o implicito de los indicadores (seccion M) y reportes (seccion N) de practicamente todos los demas modulos: ver el catalogo consolidado de esta ficha y la nota final sobre la asimetria entre `depende_de` y el consumo real de datos.
Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (sin codigo, sin SQL, sin APIs, sin stack, sin infraestructura).
Fuentes usadas para esta ficha: `analisis/00_contexto_para_agentes.md`, `analisis/00_prompt_analisis_funcional.md`, `analisis/00_plantilla_ficha_modulo.md`, `analisis/02_validacion/mapa_modulos.json` (entrada MOD-020), `analisis/02_validacion/06_mapa_definitivo_de_modulos.md` (secciones 0, 2, 3, 4, 5, 6, 6.1, 7, 9), `analisis/01_legal/matriz_obligaciones.json` (verificacion de ausencia de obligaciones propias o colaboradoras), `analisis/02_validacion/02_validacion_de_la_idea.md` (secciones 2.3 a 2.7), `analisis/02_validacion/04_objetivo_exacto_del_producto.md` (secciones 1.1 a 1.3 y "Como se mide el exito"), `analisis/02_validacion/05_tipos_de_usuario.md` (secciones 5.1 a 5.4), `analisis/02_validacion/22_anti_features.md` (items 1, 5, 8, 9, 19, 22, 23, 25), `analisis/02_validacion/propuesta_mapa_obligaciones.md` (seccion 1, arbol de 8 clusters legales; seccion 2, fichas MOD-DASH y MOD-REP de la propuesta perdedora), `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` (seccion 31, Dashboard; hipotesis de producto, no decision), `analisis/02_validacion/lente_faltantes.md` y `lente_inconsistencias.md` (verificado: ninguna mencion especifica a MOD-020, Dashboard o Reportes), y las 24 fichas ya redactadas en `analisis/03_modulos/` (MOD-001 a MOD-019, MOD-021 a MOD-026), en particular sus secciones M (Dashboard) y N (Reportes) completas, extraidas con `awk '/^## M[.]/,/^## O[.]/' analisis/03_modulos/MOD-*.md`, y las menciones directas a "MOD-020" localizadas con `grep -n "MOD-020" analisis/03_modulos/*.md` (ver Nota final para el detalle del contrato de expectativas). MOD-021_ficha.md y MOD-018_ficha.md se usaron ademas como modelo de estilo y profundidad, segun pide la tarea; MOD-025_ficha.md (otro modulo terminal de lectura sin obligaciones propias) se uso como modelo estructural adicional para las secciones I, J y L. MOD-026_ficha.md (Centro de Ayuda) se releyo integramente al cerrar esta correccion, tras confirmar con un nuevo listado de la carpeta que ya existia, para integrar sus secciones M y N reales en el catalogo consolidado (ver Nota final, punto 7).

---

## A. Proposito

- **Por que existe.** Es la vista principal del sistema para saber, de un vistazo y sin tener que abrir 25 modulos distintos, en que estado esta el programa de proteccion de datos de la empresa: que esta pendiente, que esta vencido, que evidencia existe y que se puede exportar para mostrarselo a alguien mas (la gerencia, un auditor, la propia Autoridad de Ciberseguridad del Estado, ACE). Absorbe las areas 26 (Dashboard principal por perspectiva) y 28 (Reportes) del prompt de analisis funcional, que el documento maestro trata como una sola seccion (31, "Dashboard") sin desarrollar reportes como capacidad propia.
- **Que problema resuelve para la empresa.** La persona designada (que no es abogada ni tiene un equipo de privacidad dedicado) necesita, ademas de su bandeja de tareas (MOD-021), una fotografia del conjunto: cuantos tratamientos tiene registrados, cuantas solicitudes ARCO-POL estan abiertas, cuantos incidentes, que tan al dia esta la capacitacion, que controles de seguridad faltan. Sin este modulo, esa vision solo existiria abriendo cada modulo por separado y sumando mentalmente, lo cual es inviable para alguien sin experiencia y para una gerencia que solo quiere una respuesta rapida a "como vamos".
- **Que obligacion u obligaciones cubre.** Ninguna de forma directa (ver encabezado). Su valor no es instrumentar una obligacion especifica, sino hacer visibles, de forma agregada, el estado de las obligaciones que si instrumentan los demas modulos, y producir los reportes exportables que sirven como evidencia consolidada de varias de ellas (en particular OBL-PRIN-03, responsabilidad demostrada, propietaria de MOD-019, cuya vista agregada de "evidencia disponible" es uno de los indicadores que este modulo muestra).
- **Que valor aporta.**
  - *Operativo*: una sola pantalla de entrada al sistema, distinta segun quien la mira (Gerencia, Responsable, Legal/Delegado, Auditor), que reduce el tiempo de encontrar "como estamos" y dirige, mediante enlaces de detalle (drill-down), al registro fuente exacto cuando hace falta actuar.
  - *Probatorio*: los reportes exportables (seccion N) son, para varias obligaciones, la forma en que la empresa entrega evidencia consolidada a un auditor, a la Junta Directiva o a la ACE, siempre con verificacion de integridad delegada en MOD-019.
  - *De reduccion de riesgo*: hace visibles de inmediato las acciones vencidas, los expedientes sin evidencia y los controles obligatorios sin implementar, en vez de que esa informacion quede dispersa y solo se descubra durante una auditoria o una inspeccion.
- **Que NO hace este modulo (limites explicitos).**
  - No calcula ni muestra nunca un "porcentaje de cumplimiento legal": esta prohibido de forma expresa (`22_anti_features.md`, item 5; `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md`, seccion 31). Todo indicador se expresa como estado del programa, controles configurados, tareas pendientes o evidencia disponible.
  - No genera sus propios datos de negocio: no crea tratamientos, tareas, incidentes, controles ni evidencia; solo lee y agrega lo que otros modulos ya registraron (regla de conexion 5 y 6 de `06_mapa_definitivo_de_modulos.md`, seccion 4, aplicada aqui igual que a MOD-025 y MOD-026).
  - No crea tareas ni modifica ningun otro modulo: es un modulo terminal de lectura, tal como lo declara su propia entrada en `mapa_modulos.json` (`"alimenta_a": []`). Un indicador en rojo no crea automaticamente una tarea; si hace falta actuar, el usuario sigue el enlace de detalle hasta el modulo de origen y actua alli (por ejemplo, en MOD-021 o en el modulo de negocio correspondiente).
  - No decide ni interpreta juridicamente nada: no afirma que una obligacion "esta cumplida", solo que existe evidencia disponible o una tarea completada para ella.
  - No muestra nunca un dato personal de un titular externo: solo conteos y agregados (`22_anti_features.md`, item 8; ver regla de minimizacion en la seccion D.4).
  - No es un motor de analitica de negocio generico ni un BI comercial: sus indicadores y reportes estan acotados al programa de proteccion de datos de la empresa, no a metricas comerciales ajenas. Esto incluye, en particular, no duplicar la base de clientes de la empresa ni convertirse en un CRM de sus clientes (`22_anti_features.md`, item 1); el resto de este limite (no ser un BI generico) es un limite de alcance de producto que se desprende directamente del proposito del modulo (ver arriba, "Por que existe"), sin que exista un anti-feature especifico adicional que lo respalde por separado.
  - No usa en ningun texto de pantalla, de ayuda contextual ni de comunicacion comercial frases del tipo "cumplimiento garantizado" o "blindaje legal 100%": el Dashboard describe siempre estado del programa, controles configurados, tareas pendientes o evidencia disponible, nunca una promesa de resultado juridico (`22_anti_features.md`, item 22; ver tambien seccion H).
  - No trata las distintas categorias de sensibilidad de un dato personal de forma identica en sus indicadores agregados: cuando un indicador cuenta "tratamientos con dato sensible" (por ejemplo, el de MOD-006 en la seccion M.3.1), respeta la subclasificacion por categoria (salud, biometria, afiliacion sindical, etc.) que ya define el modulo fuente, en vez de mostrar una unica cifra que equipare categorias de riesgo distinto; MOD-020 tampoco introduce por su cuenta una categoria generica de "datos laborales" como si fuera, en si misma, una categoria sensible (`22_anti_features.md`, item 23).

---

## B. Usuarios

Roles estandar segun `analisis/02_validacion/05_tipos_de_usuario.md`, seccion 5.3 (los 12 roles del sistema). El area 26 del prompt de analisis funcional describe el Dashboard en 4 "perspectivas" (Gerencia, Responsable, Legal/Delegado, Auditor); estas perspectivas son una capa de presentacion sobre los 12 roles, no una quinta categoria de rol nueva ni un reemplazo del sistema de permisos de la seccion C. La tabla siguiente mapea cada rol a la perspectiva que ve por defecto al entrar al Dashboard (configurable: un usuario con varios roles ve la perspectiva de mayor alcance que le corresponda, y puede cambiar manualmente de perspectiva si su rol se lo permite, ver seccion C).

| Rol | Perspectiva por defecto | Para que usa MOD-020 |
|---|---|---|
| Administrador de la organizacion | Gerencia (con acceso adicional a las demas perspectivas) | Ve la vision general de la organizacion, revisa el estado de cada modulo, decide a quien mas compartir un reporte, y es quien puede exportar el Informe para Junta Directiva. |
| Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | Legal/Delegado | Ve riesgos y decisiones pendientes de su rol, revisa el avance por los 8 clusters legales, y exporta el paquete de reportes que respalda su informe periodico (OBL-DPO-07, propietario MOD-002). |
| Responsable ARCO-POL / Responsable del tramite | Responsable | Ve sus propias solicitudes pendientes y vencidas, agregadas desde MOD-011 y MOD-021. |
| Responsable Legal / Compliance | Legal/Delegado | Ve el mismo panel que el Delegado, con foco en base juridica, documentos y procedimiento sancionador. |
| Responsable de Seguridad / IT | Responsable (con enfasis en controles e incidentes) | Ve el estado de controles de seguridad, incidentes abiertos y cronometros de 72 horas agregados desde MOD-013 y MOD-015. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Responsable (acotado a su area) | Ve unicamente los indicadores y tareas de su propia area (tratamientos del RAT que administra, tareas asignadas), nunca el agregado de otras areas. |
| Aprobador | Responsable (vista de aprobaciones pendientes) | Ve el indicador de aprobaciones pendientes agregado desde MOD-021, sin visibilidad del resto del panel de Gerencia. |
| Auditor (interno) | Auditor | Ve el panel de evidencia disponible, huecos y vencimientos, exporta reportes con fecha de corte, siempre en modo de solo lectura. |
| Auditor externo (invitado) | Auditor (acotado a su alcance de auditoria) | Ve unicamente los indicadores y reportes del alcance temporal y de modulos habilitados para su auditoria puntual. |
| Usuario de consulta / Colaborador | Vista personal reducida (no el Dashboard completo) | Ve solo el resumen de sus propias tareas (equivalente a "Mis tareas de hoy" de MOD-021); no tiene acceso a las 4 perspectivas del Dashboard principal. |
| Titular (formulario externo) | No aplica | No usa MOD-020; su unica vista de estado es el estado de su propia solicitud dentro de MOD-011 o del Portal (MOD-012), que no pasa por este modulo. |
| Asesor externo invitado | Auditor (acotado al caso para el que fue invitado) | Ve unicamente los indicadores y reportes del caso puntual para el que fue invitado, nunca el panel general de la organizacion. |

**Nota sobre "Junta Directiva".** "Junta Directiva" no es un rol del sistema (no aparece en la seccion 5.3 de `05_tipos_de_usuario.md`): es, igual que ya lo modelan `MOD-002_ficha.md` y `MOD-005_ficha.md` en sus propios reportes, unicamente un destinatario de un reporte exportado (seccion N), que recibe el documento fuera del sistema y nunca inicia sesion como usuario para ver el Dashboard en vivo. Este modulo mantiene esa misma convencion sin crear un rol nuevo.

---

## C. Permisos

Convencion: "Si" = permitido por defecto; "Si*" = permitido solo dentro del alcance de visibilidad que el rol ya tiene en el modulo de origen de cada indicador o reporte; "No" = no permitido.

| Accion | Administrador | Delegado / Resp. interno | Resp. ARCO-POL | Legal/Compliance | Seguridad/IT | Responsable de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver perspectiva Gerencia | Si | Si* (lectura) | No | Si* (lectura) | No | No | No | Si* (lectura, como evidencia) | No | No | No |
| Ver perspectiva Responsable (la propia) | Si | Si | Si* | Si* | Si* | Si* (solo su area) | Si* (solo aprobaciones) | Si* (lectura) | No | Si* (vista personal reducida) | No |
| Ver perspectiva Legal/Delegado, incluida la vista por 8 clusters | Si | Si | No | Si | No | No | No | Si* (lectura) | No | No | No |
| Ver perspectiva Auditor (evidencia, huecos, vencimientos) | Si | Si* | No | Si* | No | No | No | Si | Si* (acotado a su alcance) | No | Si* (acotado a su caso) |
| Aplicar filtro por sucursal, unidad o modulo de origen | Si | Si | Si* | Si | Si* | Si* (solo su area) | Si* | Si | Si* | No | No |
| Bajar al registro fuente (drill-down) desde un indicador | Si | Si | Si* | Si | Si* | Si* | Si* | Si (solo lectura del destino) | Si* (solo lectura del destino) | Si* (solo lo asignado) | Si* (solo su caso) |
| Ver el detalle de una tendencia (fotos periodicas / cierres mensuales) | Si | Si | No | Si | Si* | No | No | Si | Si* | No | No |
| Exportar un reporte (seccion N) | Si | Si | Si* | Si | Si* | No | No | Si | Si* (acotado) | No | No |
| Exportar el Informe para Junta Directiva | Si | Si* | No | No | No | No | No | No | No | No | No |
| Enlazar o iniciar el paquete de evidencia para la ACE (armado por MOD-019) | Si | Si | No | Si* | No | No | No | No | No | No | No |
| Configurar umbrales de semaforo, catalogo de sucursales/unidades o el calendario de fotos mensuales | Si | No | No | No | No | No | No | No | No | No | No |
| Crear, modificar o eliminar un registro desde un indicador o reporte | No (siempre redirige al modulo de origen) | No | No | No | No | No | No | No | No | No | No |

**Separacion de funciones.** MOD-020 no crea, aprueba ni cierra ningun registro de negocio, por lo que la separacion de funciones sustantiva ya esta resuelta en el modulo de origen de cada indicador (regla de conexion 5 y 6 de `06_mapa_definitivo_de_modulos.md`, seccion 4, igual que en MOD-025). El unico control propio de este modulo es de confidencialidad, no de doble control: un Responsable de area nunca ve el agregado de otra area, y ningun rol distinto de Administrador o Delegado/Responsable interno puede exportar el Informe para Junta Directiva, porque ese documento consolida datos de toda la organizacion (incluyendo areas de otros responsables) y no solo los del rol que lo exporta. El acceso de un Auditor externo o un Asesor externo invitado queda siempre acotado al alcance temporal y de modulos habilitado para su caso, igual que en MOD-021 y MOD-025.

---

## D. Informacion de entrada

MOD-020 no administra entidades de negocio propias en el sentido de la seccion 7 de `06_mapa_definitivo_de_modulos.md` (no aparece en esa lista de entidades por modulo): es un modulo de lectura y agregacion, cuyos unicos "datos de entrada" propios son los filtros que el usuario elige, el catalogo de umbrales de semaforo y el calendario de fotos periodicas que el Administrador configura, y el propio registro tecnico de cada exportacion.

### D.1 Filtros de vista (lo que elige el usuario)

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda que vera el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Perspectiva | Seleccion unica | Obligatorio (autoseleccionada segun el rol, ver seccion B) | Gerencia, Responsable, Legal/Delegado, Auditor | Debe coincidir con una perspectiva habilitada para el rol del usuario (seccion C) | "Elija desde que punto de vista quiere ver la informacion: vision general, sus propios pendientes, riesgos y decisiones, o evidencias." | Buena practica (area 26 del prompt de analisis funcional) |
| Vista alternativa por cluster legal | Booleano | Opcional (solo visible en la perspectiva Legal/Delegado) | Activada / Desactivada | Solo disponible si la perspectiva es Legal/Delegado | "Active esta opcion para ver la informacion agrupada por los 8 temas legales del programa en vez de por las 6 etapas del recorrido." | Injerto del juez 3 (`06_mapa_definitivo_de_modulos.md`, seccion 3, ficha de MOD-020), tomado de `propuesta_mapa_obligaciones.md`, seccion 1 |
| Cluster legal (si la vista alternativa esta activada) | Seleccion unica o "Todos" | Opcional | Nucleo organizativo, Entrada y hoja de ruta, Registro y gobernanza, Relacion con el titular, Relacion con terceros, Gestion de crisis y control, Documentacion, Relacion con la autoridad | Debe ser uno de los 8 clusters definidos en la seccion M.4 | "Filtre por un tema legal especifico, por ejemplo 'Relacion con terceros' para ver solo proveedores y transferencias." | Ver mapeo de clusters en la seccion M.4 |
| Etapa del recorrido (vista por defecto) | Seleccion unica o "Todas" | Opcional | Empezar, Diagnosticar, Planificar, Registrar, Operar, Demostrar | Debe ser una de las 6 etapas de `06_mapa_definitivo_de_modulos.md`, seccion 1 | "Filtre por la etapa del recorrido del sistema, por ejemplo 'Operar' para ver ARCO-POL, incidentes y riesgos." | Estructura del mapa definitivo, seccion 1 |
| Modulo de origen | Seleccion multiple | Opcional | Catalogo de los 26 modulos (por nombre, no por codigo tecnico, en el texto de pantalla) | Debe existir en `mapa_modulos.json` | "Filtre por un modulo especifico si ya sabe cual le interesa." | Buena practica |
| Sucursal o unidad | Seleccion multiple o "Todas" | Opcional | Catalogo de sucursales y unidades de MOD-001 | Debe existir en MOD-001; un Responsable de area solo puede elegir su propia area (seccion C) | "Filtre por sucursal o area, si su empresa tiene mas de una." | Buena practica; catalogo compartido de MOD-001 |
| Sociedad (grupo empresarial) | Seleccion unica o "Todas" | Opcional; no aplicable mientras el MVP no soporte multi-sociedad | Catalogo de sociedades, si existe mas de una | Solo visible si la organizacion tiene mas de una sociedad dada de alta (funcionalidad V1/Enterprise, ver Nota final punto 2) | "Filtre por sociedad del grupo, si su organizacion administra mas de una razon social." | Decision de alcance 2.7.31 de `02_validacion_de_la_idea.md`: el MVP solo soporta una razon social con sucursales, no varias sociedades; este filtro queda listo pero inactivo hasta que exista esa capacidad (ver Nota final) |
| Periodo o fecha de corte | Fecha (rango) o snapshot especifico | Opcional (por defecto: en tiempo real, a hoy) | Rango libre, o una de las fotos periodicas (cierres mensuales) ya generadas (seccion D.3) | Fecha desde no puede ser posterior a fecha hasta | "Elija un periodo, o compare con el cierre de un mes anterior para ver la tendencia." | Regla del enfoque especifico de esta tarea: "fotos periodicas (cierres mensuales) para tendencias" |

### D.2 Configuracion de umbrales de semaforo (mantenida por el Administrador)

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda que vera el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Umbral configurable de un indicador (cuando el modulo fuente lo declara configurable) | Numero (dias, porcentaje o conteo, segun el indicador) | Opcional (cada indicador trae un valor por defecto documentado en su propia ficha, seccion M) | Depende del indicador (por ejemplo, dias habiles antes de marcar "proximo a vencer") | Debe respetar el rango minimo/maximo que declare el modulo fuente, si lo tiene | "Ajuste cuando este indicador cambia de color, segun el tamano y el ritmo de trabajo de su empresa." | Buena practica; cada umbral hereda su definicion original de la ficha del modulo que produce el indicador, MOD-020 solo expone el control de configuracion en un solo lugar |
| Umbral de empleados para separacion de funciones (referencia, no editable aqui) | Numero (solo lectura) | No aplica (se edita en MOD-001) | Valor vigente en MOD-001 | No aplica | "Este valor se configura en Organizacion y Personas; aqui solo se muestra como referencia." | `05_tipos_de_usuario.md`, seccion 5.4 |

### D.3 Fotos periodicas (cierres mensuales)

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda que vera el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Dia del mes del cierre | Numero (dia 1 a 28) | Obligatorio (con valor por defecto: ultimo dia habil del mes, via MOD-023) | Configurable por el Administrador | Debe ser un dia habil segun MOD-023 | "Elija que dia de cada mes se toma la fotografia del estado del programa para poder comparar tendencias." | Regla del enfoque especifico de esta tarea |
| Snapshot generado | Registro tecnico (autogenerado) | Obligatorio (uno por mes) | Congela el valor de todos los indicadores de la seccion M.3 en ese momento | No editable una vez generado | "Aqui puede ver como estaba cada indicador al cierre de un mes anterior, sin que los cambios posteriores lo alteren." | Buena practica de trazabilidad de tendencias |
| Motivo de recalculo manual (excepcional) | Texto | Obligatorio si se fuerza un recalculo fuera del calendario | Libre | Debe registrar quien y por que | "Si necesita regenerar una fotografia antes de tiempo, explique brevemente el motivo." | Buena practica |

### D.4 Campo generado por el sistema (registro de exportacion, no de entrada del usuario)

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda que vera el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Registro de exportacion | Registro tecnico (ver seccion J) | Obligatorio (autogenerado en cada exportacion) | Usuario, fecha y hora, reporte exportado, filtros aplicados, formato | No editable | No visible como formulario; se explica en la ayuda contextual (seccion R) | `22_anti_features.md`, item 25 (integridad de toda exportacion) |

**Campos precargados desde el diagnostico, plantillas u otros modulos.** MOD-020 no precarga un formulario de negocio propio: todo lo que muestra proviene por referencia de las secciones M y N de cada modulo (indicadores) y de MOD-001 (catalogo de sucursales, unidades y roles), MOD-023 (calendario de dias habiles para calcular "proximo a vencer" y para fijar el dia del cierre mensual) y MOD-024 (bandera `regimen_reforma_659`, mostrada como badge informativo igual que en MOD-002, MOD-017 y MOD-024).

**Que campos contienen o podrian contener datos personales, y como se minimizan.** Ningun campo de este modulo contiene un dato personal de un titular externo. Regla de minimizacion (privacy by design), analoga a la ya definida para MOD-025 en su seccion D.3:
1. Todo indicador es un conteo, un porcentaje, una fecha o un estado agregado (por ejemplo "3 solicitudes ARCO-POL abiertas"), nunca el nombre, identificacion ni cualquier dato del titular al que pertenece un expediente individual (`22_anti_features.md`, items 8 y 9).
2. El drill-down (bajar al registro fuente) respeta siempre los permisos del modulo de destino (seccion C): si el rol del usuario no puede ver el expediente individual en su modulo de origen, tampoco puede verlo llegando desde el Dashboard; el enlace simplemente no se muestra o redirige a un mensaje de "sin acceso", nunca revela el contenido.
3. Los reportes exportables (seccion N) que si incluyen contenido detallado (por ejemplo, un listado de expedientes ARCO-POL con su estado) son en realidad reportes del modulo de origen (MOD-011, MOD-013, etc.) que MOD-020 enlaza o reempaqueta para exportacion consolidada, nunca datos que MOD-020 capture o derive por si mismo; el contenido y las reglas de minimizacion de cada uno siguen definidas en la ficha de su modulo de origen.

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Vista de Dashboard por perspectiva | Indicadores agregados de la seccion M.3, filtrados por perspectiva, cluster o etapa segun la eleccion del usuario | Pantalla, con semaforos y enlaces de detalle | En tiempo real, cada vez que el usuario abre o cambia de filtro | El usuario que consulta, segun su rol y perspectiva (seccion C) |
| Foto periodica (cierre mensual) | Copia congelada del valor de todos los indicadores de la seccion M.3 en la fecha configurada | Snapshot interno, consultable como punto de comparacion de tendencia | Automaticamente en el dia configurado (seccion D.3), o manualmente con motivo registrado | Todos los roles con acceso a la perspectiva correspondiente; el historico completo, Auditor |
| Reporte exportado | Cualquiera de los reportes de la seccion N | PDF, XLSX, CSV o ZIP, segun el reporte | Bajo demanda | El rol que lo exporta y el destinatario que declare (por ejemplo, Junta Directiva, Auditor externo, ACE) |
| Informe para Junta Directiva | Sintesis ejecutiva del estado del programa por etapa y por cluster, con los indicadores de mayor severidad y el avance del Plan de Cumplimiento (MOD-005) | PDF | Bajo demanda, o de forma periodica si el Administrador lo programa | Junta Directiva (destinatario externo al sistema, ver seccion B) |
| Enlace al paquete de evidencia para la ACE | Referencia directa al paquete que arma MOD-019 (Centro de Evidencias), sin que MOD-020 genere un paquete propio paralelo | Enlace mas metadatos del paquete (fecha, alcance, estado) | Bajo demanda, cuando el usuario elige "preparar entrega a la ACE" desde el Dashboard | Delegado/Responsable interno, Legal/Compliance, Administrador |
| Evento de auditoria de consulta y de exportacion | Usuario, fecha y hora, perspectiva o reporte, filtros aplicados | Registro en el AuditLog transversal | En cada exportacion, y en el acceso a un indicador marcado con nivel de confidencialidad reforzado (por ejemplo, el propio Informe para Junta Directiva) | MOD-019 Centro de Evidencias (lectura), Auditor interno |

MOD-020 no genera tareas, alertas de negocio propias hacia otro modulo, ni documentos regulatorios: es coherente con su caracter de modulo terminal de solo lectura (`06_mapa_definitivo_de_modulos.md`, seccion 4, regla de conexion 5, y su propia entrada `"alimenta_a": []` en `mapa_modulos.json`), igual que MOD-025 y MOD-026. Por eso las secciones F, G e I de esta ficha son mas breves que las de un modulo de negocio con expedientes propios.

---

## F. Workflow

MOD-020 no administra un ciclo de vida de expedientes con estados de negocio (Pendiente, Aprobada, Completada, etc.): no posee esa entidad. Tiene, en cambio, dos ciclos propios y mas simples: el de una **consulta de vista** (analogo al de MOD-025) y el de una **foto periodica (cierre mensual)**, que si necesita estados propios porque, a diferencia de una consulta, un snapshot persiste y se conserva.

### F.1 Diagrama de estados de una consulta de vista

```
   +-----------+   el usuario abre el Dashboard o cambia   +------------+
   | INACTIVA  | -----------------------------------------> | CALCULANDO |
   +-----------+   de perspectiva, cluster o filtro         +------------+
         ^                                                        |
         |                                                        v
         |                                              +-------------------+
         |                                              |  VISTA MOSTRADA   |
         |                                              +-------------------+
         |                                                 |      |       |
         |                          el usuario cambia      |      |       | el usuario
         |                          de filtro (vuelve      |      |       | exporta un
         |                          a CALCULANDO)          |      |       | reporte (ver F.3)
         |                                                 |      |       v
         |                       el usuario hace clic      |      |  +-------------+
         |                       en un enlace de detalle   |      |  | EXPORTANDO  |
         |                       (sale de MOD-020 hacia    |      |  +-------------+
         |                       el modulo de origen)      |      |       |
         |                                                 v      |       v
         +-------------------------------------------------+      +-------+
           el usuario cierra el Dashboard o navega a otra pantalla
```

### F.2 Diagrama de estados de una foto periodica (cierre mensual)

```
                    +-------------+
         +--------->| PROGRAMADA  |
         |          +------+------+
         |                 | llega el dia configurado (via MOD-023)
         |                 v
         |          +-------------+     motivo registrado      +----------------------+
         |          | GENERANDOSE |<---------------------------| (recalculo manual,   |
         |          +------+------+                             | ver seccion D.3)     |
         |                 |                                    +----------------------+
         |                 v
         |          +-------------+
         |          |  GENERADA   |  (estado terminal para ese mes, no se recalcula
         |          +------+------+   salvo el recalculo manual con motivo)
         |                 |
         |     se archiva por antiguedad (regla de retencion de MOD-016)
         |                 v
         |          +-------------+
         +----------|  ARCHIVADA  |  (se conserva para tendencia historica, nunca se borra)
                     +-------------+
```

### F.3 Tabla de transiciones

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| Inactiva (consulta) | El usuario abre el Dashboard o cambia de filtro | Debe tener permiso de ver la perspectiva elegida (seccion C) | Calculando | Cualquier usuario con acceso al Dashboard | Se consultan los indicadores vigentes de los modulos fuente aplicables al filtro |
| Calculando | El calculo termina | Ninguna adicional | Vista mostrada | Sistema (automatico) | Se muestra la vista filtrada por permisos; no se registra evento de auditoria (una vista en pantalla no exporta nada) |
| Vista mostrada | El usuario hace clic en un enlace de detalle | El usuario debe conservar el permiso de ver ese registro en su modulo de origen en el momento del clic | (sale de MOD-020 hacia el modulo de origen) | Usuario que consulta | Ninguno adicional: la accion sobre el registro queda gobernada por los permisos de ese modulo de origen, no por MOD-020 |
| Vista mostrada | El usuario elige exportar un reporte | El reporte elegido debe estar habilitado para su rol (seccion C) | Exportando | Usuario con permiso de exportar | Se genera el archivo, se calcula su verificacion de integridad via MOD-019, y se registra el evento de exportacion (seccion D.4) |
| Exportando | El archivo se genera correctamente | Ninguna adicional | Vista mostrada | Sistema (automatico) | El archivo queda disponible para descarga; evento de auditoria completo |
| Programada (snapshot) | Llega el dia configurado del cierre mensual | El dia debe ser habil segun MOD-023; si cae en dia inhabil, se recalcula al siguiente dia habil | Generandose | Sistema (automatico) | Se congela el valor de cada indicador de la seccion M.3 en ese momento |
| Generandose (snapshot) | El calculo del snapshot termina | Ninguna adicional | Generada | Sistema (automatico) | Snapshot disponible como punto de comparacion de tendencia; evento de auditoria |
| Generada (snapshot) | Un usuario autorizado fuerza un recalculo manual | Debe registrar el motivo (seccion D.3) | Generandose | Administrador, Delegado/Responsable interno | El snapshot anterior de ese mes se conserva en el historial, no se sobrescribe en silencio (regla general de preservacion de historial, `06_mapa_definitivo_de_modulos.md`, seccion 2, principio 8) |
| Generada (snapshot) | Se cumple el plazo de retencion documental de cumplimiento propio (referencia a MOD-016) | Automatico, segun la regla que MOD-016 defina para este tipo de registro | Archivada | Sistema (automatico) | El snapshot deja de aparecer en la seleccion rapida de periodo, pero sigue disponible bajo demanda para tendencia historica de largo plazo; nunca se elimina (`22_anti_features.md`, item 19) |

**Registros vinculados.** Ninguna vista ni ningun snapshot de MOD-020 modifica el estado de un registro de otro modulo: son siempre lecturas. Si el usuario necesita actuar sobre lo que ve (por ejemplo, resolver una tarea vencida), lo hace en el modulo de origen a traves del enlace de detalle, y esa accion se refleja en el Dashboard en la siguiente vez que se recalcula la vista (en tiempo real) o en el siguiente cierre mensual (para la tendencia).

---

## G. Automatizaciones

Todas las reglas siguientes son configurables por la organizacion (activar/desactivar, ajustar umbrales), salvo que se indique lo contrario.

| Disparador | Condicion | Accion |
|---|---|---|
| El usuario abre el Dashboard o cambia de filtro | Tiene permiso de ver la perspectiva o el cluster elegido | Recalcular en tiempo real los indicadores de la seccion M.3 aplicables, filtrados por permisos, sucursal/unidad y periodo |
| Llega el dia configurado del cierre mensual (via MOD-023) | Existe al menos un indicador activo en la seccion M.3 | Generar la foto periodica (snapshot) del mes, congelando el valor de cada indicador |
| Un indicador cruza su umbral configurado (por ejemplo, pasa de amarillo a rojo) | El umbral esta definido en la ficha del modulo fuente o en la seccion D.2 | Actualizar el color del semaforo en la vista; MOD-020 no dispara una notificacion por si mismo (ver seccion I): quien recibe alertas de negocio las recibe siempre desde el modulo de origen via MOD-022 |
| Un modulo fuente archiva, elimina o cambia de estado un registro que sustenta un indicador | El indicador ya estaba calculado sobre ese registro | Reflejar el nuevo valor en la proxima vista en tiempo real, sin esperar al cierre mensual |
| MOD-024 activa la bandera de regimen FUTURO | El indicador o el badge en pantalla depende del regimen vigente (por ejemplo, el badge ACTUAL/FUTURO de MOD-002 y MOD-024) | Actualizar el badge en todas las perspectivas; no se recalculan retroactivamente las fotos periodicas ya generadas antes del cambio (regla de preservacion de historial) |
| El usuario exporta cualquier reporte de la seccion N | El reporte esta habilitado para su rol | Generar el archivo, calcular su verificacion de integridad a traves de MOD-019, y registrar el evento de exportacion en el AuditLog |
| El usuario elige "preparar entrega a la ACE" desde la perspectiva Legal/Delegado | El rol tiene el permiso correspondiente (seccion C) | Enlazar (no generar de nuevo) al paquete de evidencia que arma MOD-019, mostrando su fecha de generacion y su estado |
| Un modulo aun no existe en el MVP vigente (por ejemplo, MOD-010 Transferencias o MOD-014 Riesgos/EIPD, ambos SHOULD HAVE) | El indicador de ese modulo no tiene datos que agregar | Mostrar el indicador como "no disponible en esta version" en vez de un valor en cero o un error, para no sugerir que el riesgo correspondiente es inexistente |

---

## H. Decisiones que NO debe automatizar

- **Traducir cualquier indicador o combinacion de indicadores en una afirmacion de "cumplimiento legal", con o sin porcentaje.** Texto de advertencia: "Este panel muestra el estado del programa (controles configurados, tareas pendientes, evidencia disponible), no una medicion de cumplimiento legal. Consulte con su Delegado o con asesoria especializada antes de afirmar que su empresa cumple con la ley." Razon: es el anti-feature mas explicito del producto (`22_anti_features.md`, item 5; `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md`, seccion 31); ninguna combinacion de indicadores operativos equivale a una conclusion juridica sobre cumplimiento.
- **Decidir por si mismo si un indicador en rojo ya constituye una infraccion sancionable.** Texto de advertencia: "Un indicador en rojo senala una tarea, un control o una evidencia pendiente; no es, por si mismo, una conclusion sobre si existe una infraccion. Consulte a su Delegado o a asesoria especializada." Razon: el catalogo de infracciones (Art. 56 LPDP, propietario MOD-024) exige un analisis que el Dashboard no puede realizar automaticamente.
- **Generar o enviar el paquete de evidencia para la ACE sin que una persona autorizada lo revise y lo confirme.** Texto de advertencia: "Este enlace prepara el paquete de evidencia; su envio a la ACE requiere la revision y confirmacion de la organizacion." Razon: coherente con `22_anti_features.md`, item 13 (el sistema no presenta tramites ante la ACE en nombre de la empresa sin que esta lo autorice y ejecute); MOD-020 solo enlaza el paquete que MOD-019 arma, nunca lo envia por su cuenta.
- **Decidir por si mismo el nivel de acceso de un Auditor externo o un Asesor externo invitado a una perspectiva o a un reporte.** Texto de advertencia: "Requiere validacion de la organizacion." Razon: el alcance de una auditoria o de una invitacion puntual es una decision organizativa, no un ajuste automatico del Dashboard (misma logica que MOD-021, seccion H).
- **Eliminar en forma definitiva una foto periodica (cierre mensual), incluso a pedido del Administrador.** Texto de advertencia: "Las fotos periodicas no pueden eliminarse; solo pueden archivarse." Razon: son evidencia de la evolucion del estado del programa en el tiempo, y borrarlas rompe la trazabilidad que la propia funcionalidad de tendencia promete (`22_anti_features.md`, item 19).
- **Elegir por si mismo, sin configuracion explicita del Administrador, a que cluster legal pertenece un modulo nuevo que se agregue en el futuro.** Texto de advertencia: (no aplica advertencia visible al usuario final; nota para quien mantenga el catalogo) "La asignacion de un modulo a uno de los 8 clusters legales es una decision de diseno del producto, no una inferencia automatica del sistema." Razon: el mapeo de clusters (seccion M.4) es una clasificacion de producto, y una asignacion incorrecta desalinearia la vista Legal/Delegado sin que nadie lo note.

---

## I. Alertas

No aplica en el sentido de alertas de negocio con notificacion push: MOD-020 no genera alertas propias hacia ningun usuario ni hacia ningun otro modulo, consistente con su declaracion `"alimenta_a": []` en `mapa_modulos.json` y con la regla de conexion 5 de `06_mapa_definitivo_de_modulos.md`, seccion 4 (los modulos de solo lectura "no generan tareas ni escriben en otras entidades, solo indexan o explican"), la misma regla que ya aplica `MOD-025_ficha.md` a la Busqueda Global. Quien necesita ser avisado de que una tarea esta por vencer, que un control no tiene evidencia o que un plazo de 72 horas esta por cumplirse recibe esa alerta desde el modulo de origen (MOD-021, MOD-022) directamente, no desde el Dashboard.

Lo unico que MOD-020 aporta en este terreno es visual, no una notificacion: los semaforos de la seccion M.3 cambian de color en tiempo real cuando el modulo fuente lo justifica, y el usuario los revisa por iniciativa propia al entrar al Dashboard, exactamente igual que el patron ya documentado en `MOD-025_ficha.md`, seccion I, para el indicador de "volumen de consultas en ambito sensible". El unico indicador propio de MOD-020 que podria justificar una alerta (que una foto periodica no se genero en la fecha esperada) se modela como indicador de solo lectura para el Administrador (seccion M.2), no como una alerta con escalamiento, porque no representa un riesgo legal para la empresa cliente, solo una falla operativa menor del propio modulo.

---

## J. Evidencia

MOD-020 no es propietario de ninguna obligacion (ver encabezado), pero sus reportes exportados (seccion N) y sus fotos periodicas (seccion D.3) sirven de respaldo consolidado para varias obligaciones cuyo dueno real es otro modulo.

- **Registro de exportacion con fecha, hora, usuario, reporte y filtros aplicados** (seccion D.4): prueba quien exporto que informacion, cuando y con que alcance, igual que el patron ya definido para MOD-021 y MOD-025.
- **Verificacion de integridad de cada archivo exportado**, delegada al mecanismo unico que expone MOD-019: MOD-020 no reinventa su propio formato de hash o firma; entrega sus reportes a MOD-019 para que el paquete de evidencias sea consistente en todo el sistema (mismo principio que MOD-021, seccion J).
- **Fotos periodicas (cierres mensuales) como evidencia de la evolucion del estado del programa en el tiempo**: al conservarse sin poder editarse (seccion H), permiten mostrar, ante una auditoria o una inspeccion, que el estado mostrado en un momento dado no fue alterado retroactivamente.
- **Que obligacion prueba cada evidencia.** De forma indirecta, el indicador "evidencia disponible por obligacion aplicable" (tomado de MOD-019, ver seccion M.3) sostiene OBL-PRIN-03 (responsabilidad demostrada, Art. 5 lit. i LPDP); los reportes de auditoria y de controles de seguridad (seccion N) sostienen de forma agregada las evidencias que cada modulo fuente ya declara en su propia seccion J. MOD-020 nunca crea una evidencia nueva: siempre reempaqueta o enlaza evidencia que ya existe en su modulo de origen.
- **Tiempo de conservacion.** El registro de exportaciones y las fotos periodicas siguen la regla de conservacion documental de cumplimiento propio que defina MOD-016 Retencion y Eliminacion para este tipo de registro tecnico (no una regla propia de MOD-020); mientras MOD-016 no fije un plazo especifico, se aplica por defecto un periodo largo (propuesta inicial: 5 anios, equiparable al de los expedientes de MOD-011/MOD-013) dado que las fotos periodicas son, precisamente, el instrumento de tendencia de largo plazo que este modulo promete. [opinion de producto, sin obligacion legal que fije este plazo especifico]

---

## K. Documentos asociados

- **Documentos requeridos como entrada.** Ninguno. MOD-020 no exige ningun documento para funcionar; todo documento que un reporte referencia (por ejemplo, una version de un Aviso de Privacidad citada en el reporte gerencial) es propiedad de su modulo de origen (MOD-008).
- **Documentos generados.**
  - Cada reporte de la seccion N, en su formato correspondiente (PDF, XLSX, CSV o ZIP).
  - Informe para Junta Directiva (ver seccion E y N.1).
  - Enlace al paquete de evidencia para la ACE, armado por MOD-019 (MOD-020 no genera el archivo, solo lo enlaza y deja constancia de haberlo hecho).
- **Plantillas que el sistema provee.**
  - Plantilla del Informe para Junta Directiva, con secciones fijas (estado por etapa, estado por cluster, indicadores criticos, avance del Plan de Cumplimiento). Requiere validacion de la organizacion antes de enviarse fuera del sistema, porque combina datos de varios modulos y su interpretacion final es responsabilidad de quien lo firma.
  - Plantilla del Informe gerencial consolidado (ver N.1), reutilizable como base del Informe para Junta Directiva cuando la empresa no necesita el nivel de detalle completo de este ultimo.
- **Anexos y evidencias documentales.** Los archivos que un reporte exportado incluye como anexo (por ejemplo, el checklist de controles de MOD-015 dentro del reporte de seguridad) provienen siempre de su modulo de origen; MOD-020 los reempaqueta para la exportacion consolidada, nunca los modifica.

---

## L. Dependencias

### L.1 Diagrama

```
   Todos los modulos de negocio y transversales (MOD-001 a MOD-019, MOD-021 a MOD-026)
   escriben o exponen indicadores (seccion M de cada uno)
   y reportes (seccion N de cada uno); MOD-020 nunca escribe hacia ellos
                              |
                              v
                    +----------------------+
                    |  MOD-020 DASHBOARD   |
                    |     Y REPORTES       |
                    +----------------------+
                       ^      |        ^
   dependencia         |      | filtra siempre por permisos     |
   estructural minima  |      | del modulo de origen antes      | consulta
   (depende_de en      |      | de mostrar un resultado         | catalogo de
   mapa_modulos.json): |      v                                  | roles/sucursales
                       |  (drill-down hacia el modulo de origen) |
   MOD-005 Plan -------+                                         |
   MOD-019 Evidencias--+                                         |
   MOD-021 Tareas ------+                                        |
                                                                  v
                                                        MOD-001 Organizacion y Personas
                                                        MOD-023 Calendario (dias habiles,
                                                                 fecha del cierre mensual)
                                                        MOD-024 Regulatorio (badge de
                                                                 regimen ACTUAL/FUTURO)
```

### L.2 Lista de dependencias

**Depende_de estructural, segun `mapa_modulos.json`:** MOD-005 (Plan de Cumplimiento), MOD-019 (Centro de Evidencias), MOD-021 (Centro de Tareas). Estas tres son la dependencia estructural minima: son las que hacen operable el "dashboard basico" que la propia entrada de MOD-020 en el mapa justifica como MUST HAVE ("pendientes, vencidos, tratamientos, solicitudes"; MOD-021 aporta pendientes y vencidos, MOD-019 aporta evidencia disponible, MOD-005 aporta el avance del plan), y coinciden con el test de tres condiciones de `06_mapa_definitivo_de_modulos.md`, seccion 2, principio 7: los tres son tambien MUST HAVE.

**Consumo real de indicadores y reportes (mas amplio que el `depende_de` estructural, ver Nota final punto 1).** En la practica funcional, y confirmado por el `grep -n "MOD-020" analisis/03_modulos/*.md` ejecutado antes de escribir esta ficha (ver Nota final), MOD-020 consume, a traves de la seccion M (indicadores) y la seccion N (reportes) de cada ficha ya redactada, datos de los 24 modulos existentes al cierre de esta correccion: MOD-001 a MOD-019 y MOD-021 a MOD-026. Esto es exactamente la misma asimetria, ya documentada y aceptada, entre `depende_de` (dependencia estructural minima de construccion) y el consumo real de datos por referencia, que la seccion 6.1 de `06_mapa_definitivo_de_modulos.md` explica para MOD-001, MOD-023 y MOD-024 ("alimenta_a puede ademas listar destinatarios adicionales que no tienen una entrada depende_de reciproca explicita en el modulo consumidor"): aqui el mismo fenomeno ocurre al reves, con MOD-020 como consumidor amplio y cada modulo de origen declarando "MOD-020" en su propio `alimenta_a` (cuando lo declara) sin que eso implique que MOD-020 deba declarar una dependencia estructural reciproca hacia cada uno de ellos para poder lanzarse en su version minima.

**Que catalogos comparte.** MOD-020 no mantiene un catalogo propio de sucursales, unidades, roles o dias habiles: consulta por referencia el catalogo de MOD-001 (sucursales, unidades, roles) y el de MOD-023 (calendario de dias habiles, usado tanto para "proximo a vencer" como para fijar la fecha del cierre mensual). El badge de regimen ACTUAL/FUTURO que aparece en varias vistas del Dashboard (por ejemplo, dentro del cluster "Nucleo organizativo") se lee siempre de MOD-024, nunca se calcula ni se duplica en MOD-020.

**Que ocurre si un modulo dependiente no existe en el MVP.** MOD-005, MOD-019 y MOD-021 son los tres MUST HAVE de los que depende la version minima vendible de este modulo (seccion Q); ninguno falta en el MVP, por lo que MOD-020 no necesita un modo degradado para su nucleo. Para los modulos SHOULD HAVE o COULD HAVE que aun no existan o que solo tengan cobertura parcial (por ejemplo, MOD-010 Transferencias, MOD-012 Portal del Titular, MOD-014 Riesgos/EIPD, MOD-016 Retencion, MOD-018 Auditoria de Cumplimiento, MOD-025 Busqueda Global), el indicador correspondiente se muestra como "no disponible en esta version" en vez de un valor en cero (regla G, ultima fila), para no sugerir que el riesgo o la actividad de ese modulo es inexistente cuando en realidad el modulo simplemente aun no esta activo.

---

## M. Dashboard

MOD-020 es, en si mismo, el Dashboard: a diferencia de las demas fichas, donde esta seccion describe los pocos indicadores que ESE modulo aporta al panel principal, aqui esta seccion tiene dos partes distintas. La seccion M.2 describe los indicadores propios del Dashboard como herramienta (uso, cobertura, estado del programa agregado). La seccion M.3 consolida, en un solo lugar, el catalogo completo de indicadores que los demas 23 modulos ya redactados aportan al panel (exactamente lo que pide el enfoque especifico de esta tarea), organizados por modulo fuente. Ningun indicador de esta seccion se expresa nunca como "porcentaje de cumplimiento legal" (`22_anti_features.md`, item 5).

### M.1 Principio general de agregacion

- MOD-020 nunca recalcula ni reinterpreta el valor de un indicador: lo muestra tal como su modulo fuente lo define en su propia seccion M (formula, semaforo y umbral), y solo lo agrega (por ejemplo, sumando conteos de varios modulos de una misma etapa o cluster) cuando la agregacion es aritmeticamente directa (una suma o un promedio simple), nunca una interpretacion nueva.
- Cuando un modulo fuente aun no existe en el MVP vigente o solo tiene cobertura parcial (por ejemplo MOD-010, MOD-012, MOD-014, MOD-016, MOD-018, MOD-025), su indicador se muestra como "no disponible en esta version" (regla G), nunca en cero, para no sugerir ausencia de riesgo donde en realidad falta el modulo.
- Toda vista respeta primero el filtro de permisos del rol (seccion C) y despues el filtro de perspectiva, cluster, etapa, sucursal/unidad o periodo elegido por el usuario (seccion D.1).

### M.2 Indicadores propios del Dashboard (meta-indicadores de la herramienta, no del programa de la empresa)

Analogos, en su naturaleza, a los que `MOD-025_ficha.md` define para la Busqueda Global: no miden el programa de proteccion de datos de la empresa cliente, miden el uso y la cobertura del propio Dashboard, y solo se muestran al Administrador.

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Cobertura de indicadores activos | Conteo de modulos con al menos un indicador disponible (no "no disponible en esta version") sobre el total de 26 modulos del mapa | Informativo, sin semaforo | Administrador |
| Fotos periodicas generadas a tiempo | Conteo de cierres mensuales Generados en la fecha programada, sobre el total de cierres programados en los ultimos 12 meses | Amarillo si hubo 1 cierre generado con retraso; rojo si hubo 2 o mas | Administrador |
| Reportes exportados en el periodo, por tipo | Conteo de exportaciones del Registro de exportacion (seccion D.4), agrupado por reporte | Informativo, sin semaforo | Administrador |
| Perspectiva mas consultada | Conteo de aperturas del Dashboard agrupado por perspectiva, en el periodo | Informativo, sin semaforo (mide adopcion, no cumplimiento) | Administrador |

### M.3 Estado del programa por etapa y por cluster (indicador propio de sintesis)

[opinion de producto, sin respaldo legal especifico para esta escala; disenado para cumplir el anti-feature 5 sin dejar de dar una sintesis util]. Para cada una de las 6 etapas del recorrido y para cada uno de los 8 clusters legales (seccion M.4), MOD-020 calcula un estado de sintesis en una escala de 5 valores, nunca un porcentaje:

| Estado | Que significa | Como se calcula (regla general, ajustable por tipo de modulo) |
|---|---|---|
| Sin iniciar | Ningun modulo de esa etapa o cluster tiene registros de negocio cargados | 0 registros de negocio activos en todos los modulos de la etapa/cluster |
| En configuracion | La empresa esta completando el alta basica, pero aun no hay operacion regular | Existen registros, pero menos de la mitad de las tareas asociadas de MOD-021 estan Completadas, o el diagnostico (MOD-004) aun no marco esa etapa/cluster como aplicable de forma definitiva |
| Operando | Hay actividad regular: tareas creandose y cerrandose, expedientes abriendose y cerrandose dentro de plazo | Mas de la mitad de las tareas de MOD-021 asociadas a esa etapa/cluster estan Completadas o En proceso, sin acumulacion de Vencidas |
| Con evidencia | Ademas de operar, existe evidencia disponible verificable (via MOD-019) para las obligaciones aplicables de esa etapa/cluster | El indicador "evidencia disponible por obligacion aplicable" de MOD-019 (seccion M.3, fila MOD-019) es Verde para las obligaciones OBLIGATORIO de esa etapa/cluster |
| Revisado | Ademas de lo anterior, existe una revision o auditoria formal reciente | Existe al menos un hallazgo de auditoria (MOD-018) cerrado, o una revision periodica confirmada (por ejemplo, revision del RAT o de un control), en los ultimos 12 meses, sobre esa etapa/cluster |

Este indicador de sintesis nunca reemplaza el detalle de la seccion M.3.1: es una vista de alto nivel para la perspectiva Gerencia, que siempre puede bajar al detalle por modulo. El texto de pantalla nunca dice "cumplimiento", dice "estado del programa": por ejemplo, "Relacion con terceros: Con evidencia" en vez de cualquier expresion de porcentaje.

### M.4 Vista alternativa por los 8 clusters legales

Mapeo de los 26 modulos del mapa definitivo a los 8 clusters legales de `propuesta_mapa_obligaciones.md`, seccion 1 (injerto del juez 3, adoptado por `06_mapa_definitivo_de_modulos.md`, seccion 3, ficha de MOD-020). La propuesta original definia estos clusters (con su propia numeracion de modulos, MOD-ORG, MOD-RAT, etc.) sobre 16 modulos "de proceso"; esta ficha traduce ese mapeo a los codigos definitivos del mapa actual (MOD-001 a MOD-026) y resuelve, de forma explicita, los casos que la propuesta original no cubria (ver nota al pie de la tabla y Nota final punto 3).

| Cluster legal | Modulos incluidos (codigo definitivo) |
|---|---|
| A. Nucleo organizativo | MOD-001 (Organizacion y Personas, incluye el submodulo Usuarios y Roles), MOD-002 (Delegado / Responsable Interno) |
| B. Entrada y hoja de ruta | MOD-003 (Onboarding), MOD-004 (Diagnostico de Cumplimiento), MOD-005 (Plan de Cumplimiento) |
| C. Registro y gobernanza | MOD-006 (RAT y Mapa de Datos), MOD-007 (Consentimiento), MOD-014 (Riesgos y EIPD), MOD-016 (Retencion y Eliminacion) |
| D. Relacion con el titular | MOD-011 (ARCO-POL), MOD-012 (Portal del Titular) |
| E. Relacion con terceros | MOD-009 (Proveedores y Encargados), MOD-010 (Transferencias Internacionales) |
| F. Gestion de crisis y control | MOD-013 (Incidentes de Seguridad), MOD-015 (Controles de Seguridad), MOD-017 (Capacitacion) |
| G. Documentacion | MOD-008 (Documentos y Politicas) |
| H. Relacion con la autoridad | MOD-024 (Centro Regulatorio, incluido el Procedimiento Sancionador y los Tramites ante la ACE) |

**Modulos fuera de los 8 clusters (nota de diseno, ver Nota final punto 3).** Los 6 modulos de la barra transversal (MOD-021 a MOD-026) y los dos modulos semi-transversales de la etapa Demostrar (MOD-018 Auditoria de Cumplimiento y MOD-019 Centro de Evidencias, ademas del propio MOD-020) no tienen una casilla propia en la tabla anterior: la propuesta original de los 8 clusters los agrupaba a todos, sin distincion, dentro de una unica categoria "I. Modulos transversales" (`propuesta_mapa_obligaciones.md`, seccion 1), mientras que el mapa definitivo ya saco a MOD-018 y MOD-019 de la barra transversal para ubicarlos en la etapa Demostrar (`06_mapa_definitivo_de_modulos.md`, seccion 4). Esta ficha resuelve esa diferencia asi: cuando el usuario filtra la vista Legal/Delegado por un cluster especifico, el panel muestra tambien, de forma cruzada, las tareas (MOD-021), la evidencia (MOD-019) y los hallazgos de auditoria (MOD-018) cuyo "modulo de origen" pertenece a alguno de los modulos de ese cluster, en vez de asignarle a MOD-018 o MOD-019 un cluster propio que no les corresponde con precision. Se recomienda a quien consolide el mapa final confirmar o ajustar este criterio (ver Nota final).

### M.3.1 Catalogo consolidado de indicadores por modulo fuente

Consolidado a partir de la seccion M de las 24 fichas ya redactadas (`awk '/^## M[.]/,/^## O[.]/' analisis/03_modulos/MOD-*.md`), en orden de codigo de modulo. La formula se resume de forma breve; el detalle completo (incluidos los umbrales exactos y las notas de opinion de producto) vive siempre en la seccion M de la ficha de origen, que esta tabla no reemplaza sino que indexa. MOD-026 (Centro de Ayuda) ya tiene ficha propia (`MOD-026_ficha.md`) y se integra en esta tabla como cualquier otro modulo fuente.

**MOD-001 Organizacion y Personas**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Usuarios activos vs invitados pendientes | Activos sobre total invitado | Verde/amarillo/rojo segun invitaciones vencidas | Gerencia, Administrador |
| Roles criticos sin titular | Roles criticos (Administrador, Delegado, Seguridad) sin usuario activo | Verde 0, amarillo 1, rojo 2+ | Gerencia, Legal, Administrador |
| Sucursales registradas | Conteo de sucursales ACTIVA | Informativo | Gerencia, Responsable de area |
| Separacion de funciones | Estado activada / recomendada no activada / no aplica | Verde si activada o bajo umbral; amarillo si no | Legal, Auditor, Gerencia |
| Ultimo cambio de estructura | Fecha del ultimo alta, baja o cambio de rol | Informativo | Auditor, Seguridad/IT |

**MOD-002 Delegado / Responsable Interno de Datos**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Estado del nombramiento | ACTIVO sin plazos vencidos | Verde/amarillo (plazo a 5 dias)/rojo (sin registro o plazo vencido) | Gerencia, Responsable |
| Dias habiles para la proxima obligacion | Minimo entre fechas limite del modulo, via MOD-023 | Colorea segun cercania | Responsable, Legal |
| Informes periodicos entregados vs minimo legal | Conteo ultimos 12 meses contra el minimo de 2 (Art. 30) | Si/no cumplido | Legal, Auditor |
| Estado regulatorio vigente | Badge ACTUAL / FUTURO desde MOD-024 | Informativo | Todas |
| Evidencia disponible del modulo | X de Y evidencias requeridas disponibles | Verde/amarillo/rojo | Auditor, Legal |
| Alertas activas del modulo | Conteo por nivel INFO/WARNING/HIGH/CRITICAL | Semaforo por nivel | Gerencia (HIGH/CRITICAL), Responsable (todas) |

**MOD-003 Onboarding**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Configuracion inicial completada | Estado del onboarding (NO_INICIADO/EN_PROGRESO/ABANDONADO/COMPLETADO) | Verde/amarillo/rojo segun antiguedad | Gerencia, Administrador |
| Aceptacion de invitaciones | Usuarios que aceptaron sobre total invitados | Verde 100%, amarillo dentro de plazo, rojo vencidas | Administrador, Auditor |
| Estado de la designacion del Delegado | Heredado de MOD-002 desde el Paso 4 del onboarding | Verde/amarillo/rojo | Legal/Delegado, Gerencia |
| Fecha y usuario de creacion de la organizacion | Dato directo del evento de auditoria | Informativo | Auditor |

**MOD-004 Diagnostico de Cumplimiento**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Diagnosticos completados vs organizaciones activas | Sesiones Cerradas sobre total de organizaciones con onboarding completo | Verde 100%, amarillo parcial, rojo sin iniciar | Gerencia, Administrador |
| Avance del diagnostico en curso | Preguntas respondidas sobre obligatorias visibles | Barra de progreso | Responsable |
| Acciones criticas abiertas generadas | Conteo de acciones criticas de la seccion E.1 no Completadas en MOD-021 | Rojo si mayor a 0 | Legal/Delegado, Gerencia |
| Acciones importantes y recomendadas abiertas | Igual, para esas dos categorias | Amarillo / gris | Responsable, Legal/Delegado |
| Nivel de madurez inicial de la organizacion | Regla de la seccion E.1 (Inicial/En desarrollo/En consolidacion) | Rojo/amarillo/verde | Gerencia, Legal/Delegado |
| Dias desde el ultimo diagnostico cerrado | Hoy menos fecha de cierre de la ultima sesion | Verde/amarillo/rojo segun ciclo configurado | Administrador, Delegado |

**MOD-005 Plan de Cumplimiento** (dependencia estructural de MOD-020)

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Avance del plan | Acciones Completada sobre total de la version Vigente | Verde >80%, amarillo 50-80%, rojo <50% | Gerencia, Responsable, Legal, Auditor |
| Acciones criticas pendientes o vencidas | Conteo de prioridad Critica no Completada | Rojo si hay Vencida, amarillo si Pendiente sin vencer | Gerencia, Responsable, Legal |
| Dias promedio de retraso de acciones vencidas | Promedio de dias de retraso sobre las Vencidas | Verde 0, amarillo <10 dias, rojo >=10 | Legal, Auditor |
| Acciones por modulo de ejecucion | Distribucion por modulo | Sin semaforo | Legal, Responsable de area |
| Vigencia de la version actual del plan | Fecha de aprobacion y version | Amarillo si +90 dias sin recalculo | Administrador, Delegado, Auditor |

**MOD-006 RAT y Mapa de Datos**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Cobertura del RAT | Fichas Vigentes sobre tratamientos detectados por el diagnostico | Verde >80%, amarillo 50-80%, rojo <50% | Gerencia, Responsable, Legal, Auditor |
| Tratamientos por base de licitud | Distribucion por base de licitud elegida | Sin semaforo | Legal, Delegado |
| Tratamientos con dato sensible | Conteo con al menos una categoria sensible | Amarillo/rojo segun cobertura de EIPD | Legal, Delegado, Gerencia |
| Fichas pendientes de revision periodica | Conteo en "Requiere revision" | Verde 0, amarillo 1-5, rojo >5 | Responsable, Delegado |
| Transferencias posiblemente no documentadas | Alertas de la regla G.5 sin resolver | Verde 0, rojo >0 | Delegado, Legal, Auditor |
| Sistemas sin pais confirmado | Conteo con pais pendiente de confirmar | Amarillo/rojo segun cantidad | Seguridad/IT, Delegado |
| Antiguedad promedio del RAT | Dias desde la ultima revision confirmada | Verde <180, amarillo 180-365, rojo >365 | Gerencia, Auditor |

**MOD-007 Consentimiento**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Consentimientos vigentes por finalidad | Conteo de Consent Vigente agrupado por finalidad | Informativo | Gerencia, Responsable, Legal |
| Cobertura de captura | Tratamientos con base Consentimiento que ya tienen Consent vigente | Verde 100%, amarillo pendientes recientes, rojo >15 dias | Responsable, Gerencia |
| Revocaciones dentro de plazo | Cerradas a tiempo sobre total cerradas en el periodo | Verde 100%, amarillo 1 caso, rojo 2+ | Legal, Auditor, Gerencia |
| Consentimientos sensibles/biometricos incompletos | Presentados sin firma por mas de 2 dias | Rojo si mayor a 0 | Responsable, Legal |
| Evidencia disponible | Consent/ConsentWithdrawal con snapshot y adjunto completos | Verde/amarillo/rojo | Auditor, Legal |

**MOD-008 Documentos y Politicas**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Documentos regulatorios obligatorios vigentes | Conteo de los 3 tipos con version PUBLICADO/VIGENTE sobre 3 | Verde 3/3, amarillo 1-2/3, rojo 0/3 | Gerencia, Responsable/Legal, Auditor |
| Documentos con revision pendiente | Conteo en REQUIERE_REVISION | Amarillo si hay alguno, rojo si +30 dias | Responsable/Legal, Gerencia |
| Tiempo promedio de aprobacion | Dias habiles EN_REVISION -> APROBADO | Sin semaforo | Gerencia, Legal |
| Ultima publicacion del Aviso de Privacidad | Fecha de la version vigente y dias transcurridos | Amarillo si supera el intervalo configurado | Responsable/Legal, Auditor |

**MOD-009 Proveedores y Encargados**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Proveedores activos (total y por tipo) | Conteo ACTIVO por Encargado/Receptor/Subencargado | Informativo | Gerencia, Responsable |
| Proveedores sin contrato/DPA vigente vinculado | PENDIENTE_DE_CONTRATO o contrato vencido | Rojo si mayor a 0 | Responsable, Legal/Compliance |
| Contratos por vencer en 30 dias | Conteo con vencimiento proximo | Amarillo | Responsable, Gerencia |
| Proveedores fuera de El Salvador sin transferencia vinculada | Conteo sin registro activo en MOD-010 | Rojo | Legal/Compliance, Auditor |
| Proveedores con revision periodica vencida | Conteo EN_REVISION con fecha superada | Amarillo <30 dias, rojo >=30 | Responsable, Auditor |
| Proveedores suspendidos por incidente | Conteo SUSPENDIDO | Rojo | Gerencia, Legal/Compliance, Seguridad/IT |
| Evidencia disponible por proveedor activo | % con contrato, riesgo y revision al dia | Verde/amarillo/rojo | Auditor |

**MOD-010 Transferencias Internacionales**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Transferencias activas registradas | Conteo ACTIVA | Informativo | Gerencia, Responsable/Legal, Auditor |
| Transferencias pendientes de confirmar | Conteo DETECTADA_PENDIENTE_DE_CONFIRMAR | Verde 0, amarillo 1-4, rojo 5+ | Responsable, Legal, Gerencia |
| Transferencias sin evaluacion de pais completa | Conteo EN_EVALUACION_DE_PAIS >10 dias habiles | Verde 0, amarillo 1-2, rojo 3+ | Legal, Auditor |
| Puestas en conocimiento a la ACE pendientes de envio | Conteo de ACEFiling no enviado | Verde 0, amarillo 1-2, rojo 3+ | Delegado, Legal |
| Contratos de transferencia vencidos o por vencer | Conteo por vencer o vencidos | Verde/amarillo/rojo | Legal, Seguridad/IT, Gerencia |
| Cobertura de evidencia de transferencias | % con expediente completo | Verde 90-100%, amarillo 70-89%, rojo <70% | Auditor, Legal, Gerencia |

**MOD-011 ARCO-POL** (contribuye al "dashboard basico": solicitudes)

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Solicitudes abiertas por estado | Distribucion de expedientes activos | Sin semaforo | Gerencia, Responsable |
| Solicitudes proximas a vencer | Menos del 25%/10% del plazo restante | Amarillo/rojo | Responsable, Legal/Delegado |
| Solicitudes vencidas | Plazo aplicable ya cumplido sin resolucion | Rojo si mayor a 0 | Gerencia, Legal/Delegado, Auditor |
| Tiempo promedio de resolucion | Dias habiles admision -> cierre | Verde/amarillo/rojo segun plazo general | Legal/Delegado, Auditor |
| Solicitudes resueltas dentro del plazo legal aplicable | % cerradas a tiempo | Verde/amarillo/rojo configurable | Gerencia, Legal/Delegado |
| Solicitudes con prevencion activa | Conteo en estado Prevenida | Sin semaforo | Responsable, Legal/Delegado |
| Reclamos ante la Direccion de Proteccion de Datos abiertos | Conteo sin informe remitido | Rojo si mayor o igual a 1 | Gerencia, Legal/Delegado, Auditor |
| Expedientes con evidencia completa vs incompleta | % checklist de evidencia esperada completo | Verde/amarillo/rojo | Auditor, Legal/Delegado |

**MOD-012 Portal del Titular**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Solicitudes recibidas por canal | Conteo con origen Portal sobre total del periodo | Informativo | Gerencia, Responsable ARCO-POL |
| Tiempo promedio hasta el primer triage | Horas envio -> apertura del expediente | Verde <1 dia habil, amarillo 1-2, rojo >2 | Responsable ARCO-POL, Legal |
| Tasa de intentos de verificacion fallidos | Fallidos sobre total de intentos | Verde <5%, amarillo 5-15%, rojo >15% | Seguridad/IT, Auditor |
| Disponibilidad del contenido publicado | Aviso/Politica mostrados = version vigente en MOD-008 | Verde al dia, rojo version vencida | Legal, Auditor |
| Cobertura de evidencia | % solicitudes del Portal con comprobante documentado en MOD-019 | Se muestra como evidencia disponible | Auditor |

**MOD-013 Incidentes de Seguridad**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Incidentes abiertos por severidad | Conteo Reportado a Remediacion por severidad | Verde sin Alta/Critica, amarillo 1+ Alta, rojo 1+ Critica | Gerencia, Responsable |
| Cronometros de 72h por vencer | Conteo con menos de 24 horas restantes | Amarillo <24h, rojo <6h | Responsable, Gerencia |
| Casos con notificacion enviada dentro de plazo (12 meses) | Ratio sobre casos con notificacion requerida | Dato de estado, sin umbral de cumplimiento | Legal, Auditor |
| Tiempo promedio de cierre | Promedio de dias Reportado -> Cierre | Informativo | Responsable, Gerencia |
| Incidentes por origen | Distribucion interno/proveedor/terceros | Informativo | Legal, Auditor |
| Expedientes con documentacion incompleta (OBL-INC-04) | Riesgo=Si con campos D.5 incompletos | Rojo si +72 horas en ese estado | Responsable, Legal |

**MOD-014 Riesgos y EIPD**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Tratamientos de alto riesgo evaluados | EIPD avanzadas sobre motivos de apertura detectados | Verde 1, amarillo si hay Detectado sin avanzar, rojo si vencida | Gerencia, Responsable, Legal, Auditor |
| EIPD vigentes | Conteo en estado VIGENTE | Informativo | Todas |
| EIPD pendientes de mitigacion (Alto/Critico) | Conteo EN_MITIGACION | Amarillo/rojo segun plazo de escalamiento | Gerencia, Responsable, Legal, Auditor |
| EIPD con revision atrasada | Conteo EN_REVISION con fecha vencida | Amarillo <30 dias, rojo >30 dias | Gerencia, Responsable/Delegado, Auditor |
| Distribucion por nivel de riesgo | Conteo Bajo/Medio/Alto/Critico | Semaforo por franja | Gerencia, Legal, Auditor |
| Controles pendientes originados en una EIPD | Conteo en MOD-015 con origen EIPD | Amarillo/rojo segun escalamiento | Seguridad/IT, Gerencia |

**MOD-015 Controles de Seguridad**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Controles con evidencia vigente | Implementado/Implementado con hallazgo sobre no archivados | Verde >=80%, amarillo 50-79%, rojo <50% | Gerencia, Seguridad/IT, Legal/Delegado, Auditor |
| Controles obligatorios sin evidencia o vencidos | Conteo OBL-SEG-01 a 06 pendiente o vencido | Rojo si mayor a 0 | Gerencia, Legal/Delegado, Seguridad/IT |
| Proximas revisiones (30 dias) | Conteo con revision proxima | Informativo | Seguridad/IT |
| Excepciones activas | Conteo No aplica-Exceptuado | Amarillo si hay pendientes de aprobar | Legal/Delegado, Aprobador, Gerencia |

**MOD-016 Retencion y Eliminacion**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Reglas de retencion activas | Conteo ACTIVO/PROXIMO A VENCER | Verde/amarillo/rojo segun SLA | Responsable, Legal |
| Eliminaciones pendientes de aprobacion | Conteo LISTO PARA ELIMINAR | Rojo si mayor a 0 y vencido el SLA | Legal, Gerencia, Responsable |
| Documentos de cumplimiento bajo retencion obligatoria | Conteo reglas documentales activas | Informativo | Auditor, Legal |
| Intentos bloqueados de eliminacion anticipada (90 dias) | Conteo eventos de la automatizacion G.13 | Rojo si mayor a 0 | Auditor, Gerencia |
| Cobertura del motor de retencion | X de Y tratamientos con regla definida | Conteo, sin semaforo de porcentaje | Responsable, Legal, Gerencia |

**MOD-017 Capacitacion**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Personal con capacitacion general vigente | X de Y personas con registro vigente | Amarillo si X<Y, rojo si hay Vencida | Gerencia, Delegado/Legal, Responsable de area, Auditor |
| Inducciones pendientes | Personas dadas de alta sin induccion completada | Rojo/amarillo segun plazo configurado | RRHH/Resp. de area, Delegado, Gerencia |
| Vencimientos proximos (30/60 dias) | Conteo Proxima a vencer | Amarillo, rojo si <5 dias | Delegado, Responsable de area |
| Estado del plan anual de capacitacion e induccion | Estado cruzado con la bandera regimen_reforma_659 | Verde/amarillo/rojo/gris (no aplica) | Delegado, Gerencia, Auditor |
| Capacitacion por rol cubierta | Personas con TrainingRecord por rol sobre total con ese rol | Amarillo/rojo segun brecha | Responsable de area, Delegado |

**MOD-018 Auditoria de Cumplimiento**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Estado de la ultima auditoria | Estado del ComplianceAudit mas reciente | Verde/amarillo/rojo segun ciclo anual | Gerencia, Legal/Delegado, Resp. Legal/Compliance, Auditor, Seguridad/IT |
| Dias desde el cierre de la ultima auditoria | Hoy menos fecha de cierre | Verde <300, amarillo 300-365, rojo >365 | Gerencia, Legal/Delegado |
| Hallazgos abiertos por severidad | Conteo Abierto/En correccion por severidad | Rojo si 1+ Critico | Legal/Delegado, Seguridad/IT, Gerencia |
| Acciones correctivas vencidas | Conteo con fecha limite pasada | Rojo si mayor a 0 | Legal/Delegado, Responsable de la accion, Gerencia |

**MOD-019 Centro de Evidencias** (dependencia estructural de MOD-020)

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Evidencia disponible por obligacion aplicable | % de obligaciones aplicables con Evidence Disponible | Verde 100% OBLIGATORIO, amarillo falta RECOMENDADO/CONDICIONAL, rojo falta OBLIGATORIO | Gerencia, Legal/Delegado, Auditor |
| Huecos de evidencia abiertos | Conteo Faltante por clasificacion | Rojo si 1+ OBLIGATORIO | Legal/Delegado, Gerencia, Auditor |
| Evidencia vencida o por vencer | Conteo Vencida mas proximos 30 dias | Rojo/amarillo | Seguridad/IT, Legal/Delegado, Gerencia |
| Paquetes de evidencia generados en el periodo | Conteo EvidencePackage Exportado por tipo | Informativo | Legal/Delegado, Auditor, Gerencia |
| Tiempo promedio de aprobacion de evidencia manual | Promedio dias En revision -> Disponible | Verde <5, amarillo 5-10, rojo >10 | Legal/Delegado, Administrador |

**MOD-021 Centro de Tareas** (dependencia estructural de MOD-020)

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Tareas pendientes | Pendiente + En proceso + Bloqueada | Verde/amarillo/rojo segun promedio historico | Responsable, Gerencia, Legal |
| Tareas vencidas | Conteo con bandera Vencida | Rojo si mayor a 0 | Gerencia, Responsable, Legal, Auditor |
| Aprobaciones pendientes | Conteo sin Decision, por dias en espera | Amarillo >3 dias, rojo >5 dias | Aprobador, Delegado/Resp. interno, Gerencia |
| Tiempo promedio de cierre por tipo de tarea | Promedio dias creacion -> completada | Sin semaforo | Legal, Gerencia |
| Cumplimiento de plazos operativos con plazo legal | % completadas dentro de la fecha limite | Verde >=95%, amarillo 80-94%, rojo <80% | Gerencia, Legal, Auditor |
| Tareas archivadas por cambio de regimen | Conteo acumulado desde la activacion de FUTURO | Informativo | Delegado/Resp. interno, Legal, Auditor |
| Carga de trabajo por responsable | Conteo de tareas activas por usuario | Amarillo si supera el umbral configurado | Administrador, Gerencia |

**MOD-022 Notificaciones**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Notificaciones CRITICAL pendientes de acuse | Conteo Leida/Entregada CRITICAL sin Acuse | Rojo si mayor a 0 | Gerencia, Delegado/Resp. interno, Legal/Compliance, Auditor |
| Notificaciones escaladas en el periodo | Conteo con bandera Escalada por familia | Amarillo/rojo segun promedio historico | Gerencia, Administrador |
| Tasa de entrega fallida | Fallida tras reintentos sobre total enviado | Verde <1%, amarillo 1-5%, rojo >5% | Administrador |
| Tiempo promedio de acuse en CRITICAL | Promedio entre entrega/lectura y acuse | Sin semaforo | Legal, Gerencia, Auditor |
| Notificaciones agrupadas vs individuales | Proporcion en resumen sobre el total | Informativo | Administrador |
| Roles criticos sin titular activo | Conteo de reglas con destinatario resuelto vacio | Rojo si mayor a 0 | Gerencia, Administrador, Auditor |

**MOD-023 Calendario y Motor de Plazos**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Calendario del anio en curso y del proximo anio | Estado de la version (Vigente/Publicado/Borrador) | Verde/amarillo/rojo segun antelacion | Administrador, Gerencia, Auditor |
| Plazos legales actualmente en curso | Conteo por modulo de origen | Informativo | Gerencia, Delegado/Resp. interno, Legal |
| Plazos vencidos sin cerrar | Conteo con bandera Vencido | Rojo si mayor a 0 | Gerencia, Delegado/Resp. interno, Auditor |
| Recalculos aplicados (12 meses) | Conteo de eventos de recalculo | Informativo | Legal/Compliance, Auditor |
| Cobertura de fuente verificada en asuetos locales | % sucursales con fuente verificada en 24 meses | Verde 100%, amarillo 80-99%, rojo <80% | Administrador, Auditor |
| Casos con criterio de computo ambiguo en su valor alternativo | Conteo de cambios de criterio por defecto | Amarillo si mayor a 0 | Legal/Compliance, Delegado/Resp. interno, Auditor |

**MOD-024 Centro Regulatorio**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Estado regulatorio vigente | Badge ACTUAL/FUTURO con fecha del ultimo cambio | Informativo | Todas |
| Actualizaciones normativas pendientes de revision | Conteo de tareas "Revisar cambio normativo" no completadas | Verde 0, amarillo 1-2, rojo 3+ | Administrador, Delegado/Resp. Interno, Responsable Legal |
| Procedimientos sancionadores activos | Conteo distinto de CERRADO/PRESCRITO_ARCHIVADO | Rojo si hay uno con plazo vencido | Gerencia, Responsable Legal, Auditor |
| Dias habiles para la proxima obligacion del expediente sancionador activo | Minimo entre fechas limite del expediente | Colorea segun cercania | Responsable Legal, Administrador |
| Tramites ante la ACE pendientes de envio | Conteo BORRADOR/PENDIENTE_DE_ENVIO | Amarillo tras 15 dias, rojo tras 30 | Delegado/Resp. Interno, Administrador, Legal |
| Evidencia disponible del modulo | X de Y evidencias requeridas disponibles | Verde/amarillo/rojo | Auditor, Legal |
| Historial de sanciones y apercibimientos (RECOMENDADO) | Conteo acumulado de expedientes cerrados con sancion | Informativo | Legal, Auditor, Gerencia |
| Alertas activas del modulo | Conteo por nivel INFO/WARNING/HIGH/CRITICAL | Semaforo por nivel | Gerencia (HIGH/CRITICAL), Responsable Legal (todas) |

**MOD-025 Busqueda Global.** No aporta indicadores de estado del programa al Dashboard principal (segun su propia ficha, seccion M): sus 3 indicadores (consultas ejecutadas, proporcion sin resultados, volumen de consultas en ambito sensible) son de gestion interna de la propia busqueda y se muestran unicamente al Administrador, nunca en las 4 perspectivas de MOD-020.

**MOD-026 Centro de Ayuda**

| Indicador | Formula (resumen) | Semaforo | Perspectiva |
|---|---|---|---|
| Articulos de ayuda consultados en el periodo | Conteo de aperturas de la tarjeta de ayuda o del Glosario, agregado por modulo | Sin semaforo (dato informativo de adopcion, no de riesgo) | Responsable (Administrador), Gerencia |
| Articulos marcados para revision pendientes | Conteo de HelpArticle en estado MARCADO_PARA_REVISION | Verde 0, amarillo 1-3, rojo mas de 3 | Legal/Delegado, Auditor |
| Utilidad percibida del contenido | Votos "util" sobre el total de votos "util" mas "no fue util", por cien; se muestra siempre acompanada de la aclaracion de que mide la claridad del texto de ayuda, no el cumplimiento legal de la empresa | Verde 80% o mas, amarillo 60-79%, rojo menos de 60% | Responsable (Administrador), Gerencia |
| Casos con sugerencia de asesoria juridica en el periodo | Conteo de tareas "Evaluar necesidad de asesoria externa" creadas por la automatizacion propia del modulo | Sin semaforo (dato informativo de riesgo acumulado, util para planificar presupuesto de asesoria) | Legal/Delegado, Gerencia |

Al igual que en MOD-025, ninguno de estos cuatro indicadores mide el estado del programa de proteccion de datos de la empresa cliente: miden uso y calidad del contenido de ayuda (`MOD-026_ficha.md`, seccion M), por lo que no aparecen en la sintesis por etapa o por cluster de la seccion M.3, solo en el catalogo consolidado de este apartado.

---

## N. Reportes

Igual que en la seccion M, esta seccion tiene una parte propia (N.1, los reportes que solo MOD-020 puede producir porque combinan varios modulos) y una parte consolidada (N.2 y N.3), que indexa los reportes que cada modulo ya define en su propia seccion N.

### N.1 Reportes propios de MOD-020

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Informe gerencial consolidado | Sintesis del estado del programa por las 6 etapas del recorrido y por los 8 clusters legales (seccion M.3), indicadores criticos de cada modulo MUST HAVE, avance del Plan de Cumplimiento (MOD-005) | Por etapa, por cluster, por periodo o foto mensual | PDF | Gerencia, Administrador | Si, como pieza de sintesis del paquete general |
| Informe para Junta Directiva | Version ejecutiva del informe gerencial, pensada para un destinatario que no usa el sistema dia a dia: menos detalle operativo, mas enfasis en riesgos criticos, avance del plan y proximos hitos regulatorios (por ejemplo, la reforma 659) | Por periodo (tipicamente trimestral o semestral) | PDF | Junta Directiva (destinatario externo al sistema, ver seccion B) | Si |
| Enlace al paquete de evidencia para la ACE | Referencia al paquete que arma MOD-019 (paquete de evidencia general o paquete de preparacion de inspeccion, segun corresponda), con su fecha de generacion, alcance y estado, sin duplicar su contenido | Por tipo de paquete, por fecha de generacion | Enlace mas metadatos (el archivo en si es el que ya genera MOD-019) | Delegado/Responsable interno, Legal/Compliance, Administrador | Si (por remision directa al paquete de MOD-019) |
| Reporte comparativo de tendencia (fotos periodicas) | Evolucion de los indicadores de la seccion M.3 entre dos o mas cierres mensuales elegidos | Por rango de fechas, por modulo o cluster | PDF, XLSX | Gerencia, Legal/Delegado, Auditor | Si |
| Exportacion de la vista de Dashboard vigente | Fotografia en PDF de la pantalla tal como la ve el usuario en el momento de exportar, con sus filtros aplicados | Los mismos filtros de la seccion D.1 | PDF | El usuario que exporta, para compartir puntualmente | No (a menos que se use como respaldo puntual; no sustituye al paquete de MOD-019) |

### N.2 Los 7 reportes minimos del area 28, mas Junta Directiva y el enlace a la ACE

El area 28 del prompt de analisis funcional exige, como minimo, reportes gerencial, ARCO-POL, incidentes, proveedores, RAT, auditoria y seguridad. Ninguno de estos siete se duplica desde cero en MOD-020: cada uno ya existe, con mayor detalle, en la seccion N de su modulo de origen; el rol de MOD-020 es ofrecer un unico punto de entrada donde encontrarlos todos, ademas de dos reportes que si son exclusivos de este modulo (Informe para Junta Directiva y el enlace al paquete para la ACE, ya descritos en N.1).

| Reporte minimo del area 28 | Se satisface con (modulo y reporte de origen) |
|---|---|
| Gerencial | Informe gerencial consolidado (N.1, propio de MOD-020), que a su vez agrega el Plan de Cumplimiento vigente y el Plan de adecuacion de MOD-005 |
| ARCO-POL | Reporte de solicitudes ARCO-POL y Estadisticas ARCO-POL para el informe periodico del Delegado, ambos de MOD-011 |
| Incidentes | Listado de incidentes del periodo y Reporte de cumplimiento de plazos de notificacion, ambos de MOD-013 |
| Proveedores | Listado de proveedores/encargados y Reporte de vencimientos, ambos de MOD-009 |
| RAT | RAT consolidado y RAT de datos sensibles, ambos de MOD-006 |
| Auditoria | Informe de auditoria anual y Plan de accion exportable, ambos de MOD-018; complementado por el Historico de exportaciones de MOD-020 mismo (ver N.3) |
| Seguridad | Checklist de controles de seguridad y Reporte de excepciones y justificaciones, ambos de MOD-015 |
| (adicional, no exigido como "minimo" por el area 28 pero exigido por el enfoque especifico de esta tarea) Informe para Junta Directiva | Reporte propio de MOD-020 (N.1) |
| (adicional) Enlace al paquete para la ACE | Reporte propio de MOD-020 (N.1), que remite al paquete armado por MOD-019 |

### N.3 Catalogo consolidado de reportes por modulo fuente

Consolidado a partir de la seccion N de las 24 fichas ya redactadas. El contenido se resume de forma breve; el detalle completo (todas las columnas exactas de cada reporte) vive en la seccion N de la ficha de origen.

| Modulo fuente | Reportes (nombre resumido) | Formato tipico | Destinatario tipico | Integra paquete de evidencia |
|---|---|---|---|---|
| MOD-001 | Listado de usuarios y roles vigentes; Ficha de organizacion; Historial de cambios de estructura | PDF, XLSX, CSV | Auditor, Administrador, Gerencia | Si (control de acceso) |
| MOD-002 | Ficha del responsable del programa de datos; Bitacora de plazos del Delegado; Paquete de evidencia del Delegado; Informe de gestion periodico del Delegado | PDF, XLSX, ZIP | Auditoria interna, Gerencia, Junta Directiva | Si |
| MOD-003 | Resumen de configuracion inicial; Historial de invitaciones y aceptaciones | PDF, CSV/XLSX | Administrador, Auditor | Si |
| MOD-004 | Resultado del diagnostico; Historial comparativo de diagnosticos; Detalle de disparadores activados | PDF, XLSX, CSV | Administrador, Delegado, Legal/Compliance, Auditor | Si |
| MOD-005 | Plan de Cumplimiento vigente; Plan de adecuacion; Acciones vencidas; Historial de recalculos del plan | PDF, XLSX | Administrador, Delegado, Legal, Auditor, ACE si se requiere | Si |
| MOD-006 | RAT consolidado; RAT de datos sensibles; Mapa de Datos exportado; Reporte de transferencias no documentadas; Historial de cambios; Paquete de evidencia del RAT | PDF, XLSX/CSV | Delegado, Legal, Gerencia, Auditor | Si |
| MOD-007 | Consentimientos vigentes; Revocaciones procesadas; Expediente individual de consentimiento; Consentimientos sensibles y biometricos | XLSX, CSV, PDF | Responsable, Legal, Gerencia, Auditor | Si |
| MOD-008 | Inventario de documentos regulatorios; Historial de versiones; Paquete de evidencia documental; Checklist de contenido minimo del Aviso | PDF, XLSX, ZIP | Gerencia, Auditor, ACE | Si |
| MOD-009 | Listado de proveedores/encargados; Reporte de vencimientos; Paquete de evidencia de un proveedor; Reporte de transferencias derivadas | XLSX, CSV, PDF, ZIP | Delegado, Auditor, Responsable de area | Si (salvo el reporte de vencimientos, de uso interno) |
| MOD-010 | Listado de transferencias; Expediente individual; Paquete de evidencia de transferencias; Pendientes o con riesgo abierto; Registro de puestas en conocimiento a la ACE | XLSX, CSV, PDF, ZIP | Legal, Auditor, Delegado, Gerencia | Si (salvo el listado y el reporte de pendientes, de uso interno) |
| MOD-011 | Reporte de solicitudes ARCO-POL; Estadisticas para el informe del Delegado; Paquete de evidencia de un expediente; Reporte de reclamos ante la ACE; Reporte de tarifas cobradas | PDF, XLSX, ZIP | Delegado, Gerencia, Auditor, Legal | Si |
| MOD-012 | Solicitudes recibidas por el Portal; Accesos y verificaciones del Portal; Constancia de mecanismo operativo | XLSX, CSV, PDF | Responsable ARCO-POL, Seguridad/IT, Auditor, Delegado, Gerencia | Si |
| MOD-013 | Listado de incidentes del periodo; Expediente individual; Reporte de cumplimiento de plazos de notificacion; Reporte de incidentes por proveedor; Paquete de evidencia para auditoria anual | PDF, XLSX, CSV, ZIP | Gerencia, Legal, Auditor, Responsable de Proveedores | Si (salvo el listado del periodo, gerencial) |
| MOD-014 | Listado de EIPD; Expediente EIPD individual; Reporte de riesgos por nivel; Reporte de mitigaciones y controles pendientes; Paquete de evidencia de una EIPD | PDF, XLSX, ZIP | Delegado, Gerencia, Auditor, ACE si se requiere, Seguridad/IT | Si |
| MOD-015 | Checklist de controles de seguridad; Reporte de excepciones y justificaciones; Paquete de evidencia de seguridad; Historial de cambios de un control | PDF, XLSX, ZIP, CSV | Seguridad/IT, Delegado, Gerencia, Legal, Auditor | Si |
| MOD-016 | Inventario de reglas de retencion; Historial de eliminaciones; Excepciones y eliminaciones anticipadas; Reglas sin fundamento sectorial confirmado | PDF, XLSX, CSV, ZIP | Delegado, Gerencia, Auditor, ACE | Si (salvo el ultimo, de gestion interna) |
| MOD-017 | Listado de capacitaciones por persona; Historial por area o rol; Plan anual de capacitacion; Vencimientos e inducciones pendientes | PDF, XLSX, CSV | RRHH, Delegado, Auditor, Gerencia, ACE si la requiere | Si (salvo vencimientos, de gestion interna) |
| MOD-018 | Informe de auditoria anual; Plan de accion exportable; Historico de auditorias; Paquete de evidencia de la auditoria | PDF, XLSX, CSV, ZIP | Gerencia, Auditor externo, ACE, Legal/Delegado, Seguridad/IT | Si |
| MOD-019 | Informe de brecha de evidencia; Paquete de evidencia general; Paquete para auditoria anual; Paquete para procedimiento sancionador; Paquete de preparacion de inspeccion; Historico de exportaciones | XLSX, PDF, ZIP, CSV | Delegado, Gerencia, Auditor, ACE, Legal/Compliance | Si (salvo el informe de brecha, que orienta antes de generar el paquete) |
| MOD-021 | Listado de tareas; Tareas vencidas; Historial de una tarea; Historial de aprobaciones; Carga de trabajo; Paquete de tareas archivadas por cambio de regimen | XLSX, CSV, PDF, ZIP | Administrador, Delegado, Legal/Compliance, Gerencia, Auditor | Si (salvo carga de trabajo, de uso interno) |
| MOD-022 | Listado de notificaciones; Notificaciones CRITICAL con su acuse; Historial de una notificacion; Entregas fallidas y reintentos; Configuracion vigente de reglas | XLSX, CSV, PDF | Administrador, Delegado, Legal/Compliance, Auditor, Gerencia | Si (salvo entregas fallidas, de uso interno) |
| MOD-023 | Calendario oficial vigente por anio; Historial de calculos de plazo; Historial de recalculos; Registro de cambios de criterio de computo; Paquete de evidencia de un calculo | PDF, XLSX, CSV, ZIP | Administrador, Delegado, Legal/Compliance, Auditor | Si |
| MOD-024 | Marco normativo vigente; Catalogo de infracciones y multas; Bitacora de actualizaciones normativas; Expediente completo de un Procedimiento Sancionador; Registro de tramites ante la ACE; Historial del regimen de la reforma 659 | PDF, XLSX, CSV, ZIP | Gerencia, Legal, Auditor, Auditoria interna, ACE | Si |
| MOD-025 | Registro agregado de consultas en ambito sensible; Catalogo de sinonimos vigente | XLSX, CSV | Administrador, Auditor interno, equipo de producto | No (son reportes de gestion interna del buscador, no del programa de proteccion de datos) |
| MOD-026 | Catalogo completo de articulos de ayuda; Reporte de retroalimentacion y confusion; Uso de la ayuda por modulo | CSV, PDF | Equipo de contenido del producto; Auditor y Gerencia para el uso por modulo | No (salvo el catalogo de articulos, que puede adjuntarse como material de referencia complementario si la organizacion lo decide; ninguno de los tres es evidencia de una obligacion propia, ver `MOD-026_ficha.md`, seccion N) |

---

## O. Historial

Eventos que quedan en el registro tecnico de MOD-020 y en el AuditLog transversal (MOD-020 no tiene un historial de "cambios de campo" de un registro de negocio propio, porque no posee esa entidad; se limita a los eventos tecnicos propios del modulo, igual que MOD-025):

- Cada exportacion de un reporte (seccion N): usuario, fecha y hora, reporte, filtros aplicados, formato.
- Cada generacion de una foto periodica (cierre mensual): fecha, si fue automatica o manual, y el motivo si fue manual (seccion D.3).
- Cambios a la configuracion de umbrales de semaforo, catalogo de sucursales/unidades a efectos del Dashboard, o al calendario de cierres mensuales: quien lo cambio, el valor anterior y el nuevo.
- Acceso a una perspectiva o a un reporte marcado con nivel de confidencialidad reforzado (por ejemplo, la exportacion del Informe para Junta Directiva) por un rol distinto del habitual (Administrador o Delegado/Responsable interno), igual que MOD-021 y MOD-025 registran el acceso de segundo nivel a sus propios contenidos sensibles.
- Cada vez que se enlaza o se consulta el paquete de evidencia para la ACE desde este modulo (sin registrar el contenido del paquete en si, que ya audita MOD-019 por su cuenta).

---

## P. Riesgos

- **Riesgo legal: que un indicador o una combinacion de indicadores del Dashboard se lea como una afirmacion de cumplimiento legal.** Es el riesgo central que motiva el anti-feature 5 y toda la seccion H de esta ficha. *Mitigacion de diseno*: ningun texto de pantalla usa la palabra "cumplimiento" junto a un numero o porcentaje; se usa siempre "estado del programa", "controles configurados", "tareas pendientes" o "evidencia disponible" (`04_objetivo_exacto_del_producto.md`, seccion 1.2), y el banner general de descargo (seccion 1.3 del mismo documento) es visible en el Dashboard principal, tal como el propio maestro lo describe en su seccion 31.
- **Riesgo legal: que el indicador de "estado del programa" por etapa o por cluster (seccion M.3) se use como sustituto de una opinion juridica sobre riesgo real.** *Mitigacion de diseno*: el indicador se declara explicitamente como sintesis operativa [opinion de producto], nunca como una conclusion sobre la exposicion legal de la empresa; el texto de ayuda contextual (seccion R) lo explica y remite a asesoria especializada cuando corresponda.
- **Riesgo de UX: sobrecarga de informacion para un usuario no especialista que entra por primera vez.** Con indicadores de 23 modulos distintos, una vista sin jerarquia puede abrumar a alguien como Karla (perfil pyme de `05_tipos_de_usuario.md`). *Mitigacion de diseno*: la perspectiva por defecto (segun el rol, seccion B) muestra primero los indicadores de mayor severidad (rojos) y el resumen por etapa/cluster (seccion M.3), dejando el detalle exhaustivo del catalogo (M.3.1) accesible pero no como pantalla de entrada.
- **Riesgo de UX: que la vista alternativa por los 8 clusters legales confunda a un usuario que ya aprendio a navegar por las 6 etapas del recorrido.** *Mitigacion de diseno*: la vista por clusters es opcional y esta acotada a la perspectiva Legal/Delegado (seccion D.1); las demas perspectivas siempre usan las 6 etapas, que son el criterio de navegacion principal de todo el sistema (`06_mapa_definitivo_de_modulos.md`, seccion 2, principio 1).
- **Riesgo operativo: que un indicador quede desactualizado o incorrecto por un error en su modulo fuente, y que el Dashboard "hereda" ese error sin que nadie lo note en el lugar correcto.** *Mitigacion de diseno*: MOD-020 nunca recalcula el valor de un indicador (seccion M.1); si el valor es incorrecto, el error se corrige en el modulo fuente y se refleja aqui de inmediato, sin necesidad de un mecanismo de correccion separado en el Dashboard.
- **Riesgo operativo: que la foto periodica (cierre mensual) no se genere por una falla tecnica, y que la tendencia quede con un hueco sin que nadie lo note.** *Mitigacion de diseno*: el indicador propio de la seccion M.2 ("fotos periodicas generadas a tiempo") hace visible ese hueco al Administrador, y el estado "Programada" del snapshot (seccion F.2) queda visible hasta que se resuelve.
- **Riesgo de seguridad y privacidad: que un indicador o un reporte exponga, sin querer, un dato personal de un titular.** Por ejemplo, un reporte mal filtrado que muestre el nombre de un titular en vez de solo el conteo de solicitudes. *Mitigacion de diseno*: la regla de minimizacion de la seccion D.4 (todo indicador es un agregado, nunca un dato individual) y el hecho de que todo reporte con contenido detallado proviene, sin alteracion de sus reglas de minimizacion, del modulo de origen que ya las define (por ejemplo, MOD-011 nunca expone el nombre completo del titular fuera de su propio expediente, ver `MOD-011_ficha.md`).
- **Riesgo de seguridad: que un rol vea, a traves del drill-down, un registro que su propio modulo de origen le negaria si lo buscara directamente.** *Mitigacion de diseno*: el filtro de permisos se aplica siempre antes que el filtro de perspectiva o cluster (seccion C y seccion D.4, punto 2), exactamente con la misma regla de "no revelar existencia" que ya define `MOD-025_ficha.md` para la Busqueda Global.
- **Riesgo operativo: que el filtro por "sociedad" (seccion D.1) se active antes de que el MVP soporte realmente varias sociedades, generando expectativas de una capacidad que aun no existe.** *Mitigacion de diseno*: el campo queda modelado pero explicitamente inactivo mientras la organizacion tenga una sola sociedad dada de alta (ver Nota final punto 2), sin mostrarse como opcion de filtro cuando no aplica.

---

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Dashboard basico por perspectiva (Gerencia, Responsable, Legal/Delegado, Auditor) con los indicadores de "pendientes, vencidos, tratamientos, solicitudes" | X | | | | Es la justificacion explicita de MUST HAVE de la propia entrada de MOD-020 en `mapa_modulos.json`; sin esto el producto no cumple su promesa de dar una vision general desde el primer dia |
| Indicadores agregados desde MOD-005, MOD-019 y MOD-021 (dependencia estructural minima) | X | | | | Son los tres modulos MUST HAVE de los que depende la version minima (seccion L); sin ellos no hay avance del plan, evidencia disponible ni tareas que mostrar |
| Filtro por sucursal o unidad, y drill-down al registro fuente respetando permisos | X | | | | Sin drill-down el Dashboard es solo una foto sin accion posible; el enfoque especifico de esta tarea lo exige de forma explicita ("cada indicador permite bajar al registro fuente respetando permisos") |
| Regla de minimizacion (nunca datos personales de titulares en el Dashboard) y prohibicion de lenguaje de cumplimiento legal | X | | | | No postergable desde el primer dia: es la instrumentacion directa de dos anti-features centrales (items 5 y 8 de `22_anti_features.md`) |
| Toda exportacion queda en el AuditLog, con verificacion de integridad via MOD-019 | X | | | | Cierra el anti-feature 25 (integridad de toda exportacion); sin esto ningun reporte de este modulo es verificable despues |
| Catalogo consolidado de indicadores de los modulos MUST HAVE (seccion M.3.1, filas de MOD-001 a MOD-009, MOD-011, MOD-013, MOD-015, MOD-017, MOD-019, MOD-021 a MOD-024, MOD-026) | X | | | | Estos son los modulos MUST HAVE del mapa definitivo; sus indicadores deben estar disponibles desde el primer dia |
| Estado del programa por etapa y por cluster (seccion M.3, sintesis de alto nivel) | | X | | | Mejora de comprension para Gerencia sobre datos que ya existen en el detalle MUST HAVE; el detalle por modulo ya cubre la necesidad minima sin esta capa de sintesis |
| Vista alternativa por los 8 clusters legales | | X | | | Injerto de un solo juez, no parte de la propuesta ganadora original; util para el rol Legal/Delegado, pero la navegacion por las 6 etapas (MUST HAVE) ya cubre la necesidad de encontrar informacion |
| Fotos periodicas (cierres mensuales) y reporte comparativo de tendencia | | X | | | Util desde el inicio, pero el mismo resultado puede obtenerse revisando manualmente el Dashboard en distintos momentos mientras no exista el snapshot automatico; no es dependencia estructural de otro MUST HAVE |
| Reportes exportables avanzados por area (los 7 minimos del area 28, seccion N.2) mas alla del listado basico ya MUST HAVE en cada modulo de origen | | X | | | Cada modulo de origen ya exporta su propio reporte MUST HAVE (por ejemplo, RAT consolidado en MOD-006); lo que se difiere es la conveniencia de encontrarlos todos consolidados desde MOD-020, no la existencia del reporte en si |
| Informe gerencial consolidado e Informe para Junta Directiva | | X | | | Valor claro para clientes con Junta Directiva formal (perfil corporativo de `05_tipos_de_usuario.md`), pero no bloquea la operacion de una pyme sin ese organo, que puede seguir usando el Dashboard basico |
| Enlace al paquete de evidencia para la ACE | | X | | | Depende de que MOD-019 tenga su paquete de evidencia general ya armado; el enlace en si es de bajo costo, pero no urgente mientras la ACE no abra un requerimiento activo |
| Indicadores de indicadores no disponibles como "no disponible en esta version" para modulos SHOULD/COULD HAVE aun sin construir | | X | | | Mejora de claridad de UX sobre una version que ya podria mostrar simplemente ausencia de datos; no bloquea la utilidad basica del Dashboard |
| Personalizacion completa de umbrales de semaforo por la empresa, para cada uno de los mas de 100 indicadores del catalogo | | | X | | Los umbrales por defecto de cada modulo fuente (documentados en su propia seccion M) cubren el caso general; la personalizacion exhaustiva es una mejora posterior |
| Vista consolidada multi-sociedad del Dashboard (filtro por sociedad activo) | | | | X | Coincide con la decision de alcance 2.7.31 de `02_validacion_de_la_idea.md`: el MVP no soporta grupos multi-sociedad; el filtro por sociedad de esta ficha queda listo pero inactivo hasta esa capacidad (ver Nota final punto 2) |
| Meta-indicadores de uso del propio Dashboard (perspectiva mas consultada, etc.) mas alla de la cobertura basica de fotos mensuales | | | X | | Util para el equipo de producto, no para el programa de proteccion de datos de la empresa cliente; no aporta valor legal ni operativo directo |

**Version minima vendible del modulo.** La version minima que ya puede venderse es el Dashboard basico por las 4 perspectivas, con los indicadores de MOD-005 (avance del plan), MOD-019 (evidencia disponible) y MOD-021 (tareas pendientes y vencidas) mas los indicadores de los demas modulos MUST HAVE ya construidos al momento del lanzamiento, filtrado por sucursal/unidad, con drill-down respetando permisos, sin lenguaje de cumplimiento legal y con toda exportacion verificable via MOD-019. Esto ya resuelve la pregunta central que motiva este modulo (como vamos, desde cualquier perspectiva) y es coherente con la propia clasificacion MUST HAVE del mapa definitivo, que reserva explicitamente los reportes avanzados y la vista por clusters para una version posterior dentro del mismo modulo.

---

## R. Ayuda contextual (complemento obligatorio)

**1. Que es el Dashboard**

- *Que es*: la pantalla principal que le muestra, de un vistazo, en que esta su programa de proteccion de datos: pendientes, vencidos, tratamientos registrados, solicitudes abiertas, y mas, segun el punto de vista (perspectiva) desde el que lo mire.
- *Por que tengo que hacer esto*: para no tener que revisar cada modulo por separado cada vez que alguien le pregunte "como vamos".
- *Fundamento*: no tiene un fundamento legal propio; es la instrumentacion funcional del area 26 del prompt de analisis funcional y de la seccion 31 del documento maestro (hipotesis de producto, aqui convertida en diseno).
- *Cuando necesito ayuda juridica*: nunca por usar el Dashboard en si; si un indicador le genera una duda legal sobre que hacer, esa duda se resuelve en el modulo de origen del indicador, no aqui.

**2. Que significa "estado del programa" (y por que nunca vera un porcentaje de cumplimiento legal)**

- *Que es*: una forma de describir donde esta su empresa en su proceso de proteccion de datos (por ejemplo, "sin iniciar", "en configuracion", "operando", "con evidencia" o "revisado"), sin afirmar que su empresa "cumple" o "no cumple" con la ley.
- *Por que tengo que hacer esto*: porque solo un abogado o su Delegado, revisando su caso concreto, puede decir si su empresa cumple la ley; el sistema solo puede mostrarle que tan avanzado esta su trabajo de organizacion, documentacion y evidencia.
- *Fundamento*: anti-feature 5 de `22_anti_features.md` y seccion 1.2 de `04_objetivo_exacto_del_producto.md`: el sistema nunca declara un porcentaje de cumplimiento legal.
- *Cuando necesito ayuda juridica*: siempre que quiera saber si el estado que ve equivale a estar "en regla" con la ley; esa conclusion requiere criterio de su Delegado o de asesoria especializada.

**3. Que son los 8 clusters legales (vista alternativa a las 6 etapas)**

- *Que es*: una segunda forma de organizar la informacion del Dashboard, agrupando los modulos por tema legal (por ejemplo, "Relacion con terceros" agrupa Proveedores y Transferencias) en vez de por el orden en que normalmente se usa el sistema.
- *Por que tengo que hacer esto*: es util para el Delegado o para Legal/Compliance cuando necesita revisar un tema legal completo (por ejemplo, todo lo relacionado con la autoridad) sin importar en que etapa del recorrido vive cada modulo.
- *Fundamento*: no corresponde a un OBL-ID especifico; es una clasificacion de producto tomada de `propuesta_mapa_obligaciones.md`, adoptada como vista alternativa por `06_mapa_definitivo_de_modulos.md`, seccion 3, ficha de MOD-020.
- *Cuando necesito ayuda juridica*: no aplica directamente a la vista en si; si un cluster completo muestra muchos indicadores en rojo, consulte a su Delegado para priorizar por donde empezar.

**4. Que es una foto periodica (cierre mensual)**

- *Que es*: una copia guardada de como estaban todos los indicadores en una fecha especifica de cada mes, para poder comparar como ha cambiado su programa con el tiempo.
- *Por que tengo que hacer esto*: para ver tendencias (por ejemplo, si las solicitudes ARCO-POL vencidas estan aumentando o disminuyendo mes a mes) en vez de solo ver el dato de hoy.
- *Fundamento*: no corresponde a un OBL-ID especifico; es una buena practica de gestion definida para este modulo (seccion D.3), util ademas como evidencia de que el estado mostrado en un momento dado no se altero retroactivamente.
- *Cuando necesito ayuda juridica*: no aplica; si una tendencia negativa (por ejemplo, un aumento sostenido de incidentes) le preocupa, consulte a su Delegado o a asesoria especializada para entender la causa.

**5. Diferencia entre el Dashboard y un Reporte**

- *Que es*: el Dashboard es la vista en vivo, siempre actualizada, que usted consulta dentro del sistema; un Reporte es un archivo exportado (PDF, XLSX, CSV o ZIP) que congela esa informacion en un momento dado para compartirla fuera del sistema, con verificacion de integridad.
- *Por que tengo que hacer esto*: porque a veces necesita mostrarle el estado de su programa a alguien que no tiene acceso al sistema (por ejemplo, la Junta Directiva o un auditor externo), y para eso necesita un archivo, no solo una pantalla.
- *Fundamento*: no corresponde a un OBL-ID especifico, salvo cuando el reporte exportado es, en si mismo, evidencia de una obligacion (por ejemplo, el paquete de evidencia para la ACE, que remite a OBL-PRIN-03, propietaria de MOD-019).
- *Cuando necesito ayuda juridica*: si va a entregar un reporte a la ACE o a un tercero externo y no esta seguro de si el contenido es correcto o completo, consulte a su Delegado o a asesoria especializada antes de enviarlo.

**6. Por que un indicador puede decir "no disponible en esta version"**

- *Que es*: algunos indicadores del catalogo dependen de un modulo que su version del sistema aun no incluye (por ejemplo, Transferencias Internacionales o Riesgos/EIPD, si su empresa contrato solo el nucleo basico).
- *Por que tengo que hacer esto*: para que la ausencia de un modulo no se confunda con "no hay riesgo" en esa area; el sistema le avisa explicitamente que ese dato todavia no esta disponible, en vez de mostrar un cero enganoso.
- *Fundamento*: no corresponde a un OBL-ID especifico; es una regla de diseno de este modulo (seccion G) pensada para no contradecir el principio de no afirmar cumplimiento donde en realidad falta informacion.
- *Cuando necesito ayuda juridica*: si no sabe si su empresa deberia tener contratado ese modulo (por ejemplo, si en verdad transfiere datos al extranjero), consulte con su Delegado antes de decidir que el area "no aplica".

---

## Nota final del agente (desacuerdos y observaciones sobre las fuentes de diseno)

1. **Asimetria entre `depende_de` (3 modulos) y el consumo real de indicadores y reportes (24 modulos), y como se resolvio.** `mapa_modulos.json` declara `depende_de: ["MOD-005", "MOD-019", "MOD-021"]` para MOD-020, y la ficha resumida de la seccion 3 de `06_mapa_definitivo_de_modulos.md` describe esto como "entra desde MOD-005, MOD-019, MOD-021... sale hacia ninguno (es un modulo terminal de lectura)". Esa declaracion es correcta como dependencia estructural minima de construccion (los tres son los unicos MUST HAVE sin los cuales el "dashboard basico" no puede operar en absoluto), pero es incompleta como descripcion funcional: el `grep -n "MOD-020" analisis/03_modulos/*.md` ejecutado antes de escribir esta ficha encontro menciones explicitas a "MOD-020" en las secciones M o L de MOD-005, MOD-008, MOD-009, MOD-010, MOD-011, MOD-014, MOD-015, MOD-016, MOD-017, MOD-018, MOD-019, MOD-021, MOD-022, MOD-023, MOD-024 y MOD-025 (15 modulos con mencion literal), y ademas las secciones M de MOD-001, MOD-002, MOD-003, MOD-004, MOD-006, MOD-007, MOD-012, MOD-013 y MOD-026 (9 modulos mas, 24 en total) usan exactamente el mismo vocabulario de "vista por rol" (Gerencia, Responsable, Legal/Delegado, Auditor, o el subconjunto que aplique) que corresponde a las 4 perspectivas de este modulo, aunque no citen "MOD-020" por su codigo. Esta ficha resuelve esa asimetria exactamente con el mismo criterio que la seccion 6.1 de `06_mapa_definitivo_de_modulos.md` ya usa para explicar por que MOD-001, MOD-023 y MOD-024 alimentan a casi todos los modulos sin que cada consumidor declare una dependencia estructural reciproca: `depende_de` registra la dependencia minima de construccion, mientras que el consumo de datos por referencia (aqui, al reves: MOD-020 como consumidor amplio) es mas extenso por diseno. No se propone cambiar `depende_de` de MOD-020 en `mapa_modulos.json` (seria incorrecto declarar alli una dependencia estructural que MOD-020 no tiene para poder lanzarse en su version minima), pero se recomienda a quien consolide el mapa final documentar esta misma distincion tambien para MOD-020, con la misma nota que ya lleva la seccion 6.1, y considerar si el campo `alimenta_a` de los 24 modulos fuente deberia declarar "MOD-020" de forma mas consistente (hoy 15 de 24 lo hacen explicitamente en su ficha, aunque no siempre coincide con su propio campo `alimenta_a` en el JSON, un patron de inconsistencia ya senalado antes por `MOD-021_ficha.md` y `MOD-022_ficha.md` para otras relaciones; MOD-026 es, ademas, uno de los que no lo declara, coherente con su propio `"alimenta_a": []` en `mapa_modulos.json`).
2. **El filtro por "sociedad" del enfoque especifico de la tarea contradice, en apariencia, el alcance MVP ya decidido para MOD-001.** El enunciado de esta tarea pide explicitamente "filtros por sucursal, unidad o sociedad". Sin embargo, `MOD-001_ficha.md` (seccion D.1, campo Sucursales, y seccion Q) y la decision de alcance 2.7.31 de `02_validacion_de_la_idea.md` establecen que el MVP solo soporta "una razon social con sucursales", no multiples sociedades de un mismo grupo (esa capacidad, junto con "vision consolidada multi-sociedad en el dashboard", queda declarada explicitamente V1/Enterprise en la propia tabla Q de MOD-001). Esta ficha resuelve la aparente contradiccion sin desatender ninguna de las dos fuentes: modela el campo "Sociedad" en el filtro de vista (seccion D.1) para que el diseno del Dashboard ya contemple esa dimension cuando la capacidad exista, pero lo declara explicitamente inactivo mientras la organizacion tenga una sola sociedad dada de alta, y clasifica la "vista consolidada multi-sociedad" como FUTURE en la seccion Q, coherente con MOD-001. No se trata de un supuesto incorrecto de la tarea, sino de una instruccion redactada pensando en el diseno completo del modulo (que debe estar preparado para esa dimension) mas que en el alcance exacto del MVP; se recomienda a quien redacte o revise el enfoque especifico de proximas tareas aclarar esta distincion entre "campo modelado" y "capacidad activa en el MVP".
3. **Mapeo de los 8 clusters legales sobre el mapa definitivo de 26 modulos: ambiguedad genuina, resuelta como decision de diseno explicita.** `propuesta_mapa_obligaciones.md` (perdedora, ver `06_mapa_definitivo_de_modulos.md`, seccion 12) definio los 8 clusters sobre 16 modulos "de proceso" propios, dejando fuera de cualquier cluster a los 9 modulos que en esa propuesta eran transversales (incluyendo Dashboard, Reportes, Auditoria y Evidencias, todos agrupados sin distincion en su cluster "I"). El mapa definitivo vigente reorganizo esos modulos de forma distinta: mantuvo 6 modulos transversales (MOD-021 a MOD-026) pero saco a Auditoria (MOD-018) y Evidencias (MOD-019) de esa barra para ubicarlos en la etapa Demostrar, como modulos semi-transversales. Ninguna fuente de diseno disponible (ni la propuesta perdedora, ni el mapa definitivo, ni el objetivo del producto) resuelve explicitamente a que cluster legal, si alguno, pertenecen MOD-018 y MOD-019 bajo esta nueva organizacion. Esta ficha resuelve la ambiguedad de forma explicita en la seccion M.4: los 8 clusters se mapean 1 a 1 sobre los 16 modulos de proceso equivalentes en el mapa actual (MOD-001, MOD-002 para el cluster A; y asi sucesivamente), y MOD-018, MOD-019, MOD-020 mismo y los 6 modulos transversales (MOD-021 a MOD-026) quedan fuera de la clasificacion por cluster, apareciendo en la vista de un cluster especifico solo de forma cruzada (por ejemplo, mostrando las tareas o la evidencia cuyo "modulo de origen" pertenece a ese cluster) en vez de tener una casilla propia. Se marca como una decision de diseno de esta ficha, no como una correccion de `mapa_modulos.json` ni de `06_mapa_definitivo_de_modulos.md`, y se recomienda a quien consolide el mapa final confirmar o ajustar este criterio, en particular para el cluster H ("Relacion con la autoridad"), donde podria argumentarse en sentido contrario que MOD-018 (auditoria de cumplimiento, vinculada a las Politicas ACE) deberia tener su propia casilla.
4. **Clasificacion global MUST HAVE, mantenida sin cambios, con el desglose interno que la propia entrada del mapa ya anticipaba.** Esta ficha mantiene la clasificacion MUST HAVE de `mapa_modulos.json` para MOD-020 en su conjunto, sin proponer ningun cambio: coincide con el test de tres condiciones de `06_mapa_definitivo_de_modulos.md`, seccion 2, principio 7, porque MOD-020 es la unica forma de que el estado del programa (condicion (c), capacidad probatoria y de vision general desde el primer dia) sea visible sin recorrer 25 pantallas distintas. La propia justificacion de MVP que ya trae la entrada de MOD-020 en el mapa ("Dashboard basico... MUST HAVE; reportes exportables avanzados por area SHOULD HAVE dentro del mismo modulo") es la que esta ficha desarrolla en detalle en la seccion Q, sin reinterpretarla.
5. **Ninguna mencion especifica a MOD-020, Dashboard o Reportes se encontro en `lente_faltantes.md` ni en `lente_inconsistencias.md`.** Se verifico con busqueda de texto sobre ambos documentos completos; las unicas coincidencias de "reporte" en `lente_faltantes.md` se refieren a un reporte de buro de credito (exclusion del Art. 3) y a un reporte de incidentes de ciberseguridad a la ACE (faltante de MOD-013), ninguna relacionada con este modulo. Esto es consistente con que MOD-020 no aparece como modulo propietario ni colaborador de ninguna obligacion: los faltantes e inconsistencias de la validacion de la idea se concentran en modulos con obligaciones propias, no en el Dashboard.
6. **Ningun otro desacuerdo material se detecto entre esta ficha y las fuentes de diseno ya decididas** (`02_validacion_de_la_idea.md`, `04_objetivo_exacto_del_producto.md`, `05_tipos_de_usuario.md`, `22_anti_features.md`, `06_mapa_definitivo_de_modulos.md`, `mapa_modulos.json`). Todas las afirmaciones juridicas de esta ficha (por ejemplo, las referencias a OBL-PRIN-03 o a la reforma 659) citan su fuente y su articulo segun `01_legal/matriz_obligaciones.json` y `01_legal/03_hallazgos_regulatorios.md`, sin inventar ningun OBL-ID nuevo; donde una regla es una decision de producto sin respaldo legal expreso (los umbrales de semaforo, el plazo de retencion propuesto para el registro de exportaciones, la escala de 5 estados del "estado del programa"), esta ficha lo marca explicitamente como "[opinion de producto]", siguiendo el mismo estandar que las 24 fichas ya redactadas.
7. **Correccion aplicada tras una revision adversarial: MOD-026 si tenia ficha propia y su catalogo estaba incompleto.** El borrador original de esta ficha afirmo, en la seccion M.3.1, en la seccion N.3 y en este mismo apartado, que `MOD-026_ficha.md` "aun no tiene ficha propia", cuando en realidad ya existia en `analisis/03_modulos/` (agregada en el mismo commit inicial que el borrador de MOD-020, con fecha de archivo anterior a la version final de esta ficha). Ese error hizo que el catalogo consolidado de indicadores (seccion M.3.1) y de reportes (seccion N.3), que es el entregable central de esta ficha, quedara incompleto: faltaban los 4 indicadores y los 3 reportes propios de MOD-026. Se corrigio volviendo a listar la carpeta `analisis/03_modulos/`, confirmando la existencia de `MOD-026_ficha.md`, leyendo integramente sus secciones M y N, e integrando su contenido real en las tablas correspondientes de esta ficha; de paso se corrigio el conteo repetido de "23 fichas ya redactadas" (aritmeticamente incorrecto: MOD-001 a MOD-019 mas MOD-021 a MOD-025 son 24, no 23) a "24 fichas" en todos los lugares donde aparecia, y se corrigieron dos citas imprecisas al catalogo de `22_anti_features.md` en la seccion A (el item 1 respalda solo la parte de no duplicar la base de clientes, no la prohibicion generica de ser un BI comercial; los items 22 y 23, declarados como fuente en el encabezado pero no aplicados en el cuerpo del borrador original, ahora tienen una linea explicita propia en la seccion A). No se detecto ningun desacuerdo con el mapa en esta correccion: fue un error de ejecucion de esta ficha (no volver a listar la carpeta antes de cerrarla), no una inconsistencia de `mapa_modulos.json` ni de `06_mapa_definitivo_de_modulos.md`.






