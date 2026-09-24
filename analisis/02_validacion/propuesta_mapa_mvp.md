# Propuesta de mapa de modulos - Angulo MVP-PRIMERO

Fecha: 2026-09-24. Fase: analisis funcional (prohibido codigo, SQL, APIs, stack o infraestructura).

Pregunta rectora de este documento: cual es el producto minimo que ya puede venderse a una pyme
salvadorena en 2026, y como se organizan las capas siguientes (V1, V2/Enterprise) para que nunca obliguen
a rediseñar el MVP.

Fuentes usadas: `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md` (documento maestro, hipotesis),
`01_legal/matriz_obligaciones.md` (105 obligaciones, IDs canonicos OBL-AREA-NN),
`02_validacion/02_validacion_de_la_idea.md` (26 inconsistencias, 31 funciones faltantes, 32 decisiones de
alcance en su seccion 2.7). Toda decision de alcance de este documento que no cite un OBL-ID es opinion de
producto y se marca como tal.

Criterio de disciplina de MVP: un modulo entra al MVP solo si cumple al menos una de estas tres
condiciones: (a) cubre una obligacion OBLIGATORIO cuyo plazo transitorio ya vencio (OBL-PLAZO-03,
OBL-PLAZO-04), (b) es una dependencia estructural sin la cual otro modulo MUST HAVE no puede operar
(ejemplo: Centro de tareas, motor de plazos), o (c) es la unica forma de que el producto sea "probatorio"
desde el primer dia (Centro de evidencias, AuditLog). Todo lo demas se defiere a V1 o V2/Enterprise aunque
tenga respaldo legal OBLIGATORIO, si su ausencia en el MVP puede cubrirse con un campo o una tarea manual
dentro de un modulo MUST HAVE mientras llega su version completa. Esos casos de cobertura parcial se
marcan explicitamente en la ficha del modulo diferido.

---

## 1. Arbol de modulos

```
PLATAFORMA PRIV-SV
|
+-- CAPA 0: NUCLEO Y GOBIERNO (fundacional)
|   |
|   +-- MOD-001 Organizacion y estructura .............. MUST HAVE
|   +-- MOD-002 Usuarios, roles y permisos .............. MUST HAVE
|   +-- MOD-003 Delegado de Proteccion de Datos ......... MUST HAVE
|   +-- MOD-004 Catalogo de sistemas .................... MUST HAVE
|
+-- CAPA 1: ENTRADA (onboarding y diagnostico)
|   |
|   +-- MOD-005 Onboarding ............................... MUST HAVE
|   +-- MOD-006 Diagnostico de cumplimiento ............. MUST HAVE
|   +-- MOD-007 Plan de cumplimiento ..................... MUST HAVE
|
+-- CAPA 2: MOTORES OPERATIVOS
|   |
|   +-- MOD-008 RAT (incluye inventario y mapa de datos) . MUST HAVE
|   +-- MOD-009 ARCO-POL .................................. MUST HAVE
|   +-- MOD-010 Documentos y politicas .................... MUST HAVE
|   +-- MOD-011 Proveedores y encargados .................. MUST HAVE
|   +-- MOD-012 Incidentes de seguridad ................... MUST HAVE
|   +-- MOD-013 Controles de seguridad ..................... MUST HAVE
|   +-- MOD-014 Capacitacion (registro minimo) ............. MUST HAVE
|   |
|   +-- MOD-015 Consentimiento ............................. SHOULD HAVE (V1)
|   +-- MOD-016 Transferencias internacionales ............. SHOULD HAVE (V1)
|   +-- MOD-017 Retencion y eliminacion (motor de datos) ... SHOULD HAVE (V1)
|   +-- MOD-018 Riesgos / EIPD .............................. SHOULD HAVE (V1)
|   +-- MOD-019 Auditoria de cumplimiento (programa anual) . SHOULD HAVE (V1)
|   +-- MOD-020 Procedimiento sancionador / requerimientos ACE SHOULD HAVE (V1)
|
+-- CAPA 3: RELACION CON EL TITULAR
|   |
|   +-- MOD-021 Portal del titular ......................... SHOULD HAVE (V1)
|
+-- CAPA 4: SERVICIOS TRANSVERSALES (consumidos por toda capa anterior)
|   |
|   +-- MOD-022 Centro de tareas ........................... MUST HAVE
|   +-- MOD-023 Centro de evidencias ....................... MUST HAVE
|   +-- MOD-024 Registro de auditoria (AuditLog) ........... MUST HAVE
|   +-- MOD-025 Notificaciones .............................. MUST HAVE (canal unico)
|   +-- MOD-026 Calendario y motor de plazos habiles ....... MUST HAVE
|   +-- MOD-027 Centro regulatorio (incl. actualiz. normativas) MUST HAVE (version minima)
|   +-- MOD-028 Centro de ayuda contextual .................. MUST HAVE
|
+-- CAPA 5: VISUALIZACION Y SALIDA
    |
    +-- MOD-029 Dashboard ................................... MUST HAVE (version minima)
    +-- MOD-030 Reportes ..................................... SHOULD HAVE (V1)
    +-- MOD-031 Busqueda global .............................. COULD HAVE (V1/V2)
```

Flujo funcional principal (capas 0 a 3), simplificado:

```
Organizacion/Usuarios/Delegado (0)
        |
        v
   Onboarding -> Diagnostico -> Plan de cumplimiento (1)
        |                              |
        v                              v
  RAT <-> Documentos <-> Proveedores <-> Controles <-> Capacitacion   (2, MVP)
   |          |               |              |
   v          v               v              v
  ARCO-POL   Incidentes   (V1: Consentimiento, Transferencias, Retencion,
   |          |            Riesgos/EIPD, Auditoria de cumplimiento,
   |          |            Procedimiento sancionador)
   v          v
  Portal del titular (V1, capa 3)
```

Toda casilla de las capas 0 a 3 lee y escribe contra los servicios transversales de la capa 4
(Tareas, Evidencias, AuditLog, Notificaciones, Calendario, Regulatorio, Ayuda) y es leida por la capa 5
(Dashboard, Reportes, Busqueda). La capa 4 no depende de ninguna casilla de las capas 0 a 3: por eso es
transversal y por eso ninguna de sus piezas puede quedar fuera del MVP sin dejar sin funcion util a los
modulos operativos que si estan en el MVP (ver seccion 3).

---

## 2. Ficha resumida de cada modulo

Formato por modulo: codigo, nombre, proposito (3 lineas), obligaciones que cubre (propietario; los OBL-ID
marcados "(colab)" en la tabla de cobertura de la seccion 5 no se repiten aqui salvo que aclaren el
alcance), areas del prompt que absorbe, decision respecto al documento maestro, clasificacion MVP con
justificacion, dependencias (entra/sale).

### CAPA 0: NUCLEO Y GOBIERNO

#### MOD-001 - Organizacion y estructura

- Proposito: registra la empresa cliente (razon social, giro, sedes, unidades) como sujeto obligado de la
  LPDP. Sostiene la estructura sobre la que se asignan responsables y tareas en todos los demas modulos.
  No decide nada juridico por si solo; es el directorio base de la plataforma.
- Obligaciones que cubre (propietario): OBL-AMB-01 (colaborador de MOD-006, que hace la pregunta de
  aplicabilidad, pero el dato "esta la empresa dentro del ambito" vive aqui).
- Areas del prompt que absorbe: 8.1 Configuracion de empresa.
- Decision respecto al documento maestro: se mantiene la Sec. 11 (Modulo de organizacion), pero se retira
  de aqui el rol "Delegado de Proteccion de Datos" (pasa a MOD-003) y "contacto ARCO-POL" (se deriva del
  rol activo en MOD-002, no se captura como campo libre); ver inconsistencia 8 de la validacion.
- Clasificacion MVP: MUST HAVE. Justificacion: sin datos de la organizacion (razon social, sedes, giro) no
  puede operar ningun otro modulo; es el registro fundacional de toda cuenta.
- Dependencias: Entra de: nada (es el punto de partida). Sale a: MOD-002, MOD-003, MOD-005, MOD-006, y por
  referencia a todos los modulos que necesitan "sede" o "area responsable".

#### MOD-002 - Usuarios, roles y permisos

- Proposito: administra quien puede entrar a la plataforma, con que rol y que puede hacer. Permite que una
  persona tenga varios roles en empresas pequenas y separacion de funciones en empresas medianas. El rol
  activo "Responsable ARCO-POL" es la fuente del contacto ARCO-POL publicado, no un campo aparte.
- Obligaciones que cubre (propietario): ninguna obligacion de la matriz tiene a este modulo como
  propietario directo (es infraestructura de acceso); es colaborador de practicamente toda obligacion que
  exige "responsable" o "aprobacion" (OBL-PRIN-03, OBL-DPO-08, entre otras).
- Areas del prompt que absorbe: 8.2 Usuarios, roles y permisos.
- Decision respecto al documento maestro: se mantiene la Sec. 12, con el catalogo de roles ajustado para
  incluir "Delegado de Proteccion de Datos" como rol propio (antes ausente, ver seccion 2.4 de la
  validacion) y para fusionar "Responsable de privacidad" dentro de ese rol o eliminarlo si resulta
  redundante (inconsistencia 7).
- Clasificacion MVP: MUST HAVE. Justificacion: sin roles no hay asignacion de tareas ni aprobaciones; es
  dependencia estructural de todo el resto del MVP.
- Dependencias: Entra de: MOD-001 (estructura sobre la que se definen permisos por area). Sale a: todos los
  modulos operativos (asignacion de responsables), MOD-022 Centro de tareas.

#### MOD-003 - Delegado de Proteccion de Datos

- Proposito: gestiona el ciclo de vida completo de la figura legal que hoy exige el Art. 15 y 17 LPDP
  (nombramiento, comunicacion a la ACE, reverificacion, informes, confidencialidad post-cese), y modela el
  doble estado frente a la reforma 659 sin duplicar el modulo (ver seccion 4 de este documento). Es el
  hallazgo estructural mas importante de la validacion: el maestro no lo contemplaba como rol propio.
- Obligaciones que cubre (propietario): OBL-DPO-01, OBL-DPO-02, OBL-DPO-03, OBL-DPO-04, OBL-DPO-05,
  OBL-DPO-06, OBL-DPO-07, OBL-DPO-08.
- Areas del prompt que absorbe: ninguna de las 29 esta dedicada a esta figura en el prompt (es un hallazgo
  de la validacion); absorbe partes de 8.1 (dato "responsable de privacidad" que el maestro traia mal
  ubicado).
- Decision respecto al documento maestro: es nuevo. El maestro (Sec. 11 y 12) no incluye esta figura como
  modulo ni como rol; se crea a partir de la decision 2.7.7 y 2.7.25 de la validacion.
- Clasificacion MVP: MUST HAVE. Justificacion: mientras el Decreto 659 no se publique, el delegado es
  obligatorio hoy (OBL-DPO-01, Arts. 15 y 17); es la obligacion mas urgente que el maestro dejaba sin
  cubrir; el plazo de comunicacion a la ACE (15 dias habiles, OBL-DPO-03) exige que exista desde el primer
  dia de uso del producto.
- Dependencias: Entra de: MOD-001, MOD-002 (persona designada), MOD-027 (estado vigente de la reforma 659).
  Sale a: MOD-022 (tareas de reverificacion e informes periodicos), MOD-009 (actos que la ley atribuye al
  delegado), MOD-014 (capacitacion anual del delegado), MOD-023 (evidencia de nombramiento y comunicacion).

#### MOD-004 - Catalogo de sistemas

- Proposito: registra, una sola vez, cada sistema o aplicacion que la empresa usa para tratar datos
  personales (nombre, tipo, proveedor si es externo, pais de alojamiento). Evita que RAT, Proveedores e
  Incidentes describan el mismo sistema con texto libre distinto cada vez.
- Obligaciones que cubre (propietario): ninguna directamente; es catalogo de soporte. Colaborador de
  OBL-DOC-02 (RAT) y de las obligaciones de Proveedores/Transferencias que dependen de saber donde vive
  cada sistema.
- Areas del prompt que absorbe: ninguna area del prompt lo nombra como modulo separado; absorbe el concepto
  "sistemas" repetido en las secciones 13, 14, 22 y 25 del maestro.
- Decision respecto al documento maestro: es nuevo. Se crea por la decision 2.7.19 de la validacion
  (inconsistencia 19: "Catalogo de sistemas sin modulo propietario").
- Clasificacion MVP: MUST HAVE. Justificacion: es una dependencia estructural barata (un catalogo simple)
  sin la cual el RAT (MUST HAVE) fuerza texto libre y pierde trazabilidad desde el primer registro.
- Dependencias: Entra de: MOD-001. Sale a: MOD-008 (RAT referencia sistemas), MOD-011 (Proveedores
  referencia sistemas), MOD-012 (Incidentes referencia el sistema afectado).

### CAPA 1: ENTRADA (onboarding y diagnostico)

#### MOD-005 - Onboarding

- Proposito: da de alta la cuenta de la empresa, sus primeros usuarios y su estructura minima, y explica en
  lenguaje sencillo que va a pasar en el diagnostico. Es un flujo de configuracion, no un cuestionario de
  cumplimiento (esa es la diferencia con MOD-006, inconsistencia 5).
- Obligaciones que cubre (propietario): ninguna directamente; habilita el cumplimiento de las demas.
- Areas del prompt que absorbe: 8.3 Onboarding desde cero.
- Decision respecto al documento maestro: se divide la Sec. 15 ("Onboarding / Compliance Wizard") del
  maestro en dos modulos: MOD-005 Onboarding (alta) y MOD-006 Diagnostico (cuestionario), por la decision
  2.7.5 de la validacion.
- Clasificacion MVP: MUST HAVE. Justificacion: es el primer flujo que ve todo cliente nuevo; sin el no hay
  forma de crear la cuenta ni de llegar al diagnostico.
- Dependencias: Entra de: MOD-001, MOD-002. Sale a: MOD-006.

#### MOD-006 - Diagnostico de cumplimiento

- Proposito: cuestionario guiado (empleados, camaras, biometria, CRM, cloud, datos fuera del pais, etc.)
  donde cada respuesta activa tratamientos candidatos en el RAT, tareas, documentos y senales de riesgo.
  Es repetible: se vuelve a ejecutar cuando la empresa cambia de actividad (por ejemplo, empieza a usar
  biometria).
- Obligaciones que cubre (propietario): OBL-AMB-01, OBL-AMB-02, OBL-AMB-03, OBL-AMB-04, OBL-PLAZO-03.
- Areas del prompt que absorbe: 9 Diagnostico inicial.
- Decision respecto al documento maestro: se mantiene el contenido de la Sec. 15 del maestro como base de
  preguntas, separado de Onboarding (decision 2.7.5), y se le agregan las preguntas de exclusion del Art. 3
  (decision 2.7.27) que el maestro no contemplaba.
- Clasificacion MVP: MUST HAVE. Justificacion: es el nucleo de la propuesta de valor ("traducir la ley en
  tareas") y el unico lugar que activa OBL-PLAZO-03 (adecuacion a las Politicas ACE, plazo ya vencido el
  2/3-dic-2025), la obligacion que mas urgencia comercial valida.
- Dependencias: Entra de: MOD-005. Sale a: MOD-007 (genera el plan), MOD-008 (crea tratamientos
  candidatos), MOD-022 (crea tareas iniciales), y marca senales hacia MOD-015/MOD-016/MOD-018 (V1) aunque
  esos modulos no esten activos en el MVP (ver notas de cobertura parcial en sus fichas).

#### MOD-007 - Plan de cumplimiento

- Proposito: convierte el resultado del diagnostico en una lista priorizada de acciones (criticas,
  importantes, recomendadas), cada una con responsable, fecha, fundamento legal y evidencia esperada. Es el
  "mapa de ruta" que el usuario no especialista sigue paso a paso.
- Obligaciones que cubre (propietario): ninguna obligacion propia; es la vista priorizada de las
  obligaciones que ya detecto MOD-006. Colaborador de OBL-PLAZO-03 (referencia el plazo vencido).
- Areas del prompt que absorbe: 10 Plan de cumplimiento generado tras el diagnostico.
- Decision respecto al documento maestro: es nuevo como modulo propio (el maestro no lo distingue del
  onboarding); se separa por ser el entregable concreto que hace vendible al MVP (valor comercial
  inmediato: "aqui esta su lista de que hacer primero").
- Clasificacion MVP: MUST HAVE. Justificacion: es el resultado tangible que el usuario ve tras el
  diagnostico; sin esto, el diagnostico es solo un cuestionario sin salida util, y el producto pierde el
  argumento de venta principal ("le decimos que hacer primero").
- Dependencias: Entra de: MOD-006. Sale a: MOD-022 (cada accion del plan crea una tarea), MOD-029
  (indicador de avance del plan en el dashboard).

### CAPA 2: MOTORES OPERATIVOS (MVP)

#### MOD-008 - RAT (incluye inventario y mapa de datos)

- Proposito: fuente unica de verdad de cada actividad de tratamiento (finalidad, base juridica, categorias
  de datos y titulares, sistemas, encargados, retencion, riesgos). El Mapa de datos (origen -> sistema ->
  area -> proveedor -> pais -> eliminacion) es una vista sobre estos mismos registros, no una base aparte.
- Obligaciones que cubre (propietario): OBL-PRIN-01, OBL-PRIN-02, OBL-SENS-01, OBL-SENS-04, OBL-SENS-05,
  OBL-SENS-06, OBL-SENS-08, OBL-TRAT-01, OBL-TRAT-02, OBL-TRAT-03, OBL-DOC-02.
- Areas del prompt que absorbe: 11 RAT, 12 Mapa de datos.
- Decision respecto al documento maestro: se fusiona Inventario de datos (Sec. 13) dentro del RAT (Sec. 14)
  como una sola entidad "Tratamiento"; Mapa de datos deja de ser modulo independiente y pasa a ser una
  vista del RAT (decision 2.7.1, inconsistencia 1).
- Clasificacion MVP: MUST HAVE. Justificacion: es el modulo con mas obligaciones OBLIGATORIO asociadas de
  toda la matriz (11 de las 105) y la base de datos de la que dependen ARCO-POL, Incidentes, Proveedores y
  Documentos; sin RAT el resto del MVP no tiene sobre que operar.
- Dependencias: Entra de: MOD-004 (sistemas), MOD-006 (tratamientos candidatos del diagnostico). Sale a:
  MOD-009, MOD-010, MOD-011, MOD-012, MOD-022, MOD-023, y (V1) MOD-015, MOD-016, MOD-017, MOD-018 cuando se
  activen.

#### MOD-009 - ARCO-POL

- Proposito: gestiona cada solicitud de un titular (acceso, rectificacion, cancelacion, oposicion,
  portabilidad, limitacion) desde su recepcion hasta el cierre, con los plazos legales, la prevencion
  unica, la denegatoria motivada y las tres ramas que el maestro no contemplaba (incompetencia, notificacion
  a receptores, reclamo ante la ACE).
- Obligaciones que cubre (propietario): OBL-ARCO-01 a OBL-ARCO-15 (15 obligaciones), OBL-DOC-01, OBL-DOC-04,
  OBL-PLAZO-04, OBL-SANC-09.
- Areas del prompt que absorbe: 13 ARCO-POL.
- Decision respecto al documento maestro: se mantiene la Sec. 17 del maestro, ampliada con las tres ramas
  faltantes (decision 2.7.10) y con el subproceso de verificacion de identidad del titular (decision
  2.7.18); el "portal publico" que el maestro asumia como unica via de entrada se reemplaza en el MVP por
  un formulario interno seguro (decision 2.7.30).
- Clasificacion MVP: MUST HAVE. Justificacion: es el area con mas obligaciones de toda la matriz (20 en el
  conteo de la matriz) y cubre OBL-PLAZO-04, la segunda obligacion OBLIGATORIO con plazo transitorio ya
  vencido (23-may-2025); es, junto con OBL-PLAZO-03, la razon de urgencia comercial principal del MVP.
- Dependencias: Entra de: MOD-001, MOD-002, MOD-008 (para saber que tratamientos existen), MOD-026 (calculo
  de plazos), MOD-003 (aprobacion del delegado sobre actos que la ley le atribuye). Sale a: MOD-022,
  MOD-023, MOD-025, y (V1) MOD-021 Portal del titular como canal adicional de entrada.

#### MOD-010 - Documentos y politicas

- Proposito: gestor documental regulatorio: Aviso de Privacidad, Politica de Proteccion de Datos,
  procedimientos internos, con plantillas, borradores, aprobacion configurable por tipo de documento,
  publicacion, versionado y conservacion. Todo documento generado automaticamente se marca como borrador
  sujeto a validacion de la organizacion.
- Obligaciones que cubre (propietario): OBL-AVISO-01, OBL-AVISO-02, OBL-AVISO-03, OBL-AVISO-04,
  OBL-AVISO-05, OBL-RET-04, OBL-RET-06.
- Areas del prompt que absorbe: 15 Documentos y politicas.
- Decision respecto al documento maestro: se mantiene la Sec. 20, ajustando la aprobacion a un flujo
  configurable por tipo de documento en vez de un unico rol "Aprobador" uniforme (decision 2.7.14,
  inconsistencia 16); Contratos/DPA (Sec. 23 del maestro) se modela aqui como un tipo de documento dentro de
  MOD-011, no como modulo aparte (decision 2.7.2, inconsistencia 2).
- Clasificacion MVP: MUST HAVE. Justificacion: el Aviso de Privacidad y la Politica de Proteccion de Datos
  son OBLIGATORIO desde el primer dia (Art. 24 y Politicas ACE) y son, junto con el RAT, el primer
  entregable "probatorio" que una pyme puede mostrar a la ACE o a un cliente que lo pida.
- Dependencias: Entra de: MOD-008 (datos del tratamiento para redactar el aviso), MOD-003 (informes del
  delegado que se conservan aqui). Sale a: MOD-015 (V1, referencia la version del aviso mostrada al
  titular), MOD-022, MOD-023.

#### MOD-011 - Proveedores y encargados

- Proposito: registro de todo tercero que trata datos por cuenta de la empresa (encargados) o que recibe
  datos con fines propios (terceros/receptores), con su contrato o DPA, medidas de seguridad y pais. Aplica
  las obligaciones que la ley impone directamente al encargado y las que exige documentar sobre el.
- Obligaciones que cubre (propietario): OBL-PROV-01, OBL-PROV-02, OBL-PROV-03, OBL-PROV-04, OBL-PROV-05,
  OBL-PROV-06, OBL-PROV-07, OBL-AVISO-02 (colab), OBL-AVISO-04 (colab).
- Areas del prompt que absorbe: 17 Proveedores.
- Decision respecto al documento maestro: se fusionan las Sec. 22 (Proveedores y terceros) y 23
  (Contratos/DPA) del maestro en un solo modulo, con Contratos/DPA como tipo de documento interno (decision
  2.7.2); se definen tres tipos de entidad distintos (Encargado, Tercero/Receptor, Subencargado) en vez de
  un unico tipo "proveedor" (decision 2.7.8, inconsistencia 9).
- Clasificacion MVP: MUST HAVE. Justificacion: practicamente toda pyme salvadorena usa al menos un
  proveedor externo (nomina, contabilidad, hosting, correo); las obligaciones del encargado (Art. 33, 34,
  36) son OBLIGATORIO y no requieren esperar a que exista el motor completo de Transferencias para
  registrarse.
- Dependencias: Entra de: MOD-004 (sistemas), MOD-008 (tratamientos que usan el proveedor). Sale a:
  MOD-010 (contrato como documento), MOD-012 (proveedor como origen de un incidente), MOD-022, MOD-023, y
  (V1) MOD-016 Transferencias cuando el proveedor esta fuera de El Salvador (ver nota de cobertura parcial
  en la ficha de MOD-016).

#### MOD-012 - Incidentes de seguridad

- Proposito: gestiona toda vulneracion de seguridad desde su deteccion hasta el cierre, con dos cronometros
  de 72 horas separados y visibles (notificacion externa a ACE/Fiscalia/titulares, e inicio de la revision
  interna), checklist de contencion y remediacion, y generador de dos plantillas de notificacion distintas
  (autoridad vs. titular) a partir del mismo expediente.
- Obligaciones que cubre (propietario): OBL-INC-01, OBL-INC-02, OBL-INC-03, OBL-INC-04, OBL-INC-05.
- Areas del prompt que absorbe: 19 Incidentes.
- Decision respecto al documento maestro: se mantiene la Sec. 25, corrigiendo la falta de separacion entre
  los dos hitos de 72 horas (decision 2.7.11, inconsistencia 13); se adopta por defecto el criterio
  conservador de horas corridas para el computo, con nota de incertidumbre siempre visible (ver
  incertidumbres genuinas en `02_validacion_de_la_idea.md`, seccion 2.3.3).
- Clasificacion MVP: MUST HAVE. Justificacion: el plazo de 72 horas (Art. 25) es de los mas severos de toda
  la ley en terminos reputacionales y de multa potencial; ninguna pyme puede darse el lujo de gestionar esto
  en un correo o una hoja de calculo, y es funcionalmente barato de construir (un formulario con cronometro
  y checklist) frente a su alto valor de venta.
- Dependencias: Entra de: MOD-004 (sistema afectado), MOD-011 (proveedor afectado, si aplica), MOD-026
  (calculo del plazo de 72 horas). Sale a: MOD-022, MOD-023, MOD-025 (alertas de escalamiento), y (V1)
  MOD-020 Procedimiento sancionador si el incidente deriva en un requerimiento de la ACE.

#### MOD-013 - Controles de seguridad

- Proposito: catalogo de medidas tecnicas, organizativas y fisicas (MFA, cifrado, backups, control de
  acceso, eliminacion segura) con su responsable, evidencia y fecha de revision. El sistema no ejecuta
  controles ni sustituye un SIEM o antivirus: solo registra que existen y su evidencia.
- Obligaciones que cubre (propietario): OBL-SEG-02, OBL-SEG-03, OBL-SEG-05.
- Areas del prompt que absorbe: 21 Controles de seguridad.
- Decision respecto al documento maestro: se mantiene la Sec. 27, reforzando el limite explicito (registrar
  evidencia, no ejecutar controles) que ya traia el maestro; se comparte la entidad "Control" con MOD-018
  Riesgos/EIPD (V1) para que la EIPD nunca mantenga una lista de controles paralela (decision 2.7.3,
  inconsistencia 3).
- Clasificacion MVP: MUST HAVE. Justificacion: las medidas tecnicas y organizativas de las Politicas ACE son
  OBLIGATORIO y de aplicacion inmediata (no dependen de que exista un tratamiento de alto riesgo); construir
  el modulo es barato porque es un catalogo con evidencia adjunta, no una herramienta de seguridad real.
- Dependencias: Entra de: MOD-004 (sistema al que aplica el control). Sale a: MOD-022, MOD-023, y (V1)
  MOD-018 Riesgos/EIPD (selecciona controles de este catalogo).

#### MOD-014 - Capacitacion (registro minimo)

- Proposito: en el MVP, registra unicamente que el personal recibio capacitacion en proteccion de datos
  (fecha, participantes, tema, evidencia adjunta). No incluye en el MVP cursos interactivos, microlearning
  ni certificados: esas funciones se difieren a V1 como diferenciadores, no como obligacion minima.
- Obligaciones que cubre (propietario): OBL-CAP-01.
- Areas del prompt que absorbe: 23 Capacitacion.
- Decision respecto al documento maestro: se mantiene la Sec. 28, pero se separa explicitamente el registro
  minimo obligatorio (MVP) de las funcionalidades opcionales (decision 2.7.23, inconsistencia 25); el
  maestro trataba toda la capacitacion como "a evaluar" cuando OBL-CAP-01 es una obligacion legal minima sin
  condicion.
- Clasificacion MVP: MUST HAVE (version minima). Justificacion: OBL-CAP-01 es OBLIGATORIO y sin condicion
  (a diferencia de OBL-DPO-05 y OBL-CAP-02, que son CONDICIONAL); el registro minimo es barato de construir
  (un formulario y un archivo adjunto) frente al riesgo legal de omitirlo.
- Dependencias: Entra de: MOD-002 (lista de personal). Sale a: MOD-022, MOD-023, MOD-003 (colaborador de
  OBL-DPO-05, capacitacion especifica del delegado).

### CAPA 2: MOTORES OPERATIVOS (V1)

#### MOD-015 - Consentimiento

- Proposito: gestiona el consentimiento como base juridica cuando el RAT la selecciona: registro del
  titular, finalidad, version del aviso mostrado (por referencia, nunca copiada), evidencia, y el mini flujo
  de revocacion con sus dos plazos encadenados (5 dias para dejar de tratar, 5 dias mas para informar al
  encargado).
- Obligaciones que cubre (propietario): OBL-CONS-01, OBL-CONS-02, OBL-CONS-03, OBL-CONS-04, OBL-CONS-05,
  OBL-CONS-06, OBL-PRIN-04, OBL-SENS-02, OBL-SENS-03, OBL-SENS-07, OBL-TRANSF-04 (colab).
- Areas del prompt que absorbe: 16 Consentimiento.
- Decision respecto al documento maestro: se mantiene la Sec. 19, corrigiendo que el registro de
  consentimiento referencia (no copia) la version del aviso gestionada en MOD-010 (decision 2.7.6,
  inconsistencia 6), y modelando la revocacion como maquina de estados con dos plazos, no un campo de fecha
  suelto (decision 2.7.12, inconsistencia 14).
- Clasificacion MVP: SHOULD HAVE (V1). Justificacion: el propio prompt del cliente marca este modulo como
  "si va en MVP" (area 16, pregunta abierta), y la ley exige evaluar seis bases de licitud, no solo
  consentimiento (OBL-PRIN-02); en el MVP, el RAT permite elegir "consentimiento" como base y la evidencia
  se adjunta manualmente en MOD-023 (Centro de evidencias) mientras no existe el motor de revocacion
  automatico. Riesgo de este diferimiento: empresas cuya base principal es el consentimiento (marketing,
  e-commerce) quedan con un flujo manual mas lento en el MVP; se documenta en la seccion 8 de riesgos.
- Dependencias: Entra de: MOD-008 (tratamiento con base "consentimiento"), MOD-010 (version del aviso). Sale
  a: MOD-009 (oposicion/marketing directo), MOD-011 (revocacion notifica al encargado), MOD-022, MOD-023.

#### MOD-016 - Transferencias internacionales

- Proposito: registra cada flujo de datos hacia un proveedor o encargado fuera de El Salvador, con pais,
  base, salvaguarda, contrato (por referencia a MOD-011) y el tramite de puesta en conocimiento de la ACE.
  Todo proveedor extranjero genera automaticamente un registro "pendiente de confirmar" aqui.
- Obligaciones que cubre (propietario): OBL-TRANSF-01, OBL-TRANSF-02, OBL-TRANSF-03, OBL-TRANSF-05,
  OBL-TRANSF-06, OBL-SEG-04.
- Areas del prompt que absorbe: 18 Transferencias internacionales.
- Decision respecto al documento maestro: se mantiene la Sec. 24, enlazando por referencia al proveedor y
  contrato ya registrados en MOD-011 en vez de duplicar esos campos (decision 2.7.2); se modela la
  ambiguedad "transferencia vs. acceso del encargado extranjero" como registro "pendiente de confirmar" en
  vez de resolverla de forma automatica (decision 2.7.9, inconsistencia 10).
- Clasificacion MVP: SHOULD HAVE (V1). Justificacion: aunque el uso de proveedores cloud extranjeros es
  comun en pymes salvadorenas y OBL-TRANSF-05 es OBLIGATORIO, el tramite de puesta en conocimiento a la ACE
  no tiene canal formal habilitado por la autoridad (ver seccion 2.3.2 de la validacion), lo que reduce la
  urgencia de construir el flujo completo antes que RAT y Proveedores. Cobertura parcial en el MVP: el
  diagnostico (MOD-006) marca "datos fuera de El Salvador: si" y crea una tarea manual en MOD-022 para que
  el responsable documente la transferencia como evidencia suelta en MOD-023, sin el motor de deteccion
  automatica ni el registro formal "pendiente de confirmar".
- Dependencias: Entra de: MOD-008, MOD-011 (proveedor y contrato). Sale a: MOD-022, MOD-023, MOD-027
  (referencia del tramite ante la ACE).

#### MOD-017 - Retencion y eliminacion (motor de datos)

- Proposito: motor de retencion de los datos personales del titular por finalidad (no por fecha fija),
  donde la fecha efectiva de retencion es el maximo entre todos los OBL-RET aplicables (mercantil,
  tributario, lavado de dinero). Se distingue de la conservacion documental de cumplimiento propio, que vive
  en MOD-010 (Aviso, OBL-RET-04/06) y en el expediente de MOD-009/MOD-012 (OBL-RET-05).
- Obligaciones que cubre (propietario): OBL-RET-01, OBL-RET-02, OBL-RET-03, OBL-RET-05.
- Areas del prompt que absorbe: 22 Retencion.
- Decision respecto al documento maestro: se mantiene la Sec. 21, separando dos motores de retencion en vez
  de uno solo (decision 2.7.13, inconsistencia 15), para evitar que una misma regla borre datos del titular
  junto con un documento de cumplimiento propio, o viceversa.
- Clasificacion MVP: SHOULD HAVE (V1). Justificacion: las obligaciones que este modulo cubre son en su
  mayoria CONDICIONAL (dependen del giro de cada empresa: banca, comercio, sector financiero) o RECOMENDADO
  (OBL-RET-05), no OBLIGATORIO sin condicion; el motor completo (alertas, aprobacion de eliminacion,
  evidencia de borrado) es complejo de construir frente a su urgencia real para una pyme generica. Cobertura
  parcial en el MVP: el campo "periodo de conservacion" ya existe como texto libre dentro del RAT (MOD-008,
  Sec. 14 del maestro), sin alertas automaticas ni flujo de aprobacion de eliminacion.
- Dependencias: Entra de: MOD-008. Sale a: MOD-011 (devolucion/eliminacion de datos por el encargado),
  MOD-022, MOD-023.

#### MOD-018 - Riesgos / EIPD

- Proposito: cuestionario de evaluacion de impacto para tratamientos de alto riesgo (biometria, salud,
  menores, videovigilancia, gran escala), con nivel de riesgo, controles seleccionados del catalogo de
  MOD-013, aprobacion y riesgo residual. El resultado nunca se convierte automaticamente en conclusion legal
  definitiva.
- Obligaciones que cubre (propietario): OBL-DOC-03, OBL-SENS-08 (colab).
- Areas del prompt que absorbe: 20 EIPD / riesgos.
- Decision respecto al documento maestro: se mantiene la Sec. 26, con Control como entidad unica compartida
  con MOD-013 en vez de una lista paralela (decision 2.7.3, inconsistencia 3); se deja explicito que la
  metodologia de scoring es propia del producto, no un formato oficial de la ACE (seccion 2.3.4 de la
  validacion).
- Clasificacion MVP: SHOULD HAVE (V1). Justificacion: las Politicas ACE exigen EIPD (OBL-DOC-03,
  OBLIGATORIO) pero solo para tratamientos de alto riesgo, no para toda pyme desde el primer dia; construir
  un cuestionario de scoring completo es mas complejo que el resto del MVP. Cobertura parcial en el MVP:
  cuando el diagnostico (MOD-006) detecta biometria, salud, menores o camaras, crea una tarea en MOD-022
  ("elaborar EIPD") con una plantilla generica en MOD-010, llenada manualmente, sin el motor de scoring.
  Riesgo: empresas de los sectores mas regulados (bancos, clinicas, empresas con biometria) sienten este
  vacio antes que una pyme generica; se documenta en la seccion 8.
- Dependencias: Entra de: MOD-006 (senal de alto riesgo), MOD-008 (tratamiento evaluado), MOD-013 (catalogo
  de controles). Sale a: MOD-022, MOD-023.

#### MOD-019 - Auditoria de cumplimiento (programa anual)

- Proposito: programa sustantivo de auditoria anual (alcance, hallazgos, plan de accion, cierre), distinto
  del registro tecnico de trazabilidad (MOD-024 AuditLog). Genera el recordatorio anual anclado a la ultima
  auditoria registrada.
- Obligaciones que cubre (propietario): OBL-AUD-01.
- Areas del prompt que absorbe: 24 Auditoria (parte sustantiva; la parte tecnica de trazabilidad la absorbe
  MOD-024).
- Decision respecto al documento maestro: es una separacion nueva. El maestro (Sec. 29, "Auditoria y
  trazabilidad") confunde bajo un mismo nombre el log tecnico y el programa de auditoria sustantivo; se
  separan en dos modulos (decision 2.7.26, faltante 19 de prioridad alta).
- Clasificacion MVP: SHOULD HAVE (V1). Justificacion: es un ciclo anual; una empresa que recien adopta el
  producto no tiene todavia un ano de historial de controles y evidencia sobre el cual auditar de forma
  sustantiva, mientras que el AuditLog tecnico (MOD-024, MUST HAVE) ya deja evidencia desde el primer dia
  para cuando el primer ciclo de auditoria llegue.
- Dependencias: Entra de: MOD-013, MOD-008, MOD-023 (todo lo que se audita). Sale a: MOD-022, MOD-023,
  MOD-029.

#### MOD-020 - Procedimiento sancionador / requerimientos ACE

- Proposito: gestiona la relacion reactiva con la ACE cuando esta abre un procedimiento: contestacion del
  emplazamiento (5 dias habiles), requerimientos de informacion, pago de la multa (15 dias habiles),
  medidas adicionales y seguimiento de la publicidad de resoluciones. Es distinto del Centro regulatorio
  (MOD-027), que solo muestra el catalogo de infracciones como informacion de referencia.
- Obligaciones que cubre (propietario): OBL-SANC-02, OBL-SANC-03, OBL-SANC-04, OBL-SANC-05, OBL-SANC-06,
  OBL-SANC-07.
- Areas del prompt que absorbe: ninguna de las 29 areas lo nombra (es un hallazgo de la validacion); absorbe
  el vacio que deja la Sec. 8.12 del maestro (Sanciones, tratada solo como investigacion, no como modulo
  operativo).
- Decision respecto al documento maestro: es nuevo. El maestro no le da ningun lugar funcional al
  procedimiento sancionador; se crea por la decision 2.7.25 de la validacion (es una de las dos areas
  completas de la matriz sin modulo propio, junto con Delegado).
- Clasificacion MVP: SHOULD HAVE (V1). Justificacion: la mayoria de sus obligaciones son CONDICIONAL (solo
  aplican si la ACE efectivamente abre un procedimiento contra la empresa); no es urgente para una pyme que
  recien empieza a ordenarse, pero es alto valor diferenciador una vez que una empresa cliente enfrenta una
  inspeccion real. El catalogo de infracciones (informativo, OBL-SANC-01) si se muestra desde el MVP dentro
  de MOD-027.
- Dependencias: Entra de: MOD-026 (calculo de plazos de 5 y 15 dias), MOD-012 (incidente que deriva en
  requerimiento). Sale a: MOD-022, MOD-023, MOD-027.

### CAPA 3: RELACION CON EL TITULAR

#### MOD-021 - Portal del titular

- Proposito: sitio publico por organizacion donde el titular consulta el aviso de privacidad, presenta una
  solicitud ARCO-POL, adjunta documentos y consulta el estado de su expediente mediante un mecanismo seguro
  de autenticacion, sin depender de que un empleado reciba el correo o llamada.
- Obligaciones que cubre (propietario): OBL-DOC-04 (colab de MOD-009, que es su propietario), OBL-PLAZO-04
  (colab).
- Areas del prompt que absorbe: 33 Portal del titular.
- Decision respecto al documento maestro: se mantiene la Sec. 18 del maestro como modulo aparte, pero se
  reclasifica su alcance: el maestro lo asumia como la unica arquitectura posible de ARCO-POL; la ley exige
  "mecanismos", no un portal publico especifico (decision 2.7.30, seccion 2.3.4 de la validacion).
- Clasificacion MVP: SHOULD HAVE (V1). Justificacion: un portal publico agrega superficie de riesgo real
  (suplantacion de identidad, exposicion de datos) que conviene madurar despues de validar el flujo interno
  de ARCO-POL (MOD-009, MUST HAVE) con clientes reales; el MVP satisface la obligacion legal con un
  formulario interno seguro operado por el responsable ARCO-POL de la empresa.
- Dependencias: Entra de: MOD-009 (expedientes y su estado), MOD-010 (aviso de privacidad publicado). Sale
  a: MOD-009 (nuevas solicitudes), MOD-025 (comunicaciones al titular).

### CAPA 4: SERVICIOS TRANSVERSALES

Estos siete modulos no tienen "obligaciones propietarias" propias en su mayoria: existen para que los
modulos operativos de las capas 0 a 3 puedan cumplir las suyas de forma probatoria, auditable y usable por
una persona no especialista. Ver seccion 3 para el detalle de por que son transversales y como se conectan.

#### MOD-022 - Centro de tareas

- Proposito: convierte cada obligacion activada por el diagnostico, el RAT, ARCO-POL, incidentes,
  proveedores, controles o cualquier otro modulo operativo en una accion concreta con responsable, fecha,
  fundamento, evidencia requerida y estado (pendiente, en proceso, bloqueada, en revision, aprobada,
  completada, vencida).
- Obligaciones que cubre (propietario): ninguna directamente; es el mecanismo de ejecucion de todas.
- Areas del prompt que absorbe: 14 Centro de tareas.
- Decision respecto al documento maestro: se mantiene la Sec. 16 del maestro sin cambios estructurales
  relevantes.
- Clasificacion MVP: MUST HAVE. Justificacion: sin tareas, el diagnostico y el plan de cumplimiento (ambos
  MUST HAVE) son solo listas de lectura, no un sistema de gestion; es el mecanismo que convierte "lo que la
  ley exige" en "lo que alguien tiene que hacer el martes".
- Dependencias: Entra de: todos los modulos operativos de las capas 0 a 3. Sale a: MOD-025 (recordatorios),
  MOD-023 (evidencia adjunta a la tarea), MOD-029.

#### MOD-023 - Centro de evidencias

- Proposito: responde "que evidencia tenemos de esta obligacion" conectando archivos, aprobaciones,
  documentos, tareas cerradas y responsables. Es una entidad propia (Evidencia: artefacto o referencia
  inmutable vinculada a un registro especifico), distinta del Documento (contenido versionado) y del
  AuditLog (registro tecnico de acciones); el paquete de evidencias exportable es una vista sobre las tres,
  sin almacenamiento propio, y siempre incluye un mecanismo de verificacion de integridad (hash o firma).
- Obligaciones que cubre (propietario): OBL-PRIN-03.
- Areas del prompt que absorbe: 25 Centro de evidencias.
- Decision respecto al documento maestro: se separan explicitamente tres entidades que el maestro mezclaba
  (Sec. 16 a 27 de forma dispersa, Sec. 29, Sec. 30): Documento, Evidencia y AuditLog (decision 2.7.4,
  inconsistencias 4 y 11); el paquete de evidencias exportado siempre lleva verificacion de integridad
  propia (decision 2.7.24, inconsistencia 26).
- Clasificacion MVP: MUST HAVE. Justificacion: es la pieza que hace al MVP "probatorio", no solo
  "organizado"; sin esto, cada modulo MUST HAVE (RAT, ARCO-POL, Incidentes, Controles, Capacitacion) genera
  registros que nadie puede presentar de forma consolidada ante la ACE o un cliente que audita.
- Dependencias: Entra de: todos los modulos operativos y MOD-022. Sale a: MOD-024 (cada evidencia genera un
  evento de auditoria), MOD-030 (V1, exportacion como reporte), MOD-029.

#### MOD-024 - Registro de auditoria (AuditLog)

- Proposito: registro tecnico e inmutable de toda accion relevante (usuario, fecha, hora, recurso, valor
  anterior y nuevo, motivo, aprobacion). Los usuarios normales no pueden borrar ni modificar estos registros;
  requiere un control de integridad especifico, no solo un permiso mas del RBAC generico.
- Obligaciones que cubre (propietario): OBL-PRIN-03 (colab de MOD-023, que es su propietario para efectos de
  la ficha, pero el AuditLog es quien materialmente sostiene la responsabilidad demostrada a nivel tecnico).
- Areas del prompt que absorbe: 24 Auditoria (parte tecnica de trazabilidad).
- Decision respecto al documento maestro: se mantiene la Sec. 29 del maestro, separando expresamente el log
  tecnico del programa de auditoria sustantivo (MOD-019, decision 2.7.26); las tecnicas de integridad
  (WORM, hash chaining, append-only) se documentan como estandar propio de ingenieria, no como requisito
  legal expreso (seccion 2.3.5 de la validacion, punto 29).
- Clasificacion MVP: MUST HAVE. Justificacion: registrar cada accion es barato de construir junto con cada
  CRUD de los modulos MUST HAVE (se agrega al mismo tiempo que se construye cada modulo, no despues) y es
  la base tecnica sin la cual el Centro de evidencias (MUST HAVE) no tiene de donde sacar "quien hizo que y
  cuando".
- Dependencias: Entra de: todos los modulos. Sale a: MOD-023.

#### MOD-025 - Notificaciones

- Proposito: envia alertas de plazos, tareas asignadas, escalamientos y avisos (deadline de ARCO-POL, 72
  horas de incidentes, tareas vencidas) por un canal configurable, sin asumir de entrada que la empresa usa
  Teams, Slack, SMS o WhatsApp.
- Obligaciones que cubre (propietario): ninguna directamente; es el mecanismo que hace efectivos los plazos
  de otras obligaciones (soporta el cumplimiento de OBL-ARCO-10, OBL-INC-01, entre otras, sin ser su
  propietario).
- Areas del prompt que absorbe: 27 Notificaciones.
- Decision respecto al documento maestro: se mantiene la Sec. "27. Notificaciones" (area del prompt
  consolidado; corresponde a los canales evaluados de forma generica en distintas secciones del maestro),
  sin asumir todos los canales listados.
- Clasificacion MVP: MUST HAVE (canal unico). Justificacion: sin alertas, los plazos de 20+20 dias
  (ARCO-POL) y 72 horas (incidentes) dependen de que alguien recuerde revisar la plataforma; el canal
  minimo (correo electronico o notificacion dentro de la plataforma) es barato de construir y es el que
  vuelve utiles a MOD-009 y MOD-012 desde el primer dia. Canales adicionales (Teams, Slack, SMS, WhatsApp)
  se difieren a V1 segun demanda real de los primeros clientes.
- Dependencias: Entra de: MOD-022, MOD-009, MOD-012, MOD-026 (calculo de cuando alertar). Sale a: MOD-021
  (V1, comunicaciones al titular), MOD-024 (registro de envio).

#### MOD-026 - Calendario y motor de plazos habiles

- Proposito: unica fuente de calculo de dias y horas habiles (asuetos nacionales configurables por ano) que
  consultan ARCO-POL, Incidentes, Delegado y, en V1, Procedimiento sancionador. Evita que cada modulo
  implemente su propio calculo con riesgo de reglas inconsistentes entre si.
- Obligaciones que cubre (propietario): OBL-PLAZO-01, OBL-PLAZO-02.
- Areas del prompt que absorbe: 30 Calendario central.
- Decision respecto al documento maestro: es una separacion nueva respecto de la Sec. 17 y 25 del maestro,
  que trataban el calendario como un detalle de cada modulo en vez de una dependencia central (decision
  2.7.15, inconsistencia 17, faltante 31); el calendario de dias inhabiles es un dato configurable y
  versionado por ano, mantenido manualmente por el equipo del producto hasta que exista una fuente oficial
  unica (seccion 2.3.1 de la validacion).
- Clasificacion MVP: MUST HAVE. Justificacion: MOD-009 (ARCO-POL) y MOD-012 (Incidentes), ambos MUST HAVE,
  no pueden calcular un solo plazo legal correcto sin este motor; construirlo una vez y compartirlo es mas
  barato y mas seguro que dejar que cada modulo calcule por su cuenta.
- Dependencias: Entra de: nada (catalogo de configuracion). Sale a: MOD-009, MOD-012, MOD-003, MOD-025, y
  (V1) MOD-020.

#### MOD-027 - Centro regulatorio (incl. actualizaciones normativas)

- Proposito: muestra el marco normativo consultable (ley, politicas ACE, lineamientos) diferenciando
  VIGENTE, FUTURO, DEROGADO y MODIFICADO, y aloja el interruptor de activacion manual del doble estado de la
  reforma 659 (ver seccion 4). La experiencia de "que cambio, que afecta, que procesos requieren revision"
  (area 32 del prompt) es una funcion transversal de este mismo modulo, no un modulo aparte.
- Obligaciones que cubre (propietario): OBL-SEG-01, OBL-SEG-06, OBL-SANC-01, OBL-SANC-08, OBL-AUD-02,
  OBL-PLAZO-05.
- Areas del prompt que absorbe: 31 Centro regulatorio, 32 Actualizaciones normativas (funcion transversal
  de este modulo).
- Decision respecto al documento maestro: corresponde a la Sec. 40 y 41 del maestro (Motor regulatorio,
  Actualizacion normativa), separando explicitamente que campos son genericos ("Core Privacy Engine") y
  cuales son especificos de El Salvador en la ficha de cada modulo operativo (decision 2.7.20, inconsistencia
  22); documenta la reforma 659 como primer caso de uso concreto del motor de doble estado (decision 2.7.16,
  inconsistencia 18).
- Clasificacion MVP: MUST HAVE (version minima). Justificacion: el interruptor manual del estado de la
  reforma 659 debe existir desde el primer dia porque MOD-003 (Delegado) y MOD-009 (ARCO-POL) cambian de
  comportamiento segun ese estado; la version completa (biblioteca navegable de cada articulo con historial
  de versiones) se difiere a V1, y el MVP se limita a un panel de estado (vigente/pendiente de confirmar)
  mas la lista de las 17 obligaciones afectadas por la reforma.
- Dependencias: Entra de: nada (fuente de verdad regulatoria). Sale a: MOD-003, MOD-009, MOD-020, MOD-028,
  y todo modulo que necesite mostrar el estado de vigencia de una obligacion.

#### MOD-028 - Centro de ayuda contextual

- Proposito: para cada obligacion o campo, explica que es, por que hay que registrarlo, el fundamento legal
  (OBL-ID y articulo, en segundo nivel) y cuando se necesita ayuda juridica externa, en lenguaje sencillo
  para quien no es especialista.
- Obligaciones que cubre (propietario): ninguna directamente; es la capa de accesibilidad de todas.
- Areas del prompt que absorbe: 34 Centro de ayuda contextual por modulo.
- Decision respecto al documento maestro: corresponde a la Sec. 32 (UX) y a la frase reutilizable "requiere
  validacion de la organizacion o asesoria especializada" (Sec. 42), que la validacion identifica como una
  etiqueta que debe repetirse en toda la plataforma (seccion 2.2, fila sobre Sec. 42).
- Clasificacion MVP: MUST HAVE. Justificacion: el principio central del producto ("usable por una persona no
  especialista") no es alcanzable sin ayuda contextual; su costo de construccion es bajo (contenido estatico
  ligado a cada obligacion) frente a su impacto en la adopcion real del MVP.
- Dependencias: Entra de: MOD-027 (fundamento legal de cada texto de ayuda). Sale a: todos los modulos
  operativos (contenido de ayuda por campo y por obligacion).

### CAPA 5: VISUALIZACION Y SALIDA

#### MOD-029 - Dashboard

- Proposito: vista de estado del programa por perspectiva (Gerencia: vision general; Responsable:
  pendientes propios). Nunca expresa "cumplimiento legal X%"; usa "controles configurados", "tareas
  pendientes", "evidencia disponible".
- Obligaciones que cubre (propietario): ninguna directamente; es la capa de lectura de todas.
- Areas del prompt que absorbe: 26 Dashboard principal.
- Decision respecto al documento maestro: se mantiene la Sec. 31, reforzando la prohibicion de mostrar un
  porcentaje de cumplimiento legal (coherente con OBL-PRIN-03 y con la Sec. 9 del maestro).
- Clasificacion MVP: MUST HAVE (version minima). Justificacion: es el primer elemento que una gerencia mira
  al entrar; sin el, el MVP no se siente como un producto terminado. Las vistas de Legal (riesgos y
  decisiones) y Auditor (evidencias) se difieren a V1 porque dependen de datos que solo existen cuando
  MOD-018 (Riesgos/EIPD) y MOD-019 (Auditoria de cumplimiento) esten activos; en el MVP, Legal y Auditor usan
  la misma vista que Responsable con filtros mas amplios.
- Dependencias: Entra de: MOD-022, MOD-023, MOD-007, y todo modulo operativo activo. Sale a: nada (es
  consumidor final).

#### MOD-030 - Reportes

- Proposito: reportes formales por area (gerencial, ARCO-POL, incidentes, proveedores, RAT, seguridad) en
  PDF/XLSX/CSV, distintos del paquete de evidencias puntual de MOD-023 (que responde "que evidencia tenemos
  de esta obligacion"): este modulo responde "como va el programa en el periodo X".
- Obligaciones que cubre (propietario): ninguna directamente.
- Areas del prompt que absorbe: 28 Reportes.
- Decision respecto al documento maestro: se mantiene la Sec. "28. Reportes" del prompt consolidado,
  diferenciandolo explicitamente del paquete de evidencias (Sec. 30 del maestro), que en el maestro
  aparecian mezclados.
- Clasificacion MVP: SHOULD HAVE (V1). Justificacion: con pocos meses de historial, una pyme recien
  incorporada no tiene todavia series de datos que justifiquen reportes periodicos formales; el Centro de
  evidencias (MUST HAVE) ya cubre la necesidad inmediata de "mostrar evidencia de esto" ante una auditoria o
  un cliente puntual.
- Dependencias: Entra de: todos los modulos operativos, MOD-023. Sale a: nada (consumidor final).

#### MOD-031 - Busqueda global

- Proposito: busqueda por texto libre a traves de tratamientos, tareas, documentos, proveedores,
  expedientes ARCO-POL e incidentes, con resultados filtrados por permiso del usuario.
- Obligaciones que cubre (propietario): ninguna.
- Areas del prompt que absorbe: 29 Busqueda global.
- Decision respecto al documento maestro: se mantiene la Sec. "29. Busqueda global" del prompt consolidado
  sin cambios de alcance.
- Clasificacion MVP: COULD HAVE (V1/V2). Justificacion: con el volumen de datos que una pyme genera en sus
  primeros meses (decenas de registros, no miles), la navegacion por modulo y por el Centro de tareas es
  suficiente; el valor de una busqueda global crece con el volumen de datos, que solo aparece con el tiempo
  o en clientes Enterprise con muchas sedes.
- Dependencias: Entra de: todos los modulos con contenido indexable. Sale a: nada (consumidor final).

---

## 3. Modulos transversales y como se conectan

Siete modulos son transversales en sentido estricto: existen para servir a todos los demas y ninguno de
los modulos operativos (capas 0 a 3) podria cumplir su obligacion de forma completa y probatoria sin ellos.
Se reconocen por una propiedad comun: no tienen obligaciones OBLIGATORIO propias en su mayoria (excepto
donde se indica), y su ausencia no elimina una obligacion legal pero si elimina la capacidad del producto de
demostrarla o de operarla a tiempo.

| Modulo | Que aportaria si faltara (riesgo de no tenerlo) | Quien lo consume |
|---|---|---|
| MOD-022 Centro de tareas | Las obligaciones detectadas quedarian como texto sin responsable ni fecha | Todos los modulos operativos |
| MOD-023 Centro de evidencias | El programa existiria pero no seria demostrable ante la ACE o un cliente | Todos los modulos operativos, MOD-029, MOD-030 |
| MOD-024 Registro de auditoria | No habria forma de probar quien hizo que y cuando (OBL-PRIN-03) | MOD-023, y cualquier disputa interna o requerimiento de la ACE |
| MOD-025 Notificaciones | Los plazos legales (20+20 dias, 72 horas, 5 dias) dependerian de que alguien recuerde entrar a mirar | MOD-009, MOD-012, MOD-022 |
| MOD-026 Calendario y motor de plazos | Cada modulo con plazo legal calcularia dias habiles por su cuenta, con riesgo de resultados distintos para el mismo caso | MOD-009, MOD-012, MOD-003, (V1) MOD-020 |
| MOD-027 Centro regulatorio | No existiria un lugar unico donde saber si la reforma 659 ya aplica o no, y cada modulo tendria que decidirlo por separado | MOD-003, MOD-009, (V1) MOD-020 |
| MOD-028 Centro de ayuda | El usuario no especialista quedaria solo frente a terminologia juridica, rompiendo el principio central del producto | Todos los modulos operativos |

Conexion tipica de un caso real (ejemplo: una solicitud ARCO-POL que vence en 3 dias):

```
MOD-026 calcula el plazo restante
        |
        v
MOD-025 dispara una alerta al Responsable ARCO-POL
        |
        v
MOD-022 muestra la tarea "responder solicitud X" con prioridad alta
        |
        v
Al cerrarse, MOD-023 registra la respuesta enviada como evidencia
        |
        v
MOD-024 deja el rastro tecnico de quien aprobo y cuando
        |
        v
MOD-029 refleja "0 solicitudes vencidas" en el dashboard de Gerencia
```

Dos modulos de la capa 5 (MOD-029 Dashboard, MOD-030 Reportes) y MOD-031 Busqueda global no se cuentan
como transversales en sentido estricto: son consumidores de los datos que generan los modulos operativos y
los siete transversales, pero ningun modulo operativo depende de ellos para cumplir una obligacion (son de
salida, no de soporte a la operacion). Por eso MOD-029 puede quedar en MVP con alcance minimo mientras
MOD-030 y MOD-031 se difieren sin bloquear a ningun modulo MUST HAVE.

---

## 4. Como se modela el doble estado de la reforma 659

Contexto juridico (ver `01_legal/matriz_obligaciones.md` y `02_validacion_de_la_idea.md`, seccion 2.7.16):
el Decreto Legislativo 659 fue aprobado el 17-sep-2026 pero al 24-sep-2026 no esta confirmada su
publicacion en el Diario Oficial. Mientras no se publique, el texto vigente del Decreto 144 (Arts. 15 y 17)
exige delegado obligatorio en el sector privado. Segun fuentes secundarias, la reforma eliminaria esa
obligatoriedad y trasladaria las funciones al "sujeto obligado" (responsable interno, sin nombramiento
formal ante la ACE). 17 obligaciones de la matriz quedan marcadas como afectadas por esta reforma.

**Regla de diseno: no se crean dos modulos ("Delegado" y "Responsable interno").** Existe un unico modulo,
MOD-003, que gestiona una sola entidad conceptual ("la persona o area interna responsable de proteccion de
datos de la empresa"). Lo que cambia entre los dos estados no es el modulo ni la entidad: es que campos y
pasos del mismo flujo son obligatorios, opcionales u ocultos.

Mecanismo concreto:

1. **Bandera de estado regulatorio en MOD-027 (Centro regulatorio), nunca automatica por fecha de
   aprobacion legislativa** (decision 2.7.16 y supuesto correcto de la seccion 2.2, fila sobre Sec. 8.2 del
   maestro). Dos valores posibles: `ESTADO_ACTUAL` (Decreto 144 vigente, delegado obligatorio) y
   `ESTADO_REFORMADO` (Decreto 659 confirmado como publicado y vigente). El cambio de `ESTADO_ACTUAL` a
   `ESTADO_REFORMADO` lo activa manualmente una persona con permiso de administracion de la plataforma
   (nunca un usuario de la empresa cliente ni un disparador automatico), y solo despues de que el equipo del
   producto verifique el texto oficial publicado en el Diario Oficial.
2. **Cada obligacion de la matriz que cita `afectada_por_reforma_659.afectada = true` (17 en total, ver
   `matriz_obligaciones.json`) lleva una referencia a esta bandera.** Mientras la bandera este en
   `ESTADO_ACTUAL`, MOD-003 exige los pasos completos: nombramiento formal, comunicacion a la ACE en 15 dias
   habiles (OBL-DPO-03), reverificacion cada 3 anos (OBL-DPO-04), capacitacion anual especifica (OBL-DPO-05),
   informes semestrales (OBL-DPO-07). Cuando la bandera pase a `ESTADO_REFORMADO`, esos pasos dejan de ser
   obligatorios para empresas nuevas; las tareas abiertas que dependian de ellos se marcan "no aplica bajo el
   estado regulatorio actual, ver historial" en vez de eliminarse (no se borra informacion: se preserva el
   rastro de auditoria, coherente con el principio de responsabilidad demostrada, OBL-PRIN-03).
3. **El rol en MOD-002 no cambia de nombre tecnico entre estados** (sigue siendo el mismo registro de
   persona con el mismo historial de asignaciones); solo cambia la etiqueta visible al usuario ("Delegado de
   Proteccion de Datos" en `ESTADO_ACTUAL`, "Responsable interno de proteccion de datos" en
   `ESTADO_REFORMADO`) y el conjunto de campos obligatorios que MOD-003 le exige completar.
4. **Un expediente resuelto antes del cambio de estado conserva las reglas vigentes en el momento en que se
   resolvio** (decision correcta ya identificada en la seccion 2.2 de la validacion, fila sobre Sec. 41 del
   maestro): MOD-003 versiona sus propios formularios y checklists igual que MOD-027 versiona las reglas
   normativas, de modo que un nombramiento certificado bajo `ESTADO_ACTUAL` no se reinterpreta
   retroactivamente cuando el estado cambie.
5. **Empresas que ya nombraron delegado bajo `ESTADO_ACTUAL` pueden mantenerlo voluntariamente en
   `ESTADO_REFORMADO`** (el sistema no fuerza el cese); el modulo simplemente deja de exigir los pasos que la
   reforma habria vuelto opcionales, pero conserva la opcion de seguir usandolos si la empresa lo decide como
   buena practica.

Consecuencia para el MVP: MOD-003 se construye una sola vez, con la bandera de MOD-027 como parametro de
entrada desde el primer dia. No hay version "MVP sin reforma" y version "V1 con reforma" del modulo: hay un
solo modulo cuyo comportamiento depende de un dato de configuracion regulatoria que hoy, al 24-sep-2026,
esta fijo en `ESTADO_ACTUAL` porque la publicacion no esta confirmada.

---

## 5. Tabla de cobertura: OBL-ID -> modulo propietario (105 obligaciones)

Fuente: `01_legal/matriz_obligaciones.md`. Cada obligacion tiene exactamente un modulo propietario; los
modulos colaboradores relevantes se mencionan en la ficha del modulo (seccion 2), no aqui, para mantener
esta tabla legible.

### AMB - Ambito de aplicacion

| OBL-ID | Modulo propietario |
|---|---|
| OBL-AMB-01 | MOD-006 Diagnostico de cumplimiento |
| OBL-AMB-02 | MOD-006 Diagnostico de cumplimiento |
| OBL-AMB-03 | MOD-006 Diagnostico de cumplimiento |
| OBL-AMB-04 | MOD-006 Diagnostico de cumplimiento |

### PRIN - Principios rectores

| OBL-ID | Modulo propietario |
|---|---|
| OBL-PRIN-01 | MOD-008 RAT |
| OBL-PRIN-02 | MOD-008 RAT |
| OBL-PRIN-03 | MOD-023 Centro de evidencias |
| OBL-PRIN-04 | MOD-015 Consentimiento (V1) |

### ARCO - Derechos ARCO-POL

| OBL-ID | Modulo propietario |
|---|---|
| OBL-ARCO-01 | MOD-009 ARCO-POL |
| OBL-ARCO-02 | MOD-009 ARCO-POL |
| OBL-ARCO-03 | MOD-009 ARCO-POL |
| OBL-ARCO-04 | MOD-009 ARCO-POL |
| OBL-ARCO-05 | MOD-009 ARCO-POL |
| OBL-ARCO-06 | MOD-009 ARCO-POL |
| OBL-ARCO-07 | MOD-009 ARCO-POL |
| OBL-ARCO-08 | MOD-009 ARCO-POL |
| OBL-ARCO-09 | MOD-009 ARCO-POL |
| OBL-ARCO-10 | MOD-009 ARCO-POL |
| OBL-ARCO-11 | MOD-009 ARCO-POL |
| OBL-ARCO-12 | MOD-009 ARCO-POL |
| OBL-ARCO-13 | MOD-009 ARCO-POL |
| OBL-ARCO-14 | MOD-009 ARCO-POL |
| OBL-ARCO-15 | MOD-009 ARCO-POL |

### DPO - Delegado de Proteccion de Datos

| OBL-ID | Modulo propietario |
|---|---|
| OBL-DPO-01 | MOD-003 Delegado de Proteccion de Datos |
| OBL-DPO-02 | MOD-003 Delegado de Proteccion de Datos |
| OBL-DPO-03 | MOD-003 Delegado de Proteccion de Datos |
| OBL-DPO-04 | MOD-003 Delegado de Proteccion de Datos |
| OBL-DPO-05 | MOD-003 Delegado de Proteccion de Datos |
| OBL-DPO-06 | MOD-003 Delegado de Proteccion de Datos |
| OBL-DPO-07 | MOD-003 Delegado de Proteccion de Datos |
| OBL-DPO-08 | MOD-003 Delegado de Proteccion de Datos |

### AVISO - Aviso y politica de privacidad

| OBL-ID | Modulo propietario |
|---|---|
| OBL-AVISO-01 | MOD-010 Documentos y politicas |
| OBL-AVISO-02 | MOD-010 Documentos y politicas |
| OBL-AVISO-03 | MOD-010 Documentos y politicas |
| OBL-AVISO-04 | MOD-010 Documentos y politicas |
| OBL-AVISO-05 | MOD-010 Documentos y politicas |

### CONS - Consentimiento

| OBL-ID | Modulo propietario |
|---|---|
| OBL-CONS-01 | MOD-015 Consentimiento (V1) |
| OBL-CONS-02 | MOD-015 Consentimiento (V1) |
| OBL-CONS-03 | MOD-015 Consentimiento (V1) |
| OBL-CONS-04 | MOD-015 Consentimiento (V1) |
| OBL-CONS-05 | MOD-015 Consentimiento (V1) |
| OBL-CONS-06 | MOD-015 Consentimiento (V1) |

### SENS - Datos sensibles

| OBL-ID | Modulo propietario |
|---|---|
| OBL-SENS-01 | MOD-008 RAT |
| OBL-SENS-02 | MOD-015 Consentimiento (V1) |
| OBL-SENS-03 | MOD-015 Consentimiento (V1) |
| OBL-SENS-04 | MOD-008 RAT |
| OBL-SENS-05 | MOD-008 RAT |
| OBL-SENS-06 | MOD-008 RAT |
| OBL-SENS-07 | MOD-015 Consentimiento (V1) |
| OBL-SENS-08 | MOD-008 RAT |

### TRAT - Tratamiento general

| OBL-ID | Modulo propietario |
|---|---|
| OBL-TRAT-01 | MOD-008 RAT |
| OBL-TRAT-02 | MOD-008 RAT |
| OBL-TRAT-03 | MOD-008 RAT |

### PROV - Proveedores / Encargados

| OBL-ID | Modulo propietario |
|---|---|
| OBL-PROV-01 | MOD-011 Proveedores y encargados |
| OBL-PROV-02 | MOD-011 Proveedores y encargados |
| OBL-PROV-03 | MOD-011 Proveedores y encargados |
| OBL-PROV-04 | MOD-011 Proveedores y encargados |
| OBL-PROV-05 | MOD-011 Proveedores y encargados |
| OBL-PROV-06 | MOD-011 Proveedores y encargados |
| OBL-PROV-07 | MOD-011 Proveedores y encargados |

### TRANSF - Transferencias de datos

| OBL-ID | Modulo propietario |
|---|---|
| OBL-TRANSF-01 | MOD-016 Transferencias internacionales (V1) |
| OBL-TRANSF-02 | MOD-016 Transferencias internacionales (V1) |
| OBL-TRANSF-03 | MOD-016 Transferencias internacionales (V1) |
| OBL-TRANSF-04 | MOD-016 Transferencias internacionales (V1) |
| OBL-TRANSF-05 | MOD-016 Transferencias internacionales (V1) |
| OBL-TRANSF-06 | MOD-016 Transferencias internacionales (V1) |

### SEG - Seguridad (medidas tecnicas/organizativas)

| OBL-ID | Modulo propietario |
|---|---|
| OBL-SEG-01 | MOD-027 Centro regulatorio |
| OBL-SEG-02 | MOD-013 Controles de seguridad |
| OBL-SEG-03 | MOD-013 Controles de seguridad |
| OBL-SEG-04 | MOD-016 Transferencias internacionales (V1) |
| OBL-SEG-05 | MOD-013 Controles de seguridad |
| OBL-SEG-06 | MOD-027 Centro regulatorio |

### DOC - Documentacion

| OBL-ID | Modulo propietario |
|---|---|
| OBL-DOC-01 | MOD-009 ARCO-POL |
| OBL-DOC-02 | MOD-008 RAT |
| OBL-DOC-03 | MOD-018 Riesgos / EIPD (V1) |
| OBL-DOC-04 | MOD-009 ARCO-POL |

### INC - Incidentes / vulneraciones

| OBL-ID | Modulo propietario |
|---|---|
| OBL-INC-01 | MOD-012 Incidentes de seguridad |
| OBL-INC-02 | MOD-012 Incidentes de seguridad |
| OBL-INC-03 | MOD-012 Incidentes de seguridad |
| OBL-INC-04 | MOD-012 Incidentes de seguridad |
| OBL-INC-05 | MOD-012 Incidentes de seguridad |

### CAP - Capacitacion

| OBL-ID | Modulo propietario |
|---|---|
| OBL-CAP-01 | MOD-014 Capacitacion |
| OBL-CAP-02 | MOD-014 Capacitacion |

### AUD - Auditoria

| OBL-ID | Modulo propietario |
|---|---|
| OBL-AUD-01 | MOD-019 Auditoria de cumplimiento (V1) |
| OBL-AUD-02 | MOD-027 Centro regulatorio |

### SANC - Sanciones y procedimiento

| OBL-ID | Modulo propietario |
|---|---|
| OBL-SANC-01 | MOD-027 Centro regulatorio |
| OBL-SANC-02 | MOD-020 Procedimiento sancionador (V1) |
| OBL-SANC-03 | MOD-020 Procedimiento sancionador (V1) |
| OBL-SANC-04 | MOD-020 Procedimiento sancionador (V1) |
| OBL-SANC-05 | MOD-020 Procedimiento sancionador (V1) |
| OBL-SANC-06 | MOD-020 Procedimiento sancionador (V1) |
| OBL-SANC-07 | MOD-020 Procedimiento sancionador (V1) |
| OBL-SANC-08 | MOD-027 Centro regulatorio |
| OBL-SANC-09 | MOD-009 ARCO-POL |

### PLAZO - Plazos y calendario

| OBL-ID | Modulo propietario |
|---|---|
| OBL-PLAZO-01 | MOD-026 Calendario y motor de plazos |
| OBL-PLAZO-02 | MOD-026 Calendario y motor de plazos |
| OBL-PLAZO-03 | MOD-006 Diagnostico de cumplimiento |
| OBL-PLAZO-04 | MOD-009 ARCO-POL |
| OBL-PLAZO-05 | MOD-027 Centro regulatorio |

### RET - Retencion / conservacion documental

| OBL-ID | Modulo propietario |
|---|---|
| OBL-RET-01 | MOD-017 Retencion y eliminacion (V1) |
| OBL-RET-02 | MOD-017 Retencion y eliminacion (V1) |
| OBL-RET-03 | MOD-017 Retencion y eliminacion (V1) |
| OBL-RET-04 | MOD-010 Documentos y politicas |
| OBL-RET-05 | MOD-017 Retencion y eliminacion (V1) |
| OBL-RET-06 | MOD-010 Documentos y politicas |

Verificacion de conteo: 4+4+15+8+5+6+8+3+7+6+6+4+5+2+2+9+5+6 = 105 obligaciones cubiertas, cada una con
exactamente un modulo propietario.

---

## 6. Tabla de cobertura: areas del prompt (8.1 a 34) -> modulo

Las 29 areas exigidas por `00_prompt_analisis_funcional.md`. "Transversal de" indica que el area no es un
modulo en si, sino una funcion que absorbe el modulo transversal indicado.

| Area | Nombre | Modulo(s) |
|---|---|---|
| 8.1 | Configuracion de empresa | MOD-001 Organizacion y estructura |
| 8.2 | Usuarios, roles y permisos | MOD-002 Usuarios, roles y permisos |
| 8.3 | Onboarding | MOD-005 Onboarding |
| 9 | Diagnostico | MOD-006 Diagnostico de cumplimiento |
| 10 | Plan de cumplimiento | MOD-007 Plan de cumplimiento |
| 11 | RAT | MOD-008 RAT |
| 12 | Mapa de datos | MOD-008 RAT (vista, no base de datos aparte) |
| 13 | ARCO-POL | MOD-009 ARCO-POL |
| 14 | Centro de tareas | MOD-022 Centro de tareas (transversal) |
| 15 | Documentos y politicas | MOD-010 Documentos y politicas |
| 16 | Consentimiento | MOD-015 Consentimiento (V1) |
| 17 | Proveedores | MOD-011 Proveedores y encargados |
| 18 | Transferencias internacionales | MOD-016 Transferencias internacionales (V1) |
| 19 | Incidentes | MOD-012 Incidentes de seguridad |
| 20 | EIPD / Riesgos | MOD-018 Riesgos / EIPD (V1) |
| 21 | Controles de seguridad | MOD-013 Controles de seguridad |
| 22 | Retencion | MOD-017 Retencion y eliminacion (V1); conservacion documental especifica en MOD-010 |
| 23 | Capacitacion | MOD-014 Capacitacion |
| 24 | Auditoria | MOD-019 Auditoria de cumplimiento (programa, V1) + MOD-024 AuditLog (transversal, tecnico) |
| 25 | Centro de evidencias | MOD-023 Centro de evidencias (transversal) |
| 26 | Dashboard | MOD-029 Dashboard |
| 27 | Notificaciones | MOD-025 Notificaciones (transversal) |
| 28 | Reportes | MOD-030 Reportes (V1) |
| 29 | Busqueda global | MOD-031 Busqueda global (V1/V2) |
| 30 | Calendario central | MOD-026 Calendario y motor de plazos (transversal) |
| 31 | Centro regulatorio | MOD-027 Centro regulatorio (transversal) |
| 32 | Actualizaciones normativas | Transversal de MOD-027 Centro regulatorio |
| 33 | Portal del titular | MOD-021 Portal del titular (V1) |
| 34 | Centro de ayuda contextual | MOD-028 Centro de ayuda (transversal) |

Nota sobre el area 24: se asigna a dos modulos porque la propia validacion (decision 2.7.26) exige separar
el programa sustantivo de auditoria (ciclo anual, hallazgos, plan de accion) del registro tecnico
inmutable de acciones (AuditLog); tratarlos como un area con un unico modulo repetiria la confusion que el
documento maestro ya tenia en su Sec. 29.

---

## 7. Entidades conceptuales principales que implica el mapa

Lista de entidades que el mapa de modulos obliga a modelar (sin SQL ni esquema tecnico, solo el concepto y
su rol). Agrupadas por el modulo que las origina como propietario; una entidad puede ser referenciada por
muchos modulos.

- **Organization** (MOD-001): la empresa cliente. **Branch/Sede** (MOD-001): sucursal dentro de la misma
  razon social (multi-sede en MVP; multi-empresa/grupo queda fuera de MVP, ver decision 2.7.31).
- **Department/Area** (MOD-001): unidad interna a la que se asignan responsables.
- **User** (MOD-002), **Role** (MOD-002), **Permission** (MOD-002): identidad, rol activo y permisos por
  modulo/accion.
- **DPOAssignment** (MOD-003): registro del nombramiento vigente (persona, fecha, estado ACTUAL/REFORMADO,
  comunicaciones a la ACE, reverificaciones, informes).
- **System** (MOD-004): sistema o aplicacion que trata datos, con pais de alojamiento.
- **DiagnosticAnswer** (MOD-006): respuesta a una pregunta del cuestionario guiado, con el tratamiento,
  tarea o riesgo que dispara.
- **ComplianceAction** (MOD-007): accion priorizada del plan (critica/importante/recomendada).
- **Treatment** (MOD-008): actividad de tratamiento (el nucleo del RAT), con finalidad, base juridica,
  categorias de datos y de titulares, sistemas, encargados, retencion.
- **Purpose**, **LegalBasis**, **DataCategory**, **DataSubjectCategory** (MOD-008): catalogos que
  parametrizan cada Treatment.
- **PrivacyRequest** (MOD-009): expediente ARCO-POL, con tipo de derecho, solicitante, plazos,
  prevenciones, prorroga, resolucion.
- **IdentityVerification** (MOD-009): subproceso de verificacion del solicitante (titular, representante,
  heredero).
- **Document** (MOD-010) y **DocumentVersion** (MOD-010): contenido versionado (aviso, politica,
  procedimientos), con estado de aprobacion y publicacion.
- **Vendor/Encargado**, **ThirdPartyReceptor**, **Subprocessor/Subencargado** (MOD-011): tres tipos de
  entidad externa con reglas propias.
- **Contract/DPA** (MOD-011, como tipo de Document referenciado): acuerdo con el proveedor.
- **Incident** (MOD-012): vulneracion de seguridad, con los dos cronometros de 72 horas y su cadena de
  contencion, notificacion y cierre.
- **Control** (MOD-013): medida tecnica/organizativa/fisica, compartida con MOD-018.
- **TrainingRecord** (MOD-014): evidencia de capacitacion recibida.
- **Consent** (MOD-015, V1): registro de consentimiento por titular y finalidad, con su revocacion.
- **Transfer** (MOD-016, V1): flujo de datos hacia un pais o proveedor extranjero, con su estado
  "pendiente de confirmar".
- **Country** (catalogo compartido por MOD-016 y MOD-001).
- **RetentionRule** (MOD-017, V1): regla de retencion por finalidad, con la fecha efectiva calculada.
- **RiskAssessment/DPIA** (MOD-018, V1): evaluacion de impacto, con nivel de riesgo y riesgo residual.
- **AuditProgram** y **AuditFinding** (MOD-019, V1): ciclo anual sustantivo y sus hallazgos.
- **SanctionCase** (MOD-020, V1): procedimiento abierto por la ACE, con emplazamiento, defensa y multa.
- **DataSubjectPortalAccount** (MOD-021, V1): acceso del titular al portal.
- **Task** (MOD-022): unidad de trabajo asignable, con fundamento, evidencia requerida y estado.
- **Evidence** (MOD-023): artefacto o referencia inmutable vinculado a un registro especifico, distinto de
  Document y de AuditLogEvent.
- **AuditLogEvent** (MOD-024): registro tecnico de una accion (quien, que, cuando, valor anterior/nuevo).
- **Notification** (MOD-025): alerta enviada, con su canal, destinatario y estado de lectura.
- **CalendarHolidayRule** (MOD-026): dia inhabil configurado por ano.
- **RegulatoryRule** (MOD-027): norma o articulo versionado, con su estado VIGENTE/FUTURO/DEROGADO/MODIFICADO
  y, para la reforma 659, la bandera ESTADO_ACTUAL/ESTADO_REFORMADO descrita en la seccion 4.
- **HelpTopic** (MOD-028): texto de ayuda contextual ligado a una obligacion o campo.
- **DataSubject** (titular): entidad externa referenciada por PrivacyRequest, Consent, Incident e
  IdentityVerification; nunca se centraliza como base completa de clientes/empleados (privacy by design,
  decision 2.7.21), solo se referencia por caso.

---

## 8. Riesgos del mapa propuesto

Todo lo que sigue es opinion de producto sobre el propio diseno de este mapa (no una obligacion legal), a
menos que se cite un OBL-ID.

1. **El MVP resultante sigue teniendo 20 modulos (13 transversales/nucleo + 7 operativos MUST HAVE), no un
   numero pequeno de forma literal.** Es MVP-PRIMERO en el sentido de que cada modulo tuvo que justificar su
   entrada de forma individual (ver criterio de disciplina en la introduccion), pero el resultado sigue
   siendo un producto con varias piezas moviles porque la ley misma exige varias piezas moviles simultaneas
   (organizacion, delegado, diagnostico, RAT, ARCO-POL, documentos, proveedores, incidentes, controles,
   capacitacion) para que una pyme pueda operar con evidencia desde el primer dia. Mitigacion: la
   experiencia de onboarding (MOD-005/MOD-006/MOD-007) debe ocultar esta complejidad al usuario, mostrando
   un plan secuencial en vez de 20 modulos sueltos.
2. **Diferir Consentimiento, Transferencias y Riesgos/EIPD a V1 puede quedarse corto para segmentos
   especificos desde el dia uno** (marketing digital y e-commerce dependen fuertemente de consentimiento;
   empresas con proveedores cloud extranjeros generan transferencias de inmediato; bancos, clinicas y
   empresas con biometria necesitan EIPD pronto). La cobertura parcial descrita en cada ficha (campo de
   texto libre, tarea manual, plantilla generica) reduce el riesgo pero no lo elimina: un cliente de estos
   segmentos podria sentir el MVP incompleto frente a su necesidad real. Mitigacion: usar el diagnostico
   (MOD-006) para detectar estos perfiles antes de la venta y ser explicito comercialmente sobre que va en
   V1.
3. **El interruptor de estado regulatorio de la reforma 659 (MOD-027) es un unico punto de fallo legal para
   dos modulos MUST HAVE (MOD-003 y MOD-009).** Si se activa de forma incorrecta o prematura (antes de que
   el Diario Oficial confirme la publicacion), toda empresa cliente dejaria de recibir las tareas del
   delegado obligatorio de forma incorrecta. Mitigacion de diseno: el cambio de estado requiere permiso de
   administracion de plataforma (nunca de la empresa cliente) y una verificacion documentada contra el
   Diario Oficial antes de activarse; no existe automatismo por fecha.
4. **Fusionar Inventario, RAT y Mapa de datos en un solo modulo (MOD-008) crea una dependencia muy cargada:**
   es propietario de 11 obligaciones y colaborador de la mayoria de los demas modulos operativos. Si su
   diseno de datos no anticipa bien los campos que RAT, Consentimiento (V1), Transferencias (V1) y
   Riesgos/EIPD (V1) necesitaran leer de el, la llegada de V1 podria forzar cambios estructurales en MOD-008
   pese a la regla de "las capas siguientes no obligan a rediseñar". Mitigacion: los campos que V1 necesitara
   (base juridica = consentimiento, pais de alojamiento del sistema, bandera de alto riesgo) ya existen como
   datos capturables en el MVP (aunque sin motor propio), precisamente para que V1 los active sin agregar
   columnas nuevas al Treatment.
5. **La distincion entre Documento, Evidencia y AuditLog (decision 2.7.4) es conceptualmente correcta pero
   dificil de explicar a un usuario no especialista** ("por que el mismo archivo aparece en dos lugares
   distintos"). Riesgo de UX, no legal. Mitigacion: MOD-023 (Centro de evidencias) debe presentarse siempre
   como una vista consolidada, nunca pidiendole al usuario que entienda la separacion tecnica subyacente.
6. **Clasificar Capacitacion como MUST HAVE solo en su version minima, y Auditoria de cumplimiento y
   Procedimiento sancionador como SHOULD HAVE, asume que ninguna empresa cliente llegara a la plataforma ya
   en medio de un procedimiento sancionador o de cara a una auditoria inminente.** Si el primer segmento de
   clientes reales incluye empresas que ya recibieron un requerimiento de la ACE, el MVP tal como esta
   definido no las atenderia bien el primer dia. Mitigacion: revisar la priorizacion de MOD-020 hacia MUST
   HAVE si la investigacion de mercado (fuera del alcance de esta fase) confirma que este perfil de cliente
   es significativo en los primeros meses.
7. **Portal del titular como SHOULD HAVE (V1) mantiene el ARCO-POL del MVP dependiente de que un empleado
   reciba la solicitud por un canal interno seguro, en vez de un canal publico self-service.** Esto es
   coherente con la decision 2.7.30 de la validacion (la ley exige "mecanismos", no portal), pero es un
   riesgo comercial frente a competidores que si ofrecen portal publico desde el inicio (Sec. 43 del
   maestro, OneTrust, TrustArc y similares). Mitigacion: dejar claro en la venta que el formulario interno
   del MVP ya satisface la obligacion legal, y que el portal publico es una mejora de experiencia, no un
   requisito pendiente.
8. **El numero de decreto de la reforma (659) tiene fuentes contradictorias** (659 y 660 segun distintas
   fuentes secundarias, ver seccion 2.3.1 de la validacion); todo el diseno de la seccion 4 de este documento
   asume que el numero correcto se confirmara junto con la publicacion oficial. Si el numero de decreto
   cambia, el mecanismo de la bandera de estado no cambia, pero toda referencia textual a "Decreto 659" en
   la plataforma (etiquetas, ayuda contextual) tendria que corregirse.
9. **Este documento no resuelve, y no debe resolver, las incertidumbres juridicas genuinas identificadas en
   `02_validacion_de_la_idea.md`** (computo de 72 horas en horas corridas vs habiles, si la prevencion
   suspende el plazo de 20 dias, transferencia vs. acceso del encargado extranjero, edad de consentimiento
   de menores). El mapa de modulos asume los criterios conservadores por defecto que ya fijo la validacion,
   pero un cambio de criterio por parte de la ACE o de un abogado consultado podria alterar el
   comportamiento esperado de MOD-009, MOD-012 y MOD-015 sin cambiar la estructura de modulos en si.

