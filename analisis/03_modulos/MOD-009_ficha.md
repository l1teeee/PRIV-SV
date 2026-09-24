# MODULO: Proveedores y Encargados

Codigo corto del modulo: MOD-009
Clasificacion global del modulo: MUST HAVE (para el MVP)
Obligaciones que cubre:
- Propias: OBL-PROV-01, OBL-PROV-02, OBL-PROV-03, OBL-PROV-04, OBL-PROV-05, OBL-PROV-06, OBL-PROV-07
- Colaboradoras (obligacion propia de otro modulo, en las que este modulo participa como ejecutor o receptor de la tarea): OBL-ARCO-05, OBL-ARCO-11, OBL-AVISO-02, OBL-AVISO-04, OBL-CONS-03, OBL-TRANSF-02

Fuente de esta clasificacion: `02_validacion/mapa_modulos.json` (entrada MOD-009) y `02_validacion/06_mapa_definitivo_de_modulos.md`, seccion "MOD-009 Proveedores y Encargados". Esta ficha no contradice esas decisiones; cualquier precision adicional queda anotada en la seccion final de notas.

---

## A. Proposito

**Por que existe.** Casi ninguna empresa salvadorena trata todos sus datos personales por si misma: usa un proveedor de nomina, un servicio de correo o CRM en la nube, una agencia de mercadeo, un servicio de mensajeria, un despacho de cobranza, etc. La Ley para la Proteccion de Datos Personales (LPDP, Decreto Legislativo 144) no deja esta relacion sin regular: exige que esos proveedores se sometan a la ley (Art. 33 inc. 2), que limiten el tratamiento a lo instruido y guarden confidencialidad (Art. 34), y que cumplan las mismas medidas de seguridad que la empresa (Art. 36). MOD-009 es el lugar unico donde la empresa registra, evalua y da seguimiento a cada proveedor, encargado, tercero receptor y subencargado que participa en sus tratamientos de datos personales.

**Que problema resuelve para la empresa.** Sin este modulo, la relacion con los proveedores vive dispersa entre correos, carpetas de contratos y memoria de quien los contrato. El modulo centraliza: quien es el proveedor, que hace, a que datos accede, que tan riesgoso es, si tiene contrato vigente, cuando vence, y si la relacion terminada devolvio o elimino los datos como se esperaba.

**Que obligacion u obligaciones cubre (IDs y articulos).**

| OBL-ID | Titulo | Articulo | Clasificacion |
|---|---|---|---|
| OBL-PROV-01 | Sometimiento de proveedores subcontratados a la LPDP | Art. 33 inc. 2 | OBLIGATORIO |
| OBL-PROV-02 | Obligaciones directas del encargado del tratamiento | Art. 34 | OBLIGATORIO |
| OBL-PROV-03 | Medidas de seguridad tambien obligatorias para el encargado | Art. 36 | OBLIGATORIO |
| OBL-PROV-04 | No publicar datos de contacto del encargado (infraccion leve) | Art. 56 lit. a num. 2 | OBLIGATORIO |
| OBL-PROV-05 | Subcontratacion en cadena por el encargado (subencargados) | Art. 33 inc. 2 (lectura extensiva, `verificada: false`) | CONDICIONAL |
| OBL-PROV-06 | Instrucciones documentadas del responsable al encargado | Art. 34 lit. a / Art. 5 lit. i (sin articulo expreso, `verificada: false`) | RECOMENDADO |
| OBL-PROV-07 | Devolucion o eliminacion de datos por el encargado al finalizar la relacion | Art. 34 lit. a / Art. 5 lit. h (sin articulo expreso, `verificada: false`) | RECOMENDADO |

Ademas, este modulo ejecuta o recibe tareas derivadas de seis obligaciones que son propiedad de otros modulos (colaboradoras): OBL-AVISO-02 (Art. 24 lit. h, datos de contacto del encargado en el aviso, propiedad de MOD-008), OBL-AVISO-04 (Art. 7, derecho de informacion en la recoleccion, propiedad de MOD-008), OBL-CONS-03 (Art. 30, plazo de 5 dias habiles para notificar al encargado tras una revocacion de consentimiento, propiedad de MOD-007), OBL-ARCO-05 (Art. 12, oposicion al tratamiento incluido marketing directo, propiedad de MOD-011), OBL-ARCO-11 (Art. 21 inc. 3, notificacion a receptores tras rectificacion/eliminacion en 5 dias habiles, propiedad de MOD-011) y OBL-TRANSF-02 (Art. 41, contrato con el responsable receptor, propiedad de MOD-010).

**Que valor aporta.**
- Operativo: da de alta un proveedor en minutos, con un flujo que impide activarlo sin la evidencia minima (documento de sometimiento a la ley), y recuerda automaticamente cuando revisar o renovar.
- Probatorio: es la fuente de evidencia que demuestra, ante una auditoria o ante la ACE, que la empresa conoce a sus encargados, verifico sus medidas de seguridad y documento el cierre de cada relacion.
- De reduccion de riesgo: la infraccion mas visible de este bloque (no publicar los datos de contacto del encargado) es de las mas baratas de evitar y, sin este modulo, de las mas faciles de olvidar; ademas concentra dos obligaciones OBLIGATORIO (Art. 34, Art. 36) cuyo incumplimiento habilita infracciones graves (11 a 25 salarios minimos, US$4,496.80 a US$10,220.00, Art. 56 lit. b num. 5 y 7).

**Que NO hace este modulo (limites explicitos).**
- No sustituye la revision juridica del contrato o DPA: genera un borrador con la plantilla del sistema, pero la validez de las clausulas la revisa la organizacion o su asesoria legal (anti-feature 17).
- No ejecuta controles de seguridad en los sistemas del proveedor (no audita, no escanea, no hace pentesting); solo registra la evidencia de que el proveedor declara tener esos controles (anti-feature 2 y 11).
- No decide si el pais donde el proveedor trata los datos tiene "nivel de proteccion adecuado" bajo el Art. 44; ese juicio no esta atribuido por la ley a ningun organo y el modulo solo activa el registro correspondiente en MOD-010 (anti-feature 18).
- No es un directorio comercial ni un CRM de proveedores para fines de compras o facturacion; solo registra los metadatos relevantes para proteccion de datos.
- No almacena la base de datos completa del proveedor ni copias de los datos personales que ese proveedor trata; solo metadatos y referencias (ver seccion D).

**Doble estado de la reforma 659 en este modulo.** Segun `mapa_modulos.json`, la reforma "no aplica directamente" a MOD-009: ningun campo, estado ni catalogo de este modulo cambia entre el regimen ACTUAL y el regimen FUTURO. La unica interaccion indirecta es a traves de la obligacion colaboradora OBL-CONS-03 (automatizacion 6, seccion G): hoy, la tarea de notificar al encargado tras una revocacion de consentimiento queda pendiente de aprobacion de quien ocupe el rol Delegado de Proteccion de Datos (Art. 30 LPDP vigente, que atribuye el tramite al delegado); si el estado FUTURO se activa en MOD-024, la misma tarea queda pendiente de aprobacion de quien ocupe el rol "Responsable del tramite ARCO-POL / Delegado" configurado como responsable interno (ver `05_tipos_de_usuario.md`, seccion 5.2). El campo o la tarea en si no cambia, solo quien la aprueba, y el sistema registra esa version de la regla en el historial del expediente (ver seccion O). Segun fuentes secundarias, el plazo de 5 dias habiles no cambiaria con la reforma.

---

## B. Usuarios

| Rol estandar | Para que usa este modulo |
|---|---|
| Administrador de la organizacion | Da de alta proveedores cuando no hay un responsable de area designado; configura el catalogo de tipos de riesgo y el umbral de separacion de funciones; tiene visibilidad total y puede archivar registros duplicados o creados por error. |
| Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | Aprueba la evaluacion de riesgo y la activacion de proveedores de riesgo alto; recibe y aprueba las notificaciones a encargados por revocacion de consentimiento (OBL-CONS-03); coordina el informe periodico al responsable citando la evidencia de este modulo. |
| Responsable ARCO-POL / Responsable del tramite | Consulta que receptores tienen los datos de un titular cuando debe ejecutar la rama de notificacion a receptores de una solicitud ARCO-POL (OBL-ARCO-11); deja evidencia del envio dentro de este modulo. |
| Responsable Legal / Compliance | Revisa el documento de sometimiento a la ley y las clausulas del contrato/DPA; decide si una cadena de subcontratacion configura un subencargado sometido a la ley (OBL-PROV-05); aprueba denegatorias o casos ambiguos. |
| Responsable de Seguridad / IT | Evalua las medidas de seguridad declaradas por el proveedor usando el mismo catalogo de controles de MOD-015 (OBL-PROV-03); registra hallazgos tecnicos; vincula incidentes de seguridad asociados a un proveedor. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Da de alta el proveedor que contrata su area (por ejemplo la plataforma de nomina o la agencia de mercadeo), completa los datos operativos iniciales (que hace, con que sistema, que datos) y ejecuta las tareas de revision periodica de sus proveedores. |
| Aprobador | Aprueba el paso de un proveedor a estado ACTIVO cuando el nivel de riesgo es Alto o el pais es distinto de El Salvador (doble control); aprueba el cierre de relaciones de riesgo alto. |
| Auditor (interno) | Consulta de solo lectura todo el modulo; exporta el paquete de evidencia de proveedores para la auditoria anual de cumplimiento (OBL-AUD-01, MOD-018); nunca crea, modifica ni aprueba. |
| Auditor externo (invitado) | Acceso temporal de solo lectura, acotado a los proveedores que la empresa decida incluir en una auditoria puntual; exporta el paquete de evidencia correspondiente. |
| Usuario de consulta / Colaborador | Completa unicamente la tarea puntual que se le asigna, por ejemplo subir el contrato firmado o confirmar la fecha de vencimiento de una certificacion de seguridad. |
| Titular (formulario externo) | No aplica: el titular no interactua directamente con este modulo. Se beneficia de forma indirecta porque los datos de contacto del encargado que aqui se registran aparecen en el aviso de privacidad (OBL-AVISO-02) y porque este modulo ejecuta las notificaciones a receptores y encargados derivadas de sus solicitudes. |
| Asesor externo invitado | Acceso puntual y acotado a un caso especifico, por ejemplo dictaminar si una cadena de subcontratacion concreta debe tratarse como subencargado sometido a la ley (OBL-PROV-05) o si un contrato cumple el Art. 34 y el Art. 36. |

---

## C. Permisos

| Accion | Administrador | Delegado / Resp. interno | Resp. ARCO-POL | Legal / Compliance | Seguridad / IT | Resp. de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver | Si | Si | Solo lectura, filtrado a datos de receptores/encargados de un caso ARCO-POL | Si | Si | Solo sus proveedores | Si (de los pendientes de aprobar) | Si (solo lectura) | Si (acotado, temporal) | Solo lo asignado | Solo el caso invitado |
| Crear (alta) | Si | Si | No | Si | No | Si | No | No | No | No | No |
| Modificar | Si | Si | No | Si (clausulas, sometimiento) | Si (campos de evaluacion) | Si (datos operativos) | No | No | No | No | No |
| Aprobar (activacion, evaluacion) | No (salvo pyme, ver nota) | Si | No | Si (documento de sometimiento) | No (evalua, no aprueba) | No | Si | No | No | No | No |
| Cerrar (relacion finalizada / cerrado) | Si | Si | No | No | No | Si (propone) | No | No | No | No | No |
| Eliminar / archivar | No (solo archivar con justificacion) | No (solo archivar con justificacion) | No | No | No | No | No | No | No | No | No |
| Exportar | Si | Si | No | Si | Si (evidencia tecnica) | No | No | Si | Si (acotado) | No | No |
| Asignar | Si | Si | No | No | No | No | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si |
| Adjuntar evidencia | Si | Si | Si (evidencia de notificacion) | Si | Si | Si | No | No | No | Si (lo asignado) | No |

**Separacion de funciones.** El sistema nunca deja que la misma persona registre y evalue un proveedor de riesgo Alto y ademas apruebe su activacion: quien ejecuta la evaluacion tecnica (Responsable de Seguridad/IT) no puede ser quien aprueba (Aprobador o Delegado), salvo en empresas por debajo del umbral configurable de tamano (propuesta inicial: 50 empleados, `05_tipos_de_usuario.md`, seccion 5.4), donde el sistema lo permite con una advertencia visible de "autorrevision". Ningun rol distinto de Administrador y Delegado puede eliminar un registro; solo pueden archivarlo con una justificacion obligatoria que queda en el historial (bitacora append-only, anti-feature 19). El rol Auditor (interno o externo) nunca puede crear, modificar, aprobar ni adjuntar evidencia, para que su verificacion sea independiente (regla general de `05_tipos_de_usuario.md`, seccion 5.4).

---

## D. Informacion de entrada

**Minimizacion de datos personales.** Este modulo registra datos del proveedor como entidad (razon social, contacto, pais), no datos personales de los titulares del cliente: las "categorias de datos a las que accede" se heredan por referencia del RAT (MOD-006) y nunca se capturan de nuevo como texto libre ni se copian registros individuales de personas. El unico dato de contacto que se almacena es el de una persona de enlace del proveedor (no de un titular), necesario para publicarlo en el aviso de privacidad (OBL-AVISO-02).

### D.1 Identificacion general (Encargado, Tercero/Receptor y Subencargado)

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Nombre comercial | Texto | Obligatorio | - | 2 a 120 caracteres | "Como conoce su empresa a este proveedor. Ejemplo: Amazon Web Services." | Buena practica |
| Razon social / nombre legal | Texto | Obligatorio | - | 2 a 200 caracteres | "Nombre legal completo, tal como aparece en el contrato." | OBL-PROV-01, Art. 33 inc. 2 |
| Tipo de entidad | Seleccion unica | Obligatorio | Encargado del tratamiento / Tercero-Receptor / Subencargado | Determina que reglas del modulo se activan | "Elija Encargado si el proveedor trata datos siguiendo sus instrucciones (por ejemplo su proveedor de nomina). Elija Tercero/Receptor si usted le entrega datos para que los use con su propia finalidad (por ejemplo otra empresa a la que transfiere una base). Elija Subencargado si fue contratado por uno de sus Encargados, no directamente por usted." | Decision 2.7.8 y inconsistencia 9 de `02_validacion_de_la_idea.md` |
| Encargado del que depende | Referencia a otro registro de este modulo (tipo = Encargado) | Obligatorio si Tipo de entidad = Subencargado | Lista de Encargados activos de la organizacion | Debe existir y estar en estado ACTIVO o EN_EVALUACION | "A cual de sus proveedores subcontrata este subencargado." | OBL-PROV-05, Art. 33 inc. 2 (lectura extensiva) |
| Servicio que presta | Texto largo | Obligatorio | - | 10 a 500 caracteres | "Describa en una frase que hace este proveedor por su empresa. Ejemplo: almacena el expediente digital de recursos humanos." | Buena practica |
| Area o responsable interno que lo contrata | Referencia a Departamento (MOD-001) | Obligatorio | Catalogo de areas de la organizacion | Debe existir en MOD-001 | "Quien en su empresa es el punto de contacto con este proveedor." | Buena practica |
| Sistemas relacionados | Referencia multiple al Catalogo de sistemas (MOD-006) | Opcional, recomendado | Catalogo de sistemas | - | "Que sistema o sistemas usa este proveedor para tratar los datos." | Buena practica; evita texto libre duplicado (decision de unificar el catalogo de sistemas) |
| Tratamientos del RAT vinculados | Referencia multiple a Treatment (MOD-006) | Obligatorio antes de pasar a EN_EVALUACION | Lista de tratamientos del RAT de la organizacion | Al menos uno | "Con que actividad de tratamiento de su Registro (RAT) esta relacionado este proveedor." | Trazabilidad, apoya OBL-TRAT-01 (propiedad de MOD-006) |
| Categorias de datos a las que accede | Seleccion multiple, precargada y de solo lectura | Se calcula automaticamente al vincular tratamientos | Catalogo de categorias del RAT | No editable directamente | "Que tipos de datos puede ver o tratar este proveedor (se completa solo, segun los tratamientos que usted vinculo)." | Minimizacion, Art. 5 lit. d |
| Pais o paises donde trata los datos | Seleccion multiple de paises | Obligatorio | Catalogo ISO de paises | Al menos uno | "En que pais o paises estaran los datos cuando este proveedor los trate, incluidos los paises donde ese proveedor aloja sus servidores en la nube." | Dispara la automatizacion hacia MOD-010, ver seccion G |

### D.2 Evaluacion y seguridad

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Nivel de riesgo asignado | Seleccion unica | Obligatorio antes de ACTIVO | Bajo / Medio / Alto | Se sugiere con un cuestionario de apoyo, editable por Responsable de Seguridad | "Que tan critico es este proveedor si algo sale mal. Ejemplo: un proveedor de nomina con datos de salarios es mas riesgoso que uno de mensajeria de paquetes." | Buena practica, apoya OBL-PROV-03 |
| Medidas de seguridad declaradas | Referencia multiple al Catalogo de controles (MOD-015) | Obligatorio antes de ACTIVO si el riesgo es Medio o Alto | Catalogo de controles de MOD-015 | Al menos una si riesgo Medio/Alto | "Que controles de seguridad tiene este proveedor (cifrado, control de acceso, respaldos, etc.), tomados del mismo catalogo que usa su empresa." | OBL-PROV-03, Art. 36 |
| Evidencia de seguridad del proveedor | Archivo(s) adjuntos | Opcional, recomendado si riesgo Alto | - | Formato y tamano segun politica de archivos del sistema | "Certificaciones, autoevaluaciones o reportes de seguridad que el proveedor le compartio." | OBL-PROV-03 |
| Instrucciones documentadas de tratamiento | Texto largo o archivo | Opcional | - | - | "Que le indico por escrito a este proveedor sobre como debe tratar los datos: alcance, finalidad autorizada, tipos de datos permitidos." | OBL-PROV-06, RECOMENDADO, sin articulo expreso |
| Fecha de ultima revision | Fecha | Se autocompleta al cerrar cada ciclo de revision | - | No puede ser futura | "Cuando fue la ultima vez que su empresa reviso a este proveedor." | Buena practica |
| Periodicidad de revision | Seleccion unica | Obligatorio antes de ACTIVO | Anual / Semestral / Configurable (numero de meses) | - | "Cada cuanto quiere que el sistema le recuerde revisar a este proveedor." | Buena practica; alimenta MOD-023 |

### D.3 Contrato o DPA

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Contrato o DPA vinculado | Referencia a Documento (MOD-008, tipo "Contrato/DPA") | Obligatorio antes de ACTIVO, para Encargado y Tercero/Receptor | Documentos tipo Contrato/DPA de la organizacion | Debe existir y estar en estado vigente | "El documento firmado que respalda esta relacion. Si aun no lo tiene, puede generar un borrador con la plantilla del sistema." | OBL-PROV-01, Art. 33 inc. 2 |
| Fecha de vigencia del contrato (inicio) | Fecha | Obligatorio si hay contrato vinculado | - | Anterior o igual a la fecha de vencimiento | "Desde cuando aplica el contrato." | Buena practica |
| Fecha de vencimiento del contrato | Fecha | Obligatorio si hay contrato vinculado | - | Posterior a la fecha de inicio | "Hasta cuando aplica el contrato. El sistema le avisara antes de que venza." | Buena practica, dispara alertas |
| Clausula de devolucion/eliminacion pactada | Booleano | Opcional | Si / No / No aplica | - | "Indica si el contrato dice que pasa con los datos cuando termine la relacion." | OBL-PROV-07, RECOMENDADO, sin articulo expreso |

### D.4 Estado y cierre

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Estado de la relacion | Seleccion unica, controlada por el flujo (seccion F) | El sistema lo asigna | Ver diagrama de estados | No editable manualmente | "En que etapa esta este proveedor dentro de su ciclo de vida." | Buena practica |
| Motivo de cierre o finalizacion | Texto largo | Obligatorio al pasar a Relacion finalizada | Contrato vencido / Terminacion anticipada / Cambio de proveedor / Otro | - | "Por que termino la relacion con este proveedor." | Trazabilidad, OBL-PRIN-03 (propiedad transversal) |
| Constancia de devolucion o eliminacion de datos | Archivo adjunto | Obligatorio para pasar a Cerrado si se marco "Si" en la clausula de devolucion/eliminacion (D.3) | - | - | "El documento o correo donde el proveedor confirma que devolvio o elimino los datos." | OBL-PROV-07 |

### D.5 Datos de contacto para el aviso de privacidad (solo Encargado)

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Nombre de contacto del encargado | Texto | Obligatorio si Tipo = Encargado y Estado = Activo | - | - | "Persona o area de contacto del proveedor que aparecera en su aviso de privacidad." | OBL-AVISO-02, Art. 24 lit. h (colaboradora) |
| Correo o telefono de contacto | Texto | Obligatorio si Tipo = Encargado y Estado = Activo | - | Formato de correo o telefono valido | "Como puede el titular o su empresa contactar a este encargado." | OBL-AVISO-02, Art. 24 lit. h (colaboradora) |

**Que campos se precargan.** Las categorias de datos (D.1) se precargan desde los tratamientos del RAT vinculados. El catalogo de controles de seguridad (D.2) y el catalogo de sistemas (D.1) se consultan por referencia desde MOD-015 y MOD-006, nunca se digitan de nuevo. El contrato/DPA (D.3) se genera, si no existe, a partir de la plantilla de MOD-008 con las variables descritas en la seccion K.

---

## E. Informacion generada

| Que genera | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Registro de Proveedor/Encargado con historial de estados | Ficha completa mas bitacora de cambios | Registro interno | Al dar de alta y en cada cambio | Roles con acceso al modulo (seccion B) |
| Tarea en el Centro de Tareas (MOD-021) | "Revisar el proveedor X", "renovar el contrato con Y", "verificar devolucion o eliminacion de datos de Z" | Tarea con responsable y fecha | Segun las automatizaciones de la seccion G | Responsable de area, Delegado |
| Alerta en Notificaciones (MOD-022) | Ver tabla de la seccion I | Notificacion en plataforma y correo | Segun disparador | Segun tabla de alertas |
| Registro "pendiente de confirmar" en Transferencias Internacionales (MOD-010) | Referencia al proveedor, pais, tratamiento y nota de la ambiguedad legal (Art. 44/45 vs Art. 4 lit. u) | Registro interno | Cuando el pais del proveedor es distinto de El Salvador (automatizacion 1) | Legal/Compliance, Delegado |
| Evento de auditoria (AuditLog, embebido, con salida a MOD-019) | Quien hizo que, cuando, sobre que campo | Evento inmutable | En cada creacion, cambio, aprobacion, adjunto o exportacion | Auditor, Centro de Evidencias |
| Calculo de plazo (5 dias habiles) | Fecha limite para notificar a un Encargado o Receptor | Contador visible en la tarea | Cuando MOD-007 o MOD-011 disparan una notificacion (automatizaciones 6 y 7) | Delegado, Responsable ARCO-POL |
| Borrador de documento (Contrato/DPA, instrucciones, notificacion) | Texto con variables completadas, marcado "borrador pendiente de revision" | Documento en MOD-008 | Cuando el usuario lo solicita o cuando falta el documento antes de activar | Responsable Legal, Delegado |
| Indicador para el Dashboard (MOD-020) | Proveedores activos, sin contrato vigente, con revision vencida, suspendidos | Cifra y semaforo | Calculo continuo | Gerencia, Responsable, Legal, Auditor (ver seccion M) |
| Reporte exportable | Ver seccion N | PDF, XLSX, CSV o ZIP firmado | Bajo demanda o programado | Auditor, Delegado, Gerencia |

---

## F. Workflow

```
                (alta de un nuevo proveedor)
                          |
                          v
                    [BORRADOR]
                          |
        completar datos minimos (D.1) y
        vincular al menos un tratamiento del RAT
                          |
                          v
                 [EN_EVALUACION] -------------------+
                          |                          |
        evaluacion de riesgo y seguridad             | observaciones graves
        aprobada (D.2 completo)                      | (rechazo motivado)
                          |                          |
                          v                          v
             [PENDIENTE_DE_CONTRATO]            [BORRADOR]
                          |
       contrato/DPA vinculado y vigente (D.3)
       + aprobacion del Aprobador o Delegado
       (doble control si riesgo Alto o pais != SV)
                          |
                          v
     +------------->  [ACTIVO]  <---------------------+
     |                   |   |                         |
     |    llega la fecha |   | se vincula un incidente  |
     |    de revision    |   | de seguridad grave       |
     |    programada      |   | (desde MOD-013)          | incidente resuelto y
     |                   v   v                         | medidas verificadas
     |            [EN_REVISION]  [SUSPENDIDO] ----------+
     |                   |             |
     |  revision OK,     |             | empresa decide terminar
     |  sin cambios      |             | la relacion tras el incidente
     |  materiales       |             |
     +-------------------+             |
                          |            |
     cambios materiales   |            |
     (nuevo pais, nuevo   |            |
     tipo de dato, riesgo)|            |
                          v            |
                 [EN_EVALUACION]       |
                 (reinicia sub-flujo,  |
                 conserva historial)   |
                                       |
     fin natural del contrato o        |
     decision de no renovar            |
                          |            |
                          v            v
                   [RELACION_FINALIZADA]
                          |
       verificacion de devolucion/eliminacion
       completada (o "no aplica" justificado)
                          |
                          v
                     [CERRADO]  (solo lectura, permanece consultable)


     [BORRADOR] o [EN_EVALUACION] -- alta duplicada, cancelada
                    o creada por error, con justificacion --> [ARCHIVADO]
                    (no cuenta en indicadores activos, visible para Auditor)
```

### Tabla de transiciones

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (nuevo) | Alta de proveedor | Nombre, tipo de entidad y area responsable capturados | BORRADOR | Administrador, Responsable de area, Delegado | Crea el registro; evento de auditoria "alta creada" |
| BORRADOR | Enviar a evaluacion | Campos obligatorios de D.1 completos, incluido al menos un tratamiento del RAT y el pais | EN_EVALUACION | Responsable de area, Delegado | Crea tarea en MOD-021 para Responsable de Seguridad/IT; si el pais es distinto de El Salvador, crea el registro "pendiente de confirmar" en MOD-010 |
| EN_EVALUACION | Rechazar evaluacion | Responsable de Seguridad o Delegado registra el motivo | BORRADOR | Responsable de Seguridad/IT, Delegado | Notifica a quien creo el registro; queda evidencia del motivo de rechazo |
| EN_EVALUACION | Aprobar evaluacion de riesgo y seguridad | Nivel de riesgo asignado; si es Medio o Alto, medidas de seguridad declaradas (D.2) | PENDIENTE_DE_CONTRATO | Responsable de Seguridad/IT evalua; Aprobador o Delegado aprueba (separacion de funciones si supera el umbral) | Evento de auditoria "evaluacion aprobada"; crea tarea "vincular contrato/DPA" |
| PENDIENTE_DE_CONTRATO | Vincular contrato/DPA y aprobar activacion | Documento tipo Contrato/DPA vinculado, vigente, con fechas de vigencia y vencimiento capturadas | ACTIVO | Aprobador o Delegado (doble control si riesgo Alto o pais distinto de El Salvador) | Programa la proxima revision en MOD-023; habilita los campos de contacto para el aviso si Tipo = Encargado; evento de auditoria "proveedor activado" |
| ACTIVO | Llega la fecha de revision periodica | Alerta emitida por MOD-023/MOD-022 | EN_REVISION | Responsable de area, Delegado, Responsable de Seguridad | Crea tarea de revision en MOD-021 |
| EN_REVISION | Revision completada sin hallazgos que cambien el riesgo | Registro de revision (fecha, quien, resultado) | ACTIVO | Quien ejecuto la revision | Actualiza "fecha de ultima revision"; queda evidencia de la revision |
| EN_REVISION | Revision detecta cambios materiales (nuevo pais, nueva categoria de dato, cambio de riesgo) | Cambio material registrado con motivo | EN_EVALUACION | Responsable de Seguridad/IT, Delegado | Reinicia el sub-flujo de evaluacion conservando el historial anterior |
| ACTIVO | Se vincula un incidente de seguridad grave o critico (desde MOD-013) | Vinculo con el expediente de incidente | SUSPENDIDO | Responsable de Seguridad/IT, Delegado (tambien puede activarse automaticamente, ver automatizacion 11) | Notifica a Responsable de area; advertencia operativa de no enviar nuevos datos a ese proveedor hasta resolver (el sistema no ejecuta ningun bloqueo tecnico) |
| SUSPENDIDO | Incidente resuelto y medidas correctivas verificadas | Evidencia de cierre del incidente vinculado | ACTIVO | Delegado, Aprobador | Evento de auditoria "reactivado tras suspension" |
| SUSPENDIDO | Empresa decide terminar la relacion tras el incidente | Motivo de cierre registrado | RELACION_FINALIZADA | Delegado, Administrador | Crea tarea de verificacion de devolucion/eliminacion en MOD-021 |
| ACTIVO | Fin natural del contrato o decision de no renovar | Motivo de cierre registrado | RELACION_FINALIZADA | Responsable de area, Delegado, Administrador | Crea tarea de verificacion de devolucion/eliminacion (si D.3 indico "Si") en MOD-021, con copia informativa a MOD-016 cuando ese modulo exista |
| RELACION_FINALIZADA | Verificacion de devolucion/eliminacion completada, o "no aplica" justificado | Constancia adjunta si la clausula existia (D.4) | CERRADO | Delegado, Administrador | Evento de auditoria final; el registro pasa a solo lectura, sigue consultable para evidencia |
| BORRADOR o EN_EVALUACION | Archivar (alta duplicada, cancelada o creada por error) | Justificacion obligatoria | ARCHIVADO | Administrador | No cuenta en los indicadores de proveedores activos; permanece visible para Auditor |

**Estados terminales.** CERRADO y ARCHIVADO son terminales para ese registro especifico; ninguno de los dos admite edicion de los campos de contenido, solo comentarios y consulta.

**Reapertura.** Un proveedor en CERRADO no se reactiva: si la empresa vuelve a contratarlo, se crea un nuevo registro que referencia al anterior como historico, para no mezclar la evidencia de dos relaciones contractuales distintas (dos contratos, dos periodos de vigencia, dos ciclos de revision). El registro CERRADO permanece intacto como evidencia del ciclo anterior.

**Registros vinculados al cerrar o archivar.** Los tratamientos del RAT que referenciaban a este proveedor no se eliminan ni se modifican (el RAT es su unico propietario, ver seccion L); solo dejan de listar a este proveedor como activo. Las tareas abiertas en MOD-021 que dependian de este proveedor se marcan "proveedor cerrado, verificar si la tarea sigue aplicando" en vez de cerrarse automaticamente, para que una persona confirme si la tarea aun tiene sentido.

---

## G. Automatizaciones

| # | Disparador | Condicion | Accion | Configurable |
|---|---|---|---|---|
| 1 | Pais del proveedor distinto de El Salvador | El proveedor pasa de BORRADOR a EN_EVALUACION o posterior | Crea un registro "pendiente de confirmar" en MOD-010 Transferencias, con nota visible de la ambiguedad entre transferencia (Art. 44/45) y acceso del encargado extranjero (Art. 4 lit. u) | No (regla legal fija); el registro se crea una sola vez por combinacion proveedor-pais |
| 2 | Intento de pasar a ACTIVO | No existe documento de sometimiento (contrato/DPA) vinculado y vigente | Bloquea la transicion y muestra el mensaje citando OBL-PROV-01, Art. 33 inc. 2 | No |
| 3 | Alta con Tipo de entidad = Subencargado | No tiene un Encargado padre activo o en evaluacion vinculado | Bloquea el guardado hasta vincular al Encargado del que depende | No |
| 4 | Fecha de vencimiento del contrato | Faltan 30 dias | Alerta WARNING al Responsable de area y al Delegado, mas tarea en MOD-021 | Si, los dias de anticipacion |
| 4b | Fecha de vencimiento del contrato | Faltan 7 dias | Alerta HIGH, ver seccion I | Si |
| 5 | Fecha de proxima revision periodica (calculada por MOD-023) | Llega la fecha configurada en D.2 | Crea la tarea "revisar proveedor X" y mueve el estado a EN_REVISION | Si, la periodicidad (campo D.2) |
| 6 | MOD-007 marca la revocacion de un consentimiento vinculado a un tratamiento con Encargado asociado | El Encargado esta en estado ACTIVO | Crea la tarea "notificar la revocacion a [Encargado]" con plazo de 5 dias habiles calculado por MOD-023, pendiente de aprobacion del Delegado antes de enviarse (OBL-CONS-03, Art. 30) | No, el plazo es legal; si el texto de la notificacion |
| 7 | MOD-011 cierra un caso de rectificacion, actualizacion o eliminacion con receptores previos registrados | Existe al menos un Tercero/Receptor vinculado al tratamiento afectado | Crea la tarea "notificar a [Receptor]" con plazo de 5 dias habiles (OBL-ARCO-11, Art. 21 inc. 3) | No, el plazo es legal; si el texto |
| 8 | Se registra un Subencargado dentro de una cadena de subcontratacion | El Subencargado no tiene su propio documento de sometimiento vinculado | Alerta CRITICAL con nota de que la exigencia es una lectura extensiva del Art. 33 inc. 2 (OBL-PROV-05, `verificada: false`); no bloquea automaticamente, requiere decision de la organizacion | No |
| 9 | Proveedor pasa a RELACION_FINALIZADA | El campo "clausula de devolucion/eliminacion pactada" (D.3) es "Si" | Crea tarea obligatoria "verificar devolucion o eliminacion de datos" que debe completarse antes de permitir el paso a CERRADO (OBL-PROV-07) | No |
| 10 | Se intenta activar (PENDIENTE_DE_CONTRATO a ACTIVO) | Nivel de riesgo = Alto, o pais distinto de El Salvador | Exige que quien aprueba sea distinto de quien registro o evaluo (doble control) | Si, el umbral de riesgo que dispara el doble control |
| 11 | MOD-013 vincula un incidente de seguridad a este proveedor con severidad Alta o Critica | El proveedor esta en ACTIVO | Mueve automaticamente a SUSPENDIDO y notifica a Responsable de Seguridad, Delegado y Administrador | Si, la severidad minima que dispara la suspension automatica |

---

## H. Decisiones que NO debe automatizar

| Decision | Por que requiere persona responsable, aprobacion interna o abogado |
|---|---|
| Si un subencargado dentro de una cadena de subcontratacion queda efectivamente sometido a la LPDP | OBL-PROV-05 es una lectura extensiva del Art. 33 inc. 2, sin lineamiento especifico de la ACE al 24-sep-2026 (`verificada: false`). El sistema muestra "Requiere validacion de la organizacion o asesoria especializada" y no decide por si solo si la cadena entera cae bajo la ley. |
| Si el nivel de riesgo asignado a un proveedor es el correcto | El cuestionario de apoyo sugiere un nivel, pero la calificacion final y su consecuencia (medidas exigidas, doble control) las fija una persona con el rol Responsable de Seguridad/IT o Delegado. |
| Si las clausulas del contrato o DPA vinculado cumplen realmente el Art. 34 y el Art. 36 | El sistema no interpreta el texto del contrato; solo verifica que existe un documento vinculado, vigente y del tipo correcto. La suficiencia del contenido legal requiere revision de la organizacion o de su asesoria legal (anti-feature 17). |
| Si el pais donde el proveedor trata los datos tiene "nivel de proteccion adecuado" (Art. 44) | La ley no atribuye esa calificacion a ningun organo y la ACE no ha publicado lista ni criterios; el sistema solo marca el registro "pendiente de confirmar" en MOD-010 (anti-feature 18). |
| Si procede reactivar, terminar o mantener suspendido a un proveedor tras un incidente de seguridad grave | El sistema solo sugiere el cambio de estado a partir de la severidad reportada por MOD-013; la decision final la aprueba una persona con el rol Delegado o Aprobador. |
| Si las instrucciones documentadas y la clausula de devolucion/eliminacion son suficientes o exigibles en el caso concreto | OBL-PROV-06 y OBL-PROV-07 son RECOMENDADO, sin articulo expreso que las exija; se presentan siempre como buena practica, nunca como obligacion legal cerrada. |

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Contrato/DPA proximo a vencer (30 dias) | Fecha de vencimiento menos 30 dias | WARNING | Responsable de area, Delegado | Plataforma + correo | Una vez, repite cada semana si no hay accion | Si faltan 7 dias sin gestion, escala a Aprobador | Se vincula un nuevo contrato vigente o se cierra formalmente la relacion |
| Contrato/DPA proximo a vencer (7 dias) | Fecha de vencimiento menos 7 dias | HIGH | Responsable de area, Delegado, Aprobador | Plataforma + correo | Diaria | Si vence sin renovar, escala a Administrador | Idem |
| Contrato/DPA vencido sin renovar | Fecha de vencimiento superada | CRITICAL | Delegado, Administrador | Plataforma + correo | Diaria hasta resolver | Automatico desde el nivel HIGH | Se vincula un nuevo contrato o se cierra formalmente la relacion |
| Revision periodica vencida | Fecha de proxima revision superada sin registro nuevo | WARNING | Responsable de area, Delegado | Plataforma | Semanal | A los 15 dias sin revisar, escala a Aprobador | Se completa la revision |
| Proveedor activo sin evaluacion de riesgo vigente | Periodo maximo configurable superado desde la ultima evaluacion | WARNING | Delegado | Plataforma | Mensual | -- | Se registra una nueva evaluacion |
| Pais fuera de El Salvador sin registro vinculado en Transferencias | La creacion automatica del registro en MOD-010 falla o el vinculo se pierde | HIGH | Delegado, Legal/Compliance | Plataforma + correo | Al detectarse | Escala a Administrador si persiste 5 dias | Se crea o se revincula el registro en MOD-010 |
| Incidente de seguridad grave vinculado | Evento desde MOD-013 con severidad Alta o Critica | CRITICAL | Delegado, Responsable de Seguridad/IT, Administrador | Plataforma + correo (mas SMS si el canal esta configurado) | Inmediata | Notifica de forma automatica tambien al Aprobador | El incidente vinculado se cierra en MOD-013 |
| Relacion finalizada sin verificar devolucion o eliminacion | Mas de 30 dias en RELACION_FINALIZADA sin constancia adjunta | WARNING | Responsable de area, Delegado | Plataforma | Semanal | A los 60 dias, escala a Administrador | Se adjunta la constancia o se marca "no aplica" con justificacion |
| Subencargado sin documento de sometimiento propio | Alta de subencargado sin documento vinculado | HIGH | Delegado, Legal/Compliance | Plataforma | Al detectarse, repite semanal | -- | Se vincula el documento o se archiva el registro con justificacion |

---

## J. Evidencia

| Evidencia que conserva el modulo | Como se registra | OBL-ID que prueba | Tiempo de conservacion |
|---|---|---|---|
| Historial de creacion y cambios de cada proveedor (quien, cuando, campo anterior y nuevo) | Evento de auditoria inmutable (AuditLog, con salida a MOD-019) | OBL-PRIN-03 (responsabilidad demostrada, propiedad transversal) | Mismo periodo que el expediente del proveedor; ver retencion documental de MOD-016 |
| Documento de sometimiento / contrato-DPA vinculado, con version y hash de integridad | Referencia a Documento de MOD-008, con su propio versionado | OBL-PROV-01 (Art. 33 inc. 2), OBL-PROV-02 (Art. 34) | Mientras la relacion este ACTIVA y, tras el cierre, segun la retencion documental de expedientes de proveedores (MOD-016, motor de retencion documental) |
| Evidencia de seguridad adjunta (certificaciones, autoevaluaciones, reportes) | Archivo con fecha, usuario y hash | OBL-PROV-03 (Art. 36) | Igual que el contrato vinculado |
| Aprobacion de la evaluacion de riesgo y de la activacion, con identidad y fecha de quien aprobo | Evento de auditoria de la transicion PENDIENTE_DE_CONTRATO a ACTIVO | OBL-PROV-02, OBL-PROV-03 | Igual que el registro del proveedor |
| Registro y evidencia de la notificacion enviada al Encargado tras una revocacion de consentimiento, con fecha y verificacion del plazo | Tarea completada mas adjunto de la comunicacion enviada | OBL-CONS-03 (Art. 30, colaboradora, propiedad de MOD-007) | Igual que el expediente de consentimiento en MOD-007 |
| Registro y evidencia de la notificacion enviada a un Tercero/Receptor tras una rectificacion, actualizacion o eliminacion | Tarea completada mas adjunto de la comunicacion enviada | OBL-ARCO-11 (Art. 21 inc. 3, colaboradora, propiedad de MOD-011) | Igual que el expediente ARCO-POL en MOD-011 |
| Datos de contacto del encargado, con historial de version, que efectivamente aparecen publicados en el aviso vigente | Referencia de solo lectura al aviso publicado en MOD-008 | OBL-AVISO-02 (Art. 24 lit. h, colaboradora, propiedad de MOD-008); tambien es la evidencia que descarta la infraccion leve de OBL-PROV-04 (Art. 56 lit. a num. 2) | Igual que el aviso de privacidad vigente en MOD-008 |
| Constancia de devolucion o eliminacion de datos al cierre de la relacion | Archivo adjunto en la transicion a CERRADO | OBL-PROV-07 (Art. 34 lit. a / Art. 5 lit. h, RECOMENDADO) | Segun retencion documental de expedientes cerrados (MOD-016) |
| Documento de instrucciones de tratamiento | Archivo o texto versionado | OBL-PROV-06 (Art. 34 lit. a / Art. 5 lit. i, RECOMENDADO) | Igual que el contrato vinculado |
| Historial de evaluaciones de riesgo y revisiones periodicas | Registro con fecha, usuario y resultado por cada ciclo | OBL-PRIN-03 (Art. 5 lit. i) | Igual que el registro del proveedor |
| Exportaciones del paquete de evidencia de un proveedor, con verificacion de integridad | Evento de exportacion mas hash o firma del paquete | OBL-PRIN-03; insumo del paquete de evidencia general de MOD-019 | Se registra el evento de exportacion de forma permanente, aunque el paquete exportado quede fuera del sistema |

**Nota sobre retencion.** Este modulo aun no define su propio motor de retencion: sigue las reglas centrales del motor de retencion documental de cumplimiento de MOD-016 (SHOULD HAVE en el mapa definitivo). Mientras ese motor no exista o no este activo para una organizacion, MOD-009 no elimina evidencia de proveedores de forma automatica; solo el archivado manual con justificacion (seccion F) saca un registro de los indicadores activos, sin borrar su historial.

---

## K. Documentos asociados

**Documentos requeridos como entrada.**
- Contrato o DPA ya firmado, si el proveedor lo tenia antes de darse de alta en el sistema.
- Certificaciones o reportes de seguridad que el proveedor comparta (ISO 27001, SOC 2, autoevaluaciones, etc.).
- Constancia de devolucion o eliminacion de datos al finalizar la relacion.

**Documentos generados por el sistema.**
- Ficha de evaluacion de proveedor (PDF), con el resumen de riesgo, medidas de seguridad y fechas clave.
- Carta o formato de notificacion de revocacion de consentimiento al Encargado (OBL-CONS-03).
- Carta o formato de notificacion a Receptor tras rectificacion, actualizacion o eliminacion (OBL-ARCO-11).
- Paquete de evidencia exportable por proveedor (ver seccion N).

**Plantillas que el sistema provee.**

| Plantilla | Variables principales | Requiere validacion de la organizacion |
|---|---|---|
| Contrato/DPA estandar (Encargado) | nombre del proveedor, razon social, servicio, finalidad autorizada, categorias de datos, medidas de seguridad exigidas, plazo de vigencia, clausula de confidencialidad, clausula de devolucion/eliminacion, pais de tratamiento | Si, siempre; se recomienda ademas revision de asesoria legal antes de firmar |
| Documento de sometimiento a la LPDP (Tercero/Receptor) | nombre del receptor, finalidad de la transferencia, categorias de datos, obligaciones equivalentes (Art. 41) | Si |
| Instrucciones documentadas de tratamiento | alcance, finalidad autorizada, tipos de datos permitidos, medidas de seguridad exigidas | Si (documento de buena practica, no de exigencia legal expresa) |
| Notificacion de revocacion de consentimiento al Encargado | referencia al tratamiento afectado (no el nombre del titular en texto libre, sino una referencia al expediente de MOD-007), fecha de la revocacion, plazo aplicable | Si, antes de enviarse (aprobacion del Delegado, ver automatizacion 6) |
| Notificacion a Receptor tras rectificacion, actualizacion o eliminacion | referencia al tratamiento y al caso ARCO-POL, tipo de cambio, fecha | Si, antes de enviarse |

**Anexos y evidencias documentales.** Evidencia de seguridad del proveedor, constancia de devolucion/eliminacion, y cualquier comunicacion enviada quedan como anexos del registro, vinculados con fecha, usuario y hash de integridad.

---

## L. Dependencias

```
MOD-006 RAT y Mapa de Datos
  (tratamientos, categorias de datos,
   catalogo de sistemas: solo lectura)
          |
          v
MOD-009 Proveedores y Encargados
          |            |            |
          v            v            v
   MOD-008 Docs.  MOD-010 Transf.  MOD-019 Evidencia
   (Contrato/DPA  ("pendiente de   (paquete de
    como tipo de   confirmar" si   evidencia)
    documento)     pais != SV)

Eventos puntuales que MOD-009 recibe (no dependencia estructural, si funcional):
  MOD-007 Consentimiento  --(revocacion)-->  MOD-009 (notificar a Encargado, OBL-CONS-03)
  MOD-011 ARCO-POL        --(rectif./elim.)->  MOD-009 (notificar a Receptor, OBL-ARCO-11)
  MOD-013 Incidentes      --(incidente grave)->  MOD-009 (suspender proveedor)

Capa transversal consultada de forma constante (nunca escribe hacia ella):
  MOD-001 (organizacion, areas) | MOD-021 (tareas) | MOD-022 (notificaciones)
  MOD-023 (calendario / plazos) | MOD-024 (estado regulatorio vigente) | MOD-026 (ayuda)
```

**De que modulos recibe datos.** Dependencia estructural minima (`depende_de` en `mapa_modulos.json`): MOD-006 RAT y Mapa de Datos, del cual lee por referencia los tratamientos, las categorias de datos y el catalogo de sistemas, sin duplicarlos (regla de "direccion unica" entre modulos de proceso, seccion 4 regla 7 de `06_mapa_definitivo_de_modulos.md`). Ademas recibe eventos puntuales de MOD-007, MOD-011 y MOD-013 cuando disparan una tarea especifica dentro de este modulo (ver seccion G), y consulta de forma constante la capa transversal (MOD-001, MOD-021, MOD-022, MOD-023, MOD-024, MOD-026).

**A que modulos envia datos o eventos.** MOD-008 (el Contrato/DPA vive como tipo de documento alli), MOD-010 (registro "pendiente de confirmar" cuando el pais es distinto de El Salvador) y MOD-019 (evidencia continua de todo lo que ocurre en este modulo).

**Que ocurre si el modulo dependiente no existe en el MVP.**
- MOD-010 Transferencias Internacionales es SHOULD HAVE. Si aun no esta disponible, el registro "pendiente de confirmar" se sustituye por una tarea manual en MOD-021 ("documentar la transferencia hacia [pais]") con la evidencia suelta en MOD-019, siguiendo el mismo patron que el propio mapa definitivo describe para la cobertura parcial de MOD-010 en el MVP.
- MOD-016 Retencion y Eliminacion es SHOULD HAVE. Si aun no existe, la tarea de verificar devolucion/eliminacion de datos (seccion F, automatizacion 9) queda registrada solo dentro de MOD-009 y MOD-021, sin el motor de alertas de retencion documental compartido; el campo de evidencia sigue siendo obligatorio de todas formas.
- MOD-015 Controles de Seguridad es MUST HAVE, siempre disponible: el catalogo de medidas de seguridad (D.2) siempre existe como referencia.
- MOD-002 Delegado, MOD-001 Organizacion y MOD-003 Onboarding son MUST HAVE previos en el recorrido; el rol que aprueba las notificaciones a Encargado/Receptor siempre existe porque estos tres modulos se configuran antes que MOD-009.

---

## M. Dashboard

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Proveedores activos (total y por tipo: Encargado / Receptor / Subencargado) | Conteo de registros en estado ACTIVO, agrupado por Tipo de entidad | Informativo (sin semaforo) | Gerencia (cifra resumen), Responsable (detalle por area) |
| Proveedores sin contrato/DPA vigente vinculado | Conteo de registros en PENDIENTE_DE_CONTRATO, o en ACTIVO con contrato vencido | Rojo si mayor a 0 | Responsable, Legal/Compliance |
| Contratos por vencer en 30 dias | Conteo de contratos con fecha de vencimiento en los proximos 30 dias | Amarillo | Responsable, Gerencia |
| Proveedores fuera de El Salvador sin transferencia vinculada | Conteo de proveedores con pais distinto de El Salvador sin registro activo en MOD-010 | Rojo | Legal/Compliance, Auditor |
| Proveedores con revision periodica vencida | Conteo de proveedores en EN_REVISION con la fecha programada superada | Amarillo si menos de 30 dias de atraso, rojo si mas | Responsable, Auditor |
| Proveedores suspendidos por incidente | Conteo de registros en estado SUSPENDIDO | Rojo | Gerencia, Legal/Compliance, Seguridad/IT |
| Evidencia disponible por proveedor activo | Porcentaje de proveedores ACTIVO con contrato vigente, evaluacion de riesgo y ultima revision al dia, los tres a la vez | Verde/amarillo/rojo segun el porcentaje configurado por producto | Auditor |

Todos los indicadores se muestran como estado del programa (proveedores activos, tareas pendientes, evidencia disponible), nunca como un porcentaje de "cumplimiento legal" (regla general del producto, `04_objetivo_exacto_del_producto.md`, seccion 1.2). En la perspectiva Legal/Delegado del Dashboard (MOD-020), estos indicadores tambien pueden filtrarse dentro del cluster legal "Relacion con terceros".

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Listado de proveedores/encargados | Nombre, tipo, pais, estado, nivel de riesgo, contrato vigente hasta | Tipo de entidad, estado, pais, nivel de riesgo | XLSX, CSV, PDF | Delegado, Auditor | Si |
| Reporte de vencimientos | Contratos y revisiones proximas a vencer, ordenados por fecha | Rango de fechas, area | PDF, XLSX | Responsable de area, Gerencia | No (es operativo, de seguimiento interno) |
| Paquete de evidencia de un proveedor especifico | Ficha completa, contrato vinculado, evaluaciones de riesgo, revisiones, notificaciones enviadas, con verificacion de integridad (hash o firma) | Un proveedor a la vez | PDF y ZIP firmado | Auditor interno, Auditor externo, y la empresa si lo requiere para presentarlo a la ACE | Si, es el paquete de evidencia principal de este modulo |
| Reporte de transferencias derivadas | Cruce de proveedores con pais distinto de El Salvador contra los registros de MOD-010 | Pais, estado del registro de transferencia | XLSX | Legal/Compliance, Delegado | Si, alimenta la evidencia de MOD-010 |

---

## O. Historial

Eventos que quedan en el historial de cada registro y en la auditoria transversal (AuditLog):
- Creacion del registro, con usuario y fecha.
- Cambio de cada campo relevante (valor anterior y nuevo), en especial Tipo de entidad, Nivel de riesgo y Estado de la relacion.
- Cada cambio de estado (seccion F), con quien lo ejecuto, cuando y bajo que condicion.
- Asignaciones de responsable de area.
- Aprobaciones: quien aprobo la evaluacion de riesgo, quien aprobo la activacion, quien aprobo el cierre.
- Adjuntos: contrato/DPA, evidencia de seguridad, constancia de devolucion/eliminacion, con hash de cada archivo.
- Exportaciones del paquete de evidencia, con quien exporto, cuando y que version del registro se exporto.
- Accesos de lectura de un Auditor externo invitado (quien vio que expediente y cuando), dado que su acceso es temporal y por invitacion.
- Archivado (nunca hay eliminacion real de un registro con contenido), con el motivo obligatorio.

Estos eventos son la fuente primaria del paquete de evidencia (seccion J) que prueba OBL-PROV-01 a OBL-PROV-07, y de las evidencias colaboradoras de OBL-CONS-03, OBL-ARCO-11 y OBL-AVISO-02. Sin este historial, el modulo podria mostrar el estado actual de un proveedor pero no podria demostrar, ante una auditoria o ante la ACE, cuando y por quien se tomo cada decision (OBL-PRIN-03, Art. 5 lit. i).

---

## P. Riesgos

| Riesgo | Tipo | Mitigacion de diseno |
|---|---|---|
| Que un usuario entienda la evaluacion de riesgo o el contrato vinculado como una validacion juridica del sistema | Legal | Textos de descargo estandar del producto ("documento generado como borrador...", "requiere validacion de asesoria legal especializada"); el sistema nunca certifica el contenido del contrato. |
| Que se trate la interpretacion extensiva de subencargados (OBL-PROV-05) como una obligacion cerrada e indiscutible | Legal | Se marca siempre como CONDICIONAL con nota visible de que es una lectura extensiva del Art. 33 inc. 2, sin lineamiento ACE especifico; nunca bloquea, solo alerta (automatizacion 8). |
| Que el formulario de alta se perciba como largo o tecnico por un usuario no especialista (por ejemplo, un Responsable de area sin conocimiento legal) | UX | Division en pasos (wizard) por bloque de campos (D.1 a D.5); precarga automatica desde el RAT; textos de ayuda con ejemplos concretos en cada campo. |
| Que las alertas de vencimiento se calculen mal si el proveedor tiene mas de un contrato vigente o renovaciones automaticas no registradas | Operativo | Un solo contrato/DPA vigente por proveedor a la vez; las versiones anteriores quedan como historico visible, nunca se sobrescriben. |
| Que se confunda Encargado con Tercero/Receptor y se omita una obligacion (por ejemplo, no notificar a un receptor porque se registro como encargado) | Operativo | Texto de ayuda que diferencia ambos tipos con ejemplos concretos (seccion R); validacion opcional del Delegado o de Legal/Compliance antes de activar un registro con Tipo de entidad ambiguo. |
| Que se adjunten copias de bases de datos completas del proveedor como "evidencia de seguridad" en vez de solo certificaciones o reportes | Seguridad y privacidad | El campo de evidencia (D.2) se limita por diseno a certificaciones, autoevaluaciones y reportes; el texto de ayuda advierte explicitamente no subir bases de datos; el modulo no almacena PII de los titulares del cliente, solo metadatos y referencias (seccion D). |
| Que se exponga el nombre y el contacto de todos los proveedores a cualquier usuario interno sin necesidad de conocerlo | Seguridad y privacidad | Visibilidad por area asignada, salvo para roles con alcance global (Delegado, Administrador, Auditor), segun la tabla de permisos (seccion C). |

---

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Alta y ficha de Encargado / Tercero-Receptor / Subencargado (bloques D.1 y D.2) | X | | | | Nucleo del modulo; sostiene OBL-PROV-01, 02 y 03, todas OBLIGATORIO; identificado como nucleo por `02_validacion_de_la_idea.md`, seccion 2.1. |
| Vinculacion de Contrato/DPA (referencia a MOD-008) | X | | | | OBL-PROV-01, Art. 33 inc. 2; es la condicion bloqueante para activar cualquier proveedor. |
| Flujo de estados con aprobacion de activacion y doble control en riesgo alto | X | | | | Da evidencia de OBL-PRIN-03 (responsabilidad demostrada) y aplica la separacion de funciones exigida por diseno (seccion 5.4 de `05_tipos_de_usuario.md`). |
| Alertas de vencimiento de contrato y de revision periodica | X | | | | Sin esto el modulo pierde su valor operativo principal: recordar antes de que algo venza. |
| Notificacion automatica a Encargado tras revocacion de consentimiento (integracion con MOD-007) | X | | | | OBL-CONS-03 es OBLIGATORIO, con plazo legal de 5 dias habiles y riesgo de infraccion muy grave si se incumple la revocacion. |
| Notificacion automatica a Receptor tras rectificacion/eliminacion (integracion con MOD-011) | X | | | | OBL-ARCO-11, plazo de 5 dias habiles, dentro del bloque de obligaciones con mayor concentracion normativa (MOD-011). |
| Datos de contacto del encargado para el aviso de privacidad (integracion con MOD-008) | X | | | | OBL-AVISO-02, con infraccion leve especifica si se omite (OBL-PROV-04, Art. 56 lit. a num. 2). |
| Paquete de evidencia exportable por proveedor, con verificacion de integridad | X | | | | Decision de producto 2.7.24 (integridad verificable de todo paquete exportado); requerido por el rol Auditor desde el primer dia. |
| Creacion automatica de registro "pendiente de confirmar" en Transferencias cuando el pais es distinto de El Salvador | | X | | | Depende de que exista MOD-010 (SHOULD HAVE); en su ausencia se cubre con la tarea manual descrita en la seccion L. |
| Modelado de cadenas de subcontratacion (Subencargados de segundo nivel o mas) | | X | | | Obligacion CONDICIONAL y no verificada (OBL-PROV-05); util para empresas medianas/corporativas, no bloquea la venta del MVP a una pyme tipica. |
| Tarea de verificacion de devolucion/eliminacion de datos al finalizar la relacion | | X | | | OBL-PROV-07 es RECOMENDADO, pero de alto valor probatorio si el contrato lo pacta; se incluye desde temprano por bajo costo de implementacion. |
| Suspension automatica al vincular un incidente de seguridad grave (integracion con MOD-013) | | | X | | Mejora de control operativo; la suspension manual ya cubre el caso desde el MVP. |
| Reportes exportables adicionales y dashboard de indicadores completo | | X | | | Valor de gestion; el listado y el paquete de evidencia por proveedor (ambos MUST HAVE) ya cubren la necesidad probatoria minima. |
| Campo de instrucciones documentadas de tratamiento con plantilla dedicada | | | X | | OBL-PROV-06 es RECOMENDADO sin articulo expreso; el campo de texto simple ya cubre la necesidad minima desde el MVP dentro de D.2. |
| Motor de scoring automatizado de riesgo de proveedores (mas alla del campo manual con cuestionario de apoyo) | | | | X | Hoy el nivel de riesgo se asigna con apoyo de un cuestionario y criterio humano; un motor de scoring propio, con ponderaciones configurables, es una mejora de V2/Enterprise. |

**Version minima que ya puede venderse.** Alta y ficha de proveedores con los tres tipos de entidad, vinculacion obligatoria de Contrato/DPA, flujo de aprobacion con doble control en riesgo alto, alertas de vencimiento y revision, las dos notificaciones legales de 5 dias (a Encargado por revocacion, a Receptor por rectificacion/eliminacion), los datos de contacto del encargado para el aviso, y el paquete de evidencia exportable por proveedor. Razon: esa combinacion cubre las 7 obligaciones propias del modulo (3 OBLIGATORIO, 1 infraccion evitable, 3 RECOMENDADO) mas las obligaciones colaboradoras de mayor riesgo sancionador (una infraccion muy grave si no se ejecuta la revocacion, otra si no se atiende ARCO-POL a tiempo), sin necesitar todavia el motor de scoring ni la integracion completa con Transferencias Internacionales.

---

## R. Ayuda contextual

**1. Encargado del tratamiento**
- Que es: es el proveedor que trata datos personales de sus clientes o empleados siguiendo las instrucciones de su empresa, no por cuenta propia. Ejemplo: la plataforma que procesa su nomina, el proveedor de correo electronico corporativo.
- Por que tengo que registrarlo: la ley exige que estos proveedores tambien cumplan la ley y sus lineamientos, y que usted verifique sus medidas de seguridad y tenga un contrato con ellos.
- Fundamento: OBL-PROV-01 (Art. 33 inc. 2), OBL-PROV-02 (Art. 34), OBL-PROV-03 (Art. 36).
- Cuando necesito ayuda juridica: cuando no esta seguro si un proveedor concreto trata los datos por sus instrucciones (Encargado) o con su propia finalidad (Tercero/Receptor), o al revisar si las clausulas del contrato cumplen la ley.

**2. Tercero / Receptor**
- Que es: es una empresa u organizacion a la que usted le entrega datos personales para que los use con su propia finalidad, distinta de la suya. Ejemplo: una aseguradora a la que le transfiere datos de sus empleados para gestionar un beneficio, y que luego decide como tratarlos para ese fin.
- Por que tengo que registrarlo: si mas adelante un titular pide corregir o eliminar sus datos, usted debe poder avisarle a este receptor en 5 dias habiles.
- Fundamento: OBL-ARCO-11 (Art. 21 inc. 3), OBL-TRANSF-02 (Art. 41, si aplica transferencia).
- Cuando necesito ayuda juridica: cuando no esta claro si la transferencia a este tercero necesitaba el consentimiento previo del titular o si aplica alguna excepcion del Art. 28.

**3. Subencargado**
- Que es: es un proveedor contratado, no por usted, sino por uno de sus Encargados, para ayudarle a prestar el servicio. Ejemplo: su proveedor de nomina (Encargado) usa a su vez un servicio de nube externo (Subencargado) para almacenar la informacion.
- Por que tengo que registrarlo: si esta cadena de subcontratacion existe, es razonable esperar que ese subencargado tambien deba someterse a la ley, aunque este punto no esta resuelto de forma expresa en el texto legal.
- Fundamento: OBL-PROV-05 (Art. 33 inc. 2, lectura extensiva, no verificada; requiere confirmacion de abogado).
- Cuando necesito ayuda juridica: siempre que identifique una cadena de subcontratacion, antes de asumir que la misma obligacion de sometimiento aplica automaticamente al subencargado.

**4. Contrato o DPA (documento de sometimiento)**
- Que es: el documento que respalda por escrito la relacion con su proveedor y traslada a el las obligaciones de confidencialidad, seguridad, finalidad y, si corresponde, devolucion o eliminacion de datos.
- Por que tengo que registrarlo: sin este documento vinculado, el sistema no le permite activar al proveedor, porque la ley exige que estos proveedores se sometan expresamente a la LPDP.
- Fundamento: OBL-PROV-01 (Art. 33 inc. 2), OBL-PROV-02 (Art. 34).
- Cuando necesito ayuda juridica: antes de firmar cualquier contrato generado por el sistema; el borrador no sustituye la revision de su asesoria legal.

**5. Evaluacion de riesgo del proveedor**
- Que es: la calificacion (Bajo, Medio o Alto) que su empresa le asigna a un proveedor segun que tan grave seria un problema con los datos que maneja.
- Por que tengo que hacerlo: un proveedor de riesgo Alto exige mas controles y una aprobacion separada de quien lo evaluo, para reducir la posibilidad de un incidente grave.
- Fundamento: apoya OBL-PROV-03 (Art. 36); el nivel de riesgo en si es una decision de producto, no una categoria definida por la ley.
- Cuando necesito ayuda juridica: si el proveedor trata datos sensibles (salud, biometria, afiliacion sindical) o datos de menores, consulte tambien la ayuda contextual de MOD-006 y MOD-007 antes de decidir el nivel de riesgo.

**6. Pais fuera de El Salvador y transferencia**
- Que es: cuando el proveedor trata los datos en otro pais (por ejemplo, un servidor en la nube fuera de El Salvador), esa situacion puede activar las reglas de transferencias internacionales.
- Por que tengo que registrarlo: la ley exige informar al titular y, en algunos casos, poner la transferencia en conocimiento de la ACE.
- Fundamento: OBL-TRANSF-01 a OBL-TRANSF-06 (Arts. 40, 41, 44 y 45, propiedad de MOD-010); este modulo solo detecta el caso y crea el registro correspondiente.
- Cuando necesito ayuda juridica: siempre que un proveedor trate datos fuera de El Salvador, porque no esta resuelto en la ley si un encargado extranjero debe tratarse como "transferencia" o como "flujo transfronterizo", y esa distincion cambia que articulo aplica.

---

## Notas finales (precisiones y posibles observaciones al mapa)

- No se identifico ninguna contradiccion con `06_mapa_definitivo_de_modulos.md` ni con `mapa_modulos.json` para MOD-009. Las siete obligaciones propias (OBL-PROV-01 a 07) y las seis colaboradoras (OBL-ARCO-05, OBL-ARCO-11, OBL-AVISO-02, OBL-AVISO-04, OBL-CONS-03, OBL-TRANSF-02) declaradas en el mapa se verificaron contra `01_legal/matriz_obligaciones.json` y coinciden.
- Precision sobre la nota "No aplica directamente" de la reforma 659 para este modulo: es correcta en cuanto a que ningun campo, catalogo o estado de MOD-009 cambia entre el regimen ACTUAL y el FUTURO. Esta ficha aclara, sin contradecir esa nota, que existe un efecto indirecto sobre quien aprueba la tarea derivada de OBL-CONS-03 (ver seccion A y automatizacion 6 de la seccion G), porque esa obligacion si esta marcada como afectada por la reforma en `matriz_obligaciones.json` y en `03_hallazgos_regulatorios.md`.
- Se detecto que OBL-PROV-04 (infraccion leve por no publicar los datos de contacto del encargado, Art. 56 lit. a num. 2, propiedad de MOD-009) y OBL-AVISO-02 (el deber positivo de publicar esos mismos datos, Art. 24 lit. h, propiedad de MOD-008) describen, desde dos angulos distintos, la misma conducta esperada. Esto no es un error: asi esta modelado de forma consistente en `matriz_obligaciones.json` y en la tabla de equivalencia de `03_hallazgos_regulatorios.md` (seccion 11.8), que documenta explicitamente por que la matriz cataloga la infraccion como obligacion propia ademas del deber positivo. Esta ficha simplemente hace explicita la relacion en la seccion J (evidencia) para que ambas obligaciones queden cubiertas por la misma evidencia (los datos de contacto efectivamente publicados en el aviso vigente).
- Los campos de "instrucciones documentadas" (OBL-PROV-06) y "clausula de devolucion/eliminacion" (OBL-PROV-07) se disenaron como opcionales y no bloqueantes, consistente con su clasificacion RECOMENDADO y con la advertencia de `01_legal/matriz_obligaciones.md` de que ambas obligaciones carecen de articulo expreso (`verificada: false`); si una futura confirmacion de abogado encuentra base legal expresa, estos dos campos deberian reclasificarse a obligatorios antes de activar el proveedor.
