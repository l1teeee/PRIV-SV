# 8. Workflows end-to-end

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (prohibido codigo, SQL, APIs, endpoints, esquemas de base de datos, nombres de tecnologias, stack o infraestructura). Esta seccion consolida y cruza lo ya definido en las 26 fichas de modulo (`03_modulos/MOD-001_ficha.md` a `MOD-026_ficha.md`) y en el mapa de modulos (`02_validacion/06_mapa_definitivo_de_modulos.md`, `02_validacion/mapa_modulos.json`); no inventa funcionalidades que ninguna ficha define. Donde el prompt del cliente exige algo que ninguna ficha cubre todavia, se marca de forma expresa "propuesta de esta seccion, no presente en las fichas". Donde un paso necesario no existe en ninguna ficha, se marca "hueco: no definido en la ficha de MOD-XXX" y se enumera al final de este documento.

Esta es la parte 1 de 4 de la seccion 8. Contiene los casos 1 a 3. Los casos 4 a 6 estan en `08b_workflows_casos_04_06.md`, los casos 7 y 8 en `08c_workflows_casos_07_08.md`, y los casos 9 a 11 en `08d_workflows_casos_09_11.md`.

## 8.0 Que es un workflow end-to-end en este blueprint

Un workflow end-to-end es el recorrido completo que sigue un hecho de negocio (una empresa que se da de alta, un area que registra un tratamiento nuevo, un titular que ejerce un derecho, una brecha de seguridad) desde el disparador que lo origina hasta su cierre, cruzando varios modulos, roles, plazos y evidencias. No es una especificacion tecnica nueva: es una lectura horizontal de lo que las secciones F (Workflow), G (Automatizaciones), H (Decisiones que NO debe automatizar), I (Alertas) y J (Evidencia) de cada ficha de modulo ya definieron por separado, mostrando como esas piezas encajan cuando un mismo caso las atraviesa en secuencia. Por esa razon, cada paso de cada caso cita el estado, la transicion, la automatizacion, el plazo o la alerta exacta de la ficha de origen, con el mismo nombre que usa esa ficha; ningun paso inventa un estado o un plazo que la ficha correspondiente no haya definido ya.

### Como leer la plantilla de cada caso

Cada uno de los 11 casos exigidos por el prompt del cliente (seccion 35 de `00_prompt_analisis_funcional.md`) se documenta con los mismos 11 apartados, en este orden:

1. **Situacion de partida.** Un escenario concreto, protagonizado por una de las tres empresas de ejemplo (ver mas abajo), nunca una empresa generica y abstracta.
2. **Disparador.** El hecho puntual que arranca el workflow.
3. **Actores (roles estandar) y modulos que intervienen.** Los roles usan exactamente los nombres de `02_validacion/05_tipos_de_usuario.md`, seccion 5.3; los modulos citan su codigo y su nombre exactos de `02_validacion/mapa_modulos.json`.
4. **Diagrama ASCII del recorrido de extremo a extremo.** Vista general del caso, en bloques de codigo con caracteres ASCII puros.
5. **Paso a paso.** Una tabla con columnas Paso, Quien, Modulo, Que hace en el sistema, Que genera, Plazo y como se calcula, y Fundamento (OBL-ID y articulo, o "buena practica" cuando no hay mandato legal expreso).
6. **Decisiones que el sistema NO toma.** Con el texto de advertencia exacto que cada ficha ya definio para ese punto de decision.
7. **Alertas y escalamientos.** Las alertas de la seccion I de cada ficha que efectivamente se disparan en el recorrido de este caso especifico, con su nivel y su escalamiento.
8. **Evidencia resultante.** Que queda demostrado al final del caso, en que modulo vive esa evidencia y cuanto tiempo se conserva.
9. **Variantes y casos borde.** Como cambia el mismo caso en una pyme donde una persona acumula varios roles, en un grupo corporativo con varias sociedades, y cuando aplica el doble estado de la reforma 659 (MOD-024).
10. **Cobertura por version.** Que parte del caso ya funciona en el MVP y que exige que un modulo SHOULD HAVE o COULD HAVE este construido (seccion Q de la ficha correspondiente).
11. **Riesgos especificos del caso y su mitigacion.** Tomados de la seccion P de las fichas involucradas, en la version relevante para el caso concreto.

### Las tres empresas de ejemplo

Los 11 casos usan siempre una de estas tres empresas, definidas en `02_validacion/05_tipos_de_usuario.md`, seccion 5.1, nunca una empresa generica:

- **Ferreteria y Suministros El Roble, S.A. de C.V.**: pyme de unos 30 empleados, sin abogado ni personal de TI dedicado; Karla Beatriz Hernandez Mejia (Gerente Administrativa y Financiera) acumula el rol de Administradora de la organizacion y de Delegada de Proteccion de Datos interna.
- **Avicola San Andres, S.A. de C.V.**: empresa mediana de unos 300 empleados, con areas separadas; Jorge Alberto Menendez Rauda (Jefe de Cumplimiento y Riesgo) es el Delegado interno en proceso de certificacion ante la ACE, Daniela Patricia Cornejo Lazo coordina Recursos Humanos y Roberto Antonio Villalta es el Gerente de Tecnologia.
- **Grupo Financiero Itzalco**: corporativo con varias sociedades (banco, aseguradora y financiera) bajo una misma holding; Licda. Ana Gabriela Reyes Portillo dirige el Cumplimiento Corporativo a nivel de grupo y Lic. Mauricio Ernesto Aguilar Sandoval es el Delegado certificado dedicado a la sociedad aseguradora.

### Indice de los 11 casos

| Caso | Titulo | Parte de la seccion 8 |
|---|---|---|
| 1 | Una empresa nueva implementa el sistema | Esta parte (08a) |
| 2 | La empresa registra un nuevo proceso (alta en el RAT) | Esta parte (08a) |
| 3 | Marketing implementa un nuevo formulario (web o evento) | Esta parte (08a) |
| 4 | RRHH comienza a usar biometria | Parte 2 (`08b_workflows_casos_04_06.md`) |
| 5 | La empresa contrata un proveedor cloud | Parte 2 (`08b_workflows_casos_04_06.md`) |
| 6 | Un proveedor almacena datos fuera del pais | Parte 2 (`08b_workflows_casos_04_06.md`) |
| 7 | Un titular solicita acceso | Parte 3 (`08c_workflows_casos_07_08.md`) |
| 8 | Un titular solicita eliminacion | Parte 3 (`08c_workflows_casos_07_08.md`) |
| 9 | Ocurre una brecha de datos | Parte 4 (`08d_workflows_casos_09_11.md`) |
| 10 | Se acerca una auditoria | Parte 4 (`08d_workflows_casos_09_11.md`) |
| 11 | Cambia la normativa | Parte 4 (`08d_workflows_casos_09_11.md`) |

---

## Caso 1. Una empresa nueva implementa el sistema

### Situacion de partida

Ferreteria y Suministros El Roble, S.A. de C.V. (pyme, unos 30 empleados, giro de venta de ferreteria y materiales de construccion, sin abogado ni personal de TI dedicado) contrata la plataforma el 24 de septiembre de 2026, despues de que la Gerencia General le asignara el tema a Karla Beatriz Hernandez Mejia, Gerente Administrativa y Financiera. La empresa trata datos de personal (planilla, marcaje), datos de clientes (facturacion, credito) y usa camaras de seguridad en la bodega principal. Karla no es abogada, tiene conocimiento legal bajo-medio y le preocupa quedar personalmente expuesta por desconocimiento (perfil 1 de `02_validacion/05_tipos_de_usuario.md`, seccion 5.1).

### Disparador

La contratacion comercial del software (proceso externo de venta, fuera del alcance funcional de este blueprint) crea la cuenta de la organizacion. Ese alta comercial deja el Onboarding (MOD-003) en estado NO_INICIADO y ya genera la tarea "Completar configuracion inicial" en el Centro de Tareas (MOD-021), ademas de la alerta de bienvenida (MOD-003, seccion F, tabla de transiciones, fila "(inicio)"; seccion I, "Bienvenida: configure su organizacion").

### Actores y modulos que intervienen

- **Karla Beatriz Hernandez Mejia**: Administradora de la organizacion y Delegada de Proteccion de Datos interna (rol acumulado, permitido en pyme segun `05_tipos_de_usuario.md`, seccion 5.3).
- Modulos: MOD-003 Onboarding, MOD-001 Organizacion y Personas, MOD-002 Delegado / Responsable Interno de Datos, MOD-004 Diagnostico de Cumplimiento, MOD-005 Plan de Cumplimiento, MOD-006 RAT y Mapa de Datos, MOD-008 Documentos y Politicas, MOD-021 Centro de Tareas, MOD-022 Notificaciones, MOD-023 Calendario y Motor de Plazos, MOD-026 Centro de Ayuda, MOD-020 Dashboard y Reportes. MOD-024 Centro Regulatorio interviene solo como consulta pasiva (bandera de la reforma 659 en estado ACTUAL).

### Diagrama del recorrido de extremo a extremo

```
  [alta comercial]
        |
        v
  MOD-003 Onboarding (NO_INICIADO)
        |  Paso 1 empresa -> Paso 2 estructura -> Paso 3 usuarios/roles
        |  -> Paso 4 pregunta del Delegado -> Paso 5 confirmar y finalizar
        v
  MOD-003 COMPLETADO
        |
        +--------------------------+---------------------------+
        v                          v                           v
  MOD-001 Organizacion       MOD-002 Delegado             MOD-021/022/023
  (ACTIVA)                   (BORRADOR -> ... -> ACTIVO)  (tareas, avisos,
        |                          |                        plazos, en todo
        v                          |                        momento)
  MOD-004 Diagnostico  <-----------+
  (EN PROGRESO -> CERRADO)
        |
        v
  MOD-005 Plan de Cumplimiento (GENERADO -> VIGENTE)
        |
        +----------------+----------------+
        v                v                v
  MOD-006 RAT       MOD-008 Documentos   MOD-021 tareas del plan
  (primeras fichas  (Aviso de Privacidad
   Vigentes)         y Politica publicados)
        |                |
        +--------+-------+
                 v
        MOD-020 Dashboard (cierre del primer mes:
        vision de Gerencia y de Responsable)

        (MOD-026 Centro de Ayuda disponible en cada pantalla
         de todo el recorrido anterior, MOD-024 consultado
         de forma pasiva por la bandera regimen_reforma_659)
```

### Paso a paso

| Paso | Quien | Modulo | Que hace en el sistema | Que genera | Plazo y como se calcula | Fundamento |
|---|---|---|---|---|---|---|
| 1 | Karla | MOD-003 | Inicia el wizard de configuracion (Paso 1: razon social, NIT, sector, pais, numero de empleados) | Pasa de NO_INICIADO a EN_PROGRESO; evento de auditoria "onboarding iniciado" | Sin plazo legal; alerta INFO si no se inicia en 48 horas | Buena practica |
| 2 | Karla | MOD-003 | Completa el Paso 2 (estructura minima: pais, sucursal) y el Paso 3 (usuarios y roles: se asigna a si misma Administradora y, en el Paso 4, tambien Delegada) | Autoguardado por paso; catalogo de areas disponible en la invitacion de usuarios | Sin plazo legal | Buena practica |
| 3 | Karla | MOD-003 | Responde la pregunta del Delegado (Paso 4) con "designarlo ahora", indicandose a si misma | Crea automaticamente el registro inicial del Delegado en MOD-002 en estado "designacion en curso"; siembra en MOD-023 el conteo del plazo de comunicacion a la ACE (15 dias habiles) a partir de cuando MOD-002 confirme el nombramiento | El plazo de 15 dias habiles corre desde la confirmacion del nombramiento en MOD-002, no desde este paso | OBL-DPO-01 (Art. 15 y 17); OBL-DPO-03 (Art. 10) |
| 4 | Karla | MOD-003 | Confirma y finaliza (Paso 5): casilla de descargo marcada, al menos un usuario Administrador activo | Activa la Organizacion en MOD-001; crea el registro del Delegado en MOD-002; envia invitaciones (MOD-022); crea la tarea "Iniciar el Diagnostico" y redirige a MOD-004 | Sin plazo legal para este paso especifico | Buena practica |
| 5 | Sistema | MOD-001 | La organizacion pasa de BORRADOR a ACTIVA al completarse los campos minimos de la seccion D.1 | Evento "organizacion lista"; habilita MOD-004 | Automatico, sin plazo | OBL-AMB-01 (Art. 2 inc. 1), obligacion colaboradora del modulo |
| 6 | Karla | MOD-002 | Acepta el cargo de Delegada (declaracion jurada digital) | El registro pasa de PENDIENTE_ACEPTACION a NOMBRADO; se fija fecha_nombramiento; se calcula el limite de 3 dias habiles para la notificacion interna | 3 dias habiles desde fecha_nombramiento (MOD-023) | OBL-DPO-02 (Art. 8) |
| 7 | Karla | MOD-002 | Registra la notificacion interna completada (constancia adjunta) | El registro pasa a NOTIFICADO_INTERNAMENTE; se calcula el limite de 15 dias habiles para comunicar a la ACE | 15 dias habiles desde fecha_nombramiento + 1 dia (MOD-023) | OBL-DPO-03 (Art. 10) |
| 8 | Karla | MOD-002 | Envia la comunicacion a la ACE (documento de acta de nombramiento adjunto) | El registro pasa a COMUNICADO_A_ACE; evento saliente hacia MOD-024 (Tramites ante la ACE) | Igual al paso anterior | OBL-DPO-03 (Art. 10) |
| 9 | Sistema | MOD-002 | Transcurren 15 dias habiles sin observacion de la ACE (o se recibe la credencial) | El registro pasa a ACTIVO; el "contacto ARCO-POL" derivado queda disponible para MOD-007, MOD-008 y MOD-011 | Automatico al cumplirse el plazo, o al registrar numero_registro_ace | OBL-DPO-03 (Art. 10) |
| 10 | Karla | MOD-004 | Inicia la sesion del Diagnostico de Cumplimiento (version del cuestionario vigente) | Sesion en EN PROGRESO; evento de auditoria | Alerta WARNING si el diagnostico no se inicia dentro de los 7 dias siguientes al onboarding | OBL-PLAZO-03 (Art. 60 inc. 2, colaboradora) |
| 11 | Karla | MOD-004 | Responde bloque por bloque (personal, clientes, marketing, tecnologia, seguridad, gobierno), incluyendo P-PER-01 (Si, gestiona datos de personal), P-CLI-01 (Si, gestiona datos de clientes), P-VID-01 (Si, tiene camaras) y P-GOB-01 a 03 (No, aun no tiene Delegado formalizado en el momento del diagnostico / no tiene Politica de Privacidad / no tiene Aviso de Privacidad publicado) | Cada respuesta dispara tratamiento sugerido (a MOD-006), tarea (a MOD-021), documento sugerido (a MOD-008) segun la tabla G.2 de la ficha del modulo | Sin plazo propio; alimenta el plan siguiente | OBL-DOC-02 (Art. 4 Medidas Organizativas, lit. d); OBL-AVISO-01 (Art. 24); OBL-AVISO-05 (Art. 24 inc. 1) |
| 12 | Karla | MOD-004 | Completa todos los bloques obligatorios; el sistema calcula el resultado preliminar y pasa a Pendiente de cierre; Karla confirma el cierre | Sesion Cerrada - resultado generado; se generan los tratamientos, tareas y documentos sugeridos en un solo paso; bloquea la edicion de respuestas | Sin plazo propio | OBL-PRIN-03 (Art. 5 lit. i, responsabilidad demostrada) |
| 13 | Sistema | MOD-005 | El cierre del diagnostico dispara la generacion de la primera version del Plan de Cumplimiento (v1, estado Generado) | Se crean todas las AccionDelPlan calculadas, clasificadas CRITICA / IMPORTANTE / RECOMENDADA por el motor de priorizacion (seccion G.1 de la ficha) | Sin plazo propio para este paso | OBL-PLAZO-03 (Art. 60 inc. 2) |
| 14 | Karla | MOD-005 | Envia el plan a revision y lo aprueba ella misma como Aprobador (rol acumulado en pyme, con advertencia de autorrevision visible) | El plan pasa de Generado a En revision a Vigente; se congela un snapshot con hash de integridad; se crean las tareas equivalentes en MOD-021 con la misma fecha limite | Alerta INFO/WARNING si el plan queda mas de 2 dias habiles sin aprobar | Buena practica de gobierno interno |
| 15 | Karla | MOD-006 | Completa las primeras fichas del RAT que el diagnostico ya creo en Borrador (personal, clientes, camaras de seguridad de la bodega) y las envia a revision | Cada ficha pasa de Borrador a En revision; si tiene dato sensible, exige justificacion | Alerta INFO si una ficha queda 15 dias en Borrador sin avanzar | OBL-DOC-02 (Art. 4 Medidas Organizativas, lit. d) |
| 16 | Karla | MOD-006 | Aprueba cada ficha (ella misma como Aprobador, con la misma advertencia de autorrevision) | Las fichas pasan a Vigente; se disparan alertas hacia MOD-007/008 segun corresponda | Alerta CRITICAL si a los 30 dias del diagnostico ninguna ficha esta Vigente | OBL-DOC-02; OBL-PRIN-02 (Art. 5 lit. g) |
| 17 | Karla | MOD-008 | Redacta y aprueba el Aviso de Privacidad y la Politica de Privacidad a partir de las plantillas precargadas por MOD-004 (checklist de los 9 literales del Art. 24 y de los 5 elementos del Art. 7 completos) | Documentos pasan de Borrador a En_revision a Aprobado a Publicado / Vigente; se calcula el hash de integridad; evidencia de publicacion en el historial propio del modulo | Alerta CRITICAL si no existe ninguna version publicada del Aviso pese a que ya hay tratamientos activos en el RAT | OBL-AVISO-01 (Art. 24); OBL-AVISO-05 (Art. 24 inc. 1); OBL-AVISO-04 (Art. 7) |
| 18 | Karla | MOD-021 / MOD-022 | Ejecuta, a lo largo del mes, las tareas CRITICA e IMPORTANTE del plan (cada una con su plazo calculado por MOD-023) y recibe las alertas correspondientes | Tareas pasan de Pendiente a En proceso a Completada; se genera evidencia en el historial de cada tarea | Cada tarea usa el plazo de su obligacion de origen, o el plazo por defecto de su prioridad (ver MOD-005, seccion G.2, regla 2) | Segun la obligacion de cada tarea |
| 19 | Karla | MOD-020 | Al cierre del primer mes, revisa el Dashboard en la vista de Responsable (pendientes) y en la vista de Gerencia (vision general en semaforos) | Vista recalculada en tiempo real; no genera evento de auditoria por ser solo lectura | Sin plazo propio | Buena practica (nunca se expresa como "porcentaje de cumplimiento legal") |
| 20 | Karla | MOD-026 | Consulta el Centro de Ayuda contextual en cada paso donde tuvo dudas (por ejemplo, "que es un Delegado de Proteccion de Datos", "por que debo publicar un Aviso de Privacidad") | Muestra la tarjeta de 4 partes (que es, por que, fundamento, cuando necesito ayuda juridica) | Sin plazo | Coherente con el principio de lenguaje claro, Art. 5 lit. e |

### Decisiones que el sistema NO toma

- **Si la empresa esta dentro del ambito de la LPDP o le corresponde alguna exclusion del Art. 3.** Texto que muestra el sistema: "Requiere validacion de la organizacion o asesoria especializada." (MOD-001, seccion H; MOD-004, seccion H).
- **Si Karla realmente necesita ser Delegada, o si le conviene un Delegado externo.** El sistema solo registra la respuesta del Paso 4 de MOD-003 y crea la tarea correspondiente; nunca concluye "su empresa no necesita Delegado". Texto: "Requiere validacion de la organizacion o asesoria especializada." (MOD-003, seccion H).
- **Si Karla cumple realmente el perfil legal exigido para ser Delegada** (grado universitario, mayor de 21 anos, experiencia acreditada, ausencia de sanciones firmes, Art. 5 Lineamientos DPO). El sistema solo ofrece el checklist de autoevaluacion. Texto: "Requiere validacion de la organizacion o asesoria especializada." (MOD-002, seccion H).
- **Si existe conflicto de intereses entre el cargo de Karla como Gerente Administrativa y su rol de Delegada.** El sistema registra la declaracion jurada y advierte sobre cargos tipicamente incompatibles, pero no decide el caso concreto (MOD-002, seccion H).
- **Aprobar automaticamente el Plan de Cumplimiento como Vigente.** El sistema nunca lo publica por su cuenta; siempre requiere la accion explicita del rol Aprobador, aunque en este caso ese rol lo ocupe la misma Karla con advertencia de autorrevision (MOD-005, seccion H).
- **Declarar que una accion "Completada" satisface la obligacion legal correspondiente.** El responsable debe declarar explicitamente que la evidencia cargada satisface la tarea (MOD-005, seccion H).
- **Decidir si el texto redactado del Aviso de Privacidad es legalmente adecuado mas alla de que el checklist estructural este completo.** Texto: "Este documento incluye las secciones minimas exigidas por la ley. Su contenido especifico requiere validacion de la organizacion o asesoria especializada." (MOD-008, seccion H).

### Alertas y escalamientos

| Alerta | Modulo | Nivel | Se dispara en este caso cuando | Escalamiento |
|---|---|---|---|---|
| Bienvenida: configure su organizacion | MOD-003 | INFO | La cuenta se crea y nadie inicia el wizard en 48 horas | Ninguno (aun no hay otro usuario) |
| Debe resolver si necesita un Delegado de Proteccion de Datos | MOD-003 | CRITICAL | Si Karla hubiera respondido "no estoy seguro" en el Paso 4 (en este caso no aplica, ella designa directamente) | A la vista de Gerencia a los 15 dias habiles |
| Falta nombrar Delegado/Responsable Interno | MOD-002 | CRITICAL | No existe ningun registro ACTIVO al finalizar el onboarding | A Aprobador a los 5 dias habiles |
| Comunicacion a la ACE por vencer / vencida | MOD-002 | WARNING / CRITICAL | Faltan 3 dias habiles del plazo de 15 dias, o el plazo vence sin enviarse | Visible en el dashboard de Gerencia si vence |
| Diagnostico nunca iniciado tras onboarding | MOD-004 | WARNING | Pasan mas de 7 dias sin iniciar la sesion | A Delegado a los 21 dias |
| Resultado con acciones criticas pendientes de asignar | MOD-004 | HIGH | El cierre del diagnostico deja alguna accion CRITICA sin tarea asignada | A Administrador a los 5 dias |
| Plan pendiente de aprobacion | MOD-005 | INFO/WARNING | La version queda en Generado o En revision mas de 2 dias habiles | A Gerencia a los 5 dias habiles |
| RAT sin ninguna ficha Vigente 30 dias despues del diagnostico | MOD-006 | CRITICAL | Ninguna ficha llega a Vigente en ese plazo | Aparece en el resumen ejecutivo de Gerencia a los 45 dias |
| Aviso de Privacidad sin publicar | MOD-008 | CRITICAL | No existe version Publicado/Vigente pese a tratamientos activos | Escala al Aprobador a los 5 dias habiles |

### Evidencia resultante

- **Ficha de organizacion con giro y tipos de tratamiento** (MOD-001): registro con fecha de creacion e historial de cada edicion; prueba OBL-AMB-01. Vive en el historial propio de MOD-001 y se conserva mientras la cuenta este activa.
- **Acta de nombramiento del Delegado, constancia de notificacion interna y comprobante de envio a la ACE** (MOD-002): archivo con hash, fecha, usuario; prueba OBL-DPO-01 a 03. Vive en el historial propio de MOD-002, historico indefinido.
- **Sesion cerrada del diagnostico, version 1** (MOD-004): registro exportable con verificacion de integridad, prueba que la empresa evaluo su aplicabilidad y sus tratamientos iniciales (OBL-AMB-01 a 04).
- **Plan de Cumplimiento v1, aprobado con hash de integridad** (MOD-005): snapshot congelado, prueba OBL-PLAZO-03.
- **Fichas del RAT en estado Vigente** (MOD-006): historial completo de aprobacion, prueba OBL-DOC-02.
- **Aviso de Privacidad y Politica de Privacidad publicados, con hash** (MOD-008): version vigente mas historico de versiones anteriores, prueba OBL-AVISO-01, OBL-AVISO-04 y OBL-AVISO-05.
- Toda esta evidencia queda disponible, ademas, para su consulta y exportacion consolidada desde MOD-019 Centro de Evidencias cuando el modulo la referencia (ver nota en "Contradicciones y huecos detectados" sobre el alcance exacto de esa referencia para MOD-001 y MOD-002).

### Variantes y casos borde

- **Pyme con una persona en varios roles (el caso base de este ejemplo).** Karla acumula Administradora, Delegada y Aprobador. El sistema muestra la advertencia de "autorrevision" en cada aprobacion que ella misma ejecuta sobre su propio trabajo (MOD-001, seccion H; `05_tipos_de_usuario.md`, seccion 5.4). Si la ferreteria superara el umbral configurable de 50 empleados, el sistema generaria la alerta "Umbral de separacion de funciones alcanzado" (MOD-001, seccion I) y ofreceria activar el bloqueo de acumulacion Aprobador + Auditor.
- **Empresa mediana o corporativo.** En Avicola San Andres o en Grupo Financiero Itzalco, el mismo recorrido reparte los roles: un Administrador de TI distinto del Delegado, un Aprobador de Gerencia distinto de quien redacta las fichas del RAT, y (en el caso del grupo corporativo) un onboarding independiente por cada sociedad, porque la vision consolidada multi-sociedad queda fuera del MVP (decision 2.7.31 de `02_validacion_de_la_idea.md`).
- **Doble estado de la reforma 659.** Si la bandera `regimen_reforma_659` de MOD-024 estuviera en FUTURO al momento del onboarding, el Paso 4 de MOD-003 seguiria preguntando por la misma figura, pero MOD-002 registraria a Karla con `tipo_rol = RESPONSABLE_INTERNO` en vez de `DELEGADO`, sin comunicacion obligatoria a la ACE (aunque el sistema seguiria permitiendo mantenerla voluntariamente). En este caso concreto (fecha de referencia 2026-09-24), la bandera esta en ACTUAL.

### Cobertura por version

Todos los modulos protagonistas de este caso son MUST HAVE (MOD-001, MOD-002, MOD-003, MOD-004, MOD-005, MOD-006, MOD-008, MOD-020, MOD-021, MOD-022, MOD-023, MOD-026), segun `02_validacion/mapa_modulos.json`: el caso completo, tal como esta descrito, ya funciona en el MVP. La unica limitacion de version dentro de este recorrido es que el calculo automatico del nivel de riesgo del RAT y la deteccion automatica de transferencias no documentadas dependen de MOD-014 y MOD-010 (ambos SHOULD HAVE), que en este caso 1 no llegan a activarse porque ninguno de los tratamientos declarados (personal, clientes, camaras convencionales sin reconocimiento facial) dispara esas reglas.

### Riesgos especificos del caso y su mitigacion

- **Riesgo de UX: abandono del onboarding o del diagnostico por complejidad percibida**, dado el perfil de Karla (conocimiento legal bajo-medio, sin tiempo). Mitigacion de diseno: wizard de 5 pasos con autoguardado (MOD-003), Centro de Ayuda contextual disponible en cada pantalla (MOD-026), lenguaje sencillo con el fundamento legal en segundo nivel.
- **Riesgo legal: dar por valida una designacion de Delegado sin verificar realmente los requisitos del Art. 5 Lineamientos DPO.** Mitigacion: el sistema nunca certifica el cumplimiento del perfil, solo ofrece el checklist de autoevaluacion con advertencia explicita (MOD-002, seccion H).
- **Riesgo operativo: que Karla, al acumular Administradora, Delegada y Aprobador, apruebe sin verdadero control cruzado su propio Plan de Cumplimiento y sus propias fichas del RAT.** Mitigacion: advertencia visible de autorrevision en cada aprobacion (MOD-001, seccion I, "Umbral de separacion de funciones alcanzado"; `05_tipos_de_usuario.md`, seccion 5.4).
- **Riesgo de plazo: perder el conteo de los 15 dias habiles para comunicar el nombramiento del Delegado a la ACE, por ser una empresa pequena sin equipo dedicado a plazos legales.** Mitigacion: el computo lo ejecuta siempre MOD-023 (nunca un calculo manual), con alertas escalonadas desde MOD-002 y MOD-022.

---

## Caso 2. La empresa registra un nuevo proceso

### Situacion de partida

Avicola San Andres, S.A. de C.V. (empresa mediana, unos 300 empleados, con areas separadas) decide sustituir el marcaje por tarjeta de sus dos plantas de produccion por un lector biometrico de huella digital para el control de asistencia del personal. Daniela Patricia Cornejo Lazo, Coordinadora de Recursos Humanos, debe registrar este tratamiento nuevo antes de que el equipo se active; Jorge Alberto Menendez Rauda (Jefe de Cumplimiento y Riesgo, Delegado interno en proceso de certificacion) y Roberto Antonio Villalta (Gerente de Tecnologia, Responsable de Seguridad/IT) intervienen en distintos puntos del recorrido, porque en una empresa mediana estos roles no se acumulan en una sola persona (`05_tipos_de_usuario.md`, seccion 5.3 y 5.4).

### Disparador

Daniela crea una ficha nueva en el Registro de Actividades de Tratamiento (MOD-006) para el tratamiento "Control de marcaje biometrico de personal", antes de instalar el equipo.

### Actores y modulos que intervienen

- **Daniela Patricia Cornejo Lazo**: Responsable de area (RRHH).
- **Jorge Alberto Menendez Rauda**: Delegado de Proteccion de Datos interno.
- **Roberto Antonio Villalta**: Responsable de Seguridad/IT.
- **Aprobador** (Gerencia, distinto de quien registra, por la regla de separacion de funciones de empresa mediana).
- Modulos: MOD-006 RAT y Mapa de Datos (propietario del caso), MOD-007 Consentimiento, MOD-008 Documentos y Politicas, MOD-009 Proveedores y Encargados, MOD-010 Transferencias Internacionales, MOD-014 Riesgos y EIPD, MOD-015 Controles de Seguridad, MOD-016 Retencion y Eliminacion, MOD-019 Centro de Evidencias, mas los transversales MOD-021, MOD-022, MOD-023.

### Diagrama del recorrido de extremo a extremo

```
  Daniela crea ficha en MOD-006 (Borrador)
  marca categoria "Informacion biometrica"
        |
        v
  MOD-006 dispara automatizaciones:
  exige justificacion + sugiere "Requiere EIPD: Si"
        |
        +-----------------+-----------------+------------------+
        v                 v                 v                  v
  MOD-007            MOD-008           MOD-009            MOD-014
  Consentimiento     Aviso RRHH        Proveedor del       EIPD
  (captura firmada)  (nueva version)   lector biometrico   (riesgo Alto)
        |                 |                 |                  |
        |                 |                 v                  v
        |                 |           MOD-010 (si aloja   MOD-015 Controles
        |                 |           datos fuera de SV)  (cifrado, acceso)
        |                 |                 |                  |
        +-----------------+-----------------+------------------+
                           |
                           v
                    MOD-016 Retencion
                 (regla para plantillas biometricas)
                           |
                           v
                MOD-006 ficha pasa a Vigente
             (bloqueada hasta enlazar un control
              de MOD-015, ver seccion I de esa ficha)
                           |
                           v
              MOD-019 Centro de Evidencias
        (consentimiento, EIPD, contrato/DPA y
         control quedan disponibles por referencia)
```

### Paso a paso

| Paso | Quien | Modulo | Que hace en el sistema | Que genera | Plazo y como se calcula | Fundamento |
|---|---|---|---|---|---|---|
| 1 | Daniela | MOD-006 | Crea la ficha "Control de marcaje biometrico de personal" en Borrador y marca la categoria de dato "Informacion biometrica" | Exige justificacion de base legal; sugiere automaticamente "Requiere EIPD: Si"; crea tarea "confirmar consentimiento escrito y alternativa no biometrica" enlazada a MOD-007 | Sin plazo propio de este paso | OBL-SENS-06 (Art. 4 lit. g); OBL-DOC-03 (Art. 4 Medidas Organizativas, colaboradora, propietaria MOD-014) |
| 2 | Daniela | MOD-006 | Elige la base de licitud (Consentimiento, reforzado por tratarse de dato sensible) y completa el resto de los campos obligatorios de Borrador | El sistema exige el campo de justificacion de base | Sin plazo propio | OBL-PRIN-02 (Art. 5 lit. g); OBL-SENS-07 (Art. 26 inc. 4, Art. 37) |
| 3 | Daniela | MOD-006 | Envia la ficha a revision | Pasa a En revision; crea tarea de revision para Jorge (Delegado); notifica al Aprobador porque el riesgo es Alto | Alerta WARNING si la ficha lleva 5 dias habiles sin decision | OBL-DOC-02 (Art. 4, lit. d) |
| 4 | Jorge | MOD-006 | Revisa la ficha; confirma que "Requiere EIPD" queda en Si antes de aprobar | Registra la decision explicita sobre EIPD (exigida por la ficha antes de pasar a Vigente) | Sin plazo propio | OBL-DOC-03 (Art. 4 Medidas Organizativas, propietaria MOD-014) |
| 5 | Daniela | MOD-007 | Presenta el aviso especifico de biometria laboral a cada persona empleada y captura el consentimiento (tipo Biometrico, con firma o medio equivalente obligatorio, y campo "alternativa no biometrica ofrecida") | Cada registro pasa de Presentado a Vigente; snapshot inmutable del texto y de la version del Aviso mostrada | Sin plazo legal propio de captura; alerta si queda en Presentado mas de 2 dias con tipo Biometrico sin firma adjunta | OBL-CONS-04 (Art. 26 inc. 4); OBL-SENS-02 (Art. 37 inc. 1); OBL-SENS-07 (Art. 26 inc. 4, Art. 37) |
| 6 | Jorge | MOD-008 | El RAT registra la nueva finalidad (marcaje biometrico) y el Aviso de RRHH vigente no la menciona; el sistema crea la tarea "Actualizar Aviso de Privacidad: nueva finalidad detectada" y pasa el documento a REQUIERE_REVISION | Se redacta una nueva version (Borrador -> En_revision -> Aprobado -> Publicado); la version anterior pasa a Historico | Alerta WARNING al dispararse; el disparo mismo no es desactivable | OBL-AVISO-04 (Art. 7); OBL-AVISO-01 (Art. 24) |
| 7 | Roberto | MOD-009 | Registra al proveedor del lector y del software biometrico como Encargado, vincula el tratamiento del RAT, envia a evaluacion | Pasa de Borrador a EN_EVALUACION; si el pais del proveedor es distinto de El Salvador, crea automaticamente el registro "pendiente de confirmar" en MOD-010 | Sin plazo legal propio; alerta HIGH si el vinculo con MOD-010 falla | OBL-PROV-01 (Art. 33 inc. 2) |
| 8 | Roberto | MOD-009 | Completa la evaluacion de riesgo y seguridad (nivel Alto, por combinar dato biometrico y alojamiento posiblemente extranjero) | Pasa a PENDIENTE_DE_CONTRATO; crea tarea "vincular contrato/DPA" | Sin plazo propio | OBL-PROV-02, OBL-PROV-03 (Art. 34) |
| 9 | Jorge | MOD-009 | Vincula el contrato/DPA vigente y aprueba la activacion; por ser riesgo Alto, exige doble control (aprobador distinto de quien registro) | Pasa a ACTIVO; programa la proxima revision en MOD-023; habilita los campos de contacto para el aviso | Sin plazo legal propio de este acto | OBL-PROV-01 (Art. 33 inc. 2) |
| 10 | Jorge | MOD-010 | Confirma que el registro detectado es una transferencia real (si el proveedor aloja las plantillas biometricas fuera de El Salvador), completa la evaluacion de pais y la base juridica | Pasa de DETECTADA_PENDIENTE_DE_CONFIRMAR a BORRADOR a EN_EVALUACION_DE_PAIS a PENDIENTE_DE_APROBACION; genera el borrador de puesta en conocimiento a la ACE en MOD-024 | Alerta HIGH si queda mas de 10 dias habiles en evaluacion sin completar | OBL-TRANSF-01 (Art. 40); OBL-TRANSF-03 (Art. 44 inc. 1) |
| 11 | Aprobador (Gerencia) | MOD-010 | Aprueba la transferencia (persona distinta de quien la redacto) | Pasa a ACTIVA; entra al Centro de Evidencias | Sin plazo legal propio de este acto especifico | OBL-TRANSF-04 (Art. 44 inc. final); OBL-TRANSF-05 (Art. 45) |
| 12 | Roberto | MOD-014 | Completa el cuestionario de la EIPD abierta automaticamente (DETECTADO -> ABIERTO); el sistema calcula el nivel de riesgo (Alto, por biometria) | Pasa a EVALUADO, luego a EN_MITIGACION (bloqueado hasta registrar al menos una mitigacion) | Sin plazo legal propio del cuestionario; buena practica: plazo interno por defecto de 15 dias habiles | OBL-DOC-03 (Art. 4 Medidas Organizativas) |
| 13 | Roberto | MOD-014 / MOD-015 | Registra las mitigaciones (cifrado de las plantillas biometricas, control de acceso reforzado al sistema); si una mitigacion no coincide con un control existente, se crea automaticamente un Control "pendiente de implementar" en MOD-015 | La EIPD pasa a PENDIENTE_DE_APROBACION; el Control queda visible en MOD-015 | Sin plazo legal propio | OBL-SEG-01 a 03 (Art. 35 y Art. 4 Medidas Tecnicas/Organizativas) |
| 14 | Jorge (o Responsable Interno, si aplica FUTURO) | MOD-014 | Aprueba la EIPD (debe ser persona distinta del responsable de la evaluacion, por ser riesgo Alto) | Pasa a VIGENTE; calcula la fecha de proxima revision (12 meses); genera evidencia formal | Sin plazo legal propio de este acto | OBL-DOC-03 |
| 15 | Roberto | MOD-015 | Implementa el control (cifrado, acceso reforzado) y adjunta evidencia | Pasa de Pendiente de implementar a Implementado; calcula la proxima fecha de revision | Alerta segun proximidad de revision (30/7 dias) | OBL-SEG-01 a 06 (Art. 35 y Art. 4) |
| 16 | Jorge | MOD-016 | Define la regla de retencion de las plantillas biometricas (sugerida automaticamente al registrarse dato sensible con proveedor potencialmente extranjero) | Regla en estado ACTIVO, con fecha efectiva calculada | Sin plazo legal propio (plazo depende del fundamento elegido: relacion laboral vigente + periodo adicional) | Buena practica, con referencia a OBL-RET-01/02 segun el fundamento aplicable |
| 17 | Daniela | MOD-006 | Con el consentimiento capturado, el Aviso actualizado, el proveedor activo y al menos un control de MOD-015 enlazado, confirma la ficha del RAT | Pasa de En revision a Vigente (el sistema bloquea este paso mientras no exista un control de MOD-015 enlazado a un dato biometrico, alerta HIGH "Dato biometrico sin control de seguridad enlazado") | Sin plazo legal propio | OBL-DOC-02 (Art. 4, lit. d) |
| 18 | Sistema | MOD-019 | Cada aprobacion anterior (consentimiento en MOD-007, EIPD en MOD-014, contrato/DPA en MOD-009, control en MOD-015) crea automaticamente su Evidencia correspondiente, en estado Disponible, por referencia | Paquete de evidencia consultable y exportable con verificacion de integridad | Sin plazo propio; alerta si alguna evidencia con vigencia definida esta por vencer | OBL-PRIN-03 (Art. 5 lit. i) |

### Decisiones que el sistema NO toma

- **Si la base de licitud elegida (Consentimiento reforzado) es valida y proporcional para este tratamiento concreto.** Texto: "La eleccion de esta base requiere el criterio de su organizacion sobre si es defendible para este tratamiento especifico. Requiere validacion de la organizacion o asesoria especializada." (MOD-006, seccion H).
- **Si el consentimiento sigue siendo "libre" en una relacion de subordinacion laboral** (marcaje biometrico de empleados). El sistema solo registra si se ofrecio una alternativa no biometrica; no concluye si eso hace al consentimiento valido (MOD-007, seccion H).
- **Si el nivel de riesgo calculado automaticamente por MOD-014 (Alto) refleja el riesgo real del tratamiento.** Texto: "Este resultado es un calculo de apoyo interno basado en los factores que usted registro. No es una conclusion juridica sobre la legalidad del tratamiento. Requiere validacion de la organizacion o asesoria especializada." (MOD-014, seccion H).
- **Si el pais donde el proveedor del lector biometrico aloja los datos tiene "nivel de proteccion adecuado" (Art. 44).** Ni la ley ni la ACE atribuyen esa calificacion a ningun organo; el sistema muestra el cuestionario de factores y exige confirmacion humana (MOD-010 y MOD-009, seccion H).
- **Si el subencargado del proveedor (si lo hay) queda efectivamente sometido a la LPDP.** Texto: "Requiere validacion de la organizacion o asesoria especializada." (MOD-009, seccion H).
- **Aceptar el riesgo residual de la EIPD.** El paso de EN_MITIGACION a PENDIENTE_DE_APROBACION nunca ocurre solo porque el calculo baje de Alto a Medio; siempre requiere aprobacion explicita de una persona distinta del responsable de la evaluacion (MOD-014, seccion H).
- **Aprobar la eliminacion definitiva de las plantillas biometricas cuando termine la relacion laboral.** El sistema calcula cuando el dato "puede" eliminarse; ejecutar la eliminacion siempre requiere aprobacion humana explicita (MOD-016, seccion H).

### Alertas y escalamientos

| Alerta | Modulo | Nivel | Se dispara en este caso cuando | Escalamiento |
|---|---|---|---|---|
| Tratamiento con dato sensible sin justificacion de base | MOD-006 | HIGH | Se intenta guardar la ficha sin el campo de justificacion completo (bloqueo en pantalla) | No aplica, es bloqueo |
| Dato biometrico sin control de seguridad enlazado | MOD-006 | HIGH | La ficha intenta pasar a Vigente sin un control de MOD-015 enlazado | No aplica, es bloqueo de aprobacion |
| Transferencia posiblemente no documentada | MOD-006 | HIGH | El tratamiento declara transferencia sin ficha correspondiente en MOD-010 | A los 15 dias, al Administrador |
| Consentimiento sensible incompleto | MOD-007 | WARNING | Un registro Biometrico queda mas de 2 dias sin firma adjunta | A Administrador tras 5 dias |
| Consentimiento biometrico sin alternativa ofrecida | MOD-007 | WARNING | Se guarda un consentimiento Biometrico con "alternativa no biometrica ofrecida = No" | A Delegado si se repite en el mismo tratamiento |
| Aviso de Privacidad no menciona un encargado nuevo | MOD-008 | HIGH | MOD-009 registra un encargado y el Aviso vigente no lo lista en el literal h) | A Administrador tras 5 dias habiles |
| Contrato/DPA proximo a vencer | MOD-009 | WARNING / HIGH | Faltan 30 o 7 dias para el vencimiento | Escala a Aprobador o a Administrador |
| Pais fuera de El Salvador sin registro vinculado en Transferencias | MOD-009 | HIGH | La creacion automatica del registro en MOD-010 falla o se pierde | A Administrador si persiste 5 dias |
| Transferencia internacional sin evaluacion de pais completa | MOD-010 | HIGH | Mas de 10 dias habiles en EN_EVALUACION_DE_PAIS | A Administrador a los 20 dias habiles |
| Tratamiento de alto riesgo sin EIPD | MOD-014 | WARNING/HIGH | El cuestionario no se completa dentro del plazo interno configurado | A Delegado tras 5 dias habiles sin avance |
| EIPD con riesgo Alto pendiente de mitigacion | MOD-014 | HIGH | La EIPD entra en EN_MITIGACION | A Aprobador/Gerencia tras 10 dias habiles |
| Control obligatorio sin evidencia | MOD-015 | HIGH | El control permanece en Pendiente de implementar mas de 30 dias | A Gerencia a los 60 dias, con referencia al riesgo de infraccion grave |

### Evidencia resultante

- **Ficha del RAT en Vigente, con su historial de justificacion de base y de aprobacion** (MOD-006): prueba OBL-DOC-02 y OBL-PRIN-02; vive en el historial propio de MOD-006.
- **Consentimientos firmados con snapshot del texto y de la version del Aviso** (MOD-007): prueba OBL-CONS-04, OBL-CONS-05 y OBL-SENS-02; disponible en MOD-019 desde su aprobacion.
- **Contrato/DPA vigente y evaluacion de riesgo del proveedor** (MOD-009): prueba OBL-PROV-01 a 03; disponible en MOD-019.
- **Registro de transferencia aprobado, con evidencia de puesta en conocimiento a la ACE** (MOD-010): prueba OBL-TRANSF-01, 03, 04 y 05; disponible en MOD-019.
- **EIPD aprobada con mitigaciones registradas** (MOD-014): prueba OBL-DOC-03; disponible en MOD-019.
- **Control de seguridad implementado con evidencia adjunta** (MOD-015): prueba OBL-SEG-01 a 06; disponible en MOD-019.
- **Regla de retencion activa sobre las plantillas biometricas** (MOD-016): referencia de cuando y bajo que fundamento se eliminaran.
- Todo lo anterior queda consolidado y exportable con verificacion de integridad desde MOD-019 Centro de Evidencias, porque los seis modulos de origen (MOD-007, MOD-009, MOD-010, MOD-014, MOD-015, MOD-016) estan dentro del rango que la propia ficha de MOD-019 declara como alimentacion automatica (MOD-007 a MOD-018).

### Variantes y casos borde

- **Pyme con una persona en varios roles.** Si Ferreteria y Suministros El Roble hiciera este mismo cambio, Karla concentraria los roles de Responsable de area, Delegada y (con advertencia de autorrevision) Aprobador; el doble control de la evaluacion de proveedor de riesgo Alto (paso 9) se mostraria igual, pero con la advertencia de que el mismo Aprobador no deberia coincidir con quien registro, salvo confirmacion explicita en pyme (MOD-009, seccion F, tabla de transiciones).
- **Grupo corporativo.** En Grupo Financiero Itzalco, si el banco del grupo implementara el mismo lector biometrico, la ficha del RAT, el consentimiento, el proveedor y la EIPD se registrarian de forma independiente para esa sociedad especifica (la vision consolidada multi-sociedad es V1/Enterprise, no MVP).
- **Doble estado de la reforma 659.** Si la bandera estuviera en FUTURO, el paso 14 (aprobacion de la EIPD) la ejecutaria la persona con `tipo_rol = RESPONSABLE_INTERNO` en vez de Delegado, sin que eso cambie el contenido tecnico de la evaluacion (MOD-014, seccion G, regla 6).

### Cobertura por version

MOD-006, MOD-007, MOD-008, MOD-009, MOD-015 y MOD-019 son MUST HAVE: el nucleo de este caso (alta del tratamiento, consentimiento, aviso, proveedor y controles) ya funciona en el MVP. MOD-010 (Transferencias) y MOD-014 (Riesgos y EIPD) son SHOULD HAVE. Segun la nota de cobertura parcial de sus propias fichas de MVP: si MOD-014 no esta construido todavia, el Diagnostico o el RAT igual detectan la biometria y crean una tarea "elaborar EIPD" en MOD-021 con una plantilla generica en MOD-008, llenada manualmente, sin el motor de scoring (MOD-014, seccion Q); si MOD-010 no esta construido, el registro de la transferencia se cubre con la deteccion manual desde el Diagnostico, sin el motor de deteccion automatica de transferencias no documentadas (MOD-010, seccion Q). MOD-016 (Retencion) tambien es SHOULD HAVE: mientras no exista, la conservacion pasiva ya ocurre porque MOD-008 y MOD-011 no permiten eliminar antes de su plazo minimo, aunque sin el estado visible ni la alerta formal que aporta MOD-016 (MOD-016, seccion Q).

### Riesgos especificos del caso y su mitigacion

- **Riesgo legal: registrar un tratamiento biometrico sin verificar realmente que el consentimiento sea "libre" en un contexto de subordinacion laboral.** Mitigacion de diseno: campo obligatorio "alternativa no biometrica ofrecida" con advertencia si es "No" (MOD-007, seccion I).
- **Riesgo operativo: que el proveedor del lector biometrico aloje las plantillas fuera de El Salvador sin que nadie lo detecte a tiempo.** Mitigacion: creacion automatica del registro "pendiente de confirmar" en MOD-010 en cuanto MOD-009 registra un pais distinto de El Salvador (MOD-009, seccion G, regla 1).
- **Riesgo de seguridad: implementar el lector biometrico sin cifrado ni control de acceso reforzado sobre las plantillas.** Mitigacion: la ficha del RAT no puede pasar a Vigente sin un control de MOD-015 enlazado a la categoria "Informacion biometrica" (MOD-006, seccion I).
- **Riesgo de UX: que Roberto (Seguridad/IT) perciba el cuestionario de la EIPD como carga tecnica ajena a su rol.** Mitigacion: ayuda contextual de MOD-026 en cada campo del cuestionario, y reutilizacion del mismo catalogo de controles de MOD-015 que el ya administra.

---

## Caso 3. Marketing implementa un nuevo formulario

### Situacion de partida

Grupo Financiero Itzalco (corporativo con banco, aseguradora y financiera bajo una misma holding) prepara, dentro de la sociedad aseguradora del grupo, el lanzamiento de un nuevo producto: el "Plan de Ahorro y Proteccion Familiar", dirigido a padres y madres de familia e incluye, como beneficiario, a un hijo o hija menor de edad. El area de Mercadeo de la aseguradora capta datos por dos canales: una feria presencial en un centro comercial (stand con tableta) y una landing page en el sitio web de la aseguradora. El formulario recoge nombre, DUI, telefono, correo y direccion del padre o madre solicitante, mas nombre y fecha de nacimiento del hijo o hija beneficiario. Lic. Mauricio Ernesto Aguilar Sandoval, Delegado certificado dedicado a la sociedad aseguradora, es quien aprueba los actos legales de esta campana; Licda. Ana Gabriela Reyes Portillo, Directora de Cumplimiento Corporativo, supervisa a nivel de grupo sin sustituir la aprobacion especifica de la sociedad.

### Disparador

El area de Mercadeo solicita a Cumplimiento habilitar el nuevo formulario (web y feria) antes de la fecha del evento.

### Actores y modulos que intervienen

- **Responsable de area (Mercadeo)** de la aseguradora.
- **Lic. Mauricio Ernesto Aguilar Sandoval**: Delegado de Proteccion de Datos (dedicado a la sociedad aseguradora).
- **Responsable Legal / Compliance** de la sociedad (o Ana Gabriela a nivel de grupo, en consulta).
- **Responsable de Seguridad/IT** (evaluacion del proveedor de la herramienta de marketing).
- Modulos: MOD-006 RAT y Mapa de Datos (alta del tratamiento "Captacion de leads - Plan de Ahorro y Proteccion Familiar"), MOD-007 Consentimiento (consentimiento especifico por finalidad y sub-flujo parental), MOD-008 Documentos y Politicas (informacion en el punto de recoleccion), MOD-009 Proveedores y Encargados (herramienta de automatizacion de marketing), MOD-010 Transferencias Internacionales (si esa herramienta aloja datos fuera de El Salvador), MOD-011 ARCO-POL (oposicion a mercadotecnia directa), MOD-014 Riesgos y EIPD (dato de menor con finalidad de mercadeo), mas los transversales MOD-021, MOD-022, MOD-023 y MOD-026.

### Diagrama del recorrido de extremo a extremo

```
   Mercadeo disena el formulario (web + feria)
                  |
                  v
   MOD-006: alta del tratamiento "Captacion de leads"
   (marca "Incluye menores de edad: Si")
                  |
      +-----------+-----------+
      v                       v
  MOD-008                MOD-007
  Aviso en el punto de    Consentimiento especifico
  recoleccion (Art. 7     por finalidad + sub-flujo
  y Art. 24)              parental (titular NNA)
      |                       |
      v                       v
  MOD-009 Proveedor       (si titular no consiente
  (herramienta de          o declina: no se guarda
  marketing)               el dato, se documenta)
      |
      v
  MOD-010 (si el proveedor
  aloja datos fuera de SV)
      |
      v
  MOD-014 EIPD (si aplica por
  combinar dato de menor +
  finalidad de mercadeo)
      |
      v
  Formulario activo (feria y web)
      |
      +-------------------------------+
      v                                v
  Titular pide retirar su         Titular se opone a la
  consentimiento (MOD-007,        mercadotecnia directa
  5 + 5 dias habiles)             (MOD-011, Oposicion)
      |                                |
      v                                v
  Lista de supresion de marketing (enlace MOD-007 / MOD-011)
```

### Paso a paso

| Paso | Quien | Modulo | Que hace en el sistema | Que genera | Plazo y como se calcula | Fundamento |
|---|---|---|---|---|---|---|
| 1 | Responsable de Mercadeo | MOD-006 | Crea la ficha "Captacion de leads - Plan de Ahorro y Proteccion Familiar" en Borrador; marca finalidad de mercadeo directo, categorias de datos de contacto y "Incluye menores de edad: Si" | El sistema sugiere automaticamente "Requiere EIPD" a confirmar, por la combinacion de menores y finalidad de mercadeo | Sin plazo propio | OBL-CONS-05 (colaboradora, Art. 54); OBL-DOC-03 (propietaria MOD-014) |
| 2 | Responsable de Mercadeo | MOD-006 | Elige base de licitud (Consentimiento, dado que es mercadeo directo) y completa los campos obligatorios de Borrador | Exige justificacion de base | Sin plazo propio | OBL-PRIN-02 (Art. 5 lit. g) |
| 3 | Mauricio (Delegado) | MOD-006 | Revisa y confirma la decision sobre EIPD antes de aprobar la ficha | Ficha pasa a Vigente; dispara alertas hacia MOD-007, MOD-008, MOD-009 | Sin plazo propio | OBL-DOC-02 (Art. 4, lit. d) |
| 4 | Responsable Legal / Mercadeo | MOD-008 | Redacta o actualiza el texto de informacion en el punto de recoleccion (banner en la landing page y hoja informativa en el stand de la feria), verificando el checklist de los 5 elementos del Art. 7 y, para el Aviso de Privacidad completo enlazado, los 9 literales del Art. 24 | Documento en Borrador -> En_revision -> Aprobado -> Publicado; hash de integridad | Alerta CRITICAL si no existe version publicada mientras el formulario ya capta datos | OBL-AVISO-04 (Art. 7); OBL-AVISO-01 (Art. 24) |
| 5 | Titular (padre/madre) | MOD-007 | En la landing page o en la tableta de la feria, ve el aviso de informacion y otorga consentimiento especifico para la finalidad de mercadeo; marca "Titular es NNA = Si" para los datos del hijo o hija beneficiario y declara la relacion de parentesco | Registro Presentado -> Vigente (adulto) y registro parental para el menor con nombre del padre/madre que consiente y relacion declarada | Sin plazo legal de captura; snapshot inmutable del texto y version del aviso vistos | OBL-CONS-01 (Art. 26 y 27); OBL-CONS-06 (Art. 56 lit. c num. 3, Art. 5 lit. j, Art. 42); OBL-PRIN-04 (Art. 5 lit. j) |
| 6 | Titular (padre/madre) | MOD-007 | Si declina, el sistema no guarda el dato del formulario mas alla de la constancia de que se le informo el derecho a no darlo | Registro pasa a No otorgado | Sin plazo | OBL-SENS-02 no aplica aqui (dato no sensible); buena practica de trazabilidad |
| 7 | Responsable de Seguridad/IT | MOD-009 | Registra la herramienta de automatizacion de marketing usada para gestionar los leads como Encargado, vincula el tratamiento del RAT | Pasa de Borrador a EN_EVALUACION; si el pais de alojamiento es distinto de El Salvador, crea automaticamente el registro "pendiente de confirmar" en MOD-010 | Sin plazo propio | OBL-PROV-01 (Art. 33 inc. 2) |
| 8 | Mauricio | MOD-009 | Aprueba la evaluacion y vincula el contrato/DPA | Pasa a ACTIVO | Alerta WARNING/HIGH segun vencimiento del contrato | OBL-PROV-01 a 03 |
| 9 | Responsable Legal | MOD-010 | Si el registro se confirma como transferencia real, completa la evaluacion de pais y la base juridica (por ejemplo, consentimiento previo especifico) | Pasa a EN_EVALUACION_DE_PAIS -> PENDIENTE_DE_APROBACION -> ACTIVA | Alerta HIGH si excede 10 dias habiles sin completar | OBL-TRANSF-01 (Art. 40); OBL-TRANSF-04 (Art. 44 inc. final) |
| 10 | Roberto o equivalente | MOD-014 | Completa el cuestionario de riesgo activado por combinar dato de menor y finalidad de mercadeo | Calcula el nivel de riesgo; si es Alto, bloquea el paso directo a aprobacion hasta registrar mitigacion | Sin plazo legal propio | OBL-DOC-03 (Art. 4 Medidas Organizativas) |
| 11 | Mauricio | MOD-014 | Aprueba la EIPD (si aplico) antes de que el formulario quede definitivamente activo | Pasa a VIGENTE | Sin plazo propio | OBL-DOC-03 |
| 12 | Titular (padre/madre) | MOD-007 | Meses despues, solicita revocar el consentimiento de mercadeo para el o para su hijo/hija | Se crea el registro ConsentWithdrawal en Recibida; se calcula la fecha limite de ejecucion | 5 dias habiles desde la recepcion (MOD-023) | OBL-CONS-03 (Art. 30) |
| 13 | Mauricio | MOD-007 | Valida y ejecuta la revocacion (deja de tratar el dato para esa finalidad) | Pasa a Ejecutada; el Consent origen pasa a Revocado | Igual al paso anterior | OBL-CONS-03 (Art. 30) |
| 14 | Responsable de Seguridad/IT | MOD-007 / MOD-009 | Si el tratamiento tiene encargado (la herramienta de marketing), se notifica la revocacion al encargado | Pasa a Encargado notificado -> Cerrada | 5 dias habiles adicionales desde la ejecucion (MOD-023) | OBL-CONS-04 (Art. 26 inc. 4, segundo tramo) |
| 15 | Sistema | MOD-007 | Si la finalidad revocada incluye marketing directo, envia automaticamente al titular a la lista de supresion de marketing, enlazada con la oposicion de MOD-011 | Entrada en la lista de supresion, referenciada desde MOD-011 | Automatico al ejecutarse la revocacion | Buena practica (faltante 29 de `02_validacion_de_la_idea.md`) |
| 16 | Titular (distinto, ejemplo alterno) | MOD-011 | En vez de revocar el consentimiento, presenta una solicitud ARCO-POL marcando derecho "Oposicion" y "Es oposicion a mercadotecnia directa / perfilado: Si" | Expediente Nueva/Recibida -> Verificando identidad -> Evaluando requisitos Art. 18 -> Admitida | Contador de 20 dias habiles desde Admitida (MOD-023) | OBL-ARCO-05 (Art. 12) |
| 17 | Mauricio | MOD-011 | Analiza la procedencia (no hay interes legitimo prevalente que la contradiga) y aprueba el reconocimiento | Expediente pasa a Reconocida; al reconocerse la oposicion a mercadotecnia, se envia automaticamente el dato del titular a la lista de supresion de MOD-007/Consentimiento | Sin plazo adicional a los 20 dias habiles ya corridos | OBL-ARCO-05 (Art. 12) |

### Decisiones que el sistema NO toma

- **Si el texto del aviso mostrado en el punto de recoleccion (banner web y hoja de la feria) es legalmente suficiente mas alla de que el checklist estructural de los 5 elementos del Art. 7 y los 9 literales del Art. 24 este completo.** Texto: "Este documento incluye las secciones minimas exigidas por la ley. Su contenido especifico requiere validacion de la organizacion o asesoria especializada." (MOD-008, seccion H).
- **Si un adolescente (12 a 18 anos) podria autoconsentir bajo la Ley Crecer Juntos en vez de requerir siempre consentimiento parental bajo la LPDP.** El sistema siempre pide el flujo parental completo por defecto (criterio conservador) y muestra la tension como nota visible: "Existe una tension entre la LPDP (consentimiento parental) y la Ley Crecer Juntos... Requiere validacion de la organizacion o asesoria especializada." (MOD-007, seccion H; MOD-011, seccion D.5 y F.3).
- **La ponderacion de interes legitimo prevalente para negar una oposicion a mercadotecnia directa (Art. 12).** No existe formula ni umbral legal para "prevalencia"; requiere criterio humano (MOD-011, seccion H).
- **Si un encargado extranjero (la herramienta de marketing, si aloja datos fuera de El Salvador) cuenta como "transferencia" o como simple encargo de tratamiento.** El sistema aplica el criterio conservador (tratarlo como transferencia) pero lo muestra como decision pendiente de confirmar (MOD-009 y MOD-010, seccion H).
- **La aprobacion final de la notificacion de revocacion**, tanto al titular como al encargado. El sistema calcula el plazo y prepara el contenido, pero la emision requiere aprobacion explicita del Delegado o Responsable interno segun el estado vigente (MOD-007, seccion H).
- **Resolver la solicitud de oposicion en si misma.** El sistema calcula el plazo, presenta las causales tasadas y prepara el borrador; el Delegado decide y aprueba antes de que cualquier acto se considere emitido (MOD-011, seccion H).

### Alertas y escalamientos

| Alerta | Modulo | Nivel | Se dispara en este caso cuando | Escalamiento |
|---|---|---|---|---|
| Aviso de Privacidad sin publicar | MOD-008 | CRITICAL | El formulario ya capta datos sin version publicada de aviso | Escala al Aprobador tras 5 dias habiles |
| Consentimiento sensible incompleto (aplicado al sub-flujo parental) | MOD-007 | WARNING | El registro parental queda incompleto (falta relacion o evidencia recomendada) mas de 2 dias | A Administrador tras 5 dias |
| Revocacion proxima a vencer / vencida (primer plazo) | MOD-007 | WARNING / CRITICAL | Faltan 2 dias habiles de los 5, o el plazo vence sin ejecutar | Inmediato a Administrador y Gerencia si vence |
| Notificacion a encargado proxima a vencer / vencida (segundo plazo) | MOD-007 | WARNING / CRITICAL | Faltan 2 dias habiles de los 5 adicionales, o vence | Inmediato a Administrador si vence |
| Transferencia detectada automaticamente sin confirmar | MOD-010 | WARNING | Alta del proveedor de marketing con pais distinto de El Salvador | A Delegado a los 15 dias habiles |
| Plazo general proximo a vencer / vencido (Oposicion) | MOD-011 | HIGH / CRITICAL | Faltan 5 dias habiles de los 20, o vencen sin resolucion | Escala a Gerencia si vence |
| Tratamiento de alto riesgo sin EIPD | MOD-014 | WARNING/HIGH | El cuestionario de riesgo (menor + mercadeo) no se completa a tiempo | A Delegado tras 5 dias habiles |

### Evidencia resultante

- **Ficha del RAT vigente para "Captacion de leads"** (MOD-006): prueba OBL-DOC-02.
- **Aviso publicado en el punto de recoleccion, con hash** (MOD-008): prueba OBL-AVISO-01 y OBL-AVISO-04.
- **Consentimientos capturados (adulto y sub-flujo parental), con snapshot del texto y firma o medio equivalente** (MOD-007): prueba OBL-CONS-01, OBL-CONS-04, OBL-CONS-06; disponible en MOD-019.
- **Expediente de revocacion cerrado, con evidencia de ejecucion y de notificacion al encargado** (MOD-007): prueba OBL-CONS-03; disponible en MOD-019.
- **Expediente ARCO-POL de oposicion, con resolucion de reconocimiento y entrada en la lista de supresion** (MOD-011): prueba OBL-ARCO-05; retencion de 5 anos (OBL-RET-05) desde el cierre.
- **Contrato/DPA del proveedor de marketing y, si aplica, registro de transferencia aprobado** (MOD-009 y MOD-010): prueba OBL-PROV-01 a 03 y OBL-TRANSF-01/04.
- Todo lo anterior queda disponible y exportable con verificacion de integridad desde MOD-019 Centro de Evidencias.

### Variantes y casos borde

- **Pyme con una persona en varios roles.** Si Ferreteria y Suministros El Roble lanzara una promocion similar (por ejemplo, un formulario de feria comercial para un sorteo), Karla concentraria Responsable de Mercadeo, Delegada y Aprobador, con la misma advertencia de autorrevision al aprobar el aviso y el consentimiento.
- **Grupo corporativo (caso base de este ejemplo).** La aprobacion legal del formulario, del consentimiento y de la oposicion es siempre de Mauricio como Delegado de la sociedad aseguradora, nunca de Ana Gabriela a nivel de grupo, aunque ella tenga visibilidad de supervision (rol de grupo es V1/Enterprise, no MVP, `05_tipos_de_usuario.md`, perfil 5).
- **Doble estado de la reforma 659.** Si la bandera estuviera en FUTURO al momento de una revocacion o de una oposicion, quien aprueba el acto pasa a ser la persona con `tipo_rol = RESPONSABLE_INTERNO` en vez de Delegado, sin cambiar los plazos de 5+5 dias ni el de 20 dias habiles (MOD-007, seccion G, regla 9; MOD-011, seccion G, regla 14).
- **Menor no aplica.** Si el mismo formulario no capturara datos de beneficiarios menores (por ejemplo, una campana de seguro de auto sin hijos involucrados), el paso del sub-flujo parental de MOD-007 simplemente no se activa, y la EIPD del paso 10 solo se dispararia si otro factor de riesgo estuviera presente.

### Cobertura por version

MOD-006, MOD-007, MOD-008, MOD-009, MOD-011 son MUST HAVE: el nucleo de este caso (alta del tratamiento, aviso en el punto de recoleccion, consentimiento especifico, proveedor de marketing y oposicion/revocacion) ya funciona en el MVP. MOD-010 (Transferencias) y MOD-014 (Riesgos y EIPD) son SHOULD HAVE, con el mismo mecanismo de cobertura parcial descrito en el Caso 2: mientras no esten construidos, el registro manual desde el Diagnostico y una plantilla generica de EIPD en MOD-008 cubren el minimo legal, sin el motor automatico completo (MOD-010 y MOD-014, seccion Q).

### Riesgos especificos del caso y su mitigacion

- **Riesgo legal: tratar datos de un menor de edad sin el sub-flujo de consentimiento parental completo, por la presion de tiempo de una feria presencial.** Mitigacion de diseno: el campo "Titular es NNA" activa obligatoriamente los campos parentales antes de guardar (MOD-007, seccion G, regla 3); no hay forma de omitirlo desde la interfaz.
- **Riesgo de UX: que el personal de Mercadeo en el stand de la feria no capture correctamente la evidencia de consentimiento por la premura del evento.** Mitigacion: el mismo formulario de captura (tableta) se usa en ambos canales (web y feria), con snapshot automatico del texto y de la version del aviso, sin depender de que el promotor redacte nada a mano.
- **Riesgo operativo: que la herramienta de automatizacion de marketing aloje los leads fuera de El Salvador sin que nadie lo detecte hasta despues del lanzamiento.** Mitigacion: creacion automatica del registro "pendiente de confirmar" en MOD-010 en cuanto MOD-009 registra el pais del proveedor (MOD-009, seccion G, regla 1).
- **Riesgo reputacional: que un titular se oponga a la mercadotecnia directa y la empresa siga contactandolo por no sincronizar la lista de supresion entre el flujo de revocacion (MOD-007) y el de oposicion (MOD-011).** Mitigacion: ambos flujos alimentan la misma lista de supresion por diseno (MOD-007, seccion G, regla 8; MOD-011, seccion G, regla 13).

---

## Contradicciones y huecos detectados

Esta seccion enumera, siguiendo la jerarquia indicada en el encargo (fuente legal primaria y `matriz_obligaciones.json` > `mapa_modulos.json` y `06_mapa_definitivo_de_modulos.md` > `05_tipos_de_usuario.md` para roles > ficha del modulo propietario > otras fichas), las contradicciones y huecos encontrados al redactar los casos 1 a 3.

### Contradicciones

1. **Alcance de la alimentacion automatica hacia MOD-019 Centro de Evidencias.** La tabla de automatizaciones de `MOD-019_ficha.md` (seccion G) limita la creacion automatica de Evidencia a "un modulo estructurado (MOD-007 a MOD-018)", lo que excluye de forma literal a MOD-001 (Organizacion y Personas), MOD-002 (Delegado) y MOD-006 (RAT). Sin embargo, la propia seccion J de `MOD-001_ficha.md` ("Exportacion firmada del listado de usuarios y roles... insumo del paquete de evidencia que arma MOD-019") y la nota final de `MOD-002_ficha.md` ("toda exportacion hacia el paquete de evidencias de MOD-019 incluye un mecanismo propio de verificacion de integridad") dan por hecho que su evidencia si llega a MOD-019. Se adopto, para el Caso 1, la lectura de que la evidencia de MOD-001, MOD-002 y MOD-006 vive primero en el historial propio de cada modulo y se consolida en MOD-019 por referencia o exportacion, sin asumir que la tabla de automatizacion de MOD-019 (pensada para el rango 007-018) sea una lista cerrada que excluye a los modulos anteriores; se prefirio esta lectura porque MOD-019 se define en su propia seccion A como la respuesta a "que evidencia tenemos de esta obligacion" para cualquier obligacion del sistema, no solo para las de MOD-007 a MOD-018. Se recomienda que una revision posterior de `MOD-019_ficha.md` seccion G aclare de forma expresa si MOD-001, MOD-002, MOD-003, MOD-004, MOD-005, MOD-006, MOD-020, MOD-023 y MOD-024 tambien alimentan la Evidencia de forma automatica o solo por referencia manual.
2. **Nombres de rol de la plantilla de ficha frente a los 12 roles estandar.** `00_plantilla_ficha_modulo.md`, seccion B, enumera un catalogo de roles de ejemplo ("Responsable de privacidad, Gestor ARCO-POL, Legal, IT/Seguridad, RRHH, Marketing") que no coincide exactamente con los 12 roles estandar definidos despues en `05_tipos_de_usuario.md`, seccion 5.3 ("Delegado de Proteccion de Datos", "Responsable ARCO-POL / Responsable del tramite", "Responsable Legal / Compliance", "Responsable de Seguridad / IT", "Responsable de area"). Esta seccion 8 usa en todos sus casos exclusivamente los nombres de `05_tipos_de_usuario.md` seccion 5.3, por ser la fuente mas reciente y mas especifica sobre roles, segun la jerarquia del encargo; la plantilla de ficha es un documento de trabajo anterior y no se cita como fuente de nombres de rol.

### Huecos (pasos o piezas que ninguna ficha define)

1. **Hueco: no definido en la ficha de ningun modulo.** Ninguna ficha (ni MOD-006, ni MOD-009, ni MOD-010) define un paso explicito de "verificar si la herramienta de automatizacion de marketing usada en una campana puntual (por ejemplo, para una feria de duracion de un dia) requiere el mismo flujo completo de evaluacion de proveedor que un Encargado permanente", o si existe una version simplificada para relaciones de muy corta duracion. El Caso 3 aplico el flujo completo de MOD-009 por ser la unica ruta definida, marcandolo como el criterio por defecto hasta que una ficha lo aclare.
2. **Hueco: no definido en la ficha de MOD-007 ni de MOD-011.** Ninguna de las dos fichas especifica que sucede cuando el mismo titular revoca el consentimiento de mercadeo (MOD-007) y, ademas, presenta una solicitud de oposicion formal (MOD-011) para el mismo tratamiento: no hay una regla de deduplicacion entre el flujo de revocacion y el flujo ARCO-POL de oposicion, mas alla de que ambos alimentan la misma lista de supresion. El Caso 3 los presento como dos rutas alternativas e independientes (pasos 12 a 15 frente a pasos 16 y 17), sin fusionarlas, por ser la unica forma de mantenerse fiel a lo que cada ficha define por separado.
3. **Hueco: no definido en la ficha de MOD-008.** La ficha de MOD-008 no aclara si el "texto de informacion en el punto de recoleccion" de un evento presencial (por ejemplo, una hoja o cartel en un stand de feria) es un documento propio con su propio ciclo de aprobacion, o una vista reducida del mismo Aviso de Privacidad publicado para el canal web. El Caso 3 lo trato como parte del mismo documento de tipo Aviso de Privacidad (con el mismo checklist del Art. 7 y del Art. 24), por ser la lectura mas conservadora y la unica opcion que la ficha efectivamente define en su catalogo fijo de tipos de documento.
