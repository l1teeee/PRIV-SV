## Caso 7. Un titular solicita acceso a sus datos

Caso con profundidad especial. Fuente principal: `03_modulos/MOD-011_ficha.md` (leida completa), cruzada con `03_modulos/MOD-012_ficha.md` (Portal del Titular), `03_modulos/MOD-016_ficha.md` (Retencion y Eliminacion, leida completa) y `03_modulos/MOD-023_ficha.md` (Calendario y Motor de Plazos, leida completa).

### Situacion de partida

Avicola San Andres, S.A. de C.V. (empresa mediana, aprox. 300 empleados) tiene un sistema de control de acceso biometrico (huella dactilar) para marcar la asistencia del personal de planta, un tratamiento ya registrado en el RAT (MOD-006) con base juridica de consentimiento reforzado por tratarse de un dato biometrico (OBL-SENS-06, OBL-SENS-07). Parte de la nomina de Avicola es procesada por el mismo proveedor de nomina en la nube que aparece en el Caso 9 de este documento, registrado en MOD-009 Proveedores y Encargados como Encargado en estado ACTIVO. Jorge Alberto Menendez Rauda ejerce el rol de Delegado de Proteccion de Datos interno; Daniela Patricia Cornejo Lazo, Coordinadora de RRHH, ejerce el rol de Responsable de area del tratamiento de marcaje biometrico y de la nomina; Roberto Antonio Villalta, Gerente de Tecnologia, ejerce el rol de Responsable de Seguridad / IT y administra tecnicamente el sistema de control de acceso. Avicola, al superar el umbral de 50 empleados (`05_tipos_de_usuario.md`, seccion 5.4), designo ademas a una persona de Cumplimiento como Responsable ARCO-POL / Responsable del tramite, distinta de quien aprueba.

El Sr. Manuel de Jesus Pineda Rivas trabajo en la planta de Avicola durante cuatro anos y dejo de laborar hace cuatro meses. No tiene cuenta ni acceso a ningun sistema de Avicola.

### Disparador

Manuel envia un correo electronico a la direccion de contacto publicada en el Aviso de Privacidad de Avicola, pidiendo que le informen que datos personales conserva la empresa sobre el, incluyendo especificamente su huella dactilar usada para el marcaje de asistencia, y quien ha consultado esos datos desde que dejo de trabajar alli. En el MVP no existe todavia el Portal del Titular (MOD-012, SHOULD HAVE): el canal de recepcion es el formulario interno seguro que administra MOD-011, y el correo de Manuel se traslada a ese formulario, adjuntando el mensaje original como evidencia (MOD-011, seccion F.3, caso "Solicitud por WhatsApp, correo electronico o presencial"). Cuando MOD-012 este disponible, Manuel habria podido usar en su lugar el formulario publico de ese modulo, que crea la misma Solicitud dentro de MOD-011 sin cambiar el resto del recorrido (`03_modulos/MOD-012_ficha.md`, seccion F.1).

### Actores (roles estandar) y modulos que intervienen

| Rol estandar (05_tipos_de_usuario.md 5.3) | Participacion en este caso |
|---|---|
| Titular (formulario externo) | Presenta la solicitud de acceso, aporta copia de su DUI y datos de contacto, recibe la respuesta |
| Responsable ARCO-POL / Responsable del tramite | Registra la solicitud en el formulario interno, verifica identidad, redacta los borradores (prevencion, informe de acceso), coordina con RRHH e IT |
| Delegado de Proteccion de Datos (o Responsable interno) | Aprueba y emite la prevencion (si aplica) y el informe de acceso final; gestiona un eventual reclamo ante la ACE |
| Responsable de area (RRHH, Daniela) | Confirma y aporta el detalle de los datos laborales y de marcaje que Avicola conserva sobre Manuel |
| Responsable de Seguridad / IT (Roberto) | Extrae del sistema de control de acceso biometrico el detalle tecnico y la bitacora de consultas sobre el registro de Manuel |
| Responsable Legal / Compliance | Revisa el criterio de filtrado de datos de terceros del informe de acceso antes de la segunda aprobacion |
| Aprobador | Segundo revisor del informe de acceso, por tratarse de un dato sensible (biometrico), segun `05_tipos_de_usuario.md` seccion 5.4 |
| Administrador de la organizacion | Ve el caso en los reportes agregados de volumen y de cumplimiento de plazos; no interviene en la resolucion individual |
| Auditor (interno) | Solo lectura del expediente cerrado, como parte de la auditoria anual de cumplimiento |

| Modulo | Codigo | Papel en este caso |
|---|---|---|
| ARCO-POL | MOD-011 | Propietario del caso; gestiona todo el ciclo de vida del expediente |
| Delegado / Responsable Interno de Datos | MOD-002 | Determina quien ocupa, hoy y en el estado FUTURO, el rol que aprueba cada acto legalmente atribuido a esa figura |
| RAT y Mapa de Datos | MOD-006 | Localiza el Tratamiento "Marcaje biometrico de asistencia" y confirma que ya esta clasificado como sensible |
| Proveedores y Encargados | MOD-009 | Confirma si el proveedor de nomina (Encargado) conserva datos de contacto o de pago de Manuel, para el contenido del informe de acceso |
| Portal del Titular | MOD-012 | No interviene en este caso concreto (MVP); canal adicional futuro, referenciado en el Disparador |
| Retencion y Eliminacion | MOD-016 | Recibe la fecha de conservacion del expediente al cerrarse (SHOULD HAVE, ver Cobertura por version) |
| Centro de Tareas | MOD-021 | Aloja las tareas derivadas: localizar el dato en RRHH e IT, preparar el informe de acceso |
| Notificaciones | MOD-022 | Canal de las alertas de plazo |
| Calendario y Motor de Plazos | MOD-023 | Calcula el plazo de prevencion (10 dh), el plazo general (20+20 dh) y, si se presenta, el del reclamo ante la ACE (10 dh) |
| Centro de Evidencias | MOD-019 | Recibe el expediente completo y el informe de acceso final con verificacion de integridad |
| Centro Regulatorio | MOD-024 | Aloja la bandera de doble estado de la reforma 659 y, si se presenta, el reclamo ante la Direccion de Proteccion de Datos |
| Dashboard y Reportes | MOD-020 | Muestra el indicador de solicitudes proximas a vencer y el tiempo promedio de resolucion |

### Diagrama ASCII del recorrido de extremo a extremo

```
Manuel (Titular)         Resp. ARCO-POL              Delegado (Jorge)         MOD-006/MOD-009/MOD-023/MOD-019
      |                        |                            |                              |
      | correo pidiendo acceso |                            |                              |
      +----------------------->|                            |                              |
      |                  registra en formulario interno       |                              |
      |                  (MOD-011: NUEVA/RECIBIDA)             |                              |
      |                        |------------------------------------------------------------>|
      |                        v                            |         arranca calculo de plazos
      |                [VERIFICANDO IDENTIDAD]                |                              |
      |                        v                            |                              |
      |     [EVALUANDO REQ. ART.18] --incompleta--> [PREVENIDA] (10 dh) ----------------------->|
      |<--------------- notifica prevencion --------|                            |             |
      | subsana (domicilio)    |                            |                              |
      +----------------------->|                            |                              |
      |     [EVALUANDO REQ. ART.18] --completa--> [ADMITIDA] (arranca 20+20 dh) -------------->|
      |                        v                            |                              |
      |                [EN ANALISIS DE PROCEDENCIA]                                          |
      |                localiza dato en RAT (MOD-006)                                        |
      |                y consulta Encargado (MOD-009)                                        |
      |                        v                            |                              |
      |                redacta Informe de Acceso                                            |
      |                (filtra datos de terceros)                                           |
      |                        |--- 2do revisor (Aprobador, dato sensible) --------------->  |
      |                        v                            |                              |
      |     [PENDIENTE DE APROBAR RECONOCIMIENTO] -- aprueba y emite ----------------------->|
      |<--------------- entrega Informe de Acceso, sin costo (Art. 23) ----------------------|
      |                        v                            |                              |
      |                   [CERRADA] --------------------------------------------------------|
      |                                                                    expediente + evidencia
      |                                                                    con hash a MOD-019;
      |                                                                    retencion (cierre + 5 anos)
      |                                                                    a MOD-016
      |
      | (variante) no conforme, reclamo ante la ACE dentro de 10 dh
      +------------------------------------------------------------------------------->[RECLAMO ANTE LA ACE]
```

### Paso a paso

| Paso | Quien | Modulo | Que hace en el sistema | Que genera | Plazo y como se calcula | Fundamento |
|---|---|---|---|---|---|---|
| 1 | Responsable ARCO-POL | MOD-011 | Registra la solicitud recibida por correo en el formulario interno (D.1 a D.10): datos de Manuel, derecho ejercido = Acceso, descripcion de lo que pide (incluye la huella biometrica) | Expediente ARCO-2026-0134 creado (Nueva/Recibida); evento de auditoria | Sin plazo aun: el computo de 20 dh no arranca hasta admitir la solicitud | OBL-ARCO-08 (Art. 18) |
| 2 | Responsable ARCO-POL | MOD-011 | Marca tipo de solicitante = Titular; pide copia del DUI de Manuel y la coteja contra el registro laboral ya existente en RAT/RRHH | Registro de verificacion de identidad, con hash del documento adjunto | Sin plazo propio | OBL-ARCO-01 (Art. 6) |
| 3 | Sistema (automatico) | MOD-011 | Revisa el checklist de los 7 elementos del Art. 18; detecta que falta el domicilio actual de Manuel | Genera borrador de prevencion; pasa a estado Prevenida | 10 dias habiles calculados por MOD-023 (dias habiles, capas 0 a 2) desde la notificacion de la prevencion | OBL-ARCO-08 (Art. 18 inciso final) |
| 4 | Delegado (Jorge) | MOD-011 | Aprueba y emite la prevencion | Notificacion a Manuel por correo | Arranca el contador de 10 dh | OBL-ARCO-08 |
| 5 | Titular | MOD-011 | Manuel aporta su domicilio actual dentro del plazo | El contador de 10 dh se detiene; el expediente vuelve a Evaluando requisitos Art. 18 | El computo del plazo general de 20 dh sigue el criterio conservador (no se suspende por la prevencion): "La ley no precisa si la prevencion suspende este plazo. El sistema aplica por defecto el criterio mas conservador (no suspende). Verifique este criterio con asesoria legal si el caso es critico." | MOD-011, seccion H |
| 6 | Sistema (automatico) | MOD-011 / MOD-023 | Checklist completo; pasa a Admitida | Arranca el contador de 20 dh; crea la tarea "Resolver solicitud" en MOD-021 | 20 dias habiles desde la admision, prorrogable una vez hasta 20 dh mas por causa justificada | OBL-ARCO-10 (Art. 20) |
| 7 | Responsable ARCO-POL | MOD-006 | Consulta el RAT para localizar el Tratamiento "Marcaje biometrico de asistencia" y confirmar que ya esta clasificado como dato sensible | Referencia al Tratamiento vinculada al expediente | Sin plazo propio | Buena practica (OBL-ARCO-08, Art. 18 lit. c) |
| 8 | Responsable de area (RRHH, Daniela) | MOD-021 / MOD-006 | Ejecuta la tarea "confirmar datos de Manuel en el expediente laboral": nomina, fecha de ingreso y de baja, categorias de dato | Aporta el detalle al expediente ARCO-POL | Fecha limite interna anterior al vencimiento del plazo maestro | Buena practica |
| 9 | Responsable de Seguridad / IT (Roberto) | MOD-021 | Ejecuta la tarea "extraer bitacora de accesos al registro biometrico de Manuel": quien consulto ese dato desde su baja, con que proposito | Extracto tecnico adjunto al expediente, con hash de integridad | Fecha limite interna | OBL-ARCO-02 (Art. 8, insumo) |
| 10 | Responsable ARCO-POL | MOD-009 | Consulta si el proveedor de nomina (Encargado) conserva todavia datos de contacto o de pago de Manuel | Referencia al Encargado, sin transferencia de titularidad de los datos | Sin plazo propio | MOD-011, seccion L.2 |
| 11 | Responsable ARCO-POL | MOD-011 | Redacta el Informe de Acceso (Art. 8): quienes consultaron los datos de Manuel y con que proposito, filtrando automaticamente cualquier dato de otro empleado que pudiera aparecer mezclado en la misma bitacora | Borrador de Informe de Acceso, con el texto "Documento generado como borrador a partir de la informacion registrada. Requiere revision y aprobacion de su organizacion antes de usarse..." | Antes de vencer el plazo de 20 dh | OBL-ARCO-02 (Art. 8) |
| 12 | Aprobador | MOD-011 | Revisa el borrador como segundo revisor, por tratarse de un dato biometrico (categoria sensible), antes de que el Delegado lo apruebe | Segunda aprobacion registrada, distinta de quien redacto el borrador | Antes de la aprobacion del Delegado | `05_tipos_de_usuario.md`, seccion 5.4 |
| 13 | Delegado (Jorge) | MOD-011 | Aprueba el Informe de Acceso final y confirma la modalidad de entrega que Manuel eligio (copia simple por correo electronico) | Estado pasa de Pendiente de aprobar reconocimiento a Reconocida | Aprobacion explicita humana antes de emitir (decision 2.7.22) | OBL-ARCO-02 |
| 14 | Sistema (automatico) | MOD-011 / MOD-008 | Verifica que la modalidad elegida (correo electronico) no genera costo de reproduccion segun la tabla publicada en la Politica de Privacidad | Registro de tarifa aplicada = 0 | Sin plazo propio | OBL-ARCO-13 (Art. 23) |
| 15 | Delegado (Jorge) | MOD-011 | Emite y notifica el Informe de Acceso a Manuel por el medio que el senalo | Constancia de notificacion; el expediente pasa a Cerrada | Dentro del plazo de 20 dh (en este caso, sin necesitar prorroga) | OBL-ARCO-10 |
| 16 | Sistema (automatico) | MOD-011 / MOD-016 | Calcula la fecha sugerida de fin de retencion del expediente (cierre + 5 anos, criterio recomendado) y la envia a MOD-016 | Regla de retencion documental creada en MOD-016 | 5 anos desde el cierre (criterio recomendado, sin norma expresa) | OBL-RET-05 |
| 17 | Sistema (automatico) | MOD-019 | Consolida el expediente completo (checklist, verificacion de identidad, aprobaciones, Informe de Acceso final, registro de tarifa) como evidencia con verificacion de integridad | Paquete de evidencia exportable | Se genera al cerrar el caso | OBL-PRIN-03; anti-feature 25 |
| 18 (variante, no ejercida en este caso) | Responsable ARCO-POL | MOD-011 | Si Avicola no fuera competente sobre el dato pedido (por ejemplo, si perteneciera a otra sociedad del grupo), el Responsable ARCO-POL declararia incompetencia | Borrador de devolucion motivada; el Delegado aprueba y emite | 5 dias habiles desde la recepcion, calculados por MOD-023 | OBL-ARCO-09 (Art. 19) |
| 19 (variante, no ejercida en este caso) | Responsable ARCO-POL, Aprobador y Delegado | MOD-011 | Si una parte de la bitacora no pudiera depurarse por completo de datos de otro empleado, se seleccionaria una de las 8 causales tasadas del Art. 22 para una denegatoria parcial motivada de esa parte especifica | Borrador de denegatoria parcial; segunda aprobacion del Aprobador mas aprobacion del Delegado | 3 dias habiles desde que se aprueba la decision de denegar (no desde que se redacta el borrador), calculados por MOD-023 | OBL-ARCO-12 (Art. 22) |
| 20 (variante) | Titular | MOD-011 / MOD-024 | Manuel no esta conforme con el Informe de Acceso y presenta un reclamo ante la Direccion de Proteccion de Datos de la ACE | Sub-registro "Reclamo ante la ACE"; el expediente Cerrado original no se modifica | 10 dias habiles desde la notificacion de la resolucion | OBL-ARCO-14 (Lineamientos DPO, Art. 33 inc. 4) |
| 21 (variante) | Delegado (Jorge) | MOD-011 | Prepara el borrador del informe de actuaciones para responder al requerimiento de la Direccion de Proteccion de Datos | Borrador de informe de actuaciones, conservado junto al expediente sin reabrir ni modificar la resolucion original | Sin plazo propio fijado en la ficha; se prepara antes de que la empresa lo remita por el canal oficial | OBL-ARCO-14 |

### Decisiones que el sistema NO toma

El sistema muestra siempre el texto "Requiere validacion de la organizacion o asesoria especializada" junto a cada una de estas decisiones (MOD-011, seccion H), salvo donde se indica un texto distinto:

1. Decidir si el checklist del Art. 18 esta realmente completo mas alla de la validacion de formato de cada campo: la revision sustantiva es del Responsable ARCO-POL.
2. Confirmar de forma definitiva que ningun dato de un tercero quedo en el Informe de Acceso: el filtrado es automatico, pero la verificacion final de que no quedo ningun dato de otro empleado es responsabilidad humana antes de aprobar.
3. Decidir si la prevencion suspende o no el computo del plazo general de 20 dias habiles (incertidumbre juridica no resuelta, por analogia con el Art. 90.1 de la Ley de Procedimientos Administrativos); el sistema aplica por defecto el criterio conservador (no suspende) y muestra el texto citado en el Paso 5.
4. Resolver la solicitud en si misma (reconocer el acceso o denegarlo, total o parcialmente): el sistema calcula el plazo, presenta el checklist y prepara el borrador; el Delegado (y el Aprobador, cuando hay un dato sensible) decide y aprueba antes de que cualquier acto se considere emitido.
5. Determinar si el proveedor de nomina cuenta como "receptor" que deberia notificarse bajo el Art. 21 inc. 3 en caso de que el dato hubiera sido corregido o eliminado en vez de consultado (no aplica a un acceso, pero el sistema aplicaria por defecto el criterio conservador de tratarlo como receptor si correspondiera a otro derecho).
6. Autorizar el envio real del informe de actuaciones a la Direccion de Proteccion de Datos de la ACE: el sistema prepara el borrador; la empresa (Delegado o Administrador) revisa y ejecuta el envio por el canal oficial.

### Alertas y escalamientos

| Alerta | Disparador | Nivel | Destinatario | Escalamiento |
|---|---|---|---|---|
| Solicitud nueva sin responsable asignado | Se recibe la solicitud y no tiene Responsable ARCO-POL asignado | WARNING | Administrador, Delegado | Escala al Delegado si sigue sin asignar 24 horas despues |
| Prevencion proxima a vencer | Faltan 3 dias habiles de los 10 | WARNING | Responsable ARCO-POL | Escala al Delegado si falta 1 dia habil |
| Plazo general proximo a vencer | Faltan 5 dias habiles de los 20 (o de la prorroga) | HIGH | Responsable ARCO-POL, Delegado | Escala a Administrador si faltan 2 dias habiles |
| Solicitud pendiente de aprobacion del Delegado | Borrador listo, sin aprobacion en el plazo interno configurado | WARNING | Delegado | Escala a Administrador si pasan 2 dias sin aprobar |
| Reclamo recibido de la Direccion de Proteccion de Datos | Se registra un reclamo dentro del expediente | CRITICAL | Delegado, Legal, Administrador | Escala a Gerencia (perspectiva Administrador del dashboard) |
| Retencion del expediente proxima a vencer | Faltan 90 dias para cumplirse el plazo de retencion sugerido (5 anos) | INFO | Administrador, Auditor | No escala |

### Evidencia resultante

Vive en MOD-019 Centro de Evidencias, referenciada desde el expediente de MOD-011:

- Expediente completo, con fecha/hora de recepcion, canal usado y checklist de los 7 elementos del Art. 18, con usuario y fecha de cada marca (OBL-ARCO-08).
- Registro de verificacion de identidad de Manuel (hash del DUI adjunto) (OBL-ARCO-01).
- Historial completo de estados, incluida la prevencion y su subsanacion (OBL-ARCO-10, trazabilidad del plazo maestro).
- Version final del Informe de Acceso, con la aprobacion del Aprobador (segundo revisor) y del Delegado, cada una con identidad y fecha distintas de quien redacto el borrador (OBL-ARCO-02, OBL-PRIN-03).
- Registro de la tarifa aplicada (0, por gratuidad) (OBL-ARCO-13).
- Registro de los accesos de lectura al documento de identidad de Manuel (buena practica de seguridad).
- Si se presenta, registro del reclamo ante la Direccion de Proteccion de Datos y del informe de actuaciones preparado (OBL-ARCO-14).

Conservacion: minimo recomendado de 5 anos desde el cierre (OBL-RET-05, RECOMENDADO, sin norma expresa que fije ese numero; requiere validacion de asesoria legal), calculado por MOD-011 al cerrar el caso y gestionado por MOD-016.

### Variantes y casos borde

- **Pyme con una persona en varios roles.** En Ferreteria y Suministros El Roble (aprox. 30 empleados, por debajo del umbral de 50), Karla Beatriz Hernandez Mejia acumula Administradora y Delegada; si un ex-empleado de la ferreteria pidiera acceso, Karla redactaria y aprobaria, pero el sistema exigiria una segunda confirmacion explicita separada del guardado del borrador, con advertencia visible de "autorrevision"; al no superar los 50 empleados, no se exige un Aprobador distinto para el dato sensible, salvo que Karla decida invitar a alguien igual.
- **Grupo corporativo.** En Grupo Financiero Itzalco, si un cliente de la aseguradora pidiera acceso a sus datos, el expediente pertenece a esa sociedad especifica; Ana Gabriela Reyes Portillo (Directora de Cumplimiento Corporativo) revisaria el caso entrando a la organizacion de esa sociedad, sin una vista consolidada de grupo (funcionalidad V1/Enterprise, `02_validacion_de_la_idea.md`, decision 2.7.31).
- **Doble estado de la reforma 659.** De las 15 obligaciones propietarias de este modulo, 5 estan marcadas como afectadas (OBL-ARCO-01, 08, 10, 11, 14); si el estado FUTURO se activa durante la tramitacion, el expediente de Manuel conserva la regla vigente al momento de tramitarse (aprobador = Delegado); solo los expedientes nuevos usarian al Responsable interno como aprobador por defecto (MOD-011, "Doble estado de la reforma 659: efecto especifico sobre este modulo").
- **Solicitud por canal presencial.** Si Manuel hubiera preferido acudir en persona (como la persona Cecilia Marroquin de `05_tipos_de_usuario.md`, que desconfia de canales digitales), el Responsable ARCO-POL habria trasladado la informacion al mismo formulario interno, adjuntando la constancia de la reunion como evidencia; el plazo corre desde la recepcion efectiva, no desde su transcripcion al sistema.
- **Titular menor de edad.** No aplica a este caso (Manuel es un ex-empleado adulto), pero si el titular fuera un hijo de un empleado inscrito en el seguro medico colectivo, se activaria el sub-flujo de NNA (MOD-011, seccion D.5) con el aviso de tension normativa entre la LPDP y la Ley Crecer Juntos.
- **Solicitud potencialmente masiva.** Si varios ex-empleados de una misma salida de personal presentaran solicitudes similares en pocos dias, el sistema marcaria el patron con una alerta INFO al Delegado, sin denegar ni acelerar el archivo automaticamente, porque no existe en la LPDP una causal tasada de "solicitud abusiva" para el sector privado.

### Cobertura por version

| Funcionalidad | MVP | V1 / V2 |
|---|---|---|
| Formulario interno seguro con verificacion de identidad, prevencion, plazo 20+20 y gratuidad | MUST HAVE | - |
| Informe de acceso con filtrado automatico de datos de terceros | MUST HAVE | - |
| Segundo revisor (Aprobador) obligatorio cuando el dato es sensible | MUST HAVE (regla general de separacion de funciones) | - |
| Registro basico del reclamo ante la Direccion de Proteccion de Datos (fecha, texto libre) | MUST HAVE (registro como texto libre desde el MVP) | V1: plantilla dedicada de informe de actuaciones |
| Portal del Titular como canal adicional de presentacion y consulta de estado | No incluido (MOD-012 es SHOULD HAVE); la obligacion legal ya esta cubierta por el formulario interno | V1: formulario publico sin cuenta persistente y consulta de estado por codigo de un solo uso |
| Motor de retencion de datos del titular con calculo del maximo entre normas sectoriales | No incluido; la conservacion del expediente ocurre de forma pasiva (MOD-011 no permite borrar por defecto) | V1: MOD-016 (SHOULD HAVE), con estado, alerta y flujo de aprobacion de eliminacion |
| Deteccion automatica de solicitudes potencialmente masivas o duplicadas | No incluido | V2 / COULD HAVE |

### Riesgos especificos del caso y su mitigacion

| Riesgo | Mitigacion de diseno |
|---|---|
| Exponer datos biometricos o de otro empleado mezclados en la bitacora de accesos dentro del Informe de Acceso | Filtrado automatico de datos de terceros mas verificacion humana final antes de aprobar; segundo revisor obligatorio por tratarse de dato sensible |
| Que el proveedor de nomina (Encargado) no responda a tiempo sobre si conserva datos de Manuel | Tarea en MOD-021 con fecha limite interna anterior al vencimiento del plazo maestro de 20 dh, mas alerta escalonada |
| Calculo erroneo del plazo por un calendario de dias habiles desactualizado | Motor unico de plazos (MOD-023), con alerta si el calendario del ano en curso no esta configurado antes de admitir la solicitud |
| Que el ex-empleado reclame ante la ACE por demora o por considerar incompleto el informe | Evidencia continua desde el primer dia (MOD-019); alertas tempranas de vencimiento (desde 5 dh antes del plazo general) |
| Confundir a un Encargado (proveedor de nomina) con un "receptor" a notificar, aplicando de mas o de menos el Art. 21 inc. 3 | El sistema aplica el criterio conservador documentado en la ficha, dejando la decision final ajustable por una persona con nota de riesgo |

---

## Caso 8. Un titular solicita la eliminacion de sus datos

Caso con profundidad especial. Fuente principal: `03_modulos/MOD-011_ficha.md` (leida completa), cruzada con `03_modulos/MOD-016_ficha.md` (Retencion y Eliminacion, leida completa) y `03_modulos/MOD-023_ficha.md` (Calendario y Motor de Plazos, leida completa).

### Situacion de partida

Grupo Financiero Itzalco es un grupo corporativo con tres sociedades bajo una misma holding (un banco, una aseguradora y una financiera). Cada sociedad mantiene su propia organizacion dentro del sistema, sin una vista consolidada de grupo (funcionalidad V1/Enterprise, `02_validacion_de_la_idea.md`, decision 2.7.31). El Banco Itzalco (una de las tres sociedades) mantiene su propio Registro de Actividades de Tratamiento (RAT, MOD-006), donde el tratamiento "Cartera de clientes bancarios" y el tratamiento "Comunicaciones institucionales y prensa" estan registrados por separado. Parte de los sistemas del banco (el nucleo bancario y el sitio web corporativo) son operados por proveedores externos, registrados en MOD-009 como Encargados con contrato/DPA vigente. Lic. Mauricio Ernesto Aguilar Sandoval ejerce el rol de Delegado de Proteccion de Datos certificado, dedicado exclusivamente al banco; Licda. Ana Gabriela Reyes Portillo, Directora de Cumplimiento Corporativo, ejerce el rol de Responsable Legal / Compliance con visibilidad sobre las tres sociedades, sin fusionar sus expedientes.

El Sr. Wilfredo Antonio Cea Melgar fue cliente del Banco Itzalco hasta hace dos anos, cuando cerro su cuenta. Anos atras, el banco publico en su propio sitio web una nota de prensa sobre un evento comunitario que patrocino, que menciona el nombre completo de Wilfredo y una fotografia suya como asistente.

### Disparador

Wilfredo presenta, mediante el formulario interno seguro de MOD-011, una solicitud con dos partes: (a) que el banco elimine todos sus datos personales porque ya no es cliente, y (b) que retire de la nota de prensa publicada en el sitio web su nombre y su fotografia, porque aparecen al buscar su nombre en internet.

### Actores (roles estandar) y modulos que intervienen

| Rol estandar (05_tipos_de_usuario.md 5.3) | Participacion en este caso |
|---|---|
| Titular (formulario externo) | Presenta la solicitud con sus dos partes, recibe ambas resoluciones |
| Delegado de Proteccion de Datos (Mauricio) | Aprueba y emite cada acto del expediente; decide sobre la denegatoria parcial de la cancelacion |
| Responsable ARCO-POL / Responsable del tramite | Registra, verifica identidad, clasifica ambas partes de la solicitud (cancelacion y olvido), redacta los borradores |
| Responsable Legal / Compliance (Ana Gabriela) | Confirma si el Banco Itzalco es sujeto obligado bajo la LCLDA y valida los fundamentos de retencion sectorial; co-aprueba la denegatoria parcial |
| Responsable de area (Operaciones/Banca) | Confirma que datos de Wilfredo siguen en los sistemas del banco y por que (registros contables, prevencion de lavado de dinero) |
| Responsable de area (Marketing/Comunicaciones) | Ejecuta la eliminacion o edicion de la nota de prensa en el sitio web |
| Responsable de Seguridad / IT | Ejecuta y certifica la eliminacion tecnica en los sistemas propios; coordina con el proveedor del sitio web |
| Aprobador | Segundo revisor de la denegatoria parcial de la cancelacion, por el riesgo de reclamo ante la ACE |
| Auditor (interno) | Solo lectura del expediente y del historial de eliminaciones, en la auditoria anual |

| Modulo | Codigo | Papel en este caso |
|---|---|---|
| ARCO-POL | MOD-011 | Propietario del caso; distingue la cancelacion (Art. 10) del olvido (Art. 10 inciso final) dentro del mismo expediente |
| Retencion y Eliminacion | MOD-016 | Aporta el fundamento de retencion sectorial que sustenta la denegatoria parcial de la cancelacion |
| RAT y Mapa de Datos | MOD-006 | Localiza los tratamientos "Cartera de clientes bancarios" y "Comunicaciones institucionales y prensa" |
| Proveedores y Encargados | MOD-009 | Identifica al proveedor del nucleo bancario y al proveedor de hosting del sitio web como Encargados que deben ejecutar la eliminacion en sus sistemas |
| Documentos y Politicas | MOD-008 | Fuente de la Politica de Privacidad y de la tabla de costos (no aplica cobro en este caso, gratuidad) |
| Centro de Tareas | MOD-021 | Aloja las tareas de ejecucion en Operaciones, Marketing e IT |
| Notificaciones | MOD-022 | Canal de las alertas de plazo |
| Calendario y Motor de Plazos | MOD-023 | Calcula el plazo general (20+20 dh), el de notificacion a receptores (5 dh) y el de la denegatoria (3 dh) |
| Centro de Evidencias | MOD-019 | Recibe el expediente, la denegatoria motivada y las constancias de eliminacion |
| Centro Regulatorio | MOD-024 | Aloja la bandera de doble estado de la reforma 659 |

**Nota sobre el bloqueo cautelar.** La ficha de MOD-011 solo define un bloqueo cautelar automatico sobre el dato en revision para la rectificacion (Art. 9, OBL-ARCO-03); no existe en ninguna ficha una regla equivalente documentada para la cancelacion o el olvido. Este recorrido, por tanto, no aplica ningun bloqueo automatico sobre los datos de Wilfredo mientras se analiza su solicitud (ver "Contradicciones y huecos detectados" al final del archivo).

### Diagrama ASCII del recorrido de extremo a extremo

```
Wilfredo (Titular)       Resp. ARCO-POL         Delegado (Mauricio)      MOD-016/MOD-009/MOD-023
      |                        |                        |                          |
      | solicita cancelacion   |                        |                          |
      | + olvido (nota prensa) |                        |                          |
      +----------------------->|                        |                          |
      |                  registra 2 partes                |                          |
      |                  (MOD-011: NUEVA/RECIBIDA)         |                          |
      |                        |------------------------------------------------------>|
      |                        v                        |          arranca plazo 20+20 dh
      |                [VERIFICANDO IDENTIDAD]            |                          |
      |                        v                        |                          |
      |     [EVALUANDO REQ. ART.18] --completa--> [ADMITIDA]                          |
      |                        v                        |                          |
      |     [EN ANALISIS DE PROCEDENCIA]  (dos ramas en paralelo)                     |
      |                        |                        |                          |
      |   rama CANCELACION     |          rama OLVIDO (nota de prensa)                |
      |   (cartera bancaria)   |                        |                          |
      |                        |                        |                          |
      |   consulta MOD-016:    |          consulta MOD-009 (hosting) y confirma        |
      |   retenido por         |          que no hay obligacion de retencion           |
      |   OBL-RET-01/02/03     |          sobre la nota                              |
      |   (Cod. Comercio,      |                        |                          |
      |    Tributario, LCLDA)  |                        |                          |
      |                        v                        v                          |
      |    [PENDIENTE DE APROBAR       [PENDIENTE DE APROBAR                        |
      |     DENEGATORIA PARCIAL]        RECONOCIMIENTO (olvido)]                    |
      |    (Aprobador + Delegado)               |                                    |
      |                        |                v                                    |
      |                        |        [RECONOCIDA] --hubo receptor--> NOTIFICANDO A |
      |                        |        (elimina en sitio propio     RECEPTORES (5 dh)|
      |                        |         y pide al Encargado de hosting)              |
      |                        v                v                                    |
      |               [DENEGADA parcial]   [CERRADA (olvido)]                         |
      |               (3 dh para notificar)                                          |
      |<--------------- notifica ambas resoluciones -------------|                   |
      |                        v                                                     |
      |                   [CERRADA]  ----------------------------------------------->|
      |                                                       expediente + constancias
      |                                                       de eliminacion a MOD-019
      |
      | (variante) reclamo ante la ACE dentro de 10 dh
      +------------------------------------------------------------------------>[RECLAMO ANTE LA ACE]
```

### Paso a paso

| Paso | Quien | Modulo | Que hace en el sistema | Que genera | Plazo y como se calcula | Fundamento |
|---|---|---|---|---|---|---|
| 1 | Responsable ARCO-POL | MOD-011 | Registra la solicitud de Wilfredo con dos partes: derecho ejercido = Cancelacion (causal: los datos ya no son necesarios, el titular no es cliente) y derecho ejercido = Olvido (marca "los datos objeto de olvido estan publicados en internet") | Expediente ARCO-2026-0151 creado (Nueva/Recibida), con dos elementos de solicitud vinculados | Sin plazo aun | OBL-ARCO-04 (Art. 10, cancelacion y olvido) |
| 2 | Responsable ARCO-POL | MOD-011 | Verifica identidad: Wilfredo aporta copia de su DUI, comparado contra el expediente historico del banco | Registro de verificacion con hash | Sin plazo propio | OBL-ARCO-01 (Art. 6) |
| 3 | Sistema (automatico) | MOD-011 | Checklist del Art. 18 completo (ambas partes describen los datos y el motivo con suficiente detalle) | Pasa a Admitida | Arranca el contador de 20 dh (MOD-023) | OBL-ARCO-08, OBL-ARCO-10 |
| 4 | Responsable ARCO-POL | MOD-006 | Localiza en el RAT los dos tratamientos involucrados: "Cartera de clientes bancarios" (cancelacion) y "Comunicaciones institucionales y prensa" (olvido) | Dos referencias a Tratamiento vinculadas al mismo expediente | Sin plazo propio | Buena practica (OBL-ARCO-08, Art. 18 lit. c) |
| 5 | Responsable de area (Operaciones/Banca) | MOD-021 / MOD-016 | Consulta si existe una regla de retencion activa sobre los datos de la cartera bancaria de Wilfredo | El sistema encuentra reglas con fundamento OBL-RET-01 (Codigo de Comercio, 10 anos) y OBL-RET-02 (Codigo Tributario, 10 anos), y un fundamento OBL-RET-03 (LCLDA) pendiente de confirmacion | La fecha efectiva de retencion es el maximo entre los fundamentos activos | OBL-RET-01, OBL-RET-02, OBL-RET-03 (MOD-016) |
| 6 | Responsable Legal / Compliance (Ana Gabriela) | MOD-016 | Confirma que el Banco Itzalco es sujeto obligado bajo el Art. 2 de la LCLDA (el sistema no lo determina automaticamente) | El fundamento OBL-RET-03 queda activado con esa confirmacion, con el texto "Requiere validacion de la organizacion o asesoria especializada" | Sin plazo propio | MOD-016, seccion H.1 |
| 7 | Sistema (automatico) | MOD-016 / MOD-011 | Al encontrar reglas de retencion vigentes sobre la cartera bancaria, genera un borrador de denegatoria parcial motivada para la parte de Cancelacion, con el fundamento de retencion | Borrador de denegatoria parcial | Sin plazo propio en la generacion; el contador de 3 dh arranca al aprobarse la decision, no al redactarse el borrador | OBL-ARCO-04 (Art. 10 inciso 2, causal de improcedencia por obligacion de conservar) y OBL-ARCO-12 (Art. 22, denegatoria motivada) |
| 8 | Responsable ARCO-POL | MOD-009 | Consulta al proveedor de hosting del sitio web (Encargado) para confirmar que no existe ninguna obligacion de conservacion sobre la nota de prensa que menciona a Wilfredo | Referencia al Encargado; confirma que la nota puede eliminarse | Sin plazo propio | MOD-011, seccion L.2 |
| 9 | Responsable ARCO-POL | MOD-011 | Para la parte de Olvido, redacta el borrador de reconocimiento (procede eliminar el nombre y la fotografia de la nota de prensa) | Borrador de resolucion de reconocimiento (olvido) | Sin plazo propio | OBL-ARCO-04 (Art. 10 inciso final) |
| 10 | Aprobador + Responsable Legal | MOD-011 | Segunda revision de la denegatoria parcial de la cancelacion, por el riesgo de reclamo ante la ACE que implica invocar una obligacion sectorial ajena a la LPDP | Segunda aprobacion registrada | Antes de la aprobacion del Delegado | `05_tipos_de_usuario.md`, seccion 5.4 |
| 11 | Delegado (Mauricio) | MOD-011 | Aprueba ambas decisiones: la denegatoria parcial de la cancelacion (por retencion) y el reconocimiento del olvido | Los estados pasan a Denegada (parcial) y a Reconocida (olvido) | Aprobacion explicita humana antes de emitir (decision 2.7.22) | OBL-ARCO-12 (Art. 22), OBL-ARCO-04 |
| 12 | Sistema (automatico) | MOD-023 | Arranca el contador de 3 dh para notificar la denegatoria parcial, desde que se aprueba la decision | Alerta si faltan pocos dias habiles | 3 dias habiles | OBL-ARCO-12 (Art. 22) |
| 13 | Responsable de area (Marketing/Comunicaciones) | MOD-021 | Ejecuta la tarea "eliminar nombre y fotografia de la nota de prensa en el sitio propio" | Tarea marcada como ejecutada, con constancia (captura del cambio) | Antes de cerrar el caso de olvido | OBL-SEG-05 (eliminacion segura) |
| 14 | Responsable ARCO-POL | MOD-009 | Solicita al Encargado de hosting que confirme la propagacion del cambio | Constancia de la solicitud al Encargado | Sin plazo propio definido en ninguna ficha (ver huecos al final del archivo) | Buena practica |
| 15 | Sistema (automatico) | MOD-011 | Como el dato del olvido ya habia sido transferido a un receptor (el proveedor de hosting que aloja la pagina publicada), genera la lista de notificacion a receptores | Lista de receptores a notificar; contador de 5 dh por cada uno | 5 dias habiles desde que se determina la procedencia | OBL-ARCO-11 (Art. 21 inc. 3) |
| 16 | Responsable ARCO-POL | MOD-011 | Ejecuta y registra la notificacion a cada receptor identificado (el proveedor de hosting) | Evidencia de notificacion de cada receptor | Dentro de los 5 dh | OBL-ARCO-11 |
| 17 | Responsable de Seguridad / IT | MOD-016 | Registra el evento de eliminacion tecnica de la nota de prensa: metodo (borrado logico en el sistema de gestion de contenidos del sitio), constancia adjunta | Evento de eliminacion con hash de integridad | Sin plazo propio | OBL-SEG-05 |
| 18 | Delegado (Mauricio) | MOD-011 | Notifica a Wilfredo la denegatoria parcial motivada de la cancelacion (con el fundamento de retencion) y, por separado, la resolucion de reconocimiento del olvido ya ejecutada | Dos constancias de notificacion distintas | Denegatoria: dentro de 3 dh desde su aprobacion. Olvido: dentro del plazo general de 20 dh | OBL-ARCO-12, OBL-ARCO-10 |
| 19 | Sistema (automatico) | MOD-011 | Ambas partes de la solicitud llegan a un estado terminal (Denegada notificada y Cerrada); el expediente completo pasa a Cerrada | Fecha de cierre registrada | Se cumple dentro del plazo general de 20 dh, sin necesitar prorroga en este caso | OBL-ARCO-10 |
| 20 | Sistema (automatico) | MOD-011 / MOD-016 | Calcula la fecha sugerida de fin de retencion del expediente (cierre + 5 anos); en paralelo, la regla de retencion de la cartera bancaria (OBL-RET-01/02/03) sigue vigente de forma independiente, con su propia fecha efectiva mas lejana | Dos reglas de retencion distintas: la del expediente ARCO-POL (5 anos) y la de los datos bancarios de Wilfredo (10 a 15 anos, segun el fundamento) | OBL-RET-05 (expediente, 5 anos); OBL-RET-01/02/03 (datos bancarios, 10 a 15 anos) | - |
| 21 | Sistema (automatico) | MOD-019 | Consolida el expediente completo (checklist, verificacion, ambas aprobaciones, denegatoria motivada, resolucion de olvido, notificaciones a receptores, constancia de eliminacion) como evidencia con verificacion de integridad | Paquete de evidencia exportable | Se genera al cerrar el caso | OBL-PRIN-03; anti-feature 25 |
| 22 (limite declarado, no un paso omitido) | Responsable de Seguridad / IT | MOD-016 | Confirma que la eliminacion ejecutada en el sistema de gestion de contenidos no incluye la eliminacion en las copias de respaldo (backups) del sitio, que son infraestructura tecnica fuera del alcance del sistema | El expediente registra explicitamente esta limitacion como parte de la respuesta al titular | Sin plazo propio | Anti-feature 11; MOD-016, secciones A y P |
| 23 (variante) | Titular | MOD-011 / MOD-024 | Wilfredo no esta conforme con la denegatoria parcial de la cancelacion y presenta un reclamo ante la Direccion de Proteccion de Datos de la ACE | Sub-registro "Reclamo ante la ACE" | 10 dias habiles desde la notificacion | OBL-ARCO-14 |
| 24 (rama no ejercida, mencionada por completitud) | Responsable ARCO-POL | MOD-011 | Si Wilfredo hubiera pedido en cambio que el banco dejara de usar sus datos para mercadotecnia directa, correspondia clasificar la solicitud como Oposicion; si hubiera pedido detener el uso mientras se verifica un dato impugnado, correspondia Limitacion | No ocurre en este expediente | - | OBL-ARCO-05 (Art. 12, Oposicion), OBL-ARCO-06 (Art. 13, Limitacion) |

### Decisiones que el sistema NO toma

El sistema muestra siempre el texto "Requiere validacion de la organizacion o asesoria especializada" junto a cada una de estas decisiones (MOD-011, seccion H; MOD-016, seccion H):

1. Determinar si un plazo sectorial (mercantil, tributario, LCLDA) aplica realmente al giro de una empresa concreta, en este caso si el Banco Itzalco es sujeto obligado bajo la LCLDA: el sistema muestra el catalogo y calcula el maximo entre los fundamentos elegidos, pero exige confirmacion humana.
2. Aprobar la eliminacion definitiva de datos de un titular, incluso cuando no hay ningun fundamento de retencion activo: siempre requiere una aprobacion humana explicita, porque una eliminacion es irreversible.
3. Resolver el conflicto entre el principio de minimizacion y una obligacion de conservacion ajena a la LPDP cuando ambas parecen tener el mismo peso: el sistema muestra ambos fundamentos y su plazo, sin decidir cual prevalece.
4. Denegar una solicitud de cancelacion u olvido invocando una regla de retencion: el sistema genera el borrador de denegatoria motivada, pero nunca lo envia automaticamente; siempre requiere la aprobacion explicita del Delegado (y del Aprobador, por el riesgo de reclamo ante la ACE).
5. Certificar que la conservacion electronica de un documento concreto cumple los requisitos de integridad del Art. 13-A de la Ley de Firma Electronica (OBL-RET-06): el sistema solo registra el formato declarado, no certifica su validez tecnica futura.
6. Confirmar que un encargado (por ejemplo, el proveedor de hosting) cuenta como "receptor" que debe notificarse bajo el Art. 21 inc. 3: el sistema aplica por defecto el criterio conservador de tratarlo como receptor, dejando la decision final ajustable por una persona con nota de riesgo.
7. Determinar que la disociacion de un dato es efectiva e irreversible antes de aplicarla como causal de improcedencia de una cancelacion (Art. 10 inciso 2): no se invoca en este caso concreto, pero el sistema nunca lo confirma por si solo cuando se plantea.

### Alertas y escalamientos

| Alerta | Disparador | Nivel | Destinatario | Escalamiento |
|---|---|---|---|---|
| Solicitud choca con un dato retenido por obligacion | Se detecta una regla de MOD-016 en estado Retenido por obligacion sobre el tratamiento de la cartera bancaria | INFO (Responsable ARCO-POL) / WARNING (Delegado) | Responsable ARCO-POL, Delegado | Si no se resuelve 5 dh antes del vencimiento del plazo total, escala al Delegado con prioridad alta |
| Notificacion a receptores pendiente | Procedencia declarada (olvido) con receptores por notificar, faltan 2 dh de los 5 | WARNING | Responsable ARCO-POL | Escala al Delegado si falta 1 dia habil |
| Denegatoria pendiente de notificar | Denegatoria aprobada, faltan dias de los 3 dh | HIGH | Responsable ARCO-POL | Escala al Delegado si falta el ultimo dia habil |
| Plazo general proximo a vencer | Faltan 5 dh de los 20 (o de la prorroga) | HIGH | Responsable ARCO-POL, Delegado | Escala a Administrador si faltan 2 dh |
| Intento de eliminar antes del plazo minimo documental | Un usuario intenta forzar la eliminacion de un documento de cumplimiento antes de su plazo minimo | CRITICAL | Delegado, Responsable Legal, Administrador | Inmediata, sin plazo de espera |
| Reclamo recibido de la Direccion de Proteccion de Datos | Se registra un reclamo dentro del expediente | CRITICAL | Delegado, Legal, Administrador | Escala a Gerencia |

### Evidencia resultante

Vive en MOD-019 Centro de Evidencias, mas la regla de retencion documental del propio expediente y la regla de retencion de los datos bancarios en MOD-016 (esta ultima, independiente del cierre del expediente ARCO-POL):

- Expediente completo con checklist del Art. 18, verificacion de identidad de Wilfredo, historial de estados de ambas ramas (cancelacion y olvido).
- Denegatoria parcial motivada de la cancelacion, con el fundamento de retencion (OBL-RET-01/02/03) y la aprobacion de dos personas distintas, Aprobador y Delegado (OBL-ARCO-12, OBL-PRIN-03).
- Resolucion de reconocimiento del olvido, con evidencia de la eliminacion en el sitio propio (constancia con hash) y de la notificacion al receptor de hosting (OBL-ARCO-04, OBL-ARCO-11, OBL-SEG-05).
- Registro de la confirmacion de Legal sobre la aplicabilidad de la LCLDA al banco, con la advertencia de que requiere asesoria especializada (MOD-016, seccion H.1).
- Registro explicito de la limitacion sobre copias de respaldo (backups), como parte de la respuesta transparente al titular.
- Si se presenta, registro del reclamo ante la Direccion de Proteccion de Datos.

Conservacion: el expediente ARCO-POL, 5 anos desde el cierre (OBL-RET-05); los datos bancarios de Wilfredo que el banco sigue reteniendo por obligacion sectorial, hasta la fecha efectiva mas lejana entre los fundamentos activos (OBL-RET-01, OBL-RET-02, OBL-RET-03), calculada de forma independiente por MOD-016.

### Variantes y casos borde

- **Pyme.** En Ferreteria y Suministros El Roble, una solicitud de cancelacion de un ex-cliente probablemente solo encontraria el fundamento OBL-RET-01 (Codigo de Comercio, si la ferreteria conserva el dato en una factura), sin la complejidad adicional de la LCLDA; Karla Hernandez redactaria y aprobaria la denegatoria parcial con advertencia visible de autorrevision, sin segundo Aprobador por estar bajo el umbral de 50 empleados.
- **Empresa mediana.** En Avicola San Andres, un ex-empleado (como Manuel Pineda del Caso 7) que ademas pidiera la eliminacion de su huella biometrica encontraria que, tras su baja, ya no existe finalidad vigente para conservarla; sin un fundamento de retencion sectorial que lo impida, corresponderia reconocer la cancelacion y ejecutar la eliminacion tecnica en el sistema de control de acceso, con constancia adjunta.
- **Doble estado de la reforma 659.** OBL-CONS-03 no aplica a este caso (no hay revocacion de consentimiento), pero OBL-ARCO-01, 08, 10, 11 y 14 si estan afectadas; si el estado FUTURO se activa a mitad de tramite, el expediente de Wilfredo conserva la regla vigente al momento de tramitarse.
- **Bloqueo cautelar no definido.** Como se senala antes del diagrama, ninguna ficha define un bloqueo automatico del dato de la cartera bancaria mientras se revisa la solicitud de cancelacion (a diferencia de la rectificacion, que si lo tiene); este recorrido lo documenta como hueco en vez de inventar una regla no definida.
- **Solicitud de oposicion o limitacion en lugar de cancelacion.** Si Wilfredo hubiera pedido solo dejar de recibir comunicaciones de mercadeo del banco, el derecho aplicable seria Oposicion (Art. 12, OBL-ARCO-05), no Cancelacion; si hubiera impugnado la exactitud de un dato mientras se verifica, corresponderia Limitacion (Art. 13, OBL-ARCO-06); ninguno de los dos activa por si solo el motor de retencion de MOD-016.

### Cobertura por version

| Funcionalidad | MVP | V1 / V2 |
|---|---|---|
| Formulario interno seguro con verificacion de identidad, plazo 20+20, denegatoria motivada y notificacion a receptores en 5 dh | MUST HAVE | - |
| Registro pasivo de la conservacion de datos de cumplimiento propio (aviso, expediente) sin borrar por defecto | MUST HAVE (comportamiento nativo de MOD-008/MOD-011) | - |
| Motor de retencion de datos del titular con catalogo de fundamentos sectoriales (Codigo de Comercio, Tributario, LCLDA) y calculo del maximo entre ellos | No incluido; la resolucion de conflictos entre normas queda como nota manual en el campo "plazo de conservacion" del RAT (MOD-006) | V1: MOD-016 (SHOULD HAVE), con estado, alerta y borrador automatico de denegatoria parcial |
| Flujo de excepcion con doble aprobacion para forzar una eliminacion anticipada de un documento de cumplimiento | No incluido en el MVP; la proteccion equivalente es que MOD-008/MOD-011 no exponen un boton de borrar | V1, junto con el motor de retencion completo |
| Gestion de retencion de copias de seguridad (backups) tecnicas | Fuera de alcance permanente (anti-feature 11) | Fuera de alcance permanente; no es una fase futura del producto |

### Riesgos especificos del caso y su mitigacion

| Riesgo | Mitigacion de diseno |
|---|---|
| Dar por valido un fundamento sectorial (LCLDA) que en realidad no aplica al banco | Exigir siempre confirmacion humana explicita antes de activar el fundamento, con advertencia visible |
| Eliminar datos bancarios antes de cumplir una obligacion de conservacion simultanea | Calculo del maximo entre todos los fundamentos activos |
| Que el titular entienda la denegatoria parcial como un rechazo total de su solicitud | Notificar ambas resoluciones (cancelacion y olvido) de forma separada y explicita, cada una con su propio fundamento |
| Que la eliminacion de la nota de prensa no se propague a copias indexadas por un buscador externo | Registrar explicitamente esa limitacion como parte de la respuesta, sin prometer un resultado sobre infraestructura de un tercero que el sistema no controla |
| Que un usuario intente forzar el borrado de evidencia de retencion para ocultarla | Bloqueo estructural con doble aprobacion y alerta CRITICAL inmediata al Delegado y al Responsable Legal |

---

## Contradicciones y huecos detectados

### Contradicciones

- **Fundamento citado en `03_modulos/MOD-016_ficha.md` (seccion G, automatizacion 10) para la denegatoria por retencion.** Esa ficha dice: "Generar un borrador de denegatoria parcial motivada con el fundamento correspondiente (Art. 22, OBL-ARCO-06), para revision del Delegado antes de enviarse." Sin embargo, `01_legal/matriz_obligaciones.json` y `03_modulos/MOD-011_ficha.md` (seccion A, tabla de OBL-ID) asignan la cancelacion y el olvido a OBL-ARCO-04 (Art. 10), mientras que OBL-ARCO-06 corresponde a un derecho distinto, Limitacion (Art. 13). Se adopto OBL-ARCO-04 (Art. 10) como fundamento de la denegatoria parcial de cancelacion/olvido en el Paso 7 del Caso 8, porque MOD-011 es el modulo propietario de ambas obligaciones (ARCO-04 y ARCO-06) y su propia tabla de OBL-ID es mas especifica que la referencia colateral de MOD-016 (modulo colaborador), siguiendo la jerarquia "ficha del modulo propietario" sobre "otras fichas".
- **Arista de dependencia MOD-011 hacia MOD-009/MOD-010 no declarada en `02_validacion/mapa_modulos.json`.** `03_modulos/MOD-011_ficha.md` (notas finales, punto 1) senala que el modulo necesita leer el catalogo de receptores/encargados de MOD-009 y el registro de MOD-010 para construir la lista de notificacion a receptores (usada en el Paso 15 del Caso 8), pero `mapa_modulos.json` solo declara la relacion en sentido MOD-011 -> MOD-009/MOD-010 (`alimenta_a`), sin declarar la lectura inversa como `depende_de`. Se adopto la relacion funcional descrita por la propia ficha de MOD-011 (que ya reconoce la omision como pendiente de correccion en el mapa, sin proponer un mecanismo distinto), por ser necesaria para que OBL-ARCO-11 se cumpla de forma automatizada.
- **Arista de dependencia MOD-016 hacia MOD-011/MOD-013 no declarada en `mapa_modulos.json`.** `03_modulos/MOD-016_ficha.md` (seccion L y notas finales, punto 1) senala que su automatizacion G.3 (crear la regla de retencion documental OBL-RET-05 al cerrarse un expediente) necesita leer la fecha de cierre de MOD-011 y de MOD-013, pero `mapa_modulos.json` solo declara `depende_de: [MOD-006, MOD-008]` para MOD-016. Se adopto la relacion funcional descrita por la ficha de MOD-016 (usada en el Paso 16 del Caso 7 y el Paso 20 del Caso 8), por la misma razon que el punto anterior: es necesaria para que OBL-RET-05 opere y la propia ficha ya la documenta como pendiente de reflejar en el mapa, sin contradecir su clasificacion de modulos ni de obligaciones.

### Huecos

- **Bloqueo cautelar durante la revision de una cancelacion o de un olvido:** hueco, no definido en la ficha de MOD-011 (esa ficha solo define un bloqueo cautelar automatico para la rectificacion, Art. 9, OBL-ARCO-03). El Caso 8 lo documenta explicitamente antes del diagrama en vez de inventar una regla equivalente para cancelacion/olvido.
- **Plazo o mecanismo para que un Encargado externo (por ejemplo, un proveedor de hosting) confirme la propagacion de una eliminacion a copias indexadas por un buscador externo:** hueco, no definido en la ficha de MOD-009, de MOD-011 ni de MOD-016. El Paso 14 del Caso 8 lo trata como gestion operativa sin plazo legal propio, sobre infraestructura de un tercero que el sistema no controla.
