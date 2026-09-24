# MODULO: Delegado / Responsable Interno de Datos

Codigo corto del modulo: MOD-002
Clasificacion global del modulo: MUST HAVE (para el MVP)
Obligaciones que cubre: OBL-DPO-01, OBL-DPO-02, OBL-DPO-03, OBL-DPO-04, OBL-DPO-05, OBL-DPO-06, OBL-DPO-07, OBL-DPO-08 (propietario, matriz_obligaciones.json). Colabora en OBL-CAP-02 (propietario MOD-017) y OBL-PLAZO-05 (propietario MOD-024).

Fecha de elaboracion: 2026-09-24. Fecha de referencia del analisis: 2026-09-23/24.

Nota de lectura sobre la reforma 659: en toda esta ficha, "el Decreto Legislativo 659" se cita segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado (decision 2.7.32 de `02_validacion_de_la_idea.md`). Mientras no se confirme su publicacion en el Diario Oficial, el regimen vigente es el del texto actual del Decreto 144 (delegado obligatorio en el sector privado, Arts. 15 y 17).

---

## A. Proposito

- **Por que existe.** Hoy la Ley para la Proteccion de Datos Personales (Decreto Legislativo 144, Arts. 15 y 17) obliga a toda empresa privada salvadorena sujeta a la ley a nombrar un Delegado de Proteccion de Datos Personales, con requisitos de perfil, un tramite de comunicacion a la Agencia de Ciberseguridad del Estado (ACE) con plazo ya corriendo, reverificaciones periodicas, capacitacion anual y un deber de confidencialidad que sobrevive al cese del cargo. Sin un modulo propio, esta figura no tenia a donde vivir dentro del producto: la validacion de la idea la identifico como "el hallazgo estructural mas importante de toda la validacion" (`02_validacion_de_la_idea.md`, decision 2.7.7) porque, enterrada como un campo mas de Organizacion, el motor de tareas no tenia a quien asignar las obligaciones que la ley atribuye especificamente a esta figura.
- **Que problema resuelve para la empresa.** Da a la empresa un lugar unico donde nombrar, documentar, dar seguimiento y demostrar que cumplio con el ciclo de vida completo de su Delegado (o, si la reforma 659 llega a estar vigente, de su Responsable Interno), sin que la persona designada tenga que recordar por su cuenta cinco plazos distintos ni la empresa tenga que reconstruir despues, ante un requerimiento de la ACE, cuando se nombro, cuando se comunico y cuando se reverifico a esa persona.
- **Que obligacion u obligaciones cubre.** Propietario de OBL-DPO-01 a OBL-DPO-08 (Arts. 15 y 17 LPDP; Arts. 8, 9, 10, 18, 22 y 36 de los Lineamientos para el Delegado de Proteccion de Datos Personales de la ACE, D.O. 11-ago-2026, vigentes desde 19-ago-2026). Colabora, sin ser propietario, en OBL-CAP-02 (plan anual de capacitacion del personal que el propio Delegado elabora, Art. 22 Lineamientos DPO, propietario MOD-017) y en OBL-PLAZO-05 (seguimiento del estado de publicacion de la reforma 659, propietario MOD-024, cuya bandera este modulo consulta pero no controla).
- **Que valor aporta.**
  - Operativo: asigna un responsable fijo y localizable para que ARCO-POL (MOD-011), la revocacion del consentimiento (MOD-007) y el deber de asistencia interna (OBL-DPO-08) tengan a quien dirigir la aprobacion, en vez de depender de que alguien recuerde quien es "el delegado" ese mes.
  - Probatorio: concentra el acta de nombramiento, la comunicacion a la ACE, los atestados de reverificacion, la capacitacion y los informes periodicos como evidencia verificable, alineado con el principio de responsabilidad demostrada (OBL-PRIN-03, Art. 5 lit. i, propietario MOD-019).
  - Reduccion de riesgo: modela el doble estado de la reforma 659 con una sola entidad y un interruptor de regimen alojado en MOD-024, de modo que la empresa nunca se queda sin cobertura del modulo por un cambio normativo, y el sistema nunca declara vigente un regimen que aun no fue publicado oficialmente (anti-feature 14 de `22_anti_features.md`).
- **Que NO hace este modulo (limites explicitos).**
  - No actua como el Delegado de la empresa cliente ni ejerce sus funciones legales; es la herramienta que usa la persona (interna o externa) formalmente designada (anti-feature 4).
  - No certifica a la persona ante el "Programa de Certificacion de Delegados de Proteccion de Datos Personales" de la ACE; esa es facultad exclusiva de la Direccion de Proteccion de Datos (Art. 12 Lineamientos DPO; anti-feature 12).
  - No presenta el tramite de comunicacion a la ACE en nombre de la empresa sin que esta lo autorice y ejecute; prepara el contenido y deja evidencia del intento (anti-feature 13).
  - No decide por si mismo si la persona propuesta cumple los requisitos de idoneidad del Art. 5 de los Lineamientos, ni si existe un conflicto de intereses; ofrece el checklist y la declaracion jurada, la valoracion es de la organizacion (ver seccion H).
  - No activa automaticamente el estado FUTURO de la reforma 659 por la sola aprobacion legislativa; ese interruptor vive en MOD-024 y requiere confirmacion manual del equipo del producto tras verificar la publicacion oficial (anti-feature 14, decision 2.7.16).
  - No resuelve por si mismo las solicitudes ARCO-POL; solo identifica quien es hoy el "responsable del tramite" para que MOD-011 le asigne la aprobacion de cada caso.

---

## B. Usuarios

Roles estandar usados (`02_validacion/05_tipos_de_usuario.md`, seccion 5.3):

- **Administrador de la organizacion.** Da de alta el registro de nombramiento (representa a la maxima autoridad que nombra, Art. 6 Lineamientos DPO), invita a la persona designada como usuario del sistema, ve el estado del modulo desde el primer dia (bloqueante en el onboarding si no existe ningun responsable activo) y gestiona el archivado de registros historicos.
- **Delegado de Proteccion de Datos (o Responsable Interno, si el estado FUTURO esta activo).** Usuario principal del modulo: completa y mantiene su propio perfil, acepta la declaracion jurada de conflicto de intereses, adjunta atestados en cada reverificacion, registra su capacitacion anual, elabora el informe periodico con las estadisticas ARCO-POL, y ve la cola de tareas que este modulo genera para el en MOD-021.
- **Responsable ARCO-POL / Responsable del tramite.** En pyme suele ser la misma persona que el Delegado; en empresa mediana o corporativo puede ser un rol distinto que consulta este modulo para saber a quien corresponde aprobar cada caso de MOD-011 y MOD-007 en un momento dado.
- **Responsable Legal / Compliance.** Revisa la suficiencia juridica del acta de nombramiento, participa en la valoracion del conflicto de intereses y de los requisitos de perfil cuando el caso es dudoso, y evalua el impacto legal de un eventual cambio de estado ACTUAL a FUTURO.
- **Responsable de Seguridad / IT.** No administra el modulo, pero recibe y debe atender las peticiones que el Delegado le canalice en ejercicio de sus funciones (OBL-DPO-08); registra evidencia de haberlas atendido.
- **Responsable de area (RRHH, Marketing, Operaciones, etc.).** Igual que Seguridad/IT: atiende las peticiones internas del Delegado y deja constancia, sin acceso de edicion al modulo.
- **Aprobador.** Aprueba el acta de nombramiento antes de considerarla definitiva, aprueba cada reverificacion periodica y aprueba el cambio de tipo_rol cuando la empresa decide mantener voluntariamente la figura de Delegado bajo el estado FUTURO.
- **Auditor (interno).** Solo lectura y exportacion: consulta el historial de nombramientos, informes periodicos y evidencia de asistencia, para el programa de auditoria de cumplimiento (MOD-018). En pyme, si coincide con quien administra el modulo, ve la advertencia de autorrevision descrita en `05_tipos_de_usuario.md`, seccion 5.4.
- **Auditor externo (invitado).** Acceso temporal de solo lectura al expediente del Delegado durante una auditoria puntual, sin capacidad de comentar ni modificar.
- **Usuario de consulta / Colaborador.** Ve unicamente el nombre y el contacto institucional publicado del responsable activo (el mismo dato que aparece en el aviso de privacidad), sin acceso al expediente completo.
- **Titular (formulario externo).** No entra al modulo. Consulta el nombre y contacto del responsable vigente a traves del aviso de privacidad (MOD-008) o del Portal del Titular (MOD-012), generados con el dato que este modulo mantiene actualizado.
- **Asesor externo invitado.** Puede ser invitado a un caso puntual (por ejemplo, dictaminar si una situacion configura conflicto de intereses del Delegado), con acceso acotado a ese expediente especifico y sin licencia permanente.

---

## C. Permisos

| Accion | Admin. organizacion | Delegado / Resp. Interno | Resp. ARCO-POL | Resp. Legal | Resp. Seguridad/IT | Resp. de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Titular externo | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver expediente completo | Si | Si (propio) | Si | Si | No | No | Si | Si | Si (alcance temporal) | No | No | Si (caso asignado) |
| Ver dato publico (nombre/contacto) | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si |
| Crear registro de nombramiento | Si | No | No | Si | No | No | No | No | No | No | No | No |
| Modificar datos de perfil/contacto | Si | Si (propio) | No | No | No | No | No | No | No | No | No | No |
| Aprobar (acta, reverificacion, cambio de tipo_rol) | Si (ver nota) | No | No | Si | No | No | Si | No | No | No | No | No |
| Cerrar (registrar cese) | Si | No | No | Si | No | No | Si | No | No | No | No | No |
| Eliminar / archivar | Si (solo archivar, nunca eliminar historial) | No | No | No | No | No | No | No | No | No | No | No |
| Exportar (reportes, paquete de evidencia) | Si | Si (propio) | No | Si | No | No | No | Si | Si (alcance temporal) | No | No | No |
| Asignar (sustituto, delegado comun) | Si | No | No | No | No | No | Si | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | No | No | Si | No | No | No | No | Si (caso asignado) |
| Adjuntar evidencia (atestados, credencial, informes) | Si | Si | No | Si | No | No | No | No | No | No | No | No |
| Registrar atencion de una peticion canalizada | No | No | No | No | Si | Si | No | No | No | No | No | No |

Separacion de funciones:

- Quien crea o edita el registro de nombramiento no deberia ser tambien quien lo aprueba en empresa mediana o corporativo; en pyme (por debajo del umbral de 50 empleados, `05_tipos_de_usuario.md` 5.4) el sistema permite que Administrador de organizacion cree y apruebe, mostrando siempre la advertencia visible de "autorrevision" [opinion de producto, umbral sin respaldo legal].
- El rol Auditor (interno o externo) es siempre de solo lectura: nunca puede comentar, aprobar ni adjuntar evidencia, para preservar la independencia de su verificacion [opinion de producto].
- Aprobar el cambio de tipo_rol (mantener voluntariamente al Delegado bajo el estado FUTURO, o migrar a Responsable Interno) exige doble control: quien lo propone (tipicamente el propio Delegado o Administrador) no puede ser la unica firma; se requiere ademas Aprobador o Responsable Legal.
- El documento de identidad de la persona designada (dato personal del propio Delegado) solo es visible para Administrador de organizacion, Aprobador y Responsable Legal; cada lectura queda en el historial (seccion O).

---

## D. Informacion de entrada

Precarga: `tipo_rol` se precarga desde la bandera `regimen_reforma_659` de MOD-024; si la persona designada ya existe como usuario en MOD-001, `nombre_completo`, `correo_electronico_institucional` y `telefono_institucional` se precargan desde su perfil de usuario (editable). `plan_capacitacion_personal` no se duplica: es una referencia al mismo registro que administra MOD-017.

Minimizacion de datos personales (privacy by design): los campos de esta seccion describen a la persona designada como Delegado o Responsable Interno, no a titulares externos del cliente. Se limitan a los datos minimos que exigen el Art. 7 de los Lineamientos DPO para el acta de nombramiento y el registro ante la ACE. El numero de documento de identidad se guarda como dato de referencia (numero y tipo), nunca como imagen escaneada, salvo que la propia empresa decida adjuntar una copia como evidencia adicional puntual, con acceso restringido segun la tabla de permisos.

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|
| tipo_rol | Seleccion unica | Obligatorio | DELEGADO, RESPONSABLE_INTERNO | Precargado segun la bandera de MOD-024; editable solo con aprobacion de doble control si difiere del valor por defecto | "Hoy la ley llama a esta persona 'Delegado de Proteccion de Datos'. Si la reforma que la Asamblea ya aprobo llega a publicarse oficialmente, esta figura pasara a llamarse 'Responsable interno' y dejara de ser obligatoria; usted podra decidir si la mantiene de todas formas." | OBL-DPO-01, Arts. 15 y 17; doble estado, MOD-024 |
| modalidad | Seleccion unica | Obligatorio | INTERNO, EXTERNO_PERSONA_NATURAL, EXTERNO_PERSONA_JURIDICA | Si EXTERNO_PERSONA_JURIDICA, exige completar razon_social_persona_juridica y persona_natural_responsable | "Indique si quien ejerce esta funcion es empleado de su empresa, o si fue contratado por fuera, ya sea como persona individual o como firma." | Art. 13 y 14 Lineamientos DPO |
| nombre_completo | Texto | Obligatorio | - | No vacio | "Nombre completo de la persona que ejercera las funciones." | Art. 7 lit. e Lineamientos DPO |
| documento_identidad (numero y tipo) | Texto | Obligatorio (salvo EXTERNO_PERSONA_JURIDICA sin persona natural aun designada) | DUI, Pasaporte, Carnet de residente | Formato segun tipo | "Numero de documento de identidad de la persona designada. Este dato es de acceso restringido dentro del sistema." | Art. 7 lit. e Lineamientos DPO |
| razon_social_persona_juridica | Texto | Obligatorio si modalidad = EXTERNO_PERSONA_JURIDICA | - | No vacio | "Nombre legal de la firma contratada como Delegado externo." | Art. 14 Lineamientos DPO |
| nit_persona_juridica | Texto | Obligatorio si modalidad = EXTERNO_PERSONA_JURIDICA | - | Formato NIT | "Numero de identificacion tributaria de la firma." | Art. 14 Lineamientos DPO |
| persona_natural_responsable (si aplica) | Referencia a otra entidad (persona) | Obligatorio si modalidad = EXTERNO_PERSONA_JURIDICA | - | Debe cumplir el mismo perfil del Art. 5 | "Toda persona juridica designada como Delegado debe nombrar a una persona natural especifica que atienda el dia a dia." | Art. 14 Lineamientos DPO |
| correo_electronico_institucional | Texto | Obligatorio | - | Formato de correo valido | "Correo institucional de contacto. Este dato se publicara en el aviso de privacidad de su empresa." | Art. 7 lit. e Lineamientos DPO |
| telefono_institucional | Texto | Obligatorio | - | Formato telefonico | "Telefono institucional de contacto, tambien visible en el aviso de privacidad." | Art. 7 lit. e Lineamientos DPO |
| direccion_institucional | Texto largo | Opcional (recomendado) | - | - | "Direccion donde puede ubicarse a esta persona por motivos oficiales." | Buena practica, Art. 7 lit. e |
| fecha_nombramiento | Fecha | Obligatorio | - | No puede ser futura | "Fecha en que su organizacion designo formalmente a esta persona. A partir de esta fecha el sistema calcula los plazos legales." | OBL-DPO-01/02/03; Arts. 8 y 10 Lineamientos DPO |
| numero_acuerdo_acta | Texto | Obligatorio | - | No vacio | "Numero del acuerdo, punto de acta o resolucion que respalda el nombramiento." | Art. 7 lit. a Lineamientos DPO |
| fundamento_legal_nombramiento | Texto largo | Obligatorio | - | No vacio | "Explique brevemente quien tomo la decision y con que facultad (por ejemplo, 'Acuerdo de Junta Directiva No. 12')." | Art. 7 lit. d Lineamientos DPO |
| documento_acta_nombramiento | Archivo (PDF) | Obligatorio antes de comunicar a la ACE | - | Formato PDF, tamano maximo configurable | "Adjunte la certificacion del acuerdo o acta con la firma correspondiente." | Art. 6 y 7 Lineamientos DPO |
| plazo_nombramiento | Seleccion unica + fecha_fin si aplica | Obligatorio | INDEFINIDO, PLAZO_FIJO | Si PLAZO_FIJO, exige fecha_fin posterior a fecha_nombramiento | "Indique si el nombramiento es por tiempo indefinido o tiene una fecha de vencimiento." | Art. 7 lit. g Lineamientos DPO |
| requisitos_perfil (checklist) | Seleccion multiple | Obligatorio antes de aprobar | Grado universitario; mayor de 21 anos; experiencia acreditada (proteccion de datos, procedimientos administrativos, cumplimiento normativo, gestion de riesgos, TI, seguridad de la informacion o ciberseguridad); sin sentencia firme por delitos dolosos relacionados; sin sancion firme por infracciones a la LPDP | Ninguna casilla puede quedar sin marcar explicitamente (Si/No) antes de pasar a NOMBRADO | "Marque cada requisito que la persona designada cumple, segun los Lineamientos de la ACE. El sistema no verifica esto por usted: es responsabilidad de su organizacion confirmarlo con la documentacion de respaldo." | Art. 5 Lineamientos DPO; decision no automatizable (seccion H) |
| declaracion_jurada_conflicto_intereses | Booleano + texto si aplica | Obligatorio antes de aceptar el cargo | Sin conflicto declarado / Con situacion declarada (texto libre) | Si "con situacion declarada", exige adjuntar la medida correctiva adoptada | "La persona designada debe declarar si tiene alguna situacion personal que pudiera afectar su independencia (por ejemplo, si tambien decide sobre los fines del tratamiento de datos)." | Art. 9 Lineamientos DPO |
| cargo_funciones_adicionales | Texto | Opcional | - | Si coincide con gerente, subgerente, jefe o cargo de direccion con funciones amplias, dispara advertencia de incompatibilidad | "Indique si la persona ocupa ademas otro cargo dentro de la empresa." | Art. 26, 27 y 28 Lineamientos DPO |
| certificacion_ace_estado | Seleccion unica | Condicional (obligatorio cuando el Programa de Certificacion de la ACE este habilitado) | NO_INICIADA, EN_CURSO, APROBADA, REPROBADA_1_INTENTO, REPROBADA_2_INTENTOS | - | "Estado del examen de certificacion ante la ACE. Este requisito aplica desde que la Agencia lo habilite formalmente." | Art. 5 lit. e, 20 y 21 Lineamientos DPO |
| fecha_comunicacion_ace | Fecha | Se completa al enviar el tramite | - | No anterior a fecha_nombramiento | "Fecha en que se envio la comunicacion del nombramiento a la ACE." | OBL-DPO-03, Art. 10 Lineamientos DPO |
| numero_registro_ace / credencial_ace | Texto | Opcional hasta que la ACE la emita | - | - | "Numero de registro o credencial que la ACE entregue, cuando este disponible." | Art. 11 y 12 Lineamientos DPO |
| fecha_ultima_reverificacion | Fecha (calculada, editable al completar una reverificacion) | Obligatorio a partir de la primera reverificacion | - | - | "Fecha de la ultima vez que se confirmo que el perfil sigue vigente." | OBL-DPO-04, Art. 18 Lineamientos DPO |
| atestados_reverificacion | Archivo (multiple) | Obligatorio en cada reverificacion | - | Formato PDF/imagen | "Adjunte las constancias de capacitacion o certificacion que respaldan la reverificacion." | Art. 18 Lineamientos DPO |
| fecha_ultima_capacitacion_delegado | Fecha | Obligatorio anual | - | - | "Fecha de la ultima capacitacion recibida por esta persona en proteccion de datos." | OBL-DPO-05, Art. 22 Lineamientos DPO |
| plan_capacitacion_personal (referencia) | Referencia a documento (MOD-017/MOD-008) | Obligatorio anual | - | - | "Plan de capacitacion para el resto del personal que esta persona debe elaborar cada ano." | OBL-CAP-02, Art. 22 inciso final Lineamientos DPO |
| informes_periodicos (registro repetible) | Grupo de campos: fecha, periodo cubierto, estadisticas ARCO-POL (referencia), recomendaciones emitidas | Obligatorio al menos dos veces al ano | - | El periodo cubierto no puede solaparse con un informe anterior | "Registre el informe que debe presentar al responsable al menos dos veces al ano." | OBL-DPO-07, Art. 30 Lineamientos DPO |
| recomendaciones_no_acatadas | Texto largo, repetible | Condicional (si el responsable no sigue una recomendacion) | - | - | "Si su recomendacion no fue seguida, dejelo registrado aqui: esto protege su responsabilidad personal como Delegado." | Art. 30 lit. a y Art. 24 inciso final Lineamientos DPO |
| fecha_cese | Fecha | Condicional (al cesar) | - | No anterior a fecha_nombramiento | "Fecha en que la persona dejo de ejercer esta funcion." | Art. 19 Lineamientos DPO |
| motivo_cese | Seleccion unica | Obligatorio si hay fecha_cese | RENUNCIA, FALLECIMIENTO, TERMINACION_DE_CONTRATO, AUSENCIA_TEMPORAL, OTRA (con texto libre) | - | "Seleccione la causa mas cercana. Si ninguna encaja exactamente, use 'Otra' y explique." | Art. 19 Lineamientos DPO |
| clausula_confidencialidad_postcontractual | Booleano + referencia a documento | Obligatorio en el contrato o acta | - | - | "Confirme que el contrato o acta incluye la clausula de confidencialidad que se mantiene 5 anos despues del cese." | OBL-DPO-06, Art. 36 Lineamientos DPO |
| delegado_comun_grupo_societario | Booleano | Opcional (fuera del MVP, ver seccion Q) | - | - | "Marque si esta misma persona es Delegado de otras sociedades de su mismo grupo empresarial." | Art. 16 Lineamientos DPO; decision 2.7.31 |
| delegado_sustituto (referencia) | Referencia a otro registro | Opcional | - | Debe cumplir el mismo perfil del Art. 5 | "Puede designar a una o mas personas que suplan a este Delegado en caso de ausencia." | Art. 17 Lineamientos DPO |

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Registro activo "Responsable del Programa de Datos" | Todos los campos vigentes de la seccion D | Registro en pantalla | Al completar el alta | Toda persona con permiso de ver expediente o dato publico |
| Historial de nombramientos | Registros anteriores, con motivo de cierre o cambio | Registro en pantalla, exportable | Cada vez que cambia la persona o el tipo_rol | Delegado, Aprobador, Legal, Auditor |
| Tareas automaticas en MOD-021 | Ver lista completa en seccion G | Tarea con titulo, fundamento, responsable, fecha | Al disparar cada automatizacion | Persona asignada segun la regla |
| Contadores de plazo en MOD-023 | Dias habiles restantes para cada obligacion con plazo | Indicador numerico | Continuo, recalculado cada dia habil | Delegado, Administrador, Aprobador |
| Evento saliente "tramite de nombramiento" | Estado del tramite ante la ACE (Preparado, Enviado, Confirmado, Rechazado) | Registro en MOD-024, submodulo Tramites ante la ACE | Al enviar la comunicacion del nombramiento | MOD-024, Administrador, Legal |
| Borrador de clausula de confidencialidad | Texto de clausula para incorporar al contrato/acta | Documento borrador | Al crear un registro de modalidad EXTERNO | MOD-008, Delegado, Legal |
| Contacto ARCO-POL derivado | Nombre, correo, telefono del responsable activo | Variable de plantilla | Cada vez que otro modulo genera un documento que lo requiere | MOD-008 (aviso de privacidad), MOD-011 (respuestas ARCO-POL) |
| Evento de auditoria | Cada creacion, edicion, aprobacion, adjunto, exportacion o acceso a dato restringido | Registro tecnico inmutable | En cada accion | AuditLog transversal, Auditor |
| Indicadores de dashboard | Ver seccion M | Semaforo, numero, badge | Continuo | Gerencia, Responsable, Legal, Auditor |
| Informe de gestion periodico | Estadisticas ARCO-POL, recomendaciones, seguimiento | Documento PDF exportable | Cada vez que se registra un informe periodico | Delegado, Aprobador, Auditor, Legal |

---

## F. Workflow

```
                    (1) completar datos obligatorios
                        + checklist de perfil
      [BORRADOR] ------------------------------------> [PENDIENTE_ACEPTACION]
                                                                |
                                                                | (2) persona designada
                                                                |     firma declaracion jurada
                                                                |     y acepta el cargo
                                                                v
                                                          [NOMBRADO]
                                                                |
                                                                | (3) notificacion interna
                                                                |     completada (<=3 dias habiles)
                                                                v
                                                    [NOTIFICADO_INTERNAMENTE]
                                                                |
                                                                | (4) tramite enviado a la ACE
                                                                |     (<=15 dias habiles)
                                                                v
                                                     [COMUNICADO_A_ACE] -----(4b) ACE no inscribe----> [RECHAZADO_ACE]
                                                                |                                              |
                                                                | (5) credencial recibida                      | (10 dias habiles,
                                                                |     o plazo de emision agotado                |  designar otro Delegado)
                                                                v                                              |
                                                           [ACTIVO] <-------------------------------------------+
                                                          /   |   \
             (6) faltan 30 dias para 3 anos             /    |    \    (9) fecha_cese registrada
                 desde nombramiento/reverificacion      v     |     v
                                          [EN_REVERIFICACION] |  [CESADO]
                                                    |         |      |
                          (6b) atestados aprobados  |         |      | (10 dias habiles,
                                                     v         |      |  designar sustituto)
                                                [ACTIVO] <-----+      v
                                                                  [nuevo BORRADOR]
                                                                       |
                                                                       | tras 5 anos desde
                                                                       | el cese (OBL-DPO-06)
                                                                       v
                                                              [ARCHIVADO]
```

Nota de diseno (decision de doble estado, `06_mapa_definitivo_de_modulos.md`, seccion 5): el cambio de `tipo_rol` entre DELEGADO y RESPONSABLE_INTERNO no es una transicion de estado del workflow anterior; es un cambio de atributo sobre el mismo registro ACTIVO, disparado por el evento externo "la bandera de MOD-024 pasa a FUTURO" (automatizacion 9, seccion G) mas la confirmacion humana de la empresa (seccion H). El registro conserva su historial de estados sin reiniciarse.

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (ninguno) | Iniciar alta | Ninguna | BORRADOR | Administrador de organizacion, Responsable Legal | Crea el registro; sin efectos de plazo todavia |
| BORRADOR | Completar datos obligatorios y checklist de perfil | Todos los campos obligatorios de la seccion D sin fecha_comunicacion_ace completos; checklist con cada casilla marcada Si/No | PENDIENTE_ACEPTACION | Administrador de organizacion | Evento de auditoria; no genera tareas aun |
| PENDIENTE_ACEPTACION | Aceptar el cargo (declaracion jurada) | La persona designada firma/acepta digitalmente la declaracion jurada | NOMBRADO | Persona designada como Delegado/Responsable Interno | Se fija fecha_nombramiento; se calcula el limite de 3 dias habiles (MOD-023); se crea la tarea "Notificar al Delegado" en MOD-021; evidencia J1 y J4 |
| NOMBRADO | Registrar notificacion interna completada | Se adjunta constancia de notificacion (medio idoneo, Art. 8) | NOTIFICADO_INTERNAMENTE | Administrador de organizacion | Se calcula el limite de 15 dias habiles para comunicar a la ACE; se crea tarea correspondiente; evidencia J2 |
| NOTIFICADO_INTERNAMENTE | Enviar comunicacion a la ACE | documento_acta_nombramiento adjunto; requisitos_perfil completo | COMUNICADO_A_ACE | Administrador de organizacion, Responsable Legal | Evento saliente hacia MOD-024 (Tramites ante la ACE); evidencia J3 |
| COMUNICADO_A_ACE | Registrar credencial recibida o vencer el plazo de emision sin rechazo | numero_registro_ace completado, o transcurridos 15 dias habiles sin observacion de la ACE | ACTIVO | Administrador de organizacion | Contacto ARCO-POL derivado queda disponible para MOD-007, MOD-008, MOD-011; indicadores de dashboard pasan a Verde |
| COMUNICADO_A_ACE | La ACE notifica que no inscribe al Delegado | Notificacion formal de incumplimiento de requisitos (Art. 12 Lineamientos DPO) | RECHAZADO_ACE | Administrador de organizacion (registra el resultado) | Alerta CRITICAL; cuenta atras de 10 dias habiles para nombrar a otra persona |
| RECHAZADO_ACE | Iniciar nuevo nombramiento | Ninguna adicional | BORRADOR (nuevo registro) | Administrador de organizacion | El registro anterior queda archivado con motivo "rechazado por la ACE", sin eliminarse |
| ACTIVO | Se cumplen 3 anos menos 30 dias desde nombramiento o ultima reverificacion | Automatico (evento de calendario, MOD-023) | EN_REVERIFICACION | Sistema (automatizacion, ver seccion G) | Tarea "Reverificar perfil" en MOD-021; alerta segun seccion I |
| EN_REVERIFICACION | Aprobar reverificacion | atestados_reverificacion adjuntos y checklist reconfirmado | ACTIVO | Aprobador | Se actualiza fecha_ultima_reverificacion; evidencia J5 |
| EN_REVERIFICACION | Vencer sin completar | Transcurre la fecha limite de 3 anos sin reverificacion registrada | ACTIVO (con alerta HIGH persistente) | Sistema | El registro no pasa a un estado bloqueante distinto (la ley no lo exige), pero el indicador de dashboard pasa a Rojo hasta regularizarse |
| ACTIVO | Registrar cese | fecha_cese y motivo_cese completos | CESADO | Administrador de organizacion, Aprobador | Se activa el contador de confidencialidad post-cese (5 anos, OBL-DPO-06); tarea "Designar sustituto" con vencimiento a 10 dias habiles (OBL-DPO-01, continuidad de la figura; Art. 19 Lineamientos DPO); el contacto ARCO-POL derivado queda vacante y MOD-011 muestra advertencia |
| CESADO | Designar sustituto | Se completa un nuevo registro hasta NOMBRADO | (nuevo BORRADOR arranca su propio ciclo) | Administrador de organizacion | El registro CESADO queda archivado, visible en el historial, con el periodo de confidencialidad corriendo |
| CESADO (archivado) | Transcurren 5 anos desde fecha_cese | Automatico | ARCHIVADO | Sistema | Se cierra la obligacion de confidencialidad activa en el sistema; el registro permanece disponible como historico, nunca se elimina (anti-feature 19) |

Registros vinculados: al cesar o archivar un registro, las tareas pendientes que dependian de esa persona (por ejemplo, un informe periodico a medio elaborar) no se eliminan: se marcan "pendiente de reasignar" y quedan visibles para el Administrador hasta que se asignen al nuevo responsable, preservando el historial (principio heredado de `06_mapa_definitivo_de_modulos.md`, seccion 5, punto 6).

---

## G. Automatizaciones

1. **Disparador:** el registro pasa a NOMBRADO. **Condicion:** ninguna. **Accion:** calcular la fecha limite de notificacion interna (fecha_nombramiento + 3 dias habiles, via MOD-023) y crear la tarea "Notificar al Delegado su nombramiento" en MOD-021, asignada a Administrador de organizacion. Configurable: el plazo legal no; el canal de recordatorio si.
2. **Disparador:** el registro pasa a NOTIFICADO_INTERNAMENTE. **Condicion:** ninguna. **Accion:** calcular la fecha limite de comunicacion a la ACE (fecha_nombramiento + 1 dia + 15 dias habiles) y crear la tarea "Comunicar el nombramiento a la ACE", mas un evento "Tramite pendiente" visible en MOD-024. Configurable: no en el plazo.
3. **Disparador:** se edita cualquier campo de contacto o modalidad de un registro ACTIVO. **Condicion:** el registro ya fue comunicado a la ACE. **Accion:** calcular la fecha limite de actualizacion ante la ACE (+10 dias habiles, Art. 10 inciso final) y crear la tarea correspondiente. Configurable: no.
4. **Disparador:** faltan 30 dias para cumplir 3 anos desde el nombramiento o la ultima reverificacion. **Condicion:** el registro esta ACTIVO. **Accion:** crear la tarea "Reverificar perfil del Delegado" y, si llega la fecha sin completarse, mover el registro a EN_REVERIFICACION. Configurable: el margen de anticipacion (30 dias) si; el plazo legal de 3 anos no.
5. **Disparador:** faltan 30 dias para cumplir 1 ano desde la ultima capacitacion registrada del Delegado. **Condicion:** ninguna. **Accion:** crear la tarea "Renovar capacitacion anual del Delegado". Configurable: el margen si, el plazo legal no.
6. **Disparador:** transcurren 6 meses desde el ultimo informe periodico registrado (o desde fecha_nombramiento si es el primero). **Condicion:** ninguna. **Accion:** crear la tarea "Elaborar informe periodico al responsable" y precargar, solo como referencia de lectura, las estadisticas ARCO-POL del periodo desde MOD-011, sin alterar los expedientes originales. Configurable: la periodicidad minima (6 meses) es el minimo legal; la empresa puede acortarla, no alargarla.
7. **Disparador:** se registra fecha_cese. **Condicion:** ninguna. **Accion:** mover el registro a CESADO, crear la tarea "Designar sustituto" con vencimiento a 10 dias habiles (OBL-DPO-01, continuidad de la figura; Art. 19 Lineamientos DPO), y marcar el inicio del periodo de confidencialidad post-cese de 5 anos sobre el historial del registro. Configurable: no.
8. **Disparador:** la bandera `regimen_reforma_659` de MOD-024 cambia de ACTUAL a FUTURO. **Condicion:** ninguna (evento regulatorio global). **Accion:** para cada registro ACTIVO, crear la tarea "Revisar si mantiene esta figura de forma voluntaria" dirigida a Administrador de organizacion, sin cambiar automaticamente `tipo_rol` (ver seccion H); actualizar la etiqueta de clasificacion visible de OBL-DPO-02 a 08 de OBLIGATORIO/CONDICIONAL a "opcional bajo el regimen vigente", preservando la clasificacion anterior en el historial. Configurable: no.
9. **Disparador:** cualquier otro modulo genera un documento que necesita el contacto del "responsable del tramite" (aviso de privacidad en MOD-008, respuesta ARCO-POL en MOD-011). **Condicion:** existe un registro ACTIVO. **Accion:** insertar el dato de contacto vigente como variable de plantilla, por referencia, sin duplicarlo. Configurable: no.
10. **Disparador:** un usuario de Seguridad/IT o de un area marca como atendida una peticion canalizada por el Delegado. **Condicion:** ninguna. **Accion:** registrar el evento en la bitacora de asistencia interna (evidencia de OBL-DPO-08). Configurable: no.
11. **Disparador:** se registra una recomendacion no acatada por el responsable (campo `recomendaciones_no_acatadas`). **Condicion:** ninguna. **Accion:** dejar constancia con fecha y usuario, visible en el informe periodico y en el historial, sin bloquear ningun flujo. Configurable: no.

---

## H. Decisiones que NO debe automatizar

1. **Si la persona propuesta cumple realmente el perfil exigido** (grado universitario, mayor de 21 anos, experiencia acreditada, ausencia de sentencias o sanciones firmes, Art. 5 Lineamientos DPO). El sistema solo ofrece el checklist de autoevaluacion. Texto que muestra el sistema: "Requiere validacion de la organizacion o asesoria especializada." Por que: verificar antecedentes penales, titulos y sanciones firmes exige constatar documentos originales que el sistema no puede validar por si mismo.
2. **Si existe conflicto de intereses real, potencial o aparente** (Arts. 9, 27 y 28 Lineamientos DPO). El sistema registra la declaracion jurada y advierte sobre cargos tipicamente incompatibles (gerente, subgerente, jefe con funciones amplias de direccion), pero no decide si el caso concreto configura conflicto. Mismo texto de advertencia. Por que: exige un juicio sobre independencia funcional que es materia de criterio organizacional o juridico, no un hecho verificable automaticamente.
3. **Decidir si mantener voluntariamente la figura de Delegado, o migrar a Responsable Interno sin certificacion ACE, tras confirmarse el estado FUTURO de la reforma 659.** El sistema notifica el cambio y ofrece la opcion (automatizacion 8), pero no ejecuta el cambio de `tipo_rol` sin aprobacion explicita. Mismo texto de advertencia. Por que: es una decision estrategica y de riesgo reputacional de la empresa, no un hecho que el sistema pueda inferir.
4. **Aprobar o rechazar el resultado del "Programa de Certificacion de Delegados" de la ACE.** El sistema solo registra el estado que la empresa o la ACE informen (`certificacion_ace_estado`); no evalua examenes ni emite certificaciones. Por que: es facultad exclusiva de la Direccion de Proteccion de Datos de la ACE (Art. 12 Lineamientos DPO, anti-feature 12).
5. **Redactar con fuerza legal el acuerdo o acta de nombramiento ante la maxima autoridad de la empresa** (Junta Directiva, Administrador Unico, Consejo Directivo, segun corresponda). El sistema ofrece una plantilla guia; la validez juridica del acto societario que designa al Delegado es responsabilidad de la organizacion. Mismo texto de advertencia. Por que: es un acto corporativo interno que el software no puede sustituir (anti-feature 17).
6. **Calificar la causal exacta de un cese cuando no encaja claramente en una de las opciones listadas** (renuncia, fallecimiento, terminacion de contrato, ausencia temporal). El sistema pide elegir la mas cercana con texto libre adicional, sin inferirla. Por que: la causal puede tener efectos legales o laborales distintos que el sistema no esta en condiciones de determinar.
7. **Certificar que el tramite ante la ACE fue efectivamente recibido y aceptado**, especialmente mientras la plataforma oficial del Registro de Delegados de la ACE no este plenamente operativa. El sistema deja evidencia del intento de envio (fecha, documento remitido), no certifica la recepcion por un sistema externo fuera de su control. Por que: depende de la disponibilidad e implementacion del canal oficial de la ACE, que a la fecha de este analisis aun no esta plenamente habilitado (ver seccion 8, incertidumbre 3, de `01_legal/03_hallazgos_regulatorios.md`; anti-feature 13).

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Falta nombrar Delegado/Responsable Interno | No existe ningun registro ACTIVO al finalizar el onboarding (MOD-003) | CRITICAL | Administrador de organizacion | Plataforma + correo | Diaria hasta resolver | A Aprobador a los 5 dias habiles | Existe un registro que llega a ACTIVO |
| Notificacion interna por vencer | Falta 1 dia habil para el limite de 3 dias habiles (Art. 8) | WARNING | Administrador de organizacion | Plataforma + correo | Una vez | A Aprobador si vence | Tarea de notificacion completada |
| Notificacion interna vencida | Vencio el plazo de 3 dias habiles sin completarse | HIGH | Administrador de organizacion, Aprobador | Plataforma + correo | Diaria | A quien tenga el rol Aprobador a las 48 horas | Tarea completada |
| Comunicacion a la ACE por vencer | Faltan 3 dias habiles para el limite de 15 dias habiles (Art. 10) | WARNING | Administrador de organizacion, Delegado | Plataforma + correo | Una vez | A Aprobador | Tramite marcado Enviado |
| Comunicacion a la ACE vencida | Vencio el plazo de 15 dias habiles sin enviar el tramite | CRITICAL | Administrador de organizacion, Aprobador, Responsable Legal | Plataforma + correo | Diaria | Visible en el dashboard de Gerencia | Tramite marcado Enviado |
| Actualizacion ante la ACE pendiente | Se edito el perfil activo y faltan 2 dias habiles para el limite de 10 dias habiles | WARNING | Administrador de organizacion | Plataforma + correo | Una vez | A Aprobador | Tramite de actualizacion marcado Enviado |
| Reverificacion proxima a vencer | Faltan 30 dias para cumplir 3 anos desde el nombramiento o ultima reverificacion (Art. 18) | INFO, sube a WARNING a 10 dias | Delegado, Administrador de organizacion | Plataforma + correo | Semanal desde 30 dias | A Aprobador a los 10 dias sin atender | Reverificacion completada y aprobada |
| Reverificacion vencida | Paso la fecha de 3 anos sin reverificar | HIGH | Administrador de organizacion, Aprobador, Responsable Legal | Plataforma + correo | Diaria | Visible en el dashboard de Gerencia | Reverificacion completada |
| Capacitacion anual del Delegado proxima a vencer | Faltan 30 dias para cumplir 1 ano desde la ultima capacitacion (Art. 22) | INFO, sube a WARNING a 10 dias | Delegado | Plataforma + correo | Semanal | A Administrador de organizacion a los 10 dias | Capacitacion registrada |
| Informe periodico pendiente | Transcurrieron 6 meses sin registrar informe (Art. 30) | WARNING | Delegado, Administrador de organizacion | Plataforma + correo | Mensual desde que vence | A Responsable Legal a los 30 dias de retraso | Informe registrado |
| Sustituto no designado tras cese | Vencen 10 dias habiles desde fecha_cese sin un nuevo registro en NOMBRADO | CRITICAL | Administrador de organizacion, Aprobador | Plataforma + correo | Diaria | Visible en el dashboard de Gerencia | Nuevo registro llega a NOMBRADO |
| Cambio de estado regulatorio (reforma 659) | La bandera de MOD-024 cambia a FUTURO | INFO | Administrador de organizacion, Delegado, Responsable Legal | Plataforma + correo | Una vez | No aplica (informativa) | Se confirma la lectura de la notificacion |
| Confidencialidad post-cese proxima a expirar | Faltan 60 dias para cumplir 5 anos desde el cese (OBL-DPO-06) | INFO | Responsable Legal, Administrador de organizacion | Plataforma | Una vez | No aplica | Transcurre la fecha; el registro pasa a ARCHIVADO |

---

## J. Evidencia

| Evidencia | Como se conserva | Obligacion que prueba | Retencion |
|---|---|---|---|
| Acta o acuerdo de nombramiento (archivo con hash) | Adjunto con fecha, usuario que lo cargo y version | OBL-DPO-01, Art. 15 y 17 | Historico indefinido, nunca se elimina (solo se archiva junto al registro) |
| Constancia de notificacion interna al designado | Registro con fecha, hora y usuario que la genero | OBL-DPO-02, Art. 8 | Igual que el expediente del nombramiento |
| Comprobante de envio del tramite a la ACE y su resultado (credencial o rechazo) | Registro con fecha de envio, documento remitido y respuesta recibida | OBL-DPO-03, Art. 10 | Igual que el expediente del nombramiento |
| Declaracion jurada de conflicto de intereses firmada/aceptada | Registro con fecha y contenido declarado | Diligencia previa a la aceptacion del cargo, Art. 9 | Igual que el expediente del nombramiento |
| Atestados de capacitacion o certificacion en cada reverificacion | Archivo versionado, cada reverificacion conserva su propio conjunto de atestados | OBL-DPO-04, Art. 18 | Historico completo, sin sobrescribir versiones anteriores |
| Registro de capacitacion anual del Delegado | Registro con fecha, contenido y proveedor de la capacitacion | OBL-DPO-05, Art. 22 | Historico completo |
| Clausula de confidencialidad y evento de inicio del periodo post-cese | Referencia al documento contractual mas fecha de activacion del contador | OBL-DPO-06, Art. 36 | 5 anos desde el cese (regla propia del modulo, referenciada como retencion documental de cumplimiento en MOD-016) |
| Informes periodicos con estadisticas ARCO-POL y recomendaciones (incluidas las no acatadas) | Registro exportable con fecha, periodo y firma de quien lo presento | OBL-DPO-07, Art. 30 | Historico completo, no se elimina |
| Bitacora de peticiones internas canalizadas y su atencion por cada area | Registro con fecha, area, peticion y evidencia de respuesta | OBL-DPO-08, Art. 17 LPDP | Alineada al expediente relacionado (por ejemplo, el incidente o el caso ARCO-POL que origino la peticion) |
| Historial de cambios de `tipo_rol` (DELEGADO / RESPONSABLE_INTERNO) | Registro con fecha, usuario, motivo (activacion de bandera de MOD-024 o decision voluntaria) | OBL-PRIN-03, Art. 5 lit. i (responsabilidad demostrada, propietario MOD-019) | Historico indefinido |

Todo evento de esta tabla queda ademas en el AuditLog transversal de solo escritura por adicion (append-only), y toda exportacion hacia el paquete de evidencias de MOD-019 incluye un mecanismo propio de verificacion de integridad (hash o firma), conforme a la decision 2.7.24 de `02_validacion_de_la_idea.md`.

---

## K. Documentos asociados

- **Documentos requeridos como entrada:** acta o acuerdo de nombramiento (Art. 7 Lineamientos DPO); curriculum vitae de la persona designada; contrato de servicios profesionales si la modalidad es externa; documentos que acrediten la existencia legal de la persona juridica designada, cuando aplica (Art. 10 inciso 2).
- **Documentos generados:** constancia de notificacion interna (Art. 8); comunicacion o tramite enviado a la ACE (Art. 10); constancia de reverificacion periodica; informe periodico de gestion (Art. 30); registro de cese y de designacion de sustituto.
- **Plantillas que el sistema provee:**
  - "Modelo de acta de nombramiento de Delegado / Responsable Interno" (variables: razon social, datos de la persona designada, fecha, fundamento legal). Requiere validacion de la organizacion antes de usarse.
  - "Modelo de declaracion jurada de conflicto de intereses" (variables: nombre, cargo, situacion declarada). Requiere validacion de la organizacion.
  - "Modelo de clausula de confidencialidad post-cese" para incorporar al contrato o acta (variable: plazo de 5 anos). Requiere validacion de la organizacion o asesoria especializada antes de incorporarse a un contrato firmado.
  - "Formato de informe periodico al responsable" (variables: periodo cubierto, estadisticas ARCO-POL precargadas por referencia, recomendaciones, recomendaciones no acatadas).
- **Anexos y evidencias documentales:** credencial emitida por la ACE (cuando este disponible), atestados de capacitacion o certificacion, comprobantes de envio del tramite ante la ACE.

---

## L. Dependencias

```
MOD-001 Organizacion y Personas              MOD-023 Calendario y Motor de Plazos
  (usuarios, estructura, maxima autoridad)        (dias/horas habiles, ver nota abajo)
              |                                              |
              v                                              v
              +--------------> MOD-002 <--------------------+
              |          Delegado / Responsable              |
              |               Interno de Datos                |
              |                     ^                          |
              |                     | bandera regimen_659       |
              |                     |                           |
              |              MOD-024 Centro Regulatorio ---------+
              |             (doble estado + Tramites ACE)
              v
   +----------+----------+----------+----------+----------+----------+
   v          v          v          v          v          v          v
MOD-007    MOD-008    MOD-011    MOD-017    MOD-018    MOD-021    MOD-024
Consenti-  Documentos ARCO-POL  Capacita-  Auditoria  Centro de  Tramites
miento     y Politicas (respon- cion       de Cumpli- Tareas     ante la
(destino   (contacto  sable del (capacita- miento     (tareas    ACE
de revo-   publicado) tramite)  cion del   (informes  generadas) (evento
cacion)                          Delegado)  periodicos               saliente)
                                             como
                                             evidencia)
```

- **Entra desde MOD-001** (Organizacion y Personas): identidad de la persona designada como usuario del sistema, estructura organizacional y quien representa a la maxima autoridad que aprueba el nombramiento.
- **Entra desde MOD-024** (Centro Regulatorio): la bandera `regimen_reforma_659` (ACTUAL/FUTURO) que determina el valor por defecto de `tipo_rol`.
- **Entra desde MOD-023** (Calendario y Motor de Plazos): el servicio unico de calculo de dias y horas habiles que MOD-002 consulta para los contadores de 3, 10 y 15 dias habiles y de 1, 3 y 5 anos (decision 2.7.15 de `02_validacion_de_la_idea.md`, que nombra explicitamente a "Delegado" como uno de los cuatro consumidores del motor de plazos). Ver nota de discrepancia al final de esta ficha.
- **Sale hacia MOD-007** (Consentimiento): el nombre de quien es hoy el "responsable del tramite" determina a quien se dirige la notificacion de revocacion del consentimiento (nota reforma 659 de MOD-007 en `06_mapa_definitivo_de_modulos.md`).
- **Sale hacia MOD-008** (Documentos y Politicas): el contacto institucional publicado en el aviso de privacidad y la clausula de confidencialidad del contrato.
- **Sale hacia MOD-011** (ARCO-POL): quien es hoy el responsable del tramite, incluida la rama de reclamo del titular ante la Direccion de Proteccion de Datos de la ACE.
- **Sale hacia MOD-017** (Capacitacion): la capacitacion especifica anual del Delegado y el plan de capacitacion del personal que el mismo elabora (OBL-CAP-02).
- **Sale hacia MOD-018** (Auditoria de Cumplimiento): los informes periodicos del Delegado como insumo de evidencia para el programa anual de auditoria.
- **Sale hacia MOD-021** (Centro de Tareas): todas las tareas descritas en la seccion G.
- **Sale hacia MOD-024** (Tramites ante la ACE): el evento saliente del tramite de comunicacion del nombramiento, para su seguimiento como tramite pendiente ante la autoridad.

**Que ocurre si el modulo dependiente no existe en el MVP:** todos los modulos hacia los que MOD-002 alimenta son MUST HAVE, salvo MOD-018 (SHOULD HAVE, ver `06_mapa_definitivo_de_modulos.md`). Si MOD-018 aun no esta disponible, los informes periodicos se generan y archivan igual dentro de MOD-002 (sirven como evidencia autonoma) y quedan disponibles para cuando MOD-018 se active, sin perdida de historial.

**Nota de discrepancia detectada respecto al mapa definitivo (senalada, no corregida sobre el documento fuente):** la ficha de MOD-023 en `06_mapa_definitivo_de_modulos.md` declara explicitamente "Sale hacia MOD-002" entre sus dependencias, y la decision 2.7.15 nombra a "Delegado" como uno de los cuatro consumidores del motor de plazos unico. Sin embargo, la propia ficha de MOD-002 (misma fuente, y el arreglo `depende_de` de `mapa_modulos.json`) no incluye a MOD-023 en su lista de entrada ("entra desde MOD-001, MOD-024"), solo en su lista de salida ("sale hacia... MOD-023"). Es una asimetria de documentacion: MOD-023 declara que envia a MOD-002, pero MOD-002 no declara que recibe de MOD-023. Esta ficha modela la dependencia real (MOD-002 consulta a MOD-023 para todos sus contadores de plazo, coherente con la decision 2.7.15) y recomienda agregar "MOD-023" a la lista `depende_de` de MOD-002 en `mapa_modulos.json` y a "entra desde" en `06_mapa_definitivo_de_modulos.md` para cerrar la asimetria.

---

## M. Dashboard

| Indicador | Formula / definicion | Semaforo | Vista por rol |
|---|---|---|---|
| Estado del nombramiento | Verde: ACTIVO sin plazos vencidos. Amarillo: algun plazo vence en los proximos 5 dias habiles. Rojo: no existe registro ACTIVO, o hay un plazo legal (OBL-DPO-01/02/03) vencido | Si | Gerencia, Responsable |
| Dias habiles para la proxima obligacion | Minimo entre las fechas limite de notificacion interna, comunicacion ACE, reverificacion, capacitacion e informe periodico, menos la fecha de hoy, en dias habiles (via MOD-023) | Si (colorea segun cercania) | Responsable, Legal |
| Informes periodicos entregados en el ultimo ano vs. minimo legal | Conteo de registros en `informes_periodicos` con fecha en los ultimos 12 meses, contra el minimo de 2 (Art. 30) | Si | Legal, Auditor |
| Estado regulatorio vigente | Badge ACTUAL / FUTURO, tomado de MOD-024, con fecha del ultimo cambio | No (informativo) | Todas |
| Evidencia disponible del modulo | Conteo "X de Y evidencias requeridas disponibles" (acta, declaracion jurada, atestados de la ultima reverificacion, informes periodicos del periodo vigente). Nunca se expresa como porcentaje de cumplimiento legal | Si | Auditor, Legal |
| Alertas activas del modulo | Conteo por nivel (INFO, WARNING, HIGH, CRITICAL) | Si | Gerencia (solo HIGH/CRITICAL), Responsable (todas) |

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Ficha del responsable del programa de datos | Datos vigentes del registro ACTIVO mas resumen del historico | Por organizacion, por periodo | PDF | Auditoria interna, asesor externo | Si |
| Bitacora de plazos del Delegado | Todos los plazos calculados por MOD-023 para este modulo, cumplidos y vencidos, con fechas | Por rango de fechas, por tipo de plazo | XLSX, CSV | Gerencia, Junta Directiva | Si |
| Paquete de evidencia del Delegado | Acta, declaracion jurada, atestados, informes periodicos, comunicaciones a la ACE, con manifiesto y hash de integridad | Por periodo, por estado del regimen (ACTUAL/FUTURO) | ZIP con manifiesto firmado | Auditoria anual (MOD-018), requerimiento de la ACE | Si (via MOD-019) |
| Informe de gestion periodico del Delegado | Estadisticas ARCO-POL del periodo, recomendaciones emitidas, seguimiento a las no acatadas | Por periodo cubierto | PDF | Responsable de la organizacion, Junta Directiva | Si |

---

## O. Historial

Eventos que quedan en el historial del modulo y en la auditoria transversal (AuditLog):

- Creacion del registro (quien, cuando).
- Cada cambio de campo, con valor anterior y valor nuevo (por ejemplo, cambio de correo institucional o de modalidad).
- Cambios de estado del workflow (seccion F), con fecha y usuario que los ejecuto.
- Cambio de `tipo_rol` (DELEGADO <-> RESPONSABLE_INTERNO), con motivo: activacion de la bandera de MOD-024, o decision voluntaria de la empresa (con la aprobacion de doble control registrada).
- Asignaciones: quien fue nombrado, quien fue designado sustituto, a quien se reasigno una tarea pendiente tras un cese.
- Aprobaciones: quien aprobo el acta de nombramiento, quien aprobo cada reverificacion, quien aprobo el cambio de `tipo_rol`.
- Adjuntos: acta de nombramiento, atestados, credencial de la ACE, informes periodicos.
- Exportaciones: quien exporto que reporte, cuando, y con que alcance (por ejemplo, un auditor externo exportando el expediente completo).
- Accesos de lectura al dato de identidad de la persona designada (documento_identidad), por ser un dato personal de acceso restringido.
- Eliminaciones o archivados: nunca hay eliminacion real de un registro, solo archivado, siempre con motivo registrado (rechazo de la ACE, cese, vencimiento del periodo de confidencialidad).
- Envios del tramite a la ACE y su resultado (credencial recibida, rechazo, o falta de respuesta al vencer el plazo).

---

## P. Riesgos

**Riesgos legales**

- Tratar el estado FUTURO de la reforma 659 como vigente antes de su publicacion oficial, dejando de nombrar Delegado cuando la ley todavia lo exige. **Mitigacion de diseno:** la bandera vive exclusivamente en MOD-024, se activa manualmente solo tras verificar la publicacion oficial (nunca por la fecha de aprobacion legislativa), y el modulo muestra siempre el banner "Decreto Legislativo 659, segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado" mientras la bandera sea ACTUAL (anti-feature 14).
- Que el checklist de perfil (Art. 5) se interprete como una validacion del sistema sobre la idoneidad del Delegado. **Mitigacion:** se presenta siempre como autoevaluacion de la empresa, con el texto de advertencia estandar (seccion H, decision 1).

**Riesgos de UX**

- Abandono del formulario de nombramiento por la cantidad de campos que exigen los Lineamientos DPO (cerca de 30). **Mitigacion:** dividir el alta en pasos (datos basicos, perfil, declaracion jurada, revision final), permitir guardar como BORRADOR en cualquier punto, y exigir los campos mas exhaustivos (checklist completo, documento del acta) solo antes de pasar a NOTIFICADO_INTERNAMENTE o COMUNICADO_A_ACE, no desde el primer paso.
- Confusion entre "Delegado" y "Responsable interno" mientras la reforma este en un estado intermedio (aprobada, no publicada). **Mitigacion:** un nombre de pantalla neutro ("Responsable del programa de datos") con una etiqueta secundaria que muestra el termino legal vigente segun la bandera activa.

**Riesgos operativos**

- Plazos mal calculados si el calendario de dias habiles y asuetos de MOD-023 no esta actualizado para el ano en curso. **Mitigacion:** MOD-002 nunca calcula plazos por su cuenta, siempre consulta el servicio unico de MOD-023 (decision 2.7.15); si el calendario del ano no esta configurado, el sistema bloquea la creacion de nuevas fechas limite y alerta al Administrador en vez de asumir un calendario por defecto.
- Que un cese no dispare a tiempo la designacion de sustituto y la empresa quede sin responsable del tramite mientras hay solicitudes ARCO-POL activas. **Mitigacion:** la automatizacion 7 (seccion G) no es configurable y la alerta correspondiente es CRITICAL (seccion I); MOD-011 muestra una advertencia visible en cualquier caso abierto mientras no exista un registro ACTIVO en MOD-002.

**Riesgos de seguridad y privacidad**

- Exposicion del numero de documento de identidad del Delegado en pantallas de acceso amplio (por ejemplo, si se confunde con el dato publico del aviso de privacidad). **Mitigacion:** el documento de identidad nunca se incluye en documentos publicos; solo nombre, correo y telefono institucional se publican; el campo con el numero de documento tiene acceso restringido y cada lectura queda en el historial (seccion O).
- Que la declaracion jurada de conflicto de intereses, al contener informacion personal sensible sobre la situacion del designado, sea visible para roles que no la necesitan. **Mitigacion:** visible solo para Administrador de organizacion, Aprobador y Responsable Legal; no visible para Auditor externo salvo que el alcance de esa auditoria puntual lo requiera de forma explicita.

---

## Q. MVP

| Funcionalidad del modulo | MUST | SHOULD | COULD | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Alta y edicion del nombramiento (datos basicos, perfil, modalidad) | X | | | | OBL-DPO-01 es obligatoria hoy; sin ella no hay a quien asignar el resto de tareas del modulo, ni MOD-011 ni MOD-007 tienen un "responsable del tramite" identificado |
| Contador y tarea de notificacion interna (3 dias habiles) | X | | | | OBL-DPO-02, plazo legal en curso, bajo costo de implementar |
| Contador, tarea y registro del tramite de comunicacion a la ACE (15 dias habiles) | X | | | | OBL-DPO-03, plazo legal con posible multa asociada por remision del Art. 53 a la Ley de Ciberseguridad |
| Declaracion jurada de conflicto de intereses | X | | | | Art. 9 Lineamientos DPO, condicion previa a aceptar el cargo, bajo costo (formulario booleano mas texto) |
| Checklist de perfil como autoevaluacion (Art. 5) | X | | | | Bajo costo de implementacion, alto valor probatorio de diligencia (Art. 24 inciso ultimo Lineamientos DPO) |
| Contador y tarea de reverificacion cada 3 anos | X | | | | OBL-DPO-04; estructural para el historico y para empresas que migren un Delegado ya nombrado antes de usar el sistema |
| Contador y tarea de capacitacion anual del propio Delegado | X | | | | OBL-DPO-05, plazo legal anual sin condicion adicional |
| Gestion de cese y disparo del plazo de 10 dias para sustituto | X | | | | Vacio critico si falta: deja a la empresa sin responsable del tramite en pleno funcionamiento |
| Clausula y contador de confidencialidad post-cese (5 anos) | X | | | | OBL-DPO-06, bajo costo (un campo de fecha mas alerta), alto valor probatorio |
| Interruptor de doble estado (lectura de la bandera de MOD-024) | X | | | | Pieza central del diseno de doble estado (decision 2.7.16); sin ella el modulo no sobrevive a la reforma 659 sin rediseno |
| Registro de informes periodicos semestrales con estadisticas ARCO-POL | | X | | | OBL-DPO-07 es obligatoria pero condicional a que ya exista al menos un semestre de operacion; el MVP puede lanzar con formulario manual y anadir la precarga automatica cuando MOD-011 acumule historico suficiente |
| Bitacora de peticiones internas atendidas por otras areas | | X | | | OBL-DPO-08 es obligatoria, pero es de las mas faciles de diferir sin vacio legal inmediato: la asistencia ocurre igual entre areas mientras se habilita el registro formal en el sistema |
| Precarga automatica de estadisticas ARCO-POL en el informe periodico | | | X | | Mejora de UX que depende de que MOD-011 tenga datos suficientes; sin ella el informe se sigue pudiendo generar manualmente |
| Paquete de evidencia exportable con hash de integridad | | X | | | Depende de que MOD-019 este disponible; mientras tanto el modulo exporta documentos individuales sin el paquete unificado |
| Delegado comun para grupos de sociedades (Art. 16 Lineamientos DPO) | | | | X | La gestion de grupos empresariales con delegado comun queda fuera del MVP (decision 2.7.31); el MVP soporta una organizacion con varias sucursales de la misma razon social, no varias sociedades distintas |
| Multiples delegados propietarios simultaneos por especializacion (Art. 17) | | | X | | La ley lo permite pero no lo exige; el MVP soporta un responsable activo mas un historico de sustituciones secuenciales, no varios simultaneos por area |

**Conclusion MVP:** la version minima vendible de MOD-002 cubre el alta y el ciclo de vida basico del responsable (alta y edicion del nombramiento, los tres contadores legales de nombramiento -3, 15 y 10 dias habiles-, la declaracion jurada, el checklist de perfil, la reverificacion trienal, la capacitacion anual, el cese con designacion de sustituto, la confidencialidad post-cese, y el interruptor de doble estado), porque estas son las unicas piezas que la ley exige hoy sin condicion adicional distinta de operar como empresa privada salvadorena sujeta a la LPDP, y porque MOD-011 y MOD-007 (ambos MUST HAVE) dependen de que exista, desde el primer dia de uso del sistema, alguien identificado como responsable del tramite.

---

## R. Ayuda contextual (complemento obligatorio)

**1. Delegado de Proteccion de Datos / Responsable interno**
- Que es: la persona (empleada de su empresa o contratada externamente) encargada de gestionar las solicitudes de los titulares y de velar por el cumplimiento de la proteccion de datos dentro de su organizacion.
- Por que tengo que hacer esto: hoy la ley exige que toda empresa privada nombre a esta persona; sin ella, su empresa no tiene un punto de contacto formal ante la Agencia de Ciberseguridad del Estado ni ante las personas cuyos datos trata.
- Fundamento: OBL-DPO-01, Arts. 15 y 17 de la Ley para la Proteccion de Datos Personales (Decreto Legislativo 144).
- Cuando necesito ayuda juridica: si duda sobre si la persona que quiere nombrar cumple los requisitos del perfil, o si podria existir un conflicto de intereses (por ejemplo, si tambien decide sobre el uso de los datos), consulte a su area legal o a un asesor externo antes de formalizar el nombramiento.

**2. Comunicacion del nombramiento a la ACE**
- Que es: el tramite mediante el cual su empresa informa oficialmente a la Agencia de Ciberseguridad del Estado quien es su Delegado, dentro de los 15 dias habiles siguientes al nombramiento.
- Por que tengo que hacer esto: es un plazo legal con fecha ya corriendo desde el dia del nombramiento; si no se cumple, su empresa queda expuesta a que la ACE considere que no tiene Delegado formalmente registrado.
- Fundamento: OBL-DPO-03, Art. 10 de los Lineamientos para el Delegado de Proteccion de Datos Personales (ACE).
- Cuando necesito ayuda juridica: si la plataforma de la ACE no esta disponible o rechaza el tramite por una razon que no entiende, consulte a su area legal para documentar el intento y decidir los siguientes pasos.

**3. Reverificacion del perfil**
- Que es: la confirmacion, cada tres anos, de que la persona que ejerce como Delegado sigue cumpliendo los requisitos con los que fue nombrada, con constancias de capacitacion o certificacion actualizadas.
- Por que tengo que hacer esto: el perfil de un Delegado puede quedar desactualizado con el tiempo; la ley exige revisarlo periodicamente, no solo una vez al inicio.
- Fundamento: OBL-DPO-04, Art. 18 de los Lineamientos DPO.
- Cuando necesito ayuda juridica: si la persona ya no cumple algun requisito (por ejemplo, cambio de cargo que genera un conflicto de intereses), consulte a su area legal antes de decidir si continua o se nombra a otra persona.

**4. Confidencialidad despues del cese**
- Que es: la obligacion de la persona que fue Delegado de mantener en reserva la informacion que conocio en ejercicio del cargo, incluso despues de dejar de serlo, durante cinco anos.
- Por que tengo que hacer esto: la ley protege la informacion que el Delegado manejo, no solo mientras esta en funciones; el sistema le ayuda a no perder de vista este compromiso una vez que la persona ya no trabaja para usted.
- Fundamento: OBL-DPO-06, Art. 36 de los Lineamientos DPO.
- Cuando necesito ayuda juridica: si sospecha un incumplimiento de esta confidencialidad por parte de un exDelegado, consulte a su area legal de inmediato.

**5. Doble estado (reforma 659)**
- Que es: la Asamblea Legislativa aprobo una reforma que eliminaria la obligatoriedad del Delegado en el sector privado, pero esa reforma aun no esta confirmada como publicada en el Diario Oficial. Mientras eso no ocurra, la ley actual sigue exigiendo el Delegado.
- Por que tengo que hacer esto: mientras el sistema muestre el estado ACTUAL, usted debe seguir cumpliendo las obligaciones del Delegado tal como estan hoy; el sistema le avisara claramente si esto cambia.
- Fundamento: OBL-PLAZO-05; Decreto Legislativo 659, segun fuentes secundarias, pendiente de confirmar contra el texto oficial publicado.
- Cuando necesito ayuda juridica: si necesita decidir si mantiene o no a su Delegado una vez que el sistema confirme el estado FUTURO, consulte a su asesoria legal para evaluar el impacto en su empresa especifica.

**6. Declaracion jurada de conflicto de intereses**
- Que es: una declaracion que la persona designada como Delegado debe firmar antes de aceptar el cargo, indicando si tiene alguna situacion personal que pudiera afectar su independencia para ejercer la funcion.
- Por que tengo que hacer esto: el Delegado debe actuar con autonomia; si la misma persona decide sobre los fines del tratamiento de datos o tiene otro interes en juego, su criterio tecnico podria verse comprometido.
- Fundamento: Art. 9 de los Lineamientos DPO.
- Cuando necesito ayuda juridica: si la persona declara una situacion que podria ser un conflicto de intereses, consulte a su area legal antes de continuar con el nombramiento.

---

## Notas finales (desacuerdos y observaciones sobre las fuentes de diseno)

1. **Asimetria de dependencias entre MOD-002 y MOD-023** (detallada en la seccion L): `06_mapa_definitivo_de_modulos.md` y `mapa_modulos.json` documentan que MOD-023 "sale hacia" MOD-002, pero no documentan la relacion inversa ("entra desde MOD-023") en la propia ficha de MOD-002, pese a que la decision 2.7.15 nombra explicitamente al Delegado como uno de los cuatro consumidores del motor de plazos unico. Se recomienda agregar MOD-023 a `depende_de` de MOD-002 en `mapa_modulos.json` para cerrar esa asimetria. No se corrigio el archivo fuente; esta ficha se disenio asumiendo la dependencia real (MOD-002 consulta a MOD-023).
2. **Numeracion de OBL-DPO entre fuentes:** `01_legal/03_hallazgos_regulatorios.md` (seccion 4.4) usa una numeracion OBL-DPO-01 a 09 distinta de la numeracion canonica de `01_legal/matriz_obligaciones.json` (OBL-DPO-01 a 08), reconciliada en la tabla de equivalencia de esa misma fuente (seccion 11.4). Esta ficha cita exclusivamente los IDs canonicos de la matriz, tal como exige el contexto compartido para agentes; se deja esta nota solo para quien compare ambas fuentes y note la diferencia de numeracion.
3. **Ninguna otra inconsistencia material fue detectada** entre el proposito, las obligaciones propietarias/colaboradoras y las dependencias de MOD-002 tal como estan documentadas en `mapa_modulos.json` y `06_mapa_definitivo_de_modulos.md`, y el contenido articulado de los Lineamientos para el Delegado de Proteccion de Datos Personales (OCR local) y de la matriz de obligaciones. Los 8 articulos citados por la matriz para OBL-DPO-01 a 08 (Arts. 15, 17 LPDP; Arts. 8, 9, 10, 18, 22, 36 Lineamientos DPO) coinciden con el texto de las fuentes primarias locales revisadas para esta ficha.
