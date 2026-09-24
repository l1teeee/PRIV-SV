# EP-015 Controles de Seguridad (MOD-015)

**Objetivo.** Con esta epica la empresa mantiene un catalogo unico de controles de seguridad organizativos, tecnicos y fisicos, cada uno con estado, responsable y evidencia adjunta, puede exceptuar un control con la aprobacion de un segundo usuario, vincula cada control al sistema o tratamiento del RAT que protege, y ve de un vistazo cuantos controles obligatorios del catalogo base siguen sin evidencia frente al riesgo de infraccion grave del Art. 56 lit. b.

| Release principal | HU | Puntos | Puntos R1 | Puntos R2 | Ficha funcional |
|---|---|---|---|---|---|
| R2 | 14 | 51 | 0 | 51 | [MOD-015](../../03_modulos/MOD-015_ficha.md) |

**Notas de la epica.**

- El campo Estado de la seccion D de la ficha enumera seis valores (incluye Implementado con hallazgo y Vencido), pero el subciclo que los alcanza (En revision, deteccion de hallazgos en revision periodica, vencimiento automatico) pertenece por completo a la fila SHOULD HAVE 'Alertas de vencimiento y revision periodica' de la tabla Q y coincide con la indicacion explicita del encargo 'sin alertas automatizadas de vencimiento en el MVP'. Esta epica limita el MVP a los estados Pendiente de implementar, Implementado, No aplica - Exceptuado y Archivado (con reactivacion a Pendiente de implementar); Implementado con hallazgo, En revision y Vencido quedan fuera de esta epica y no se generan HU para ellos.
- Por el mismo motivo, el indicador 'Controles obligatorios sin evidencia o vencidos' de las secciones E y M de la ficha se cubre en esta epica solo en su parte 'sin evidencia' (controles del catalogo base en Pendiente de implementar); la parte 'o vencidos' depende del estado Vencido excluido en el punto anterior.
- La fila Q 'Reportes exportables (checklist, paquete de evidencia con verificacion de integridad)' es SHOULD HAVE. Esta epica cubre unicamente la vista y el filtro en pantalla del catalogo, como parte de la fila MUST HAVE 'Catalogo base de controles'; no incluye exportacion formal a PDF/XLSX, paquete de evidencia en ZIP ni verificacion de integridad del paquete exportado.
- Las filas Q 'Vinculacion estructurada con Transferencias Internacionales (MOD-010)' (COULD HAVE) y 'Entidad Control compartida en tiempo real con EIPD (MOD-014)' (SHOULD HAVE) quedan fuera de esta epica. Para OBL-SEG-04 se cubre con el campo generico de texto libre (pais y proveedor) que la propia ficha describe en su seccion L, tal como indica el encargo. La automatizacion de la seccion G 'MOD-014 necesita un control que no existe' tampoco genera HU porque depende de MOD-014, modulo SHOULD HAVE fuera de las release R1/R2 de esta ronda del MVP.
- La ficha usa 'Gerencia' como destinatario de varios indicadores, pero ese texto no es uno de los roles permitidos por las instrucciones comunes. Se homologa a 'Administrador de la organizacion', conforme a 05_tipos_de_usuario.md seccion 5.3 (el rol Administrador lo suele ocupar el dueno o gerente general de la empresa).
- El registro de accesos de lectura a evidencia tecnica sensible (secciones J y O de la ficha) esta marcado en la propia ficha como opinion de producto/buena practica de seguridad, no como exigencia de la LPDP, y no corresponde a ninguna fila MUST HAVE de la tabla Q ni a una indicacion especifica del encargo; no se genera HU para el en esta epica.
- Todas las HU de esta epica van a release R2, igual que el resto del modulo, porque MOD-015 no tiene una capa de infraestructura propia en R1 (a diferencia de modulos como MOD-021 o MOD-023): toda su version minima depende de que el diagnostico (MOD-004, R1) y el RAT (MOD-006, R1) ya existan, pero el propio catalogo de controles se construye completo en R2, segun 19.9.

## Resumen

| HU | Titulo | Rol | Puntos | Release | Sprint | Depende de |
|---|---|---|---|---|---|---|
| HU-015-01 | Crear un control de seguridad en el catalogo | Responsable de Seguridad / IT | 3 | R2 | 8 | - |
| HU-015-02 | Editar los datos de un control existente | Responsable de Seguridad / IT | 2 | R2 | 24 | HU-015-01, MOD-009 |
| HU-015-03 | Consultar y filtrar el catalogo de controles segun el rol | Responsable de Seguridad / IT | 5 | R2 | 24 | HU-015-01 |
| HU-015-04 | Vincular un control al Sistema o Tratamiento que protege | Responsable de Seguridad / IT | 3 | R2 | 24 | HU-015-01, MOD-006 |
| HU-015-05 | Registrar pais y proveedor de una transferencia en un control SSL/TLS | Responsable de Seguridad / IT | 2 | R2 | 24 | HU-015-01 |
| HU-015-06 | Marcar un control como Implementado adjuntando evidencia | Responsable de Seguridad / IT | 5 | R2 | 24 | HU-015-01, HU-015-04, MOD-019, MOD-008 |
| HU-015-07 | Exigir un segundo aprobador para implementar un control critico | Administrador de la organizacion | 5 | R2 | 25 | HU-015-06, MOD-021 |
| HU-015-08 | Registrar una excepcion de control con justificacion | Responsable de Seguridad / IT | 3 | R2 | 25 | HU-015-01, MOD-021 |
| HU-015-09 | Aprobar o rechazar una excepcion de control | Aprobador | 5 | R2 | 25 | HU-015-08, MOD-021 |
| HU-015-10 | Archivar y reactivar un control | Responsable de Seguridad / IT | 3 | R2 | 25 | HU-015-01 |
| HU-015-11 | Precargar el catalogo base de controles al completar el diagnostico | Responsable de Seguridad / IT | 5 | R2 | 25 | HU-015-01, MOD-004, MOD-024 |
| HU-015-12 | Mostrar el indicador de controles con evidencia vigente | Responsable de Seguridad / IT | 5 | R2 | 25 | HU-015-06, HU-015-10 |
| HU-015-13 | Mostrar el indicador de controles obligatorios sin evidencia | Responsable Legal / Compliance | 3 | R2 | 25 | HU-015-11 |
| HU-015-14 | Consultar el historial de cambios de un control | Auditor (interno) | 2 | R2 | 24 | HU-015-01 |

## Historias

### HU-015-01. Crear un control de seguridad en el catalogo

**Como** Responsable de Seguridad / IT, **quiero** registrar un nuevo control de seguridad indicando su nombre, categoria (Organizativa, Tecnica o Fisica), tipo de control, responsable interno y periodicidad de revision, **para** tener en un solo catalogo cada medida organizativa, tecnica y fisica que exige el Art. 4 de las Politicas de Actuacion de la ACE, con quien responde por ella.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 8 | No |

- Fundamento: OBL-SEG-02 (Art. 4 (Medidas Organizativas, lit. a-f), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-SEG-03 (Art. 4 (Medidas Tecnicas), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-SEG-05 (Art. 4, Medidas Fisicas lit. e), Politicas de Actuacion ACE)
- Depende de: -
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el Responsable de Seguridad / IT completa Nombre del control, Categoria, Tipo de control, Responsable del control y Periodicidad de revision, cuando guarda el formulario, entonces el sistema crea el control en estado Pendiente de implementar y registra el evento de creacion en el historial (AuditLog) con la identidad de quien lo creo.
2. Dado que el campo Nombre del control queda vacio, cuando el usuario intenta guardar, entonces el sistema rechaza el guardado y senala que el nombre es obligatorio.
3. Dado que el usuario escribe mas de 120 caracteres en Nombre del control o mas de 2000 caracteres en Descripcion / alcance, cuando intenta guardar, entonces el sistema rechaza el guardado por exceder el maximo permitido.
4. Dado que el usuario selecciona la categoria Tecnica, cuando abre la lista de Tipo de control, entonces solo ve las opciones del catalogo tecnico (por ejemplo Autenticacion en dos pasos (2FA), Cifrado en reposo, Cifrado en transito, Copias de respaldo, Firewall / antivirus / IDS-IPS, Analisis de vulnerabilidades, Pentesting, Digitalizacion mediante sistema especializado, Protocolo de comunicacion segura (SSL/TLS) para transferencias, Otro), y no ve las opciones de Organizativa ni de Fisica.
5. Dado que el usuario elige el tipo de control Otro, cuando guarda el formulario sin escribir el texto libre que describe ese tipo, entonces el sistema rechaza el guardado por dato obligatorio faltante.
6. Dado un usuario con rol Responsable de area, Usuario de consulta / Colaborador o Auditor (interno), cuando intenta crear un control, entonces el sistema deniega la accion porque su rol no tiene permiso para crear controles.
7. Dado que se crea un control, cuando se guarda, entonces el sistema no ejecuta, instala ni configura ningun control tecnico real en los sistemas de la empresa; solo registra el dato del catalogo.

**Reglas de negocio**

- El estado inicial de todo control creado es siempre Pendiente de implementar (secciones D y F de la ficha).
- El Tipo de control pertenece al catalogo cerrado de la Categoria elegida; la opcion Otro habilita un texto libre (seccion D).
- Solo Administrador de la organizacion y Responsable de Seguridad / IT pueden crear controles (seccion C, fila Crear control).

**Fuera de alcance**

- Vincular el control a un Sistema o Tratamiento (ver HU-015-04).
- Adjuntar evidencia y marcar el control como Implementado (ver HU-015-06).

- Referencia: MOD-015 secciones C (permisos, fila Crear control), D (campos Nombre del control, Categoria, Tipo de control, Responsable del control, Periodicidad de revision) y F (estado inicial del workflow)

### HU-015-02. Editar los datos de un control existente

**Como** Responsable de Seguridad / IT, **quiero** modificar los campos de un control ya creado, incluido el proveedor externo que lo administra, **para** mantener el catalogo actualizado cuando cambian los datos de una medida de seguridad.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R2 | 24 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales); OBL-PROV-03 (Art. 36, Ley para la Proteccion de Datos Personales)
- Depende de: HU-015-01
- Modulos requeridos: MOD-009

**Criterios de aceptacion**

1. Dado un control existente, cuando el Responsable de Seguridad / IT cambia el Responsable del control y guarda, entonces el sistema aplica el cambio y registra en el historial el valor anterior y el valor nuevo del campo, junto con quien lo cambio y cuando.
2. Dado que se intenta dejar vacio el Nombre del control, la Categoria o el Tipo de control al editar, cuando se guarda, entonces el sistema rechaza el cambio por dato obligatorio faltante.
3. Dado un control en estado Archivado, cuando un usuario intenta editar sus campos, entonces el sistema deniega la edicion y solo permite reactivarlo primero.
4. Dado que el usuario vincula un Proveedor externo asociado desde el catalogo de proveedores, cuando guarda el cambio, entonces el control muestra el nombre del proveedor enlazado junto con el texto de advertencia "Requiere validacion de la organizacion." sobre la idoneidad de ese proveedor, sin que el sistema la evalue de forma automatica.
5. Dado un usuario con rol Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), Responsable Legal / Compliance, Responsable de area (RRHH, Marketing, Operaciones, etc.) o Usuario de consulta / Colaborador, cuando intenta editar un control, entonces el sistema deniega la accion.
6. Dado que se cambia la Categoria de un control ya creado, cuando se guarda, entonces el sistema exige elegir de nuevo un Tipo de control valido para la nueva categoria.

**Reglas de negocio**

- Solo Administrador de la organizacion y Responsable de Seguridad / IT pueden modificar un control (seccion C, fila Modificar control).
- Todo cambio de campo deja valor anterior y valor nuevo en el historial (seccion O).

**Fuera de alcance**

- Cambios de estado del control (crear excepcion, marcar Implementado, archivar), cubiertos en HU propias.

- Referencia: MOD-015 secciones D (campos editables y Proveedor externo asociado), C (permisos) y O (historial de cambios de campo)

### HU-015-03. Consultar y filtrar el catalogo de controles segun el rol

**Como** Responsable de Seguridad / IT, **quiero** ver el catalogo completo de controles con filtros por categoria, estado y responsable, respetando lo que cada rol puede ver, **para** encontrar rapidamente el estado de cualquier control y saber cuales necesitan atencion.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 24 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-015-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado que el Responsable de Seguridad / IT abre el catalogo, cuando aplica un filtro por categoria, estado o responsable, entonces el listado muestra solo los controles que cumplen ese filtro.
2. Dado un usuario con rol Responsable de area (RRHH, Marketing, Operaciones, etc.), cuando consulta el catalogo, entonces solo ve los controles cuyo Ambito de aplicacion incluye un sistema o tratamiento de su area, o Toda la organizacion.
3. Dado un Auditor externo (invitado) con acceso concedido durante una ventana de auditoria, cuando esa ventana vence y el usuario intenta volver a acceder, entonces el sistema le deniega el acceso.
4. Dado un Usuario de consulta / Colaborador o un Asesor externo invitado, cuando abre el modulo, entonces solo ve el control especifico que se le asigno o al que fue invitado, no el resto del catalogo.
5. Dado un usuario con rol Administrador de la organizacion, Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), Responsable Legal / Compliance o Auditor (interno), cuando abre el catalogo, entonces ve la lista completa de controles, en modo lectura o edicion segun el permiso de la seccion C.
6. Dado que no existe ningun control creado todavia en la organizacion, cuando se abre el catalogo, entonces se muestra un listado vacio indicando que no hay controles registrados.

**Reglas de negocio**

- La visibilidad del catalogo completo depende del rol, segun la tabla de la seccion C (fila Ver catalogo completo).
- El acceso del Auditor externo invitado es temporal y limitado a la ventana de auditoria habilitada.

**Fuera de alcance**

- Exportacion del catalogo a PDF, XLSX o paquete ZIP con verificacion de integridad (SHOULD HAVE, ver notas_epica).

- Referencia: MOD-015 secciones B (usuarios) y C (permisos, fila Ver catalogo completo)

### HU-015-04. Vincular un control al Sistema o Tratamiento que protege

**Como** Responsable de Seguridad / IT, **quiero** indicar a que Sistema o Tratamiento del RAT aplica un control, o marcarlo como aplicable a Toda la organizacion, **para** saber que controles protegen cada tratamiento y poder filtrar el catalogo por tratamiento o sistema.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 24 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-015-01
- Modulos requeridos: MOD-006

**Criterios de aceptacion**

1. Dado un control en cualquier estado, cuando el Responsable de Seguridad / IT selecciona uno o mas sistemas o tratamientos vigentes del RAT como Ambito de aplicacion y guarda, entonces el control queda vinculado a esos registros.
2. Dado que el control protege a toda la empresa por igual, cuando el usuario elige la opcion Toda la organizacion en Ambito de aplicacion, entonces el sistema acepta esa opcion en lugar de exigir un sistema o tratamiento especifico.
3. Dado un control sin ningun valor en Ambito de aplicacion, cuando el usuario intenta marcarlo como Implementado, entonces el sistema bloquea la transicion y exige completar primero el Ambito de aplicacion.
4. Dado que el usuario completa ademas el campo opcional Sistema o activo asociado con un sistema del catalogo del RAT, cuando guarda, entonces el control queda visible junto a ese sistema cuando se consulta el RAT.
5. Dado un tratamiento del RAT que queda archivado o dado de baja, cuando se consulta un control vinculado a el, entonces el sistema muestra el vinculo como historico sin borrar la referencia.
6. Dado que el usuario filtra el catalogo de controles por un tratamiento especifico del RAT, cuando aplica el filtro, entonces solo ve los controles cuyo Ambito de aplicacion incluye ese tratamiento o Toda la organizacion.

**Reglas de negocio**

- El Ambito de aplicacion es obligatorio antes de marcar un control como Implementado (seccion D).
- El catalogo de sistemas y tratamientos es propio de MOD-006; MOD-015 solo lo consume por referencia, nunca duplica esa lista (seccion L).

**Fuera de alcance**

- Deteccion automatica de que controles corresponden a un tratamiento nuevo; la vinculacion es siempre manual en esta epica.

- Referencia: MOD-015 secciones D (campos Ambito de aplicacion y Sistema o activo asociado) y F (condicion para pasar a Implementado)

### HU-015-05. Registrar pais y proveedor de una transferencia en un control SSL/TLS

**Como** Responsable de Seguridad / IT, **quiero** anotar en un campo de texto libre el pais y el proveedor de una transferencia cuando el tipo de control es Protocolo de comunicacion segura (SSL/TLS) para transferencias, **para** dejar constancia minima de OBL-SEG-04 mientras el modulo de Transferencias Internacionales no exista todavia.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R2 | 24 | No |

- Fundamento: OBL-SEG-04 (Art. 4 (bloque Medidas de Seguridad en Transferencias de Datos) y Art. 6 lit. d), Politicas de Actuacion ACE N. 001-0309025-DPDP)
- Depende de: HU-015-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un control de categoria Tecnica con Tipo de control igual a Protocolo de comunicacion segura (SSL/TLS) para transferencias, cuando el Responsable de Seguridad / IT abre el control, entonces el sistema muestra los campos de texto libre Pais de destino y Proveedor de la transferencia.
2. Dado un control de cualquier otro tipo, cuando se abre el control, entonces el sistema no muestra los campos Pais de destino ni Proveedor de la transferencia.
3. Dado que el usuario deja vacios Pais de destino y Proveedor de la transferencia, cuando guarda el control, entonces el sistema permite guardarlo igual porque ambos campos son opcionales.
4. Dado que se completan Pais de destino y Proveedor de la transferencia, cuando se guarda, entonces el sistema los conserva junto con el resto del control y los muestra en el detalle del control.
5. Dado que el modulo de Transferencias Internacionales todavia no existe como modulo estructurado, cuando se necesita registrar el pais y el proveedor de una transferencia, entonces estos dos campos de texto libre dentro del control son la unica forma de dejar esa constancia en el MVP.

**Reglas de negocio**

- Esta cobertura es generica y temporal mientras MOD-010 no exista como modulo completo (seccion L de la ficha).

**Fuera de alcance**

- Catalogo estructurado de paises con nivel de proteccion adecuado y registro formal de transferencias (MOD-010, fuera de esta epica).

- Referencia: MOD-015 seccion L (cobertura mientras MOD-010 no exista) y D (catalogo Tecnica, subcategoria SSL/TLS)
- Notas: Cubre la indicacion especifica del encargo: campo generico para transferencias mientras MOD-010 no exista.

### HU-015-06. Marcar un control como Implementado adjuntando evidencia

**Como** Responsable de Seguridad / IT, **quiero** adjuntar la evidencia que demuestra que un control ya existe y marcarlo como Implementado, **para** poder demostrar en cualquier momento que la medida de seguridad esta funcionando desde una fecha concreta.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 24 | No |

- Fundamento: OBL-SEG-01 (Art. 35 LPDP, Ley para la Proteccion de Datos Personales); OBL-SEG-02 (Art. 4 (Medidas Organizativas, lit. a-f), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-SEG-03 (Art. 4 (Medidas Tecnicas), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-SEG-04 (Art. 4 (bloque Medidas de Seguridad en Transferencias de Datos) y Art. 6 lit. d), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-SEG-05 (Art. 4, Medidas Fisicas lit. e), Politicas de Actuacion ACE); OBL-SEG-06 (Art. 56 lit. b num. 5 y 7, Ley para la Proteccion de Datos Personales); OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-015-01, HU-015-04
- Modulos requeridos: MOD-019, MOD-008

**Criterios de aceptacion**

1. Dado un control en Pendiente de implementar con Ambito de aplicacion ya definido, cuando el Responsable de Seguridad / IT adjunta al menos un archivo de evidencia o una referencia a un documento de Documentos y Politicas, indica la Fecha de implementacion y confirma, entonces el control pasa a Implementado, el sistema calcula la Proxima fecha de revision sumando la Periodicidad de revision a la Fecha de implementacion, y registra el evento en el historial.
2. Dado un control sin ningun archivo de evidencia ni referencia de documento adjunta, cuando el usuario intenta marcarlo como Implementado, entonces el sistema rechaza la transicion por falta de evidencia obligatoria.
3. Dado que el usuario indica una Fecha de implementacion posterior al dia de hoy, cuando intenta guardar, entonces el sistema rechaza el dato por ser una fecha futura.
4. Dado un control sin Ambito de aplicacion definido, cuando el usuario intenta marcarlo como Implementado, entonces el sistema bloquea la transicion y remite a completar primero el Ambito de aplicacion.
5. Dado que se adjunta un archivo de evidencia, cuando se sube, entonces el sistema calcula su hash y lo registra en el Centro de Evidencias junto con la fecha, version y usuario que lo subio, y muestra el texto de ayuda "Revise que este archivo no contenga datos personales innecesarios antes de subirlo."
6. Dado que un control pasa a Implementado, cuando el sistema confirma el cambio, entonces muestra el texto "Requiere validacion de la organizacion o asesoria especializada." aclarando que el registro de evidencia no certifica que el control sea tecnicamente suficiente o adecuado frente a un riesgo real.
7. Dado que se marca un control como Implementado, cuando el sistema procesa la accion, entonces unicamente registra la evidencia adjunta y no ejecuta, instala, cifra ni configura ningun control tecnico real en la infraestructura de la empresa.
8. Dado un usuario con rol Responsable de area, Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) o Responsable Legal / Compliance, cuando intenta marcar un control como Implementado, entonces el sistema deniega la accion por no tener el permiso requerido.

**Reglas de negocio**

- La Proxima fecha de revision se calcula sumando la Fecha de implementacion y la Periodicidad de revision (seccion D y automatizacion de la seccion G); si se edita manualmente despues, el sistema exige un motivo.
- Solo Administrador de la organizacion y Responsable de Seguridad / IT pueden ejecutar esta transicion (seccion C y F).

**Fuera de alcance**

- Creacion de tareas o alertas automaticas de proxima revision o de vencimiento (SHOULD HAVE, ver notas_epica).
- Transiciones posteriores En revision, Implementado con hallazgo y Vencido (fuera de esta epica, ver notas_epica).

- Referencia: MOD-015 secciones D (Evidencia de implementacion, Fecha de implementacion, Proxima fecha de revision), F (transicion Pendiente de implementar a Implementado), G (calculo de proxima revision y hash de evidencia) y H (primera y quinta decision que el sistema no automatiza)

### HU-015-07. Exigir un segundo aprobador para implementar un control critico

**Como** Administrador de la organizacion, **quiero** marcar ciertos controles como criticos para que su paso a Implementado quede bloqueado hasta que un Aprobador distinto lo confirme, **para** reforzar el control interno sobre las medidas de seguridad mas sensibles, como el cifrado de la base de datos principal.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 25 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-015-06
- Modulos requeridos: MOD-021

**Criterios de aceptacion**

1. Dado que el Administrador de la organizacion marca un control existente como critico, cuando guarda ese cambio, entonces el sistema recuerda esa marca para los siguientes intentos de pasar ese control a Implementado.
2. Dado un control marcado como critico en Pendiente de implementar con evidencia y Fecha de implementacion completas, cuando el Responsable de Seguridad / IT confirma el paso a Implementado, entonces el sistema no aplica el cambio todavia y crea una tarea de confirmacion para el rol Aprobador.
3. Dado que un usuario con rol Aprobador, distinto de quien registro la evidencia, confirma esa tarea, cuando la confirma, entonces el control pasa a Implementado y el sistema registra en el historial quien confirmo el paso y cuando.
4. Dado que el mismo usuario que registro la evidencia intenta confirmar tambien la aprobacion, cuando lo intenta, entonces el sistema deniega la confirmacion por tratarse de la misma persona.
5. Dado un control que no fue marcado como critico, cuando se marca como Implementado, entonces el sistema aplica el cambio de inmediato sin exigir una segunda confirmacion.
6. Dado un usuario distinto de Administrador de la organizacion, cuando intenta marcar un control como critico, entonces el sistema deniega la accion.

**Reglas de negocio**

- Marcar un control como critico y exigirle doble control es una configuracion de la empresa, sin exigencia legal directa (seccion C de la ficha).
- Que controles se marcan como criticos es configurable por la empresa (seccion G, automatizacion 8).

**Fuera de alcance**

- Definicion de una lista fija de controles criticos por parte del producto; la empresa decide cuales marcar.

- Referencia: MOD-015 secciones C (parrafo de doble control para controles criticos) y G (automatizacion 8)
- Notas: La marca de control critico y su doble control son opinion de producto, no exigencia legal (seccion C de la ficha).

### HU-015-08. Registrar una excepcion de control con justificacion

**Como** Responsable de Seguridad / IT, **quiero** marcar un control como No aplica - Exceptuado explicando por que no corresponde implementarlo en mi empresa, **para** dejar constancia de que la falta de implementacion fue una decision documentada y no un simple incumplimiento.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 25 | No |

- Fundamento: OBL-SEG-06 (Art. 56 lit. b num. 5 y 7, Ley para la Proteccion de Datos Personales)
- Depende de: HU-015-01
- Modulos requeridos: MOD-021

**Criterios de aceptacion**

1. Dado un control en Pendiente de implementar, cuando el Responsable de Seguridad / IT escribe una Justificacion de no implementacion de al menos 100 caracteres y confirma, entonces el control pasa a No aplica - Exceptuado y el sistema crea una tarea de aprobacion para el rol Aprobador.
2. Dado una Justificacion de no implementacion de menos de 100 caracteres, cuando el usuario intenta confirmar la excepcion, entonces el sistema rechaza el cambio por justificacion insuficiente.
3. Dado que se va a registrar la excepcion, cuando el sistema muestra el formulario, entonces incluye el texto "Recuerda que no implementar un control sin buena razon documentada es una infraccion grave (multa de 11 a 25 salarios minimos)."
4. Dado que se confirma una excepcion, cuando el sistema la registra, entonces deja constancia en el historial de quien la creo, cuando y con que justificacion, sin que la excepcion quede aprobada todavia.
5. Dado un usuario con rol Administrador de la organizacion, cuando registra una excepcion, entonces el sistema permite la accion igual que al Responsable de Seguridad / IT.
6. Dado un usuario con rol Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO), Responsable Legal / Compliance, Aprobador o Responsable de area, cuando intenta registrar una excepcion, entonces el sistema deniega la accion.

**Reglas de negocio**

- La Justificacion de no implementacion exige un minimo de 100 caracteres (seccion D).
- Solo Administrador de la organizacion y Responsable de Seguridad / IT pueden registrar una excepcion (seccion C, fila Aprobar excepcion se reserva para el segundo paso).

**Fuera de alcance**

- Aprobacion o rechazo de la excepcion (ver HU-015-09).

- Referencia: MOD-015 secciones D (Justificacion de no implementacion), F (transicion a No aplica - Exceptuado) y G (automatizacion de tarea de aprobacion)

### HU-015-09. Aprobar o rechazar una excepcion de control

**Como** Aprobador, **quiero** revisar la justificacion de una excepcion registrada y aprobarla o rechazarla, **para** que ninguna excepcion quede vigente sin la revision independiente de una segunda persona.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 25 | No |

- Fundamento: OBL-SEG-06 (Art. 56 lit. b num. 5 y 7, Ley para la Proteccion de Datos Personales)
- Depende de: HU-015-08
- Modulos requeridos: MOD-021

**Criterios de aceptacion**

1. Dado una excepcion pendiente de aprobacion, cuando un usuario con rol Aprobador, distinto de quien la creo, la aprueba, entonces la excepcion queda vigente, el sistema registra la identidad del Aprobador, la fecha y la justificacion en el historial, y el control entra al indicador de excepciones activas como aprobada.
2. Dado una excepcion pendiente, cuando el Aprobador la rechaza indicando un motivo, entonces el control vuelve a Pendiente de implementar y la tarea original se reabre mostrando el motivo del rechazo.
3. Dado que el Aprobador intenta rechazar sin escribir un motivo, cuando lo intenta, entonces el sistema rechaza la accion por motivo obligatorio faltante.
4. Dado que la organizacion esta por debajo del umbral configurable de tamano de pyme, cuando el mismo usuario que creo la excepcion la aprueba el mismo, entonces el sistema permite la aprobacion pero muestra una advertencia visible de autorrevision.
5. Dado que la organizacion esta por encima del umbral configurable de tamano, cuando el mismo usuario que creo la excepcion intenta aprobarla, entonces el sistema deniega la aprobacion por exigir un Aprobador distinto.
6. Dado que el Aprobador abre la pantalla de revision de una excepcion, cuando la abre, entonces el sistema muestra junto a la justificacion el texto "Requiere validacion de la organizacion o asesoria especializada.", sin calificar por si mismo si la justificacion es razonable.
7. Dado un usuario sin rol Aprobador, cuando intenta aprobar o rechazar una excepcion, entonces el sistema deniega la accion.

**Reglas de negocio**

- El Aprobador debe ser distinto de quien creo la excepcion, salvo pyme por debajo del umbral configurable, donde se permite la acumulacion mostrando siempre la advertencia de autorrevision (seccion C y 05_tipos_de_usuario.md seccion 5.4).
- Rechazar exige motivo; la tarea original se reabre con ese motivo visible (seccion F).

- Referencia: MOD-015 secciones C (separacion de funciones), F (transiciones Aprobar la excepcion / Rechazar la excepcion) y H (tercera decision que el sistema no automatiza)

### HU-015-10. Archivar y reactivar un control

**Como** Responsable de Seguridad / IT, **quiero** archivar un control que la empresa ya no usa y reactivarlo si vuelve a ser necesario, **para** sacar del catalogo activo lo que ya no aplica sin perder su historial.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 25 | No |

- Fundamento: Soporte o buena practica (sin OBL-ID)
- Depende de: HU-015-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un control en cualquier estado no terminal, cuando el Responsable de Seguridad / IT lo archiva indicando un motivo, entonces el control pasa a Archivado, deja de contar en los indicadores del dashboard, y el sistema registra el evento con el motivo en el historial.
2. Dado que el usuario intenta archivar un control sin escribir un motivo, cuando lo intenta, entonces el sistema rechaza la accion por motivo obligatorio faltante.
3. Dado un control Archivado, cuando el Administrador de la organizacion lo reactiva indicando un motivo, entonces el control vuelve a Pendiente de implementar y retoma su ciclo desde cero, con el evento de reapertura registrado en el historial.
4. Dado un control Archivado, cuando cualquier usuario busca una accion para eliminarlo de forma definitiva, entonces el sistema no ofrece ninguna opcion de borrado; archivar es la unica forma de retirarlo y su historial permanece intacto.
5. Dado un control archivado que fue citado como evidencia dentro de un expediente ya cerrado de otro modulo, cuando se consulta ese expediente, entonces el control archivado sigue visible como referencia historica y el archivado no elimina la evidencia ya citada.
6. Dado un usuario con rol distinto de Administrador de la organizacion o Responsable de Seguridad / IT, cuando intenta archivar o reactivar un control, entonces el sistema deniega la accion.

**Reglas de negocio**

- Archivado es el unico estado terminal y admite reapertura explicita con motivo; no existe borrado real de un control ni de su historial (seccion F y anti-feature 19 de 22_anti_features.md).

- Referencia: MOD-015 seccion F (transiciones Archivar y Reactivar)

### HU-015-11. Precargar el catalogo base de controles al completar el diagnostico

**Como** Responsable de Seguridad / IT, **quiero** que el sistema cree automaticamente el catalogo base de controles organizativos, tecnicos y fisicos la primera vez que la organizacion completa el diagnostico inicial, **para** partir de la lista completa de medidas que exige el Art. 4 de las Politicas ACE en vez de armar el catalogo desde cero.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 25 | No |

- Fundamento: OBL-SEG-01 (Art. 35 LPDP, Ley para la Proteccion de Datos Personales); OBL-SEG-02 (Art. 4 (Medidas Organizativas, lit. a-f), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-SEG-03 (Art. 4 (Medidas Tecnicas), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-SEG-04 (Art. 4 (bloque Medidas de Seguridad en Transferencias de Datos) y Art. 6 lit. d), Politicas de Actuacion ACE N. 001-0309025-DPDP); OBL-SEG-05 (Art. 4, Medidas Fisicas lit. e), Politicas de Actuacion ACE); OBL-SEG-06 (Art. 56 lit. b num. 5 y 7, Ley para la Proteccion de Datos Personales); OBL-SENS-05 (Art. 59, Ley para la Proteccion de Datos Personales)
- Depende de: HU-015-01
- Modulos requeridos: MOD-004, MOD-024

**Criterios de aceptacion**

1. Dado que una organizacion completa por primera vez el diagnostico inicial, cuando el diagnostico se guarda, entonces el sistema crea en Pendiente de implementar las seis medidas organizativas del catalogo base (Politica de Proteccion de Datos, Delegado de Proteccion de Datos designado, Capacitacion del personal, Registro de Actividades de Tratamiento, Evaluaciones de Impacto en la Privacidad, Auditorias de cumplimiento) mas los items tecnicos y fisicos mas comunes del catalogo de la seccion D, sin marcar ninguno como ya implementado.
2. Dado que un control del catalogo base corresponde a una de las obligaciones OBL-SEG-01 a 06 u OBL-SENS-05, cuando se crea, entonces el sistema lo marca internamente como control obligatorio del catalogo base, distinto de un control que la propia empresa agregue despues de forma manual.
3. Dado que la organizacion vuelve a completar el diagnostico una segunda vez, cuando lo guarda, entonces el sistema no crea un segundo catalogo base duplicado.
4. Dado que el estado normativo del Centro Regulatorio esta en ACTUAL, cuando se crea el catalogo base, entonces el item organizativo del Delegado se llama Delegado de Proteccion de Datos designado y se marca como obligatorio.
5. Dado que la empresa revisa el catalogo precargado y no necesita alguno de sus items (por ejemplo, no maneja dispositivos fisicos que destruir), cuando el Responsable de Seguridad / IT lo revisa, entonces puede archivarlo con motivo en lugar de dejarlo pendiente de forma indefinida.

**Reglas de negocio**

- El catalogo base es fijo y no configurable por la empresa; la empresa solo puede archivar despues los items que no le apliquen (seccion G, automatizacion 1).
- OBL-SENS-05 se cubre con el mismo item organizativo Politica de Proteccion de Datos, sin un tipo de control propio adicional (seccion A y D de la ficha).

**Fuera de alcance**

- Creacion de un control cuando una EIPD (MOD-014) selecciona uno inexistente en el catalogo (depende de MOD-014, SHOULD HAVE, fuera de esta epica).

- Referencia: MOD-015 secciones D (Campos precargados y catalogo detallado de Tipo de control) y G (automatizacion 1); nota sobre el doble estado de la reforma 659 en la seccion A
- Notas: Si el estado normativo pasara a FUTURO, ese mismo item organizativo cambiaria de nombre a Responsable interno del programa de datos designado y dejaria de marcarse obligatorio (nota de la seccion A de la ficha); ese cambio lo dispara el evento de cambio de bandera de MOD-024 y no es parte de esta HU, porque el MVP fija el estado en ACTUAL.

### HU-015-12. Mostrar el indicador de controles con evidencia vigente

**Como** Responsable de Seguridad / IT, **quiero** ver que porcentaje de los controles aplicables esta en estado Implementado, **para** saber de un vistazo cuanto del catalogo ya tiene evidencia vigente y cuanto sigue pendiente.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 5 | R2 | 25 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-015-06, HU-015-10
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado el conjunto de controles no archivados de la organizacion, cuando se calcula el indicador Controles con evidencia vigente, entonces el sistema muestra el numero de controles en Implementado dividido entre el total de controles no archivados, multiplicado por 100.
2. Dado que el indicador es 80% o mas, cuando se muestra, entonces aparece en semaforo verde; entre 50% y 79% aparece en amarillo; y por debajo de 50% aparece en rojo.
3. Dado un cambio de estado de cualquier control, cuando el cambio se guarda, entonces el indicador se recalcula de inmediato.
4. Dado un usuario con rol Administrador de la organizacion, cuando consulta el indicador, entonces solo ve el semaforo, sin el detalle de la lista de controles pendientes.
5. Dado un usuario con rol Responsable de Seguridad / IT, cuando consulta el indicador, entonces ve ademas el numero exacto y la lista de controles pendientes.
6. Dado un usuario con rol Responsable Legal / Compliance, cuando consulta el indicador, entonces lo ve con enfasis en los controles marcados como obligatorios del catalogo base.
7. Dado que se muestra este indicador en cualquier vista, cuando se muestra, entonces nunca aparece con la palabra cumplimiento ni como un porcentaje de cumplimiento legal, y siempre aparece junto al banner de descargo estandar del sistema.

**Reglas de negocio**

- Formula: controles en Implementado dividido entre total de controles no archivados, por 100 (seccion M).
- Umbrales de semaforo 80/50 por ciento son opinion de producto sin respaldo legal (seccion M).
- Ningun indicador de este modulo se expresa como porcentaje de cumplimiento legal (seccion M y anti-feature 5).

- Referencia: MOD-015 seccion M (tabla de indicadores, fila Controles con evidencia vigente)

### HU-015-13. Mostrar el indicador de controles obligatorios sin evidencia

**Como** Responsable Legal / Compliance, **quiero** ver cuantos controles del catalogo base obligatorio siguen sin evidencia, **para** dimensionar el riesgo de la infraccion grave del Art. 56 lit. b antes de que la ACE lo requiera.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 3 | R2 | 25 | No |

- Fundamento: OBL-SEG-06 (Art. 56 lit. b num. 5 y 7, Ley para la Proteccion de Datos Personales)
- Depende de: HU-015-11
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado el conjunto de controles marcados como obligatorios del catalogo base (OBL-SEG-01 a 06), cuando se calcula el indicador, entonces el sistema cuenta cuantos de ellos siguen en estado Pendiente de implementar.
2. Dado que el numero de controles obligatorios sin evidencia es mayor a 0, cuando se muestra el indicador, entonces aparece en rojo.
3. Dado que el numero de controles obligatorios sin evidencia es 0, cuando se muestra el indicador, entonces aparece sin la bandera de riesgo.
4. Dado un usuario con rol Responsable Legal / Compliance o Administrador de la organizacion, cuando consulta el indicador, entonces lo ve vinculado de forma explicita al riesgo de infraccion grave del Art. 56 lit. b.
5. Dado un usuario con rol Responsable de Seguridad / IT, cuando consulta el indicador, entonces ademas ve la lista detallada de esos controles pendientes.
6. Dado que un control obligatorio del catalogo base pasa de Pendiente de implementar a Implementado, o se le aprueba una excepcion, cuando el cambio se guarda, entonces el indicador se recalcula y ese control deja de contarse.

**Reglas de negocio**

- El indicador cuenta solo controles del catalogo base marcados obligatorios (OBL-SEG-01 a 06) en Pendiente de implementar (seccion E y M).

**Fuera de alcance**

- Conteo de controles en estado Vencido dentro de este indicador (excluido en esta epica, ver notas_epica).

- Referencia: MOD-015 secciones E (Bandera de riesgo sancionador) y M (indicador Controles obligatorios sin evidencia o vencidos, limitado en esta epica a sin evidencia)
- Notas: Limitado a sin evidencia (Pendiente de implementar); la parte o vencidos de la ficha depende del estado Vencido, fuera de esta epica (ver notas_epica).

### HU-015-14. Consultar el historial de cambios de un control

**Como** Auditor (interno), **quiero** ver la linea de tiempo de un control especifico con quien cambio que y cuando, **para** verificar de forma independiente la trazabilidad de las medidas de seguridad durante una auditoria.

| Puntos | Release | Sprint | Habilitadora |
|---|---|---|---|
| 2 | R2 | 24 | No |

- Fundamento: OBL-PRIN-03 (Art. 5 lit. i), Ley para la Proteccion de Datos Personales)
- Depende de: HU-015-01
- Modulos requeridos: -

**Criterios de aceptacion**

1. Dado un control con varios cambios de estado y de campos a lo largo del tiempo, cuando el Auditor (interno) abre su historial, entonces ve cada evento en orden cronologico con quien lo hizo, cuando, y el valor anterior y el valor nuevo cuando el evento es un cambio de campo.
2. Dado un control con una excepcion aprobada, cuando se consulta su historial, entonces se ve por separado quien creo la excepcion y quien la aprobo o rechazo, con fecha y justificacion.
3. Dado un archivo de evidencia adjuntado o reemplazado, cuando se consulta el historial, entonces se ve el hash, la version y el usuario que lo subio.
4. Dado un control archivado y luego reactivado, cuando se consulta su historial, entonces ambos eventos aparecen con el motivo indicado por el usuario en cada caso.
5. Dado un usuario con rol Auditor externo (invitado), cuando consulta el historial de un control compartido con el durante su ventana de auditoria, entonces lo ve en modo lectura igual que el Auditor (interno).
6. Dado un usuario sin ningun permiso de lectura sobre el catalogo, cuando intenta abrir el historial de un control, entonces el sistema deniega el acceso.

**Reglas de negocio**

- El historial es de solo lectura para Auditor (interno) y Auditor externo (invitado); ninguno de los dos puede crear ni aprobar nada (seccion B y C).

**Fuera de alcance**

- Exportacion del historial a CSV como reporte formal (SHOULD HAVE, ver notas_epica).

- Referencia: MOD-015 secciones O (historial) y N (fila Historial de cambios de un control)

## Cobertura de la tabla MVP de la ficha

| Funcionalidad MUST HAVE | HU |
|---|---|
| Catalogo base de controles (organizativos, tecnicos, fisicos) con estado y evidencia adjunta | HU-015-01, HU-015-02, HU-015-03, HU-015-05, HU-015-06, HU-015-07, HU-015-10, HU-015-11, HU-015-14 |
| Registro de excepciones con justificacion y aprobacion de un segundo usuario | HU-015-08, HU-015-09 |
| Vinculacion con Sistema/Tratamiento del RAT (MOD-006) | HU-015-04 |
| Indicadores de dashboard (evidencia vigente, controles obligatorios sin evidencia) | HU-015-12, HU-015-13 |
