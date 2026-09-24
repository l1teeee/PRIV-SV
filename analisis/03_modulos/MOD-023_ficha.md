# MODULO: Calendario y Motor de Plazos

Codigo corto del modulo: MOD-023
Clasificacion global del modulo: MUST HAVE
Obligaciones que cubre: Propietarias: OBL-PLAZO-01 (Art. 82 Ley de Procedimientos Administrativos, D.L. 856, supletoria por Art. 62 LPDP; regla de computo de dias y horas habiles), OBL-PLAZO-02 (Art. 190 Codigo de Trabajo y D.L. 339/2016, D.L. 208/2012; calendario de asuetos nacionales). Colaboradoras (este modulo calcula el plazo pero el fundamento y el expediente los define el modulo propietario): OBL-ARCO-08 (Art. 18 LPDP, prevencion y subsanacion en 10 dias habiles, propietario MOD-011 ARCO-POL), OBL-ARCO-09 (Art. 19 LPDP, devolucion por incompetencia en 5 dias habiles, propietario MOD-011), OBL-ARCO-10 (Art. 20 LPDP, plazo general de 20 dias habiles prorrogable hasta 20 mas, propietario MOD-011), OBL-DPO-02 (Art. 8 Lineamientos DPO, notificacion interna del nombramiento del delegado en 3 dias habiles, propietario MOD-002 Delegado / Responsable Interno de Datos), OBL-DPO-03 (Arts. 10 y 12 Lineamientos DPO, comunicacion del nombramiento a la ACE en 15 dias habiles, propietario MOD-002), OBL-INC-01 (Art. 25 LPDP, notificacion de vulneraciones en 72 horas, propietario MOD-013 Incidentes de Seguridad), OBL-INC-02 (Art. 25 inc. 2 LPDP, inicio de la revision exhaustiva dentro de las mismas 72 horas, propietario MOD-013), OBL-SANC-05 (Art. 21 Normativa para el Procedimiento Administrativo Sancionador de la ACE, contestacion del emplazamiento en 5 dias habiles, propietario MOD-024 Centro Regulatorio).

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (sin codigo, sin SQL, sin APIs, sin stack, sin infraestructura).

Fuentes usadas para esta ficha: `analisis/00_contexto_para_agentes.md`; `analisis/00_prompt_analisis_funcional.md`; `analisis/00_plantilla_ficha_modulo.md`; `analisis/02_validacion/mapa_modulos.json` (entrada MOD-023); `analisis/02_validacion/06_mapa_definitivo_de_modulos.md` (secciones 0, 2, 3, 4, 5, 6, 6.1, 7, 8, 9); `analisis/01_legal/matriz_obligaciones.json` (registros OBL-PLAZO-01, OBL-PLAZO-02, OBL-PLAZO-03, OBL-PLAZO-04, OBL-PLAZO-05, OBL-ARCO-08, OBL-ARCO-09, OBL-ARCO-10, OBL-DPO-02, OBL-DPO-03, OBL-DPO-04, OBL-SANC-05, OBL-SANC-06, OBL-INC-01, OBL-INC-02, OBL-CONS-03); `analisis/01_legal/sweep_plazos_calendario_retencion.md` (completo); `analisis/01_legal/03_hallazgos_regulatorios.md` (pasajes de plazos, secciones 3, 4.1 a 4.4 y 9); `analisis/01_legal/fuentes/asamblea_decreto_856_lpa.txt` (Art. 82, contrastado en linea 1445); `analisis/02_validacion/02_validacion_de_la_idea.md` (hallazgo/decision 15 de la seccion de resoluciones, sobre el motor de plazos transversal); `analisis/02_validacion/04_objetivo_exacto_del_producto.md` (secciones 1.1 a 1.3); `analisis/02_validacion/05_tipos_de_usuario.md` (secciones 5.3 y 5.4); `analisis/02_validacion/22_anti_features.md` (items 1, 8, 19, 20, 23, 25); `analisis/02_validacion/lente_faltantes.md` (hallazgo 31); `analisis/02_validacion/lente_inconsistencias.md` (inconsistencia 17); `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` (secciones 17 y 25, hipotesis del documento maestro); fichas ya redactadas de `analisis/03_modulos/` (MOD-002, MOD-003, MOD-006, MOD-007, MOD-008, MOD-009, MOD-010, MOD-011, MOD-012, MOD-013, MOD-014, MOD-015, MOD-016, MOD-018, MOD-021), consultadas con `grep -n "MOD-023"` y leidas en su contexto; MOD-011 y MOD-021 leidas completas como modelo de estilo y profundidad.

---

## A. Proposito

**Por que existe.** El documento maestro nunca definio un modulo propio de calendario: menciono el calculo de dias habiles como un detalle disperso dentro de ARCO-POL (seccion 17: "el calculo de plazos debe considerar dias habiles, fines de semana, feriados, asuetos configurables... investigar cual debe ser la fuente de calendario oficial") y dentro de Incidentes (seccion 25: "verificar exactamente cuando comienza el plazo" de las 72 horas), sin conectar ambos con el Delegado ni con el Procedimiento sancionador. La validacion de la idea identifico esto como la inconsistencia 17 ("Calendario de dias habiles tratado como detalle, no como dependencia central") y el hallazgo 31 de funciones faltantes ("un motor de computo de dias y horas habiles... que sea un servicio compartido por todos los modulos con plazo legal, y no solo una vista de calendario"), y la decision de disenio correspondiente (`02_validacion_de_la_idea.md`, resolucion 15: "Definir un motor de plazos habiles transversal... como unica fuente consultada por ARCO-POL, Incidentes, Delegado y Procedimiento sancionador") es la que crea este modulo como pieza de primer nivel del mapa definitivo, en la barra transversal.

**Que problema resuelve para la empresa.** Casi todas las obligaciones con plazo legal de la matriz (105 obligaciones) dependen de una misma pregunta tecnica que la ley no siempre responde con claridad: que dia es habil, cuando empieza a contar un plazo, que pasa si el ultimo dia cae en un dia inhabil, y como se cuenta un plazo en horas cuando la urgencia de la norma (72 horas de un incidente) no encaja bien con la logica de "solo horas habiles". Sin un unico lugar que resuelva esto, cada modulo (ARCO-POL, Delegado, Incidentes, Procedimiento sancionador, y en la practica casi todos los demas) tendria que programar su propia nocion de "dia habil", con el riesgo de que dos modulos calculen fechas distintas para el mismo caso, o de que un asueto decretado a ultima hora quede actualizado en un modulo y olvidado en otro.

**Que obligacion u obligaciones cubre (IDs y articulos).**

| OBL-ID | Clasificacion | Articulo / fuente | Contenido resumido | Rol de este modulo |
|---|---|---|---|---|
| OBL-PLAZO-01 | OBLIGATORIO | Art. 82 Ley de Procedimientos Administrativos (D.L. 856), supletoria por Art. 62 LPDP | Los plazos por dias u horas se computan solo en dias y horas habiles; el computo inicia el dia siguiente a la notificacion o recepcion; los plazos por meses o anios van de fecha a fecha; si el ultimo dia es inhabil, se prorroga al primer dia habil siguiente | Propietario: este modulo ES la regla de computo hecha servicio |
| OBL-PLAZO-02 | OBLIGATORIO | Art. 190 Codigo de Trabajo; D.L. 339/2016 (10 de mayo); D.L. 208/2012 (17 de junio) | Calendario de asuetos nacionales que se excluyen del computo de dias habiles, mas los asuetos locales (3 y 5 de agosto en San Salvador, fiesta patronal en el resto del pais) y los asuetos ad hoc que decrete la Asamblea Legislativa | Propietario: este modulo mantiene y versiona ese calendario |
| OBL-ARCO-08 | OBLIGATORIO | Art. 18 LPDP | Prevencion unica, 10 dias habiles para subsanar | Colaborador: calcula la fecha limite de subsanacion; el fundamento, el archivo y la decision son de MOD-011 |
| OBL-ARCO-09 | CONDICIONAL (aplica solo cuando el responsable no es competente sobre los datos) | Art. 19 LPDP | Devolucion por incompetencia en 5 dias habiles | Colaborador: calcula la fecha limite; MOD-011 declara la incompetencia y notifica |
| OBL-ARCO-10 | OBLIGATORIO | Art. 20 LPDP | Plazo general de 20 dias habiles, prorrogable una vez hasta 20 dias habiles mas | Colaborador: calcula ambas fechas (ordinaria y prorrogada); MOD-011 decide y motiva la prorroga |
| OBL-DPO-02 | CONDICIONAL (aplica mientras el cliente tenga obligacion de delegado o lo mantenga voluntariamente) | Art. 8 Lineamientos para el Delegado (ACE) | Notificacion interna del nombramiento del delegado en 3 dias habiles | Colaborador: calcula la fecha limite; MOD-002 ejecuta y aprueba |
| OBL-DPO-03 | CONDICIONAL (misma condicion que OBL-DPO-02) | Arts. 10 y 12 Lineamientos DPO | Comunicacion del nombramiento a la ACE en 15 dias habiles; actualizaciones en 10 dias habiles | Colaborador: calcula ambas fechas usando el calendario de la autoridad (capa 5, ver seccion D); MOD-002 ejecuta el tramite |
| OBL-INC-01 | OBLIGATORIO | Art. 25 LPDP | Notificacion de vulneraciones a la ACE, la Fiscalia y los titulares en 72 horas desde que se tuvo conocimiento | Colaborador: calcula el vencimiento en horas corridas por defecto (ver incertidumbre en H); MOD-013 gestiona el incidente |
| OBL-INC-02 | OBLIGATORIO | Art. 25 inc. 2 LPDP | Inicio (no necesariamente conclusion) de la revision exhaustiva dentro de las mismas 72 horas | Colaborador: mismo cronometro que OBL-INC-01 |
| OBL-SANC-05 | CONDICIONAL (aplica solo cuando la ACE emplaza al responsable en un procedimiento sancionador) | Art. 21 Normativa para el Procedimiento Administrativo Sancionador (ACE) | Contestacion del emplazamiento en 5 dias habiles desde el dia siguiente habil a la notificacion | Colaborador: calcula la fecha limite usando el calendario de la autoridad; MOD-024 gestiona el expediente sancionador |

Clasificacion de cada OBL-ID verificada contra `01_legal/matriz_obligaciones.json` (campo `clasificacion`); las obligaciones colaboradoras OBL-ARCO-09, OBL-DPO-02, OBL-DPO-03 y OBL-SANC-05 son CONDICIONAL (dependen de un supuesto especifico), a diferencia de las demas, que son OBLIGATORIO.

**Que valor aporta.**
- *Operativo*: un unico lugar donde vive la regla de computo y el calendario de dias inhabiles, consultado por cada modulo con plazo legal en vez de que cada uno programe su propia cuenta; cuando se corrige el calendario (por ejemplo, se agrega un asueto decretado a ultima hora), la correccion se aplica una sola vez y se propaga a todos los plazos abiertos.
- *Probatorio*: cada fecha limite calculada queda con su desglose completo (dia de inicio, dias excluidos y por que, fecha resultante) y con la version exacta del calendario que se uso, de modo que la empresa puede demostrar, mucho tiempo despues, exactamente como llego a esa fecha.
- *Reduccion de riesgo*: evita que dos modulos calculen fechas distintas para el mismo tipo de plazo (por ejemplo, que ARCO-POL cuente el sabado como habil mientras Incidentes lo cuenta como inhabil), y evita que un cambio de calendario quede aplicado en un modulo y olvidado en otro.

**Que NO hace este modulo (limites explicitos).**
- No decide que plazo legal aplica a un caso concreto ni por que articulo: eso lo define siempre el modulo propietario de la obligacion (MOD-011, MOD-002, MOD-013, MOD-024); este modulo solo calcula la fecha una vez que el modulo de origen le indica el evento de inicio, la duracion, la unidad y el fundamento.
- No decide si una incertidumbre juridica documentada se resuelve de una forma u otra para la empresa (por ejemplo, si el Art. 82 LPA aplica realmente a la relacion titular-empresa privada, si el sabado es habil para una empresa que abre ese dia, o si las 72 horas del Art. 25 se cuentan corridas o habiles): aplica siempre el criterio por defecto documentado en `01_legal/sweep_plazos_calendario_retencion.md` y muestra la advertencia correspondiente (ver seccion H).
- No suspende ni prorroga un plazo por iniciativa propia: solo ejecuta la suspension o la prorroga cuando el modulo propietario se la solicita de forma explicita, con el fundamento que ese modulo declare.
- No es un calendario personal ni una agenda de reuniones de la empresa: solo administra dias habiles/inhabiles y fechas limite legales u operativas ligadas a una obligacion o a una revision periodica de otro modulo; no gestiona citas, invitaciones ni disponibilidad de personas.
- No mueve nunca una fecha limite "en silencio": todo recalculo (por ejemplo, al agregarse un asueto ad hoc dentro de un plazo ya abierto) queda registrado, notificado y con el valor anterior conservado en el historial (ver secciones F y O).
- No confirma por si mismo la fuente oficial de un asueto ad hoc o de una fiesta patronal local: exige que quien lo carga (el equipo del producto para las capas nacionales, la empresa para la capa local) documente la fuente antes de publicarlo (ver seccion D).

---

## B. Usuarios

Roles estandar segun `02_validacion/05_tipos_de_usuario.md`, seccion 5.3 (los 12 roles del sistema), mas un actor adicional que no es un rol de la organizacion cliente.

| Rol | Para que usa MOD-023 |
|---|---|
| Administrador de la organizacion | Configura el calendario propio de la empresa (capa 4: horario habil, si activa "sabado habil" solo para metas internas), designa que sucursal usa que calendario local, y ve el reporte de calendario vigente y el historial de recalculos. |
| Delegado de Proteccion de Datos (o Responsable interno) | Consulta los plazos calculados para sus propias obligaciones (notificacion interna de 3 dias, comunicacion a la ACE de 15 dias, reverificacion trienal); aprueba, junto con Legal/Compliance, cualquier cambio del criterio de computo por defecto en un caso con ambiguedad juridica documentada (ver seccion C). |
| Responsable ARCO-POL / Responsable del tramite | Ve el desglose de cada plazo de sus expedientes (prevencion, plazo general 20+20, incompetencia, notificacion a receptores, denegatoria) tal como lo calculo MOD-023 para MOD-011; no edita el calculo. |
| Responsable Legal / Compliance | Revisa y aprueba, junto con el Delegado, el cambio del criterio de computo por defecto en un caso ambiguo (por ejemplo, activar horas habiles para el cronometro de 72 horas); consulta el historial de recalculos para evaluar riesgo. |
| Responsable de Seguridad / IT | Ve el cronometro de 72 horas de un incidente en curso, calculado por este modulo, y la alerta si el criterio de computo aplicado esta marcado como incierto. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Ve, dentro de la vista de calendario central (seccion area 30), las fechas limite de las tareas y revisiones que le corresponden, filtradas por su area o sucursal. |
| Aprobador | Participa en el doble control cuando se cambia el criterio de computo por defecto de un plazo con ambiguedad juridica, si la organizacion lo configura como segundo revisor. |
| Auditor (interno) | Solo lectura: consulta el historial completo de calculos, recalculos y cambios de calendario como evidencia de que el motor de plazos se aplico de forma consistente. |
| Auditor externo (invitado) | Acceso temporal de solo lectura al reporte de calendario vigente y al historial de calculos de los expedientes que esta auditando. |
| Usuario de consulta / Colaborador | Ve, en la vista de calendario central, las fechas limite de las tareas puntuales que tiene asignadas (via MOD-021), sin acceso a la configuracion del calendario. |
| Titular (formulario externo) | No usa este modulo directamente: ve el numero de dias restantes de su propia solicitud a traves de MOD-012 Portal del Titular, que consulta a MOD-023 en modo de solo lectura. |
| Asesor externo invitado | Consulta, dentro del expediente puntual al que fue invitado, la fecha limite y el desglose calculados para ese caso, sin acceso a la configuracion general del calendario. |

**Actor adicional (no es un rol de la organizacion cliente): Equipo del producto (proveedor).** El mantenimiento de las capas nacionales del calendario (capa 1: calendario nacional base; capa 2: asuetos ad hoc; capa 5: calendario de la autoridad) no lo hace ninguno de los 12 roles de la empresa cliente, sino el equipo que mantiene el producto, de la misma forma en que la bandera de regimen de la reforma 659 en MOD-024 solo la activa "el equipo del producto tras confirmar la publicacion oficial" (`06_mapa_definitivo_de_modulos.md`, seccion 5, punto 2). Esto es coherente con que ninguna empresa cliente deberia decidir por su cuenta si el 16 de septiembre de tal anio fue o no asueto nacional: es un hecho publico unico para todos los clientes, y su verificacion contra el Diario Oficial es responsabilidad del proveedor del software, no de cada organizacion. La empresa cliente solo administra las capas que le son propias: la capa 3 (asuetos locales por sede) y la capa 4 (calendario propio y horario habil).

---

## C. Permisos

Convencion: "Si" = permitido por defecto; "Si*" = permitido solo sobre el ambito propio (su sucursal o su expediente); "No" = no permitido; "Doble control" = exige una segunda persona distinta de quien inicio la accion (`05_tipos_de_usuario.md`, seccion 5.4). La columna "Equipo del producto" no es un rol de la organizacion cliente (ver seccion B) y se incluye solo para dejar explicito que las capas nacionales no las edita ningun rol de la empresa.

| Accion | Administrador | Delegado / Resp. interno | Legal/Compliance | Seguridad/IT | Responsable de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Titular | Asesor externo | Equipo del producto |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver calendario vigente y vista central (area 30) | Si | Si | Si | Si | Si* (su area/sucursal) | Si | Si (solo lectura) | Si* (solo lectura, temporal) | Si* (sus tareas) | No (ve solo su propio caso via MOD-012) | Si* (su caso) | Si |
| Ver desglose y version usada de un calculo especifico | Si | Si | Si | Si* (incidentes) | Si* (sus tareas) | Si* (casos que aprueba) | Si (solo lectura) | Si* (solo lectura) | Si* (sus tareas) | No (ve dias restantes, no el desglose tecnico) | Si* (su caso) | Si |
| Configurar calendario nacional base (capa 1), asuetos ad hoc (capa 2) y calendario de la autoridad (capa 5) | No | No | No | No | No | No | No | No | No | No | No | Si |
| Configurar asuetos locales por sede (capa 3), con fuente y fecha de verificacion | Si | No | No | No | No | No | No | No | No | No | No | No (revisa que la fuente este documentada, no la impone) |
| Configurar calendario propio de la empresa (capa 4: horario habil, "sabado habil" solo interno) | Si | No | No | No | No | No | No | No | No | No | No | No |
| Cambiar el criterio de computo por defecto en un plazo con ambiguedad juridica documentada (por ejemplo, 72 horas corridas vs. habiles) | No (solo lo solicita) | Doble control (junto con Legal) | Doble control (junto con Delegado) | No | No | Si* (si la organizacion lo designa segundo revisor) | No | No | No | No | No | No |
| Publicar una nueva version anual del calendario (Borrador -> Publicado) | No | No | No | No | No | No | No | No | No | No | No | Si |
| Registrar un recalculo por asueto ad hoc agregado despues de calcular un plazo | No (solo lo ve) | No | No | No | No | No | No | No | No | No | No | Si (dispara el recalculo; el sistema lo aplica de forma automatica a los plazos abiertos, ver seccion F) |
| Exportar reporte de calendario vigente o historial de calculos | Si | Si | Si | Si | No | No | Si | Si* (lo asignado) | No | No | No | Si |
| Eliminar un registro de calendario o un calculo ya realizado | Nadie. No existe esta accion para ningun rol: un calendario o un calculo se archiva como historico, nunca se borra (anti-feature 19) | | | | | | | | | | | |
| Comentar (por ejemplo, dejar nota sobre una fuente dudosa de fiesta patronal) | Si | Si | Si | No | Si* | No | No | No | No | No | No | Si |
| Adjuntar evidencia (decreto, comunicado municipal, aviso oficial) | Si | No | No | No | Si* (su sucursal) | No | No | No | No | No | No | Si |

**Separacion de funciones.** Cambiar el criterio de computo por defecto de un plazo con ambiguedad juridica documentada es la unica decision de este modulo con impacto legal directo sobre todos los casos abiertos de ese tipo; por eso exige doble control entre el Delegado/Responsable interno y Legal/Compliance (o un Aprobador designado), nunca lo ejecuta una sola persona ni el Administrador por si solo. Quien confirma la fuente de un asueto ad hoc o de la capa de la autoridad (equipo del producto) nunca es la misma persona ni organizacion que decide el criterio de computo ambiguo de un cliente especifico, para que la fuente del calendario y la interpretacion juridica de un caso queden como dos decisiones distintas y verificables por separado.

---

## D. Informacion de entrada

MOD-023 administra dos tipos de informacion de entrada: la configuracion del calendario de dias inhabiles (entidad HolidayCalendar, organizada en capas) y las solicitudes de calculo de plazo que le hacen los demas modulos (instancias de la entidad CalendarEvent). Ambas siguen la convencion de la plantilla: 7 columnas por campo.

### D.1 Capas del calendario de dias inhabiles (HolidayCalendar)

Segun `01_legal/sweep_plazos_calendario_retencion.md`, seccion 3.9, el calendario se organiza en 6 capas, cada una con su propio mantenedor y su propia fuente.

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Anio calendario | Numero | Obligatorio | Anio de 4 digitos, por ejemplo 2027 | Entero valido, no puede repetirse una version Publicada para el mismo anio y la misma capa | "El anio que cubre esta version del calendario." | OBL-PLAZO-02 |
| Capa | Seleccion unica | Obligatorio | Capa 0 (fin de semana); Capa 1 (calendario nacional base); Capa 2 (asuetos ad hoc); Capa 3 (asuetos locales por sede); Capa 4 (calendario propio de la empresa); Capa 5 (calendario de la autoridad, ACE) | Determina quien puede editarla (ver seccion C) | "A que tipo de dia inhabil pertenece este registro." | OBL-PLAZO-02; sweep seccion 3.9 |
| Fecha | Fecha | Obligatorio | - | Debe caer dentro del Anio calendario declarado (salvo fechas moviles calculadas, como Semana Santa) | "El dia exacto que el sistema no contara como habil." | OBL-PLAZO-02 |
| Nombre del asueto o evento | Texto | Obligatorio | Libre, con catalogo sugerido (por ejemplo "Dia de la Independencia", "Fiestas agostinas", "Asueto decretado por [motivo]") | Maximo 140 caracteres | "Como se llama esta fecha, para que el usuario entienda por que no se cuenta como dia habil." | Buena practica (transparencia) |
| Alcance | Seleccion multiple | Obligatorio | Sector privado; Sector publico (autoridad/ACE); Ambos; Solo la sede indicada | Debe ser coherente con la Capa elegida (por ejemplo, Capa 3 exige "Solo la sede indicada") | "A quien aplica este dia libre: a toda empresa privada, solo a las oficinas publicas, o solo a una sucursal suya." | OBL-PLAZO-02; sweep secciones 3.3 y 3.5 |
| Sede o municipio | Referencia a sucursal de MOD-001 | Obligatorio solo si Capa = 3 | Catalogo de sucursales/areas de MOD-001 | Debe existir en MOD-001 | "A que sucursal de su empresa corresponde esta fiesta patronal." | sweep seccion 3.4 |
| Fuente de la fecha | Texto mas archivo adjunto | Obligatorio | Decreto legislativo; Diario Oficial; comunicado de la alcaldia; aviso del Ministerio de Trabajo; algoritmo de fecha movil (Semana Santa) | Debe incluir enlace verificable o archivo adjunto, salvo fecha calculada por algoritmo | "De donde se tomo esta fecha, para poder demostrarlo si alguien lo pregunta despues." | OBL-PLAZO-02; principio de responsabilidad demostrada |
| Fecha de verificacion de la fuente | Fecha | Obligatorio | - | No puede ser posterior a hoy | "Cuando se confirmo que esta fecha es correcta." | Buena practica |
| Estado de la version | Seleccion unica (autogenerado en las transiciones de la seccion F) | Obligatorio | Borrador; Publicado; Vigente; Actualizado; Historico | Ver seccion F | "En que etapa esta el calendario de este anio." | Buena practica |

**Campos precargados.** La sucursal (para la Capa 3) se precarga desde el catalogo de MOD-001. La fecha de la Semana Santa de cada anio se calcula por el algoritmo de Pascua gregoriana (sin necesidad de fuente documental adicional, segun `sweep_plazos_calendario_retencion.md`, seccion 3.8), y el equipo del producto solo confirma el resultado contra una fuente secundaria de verificacion antes de publicar.

**Minimizacion de datos personales.** Esta entidad no contiene datos personales de titulares: solo fechas, nombres de asuetos, sucursales y fuentes documentales publicas. La unica referencia a personas es indirecta, a traves del usuario que registra o verifica una fuente (Administrador o equipo del producto), que ya queda identificado por el historial general del sistema (seccion O), sin que este modulo necesite capturar ningun dato adicional del titular.

### D.2 Solicitud de calculo de plazo (entidad CalendarEvent, tipo Plazo)

Esta es la informacion que un modulo consumidor (MOD-002, MOD-006 a MOD-018, MOD-021, MOD-024, etc.) entrega a MOD-023 cada vez que necesita una fecha limite. El usuario humano no llena este formulario directamente: lo completa el modulo de origen a partir de sus propios campos (por ejemplo, MOD-011 entrega "fecha de recepcion de la solicitud" mas "20 dias habiles" mas el OBL-ID correspondiente); se documenta aqui como informacion de entrada porque asi lo exige la seccion D de la plantilla, y porque el usuario si ve, dentro del modulo de origen, el resultado y el desglose que produce.

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Modulo solicitante | Referencia a otro modulo | Obligatorio (autogenerado) | Catalogo de los 26 modulos | Debe ser un modulo existente | "De donde vino este plazo." | Trazabilidad |
| Obligacion relacionada (OBL-ID) | Referencia (lista, opcional) | Opcional; obligatorio cuando el plazo es de origen legal | Lista de `matriz_obligaciones.json` | Debe existir en la matriz | "El fundamento legal exacto de este plazo, mostrado como ayuda contextual." | Regla de oro de la plantilla: el OBL-ID se muestra en segundo nivel |
| Evento de inicio | Fecha y hora | Obligatorio | - | No puede ser una fecha futura, salvo un caso de prorroga o suspension explicitamente programada por el modulo de origen | "El momento exacto desde el que empieza a contar este plazo, por ejemplo cuando se recibio la solicitud del titular." | OBL-PLAZO-01 |
| Tipo de computo | Seleccion unica | Obligatorio | Dias habiles; Dias corridos; Horas corridas; Horas habiles; Meses de fecha a fecha; Anios de fecha a fecha | Determina el algoritmo que se aplica (ver seccion G) | "Como cuenta este plazo la norma que lo crea: por ejemplo, en dias habiles o en horas corridas." | OBL-PLAZO-01 |
| Duracion | Numero | Obligatorio | Entero positivo | Mayor que 0 | "Cuantas unidades de tiempo dura el plazo, por ejemplo 20, 10, 5, 3 o 72." | Depende de la obligacion citada |
| Capa de calendario aplicable | Seleccion unica | Obligatorio | Empresa frente al titular (capas 0 a 4); Empresa frente a la autoridad -ACE- (capa 5) | Determina que dias se excluyen (ver seccion G) | "Si este plazo corre frente a una persona (el titular) o frente a la Agencia de Ciberseguridad del Estado." | sweep secciones 3.3 y 3.9 |
| Es plazo suspendible | Booleano | Obligatorio (por defecto No) | Si / No | Solo puede ser "Si" si el modulo solicitante declara ademas la causal de suspension configurada | "Si este plazo se puede detener temporalmente por una causa prevista (por ejemplo, mientras el titular completa informacion pendiente)." | Incertidumbre 4, `sweep_plazos_calendario_retencion.md` seccion 9 |
| Criterio elegido ante ambiguedad juridica | Seleccion unica, solo si aplica | Obligatorio cuando el tipo de plazo tiene una ambiguedad documentada (por ejemplo, las 72 horas del Art. 25) | Criterio conservador por defecto; Criterio alternativo (exige el doble control de la seccion C) | Cambiar del valor por defecto exige aprobacion registrada | "Cuando la ley no aclara como contar este plazo, el sistema aplica el criterio mas prudente, salvo que su organizacion decida cambiarlo con respaldo legal." | sweep seccion 9, incertidumbres 1 a 4 |
| Sucursal relevante | Referencia a MOD-001 | Opcional | Catalogo de sucursales | - | "Si el caso involucra una sucursal con fiesta patronal propia, indiquela para que el calculo la excluya." | sweep seccion 3.4 |

**Campos precargados.** Todos los campos de esta subseccion llegan precargados desde el modulo de origen (por ejemplo, MOD-011 entrega automaticamente "Evento de inicio" = fecha de recepcion de la solicitud, "Tipo de computo" = dias habiles, "Duracion" = 20, "OBL-ID" = OBL-ARCO-10); ningun usuario los captura a mano dentro de MOD-023.

**Minimizacion de datos personales.** Una solicitud de calculo no contiene el dato personal del titular en si (nombre, documento, contenido de su solicitud): solo referencia el expediente de origen (por ejemplo, el numero de expediente ARCO-POL) para poder auditar despues a que caso pertenece ese calculo, igual que hace MOD-021 con sus tareas.

### D.3 Configuracion de la empresa (capa 4 y parametros propios)

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Horario habil de la empresa | Hora de inicio y hora de fin | Opcional (si no se configura, se usa medianoche como cierre por defecto, CC Art. 47) | - | Hora de fin posterior a hora de inicio | "El horario en que su empresa atiende, para calcular si una solicitud llego dentro o fuera de horario habil." | sweep seccion 3.7 |
| Sabado habil (solo para metas internas) | Booleano | Opcional (por defecto No) | Si / No | Si es "Si", el sistema muestra siempre ademas la fecha calculada con sabado inhabil (la mas exigente frente al titular) | "Puede marcar el sabado como dia habil solo para sus propias metas internas; nunca reduce el plazo que la ley da al titular." | sweep secciones 3.6 y 9, incertidumbre 3 |
| Criterio de computo de las 72 horas | Seleccion unica | Obligatorio (por defecto: Horas corridas) | Horas corridas (criterio conservador); Horas habiles (requiere aprobacion, ver seccion C) | Cambiar a "Horas habiles" exige doble control | "Como cuenta su empresa las 72 horas de un incidente. El sistema recomienda horas corridas porque es el criterio mas prudente." | OBL-INC-01; sweep seccion 2.5 |
| Aplicar suspension del plazo de 20 dias durante la prevencion (Art. 90.1 LPA) | Booleano | Obligatorio (por defecto No, criterio mas exigente) | Si / No | Cambiar a "Si" exige doble control (Delegado y Legal) | "La ley no aclara si el tiempo de la prevencion detiene el plazo general de 20 dias. Por defecto el sistema no lo detiene, para ser mas prudente. Puede cambiarlo con respaldo legal." | Incertidumbre 4, sweep seccion 9; MOD-011 seccion H |

### D.4 Catalogo consolidado de plazos que MOD-023 calcula

Esta subseccion reune, en un solo lugar, los plazos concretos que otros modulos piden calcular a MOD-023 (seccion D.2), dispersos hasta ahora entre la seccion A, la seccion B y el diagrama de dependencias L.1. No introduce ninguna regla nueva de computo: es una vista consolidada de datos ya presentes en esta ficha, en `01_legal/matriz_obligaciones.json` y en `01_legal/sweep_plazos_calendario_retencion.md`.

| Plazo | Valor y unidad | Evento de inicio | Modulo consumidor | OBL-ID | Norma y articulo | Tipo de computo | Incertidumbre juridica |
|---|---|---|---|---|---|---|---|
| Plazo general de respuesta ARCO-POL, con prorroga | 20 dh, prorrogable hasta 20 dh mas | Recepcion de la solicitud del titular | MOD-011 | OBL-ARCO-10 | Art. 20 LPDP | Dias habiles (capas 0 a 3) | Incertidumbre 1 (aplicabilidad del Art. 82 LPA) e incertidumbre 4 (si la prevencion suspende este plazo), sweep seccion 9 |
| Prevencion y subsanacion | 10 dh | Notificacion de la prevencion al titular | MOD-011 | OBL-ARCO-08 | Art. 18 LPDP | Dias habiles | Incertidumbre 1 |
| Devolucion por incompetencia | 5 dh | Recepcion de la solicitud | MOD-011 | OBL-ARCO-09 | Art. 19 LPDP | Dias habiles | Incertidumbre 1 |
| Notificacion a receptores tras rectificacion, actualizacion o eliminacion | 5 dh | Determinacion de la procedencia de la solicitud | MOD-011 | OBL-ARCO-11 | Art. 21 inc. 3 LPDP | Dias habiles | Incertidumbre 1 |
| Denegatoria motivada de una solicitud ARCO-POL | 3 dh | Adopcion de la decision de denegar | MOD-011 | OBL-ARCO-12 | Art. 22 LPDP | Dias habiles | Incertidumbre 1 |
| Revocacion del consentimiento (ejecutarla) | 5 dh | Recepcion de la solicitud de revocacion | MOD-007 | OBL-CONS-03 | Art. 30 inc. 1 LPDP | Dias habiles | Incertidumbre 1 |
| Revocacion del consentimiento (informar al encargado) | 5 dh | Emision de la resolucion de revocacion | MOD-007 | OBL-CONS-03 | Art. 30 inc. 2 LPDP | Dias habiles | Incertidumbre 1 |
| Notificacion interna del nombramiento del delegado | 3 dh | Designacion del delegado | MOD-002 | OBL-DPO-02 | Art. 8 Lineamientos DPO | Dias habiles | Incertidumbre 1; ademas condicionado por la incertidumbre 6 (reforma 659, vigencia pendiente de publicacion) |
| Comunicacion del nombramiento del delegado a la ACE | 15 dh | Dia siguiente al nombramiento del delegado | MOD-002 | OBL-DPO-03 | Arts. 10 y 12 Lineamientos DPO | Dias habiles (capa 5, autoridad) | Incertidumbre 6 |
| Reverificacion periodica del perfil del delegado | 3 anos | Nombramiento o ultima reverificacion del delegado | MOD-002 | OBL-DPO-04 | Art. 18 Lineamientos DPO | Anos de fecha a fecha | Incertidumbre 6 |
| Notificacion de vulneraciones a la ACE, la Fiscalia y los titulares | 72 horas | Momento en que se tuvo conocimiento de la vulneracion | MOD-013 | OBL-INC-01 | Art. 25 LPDP | Horas corridas (criterio por defecto, seccion D.3) | Incertidumbre 2 (horas corridas frente a horas habiles) |
| Inicio de la revision exhaustiva del incidente | 72 horas | Mismo evento que OBL-INC-01 | MOD-013 | OBL-INC-02 | Art. 25 inc. 2 LPDP | Horas corridas (criterio por defecto) | Incertidumbre 2 |
| Contestacion del emplazamiento en el procedimiento sancionador | 5 dh | Dia siguiente habil a la notificacion del emplazamiento | MOD-024 | OBL-SANC-05 | Art. 21 Normativa para el Procedimiento Administrativo Sancionador (ACE) | Dias habiles (capa 5, autoridad) | Ninguna documentada: es un plazo de un procedimiento propio de la ACE, sin depender de la supletoriedad del Art. 62 LPDP |
| Pago de la multa impuesta | 15 dh | Notificacion de la resolucion sancionatoria | MOD-024 | OBL-SANC-06 | Art. 44 Normativa para el Procedimiento Administrativo Sancionador (ACE) | Dias habiles (capa 5, autoridad) | Ninguna documentada |
| Plan anual de capacitacion del delegado y del personal | 1 ano (periodicidad) | Nombramiento del delegado o cierre del plan anterior | MOD-002 / MOD-017 | OBL-CAP-02 | Art. 22 Lineamientos DPO | Anos de fecha a fecha | Incertidumbre 6 |
| Auditoria anual de cumplimiento de las Politicas ACE | 1 ano (periodicidad) | Adecuacion inicial de la empresa o ultima auditoria | MOD-018 | OBL-AUD-01 | Politicas de Actuacion ACE, Art. 8 lit. b | Anos de fecha a fecha | Ninguna documentada |
| Revisiones periodicas internas (RAT, documentos, proveedores, transferencias, EIPD, controles, retencion) | Periodicidad configurable, tipicamente 1 ano | Fecha de la ultima revision o de creacion del registro | MOD-006, MOD-008, MOD-009, MOD-010, MOD-014, MOD-015, MOD-016 | No aplica (periodicidad de buena practica, sin obligacion con plazo legal propio) | Buena practica de gestion de riesgos (Politica ACE Art. 4, medidas organizativas) | Meses o anos de fecha a fecha, definido por el modulo de origen | No aplica |

**Nota sobre `mapa_modulos.json`.** El campo `obligaciones_colaboradoras` de la entrada MOD-023 en `02_validacion/mapa_modulos.json` (OBL-ARCO-08, OBL-ARCO-09, OBL-ARCO-10, OBL-DPO-02, OBL-DPO-03, OBL-INC-01, OBL-INC-02, OBL-SANC-05) no incluye OBL-ARCO-11, OBL-ARCO-12, OBL-CONS-03, OBL-DPO-04 ni OBL-SANC-06, aunque esta ficha (seccion B) y la propia matriz de obligaciones confirman que MOD-023 calcula tambien esos plazos para los mismos modulos propietarios (MOD-011, MOD-007, MOD-002, MOD-024). Esta tabla documenta ese calculo adicional sin modificar `mapa_modulos.json`; se registra como posible omision de esa entrada en la nota final de esta ficha.

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Fecha limite calculada | Fecha (y hora, si el plazo es en horas) exacta del vencimiento | Valor devuelto al modulo solicitante, mas vista en pantalla dentro de ese modulo | Al recibir una solicitud de calculo (seccion D.2) | Modulo solicitante (MOD-002, MOD-006 a MOD-018, MOD-021, MOD-024, etc.), que la muestra en su propia pantalla |
| Desglose del calculo | Dia 1 del computo, cada dia u hora excluido y el motivo (fin de semana, asueto nacional, asueto local, asueto ad hoc, capa de la autoridad), fecha resultante | Vista expandible junto a la fecha limite | Junto con cada fecha limite calculada | Responsable del expediente en el modulo solicitante, Auditor, Delegado |
| Version del calendario aplicada (snapshot) | Identificador de la version de HolidayCalendar usada para ese calculo especifico | Registro interno, referenciado desde el calculo | En cada calculo | MOD-019 Centro de Evidencias (a traves del modulo de origen), Auditor |
| Evento "recalculo aplicado" | Plazo afectado, fecha anterior, fecha nueva, motivo (por ejemplo, "asueto ad hoc agregado el [fecha]") | Evento interno entregado al modulo de origen y a MOD-022 | Cuando cambia el calendario mientras un plazo sigue abierto (ver seccion F) | Modulo de origen (actualiza su propia fecha mostrada), MOD-022 (decide el canal de aviso), MOD-021 (si el plazo esta alojado en una tarea) |
| Alerta "calendario del anio no cargado" | Anio faltante, capas pendientes | Evento interno | Si al 1 de noviembre del anio en curso no existe una version Publicada del anio siguiente (ver seccion I) | Equipo del producto, Administrador (como aviso informativo) |
| Evento de calendario para la vista central (area 30) | Tipo de evento (plazo legal, revision periodica, vencimiento, auditoria, ARCO-POL, incidente, tarea), fecha, modulo de origen, responsable, sucursal | Registro visible en la vista de calendario central | Cada vez que un modulo consumidor crea o actualiza un plazo o una fecha de revision | Todos los roles con acceso a la vista central, filtrada por su ambito (ver seccion C) |
| Indicadores para el dashboard | Ver seccion M | Datos agregados | Actualizacion continua | MOD-020 Dashboard y Reportes |
| Eventos de auditoria | Ver seccion O | Registro append-only | En cada calculo, recalculo o cambio de calendario | AuditLog transversal, MOD-019, MOD-018 |

---

## F. Workflow

MOD-023 tiene dos ciclos de vida distintos que conviene separar: el de una version anual del calendario (F.1) y el de un calculo de plazo individual (F.2).

### F.1 Ciclo de vida de una version anual del calendario (HolidayCalendar)

```
                    +-------------+
                    |  BORRADOR   |  (equipo del producto carga capas 1,2,5;
                    +------+------+   empresa carga su capa 3 y su capa 4)
                           |
                confirma fuente de cada fecha
                           v
                    +-------------+
                    | PUBLICADO   |  (version lista, aun no es la aplicada
                    +------+------+   por defecto)
                           |
                 llega el 1 de enero del anio que cubre
                           v
                    +-------------+
                    |  VIGENTE    |<---------------------------+
                    +------+------+                             |
                           |                                     |
             se decreta un asueto ad hoc durante el anio         |
                           v                                     |
                    +-------------+   se confirma otro           |
                    | ACTUALIZADA |-- asueto ad hoc adicional ----+
                    +------+------+   (puede repetirse varias veces)
                           |
                 termina el anio calendario que cubre
                           v
                    +-------------+
                    |  HISTORICO  |  (estado terminal; se conserva siempre,
                    +-------------+   nunca se elimina, para poder auditar
                                       calculos ya cerrados de ese anio)
```

### F.2 Tabla de transiciones de una version anual

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (no existe) | Se inicia la carga del calendario de un anio | Ninguna | Borrador | Equipo del producto (capas 1, 2, 5); Administrador (capas 3 y 4) | Se crea el registro de version; evento de auditoria |
| Borrador | Se confirma la fuente de cada fecha de las capas 1, 2 y 5 | Cada fecha tiene fuente y fecha de verificacion (seccion D.1) | Publicado | Equipo del producto | Version disponible para revision, aun no aplicada a calculos nuevos por defecto |
| Publicado | Llega el 1 de enero del anio que cubre esta version | Automatico | Vigente | Sistema (automatico) | Todo calculo nuevo usa esta version por defecto; se dispara el aviso "calendario del anio ya vigente" |
| Vigente | Se decreta y confirma un asueto ad hoc adicional durante el anio | Fuente y fecha de verificacion documentadas (seccion D.1) | Actualizada | Equipo del producto | Se crea una nueva sub-version con numero de revision; se disparan los recalculos de la seccion G sobre todo plazo abierto que la fecha afecte; evento de auditoria con el detalle del cambio |
| Actualizada | Se confirma otro asueto ad hoc adicional | Igual que la transicion anterior | Actualizada (permanece, incrementa su numero de revision) | Equipo del producto | Igual que la transicion anterior; puede repetirse cuantas veces sea necesario dentro del mismo anio |
| Vigente o Actualizada | Termina el anio calendario que cubre esta version | Automatico, al iniciar el 1 de enero del anio siguiente | Historico | Sistema (automatico) | Deja de aplicarse a calculos nuevos; se conserva integra para auditar los calculos ya cerrados de ese anio; nunca se elimina (anti-feature 19) |

**Estados terminales.** Historico es el unico estado terminal; no se reabre ni se reutiliza para calculos nuevos, pero permanece consultable de forma indefinida como evidencia de que criterio se aplico a cada caso cerrado en su momento.

### F.3 Diagrama de estados de un calculo de plazo individual (CalendarEvent, tipo Plazo)

```
                         +-------------+
              +--------->|  ABIERTO    |
              |          +------+------+
              |                 |
              |     el modulo de origen declara
              |     una causal de suspension
              |                 v
              |          +-------------+
              |          | SUSPENDIDO  |
              |          +------+------+
              |                 |
              |     cesa la causal (por ejemplo,
              |     el titular subsana)
              |                 v
              +----------(vuelve a ABIERTO,
                          se muestran ambas fechas
                          si el criterio no esta resuelto,
                          ver seccion H)

  Desde ABIERTO, en paralelo (no excluyente entre si):

  ABIERTO -- el modulo de origen solicita una prorroga valida --> PRORROGADO
      (nueva fecha limite calculada; conserva la fecha original en el historial)

  ABIERTO/SUSPENDIDO/PRORROGADO -- cambia el calendario aplicable
      mientras el plazo sigue abierto --> RECALCULADO
      (evento, no estado exclusivo: el calculo vuelve a su estado anterior
       con la nueva fecha limite, el valor previo queda en el historial,
       se notifica al modulo de origen y a MOD-022; nunca se mueve en silencio)

  ABIERTO/PRORROGADO -- se cumple la fecha limite sin que el modulo
      de origen marque el caso resuelto --> bandera VENCIDO (paralela,
      visible junto al estado real, igual que en MOD-021 seccion F.1)

  ABIERTO/SUSPENDIDO/PRORROGADO -- el modulo de origen informa
      que el caso quedo resuelto (con o sin exceder la fecha) --> CERRADO
      (estado terminal para este calculo especifico)

  CERRADO -- termina el anio de retencion aplicable (ver MOD-016) --> ARCHIVADO_HISTORICO
      (estado terminal final; nunca se borra, anti-feature 19)
```

### F.4 Tabla de transiciones de un calculo de plazo individual

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (no existe) | Un modulo consumidor solicita un calculo (seccion D.2) | Evento de inicio, tipo de computo y duracion presentes | Abierto | Sistema (automatico, a peticion del modulo de origen) | Se calcula la fecha limite provisional con el desglose; se guarda la version del calendario usada (snapshot); evento de auditoria |
| Abierto | El modulo de origen declara una causal de suspension configurada (por ejemplo, prevencion del Art. 18, solo si la empresa activo la regla de D.3) | El campo "Es plazo suspendible" es Si | Suspendido | Modulo de origen (automatico, segun su propia logica) | Se detiene el conteo; se muestra tambien la fecha "sin suspension" como referencia mas exigente, mientras el criterio siga siendo incertidumbre juridica |
| Suspendido | El modulo de origen informa que ceso la causal | - | Abierto | Modulo de origen | Se reanuda el conteo desde donde quedo; evento de auditoria con la duracion exacta de la suspension |
| Abierto | El modulo de origen solicita una prorroga, dentro del plazo ordinario y con motivacion registrada en su propio expediente | La prorroga debe pedirse antes del vencimiento (analogia Art. 83 LPA); MOD-023 no valida el fondo de la motivacion, solo que llegue a tiempo | Prorrogado | Modulo de origen (por ejemplo, MOD-011 al aprobar la prorroga del Art. 20) | Se calcula la nueva fecha limite sumando la extension declarada; se conserva la fecha original |
| Abierto, Suspendido o Prorrogado | Se agrega o confirma un asueto ad hoc que cae dentro de la ventana de este plazo (evento paralelo de la seccion F.1) | El asueto queda Publicado con fuente documentada | El mismo estado, con el evento "recalculado" | Sistema (automatico, disparado por el cambio de calendario) | Nueva fecha limite; la anterior queda en el historial; se notifica al modulo de origen y a MOD-022; nunca se aplica sin dejar rastro |
| Abierto o Prorrogado | Se alcanza la fecha limite sin que el modulo de origen marque el caso resuelto | Automatico | El mismo estado, con la bandera "Vencido" | Sistema (automatico) | Se dispara el evento correspondiente para que el modulo de origen y MOD-021/MOD-022 lo muestren y alerten |
| Abierto, Suspendido o Prorrogado | El modulo de origen informa que el caso quedo resuelto | - | Cerrado | Modulo de origen | Fecha de cierre registrada; el calculo queda disponible para consulta y para el paquete de evidencias |
| Cerrado | Se cumple el periodo de retencion documental aplicable (regla de MOD-016, ver seccion J) | - | Archivado historico | Sistema (automatico, con la misma regla de retencion que el expediente de origen) | Se conserva de forma indefinida como evidencia historica; nunca se elimina |

**Registros vinculados.** Cuando un calculo se recalcula por un cambio de calendario, cualquier tarea de MOD-021 que muestre esa fecha limite se actualiza automaticamente (MOD-021 nunca calcula el plazo por su cuenta, siempre refleja el valor vigente de MOD-023, segun su propia ficha, seccion L). Cuando un calculo se cierra, el modulo de origen decide si archiva o no su propio expediente; MOD-023 no cierra por si mismo el expediente del modulo de origen, solo su propio registro de calculo.

---

## G. Automatizaciones

| # | Disparador | Condicion | Accion | Configurable por la empresa |
|---|---|---|---|---|
| 1 | Un modulo consumidor solicita un calculo de plazo | Evento de inicio, tipo de computo, duracion y capa de calendario presentes (seccion D.2) | Aplicar el algoritmo correspondiente: para dias habiles, contar desde el dia siguiente al evento de inicio, saltando fin de semana (capa 0), calendario nacional (capa 1), asuetos ad hoc (capa 2) y, si corresponde, asuetos locales de la sucursal (capa 3); para dias corridos, contar todos los dias sin excluir ninguno; para horas corridas, contar horas de reloj continuo; para horas habiles, contar solo horas dentro del horario habil configurado en dias habiles; para meses o anios, contar de fecha a fecha (Art. 82 LPA); si el ultimo dia cae en inhabil, trasladar al primer dia habil siguiente | No en el algoritmo (Art. 82 LPA); si en que capas de calendario aplican segun la capa declarada |
| 2 | El calculo usa la capa "Empresa frente a la autoridad (ACE)" | La solicitud declaro Capa de calendario = 5 | Excluir ademas los sabados, domingos y las vacaciones colectivas de la Ley de Asuetos de los Empleados Publicos (Semana Santa completa, 1 a 6 de agosto, 24 de diciembre a 2 de enero) | No |
| 3 | Se recibe una solicitud fuera del horario habil configurado o en un dia inhabil | La empresa configuro un horario habil (seccion D.3) | Marcar la fecha de recepcion efectiva para el registro, pero iniciar el conteo del plazo el dia habil siguiente a la recepcion, mostrando tambien la fecha mas exigente (desde la recepcion real) como referencia de prudencia | Si, el horario habil configurado |
| 4 | Se publica o actualiza una version del calendario mientras existen calculos en estado Abierto, Suspendido o Prorrogado cuya ventana de fechas se ve afectada | La nueva fecha (asueto ad hoc) cae entre el evento de inicio y la fecha limite actual de al menos un calculo | Recalcular automaticamente cada calculo afectado, conservar el valor anterior en el historial, notificar al modulo de origen y a MOD-022 (regla explicita de la tarea: nunca mover un plazo en silencio) | No (el recalculo automatico no es opcional; si lo es el canal de la notificacion) |
| 5 | Llega el 1 de noviembre de un anio sin que exista una version Publicada del calendario del anio siguiente | Automatico | Disparar la alerta "calendario del proximo anio no cargado" (seccion I) | No |
| 6 | Un modulo consumidor marca un plazo como suspendible y se cumple su causal | La regla de suspension esta activada en la configuracion de la empresa (seccion D.3) | Pasar el calculo a Suspendido y detener el conteo | Si, activar o no la regla de suspension (con doble control, seccion C) |
| 7 | Faltan N dias habiles u horas (configurable por el modulo de origen) para el vencimiento de un calculo Abierto o Prorrogado | El modulo de origen define su propio umbral (por ejemplo, MOD-011 usa 5 dias habiles para el plazo general; para el cronometro de 72 horas de incidentes, `01_legal/sweep_plazos_calendario_retencion.md` seccion 2.5 propone 24, 48 y 60 horas como valor por defecto, ver seccion I) | Emitir el evento "plazo proximo a vencer" hacia el modulo de origen y hacia MOD-022 | Si, el umbral lo define cada modulo consumidor, no MOD-023; MOD-023 solo documenta el valor por defecto recomendado por el sweep |
| 8 | Un calculo llega a su fecha limite sin que el modulo de origen lo marque Cerrado | Automatico | Activar la bandera "Vencido" y emitir el evento correspondiente | No |
| 9 | Se agrega una sucursal nueva en MOD-001 en un municipio sin fiesta patronal registrada en la Capa 3 | Automatico | Alertar al Administrador para que registre la fiesta patronal local con su fuente, antes de que esa sucursal participe en calculos que dependan de la capa 3 | No en la deteccion; si en como se resuelve (queda como tarea pendiente hasta que se documente) |
| 10 | Se activa la bandera de regimen FUTURO en MOD-024 (reforma 659) | Cambio confirmado manualmente por el equipo del producto | Ningun recalculo de plazos: la regla de computo de OBL-PLAZO-01 y el calendario de OBL-PLAZO-02 son los mismos en ambos regimenes (notas_reforma_659 de `mapa_modulos.json`); MOD-023 no reacciona a este evento | No aplica |

---

## H. Decisiones que NO debe automatizar

- **Si el Art. 82 de la Ley de Procedimientos Administrativos aplica de forma supletoria a la relacion entre el titular y una empresa privada.** Texto de advertencia: "La aplicacion de esta regla de computo a su empresa se basa en la remision del Art. 62 de la Ley para la Proteccion de Datos Personales. Existe un argumento en contra (el Art. 2 de la Ley de Procedimientos Administrativos limita su ambito a la Administracion Publica). Requiere validacion de asesoria juridica." Razon: es la incertidumbre 1 de `sweep_plazos_calendario_retencion.md`, seccion 9; el sistema aplica el criterio mas defendible (Art. 82 LPA) por ser el que la propia ACE usa en sus instrumentos, pero no puede declarar resuelta una discusion juridica abierta.
- **Si el sabado debe tratarse como dia habil para una empresa privada que abre ese dia.** Texto de advertencia: "Por defecto el sistema trata el sabado como inhabil en todos los plazos frente al titular, porque es el criterio mas prudente. Su empresa puede configurar el sabado como habil solo para sus propias metas internas, nunca para exigir al titular un plazo mas corto. Requiere validacion de asesoria juridica si necesita un criterio distinto." Razon: incertidumbre 3 de la misma seccion 9.
- **Si las 72 horas del Art. 25 se cuentan en horas corridas o en horas habiles.** Texto de advertencia: "La ley no precisa si este plazo se cuenta en horas corridas u horas habiles. El sistema aplica por defecto el criterio mas conservador (horas corridas). Verifique este criterio con asesoria legal si el caso es critico" (texto estandar de `04_objetivo_exacto_del_producto.md`, seccion 1.3). Razon: incertidumbre 2 de la seccion 9 del sweep; cambiarlo exige el doble control de la seccion C, nunca una decision automatica del sistema.
- **Si la prevencion del Art. 18 suspende el computo del plazo general de 20 dias del Art. 20.** Texto de advertencia identico al que ya usa MOD-011 en su seccion H: "La ley no precisa si la prevencion suspende este plazo. El sistema aplica por defecto el criterio mas conservador (no suspende). Verifique este criterio con asesoria legal si el caso es critico." Razon: incertidumbre 4 de la seccion 9; MOD-023 solo ejecuta la regla que la empresa active, nunca decide por su cuenta cual es la correcta.
- **Confirmar que una fecha de fiesta patronal local es correcta sin que exista fuente documentada.** Texto de advertencia: "Esta fecha no tiene una fuente oficial verificable. No se puede usar para calcular un plazo legal hasta que se documente su origen (comunicado municipal o del Ministerio de Trabajo)." Razon: no existe una lista oficial centralizada de fiestas patronales (sweep seccion 3.4); aceptar una fecha sin fuente expondria a la empresa a un calculo indefendible ante una fiscalizacion.
- **Aplicar automaticamente un asueto ad hoc anunciado por prensa antes de que el equipo del producto confirme su alcance (sector publico, privado o ambos) y su fuente oficial.** Texto de advertencia: "Este posible asueto esta pendiente de confirmacion oficial y no se aplica todavia a ningun calculo." Razon: la lista oficial de decretos no siempre usa la palabra "asueto" en el titulo (sweep seccion 3.5), por lo que una fecha sin confirmar podria ser incorrecta o tener un alcance distinto (solo sector publico, por ejemplo).
- **Decidir por si mismo cual capa de calendario (empresa-titular o autoridad) aplica cuando un mismo tramite tiene un componente frente al titular y otro frente a la ACE** (por ejemplo, el plazo de comunicacion del nombramiento del delegado corre frente a la ACE, pero la notificacion interna al propio delegado corre frente a una persona dentro de la empresa). Texto de advertencia: "Verifique que la capa de calendario elegida corresponda al destinatario real de este plazo." Razon: es una decision que le corresponde al modulo propietario de la obligacion (MOD-002, MOD-011, MOD-013, MOD-024), no a este modulo, que solo ejecuta el calculo con la capa que se le indique.

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia o repeticion | Escalamiento (a quien y cuando) | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Calendario del proximo anio no cargado | Llega el 1 de noviembre del anio en curso sin una version Publicada del anio siguiente para las capas 1, 2 y 5 | WARNING | Equipo del producto | Plataforma interna del proveedor | Semanal mientras siga pendiente | A los 15 dias sin resolver, escala a nivel CRITICAL para el equipo del producto | Se publica la version del anio siguiente |
| Sucursal sin fiesta patronal local documentada | Se agrega una sucursal fuera de San Salvador sin registro en la Capa 3 | WARNING | Administrador de la organizacion | Plataforma + correo | Una vez al crearse la sucursal, luego mensual mientras siga pendiente | A los 60 dias, se copia a Legal/Compliance como riesgo de calculo incompleto | Se registra la fecha con fuente y verificacion |
| Recalculo aplicado a un plazo abierto por cambio de calendario | Se confirma un asueto ad hoc que cae dentro de la ventana de un calculo Abierto, Suspendido o Prorrogado | INFO (o WARNING si el recalculo acerca la fecha limite a menos de 3 dias habiles) | Responsable del expediente en el modulo de origen, Delegado/Responsable interno | Plataforma + correo | Una vez por cada recalculo | Si el recalculo deja menos de 1 dia habil para vencer, escala de inmediato al Administrador | El calculo se cierra o se recalcula de nuevo |
| Fuente de fiesta patronal local vencida (mas de 24 meses sin verificacion) | Pasan 24 meses desde la ultima fecha de verificacion de una fuente de Capa 3 | INFO | Administrador de la organizacion | Plataforma | Anual | No escala automaticamente | Se actualiza la fecha de verificacion |
| Cambio de criterio de computo pendiente de segunda aprobacion | Un usuario con rol Delegado o Legal inicia el cambio de un criterio ambiguo (seccion C) | WARNING | El segundo revisor requerido (Legal o Delegado, segun quien inicio) | Plataforma + correo | Diaria mientras siga pendiente | A los 5 dias habiles sin la segunda aprobacion, escala al Administrador | Se completa el doble control o se cancela el cambio |
| Cronometro de 72 horas de un incidente proximo a vencer (alertas intermedias) | Transcurren 24, 48 o 60 horas desde el evento de inicio de un calculo de tipo "Horas corridas" ligado a OBL-INC-01 u OBL-INC-02 | INFO a las 24 y 48 horas; WARNING a las 60 horas | Responsable de Seguridad/IT, Delegado/Responsable interno | Plataforma + correo | Una vez por cada umbral (24, 48 y 60 horas) | Si a las 60 horas el incidente sigue sin notificarse, escala de inmediato al Administrador y a Legal/Compliance | El calculo se cierra (incidente notificado) o alcanza las 72 horas y pasa a la bandera Vencido |
| Version del calendario aun en Borrador a menos de 30 dias del inicio del anio que cubre | Faltan 30 dias para el 1 de enero y la version del anio siguiente sigue en Borrador | HIGH | Equipo del producto | Plataforma interna del proveedor | Diaria | Inmediata a nivel CRITICAL interno del proveedor | La version pasa a Publicado |

Los umbrales de 24, 48 y 60 horas para el cronometro de incidentes son el valor por defecto propuesto por `01_legal/sweep_plazos_calendario_retencion.md` (seccion 2.5); siguen siendo, como el resto de esta tabla, un umbral que MOD-013 puede ajustar (ver automatizacion 7 de la seccion G), no una regla que MOD-023 imponga por su cuenta.

---

## J. Evidencia

| Evidencia que genera o conserva el modulo | Como se registra | OBL-ID que prueba | Retencion |
|---|---|---|---|
| Snapshot de la version del calendario usada en cada calculo | Referencia inmutable a la version exacta de HolidayCalendar vigente en el momento del calculo, aunque esa version cambie despues | OBL-PLAZO-01, OBL-PLAZO-02 | Igual que el expediente del modulo de origen (por ejemplo, 5 anios para un expediente ARCO-POL, segun MOD-011 seccion J) |
| Desglose completo de cada calculo (dia 1, dias u horas excluidos y su motivo, fecha resultante) | Registro estructurado ligado al calculo | OBL-PLAZO-01 | Igual que el expediente del modulo de origen |
| Historial de recalculos, con la fecha anterior, la fecha nueva y el motivo documentado | AuditLog append-only, sin edicion ni borrado para ningun rol (anti-feature 19) | OBL-PLAZO-02; principio de responsabilidad demostrada | Igual que el expediente del modulo de origen; minimo 5 anios para el propio historial de calendario |
| Fuente documental de cada fecha del calendario (decreto, Diario Oficial, comunicado municipal, aviso oficial) | Adjunto con enlace o archivo, mas fecha de verificacion | OBL-PLAZO-02 | 10 anios (analogia con la retencion de documentacion regulatoria del sistema, ver `sweep_plazos_calendario_retencion.md`, seccion 8) |
| Registro de cada cambio del criterio de computo por defecto, con identidad de ambos aprobadores y fecha | Registro de doble aprobacion, distinto del registro de quien lo solicito | OBL-PLAZO-01, OBL-INC-01 | 5 anios (analogia con la prescripcion sancionadora, sweep seccion 6) |
| Registro de la fecha y hora real de recepcion de cada solicitud entrante que da inicio a un plazo | Timestamp capturado por el modulo de origen, referenciado por el calculo | OBL-PLAZO-01 | Igual que el expediente del modulo de origen |
| Mecanismo de verificacion de integridad (hash o firma validable de forma independiente) de cada paquete de evidencia exportado (seccion N) | Calculado automaticamente sobre el contenido completo del paquete al momento de exportarlo; se entrega junto con el paquete para que un tercero (por ejemplo, la ACE o un auditor externo) pueda comprobar despues que no fue alterado | OBL-PLAZO-01, OBL-PLAZO-02 (protege la misma evidencia probatoria del calculo que empaqueta) | Igual que el paquete de evidencia que protege |

**Sobre el plazo de retencion propio de este modulo.** Ni la LPDP ni la Normativa Sancionadora fijan un plazo expreso de conservacion para el historial del motor de plazos en si. Este modulo aplica por analogia la misma logica que MOD-011 aplica a sus expedientes (minimo 5 anios desde el cierre del calculo, tomando como referencia la prescripcion de infracciones y sanciones de 5 anios, Art. 47 Normativa PAS y Art. 29 Ley de Ciberseguridad), marcado como "criterio propio del producto ante ausencia de norma expresa, requiere validacion de asesoria legal", igual que hace MOD-011 en su seccion J.

---

## K. Documentos asociados

- **Documentos requeridos como entrada.** Fuente documental de cada fecha del calendario: decreto legislativo, pagina del Diario Oficial, comunicado de la alcaldia respectiva, aviso del Ministerio de Trabajo y Prevision Social, o noticia oficial de la Asamblea Legislativa cuando el decreto aun no este publicado en el Diario Oficial (ver `00_contexto_para_agentes.md`, seccion 2, sobre las fuentes ya descargadas del corpus juridico).
- **Documentos generados.**
  - Reporte de calendario vigente por anio (ver seccion N).
  - Nota de recalculo (documento breve que enumera el plazo afectado, la fecha anterior y la nueva, y el motivo), disponible dentro del expediente del modulo de origen.
  - Constancia de cambio de criterio de computo, con identidad de ambos aprobadores.
- **Plantillas que el sistema provee.**
  - Ficha de registro de fuente de asueto local por sede (municipio, fecha, tipo de fuente, enlace o archivo, fecha de verificacion), que el Administrador completa al configurar la Capa 3. Requiere validacion de la organizacion antes de usarse para calcular un plazo legal.
- **Anexos y evidencias documentales.** Cada fuente cargada en la seccion D.1 queda vinculada a la version del calendario correspondiente y disponible para el paquete de evidencias exportable de MOD-019, junto con el snapshot de calendario de cada calculo especifico que la use.

---

## L. Dependencias

### L.1 Diagrama

```
                    (sin dependencias de entrada:
                     MOD-023 es un punto de entrada/configuracion,
                     depende_de = [] en mapa_modulos.json)

                    +---------------------------------------------+
                    |     MOD-023 CALENDARIO Y MOTOR DE PLAZOS     |
                    |     CalendarEvent ; HolidayCalendar          |
                    +----+------+------+------+------+------+-----+
                         |      |      |      |      |      |
                         v      v      v      v      v      v
                    MOD-002  MOD-011 MOD-013 MOD-021 MOD-022 MOD-024
                    (Delegado)(ARCO- (Inci-  (Tareas)(Notif.)(Regu-
                              POL)   dentes)                  latorio)

  Consumo adicional documentado en las fichas ya redactadas, mas alla
  de la lista alimenta_a formal de mapa_modulos.json (ver nota L.3):

     MOD-006 (RAT, fecha de proxima revision) ---> MOD-023 (lectura)
     MOD-007 (Consentimiento, plazos de revocacion 5+5 dias) --> MOD-023
     MOD-008 (Documentos, fecha de revision programada) -------> MOD-023
     MOD-009 (Proveedores, periodicidad de revision) -----------> MOD-023
     MOD-010 (Transferencias, revision periodica) --------------> MOD-023
     MOD-012 (Portal del Titular, dias restantes, solo lectura) > MOD-023
     MOD-014 (Riesgos/EIPD, fecha de proxima revision) ---------> MOD-023
     MOD-015 (Controles, alertas de revision periodica) --------> MOD-023
     MOD-016 (Retencion, fecha efectiva de retencion) -----------> MOD-023
     MOD-018 (Auditoria, recordatorio del ciclo anual) ----------> MOD-023
```

### L.2 Lista de dependencias

**De que modulos recibe datos (depende_de, segun `mapa_modulos.json`):** ninguno. MOD-023 es, junto con MOD-001 y MOD-024, uno de los tres modulos que la seccion 6.1 de `06_mapa_definitivo_de_modulos.md` describe como fuente de referencia constante para practicamente todo el sistema (identidad de organizacion, plazos, o estado normativo vigente), sin que eso implique que dependa de ningun otro modulo para funcionar: su unica entrada de configuracion es la que aporta el equipo del producto (calendario nacional y de la autoridad) y la propia empresa (calendario local y propio, seccion D).

**A que modulos envia datos o eventos (alimenta_a, segun `mapa_modulos.json`):** MOD-002 (Delegado / Responsable Interno de Datos), MOD-011 (ARCO-POL), MOD-013 (Incidentes de Seguridad), MOD-021 (Centro de Tareas), MOD-022 (Notificaciones), MOD-024 (Centro Regulatorio). Esta lista coincide exactamente con los cuatro modulos propietarios de las obligaciones colaboradoras que este modulo calcula (MOD-002, MOD-011, MOD-013, MOD-024) mas los dos modulos transversales que instrumentan el resultado de cada calculo (MOD-021 aloja la fecha limite en una tarea; MOD-022 decide el canal de cada alerta).

**Que ocurre si un modulo dependiente no existe en el MVP.** No aplica como escenario real para MOD-023: al no tener `depende_de`, este modulo nunca queda bloqueado por la ausencia de otro. Lo relevante es el escenario inverso, ya cubierto en la seccion Q: MOD-023 mismo es MUST HAVE y sostiene a otros cuatro modulos MUST HAVE (MOD-002, MOD-011, MOD-013) y a la barra transversal (MOD-021, MOD-022, MOD-024); su ausencia si bloquearia a todos ellos, razon por la cual el mapa definitivo lo declara la unica excepcion real entre los transversales que posee una obligacion propia (`06_mapa_definitivo_de_modulos.md`, seccion 2, principio 5).

### L.3 Nota sobre el consumo mas amplio que el declarado en `alimenta_a`

Al revisar con `grep -n "MOD-023"` cada ficha ya redactada (MOD-002, MOD-003, MOD-006, MOD-007, MOD-008, MOD-009, MOD-010, MOD-011, MOD-012, MOD-013, MOD-014, MOD-015, MOD-016, MOD-018, MOD-021), se confirma que MOD-023 es consultado, ademas de por los seis modulos que `mapa_modulos.json` declara en su `alimenta_a`, tambien por MOD-006 (fecha de proxima revision del RAT), MOD-007 (plazos de revocacion del consentimiento y vencimiento de finalidad), MOD-008 (fechas de revision de documentos), MOD-009 (periodicidad de revision de proveedores), MOD-010 (revision periodica de transferencias), MOD-012 (lectura del conteo de dias restantes para el titular), MOD-014 (fecha de proxima revision de una EIPD), MOD-015 (alertas de revision periodica de controles) y MOD-018 (recordatorio del ciclo anual de auditoria). Esto no es una discrepancia del mapa: la propia seccion 6.1 de `06_mapa_definitivo_de_modulos.md` advierte de forma explicita que "MOD-001, MOD-023 y MOD-024 alimentan a practicamente todos los modulos porque proveen identidad de organizacion, plazos o el estado normativo vigente, sin que cada consumidor declare esa lectura de referencia constante como una dependencia estructural propia", y que esa asimetria "es intencional". Esta ficha documenta ese consumo mas amplio en el diagrama L.1 precisamente para que quede trazado en algun lugar, sin proponer ningun cambio al campo `alimenta_a` de `mapa_modulos.json`, que ya es correcto para lo que esta disenado a expresar (la dependencia estructural minima, no cada lectura de referencia).

**Sobre la asimetria senalada por la ficha de MOD-002 (no corregida aqui).** La ficha de MOD-002 (su seccion L) senala que, aunque `06_mapa_definitivo_de_modulos.md` y `mapa_modulos.json` declaran que MOD-023 "sale hacia" MOD-002 (coherente con el `alimenta_a` de MOD-023 verificado en esta ficha), el propio `depende_de` de MOD-002 no incluye a MOD-023 como entrada. Esta ficha confirma, desde el lado de MOD-023, que la relacion si existe en la practica (MOD-002 consulta a MOD-023, segun la propia ficha de MOD-002, linea 313, para sus contadores de 3, 10 y 15 dias habiles y de 1, 3 y 5 anos) y coincide con la recomendacion ya dejada por MOD-002 de agregar MOD-023 a su propio `depende_de`; no se modifica ningun archivo fuente desde esta ficha.

---

## M. Dashboard

Todos los indicadores se expresan como estado del programa (calendario cargado, plazos activos, recalculos aplicados), nunca como porcentaje de cumplimiento legal (`04_objetivo_exacto_del_producto.md`, seccion 1.2).

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Calendario del anio en curso y del proximo anio | Estado de la version (Vigente/Actualizada para el anio en curso; Publicado o Borrador para el anio siguiente) | Verde si el anio siguiente ya esta Publicado antes del 1 de noviembre; amarillo si esta en Borrador; rojo si no existe version | Administrador, Gerencia, Auditor |
| Plazos legales actualmente en curso (Abiertos, Suspendidos o Prorrogados) | Conteo de calculos activos, agrupado por modulo de origen | Sin semaforo (indicador de volumen) | Gerencia, Delegado/Responsable interno, Legal |
| Plazos vencidos sin cerrar | Conteo de calculos con la bandera Vencido activa | Rojo si mayor a 0 | Gerencia, Delegado/Responsable interno, Auditor |
| Recalculos aplicados en los ultimos 12 meses | Conteo de eventos "recalculo aplicado" | Informativo, sin semaforo | Legal/Compliance, Auditor |
| Cobertura de fuente verificada en asuetos locales | Porcentaje de sucursales con fecha de fiesta patronal registrada y con fuente verificada en los ultimos 24 meses | Verde >= 100%, amarillo 80 a 99%, rojo < 80% | Administrador, Auditor |
| Casos con criterio de computo ambiguo activo en su valor alternativo (no conservador) | Conteo de casos que cambiaron del criterio por defecto (por ejemplo, 72 horas habiles en vez de corridas) | Amarillo si mayor a 0, con enlace a la constancia de doble aprobacion | Legal/Compliance, Delegado/Responsable interno, Auditor |

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Calendario oficial vigente por anio | Todas las fechas inhabiles de las capas 0 a 5 aplicables, con su fuente | Anio, capa | PDF, XLSX | Administrador, Auditor, Auditor externo | Si |
| Historial de calculos de plazo | Cada calculo realizado, con evento de inicio, tipo de computo, fecha limite, version de calendario usada | Rango de fechas, modulo de origen, OBL-ID | XLSX, CSV | Delegado/Responsable interno, Legal/Compliance, Auditor | Si |
| Historial de recalculos | Cada recalculo aplicado, con fecha anterior, fecha nueva y motivo | Rango de fechas, modulo de origen | PDF, XLSX | Legal/Compliance, Auditor | Si |
| Registro de cambios de criterio de computo | Cada cambio de criterio ambiguo, con identidad de ambos aprobadores y fecha | Rango de fechas | PDF | Delegado/Responsable interno, Legal/Compliance, Auditor externo | Si |
| Paquete de evidencia de un calculo especifico | Desglose completo, snapshot del calendario usado, fuente de cada fecha excluida, y un hash o firma de verificacion de integridad calculado sobre el contenido completo del paquete (anti-feature 25 de `22_anti_features.md`: todo paquete de evidencia exportado debe permitir comprobar despues que no fue alterado) | Un calculo puntual | ZIP (PDF resumen mas anexos, mas el archivo o valor de verificacion de integridad) | Auditor, Auditor externo | Si, insumo directo para demostrar un plazo puntual ante la ACE |

---

## O. Historial

Eventos que quedan en el historial de este modulo y en el AuditLog transversal:

- Creacion de cada version anual del calendario (usuario o equipo del producto, fecha, capas incluidas).
- Cada fecha agregada, modificada o confirmada dentro de una capa, con su fuente y fecha de verificacion.
- Cada transicion de estado de una version del calendario (Borrador, Publicado, Vigente, Actualizada, Historico).
- Cada calculo de plazo realizado, con el modulo solicitante, el evento de inicio, el tipo de computo, la duracion y la fecha limite resultante.
- Cada suspension y reanudacion de un calculo, con la duracion exacta de la suspension.
- Cada prorroga aplicada, con la fecha original y la fecha prorrogada.
- Cada recalculo aplicado por un cambio de calendario, con el valor anterior, el valor nuevo y el motivo (nunca se sobrescribe sin dejar rastro).
- Cada cambio del criterio de computo por defecto en un caso ambiguo, con la identidad de ambos aprobadores.
- Cada cierre de un calculo y su paso a archivado historico.
- Exportaciones de reportes que incluyan este modulo (quien exporto, cuando, que reporte).

---

## P. Riesgos

- **Riesgo legal: aplicar el Art. 82 de la Ley de Procedimientos Administrativos como si fuera una regla ya confirmada para la relacion titular-empresa privada, cuando en realidad es una incertidumbre documentada.** *Mitigacion de diseno*: el sistema siempre muestra el fundamento y la advertencia de la seccion H junto al calculo, nunca lo presenta como una certeza.
- **Riesgo legal: que la empresa interprete el criterio por defecto de un plazo ambiguo (por ejemplo, 72 horas corridas) como la unica interpretacion valida ante una fiscalizacion.** *Mitigacion de diseno*: el "criterio de computo mostrado" (heredado por cada modulo consumidor, como ya documenta MOD-021 en su seccion D.1) siempre es visible junto a la fecha, con el texto estandar de `04_objetivo_exacto_del_producto.md`, seccion 1.3.
- **Riesgo de UX: mostrar el desglose tecnico completo (dia 1, cada dia excluido, capa aplicada) puede abrumar a una persona sin conocimiento juridico ni tecnico.** *Mitigacion de diseno*: la fecha limite se muestra siempre en lenguaje simple primero ("responder antes del [fecha]"), y el desglose completo queda disponible como una vista expandible opcional, coherente con la regla de oro de la plantilla (fundamento legal en segundo nivel).
- **Riesgo operativo: el calendario del anio en curso o del siguiente no se actualiza a tiempo, y todos los modulos que dependen de MOD-023 heredan fechas mal calculadas en cascada.** *Mitigacion de diseno*: la alerta escalonada de la seccion I (WARNING a partir del 1 de noviembre, HIGH si la version sigue en Borrador a menos de 30 dias del inicio del anio), y el hecho de que el calendario es mantenido de forma centralizada por el equipo del producto para todos los clientes a la vez, en vez de que cada empresa lo configure por separado con riesgo de errores dispersos.
- **Riesgo operativo: una fiesta patronal local mal configurada o sin fuente verificable produce un calculo indefendible para esa sucursal.** *Mitigacion de diseno*: el campo Fuente es obligatorio para la Capa 3 (seccion D.1); sin fuente documentada, el sistema no permite usar esa fecha para excluir un dia de un calculo legal (seccion H).
- **Riesgo operativo: mover una fecha limite sin que nadie lo note, si un asueto ad hoc se agrega despues de haber calculado un plazo ya en curso.** *Mitigacion de diseno*: la regla explicita de disenio de este modulo (secciones F y G) es que ningun recalculo ocurre en silencio: siempre se notifica, se conserva el valor anterior y se deja registrado el motivo.
- **Riesgo de seguridad y privacidad: bajo, porque este modulo no procesa datos personales de titulares (seccion D.2).** El unico dato identificable que maneja es el de los usuarios internos que configuran o aprueban cambios de calendario y de criterio, cubierto por el historial general del sistema (seccion O).

---

## Q. MVP

| Funcionalidad del modulo | Clasificacion | Justificacion |
|---|---|---|
| Calculo de dias y horas habiles con las capas 0, 1 y 2 (fin de semana, calendario nacional, asuetos ad hoc) | MUST HAVE | Condicion (b) del test de tres condiciones del mapa definitivo: sin esto, MOD-002, MOD-011 y MOD-013 (todos MUST HAVE) no pueden calcular correctamente sus plazos legales. |
| Regla de computo del Art. 82 LPA (inicio al dia siguiente, meses/anios de fecha a fecha, ultimo dia inhabil se traslada al siguiente habil) | MUST HAVE | Es OBL-PLAZO-01, obligacion propia de este modulo y base de todo el sistema de plazos. |
| Calendario de asuetos nacionales del Codigo de Trabajo y de los decretos D.L. 339/2016 y D.L. 208/2012 | MUST HAVE | Es OBL-PLAZO-02, obligacion propia; sin el calendario base no hay calculo posible. |
| Desglose visible de cada calculo (dia 1, dias excluidos y motivo, fecha resultante) | MUST HAVE | Es la unica forma de que el calculo sea verificable por la empresa y defendible ante una fiscalizacion; sin esto, el motor de plazos seria una caja negra. |
| Suspension y reanudacion de un calculo por causal declarada por el modulo de origen | MUST HAVE | MOD-011 (MUST HAVE) necesita esta capacidad desde el primer dia para la prevencion del Art. 18. |
| Recalculo automatico, notificado y con historial, cuando cambia el calendario mientras un plazo sigue abierto | MUST HAVE | Es la regla central de disenio de este modulo (nunca mover un plazo en silencio); sin ella, un asueto ad hoc podria dejar a la empresa con una fecha limite incorrecta sin saberlo. |
| Alerta de "calendario del proximo anio no cargado" | MUST HAVE | Es la unica forma de evitar que el sistema entero quede sin calendario valido al iniciar un anio nuevo. |
| Capa 5 (calendario de la autoridad, ACE) diferenciado de la capa de la empresa frente al titular | SHOULD HAVE, con cobertura minima en el MVP | El MVP puede lanzar aplicando las capas 0 a 2 tambien a los plazos frente a la autoridad (mas generoso para el plazo, nunca mas corto), mientras se completa la diferenciacion fina de las vacaciones colectivas de la Ley de Asuetos de los Empleados Publicos. |
| Capa 3 (asuetos locales por sede, fiestas patronales) configurable por la empresa con fuente obligatoria | SHOULD HAVE | El MVP puede operar con las capas 0 a 2 como base nacional; la capa local mejora la precision para sedes fuera de San Salvador, pero su ausencia no impide calcular los plazos generales del sistema. |
| Configurabilidad del criterio de computo de las 72 horas (corridas por defecto, horas habiles con doble control) | SHOULD HAVE | El valor por defecto (horas corridas) ya cubre el caso general desde el MVP; la opcion de cambiarlo es una mejora posterior para casos especificos con respaldo legal propio. |
| Vista de calendario central (area 30) con filtros por modulo, responsable y sucursal | MUST HAVE | Es la instrumentacion directa del area 30 del prompt de analisis funcional y la unica pantalla donde el usuario no especialista ve, en un solo lugar, todos sus plazos, revisiones, vencimientos y tareas. |
| Configuracion de horario habil propio y "sabado habil" solo para metas internas | COULD HAVE | Mejora de precision para empresas con horarios atipicos; el MVP puede operar con un horario habil por defecto razonable (por ejemplo, jornada diurna estandar) sin bloquear ningun otro modulo. |
| Sincronizacion de los eventos de la vista de calendario central con la aplicacion de calendario personal del usuario | FUTURE | Requiere definicion tecnica fuera del alcance de este analisis funcional; no es una dependencia estructural de ningun modulo MUST HAVE. |
| Vista consolidada de calendario entre varias sociedades de un mismo grupo corporativo | FUTURE | Coincide con el mismo criterio que MOD-021 aplica a su vista consolidada multi-sociedad (decision 2.7.31 de `02_validacion_de_la_idea.md`): funcionalidad V1/Enterprise, no MVP. |

**Version minima vendible del modulo.** La version minima que ya puede venderse incluye: el calculo de dias habiles con las capas 0 a 2, la regla de computo del Art. 82 LPA, el desglose visible de cada calculo, la suspension/reanudacion por causal declarada, el recalculo notificado con historial ante un cambio de calendario, la alerta de calendario no cargado, y la vista de calendario central del area 30. Esta combinacion ya resuelve el problema central de este modulo (que todos los plazos legales del sistema se calculen una sola vez, de la misma forma, con el mismo calendario) y es la unica forma de que MOD-002, MOD-011 y MOD-013 -todos MUST HAVE- puedan operar como fueron disenados.

---

## R. Ayuda contextual (complemento obligatorio)

**1. Que es un dia habil**
- *Que es*: un dia en que se cuenta el tiempo de un plazo legal; no son dias habiles los sabados, los domingos, los asuetos nacionales, los asuetos locales de su sucursal y los asuetos que decrete la Asamblea Legislativa.
- *Por que tengo que hacer esto*: porque la ley exige que ciertos plazos (por ejemplo, responder una solicitud de un titular) se cuenten solo en dias habiles, no en dias corridos.
- *Fundamento*: Art. 82 de la Ley de Procedimientos Administrativos (D.L. 856), aplicable de forma supletoria por el Art. 62 de la Ley para la Proteccion de Datos Personales (OBL-PLAZO-01); Art. 190 del Codigo de Trabajo (OBL-PLAZO-02).
- *Cuando necesito ayuda juridica*: si tiene dudas sobre si un dia especifico es habil o no para un caso critico, o si su empresa opera en un municipio cuya fiesta patronal no esta documentada en el sistema.

**2. Que es el motor de plazos (por que el mismo servicio calcula todos los plazos del sistema)**
- *Que es*: el unico lugar del sistema que calcula cuando vence cada plazo legal, para que ARCO-POL, el Delegado, los Incidentes y el Procedimiento sancionador usen siempre la misma cuenta, en vez de que cada uno calcule por su lado.
- *Por que tengo que hacer esto*: para que dos casos con el mismo tipo de plazo nunca tengan fechas distintas por un error de calculo, y para que una correccion del calendario se aplique una sola vez a todos los casos.
- *Fundamento*: decision de disenio del mapa definitivo de modulos (regla de conexion 3, `06_mapa_definitivo_de_modulos.md`, seccion 4); OBL-PLAZO-01 y OBL-PLAZO-02.
- *Cuando necesito ayuda juridica*: si no entiende por que una fecha limite especifica salio como salio, revise primero el desglose visible junto a la fecha; si aun asi tiene dudas sobre el fundamento legal, consulte a su Delegado o Responsable interno.

**3. Que es un recalculo y por que una fecha limite puede cambiar**
- *Que es*: cuando se confirma un nuevo dia inhabil (por ejemplo, un asueto decretado por la Asamblea Legislativa) que cae dentro de un plazo que ya estaba corriendo, el sistema vuelve a calcular la fecha limite de ese plazo, en vez de dejarla equivocada.
- *Por que tengo que hacer esto*: para que la fecha limite que ve siempre sea la correcta segun el calendario mas actualizado, sin que usted tenga que revisarlo manualmente.
- *Fundamento*: OBL-PLAZO-02; principio de este modulo de nunca mover un plazo sin dejar registro (ver el historial del calculo).
- *Cuando necesito ayuda juridica*: si un recalculo deja muy poco tiempo para cumplir el plazo, consulte de inmediato a su Delegado o Responsable interno para decidir como proceder.

**4. Diferencia entre un plazo frente al titular y un plazo frente a la Agencia de Ciberseguridad del Estado (ACE)**
- *Que es*: algunos plazos corren frente a una persona (por ejemplo, responder a quien pidio sus datos) y otros corren frente a la autoridad (por ejemplo, comunicarle a la ACE el nombramiento de su Delegado); el sistema puede usar un calendario ligeramente distinto para cada uno, porque la autoridad no atiende los mismos dias que una empresa privada.
- *Por que tengo que hacer esto*: para que el plazo se calcule con el calendario correcto segun a quien va dirigido.
- *Fundamento*: Ley de Asuetos, Vacaciones y Licencias de los Empleados Publicos (para el calendario de la autoridad); OBL-DPO-03, OBL-SANC-05 (ejemplos de plazos frente a la ACE).
- *Cuando necesito ayuda juridica*: si no esta seguro de si un tramite especifico corre frente al titular o frente a la autoridad, consulte a su Delegado o Responsable interno.

**5. Que significa que el sistema aplique un "criterio conservador" cuando la ley no es clara**
- *Que es*: cuando la ley no dice con precision como contar un plazo (por ejemplo, si las 72 horas de un incidente son horas corridas u horas habiles), el sistema elige por defecto la interpretacion mas prudente, es decir, la que le da menos tiempo a la empresa, para no arriesgarse a llegar tarde.
- *Por que tengo que hacer esto*: para que su empresa nunca confie en una interpretacion optimista de un plazo ambiguo sin saberlo.
- *Fundamento*: incertidumbres documentadas en `01_legal/sweep_plazos_calendario_retencion.md`, seccion 9 (por ejemplo, incertidumbres 1 a 4).
- *Cuando necesito ayuda juridica*: siempre que el sistema le muestre la advertencia de criterio conservador en un caso importante; cambiar ese criterio exige la aprobacion conjunta de su Delegado/Responsable interno y de Legal/Compliance, con respaldo de asesoria juridica.

**6. Que es la vista de calendario central**
- *Que es*: una sola pantalla donde ve, en un mismo lugar, todos los plazos legales, las revisiones periodicas, las auditorias, los vencimientos, las tareas y los casos de solicitudes de titulares e incidentes que le corresponden, filtrables por modulo, por responsable o por sucursal.
- *Por que tengo que hacer esto*: para no tener que entrar a 20 modulos distintos a buscar que fecha vence cuando.
- *Fundamento*: area 30 de `00_prompt_analisis_funcional.md` ("Calendario central: revisiones, plazos, auditorias, vencimientos, tareas, ARCO-POL, incidentes").
- *Cuando necesito ayuda juridica*: la vista central no requiere ayuda juridica por si misma; consulte la ayuda contextual del modulo especifico (por ejemplo, ARCO-POL o Incidentes) si tiene dudas sobre un caso puntual que ve alli.

---

## Nota final del agente (desacuerdos y observaciones sobre las fuentes de diseno)

1. **Ninguna discrepancia material con `mapa_modulos.json` ni con `06_mapa_definitivo_de_modulos.md`.** El nombre, el codigo, la etapa (Transversal), la clasificacion MVP (MUST HAVE), las areas del prompt que absorbe (30), las obligaciones propietarias (OBL-PLAZO-01, OBL-PLAZO-02), las colaboradoras (OBL-ARCO-08, OBL-ARCO-09, OBL-ARCO-10, OBL-DPO-02, OBL-DPO-03, OBL-INC-01, OBL-INC-02, OBL-SANC-05), el `depende_de` vacio y el `alimenta_a` (MOD-002, MOD-011, MOD-013, MOD-021, MOD-022, MOD-024) coinciden exactamente con la entrada de `mapa_modulos.json` y con la ficha resumida de la seccion 3 del mapa definitivo. Esta ficha comparte la clasificacion MUST HAVE del mapa sin reservas: el propio mapa ya identifica a MOD-023 como la unica excepcion real entre los modulos transversales que posee una obligacion de negocio propia (seccion 2, principio 5), precisamente por la razon que desarrolla la seccion A de esta ficha.
2. **El consumo real de este modulo es mas amplio que el declarado en `alimenta_a`, pero eso ya esta previsto y explicado por el propio mapa (seccion 6.1), no es una discrepancia.** Detallado en la seccion L.3: MOD-006, MOD-007, MOD-008, MOD-009, MOD-010, MOD-012, MOD-014, MOD-015 y MOD-018 consultan a MOD-023 en sus propias fichas, ademas de los seis modulos declarados formalmente. Esta ficha documenta ese patron en el diagrama L.1 sin proponer ningun cambio a `mapa_modulos.json`.
3. **Expectativas de las fichas ya escritas, y como quedaron satisfechas.** Se ejecuto `grep -n "MOD-023" analisis/03_modulos/*.md` sobre las 17 fichas existentes al momento de escribir esta (MOD-001 a MOD-016, MOD-018 y MOD-021; no existian aun MOD-017, MOD-019, MOD-020, MOD-022, MOD-024, MOD-025, MOD-026). Todas las menciones encontradas describen a MOD-023 como: (a) el unico servicio que calcula fechas limite en dias u horas habiles, nunca reimplementado por el modulo consumidor (MOD-002, MOD-006, MOD-007, MOD-008, MOD-009, MOD-010, MOD-011, MOD-012, MOD-013, MOD-014, MOD-015, MOD-016, MOD-018, MOD-021); (b) el que "siembra" o "arranca" un contador a partir de un evento de inicio y una duracion en dias habiles (MOD-002, MOD-003, MOD-011); (c) el que expone el "criterio de computo" visible junto a la fecha calculada (dias habiles, horas corridas, horas habiles), vocabulario que esta ficha adopta sin cambios (seccion D.2, campo "Tipo de computo"); (d) el que debe recalcular y nunca mover una fecha en silencio cuando cambia el calendario, y que MOD-021 en particular exige que "solo MOD-023 puede recalcular" el campo Fecha limite de una tarea, lo cual esta ficha satisface en las secciones F.3, F.4 y G (regla 4); (e) el que diferencia una capa de calendario para la empresa/titular de una capa para la autoridad (ACE), mencionada explicitamente por MOD-002 y MOD-024 (via OBL-DPO-03 y OBL-SANC-05); (f) el que alimenta la vista de calendario central del area 30 con filtros por modulo, responsable y sucursal, exigencia explicita de la tarea que esta ficha instrumenta en la seccion Q. Ninguna expectativa encontrada en las fichas existentes resulto incorrecta o contradictoria con el diseno que exige esta tarea: todas fueron compatibles y quedaron satisfechas con el mismo vocabulario que ya usaban (contador, criterio de computo, snapshot/version del calendario, recalculo, capa de calendario).
4. **Sobre la asimetria de `depende_de` que la propia ficha de MOD-002 ya senalo.** Ver el detalle en la seccion L.3: esta ficha coincide con la recomendacion de MOD-002 (agregar MOD-023 al `depende_de` de MOD-002 en `mapa_modulos.json`), sin modificar ningun archivo fuente desde aqui.
5. **Todas las afirmaciones juridicas de esta ficha citan su OBL-ID y su articulo** segun `01_legal/matriz_obligaciones.json` y se contrastaron contra `01_legal/sweep_plazos_calendario_retencion.md` y, para el Art. 82 LPA, contra la fuente primaria `01_legal/fuentes/asamblea_decreto_856_lpa.txt` (linea 1445). Donde la ley es ambigua (aplicabilidad del Art. 82 LPA a la relacion titular-empresa, si el sabado es habil, el computo de las 72 horas, y si la prevencion suspende el plazo de 20 dias), esta ficha lo senala explicitamente como incertidumbre que requiere validacion de asesoria juridica, en vez de asumir una interpretacion como cierta, siguiendo el mismo criterio conservador que ya documenta `sweep_plazos_calendario_retencion.md`, seccion 9.
6. **Correcciones aplicadas tras revision adversarial (2026-09-24), y un desacuerdo puntual con `mapa_modulos.json`.** Se agrego la seccion D.4 (catalogo consolidado de plazos, con al menos 14 plazos y las 8 columnas: plazo, valor y unidad, evento de inicio, modulo consumidor, OBL-ID, norma y articulo, tipo de computo, incertidumbre juridica), el mecanismo de verificacion de integridad del paquete de evidencia exportado que exige el anti-feature 25 (secciones J y N, que ya citaban ese item como fuente sin implementarlo), una fila de alertas intermedias a 24, 48 y 60 horas para el cronometro de incidentes (seccion I, con la referencia correspondiente en la automatizacion 7 de la seccion G), la columna de clasificacion OBLIGATORIO/CONDICIONAL en la tabla de la seccion A (OBL-ARCO-09, OBL-DPO-02, OBL-DPO-03 y OBL-SANC-05 son CONDICIONAL segun `matriz_obligaciones.json`, no OBLIGATORIO), y la correccion de los seis contadores completos de MOD-002 en la nota de la seccion L.3 (3, 10 y 15 dias habiles; 1, 3 y 5 anos, en vez de solo tres de ellos). La seccion D.4 documenta ademas un desacuerdo con `mapa_modulos.json`: su campo `obligaciones_colaboradoras` para MOD-023 (OBL-ARCO-08, OBL-ARCO-09, OBL-ARCO-10, OBL-DPO-02, OBL-DPO-03, OBL-INC-01, OBL-INC-02, OBL-SANC-05) no incluye OBL-ARCO-11, OBL-ARCO-12, OBL-CONS-03, OBL-DPO-04 ni OBL-SANC-06, aunque esta misma ficha (seccion B) ya mencionaba que MOD-023 calcula esos plazos; se recomienda revisar y completar ese campo en `mapa_modulos.json`, sin modificarlo desde aqui. No se aplico la exigencia de la revision de que el encargo original hubiera pedido "textualmente" una tabla de exactamente esas 8 columnas: no se encontro ningun documento accesible en el repositorio (ni `00_plantilla_ficha_modulo.md`, ni `00_contexto_para_agentes.md`, ni el mapa definitivo) que fije ese formato como obligatorio, y la revision tampoco cito una fuente verificable para esa afirmacion especifica; aun asi, se incorporo la tabla porque el vacio de fondo que senala (obligaciones citadas como consultadas pero nunca usadas en el cuerpo del documento) si es real y verificable, segun se detalla en la seccion D.4.


