# MODULO: Retencion y Eliminacion

Codigo corto del modulo: MOD-016
Clasificacion global del modulo: SHOULD HAVE (para el MVP)
Obligaciones que cubre (propietario): OBL-RET-01, OBL-RET-02, OBL-RET-03, OBL-RET-04, OBL-RET-05, OBL-RET-06
Obligaciones colaboradoras (propietarias de otro modulo, MOD-016 aporta el patron de evidencia de eliminacion): OBL-PROV-07 (propietario MOD-009), OBL-SEG-05 (propietario MOD-015), OBL-SANC-07 (propietario MOD-024)

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (prohibido codigo, SQL, APIs, stack o infraestructura).

---

## A. Proposito

- **Por que existe.** El Art. 5 lit. h) LPDP (principio de temporalidad) exige que los datos personales se conserven solo el tiempo necesario para cumplir la finalidad para la que fueron recolectados, y que despues se eliminen o anonimicen, salvo que otra norma obligue a conservarlos por mas tiempo. En la practica esa segunda parte ("salvo que otra norma obligue") choca todos los dias contra la primera: el Codigo de Comercio, el Codigo Tributario y la Ley Contra el Lavado de Dinero y de Activos (LCLDA) exigen conservar comprobantes, planillas y registros de operaciones durante 10, 10 y hasta 15 anos respectivamente, plazos muy superiores al tiempo que la LPDP permitiria si solo se mirara la finalidad original del dato. MOD-016 existe para que esa tension no la resuelva cada area por su cuenta, sino un mismo criterio documentado y consultable.
- **Que problema resuelve para la empresa.** Sin este modulo, una empresa que quiere "hacer las cosas bien" corre dos riesgos opuestos: (a) eliminar un dato personal porque ya no lo necesita para la finalidad de la LPDP, sin darse cuenta de que el Codigo Tributario todavia lo exige por 10 anos (riesgo fiscal/mercantil, ajeno a la LPDP pero real para la empresa); o (b) conservar datos personales indefinidamente "por si acaso", lo que en si mismo es una infraccion al principio de temporalidad y agrava el riesgo si luego ocurre un incidente o una solicitud de cancelacion. MOD-016 obliga a que toda decision de "hasta cuando conservar" quede escrita, con su fundamento, antes de que ocurra.
- **Que obligacion(es) cubre.**
  - OBL-RET-01 (Codigo de Comercio, Art. 451 y 454): conservacion de registros mercantiles, 10 anos (hasta 5 anos adicionales tras liquidacion). CONDICIONAL a que la empresa tenga calidad de comerciante.
  - OBL-RET-02 (Codigo Tributario, Art. 147): conservacion de documentacion tributaria y contable, 10 anos. CONDICIONAL a que la empresa tenga obligaciones tributarias en El Salvador (en la practica, casi toda empresa formal).
  - OBL-RET-03 (LCLDA, Art. 10 lit. b y Art. 12): conservacion de documentacion de operaciones (5 anos) y de registros de transacciones (minimo 15 anos). CONDICIONAL a que la empresa sea sujeto obligado bajo el Art. 2 de esa ley (determinacion caso por caso, no automatica).
  - OBL-RET-04 (Lineamientos para el Delegado, Art. 31): conservacion de la documentacion de autorizacion y publicacion del aviso de privacidad, minimo 10 anos. OBLIGATORIO, sin condicion.
  - OBL-RET-05 (Normativa PAS Art. 47 por analogia con la prescripcion de infracciones; Art. 5 lit. i LPDP responsabilidad demostrada): criterio recomendado de retener el expediente de una solicitud ARCO-POL o de un incidente por un minimo de 5 anos, como prueba de descargo. RECOMENDADO; no existe norma expresa que fije este plazo, es un criterio de diseno que requiere validacion de abogado.
  - OBL-RET-06 (Ley de Firma Electronica, Art. 13-A): requisitos para que la conservacion electronica de un documento con relevancia legal (consentimientos, avisos, contratos) cumpla la exigencia legal: consultable en cualquier momento, en el formato original o uno que lo reproduzca con exactitud, integro, legible, completo y sin alteraciones. OBLIGATORIO.
  - Colaboradoras: OBL-PROV-07 (devolucion o eliminacion de datos por el encargado al finalizar la relacion, RECOMENDADO, propietario MOD-009 Proveedores) y OBL-SEG-05 (eliminacion segura de documentos y dispositivos, OBLIGATORIO, propietario MOD-015 Controles de Seguridad) comparten con MOD-016 el mismo patron de "evento de eliminacion con evidencia" (ver seccion D.3), sin que exista entre esos modulos y MOD-016 una dependencia de datos automatizada declarada en el mapa de modulos (ver seccion L). OBL-SANC-07 (prescripcion de infracciones y sanciones a 5 anos, propietario MOD-024 Centro Regulatorio) es la referencia normativa que MOD-016 usa como plazo por defecto de OBL-RET-05.
- **Que valor aporta.**
  - Operativo: evita que cada area (RRHH, Contabilidad, Marketing) decida por su cuenta cuanto tiempo guardar algo, con reglas y alertas centralizadas.
  - Probatorio: cuando la ACE pregunte "por que todavia tienen este dato" o "por que lo eliminaron", la empresa tiene un registro con fecha, fundamento y aprobacion.
  - De reduccion de riesgo: evita dos infracciones simultaneas y opuestas (conservar sin causa, o eliminar antes de una obligacion ajena a la LPDP).
- **Que NO hace este modulo (limites explicitos).**
  - No ejecuta la eliminacion tecnica real en las bases de datos, aplicaciones, archivos o copias de seguridad del cliente; eso lo hace el cliente o su proveedor de TI. El sistema registra la decision, la aprobacion y la constancia, no opera la infraestructura ajena (anti-feature 11 de `22_anti_features.md`).
  - No decide por si mismo si una norma sectorial (mercantil, tributaria, LCLDA, u otra) aplica al giro concreto de la empresa; eso siempre requiere confirmacion humana (ver seccion H).
  - No gestiona la retencion tecnica de copias de seguridad (backups) del cliente; el documento maestro senala esto como "investigar como manejar backups" y esta ficha lo deja fuera del alcance del MVP (ver seccion P, riesgo operativo, y seccion Q).
  - No sustituye el criterio de un abogado sobre que norma sectorial prevalece cuando hay ambiguedad real entre el principio de minimizacion de la LPDP y una obligacion de conservacion de otra ley.

### Doble estado de la reforma 659 aplicado a este modulo

De las 17 obligaciones de la matriz marcadas como afectadas por la reforma 659, una es propia de MOD-016: **OBL-RET-04** (conservacion de la documentacion del aviso de privacidad por 10 anos). La obligacion en si (conservar 10 anos) no desaparece con la reforma, porque el fundamento (Art. 31 de los Lineamientos para el Delegado) es independiente de que el cargo de Delegado sea obligatorio o no. Lo que cambia es el contenido que hay que conservar: mientras el regimen sea `ACTUAL`, el aviso de privacidad debe indicar los datos de contacto del Delegado (Art. 24 lit. h LPDP); si el regimen pasa a `FUTURO`, el aviso republicado indicara los datos del "sujeto obligado" o su Responsable Interno en su lugar. MOD-016 no reescribe versiones ya publicadas (eso corresponde a MOD-008, ver seccion 5, punto 5 de `06_mapa_definitivo_de_modulos.md`); simplemente sigue reteniendo cada version del aviso, con su fecha de publicacion y el regimen vigente en ese momento, durante el minimo de 10 anos, sin importar cuantas veces cambie la bandera `regimen_reforma_659` de MOD-024 mientras tanto. En otras palabras: el motor de retencion documental de MOD-016 es agnostico al regimen; solo consulta la bandera de MOD-024 para decidir que texto de ayuda contextual mostrar (ver seccion R), nunca para acortar o alargar el plazo de conservacion.

---

## B. Usuarios

| Rol estandar | Para que usa MOD-016 |
|---|---|
| Administrador de la organizacion | Configura los parametros generales del modulo (dias de anticipacion de alertas, umbral de doble control) y ve el estado global; normalmente no crea reglas individuales. |
| Delegado de Proteccion de Datos (o Responsable Interno, en estado FUTURO) | Revisa y aprueba las reglas de retencion, aprueba o rechaza eliminaciones cuando actua como Aprobador por defecto, resuelve la revision cuando un dato queda "retenido por obligacion". |
| Responsable ARCO-POL / Responsable del tramite | Consulta si un dato esta "retenido por obligacion" antes de resolver una solicitud de cancelacion u olvido; recibe el borrador de denegatoria parcial motivada que genera MOD-016. |
| Responsable Legal / Compliance | Valida que fundamento (OBL-RET-ID) aplica al giro de la empresa, ajusta plazos cuando el catalogo por defecto no encaja, aprueba excepciones de eliminacion anticipada de documentos de cumplimiento. |
| Responsable de Seguridad / IT | Ejecuta la eliminacion tecnica real fuera del sistema (en las bases de datos, archivos o dispositivos) y sube la constancia; recibe las tareas de "listo para eliminar" que caen en sistemas tecnicos. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Recibe tareas de revision y de eliminacion sobre los datos que administra su area (por ejemplo, CVs de candidatos no contratados, bases de marketing); confirma la constancia cuando ejecuta la eliminacion el mismo. |
| Aprobador | Aprueba la regla de retencion o la eliminacion cuando la cadena de aprobacion configurada exige un segundo revisor distinto de quien la solicito. |
| Auditor (interno) | Solo lectura y exportacion; revisa que cada regla y cada eliminacion tenga fundamento y evidencia completa; nunca aprueba ni adjunta evidencia. |
| Auditor externo (invitado) | Acceso temporal de solo lectura al inventario de reglas y al historial de eliminaciones, durante la auditoria anual de cumplimiento (MOD-018). |
| Usuario de consulta / Colaborador | Ejecuta la tarea puntual de eliminacion o revision que se le asigno, sin ver el resto de las reglas de la organizacion. |
| Titular (formulario externo) | No usa el modulo directamente; lo activa de forma indirecta cuando presenta una solicitud de cancelacion u olvido (MOD-011) que MOD-016 puede bloquear parcialmente si hay una obligacion de retencion vigente. |
| Asesor externo invitado | Acceso puntual y acotado a una regla o un caso concreto en disputa, por ejemplo para dictaminar si aplica o no un fundamento sectorial dudoso. |

---

## C. Permisos

| Accion | Administrador | Delegado / Resp. Interno | Resp. ARCO-POL | Resp. Legal | Resp. Seguridad/IT | Resp. de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Titular | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver reglas e inventario | Si | Si | Si (solo estado "retenido por obligacion" del dato consultado) | Si | Si (solo tecnicas de su area) | Si (solo su area) | Si | Si (solo lectura) | Si (solo lectura, invitado) | Si (solo su tarea asignada) | No | Si (solo caso puntual) |
| Crear regla | Si (config general) | Si | No | Si | No | No | No | No | No | No | No | No |
| Modificar regla (plazo, fundamento) | Si (con motivo) | Si | No | Si | No | No | No | No | No | No | No | No |
| Aprobar regla nueva o eliminacion | No (salvo pyme con advertencia de autorrevision) | Si | No | Si (excepciones documentales) | No | No | Si | No | No | No | No | No |
| Cerrar (confirmar ejecucion tecnica) | No | Si | No | No | Si | Si | No | No | No | Si (si se le asigno la tarea) | No | No |
| Eliminar/archivar el registro de la regla en si | Si (solo config, nunca sobre una regla en ELIMINADO) | No | No | No | No | No | No | No | No | No | No | No |
| Exportar inventario o evidencia | Si | Si | No | Si | No | No | No | Si | Si (solo lo compartido con el) | No | No | No |
| Asignar tarea de revision/ejecucion | Si | Si | No | Si | No | No | No | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si | No | Si |
| Adjuntar evidencia de eliminacion | No | Si | No | No | Si | Si | No | No | No | Si (si se le asigno) | No | No |

**Separacion de funciones.** Quien solicita o ejecuta tecnicamente una eliminacion (Responsable de area o Responsable de Seguridad/IT) no puede ser la misma persona que la aprueba (Aprobador o Delegado), salvo en organizaciones por debajo del umbral configurable (propuesta inicial 50 empleados, ver `05_tipos_de_usuario.md` seccion 5.4), donde se permite con una advertencia visible de "autorrevision". El rol Auditor (interno o externo) nunca crea, aprueba ni adjunta evidencia: su valor depende de que su verificacion sea independiente. Toda excepcion de eliminacion anticipada de un documento de cumplimiento (OBL-RET-04/05) exige doble aprobacion (Delegado y Responsable Legal), sin excepcion de tamano de empresa, porque protege la capacidad probatoria minima del programa.

---

## D. Informacion de entrada

MOD-016 tiene dos motores separados (decision 2.7.13 de `02_validacion_de_la_idea.md`, inconsistencia 15), cada uno con sus propios campos, mas un tercer conjunto de campos comun al momento de ejecutar una eliminacion.

### D.1 Motor de retencion de datos del titular (regla por tratamiento/categoria)

| Campo | Tipo | Obligatorio/opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Nombre de la regla | Texto | Obligatorio | N/A | Maximo 120 caracteres, unico dentro de la organizacion | "Ponle un nombre facil de reconocer, por ejemplo 'Datos de clientes - facturacion'." | Buena practica |
| Tratamiento vinculado | Referencia a Treatment (MOD-006 RAT) | Obligatorio | Catalogo de tratamientos activos del RAT | Debe existir y estar activo | "Elige el tratamiento del RAT al que aplica esta regla, por ejemplo 'Nomina de empleados'." | Buena practica, estructura del RAT |
| Categoria de datos afectada | Seleccion multiple | Obligatorio | Catalogo de categorias del RAT (identificacion, laborales, financieros, sensibles, etc.) | Debe coincidir con las categorias ya registradas en el tratamiento elegido | "Que tipo de dato cubre esta regla." | Buena practica |
| Finalidad | Referencia a Purpose (MOD-006), heredada | Obligatorio, se precarga | Heredado del tratamiento elegido | No editable manualmente | "La razon por la que se recolecto el dato define cuanto tiempo puede conservarse." | Art. 5 lit. h) LPDP |
| Fundamento de retencion | Seleccion multiple | Obligatorio (minimo uno) | Catalogo cerrado: OBL-RET-01 (mercantil, 10a), OBL-RET-02 (tributario, 10a), OBL-RET-03 (LCLDA, 5-15a), "Finalidad de negocio sin norma especifica" | Si se elige la opcion sin norma especifica, el campo de justificacion (siguiente fila) pasa a ser obligatorio | "Elige la norma que te obliga a conservar este dato; si no hay ninguna, dilo y explica por que lo necesitas." | Decision 2.7.13 / inconsistencia 15 de `02_validacion_de_la_idea.md` |
| Justificacion propia | Texto largo | Obligatorio solo si el fundamento elegido es "sin norma especifica" | N/A | Minimo 20 caracteres | "Explica en tus palabras por que necesitas conservar este dato ese tiempo." | Buena practica |
| Plazo por cada fundamento elegido | Numero + unidad (dias, meses, anos) | Obligatorio, se precarga | Precargado segun el OBL-RET elegido (editable solo por Responsable Legal, con motivo) | Mayor a 0 | "El sistema ya trae el plazo legal tipico; puedes ajustarlo si tu abogado te indica otro." | OBL-RET-01/02/03 segun el elegido |
| Evento que dispara el computo | Seleccion unica | Obligatorio | Catalogo: fecha de recoleccion, fecha de fin de la relacion contractual, fecha de la ultima interaccion, fecha de emision del documento | Debe existir un campo de fecha real vinculado en el registro de origen | "Desde que momento empieza a contar el plazo." | Depende del OBL-RET elegido |
| Fecha efectiva de retencion | Fecha, calculada, solo lectura | Generada por el sistema | N/A | Igual al maximo entre todos los plazos de todos los fundamentos activos de la regla | "Esta es la fecha real hasta la que debes conservar el dato; si hay varias normas, el sistema usa la mas larga." | Decision 2.7.13 / inconsistencia 15 |
| Accion al vencer | Seleccion unica | Obligatorio | Catalogo: eliminar, anonimizar, revisar manualmente antes de decidir | Ninguna | "Que debe pasar cuando se cumpla el plazo." | Art. 5 lit. h) LPDP |
| Requiere aprobacion antes de eliminar | Booleano | Obligatorio, por defecto Si | N/A | No editable a "No" si el volumen de titulares afectados supera el umbral configurado | "Por seguridad, casi toda eliminacion necesita que alguien mas la apruebe antes de ejecutarse." | Buena practica, separacion de funciones (05_tipos_de_usuario.md 5.4) |
| Sistema donde vive el dato | Referencia o texto libre | Opcional en el MVP (no existe aun un submodulo dedicado de Catalogo de sistemas, faltante 19 de `02_validacion_de_la_idea.md`) | Catalogo de sistemas si existiera | N/A | "En que sistema o carpeta vive este dato, para que la persona de TI sepa donde ejecutar la eliminacion." | Buena practica |

### D.2 Motor de retencion documental de cumplimiento (reglas predefinidas por el sistema)

| Campo | Tipo | Obligatorio/opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Tipo de documento de cumplimiento | Seleccion unica, preconfigurada | Obligatorio, no editable | Catalogo fijo: Aviso de privacidad publicado, Expediente ARCO-POL cerrado, Expediente de incidente cerrado | Precargado por el sistema al crear el documento/expediente de origen | "Que tipo de prueba de tu propio cumplimiento estas conservando (no es un dato del titular, es la prueba de que hiciste las cosas bien)." | OBL-RET-04 / OBL-RET-05 |
| Documento o expediente de origen | Referencia a Document (MOD-008), PrivacyRequest (MOD-011) o Incident (MOD-013) | Obligatorio | N/A | Debe existir y estar en estado "publicado" (aviso) o "cerrado" (expediente) | "El documento o caso concreto que esta regla protege de borrado." | Buena practica |
| Fecha de inicio del computo | Fecha, heredada automaticamente | Generada por el sistema | Fecha de publicacion (aviso) o fecha de cierre (expediente) | No editable manualmente | "Desde que fecha se cuenta el plazo de conservacion." | OBL-RET-04 (publicacion) / OBL-RET-05 (cierre) |
| Plazo minimo de conservacion | Numero fijo | Generado por el sistema, no editable por defecto | 10 anos (aviso) / 5 anos (expediente, recomendado) | No editable salvo excepcion documentada (ver campo siguiente) | "Este plazo minimo lo trae el sistema; no se puede acortar sin autorizacion." | OBL-RET-04 (10a) / OBL-RET-05 (5a, recomendado) |
| Bloqueo de eliminacion anticipada | Booleano, siempre "Si" por defecto | No editable salvo excepcion con doble aprobacion | N/A | N/A | "Este documento no se puede borrar antes de la fecha, ni por error, sin que dos personas lo autoricen explicitamente." | OBL-RET-04/05, coherente con OBL-RET-06 |
| Motivo de excepcion (eliminacion anticipada) | Texto largo | Obligatorio solo si se solicita forzar la eliminacion antes del plazo | N/A | Minimo 30 caracteres, requiere aprobacion de Delegado y de Responsable Legal | "Explica por que necesitas eliminar esto antes de tiempo; esto queda registrado y puede pedirte explicaciones la ACE." | Advertencia legal, requiere asesoria (ver seccion H) |

### D.3 Evento de eliminacion (comun a ambos motores, se registra al ejecutar)

| Campo | Tipo | Obligatorio/opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Metodo de eliminacion | Seleccion unica | Obligatorio | Catalogo: borrado logico en sistema, borrado fisico/definitivo, anonimizacion, destruccion fisica de documento (trituracion), destruccion de dispositivo | Ninguna | "Como se elimino realmente el dato." | OBL-SEG-05 |
| Constancia adjunta | Archivo | Obligatorio si el metodo es destruccion fisica o ejecucion por proveedor externo; recomendado en los demas casos | N/A | Formato y tamano segun la politica general de adjuntos del sistema | "Sube la foto, acta o certificado que demuestra que se elimino." | OBL-SEG-05, OBL-PRIN-03 |
| Responsable que ejecuto | Referencia a usuario, automatica | Obligatorio | N/A | Debe coincidir con el usuario que confirma el evento | "Quien realizo la eliminacion." | Buena practica, evidencia |
| Aprobador de la eliminacion | Referencia a usuario | Obligatorio si la regla exige aprobacion | N/A | Debe ser distinto del responsable que ejecuto, salvo pyme con advertencia de autorrevision | "Quien autorizo que se eliminara." | Separacion de funciones (05_tipos_de_usuario.md 5.4) |

**Precarga.** Tratamiento, categoria y finalidad (D.1) se precargan desde MOD-006 (RAT). Tipo de documento y documento/expediente de origen, junto con la fecha de inicio del computo (D.2), se precargan automaticamente desde MOD-008, MOD-011 y MOD-013 en el momento en que ese documento se publica o ese expediente se cierra. Los plazos legales por defecto (D.1 y D.2) se precargan desde el catalogo del sistema, basado en el OBL-RET-ID elegido, y solo el Responsable Legal puede editarlos, siempre con motivo.

**Minimizacion de datos personales.** El motor de datos del titular (D.1) no almacena el dato personal en si: guarda referencias (nombre del tratamiento, categoria, sistema donde vive el dato) y metadatos de plazo, coherente con el principio de minimizacion y con el anti-feature 8 de `22_anti_features.md` ("no copiar o centralizar la base de datos completa del cliente"). El motor documental (D.2) tampoco copia datos del titular: referencia el documento o expediente, no su contenido completo. La unica excepcion es indirecta: cuando la regla documental protege un expediente ARCO-POL o de incidente (D.2), ese expediente en si mismo contiene datos personales del titular (nombre, identificacion) porque el proceso de MOD-011/MOD-013 lo exige; MOD-016 no duplica esos datos, solo referencia el expediente por su identificador.

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Estado de retencion por regla (semaforo) | Activo, proximo a vencer, retenido por obligacion, listo para eliminar, aprobado para eliminar, eliminado | Vista en pantalla | Se recalcula diariamente (motor de calendario, MOD-023) y en cada cambio manual | Responsable de area, Delegado, MOD-020 |
| Fecha efectiva de retencion | Fecha calculada (maximo entre todos los fundamentos) | Dato en la regla | Al crear o modificar la regla, o al agregar/quitar un fundamento | Delegado, Responsable Legal, MOD-023 |
| Tarea "Revisar dato proximo a vencer" | Referencia a la regla, plazo restante | Tarea en MOD-021 | Al entrar al estado "proximo a vencer" | Responsable de area, con copia al Delegado |
| Tarea "Aprobar eliminacion" | Referencia a la regla, fundamento, dato/documento afectado | Tarea en MOD-021 | Al entrar al estado "listo para eliminar" | Aprobador o Delegado |
| Tarea "Ejecutar eliminacion tecnica" | Referencia a la regla, metodo sugerido | Tarea en MOD-021 | Al entrar al estado "aprobado para eliminar" | Responsable de area o Responsable de Seguridad/IT |
| Alerta de vencimiento y de eliminacion pendiente | Ver seccion I | Notificacion (MOD-022) | Segun disparador de cada alerta | Segun destinatario de cada alerta |
| Registro de evidencia de eliminacion | Constancia, metodo, responsable, aprobador, fecha | Evidencia en MOD-019 | Al confirmarse la eliminacion (estado "eliminado") | Auditor, ACE en caso de requerimiento |
| Reporte "Inventario de reglas de retencion" | Todas las reglas activas, con estado y fundamento | Reporte (PDF/XLSX) | Bajo demanda o mensual | Delegado, Gerencia, Auditor |
| Indicador de dashboard | "X de Y tratamientos con regla de retencion definida", conteo de pendientes | Vista de dashboard | Continuo | Gerencia, Responsable, Legal, Auditor (MOD-020) |
| Borrador de denegatoria parcial motivada | Fundamento de la retencion vigente sobre el dato solicitado | Texto/borrador | Cuando una solicitud ARCO-POL de cancelacion u olvido (MOD-011) coincide con un dato retenido por obligacion | Responsable ARCO-POL, para revision y aprobacion del Delegado antes de enviarse |
| Evento de auditoria | Creacion, modificacion, cambio de estado, aprobacion, exportacion | Registro en AuditLog (MOD-018) | En cada accion relevante | Auditor |

---

## F. Workflow

MOD-016 usa un unico ciclo de estados, aplicado tanto a las reglas del motor de datos del titular como a las del motor documental (con la diferencia de que en el motor documental el estado "listo para eliminar" nunca se alcanza antes del plazo minimo, salvo excepcion con doble aprobacion, ver D.2).

```
                         +--------------------------+
                    +--->|         ACTIVO           |
                    |    +--------------------------+
                    |               |
                    |               | faltan N dias para la fecha
                    |               | efectiva (configurable, def. 30)
                    |               v
                    |    +--------------------------+
                    |    |   PROXIMO A VENCER        |
                    |    +--------------------------+
                    |          |              |
    vence el nuevo   |         | se cumple    | se registra un
    fundamento        |         | la fecha     | fundamento adicional
    adicional          |         | sin bloqueo  | de retencion
                    |          |              |
                    |          v              v
                    |  +-----------------+  +---------------------------+
                    +--|LISTO PARA       |  | RETENIDO POR OBLIGACION   |
                       |ELIMINAR         |  +---------------------------+
                       +-----------------+              ^
                              |                          |
                              | aprobador confirma        | (recalcula fecha
                              v                          |  efectiva, puede volver
                       +-----------------+                |  a activarse el ciclo)
                       |APROBADO PARA    |----------------+
                       |ELIMINAR         |
                       +-----------------+
                          |          |
           se ejecuta con |          | rechazo tardio o se
           constancia     |          | detecta nueva obligacion
                          v          v
                  +-------------+  +-----------------+
                  |  ELIMINADO  |  | LISTO PARA       |
                  |(o ANONIMIZADO)| | ELIMINAR (vuelve)|
                  +-------------+  +-----------------+
                   (estado terminal)

        +---------------------------------------------------------+
        |                       ARCHIVADO                          |
        |  se alcanza desde cualquier estado activo cuando el      |
        |  tratamiento o documento de origen se da de baja en su   |
        |  modulo propietario antes de cumplirse el plazo; la      |
        |  regla deja de generar alertas pero queda visible en el  |
        |  historial, sin eliminar el dato por si sola             |
        +---------------------------------------------------------+
```

### Tabla de transiciones

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (creacion) | Crear regla de retencion | Debe citar al menos un OBL-RET o justificacion propia; el tratamiento/documento de origen debe existir | ACTIVO | Delegado, Responsable Legal, Administrador (config) | Se calcula la fecha efectiva; evento de auditoria "regla creada" |
| ACTIVO | Paso del tiempo | Faltan N dias (configurable, por defecto 30) para la fecha efectiva | PROXIMO A VENCER | Sistema (automatico, via MOD-023) | Alerta WARNING; tarea de revision en MOD-021 |
| PROXIMO A VENCER | Paso del tiempo | Se cumple la fecha efectiva y no hay fundamento adicional activo | LISTO PARA ELIMINAR | Sistema (automatico) | Alerta HIGH; tarea de aprobacion en MOD-021 |
| PROXIMO A VENCER o LISTO PARA ELIMINAR | Registrar fundamento adicional de retencion | Requiere que el Responsable Legal o el Delegado documenten el nuevo fundamento (OBL-RET-ID o motivo propio) | RETENIDO POR OBLIGACION | Responsable Legal, Delegado | Recalcula la fecha efectiva (nuevo maximo); evento de auditoria; notifica que la revision se pospone |
| RETENIDO POR OBLIGACION | Vence el fundamento adicional | Se cumple la nueva fecha efectiva calculada | ACTIVO o PROXIMO A VENCER (segun la nueva fecha) | Sistema (automatico) | Recalcula el estado |
| LISTO PARA ELIMINAR | Aprobar eliminacion | El aprobador debe ser distinto de quien solicito/ejecuta, salvo pyme con advertencia; para reglas documentales exige doble aprobacion si es antes del plazo minimo | APROBADO PARA ELIMINAR | Aprobador, Delegado (motor documental: tambien Responsable Legal) | Evento de auditoria con identidad y fecha; se habilita la tarea de ejecucion tecnica |
| APROBADO PARA ELIMINAR | Confirmar ejecucion con constancia | Debe registrarse el metodo de eliminacion y, si aplica, la constancia adjunta | ELIMINADO | Responsable de area, Responsable de Seguridad/IT | Se genera evidencia en MOD-019 (OBL-PRIN-03); estado terminal; la regla pasa a solo lectura |
| APROBADO PARA ELIMINAR | Rechazo tardio o error detectado antes de ejecutar | El aprobador revierte con motivo, mientras no se haya confirmado la ejecucion | LISTO PARA ELIMINAR | Aprobador, Delegado | Evento de auditoria con el motivo del rechazo |
| Cualquier estado activo (no terminal) | El tratamiento o documento de origen se da de baja en su modulo propietario (MOD-006, MOD-008, MOD-011, MOD-013) antes de cumplirse el plazo | Automatico cuando el registro de origen se archiva o elimina | ARCHIVADO | Sistema (automatico), o Administrador manualmente con motivo | La regla deja de generar alertas; queda visible en el historial; no elimina el dato por si sola |
| Regla documental (D.2) en cualquier estado no terminal | Solicitud de eliminacion anticipada (antes del plazo minimo) | Requiere motivo documentado y doble aprobacion (Delegado + Responsable Legal) | LISTO PARA ELIMINAR (excepcion) | Delegado y Responsable Legal, ambos | Evento de auditoria CRITICAL; queda registrado como excepcion en el reporte de excepciones (seccion N) |

**Estados terminales.** ELIMINADO y ANONIMIZADO son terminales: no se reabren. Si despues se detecta un error (por ejemplo, se elimino algo que en realidad estaba retenido por otra obligacion), el hecho se documenta como un nuevo evento en MOD-013 (Incidentes de Seguridad), no editando el historial ya cerrado (coherente con el anti-feature 19, bitacora de solo escritura por adicion).

**Reapertura y registros vinculados.** ARCHIVADO no es terminal en sentido estricto: si el tratamiento o documento de origen se reactiva en su modulo propietario, la regla vuelve automaticamente al estado que le corresponda segun su fecha efectiva. Si un documento del motor documental tiene una nueva version publicada en MOD-008, la version anterior sigue sujeta a su propia regla de retencion (OBL-RET-04) hasta cumplir el plazo, incluso si ya no es la version vigente que se muestra al publico.

---

## G. Automatizaciones

| # | Disparador | Condicion | Accion | Configurable por la empresa |
|---|---|---|---|---|
| 1 | Se da de alta un tratamiento en MOD-006 con categoria de datos sensibles o con proveedor fuera del pais | El tratamiento no tiene ninguna regla de retencion de datos del titular asociada | Crear tarea sugerida "Definir regla de retencion para este tratamiento" en MOD-021, para el Responsable de area con copia al Delegado | Si (la sugerencia se puede desactivar; la posibilidad de crear la regla, no) |
| 2 | Se publica una nueva version del aviso de privacidad en MOD-008 | Automatico, sin condicion adicional | Crear automaticamente la regla de retencion documental (OBL-RET-04, 10 anos desde la publicacion) sobre esa version especifica | No (el plazo minimo no se puede desactivar) |
| 3 | Un expediente ARCO-POL (MOD-011) o de incidente (MOD-013) cambia a estado "cerrado" | Automatico, mediante una consulta de referencia a la fecha de cierre (ver nota de dependencia en seccion L) | Crear o actualizar la regla de retencion documental (OBL-RET-05) con fecha efectiva = fecha de cierre + 5 anos por defecto | El plazo por defecto es ajustable por el Responsable Legal (puede extenderse, no acortarse sin excepcion documentada) |
| 4 | La fecha efectiva de una regla llega a N dias de anticipacion | La regla esta en estado ACTIVO | Cambiar a PROXIMO A VENCER; generar alerta WARNING y tarea de revision | Si (dias de anticipacion, por defecto 30) |
| 5 | Se cumple la fecha efectiva de una regla | No existe otro fundamento activo que la retenga | Cambiar a LISTO PARA ELIMINAR; generar alerta HIGH y tarea de aprobacion | No el disparo; si el destinatario |
| 6 | Se registra un fundamento adicional de retencion sobre un dato en PROXIMO A VENCER o LISTO PARA ELIMINAR | Requiere aprobacion de Responsable Legal o Delegado | Cambiar a RETENIDO POR OBLIGACION; recalcular la fecha efectiva | No |
| 7 | Existen dos o mas fundamentos de retencion activos sobre la misma regla | Siempre | Calcular la fecha efectiva como el maximo entre todos los plazos de todos los fundamentos | No (decision 2.7.13, inconsistencia 15) |
| 8 | Se registra la aprobacion de una eliminacion | El estado es LISTO PARA ELIMINAR | Cambiar a APROBADO PARA ELIMINAR; crear tarea de ejecucion tecnica | No |
| 9 | Se confirma la ejecucion con constancia adjunta | El estado es APROBADO PARA ELIMINAR | Cambiar a ELIMINADO; generar evidencia en MOD-019; cerrar la tarea | No |
| 10 | Se presenta una solicitud ARCO-POL de cancelacion u olvido sobre un titular/tratamiento (MOD-011) | El sistema encuentra una regla en estado RETENIDO POR OBLIGACION o con fundamento sectorial activo para ese tratamiento | Generar un borrador de denegatoria parcial motivada con el fundamento correspondiente (Art. 22, OBL-ARCO-06), para revision del Delegado antes de enviarse | No el disparo; el texto del borrador es editable |
| 11 | Se archiva o elimina un tratamiento en MOD-006, o un documento en MOD-008 | La regla de retencion asociada sigue en un estado activo | Cambiar la regla a ARCHIVADO | No |
| 12 | Vence el fundamento adicional que mantenia RETENIDO POR OBLIGACION | Automatico por fecha | Recalcular el estado (vuelve a ACTIVO o PROXIMO A VENCER segun la nueva fecha efectiva) | No |
| 13 | Un usuario intenta forzar el paso a LISTO PARA ELIMINAR sobre una regla documental (OBL-RET-04/05) antes de su plazo minimo | Siempre, salvo que se siga el flujo de excepcion (D.2, campo de motivo, con doble aprobacion) | Bloquear la accion y exigir el flujo de excepcion documentada | No (proteccion minima legal, no configurable) |

---

## H. Decisiones que NO debe automatizar

1. **Determinar si un plazo sectorial (mercantil, tributario, LCLDA, u otro) aplica realmente al giro de una empresa concreta.** El sistema ofrece el catalogo y calcula el maximo entre los fundamentos que el usuario elige, pero no decide por si mismo si esas normas aplican al negocio del cliente. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada". Por que: calificar si una empresa es "sujeto obligado" bajo una ley sectorial (por ejemplo la LCLDA) es una calificacion juridica que depende de hechos del negocio, no de un dato estructurado en el sistema.
2. **Aprobar la eliminacion definitiva de datos de un titular.** El sistema calcula cuando un dato "puede" eliminarse, pero la decision de ejecutar esa eliminacion siempre requiere una aprobacion humana explicita, incluso cuando no hay ningun fundamento de retencion activo. Texto de advertencia mostrado antes de habilitar la accion de aprobar. Por que: una eliminacion es irreversible y puede tener efectos legales o de negocio que el sistema no puede anticipar (por ejemplo, un litigio todavia no registrado en la plataforma).
3. **Resolver un conflicto entre el principio de minimizacion (Art. 5 lit. d) y una obligacion de conservacion ajena a la LPDP, cuando ambas parecen tener el mismo peso.** El sistema muestra ambos fundamentos y su plazo, pero no decide cual prevalece si hay ambiguedad real. Texto de advertencia. Por que: es una cuestion de interpretacion entre normas de distinta materia, propia de asesoria juridica.
4. **Denegar una solicitud ARCO-POL de cancelacion u olvido invocando una regla de retencion.** El sistema genera el borrador de denegatoria motivada, pero nunca lo envia automaticamente al titular; siempre requiere la aprobacion explicita del Delegado (o del Responsable Interno, en estado FUTURO) antes de notificar. Texto de advertencia. Por que: la denegatoria indebida esta en el catalogo de infracciones muy graves (Art. 56 LPDP); exige revision humana con fundamento valido.
5. **Decidir si la conservacion electronica de un documento concreto cumple realmente los requisitos de integridad del Art. 13-A de la Ley de Firma Electronica (OBL-RET-06).** El sistema solo registra el formato declarado; no certifica su validez tecnica futura (por ejemplo, si un formato propietario podria dejar de ser legible con el tiempo). Texto de advertencia. Por que: es una evaluacion tecnico-legal que requiere criterio especializado.
6. **Extender o, sobre todo, acortar el plazo minimo de retencion documental (10 anos del aviso, 5 anos del expediente) por decision unilateral de un solo usuario.** El sistema exige siempre motivo documentado y doble aprobacion (Delegado + Responsable Legal) antes de permitirlo. Texto de advertencia. Por que: acortar estos plazos por debajo del minimo recomendado compromete la capacidad probatoria del programa ante una eventual sancion (OBL-PRIN-03).

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia o repeticion | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Regla proxima a vencer | La regla pasa a PROXIMO A VENCER (N dias antes, por defecto 30) | WARNING | Responsable de area dueno del tratamiento/documento, copia al Delegado | Plataforma + correo | Una vez al entrar, recordatorio semanal mientras siga en ese estado | Si no hay accion en 15 dias, escala al Delegado | Cambia de estado (a LISTO PARA ELIMINAR, RETENIDO POR OBLIGACION o ARCHIVADO) |
| Eliminacion pendiente de aprobacion | La regla pasa a LISTO PARA ELIMINAR | HIGH | Aprobador asignado, copia al Delegado | Plataforma + correo | Una vez, recordatorio cada 5 dias habiles | Si no hay respuesta en 10 dias habiles, escala al Administrador | Se aprueba, se rechaza, o la regla cambia de estado |
| Eliminacion aprobada sin ejecutar | Pasan X dias (configurable, por defecto 5) desde APROBADO PARA ELIMINAR sin confirmar la ejecucion | HIGH | Responsable de area o de Seguridad/IT asignado, copia al Delegado | Plataforma + correo | Recordatorio diario mientras persista | Escala al Delegado a los 10 dias | Se confirma la ejecucion con constancia |
| Intento de eliminar antes del plazo minimo documental | Un usuario intenta forzar LISTO PARA ELIMINAR sobre una regla documental (OBL-RET-04/05) antes de tiempo | CRITICAL | Delegado, Responsable Legal, Administrador | Plataforma + correo | Inmediata, una vez por intento | No hay plazo de espera: ya es notificacion de un intento, no de una tarea pendiente | Se cierra el registro del intento (aprobado como excepcion documentada o descartado) |
| Solicitud ARCO-POL choca con un dato retenido por obligacion | Se dispara la automatizacion G.10 | INFO (Responsable ARCO-POL) / WARNING (Delegado) | Responsable ARCO-POL, Delegado | Plataforma | Una vez por solicitud | Si no se resuelve 5 dias habiles antes del vencimiento del plazo total de la solicitud, escala al Delegado con prioridad alta | Se envia la respuesta al titular |
| Conflicto de fundamentos con plazos muy distintos | Se agregan dos o mas fundamentos a la misma regla con diferencia de plazo mayor a un umbral configurable (por defecto 3 anos) | INFO | Responsable Legal, Delegado | Plataforma | Una vez, al crearse la combinacion | No escala automaticamente (es informativa) | El Responsable Legal confirma que la reviso |

---

## J. Evidencia

| Evidencia | Que prueba (OBL-ID) | Como se conserva |
|---|---|---|
| Registro con fecha y hora de creacion/modificacion de cada regla (quien, cuando, que cambio) | OBL-RET-01 a 06 (existe una politica de retencion documentada y con fundamento); OBL-PRIN-03 (responsabilidad demostrada) | Segun la propia regla documental de cumplimiento del motor (minimo 5 anos tras el cierre del caso relacionado) |
| Historial de cambio de estado de cada regla, con motivo en cada transicion manual | Que el dato no se elimino ni antes ni despues de lo debido (OBL-RET-01 a 06) | Igual que arriba |
| Aprobacion de eliminacion con identidad y fecha del aprobador (doble control) | Separacion de funciones y decision humana explicita (OBL-PRIN-03) | Igual que arriba |
| Constancia de eliminacion (archivo adjunto, con hash si es documento digital) | Eliminacion segura (OBL-SEG-05) | Igual que arriba |
| Evento de auditoria de cada exportacion del inventario o del paquete de evidencia | Trazabilidad (OBL-PRIN-03) | AuditLog (MOD-018), append-only |
| Registro de intentos bloqueados de eliminar antes del plazo minimo documental | Que el control de integridad funciono (OBL-RET-06) | Igual que la regla documental que protegio |
| Vinculo entre la denegatoria motivada de una solicitud ARCO-POL y la regla de retencion que la sustenta | Fundamento de la denegatoria (OBL-ARCO-06, propietario MOD-011) | Se conserva junto al expediente ARCO-POL, sujeto a su propia regla documental (OBL-RET-05) |

Toda esta evidencia se expone tambien, de forma consolidada, en el Centro de Evidencias (MOD-019), con verificacion de integridad en cada exportacion (anti-feature 25 de `22_anti_features.md`).

---

## K. Documentos asociados

- **Documentos requeridos como entrada:** contrato con proveedor de destruccion certificada (si la empresa contrata ese servicio, como evidencia de OBL-SEG-05); politica de retencion documental previa de la empresa, si ya existia antes de migrar a la plataforma.
- **Documentos generados:**
  - Constancia interna de eliminacion (documento simple generado por el sistema con los datos del evento: que, cuando, quien, metodo).
  - Inventario de reglas de retencion (exportable).
  - Borrador de denegatoria motivada por retencion, para uso de MOD-011.
- **Plantillas que el sistema provee:**
  - "Politica de retencion y eliminacion de datos personales" (variables: nombre de la empresa, catalogo de reglas configuradas, plazos por categoria; requiere validacion de la organizacion antes de publicarse como politica oficial).
  - "Acta o constancia de destruccion" (variables: metodo, responsable, fecha, testigo si aplica).
- **Anexos y evidencias documentales:** constancias de destruccion fisica, capturas o logs de borrado de sistemas, contrato con proveedor de destruccion certificada.

---

## L. Dependencias

```
MOD-006 RAT y Mapa de Datos    ---->  +-----------------------------+
                                        |   MOD-016 Retencion y        |  ----> MOD-011 ARCO-POL
MOD-008 Documentos y Politicas ---->  |   Eliminacion (dos motores)  |  ----> MOD-019 Centro de Evidencias
                                        +-----------------------------+
```

- **Entra desde (dependencia estructural declarada en `mapa_modulos.json`):** MOD-006 (tratamientos, categorias, finalidad, para el motor de datos del titular), MOD-008 (avisos publicados y sus versiones, para el motor documental).
- **Sale hacia (alimenta_a declarado):** MOD-011 (consulta si un dato esta retenido antes de resolver una cancelacion u olvido), MOD-019 (toda evidencia de reglas y eliminaciones).
- **Consumo del patron transversal general (igual que todo modulo operativo, sin ser una dependencia especifica de MOD-016):** MOD-021 (tareas), MOD-022 (alertas), MOD-023 (calendario, para calcular la fecha efectiva), MOD-020 (indicadores de dashboard), MOD-024 (referencia constante del regimen de la reforma 659 para el texto de ayuda de OBL-RET-04).
- **Colaboracion conceptual sin dependencia de datos automatizada (comparten el mismo patron de "evento de eliminacion con evidencia", D.3, pero sin flujo declarado en el mapa de modulos):** MOD-009 (cuando termina una relacion con un encargado, OBL-PROV-07), MOD-015 (cuando se ejecuta un control de eliminacion segura de un dispositivo, OBL-SEG-05).
- **Que ocurre si el modulo no existe en el MVP.** La conservacion pasiva de los documentos de cumplimiento (aviso 10 anos, expedientes 5 anos) sigue ocurriendo, porque MOD-008, MOD-011 y MOD-013 simplemente no permiten borrar esos registros por defecto (comportamiento nativo de cada modulo, sin alerta ni flujo de aprobacion explicito). El motor de retencion de datos del titular, con calculo del maximo entre normas sectoriales (inconsistencia 15), no existe: la resolucion de conflictos entre bases queda como una nota manual en el campo de texto libre "plazo de conservacion" dentro del RAT (MOD-006), sin automatizacion ni alerta. La empresa asume ese riesgo de forma manual hasta que el modulo se construya (ver seccion Q).

> **Nota de coherencia con el mapa de modulos (senalada aqui, no corregida por esta ficha).** `mapa_modulos.json` declara `depende_de: ["MOD-006", "MOD-008"]` y `alimenta_a: ["MOD-011", "MOD-019"]` para MOD-016. Esta ficha disena la automatizacion G.3 (creacion de la regla documental OBL-RET-05 al cerrarse un expediente ARCO-POL o de incidente) de forma que MOD-016 necesita leer la fecha de cierre de MOD-011 y de MOD-013, ademas de MOD-008. En sentido estricto, eso implica que MOD-016 tambien deberia listar a MOD-011 y a MOD-013 en su `depende_de`, y esos dos modulos deberian incluir a MOD-016 en su `alimenta_a` (regla de consistencia de la seccion 6.1 de `06_mapa_definitivo_de_modulos.md`). Hoy ninguno de los dos lo hace: el `alimenta_a` de MOD-011 y de MOD-013 no incluye a MOD-016. Se recomienda actualizar el mapa definitivo para reflejar esa dependencia adicional (necesaria para que OBL-RET-05 se cumpla de forma activa una vez que el modulo se construya), en vez de omitir la obligacion o inventar un mecanismo distinto al descrito en la seccion 6.1.

---

## M. Dashboard

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Reglas de retencion activas | Cuenta de reglas en estado ACTIVO o PROXIMO A VENCER | Verde si ninguna esta vencida sin revisar; amarillo si hay proximas a vencer; rojo si hay LISTO PARA ELIMINAR sin aprobar por mas del SLA interno | Responsable, Legal |
| Eliminaciones pendientes de aprobacion | Cuenta de reglas en estado LISTO PARA ELIMINAR | Rojo si es mayor a 0 y vencido el SLA interno | Legal, Gerencia (resumen), Responsable |
| Documentos de cumplimiento bajo retencion obligatoria | Cuenta de reglas documentales activas (avisos + expedientes) | Sin semaforo (informativo) | Auditor, Legal |
| Intentos bloqueados de eliminacion anticipada (ultimos 90 dias) | Cuenta de eventos de la automatizacion G.13 en el periodo | Rojo si es mayor a 0 | Auditor, Gerencia |
| Cobertura del motor de retencion | Tratamientos del RAT con al menos una regla de retencion definida, sobre el total de tratamientos activos, mostrado como "X de Y tratamientos con regla de retencion definida" | Sin semaforo de porcentaje; se muestra como conteo | Responsable, Legal, Gerencia |

Todas las vistas usan lenguaje de estado del programa (controles configurados, tareas pendientes, evidencia disponible); nunca se expresa como "porcentaje de cumplimiento legal" (anti-feature 5 de `22_anti_features.md`).

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Inventario de reglas de retencion | Todas las reglas, estado, fundamento, fecha efectiva | Modulo de origen, estado, categoria de datos | PDF / XLSX | Delegado, Gerencia, Auditor | Si |
| Historial de eliminaciones | Eventos ELIMINADO con constancia, aprobador, metodo | Rango de fechas, tipo de dato o documento | PDF / CSV / ZIP (con adjuntos) | Auditor, ACE en caso de requerimiento | Si |
| Excepciones y eliminaciones anticipadas | Casos donde se forzo una eliminacion antes del plazo minimo documental, con motivo y doble aprobacion | Rango de fechas | PDF | Delegado, Auditor | Si |
| Reglas sin fundamento sectorial confirmado | Reglas creadas con fundamento propio (no un OBL-RET catalogado), pendientes de validacion legal | Por area | XLSX | Responsable Legal | No (es de gestion interna) |

---

## O. Historial

Eventos que quedan en el historial del modulo y en la auditoria transversal (MOD-018):
- Creacion de una regla, con el fundamento citado en ese momento.
- Modificacion de cualquier campo, en especial plazo y fundamento (valor anterior y nuevo).
- Cambio de estado, con motivo cuando la transicion es manual (por ejemplo, registrar un fundamento adicional o forzar una excepcion).
- Asignacion de tarea de revision, aprobacion o ejecucion.
- Aprobacion o rechazo de una eliminacion, con identidad, fecha y motivo si es un rechazo.
- Adjunto de la constancia de eliminacion.
- Exportacion del inventario o de un paquete de evidencia.
- Intento bloqueado de eliminacion anticipada (automatizacion G.13).
- Archivado de una regla por baja del registro de origen.
- Acceso de lectura a un expediente vinculado que contenga datos sensibles del titular, cuando la regla se relaciona con un expediente ARCO-POL o de incidente.

---

## P. Riesgos

- **Legal.** Dar por valido un fundamento sectorial que en realidad no aplica al giro del cliente (por ejemplo, asumir la LCLDA sin que la empresa sea sujeto obligado). Mitigacion de diseno: obligar a citar el OBL-RET especifico y mostrar siempre el texto "Requiere validacion de la organizacion o asesoria especializada" antes de activar un fundamento sectorial nuevo (seccion H.1).
- **Legal.** Eliminar un dato antes de tiempo por no detectar una obligacion de conservacion simultanea de otra norma. Mitigacion: calculo del maximo entre todos los fundamentos activos (G.7) y bloqueo estructural para las reglas documentales (G.13).
- **UX.** Abandono de la configuracion de reglas por percibirse como una tarea tecnica y ajena a un usuario no especialista. Mitigacion: las reglas documentales se crean automaticamente sin intervencion (G.2, G.3); el motor de datos del titular ofrece sugerencias con plazos precargados en vez de un formulario en blanco.
- **Operativo.** Plazos mal calculados por una fecha de inicio de computo mal capturada en el modulo de origen, o por un calendario de dias/anos desactualizado. Mitigacion: la fecha de inicio se hereda automaticamente de MOD-006/MOD-008/MOD-011/MOD-013, no se digita manualmente salvo excepcion justificada; el calculo de la fecha efectiva usa el motor de calendario centralizado (MOD-023).
- **Operativo.** Acumulacion de reglas "proximas a vencer" sin revisar, por sobrecarga del responsable de area. Mitigacion: escalamiento automatico al Delegado tras 15 dias sin accion (I, fila 1).
- **Seguridad y privacidad.** La constancia de eliminacion adjunta contiene, por error, datos personales completos del titular en vez de solo evidencia del evento. Mitigacion: plantilla de constancia predefinida que solo captura metadatos (metodo, fecha, responsable), con advertencia al subir archivos distintos de la plantilla.
- **Seguridad y privacidad.** Un usuario con permisos de Administrador fuerza una eliminacion anticipada de un documento de cumplimiento para ocultar evidencia desfavorable. Mitigacion: bloqueo estructural con doble aprobacion obligatoria y alerta CRITICAL inmediata al Delegado y al Responsable Legal (G.13, I fila 4), sin posibilidad de que el mismo Administrador se autoapruebe.
- **Operativo y legal.** La eliminacion tecnica real se ejecuta fuera del sistema (en la base de datos del cliente) sin que quede registrada la constancia, dejando el estado del modulo desalineado con la realidad. Mitigacion: el estado APROBADO PARA ELIMINAR no pasa a ELIMINADO automaticamente; requiere confirmacion explicita con constancia (seccion F, transicion correspondiente), y genera alerta si pasan mas de X dias sin confirmarse (I, fila 3).
- **Operativo (fuera de alcance declarado).** El documento maestro senala "investigar como manejar backups" sin resolverlo; si una empresa interpreta que MOD-016 tambien controla la retencion de copias de seguridad tecnicas, se generaria una falsa sensacion de cobertura. Mitigacion: el modulo declara explicitamente en la seccion A que no gestiona backups tecnicos, y el texto de ayuda contextual (seccion R) lo aclara.

---

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Motor de retencion de datos del titular: reglas por categoria/tratamiento/sistema/finalidad, citando uno o mas OBL-RET | | X | | | Resuelve la inconsistencia 15, pero solo aplica de forma condicional segun el giro de la empresa; sin plazo transitorio vencido especifico ni ser dependencia estructural de otro modulo MUST HAVE (coherente con la clasificacion global SHOULD HAVE del mapa). |
| Calculo automatico de la fecha efectiva como maximo entre todos los fundamentos aplicables | | X | | | Depende de que exista el motor de datos del titular (fila anterior); sin el, no tiene sentido por si solo. |
| Motor de retencion documental de cumplimiento con estado explicito, alerta y flujo de aprobacion de eliminacion (OBL-RET-04, OBL-RET-05) | | X | | | OBL-RET-04 y OBL-RET-06 son OBLIGATORIO, pero la conservacion pasiva ya ocurre desde el MVP dentro de MOD-008/MOD-011/MOD-013 sin necesidad de este motor (patron de "cobertura parcial" documentado en `06_mapa_definitivo_de_modulos.md`); lo que aporta este motor es el estado visible, la alerta y el flujo formal de excepcion. |
| Estados completos con semaforo (activo, proximo a vencer, retenido por obligacion, listo para eliminar, aprobado para eliminar, eliminado, archivado) | | X | | | Requiere que exista al menos uno de los dos motores; no tiene valor por separado. |
| Flujo de aprobacion de eliminacion con doble control | | X | | | Ligado a la separacion de funciones general del sistema (05_tipos_de_usuario.md 5.4), que ya es SHOULD/MUST segun el modulo que la implemente; aqui depende de que el motor exista primero. |
| Registro de evidencia de eliminacion (constancia, metodo, hash si aplica) | | X | | | Intrinseco al modulo una vez construido; no se puede separar sin perder el valor probatorio, por eso viaja con la misma clasificacion del conjunto. |
| Bloqueo estructural de eliminacion anticipada de documentos de cumplimiento, con excepcion de doble aprobacion | | X | | | Proteccion minima que solo tiene sentido si el motor documental existe; en su ausencia, la proteccion equivalente es que MOD-008/011/013 simplemente no exponen un boton de borrar. |
| Catalogo de plazos sectoriales preconfigurados adicionales (por ejemplo, expediente clinico 10 anos para el sector salud) | | | X | | Enriquecimiento del catalogo de fundamentos; requiere mantenimiento por sector y no es indispensable para que el motor basico funcione con los tres fundamentos ya cubiertos (mercantil, tributario, LCLDA). |
| Panel de conflictos de fundamentos con recomendaciones automaticas de consolidacion | | | X | | Mejora de analisis sobre datos que el motor basico ya calcula; no es necesario para que el calculo del maximo (G.7) funcione. |
| Gestion de retencion de copias de seguridad (backups) tecnicas del cliente | | | | X | El documento maestro lo deja como pendiente de investigar; toca infraestructura tecnica que este modulo no ejecuta (anti-feature 11); requiere primero definir con el cliente que herramienta tecnica gestiona sus backups. |
| Integracion tecnica que ejecute la eliminacion real en los sistemas del cliente (purga automatizada) | | | | | Fuera de alcance permanente (no es una fase futura, es un limite de producto): el sistema nunca ejecuta controles tecnicos en la infraestructura del cliente (anti-feature 11 de `22_anti_features.md`); la ejecucion siempre la confirma una persona con una constancia. |

**Version minima ya vendible del modulo.** Sin construir MOD-016, el producto ya cumple de forma pasiva OBL-RET-04 y OBL-RET-06 (MOD-008 no permite borrar avisos publicados antes de 10 anos) y aplica el criterio recomendado de OBL-RET-05 dentro de MOD-011 y MOD-013 (los expedientes cerrados no se eliminan por defecto). La version minima de MOD-016 que justifica construirlo como modulo propio, para V1, es el motor de retencion de datos del titular con calculo del maximo entre fundamentos (filas 1 y 2 de esta tabla) junto con el estado y la alerta basica (fila 4): eso es lo que ninguna otra parte del sistema puede resolver por si sola, porque exige combinar catalogos legales de fuera de la LPDP (Codigo de Comercio, Codigo Tributario, LCLDA) que hoy no vive en ningun otro modulo.

---

## R. Ayuda contextual

**1. Que es una regla de retencion**
- Que es: una instruccion que le dice al sistema cuanto tiempo debe conservarse un dato o un documento, y que hacer cuando se cumpla ese tiempo.
- Por que tengo que hacer esto: para no guardar datos personales mas tiempo del necesario, pero tampoco eliminarlos antes de una obligacion legal distinta que te exige conservarlos (por ejemplo, tus registros contables).
- Fundamento: Art. 5 lit. h) LPDP (principio de temporalidad); OBL-RET-01 a 06 segun el tipo de dato.
- Cuando necesito ayuda juridica: cuando no estas seguro si una ley distinta a la LPDP (tributaria, mercantil, contra el lavado de dinero) aplica a tu empresa o al dato concreto.

**2. Que es la fecha efectiva de retencion**
- Que es: la fecha real hasta la que debes conservar un dato, calculada automaticamente como la mas lejana entre todos los plazos que apliquen a ese dato.
- Por que tengo que hacer esto: si un mismo dato tiene dos razones para conservarse (por ejemplo, la LPDP y una obligacion tributaria), el sistema usa siempre la fecha mas larga, para que no elimines algo antes de tiempo por error.
- Fundamento: decision de diseno documentada en `02_validacion_de_la_idea.md`, seccion 2.7.13 (inconsistencia 15), basada en el Art. 5 lit. h) LPDP y en las obligaciones sectoriales OBL-RET-01 a 03.
- Cuando necesito ayuda juridica: cuando la diferencia entre los plazos es muy grande (por ejemplo, varios anos) y no tienes claro cual de las dos normas realmente aplica a tu caso.

**3. Diferencia entre el motor de datos del titular y el motor de retencion documental**
- Que es: MOD-016 tiene dos motores separados. Uno cuida los datos personales de tus clientes o empleados (por ejemplo, cuanto tiempo guardar su numero de telefono). El otro cuida tus propios documentos de cumplimiento (el aviso de privacidad que publicaste, o el expediente de una solicitud que ya cerraste), que son tu prueba de que hiciste las cosas bien.
- Por que tengo que hacer esto: si se mezclaran los dos, podrias borrar por error el aviso de privacidad junto con los datos de un titular especifico, o borrar datos del titular antes de tiempo por una obligacion de conservar tu propio expediente.
- Fundamento: decision de diseno 2.7.13 de `02_validacion_de_la_idea.md`; OBL-RET-04 y OBL-RET-05 (motor documental) frente a OBL-RET-01 a 03 (motor de datos del titular).
- Cuando necesito ayuda juridica: si no tienes claro si un registro concreto es un "dato del titular" o un "documento de tu propio cumplimiento".

**4. Que significa que un dato quede "retenido por obligacion"**
- Que es: un estado que indica que, aunque el plazo normal de la LPDP ya se cumplio, existe otra razon documentada (por ejemplo, un litigio en curso o una obligacion tributaria) que impide eliminar ese dato todavia.
- Por que tengo que hacer esto: para poder explicar, si un titular pide que elimines su dato, por que legitimamente no puedes hacerlo todavia (denegatoria parcial motivada).
- Fundamento: Art. 22 LPDP (denegatoria motivada), OBL-ARCO-06 (propietario MOD-011); OBL-RET-01 a 03 como fundamento tipico de esta retencion.
- Cuando necesito ayuda juridica: siempre que vayas a usar este estado para responder a una solicitud de un titular, antes de enviar la respuesta.

**5. Eliminacion segura**
- Que es: destruir un documento fisico (por ejemplo, con trituradora) o borrar de forma definitiva un archivo o dispositivo electronico, de manera que el dato personal no se pueda recuperar despues.
- Por que tengo que hacer esto: para que la eliminacion sea real y no solo aparente (por ejemplo, mover un archivo a una carpeta de "papelera" no es eliminacion segura).
- Fundamento: OBL-SEG-05 (Politicas de Actuacion ACE, Art. 4, Medidas Fisicas lit. e).
- Cuando necesito ayuda juridica: si vas a contratar un proveedor externo de destruccion certificada y necesitas saber que clausulas debe incluir el contrato.

**6. Por que este modulo no cambia de nombre ni de estructura con la reforma 659**
- Que es: aunque la reforma 659 puede cambiar quien es responsable de las funciones del Delegado, este modulo sigue funcionando igual: conserva cada version del aviso de privacidad y cada expediente por el plazo minimo que le corresponde, sin importar si el regimen es el actual o el futuro.
- Por que tengo que hacer esto: para que no pierdas evidencia de cumplimiento pasado solo porque cambio quien firma los documentos nuevos.
- Fundamento: seccion 5 de `06_mapa_definitivo_de_modulos.md` (doble estado sin duplicar modulos); OBL-RET-04.
- Cuando necesito ayuda juridica: si tienes dudas sobre que version de un aviso de privacidad sigue vigente despues de un cambio de regimen.

---

## Notas finales (desacuerdos y observaciones sobre las fuentes de diseno)

1. **Dependencia no declarada entre MOD-016 y MOD-011/MOD-013 para OBL-RET-05.** Como se explica en la seccion L, esta ficha disena el motor documental de MOD-016 para que lea la fecha de cierre de los expedientes ARCO-POL (MOD-011) y de incidentes (MOD-013), porque OBL-RET-05 cubre expresamente ambos tipos de expediente. `mapa_modulos.json` no incluye esa relacion: el `depende_de` de MOD-016 solo lista MOD-006 y MOD-008, y el `alimenta_a` de MOD-011 y de MOD-013 no incluye a MOD-016. Se recomienda agregar esa dependencia al mapa definitivo (MOD-016 depende tambien de MOD-011 y MOD-013; ambos incluyen a MOD-016 en su `alimenta_a`), para que la automatizacion G.3 de esta ficha sea consistente con la regla de trazabilidad de la seccion 6.1 del mapa. No se modifico el mapa desde esta ficha; solo se senala aqui.
2. **OBL-PROV-07 y OBL-SEG-05 como colaboradoras sin flujo automatizado.** El mapa marca estas dos obligaciones como colaboradoras de MOD-016, pero ni MOD-009 ni MOD-015 aparecen conectados a MOD-016 en el grafo de dependencias. Esta ficha interpreta esa colaboracion como conceptual (comparten el mismo patron de "evento de eliminacion con evidencia", seccion D.3), sin proponer un flujo de datos automatizado entre modulos que el mapa no contempla. Si en una siguiente iteracion se decide automatizar esa relacion, deberia reflejarse tambien en `mapa_modulos.json`.
3. **Plazo de OBL-RET-03 (LCLDA) con dos valores distintos segun el tipo de registro.** La matriz de obligaciones distingue documentacion de operaciones (5 anos) de registros de transacciones (minimo 15 anos), ambos bajo el mismo OBL-ID. Esta ficha modela el campo "plazo" del fundamento OBL-RET-03 como editable por el Responsable Legal (D.1) precisamente porque un solo plazo precargado no puede representar ambos casos sin intervencion humana; se advierte esto para que no se automatice un valor unico de 5 o de 15 anos sin revision.
4. **Backups fuera de alcance.** Se confirma como decision de esta ficha (no como hallazgo nuevo) que la gestion de retencion de copias de seguridad tecnicas queda fuera del MVP y de V1 de este modulo, coherente con el anti-feature 11 y con la nota "investigar como manejar backups" del documento maestro, que sigue sin resolverse y no le corresponde resolverla a esta ficha funcional.
