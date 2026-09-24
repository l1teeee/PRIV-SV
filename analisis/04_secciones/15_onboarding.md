# 15. Propuesta de onboarding

Fecha de esta seccion: 2026-09-24. Fase: analisis funcional (prohibido codigo, SQL, APIs, esquemas de base de datos, nombres de tecnologias, stack o infraestructura).

Fuentes principales: `03_modulos/MOD-003_ficha.md` (Onboarding), `03_modulos/MOD-004_ficha.md` (Diagnostico de Cumplimiento), `03_modulos/MOD-005_ficha.md` (Plan de Cumplimiento), `03_modulos/MOD-001_ficha.md` (Organizacion y Personas), `03_modulos/MOD-002_ficha.md` (Delegado / Responsable Interno de Datos), `03_modulos/MOD-026_ficha.md` (Centro de Ayuda), `02_validacion/05_tipos_de_usuario.md` (roles estandar y perfiles), `02_validacion/06_mapa_definitivo_de_modulos.md` (mapa de modulos y doble estado de la reforma 659), `02_validacion/mapa_modulos.json`, `02_validacion/22_anti_features.md` y `01_legal/matriz_obligaciones.json` / `.md`. Esta seccion no define funcionalidad nueva: consolida y cruza lo ya decidido en esas fichas. Donde se propone algo que ninguna ficha define, queda marcado explicitamente como "propuesta de esta seccion, no presente en las fichas".

Regla transversal de esta seccion, heredada de todas las fuentes: el sistema orienta, explica, organiza, alerta, calcula, registra, documenta y genera evidencia; nunca decide cuestiones juridicas ni afirma cumplimiento legal. Ninguna pantalla de onboarding, diagnostico o plan usa la expresion "porcentaje de cumplimiento legal" ni equivalente; se usa siempre estado del programa, controles configurados, tareas pendientes o evidencia disponible.

---

## 15.1 Objetivo del onboarding y resultado del dia 1

**Objetivo.** Que una persona designada por una empresa privada salvadorena, sin formacion juridica previa, pueda completar en una sola sesion guiada (MOD-003 Onboarding) el alta minima de su organizacion, sus primeros usuarios y roles, y la pregunta inicial sobre el Delegado de Proteccion de Datos, y llegar en esa misma sesion o en la inmediatamente siguiente al Diagnostico de Cumplimiento (MOD-004), de forma que el "dia 1" del uso del sistema entregue algo mas que una cuenta creada: un punto de partida verificable de que la empresa empezo a gestionar su programa de proteccion de datos.

**Que tiene la empresa al terminar la primera sesion** (contenido tomado de MOD-003, seccion E, y de la salida de MOD-004, seccion E, cuando el diagnostico se completa en la misma sesion):

| Al terminar el Onboarding (MOD-003), siempre | Al terminar tambien el Diagnostico (MOD-004), si la sesion continua |
|---|---|
| Una organizacion activa en MOD-001, con razon social, sector, tamano y pais(es) declarados | Un nivel de madurez inicial (INICIAL / EN DESARROLLO / EN CONSOLIDACION), nunca un porcentaje de cumplimiento |
| Al menos una cuenta activa con rol Administrador de la organizacion | Un conteo de acciones por prioridad (por ejemplo "7 acciones criticas, 8 importantes, 8 recomendadas" en el caso pyme de referencia, ver seccion 15.4) |
| Cuentas en estado "invitado" para los demas usuarios que el Administrador dio de alta, con su rol propuesto | Tratamientos sugeridos precargados en el RAT (MOD-006) |
| Un registro inicial del Delegado de Proteccion de Datos en MOD-002 (si la respuesta del Paso 4 fue "ya designado" o "designarlo ahora"), o una tarea CRITICAL persistente para resolverlo (si la respuesta fue "no estoy seguro") | Documentos sugeridos para iniciar en MOD-008 (por ejemplo el Aviso de Privacidad) |
| La tarea "Iniciar el Diagnostico de Cumplimiento" creada en el Centro de Tareas (MOD-021) | Evaluaciones de riesgo o EIPD sugeridas en MOD-014, cuando el diagnostico las detecta |
| Un evento de auditoria "onboarding completado", con fotografia de todo lo capturado, como linea base historica | Un Plan de Cumplimiento generado en borrador (MOD-005), pendiente de revision y aprobacion (ver seccion 15.4); el plan no se genera hasta que el diagnostico cierra |

En ningun momento del dia 1 el sistema declara que la empresa "ya cumple" la ley: el texto de descargo del Paso 5 del onboarding (seccion 15.2) y el texto fijo del resultado del diagnostico ("Este resultado es un calculo de apoyo interno... no una declaracion de cumplimiento legal", MOD-004 seccion E.1) acompanan ambos cierres.

### Duracion estimada por tamano de empresa

**Advertencia de origen.** Ninguna ficha (MOD-003, MOD-004 ni MOD-005) fija una duracion en minutos u horas para el onboarding o el diagnostico. Las estimaciones de esta tabla son una **propuesta de esta seccion, no presente en las fichas**, calculada a partir del numero de pasos y campos que si estan definidos (5 pasos del onboarding, con entre 1 y 4 campos obligatorios por paso segun MOD-003 seccion D; 11 bloques y 47 preguntas del diagnostico segun MOD-004 seccion D.2) y del numero de personas que participan segun el perfil de empresa de `05_tipos_de_usuario.md`, seccion 5.1. Se marcan como estimacion orientativa para el equipo de UX, no como un compromiso de producto.

| Tamano de empresa | Quien participa (perfil de referencia) | Onboarding (MOD-003) | Diagnostico (MOD-004) | Nota |
|---|---|---|---|---|
| Pyme (una sola persona, ejemplo Karla, ~30 empleados) | Una persona concentra Administrador + Delegada | 10 a 15 minutos, en una sola sesion | 45 a 60 minutos, en una o dos sesiones (guardar y continuar) | Puede completar onboarding y diagnostico el mismo dia, ver variante 15.6.1 |
| Empresa mediana (ejemplo Avicola San Andres, ~300 empleados) | Administrador inicia; bloques del diagnostico asignados a Delegado, RRHH, Marketing, IT (MOD-004 seccion C) | 20 a 30 minutos para el Administrador | 10 a 15 minutos por bloque y por responsable, en paralelo; el cierre formal (todos los bloques obligatorios completos) puede tardar de 3 a 10 dias calendario en coordinarse entre areas, no una sola sesion | El "dia 1" cubre el onboarding y el arranque del diagnostico, no necesariamente su cierre completo |
| Grupo corporativo (ejemplo Grupo Financiero Itzalco) | Administrador de cada sociedad regulada del grupo, con su propio Delegado dedicado | 30 a 45 minutos por sociedad (mas campos de contacto institucional y coordinacion con Compliance corporativo) | Igual que empresa mediana, por sociedad; la vision consolidada entre sociedades es funcionalidad V1/Enterprise (decision 2.7.31 de `05_tipos_de_usuario.md`) y no forma parte del dia 1 del MVP | Cada sociedad del grupo completa su propio ciclo de onboarding y diagnostico; no existe en el MVP una sesion unica que de de alta varias razones sociales a la vez (MOD-003 seccion Q, funcionalidad FUTURE) |

---

**Nota de origen de esta sub-seccion.** Todo el contenido de 15.2 proviene de MOD-003 seccion D y F; ninguna cifra ni regla fue inventada para esta seccion.

## 15.2 Flujo paso a paso de la primera sesion (MOD-003 Onboarding)

El onboarding es, por diseno, un proceso lineal de una sola pasada por organizacion (MOD-003 seccion F): no es repetible como el diagnostico. Lo ejecuta en la practica una sola persona, quien se autoasigna el rol Administrador de la organizacion (MOD-003 seccion B).

### Diagrama ASCII del flujo de los 5 pasos

```
   (alta comercial de la cuenta; evento externo, fuera de este modulo)
                              |
                              v
                    +-------------------+
                    |   NO_INICIADO     |
                    +-------------------+
                              |
                       "Iniciar configuracion"
                              v
   +--------------------------------------------------------------+
   |                      EN_PROGRESO                              |
   |                                                                |
   |   [Paso 1: Datos de la empresa]                                |
   |     razon social (obligatorio) -> NIT -> sector (obligatorio)  |
   |     -> cantidad de empleados (obligatorio) -> pais(es)         |
   |        (obligatorio) -> direccion -> sitio web                 |
   |        "Guardar y continuar" ---> autoguardado (punto 1)       |
   |              |                                                 |
   |              v                                                 |
   |   [Paso 2: Primer usuario - Administrador]                     |
   |     nombre completo (obligatorio) -> correo (obligatorio)      |
   |        -> cargo (opcional)                                     |
   |        "Guardar y continuar" ---> autoguardado (punto 2)       |
   |              |                                                 |
   |              v                                                 |
   |   [Paso 3: Usuarios adicionales, 0 a N filas, todo opcional]    |
   |     por cada fila: nombre + correo + rol propuesto (obligat.   |
   |        si se agrega la fila) + area (opcional)                 |
   |        "Guardar y continuar" ---> autoguardado (punto 3)       |
   |              |                                                 |
   |              v                                                 |
   |   [Paso 4: Delegado de Proteccion de Datos]                    |
   |     "Ya designado" / "Designarlo ahora" / "No estoy seguro"    |
   |        (obligatorio elegir una opcion)                         |
   |        si no es "no estoy seguro": nombre + correo + tipo      |
   |        interno/externo (obligatorio)                          |
   |        "Guardar y continuar" ---> autoguardado (punto 4)       |
   |              |                                                 |
   |              v                                                 |
   |   [Paso 5: Confirmacion]                                       |
   |     casilla de descargo de responsabilidad (obligatoria)       |
   |        "Confirmar y finalizar"                                 |
   |                                                                |
   +--------------------------------------------------------------+
        |                                              ^
        | inactividad prolongada (5 dias, configurable)|
        v                                              | reingresar al wizard
   +----------------+                                  |
   |   ABANDONADO   | ---------------------------------+
   +----------------+
                              |
                (Paso 5 confirmado, todos los obligatorios validos)
                              v
                    +-------------------+
                    |    COMPLETADO     |
                    +-------------------+
                              |
        activa MOD-001 (organizacion, usuarios, roles)
        siembra MOD-002 (si aplica, Paso 4) y crea tarea en MOD-021
                              v
              redirige a MOD-004 Diagnostico de Cumplimiento
```

**Puntos de guardado y reanudacion.** El wizard autoguarda al final de cada uno de los 5 pasos (MOD-003 seccion F, evento "Guardar y continuar"); no existe un autoguardado a nivel de campo individual dentro de un mismo paso. Si la organizacion queda inactiva 5 dias (valor por defecto, configurable por el equipo del producto, no por la empresa) sin completar un paso nuevo, el estado pasa a ABANDONADO sin perder el avance ya guardado; al reingresar, el wizard continua exactamente en el ultimo paso guardado (MOD-003 tabla de transiciones, seccion F). No existe una funcion de "reabrir" una vez que el estado llega a COMPLETADO: cualquier cambio posterior a organizacion, usuarios o roles se hace directamente en MOD-001.

### Preguntas de alta, paso a paso

**Paso 1, datos de la empresa** (MOD-003 seccion D, Paso 1; ver nota de contradiccion sobre el campo NIT al final de esta seccion): razon social, nombre comercial, identificacion tributaria (NIT), sector o industria (catalogo cerrado), cantidad aproximada de empleados, pais o paises donde opera (El Salvador preseleccionado), direccion principal, sitio web. Los campos de sector, cantidad de empleados y pais se reutilizan como precarga de las preguntas P-EMP-01, P-EMP-02 y P-EMP-08 del Diagnostico (MOD-004 seccion D.3), de modo que la empresa nunca los declara dos veces.

**Paso 2, primer usuario (Administrador)**: nombre completo (obligatorio), correo electronico (obligatorio, unico en el sistema), cargo dentro de la empresa (opcional, de catalogo o texto libre). Quien completa este paso queda con el rol "Administrador de la organizacion" desde `05_tipos_de_usuario.md`, seccion 5.3.

**Paso 3, usuarios adicionales (tabla repetible, 0 a N filas, opcional en su totalidad)**: por cada fila, nombre completo, correo electronico, rol propuesto (catalogo de los 12 roles estandar de `05_tipos_de_usuario.md` seccion 5.3, excluyendo Titular externo, Auditor externo y Asesor externo invitado, que no se asignan en el alta inicial) y area o departamento (opcional). El sistema puede sugerir un rol a partir del cargo declarado, pero el Administrador siempre confirma la asignacion final (MOD-003 seccion H, decision no automatizable 2).

**Paso 4, Delegado de Proteccion de Datos**: la pregunta central es "Su empresa, tiene ya una persona designada como Delegado de Proteccion de Datos", con tres opciones ("Si, ya esta designado" / "No, quiero designarlo ahora" / "No estoy seguro, necesito ayuda para decidir"). Si la respuesta no es "no estoy seguro", se piden nombre, correo y si el Delegado es interno, externo persona natural o externo persona juridica (MOD-003 seccion D, Paso 4). Fundamento de por que se pregunta desde el primer contacto: OBL-DPO-01, Arts. 15 y 17 de la Ley para la Proteccion de Datos Personales (Decreto Legislativo 144), clasificacion OBLIGATORIO en `matriz_obligaciones.json`, con el plazo de comunicacion a la ACE de 15 dias habiles (OBL-DPO-03, Art. 10 de los Lineamientos para el Delegado de Proteccion de Datos Personales de la ACE) ya corriendo desde el nombramiento. El sistema nunca concluye por si mismo si la empresa necesita o no un Delegado (MOD-003 seccion H, decision no automatizable 1); si la respuesta es "no estoy seguro", se crea una tarea CRITICAL persistente en el Centro de Tareas.

**Paso 5, confirmacion**: una sola casilla obligatoria, "Acepto el aviso de que este sistema no sustituye asesoria legal", con el texto: "Confirmo que entiendo que este sistema organiza y documenta el programa de proteccion de datos de mi empresa, pero no sustituye asesoria legal ni garantiza cumplimiento" (MOD-003 seccion D, Paso 5, fundamento en `02_validacion/04_objetivo_exacto_del_producto.md`, secciones 1.2 y 1.3).

### Alta de organizacion, usuarios, roles y Delegado, en una sola tabla

| Que se pide | En que paso | Obligatorio | Destino | Fundamento |
|---|---|---|---|---|
| Razon social, sector, tamano, pais(es) | Paso 1 | Si (los cuatro) | MOD-001 (Organizacion) | Buena practica; sector y tamano precargan MOD-004 |
| NIT | Paso 1 | Ver nota de contradiccion al final de la seccion | MOD-001 | Buena practica |
| Primer usuario, rol Administrador | Paso 2 | Si (nombre y correo) | MOD-001 (Usuario) | Buena practica |
| Usuarios adicionales y su rol propuesto | Paso 3 | Opcional en su totalidad; si se agrega fila, nombre/correo/rol son obligatorios | MOD-001 (Usuario, Rol) | `05_tipos_de_usuario.md`, seccion 5.3 |
| Existencia o designacion del Delegado | Paso 4 | Si (elegir una de tres opciones) | MOD-002 (si aplica) o tarea CRITICAL en MOD-021 | OBL-DPO-01, Arts. 15 y 17 LPDP |
| Descargo de responsabilidad | Paso 5 | Si | Evidencia de auditoria (MOD-019, por referencia) | `04_objetivo_exacto_del_producto.md`, secciones 1.2 y 1.3 |

---

## 15.3 Arbol de decision del Diagnostico de Cumplimiento (MOD-004, area 9 del prompt)

El Diagnostico traduce el cuestionario en tratamientos, tareas, documentos y evaluaciones de riesgo sugeridas. Tiene 47 preguntas en 11 bloques (MOD-004 seccion D.2). Todas las preguntas se muestran en lenguaje simple; el fundamento normativo (OBL-ID y articulo) solo aparece en la ayuda contextual de segundo nivel, nunca en el texto principal de la pregunta.

### 15.3.1 Deteccion de exclusiones del Art. 3 (Bloque 1, antes de sobre-obligar a la empresa)

Estas cuatro reglas (MOD-004 seccion G.1) nunca generan una tarea de ejecucion: generan una advertencia visible y exigen confirmacion humana de Legal/Compliance antes de excluir cualquier tratamiento del alcance del diagnostico. El sistema nunca concluye por si mismo que una empresa "esta" o "no esta" sujeta a la ley (MOD-004 seccion H).

```
BLOQUE 1: EMPRESA (aplicabilidad de la ley)
|
|-- P-EMP-03 (es entidad supervisada por la SSF) = Si
|      +-- P-EMP-04 (reporta historial crediticio) = Si
|             -> advertencia: "posible exclusion PARCIAL: solo el reporte de
|                historial crediticio bajo su ley especial queda fuera de la
|                LPDP; el resto de datos de la entidad supervisada por la SSF
|                sigue sujeto a la ley" [OBL-AMB-02, Art. 3 lit. a]
|                requiere confirmacion de Legal/Compliance, NO automatizable
|
|-- P-EMP-05 (tratamiento exclusivamente domestico, sin fin comercial) = Si
|      -> advertencia: "una empresa registrada formalmente rara vez cumple
|         esta condicion" [OBL-AMB-03, Art. 3 lit. b]
|         exige confirmacion explicita del Administrador antes de continuar
|
|-- P-EMP-06 (objeto es seguridad publica / registro publico oficial) = Si
|      -> advertencia: "esta exclusion no se extiende por analogia a
|         seguridad privada ni a prevencion de fraude de empresas privadas"
|         [OBL-AMB-04, Art. 3 lit. c y d]
|         exige confirmacion de Legal/Compliance
|
+-- P-EMP-07 (la ACE notifico que es operador de infraestructura critica)
       = Si / No lo se
       -> crea tarea: "confirmar ante la ACE si la empresa esta calificada
          como operador de infraestructura critica" [OBL-INC-05, Art. 6
          lit. f-g Ley de Ciberseguridad]
          la calificacion es facultad EXCLUSIVA de la ACE, nunca automatizable
```

### 15.3.2 Arbol ASCII completo de dependencias, bloque por bloque

Convencion: una pregunta sin sangria no depende de ninguna otra; una pregunta con sangria y "+--"/"`--" solo se muestra si la pregunta de la que cuelga recibio la respuesta indicada.

```
BLOQUE 1: Empresa (aplicabilidad de la ley) -- 8 preguntas
  P-EMP-01 giro o sector principal (precargado de MOD-001/MOD-003)
  P-EMP-02 cantidad de empleados (precargado)
  P-EMP-03 es entidad supervisada por la SSF -----------\
  P-EMP-04 reporta historial crediticio bajo ley especial } ver 15.3.1
  P-EMP-05 tratamiento exclusivamente domestico ---------/
  P-EMP-06 objeto es seguridad publica / registro oficial
  P-EMP-07 la ACE notifico infraestructura critica
  P-EMP-08 mas de una sucursal o sede (precargado)

BLOQUE 2: Personas (RRHH) -- 7 preguntas
  P-PER-01 tiene personal en planilla
     +-- P-PER-03 usa sistema de control de asistencia/marcaje (si P-PER-01=Si)
     |      +-- P-PER-04 ese marcaje usa huella/facial/biometria (si P-PER-03=Si)
     +-- P-PER-05 hace examenes medicos o conserva expedientes de salud (si P-PER-01=Si)
     +-- P-PER-06 registra afiliacion sindical (si P-PER-01=Si)
  P-PER-02 recibe curriculums o solicitudes de empleo (independiente)
  P-PER-07 contrata verificacion de antecedentes penales/crediticios (opcional, independiente)

BLOQUE 3: Clientes -- 4 preguntas
  P-CLI-01 registra datos de clientes
     +-- P-CLI-02 usa CRM o similar (si P-CLI-01=Si)
  P-CLI-03 programa de fidelizacion, puntos o membresias (opcional, independiente)
  P-CLI-04 ofrece financiamiento o evalua capacidad de pago (opcional, independiente)

BLOQUE 4: Marketing y web -- 6 preguntas
  P-MKT-01 tiene sitio web propio
     +-- P-MKT-02 el sitio usa cookies o tecnologias de rastreo (si P-MKT-01=Si)
  P-MKT-03 tiene formularios de captura de datos (opcional, independiente)
  P-MKT-04 hace email marketing o campanas dirigidas (opcional, independiente)
  P-MKT-05 usa WhatsApp Business u otra mensajeria (opcional, independiente)
  P-MKT-06 tiene aplicacion movil propia (opcional, independiente)

BLOQUE 5: Tecnologia y proveedores -- 4 preguntas
  P-TEC-01 usa servicios en la nube
     +-- P-TEC-02 algun proveedor tiene servidores fuera de El Salvador (si P-TEC-01=Si)
  P-TEC-03 contrata proveedores externos con acceso a datos personales
     +-- P-TEC-04 sabe si ese proveedor subcontrata a otro (si P-TEC-03=Si)

BLOQUE 6: Datos sensibles -- 2 preguntas
  P-SEN-01 categorias adicionales de datos sensibles (seleccion multiple, opcional, independiente)
  P-SEN-02 trata datos geneticos (opcional, independiente)

BLOQUE 7: Menores -- 2 preguntas
  P-MEN-01 trata datos de ninas, ninos o adolescentes
     +-- P-MEN-02 esos menores pueden registrarse o comprar sin un adulto (si P-MEN-01=Si)

BLOQUE 8: Videovigilancia y biometria -- 3 preguntas
  P-VID-01 tiene camaras de videovigilancia
     +-- P-VID-02 esas camaras usan reconocimiento facial u otro biometrico (si P-VID-01=Si)
  P-VID-03 usa biometria para clientes o publico general (opcional, independiente)

BLOQUE 9: Transferencias -- 3 preguntas
  P-TRF-01 los datos se almacenan/procesan fuera de El Salvador
           (sugerido, prellenado desde P-TEC-02, confirmable de forma independiente)
  P-TRF-02 comparte datos con sociedades del mismo grupo en otros paises (opcional, independiente)
  P-TRF-03 le han pedido enviar datos personales fuera de El Salvador (opcional, independiente)

BLOQUE 10: Seguridad -- 4 preguntas (todas independientes entre si)
  P-SEG-01 hay responsable de administrar accesos a los sistemas
  P-SEG-02 los sistemas usan autenticacion de dos factores (2FA/MFA)
  P-SEG-03 la informacion se respalda (backup) periodicamente
  P-SEG-04 hubo algun acceso no autorizado, perdida o fuga en el ultimo ano

BLOQUE 11: Gobernanza -- 4 preguntas (todas independientes entre si)
  P-GOB-01 ya cuenta con Delegado o responsable interno designado
  P-GOB-02 ya cuenta con Politica de Proteccion de Datos redactada
  P-GOB-03 ya publico un Aviso de Privacidad
  P-GOB-04 recibio en el ultimo ano alguna solicitud de una persona sobre sus datos
```

### 15.3.3 Tabla completa: pregunta, dependencia y que dispara cada respuesta

La columna "Que dispara" resume, para la respuesta indicada, el tratamiento sugerido (a MOD-006), la tarea creada (a MOD-021), el documento sugerido (a MOD-008) y la evaluacion de riesgo o EIPD sugerida (a MOD-014), tal como los define MOD-004 secciones G.1 y G.2. Cuando una celda dice "-", esa salida no aplica para esa fila. La columna "Prioridad" alimenta el conteo del nivel de madurez (MOD-004 seccion E.1).

| Bloque | ID | Pregunta (resumen) | Depende de | Respuesta que dispara | Que dispara (tratamiento / tarea / documento / riesgo) | OBL-ID (Art.) | Prioridad |
|---|---|---|---|---|---|---|---|
| 1 Empresa | P-EMP-01 | Sector o giro principal | - | Salud | Riesgo: EIPD recomendada (prestacion de servicios de salud) | OBL-SENS-04 | IMPORTANTE |
| 1 | P-EMP-02 | Cantidad de empleados | - | Mayor o igual al umbral configurado (propuesta inicial 50) | Tarea: activar la recomendacion de separacion de funciones (Aprobador distinto de Auditor) | Buena practica, `05_tipos_de_usuario.md` 5.4 | RECOMENDADA |
| 1 | P-EMP-03 | Empresa supervisada por la SSF | - | Si (junto con P-EMP-04 = Si) | Advertencia de posible exclusion PARCIAL (ver 15.3.1); no automatizable | OBL-AMB-02 (Art. 3 lit. a) | No aplica (advertencia, no accion) |
| 1 | P-EMP-04 | Reporta historial crediticio bajo ley especial | - | Si | Ver P-EMP-03 | OBL-AMB-02 (Art. 3 lit. a) | No aplica |
| 1 | P-EMP-05 | Tratamiento exclusivamente domestico | - | Si | Advertencia de posible exclusion; exige confirmacion del Administrador | OBL-AMB-03 (Art. 3 lit. b) | No aplica |
| 1 | P-EMP-06 | Objeto es seguridad publica o registro oficial | - | Si | Advertencia de posible exclusion; exige confirmacion de Legal | OBL-AMB-04 (Art. 3 lit. c y d) | No aplica |
| 1 | P-EMP-07 | ACE notifico infraestructura critica | - | Si / No lo se | Tarea: confirmar ante la ACE la calificacion | OBL-INC-05 (Art. 6 lit. f-g Ley de Ciberseguridad) | No aplica (tarea de confirmacion, no de ejecucion) |
| 1 | P-EMP-08 | Mas de una sucursal o sede | - | Si | Tarea: confirmar si cada sucursal comparte el mismo Aviso de Privacidad o requiere uno propio | Buena practica | RECOMENDADA |
| 2 Personas | P-PER-01 | Tiene personal en planilla | - | Si | Tratamiento: gestion de datos de personal; tarea: completar ficha RAT | OBL-DOC-02 (Art. 33 inc. 1) | CRITICA (plazo OBL-PLAZO-03 vencido) |
| 2 | P-PER-02 | Recibe curriculums o solicitudes de empleo | - | Si | (siembra tratamiento de clientes/candidatos, ver P-CLI-01 para el patron equivalente) | OBL-DOC-02 | - |
| 2 | P-PER-03 | Usa sistema de control de asistencia/marcaje | P-PER-01 = Si | Si | Tratamiento: control de asistencia; tarea: completar ficha RAT | OBL-DOC-02 | RECOMENDADA |
| 2 | P-PER-04 | Ese marcaje usa huella/facial/biometria | P-PER-03 = Si | Si | Tratamiento: control de acceso biometrico (dato sensible); tarea: registrar consentimiento por escrito y ofrecer alternativa no biometrica; documento: aviso especifico de biometria laboral; riesgo: EIPD recomendada | OBL-SENS-06, OBL-SENS-07, OBL-CONS-04 | CRITICA |
| 2 | P-PER-05 | Examenes medicos o expedientes de salud | P-PER-01 = Si | Si | Tratamiento: expedientes de salud ocupacional; tarea: definir base juridica y medidas reforzadas; documento: clausula de datos de salud; riesgo: EIPD recomendada | OBL-SENS-01, OBL-SENS-04 | IMPORTANTE |
| 2 | P-PER-06 | Registra afiliacion sindical | P-PER-01 = Si | Si | Tratamiento: registro de afiliacion sindical; tarea: confirmar base juridica y consentimiento reforzado; riesgo: evaluacion de riesgo basica | OBL-SENS-01 | IMPORTANTE |
| 2 | P-PER-07 | Contrata verificacion de antecedentes | - | Si | Ver nota de hueco al final de esta seccion (D.2 cita OBL-PROV-01 como fundamento, pero G.2 no define una fila de disparador propia) | OBL-PROV-01 | Sin prioridad calculada (hueco) |
| 3 Clientes | P-CLI-01 | Registra datos de clientes | - | Si | Tratamiento: gestion de datos de clientes; tarea: completar ficha RAT; documento: Aviso de Privacidad (clientes) | OBL-DOC-02, OBL-AVISO-01 | CRITICA (plazos OBL-PLAZO-03 y OBL-PLAZO-04 vencidos) |
| 3 | P-CLI-02 | Usa CRM o similar | P-CLI-01 = Si | Si | Tratamiento: gestion via CRM; tarea: registrar el CRM en el Catalogo de sistemas y, si es externo, en Proveedores | OBL-DOC-02, OBL-PROV-01 | RECOMENDADA |
| 3 | P-CLI-03 | Programa de fidelizacion, puntos o membresias | - | Si | Tratamiento: programa de fidelizacion; tarea: completar ficha RAT | OBL-DOC-02 | RECOMENDADA |
| 3 | P-CLI-04 | Ofrece financiamiento o evalua capacidad de pago | - | Si | Tratamiento: evaluacion de capacidad de pago; tarea: confirmar base juridica (contrato); riesgo: evaluacion de base juridica | OBL-PRIN-02 | RECOMENDADA |
| 4 Marketing y web | P-MKT-01 | Tiene sitio web propio | - | Si | Tratamiento: sitio web con captura de datos; tarea: verificar que el sitio muestre el Aviso de Privacidad de forma accesible | OBL-AVISO-01 | IMPORTANTE |
| 4 | P-MKT-02 | El sitio usa cookies o tecnologias de rastreo | P-MKT-01 = Si | Si | Tratamiento: uso de cookies; tarea: incluir seccion de cookies en el Aviso; documento: clausula de cookies | OBL-AVISO-03 (Art. 24 lit. i) | IMPORTANTE |
| 4 | P-MKT-03 | Formularios de captura de datos en web o redes | - | Si | Tratamiento: captura via formularios; tarea: verificar que cada formulario muestre el aviso antes de enviar datos | OBL-AVISO-04 (Art. 7) | IMPORTANTE |
| 4 | P-MKT-04 | Email marketing o campanas dirigidas | - | Si | Tratamiento: marketing directo; tarea: habilitar mecanismo de baja/oposicion enlazado a ARCO-POL | OBL-ARCO-05 (Art. 12) | IMPORTANTE |
| 4 | P-MKT-05 | WhatsApp Business u otra mensajeria | - | Si | Tratamiento: atencion/marketing via WhatsApp; tarea: confirmar con el proveedor si los datos se procesan fuera de El Salvador; registrar como transferencia "pendiente de confirmar" | OBL-TRANSF-01, OBL-TRANSF-03 | RECOMENDADA |
| 4 | P-MKT-06 | Aplicacion movil propia | - | Si | Tratamiento: app movil propia; tarea: verificar permisos del dispositivo y su justificacion en el aviso | OBL-AVISO-01, OBL-PRIN-02 | IMPORTANTE |
| 5 Tecnologia y proveedores | P-TEC-01 | Usa servicios en la nube | - | Si | Tratamiento: uso de servicios en la nube; tarea: completar el Catalogo de sistemas con cada proveedor | OBL-DOC-02 | IMPORTANTE |
| 5 | P-TEC-02 | Proveedor con servidores fuera de El Salvador | P-TEC-01 = Si | Si | Registro "pendiente de confirmar" en Transferencias; tarea: confirmar pais y documentar la transferencia | OBL-TRANSF-01, OBL-TRANSF-03, OBL-TRANSF-05 | CRITICA |
| 5 | P-TEC-02 | (misma pregunta) | P-TEC-01 = Si | No lo se | Registro "pendiente de confirmar"; tarea: solicitar al proveedor confirmacion escrita de la ubicacion de sus servidores | OBL-TRANSF-01, OBL-TRANSF-03 | IMPORTANTE |
| 5 | P-TEC-03 | Contrata proveedores externos con acceso a datos | - | Si | Tratamiento: encargados del tratamiento; tarea: registrar el proveedor y verificar contrato/DPA vigente; documento: plantilla de DPA | OBL-PROV-01, OBL-PROV-02, OBL-PROV-03 | CRITICA |
| 5 | P-TEC-04 | Ese proveedor subcontrata a otro (subencargado) | P-TEC-03 = Si | Si / No lo se | Tarea: confirmar con el proveedor si subcontrata y documentar la cadena | OBL-PROV-05 (Art. 33 inc. 2) | RECOMENDADA |
| 6 Datos sensibles | P-SEN-01 | Categorias adicionales de datos sensibles (etnia, opiniones politicas, religion, orientacion sexual, nacionalidad) | - | Cualquier categoria marcada | Tratamiento de dato sensible especifico; tarea: confirmar base juridica reforzada (consentimiento por escrito); riesgo: EIPD recomendada | OBL-SENS-01, OBL-CONS-04 (Art. 4 lit. g, Art. 59 lit. b) | CRITICA |
| 6 | P-SEN-02 | Trata datos geneticos | - | Si | Tratamiento de datos geneticos; tarea: elaborar EIPD; riesgo: EIPD obligatoria (alto riesgo) | OBL-DOC-03, OBL-SENS-04 | CRITICA |
| 7 Menores | P-MEN-01 | Trata datos de menores de 18 anos | - | Si | Tratamiento de datos de NNA; tarea: activar subflujo de consentimiento parental (MOD-007); documento: aviso adaptado a menores | OBL-PRIN-04 (Art. 5 lit. j), OBL-CONS-06 | CRITICA |
| 7 | P-MEN-02 | Esos menores pueden registrarse o comprar sin un adulto | P-MEN-01 = Si | Si | Tarea: revisar con asesoria legal el mecanismo de verificacion de edad y consentimiento parental; riesgo: nota de advertencia (tension LPDP / Ley Crecer Juntos, requiere asesoria legal) | OBL-CONS-06 (Art. 56 lit. c num. 3) | CRITICA |
| 8 Videovigilancia y biometria | P-VID-01 | Camaras de videovigilancia | - | Si | Tratamiento: videovigilancia; tarea: verificar senalizacion visible y aviso de privacidad de videovigilancia | OBL-SENS-08 (Art. 4 lit. f), OBL-AVISO-04 | IMPORTANTE |
| 8 | P-VID-02 | Camaras con reconocimiento facial u otro biometrico | P-VID-01 = Si | Si | Tratamiento: videovigilancia con reconocimiento facial; tarea: elaborar EIPD; riesgo: EIPD obligatoria | OBL-SENS-06, OBL-SENS-08, OBL-DOC-03 | CRITICA |
| 8 | P-VID-03 | Biometria para clientes o publico general | - | Si | Tratamiento: biometria de publico general; tarea: registrar consentimiento por escrito y ofrecer alternativa no biometrica; riesgo: EIPD recomendada | OBL-SENS-06, OBL-SENS-07 | CRITICA |
| 9 Transferencias | P-TRF-01 | Datos almacenados/procesados fuera de El Salvador | (sugerido desde P-TEC-02) | Si | Tratamiento: registro de transferencia internacional; tarea: registrar (o "pendiente de confirmar") con base juridica y evidencia de puesta en conocimiento a la ACE | OBL-TRANSF-01, OBL-TRANSF-03, OBL-TRANSF-04, OBL-TRANSF-05, OBL-TRANSF-06 | CRITICA |
| 9 | P-TRF-02 | Comparte datos con sociedades del grupo en otros paises | - | Si | Tratamiento: transferencia intragrupo; tarea: documentar igual que a un tercero, salvo excepcion de integracion economica centroamericana | OBL-TRANSF-01, OBL-TRANSF-02, OBL-TRANSF-03 | IMPORTANTE |
| 9 | P-TRF-03 | Le han pedido enviar datos personales al extranjero | - | Si | Tarea: no enviar datos sin verificar primero base juridica y consentimiento previo; riesgo: alerta de riesgo alto | OBL-TRANSF-04 (Art. 44) | CRITICA |
| 10 Seguridad | P-SEG-01 | Hay responsable de administrar accesos | - | No | Tarea: definir un responsable de administracion de accesos | OBL-SEG-02 | IMPORTANTE |
| 10 | P-SEG-02 | Sistemas con autenticacion de dos factores (2FA/MFA) | - | No / No lo se | Tarea: evaluar la implementacion de 2FA | OBL-SEG-03 | IMPORTANTE |
| 10 | P-SEG-03 | Se respalda (backup) la informacion periodicamente | - | No / No lo se | Tarea: confirmar y documentar la politica de respaldo | OBL-SEG-03 | IMPORTANTE |
| 10 | P-SEG-04 | Acceso no autorizado, perdida o fuga en el ultimo ano | - | Si | Alerta CRITICAL inmediata; tarea: evaluar de inmediato, con apoyo del Delegado, si activa el flujo de Incidentes y sus plazos | OBL-INC-01, OBL-INC-02, OBL-INC-04 | CRITICA |
| 11 Gobernanza | P-GOB-01 | Ya cuenta con Delegado o responsable interno designado | - | No | Tarea: designar formalmente un Delegado y comunicarlo a la ACE en 15 dias habiles | OBL-DPO-01, OBL-DPO-03 | CRITICA |
| 11 | P-GOB-02 | Ya cuenta con Politica de Proteccion de Datos | - | No | Tarea: elaborar la Politica; documento: plantilla de Politica de Privacidad | OBL-AVISO-05, OBL-SEG-02 | CRITICA (plazo OBL-PLAZO-03 vencido) |
| 11 | P-GOB-03 | Ya publico un Aviso de Privacidad | - | No | Tarea: elaborar y publicar el Aviso con los 9 literales del Art. 24; documento: plantilla de Aviso de Privacidad | OBL-AVISO-01, OBL-PLAZO-04 | CRITICA (plazo vencido 23-may-2025) |
| 11 | P-GOB-04 | Recibio en el ultimo ano una solicitud sobre sus datos | - | Si | Alerta CRITICAL; tarea: revisar de inmediato si existe una solicitud ARCO-POL pendiente fuera de plazo y regularizarla con apoyo de asesoria legal | OBL-ARCO-08, OBL-ARCO-10, OBL-DOC-01 | CRITICA |

**Fusion de disparadores duplicados.** Cuando dos o mas preguntas distintas apuntan al mismo tratamiento u obligacion (por ejemplo P-PER-04 y P-VID-03, ambas sobre biometria), el sistema fusiona ambos disparadores en una sola accion antes de contarla en el resultado, para no inflar el conteo con tareas duplicadas (MOD-004 seccion E.1).

**Hueco detectado en esta sub-seccion.** La pregunta P-PER-07 (verificacion de antecedentes penales o crediticios de candidatos) tiene fundamento normativo citado en MOD-004 seccion D.2 (OBL-PROV-01), pero no aparece con una fila propia en la tabla de disparadores G.2 de esa misma ficha: ninguna fuente define que tratamiento, tarea, documento o riesgo especifico dispara una respuesta "Si" a esa pregunta, mas alla de lo que ya cubre P-TEC-03 (proveedores externos con acceso a datos personales) de forma generica. Se deja constancia de este hueco en la seccion final de este documento en lugar de inventar un disparador que ninguna ficha define.

---

## 15.4 Del diagnostico al plan: como se construye el plan priorizado (MOD-005)

Cuando el diagnostico cierra (estado "Cerrado - resultado generado", MOD-004 seccion F), el Plan de Cumplimiento se genera automaticamente en un solo paso, en estado GENERADO (borrador), aplicando a cada obligacion aplicable el motor de priorizacion de tres niveles de MOD-005 seccion G.1:

- **CRITICA** si la obligacion tiene un plazo transitorio ya vencido (por ejemplo OBL-PLAZO-03 o OBL-PLAZO-04); o esta clasificada OBLIGATORIO en la matriz y su incumplimiento esta asociado a una infraccion GRAVE o MUY GRAVE (Art. 56/57); o es condicion previa para que otras obligaciones puedan cumplirse (por ejemplo, nombrar Delegado o publicar el Aviso de Privacidad).
- **IMPORTANTE** si no califica como Critica y la obligacion es OBLIGATORIO con infraccion LEVE o sin infraccion directa asociada, o es CONDICIONAL y el diagnostico confirmo que la condicion aplica a esta empresa.
- **RECOMENDADA** si no califica como Critica ni Importante: obligacion RECOMENDADO en la matriz, buena practica sin obligacion legal directa adicional, o CONDICIONAL de plazo lejano o bajo impacto.

El borrador pasa a EN REVISION (Administrador o Delegado lo envian) y solo se publica como VIGENTE cuando el rol Aprobador lo confirma explicitamente: el sistema nunca publica un plan por si mismo (MOD-005 seccion H, decision no automatizable 2). Al aprobarse, cada accion Pendiente crea una tarea equivalente en el Centro de Tareas (MOD-021), con el mismo responsable y fecha limite.

### Ejemplo concreto: plan de 23 acciones para una pyme

Este ejemplo reproduce, sin modificarlo, el anexo de MOD-005 ("ejemplo completo de plan para una pyme, 23 acciones"), basado en el mismo perfil de referencia usado en toda esta seccion (Ferreteria y Suministros El Roble, S.A. de C.V., ~30 empleados): personal en planilla, camaras de seguridad, recepcion de curriculums, marketing por WhatsApp y redes sociales, sistema de facturacion en la nube con proveedor externo, sin biometria y sin transferencias internacionales conocidas. Las fechas son relativas al dia de aprobacion del plan (dia 0), con los valores por defecto de MOD-005 seccion D (10 dias habiles para Critica, 30 para Importante, 90 para Recomendada).

**7 acciones CRITICAS (vencen a los 10 dias habiles):** 1) adecuarse a las Politicas de Actuacion de la ACE (OBL-PLAZO-03); 2) habilitar y publicar el mecanismo interno de solicitudes ARCO-POL (OBL-PLAZO-04); 3) nombrar formalmente al Delegado interno (OBL-DPO-01); 4) elaborar y publicar el Aviso de Privacidad con el contenido minimo del Art. 24 (OBL-AVISO-01); 5) completar el RAT de los tratamientos identificados (OBL-DOC-02); 6) implementar las medidas tecnicas minimas de las Politicas ACE (OBL-SEG-03); 7) establecer el procedimiento y canal interno para notificar vulneraciones en 72 horas (OBL-INC-01).

**8 acciones IMPORTANTES (vencen a los 30 dias habiles, salvo la 15):** 8) elaborar la Politica de Privacidad interna (OBL-AVISO-05); 9) documentar por escrito el procedimiento ARCO-POL (OBL-DOC-01); 10) registrar y controlar el consentimiento de marketing por WhatsApp y redes sociales (OBL-CONS-01); 11) elaborar el aviso de videovigilancia y registrar la base legal de las camaras (OBL-SENS-08); 12) firmar contrato o adenda de tratamiento con el proveedor de facturacion en la nube (OBL-PROV-01 y OBL-PROV-02); 13) impartir la capacitacion inicial en proteccion de datos a todo el personal (OBL-CAP-01); 14) definir y registrar el periodo de conservacion del Aviso de Privacidad, 10 anos (OBL-RET-04); 15) comunicar el nombramiento del Delegado a la ACE dentro de 15 dias habiles desde su designacion (OBL-DPO-03; fecha limite encadenada a la accion 3, no a dia 0).

**8 acciones RECOMENDADAS (vencen a los 90 dias habiles):** 16) plan anual de capacitacion mas alla del registro minimo (OBL-CAP-02); 17) primer informe periodico del Delegado (OBL-DPO-07); 18) documentar instrucciones formales al proveedor de facturacion (OBL-PROV-06); 19) revisar y documentar la eliminacion segura de documentos fisicos (OBL-SEG-05); 20) evaluacion de riesgo simplificada del tratamiento de videovigilancia (OBL-DOC-03); 21) configurar el calendario de dias inhabiles del ano en curso (OBL-PLAZO-02); 22) agendar la reverificacion del perfil del Delegado a 3 anos (OBL-DPO-04); 23) preparar la carpeta base de evidencia para la primera auditoria anual de cumplimiento (OBL-AUD-01).

Cada accion trae, ademas de lo resumido aqui, un modulo de ejecucion, un responsable sugerido y la evidencia esperada (ver MOD-005 seccion D y el anexo completo). El Plan nunca declara que estas 23 acciones "satisfacen" la ley: cada cierre exige que el responsable declare explicitamente que la evidencia adjunta satisface la tarea (MOD-005 seccion H, decision no automatizable 3), y descartar cualquier accion ligada a una obligacion OBLIGATORIO exige justificacion y, si la infraccion asociada es GRAVE o MUY GRAVE, una segunda validacion (seccion H, decision 4).

---

## 15.5 Primeros 30, 60 y 90 dias recomendados para la empresa

**Advertencia de origen.** Los plazos internos del Plan de Cumplimiento estan expresados en dias habiles (10 para Critica, 30 para Importante, 90 para Recomendada; valores por defecto configurables de MOD-005 seccion D, no dias calendario). La agrupacion en checkpoints de "30, 60 y 90 dias" calendario que sigue es una **propuesta de esta seccion, no presente en las fichas**: agrupa esos mismos plazos habiles en una cadencia de seguimiento gerencial, sin cambiar ninguna fecha limite real, que siempre calcula el motor de plazos habiles compartido del sistema (MOD-023).

| Ventana | Que deberia estar completado o en curso, segun el ejemplo de 23 acciones (seccion 15.4) | Modulos involucrados |
|---|---|---|
| Dia 1 | Onboarding completado (MOD-003); Diagnostico completado y Plan aprobado como Vigente (MOD-004, MOD-005) | MOD-003, MOD-004, MOD-005 |
| Primeros 30 dias | Las 7 acciones CRITICAS completadas o, si no, escaladas (vencen a los 10 dias habiles, aproximadamente 2 semanas calendario); inicio de las acciones IMPORTANTES | MOD-002 (Delegado), MOD-006 (RAT), MOD-008 (Aviso de Privacidad), MOD-011 (canal ARCO-POL), MOD-013 (procedimiento de 72 horas), MOD-015 (medidas tecnicas minimas) |
| Dia 31 a 60 | Cierre de la mayoria de las 8 acciones IMPORTANTES (vencen a los 30 dias habiles, aproximadamente 6 semanas calendario), incluida la comunicacion del nombramiento del Delegado a la ACE (15 dias habiles desde su designacion) | MOD-002, MOD-007 (consentimiento), MOD-008 (Politica de Privacidad), MOD-009 (contrato con el proveedor de facturacion), MOD-017 (capacitacion inicial) |
| Dia 61 a 90 | Avance visible de las 8 acciones RECOMENDADAS (vencen a los 90 dias habiles, aproximadamente 4 meses calendario; a los 90 dias calendario la empresa normalmente esta en la mitad de esta ventana, no al cierre) | MOD-014 (EIPD de videovigilancia), MOD-018 (carpeta base de auditoria), MOD-023 (calendario de dias inhabiles) |

A partir del dia 90, la gestion pasa a ser continua: alertas de vencimiento (MOD-022), el Centro de Tareas (MOD-021) como vista unica de trabajo pendiente, y el ciclo de re-diagnostico periodico (por defecto cada 12 meses o antes si cambia la actividad de la empresa, MOD-004 seccion G.3).

---

## 15.6 Variantes del onboarding

### 15.6.1 Pyme con una sola persona

Perfil de referencia: Karla Beatriz Hernandez Mejia, Gerente Administrativa y Financiera, que acumula el rol Administrador de la organizacion y Delegada de Proteccion de Datos interna (`05_tipos_de_usuario.md`, seccion 5.1, perfil 1; seccion 5.3 confirma que ambos roles son acumulables en pyme). En este caso:

- El Paso 3 del onboarding (usuarios adicionales) puede quedar vacio por completo; el wizard lo permite, aunque MOD-003 seccion P recomienda (sin bloquear) invitar al menos a un segundo usuario con permisos administrativos, para que la organizacion no dependa de una sola cuenta.
- El Paso 4 se responde tipicamente como "designarlo ahora", con la misma persona que completa el onboarding.
- Al no existir separacion de funciones por debajo del umbral de 50 empleados (`05_tipos_de_usuario.md`, seccion 5.4), Karla puede tambien aprobar su propio Plan de Cumplimiento como Aprobador, aunque el sistema muestra la advertencia de "autorrevision" (MOD-005 seccion C).
- El diagnostico completo (47 preguntas) lo responde una sola persona, sin asignacion de bloques por area (MOD-004 seccion Q clasifica esa asignacion como SHOULD HAVE, no indispensable en pyme).

### 15.6.2 Empresa mediana

Perfil de referencia: Avicola San Andres, S.A. de C.V., ~300 empleados (`05_tipos_de_usuario.md`, seccion 5.1, perfiles 2 a 4). En este caso:

- El Administrador tipicamente invita desde el Paso 3 a los responsables de area que ya tiene identificados (Delegado/Jefe de Cumplimiento, Coordinadora de RRHH, Gerente de Tecnologia), en lugar de dejarlo para despues.
- El diagnostico se reparte por bloques asignados a distintos responsables (MOD-004 seccion D.1, campo "Bloques asignados por responsable"; seccion C confirma el permiso "P" de responder solo el bloque asignado), lo que reduce el riesgo de abandono por extension del cuestionario (47 preguntas) pero implica que el cierre formal del diagnostico depende de que todas las areas completen su bloque, no de una sola sesion.
- Al superar el umbral de tamano configurable (propuesta inicial 50 empleados), el sistema recomienda y permite activar el bloqueo de separacion de funciones (por ejemplo, que Aprobador y Auditor no sean la misma persona), a diferencia de la pyme donde solo se advierte (`05_tipos_de_usuario.md`, seccion 5.4).
- El cierre del diagnostico exige doble confirmacion (Legal/Compliance o Aprobador, distinto de quien respondio) cuando el resultado contiene al menos una accion CRITICA (MOD-004 seccion C).

### 15.6.3 Grupo corporativo

Perfil de referencia: Grupo Financiero Itzalco (banco, aseguradora y financiera bajo una misma holding, `05_tipos_de_usuario.md`, seccion 5.1, perfiles 5 y 6). En este caso:

- Cada sociedad del grupo completa su propio ciclo de onboarding, diagnostico y plan, como una organizacion independiente dentro del sistema; no existe en el MVP una sesion de onboarding que de de alta varias razones sociales relacionadas a la vez (MOD-003 seccion Q, funcionalidad FUTURE; decision de alcance 2.7.31 de `05_tipos_de_usuario.md`).
- Una sociedad regulada del grupo (por ejemplo el banco) puede tener su propio Delegado dedicado, certificado ante la ACE, mientras que la vision consolidada entre sociedades (comparar el estado entre ellas, exportar evidencia consolidada) queda fuera del MVP y se ubica en V1/Enterprise.
- La Directora de Cumplimiento Corporativo (perfil 5) no participa en el onboarding de cada sociedad como Administrador; su acceso es de supervision con visibilidad sobre varias organizaciones, una capacidad tambien de alcance V1/Enterprise segun la misma decision 2.7.31.

### 15.6.4 Empresa que ya tiene documentos elaborados

Cuando la empresa llega al diagnostico con una Politica de Proteccion de Datos o un Aviso de Privacidad ya redactados fuera del sistema:

- Las preguntas P-GOB-02 (Politica) y P-GOB-03 (Aviso) se responden "Si", lo que evita que el diagnostico genere la accion CRITICA correspondiente por ausencia de esos documentos (MOD-004 seccion G.2).
- Para que ese documento quede dentro del sistema como version vigente, se registra en MOD-008 (Documentos y Politicas), donde el campo "Archivo adjunto" permite adjuntar el documento ya firmado fuera del sistema como respaldo (MOD-008 seccion D); esto no sustituye el checklist obligatorio de los 9 literales del Art. 24 (Aviso) ni el de los 5 elementos del Art. 7 (Politica y Aviso), que igual deben completarse antes de que el documento pueda aprobarse como version vigente dentro del sistema.
- De forma similar, si la empresa ya tiene una persona ejerciendo funciones de Delegado antes de usar el sistema, MOD-002 permite dar de alta ese nombramiento con su fecha real (campo `fecha_nombramiento`, no necesariamente la fecha de uso del sistema) y calcula desde alli los plazos de reverificacion trienal y capacitacion anual (MOD-002 seccion Q, "estructural... para empresas que migren un Delegado ya nombrado antes de usar el sistema").

### 15.6.5 Doble estado de la reforma 659 durante el onboarding

El Decreto Legislativo 659 fue aprobado el 17 de septiembre de 2026; al 24 de septiembre de 2026 su publicacion en el Diario Oficial no esta confirmada (`00_contexto_para_agentes.md`, seccion 3). Mientras esa publicacion no se confirme, el regimen vigente exige Delegado obligatorio en el sector privado (Arts. 15 y 17 LPDP). El sistema modela esto con una sola entidad y una bandera manual `regimen_reforma_659` (valores ACTUAL / FUTURO) alojada en MOD-024, nunca activada automaticamente por la sola fecha de aprobacion legislativa (`06_mapa_definitivo_de_modulos.md`, seccion 5). Efecto sobre el onboarding y el diagnostico:

- El Paso 4 del onboarding (MOD-003) y la pregunta P-GOB-01 del diagnostico (MOD-004) siempre preguntan por "Delegado de Proteccion de Datos o responsable interno", usando el nombre que corresponde al estado ACTUAL o FUTURO segun la bandera vigente en el momento en que la persona usa el sistema; el campo subyacente en MOD-002 es el mismo (`tipo_rol`), solo cambia la etiqueta mostrada.
- Si una organizacion completo su onboarding y diagnostico bajo el estado ACTUAL y, mas adelante, el equipo del producto confirma la publicacion oficial y activa el estado FUTURO, las tareas ya generadas que dependian de pasos exclusivos del regimen ACTUAL (por ejemplo, la comunicacion formal a la ACE) no se eliminan: se marcan "no aplica bajo el estado regulatorio actual, ver historial" (`06_mapa_definitivo_de_modulos.md`, seccion 5, punto 6; MOD-004 seccion G.3). El sistema nunca reescribe retroactivamente un onboarding o un diagnostico ya cerrado bajo el estado anterior.
- Una empresa que ya nombro un Delegado certificado bajo el estado ACTUAL puede mantenerlo voluntariamente si el estado cambia a FUTURO; el sistema no fuerza su cese (`06_mapa_definitivo_de_modulos.md`, seccion 5, punto 7).

---

## 15.7 Ayuda y lenguaje, puntos de abandono y metricas de exito

### Ayuda contextual (MOD-026)

Todo texto de pantalla del onboarding y del diagnostico sigue el mismo formato de MOD-026: una explicacion en lenguaje sencillo de "que es" y "por que tengo que hacer esto" en el cuerpo de la pantalla, con el fundamento normativo (OBL-ID, articulo, y si es OBLIGATORIO/RECOMENDADO/CONDICIONAL) siempre en un segundo nivel de ayuda contextual, nunca en el texto principal de la pregunta (regla de oro heredada de `00_plantilla_ficha_modulo.md` y confirmada en MOD-004 seccion D.2). El catalogo inicial de articulos de ayuda para estos dos modulos (MOD-026 seccion D.1) reutiliza, sin duplicarlo, el texto ya redactado en la seccion R de MOD-003 y MOD-004: "Que es la organizacion en este sistema", "Que es el Delegado de Proteccion de Datos", "Que son los roles y por que debo asignarlos desde ahora", "Por que tengo que aceptar el aviso sobre lo que este sistema no hace" y "Que pasa despues de terminar esta configuracion inicial" (onboarding); "Que es el Diagnostico de Cumplimiento", "Que es una exclusion del Art. 3", "Que es un dato personal sensible", "Que es una transferencia internacional de datos" y "Por que me preguntan sobre menores, biometria o videovigilancia" (diagnostico). Cada articulo indica ademas, cuando corresponde, "cuando necesito ayuda juridica": una condicion concreta, nunca un generico "consulte siempre a un abogado" (MOD-026 seccion D, regla del campo "Cuando necesito ayuda juridica").

### Puntos probables de abandono y su mitigacion

| Punto de abandono | Donde ocurre | Mitigacion de diseno (fuente) |
|---|---|---|
| Formulario de alta de organizacion percibido como largo | Onboarding, Paso 1 | Solo razon social, sector, cantidad de empleados y pais son obligatorios; el resto (NIT segun la nota de contradiccion, direccion, sitio web) es opcional y completable despues (MOD-003 seccion P) |
| No saber si la empresa necesita un Delegado | Onboarding, Paso 4 | La opcion "no estoy seguro" nunca cierra el tema: crea una tarea CRITICAL persistente con el texto "requiere validacion de la organizacion o asesoria especializada"; el sistema nunca asume "no aplica" por defecto (MOD-003 seccion P) |
| Mala asignacion de roles desde el primer momento | Onboarding, Paso 3 | Advertencia (no bloqueo, porque la organizacion aun no esta activa) cuando se detecta una combinacion de roles marcada como riesgosa (MOD-003 seccion P, seccion G automatizacion 9) |
| Cuestionario de 47 preguntas en 11 bloques percibido como extenso | Diagnostico | Guardar y continuar en cualquier punto; asignacion de bloques por responsable de area en empresa mediana/corporativo; lenguaje simple con ejemplos en cada pregunta; barra de progreso por bloque (MOD-004 seccion P) |
| Preguntas de dependencia condicional ocultan un tratamiento relevante (por ejemplo biometria, que solo aparece si la pregunta base fue "Si") | Diagnostico | Las preguntas base de cada bloque estan formuladas de forma amplia a proposito, para minimizar el riesgo de un "No" incorrecto (MOD-004 seccion P) |
| Ver 23 o mas acciones de golpe en el primer Plan de Cumplimiento | Plan de Cumplimiento (MOD-005), inmediatamente despues del diagnostico | Agrupacion por prioridad mostrando primero las Criticas; Importantes y Recomendadas en pestanas separadas; lenguaje simple en titulo y descripcion de cada accion (MOD-005 seccion P) |
| Organizacion depende de una sola cuenta de Administrador sin respaldo | Onboarding | Recomendacion (no bloqueo, en el MVP) de invitar a un segundo usuario con rol administrativo desde el Paso 3 (MOD-003 seccion P) |

### Metricas de exito del onboarding, sin datos personales

Consistente con la regla de que el sistema nunca declara un porcentaje de cumplimiento legal, las metricas de exito de esta etapa (MOD-003 seccion M, MOD-004 seccion M) son metricas de adopcion y de estado del programa, nunca de contenido de los titulares:

| Metrica | Formula | Fuente |
|---|---|---|
| Organizaciones que completan el onboarding | Sesiones en estado COMPLETADO / total de cuentas creadas | MOD-003 seccion M |
| Tasa de aceptacion de invitaciones | Usuarios que aceptaron su invitacion / usuarios invitados, por 100 | MOD-003 seccion M |
| Organizaciones que llegan al Diagnostico dentro de los primeros 7 dias | Sesiones de diagnostico iniciadas dentro de 7 dias del onboarding COMPLETADO / total de onboardings COMPLETADOS | Derivado de la alerta "Diagnostico nunca iniciado tras onboarding" de MOD-004 seccion I (umbral de 7 dias ya definido en esa ficha) |
| Diagnosticos completados frente a organizaciones activas | Sesiones de diagnostico en estado Cerrado / organizaciones con onboarding completo | MOD-004 seccion M |
| Nivel de madurez inicial de la organizacion | Regla de MOD-004 seccion E.1 (INICIAL / EN DESARROLLO / EN CONSOLIDACION) | MOD-004 seccion M |
| Planes de cumplimiento aprobados como Vigente dentro de los primeros 30 dias | Planes en estado Vigente con fecha de aprobacion dentro de 30 dias del cierre del diagnostico / total de diagnosticos cerrados | Propuesta de esta seccion, no presente en las fichas; combina el estado del Plan (MOD-005 seccion F.1) con la ventana de 30 dias de la seccion 15.5 |
| Utilidad percibida del contenido de ayuda durante el onboarding | Votos "util" / (votos "util" + "no fue util"), acompanado siempre de la aclaracion "mide la claridad del texto de ayuda, no el cumplimiento legal de su empresa" | MOD-026 seccion M |

Ninguna de estas metricas requiere, ni permite, almacenar datos personales de titulares externos (clientes, empleados de clientes, candidatos): todas se calculan sobre metadatos de uso de la plataforma (estados, fechas, conteos), consistente con el anti-feature 8 de `22_anti_features.md` (nunca copiar o centralizar la base de datos completa del cliente).

---

## Contradicciones y huecos detectados

### Contradicciones

1. **Obligatoriedad del campo NIT en el Paso 1 del onboarding.** `03_modulos/MOD-003_ficha.md`, seccion D (tabla del Paso 1), clasifica el campo "Identificacion tributaria (NIT)" como "Opcional en el onboarding (se puede pedir como obligatorio mas adelante, en MOD-008...)". Sin embargo, la misma ficha, en su seccion P (Riesgos), al describir la mitigacion del riesgo de abandono "durante el onboarding", afirma: "solo 5 campos son obligatorios en el alta minima (razon social, NIT, sector, pais, numero de empleados)", incluyendo el NIT como obligatorio. `03_modulos/MOD-001_ficha.md` (propietaria de la entidad Organizacion) repite exactamente esa misma lista de 5 campos obligatorios, con NIT incluido, en su propia seccion P. Se adopto la version de `MOD-001_ficha.md` (y la seccion P de MOD-003) para esta seccion 15: el NIT se trata como parte del conjunto minimo obligatorio del Paso 1, junto con razon social, sector, pais y cantidad de empleados. Razon: segun la jerarquia de fuentes de esta tarea, la ficha del modulo propietario de la entidad en disputa (MOD-001, propietaria de Organizacion) prevalece sobre el detalle de otra ficha (MOD-003, que "ejecuta el alta de MOD-001" pero no es su propietaria); ademas la propia MOD-003 se contradice internamente entre su seccion D y su seccion P, y la seccion P es la que coincide con MOD-001. Se recomienda a quien mantenga MOD-003 corregir la tabla de la seccion D (Paso 1) para que el campo NIT quede marcado "Obligatorio" y no "Opcional", alineandola con su propia seccion P y con MOD-001.

2. **Arista MOD-024 -> MOD-005 ausente en `mapa_modulos.json`, senalada por la propia ficha MOD-005.** La nota final de `03_modulos/MOD-005_ficha.md` ya deja constancia de que `mapa_modulos.json` no declara una dependencia directa entre MOD-024 (Centro Regulatorio) y MOD-005 (Plan de Cumplimiento), aunque el recalculo del plan por cambio normativo (por ejemplo, activacion del estado FUTURO de la reforma 659) si esta descrito en la seccion G.2, regla 9, de esa misma ficha. Para esta seccion 15 se adopto el modelo que la propia ficha MOD-005 propone como solucion (el evento llega a traves de MOD-004, que si es entrada declarada de MOD-005), sin inventar una arista nueva en el mapa. No es una contradiccion introducida por esta seccion, sino heredada y ya documentada por MOD-005; se repite aqui unicamente porque la seccion 15.6.5 depende de ese mismo mecanismo de propagacion del cambio de regimen hacia el onboarding y el diagnostico.

### Huecos (pasos o piezas que ninguna ficha define)

1. **Disparador de la pregunta P-PER-07 del diagnostico.** `03_modulos/MOD-004_ficha.md`, seccion D.2, define la pregunta "Contrata servicios externos de verificacion de antecedentes penales o crediticios de candidatos o personal" con fundamento OBL-PROV-01, pero la tabla completa de disparadores (seccion G.2, la unica fuente que define que tratamiento, tarea, documento o riesgo genera cada respuesta) no incluye ninguna fila para P-PER-07. Ninguna ficha precisa que ocurre especificamente cuando esta pregunta se responde "Si", mas alla de lo que ya cubre de forma generica P-TEC-03 (proveedores externos con acceso a datos personales). Documentado tambien en la seccion 15.3.3 de este mismo archivo.

2. **Duracion en tiempo del onboarding y del diagnostico.** Ninguna ficha (MOD-003, MOD-004 ni MOD-005) fija cuantos minutos u horas toma completar el wizard de 5 pasos o el cuestionario de 47 preguntas, ni por tamano de empresa. La tabla de la seccion 15.1 de este documento es una estimacion propuesta por esta seccion, marcada explicitamente como tal, y queda pendiente de validarse con usuarios reales (en linea con el anti-feature 24 de `22_anti_features.md`, que exige no fijar un diseno de UX sin validacion real).

3. **Traduccion de los plazos en dias habiles del Plan de Cumplimiento a una cadencia de 30/60/90 dias calendario.** MOD-005 seccion D fija los plazos por defecto de cada nivel de prioridad en dias habiles (10, 30 y 90), no en dias calendario, y ninguna ficha propone una agrupacion de seguimiento en "primeros 30, 60 y 90 dias" como la que exige el criterio minimo de esta tarea. La tabla de la seccion 15.5 de este documento es una propuesta de esta seccion que superpone esa cadencia de calendario sobre los plazos habiles ya definidos, sin alterarlos; el hueco es que ninguna ficha original define esa capa de seguimiento por si misma.

4. **Onboarding para el rol Delegado externo que atiende a varios clientes (perfil 10 de `05_tipos_de_usuario.md`).** Ninguna ficha describe el flujo de alta especifico para una persona como la Delegada externa Silvia Carolina Melendez, que necesita "cambiar entre las organizaciones de sus distintos clientes dentro de una misma cuenta" (`05_tipos_de_usuario.md`, seccion 5.1, perfil 10). MOD-003 solo contempla la invitacion de un Delegado externo desde el Paso 4 de una organizacion cliente especifica (con nombre, correo y modalidad interno/externo); no existe en MOD-003 ni en MOD-002 una descripcion de como esa misma persona, ya con cuenta activa en el sistema por otro cliente, acepta una nueva invitacion sin crear una cuenta duplicada. Se deja como hueco pendiente de definicion en una ficha futura (probablemente MOD-001 o MOD-002), no resuelto por esta seccion.

5. **Que pasa si la organizacion completa el diagnostico pero el Plan de Cumplimiento no llega a aprobarse como Vigente en un plazo razonable.** MOD-004 genera el resultado del diagnostico y siembra el Plan (MOD-005 lo recibe en estado GENERADO), y MOD-005 seccion I ya define la alerta "Plan pendiente de aprobacion" (escala a Gerencia tras 5 dias habiles). Sin embargo, ninguna ficha describe si el "dia 1" del onboarding, tal como lo exige el criterio minimo de esta tarea (seccion 15.1), se considera completo cuando el diagnostico cierra o solo cuando el Plan llega a Vigente; esta seccion asumio, sin que ninguna ficha lo declare de forma expresa, que el resultado del diagnostico ya constituye el resultado minimo del dia 1, y que la aprobacion del Plan es un hito posterior, normalmente dentro de los primeros dias pero no necesariamente en la misma sesion.
