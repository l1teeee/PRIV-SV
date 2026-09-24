# Sweep juridico: Ley base, vigencia, transitorios, ambito y Ley de Ciberseguridad conexa

Proyecto PRIV-SV - Analisis funcional - Lente "ley_base_vigencia"
Fecha de consulta de todas las fuentes: 2026-09-23
Autor: investigador juridico (agente), para el equipo de producto. Este documento no es asesoria legal.

---

## 1. Resumen ejecutivo

1. La norma base es la "Ley para la Proteccion de Datos Personales" (LPDP), Decreto Legislativo N. 144, aprobado el 12 de noviembre de 2024, sancionado el 14 de noviembre de 2024 y publicado en el Diario Oficial N. 219, Tomo N. 445, del 15 de noviembre de 2024 (paginas 24 a 62). Entro en vigencia el 23 de noviembre de 2024 (Art. 64: ocho dias despues de su publicacion). Tiene 64 articulos en 5 titulos. Estado: VIGENTE.

2. El ambito (Art. 2) es universal: toda persona natural o juridica, publica o privada, que trate datos personales de forma manual o automatizada, directamente o a traves de terceros. El sector publico queda ademas sujeto al Titulo III (Arts. 46 a 49). Las exclusiones (Art. 3) son cuatro y todas son "por objeto del tratamiento", no por tipo de entidad, salvo el matiz expreso de los supervisados por la Superintendencia del Sistema Financiero (SSF): a ellos la ley SI les aplica sobre toda la informacion que no sea historial crediticio.

3. Los plazos transitorios estan todos vencidos a la fecha de consulta: la ACE debia dictar sus disposiciones a mas tardar el 23 de febrero de 2025 (Art. 60 inc. 1) y las emitio recien el 2 de septiembre de 2025 (Politicas N. 001-0309025-DPDP, vigentes desde el 3 de septiembre de 2025, segun fuente secundaria); los sujetos obligados tenian tres meses desde esa emision para adecuarse (Art. 60 inc. 2), es decir, hasta el 2 o 3 de diciembre de 2025; y tenian seis meses desde la vigencia de la ley para habilitar mecanismos de ejercicio de derechos (Art. 61 inc. 2), es decir, hasta el 23 de mayo de 2025. No existe ningun periodo de gracia vigente: cualquier empresa que hoy no cumpla esta en mora regulatoria.

4. Barrido de reformas (noviembre 2024 a septiembre 2026): la UNICA reforma a la LPDP es el Decreto Legislativo N. 659 del 17 de septiembre de 2026, que al 23 de septiembre de 2026 figura en el portal de la Asamblea Legislativa como "Pendiente de Publicacion Material en el Diario Oficial y de Entrada en Vigencia". No hay ninguna otra reforma en los listados oficiales de decretos de 2024 (267 decretos), 2025 (302 decretos) ni 2026 (159 decretos al 17 de septiembre). Normas conexas que si se movieron: Decreto 332 (19 jun 2025) reformo la Ley Especial contra los Delitos Informaticos y Conexos; Decreto 523 (24 feb 2026, D.O. 41, Tomo 450, 27 feb 2026) reformo la Ley de Procedimientos Administrativos (nuevo Art. 4-A, apostilla); Decreto 289 (30 abr 2025) dio presupuesto a la ACE. La Ley de Ciberseguridad (Decreto 143) no ha sido reformada.

5. La Ley de Ciberseguridad y Seguridad de la Informacion (Decreto 143, misma fecha y mismo Diario Oficial, paginas 3 a 23, 32 articulos, vigente desde el 23 de noviembre de 2024) NO es una ley de aplicacion general al sector privado: su Art. 2 la dirige a organos del Gobierno, dependencias, autonomas, municipalidades y "cualquier otra entidad u organismo... que posean incidencia en las infraestructuras criticas de la nacion". Una empresa privada solo queda sujeta a sus obligaciones de gestion de ciberseguridad y reporte de incidentes (Art. 6) si tiene incidencia en infraestructuras criticas, lo que la ACE califica por resolucion fundada ratificada por el Presidente (Art. 8 lit. f). Para todas las empresas, en cambio, el Decreto 143 opera por remision del Art. 53 LPDP: aporta el procedimiento sancionador (procedimiento simplificado de la LPA, Art. 28) y la prescripcion de cinco anos de infracciones y sanciones (Art. 29). La ACE desarrollo esa remision en la Normativa para el Procedimiento Administrativo Sancionador (D.O. 146, Tomo 452, 11 ago 2026, vigente 19 ago 2026).

6. La Ley de Procedimientos Administrativos (LPA, Decreto 856 de 2017, vigente desde el 13 de febrero de 2019) es supletoria (Art. 62 LPDP) y aporta las reglas que el software debe modelar para cualquier interaccion con la ACE: computo de plazos solo en dias habiles y desde el dia siguiente a la notificacion (Art. 82), notificacion dentro de tres dias con texto integro y por cualquier medio con constancia (Arts. 97 y 98), obligacion de senalar medio electronico para notificaciones (Art. 99), medidas provisionales incluso antes del procedimiento (Arts. 78 y 152), recursos de reconsideracion (10 dias), apelacion (15 dias, suspende la ejecucion de multas) y revision extraordinaria (Arts. 132 a 138), y el procedimiento simplificado con cinco dias para alegar y quince para resolver, sin recurso administrativo (Art. 158).

7. Hallazgo sobre el corpus local: el archivo diario_oficial_2024-11-15_mh.txt y su PDF solo contienen la pagina indice y las paginas 24 a 62 del Diario Oficial (Decreto 144). Las paginas 3 a 23 (Decreto 143) no estan. Se incorporo al corpus el texto oficial del Decreto 143 publicado por la Asamblea Legislativa (asamblea_decreto_143_ciberseguridad.txt y .pdf), asi como el texto de la LPA (asamblea_decreto_856_lpa.txt) y del Decreto 523 (asamblea_decreto_523_reforma_lpa.txt).

---

## 2. Identidad completa de la Ley para la Proteccion de Datos Personales

| Dato | Valor verificado | Fuente |
|---|---|---|
| Nombre oficial | Ley para la Proteccion de Datos Personales | ace_decreto_144.txt, pag. 1; diario_oficial_2024-11-15_mh.txt, pag. 3 (D.O. pag. 25) |
| Instrumento | Decreto Legislativo N. 144 | Idem, encabezado "DECRETO N.° 144" |
| Iniciativa | Presidente de la Republica, por medio del Ministro de Justicia y Seguridad Publica | ace_decreto_144.txt, pag. 1 ("POR TANTO, en uso de sus facultades constitucionales y a iniciativa del presidente de la Republica, por medio del ministro de Justicia y Seguridad Publica") |
| Fecha de aprobacion | 12 de noviembre de 2024 (Salon Azul del Palacio Legislativo) | ace_decreto_144.txt, pag. 27 |
| Fecha de sancion | 14 de noviembre de 2024 (Casa Presidencial) | ace_decreto_144.txt, pag. 28 |
| Publicacion | Diario Oficial N. 219, Tomo N. 445, viernes 15 de noviembre de 2024, paginas 24 a 62 | diario_oficial_2024-11-15_mh.txt, pag. 1 (sumario: "Decreto No. 144.- Ley para la Proteccion de Datos Personales... 24-62") y pag. 40 (pie "D. O. N° 219 Tomo N° 445") |
| Entrada en vigencia | 23 de noviembre de 2024 (Art. 64: "ocho dias despues de su publicacion en el Diario Oficial") | ace_decreto_144.txt, pag. 27 |
| Extension | 64 articulos, 5 titulos | Conteo sobre el texto integro |
| Firmantes | Ernesto Alfredo Castro Aldana (Presidente AL); Nayib Armando Bukele Ortez (Presidente de la Republica); Hector Gustavo Villatoro (Ministro de Justicia y Seguridad Publica) | ace_decreto_144.txt, pags. 27 y 28 |
| Antecedente legislativo | Dictamen N. 11 de la Comision de Seguridad Nacional y Justicia, 11 nov 2024 (solo historia legislativa) | dictamen_11_2024_ley_original_OCR.txt |
| Estado al 2026-09-23 | VIGENTE, con una reforma aprobada y pendiente de publicacion (Decreto 659, ver seccion 6) | asamblea.gob.sv/leyes-y-decretos/view/7022 |

Nota sobre el texto: la copia publicada por la ACE (ace_decreto_144.txt, 28 paginas, texto limpio) coincide articulo por articulo con la transcripcion del Diario Oficial (diario_oficial_2024-11-15_mh.txt, paginas 2 a 40, con errores de OCR propios de la Imprenta). Para citas textuales se uso la copia de la ACE y se verifico contra el Diario Oficial.

Dato adicional relevante: el Art. 63 inc. 2 derogo expresamente el literal h) del Art. 3, los literales a) y b) del Art. 6, el Titulo III, el literal b) del Art. 50, los literales i) y j) del Art. 58 y los literales a) y b) del Art. 83 de la Ley de Acceso a la Informacion Publica (D.L. 534 de 2010), y "cualquier otra mencion que haga alusion a los datos personales" en esa ley. La LPDP tiene caracter especial y deroga toda disposicion de leyes generales o especiales que la contrarie (Art. 63 inc. 1).

### 2.1 Estructura por titulos, capitulos y rango de articulos

| Titulo | Capitulo / Seccion | Articulos | Contenido |
|---|---|---|---|
| I. Disposiciones generales | Cap. I Objeto y ambito de aplicacion | 1 a 3 | Objeto, ambito, exclusiones |
| I | Cap. II Definiciones y principios rectores | 4 a 5 | 21 definiciones (lit. a a u); 10 principios (lit. a a j) |
| I | Cap. III Derechos de los titulares y su ejercicio - Seccion A Derechos ARCO-POL | 6 a 14 | Derecho general (6), informacion en la recoleccion (7), acceso (8), rectificacion (9), cancelacion y olvido (10), bloqueo (11), oposicion (12), limitacion (13), portabilidad (14) |
| I | Cap. III - Seccion B Del ejercicio de los derechos ARCO-POL | 15 a 23 | Delegado (15), atribuciones (16), deber de asistencia (17), solicitud (18), incompetencia (19), plazos (20), entrega (21), excepciones (22), costos (23) |
| II. De las actividades realizadas sobre los datos personales | Cap. I Privacidad de los datos personales | 24 a 25 | Aviso de privacidad (24), notificacion de vulneraciones (25) |
| II | Cap. II Del previo consentimiento informado | 26 a 31 | Formas (26), requisitos (27), excepciones (28), revocacion (29 a 31) |
| II | Cap. III Del tratamiento de datos personales | 32 a 36 | Finalidad (32), procedimientos ARCO-POL y proveedores (33), obligaciones (34), politicas de actuacion (35), medidas de seguridad (36) |
| II | Cap. IV Del tratamiento de datos sensibles | 37 a 39 | Sensibles (37), recoleccion (38), salud (39) |
| II | Cap. V De la transferencia de datos | 40 a 45 | Transferencia (40), contrato (41), NNA (42), otras garantias (43), internacional (44), participacion de la ACE (45) |
| III. Entidades publicas y relacionadas | Capitulo unico | 46 a 49 | Sector publico |
| IV. De la Entidad Rectora y el regimen sancionador | Cap. I Entidad Rectora | 50 a 52 | ACE y atribuciones (50), ejercicio de potestades y Director de Proteccion de Datos (51), requisitos (52) |
| IV | Cap. II Del procedimiento sancionador | 53 a 55 | Remision a la Ley de Ciberseguridad (53), carga de la prueba (54), publicidad de resoluciones (55) |
| IV | Cap. III De las infracciones y sanciones | 56 a 59 | Infracciones (56), multas (57), medidas adicionales (58), prohibiciones (59) |
| V. Disposiciones transitorias y finales | Capitulo unico | 60 a 64 | Transitorios (60 y 61), ley supletoria (62), especialidad y derogatoria (63), vigencia (64) |

Observacion: la Normativa sancionadora de la ACE (Art. 2) dice que las infracciones estan en el "Titulo IV, Capitulo II" de la LPDP; en el texto de la ley estan en el Capitulo III del Titulo IV (Arts. 56 a 59). Es una imprecision de la normativa, sin efecto practico.

---

## 3. Ambito de aplicacion (Art. 2) y exclusiones (Art. 3)

### 3.1 Texto del Art. 2

"Art. 2.- Esta ley se aplicara a toda persona natural o juridica, de caracter publico o privado, que lleve a cabo actividades relativas o conexas al tratamiento de datos personales, ya sea de manera manual, parcial o totalmente automatizado o a traves de terceros. Se entenderan incluidos incluso aquellos sujetos que realicen las referidas actividades sin cumplir con los requisitos y limites dispuestos en la presente ley.

Los organos del Estado, sus dependencias, las instituciones oficiales autonomas, las autoridades municipales y cualquier otra entidad u organismo, independientemente de su forma, naturaleza o situacion juridica, mediante las cuales se administren recursos publicos, bienes del Estado o ejecuten actos de la administracion publica en general, asi como los servidores publicos y personas que laboren en ellas, dentro o fuera del territorio de la Republica, estaran sujetos especificamente a las disposiciones que se establecen en el Titulo III de la presente ley."

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 2 inc. 1
**Obligacion:** Sujecion a la ley de toda persona natural o juridica, publica o privada, que realice actividades relativas o conexas al tratamiento de datos personales, manual o automatizado, directamente o a traves de terceros. La ley se aplica incluso a quien trata datos sin cumplir sus requisitos (no hay "escape" por informalidad).
**A quien aplica:** Todo responsable y todo encargado (Art. 4 lit. j y p), sin umbral de tamano, facturacion, numero de empleados o volumen de datos. Incluye personas naturales con actividad economica (comerciantes individuales, profesionales).
**Implicacion para el software:** El onboarding no debe preguntar "si" la empresa esta sujeta, sino "en que calidad" (responsable, encargado, o ambas por tratamiento) y "que exclusiones parciales" le alcanzan (seccion 3.2). Debe permitir registrar tratamientos manuales (archivos fisicos) y no solo sistemas. Debe soportar el rol de encargado (proveedor que trata por cuenta de otro) como perfil propio, porque los Arts. 33 inc. 2, 34 y 36 le imponen obligaciones directas.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt pag. 2; diario_oficial_2024-11-15_mh.txt pag. 3 (D.O. pag. 25). Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

Observacion sobre territorialidad: el Art. 2 no contiene un criterio territorial expreso (ni "establecimiento en El Salvador" ni "oferta de bienes o servicios a residentes"). Las Politicas de Actuacion de la ACE (Art. 2) afirman que "tambien aplican a operaciones internacionales vinculadas a ciudadanos salvadorenos", pero una politica administrativa no puede ampliar el ambito de una ley (Art. 161 LPA). La aplicacion a empresas extranjeras sin presencia local es una incertidumbre juridica (ver seccion 10).

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 2 inc. 2 en relacion con Arts. 46 a 49
**Obligacion:** Las entidades publicas (organos del Estado, dependencias, autonomas, municipalidades y cualquier entidad que administre recursos publicos o ejecute actos de administracion publica) quedan sujetas "especificamente" al Titulo III: pueden tratar datos en ejercicio de sus competencias sin consentimiento (Art. 46), con un catalogo reducido de derechos ejercitables (acceso, rectificacion, cancelacion solo por obligacion legal, oposicion, limitacion parcial), deben nombrar delegado que puede ser el Oficial de Informacion (Art. 47), deben informar por avisos en sitios web, plataformas y formularios (Art. 48) y no pueden transferir ni comercializar datos salvo consentimiento escrito o las excepciones del Art. 49.
**A quien aplica:** Sector publico. Tambien alcanza indirectamente a los proveedores privados que tratan datos por cuenta de una entidad publica: deben suscribir acuerdo de confidencialidad y quedan sujetos a todas las obligaciones de la ley (Art. 49 inc. final).
**Implicacion para el software:** El producto se dirige al sector privado, pero (a) un cliente privado que sea proveedor del Estado debe poder registrar ese contrato con la bandera "acuerdo de confidencialidad Art. 49 lit. e" y (b) si en el futuro se ofrece a entidades publicas, el modelo de derechos ARCO-POL debe admitir el catalogo reducido del Art. 46 y el delegado obligatorio del Art. 47 (que la reforma pendiente mantiene).
**Fuente oficial:** ace_decreto_144.txt pags. 2 y 20 a 21. Consulta 2026-09-23.
**Vigencia:** VIGENTE (el Art. 47 sera reformado por el Decreto 659, pendiente de publicacion, manteniendo el delegado publico segun fuentes secundarias)
**Clasificacion:** CONDICIONAL (solo entidades publicas y sus proveedores)

### 3.2 Exclusiones (Art. 3) y su lectura por segmento de clientes

Texto integro del Art. 3:

"Art. 3.- Quedan excluidos de la aplicacion de la presente ley:

a) El tratamiento de datos de historial crediticios que realicen los sujetos obligados en los supuestos de la Ley de Regulacion de los Servicios de Informacion sobre el Historial de Creditos de las Personas. Sin embargo, esta exclusion no aplicara a los integrantes del Sistema Financiero y demas supervisados por la Superintendencia del Sistema Financiero, sobre aquella informacion que no sea relativa al historial crediticio de sus usuarios.

b) El tratamiento de datos personales destinados exclusivamente a actividades en el marco de la vida familiar o domestica, mientras no tengan como proposito una divulgacion o utilizacion comercial.

c) El tratamiento de datos personales u actividades que tengan por objeto la seguridad publica, la defensa, la seguridad del Estado, prevencion, investigacion, deteccion y represion del delito, todo en observancia al debido proceso y respeto a los Derechos Humanos.

d) Cualquier tratamiento de los datos personales realizados en los registros publicos, asi como, en el registro del estado familiar de las alcaldias, en los procedimientos establecidos en la Ley Transitoria del Registro del Estado Familiar y de los Regimenes Patrimoniales del Matrimonio. Se excluye ademas todo tratamiento de datos personales efectuado en aplicacion de la Ley Especial Reguladora de la Emision del Documento Unico de Identidad, Ley de Emision del Documento Unico de Identidad en el Exterior, Ley del Nombre de la Persona Natural por el Registro del Estado Familiar de las Personas Naturales."

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 3 lit. a)
**Obligacion:** Exclusion limitada al tratamiento de datos de historial crediticio que realicen los sujetos obligados de la Ley de Regulacion de los Servicios de Informacion sobre el Historial de Creditos de las Personas (buros o agencias de informacion de datos y los agentes economicos que les reportan). Contra-excepcion expresa: los integrantes del sistema financiero y demas supervisados por la SSF SI quedan sujetos a la LPDP sobre toda la informacion que no sea historial crediticio de sus usuarios.
**A quien aplica:** (1) Bancos, aseguradoras, cooperativas de ahorro y credito, casas de bolsa, administradoras de pensiones, emisores de tarjetas y demas supervisados por la SSF: la LPDP les aplica plenamente sobre datos de clientes (KYC, contacto, transacciones no crediticias, marketing, biometria, grabaciones), empleados, proveedores y prospectos; solo el tratamiento del historial crediticio en los supuestos de la ley especial queda fuera. (2) Buros de credito: el nucleo de su actividad (historial crediticio) esta excluido y regido por su ley especial; todo lo demas (empleados, clientes corporativos como personas naturales, datos que no sean historial crediticio) queda dentro de la LPDP, lectura que debe confirmar un abogado. (3) Comercios que reportan a buros: el reporte de historial crediticio en los supuestos de la ley especial esta excluido, pero el resto de su tratamiento de datos de clientes no.
**Implicacion para el software:** El inventario de tratamientos debe permitir marcar por actividad (no por empresa) la bandera "tratamiento de historial crediticio bajo ley especial - excluido Art. 3 a)", con advertencia de que la exclusion no exime del resto de tratamientos. Para el segmento SSF se debe mostrar un texto explicativo de la contra-excepcion. La normativa sectorial de la SSF sobre datos (secreto bancario, normas tecnicas) coexiste y no fue objeto de este lente.
**Fuente oficial:** ace_decreto_144.txt pag. 2. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (solo respecto de tratamientos de historial crediticio en los supuestos de la ley especial)

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 3 lit. b)
**Obligacion:** Exclusion del tratamiento "destinado exclusivamente a actividades en el marco de la vida familiar o domestica, mientras no tengan como proposito una divulgacion o utilizacion comercial".
**A quien aplica:** Personas naturales en su esfera privada (agenda personal, fotos familiares). No aplica a un comerciante individual que use una lista de contactos para vender, ni a una persona que publique datos de terceros.
**Implicacion para el software:** El producto es B2B; no necesita modelar esta exclusion salvo para explicar en el modulo educativo que el criterio es el proposito (comercial o de divulgacion) y no el tamano del negocio. Un emprendedor individual con clientes esta dentro de la ley.
**Fuente oficial:** ace_decreto_144.txt pag. 2. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 3 lit. c)
**Obligacion:** Exclusion del tratamiento "que tenga por objeto la seguridad publica, la defensa, la seguridad del Estado, prevencion, investigacion, deteccion y represion del delito".
**A quien aplica:** Por su objeto, corresponde a autoridades estatales (PNC, FGR, Fuerza Armada, sistema penitenciario). La ley no dice que las empresas de seguridad privada, de videovigilancia o los departamentos de prevencion de fraude esten excluidos: su tratamiento tiene fines privados (proteccion de bienes propios, cumplimiento contractual), no "seguridad publica". Requiere confirmacion de abogado caso por caso.
**Implicacion para el software:** No ofrecer una opcion de "exclusion por seguridad" a clientes privados. Los tratamientos de videovigilancia, control de acceso y prevencion de fraude de empresas privadas deben inventariarse como tratamientos ordinarios, normalmente con base de licitud "interes legitimo" u "obligacion legal" (Art. 5 lit. g, numerales 3 y 6), lo que determinara otro lente.
**Fuente oficial:** ace_decreto_144.txt pag. 2. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 3 lit. d)
**Obligacion:** Exclusion del tratamiento realizado "en los registros publicos", en el registro del estado familiar de las alcaldias y en la emision del DUI y del nombre de la persona natural.
**A quien aplica:** Entidades registrales (CNR, RNPN, registros del estado familiar municipales). La exclusion cubre el tratamiento "realizado en" esos registros, no el uso posterior que un privado haga de la informacion obtenida de ellos: una empresa que consulta un registro publico sigue sujeta a la LPDP en su propio tratamiento, con la unica ventaja de que los datos de "fuentes de acceso publico" no requieren consentimiento si no son sensibles (Art. 28 lit. a, con la definicion del Art. 4 lit. l).
**Implicacion para el software:** El inventario de tratamientos debe permitir declarar como origen del dato "fuente de acceso publico" (Art. 4 lit. l) y derivar de ello la base de licitud aplicable, sin tratar esos datos como "excluidos".
**Fuente oficial:** ace_decreto_144.txt pag. 2. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

Tabla resumen por segmento de clientes:

| Segmento | Sujeto a la LPDP | Exclusion o regimen especial | Efecto practico para el producto |
|---|---|---|---|
| Empresa privada en general (comercio, servicios, industria, salud privada, educacion privada, tecnologia) | Si, plenamente (Art. 2 inc. 1) | Ninguna | Cliente tipo. Todos los modulos aplican |
| Banco, aseguradora, cooperativa y otros supervisados por la SSF | Si (Art. 3 lit. a, segunda frase) | Solo el historial crediticio bajo la ley especial queda fuera | Cliente tipo con bandera "historial crediticio excluido" por tratamiento; coexistencia con normativa SSF a documentar por otro lente |
| Buro de credito / agencia de informacion de datos | Parcialmente | Su actividad principal esta excluida (Art. 3 lit. a, primera frase) | Segmento marginal; requiere abogado; el resto de sus tratamientos entra |
| Encargado (proveedor tecnologico, call center, nube, nomina externa) | Si (Arts. 4 lit. j, 33 inc. 2, 34, 36) | Ninguna | Perfil propio "encargado" con obligaciones de seguridad y confidencialidad |
| Entidad publica | Si, bajo Titulo III (Arts. 46 a 49) | Regimen especial | Fuera del alcance comercial inicial; modelo de derechos reducido si se incorpora |
| Proveedor privado de una entidad publica | Si (Art. 49 inc. final) | Debe firmar acuerdo de confidencialidad | Bandera contractual en el modulo de terceros |
| Persona natural, uso domestico | No (Art. 3 lit. b) | Excluida | No es cliente |
| Autoridades de seguridad publica y registros publicos | No en esas actividades (Art. 3 lit. c y d) | Excluidas por objeto | No son clientes |

---

## 4. Definiciones clave (Art. 4) y principios (Art. 5)

### 4.1 Definiciones con impacto directo en el diseno

| Literal | Termino | Nucleo de la definicion legal | Implicacion concreta para el software |
|---|---|---|---|
| a) | Autodeterminacion informativa | Facultad de la persona de ejercer sus derechos y accionar los mecanismos de la ley sobre su informacion, en registros publicos o privados, digitales o no | Fundamento de todo el modulo de derechos: el titular controla "la divulgacion y el uso" de sus datos "en cada momento" |
| b) | Base de datos o repositorio | Conjunto organizado de datos personales objeto de tratamiento, "electronico o no", cualquiera sea su modalidad | El inventario debe admitir repositorios fisicos (archivos, expedientes en papel) y no solo sistemas |
| c) | Bloqueo de datos | Restriccion temporal o permanente de cualquier acceso o tratamiento | Estado "bloqueado" en el ciclo de vida del dato y del tratamiento (Arts. 9 inc. 3 y 11) |
| d) | Consentimiento | Manifestacion libre, especifica, informada, expresa e individualizada, por declaracion o "clara accion afirmativa", "en los casos en que no exista otro fundamento legal" | Registro de consentimientos con evidencia; el consentimiento es residual frente a otras bases del Art. 5 lit. g |
| e) | Cookie | Informacion enviada por un sitio web y almacenada en el navegador | El aviso de privacidad debe declarar el uso de cookies (Art. 24 lit. i); plantilla de aviso con seccion de cookies |
| f) | Datos personales | Informacion concerniente a persona natural identificada o identificable, en texto, imagen o audio; incluye domicilio, nacionalidad, estado familiar y canales de contacto; "No se tratan como datos personales aquellos que no permiten identificar o localizar a una persona" | Catalogo de categorias de datos con ejemplos de imagen y audio (videovigilancia, grabacion de llamadas); los datos anonimizados salen del ambito |
| g) | Datos personales sensibles | Datos sobre caracteristicas fisicas o morales o circunstancias de la vida privada cuyo uso indebido pueda causar discriminacion o afectar honor, intimidad e imagen; lista "enunciativa pero no limitativa": creencias religiosas, origen etnico, afiliacion o ideologia politica, afiliacion sindical, preferencias sexuales, salud fisica y mental, informacion biometrica, genetica, situacion moral y familiar, habitos personales | Marcado obligatorio de categoria sensible en el inventario; dispara consentimiento escrito con firma autografa o equivalente (Art. 26 inc. 4), advertencia del derecho a no darlo (Art. 37) y las prohibiciones del Art. 59. La lista abierta obliga a permitir categorias sensibles "otras" definidas por el usuario |
| h) | Disociacion o anonimizacion | Procedimiento "irreversible" por el cual los datos dejan de asociarse al titular | Solo la anonimizacion irreversible saca datos del ambito; el software debe distinguirla de la seudonimizacion y registrar el metodo |
| i) | Derechos ARCO-POL | Acceso, Rectificacion, Cancelacion, Oposicion, Portabilidad, Olvido y Limitacion; "personalisimos e independientes" | Siete tipos de solicitud, cada uno con su flujo; el titular puede ejercerlos por separado |
| j) | Encargado del tratamiento | Quien trata datos "por cuenta del responsable" | Perfil de proveedor con obligaciones propias (Arts. 34 y 36) |
| k) | Emisor de datos personales | Titular del banco de datos o encargado en El Salvador que transfiere a otro pais | Rol en el modulo de transferencias internacionales |
| l) | Fuentes de acceso publico | Bases de datos publicas o privadas cuya consulta puede realizarse "por disposicion de ley" por cualquier persona, incluso pagando tarifa | Origen del dato que exime de consentimiento si no es sensible (Art. 28 lit. a); no incluye redes sociales ni sitios web por el solo hecho de ser accesibles: exige que una ley habilite la consulta |
| m) | Limitacion | El titular pide que se apliquen medidas para evitar modificacion, borrado o supresion | Estado "limitado" del tratamiento vinculado a la solicitud del Art. 13 |
| n) | Medidas de seguridad | Politicas, acciones o controles que garanticen confidencialidad, integridad y disponibilidad de registros fisicos o electronicos | Catalogo de controles organizativos, tecnicos y fisicos (desarrollado por las Politicas ACE) |
| o) | Receptor de datos personales | Quien recibe datos en transferencia internacional, como titular, encargado o tercero | Rol en el modulo de transferencias |
| p) | Responsable del tratamiento | Administrador de la base de datos o quien decide finalidad y medios | Perfil principal del cliente |
| q) | Seudonimizacion | Los datos ya no pueden asociarse al titular sin informacion adicional, que debe estar "separada, oculta, clasificada y resguardada" | Control de seguridad registrable; revertirla sin consentimiento es infraccion muy grave (Art. 56 lit. c num. 8) |
| r) | Sitios de contingencia | Sitio alterno donde se replican los datos | Deben informarse al titular en la recoleccion (Art. 7 lit. b); el inventario debe registrar respaldos y sitios alternos |
| s) | Titular | "toda persona natural cuyos datos sean objeto del tratamiento" | Los datos de personas juridicas no estan protegidos por esta ley; los datos de sus representantes o contactos (personas naturales) si |
| t) | Tratamiento de datos | Cualquier operacion automatizada o manual: obtencion, uso, registro, organizacion, conservacion, difusion, almacenamiento, posesion, acceso, manejo y divulgacion | El inventario debe capturar el ciclo completo, incluido el acceso y la mera posesion |
| u) | Transferencia de datos personales | Toda comunicacion a persona distinta del responsable o encargado, "con el consentimiento previo e informado de su titular" | La comunicacion a un encargado no es transferencia; la comunicacion a un tercero exige consentimiento previo salvo excepciones (Arts. 28, 40, 44) |

### 4.2 Principios (Art. 5) y su traduccion a controles

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 5 lit. g) Principio de licitud
**Obligacion:** Todo tratamiento debe apoyarse en al menos una de seis condiciones: (1) consentimiento expreso para una o varias finalidades; (2) necesidad para ejecutar un contrato del que el titular es parte o medidas precontractuales; (3) cumplimiento de obligacion legal del responsable; (4) proteccion de intereses vitales; (5) fin de interes publico o ejercicio de poderes publicos; (6) intereses legitimos del responsable "siempre y cuando esos intereses no atenten contra los derechos o libertades de los titulares".
**A quien aplica:** Responsables (y encargados en cuanto ejecutan tratamientos por cuenta de aquellos).
**Implicacion para el software:** Cada tratamiento del inventario debe tener una base de licitud obligatoria seleccionada de este catalogo cerrado de seis, con justificacion documentada cuando sea interes legitimo (ponderacion) y con enlace al consentimiento o al contrato cuando corresponda. Sin base de licitud el tratamiento debe quedar marcado como riesgo.
**Fuente oficial:** ace_decreto_144.txt pag. 5. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 5 lit. c) Principio de consentimiento y finalidad
**Obligacion:** El consentimiento debe ser libre, especifico, informado, expreso e individualizado y "que establezca el fin, proposito y periodo de almacenamiento y tratamiento".
**A quien aplica:** Responsables.
**Implicacion para el software:** El registro de consentimiento debe capturar, ademas de la evidencia, la finalidad y el periodo de almacenamiento declarado. Las plantillas de clausulas de consentimiento deben incluir esos tres elementos como campos obligatorios.
**Fuente oficial:** ace_decreto_144.txt pag. 5. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 5 lit. e) Principio de transparencia
**Obligacion:** Informar al titular todas las caracteristicas del tratamiento "en forma concisa, de facil acceso y con un lenguaje claro y sencillo. Se prohibe recurrir a textos extensos, terminologias tecnicas o legales y/o letra pequena".
**A quien aplica:** Responsables.
**Implicacion para el software:** El generador de avisos y politicas de privacidad debe medir extension y legibilidad y advertir cuando el texto sea largo o use jerga; debe orientar a formatos por capas. El cumplimiento de este principio es tambien una defensa probatoria (Art. 54: la carga de probar la comunicacion del aviso recae en el responsable).
**Fuente oficial:** ace_decreto_144.txt pag. 5. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 5 lit. d) minimizacion y lit. h) temporalidad
**Obligacion:** Datos "suficientes, pertinentes y no excesivos" respecto del proposito especifico y legitimo; conservacion "limitada al periodo en el que se lograran los fines".
**A quien aplica:** Responsables y encargados.
**Implicacion para el software:** Cada tratamiento debe declarar categorias de datos y periodo de conservacion con criterio de fin; el sistema debe generar alertas de revision o supresion al vencer el periodo y registrar la evidencia de la supresion o del bloqueo (Art. 11 permite conservar bloqueados los datos a disposicion de autoridades por los plazos legales).
**Fuente oficial:** ace_decreto_144.txt pags. 5 y 6. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 5 lit. a) Principio de exactitud
**Obligacion:** Mantener datos exactos, completos y actualizados; suprimir o rectificar "sin dilacion" los inexactos. "Se presumiran exactos y actualizados los datos obtenidos directamente de su titular."
**A quien aplica:** Responsables.
**Implicacion para el software:** Registrar el origen del dato (directo del titular o de terceros) porque de ello depende la presuncion de exactitud; vincular con el flujo de rectificacion del Art. 9 (20 dias habiles y bloqueo durante la revision).
**Fuente oficial:** ace_decreto_144.txt pags. 4 y 5. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 5 lit. f) Principio de seguridad de datos, en relacion con Art. 36
**Obligacion:** Garantizar seguridad, integridad, disponibilidad y confidencialidad para evitar alteracion, perdida, consulta o tratamiento no autorizado, y "detectar desviaciones de informacion, intencionales o no". El Art. 36 obliga a acatar las medidas de seguridad que establezca la ACE y extiende la obligacion al encargado.
**A quien aplica:** Responsables y encargados.
**Implicacion para el software:** Modulo de controles de seguridad con el catalogo minimo de las Politicas ACE (organizativas, tecnicas, fisicas y de transferencia) y registro de evidencia; el principio exige capacidad de deteccion, lo que enlaza con el registro de incidentes del Art. 25.
**Fuente oficial:** ace_decreto_144.txt pags. 5 y 17. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 5 lit. i) Principio de responsabilidad demostrada, en relacion con Arts. 44 inc. 3 y 54
**Obligacion:** La entidad que trata datos "debe ser responsable del cumplimiento efectivo de las medidas que implementen" y de garantizar una efectiva proteccion; en transferencias debe implementar medidas "apropiadas y efectivas" (Art. 44); la carga de probar el consentimiento y la comunicacion del aviso recae en el responsable (Art. 54).
**A quien aplica:** Responsables (y encargados en lo que les corresponde).
**Implicacion para el software:** Es el fundamento juridico de la plataforma: todo lo que el software registra (politicas, tareas, evidencias, consentimientos, avisos, incidentes, contratos) debe ser exportable como expediente probatorio con fecha, autor y hash o equivalente, porque la empresa tendra que demostrar, no solo afirmar, el cumplimiento.
**Fuente oficial:** ace_decreto_144.txt pags. 6, 19 y 24. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 5 lit. j) ejercicio progresivo de facultades, con Arts. 26 inc. 2, 42 y 56 lit. c num. 3
**Obligacion:** Los derechos de ninas, ninos y adolescentes se ejercen de forma progresiva segun su desarrollo, con la direccion de padres o representantes; en cualquier tratamiento se garantiza su interes superior y se les informa en lenguaje adaptado (Art. 42). Usar datos de NNA sin consentimiento previo de padres, representantes o tutores es infraccion muy grave.
**A quien aplica:** Todo responsable que trate datos de menores de 18 anos (colegios, clinicas, comercio en linea, entretenimiento, seguros).
**Implicacion para el software:** Bandera "titulares menores de edad" en el tratamiento, que exige consentimiento de representante, aviso en lenguaje adaptado y control de la excepcion de cancelacion del Art. 10 lit. f. La ley no fija una edad de consentimiento digital; es una incertidumbre a resolver con abogado.
**Fuente oficial:** ace_decreto_144.txt pags. 6, 15, 19 y 25. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (solo si se tratan datos de NNA)

Los principios de lealtad (lit. b) y las prohibiciones del Art. 59 completan el cuadro: recabar datos por medios fraudulentos, desleales o ilicitos viola el principio de lealtad, y el Art. 59 prohibe crear bases de datos sensibles en contravencion de la ley, tratar datos que revelen origen racial, afiliacion partidaria, convicciones religiosas, salud, vida y orientacion sexual sin observar el Capitulo IV del Titulo II, y revelar, difundir, comercializar, utilizar, transferir o compartir datos en contravencion de la ley (infraccion grave por Art. 56 lit. b num. 6).

---

## 5. Disposiciones transitorias (Arts. 60 y 61): calculo de fechas y estado

Texto integro:

"Art. 60.- La ACE debera dictar las politicas, medidas, guias y cualquier otra disposicion necesaria para la aplicacion de la presente ley a mas tardar tres meses contados a partir de la vigencia de la misma.

Los sujetos obligados tendran un plazo de tres meses a partir de la emision de las referidas disposiciones para adecuar e implementar lo regulado respecto a la proteccion de datos personales."

"Art. 61.- A partir de la entrada en vigencia de la presente ley, los sujetos obligados deberan adoptar las medidas de proteccion de datos personales que establezca la ACE para aquellos datos personales obtenidos previo a la entrada en vigencia de la misma.

Asimismo, tendran un plazo de seis meses contados a partir de la vigencia de la presente ley para establecer mecanismos para que los titulares de los datos personales ejercen sus derechos en el marco de la proteccion de datos personales."

Hechos de calculo:
- Publicacion: viernes 15 de noviembre de 2024. Vigencia (Art. 64, ocho dias despues): sabado 23 de noviembre de 2024.
- Emision de las Politicas de Actuacion y Manejo de Datos Personales N. 001-0309025-DPDP: 2 de septiembre de 2025, vigentes desde el 3 de septiembre de 2025 (Diario El Mundo, 12 sep 2025, fuente secundaria; el numero de referencia "0309025" es consistente con la fecha 03-09-2025). El texto de las Politicas (Art. 9) dice que "entraran en vigencia a partir de su publicacion"; no se localizo el numero y tomo del Diario Oficial en que se publicaron, ni consta que se hayan publicado en el Diario Oficial. Fecha de emision y publicacion: PENDIENTE de verificacion en fuente primaria.
- Lineamientos para el Delegado y Normativa sancionadora de la ACE: dados el 24 de julio de 2026, publicados en el Diario Oficial N. 146, Tomo 452, del martes 11 de agosto de 2026, vigentes ocho dias despues (19 de agosto de 2026).

Regla de computo aplicada: plazos por meses "de fecha a fecha" y, si el ultimo dia es inhabil, se prorroga al primer dia habil siguiente (Art. 82 LPA, supletoria por Art. 62 LPDP).

| Plazo | Base | Computo | Fecha resultante | Estado al 2026-09-23 |
|---|---|---|---|---|
| Art. 60 inc. 1: ACE dicta politicas, medidas y guias | 3 meses desde la vigencia (23 nov 2024) | 23 nov 2024 + 3 meses | 23 feb 2025 (domingo; primer dia habil siguiente 24 feb 2025) | VENCIDO. La ACE incumplio: emitio las Politicas el 2 sep 2025, unos seis meses tarde. El incumplimiento de la ACE no suspendio las obligaciones de la ley, que estaban vigentes desde el 23 nov 2024 |
| Art. 60 inc. 2: sujetos obligados adecuan e implementan | 3 meses desde la emision de las disposiciones ACE | 2 sep 2025 + 3 meses (o 3 sep 2025 + 3 meses si se cuenta desde la vigencia de las Politicas) | 2 dic 2025 (o 3 dic 2025) | VENCIDO. No hay periodo de adecuacion vigente respecto de las Politicas |
| Art. 60 inc. 2 aplicado a los Lineamientos y Normativa de agosto 2026 (lectura alternativa: cada nueva disposicion abre tres meses de adecuacion) | 3 meses desde la emision (24 jul 2026), publicacion (11 ago 2026) o vigencia (19 ago 2026) | Segun el hito que se tome | 24 oct 2026, 11 nov 2026 o 19 nov 2026 | INCIERTO. Es una interpretacion posible pero no expresa; ademas el Decreto 659 (pendiente) deja sin objeto para el sector privado buena parte de los Lineamientos del Delegado. Requiere abogado |
| Art. 61 inc. 1: medidas ACE para datos obtenidos antes de la vigencia | Desde la vigencia (23 nov 2024), sin plazo propio; depende de las medidas ACE | Exigible desde que existen medidas ACE (3 sep 2025) | Exigible | VIGENTE Y EXIGIBLE. Los datos historicos (bases anteriores al 23 nov 2024) no estan exentos |
| Art. 61 inc. 2: mecanismos para que los titulares ejerzan derechos | 6 meses desde la vigencia | 23 nov 2024 + 6 meses | 23 may 2025 (viernes) | VENCIDO |
| Decreto 143 Art. 31: ACE emite normativas de ciberseguridad | 90 dias desde la vigencia (23 nov 2024) | 23 nov 2024 + 90 dias | 21 feb 2025 | VENCIDO (plazo para la ACE) |

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 60 inc. 2
**Obligacion:** Adecuar e implementar lo regulado en materia de proteccion de datos dentro de los tres meses siguientes a la emision de las disposiciones de la ACE.
**A quien aplica:** Todos los sujetos obligados (responsables y encargados, publicos y privados).
**Implicacion para el software:** El plazo esta vencido desde el 2 o 3 de diciembre de 2025: el producto no puede presentar la adecuacion como "pendiente de plazo" sino como "en mora". El plan de adecuacion debe arrancar con un diagnostico de brecha y priorizar lo que tiene sancion directa (aviso de privacidad, procedimientos ARCO-POL, medidas de seguridad de las Politicas, notificacion de vulneraciones). Si la ACE emite nuevas disposiciones, el software debe poder abrir un "periodo de adecuacion" configurable de tres meses desde la fecha de emision, con la advertencia de que su aplicabilidad es interpretativa.
**Fuente oficial:** ace_decreto_144.txt pags. 26 y 27; ace_politicas_protecciondatos.txt (Art. 9); https://diario.elmundo.sv/politica/vigentes-politicas-de-actuacion-y-manejo-de-datos-personales-en-el-salvador (fecha de emision, fuente secundaria). Consulta 2026-09-23.
**Vigencia:** VIGENTE (plazo vencido)
**Clasificacion:** OBLIGATORIO

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 61 inc. 1
**Obligacion:** Aplicar las medidas de proteccion que establezca la ACE a los datos personales obtenidos antes del 23 de noviembre de 2024.
**A quien aplica:** Todos los sujetos obligados.
**Implicacion para el software:** El inventario debe cubrir bases historicas ("legado") y no solo tratamientos nuevos; debe registrar para cada base la fecha de creacion y si sus datos fueron obtenidos antes de la vigencia, para documentar la aplicacion retroactiva de medidas de seguridad, sin exigir consentimiento retroactivo (la ley no lo pide expresamente; punto para abogado).
**Fuente oficial:** ace_decreto_144.txt pag. 27. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 61 inc. 2
**Obligacion:** Establecer mecanismos para que los titulares ejerzan sus derechos, dentro de seis meses desde la vigencia (vencio el 23 de mayo de 2025).
**A quien aplica:** Todos los sujetos obligados.
**Implicacion para el software:** El canal de recepcion de solicitudes ARCO-POL y de revocacion de consentimiento (Arts. 18, 24 lit. e y 29) debe estar operativo desde el primer dia de uso; su ausencia es hoy un incumplimiento consumado, y no atender solicitudes en tiempo y forma es infraccion grave (Art. 56 lit. b num. 2).
**Fuente oficial:** ace_decreto_144.txt pag. 27. Consulta 2026-09-23.
**Vigencia:** VIGENTE (plazo vencido)
**Clasificacion:** OBLIGATORIO

Diagrama de la linea de tiempo:

```
2024-11-12  Aprobacion D.L. 143 y 144
2024-11-14  Sancion
2024-11-15  Publicacion D.O. 219 Tomo 445
2024-11-23  Vigencia LPDP y Ley de Ciberseguridad
     |
     |-- +90 dias ----> 2025-02-21  limite ACE normativas ciberseguridad (Art. 31 D.143)
     |-- +3 meses ---> 2025-02-23  limite ACE politicas LPDP (Art. 60 inc.1)  [incumplido]
     |-- +6 meses ---> 2025-05-23  limite mecanismos ARCO-POL (Art. 61 inc.2) [vencido]
     |
2025-09-02  Emision Politicas ACE 001-0309025-DPDP (vigentes 2025-09-03, fuente secundaria)
     |-- +3 meses ---> 2025-12-02/03  limite adecuacion sujetos obligados (Art. 60 inc.2) [vencido]
     |
2026-02-24  D.L. 523 reforma LPA (Art. 4-A), D.O. 41 T.450 del 2026-02-27, vigente 2026-03-07
2026-06-19  D.L. 332 reforma Ley Especial contra Delitos Informaticos (no toca la LPDP)
2026-07-24  ACE emite Lineamientos Delegado y Normativa Sancionadora
2026-08-11  Publicacion D.O. 146 T.452 -> vigentes 2026-08-19
2026-09-12  ACE deja sin efecto la fecha limite de registro de delegados (2026-09-16) [fuente secundaria]
2026-09-17  D.L. 659 reforma LPDP (57 votos) -> PENDIENTE DE PUBLICACION al 2026-09-23
     |-- +8 dias desde publicacion en D.O. -> vigencia (fecha desconocida)
```

---

## 6. Reformas a la LPDP entre noviembre 2024 y septiembre 2026

### 6.1 Metodo de busqueda y evidencia

Se descargaron y analizaron los listados oficiales "Decretos emitidos por ano" del portal de la Asamblea Legislativa (https://www.asamblea.gob.sv/leyes-y-decretos/decretos-por-anios/{2024,2025,2026}/{0,1,2,3}), filtrando por titulo con las palabras "Datos Personales", "Ciberseguridad", "Procedimientos Administrativos" y "Delitos Informaticos":

| Ano | Decretos listados | Rango de fechas cubierto | Coincidencias |
|---|---|---|---|
| 2024 | 267 | 03/01/2024 a 23/12/2024 | D.L. 143 (12/11/2024) Ley de Ciberseguridad y Seguridad de la Informacion; D.L. 144 (12/11/2024) Ley para la Proteccion de Datos Personales. Ninguna reforma posterior en 2024 |
| 2025 | 302 | todo 2025 | D.L. 289 (30/04/2025) reforma a la Ley de Presupuesto 2025 para incorporar el presupuesto especial de la ACE por US$12,000,000; D.L. 332 (19/06/2025) Reformas a la Ley Especial contra los Delitos Informaticos y Conexos. Ninguna reforma a la LPDP |
| 2026 | 154 + 5 (pagina de recientes) | hasta 17/09/2026 | D.L. 523 (24/02/2026) Reforma a la Ley de Procedimientos Administrativos; D.L. 659 (17/09/2026) "Reformase la Ley para la Proteccion de Datos Personales" |

Ademas se consulto la ficha individual de cada decreto relevante (view/7022 para el 659, view/6779 para el 523) y las noticias oficiales de la Asamblea (node/14116). El buscador de decretos (busqueda-decretos) es un formulario dinamico que no devolvio resultados por URL; la pagina "ultimos-aprobados" tampoco lista contenido estatico. Con esa evidencia se afirma: no existe ninguna reforma a la LPDP distinta del Decreto 659 en el periodo noviembre 2024 a septiembre 2026. Tampoco existe reforma alguna a la Ley de Ciberseguridad (Decreto 143).

### 6.2 Decreto Legislativo N. 659 (17 de septiembre de 2026)

| Dato | Valor | Fuente |
|---|---|---|
| Titulo en el portal | "REFORMASE LA LEY PARA LA PROTECCION DE DATOS PERSONALES" | asamblea.gob.sv/leyes-y-decretos/view/7022 |
| Numero y fecha de emision | Decreto N. 659, 17/09/2026 | Idem |
| Estado en el portal al 2026-09-23 | "Pendiente de Publicacion Material en el Diario Oficial y de Entrada en Vigencia"; sin numero de Diario Oficial, tomo ni fecha de publicacion; sin documento adjunto | Idem (fuente primaria del estado) |
| Votacion | 57 votos a favor (Infobae agrega 1 en contra), con dispensa de tramites | asamblea.gob.sv/node/14116; eldiariodehoy.com; infobae.com (secundarias) |
| Iniciativa | Presidente de la Republica por medio del Ministro de Justicia y Seguridad Publica; ingreso formal 16/09/2026 | eldiariodehoy.com, infobae.com (secundarias) |
| Contenido reportado | Deroga Arts. 15 y 17 (delegado obligatorio y deber de asistencia al delegado); reforma Art. 16 (las funciones pasan a los "sujetos obligados", que deben auxiliar a sus dependencias o proveedores y fijar lineamientos internos para gestionar solicitudes ARCO-POL); reforma Art. 47 (instituciones publicas mantienen delegado, que puede ser el Oficial de Informacion); reforma Art. 51 (el Presidente nombra al Director de Proteccion de Datos Personales por tres anos). Las solicitudes ARCO-POL se presentan directamente ante la empresa. Se mantienen los plazos: 20 dias habiles prorrogables por 20, prevencion unica con 10 dias habiles para subsanar, devolucion por incompetencia en 5 dias habiles, notificacion a terceros de rectificacion o eliminacion en 5 dias habiles, denegatoria motivada en 3 dias habiles, revocacion de consentimiento en 5 dias habiles | eldiariodehoy.com/noticias/nacionales/asamblea-legislativa-deroga-obligatoriedad...; infobae.com/el-salvador/2026/09/17/...; asamblea.gob.sv/node/14116 (todas secundarias respecto del texto) |
| Vigencia prevista | Ocho dias despues de su publicacion en el Diario Oficial | Fuentes secundarias; consistente con la practica legislativa |
| Texto oficial | NO LOCALIZADO. No esta en el portal de la Asamblea ni en el Diario Oficial | Verificado 2026-09-23 |

**Norma:** Decreto Legislativo N. 659 (reforma a la LPDP)
**Articulo:** Arts. 15, 16, 17, 47 y 51 LPDP (segun fuentes secundarias)
**Obligacion:** Al entrar en vigencia, las empresas privadas dejaran de estar obligadas a nombrar delegado y asumiran directamente, como "sujetos obligados", las funciones de recibir, tramitar y resolver solicitudes ARCO-POL, auxiliar a sus dependencias y proveedores, y fijar lineamientos internos. Los plazos de respuesta no cambian.
**A quien aplica:** Sector privado (derogacion de la obligacion de delegado); sector publico (mantiene delegado).
**Implicacion para el software:** El rol "delegado" debe ser configurable y no un requisito bloqueante: el sistema debe permitir asignar las funciones del Art. 16 a una o varias personas internas ("responsable de solicitudes ARCO-POL") sin llamarlas delegado, y conservar el modo "delegado nombrado" para clientes que opten por mantenerlo voluntariamente o para entidades publicas. Todas las plantillas (aviso de privacidad Art. 24 lit. f, que hoy exige "nombre del delegado") deben tener version pre y post reforma con conmutacion por fecha de vigencia. Hasta que se publique, la ley vigente sigue exigiendo delegado (Art. 15), aunque la ACE dejo sin efecto la fecha limite de registro.
**Fuente oficial:** https://www.asamblea.gob.sv/leyes-y-decretos/view/7022 (estado); https://www.asamblea.gob.sv/node/14116 (nota oficial); prensa citada (contenido). Consulta 2026-09-23.
**Vigencia:** APROBADA-PENDIENTE-PUBLICACION
**Clasificacion:** CONDICIONAL (condicionada a la publicacion y transcurso de ocho dias; contenido exacto pendiente del texto oficial)

Hecho conexo (fuente secundaria): el 12 de septiembre de 2026 la ACE comunico que "queda sin efecto la fecha limite establecida para el nombramiento del delegado de proteccion de datos personales" (16 de septiembre de 2026, que resultaba de los veinte dias habiles del Art. 40 de los Lineamientos contados desde su vigencia) y que "no sera necesario realizar accion alguna al respecto por el momento" (elsalvador.com, 12 sep 2026; contrapunto.com.sv, 13 sep 2026). No se localizo el comunicado en ace.gob.sv.

### 6.3 Normas conexas reformadas en el periodo (no reforman la LPDP)

| Decreto | Fecha | Objeto | Publicacion y vigencia | Relevancia para PRIV-SV |
|---|---|---|---|---|
| D.L. 289 | 30/04/2025 | Reforma a la Ley de Presupuesto 2025: presupuesto especial de la ACE por US$12,000,000 | Listado Asamblea 2025 | Confirma la operatividad presupuestaria de la entidad rectora |
| D.L. 332 | 19/06/2025 | Reformas a la Ley Especial contra los Delitos Informaticos y Conexos | Segun Lexology (secundaria): D.O. 25 jun 2025, vigente 3 jul 2025 | Regimen penal paralelo (Art. 57 LPDP: "sin perjuicio de las responsabilidades penales"); segun la misma fuente, quienes custodian o procesan datos pueden ser reconocidos como sujetos afectados en fraudes informaticos. No verificado en fuente primaria |
| D.L. 523 | 24/02/2026 | Reforma a la LPA: nuevo Art. 4-A "Documentos emanados en el extranjero" | D.O. N. 41, Tomo 450, 27/02/2026; vigente 07/03/2026 (Art. 2: ocho dias) | La Administracion (incluida la ACE) no exigira legalizacion ni apostilla de documentos publicos extranjeros en operaciones comerciales o aduaneras, ni cuando pueda verificarlos electronicamente; en los demas casos admite el tramite y permite aportar la apostilla hasta antes de la resolucion definitiva, con resoluciones provisionales y plazo maximo de diez dias habiles. Relevante solo para clientes extranjeros que deban acreditar personeria ante la ACE |

---

## 7. Ley de Ciberseguridad y Seguridad de la Informacion (Decreto 143)

### 7.1 Identidad y estructura

| Dato | Valor | Fuente |
|---|---|---|
| Nombre | Ley de Ciberseguridad y Seguridad de la Informacion | asamblea_decreto_143_ciberseguridad.txt pag. 1 |
| Instrumento | Decreto Legislativo N. 143 | Idem |
| Aprobacion / sancion | 12 nov 2024 / 14 nov 2024 | Idem pag. 15 |
| Publicacion | D.O. N. 219, Tomo 445, 15 nov 2024, paginas 3 a 23 | diario_oficial_2024-11-15_mh.txt pag. 1 (sumario "3-23"); asamblea_decreto_143_ciberseguridad.txt pag. 16 (pie "D. O. N° 219 Tomo N° 445") |
| Vigencia | 23 nov 2024 (Art. 32: ocho dias despues de su publicacion) | Idem pag. 15 |
| Extension | 32 articulos en 4 capitulos: I Disposiciones generales (Arts. 1 a 6); II Agencia de Ciberseguridad del Estado (Arts. 7 a 16); III Infracciones, sanciones, procedimientos y recursos (Arts. 17 a 29); IV Disposiciones finales (Arts. 30 a 32) | Texto integro |
| Reformas | Ninguna localizada (listados Asamblea 2024 a 2026) | Seccion 6.1 |
| Nota sobre el corpus | Las paginas 3 a 23 del Diario Oficial no estan en el corpus local; se uso el texto de la Asamblea, cuyo pie de pagina identifica la misma publicacion | Verificado con pypdf: el PDF local tiene 40 paginas (indice + D.O. pags. 24 a 62) |

### 7.2 A quien aplica: el punto critico para el sector privado

"Art. 2.- Estan obligados al cumplimiento de esta ley los organos del Gobierno, sus dependencias, las instituciones oficiales autonomas, las autoridades municipales o cualquier otra entidad u organismo, independientemente de su forma, naturaleza o situacion juridica, mediante las cuales se administren recursos publicos, bienes del Estado, ejecuten actos de la administracion publica en general o que posean incidencia en las infraestructuras criticas de la nacion."

El Art. 1 confirma el objeto: regular, auditar y fiscalizar "las medidas de ciberseguridad y seguridad de la informacion en poder de las instituciones publicas". Las definiciones del Art. 4 lit. d) y g) delimitan "infraestructuras criticas" (sistemas, redes o servicios tecnologicos que soportan servicios esenciales) y "servicio esencial" (seguridad nacional, defensa, economia del pais, relaciones exteriores, orden publico, salud, bienestar y actividades sociales cruciales). La ACE "califica, mediante resolucion fundada, a los operadores de infraestructuras criticas, y lo somete a ratificacion del presidente" (Art. 8 lit. f) y puede retirar la calificacion (lit. g). No se localizo ninguna resolucion publica de calificacion de operadores privados (el presupuesto de busquedas web se agoto antes de poder confirmarlo; queda como pendiente).

Conclusion: para una empresa privada ordinaria (comercio, servicios, manufactura, salud privada, tecnologia) la Ley de Ciberseguridad NO impone obligaciones directas. Las impone solo si (a) administra recursos publicos o ejecuta actos de administracion publica (concesionarios, contratistas en ciertos casos) o (b) posee incidencia en infraestructuras criticas (energia, telecomunicaciones, agua, banca y pagos, salud, transporte), sobre todo si la ACE la califica como operador. Que la sancion de los Arts. 23 y 24 distinga expresamente al "infractor del sector privado" confirma que la ley preve sujetos privados.

**Norma:** Ley de Ciberseguridad y Seguridad de la Informacion (D.L. 143)
**Articulo:** Arts. 2, 4 lit. d) y g), 8 lit. f) y g)
**Obligacion:** Sujecion a la ley de las entidades privadas que administren recursos publicos, ejecuten actos de administracion publica o posean incidencia en infraestructuras criticas; calificacion de operadores por la ACE.
**A quien aplica:** Empresas privadas en sectores de servicios esenciales o contratistas del Estado; no a la generalidad del sector privado.
**Implicacion para el software:** Incluir en el perfil del cliente una pregunta de calificacion ("opera infraestructura critica o ha sido calificada por la ACE como operador") que active un modulo complementario de obligaciones del Art. 6; por defecto ese modulo esta apagado y el software explica por que.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\asamblea_decreto_143_ciberseguridad.txt pags. 2, 3, 4 y 7 (https://www.asamblea.gob.sv/sites/default/files/documents/decretos/D056D9A1-299D-4188-941A-9C3B5898D3F3.pdf). Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

### 7.3 Obligaciones para los sujetos obligados (Art. 6) que un privado calificado tendria que cumplir

"Art. 6.- Los sujetos a quienes aplique la presente ley de conformidad con el Art. 2, tendran las obligaciones siguientes:
a) Implementar un sistema de gestion de ciberseguridad y seguridad de la informacion permanente...
b) Elaborar una estrategia de seguridad informatica y de la informacion apegado a estandares o marcos de referencia nacionales e internacionales.
c) Mantener un registro actualizado de todas las acciones ejecutadas que compongan el sistema de gestion...
d) Elaborar e implementar planes de continuidad operacional y ciberseguridad, los cuales deberan ser aprobados por la autoridad competente y se someteran a revisiones periodicas...
e) Realizar continuamente operaciones de revision, ejercicios, simulacros y analisis...
f) Aplicar y cumplir de manera inmediata y eficaz las medidas necesarias para prevenir, reportar y resolver las amenazas...
g) Adoptar de forma oportuna, expedita y eficiente las acciones necesarias para reducir el impacto y la propagacion de un incidente...
h) Remitir en el tiempo, forma y especificidad los informes relacionados con la ciberseguridad y seguridad de la informacion que le sean exigidos por la autoridad competente.
i) Crear o designar un area o areas responsables para la implementacion, seguimiento, revision y adecuacion de las acciones y medidas... otorgandoles internamente independencia y atribuciones necesarias...
j) Cumplir con los requerimientos de informacion o instrucciones que realice la autoridad competente...
k) Facilitar las labores de gestion, auditoria e inspeccion que realice la autoridad competente...
l) Informar a los potenciales afectados, en la medida que puedan identificarse y cuando asi lo determine la Agencia de Ciberseguridad del Estado, sobre la ocurrencia de incidentes que pudieran comprometer o comprometan gravemente su informacion, asi como las posibles medidas que pueden adoptar para mitigar los riesgos...
m) Realizar las planificaciones, gestiones y tramites necesarios para implementar las obligaciones...
n) Las demas que establecieran las disposiciones contenidas en politicas, normativas, protocolos, lineamientos, estandares y criterios tecnicos..."

**Norma:** Ley de Ciberseguridad y Seguridad de la Informacion (D.L. 143)
**Articulo:** Art. 6 lit. a) a n); Art. 8 lit. e) y h)
**Obligacion:** Sistema de gestion de ciberseguridad permanente, estrategia alineada a marcos de referencia, registro actualizado de acciones, planes de continuidad aprobados por la ACE, ejercicios y simulacros, prevencion y reporte de amenazas e incidentes, area responsable con independencia, informes a la ACE en tiempo y forma, informar a los afectados cuando la ACE lo determine. La ACE administra un "Registro Nacional de Amenazas e Incidentes de Ciberseguridad" (Art. 8 lit. e) y puede requerir a la entidad afectada que entregue informacion veraz, suficiente y oportuna a afectados y autoridades (Art. 8 lit. h). La ley no fija un plazo en horas para el reporte de incidentes de los sujetos obligados: lo remite a las disposiciones tecnicas de la ACE ("en el tiempo, forma y especificidad", lit. h). El unico plazo de 72 horas del Decreto 143 es el de la propia ACE para dar aviso a la Fiscalia cuando advierta posibles delitos (Art. 8 lit. v).
**A quien aplica:** Solo los sujetos del Art. 2 (sector publico y privados con incidencia en infraestructuras criticas).
**Implicacion para el software:** Para clientes calificados, un modulo "ciberseguridad D.143" con: registro de acciones del sistema de gestion (lit. c), calendario de simulacros (lit. e), plan de continuidad con fecha de aprobacion ACE (lit. d), area responsable designada (lit. i), bitacora de requerimientos ACE (lit. h y j) y flujo de comunicacion a afectados (lit. l). Para todos los clientes, el flujo de incidentes debe distinguir el reporte LPDP Art. 25 (72 horas a ACE, FGR y titulares, obligatorio para todo responsable) del reporte D.143 (solo sujetos calificados, plazos segun normativa ACE, no localizada). No se encontro la normativa tecnica de la ACE sobre reporte de incidentes; el sitio ace.gob.sv enlaza un documento "politicas_ciberseguridad.pdf" que devolvio error 404.
**Fuente oficial:** asamblea_decreto_143_ciberseguridad.txt pags. 5 a 8. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

### 7.4 Infracciones y sanciones propias del Decreto 143 (solo para sus sujetos)

| Categoria | Ejemplos (Arts. 19 a 21) | Sancion (Arts. 22 a 24) |
|---|---|---|
| Leves | Remitir informes fuera de plazo o sin especificaciones cuando no se relacionen con incidentes; incumplir politicas o lineamientos sin incidencia en el sistema de gestion o en incidentes | Amonestacion escrita o multa de 1 a 10 salarios minimos mensuales del sector comercio (Art. 22) |
| Graves | No llevar registro actualizado; no elaborar o no implementar planes de continuidad; no realizar simulacros; incumplir lineamientos relacionados con el sistema de gestion o la gestion de incidentes; obstaculizar al area responsable; presentar informacion incompleta o inexacta | Sector publico: despido o destitucion mas multa de 11 a 50 salarios minimos; sector privado: multa de 11 a 50 salarios minimos (Art. 23) |
| Muy graves | Informes sobre incidentes fuera de plazo o sin especificaciones; no implementar el sistema de gestion; no prevenir, reportar y resolver amenazas; no reducir impacto de incidentes; no designar area responsable; obstaculizar auditorias; no informar a afectados cuando la ACE lo determine; incumplir ordenes de prohibicion de uso de sistemas | Sector publico: despido o destitucion mas multa de 51 a 100 salarios minimos; sector privado: multa de 51 a 100 salarios minimos (Art. 24; el texto dice por error "Las infracciones graves" en su primera linea) |
| Coercitiva | Para lograr la ejecucion de sus actos, la ACE puede imponer multas coercitivas de 1 a 10 salarios minimos del sector comercio por cada dia habil de incumplimiento, compatibles con las demas sanciones (Art. 27) | Aplica a los sujetos del D.143; su aplicacion a infracciones LPDP no esta prevista expresamente en el Art. 53 LPDP (ver seccion 10) |

Estas multas del Decreto 143 no sustituyen las de la LPDP: las infracciones de datos personales se sancionan con las multas del Art. 57 LPDP (leves 1 a 10, graves 11 a 25, muy graves 26 a 40 salarios minimos mensuales del sector comercio). Tambien responden los titulares, la alta direccion y cualquier funcionario o empleado cuando la infraccion se materialice por su orden, instruccion, negligencia u omision (Arts. 19 a 21, inciso final de cada uno).

### 7.5 Reglas de procedimiento sancionador y prescripcion que aplican a la LPDP por remision del Art. 53

"Art. 53 (LPDP).- Para el ejercicio de potestad sancionadora, el desarrollo del procedimiento y las reglas de prescripcion de las infracciones y sanciones contemplada en la presente ley se aplicara lo dispuesto en la Ley de Ciberseguridad y Seguridad de la Informacion."

Lo que el Decreto 143 aporta:

"Art. 17.- ... A las infracciones y sanciones que se impongan en virtud de la presente ley le seran aplicables los principios de la potestad sancionadora previstos en la Ley de Procedimientos Administrativos; especialmente el de proporcionalidad..."

"Art. 28.- El procedimiento para la determinacion de las infracciones y sanciones que establece la presente ley debera realizarse de conformidad con el procedimiento simplificado contemplado en la Ley de Procedimientos Administrativos. El procedimiento podra iniciarse de oficio, por aviso, por denuncia o por cualquier otro medio. Cuando la informacion sobre la presunta comision de la infraccion se recibiera de forma verbal o de tal manera que no hubiera un respaldo escrito de la misma, la Agencia levantara un acta..."

"Art. 29.- Las infracciones y sanciones contempladas en la presente ley prescribiran a los cinco anos."

"Art. 30.- ... En todo lo no previsto, se aplicara supletoriamente lo dispuesto en la Ley de Procedimientos Administrativos."

Cadena de remisiones:

```
LPDP Art. 53 (potestad sancionadora, procedimiento, prescripcion)
   |
   v
D.143 Art. 17 (principios LPA) -> Art. 28 (procedimiento simplificado LPA) -> Art. 29 (prescripcion 5 anos)
   |                                        |
   |                                        v
   |                              LPA Art. 158 (simplificado: 5 dias alegatos, 15 dias resolucion, sin recurso)
   |                              LPA Arts. 139 a 157 (principios, derechos, autoria, computo de prescripcion Art. 149)
   v
ACE Normativa PAS (D.O. 146 T.452, 11 ago 2026): Art. 4 simplificado / excepcionalmente ordinario,
   Arts. 7 a 12 diligencias preliminares (hasta 90 dias habiles), Art. 19 y 21 emplazamiento y
   contestacion 5 dias habiles, Art. 32 resolucion 15 dias habiles, Art. 33 recursos solo en via
   ordinaria, Art. 35 medidas provisionales previas (confirmar en 15 dias calendario),
   Art. 44 pago de multa 15 dias habiles, Art. 47 prescripcion 5 anos con computo del Art. 149 LPA
   |
   v
LPDP Art. 62 y D.143 Art. 30: LPA supletoria en todo lo no previsto
```

**Norma:** Ley de Ciberseguridad y Seguridad de la Informacion (D.L. 143), por remision del Art. 53 LPDP
**Articulo:** Art. 29 D.143; Art. 47 Normativa PAS ACE; Art. 149 LPA
**Obligacion:** Las infracciones y sanciones de la LPDP prescriben a los cinco anos. El computo (Art. 149 LPA) corre desde el dia siguiente a la comision; en infracciones continuadas o permanentes desde el ultimo hecho o desde que se elimino la situacion ilicita; se interrumpe con la iniciacion del procedimiento con conocimiento del presunto responsable y se reanuda por el plazo integro tras un mes de paralizacion no imputable a este; la prescripcion de la sancion corre desde la firmeza en via administrativa.
**A quien aplica:** Todos los sujetos obligados por la LPDP.
**Implicacion para el software:** Politica minima de retencion de evidencias de cumplimiento de cinco anos desde el ultimo acto relevante (y mas, si el tratamiento es continuado, porque el plazo no empieza a correr mientras persista la situacion). Las bitacoras de consentimiento, avisos, solicitudes ARCO-POL, incidentes y contratos no deben poder purgarse antes de ese horizonte. Este plazo desplaza los plazos por defecto del Art. 148 LPA (3, 2 anos y 6 meses).
**Fuente oficial:** asamblea_decreto_143_ciberseguridad.txt pags. 14 y 15; normativa_sancionadora_OCR.txt pag. 9 (verificado contra ocr/normativa_sancionadora/page-09.png); asamblea_decreto_856_lpa.txt (Art. 149). Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (regla de prescripcion) y RECOMENDADO (retencion de evidencia de cinco anos como buena practica derivada)

**Norma:** Ley de Ciberseguridad y Seguridad de la Informacion (D.L. 143) y Normativa PAS de la ACE
**Articulo:** Art. 28 D.143; Arts. 4, 6, 19, 21, 23, 29 a 33 Normativa PAS; Art. 158 LPA
**Obligacion:** El procedimiento sancionador por infracciones a la LPDP se tramita por el procedimiento simplificado de la LPA y, excepcionalmente, por el ordinario. Etapas: resolucion de inicio, contestacion, termino de prueba y resolucion final (mas alegatos finales en via ordinaria). Emplazamiento personal con cinco dias habiles para contestar, alegar y proponer prueba; si no comparece, se tienen por contestados negativamente los hechos y el procedimiento sigue. Resolucion final en quince dias habiles desde la recepcion del expediente. En via simplificada no hay recurso administrativo y queda abierta la via contencioso administrativa; en via ordinaria caben reconsideracion, apelacion y revision segun la LPA. Puede haber diligencias preliminares de investigacion de hasta noventa dias habiles antes del procedimiento, iniciadas de oficio, por denuncia, a solicitud del propio sujeto obligado tras un incidente, o de forma preventiva con base en riesgos.
**A quien aplica:** Todos los sujetos obligados por la LPDP.
**Implicacion para el software:** Modulo "requerimientos y procedimientos ACE" con: registro de la fecha y medio de notificacion, calculo automatico del vencimiento de cinco dias habiles para contestar, checklist de contestacion (alegatos, documentos, proposicion de prueba, senalamiento de medio electronico de notificacion), alerta de que la ausencia de respuesta equivale a negativa ficta con continuacion del proceso, registro de la via (simplificada u ordinaria) para saber si hay recursos, y generacion del expediente probatorio desde la evidencia ya almacenada. Tambien debe permitir documentar la solicitud voluntaria de diligencias preliminares tras un incidente (Art. 8 lit. c Normativa).
**Fuente oficial:** asamblea_decreto_143_ciberseguridad.txt pag. 14; normativa_sancionadora_OCR.txt pags. 3 a 8 (verificado contra ocr/normativa_sancionadora/page-03.png y page-08.png); asamblea_decreto_856_lpa.txt (Art. 158). Consulta 2026-09-23.
**Vigencia:** VIGENTE (Normativa PAS vigente desde el 19 de agosto de 2026)
**Clasificacion:** CONDICIONAL (aplica cuando la empresa es objeto de investigacion o procedimiento)

**Norma:** Normativa para el Desarrollo del Procedimiento Administrativo Sancionador (ACE), con LPDP Art. 57 y LPA
**Articulo:** Arts. 43 a 45 Normativa PAS
**Obligacion:** Criterios de graduacion de la multa: gravedad del dano o peligro, efecto disuasivo, duracion de la conducta, caracter intencional o negligente, naturaleza o categoria de los datos afectados y capacidad economica del infractor. Pago de la multa en la Colecturia Central o regionales de la Direccion General de Tesoreria dentro de los quince dias habiles siguientes a la notificacion; si no se paga, la Fiscalia la cobra por via ejecutiva con la certificacion de la resolucion.
**A quien aplica:** Sujetos sancionados.
**Implicacion para el software:** Los criterios de graduacion son la lista de "atenuantes documentables": duracion corta (deteccion temprana), ausencia de intencionalidad, categoria no sensible, y medidas correctivas inmediatas; el software debe ayudar a evidenciarlos. Ademas, la aceptacion expresa de los hechos permite reducir hasta una cuarta parte la multa (Art. 156 LPA). Alerta de pago a quince dias habiles.
**Fuente oficial:** normativa_sancionadora_OCR.txt pag. 9; asamblea_decreto_856_lpa.txt (Art. 156). Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

### 7.6 Otras relaciones entre ambas leyes

| Vinculo | LPDP | Decreto 143 | Efecto |
|---|---|---|---|
| Entidad rectora | Art. 50: la ACE aplica y supervisa la LPDP | Art. 7: crea la ACE como dependencia de derecho publico con personalidad juridica, autonomia administrativa y financiera; Art. 9: Director General nombrado por el Presidente por tres anos prorrogables | Una sola autoridad para ambas materias; la ACE es tambien autoridad tecnica de ciberseguridad del Estado |
| Director de Proteccion de Datos | Art. 51: nombrado para asistir al Director General; conoce los procedimientos sancionadores y puede delegar instruccion, no la sancion; Art. 52: requisitos | Arts. 11 y 12: impedimentos, incompatibilidades y cesacion (aplicables por remision del Art. 52 inc. final LPDP) | El Decreto 659 reformaria el Art. 51 para que lo nombre el Presidente por tres anos (fuente secundaria) |
| Medidas provisionales | Art. 50 lit. c): dictar, modificar o anular medidas provisionales segun la LPA | Art. 8 lit. q): identica atribucion | Ver seccion 8 |
| Confidencialidad de la ACE | Art. 50 lit. t): puede requerir antecedentes, documentos y programas garantizando confidencialidad | Art. 16: secreto de funcionarios de la ACE, incluso cinco anos despues de cesar | Base para entregar informacion sensible a la ACE en inspecciones |
| Anonimizacion en gestion de incidentes | Art. 4 lit. h) | Art. 8 lit. j): al requerir informacion para gestionar incidentes, los datos personales deben tratarse con el proposito de anonimizar a sus titulares siempre que sea posible | Los reportes de incidentes a la ACE deben minimizar datos personales |
| Aviso a la Fiscalia | Art. 25: el responsable notifica a la FGR en 72 horas | Art. 8 lit. v): la ACE avisa a la FGR en 72 horas cuando advierta posibles delitos informaticos; Normativa PAS Art. 34: aviso en 72 horas tras la resolucion sancionadora | Doble canal hacia la FGR: el de la empresa (Art. 25) y el de la ACE |
| Sanciones penales | Art. 57: multas "sin perjuicio de las responsabilidades penales" | Art. 17: sanciones administrativas sin perjuicio de responsabilidades civiles, penales o de otro orden | Coexistencia con la Ley Especial contra los Delitos Informaticos y Conexos (reformada por D.L. 332 de 2025) |

---

## 8. Ley de Procedimientos Administrativos como supletoria (Art. 62 LPDP)

### 8.1 Identidad

| Dato | Valor | Fuente |
|---|---|---|
| Norma | Ley de Procedimientos Administrativos (LPA) | asamblea_decreto_856_lpa.txt pag. 1 |
| Instrumento | Decreto Legislativo N. 856, 15 de diciembre de 2017 (devuelto con observaciones por el Presidente el 9 ene 2018, aceptadas parcialmente el 30 ene 2018) | Idem pags. 53 y 54 |
| Publicacion | D.O. N. 30, Tomo 418, 13 de febrero de 2018 | Idem pag. 54 |
| Vigencia | 13 de febrero de 2019 (Art. 168: doce meses despues de su publicacion) | Idem |
| Extension | 168 articulos en 7 titulos | Indice del texto |
| Reforma reciente | D.L. 523 (24 feb 2026, D.O. 41 T.450 de 27 feb 2026, vigente 7 mar 2026): nuevo Art. 4-A sobre documentos emanados en el extranjero | asamblea_decreto_523_reforma_lpa.txt |
| Advertencia | El texto usado es la version publicada por la Asamblea con fecha de indice 23-03-2018; la numeracion citada coincide con las remisiones que hace la ACE en su Normativa PAS (Arts. 90, 94, 98, 149, 158 y 159), lo que corrobora que la numeracion no ha cambiado. Pueden existir otras reformas puntuales no relevantes para este lente (por ejemplo la armonizacion con la Ley Crecer Juntos, noticia asamblea.gob.sv/node/12249, no verificada) | - |

Remisiones expresas de la LPDP y del Decreto 143 a la LPA: Art. 50 lit. c) LPDP (medidas provisionales), Art. 62 LPDP (supletoria general), Art. 17 D.143 (principios sancionadores), Art. 28 D.143 (procedimiento simplificado), Art. 30 D.143 (supletoria), Art. 8 lit. q) D.143 (medidas provisionales). La ACE, a su vez, dicta sus lineamientos y normativas invocando el Art. 159 LPA (potestad normativa) junto con el Art. 60 LPDP.

### 8.2 Computo de plazos (Arts. 80 a 90 LPA)

**Norma:** Ley de Procedimientos Administrativos (D.L. 856), supletoria por Art. 62 LPDP
**Articulo:** Arts. 80, 81, 82, 83
**Obligacion:** Los terminos y plazos son "obligatorios y perentorios para la Administracion y para los particulares" (Art. 80). Los actos se realizan en dias y horas habiles, salvo habilitacion motivada por urgencia (Art. 81). "Si los plazos se senalan por dias u horas, se computaran unicamente los dias y horas habiles"; el plazo en dias "se contara a partir del dia siguiente a aquel en que tenga lugar la notificacion o publicacion del acto"; los plazos por meses o anos se computan de fecha a fecha, y si no hay dia equivalente el plazo expira el ultimo dia del mes; "Cuando el ultimo dia del plazo sea inhabil, se entendera prorrogado al primer dia habil siguiente" (Art. 82). La Administracion debe expresar en sus resoluciones el plazo, la fecha de vencimiento y las consecuencias del incumplimiento (Art. 82 inc. 2). Prorroga: la Administracion puede ampliar plazos legales hasta la mitad del tiempo, de oficio o a peticion presentada antes del vencimiento, nunca para el plazo de conclusion ni para interponer recursos (Art. 83).
**A quien aplica:** A la ACE y a los administrados en todo procedimiento; por analogia, es la regla de computo mas segura para los plazos en "dias habiles" que la LPDP impone a las empresas (Arts. 9, 18, 19, 20, 21, 22 y 30), a falta de regla propia en la LPDP.
**Implicacion para el software:** Motor de plazos con calendario de dias habiles administrativos de El Salvador (fines de semana y asuetos nacionales, mas asuetos locales configurables), inicio del computo el dia siguiente a la recepcion o notificacion, y corrimiento al siguiente dia habil cuando el vencimiento cae en inhabil. Las prorrogas del Art. 20 LPDP (hasta otros veinte dias habiles "por causas justificadas") deben registrarse con su motivacion antes del vencimiento del plazo original. El plazo de 72 horas del Art. 25 LPDP se expresa en horas: la lectura literal del Art. 82 ("dias y horas habiles") abre la duda de si son horas corridas o habiles; se recomienda computar horas corridas como criterio conservador y senalar el punto al abogado.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\asamblea_decreto_856_lpa.txt pags. 25 y 26 (https://www.asamblea.gob.sv/sites/default/files/documents/decretos/361DDB77-97E7-4EFF-B353-C6D872547E7C.pdf). Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (en procedimientos ante la ACE); RECOMENDADO (como regla de computo de los plazos internos de la LPDP, hasta que la ACE o un abogado confirme)

Otros plazos de la LPA utiles para modelar la relacion con la ACE:

| Regla | Articulo | Plazo |
|---|---|---|
| Actos de mero tramite de la Administracion | Art. 86 num. 1 | 5 dias |
| Dictamenes, peritajes e informes tecnicos | Art. 86 num. 2 | 20 dias, ampliables por otros 20 |
| Informes administrativos no tecnicos | Art. 86 num. 3 | 15 dias |
| Tramites a cargo del interesado (regla general) | Art. 88 | 10 dias, ampliables por otros 10 de forma fundamentada |
| Conclusion del procedimiento | Art. 89 | 9 meses maximo desde su inicio, salvo ley especial; 20 dias si solo requiere el escrito de peticion |
| Suspension del plazo para resolver | Art. 90 | Por requerimiento de subsanacion; informes preceptivos (maximo 2 meses); pruebas tecnicas (maximo 2 meses); actuaciones complementarias. La Normativa PAS (Art. 39) remite a este articulo |
| Suspension del procedimiento | Art. 94 | Caso fortuito o fuerza mayor, con resolucion motivada. La Normativa PAS (Art. 40) remite a este articulo |
| Reposicion de actuaciones por fuerza mayor | Art. 85 | Solicitud dentro de 5 dias desde que ceso la causa |

### 8.3 Notificaciones (Arts. 97 a 104 LPA)

**Norma:** Ley de Procedimientos Administrativos (D.L. 856), supletoria
**Articulo:** Arts. 97, 98, 99, 100, 101, 102, 104
**Obligacion:** Todo acto que afecte derechos debe notificarse dentro de tres dias desde que se dicta, con el texto integro y sus anexos (Art. 97). Puede practicarse "por cualquier medio que permita tener constancia de la recepcion", incluido correo postal con acuse; en el domicilio puede recibirla cualquier mayor de edad; si nadie la recibe o se rechaza, se fija aviso y, si no acude en tres dias, se tiene por notificado (Art. 98). En su primer escrito el interesado "debera senalar el medio electronico o direccion postal para recibir las sucesivas notificaciones" (Art. 99). Si no se senala medio o no se localiza al destinatario procede la notificacion por tablero, previa resolucion motivada (Art. 100). La notificacion electronica se acredita con constancia escrita anexada al expediente (Art. 101). La notificacion defectuosa es nula salvo que el interesado se de por enterado (Art. 102). El texto notificado debe indicar si cabe recurso, cual, plazo, lugar y autoridad (Art. 104). La Normativa PAS anade el emplazamiento personal a la persona juridica por medio de su representante o apoderado en su sede, o por esquela a cualquier empleado presente (Art. 19), y la notificacion por edicto en un diario de circulacion nacional cuando ningun medio funcione (Art. 20).
**A quien aplica:** ACE y empresas en cualquier procedimiento (investigacion preliminar, requerimiento, sancionador).
**Implicacion para el software:** (1) Registrar y mantener actualizados los datos de contacto formal de la empresa ante la ACE (sede, representante legal, apoderado, correo institucional designado) porque la ACE buscara "la direccion de sus oficinas principales registradas en la base de datos de la Agencia" (Art. 19 Normativa). (2) Bandeja de "notificaciones recibidas" con fecha y hora de recepcion, medio, receptor y adjuntos, que dispara el computo de plazos. (3) Recordatorio de que cualquier empleado presente puede recibir validamente un emplazamiento: procedimiento interno de escalamiento inmediato. (4) Advertencia de que un correo designado no atendido no detiene los plazos.
**Fuente oficial:** asamblea_decreto_856_lpa.txt pags. 29 a 31; normativa_sancionadora_OCR.txt pags. 5 y 6. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (en procedimientos ante la ACE)

### 8.4 Medidas provisionales (Arts. 78 y 152 LPA; Arts. 35 y 36 Normativa PAS)

**Norma:** Ley de Procedimientos Administrativos (D.L. 856), por remision de los Arts. 50 lit. c) LPDP y 8 lit. q) D.143
**Articulo:** Arts. 78 y 152 LPA; Arts. 35 a 38 Normativa PAS
**Obligacion:** Iniciado el procedimiento, el organo competente puede adoptar medidas provisionales para asegurar la eficacia de la resolucion "siempre que exista apariencia de buen derecho y peligro, lesion o frustracion por demora"; no pueden causar perjuicios de imposible o dificil reparacion; pueden modificarse o levantarse y se extinguen con la resolucion final. Antes del procedimiento tambien pueden adoptarse, pero deben confirmarse, modificarse o levantarse al iniciarlo "dentro de los quince dias siguientes a su adopcion", y caducan si no se inicia (Art. 78). En materia sancionadora, en cualquier momento, por resolucion motivada, "para asegurar la eficacia de la resolucion, el buen fin del procedimiento, el cese de los efectos de la infraccion y las exigencias de los intereses generales" (Art. 152). La Normativa PAS (Art. 35) faculta al Director de Proteccion de Datos o su delegado a dictarlas "en caso de urgencia o riesgo grave" antes y durante el procedimiento, con confirmacion en el auto de inicio dentro de quince dias calendario. Tras la sancion, la ACE puede ordenar medidas adicionales para restablecer la legalidad y les da seguimiento con requerimientos, inspecciones o auditorias (Arts. 37 y 38 Normativa; Art. 58 LPDP).
**A quien aplica:** Empresas objeto de investigacion o procedimiento.
**Implicacion para el software:** Estado "medida provisional vigente" sobre un tratamiento o base de datos (por ejemplo suspension de un tratamiento, bloqueo de una base, prohibicion de transferir), con fecha de adopcion, plazo de quince dias para verificar que la ACE inicio el procedimiento y la confirmo, y registro de cumplimiento; estado "medida adicional ordenada" post sancion con plan de cumplimiento y evidencia para inspecciones de seguimiento.
**Fuente oficial:** asamblea_decreto_856_lpa.txt pags. 24, 25 y 47; normativa_sancionadora_OCR.txt pag. 8 (verificado contra ocr/normativa_sancionadora/page-08.png). Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

### 8.5 Recursos (Arts. 123 a 138 LPA; Arts. 32 y 33 Normativa PAS)

**Norma:** Ley de Procedimientos Administrativos (D.L. 856), supletoria
**Articulo:** Arts. 124, 127, 131, 132 a 138 LPA; Arts. 32 inc. 3 y 33 Normativa PAS; Art. 158 num. 5 LPA
**Obligacion:** En la via simplificada (la regla en materia LPDP) "no habra recurso alguno y quedara habilitada la via contencioso-administrativa" (Art. 32 Normativa; Art. 158 num. 5 LPA). Solo si el procedimiento se tramito por la via ordinaria caben: reconsideracion (potestativo, ante el mismo organo, 10 dias desde la notificacion, resolucion en un mes, Arts. 132 y 133); apelacion (preceptivo para acceder a la jurisdiccion contencioso administrativa, ante el superior jerarquico u organo que determine la ley, 15 dias desde la notificacion, admision en 5 dias, prueba 5 dias, resolucion en un mes, Arts. 134 y 135); revision extraordinaria contra actos firmes (error de hecho: un ano; documentos esenciales: tres meses desde su descubrimiento; falsedad o cohecho declarados judicialmente: un ano, Arts. 136 a 138). La interposicion de recursos no suspende la ejecucion, salvo que la apelacion contra actos que ordenan pagos liquidos o imponen sanciones si suspende sus efectos (Art. 127 inc. final). El error en la calificacion del recurso no impide su tramite (Art. 125). La resolucion del recurso no puede agravar la situacion del recurrente (Art. 129).
**A quien aplica:** Empresas sancionadas.
**Implicacion para el software:** Al registrar una resolucion final de la ACE, el sistema debe (1) capturar la via del procedimiento, (2) si es ordinaria, calcular los vencimientos de 10 dias (reconsideracion) y 15 dias (apelacion) habiles desde el dia siguiente a la notificacion y advertir que la apelacion suspende la ejecucion de la multa; (3) si es simplificada, indicar que no hay recurso administrativo y que la impugnacion es judicial (contencioso administrativa, con plazo propio de la Ley de la Jurisdiccion Contencioso Administrativa, no analizada aqui); (4) en todo caso, escalar a asesoria juridica externa. El software no decide si recurrir.
**Fuente oficial:** asamblea_decreto_856_lpa.txt pags. 38 a 43 y 49; normativa_sancionadora_OCR.txt pag. 8 (verificado contra imagen). Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

### 8.6 Procedimiento simplificado y otras reglas sancionadoras (Arts. 139 a 158 LPA)

**Norma:** Ley de Procedimientos Administrativos (D.L. 856), por remision del Art. 28 D.143 y Art. 53 LPDP
**Articulo:** Arts. 139, 140, 142, 145, 151, 156, 157 y 158 LPA
**Obligacion:** Principios: reserva de ley, tipicidad (los reglamentos pueden especificar pero no crear infracciones ni sanciones), irretroactividad, presuncion de inocencia, responsabilidad a titulo de dolo o culpa, prohibicion de doble sancion y proporcionalidad (Art. 139). Derechos del presunto responsable: ser informado de hechos, infracciones y sanciones posibles, alegar y probar, no declarar contra si mismo (Art. 140). Cuando el responsable es persona juridica, el juicio de culpabilidad se hace respecto de las personas fisicas que formaron su voluntad, sin sancionarlas por separado (Art. 142). Non bis in idem con la via penal, y deber de comunicar a la FGR hechos que puedan ser delito (Art. 145). El auto de inicio contiene identificacion, hechos, calificacion preliminar y sancion posible, y derecho a alegar (Art. 151). Aceptacion expresa y escrita de responsabilidad: atenuante, con reduccion de hasta una cuarta parte de la multa (Art. 156). Apercibimiento en lugar de sancion para infracciones leves de primer infractor, solo "siempre que una Ley lo autorice" (Art. 157): la LPDP no lo autoriza expresamente. Procedimiento simplificado: resolucion de inicio notificada; cinco dias para actuaciones preliminares, alegaciones, documentos y proposicion de prueba; practica de prueba; resolucion definitiva en quince dias desde la ultima actuacion; posible conversion a ordinario con cinco dias para alegar; sin recurso, via contencioso administrativa (Art. 158).
**A quien aplica:** Empresas investigadas o sancionadas por la ACE.
**Implicacion para el software:** Ademas de lo indicado en 7.5: (1) registro de decisiones internas con nombre de quien decide, porque la culpabilidad de la persona juridica se juzga por las personas fisicas que formaron su voluntad; (2) opcion documentada de "aceptacion de hechos" con calculo orientativo de la reduccion maxima de un cuarto (sin recomendar la decision); (3) advertencia de que no existe apercibimiento previo garantizado para leves.
**Fuente oficial:** asamblea_decreto_856_lpa.txt pags. 43 a 49. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

### 8.7 Potestad normativa de la ACE (Arts. 159 a 162 LPA) y sus limites

**Norma:** Ley de Procedimientos Administrativos (D.L. 856)
**Articulo:** Arts. 159, 160, 161 y 162 LPA, con Arts. 35, 50 lit. i) y n) y 60 LPDP
**Obligacion:** La ACE ejerce potestad normativa (politicas, lineamientos, normativas) bajo las reglas de la LPA: principios de necesidad, eficacia, proporcionalidad, seguridad juridica, participacion ciudadana y transparencia (Art. 160); sujecion a la Constitucion y las leyes, funcion de desarrollo o colaboracion con la ley, prohibicion de tipificar infracciones o sanciones, y Evaluacion de Impacto Regulatorio previa (Art. 161); procedimiento de aprobacion con consulta (Art. 162). Las Politicas de Actuacion "seran imperativas a los sujetos obligados" (Art. 35 LPDP) y no cumplirlas es infraccion grave (Art. 56 lit. b num. 5 y 7 LPDP).
**A quien aplica:** ACE (como emisora) y sujetos obligados (como destinatarios).
**Implicacion para el software:** El catalogo de obligaciones debe distinguir tres niveles con etiqueta visible: ley (LPDP, D.143, LPA), normativa o lineamiento ACE (imperativos por Art. 35 LPDP, pero que no pueden crear infracciones nuevas) y buena practica (ISO 27001 y similares referidas en las Politicas). Cada obligacion de nivel ACE debe enlazar a la infraccion legal que la respalda (normalmente Art. 56 lit. b num. 5 o 7). Debe existir un proceso de "vigilancia normativa" para incorporar nuevas disposiciones ACE con su fecha de emision, publicacion y vigencia.
**Fuente oficial:** asamblea_decreto_856_lpa.txt pags. 49 a 51; ace_decreto_144.txt pags. 17, 22 y 26. Consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (imperatividad de las politicas ACE) y HECHO (limites de la potestad normativa)

---

## 9. Sintesis de fechas y estados para el motor de reglas

| Instrumento | Emision | Publicacion D.O. | Vigencia | Estado 2026-09-23 |
|---|---|---|---|---|
| LPDP, D.L. 144 | 12 nov 2024 | N. 219, T. 445, 15 nov 2024, pp. 24-62 | 23 nov 2024 | VIGENTE |
| Ley de Ciberseguridad, D.L. 143 | 12 nov 2024 | N. 219, T. 445, 15 nov 2024, pp. 3-23 | 23 nov 2024 | VIGENTE, sin reformas |
| LPA, D.L. 856 | 15 dic 2017 | N. 30, T. 418, 13 feb 2018 | 13 feb 2019 | VIGENTE (reformada) |
| Reforma LPA, D.L. 523 (Art. 4-A) | 24 feb 2026 | N. 41, T. 450, 27 feb 2026 | 7 mar 2026 | VIGENTE |
| Politicas ACE N. 001-0309025-DPDP | 2 sep 2025 (secundaria) | No localizada | 3 sep 2025 (secundaria; el texto dice "a partir de su publicacion") | VIGENTE (fechas pendientes de verificar en fuente primaria) |
| Lineamientos Delegado (ACE) | 24 jul 2026 | N. 146, T. 452, 11 ago 2026, pp. 12-21 | 19 ago 2026 (Art. 42: "ocho dias despues contados a partir del dia siguiente de su publicacion"; una lectura estricta daria 20 ago 2026) | VIGENTE, pero su registro transitorio fue dejado sin efecto por la ACE y su objeto principal (delegado privado) sera derogado por el D.L. 659 |
| Normativa PAS (ACE) | 24 jul 2026 | N. 146, T. 452, 11 ago 2026, pp. 22-29 | 19 ago 2026 (Art. 49: ocho dias despues de su publicacion) | VIGENTE |
| Reforma LPDP, D.L. 659 | 17 sep 2026 | Pendiente | 8 dias despues de la publicacion | APROBADA-PENDIENTE-PUBLICACION |
| Reforma Delitos Informaticos, D.L. 332 | 19 jun 2025 | 25 jun 2025 (secundaria) | 3 jul 2025 (secundaria) | VIGENTE (no verificada en primaria) |

---

## 10. Incertidumbres y puntos que requieren abogado

1. Texto del Decreto 659. No se ha localizado el texto oficial; todo lo dicho sobre su contenido proviene de la nota de la Asamblea y de prensa. Hasta su publicacion, la ley vigente exige delegado (Art. 15) aunque la ACE haya dejado sin efecto la fecha limite de registro. Hay que definir con abogado la conducta prudente durante el interregno (nombrar delegado interno provisional, o documentar la asignacion de funciones del Art. 16 a un responsable interno).

2. Fecha de emision y publicacion de las Politicas ACE 001-0309025-DPDP. Solo consta por fuente secundaria (2 y 3 de septiembre de 2025). Como de esa fecha depende el vencimiento del Art. 60 inc. 2, debe confirmarse en el Diario Oficial o mediante consulta a la ACE. No consta que las Politicas se hayan publicado en el Diario Oficial, lo que abre la duda de si son eficaces frente a terceros (Art. 162 LPA exige publicacion de las normas administrativas).

3. Lectura del Art. 60 inc. 2 frente a disposiciones ACE posteriores. Si cada nueva disposicion abre un periodo de tres meses de adecuacion, los Lineamientos y la Normativa de agosto de 2026 darian plazo hasta octubre o noviembre de 2026. La ley no lo dice expresamente; conviene tratarlo como argumento defensivo y no como derecho adquirido.

4. Ambito territorial. El Art. 2 LPDP no fija criterio territorial; las Politicas ACE (Art. 2) extienden su aplicacion a "operaciones internacionales vinculadas a ciudadanos salvadorenos", lo que excede lo que una politica puede hacer (Art. 161 LPA). Empresas extranjeras sin establecimiento en El Salvador que traten datos de residentes: sujeto a criterio de abogado.

5. Buros de credito y supervisados SSF. La contra-excepcion del Art. 3 lit. a) es clara para los supervisados; para los buros, la delimitacion entre "historial crediticio bajo la ley especial" y el resto de sus tratamientos requiere analisis de la Ley de Regulacion de los Servicios de Informacion sobre el Historial de Creditos de las Personas (no analizada en este lente). Tambien debe revisarse la interaccion con el secreto bancario y con la normativa tecnica de la SSF.

6. Seguridad privada y prevencion de fraude. La exclusion del Art. 3 lit. c) es por objeto (seguridad publica); su extension a privados es dudosa y se recomienda no aplicarla.

7. Computo de "horas" (Art. 25: 72 horas) bajo el Art. 82 LPA, que habla de "dias y horas habiles". Criterio conservador: horas corridas. Confirmar con abogado.

8. Aplicacion de la multa coercitiva del Art. 27 D.143 a infracciones LPDP. El Art. 53 LPDP remite a la Ley de Ciberseguridad para "el ejercicio de potestad sancionadora", lo que podria incluir la multa coercitiva; la Normativa PAS no la menciona. Punto abierto.

9. Calificacion de operadores de infraestructuras criticas. No se localizo ninguna resolucion publica de la ACE que califique operadores privados (Art. 8 lit. f D.143), ni normativa tecnica de reporte de incidentes con plazos para privados. Para clientes de energia, telecomunicaciones, banca, salud o transporte hay que consultar directamente a la ACE.

10. Edad de consentimiento de NNA. La LPDP no fija edad; remite al principio de ejercicio progresivo y a "las leyes vigentes" (LEPINA). Parametro a definir con abogado.

11. Datos anteriores a la vigencia (Art. 61 inc. 1). La ley exige aplicar medidas de proteccion a datos historicos, pero no dice si hay que obtener consentimiento retroactivo o reinformar a los titulares. Recomendable definir criterio juridico antes de disenar el flujo de "regularizacion de bases legado".

12. Vigencia exacta de los Lineamientos del Delegado (19 o 20 de agosto de 2026) por la formula "ocho dias despues contados a partir del dia siguiente de su publicacion". Sin efecto practico tras la anulacion del plazo de registro, pero conviene fijar criterio de computo general para formulas de vigencia.

13. Discrepancia menor: la Normativa PAS ubica las infracciones en el "Titulo IV, Capitulo II" de la LPDP cuando estan en el Capitulo III. No afecta la validez.

14. Error de redaccion del Art. 24 D.143 ("Las infracciones graves" en la sancion de muy graves). Irrelevante para clientes no sujetos al D.143, pero conviene citarlo con cautela.

15. Otras reformas a la LPA. Se verifico la de febrero de 2026 (Art. 4-A). Pueden existir otras (armonizacion con Ley Crecer Juntos) que no alteran los articulos aqui citados, segun la coincidencia de numeracion con la Normativa PAS de agosto 2026. Un abogado deberia confirmar con el texto consolidado vigente.

---

## 11. Fuentes consultadas (todas al 2026-09-23)

Fuentes primarias locales:
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (texto integro LPDP, copia ACE, 28 paginas)
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\diario_oficial_2024-11-15_mh.txt y .pdf (D.O. 219 T. 445: indice y paginas 24 a 62; NO contiene las paginas 3 a 23)
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\asamblea_decreto_143_ciberseguridad.txt y .pdf (texto integro Ley de Ciberseguridad, incorporado en este sweep desde https://www.asamblea.gob.sv/sites/default/files/documents/decretos/D056D9A1-299D-4188-941A-9C3B5898D3F3.pdf)
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\asamblea_decreto_856_lpa.txt (texto integro LPA, incorporado desde https://www.asamblea.gob.sv/sites/default/files/documents/decretos/361DDB77-97E7-4EFF-B353-C6D872547E7C.pdf)
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\asamblea_decreto_523_reforma_lpa.txt (D.L. 523, incorporado desde https://www.asamblea.gob.sv/sites/default/files/documents/decretos/9364667E-20C8-4FA8-A5D8-E89BEB0A492A.pdf)
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\normativa_sancionadora_OCR.txt y ocr\normativa_sancionadora\page-03.png, page-08.png, page-09.png (Normativa PAS ACE, D.O. 146 T. 452, 11 ago 2026)
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\lineamientos_dpo_OCR.txt (Lineamientos Delegado ACE, misma publicacion; Arts. 40 a 42)
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_politicas_protecciondatos.txt (Politicas N. 001-0309025-DPDP; verificada tambien la copia en linea https://ace.gob.sv/page/documentos/politicas/politicas_protecciondatos.pdf, sin fecha en el texto)
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\dictamen_11_2024_ley_original_OCR.txt (historia legislativa)

Fuentes primarias en linea:
- https://www.asamblea.gob.sv/leyes-y-decretos/decretos-por-anios/2024/0 ; /2025/0 ; /2026/0 y /2026/1 (listados oficiales de decretos por ano)
- https://www.asamblea.gob.sv/leyes-y-decretos/view/7022 (ficha D.L. 659: "Pendiente de Publicacion Material en el Diario Oficial y de Entrada en Vigencia")
- https://www.asamblea.gob.sv/leyes-y-decretos/view/6779 (ficha D.L. 523: D.O. 41, T. 450, 27/02/2026)
- https://www.asamblea.gob.sv/node/14116 (nota oficial de la Asamblea sobre la reforma, 17 sep 2026)
- https://transparencia.mh.gob.sv/downloads/pdf/700-UAIP-LY-2024-14993.pdf (copia del D.O. 15 nov 2024 publicada por Hacienda; mismas 40 paginas que el corpus local)
- https://ace.gob.sv/politicas.php (indice de instrumentos ACE; el enlace a "politicas_ciberseguridad.pdf" devolvio 404)
- https://www.diariooficial.gob.sv/ (buscador dinamico; no devolvio ediciones de septiembre 2026 por URL)

Fuentes secundarias (usadas solo para orientar; marcadas como tales en el texto):
- https://www.eldiariodehoy.com/noticias/nacionales/asamblea-legislativa-deroga-obligatoriedad-de-las-empresas-privadas-de-nombrar-delegados-de-proteccion-de-datos-personales/93615/2026/
- https://www.infobae.com/el-salvador/2026/09/17/el-salvador-la-asamblea-legislativa-elimina-la-obligacion-del-delegado-de-proteccion-de-datos-para-las-empresas/
- https://www.elsalvador.com/noticias/nacional/reforma-proteccion-datos-personales/1293875/2026/
- https://www.elsalvador.com/dinero-y-negocios/entorno-economico/empresas-ley-de-proteccion-datos-el-salvador/1292968/2026/ (comunicado ACE del 12 sep 2026 que deja sin efecto el plazo del 16 sep 2026)
- https://www.contrapunto.com.sv/sin-fecha-para-nombrar-a-los-delegados-de-proteccion-de-datos-personales-la-ace-establece-el-registro-obligatorio/
- https://diario.elmundo.sv/politica/vigentes-politicas-de-actuacion-y-manejo-de-datos-personales-en-el-salvador (emision 2 sep 2025 y vigencia 3 sep 2025 de las Politicas ACE)
- https://www.ey.com/es_ce/technical/tax/tax-alerts/el-salvador-la-agencia-de-ciberseguridad-del-estado-desarrolla-aspectos-relevantes-de-la-ley-de-proteccion-de-datos-personales (alerta 26 ago 2026 sobre Lineamientos y Normativa ACE)
- https://consortiumlegal.com/2026/03/11/reforma-a-la-ley-de-procedimientos-administrativos-en-el-salvador/ (D.L. 523)
- https://www.lexology.com/library/detail.aspx?g=a1188143-72f2-47a2-9c1d-df5098a8ecee (D.L. 332, reforma Ley Especial contra Delitos Informaticos, fechas de publicacion y vigencia)
