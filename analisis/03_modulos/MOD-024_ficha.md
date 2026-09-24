# MODULO: Centro Regulatorio

Codigo corto del modulo: MOD-024
Clasificacion global del modulo: MUST HAVE (el nucleo del modulo; ver seccion Q para el detalle de que parte es MUST, SHOULD o COULD dentro del propio modulo)
Obligaciones que cubre: propietario de OBL-AUD-02, OBL-PLAZO-05, OBL-SANC-01, OBL-SANC-02, OBL-SANC-03, OBL-SANC-04, OBL-SANC-05, OBL-SANC-06, OBL-SANC-07, OBL-SANC-08, OBL-SANC-09 (11 obligaciones, `matriz_obligaciones.json`). Colabora, sin ser propietario, en OBL-ARCO-14 (propietario MOD-011 ARCO-POL), OBL-DPO-01 (propietario MOD-002 Delegado / Responsable Interno de Datos), OBL-INC-05 (propietario MOD-013 Incidentes de Seguridad), OBL-SEG-01 y OBL-SEG-06 (propietario MOD-015 Controles de Seguridad) y OBL-TRANSF-05 (propietario MOD-010 Transferencias Internacionales).

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (sin codigo, sin SQL, sin APIs, sin stack, sin infraestructura).

Fuentes usadas para esta ficha: `00_contexto_para_agentes.md`; `00_prompt_analisis_funcional.md`; `00_plantilla_ficha_modulo.md`; `02_validacion/mapa_modulos.json` (entrada MOD-024); `02_validacion/06_mapa_definitivo_de_modulos.md` (secciones 2, 3, 4, 5, 6, 6.1 y 7); `01_legal/matriz_obligaciones.json` (registro completo de las 11 obligaciones propietarias y las 6 colaboradoras); `01_legal/03_hallazgos_regulatorios.md` (secciones 3 y 9); `01_legal/sweep_sanciones_procedimiento.md` (completo); `01_legal/sweep_reforma_659.md`; `01_legal/fuentes/ace_decreto_144.txt` (Arts. 50, 53, 55 a 59); `01_legal/fuentes/normativa_sancionadora_OCR.txt` y sus imagenes `01_legal/fuentes/ocr/normativa_sancionadora/page-02.png` a `page-09.png`; `02_validacion/02_validacion_de_la_idea.md` (secciones 2.3 a 2.7, en particular las decisiones 16, 19, 25 y 32); `02_validacion/04_objetivo_exacto_del_producto.md`; `02_validacion/05_tipos_de_usuario.md` (secciones 5.2, 5.3 y 5.4); `02_validacion/22_anti_features.md` (anti-features 4, 5, 6, 7, 12, 13, 14 y 19); `02_validacion/lente_faltantes.md` (hallazgos 6, 13, 15, 16, 17, 18 y 31); `02_validacion/lente_inconsistencias.md` (inconsistencias 7, 18 y 21); `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` (secciones 8.2, 8.12, 40, 41 y 42, tratadas como hipotesis, no como decisiones); y las fichas ya escritas `03_modulos/MOD-001_ficha.md`, `MOD-002_ficha.md`, `MOD-004_ficha.md`, `MOD-005_ficha.md`, `MOD-006_ficha.md`, `MOD-007_ficha.md`, `MOD-008_ficha.md`, `MOD-009_ficha.md`, `MOD-010_ficha.md`, `MOD-011_ficha.md`, `MOD-013_ficha.md`, `MOD-014_ficha.md`, `MOD-015_ficha.md`, `MOD-016_ficha.md`, `MOD-018_ficha.md` y `MOD-021_ficha.md` (usadas como modelo de estilo y profundidad MOD-002 y MOD-011, y como fuente del contrato de expectativas detallado en la Nota final).

Nota de lectura sobre la reforma 659: en toda esta ficha, "el Decreto Legislativo 659" se cita segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado (decision 2.7.32 de `02_validacion_de_la_idea.md`; incertidumbre 13 de `01_legal/03_hallazgos_regulatorios.md`, seccion 9). Mientras no se confirme su publicacion en el Diario Oficial, el regimen vigente es el del texto actual del Decreto 144 (delegado obligatorio en el sector privado, Arts. 15 y 17).

---

## A. Proposito

- **Por que existe.** Ninguna empresa cliente sin equipo juridico dedicado puede seguir por su cuenta que version de la ley esta vigente, si un cambio normativo la afecta, que hacer si la Agencia de Ciberseguridad del Estado (ACE) le abre un procedimiento sancionador, o como comunicarle a la ACE un tramite que la ley exige poner en su conocimiento. El documento maestro trataba esto como arquitectura tecnica (secciones 40 "Motor regulatorio" y 41 "Actualizacion normativa"); la validacion de la idea identifico dos vacios completos de la matriz de obligaciones sin ningun lugar funcional (area SANC, 9 obligaciones, y el tramite del Art. 45 sin campo ni evidencia asociada) y decidio convertir ambas piezas, mas el motor de doble estado, en un modulo funcional propio (decisiones 2.7.16, 2.7.19 y 2.7.25 de `02_validacion_de_la_idea.md`; hallazgos 6, 13, 15 a 18 y 31 de `lente_faltantes.md`).
- **Que problema resuelve para la empresa.** Da a la empresa un unico lugar donde: (1) consultar el marco normativo aplicable sin tener que rastrear el Diario Oficial por su cuenta; (2) enterarse, con una experiencia guiada, de que cambio cuando la norma cambia y que debe revisar; (3) gestionar un procedimiento sancionador activo con sus plazos reales calculados automaticamente en vez de perder el emplazamiento en un correo suelto; y (4) dejar constancia de los tramites que la ley exige poner en conocimiento de la ACE, aunque la propia ACE aun no tenga habilitado un canal oficial para recibirlos.
- **Que obligacion u obligaciones cubre.** Propietario de OBL-AUD-02 (Art. 50 lit. j, k, l LPDP, facultad de la ACE de crear certificaciones o sellos, RECOMENDADO, sin mecanismo habilitado a la fecha), OBL-PLAZO-05 (seguimiento del estado de publicacion de la reforma 659, CONDICIONAL), y OBL-SANC-01 a OBL-SANC-09 (Arts. 53 a 59 LPDP y Arts. 1 a 49 de la Normativa para el Procedimiento Administrativo Sancionador de la ACE, en adelante Normativa PAS; OBLIGATORIO el catalogo de infracciones en si, OBL-SANC-01; CONDICIONAL el resto, porque solo se activan si la ACE abre un caso o impone una sancion; RECOMENDADO OBL-SANC-07, retencion de evidencia por prescripcion). Colabora, sin ser propietario: OBL-ARCO-14 (reclamo del titular ante la Direccion de Proteccion de Datos, propietario MOD-011: este modulo muestra el estado del reclamo dentro del expediente sancionador cuando existe uno relacionado), OBL-DPO-01 (obligatoriedad de nombrar delegado, propietario MOD-002: este modulo es donde se consulta si esa obligacion sigue vigente segun el regimen activo de la bandera), OBL-INC-05 (reporte de incidentes de ciberseguridad para operadores de infraestructura critica, propietario MOD-013: se muestra como parte del marco normativo consultable), OBL-SEG-01 y OBL-SEG-06 (caracter imperativo de las Politicas de Actuacion ACE e infraccion grave por no implementarlas, propietario MOD-015: se referencian desde el catalogo de infracciones del Procedimiento Sancionador), y OBL-TRANSF-05 (puesta en conocimiento de la ACE del flujo transfronterizo, propietario MOD-010: el contenido nace en Transferencias, pero el registro del tramite saliente y su estado viven en el submodulo Tramites ante la ACE de este modulo, exactamente como ya lo describe `03_modulos/MOD-010_ficha.md`, secciones D, G y K).
- **Que valor aporta.**
  - Operativo: es el unico lugar donde se decide que version de una regla esta activa (regla de conexion 4 de `06_mapa_definitivo_de_modulos.md`, seccion 4); ningun otro modulo evalua por si mismo si la reforma 659 esta vigente, evitando que dos modulos distintos muestren estados normativos contradictorios el mismo dia.
  - Probatorio: aloja el expediente completo de cualquier procedimiento sancionador (emplazamiento, contestacion, pruebas, resolucion, recursos, pago) y el registro de cada tramite saliente ante la ACE, como evidencia verificable de que la empresa reaccion a tiempo, alineado con el principio de responsabilidad demostrada (OBL-PRIN-03, Art. 5 lit. i, propietario MOD-019).
  - Reduccion de riesgo: nunca declara vigente un regimen que aun no fue publicado oficialmente (anti-feature 14) y separa visualmente, en toda su interfaz, el contenido informativo (marco normativo, catalogo de infracciones y multas) del flujo operativo con dinero y plazos reales (expediente sancionador activo), para que nadie confunda un catalogo de consulta con un caso propio en curso.
- **Que NO hace este modulo (limites explicitos).**
  - No decide por si mismo que version de la reforma 659 aplica por la sola fecha de aprobacion legislativa (17-sep-2026); la bandera unica solo cambia cuando el equipo del producto confirma la publicacion oficial en el Diario Oficial y transcurren los 8 dias de vacatio legis (anti-feature 14; decision 2.7.16).
  - No presenta tramites ni comunicaciones ante la ACE en nombre de la empresa sin que esta lo autorice y ejecute; prepara el contenido y deja evidencia del intento de cumplimiento, mientras la ACE no habilite un canal oficial para varios de estos tramites (anti-feature 13).
  - No predice si la ACE abrira un procedimiento sancionador, no califica por si mismo si un hecho concreto encaja en el catalogo de infracciones del Art. 56, ni califica la gravedad de una infraccion o gradua una multa (facultad exclusiva de la ACE, Art. 43 Normativa PAS).
  - No calcula la probabilidad ni el monto exacto de una multa para un caso concreto; la informacion de multas (Art. 57 LPDP) es siempre orientativa, expresada en salarios minimos con su equivalente en dolares segun el decreto de salario minimo vigente, y remite a asesoria juridica antes de cualquier decision.
  - No emite la certificacion oficial de Delegado ni ningun sello o certificacion de proteccion de datos; solo recuerda el tramite y enlaza al canal oficial de la ACE cuando exista (anti-feature 12; OBL-AUD-02 es hoy informativa porque la ACE no ha habilitado ese mecanismo).
  - No decide la estrategia de defensa de la empresa (allanarse, pedir inspeccion o peritaje, interponer un recurso); calcula plazos, organiza el expediente y deja constancia de la decision que tome la organizacion (ver seccion H).
  - No declara "porcentaje de cumplimiento legal"; el estado del marco normativo y del expediente sancionador se expresa siempre como estado del programa, evidencia disponible y plazos cumplidos o vencidos (anti-feature 5).
  - No permite que ningun usuario de la organizacion cliente edite o borre el contenido normativo ni la bandera de doble estado; ese contenido lo gobierna exclusivamente personal interno del proveedor del software (ver seccion B), nunca un rol de la empresa cliente.

---

## B. Usuarios

Roles estandar de la organizacion cliente que usan este modulo (`02_validacion/05_tipos_de_usuario.md`, seccion 5.3):

- **Administrador de la organizacion.** Ve el estado normativo vigente desde el dashboard, recibe la notificacion cuando cambia la bandera de la reforma 659, y es quien registra o revisa el expediente de un procedimiento sancionador cuando la empresa recibe un emplazamiento (junto con Responsable Legal); confirma que tomo conocimiento de cada actualizacion normativa relevante.
- **Delegado de Proteccion de Datos (o Responsable Interno, si el estado FUTURO esta activo).** Consulta el marco normativo para fundamentar sus decisiones, recibe las tareas de revision que dispara un cambio de bandera, y participa como responsable tecnico en la preparacion de la respuesta a un procedimiento sancionador o de un tramite ante la ACE.
- **Responsable ARCO-POL / Responsable del tramite.** Consulta el estado del reclamo del titular ante la Direccion de Proteccion de Datos (OBL-ARCO-14) cuando existe uno vinculado a un caso ARCO-POL propio, y ve si una denuncia del titular por incumplimiento de plazos (OBL-SANC-09) esta relacionada con un expediente que gestiona.
- **Responsable Legal / Compliance.** Usuario principal del submodulo Procedimiento Sancionador y Tramites ante la ACE: redacta o revisa la contestacion del emplazamiento, decide la estrategia de defensa con apoyo externo, aprueba el contenido de cada tramite saliente antes de su envio, y es quien confirma la validacion juridica del texto oficial de una reforma antes de recomendar el cambio de bandera al equipo del producto (el modulo nunca activa la bandera por si solo, ver seccion H).
- **Responsable de Seguridad / IT.** Consulta el marco normativo relacionado con medidas de seguridad (OBL-SEG-01, OBL-SEG-06) y con el reporte de incidentes de ciberseguridad para operadores de infraestructura critica (OBL-INC-05), y aporta evidencia tecnica cuando un procedimiento sancionador se origina en un incidente de seguridad.
- **Responsable de area (RRHH, Marketing, Operaciones, etc.).** Solo lectura del marco normativo y de las tareas de revision que le asigne un cambio normativo a traves de MOD-021; no tiene acceso de edicion a este modulo.
- **Aprobador.** Aprueba el envio de cada tramite ante la ACE y la version final de la contestacion de un emplazamiento antes de enviarla, y aprueba la confirmacion de "toma de conocimiento" cuando un cambio normativo lo exige con doble control.
- **Auditor (interno).** Solo lectura y exportacion: consulta el historial de versiones normativas, el registro de tramites ante la ACE y el expediente completo de cualquier procedimiento sancionador cerrado, para el programa de auditoria de cumplimiento (MOD-018).
- **Auditor externo (invitado).** Acceso temporal de solo lectura a un expediente sancionador especifico o al marco normativo, para una auditoria puntual, sin capacidad de comentar ni modificar.
- **Usuario de consulta / Colaborador.** Ve el marco normativo consultable y el catalogo de infracciones y multas como material informativo, sin acceso a ningun expediente sancionador ni a la bandera de doble estado.
- **Titular (formulario externo).** No entra a este modulo. Puede consultar, a traves de su solicitud ARCO-POL en MOD-011, el estado de un reclamo o denuncia que haya presentado ante la ACE, pero nunca el expediente sancionador de la empresa.
- **Asesor externo invitado.** Puede ser invitado a un procedimiento sancionador puntual como abogado externo, con acceso acotado a ese expediente especifico y sin licencia permanente.

**Rol interno del proveedor, fuera del catalogo de roles de la organizacion cliente (gobierno del contenido normativo).** Este modulo requiere ademas un "Editor de contenido regulatorio" con revision juridica, que mantiene el catalogo de instrumentos normativos, versiona cada regla y es la unica persona (junto con la validacion juridica que aporte Responsable Legal de cada organizacion cliente, de forma consultiva y no vinculante) que puede activar el cambio de la bandera `regimen_reforma_659` de ACTUAL a FUTURO. Este rol no pertenece a los 12 roles estandar de `05_tipos_de_usuario.md` seccion 5.3 porque no es un usuario de ninguna organizacion cliente: es personal del proveedor del software, y se documenta aqui unicamente porque gobierna el contenido que todas las organizaciones consultan. Ninguna accion de este rol se ejecuta dentro de una cuenta de cliente ni aparece en la tabla de permisos de la seccion C, que solo cubre roles de la organizacion cliente.

---

## C. Permisos

| Accion | Admin. organizacion | Delegado / Resp. Interno | Resp. ARCO-POL | Resp. Legal | Resp. Seguridad/IT | Resp. de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Titular externo | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver marco normativo y catalogo de infracciones/multas (informativo) | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si | No | Si (caso asignado) |
| Ver expediente de un procedimiento sancionador propio | Si | Si | No (salvo caso vinculado) | Si | Si (si aplica) | No | Si | Si | Si (alcance temporal) | No | No | Si (caso asignado) |
| Crear expediente de procedimiento sancionador (registrar emplazamiento recibido) | Si | No | No | Si | No | No | No | No | No | No | No | No |
| Redactar/editar contestacion, pruebas y decisiones del expediente | No | Colabora | No | Si | Colabora | No | No | No | No | No | No | Colabora |
| Aprobar y enviar contestacion, recurso o tramite ante la ACE | Si (ver nota) | No | No | Si | No | No | Si | No | No | No | No | No |
| Cerrar (registrar resolucion final / archivar) | Si | No | No | Si | No | No | Si | No | No | No | No | No |
| Eliminar / archivar | No (solo archivar, nunca eliminar historial) | No | No | No | No | No | No | No | No | No | No | No |
| Exportar (paquete de evidencia del expediente) | Si | Si (propio) | No | Si | No | No | No | Si | Si (alcance temporal) | No | No | No |
| Confirmar "toma de conocimiento" de un cambio normativo | Si | Si | Si | Si | Si | Si | Si | No | No | No | No | No |
| Recomendar (no activar) el cambio de bandera ante el proveedor | No | No | No | Si | No | No | No | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | Si | No | Si | No | No | No | No | Si (caso asignado) |
| Adjuntar evidencia (acuses, comprobantes, escritos) | Si | Si | No | Si | Si (si aplica) | No | No | No | No | No | No | Si (caso asignado) |

Separacion de funciones:

- La bandera `regimen_reforma_659` y el contenido versionado del marco normativo no son editables por ningun rol de la organizacion cliente; los edita exclusivamente el Editor de contenido regulatorio del proveedor (seccion B). Ningun rol de esta tabla tiene, por tanto, columna de "editar marco normativo".
- Quien crea o edita el expediente de un procedimiento sancionador (tipicamente Administrador o Responsable Legal) no deberia ser el unico que aprueba y envia la contestacion final o un recurso; en empresa mediana o corporativo se exige un segundo firmante (Aprobador o un segundo miembro de Responsable Legal). En pyme, por debajo del umbral de 50 empleados (`05_tipos_de_usuario.md`, 5.4), el sistema permite que Administrador cree y apruebe, mostrando siempre la advertencia visible de "autorrevision".
- El rol Auditor (interno o externo) es siempre de solo lectura: nunca puede comentar, aprobar ni adjuntar evidencia, para preservar la independencia de su verificacion.
- Aprobar el envio de cualquier tramite ante la ACE (contestacion, recurso, comprobante de pago, registro ACEFiling generado desde MOD-002 o MOD-010) exige doble control: quien redacta no puede ser la unica firma; se requiere ademas Aprobador o un segundo Responsable Legal antes de marcar el tramite como enviado.
- El documento con el numero de expediente y los datos de la persona natural del presunto infractor (cuando aplica) es de acceso restringido a Administrador, Responsable Legal y Aprobador; cada lectura queda en el historial (seccion O).

---

## D. Informacion de entrada

Precarga y minimizacion de datos personales (privacy by design): el marco normativo y el catalogo de infracciones son contenido del proveedor, no datos personales de la empresa cliente. Los unicos datos personales que este modulo puede llegar a contener son los de la persona que firma un escrito de contestacion o la persona natural que la ACE identifique como presunto responsable dentro de un procedimiento sancionador; el modulo referencia esos nombres por lo estrictamente necesario para el expediente, sin duplicar el RAT ni el inventario de personas de MOD-001.

### D.1 Marco normativo consultable (RegulatoryInstrument y RegulatoryRuleVersion)

Este bloque es de solo lectura para toda la organizacion cliente; sus campos los completa el Editor de contenido regulatorio del proveedor. Se documentan igual, con las 7 columnas de la plantilla, porque son la informacion de entrada real del submodulo, solo que su origen no es un formulario de la empresa cliente.

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|
| nombre_instrumento | Texto | Obligatorio | - | No vacio | "Nombre completo de la norma o disposicion, por ejemplo 'Ley para la Proteccion de Datos Personales'." | Buena practica de trazabilidad normativa |
| tipo_instrumento | Seleccion unica | Obligatorio | LEY, NORMATIVA_ACE, LINEAMIENTO_ACE, POLITICA_DE_ACTUACION_ACE, BUENA_PRACTICA | - | "Indica si es una ley, un reglamento de la ACE, un lineamiento, una politica de actuacion obligatoria o una buena practica recomendada, para que usted sepa cuanto peso legal tiene." | Regla 4 de las reglas no negociables de este blueprint (distinguir ley, normativa ACE, lineamientos, politicas y buena practica) |
| clasificacion_exigibilidad | Seleccion unica | Obligatorio | OBLIGATORIO, RECOMENDADO, CONDICIONAL | Igual a la clasificacion de `matriz_obligaciones.json` cuando el instrumento se vincula a un OBL-ID | "Nivel de exigencia de esta disposicion." | Regla 4 de las reglas no negociables |
| numero_y_fecha_emision | Texto + fecha | Obligatorio | - | - | "Numero del decreto, acuerdo o resolucion, y fecha en que se emitio." | Trazabilidad de la fuente |
| fecha_publicacion_diario_oficial | Fecha | Obligatorio cuando aplica (vacio si aun no se publica) | - | No puede ser futura una vez completada | "Fecha en que este instrumento se publico oficialmente." | Regla del contexto: toda afirmacion juridica cita norma, articulo, fuente y fecha de consulta |
| fecha_entrada_en_vigencia | Fecha (calculada o manual) | Obligatorio cuando aplica | - | Por defecto, publicacion + 8 dias, salvo que el propio instrumento fije otro plazo | "Fecha desde la cual esta disposicion produce efectos." | Idem |
| estado_instrumento | Seleccion unica | Obligatorio | VIGENTE, FUTURO, DEROGADO, MODIFICADO | Editable solo por el Editor de contenido regulatorio | "Muestra si esta disposicion esta vigente hoy, si entrara en vigencia mas adelante, si ya fue derogada o si fue modificada por otra norma posterior." | Requisito explicito de la tarea: marco normativo con estos cuatro estados |
| estado_verificacion | Seleccion unica | Obligatorio | VERIFICADO_CONTRA_FUENTE_PRIMARIA, SEGUN_FUENTES_SECUNDARIAS, OCR_PENDIENTE_DE_VERIFICAR | - | "Indica que tan confiable es el texto que estamos mostrando: si ya se confirmo contra el documento oficial, si todavia depende de prensa u otras fuentes secundarias, o si viene de un escaneo que puede tener errores de reconocimiento." | Regla del contexto compartido, seccion 4 |
| fuente_oficial | Texto (URL o ruta de archivo) | Obligatorio | - | - | "De donde sacamos este texto." | Regla del contexto compartido |
| fecha_ultima_consulta | Fecha | Obligatorio | - | - | "Ultima vez que se confirmo que esta informacion sigue siendo correcta." | Regla del contexto compartido |
| obligaciones_relacionadas | Seleccion multiple (referencia) | Opcional | Lista de OBL-ID de `matriz_obligaciones.json` | - | "A que obligaciones de la matriz afecta esta disposicion." | Trazabilidad OBL-ID |
| version_regla (dentro de RegulatoryRuleVersion) | Numero + fecha_vigencia_desde + fecha_vigencia_hasta | Obligatorio si el instrumento tiene reglas operativas (plazos, formularios, campos) | - | La version anterior siempre conserva su fecha_vigencia_hasta al crearse una nueva version; nunca se sobrescribe | "Cada vez que una regla cambia (por ejemplo, un plazo), guardamos la version anterior con las fechas en que estuvo vigente, para poder reconstruir que regla aplicaba a un caso en una fecha pasada." | Hipotesis de `PROMPT_BASE...md` seccion 41 ("Actualizacion normativa"), adoptada como diseno funcional |

### D.2 Bandera de doble estado (ReformaActivationFlag)

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|
| regimen_reforma_659 | Seleccion unica (unica instancia global, no editable por la organizacion cliente) | Obligatorio | ACTUAL, FUTURO | Solo el Editor de contenido regulatorio del proveedor puede cambiar este valor; nunca se activa FUTURO por la sola fecha de aprobacion legislativa | "Muestra si hoy aplica la ley vigente (Delegado obligatorio) o si ya aplica la reforma aprobada por la Asamblea Legislativa (Delegado ya no obligatorio)." | OBL-PLAZO-05; anti-feature 14 |
| fecha_aprobacion_legislativa | Fecha | Informativo, ya completo (17-sep-2026) | - | No editable | "Fecha en que la Asamblea Legislativa aprobo la reforma. Esto no significa que ya este vigente." | Seccion 3 de `03_hallazgos_regulatorios.md` |
| estado_interno_verificacion_659 (campo tecnico de workflow, distinto de `regimen_reforma_659`) | Seleccion unica | Autogenerado | SIN_CAMBIOS_DETECTADOS, EN_VERIFICACION, LISTO_PARA_ACTIVAR | Pasa a EN_VERIFICACION automaticamente al completarse `fecha_aprobacion_legislativa`; mientras este campo no llegue a LISTO_PARA_ACTIVAR, `regimen_reforma_659` permanece en ACTUAL sin excepcion | No visible como campo de captura para la organizacion cliente; en el panel del Editor de contenido regulatorio: "Paso interno de revision en el que esta el equipo del proveedor antes de poder activar el nuevo regimen." | Aclaracion de diseno: la bandera `regimen_reforma_659` conserva solo los dos valores que describe `06_mapa_definitivo_de_modulos.md` seccion 5 punto 2 (ACTUAL y FUTURO); EN_VERIFICACION del diagrama F.1 es un estado de este campo tecnico de seguimiento interno, no un tercer valor de la bandera misma |
| fecha_publicacion_diario_oficial_reforma | Fecha | Condicional (vacio mientras no se confirme) | - | No editable por la organizacion cliente | "Fecha en que la reforma se publico oficialmente. Mientras este campo este vacio, la reforma no esta vigente." | Regla explicita de la tarea (condiciones de activacion) |
| validacion_juridica_texto_oficial | Booleano + referencia a informe | Obligatorio antes de activar FUTURO | Si / No | Solo se marca Si cuando el Editor de contenido regulatorio confirma que el texto oficial publicado coincide con lo descrito por fuentes secundarias | "Confirma que alguien reviso el texto oficial completo del decreto antes de activar el nuevo estado, no solo la nota de prensa." | Regla explicita de la tarea; incertidumbre 4 y 13 de `03_hallazgos_regulatorios.md` seccion 9 |
| fecha_cumplimiento_vacatio_legis | Fecha (calculada) | Obligatorio antes de activar FUTURO | fecha_publicacion + 8 dias | No editable manualmente | "Fecha en que la reforma empieza a producir efectos, ocho dias despues de su publicacion oficial." | Regla explicita de la tarea; Art. 64 LPDP como precedente de calculo de vacatio legis |
| fecha_activacion_bandera | Fecha + hora | Se completa al activar | - | Posterior o igual a fecha_cumplimiento_vacatio_legis | "Fecha y hora exactas en que el sistema empezo a mostrar el nuevo regimen." | Trazabilidad, decision 2.7.16 |
| motivo_reversion (si aplica) | Texto largo | Condicional | DECRETO_NO_PUBLICADO, DECRETO_IMPUGNADO, TEXTO_DIFIERE_DE_LO_REPORTADO, OTRO (texto libre) | Obligatorio si se revierte de FUTURO a ACTUAL | "Si la reforma no llega a aplicarse como se esperaba, explique por que se revierte el estado." | Requisito explicito de la tarea (reversion si el decreto no se publica, es impugnado o su texto difiere) |
| organizaciones_notificadas (registro tecnico) | Lista (autogenerada) | Autogenerado | - | - | No visible como campo de captura; es el registro de que cada organizacion cliente recibio la notificacion del cambio | Requisito explicito de la tarea (comunicacion a cada organizacion) |

### D.3 Procedimiento Sancionador (SanctionProcedure)

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|
| origen_del_caso | Seleccion unica | Obligatorio | EMPLAZAMIENTO_RECIBIDO, DILIGENCIA_PRELIMINAR_NOTIFICADA, DENUNCIA_DE_TITULAR_CONOCIDA, OTRO | - | "Como se entero su empresa de este procedimiento." | Normativa PAS Arts. 8 y 15 |
| fecha_notificacion_recibida | Fecha | Obligatorio | - | No puede ser futura | "Fecha en que su empresa recibio la notificacion de la ACE. A partir de aqui el sistema calcula todos los plazos." | Normativa PAS Art. 19 |
| via_procedimiento | Seleccion unica | Obligatorio (por defecto SIMPLIFICADA) | SIMPLIFICADA, ORDINARIA | Cambia a ORDINARIA solo si la ACE lo notifica por resolucion motivada (Art. 31) | "La mayoria de los casos siguen la via simplificada; la ACE puede pasar el caso a la via ordinaria si es mas complejo." | Normativa PAS Art. 4 |
| infracciones_imputadas | Seleccion multiple (referencia al catalogo Art. 56) | Obligatorio | Catalogo de infracciones leves (9), graves (7) y muy graves (10) del Art. 56 | - | "Que infraccion o infracciones le atribuye la ACE, segun la resolucion de inicio." | OBL-SANC-01, Art. 56 |
| documento_resolucion_inicio | Archivo (PDF) | Obligatorio | - | Formato PDF | "Adjunte la resolucion de inicio y el emplazamiento que recibio." | Normativa PAS Arts. 17 y 18 |
| escrito_de_contestacion | Texto largo + archivo | Obligatorio antes de vencer el plazo de 5 dias habiles | - | - | "Redacte o adjunte su respuesta, alegatos y pruebas dentro de los 5 dias habiles desde el dia siguiente a la notificacion." | OBL-SANC-05, Art. 21 Normativa PAS |
| decision_allanamiento | Booleano | Opcional, en cualquier etapa | Si / No | Si es Si, se omiten las etapas no agotadas | "Puede aceptar los hechos en cualquier momento del procedimiento; esto puede reducir la multa hasta en una cuarta parte." | Normativa PAS Art. 23; LPA Art. 156 |
| solicitud_inspeccion_peritaje | Booleano | Opcional (solo al contestar, en via simplificada) | Si / No | Debe registrarse en el mismo momento de la contestacion si la via es SIMPLIFICADA | "En la via simplificada, debe pedir inspeccion o peritaje justo al momento de contestar, no despues." | Normativa PAS Art. 25 inciso final |
| pruebas_propuestas | Archivo (multiple) + texto | Opcional | - | - | "Adjunte los documentos, informes de auditoria u otra prueba que respalde su version de los hechos." | Normativa PAS Art. 24 |
| medidas_provisionales_recibidas | Texto largo + archivo | Condicional | - | - | "Si la ACE le ordeno una medida provisional antes o durante el procedimiento, registrela aqui." | Normativa PAS Arts. 35 y 36 |
| resultado_resolucion_final | Seleccion unica | Se completa al recibir la resolucion | SIN_RESOLVER, SIN_SANCION_ARCHIVADO, SANCION_LEVE, SANCION_GRAVE, SANCION_MUY_GRAVE | - | "Resultado final del procedimiento, cuando la ACE lo resuelva." | Normativa PAS Art. 32 |
| monto_multa_impuesta | Numero (salarios minimos) + monto en USD (calculado) | Obligatorio si hay sancion | Rango segun categoria (1-10, 11-25, 26-40 SM) | El monto en USD se calcula con el salario minimo vigente en la fecha de la resolucion, mostrando tambien el vigente en la fecha del hecho si difieren | "Monto de la multa que le impuso la ACE, en salarios minimos y su equivalente en dolares. Este campo se llena con el resultado real de la ACE, nunca es una prediccion del sistema." | OBL-SANC-02, Art. 57 |
| medidas_adicionales_ordenadas | Texto largo, repetible | Condicional | - | - | "Medidas que la ACE le ordeno para corregir la situacion, ademas de la multa." | OBL-SANC-03, Art. 58 |
| comprobante_pago_multa | Archivo | Obligatorio si hay multa firme | - | Fecha del comprobante dentro de los 15 dias habiles desde la notificacion de la resolucion | "Adjunte el comprobante de pago en la Colecturia Central o en las oficinas regionales de la Direccion General de Tesoreria, dentro de los 15 dias habiles." | OBL-SANC-06, Art. 44 Normativa PAS |
| recurso_interpuesto | Seleccion unica | Condicional (solo via ORDINARIA) | NINGUNO, RECONSIDERACION, APELACION, REVISION_EXTRAORDINARIA | Solo disponible si via_procedimiento = ORDINARIA (en via simplificada no hay recurso administrativo, Art. 32; el numero exacto del inciso no se cita porque el texto OCR disponible no numera los incisos de ese articulo de forma explicita y no se ha confirmado contra el texto oficial publicado en el Diario Oficial -- requiere validacion de asesoria juridica antes de citarse con esa precision) | "Si el procedimiento fue por via ordinaria, puede impugnar la resolucion dentro de los plazos que le indique el sistema." | Normativa PAS Art. 33 |
| fecha_firmeza_resolucion | Fecha (calculada) | Se completa al agotarse recursos o vencer plazos | - | - | "Fecha en que la resolucion queda firme y comienza a correr la prescripcion de la sancion." | LPA Art. 149 |
| fecha_limite_prescripcion | Fecha (calculada) | Autogenerado | fecha del hecho o cese de la conducta + 5 anos | Se interrumpe si se inicia un nuevo procedimiento con conocimiento de la empresa | "Fecha limite en que esta infraccion o sancion prescribe, segun la ley." | OBL-SANC-07, Art. 47 Normativa PAS |
| requerimiento_informacion_ace (registro repetible) | Grupo de campos: fecha, contenido solicitado, plazo otorgado, respuesta enviada | Condicional | - | - | "Registre cada vez que la ACE le pida documentos, antecedentes o informes dentro de este procedimiento." | Art. 50 lit. t) LPDP |

### D.4 Tramites ante la ACE (ACEFiling)

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|
| tipo_tramite | Seleccion unica | Obligatorio | COMUNICACION_NOMBRAMIENTO_DELEGADO, ACTUALIZACION_DATOS_DELEGADO, PUESTA_EN_CONOCIMIENTO_TRANSFERENCIA, SOLICITUD_OPINION_PREVIA_TRANSFERENCIA, SOLICITUD_CERTIFICACION_O_SELLO, OTRO | - | "Que tipo de tramite es este." | Decision 2.7.19 ("Anadir el concepto Tramites ante la ACE") |
| modulo_origen | Referencia (MOD-002, MOD-010, "Manual") | Obligatorio | - | Si el origen no es "Manual", el registro de origen debe existir | "De donde nacio este tramite: por ejemplo, del nombramiento de su Delegado o de una transferencia internacional que registro." | Coherente con `MOD-002_ficha.md` seccion E ("evento saliente tramite de nombramiento") y `MOD-010_ficha.md` secciones D, G y K |
| contenido_del_tramite | Referencia a otra entidad + campos precargados | Obligatorio | - | Precargado por referencia desde el modulo de origen, sin duplicar el dato | "Datos que se enviaran a la ACE, tomados directamente del registro donde los completo por primera vez." | Regla de "direccion unica": el modulo que crea el dato original sigue siendo su unico propietario |
| estado_tramite | Seleccion unica | Obligatorio | BORRADOR, PENDIENTE_DE_ENVIO, ENVIADO, CONFIRMADO, RECHAZADO, NO_APLICA | - | "En que etapa esta este tramite frente a la ACE." | Estos seis estados son el modelo completo de ACEFiling, propiedad de este modulo. `MOD-010_ficha.md` seccion D hereda y muestra, en modo de solo lectura dentro de su propio formulario, una simplificacion de lectura de cuatro de estos seis ("Borrador / Pendiente de envio / Enviado -sin canal oficial confirmado- / No aplica"), porque para el usuario de Transferencias solo importa distinguir esos cuatro momentos; CONFIRMADO y RECHAZADO existen igual para ese registro dentro de este modulo, solo que MOD-010 no los distingue en su propia pantalla. No se modifica `MOD-010_ficha.md` en esta ficha; se deja como recomendacion para una proxima revision de ese modulo que, si el usuario de Transferencias necesita distinguir CONFIRMADO de RECHAZADO sin entrar a este modulo, incorpore esos dos estados a su propia vista de solo lectura |
| fecha_generado | Fecha (autogenerada) | Obligatorio | - | - | "Fecha en que el sistema creo este registro." | Trazabilidad |
| canal_de_envio | Texto | Obligatorio antes de marcar ENVIADO | Correo institucional, formulario web de contacto de la ACE, plataforma de la ACE (cuando exista), presencial | "Por donde se envio o se intento enviar este tramite. A la fecha de este analisis, la ACE no ha habilitado un canal oficial dedicado para varios de estos tramites; use el canal disponible y dejelo registrado." | Anti-feature 13; incertidumbre I-11 de `sweep_sanciones_procedimiento.md` |
| fecha_envio | Fecha | Se completa al marcar ENVIADO | - | No anterior a fecha_generado | "Fecha en que efectivamente se envio el tramite." | OBL-DPO-01 (via MOD-002), OBL-TRANSF-05 |
| documento_adjunto | Archivo (PDF) | Obligatorio antes de marcar ENVIADO | - | - | "Documento final que se envio a la ACE." | Trazabilidad |
| acuse_o_respuesta_ace | Archivo + fecha | Opcional (depende de si la ACE responde) | - | - | "Si la ACE le confirma la recepcion o responde, adjunte esa constancia aqui." | Evidencia J3 de `MOD-002_ficha.md` |

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Marco normativo consultable | Lista de instrumentos con su estado (VIGENTE/FUTURO/DEROGADO/MODIFICADO), fuente y fecha de consulta | Vista en pantalla, exportable | Continuo (actualizado por el Editor de contenido regulatorio) | Todos los roles internos de la organizacion |
| Alerta de actualizacion normativa | Que cambio, a que obligaciones/modulos/documentos/tareas afecta, que debe revisar la empresa | Notificacion + pagina de detalle | Cada vez que el Editor de contenido regulatorio publica una nueva version de una regla | Administrador, Delegado/Responsable Interno, Responsable Legal |
| Tareas de revision en MOD-021 | Titulo, fundamento, modulo afectado, responsable sugerido, fecha limite | Tarea | Al publicarse una actualizacion normativa o al cambiar la bandera de reforma 659 | Persona asignada segun la regla (ver seccion G) |
| Evento saliente "cambio de bandera" | Valor nuevo de `regimen_reforma_659`, fecha de activacion, motivo | Evento hacia MOD-002, MOD-007, MOD-008, MOD-011, MOD-015, MOD-017 | Al activarse el cambio de regimen | Esos seis modulos, mas MOD-021 (tareas) y MOD-022 (notificaciones) |
| Catalogo de infracciones y multas (informativo) | Las 26 infracciones del Art. 56, rango de multa por categoria en salarios minimos y su equivalente orientativo en USD | Vista en pantalla, PDF exportable | Continuo | Todos los roles internos de la organizacion |
| Expediente de procedimiento sancionador | Todos los campos de la seccion D.3, con su historial de estados | Registro en pantalla, exportable | Al registrar el primer emplazamiento o notificacion | Administrador, Responsable Legal, Aprobador, Auditor |
| Contadores de plazo en MOD-023 | Dias habiles restantes para contestacion, alegatos, remision, resolucion, pago y prescripcion | Indicador numerico | Continuo, recalculado cada dia habil | Responsable Legal, Administrador, Aprobador |
| Registro de tramites ante la ACE (ACEFiling) | Todos los campos de la seccion D.4, con su historial de estados | Registro en pantalla, exportable | Cada vez que este modulo o un modulo de origen (MOD-002, MOD-010) genera un tramite | Administrador, Responsable Legal, Delegado/Responsable Interno, modulo de origen |
| Evento de auditoria | Cada creacion, edicion, aprobacion, adjunto, exportacion o cambio de bandera | Registro tecnico inmutable | En cada accion | AuditLog transversal, Auditor |
| Indicadores de dashboard | Ver seccion M | Semaforo, numero, badge | Continuo | Gerencia, Responsable, Legal, Auditor |
| Paquete de evidencia del expediente sancionador o de tramites ACE | Documentos, comunicaciones, comprobantes, con manifiesto y hash de integridad | ZIP exportable | Bajo demanda, o automaticamente al cerrar un expediente | MOD-019 (Centro de Evidencias), auditoria interna o externa, requerimiento de la ACE |

---

## F. Workflow

Este modulo gestiona tres ciclos de vida independientes: (F.1) la bandera de doble estado de la reforma 659, que es una unica instancia global consultada por todas las organizaciones; (F.2) el registro de tramites ante la ACE (ACEFiling), que puede originarse en este mismo modulo o llegar como evento desde MOD-002 o MOD-010; y (F.3) el expediente de un procedimiento sancionador, que es propio de cada organizacion cliente. Los tres comparten el mismo principio: nada se borra, todo se versiona o se archiva con motivo (seccion 5, punto 6 de `06_mapa_definitivo_de_modulos.md`).

### F.1 Bandera de doble estado (ReformaActivationFlag)

Nota de lectura sobre el diagrama: el estado EN_VERIFICACION que aparece abajo no es un tercer valor de `regimen_reforma_659` (que conserva solo ACTUAL y FUTURO, ver D.2 y `06_mapa_definitivo_de_modulos.md` seccion 5 punto 2); es el valor intermedio del campo tecnico `estado_interno_verificacion_659` (D.2), que registra en que paso de revision interna esta el equipo del proveedor mientras `regimen_reforma_659` sigue mostrando ACTUAL a toda la organizacion cliente.

```
                (1) equipo del producto detecta
                    aprobacion legislativa
        [ACTUAL] -------------------------------> [EN_VERIFICACION]
           ^                                              |
           |                                              | (2) se confirma publicacion
           |                                              |     en el Diario Oficial +
           |                                              |     8 dias de vacatio legis +
           |                                              |     validacion juridica del
           |                                              |     texto oficial
           |                                              v
           |                                         [FUTURO]
           |                                              |
           | (3) el decreto no se publica,                |
           |     es impugnado, o su texto                 | (4) opera con normalidad
           |     difiere de lo reportado                   |     (evento emitido a los
           |     (reversion)                               |      5 modulos consumidores)
           +----------------------------------------------+
```

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| ACTUAL | El equipo del producto detecta que la Asamblea Legislativa aprobo la reforma (ya ocurrido: 17-sep-2026) | Ninguna | EN_VERIFICACION | Editor de contenido regulatorio del proveedor | Se muestra un banner informativo a todas las organizaciones: "Decreto Legislativo 659, segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado" (decision 2.7.32); no cambia ninguna obligacion todavia |
| EN_VERIFICACION | Confirmar publicacion oficial + vacatio legis cumplida + validacion juridica del texto | `fecha_publicacion_diario_oficial_reforma` completa; `fecha_cumplimiento_vacatio_legis` alcanzada; `validacion_juridica_texto_oficial` = Si | FUTURO | Editor de contenido regulatorio del proveedor (nunca automatico; nunca ejecutado por un usuario de la organizacion cliente) | Se registra `fecha_activacion_bandera`; se emite el evento "cambio de bandera" hacia MOD-002, MOD-007, MOD-008, MOD-011, MOD-015 y MOD-017; se crean tareas de revision en MOD-021 para cada organizacion; se actualiza el `estado_instrumento` del instrumento normativo relacionado (via `obligaciones_relacionadas`, seccion D.1) con cada una de las 17 obligaciones afectadas, preservando su clasificacion anterior en el historial |
| EN_VERIFICACION | El decreto no llega a publicarse en un plazo razonable, o se retira | Ninguna condicion adicional | ACTUAL | Editor de contenido regulatorio del proveedor | Se mantiene el banner informativo; no hay cambio de obligaciones |
| FUTURO | El decreto es impugnado, no se publica conforme a lo reportado, o su texto oficial difiere materialmente de las fuentes secundarias usadas | `motivo_reversion` completo | ACTUAL | Editor de contenido regulatorio del proveedor | Se emite el evento "reversion de bandera" hacia los mismos seis modulos; las tareas y registros que dependian de pasos exclusivos del regimen FUTURO se marcan "no aplica bajo el estado regulatorio actual, ver historial", sin eliminarse (principio de la seccion 5, punto 6, de `06_mapa_definitivo_de_modulos.md`); los expedientes ya cerrados bajo FUTURO conservan la regla que aplicaba al momento de su cierre |
| FUTURO | Confirmacion de que el estado FUTURO es definitivo (no hay transicion adicional prevista; el sistema permanece en FUTURO de forma indefinida salvo una reversion excepcional) | - | FUTURO | - | Estado estable |

Registros vinculados: el cambio de bandera nunca modifica retroactivamente un expediente sancionador, un registro de MOD-002 o un aviso de privacidad ya publicado; cada uno conserva la version de la regla que le aplicaba en el momento de su ultima accion (ver `MOD-008_ficha.md`, seccion G, regla 3, y `MOD-002_ficha.md`, seccion F).

### F.2 Tramites ante la ACE (ACEFiling)

```
      (1) se genera desde este modulo,               (1b) o llega como evento desde
          o desde MOD-002/MOD-010                         MOD-002 (nombramiento) o
                    |                                      MOD-010 (transferencia)
                    v
              [BORRADOR]
                    |
                    | (2) se completa documento_adjunto
                    |     y canal_de_envio
                    v
          [PENDIENTE_DE_ENVIO]
                    |
                    | (3) doble control: quien redacta no aprueba solo;
                    |     Aprobador o segundo Responsable Legal confirma el envio
                    v
               [ENVIADO] ------(4a) la ACE confirma recepcion)-----> [CONFIRMADO]
                    |
                    +----------(4b) la ACE rechaza o el canal no existe)---> [RECHAZADO]
                    |
                    +----------(4c) el tramite deja de ser necesario,
                                     por ejemplo se revierte la bandera
                                     de reforma 659)---------------------> [NO_APLICA]
```

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (ninguno) | Se genera el registro | Automatico si el origen es MOD-002 o MOD-010; manual si el origen es "Manual" (por ejemplo, OBL-AUD-02 o una solicitud de opinion previa iniciada directamente aqui) | BORRADOR | Sistema (automatico) o Administrador/Responsable Legal | Evento de auditoria; visible en el modulo de origen como estado de solo lectura (ver `MOD-010_ficha.md`, seccion D) |
| BORRADOR | Completar canal de envio y adjuntar el documento final | documento_adjunto y canal_de_envio completos | PENDIENTE_DE_ENVIO | Administrador de organizacion, Responsable Legal, Delegado/Responsable Interno | Se crea la tarea "Aprobar y enviar tramite ante la ACE" en MOD-021 |
| PENDIENTE_DE_ENVIO | Aprobar y marcar como enviado | Doble control: aprobador distinto de quien completo el borrador | ENVIADO | Aprobador, Responsable Legal (si no redacto el borrador) | Se registra fecha_envio; evidencia del intento de cumplimiento (anti-feature 13); se notifica al modulo de origen para actualizar su estado visible |
| ENVIADO | La ACE confirma recepcion o emite una respuesta | acuse_o_respuesta_ace adjunto | CONFIRMADO | Administrador de organizacion (registra el acuse recibido) | Se cierra la alerta de seguimiento; evidencia completa disponible para MOD-019 |
| ENVIADO | La ACE rechaza el tramite, o transcurre un plazo razonable sin que exista canal oficial habilitado para confirmar la recepcion | Nota explicita de que, a la fecha de este analisis, varios de estos tramites no tienen canal oficial de la ACE (anti-feature 13) | RECHAZADO | Administrador de organizacion (registra el resultado conocido) | Alerta segun tipo_tramite (ver seccion I); no bloquea al modulo de origen, que ya dejo constancia del intento |
| BORRADOR / PENDIENTE_DE_ENVIO / ENVIADO | El tramite deja de ser necesario (por ejemplo, una reversion de la bandera de reforma 659 vuelve opcional una comunicacion pendiente) | Evento automatico desde F.1 | NO_APLICA | Sistema (automatico), con nota visible | Se conserva el registro con la nota "no aplica bajo el estado regulatorio actual, ver historial"; nunca se elimina |

### F.3 Procedimiento Sancionador (SanctionProcedure)

```
Hecho -> denuncia / aviso / oficio / solicitud del propio sujeto obligado
   |
   v
[DILIGENCIA_PRELIMINAR] (opcional, hasta 90 dias habiles prorrogables)
   |
   v
[EMPLAZADO] --(1) se registra fecha_notificacion_recibida y documento_resolucion_inicio
   |
   | (2) 5 dias habiles: contestar, alegar, proponer prueba
   v
[EN_CONTESTACION] ----(2b) no se contesta a tiempo)----> [CONTESTADO_NEGATIVAMENTE] (continua igual)
   |
   | (3) se completa escrito_de_contestacion
   v
[EN_PRUEBA] --(solo via ORDINARIA: alegatos finales, 10 dias habiles)--> [ALEGATOS_FINALES]
   |                                                                            |
   |<---------------------------------------------------------------------------+
   |
   | (4) remision del expediente (maximo 8 dias habiles; 5 si hay allanamiento)
   v
[EN_RESOLUCION] (15 dias habiles)
   |
   | (5) resolucion final
   v
[RESUELTO] --(6a) via simplificada: sin recurso, contencioso-administrativo)--> [FIRME]
   |
   +----(6b) via ordinaria: recurso interpuesto dentro de plazo)----> [EN_RECURSO] --> [FIRME]
   |
   v
[FIRME] --(7) si hay multa: 15 dias habiles para pagar)--> [PAGADO] o [EN_COBRO_EJECUTIVO_FGR] (informativo)
   |
   v
[CERRADO] --(8) transcurren 5 anos desde la firmeza o el ultimo hecho)--> [PRESCRITO_ARCHIVADO]
```

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (ninguno) | Iniciar registro del caso | Se conoce el origen del caso (emplazamiento, diligencia preliminar o denuncia conocida) | DILIGENCIA_PRELIMINAR o EMPLAZADO (segun origen_del_caso) | Administrador de organizacion, Responsable Legal | Evento de auditoria; alerta HIGH inmediata (seccion I) |
| DILIGENCIA_PRELIMINAR | Se recibe resolucion de inicio con emplazamiento | documento_resolucion_inicio adjunto | EMPLAZADO | Administrador de organizacion, Responsable Legal | Se calcula, via MOD-023, la fecha limite de contestacion (fecha_notificacion + 1 dia + 5 dias habiles) |
| EMPLAZADO | Completar y enviar escrito de contestacion | escrito_de_contestacion completo dentro del plazo de 5 dias habiles | EN_CONTESTACION -> EN_PRUEBA | Responsable Legal (con apoyo de Delegado/Responsable Interno y Asesor externo si aplica); aprobacion de doble control antes de considerarse enviado | Evidencia del escrito con fecha cierta; si vence sin contestar, los hechos se tienen por contestados negativamente y el procedimiento continua igual (Art. 21 Normativa PAS) |
| EN_PRUEBA | Via ORDINARIA: presentar alegatos finales | Solo si via_procedimiento = ORDINARIA; plazo de 10 dias habiles | ALEGATOS_FINALES -> EN_RESOLUCION | Responsable Legal | Limitado a los hechos e infracciones de la resolucion de inicio (Art. 29 Normativa PAS) |
| EN_PRUEBA / ALEGATOS_FINALES | Remision del expediente por el delegado instructor de la ACE (hecho externo, se registra su plazo) | Maximo 8 dias habiles (5 si hubo allanamiento) | EN_RESOLUCION | Sistema (registra el plazo esperado); Administrador (registra la fecha real si la conoce) | Contador de plazo visible, sin accion propia de la empresa |
| EN_RESOLUCION | Se recibe la resolucion final | resultado_resolucion_final completado | RESUELTO | Administrador de organizacion, Responsable Legal | Si hay sancion: monto_multa_impuesta y medidas_adicionales_ordenadas completos; se calcula el plazo de pago de 15 dias habiles; alerta segun seccion I |
| RESUELTO | Via simplificada: no cabe recurso administrativo | via_procedimiento = SIMPLIFICADA | FIRME | Sistema (automatico, informativo: queda abierta la via contencioso-administrativa, fuera del alcance de este modulo) | Se activa el conteo de prescripcion de la sancion |
| RESUELTO | Via ordinaria: interponer recurso dentro de plazo | via_procedimiento = ORDINARIA; recurso_interpuesto distinto de NINGUNO, dentro del plazo de la LPA | EN_RECURSO | Responsable Legal, con aprobacion de Aprobador | Contador de plazo del recurso; decision de interponerlo queda registrada como decision de la organizacion (seccion H) |
| EN_RECURSO | Se resuelve el recurso (sin mas recurso disponible) | - | FIRME | Sistema (registra el resultado) | Se activa el conteo de prescripcion de la sancion |
| FIRME | Se paga la multa dentro de 15 dias habiles | comprobante_pago_multa adjunto | PAGADO | Administrador de organizacion | Evidencia J (seccion J); cierra la alerta de pago |
| FIRME | Vence el plazo de pago sin registrar comprobante | Transcurridos 15 dias habiles | EN_COBRO_EJECUTIVO_FGR (informativo) | Sistema (informativo; el cobro ejecutivo lo ejecuta la FGR, no el software) | Alerta CRITICAL persistente; el sistema nunca ejecuta ni simula el cobro, solo documenta que el plazo establecido por la Normativa PAS vencio |
| PAGADO / EN_COBRO_EJECUTIVO_FGR | Se completan las medidas adicionales ordenadas (si las hay) | Tareas asociadas en MOD-021 completadas | CERRADO | Administrador de organizacion, Responsable Legal | El caso queda disponible como historico completo; alimenta el indicador de historial de sanciones (seccion M) |
| CERRADO | Transcurren 5 anos desde la firmeza de la sancion o desde el ultimo hecho de la infraccion (lo que corresponda) | Automatico, via MOD-023 | PRESCRITO_ARCHIVADO | Sistema | Se cierra el requisito de retencion minima de evidencia (OBL-SANC-07); el expediente permanece disponible como historico, nunca se elimina (anti-feature 19) |

Registros vinculados: si el caso se origina en un incidente de seguridad (MOD-013) o en una solicitud ARCO-POL vencida (MOD-011, OBL-SANC-09) o en un reclamo del titular (MOD-011, OBL-ARCO-14), el expediente sancionador referencia esos registros por enlace, nunca los duplica; al cerrar el expediente, esos modulos de origen quedan con el enlace visible en su propio historial.

---

## G. Automatizaciones

1. **Disparador:** la bandera `regimen_reforma_659` cambia de ACTUAL a FUTURO (o se revierte de FUTURO a ACTUAL). **Condicion:** ninguna (evento regulatorio global, aplicado a cada organizacion por igual). **Accion:** emitir el evento "cambio de bandera" hacia MOD-002, MOD-007, MOD-008, MOD-011, MOD-015 y MOD-017; crear en MOD-021, para cada organizacion, la tarea "Revisar el impacto del cambio de regimen normativo"; actualizar la etiqueta de `estado_instrumento` del instrumento normativo relacionado (via `obligaciones_relacionadas`, seccion D.1) con cada una de las 17 obligaciones afectadas, preservando la clasificacion anterior en el historial (no se sobrescribe, se versiona). Configurable: no.
   - De estos seis modulos, `mapa_modulos.json` solo declara cinco (MOD-002, MOD-007, MOD-011, MOD-015 y MOD-017) en el `alimenta_a` de MOD-024. Se agrega MOD-008 a la lista real de receptores del evento porque su propia ficha ya escrita (`MOD-008_ficha.md`, seccion G, regla 3) declara una automatizacion propia disparada exactamente por "MOD-024 cambia la bandera `regimen_reforma_659` de ACTUAL a FUTURO", condicionada a que exista al menos un Aviso de Privacidad en estado PUBLICADO/VIGENTE; sin recibir este evento, MOD-008 no tendria como disparar esa automatizacion. Discrepancia detectada, no corregida sobre el documento fuente (mismo patron que la seccion L usa para MOD-002/MOD-010): se recomienda que una proxima revision de `mapa_modulos.json` agregue "MOD-008" al `alimenta_a` de MOD-024.
   - No se agrega MOD-016 a esta lista, a pesar de que OBL-RET-04 (propiedad de MOD-016) es una de las 17 obligaciones afectadas por la reforma 659 (`06_mapa_definitivo_de_modulos.md`, seccion 5, punto 3). `MOD-016_ficha.md` (seccion D.3, fundamento de OBL-RET-04, y seccion L) describe su relacion con la bandera como una consulta de referencia bajo demanda ("solo consulta la bandera de MOD-024 para decidir que texto de ayuda contextual mostrar... nunca para acortar o alargar el plazo de conservacion"), no como una automatizacion propia disparada por el evento; el propio `MOD-016_ficha.md`, seccion G, no tiene ninguna regla con disparador "cambio de bandera de MOD-024". Ese patron de consulta por referencia, sin copia ni evento, es exactamente el que ya cubre la automatizacion 9 de esta misma seccion ("cualquier otro modulo consulta si el estado normativo vigente afecta a una obligacion propia... responder con el estado vigente por referencia, nunca por copia"), y la actualizacion de `estado_instrumento` de esta regla 1 ya dejo esa informacion actualizada para que MOD-016 la lea cuando la necesite. Agregar MOD-016 a la lista de receptores del evento push duplicaria, sin necesidad funcional, un mecanismo que ya existe como consulta.
2. **Disparador:** el Editor de contenido regulatorio publica una nueva `RegulatoryRuleVersion` sobre un instrumento existente (por ejemplo, un cambio de plazo o de formulario). **Condicion:** ninguna. **Accion:** conservar la version anterior con su `fecha_vigencia_hasta` cerrada (nunca se sobrescribe); identificar que obligaciones, modulos, documentos y tareas cita esa regla; crear en MOD-021 la tarea "Revisar cambio normativo: [nombre del instrumento]" dirigida a Administrador, Delegado/Responsable Interno y Responsable Legal; mostrar la experiencia completa de "que cambio" descrita en el requisito de la tarea (submodulo Actualizaciones normativas). Configurable: no.
3. **Disparador:** una organizacion registra `fecha_notificacion_recibida` en un nuevo expediente de Procedimiento Sancionador. **Condicion:** ninguna. **Accion:** calcular, via MOD-023, la fecha limite de contestacion (fecha_notificacion + 1 dia + 5 dias habiles, OBL-SANC-05); crear la tarea urgente "Contestar emplazamiento de la ACE" en MOD-021, con prioridad maxima; emitir alerta CRITICAL inmediata (seccion I). Configurable: el plazo legal no; el canal de recordatorio si.
4. **Disparador:** MOD-002 completa el paso "Enviar comunicacion a la ACE" de su propio workflow (nombramiento del Delegado), o MOD-010 pasa una transferencia internacional a ACTIVA. **Condicion:** ninguna. **Accion:** crear automaticamente un registro ACEFiling en estado BORRADOR, con `modulo_origen` y `contenido_del_tramite` precargados por referencia desde el modulo que lo origino, sin duplicar los datos (regla de "direccion unica"). Configurable: no.
5. **Disparador:** un registro ACEFiling permanece en BORRADOR o PENDIENTE_DE_ENVIO mas alla de un umbral configurable (por defecto, 15 dias habiles desde su creacion). **Condicion:** ninguna. **Accion:** emitir alerta WARNING semanal, escalando a CRITICAL y a Administrador de organizacion a los 30 dias habiles (mismo patron ya documentado en `MOD-010_ficha.md`, seccion I, para la puesta en conocimiento de transferencias). Configurable: el umbral en dias si; que la alerta exista, no.
6. **Disparador:** un expediente de Procedimiento Sancionador llega a RESUELTO con `resultado_resolucion_final` distinto de SIN_SANCION_ARCHIVADO. **Condicion:** ninguna. **Accion:** calcular el plazo de pago de 15 dias habiles (OBL-SANC-06); crear tareas en MOD-021 para cada medida adicional ordenada (OBL-SANC-03), enlazadas al catalogo de controles de MOD-015 cuando la medida sea de naturaleza tecnica u organizativa; calcular `fecha_limite_prescripcion` a 5 anos desde la firmeza (OBL-SANC-07), coordinando con la regla de retencion de evidencia de MOD-016. Configurable: no en los plazos legales.
7. **Disparador:** una resolucion sancionatoria queda FIRME. **Condicion:** ninguna. **Accion:** crear la tarea informativa "Monitorear publicacion de la resolucion en el sitio de la ACE" (OBL-SANC-08, Art. 55), sin que el sistema publique ni gestione nada por su cuenta; registrar el enlace a la version publica cuando la organizacion lo aporte. Configurable: la frecuencia de monitoreo si.
8. **Disparador:** MOD-011 detecta que una solicitud ARCO-POL incumplio el plazo de rectificacion o de tramite de revocacion (OBL-SANC-09) o registra un reclamo del titular ante la Direccion de Proteccion de Datos (OBL-ARCO-14). **Condicion:** ninguna. **Accion:** mostrar el enlace a ese caso dentro del panel de "Denuncias y reclamos" de este modulo, sin crear un expediente de Procedimiento Sancionador de forma automatica (eso exige que la ACE efectivamente abra un caso, ver seccion H). Configurable: no.
9. **Disparador:** cualquier otro modulo consulta si el estado normativo vigente afecta a una obligacion propia (por ejemplo, MOD-015 mostrando si "Delegado de Proteccion de Datos designado" sigue siendo obligatorio). **Condicion:** existe una `RegulatoryRuleVersion` vigente para esa obligacion. **Accion:** responder con el estado vigente por referencia, nunca por copia. Configurable: no.
10. **Disparador:** se completa `monto_multa_impuesta` en un expediente. **Condicion:** ninguna. **Accion:** mostrar, ademas del monto real impuesto por la ACE, el rango orientativo completo de la categoria de infraccion (informativo, nunca una prediccion), con la tabla de salarios minimos vigente y, si el salario minimo cambio entre la fecha del hecho y la fecha de la resolucion, ambos valores (incertidumbre I-1 de `sweep_sanciones_procedimiento.md`). Configurable: no.

---

## H. Decisiones que NO debe automatizar

1. **Activar el estado FUTURO de la bandera `regimen_reforma_659`, o revertirlo.** El sistema nunca lo hace por la sola aprobacion legislativa, por el paso del tiempo o por una fecha calculada; requiere que el Editor de contenido regulatorio del proveedor confirme manualmente la publicacion oficial, la vacatio legis y la validacion juridica del texto. Texto que muestra el sistema mientras la bandera sea ACTUAL: "Decreto Legislativo 659, segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado." Por que: activar un regimen legal que no esta vigente dejaria a las organizaciones sin cumplir obligaciones que la ley todavia exige (anti-feature 14).
2. **Calificar si un hecho concreto de la empresa encaja en alguna de las 26 infracciones del Art. 56, o si constituye una infraccion en absoluto.** El sistema solo ofrece el catalogo como referencia; la calificacion es facultad exclusiva de la ACE dentro del procedimiento. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada." Por que: es un juicio juridico sobre hechos propios que el software no puede verificar por si mismo.
3. **Graduar la multa o predecir su monto exacto para un caso concreto.** El sistema muestra el rango legal completo (Art. 57) y los criterios de graduacion del Art. 43 de la Normativa PAS (gravedad del dano, efecto disuasivo, duracion, intencionalidad, categoria de los datos, capacidad economica) solo como informacion, nunca como calculo propio. Mismo texto de advertencia. Por que: la ponderacion de esos criterios es facultad exclusiva de la Direccion de Proteccion de Datos de la ACE.
4. **Decidir la estrategia de defensa de la organizacion:** si allanarse, si pedir inspeccion o peritaje, que pruebas presentar, si interponer un recurso y cual. El sistema calcula los plazos disponibles para cada opcion y organiza el expediente, pero la decision y su redaccion final quedan siempre a cargo de Responsable Legal, con o sin asesor externo. Mismo texto de advertencia. Por que: son decisiones estrategicas con consecuencias legales que exceden lo que un sistema de gestion puede o debe decidir.
5. **Certificar que un tramite ante la ACE (comunicacion del nombramiento del Delegado, puesta en conocimiento de una transferencia, solicitud de opinion previa o de certificacion/sello) fue efectivamente recibido y aceptado**, mientras la ACE no habilite un canal oficial para varios de estos tramites. El sistema deja evidencia del intento de envio (fecha, documento, canal usado), no certifica la recepcion por un sistema externo fuera de su control. Por que: depende de la disponibilidad de un canal que, a la fecha de este analisis, la ACE aun no ha habilitado formalmente para todos los casos (anti-feature 13; incertidumbre I-11 de `sweep_sanciones_procedimiento.md`).
6. **Decidir si una recomendacion de la ACE, una medida provisional o una medida adicional ordenada esta correctamente cumplida.** El sistema registra la evidencia de ejecucion que la organizacion aporte; la suficiencia de esa evidencia frente a lo que la ACE espera es una valoracion de la organizacion, idealmente con apoyo legal. Mismo texto de advertencia.
7. **Emitir la certificacion oficial de Delegado o cualquier sello o certificacion de proteccion de datos (OBL-AUD-02).** El sistema solo recuerda que esa facultad existe y, cuando la ACE la habilite, enlaza al canal oficial. Por que: es facultad exclusiva de la ACE (anti-feature 12), y a la fecha de este analisis no existe ningun mecanismo de certificacion habilitado para organizaciones.

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Cambio de estado regulatorio (reforma 659) | La bandera pasa de ACTUAL a FUTURO, o se revierte | INFO | Administrador, Delegado/Responsable Interno, Responsable Legal, Responsable de area | Plataforma + correo | Una vez por cambio | No aplica (informativa) | Se confirma la lectura de la notificacion |
| Nueva actualizacion normativa publicada | El Editor de contenido regulatorio publica una nueva version de una regla | INFO o WARNING segun impacto declarado | Administrador, Delegado/Responsable Interno, Responsable Legal | Plataforma + correo | Una vez por publicacion | A Aprobador si no se revisa en 10 dias habiles | La tarea de revision se completa |
| Emplazamiento recibido (nuevo procedimiento sancionador) | Se registra `fecha_notificacion_recibida` | CRITICAL | Administrador de organizacion, Responsable Legal, Aprobador | Plataforma + correo | Inmediata y diaria hasta que se asigne responsable | Visible en el dashboard de Gerencia desde el primer dia | Se asigna un responsable a la tarea de contestacion |
| Contestacion por vencer | Faltan 2 dias habiles para el limite de 5 dias habiles (Art. 21 Normativa PAS) | WARNING, sube a CRITICAL al ultimo dia | Responsable Legal, Administrador | Plataforma + correo | Diaria desde 2 dias | A Aprobador el ultimo dia | Escrito de contestacion enviado |
| Contestacion vencida | Vencio el plazo sin contestar | HIGH | Responsable Legal, Administrador, Aprobador | Plataforma + correo | Diaria | Visible en el dashboard de Gerencia | El procedimiento avanza igual (hechos contestados negativamente); alerta se cierra al pasar a EN_PRUEBA |
| Resolucion final con sancion registrada | `resultado_resolucion_final` distinto de SIN_SANCION_ARCHIVADO | HIGH | Administrador, Responsable Legal, Aprobador | Plataforma + correo | Una vez | Visible en el dashboard de Gerencia | Se completa el pago o se cierra el caso |
| Pago de multa por vencer | Faltan 3 dias habiles para el limite de 15 dias habiles (Art. 44 Normativa PAS) | WARNING | Administrador de organizacion | Plataforma + correo | Diaria desde 3 dias | A Aprobador el ultimo dia | comprobante_pago_multa adjunto |
| Pago de multa vencido | Vencio el plazo de 15 dias habiles sin comprobante | CRITICAL | Administrador, Responsable Legal, Aprobador | Plataforma + correo | Diaria | Visible en el dashboard de Gerencia | Se adjunta comprobante, o se documenta el cobro ejecutivo por la FGR |
| Prescripcion proxima | Faltan 90 dias para cumplir 5 anos desde la firmeza o el ultimo hecho (OBL-SANC-07) | INFO | Responsable Legal, Auditor | Plataforma | Una vez | No aplica | Transcurre la fecha; el registro pasa a PRESCRITO_ARCHIVADO |
| Tramite ante la ACE pendiente de envio | Registro ACEFiling en BORRADOR o PENDIENTE_DE_ENVIO por mas de 15 dias habiles | WARNING | Administrador, Responsable Legal, Delegado/Responsable Interno | Plataforma + correo | Semanal | A Administrador de organizacion a los 30 dias habiles | Se marca ENVIADO |
| Reclamo o denuncia del titular vinculada | MOD-011 registra un reclamo (OBL-ARCO-14) o una posible denuncia por incumplimiento de plazos (OBL-SANC-09) | WARNING | Responsable Legal, Administrador | Plataforma + correo | Una vez | A Aprobador a los 5 dias habiles sin revisar | Se revisa el enlace y se decide si amerita seguimiento adicional |
| Falta calendario de dias habiles configurado para el ano en curso | MOD-023 no tiene el calendario del ano vigente | CRITICAL | Administrador de organizacion | Plataforma + correo | Diaria hasta resolver | A Aprobador a los 2 dias | Se configura el calendario en MOD-023 |

---

## J. Evidencia

| Evidencia | Como se conserva | Obligacion que prueba | Retencion |
|---|---|---|---|
| Historial de versiones del marco normativo (RegulatoryRuleVersion) | Cada version con su fecha de vigencia_desde/hasta, nunca sobrescrita | Trazabilidad de que regla aplicaba a un expediente en una fecha pasada (hipotesis de `PROMPT_BASE...md` seccion 41, adoptada como diseno) | Historico indefinido |
| Registro de activacion y reversion de la bandera de reforma 659, con evidencia de verificacion (publicacion, vacatio legis, validacion juridica) | Registro con fecha, hora y responsable (Editor de contenido regulatorio) | OBL-PLAZO-05 | Historico indefinido, nunca se elimina |
| Constancia de notificacion de cada cambio de bandera a cada organizacion | Registro con fecha y organizacion notificada | OBL-PLAZO-05; principio de responsabilidad demostrada (OBL-PRIN-03) | Historico indefinido |
| Expediente completo de cada Procedimiento Sancionador (resolucion de inicio, contestacion, pruebas, resolucion final, recursos, comprobante de pago) | Adjuntos con hash, fecha, usuario que los cargo, version | OBL-SANC-01 a 09 | Minimo 5 anos desde la firmeza o el ultimo hecho relevante (OBL-SANC-07); si hay procedimiento abierto, hasta su firmeza y ejecucion completa |
| Registro de requerimientos de informacion de la ACE y sus respuestas | Registro con fecha, contenido solicitado, plazo y respuesta enviada | Art. 50 lit. t) LPDP | Igual que el expediente relacionado |
| Registro de cada tramite ante la ACE (ACEFiling), con su documento final y acuse o respuesta si existe | Registro con fecha de generacion, envio, canal usado y resultado | OBL-DPO-01 (via MOD-002), OBL-TRANSF-05 (via MOD-010), OBL-AUD-02 | Historico indefinido, nunca se elimina |
| Bitacora de monitoreo de publicidad de resoluciones sancionatorias (OBL-SANC-08) | Registro con fecha de verificacion y enlace a la version publica cuando exista | OBL-SANC-08 | Igual que el expediente relacionado |
| Historial de infracciones, apercibimientos y medidas recibidas de la ACE (RECOMENDADO, buena practica) | Registro consolidado por organizacion | Base factica de atenuantes (LPA Arts. 145, 156, 157) y de elegibilidad del Delegado (Lineamientos DPO) | Historico indefinido |

Todo evento de esta tabla queda ademas en el AuditLog transversal de solo escritura por adicion (append-only), y toda exportacion hacia el paquete de evidencias de MOD-019 incluye un mecanismo propio de verificacion de integridad (hash o firma), conforme a la decision 2.7.24 de `02_validacion_de_la_idea.md`.

---

## K. Documentos asociados

- **Documentos requeridos como entrada:** resolucion de inicio y emplazamiento emitidos por la ACE; escritos, pruebas e informes de auditoria internos o externos que la organizacion decida presentar; comprobante de pago de la multa; acta o documento que respalde el nombramiento del Delegado o la transferencia internacional cuando el tramite ante la ACE se origina en MOD-002 o MOD-010.
- **Documentos generados:** escrito de contestacion del emplazamiento; registro de decision de allanamiento; escrito de recurso (via ordinaria); registro de tramite ante la ACE con su documento final; reporte de "que cambio" de cada actualizacion normativa.
- **Plantillas que el sistema provee:**
  - "Modelo de escrito de contestacion de emplazamiento" (variables: identificacion de la organizacion, numero de expediente, hechos, alegatos, prueba propuesta). Requiere validacion de la organizacion o asesoria especializada antes de usarse (seccion H).
  - "Formato de registro de tramite ante la ACE" (variables: tipo de tramite, contenido precargado por referencia desde el modulo de origen, canal usado).
  - "Bitacora de verificacion de publicacion oficial de un cambio normativo" (variables: instrumento, fecha de publicacion, fecha de vacatio legis, resultado de la validacion juridica). Uso exclusivo del Editor de contenido regulatorio del proveedor.
  - "Catalogo descargable de infracciones y multas" (Art. 56 y 57 LPDP), informativo, sin variables de la organizacion.
- **Anexos y evidencias documentales:** imagenes OCR de las fuentes primarias citadas (`01_legal/fuentes/ocr/normativa_sancionadora/`), comprobantes de pago, acuses de recepcion de la ACE cuando existan, resoluciones sancionatorias publicadas en version publica.

---

## L. Dependencias

```
                    MOD-023 Calendario y Motor de Plazos
                       (dias/horas habiles para todo plazo)
                                    |
                                    v
   MOD-002 Delegado -----> [ evento: tramite de     MOD-010 Transferencias
   (evento saliente:         nombramiento ]  <----- (evento saliente: borrador
    tramite de                    |                  de puesta en conocimiento
    nombramiento)                 v                  a la ACE, ACEFiling)
                        +-------------------+
                        |     MOD-024       |
                        | Centro Regulatorio|
                        +-------------------+
                                    |
        +----------+----------+----------+----------+----------+----------+----------+
        v          v          v          v          v          v          v
     MOD-002    MOD-007    MOD-008    MOD-011    MOD-015    MOD-017    MOD-021
   (bandera    (bandera    (evento    (bandera    (catalogo  (capacita-  (tareas de
    de doble    de doble    "cambio    de doble    de         cion del    revision y
    estado      estado      de         estado      disposi-   Delegado:   del expe-
    para        para        bandera",  para        ciones     opcional    diente
    tipo_rol)   revoca-     regla G-3  aprobador   ACE, item  bajo        sancio-
                ciones)     propia)    por         "Delegado  FUTURO)     nador)
                                       defecto)    designado")
```

- **Entra desde MOD-023** (Calendario y Motor de Plazos): el servicio unico de calculo de dias y horas habiles que este modulo consulta para todos los contadores del Procedimiento Sancionador (5, 8, 10, 15 dias habiles) y para el conteo de prescripcion a 5 anos (decision 2.7.15 de `02_validacion_de_la_idea.md`, que nombra explicitamente a "Procedimiento sancionador" como uno de los cuatro consumidores del motor de plazos unico).
- **Entra desde MOD-002** (Delegado / Responsable Interno de Datos): el evento saliente "tramite de nombramiento" que `03_modulos/MOD-002_ficha.md` (seccion E y F, transicion NOTIFICADO_INTERNAMENTE -> COMUNICADO_A_ACE) declara expresamente que envia a este modulo, y que este modulo recibe como un nuevo registro ACEFiling en BORRADOR (ver seccion F.2).
- **Entra desde MOD-010** (Transferencias Internacionales): el borrador de "puesta en conocimiento a la ACE" (ACEFiling) que `03_modulos/MOD-010_ficha.md` (secciones D, G y K) declara expresamente que genera dentro de este modulo cuando una transferencia internacional pasa a ACTIVA, y la solicitud opcional de opinion previa a la ACE.
- **Entra desde MOD-011** (ARCO-POL): el enlace a un reclamo del titular ante la Direccion de Proteccion de Datos (OBL-ARCO-14) o a una posible denuncia por incumplimiento de plazos (OBL-SANC-09), mostrados en el panel de "Denuncias y reclamos" de este modulo (ver seccion G, regla 8).
- **Entra desde MOD-013** (Incidentes de Seguridad): informacion de referencia sobre si la organizacion fue calificada como operador de infraestructura critica (OBL-INC-05), mostrada como parte del marco normativo consultable.
- **Sale hacia MOD-002** (Delegado / Responsable Interno de Datos): la bandera `regimen_reforma_659`, que determina el valor por defecto de `tipo_rol` (ver `MOD-002_ficha.md`, seccion D, campo `tipo_rol`).
- **Sale hacia MOD-007** (Consentimiento): la bandera de doble estado, que determina quien aprueba y ejecuta cada revocacion de consentimiento (ver `MOD-007_ficha.md`, seccion D y G, regla 9).
- **Sale hacia MOD-008** (Documentos y Politicas): el evento "cambio de bandera", que dispara la automatizacion propia de MOD-008 (ver `MOD-008_ficha.md`, seccion G, regla 3) que crea la tarea "Revisar avisos publicados tras el cambio de regimen" cuando existe al menos un Aviso de Privacidad en estado PUBLICADO/VIGENTE.
- **Sale hacia MOD-011** (ARCO-POL): la bandera de doble estado, que determina el aprobador por defecto de todo acto atribuido hoy "al Delegado" (ver `MOD-011_ficha.md`, seccion G, regla 14).
- **Sale hacia MOD-015** (Controles de Seguridad): la bandera de doble estado, que determina si el item de catalogo "Delegado de Proteccion de Datos designado" sigue siendo obligatorio o pasa a buena practica recomendada (ver `MOD-015_ficha.md`, nota sobre la reforma 659).
- **Sale hacia MOD-017** (Capacitacion): la bandera de doble estado, que determina si OBL-CAP-02 (capacitacion especifica del Delegado) sigue siendo obligatoria o pasa a buena practica voluntaria.
- **Sale hacia MOD-021** (Centro de Tareas): todas las tareas descritas en la seccion G, incluidas las del expediente de Procedimiento Sancionador y las de revision de cambios normativos.
- **Sale hacia MOD-019** (Centro de Evidencias, via el patron transversal general de todo modulo operativo): el paquete de evidencia del expediente sancionador y del registro de tramites ante la ACE.
- **Consulta (servicio transversal, no dependencia de datos de negocio):** MOD-001 (catalogo de usuarios y roles), MOD-022 (notificaciones), MOD-026 (ayuda contextual).

**Que ocurre si un modulo dependiente no existe en el MVP.** MOD-023 es MUST HAVE, de modo que el calculo de plazos del Procedimiento Sancionador esta garantizado desde el primer dia. MOD-002 y MOD-011 son MUST HAVE; MOD-007, MOD-008, MOD-015 y MOD-017 tambien son MUST HAVE (ver `06_mapa_definitivo_de_modulos.md`, seccion 0); ninguno de los seis modulos que reciben el evento "cambio de bandera" falta en el MVP. MOD-010 es SHOULD HAVE: mientras no este disponible en su version completa, el borrador automatico de ACEFiling para transferencias no se genera, y la cobertura parcial ya documentada en `06_mapa_definitivo_de_modulos.md` (el Diagnostico crea una tarea manual en MOD-021) se traduce, para este modulo, en que la organizacion puede registrar manualmente un tramite ACEFiling con `modulo_origen` = "Manual" en vez de recibirlo automaticamente.

**Discrepancia detectada respecto al mapa definitivo (senalada, no corregida sobre el documento fuente).** El campo `depende_de` de MOD-024 en `mapa_modulos.json` esta vacio ("entra desde ninguno") y asi lo repite `06_mapa_definitivo_de_modulos.md`, seccion 3, ficha resumida de MOD-024. Sin embargo, las fichas ya escritas de MOD-002 (seccion E: "Evento saliente tramite de nombramiento... Registro en MOD-024, submodulo Tramites ante la ACE"; seccion L: "Sale hacia MOD-024") y de MOD-010 (secciones D, G y K: el borrador de ACEFiling "se materializa como registro... dentro de MOD-024") declaran de forma explicita y consistente entre si que ambos modulos SI envian datos hacia este modulo. Esta ficha modela esa dependencia real (MOD-024 recibe eventos de MOD-002 y MOD-010 para poblar su submodulo Tramites ante la ACE, ver seccion F.2), en vez de contradecir dos fichas ya escritas que coinciden entre si. Se recomienda que una proxima revision de `mapa_modulos.json` agregue "MOD-002" y "MOD-010" a la lista `depende_de` de MOD-024, y "MOD-024" a la lista `alimenta_a` de ambos, para cerrar esta asimetria de documentacion (mismo patron de discrepancia ya senalado, sin corregirse en la fuente, por `MOD-002_ficha.md` respecto de MOD-023 y por `MOD-021_ficha.md` respecto de MOD-014 y MOD-018).

La misma asimetria existe en sentido inverso con MOD-008: `mapa_modulos.json` no incluye "MOD-008" en el `alimenta_a` de MOD-024 (solo lista MOD-002, MOD-007, MOD-011, MOD-015 y MOD-017), pero `MOD-008_ficha.md` (seccion G, regla 3) ya declara una automatizacion propia disparada por el cambio de esta bandera. Esta ficha modela esa dependencia real (ver seccion G, regla 1, y el bullet "Sale hacia MOD-008" arriba) por el mismo motivo que en el parrafo anterior, y deja la misma recomendacion de actualizar `mapa_modulos.json`. No se agrega MOD-016 a esta lista de eventos salientes: aunque OBL-RET-04 (propiedad de MOD-016) es una de las 17 obligaciones afectadas por la reforma 659, `MOD-016_ficha.md` describe su relacion con esta bandera como una consulta bajo demanda para texto de ayuda contextual (automatizacion 9 de la seccion G de esta ficha), no como una automatizacion propia disparada por el evento; no hay discrepancia que senalar en ese caso porque `mapa_modulos.json` tampoco declara esa arista y el diseno funcional no la necesita.

---

## M. Dashboard

| Indicador | Formula / definicion | Semaforo | Vista por rol |
|---|---|---|---|
| Estado regulatorio vigente | Badge ACTUAL / FUTURO, con fecha del ultimo cambio | No (informativo) | Todas |
| Actualizaciones normativas pendientes de revision | Conteo de tareas "Revisar cambio normativo" en MOD-021 aun no completadas | Si (verde 0, amarillo 1-2, rojo 3 o mas, o cualquiera vencida) | Administrador, Delegado/Responsable Interno, Responsable Legal |
| Procedimientos sancionadores activos | Conteo de expedientes en cualquier estado distinto de CERRADO o PRESCRITO_ARCHIVADO | Si (rojo si hay al menos uno con plazo legal vencido) | Gerencia, Responsable Legal, Auditor |
| Dias habiles para la proxima obligacion del expediente sancionador activo | Minimo entre las fechas limite de contestacion, alegatos, resolucion, recurso y pago, menos la fecha de hoy, en dias habiles (via MOD-023) | Si (colorea segun cercania) | Responsable Legal, Administrador |
| Tramites ante la ACE pendientes de envio | Conteo de registros ACEFiling en BORRADOR o PENDIENTE_DE_ENVIO | Si (amarillo tras 15 dias habiles, rojo tras 30) | Delegado/Responsable Interno, Administrador, Legal |
| Evidencia disponible del modulo | Conteo "X de Y evidencias requeridas disponibles" (contestacion, comprobante de pago, acuses de tramites ACE del periodo vigente). Nunca se expresa como porcentaje de cumplimiento legal | Si | Auditor, Legal |
| Historial de sanciones y apercibimientos (RECOMENDADO) | Conteo acumulado de expedientes cerrados con sancion, por categoria | No (informativo, buena practica) | Legal, Auditor, Gerencia |
| Alertas activas del modulo | Conteo por nivel (INFO, WARNING, HIGH, CRITICAL) | Si | Gerencia (solo HIGH/CRITICAL), Responsable Legal (todas) |

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Marco normativo vigente | Lista completa de instrumentos con su estado, fuente y fecha de consulta | Por tipo de instrumento, por estado | PDF, XLSX | Gerencia, Legal, Auditor | Si |
| Catalogo de infracciones y multas | Las 26 infracciones del Art. 56 con su rango de multa orientativo | Por categoria (leve/grave/muy grave) | PDF | Legal, Gerencia | Si |
| Bitacora de actualizaciones normativas | Cada cambio publicado, con fecha, obligaciones y modulos afectados, y estado de revision | Por rango de fechas | XLSX, CSV | Legal, Auditor | Si |
| Expediente completo de un Procedimiento Sancionador | Resolucion de inicio, contestacion, pruebas, resolucion final, recursos, comprobante de pago, con manifiesto y hash de integridad | Por expediente, por periodo | ZIP con manifiesto firmado | Auditoria interna (MOD-018), asesor externo, requerimiento de la ACE | Si (via MOD-019) |
| Registro de tramites ante la ACE | Todos los ACEFiling con su estado, canal usado y resultado | Por tipo de tramite, por modulo de origen, por periodo | XLSX, CSV | Gerencia, Legal, Auditor | Si |
| Historial del regimen de la reforma 659 | Cada cambio de bandera, fecha, motivo y organizaciones notificadas | Por periodo | PDF | Legal, Auditoria | Si |

---

## O. Historial

Eventos que quedan en el historial del modulo y en la auditoria transversal (AuditLog):

- Publicacion de cada nueva version de un instrumento o regla normativa (quien la publico, dentro del equipo del proveedor, y cuando).
- Cambios de `estado_instrumento` (VIGENTE, FUTURO, DEROGADO, MODIFICADO) de cada instrumento.
- Activacion o reversion de la bandera `regimen_reforma_659`, con fecha, motivo y evidencia de verificacion.
- Confirmaciones de "toma de conocimiento" de cada organizacion ante un cambio normativo relevante.
- Creacion y cada cambio de campo de un expediente de Procedimiento Sancionador (valor anterior y valor nuevo).
- Cambios de estado del expediente (seccion F.3), con fecha y usuario que los ejecuto.
- Decisiones registradas por la organizacion dentro de un expediente: allanamiento, solicitud de inspeccion o peritaje, interposicion de un recurso (quien decidio, cuando, con que fundamento).
- Creacion y cambios de estado de cada registro ACEFiling (seccion F.2), incluido el modulo de origen que lo genero.
- Asignaciones: quien redacto una contestacion o un tramite, quien lo aprobo y envio (doble control).
- Adjuntos: resolucion de inicio, escritos, pruebas, comprobante de pago, documento final de cada tramite, acuses de la ACE.
- Exportaciones: quien exporto que reporte o paquete de evidencia, cuando y con que alcance.
- Accesos de lectura al numero de expediente y a los datos de la persona natural del presunto responsable, por ser de acceso restringido.
- Archivados: un expediente nunca se elimina, solo pasa a CERRADO y luego a PRESCRITO_ARCHIVADO con motivo registrado; un registro ACEFiling que deja de aplicar se marca NO_APLICA, nunca se borra.

---

## P. Riesgos

**Riesgos legales**

- Tratar el estado FUTURO de la reforma 659 como vigente antes de su publicacion oficial, dejando de exigir el Delegado o de calcular las obligaciones afectadas cuando la ley todavia las exige. **Mitigacion de diseno:** la bandera vive exclusivamente en este modulo, se activa manualmente solo tras verificar publicacion, vacatio legis y validacion juridica del texto oficial, y el modulo muestra siempre el banner de advertencia mientras el estado sea ACTUAL (anti-feature 14).
- Que la informacion de multas orientativas (Art. 57) se lea como una prediccion o una determinacion del monto que la ACE impondria en un caso concreto. **Mitigacion:** el rango se muestra siempre junto al texto "informacion orientativa, no una determinacion de la sancion; la graduacion es facultad exclusiva de la ACE" y remite a asesoria juridica (seccion H, decision 3).
- Que el catalogo de infracciones se use para autocalificar un hecho propio como infraccion o como no infraccion. **Mitigacion:** el catalogo se presenta como material de consulta general; la calificacion de un caso concreto siempre exige el texto de advertencia estandar (seccion H, decision 2).

**Riesgos de UX**

- Que la organizacion confunda el contenido informativo (marco normativo, catalogo de infracciones) con un caso propio en curso, sobre todo si nunca ha tenido un procedimiento sancionador activo. **Mitigacion:** separacion visual explicita en toda la interfaz entre los dos submodulos informativos (Marco normativo, Actualizaciones normativas) y los dos submodulos operativos con dinero y plazos reales (Procedimiento Sancionador, Tramites ante la ACE), tal como exige el requisito de la tarea; el panel operativo solo aparece con contenido cuando existe al menos un expediente o tramite real.
- Sobrecarga de notificaciones ante cada actualizacion normativa menor. **Mitigacion:** solo se notifica con WARNING cuando la actualizacion tiene impacto declarado sobre obligaciones o modulos; los cambios puramente editoriales (por ejemplo, corregir una fecha de consulta) quedan en INFO silenciosa dentro del historial de versiones.

**Riesgos operativos**

- Plazos del Procedimiento Sancionador mal calculados si el calendario de dias habiles y asuetos de MOD-023 no esta actualizado para el ano en curso. **Mitigacion:** este modulo nunca calcula plazos por su cuenta, siempre consulta el servicio unico de MOD-023; si el calendario del ano no esta configurado, el sistema bloquea la creacion de nuevas fechas limite y alerta CRITICAL al Administrador en vez de asumir un calendario por defecto.
- Que un ACEFiling generado automaticamente desde MOD-002 o MOD-010 quede en BORRADOR indefinidamente por falta de seguimiento, dejando a la empresa sin evidencia del intento de cumplimiento. **Mitigacion:** la automatizacion 5 (seccion G) y la alerta correspondiente (seccion I) no son configurables en su existencia, solo en su umbral de dias.

**Riesgos de seguridad y privacidad**

- Exposicion del expediente de un Procedimiento Sancionador (que puede describir hechos sensibles de la organizacion) a roles que no lo necesitan. **Mitigacion:** visible solo para Administrador, Responsable Legal, Aprobador y Auditor (con las restricciones de la seccion C); Usuario de consulta y Responsable de area nunca lo ven.
- Que la bandera de doble estado o el contenido normativo sean editables por error desde una cuenta de organizacion cliente. **Mitigacion:** la edicion de `estado_instrumento` y de `regimen_reforma_659` no esta disponible en ningun permiso de la tabla de la seccion C; solo el Editor de contenido regulatorio del proveedor, fuera del RBAC de la organizacion cliente, puede modificarlos.

---

## Q. MVP

| Funcionalidad del modulo | MUST | SHOULD | COULD | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Marco normativo consultable (instrumentos con estado VIGENTE/FUTURO/DEROGADO/MODIFICADO, fuente y fecha de consulta) | X | | | | Nucleo del modulo (mapa definitivo, seccion 3); sin el, ningun otro modulo tiene donde consultar que version de la ley esta vigente |
| Bandera `regimen_reforma_659` con interruptor manual, registro de fecha y notificacion a cada organizacion | X | | | | Pieza central del diseno de doble estado (decision 2.7.16); MOD-002 y MOD-011, ambos MUST HAVE, dependen de ella desde el primer dia |
| Catalogo de infracciones y multas (Art. 56 y 57), informativo | X | | | | Cobertura parcial ya documentada en `06_mapa_definitivo_de_modulos.md`: se muestra desde el MVP aunque el flujo operativo completo se difiera; OBL-SANC-01 es OBLIGATORIO sin condicion |
| Registro basico de tramites ante la ACE (ACEFiling), incluida la recepcion automatica de eventos desde MOD-002 y MOD-010 | X | | | | Bajo costo de implementacion; dependencia estructural de OBL-DPO-03 (MOD-002) y OBL-TRANSF-05 (MOD-010), ambas con plazo legal ya corriendo y ambas MUST HAVE |
| Tarea automatica de revision al publicarse una actualizacion normativa o al cambiar la bandera | X | | | | Bajo costo, alto valor: sin ella, un cambio normativo no llega a ningun responsable concreto |
| Registro manual de un expediente de Procedimiento Sancionador (datos basicos, contestacion, resultado) con contadores de plazo | | X | | | Las 9 obligaciones SANC son mayormente CONDICIONAL: solo se activan si la ACE abre un caso; la mayoria de organizaciones cliente no tendra un expediente activo en sus primeros meses de uso |
| Flujo operativo completo del Procedimiento Sancionador (vias simplificada/ordinaria, medidas provisionales, recursos, seguimiento de medidas adicionales) | | X | | | Depende de la profundidad de casuistica (Normativa PAS, 49 articulos); el MVP puede operar con el registro manual anterior y anadir el flujo completo de estados cuando el primer caso real lo exija |
| Observatorio de publicidad de resoluciones sancionatorias de la ACE (OBL-SANC-08) | | | X | | RECOMENDADO/CONDICIONAL, sin resoluciones publicadas por la ACE a la fecha de este analisis; mejora de contexto, no bloquea ninguna obligacion propia de la empresa |
| Historial propio de sanciones, apercibimientos y medidas recibidas (RECOMENDADO, buena practica) | | | X | | Sin base legal expresa de reincidencia (seccion 9 de `sweep_sanciones_procedimiento.md`); util para gestion de riesgo interno, no urgente |
| Certificaciones o sellos de proteccion de datos (OBL-AUD-02) | | | | X | RECOMENDADO y sin mecanismo habilitado por la ACE a la fecha de este analisis; el modulo solo puede, como mucho, recordar que la facultad existe |
| Integracion automatica completa entre ACEFiling y el modulo de origen (por ejemplo, cierre automatico al recibir acuse de la ACE) | | | X | | Depende de que la ACE habilite canales oficiales; mientras tanto, el registro manual de acuses (seccion D.4) cubre la necesidad |

**Conclusion MVP:** la version minima vendible de MOD-024 cubre el marco normativo consultable con sus cuatro estados, la bandera de doble estado con su interruptor manual y su notificacion a cada organizacion, el catalogo informativo de infracciones y multas, el registro basico de tramites ante la ACE (incluida la recepcion automatica desde MOD-002 y MOD-010) y la tarea automatica de revision ante cualquier cambio normativo. Estas piezas son las que el mapa definitivo exige como nucleo MUST HAVE (`06_mapa_definitivo_de_modulos.md`, seccion 3, ficha de MOD-024) porque otros modulos MUST HAVE (MOD-002, MOD-007, MOD-010, MOD-011, MOD-015, MOD-017) dependen de ellas desde el primer dia de uso del sistema. El flujo operativo completo del Procedimiento Sancionador queda como SHOULD HAVE porque sus obligaciones son mayormente condicionales a que la ACE efectivamente abra un caso; mientras tanto, el registro manual basico ya permite documentar un expediente real si llegara a presentarse.

---

## R. Ayuda contextual (complemento obligatorio)

**1. Marco normativo consultable**
- Que es: la lista de leyes, normativas, lineamientos y politicas de la ACE que aplican a la proteccion de datos personales en El Salvador, con un indicador de si cada una esta vigente, si entrara en vigencia mas adelante, si ya fue derogada o si fue modificada.
- Por que tengo que hacer esto: para saber, en cualquier momento, cual es la version de la ley que su empresa debe seguir hoy, sin tener que rastrear el Diario Oficial por su cuenta.
- Fundamento: regla 4 de las reglas no negociables de este blueprint (distinguir ley, normativa ACE, lineamientos, politicas de actuacion y buena practica); contenido gestionado con revision juridica interna del proveedor.
- Cuando necesito ayuda juridica: si necesita aplicar una norma a un caso especifico de su empresa, o si dos disposiciones parecen contradecirse, consulte a su asesoria legal.

**2. Actualizaciones normativas**
- Que es: el aviso que recibe su empresa cada vez que una norma que le aplica cambia, explicando que cambio, a que obligaciones y modulos afecta, y que debe revisar.
- Por que tengo que hacer esto: una norma que cambia sin que nadie se entere puede dejar a su empresa cumpliendo una regla que ya no aplica, o incumpliendo una nueva sin saberlo.
- Fundamento: hipotesis de `PROMPT_BASE...md`, seccion 41 ("Actualizacion normativa"), convertida en diseno funcional de este modulo.
- Cuando necesito ayuda juridica: si el cambio afecta un proceso ya en curso en su empresa (por ejemplo, un aviso de privacidad publicado) y no esta segura si debe republicarlo, consulte a su asesoria legal.

**3. Doble estado de la reforma 659**
- Que es: el interruptor que muestra si hoy aplica la ley vigente (Delegado obligatorio en el sector privado) o si ya aplica la reforma que aprobo la Asamblea Legislativa (Delegado ya no obligatorio), una vez que esa reforma se confirme publicada oficialmente.
- Por que tengo que hacer esto: mientras el sistema muestre el estado ACTUAL, su empresa debe seguir cumpliendo las obligaciones de hoy; el sistema le avisara con claridad si esto cambia, y nunca activara el nuevo estado por su cuenta.
- Fundamento: OBL-PLAZO-05; Decreto Legislativo 659, segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado.
- Cuando necesito ayuda juridica: si necesita decidir el impacto especifico del cambio de regimen en su empresa (por ejemplo, si mantiene o no a su Delegado), consulte a su asesoria legal.

**4. Procedimiento Sancionador**
- Que es: el proceso mediante el cual la Agencia de Ciberseguridad del Estado investiga y, si corresponde, sanciona a una empresa por una infraccion a la Ley para la Proteccion de Datos Personales, con pasos y plazos fijos (por ejemplo, 5 dias habiles para contestar un emplazamiento).
- Por que tengo que hacer esto: si su empresa recibe una notificacion de la ACE, los plazos para responder son cortos y su incumplimiento puede agravar la situacion; este modulo calcula esos plazos y organiza el expediente para que no se pierda ningun paso.
- Fundamento: OBL-SANC-01 a OBL-SANC-09; Arts. 53 a 59 de la Ley para la Proteccion de Datos Personales; Normativa para el Procedimiento Administrativo Sancionador de la ACE.
- Cuando necesito ayuda juridica: en cuanto reciba cualquier notificacion de un procedimiento sancionador, consulte a su asesoria legal antes de decidir su respuesta; el sistema organiza el expediente y calcula plazos, pero no decide su estrategia de defensa.

**5. Multas orientativas**
- Que es: el rango de multa (en salarios minimos y su equivalente en dolares) que la ley fija para cada categoria de infraccion (leve, grave, muy grave).
- Por que tengo que hacer esto: para entender la magnitud del riesgo economico de una infraccion, sin que esto signifique que el sistema esta prediciendo cuanto le costaria a su empresa un caso especifico.
- Fundamento: OBL-SANC-02, Art. 57 de la Ley para la Proteccion de Datos Personales; Decreto Ejecutivo del salario minimo vigente.
- Cuando necesito ayuda juridica: siempre que este frente a un caso real; la graduacion exacta de una multa es facultad exclusiva de la ACE y depende de criterios que solo un abogado puede ayudarle a evaluar.

**6. Tramites ante la ACE**
- Que es: los envios que la ley exige que su empresa haga hacia la Agencia de Ciberseguridad del Estado, como comunicar el nombramiento de su Delegado o poner en conocimiento una transferencia internacional de datos.
- Por que tengo que hacer esto: son obligaciones legales independientes de documentar internamente el tramite; sin un registro de que se envio y cuando, su empresa no puede demostrar que informo a la autoridad cuando correspondia.
- Fundamento: OBL-DPO-01 (via MOD-002), OBL-TRANSF-05 (via MOD-010), OBL-AUD-02; Arts. 15, 17 y 45 de la Ley para la Proteccion de Datos Personales.
- Cuando necesito ayuda juridica: si la ACE rechaza un tramite, o si no existe un canal oficial habilitado para enviarlo, consulte a su asesoria legal para decidir los siguientes pasos; el sistema deja constancia del intento, pero no presenta el tramite en su nombre.

---

## Nota final del agente (desacuerdos y observaciones sobre las fuentes de diseno)

1. **Discrepancia de dependencias con `mapa_modulos.json` (detallada en la seccion L).** El campo `depende_de` de MOD-024 esta vacio, pero dos fichas ya escritas y mutuamente consistentes (MOD-002 y MOD-010) declaran de forma explicita que envian eventos hacia este modulo (el tramite de nombramiento del Delegado y el borrador de puesta en conocimiento de una transferencia, respectivamente). Esta ficha modela esa dependencia real en vez de contradecir dos fichas ya escritas que coinciden entre si, y recomienda que una proxima revision de `mapa_modulos.json` agregue "MOD-002" y "MOD-010" al `depende_de` de MOD-024, y "MOD-024" al `alimenta_a` de ambos.
2. **Precision sobre la obligacion colaboradora OBL-DPO-01 (no OBL-DPO-03).** La lista de obligaciones colaboradoras de MOD-024 en `mapa_modulos.json` cita OBL-DPO-01 (obligatoriedad de nombrar delegado), no OBL-DPO-03 (comunicacion del nombramiento a la ACE en 15 dias habiles, propietario MOD-002). Esta ficha respeta esa lista tal como esta y la interpreta de forma coherente: MOD-024 colabora con OBL-DPO-01 mostrando, dentro del marco normativo consultable, si esa obligacion sigue vigente segun el regimen activo de la bandera; el tramite operativo de comunicacion en si (OBL-DPO-03) sigue siendo propiedad exclusiva de MOD-002, y este modulo solo aloja el registro pasivo de ese tramite (ACEFiling) sin ser su colaborador declarado en la matriz. Se deja esta precision por si una futura revision de la matriz considera mas exacto anadir OBL-DPO-03 a la lista de colaboradoras de MOD-024.
3. **Numero del decreto de reforma.** Toda referencia al "Decreto Legislativo 659" en esta ficha sigue la decision 2.7.32 de `02_validacion_de_la_idea.md`: se cita segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado, porque la investigacion juridica (incertidumbre 13 de `01_legal/03_hallazgos_regulatorios.md`, seccion 9) reporta cifras contradictorias para el numero exacto del decreto.
4. **Alcance de "Gobierno del contenido normativo" fuera del RBAC de la organizacion cliente.** El enfoque especifico de la tarea pide modelar "un rol interno del proveedor (editor de contenido regulatorio con revision juridica)". Esta ficha lo documenta en la seccion B como una nota aparte, explicitamente fuera de la tabla de permisos de la seccion C, porque los 12 roles estandar de `05_tipos_de_usuario.md` seccion 5.3 son todos roles de la organizacion cliente, y mezclarlos habria violado la regla 7 de las reglas no negociables (usar los roles estandar con sus nombres exactos). Si una futura revision del blueprint decide modelar formalmente el lado "proveedor" del sistema (por ejemplo, para una seccion transversal de gobierno de contenido), esta nota puede servir de punto de partida.
5. **No se agrega una arista directa MOD-024 -> MOD-005 en el mapa.** `03_modulos/MOD-005_ficha.md` (nota final, punto 2) recomienda que una proxima revision del mapa considere una arista directa entre MOD-024 y MOD-005 para el recalculo del Plan de Cumplimiento ante un cambio normativo. Esta ficha no la agrega, por coherencia con el `alimenta_a` real de `mapa_modulos.json` (que no incluye MOD-005) y para no introducir una segunda discrepancia no solicitada por el enfoque especifico de esta tarea; se deja la recomendacion en manos de quien mantenga el mapa definitivo.
6. **Los 11 articulos y referencias citados por la matriz para OBL-AUD-02, OBL-PLAZO-05 y OBL-SANC-01 a 09 coinciden con el texto de las fuentes primarias y secundarias locales revisadas para esta ficha,** y no se detecto ninguna otra inconsistencia material entre el proposito, las obligaciones propietarias y colaboradoras, y las dependencias de MOD-024 tal como estan documentadas en `mapa_modulos.json` y `06_mapa_definitivo_de_modulos.md`, y el contenido articulado de la Ley para la Proteccion de Datos Personales (Arts. 50, 53 y 55 a 59), la Normativa para el Procedimiento Administrativo Sancionador de la ACE (49 articulos, verificada contra imagenes OCR) y `01_legal/sweep_sanciones_procedimiento.md`, salvo la discrepancia sobre `alimenta_a` con MOD-008 que se documenta en el punto 7.
7. **Correccion aplicada tras revision adversarial: MOD-008 se agrega a los receptores del evento "cambio de bandera" (secciones G y L); MOD-016 no se agrega.** `MOD-008_ficha.md` (seccion G, regla 3) ya declaraba, antes de esta correccion, una automatizacion propia disparada por el cambio de esta bandera; esta ficha no lo reflejaba en su propia lista de receptores del evento (secciones E, F.1, G y L), a pesar de que `mapa_modulos.json` tampoco declara esa arista en el `alimenta_a` de MOD-024 (misma naturaleza que la discrepancia del punto 1, ahora en sentido inverso). Se corrige agregando MOD-008 en las secciones E, F.1, G (regla 1) y L, con la discrepancia senalada, no corregida sobre `mapa_modulos.json`. En cambio, no se agrega MOD-016 a esa misma lista: `MOD-016_ficha.md` describe su relacion con la bandera como una consulta de referencia bajo demanda para texto de ayuda contextual (no como una automatizacion propia disparada por el evento, y su propia seccion G no tiene ninguna regla con ese disparador), patron que ya cubre la automatizacion 9 de la seccion G de esta ficha; agregar MOD-016 a la lista de receptores del evento duplicaria, sin necesidad funcional, un mecanismo de consulta que ya existe. Ademas: se aclaro en D.2 y F.1 que EN_VERIFICACION es un estado del campo tecnico interno `estado_interno_verificacion_659`, no un tercer valor de la bandera `regimen_reforma_659` (que conserva solo ACTUAL y FUTURO); se preciso en G (regla 1) y F.1 que lo que se actualiza es el `estado_instrumento` del instrumento normativo relacionado con cada obligacion afectada (D.1), no un campo propio de la obligacion, que la tabla D no define; se aclaro en D.4 que los seis estados de `estado_tramite` son el modelo completo y que `MOD-010_ficha.md` muestra una simplificacion de lectura de cuatro, sin modificar ese otro archivo; y se retiro la cita de un numero de inciso no verificable ("Art. 32 inc. 3") en D.3, dejando solo "Art. 32" con la incertidumbre senalada, conforme a la regla de no inventar articulos ni incisos.
