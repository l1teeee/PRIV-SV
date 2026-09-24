# MODULO: Dashboard y Reportes

Codigo corto del modulo: MOD-020
Clasificacion global del modulo: MUST HAVE (dashboard basico por perspectiva: pendientes, vencidos, tratamientos, solicitudes). Dentro del mismo modulo, los reportes exportables avanzados por area y la vista alternativa por los 8 clusters legales son SHOULD HAVE (ver seccion Q); esta ficha no cambia la clasificacion global MUST HAVE que trae `mapa_modulos.json`, solo documenta el desglose interno que la propia entrada del mapa ya anticipa en su campo `mvp`.
Obligaciones que cubre: ninguna obligacion propia (ningun OBL-ID de `analisis/01_legal/matriz_obligaciones.json` lo tiene como modulo propietario; verificado por busqueda directa de "MOD-020" sobre el archivo completo de las 105 obligaciones, sin resultados). Ninguna obligacion colaboradora tampoco: MOD-020 no aparece en el campo `modulos_candidatos` de ningun registro de la matriz. Esto es consistente con el principio de diseno de que los modulos transversales o de solo lectura no poseen obligaciones de negocio propias (`analisis/02_validacion/06_mapa_definitivo_de_modulos.md`, seccion 2, principio 5) y con la propia entrada de MOD-020 en `mapa_modulos.json` (`"obligaciones_propietarias": []`, `"obligaciones_colaboradoras": []`). MOD-020 es, en cambio, el punto de consumo declarado o implicito de los indicadores (seccion M) y reportes (seccion N) de practicamente todos los demas modulos: ver el catalogo consolidado de esta ficha y la nota final sobre la asimetria entre `depende_de` y el consumo real de datos.
Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (sin codigo, sin SQL, sin APIs, sin stack, sin infraestructura).
Fuentes usadas para esta ficha: `analisis/00_contexto_para_agentes.md`, `analisis/00_prompt_analisis_funcional.md`, `analisis/00_plantilla_ficha_modulo.md`, `analisis/02_validacion/mapa_modulos.json` (entrada MOD-020), `analisis/02_validacion/06_mapa_definitivo_de_modulos.md` (secciones 0, 2, 3, 4, 5, 6, 6.1, 7, 9), `analisis/01_legal/matriz_obligaciones.json` (verificacion de ausencia de obligaciones propias o colaboradoras), `analisis/02_validacion/02_validacion_de_la_idea.md` (secciones 2.3 a 2.7), `analisis/02_validacion/04_objetivo_exacto_del_producto.md` (secciones 1.1 a 1.3 y "Como se mide el exito"), `analisis/02_validacion/05_tipos_de_usuario.md` (secciones 5.1 a 5.4), `analisis/02_validacion/22_anti_features.md` (items 1, 5, 8, 9, 19, 22, 23, 25), `analisis/02_validacion/propuesta_mapa_obligaciones.md` (seccion 1, arbol de 8 clusters legales; seccion 2, fichas MOD-DASH y MOD-REP de la propuesta perdedora), `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` (seccion 31, Dashboard; hipotesis de producto, no decision), `analisis/02_validacion/lente_faltantes.md` y `lente_inconsistencias.md` (verificado: ninguna mencion especifica a MOD-020, Dashboard o Reportes), y las 23 fichas ya redactadas en `analisis/03_modulos/` (MOD-001 a MOD-019, MOD-021 a MOD-025), en particular sus secciones M (Dashboard) y N (Reportes) completas, extraidas con `awk '/^## M[.]/,/^## O[.]/' analisis/03_modulos/MOD-*.md`, y las menciones directas a "MOD-020" localizadas con `grep -n "MOD-020" analisis/03_modulos/*.md` (ver Nota final para el detalle del contrato de expectativas). MOD-021_ficha.md y MOD-018_ficha.md se usaron ademas como modelo de estilo y profundidad, segun pide la tarea; MOD-025_ficha.md (otro modulo terminal de lectura sin obligaciones propias) se uso como modelo estructural adicional para las secciones I, J y L.

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
  - No es un motor de analitica de negocio generico ni un BI comercial: sus indicadores y reportes estan acotados al programa de proteccion de datos de la empresa, no a metricas comerciales ajenas (`22_anti_features.md`, item 1).

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
   Todos los modulos de negocio y transversales (MOD-001 a MOD-019, MOD-021 a MOD-025;
   MOD-026 cuando exista su ficha) escriben o exponen indicadores (seccion M de cada uno)
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

**Consumo real de indicadores y reportes (mas amplio que el `depende_de` estructural, ver Nota final punto 1).** En la practica funcional, y confirmado por el `grep -n "MOD-020" analisis/03_modulos/*.md` ejecutado antes de escribir esta ficha (ver Nota final), MOD-020 consume, a traves de la seccion M (indicadores) y la seccion N (reportes) de cada ficha ya redactada, datos de los 23 modulos existentes al momento de escribir esta ficha: MOD-001 a MOD-019 y MOD-021 a MOD-025. Esto es exactamente la misma asimetria, ya documentada y aceptada, entre `depende_de` (dependencia estructural minima de construccion) y el consumo real de datos por referencia, que la seccion 6.1 de `06_mapa_definitivo_de_modulos.md` explica para MOD-001, MOD-023 y MOD-024 ("alimenta_a puede ademas listar destinatarios adicionales que no tienen una entrada depende_de reciproca explicita en el modulo consumidor"): aqui el mismo fenomeno ocurre al reves, con MOD-020 como consumidor amplio y cada modulo de origen declarando "MOD-020" en su propio `alimenta_a` (cuando lo declara) sin que eso implique que MOD-020 deba declarar una dependencia estructural reciproca hacia cada uno de ellos para poder lanzarse en su version minima.

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

<!-- CONTINUAR AQUI 4 -->



