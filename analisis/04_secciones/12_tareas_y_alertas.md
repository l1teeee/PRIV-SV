# 12. Sistema de tareas y alertas

Fecha de esta seccion: 2026-09-24. Fase: analisis funcional (prohibido codigo, SQL, APIs, esquemas de base de datos, nombres de tecnologias, stack o infraestructura).

Fuentes principales: `03_modulos/MOD-021_ficha.md` (Centro de Tareas), `03_modulos/MOD-022_ficha.md` (Notificaciones) y `03_modulos/MOD-023_ficha.md` (Calendario y Motor de Plazos), leidas completas como fuente principal de esta seccion; las secciones G (Automatizaciones) e I (Alertas) de las 26 fichas de `03_modulos/` (MOD-001 a MOD-026); `02_validacion/05_tipos_de_usuario.md` (los 12 roles estandar, seccion 5.3, y las reglas de separacion de funciones, seccion 5.4); `02_validacion/06_mapa_definitivo_de_modulos.md` (secciones 4 y 5, reglas de conexion de los modulos transversales y doble estado de la reforma 659); `02_validacion/mapa_modulos.json`; `02_validacion/04_objetivo_exacto_del_producto.md` (secciones 1.1 a 1.3, limites de lo que el sistema puede y no debe afirmar); `02_validacion/22_anti_features.md`; `01_legal/matriz_obligaciones.json` y `01_legal/03_hallazgos_regulatorios.md`. Todo OBL-ID citado en esta seccion es el ID canonico de `matriz_obligaciones.json` (formato OBL-AREA-NN, 105 obligaciones); ningun ID preliminar de `03_hallazgos_regulatorios.md` (por ejemplo OBL-AMBITO-xx u OBL-CONSENT-xx) se usa aqui.

Esta seccion no define funcionalidad nueva: consolida y cruza lo ya decidido en las fichas de los 26 modulos, en particular MOD-021, MOD-022 y MOD-023. Donde se propone algo que ninguna ficha define, queda marcado explicitamente como "propuesta de esta seccion, no presente en las fichas". Las contradicciones detectadas entre fuentes se resuelven segun la jerarquia: fuente legal primaria y `matriz_obligaciones.json` > `mapa_modulos.json` y `06_mapa_definitivo_de_modulos.md` > `05_tipos_de_usuario.md` (para roles) > ficha del modulo propietario > otras fichas; el detalle de cada eleccion queda al final, en "Contradicciones y huecos detectados".

Regla transversal heredada de todas las fuentes: el sistema orienta, explica, organiza, alerta, calcula, registra, documenta y genera evidencia; nunca decide cuestiones juridicas ni afirma cumplimiento legal. Ninguna pantalla de este sistema usa la expresion "porcentaje de cumplimiento legal" ni equivalente; se usa siempre estado del programa, controles configurados, tareas pendientes o evidencia disponible (`04_objetivo_exacto_del_producto.md`, seccion 1.2).

---

## 12.1 Modelo de tarea (MOD-021 Centro de Tareas)

MOD-021 es, por diseno, el unico lugar del sistema donde una obligacion detectada, un paso de un flujo o un hallazgo de auditoria se convierte en una accion concreta: titulo, fundamento, responsable, fecha limite, dependencia, evidencia requerida y estado. Ningun otro modulo mantiene su propia lista de pendientes; todos escriben aqui (MOD-021, seccion A). MOD-021 no es propietario de ninguna obligacion (ningun OBL-ID lo tiene como modulo propietario, por diseno explicito de `06_mapa_definitivo_de_modulos.md`, seccion 4, regla 5); es colaborador de OBL-INC-01, OBL-PLAZO-01, OBL-SANC-03, OBL-SANC-05 y OBL-SANC-06 (aloja la tarea con fecha y responsable, pero el fundamento y el estado del expediente los define siempre el modulo propietario correspondiente).

MOD-021 administra dos entidades: **Tarea** (Task) y **Aprobacion** (Approval).

### 12.1.1 Campos funcionales de la Tarea

| Campo | Tipo | Obligatorio u opcional | Notas funcionales |
|---|---|---|---|
| Titulo | Texto (maximo 140 caracteres) | Obligatorio siempre | Sugerido por el modulo de origen; libre para tareas manuales |
| Descripcion | Texto largo (maximo 2000 caracteres) | Opcional al crear, obligatorio antes de "En revision" | Explica en que consiste la tarea |
| Modulo de origen | Referencia | Obligatorio (autogenerado si no es manual) | Catalogo: MOD-002, MOD-004, MOD-005, MOD-006, MOD-008, MOD-009, MOD-011, MOD-013, MOD-014, MOD-016, MOD-017, MOD-018, MOD-024, o "Manual" |
| Obligacion relacionada | Lista de OBL-ID | Opcional; obligatorio si el origen la trae | Debe existir en `matriz_obligaciones.json`; una tarea puede sostener cero, uno o varios OBL-ID; se muestra como ayuda contextual, nunca en el lenguaje principal |
| Tipo de tarea | Seleccion unica | Obligatorio | Diagnostico, Plan de cumplimiento, ARCO-POL, Incidente, Documento, Proveedor, Riesgo/EIPD, Retencion, Capacitacion, Auditoria, Delegado/Responsable interno, Procedimiento sancionador, Regulatorio (cambio de regimen), Otra (manual) |
| Prioridad | Baja / Media / Alta / Critica | Obligatorio | Se sugiere automaticamente Alta o Critica cuando el plazo legal en curso queda a menos de 5 dias habiles (umbral configurable) |
| Responsable | Usuario | Obligatorio antes de "En proceso" | Filtrado por rol compatible con el tipo de tarea |
| Area o unidad responsable | Referencia a MOD-001 | Opcional (obligatorio en empresa mediana o corporativo) | Catalogo de sucursales/areas |
| Fecha de creacion | Fecha (autogenerada) | Obligatorio | No editable |
| Fecha limite | Fecha | Obligatorio si hay plazo legal o interno | Calculada por MOD-023 cuando hay plazo legal; ese campo queda bloqueado para edicion manual y solo MOD-023 puede recalcularlo |
| Criterio de computo mostrado | Texto (solo lectura, autogenerado) | Automatico cuando el plazo es ambiguo | "Dias habiles", "Horas corridas (criterio conservador)" u "Horas habiles"; ver 12.5 |
| Dependencia (tarea previa) | Lista de tareas | Opcional | No puede formar un ciclo |
| Evidencia requerida | Seleccion multiple | Obligatorio antes de "En revision" en Incidente, ARCO-POL, Delegado o Procedimiento sancionador; opcional en el resto | Documento adjunto, Captura de pantalla, Comprobante de envio/notificacion, Comprobante de pago, Acta de aprobacion, Otro |
| Archivos adjuntos | Archivo (lista) | Condicional | Tamano y tipo segun politica de la organizacion |
| Comentarios | Texto largo (bitacora) | Opcional | Con autor y fecha, no editable ni borrable |
| Estado | Ver 12.1.2 | Obligatorio (autogenerado en "Pendiente") | Ver diagrama de estados |
| Motivo de bloqueo | Texto | Obligatorio si Estado = Bloqueada | Con sugerencias predefinidas |
| Motivo de archivado ("no aplica") | Texto (autogenerado) | Obligatorio si Estado = No aplica | Generado por el sistema al activarse el cambio de regimen de la reforma 659, ver 12.7 |
| Es recurrente | Booleano (por defecto No) | Obligatorio | Si es Si, exige Periodicidad |
| Periodicidad | Mensual / Trimestral / Semestral / Anual / Cada 3 anos / Personalizada | Obligatorio si Es recurrente = Si | Requiere fecha base de referencia |
| Nivel de confidencialidad | Normal / Sensible / Muy sensible | Obligatorio | Limita quien puede ver la tarea ademas del responsable y el rol correspondiente; sostiene OBL-SENS-01 a OBL-SENS-08 |

**Campos precargados desde otros modulos.** Titulo, Descripcion, Modulo de origen, Obligacion relacionada, Tipo de tarea y, cuando aplica, Fecha limite llegan precargados desde el modulo que genera la tarea. El Responsable sugerido se precarga segun el rol por defecto de ese tipo de tarea, pero el Administrador o el propio responsable pueden reasignarla.

**Minimizacion de datos personales.** La Tarea nunca almacena el dato personal del titular en si: guarda una referencia al expediente correspondiente (por ejemplo, el numero de expediente ARCO-POL en MOD-011, o el numero de caso en MOD-013); cuando el proceso exige un adjunto puntual, ese adjunto vive en el expediente de origen y la Tarea solo referencia su existencia, nunca lo duplica. El campo "Nivel de confidencialidad" existe precisamente para distinguir una tarea administrativa de una que toca datos sensibles de un titular.

### 12.1.2 Campos funcionales de la Aprobacion

| Campo | Notas funcionales |
|---|---|
| Tarea relacionada | Obligatorio; debe estar en "En revision" |
| Tipo de aprobacion | Documento, Acto del Delegado/Responsable interno (prevencion, incompetencia, notificacion a receptores, revocacion), Cierre de incidente, Resultado de EIPD/riesgo, Respuesta ARCO-POL sensible, Plan de accion correctiva sancionador, Otra |
| Rol requerido | Delegado/Responsable interno, Legal/Compliance, Aprobador, Administrador (doble control); autogenerado segun el tipo |
| Aprobador asignado | Usuario con el rol requerido; no puede coincidir con quien dejo la tarea en revision, salvo pyme bajo el umbral, con advertencia |
| Fecha de solicitud / Fecha de resolucion | Autogeneradas, no editables |
| Decision | Aprobada / Devuelta con cambios / Rechazada |
| Comentario de la decision | Obligatorio si Devuelta o Rechazada |
| Identidad del aprobador | Autogenerada, con fecha y hora; equivale a una firma dentro del sistema |
| Version del objeto aprobado | Obligatorio cuando el tipo es "Documento": la version exacta de MOD-008 |

### 12.1.3 Estados y transiciones de la Tarea

```
                         +-------------+
              +--------->|  PENDIENTE  |
              |          +------+------+
              |                 |
              | reapertura      | responsable inicia el trabajo
              |                 v
              |          +-------------+      falta un insumo      +-------------+
              |          | EN PROCESO  |-------------------------->|  BLOQUEADA  |
              |          +------+------+                           +------+------+
              |                 |                                          |
              |     listo para revision                     se resuelve el bloqueo
              |                 v                                          |
              |          +-------------+<---------------------------------+
              |          | EN REVISION |
              |          +------+------+
              |            /          \
              |   aprobador aprueba    aprobador devuelve o rechaza
              |          v                          \
              |   +-------------+                    v
              |   |  APROBADA   |             (regresa a EN PROCESO)
              |   +------+------+
              |          |
              |  se confirma evidencia final
              |          v
              |   +-------------+
              +---| COMPLETADA  |  (estado terminal, puede reabrirse)
                  +------+------+
                         |
          la obligacion deja de aplicar (cambio de regimen en MOD-024)
                         v
                  +-------------+
                  |  NO APLICA  |  (estado terminal archivado, nunca se borra)
                  +-------------+

Bandera paralela, no excluyente con los estados anteriores (salvo COMPLETADA y NO APLICA):
  si la fecha limite se cumple sin que la tarea llegue a COMPLETADA o NO APLICA,
  la tarea se marca visualmente VENCIDA (se muestra en rojo, sigue su flujo normal
  desde el estado en que estaba). El vencimiento nunca se oculta ni se borra del
  historial, aunque la tarea despues se complete (ver 12.5.3).
```

Reglas clave de transicion (tabla completa en `MOD-021_ficha.md`, seccion F.2):

- De "En proceso" a "En revision" exige evidencia cargada cuando el tipo de tarea la requiere, y descripcion completa.
- De "En revision" a "Aprobada" exige que el aprobador no sea la misma persona que envio a revision (bloqueo tecnico de autorrevision), salvo en organizaciones por debajo del umbral configurable de pyme (propuesta inicial: 50 empleados), donde se permite con advertencia visible de "autorrevision" (`05_tipos_de_usuario.md`, seccion 5.4).
- Ninguna tarea se aprueba a si misma de forma automatica: la Aprobacion siempre requiere una persona identificada con el rol correspondiente.
- El paso a "No aplica" solo lo dispara, de forma automatica, el cambio de bandera `regimen_reforma_659` de MOD-024 sobre tipos de tarea exclusivos del regimen anterior, con confirmacion visible del Administrador; ningun otro motivo de "ya no aplica" se automatiza (ver 12.7 y seccion H de MOD-021).
- Nunca se elimina una tarea ni su historial: solo se archiva o se marca "No aplica" (`22_anti_features.md`, item 19).

### 12.1.4 Dependencias entre tareas

Una tarea puede declarar otra tarea como dependencia previa (campo "Dependencia" de 12.1.1); el sistema valida que esa relacion no forme un ciclo antes de guardar. Mientras la tarea previa no llegue a "Completada" o "No aplica", la tarea dependiente permanece en "Bloqueada" con el motivo autogenerado correspondiente. Cuando una tarea con dependientes pasa a "No aplica" por el cambio de regimen (ver 12.7), cualquier otra tarea que la tuviera como dependencia recibe una alerta para que su responsable decida si tambien deja de aplicar o si necesita una tarea de reemplazo; esa decision nunca se automatiza (MOD-021, seccion F, "Registros vinculados").

### 12.1.5 Evidencia requerida y aprobacion humana obligatoria

Toda tarea de tipo Incidente, ARCO-POL, Delegado/Responsable interno o Procedimiento sancionador exige, antes de pasar a "En revision", al menos un tipo de evidencia del catalogo (documento adjunto, captura, comprobante de envio o de pago, acta de aprobacion, u otro). La Aprobacion es una entidad separada, nunca un simple cambio de estado: registra quien decidio, cuando y con que comentario, y para los actos hoy atribuidos al Delegado (prevencion, incompetencia, notificacion a receptores, revocacion) exige doble control cuando la organizacion supera el umbral de pyme, de modo que quien redacto el borrador (el sistema o un colaborador) no sea la misma persona investida como Delegado que lo aprueba. Ninguna Aprobacion se resuelve por si sola: el sistema nunca marca "Aprobada" una tarea de forma automatica (MOD-021, seccion H).

### 12.1.6 Tareas con plazo legal frente a tareas internas

El campo "Fecha limite" distingue dos origenes posibles, con tratamiento distinto:

| | Tarea con plazo legal | Tarea interna (sin plazo legal) |
|---|---|---|
| Quien calcula la fecha limite | Siempre MOD-023 Calendario y Motor de Plazos (nunca MOD-021 por su cuenta) | El propio modulo de origen o el usuario, con dias por defecto segun prioridad (por ejemplo, MOD-005 usa 5 dias habiles para Critica, 10 para Importante/Recomendada) |
| Edicion manual de la fecha | Bloqueada; solo MOD-023 puede recalcularla | Permitida, con justificacion registrada si se cambia |
| Ejemplos | Respuesta ARCO-POL (20+20 dias habiles, OBL-ARCO-10), notificacion de vulneraciones (72 horas, OBL-INC-01), comunicacion del nombramiento del Delegado a la ACE (15 dias habiles, OBL-DPO-03) | "Completar el catalogo de sistemas", "Revisar proveedor X", tareas creadas manualmente |
| Que pasa si vence | Queda con bandera VENCIDA visible de forma permanente en el historial, nunca se oculta (ver 12.5.3); dispara alertas segun el catalogo de 12.3 | Igual bandera visual, pero sin la misma escalada legal; el escalamiento sigue las reglas configurables de la tarea |
| Ayuda contextual mostrada | El "criterio de computo mostrado" (dias habiles, horas corridas u horas habiles) siempre visible junto a la fecha, con la advertencia de incertidumbre juridica cuando aplica (ver 12.5) | No aplica ese campo |

La distincion no cambia el modelo de datos de la Tarea (es el mismo campo Fecha limite en ambos casos): lo que cambia es quien la calcula, si se puede editar a mano, y que ayuda contextual y que catalogo de alertas se activan.

### 12.1.7 Separacion de funciones y bloqueo de autorrevision

Quien crea o ejecuta una tarea nunca puede aprobarla a si mismo cuando esa tarea tiene una Aprobacion asociada: el sistema bloquea la accion "Aprobar" si el usuario conectado es el mismo que dejo la tarea en "En revision", salvo en organizaciones por debajo del umbral configurable (propuesta inicial: 50 empleados), donde se permite con una advertencia visible de "autorrevision". El rol Auditor (interno o externo) es siempre de solo lectura, nunca puede aprobar ni cerrar una tarea. Las aprobaciones que hoy corresponden al Delegado (prevencion, incompetencia, notificacion a receptores, revocacion) exigen doble control cuando la organizacion supera el umbral: quien redacto el borrador no es la misma persona investida como Delegado que lo aprueba (`05_tipos_de_usuario.md`, seccion 5.4; MOD-021, seccion C).

---

## 12.2 Catalogo de reglas de generacion de tareas por modulo

Esta tabla consolida las reglas de automatizacion (seccion G de cada ficha) que terminan en la creacion de una Tarea (o una Aprobacion) dentro de MOD-021. No repite aqui las automatizaciones de cada modulo que no generan tarea (por ejemplo, calculos internos o validaciones de guardado): esas quedan en la ficha propia. Cuando la fecha limite proviene de un plazo legal, la columna "Plazo y quien lo calcula" cita el OBL-ID y confirma que el calculo lo hace siempre MOD-023 (regla de conexion 3 de `06_mapa_definitivo_de_modulos.md`); cuando no hay plazo legal, se indica el criterio interno (por defecto configurable) y quien lo fija. MOD-021, MOD-022, MOD-023 y MOD-025 no aparecen como filas de origen en este catalogo: MOD-021 es el destino de todas las filas; MOD-022 solo entrega el aviso, nunca crea la tarea; MOD-023 solo calcula la fecha, nunca decide crear la tarea; MOD-025 es de solo lectura y no genera tareas ni escribe en otras entidades (regla de conexion 5).

### 12.2.1 MOD-001 Organizacion y Personas

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| Se invita a un usuario | Correo valido, rol seleccionado | "Completar perfil" | El usuario invitado | Interno, sin plazo legal; recordatorio de invitacion configurable |
| Se agrega un pais distinto de El Salvador en "paises donde opera", o se da de alta una sucursal en el exterior | Ninguna adicional | "Revisar si esto implica una transferencia internacional de datos" (enlace a MOD-010) | Delegado/Responsable interno | Interno, sin plazo legal; la empresa puede desactivar la sugerencia |
| Se intenta dar de baja al unico titular de un rol critico (Delegado, Seguridad, Administrador) | No existe reemplazo | Bloqueo de la accion hasta asignar reemplazo, o confirmacion explicita registrada | Administrador | No aplica (validacion de integridad, no un plazo) |

### 12.2.2 MOD-002 Delegado / Responsable Interno de Datos

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| El registro pasa a NOMBRADO | Ninguna | "Notificar al Delegado su nombramiento" | Administrador de la organizacion | 3 dias habiles desde el nombramiento (OBL-DPO-02, Art. 8 Lineamientos DPO); calcula MOD-023 |
| El registro pasa a NOTIFICADO_INTERNAMENTE | Ninguna | "Comunicar el nombramiento a la ACE" | Administrador de la organizacion | 15 dias habiles (OBL-DPO-03, Arts. 10 y 12 Lineamientos DPO); calcula MOD-023, capa 5 (autoridad) |
| Se edita un campo de contacto o modalidad de un registro ACTIVO ya comunicado a la ACE | El registro fue comunicado previamente | "Actualizar el tramite ante la ACE" | Administrador de la organizacion | 10 dias habiles (Art. 10 inciso final Lineamientos DPO); calcula MOD-023 |
| Faltan 30 dias para cumplir 3 anos desde el nombramiento o la ultima reverificacion | El registro esta ACTIVO | "Reverificar perfil del Delegado" | Delegado/Responsable interno | 3 anos, plazo legal (OBL-DPO-04, Art. 18 Lineamientos DPO); calcula MOD-023, margen de aviso configurable |
| Faltan 30 dias para cumplir 1 ano desde la ultima capacitacion del Delegado | Ninguna | "Renovar capacitacion anual del Delegado" | Delegado/Responsable interno | 1 ano, plazo legal (OBL-DPO-05, Art. 22 Lineamientos DPO); calcula MOD-023 |
| Transcurren 6 meses desde el ultimo informe periodico | Ninguna | "Elaborar informe periodico al responsable" | Delegado/Responsable interno | 6 meses, minimo legal (OBL-DPO-07, Art. 30 Lineamientos DPO); calcula MOD-023, la empresa puede acortarlo, no alargarlo |
| Se registra fecha_cese del Delegado | Ninguna | "Designar sustituto" | Administrador de la organizacion | 10 dias habiles (Art. 19 Lineamientos DPO); calcula MOD-023 |
| La bandera `regimen_reforma_659` de MOD-024 cambia a FUTURO | Existe registro ACTIVO | "Revisar si mantiene esta figura de forma voluntaria" | Administrador de la organizacion | Interno, sin plazo legal (ver 12.7) |

### 12.2.3 MOD-003 Onboarding

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| Se responde "no estoy seguro" a si la empresa necesita Delegado (Paso 4) | Ninguna | "Resolver si su empresa necesita designar un Delegado de Proteccion de Datos" (CRITICAL) | Administrador | Interno, sin plazo legal propio; referencia a los Arts. 15 y 17 |
| Se agrega un usuario con rol Delegado, o se responde "ya designado"/"designarlo ahora" en el Paso 4 | Ninguna | Crea el registro inicial en MOD-002 en "designacion en curso" | Administrador | Siembra en MOD-023 el conteo de 15 dias habiles de OBL-DPO-03 desde que MOD-002 confirme el nombramiento |
| El onboarding pasa a COMPLETADO | Siempre | "Completar el Diagnostico de Cumplimiento" | Administrador | Interno, sin plazo legal |

### 12.2.4 MOD-004 Diagnostico de Cumplimiento

Cada respuesta afirmativa del cuestionario guiado dispara, ademas del tratamiento sugerido en el RAT (MOD-006), una tarea en MOD-021; la tabla completa de 30 filas vive en `MOD-004_ficha.md`, seccion G.2. Filas representativas (todas con destino unico hacia MOD-021, seccion G.2, nota de dependencias):

| Disparador (pregunta) | Tarea generada | Responsable por defecto | OBL-ID | Prioridad |
|---|---|---|---|---|
| P-PER-04 (biometria laboral) | "Registrar consentimiento por escrito y ofrecer alternativa no biometrica" | Responsable de area (RRHH) | OBL-SENS-06, OBL-SENS-07, OBL-CONS-04 | CRITICA |
| P-CLI-01 (datos de clientes) | "Completar la ficha de RAT del tratamiento de clientes" | Responsable de area | OBL-DOC-02 | CRITICA (plazo transitorio OBL-PLAZO-03/04 ya vencido) |
| P-TEC-02 (confirmar pais del proveedor cloud) | "Confirmar el pais donde el proveedor almacena los datos y documentar la transferencia" | Responsable de area / IT | OBL-TRANSF-01, OBL-TRANSF-03, OBL-TRANSF-05 | CRITICA |
| P-SEN-02 (datos geneticos) | "Elaborar EIPD para el tratamiento de datos geneticos" | Delegado/Responsable interno | OBL-DOC-03, OBL-SENS-04 | CRITICA |
| P-MEN-01 (menores de edad) | "Activar el subflujo de consentimiento parental" | Responsable de area | OBL-PRIN-04, OBL-CONS-06 | CRITICA |
| P-GOB-01 (sin Delegado nombrado) | "Designar formalmente un Delegado o responsable interno y comunicarlo a la ACE en 15 dias habiles" | Administrador | OBL-DPO-01, OBL-DPO-03 | CRITICA |
| P-SEG-04 (posible incidente ya ocurrido) | "Evaluar de inmediato si el hecho declarado activa el flujo de Incidentes y sus plazos de notificacion" (alerta CRITICAL inmediata) | Delegado, Responsable de Seguridad/IT | OBL-INC-01, OBL-INC-02, OBL-INC-04 | CRITICA |
| P-EMP-07 (posible operador de infraestructura critica) | "Confirmar ante la ACE si la empresa esta calificada como operador de infraestructura critica" | Administrador | OBL-INC-05 | Segun G.1, la calificacion es exclusiva de la ACE |

Plazo y quien lo calcula (todas las filas anteriores): la fecha limite de cada tarea la calcula MOD-023 cuando la obligacion citada trae un plazo legal propio (por ejemplo, la reverificacion o comunicacion del Delegado); cuando la obligacion no tiene plazo legal propio, MOD-005 asigna dias por defecto segun el nivel de prioridad al momento de trasladar la accion al Plan de Cumplimiento (ver 12.2.5).

### 12.2.5 MOD-005 Plan de Cumplimiento

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| Version del plan aprobada como Vigente | La accion esta en estado Pendiente | Tarea equivalente en MOD-021, con el mismo responsable y fecha limite, enlazada de vuelta a la accion | El de la accion del plan | Si la obligacion tiene plazo legal ya vencido: fecha de generacion + dias por defecto del nivel (Critica: 5 dias habiles; Importante/Recomendada: 10 dias habiles), calculados por MOD-023; si no tiene plazo legal propio, igual criterio por defecto |
| MOD-024 confirma un cambio de estado de vigencia sobre una obligacion con acciones activas (por ejemplo, activacion del estado FUTURO) | La obligacion afectada tiene acciones en el plan Vigente | Recalculo de las acciones ligadas, pendiente de revision de Delegado y Legal antes de publicarse | Delegado/Responsable interno, Legal/Compliance | No en el disparo; la publicacion del recalculo siempre exige aprobacion humana |

### 12.2.6 MOD-006 RAT y Mapa de Datos

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| Se marca "Informacion biometrica" en una ficha | Ninguna | "Confirmar consentimiento escrito y alternativa no biometrica" (enlace a MOD-007) | Responsable de area | Interno, sin plazo legal propio |
| Se registra un tratamiento de "camaras de seguridad" | Ninguna | "Verificar el aviso de videovigilancia visible" (enlace a MOD-008) | Responsable de area | Interno |
| Se marca transferencia fuera de El Salvador sin ficha en MOD-010 | El tratamiento pasa a Vigente sin ficha en MOD-010 | "Crear el registro de transferencia en MOD-010" | Responsable de area, con copia a Legal/Compliance | Interno; el plazo de la tarea es configurable |
| Llega la fecha de proxima revision de una ficha Vigente | Automatico (MOD-023) | Tarea de revision, ficha pasa a "Requiere revision" | Responsable de area, con notificacion al Delegado | Periodicidad de buena practica (por defecto 12 meses), configurable; MOD-023 calcula la fecha |
| Una ficha pasa a Vigente con "Requiere EIPD: Si" confirmado | Ninguna | "Elaborar EIPD para este tratamiento" | Delegado/Responsable interno (enlace a MOD-014) | Interno |
| Una ficha pasa a Vigente y el tratamiento involucra un encargado | Ninguna | Verificar contrato/DPA vigente en MOD-009; si no existe, se crea la tarea | Responsable de area | Interno |

### 12.2.7 MOD-007 Consentimiento

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| El RAT marca un tratamiento con base juridica = Consentimiento | No existe registro Consent vigente | "Capturar consentimiento" | Responsable de area | Interno, sin plazo legal propio |
| Se registra una solicitud de revocacion | Ninguna | Tarea de ejecucion de la revocacion | Responsable ARCO-POL y Delegado/Responsable interno | 5 dias habiles (OBL-CONS-03, Art. 30 inc. 1 LPDP); calcula MOD-023 |
| Se ejecuta una revocacion | El tratamiento tiene al menos un encargado registrado | "Notificar la revocacion al encargado" | Responsable de Proveedores/IT | 5 dias habiles adicionales (OBL-CONS-03, Art. 30 inc. 2 LPDP); calcula MOD-023 |
| Se cumple la fecha de vigencia declarada de una finalidad | El consentimiento sigue Vigente | Tarea de revision del consentimiento expirado | Responsable de area | Interno, activable si la empresa usa vigencias por finalidad |

### 12.2.8 MOD-008 Documentos y Politicas

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| MOD-006 registra una finalidad nueva no mencionada en el Aviso vigente | El Aviso publicado no la menciona | "Actualizar Aviso de Privacidad: nueva finalidad detectada" | Legal/Compliance (configurable) | Interno, sin plazo legal propio; el disparo en si no es desactivable (OBL-AVISO-04, Art. 7) |
| MOD-009 registra o modifica un encargado | El Aviso publicado no lo lista en el literal h) | Tarea de revision del aviso | Legal/Compliance (configurable) | Interno (OBL-AVISO-02, OBL-PROV-04) |
| MOD-024 cambia la bandera a FUTURO | Existe un Aviso PUBLICADO/VIGENTE | "Revisar avisos publicados tras el cambio de regimen" | Delegado/Responsable interno | Interno, sin plazo legal; ver 12.7 |
| Transcurre el intervalo de revision periodica desde la ultima publicacion | El documento esta PUBLICADO/VIGENTE | Tarea de revision, documento pasa a REQUIERE_REVISION | Legal/Compliance | Periodicidad configurable por tipo de documento (por ejemplo 12 meses) |

Nota de fuente: aunque `mapa_modulos.json` no declara `alimenta_a` de MOD-008 hacia MOD-021, la propia seccion G de `MOD-008_ficha.md` (reglas 1 a 3) describe explicitamente la creacion de estas tareas; esta tabla sigue la ficha propietaria de MOD-008 (ver "Contradicciones y huecos detectados", punto 3).

### 12.2.9 MOD-009 Proveedores y Encargados

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| Fecha de vencimiento del contrato/DPA | Faltan 30 dias (luego 7 dias) | Tarea de renovacion | Responsable de area, con copia al Delegado | Interno, dias de anticipacion configurables |
| Llega la fecha de proxima revision periodica | Automatico (MOD-023) | "Revisar proveedor X" | Responsable de area | Periodicidad configurable; calcula MOD-023 |
| MOD-007 marca la revocacion de un consentimiento vinculado a un tratamiento con encargado ACTIVO | Ninguna | "Notificar la revocacion a [Encargado]" | Delegado/Responsable interno (aprueba antes de enviarse) | 5 dias habiles (OBL-CONS-03, Art. 30); calcula MOD-023 |
| MOD-011 cierra un caso de rectificacion, actualizacion o eliminacion con receptores previos | Existe al menos un Tercero/Receptor vinculado | "Notificar a [Receptor]" | Responsable de area (Proveedores) | 5 dias habiles (OBL-ARCO-11, Art. 21 inc. 3 LPDP); calcula MOD-023 |
| Proveedor pasa a RELACION_FINALIZADA con clausula de devolucion/eliminacion pactada | Campo D.3 = "Si" | "Verificar devolucion o eliminacion de datos" (obligatoria antes de CERRADO) | Responsable de area | Interno (OBL-PROV-07) |

### 12.2.10 MOD-010 Transferencias Internacionales

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| Se crea o edita un proveedor/encargado/receptor en MOD-009 con pais distinto de El Salvador | Ninguna | Registro DETECTADA_PENDIENTE_DE_CONFIRMAR mas tarea de confirmacion | Responsable de area que dio de alta el proveedor, con copia a Legal/Compliance | Interno |
| MOD-004 marca "trata datos fuera de El Salvador: si" para un tratamiento | El tratamiento no tiene transferencia vinculada | "Registrar la transferencia correspondiente" | Responsable de area | Interno |
| Se marca base juridica "Consentimiento previo" sin Consent vinculado | Ninguna | "Capturar consentimiento especifico para esta transferencia" | Responsable de area | Interno; bloquea el paso a PENDIENTE_DE_APROBACION |
| Transferencia pasa a PENDIENTE_DE_APROBACION, tipo Internacional | Siempre | Genera el borrador de "puesta en conocimiento a la ACE" en MOD-024 | Delegado/Responsable interno | Sin plazo legal expreso para el envio en si (Art. 45 LPDP); el borrador queda pendiente de enviar |
| Se aprueba una solicitud ARCO-POL sobre un tratamiento con transferencias ACTIVAS | Automatico | "Notificar la rectificacion/eliminacion al receptor" | Responsable de area | 5 dias habiles (OBL-ARCO-11 colaboradora); calcula MOD-023 |

### 12.2.11 MOD-011 ARCO-POL

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| Se completa el registro de una solicitud con los 7 elementos del Art. 18 | Ninguna | Expediente pasa a Admitida; "Resolver solicitud" | Responsable ARCO-POL | 20 dias habiles (OBL-ARCO-10, Art. 20 LPDP); calcula MOD-023 |
| Se completa el registro sin uno o mas de los 7 elementos | Ninguna | Borrador de prevencion | Responsable ARCO-POL | 10 dias habiles (OBL-ARCO-08, Art. 18 LPDP); calcula MOD-023 |
| Se determina procedencia de rectificacion, cancelacion u olvido con receptores vinculados | Existe registro de transferencia/receptor en MOD-009/MOD-010 | Lista de receptores a notificar | Responsable ARCO-POL | 5 dias habiles por cada receptor (OBL-ARCO-11, Art. 21 inc. 3); calcula MOD-023 |
| Se aprueba una denegatoria | Ninguna | Tarea de notificacion de la denegatoria | Responsable ARCO-POL | 3 dias habiles (OBL-ARCO-12, Art. 22 LPDP); calcula MOD-023 |
| Se declara incompetencia | Ninguna | Borrador de devolucion | Responsable ARCO-POL | 5 dias habiles (OBL-ARCO-09, Art. 19 LPDP); calcula MOD-023 |
| Se registra un reclamo del titular ante la Direccion de Proteccion de Datos | Dentro de 10 dias habiles de notificada la resolucion | "Preparar informe de actuaciones" | Delegado/Responsable interno | Interno (referencia OBL-ARCO-14) |
| El expediente pasa a Cerrada | Ninguna | Calcula fecha sugerida de fin de retencion, la envia a MOD-016 | No aplica (calculo automatico) | Cierre + 5 anos por defecto (OBL-RET-05, criterio recomendado); ajustable por Legal si otra norma exige mas |

### 12.2.12 MOD-012 Portal del Titular

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| Titular envia el formulario completo | Todos los campos obligatorios validos, identidad adjunta | Crea la Solicitud ARCO-POL en MOD-011 (Recibida, origen Portal) | Se asigna al triage de MOD-011 | El plazo lo hereda la solicitud creada en MOD-011 (ver 12.2.11) |
| Intentos de verificacion fallidos superan el umbral (5, configurable) | Ninguna | Bloqueo temporal del origen, mas alerta de seguridad | Responsable de Seguridad/IT | Interno |

Nota: el Portal no crea una entidad de tarea propia distinta de la que ya crea MOD-011; solo es el canal de entrada del formulario (ver 12.8 y `MOD-012_ficha.md`, seccion A.1).

### 12.2.13 MOD-013 Incidentes de Seguridad

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| Se registra la fecha de conocimiento de una vulneracion | Siempre | Inicia el cronometro de notificacion y el de revision exhaustiva, ambos en paralelo | Responsable de Seguridad/IT | 72 horas cada uno (OBL-INC-01 notificacion; OBL-INC-02 inicio de revision, Art. 25 y Art. 25 inc. 2 LPDP); calcula MOD-023, criterio por defecto horas corridas |
| Se marca "existe riesgo = Si" | Al entrar a Evaluacion | Bloquea el avance a Decision hasta completar los campos de OBL-INC-04 | Responsable de Seguridad/IT | Interno (documentacion obligatoria del incidente) |
| Se completan los campos de naturaleza, datos comprometidos, acciones correctivas y medios de contacto | En estado Decision | Genera los dos borradores de notificacion (ACE/FGR y titulares), pendientes de aprobacion | Delegado/Responsable interno (aprueba) | Contenido minimo de OBL-INC-03 (Art. 25 incisos a-e) |
| Se marcan categorias Biometrica o Salud sin EIPD registrada | Durante Evaluacion o Investigacion | "Evaluar si corresponde EIPD" (enlace a MOD-014) | Delegado/Responsable interno | Interno |
| Se cierra el caso | Estado Cierre alcanzado | Calcula fecha de conservacion del expediente, la envia a MOD-016 | No aplica (calculo automatico) | Cierre + minimo recomendado (OBL-RET-05) |
| Se registra una medida correctiva nueva en "Lecciones aprendidas" | Ninguna | Crea o actualiza un Control en MOD-015 | Responsable de Seguridad/IT | Interno |

### 12.2.14 MOD-014 Riesgos y EIPD

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| MOD-004 marca biometria, salud, menores o camaras, o MOD-006 marca dato sensible/gran escala/transferencia | No existe EIPD vigente o en curso para ese tratamiento | "Completar cuestionario de riesgo" | Responsable de area | 15 dias habiles por defecto, configurable; interno |
| El riesgo calculado es Alto o Critico sin mitigacion registrada | Ninguna | Bloquea el paso a PENDIENTE_DE_APROBACION; tarea de mitigacion | Responsable de Seguridad/IT o de area | Interno |
| Se registra una mitigacion sin control equivalente en MOD-015 | Ninguna | Crea un Control "pendiente de implementar" | Responsable de Seguridad/IT | Interno |
| La EIPD pasa a PENDIENTE_DE_APROBACION | Ninguna | Tarea de aprobacion | Aprobador o Delegado/Responsable interno | Interno, con recordatorio periodico |
| La EIPD es aprobada (VIGENTE) | Ninguna | Calcula fecha de proxima revision | No aplica (calculo automatico) | 12 meses por defecto, ajustable por politica de la empresa; MOD-023 |
| Llega la fecha de proxima revision, o el RAT reporta cambio material en el tratamiento vinculado | La EIPD esta VIGENTE | Tarea de revision, pasa a EN_REVISION | Responsable de la evaluacion original | MOD-023 calcula la fecha periodica |

### 12.2.15 MOD-015 Controles de Seguridad

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| Se completa el diagnostico inicial | Primera vez | Crea el catalogo base de controles en "Pendiente de implementar" | Responsable de Seguridad/IT | Interno, catalogo fijo |
| MOD-014 necesita un control que no existe en el catalogo | Ninguna | Crea el registro en "Pendiente de implementar" | Responsable de Seguridad/IT | Interno |
| Faltan N dias para la proxima fecha de revision (30, 15 o 7, configurable) | Ninguna | Tarea de revision | Responsable del control | Periodicidad por tipo de control, ajustable; MOD-023 calcula la fecha |
| Se registra una excepcion | Estado pasa a "No aplica - Exceptuado" | Tarea de aprobacion de la excepcion | Aprobador | Interno |

### 12.2.16 MOD-016 Retencion y Eliminacion

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| Se da de alta un tratamiento sensible o con proveedor fuera del pais sin regla de retencion | Ninguna | "Definir regla de retencion para este tratamiento" | Responsable de area, con copia al Delegado | Interno |
| Se publica una nueva version del Aviso de Privacidad | Automatico | Crea la regla de retencion documental (10 anos desde la publicacion) | No aplica (calculo automatico) | 10 anos (OBL-RET-04); no desactivable |
| Un expediente ARCO-POL o de incidente cambia a "cerrado" | Automatico | Crea o actualiza la regla de retencion (cierre + 5 anos por defecto) | No aplica (calculo automatico) | 5 anos por defecto (OBL-RET-05); ajustable por Legal, solo para extender |
| La regla llega a "LISTO PARA ELIMINAR" | No existe otro fundamento que la retenga | Tarea de aprobacion de la eliminacion | Aprobador, con copia al Delegado | Interno |
| Se aprueba la eliminacion | Estado "APROBADO PARA ELIMINAR" | Tarea de ejecucion tecnica | Responsable de area o Seguridad/IT | Interno |
| Se presenta una solicitud ARCO-POL de cancelacion/olvido y existe una regla en "RETENIDO POR OBLIGACION" | Ninguna | Borrador de denegatoria parcial motivada, para revision del Delegado | Delegado/Responsable interno | Interno (Art. 22, OBL-ARCO-06) |

### 12.2.17 MOD-017 Capacitacion

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| Se da de alta un nuevo usuario en MOD-001 | Siempre | Induccion de personal nuevo | Responsable de area (RRHH) | 30 dias desde el alta por defecto, configurable; interno |
| Un usuario cambia a un rol con capacitacion por rol asociada | Existe un programa Vigente para ese rol | Registro de capacitacion programada | La persona con el nuevo rol | Interno |
| Se cumple la fecha de proxima renovacion (menos dias de anticipacion) | El programa tiene periodicidad de renovacion | Tarea de renovacion | La persona | Interno, dias de anticipacion configurables |
| Se acerca el aniversario del ultimo Plan anual publicado (o nunca existio uno), bajo bandera ACTUAL | Existe un Delegado/Responsable interno activo | "Elaborar/actualizar el plan anual de capacitacion e induccion" | Delegado/Responsable interno | 1 ano (OBL-CAP-02, Art. 22 Lineamientos DPO); calcula MOD-023; deja de exigir la tarea recordatoria bajo el estado FUTURO sin Delegado voluntario (ver 12.7) |
| Se cierra un incidente con una leccion aprendida que senala necesidad de capacitacion | El usuario que cierra el caso lo marca | Tarea sugerida de capacitacion | Delegado o Responsable de Seguridad/IT | Interno; nunca crea el programa automaticamente |

### 12.2.18 MOD-018 Auditoria de Cumplimiento

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| Se cierra una auditoria (o se completa el diagnostico inicial si nunca hubo una) | Siempre | Crea el siguiente registro de auditoria en "Planificada" | Delegado/Responsable interno | Periodicidad de 12 meses (OBL-AUD-01, Politicas ACE Art. 8 lit. b), configurable solo hacia mas frecuente; calcula MOD-023 |
| Se registra un hallazgo con severidad Alta o Critica | Siempre | Tarea de plan de accion correctiva | Responsable senalado en el hallazgo | 15 dias habiles (Critica) o 30 dias habiles (Alta), configurable; interno |

### 12.2.19 MOD-019 Centro de Evidencias

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| MOD-004 confirma que una obligacion OBLIGATORIO aplica sin evidencia registrada | Ninguna | Sugiere tarea de carga de evidencia | Responsable de area | Interno |
| Una Evidencia con fecha de vigencia llega a 30 dias de vencer | Siempre | Tarea de renovacion | Responsable de carga original | Dias de anticipacion configurables; interno |
| Se genera un paquete de evidencia (EvidencePackage) con destinatario externo | Siempre | Exige tarea de segundo control antes de habilitar la exportacion | Aprobador designado como segundo control | Interno, no desactivable |

### 12.2.20 MOD-020 Dashboard y Reportes

MOD-020 no genera tareas: es de solo lectura sobre los indicadores que ya produce cada modulo de origen, consistente con su `alimenta_a: []` en `mapa_modulos.json` y con la regla de conexion 5 de `06_mapa_definitivo_de_modulos.md`.

### 12.2.21 MOD-024 Centro Regulatorio

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| La bandera `regimen_reforma_659` cambia de ACTUAL a FUTURO (o se revierte) | Ninguna | "Revisar el impacto del cambio de regimen normativo" (una por organizacion) | Administrador (ademas emite el evento hacia MOD-002, MOD-007, MOD-008, MOD-011, MOD-015 y MOD-017, ver 12.7) | Interno, sin plazo legal |
| Se publica una nueva `RegulatoryRuleVersion` sobre un instrumento existente | Ninguna | "Revisar cambio normativo: [instrumento]" | Administrador, Delegado/Responsable interno, Responsable Legal | Interno |
| Se registra `fecha_notificacion_recibida` de un procedimiento sancionador | Ninguna | "Contestar emplazamiento de la ACE" (prioridad maxima) | Responsable Legal/Compliance | 5 dias habiles (OBL-SANC-05, Art. 21 Normativa PAS); calcula MOD-023 |
| Un expediente sancionador llega a RESUELTO con sancion | Ninguna | Tarea de pago de multa; tareas por cada medida adicional ordenada | Administrador (pago); Responsable de area segun la medida | 15 dias habiles para el pago (OBL-SANC-06, Art. 44 Normativa PAS); calcula MOD-023 |
| Una resolucion sancionatoria queda FIRME | Ninguna | "Monitorear publicacion de la resolucion en el sitio de la ACE" (informativa) | Responsable Legal/Compliance | Interno (OBL-SANC-08, Art. 55 LPDP) |

### 12.2.22 MOD-026 Centro de Ayuda

| Disparador | Condicion | Tarea generada | Responsable por defecto | Plazo y quien lo calcula |
|---|---|---|---|---|
| El usuario hace clic en "necesito ayuda juridica" de un articulo de alerta, o abre 3 o mas articulos de ese tipo en la misma sesion (umbral configurable por el proveedor) | Ninguna | "Evaluar necesidad de asesoria externa para [caso/modulo]" | Delegado/Responsable interno o Legal/Compliance | Interno; nunca invita por su cuenta a un Asesor externo |

---

## 12.3 Catalogo consolidado de alertas (secciones I)

Toda alerta de negocio de este sistema llega al destinatario final por MOD-022 Notificaciones, que decide canal, escalamiento y frecuencia (12.4); esta tabla organiza, por modulo emisor, las alertas que cada ficha declara en su propia seccion I. La columna "Plazo legal" marca con **Si (OBL-ID)** las alertas que sostienen un plazo de la matriz de obligaciones (estas nunca se pueden silenciar ni agrupar en un resumen, ver 12.4.6); el resto son buena practica o riesgo operativo, marcadas **No**.

### 12.3.1 MOD-001 Organizacion y Personas

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Organizacion incompleta | 3 dias desde el alta sin completar campos minimos | WARNING | Administrador | Plataforma + correo | 3 y 7 dias | No escala | Organizacion pasa a ACTIVA | No |
| Rol critico sin titular | Ningun usuario activo con rol critico (Administrador, Delegado, Seguridad) | HIGH | Administrador | Plataforma + correo | Semanal | A Gerencia a los 15 dias | Se asigna el rol | No |
| Invitacion pendiente de aceptar | Usuario invitado no activa su cuenta | INFO | Administrador | Plataforma | 15 y 30 dias | No escala | Se acepta o se cancela | No |
| Umbral de separacion de funciones alcanzado | Empleados > 50 sin separacion activada | WARNING | Administrador | Plataforma + correo | Mensual | A Legal a los 30 dias | Se activa, o se documenta la decision | No |
| Baja de unico titular de rol critico sin reemplazo | Se intenta dar de baja sin reemplazo | CRITICAL | Administrador y Delegado | Plataforma + correo (+ SMS si configurado) | Inmediata | A Gerencia en 24 horas | Se asigna reemplazo o se cancela | No |
| Estructura sin actualizar | Sin cambios de usuarios/roles/sucursales en 6 meses | INFO | Administrador, Seguridad/IT | Plataforma | Por periodo | No escala | Hay cambio o confirmacion | No |

### 12.3.2 MOD-002 Delegado / Responsable Interno de Datos

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Falta nombrar Delegado/Responsable Interno | No hay registro ACTIVO al cierre del onboarding | CRITICAL | Administrador | Plataforma + correo | Diaria | A Aprobador a los 5 dias habiles | Existe registro ACTIVO | Si (OBL-DPO-01) |
| Notificacion interna por vencer / vencida | Faltan 1 dia, o vencio, de los 3 dias habiles | WARNING / HIGH | Administrador (vencida: + Aprobador) | Plataforma + correo | Una vez / diaria | A Aprobador | Tarea completada | Si (OBL-DPO-02) |
| Comunicacion a la ACE por vencer / vencida | Faltan 3 dias, o vencio, de los 15 dias habiles | WARNING / CRITICAL | Administrador, Delegado (vencida: + Legal) | Plataforma + correo | Una vez / diaria | Visible en dashboard de Gerencia | Tramite marcado Enviado | Si (OBL-DPO-03) |
| Reverificacion proxima a vencer / vencida | Faltan 30 dias, o vencio, de los 3 anos | INFO/WARNING / HIGH | Delegado, Administrador (+ Legal si vencida) | Plataforma + correo | Semanal | A Aprobador a los 10 dias sin atender | Reverificacion aprobada | Si (OBL-DPO-04) |
| Capacitacion anual del Delegado proxima a vencer | Faltan 30 dias del ciclo anual | INFO/WARNING | Delegado | Plataforma + correo | Semanal | A Administrador a los 10 dias | Capacitacion registrada | Si (OBL-DPO-05) |
| Informe periodico pendiente | Pasaron 6 meses sin informe | WARNING | Delegado, Administrador | Plataforma + correo | Mensual | A Legal a los 30 dias de retraso | Informe registrado | Si (OBL-DPO-07) |
| Sustituto no designado tras cese | Vencen 10 dias habiles sin nuevo NOMBRADO | CRITICAL | Administrador, Aprobador | Plataforma + correo | Diaria | Visible en dashboard de Gerencia | Nuevo registro NOMBRADO | No |
| Cambio de estado regulatorio (reforma 659) | Bandera cambia a FUTURO | INFO | Administrador, Delegado, Legal | Plataforma + correo | Una vez | No aplica | Se confirma lectura | No |
| Confidencialidad post-cese proxima a expirar | Faltan 60 dias de los 5 anos desde el cese | INFO | Legal, Administrador | Plataforma | Una vez | No aplica | Pasa a ARCHIVADO | Si (OBL-DPO-06) |

### 12.3.3 MOD-003 Onboarding

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Bienvenida: configure su organizacion | Cuenta creada, sin iniciar | INFO | Administrador | Correo + plataforma | Una vez, recordatorio 48h | Ninguno | Entra a EN_PROGRESO | No |
| Configuracion inicial incompleta | Sin avance 5 dias (configurable) | WARNING | Administrador | Correo + plataforma | Cada 5 dias, hasta 3 | Ninguno | Avanza o finaliza | No |
| Debe resolver si necesita Delegado | Respuesta "no estoy seguro" | CRITICAL | Administrador (+ Delegado si invitado) | Plataforma + correo | Cada 7 dias | Visible en dashboard de Gerencia a los 15 dias habiles | Se registra Delegado o decision documentada | Si (referencia OBL-DPO-03) |
| Invitacion de usuario pendiente | Invitacion no aceptada | INFO/WARNING | Administrador | Correo + plataforma | 5 y 10 dias | Se marca vencida a los 30 dias | Se acepta | No |
| Onboarding abandonado | Estado ABANDONADO | WARNING | Administrador | Correo | Una vez, luego semanal | Ninguno | Se reingresa | No |

### 12.3.4 MOD-004 Diagnostico de Cumplimiento

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Diagnostico nunca iniciado | Onboarding completo hace mas de 7 dias sin sesion | WARNING | Administrador | Plataforma + correo | Una vez, luego semanal | A Delegado a los 21 dias | Se inicia la sesion | No |
| Sesion estancada | Sin actividad mas del umbral (15 dias) | WARNING | Responsable del bloque, Administrador | Plataforma + correo | Semanal | A Delegado a los 30 dias | Se retoma o se cierra | No |
| Acciones criticas sin asignar | Cierre con accion CRITICA sin tarea asignada | HIGH | Delegado/Responsable interno | Plataforma + correo | Diaria | A Administrador a los 5 dias | Todas quedan asignadas | No |
| Posible incidente no reportado detectado | Respuesta P-SEG-04 = Si | CRITICAL | Delegado, Seguridad/IT | Plataforma + correo inmediato | Inmediata | A Administrador de inmediato | Se abre el expediente en MOD-013 | Si (referencia OBL-INC-01) |
| Solicitud ARCO-POL previa sin gestionar | Respuesta P-GOB-04 = Si | CRITICAL | Delegado, Responsable ARCO-POL | Plataforma + correo inmediato | Inmediata | A Legal de inmediato | Se registra el caso en MOD-011 | Si (referencia OBL-ARCO-08/10) |
| Re-diagnostico recomendado por antiguedad | Diagnostico cerrado hace mas de 12 meses | INFO | Administrador, Delegado | Plataforma | Una vez | No escala | Se inicia re-diagnostico | No |
| Cambio de estado regulatorio con diagnostico bajo el estado anterior | MOD-024 activa FUTURO | WARNING | Delegado/Responsable interno | Plataforma + correo | Una vez | A Administrador a los 10 dias | Tareas afectadas revisadas | No |

### 12.3.5 MOD-005 Plan de Cumplimiento

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Plan pendiente de aprobacion | Mas de 2 dias habiles en Generado/En revision | INFO/WARNING | Aprobador, Administrador | Plataforma + correo | Cada 3 dias habiles | A Gerencia a los 5 dias habiles | Se aprueba o rechaza | No |
| Accion proxima a vencer | 5 dias (Critica) o 10 dias (Importante/Recomendada) antes del limite | WARNING | Responsable asignado | Plataforma + correo | Diaria | A Delegado si es Critica y quedan 2 dias | Se completa o cambia fecha | Depende (hereda el OBL-ID de la accion, si lo tiene) |
| Accion critica vencida | Fecha limite superada, prioridad Critica | HIGH | Responsable, Delegado | Plataforma + correo | Diaria | A Gerencia a los 5 dias; CRITICAL a los 15 | Se completa o descarta | Idem |
| Multiples acciones criticas vencidas | Umbral configurable (default 3) | CRITICAL | Administrador, Gerencia | Plataforma + correo | Al cruzar el umbral, luego semanal | No escala mas alla de Gerencia | Vuelve bajo el umbral | No |
| Plan desactualizado | Cambian respuestas del diagnostico sin recalcular en 5 dias habiles | WARNING | Administrador, Delegado | Plataforma | Cada 5 dias habiles | A Legal a los 15 dias | Se recalcula | No |
| Cambio normativo con impacto en el plan | MOD-024 confirma cambio sobre obligacion con acciones activas | HIGH | Delegado, Legal | Plataforma + correo | Una vez | A Administrador a los 10 dias | Se revisa y publica el recalculo | No |

### 12.3.6 MOD-006 RAT y Mapa de Datos

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Ficha pendiente de completar | Borrador mas de 15 dias sin avanzar | INFO | Responsable de area | Plataforma + resumen semanal | Semanal | A Delegado a los 30 dias | Avanza o se archiva | No |
| Ficha esperando aprobacion | En revision mas de 5 dias habiles | WARNING | Aprobador o Legal | Plataforma + correo | Cada 3 dias habiles | A Delegado a los 10 dias habiles | Pasa a Vigente o se rechaza | No |
| Revision periodica vencida | Fecha alcanzada sin confirmar | WARNING | Responsable de area, Delegado | Plataforma + correo | Semanal | A Administrador a los 30 dias | Se confirma o actualiza | No |
| Transferencia posiblemente no documentada | Tratamiento con transferencia sin ficha en MOD-010 | HIGH | Delegado, Legal | Plataforma + correo | Al detectar, luego semanal | A Administrador a los 15 dias | Se crea la ficha o se corrige | No |
| Sistema dado de baja con tratamientos vigentes | Sistema del catalogo cambia de estado | HIGH | Responsable de area, Seguridad/IT | Plataforma + correo | Inmediata | A Delegado a los 10 dias | Se reconfirma con el sistema correcto | No |
| RAT sin ninguna ficha Vigente 30 dias tras el diagnostico | Sin ficha Vigente pese a diagnostico completo | CRITICAL | Administrador, Delegado | Plataforma + correo + dashboard Gerencia | Una vez, luego quincenal | Al resumen ejecutivo de Gerencia a los 45 dias | Existe al menos una ficha Vigente | Si (OBL-DOC-02) |

### 12.3.7 MOD-007 Consentimiento

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Consentimiento pendiente de captura | Sin registro vigente X dias tras el RAT | INFO | Responsable de area | Plataforma | Semanal si persiste | A Delegado a los 15 dias | Se captura o se marca No otorgado | No |
| Consentimiento sensible incompleto | Sin firma adjunta mas de 2 dias | WARNING | Responsable de area, Delegado | Plataforma + correo | Diaria | A Administrador a los 5 dias | Se adjunta firma | Si (OBL-SENS-01/07) |
| Revocacion proxima a vencer / vencida (primer plazo) | Faltan 2 dias, o vencio, de los 5 dias habiles de ejecucion | WARNING / CRITICAL | Responsable ARCO-POL, Delegado (vencida: + Administrador, dashboard Gerencia) | Plataforma + correo | Diaria | A Administrador si falta 1 dia | Se ejecuta la revocacion | Si (OBL-CONS-03, Art. 30 inc. 1) |
| Notificacion a encargado proxima a vencer / vencida (segundo plazo) | Faltan 2 dias, o vencio, de los 5 dias habiles de notificacion | WARNING / CRITICAL | Responsable Proveedores/IT, Delegado | Plataforma + correo | Diaria | A Administrador si falta 1 dia | Se notifica al encargado | Si (OBL-CONS-03, Art. 30 inc. 2) |
| Version de Aviso no disponible | Se intenta capturar consentimiento sin version publicada del Aviso | CRITICAL | Delegado, Administrador | Plataforma | Al intento | Inmediato | Existe version publicada | No |
| Consentimiento biometrico sin alternativa ofrecida | Se guarda sin alternativa no biometrica | WARNING | Responsable de area, Legal | Plataforma | Al guardar | A Delegado si se repite | Es nota de riesgo permanente, no bloquea | Si (OBL-SENS-07) |

### 12.3.8 MOD-008 Documentos y Politicas

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Aviso de Privacidad sin publicar | Sin version PUBLICADO/VIGENTE pese a tratamientos activos | CRITICAL | Administrador, Delegado | Plataforma + correo | Diaria | A Aprobador a los 5 dias habiles | Existe version PUBLICADO/VIGENTE | Si (OBL-AVISO-01, Art. 24) |
| Documento pendiente de aprobacion | Mas de 5 dias habiles en EN_REVISION | WARNING | Aprobador(es) | Plataforma + correo | Al vencer, cada 2 dias habiles | A Administrador a los 10 dias habiles | Se aprueba o rechaza | No |
| Documento requiere revision | Pasa a REQUIERE_REVISION | WARNING | Legal, Delegado | Plataforma + correo | Una vez, recordatorio semanal | A Administrador a los 15 dias | Se publica nueva version o se archiva | No |
| Aviso no menciona un encargado nuevo | MOD-009 registra encargado no listado | HIGH | Delegado, Legal | Plataforma + correo | Una vez | A Administrador a los 5 dias habiles | Se publica version que lo incluye | Si (OBL-AVISO-02) |
| Cambio de regimen 659: revisar avisos publicados | MOD-024 activa FUTURO | WARNING | Delegado, Administrador | Plataforma + correo | Una vez | Si no hay avance en 30 dias | Todos los avisos quedan revisados | No |
| Documento proximo a su revision periodica | Faltan 30 dias | INFO | Autor original, Legal | Plataforma | Una vez, luego semanal ultima semana | Se convierte en "requiere revision" al llegar la fecha | Se publica nueva version o se pospone | No |

### 12.3.9 MOD-009 Proveedores y Encargados

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Contrato/DPA proximo a vencer (30 dias) | Faltan 30 dias | WARNING | Responsable de area, Delegado | Plataforma + correo | Una vez, semanal | A Aprobador si faltan 7 dias | Se renueva o se cierra la relacion | No |
| Contrato/DPA proximo a vencer (7 dias) | Faltan 7 dias | HIGH | Responsable de area, Delegado, Aprobador | Plataforma + correo | Diaria | A Administrador si vence | Idem | No |
| Contrato/DPA vencido sin renovar | Fecha superada | CRITICAL | Delegado, Administrador | Plataforma + correo | Diaria | Automatico desde HIGH | Se renueva o se cierra | Si (OBL-PROV-01, Art. 33 inc. 2) |
| Proveedor activo sin evaluacion de riesgo vigente | Periodo maximo superado | WARNING | Delegado | Plataforma | Mensual | -- | Nueva evaluacion registrada | No |
| Incidente de seguridad grave vinculado | Evento desde MOD-013, severidad Alta/Critica | CRITICAL | Delegado, Seguridad/IT, Administrador | Plataforma + correo (+ push si configurado) | Inmediata | Al Aprobador de forma automatica | El incidente se cierra en MOD-013 | No |
| Relacion finalizada sin verificar devolucion/eliminacion | Mas de 30 dias en RELACION_FINALIZADA sin constancia | WARNING | Responsable de area, Delegado | Plataforma | Semanal | A Administrador a los 60 dias | Se adjunta constancia o se justifica | Si (OBL-PROV-07) |
| Subencargado sin documento de sometimiento propio | Alta sin documento vinculado | HIGH | Delegado, Legal | Plataforma | Al detectar, semanal | -- | Se vincula o se archiva con justificacion | Si (OBL-PROV-05, verificada: false) |

### 12.3.10 MOD-010 Transferencias Internacionales

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Transferencia detectada sin confirmar | Alta de proveedor/encargado con pais distinto de El Salvador | WARNING | Responsable de area, Legal | Plataforma + correo | Al crear, semanal | A Delegado a los 15 dias habiles | Se confirma o se descarta | No |
| Sin evaluacion de pais completa | Mas de 10 dias habiles en EN_EVALUACION_DE_PAIS | HIGH | Legal, Delegado | Plataforma + correo | Diaria | A Administrador a los 20 dias habiles | Evaluacion registrada | No |
| Sin consentimiento especifico vinculado | Base = Consentimiento previo sin Consent enlazado | HIGH | Legal, Responsable de area | Plataforma + correo | Al avanzar de estado, cada 5 dias | A Delegado a los 10 dias habiles | Se vincula Consent vigente | Si (OBL-TRANSF-04) |
| Contrato de transferencia proximo a vencer / vencido | Faltan 30 dias / vencio | WARNING / CRITICAL | Legal, Seguridad/IT (vencido: + Delegado, Aprobador) | Plataforma + correo (+ push) | Semanal / diaria | A Aprobador (30 dias) / a Administrador (vencido) | Contrato vigente o transferencia suspendida | No |
| Puesta en conocimiento a la ACE pendiente de envio | Borrador sin marcar enviado 15 dias habiles | WARNING | Delegado | Plataforma + correo | Semanal | A Administrador a los 30 dias habiles | Se marca enviada o se documenta imposibilidad | Si (Art. 45 LPDP) |
| Transferencia huerfana | Se elimina el tratamiento o receptor vinculado | HIGH | Delegado, Legal | Plataforma + correo | Inmediata, semanal | A Administrador a los 10 dias habiles | Se revincula o pasa a FINALIZADA | No |

### 12.3.11 MOD-011 ARCO-POL

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Solicitud nueva sin responsable | Recibida sin Responsable ARCO-POL asignado | WARNING | Administrador, Delegado | Plataforma + correo | Cada 24 horas | A Delegado a las 24 horas | Se asigna responsable | No |
| Prevencion proxima a vencer | Faltan 3 dias de los 10 dias habiles | WARNING | Responsable ARCO-POL | Plataforma + correo | Diaria | A Delegado si falta 1 dia habil | Se subsana o se archiva | Si (OBL-ARCO-08, Art. 18) |
| Plazo general proximo a vencer / vencido | Faltan 5 dias, o vencio, de los 20 (o 40 con prorroga) dias habiles | HIGH / CRITICAL | Responsable ARCO-POL, Delegado (vencido: + Administrador) | Plataforma + correo | Diaria | A Gerencia (dashboard) si vence | Se cierra el expediente (el vencimiento queda registrado permanentemente) | Si (OBL-ARCO-10, Art. 20) |
| Notificacion a receptores pendiente | Faltan 2 dias de los 5 dias habiles | WARNING | Responsable ARCO-POL | Plataforma | Diaria | A Delegado si falta 1 dia | Todos los receptores notificados | Si (OBL-ARCO-11, Art. 21 inc. 3) |
| Denegatoria pendiente de notificar | Faltan dias de los 3 dias habiles | HIGH | Responsable ARCO-POL | Plataforma + correo | Diaria | A Delegado en el ultimo dia habil | Se notifica al titular | Si (OBL-ARCO-12, Art. 22) |
| Incompetencia pendiente de devolver | Faltan dias de los 5 dias habiles | WARNING | Responsable ARCO-POL | Plataforma + correo | Diaria | A Delegado si falta 1 dia habil | Se notifica la devolucion | Si (OBL-ARCO-09, Art. 19) |
| Reclamo recibido de la Direccion de Proteccion de Datos | Se registra reclamo en el expediente | CRITICAL | Delegado, Legal, Administrador | Plataforma + correo | Inmediata | A Gerencia | Se remite el informe de actuaciones | Si (OBL-ARCO-14) |
| Solicitud pendiente de aprobacion del Delegado | Borrador listo sin aprobar X dias | WARNING | Delegado/Responsable interno | Plataforma + correo | Diaria | A Administrador a los 2 dias sin aprobar | Se aprueba o rechaza | No |
| Retencion del expediente proxima a vencer | Faltan 90 dias de los 5 anos sugeridos | INFO | Administrador, Auditor | Plataforma | Unica | No escala | Se conserva o se purga | No |

### 12.3.12 MOD-012 Portal del Titular

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Nueva solicitud recibida via Portal | Envio exitoso del formulario | INFO | Responsable ARCO-POL | Plataforma + correo | Inmediata | A Delegado si no hay triage en 24 horas | Se abre el expediente en MOD-011 | No |
| Intentos de verificacion fallidos superan el umbral | 5 intentos (configurable) | WARNING | Seguridad/IT, Responsable ARCO-POL | Plataforma + correo | Inmediata | A HIGH y al Delegado si se repite en 24 horas | Se revisa y cierra | No |
| Solicitud del Portal sin triage cerca del vencimiento de la prevencion | A 2 dias habiles del limite de 10 dias habiles | HIGH | Responsable ARCO-POL, Delegado | Plataforma + correo | Diaria | Al Aprobador | Cambia de estado en MOD-011 | Si (OBL-ARCO-08) |

### 12.3.13 MOD-013 Incidentes de Seguridad

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Cronometro de notificacion - aviso temprano | 50% del plazo de 72h consumido | WARNING | Seguridad/IT, Delegado | Plataforma + correo | Una vez | A Administrador si no hay accion en 6 horas | Notificacion enviada, o caso Descartado | Si (OBL-INC-01) |
| Cronometro de notificacion - critico | 6 horas restantes | CRITICAL | Delegado, Administrador, Aprobador | Plataforma + correo (+ SMS si configurado) | Cada hora | Inmediato a Gerencia | Notificacion enviada | Si (OBL-INC-01) |
| Plazo de notificacion vencido | 72 horas cumplidas sin notificar | CRITICAL | Administrador, Delegado, Legal | Plataforma + correo | Diaria | Gerencia General | Nunca se apaga del todo: el incumplimiento queda registrado de forma permanente aunque la alerta activa deje de repetirse | Si (OBL-INC-01) |
| Cronometro de revision - inicio pendiente | 60 horas sin marcar inicio de revision | WARNING | Seguridad/IT | Plataforma + correo | Una vez | A Delegado a las 70 horas | Pasa a Investigacion | Si (OBL-INC-02) |
| Documentacion incompleta con riesgo confirmado | Se intenta avanzar sin campos de OBL-INC-04 | HIGH (bloqueante) | Seguridad/IT | Plataforma | Cada intento | No aplica (bloqueo) | Se completan los campos | Si (OBL-INC-04) |
| Incidente en proveedor sin evidencia de aviso | Origen Proveedor sin registro de aviso | WARNING | Seguridad/IT, Responsable de Proveedores | Plataforma + correo | Una vez | A Legal al 80% del plazo | Se registra el aviso o avanza con nota | No |
| Caso cerrado con notificacion tardia | Se cierra un caso con hito de notificacion vencido | INFO (registro para auditoria) | Auditor interno, Legal | Plataforma | Una vez | No aplica | No se apaga: marca permanente en reportes | Si (referencia OBL-INC-01) |

### 12.3.14 MOD-014 Riesgos y EIPD

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Tratamiento de alto riesgo sin EIPD | Factor de riesgo detectado sin cuestionario completo en plazo | WARNING/HIGH | Responsable de area | Plataforma + correo | Diaria si vencida | A Delegado a los 5 dias habiles | Pasa a EVALUADO | No |
| EIPD con riesgo Alto/Critico pendiente de mitigacion | Entra a EN_MITIGACION | HIGH | Seguridad/IT o de area, Delegado | Plataforma + correo | Cada 3 dias habiles | A Aprobador/Gerencia a los 10 dias habiles | Se registra mitigacion y se recalcula el residual | No |
| EIPD pendiente de aprobacion | Entra a PENDIENTE_DE_APROBACION | WARNING | Aprobador, Delegado | Plataforma + correo | Semanal | A Administrador a los 15 dias habiles | Pasa a VIGENTE o se rechaza | No |
| EIPD proxima a vencer | Faltan 30 dias de la revision periodica | INFO/WARNING/HIGH | Delegado, responsable original | Plataforma + correo | 30 dias unica, semanal si vencida | A Administrador a los 30 dias habiles de vencida | Se completa la revision | No |
| Cambio material en tratamiento con EIPD vigente | RAT reporta cambio de categoria, volumen, finalidad, encargado o transferencia | CRITICAL | Delegado, Responsable de area, Legal | Plataforma + correo inmediato | Unica | Inmediata a Legal | Entra a EN_REVISION y se confirma o recalcula | No |
| EIPD rechazada | Aprobador la rechaza | WARNING | Responsable original, Delegado | Plataforma + correo | 10 dias habiles | A Delegado a los 15 dias habiles | Se reabre | No |
| Control pendiente de implementar generado desde EIPD | Se crea un control desde una mitigacion | WARNING | Seguridad/IT | Plataforma + correo | Semanal | A Delegado a los 30 dias habiles | Pasa a "implementado" | No |

### 12.3.15 MOD-015 Controles de Seguridad

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Proxima revision de un control | Faltan 30 dias | INFO | Responsable del control | Plataforma | Una vez | No escala | Se confirma o cambia de estado | No |
| Revision urgente de un control | Faltan 7 dias | WARNING | Responsable del control | Plataforma + correo | Cada 3 dias | A Administrador a los 5 dias sin respuesta | Idem | No |
| Control vencido | Estado cambia a Vencido | HIGH | Responsable del control, Delegado | Plataforma + correo | Diaria | A Legal/Delegado y Gerencia a los 15 dias | Vuelve a Implementado | No |
| Control obligatorio sin evidencia | Un control del catalogo base sigue "pendiente" mas de 30 dias | HIGH | Seguridad/IT, Delegado | Plataforma + correo | Semanal | A Gerencia a los 60 dias, con referencia a riesgo de infraccion grave | Se implementa o se aprueba una excepcion | Si (OBL-SEG-06) |
| Excepcion pendiente de aprobacion | Se registra una excepcion | WARNING | Aprobador | Plataforma | Cada 3 dias | A Administrador a los 10 dias | Se aprueba o rechaza | No |
| Hallazgo detectado en revision | Control pasa a Implementado con hallazgo | WARNING | Responsable del control, Legal si es OBLIGATORIO | Plataforma | Una vez, semanal mientras siga abierto | A Gerencia a los 30 dias si es OBLIGATORIO | Se corrige y se aprueba | No |

### 12.3.16 MOD-016 Retencion y Eliminacion

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Regla proxima a vencer | Entra a PROXIMO A VENCER (30 dias antes) | WARNING | Responsable de area, Delegado | Plataforma + correo | Una vez, semanal | A Delegado a los 15 dias | Cambia de estado | No |
| Eliminacion pendiente de aprobacion | Pasa a LISTO PARA ELIMINAR | HIGH | Aprobador, Delegado | Plataforma + correo | Cada 5 dias habiles | A Administrador a los 10 dias habiles | Se aprueba, rechaza o cambia de estado | No |
| Eliminacion aprobada sin ejecutar | 5 dias (configurable) desde APROBADO PARA ELIMINAR | HIGH | Responsable de area o Seguridad/IT, Delegado | Plataforma + correo | Diaria | A Delegado a los 10 dias | Se confirma la ejecucion | No |
| Intento de eliminar antes del plazo minimo documental | Intento de forzar sobre OBL-RET-04/05 | CRITICAL | Delegado, Legal, Administrador | Plataforma + correo | Inmediata | No aplica (ya es notificacion del intento) | Se cierra el registro del intento | Si (OBL-RET-04/05) |
| Solicitud ARCO-POL choca con dato retenido | Automatizacion G.10 | INFO/WARNING | Responsable ARCO-POL, Delegado | Plataforma | Una vez | A Delegado si no se resuelve 5 dias habiles antes del vencimiento total | Se envia la respuesta al titular | Si (referencia OBL-ARCO-06) |
| Conflicto de fundamentos con plazos muy distintos | Diferencia mayor a 3 anos entre fundamentos | INFO | Legal, Delegado | Plataforma | Una vez | No escala | Legal confirma revision | No |

### 12.3.17 MOD-017 Capacitacion

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Induccion pendiente de nuevo ingreso | 30 dias sin completar | WARNING | Responsable de area (RRHH), Delegado | Plataforma + correo | Cada 5 dias | A Administrador a los 60 dias desde el alta | Se completa | No |
| Capacitacion proxima a vencer / vencida | Faltan 30 dias / vencio la renovacion | INFO-WARNING / HIGH | La persona, Responsable de area (+ Delegado si vencida) | Plataforma (+ correo si vencida) | Semanal | A Delegado si faltan menos de 5 dias / a los 15 dias si vencida | Se completa el nuevo registro | No |
| Plan anual proximo a vencer / vencido | Faltan 60 o 30 dias / paso el ciclo, bajo bandera ACTUAL | WARNING / HIGH | Delegado/Responsable interno (+ Administrador si vencido) | Plataforma + correo | Una vez / semanal | A Administrador a los 15 dias / a Gerencia a los 30 dias | Se publica el nuevo plan | Si (OBL-CAP-02) |
| Capacitacion por rol faltante tras cambio de rol | No se completa en 15 dias (configurable) | WARNING | Responsable de area, Delegado | Plataforma | Cada 5 dias | A Delegado a los 15 dias | Se completa el registro | No |
| Sugerencia de capacitacion por leccion aprendida sin atender | Tarea de la regla G.7 abierta mas de 15 dias | INFO | Delegado, Seguridad/IT | Plataforma | Una vez, a los 15 dias | No escala | Se marca atendida o descartada | No |

### 12.3.18 MOD-018 Auditoria de Cumplimiento

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Recordatorio de proxima auditoria | Faltan 60 dias | INFO | Delegado, Administrador | Plataforma | Una vez | No escala | Se planifica | No |
| Auditoria proxima a vencer | Faltan 15 dias sin planificar | WARNING | Delegado, Legal | Plataforma + correo | Cada 5 dias | A Administrador | Se planifica | No |
| Auditoria vencida | Paso la fecha sin pasar a "En ejecucion" | HIGH | Delegado, Administrador | Plataforma + correo | Semanal | A Gerencia a los 60 dias, con referencia a riesgo de infraccion grave | Se inicia | Si (OBL-AUD-01) |
| Hallazgo critico sin plan de accion | Hallazgo Critico sin accion correctiva | HIGH | Delegado, Legal | Plataforma + correo | Diaria | A Gerencia a las 72 horas | Se crea la accion | No |
| Accion correctiva vencida | Fecha limite superada | WARNING | Responsable de la accion, Delegado | Plataforma + correo | Cada 3 dias | A Legal/Delegado y Gerencia a los 15 dias | Se marca corregida o se aprueba riesgo aceptado | No |
| Auditoria abierta mas de 90 dias sin cerrar | Sigue en Plan de accion mas de 90 dias | WARNING | Delegado, Administrador | Plataforma | Semanal | A Gerencia a los 120 dias | Se cierra o se documenta el motivo | No |

### 12.3.19 MOD-019 Centro de Evidencias

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Hueco de evidencia detectado (obligacion OBLIGATORIO) | Obligacion aplicable confirmada sin evidencia | WARNING | Delegado, Legal | Plataforma | Una vez, semanal mientras siga abierto | A Gerencia a los 30 dias | Se carga y aprueba evidencia, o deja de aplicar | Si (obligacion referenciada) |
| Evidencia por vencer / vencida | Faltan 30 dias / vencio la vigencia | WARNING / HIGH | Responsable de carga, Delegado (+ Legal si vencida) | Plataforma + correo | Cada 7 dias / semanal | Al Aprobador (15 dias) / a Gerencia (30 dias vencida) | Se renueva y aprueba | No |
| Evidencia rechazada | Aprobador rechaza una carga manual | INFO | Responsable de carga | Plataforma | Una vez | No escala | Se vuelve a cargar y aprobar | No |
| Evidencia cargada pendiente de aprobacion | Mas de 5 dias habiles En revision | WARNING | Aprobador, Delegado | Plataforma + correo | Cada 3 dias | A Administrador a los 10 dias habiles | Se aprueba o rechaza | No |
| Paquete de evidencia pendiente de segundo control | Destino externo sin segundo control 3 dias habiles | WARNING | Aprobador (segundo control) | Plataforma + correo | Diaria | A Administrador a los 5 dias habiles | Se aprueba o rechaza | No |

### 12.3.20 MOD-020 Dashboard y Reportes

MOD-020 no genera alertas propias (declara `alimenta_a: []`): quien necesita ser avisado recibe la alerta desde el modulo de origen (MOD-021, MOD-022) directamente. MOD-020 solo cambia el color del semaforo en pantalla, sin notificacion push (ver `MOD-020_ficha.md`, seccion I).

### 12.3.21 MOD-023 Calendario y Motor de Plazos

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Calendario del proximo ano no cargado | 1 de noviembre sin version Publicada del ano siguiente | WARNING | Equipo del producto | Interno del proveedor | Semanal | A CRITICAL interno a los 15 dias | Se publica la version | No (riesgo operativo del proveedor) |
| Sucursal sin fiesta patronal local documentada | Alta de sucursal sin registro en Capa 3 | WARNING | Administrador | Plataforma + correo | Una vez, luego mensual | A Legal a los 60 dias | Se registra con fuente | No |
| Recalculo aplicado a un plazo abierto | Se confirma un asueto ad hoc dentro de la ventana de un calculo | INFO/WARNING | Responsable del expediente, Delegado | Plataforma + correo | Una vez por recalculo | Inmediato al Administrador si deja menos de 1 dia habil | El calculo se cierra o se recalcula de nuevo | No |
| Cambio de criterio de computo pendiente de segunda aprobacion | Se inicia el cambio de un criterio ambiguo | WARNING | El segundo revisor (Legal o Delegado) | Plataforma + correo | Diaria | A Administrador a los 5 dias habiles | Se completa el doble control o se cancela | No |
| Cronometro de 72 horas proximo a vencer (24, 48, 60 horas) | Transcurren esos umbrales desde el inicio | INFO/INFO/WARNING | Seguridad/IT, Delegado | Plataforma + correo | Una vez por umbral | Inmediato a Administrador y Legal a las 60 horas | Se cierra el calculo o llega a 72 horas | Si (OBL-INC-01/02) |

### 12.3.22 MOD-024 Centro Regulatorio

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Cambio de estado regulatorio (reforma 659) | Bandera cambia (o se revierte) | INFO | Administrador, Delegado, Legal, Responsable de area | Plataforma + correo | Una vez | No aplica | Se confirma la lectura | No |
| Nueva actualizacion normativa publicada | Editor de contenido publica nueva version | INFO/WARNING | Administrador, Delegado, Legal | Plataforma + correo | Una vez | A Aprobador a los 10 dias habiles | Se completa la revision | No |
| Emplazamiento recibido | Se registra fecha de notificacion recibida | CRITICAL | Administrador, Legal, Aprobador | Plataforma + correo | Inmediata, diaria hasta asignar | Visible en dashboard de Gerencia desde el primer dia | Se asigna responsable | Si (OBL-SANC-05) |
| Contestacion por vencer / vencida | Faltan 2 dias / vencio de los 5 dias habiles | WARNING-CRITICAL / HIGH | Legal, Administrador (+ Aprobador) | Plataforma + correo | Diaria | Visible en dashboard de Gerencia | Escrito enviado (o avanza igual si vencida) | Si (OBL-SANC-05, Art. 21 Normativa PAS) |
| Resolucion final con sancion registrada | Resultado distinto de SIN_SANCION_ARCHIVADO | HIGH | Administrador, Legal, Aprobador | Plataforma + correo | Una vez | Visible en dashboard de Gerencia | Se completa el pago o se cierra | No |
| Pago de multa por vencer / vencido | Faltan 3 dias / vencio de los 15 dias habiles | WARNING / CRITICAL | Administrador (+ Legal, Aprobador si vencido) | Plataforma + correo | Diaria | Visible en dashboard de Gerencia | Comprobante adjunto o cobro ejecutivo documentado | Si (OBL-SANC-06, Art. 44 Normativa PAS) |
| Prescripcion proxima | Faltan 90 dias de los 5 anos desde firmeza | INFO | Legal, Auditor | Plataforma | Una vez | No aplica | Pasa a PRESCRITO_ARCHIVADO | Si (OBL-SANC-07) |
| Tramite ante la ACE pendiente de envio | Mas de 15 dias habiles en BORRADOR/PENDIENTE_DE_ENVIO | WARNING | Administrador, Legal, Delegado | Plataforma + correo | Semanal | A Administrador a los 30 dias habiles | Se marca ENVIADO | No |
| Reclamo o denuncia del titular vinculada | MOD-011 registra reclamo u OBL-SANC-09 | WARNING | Legal, Administrador | Plataforma + correo | Una vez | A Aprobador a los 5 dias habiles | Se revisa el enlace | No |
| Falta calendario de dias habiles del ano en curso | MOD-023 no tiene calendario vigente | CRITICAL | Administrador | Plataforma + correo | Diaria | A Aprobador a los 2 dias | Se configura el calendario | No |

### 12.3.23 MOD-025 Busqueda Global

Modulo de solo lectura: no genera alertas de negocio propias, salvo el indicador informativo de "volumen de consultas en ambito sensible" que solo se muestra en pantalla (`MOD-025_ficha.md`, seccion I).

### 12.3.24 MOD-026 Centro de Ayuda

| Alerta | Disparador | Nivel | Destinatario | Canal | Frecuencia | Escalamiento | Se apaga cuando | Plazo legal |
|---|---|---|---|---|---|---|---|---|
| Sugerencia de evaluar asesoria juridica externa | Automatizacion 4 (clic en "necesito ayuda juridica" o 3+ articulos de alerta en la misma sesion) | INFO | Delegado/Responsable interno o Legal/Compliance | Tarea en MOD-021 y aviso via MOD-022 | Una vez por caso | Ninguno automatico | Se marca atendida o descartada | No |

---
