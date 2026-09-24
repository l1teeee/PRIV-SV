# Sweep juridico: Vulneraciones de seguridad e incidentes

Lente asignado: Vulneraciones de seguridad e incidentes (Art. 25 LPDP, canal de notificacion, Ley de
Ciberseguridad, reforma a la Ley Especial contra los Delitos Informaticos y Conexos, infracciones,
evidencia, ciclo de vida del incidente).

Fecha de consulta de todas las fuentes: 2026-09-23 y 2026-09-24.

Investigador: agente de IA (Claude Sonnet 5), equipo de producto PRIV-SV.

---

## 1. Resumen ejecutivo

1. El Art. 25 de la Ley para la Proteccion de Datos Personales (LPDP, Decreto 144) es la norma central
   de este lente. Establece un plazo maximo de 72 horas "desde que se tuvo conocimiento de la
   vulneracion" para notificar a tres destinatarios distintos (ACE, FGR, titulares afectados), cada uno
   con contenido minimo propio, y ademas obliga a iniciar dentro del mismo plazo una revision exhaustiva
   y a documentar toda vulneracion que "ocasione un riesgo". El texto no define que es "tener
   conocimiento" ni si las 72 horas son corridas o habiles: ambos puntos requieren un criterio
   operativo propio del producto (ver seccion 2) y confirmacion de un abogado.
2. La ACE no tiene un formulario ni plataforma dedicada para "Reporte de Incidentes". La tarjeta de
   servicio en ace.gob.sv/page/formularios redirige al canal general de contacto (telefono, correo,
   formulario web de contacto), a diferencia de los tramites ARCO-POL que si tienen formularios PDF
   propios. Esto es un hallazgo operativo importante: el software no puede asumir un "numero de
   expediente" o acuse automatizado como el que existe en otras jurisdicciones.
3. La Ley de Ciberseguridad y Seguridad de la Informacion (Decreto 143) tiene un ambito de aplicacion
   (Art. 2) limitado al sector publico y a los operadores de infraestructura critica formalmente
   calificados por la ACE (Art. 8 lit. f). La mayoria de empresas privadas clientes de PRIV-SV
   probablemente NO son "sujetos obligados" bajo el Decreto 143, salvo que operen infraestructura
   critica y hayan sido calificadas como tal. El Decreto 143 tampoco fija un plazo numerico (tipo
   "72 horas") para que el sujeto obligado reporte un incidente a la ACE: usa estandares abiertos
   ("de manera inmediata y eficaz", "de forma oportuna, expedita y eficiente"). El unico plazo de 72
   horas que aparece en el Decreto 143 corre a cargo de la ACE hacia la FGR (Art. 8 lit. v), no del
   sujeto obligado.
4. La reforma de 2025 a la Ley Especial contra los Delitos Informaticos y Conexos (Decreto Legislativo
   332, vigente desde el 3 de julio de 2025 segun fuentes secundarias) no crea un deber de reporte de
   incidentes. Es, sobre todo, una reforma penal: agrega definiciones (dueño de datos, custodia de
   datos, controlador, procesador, metadatos), modifica el tipo de fraude informatico (aumenta la pena
   y agrega un agravante) y reconoce a las entidades que custodian, controlan o procesan datos
   personales como sujetos directamente afectados en delitos de fraude informatico, lo que les permite
   ejercer accion penal. La numeracion exacta de articulos del texto original (acceso indebido, dano a
   sistemas, interceptacion, revelacion indebida) no pudo confirmarse contra el texto oficial completo
   en esta sesion (los PDF oficiales no fueron legibles por las herramientas disponibles) y se marca con
   confianza media/baja.
5. La reforma de septiembre de 2026 (Decreto 659, que elimina el delegado obligatorio en el sector
   privado) no toca el Art. 25 segun las fuentes secundarias revisadas. Al 24 de septiembre de 2026 su
   publicacion material en el Diario Oficial seguia sin confirmarse: tratarla como aprobada pero de
   vigencia pendiente, tal como indica el contexto compartido del proyecto.
6. Omitir la notificacion de una vulneracion (Art. 25) esta clasificada como infraccion LEVE (Art. 56
   lit. a numeral 3), sancionada con multa de 1 a 10 salarios minimos mensuales del sector comercio
   (aprox. USD 408.80 a USD 4,088.00, con el salario minimo vigente de USD 408.80/mes). Esto contrasta
   con la gravedad tipica de una vulneracion de datos: el riesgo de sancion directa por Art. 25 es
   relativamente bajo comparado con otras infracciones graves o muy graves de la misma ley, aunque la
   vulneracion en si puede originar ademas responsabilidad civil, penal o sanciones por otras normas
   (Ciberseguridad, LPDP por otras causales).
7. El software puede y debe: (a) ofrecer un cronometro operativo desde el momento en que el usuario
   registra "conocimiento" de una posible vulneracion, con alertas antes de las 72 horas; (b) generar y
   conservar evidencia estructurada (bitacora, contenido de cada notificacion, acuses); (c) recordar la
   obligacion de iniciar la revision exhaustiva y la actualizacion de politicas dentro del mismo plazo;
   (d) nunca decidir por el usuario si una vulneracion "ocasiona un riesgo" o si debe notificarse: eso
   es una decision juridica del responsable (con o sin su Delegado, segun el estado de la reforma de
   2026), que el software solo apoya con informacion y checklist.

---

## 2. Art. 25 LPDP en profundidad

### 2.1 Texto integro del articulo (fuente primaria local)

> **Art. 25.-** Cuando el responsable tenga conocimiento de una vulneracion de seguridad de datos
> personales ocurrida en cualquier fase del tratamiento, entendiendose esta como cualquier daño,
> perdida, alteracion, destruccion, acceso ilegitimo, y en general, cualquier uso ilicito o no
> autorizado de los datos personales aun cuando ocurriera de manera accidental, notificara a la Agencia
> de Ciberseguridad del Estado, a la Fiscalia General de la Republica y a los titulares afectados dicho
> acontecimiento, para lo cual se establece un plazo maximo de setenta y dos horas desde que se tuvo
> conocimiento de la vulneracion de seguridad.
>
> Dentro de este mismo plazo, el responsable debera iniciar un proceso de revision exhaustiva para
> determinar la magnitud de la afectacion, y las medidas correctivas y preventivas que correspondan, asi
> como la actualizacion de las politicas de seguridad del responsable de la base de datos para evitar
> nuevas vulneraciones.
>
> La notificacion que realice el responsable a la Entidad Rectora estara redactada en un lenguaje claro
> y sencillo y contendra, al menos, la siguiente informacion:
>
> a) La naturaleza del incidente.
> b) Los datos personales comprometidos.
> c) Las acciones correctivas generales realizadas de forma inmediata.
> d) Las recomendaciones al titular sobre las medidas que este pueda adoptar para proteger sus
>    intereses.
> e) Los medios disponibles al titular para obtener mayor informacion al respecto.
>
> La notificacion dirigida a los titulares afectados unicamente debera contener lo establecido en los
> literales a), b), d) y e).
>
> Asimismo, el responsable documentara toda vulneracion ocurrida en cualquier fase del tratamiento que
> ocasione un riesgo en la seguridad de los datos personales, identificando de manera enunciativa mas no
> limitativa, la fecha en que ocurrio, el motivo de la vulneracion, los hechos relacionados con ella, sus
> efectos o implicaciones y las medidas correctivas implementadas de forma inmediata y definitiva, la
> cual estara a disposicion de la autoridad encargada de la materia.

**Fuente oficial:** `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt` (lineas 791-825),
copia de texto integro de la LPDP publicada por la ACE. Contrastar contra Diario Oficial Tomo 445, N.
219, 15 nov 2024 (archivo local `diario_oficial_2024-11-15_mh.txt`). Fecha de consulta: 2026-09-23.
**Vigencia:** VIGENTE desde el 23 de noviembre de 2024 (Art. 64 LPDP, 8 dias despues de su publicacion).

### 2.2 Definicion de "vulneracion de seguridad"

**Norma:** LPDP (Decreto 144)
**Articulo:** 25, primer inciso
**Obligacion:** No es una obligacion en si, sino la definicion legal que activa todas las demas
obligaciones del articulo. Una "vulneracion de seguridad de datos personales" es "cualquier daño,
perdida, alteracion, destruccion, acceso ilegitimo, y en general, cualquier uso ilicito o no autorizado
de los datos personales aun cuando ocurriera de manera accidental". Es una definicion deliberadamente
amplia: cubre los cuatro ejes clasicos (confidencialidad, integridad, disponibilidad, y en general
licitud del uso) e incluye expresamente los incidentes accidentales (no solo ataques dolosos).
**A quien aplica:** Al responsable del tratamiento (empresa cliente de PRIV-SV). La ley no distingue
expresamente si el encargado que sufre la vulneracion notifica directamente o via el responsable; el
Art. 34 (obligaciones de responsable y encargado) y el Art. 36 (medidas de seguridad tambien obligatorias
para el encargado) sugieren que el encargado debe informar sin demora al responsable para que este
cumpla el Art. 25, pero la ley no fija un sub-plazo para esa cadena. Se marca como incertidumbre (ver
seccion 8).
**Implicacion para el software:** El producto necesita un catalogo de tipos de evento (perdida de
dispositivo, acceso no autorizado, exfiltracion, error de envio, ransomware, error de configuracion en
la nube, etc.) mapeado a esta definicion amplia, y debe advertir que "vulneracion" incluye incidentes
accidentales y errores internos, no solo ataques externos.
**Fuente oficial:** `ace_decreto_144.txt`, linea 791. Fecha de consulta: 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (define el hecho que dispara las obligaciones del articulo).

### 2.3 Cuando nace el plazo: "desde que se tuvo conocimiento"

La ley no define "conocimiento". Es el punto mas delicado del articulo porque de el depende el computo
de las 72 horas.

**Lo que el texto permite afirmar con certeza (fuente primaria):**
- El plazo corre "desde que se tuvo conocimiento de la vulneracion", no desde que ocurrio la
  vulneracion. Puede haber una diferencia (a veces de meses) entre el momento en que una vulneracion
  ocurre tecnicamente y el momento en que el responsable la detecta o es informado de ella.
- La ley no dice "desde que debio tener conocimiento" (estandar objetivo/de diligencia) sino "desde que
  se tuvo conocimiento" (estandar que en su literalidad parece subjetivo/factico). Esto abre una
  pregunta de interpretacion: si la empresa tenia señales claras y no investigo, un regulador podria
  igualmente argumentar que el conocimiento "se tuvo" en el momento en que la señal era razonablemente
  concluyente, no en el momento en que alguien finalmente la leyo. Esta es una interpretacion posible,
  no un hecho confirmado en el texto: se marca como incertidumbre.

**Criterio operativo propuesto para el software (RECOMENDACION, no norma):**
Distinguir tres momentos y usar el segundo como disparador del cronometro de 72 horas:
1. **Evento/senal** (ej. una alerta de un sistema de monitoreo, un correo de un usuario reportando algo
   raro): todavia no es "conocimiento" de una vulneracion en el sentido del Art. 25, es solo una señal
   que amerita revision.
2. **Conocimiento** (triggers el plazo): el momento en que una persona con capacidad de decision dentro
   de la organizacion (el Delegado de Proteccion de Datos, si existe; si no, quien la empresa designe
   como responsable de gestion de incidentes) cuenta con informacion suficiente para concluir, con un
   grado razonable de certeza, que ocurrio una vulneracion de seguridad de datos personales conforme a
   la definicion del Art. 25. No hace falta conocer el alcance total ni el numero exacto de titulares
   afectados: basta con la conviccion razonable de que hubo una vulneracion.
3. **Confirmacion/alcance final:** puede llegar despues, dentro de la revision exhaustiva del segundo
   parrafo del Art. 25, y no retrasa el inicio del plazo de 72 horas.
Este criterio de "conviccion razonable" es una construccion analitica del equipo de producto inspirada
en el estandar comparado de "awareness" usado en el RGPD europeo (no aplicable en El Salvador, se cita
solo como referencia de buena practica de la industria, nunca como fuente de derecho salvadoreño) y debe
ser validado por un abogado salvadoreño antes de implementarse como regla vinculante en el producto. El
software debe dejar dicho criterio configurable y explicito para el usuario, nunca oculto.
**Clasificacion:** RECOMENDADO (criterio operativo del producto, no obligacion legal expresa; la
obligacion legal expresa es solo "notificar dentro de 72 horas desde que se tuvo conocimiento", sin mas
precision).

### 2.4 Horas corridas u horas habiles

**Norma:** LPDP Art. 25 (plazo) en relacion con la Ley de Procedimientos Administrativos (LPA, Decreto
856), Arts. 80 a 82, aplicable de forma supletoria por remision del Art. 62 LPDP ("en todo lo no
previsto en la presente ley se estara a lo dispuesto en la Ley de Procedimientos Administrativos").

**Texto literal de la LPA citado:**
> **Art. 81.-** Los actos, tanto de la Administracion como de los particulares, deberan llevarse a cabo
> en dias y horas habiles. El organo competente podra acordar, por resolucion motivada y siempre que
> existan razones de urgencia, habilitar dias y horas inhabiles para realizar actos procedimentales.
>
> **Art. 82.-** Si los plazos se señalan por dias u horas, se computaran unicamente los dias y horas
> habiles. [...]

**Argumento a favor de "horas habiles" (interpretacion mas restrictiva para la empresa):**
El Art. 62 LPDP remite expresamente a la LPA para "todo lo no previsto" en la LPDP, y la LPDP no aclara
si sus plazos en horas son corridos o habiles. El Art. 82 LPA es la regla general de computo de plazos
del ordenamiento administrativo salvadoreño y dice, sin matices, que los plazos en horas "se computaran
unicamente los dias y horas habiles". Bajo esta lectura literal y supletoria, las 72 horas del Art. 25
LPDP serian horas habiles (Lunes a Viernes, jornada laboral), lo que en la practica puede estirar el
plazo real a mas de una semana calendario si la vulneracion se detecta, por ejemplo, un viernes por la
tarde.

**Argumento a favor de "horas corridas" (interpretacion mas protectora y mas consistente con el proposito
de la norma):**
1. La LPA regula el "procedimiento administrativo", es decir, actuaciones dentro de un expediente ante
   la Administracion (Titulo III de la LPA, "Terminos y Plazos", ubicado dentro de las normas de
   tramitacion de expedientes). La notificacion del Art. 25 LPDP no es un acto dentro de un
   procedimiento administrativo ya iniciado por la ACE: es un deber sustantivo autonomo que nace
   directamente de la ley para el responsable, dirigido no solo a la ACE sino tambien a la FGR (otra
   institucion, con logica procesal distinta) y a los titulares (que no son parte de ningun
   procedimiento administrativo). Puede argumentarse que el Art. 82 LPA, pensado para plazos dentro de
   un expediente administrativo, no es directamente trasladable a un deber de notificacion como el del
   Art. 25.
2. Una vulneracion de datos no ocurre solo en horario habil: si las 72 horas solo corrieran en horario
   de oficina, una vulneracion detectada un viernes a las 17:01 practicamente no generaria presion de
   notificacion sino hasta la semana siguiente, lo que es dificil de conciliar con el proposito
   protector de la norma (permitir a los titulares reaccionar rapido y a la ACE/FGR intervenir a
   tiempo).
3. La practica comparada mas conocida en proteccion de datos (el estandar de 72 horas del RGPD europeo,
   que inspiro visiblemente la redaccion salvadoreña) se interpreta como horas corridas (calendario),
   no habiles. Aunque el RGPD no es derecho salvadoreño y no puede citarse como fuente de obligacion
   aqui, es un elemento de contexto sobre el proposito probable de la formula "72 horas".

**Conclusion para el proyecto (recomendacion operativa, no dictamen legal):** Ante la ambiguedad,
PRIV-SV deberia programar el cronometro por defecto en horas corridas (interpretacion mas exigente y mas
segura para el cliente), mostrando claramente al usuario que se trata de un criterio adoptado por el
producto ante un vacio legal, con un enlace a esta seccion del informe, y ofrecer en paralelo una
referencia informativa de cuando vencerian las 72 horas si se contaran solo en horas habiles, para que el
usuario y su abogado puedan evaluar el margen real. Esta es la unica forma de que el software no asuma
por si mismo una postura juridica no confirmada como si fuera un hecho.
**Fuente oficial:** LPDP Art. 25 y Art. 62 (`ace_decreto_144.txt`, lineas 791-825 y contexto del Art.
62); LPA Arts. 80-82 (`asamblea_decreto_856_lpa.txt`, lineas 1429-1460). Fecha de consulta: 2026-09-23.
**Vigencia:** VIGENTE (ambas normas).
**Clasificacion:** INCERTIDUMBRE JURIDICA — requiere opinion de abogado salvadoreño antes de fijarse
como regla del producto. Hasta esa confirmacion, tratar el punto como CONDICIONAL: el computo depende de
la interpretacion legal que finalmente se adopte.

### 2.5 Destinatarios y contenido minimo de cada notificacion

**Norma:** LPDP
**Articulo:** 25, incisos 3 a 5
**Obligacion:** Notificar la vulneracion a tres destinatarios distintos, cada uno con contenido minimo
propio:

| Destinatario | Contenido minimo exigido por el Art. 25 | Literal |
|---|---|---|
| Agencia de Ciberseguridad del Estado (ACE) | a) Naturaleza del incidente; b) Datos personales comprometidos; c) Acciones correctivas generales realizadas de forma inmediata; d) Recomendaciones al titular sobre medidas que este pueda adoptar; e) Medios disponibles al titular para obtener mas informacion | a, b, c, d, e (las 5) |
| Fiscalia General de la Republica (FGR) | La ley no detalla un contenido separado para la FGR; el texto dice que se notificara "dicho acontecimiento" a los tres destinatarios y luego detalla el contenido "de la notificacion que realice el responsable a la Entidad Rectora" (ACE). No hay literal especifico para FGR: se interpreta razonablemente que debe recibir, como minimo, la misma informacion que la ACE (a-e), dado que la ley no distingue un contenido reducido para la FGR como si lo hace expresamente para los titulares. Esto es una interpretacion, no un texto literal: marcar como incertidumbre menor. | (sin literal propio en el texto) |
| Titulares afectados | Unicamente a) Naturaleza del incidente; b) Datos personales comprometidos; d) Recomendaciones al titular; e) Medios para obtener mas informacion (se omite c: las acciones correctivas internas no se exigen al titular) | a, b, d, e (4 de 5) |

**A quien aplica:** Al responsable del tratamiento.
**Implicacion para el software:** El producto debe generar tres plantillas de notificacion distintas
(ACE, FGR, titulares) a partir de una unica fuente de datos del incidente, con el contenido minimo
exacto de cada una preconfigurado como campos obligatorios, y debe impedir enviar (o marcar como
incompleta) una notificacion a titulares que incluya el literal c) si el usuario no lo desea, o que
omita alguno de los literales obligatorios para cada destinatario.
**Fuente oficial:** `ace_decreto_144.txt`, lineas 800-822. Fecha de consulta: 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

### 2.6 Revision exhaustiva dentro del mismo plazo

**Norma:** LPDP
**Articulo:** 25, segundo inciso
**Obligacion:** "Dentro de este mismo plazo, el responsable debera iniciar un proceso de revision
exhaustiva para determinar la magnitud de la afectacion, y las medidas correctivas y preventivas que
correspondan, asi como la actualizacion de las politicas de seguridad del responsable de la base de
datos para evitar nuevas vulneraciones."
**Nota de precision textual:** la ley exige **iniciar** la revision exhaustiva dentro de las 72 horas,
no necesariamente concluirla en ese plazo. La revision puede seguir despues de vencidas las 72 horas; lo
que debe ocurrir dentro del plazo es el arranque formal del proceso (y, logicamente, avanzar lo
suficiente para poder cumplir el contenido minimo de las notificaciones del punto 2.5, que exige ya
conocer "la naturaleza del incidente" y "los datos personales comprometidos").
**A quien aplica:** Al responsable del tratamiento.
**Implicacion para el software:** Debe existir una tarea de "revision exhaustiva" con fecha de inicio
obligatoria dentro de la ventana de 72 horas (idealmente registrada automaticamente al marcar
"conocimiento" del incidente), separada de la tarea de "notificaciones", con su propio checklist:
magnitud de la afectacion, medidas correctivas, medidas preventivas, actualizacion de politicas de
seguridad.
**Fuente oficial:** `ace_decreto_144.txt`, lineas 802-806. Fecha de consulta: 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

### 2.7 Actualizacion de politicas de seguridad

**Norma:** LPDP
**Articulo:** 25, segundo inciso; en relacion con Politicas de Actuacion ACE N. 001-0309025-DPDP.
**Obligacion:** Actualizar las politicas de seguridad del responsable de la base de datos "para evitar
nuevas vulneraciones", como parte de la revision exhaustiva. Las Politicas de Actuacion de la ACE
confirman esta misma obligacion como mecanismo de cumplimiento y supervision ("Actualizacion de
Politicas: Adaptacion a nuevas amenazas y regulaciones", Art. 5 lit. b de dichas politicas) y ademas
listan expresamente, dentro de las medidas de seguridad en transferencias de datos, la "Notificacion de
Brechas de Seguridad: Reporte a la Agencia de Ciberseguridad del Estado, Fiscalia General de la
Republica y titulares en un maximo de 72 horas", replicando el Art. 25 LPDP.
**A quien aplica:** Al responsable del tratamiento.
**Implicacion para el software:** El modulo de politicas internas del producto debe quedar vinculado al
modulo de incidentes: cada incidente cerrado que haya generado una actualizacion de politica debe dejar
un registro de version de politica "antes/despues" y la fecha del cambio, como evidencia de cumplimiento
de este punto.
**Fuente oficial:** `ace_decreto_144.txt`, linea 805; `ace_politicas_protecciondatos.txt`, lineas
150-151 y 163-164. Fecha de consulta: 2026-09-23. Nota: la fecha exacta de emision/publicacion de esta
Politica de Actuacion sigue pendiente de verificar (ver contexto compartido del proyecto, punto 3,
tercera fila de la tabla de corpus).
**Vigencia:** VIGENTE (LPDP); Politicas de Actuacion con fecha de emision pendiente de verificar.
**Clasificacion:** OBLIGATORIO (por el texto del Art. 25); la Politica de Actuacion lo confirma como
mecanismo de cumplimiento obligatorio segun el propio texto de dicha politica.

### 2.8 Documentacion obligatoria de toda vulneracion que ocasione un riesgo

**Norma:** LPDP
**Articulo:** 25, ultimo inciso
**Obligacion:** "El responsable documentara toda vulneracion ocurrida en cualquier fase del tratamiento
que ocasione un riesgo en la seguridad de los datos personales, identificando de manera enunciativa mas
no limitativa: la fecha en que ocurrio, el motivo de la vulneracion, los hechos relacionados con ella,
sus efectos o implicaciones y las medidas correctivas implementadas de forma inmediata y definitiva, la
cual estara a disposicion de la autoridad encargada de la materia."

**Puntos clave de esta obligacion:**
1. Es una obligacion **distinta** de la notificacion. Aplica a "toda vulneracion... que ocasione un
   riesgo", no solo a las que efectivamente se notificaron. En teoria, una vulneracion que el responsable
   considero de riesgo tan bajo que no la noto podria, aun asi, requerir documentacion si de hecho
   "ocasiono un riesgo" (el estandar de activacion de la documentacion no esta expresamente atado al
   mismo estandar de activacion de la notificacion). Esto es una lectura literal del texto, no una
   interpretacion forzada; aun asi, conviene que un abogado confirme si en la practica se exige
   documentar cualquier vulneracion "de riesgo" incluso cuando no se notifico.
2. La lista de contenidos ("fecha, motivo, hechos, efectos, medidas correctivas inmediatas y
   definitivas") es enunciativa, no taxativa ("de manera enunciativa mas no limitativa"): la ACE podria
   exigir mas contenido.
3. El documento debe estar "a disposicion de la autoridad encargada de la materia" (la ACE), es decir,
   se trata de evidencia que debe poder exhibirse ante requerimiento, no necesariamente de un envio
   proactivo separado de la notificacion.
4. No hay plazo expreso para la documentacion (a diferencia de la notificacion y la revision, que si
   tienen las 72 horas). La lectura razonable es que la documentacion se construye y se completa como
   parte del mismo proceso de revision exhaustiva y de las medidas correctivas definitivas, por lo que
   en la practica debe coincidir con el cierre del incidente, no con las 72 horas iniciales.

**A quien aplica:** Al responsable del tratamiento.
**Implicacion para el software:** El expediente de incidente en PRIV-SV debe tener, como campos
minimos estructurados y obligatorios para poder cerrarse: fecha del hecho, motivo/causa, relato de los
hechos, efectos/implicaciones, medidas correctivas inmediatas, medidas correctivas definitivas, y debe
poder exportarse como "expediente para la ACE" en cualquier momento. El software debe advertir al
usuario que esta obligacion de documentar puede aplicar aunque el usuario decida no notificar (por
considerar que no hubo riesgo), y dejar esa decision de "hubo riesgo / no hubo riesgo" registrada con su
justificacion, como parte de la evidencia.
**Fuente oficial:** `ace_decreto_144.txt`, lineas 819-825. Fecha de consulta: 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

### 2.9 Excepciones a la obligacion de notificar

**Hallazgo:** Tras revisar el texto integro del Art. 25 y del resto del Titulo II de la LPDP en el
corpus local, **no se encontro ninguna excepcion expresa** a la obligacion de notificar una vulneracion
dentro de las 72 horas (a diferencia de, por ejemplo, el consentimiento, que si tiene un catalogo de
excepciones en el Art. 28). La ley tampoco distingue por tamaño de empresa, sector, o volumen de datos
afectados: el deber de notificar nace, en el texto, de la sola existencia de una "vulneracion de
seguridad de datos personales", sin condicionarlo a un umbral de gravedad para notificar a la ACE y la
FGR (el unico lugar donde la ley sí introduce un filtro de gravedad es en el deber de documentar,
limitado a vulneraciones "que ocasionen un riesgo": ver 2.8).
**Norma:** LPDP
**Articulo:** 25 (ausencia de excepcion) en contraste con Art. 28 (excepciones al consentimiento, que si
existen)
**A quien aplica:** Al responsable del tratamiento.
**Implicacion para el software:** El producto no debe ofrecer una opcion de "esta vulneracion esta
exenta de notificacion" basada en criterios propios (tamaño, tipo de dato, etc.) sin una base legal
citada; solo debe ayudar al usuario a evaluar y documentar si el hecho constituye o no una "vulneracion
de seguridad" en el sentido del primer inciso del Art. 25 (ver 2.2), que es la unica puerta de entrada o
salida que el texto reconoce.
**Fuente oficial:** `ace_decreto_144.txt`, articulos 25 y 28 completos. Fecha de consulta: 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** HECHO (ausencia de excepcion expresa en el texto revisado) — confirmar con abogado
que no exista una excepcion en normativa secundaria de la ACE aun no revisada en este sweep.

---

## 3. Canal oficial de notificacion

### 3.1 Canal hacia la ACE

**Hallazgo (fuente web, no normativa):** La pagina oficial `https://ace.gob.sv/page/formularios` lista
un catalogo de "Formularios y Servicios" que incluye, entre otros: Acceso a Datos Personales, Derecho al
Olvido, Derecho de Oposicion, Derecho de Portabilidad, Nombramiento de Delegado, Rectificacion de Datos,
Cancelacion o Supresion, Limitacion del Tratamiento, **Reporte de Incidentes**, y Consulta Tecnica. De
estos, los tramites ARCO-POL y el nombramiento de delegado si tienen formularios PDF descargables
propios (confirmado tambien en el corpus local: `ace_form_acceso.txt`, `ace_form_cancelacion.txt`,
`ace_form_portabilidad.txt`, `ace_form_nombramiento_delegado.txt`, `ace_form_limitacion.txt`,
`ace_form_olvido.txt`, `ace_form_oposicion.txt`, `ace_form_rectificacion.txt`).

"Reporte de Incidentes" es distinto: **no tiene formulario descargable**. El texto literal de esa
tarjeta de servicio, obtenido de la pagina el 2026-09-24, es:

> Titulo: "Reporte de Incidentes"
> Descripcion: "¿Detectaste una amenaza o ataque? Reportalo inmediatamente para recibir asistencia
> especializada."
> Elementos: "Respuesta inmediata", "Confidencial", "Disponible 24/7"
> Boton: "Reportar Ahora" -> redirige a la pagina `/contacto`
> Tiempo estimado indicado en la tarjeta: "3 min"

Es decir, el "reporte de incidentes" en la ACE **no es un tramite formal con formulario propio y numero
de expediente visible al usuario**, sino una derivacion al canal de contacto general.

**Canal de contacto general (`https://ace.gob.sv/contacto` o `/page/contacto`), segun la misma consulta
web:**
- Telefono: **(503) 7530-6114** (confirmado, coincide con el numero citado en la tarea).
- Correo electronico de contacto general (la pagina distingue conceptualmente contacto general, soporte
  tecnico con respuesta en 24-48 horas, y un canal de "emergencias ciberneticas" disponible 24/7, pero
  las direcciones de correo exactas no pudieron extraerse de forma fiable con las herramientas de esta
  sesion: se recomienda verificarlas visitando la pagina directamente o por telefono antes de
  publicarlas en el producto).
- Horario: lunes a viernes, 8:00 a 16:00; con un canal de emergencias disponible 24/7.
- Ubicacion: San Salvador.

**Norma:** No es una norma sino un hecho operativo del sitio web oficial de la ACE.
**Articulo:** No aplica (dato de canal, no de ley).
**Obligacion:** El responsable debe notificar "a la Agencia de Ciberseguridad del Estado" (Art. 25
LPDP); la ley no especifica el medio, por lo que el medio disponible hoy es el canal de contacto general
de la ACE (telefono, correo, o el formulario web de contacto), no un formulario o plataforma dedicada de
reporte de incidentes.
**A quien aplica:** Al responsable del tratamiento que deba notificar una vulneracion.
**Implicacion para el software:** El producto no puede prometer una integracion API o un envio
automatizado con acuse formal hacia la ACE, porque ese canal formal no existe hoy publicamente. Lo que
si puede hacer es: (1) generar el documento de notificacion con el contenido minimo exacto del Art. 25
(seccion 2.5), listo para enviarlo por correo o presentarlo por el canal de contacto; (2) registrar
como evidencia la fecha, hora y medio por el cual se envio, y guardar copia del envio (captura de
pantalla del formulario de contacto, copia del correo enviado, o nota de la llamada telefonica con
nombre de quien atendio, si aplica); (3) advertir al usuario que debe verificar el canal vigente en
ace.gob.sv al momento de notificar, porque el canal es un dato operativo del sitio web de la ACE y puede
cambiar sin que cambie la ley.
**Fuente oficial:** https://ace.gob.sv/page/formularios y https://ace.gob.sv/contacto (o
/page/contacto). Fecha de consulta: 2026-09-24.
**Vigencia:** Dato operativo vigente a la fecha de consulta; sujeto a cambios por parte de la ACE sin
previo aviso al publico. Confianza: media (contenido obtenido mediante lectura automatizada de la
pagina web, no mediante verificacion humana directa ni fuente normativa).
**Clasificacion:** HECHO (dato operativo, no obligacion legal en si mismo).

### 3.2 Canal hacia la Fiscalia General de la Republica (FGR)

**Hallazgo (fuente web secundaria/institucional):** La FGR no tiene, segun la busqueda realizada, un
formulario en linea especifico para "denuncia de vulneracion de datos personales" como tramite separado.
El mecanismo general para poner en conocimiento de la FGR un hecho con apariencia delictiva (que es, en
sustancia, lo que exige notificar el Art. 25 LPDP: "y a la Fiscalia General de la Republica") es la
denuncia o aviso, que segun fuentes institucionales y de prensa puede presentarse: (a) de forma verbal o
escrita, personalmente o por medio de apoderado, en cualquier sede de la FGR; (b) ante la Policia
Nacional Civil (particularmente su unidad de delitos informaticos); o (c) ante un Juzgado de Paz. La LPDP
no dice cual de estas vias usar especificamente para el aviso del Art. 25 ni si el "aviso" a la FGR bajo
el Art. 25 LPDP debe tramitarse formalmente como una denuncia penal o si basta una comunicacion
administrativa informativa: este es un punto de incertidumbre real (ver seccion 8).
**Norma:** LPDP Art. 25 (obligacion de notificar a la FGR); canal segun practica institucional de la FGR
(fuente secundaria, no un articulo especifico de la LPDP).
**A quien aplica:** Al responsable del tratamiento.
**Implicacion para el software:** El producto debe ofrecer al usuario una guia clara de que la
notificacion a la FGR bajo el Art. 25 LPDP no tiene, por ahora, un canal digital dedicado identificado,
y sugerir contactar directamente a la FGR (sede mas cercana o unidad de delitos informaticos de la
PNC) para confirmar el procedimiento correcto en cada caso, dejando este punto explicitamente como
"pendiente de confirmar con la FGR o con abogado" en la plantilla de notificacion.
**Fuente oficial:** https://www.fiscalia.gob.sv/ (pagina institucional general); nota de prensa de
referencia: La Prensa Grafica, "La agresion digital: como denunciar..."
(https://www.laprensagrafica.com/elsalvador/La-agresion-digital-como-denunciar-y-protegernos-virtualmente-de-este-delito-en-El-Salvador-20230303-0061.html).
Fecha de consulta: 2026-09-24.
**Vigencia:** Dato operativo, confianza media-baja (fuente de prensa, no un procedimiento oficial
publicado por la FGR especificamente para el Art. 25 LPDP).
**Clasificacion:** HECHO / INCERTIDUMBRE (ver seccion 8).

---

## 4. Ley de Ciberseguridad y Seguridad de la Informacion (Decreto 143): aplicabilidad al sector privado

### 4.1 Ambito de aplicacion: por que la mayoria de empresas privadas NO son "sujetos obligados"

**Norma:** Ley de Ciberseguridad y Seguridad de la Informacion, Decreto Legislativo N. 143.
**Articulo:** 1 (objeto) y 2 (ambito de aplicacion)
**Texto literal:**
> **Art. 1.-** La presente ley tiene como objeto establecer los principios, el marco legal, la
> institucionalidad, los lineamientos, asi como las politicas de proteccion que permitan estructurar,
> regular, auditar y fiscalizar las medidas de ciberseguridad y seguridad de la informacion **en poder
> de las instituciones publicas**.
>
> **Art. 2.-** Estan obligados al cumplimiento de esta ley los organos del Gobierno, sus dependencias,
> las instituciones oficiales autonomas, las autoridades municipales o cualquier otra entidad u
> organismo, independientemente de su forma, naturaleza o situacion juridica, mediante las cuales se
> administren recursos publicos, bienes del Estado, ejecuten actos de la administracion publica en
> general **o que posean incidencia en las infraestructuras criticas de la nacion.**

**Obligacion:** El Decreto 143 aplica, por su propio texto, al sector publico y a cualquier entidad
(publica o privada) que "posea incidencia en las infraestructuras criticas de la nacion". La calificacion
formal de quien es "operador de infraestructura critica" no la decide la empresa unilateralmente: la
otorga la ACE mediante resolucion fundada, sometida a ratificacion del Presidente de la Republica (Art.
8 lit. f y g: "Calificar, mediante resolucion fundada, a los operadores de infraestructuras criticas... /
Retirar la calificacion..."). Es decir, una empresa privada solo queda sujeta al Decreto 143 si la ACE la
ha calificado formalmente como operador de infraestructura critica (tipicamente: banca, telecomunicaciones,
energia, agua, salud, y sectores equivalentes con impacto en servicios esenciales, aunque la ley no
publica en este corpus un listado cerrado de sectores).

**A quien aplica:** Sector publico siempre; sector privado solo si fue calificado como operador de
infraestructura critica por la ACE.
**Implicacion para el software:** El producto PRIV-SV, orientado a empresas privadas en general, debe
tratar el Decreto 143 como **CONDICIONAL**: solo relevante si el cliente confirma que ha sido calificado
(o es razonablemente candidato a ser calificado) como operador de infraestructura critica. Para la gran
mayoria de clientes tipicos (comercio, servicios, tecnologia sin infraestructura critica), el regimen
aplicable en materia de incidentes es unicamente la LPDP (Art. 25), no el Decreto 143. El producto debe
incluir una pregunta de onboarding ("es su empresa un operador de infraestructura critica calificado por
la ACE, o presta servicios esenciales segun la definicion del Art. 4 lit. g del Decreto 143?") para
activar o no el modulo de Ciberseguridad.
**Fuente oficial:** `asamblea_decreto_143_ciberseguridad.txt`, lineas 68-90 (Art. 1-2) y linea 368-372
(Art. 8 lit. f-g). Fecha de consulta: 2026-09-23.
**Vigencia:** VIGENTE (Decreto 143 fue publicado junto con la LPDP en el mismo Diario Oficial del 15 de
noviembre de 2024; verificar fecha exacta de vigencia propia del Decreto 143 si difiere de la LPDP, no
confirmada en este sweep).
**Clasificacion:** CONDICIONAL (aplica solo si la empresa es o pudiera ser operador de infraestructura
critica calificado por la ACE).

### 4.2 Obligaciones de reporte de incidentes para los sujetos obligados del Decreto 143

**Norma:** Decreto 143
**Articulo:** 6 (obligaciones), literales f, g y h
**Texto literal relevante:**
> f) Aplicar y cumplir de manera inmediata y eficaz las medidas necesarias para prevenir, reportar y
> resolver las amenazas de ciberseguridad y seguridad de la informacion, de conformidad con las
> disposiciones juridicas establecidas al respecto.
>
> g) Adoptar de forma oportuna, expedita y eficiente las acciones necesarias para reducir el impacto y
> la propagacion de un incidente de ciberseguridad o seguridad de la informacion.
>
> h) Remitir en el tiempo, forma y especificidad los informes relacionados con la ciberseguridad y
> seguridad de la informacion que le sean exigidos por la autoridad competente.
>
> l) Informar a los potenciales afectados, en la medida que puedan identificarse y cuando asi lo
> determine la Agencia de Ciberseguridad del Estado, sobre la ocurrencia de incidentes que pudieran
> comprometer o comprometan gravemente su informacion... Esta obligacion de informar debera cumplirse a
> traves de los medios o mecanismos que determine la referida autoridad.

**Hallazgo clave:** El Decreto 143 **no fija un numero de horas** (como si hace la LPDP con sus 72
horas) para que el sujeto obligado reporte un incidente a la ACE. Usa estandares abiertos: "de manera
inmediata y eficaz" (f), "de forma oportuna, expedita y eficiente" (g), "en el tiempo, forma y
especificidad" que exija la autoridad (h). El deber de informar a los "potenciales afectados" (l) ademas
queda condicionado a que la ACE "asi lo determine" y a que use "los medios o mecanismos que determine la
referida autoridad": no es un deber automatico de la empresa como si lo es, sin condicion, el de la LPDP
hacia los titulares.

**El unico "72 horas" que aparece en el Decreto 143** corre a cargo de la ACE, no del sujeto obligado:

> **Art. 8 lit. v)** Dar aviso a la Fiscalia General de la Republica en un plazo maximo de setenta y dos
> horas, cuando en el ejercicio de sus facultades o con ocasion de ellas, advierta que existen elementos
> que pudieren configurar algun delito de los contemplados en la Ley Especial contra los Delitos
> Informaticos y Conexos u otras leyes penales.

Esto es una obligacion de la propia ACE hacia la FGR cuando la ACE, investigando, detecta indicios de
delito informatico; no es una obligacion del sujeto obligado privado.

**A quien aplica:** Sujetos obligados del Decreto 143 (ver 4.1): sector publico y operadores de
infraestructura critica calificados.
**Implicacion para el software:** Para los clientes a los que si aplique el Decreto 143 (casos
condicionales), el producto debe ofrecer un modulo separado de "reporte a la ACE bajo la Ley de
Ciberseguridad" con un estandar de urgencia ("inmediato") en lugar de un cronometro fijo de 72 horas, y
dejar explicito que este reporte es adicional (no sustituye) al reporte de 72 horas del Art. 25 LPDP
cuando el incidente tambien involucre datos personales (ver 4.3).
**Fuente oficial:** `asamblea_decreto_143_ciberseguridad.txt`, lineas 265-278 (Art. 6, lit. f-h y l) y
linea 445-448 (Art. 8, lit. v). Fecha de consulta: 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO para los sujetos obligados del Decreto 143 (condicional a la calificacion
de infraestructura critica en el caso del sector privado); sin plazo numerico fijo, a diferencia de la
LPDP.

### 4.3 Doble notificacion: LPDP y Decreto 143 no son excluyentes

**Analisis:** Cuando una empresa privada SI es un operador de infraestructura critica calificado por la
ACE (ver 4.1) y sufre un incidente que ademas involucra datos personales, no existe en el texto revisado
ninguna clausula que diga que notificar bajo un regimen exime de notificar bajo el otro. Son dos leyes
con objetos distintos: la LPDP protege datos personales (Art. 25: notificacion a ACE, FGR y titulares
sobre la vulneracion de datos personales especificamente); el Decreto 143 protege la ciberseguridad y
continuidad de infraestructuras criticas y sistemas en general (Art. 6: reporte de amenazas/incidentes
de ciberseguridad a la ACE, de forma inmediata). Ademas, el propio Art. 53 LPDP remite al Decreto 143
solo para "el desarrollo del procedimiento" sancionador y "las reglas de prescripcion" de las
infracciones de la LPDP, no para sustituir el deber sustantivo de notificacion del Art. 25.
**Conclusion (analisis propio, no cita textual de una norma que lo diga expresamente):** una empresa
privada que sea operador de infraestructura critica calificado y sufra una vulneracion de datos
personales por un incidente de ciberseguridad debe, en principio, cumplir **ambos** regimenes: notificar
a ACE/FGR/titulares dentro de 72 horas conforme al Art. 25 LPDP, y ademas reportar el incidente de
ciberseguridad a la ACE de forma inmediata conforme al Art. 6 del Decreto 143 (y a las disposiciones que
la ACE haya emitido para dicho reporte). Esta conclusion es razonable a partir del texto pero no esta
dicha en ningun articulo de forma expresa: se marca como incertidumbre que un abogado deberia confirmar,
especialmente en cuanto a si en la practica la ACE unifica ambos reportes en una sola gestion cuando el
mismo sujeto le reporta.
**Clasificacion:** CONDICIONAL / INCERTIDUMBRE (ver seccion 8).

---

## 5. Reforma a la Ley Especial contra los Delitos Informaticos y Conexos (vigente desde julio 2025)

**Aviso de fuente:** El corpus local no incluye el texto de esta reforma ni el texto completo vigente de
la Ley Especial contra los Delitos Informaticos y Conexos (Decreto 260, 2016, con sus reformas). Los PDF
oficiales de la Asamblea Legislativa y de la FGR consultados en esta sesion no pudieron leerse de forma
fiable con las herramientas disponibles (aparecieron como contenido binario/comprimido no legible). Por
lo tanto, todo lo que sigue en esta seccion proviene de fuentes secundarias (nota de Lexology, notas de
prensa institucional de la Asamblea Legislativa, y una base de datos juridica de terceros -vLex- con
posible desfase en la numeracion de articulos) y debe tratarse con **confianza media a baja**, marcado
expresamente como tal.

### 5.1 Identificacion de la reforma

**Norma:** Reforma a la Ley Especial contra los Delitos Informaticos y Conexos.
**Articulo:** No aplica un solo articulo; ver 5.2 y 5.3.
**Obligacion:** Segun fuente secundaria, la reforma fue aprobada por la Asamblea Legislativa el 19 de
junio de 2025 mediante Decreto Legislativo N. 332, publicada en el Diario Oficial el 25 de junio de 2025,
vigente desde el 3 de julio de 2025. Esta fecha de vigencia coincide con lo señalado en la tarea ("vigente
desde julio 2025").
**A quien aplica:** Sujetos que puedan incurrir en los tipos penales de la ley (personas naturales y, por
extension, hechos cometidos en el contexto de operaciones de empresas); y, tras la reforma, tambien
otorga a las empresas que custodian/controlan/procesan datos un rol procesal nuevo (ver 5.3).
**Implicacion para el software:** Bajo reserva de confirmacion con el texto oficial, el producto puede
mencionar esta reforma en el modulo educativo/informativo sobre el marco legal aplicable a incidentes,
pero no debe construir logica de plazos o formularios sobre ella hasta verificar el texto oficial
completo.
**Fuente oficial:** Nota de prensa de la Asamblea Legislativa
(https://www.asamblea.gob.sv/node/13595, https://www.asamblea.gob.sv/node/13592) y analisis de firma
legal (Lexology, resultado de busqueda, URL no accedida directamente por bloqueo HTTP 403:
https://www.lexology.com/library/detail.aspx?g=a1188143-72f2-47a2-9c1d-df5098a8ecee). Fecha de consulta:
2026-09-24.
**Vigencia:** Segun fuente secundaria, VIGENTE desde el 3 de julio de 2025. Confianza: media (no se pudo
leer el texto oficial completo del decreto ni confirmar el numero exacto 332 contra el propio PDF del
decreto, que resulto binariamente ilegible con las herramientas de esta sesion).
**Clasificacion:** HECHO (existencia y fecha de la reforma) con confianza media.

### 5.2 Contenido principal de la reforma (segun fuente secundaria)

- Se agregan nuevas definiciones al Art. 3 de la ley: **dueño de datos, custodia de datos, controlador,
  procesador y metadatos**. Esto acerca el vocabulario penal al vocabulario de proteccion de datos
  (LPDP) y de ciberseguridad, aunque no se pudo confirmar el texto literal exacto de cada definicion.
- Se modifica el articulo sobre **fraude informatico** (identificado por la fuente secundaria como el
  Art. 11, aunque otra fuente lo identifica como Art. 10 bajo el nombre "estafa informatica": existe
  contradiccion entre fuentes secundarias sobre el numero exacto, ver seccion 8): se agregan como
  conductas punibles la "configuracion" de manipulaciones del sistema y la "insercion" de instrucciones
  falsas o fraudulentas, se agrega un agravante cuando el delito lo comete alguien que por su trabajo
  conoce, opera o administra los sistemas de datos, y se **aumenta la pena de 6-10 años a 10-12 años de
  prision** cuando el fraude afecta sistemas bancarios o financieros.
- Se reconoce a las entidades que **custodian, controlan o procesan datos personales** como sujetos
  **directamente afectados** en casos de fraude informatico, lo que les permite ejercer accion penal
  (presentar querella) contra quienes cometan el delito. Antes de la reforma, segun la misma fuente, esta
  legitimacion aparentemente no estaba tan clara para las entidades custodias/procesadoras (solo para el
  titular del patrimonio afectado).
**Norma:** Reforma a la Ley Especial contra los Delitos Informaticos y Conexos (Decreto 332, segun fuente
secundaria).
**A quien aplica:** Empresas que sufren fraude informatico sobre datos que custodian, controlan o
procesan (esto incluye tipicamente a las empresas clientes de PRIV-SV que procesan datos personales de
terceros).
**Implicacion para el software:** Si se confirma el texto, esto es relevante para el modulo de
"decision de notificar" y "medidas legales" del ciclo de vida del incidente (seccion 7): una empresa
victima de fraude informatico sobre datos que custodia podria, tras esta reforma, tener legitimacion
propia para presentar una denuncia/querella penal, no solo un aviso informativo. Este es un punto que el
producto deberia comunicar solo como informacion general ("consulte con su abogado sobre su legitimacion
para actuar penalmente"), nunca como asesoria legal definitiva.
**Fuente oficial:** Nota de prensa Asamblea Legislativa (URLs citadas en 5.1); resumen de fuente
secundaria (Lexology, via busqueda). Fecha de consulta: 2026-09-24.
**Vigencia:** Segun fuente secundaria, VIGENTE desde el 3 de julio de 2025.
**Clasificacion:** HECHO, confianza media-baja (no verificado contra texto oficial completo).

### 5.3 Esta reforma no crea un deber de reporte de incidentes

**Hallazgo negativo (importante):** Ninguna de las fuentes secundarias consultadas (nota de prensa
institucional ni resumenes de firmas) menciona que la reforma de 2025 a la Ley Especial contra los
Delitos Informaticos y Conexos cree una obligacion de reportar incidentes a una autoridad. Su contenido,
segun lo revisado, es de naturaleza **penal sustantiva** (nuevos tipos/agravantes, nuevas penas) y
**procesal** (legitimacion para querellarse), no de naturaleza administrativa de reporte. El deber de
reporte de incidentes en el ordenamiento salvadoreño sigue estando, segun lo revisado en este sweep,
unicamente en el Art. 25 LPDP (para datos personales) y en el Art. 6 del Decreto 143 (para
ciberseguridad, limitado a sujetos obligados de esa ley).
**Clasificacion:** HECHO (ausencia de deber de reporte en esta reforma, segun fuentes secundarias
disponibles) — confirmar contra el texto oficial completo del decreto cuando se consiga una copia
legible.

### 5.4 Tipos penales relevantes para empresas (ley base, no la reforma): confianza baja, pendiente de verificacion

La tarea pide identificar "tipos penales relevantes para empresas (acceso indebido, divulgacion, etc.)".
No se pudo leer el texto oficial completo de la Ley Especial contra los Delitos Informaticos y Conexos
en esta sesion (los tres PDF oficiales/institucionales intentados —Asamblea, FGR, y el espejo de
UNODC/Sherloc— resultaron ilegibles o bloqueados con las herramientas disponibles). La siguiente tabla
resume lo que arrojaron fuentes terciarias (una base de datos juridica privada, vLex, y resumenes de
busqueda sobre el espejo de UNODC) y debe tratarse como **orientativa unicamente**, con **confianza
baja** en la numeracion exacta de articulos:

| Delito (nombre orientativo) | Articulo segun fuente consultada | Pena orientativa segun fuente consultada |
|---|---|---|
| Acceso indebido a sistemas informaticos | Art. 4 (segun vLex) | Prision de 1 a 4 años |
| Acceso indebido a programas o datos informaticos | Art. 5 (segun vLex) | Prision de 2 a 4 años |
| Daños a sistemas informaticos | Art. 7 (segun vLex) | Prision de 3 a 6 años (agravado 4-7 si afecta sistemas publicos o financieros) |
| Estafa informatica / fraude informatico | Art. 10 u 11 segun la fuente (contradiccion entre fuentes) | 6-10 años originalmente; 10-12 años tras la reforma 2025 en el supuesto agravado |
| Interceptacion de datos informaticos (espionaje informatico) | Art. 12 (segun vLex) | Prision de 5 a 8 años (6-10 si pone en peligro la seguridad del Estado) |
| Hurto por medios informaticos | Art. 13 (segun vLex) | Prision de 5 a 8 años (otra fuente cita 2-6 años mas multa) |
| Revelacion indebida de datos o informacion de caracter personal | Art. 26 (segun vLex) | Prision de 3 a 5 años (4-8 con animo de lucro) |

**Norma:** Ley Especial contra los Delitos Informaticos y Conexos (Decreto 260, 2016) con la reforma de
2025.
**A quien aplica:** Personas naturales (incluyendo empleados, exempleados, terceros) que cometan estas
conductas contra sistemas o datos de una empresa, o cuyos sistemas sean usados para cometerlas.
**Implicacion para el software:** Estos tipos penales son relevantes para el modulo de "clasificacion
del incidente" (¿el incidente parece configurar ademas un delito?) y para justificar por que la LPDP
exige notificar tambien a la FGR: muchas vulneraciones de datos personales (acceso no autorizado,
filtracion, robo de informacion) coinciden con alguno de estos tipos penales. El producto debe presentar
esta tabla como orientativa y no citar numeros de articulo especificos al usuario final hasta que se
verifique el texto oficial; puede, en cambio, listar los **nombres** de las conductas tipificadas (sin
numero de articulo) como ayuda de clasificacion.
**Fuente oficial:** vLex El Salvador (https://sv.vlex.com/vid/ley-especial-delitos-informaticos-644825729,
fuente terciaria/base de datos juridica privada) y resumen de busqueda sobre espejo de UNODC/Sherloc
(https://sherloc.unodc.org/cld/en/legislation/slv/ley_especial_contra_los_delitos_informaticos_y_conexos_decreto_no._260/,
acceso directo bloqueado con HTTP 403, informacion obtenida solo via resumen de resultados de busqueda).
Fecha de consulta: 2026-09-24.
**Vigencia:** Texto base VIGENTE desde 2016 con reformas (incluida la de 2025); numeracion de articulos
sin confirmar contra el Diario Oficial.
**Clasificacion:** INCERTIDUMBRE (confianza baja en la numeracion exacta) — requiere obtener el texto
oficial legible (Diario Oficial o PDF no protegido) y validacion de un abogado penalista antes de usarse
como referencia normativa en el producto.

---

## 6. Infracciones y multas asociadas a la falta de notificacion

### 6.1 Clasificacion de la infraccion

**Norma:** LPDP
**Articulo:** 56, literal a), numeral 3
**Texto literal:**
> a) Son consideradas infracciones leves, las siguientes: [...] 3. Omitir notificar respecto de las
> vulneraciones a la seguridad de los datos personales acaecidas a los sujetos pertinentes, de
> conformidad con lo dispuesto en el articulo 25 de la presente ley.

**Obligacion:** Incumplir el deber de notificacion del Art. 25 (omitirlo) esta clasificado por la propia
LPDP como infraccion **leve**, no grave ni muy grave.
**A quien aplica:** Al responsable del tratamiento.
**Implicacion para el software:** Es un hallazgo relevante para el diseño de riesgo del producto: la
sancion administrativa directa por no notificar una vulneracion es, en terminos comparativos dentro de la
misma ley, la categoria mas baja de infraccion (ver el catalogo completo de infracciones graves y muy
graves en el contexto compartido del proyecto, punto 3). Esto no significa que el riesgo real para la
empresa sea bajo: una vulneracion de datos personales puede generar, ademas de esta sancion leve por "no
notificar", dano reputacional, responsabilidad civil, eventual responsabilidad penal de terceros
(seccion 5), y si el mismo hecho revela ademas otras infracciones a la LPDP (p. ej. tratamiento sin
consentimiento, transferencias irregulares), esas otras conductas pueden calificar como graves o muy
graves por si mismas, de forma independiente a la sancion por "omitir notificar". El producto debe
comunicar esto con cuidado: el riesgo de sancion por Art. 25 en si es leve, pero el incidente subyacente
puede implicar riesgos mucho mayores que el software debe seguir ayudando a gestionar.
**Fuente oficial:** `ace_decreto_144.txt`, lineas 1375-1391. Fecha de consulta: 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (la clasificacion de la infraccion es un hecho normativo, no una
recomendacion).

### 6.2 Multa aplicable

**Norma:** LPDP
**Articulo:** 57, literal a)
**Texto literal:** "Las infracciones leves se sancionaran con multa de uno hasta un maximo de diez
salarios minimos mensuales vigentes del sector comercio."
**Calculo orientativo (fuente secundaria para el monto del salario minimo, no de la LPDP):** con el
salario minimo mensual del sector comercio, industria y servicios vigente en 2026 (USD 408.80/mes segun
Decreto Ejecutivo N. 11 del MTPS, con incremento del 12% desde el 1 de junio de 2025, segun fuentes
secundarias), la multa por omitir notificar una vulneracion oscilaria entre **USD 408.80 y USD 4,088.00**
por infraccion. Este calculo es aritmetica propia sobre un dato de salario minimo obtenido por fuente
secundaria (no del Diario Oficial directamente en esta sesion): confianza media.
**A quien aplica:** Al responsable del tratamiento sancionado.
**Implicacion para el software:** Util para dashboards de riesgo/exposicion economica del cliente, mostrando
siempre la referencia "salario minimo mensual del sector comercio vigente" en vez de un monto fijo en
dolares, para que el calculo se actualice si cambia el salario minimo.
**Fuente oficial:** `ace_decreto_144.txt`, lineas 1470-1480 (Art. 57); monto del salario minimo: fuentes
secundarias consultadas el 2026-09-24 (multiples portales coinciden en USD 408.80/mes desde junio 2025;
no se accedio al Decreto Ejecutivo del MTPS directamente en esta sesion). Fecha de consulta: 2026-09-24.
**Vigencia:** VIGENTE (multa); salario minimo vigente segun fuente secundaria, confirmar contra Decreto
del MTPS si se usara como dato oficial en el producto.
**Clasificacion:** OBLIGATORIO (el rango de la multa en salarios minimos, segun texto de la LPDP);
confianza media unicamente en la conversion a dolares.

### 6.3 Medidas adicionales

**Norma:** LPDP
**Articulo:** 58
**Obligacion:** Ademas de la multa, "determinada la procedencia de la sancion, la Agencia podra ordenar
al infractor... que adopte las medidas que fueren necesarias para restablecer la legalidad alterada por
la infraccion". Las sanciones de la LPDP "no eximen al infractor de las responsabilidades civiles o
penales derivadas de las investigaciones correspondientes".
**A quien aplica:** Al responsable sancionado.
**Implicacion para el software:** El producto debe dejar claro que una sancion administrativa leve por
Art. 56 no cierra el caso: pueden venir medidas correctivas ordenadas por la ACE, ademas de procesos
civiles o penales independientes derivados del mismo hecho.
**Fuente oficial:** `ace_decreto_144.txt`, lineas 1495-1502. Fecha de consulta: 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

---

## 7. Evidencia que la empresa debe conservar para demostrar cumplimiento

Esta seccion combina el texto expreso del Art. 25 (documentacion obligatoria, ver 2.8), la regla general
de carga de la prueba del Art. 54 LPDP, y las reglas generales de prueba de la Normativa para el
Procedimiento Administrativo Sancionador de la ACE.

**Norma:** LPDP, Art. 25 (ultimo inciso) y Art. 54; Normativa para el Procedimiento Administrativo
Sancionador de la ACE (normativa_sancionadora_OCR.txt).
**Articulo:** 25 y 54 LPDP; Art. 7-10 y reglas de prueba de la normativa sancionadora (numeracion propia
de esa normativa, sujeta a errores de OCR: verificar contra imagenes en
`fuentes\ocr\normativa_sancionadora\` si se usa en detalle).
**Obligacion / recomendacion combinada:**
1. **OBLIGATORIO por texto expreso (Art. 25):** conservar el expediente de documentacion de la
   vulneracion con, como minimo: fecha en que ocurrio, motivo, hechos relacionados, efectos e
   implicaciones, medidas correctivas inmediatas y medidas correctivas definitivas.
2. **RECOMENDADO (no dicho expresamente para incidentes, mejor practica derivada de Art. 54 y de la
   logica de carga de la prueba de la LPDP):** dado que el Art. 54 LPDP pone la carga de la prueba sobre
   el responsable para demostrar el consentimiento y la comunicacion del aviso de privacidad, y que la
   normativa sancionadora de la ACE reconoce como prueba "los instrumentos publicos, los autenticos, los
   instrumentos privados" y similares, es razonable esperar que, ante un procedimiento sancionador por
   presunto incumplimiento del Art. 25, la ACE exija al responsable probar que si notifico a tiempo y con
   el contenido correcto. Por prudencia, ademas del expediente minimo del punto 1, la empresa deberia
   conservar:
   - Registro con fecha y hora exacta del momento en que se considero que hubo "conocimiento" de la
     vulneracion (ver criterio operativo de la seccion 2.3), y quien tomo esa determinacion.
   - Copia integra de cada notificacion enviada (a ACE, a FGR, a cada titular o al mensaje masivo usado),
     con fecha y hora de envio.
   - Evidencia del envio y, si existe, del acuse de recibo (captura del formulario de contacto enviado,
     copia del correo con confirmacion de entrega, nota de la llamada telefonica con nombre de quien
     atendio en la ACE, acuse de recepcion de la FGR).
   - Bitacora tecnica del incidente (logs, hallazgos forenses, alcance de datos y titulares afectados).
   - Evidencia de que se inicio la revision exhaustiva dentro de las 72 horas (fecha de apertura del caso
     de revision).
   - Version de las politicas de seguridad antes y despues del incidente, con fecha del cambio (evidencia
     de la actualizacion de politicas exigida por el mismo Art. 25).
   - Si se decidio NO notificar por considerar que no hubo "vulneracion" en el sentido del Art. 25 o que
     no "ocasiono un riesgo" (para efectos de la obligacion de documentar), dejar registrada esa decision
     y su justificacion, con fecha, para poder sustentarla despues ante la ACE si se cuestiona.
**A quien aplica:** Al responsable del tratamiento.
**Implicacion para el software:** Este es, en esencia, el diseño funcional del modulo de "expediente de
incidente" de PRIV-SV: cada campo de esta lista deberia ser un campo estructurado del expediente, con
control de version y con marca de tiempo inmutable (o casi inmutable) para que sirva como evidencia
confiable.
**Fuente oficial:** `ace_decreto_144.txt` Art. 25 (lineas 819-825) y Art. 54 (lineas 1354-1360);
`normativa_sancionadora_OCR.txt`, seccion "DE LA PRUEBA" (lineas 316-346, con posibles errores de OCR:
confirmar contra `fuentes\ocr\normativa_sancionadora\page-NN.png` si se cita textualmente en otro
entregable). Fecha de consulta: 2026-09-23.
**Vigencia:** VIGENTE (LPDP); Normativa sancionadora vigente desde el 19 de agosto de 2026 segun el
contexto compartido del proyecto.
**Clasificacion:** OBLIGATORIO (punto 1, expediente minimo del Art. 25) + RECOMENDADO (el resto de la
lista, buena practica evidencial derivada mas no impuesta articulo por articulo).

---

## 8. Ciclo de vida del incidente: que exige la ley y que es buena practica

El siguiente mapeo distingue en cada etapa lo que el marco legal salvadoreño revisado exige de forma
expresa, frente a lo que es buena practica de la industria (se cita ISO 27035 y NIST SP 800-61
unicamente como referencias de buena practica ampliamente usadas en gestion de incidentes de seguridad
de la informacion, no como fuente de obligacion legal en El Salvador).

```
DETECCION       CONOCIMIENTO      TRIAGE          CONTENCION        EVALUACION DE
(senal/alerta)  (art. 25:         (clasificar y   (detener/limitar  RIESGO
                dispara el        confirmar       el dano)          (que datos,
                reloj de 72h)     alcance inicial)                  cuantos titulares,
     |               |                 |                |            que riesgo)
     v               v                 v                v                v
  [buena          [LEY: aqui       [buena          [buena          [LEY: sirve de
  practica]       nace el plazo    practica]       practica]       base a la decision
                  de 72h; LEY                                      de si "ocasiona
                  no dice como                                     riesgo" (art. 25,
                  se determina]                                    doc. obligatoria)]


DECISION DE          NOTIFICACIONES          REMEDIACION           CIERRE Y
NOTIFICAR             (dentro de 72h          (medidas             LECCIONES
(LEY: sin             desde el                correctivas          APRENDIDAS
excepcion             conocimiento;           definitivas;         (buena practica;
expresa hallada       LEY fija contenido      actualizar           LEY exige la
para Art. 25;         minimo distinto         politicas de         actualizacion de
CONDICIONAL           para ACE/FGR y          seguridad -          politicas como
si aplica ademas      para titulares)         art. 25 LPDP;        parte de la
Decreto 143)          -> ACE (sin canal       reportar a           revision
     |                dedicado, ver           Ciberseguridad       exhaustiva)
     v                seccion 3)              si aplica el
[LEY: decision        -> FGR (canal           Decreto 143)
no delegable al       de denuncia penal            |
software; LEY         general, ver                 v
no da excepciones     seccion 3)              [LEY + buena
expresas]             -> Titulares                 practica]
     |                (contenido
     v                reducido, art. 25)
[LEY: 72 horas             |
desde el                   v
conocimiento]        [LEY: 72 horas
                      desde el
                      conocimiento;
                      documentacion
                      obligatoria del
                      incidente que
                      ocasione riesgo]
```

**Norma:** LPDP Art. 25 (para las etapas de conocimiento, decision de notificar, notificaciones,
documentacion y actualizacion de politicas); Decreto 143 Art. 6 (para la etapa de reporte de
ciberseguridad, solo si aplica, ver seccion 4).
**Obligacion por etapa (resumen):**
- **Deteccion:** sin exigencia legal especifica de como detectar; es enteramente buena practica
  (monitoreo, alertas, canal de reporte interno).
- **Conocimiento:** etapa juridicamente critica porque dispara el plazo de 72 horas (Art. 25); la ley no
  define el criterio, ver seccion 2.3.
- **Triage / evaluacion de riesgo:** sin plazo propio en la ley; debe completarse a tiempo para poder
  cumplir el contenido minimo de las notificaciones (que exige ya conocer "la naturaleza del incidente" y
  "los datos comprometidos") dentro de las 72 horas, y para decidir si el incidente "ocasiona un riesgo"
  a efectos del deber de documentar (Art. 25, ultimo inciso).
- **Contencion / remediacion inmediata:** el Art. 25 exige que la notificacion a la ACE incluya "las
  acciones correctivas generales realizadas de forma inmediata" (literal c), por lo que alguna contencion
  debe haber ocurrido, o al menos iniciado, antes de notificar.
- **Decision de notificar:** no delegable al software; no se hallo excepcion legal expresa a la
  obligacion de notificar (seccion 2.9), por lo que el criterio por defecto del producto debe ser "toda
  vulneracion de datos personales se notifica salvo que el usuario, con su propio criterio o el de su
  abogado, documente por que un hecho concreto no encaja en absoluto en la definicion del primer inciso
  del Art. 25".
- **Notificaciones:** plazo de 72 horas, contenido minimo por destinatario (seccion 2.5), canal ACE sin
  formulario dedicado (seccion 3.1), canal FGR via denuncia/aviso general (seccion 3.2), y —si aplica el
  Decreto 143— reporte adicional a la ACE bajo ese regimen (seccion 4).
- **Remediacion definitiva y actualizacion de politicas:** exigida por el Art. 25, segundo inciso, dentro
  del mismo proceso de revision exhaustiva iniciado en las 72 horas (aunque puede concluir despues).
- **Cierre:** exige, como minimo, que el expediente de documentacion (seccion 2.8 y seccion 7) quede
  completo y disponible para la ACE.
- **Lecciones aprendidas:** no exigida expresamente por la LPDP como etapa separada; se solapa con la
  "actualizacion de politicas de seguridad" que si es obligatoria. El resto (retrospectivas formales,
  metricas de tiempo de respuesta, etc.) es buena practica de la industria (ISO 27035, NIST SP 800-61),
  no un mandato legal salvadoreño encontrado en este sweep.
**A quien aplica:** Al responsable del tratamiento.
**Implicacion para el software:** Este mapeo es, en esencia, el esqueleto del modulo de gestion de
incidentes de PRIV-SV: cada etapa con exigencia legal debe marcarse visualmente distinta de las etapas de
buena practica, y el cronometro de 72 horas debe anclarse expresamente a la etapa de "Conocimiento", no a
"Deteccion" ni a "Cierre".
**Fuente oficial:** Elaboracion propia a partir de LPDP Art. 25 (`ace_decreto_144.txt`, lineas 791-825) y
Decreto 143 Art. 6 (`asamblea_decreto_143_ciberseguridad.txt`, lineas 265-278). Las referencias a ISO
27035 y NIST SP 800-61 son de conocimiento general de la industria, citadas solo como buena practica, no
verificadas contra un documento especifico en esta sesion. Fecha de consulta: 2026-09-23 / 2026-09-24.
**Vigencia:** VIGENTE.
**Clasificacion:** Mixta, ver el detalle por etapa arriba (OBLIGATORIO para las etapas de conocimiento,
notificaciones, documentacion y actualizacion de politicas; RECOMENDADO para deteccion, triage detallado,
cierre formal y lecciones aprendidas).

---

## 9. Incertidumbres y puntos que requieren abogado

1. **Computo de las 72 horas (corridas u habiles):** no resuelto por el texto de la LPDP; existe un
   argumento serio en ambos sentidos usando la LPA como supletoria (seccion 2.4). Se necesita opinion de
   un abogado administrativista salvadoreño, e idealmente un criterio publicado o informal de la propia
   ACE, antes de fijar esto como regla del producto. Recomendacion interina: usar horas corridas por
   defecto (mas protector) y mostrar tambien el limite si se contara en horas habiles.
2. **Definicion operativa de "conocimiento":** la ley no lo define. El criterio de "conviccion razonable
   por parte de una persona con capacidad de decision" propuesto en la seccion 2.3 es una construccion
   del equipo de producto, no un texto legal, y debe validarse con abogado antes de presentarse al
   usuario final como si fuera la interpretacion oficial.
3. **Contenido minimo de la notificacion a la FGR:** el Art. 25 detalla el contenido minimo "a la Entidad
   Rectora" (ACE) y, por separado, a los titulares, pero no detalla expresamente el contenido para la
   FGR. Se asumio por interpretacion razonable que debe ser, al menos, el mismo que el de la ACE (seccion
   2.5), pero esto no es un texto literal y debe confirmarse.
4. **Canal formal de notificacion a la FGR bajo el Art. 25 LPDP:** no se identifico un procedimiento
   especifico de la FGR pensado para esta notificacion (distinto de una denuncia penal general). Falta
   confirmar con la propia FGR si existe un canal administrativo mas liviano para este aviso especifico
   de la LPDP, o si en la practica se tramita siempre como denuncia penal formal.
5. **Doble notificacion LPDP + Decreto 143:** se concluyo por analisis propio (seccion 4.3) que ambos
   regimenes aplican de forma acumulativa cuando corresponde, pero ningun articulo lo dice de forma
   expresa. Falta confirmar si en la practica la ACE coordina o unifica ambos reportes cuando el mismo
   sujeto obligado le reporta bajo las dos leyes.
6. **Numeracion exacta de los tipos penales de la Ley Especial contra los Delitos Informaticos y
   Conexos** (acceso indebido, daños, interceptacion, hurto, revelacion indebida, fraude/estafa
   informatica): las fuentes secundarias consultadas (vLex, resumenes sobre el espejo de UNODC) se
   contradicen parcialmente entre si en la numeracion (por ejemplo, si el fraude informatico es el Art.
   10 o el Art. 11). No se pudo leer el texto oficial completo en esta sesion. Requiere obtener una copia
   legible del Diario Oficial o del decreto original y validacion de un abogado penalista.
7. **Contenido exacto del Decreto 332 (reforma 2025 a la Ley de Delitos Informaticos):** toda la seccion
   5 de este informe se basa en fuentes secundarias (nota de prensa institucional y resumenes de firma
   legal); no se confirmo el texto oficial linea por linea. Requiere el texto oficial del Diario Oficial
   del 25 de junio de 2025 (segun la fecha reportada) para citarlo con precision.
8. **Estado de publicacion del Decreto 659 (reforma de septiembre 2026):** al 24 de septiembre de 2026,
   segun las fuentes secundarias consultadas (incluyendo un articulo de opinion que cita la propia pagina
   de decretos de la Asamblea), la publicacion material en el Diario Oficial seguia sin confirmarse.
   Mantener como APROBADA-PENDIENTE-PUBLICACION hasta verificar directamente en diariooficial.gob.sv. Las
   fuentes secundarias revisadas en esta sesion coinciden en que esta reforma no modifica el Art. 25, pero
   esto tampoco esta confirmado contra el texto oficial del decreto.
9. **Fecha exacta de vigencia propia del Decreto 143** (si difuere de la vigencia de la LPDP, publicada
   en el mismo Diario Oficial del 15 de noviembre de 2024): no se verifico especificamente el articulo de
   vigencia del Decreto 143 en esta sesion (si se confirmo el de la LPDP, Art. 64). Revisar el propio
   texto del Decreto 143 para su articulo de vigencia.
10. **Direcciones de correo electronico exactas de la ACE** para contacto general, soporte tecnico y
    emergencias ciberneticas: no se lograron extraer con confianza alta desde la pagina web en esta
    sesion; verificar visitando directamente ace.gob.sv/contacto antes de publicarlas en el producto.
11. **Umbral entre "vulneracion" (que siempre se notifica, sin excepcion hallada) y "vulneracion que
    ocasiona un riesgo" (que ademas debe documentarse formalmente):** el texto usa dos estandares
    distintos en el mismo articulo (ver seccion 2.8) y no aclara si toda vulneracion notificada
    automaticamente "ocasiona un riesgo" a efectos de la documentacion, o si podrian existir
    vulneraciones notificadas que el propio responsable considere de riesgo tan bajo que no ameriten el
    expediente de documentacion completo. Confirmar con abogado antes de que el producto ofrezca esa
    distincion como opcion al usuario.

---

## 10. Fuentes consultadas

**Corpus local (fecha de consulta: 2026-09-23):**
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt` (LPDP, texto integro, Art. 25 en
  lineas 791-825, Art. 26-28 en lineas 828 y siguientes, Art. 53-59 en lineas 1342-1420, Art. 60-64 al
  final).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\diario_oficial_2024-11-15_mh.txt` (Diario Oficial que
  contiene el Decreto 143 y el Decreto 144, no revisado linea por linea en este sweep salvo para
  contrastar el ambito de aplicacion del Decreto 143).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\asamblea_decreto_143_ciberseguridad.txt` (texto integro
  de la Ley de Ciberseguridad y Seguridad de la Informacion, Art. 1-26 revisados en detalle).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\asamblea_decreto_856_lpa.txt` (Ley de Procedimientos
  Administrativos, Art. 80-84 sobre terminos y plazos).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_politicas_protecciondatos.txt` (Politicas de
  Actuacion ACE N. 001-0309025-DPDP, seccion de notificacion de brechas de seguridad).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\lineamientos_dpo_OCR.txt` (Lineamientos para el Delegado
  de Proteccion de Datos, OCR, revisado para menciones de gestion de incidentes).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\normativa_sancionadora_OCR.txt` (Normativa para el
  Procedimiento Administrativo Sancionador de la ACE, OCR, revisado para reglas de prueba y diligencias
  preliminares por incidentes).
- `C:\Proyects\PRIV-SV\analisis\00_contexto_para_agentes.md` (contexto compartido del proyecto, hechos ya
  verificados).

**Fuentes web oficiales o institucionales (fecha de consulta: 2026-09-24 salvo que se indique otra):**
- https://ace.gob.sv/page/formularios (catalogo de formularios y servicios, seccion "Reporte de
  Incidentes").
- https://ace.gob.sv/contacto (canal de contacto general de la ACE).
- https://www.asamblea.gob.sv/node/13592 y https://www.asamblea.gob.sv/node/13595 (notas de prensa de la
  Asamblea Legislativa sobre la reforma 2025 a la Ley Especial contra los Delitos Informaticos y
  Conexos).
- https://www.asamblea.gob.sv/node/14116 (nota de prensa de la Asamblea Legislativa sobre la reforma de
  septiembre de 2026 a la LPDP).
- https://www.fiscalia.gob.sv/ (portal institucional general de la FGR, para el canal de denuncia).

**Fuentes secundarias (prensa y firmas legales, marcadas explicitamente como tal en el cuerpo del
informe; fecha de consulta: 2026-09-24):**
- Lexology, "Reformas A La Ley Contra Delitos Informaticos..."
  (https://www.lexology.com/library/detail.aspx?g=a1188143-72f2-47a2-9c1d-df5098a8ecee) — resumen
  obtenido via busqueda, el acceso directo a la pagina devolvio HTTP 403.
- vLex El Salvador (https://sv.vlex.com/vid/ley-especial-delitos-informaticos-644825729) — base de datos
  juridica privada, fuente terciaria.
- Espejo de UNODC/Sherloc para el Decreto 260 de El Salvador
  (https://sherloc.unodc.org/cld/en/legislation/slv/ley_especial_contra_los_delitos_informaticos_y_conexos_decreto_no._260/)
  — acceso directo bloqueado con HTTP 403; informacion obtenida solo via resumen de resultados de
  busqueda.
- El Diario de Hoy, "Se elimina el delegado de las empresas, pero no la responsabilidad de proteger los
  datos de las personas"
  (https://www.eldiariodehoy.com/opinion/se-elimina-el-delegado-de-las-empresas-pero-no-la-responsabilidad-de-proteger-los-datos-de-las-personas/93642/2026/).
- Infobae, "El Salvador: La Asamblea Legislativa elimina la obligacion del delegado de proteccion de
  datos para las empresas" (referenciado via busqueda, no accedido directamente).
- La Prensa Grafica, "La agresion digital: como denunciar y protegernos virtualmente de este delito en El
  Salvador"
  (https://www.laprensagrafica.com/elsalvador/La-agresion-digital-como-denunciar-y-protegernos-virtualmente-de-este-delito-en-El-Salvador-20230303-0061.html).
- Multiples portales de asesoria laboral/contable coincidentes en el monto del salario minimo del sector
  comercio 2026 (USD 408.80/mes): utilizados solo para el calculo orientativo de la seccion 6.2, no como
  fuente normativa.

**Nota sobre limitaciones tecnicas de esta sesion:** varios documentos oficiales en PDF (el decreto de
reforma a la Ley Especial contra los Delitos Informaticos y Conexos en el sitio de la Asamblea, el texto
de dicha ley en el portal de transparencia de la FGR) no pudieron leerse de forma fiable con las
herramientas de extraccion de texto disponibles en esta sesion (se recibieron como contenido
binario/comprimido no legible). Esto explica por que la seccion 5 de este informe se apoya en fuentes
secundarias y terciarias en lugar de en el texto primario, y por que esos puntos se marcaron con
confianza media o baja. Se recomienda, en una siguiente iteracion, intentar obtener estos textos en un
formato de PDF con texto extraible (no escaneado/protegido) para elevar la confianza de la seccion 5.
