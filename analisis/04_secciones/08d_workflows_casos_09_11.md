## Caso 9. Ocurre una brecha de datos

Caso con profundidad especial. Fuente principal: `03_modulos/MOD-013_ficha.md` (leida completa), cruzada con `03_modulos/MOD-023_ficha.md` (Calendario y Motor de Plazos, computo de las 72 horas) y `03_modulos/MOD-009_ficha.md` (Proveedores y Encargados, rol del proveedor de origen).

### Situacion de partida

Avicola San Andres, S.A. de C.V. (empresa mediana, aprox. 300 empleados) tiene contratado, desde hace dos anos, un proveedor de nomina en la nube que procesa datos de sus 300 empleados (identificacion, cuenta bancaria de deposito de salario y, para quienes tienen seguro medico colectivo, categoria de afiliacion de salud). Ese proveedor esta registrado en MOD-009 Proveedores y Encargados como Encargado, en estado ACTIVO, con contrato/DPA vigente y con una clausula de aviso de incidentes que fija un plazo interno de 24 horas para que el proveedor notifique a Avicola cualquier vulneracion (referencia informativa, `sweep_encargados_transferencias.md` seccion 5.6). Jorge Alberto Menendez Rauda ejerce el rol de Delegado de Proteccion de Datos interno (perfil 2 de `05_tipos_de_usuario.md`, seccion 5.1); Roberto Antonio Villalta ejerce el rol de Responsable de Seguridad / IT (perfil 4); Daniela Patricia Cornejo Lazo, Coordinadora de RRHH, ejerce el rol de Responsable de area para el tratamiento de nomina (perfil 3).

### Disparador

El proveedor de nomina envia un correo a Roberto Villalta informando que detecto un acceso no autorizado a la base de datos de nomina durante el fin de semana anterior, y que no puede confirmar todavia el alcance exacto. No es una alerta generada por el software (MOD-013 no detecta incidentes por si mismo, es un anti-feature declarado en la ficha): es un aviso humano externo que un usuario debe registrar.

### Actores y modulos que intervienen

| Rol estandar (05_tipos_de_usuario.md 5.3) | Participacion en este caso |
|---|---|
| Responsable de Seguridad / IT | Registra el incidente, ejecuta triage, contencion e investigacion, prepara los borradores de notificacion |
| Delegado de Proteccion de Datos (o Responsable interno) | Aprueba y marca como enviada cada notificacion externa; co-decide si corresponde notificar |
| Responsable Legal / Compliance | Co-revisa la decision de notificar y el contenido cuando hay riesgo, participa en el cierre en un caso sensible |
| Responsable de area (RRHH) | Aporta la lista de empleados afectados y el detalle de las categorias de dato de nomina y salud |
| Administrador de la organizacion | Recibe las alertas de escalamiento de los dos cronometros de 72 horas, ve el caso en el dashboard |
| Aprobador | Firma como segunda persona el cierre del caso, porque Avicola (300 empleados) supera el umbral configurable de separacion de funciones (propuesta inicial 50 empleados) |
| Auditor (interno) | Solo lectura del expediente cerrado, como parte de la auditoria anual (Caso 10) |
| Titular (formulario externo) | No usa el modulo; solo recibe la notificacion externa por el canal disponible (correo) |

| Modulo | Codigo | Papel en este caso |
|---|---|---|
| Incidentes de Seguridad | MOD-013 | Propietario del caso; gestiona todo el ciclo de vida del expediente |
| Calendario y Motor de Plazos | MOD-023 | Calcula ambos cronometros de 72 horas en horas corridas (criterio por defecto) |
| Proveedores y Encargados | MOD-009 | Registra al proveedor de origen; se suspende automaticamente si la severidad es Alta o Critica |
| RAT y Mapa de Datos | MOD-006 | Identifica el tratamiento de nomina y confirma si el dato de salud ya estaba marcado como sensible |
| Controles de Seguridad | MOD-015 | Recibe las medidas correctivas definitivas como Control nuevo o reforzado |
| Riesgos y EIPD | MOD-014 | Recibe la tarea de evaluar si corresponde EIPD (dato de salud involucrado) |
| Centro de Tareas | MOD-021 | Aloja las tareas automaticas del caso (iniciar revision, notificar, documentar) |
| Notificaciones | MOD-022 | Canal de las alertas internas de cronometro |
| Centro de Evidencias | MOD-019 | Recibe el expediente completo y las constancias de envio con verificacion de integridad |
| Retencion y Eliminacion | MOD-016 | Colaboradora: calcula el plazo minimo recomendado de conservacion del expediente cerrado (SHOULD HAVE, ver Cobertura por version) |
| Dashboard y Reportes | MOD-020 | Muestra el indicador de incidentes abiertos y de cronometros por vencer |
| Centro Regulatorio | MOD-024 | Referencia constante de la bandera de infraestructura critica del Decreto 143, si aplicara |

### Diagrama ASCII del recorrido de extremo a extremo

```
Proveedor de nomina                Roberto (Seg/IT)         Jorge (Delegado)          MOD-023 / MOD-021 / MOD-019
        |                                |                        |                              |
        | avisa acceso no autorizado     |                        |                              |
        +------------------------------->|                        |                              |
                                          | registra incidente     |                              |
                                          | (MOD-013: REPORTADO)   |                              |
                                          |----------------------->|                              |
                                          | confirma fecha de      |                              |
                                          | conocimiento            |                              |
                                          |------------------------------------------------------->|
                                          |                        |         arrancan los dos cronometros
                                          |                        |         de 72h (notificacion y revision)
                                          v                        |                              |
                                    [TRIAGE]                       |                              |
                                          |                        |                              |
                             es vulneracion = Si (decision humana)  |                              |
                                          v                        |                              |
                                  [INVESTIGACION] --inicia revision exhaustiva (<=72h)------------>|
                                          v                        |                              |
                                  [CONTENCION] (bitacora de acciones)                              |
                                          v                        |                              |
                                  [EVALUACION] --riesgo=Si, dato de salud--> tarea EIPD a MOD-014   |
                                          v                        |                              |
                                     [DECISION] <-------- co-revision Delegado + Legal ------------|
                                          |                        |                              |
                                genera borradores ACE/FGR y titulares                              |
                                          |                        |                              |
                                          v                        v                              |
                                  [NOTIFICACION] <-- aprueba y marca enviado (<=72h) ---------------|
                                          |                        |                              |
                                          |            paralelo: MOD-009 suspende al proveedor       |
                                          |            (severidad Alta/Critica)                     |
                                          v                        |                              |
                                  [REMEDIACION] --medida correctiva--> Control en MOD-015          |
                                          v                        |                              |
                                     [CIERRE] <-- segunda firma del Aprobador (>50 empleados) ------|
                                          |                                                         |
                                          +-------------------------------------------------------->|
                                                                        expediente + constancias con hash
                                                                        a MOD-019; fecha de conservacion
                                                                        (cierre + 5 anos recomendados) a MOD-016
```

### Paso a paso

| Paso | Quien | Modulo | Que hace en el sistema | Que genera | Plazo y como se calcula | Fundamento |
|---|---|---|---|---|---|---|
| 1 | Responsable de Seguridad/IT | MOD-013 | Reporta el incidente: titulo, fecha de deteccion, quien reporta, origen = Proveedor/Encargado, vincula al proveedor en MOD-009 | Expediente creado (estado Reportado); evento de auditoria | Sin plazo aun: los cronometros no arrancan hasta registrar la fecha de conocimiento | Buena practica (OBL-INC-04 en preparacion) |
| 2 | Responsable de Seguridad/IT | MOD-013 / MOD-023 | Confirma la fecha y hora de conocimiento (criterio: el momento mas temprano en que se pudo concluir razonablemente que hubo vulneracion) | Arrancan en paralelo los dos cronometros de 72h; tareas "iniciar revision antes de..." y "notificar antes de..." en MOD-021; alerta INFO | 72 horas desde el conocimiento, en horas corridas por defecto (MOD-023, criterio conservador, editable con doble control) | OBL-INC-01, OBL-INC-02 (Art. 25 LPDP) |
| 3 | Responsable de Seguridad/IT (con apoyo del Delegado) | MOD-013 | Marca "Es vulneracion de datos personales = Si", con tipo de vulneracion (acceso ilegitimo) y categorias de datos (identificacion, financiera, salud) | Pasa a estado Investigacion; se marca automaticamente "incluye datos sensibles = Si" por la categoria salud | Sin plazo propio; decision humana no automatizable (ver seccion siguiente) | Decision no automatizable; base OBL-INC-01 |
| 4 | Responsable de Seguridad/IT | MOD-013 / MOD-023 | Registra la fecha de inicio de la revision exhaustiva | Si se registra despues de 72h desde el conocimiento, el hito queda marcado como vencido en el historial de forma permanente, sin bloquear el caso | Debe iniciar (no concluir) dentro de las 72 horas desde el conocimiento | OBL-INC-02 (Art. 25 inc. 2) |
| 5 | Responsable de Seguridad/IT | MOD-013 | Registra al menos una accion de contencion (por ejemplo: se exige al proveedor rotar credenciales y cerrar el acceso comprometido) | Bitacora de contencion con fecha y usuario | Sin plazo propio; puede iniciar desde Reportado | OBL-INC-03 lit. c) |
| 6 | Responsable de Seguridad/IT + Responsable de area (RRHH) | MOD-013 / MOD-006 | Completa evaluacion: cantidad estimada de titulares afectados (300, todo el personal con nomina en ese sistema), impacto estimado, y marca "existe riesgo en la seguridad de los datos = Si" | Si "riesgo = Si", se bloquea el avance a Decision hasta completar los campos de OBL-INC-04; si el tratamiento de nomina no tenia EIPD, se crea tarea hacia MOD-014 | Sin plazo propio; debe completarse antes de Decision | OBL-INC-04; decision de riesgo no automatizable |
| 7 | Delegado + Responsable Legal/Compliance (co-revision) | MOD-013 | Decide, con justificacion documentada, que si corresponde notificar externamente (caso involucra datos financieros y de salud de 300 personas) | Evento de auditoria de la decision, visible para cualquier auditoria posterior de la ACE | Sin plazo propio; decision humana explicita, nunca automatica | Art. 25 LPDP; decision no automatizable |
| 8 | Responsable de Seguridad/IT (prepara) | MOD-013 | Completa naturaleza del incidente, datos comprometidos, acciones correctivas inmediatas, recomendaciones al titular y medios de contacto | Se generan automaticamente dos borradores: notificacion a ACE/FGR (5 elementos) y notificacion a titulares (4 elementos, sin acciones correctivas internas) | Antes de vencer las 72h | OBL-INC-03 (Art. 25 incs. 3 y 4) |
| 9 | Delegado | MOD-013 | Aprueba y marca como enviada la notificacion a la ACE y a la Fiscalia General de la Republica | Constancia de envio con fecha, hora, canal y hash de integridad, hacia MOD-019 | Dentro de las 72 horas desde el conocimiento; si se envia despues, el sistema no bloquea el envio pero marca el hito como vencido de forma permanente | OBL-INC-01, OBL-INC-03 |
| 10 | Delegado | MOD-013 | Aprueba y marca como enviada la notificacion a los 300 titulares afectados (por correo, canal disponible desde el MVP) | Constancia de envio por lote, con hash de integridad | Mismo plazo de 72 horas | OBL-INC-01, OBL-INC-03 |
| 11 | Responsable de Seguridad/IT | MOD-009 | Consulta si el proveedor aviso dentro del plazo interno pactado de 24 horas; si no hay evidencia de aviso a tiempo, el sistema emite alerta WARNING | Alerta informativa; no bloquea el caso | Referencia informativa, no plazo legal exigible por si mismo (el contrato especifico es el que fija el plazo real) | Buena practica, `sweep_encargados_transferencias.md` seccion 5.6 |
| 11b | Sistema (automatico) | MOD-009 | Si la severidad del incidente vinculado es Alta o Critica, el proveedor pasa automaticamente de ACTIVO a SUSPENDIDO | Notificacion a Responsable de Seguridad, Delegado y Administrador; advertencia operativa de no enviar mas datos al proveedor (sin bloqueo tecnico) | Inmediato al vincular la severidad | Automatizacion 11 de MOD-009 |
| 12 | Responsable de Seguridad/IT | MOD-013 | Registra medidas correctivas definitivas (por ejemplo, exigir 2FA en el acceso del proveedor) y confirma si se requiere actualizar la politica de seguridad | Enlaza o crea Control en MOD-015; si corresponde, tarea de actualizacion de politica hacia MOD-008 | Antes de Cierre | OBL-INC-02 |
| 13 | Responsable de Seguridad/IT o Delegado, con segunda firma del Aprobador | MOD-013 | Completa la decision final de cierre (Resuelto con notificacion enviada) y su justificacion | Calcula la fecha de conservacion del expediente (cierre + minimo recomendado 5 anos, OBL-RET-05) y la envia a MOD-016; el expediente queda de solo lectura | Avicola (300 empleados) supera el umbral de 50, por lo que el cierre exige la segunda firma del Aprobador (separacion de funciones) | OBL-INC-04, OBL-PRIN-03; `05_tipos_de_usuario.md` 5.4 |
| 14 | Delegado, tras verificar medidas correctivas | MOD-009 | Decide si reactivar al proveedor (ACTIVO) o terminar la relacion (RELACION_FINALIZADA) | Evento de auditoria "reactivado tras suspension", o tarea de verificacion de devolucion/eliminacion de datos si se termina la relacion | Sin plazo legal propio; decision de negocio de la empresa | Buena practica; OBL-PROV-07 si se termina la relacion |
| 15 | Sistema (automatico) | MOD-019 | Consolida el expediente completo, la bitacora y las constancias de notificacion como paquete de evidencia con verificacion de integridad | Evidencia disponible para el Auditor y para una eventual auditoria anual (Caso 10) | Se genera al cerrar el caso | OBL-PRIN-03; anti-feature 25 |

### Decisiones que el sistema NO toma

El sistema muestra siempre el texto "Requiere validacion de la organizacion o asesoria especializada" junto a cada una de estas decisiones (MOD-013, seccion H):

1. Calificar si el aviso del proveedor describe realmente una "vulneracion de seguridad de datos personales" bajo el Art. 25: el sistema exige que una persona lo confirme o lo descarte con justificacion.
2. Determinar si existe "riesgo en la seguridad de los datos personales" para efectos del deber reforzado de documentacion (OBL-INC-04): no hay un score automatico que sustituya este juicio.
3. Decidir el contenido final y el momento exacto de envio de cada notificacion, en particular si la investigacion no ha concluido al llegar a las 72 horas.
4. Cambiar el criterio de computo del plazo de 72 horas (de horas corridas a horas habiles); el sistema aplica por defecto el criterio conservador y muestra siempre: "La ley no precisa si este plazo se cuenta en horas corridas u horas habiles. El sistema aplica por defecto el criterio mas conservador. Verifique este criterio con asesoria legal si el caso es critico."
5. Aprobar el envio de cualquier notificacion externa a la ACE, a la FGR o a los titulares: siempre requiere la aprobacion explicita y trazable del Delegado, con el texto "Documento generado como borrador a partir de la informacion registrada. Requiere revision y aprobacion de su organizacion antes de usarse, y puede requerir validacion de asesoria legal especializada."
6. Decidir la decision final de cierre del caso y si las medidas correctivas fueron suficientes.
7. Determinar si el proveedor de nomina incumplio su obligacion contractual de aviso oportuno (es una cuestion contractual y comercial, no algo que el sistema resuelva).

### Alertas y escalamientos

| Alerta | Disparador | Nivel | Destinatario | Escalamiento |
|---|---|---|---|---|
| Cronometro de notificacion, aviso temprano | 50% del plazo (24h) consumido sin notificacion enviada | WARNING | Responsable de Seguridad/IT, Delegado | A Administrador si no hay accion en 6 horas |
| Cronometro de notificacion, critico | Faltan 6 horas para vencer sin notificacion enviada | CRITICAL | Delegado, Administrador, Aprobador | Inmediato a Gerencia (perspectiva Administrador del dashboard) |
| Plazo de notificacion vencido | 72 horas cumplidas sin notificacion enviada | CRITICAL | Administrador, Delegado, Legal | Diaria hasta resolverse; el incumplimiento queda marcado de forma permanente aunque se notifique despues |
| Cronometro de revision, inicio pendiente | 60 horas transcurridas sin marcar inicio de la revision exhaustiva | WARNING | Responsable de Seguridad/IT | A Delegado a las 70 horas |
| Documentacion incompleta con riesgo confirmado | Se intenta avanzar a Decision con riesgo=Si y campos de OBL-INC-04 incompletos | HIGH (bloqueante) | Responsable de Seguridad/IT | No aplica, es un bloqueo, no un escalamiento |
| Incidente en proveedor sin evidencia de aviso | Origen=Proveedor y no hay registro de aviso dentro del plazo pactado | WARNING | Responsable de Seguridad/IT, Responsable de Proveedores | A Legal si transcurre el 80% del plazo total de 72h |
| Incidente de seguridad grave vinculado (en MOD-009) | Severidad Alta o Critica vinculada al proveedor | CRITICAL | Delegado, Responsable de Seguridad/IT, Administrador | Notifica tambien al Aprobador |

### Evidencia resultante

Vive en MOD-019 Centro de Evidencias, referenciada desde el expediente de MOD-013:

- Expediente completo versionado (todos los campos, con valor anterior y nuevo de cada cambio), prueba de OBL-INC-04.
- Bitacora de deteccion y conocimiento, registro inmutable de solo adicion, prueba del inicio de ambos plazos de 72 horas (OBL-INC-01, OBL-INC-02).
- Constancia de envio de cada notificacion (ACE/FGR y titulares), con hash de integridad verificable, prueba de OBL-INC-01 y OBL-INC-03.
- Registro de aprobacion del Delegado para cada notificacion, prueba de OBL-PRIN-03.
- Bitacora de contencion y hallazgos de la revision exhaustiva.
- Registro de la decision de cierre, con la segunda firma del Aprobador (Avicola supera el umbral de 50 empleados).
- Historial de cualquier vencimiento, si lo hubo, como marca permanente no eliminable.

Conservacion: minimo recomendado de 5 anos desde el cierre (OBL-RET-05, RECOMENDADO, sin norma expresa que fije ese numero; requiere validacion de asesoria legal), calculado por MOD-013 al cerrar el caso y enviado a MOD-016.

### Variantes y casos borde

- **Pyme con una persona en varios roles.** En Ferreteria y Suministros El Roble (aprox. 30 empleados, por debajo del umbral de 50), Karla Beatriz Hernandez Mejia acumula Administradora y Delegada. Puede investigar, decidir y cerrar el mismo caso sin una segunda firma, pero el sistema muestra siempre la advertencia visible de "autorrevision" en el cierre (no bloquea, solo advierte). La aprobacion de la notificacion externa sigue exigiendo la accion explicita del rol Delegado, aunque sea la misma persona que redacto el borrador.
- **Grupo corporativo.** En Grupo Financiero Itzalco, si el incidente ocurre en una de las sociedades (por ejemplo, la aseguradora), el expediente y sus cronometros son propios de esa sociedad; una vision consolidada del incidente a nivel de todo el grupo es funcionalidad V1/Enterprise, no MVP (`02_validacion_de_la_idea.md`, decision 2.7.31), de modo que Ana Gabriela Reyes Portillo (Directora de Cumplimiento Corporativo) revisaria el caso entrando a la organizacion de esa sociedad especifica, no desde una vista unica de grupo.
- **Doble estado de la reforma 659.** El Art. 25 LPDP atribuye el deber de notificar al "responsable" (la empresa), no al Delegado, por lo que ninguna de las cinco obligaciones propietarias de MOD-013 depende de la bandera de MOD-024. Lo unico que cambiaria, si el estado FUTURO se activa, es quien aprueba y firma la notificacion por defecto: pasaria del Delegado al Responsable interno configurable en MOD-002, sin alterar plazos ni contenido.
- **Una persona (Responsable de Seguridad/IT, Delegado o Legal) marca en Triage que no es una vulneracion, con justificacion obligatoria.** El caso pasa a Descartado (estado terminal, reabribile con justificacion); ambos cronometros se detienen y el motivo queda en el historial, visible para Auditor.
- **Se vence el plazo de notificacion sin enviar.** El sistema no bloquea el envio posterior, pero marca el hito como vencido de forma permanente e irreversible en el historial; el incumplimiento queda documentado en vez de ocultado.
- **La empresa decide no notificar externamente, de forma justificada.** El caso pasa a "Cierre sin notificacion externa (justificado)"; exige una justificacion de al menos 20 caracteres y queda marcado explicitamente en reportes.

### Cobertura por version

| Funcionalidad | MVP | V1 / V2 |
|---|---|---|
| Flujo completo de un incidente de origen interno, dos cronometros de 72h, plantillas diferenciadas de notificacion, documentacion obligatoria bloqueante | MUST HAVE | - |
| Referencia informativa al proveedor de origen (MOD-009) y su plazo pactado de aviso | SHOULD HAVE (disponible pero no bloqueante en el primer ano) | - |
| Creacion automatica de tarea de EIPD hacia MOD-014 con cuestionario de scoring completo | Se crea igual una tarea generica en el MVP | El cuestionario de scoring completo depende de que MOD-014 (SHOULD HAVE) este activo |
| Calculo de la fecha de conservacion del expediente y archivado automatico al vencer | Se calcula la fecha, pero el archivado automatico y las alertas de vencimiento dependen de MOD-016 (SHOULD HAVE); mientras tanto, el expediente simplemente no se puede borrar por defecto (cobertura pasiva) | Motor de retencion completo con alerta y flujo de excepcion |
| Flujo condicional del Decreto 143 (infraestructura critica) | Campo disponible, flujo operativo completo puede madurar despues | Plantilla y evidencia especifica ampliada |
| Alertas por canales adicionales (SMS, WhatsApp, Teams, Slack) | No incluido | COULD HAVE, segun MOD-022 |

### Riesgos especificos del caso y su mitigacion

| Riesgo | Mitigacion de diseno |
|---|---|
| Confundir fecha de deteccion con fecha de conocimiento, retrasando el inicio real del cronometro | Dos campos separados y obligatorios, con justificacion exigida si la de conocimiento es posterior a la de deteccion |
| Enviar a los titulares el contenido reservado para la ACE/FGR (acciones correctivas internas) | Generacion automatica de dos plantillas separadas por diseno, nunca una sola plantilla editada a mano |
| Tratar el criterio de horas corridas como la unica interpretacion legal posible | Advertencia de incertidumbre siempre visible; cambiarlo exige doble control (Delegado y Legal) |
| Que la relacion con el proveedor de origen quede documentada de forma incompleta | Campo de referencia al proveedor y alerta especifica si falta evidencia de su aviso dentro del plazo pactado |
| Que el cierre no deje constancia de por que no se notifico, si esa fue la decision | Campo de justificacion obligatorio (minimo 20 caracteres) para "Cierre sin notificacion externa" |
| Exposicion de datos sensibles de los 300 titulares dentro del propio expediente | El expediente registra categorias y cantidades, nunca una copia de la base de nomina comprometida; adjuntos puntuales con controles reforzados |

---

## Caso 10. Se acerca una auditoria

Fuentes principales: `03_modulos/MOD-018_ficha.md` (Auditoria de Cumplimiento), `03_modulos/MOD-019_ficha.md` (Centro de Evidencias), `03_modulos/MOD-015_ficha.md` (Controles de Seguridad), `03_modulos/MOD-020_ficha.md` (Dashboard y Reportes), `03_modulos/MOD-024_ficha.md` (Centro Regulatorio, variante de requerimiento/inspeccion de la ACE), `03_modulos/MOD-001_ficha.md` (invitacion de usuarios externos).

Este caso tiene dos variantes con disparador distinto y, en parte, flujo distinto: la auditoria anual programada por la propia empresa (variante principal) y un requerimiento o inspeccion que inicia la ACE (variante regulatoria, ver "Variantes y casos borde").

### Situacion de partida

Avicola San Andres, S.A. de C.V. (empresa mediana, aprox. 300 empleados) completo su diagnostico inicial y su adecuacion hace poco mas de 11 meses. Jorge Alberto Menendez Rauda, Jefe de Cumplimiento y Riesgo, ejerce el rol de Delegado de Proteccion de Datos interno y esta en proceso de certificacion ante la ACE. Avicola nunca ha cerrado un ciclo formal de auditoria en el sistema: hasta ahora solo contaba con el recordatorio generico del Calendario (MOD-023) anclado a la fecha de adecuacion inicial, y con el registro tecnico automatico (AuditLog) que cada modulo MUST HAVE ya deja desde el primer dia de uso.

### Disparador

El sistema genera automaticamente el recordatorio "corresponde iniciar la auditoria anual de cumplimiento" al cumplirse el periodo configurado (12 meses) desde la fecha de adecuacion inicial (MOD-018, ya que nunca hubo un cierre anterior que sirviera de ancla). Jorge recibe la alerta INFO 60 dias antes de la fecha sugerida.

### Actores y modulos que intervienen

| Rol estandar | Participacion en este caso |
|---|---|
| Delegado de Proteccion de Datos (o Responsable interno) | Coordina el ciclo completo: planifica, registra hallazgos, valida el plan de accion |
| Responsable Legal / Compliance | Co-coordina el ciclo, revisa severidad y redaccion de la conclusion antes del cierre |
| Responsable de Seguridad / IT | Prepara evidencia de sus controles antes de que inicie la auditoria; ejecuta tareas de correccion de hallazgos tecnicos |
| Responsable de area (RRHH, Marketing, Operaciones) | Recibe tareas puntuales de correccion cuando un hallazgo toca un tratamiento de su area |
| Administrador de la organizacion | Ve el semaforo de "estado de la ultima auditoria" en el dashboard; en pyme puede planificar y cerrar (con advertencia) si no hay Delegado o Legal designado |
| Aprobador | Aprueba el cierre de la auditoria (distinto de quien registro los hallazgos) y aprueba cualquier "riesgo aceptado" |
| Auditor (interno) | Solo lectura; revisa el historico de auditorias cerradas como verificacion independiente, nunca registra ni aprueba hallazgos |
| Auditor externo (invitado) | Ing. Francisco Javier Bonilla (perfil 8, `05_tipos_de_usuario.md`): acceso temporal de solo lectura al paquete de evidencias durante la semana de la auditoria |

| Modulo | Codigo | Papel en este caso |
|---|---|---|
| Auditoria de Cumplimiento | MOD-018 | Propietario del ciclo: planificacion, ejecucion, hallazgos, plan de accion, cierre |
| Centro de Evidencias | MOD-019 | Fuente de la evidencia ya acumulada de MOD-006 a MOD-017; recibe el informe cerrado como nueva evidencia (relacion reciproca declarada en `mapa_modulos.json`) |
| Controles de Seguridad | MOD-015 | Precarga el checklist de controles y su estado vigente |
| RAT y Mapa de Datos | MOD-006 | Precarga el listado de tratamientos vigentes como parte del checklist |
| Centro de Tareas | MOD-021 | Aloja una tarea por cada accion del plan de accion |
| Dashboard y Reportes | MOD-020 | Muestra el semaforo de estado de la ultima auditoria y de hallazgos/acciones abiertas |
| Organizacion y Personas | MOD-001 | Invita al auditor externo con acceso temporal acotado |
| Delegado / Responsable Interno de Datos | MOD-002 | Recibe la notificacion de que hay un informe nuevo disponible para su propio informe periodico (OBL-DPO-07) |
| Calendario y Motor de Plazos | MOD-023 | Calcula la fecha del recordatorio anual y los plazos internos de correccion |

### Diagrama ASCII del recorrido de extremo a extremo

```
MOD-023 (recordatorio anual)          Jorge (Delegado)              Roberto (Seg/IT)          MOD-019 / MOD-021
        |                                    |                             |                          |
        | INFO: faltan 60 dias               |                             |                          |
        +----------------------------------->|                             |                          |
                                              | planifica auditoria         |                          |
                                              | (MOD-018: PLANIFICADA)      |                          |
                                              |----------------------------------------------------->  |
                                              | inicia ejecucion            |         precarga checklist
                                              v                             |         (MOD-015, MOD-006)
                                       [EN EJECUCION]                       |                          |
                                              |                             |                          |
                                       revisa checklist, pide evidencia     |                          |
                                              |---------------------------->| aporta evidencia de sus |
                                              |                             | controles (MOD-019)     |
                                              v                             |                          |
                                  [HALLAZGOS EN REVISION] --registra hallazgos con severidad----------->|
                                              v                             |                          |
                                [PLAN DE ACCION EN CURSO] --tarea por accion---------------------------->|
                                              |                                                          |
                                   acciones se corrigen o se aprueba                                     |
                                   riesgo aceptado (Aprobador)                                            |
                                              v                                                          |
                                        [CERRADA] <-- Aprobador confirma el cierre ------------------------
                                              |
                                              +--> informe cerrado con hash a MOD-019
                                              +--> notificacion a MOD-002 (insumo del informe periodico)
                                              +--> recalcula el recordatorio del siguiente ciclo (MOD-023)
```

### Paso a paso

| Paso | Quien | Modulo | Que hace en el sistema | Que genera | Plazo y como se calcula | Fundamento |
|---|---|---|---|---|---|---|
| 1 | Sistema (automatico) | MOD-023 / MOD-018 | Genera el recordatorio "corresponde iniciar la auditoria anual" al cumplirse 12 meses desde la adecuacion inicial | Tarea en MOD-021 y alerta INFO en MOD-022 | 12 meses desde el cierre de la ultima auditoria, o desde la adecuacion inicial si nunca hubo una (periodo configurable) | OBL-AUD-01 (Art. 8 lit. b Politicas de Actuacion ACE) |
| 2 | Delegado | MOD-018 | Planifica la auditoria: titulo, tipo (Interna), periodo cubierto, alcance (obligaciones OBLIGATORIO como punto de partida sugerido) | Registro ComplianceAudit en estado Planificada | Sin plazo propio | Buena practica; alcance no fijado por norma expresa |
| 3 | Delegado | MOD-018 | Inicia ejecucion | Se precarga automaticamente el checklist con los controles vigentes de MOD-015 y los tratamientos vigentes de MOD-006 | Sin plazo propio | Buena practica |
| 4 | Responsable de Seguridad/IT | MOD-015 / MOD-019 | Aporta o confirma la evidencia de sus controles ya cargada (por ejemplo, evidencia de cifrado en transito, backups, control de acceso) | Evidencia ya Disponible en MOD-019, referenciada desde el checklist | Sin plazo propio | OBL-SEG-01 a 06 |
| 5 | Delegado + Responsable Legal/Compliance | MOD-018 | Revisan cada elemento del checklist y registran hallazgos donde corresponda, con severidad (Baja/Media/Alta/Critica) y evidencia del hallazgo | Pasa a Hallazgos en revision; evento de auditoria por cada hallazgo | Sin plazo propio | OBL-AUD-01 |
| 6 | Sistema (automatico) | MOD-018 / MOD-021 | Si un hallazgo tiene severidad Alta o Critica, crea automaticamente una tarea de plan de accion con fecha limite sugerida | Tarea en MOD-021 (15 dias habiles para Critica, 30 para Alta, configurable) | 15 o 30 dias habiles segun severidad, calculado por MOD-023 | Buena practica |
| 7 | Delegado + Responsable Legal/Compliance | MOD-018 | Validan que cada hallazgo tiene al menos una accion correctiva o un riesgo aceptado justificado | Pasa a Plan de accion en curso | Sin plazo propio | OBL-AUD-01 |
| 8 | Responsable de area / Responsable de Seguridad/IT | MOD-021 | Ejecuta la accion correctiva asignada (por ejemplo, actualizar un campo del RAT, renovar evidencia de un control) | Tarea pasa por Pendiente, En proceso, En revision, Aprobada, Completada | Segun la fecha limite asignada a cada accion | Buena practica |
| 9 | Aprobador | MOD-018 | Si una accion no se corrige, aprueba explicitamente el "riesgo aceptado" con justificacion | Evento de auditoria con la justificacion, visible para OBL-PRIN-03 | Sin plazo propio; decision no automatizable | OBL-PRIN-03 |
| 10 | Delegado | MOD-018 | Redacta la conclusion / resumen ejecutivo y adjunta o confirma el informe de auditoria | Habilita el boton de cierre solo cuando todas las acciones estan Corregida o Riesgo aceptado aprobado | Sin plazo propio | OBL-AUD-01 |
| 11 | Aprobador (distinto de quien registro los hallazgos) | MOD-018 | Confirma el cierre de la auditoria | Informe queda en MOD-019 con verificacion de integridad; se recalcula el recordatorio del siguiente ciclo; notificacion a MOD-002 para su informe periodico (OBL-DPO-07) | Cierre disponible solo si no quedan hallazgos Criticos sin resolver | OBL-AUD-01, OBL-PRIN-03 |
| 12 | Administrador | MOD-001 | Invita al auditor externo con acceso temporal de solo lectura, acotado a esta auditoria | Usuario en estado INVITADO, luego ACTIVO al aceptar; cada acceso queda registrado | Ventana de invitacion configurable | Buena practica |
| 13 | Auditor externo (invitado) | MOD-019 / MOD-018 | Revisa el paquete de evidencia exportado con verificacion de integridad; puede comentar y adjuntar su propio informe | Evidencia de la auditoria externa, registrada como evidencia de esta auditoria puntual | Sin plazo propio | Anti-feature 25 |

### Decisiones que el sistema NO toma

1. Si un hallazgo constituye o no una infraccion sancionable ante la ACE: "Requiere validacion de la organizacion o asesoria especializada" (calificar infracciones del Art. 56 es facultad exclusiva de la ACE).
2. La severidad final de un hallazgo: el sistema puede sugerir un valor inicial, pero la persona que registra decide y puede cambiarla.
3. Si el alcance de la auditoria es suficiente o adecuado para ese ciclo: el sistema sugiere las obligaciones OBLIGATORIO como punto de partida, no decide si eso basta.
4. Aceptar un riesgo en vez de corregir un hallazgo ("Riesgo aceptado"): siempre requiere la aprobacion explicita de un segundo usuario con rol Aprobador.
5. Cerrar la auditoria con hallazgos Criticos aun abiertos: el sistema bloquea el boton de cierre en ese caso; forzarlo exige una decision explicita y documentada del Aprobador.
6. Si la empresa deberia contratar una auditoria externa en vez de hacerla internamente: decision de negocio, el sistema no la sugiere ni la exige.
7. Si el historial de auditorias equivale a una certificacion de la ACE (OBL-AUD-02): el sistema nunca usa las palabras "certificacion" ni "sello" dentro de este ciclo, porque la ACE aun no habilito ese mecanismo.

### Alertas y escalamientos

| Alerta | Disparador | Nivel | Destinatario | Escalamiento |
|---|---|---|---|---|
| Recordatorio de proxima auditoria | Faltan 60 dias para la fecha sugerida | INFO | Delegado, Administrador | No escala |
| Auditoria proxima a vencer | Faltan 15 dias y sigue sin planificarse | WARNING | Delegado, Legal/Compliance | Si no se planifica, escala al Administrador |
| Auditoria vencida | Paso la fecha sugerida sin pasar a "En ejecucion" | HIGH | Delegado, Administrador | A los 60 dias, escala a Gerencia con referencia al riesgo de infraccion grave (Art. 56 lit. b) |
| Hallazgo critico sin plan de accion | Se registra un hallazgo Critico sin accion correctiva | HIGH | Delegado, Legal/Compliance | Escala a Gerencia a las 72 horas |
| Accion correctiva vencida | La fecha limite de una accion paso sin cerrarse | WARNING | Responsable de la accion, Delegado | A los 15 dias vencida, escala a Legal/Delegado y Gerencia |
| Auditoria abierta mas de 90 dias sin cerrar | Sigue en Plan de accion en curso mas de 90 dias | WARNING | Delegado, Administrador | A los 120 dias, escala a Gerencia |

### Evidencia resultante

- Informe de auditoria cerrado (alcance, hallazgos, plan de accion, conclusion), con hash, version, fecha y responsable, prueba de OBL-AUD-01 y OBL-PRIN-03; vive en MOD-019 y se conserva de forma indefinida con opcion de archivado manual hasta que MOD-016 defina un plazo especifico.
- Cada hallazgo con su evidencia adjunta, registro inmutable con fecha, usuario y referencia a la obligacion o control.
- Historial de estados de la auditoria (AuditLog), prueba de OBL-PRIN-03.
- Aprobacion del cierre, con identidad del Aprobador y, si hubo, la justificacion de cada riesgo aceptado.
- Vinculacion de cada accion correctiva con su tarea y su cierre en MOD-021.
- Notificacion enviada al Delegado como insumo de su informe periodico (OBL-DPO-07), sin que eso equivalga a que ese informe periodico ya se cumplio.
- Paquete de evidencia exportable con verificacion de integridad (hash o firma), disponible para el Auditor externo, la Gerencia y, si lo requiere, la ACE.

### Variantes y casos borde

- **Variante regulatoria: requerimiento o inspeccion de la ACE (no auditoria propia).** En Grupo Financiero Itzalco (corporativo con banco, aseguradora y financiera), la Direccion de Proteccion de Datos de la ACE envia a la sociedad aseguradora un oficio pidiendo documentos y antecedentes especificos (Art. 50 lit. t) LPDP), sin que exista todavia una resolucion de inicio de un procedimiento sancionador. Administrador de la organizacion o Responsable Legal registra el requerimiento dentro de un expediente de MOD-024 (campo repetible `requerimiento_informacion_ace`, dentro de la entidad Procedimiento Sancionador), con la fecha, el contenido solicitado, el plazo otorgado y la respuesta enviada; Ana Gabriela Reyes Portillo (Directora de Cumplimiento Corporativo) coordina la respuesta usando el mismo Centro de Evidencias (MOD-019) para reunir lo solicitado, con doble control obligatorio para cualquier paquete con destino externo. **Hueco:** ninguna ficha modela un flujo ligero e independiente para un requerimiento simple de informacion que no forme parte de un procedimiento sancionador ya abierto; el campo mas cercano que existe (`requerimiento_informacion_ace`) vive dentro de la entidad Procedimiento Sancionador de MOD-024, por lo que registrar un requerimiento aislado exige abrir ese mismo expediente (por ejemplo con `origen_del_caso = OTRO`), aunque la empresa no este bajo un procedimiento sancionador formal. Se marca "hueco: no definido en la ficha de MOD-024" y se lista al final de este documento.
- **Pyme sin Delegado ni Legal designado.** En Ferreteria y Suministros El Roble, Karla Beatriz Hernandez Mejia (Administradora y Delegada) planifica, registra los hallazgos y cierra la auditoria ella misma; el sistema lo permite pero muestra la advertencia de "autorrevision" tanto en la aprobacion de riesgo aceptado como en el cierre, porque Ferreteria esta por debajo del umbral configurable de 50 empleados.
- **Auditoria tipo Externa o Mixta.** Si Avicola decide contratar una firma auditora en vez de auditarse de forma interna, el tipo de auditoria pasa a Externa o Mixta, se invita al auditor externo desde la planificacion, y su informe se adjunta como evidencia adicional de esa auditoria puntual (funcionalidad COULD HAVE, ver Cobertura por version).
- **Primera auditoria de la organizacion.** La fecha de "periodo cubierto - desde" se precarga automaticamente con la fecha de adecuacion inicial registrada en el diagnostico (MOD-004), para que el primer ciclo no quede con un periodo ambiguo.
- **Reapertura de una auditoria cerrada.** Si surge un hallazgo relacionado despues del cierre, o la ACE pide informacion sobre ese mismo periodo, la auditoria puede reabrirse con motivo obligatorio; el informe anterior se conserva como version historica, nunca se sobrescribe.

### Cobertura por version

| Funcionalidad | MVP | V1 / V2 |
|---|---|---|
| Ciclo estructurado completo de MOD-018 (planificar, ejecutar, hallazgos, plan de accion, cierre con aprobacion separada) | SHOULD HAVE (todo el modulo es SHOULD HAVE; no bloquea a ningun MUST HAVE) | - |
| Cobertura parcial mientras MOD-018 no este activo: recordatorio generico anual en MOD-023 (MUST HAVE) mas AuditLog embebido | Disponible desde el primer dia de uso del sistema | Se reemplaza por el ciclo estructurado al activarse MOD-018 |
| Auditoria de tipo Externa o Mixta con invitacion de auditor externo y adjunto de su informe | No en el primer ciclo | COULD HAVE |
| Plantillas de checklist diferenciadas por sector o tamano de empresa | No incluido | FUTURE |
| Integracion con un futuro mecanismo de certificacion de la ACE (OBL-AUD-02) | No incluido; la ACE no ha habilitado ningun mecanismo a la fecha de este analisis | FUTURE, condicionado a que la ACE lo habilite |
| Centro de Evidencias (MOD-019), Controles (MOD-015), RAT (MOD-006), Centro de Tareas (MOD-021) que este caso consume | MUST HAVE, disponibles desde el MVP | - |

### Riesgos especificos del caso y su mitigacion

| Riesgo | Mitigacion de diseno |
|---|---|
| Que un tercero interprete una auditoria "Cerrada" como una declaracion de que la empresa cumple la LPDP | Banner de descargo estandar mas el texto especifico: "Este informe documenta el alcance revisado y los hallazgos de esta auditoria interna; no constituye una certificacion de cumplimiento legal ni sustituye la facultad de la ACE" |
| Que se confunda el historial de auditorias con la certificacion oficial de la ACE (OBL-AUD-02), que aun no existe | El sistema nunca usa las palabras "certificacion" ni "sello" dentro de este modulo, salvo para aclarar en la ayuda contextual que ese mecanismo no esta habilitado |
| Que una pyme posponga indefinidamente su primera auditoria por parecer un proceso demasiado formal | Checklist precargado automaticamente desde MOD-006 y MOD-015; alcance sugerido por defecto limitado a las obligaciones OBLIGATORIO |
| Que la fecha del recordatorio anual quede mal calculada, o una auditoria quede "Planificada" indefinidamente sin iniciarse | Alertas escalonadas (60, 15 dias, vencida) sobre el mismo motor de plazos (MOD-023) que usa el resto del sistema |
| Que un hallazgo describa una debilidad de seguridad real cuya filtracion facilite un ataque | Acceso a los hallazgos restringido a los roles con necesidad de conocerlos; el paquete exportado a un auditor externo o a la ACE se limita al alcance de esa auditoria especifica |
| Que la misma persona registre el hallazgo, decida aceptar el riesgo y cierre la auditoria, sin segundo control real (tipico en pyme) | Advertencia visible de autorrevision en cada aprobacion de riesgo aceptado y en cada cierre hecho por el mismo usuario que registro los hallazgos |

---

## Caso 11. Cambia la normativa

Fuentes principales: `03_modulos/MOD-024_ficha.md` (Centro Regulatorio, bandera de doble estado), `02_validacion/06_mapa_definitivo_de_modulos.md` seccion 5 (explicacion completa del doble estado de la reforma 659), y las secciones de cada ficha afectada (`MOD-002_ficha.md`, `MOD-007_ficha.md`, `MOD-008_ficha.md`, `MOD-011_ficha.md`, `MOD-016_ficha.md`, `MOD-017_ficha.md`).

Este caso tiene un ejemplo principal, con profundidad completa (la reforma 659), y un segundo ejemplo breve (un cambio normativo menor que afecta un plazo ya calculado).

### Ejemplo principal: activacion del regimen FUTURO de la reforma 659

#### Situacion de partida

Las tres empresas de ejemplo estan usando el sistema bajo el regimen `ACTUAL` (Delegado de Proteccion de Datos obligatorio en el sector privado, Arts. 15 y 17 LPDP vigentes). En Grupo Financiero Itzalco, Lic. Mauricio Ernesto Aguilar Sandoval ejerce como Delegado certificado ante la ACE, dedicado al banco del grupo; en Avicola San Andres, Jorge Alberto Menendez Rauda ejerce como Delegado interno en proceso de certificacion; en Ferreteria y Suministros El Roble, Karla Beatriz Hernandez Mejia acumula el rol de Delegada junto con el de Administradora. El Decreto Legislativo 659 (numero pendiente de confirmar contra el texto oficial) fue aprobado por la Asamblea Legislativa el 17 de septiembre de 2026, pero al 24 de septiembre de 2026 su publicacion en el Diario Oficial no esta confirmada.

#### Disparador

El equipo del producto (Editor de contenido regulatorio, actor que no es un rol de ninguna organizacion cliente) confirma, semanas o meses despues, que el decreto se publico en el Diario Oficial, que transcurrieron los 8 dias de vacatio legis, y que el texto oficial coincide con lo reportado por fuentes secundarias.

#### Actores y modulos que intervienen

| Rol / actor | Participacion en este caso |
|---|---|
| Equipo del producto (Editor de contenido regulatorio) | Unico actor que puede activar la bandera; no es un rol de la organizacion cliente |
| Delegado de Proteccion de Datos (o Responsable interno) | Recibe la notificacion del cambio en cada empresa; decide si mantiene la figura de forma voluntaria |
| Administrador de la organizacion | Recibe la tarea "Revisar si mantiene esta figura de forma voluntaria"; en pyme, decide junto con el rol Delegado que acumula |
| Responsable Legal / Compliance | Revisa el impacto del cambio sobre avisos publicados, revocaciones y expedientes ARCO-POL en curso |
| Responsable ARCO-POL / Responsable del tramite | Ve que el aprobador por defecto de sus expedientes nuevos pasa a ser el Responsable interno vigente |

| Modulo | Codigo | Papel en este caso |
|---|---|---|
| Centro Regulatorio | MOD-024 | Propietario de la bandera `regimen_reforma_659`; unico origen del cambio |
| Delegado / Responsable Interno de Datos | MOD-002 | Recalcula `tipo_rol` por defecto; crea tarea de continuidad voluntaria |
| Consentimiento | MOD-007 | Recalcula quien aprueba una revocacion de consentimiento pendiente |
| Documentos y Politicas | MOD-008 | Crea tarea de revision de avisos de privacidad publicados; no los reescribe automaticamente |
| ARCO-POL | MOD-011 | Recalcula el aprobador por defecto de expedientes nuevos; conserva la regla original en los expedientes ya cerrados o en curso |
| Capacitacion | MOD-017 | El plan anual de capacitacion e induccion pasa de obligatorio a buena practica recomendada (salvo Delegado voluntario) |
| Retencion y Eliminacion | MOD-016 | No cambia el plazo de conservacion del aviso (10 anos); solo el texto de ayuda contextual sobre a quien menciona el aviso conservado |
| Centro de Tareas | MOD-021 | Aloja la tarea transversal "Revisar el impacto del cambio de regimen normativo" en cada organizacion |
| Centro de Evidencias | MOD-019 | Conserva cada pieza de evidencia con el regimen vigente en el momento en que se genero, sin reinterpretarla |

#### Diagrama ASCII del recorrido de extremo a extremo

```
Equipo del producto                MOD-024                    MOD-002 / MOD-007 / MOD-008 / MOD-011 / MOD-017
        |                              |                                      |
        | confirma publicacion +        |                                      |
        | vacatio legis + validacion     |                                      |
        | juridica del texto oficial     |                                      |
        +------------------------------>|                                      |
                                         | bandera regimen_reforma_659:         |
                                         | ACTUAL -> FUTURO                     |
                                         | (fecha_activacion_bandera registrada)|
                                         |-------------------------------------->|
                                         |                    evento "cambio de bandera"
                                         |                    hacia los 6 modulos consumidores
                                         |                                      |
                                         |                    MOD-002: tarea "revisar si mantiene
                                         |                    la figura de forma voluntaria";
                                         |                    tipo_rol no cambia solo, requiere
                                         |                    decision explicita
                                         |                                      |
                                         |                    MOD-008: tarea "revisar avisos
                                         |                    publicados tras el cambio de regimen"
                                         |                    (no republica nada por si solo)
                                         |                                      |
                                         |                    MOD-011: aprobador por defecto de
                                         |                    expedientes NUEVOS pasa a Responsable
                                         |                    interno; expedientes cerrados o en
                                         |                    curso conservan su regla original
                                         |                                      |
                                         |                    MOD-017: plan anual pasa de
                                         |                    obligatorio a buena practica
                                         |                    recomendada (si no hay Delegado
                                         |                    voluntario)
                                         v                                      v
                                MOD-021: tarea "Revisar el impacto del cambio     MOD-019: evidencia
                                de regimen normativo" en cada organizacion        historica preservada
                                                                                  con su regimen original
```

#### Paso a paso

| Paso | Quien | Modulo | Que hace en el sistema | Que genera | Plazo y como se calcula | Fundamento |
|---|---|---|---|---|---|---|
| 1 | Equipo del producto | MOD-024 | Detecta la aprobacion legislativa (ya ocurrida, 17-sep-2026); la bandera pasa de ACTUAL a EN_VERIFICACION (estado tecnico interno) | Banner informativo a todas las organizaciones: "Decreto Legislativo 659, segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado"; ninguna obligacion cambia todavia | Sin plazo legal; paso interno de seguimiento | OBL-PLAZO-05; decision 2.7.32 |
| 2 | Equipo del producto | MOD-024 | Confirma `fecha_publicacion_diario_oficial_reforma`, `fecha_cumplimiento_vacatio_legis` (publicacion + 8 dias) y `validacion_juridica_texto_oficial = Si` | Bandera pasa a FUTURO; se registra `fecha_activacion_bandera` | Vacatio legis: 8 dias desde la publicacion oficial (analogia con el Art. 64 LPDP) | OBL-PLAZO-05; decision no automatica (ver seccion siguiente) |
| 3 | Sistema (automatico) | MOD-024 | Emite el evento "cambio de bandera" hacia MOD-002, MOD-007, MOD-008, MOD-011, MOD-015 y MOD-017 (MOD-008 se agrega por precision de esta ficha porque `mapa_modulos.json` aun no lo incluye en el `alimenta_a` de MOD-024, ver Contradicciones); actualiza `estado_instrumento` de cada una de las 17 obligaciones afectadas, preservando su clasificacion anterior en el historial | Registro versionado de cada obligacion afectada | Inmediato al activarse la bandera | `06_mapa_definitivo_de_modulos.md` seccion 5 |
| 4 | Sistema (automatico) | MOD-021 | Crea, para cada organizacion cliente, la tarea "Revisar el impacto del cambio de regimen normativo" | Tarea dirigida a Administrador, Delegado/Responsable interno y Responsable Legal | Sin plazo legal fijo; plazo interno configurable | Automatizacion 1 y 2 de MOD-024, seccion G |
| 5 | Sistema (automatico) | MOD-002 | Para cada registro ACTIVO de Delegado, crea la tarea "Revisar si mantiene esta figura de forma voluntaria"; actualiza la etiqueta de OBL-DPO-02 a 08 de OBLIGATORIO/CONDICIONAL a "opcional bajo el regimen vigente" | Tarea hacia Administrador de la organizacion; clasificacion anterior preservada en el historial | Sin plazo legal; decision de continuidad no automatica | `06_mapa_definitivo_de_modulos.md` seccion 5, punto 7 |
| 6 | Administrador (o Delegado, en pyme) | MOD-002 | Decide si mantiene voluntariamente al Delegado o migra a Responsable Interno sin certificacion ACE | El campo `tipo_rol` solo cambia con esta decision explicita, nunca de forma automatica | Sin plazo legal; decision estrategica de la empresa | Decision no automatizable (seccion H de MOD-002) |
| 7 | Sistema (automatico) | MOD-008 | Si existe al menos un Aviso de Privacidad en estado PUBLICADO/VIGENTE, crea la tarea "Revisar avisos publicados tras el cambio de regimen"; nunca reescribe ni republica el documento por si solo | Tarea hacia el Delegado/Responsable interno; alerta WARNING | Sin plazo legal fijo para la revision misma; el Art. 24 lit. h) exige que el aviso vigente indique los datos de contacto correctos | OBL-RET-04 (colateral); MOD-008 seccion G regla 3 |
| 8 | Delegado / Responsable interno | MOD-008 | Revisa si el aviso vigente sigue mencionando correctamente al Delegado o si ya debe mencionar al "sujeto obligado" / Responsable Interno; decide si republica | Nueva version del aviso, si se decide publicarla; la version anterior se conserva integra | Sin plazo legal fijo | Decision no automatizable (MOD-008 seccion H) |
| 9 | Sistema (automatico) | MOD-011 | Para expedientes ARCO-POL nuevos, el aprobador por defecto de todo acto atribuido a "el Delegado" (prevencion, incompetencia, resolucion, notificacion a receptores) pasa a ser la persona con el rol Responsable interno vigente | Expedientes en curso o ya cerrados bajo el regimen ACTUAL conservan su regla original en el historial | Sin cambio de plazos: 20+20, prevencion 10, devolucion 5, notificacion a receptores 5 se mantienen iguales segun fuentes secundarias | OBL-ARCO-01, 08, 10, 11, 14 |
| 10 | Sistema (automatico) | MOD-007 | El campo "persona que aprueba y ejecuta" de toda revocacion de consentimiento pendiente se recalcula segun el rol vigente | Expedientes ya cerrados conservan el rol que aplicaba cuando se cerraron | Plazos de 5 dias habiles (ejecutar) y 5 dias habiles (informar al encargado) sin cambio | OBL-CONS-03 |
| 11 | Sistema (automatico) | MOD-017 | Si no hay Delegado voluntario activo, el Plan anual de capacitacion e induccion se marca "buena practica recomendada" en su ayuda contextual y deja de generar la tarea recordatoria obligatoria; OBL-CAP-01 (capacitacion general del personal) continua exactamente igual | Cambio de etiqueta visible, sin afectar planes ya publicados (version historica preservada) | Sin plazo legal fijo | OBL-CAP-02; `06_mapa_definitivo_de_modulos.md` seccion 5, punto 7 |
| 12 | MOD-016 (consulta de referencia, sin automatizacion propia) | MOD-016 | Consulta la bandera de MOD-024 unicamente para decidir que texto de ayuda contextual mostrar sobre el aviso conservado; el plazo de conservacion (10 anos, OBL-RET-04) no cambia | Ninguna accion sobre el plazo de retencion | El plazo de 10 anos sigue corriendo igual, sin importar cuantas veces cambie la bandera | OBL-RET-04; MOD-016 seccion "Doble estado" |
| 13 | Legal/Compliance | MOD-024 / MOD-021 | Revisa el conjunto de tareas generadas por el cambio de bandera en toda la organizacion y confirma que cada una fue atendida o descartada con motivo | Cierre documentado de la revision del cambio normativo | Sin plazo legal fijo; buena practica de seguimiento | Buena practica |

#### Decisiones que el sistema NO toma

1. **Activar el estado FUTURO de la bandera, o revertirlo**: nunca ocurre por la sola aprobacion legislativa, por el paso del tiempo o por una fecha calculada; requiere confirmacion manual del equipo del producto. Texto mostrado mientras la bandera sea ACTUAL: "Decreto Legislativo 659, segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado."
2. **Decidir si mantener voluntariamente al Delegado, o migrar a Responsable Interno sin certificacion ACE**: el sistema notifica y ofrece la opcion, nunca ejecuta el cambio de `tipo_rol` sin aprobacion explicita. "Requiere validacion de la organizacion o asesoria especializada."
3. **Determinar si el aviso de privacidad vigente sigue siendo valido despues del cambio de regimen**: el sistema solo crea la tarea de revision, la decision y la eventual republicacion quedan a la organizacion.
4. **Confirmar que el texto oficial del decreto coincide exactamente con lo reportado por fuentes secundarias**: exige validacion juridica explicita del Editor de contenido regulatorio antes de activar FUTURO; ninguna organizacion cliente puede forzar ni omitir este paso.

#### Alertas y escalamientos

| Alerta | Disparador | Nivel | Destinatario | Escalamiento |
|---|---|---|---|---|
| Cambio de estado regulatorio (reforma 659) | La bandera de MOD-024 cambia a FUTURO | INFO | Administrador, Delegado, Responsable Legal (en MOD-002) | No aplica, es informativa; se apaga al confirmar la lectura |
| Cambio de regimen 659, revisar avisos publicados | MOD-024 activa la bandera FUTURO y hay al menos un aviso vigente | WARNING | Delegado/Responsable interno, Administrador (en MOD-008) | Escala si no hay avance en 30 dias |
| Tarea transversal "Revisar el impacto del cambio de regimen normativo" vencida | La tarea generada en MOD-021 supera su fecha limite interna sin completarse | WARNING | Administrador, Delegado, Legal | Segun las reglas generales de tareas vencidas de MOD-021 |

#### Evidencia resultante

- Registro de la fecha exacta de activacion de la bandera (`fecha_activacion_bandera`) y de la validacion juridica del texto oficial, en MOD-024.
- Historial de la clasificacion anterior de cada una de las 17 obligaciones afectadas, preservado junto a la nueva, sin sobrescritura.
- En MOD-002: historial de que persona tenia `tipo_rol = DELEGADO` o `RESPONSABLE_INTERNO` en cada momento, y la decision documentada de continuidad voluntaria si la hubo.
- En MOD-011: cada expediente ARCO-POL conserva, de forma inmutable, la regla de aprobador que le aplicaba en el momento de su tramite, aunque el regimen cambie despues.
- En MOD-008: cada version del aviso de privacidad, con su fecha de publicacion y el regimen vigente en ese momento, conservada por MOD-016 durante el minimo de 10 anos.
- En MOD-019: toda evidencia generada bajo el regimen ACTUAL sigue siendo valida para la obligacion que prueba, mostrando siempre el regimen bajo el que se genero.

#### Variantes y casos borde

- **Reversion del regimen.** Si el decreto no llega a publicarse conforme a lo reportado, es impugnado, o su texto oficial difiere materialmente de las fuentes secundarias, el equipo del producto revierte la bandera a ACTUAL con `motivo_reversion` obligatorio; las tareas y registros que dependian de pasos exclusivos del regimen FUTURO se marcan "no aplica bajo el estado regulatorio actual, ver historial", nunca se eliminan; los expedientes ya cerrados bajo FUTURO conservan la regla que aplicaba al momento de su cierre.
- **Pyme con Delegado acumulado (Ferreteria El Roble).** Karla Beatriz Hernandez Mejia recibe la tarea de continuidad voluntaria como Administradora; al decidir, el sistema le muestra el mismo texto de advertencia de decision no automatizable que a cualquier otra organizacion, sin trato especial por el tamano de la empresa.
- **Delegado externo (Licda. Silvia Carolina Melendez, perfil 10).** Si Ferreteria El Roble decide no continuar con la figura de Delegado tras el cambio a FUTURO, el vinculo contractual con la Delegada externa se revisa fuera del sistema (es una decision comercial de la empresa); el sistema conserva integro el historial de los informes periodicos que esa persona genero mientras el cargo era obligatorio.
- **Grupo corporativo (Itzalco).** El cambio de bandera es un evento global unico, aplicado por igual a cada sociedad del grupo como organizacion independiente; no existe una decision de continuidad "a nivel de grupo": cada sociedad (banco, aseguradora, financiera) decide por separado si mantiene su propio Delegado.
- **Sector publico no afectado.** La reforma, segun fuentes secundarias, mantiene la figura del delegado en el sector publico (reforma al Art. 47); este producto se dirige al sector privado, por lo que esta variante queda fuera de alcance.

#### Cobertura por version

| Funcionalidad | MVP | V1 / V2 |
|---|---|---|
| Bandera de doble estado en MOD-024 (MUST HAVE) y su lectura por referencia desde MOD-002, MOD-007, MOD-008, MOD-011, MOD-017 (todos MUST HAVE) | MUST HAVE | - |
| Tarea automatica de revision de avisos publicados tras el cambio de regimen (MOD-008, regla G-3) | SHOULD HAVE: logica simple, pero solo se activa si la reforma efectivamente se publica y MOD-024 existe | - |
| Consulta de referencia desde MOD-016 (SHOULD HAVE) para el texto de ayuda contextual | Disponible cuando MOD-016 este activo; mientras tanto, el aviso simplemente sigue conservado sin el texto de ayuda diferenciado | - |
| Vision consolidada del impacto del cambio de regimen a nivel de grupo corporativo | No incluida | V1/Enterprise (decision 2.7.31) |

#### Riesgos especificos del caso y su mitigacion

| Riesgo | Mitigacion de diseno |
|---|---|
| Tratar el estado FUTURO como vigente antes de su publicacion oficial, dejando de nombrar Delegado cuando la ley todavia lo exige | La bandera vive exclusivamente en MOD-024, se activa manualmente solo tras verificar la publicacion oficial; el banner de incertidumbre se muestra siempre mientras la bandera sea ACTUAL |
| Que un aviso de privacidad quede con menciones desactualizadas (al Delegado en vez de al Responsable interno) sin que nadie lo note | Tarea automatica obligatoria de revision al activarse FUTURO, con alerta y escalamiento a 30 dias; nunca hay republicacion automatica sin revision humana |
| Que un expediente ARCO-POL o un registro del Delegado ya cerrado se reinterprete retroactivamente con la regla nueva | Cada expediente y cada registro conservan la regla vigente en el momento de su cierre; el cambio de bandera nunca se aplica hacia atras |
| Que la incertidumbre sobre el numero y contenido exacto del decreto se presente como un hecho verificado | Toda referencia a la reforma se cita siempre como "Decreto Legislativo 659, segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado" (decision 2.7.32), incluso dentro de los textos de ayuda de cada modulo afectado |

### Segundo ejemplo (breve): nueva guia de la ACE o nuevo asueto que afecta plazos ya calculados

**Situacion de partida y disparador.** Avicola San Andres tiene un expediente ARCO-POL abierto en MOD-011 (una solicitud de acceso de un ex empleado), con fecha limite calculada por MOD-023 a 20 dias habiles desde la recepcion. A mitad del plazo, la Asamblea Legislativa decreta un asueto nacional no programado (por ejemplo, con motivo de un evento oficial), y el equipo del producto lo confirma con su fuente oficial (Diario Oficial o decreto especifico) dentro de MOD-023.

**Actores y modulos.** Equipo del producto (confirma el asueto en la capa 2 de MOD-023); Responsable ARCO-POL / Responsable del tramite (ve el recalculo); Delegado (revisa si el nuevo plazo cambia alguna decision pendiente); Modulos: MOD-023 (Calendario y Motor de Plazos, propietario del recalculo), MOD-011 (ARCO-POL, modulo de origen del plazo afectado), MOD-021 (tarea actualizada), MOD-022 (notificacion del recalculo), MOD-024 (si el cambio proviene de una nueva `RegulatoryRuleVersion`, por ejemplo una nueva guia de la ACE sobre formularios ARCO-POL, en vez de un asueto).

**Paso a paso resumido.**

| Paso | Quien | Modulo | Que hace | Que genera | Fundamento |
|---|---|---|---|---|---|
| 1 | Equipo del producto | MOD-023 | Confirma el nuevo asueto (fecha, fuente, alcance sector privado/publico) y publica la actualizacion de la version anual del calendario (pasa de Vigente a Actualizada) | Nueva sub-version del calendario, con numero de revision | OBL-PLAZO-02 |
| 2 | Sistema (automatico) | MOD-023 | Detecta que la nueva fecha cae dentro de la ventana de un calculo Abierto (el plazo ARCO-POL de Avicola) y lo recalcula automaticamente | Nueva fecha limite; la fecha anterior queda conservada en el historial; nunca se mueve en silencio | OBL-PLAZO-01, OBL-PLAZO-02 |
| 3 | Sistema (automatico) | MOD-011 / MOD-022 | Notifica al Responsable ARCO-POL y, si el recalculo deja menos de 3 dias habiles para vencer, escala de inmediato al Administrador | Notificacion "recalculo aplicado a un plazo abierto" | Regla de la seccion I de MOD-023 |
| 4 (variante: nueva guia de la ACE) | Equipo del producto | MOD-024 | Si en vez de un asueto se trata de una nueva guia o lineamiento de la ACE, publica una nueva `RegulatoryRuleVersion` sobre el instrumento existente, conservando la version anterior con su fecha de vigencia cerrada | Tarea "Revisar cambio normativo: [nombre del instrumento]" en MOD-021 dirigida a Administrador, Delegado y Legal/Compliance | Automatizacion 2 de MOD-024, seccion G |

**Decision que el sistema NO toma.** Si el nuevo asueto o la nueva guia de la ACE debieron aplicarse desde antes de su confirmacion oficial (por ejemplo, un anuncio de prensa previo): el sistema nunca aplica un asueto no confirmado; muestra "Este posible asueto esta pendiente de confirmacion oficial y no se aplica todavia a ningun calculo."

**Evidencia y cobertura.** El snapshot de la version del calendario usada en cada calculo, y el historial de recalculos con la fecha anterior y el motivo, quedan en MOD-019 (via el modulo de origen); ambos son funcionalidad MUST HAVE desde el MVP, porque MOD-023 y MOD-024 son ambos MUST HAVE.

---

## Contradicciones y huecos detectados

Contradicciones (no se repiten en el cuerpo del documento; se adopta la version correcta segun la jerarquia definida en la tarea: fuente legal primaria y `matriz_obligaciones.json` > `mapa_modulos.json` y `06_mapa_definitivo_de_modulos.md` > `05_tipos_de_usuario.md` para roles > ficha del modulo propietario > otras fichas):

1. **Archivo:** `03_modulos/MOD-024_ficha.md` (seccion G, regla 1) frente a `02_validacion/mapa_modulos.json`. Que dice cada fuente: `mapa_modulos.json` declara en el `alimenta_a` de MOD-024 seis receptores: MOD-002, MOD-011, MOD-007, MOD-017, MOD-015 y MOD-021 (este ultimo coherente con la tarea que el mismo paso 3/4 de este caso crea en MOD-021); no es, entonces, que falte agregar un sexto receptor a una lista de cinco, sino que esa lista de seis ya incluye a MOD-021 y sigue sin incluir a MOD-008. La propia ficha de MOD-024 (que es la ficha del modulo propietario de la bandera) agrega a MOD-008 como receptor real del evento "cambio de bandera", porque la ficha ya redactada de MOD-008 (seccion G, regla 3) declara una automatizacion propia disparada exactamente por ese evento. Version adoptada en este documento (paso 3 y 7 del ejemplo principal del Caso 11): se incluye a MOD-008 entre los receptores del evento, siguiendo a la ficha del modulo propietario de la bandera (MOD-024) sobre el campo `alimenta_a` de `mapa_modulos.json`, que queda senalado en ambas fichas como pendiente de actualizar en una proxima revision del mapa (agregando MOD-008; MOD-021 ya figura en el mapa actual).
2. **Archivo:** `03_modulos/MOD-017_ficha.md` (seccion A y nota final) frente a `02_validacion/06_mapa_definitivo_de_modulos.md` (seccion 3) y `02_validacion/mapa_modulos.json` (campo `notas_reforma_659`). Que dice cada fuente: el mapa definitivo y el campo `notas_reforma_659` describen OBL-CAP-02 como "capacitacion especifica anual del Delegado"; la ficha de MOD-017, verificada contra `01_legal/matriz_obligaciones.json` y contra la fuente primaria (`lineamientos_dpo_OCR.txt`, Art. 22 ultimo parrafo), confirma que OBL-CAP-02 es el plan anual de capacitacion e induccion **dirigido al personal**, que el Delegado **elabora**, no una capacitacion que el Delegado recibe para si mismo (eso es OBL-DPO-05). Version adoptada en este documento (paso 11 del ejemplo principal del Caso 11): se usa la definicion de la ficha propietaria (MOD-017), verificada contra la matriz canonica y la fuente primaria, por estar mas arriba en la jerarquia que la frase abreviada del mapa.

Huecos detectados (pasos o piezas que ninguna ficha define):

1. **Hueco: no definido en la ficha de MOD-024.** Ninguna ficha modela un flujo ligero e independiente para un requerimiento simple de informacion de la ACE (Art. 50 lit. t) LPDP) que no forme parte de un procedimiento sancionador ya abierto. El campo mas cercano que existe (`requerimiento_informacion_ace`) vive dentro de la entidad Procedimiento Sancionador de MOD-024 (seccion D.3), por lo que registrar un requerimiento aislado, como el que recibe Grupo Financiero Itzalco en la variante regulatoria del Caso 10, exige abrir ese mismo tipo de expediente (por ejemplo con `origen_del_caso = OTRO`), aunque la empresa no este bajo un procedimiento sancionador formal.
2. **Hueco: no definido en ninguna ficha revisada.** Ninguna ficha de las 26 modela de forma explicita un mecanismo para que una empresa demuestre, ante una inspeccion de la ACE que no deriva en sancion, que colaboro y respondio a tiempo (mas alla del registro generico de `requerimiento_informacion_ace`); no existe, por ejemplo, un estado o informe especifico de "inspeccion cerrada sin hallazgos" distinto del cierre de un Procedimiento Sancionador.

