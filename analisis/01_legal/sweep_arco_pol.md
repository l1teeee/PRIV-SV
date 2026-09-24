# Sweep juridico - Derechos ARCO-POL: contenido, procedimiento, plazos y formularios

Proyecto: PRIV-SV. Lente asignado: Derechos ARCO-POL.
Fecha de consulta de todas las fuentes: 2026-09-23, salvo las fuentes marcadas expresamente como consultadas el 2026-09-24 (verificacion complementaria de una ejecucion posterior).
Norma base: Ley para la Proteccion de Datos Personales (LPDP), Decreto Legislativo N. 144, D.O. N. 219, Tomo 445, 15 nov 2024, vigente desde el 23 nov 2024.

Convenciones: "Art." remite a la LPDP salvo que se indique otra norma. "Lineamientos" = Lineamientos para el Delegado de Proteccion de Datos Personales (ACE, D.O. 11 ago 2026, vigentes 19 ago 2026). "Normativa sancionadora" = Normativa para el Desarrollo del Procedimiento Administrativo Sancionador en el Ambito de la LPDP (ACE, D.O. 11 ago 2026, vigente 19 ago 2026). "Politicas ACE" = Politicas N. 001-0309025-DPDP. "Reforma 659" = Decreto Legislativo N. 659 aprobado el 17 sep 2026, publicacion en D.O. no confirmada al 23 sep 2026.

---

## 1. Resumen ejecutivo

1. La LPDP reconoce siete derechos "personalisimos e independientes" (Art. 4 lit. i): Acceso (Art. 8), Rectificacion (Art. 9), Cancelacion o supresion (Art. 10), Oposicion (Art. 12), Limitacion (Art. 13), Portabilidad (Art. 14) y Olvido (Art. 10 inciso final). El bloqueo (Art. 11) no es un derecho autonomo sino un efecto posible de la cancelacion, y el Art. 6 lo menciona junto con rectificacion y cancelacion.
2. El procedimiento (Arts. 18 a 23) es unico para todos los derechos: solicitud con siete requisitos (Art. 18), prevencion por una sola vez con 10 dias habiles para subsanar y archivo si no se subsana (Art. 18), devolucion por incompetencia en 5 dias habiles (Art. 19), respuesta en 20 dias habiles prorrogables por causas justificadas hasta otros 20 (Art. 20; Art. 9 para rectificacion), notificacion a receptores de la rectificacion, actualizacion o eliminacion en 5 dias habiles desde que se determina la procedencia (Art. 21), denegatoria total o parcial por resolucion motivada notificada en 3 dias habiles desde la decision, por el mismo medio senalado por el titular y con las pruebas (Art. 22), y gratuidad con cobro solo de reproduccion, certificacion o envio a costo, publicado previamente (Art. 23).
3. Los Lineamientos de la ACE (vigentes desde el 19 ago 2026) anaden reglas operativas que el software debe recoger: uso de los formularios oficiales como estandar minimo y obligacion de aceptarlos (Art. 32), obligacion de resolver toda solicitud mediante resolucion documentada (admision, prevencion, subsanacion, reconocimiento, incompetencia, denegatoria o resolucion final) notificada en 3 dias habiles desde su emision (Art. 33), prorroga motivada y notificada en 3 dias habiles dentro del plazo ordinario (Art. 34), causales de incompetencia (Art. 35), publicacion de costos (Art. 38) y un mecanismo de reclamo del titular ante la Direccion de Proteccion de Datos Personales de la ACE en 10 dias habiles desde la notificacion (Art. 33). Estos lineamientos estan redactados para el Delegado; su aplicacion a empresas privadas sin delegado tras la reforma 659 es una incertidumbre juridica que requiere abogado.
4. La ACE publica ocho formularios oficiales (version 07-07-2025): acceso, rectificacion, cancelacion o supresion, oposicion, limitacion, portabilidad, olvido y nombramiento de delegado. Los siete formularios ARCO-POL comparten estructura y campos; este informe extrae la lista completa de campos de cada uno (seccion 7) para que el software los replique. El documento de identidad que piden es la copia del DUI; para representacion piden poder; para ninez, partida de nacimiento o carne de minoridad; para fallecidos, partida de defuncion y documento de vinculo familiar.
5. No existe norma expresa sobre cuanto tiempo conservar el expediente de una solicitud ARCO-POL. Las referencias mas cercanas son: prescripcion de infracciones y sanciones en 5 anos (Normativa sancionadora Art. 47, con computo segun LPA Art. 149), conservacion minima de 10 anos de la documentacion del aviso de privacidad (Lineamientos Art. 31) y conservacion de 10 anos de libros y documentos del comerciante (Codigo de Comercio Art. 451, fuente secundaria). Se propone un criterio de retencion configurable con minimo de 5 anos desde el cierre y valor recomendado de 10 anos (seccion 9).
6. Las infracciones directamente asociadas son: no atender solicitudes ARCO-POL en tiempo y forma (grave, Art. 56 lit. b num. 2), denegar solicitudes en contravencion a la ley (muy grave, Art. 56 lit. c num. 2), exigir pago por lo que es gratuito (leve, Art. 56 lit. a num. 7) e informacion incompleta o inexacta al atender un acceso (grave, Art. 56 lit. b num. 1). Multas: 1 a 10, 11 a 25 y 26 a 40 salarios minimos mensuales del sector comercio (Art. 57).
7. La reforma 659 (segun fuentes secundarias y nota oficial de la Asamblea) deroga los Arts. 15 y 17, reforma el 16, el 47 y el 51, elimina el delegado obligatorio en el sector privado y hace que las solicitudes se presenten directamente al sujeto obligado, manteniendo todos los plazos. El texto oficial no esta disponible; al 23 sep 2026 no consta su publicacion en el Diario Oficial, por lo que la version vigente sigue siendo la del Decreto 144. El software debe modelar la figura "quien atiende ARCO-POL" como rol configurable (delegado o unidad responsable) y no como campo fijo "delegado".

---

## 2. Mapa normativo y jerarquia

| Nivel | Instrumento | Que aporta al lente ARCO-POL | Vigencia |
|---|---|---|---|
| Ley | LPDP, D.L. 144 | Derechos (Arts. 6 a 14), procedimiento (Arts. 15 a 23), NNA (Arts. 5 lit. j, 26, 42), revocacion (Arts. 29 a 31), procedimientos documentados (Art. 33), carga de la prueba (Art. 54), infracciones (Arts. 56 a 59), LPA supletoria (Art. 62) | VIGENTE |
| Ley (reforma) | D.L. 659, 17 sep 2026 | Deroga Arts. 15 y 17, reforma 16, 47 y 51; solicitudes directas al sujeto obligado; plazos sin cambio (segun fuentes secundarias) | APROBADA-PENDIENTE-PUBLICACION |
| Ley supletoria | Ley de Procedimientos Administrativos (LPA) | Computo de plazos en dias habiles (Art. 82), representacion (Arts. 67 y 69), prescripcion (Art. 149). Texto tomado de transcripcion secundaria | VIGENTE (texto no verificado en fuente primaria) |
| Normativa ACE | Normativa sancionadora, D.O. 11 ago 2026 | Denuncia del titular (Arts. 8, 15 y 16), medios de prueba (Art. 24), parametros de multa (Art. 43), prescripcion 5 anos (Art. 47) | VIGENTE desde 19 ago 2026 |
| Lineamiento ACE | Lineamientos para el Delegado, D.O. 11 ago 2026 | Formularios (Art. 32), resolucion y documentacion (Art. 33), plazos y prorroga (Art. 34), incompetencia (Art. 35), costos (Art. 38), informes semestrales con estadisticas ARCO-POL (Art. 30), conservacion 10 anos del aviso (Art. 31) | VIGENTE desde 19 ago 2026; aplicabilidad a privados sin delegado incierta tras reforma 659 |
| Politica de actuacion ACE | Politicas N. 001-0309025-DPDP | Mecanismos de denuncia para titulares (Art. 5 lit. c), digitalizacion con sistemas que documenten el tratamiento (Art. 4, medidas tecnicas lit. g) | Fecha de emision y publicacion pendiente de verificar |
| Formularios ACE | 8 formularios version 07-07-2025 | Campos y documentos de identidad y representacion | Publicados en ace.gob.sv/page/formularios |

---

## 3. Los derechos, uno por uno

### 3.1 Derecho general y legitimacion (Art. 6)

Transcripcion (ace_decreto_144.txt, pagina 6):

"Art. 6.- Toda persona, por si mismo o por medio de su representante con facultades especiales, tendra derecho a conocer si sus datos personales estan siendo procesados para garantizar la proteccion de los mismos, cuando sea procedente podra solicitar la rectificacion, cancelacion o bloqueo de estos; a oponerse al tratamiento de sus datos; y, a solicitar que se limite su tratamiento en el futuro para usos distintos a los consentidos. Asimismo, tendran derecho a obtener una reproduccion inteligible de sus datos personales y a transferirlos cuando asi lo consideren pertinente. Tratandose de los datos personales de personas fallecidas, le correspondera a sus herederos o sucesores ejercer los derechos correspondientes, debiendo acreditar con documentacion que demuestre su calidad de heredero o sucesor."

Puntos clave:
- Legitimados: el titular (persona natural, Art. 4 lit. s) por si mismo; su representante "con facultades especiales"; herederos o sucesores del titular fallecido, acreditando esa calidad con documentacion.
- La ley no define "facultades especiales". En derecho salvadoreno la expresion remite a un poder que mencione expresamente la facultad (poder especial), lo cual excede un poder general administrativo. Requiere confirmacion de abogado (ver seccion 14).

**Norma:** LPDP
**Articulo:** Art. 6
**Obligacion:** Atender solicitudes presentadas por el titular, por su representante con facultades especiales o, si el titular fallecio, por herederos o sucesores que acrediten su calidad.
**A quien aplica:** Responsable del tratamiento (toda persona natural o juridica, publica o privada, Art. 2).
**Implicacion para el software:** El formulario de solicitud debe tener un campo "quien solicita" con tres valores (titular, representante, heredero o sucesor) y exigir los adjuntos correspondientes a cada uno (ver seccion 7). Debe existir un estado "acreditacion pendiente" que dispare la prevencion del Art. 18.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (pagina 6), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 3.2 Acceso (Art. 8)

Transcripcion (ace_decreto_144.txt, pagina 7):

"Art. 8.- El titular de datos personales tendra derecho a obtener toda la informacion que sobre si mismo se encuentre en bases de datos o registros fisicos. Este derecho de acceso sera ejercido en forma gratuita conforme a lo establecido en la presente ley.
La informacion personal a la cual se concedera acceso debera ser suministrada:
a) En forma clara y exenta de codificaciones, la cual debera ser acompanada de una explicacion de los terminos que se utilicen, los sujetos que han consultado dicha informacion y con que proposito.
b) De manera completa, siempre y cuando la misma no haya sido objeto de seudonimizacion o disociacion, en cuyo caso se dejara constancia de dichas circunstancias. En ningun caso el informe podra revelar datos pertenecientes a terceros, aun cuando se vinculen con el titular.
Esta informacion podra obtenerse mediante la mera consulta de su titular o su representante, previa identificacion de su identidad y de los datos que por medio de su visualizacion pretende conocer, o tambien se podra obtener con la indicacion de los datos que son objeto de tratamiento por medios electronicos o por cualquier otro medio que la tecnologia permita y cuyo contenido sea legible e inteligible; esto sin utilizar claves o codigos que requieran el uso de dispositivos mecanicos especificos, imagenes o cualquier otro medio usado para dicho proposito.
Adicionalmente, se debe comunicar si se ha realizado un intercambio de su informacion personal con otras instituciones o entidades."

Contenido minimo de la respuesta de acceso (lo que el software debe ayudar a compilar):

| Elemento | Base |
|---|---|
| Toda la informacion sobre el titular en bases de datos o registros fisicos | Art. 8 inc. 1 |
| Forma clara, sin codificaciones, con explicacion de los terminos usados | Art. 8 lit. a |
| Sujetos que han consultado la informacion y con que proposito | Art. 8 lit. a |
| Informacion completa; si hubo seudonimizacion o disociacion, dejar constancia | Art. 8 lit. b |
| Nunca revelar datos de terceros, aunque se vinculen con el titular | Art. 8 lit. b |
| Comunicar si hubo intercambio de la informacion con otras instituciones o entidades | Art. 8 inc. final |
| Modalidad de reproduccion elegida por el titular, salvo imposibilidad fisica o juridica fundada | Art. 18 inc. 2 |
| Cumplimiento mediante copias simples, certificadas, consulta directa, documentos electronicos o medio analogo | Art. 21 inc. 1 |
| Gratuito; solo costos de reproduccion, certificacion o envio | Arts. 8 y 23 |

Nota sobre la "mera consulta" (Art. 8 inc. 3): la ley admite el acceso por consulta directa, previa identificacion, sin necesidad de un tramite escrito. El formulario oficial de acceso incluye "Consulta directa" como modalidad. El software debe poder registrar accesos por consulta directa como expediente simplificado con evidencia de la identificacion.

**Norma:** LPDP
**Articulo:** Art. 8
**Obligacion:** Entregar al titular toda su informacion, en forma clara y completa, con explicacion de terminos, indicando quienes consultaron la informacion y con que proposito, dejando constancia de seudonimizacion o disociacion, sin revelar datos de terceros e informando si hubo intercambio con otras entidades.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** La respuesta de acceso necesita insumos que el resto del sistema debe generar de forma continua: (1) inventario de bases y sistemas donde hay datos del titular (Registro de Actividades de Tratamiento), (2) bitacora de consultas por usuario y proposito, (3) registro de transferencias e intercambios con terceros, (4) marcador de datos seudonimizados o disociados. Sin bitacora de consultas no es posible cumplir el Art. 8 lit. a. Debe existir una plantilla de "informe de acceso" con estas secciones y un control de "datos de terceros excluidos".
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (pagina 7), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

Infraccion asociada: proporcionar de forma incompleta o inexacta la informacion al ejercer el acceso es infraccion grave (Art. 56 lit. b num. 1).

### 3.3 Rectificacion (Art. 9)

Transcripcion (ace_decreto_144.txt, paginas 7 y 8):

"Art. 9.- El titular tendra derecho a solicitar al responsable la rectificacion o correccion de sus datos personales, cuando estos sean inexactos, incompletos o no se encuentren actualizados. Ademas, el titular podra solicitar la rectificacion y actualizacion de sus datos personales, en el caso de que estos hayan sido sometidos a tratamiento en inobservancia de las disposiciones de la presente ley.
El titular debera ofrecer la documentacion que acredite que es procedente la rectificacion de sus datos personales o podra informar la ubicacion en la cual se encuentra almacenada o registrada la misma.
El responsable del tratamiento debera cumplir con lo solicitado por el titular o su representante de manera gratuita, y resolver en el sentido que corresponda en el plazo de veinte dias habiles, contados a partir de la recepcion de la solicitud. El incumplimiento de esta obligacion dentro del plazo determinado habilitara al interesado para presentar la denuncia correspondiente ante la Entidad Rectora a efecto de que se garanticen sus derechos.
Durante el proceso de verificacion para rectificar la informacion de los datos personales, el responsable del banco de datos, base de datos, repositorio o de los sistemas o registros, tanto manuales como informaticos, bloqueara aquellos que se esten analizando para su rectificacion, dando a conocer que se encuentra en revision o actualizacion, segun lo solicitado."

Causales: datos inexactos, incompletos, desactualizados, o tratados en inobservancia de la ley. Requisito del titular: documentacion que acredite la procedencia o indicacion de donde esta almacenada. Plazo: 20 dias habiles desde la recepcion. Efecto durante la verificacion: bloqueo de los datos en analisis con leyenda "en revision o actualizacion". Via ante incumplimiento: denuncia ante la ACE (inciso tercero segun la numeracion de parrafos del texto ACE; la tarea lo cita como inciso 2).

**Norma:** LPDP
**Articulo:** Art. 9
**Obligacion:** Resolver la rectificacion en 20 dias habiles desde la recepcion, gratuitamente, y bloquear los datos en analisis indicando que estan en revision o actualizacion.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** El expediente de rectificacion debe: (1) registrar la documentacion aportada o la ubicacion indicada por el titular; (2) generar una tarea de "bloqueo con leyenda" hacia los sistemas donde estan los datos, con evidencia de ejecucion y fecha; (3) contar 20 dias habiles desde la recepcion; (4) al cerrar, generar la tarea de notificacion a receptores (Art. 21). El Art. 21 inc. 2 exige ademas dejar constancia de que la informacion esta en proceso de rectificacion si un tercero pide acceso.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (paginas 7 y 8), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 3.4 Cancelacion o supresion (Art. 10)

Causales de procedencia (Art. 10 inc. 1, "al menos uno de los siguientes casos"):
- a) Los datos ya no son necesarios para los fines del tratamiento.
- b) El titular retira su consentimiento, cuando este fue la base de licitud y no existe otra.
- c) El titular se opone al tratamiento y no prevalecen otros motivos legitimos para el almacenamiento.
- d) Los datos fueron obtenidos o tratados ilicitamente.
- e) Deben suprimirse para cumplir una obligacion legal del responsable.
- f) Datos obtenidos en relacion con oferta de servicios de la sociedad de la informacion, en caso de oferta directa a ninos.
- g) Datos obtenidos en relacion con la oferta de servicios de instituciones publicas o privadas.

Causales de improcedencia (Art. 10 inc. 2, "no procedera"):
- a) Cuando causen perjuicio a derechos o intereses legitimos de terceros, siempre que exista resolucion judicial u orden administrativa de conservar los datos.
- b) Si contraviene una obligacion legal.
- c) Cuando sean necesarios para la libertad de expresion, informacion y prensa (los datos deben cumplir el principio de exactitud).
- d) Cuando los datos hayan sido objeto de disociacion.
- e) Fines de investigacion cientifica, historica o estadisticos, si los datos han sido seudonimizados o disociados.
- f) Fines de archivo en interes publico; o para la formulacion, ejercicio o defensa de reclamaciones.

Estandar temporal: "sin dilaciones indebidas" (Art. 10 inc. 1), dentro del plazo general de 20 dias habiles (Art. 20).

Observacion: el formulario oficial de cancelacion lista solo seis causales mas "Otro"; omite la causal g) del texto legal. El software debe incluir las siete causales legales y la opcion "Otro".

**Norma:** LPDP
**Articulo:** Art. 10 incisos 1 y 2
**Obligacion:** Eliminar los datos sin dilaciones indebidas cuando concurra una causal de procedencia y no concurra una de improcedencia; en caso de improcedencia, denegar motivadamente (Art. 22).
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Lista de verificacion en dos pasos: causal invocada (a-g) y prueba de improcedencia (a-f). El sistema debe pedir al analista que documente que reviso las causales de improcedencia, en particular obligaciones legales de conservacion (tributarias, laborales, mercantiles) y reclamaciones en curso. Debe soportar el resultado "bloqueo en vez de supresion" (Art. 11) y "negativa parcial" (Art. 22 inc. 2).
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (paginas 8 y 9), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 3.5 Olvido (Art. 10 inciso final)

Transcripcion (ace_decreto_144.txt, pagina 9):

"El titular tambien podra ejercer el derecho al olvido de sus datos personales, cuando estos hayan sido publicados en el entorno electronico, debiendo el responsable informar a otros responsables del tratamiento de dichos datos personales para que estos sean suprimidos de los enlaces, copias o replicas que los contengan. Este derecho incluye ademas el de solicitar que se eliminen de los motores de busqueda en Internet las listas de resultados que se obtuvieran al realizar una busqueda a partir de los datos personales del titular de los enlaces publicados que contuvieran informacion relativa al mismo, cuando estos sean inadecuados, inexactos, no pertinentes, no actualizados o excesivos o hubieren devenido como tales por el transcurso del tiempo, teniendo en cuenta los fines para los que se recogieron o trataron, el tiempo transcurrido, la naturaleza e interes publico de dicha informacion."

Elementos: (1) supuesto de hecho: datos publicados en entorno electronico; (2) obligacion del responsable: suprimir e informar a otros responsables para que supriman enlaces, copias o replicas; (3) frente a motores de busqueda: eliminar listas de resultados obtenidas a partir del nombre u otros datos del titular; (4) criterios de ponderacion: inadecuados, inexactos, no pertinentes, no actualizados, excesivos, o devenidos tales por el tiempo, considerando fines, tiempo transcurrido, naturaleza e interes publico. El formulario oficial de olvido recoge tres motivos (inexacta o incorrecta; desactualizada o no pertinente; ha dejado de ser relevante con el paso del tiempo) mas "Otro".

**Norma:** LPDP
**Articulo:** Art. 10 inciso final
**Obligacion:** Ante solicitud de olvido procedente, suprimir la publicacion e informar a los otros responsables que tengan enlaces, copias o replicas para que los supriman.
**A quien aplica:** Responsable que publico los datos en entorno electronico.
**Implicacion para el software:** El expediente de olvido necesita: inventario de publicaciones (URL, plataforma, fecha), lista de terceros a los que se comunico la supresion (con fecha y evidencia), y campo de ponderacion de interes publico. La obligacion de informar a otros responsables se conecta con el plazo de 5 dias habiles del Art. 21 inc. 3 (comunicacion a quienes recibieron los datos).
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (pagina 9), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (solo si el responsable publico los datos en entorno electronico)

### 3.6 Bloqueo (Art. 11)

Transcripcion (ace_decreto_144.txt, pagina 9):

"Art. 11.- El derecho de supresion o cancelacion de datos personales podra dar lugar al bloqueo de dichos datos, conservandose unicamente estos a disposicion de la Administracion Publica, Jueces y Tribunales en el ejercicio estricto de sus funciones, para la atencion de las posibles responsabilidades nacidas del tratamiento, en los plazos establecidos para el resguardo segun las leyes aplicables."

Definicion legal de bloqueo: "restriccion temporal o permanente de cualquier acceso o tratamiento de los datos almacenados" (Art. 4 lit. c). El bloqueo aparece en tres contextos: como efecto de la cancelacion (Art. 11), como medida cautelar durante la rectificacion (Art. 9 inc. final) y como facultad general (Art. 6). No es un derecho con formulario propio.

**Norma:** LPDP
**Articulo:** Art. 11 y Art. 4 lit. c
**Obligacion:** Cuando la supresion se sustituya por bloqueo, restringir todo acceso o tratamiento y conservar los datos solo a disposicion de autoridades, durante los plazos de resguardo de las leyes aplicables.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Estado "bloqueado" a nivel de registro o categoria de dato, con motivo (cancelacion con deber de conservacion, rectificacion en curso), fecha de inicio, fecha estimada de fin (segun plazo legal de resguardo configurado) y bitacora de accesos excepcionales (solo autoridad). El sistema orienta pero no ejecuta el bloqueo en los sistemas del cliente; genera la tarea y guarda la evidencia.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (paginas 3 y 9), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (cuando procede la cancelacion pero existe deber de conservacion, o durante una rectificacion)

### 3.7 Oposicion (Art. 12)

Transcripcion (ace_decreto_144.txt, pagina 9):

"Art. 12.- Es el derecho del interesado a solicitar el cese en el tratamiento de sus datos personales, incluida la elaboracion de perfiles o clasificaciones con fines comerciales o de mercadotecnia directa. No obstante, el derecho de oposicion no podra ejercerse en los siguientes escenarios:
a) Cuando el tratamiento sea necesario para el cumplimiento de una mision realizada en interes publico o en el ejercicio de facultades conferidos al responsable.
b) Cuando el tratamiento sea necesario para la satisfaccion de intereses legitimos perseguidos por el responsable o por un tercero, siempre que sobre dichos intereses no prevalezcan los intereses o los derechos y libertades fundamentales del titular que requiera la proteccion de sus datos personales, en particular cuando el titular sea un nino o nina."

Efectos: cese del tratamiento (total o de la finalidad especifica, por ejemplo mercadotecnia directa). La oposicion procedente puede conducir a cancelacion (Art. 10 lit. c) o a limitacion mientras se pondera (Art. 13 lit. d). Mientras se verifica si prevalecen los motivos legitimos del responsable, el titular puede pedir limitacion.

**Norma:** LPDP
**Articulo:** Art. 12
**Obligacion:** Cesar el tratamiento objetado salvo que concurra interes publico o interes legitimo prevalente, ponderando con especial cuidado si el titular es nino o nina.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Para oposicion a mercadotecnia directa el sistema debe permitir registrar el cese como "lista de exclusion" con fecha y evidencia de aplicacion en los canales de marketing. Para otros motivos, plantilla de ponderacion de interes legitimo (motivos del responsable vs derechos del titular) que quede documentada en el expediente, con marcador de minoridad que eleve el estandar.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (pagina 9), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (la denegatoria es CONDICIONAL a los supuestos a y b)

### 3.8 Limitacion (Art. 13)

Supuestos (Art. 13 lit. a-d): a) el titular impugna la exactitud, durante el plazo de verificacion; b) el tratamiento es ilicito y el titular se opone a la supresion y pide limitacion en su lugar; c) el responsable ya no necesita los datos pero el titular los necesita para formular, ejercer o defender reclamaciones; d) el titular se opuso al tratamiento mientras se verifica si prevalecen los motivos legitimos del responsable. Efecto: "los efectos de la limitacion operaran mientras subsistan las razones que motivaron al titular" (Art. 13 inc. final). Definicion: Art. 4 lit. m (medidas para evitar la modificacion o, en su caso, el borrado o supresion).

**Norma:** LPDP
**Articulo:** Art. 13 y Art. 4 lit. m
**Obligacion:** Aplicar medidas que impidan la modificacion o supresion de los datos mientras subsista la causa invocada por el titular.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Estado "limitado" con causal (a-d), fecha de inicio, condicion de levantamiento y revision periodica; alerta cuando la causa desaparece (por ejemplo, se resolvio la verificacion de exactitud o la ponderacion de la oposicion). Debe vincularse con expedientes de rectificacion y oposicion en curso.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (paginas 9 y 10), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (procede solo en los cuatro supuestos legales)

### 3.9 Portabilidad (Art. 14)

Transcripcion (ace_decreto_144.txt, pagina 10):

"Art. 14.- Es el derecho del titular a recibir los datos personales que haya facilitado al responsable, en un formato estructurado, de uso comun, de lectura mecanica e interoperable, y el derecho a transmitirlos a otro responsable si este asi lo desea.
El ejercicio de este derecho exige dos requisitos: que el tratamiento este fundado en el consentimiento del titular y que dicho tratamiento sea efectuado por medios automatizados. Para facilitar este proceso, es necesario motivar la interoperabilidad entre los servicios.
Es obligacion de los responsables realizar con agilidad y sin costo para el titular, todos los tramites para la migracion de los datos de este a otro responsable del tratamiento, en un formato estructurado, de uso comun y facil lectura, cuando asi lo solicite legitimamente."

Requisitos de procedencia: base de licitud = consentimiento, y tratamiento automatizado. Alcance: datos "que haya facilitado al responsable". Efectos: entrega en formato estructurado, de uso comun, lectura mecanica e interoperable; y, si el titular lo pide, transmision directa a otro responsable, sin costo y con agilidad.

**Norma:** LPDP
**Articulo:** Art. 14
**Obligacion:** Entregar los datos facilitados por el titular en formato estructurado, de uso comun, lectura mecanica e interoperable, y realizar sin costo la migracion a otro responsable cuando se solicite, siempre que el tratamiento se base en consentimiento y sea automatizado.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** El expediente debe verificar los dos requisitos (base de licitud del tratamiento segun el Registro de Actividades de Tratamiento y caracter automatizado) antes de admitir, registrar el formato entregado y, si aplica, los datos del responsable destinatario (el formulario oficial tiene un bloque "Destinatario/a de los datos"). La migracion directa a otro responsable es una transferencia: el sistema debe dejar evidencia del consentimiento del titular para ella.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (pagina 10), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (consentimiento como base y tratamiento automatizado)

### 3.10 Derechos conexos que entran por el mismo canal

- Derecho de informacion en la recoleccion (Art. 7): incluye conocer al encargado (proveedores de nube o almacenamiento) y el contenido de los derechos ARCO-POL y mecanismos para ejercerlos (Art. 7 lit. d). Infraccion leve si se incumple (Art. 56 lit. a num. 8).
- Revocacion del consentimiento (Arts. 29 a 31): no es un derecho ARCO-POL pero llega por el mismo canal. Plazo de 5 dias habiles para proceder y 5 dias habiles para informar al encargado (Art. 30). Negativa: denuncia ante la ACE (Art. 31). Infracciones muy graves 9 y 10 (Art. 56 lit. c). La ACE debe elaborar modelos de formularios de revocacion (Art. 50 lit. q); al 23 sep 2026 la pagina de formularios de la ACE no lista un formulario de revocacion. El software debe ofrecer un formulario propio de revocacion con plazo de 5 dias habiles.
- Sector publico (Arts. 46 a 49): derechos recortados (cancelacion solo por obligacion legal; limitacion solo supuestos a, c y d). Fuera del alcance del producto, pero un cliente privado que actue como encargado de una entidad publica puede recibir solicitudes bajo ese regimen.

---

## 4. El procedimiento (Arts. 15 a 23)

### 4.1 Diagrama del flujo

```
[Titular / representante / heredero]
        |
        v
+-------------------------------+
| Presentacion de la solicitud  |  Art. 18: 7 requisitos (a-g); acceso: indicar modalidad
| (formulario ACE o propio)     |  Lineamientos Art. 32: aceptar siempre el formulario ACE
+-------------------------------+
        |
        v
+-------------------------------+     incompleta o falta info
| Verificacion de admision      |---------------------------------> PREVENCION (una sola vez)
| (identidad, representacion,   |                                    subsanar en 10 dias habiles
|  datos, derecho, firma)       |                                    desde el dia siguiente a la
+-------------------------------+                                    notificacion (Art. 18)
        |                                                                |
        | no competente / derecho ajeno a la ley                         | no subsana o subsana mal
        |------------------------------> DEVOLUCION + aviso al titular   v
        |                                en 5 dias habiles (Art. 19)   ARCHIVO sin mas tramite;
        v                                                              queda a salvo nueva solicitud
+-------------------------------+
| Analisis de fondo             |  Rectificacion: bloqueo con leyenda "en revision" (Art. 9)
| (causales, excepciones Art.22,|  Limitacion: aplicar mientras subsista la causa (Art. 13)
|  datos de terceros, encargados|
+-------------------------------+
        |
        | plazo 20 dias habiles (Arts. 9 y 20)
        | prorroga justificada hasta 20 mas (Art. 20); notificar prorroga en 3 dias
        | habiles y dentro del plazo ordinario (Lineamientos Art. 34)
        v
+---------------+   +------------------+   +----------------------------+
| PROCEDENTE    |   | PARCIAL          |   | DENEGATORIA                |
| resolucion +  |   | ejecutar solo lo |   | resolucion motivada, con   |
| fecha de      |   | procedente       |   | pruebas, notificada en 3   |
| efectividad   |   | (Art. 22 inc. 2) |   | dias habiles por el medio  |
| (Lin. Art.33) |   |                  |   | senalado (Art. 22 inc. 3)  |
+---------------+   +------------------+   +----------------------------+
        |                    |
        v                    v
+-------------------------------------------+
| Ejecucion y entrega                        |  Art. 21: copias simples, certificadas, consulta
| + notificacion a receptores/terceros en    |  directa, documentos electronicos u otro medio
|   5 dias habiles desde la procedencia      |  Costos: solo reproduccion, certificacion, envio
|   (Art. 21 inc. 3)                          |  a precio de materiales, publicados (Art. 23)
+-------------------------------------------+
        |
        v
[Cierre del expediente y conservacion como evidencia]
        |
        | titular inconforme
        v
[Reclamo ante Direccion de Proteccion de Datos de la ACE en 10 dias habiles
 (Lineamientos Art. 33) / Denuncia ante la ACE (Arts. 9 y 31; Normativa
 sancionadora Arts. 8, 15 y 16)]
```

### 4.2 Tabla de plazos

| Hito | Plazo | Computo | Norma |
|---|---|---|---|
| Subsanar la prevencion | 10 dias habiles | Desde el dia siguiente a la notificacion de la prevencion | Art. 18 inc. 3 |
| Devolver solicitud por incompetencia o derecho ajeno a la ley | 5 dias habiles | Posteriores a la recepcion | Art. 19 |
| Resolver rectificacion | 20 dias habiles | Desde la recepcion de la solicitud | Art. 9 inc. 3 |
| Entregar respuesta (todos los derechos) | 20 dias habiles | La ley no fija el dia inicial; LPA Art. 82: desde el dia siguiente a la notificacion (aqui, recepcion). Ver incertidumbre 14.3 | Art. 20 |
| Prorroga | Hasta 20 dias habiles adicionales | Por causas justificadas | Art. 20 |
| Notificar la prorroga | 3 dias habiles y dentro del plazo ordinario | Desde la decision de prorrogar | Lineamientos Art. 34 |
| Documentar y notificar cada actuacion (admision, prevencion, subsanacion, reconocimiento, incompetencia, denegatoria, final) | 3 dias habiles | Desde su emision | Lineamientos Art. 33 |
| Notificar rectificacion, actualizacion o eliminacion a quienes recibieron los datos | 5 dias habiles | Posteriores a la determinacion de procedencia | Art. 21 inc. 3 |
| Notificar denegatoria motivada | 3 dias habiles | Desde la adopcion de la decision | Art. 22 inc. 3 |
| Reclamo del titular ante la ACE por la resolucion | 10 dias habiles | Siguientes a la notificacion | Lineamientos Art. 33 inc. 4 |
| Proceder a la revocacion del consentimiento | 5 dias habiles | Desde la recepcion | Art. 30 |
| Informar la revocacion al encargado | 5 dias habiles | Desde la emision de la resolucion | Art. 30 |

Regla de computo (LPA, supletoria por Art. 62 LPDP, texto segun transcripcion secundaria hazconta.com): los plazos por dias se cuentan solo en dias habiles; el conteo empieza el dia siguiente a la notificacion; si el ultimo dia es inhabil, se prorroga al primer dia habil siguiente (LPA Art. 82). El software necesita un calendario de dias habiles de El Salvador (feriados nacionales y asuetos) mantenido por el proveedor y editable por el cliente.

### 4.3 Bloques de obligacion del procedimiento

**Norma:** LPDP
**Articulo:** Art. 15 (delegado) y Art. 16 (atribuciones), Art. 17 (deber de asistencia)
**Obligacion:** Nombrar un delegado que reciba, tramite y resuelva las solicitudes ARCO-POL y establezca mecanismos para que los datos solo se entreguen al titular o a su representante acreditado; toda dependencia, empleado o proveedor debe asistir al delegado.
**A quien aplica:** Sujetos obligados (Art. 2). Segun fuentes secundarias, la reforma 659 deroga los Arts. 15 y 17 y traslada las funciones del Art. 16 a los sujetos obligados.
**Implicacion para el software:** Modelar "Responsable de atencion ARCO-POL" como rol configurable (delegado nombrado o unidad interna) y un flujo de asistencia interna con tareas asignadas a areas y proveedores, con plazos internos mas cortos que el legal. Mantener la funcionalidad de nombramiento de delegado como opcional para privados y obligatoria para publicos.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (paginas 10 y 11); reforma: https://www.asamblea.gob.sv/node/14116 y https://www.eldiariodehoy.com/noticias/nacionales/asamblea-legislativa-deroga-obligatoriedad-de-las-empresas-privadas-de-nombrar-delegados-de-proteccion-de-datos-personales/93615/2026/ (secundaria), consultados 2026-09-23
**Vigencia:** VIGENTE (Decreto 144); MODIFICADA por D.L. 659 con vigencia pendiente de publicacion
**Clasificacion:** OBLIGATORIO hoy; tras la reforma, la funcion sigue siendo OBLIGATORIA pero el nombramiento de delegado pasa a RECOMENDADO en el sector privado (segun fuentes secundarias)

**Norma:** LPDP
**Articulo:** Art. 18 (requisitos de la solicitud)
**Obligacion:** Admitir solicitudes que contengan: a) nombre del titular o representante, domicilio y medios para notificaciones; b) documentos que acrediten la identidad del titular y, en su caso, del representante; c) de ser posible, el area que trata los datos; d) descripcion clara y precisa de los datos (salvo acceso); e) descripcion del derecho que se ejerce o de lo que se solicita; f) cualquier otro elemento que facilite localizar los datos; g) firma del titular o representante "o cualquier otro medio equivalente que permite establecer la anuencia de estos". En acceso, el titular indica la modalidad de reproduccion y el responsable debe atenderla salvo imposibilidad fisica o juridica fundada, ofreciendo otras modalidades.
**A quien aplica:** Responsable del tratamiento (en el texto vigente, a traves del delegado).
**Implicacion para el software:** Formulario de captura con los siete requisitos como campos, validacion de completitud que marque que falta y genere automaticamente el borrador de prevencion. Campo "modalidad de entrega" con las cinco opciones del formulario ACE y campo "imposibilidad fisica o juridica" con motivacion obligatoria si no se puede atender la modalidad pedida. Aceptar como "medio equivalente a la firma" mecanismos configurables por el cliente (firma electronica, confirmacion desde correo verificado, comparecencia presencial), con decision documentada por abogado del cliente.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (pagina 11), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

**Norma:** LPDP
**Articulo:** Art. 18 inciso final (prevencion y archivo)
**Obligacion:** Si falta un requisito o se necesita informacion adicional, prevenir por una sola ocasion para que se subsane en 10 dias habiles contados desde el dia siguiente a la notificacion; si no se subsana o se subsana sin atender la prevencion, archivar sin mas tramite dejando a salvo el derecho a presentar nueva solicitud.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Estado "prevenida" con contador de 10 dias habiles, bloqueo de segunda prevencion (solo una), estado "archivada por falta de subsanacion" con resolucion de archivo notificada, y posibilidad de vincular una nueva solicitud del mismo titular. La prevencion debe listar exactamente los requisitos omitidos.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (pagina 11), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (CONDICIONAL a que la solicitud sea incompleta)

**Norma:** LPDP; Lineamientos ACE
**Articulo:** Art. 19 LPDP; Lineamientos Art. 35
**Obligacion:** Si el responsable no es competente o la solicitud corresponde a un derecho distinto de los previstos en la ley, comunicarlo al titular y devolver la peticion dentro de los 5 dias habiles posteriores a su recepcion. Los Lineamientos precisan las causales: a) no se posee en los registros la informacion requerida; b) no se esta legalmente habilitado para el tratamiento de los datos solicitados por corresponder a un derecho diferente a lo regulado en la LPDP.
**A quien aplica:** Responsable del tratamiento (en el texto vigente, el delegado).
**Implicacion para el software:** Resolucion de incompetencia con causal (a o b), plazo de 5 dias habiles desde la recepcion, notificacion al titular con orientacion (si se conoce el responsable competente, sugerirlo sin obligacion legal). El Art. 22 lit. g permite ademas denegar por incompetencia si se detecta despues.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (pagina 12); C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ocr\lineamientos_dpo\page-10.png (Art. 35, verificado en imagen), consultados 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (CONDICIONAL a la incompetencia)

**Norma:** LPDP; Lineamientos ACE
**Articulo:** Art. 20 LPDP; Lineamientos Art. 34
**Obligacion:** Entregar la respuesta en 20 dias habiles, prorrogables por causas justificadas sin exceder otros 20 dias habiles. La prorroga debe motivarse y notificarse al interesado en 3 dias habiles y dentro del plazo ordinario.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Contador de 20 dias habiles con semaforo (verde, amarillo a los 10, rojo a los 15), accion "prorrogar" que exige motivo escrito, genera la notificacion y solo esta disponible mientras el plazo ordinario no haya vencido; segundo contador de hasta 20 dias. Registro del vencimiento como evento de riesgo (infraccion grave Art. 56 lit. b num. 2).
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (pagina 12); C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ocr\lineamientos_dpo\page-10.png (Art. 34), consultados 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

**Norma:** LPDP
**Articulo:** Art. 21 (entrega de la informacion, constancia y notificacion a receptores)
**Obligacion:** (1) El acceso se cumple poniendo los datos a disposicion mediante copias simples, copias certificadas, consulta directa, documentos electronicos o cualquier medio analogo. (2) Durante la rectificacion, dejar constancia de que la informacion esta sometida a rectificacion cuando un tercero pida acceso. (3) Si hubo comunicacion o transferencia, notificar la rectificacion, actualizacion o eliminacion a quienes recibieron los datos dentro de los 5 dias habiles posteriores a la determinacion de procedencia.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Acta de entrega con modalidad, fecha, medio y evidencia (acuse). Subtarea automatica "notificar a receptores" al marcar procedente una rectificacion, actualizacion o eliminacion, alimentada por el registro de transferencias y encargados del titular, con plazo de 5 dias habiles y evidencia por receptor. Leyenda "en proceso de rectificacion" visible para consultas de terceros.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (pagina 12), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (la notificacion a receptores es CONDICIONAL a que haya habido comunicacion o transferencia)

**Norma:** LPDP
**Articulo:** Art. 22 (excepciones, negativa parcial y resolucion motivada)
**Obligacion:** Solo se puede denegar en los supuestos a) a h): a) el solicitante no es el titular o el representante no esta acreditado; b) no se encuentran los datos del solicitante; c) se perjudican derechos e intereses legitimos de un tercero; d) notorio error en la identificacion de los datos o falsedad de los hechos descritos; e) impedimento legal o resolucion de autoridad competente; f) cancelacion u oposicion ya realizada previamente; g) el responsable no es competente; h) demas casos de esta u otras leyes. La negativa puede ser parcial. En todos los casos: resolucion motivada, notificada al titular o representante en 3 dias habiles desde la adopcion de la decision, por el mismo medio senalado por el titular, acompanada de las pruebas y documentacion consideradas.
**A quien aplica:** Responsable del tratamiento (en el texto vigente, el delegado).
**Implicacion para el software:** Catalogo cerrado de causales de denegatoria (a-h) con obligacion de seleccionar al menos una y redactar motivacion; soporte para negativa parcial por dato o categoria; generador de resolucion motivada; adjuntar pruebas; plazo de 3 dias habiles desde la fecha de decision; canal de notificacion igual al senalado en la solicitud, validado por el sistema. Toda denegatoria queda marcada como evento de riesgo alto (infraccion muy grave Art. 56 lit. c num. 2 si es contraria a la ley).
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (paginas 12 y 13), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

**Norma:** LPDP; Lineamientos ACE
**Articulo:** Art. 23 LPDP; Lineamientos Art. 38
**Obligacion:** El ejercicio es gratuito; solo se pueden cobrar costos de reproduccion, certificacion o envio, sin superar el valor de los materiales o de la remision; el responsable debe publicar y comunicar esos costos (los Lineamientos: preferentemente en formato electronico o sitio web, y comunicarlos al interesado antes de la entrega). Si se entrega en dispositivo magnetico o electronico, el interesado aporta el medio. El envio electronico no tiene costo cuando sea posible.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Tabla de costos publicada por el cliente (con fecha de publicacion y URL o evidencia), calculo automatico del costo por modalidad, bloqueo de cualquier cobro por la tramitacion en si, registro de que el costo fue comunicado antes de la entrega. Exigir pago indebido es infraccion leve (Art. 56 lit. a num. 7).
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (pagina 13); C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\lineamientos_dpo_OCR.txt (Art. 38, page-11), consultados 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

**Norma:** LPDP
**Articulo:** Art. 33 inciso 1
**Obligacion:** "El responsable establecera y documentara procedimientos para el ejercicio de los derechos ARCO-POL sobre los datos personales objetos de tratamiento, con base en las politicas de actuacion emitidas por la Entidad Rectora y las medidas de seguridad minimas necesarias."
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** El procedimiento ARCO-POL del cliente debe existir como documento versionado dentro del sistema (plantilla generada a partir de la ley y los lineamientos, adaptada por el cliente), con fecha de aprobacion y evidencia de comunicacion interna. Es la base documental que se exhibira a la ACE.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (pagina 17), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

**Norma:** LPDP
**Articulo:** Art. 24 lit. e y f; Art. 61 inc. 2
**Obligacion:** El aviso de privacidad debe indicar los mecanismos, medios y procedimientos para ejercer los derechos ARCO-POL y revocar el consentimiento, y el nombre del delegado y lugar o medios para presentar la solicitud. Los sujetos obligados tenian 6 meses desde la vigencia de la ley (hasta el 23 may 2025) para establecer mecanismos de ejercicio de derechos.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Los canales de recepcion configurados en el modulo ARCO-POL (correo, direccion fisica, portal) deben sincronizarse con el texto del aviso de privacidad generado por el sistema. Tras la reforma 659 el literal f) podria cambiar de "delegado" a otra denominacion: el campo debe ser configurable.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (paginas 13, 14 y 27), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 4.4 Reglas operativas de los Lineamientos de la ACE (Capitulo VIII, Arts. 32 a 38)

Los Lineamientos para el Delegado (D.O. Tomo 452, N. 146, 11 ago 2026, emitidos el 24 jul 2026) contienen un capitulo especifico "Del ejercicio de los derechos ARCO-POL". Texto verificado en la imagen page-10.png del OCR. Puntos operativos:

- Art. 32: el delegado promovera el uso de los formularios elaborados por la ACE "como estandar minimo"; puede incorporar elementos adicionales justificados que no obstaculicen, desmotiven ni impidan el ejercicio; los formularios de la ACE "seran aceptados por todos los responsables y Delegados aun cuando cuenten con modelos propios"; no se puede rechazar una solicitud presentada en formulario oficial. Los responsables, publicos o privados, pondran a disposicion del publico los formularios "a traves de sus sitios web, plataformas digitales, oficinas fisicas u otros medios institucionales adecuados", garantizando formularios fisicos en todas sus sedes cuando se requiera.
- Art. 33: resolver todas las solicitudes mediante resolucion: "admision, prevencion, subsanacion, reconocimiento del derecho, incompetencia, denegatoria o resolucion final". Todas se documentan y notifican al interesado en 3 dias habiles desde su emision. Si es procedente, la resolucion senala la fecha en que se hara efectivo el derecho, dentro del plazo legal, salvo impedimento justificado y documentado. El titular agraviado puede presentar escrito ante la Direccion de Proteccion de Datos Personales de la ACE en 10 dias habiles desde la notificacion; la ACE pedira informe al delegado o responsable.
- Art. 34: 20 dias habiles; prorroga motivada y notificada en 3 dias habiles dentro del plazo ordinario.
- Art. 35: causales de incompetencia (ver bloque del Art. 19).
- Art. 36: deber de confidencialidad del delegado, que subsiste 5 anos despues de cesar en el cargo.
- Art. 37: los sujetos obligados respaldan al delegado con recursos y acceso a los datos y operaciones.
- Art. 38: publicar costos, preferentemente en sitio web, y comunicarlos antes de la entrega.
- Art. 30 (Capitulo VII): el delegado informa al responsable al menos dos veces al ano, incluyendo "las estadisticas de solicitudes de derechos ARCO-POL tramitadas".

**Norma:** Lineamientos para el Delegado de Proteccion de Datos Personales (ACE)
**Articulo:** Arts. 32 y 33
**Obligacion:** Aceptar los formularios oficiales de la ACE, ponerlos a disposicion del publico (web, plataformas, oficinas), resolver cada solicitud mediante resolucion documentada (siete tipos) y notificarla en 3 dias habiles desde su emision, fijando la fecha de efectividad cuando sea procedente.
**A quien aplica:** Delegado y responsable (publicos y privados). Aplicabilidad a privados sin delegado tras la reforma 659: incierta.
**Implicacion para el software:** Maquina de estados con los siete tipos de resolucion como salidas formales, cada una con plantilla, fecha de emision, fecha de notificacion (control de 3 dias habiles) y evidencia del envio. Campo "fecha de efectividad del derecho" obligatorio en reconocimientos. Portal publico o enlace descargable con los formularios oficiales y con el formulario propio del cliente si lo tiene. Estadisticas semestrales de solicitudes por derecho, estado y plazo.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\lineamientos_dpo_OCR.txt y C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ocr\lineamientos_dpo\page-10.png, consultados 2026-09-23
**Vigencia:** VIGENTE desde 19 ago 2026 (aplicabilidad a privados sin delegado pendiente de la reforma 659)
**Clasificacion:** OBLIGATORIO para quien tenga delegado; RECOMENDADO como estandar minimo para todo responsable privado mientras no se aclare el alcance tras la reforma

---

## 5. Representacion, herederos, ninez y adolescencia, personas incapaces

### 5.1 Representacion

- Art. 6: "representante con facultades especiales". Art. 18 lit. b: documentos que acrediten la identidad del titular y, en su caso, de la persona que le represente. Art. 22 lit. a: denegar si el representante no esta debidamente acreditado. Art. 16 lit. c: mecanismos para que los datos solo se entreguen al titular o a su representante debidamente acreditado.
- Formularios ACE: "Copia del poder de representacion (si aplica)" y campo "Representante Legal (si aplica)".
- LPA (supletoria, texto segun transcripcion secundaria): la representacion se otorga "mediante instrumento publico o documento privado con firma legalizada notarialmente", o por comparecencia ante el funcionario (Art. 69); la falta o insuficiencia de acreditacion no impide tener por realizado el acto si se subsana en diez dias (Art. 67 inc. 4), lo que es coherente con la prevencion del Art. 18 LPDP.
- Representacion legal (no voluntaria): padres, madres o tutores de NNA; representante de persona declarada incapaz (Art. 26 inc. 3: derecho comun); representante legal de personas juridicas no aplica porque el titular siempre es persona natural (Art. 4 lit. s).

**Norma:** LPDP
**Articulo:** Arts. 6, 16 lit. c, 18 lit. b y 22 lit. a
**Obligacion:** Verificar que el representante esta debidamente acreditado antes de entregar datos o ejecutar el derecho; denegar (o prevenir) si no lo esta.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Adjunto obligatorio "poder de representacion" cuando el solicitante es representante voluntario, con campos: tipo de instrumento (escritura publica, documento privado con firma legalizada, otro), notario, fecha, alcance (menciona expresamente derechos ARCO-POL o proteccion de datos: si/no). Lista de verificacion de acreditacion con firma del analista. Para representacion legal de NNA o incapaces, adjuntos alternativos (partida de nacimiento, carne de minoridad, resolucion judicial de tutela o declaratoria).
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (paginas 6, 10, 11 y 12); LPA Arts. 67 y 69 via https://hazconta.com/leyes/ley-de-procedimientos-administrativos/art-69 (secundaria), consultados 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 5.2 Herederos y sucesores (titular fallecido)

- Art. 6 inc. 3: los herederos o sucesores ejercen los derechos "debiendo acreditar con documentacion que demuestre su calidad de heredero o sucesor".
- Formularios ACE (todos salvo portabilidad): casilla "Los datos corresponden a: Persona fallecida"; adjuntos "Copia de certificacion de partida de defuncion (si aplica)" y "Copia de documento que compruebe el vinculo familiar con el fallecido (si aplica)".
- Punto abierto: la ley exige acreditar la calidad de heredero o sucesor; el formulario se conforma con partida de defuncion y prueba de vinculo familiar, que acreditan parentesco pero no necesariamente la calidad de heredero (que en derecho salvadoreno se acredita con declaratoria de herederos). El formulario de la ACE es un estandar minimo, asi que lo prudente es aceptar la solicitud con esos documentos y, si el analista tiene dudas, prevenir para pedir la declaratoria. Requiere abogado.

**Norma:** LPDP
**Articulo:** Art. 6 inc. 3
**Obligacion:** Atender solicitudes de herederos o sucesores del titular fallecido, previa acreditacion documental de esa calidad.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Tipo de solicitante "heredero o sucesor" con adjuntos: partida de defuncion, documento de vinculo familiar, y opcionalmente declaratoria de herederos o testamento. Advertencia al analista de que la prueba de vinculo no equivale a calidad de heredero y que puede prevenir. Los formularios ACE de portabilidad no contemplan fallecidos; el sistema puede permitirlo con base en el Art. 6 pero marcarlo como caso a revisar.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (pagina 6); formularios en C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_form_*.txt, consultados 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (titular fallecido)

### 5.3 Ninez y adolescencia

- Art. 5 lit. j: principio de ejercicio progresivo de las facultades: los derechos de NNA se ejercen de manera progresiva segun el desarrollo evolutivo, con la direccion y orientacion de padres, madres o representante legal y la legislacion vigente (LEPINA, no analizada en este sweep).
- Art. 26 inc. 2: el consentimiento de NNA se rige por el ejercicio progresivo. Art. 42: interes superior; antes de ejercer derechos hay que informar a los NNA y a sus progenitores o tutores sobre el contenido y como ejercerlos, en lenguaje adaptado a su edad.
- Art. 12 lit. b: en la ponderacion de intereses legitimos para la oposicion, especial proteccion "cuando el titular sea un nino o nina". Art. 10 lit. f: causal de cancelacion especifica para datos obtenidos en oferta directa de servicios de la sociedad de la informacion a ninos.
- Art. 56 lit. c num. 3: usar datos de NNA sin consentimiento previo de padres, representantes o tutores es infraccion muy grave.
- Formularios ACE: casilla "Los datos corresponden a: Ninez y Adolescencia"; adjuntos "Copia de certificacion de partida de nacimiento (si aplica)" y "Copia de carne de minoridad (si aplica)"; campo de representante legal.
- La ley no fija una edad a partir de la cual el adolescente puede presentar la solicitud por si mismo. Requiere abogado (ver seccion 14).

**Norma:** LPDP
**Articulo:** Arts. 5 lit. j, 26 inc. 2 y 42
**Obligacion:** Garantizar el interes superior y el ejercicio progresivo: informar a NNA y a sus progenitores o tutores del contenido de los derechos y de como ejercerlos, en lenguaje claro y adaptado; tramitar las solicitudes con intervencion del representante legal segun el desarrollo del NNA.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Marcador "titular NNA" que: exige datos y acreditacion del representante legal (partida de nacimiento o carne de minoridad), eleva la prioridad y el estandar de ponderacion en oposicion y cancelacion, y usa plantillas de respuesta en lenguaje sencillo. Si un adolescente presenta la solicitud por si mismo, el sistema no la rechaza automaticamente; la marca para decision documentada del analista con base en el ejercicio progresivo.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (paginas 6, 15 y 19), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (CONDICIONAL a que el titular sea NNA)

### 5.4 Personas declaradas incapaces

- Art. 26 inc. 3: "Cuando se trate de datos personales de personas declaradas incapaces se estara a lo dispuesto por el derecho comun" (Codigo de Familia y Codigo Civil: tutela o curatela, representante designado judicialmente).
- Art. 56 lit. c num. 4: tratar datos de personas declaradas incapaces sin consentimiento del titular o su representante es infraccion muy grave.
- Art. 43: observar leyes y tratados sobre grupos en situacion de desventaja (personas con discapacidad, adultos mayores, poblacion indigena).
- Los formularios ACE no tienen casilla para este supuesto; se cubre con "Representante Legal (si aplica)" y "Copia del poder de representacion".

**Norma:** LPDP
**Articulo:** Art. 26 inc. 3 y Art. 43
**Obligacion:** Tramitar las solicitudes relativas a personas declaradas incapaces a traves de su representante conforme al derecho comun, con acreditacion documental (resolucion judicial de tutela o curatela).
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Tipo de representacion "tutor o curador judicial" con adjunto de resolucion judicial; accesibilidad de los canales de solicitud para personas con discapacidad (Art. 43) como criterio de diseno del portal.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (paginas 15 y 19), consultado 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (titular declarado incapaz)

---

## 6. Verificacion de identidad

### 6.1 Que exige la ley

- Art. 18 lit. b: "Los documentos que acrediten la identidad del titular y, en su caso, de la persona que le represente". La ley no especifica cuales documentos.
- Art. 8 inc. 3: el acceso por consulta directa procede "previa identificacion de su identidad y de los datos que por medio de su visualizacion pretende conocer".
- Art. 16 lit. c: mecanismos "para asegurar que los datos personales solo se entreguen a su titular o al representante de este que se encuentre debidamente acreditado".
- Art. 22 lit. a: causal de denegatoria si el solicitante no es el titular o el representante no esta acreditado.
- Art. 22 inc. 3: la notificacion se hace "por el mismo medio senalado por el titular", lo que refuerza la importancia de registrar y validar el canal de notificacion.
- Principio de seguridad (Art. 5 lit. f) y de minimizacion (Art. 5 lit. d): los documentos de identidad recabados para verificar son a su vez datos personales que deben protegerse y no conservarse mas de lo necesario.

### 6.2 Que piden los formularios oficiales

Los siete formularios ARCO-POL de la ACE piden:
- "Copia del Documento Unico de Identidad del solicitante DUI." (siempre)
- "Copia del poder de representacion (si aplica)."
- "Pruebas o documentos adicionales que respalden la solicitud (si aplica)."
- "Copia de certificacion de partida de nacimiento (si aplica)" y "Copia de carne de minoridad (si aplica)" para NNA.
- "Copia de certificacion de partida de defuncion (si aplica)" y "Copia de documento que compruebe el vinculo familiar con el fallecido (si aplica)" para fallecidos (no en portabilidad).

Brechas: los formularios no mencionan pasaporte ni carne de residente para extranjeros, ni documentos de identidad de personas no salvadorenas. Por analogia, los Lineamientos Art. 7 admiten para el delegado "Documento Unico de Identidad o Pasaporte". Recomendacion: aceptar DUI, pasaporte o carne de residente, documentado en el procedimiento interno (Art. 33), y consultar con abogado.

**Norma:** LPDP; formularios ACE
**Articulo:** Art. 18 lit. b, Art. 16 lit. c, Art. 22 lit. a; formularios version 07-07-2025
**Obligacion:** Verificar la identidad del solicitante (y del representante) con documentos antes de ejecutar cualquier derecho; el estandar minimo del formulario oficial es la copia del DUI.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Paso obligatorio "verificacion de identidad" con: tipo de documento (DUI, pasaporte, carne de residente, otro), numero, adjunto, cotejo con los datos que la empresa ya tiene del titular (nombre, DUI o correo registrado), metodo de verificacion (documento, comparecencia, correo verificado, videollamada) y quien verifico y cuando. Los adjuntos de identidad deben tener retencion corta y acceso restringido (minimizacion y seguridad). El sistema nunca declara "identidad verificada" por si mismo; registra la verificacion hecha por una persona del cliente.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (paginas 10 a 12); https://ace.gob.sv/page/formularios y archivos C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_form_*.txt, consultados 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

---

## 7. Formularios oficiales de la ACE: inventario y campos completos

Fuente: https://ace.gob.sv/page/formularios (consultado 2026-09-23). Version de todos los formularios: 07-07-2025. Los cuatro formularios que no estaban en el corpus local (oposicion, olvido, rectificacion, limitacion) se descargaron el 2026-09-23 y se guardaron en C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ como ace_form_oposicion.pdf/.txt, ace_form_olvido.pdf/.txt, ace_form_rectificacion.pdf/.txt y ace_form_limitacion.pdf/.txt.

| Formulario | URL oficial (relativa a https://ace.gob.sv/) | Archivo local |
|---|---|---|
| Acceso | documentos/formularios/FORMULARIODEACCESOADATOSPERSONALES07072025.pdf | ace_form_acceso.txt |
| Rectificacion | documentos/formularios/FORMULARIODERECTIFICACIONDEDATOSPERSONALES07072025.pdf (con acento en el nombre real del archivo) | ace_form_rectificacion.txt |
| Cancelacion o supresion | documentos/formularios/FORMULARIODESOLICITUDDECANCELACIONOSUPRESIONDEDATOSPERSONALES07072025.pdf (con acentos) | ace_form_cancelacion.txt |
| Oposicion | documentos/formularios/FORMULARIODELDERECHODEOPOSICION07072025.pdf (con acento) | ace_form_oposicion.txt |
| Limitacion | documentos/formularios/FORMULARIODELDERECHOALALIMITACIONDELTRATAMIENTODEDATOSPERSONALES07072025.pdf (con acento) | ace_form_limitacion.txt |
| Portabilidad | documentos/formularios/FORMULARIODELDERECHODEPORTABILIDAD07072025.pdf | ace_form_portabilidad.txt |
| Olvido | documentos/formularios/FORMULARIODELDERECHOALOLVIDO07072025.pdf | ace_form_olvido.txt |
| Nombramiento de delegado | documentos/formularios/FORMULARIODENOMBRAMIENTODEDELEGADODEPROTECCIONDEDATOSPERSONALES07072025.pdf (con acento) | ace_form_nombramiento_delegado.txt |

No existe formulario oficial de revocacion del consentimiento en la pagina, aunque el Art. 50 lit. q lo preve.

### 7.1 Estructura comun a los siete formularios ARCO-POL

Encabezado:
1. Logo de la institucion (espacio para el logo del responsable).
2. Referencia (numero de expediente o referencia interna).
3. Titulo del formulario y cita textual del articulo de la LPDP que fundamenta el derecho.

Bloque "DATOS DE LA ENTIDAD RESPONSABLE DEL TRATAMIENTO":
4. Nombre o razon social.
5. Domicilio.
6. Correo electronico.
7. Telefono.

Bloque "DATOS DEL O LA SOLICITANTE O REPRESENTANTE LEGAL":
8. Nombre completo del solicitante.
9. Domicilio.
10. Correo electronico.
11. Telefono.
12. Representante legal (si aplica) / Nombre del representante legal (si aplica).
13. Los datos corresponden a: casilla "Ninez y Adolescencia".
14. Los datos corresponden a: casilla "Persona fallecida" (ausente en portabilidad).

Bloque especifico del derecho (ver 7.2).

Bloque "FORMA DE ENTREGA DE LA RESPUESTA" (en acceso se llama "Modalidad de acceso"):
15. Modalidad: Copia simple / Correo electronico / Copia certificada / Dispositivo de almacenamiento (acceso anade "Consulta directa"; limitacion indica "si aplica").
16. Lugar o medio para recibir notificaciones: Correo electronico (linea para escribirlo) / Acudir con el delegado de Proteccion de Datos Personales.

Bloque "DOCUMENTACION ADJUNTA" (casillas):
17. Copia del Documento Unico de Identidad del solicitante DUI.
18. Copia del poder de representacion (si aplica).
19. Pruebas o documentos adicionales que respalden la solicitud (si aplica).
20. Copia de certificacion de partida de nacimiento (si aplica).
21. Copia de carne de minoridad (si aplica).
22. Copia de certificacion de partida de defuncion (si aplica) (ausente en portabilidad).
23. Copia de documento que compruebe el vinculo familiar con el fallecido (si aplica) (ausente en portabilidad).

Bloque "FIRMA DEL O LA SOLICITANTE":
24. Lugar.
25. Fecha.
26. Firma del solicitante o representante legal.

Bloque "USO INTERNO (responsable del tratamiento)":
27. Recepcionista.
28. Fecha de recepcion.
29. Sello.

Pie:
30. "La presente solicitud puede ser enviada por los siguientes medios: Correo electronico: ____ Direccion fisica: ____" (el responsable rellena sus canales).
31. Nota (*) sobre costos del Art. 23: los costos de reproduccion, certificacion y envio seran establecidos y previamente publicados por los sujetos obligados; el titular aporta el dispositivo de almacenamiento.
32. Nota (**): si se inicia un proceso ante la ACE, esta podra requerir informacion adicional a las partes.

### 7.2 Campos especificos por formulario

Acceso (Art. 8):
- "Derecho que se ejerce: ACCESO A DATOS PERSONALES" (fijo).
- "Descripcion de la solicitud: Indique de forma clara y precisa los datos personales que desea consultar, la fecha o periodo en que se llevo a cabo la recoleccion de sus datos y el area que considera responsable de su tratamiento, si lo conoce." (texto libre).
- "Modalidad de acceso (Seleccione una opcion)": Consulta directa / Copia simple / Correo electronico / Copia certificada / Dispositivo de almacenamiento.

Rectificacion (Art. 9):
- "Derecho que se ejerce: RECTIFICACION DE DATOS PERSONALES" (fijo).
- "Descripcion de la solicitud: Indique de forma clara y precisa los datos personales que desea rectificar y el area que considera responsable de su tratamiento, si lo conoce." (texto libre).
- "Documentacion que acredita la procedencia de la rectificacion": Documento 1 / Documento 2.

Cancelacion o supresion (Art. 10):
- "MOTIVO DE LA SOLICITUD" (casillas): (1) Los datos personales ya no son necesarios para los fines para los cuales fueron tratados; (2) El titular retira su consentimiento y el tratamiento no se basa en otra causa de licitud; (3) El titular se opone al tratamiento y no existen motivos legitimos que justifiquen su conservacion; (4) Los datos personales han sido obtenidos o tratados ilicitamente; (5) Los datos personales deben suprimirse para el cumplimiento de una obligacion legal; (6) Los datos personales se obtuvieron en relacion con la oferta de servicios dirigidos a ninos; (7) Otro (especificar).
- "Fecha aproximada del inicio del tratamiento de datos personales y descripcion de los hechos que motivan la causal de su solicitud" (texto libre).

Oposicion (Art. 12):
- Texto fijo: "Solicito el cese en el tratamiento de mis datos personales con base en el derecho de oposicion contemplado en el Articulo 12 ... por las siguientes razones:" (casillas): (1) Oposicion a la elaboracion de perfiles o clasificaciones con fines comerciales o de mercadotecnia directa; (2) Otro motivo (especificar).
- "DESCRIPCION DE LOS DATOS PERSONALES AFECTADOS: Indique y describa la fecha o tiempo aproximado de los datos personales respecto a los cuales solicita la oposicion y la razon especifica" (texto libre).

Limitacion (Art. 13):
- Texto fijo con casillas de supuestos: (1) Impugnacion de la exactitud de mis datos personales mientras se verifica su exactitud; (2) El tratamiento de mis datos es ilicito y me opongo a su supresion, solicitando en su lugar la limitacion de su uso; (3) El responsable ya no necesita los datos personales para los fines del tratamiento, pero el titular los necesita para la formulacion, el ejercicio o la defensa de reclamaciones; (4) Me he opuesto al tratamiento de mis datos personales mientras se verifica si los motivos legitimos del responsable prevalecen sobre los mios.
- "DESCRIPCION DE LOS DATOS PERSONALES AFECTADOS: Indique los datos personales respecto de los cuales solicita la limitacion del tratamiento" (texto libre).

Portabilidad (Art. 14):
- Texto fijo: "Solicito el ejercicio del derecho de portabilidad ... para recibir mis datos personales en un formato estructurado, de uso comun, de lectura mecanica e interoperable."
- "DATOS PERSONALES QUE SOLICITA" (texto libre).
- "DESTINATARIO/A DE LOS DATOS (si aplica)": Nombre o razon social / Domicilio / Correo electronico / Telefono.
- Documentacion adjunta reducida a 5 casillas (sin partida de defuncion ni vinculo familiar); no hay casilla "Persona fallecida".

Olvido (Art. 10 inciso final):
- "Derecho que se ejerce: EJERCICIO DEL DERECHO AL OLVIDO" (fijo).
- "Descripcion, fecha o periodo aproximado de los datos a eliminar: Indique de forma clara y precisa los datos personales que desea eliminar y, si aplica, la ubicacion de estos en la base de datos del responsable" (texto libre).
- "MOTIVO DE LA SOLICITUD" (casillas): (1) La informacion publicada es inexacta o incorrecta; (2) La informacion es desactualizada o no pertinente; (3) La informacion ha dejado de ser relevante con el paso del tiempo; (4) Otro motivo (especificar).
- "DOCUMENTACION QUE ACREDITA LA PROCEDENCIA DE LA ELIMINACION": Documento 1 / Documento 2.

Nombramiento de delegado (Arts. 15 y 16), para referencia: datos del sujeto obligado (nombre, NIT, domicilio, correo, telefono); datos del delegado (nombre completo, domicilio, correo, telefono, documento de identidad, fecha de nombramiento); atribuciones transcritas; firmas del delegado y del representante legal; sello; nota de que se requiere acuerdo institucional suscrito por el titular de la institucion.

### 7.3 Observaciones de diseno derivadas de los formularios

- El campo "Referencia" implica un numero de expediente asignado por el responsable: el software debe generar una referencia unica por solicitud.
- "Recepcionista, Fecha de recepcion, Sello" implica un acuse de recibo: el software debe emitir acuse con fecha, hora y persona que recibe, porque de esa fecha dependen los plazos de 5 y 20 dias habiles.
- La opcion "Acudir con el delegado de Proteccion de Datos Personales" como medio de notificacion puede quedar desactualizada tras la reforma 659: etiqueta configurable.
- La casilla "Otro" en cancelacion, oposicion y olvido significa que el sistema no puede restringir las causales a una lista cerrada; debe permitir texto libre y que el analista lo reconduzca a una causal legal.
- Los formularios son un "estandar minimo" (Lineamientos Art. 32): el cliente puede anadir campos justificados, pero no puede rechazar el formulario oficial. El software debe importar solicitudes recibidas en formulario oficial (PDF o papel) y transcribirlas a la misma estructura.

---

## 8. Vias del titular ante incumplimiento y valor probatorio del expediente

### 8.1 Vias

1. Denuncia ante la ACE por incumplimiento del plazo de rectificacion (Art. 9 inc. 3) y por negativa a tramitar la revocacion del consentimiento (Art. 31). Ambas normas habilitan la denuncia de forma expresa; la ACE tiene competencia general de supervision y sancion (Art. 50 lit. a y b) y de asistencia a los ciudadanos (Art. 50 lit. s), por lo que cualquier incumplimiento ARCO-POL puede denunciarse.
2. Reclamo o escrito ante la Direccion de Proteccion de Datos Personales de la ACE contra la resolucion del delegado, en 10 dias habiles desde la notificacion, senalando motivos y pruebas; la ACE pide informe al delegado o responsable (Lineamientos Art. 33 inc. 4 y 5).
3. Procedimiento sancionador (Normativa sancionadora): inicio de oficio, por denuncia, por aviso o por cualquier otro medio (Art. 15); diligencias preliminares de investigacion (Arts. 7 a 12, maximo 90 dias habiles prorrogables); requisitos de la denuncia (Art. 16: organo al que se dirige, nombre y generales del titular, domicilio y medio para notificaciones, relacion de hechos, identificacion de presuntos responsables, peticion, firma, lugar y fecha; puede presentarse por escrito o por medio tecnologico habilitado; con apoderado, acompanando personeria); emplazamiento al presunto infractor con 5 dias habiles para contestar y proponer prueba (Arts. 19 y 21); resolucion final en 15 dias habiles desde recibido el expediente (Art. 32); via contencioso administrativa (Art. 32 inc. final y Art. 33).
4. Otras acciones "que conforme al ordenamiento juridico pudiera ejercer" (Art. 31), como el amparo constitucional por autodeterminacion informativa; fuera del alcance de este sweep.

### 8.2 El expediente como prueba

- Art. 54: la carga de la prueba del consentimiento y de la comunicacion del aviso recae en el responsable. Aunque el Art. 54 no menciona el ARCO-POL, el principio de responsabilidad demostrada (Art. 5 lit. i) y la obligacion de documentar procedimientos (Art. 33) trasladan al responsable la necesidad de probar que atendio en tiempo y forma.
- Normativa sancionadora Art. 24: constituyen prueba "los instrumentos publicos, los autenticos, los instrumentos privados, las declaraciones de testigos, los resultados de peritajes, la inspeccion de los lugares o de las cosas, la confesion, los informes de auditoria internos o externos, cualquier otra informacion que hubiese sido proporcionada por el presunto infractor a la Agencia u obtenida por esta ultima ... las presunciones legales y cualquier otro medio admisible en derecho". Valoracion segun sana critica, con aplicacion supletoria del Codigo Procesal Civil y Mercantil.
- Normativa sancionadora Art. 43: parametros de la multa: gravedad del dano, efecto disuasivo, duracion de la conducta, caracter intencional o negligente, categoria de los datos, capacidad economica. Un expediente completo permite demostrar diligencia (no intencionalidad) y corta duracion.
- Lineamientos Art. 33: el reclamo del titular provoca que la ACE pida informe al delegado o responsable "a fin de verificar sus actuaciones dentro del procedimiento administrativo"; ese informe se construye desde el expediente.
- Formularios ACE, nota (**): "En caso de que se inicie la sustanciacion de un proceso ante la Agencia de Ciberseguridad del Estado, dicha entidad podra requerir informacion adicional a las partes involucradas".

**Norma:** LPDP; Normativa sancionadora ACE; Lineamientos ACE
**Articulo:** Arts. 5 lit. i, 33 y 54 LPDP; Normativa Arts. 16, 24 y 43; Lineamientos Art. 33
**Obligacion:** Poder demostrar ante la ACE, con documentos, que cada solicitud fue recibida, tramitada, resuelta y notificada en los plazos y formas legales.
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Expediente inmutable por solicitud con: solicitud original (archivo y transcripcion), acuse con fecha y hora, verificacion de identidad, prevenciones y subsanaciones, analisis de fondo con causales, resoluciones con fecha de emision y de notificacion, evidencia de envio por el canal elegido, actas de entrega, notificaciones a receptores, costos comunicados, prorrogas motivadas, y bitacora de usuarios y fechas de cada actuacion. Funcion "exportar expediente para la ACE" en formato legible con indice y sellos de tiempo. Funcion "informe de actuaciones" para responder el requerimiento del Lineamientos Art. 33.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (paginas 6, 17 y 24); C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\normativa_sancionadora_OCR.txt (pages 05, 06 y 09); C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ocr\lineamientos_dpo\page-10.png, consultados 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (la forma concreta del expediente es RECOMENDADO; el deber de demostrar es obligatorio)

---

## 9. Conservacion del expediente ARCO-POL

Hallazgo: no existe en la LPDP, en la Normativa sancionadora, en los Lineamientos ni en las Politicas ACE una norma que fije cuanto tiempo debe conservarse el expediente de una solicitud ARCO-POL. Se buscaron los terminos "conserv", "archiv", "expediente" y "prescri" en todo el corpus local.

Normas relacionadas que sirven para construir un criterio:

| Norma | Regla | Uso como referencia |
|---|---|---|
| Normativa sancionadora Art. 47 | Las infracciones y sanciones de la LPDP prescriben en 5 anos; computo segun LPA Art. 149 (desde el dia siguiente a la comision de la infraccion; se interrumpe con el inicio del procedimiento notificado) | Mientras la ACE pueda sancionar, el expediente es la prueba de descargo: minimo 5 anos desde la ultima actuacion |
| Lineamientos Art. 31 | La documentacion de la autorizacion y publicacion del aviso de privacidad se conserva "durante un plazo minimo de diez anos" | Muestra el estandar de la ACE para documentacion de cumplimiento: 10 anos |
| Lineamientos Art. 36 | Confidencialidad del delegado subsiste 5 anos tras el cese | Coherente con el plazo de prescripcion de 5 anos |
| LPDP Art. 11 | Los datos bloqueados se conservan "en los plazos establecidos para el resguardo segun las leyes aplicables" | La propia ley remite a plazos externos de conservacion |
| LPDP Art. 5 lit. h y Art. 10 inc. 2 lit. f | Principio de temporalidad; la supresion no procede cuando los datos se necesitan "para la formulacion, el ejercicio o la defensa de reclamaciones" | Conservar el expediente para defensa es una finalidad licita, pero con minimizacion |
| Codigo de Comercio Art. 451 (fuente secundaria, no verificado en texto oficial) | Los comerciantes conservan libros y documentos de su giro por 10 anos y hasta 5 anos despues de la liquidacion | Referencia general de archivo empresarial |

Criterio propuesto para el software (RECOMENDADO, requiere validacion de abogado):
- Retencion minima por defecto: 5 anos contados desde el cierre del expediente (fecha de la ultima notificacion o entrega), alineada con la prescripcion de infracciones y sanciones. Si se abre un procedimiento ante la ACE o un litigio, la retencion se extiende hasta 5 anos despues de la firmeza de la resolucion.
- Retencion recomendada: 10 anos, alineada con el estandar de la ACE para documentacion de cumplimiento (Lineamientos Art. 31) y con el archivo mercantil.
- Minimizacion dentro del expediente: las copias de documentos de identidad y poderes pueden tener una retencion mas corta (por ejemplo, hasta que venza el plazo de reclamo del titular ante la ACE mas un margen) y sustituirse por un acta de verificacion; los datos entregados en un acceso no necesitan copiarse en el expediente, basta el acta de entrega con descripcion.
- El plazo debe ser un parametro configurable por cliente, con justificacion documentada, y el sistema debe alertar al vencimiento y registrar la eliminacion.

**Norma:** Normativa sancionadora ACE; Lineamientos ACE; LPDP
**Articulo:** Normativa Art. 47; Lineamientos Art. 31; LPDP Arts. 5 lit. h y 11
**Obligacion:** No hay obligacion expresa de plazo. Obligacion implicita de conservar evidencia mientras subsista la posibilidad de sancion (5 anos) y de no conservar datos mas alla de lo necesario (temporalidad).
**A quien aplica:** Responsable del tratamiento.
**Implicacion para el software:** Politica de retencion del expediente ARCO-POL configurable, con valor por defecto de 5 anos y valor recomendado de 10, distinguiendo retencion del expediente y retencion de adjuntos de identidad; motor de alertas y registro de eliminacion.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\normativa_sancionadora_OCR.txt (page-09); C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\lineamientos_dpo_OCR.txt (Art. 31); LPA Art. 149 via https://hazconta.com/leyes/ley-de-procedimientos-administrativos/art-149 (secundaria), consultados 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** RECOMENDADO (no hay mandato expreso)

---

## 10. Casos especiales

| Caso | Regla aplicable | Tratamiento recomendado en el software | Clasificacion |
|---|---|---|---|
| Solicitud anonima o sin identificacion | Art. 18 lit. a y b exigen nombre y documentos de identidad; Art. 22 lit. a permite denegar si el solicitante no es el titular ni representante acreditado | No se rechaza de plano: se registra, se emite prevencion unica (10 dias habiles) pidiendo identificacion; si no se subsana, archivo (Art. 18). Si es imposible notificar la prevencion por falta de medio, archivar dejando constancia | OBLIGATORIO (prevencion) |
| Solicitudes masivas, repetitivas o abusivas | La LPDP no regula solicitudes abusivas. Unicos apoyos: Art. 22 lit. f (cancelacion u oposicion "previamente realizada") y lit. d (notorio error o falsedad) | Cada solicitud tiene su propio plazo de 20 dias; el sistema detecta duplicados por titular y derecho y sugiere resolver por Art. 22 lit. f cuando ya se ejecuto lo pedido, con motivacion. No existe base para cobrar ni para negarse por volumen. Requiere abogado para casos extremos | INCERTIDUMBRE |
| Solicitud a quien no es competente | Art. 19: informar y devolver en 5 dias habiles; Lineamientos Art. 35: causales a) y b); Art. 22 lit. g | Resolucion de incompetencia en 5 dias habiles con causal; sugerir al titular el responsable correcto si se conoce (sin obligacion legal) | OBLIGATORIO |
| Datos en poder de un encargado | El encargado trata por cuenta del responsable (Art. 4 lit. j); el titular tiene derecho a conocer al encargado (Art. 7); Art. 21 inc. 3 (notificar a quienes recibieron los datos en 5 dias habiles); Art. 30 por analogia (informar al encargado en 5 dias habiles); Art. 33 inc. 2 y Art. 34 (encargado sometido a la ley) | El responsable responde siempre. El sistema mantiene el registro de encargados por tratamiento y genera tareas de requerimiento al encargado (para localizar, rectificar, suprimir) con plazo interno y evidencia; si un encargado recibe directamente una solicitud, debe redirigirla al responsable (clausula contractual recomendada) | OBLIGATORIO (responder) / RECOMENDADO (clausula) |
| Datos ya disociados o anonimizados | Art. 4 lit. h (disociacion irreversible); Art. 8 lit. b (dejar constancia); Art. 10 inc. 2 lit. d (no procede la cancelacion); Art. 22 lit. b (no se encuentran datos) | Respuesta de acceso con constancia de disociacion; cancelacion improcedente sobre la parte disociada, con motivacion; si todo esta disociado, resolucion por Art. 22 lit. b. Datos seudonimizados (Art. 4 lit. q) no son disociados: siguen siendo accesibles | CONDICIONAL |
| Datos de terceros mezclados | Art. 8 lit. b ("en ningun caso el informe podra revelar datos pertenecientes a terceros"); Art. 22 lit. c (perjuicio a terceros) e inc. 2 (negativa parcial) | Herramienta de redaccion o exclusion de datos de terceros en el informe de acceso, con registro de que se excluyo y por que; negativa parcial motivada | OBLIGATORIO |
| Titular fallecido | Art. 6 inc. 3; formularios: partida de defuncion y vinculo familiar | Tipo de solicitante "heredero o sucesor"; ver 5.2; prevenir si la calidad de heredero no esta acreditada | CONDICIONAL |
| Titular menor de edad | Arts. 5 lit. j, 26 inc. 2, 42; Art. 56 lit. c num. 3; formularios: partida de nacimiento o carne de minoridad, representante legal | Marcador NNA; ver 5.3; no rechazar automaticamente la solicitud de un adolescente; decision documentada | CONDICIONAL |
| Solicitud por correo electronico | Art. 18 no limita el canal; formularios preven "Correo electronico" como medio de envio y de notificacion; Art. 23 (envio electronico sin costo); Lineamientos Art. 32 (sitios web y plataformas digitales) | Canal formal. El correo de recepcion debe estar publicado en el aviso de privacidad (Art. 24 lit. e y f); el sistema crea el expediente desde el correo, con acuse automatico con fecha y hora | OBLIGATORIO (atender) |
| Solicitud por WhatsApp u otra mensajeria | No mencionado en ley ni lineamientos. Art. 18 lit. g admite "cualquier otro medio equivalente" para la anuencia; Art. 24 lit. e obliga a publicar los mecanismos disponibles | Si el cliente publico WhatsApp como canal, es canal formal y corre el plazo. Si no, buena practica: registrar la fecha de recepcion, responder por el mismo medio indicando los canales formales y el formulario, sin ignorar la peticion. Riesgo: la ACE podria considerar recibida la solicitud desde el primer contacto. Requiere abogado | INCERTIDUMBRE |
| Solicitud presencial | Art. 8 inc. 3 ("mera consulta"); Art. 21 inc. 1 (consulta directa); formularios: "Direccion fisica" y "Acudir con el delegado"; Lineamientos Art. 32 (formularios fisicos en todas las sedes) | Modulo de recepcion presencial: transcripcion del formulario fisico, acuse con sello, fecha y recepcionista; para acceso por consulta directa, acta de la consulta con identificacion | OBLIGATORIO |
| Solicitud sin firma | Art. 18 lit. g: firma "o cualquier otro medio equivalente que permite establecer la anuencia" | No es causal de denegatoria; es causal de prevencion. El cliente define en su procedimiento (Art. 33) que medios acepta como equivalentes (firma electronica, confirmacion desde correo verificado, comparecencia). Requiere abogado para fijar el estandar | OBLIGATORIO (prevencion) / INCERTIDUMBRE (estandar) |
| Solicitud de un derecho no previsto en la ley (por ejemplo, indemnizacion) | Art. 19 y Lineamientos Art. 35 lit. b | Devolucion en 5 dias habiles indicando que no corresponde a un derecho ARCO-POL | OBLIGATORIO |
| Titular que pide varios derechos en una sola solicitud | Los derechos son "independientes" (Art. 4 lit. i); la ley no prohibe acumular | Un expediente por derecho, vinculados entre si, cada uno con su resolucion y plazo; o un expediente con sub-resoluciones. Recomendado: expedientes separados para que la negativa parcial de uno no contamine a otro | RECOMENDADO |

---

## 11. Infracciones y multas asociadas al lente

Transcripcion de las infracciones pertinentes (ace_decreto_144.txt, paginas 24 y 25):

Leves (Art. 56 lit. a):
- 7. "Exigir pago para atender las solicitudes que en la presente ley se establecen como gratuitas."
- 8. "Incumplir con el Derecho de Informacion frente a la Recoleccion de Datos contenido en el articulo 7 o la obligacion de informar del articulo 48".
- 9. "No atender las solicitudes realizadas por parte de la ACE en materia de proteccion de datos personales."

Graves (Art. 56 lit. b):
- 1. "Proporcionar de forma incompleta o inexacta la informacion relativa a los datos personales que del titular se traten, ya sean recolectados o inferidos, cuando este ejerza su derecho de acceso."
- 2. "No atender las solicitudes de derechos ARCO-POL, en el tiempo y forma establecidos por la presente ley."

Muy graves (Art. 56 lit. c):
- 2. "Denegar las solicitudes realizadas para el ejercicio de los derechos ARCO-POL en contravencion a lo establecido en esta ley."
- 3. Uso de datos de NNA sin consentimiento de padres, representantes o tutores.
- 4. Tratar datos de personas declaradas incapaces sin consentimiento del titular o su representante.
- 9. "Tratar datos personales a pesar de la revocacion del consentimiento otorgado por el titular."
- 10. "No hacer efectiva la revocacion del consentimiento ante la solicitud del titular cuando esta proceda."

Multas (Art. 57), en salarios minimos mensuales vigentes del sector comercio:

| Categoria | Rango en salarios minimos | Estimacion en USD con salario minimo de comercio y servicios de US$408.80 (fuente primaria confirmada: Decreto Ejecutivo N. 11 del Organo Ejecutivo en el Ramo de Trabajo y Prevision Social, 22 may 2025, reformado por Decreto Ejecutivo N. 12, 24 may 2025, D.O. N. 96, Tomo 447, 26 may 2025, vigente desde el 1 jun 2025) |
|---|---|---|
| Leve | 1 a 10 | US$408.80 a US$4,088.00 |
| Grave | 11 a 25 | US$4,496.80 a US$10,220.00 |
| Muy grave | 26 a 40 | US$10,628.80 a US$16,352.00 |

Reglas complementarias: medidas adicionales para restablecer la legalidad (Art. 58; Normativa Art. 37); las sanciones no eximen de responsabilidad civil o penal (Art. 58 inc. 2); parametros de graduacion (Normativa Art. 43); pago en 15 dias habiles (Normativa Art. 44); publicacion de resoluciones en version publica (Art. 55; Normativa Art. 46); prescripcion en 5 anos (Normativa Art. 47); aviso a la FGR en 72 horas si hay ilicito penal (Normativa Art. 34).

**Norma:** LPDP
**Articulo:** Art. 56 lit. a num. 7, lit. b num. 1 y 2, lit. c num. 2; Art. 57
**Obligacion:** Evitar las conductas tipificadas: cobrar por lo gratuito, entregar acceso incompleto o inexacto, no atender en tiempo y forma, denegar en contravencion a la ley.
**A quien aplica:** Sujetos obligados (Art. 2).
**Implicacion para el software:** Mapa de riesgos por expediente: cada vencimiento, denegatoria, cobro o entrega parcial se etiqueta con la infraccion potencial y su rango de multa, para priorizar la atencion. El sistema muestra el rango en salarios minimos y permite configurar el monto vigente del salario minimo con fecha y fuente, sin afirmar cual es la sancion aplicable.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (paginas 24 a 26); salario minimo: https://www.jurisprudencia.gob.sv/DocumentosBoveda/D/2/2020-2029/2025/05/10A4DA.PDF (Decreto Ejecutivo N. 11, texto integro, primaria), consultado 2026-09-24
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

---

## 12. Reforma 659 (17 sep 2026): cambios en este procedimiento

Estado: aprobada con 57 votos y dispensa de tramite el 17 sep 2026, a iniciativa del Ejecutivo. Al 23 sep 2026 no se localizo el texto del decreto ni constancia de publicacion en el Diario Oficial. Vigencia prevista: ocho dias despues de su publicacion. Todo lo siguiente es "segun fuentes secundarias" (nota oficial de la Asamblea, El Diario de Hoy, Infobae, elsalvador.com).

Cambios reportados:
1. Derogatoria de los Arts. 15 (delegado obligatorio) y 17 (deber de asistencia al delegado).
2. Reforma del Art. 16: las atribuciones del delegado pasan a los "sujetos obligados", que deberan "fijar lineamientos internos para gestionar las solicitudes ARCO-POL" (El Diario de Hoy).
3. Las solicitudes ARCO-POL se presentan "directamente ante la institucion, empresa u organizacion que tiene o utiliza sus datos" (Asamblea, node/14116).
4. Plazos sin cambio: 20 dias habiles de respuesta, prorroga justificada de hasta 20 mas, prevencion unica con 10 dias habiles para subsanar, devolucion por incompetencia en 5 dias habiles, notificacion a terceros de correccion, actualizacion o eliminacion en 5 dias habiles, denegatoria en 3 dias habiles, revocacion en 5 dias habiles y comunicacion al encargado en 5 dias habiles (El Diario de Hoy, Infobae, Asamblea).
5. Art. 47: el sector publico mantiene el delegado, que puede ser el Oficial de Informacion.
6. Art. 51: el Presidente de la Republica nombra al Director de Proteccion de Datos Personales por 3 anos; la instruccion puede delegarse, la sancion no.
7. Justificacion legislativa: reducir costos administrativos a micro y pequenas empresas sin reducir garantias (diputada Dania Gonzalez, diputado Walter Coto, segun prensa).

Efectos previsibles sobre este lente (analisis propio, no confirmado):
- Los Arts. 18 a 22 mencionan "el delegado" como quien recibe, previene, devuelve, responde, notifica y deniega. Si la reforma solo deroga 15 y 17 y reforma 16, 47 y 51 sin tocar 18 a 22, quedaria una incoherencia textual que habra que interpretar (las funciones las asume el sujeto obligado por la reforma del Art. 16). Verificar en el texto oficial si tambien se reformaron los Arts. 18 a 22, 24 lit. f y 30.
- Los Lineamientos para el Delegado (incluido el Capitulo VIII sobre ARCO-POL) fueron dictados con base en los Arts. 15 y 16; su aplicabilidad a empresas privadas sin delegado queda en duda hasta que la ACE los adapte o emita nuevos lineamientos. Segun el contexto compartido, la ACE dejo sin efecto el registro transitorio de delegados tras el anuncio de la reforma.
- Los formularios oficiales dicen "Acudir con el delegado de Proteccion de Datos Personales" y el aviso de privacidad debe indicar "el nombre del delegado" (Art. 24 lit. f): es probable que la ACE actualice formularios y que el literal f) cambie.
- El registro de delegados ante la ACE (Lineamientos Arts. 9 a 11) deja de ser exigible al sector privado si el nombramiento es voluntario.

**Norma:** Decreto Legislativo N. 659 (reforma a la LPDP)
**Articulo:** Deroga Arts. 15 y 17; reforma Arts. 16, 47 y 51 (segun fuentes secundarias)
**Obligacion:** Las empresas privadas dejan de estar obligadas a nombrar delegado pero asumen directamente la recepcion, tramite y resolucion de las solicitudes ARCO-POL con los mismos plazos, y deben fijar lineamientos internos para gestionarlas.
**A quien aplica:** Sujetos obligados del sector privado.
**Implicacion para el software:** (1) Rol "atencion ARCO-POL" configurable: delegado nombrado (opcional) o unidad o persona responsable; (2) generador de "lineamientos internos" o procedimiento ARCO-POL (ya exigido por el Art. 33); (3) etiquetas de formularios y aviso de privacidad configurables ("delegado" vs "responsable de atencion"); (4) bandera de version normativa: mientras la reforma no se publique, el sistema muestra la version del Decreto 144 y advierte del cambio pendiente; al publicarse, el proveedor activa la nueva version sin cambiar los plazos.
**Fuente oficial:** https://www.asamblea.gob.sv/node/14116 (nota oficial, sin numero de decreto ni articulos); https://www.eldiariodehoy.com/noticias/nacionales/asamblea-legislativa-deroga-obligatoriedad-de-las-empresas-privadas-de-nombrar-delegados-de-proteccion-de-datos-personales/93615/2026/ ; https://www.infobae.com/el-salvador/2026/09/17/el-salvador-la-asamblea-legislativa-elimina-la-obligacion-del-delegado-de-proteccion-de-datos-para-las-empresas/ ; https://www.elsalvador.com/noticias/nacional/reforma-proteccion-datos-personales/1293875/2026/ (todas secundarias), consultados 2026-09-23
**Vigencia:** APROBADA-PENDIENTE-PUBLICACION
**Clasificacion:** CONDICIONAL (a la publicacion y vigencia de la reforma)

---

## 13. Sintesis de requisitos funcionales derivados (para el blueprint)

1. Canales de recepcion configurables y publicados (correo, direccion fisica, portal, otros), sincronizados con el aviso de privacidad (Arts. 18, 24 lit. e y f; Lineamientos Art. 32).
2. Formularios digitales que repliquen los ocho formularios ACE campo a campo (seccion 7), mas importacion de formularios oficiales recibidos en papel o PDF, y formulario propio de revocacion (Art. 30).
3. Acuse de recibo con referencia unica, fecha, hora y receptor; de esta fecha nacen todos los plazos.
4. Lista de verificacion de admision con los siete requisitos del Art. 18 y verificacion de identidad y representacion (seccion 6), con generacion automatica de la prevencion unica (10 dias habiles) y archivo.
5. Resolucion de incompetencia en 5 dias habiles con causales de Lineamientos Art. 35.
6. Contador de 20 dias habiles con calendario de dias habiles de El Salvador, semaforos, prorroga motivada hasta 20 dias notificada en 3 dias habiles dentro del plazo ordinario.
7. Maquina de estados con las siete resoluciones de Lineamientos Art. 33, plantillas, control de notificacion en 3 dias habiles por el canal elegido, fecha de efectividad del derecho.
8. Analisis de fondo guiado por derecho: causales de procedencia e improcedencia (Art. 10), excepciones de oposicion (Art. 12), supuestos de limitacion (Art. 13), requisitos de portabilidad (Art. 14), ponderacion de olvido (Art. 10 inc. final), catalogo cerrado de denegatorias (Art. 22 a-h), negativa parcial.
9. Insumos para el acceso: inventario de sistemas (RAT), bitacora de consultas por usuario y proposito, registro de transferencias e intercambios, marcador de seudonimizacion o disociacion, exclusion de datos de terceros.
10. Tareas de ejecucion hacia areas internas, encargados y receptores: bloqueo con leyenda (Art. 9), limitacion (Art. 13), supresion o bloqueo (Arts. 10 y 11), notificacion a receptores en 5 dias habiles (Art. 21), comunicacion a otros responsables y buscadores (olvido).
11. Costos: tabla publicada, calculo y comunicacion previa; prohibicion de cobrar por la tramitacion (Art. 23; Lineamientos Art. 38).
12. Expediente probatorio inmutable con exportacion para la ACE y generador de "informe de actuaciones" (seccion 8).
13. Politica de retencion del expediente configurable (5 anos minimo, 10 recomendado) con minimizacion de adjuntos de identidad (seccion 9).
14. Estadisticas de solicitudes por derecho, estado, plazo y resultado para los informes semestrales (Lineamientos Art. 30) y para auditorias.
15. Rol de atencion ARCO-POL configurable y bandera de version normativa (Decreto 144 vs reforma 659).
16. Marcadores de casos especiales: NNA, fallecido, incapaz, representante, datos de terceros, datos disociados, encargado, canal informal, duplicado.

---

## 14. Incertidumbres y puntos que requieren abogado

1. Texto oficial de la reforma 659: no localizado. Se desconoce si reforma los Arts. 18 a 22, 24 lit. f y 30 para sustituir "delegado" por "sujeto obligado" o "responsable", si contiene disposiciones transitorias para delegados ya nombrados y registrados, y su fecha exacta de vigencia. Verificar en el Diario Oficial y en el buscador de decretos de la Asamblea antes de congelar el diseno.
2. Aplicabilidad de los Lineamientos para el Delegado (en especial el Capitulo VIII sobre ARCO-POL, Arts. 32 a 38) a empresas privadas que, tras la reforma, no nombren delegado. Posiciones posibles: (a) siguen vigentes como lineamientos de la ACE bajo el Art. 50 lit. n y el Art. 33 LPDP; (b) pierden base legal al derogarse el Art. 15. El software debe tratar sus reglas (resolucion documentada en 3 dias habiles, prorroga notificada en 3 dias habiles, reclamo en 10 dias habiles, publicacion de costos) como estandar recomendado hasta que un abogado o la ACE confirmen.
3. Dia inicial del plazo de 20 dias habiles del Art. 20: la ley no lo fija (el Art. 9 si: "a partir de la recepcion de la solicitud"). Aplicando LPA Art. 82 (supletoria, texto segun fuente secundaria) el conteo empieza el dia siguiente a la recepcion. Ademas, no esta regulado si la prevencion suspende o reinicia el plazo. Criterio conservador para el software: contar desde el dia siguiente a la recepcion original y mostrar tambien la fecha de subsanacion; el abogado del cliente decide cual se aplica.
4. Alcance de "representante con facultades especiales" (Art. 6): si exige poder especial que mencione expresamente el ejercicio de derechos ARCO-POL o basta un poder general con clausula especial; y forma del poder (LPA Art. 69: instrumento publico o documento privado con firma legalizada, segun fuente secundaria).
5. Acreditacion de herederos o sucesores: la ley pide acreditar "su calidad de heredero o sucesor"; los formularios se conforman con partida de defuncion y vinculo familiar. Definir si se exige declaratoria de herederos y como tratar a convivientes o legatarios.
6. Edad a partir de la cual un adolescente puede presentar la solicitud por si mismo (ejercicio progresivo, Art. 5 lit. j; LEPINA no analizada) y como acreditar la representacion de NNA cuando los padres estan separados o el NNA esta bajo tutela.
7. Medios equivalentes a la firma (Art. 18 lit. g): que mecanismos electronicos (Ley de Firma Electronica, confirmacion por correo verificado, autenticacion en portal) son aceptables como "anuencia".
8. Documentos de identidad admisibles para extranjeros (pasaporte, carne de residente): no previstos en los formularios.
9. Solicitudes abusivas o masivas: sin regla en la LPDP; definir con abogado un protocolo de respuesta que no implique denegatoria contraria a la ley (infraccion muy grave).
10. Canales informales (WhatsApp, redes sociales): desde cuando corre el plazo si el titular escribe por un canal no publicado.
11. Conservacion del expediente: sin norma expresa; el criterio de 5 anos minimo y 10 recomendado es propuesta del equipo y debe validarse, incluyendo la retencion diferenciada de copias de DUI y poderes.
12. Reglas de prescripcion de la Ley de Ciberseguridad y Seguridad de la Informacion (a la que remite el Art. 53 LPDP): no se localizaron en el texto local del Diario Oficial; la Normativa sancionadora fija 5 anos, pero conviene confirmar la coherencia con la ley remitida.
13. Politicas ACE N. 001-0309025-DPDP: fecha de emision y publicacion pendiente de verificar; su Art. 5 lit. c (mecanismos de denuncia) y Art. 4 lit. g (digitalizacion) apoyan el producto pero no anaden plazos ARCO-POL.
14. Texto de la LPA (Arts. 67, 69, 81, 82 y 149) tomado de una transcripcion privada (hazconta.com) porque el PDF oficial de la Asamblea es una imagen sin texto; confirmar contra el Diario Oficial.
15. RESUELTO (2026-09-24): el salario minimo de comercio y servicios (US$408.80) quedo confirmado en fuente primaria (Decreto Ejecutivo N. 11 del Organo Ejecutivo en el Ramo de Trabajo y Prevision Social, 22 may 2025, reformado por Decreto Ejecutivo N. 12, 24 may 2025, D.O. N. 96, Tomo 447, 26 may 2025, vigente desde el 1 jun 2025, texto integro en https://www.jurisprudencia.gob.sv/DocumentosBoveda/D/2/2020-2029/2025/05/10A4DA.PDF). Sigue pendiente solo la vigilancia de la proxima revision trienal del Consejo Nacional de Salario Minimo (prevista para 2028) antes de mostrar montos en el producto.
16. Interaccion entre el reclamo del titular ante la ACE (Lineamientos Art. 33, 10 dias habiles) y la denuncia (Arts. 9 y 31; Normativa Art. 16): son vias distintas con requisitos distintos; el software solo necesita informar al titular de su existencia en la resolucion, pero conviene que un abogado redacte el texto.

---

## 15. Fuentes consultadas (fecha de consulta: 2026-09-23)

Fuentes primarias locales:
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (LPDP, copia publicada por la ACE). Arts. 2, 4, 5, 6 a 23, 24, 26, 29 a 34, 42, 43, 46 a 50, 53 a 59, 61, 62, 64.
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\diario_oficial_2024-11-15_mh.txt (D.O. N. 219, Tomo 445; cotejo de Arts. 6, 18, 20 y 22).
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\lineamientos_dpo_OCR.txt y C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ocr\lineamientos_dpo\page-10.png (Lineamientos para el Delegado, D.O. Tomo 452, N. 146, 11 ago 2026; Arts. 30 a 38 y 40 a 42; Arts. 33 a 37 verificados en imagen).
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\normativa_sancionadora_OCR.txt (Normativa sancionadora, D.O. 11 ago 2026; Arts. 4, 6 a 12, 15, 16, 19, 21, 23, 24, 32 a 34, 37, 43 a 47, 49).
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_politicas_protecciondatos.txt (Politicas N. 001-0309025-DPDP; Arts. 2, 4, 5).
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_form_acceso.txt, ace_form_cancelacion.txt, ace_form_portabilidad.txt, ace_form_nombramiento_delegado.txt (corpus previo).
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_form_oposicion.pdf/.txt, ace_form_olvido.pdf/.txt, ace_form_rectificacion.pdf/.txt, ace_form_limitacion.pdf/.txt (descargados el 2026-09-23 desde ace.gob.sv y anadidos al corpus).

Fuentes primarias en linea:
- https://ace.gob.sv/page/formularios (inventario de formularios y URLs, version 07-07-2025).
- https://www.jurisprudencia.gob.sv/DocumentosBoveda/D/2/2020-2029/2025/05/10A4DA.PDF (Decreto Ejecutivo N. 11, Organo Ejecutivo, Ramo de Trabajo y Prevision Social, texto integro de las tarifas de salario minimo vigentes; consultado 2026-09-24).
- https://www.asamblea.gob.sv/node/14116 (nota oficial sobre la reforma, 17 sep 2026; releida el 2026-09-24, sin mencion de fecha de publicacion en el Diario Oficial).
- https://www.asamblea.gob.sv/sites/default/files/documents/decretos/361DDB77-97E7-4EFF-B353-C6D872547E7C.pdf (LPA, PDF imagen sin texto extraible).
- https://www.asamblea.gob.sv/sites/default/files/documents/dictamenes/498798FA-A563-4830-A0C8-306AFBC71497.pdf y https://www.asamblea.gob.sv/sites/default/files/documents/correspondencia/EFBA7BEE-871B-40BE-BD0A-5BD80237CA90.pdf (revisados: corresponden al Dictamen 46 de 2021 y al veto presidencial del D.L. 875 de 2021; historia legislativa, no a la reforma 659).

Fuentes secundarias:
- https://www.eldiariodehoy.com/noticias/nacionales/asamblea-legislativa-deroga-obligatoriedad-de-las-empresas-privadas-de-nombrar-delegados-de-proteccion-de-datos-personales/93615/2026/ (articulos derogados y reformados, plazos).
- https://www.infobae.com/el-salvador/2026/09/17/el-salvador-la-asamblea-legislativa-elimina-la-obligacion-del-delegado-de-proteccion-de-datos-para-las-empresas/ (plazos, votacion 57-1).
- https://www.elsalvador.com/noticias/nacional/reforma-proteccion-datos-personales/1293875/2026/ (solicitudes directas, notificacion a terceros, revocacion).
- https://consortiumlegal.com/2026/09/02/delegado-proteccion-datos-el-salvador/ (contexto sobre lineamientos; sin datos operativos).
- https://hazconta.com/leyes/ley-de-procedimientos-administrativos/art-67 , /art-69 , /art-81 , /art-82 , /art-149 (transcripcion de la LPA).
- https://www.ey.com/es_ce/technical/tax/tax-alerts/el-salvador-salario-minimo-2026 y https://www.mtps.gob.sv/2025/04/25/408-80-seria-nuevo-salario-minimo-en-industria-y-servicio-tras-incremento-del-12-anunciado-por-el-presidente-nayib-bukele/ (salario minimo de comercio y servicios).
- Codigo de Comercio Art. 451 (conservacion de 10 anos), referido por https://www.elsalvadorlegis.com/aspectos-legales-de-la-contabilidad-en-el-salvador/ y resultados de busqueda; no verificado en texto oficial.
