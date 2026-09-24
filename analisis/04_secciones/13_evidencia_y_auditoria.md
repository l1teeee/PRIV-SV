# 13. Sistema de evidencia y auditoria

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (prohibido codigo, SQL, APIs, esquemas de base de datos, nombres de tecnologias, stack o infraestructura).

Esta seccion consolida y cruza lo ya decidido en las 26 fichas funcionales de `03_modulos/MOD-001_ficha.md` a `MOD-026_ficha.md` (en especial la seccion J "Evidencia" y la seccion O "Historial" de cada una, y las fichas completas de MOD-019 Centro de Evidencias, MOD-018 Auditoria de Cumplimiento, MOD-016 Retencion y Eliminacion y MOD-013 Incidentes de Seguridad), en `01_legal/matriz_obligaciones.json` (105 obligaciones canonicas) y en `02_validacion/06_mapa_definitivo_de_modulos.md` (seccion 7, entidades conceptuales; seccion 8, tabla de cobertura OBL-ID -> modulo propietario). No inventa funcionalidades que ninguna ficha defina; donde el prompt del cliente exige un contenido que ninguna ficha cubre, se marca explicitamente "propuesta de esta seccion, no presente en las fichas". Toda obligacion legal se cita con su ID canonico de `matriz_obligaciones.json` (formato OBL-AREA-NN), norma y articulo; los IDs preliminares de `01_legal/03_hallazgos_regulatorios.md` (OBL-AMBITO-xx, OBL-CONSENT-xx y similares) no se usan aqui, conforme a la equivalencia de la seccion 11 de ese documento.

Jerarquia usada para resolver cualquier discrepancia entre fuentes: fuente legal primaria y `matriz_obligaciones.json` sobre `mapa_modulos.json` y `06_mapa_definitivo_de_modulos.md`, estos sobre `05_tipos_de_usuario.md` para lo relativo a roles, y estos sobre la ficha del modulo propietario de la obligacion o entidad en cuestion, y esta sobre cualquier otra ficha que mencione el mismo tema de forma colaboradora. Las contradicciones detectadas al aplicar esta jerarquia y los huecos (piezas que ninguna ficha define) se listan al final, en "Contradicciones y huecos detectados".

El software nunca decide cuestiones juridicas ni afirma cumplimiento legal: "evidencia disponible" nunca significa "cumplimiento confirmado", y ningun indicador de esta seccion usa la expresion "porcentaje de cumplimiento legal"; se usa siempre estado del programa, controles configurados, tareas pendientes o evidencia disponible (anti-feature 5 de `22_anti_features.md`).

---

## 13.1 Principios

### 13.1.1 Responsabilidad demostrada (accountability)

- OBL-PRIN-03, Art. 5 lit. i) LPDP, OBLIGATORIO, propietario MOD-019 Centro de Evidencias: la empresa debe poder demostrar, en cualquier momento, que cumple sus obligaciones, no solo cumplirlas. Es la obligacion mas transversal de toda la matriz: cualquier evidencia que otro modulo produzca para su propia obligacion especifica es al mismo tiempo evidencia parcial de OBL-PRIN-03 (MOD-019 seccion A).
- Todo el sistema de evidencia y auditoria de esta seccion existe para responder, en cualquier momento, la pregunta "que evidencia tenemos de esta obligacion" (MOD-019 seccion A), no para calcular una nota de cumplimiento.

### 13.1.2 Carga de la prueba

- Art. 54 LPDP: la carga de la prueba del consentimiento y de la comunicacion del aviso de privacidad recae en el responsable (OBL-CONS-05, propietario MOD-007 Consentimiento, colaboradora MOD-019). El inciso 2 del mismo articulo extiende el mismo criterio a las transferencias internacionales (OBL-TRANSF-06, propietario MOD-010 Transferencias Internacionales, colaboradora MOD-019): quien alega haber cumplido debe poder probarlo, no basta con afirmarlo.
- Este principio es la razon funcional de que el sistema conserve snapshots congelados (version exacta del texto de un aviso, version exacta de un contrato) en vez de solo el estado actual: si el dato cambia despues, la version que el titular efectivamente vio en su momento debe seguir siendo reconstruible.

### 13.1.3 Tres entidades separadas que nunca se mezclan

Decision de alcance 2.7.4 de `02_validacion/02_validacion_de_la_idea.md`, adoptada sin cambios por `02_validacion/06_mapa_definitivo_de_modulos.md` seccion 7 y por MOD-019 seccion A:

```
+----------------+      +----------------+      +----------------+
|   DOCUMENTO    |      |   EVIDENCIA    |      |   AUDITLOG     |
|   (MOD-008)    |      |   (MOD-019)    |      | (transversal)  |
|                |      |                |      |                |
| Contenido      |      | Prueba de que  |      | Registro       |
| versionado:    |      | algo ocurrio:  |      | tecnico e      |
| avisos,        |      | archivo con    |      | inmutable:     |
| politicas,     |      | hash o         |      | quien hizo     |
| contratos,     |      | referencia a   |      | que y cuando,  |
| informes       |      | un registro de |      | en cualquier   |
|                |      | otro modulo    |      | parte del      |
|                |      |                |      | sistema        |
+-------+--------+      +--------+-------+      +--------+-------+
        |                        |                        |
        |   se referencia,       |  ambas se consultan,    |
        |   nunca se copia       |  nunca se administran   |
        |                        |  entre si                |
        v                        v                        v
   +----------------------------------------------------------+
   |         EVIDENCEPACKAGE (paquete de evidencia)            |
   |   vista de exportacion sobre las tres entidades           |
   |   anteriores, sin almacenamiento propio; manifiesto +     |
   |   verificacion de integridad (ver 13.5)                   |
   +----------------------------------------------------------+
```

- **Documento**: contenido versionado (avisos, politicas, contratos, informes). Propiedad de MOD-008 Documentos y Politicas; el resto del sistema lo referencia, nunca lo copia (MOD-019 seccion A).
- **Evidencia (Evidence)**: propiedad de MOD-019. Un artefacto (archivo con hash) o una referencia a un registro especifico de otro modulo (una aprobacion, un cambio de estado, un envio) que demuestra que algo ocurrio.
- **AuditLog**: registro tecnico e inmutable de acciones del sistema, embebido en todos los modulos desde el primer dia de uso (anti-feature 19 de `02_validacion/22_anti_features.md`). No tiene modulo propietario unico: cada modulo escribe sus propios eventos; MOD-018 y MOD-019 lo consultan como fuente de contexto tecnico, nunca lo administran (`06_mapa_definitivo_de_modulos.md`, seccion 7).
- **EvidencePackage**: no es una cuarta base de datos, es una vista de exportacion sobre las tres entidades anteriores, con manifiesto y verificacion de integridad (anti-feature 25; ver 13.5).

### 13.1.4 El paquete como vista, no como copia

Un EvidencePackage nunca duplica fisicamente el contenido que referencia: cuando incluye un Documento, referencia la version congelada exacta que ya existe en MOD-008; cuando incluye Evidencia, referencia el archivo o el registro de origen con su propio hash, sin copiarlo fisicamente entre paquetes (MOD-019 seccion D.2 y K). Esto evita mantener dos copias del mismo dato con el riesgo de que diverjan.

---

## 13.2 Matriz obligacion -> evidencia (105 obligaciones)

Metodologia: tabla generada a partir de `01_legal/matriz_obligaciones.json` (campos `id`, `titulo`, `clasificacion`, `evidencia_esperada`, leidos con un script auxiliar en Python solo para extraer los datos; el entregable de esta seccion es integramente Markdown) cruzado con el modulo propietario segun `02_validacion/mapa_modulos.json` (campo `obligaciones_propietarias`) y verificado contra la tabla de cobertura de `06_mapa_definitivo_de_modulos.md` seccion 8 ("Tabla completa de cobertura: OBL-ID -> modulo propietario"): ambas fuentes coinciden en las 105 obligaciones, sin discrepancias, por lo que no hay contradiccion que resolver en esta parte.

Las columnas "Forma" y "Retencion" provienen de la seccion J ("Evidencia") de la ficha del modulo propietario, en particular del catalogo consolidado D.0 de MOD-019 (que ya agrupa por modulo de origen el tipo de evidencia, la forma y la retencion de referencia). Donde la propia obligacion fija un plazo especifico distinto del generico de su modulo (las seis obligaciones de retencion, OBL-RET-01 a 06), se usa ese plazo especifico tal como lo define su propia ficha (MOD-016), no el generico del modulo.

Convencion de "Forma": **Registro** (dato estructurado dentro de una entidad), **Archivo** (adjunto con hash), **Aprobacion** (accion humana registrada con identidad y fecha), **Log** (evento de AuditLog). La mayoria de las obligaciones usa una combinacion de las tres primeras; ver la ficha del modulo propietario, seccion D, para el detalle campo por campo.

Convencion de "Retencion": cuando el texto dice "Segun [modulo]", significa que el plazo de esa evidencia especifica esta gobernado por el motor de retencion de MOD-016 y no tiene todavia un numero de anos fijo propio distinto; cuando aparece un numero de anos con un OBL-ID entre parentesis, ese es el fundamento (legal o de criterio recomendado) de ese plazo especifico. Las obligaciones marcadas RECOMENDADO en la columna "Clasif." y cuyo plazo depende de OBL-RET-05 u OBL-SANC-07 requieren validacion de asesoria juridica antes de tratarse como una regla cerrada (ver 13.6).

### AMB - Ambito de aplicacion (4)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-AMB-01 | Ambito de aplicacion universal de la LPDP | OBLIGATORIO | Analisis de aplicabilidad de la ley al cliente; Ficha de organizacion con giro y tipos de tratamiento | MOD-004 Diagnostico de Cumplimiento | Registro | Igual que el expediente de cumplimiento de la organizacion (MOD-016) |
| OBL-AMB-02 | Exclusion de historial crediticio (con excepcion para sector financiero) | CONDICIONAL | Clasificacion del giro del cliente | MOD-004 Diagnostico de Cumplimiento | Registro | Igual que el expediente de cumplimiento de la organizacion (MOD-016) |
| OBL-AMB-03 | Exclusion de ambito domestico | CONDICIONAL | Analisis de aplicabilidad | MOD-004 Diagnostico de Cumplimiento | Registro | Igual que el expediente de cumplimiento de la organizacion (MOD-016) |
| OBL-AMB-04 | Exclusiones por seguridad publica y registros publicos | CONDICIONAL | Analisis de aplicabilidad | MOD-004 Diagnostico de Cumplimiento | Registro | Igual que el expediente de cumplimiento de la organizacion (MOD-016) |

### PRIN - Principios generales (4)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-PRIN-01 | Principio de consentimiento y finalidad | OBLIGATORIO | Registro de consentimientos con finalidad y periodo declarados | MOD-007 Consentimiento | Registro / archivo / aprobacion | Segun regla de MOD-016 |
| OBL-PRIN-02 | Principio de licitud: seis bases de tratamiento | OBLIGATORIO | RAT con base de licitud y justificacion por cada actividad de tratamiento | MOD-006 RAT y Mapa de Datos | Registro / aprobacion | 5 anios como minimo por defecto |
| OBL-PRIN-03 | Principio de responsabilidad demostrada | OBLIGATORIO | Repositorio de evidencia de cumplimiento (RAT, EIPD, contratos, capacitaciones, auditorias) | MOD-019 Centro de Evidencias | Registro / aprobacion / log | Igual que la evidencia consolidada (por obligacion de origen) |
| OBL-PRIN-04 | Principio de ejercicio progresivo de facultades (NNA) | CONDICIONAL | Procedimiento diferenciado para titulares NNA | MOD-007 Consentimiento | Registro / archivo / aprobacion | Segun regla de MOD-016 |

### ARCO - Derechos ARCO-POL (15)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-ARCO-01 | Legitimacion para ejercer derechos ARCO-POL | OBLIGATORIO | Formulario de verificacion de identidad y representacion | MOD-011 ARCO-POL | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05, RECOMENDADO) |
| OBL-ARCO-02 | Contenido de la respuesta al derecho de acceso | OBLIGATORIO | Plantilla de respuesta de acceso con historial de consultas/comparticiones | MOD-011 ARCO-POL | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05, RECOMENDADO) |
| OBL-ARCO-03 | Rectificacion: plazo, gratuidad y bloqueo cautelar | OBLIGATORIO | Registro de solicitud, bloqueo cautelar y resolucion dentro de plazo | MOD-011 ARCO-POL | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05, RECOMENDADO) |
| OBL-ARCO-04 | Cancelacion: causales de procedencia e improcedencia | CONDICIONAL | Analisis motivado de procedencia/improcedencia de cada solicitud | MOD-011 ARCO-POL | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05, RECOMENDADO) |
| OBL-ARCO-05 | Oposicion al tratamiento, incluido marketing directo | CONDICIONAL | Registro de solicitudes de oposicion y su resolucion; Mecanismo de exclusion (opt-out) de campanas de marketing | MOD-011 ARCO-POL | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05, RECOMENDADO) |
| OBL-ARCO-06 | Limitacion del tratamiento | CONDICIONAL | Registro de datos marcados en estado de limitacion | MOD-011 ARCO-POL | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05, RECOMENDADO) |
| OBL-ARCO-07 | Portabilidad de datos | CONDICIONAL | Registro de exportacion de datos en formato portable | MOD-011 ARCO-POL | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05, RECOMENDADO) |
| OBL-ARCO-08 | Requisitos de la solicitud ARCO-POL y prevencion unica | OBLIGATORIO | Checklist de requisitos de la solicitud; Registro de prevenciones enviadas y plazo de subsanacion | MOD-011 ARCO-POL | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05, RECOMENDADO) |
| OBL-ARCO-09 | Devolucion de solicitud por incompetencia | CONDICIONAL | Registro de devolucion motivada por incompetencia | MOD-011 ARCO-POL | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05, RECOMENDADO) |
| OBL-ARCO-10 | Plazo general de respuesta ARCO-POL y prorroga | OBLIGATORIO | Calendario de vencimiento por solicitud; Alertas de proximidad de vencimiento | MOD-011 ARCO-POL | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05, RECOMENDADO) |
| OBL-ARCO-11 | Notificacion a receptores de datos tras rectificacion, actualizacion o eliminacion | CONDICIONAL | Registro de notificaciones a receptores/terceros | MOD-011 ARCO-POL | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05, RECOMENDADO) |
| OBL-ARCO-12 | Denegatoria motivada de solicitudes ARCO-POL | OBLIGATORIO | Resolucion motivada de denegatoria con soporte probatorio | MOD-011 ARCO-POL | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05, RECOMENDADO) |
| OBL-ARCO-13 | Gratuidad del ejercicio de derechos ARCO-POL | OBLIGATORIO | Tabla de costos de reproduccion/envio publicada | MOD-011 ARCO-POL | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05, RECOMENDADO) |
| OBL-ARCO-14 | Atencion al reclamo del titular ante la Direccion de Proteccion de Datos de la ACE | CONDICIONAL | Registro del reclamo recibido de la ACE; Informe de actuaciones remitido a la ACE | MOD-011 ARCO-POL | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05, RECOMENDADO) |
| OBL-ARCO-15 | Aceptacion de los formularios oficiales ARCO-POL de la ACE | OBLIGATORIO | Formularios oficiales ACE disponibles para el titular; Registro de solicitudes recibidas en formulario oficial | MOD-011 ARCO-POL | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05, RECOMENDADO) |

### DPO - Delegado / Responsable interno (8)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-DPO-01 | Obligatoriedad de nombrar delegado en el sector privado | OBLIGATORIO | Acta de nombramiento del delegado; Credencial ACE del delegado | MOD-002 Delegado / Responsable Interno de Datos | Archivo / registro / aprobacion | Historico indefinido (min. 5 anios tras el cese, OBL-DPO-06) |
| OBL-DPO-02 | Notificacion interna del nombramiento del delegado | CONDICIONAL | Comunicacion formal de notificacion al delegado | MOD-002 Delegado / Responsable Interno de Datos | Archivo / registro / aprobacion | Historico indefinido (min. 5 anios tras el cese, OBL-DPO-06) |
| OBL-DPO-03 | Comunicacion del nombramiento del delegado a la ACE | CONDICIONAL | Constancia de registro del delegado ante la ACE; Credencial emitida por la ACE | MOD-002 Delegado / Responsable Interno de Datos | Archivo / registro / aprobacion | Historico indefinido (min. 5 anios tras el cese, OBL-DPO-06) |
| OBL-DPO-04 | Reverificacion periodica del perfil del delegado | CONDICIONAL | Atestados de capacitacion o certificacion vigentes del delegado | MOD-002 Delegado / Responsable Interno de Datos | Archivo / registro / aprobacion | Historico indefinido (min. 5 anios tras el cese, OBL-DPO-06) |
| OBL-DPO-05 | Capacitacion anual del propio delegado | CONDICIONAL | Constancia de capacitacion anual del delegado | MOD-002 Delegado / Responsable Interno de Datos | Archivo / registro / aprobacion | Historico indefinido (min. 5 anios tras el cese, OBL-DPO-06) |
| OBL-DPO-06 | Confidencialidad del delegado tras el cese | CONDICIONAL | Clausula de confidencialidad post-contractual en el contrato del delegado | MOD-002 Delegado / Responsable Interno de Datos | Archivo / registro / aprobacion | Historico indefinido (min. 5 anios tras el cese, OBL-DPO-06) |
| OBL-DPO-07 | Informe periodico del delegado al responsable | CONDICIONAL | Informes semestrales o bianuales del delegado con estadisticas ARCO-POL | MOD-002 Delegado / Responsable Interno de Datos | Archivo / registro / aprobacion | Historico indefinido (min. 5 anios tras el cese, OBL-DPO-06) |
| OBL-DPO-08 | Deber de asistencia de dependencias, empleados y proveedores al delegado | OBLIGATORIO | Registro de peticiones internas del delegado y su atencion | MOD-002 Delegado / Responsable Interno de Datos | Archivo / registro / aprobacion | Historico indefinido (min. 5 anios tras el cese, OBL-DPO-06) |

### AVISO - Aviso de privacidad (5)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-AVISO-01 | Contenido minimo del aviso de privacidad | OBLIGATORIO | Aviso de privacidad publicado; Registro de comunicacion del aviso al titular | MOD-008 Documentos y Politicas | Registro / archivo / aprobacion | Minimo 10 anios por version (OBL-RET-04) |
| OBL-AVISO-02 | Datos de contacto del encargado en el aviso de privacidad | CONDICIONAL | Aviso de privacidad con seccion de encargados | MOD-008 Documentos y Politicas | Registro / archivo / aprobacion | Minimo 10 anios por version (OBL-RET-04) |
| OBL-AVISO-03 | Informar el uso de cookies | CONDICIONAL | Aviso de privacidad con seccion de cookies | MOD-008 Documentos y Politicas | Registro / archivo / aprobacion | Minimo 10 anios por version (OBL-RET-04) |
| OBL-AVISO-04 | Derecho de informacion en la recoleccion | OBLIGATORIO | Aviso de privacidad con listado de encargados/proveedores de almacenamiento | MOD-008 Documentos y Politicas | Registro / archivo / aprobacion | Minimo 10 anios por version (OBL-RET-04) |
| OBL-AVISO-05 | Elaboracion de la politica de privacidad | OBLIGATORIO | Documento de politica de privacidad aprobado internamente | MOD-008 Documentos y Politicas | Registro / archivo / aprobacion | Minimo 10 anios por version (OBL-RET-04) |

### CONS - Consentimiento (6)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-CONS-01 | Requisitos del consentimiento | OBLIGATORIO | Registro de consentimiento con medio, fecha y finalidad | MOD-007 Consentimiento | Registro / archivo / aprobacion | Segun regla de MOD-016 |
| OBL-CONS-02 | Revocacion del consentimiento en cualquier momento | OBLIGATORIO | Mecanismo de revocacion disponible al titular; Registro de revocaciones | MOD-007 Consentimiento | Registro / archivo / aprobacion | Segun regla de MOD-016 |
| OBL-CONS-03 | Plazo para procesar la revocacion del consentimiento | OBLIGATORIO | Registro de fecha de recepcion y ejecucion de la revocacion; Constancia de notificacion al encargado | MOD-007 Consentimiento | Registro / archivo / aprobacion | Segun regla de MOD-016 |
| OBL-CONS-04 | Consentimiento por escrito para datos sensibles | OBLIGATORIO | Formulario de consentimiento firmado para datos sensibles | MOD-007 Consentimiento | Registro / archivo / aprobacion | Segun regla de MOD-016 |
| OBL-CONS-05 | Carga de la prueba del consentimiento y del aviso de privacidad | OBLIGATORIO | Registro probatorio de consentimiento (fecha, medio, texto aceptado); Constancia de entrega del aviso de privacidad | MOD-007 Consentimiento | Registro / archivo / aprobacion | Segun regla de MOD-016 |
| OBL-CONS-06 | Consentimiento parental para datos de ninez y adolescencia | CONDICIONAL | Registro de consentimiento parental para titulares NNA | MOD-007 Consentimiento | Registro / archivo / aprobacion | Segun regla de MOD-016 |

### SENS - Datos sensibles (8)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-SENS-01 | Identificacion de datos personales sensibles | OBLIGATORIO | Clasificacion de datos por categoria (ordinarios/sensibles) en el RAT | MOD-006 RAT y Mapa de Datos | Registro / aprobacion | 5 anios como minimo por defecto |
| OBL-SENS-02 | Advertencia del derecho a no proporcionar datos sensibles | OBLIGATORIO | Texto de advertencia en formularios de recoleccion de datos sensibles | MOD-007 Consentimiento | Registro / archivo / aprobacion | Segun regla de MOD-016 |
| OBL-SENS-03 | Excepciones al consentimiento para datos sensibles | CONDICIONAL | Justificacion documentada de la excepcion invocada | MOD-007 Consentimiento | Registro / archivo / aprobacion | Segun regla de MOD-016 |
| OBL-SENS-04 | Tratamiento de datos de salud | CONDICIONAL | Politica de manejo de expediente clinico alineada a la ley de pacientes | MOD-006 RAT y Mapa de Datos | Registro / aprobacion | 5 anios como minimo por defecto |
| OBL-SENS-05 | Prohibiciones sobre datos sensibles y comercializacion indebida | OBLIGATORIO | Politica interna de prohibiciones y sanciones internas por incumplimiento | MOD-015 Controles de Seguridad | Archivo / aprobacion | Indefinida hasta que MOD-016 fije un plazo; algunas con vigencia propia |
| OBL-SENS-06 | Informacion biometrica como dato personal sensible | OBLIGATORIO | Inventario de sistemas biometricos; Clasificacion del dato como sensible en el RAT | MOD-006 RAT y Mapa de Datos | Registro / aprobacion | 5 anios como minimo por defecto |
| OBL-SENS-07 | Consentimiento escrito y alternativa no biometrica para datos biometricos | CONDICIONAL | Formulario de consentimiento biometrico firmado; Registro de alternativa no biometrica ofrecida | MOD-007 Consentimiento | Registro / archivo / aprobacion | Segun regla de MOD-016 |
| OBL-SENS-08 | Videovigilancia y reconocimiento facial | CONDICIONAL | Aviso de videovigilancia visible; RAT con base de licitud declarada; EIPD si hay reconocimiento facial | MOD-006 RAT y Mapa de Datos | Registro / aprobacion | 5 anios como minimo por defecto |

### TRAT - Tratamiento y RAT (3)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-TRAT-01 | Prohibicion de desviacion de finalidad | OBLIGATORIO | RAT con finalidad declarada por cada tratamiento; Control de cambios de finalidad | MOD-006 RAT y Mapa de Datos | Registro / aprobacion | 5 anios como minimo por defecto |
| OBL-TRAT-02 | Excepciones al consentimiento previo | CONDICIONAL | Justificacion documentada de la excepcion invocada en el RAT | MOD-007 Consentimiento | Registro / archivo / aprobacion | Segun regla de MOD-016 |
| OBL-TRAT-03 | Definicion estricta de fuentes de acceso publico | CONDICIONAL | Analisis documentado de si la fuente califica como acceso publico | MOD-006 RAT y Mapa de Datos | Registro / aprobacion | 5 anios como minimo por defecto |

### PROV - Proveedores y encargados (7)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-PROV-01 | Sometimiento de proveedores subcontratados a la LPDP | OBLIGATORIO | Inventario de proveedores con acceso a datos; Clausulas de sometimiento a la LPDP en contratos | MOD-009 Proveedores y Encargados | Registro / archivo / aprobacion | Segun MOD-016 |
| OBL-PROV-02 | Obligaciones directas del encargado del tratamiento | OBLIGATORIO | Clausulas contractuales que trasladen estas obligaciones al encargado | MOD-009 Proveedores y Encargados | Registro / archivo / aprobacion | Segun MOD-016 |
| OBL-PROV-03 | Medidas de seguridad tambien obligatorias para el encargado | OBLIGATORIO | Certificaciones o autoevaluaciones de seguridad del proveedor/encargado | MOD-009 Proveedores y Encargados | Registro / archivo / aprobacion | Segun MOD-016 |
| OBL-PROV-04 | No publicar datos de contacto del encargado (infraccion leve) | OBLIGATORIO | Aviso de privacidad con datos de contacto del encargado publicados | MOD-009 Proveedores y Encargados | Registro / archivo / aprobacion | Segun MOD-016 |
| OBL-PROV-05 | Subcontratacion en cadena por el encargado (subencargados) | CONDICIONAL | Mapa de cadena de proveedores con subencargados identificados; Autorizacion o registro de la subcontratacion | MOD-009 Proveedores y Encargados | Registro / archivo / aprobacion | Segun MOD-016 |
| OBL-PROV-06 | Instrucciones documentadas del responsable al encargado | RECOMENDADO | Documento de instrucciones firmado o anexo contractual | MOD-009 Proveedores y Encargados | Registro / archivo / aprobacion | Segun MOD-016 |
| OBL-PROV-07 | Devolucion o eliminacion de datos por el encargado al finalizar la relacion | RECOMENDADO | Clausula contractual de devolucion o eliminacion; Constancia de eliminacion o devolucion al cierre del contrato | MOD-009 Proveedores y Encargados | Registro / archivo / aprobacion | Segun MOD-016 |

### TRANSF - Transferencias (6)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-TRANSF-01 | Requisitos de la transferencia nacional de datos | OBLIGATORIO | Registro de transferencias con consentimiento e identificacion del cesionario | MOD-010 Transferencias Internacionales | Registro / archivo | 5 anios minimo tras finalizar [opinion de producto, sin norma expresa] |
| OBL-TRANSF-02 | Contrato con el responsable receptor de la transferencia | CONDICIONAL | Contrato de transferencia firmado con clausulas equivalentes | MOD-010 Transferencias Internacionales | Registro / archivo | 5 anios minimo tras finalizar [opinion de producto, sin norma expresa] |
| OBL-TRANSF-03 | Nivel de proteccion exigido para transferencias internacionales | CONDICIONAL | Evaluacion documentada del nivel de proteccion del pais receptor | MOD-010 Transferencias Internacionales | Registro / archivo | 5 anios minimo tras finalizar [opinion de producto, sin norma expresa] |
| OBL-TRANSF-04 | Consentimiento previo para transferencias internacionales | OBLIGATORIO | Registro de consentimiento especifico para transferencia internacional | MOD-010 Transferencias Internacionales | Registro / archivo | 5 anios minimo tras finalizar [opinion de producto, sin norma expresa] |
| OBL-TRANSF-05 | Puesta en conocimiento de la ACE del flujo transfronterizo | OBLIGATORIO | Constancia de intento de notificacion a la ACE (mientras no exista canal habilitado) | MOD-010 Transferencias Internacionales | Registro / archivo | 5 anios minimo tras finalizar [opinion de producto, sin norma expresa] |
| OBL-TRANSF-06 | Carga de la prueba en transferencias internacionales | OBLIGATORIO | Expediente probatorio de cumplimiento por cada transferencia internacional | MOD-010 Transferencias Internacionales | Registro / archivo | 5 anios minimo tras finalizar [opinion de producto, sin norma expresa] |

### SEG - Seguridad (6)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-SEG-01 | Caracter imperativo de las politicas de actuacion de la ACE | OBLIGATORIO | Checklist de cumplimiento de las Politicas ACE | MOD-015 Controles de Seguridad | Archivo / aprobacion | Indefinida hasta que MOD-016 fije un plazo; algunas con vigencia propia |
| OBL-SEG-02 | Medidas organizativas minimas de las Politicas ACE | OBLIGATORIO | Documentos de cada una de las seis medidas organizativas | MOD-015 Controles de Seguridad | Archivo / aprobacion | Indefinida hasta que MOD-016 fije un plazo; algunas con vigencia propia |
| OBL-SEG-03 | Medidas tecnicas minimas de las Politicas ACE | OBLIGATORIO | Configuracion de 2FA; Evidencia de cifrado; Reportes de pentesting/analisis de vulnerabilidades; Bitacoras de backups | MOD-015 Controles de Seguridad | Archivo / aprobacion | Indefinida hasta que MOD-016 fije un plazo; algunas con vigencia propia |
| OBL-SEG-04 | Medidas de seguridad especificas para transferencias de datos | OBLIGATORIO | Configuracion SSL/TLS; Contratos de confidencialidad y transferencia | MOD-015 Controles de Seguridad | Archivo / aprobacion | Indefinida hasta que MOD-016 fije un plazo; algunas con vigencia propia |
| OBL-SEG-05 | Eliminacion segura de documentos y dispositivos | OBLIGATORIO | Politica de eliminacion segura; Constancia o certificado de destruccion/borrado; Contrato con proveedor de destruccion certificada, si aplica | MOD-015 Controles de Seguridad | Archivo / aprobacion | Indefinida hasta que MOD-016 fije un plazo; algunas con vigencia propia |
| OBL-SEG-06 | Infraccion grave por no implementar medidas o controles de la ACE | OBLIGATORIO | Checklist de medidas de seguridad con evidencia adjunta, vinculado al riesgo sancionador | MOD-015 Controles de Seguridad | Archivo / aprobacion | Indefinida hasta que MOD-016 fije un plazo; algunas con vigencia propia |

### DOC - Documentacion (4)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-DOC-01 | Establecer y documentar procedimientos ARCO-POL | OBLIGATORIO | Manual o procedimiento documentado de atencion ARCO-POL | MOD-008 Documentos y Politicas | Registro / archivo / aprobacion | Minimo 10 anios por version (OBL-RET-04) |
| OBL-DOC-02 | Registro de Actividades de Tratamiento (RAT) | OBLIGATORIO | RAT actualizado por actividad de tratamiento | MOD-006 RAT y Mapa de Datos | Registro / aprobacion | 5 anios como minimo por defecto |
| OBL-DOC-03 | Evaluaciones de Impacto en la Privacidad (EIPD) | OBLIGATORIO | EIPD documentada para tratamientos de alto riesgo | MOD-014 Riesgos y EIPD | Registro / aprobacion | Tratamiento activo mas 5 anios [opinion de producto] |
| OBL-DOC-04 | Elaboracion y publicacion de formularios/mecanismos ARCO-POL propios | OBLIGATORIO | Canal(es) publicados para presentar solicitudes ARCO-POL (formulario, correo, portal) | MOD-012 Portal del Titular | Registro | Alineado al expediente ARCO-POL relacionado (MOD-011) |

### INC - Incidentes (5)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-INC-01 | Notificacion de vulneraciones de seguridad en 72 horas | OBLIGATORIO | Bitacora de deteccion del incidente; Constancia de notificacion a ACE, FGR y titulares dentro de plazo | MOD-013 Incidentes de Seguridad | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05), con cadena de custodia |
| OBL-INC-02 | Revision exhaustiva del incidente dentro de las 72 horas | OBLIGATORIO | Registro de inicio de la investigacion interna del incidente | MOD-013 Incidentes de Seguridad | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05), con cadena de custodia |
| OBL-INC-03 | Contenido minimo de la notificacion de vulneracion | OBLIGATORIO | Plantillas diferenciadas de notificacion (ACE/FGR vs. titulares) | MOD-013 Incidentes de Seguridad | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05), con cadena de custodia |
| OBL-INC-04 | Documentacion obligatoria de toda vulneracion con riesgo | OBLIGATORIO | Expediente documentado de cada vulneracion con riesgo | MOD-013 Incidentes de Seguridad | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05), con cadena de custodia |
| OBL-INC-05 | Reporte de incidentes de ciberseguridad a la ACE (operadores de infraestructura critica) | CONDICIONAL | Resolucion de calificacion de infraestructura critica (si aplica); Bitacora de reporte de incidentes de ciberseguridad | MOD-013 Incidentes de Seguridad | Registro / archivo / aprobacion | 5 anios desde el cierre (OBL-RET-05), con cadena de custodia |

### CAP - Capacitacion (2)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-CAP-01 | Capacitacion del personal como medida organizativa obligatoria | OBLIGATORIO | Plan de capacitacion del personal; Constancias de asistencia | MOD-017 Capacitacion | Registro / archivo | Segun MOD-016 |
| OBL-CAP-02 | Plan anual de capacitacion del personal e induccion | CONDICIONAL | Plan anual de capacitacion elaborado por el delegado; Programa de induccion para personal nuevo | MOD-017 Capacitacion | Registro / archivo | Segun MOD-016 |

### AUD - Auditoria (2)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-AUD-01 | Auditorias anuales de cumplimiento de las Politicas ACE | OBLIGATORIO | Informe de auditoria anual de cumplimiento | MOD-018 Auditoria de Cumplimiento | Registro / archivo / aprobacion | Indefinida con archivado manual hasta que MOD-016 fije plazo especifico |
| OBL-AUD-02 | Facultad de la ACE de crear certificaciones o sellos de proteccion de datos | RECOMENDADO | - | MOD-024 Centro Regulatorio | Registro / archivo | 5 anios minimo (OBL-SANC-07) o segun expediente sancionador |

### SANC - Sanciones y procedimiento (9)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-SANC-01 | Catalogo de infracciones leves, graves y muy graves | OBLIGATORIO | Matriz de riesgo de infracciones por modulo | MOD-024 Centro Regulatorio | Registro / archivo | 5 anios minimo (OBL-SANC-07) o segun expediente sancionador |
| OBL-SANC-02 | Multas por clasificacion de infraccion | CONDICIONAL | Calculo de exposicion economica por tipo de infraccion (uso interno de riesgo) | MOD-024 Centro Regulatorio | Registro / archivo | 5 anios minimo (OBL-SANC-07) o segun expediente sancionador |
| OBL-SANC-03 | Medidas adicionales tras la sancion | CONDICIONAL | Plan de accion correctiva tras resolucion sancionatoria | MOD-024 Centro Regulatorio | Registro / archivo | 5 anios minimo (OBL-SANC-07) o segun expediente sancionador |
| OBL-SANC-04 | Remision del procedimiento sancionador y prescripcion a la Ley de Ciberseguridad | CONDICIONAL | Seguimiento del expediente sancionador y sus plazos | MOD-024 Centro Regulatorio | Registro / archivo | 5 anios minimo (OBL-SANC-07) o segun expediente sancionador |
| OBL-SANC-05 | Contestacion del emplazamiento en el procedimiento sancionador | CONDICIONAL | Escrito de contestacion y prueba presentada dentro de plazo | MOD-024 Centro Regulatorio | Registro / archivo | 5 anios minimo (OBL-SANC-07) o segun expediente sancionador |
| OBL-SANC-06 | Pago de la multa impuesta | CONDICIONAL | Comprobante de pago de la multa | MOD-024 Centro Regulatorio | Registro / archivo | 5 anios minimo (OBL-SANC-07) o segun expediente sancionador |
| OBL-SANC-07 | Prescripcion de infracciones y sanciones | RECOMENDADO | Politica de retencion de evidencia de cumplimiento con horizonte minimo de 5 anos | MOD-024 Centro Regulatorio | Registro / archivo | 5 anios minimo (OBL-SANC-07) o segun expediente sancionador |
| OBL-SANC-08 | Publicidad de las resoluciones sancionatorias | CONDICIONAL | Monitoreo del sitio web de la ACE por resoluciones publicadas | MOD-024 Centro Regulatorio | Registro / archivo | 5 anios minimo (OBL-SANC-07) o segun expediente sancionador |
| OBL-SANC-09 | Derecho de denuncia del titular ante la ACE | CONDICIONAL | Seguimiento de plazos internos para evitar habilitar la via de denuncia | MOD-024 Centro Regulatorio | Registro / archivo | 5 anios minimo (OBL-SANC-07) o segun expediente sancionador |

### PLAZO - Plazos (5)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-PLAZO-01 | Regla de computo de plazos (dias y horas habiles) | OBLIGATORIO | Motor de calculo de plazos con calendario de dias habiles | MOD-023 Calendario y Motor de Plazos | Registro | Segun MOD-016 |
| OBL-PLAZO-02 | Calendario de dias inhabiles (asuetos nacionales) | OBLIGATORIO | Calendario anual de dias inhabiles configurado en el sistema | MOD-023 Calendario y Motor de Plazos | Registro | Segun MOD-016 |
| OBL-PLAZO-03 | Plazo transitorio vencido: adecuacion de sujetos obligados tras las Politicas ACE | OBLIGATORIO | Plan de adecuacion y evidencia de su ejecucion | MOD-005 Plan de Cumplimiento | Registro / archivo / aprobacion | Vida de la cuenta mas 5 anios [opinion de producto] |
| OBL-PLAZO-04 | Plazo transitorio vencido: mecanismos de ejercicio de derechos ARCO-POL | OBLIGATORIO | Canal(es) de recepcion de solicitudes ARCO-POL operativo desde esa fecha | MOD-012 Portal del Titular | Registro | Alineado al expediente ARCO-POL relacionado (MOD-011) |
| OBL-PLAZO-05 | Seguimiento de la reforma 659 a la LPDP (pendiente de publicacion) | CONDICIONAL | Monitoreo periodico del Diario Oficial y del portal de la Asamblea | MOD-024 Centro Regulatorio | Registro / archivo | 5 anios minimo (OBL-SANC-07) o segun expediente sancionador |

### RET - Retencion (6)

| OBL-ID | Titulo | Clasif. | Evidencia esperada | Modulo generador | Forma | Retencion |
|---|---|---|---|---|---|---|
| OBL-RET-01 | Conservacion de registros mercantiles | CONDICIONAL | Politica de retencion documental alineada a 10 anos para registros mercantiles | MOD-016 Retencion y Eliminacion | Registro / aprobacion / archivo | Minimo 10 anios (Codigo de Comercio, plazo que fija la propia obligacion; hasta 5 anios adicionales tras liquidacion) |
| OBL-RET-02 | Conservacion de documentacion tributaria | CONDICIONAL | Politica de retencion documental alineada a 10 anos para documentacion tributaria | MOD-016 Retencion y Eliminacion | Registro / aprobacion / archivo | Minimo 10 anios (Codigo Tributario, plazo que fija la propia obligacion) |
| OBL-RET-03 | Conservacion de documentacion bajo la Ley Contra el Lavado de Dinero | CONDICIONAL | Politica de retencion sectorial LCLDA | MOD-016 Retencion y Eliminacion | Registro / aprobacion / archivo | Documentacion de operaciones 5 anios; registros de transacciones minimo 15 anios (LCLDA, plazo que fija la propia obligacion) |
| OBL-RET-04 | Conservacion de la documentacion del aviso de privacidad | OBLIGATORIO | Archivo historico de versiones del aviso de privacidad con evidencia de publicacion | MOD-016 Retencion y Eliminacion | Registro / aprobacion / archivo | Minimo 10 anios por version del aviso publicado (plazo que fija la propia obligacion, OBL-RET-04) |
| OBL-RET-05 | Criterio de retencion del expediente ARCO-POL e incidentes como prueba de descargo | RECOMENDADO | Politica de retencion del expediente ARCO-POL/incidentes | MOD-016 Retencion y Eliminacion | Registro / aprobacion / archivo | 5 anios desde el cierre del expediente (plazo que fija la propia obligacion; RECOMENDADO, requiere validacion de abogado) |
| OBL-RET-06 | Requisitos de la conservacion electronica de documentos con relevancia legal | OBLIGATORIO | Politica de gestion documental electronica; Controles tecnicos de integridad (hash, sello de tiempo) | MOD-016 Retencion y Eliminacion | Registro / aprobacion / archivo | Minimo 5 anios tras el cierre del caso relacionado |
---

## 13.3 AuditLog: catalogo de eventos, integridad y consulta

### 13.3.1 Que es y que no es

MOD-018 seccion A: el AuditLog es "el registro tecnico e inmutable de acciones del sistema que queda embebido en todos los modulos desde el primer dia de uso", completamente distinto del programa sustantivo de auditoria anual (MOD-018, ver 13.4). No tiene modulo propietario unico: cada modulo escribe sus propios eventos (`06_mapa_definitivo_de_modulos.md`, seccion 7).

### 13.3.2 Catalogo consolidado de eventos que se registran

Consolidado de la seccion O ("Historial") de las 26 fichas. Toda accion que cambia el estado de un registro sustantivo, toda aprobacion o rechazo, y todo acceso de lectura a evidencia sensible queda en el AuditLog. Catalogo por tipo de evento (no repite el detalle modulo por modulo, que ya documenta cada ficha en su propia seccion O):

| Categoria de evento | Ejemplos (modulo de origen) |
|---|---|
| Creacion de un registro sustantivo | Incidente reportado (MOD-013); solicitud ARCO-POL recibida (MOD-011); tratamiento dado de alta en el RAT (MOD-006); auditoria planificada (MOD-018) |
| Cambio de estado | Evidencia que pasa de En revision a Disponible (MOD-019); incidente que pasa de Investigacion a Contencion (MOD-013); regla de retencion que pasa a Listo para eliminar (MOD-016) |
| Aprobacion o rechazo | Aprobacion de una evidencia cargada manualmente (MOD-019); aprobacion del cierre de una auditoria (MOD-018); aprobacion de una eliminacion (MOD-016); aprobacion de una notificacion de incidente (MOD-013) |
| Exportacion | Exportacion de un EvidencePackage (MOD-019); exportacion del informe de auditoria (MOD-018); exportacion del inventario de reglas de retencion (MOD-016) |
| Intento bloqueado o rechazado | Intento de eliminar un documento de cumplimiento antes de su plazo minimo (MOD-016); intento de archivar evidencia bloqueada por un procedimiento abierto (MOD-019) |
| Acceso de lectura a informacion sensible | Consulta de evidencia con nivel de sensibilidad "datos personales sensibles" o "informacion tecnica de seguridad sensible" (MOD-019); acceso de un Auditor externo invitado a un expediente especifico (MOD-013, MOD-014, MOD-018) |
| Cambio de bandera regulatoria | Activacion o reversion de `regimen_reforma_659` (MOD-024) |
| Reapertura | Reapertura de un incidente cerrado (MOD-013); reapertura de una auditoria cerrada (MOD-018) |

### 13.3.3 Datos minimos de cada evento

Ninguna ficha define, en una tabla propia de campos (equivalente a la seccion D.1 de Evidence en MOD-019), la estructura formal de un evento de AuditLog: todas la describen de forma narrativa como "quien hizo que, cuando" (por ejemplo MOD-018 seccion A). Esta seccion propone, a partir de ese patron repetido en las 26 fichas, los campos minimos que un evento deberia tener; se marca como **propuesta de esta seccion, no presente literalmente en las fichas** (ver tambien "Contradicciones y huecos detectados"):

| Campo propuesto | Contenido |
|---|---|
| Marca de tiempo | Fecha y hora del evento |
| Usuario | Quien lo ejecuto, o "Sistema" si fue una automatizacion |
| Modulo y entidad de origen | En que modulo ocurrio y sobre que registro |
| Tipo de evento | Creacion, cambio de estado, aprobacion, rechazo, exportacion, acceso de lectura, intento bloqueado |
| Valor anterior y valor nuevo | Cuando el evento es un cambio de campo o de estado |
| Motivo o justificacion | Cuando la ficha de origen lo exige (por ejemplo, un rechazo o una excepcion) |

### 13.3.4 Inmutabilidad e integridad

Anti-feature 19 de `02_validacion/22_anti_features.md`: "Permitir que un usuario borre o modifique el historial de auditoria" esta expresamente prohibido. El AuditLog es una "bitacora de solo escritura por adicion (append-only)... sin funcion de edicion ni borrado para ningun rol", ni siquiera el Administrador (MOD-014 seccion A lo cita de forma explicita).

### 13.3.5 Quien puede consultarlo

Segun el mismo anti-feature 19, el AuditLog es "visible para Auditor y Administrador". Ademas, cada ficha de modulo lo hace visible como parte de su propio historial (seccion O) para los roles que ya tienen acceso a ese expediente, y MOD-018 y MOD-019 lo consultan como fuente de contexto tecnico para sus propios procesos (auditoria sustantiva y centro de evidencias, respectivamente), sin administrarlo (`06_mapa_definitivo_de_modulos.md`, seccion 7). El rol Auditor (interno o externo) es siempre de solo lectura sobre el, en todos los modulos que lo exponen (por ejemplo MOD-018 y MOD-019, seccion C de cada ficha).

### 13.3.6 Conservacion

Cada evento de AuditLog se conserva, como minimo, el mismo plazo que el registro o expediente al que pertenece (patron repetido en las secciones J de MOD-011, MOD-013, MOD-016, MOD-017 y MOD-023: "AuditLog... igual que el expediente [del modulo de origen]"). Donde el expediente de origen no tiene todavia un plazo especifico definido (por ejemplo, MOD-015 o MOD-018 antes de que MOD-016 fije uno), la conservacion es indefinida con archivado manual (MOD-018 seccion J).

### 13.3.7 Exportacion

Ninguna ficha describe una exportacion directa del AuditLog crudo, sin acotarlo por obligacion o por expediente: la unica via de exportacion documentada en el sistema es a traves de un EvidencePackage de MOD-019 (que incluye "los eventos de AuditLog relacionados" a los filtros elegidos, MOD-019 seccion D.2) o del paquete de evidencia de una auditoria (MOD-018) o de un incidente (MOD-013) especifico. Esto se marca en "Contradicciones y huecos detectados" como un hueco.

### 13.3.8 Lectura de datos sensibles

El campo "Nivel de sensibilidad del contenido" de cada Evidencia (MOD-019 seccion D.1: Sin datos personales / Datos personales de identificacion basica / Datos personales sensibles / Informacion tecnica de seguridad sensible) determina quien puede verla; todo acceso de lectura a una Evidencia con nivel "Datos personales sensibles" o "Informacion tecnica de seguridad sensible" queda registrado en el AuditLog con quien la consulto y cuando (MOD-019 secciones D.2, J.2 y O). El mismo criterio reforzado aplica a los hallazgos de una auditoria que describan una debilidad de seguridad real, con acceso restringido a los roles con necesidad de conocerla (MOD-018 seccion P).

---

## 13.4 Programa de auditoria anual (MOD-018) y su relacion reciproca con el Centro de Evidencias (MOD-019)

### 13.4.1 Por que son dos modulos distintos

El documento maestro trataba la auditoria sustantiva y el AuditLog tecnico bajo la misma seccion ("29. Auditoria y trazabilidad"); el mapa definitivo los separa de forma explicita (decision 2.7.26 de `02_validacion/02_validacion_de_la_idea.md`). MOD-018 es el programa sustantivo (planificar, ejecutar, encontrar hallazgos, dar seguimiento a un plan de accion y cerrar formalmente un ciclo anual); MOD-019 es la vista consolidada de evidencia por obligacion. Ninguno sustituye al otro (MOD-018 seccion A).

### 13.4.2 Fundamento legal del ciclo anual

OBL-AUD-01 (propietaria MOD-018), Art. 8 lit. b) de las Politicas de Actuacion y Manejo de Datos Personales de la ACE (N. 001-0309025-DPDP), OBLIGATORIO: realizar auditorias anuales para evaluar el cumplimiento de esas Politicas. Nota de transparencia (MOD-018 seccion A): la propia Politica cita como base el Art. 50 lit. l) LPDP, que en realidad faculta a la ACE para auditar sus propias certificaciones, no para imponer un deber de auditoria interna a las empresas; esto no invalida la obligacion, que nace del texto expreso del Art. 8 lit. b de la Politica.

### 13.4.3 Ciclo del programa de auditoria

Diagrama simplificado (detalle completo de estados y transiciones en MOD-018 seccion F):

```
PLANIFICADA -> EN EJECUCION -> HALLAZGOS EN REVISION -> PLAN DE ACCION EN CURSO -> CERRADA
                                                                |                     |
                                                                +---- reabrir <-------+
                                                                    (motivo obligatorio)
```

El checklist inicial se precarga desde MOD-015 (controles vigentes) y MOD-006 (RAT vigente). Cada hallazgo (severidad Baja / Media / Alta / Critica) genera una o mas acciones del plan de accion, con tarea automatica en MOD-021. El cierre exige que todas las acciones esten en Corregida o Riesgo aceptado aprobado, con aprobacion de un Aprobador distinto de quien registro los hallazgos (salvo pyme, con advertencia visible de autorrevision).

### 13.4.4 Relacion reciproca con MOD-019 (unica excepcion aciclica del mapa)

`06_mapa_definitivo_de_modulos.md` seccion 6.1: MOD-018 y MOD-019 son el unico par de modulos de todo el mapa que se declaran mutuamente en su `depende_de`. No es un error de copia: MOD-018 consulta la evidencia ya acumulada en MOD-019 (recibida de MOD-006 a MOD-017 de forma continua) para elaborar sus hallazgos; el informe y los hallazgos resultantes de MOD-018, al cerrarse la auditoria, se registran a su vez como nueva evidencia en MOD-019. Es una dependencia de datos bidireccional y continua, no una precedencia de construccion.

```
MOD-006 RAT -----+
MOD-015 Controles-+--> MOD-018 Auditoria <====evidencia acumulada====> MOD-019 Centro de
MOD-019 Evidencias +        |          (MOD-018 consulta)                  Evidencias
                             v          (MOD-019 recibe)
                    informe + hallazgos cerrados
                    se registran como nueva evidencia en MOD-019
```

### 13.4.5 Vinculo con el informe periodico del Delegado (OBL-DPO-07)

Al cerrarse una auditoria, MOD-018 notifica al Delegado / Responsable interno que hay un informe nuevo disponible para citar en su proximo informe periodico (OBL-DPO-07, propietario MOD-002, CONDICIONAL mientras exista la figura, minimo dos veces al ano segun Art. 30 de los Lineamientos para el Delegado). Es un vinculo informativo, sin dependencia estructural declarada en el mapa (MOD-018 seccion L): MOD-018 no genera ese informe, solo le entrega un insumo mas.

### 13.4.6 Cobertura parcial antes de que MOD-018 exista (SHOULD HAVE)

MOD-018 es SHOULD HAVE. Mientras no se active, la obligacion OBL-AUD-01 queda cubierta de forma parcial por un recordatorio generico anual en el Calendario y Motor de Plazos (MOD-023, MUST HAVE) y por el AuditLog tecnico, que ya deja evidencia verificable desde el primer dia en cada modulo MUST HAVE, sin el flujo estructurado de hallazgos y plan de accion (MOD-018 seccion Q).

---
## 13.5 Paquetes de evidencia (EvidencePackage)

### 13.5.1 Tipos de paquete

MOD-019 seccion D.2, campo "Tipo de paquete":

| Tipo | Uso tipico | Contenido sugerido |
|---|---|---|
| Auditoria anual (MOD-018) | Alcance de un ciclo de auditoria en curso | Evidencia del alcance revisado, checklist de MOD-015 y MOD-006 relacionado |
| Requerimiento de la ACE | Responder a un pedido puntual de informacion o inspeccion | Evidencia completa por obligacion OBLIGATORIO, priorizada |
| Procedimiento sancionador (MOD-024) | Defensa en un expediente sancionador abierto | Evidencia relacionada con la obligacion o el hecho investigado, incluida la evidencia bloqueada por el propio expediente |
| Due diligence de cliente o socio | Demostrar el programa a un tercero antes de firmar un contrato | Segun los filtros que la empresa elija |
| Preparacion de inspeccion | Anticiparse a una diligencia preliminar de la ACE | Evidencia completa por las 105 obligaciones, priorizando OBLIGATORIO |
| Paquete a medida | Cualquier otro uso interno | Segun filtros libres |

### 13.5.2 Contenido y manifiesto de integridad

El contenido se precarga automaticamente a partir de los filtros elegidos (periodo, obligacion, modulo de origen), consultando en tiempo real la Evidencia ya acumulada mas los eventos de AuditLog relacionados; los Documentos de MOD-008 nunca se copian dentro del paquete, se referencian por version exacta (MOD-019 seccion D.2). Al generarse, el paquete calcula un **manifiesto** (lista con el hash de cada archivo incluido y el hash del conjunto); al aprobarse, calcula ademas una **firma o huella del paquete completo** (anti-feature 25 de `02_validacion/22_anti_features.md`; decision de alcance 2.7.24 de `02_validacion_de_la_idea.md`).

### 13.5.3 Doble control para envios externos

Todo paquete cuyo "Destinatario declarado" sea externo a la organizacion (la ACE, un auditor externo, un cliente o socio en due diligence) exige doble control obligatorio, **sin excepcion de pyme**: quien lo genera propone la exportacion, y una segunda persona con rol Aprobador debe aprobarla antes de que el archivo quede disponible para descarga (MOD-019 seccion C). Es una de las pocas reglas del sistema sin excepcion configurable para empresa pequena, porque el riesgo de un envio irreversible a un tercero es distinto del riesgo de una autorrevision interna.

```
                         destino interno
   BORRADOR ------------------------------------> APROBADO --> EXPORTADO --(vence plazo)--> ARCHIVADO
      |
      | destino externo declarado
      v
   PENDIENTE DE SEGUNDO CONTROL --(aprueba, rol Aprobador)--> APROBADO --> EXPORTADO
      |
      +--(rechaza, motivo obligatorio)--> BORRADOR (con el motivo visible)
```

Un paquete Exportado nunca se modifica: cualquier cambio de alcance exige generar un paquete nuevo, para que cada exportacion sea individualmente verificable (MOD-019 seccion F.2).

### 13.5.4 Registro de exportaciones

Toda exportacion queda registrada de forma permanente (quien, cuando, destinatario declarado, formato), incluso si el archivo exportado en si queda fuera del sistema una vez entregado al destinatario (MOD-019 seccion J.2). El "Historico de exportaciones" es en si mismo parte del paquete de evidencia disponible para un auditor (MOD-019 seccion N).

---

## 13.6 Conservacion (retencion de evidencia y de registros)

### 13.6.1 Coherencia con MOD-016

MOD-019 no fija un plazo de retencion propio distinto del que ya declara cada obligacion o cada modulo de origen (regla de direccion unica, `06_mapa_definitivo_de_modulos.md` seccion 4): conserva cada pieza de evidencia al menos el plazo que indique su propio origen (MOD-019 seccion J.2). Los plazos base que gobiernan esa conservacion, todos propiedad de MOD-016 salvo donde se indica:

| Retencion | Plazo | Fuente | Estado |
|---|---|---|---|
| Aviso de privacidad publicado (cada version) | Minimo 10 anos desde la publicacion | OBL-RET-04, Art. 31 Lineamientos para el Delegado | OBLIGATORIO |
| Expediente ARCO-POL cerrado | Minimo 5 anos desde el cierre | OBL-RET-05, Normativa PAS Art. 47 por analogia; Art. 5 lit. i LPDP | **RECOMENDADO, requiere validacion de abogado**: no existe norma expresa que fije este plazo |
| Expediente de incidente cerrado | Minimo 5 anos desde el cierre, con cadena de custodia (ver 13.7) | OBL-RET-05 (misma nota anterior) | **RECOMENDADO, requiere validacion de abogado** |
| Prescripcion de infracciones y sanciones (horizonte minimo usado por defecto para evidencia sin plazo propio) | 5 anos | OBL-SANC-07, Art. 29 D.L. 143 por remision del Art. 53 LPDP; Art. 47 Normativa PAS | RECOMENDADO |
| Registros mercantiles | 10 anos (hasta 5 adicionales tras liquidacion) | OBL-RET-01, Codigo de Comercio Arts. 451 y 454 | CONDICIONAL (si la empresa tiene calidad de comerciante) |
| Documentacion tributaria y contable | 10 anos | OBL-RET-02, Codigo Tributario Art. 147 | CONDICIONAL (si la empresa tiene obligaciones tributarias) |
| Documentacion LCLDA | 5 anos (operaciones) / minimo 15 anos (registros de transacciones) | OBL-RET-03, LCLDA Arts. 10 lit. b y 12 | CONDICIONAL (si la empresa es sujeto obligado bajo el Art. 2 de esa ley) |
| Conservacion electronica con relevancia legal (consentimientos, avisos, contratos) | Consultable, integra, legible, completa y sin alteraciones en cualquier momento | OBL-RET-06, Ley de Firma Electronica Art. 13-A | OBLIGATORIO |

Cuando un mismo dato tiene mas de un fundamento de retencion activo (por ejemplo, la LPDP y una obligacion tributaria), MOD-016 calcula la fecha efectiva como el maximo entre todos los plazos aplicables, nunca el minimo (MOD-016 seccion D.1 y G.7), evitando que un dato se elimine antes de tiempo por una obligacion ajena a la LPDP.

### 13.6.2 Bloqueo por procedimiento abierto

Cuando se abre un procedimiento sancionador (MOD-024) o un reclamo del titular ante la Direccion de Proteccion de Datos de la ACE (MOD-011, OBL-ARCO-14) que referencia una o mas Evidencias, esas Evidencias se marcan Bloqueada = Si de forma automatica; el sistema impide su archivado o reemplazo mientras el expediente relacionado siga abierto, sin excepcion manual, ni siquiera del Administrador (MOD-019 secciones F, G y H). El mismo mecanismo aplica al motor documental de MOD-016 para los documentos de cumplimiento (aviso, expediente ARCO-POL/incidente): forzar una eliminacion anticipada exige motivo documentado y doble aprobacion (Delegado y Responsable Legal), sin excepcion de pyme para este paso (MOD-016 secciones D.2, G.13 y H).

### 13.6.3 Eliminacion segura con constancia

OBL-SEG-05 (Art. 4 de las Politicas ACE, Medidas Fisicas lit. e, OBLIGATORIO, propietario MOD-015 Controles de Seguridad): eliminacion segura de documentos y dispositivos. El evento de eliminacion (comun a ambos motores de MOD-016) exige registrar el metodo (borrado logico, borrado fisico/definitivo, anonimizacion, destruccion fisica de documento, destruccion de dispositivo), la constancia adjunta (obligatoria si el metodo es destruccion fisica o ejecucion por proveedor externo) y la identidad del responsable que ejecuto y del aprobador (MOD-016 seccion D.3). El sistema nunca ejecuta la eliminacion tecnica real en la infraestructura del cliente (anti-feature 11 de `22_anti_features.md`); solo registra la decision, la aprobacion y la constancia.

### 13.6.4 Que pasa cuando se elimina algo que no debia eliminarse

Ningun estado terminal de eliminacion se reabre: si despues se detecta un error (por ejemplo, se elimino algo que en realidad estaba retenido por otra obligacion), el hecho se documenta como un nuevo evento en MOD-013 Incidentes de Seguridad, nunca editando el historial ya cerrado (MOD-016 seccion F, coherente con el anti-feature 19).

---

## 13.7 Cadena de custodia de la evidencia de incidentes (MOD-013)

Ninguna ficha usa el termino "cadena de custodia" como titulo de una seccion propia; el mecanismo esta descrito de forma funcional en MOD-019 seccion F, aplicado especificamente a la evidencia que proviene de MOD-013, y complementado por la seccion J de la propia ficha de MOD-013. Esta subseccion consolida ambas fuentes bajo ese nombre porque es el termino que mejor describe lo que ambas fichas ya disenan.

### 13.7.1 Mecanismo de inmutabilidad

Una vez que una Evidencia proveniente de un incidente pasa a Disponible, su contenido (archivo, huella de integridad, fecha, responsable) no puede editarse; solo puede renovarse (nueva version, la anterior se conserva como Historica) o archivarse. Este mismo mecanismo de inmutabilidad funciona como cadena de custodia funcional para la evidencia de MOD-013 (MOD-019 seccion F):

- Cada acceso de lectura queda registrado (quien, cuando).
- El archivo original nunca se sobrescribe.
- Cualquier version posterior (por ejemplo, una copia forense adicional) se agrega como una nueva pieza de evidencia enlazada al mismo incidente, nunca reemplazando la anterior.

Esto asegura que el expediente conserve intacta su capacidad probatoria si mas adelante se usa en un procedimiento sancionador (MOD-024) o ante un requerimiento de la ACE.

### 13.7.2 Dentro del propio expediente de incidente

MOD-013 seccion J: el expediente completo (todos los campos), la bitacora de deteccion y conocimiento, la bitacora de acciones de contencion y hallazgos, y el historial de vencimientos son registros versionados o de solo adicion (append-only), con fecha, hora, usuario y, cuando aplica, valor anterior y nuevo. La reapertura de un incidente cerrado nunca borra ni sobrescribe el expediente original: agrega una nueva linea de tiempo dentro del mismo caso, preservando integramente la version anterior (MOD-013 seccion F).

### 13.7.3 Constancia de notificaciones como evidencia reforzada

La constancia de envio de cada notificacion (a la ACE, a la FGR o a los titulares) incluye fecha, hora, canal, destinatario, el contenido enviado en su version fija y un hash de integridad verificable (MOD-013 seccion J), de modo que la empresa pueda demostrar no solo que notifico, sino exactamente que dijo y cuando, dentro del plazo de 72 horas de OBL-INC-01 (Art. 25 LPDP).

### 13.7.4 Retencion del expediente de incidente

5 anos desde el cierre (OBL-RET-05, propietaria MOD-016, RECOMENDADO, requiere validacion de abogado, ver 13.6.1), con bloqueo automatico mientras un procedimiento o reclamo relacionado siga abierto (ver 13.6.2).

---

## 13.8 Evidencia que el sistema nunca debe guardar (minimizacion)

Consolidado de los anti-features 1, 8, 9 y 10 de `02_validacion/22_anti_features.md` y de la seccion D.2 de MOD-019 ("Minimizacion de datos personales"):

- **Nunca copiar o centralizar la base de datos completa del cliente** (por ejemplo, toda la base de un CRM o un ERP): el sistema registra solo metadatos del tratamiento (que sistema, quien lo administra, categorias, retencion), nunca el dato personal en si (anti-features 1 y 8).
- **Nunca almacenar dentro del sistema los datos biometricos, de salud u otros datos sensibles de los titulares del cliente** como base de datos propia: se registra la existencia del tratamiento, su base legal y su ubicacion, no el dato sensible en si, salvo un adjunto puntual estrictamente necesario para un expediente ARCO-POL o de incidente, con controles reforzados (anti-feature 9).
- **Nunca guardar las imagenes de videovigilancia**: se registra el tratamiento, su base legal y su EIPD, nunca las grabaciones mismas (anti-feature 10).
- **Excepcion legitima y deliberada**: el Centro de Evidencias si puede contener datos personales de titulares externos cuando el dato personal es en si mismo el objeto de la prueba (por ejemplo, un documento de identidad adjunto a un expediente ARCO-POL, o la descripcion de las personas afectadas en un expediente de incidente); en ese caso la minimizacion no significa "no guardar el dato" sino: control de acceso por nivel de sensibilidad del contenido, guia de minimizacion visible antes de adjuntar ("no adjunte una base de datos completa ni un listado de clientes; adjunte solo el documento puntual que prueba esta obligacion, y reemplace por una referencia cualquier dato que no sea estrictamente necesario para la prueba"), y prohibicion explicita de ofrecer una funcionalidad de importacion masiva de bases de datos externas (MOD-019 seccion D.2).
- El texto de ayuda al cargar evidencia manual advierte explicitamente sobre esto en cada modulo que permite adjuntos (patron documentado primero en MOD-019 seccion D.2, replicado en MOD-013, MOD-016 y MOD-018).

---
## Contradicciones y huecos detectados

### Contradicciones (entre fichas, o entre una ficha y el mapa)

1. **Dependencia no declarada entre MOD-016 y MOD-011/MOD-013 para OBL-RET-05.**
   - Archivos: `02_validacion/mapa_modulos.json` y `03_modulos/MOD-016_ficha.md` (seccion L, "Nota de coherencia con el mapa de modulos").
   - Que dice cada fuente: `mapa_modulos.json` declara `depende_de` de MOD-016 = [MOD-006, MOD-008] y el `alimenta_a` de MOD-011 y de MOD-013 no incluye a MOD-016. La propia ficha de MOD-016 (seccion L) disena la automatizacion G.3 (crear o actualizar la regla de retencion documental de OBL-RET-05 cuando un expediente ARCO-POL o de incidente se cierra) de forma que MOD-016 necesita leer la fecha de cierre de MOD-011 y de MOD-013, lo que exige esa dependencia adicional no declarada en el mapa.
   - Cual se adopto: el mecanismo que describe la ficha propietaria de OBL-RET-05 (MOD-016), es decir, que MOD-016 lea la fecha de cierre de MOD-011 y de MOD-013 para calcular y vigilar el plazo de conservacion del expediente. Esta seccion documenta la ausencia en `mapa_modulos.json` como un hueco a corregir en una siguiente iteracion del mapa (agregar MOD-011 y MOD-013 al `depende_de` de MOD-016, y MOD-016 al `alimenta_a` de ambos), no como una funcionalidad que esta seccion deba omitir.
   - Por que: la jerarquia de esta tarea situa a la ficha del modulo propietario de la obligacion por encima de un campo de metadatos de dependencias que la misma ficha ya senala como incompleto; sin esa lectura, la automatizacion que exige OBL-RET-05 no podria ejecutarse.

2. **Referencia informativa de MOD-013 a MOD-009 (Proveedores y Encargados) no declarada en el mapa.**
   - Archivos: `02_validacion/mapa_modulos.json` y `03_modulos/MOD-013_ficha.md` (seccion L, "Nota sobre MOD-009").
   - Que dice cada fuente: `mapa_modulos.json` no incluye a MOD-009 en `depende_de` ni en `alimenta_a` de MOD-013. La ficha MOD-013 modela un campo "Proveedor/Encargado relacionado" para documentar la causa de un incidente cuando se origina en un proveedor, citando la clausula de aviso de incidentes de `01_legal/sweep_encargados_transferencias.md` seccion 5.6.
   - Cual se adopto: el campo informativo que describe la ficha MOD-013, sin proponerlo como una dependencia estructural nueva del mapa, tal como la propia ficha ya lo distingue ("referencia informativa... sin ser dependencia formal").
   - Por que: no hay una instruccion contraria de una fuente de mayor jerarquia (matriz de obligaciones o mapa definitivo) que la contradiga; es una omision de metadatos senalada por la propia ficha, no una contradiccion sustantiva de contenido.

### Huecos (piezas que ninguna ficha define)

3. **Estructura formal de campos del AuditLog.** Ninguna de las 26 fichas define, en una tabla de campos (equivalente a la seccion D.1 de Evidence en MOD-019), la estructura formal de un evento de AuditLog; todas lo describen de forma narrativa ("quien hizo que, cuando"). La tabla de la subseccion 13.3.3 de esta seccion es una propuesta de esta seccion, no presente literalmente en las fichas, construida a partir del patron repetido en ellas.

4. **Reporte de exportacion del AuditLog crudo.** Ninguna ficha describe una exportacion del AuditLog completo sin acotarlo a una obligacion o a un expediente especifico: toda exportacion documentada pasa por un EvidencePackage de MOD-019 o por el paquete especifico de una auditoria (MOD-018) o de un incidente (MOD-013). Si una organizacion necesita el registro tecnico completo ante un requerimiento amplio de la ACE, ningun modulo describe ese reporte especifico; esta seccion no lo inventa, solo senala el vacio.

5. **Plazo de retencion definitivo para el informe de auditoria (MOD-018) y para la evidencia tecnica de MOD-015.** Ambas fichas declaran su propia evidencia como "conservacion indefinida con archivado manual hasta que el motor de retencion documental (MOD-016) defina un plazo especifico" (MOD-018 seccion J; MOD-015 seccion J, mismo criterio). No es una contradiccion entre fichas (ambas coinciden en el mismo criterio provisional), pero es un hueco real: el catalogo fijo de tipos de documento de cumplimiento de MOD-016 (seccion D.2) solo cubre hoy tres tipos (aviso de privacidad publicado, expediente ARCO-POL cerrado, expediente de incidente cerrado), sin incluir todavia el informe de auditoria ni la evidencia tecnica de controles como un cuarto y quinto tipo con plazo propio. Esta seccion no fija ese plazo por su cuenta, conforme a la regla de no inventar plazos que ninguna fuente defina.

6. **Plazo de conservacion de OBL-RET-05 (expediente ARCO-POL e incidentes).** No es un hueco ni una contradiccion en si mismo (el criterio de 5 anos esta documentado de forma consistente en MOD-016, MOD-013 y MOD-019), pero se deja constancia aqui de que su clasificacion es RECOMENDADO y su condicion expresa en `matriz_obligaciones.json` es "criterio de diseno recomendado ante ausencia de norma expresa; requiere validacion de abogado". Esta seccion mantiene esa marca en toda referencia al plazo (13.2, 13.6.1, 13.7.4), sin tratarlo como una regla legal cerrada.
