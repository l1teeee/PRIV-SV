# MODULO: Riesgos y EIPD

Codigo corto del modulo: MOD-014
Clasificacion global del modulo: SHOULD HAVE (para el MVP)
Obligaciones que cubre:
- Propietaria: OBL-DOC-03 (Evaluaciones de Impacto en la Privacidad, Art. 4 Medidas Organizativas lit. e, Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Colaboradoras: OBL-SEG-02 (Art. 4 Medidas Organizativas lit. a-f, Politicas ACE), OBL-SENS-04 (Art. 39 LPDP, datos de salud), OBL-SENS-06 (Art. 4 lit. g LPDP, biometria), OBL-SENS-08 (Arts. 4, 7, 12, 16 LPDP, videovigilancia y reconocimiento facial)

Fuente de esta ficha: `mapa_modulos.json` (entrada MOD-014), `06_mapa_definitivo_de_modulos.md` (seccion "MOD-014 Riesgos y EIPD"), `02_validacion_de_la_idea.md` (decision 2.7.3, decision 2.7.28), `05_tipos_de_usuario.md` (roles estandar), `04_objetivo_exacto_del_producto.md` y `22_anti_features.md` (limites del sistema), `01_legal\matriz_obligaciones.json` y `01_legal\03_hallazgos_regulatorios.md` (fundamento juridico). Fecha de consulta: 2026-09-24.

---

## A. Proposito

- **Por que existe.** Las Politicas de Actuacion de la ACE obligan a realizar Evaluaciones de Impacto en la Privacidad (EIPD) como una de las seis medidas organizativas minimas (Art. 4, Medidas Organizativas, lit. e; OBL-DOC-03), pero no fijan formato, contenido minimo ni umbral de riesgo que determine cuando una EIPD especifica es obligatoria (hallazgo de ambiguedad numero 2 de `01_legal\03_hallazgos_regulatorios.md`, seccion 8). Este modulo traduce esa obligacion abierta en un proceso concreto que una persona sin formacion juridica puede ejecutar: detecta cuando un tratamiento entra en una categoria de alto riesgo, guia un cuestionario, calcula un nivel de riesgo de apoyo, organiza las medidas de mitigacion y deja evidencia de que la evaluacion se hizo y de quien la aprobo.
- **Que problema resuelve para la empresa.** Sin este modulo, la evaluacion de un tratamiento de alto riesgo (biometria de marcaje, camaras con reconocimiento facial, datos de salud, datos de menores) queda en la cabeza de una sola persona, sin metodologia, sin registro fechado y sin aprobacion formal. Eso deja a la empresa sin evidencia defendible si la ACE pregunta por que se considero segura una camara con reconocimiento facial en una tienda, y la expone al bloque de infraccion grave del Art. 56 lit. b num. 5 y 7 (no implementar medidas o controles exigidos por la ACE, entre ellos la EIPD).
- **Que obligacion u obligaciones cubre.** OBL-DOC-03 (propietaria, Art. 4 lit. e Politicas ACE, OBLIGATORIO) es la obligacion central: realizar EIPD para identificar y mitigar riesgos. El modulo tambien recoge la evidencia que prueba tres obligaciones colaboradoras que activan el analisis de riesgo por el tipo de dato: OBL-SENS-04 (Art. 39 LPDP, tratamiento de datos de salud, CONDICIONAL a giro sanitario), OBL-SENS-06 (Art. 4 lit. g LPDP, informacion biometrica como dato sensible, OBLIGATORIO) y OBL-SENS-08 (Arts. 4, 7, 12 y 16 LPDP, videovigilancia y reconocimiento facial, CONDICIONAL a que exista videovigilancia). Ademas documenta el cumplimiento general de OBL-SEG-02 (Art. 4 Medidas Organizativas lit. a-f Politicas ACE, OBLIGATORIO), porque la EIPD es una de las seis medidas organizativas que esa obligacion exige en bloque.
- **Que valor aporta.** Operativo: convierte una obligacion abstracta ("hacer EIPD") en un checklist con responsable, plazo y estado. Probatorio: deja un expediente fechado, firmado y exportable con verificacion de integridad, listo para un requerimiento de la ACE o para la auditoria anual (MOD-018). De reduccion de riesgo: obliga a pensar en medidas de mitigacion antes de que el tratamiento de alto riesgo quede en operacion normal, no despues de un incidente.
- **Que NO hace este modulo (limites explicitos).**
  - No decide si un tratamiento es legal ni si cumple la LPDP; el resultado del cuestionario es un calculo de apoyo interno, nunca una conclusion juridica (ver seccion H).
  - No sustituye la asesoria de un abogado ni la funcion de la persona con el rol Delegado de Proteccion de Datos o Responsable Interno; solo organiza la informacion que esa persona necesita para decidir.
  - No ejecuta ni instala controles tecnicos de seguridad (eso corresponde a MOD-015 Controles de Seguridad); solo selecciona controles existentes en ese catalogo o solicita que se cree uno nuevo.
  - No mantiene un catalogo propio de controles: usa el catalogo unico y compartido con MOD-015 (decision de alcance 2.7.3, que corrige la inconsistencia 3 detectada entre Riesgos/EIPD y Controles de Seguridad en el documento maestro).
  - No decide ni resuelve solicitudes ARCO-POL ni incidentes de seguridad; solo puede quedar referenciado desde esos modulos cuando el tratamiento involucrado tiene una EIPD vigente.
  - No califica si un pais de destino de una transferencia internacional tiene "nivel de proteccion adecuado" bajo el Art. 44: ese juicio queda siempre marcado como pendiente de validacion de la organizacion (anti-feature 18 de `22_anti_features.md`).
- **Nota sobre el doble estado de la reforma 659.** El contenido tecnico de este modulo no cambia con la reforma: OBL-DOC-03, OBL-SEG-02, OBL-SENS-04, OBL-SENS-06 y OBL-SENS-08 nacen de la LPDP y de las Politicas de Actuacion de la ACE, no de los Arts. 15 y 17 que la reforma deroga (por eso `mapa_modulos.json` marca "Notas reforma 659: No aplica directamente"). Lo que si cambia es quien aprueba formalmente la EIPD: en el estado ACTUAL (vigente hoy), la aprobacion final de una EIPD de riesgo Alto o Critico recae por defecto en la persona con el rol Delegado de Proteccion de Datos; si el estado FUTURO se activa (publicacion confirmada de la reforma mas 8 dias de vacatio legis, gestionado por el interruptor unico del Centro Regulatorio, MOD-024), esa misma funcion de aprobacion recae en la persona designada como Responsable Interno, sin que cambie el cuestionario, el calculo de riesgo ni la evidencia generada. El sistema reasigna la aprobacion pendiente al nuevo rol sin perder el historial de que version de la regla de aprobacion aplicaba a cada EIPD (ver seccion B y `05_tipos_de_usuario.md`, seccion 5.2).

---

## B. Usuarios

Roles estandar del sistema (`05_tipos_de_usuario.md`, seccion 5.3) que intervienen en este modulo:

| Rol estandar | Para que usa el modulo |
|---|---|
| Administrador de la organizacion | Configura si el modulo esta activo, define umbrales de configuracion (por ejemplo el plazo por defecto para completar una EIPD detectada) y ve el resumen agregado; normalmente no responde cuestionarios. |
| Delegado de Proteccion de Datos (o Responsable Interno en estado FUTURO) | Revisa el cuestionario, decide y aprueba junto con Legal el riesgo residual aceptable, coordina que las mitigaciones asignadas se ejecuten, y es quien por defecto recibe la tarea de aprobacion final en una EIPD de riesgo Alto o Critico (ver nota de la seccion A). |
| Responsable ARCO-POL / Responsable del tramite | Consulta si el tratamiento relacionado con una solicitud ARCO-POL tiene una EIPD vigente, por ejemplo para explicar a un titular por que existe una camara con reconocimiento facial en el area donde estuvo. Uso de solo lectura, ocasional. |
| Responsable Legal / Compliance | Redacta y valida la conclusion juridica separada del score (ver seccion H), revisa la base legal citada, deja constancia formal de su criterio cuando el caso lo amerita. |
| Responsable de Seguridad / IT | Completa la parte tecnica del cuestionario (medidas de seguridad ya existentes), selecciona o crea controles del catalogo compartido con MOD-015, y es quien normalmente ejecuta las tareas de mitigacion tecnica que la EIPD genera. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Responde el cuestionario inicial del tratamiento que le compete (por ejemplo RRHH ante un lector biometrico de marcaje, Operaciones ante camaras con reconocimiento facial), y ejecuta las tareas de mitigacion que no son tecnicas (por ejemplo colocar el aviso de videovigilancia). |
| Aprobador | Aprueba formalmente la EIPD antes de que pase a estado Vigente, segun la cadena de aprobacion configurada por la empresa; en pyme suele coincidir con el Delegado. |
| Auditor (interno) | Solo lectura y exportacion; consulta el estado y la evidencia de las EIPD existentes para la auditoria anual de cumplimiento (MOD-018, OBL-AUD-01). |
| Auditor externo (invitado) | Acceso temporal de solo lectura al paquete de evidencia de una o varias EIPD, durante la semana de auditoria externa. |
| Usuario de consulta / Colaborador | Ejecuta unicamente las tareas de mitigacion puntuales que le fueron asignadas desde una EIPD (por ejemplo "instalar el rotulo de videovigilancia en la entrada"), sin ver el expediente completo. |
| Titular (formulario externo) | No aplica: el titular no tiene acceso a este modulo. |
| Asesor externo invitado | Puede recibir acceso acotado en tiempo a una EIPD compleja puntual (por ejemplo, para dictaminar sobre un tratamiento de biometria con transferencia internacional asociada), sin acceso al resto de la organizacion. |

---

## C. Permisos

Columnas abreviadas: Admin = Administrador de la organizacion; Deleg = Delegado / Responsable Interno; ARCO = Responsable ARCO-POL; Legal = Responsable Legal/Compliance; Seg = Responsable de Seguridad/IT; Area = Responsable de area; Aprob = Aprobador; AudInt = Auditor interno; AudExt = Auditor externo invitado; Colab = Usuario de consulta/Colaborador; Asesor = Asesor externo invitado. El rol Titular no figura porque no tiene acceso al modulo (ver seccion B).

| Accion | Admin | Deleg | ARCO | Legal | Seg | Area | Aprob | AudInt | AudExt | Colab | Asesor |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver listado y resumen | Si | Si | Solo si relacionado | Si | Si | Solo su area | Si | Si | Solo asignado | No | Solo su caso |
| Ver expediente EIPD completo | Si | Si | Solo lectura si relacionado | Si | Si | Solo su area | Si | Si | Solo asignado | No | Solo su caso |
| Crear EIPD manual (fuera del disparo automatico) | Si | Si | No | Si | No | Si (su area) | No | No | No | No | No |
| Completar cuestionario | No | Si | No | No | Si (parte tecnica) | Si (su area) | No | No | No | No | No |
| Modificar respuestas antes del cierre | No | Si | No | No | Si (parte tecnica) | Si (su area) | No | No | No | No | No |
| Registrar mitigacion / seleccionar control | No | Si | No | No | Si | Si (no tecnica) | No | No | No | No | No |
| Redactar conclusion juridica | No | Si | No | Si | No | No | No | No | No | No | Si (opinion registrada) |
| Aprobar (pasar a Vigente) | No | Si, salvo doble control (ver nota) | No | Si, corresponsable en riesgo Alto/Critico | No | No | Si | No | No | No | No |
| Cerrar / archivar | No | Si | No | No | No | No | Si | No | No | No | No |
| Reabrir (revision o rechazo) | Si | Si | No | Si | No | No | Si | No | No | No | No |
| Eliminar | No | No | No | No | No | No | No | No | No | No | No |
| Exportar (paquete de evidencia) | Si | Si | No | Si | No | No | Si | Si | Si (solo lo asignado) | No | No |
| Asignar tarea de mitigacion | No | Si | No | No | Si | No | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si (su tarea) | Si (su caso) |
| Adjuntar evidencia | No | Si | No | Si | Si | Si (su area) | No | No | No | Si (su tarea) | Si (su caso) |

**Separacion de funciones.** Quien completa el cuestionario y registra las mitigaciones de un tratamiento (Responsable de area o Responsable de Seguridad) no puede ser la misma persona que da la aprobacion final cuando el riesgo calculado es Alto o Critico: en ese caso el sistema exige un segundo revisor (el Aprobador, distinto del autor) antes de permitir el paso a Vigente. Esta regla de doble control es una decision de producto (no existe mandato legal expreso de "cuatro ojos" en la LPDP), coherente con la regla general de separacion de funciones para tratamientos de riesgo alto documentada en `05_tipos_de_usuario.md`, seccion 5.4. Nadie puede eliminar una EIPD; solo puede archivarse, y el registro de auditoria (AuditLog) nunca es editable ni borrable, ni siquiera por el Administrador (anti-feature 19 de `22_anti_features.md`).

---

## D. Informacion de entrada

Notas de minimizacion de datos aplicables a toda la tabla: los campos que hacen referencia a un tratamiento, un proveedor, un sistema o una transferencia son **referencias** a la entidad ya registrada en MOD-006 (RAT), MOD-009 (Proveedores) o MOD-010 (Transferencias), nunca una copia de la base de datos de titulares. Ningun campo de este modulo esta disenado para recibir el dato personal real de un titular (por ejemplo, una plantilla biometrica o un registro de salud especifico); cuando se necesita adjuntar evidencia tecnica, la ayuda del campo advierte explicitamente que no debe subirse un dato personal directo del titular, sino documentacion tecnica del tratamiento (ficha del proveedor, captura de configuracion, politica interna).

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Tratamiento evaluado | Referencia a otra entidad (Treatment, MOD-006) | Obligatorio desde la creacion | Tratamientos activos del RAT de la organizacion | Debe existir en el RAT y estar en estado activo | "Elija el tratamiento del Registro de Actividades de Tratamiento que quiere evaluar. Si el tratamiento no existe todavia, registrelo primero en el RAT." | Buena practica; conecta con OBL-DOC-03 |
| Motivo de apertura (disparador) | Seleccion multiple | Obligatorio desde la creacion | Biometria; Datos de salud; Datos de menores; Monitoreo o videovigilancia; Perfilado o decisiones automatizadas; Gran escala; Transferencia internacional; Nueva tecnologia; Acceso de terceros/subcontratacion; Otro (texto libre) | Debe marcarse al menos un motivo | "Marque por que este tratamiento necesita una evaluacion de riesgo. Puede marcar varios, por ejemplo camaras (monitoreo) con reconocimiento facial (biometria)." | OBL-SENS-06, OBL-SENS-08, OBL-SENS-04, area 20 del prompt de analisis funcional |
| Origen de apertura | Seleccion unica, autogenerada | Obligatorio, no editable | Automatica desde Diagnostico; Automatica desde RAT; Manual (Responsable de area); Manual (Auditoria o revision) | No editable tras la creacion | "Este dato indica como se abrio la evaluacion: automaticamente porque el sistema detecto un factor de riesgo, o porque alguien la abrio a mano." | Trazabilidad, buena practica |
| Responsable de la evaluacion | Referencia a usuario | Obligatorio desde la creacion | Usuarios activos con un rol habilitado para completar el cuestionario (ver seccion C) | Debe tener un rol habilitado | "Persona encargada de completar y mantener actualizada esta evaluacion." | Principio de responsabilidad demostrada, OBL-PRIN-03 (Art. 5 lit. i LPDP) |
| Fecha de apertura | Fecha, autogenerada | Obligatorio, no editable | - | Fecha del sistema al crear el registro | "Fecha en que se abrio la evaluacion." | Evidencia |
| Descripcion del tratamiento | Texto largo | Obligatorio antes de completar el cuestionario | - | Minimo un parrafo | "Describa brevemente en que consiste el tratamiento: que se hace con los datos y para que." | Prellenado desde el RAT (finalidad, base juridica), editable |
| Volumen estimado de titulares afectados | Seleccion unica | Obligatorio antes de calcular el riesgo | Menos de 100; 100 a 1,000; 1,001 a 10,000; Mas de 10,000 | Debe seleccionarse una opcion | "Aproxime cuantas personas estan o estaran sujetas a este tratamiento. No hace falta una cifra exacta." | Factor "gran escala", area 20 del prompt |
| Categorias de datos tratadas | Seleccion multiple | Obligatorio, prellenado desde el RAT | Identificacion; Contacto; Financiero; Salud; Biometrico; Laboral; Menor de edad; Ubicacion; Judicial/penal; Otro sensible | Debe coincidir con lo declarado en el RAT para ese tratamiento, o justificar la diferencia | "Estas categorias vienen de lo que ya registro en el RAT para este tratamiento. Revise que sigan siendo correctas." | Catalogo compartido con OBL-SENS-01 a OBL-SENS-08 |
| Existe monitoreo o perfilado | Booleano + texto explicativo | Obligatorio | Si / No | Si es "Si", el texto explicativo es obligatorio | "Indique si el tratamiento vigila el comportamiento de las personas o genera perfiles automaticos sobre ellas (por ejemplo, puntajes de riesgo o segmentos de marketing)." | Area 20 del prompt |
| Uso de nuevas tecnologias o automatizacion | Booleano + texto explicativo | Obligatorio | Si / No | Si es "Si", el texto explicativo es obligatorio | "Indique si el tratamiento usa una tecnologia nueva para su empresa (por ejemplo inteligencia artificial, un lector biometrico nuevo) donde todavia no tiene experiencia previa." | Area 20 del prompt; sin definicion legal de "nueva tecnologia", criterio orientativo del producto |
| Transferencia internacional asociada | Referencia a otra entidad (Transfer, MOD-010), opcional | Opcional, prellenado si existe | Transferencias activas vinculadas al mismo tratamiento | Debe existir en MOD-010 | "Si este tratamiento envia datos fuera de El Salvador, aqui se muestra automaticamente esa transferencia ya registrada." | OBL-TRANSF-03 (Art. 44 LPDP); la calificacion de "pais adecuado" no la hace este modulo (ver seccion H) |
| Encargados o terceros involucrados | Referencia a otra entidad (Encargado/TerceroReceptor, MOD-009), multiple, opcional | Opcional, prellenado si existe | Encargados y receptores activos vinculados al tratamiento | Debe existir en MOD-009 | "Proveedores o terceros que participan en este tratamiento, tomados de lo ya registrado en Proveedores." | Factor "acceso de terceros", area 20 del prompt |
| Respuestas del cuestionario de factores de riesgo | Grupo de preguntas cerradas (ver seccion G) | Obligatorio antes de calcular el riesgo | Escala fija por pregunta (ver seccion G) | Todas las preguntas del cuestionario deben responderse | "Responda cada pregunta con la opcion que mejor describa su situacion actual, no la situacion ideal." | Base del calculo de riesgo, ver seccion E y G |
| Medidas de seguridad ya existentes | Seleccion multiple, referencia a Control (MOD-015) | Opcional al abrir; obligatorio antes de aprobar si el riesgo calculado es Alto o Critico | Controles activos del catalogo de MOD-015 | Si el riesgo es Alto/Critico y no hay controles ni justificacion, no se puede aprobar | "Seleccione los controles de seguridad que ya tiene implementados y que reducen este riesgo. Si el control que necesita no existe todavia, puede crearlo desde aqui." | OBL-SEG-02, catalogo compartido MOD-015 (decision 2.7.3) |
| Nivel de riesgo calculado | Calculado, no editable directamente | Generado automaticamente | Bajo / Medio / Alto / Critico | Se recalcula cada vez que cambian las respuestas del cuestionario | "El sistema calcula este nivel a partir de sus respuestas. Es un apoyo interno, no una calificacion legal." | Ver seccion E; metodologia propia del producto |
| Riesgo residual estimado | Calculado, no editable directamente | Generado tras registrar mitigaciones | Bajo / Medio / Alto / Critico | Se recalcula cada vez que cambian las mitigaciones registradas | "Nivel de riesgo que queda despues de aplicar las medidas de mitigacion que registro." | Ver seccion E |
| Conclusion (decision sobre el tratamiento) | Seleccion unica + texto largo | Obligatorio para cerrar/aprobar | Puede continuar; Requiere mitigacion antes de continuar; Debe suspenderse; Pendiente de asesoria especializada | Siempre visible junto a la leyenda de advertencia (ver seccion H) | "Esta es la decision final sobre el tratamiento. Aunque el sistema calculo un nivel de riesgo, esta decision la toma una persona de su organizacion, con apoyo legal si hace falta." | Decision no automatizable, ver seccion H |
| Evidencia adjunta | Archivo (uno o varios), opcional | Opcional pero recomendado si el riesgo es Alto/Critico | - | Tamano y formato segun politica general de adjuntos del sistema; nunca datos personales directos de un titular | "Adjunte documentacion tecnica de respaldo (ficha del proveedor, captura de configuracion, politica interna). No suba aqui datos personales reales de las personas afectadas por el tratamiento." | Evidencia, OBL-DOC-03; minimizacion de datos |
| Aprobador y fecha de aprobacion | Referencia a usuario + fecha, autogenerado | Obligatorio para pasar a Vigente | Usuario con rol habilitado para aprobar (ver seccion C) | Debe ser distinto del Responsable de la evaluacion cuando el riesgo es Alto o Critico | "Persona que aprobo formalmente esta evaluacion y fecha en que lo hizo." | Evidencia de aprobacion, OBL-DOC-03 |
| Fecha de proxima revision | Fecha, calculada con opcion de ajuste manual | Obligatorio al pasar a Vigente | Por defecto, 12 meses desde la aprobacion; ajustable por politica de la empresa | No puede ser anterior a la fecha de aprobacion | "Fecha en que el sistema le recordara volver a revisar esta evaluacion." | Buena practica, sin plazo legal expreso en la LPDP ni en las Politicas ACE |

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Expediente EIPD | Todos los campos de la seccion D mas el historial de estados | Registro interno navegable, exportable a PDF | Al crear la EIPD y en cada actualizacion | Roles con acceso segun seccion C |
| Nivel de riesgo (score) | Combinacion de Probabilidad x Impacto segun la matriz de la tabla siguiente | Etiqueta con semaforo (Bajo verde, Medio amarillo, Alto naranja, Critico rojo) | Automaticamente al completar el cuestionario, y cada vez que se edita una respuesta | Responsable de la evaluacion, Delegado, Legal |
| Riesgo residual | Mismo calculo aplicado despues de descontar el efecto de las mitigaciones registradas | Etiqueta con semaforo, igual escala que el riesgo inicial | Al registrar o modificar una mitigacion | Delegado, Aprobador |
| Tareas de mitigacion | Una tarea por cada medida pendiente, con responsable y fecha limite | Tarjeta de tarea en MOD-021 | Al identificar una mitigacion en el cuestionario o al aprobar con riesgo residual no Bajo | Responsable asignado (Area o Seguridad/IT) |
| Alertas | Ver tabla de la seccion I | Notificacion en plataforma, correo | Segun disparador de cada alerta | Segun tabla de la seccion I |
| Borrador de documento EIPD | Version imprimible del expediente completo, marcada "borrador pendiente de revision" hasta la aprobacion | PDF | Al solicitar exportacion o al cerrar el cuestionario | Delegado, Legal, Aprobador |
| Sugerencia de control faltante | Ficha de Control en estado "pendiente de implementar" con referencia a la EIPD que lo origino | Registro en MOD-015 | Cuando una mitigacion no coincide con ningun control existente del catalogo | Responsable de Seguridad/IT |
| Indicador de dashboard | Cantidad de EIPD por estado y por nivel de riesgo | Tarjetas y semaforos (ver seccion M) | Actualizacion continua | Segun vista de rol, ver seccion M |
| Paquete de evidencia exportado | Expediente completo, respuestas, mitigaciones, aprobaciones y evento de exportacion, con mecanismo de verificacion de integridad (hash o firma) | PDF/ZIP firmado | Al exportar para auditoria o para un requerimiento de la ACE | Auditor, Delegado, Administrador |

**Matriz de riesgo (metodologia propia del producto, no un formato oficial de la ACE).** El sistema calcula un puntaje de Probabilidad (1 a 4) y un puntaje de Impacto (1 a 4) a partir de las respuestas del cuestionario (ver seccion G) y los multiplica. La leyenda "metodologia propia del producto, no un formato oficial de la ACE" se muestra siempre junto al resultado, en linea con la ambiguedad documentada en `01_legal\03_hallazgos_regulatorios.md`, seccion 8, punto 2.

```
                          IMPACTO
                1 Menor  2 Moderado  3 Grave  4 Muy grave
P 1 Improbable    BAJO      BAJO      MEDIO     MEDIO
R 2 Posible        BAJO      MEDIO     MEDIO     ALTO
O 3 Probable       MEDIO     MEDIO     ALTO      CRITICO
B 4 Casi certero   MEDIO     ALTO      CRITICO   CRITICO
```

Escalas de referencia (configurables por la empresa dentro de un rango razonable, con el valor por defecto documentado aqui):
- Probabilidad 1 Improbable: no hay monitoreo continuo, no hay nueva tecnologia, controles de seguridad ya existentes cubren el escenario.
- Probabilidad 2 Posible: existe algun factor aislado (por ejemplo un encargado adicional) pero los demas factores estan controlados.
- Probabilidad 3 Probable: existen varios factores combinados (por ejemplo monitoreo continuo mas nueva tecnologia) sin control de mitigacion previo.
- Probabilidad 4 Casi certero: no existe ningun control de seguridad relacionado registrado y el tratamiento ya esta en operacion.
- Impacto 1 Menor: datos no sensibles, bajo volumen, sin afectacion previsible mas alla de una molestia.
- Impacto 2 Moderado: datos no sensibles pero de volumen alto, o dato sensible con exposicion limitada.
- Impacto 3 Grave: dato sensible (salud, biometrico, judicial) o titular menor de edad, con volumen medio o alto.
- Impacto 4 Muy grave: combinacion de dato sensible, menor de edad, gran escala o transferencia internacional sin verificar, con riesgo de discriminacion, dano economico o dano fisico previsible.

---

## F. Workflow

```
   [Disparador automatico]        [Apertura manual]
   (MOD-004 o MOD-006)            (Area, Auditoria)
          |                              |
          +---------------+--------------+
                          v
                     DETECTADO
                          |
                (se asigna responsable)
                          v
                      ABIERTO  <---------------------+
                          |                            |
              (cuestionario completo)                  |
                          v                             |
                     EVALUADO                          |
              (riesgo calculado)                       |
                          |                             |
        +-----------------+------------------+          |
        |                                    |          |
  riesgo Bajo/Medio                   riesgo Alto/Critico|
        |                                    v          |
        |                           EN_MITIGACION        |
        |                          (se registran         |
        |                        medidas y controles)     |
        |                                    |            |
        +-----------------+------------------+            |
                          v                                |
              PENDIENTE_DE_APROBACION                      |
                          |                                |
              +-----------+-----------+                    |
              |                       |                    |
          aprobada                rechazada -------------->+
              v                    (rework)
           VIGENTE
              |
     (llega fecha de revision o
      cambio material en el RAT)
              v
          EN_REVISION ---------------------------> (vuelve a ABIERTO si el
              |                                       cuestionario cambia
      (revision confirma sin cambios)                 sustancialmente)
              v
           VIGENTE
              |
   (tratamiento se marca inactivo
      o eliminado en el RAT)
              v
          ARCHIVADA (estado terminal)
```

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (ninguno) | Diagnostico o RAT detecta un factor de riesgo en un tratamiento sin EIPD vigente | El tratamiento no tiene ya una EIPD en estado Abierto/Evaluado/En_mitigacion/Pendiente/Vigente | DETECTADO | Sistema (automatico) | Crea tarea "completar cuestionario de riesgo" en MOD-021; evento en historial |
| (ninguno) | Responsable de area o Auditoria abre una EIPD manualmente | El tratamiento existe en el RAT | DETECTADO | Delegado, Responsable Legal, Responsable de area | Igual que el disparo automatico |
| DETECTADO | Se asigna o confirma el responsable de la evaluacion | Debe existir un responsable con rol habilitado | ABIERTO | Delegado, Administrador | Notifica al responsable asignado |
| ABIERTO | Se completan todas las preguntas obligatorias del cuestionario | Ninguna pregunta obligatoria queda vacia | EVALUADO | Responsable de la evaluacion, Responsable de Seguridad/IT | Calcula automaticamente el nivel de riesgo (ver seccion E); notifica al Delegado |
| EVALUADO | Riesgo calculado es Bajo o Medio y no se requieren mitigaciones adicionales | Ninguna | PENDIENTE_DE_APROBACION | Sistema (automatico) tras confirmacion del responsable | Crea tarea de aprobacion |
| EVALUADO | Riesgo calculado es Alto o Critico | Ninguna | EN_MITIGACION | Sistema (automatico) | Bloquea el paso directo a aprobacion; crea tarea de mitigacion a Seguridad/IT o Area |
| EN_MITIGACION | Se registra al menos una mitigacion (control existente o control nuevo) o una justificacion documentada de riesgo aceptado | Debe existir al menos un registro de mitigacion o justificacion antes de continuar | PENDIENTE_DE_APROBACION | Responsable de Seguridad/IT, Responsable de area, Delegado | Recalcula el riesgo residual; crea tarea de aprobacion |
| PENDIENTE_DE_APROBACION | Aprobador o Delegado aprueba | El aprobador debe ser distinto del responsable de la evaluacion si el riesgo (inicial o residual) es Alto o Critico | VIGENTE | Aprobador, Delegado (o Responsable Interno en estado FUTURO), corresponsable Legal en riesgo Alto/Critico | Registra fecha y usuario de aprobacion; calcula fecha de proxima revision; genera evidencia formal; notifica al responsable de area |
| PENDIENTE_DE_APROBACION | Aprobador rechaza y pide rediseño | Debe registrarse un motivo de rechazo | ABIERTO | Aprobador, Delegado | Notifica al responsable original; conserva el historial de la version rechazada |
| VIGENTE | Llega la fecha de proxima revision, o el RAT reporta un cambio material en el tratamiento (categoria de datos, volumen, finalidad, nuevo encargado) | Ninguna adicional | EN_REVISION | Sistema (automatico) | Genera alerta (ver seccion I); no interrumpe la vigencia mientras dura la revision |
| EN_REVISION | La revision confirma que no hay cambios sustanciales | Debe registrarse quien reviso y la fecha | VIGENTE | Delegado, Responsable Legal | Actualiza la fecha de proxima revision |
| EN_REVISION | La revision detecta cambios sustanciales que exigen recalcular el riesgo | Ninguna adicional | ABIERTO | Delegado, Responsable Legal | Conserva la version anterior como historico; abre una nueva ronda del cuestionario |
| VIGENTE | El tratamiento asociado se marca inactivo o se elimina del RAT | Ninguna adicional | ARCHIVADA | Sistema (automatico), o Delegado de forma manual | Conserva el expediente como evidencia historica; detiene las alertas de revision |
| Cualquier estado activo | Se solicita exportacion del expediente | Ninguna | (no cambia de estado) | Segun tabla de permisos (seccion C) | Genera paquete de evidencia con verificacion de integridad; registra evento de exportacion |

Estados terminales: **ARCHIVADA** (el tratamiento ya no existe u opero de forma indefinida) y, dentro de una version concreta, **RECHAZADA** solo como transicion hacia una nueva version en estado ABIERTO, nunca como estado final por si mismo. La reapertura desde EN_REVISION conserva siempre la version anterior en el historial, sin sobrescribirla, para que quede evidencia de que decisiones se tomaron con la informacion disponible en cada momento.

---

## G. Automatizaciones

Todas las reglas son configurables por la empresa dentro de los rangos indicados (plazos, umbrales), salvo donde se indique expresamente lo contrario.

1. **Disparador -> Diagnostico marca biometria, salud, menores o camaras (MOD-004).** Condicion: el tratamiento correspondiente en el RAT no tiene ya una EIPD vigente o en curso. Accion: crea una EIPD en estado DETECTADO y una tarea "completar cuestionario de riesgo" con plazo por defecto de 15 dias habiles (configurable), asignada al Responsable de area indicado por el diagnostico.
2. **Disparador -> Se registra o edita un tratamiento en el RAT (MOD-006) marcando una categoria de dato sensible, gran escala o transferencia internacional.** Condicion: no existe EIPD vigente o en curso para ese tratamiento. Accion: crea EIPD en estado DETECTADO, igual que el punto 1.
3. **Disparador -> Se completan todas las preguntas obligatorias del cuestionario.** Condicion: ninguna pregunta obligatoria vacia. Accion: calcula automaticamente el nivel de riesgo segun la matriz de la seccion E, pasa la EIPD a EVALUADO, notifica al Delegado.
4. **Disparador -> El riesgo calculado (inicial o residual) es Alto o Critico.** Condicion: no existe al menos una mitigacion registrada o una justificacion documentada. Accion: bloquea el paso a PENDIENTE_DE_APROBACION, crea tarea de mitigacion al Responsable de Seguridad/IT o de area segun el tipo de medida sugerida.
5. **Disparador -> Se registra una mitigacion que no coincide con ningun control existente en el catalogo de MOD-015.** Condicion: ninguna. Accion: crea automaticamente un Control en estado "pendiente de implementar" en MOD-015, referenciado desde la EIPD, y notifica al Responsable de Seguridad/IT.
6. **Disparador -> La EIPD pasa a PENDIENTE_DE_APROBACION.** Condicion: ninguna. Accion: crea tarea de aprobacion al Aprobador o al Delegado configurado (o al Responsable Interno si el estado FUTURO de la reforma 659 esta activo), con recordatorio periodico hasta que se resuelva.
7. **Disparador -> La EIPD es aprobada (pasa a VIGENTE).** Condicion: ninguna. Accion: calcula la fecha de proxima revision (por defecto 12 meses desde la aprobacion, ajustable por politica de la empresa), crea el evento correspondiente en el calendario (MOD-023), y registra la evidencia de aprobacion (ver seccion J).
8. **Disparador -> Llega la fecha de proxima revision, o el RAT reporta un cambio material en el tratamiento vinculado (categoria de datos, volumen, finalidad, nuevo encargado o transferencia).** Condicion: la EIPD esta en estado VIGENTE. Accion: genera alerta (ver seccion I) y pasa la EIPD a EN_REVISION sin interrumpir su vigencia mientras dura la revision.
9. **Disparador -> El tratamiento vinculado se marca inactivo o se elimina en el RAT.** Condicion: la EIPD esta en estado VIGENTE o EN_REVISION. Accion: pasa la EIPD a ARCHIVADA, detiene las alertas de revision, conserva el expediente como evidencia historica.
10. **Disparador -> Se exporta el expediente o un paquete de evidencia.** Condicion: ninguna. Accion: genera un mecanismo de verificacion de integridad (hash o firma validable de forma independiente) sobre el archivo exportado, siguiendo la decision de alcance 2.7.24 aplicada de forma transversal por MOD-019.

---

## H. Decisiones que NO debe automatizar

1. **Si el tratamiento es legal o cumple la LPDP.** El sistema calcula un nivel de riesgo de apoyo interno, no una conclusion sobre la legalidad del tratamiento. Texto de advertencia mostrado junto a todo resultado: "Este resultado es un calculo de apoyo interno basado en los factores que usted registro. No es una conclusion juridica sobre la legalidad del tratamiento. Requiere validacion de la organizacion o asesoria especializada." Razon: las Politicas ACE no fijan metodologia de scoring (hallazgo de ambiguedad 2), y el Art. 5 lit. i LPDP (principio de responsabilidad demostrada) exige que sea la empresa quien pueda justificar su decision, no un algoritmo.
2. **Decidir si el tratamiento continua, se mitiga o se suspende.** El campo "Conclusion" (seccion D) siempre lo completa una persona (Delegado o Responsable Legal), nunca el sistema, aunque el nivel de riesgo calculado sea Critico. Razon: es una decision de negocio y de criterio legal combinados, que puede depender de informacion que el cuestionario no captura.
3. **Determinar si una medida de mitigacion es suficiente.** El sistema puede sugerir que falta una mitigacion cuando el riesgo es Alto o Critico, pero no decide si la mitigacion registrada efectivamente reduce el riesgo a un nivel aceptable: esa valoracion la hace el Delegado o el Aprobador. Razon: la suficiencia de una medida tecnica u organizativa es un juicio experto que varia segun el contexto del tratamiento.
4. **Aceptar el riesgo residual.** El paso de EN_MITIGACION a PENDIENTE_DE_APROBACION nunca ocurre solo porque el calculo automatico baje de Alto a Medio; siempre requiere la aprobacion explicita de una persona con el rol habilitado (seccion C). Razon: aceptar un riesgo residual es una decision de gobierno corporativo, no un umbral numerico.
5. **Calificar si un pais de destino de una transferencia asociada tiene "nivel de proteccion adecuado".** El campo de transferencia asociada (seccion D) solo muestra la referencia a MOD-010; la EIPD no emite ningun juicio sobre la adecuacion del pais. Texto de advertencia: "La calificacion del nivel de proteccion de este pais no la determina el sistema. Requiere validacion de la organizacion o asesoria especializada." Razon: el Art. 44 LPDP no atribuye esa facultad a ningun organo y la ACE no ha publicado lista ni criterios (incertidumbre 11 de `01_legal\03_hallazgos_regulatorios.md`, seccion 9); es tambien un limite explicito del producto (anti-feature 18 de `22_anti_features.md`).
6. **Definir que constituye "gran escala" o "nueva tecnologia" para el caso concreto.** El sistema ofrece umbrales de referencia configurables (por ejemplo, mas de 10,000 titulares para "gran escala"), pero la calificacion final de si el tratamiento concreto encaja en esa categoria queda a criterio de la organizacion. Razon: ni la LPDP ni las Politicas ACE definen estos terminos con un umbral numerico (hallazgo de ambiguedad 2).

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia o repeticion | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Tratamiento de alto riesgo sin EIPD | Diagnostico o RAT detecta un factor de riesgo y no se completa el cuestionario dentro del plazo configurado | WARNING, pasa a HIGH al vencer el plazo | Responsable de area asignado | Plataforma + correo | Diaria mientras este vencida | Escala al Delegado tras 5 dias habiles sin avance | La EIPD pasa a EVALUADO |
| EIPD con riesgo Alto o Critico pendiente de mitigacion | La EIPD entra en estado EN_MITIGACION | HIGH | Responsable de Seguridad/IT o de area, Delegado | Plataforma + correo | Cada 3 dias habiles | Escala al Aprobador/Gerencia tras 10 dias habiles sin registro de mitigacion | Se registra al menos una mitigacion y se recalcula el riesgo residual |
| EIPD pendiente de aprobacion | La EIPD entra en estado PENDIENTE_DE_APROBACION | WARNING | Aprobador, Delegado (o Responsable Interno en estado FUTURO) | Plataforma + correo | Recordatorio semanal | Escala al Administrador de la organizacion tras 15 dias habiles sin resolucion | La EIPD pasa a VIGENTE o es rechazada |
| EIPD proxima a vencer (revision periodica) | Faltan 30 dias para la fecha de proxima revision | INFO, pasa a WARNING a 7 dias y a HIGH si vence sin revisar | Delegado, Responsable de la evaluacion original | Plataforma + correo | Unica a 30 dias; semanal si ya vencio | Escala al Administrador tras 30 dias habiles de vencida sin revision | La revision se completa (vuelve a VIGENTE o pasa a ABIERTO) |
| Cambio material en tratamiento con EIPD vigente | El RAT reporta un cambio en categoria de datos, volumen, finalidad, nuevo encargado o nueva transferencia del tratamiento vinculado | CRITICAL | Delegado, Responsable de area, Responsable Legal | Plataforma + correo inmediato | Unica al detectar el cambio | Escala de inmediato a Legal, sin espera | La EIPD entra en EN_REVISION y se confirma o recalcula |
| EIPD rechazada, pendiente de rediseño | El Aprobador rechaza la EIPD | WARNING | Responsable de la evaluacion original, Delegado | Plataforma + correo | Recordatorio a los 10 dias habiles sin reapertura | Escala al Delegado si nadie reabre en 15 dias habiles | La EIPD se reabre en estado ABIERTO |
| Control pendiente de implementar generado desde una EIPD | Se crea un Control en estado "pendiente de implementar" desde una mitigacion (regla G.5) | WARNING | Responsable de Seguridad/IT | Plataforma + correo | Semanal mientras siga pendiente | Escala al Delegado tras 30 dias habiles sin cambio de estado del control | El control pasa a "implementado" en MOD-015 |

---

## J. Evidencia

- **Registro con fecha y hora de cada cambio de estado.** Toda transicion de la tabla de la seccion F queda registrada con usuario, fecha, hora y estado anterior/nuevo, de forma append-only (sin edicion ni borrado posterior por ningun rol, ver `22_anti_features.md`, item 19).
- **Version de las respuestas del cuestionario.** Una vez que la EIPD pasa a EVALUADO, las respuestas quedan fijadas en esa version; si se reabre (por rechazo o por revision con cambios sustanciales), se crea una nueva version del cuestionario, conservando la anterior integra en el historial. Prueba OBL-DOC-03 (que la evaluacion efectivamente se hizo con la informacion disponible en ese momento).
- **Aprobacion con identidad y fecha.** El campo "Aprobador y fecha de aprobacion" (seccion D) es evidencia directa de OBL-DOC-03 y de OBL-SEG-02 (la EIPD como una de las seis medidas organizativas exigidas en bloque por las Politicas ACE).
- **Vinculo con las obligaciones de dato sensible que dispararon la evaluacion.** Cuando el motivo de apertura incluye biometria, salud o videovigilancia, el expediente conserva la referencia explicita a OBL-SENS-06, OBL-SENS-04 u OBL-SENS-08 respectivamente, de modo que el paquete de evidencia muestre no solo que se hizo una EIPD, sino que se hizo por el motivo legal correcto.
- **Historial de mitigaciones y su implementacion.** Cada mitigacion registrada queda enlazada al Control correspondiente en MOD-015, y la evidencia de que ese control esta efectivamente implementado (fecha, responsable, adjunto) se consulta desde alli, sin duplicar el dato en este modulo (evita que la EIPD "prometa" un control que el catalogo de seguridad no confirma, decision de alcance 2.7.3).
- **Exportacion firmada.** Todo paquete de evidencia exportado desde este modulo incluye un mecanismo propio de verificacion de integridad (hash o firma validable de forma independiente), siguiendo la decision de alcance 2.7.24, de modo que un auditor o la ACE puedan confirmar que el archivo no fue alterado despues de generado.
- **Retencion.** La EIPD es un documento de cumplimiento propio de la empresa (no un dato personal del titular), por lo que su regla de retencion la fija el motor documental de MOD-016 (Retencion y Eliminacion), no un plazo del dato del titular. Criterio propuesto por el producto, sin mandato legal expreso que fije este plazo especifico: conservar la EIPD mientras el tratamiento este activo, y un minimo adicional de 5 anos desde su archivo, por analogia con el plazo de prescripcion de infracciones y sanciones de la LPDP (Art. 47 Normativa PAS, 5 anos) [opinion de producto, criterio conservador ante la ausencia de una regla de retencion documental especifica para la EIPD en la LPDP o en las Politicas ACE].

---

## K. Documentos asociados

- **Documentos requeridos como entrada.** Ficha del tratamiento en el RAT (MOD-006); contrato o ficha tecnica del proveedor cuando el tratamiento involucra un encargado (por ejemplo el proveedor del sistema biometrico o de las camaras, MOD-009); politica de privacidad vigente relacionada, si el tratamiento ya esta en operacion.
- **Documentos generados.**
  - Documento EIPD (borrador, luego version final tras la aprobacion), con el cuestionario completo, el nivel de riesgo, las mitigaciones y la conclusion.
  - Registro de mitigaciones, como anexo o seccion del documento EIPD.
  - Constancia de aprobacion, con identidad y fecha del Aprobador.
  - Informe de riesgo residual, reutilizable como insumo del informe periodico del Delegado (OBL-DPO-07) o del informe de la auditoria anual (OBL-AUD-01, MOD-018). (Actualizacion 2026-09-24, fase 3: el ID citado era OBL-DPO-09, que no existe en la matriz; el area DPO llega hasta OBL-DPO-08 y el registro correcto para el informe periodico del Delegado es OBL-DPO-07.)
- **Plantillas que el sistema provee.**
  - "Plantilla generica de EIPD": cuestionario base con los campos de la seccion D. Variables: nombre del tratamiento, categorias de datos, base juridica, factores de riesgo marcados, mitigaciones. Siempre marcada "borrador pendiente de revision" hasta la aprobacion.
  - Plantillas orientadas por tipo de disparador (biometria, videovigilancia/reconocimiento facial, datos de salud, menores de edad), que preseleccionan las preguntas mas relevantes de ese tipo de tratamiento: funcionalidad COULD HAVE, ver seccion Q.
- **Anexos y evidencias documentales.** Documentacion tecnica de proveedores, capturas de configuracion, politicas internas relacionadas. Explicitamente excluidos: datos personales directos de titulares (biometricos, historiales de salud, imagenes de videovigilancia reales); ver nota de minimizacion en la seccion D.

---

## L. Dependencias

```
MOD-004 Diagnostico -----+
                          |
MOD-006 RAT y Mapa de     v
Datos --------------> MOD-014 Riesgos y EIPD
                          |
        +-----------------+-----------------+
        v                 v                 v
MOD-015 Controles   MOD-019 Centro     MOD-021 Centro
de Seguridad         de Evidencias      de Tareas

Capa transversal consultada (no depende_de estructural, ver 06_mapa_definitivo_de_modulos.md seccion 6.1):
MOD-001 Organizacion y Personas (identidad y roles)
MOD-009 Proveedores y Encargados (referencia de terceros involucrados)
MOD-010 Transferencias Internacionales (referencia de transferencia asociada)
MOD-020 Dashboard y Reportes (consume indicadores)
MOD-022 Notificaciones (canaliza alertas)
MOD-023 Calendario y Motor de Plazos (fecha de proxima revision)
MOD-024 Centro Regulatorio (estado ACTUAL/FUTURO de la reforma 659, para saber a quien asignar la aprobacion)
MOD-026 Centro de Ayuda (ayuda contextual, seccion R)
```

- **Entra desde:** MOD-004 Diagnostico de Cumplimiento (dispara la deteccion automatica de tratamientos de alto riesgo) y MOD-006 RAT y Mapa de Datos (aporta la ficha del tratamiento, sus categorias de datos y su base juridica).
- **Sale hacia:** MOD-015 Controles de Seguridad (selecciona o crea controles del catalogo unico compartido), MOD-019 Centro de Evidencias (entrega el expediente y el paquete exportado con verificacion de integridad) y MOD-021 Centro de Tareas (crea las tareas de cuestionario, mitigacion y aprobacion).
- **Que ocurre si un modulo dependiente no existe en el MVP.** MOD-004 y MOD-006 son ambos MUST HAVE, por lo que estaran disponibles en cualquier version del producto que incluya MOD-014; no hay escenario del MVP en que MOD-014 exista sin sus dos dependencias de entrada. MOD-015 (catalogo de controles) tambien es MUST HAVE, por lo que la seleccion de controles siempre tiene un catalogo real donde apoyarse. El unico escenario relevante es el inverso: si la propia organizacion no incluye MOD-014 en su version contratada o en una etapa temprana del despliegue (porque el modulo completo es SHOULD HAVE, no MUST HAVE), el patron de cobertura parcial documentado en `06_mapa_definitivo_de_modulos.md` (entrada de MOD-014) aplica: el diagnostico (MOD-004) igualmente detecta biometria, salud, menores o camaras, y en lugar de abrir un expediente EIPD con cuestionario y scoring, crea una tarea generica ("elaborar EIPD") en MOD-021 con una plantilla generica de documento en MOD-008, que la empresa llena manualmente sin el motor de calculo de riesgo. Esta ficha documenta el modulo completo; la cobertura parcial es el comportamiento del sistema cuando MOD-014 todavia no esta activo (ver tambien seccion Q).

---

## M. Dashboard

Ningun indicador de este modulo se expresa como "porcentaje de cumplimiento legal"; todos muestran estado del programa, controles configurados, tareas pendientes o evidencia disponible, segun el principio general del producto (`04_objetivo_exacto_del_producto.md`, seccion 1.2).

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Tratamientos de alto riesgo evaluados | (EIPD en estado EVALUADO, EN_MITIGACION, PENDIENTE_DE_APROBACION o VIGENTE) / (tratamientos con al menos un motivo de apertura detectado) | Verde si es igual a 1; amarillo si hay al menos una EIPD en DETECTADO sin avanzar; rojo si hay alguna vencida en el plazo de apertura | Gerencia: cifra agregada; Responsable: su propio avance; Legal: lista con motivo de apertura; Auditor: cifra con enlace a evidencia |
| EIPD vigentes | Cantidad de EIPD en estado VIGENTE | Sin semaforo, es un conteo informativo | Todas las vistas |
| EIPD pendientes de mitigacion (Alto/Critico) | Cantidad de EIPD en estado EN_MITIGACION | Amarillo si hay alguna dentro del plazo configurado; rojo si alguna supero el plazo de escalamiento | Gerencia: cifra agregada; Responsable: sus tareas; Legal: lista con nivel de riesgo; Auditor: cifra con enlace a evidencia |
| EIPD con revision atrasada | Cantidad de EIPD en estado EN_REVISION con fecha de proxima revision vencida | Amarillo si vencio hace menos de 30 dias habiles; rojo si vencio hace mas | Gerencia: cifra agregada; Responsable/Delegado: lista detallada; Auditor: cifra con enlace a evidencia |
| Distribucion por nivel de riesgo | Cantidad de EIPD vigentes agrupadas por Bajo/Medio/Alto/Critico | Semaforo por franja (verde/amarillo/naranja/rojo) | Gerencia: grafico resumen; Legal: lista detallada por nivel; Auditor: cifra con enlace a evidencia |
| Controles pendientes originados en una EIPD | Cantidad de Control en MOD-015 en estado "pendiente de implementar" con origen en este modulo | Amarillo si hay alguno; rojo si alguno supero el plazo de escalamiento de la alerta correspondiente | Responsable de Seguridad/IT; Gerencia: cifra agregada |

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Listado de EIPD | Todas las EIPD de la organizacion con estado, nivel de riesgo, responsable y fecha de proxima revision | Estado, nivel de riesgo, motivo de apertura, rango de fechas | PDF, XLSX | Delegado, Gerencia | Si, como indice del paquete general |
| Expediente EIPD individual | Version completa de una EIPD: cuestionario, mitigaciones, aprobacion, historial de estados | Una EIPD especifica | PDF (con verificacion de integridad) | Auditor, ACE (si se requiere), Legal | Si, es el documento probatorio principal |
| Reporte de riesgos por nivel | Conteo y detalle de tratamientos por nivel de riesgo (Bajo/Medio/Alto/Critico), con tendencia en el tiempo si hay historico | Rango de fechas, area de la empresa | XLSX, CSV | Gerencia, Delegado | Si, como evidencia de gestion de riesgo |
| Reporte de mitigaciones y controles pendientes | Mitigaciones registradas, su estado de implementacion y el control asociado en MOD-015 | Estado del control, responsable | XLSX | Responsable de Seguridad/IT, Delegado | Si, como evidencia de seguimiento |
| Paquete de evidencia de una EIPD | Expediente individual mas todos sus adjuntos y el registro de auditoria (AuditLog) filtrado a ese expediente, comprimido con verificacion de integridad | Una EIPD especifica | ZIP firmado | Auditor externo, ACE (si se requiere) | Es el paquete de evidencia en si mismo |

---

## O. Historial

Eventos que deben quedar registrados en el historial propio del modulo y, de forma identica, en el AuditLog transversal (MOD-018/MOD-019), siempre append-only:

- Creacion de la EIPD, con el motivo de apertura y el origen (automatico o manual).
- Cada cambio de campo del cuestionario, con valor anterior y valor nuevo, usuario y fecha/hora.
- Cada cambio de estado (tabla de la seccion F), con usuario, fecha/hora, estado anterior y estado nuevo.
- Asignacion o reasignacion del responsable de la evaluacion, o de una tarea de mitigacion.
- Registro de cada mitigacion (que control se selecciono o se creo) y su vinculo con MOD-015.
- Aprobacion o rechazo, con identidad de quien decidio, fecha/hora y, en caso de rechazo, el motivo registrado.
- Adjuntos: cada archivo subido o eliminado, con usuario y fecha/hora.
- Exportaciones del expediente o del paquete de evidencia, con usuario, fecha/hora y destino declarado (por ejemplo "para auditoria interna" o "para requerimiento de la ACE").
- Accesos de lectura al expediente completo por parte de un Auditor externo o un Asesor externo invitado (no se registran accesos de lectura de roles internos con acceso permanente, salvo el propio evento de apertura de sesion que ya cubre el AuditLog general).
- Archivado, con el motivo (tratamiento inactivo o eliminado en el RAT) y la fecha.
- Reasignacion de la aprobacion pendiente por cambio de estado ACTUAL a FUTURO de la reforma 659 (de Delegado a Responsable Interno), con fecha del cambio y version de la regla aplicada (ver seccion A).

---

## P. Riesgos

- **Riesgo legal: que el resultado del cuestionario se lea como una aprobacion legal del tratamiento.** Mitigacion de diseno: separacion explicita y visible entre el nivel de riesgo calculado (automatizable) y la conclusion (siempre humana, seccion H), con la leyenda de advertencia obligatoria en cada resultado y en cada exportacion.
- **Riesgo legal: que la metodologia de scoring propia del producto se presente como un estandar oficial de la ACE.** Mitigacion de diseno: la leyenda "metodologia propia del producto, no un formato oficial de la ACE" acompana siempre la matriz de riesgo (seccion E), consistente con la ambiguedad documentada en `01_legal\03_hallazgos_regulatorios.md`, seccion 8.
- **Riesgo de UX: abandono del cuestionario por extension o lenguaje tecnico.** Mitigacion de diseno: guardado progresivo de respuestas (no se pierde avance si se cierra la sesion), lenguaje simple en cada texto de ayuda con ejemplo concreto (seccion D), y division del cuestionario en bloques cortos por factor de riesgo en lugar de un formulario unico largo.
- **Riesgo de UX: que un Responsable de area no sepa distinguir "gran escala" o "nueva tecnologia" sin apoyo.** Mitigacion de diseno: cada pregunta del cuestionario trae ejemplos concretos del sector tipico del cliente (pyme, mediana, corporativo) y enlaza a la ayuda contextual (seccion R).
- **Riesgo operativo: que la matriz de riesgo quede mal calibrada para el perfil real de la empresa** (por ejemplo, que una pyme con datos de salud reciba siempre "Critico" y pierda confianza en el indicador). Mitigacion de diseno: los umbrales de la escala de Probabilidad e Impacto son configurables dentro de un rango razonable por el Administrador, con el valor por defecto documentado en la seccion E, y toda edicion de esos umbrales queda registrada en el historial.
- **Riesgo operativo: que una EIPD quede "Vigente" indefinidamente sin revisarse pese a cambios reales en el tratamiento.** Mitigacion de diseno: la regla automatizada G.8 que detecta cambio material en el RAT y fuerza el paso a EN_REVISION, mas la alerta de revision periodica (seccion I).
- **Riesgo de seguridad y privacidad: que se adjunte por error un dato personal real de un titular** (por ejemplo una fotografia de una persona identificada o un archivo con datos de salud reales) como evidencia de la EIPD. Mitigacion de diseno: el texto de ayuda del campo de evidencia advierte explicitamente contra esto (seccion D), y el modulo no ofrece ningun campo disenado para capturar el dato personal en si, solo referencias y documentacion tecnica.
- **Riesgo de seguridad: que alguien apruebe su propia evaluacion de riesgo Alto o Critico sin segundo revisor.** Mitigacion de diseno: la regla de doble control de la seccion C, que exige un Aprobador distinto del responsable de la evaluacion cuando el riesgo es Alto o Critico.
- **Riesgo de continuidad regulatoria: que la reasignacion de la aprobacion de Delegado a Responsable Interno, al activarse el estado FUTURO de la reforma 659, deje expedientes con un aprobador invalido o pierda trazabilidad.** Mitigacion de diseno: el cambio de estado se activa manualmente desde MOD-024, nunca automaticamente, y cada EIPD conserva registrada la version de la regla de aprobacion que le aplicaba al momento de cada decision (seccion O).

---

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Apertura automatica de la EIPD desde disparadores del Diagnostico y del RAT | X | | | | Es el punto de entrada que conecta el modulo con OBL-DOC-03 (OBLIGATORIO); sin el disparo automatico, el modulo no cumple su proposito minimo de deteccion, solo quedaria como un formulario que nadie sabe cuando abrir. |
| Cuestionario estructurado por factores de riesgo (seccion D y G) | X | | | | Es la base de toda evaluacion; sin cuestionario no hay informacion sobre la que calcular nada. |
| Seleccion de controles del catalogo compartido con MOD-015 | X | | | | MOD-015 ya es MUST HAVE; conectar la mitigacion al catalogo unico evita la divergencia que corrige la decision de alcance 2.7.3. |
| Flujo de aprobacion formal con registro de aprobador y fecha | X | | | | Es la evidencia minima que prueba OBL-DOC-03; sin aprobacion registrada, el expediente no demuestra que alguien con autoridad revizo el resultado. |
| Calculo automatico del nivel de riesgo (matriz Probabilidad x Impacto) | | X | | | El valor principal de la obligacion (que exista una EIPD) puede cubrirse con una clasificacion cualitativa simple hecha a mano; el motor de calculo ponderado mejora consistencia y velocidad, pero una version inicial podria pedir al responsable clasificar el nivel manualmente con las mismas cuatro etiquetas, sin formula. |
| Calculo automatico de riesgo residual tras mitigaciones | | X | | | Depende del motor de calculo anterior; puede iniciar con un recalculo manual simple hecho por el Delegado al registrar cada mitigacion. |
| Alertas de revision periodica y de cambio material en el RAT | | X | | | Mejora la vigencia del programa en el tiempo, pero una version inicial puede operar solo con la apertura y aprobacion inicial, sin el ciclo de revision automatizado. |
| Doble control obligatorio (Aprobador distinto del autor en riesgo Alto/Critico) | | X | | | Es una buena practica de separacion de funciones (opinion de producto, sin mandato legal expreso), postergable a una version donde ya existan varios roles activos en la empresa. |
| Sugerencia automatica de Control "pendiente de implementar" en MOD-015 | | | X | | Es una conveniencia de flujo; sin ella, el Responsable de Seguridad/IT puede crear el control manualmente en MOD-015 despues de leer la mitigacion registrada en la EIPD. |
| Plantillas de cuestionario especificas por tipo de disparador (biometria, videovigilancia, salud, menores) | | | X | | La plantilla generica unica ya cubre el requisito legal minimo; las plantillas especializadas mejoran la experiencia pero no son indispensables para que la EIPD exista y sea valida. |
| Reporte de tendencia de riesgo en el tiempo (historico multi-periodo) | | | X | | Util para Gerencia en empresas medianas/corporativas, pero no cambia si la obligacion legal se cumple o no en el periodo actual. |
| Mapa de calor consolidado multi-tratamiento o multi-sociedad | | | | X | Requiere volumen de EIPD acumulado y, en el caso multi-sociedad, depende de la vision consolidada de grupo que la decision de alcance 2.7.31 deja fuera del MVP. |
| Integracion de scoring especifico para transferencias internacionales (factor de riesgo propio del pais destino) | | | | X | Depende de que exista un criterio o catalogo de "nivel de proteccion adecuado" que hoy no existe (incertidumbre 11 de los hallazgos regulatorios); construirlo antes de esa base normativa arriesga dar una falsa sensacion de calificacion legal. |
| Versionado explicito y comparable de la metodologia de scoring (para poder decir "esta EIPD se calculo con la version 2 de la formula") | | | | X | Solo se vuelve necesario cuando la empresa acumula historial suficiente como para que un cambio de formula sea relevante; en el MVP y en V1 basta con conservar la version de las respuestas (seccion J). |

**Version minima que ya puede venderse.** La combinacion de disparo automatico desde el diagnostico y el RAT, cuestionario estructurado, clasificacion de riesgo (aunque sea con una escala cualitativa simple en lugar del motor de calculo ponderado completo), seleccion de controles del catalogo ya existente en MOD-015, aprobacion formal registrada y exportacion con verificacion de integridad ya deja a la empresa con una EIPD defendible frente a OBL-DOC-03, incluso sin las funcionalidades SHOULD/COULD/FUTURE de esta tabla. Por eso el modulo completo se mantiene clasificado SHOULD HAVE a nivel global (no MUST HAVE): las obligaciones que cubre son OBLIGATORIO pero se activan solo por disparadores especificos que el diagnostico ya detecta desde el MVP base, y el modulo no tiene un plazo transitorio vencido propio ni es una dependencia estructural de otro modulo MUST HAVE (justificacion identica a la de `mapa_modulos.json`).

**Nota sobre la cobertura parcial mientras MOD-014 no esta activo.** Tal como documenta la entrada de MOD-014 en `06_mapa_definitivo_de_modulos.md`, si la version del producto no incluye este modulo todavia, el sistema no deja el vacio sin cubrir: el diagnostico (MOD-004) igual detecta biometria, salud, menores o camaras y crea una tarea "elaborar EIPD" en MOD-021 con una plantilla generica de documento en MOD-008, llenada manualmente y sin el motor de scoring. Esta ficha coincide con esa decision y no encuentra ninguna inconsistencia que senalar al respecto (ver nota final).

---

## R. Ayuda contextual (complemento obligatorio)

**1. Que es una EIPD (Evaluacion de Impacto en la Privacidad)**
- Que es: un analisis por escrito de un tratamiento de datos que puede afectar de forma importante a las personas (por ejemplo, porque usa datos biometricos, de salud, de menores, o porque hay camaras con reconocimiento facial), donde se identifican los riesgos y las medidas para reducirlos.
- Por que tengo que hacer esto: porque su empresa esta tratando datos en una categoria que la ley y las politicas de la ACE consideran de mayor riesgo, y necesita demostrar que penso en los riesgos antes de operar el tratamiento, no solo despues de un problema.
- Fundamento: OBL-DOC-03, Art. 4 (Medidas Organizativas, lit. e) de las Politicas de Actuacion de la ACE N. 001-0309025-DPDP.
- Cuando necesito ayuda juridica: cuando la conclusion de la EIPD indica "Debe suspenderse" o "Pendiente de asesoria especializada", o cuando el tratamiento involucra una transferencia internacional cuyo pais de destino no tiene calificacion de nivel de proteccion adecuado.

**2. Que es el nivel de riesgo (el resultado del cuestionario)**
- Que es: una etiqueta (Bajo, Medio, Alto o Critico) que el sistema calcula automaticamente a partir de sus respuestas, combinando que tan probable es que algo salga mal (Probabilidad) con que tan grave seria si pasara (Impacto).
- Por que tengo que hacer esto: le ayuda a priorizar donde poner atencion primero: un tratamiento Critico necesita mitigacion antes de un tratamiento Bajo.
- Fundamento: metodologia propia del producto (no existe formula oficial de la ACE); apoya el cumplimiento de OBL-DOC-03 y OBL-SEG-02.
- Cuando necesito ayuda juridica: el nivel de riesgo nunca es, por si solo, una conclusion legal; siempre que el resultado sea Alto o Critico, o que tenga dudas sobre si el tratamiento debe continuar, consulte a la persona con el rol Delegado o a asesoria legal antes de decidir.

**3. Que es el riesgo residual**
- Que es: el nivel de riesgo que queda despues de aplicar las medidas de mitigacion que registro (por ejemplo, despues de instalar un control de acceso adicional o de colocar un aviso visible de videovigilancia).
- Por que tengo que hacer esto: demuestra que las medidas que tomo realmente sirvieron para bajar el riesgo, no solo que existen en el papel.
- Fundamento: OBL-DOC-03; el registro de las mitigaciones tambien alimenta el catalogo de controles de MOD-015 (OBL-SEG-02, Art. 4 Medidas Organizativas).
- Cuando necesito ayuda juridica: si el riesgo residual sigue siendo Alto o Critico despues de aplicar todas las mitigaciones razonables, consulte con el Delegado o con asesoria legal si el tratamiento debe continuar, ajustarse mas o suspenderse.

**4. Por que el sistema no decide si mi tratamiento es legal**
- Que es: el sistema calcula un numero de apoyo interno, pero la decision final sobre si el tratamiento puede continuar la toma siempre una persona de su organizacion.
- Por que tengo que hacer esto: porque la ley exige que su empresa pueda demostrar que penso y decidio, no que un programa decidio por ella; ademas, evaluar si una base legal o un pais extranjero cumplen la ley requiere criterio que un cuestionario cerrado no puede capturar completamente.
- Fundamento: principio de responsabilidad demostrada, Art. 5 lit. i LPDP (OBL-PRIN-03); limite explicito de diseno del producto (`04_objetivo_exacto_del_producto.md`, seccion 1.2, y `22_anti_features.md`, items 3 y 6).
- Cuando necesito ayuda juridica: siempre que la conclusion no sea claramente "Puede continuar" con riesgo Bajo, o cuando el tratamiento incluya transferencia internacional, datos de menores o biometria sin alternativa no biometrica ofrecida al titular.

**5. Que es un tratamiento de alto riesgo (los disparadores que abren una EIPD)**
- Que es: una actividad de tratamiento que entra en una o mas categorias que la ley y el prompt de analisis funcional del producto reconocen como de mayor riesgo: datos biometricos, datos de salud, datos de menores de edad, monitoreo o videovigilancia, perfilado, gran escala, transferencias internacionales o uso de una tecnologia nueva para su empresa.
- Por que tengo que hacer esto: si no identifica correctamente estos factores desde el diagnostico o el RAT, el sistema no puede abrirle automaticamente la evaluacion que la ley espera para ese tipo de tratamiento.
- Fundamento: OBL-SENS-06 (Art. 4 lit. g LPDP, biometria), OBL-SENS-04 (Art. 39 LPDP, salud), OBL-SENS-08 (Arts. 4, 7, 12, 16 LPDP, videovigilancia/reconocimiento facial), area 20 del prompt de analisis funcional (`00_prompt_analisis_funcional.md`).
- Cuando necesito ayuda juridica: cuando no este seguro de si su caso concreto encaja en una de estas categorias (por ejemplo, si una camara sin reconocimiento facial cuenta como "biometria" o no), marque el factor que crea mas cercano y consulte con el Delegado o con asesoria legal para confirmar la calificacion.

---

## Notas finales (desacuerdos o senalamientos sobre las fuentes de diseno)

Esta ficha no encontro contradicciones con el mapa definitivo de modulos, la validacion de la idea ni la matriz de obligaciones. Dos precisiones que conviene dejar explicitas para quien integre esta ficha con las demas:

1. **Precision de alcance, no desacuerdo.** `mapa_modulos.json` clasifica el modulo como "Notas reforma 659: No aplica directamente". Esta ficha coincide con esa clasificacion en cuanto al contenido tecnico (cuestionario, scoring, mitigaciones), pero anadio en la seccion A y en la seccion G (regla 6) el efecto indirecto que si existe: el cambio de a quien se asigna por defecto la aprobacion final (Delegado en estado ACTUAL, Responsable Interno en estado FUTURO). Se documenta como precision, no como correccion, porque no contradice la nota del mapa: el fundamento juridico de la EIPD en si (Politicas ACE) efectivamente no cambia con la reforma.
2. **Plazo de retencion documental de la EIPD (seccion J).** No se localizo en la LPDP ni en las Politicas de Actuacion ACE un plazo de retencion especifico para el expediente de una EIPD (a diferencia del aviso de privacidad, que si tiene un plazo expreso de 10 anos en el Art. 31 de los Lineamientos DPO, OBL-RET-04/OBL-AVISO-04 segun el documento). Esta ficha propone, como criterio propio del producto y de forma explicitamente marcada como tal, conservar la EIPD mientras el tratamiento este activo mas 5 anos adicionales desde su archivo, por analogia con el plazo de prescripcion de infracciones (Art. 47 Normativa PAS). Se senala aqui para que quien defina las reglas finales de MOD-016 (Retencion y Eliminacion) decida si adopta este criterio o fija uno distinto, y para que no se presente ante el cliente como una obligacion legal expresa cuando en realidad es una recomendacion de diseno.
