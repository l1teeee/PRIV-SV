# MODULO: Controles de Seguridad

Codigo corto del modulo: MOD-015
Clasificacion global del modulo: MUST HAVE
Obligaciones que cubre: OBL-SEG-01, OBL-SEG-02, OBL-SEG-03, OBL-SEG-04, OBL-SEG-05, OBL-SEG-06, OBL-SENS-05 (propietarias); OBL-PRIN-03, OBL-PROV-03 (colaboradoras, con propietario en otro modulo)

---

## A. Proposito

- **Por que existe.** La Ley para la Proteccion de Datos Personales (LPDP, Decreto Legislativo 144) remite en su Art. 35 a las Politicas de Actuacion y Manejo de Datos Personales que dicta la ACE, y esas Politicas (N. 001-0309025-DPDP, Art. 4) enumeran un catalogo cerrado de medidas organizativas, tecnicas y fisicas que toda empresa privada sujeta a la ley debe tener implementadas. Ninguna otra parte del sistema tiene como funcion propia decidir, registrar y probar que esas medidas existen: ese es el proposito exclusivo de MOD-015.
- **Que problema resuelve para la empresa.** Convierte una lista de exigencias tecnicas dispersas en las Politicas ACE (2FA, cifrado, backups, firewall, pentesting, destruccion segura, etc.) en un catalogo unico, con responsable, evidencia, vigencia y estado, de modo que la persona designada (tipicamente el perfil de TI o de seguridad, no necesariamente el Delegado) pueda demostrar en cualquier momento, ante una auditoria interna o ante un requerimiento de la ACE, que cada medida existe y desde cuando.
- **Que obligacion u obligaciones cubre (IDs y articulos).**
  - OBL-SEG-01, Art. 35 LPDP: caracter imperativo de las Politicas de Actuacion de la ACE.
  - OBL-SEG-02, Art. 4 Medidas Organizativas (lit. a-f) de las Politicas ACE: Politica de Proteccion de Datos, Delegado/Responsable Interno, capacitacion, RAT, EIPD y auditorias como medidas organizativas minimas.
  - OBL-SEG-03, Art. 4 Medidas Tecnicas de las Politicas ACE: control de acceso con 2FA, cifrado en reposo y en transito, gestion de identidades, backups, firewall/antivirus/IDS-IPS, analisis de vulnerabilidades y pentesting, y digitalizacion mediante sistemas especializados.
  - OBL-SEG-04, Art. 4 (bloque de Medidas de Seguridad en Transferencias de Datos) y Art. 6 lit. d) de las Politicas ACE: SSL/TLS, contratos de confidencialidad y de transferencia, transferencias solo a paises con proteccion equivalente, notificacion de brechas en 72 horas.
  - OBL-SEG-05, Art. 4 Medidas Fisicas lit. e) de las Politicas ACE: eliminacion segura de documentos fisicos y borrado seguro de dispositivos.
  - OBL-SEG-06, Art. 56 lit. b num. 5 y 7 LPDP: no implementar las medidas, controles o lineamientos de la ACE es infraccion grave (11 a 25 salarios minimos del sector comercio).
  - OBL-SENS-05, Art. 59 LPDP: prohibiciones sobre datos sensibles y comercializacion indebida; el catalogo de controles es donde la empresa deja evidencia de la politica interna que sanciona estas conductas.
  - Colabora con OBL-PRIN-03 (Art. 5 lit. i, responsabilidad demostrada), cuyo modulo propietario es MOD-019 Centro de Evidencias: MOD-015 es una de las fuentes principales de esa evidencia.
  - Colabora con OBL-PROV-03 (Art. 36, medidas de seguridad tambien obligatorias para el encargado), cuyo modulo propietario es MOD-009 Proveedores y Encargados: MOD-015 provee el catalogo y el formato con el que un proveedor puede acreditar sus propios controles.
- **Que valor aporta.**
  - Operativo: un solo lugar donde la persona de TI o de seguridad (que rara vez es la misma que entiende la ley) sabe exactamente que debe tener implementado y en que estado esta.
  - Probatorio: es la fuente de evidencia especifica para el bloque de infracciones graves del Art. 56 lit. b num. 5 y 7, el mas caro de todo el catalogo sancionador despues de las infracciones muy graves.
  - De reduccion de riesgo: conecta directamente cada control con el riesgo sancionador que cubre, sin que la empresa tenga que interpretar por si misma la ley para saber que tan expuesta esta.
- **Que NO hace este modulo (limites explicitos).**
  - No ejecuta, instala, configura ni administra ningun control tecnico real (no activa 2FA, no cifra nada, no corre un antivirus ni un escaner de vulnerabilidades). Solo registra que el control existe, quien lo administra y que evidencia lo prueba.
  - No es un SIEM, un antivirus, un gestor de parches ni una herramienta de monitoreo de seguridad en tiempo real (anti-feature 2 y 11 de `22_anti_features.md`).
  - No certifica ni garantiza que un control sea tecnicamente adecuado o suficiente frente a una amenaza real; esa es una decision de seguridad informatica que corresponde al responsable de TI de la empresa o a un proveedor especializado.
  - No declara que la empresa "cumple" con las medidas de seguridad de la ACE; solo muestra estado del catalogo (controles con evidencia vigente, vencidos, sin evidencia).
  - No decide si el incumplimiento de un control concreto configura la infraccion grave del Art. 56 lit. b; eso es una calificacion que corresponde a la ACE en un procedimiento sancionador, y el sistema lo dice de forma explicita.

### Nota sobre el doble estado de la reforma 659 en este modulo

Segun el mapa definitivo (`06_mapa_definitivo_de_modulos.md`), la nota de reforma 659 de MOD-015 dice "No aplica directamente", y en efecto la inmensa mayoria del catalogo (medidas tecnicas y fisicas, OBL-SEG-03 a 06, OBL-SENS-05) proviene de las Politicas ACE (Art. 4 y 35) y del catalogo de infracciones (Art. 56), normas que la reforma 659 no toca segun ninguna fuente disponible. Sin embargo hay un matiz que este modulo si debe reflejar: una de las seis medidas organizativas minimas del Art. 4 (OBL-SEG-02) es literalmente "tener un Delegado de Proteccion de Datos". Mientras el estado normativo del Centro Regulatorio (MOD-024) sea ACTUAL, ese item del catalogo de controles organizativos se llama "Delegado de Proteccion de Datos designado" y es OBLIGATORIO. Si el estado FUTURO se activa alguna vez, ese mismo item debe pasar a llamarse "Responsable interno del programa de datos designado" y a mostrarse como buena practica recomendada en vez de obligatorio, igual que ya ocurre con la figura completa en MOD-002 (ver `05_tipos_de_usuario.md`, seccion 5.2). El resto del catalogo de MOD-015 no cambia de nombre ni de obligatoriedad con el cambio de estado.

---

## B. Usuarios

| Rol estandar | Para que usa este modulo |
|---|---|
| Administrador de la organizacion | Da de alta el catalogo inicial de controles al configurar la organizacion, asigna el rol Responsable de Seguridad/IT y, en pyme, puede ser quien registre y apruebe controles el mismo (con advertencia de autorrevision, ver seccion C) |
| Delegado de Proteccion de Datos (o Responsable interno en estado FUTURO) | Consulta el catalogo para citar el estado de las medidas de seguridad en su informe periodico al responsable y para responder consultas de la ACE sobre estas medidas; no suele registrar evidencia tecnica el mismo, salvo en pyme donde acumula el rol |
| Responsable ARCO-POL / Responsable del tramite | No usa este modulo de forma directa; solo lo consulta de forma indirecta cuando necesita citar una medida de seguridad como parte del fundamento de una respuesta ARCO-POL |
| Responsable Legal / Compliance | Revisa que la justificacion de una excepcion sea razonable antes de aprobarla, y usa el catalogo como evidencia al preparar la posicion de la empresa ante un requerimiento de la ACE relacionado con el Art. 56 lit. b |
| Responsable de Seguridad / IT | Usuario principal del modulo: crea, actualiza, adjunta evidencia, marca estados, gestiona las fechas de revision de cada control |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Consulta que controles aplican a un sistema o tratamiento de su area (por ejemplo, el lector biometrico de RRHH) y puede ser asignado como colaborador de una tarea puntual (por ejemplo, coordinar con el proveedor la destruccion certificada de expedientes fisicos) |
| Aprobador | Aprueba las excepciones (controles marcados "No aplica / Exceptuado") y, si la empresa lo configura, aprueba el paso de un control critico a estado Implementado antes de considerarlo vigente |
| Auditor (interno) | Solo lectura: revisa el estado del catalogo y descarga evidencia como parte de la auditoria anual de cumplimiento (MOD-018); no crea ni aprueba controles |
| Auditor externo (invitado) | Acceso temporal de solo lectura al catalogo y a la evidencia adjunta, durante la ventana de la auditoria anual sustantiva |
| Usuario de consulta / Colaborador | Ejecuta una tarea puntual que el modulo genero (por ejemplo, "renovar el certificado de destruccion segura con el proveedor X"), sin acceso al resto del catalogo |
| Titular externo | No aplica: este modulo no interactua nunca con titulares de datos, solo con informacion organizativa y tecnica interna |
| Asesor externo invitado | Acceso puntual y acotado cuando se le invita a dictaminar sobre un control especifico en disputa (por ejemplo, un consultor de seguridad que valida un reporte de pentest presentado como evidencia) |

---

## C. Permisos

| Accion | Administrador | Delegado / Resp. interno | Resp. Legal/Compliance | Resp. Seguridad/IT | Resp. de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Asesor externo invitado |
|---|---|---|---|---|---|---|---|---|---|---|
| Ver catalogo completo | Si | Si | Si | Si | Solo controles de su area | Si | Si (lectura) | Si (lectura, temporal) | No | Solo el control asignado |
| Crear control | Si | No | No | Si | No | No | No | No | No | No |
| Modificar control | Si | No | No | Si | No | No | No | No | No | No |
| Marcar "Implementado" | Si | No | No | Si | No | Si (si el control lo exige, ver F) | No | No | No | No |
| Aprobar excepcion ("No aplica") | Si (con advertencia si el mismo la creo) | No | Si | No | No | Si | No | No | No | No |
| Cerrar / archivar control | Si | No | No | Si | No | No | No | No | No | No |
| Eliminar control | No (solo archivar; ver anti-feature 19, sin borrado de historial) | No | No | No | No | No | No | No | No | No |
| Exportar checklist / paquete de evidencia | Si | Si | Si | Si | No | No | Si | Si (solo lo compartido con el) | No | No |
| Asignar tarea derivada | Si | No | No | Si | No | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | Si (en controles de su area) | Si | Si | Si | Si (en su tarea) | Si (en el control asignado) |
| Adjuntar evidencia | Si | No | No | Si | Si (si se le asigna la tarea) | No | No | No | Si (en su tarea) | Si (en el control asignado) |

Separacion de funciones: quien crea o adjunta la evidencia de un control no deberia ser la unica persona que lo aprueba cuando ese control es una excepcion (estado "No aplica / Exceptuado"), porque una excepcion mal justificada es la puerta de entrada mas directa al riesgo de infraccion grave del Art. 56 lit. b (OBL-SEG-06). Por eso "Aprobar excepcion" exige el rol Aprobador, distinto del rol que creo el control, salvo en pyme por debajo del umbral configurable de tamano (ver `05_tipos_de_usuario.md`, seccion 5.4), donde el sistema permite la acumulacion mostrando siempre la advertencia de autorrevision. Marcar un control como "Implementado" no exige doble control por defecto, salvo que la empresa configure ese doble control para controles que ella misma marque como criticos (por ejemplo, cifrado de la base de datos principal); esta configuracion es [opinion de producto], no una exigencia legal.

---

## D. Informacion de entrada

Entidad central: **Control** (entidad compartida con MOD-014 Riesgos y EIPD segun la decision 2.7.3 de `02_validacion_de_la_idea.md`: MOD-015 es propietario del catalogo, MOD-014 selecciona o crea controles de este mismo catalogo, nunca mantiene una lista paralela).

| Campo | Tipo | Obligatorio u opcional | Opciones o catalogo | Validacion | Texto de ayuda para el usuario | Fundamento |
|---|---|---|---|---|---|---|
| Nombre del control | Texto corto | Obligatorio | - | No vacio; maximo 120 caracteres | "Ponle un nombre corto y claro, por ejemplo: Autenticacion en dos pasos para el sistema de nomina." | Buena practica |
| Categoria | Seleccion unica | Obligatorio | Organizativa / Tecnica / Fisica | Debe elegir una | "Organizativa: una politica o una responsabilidad interna. Tecnica: una herramienta o configuracion informatica. Fisica: algo sobre espacios, papel o equipos." | OBL-SEG-02, OBL-SEG-03, OBL-SEG-05 (Art. 4 Politicas ACE) |
| Tipo de control (subcategoria) | Seleccion unica, catalogo dependiente de la categoria elegida | Obligatorio | Ver catalogo detallado abajo | Debe pertenecer a la categoria elegida; opcion "Otro" habilita un campo de texto libre | "Elige el tipo mas parecido a lo que ya tienes o vas a implementar." | OBL-SEG-02 / OBL-SEG-03 / OBL-SEG-05 segun el tipo |
| Ambito de aplicacion | Referencia multiple a Sistema o Tratamiento (MOD-006), u opcion "Toda la organizacion" | Obligatorio antes de marcar "Implementado" | Lista de sistemas/tratamientos vivos del RAT | Al menos un valor | "Indica a que sistema o proceso aplica este control. Si protege a toda la empresa por igual (por ejemplo, la politica de contrasenas), elige Toda la organizacion." | Buena practica; apoya OBL-PRIN-03 |
| Responsable del control | Referencia a usuario | Obligatorio | Usuarios activos de la organizacion (tipicamente rol Responsable de Seguridad/IT) | Debe tener un rol habilitado en el sistema | "Quien en tu empresa (o en el proveedor de TI que te apoya) es responsable de que este control siga funcionando." | Buena practica |
| Estado | Seleccion unica | Obligatorio (valor inicial: Pendiente de implementar) | Pendiente de implementar / Implementado / Implementado con hallazgo / Vencido / No aplica - Exceptuado / Archivado | Solo transiciones permitidas por el flujo de la seccion F | "Este es el semaforo del control: en que punto esta." | OBL-SEG-06 vincula el estado al riesgo de infraccion grave |
| Descripcion / alcance | Texto largo | Opcional (recomendado) | - | Maximo 2000 caracteres | "Explica en una o dos frases que hace este control y por que lo tienes asi." | Buena practica |
| Evidencia de implementacion | Archivo adjunto (uno o varios) o referencia a un documento de MOD-008 | Obligatorio para pasar a Implementado | Formatos comunes: PDF, imagen, hoja de calculo, documento | Al menos un archivo o una referencia de documento | "Sube algo que demuestre que el control existe: una captura de la configuracion, un contrato, un certificado, un reporte." | OBL-PRIN-03; especifico segun OBL-SEG-01 a 06 |
| Fecha de implementacion | Fecha | Obligatorio al marcar Implementado | - | No puede ser una fecha futura | "Desde cuando esta funcionando este control." | Buena practica |
| Periodicidad de revision | Seleccion unica | Obligatorio | Mensual / Trimestral / Semestral / Anual / Segun evento | Debe elegir una | "Cada cuanto tiempo hay que volver a comprobar que este control sigue vigente. Por ejemplo, un pentest suele revisarse una vez al ano; un backup, cada mes." | Buena practica (la ACE no fija periodicidad, salvo la auditoria anual; ver ambiguedad 2 de `03_hallazgos_regulatorios.md`, seccion 8) |
| Proxima fecha de revision | Fecha (calculada, editable) | Autogenerado a partir de fecha de implementacion + periodicidad | - | Si se edita manualmente, exige un motivo | "El sistema te avisara antes de esta fecha para que renueves la evidencia." | Buena practica |
| Proveedor externo asociado | Referencia a MOD-009 Proveedores y Encargados | Opcional | Proveedores registrados de la organizacion | - | "Si un proveedor externo te ayuda con este control (por ejemplo, la empresa que hace tu pentest o destruye tus documentos), enlazalo aqui." | OBL-PROV-03 |
| Sistema o activo asociado | Referencia a Sistema (MOD-006) | Opcional, recomendado en controles tecnicos | Catalogo de sistemas de la organizacion | - | "Si el control aplica a un sistema concreto (por ejemplo, el ERP), indicalo para que el RAT muestre este control junto al tratamiento." | Buena practica |
| Justificacion de no implementacion | Texto largo | Obligatorio si Estado = No aplica - Exceptuado | - | Minimo 100 caracteres | "Explica por que este control no aplica a tu empresa. Recuerda que no implementar un control sin buena razon documentada es una infraccion grave (multa de 11 a 25 salarios minimos)." | OBL-SEG-06 |
| Aprobador de la excepcion | Referencia a usuario con rol Aprobador | Obligatorio si Estado = No aplica - Exceptuado | Usuarios con rol Aprobador de la organizacion | Distinto del usuario que creo la excepcion, salvo pyme (ver seccion C) | "Una segunda persona debe revisar y aprobar esta excepcion antes de que quede registrada." | Buena practica de separacion de funciones (ver 5.4) |
| Nivel de riesgo si no se implementa | Seleccion unica | Opcional (recomendado si hay excepcion) | Bajo / Medio / Alto | - | "Este es tu propio calculo interno de que tan riesgoso es no tener este control; no es una calificacion legal." | [Opinion de producto] apoya la vista de riesgo sancionador de OBL-SEG-06 |
| Notas internas | Texto largo | Opcional | - | - | "Cualquier anotacion interna que quieras dejar sobre este control." | - |

Catalogo detallado de "Tipo de control" segun categoria (Art. 4 de las Politicas ACE):

- Organizativa: Politica de Proteccion de Datos; Delegado de Proteccion de Datos / Responsable interno designado; Capacitacion del personal; Registro de Actividades de Tratamiento (RAT); Evaluaciones de Impacto en la Privacidad (EIPD); Auditorias de cumplimiento; Otro.
- Tecnica: Contrasenas seguras y control de acceso; Autenticacion en dos pasos (2FA); Cifrado en reposo; Cifrado en transito; Gestion de identidades y accesos; Copias de respaldo (backups); Firewall / antivirus / IDS-IPS; Analisis de vulnerabilidades; Pentesting; Digitalizacion mediante sistema especializado (OBL-SEG-03, Art. 4 lit. g); Protocolo de comunicacion segura (SSL/TLS) para transferencias (OBL-SEG-04); Otro.
- Fisica: Eliminacion segura de documentos fisicos (trituracion); Borrado seguro de dispositivos electronicos; Seguridad fisica de instalaciones (control de acceso a oficinas, resguardo de servidores locales); Otro.

Campos precargados: al completar el diagnostico inicial (MOD-004), el sistema crea automaticamente en estado "Pendiente de implementar" los controles del catalogo base (las seis medidas organizativas mas los items tecnicos y fisicos mas comunes), como plantilla inicial, no como controles ya marcados implementados. Cuando MOD-014 (Riesgos y EIPD) necesita un control que no existe todavia en este catalogo para cubrir una EIPD, crea aqui un nuevo registro en "Pendiente de implementar" con el ambito de aplicacion precargado desde el tratamiento evaluado, sin duplicar la entidad Control (decision 2.7.3).

Minimizacion de datos personales: este modulo no almacena ni deberia almacenar datos personales de titulares del cliente bajo ninguna circunstancia; su contenido es exclusivamente informacion organizativa y tecnica (nombre del control, sistema, proveedor, responsable interno por referencia a su usuario). El unico dato de persona natural que aparece es el nombre del empleado interno responsable del control, tratado igual que en cualquier otro modulo que asigna una tarea a un usuario (referencia al User de MOD-001, no una copia de datos del titular). No se preven campos que capturen datos sensibles, biometricos o de salud; si un archivo de evidencia adjunto llegara a contener datos personales de forma incidental (por ejemplo, una captura de pantalla de un sistema con nombres visibles), el texto de ayuda del campo "Evidencia de implementacion" debe advertir que se recorten o tapen esos datos antes de subir el archivo.

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Catalogo consolidado de controles | Lista de todos los controles con categoria, tipo, estado, responsable y proxima revision | Vista en pantalla, exportable a XLSX | Siempre disponible, se actualiza en tiempo real | Responsable de Seguridad/IT, Administrador, Delegado, Auditor |
| Indicador "Controles con evidencia vigente" | Porcentaje de controles aplicables en estado Implementado sobre el total de controles no archivados | Indicador de dashboard (MOD-020) | Recalculado en cada cambio de estado | Gerencia, Responsable de Seguridad/IT, Legal/Delegado |
| Indicador "Controles obligatorios sin evidencia o vencidos" | Numero de controles OBLIGATORIO (todo el catalogo base de OBL-SEG-01 a 06) sin evidencia vigente | Indicador de dashboard, vinculado a riesgo sancionador grave | Recalculado en cada cambio de estado | Gerencia, Legal/Delegado, Responsable de Seguridad/IT |
| Tarea de revision periodica | "Revisar y renovar evidencia del control X" | Tarea en MOD-021 | Cuando falta N dias configurables para la proxima fecha de revision | Responsable del control |
| Tarea de excepcion pendiente | "Aprobar o rechazar la excepcion del control X" | Tarea en MOD-021 | Al registrarse una excepcion | Usuario con rol Aprobador |
| Alerta de vencimiento | Ver tabla de la seccion I | Notificacion (MOD-022) | Segun disparador de cada alerta | Responsable de Seguridad/IT, Delegado, Aprobador segun el caso |
| Evidencia formal | Archivo con hash, fecha, version y responsable | Paquete verificable (MOD-019) | Cada vez que se adjunta o reemplaza evidencia | Centro de Evidencias (consumo interno del sistema) |
| Checklist exportable | Catalogo completo filtrado por categoria, estado o responsable | PDF o XLSX | Bajo demanda | Responsable de Seguridad/IT, Auditor, Auditor externo |
| Bandera de riesgo sancionador | Marca visible cuando un control OBLIGATORIO del catalogo base queda sin evidencia o vencido | Indicador cualitativo en la vista de riesgo del modulo y del dashboard Legal | Al cambiar el estado a Vencido o al vencer el plazo de revision sin renovar | Legal/Delegado, Gerencia |
| Evento de auditoria (AuditLog) | Quien hizo que cambio, cuando | Registro tecnico inmutable | En cada creacion, cambio de campo, cambio de estado, aprobacion o archivado | Consultado por MOD-018 y MOD-019 |

---

## F. Workflow

```
                     crear control
                          |
                          v
              +---------------------------+
              | PENDIENTE DE IMPLEMENTAR  |
              +---------------------------+
                 |                      |
                 | registrar evidencia  | marcar como excepcion
                 | y marcar implementado| (con justificacion)
                 v                      v
        +------------------+   +---------------------------+
        |  IMPLEMENTADO    |   | NO APLICA / EXCEPTUADO     |
        +------------------+   +---------------------------+
           |        ^                    |
           |        | evidencia          | aprobador rechaza
           |        | renovada y         | la excepcion
llega fecha|        | aprobada           v
de revision|        |          (vuelve a PENDIENTE DE IMPLEMENTAR)
           v        |
        +------------------+
        |   EN REVISION    |
        +------------------+
           |        |
   revision|        | revision detecta
   sin     |        | un hallazgo menor
 hallazgos |        v
           |   +---------------------------+
           |   | IMPLEMENTADO CON HALLAZGO |
           |   +---------------------------+
           |             |
           |             | se corrige el hallazgo
           |             | y se aprueba
           |             v
           +---------> IMPLEMENTADO (reinicia contador de revision)

        (desde EN REVISION, si vence el plazo sin que nadie revise)
                          |
                          v
                    +-----------+
                    |  VENCIDO  |
                    +-----------+
                          |
                          | se retoma la revision
                          v
              IMPLEMENTADO o IMPLEMENTADO CON HALLAZGO

  Desde IMPLEMENTADO, IMPLEMENTADO CON HALLAZGO, NO APLICA - EXCEPTUADO
  o VENCIDO, en cualquier momento:
                          |
                          | archivar (control descontinuado,
                          | por ejemplo el sistema que protegia
                          | dejo de usarse)
                          v
                    +-----------+
                    | ARCHIVADO |
                    +-----------+
                          |
                          | reactivar
                          v
              PENDIENTE DE IMPLEMENTAR
```

Tabla de transiciones:

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (nuevo) | Crear control | Categoria y tipo obligatorios | Pendiente de implementar | Administrador, Responsable de Seguridad/IT | Evento de creacion en AuditLog; si viene de MOD-014, hereda ambito precargado |
| Pendiente de implementar | Registrar evidencia y marcar Implementado | Evidencia adjunta, ambito y fecha de implementacion completos | Implementado | Administrador, Responsable de Seguridad/IT (Aprobador si la empresa exige doble control para ese control) | Evidencia queda en MOD-019; se calcula la proxima fecha de revision; evento en AuditLog |
| Pendiente de implementar | Marcar como excepcion | Justificacion de minimo 100 caracteres | No aplica - Exceptuado | Administrador, Responsable de Seguridad/IT | Se crea tarea de aprobacion para el rol Aprobador; se muestra advertencia de riesgo sancionador |
| No aplica - Exceptuado | Aprobar la excepcion | Aprobador distinto de quien la creo (salvo pyme con advertencia) | No aplica - Exceptuado (queda vigente) | Aprobador | Evento de aprobacion en AuditLog; entra al indicador de "excepciones activas" del dashboard |
| No aplica - Exceptuado | Rechazar la excepcion | Debe indicar motivo | Pendiente de implementar | Aprobador | Se reabre la tarea original con el motivo de rechazo visible |
| Implementado | Llega la proxima fecha de revision | Automatico, segun periodicidad configurada | En revision | Sistema (automatico); la accion de revisar la ejecuta el Responsable de Seguridad/IT | Se crea tarea de revision en MOD-021 y alerta INFO/WARNING segun cercania |
| En revision | Confirmar evidencia vigente sin hallazgos | Evidencia revisada y, si corresponde, actualizada | Implementado | Responsable de Seguridad/IT | Reinicia el contador de proxima revision; evento en AuditLog |
| En revision | Registrar un hallazgo menor | Descripcion del hallazgo obligatoria | Implementado con hallazgo | Responsable de Seguridad/IT | Se crea tarea de correccion; alerta WARNING al Responsable Legal/Compliance si el hallazgo afecta un control OBLIGATORIO |
| En revision | Vence el plazo sin que nadie revise | Automatico, sin accion humana | Vencido | Sistema (automatico) | Alerta HIGH; sube el indicador de riesgo sancionador si el control es OBLIGATORIO |
| Implementado con hallazgo | Corregir el hallazgo y aprobar | Evidencia de la correccion adjunta | Implementado | Responsable de Seguridad/IT (o Aprobador si la empresa lo exige) | Reinicia el contador de revision; evento en AuditLog |
| Vencido | Retomar la revision | Igual que "En revision" | Implementado o Implementado con hallazgo | Responsable de Seguridad/IT | Baja el indicador de riesgo sancionador si el control vuelve a Implementado |
| Cualquier estado no terminal | Archivar | Motivo de archivado obligatorio | Archivado | Administrador, Responsable de Seguridad/IT | El control deja de contar en los indicadores del dashboard; historial permanece intacto (no se borra, ver anti-feature 19) |
| Archivado | Reactivar | Motivo de reactivacion obligatorio | Pendiente de implementar | Administrador | Evento de reapertura en AuditLog; el control retoma su ciclo desde cero |

Estados terminales: Archivado es el unico estado terminal, y admite reapertura explicita con motivo (no hay borrado real de ningun control ni de su historial, en linea con el anti-feature 19 sobre la bitacora de auditoria). Los controles vinculados desde MOD-014 (EIPD) que se archivan quedan visibles como referencia historica dentro de la EIPD correspondiente, sin que su archivado elimine la evidencia ya citada en un expediente cerrado.

---

## G. Automatizaciones

| Disparador | Condicion | Accion | Configurable por la empresa |
|---|---|---|---|
| Se completa el diagnostico inicial (MOD-004) | Primera vez que la organizacion define su alcance | Crea el catalogo base de controles en "Pendiente de implementar" segun el catalogo de la seccion D | No (el catalogo base es fijo; la empresa puede archivar los que no le apliquen despues) |
| MOD-014 necesita un control para una EIPD que no existe en el catalogo | El control seleccionado no tiene equivalente en MOD-015 | Crea un nuevo registro en Pendiente de implementar con el ambito precargado desde el tratamiento de la EIPD | No |
| Se marca Implementado | Evidencia adjunta y fecha de implementacion validas | Calcula la proxima fecha de revision (fecha de implementacion + periodicidad) | Si (la periodicidad por tipo de control es editable) |
| Faltan N dias para la proxima fecha de revision | N configurable (por defecto 30, 15 y 7 dias) | Crea tarea de revision en MOD-021 y dispara alerta segun tabla de la seccion I | Si (dias de anticipacion) |
| Vence la fecha de revision sin accion | Estado seguia en "En revision" o "Implementado" sin confirmarse | Cambia el estado a Vencido y sube el indicador de riesgo sancionador si el control es OBLIGATORIO | No (el cambio de estado es automatico; la empresa solo configura los dias de anticipacion previos) |
| Se registra una excepcion | Estado pasa a No aplica - Exceptuado | Crea tarea de aprobacion para el rol Aprobador y muestra la advertencia de riesgo sancionador | No |
| Se adjunta o reemplaza un archivo de evidencia | Cualquier estado | Calcula el hash del archivo y lo registra en MOD-019 con fecha, version y usuario | No |
| Se aprueba el paso a Implementado de un control marcado como critico por la empresa | Solo si la empresa activo "doble control" para ese control | Bloquea el cambio de estado hasta que un usuario con rol Aprobador distinto lo confirme | Si (que controles se marcan como criticos) |
| Un nuevo sistema o tratamiento se da de alta en el RAT (MOD-006) con categoria de dato sensible o con transferencia internacional marcada | El sistema detecta la senal desde MOD-006 o MOD-010 | Sugiere (no fuerza) vincular ese sistema a los controles tecnicos y del bloque de transferencias ya existentes en el catalogo | No (es una sugerencia visible, no una accion automatica) |

---

## H. Decisiones que NO debe automatizar

- **Si un control implementado es tecnicamente suficiente o adecuado frente al riesgo real.** El sistema registra que existe evidencia de un control (por ejemplo, "hay cifrado en transito"), pero no puede evaluar si esa implementacion tecnica especifica es robusta o esta bien configurada; eso exige criterio de un especialista en seguridad informatica. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada."
- **Si no implementar un control concreto constituye la infraccion grave del Art. 56 lit. b.** El sistema vincula el estado de un control con el riesgo sancionador descrito en la ley, pero calificar si un caso puntual configura o no esa infraccion es una decision que corresponde exclusivamente a la ACE en un procedimiento sancionador. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada."
- **Si la justificacion de una excepcion es razonable.** El sistema exige el campo y la aprobacion de un segundo usuario, pero no evalua por si mismo si el argumento de la empresa para no implementar un control es aceptable; esa evaluacion la hace el Aprobador humano, idealmente con apoyo de Legal/Compliance. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada."
- **Si un proveedor externo de seguridad (pentesting, destruccion certificada) es idoneo.** El sistema solo registra el contrato o certificado como evidencia; la eleccion y evaluacion del proveedor es una decision comercial y tecnica de la empresa. Texto de advertencia: "Requiere validacion de la organizacion."
- **Si un dato dentro de un archivo de evidencia adjunto es en si mismo un dato sensible o personal que no deberia haberse subido.** El sistema advierte en el texto de ayuda del campo, pero no analiza automaticamente el contenido de los archivos adjuntos para detectar datos personales, porque eso excederia el proposito de este modulo y crearia una falsa sensacion de filtro automatico de privacidad. Texto de advertencia: "Revise que este archivo no contenga datos personales innecesarios antes de subirlo."

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia o repeticion | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Proxima revision de un control | Faltan 30 dias para la proxima fecha de revision | INFO | Responsable del control | Plataforma | Una vez | No escala | Se confirma la revision o cambia el estado |
| Revision urgente de un control | Faltan 7 dias para la proxima fecha de revision | WARNING | Responsable del control | Plataforma y correo | Cada 3 dias hasta la fecha | Si no hay respuesta en 5 dias, notifica tambien al Administrador | Se confirma la revision o cambia el estado |
| Control vencido | El estado cambia automaticamente a Vencido | HIGH | Responsable del control, Delegado/Responsable interno | Plataforma y correo | Diaria mientras siga Vencido | Si sigue Vencido mas de 15 dias, escala a Legal/Delegado y a Gerencia | El control vuelve a Implementado o Implementado con hallazgo |
| Control obligatorio sin evidencia | Un control del catalogo base (OBL-SEG-01 a 06) permanece en Pendiente de implementar mas de 30 dias desde su creacion | HIGH | Responsable de Seguridad/IT, Delegado/Responsable interno | Plataforma y correo | Semanal | Si sigue sin evidencia a los 60 dias, escala a Gerencia con la referencia expresa al riesgo de infraccion grave (OBL-SEG-06) | Se marca Implementado o se registra una excepcion aprobada |
| Excepcion pendiente de aprobacion | Se registra una excepcion | WARNING | Usuario con rol Aprobador | Plataforma | Cada 3 dias hasta que se resuelva | Si no se resuelve en 10 dias, escala al Administrador | Se aprueba o se rechaza la excepcion |
| Hallazgo detectado en revision | Un control pasa a Implementado con hallazgo | WARNING | Responsable del control, Responsable Legal/Compliance si el control es OBLIGATORIO | Plataforma | Una vez, mas recordatorio semanal mientras el hallazgo siga abierto | Si el hallazgo sigue abierto mas de 30 dias y el control es OBLIGATORIO, escala a Gerencia | Se corrige el hallazgo y se aprueba el retorno a Implementado |

---

## J. Evidencia

| Que genera o conserva | Como | Obligacion que prueba (OBL-ID) | Conservacion |
|---|---|---|---|
| Archivo de evidencia de implementacion (captura, contrato, certificado, reporte) | Adjunto con hash calculado al subirse, version y fecha | OBL-SEG-01 a 06 segun el control especifico; OBL-PRIN-03 de forma transversal | Mientras el control siga activo o archivado; conservacion documental de cumplimiento propio conforme a las reglas del motor de retencion documental cuando ese modulo (MOD-016) este disponible; hasta entonces, conservacion indefinida con opcion manual de archivado |
| Historial de estados de cada control (quien cambio que y cuando) | Registro inmutable en AuditLog | OBL-PRIN-03 | Igual que el archivo de evidencia asociado |
| Aprobacion de una excepcion | Registro con identidad del Aprobador, fecha y justificacion | OBL-SEG-06 (evidencia de que la no implementacion fue una decision documentada, no un simple incumplimiento) | Igual que el control asociado |
| Vinculacion de un control al proveedor que lo ejecuta (por ejemplo, la empresa de pentesting) | Referencia a la ficha del proveedor en MOD-009 | OBL-PROV-03 | Mientras dure la relacion con el proveedor, mas el periodo de conservacion documental aplicable |
| Checklist exportado (paquete de evidencia de seguridad) | Exportacion con verificacion de integridad (hash o firma) segun la decision 2.7.24 | OBL-PRIN-03 | Se conserva el registro de que se genero la exportacion (quien, cuando), no necesariamente el archivo exportado en si, que vive en MOD-019 |
| Registro de accesos de lectura a evidencia tecnica sensible (por ejemplo, un reporte de pentest) | Registro de quien la consulto y cuando | [Opinion de producto, buena practica de seguridad, no exigida expresamente por la LPDP] | Igual que el archivo consultado |

---

## K. Documentos asociados

- **Documentos requeridos como entrada:** contrato o certificado del proveedor de pentesting o analisis de vulnerabilidades; constancia o contrato de destruccion certificada de documentos y dispositivos; la version vigente de la Politica de Seguridad de la Informacion, si la empresa la mantiene como documento independiente dentro de MOD-008.
- **Documentos generados:** este modulo no redacta borradores de politicas ni de contratos (esa funcion vive en MOD-008 Documentos y Politicas); MOD-015 solo referencia el documento vigente de MOD-008 cuando el control organizativo correspondiente es, por ejemplo, "Politica de Proteccion de Datos".
- **Plantillas que el sistema provee:**
  - "Checklist de medidas organizativas, tecnicas y fisicas" (catalogo base de la seccion D), marcado explicitamente como "criterio propio del producto, no un formato oficial de la ACE", en linea con la ambiguedad 2 de `03_hallazgos_regulatorios.md`, seccion 8, porque las Politicas ACE no fijan formato ni contenido minimo exacto para cada medida.
  - Estas plantillas no requieren aprobacion legal para usarse como checklist interno, pero cualquier documento redactado a partir de ellas (por ejemplo, una politica de seguridad completa) si requiere revision y aprobacion de la organizacion antes de publicarse, conforme al texto de descargo estandar de `04_objetivo_exacto_del_producto.md`, seccion 1.3.
- **Anexos y evidencias documentales:** reportes de pentest y de analisis de vulnerabilidades, bitacoras de backup, capturas de configuracion de 2FA o de cifrado, constancias de destruccion, contratos de confidencialidad y de transferencia (estos ultimos tambien referenciados desde MOD-010).

---

## L. Dependencias

```
MOD-006 RAT y Mapa de Datos --------+
                                     |
MOD-010 Transferencias Int. --------+---> MOD-015 Controles de Seguridad
        (SHOULD HAVE)                              |
                                                     +---> MOD-013 Incidentes de Seguridad
                                                     +---> MOD-014 Riesgos y EIPD
                                                     |       (entidad Control compartida,
                                                     |        no duplicada; decision 2.7.3)
                                                     +---> MOD-018 Auditoria de Cumplimiento
                                                     +---> MOD-019 Centro de Evidencias

     Capa transversal (consultada, nunca consulta al reves):
     MOD-001 Organizacion (identidad de usuarios/responsables)
     MOD-021 Centro de Tareas | MOD-022 Notificaciones
     MOD-023 Calendario y Motor de Plazos | MOD-024 Centro Regulatorio
     MOD-026 Centro de Ayuda
```

- **De que modulos recibe datos:**
  - MOD-006 RAT y Mapa de Datos: catalogo de sistemas y tratamientos a los que un control puede vincularse (campo "Sistema o activo asociado" y "Ambito de aplicacion").
  - MOD-010 Transferencias Internacionales: contexto de que transferencias existen, para los controles del bloque OBL-SEG-04 (SSL/TLS, contratos de transferencia). MOD-010 es SHOULD HAVE, no MUST HAVE: si en una version del producto MOD-010 todavia no existe como modulo estructurado, MOD-015 sigue funcionando de forma autonoma para OBL-SEG-04, registrando el control con la subcategoria "Protocolo de comunicacion segura (SSL/TLS) para transferencias" y un campo de texto libre para el pais y el proveedor, en el mismo patron de cobertura parcial que ya usa MOD-010 para el MVP (ver `06_mapa_definitivo_de_modulos.md`, seccion sobre MOD-010).
- **A que modulos envia datos o eventos:**
  - MOD-013 Incidentes de Seguridad: al abrir un incidente, MOD-013 puede consultar que controles existian sobre el sistema afectado, como parte del contexto de la investigacion (sin que esto sea una dependencia estructural que bloquee a MOD-013 si un control no esta registrado).
  - MOD-014 Riesgos y EIPD: comparte la entidad Control; toda EIPD que seleccione o cree un control lo hace sobre este catalogo. MOD-014 es SHOULD HAVE: si no existe todavia, MOD-015 funciona igual como catalogo independiente, simplemente sin la funcionalidad de sugerencia automatica de controles desde una EIPD.
  - MOD-018 Auditoria de Cumplimiento: consume el checklist de controles y su estado como uno de los insumos principales de la auditoria anual sustantiva.
  - MOD-019 Centro de Evidencias: recibe cada archivo de evidencia con su hash, version y fecha, para que el Centro de Evidencias pueda responder "que evidencia tenemos de esta obligacion" citando OBL-SEG-01 a 06 y OBL-SENS-05.
- **Catalogos que comparte:** el catalogo de tipos de control de la seccion D es propio de MOD-015 y se expone por referencia a MOD-014; el catalogo de sistemas es propio de MOD-006 y MOD-015 solo lo consume por referencia.
- **Que ocurre si un modulo dependiente no existe en el MVP:** ademas del caso ya descrito de MOD-010, si MOD-018 (Auditoria de Cumplimiento, SHOULD HAVE) todavia no existe, el catalogo de MOD-015 sigue siendo util por si mismo como fuente de evidencia consultable manualmente; la unica perdida es la generacion automatica del insumo de auditoria formal, que puede exportarse igual como checklist bajo demanda (seccion N).

---

## M. Dashboard

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Controles con evidencia vigente | (Controles en estado Implementado o Implementado con hallazgo) / (Total de controles no archivados) x 100 | Verde 80% o mas, amarillo 50 a 79%, rojo menos de 50% [opinion de producto, umbral sin respaldo legal] | Gerencia: solo el semaforo. Responsable de Seguridad/IT: el numero exacto y la lista de pendientes. Legal/Delegado: el mismo indicador con enfasis en los controles OBLIGATORIO. Auditor: el indicador mas el detalle exportable |
| Controles obligatorios sin evidencia o vencidos | Cuenta de controles del catalogo base (OBL-SEG-01 a 06) en estado Pendiente de implementar o Vencido | Rojo si el numero es mayor a 0 | Gerencia y Legal/Delegado ven este indicador vinculado explicitamente al riesgo de infraccion grave (Art. 56 lit. b); Responsable de Seguridad/IT ve la lista detallada |
| Proximas revisiones (30 dias) | Cuenta de controles con proxima fecha de revision dentro de los siguientes 30 dias | Sin semaforo, es informativo | Responsable de Seguridad/IT |
| Excepciones activas | Cuenta de controles en estado No aplica - Exceptuado, separando las aprobadas de las pendientes de aprobacion | Amarillo si hay pendientes de aprobar | Legal/Delegado, Aprobador, Gerencia |

Ningun indicador de este modulo se expresa como "porcentaje de cumplimiento legal"; el lenguaje siempre es "controles con evidencia vigente", "controles pendientes" o "excepciones activas", junto con el banner de descargo estandar del sistema (`04_objetivo_exacto_del_producto.md`, seccion 1.3).

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Checklist de controles de seguridad | Catalogo completo con categoria, tipo, estado, responsable y fecha de ultima revision | Categoria, estado, responsable, rango de fechas | PDF, XLSX | Responsable de Seguridad/IT, Delegado, Gerencia | Si |
| Reporte de excepciones y justificaciones | Lista de controles exceptuados, su justificacion y su aprobador | Estado, rango de fechas | PDF | Legal/Delegado, Auditor | Si |
| Paquete de evidencia de seguridad | Checklist mas los archivos de evidencia adjuntos, con verificacion de integridad | Por obligacion (OBL-SEG-01 a 06, OBL-SENS-05) o por control especifico | ZIP con verificacion de integridad, generado a traves de MOD-019 | Auditor externo, o la empresa para presentar ante la ACE si esta lo requiere | Si (es en si mismo un subconjunto del paquete general de evidencias) |
| Historial de cambios de un control | Linea de tiempo de un control especifico: quien cambio que y cuando | Un control especifico | CSV o vista en pantalla | Auditor interno, Responsable Legal/Compliance | Si |

---

## O. Historial

Eventos que quedan en el historial del modulo y en la auditoria transversal (AuditLog):

- Creacion de un control (manual, desde el diagnostico, o desde una EIPD de MOD-014), con origen registrado.
- Cambio de cualquier campo del control, con valor anterior y valor nuevo (categoria, tipo, ambito, responsable, periodicidad, etc.).
- Cambio de estado, con quien lo ejecuto, cuando, y el estado origen y destino.
- Registro y aprobacion (o rechazo) de una excepcion, con la identidad del creador y del Aprobador.
- Adjuntos de evidencia: cada archivo subido o reemplazado, con hash, version y usuario.
- Exportaciones de checklist o de paquete de evidencia, con quien la genero y cuando.
- Accesos de lectura a evidencia tecnica marcada como sensible (por ejemplo, un reporte de pentest), en linea con la buena practica de seguridad descrita en la seccion J.
- Archivado y reactivacion de un control, con el motivo indicado por el usuario.

---

## P. Riesgos

- **Riesgo legal:** que un usuario interno, o incluso un tercero que vea el dashboard, interprete el indicador "Controles con evidencia vigente" como una declaracion de que la empresa cumple con la LPDP. Mitigacion de diseno: el indicador nunca se expresa como porcentaje de cumplimiento legal, siempre lleva el banner de descargo estandar, y el texto de ayuda de cada control aclara que registrar evidencia no equivale a una validacion tecnica ni juridica de que el control sea adecuado.
- **Riesgo de UX:** una pyme sin area de TI dedicada (perfil Karla, `05_tipos_de_usuario.md`, seccion 5.1) se enfrenta a un catalogo tecnico que no entiende y abandona el modulo sin completarlo. Mitigacion de diseno: el catalogo base viene preconfigurado con lenguaje simple y ejemplos concretos, permite marcar en bloque "gestionado por mi proveedor de TI externo" para varios controles tecnicos a la vez, y el Centro de Ayuda (MOD-026) explica cada tipo de control sin jerga.
- **Riesgo operativo:** una periodicidad de revision mal configurada (por ejemplo, un pentest que deberia revisarse cada ano pero queda marcado como "Segun evento" sin que nunca ocurra el evento) deja un control critico sin revisar indefinidamente sin que nadie lo note. Mitigacion de diseno: el motor de plazos compartido (MOD-023) y las alertas escalonadas de la seccion I; ademas, el sistema sugiere (no fuerza) una periodicidad por defecto razonable segun el tipo de control al crearlo.
- **Riesgo de seguridad y privacidad:** la evidencia adjunta a un control (por ejemplo, un reporte de pentest que detalla vulnerabilidades reales de la infraestructura del cliente) es en si misma informacion sumamente sensible desde el punto de vista de seguridad, y su filtracion podria ser mas danina que el propio incumplimiento que pretende probar. Mitigacion de diseno: acceso restringido a evidencia tecnica sensible (Responsable de Seguridad/IT, Administrador y Auditor con acceso concedido explicitamente), cifrado de archivos en reposo dentro de MOD-019, y registro de accesos de lectura descrito en la seccion J.
- **Riesgo de separacion de funciones en pyme:** cuando la misma persona acumula los roles Administrador, Delegado y Responsable de Seguridad/IT (perfil Karla), esa persona puede crear un control, marcarlo como excepcion y aprobar su propia excepcion sin ningun segundo control real. Mitigacion de diseno: advertencia visible de autorrevision en cada aprobacion de excepcion hecha por el mismo usuario que la creo, siguiendo la regla general de `05_tipos_de_usuario.md`, seccion 5.4.

---

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Catalogo base de controles (organizativos, tecnicos, fisicos) con estado y evidencia adjunta | X | | | | Cubre directamente OBL-SEG-01 a 06 y OBL-SENS-05, todas OBLIGATORIO; concentra el bloque de infraccion grave del Art. 56 lit. b; su plazo transitorio de adecuacion ya vencio (OBL-PLAZO-03) |
| Registro de excepciones con justificacion y aprobacion de un segundo usuario | X | | | | Sin esto, un control OBLIGATORIO sin evidencia quedaria indistinguible de una decision consciente de no implementarlo; es necesario para no bloquear el flujo y para dejar evidencia de la decision |
| Vinculacion con Sistema/Tratamiento del RAT (MOD-006) | X | | | | Sin esta vinculacion no se puede filtrar que controles aplican a que tratamiento, funcion basica del catalogo |
| Indicadores de dashboard (evidencia vigente, controles obligatorios sin evidencia) | X | | | | Es el valor probatorio central del modulo frente al riesgo sancionador; sin el, el catalogo es solo una lista sin utilidad de gestion |
| Alertas de vencimiento y revision periodica | | X | | | El catalogo basico ya permite el registro manual; las alertas automatizadas mejoran la vigencia real pero dependen de que el motor de plazos (MOD-023) este maduro |
| Vinculacion estructurada con Transferencias Internacionales (MOD-010) para OBL-SEG-04 | | | X | | MOD-010 es SHOULD HAVE; mientras no exista como modulo completo, OBL-SEG-04 se cubre con un campo generico dentro de MOD-015 (ver seccion L), suficiente para el MVP pero no optimo |
| Entidad Control compartida en tiempo real con EIPD (MOD-014) | | X | | | Depende de que MOD-014 exista como modulo operativo; mientras tanto MOD-015 funciona de forma autonoma sin perder su propio valor |
| Reportes exportables (checklist, paquete de evidencia con verificacion de integridad) | | X | | | El registro ya existe desde el MVP; el empaquetado exportable avanzado (ZIP firmado) puede iterar una vez que MOD-019 este completo |
| Catalogo ampliado o plantillas de controles por sector/industria | | | | X | Funcionalidad diferenciadora de producto, sin urgencia regulatoria ni dependencia estructural |
| Integracion de solo lectura con herramientas reales de seguridad (SIEM, escaneres) para autocompletar evidencia | | | | X | Fuera del alcance central del MVP; ademas debe disenarse con cuidado para no convertir el producto en un SIEM (anti-feature 2), aunque una integracion de solo lectura futura no viola ese limite si el producto sigue sin ejecutar controles |

**Version minima vendible del modulo:** el catalogo base con las siete obligaciones propietarias (OBL-SEG-01 a 06 y OBL-SENS-05) registrables como controles individuales, cada uno con categoria, tipo, responsable, estado, evidencia adjunta con hash y vinculacion basica al sistema o tratamiento del RAT, mas el indicador de dashboard que vincula controles obligatorios sin evidencia al riesgo de infraccion grave. Esto ya permite a una empresa demostrar, desde el primer dia de uso, que tiene un proceso documentado para las medidas de seguridad exigidas por la ACE, que es exactamente el nucleo del valor probatorio de este modulo.

---

## R. Ayuda contextual (complemento obligatorio)

**1. Que es un "control de seguridad" en este sistema**
- Que es: una medida concreta (una regla, una herramienta o algo fisico) que tu empresa tiene para proteger los datos personales que maneja, registrada aqui junto con la prueba de que existe.
- Por que tengo que hacer esto: la Agencia de Ciberseguridad del Estado exige que toda empresa tenga un conjunto minimo de estas medidas, y este catalogo es donde demuestras que las tienes.
- Fundamento: OBL-SEG-01 (Art. 35 LPDP) y OBL-SEG-02, OBL-SEG-03, OBL-SEG-05 (Art. 4 de las Politicas de Actuacion de la ACE).
- Cuando necesito ayuda juridica: si no estas seguro de si un control especifico te aplica o no segun el tipo de negocio que tienes, consulta con tu asesor legal o con la persona designada como Delegado o Responsable interno.

**2. Por que debo adjuntar evidencia y no basta con decir que ya lo tengo**
- Que es: la evidencia es cualquier archivo o referencia (captura, contrato, certificado, reporte) que prueba que el control realmente existe, no solo que lo marcaste como hecho.
- Por que tengo que hacer esto: si la ACE te pide demostrar que cumples con una medida de seguridad, una casilla marcada sin nada detras no sirve como prueba; el archivo adjunto si.
- Fundamento: OBL-PRIN-03 (Art. 5 lit. i LPDP, responsabilidad demostrada).
- Cuando necesito ayuda juridica: si no sabes que tipo de documento podria servir como evidencia suficiente para un control especifico, consulta con tu asesor legal o de seguridad.

**3. Que significa que un control este "vencido"**
- Que es: significa que ya paso la fecha en la que debias volver a revisar que ese control sigue funcionando, y todavia no lo has confirmado.
- Por que tengo que hacer esto: un control que funcionaba hace dos anos pero nadie ha vuelto a revisar podria haber dejado de funcionar sin que nadie lo note; revisarlo periodicamente es parte de mantenerlo vigente.
- Fundamento: [opinion de producto, apoyada en OBL-SEG-01 a 06, ya que la ACE no fija una periodicidad especifica salvo para la auditoria anual].
- Cuando necesito ayuda juridica: normalmente no; esto es una decision de gestion interna, no una pregunta legal.

**4. Que pasa si un control no aplica a mi empresa (excepcion)**
- Que es: es la opcion de registrar formalmente que, por la naturaleza de tu negocio, un control especifico del catalogo no te corresponde, explicando por que.
- Por que tengo que hacer esto: dejar un control sin implementar y sin explicacion se ve igual, ante una revision, que simplemente no haberlo cumplido; una excepcion justificada y aprobada por otra persona demuestra que fue una decision consciente.
- Fundamento: OBL-SEG-06 (Art. 56 lit. b num. 5 y 7 LPDP, infraccion grave por no implementar medidas de la ACE).
- Cuando necesito ayuda juridica: si tienes dudas sobre si tu justificacion es suficiente o si la ACE podria no aceptarla, consulta con tu asesor legal antes de dar la excepcion por cerrada.

**5. Por que este modulo no es un antivirus ni un SIEM**
- Que es: este modulo no instala, ejecuta ni monitorea nada en tus sistemas; solo lleva el registro ordenado de que controles tienes y la prueba de que existen.
- Por que tengo que hacer esto: para saber que, aunque el sistema te ayude a organizar y recordar, la responsabilidad de tener realmente instalado y funcionando cada control tecnico sigue siendo tuya o de tu proveedor de TI.
- Fundamento: [opinion de producto, alineada con el anti-feature 2 y 11 de `22_anti_features.md`].
- Cuando necesito ayuda juridica: no aplica; esta es una aclaracion sobre que hace el software, no una pregunta legal.

**6. Que es la "infraccion grave" vinculada a estos controles**
- Que es: es una de las categorias de sancion que puede imponer la ACE cuando una empresa no implementa las medidas de seguridad que la ley y las Politicas de Actuacion exigen.
- Por que tengo que hacer esto: conocer que existe esta categoria de sancion, y su rango de multa, ayuda a entender por que este catalogo de controles no es un tramite opcional.
- Fundamento: OBL-SEG-06, Art. 56 lit. b num. 5 y 7 LPDP (multa de 11 a 25 salarios minimos mensuales del sector comercio, segun Art. 57).
- Cuando necesito ayuda juridica: siempre que exista un riesgo real de que la ACE este evaluando o haya iniciado un procedimiento sancionador contra tu empresa; en ese caso, contacta de inmediato a tu asesor legal.

---

## Nota final del agente (posibles observaciones sobre el mapa)

No se detecto ningun error en las decisiones ya tomadas para MOD-015 en `06_mapa_definitivo_de_modulos.md` ni en `mapa_modulos.json`. Dos precisiones que esta ficha desarrolla y que conviene dejar explicitas para quien lea el mapa junto a esta ficha:

1. La nota "No aplica directamente" de la reforma 659 para MOD-015 es correcta para el grueso del catalogo, pero dentro de las seis medidas organizativas de OBL-SEG-02 hay un item literal ("Delegado de Proteccion de Datos") cuyo nombre y obligatoriedad si cambian si el estado FUTURO llega a activarse (ver la nota dentro de la seccion A de esta ficha). No contradice el mapa, solo lo precisa a nivel de campo del catalogo.
2. MOD-015 declara `depende_de` MOD-010 (Transferencias Internacionales), que en el mapa esta clasificado SHOULD HAVE, mientras que MOD-015 es MUST HAVE. Esto no es un error de mapa (la relacion de datos es real: OBL-SEG-04 necesita saber que transferencias existen), pero si es una dependencia MUST HAVE -> SHOULD HAVE que esta ficha resuelve explicitamente en la seccion L con una cobertura parcial equivalente a la que el propio MOD-010 ya usa para su MVP, en vez de dejar a MOD-015 bloqueado por un modulo de prioridad menor.
