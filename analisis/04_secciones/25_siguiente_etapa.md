# 25. Recomendacion de siguiente etapa

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (prohibido codigo, SQL, APIs, esquemas de base de datos, nombres de tecnologias, stack o infraestructura). Esta seccion no disena ninguna funcionalidad nueva ni reabre ninguna decision ya tomada en las secciones 1 a 24 ni en las 26 fichas de `03_modulos/`: ordena, en una secuencia de seis pasos, el trabajo que debe seguir despues de que este blueprint funcional se entregue, y conecta cada paso con los riesgos de `23_riesgos_del_producto.md` (IDs `RIESGO-<CATEGORIA>-NN`) y las preguntas de `24_preguntas_pendientes.md` (IDs `PP-<TIPO>-NN`) que ese paso reduce o cierra. Todo OBL-ID citado es el identificador canonico de `01_legal/matriz_obligaciones.json`; ningun ID de esta seccion es nuevo, salvo donde se marca de forma explicita "[propuesta de esta seccion]".

Esta seccion no toma ninguna decision juridica por el equipo del producto ni por el cliente: donde una recomendacion depende de una incertidumbre juridica genuina, se dice asi y se marca "requiere validacion de asesoria juridica"; donde depende solo de una preferencia de negocio o de diseno, se marca "[opinion de producto]".

---

## 25.1 Vision general de la secuencia

Los seis pasos no son fases estrictamente sucesivas: el paso 1 (validaciones bloqueantes) y el paso 2 (prototipo de UX) pueden correr en paralelo porque dependen de audiencias distintas (asesoria juridica y clientes piloto, frente a usuarios de prueba de usabilidad); ambos alimentan el paso 3 (PRD por modulo), del cual dependen a su vez el paso 4 (que solo se nombra) y el paso 5 (que puede avanzar en paralelo al paso 4). El paso 6 (plan de pilotos) cierra la secuencia porque necesita el alcance ya fijado en el PRD y, cuando aplique, el contenido normativo y de ayuda ya gobernado.

```
PASO 1                          PASO 2
Validaciones bloqueantes         Prototipo de UX de los
(juridica externa, reforma 659   recorridos criticos
y disposiciones ACE, piloto de   (onboarding+diagnostico,
decisiones de producto)          ARCO-POL, incidentes)
        |                                |
        +----------------+---------------+
                          |
                          v
                     PASO 3
           PRD por modulo del MVP
           (20 modulos MUST HAVE,
            a partir de las fichas)
                          |
             +------------+------------+
             v                         v
        PASO 4                    PASO 5
        Fase de arquitectura      Plan de contenido
        tecnica y modelo de       normativo y de ayuda
        datos (solo se nombra    (MOD-024, MOD-026),
        como siguiente fase;     con gobierno y
        entradas: secciones      revision juridica
        9 a 13 y fichas de
        03_modulos)
             |                         |
             +------------+------------+
                          |
                          v
                       PASO 6
          Plan de pilotos y criterios
          funcionales de salida a mercado
```

Convencion usada en las tablas de 25.2 a 25.7: la fila "Participantes" usa el nombre exacto de los 12 roles estandar de `02_validacion/05_tipos_de_usuario.md`, seccion 5.3, cuando el participante es un usuario del sistema; cuando el participante es el equipo del propio proveedor del software (por ejemplo quien redacta contenido normativo o decide arquitectura tecnica), se marca explicitamente como tal, porque ese rol no es uno de los 12 roles estandar de la organizacion cliente (misma convencion que la seccion 23.2.7).

---

## 25.2 Paso 1: Validaciones bloqueantes

Este paso agrupa tres validaciones de naturaleza distinta que comparten una misma condicion: ninguna de las tres la puede cerrar el equipo de analisis funcional ni un agente de IA, y las tres deben resolverse (o al menos iniciarse) antes de comprometer el PRD del paso 3, porque varias preguntas bloqueantes de la seccion 24 dependen de ellas.

### 25.2.1 Validacion juridica con asesoria externa

| Campo | Contenido |
|---|---|
| Objetivo | Obtener el criterio de un abogado salvadoreno especializado en proteccion de datos sobre las preguntas juridicas bloqueantes que ningun documento de este analisis puede cerrar por si solo. |
| Entregable | Dictamen o memorando de asesoria externa que responda, una por una, las preguntas juridicas bloqueantes de 24.1, confirmando o corrigiendo el criterio conservador que el blueprint ya usa mientras tanto. |
| Participantes | Asesoria juridica externa (abogado especializado, no es uno de los 12 roles del sistema); Responsable Legal / Compliance como interlocutor tecnico; Delegado de Proteccion de Datos (o Responsable interno) como quien opera hoy los procesos afectados. |
| Dependencias | Ninguna interna al blueprint: puede iniciarse de inmediato. Condiciona el paso 3 para los modulos que dependen de estas preguntas (MOD-011, MOD-013, MOD-023, MOD-009, MOD-002, MOD-024). |
| Criterio de terminado | Cada pregunta bloqueante de 24.1 tiene una respuesta de asesoria externa documentada, o una confirmacion explicita de que el criterio conservador del blueprint se mantiene mientras tanto por decision informada, no por omision. |
| Riesgos que reduce | RIESGO-JUR-02, RIESGO-JUR-06, RIESGO-JUR-07. |
| Preguntas que cierra | PP-JUR-01, PP-JUR-02, PP-JUR-03, PP-JUR-04, PP-JUR-06, PP-JUR-13, PP-JUR-14. |

Nota: PP-JUR-13 y PP-JUR-14 tambien dependen de que se confirme la publicacion oficial de la reforma 659 (ver 25.2.2); la asesoria externa puede adelantar su analisis sobre el texto aprobado por la Asamblea, pero la confirmacion final exige el texto publicado en el Diario Oficial.

### 25.2.2 Seguimiento de la reforma 659 y de nuevas disposiciones de la ACE

| Campo | Contenido |
|---|---|
| Objetivo | Confirmar si el Decreto Legislativo 659 ya se publico en el Diario Oficial y transcurrio su vacatio legis de 8 dias (Art. 64 LPDP), y establecer un proceso continuo de monitoreo del Diario Oficial, de la Asamblea Legislativa y de la ACE, no solo un chequeo puntual. |
| Entregable | Bitacora de monitoreo regulatorio (fecha de cada revision, fuente consultada, resultado) y, si corresponde, el evento auditable de activacion de la bandera `regimen_reforma_659` en MOD-024, ejecutado solo tras confirmacion oficial. |
| Participantes | Equipo del producto (proveedor; no es uno de los 12 roles de la organizacion cliente), con la persona o comite que se designe en el punto de decision 25.8.1; asesoria juridica externa para validar el texto oficial contra el contenido ya construido sobre fuentes secundarias. |
| Dependencias | Ninguna interna; corre en paralelo a 25.2.1. Condiciona el contenido de MOD-002 y MOD-024 que se redacte en el paso 3 y en el paso 5. |
| Criterio de terminado | Existe una respuesta documentada (con fecha de verificacion) sobre el estado de publicacion del decreto, y un proceso de monitoreo con periodicidad definida que sigue operando aunque la reforma 659 ya se resuelva, para cubrir disposiciones futuras de la ACE. |
| Riesgos que reduce | RIESGO-JUR-01, RIESGO-NORM-01, RIESGO-NORM-02, RIESGO-NORM-04, RIESGO-NORM-05, RIESGO-NORM-06. |
| Preguntas que cierra | PP-REG-01, PP-REG-02, PP-REG-03, PP-REG-06, PP-JUR-11. |

### 25.2.3 Validacion con clientes piloto de las decisiones marcadas como opinion de producto

| Campo | Contenido |
|---|---|
| Objetivo | Confirmar o corregir, con datos reales de empresas salvadorenas (no con supuestos), las decisiones que el blueprint ya adopto como "[opinion de producto]" y que condicionan el alcance del MVP antes de redactar el PRD. |
| Entregable | Informe de validacion con al menos un grupo reducido de clientes o prospectos piloto: confirma o ajusta la hipotesis de herramientas actuales (Excel, Word, correo, carpetas compartidas), la suficiencia del formulario interno de ARCO-POL frente a un portal publico, la ausencia de necesidad de multi-sociedad en el MVP, y quien es el comprador economico real en una pyme. |
| Participantes | Equipo del producto (proveedor, direccion de producto y comercial); Administrador de la organizacion y Delegado de Proteccion de Datos (o Responsable interno) de cada empresa piloto entrevistada. |
| Dependencias | Ninguna interna; puede correr en paralelo a 25.2.1 y 25.2.2. Sus resultados condicionan el paso 3 (alcance exacto de MOD-011, MOD-012, MOD-001) y el paso 6 (perfil de piloto a priorizar). |
| Criterio de terminado | Cada pregunta de producto bloqueante de 24.3 tiene una respuesta basada en evidencia de al menos una empresa real, no solo en el criterio del equipo de analisis. |
| Riesgos que reduce | RIESGO-COM-02, RIESGO-COM-05, RIESGO-COM-06, RIESGO-OPS-05. |
| Preguntas que cierra | PP-PROD-01, PP-PROD-06, PP-PROD-08, PP-COM-04. |

---

## 25.3 Paso 2: Prototipo de UX de los recorridos criticos

| Campo | Contenido |
|---|---|
| Objetivo | Probar, antes de comprometer el diseno de navegacion completo, que una persona sin formacion juridica puede completar los tres recorridos mas criticos del producto, y decidir si la segmentacion de complejidad en tres niveles (Basico/Intermedio/Especialista) se adopta, se ajusta o se descarta, conforme exige el anti-feature 24 de `02_validacion/22_anti_features.md`. |
| Entregable | Prototipo navegable (sin funcionalidad real) de tres recorridos: onboarding mas diagnostico inicial (MOD-003 y MOD-004), presentacion y seguimiento de una solicitud ARCO-POL (MOD-011), y registro de un incidente de seguridad (MOD-013); informe de hallazgos de usabilidad de al menos una ronda de pruebas con usuarios reales no juristas, con el tiempo real de onboarding medido; decision documentada sobre la segmentacion de tres niveles. |
| Participantes | Equipo del producto (proveedor, diseno de interfaz e investigacion de UX); usuarios de prueba con el perfil de Karla Hernandez y de Jorge Menendez (`02_validacion/05_tipos_de_usuario.md`); Responsable Legal / Compliance y Delegado de Proteccion de Datos, para confirmar que el fundamento legal en segundo nivel sigue siendo correcto aunque el texto principal se simplifique. |
| Dependencias | Puede iniciarse en paralelo al paso 1. No depende de que las preguntas juridicas bloqueantes esten resueltas, porque el prototipo prueba navegacion y lenguaje, no el contenido juridico final; si depende de que existan ya los textos de descargo estandar de `04_objetivo_exacto_del_producto.md`, seccion 1.3, para probarlos con usuarios reales. |
| Criterio de terminado | Al menos una ronda de pruebas de usabilidad completada sobre los tres recorridos con usuarios reales no juristas; una decision explicita (adoptar, ajustar o descartar) sobre la segmentacion en tres niveles, documentada de forma que deje de figurar como "opinion de producto sin validar"; un tiempo objetivo de onboarding fijado y contrastado contra la medicion real. |
| Riesgos que reduce | RIESGO-UX-01, RIESGO-UX-02, RIESGO-UX-03, RIESGO-UX-06. |
| Preguntas que cierra | PP-UX-01, PP-UX-03, PP-UX-04, PP-UX-05, PP-PROD-02. |

---

## 25.4 Paso 3: PRD por modulo del MVP

| Campo | Contenido |
|---|---|
| Objetivo | Traducir cada una de las 20 fichas de modulo MUST HAVE (mas los cinco mecanismos de cobertura parcial de los modulos SHOULD HAVE, seccion 19.4) en un documento de requisitos de producto que un equipo de diseno y de desarrollo pueda usar sin releer todo el corpus juridico, sin perder ninguna obligacion OBLIGATORIO ya identificada en la ficha de origen. |
| Entregable | Un PRD por cada uno de los 20 modulos MUST HAVE de `02_validacion/mapa_modulos.json` (con historias de usuario por rol, criterios de aceptacion, y remision explicita a cada OBL-ID y a la seccion Q de su ficha de origen en `03_modulos/`), mas una nota de alcance para cada uno de los cinco mecanismos de cobertura parcial SHOULD HAVE de 19.4; de forma incidental, este paso es tambien el momento natural para cerrar las discrepancias de mapa PP-MAPA-01 a PP-MAPA-15 de la seccion 24.7, porque redactar el PRD obliga a confirmar la dependencia real entre modulos. |
| Participantes | Equipo del producto (proveedor, gestion de producto); Responsable Legal / Compliance, que revisa que ningun PRD omita una obligacion OBLIGATORIO de la ficha; Delegado de Proteccion de Datos, para los modulos que operan actos atribuidos a ese rol (MOD-002, MOD-007, MOD-011). |
| Dependencias | Depende del paso 1 para los modulos cuyo alcance cambia segun la respuesta juridica o de producto (MOD-011 y MOD-013 por el computo de plazos; MOD-002 y MOD-024 por la reforma 659; MOD-012 por la decision sobre el portal publico); depende del paso 2 para no rehacer el PRD de los tres recorridos ya prototipados. Consume `02_validacion/mapa_modulos.json`, la secuencia de construccion de 19.9 y las 26 fichas de `03_modulos/`. |
| Criterio de terminado | Existe un PRD publicado por cada uno de los 20 modulos MUST HAVE, cada uno con trazabilidad completa a su OBL-ID propietario, sin ninguna funcionalidad que la ficha de origen no contenga (o marcada de forma expresa como nueva decision de producto posterior a este blueprint). |
| Riesgos que reduce | RIESGO-OPS-05, RIESGO-OPS-08. |
| Preguntas que cierra | PP-PROD-04, PP-PROD-05. |

---

## 25.5 Paso 4: Fase de arquitectura tecnica y modelo de datos (solo se nombra como siguiente fase)

Este paso no disena arquitectura tecnica ni modelo de datos: por regla del proyecto (`00_contexto_para_agentes.md`), esta fase de analisis funcional no puede hacerlo. Esta subseccion solo deja constancia de que existe como siguiente fase y de que entradas de este blueprint debe recibir, para que el equipo de arquitectura no tenga que reconstruir decisiones que este documento ya tomo.

| Campo | Contenido |
|---|---|
| Objetivo | Entregar al equipo de arquitectura tecnica del proveedor las entradas funcionales ya cerradas por este blueprint, sin disenar la arquitectura ni el modelo de datos desde esta fase. |
| Entregable | Paquete de entrada (brief) que remite a las secciones 9 a 13 de `analisis/04_secciones/` (`09_modelo_conceptual.md`, `10_dependencias_entre_modulos.md`, `11_roles_y_permisos.md`, `12_tareas_y_alertas.md`, `13_evidencia_y_auditoria.md`) y a las 26 fichas de `03_modulos/`, mas la lista explicita de riesgos que esta fase debe resolver por tratarse de decisiones de arquitectura, no de producto: RIESGO-SEG-01, RIESGO-SEG-07 (aislamiento multi-cliente) y RIESGO-OPS-09 (volumen del AuditLog). |
| Participantes | Equipo del producto (proveedor, arquitectura tecnica), como receptor; equipo del producto (proveedor, gestion de producto), como quien entrega el paquete de entrada. Ningun rol de la organizacion cliente participa en esta fase. |
| Dependencias | Depende de que el paso 3 (PRD por modulo) exista, porque la arquitectura tecnica se disena sobre requisitos funcionales ya fijados, no sobre fichas en bruto que todavia podrian ajustarse. |
| Criterio de terminado | El equipo de arquitectura tecnica confirma haber recibido y revisado el paquete de entrada; el criterio de terminado de la fase de arquitectura en si misma queda fuera del alcance de este blueprint. |
| Riesgos que reduce | Ninguno se reduce desde esta seccion; se transfieren explicitamente para que no se pierdan: RIESGO-SEG-01, RIESGO-SEG-07, RIESGO-OPS-09 (los tres con riesgo residual Alto en 23.2, precisamente porque su mitigacion completa excede el alcance funcional). |
| Preguntas que cierra | Ninguna: PP-JUR-07, PP-JUR-08, PP-REG-05, PP-REG-07 y el hueco de gobierno del AuditLog (23.2.4, RIESGO-OPS-09) permanecen abiertos hasta que la fase de arquitectura los aborde con la informacion tecnica que este blueprint no produce. |

---

## 25.6 Paso 5: Plan de contenido normativo y de ayuda (MOD-024 y MOD-026)

| Campo | Contenido |
|---|---|
| Objetivo | Definir el proceso de gobierno y de revision juridica del contenido normativo consultable (MOD-024) y de la ayuda contextual (MOD-026), que hoy ninguna ficha detalla mas alla de mencionar un "editor de contenido regulatorio con revision juridica" fuera del RBAC de la organizacion cliente (nota final de MOD-024 y de MOD-026, huecos 3 y 4 de la seccion 24). |
| Entregable | Documento de gobierno de contenido que asigna de forma explicita: quien autoriza el cambio de la bandera `regimen_reforma_659` y que evidencia debe dejar ese cambio; con que periodicidad y quien revisa el Diario Oficial y las publicaciones de la ACE; quien mantiene el calendario de dias y horas habiles de MOD-023 cada ano y con que fuente; y quien redacta, quien aprueba y con que periodicidad se revisa el catalogo minimo de articulos de ayuda de MOD-026 (al menos 3 a 6 por cada uno de los 20 modulos MUST HAVE, seccion 19.3). |
| Participantes | Equipo del producto (proveedor: editor de contenido regulatorio con revision juridica, no es uno de los 12 roles de cliente); asesoria juridica externa del proveedor; Delegado de Proteccion de Datos (o Responsable interno), como usuario que valida que el lenguaje sencillo no pierde precision legal; Responsable Legal / Compliance del lado cliente, como validador de la usabilidad del contenido de ayuda. |
| Dependencias | Depende de que el paso 1.2 (seguimiento de la reforma 659 y de la ACE) ya tenga un proceso de monitoreo asignado, porque este plan de contenido consume ese proceso en vez de duplicarlo; puede avanzar en paralelo al paso 4. Consume el PRD de MOD-024 y MOD-026 del paso 3 para saber que pantallas necesitan ayuda contextual. |
| Criterio de terminado | Existe un documento de gobierno de contenido firmado que responde, cada una, las preguntas de operacion de la seccion 24.6; el catalogo minimo de articulos de ayuda de los 20 modulos MUST HAVE esta redactado y con su primera revision juridica registrada. |
| Riesgos que reduce | RIESGO-JUR-01, RIESGO-NORM-01, RIESGO-NORM-02, RIESGO-NORM-03, RIESGO-NORM-06. |
| Preguntas que cierra | PP-OPS-01, PP-OPS-02, PP-OPS-03, PP-OPS-04, PP-OPS-05, PP-JUR-11, PP-REG-04. |

---

## 25.7 Paso 6: Plan de pilotos y criterios funcionales de salida al mercado

| Campo | Contenido |
|---|---|
| Objetivo | Definir con que clientes piloto reales se valida el MVP completo antes del primer lanzamiento comercial general, y confirmar o ajustar, con evidencia real, los criterios funcionales de salida a mercado ya propuestos en la seccion 19.6. |
| Entregable | Plan de pilotos (perfil de cliente a priorizar segun 19.7, numero de empresas piloto, que workflows de extremo a extremo se prueban) y un checklist de salida a mercado confirmado o corregido contra la evidencia de esos pilotos, sobre las siete condiciones de 19.6. |
| Participantes | Equipo del producto (proveedor, direccion comercial y de producto); Administrador de la organizacion y Delegado de Proteccion de Datos (o Responsable interno) de cada empresa piloto; Responsable ARCO-POL / Responsable del tramite y Responsable de Seguridad / IT de esas mismas empresas, como quienes ejecutan los casos de prueba. |
| Dependencias | Depende de que el paso 3 (PRD por modulo) fije el alcance exacto que se va a probar, y del punto de decision 25.8.3 (modelo comercial) para poder ofrecer el piloto en condiciones reales; puede avanzar en paralelo al desarrollo del segundo grupo de modulos de 19.8 si el nucleo vendible ya esta operativo. |
| Criterio de terminado | Al menos una empresa piloto real completa, de inicio a fin y sin salir del sistema, los casos 1 (empresa nueva implementa el sistema), 2 (registra un nuevo proceso), 3 (marketing implementa un formulario), 7 (titular solicita acceso), 8 (titular solicita eliminacion) y 9 (ocurre una brecha de datos) de los workflows de la seccion 19.6, punto 3; las siete condiciones de esa misma seccion quedan verificadas o corregidas con evidencia real, no solo con el juicio del equipo de analisis. |
| Riesgos que reduce | RIESGO-COM-01, RIESGO-COM-02, RIESGO-COM-05, RIESGO-COM-06, RIESGO-OPS-04, RIESGO-UX-04. |
| Preguntas que cierra | PP-PROD-03, PP-PROD-07, PP-PROD-09, PP-COM-01, PP-COM-02, PP-COM-03. |

---

## 25.8 Puntos de decision que el cliente debe tomar ahora

Estos son los puntos donde el equipo del producto (el cliente de este blueprint funcional) debe decidir, no solo leer una recomendacion, porque los pasos 1 a 6 no pueden avanzar sin una respuesta. Ninguno de estos puntos resuelve una incertidumbre juridica genuina: son decisiones de gobierno, de negocio o de producto, marcadas como tales.

### 25.8.1 Gobernanza de la activacion de la bandera `regimen_reforma_659`

| Campo | Contenido |
|---|---|
| Opciones | (a) Designar una sola persona del equipo del producto con autoridad para autorizar el cambio, con registro auditable de cada decision. (b) Exigir un comite de al menos dos personas (doble control) antes de activar el cambio de ACTUAL a FUTURO. (c) Dejarlo sin definir por ahora y decidirlo cuando se confirme la publicacion. |
| Recomendacion | (b) [opinion de producto], por la severidad Critica y el alcance transversal de este riesgo: una sola bandera mal activada cambia 17 obligaciones para todos los clientes a la vez (RIESGO-JUR-01, RIESGO-NORM-02). |
| Consecuencia de no decidir | Si el Diario Oficial publica el decreto antes de que exista esta gobernanza, nadie tiene autoridad clara para activar el cambio a tiempo, o alguien lo activa sin la validacion debida (23.4, fila RIESGO-JUR-01 / RIESGO-NORM-02). |

### 25.8.2 Alcance del primer lanzamiento comercial

| Campo | Contenido |
|---|---|
| Opciones | (a) Lanzar con el nucleo vendible de 10 modulos de la seccion 19.8 y completar el segundo grupo de otros 10 en las semanas siguientes. (b) Esperar a que los 20 modulos MUST HAVE esten completos antes del primer cliente. (c) Reclasificar algunos modulos MUST HAVE a SHOULD HAVE para reducir el alcance del MVP mismo. |
| Recomendacion | (a) [opinion de producto, ya propuesta en la seccion 19.8], siempre que se confirme que ningun modulo del nucleo deja una obligacion con plazo ya vencido (OBL-PLAZO-03, OBL-PLAZO-04) sin cobertura funcional completa. |
| Consecuencia de no decidir | El equipo de desarrollo no tiene un orden de prioridad claro entre 20 modulos MUST HAVE, con riesgo de retraso no planificado o de lanzar con modulos MUST HAVE incompletos (RIESGO-OPS-05, ya senalado como decision pendiente en 23.4). |

### 25.8.3 Modelo comercial y empaquetado

| Campo | Contenido |
|---|---|
| Opciones | (a) Suscripcion unica que incluye todos los modulos MUST HAVE desde el inicio. (b) Licencia por paquetes, donde un primer paquete cubre el nucleo vendible de 19.8 y un paquete superior agrega el segundo grupo y los modulos SHOULD HAVE. (c) Diferir toda decision de precio y empaquetado hasta tener datos de los pilotos del paso 6. |
| Recomendacion | Fijar al menos la estructura de paquetes (opcion (b), sin cerrar el precio final) antes de redactar el PRD del paso 3, porque el empaquetado afecta como se agrupan las pantallas; el precio final si puede esperar a la evidencia de los pilotos [opinion de producto]. |
| Consecuencia de no decidir | El PRD y el material comercial no tienen una oferta clara que mostrar a los primeros clientes, y la pregunta bloqueante PP-COM-01 sigue abierta indefinidamente. |

### 25.8.4 Segmento de cliente piloto a priorizar

| Campo | Contenido |
|---|---|
| Opciones | (a) Priorizar el segmento pyme (mayor volumen de mercado potencial, ciclo de venta mas largo, perfil "Karla Hernandez"). (b) Priorizar sectores regulados de alto riesgo (bancos, seguros, salud; menor volumen, mayor urgencia regulatoria). (c) Disenar el primer piloto sin priorizar ningun segmento. |
| Recomendacion | Elegir (a) o (b) de forma explicita para el primer piloto del paso 6, aunque el producto sirva a ambos perfiles despues [opinion de producto; ninguna fuente del corpus resuelve esta priorizacion, ver RIESGO-COM-06]. |
| Consecuencia de no decidir | El diagnostico inicial, el onboarding y el material comercial quedan sin un publico objetivo claro, y el equipo comercial intenta servir a ambos perfiles de riesgo a la vez sin una decision explicita (RIESGO-COM-06, ya senalada como decision pendiente en 23.4). |

### 25.8.5 Adopcion de la segmentacion de navegacion en tres niveles

| Campo | Contenido |
|---|---|
| Opciones | (a) Mantenerla como hipotesis de trabajo y decidir solo despues del prototipo de UX del paso 2. (b) Descartarla desde ahora y disenar una navegacion unica simplificada para todos los usuarios. (c) Adoptarla ya, sin prueba previa con usuarios reales. |
| Recomendacion | (a), que es exactamente lo que exige el anti-feature 24 de `02_validacion/22_anti_features.md`; la opcion (c) esta desaconsejada de forma expresa por ese mismo anti-feature. |
| Consecuencia de no decidir | Se compromete un diseno de navegacion completo (a tres niveles fijos) sin haberlo probado, con riesgo de tener que rehacerlo despues de construido (RIESGO-UX-06). |

### 25.8.6 Continuidad de la asesoria juridica externa

| Campo | Contenido |
|---|---|
| Opciones | (a) Contratar asesoria juridica externa de forma puntual, solo para cerrar las preguntas bloqueantes de 24.1. (b) Contratar asesoria juridica externa de forma continua (retainer), que ademas mantenga al dia el contenido normativo del paso 5 y revise cada disposicion nueva de la ACE. (c) Resolver las preguntas bloqueantes con criterio interno del equipo del producto, sin abogado externo. |
| Recomendacion | (b) [opinion de producto], porque el paso 5 (plan de contenido normativo) y el seguimiento continuo de la ACE (25.2.2) dependen de disponibilidad juridica recurrente, no de una consulta unica; la opcion (c) contradice la regla no negociable de este proyecto de marcar "requiere validacion de asesoria juridica" ante toda incertidumbre. |
| Consecuencia de no decidir | Las preguntas bloqueantes de 24.1 se resuelven una vez, pero el contenido normativo se desactualiza en cuanto la ACE publique algo nuevo, sin que nadie con autoridad juridica lo revise (RIESGO-NORM-03, RIESGO-NORM-06, huecos 2 y 3 de la seccion 24). |

---

## Contradicciones y huecos detectados

No se detectaron contradicciones entre las secciones 19, 23 y 24 al construir esta secuencia: los seis pasos usan exclusivamente riesgos y preguntas ya registrados en esos documentos, sin reclasificar ningun modulo ni reinterpretar ninguna obligacion.

Huecos que esta seccion deja abiertos de forma deliberada, por exceder el alcance de un blueprint funcional:

1. Ningun documento de esta fase fija plazos calendario ni duracion estimada para ninguno de los seis pasos: serian estimaciones tecnicas o de capacidad de desarrollo que ninguna fuente respalda, y esta seccion no las inventa.
2. El criterio de terminado del paso 4 (fase de arquitectura tecnica) queda deliberadamente sin definir, porque definirlo exigiria disenar esa fase, prohibido para el analisis funcional.
3. El costo de la asesoria juridica continua del punto 25.8.6 y el precio final del punto 25.8.3 no se estiman aqui: son decisiones de negocio fuera del alcance de un documento de analisis funcional, igual que ya lo declara `02_validacion_de_la_idea.md`, seccion 2.3.4.
