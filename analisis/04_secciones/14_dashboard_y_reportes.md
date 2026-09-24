# 14. Dashboard y reportes

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (sin codigo, sin SQL, sin APIs, sin stack, sin infraestructura).

Alcance de esta seccion: consolida y cruza lo que ya decidieron `analisis/03_modulos/MOD-020_ficha.md` (Dashboard y Reportes, fuente principal y ficha propietaria de este modulo) y las secciones M (Dashboard) y N (Reportes) de las otras 25 fichas ya redactadas (`analisis/03_modulos/MOD-001_ficha.md` a `MOD-019_ficha.md` y `MOD-021_ficha.md` a `MOD-026_ficha.md`), extraidas con `awk '/^## M[.]/,\/^## N[.]/'` y `awk '/^## N[.]/,\/^## O[.]/'` sobre cada archivo. No inventa funcionalidades que ninguna ficha define; donde el prompt del cliente exige algo que ninguna ficha cubre de forma literal, se marca de forma explicita como "propuesta de esta seccion, no presente en las fichas". Fuentes adicionales: `analisis/02_validacion/mapa_modulos.json`, `analisis/02_validacion/06_mapa_definitivo_de_modulos.md` (secciones 5, 6.1, 7 y 8), `analisis/02_validacion/05_tipos_de_usuario.md` (seccion 5.3), `analisis/02_validacion/22_anti_features.md`, `analisis/01_legal/matriz_obligaciones.json` y `analisis/00_prompt_analisis_funcional.md` (areas 26 y 28).

**Convencion de la columna Version usada en todo el catalogo.** El prompt del cliente organiza la salida final en secciones 19 (MVP), 20 (V1) y 21 (V2/Enterprise), mientras que `mapa_modulos.json` y la seccion Q de cada ficha clasifican cada pieza como MUST HAVE, SHOULD HAVE, COULD HAVE o FUTURE. Esta seccion traduce ambas escalas con la equivalencia MUST HAVE = MVP, SHOULD HAVE = V1, COULD HAVE = V2, FUTURE = V2/Enterprise. Cuando el catalogo no distingue version por indicador o por reporte individual (las 25 fichas de origen no lo hacen: la unica excepcion es la propia MOD-020, cuya seccion Q si desglosa version por funcionalidad interna), la version de un indicador o de un reporte es la version del modulo que lo produce, porque el indicador es una lectura directa de los datos de ese modulo (principio M.1 de MOD-020: "MOD-020 nunca recalcula ni reinterpreta el valor de un indicador").

---

## 14.1 Principio rector: estado del programa, nunca porcentaje de cumplimiento legal

Ningun indicador ni ningun reporte de este modulo, ni de ningun otro modulo del sistema, expresa jamas un "porcentaje de cumplimiento legal". Esto no es una preferencia de diseno: es el anti-feature mas explicito del producto (`22_anti_features.md`, item 5: "Declarar un porcentaje de cumplimiento legal (0 a 100%)", razon Legal y Producto) y corresponde directamente a la seccion 31 del documento maestro y al principio central del prompt de analisis funcional ("nunca afirmar cumplimiento legal X%; usar estado del programa, controles configurados, tareas pendientes, evidencia disponible").

En cambio, todo indicador de este modulo describe siempre uno de estos cuatro conceptos, tal como los define `MOD-020_ficha.md` (seccion A):

- **Estado del programa**: en que etapa del recorrido o en que condicion general se encuentra un area (por ejemplo, "Operando" o "Con evidencia").
- **Controles configurados**: cuantos controles, reglas o mecanismos existen y estan activos.
- **Tareas pendientes**: cuanto trabajo falta, esta vencido o esta en curso.
- **Evidencia disponible**: cuanta evidencia verificable existe para respaldar una obligacion.

Esta distincion tiene una base legal indirecta: el indicador de evidencia disponible (MOD-019) sostiene, de forma agregada, el principio de responsabilidad demostrada (**OBL-PRIN-03**, Ley para la Proteccion de Datos Personales D.L. 144, Art. 5 lit. i, OBLIGATORIO, verificada), que exige que el responsable "sea capaz de demostrar el cumplimiento de sus obligaciones, adoptando medidas y manteniendo evidencia de su cumplimiento". Mostrar cuanta evidencia existe es coherente con esa obligacion; afirmar que la empresa "cumple" no lo es, porque esa conclusion exige un analisis juridico que el software no puede realizar por si mismo.

**Banner de descargo, visible en el Dashboard principal, en las 4 perspectivas:**

```
Este panel muestra el estado del programa (controles configurados, tareas
pendientes, evidencia disponible), no una medicion de cumplimiento legal.
Consulte con su Delegado o con asesoria especializada antes de afirmar
que su empresa cumple con la ley.
```

### 14.1.1 El modelo de estado de MOD-020: escala de 5 valores por etapa y por cluster

Para dar a la Gerencia una sintesis sin caer en un porcentaje, MOD-020 calcula, para cada una de las 6 etapas del recorrido (Empezar, Diagnosticar, Planificar, Registrar, Operar, Demostrar; `06_mapa_definitivo_de_modulos.md`, seccion 1) y para cada uno de los 8 clusters legales (seccion 14.4 de este documento), un estado en una escala cerrada de 5 valores, nunca un numero. [opinion de producto, sin respaldo legal especifico para esta escala en si; disenado para dar una sintesis util sin violar el anti-feature 5]

| Estado | Que significa | Como se calcula (regla general) |
|---|---|---|
| Sin iniciar | Ningun modulo de esa etapa o cluster tiene registros de negocio cargados | 0 registros activos en todos los modulos de la etapa o cluster |
| En configuracion | La empresa esta completando el alta basica, sin operacion regular todavia | Existen registros, pero menos de la mitad de las tareas asociadas de MOD-021 estan Completadas, o el diagnostico (MOD-004) aun no marco esa etapa o cluster como aplicable de forma definitiva |
| Operando | Hay actividad regular: tareas creandose y cerrandose, expedientes abriendose y cerrandose dentro de plazo | Mas de la mitad de las tareas de MOD-021 asociadas estan Completadas o En proceso, sin acumulacion de Vencidas |
| Con evidencia | Ademas de operar, existe evidencia disponible verificable (via MOD-019) para las obligaciones aplicables | El indicador "evidencia disponible por obligacion aplicable" de MOD-019 es Verde para las obligaciones OBLIGATORIO de esa etapa o cluster |
| Revisado | Ademas de lo anterior, existe una revision o auditoria formal reciente | Existe al menos un hallazgo de auditoria (MOD-018) cerrado, o una revision periodica confirmada, en los ultimos 12 meses |

El texto de pantalla nunca dice "cumplimiento": dice, por ejemplo, "Relacion con terceros: Con evidencia" en vez de cualquier expresion de porcentaje. Este indicador de sintesis nunca reemplaza el detalle del catalogo consolidado (seccion 14.3): es una vista de alto nivel que siempre permite bajar al detalle por modulo (drill-down).

### 14.1.2 Por que si existen indicadores con porcentaje

Varios indicadores del catalogo (seccion 14.3) usan un porcentaje: por ejemplo "Cobertura del RAT" (fichas vigentes sobre tratamientos detectados) o "Controles con evidencia vigente". Esto no contradice el principio anterior: esos porcentajes miden una magnitud operativa concreta y acotada (cuantos registros de un tipo existen sobre un total conocido), nunca "cuanto cumple la empresa con la ley" en abstracto. La diferencia es la misma que ya traza `MOD-020_ficha.md`, seccion A: el sistema puede decir "8 de 10 tratamientos detectados ya tienen ficha en el RAT" (un conteo verificable) pero nunca "su empresa cumple en un 80% con la ley" (una conclusion juridica que el sistema no puede emitir). Todo texto de ayuda que acompana un indicador porcentual aclara este limite (seccion 14.7 y `MOD-020_ficha.md`, seccion R.2).

---

## 14.2 Las cuatro perspectivas

Las 4 perspectivas (Gerencia, Responsable, Legal/Delegado, Auditor) que describe el area 26 del prompt de analisis funcional son una capa de presentacion sobre los 12 roles estandar del sistema (`05_tipos_de_usuario.md`, seccion 5.3), no una quinta categoria de rol ni un reemplazo del sistema de permisos (seccion 11 del blueprint). Cada usuario ve, por defecto, la perspectiva que corresponde a su rol principal; quien acumula varios roles ve la de mayor alcance y puede cambiar de perspectiva manualmente si su rol se lo permite. La tabla completa de correspondencia rol -> perspectiva por defecto, y la tabla de permisos por accion (ver perspectiva Gerencia, aplicar filtro, hacer drill-down, exportar, configurar umbrales), viven en `MOD-020_ficha.md`, secciones B y C, y no se repiten aqui en su totalidad; esta seccion retoma solo lo necesario para documentar cada perspectiva como pantalla.

Regla comun a las 4 perspectivas, valida para toda esta seccion: todo indicador respeta primero el filtro de permisos del rol y despues el filtro de perspectiva, cluster, etapa, sucursal/unidad o periodo que el usuario elija (`MOD-020_ficha.md`, seccion M.1); el drill-down hacia el registro fuente nunca revela un registro que el modulo de origen ya le negaria a ese rol (seccion 14.7.2).

### 14.2.1 Perspectiva Gerencia

- **Objetivo.** Dar, en una sola pantalla, una vision general de todo el programa de proteccion de datos de la empresa, sin necesidad de abrir ningun otro modulo, para poder responder "como vamos" a quien se lo pregunte (Gerencia General, Junta Directiva por via del reporte exportado).
- **Preguntas que responde.** En que etapa o cluster estamos avanzando y en cuales no. Cuales son los indicadores en rojo que requieren decision o presupuesto. Como avanza el Plan de Cumplimiento (MOD-005). Cuanta evidencia disponible tenemos frente a las obligaciones aplicables (MOD-019). Que tan cerca esta la reforma 659 de afectar nuestras obligaciones.
- **Bloques de la pantalla.**
  1. Estado del programa por las 6 etapas del recorrido (seccion 14.1.1).
  2. Indicadores criticos (en rojo) de toda la organizacion, con enlace de detalle.
  3. Avance del Plan de Cumplimiento (MOD-005).
  4. Evidencia disponible por obligacion aplicable (MOD-019).
  5. Badge de regimen normativo vigente (ACTUAL / FUTURO, MOD-024).
  6. Accesos directos a exportar el Informe gerencial y el Informe para Junta Directiva.
- **Indicadores principales (ver catalogo completo en 14.3).**

| Indicador | Modulo fuente | Semaforo |
|---|---|---|
| Avance del plan | MOD-005 | Verde mayor a 80%, amarillo 50-80%, rojo menor a 50% |
| Acciones criticas pendientes o vencidas | MOD-005 | Rojo si hay Vencida |
| Evidencia disponible por obligacion aplicable | MOD-019 | Verde 100% OBLIGATORIO, amarillo falta RECOMENDADO/CONDICIONAL, rojo falta OBLIGATORIO |
| Tareas vencidas | MOD-021 | Rojo si mayor a 0 |
| Solicitudes ARCO-POL vencidas | MOD-011 | Rojo si mayor a 0 |
| Incidentes abiertos por severidad | MOD-013 | Rojo si 1+ Critica |
| Roles criticos sin titular | MOD-001 | Verde 0, amarillo 1, rojo 2+ |

- **Acciones posibles desde el Dashboard.** Cambiar de perspectiva (si el rol lo permite). Filtrar por sucursal, unidad, etapa o periodo. Bajar al detalle (drill-down) de cualquier indicador hacia su modulo de origen, respetando permisos. Exportar el Informe gerencial consolidado o el Informe para Junta Directiva (seccion 14.5). Enlazar el paquete de evidencia para la ACE (sin generarlo, solo referenciarlo). Ver la tendencia comparando con una foto periodica (cierre mensual) anterior. Ninguna accion desde este panel crea, aprueba ni modifica un registro de negocio: toda accion correctiva se hace en el modulo de origen (seccion 14.7).
- **Maqueta ASCII.**

```
+------------------------------------------------------------------+
| DASHBOARD - Perspectiva: GERENCIA          [ cambiar perspectiva ]|
| Filtros: Sucursal [Todas]  Periodo [Hoy, tiempo real]  Etapa[Todas]|
+------------------------------------------------------------------+
| Aviso: estado del programa (controles, tareas, evidencia),       |
| no un porcentaje de cumplimiento legal.                          |
+------------------------------------------------------------------+
|                                                                    |
| ESTADO DEL PROGRAMA POR ETAPA DEL RECORRIDO                       |
|  Empezar ....... Operando        Registrar ..... Con evidencia   |
|  Diagnosticar .. Con evidencia   Operar ......... Operando        |
|  Planificar .... Operando        Demostrar ...... Revisado        |
|                                                                    |
| INDICADORES CRITICOS (rojo)                                       |
|  - Acciones criticas del plan vencidas (MOD-005) ....... rojo -->|
|  - Solicitudes ARCO-POL vencidas (MOD-011) ............. rojo -->|
|  - Controles obligatorios sin evidencia (MOD-015) ...... rojo -->|
|  - Cronometros de 72h por vencer (MOD-013) ......... amarillo -->|
|                                                                    |
| AVANCE DEL PLAN DE CUMPLIMIENTO (MOD-005): 62% Completada          |
| EVIDENCIA DISPONIBLE (MOD-019): 92% de las obligatorias            |
| REGIMEN NORMATIVO VIGENTE (MOD-024): [ ACTUAL ]                   |
|                                                                    |
| [ Exportar Informe gerencial ]   [ Exportar Informe Junta Dir. ]  |
+------------------------------------------------------------------+
```

### 14.2.2 Perspectiva Responsable

- **Objetivo.** Que la persona que ejecuta el trabajo del dia a dia (Responsable ARCO-POL, Responsable de area, Responsable de Seguridad/IT, Aprobador) vea sus propios pendientes y vencidos sin tener que revisar cada modulo por separado.
- **Preguntas que responde.** Que tengo pendiente hoy. Que se me vencio o esta por vencer. Cuantas aprobaciones esperan mi decision. Cuanto de mi propia area (si es Responsable de area) esta al dia.
- **Bloques de la pantalla.**
  1. Tareas pendientes, en proceso y vencidas asignadas a la persona (MOD-021).
  2. Aprobaciones pendientes, si el rol es Aprobador (MOD-021).
  3. Solicitudes ARCO-POL propias por vencer, si el rol es Responsable ARCO-POL (MOD-011).
  4. Controles e incidentes propios, si el rol es Seguridad/IT (MOD-015, MOD-013).
  5. Indicadores acotados a su propia sucursal o area, nunca el agregado de otras areas (seccion C de `MOD-020_ficha.md`).
- **Indicadores principales (ver catalogo completo en 14.3).**

| Indicador | Modulo fuente | Semaforo |
|---|---|---|
| Tareas pendientes | MOD-021 | Verde/amarillo/rojo segun promedio historico |
| Tareas vencidas | MOD-021 | Rojo si mayor a 0 |
| Aprobaciones pendientes | MOD-021 | Amarillo mayor a 3 dias, rojo mayor a 5 dias |
| Solicitudes ARCO-POL proximas a vencer | MOD-011 | Amarillo/rojo segun plazo restante |
| Cronometros de 72h por vencer | MOD-013 | Amarillo menor a 24h, rojo menor a 6h |
| Fichas del RAT pendientes de revision periodica (si su area administra tratamientos) | MOD-006 | Verde 0, amarillo 1-5, rojo mayor a 5 |
| Proveedores sin contrato o DPA vigente vinculado | MOD-009 | Rojo si mayor a 0 |

- **Acciones posibles desde el Dashboard.** Bajar al detalle de una tarea, una solicitud o un incidente y actuar alli (el Dashboard nunca permite completar, aprobar ni cerrar nada directamente: siempre redirige al modulo de origen, `MOD-020_ficha.md`, seccion C, ultima fila). Filtrar por su propia sucursal o area. Ver su carga de trabajo comparada con el umbral configurado.
- **Maqueta ASCII.**

```
+------------------------------------------------------------------+
| DASHBOARD - Perspectiva: RESPONSABLE       [ cambiar perspectiva ]|
| Usuario: Daniela Cornejo (RRHH)    Area: Recursos Humanos          |
+------------------------------------------------------------------+
| MIS TAREAS                                                        |
|  Pendientes ........ 4      En proceso ........ 2                 |
|  Vencidas .......... 1  (rojo)  --> ver tarea                     |
|                                                                    |
| MIS APROBACIONES PENDIENTES (si aplica el rol Aprobador)           |
|  En espera hace 4 dias .... 1  (amarillo) --> ver aprobacion       |
|                                                                    |
| MI AREA: RECURSOS HUMANOS (RAT, MOD-006)                           |
|  Fichas vigentes ........... 5 de 6 tratamientos detectados        |
|  Requiere revision ......... 1  (amarillo) --> ver ficha            |
|                                                                    |
| PROVEEDORES DE MI AREA (MOD-009)                                   |
|  Sin contrato vigente vinculado ........ 0  (verde)                |
|                                                                    |
| [ Ver todas mis tareas en el Centro de Tareas ]                    |
+------------------------------------------------------------------+
```

### 14.2.3 Perspectiva Legal/Delegado

- **Objetivo.** Que quien concentra hoy la responsabilidad legal (Delegado de Proteccion de Datos, o Responsable interno bajo el estado FUTURO de la reforma 659; Responsable Legal/Compliance) vea riesgos, decisiones pendientes y avance por tema legal, con la posibilidad de cambiar a una vista organizada por los 8 clusters legales en vez de por las 6 etapas del recorrido.
- **Preguntas que responde.** Que riesgos y decisiones legales estan pendientes. Como avanza cada uno de los 8 temas legales del programa. Cuantos informes periodicos del Delegado se han entregado frente al minimo legal. En que regimen normativo estamos (ACTUAL o FUTURO de la reforma 659) y que obligaciones cambian si cambia.
- **Bloques de la pantalla.**
  1. Selector "Vista por etapa del recorrido" / "Vista por los 8 clusters legales" (seccion 14.4).
  2. Riesgos y decisiones pendientes (EIPD de alto riesgo, denegatorias ARCO-POL con reclamo abierto, procedimientos sancionadores activos).
  3. Estado del nombramiento del Delegado/Responsable interno e informes periodicos entregados vs minimo legal (MOD-002).
  4. Badge de regimen ACTUAL/FUTURO y conteo de las 17 obligaciones afectadas por la reforma 659 (MOD-024).
  5. Evidencia disponible por cluster (MOD-019).
- **Indicadores principales (ver catalogo completo en 14.3).**

| Indicador | Modulo fuente | Semaforo |
|---|---|---|
| Informes periodicos entregados vs minimo legal (OBL-DPO-07) | MOD-002 | Si/no cumplido |
| Estado regulatorio vigente (badge ACTUAL/FUTURO) | MOD-024 | Informativo |
| Procedimientos sancionadores activos | MOD-024 | Rojo si hay uno con plazo vencido |
| Tratamientos de alto riesgo evaluados (EIPD) | MOD-014 | Verde 1, amarillo si hay Detectado sin avanzar, rojo si vencida |
| Reclamos ante la Direccion de Proteccion de Datos abiertos | MOD-011 | Rojo si mayor o igual a 1 |
| Transferencias sin evaluacion de pais completa | MOD-010 | Verde 0, amarillo 1-2, rojo 3+ |
| Huecos de evidencia abiertos | MOD-019 | Rojo si 1+ OBLIGATORIO |

- **Acciones posibles desde el Dashboard.** Activar la vista por clusters y filtrar por uno especifico (seccion 14.4). Bajar al expediente de un procedimiento sancionador, una EIPD o un reclamo ARCO-POL. Exportar cualquier reporte habilitado para este rol (seccion 14.5), incluido el Informe para Junta Directiva. Enlazar o iniciar el paquete de evidencia para la ACE (armado por MOD-019), con la advertencia de que su envio requiere revision y confirmacion de la organizacion (`MOD-020_ficha.md`, seccion H).
- **Maqueta ASCII.**

```
+------------------------------------------------------------------+
| DASHBOARD - Perspectiva: LEGAL / DELEGADO  [ cambiar perspectiva ]|
| Vista: [ 6 etapas del recorrido ] / ( 8 clusters legales )        |
+------------------------------------------------------------------+
| REGIMEN NORMATIVO VIGENTE: ACTUAL (delegado obligatorio)          |
| Reforma 659: aprobada 17-sep-2026, publicacion pendiente de       |
| verificar. 17 obligaciones cambiarian si pasa a FUTURO.           |
+------------------------------------------------------------------+
| ESTADO DEL DELEGADO (MOD-002)                                     |
|  Nombramiento ......... ACTIVO                                    |
|  Informes periodicos .. 2 de 2 minimos del periodo (verde)        |
|                                                                    |
| RIESGOS Y DECISIONES PENDIENTES                                   |
|  EIPD en mitigacion (Alto/Critico) ........ 1  (amarillo) --> ir  |
|  Reclamos ante la Direccion abiertos ....... 0  (verde)           |
|  Procedimientos sancionadores activos ....... 0  (verde)          |
|  Transferencias sin evaluacion de pais ...... 2  (amarillo) --> ir|
|                                                                    |
| EVIDENCIA DISPONIBLE POR CLUSTER (MOD-019)                        |
|  A.Nucleo organiz. ... Con evidencia   E.Terceros ... Operando    |
|  B.Entrada/hoja ruta . Con evidencia   F.Crisis ..... Con evid.   |
|  C.Registro/gobernanza Operando        G.Documentac.. Revisado    |
|  D.Titular ........... Con evidencia   H.Autoridad .. Con evid.   |
|                                                                    |
| [ Exportar Informe para Junta Directiva ] [ Preparar entrega ACE ]|
+------------------------------------------------------------------+
```

### 14.2.4 Perspectiva Auditor

- **Objetivo.** Dar al Auditor (interno o externo invitado) una vista de solo lectura centrada en evidencia disponible, huecos y vencimientos, sin exponer ningun dato personal de un titular, y con exportacion de reportes con fecha de corte.
- **Preguntas que responde.** Que evidencia existe y cual falta para cada obligacion aplicable. Que vencimientos y huecos hay en el periodo auditado. Que tan reciente es la ultima revision o auditoria formal. Que reportes puedo exportar con fecha de corte para mi expediente de auditoria.
- **Bloques de la pantalla.**
  1. Evidencia disponible y huecos abiertos, por clasificacion (OBLIGATORIO/RECOMENDADO/CONDICIONAL) (MOD-019).
  2. Estado de la ultima auditoria y hallazgos abiertos por severidad (MOD-018).
  3. Vencimientos: controles, contratos, capacitaciones, revisiones periodicas.
  4. Selector de fecha de corte o de foto periodica (cierre mensual) para comparar tendencia.
  5. Catalogo de reportes exportables habilitados para su alcance (seccion 14.5).
- **Indicadores principales (ver catalogo completo en 14.3).**

| Indicador | Modulo fuente | Semaforo |
|---|---|---|
| Evidencia disponible por obligacion aplicable | MOD-019 | Verde 100% OBLIGATORIO, amarillo falta RECOMENDADO/CONDICIONAL, rojo falta OBLIGATORIO |
| Huecos de evidencia abiertos | MOD-019 | Rojo si 1+ OBLIGATORIO |
| Estado de la ultima auditoria | MOD-018 | Verde/amarillo/rojo segun ciclo anual |
| Hallazgos abiertos por severidad | MOD-018 | Rojo si 1+ Critico |
| Controles obligatorios sin evidencia o vencidos | MOD-015 | Rojo si mayor a 0 |
| Expedientes con evidencia completa vs incompleta (ARCO-POL) | MOD-011 | Verde/amarillo/rojo segun checklist |
| Cobertura de fuente verificada en asuetos locales (calendario) | MOD-023 | Verde 100%, amarillo 80-99%, rojo menor a 80% |

- **Acciones posibles desde el Dashboard.** Fijar una fecha de corte o elegir una foto periodica para su alcance de auditoria. Bajar al registro fuente en modo de solo lectura. Exportar cualquier reporte habilitado para su alcance (seccion 14.5), siempre con verificacion de integridad via MOD-019. Un Auditor externo invitado ve unicamente los indicadores y reportes del alcance temporal y de modulos habilitado para su auditoria puntual (`MOD-020_ficha.md`, seccion B).
- **Maqueta ASCII.**

```
+------------------------------------------------------------------+
| DASHBOARD - Perspectiva: AUDITOR (solo lectura)                   |
| Alcance: [ Auditoria anual 2026 ]   Corte: [ 2026-09-24 ]         |
+------------------------------------------------------------------+
| EVIDENCIA DISPONIBLE POR OBLIGACION APLICABLE (MOD-019)           |
|  OBLIGATORIO ......... 92% Disponible  (amarillo, falta 8%) -->  |
|  RECOMENDADO ......... 78% Disponible  (amarillo) -->            |
|  CONDICIONAL ......... 100% Disponible (verde)                   |
|                                                                    |
| HUECOS DE EVIDENCIA ABIERTOS ....... 3 OBLIGATORIO (rojo) --> ir  |
|                                                                    |
| ULTIMA AUDITORIA (MOD-018)                                        |
|  Cerrada hace ...... 210 dias (verde, ciclo anual)                |
|  Hallazgos abiertos . 1 Alto, 0 Critico (amarillo) --> ir         |
|                                                                    |
| VENCIMIENTOS DEL PERIODO                                          |
|  Controles obligatorios sin evidencia ....... 0  (verde)          |
|  Contratos de proveedor por vencer (30 dias) . 2  (amarillo) -->  |
|                                                                    |
| [ Exportar Paquete de evidencia de la auditoria (MOD-019) ]       |
+------------------------------------------------------------------+
```

---
## 14.3 Catalogo consolidado de indicadores (secciones M)

Catalogo completo, consolidado a partir de la seccion M de las 26 fichas (extraido con `awk '/^## M[.]/,/^## N[.]/' analisis/03_modulos/MOD-*.md`, y verificado contra el mismo catalogo ya consolidado en `MOD-020_ficha.md`, seccion M.3.1). Se agrupa por modulo fuente en vez de repetir la columna "Modulo fuente" en cada fila (la agrupacion por subtitulo cumple la misma funcion, con menos ruido visual; es la misma convencion que ya usa `MOD-020_ficha.md` para este catalogo). La formula se resume de forma breve; el detalle completo, con los umbrales exactos y las notas de opinion de producto, vive en la seccion M de la ficha de origen, que esta tabla indexa sin reemplazar. Ningun indicador se expresa como "porcentaje de cumplimiento legal" (seccion 14.1).

### MOD-001 Organizacion y Personas (Version: MVP)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Usuarios activos vs invitados pendientes | Activos sobre total invitado | Verde/amarillo/rojo segun invitaciones vencidas | Gerencia, Administrador |
| Roles criticos sin titular | Roles criticos (Administrador, Delegado, Seguridad) sin usuario activo | Verde 0, amarillo 1, rojo 2+ | Gerencia, Legal, Administrador |
| Sucursales registradas | Conteo de sucursales ACTIVA | Informativo | Gerencia, Responsable de area |
| Separacion de funciones | Estado activada / recomendada no activada / no aplica | Verde si activada o bajo umbral; amarillo si no | Legal, Auditor, Gerencia |
| Ultimo cambio de estructura | Fecha del ultimo alta, baja o cambio de rol | Informativo | Auditor, Seguridad/IT |

### MOD-002 Delegado / Responsable Interno de Datos (Version: MVP)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Estado del nombramiento | ACTIVO sin plazos vencidos | Verde/amarillo (plazo a 5 dias)/rojo (sin registro o plazo vencido) | Gerencia, Responsable |
| Dias habiles para la proxima obligacion | Minimo entre fechas limite del modulo, via MOD-023 | Colorea segun cercania | Responsable, Legal |
| Informes periodicos entregados vs minimo legal (OBL-DPO-07) | Conteo ultimos 12 meses contra el minimo de 2 (Lineamientos DPO, Art. 30) | Si/no cumplido | Legal, Auditor |
| Estado regulatorio vigente | Badge ACTUAL / FUTURO desde MOD-024 | Informativo | Todas |
| Evidencia disponible del modulo | X de Y evidencias requeridas disponibles | Verde/amarillo/rojo | Auditor, Legal |
| Alertas activas del modulo | Conteo por nivel INFO/WARNING/HIGH/CRITICAL | Semaforo por nivel | Gerencia (HIGH/CRITICAL), Responsable (todas) |

### MOD-003 Onboarding (Version: MVP)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Configuracion inicial completada | Estado del onboarding (NO_INICIADO/EN_PROGRESO/ABANDONADO/COMPLETADO) | Verde/amarillo/rojo segun antiguedad | Gerencia, Administrador |
| Aceptacion de invitaciones | Usuarios que aceptaron sobre total invitados | Verde 100%, amarillo dentro de plazo, rojo vencidas | Administrador, Auditor |
| Estado de la designacion del Delegado | Heredado de MOD-002 desde el paso correspondiente del onboarding | Verde/amarillo/rojo | Legal/Delegado, Gerencia |
| Fecha y usuario de creacion de la organizacion | Dato directo del evento de auditoria | Informativo | Auditor |

### MOD-004 Diagnostico de Cumplimiento (Version: MVP)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Diagnosticos completados vs organizaciones activas | Sesiones cerradas sobre total de organizaciones con onboarding completo | Verde 100%, amarillo parcial, rojo sin iniciar | Gerencia, Administrador |
| Avance del diagnostico en curso | Preguntas respondidas sobre obligatorias visibles | Barra de progreso | Responsable |
| Acciones criticas abiertas generadas | Conteo de acciones criticas no completadas en MOD-021 | Rojo si mayor a 0 | Legal/Delegado, Gerencia |
| Acciones importantes y recomendadas abiertas | Igual, para esas dos categorias | Amarillo / gris | Responsable, Legal/Delegado |
| Nivel de madurez inicial de la organizacion | Regla propia (Inicial/En desarrollo/En consolidacion) | Rojo/amarillo/verde | Gerencia, Legal/Delegado |
| Dias desde el ultimo diagnostico cerrado | Hoy menos fecha de cierre de la ultima sesion | Verde/amarillo/rojo segun ciclo configurado | Administrador, Delegado |

### MOD-005 Plan de Cumplimiento (Version: MVP; dependencia estructural de MOD-020)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Avance del plan | Acciones Completada sobre total de la version Vigente | Verde mayor a 80%, amarillo 50-80%, rojo menor a 50% | Gerencia, Responsable, Legal, Auditor |
| Acciones criticas pendientes o vencidas | Conteo de prioridad Critica no Completada | Rojo si hay Vencida, amarillo si Pendiente sin vencer | Gerencia, Responsable, Legal |
| Dias promedio de retraso de acciones vencidas | Promedio de dias de retraso sobre las Vencidas | Verde 0, amarillo menor a 10 dias, rojo mayor o igual a 10 | Legal, Auditor |
| Acciones por modulo de ejecucion | Distribucion por modulo | Sin semaforo | Legal, Responsable de area |
| Vigencia de la version actual del plan | Fecha de aprobacion y version | Amarillo si mas de 90 dias sin recalculo | Administrador, Delegado, Auditor |

### MOD-006 RAT y Mapa de Datos (Version: MVP)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Cobertura del RAT | Fichas Vigentes sobre tratamientos detectados por el diagnostico | Verde mayor a 80%, amarillo 50-80%, rojo menor a 50% | Gerencia, Responsable, Legal, Auditor |
| Tratamientos por base de licitud | Distribucion por base de licitud elegida | Sin semaforo | Legal, Delegado |
| Tratamientos con dato sensible | Conteo con al menos una categoria sensible | Amarillo/rojo segun cobertura de EIPD | Legal, Delegado, Gerencia |
| Fichas pendientes de revision periodica | Conteo en "Requiere revision" | Verde 0, amarillo 1-5, rojo mayor a 5 | Responsable, Delegado |
| Transferencias posiblemente no documentadas | Alertas de la regla G.5 sin resolver | Verde 0, rojo mayor a 0 | Delegado, Legal, Auditor |
| Sistemas sin pais confirmado | Conteo con pais pendiente de confirmar | Amarillo/rojo segun cantidad | Seguridad/IT, Delegado |
| Antiguedad promedio del RAT | Dias desde la ultima revision confirmada | Verde menor a 180, amarillo 180-365, rojo mayor a 365 | Gerencia, Auditor |

### MOD-007 Consentimiento (Version: MVP)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Consentimientos vigentes por finalidad | Conteo agrupado por finalidad | Informativo | Gerencia, Responsable, Legal |
| Cobertura de captura | Tratamientos con base Consentimiento que ya tienen Consent vigente | Verde 100%, amarillo pendientes recientes, rojo mayor a 15 dias | Responsable, Gerencia |
| Revocaciones dentro de plazo | Cerradas a tiempo sobre total cerradas en el periodo | Verde 100%, amarillo 1 caso, rojo 2+ | Legal, Auditor, Gerencia |
| Consentimientos sensibles/biometricos incompletos | Presentados sin firma por mas de 2 dias | Rojo si mayor a 0 | Responsable, Legal |
| Evidencia disponible | Registros con snapshot y adjunto completos | Verde/amarillo/rojo | Auditor, Legal |

### MOD-008 Documentos y Politicas (Version: MVP)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Documentos regulatorios obligatorios vigentes | Conteo de los 3 tipos con version PUBLICADO/VIGENTE sobre 3 | Verde 3/3, amarillo 1-2/3, rojo 0/3 | Gerencia, Responsable/Legal, Auditor |
| Documentos con revision pendiente | Conteo en REQUIERE_REVISION | Amarillo si hay alguno, rojo si mas de 30 dias | Responsable/Legal, Gerencia |
| Tiempo promedio de aprobacion | Dias habiles EN_REVISION -> APROBADO | Sin semaforo | Gerencia, Legal |
| Ultima publicacion del Aviso de Privacidad | Fecha de la version vigente y dias transcurridos | Amarillo si supera el intervalo configurado | Responsable/Legal, Auditor |

### MOD-009 Proveedores y Encargados (Version: MVP)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Proveedores activos (total y por tipo) | Conteo ACTIVO por Encargado/Receptor/Subencargado | Informativo | Gerencia, Responsable |
| Proveedores sin contrato/DPA vigente vinculado | PENDIENTE_DE_CONTRATO o contrato vencido | Rojo si mayor a 0 | Responsable, Legal/Compliance |
| Contratos por vencer en 30 dias | Conteo con vencimiento proximo | Amarillo | Responsable, Gerencia |
| Proveedores fuera de El Salvador sin transferencia vinculada | Conteo sin registro activo en MOD-010 | Rojo | Legal/Compliance, Auditor |
| Proveedores con revision periodica vencida | Conteo EN_REVISION con fecha superada | Amarillo menor a 30 dias, rojo mayor o igual a 30 | Responsable, Auditor |
| Proveedores suspendidos por incidente | Conteo SUSPENDIDO | Rojo | Gerencia, Legal/Compliance, Seguridad/IT |
| Evidencia disponible por proveedor activo | Porcentaje con contrato, riesgo y revision al dia | Verde/amarillo/rojo | Auditor |

### MOD-010 Transferencias Internacionales (Version: V1)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Transferencias activas registradas | Conteo ACTIVA | Informativo | Gerencia, Responsable/Legal, Auditor |
| Transferencias pendientes de confirmar | Conteo DETECTADA_PENDIENTE_DE_CONFIRMAR | Verde 0, amarillo 1-4, rojo 5+ | Responsable, Legal, Gerencia |
| Transferencias sin evaluacion de pais completa | Conteo EN_EVALUACION_DE_PAIS mas de 10 dias habiles | Verde 0, amarillo 1-2, rojo 3+ | Legal, Auditor |
| Puestas en conocimiento a la ACE pendientes de envio | Conteo no enviado | Verde 0, amarillo 1-2, rojo 3+ | Delegado, Legal |
| Contratos de transferencia vencidos o por vencer | Conteo por vencer o vencidos | Verde/amarillo/rojo | Legal, Seguridad/IT, Gerencia |
| Cobertura de evidencia de transferencias | Porcentaje con expediente completo | Verde 90-100%, amarillo 70-89%, rojo menor a 70% | Auditor, Legal, Gerencia |

### MOD-011 ARCO-POL (Version: MVP; contribuye al "dashboard basico")

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Solicitudes abiertas por estado | Distribucion de expedientes activos | Sin semaforo | Gerencia, Responsable |
| Solicitudes proximas a vencer | Menos del 25%/10% del plazo restante | Amarillo/rojo | Responsable, Legal/Delegado |
| Solicitudes vencidas | Plazo aplicable ya cumplido sin resolucion | Rojo si mayor a 0 | Gerencia, Legal/Delegado, Auditor |
| Tiempo promedio de resolucion | Dias habiles admision -> cierre | Verde/amarillo/rojo segun plazo general | Legal/Delegado, Auditor |
| Solicitudes resueltas dentro del plazo legal aplicable | Porcentaje cerradas a tiempo | Verde/amarillo/rojo configurable | Gerencia, Legal/Delegado |
| Solicitudes con prevencion activa | Conteo en estado Prevenida | Sin semaforo | Responsable, Legal/Delegado |
| Reclamos ante la Direccion de Proteccion de Datos abiertos | Conteo sin informe remitido | Rojo si mayor o igual a 1 | Gerencia, Legal/Delegado, Auditor |
| Expedientes con evidencia completa vs incompleta | Porcentaje del checklist de evidencia esperada completo | Verde/amarillo/rojo | Auditor, Legal/Delegado |

### MOD-012 Portal del Titular (Version: V1)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Solicitudes recibidas por canal | Conteo con origen Portal sobre total del periodo | Informativo | Gerencia, Responsable ARCO-POL |
| Tiempo promedio hasta el primer triage | Horas envio -> apertura del expediente | Verde menor a 1 dia habil, amarillo 1-2, rojo mayor a 2 | Responsable ARCO-POL, Legal |
| Tasa de intentos de verificacion fallidos | Fallidos sobre total de intentos | Verde menor a 5%, amarillo 5-15%, rojo mayor a 15% | Seguridad/IT, Auditor |
| Disponibilidad del contenido publicado | Aviso/Politica mostrados = version vigente en MOD-008 | Verde al dia, rojo version vencida | Legal, Auditor |
| Cobertura de evidencia | Porcentaje de solicitudes del Portal con comprobante documentado en MOD-019 | Se muestra como evidencia disponible | Auditor |

### MOD-013 Incidentes de Seguridad (Version: MVP)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Incidentes abiertos por severidad | Conteo Reportado a Remediacion por severidad | Verde sin Alta/Critica, amarillo 1+ Alta, rojo 1+ Critica | Gerencia, Responsable |
| Cronometros de 72h por vencer | Conteo con menos de 24 horas restantes | Amarillo menor a 24h, rojo menor a 6h | Responsable, Gerencia |
| Casos con notificacion enviada dentro de plazo (12 meses) | Ratio sobre casos con notificacion requerida | Dato de estado, sin umbral de cumplimiento | Legal, Auditor |
| Tiempo promedio de cierre | Promedio de dias Reportado -> Cierre | Informativo | Responsable, Gerencia |
| Incidentes por origen | Distribucion interno/proveedor/terceros | Informativo | Legal, Auditor |
| Expedientes con documentacion incompleta (OBL-INC-04) | Riesgo=Si con campos incompletos | Rojo si mas de 72 horas en ese estado | Responsable, Legal |

### MOD-014 Riesgos y EIPD (Version: V1)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Tratamientos de alto riesgo evaluados | EIPD avanzadas sobre motivos de apertura detectados | Verde 1, amarillo si hay Detectado sin avanzar, rojo si vencida | Gerencia, Responsable, Legal, Auditor |
| EIPD vigentes | Conteo en estado VIGENTE | Informativo | Todas |
| EIPD pendientes de mitigacion (Alto/Critico) | Conteo EN_MITIGACION | Amarillo/rojo segun plazo de escalamiento | Gerencia, Responsable, Legal, Auditor |
| EIPD con revision atrasada | Conteo EN_REVISION con fecha vencida | Amarillo menor a 30 dias, rojo mayor a 30 dias | Gerencia, Responsable/Delegado, Auditor |
| Distribucion por nivel de riesgo | Conteo Bajo/Medio/Alto/Critico | Semaforo por franja | Gerencia, Legal, Auditor |
| Controles pendientes originados en una EIPD | Conteo en MOD-015 con origen EIPD | Amarillo/rojo segun escalamiento | Seguridad/IT, Gerencia |

### MOD-015 Controles de Seguridad (Version: MVP)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Controles con evidencia vigente | Implementado/Implementado con hallazgo sobre no archivados | Verde mayor o igual a 80%, amarillo 50-79%, rojo menor a 50% | Gerencia, Seguridad/IT, Legal/Delegado, Auditor |
| Controles obligatorios sin evidencia o vencidos (OBL-SEG-01 a 06) | Conteo pendiente o vencido | Rojo si mayor a 0 | Gerencia, Legal/Delegado, Seguridad/IT |
| Proximas revisiones (30 dias) | Conteo con revision proxima | Informativo | Seguridad/IT |
| Excepciones activas | Conteo No aplica-Exceptuado | Amarillo si hay pendientes de aprobar | Legal/Delegado, Aprobador, Gerencia |

### MOD-016 Retencion y Eliminacion (Version: V1)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Reglas de retencion activas | Conteo ACTIVO/PROXIMO A VENCER | Verde/amarillo/rojo segun SLA | Responsable, Legal |
| Eliminaciones pendientes de aprobacion | Conteo LISTO PARA ELIMINAR | Rojo si mayor a 0 y vencido el SLA | Legal, Gerencia, Responsable |
| Documentos de cumplimiento bajo retencion obligatoria | Conteo reglas documentales activas | Informativo | Auditor, Legal |
| Intentos bloqueados de eliminacion anticipada (90 dias) | Conteo de eventos de la automatizacion propia | Rojo si mayor a 0 | Auditor, Gerencia |
| Cobertura del motor de retencion | X de Y tratamientos con regla definida | Conteo, sin semaforo de porcentaje | Responsable, Legal, Gerencia |

### MOD-017 Capacitacion (Version: MVP)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Personal con capacitacion general vigente | X de Y personas con registro vigente | Amarillo si X menor a Y, rojo si hay Vencida | Gerencia, Delegado/Legal, Responsable de area, Auditor |
| Inducciones pendientes | Personas dadas de alta sin induccion completada | Rojo/amarillo segun plazo configurado | RRHH/Resp. de area, Delegado, Gerencia |
| Vencimientos proximos (30/60 dias) | Conteo Proxima a vencer | Amarillo, rojo si menos de 5 dias | Delegado, Responsable de area |
| Estado del plan anual de capacitacion e induccion | Estado cruzado con la bandera regimen_reforma_659 | Verde/amarillo/rojo/gris (no aplica) | Delegado, Gerencia, Auditor |
| Capacitacion por rol cubierta | Personas con registro de capacitacion por rol sobre total con ese rol | Amarillo/rojo segun brecha | Responsable de area, Delegado |

### MOD-018 Auditoria de Cumplimiento (Version: V1)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Estado de la ultima auditoria | Estado de la auditoria mas reciente | Verde/amarillo/rojo segun ciclo anual | Gerencia, Legal/Delegado, Resp. Legal/Compliance, Auditor, Seguridad/IT |
| Dias desde el cierre de la ultima auditoria | Hoy menos fecha de cierre | Verde menor a 300, amarillo 300-365, rojo mayor a 365 | Gerencia, Legal/Delegado |
| Hallazgos abiertos por severidad | Conteo Abierto/En correccion por severidad | Rojo si 1+ Critico | Legal/Delegado, Seguridad/IT, Gerencia |
| Acciones correctivas vencidas | Conteo con fecha limite pasada | Rojo si mayor a 0 | Legal/Delegado, Responsable de la accion, Gerencia |

### MOD-019 Centro de Evidencias (Version: MVP; dependencia estructural de MOD-020)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Evidencia disponible por obligacion aplicable | Porcentaje de obligaciones aplicables con evidencia Disponible | Verde 100% OBLIGATORIO, amarillo falta RECOMENDADO/CONDICIONAL, rojo falta OBLIGATORIO | Gerencia, Legal/Delegado, Auditor |
| Huecos de evidencia abiertos | Conteo Faltante por clasificacion | Rojo si 1+ OBLIGATORIO | Legal/Delegado, Gerencia, Auditor |
| Evidencia vencida o por vencer | Conteo Vencida mas proximos 30 dias | Rojo/amarillo | Seguridad/IT, Legal/Delegado, Gerencia |
| Paquetes de evidencia generados en el periodo | Conteo por tipo | Informativo | Legal/Delegado, Auditor, Gerencia |
| Tiempo promedio de aprobacion de evidencia manual | Promedio dias En revision -> Disponible | Verde menor a 5, amarillo 5-10, rojo mayor a 10 | Legal/Delegado, Administrador |

### MOD-020 Dashboard y Reportes: meta-indicadores propios de la herramienta (Version: ver seccion 14.8)

Los siguientes 3 indicadores no miden el programa de proteccion de datos de la empresa: miden el uso y la cobertura del propio Dashboard, y solo se muestran al Administrador (`MOD-020_ficha.md`, seccion M.2).

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Cobertura de indicadores activos | Conteo de modulos con al menos un indicador disponible sobre el total de 26 | Informativo, sin semaforo | Administrador |
| Fotos periodicas generadas a tiempo | Conteo de cierres mensuales generados en la fecha programada sobre el total programado en 12 meses | Amarillo si hubo 1 cierre con retraso, rojo si 2 o mas | Administrador |
| Reportes exportados en el periodo, por tipo | Conteo de exportaciones agrupado por reporte | Informativo, sin semaforo | Administrador |

Ademas, el "estado del programa por etapa y por cluster" (seccion 14.1.1) es un indicador de sintesis propio de MOD-020, sin modulo fuente unico (agrega varios), version MVP en su calculo por etapa y V1 en su calculo por cluster (ver seccion 14.8, coincide con la clasificacion Q de `MOD-020_ficha.md`).

### MOD-021 Centro de Tareas (Version: MVP; dependencia estructural de MOD-020)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Tareas pendientes | Pendiente + En proceso + Bloqueada | Verde/amarillo/rojo segun promedio historico | Responsable, Gerencia, Legal |
| Tareas vencidas | Conteo con bandera Vencida | Rojo si mayor a 0 | Gerencia, Responsable, Legal, Auditor |
| Aprobaciones pendientes | Conteo sin Decision, por dias en espera | Amarillo mayor a 3 dias, rojo mayor a 5 dias | Aprobador, Delegado/Resp. interno, Gerencia |
| Tiempo promedio de cierre por tipo de tarea | Promedio dias creacion -> completada | Sin semaforo | Legal, Gerencia |
| Cumplimiento de plazos operativos con plazo legal | Porcentaje completadas dentro de la fecha limite | Verde mayor o igual a 95%, amarillo 80-94%, rojo menor a 80% | Gerencia, Legal, Auditor |
| Tareas archivadas por cambio de regimen | Conteo acumulado desde la activacion de FUTURO | Informativo | Delegado/Resp. interno, Legal, Auditor |
| Carga de trabajo por responsable | Conteo de tareas activas por usuario | Amarillo si supera el umbral configurado | Administrador, Gerencia |

### MOD-022 Notificaciones (Version: MVP)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Notificaciones CRITICAL pendientes de acuse | Conteo Leida/Entregada CRITICAL sin Acuse | Rojo si mayor a 0 | Gerencia, Delegado/Resp. interno, Legal/Compliance, Auditor |
| Notificaciones escaladas en el periodo | Conteo con bandera Escalada por familia | Amarillo/rojo segun promedio historico | Gerencia, Administrador |
| Tasa de entrega fallida | Fallida tras reintentos sobre total enviado | Verde menor a 1%, amarillo 1-5%, rojo mayor a 5% | Administrador |
| Tiempo promedio de acuse en CRITICAL | Promedio entre entrega/lectura y acuse | Sin semaforo | Legal, Gerencia, Auditor |
| Notificaciones agrupadas vs individuales | Proporcion en resumen sobre el total | Informativo | Administrador |
| Roles criticos sin titular activo | Conteo de reglas con destinatario resuelto vacio | Rojo si mayor a 0 | Gerencia, Administrador, Auditor |

### MOD-023 Calendario y Motor de Plazos (Version: MVP)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Calendario del anio en curso y del proximo anio | Estado de la version (Vigente/Publicado/Borrador) | Verde/amarillo/rojo segun antelacion | Administrador, Gerencia, Auditor |
| Plazos legales actualmente en curso | Conteo por modulo de origen | Informativo | Gerencia, Delegado/Resp. interno, Legal |
| Plazos vencidos sin cerrar | Conteo con bandera Vencido | Rojo si mayor a 0 | Gerencia, Delegado/Resp. interno, Auditor |
| Recalculos aplicados (12 meses) | Conteo de eventos de recalculo | Informativo | Legal/Compliance, Auditor |
| Cobertura de fuente verificada en asuetos locales | Porcentaje de sucursales con fuente verificada en 24 meses | Verde 100%, amarillo 80-99%, rojo menor a 80% | Administrador, Auditor |
| Casos con criterio de computo ambiguo en su valor alternativo | Conteo de cambios de criterio por defecto | Amarillo si mayor a 0 | Legal/Compliance, Delegado/Resp. interno, Auditor |

### MOD-024 Centro Regulatorio (Version: MVP)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Estado regulatorio vigente | Badge ACTUAL/FUTURO con fecha del ultimo cambio | Informativo | Todas |
| Actualizaciones normativas pendientes de revision | Conteo de tareas "Revisar cambio normativo" no completadas | Verde 0, amarillo 1-2, rojo 3+ | Administrador, Delegado/Resp. Interno, Responsable Legal |
| Procedimientos sancionadores activos | Conteo distinto de CERRADO/PRESCRITO_ARCHIVADO | Rojo si hay uno con plazo vencido | Gerencia, Responsable Legal, Auditor |
| Dias habiles para la proxima obligacion del expediente sancionador activo | Minimo entre fechas limite del expediente | Colorea segun cercania | Responsable Legal, Administrador |
| Tramites ante la ACE pendientes de envio | Conteo BORRADOR/PENDIENTE_DE_ENVIO | Amarillo tras 15 dias, rojo tras 30 | Delegado/Resp. Interno, Administrador, Legal |
| Evidencia disponible del modulo | X de Y evidencias requeridas disponibles | Verde/amarillo/rojo | Auditor, Legal |
| Historial de sanciones y apercibimientos (RECOMENDADO) | Conteo acumulado de expedientes cerrados con sancion | Informativo | Legal, Auditor, Gerencia |
| Alertas activas del modulo | Conteo por nivel INFO/WARNING/HIGH/CRITICAL | Semaforo por nivel | Gerencia (HIGH/CRITICAL), Responsable Legal (todas) |

### MOD-025 Busqueda Global (Version: V2)

No aporta indicadores de estado del programa al Dashboard principal (`MOD-020_ficha.md`, seccion M.3.1: "No aporta indicadores de estado del programa al Dashboard principal"): sus 3 indicadores propios (consultas ejecutadas, proporcion sin resultados, volumen de consultas en ambito sensible) son de gestion interna de la propia busqueda y se muestran unicamente al Administrador, nunca en las 4 perspectivas de MOD-020.

### MOD-026 Centro de Ayuda (Version: MVP)

| Indicador | Formula (resumen) | Semaforo | Perspectiva(s) |
|---|---|---|---|
| Articulos de ayuda consultados en el periodo | Conteo de aperturas de la tarjeta de ayuda o del Glosario, agregado por modulo | Sin semaforo (informativo de adopcion) | Responsable (Administrador), Gerencia |
| Articulos marcados para revision pendientes | Conteo en estado MARCADO_PARA_REVISION | Verde 0, amarillo 1-3, rojo mas de 3 | Legal/Delegado, Auditor |
| Utilidad percibida del contenido | Votos "util" sobre el total, por cien; siempre acompanada de la aclaracion de que mide claridad del texto, no cumplimiento legal | Verde 80% o mas, amarillo 60-79%, rojo menos de 60% | Responsable (Administrador), Gerencia |
| Casos con sugerencia de asesoria juridica en el periodo | Conteo de tareas "Evaluar necesidad de asesoria externa" creadas por la automatizacion propia | Sin semaforo (informativo de riesgo acumulado) | Legal/Delegado, Gerencia |

Al igual que MOD-025, estos 4 indicadores de MOD-026 no miden el estado del programa de proteccion de datos de la empresa cliente: miden uso y calidad del contenido de ayuda, por lo que no aparecen en la sintesis por etapa o por cluster de la seccion 14.1.1, solo en este catalogo consolidado.

---

