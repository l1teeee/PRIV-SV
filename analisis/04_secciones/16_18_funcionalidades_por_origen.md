# 16. Funcionalidades obligatorias por ley

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (prohibido codigo, SQL, APIs, esquemas de base de datos, nombres de tecnologias, stack o infraestructura).

Esta seccion consolida y cruza lo ya decidido en `01_legal/matriz_obligaciones.json` (105 obligaciones), `02_validacion/mapa_modulos.json`, `02_validacion/06_mapa_definitivo_de_modulos.md` (en especial su seccion 8, tabla completa de cobertura OBL-ID -> modulo propietario) y la seccion Q ("MVP") de las 26 fichas funcionales de `03_modulos/MOD-001_ficha.md` a `MOD-026_ficha.md`, complementada donde hizo falta con las secciones A, D, E y G de la misma ficha propietaria. No inventa funcionalidades que ninguna ficha define: cuando una obligacion no tiene una fila propia en la seccion Q de su modulo propietario que cite su OBL-ID de forma literal, la funcionalidad que se le atribuye es la fila de Q mas cercana de la misma familia de campos, o una funcionalidad ya descrita en las secciones D/E/G/I de esa misma ficha; los 27 casos en que esto ocurrio se listan en "Contradicciones y huecos detectados" al final del archivo, junto con las demas discrepancias resueltas.

Convencion de identificadores: todo OBL-ID citado es el identificador canonico de `01_legal/matriz_obligaciones.json` (formato OBL-AREA-NN, 105 obligaciones), nunca los IDs preliminares de `01_legal/03_hallazgos_regulatorios.md` (OBL-AMBITO-xx, OBL-CONSENT-xx y similares); la equivalencia entre unos y otros esta en la seccion 11 de ese documento. Toda obligacion se clasifica OBLIGATORIO, RECOMENDADO o CONDICIONAL, igual que `matriz_obligaciones.json`; esta seccion no reclasifica ninguna obligacion, solo cita la clasificacion ya asignada por la matriz. Los 12 roles citados en el resto del blueprint son los de `02_validacion/05_tipos_de_usuario.md`, seccion 5.3, con su nombre exacto; esta seccion en particular no necesita citarlos porque su unidad de analisis es la obligacion, no el usuario. El sistema orienta, explica, organiza, alerta, calcula, registra, documenta y genera evidencia; nunca decide cuestiones juridicas ni afirma cumplimiento legal: por eso ninguna fila de esta seccion se expresa como "porcentaje de cumplimiento", solo como funcionalidad, estado del programa, controles configurados, tareas pendientes o evidencia disponible.

Jerarquia usada para resolver cualquier discrepancia entre fuentes: fuente legal primaria y `matriz_obligaciones.json`, sobre `mapa_modulos.json` y `06_mapa_definitivo_de_modulos.md`, estos sobre `05_tipos_de_usuario.md` para lo relativo a roles, y estos sobre la ficha del modulo propietario de la obligacion, y esta sobre cualquier otra ficha que mencione el mismo tema de forma colaboradora. Las contradicciones detectadas al aplicar esta jerarquia y los huecos (piezas que ninguna ficha define de forma explicita) se listan al final de este archivo, en "Contradicciones y huecos detectados", con archivo, lo que dice cada fuente, cual se adopto y por que.

## 16.1 Aclaracion conceptual: que significa "obligatoria por ley" aplicada al software

La Ley para la Proteccion de Datos Personales (Decreto Legislativo 144) y sus normas complementarias (Politicas de Actuacion de la ACE, Lineamientos para el Delegado, Normativa del Procedimiento Administrativo Sancionador) obligan a la empresa, nunca al software. El software no es sujeto obligado de la LPDP: es una herramienta que la empresa usa para atender sus propias obligaciones. Por eso, en todo este documento, "funcionalidad obligatoria por ley" no significa que exista un articulo que ordene construir esa pantalla; significa que, sin esa funcionalidad, la empresa cliente no podria atender de forma razonable, o no podria demostrar despues ante la ACE o ante un titular, una obligacion que la matriz clasifica como OBLIGATORIO (exigible siempre) o CONDICIONAL (exigible solo cuando se cumple la condicion de activacion que la propia matriz describe, por ejemplo "solo si la empresa usa videovigilancia").

Esta distincion importa para leer correctamente la columna "Version" de las tablas siguientes: una funcionalidad puede figurar como V1 sin que eso signifique que la obligacion legal subyacente queda descubierta durante el MVP. Varias fichas documentan un patron explicito de "cobertura parcial": la obligacion ya se satisface desde el MVP por un mecanismo mas simple (un campo de texto libre, una tarea manual, un registro basico dentro de otro modulo), y lo que se difiere a V1 o V2 es la version mas completa, automatizada o especializada de esa misma funcionalidad. Donde esto ocurre, la columna "Version" de la tabla lo indica explicitamente (por ejemplo "MVP/V1").

```
Obligacion OBLIGATORIO o CONDICIONAL          Funcionalidad que la empresa necesita
   (matriz_obligaciones.json)         -->      para atenderla o demostrarla
        |                                              |
        v                                              v
  clasificacion + norma + articulo          modulo propietario (mapa definitivo,
  + condicion de activacion                 seccion 8) + fila de la seccion Q
        |                                              |
        +---------------------> version (MVP/V1/V2) <-+
                     segun MUST HAVE / SHOULD HAVE / COULD HAVE
                     de la seccion Q de la ficha propietaria
```

## 16.2 Metodologia y verificacion mecanica de cobertura (105/105)

Para construir las tablas de esta seccion y de la seccion 17 se siguio este procedimiento, verificable de forma mecanica sobre los archivos fuente:

1. Se tomaron las 105 obligaciones de `01_legal/matriz_obligaciones.json` con su `id`, `titulo`, `norma`, `articulo`, `clasificacion` y `condicion`.
2. Se cruzo cada `id` con la tabla completa de cobertura de `02_validacion/06_mapa_definitivo_de_modulos.md`, seccion 8 ("OBL-ID -> modulo propietario"), para obtener el modulo propietario de cada obligacion. Las 105 filas de esa tabla se parsearon y se verifico que cubren exactamente las 105 obligaciones de la matriz, sin duplicados ni huecos.
3. Se extrajo la seccion Q ("MVP") de las 26 fichas (`03_modulos/MOD-001_ficha.md` a `MOD-026_ficha.md`) y se busco, para cada obligacion, la fila cuya funcionalidad o justificacion cita su OBL-ID de forma literal (incluyendo listas abreviadas del tipo "OBL-ARCO-02, 03, 08" o rangos del tipo "OBL-DPO-01 a 08"). Esto resolvio 77 de las 105 obligaciones de forma automatica.
4. Las 28 obligaciones restantes (27 de clasificacion OBLIGATORIO/CONDICIONAL para la seccion 16, mas OBL-SANC-07 de clasificacion RECOMENDADO para la seccion 17) se resolvieron leyendo directamente la seccion Q completa (y, cuando fue necesario, las secciones D, E, G e I) de su ficha propietaria, sin inventar ninguna funcionalidad nueva: se atribuyeron a la fila de Q ya existente que cubre la misma familia de campos o el mismo mecanismo. El detalle de estos 27+1 casos y su razonamiento estan en "Contradicciones y huecos detectados".
5. Se clasifico la version (MVP, V1, V2) de cada funcionalidad segun la columna marcada con "X" en la seccion Q de su ficha (MUST HAVE = MVP, SHOULD HAVE = V1, COULD HAVE = V2, FUTURE = V2/posterior, segun la convencion ya usada de forma consistente en `02_validacion/propuesta_mapa_mvp.md` y en `02_validacion/propuesta_mapa_recorrido.md`); cuando una obligacion tiene cobertura parcial documentada (una funcionalidad MVP que ya la satisface y otra V1/V2 que la amplia), la columna Version muestra ambos valores separados por "/".

La verificacion mecanica final, ejecutable con Python 3 sobre `01_legal/matriz_obligaciones.json` sin depender de ninguna transcripcion manual, es la siguiente:

```
python3 - << 'EOF'
import json
matriz = json.load(open("01_legal/matriz_obligaciones.json"))
ids = set(o["id"] for o in matriz)
assert len(ids) == 105
sec16 = set(o["id"] for o in matriz if o["clasificacion"] in ("OBLIGATORIO", "CONDICIONAL"))
sec17 = set(o["id"] for o in matriz if o["clasificacion"] == "RECOMENDADO")
assert sec16 | sec17 == ids and sec16 & sec17 == set()
print("Seccion 16 (OBLIGATORIO+CONDICIONAL):", len(sec16))
print("Seccion 17 (RECOMENDADO):", len(sec17))
print("Total:", len(sec16) + len(sec17), "== 105:", len(sec16) + len(sec17) == 105)
EOF
```

**Resultado declarado de la ejecucion** (2026-09-24, sobre el archivo actual de `matriz_obligaciones.json`): Seccion 16 (OBLIGATORIO+CONDICIONAL) = 100 obligaciones; Seccion 17 (RECOMENDADO) = 5 obligaciones; Total = 105, igual a 105: verdadero. Las 100 obligaciones de la seccion 16 y las 5 de la seccion 17 tienen, cada una, al menos una funcionalidad asignada en las tablas siguientes (verificado con el mismo script extendido para comprobar que ninguna de las 105 quedo sin funcionalidad). No hay superposicion entre ambos conjuntos: ninguna obligacion aparece en las dos secciones.

Las 18 areas de la matriz (AMB, PRIN, ARCO, DPO, AVISO, CONS, SENS, TRAT, PROV, TRANSF, SEG, DOC, INC, CAP, AUD, SANC, PLAZO, RET) se presentan a continuacion en el mismo orden y con el mismo conteo que usa `06_mapa_definitivo_de_modulos.md` seccion 8. Dentro de cada area, la columna "Condicion de activacion" queda en blanco para las obligaciones OBLIGATORIO (no tienen condicion) y muestra el texto literal del campo `condicion` de la matriz para las CONDICIONAL.

## 16.3 Tablas por area (100 obligaciones OBLIGATORIO y CONDICIONAL)

### AMB - Ambito de aplicacion (4)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Cuestionario completo de 11 bloques y 47 preguntas, con dependencias | MOD-004 (Diagnostico de Cumplimiento) | OBL-AMB-01 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 2 inc. 1 | OBLIGATORIO | - | MVP |
| Deteccion de exclusiones del Art. 3 (seccion G.1) | MOD-004 (Diagnostico de Cumplimiento) | OBL-AMB-02 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 3 lit. a) | CONDICIONAL | Aplica solo si el cliente reporta historial crediticio bajo la ley especial de buros de credito, o es supervisado por la SSF | MVP |
| Deteccion de exclusiones del Art. 3 (seccion G.1) | MOD-004 (Diagnostico de Cumplimiento) | OBL-AMB-03 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 3 lit. b) | CONDICIONAL | Aplica solo cuando el tratamiento es exclusivamente domestico y sin fin de divulgacion o uso comercial; no aplica a una empresa en su operacion ordinaria | MVP |
| Deteccion de exclusiones del Art. 3 (seccion G.1) | MOD-004 (Diagnostico de Cumplimiento) | OBL-AMB-04 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 3 lit. c) y d) | CONDICIONAL | Aplica solo al tratamiento cuyo objeto especifico sea seguridad publica/defensa/persecucion del delito o registros publicos oficiales | MVP |

### PRIN - Principios rectores (4)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Registro de consentimiento general (formulario simple, sin refuerzo) | MOD-007 (Consentimiento) | OBL-PRIN-01 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 5 lit. c) | OBLIGATORIO | - | MVP |
| Seleccion obligatoria de una de las seis bases de licitud con justificacion | MOD-006 (RAT y Mapa de Datos) | OBL-PRIN-02 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 5 lit. g) | OBLIGATORIO | - | MVP |
| Workflow de estados (Borrador, En revision, Vigente, Requiere revision, Archivado) con aprobacion; Flujo de estados con aprobacion de activacion y doble control en riesgo alto | MOD-006 (RAT y Mapa de Datos); MOD-009 (Proveedores y Encargados) | OBL-PRIN-03 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 5 lit. i) | OBLIGATORIO | - | MVP |
| Sub-flujo de consentimiento parental para NNA | MOD-007 (Consentimiento) | OBL-PRIN-04 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 5 lit. j) | CONDICIONAL | Aplica cuando el cliente trata datos de ninas, ninos o adolescentes | MVP |

### ARCO - Derechos ARCO-POL (procedimiento) (15)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Verificacion de identidad para los 3 tipos de solicitante (titular, representante, heredero) | MOD-011 (ARCO-POL) | OBL-ARCO-01 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 6 | OBLIGATORIO | - | MVP |
| Informe de acceso sin datos de terceros | MOD-011 (ARCO-POL) | OBL-ARCO-02 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 8 | OBLIGATORIO | - | MVP |
| Bloqueo cautelar durante rectificacion | MOD-011 (ARCO-POL) | OBL-ARCO-03 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 9 | OBLIGATORIO | - | MVP |
| Formulario interno seguro con los 7 elementos del Art. 18, con causales tasadas por tipo de solicitud y plazo 20+20 dias habiles | MOD-011 (ARCO-POL) | OBL-ARCO-04 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 10 | CONDICIONAL | Procede solo si se cumple alguna de las 7 causales del Art. 10 y no concurre ninguna de las 6 causales de improcedencia | MVP |
| Formulario interno seguro con los 7 elementos del Art. 18, con causales tasadas por tipo de solicitud y plazo 20+20 dias habiles | MOD-011 (ARCO-POL) | OBL-ARCO-05 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 12 | CONDICIONAL | Procede salvo que el tratamiento se ampare en interes publico o interes legitimo prevalente del responsable/tercero | MVP |
| Formulario interno seguro con los 7 elementos del Art. 18, con causales tasadas por tipo de solicitud y plazo 20+20 dias habiles | MOD-011 (ARCO-POL) | OBL-ARCO-06 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 13 | CONDICIONAL | Procede solo ante alguno de los 4 supuestos tasados del Art. 13 | MVP |
| Portabilidad condicionada (verificacion de base + automatizacion) | MOD-011 (ARCO-POL) | OBL-ARCO-07 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 14 | CONDICIONAL | Procede solo si el tratamiento se basa en consentimiento y es automatizado | MVP |
| Formulario interno seguro con los 7 elementos del Art. 18; Prevencion unica con archivo automatico | MOD-011 (ARCO-POL) | OBL-ARCO-08 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 18 | OBLIGATORIO | - | MVP |
| Rama de incompetencia (5 dias habiles) | MOD-011 (ARCO-POL) | OBL-ARCO-09 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 19 | CONDICIONAL | Aplica cuando el responsable no es competente sobre los datos objeto de la solicitud | MVP |
| Plazo general 20+20 dias habiles con una sola prorroga | MOD-011 (ARCO-POL) | OBL-ARCO-10 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 20 | OBLIGATORIO | - | MVP |
| Notificacion automatica a Receptor tras rectificacion/eliminacion (integracion con MOD-011); Rama de notificacion a receptores (5 dias habiles), con fallback manual si MOD-010 aun no esta completo | MOD-009 (Proveedores y Encargados); MOD-011 (ARCO-POL) | OBL-ARCO-11 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 21 inc. 3 | CONDICIONAL | Aplica solo si los datos objeto de la solicitud fueron previamente comunicados o transferidos a terceros | MVP |
| Denegatoria motivada con las 8 causales tasadas y notificacion en 3 dias habiles | MOD-011 (ARCO-POL) | OBL-ARCO-12 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 22 | OBLIGATORIO | - | MVP |
| Gratuidad y tabla de costos de reproduccion publicados | MOD-011 (ARCO-POL) | OBL-ARCO-13 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 23 | OBLIGATORIO | - | MVP |
| Reclamo del titular ante la Direccion de Proteccion de Datos (registro basico del reclamo como texto libre desde el MVP; plantilla dedicada de informe de actuaciones en V1) | MOD-011 (ARCO-POL) | OBL-ARCO-14 | Lineamientos para el Delegado de Proteccion de Datos Personales (ACE), Art. 33 inc. 4 | CONDICIONAL | Aplica solo si el titular presenta el reclamo ante la Direccion de Proteccion de Datos y la ACE requiere informe | V1 |
| Carga directa de los 7 formularios oficiales ARCO-POL de la ACE | MOD-011 (ARCO-POL) | OBL-ARCO-15 | Lineamientos para el Delegado de Proteccion de Datos Personales (ACE), Art. 32 | OBLIGATORIO | - | MVP |

### DPO - Delegado de Proteccion de Datos (8)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Alta y edicion del nombramiento (datos basicos, perfil, modalidad); Pregunta inicial sobre la existencia o designacion del Delegado, con siembra del registro en MOD-002 | MOD-002 (Delegado / Responsable Interno de Datos); MOD-003 (Onboarding) | OBL-DPO-01 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 15 y 17 | OBLIGATORIO | - | MVP |
| Contador y tarea de notificacion interna (3 dias habiles) | MOD-002 (Delegado / Responsable Interno de Datos) | OBL-DPO-02 | Lineamientos para el Delegado de Proteccion de Datos Personales (ACE), Art. 8 | CONDICIONAL | Aplica mientras el cliente tenga obligacion o decida mantener voluntariamente un delegado | MVP |
| Contador, tarea y registro del tramite de comunicacion a la ACE (15 dias habiles); Registro basico de tramites ante la ACE (ACEFiling), incluida la recepcion automatica de eventos desde MOD-002 y MOD-010 | MOD-002 (Delegado / Responsable Interno de Datos); MOD-024 (Centro Regulatorio) | OBL-DPO-03 | Lineamientos para el Delegado de Proteccion de Datos Personales (ACE), Art. 10 | CONDICIONAL | Aplica mientras subsista la obligatoriedad del delegado o se mantenga uno de forma voluntaria | MVP |
| Contador y tarea de reverificacion cada 3 anos; Notificacion de constancias hacia MOD-002 para sus campos de capacitacion y reverificacion del Delegado (OBL-DPO-04, OBL-DPO-05) | MOD-002 (Delegado / Responsable Interno de Datos); MOD-017 (Capacitacion) | OBL-DPO-04 | Lineamientos para el Delegado de Proteccion de Datos Personales (ACE), Art. 18 | CONDICIONAL | Aplica mientras subsista la figura del delegado | MVP |
| Contador y tarea de capacitacion anual del propio Delegado; Notificacion de constancias hacia MOD-002 para sus campos de capacitacion y reverificacion del Delegado (OBL-DPO-04, OBL-DPO-05) | MOD-002 (Delegado / Responsable Interno de Datos); MOD-017 (Capacitacion) | OBL-DPO-05 | Lineamientos para el Delegado de Proteccion de Datos Personales (ACE), Art. 22 | CONDICIONAL | Aplica mientras subsista la figura del delegado | MVP |
| Clausula y contador de confidencialidad post-cese (5 anos) | MOD-002 (Delegado / Responsable Interno de Datos) | OBL-DPO-06 | Lineamientos para el Delegado de Proteccion de Datos Personales (ACE), Art. 36 | CONDICIONAL | Aplica al cesar el delegado en el cargo | MVP |
| Registro de informes periodicos semestrales con estadisticas ARCO-POL; Notificacion al Delegado para su informe periodico (OBL-DPO-07) | MOD-002 (Delegado / Responsable Interno de Datos); MOD-018 (Auditoria de Cumplimiento) | OBL-DPO-07 | Lineamientos para el Delegado de Proteccion de Datos Personales (ACE), Art. 30 | CONDICIONAL | Aplica mientras subsista la figura del delegado | V1 |
| Bitacora de peticiones internas atendidas por otras areas | MOD-002 (Delegado / Responsable Interno de Datos) | OBL-DPO-08 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 17 | OBLIGATORIO | - | V1 |

### AVISO - Aviso y politica de privacidad (5)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Gestor de Aviso de Privacidad con checklist de 9 literales (Art. 24) y 5 elementos (Art. 7) | MOD-008 (Documentos y Politicas) | OBL-AVISO-01 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 24 | OBLIGATORIO | - | MVP |
| Gestor de Aviso de Privacidad con checklist de 9 literales (Art. 24) y 5 elementos (Art. 7); Datos de contacto del encargado para el aviso de privacidad (integracion con MOD-008) | MOD-008 (Documentos y Politicas); MOD-009 (Proveedores y Encargados) | OBL-AVISO-02 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 24 lit. h) | CONDICIONAL | Aplica cuando el responsable subcontrata a un encargado del tratamiento | MVP |
| Gestor de Aviso de Privacidad con checklist de 9 literales (Art. 24) y 5 elementos (Art. 7) | MOD-008 (Documentos y Politicas) | OBL-AVISO-03 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 24 lit. i) | CONDICIONAL | Aplica cuando el cliente opera sitios web o apps que usan cookies | MVP |
| Gestor de Aviso de Privacidad con checklist de 9 literales (Art. 24) y 5 elementos (Art. 7) | MOD-008 (Documentos y Politicas) | OBL-AVISO-04 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 7 | OBLIGATORIO | - | MVP |
| Gestor de Politica de Proteccion de Datos (plantilla, versionado, aprobacion); Gestor de Politica de Privacidad | MOD-008 (Documentos y Politicas) | OBL-AVISO-05 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 24 inc. 1 | OBLIGATORIO | - | MVP |

### CONS - Consentimiento (6)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Registro de consentimiento general (formulario simple, sin refuerzo) | MOD-007 (Consentimiento) | OBL-CONS-01 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 26 y 27 | OBLIGATORIO | - | MVP |
| Revocacion con flujo de dos plazos (5 + 5 dias habiles) | MOD-007 (Consentimiento) | OBL-CONS-02 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 29 | OBLIGATORIO | - | MVP |
| Revocacion con flujo de dos plazos (5 + 5 dias habiles); Notificacion automatica a Encargado tras revocacion de consentimiento (integracion con MOD-007) | MOD-007 (Consentimiento); MOD-009 (Proveedores y Encargados) | OBL-CONS-03 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 30 | OBLIGATORIO | - | MVP |
| Registro de consentimiento reforzado (sensible/biometrico con firma); Revocacion con flujo de dos plazos (5 + 5 dias habiles) | MOD-007 (Consentimiento) | OBL-CONS-04 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 26 inc. 4 | OBLIGATORIO | - | MVP |
| Snapshot inmutable y version del aviso referenciada | MOD-007 (Consentimiento) | OBL-CONS-05 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 54 | OBLIGATORIO | - | MVP |
| Sub-flujo de consentimiento parental para NNA; Sub-flujo de titular NNA (consentimiento parental, aviso de tension normativa) | MOD-007 (Consentimiento); MOD-011 (ARCO-POL) | OBL-CONS-06 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 56 lit. c num. 3, en relacion con Art. 5 lit. j y Art. 42 | CONDICIONAL | Aplica cuando el cliente trata datos de ninas, ninos o adolescentes | MVP |

### SENS - Datos sensibles (8)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Catalogo cerrado de categorias de datos sensibles (union Art. 4 lit. g / Art. 59 lit. b) con marcado automatico | MOD-006 (RAT y Mapa de Datos) | OBL-SENS-01 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 4 lit. g) | OBLIGATORIO | - | MVP |
| Registro de consentimiento reforzado (sensible/biometrico con firma) | MOD-007 (Consentimiento) | OBL-SENS-02 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 37 inc. 1 | OBLIGATORIO | - | MVP |
| Catalogo de excepciones al consentimiento (Art. 28 y Arts. 37-38) | MOD-007 (Consentimiento) | OBL-SENS-03 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 37 inc. 2-3 y Art. 38 inc. 1 | CONDICIONAL | Aplica solo ante uno de los tres supuestos de excepcion tasados | V1 |
| Catalogo cerrado de categorias de datos sensibles (union Art. 4 lit. g / Art. 59 lit. b) con marcado automatico | MOD-006 (RAT y Mapa de Datos) | OBL-SENS-04 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 39 | CONDICIONAL | Aplica a clientes cuyo giro sea la prestacion de servicios de salud | MVP |
| Catalogo base de controles (organizativos, tecnicos, fisicos) con estado y evidencia adjunta | MOD-015 (Controles de Seguridad) | OBL-SENS-05 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 59 | OBLIGATORIO | - | MVP |
| Catalogo cerrado de categorias de datos sensibles (union Art. 4 lit. g / Art. 59 lit. b) con marcado automatico | MOD-006 (RAT y Mapa de Datos) | OBL-SENS-06 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 4 lit. g) | OBLIGATORIO | - | MVP |
| Registro de consentimiento reforzado (sensible/biometrico con firma) | MOD-007 (Consentimiento) | OBL-SENS-07 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 26 inc. 4 y Art. 37 | CONDICIONAL | Aplica solo si la empresa recolecta datos biometricos; la alternativa no biometrica es una recomendacion de diseno, no un mandato expreso | MVP |
| Catalogo cerrado de categorias de datos sensibles (union Art. 4 lit. g / Art. 59 lit. b) con marcado automatico | MOD-006 (RAT y Mapa de Datos) | OBL-SENS-08 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 4 lit. f) y lit. g), Art. 7, Art. 12 lit. b), Art. 16 lit. g) | CONDICIONAL | Aplica solo si la empresa usa videovigilancia; el regimen de dato sensible aplica solo si hay reconocimiento facial u otro identificador biometrico | MVP |

### TRAT - Tratamiento general (3)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Ficha de actividad de tratamiento (campos basicos: nombre, area, finalidad, base de licitud, categorias, sistema) con workflow de aprobacion ante cambios | MOD-006 (RAT y Mapa de Datos) | OBL-TRAT-01 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 32 | OBLIGATORIO | - | MVP |
| Catalogo de excepciones al consentimiento (Art. 28 y Arts. 37-38) | MOD-007 (Consentimiento) | OBL-TRAT-02 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 28 | CONDICIONAL | Aplica solo ante alguno de los 8 supuestos tasados del Art. 28 | V1 |
| Seleccion obligatoria de una de las seis bases de licitud con justificacion (incluida fuente de acceso publico) | MOD-006 (RAT y Mapa de Datos) | OBL-TRAT-03 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 4 lit. l) | CONDICIONAL | Aplica cuando el responsable pretenda tratar datos sin consentimiento invocando que provienen de una fuente de acceso publico | MVP |

### PROV - Proveedores / Encargados (5)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Alta y ficha de Encargado / Tercero-Receptor / Subencargado (bloques D.1 y D.2); Vinculacion de Contrato/DPA (referencia a MOD-008) | MOD-009 (Proveedores y Encargados) | OBL-PROV-01 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 33 inc. 2 | OBLIGATORIO | - | MVP |
| Alta y ficha de Encargado / Tercero-Receptor / Subencargado (bloques D.1 y D.2) | MOD-009 (Proveedores y Encargados) | OBL-PROV-02 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 34 | OBLIGATORIO | - | MVP |
| Alta y ficha de Encargado / Tercero-Receptor / Subencargado (bloques D.1 y D.2) | MOD-009 (Proveedores y Encargados) | OBL-PROV-03 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 36 | OBLIGATORIO | - | MVP |
| Datos de contacto del encargado para el aviso de privacidad (integracion con MOD-008) | MOD-009 (Proveedores y Encargados) | OBL-PROV-04 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 56 lit. a num. 2 | OBLIGATORIO | - | MVP |
| Modelado de cadenas de subcontratacion (Subencargados de segundo nivel o mas) | MOD-009 (Proveedores y Encargados) | OBL-PROV-05 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 33 inc. 2 | CONDICIONAL | Aplica solo si existe una cadena de subcontratacion (el encargado del cliente subcontrata a otro proveedor) | V1 |

### TRANSF - Transferencias de datos (6)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Registro manual basico de una transferencia (tratamiento, receptor, pais, base, finalidad) | MOD-010 (Transferencias Internacionales) | OBL-TRANSF-01 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 40 | OBLIGATORIO | - | V1 |
| Registro manual basico de una transferencia (tratamiento, receptor, pais, base, finalidad) | MOD-010 (Transferencias Internacionales) | OBL-TRANSF-02 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 41 | CONDICIONAL | Aplica a toda transferencia de datos a otro responsable (no aplica a la relacion con un encargado, que se rige por el Art. 34/36) | V1 |
| Cuestionario de evaluacion de pais receptor | MOD-010 (Transferencias Internacionales) | OBL-TRANSF-03 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 44 inc. 1 | CONDICIONAL | Aplica a toda transferencia internacional de datos personales | V1 |
| Vinculacion de consentimiento especifico (MOD-007) | MOD-010 (Transferencias Internacionales) | OBL-TRANSF-04 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 44 inc. final | OBLIGATORIO | - | V1 |
| Registro basico de tramites ante la ACE (ACEFiling), incluida la recepcion automatica de eventos desde MOD-002 y MOD-010 | MOD-024 (Centro Regulatorio) | OBL-TRANSF-05 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 45 | OBLIGATORIO | - | MVP |
| Reportes y paquete de evidencia exportable con hash (expediente probatorio de cada transferencia internacional) | MOD-010 (Transferencias Internacionales) | OBL-TRANSF-06 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 54 inc. 2 | OBLIGATORIO | - | V1 |

### SEG - Seguridad (medidas tecnicas/organizativas) (6)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Catalogo base de controles (organizativos, tecnicos, fisicos) con estado y evidencia adjunta | MOD-015 (Controles de Seguridad) | OBL-SEG-01 | Ley para la Proteccion de Datos Personales (D.L. 144); Politicas de Actuacion ACE N. 001-0309025-DPDP, Art. 35 LPDP | OBLIGATORIO | - | MVP |
| Catalogo base de controles (organizativos, tecnicos, fisicos) con estado y evidencia adjunta | MOD-015 (Controles de Seguridad) | OBL-SEG-02 | Politicas de Actuacion ACE N. 001-0309025-DPDP, Art. 4 (Medidas Organizativas, lit. a-f) | OBLIGATORIO | - | MVP |
| Catalogo base de controles (organizativos, tecnicos, fisicos) con estado y evidencia adjunta | MOD-015 (Controles de Seguridad) | OBL-SEG-03 | Politicas de Actuacion ACE N. 001-0309025-DPDP, Art. 4 (Medidas Tecnicas) | OBLIGATORIO | - | MVP |
| Catalogo base de controles (organizativos, tecnicos, fisicos) con estado y evidencia adjunta, incluido el bloque de medidas de seguridad en transferencias de datos | MOD-015 (Controles de Seguridad) | OBL-SEG-04 | Politicas de Actuacion ACE N. 001-0309025-DPDP, Art. 4 (bloque Medidas de Seguridad en Transferencias de Datos) y Art. 6 lit. d) | OBLIGATORIO | - | MVP |
| Catalogo base de controles (organizativos, tecnicos, fisicos) con estado y evidencia adjunta | MOD-015 (Controles de Seguridad) | OBL-SEG-05 | Politicas de Actuacion ACE, Art. 4, Medidas Fisicas lit. e) | OBLIGATORIO | - | MVP |
| Catalogo base de controles (organizativos, tecnicos, fisicos) con estado y evidencia adjunta | MOD-015 (Controles de Seguridad) | OBL-SEG-06 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 56 lit. b num. 5 y 7 | OBLIGATORIO | - | MVP |

### DOC - Documentacion (4)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Gestor documental por tipo de documento (catalogo fijo incluye Procedimiento ARCO-POL), con plantilla, versionado y aprobacion | MOD-008 (Documentos y Politicas) | OBL-DOC-01 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 33 inc. 1 | OBLIGATORIO | - | MVP |
| Ficha de actividad de tratamiento (campos basicos: nombre, area, finalidad, base de licitud, categorias, sistema); Mapa de Datos como visualizacion interactiva completa (diagrama navegable) | MOD-006 (RAT y Mapa de Datos) | OBL-DOC-02 | Politicas de Actuacion ACE N. 001-0309025-DPDP, Art. 4 (Medidas Organizativas, lit. d) | OBLIGATORIO | - | MVP/V1 |
| Apertura automatica de la EIPD desde disparadores del Diagnostico y del RAT; Flujo de aprobacion formal con registro de aprobador y fecha | MOD-014 (Riesgos y EIPD) | OBL-DOC-03 | Politicas de Actuacion ACE N. 001-0309025-DPDP, Art. 4 (Medidas Organizativas, lit. e) | OBLIGATORIO | - | MVP |
| Consulta publica del Aviso de Privacidad vigente | MOD-012 (Portal del Titular) | OBL-DOC-04 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 61 inc. 2 | OBLIGATORIO | - | V1 |

### INC - Incidentes / vulneraciones (5)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Dos cronometros de 72 horas en paralelo (notificacion e inicio de revision), con criterio de horas corridas por defecto | MOD-013 (Incidentes de Seguridad) | OBL-INC-01 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 25 | OBLIGATORIO | - | MVP |
| Dos cronometros de 72 horas en paralelo (notificacion e inicio de revision), con criterio de horas corridas por defecto | MOD-013 (Incidentes de Seguridad) | OBL-INC-02 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 25 inc. 2 | OBLIGATORIO | - | MVP |
| Plantillas diferenciadas de notificacion a ACE/FGR y a titulares | MOD-013 (Incidentes de Seguridad) | OBL-INC-03 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 25 inc. 3-4 | OBLIGATORIO | - | MVP |
| Documentacion obligatoria del expediente con bloqueo si hay riesgo y faltan campos | MOD-013 (Incidentes de Seguridad) | OBL-INC-04 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 25 inc. final | OBLIGATORIO | - | MVP |
| Flujo condicional completo del Decreto 143 (reporte adicional de infraestructura critica) | MOD-013 (Incidentes de Seguridad) | OBL-INC-05 | Ley de Ciberseguridad y Seguridad de la Informacion (D.L. 143), Art. 6 lit. f-g, en relacion con Art. 2 y Art. 8 lit. f-g | CONDICIONAL | Aplica solo si la empresa privada ha sido calificada por la ACE como operador de infraestructura critica (Art. 8 lit. f Decreto 143); no aplica a empresas privadas ordinarias | V1 |

### CAP - Capacitacion (2)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Registro general de capacitacion del personal (quien, cuando, tema, modalidad, version del material, constancia, proxima renovacion) | MOD-017 (Capacitacion) | OBL-CAP-01 | Politicas de Actuacion ACE N. 001-0309025-DPDP, Art. 4 (Medidas Organizativas, lit. c) | OBLIGATORIO | - | MVP |
| Plan anual de capacitacion e induccion en su version minima (agregacion automatica de los programas del ano, elaborado por el Delegado, con aprobacion separada y exportacion como documento) | MOD-017 (Capacitacion) | OBL-CAP-02 | Lineamientos para el Delegado de Proteccion de Datos Personales (ACE), Art. 22 | CONDICIONAL | Aplica mientras subsista la figura del delegado en la empresa | MVP |

### AUD - Auditoria (1)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Registro basico de ComplianceAudit (planificar, ejecutar, cerrar) con checklist precargado desde MOD-006 y MOD-015, hallazgos con severidad y evidencia, y cierre con aprobacion separada | MOD-018 (Auditoria de Cumplimiento) | OBL-AUD-01 | Politicas de Actuacion ACE N. 001-0309025-DPDP, Art. 8 lit. b) | OBLIGATORIO | - | V1 |

### SANC - Sanciones y procedimiento (8)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Catalogo de infracciones y multas (Art. 56 y 57), informativo | MOD-024 (Centro Regulatorio) | OBL-SANC-01 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 56 | OBLIGATORIO | - | MVP |
| Registro manual de un expediente de Procedimiento Sancionador (datos basicos, contestacion, resultado) con contadores de plazo | MOD-024 (Centro Regulatorio) | OBL-SANC-02 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 57 | CONDICIONAL | Aplica cuando la ACE determina la comision de una infraccion tras el procedimiento sancionador | V1 |
| Registro manual de un expediente de Procedimiento Sancionador (datos basicos, contestacion, resultado) con contadores de plazo | MOD-024 (Centro Regulatorio) | OBL-SANC-03 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 58 | CONDICIONAL | Aplica cuando la ACE impone una sancion y ordena medidas correctivas adicionales | V1 |
| Registro manual de un expediente de Procedimiento Sancionador (datos basicos, contestacion, resultado) con contadores de plazo | MOD-024 (Centro Regulatorio) | OBL-SANC-04 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 53 | CONDICIONAL | Aplica cuando se inicia un procedimiento sancionador contra el responsable | V1 |
| Registro manual de un expediente de Procedimiento Sancionador (datos basicos, contestacion, resultado) con contadores de plazo | MOD-024 (Centro Regulatorio) | OBL-SANC-05 | Normativa para el Procedimiento Administrativo Sancionador (ACE), Art. 21 | CONDICIONAL | Aplica cuando la ACE emplaza al responsable dentro de un procedimiento sancionador | V1 |
| Registro manual de un expediente de Procedimiento Sancionador (datos basicos, contestacion, resultado) con contadores de plazo | MOD-024 (Centro Regulatorio) | OBL-SANC-06 | Normativa para el Procedimiento Administrativo Sancionador (ACE), Art. 44 | CONDICIONAL | Aplica cuando la ACE impone una multa firme | V1 |
| Observatorio de publicidad de resoluciones sancionatorias de la ACE (OBL-SANC-08) | MOD-024 (Centro Regulatorio) | OBL-SANC-08 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 55 | CONDICIONAL | Aplica cuando existe una resolucion sancionatoria firme contra el responsable | V2 |
| Registro manual de un expediente de Procedimiento Sancionador (datos basicos, contestacion, resultado) con contadores de plazo | MOD-024 (Centro Regulatorio) | OBL-SANC-09 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 9 inc. 3 y Art. 31 | CONDICIONAL | Aplica cuando el responsable incumple los plazos de rectificacion o de tramite de revocacion | V1 |

### PLAZO - Plazos y calendario (5)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Regla de computo del Art. 82 LPA (inicio al dia siguiente, meses/anios de fecha a fecha, ultimo dia inhabil se traslada al siguiente habil) | MOD-023 (Calendario y Motor de Plazos) | OBL-PLAZO-01 | Ley de Procedimientos Administrativos (D.L. 856), supletoria por Art. 62 LPDP, Art. 82 LPA | OBLIGATORIO | - | MVP |
| Calendario de asuetos nacionales del Codigo de Trabajo y de los decretos D.L. 339/2016 y D.L. 208/2012 | MOD-023 (Calendario y Motor de Plazos) | OBL-PLAZO-02 | Codigo de Trabajo y decretos legislativos de asueto, Art. 190 Codigo de Trabajo, y D.L. 339/2016, D.L. 208/2012 | OBLIGATORIO | - | MVP |
| Cuestionario completo de 11 bloques y 47 preguntas, con dependencias; Motor de priorizacion Critica / Importante / Recomendada; Exportacion del plan con hash de integridad ("Plan de adecuacion"); Catalogo base de controles (organizativos, tecnicos, fisicos) con estado y evidencia adjunta | MOD-004 (Diagnostico de Cumplimiento); MOD-005 (Plan de Cumplimiento); MOD-015 (Controles de Seguridad) | OBL-PLAZO-03 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 60 inc. 2 | OBLIGATORIO | - | MVP |
| Gestor de Aviso de Privacidad con checklist de 9 literales (Art. 24) y 5 elementos (Art. 7); Formulario interno seguro con los 7 elementos del Art. 18 | MOD-008 (Documentos y Politicas); MOD-011 (ARCO-POL) | OBL-PLAZO-04 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 61 inc. 2 | OBLIGATORIO | - | MVP |
| Bandera regimen_reforma_659 con interruptor manual, registro de fecha y notificacion a cada organizacion | MOD-024 (Centro Regulatorio) | OBL-PLAZO-05 | Decreto Legislativo N. 659 (reforma a la LPDP), Segun fuentes secundarias: deroga Arts. 15 y 17; reforma Arts. 16, 47 y 51 | CONDICIONAL | No exigible hasta su publicacion en el Diario Oficial y entrada en vigencia (8 dias despues de publicada); mientras tanto sigue vigente el texto actual (delegado obligatorio, Arts. 15 y 17) | MVP |

### RET - Retencion / conservacion documental (5)

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Clasificacion | Condicion de activacion | Version |
|---|---|---|---|---|---|---|
| Motor de retencion de datos del titular: reglas por categoria/tratamiento/sistema/finalidad, citando uno o mas OBL-RET | MOD-016 (Retencion y Eliminacion) | OBL-RET-01 | Codigo de Comercio, Art. 451 y 454 | CONDICIONAL | Aplica a la conservacion de documentacion mercantil/contable, incluida la que contenga datos personales de clientes/proveedores | V1 |
| Motor de retencion de datos del titular: reglas por categoria/tratamiento/sistema/finalidad, citando uno o mas OBL-RET | MOD-016 (Retencion y Eliminacion) | OBL-RET-02 | Codigo Tributario, Art. 147 | CONDICIONAL | Aplica a documentacion tributaria y contable que contenga datos personales (empleados, clientes, proveedores) | V1 |
| Motor de retencion de datos del titular: reglas por categoria/tratamiento/sistema/finalidad, citando uno o mas OBL-RET | MOD-016 (Retencion y Eliminacion) | OBL-RET-03 | Ley Contra el Lavado de Dinero y de Activos (LCLDA), Art. 10 lit. b) y Art. 12 | CONDICIONAL | Aplica solo si el cliente es sujeto obligado bajo el Art. 2 de la LCLDA (determinacion caso por caso) | V1 |
| Versionado con historial inmutable y regla simple de no-borrado antes de 10 anios (cobertura MVP); ampliado por el motor de retencion documental con estado, alerta y flujo de aprobacion de eliminacion (MOD-016, V1) | MOD-008 (Documentos y Politicas) | OBL-RET-04 | Lineamientos para el Delegado de Proteccion de Datos Personales (ACE), Art. 31 | OBLIGATORIO | - | MVP |
| Versionado con historial inmutable y hash de integridad por version publicada, con regla de no-borrado antes de 10 anios | MOD-008 (Documentos y Politicas) | OBL-RET-06 | Ley de Firma Electronica, Art. 13-A | OBLIGATORIO | - | MVP |

## 16.4 Lectura de la columna Version: que ya cubre el MVP

De las 100 obligaciones OBLIGATORIO y CONDICIONAL de esta seccion, 76 tienen su funcionalidad de soporte marcada MVP (sola o como primer termino de una cobertura MVP/V1), lo que significa que el nucleo MUST HAVE de los 20 modulos MUST HAVE (`mapa_modulos.json`) ya deja a la empresa en condiciones de atender o demostrar esas obligaciones desde el primer dia de uso del sistema. Las 24 restantes dependen de una funcionalidad marcada V1 o V2, casi siempre porque su modulo propietario completo es SHOULD HAVE o COULD HAVE en el mapa (MOD-010 Transferencias Internacionales, MOD-012 Portal del Titular, MOD-014 Riesgos y EIPD, MOD-016 Retencion y Eliminacion, MOD-018 Auditoria de Cumplimiento) y no porque la obligacion quede sin ninguna forma de atenderse: en la mayoria de esos casos la propia ficha documenta un mecanismo de "cobertura parcial" (una tarea manual, un campo de texto libre o un registro basico en otro modulo MUST HAVE) que ya funciona antes de que el modulo completo exista, tal como describe `06_mapa_definitivo_de_modulos.md`. Ninguna de las 100 obligaciones queda sin una funcionalidad, presente o programada, que la sostenga.

---

# 17. Funcionalidades recomendadas

Fecha de elaboracion: 2026-09-24. Misma fase, mismas fuentes y misma convencion de identificadores que la seccion 16.

Esta seccion tiene dos partes. La primera (17.1) cubre las 5 obligaciones que `matriz_obligaciones.json` clasifica como RECOMENDADO: no son exigibles de forma coactiva (no hay un articulo que ordene su cumplimiento bajo sancion), pero la propia matriz las registra porque documentan un criterio prudente ante una laguna normativa, o una facultad de la ACE que la empresa puede aprovechar. La segunda (17.2) cubre buenas practicas de diseno de producto que ninguna obligacion de la matriz exige, pero que refuerzan directamente el principio de responsabilidad demostrada (OBL-PRIN-03, Art. 5 lit. i LPDP, propietario MOD-019 Centro de Evidencias): separacion de funciones, trazabilidad de decisiones y verificacion independiente. La diferencia con la seccion 18 es exactamente esta: una funcionalidad opcional de la seccion 18 mejora la comodidad, la automatizacion o el alcance comercial del producto; una funcionalidad de esta seccion 17.2 mejora la capacidad de la empresa de demostrar despues lo que hizo.

## 17.1 Funcionalidades que sostienen las 5 obligaciones RECOMENDADO de la matriz

| Funcionalidad | Modulo | OBL-ID | Norma y articulo | Version | Por que es RECOMENDADO y no OBLIGATORIO/CONDICIONAL |
|---|---|---|---|---|---|
| Integracion con un futuro mecanismo de certificacion de la ACE (a la espera de que la ACE lo habilite) | MOD-024 (Centro Regulatorio); colabora MOD-018 (Auditoria de Cumplimiento) | OBL-AUD-02 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 50 lit. j, k, l | FUTURE | La ACE tiene la facultad de crear certificaciones o sellos de proteccion de datos, pero no existe hoy ningun mecanismo habilitado (verificado 2026-09-23 y 2026-09-24, sin resultado); el sistema solo puede recordar que la facultad existe, no construir una integracion con algo que aun no existe |
| Campo de instrucciones documentadas de tratamiento con plantilla dedicada (ademas del campo de texto simple ya disponible desde el MVP) | MOD-009 (Proveedores y Encargados) | OBL-PROV-06 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 34 lit. a), en relacion con Art. 5 lit. i) | V2 | No existe articulo que exija expresamente documentar instrucciones al encargado con una plantilla propia; el campo de texto simple del MVP ya cubre la necesidad minima, la plantilla dedicada solo mejora la calidad y consistencia del documento |
| Tarea de verificacion de devolucion/eliminacion de datos por el encargado al finalizar la relacion contractual | MOD-009 (Proveedores y Encargados) | OBL-PROV-07 | Ley para la Proteccion de Datos Personales (D.L. 144), Art. 34 lit. a), en relacion con Art. 5 lit. h) | V1 | Sin articulo expreso que la exija como tramite formal; se incluye pronto por su alto valor probatorio si el contrato ya la pacta y su bajo costo de implementacion |
| Motor de retencion documental de cumplimiento con estado explicito, alerta y flujo de aprobacion de eliminacion, aplicado al expediente ARCO-POL y de incidentes | MOD-016 (Retencion y Eliminacion) | OBL-RET-05 | Normativa para el Procedimiento Administrativo Sancionador (ACE), por analogia con el Art. 47 (prescripcion de 5 anos); Art. 5 lit. i LPDP (responsabilidad demostrada) | V1 | No existe en la LPDP, la Normativa sancionadora, los Lineamientos ni las Politicas ACE una norma expresa que fije el plazo de conservacion del expediente ARCO-POL o de un incidente; se recomienda como criterio prudente el mismo plazo de prescripcion de infracciones (5 anos), sin perjuicio de plazos mayores por otras normas; la propia matriz advierte que este criterio requiere validacion de asesoria juridica |
| Calculo automatico de fecha_limite_prescripcion (5 anos desde la firmeza o el ultimo hecho) con alerta de prescripcion proxima a 90 dias | MOD-024 (Centro Regulatorio) | OBL-SANC-07 | Ley de Ciberseguridad y Seguridad de la Informacion (D.L. 143), por remision del Art. 53 LPDP; Normativa PAS (ACE), Art. 47 | V1 | Es informativo para la gestion de riesgo y la politica de retencion de evidencia (sirve de referencia minima de 5 anos), no una obligacion cuyo incumplimiento la ACE pueda sancionar por si sola |

## 17.2 Buenas practicas que refuerzan la responsabilidad demostrada

Ninguna de las funcionalidades siguientes tiene un OBL-ID propio en `matriz_obligaciones.json`: todas aparecen en al menos una ficha marcadas explicitamente como "buena practica" o "[opinion de producto]", casi siempre ligadas a la separacion de funciones de `02_validacion/05_tipos_de_usuario.md` seccion 5.4, o al principio general de responsabilidad demostrada (OBL-PRIN-03).

| Funcionalidad | Modulo | Fundamento citado en la ficha | Justificacion |
|---|---|---|---|
| Separacion de funciones configurable con umbral por tamano de empresa (bloqueo de que Aprobador y Auditor sean la misma persona, activable por encima de un umbral de empleados) | MOD-001 (Organizacion y Personas) | Buena practica de control de acceso; `05_tipos_de_usuario.md` seccion 5.4; sin articulo especifico que la exija de forma expresa | Evita que quien aprueba una decision de riesgo sea tambien quien la audita despues; el umbral y el nombre de los roles son opinion de producto, pero el principio de separacion refuerza directamente la responsabilidad demostrada |
| Advertencia visible de "autorrevision" cuando una misma persona acumula Administrador y Auditor en una pyme pequena | MOD-001 (Organizacion y Personas) | Buena practica de control de acceso, `05_tipos_de_usuario.md` seccion 5.4 | En pyme, donde pocas personas cubren varios roles, el sistema no puede bloquear la acumulacion sin volverse inoperable, pero si puede dejar visible el riesgo y quien lo acepto |
| Auditor externo con acceso temporal por invitacion, siempre de solo lectura | MOD-001 (Organizacion y Personas); consumido por MOD-018 (Auditoria de Cumplimiento) | Buena practica de control de acceso; util para la auditoria anual de OBL-AUD-01, pero no imprescindible por si sola | Permite que una firma auditora externa verifique la evidencia sin depender de que el cliente le reenvie archivos sueltos por correo, y sin darle permisos de edicion |
| Exportacion firmada con verificacion de integridad del listado de usuarios y roles activos en un momento dado | MOD-001 (Organizacion y Personas) | Buena practica de control de acceso, necesaria para el paquete de evidencia de auditoria | Deja constancia verificable de quien tenia acceso a que, en la fecha exacta de una auditoria o de un incidente, sin depender de la memoria de la empresa |
| Justificacion obligatoria para descartar una tarea vinculada a una obligacion OBLIGATORIO, con validacion de un segundo usuario | MOD-005 (Plan de Cumplimiento) | Buena practica; "apoya la responsabilidad demostrada que exige la ley de forma general" (ficha de MOD-005) | Impide que una obligacion legal quede silenciosamente sin atender solo porque una persona marco la tarea como "Descartada"; exige dejar una razon documentada y un segundo control |
| Justificacion obligatoria para repriorizar manualmente una tarea calculada por el motor de priorizacion | MOD-005 (Plan de Cumplimiento) | Buena practica; trazabilidad de la decision | Si alguien cambia la urgencia calculada por el sistema, queda registrado por que, en vez de perderse el criterio original |
| Doble control obligatorio (Aprobador distinto del autor) para una EIPD de riesgo Alto o Critico | MOD-014 (Riesgos y EIPD) | Buena practica de separacion de funciones [opinion de producto], sin mandato legal expreso | Una autoevaluacion de riesgo alto revisada por la misma persona que la elaboro tiene menor valor probatorio ante una auditoria o un reclamo |
| Aprobacion de una segunda persona (rol Aprobador) para registrar una excepcion de "No aplica" en un control de seguridad del catalogo | MOD-015 (Controles de Seguridad) | Buena practica de separacion de funciones, `05_tipos_de_usuario.md` seccion 5.4 | Evita que una sola persona decida, sin revision, que un control de seguridad exigido por las Politicas ACE simplemente no se va a implementar |
| Registro de accesos de lectura a evidencia marcada como sensible (datos personales sensibles o informacion tecnica de seguridad, por ejemplo un reporte de pentest) | MOD-015 (Controles de Seguridad); MOD-019 (Centro de Evidencias) | Buena practica de seguridad y privacidad, sin OBL-ID propio | Deja constancia de quien consulto informacion sensible y cuando, no solo de quien la modifico, reforzando el control de acceso que las Politicas ACE esperan como medida tecnica |
| Vinculacion automatica de cada registro de evidencia con la entidad de origen que la genero (en vez de un campo de texto libre) | MOD-019 (Centro de Evidencias) | Buena practica; regla de "direccion unica" de `06_mapa_definitivo_de_modulos.md` seccion 4 | Evita duplicar el mismo dato en dos modulos y evita que la evidencia se desactualice si el registro de origen cambia |
| Snapshot mensual inmutable de todos los indicadores del dashboard, no editable una vez generado | MOD-020 (Dashboard y Reportes) | Buena practica de trazabilidad de tendencias | Permite comparar el estado del programa entre fechas y demuestra que el estado mostrado en un momento dado no se altero retroactivamente |

---

