# Sweep juridico: motor de plazos, dias habiles, asuetos y periodos de retencion en leyes conexas

Proyecto: PRIV-SV. Lente asignado: motor de plazos, calendario de dias inhabiles y retencion legal.
Fecha de consulta de todas las fuentes: 2026-09-23.
Autor: investigador juridico (agente). Este documento no es asesoria legal; las conclusiones marcadas como "requiere abogado" deben validarse antes de fijar reglas definitivas del producto.

Convenciones: LPDP = Ley para la Proteccion de Datos Personales (D.L. 144/2024). LPA = Ley de Procedimientos Administrativos (D.L. 856/2017). CT = Codigo de Trabajo. C.Com = Codigo de Comercio. CTrib = Codigo Tributario. CC = Codigo Civil. LCLDA = Ley Contra el Lavado de Dinero y de Activos. "dh" = dias habiles. Rutas locales bajo `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\`.

---

## 1. Resumen ejecutivo

1. Regla de computo. La LPDP no contiene reglas propias de computo de plazos; solo dice "dias habiles" (Arts. 9, 18, 19, 20, 21, 22, 30) y "horas" (Art. 25). Por el Art. 62 LPDP ("en todo lo no previsto ... se estara a lo dispuesto en la Ley de Procedimientos Administrativos") las reglas del Art. 82 LPA son la fuente supletoria mas defendible: los plazos por dias u horas se computan solo en dias y horas habiles; los plazos por dias corren desde el dia siguiente a la notificacion o publicacion (o, si el plazo es solo para quien debe resolver, desde el dia siguiente a la presentacion de la peticion); los plazos por meses o anos van de fecha a fecha; y si el ultimo dia es inhabil, el plazo se prorroga al primer dia habil siguiente. La propia ACE aplica esa logica en sus lineamientos y normativa ("a partir del dia siguiente habil"). El Codigo Civil (Arts. 46 a 48) es la regla residual y coincide en lo esencial: los plazos de dias corren hasta la medianoche del ultimo dia y, si son de "dias utiles", excluyen los feriados.

2. Dias inhabiles. Para el sector privado la lista nacional obligatoria es la del Art. 190 CT (1 enero; jueves, viernes y sabado de Semana Santa; 1 mayo; 6 agosto; 15 septiembre; 2 noviembre; 25 diciembre; mas 3 y 5 de agosto en la ciudad de San Salvador y, en el resto del pais, el dia principal de la fiesta patronal local), completada por dos decretos autonomos: 10 de mayo (D.L. 339/2016) y 17 de junio (D.L. 208/2012). El sector publico se rige por la Ley de Asuetos, Vacaciones y Licencias de los Empleados Publicos (sabados y domingos son asueto; vacaciones colectivas en Semana Santa, 1 a 6 de agosto y 24 diciembre a 2 enero). La Asamblea decreta asuetos ad hoc con frecuencia (16 sep 2022; 26 dic 2022 y 2 ene 2023; 1 jun 2024 solo sector privado; 18 jun 2024). No existe una lista oficial unica de fiestas patronales municipales: el motor debe tratarlas como capa configurable con fuente documentada.

3. Sabados. No hay norma que declare el sabado inhabil para una empresa privada (la semana laboral del CT es de 44 horas y el descanso legal es el domingo, Arts. 161 y 173). Pero los plazos de la LPDP son plazos de un procedimiento cuya supletoria es la LPA y cuya autoridad (la ACE) no labora sabados (Ley de Asuetos, Art. 1). Recomendacion: por defecto sabado y domingo inhabiles, con la opcion de que la empresa configure un calendario mas exigente y con un "margen de seguridad" interno. Decision final: abogado.

4. 72 horas. El Art. 25 LPDP fija "un plazo maximo de setenta y dos horas desde que se tuvo conocimiento". Si se aplicara literalmente el Art. 82 LPA (solo horas habiles) el plazo se estiraria a mas de una semana, resultado incompatible con la finalidad de la norma y con la Politica ACE ("en un maximo de 72 horas"). Regla propuesta: computar 72 horas corridas desde el momento de conocimiento, con alertas a las 24 y 48 horas. Marcar como INCERTIDUMBRE que requiere abogado.

5. Retencion. Los periodos que condicionan la eliminacion de datos y que el motor debe conocer son: 10 anos para registros mercantiles y correspondencia contable (C.Com Arts. 451 y 454); 10 anos para documentacion tributaria desde su emision o recibo (CTrib Art. 147); 5 anos para documentacion de operaciones y datos de identificacion de clientes y 15 anos para registros de transacciones en sujetos obligados de la LCLDA (Arts. 10 lit. b y 12; Instructivo UIF Arts. 57 a 59); 10 anos para expedientes clinicos (Norma Tecnica del Expediente Clinico, Art. 34); 10 anos para la documentacion del aviso de privacidad (Lineamientos ACE, Art. 31). La Ley de Firma Electronica (Arts. 13 y 13-A) y la Ley de Comercio Electronico (Art. 26) no fijan anos: remiten al plazo que exija la ley del giro y fijan requisitos de forma para la conservacion electronica. El CT no fija plazo de conservacion de planillas ni contratos; la LISP y la Ley de Bancos tampoco lo hacen de forma expresa en los textos revisados.

6. Prescripcion. Infracciones y sanciones LPDP: 5 anos (Ley de Ciberseguridad Art. 29; Normativa sancionadora ACE Art. 47), computados segun el Art. 149 LPA (desde el dia siguiente a la comision; en infracciones continuadas, desde el ultimo hecho). Civil: 10 anos accion ejecutiva, 20 ordinaria (CC 2254); 3 anos por dano o dolo (CC 2083). Mercantil: 6 meses a 5 anos (C.Com 995). Laboral: 60 y 180 dias, 2 anos por riesgo profesional (CT 610 a 616). Tributaria: 10 anos (CTrib 84), caducidad de fiscalizacion 3 o 5 anos (CTrib 175). Estos plazos fundamentan la tabla de retencion propuesta para los registros del propio software (seccion 8).

---

## 2. Reglas de computo de plazos

### 2.1 Ley de Procedimientos Administrativos (D.L. 856, 15 dic 2017)

Fuente primaria: texto oficial de la Asamblea Legislativa, https://www.asamblea.gob.sv/sites/default/files/documents/decretos/361DDB77-97E7-4EFF-B353-C6D872547E7C.pdf (consultado 2026-09-23; extraido a texto localmente). Vigencia: Art. 168, "doce meses despues de su publicacion en el Diario Oficial" (segun fuentes secundarias, publicada en D.O. 30, Tomo 418, 13 feb 2018, vigente desde el 13 feb 2019; el dato de D.O. no se pudo confirmar en el PDF, marcar confianza media).

Transcripciones textuales de los articulos clave:

- Art. 80: "Los terminos y plazos del procedimiento administrativo son obligatorios y perentorios para la Administracion y para los particulares."
- Art. 81: "Los actos, tanto de la Administracion como de los particulares, deberan llevarse a cabo en dias y horas habiles. El organo competente podra acordar, por resolucion motivada y siempre que existan razones de urgencia, habilitar dias y horas inhabiles para realizar actos procedimentales."
- Art. 82: "Si los plazos se senalan por dias u horas, se computaran unicamente los dias y horas habiles. La Administracion debera expresar en sus resoluciones, el plazo legalmente previsto para llevar a cabo un acto del procedimiento, la fecha en la que vence y las consecuencias de su incumplimiento o retraso. Si el plazo se fija en dias, se contara a partir del dia siguiente a aquel en que tenga lugar la notificacion o publicacion del acto de que se trate o desde el siguiente a aquel en que se hubiera producido la estimacion o desestimacion por silencio administrativo. Cuando el plazo se fije unicamente para la Administracion, este empezara a correr desde el dia siguiente a aquel en el que se hubiere presentado la peticion del interesado. Si el plazo se fija por meses o anos, estos se computaran de fecha a fecha. Si en el mes o ano del vencimiento no hubiera dia equivalente a aquel en que comienza el computo, se entendera que el plazo expira el ultimo dia del mes. Cuando el ultimo dia del plazo sea inhabil, se entendera prorrogado al primer dia habil siguiente."
- Art. 83 (prorroga): la Administracion puede ampliar plazos "de oficio o a peticion del interesado", de forma motivada, sin exceder "la mitad del tiempo establecido"; no aplica al plazo para concluir el procedimiento ni al de recursos; la prorroga debe pedirse o acordarse "antes del vencimiento del plazo".
- Art. 84: "El plazo se tendra por concluido, si antes de su vencimiento se cumplen todos los actos para los que estaba previsto."
- Art. 85: reposicion de actuaciones por fuerza mayor o caso fortuito; solicitud "dentro de los cinco dias posteriores al dia en que hubiera cesado la causa".
- Art. 88: regla general de 10 dias para tramites a cargo del interesado, ampliables hasta otros 10.
- Art. 89: plazo maximo para concluir el procedimiento, 9 meses; peticiones que se resuelven sin mas tramite, 20 dias.
- Art. 90: suspension del plazo maximo para resolver, entre otros, "cuando deba requerirse a cualquier interesado para la subsanacion de deficiencias y la aportacion de documentos ... por el tiempo que medie entre la notificacion del requerimiento y su efectivo cumplimiento por el destinatario o, en su defecto, el transcurso del plazo concedido".
- Art. 94: suspension del procedimiento por caso fortuito o fuerza mayor, "solo mientras subsista la causa".
- Art. 97: "Toda notificacion debera ser cursada dentro del plazo de tres dias a partir de la fecha en que el acto haya sido" dictado.
- Art. 98: la notificacion puede practicarse "por cualquier medio que permita tener constancia de la recepcion por el interesado o su representante, asi como de la fecha y el contenido del acto notificado"; en procedimientos iniciados a solicitud del interesado, "en el lugar o medio que este haya senalado a tal efecto en la solicitud".
- Art. 99: el interesado debe senalar "el medio electronico o direccion postal para recibir las sucesivas notificaciones".
- Art. 101: prueba de la notificacion; si es electronica, "debera dejarse constancia por escrito de su realizacion ... fecha y hora en que se realizo".
- Art. 149: "El plazo de prescripcion de las infracciones comenzara a contarse desde el dia siguiente a aquel en que se hubiera cometido la infraccion. En los casos de infraccion realizada de forma continuada o permanente, tal plazo se comenzara a contar desde el dia en que se realizo el ultimo hecho constitutivo de la infraccion o desde que se elimino la situacion ilicita. Interrumpira la prescripcion de la infraccion la iniciacion, con conocimiento del presunto responsable, del procedimiento administrativo. La prescripcion se reanudara, por la totalidad del plazo, desde el dia siguiente a aquel en que se cumpla un mes de paralizacion del procedimiento por causa no imputable al presunto responsable. El plazo de prescripcion de las sanciones comenzara a contarse desde el dia siguiente a aquel en que adquiera firmeza, en via administrativa, la resolucion por la que se impone la sancion."
- Art. 158 (procedimiento simplificado): 5 dias desde la notificacion del acuerdo de inicio para alegaciones y prueba; resolucion definitiva en 15 dias desde la ultima actuacion; posible paso a procedimiento ordinario con 5 dias para alegaciones.

Observaciones relevantes para el motor:

- La LPA NO define que dias son habiles ni que horas son habiles. No menciona sabados, domingos ni asuetos. El calendario de habilidad se toma de otras normas (seccion 3).
- Ambito (Art. 2): la LPA se aplica a la Administracion Publica y sus concesionarios. No rige de forma directa la relacion titular-empresa privada; entra por la remision del Art. 62 LPDP (ver 2.3).

**Norma:** Ley de Procedimientos Administrativos (D.L. 856/2017)
**Articulo:** 80, 81, 82, 83, 97, 98, 149
**Obligacion:** computar los plazos por dias u horas solo en dias y horas habiles; iniciar el computo el dia siguiente a la notificacion; prorrogar al primer dia habil siguiente cuando el ultimo dia sea inhabil; notificar dentro de 3 dias; prescripcion desde el dia siguiente a la infraccion.
**A quien aplica:** Administracion Publica (ACE) de forma directa; a los responsables privados por supletoriedad del Art. 62 LPDP.
**Implicacion para el software:** el motor debe (a) registrar fecha y hora de notificacion o recepcion de cada acto, (b) empezar a contar el dia habil siguiente, (c) saltar dias inhabiles, (d) mover el vencimiento al siguiente dia habil, (e) computar meses y anos de fecha a fecha, (f) mostrar en cada resolucion generada la fecha de vencimiento y las consecuencias del incumplimiento (Art. 82 inc. 2, buena practica trasladable).
**Fuente oficial:** https://www.asamblea.gob.sv/sites/default/files/documents/decretos/361DDB77-97E7-4EFF-B353-C6D872547E7C.pdf (2026-09-23)
**Vigencia:** VIGENTE (MODIFICADA en 2026 solo en cuanto al Art. 4-A, ver 2.2)
**Clasificacion:** OBLIGATORIO para la ACE; CONDICIONAL (por supletoriedad, salvo criterio distinto de abogado) para la empresa privada.

### 2.2 Reforma 2026 a la LPA (D.L. 523, 24 feb 2026)

Segun Consortium Legal (11 mar 2026, https://consortiumlegal.com/2026/03/11/reforma-a-la-ley-de-procedimientos-administrativos-en-el-salvador/) el D.L. 523 adiciona un Art. 4-A que suprime exigencias de legalizacion, apostilla o copias autenticadas de documentos extranjeros vinculados a operaciones comerciales o aduaneras verificables por medios electronicos, permite cumplirlas durante la sustanciacion del procedimiento y preve resoluciones provisionales con "diez dias habiles" para presentar documentacion. Vigencia ocho dias despues de su publicacion; segun la misma fuente y el titulo de la version consolidada publicada por la Direccion General de Aduanas ("actualizada con el D.O. No. 41, T. 450, 27 de febrero de 2026"), la reforma esta vigente desde el 7 de marzo de 2026. La lista oficial de decretos 2026 de la Asamblea confirma el Decreto 523 del 24/02/2026 titulado "Reforma a la Ley de Procedimientos Administrativos". Conclusion: la reforma NO toca las reglas de computo de plazos, dias habiles ni notificaciones. Confianza: media (texto del decreto no transcrito de fuente primaria; datos de D.O. segun fuente secundaria y titulo de documento oficial).

### 2.3 Codigo Civil como regla residual

Fuente: Codigo Civil, texto en https://www.oas.org/dil/esp/codigo_civil_el_salvador.pdf (2026-09-23).

- Art. 46: "Todos los plazos de dias, meses o anos de que se haga mencion en las leyes ... se entendera que han de ser completos; y correran ademas hasta la medianoche del ultimo dia del plazo. El primero y ultimo dia de un plazo de meses o anos deberan tener un mismo numero en los respectivos meses ... Se aplicaran estas reglas a los contratos, a las prescripciones, a las calificaciones de edad, y en general, a cualesquiera plazos o terminos prescritos en las leyes ... salvo que en las mismas leyes, actos o contratos se disponga expresamente otra cosa."
- Art. 47: un acto que debe ejecutarse "en o dentro de cierto plazo" vale "si se ejecuta antes de la medianoche en que termina el ultimo dia del plazo".
- Art. 48: "En los plazos que se senalaren en las leyes ... se comprenderan aun los dias feriados; a menos que el plazo senalado sea de dias utiles, expresandose asi; pues en tal caso no se contaran los feriados."

Implicacion: aun si un abogado concluyera que la LPA no es aplicable a la relacion titular-empresa, el resultado practico es casi identico: "dias habiles" equivale a "dias utiles" y excluye feriados; el plazo corre hasta la medianoche del ultimo dia; los plazos de meses van de fecha a fecha. La diferencia principal es que el CC no dice expresamente que el computo empiece el dia siguiente ni que el vencimiento en dia inhabil se traslade; la LPA si.

### 2.4 Que regimen rige los plazos entre titular y empresa privada

Argumentos a favor de aplicar la LPA (Art. 82) por supletoriedad:

1. Art. 62 LPDP es una remision expresa y general: "En todo lo no previsto en la presente ley se estara a lo dispuesto en la Ley de Procedimientos Administrativos". No distingue entre sujetos publicos y privados ni entre el procedimiento sancionador y el procedimiento de ejercicio de derechos.
2. La propia LPDP usa vocabulario procedimental administrativo para el tramite ante el responsable privado: "prevencion ... por una sola ocasion", "subsane las omisiones dentro de un plazo de diez dias habiles contados a partir del dia siguiente al de la notificacion", "se archivara su escrito sin mas tramite" (Art. 18), "resolucion motivada" (Art. 22). Es la terminologia del Art. 88 LPA.
3. La ACE, autoridad de aplicacion, adopta la misma logica en sus instrumentos: Normativa sancionadora Art. 12 ("a partir del dia siguiente habil a la emision del informe"), Art. 19 y 21 ("contados a partir del dia siguiente habil a la notificacion"); Lineamientos Art. 10 ("contados a partir del dia siguiente del nombramiento") y Art. 33 ("dentro del plazo de tres dias habiles contados a partir de su emision"). Un responsable que aplique el Art. 82 LPA se alinea con el criterio que la ACE usara al fiscalizar (infraccion grave Art. 56 lit. b num. 2: no atender solicitudes "en el tiempo y forma establecidos").
4. El Codigo Civil (Art. 46 inc. final) cede ante regla expresa en otra ley; la LPA, via Art. 62 LPDP, es esa regla.

Argumentos en contra (que un abogado podria sostener):

1. Art. 2 LPA limita su ambito a la Administracion Publica y concesionarios; el responsable privado no "dicta actos administrativos".
2. La remision del Art. 62 podria leerse restringida a los procedimientos ante la ACE.

Conclusion propuesta: aplicar el Art. 82 LPA como regla de computo para todos los plazos de la LPDP, con el CC como respaldo, y documentar esa decision en la configuracion del motor. Riesgo residual bajo porque ambos regimenes convergen. Clasificacion: CONDICIONAL (requiere validacion de abogado, ver seccion 9).

### 2.5 Plazos en horas: las 72 horas del Art. 25 LPDP

Texto: "notificara a la Agencia de Ciberseguridad del Estado, a la Fiscalia General de la Republica y a los titulares afectados dicho acontecimiento, para lo cual se establece un plazo maximo de setenta y dos horas desde que se tuvo conocimiento de la vulneracion de seguridad" (Art. 25 inc. 1, `ace_decreto_144.txt`, pag. 14). Dentro de ese mismo plazo debe iniciarse la revision exhaustiva (inc. 2). La Politica ACE N. 001-0309025-DPDP, Art. 4, medidas de transferencia lit. d), repite "en un maximo de 72 horas". La Normativa sancionadora Art. 34 usa la misma unidad para el aviso de la ACE a la FGR ("en el plazo de setenta y dos horas").

Problema: el Art. 82 LPA dice que los plazos en horas "se computaran unicamente" en horas habiles. Aplicado literalmente, 72 horas habiles equivaldrian a nueve jornadas de ocho horas, lo que vaciaria la urgencia buscada por el legislador y contradice la lectura de la ACE. Ademas, el evento inicial ("desde que se tuvo conocimiento") puede ocurrir en dia inhabil.

Regla propuesta para el software (RECOMENDADO, con INCERTIDUMBRE juridica): computar 72 horas corridas (reloj continuo) desde la marca de tiempo de conocimiento registrada por la empresa; mostrar la fecha y hora limite; alertas a 24, 48 y 60 horas; permitir al abogado del cliente cambiar el modo de computo a "horas habiles" si asi lo decide, dejando trazabilidad del criterio elegido. Evento de inicio: fecha y hora en que "el responsable tenga conocimiento" (Art. 25); el software debe exigir capturar ese dato con precision y quien lo conocio.

---

## 3. Dias inhabiles para una empresa privada

### 3.1 Calendario nacional obligatorio del Codigo de Trabajo

Fuente primaria: Codigo de Trabajo, texto oficial de la Asamblea Legislativa, https://www.asamblea.gob.sv/sites/default/files/documents/decretos/AD778A29-F1B3-495E-AE19-E2B05D93685D.pdf (2026-09-23), y extracto de la Corte Suprema de Justicia, https://www.csj.gob.sv/wp-content/uploads/2021/06/11-Co%CC%81digo-de-Trabajo-de-El-Salvador-Di%CC%81as-de-asueto.pdf.

Art. 190 (texto): "Se establecen como dias de asueto remunerado los siguientes: a) Primero de enero; b) Jueves, viernes y sabado de la Semana Santa; c) Primero de mayo; ch) Seis de agosto; d) Quince de septiembre; e) Dos de noviembre; y f) Veinticinco de diciembre. Ademas se establecen el tres y cinco de agosto en la ciudad de San Salvador; y en el resto de la Republica, el dia principal de la festividad mas importante del lugar, segun la costumbre."

Art. 191: el asueto se remunera con salario basico. Art. 192: quien trabaja en asueto devenga salario ordinario mas recargo del 100%. Art. 193: empresas de servicios publicos o esenciales, hoteles, restaurantes, ventas de primera necesidad y labores continuas mantienen personal. Art. 194: si el asueto coincide con el descanso semanal, solo salario basico salvo que se trabaje.

Nota: el 24 y el 31 de diciembre NO son asueto legal (confirmado por prensa que cita al Art. 190; diario.elmundo.sv 22 nov 2024 y comercioynegocios.org 23 nov 2024, fuentes secundarias).

**Norma:** Codigo de Trabajo
**Articulo:** 190
**Obligacion:** conceder asueto remunerado en los dias listados; en San Salvador ademas 3 y 5 de agosto; en el resto del pais el dia principal de la fiesta patronal local.
**A quien aplica:** todo patrono del sector privado.
**Implicacion para el software:** capa "calendario nacional base" con las fechas fijas y las tres fechas moviles de Semana Santa; capa "asueto local" por municipio o distrito de cada sede del cliente.
**Fuente oficial:** PDF de la Asamblea citado (2026-09-23)
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 3.2 Asuetos nacionales creados por decretos autonomos (no estan en el Art. 190)

- 10 de mayo, Dia de la Madre: D.L. 339, 14 abr 2016, Art. 1: "Declarase el 10 de mayo de cada ano como 'Dia de la Madre' con asueto nacional remunerado para el sector publico y privado ..."; Art. 3 deroga el D.L. 205 de 1983 que solo cubria al sector publico. Fuente primaria: https://www.jurisprudencia.gob.sv/DocumentosBoveda/D/2/2010-2019/2016/04/B815C.PDF (2026-09-23). La pagina de la Asamblea sobre decretos de dias conmemorativos confirma "Decreto No. 339, 14/04/2016, Dia de la Madre, asueto nacional remunerado".
- 17 de junio, Dia del Padre: D.L. 208, aprobado el 20 dic 2012, asueto remunerado para sector publico y privado. Fuente: Ministerio de Trabajo, https://www.mtps.gob.sv/2019/06/14/mtps-17-de-junio-asueto-remunerado-para-las-personas-trabajadoras/ (fuente oficial, texto del decreto no transcrito; confianza media).

Consecuencia: la lista efectiva de asuetos nacionales del sector privado tiene 11 fechas (12 en San Salvador con el 3 y el 5 de agosto, mas la fiesta patronal local fuera de la capital). La prensa habla de "11 dias de asueto" contando 10 de mayo y 17 de junio.

**Norma:** D.L. 339/2016 y D.L. 208/2012
**Articulo:** Art. 1 de cada decreto
**Obligacion:** asueto remunerado nacional el 10 de mayo y el 17 de junio, sector publico y privado.
**A quien aplica:** todo patrono.
**Implicacion para el software:** incluir ambas fechas en el calendario nacional base como inhabiles.
**Fuente oficial:** jurisprudencia.gob.sv (D.L. 339) y mtps.gob.sv (D.L. 208), 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 3.3 Sector publico: Ley de Asuetos, Vacaciones y Licencias de los Empleados Publicos (D.L. 17, 4 mar 1940, con reformas)

Fuente: texto consolidado con reformas hasta 2022, https://www.andes21dejunio.com/wp-content/uploads/2024/04/LEY-DE-ASUETOS-VACACIONES-Y-LICENCIAS-EMPLEADOS-PUBLICO-CON-REFORMAS-2022.pdf (copia del indice legislativo de la Asamblea; confianza media por no ser el portal oficial) y https://www.transparenciafiscal.gob.sv/downloads/pdf/DC5091_9_Ley_de_Asuetos_Vacaciones_y_Licencias_de_los_Empleados_Publicos.pdf.

Art. 1: "Los empleados publicos gozaran de asueto remunerado durante los siguientes dias: todos los domingos y sabados del ano; el 1 de mayo ...; el 10 de mayo ...; el 15 de septiembre ...; y, el 2 de noviembre ...". Ademas "gozaran de licencia a titulo de vacaciones durante tres periodos en el ano: uno de ocho dias, durante Semana Santa; uno de seis dias del 1 al 6 de agosto, y uno de diez dias del 24 de diciembre al 2 de enero inclusive". Art. 2: "La declaracion de un dia de fiesta nacional, no implica asueto para los empleados publicos, salvo que la Ley lo exprese claramente." Art. 3: los empleados de los departamentos fuera de San Salvador gozan de vacacion "durante los dias principales de las respectivas fiestas patronales, segun lo indique el reglamento".

Relevancia para el producto: (a) confirma que para la Administracion (incluida la ACE) el sabado es dia de asueto, es decir inhabil; (b) durante las vacaciones colectivas (Semana Santa, 1 a 6 de agosto, 24 dic a 2 ene) las oficinas publicas suelen no atender, lo que afecta a los plazos ante la ACE (comunicacion de nombramiento, respuesta a requerimientos, denuncias) aunque no a los plazos frente al titular. El Art. 81 LPA permite a la Administracion habilitar dias inhabiles por urgencia.

**Norma:** Ley de Asuetos, Vacaciones y Licencias de los Empleados Publicos
**Articulo:** 1, 2, 3
**Obligacion:** (para el Estado) asueto sabados, domingos y fechas listadas; vacaciones colectivas.
**A quien aplica:** empleados publicos; indirectamente a quien debe hacer gestiones ante la ACE.
**Implicacion para el software:** capa "calendario de la autoridad (ACE)" distinta del calendario de la empresa, usada para plazos cuyo destinatario es la ACE (registro de delegado, respuestas a requerimientos, pago de multas) y para advertir que una notificacion a la ACE en dia inhabil puede considerarse recibida el siguiente dia habil.
**Fuente oficial:** enlaces citados (2026-09-23)
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (solo para plazos cuyo destinatario es una entidad publica)

### 3.4 Asuetos locales (fiestas patronales)

Base: Art. 190 CT inc. final. El dia local es "el dia principal de la festividad mas importante del lugar, segun la costumbre". No existe en el CT ni en la Ley de Asuetos una lista oficial por municipio; el Art. 3 de la Ley de Asuetos remite a un reglamento para los empleados publicos departamentales, que no se localizo en fuente oficial en linea. En la practica la fuente es la comunicacion de cada alcaldia y el criterio del Ministerio de Trabajo y Prevision Social. Ejemplos citados por prensa (fuente secundaria, confianza baja): Santa Ana, fiestas julias en honor a Senora Santa Ana (dia principal 26 de julio); San Miguel, fiestas en honor a la Virgen de la Paz (dia principal 21 de noviembre). El instructivo interno del Organo Judicial (2019) muestra la practica publica de tomar "los ultimos tres dias de fiesta" para sedes fuera de San Salvador.

Regla propuesta: capa "asuetos locales" por sede, con campo obligatorio de fuente (comunicado municipal o del MTPS) y fecha de verificacion; el software no debe presumir fechas locales sin que el cliente las confirme. Para plazos frente al titular, la fiesta patronal de la sede que tramita la solicitud es la relevante; ante duda, computar como habil (criterio conservador para las obligaciones de la empresa) y como inhabil para los plazos del titular.

**Norma:** Codigo de Trabajo
**Articulo:** 190 inc. final
**Obligacion:** asueto local el dia principal de la fiesta patronal.
**A quien aplica:** patronos con sedes fuera de la ciudad de San Salvador; en San Salvador, 3 y 5 de agosto.
**Implicacion para el software:** calendario por sede, configurable, con fuente documentada.
**Fuente oficial:** PDF del CT (2026-09-23); reglas locales sin fuente oficial centralizada.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (depende de la ubicacion de cada sede)

### 3.5 Asuetos ad hoc decretados por la Asamblea Legislativa

Ejemplos verificados en el portal oficial de la Asamblea (2026-09-23):

- 16 de septiembre de 2022: asueto para sector publico y privado por fiestas patrias, 71 votos, con excepciones (MINSAL, ISSS, FAES, PNC, DGME, IML). https://www.asamblea.gob.sv/node/12407
- 26 de diciembre de 2022 y 2 de enero de 2023: asueto remunerado para sector publico y privado, 69 votos. https://www.asamblea.gob.sv/node/12612
- 18 de junio de 2024: asueto nacional remunerado por emergencia de lluvias, 59 votos, sector publico y privado, con excepciones. https://www.asamblea.gob.sv/node/13205
- 1 de junio de 2024: licencia remunerada para el sector privado por la toma de posesion presidencial, 57 votos (fuente secundaria: La Prensa Grafica 22 may 2024, https://www.laprensagrafica.com/elsalvador/Aprueban-asueto-para-el-1-de-junio-por-toma-de-posesion-presidencial-20240522-0071.html; confianza media).

En la lista oficial de decretos de 2025 y 2026 no aparece ningun decreto con la palabra "asueto" en el titulo (consulta a https://www.asamblea.gob.sv/leyes-y-decretos/decretos-por-anios/2025/0 y /2026/0, 2026-09-23); es posible que esos decretos usen otro titulo ("Disposiciones especiales ..."), por lo que la ausencia no es concluyente.

Regla propuesta: capa "asuetos ad hoc" administrada centralmente por el proveedor del software (no por cada cliente), con vinculo al decreto o a la noticia oficial de la Asamblea, fecha de publicacion en el D.O. y alcance (publico, privado, ambos, excepciones sectoriales). Cuando el decreto cubre solo al sector publico, el dia es inhabil para plazos ante la ACE pero habil para plazos frente al titular.

**Norma:** decretos legislativos especiales (ejemplos citados)
**Articulo:** Art. 1 de cada decreto
**Obligacion:** asueto remunerado en la fecha decretada, con el alcance que el decreto fije.
**A quien aplica:** segun cada decreto.
**Implicacion para el software:** capa central de asuetos ad hoc con alcance por sector; alerta a clientes cuando se agrega una fecha que afecta plazos en curso.
**Fuente oficial:** enlaces de asamblea.gob.sv citados
**Vigencia:** cada decreto es de efecto unico (fecha pasada)
**Clasificacion:** CONDICIONAL

### 3.6 Sabados: son habiles para una empresa privada?

Hechos normativos:

- CT Art. 161: semana laboral diurna de hasta 44 horas; Art. 173: "El dia de descanso semanal es el domingo"; Art. 170 permite pactar una hora extra diaria para "descansar, en forma consecutiva, los dias sabados y domingo". Es decir, para el CT el sabado es en principio dia laborable (jornada de medio dia o completa segun la empresa).
- Ley de Asuetos Art. 1: para los empleados publicos "todos los domingos y sabados del ano" son asueto. La ACE, como entidad publica, no atiende sabados.
- LPA Arts. 81 y 82: los actos se realizan en "dias y horas habiles" sin definirlos.
- Codigo Civil Art. 48: los "dias utiles" excluyen "los feriados"; no menciona sabados.

Argumentacion: en el derecho administrativo salvadoreno el sabado se trata como inhabil porque la Administracion no labora (Ley de Asuetos Art. 1); toda la practica de la ACE (sus lineamientos hablan de "horario y calendarizacion de El Salvador", Art. 15 lit. b) y los plazos de la Normativa sancionadora presuponen semana de lunes a viernes. Como la LPDP usa "dias habiles" con la LPA como supletoria, la lectura mas coherente es que "dias habiles" en la LPDP son los dias habiles administrativos: lunes a viernes, excluidos asuetos. Una empresa que abre sabados no convierte el sabado en "dia habil" del procedimiento; solo podria, por analogia con el Art. 81 LPA, habilitarlo voluntariamente para actuar (por ejemplo responder antes), nunca para exigirle al titular que actue.

Regla propuesta: por defecto sabado y domingo inhabiles en todos los calendarios. Opcion de configuracion "sabado habil" solo para el calculo interno de fechas objetivo de la empresa (nunca para plazos del titular), y siempre mostrando la fecha legal estimada con el calendario por defecto. Requiere confirmacion de abogado (seccion 9).

### 3.7 Horario habil y presentaciones fuera de horario

La LPA no define "horas habiles". No se localizo en la LPDP, en los lineamientos ni en la normativa ACE una definicion de horario. En la practica administrativa las horas habiles son las del horario de atencion de la oficina. Para el responsable privado, las solicitudes ARCO-POL pueden llegar por canales electronicos a cualquier hora (los formularios ACE preven notificacion por correo electronico). Regla propuesta (RECOMENDADO): registrar la marca de tiempo real de recepcion; si la recepcion ocurre en dia inhabil o fuera del horario habil configurado por la empresa, el motor considera "dia de recepcion" el siguiente dia habil y empieza a contar el plazo el dia habil posterior a ese; pero para plazos de la empresa que corren "a partir de la recepcion" (Arts. 9, 19 y 30 LPDP) se muestra tambien la fecha mas exigente (contar desde la recepcion real) como referencia de prudencia. La empresa debe publicar su horario y canal en el aviso de privacidad (Art. 24 lit. e y f LPDP).

### 3.8 Calendario 2026 y 2027 (sector privado, nacional)

Fechas de Semana Santa calculadas con el algoritmo de Pascua gregoriana (Pascua 5 abr 2026 y 28 mar 2027); las fijas provienen del Art. 190 CT y de los D.L. 339/2016 y 208/2012. Verificacion secundaria del calendario 2026: El Diario de Hoy, 2 ene 2026 (coincide en todas las fechas).

| Fecha 2026 | Dia | Fecha 2027 | Dia | Asueto | Base |
|---|---|---|---|---|---|
| 01-01-2026 | jueves | 01-01-2027 | viernes | Ano Nuevo | CT 190 a |
| 02-04-2026 | jueves | 25-03-2027 | jueves | Jueves Santo | CT 190 b |
| 03-04-2026 | viernes | 26-03-2027 | viernes | Viernes Santo | CT 190 b |
| 04-04-2026 | sabado | 27-03-2027 | sabado | Sabado Santo | CT 190 b |
| 01-05-2026 | viernes | 01-05-2027 | sabado | Dia del Trabajo | CT 190 c |
| 10-05-2026 | domingo | 10-05-2027 | lunes | Dia de la Madre | D.L. 339/2016 |
| 17-06-2026 | miercoles | 17-06-2027 | jueves | Dia del Padre | D.L. 208/2012 |
| 03-08-2026 | lunes | 03-08-2027 | martes | Solo ciudad de San Salvador | CT 190 inc. final |
| 05-08-2026 | miercoles | 05-08-2027 | jueves | Solo ciudad de San Salvador | CT 190 inc. final |
| 06-08-2026 | jueves | 06-08-2027 | viernes | Divino Salvador del Mundo | CT 190 ch |
| 15-09-2026 | martes | 15-09-2027 | miercoles | Independencia | CT 190 d |
| 02-11-2026 | lunes | 02-11-2027 | martes | Difuntos | CT 190 e |
| 25-12-2026 | viernes | 25-12-2027 | sabado | Navidad | CT 190 f |

Mas: fiesta patronal local fuera de San Salvador (fecha por sede) y asuetos ad hoc que se decreten. Para plazos ante la ACE agregar: todos los sabados y domingos, y las vacaciones publicas (Semana Santa completa, 1 a 6 de agosto, 24 dic a 2 ene) como dias de probable no atencion.

### 3.9 Configuracion recomendada del calendario del motor

```
+-----------------------------------------------------------------------+
| CAPA 0  Fin de semana: sabado y domingo inhabiles (por defecto)        |
+-----------------------------------------------------------------------+
| CAPA 1  Calendario nacional base (CT 190 + D.L. 339/2016 + D.L. 208)  |
|         Fuente: Asamblea Legislativa. Mantiene: proveedor.            |
+-----------------------------------------------------------------------+
| CAPA 2  Asuetos ad hoc (decretos legislativos, alcance por sector)    |
|         Fuente: asamblea.gob.sv y Diario Oficial. Mantiene: proveedor |
+-----------------------------------------------------------------------+
| CAPA 3  Asuetos locales por sede (3 y 5 ago en San Salvador; fiesta   |
|         patronal en el resto). Fuente: alcaldia / MTPS. Mantiene:     |
|         cliente, con fuente y fecha de verificacion obligatorias.     |
+-----------------------------------------------------------------------+
| CAPA 4  Calendario propio de la empresa (cierres, horario habil,      |
|         sabado habil opcional solo para metas internas).              |
|         Nunca reduce los plazos del titular.                          |
+-----------------------------------------------------------------------+
| CAPA 5  Calendario de la autoridad (ACE): capas 0 a 2 + vacaciones    |
|         de la Ley de Asuetos. Se usa solo para plazos ante la ACE.    |
+-----------------------------------------------------------------------+
        |
        v
  Motor: fecha/hora evento -> dia habil siguiente -> cuenta N dias habiles
         segun capas aplicables -> si vence en inhabil, siguiente habil
         -> guarda snapshot del calendario usado (evidencia)
```

Fuente oficial de cada capa: capa 1 y 2, Asamblea Legislativa y Diario Oficial (imprentanacional.gob.sv); capa 3, alcaldias y MTPS (mtps.gob.sv); capa 5, Ley de Asuetos y avisos de la ACE (ace.gob.sv). El motor debe guardar, por cada plazo calculado, una copia del calendario aplicado (evidencia de responsabilidad demostrada, Art. 5 lit. i LPDP).

---

## 4. Tabla de plazos de la LPDP, lineamientos y normativa ACE

Fuentes locales: `ace_decreto_144.txt` (LPDP), `lineamientos_dpo_OCR.txt` y `ocr/lineamientos_dpo/page-NN.png` (Lineamientos, D.O. 146 Tomo 452, 11 ago 2026, vigentes 19 ago 2026 por Art. 42), `normativa_sancionadora_OCR.txt` y `ocr/normativa_sancionadora/page-NN.png` (Normativa, mismo D.O., vigente 19 ago 2026 por Art. 49). Pasajes dudosos del OCR se confirmaron contra las imagenes page-03, page-08 (normativa) y page-10 (lineamientos).

Nota sobre la reforma de septiembre de 2026 (D.L. 659, aprobado 17 sep 2026, vigencia pendiente de publicacion): segun fuentes secundarias mantiene los plazos de 20+20, 10, 5, 5 y 5 dias y traslada las funciones del delegado al sujeto obligado en el sector privado. Todos los plazos de los Lineamientos referidos al delegado privado deben tratarse como CONDICIONALES hasta conocer el texto oficial.

### 4.1 Plazos de la LPDP

| Norma / Art. | Plazo | Unidad | Evento que lo inicia | Detiene o suspende | Prorroga | Regla propuesta para el software |
|---|---|---|---|---|---|---|
| LPDP 9 inc. 3 (rectificacion) | 20 | dh | "recepcion de la solicitud" | Prevencion del Art. 18 (por supletoriedad LPA 90.1, ver 4.4) | No expresa (aplicar la del Art. 20) | Contar desde el dia habil siguiente a la recepcion; bloquear datos en revision (Art. 9 inc. 4) mientras corre |
| LPDP 18 inc. 3 (prevencion) | 10 | dh | "dia siguiente al de la notificacion" de la prevencion | No | No; una sola prevencion | Plazo del titular; si no subsana, archivo con derecho a nueva solicitud; el software debe impedir segunda prevencion |
| LPDP 19 (incompetencia) | 5 | dh | "recepcion" de la solicitud | No | No | Devolver al titular; cierra el expediente |
| LPDP 20 (respuesta ARCO-POL) | 20 | dh | Recepcion de la solicitud (Art. 9 y Lineamientos 34) | Prevencion (ver 4.4) | Hasta 20 dh mas "por causas justificadas" | Alerta al dia 10 y 15; prorroga solo antes del vencimiento, motivada y notificada en 3 dh (Lineamientos 34) |
| LPDP 21 inc. 3 (aviso a receptores) | 5 | dh | "determinacion de la procedencia" de la solicitud | No | No | Tarea derivada automatica al resolver procedente una rectificacion, actualizacion o eliminacion cuando hubo transferencias |
| LPDP 22 inc. final (denegatoria motivada) | 3 | dh | "adopcion de la decision" | No | No | Generar resolucion motivada y notificarla por el medio senalado por el titular; adjuntar pruebas |
| LPDP 25 (vulneracion) | 72 | horas | "desde que se tuvo conocimiento" | No | No | Reloj corrido por defecto (ver 2.5); tres destinatarios: ACE, FGR, titulares; revision exhaustiva dentro del mismo plazo |
| LPDP 30 inc. 1 (revocacion) | 5 | dh | "recepcion" de la solicitud de revocacion | No | No | Ejecutar revocacion y documentar |
| LPDP 30 inc. 2 (aviso al encargado) | 5 | dh | "fecha de emision" de la resolucion de revocacion | No | No | Tarea derivada si existe encargado |
| LPDP 60 inc. 1 | 3 | meses | Vigencia de la ley (23 nov 2024) | - | - | Plazo de la ACE, historico (vencio 23 feb 2025) |
| LPDP 60 inc. 2 | 3 | meses | "emision de las referidas disposiciones" por la ACE | - | - | Contar de fecha a fecha desde cada instrumento ACE (p. ej. Lineamientos y Normativa: vigentes 19 ago 2026, adecuacion hasta 19 nov 2026 si se toma la vigencia; si se toma la fecha de emision, 24 jul 2026, hasta 24 oct 2026). INCERTIDUMBRE sobre el dies a quo |
| LPDP 61 inc. 2 | 6 | meses | Vigencia de la ley | - | - | Historico (vencio 23 may 2025) |
| LPDP 64 | 8 | dias | Publicacion en D.O. (15 nov 2024) | - | - | Vigente 23 nov 2024 (hecho verificado en contexto) |

### 4.2 Plazos de los Lineamientos para el Delegado (ACE, 2026)

| Art. | Plazo | Unidad | Evento que lo inicia | Regla propuesta |
|---|---|---|---|---|
| 8 | 3 | dh | Designacion del delegado | Notificar al delegado su nombramiento y conservar constancia |
| 10 inc. 1 | 15 | dh | "dia siguiente del nombramiento" | Comunicar a la Direccion de Proteccion de Datos de la ACE por la plataforma de registro |
| 10 inc. 3 | 10 | dh | Modificacion de datos del delegado | Actualizar la plataforma |
| 12 inc. 1 | 15 | dh | Cumplimiento de requisitos | Plazo de la ACE para emitir credencial |
| 12 inc. 2 | 10 | dh | "no inscripcion" notificada por la ACE | Nombrar otro delegado |
| 17 inc. final | 15 | dh | Nombramiento de sustituto por cesacion o suspension | Informar a la ACE |
| 18 | 3 | anos | Nombramiento (verificacion periodica) | Recordatorio de verificacion de idoneidad al menos cada 3 anos |
| 19 | 10 | dh | "ocurrencia del hecho" de cesacion o suspension | Designar nuevo delegado |
| 21 | 6 | meses | Ultimo intento reprobado de certificacion | Nuevo intento |
| 22 | 1 | ano | Anual | Capacitacion del delegado; plan anual de capacitacion al personal |
| 30 | 2 veces | por ano | Anual | Informe del delegado al responsable |
| 31 | 10 | anos | Documentacion de autorizacion y publicacion del aviso | Retencion minima (ver seccion 6) |
| 33 inc. 2 | 3 | dh | "emision" de cada actuacion (admision, prevencion, subsanacion, reconocimiento, incompetencia, denegatoria, resolucion final) | Notificar cada actuacion; el motor genera subplazo por actuacion |
| 33 inc. 4 | 10 | dh | Notificacion de la resolucion al titular | Plazo del titular para reclamar ante la ACE; el motor lo muestra como "ventana de reclamo" |
| 34 inc. 2 | 3 | dh | Decision de prorrogar | Notificar la prorroga "siempre que ... se realice dentro del plazo ordinario de respuesta" |
| 36 | 5 | anos | Cese en el cargo | Deber de confidencialidad del delegado |
| 40 inc. 2 | 20 | dh | Vigencia de los lineamientos (19 ago 2026) | Registro transitorio; segun contexto, dejado sin efecto por la ACE tras la reforma (CONDICIONAL) |
| 42 | 8 | dias | "dia siguiente de su publicacion" (11 ago 2026) | Vigencia 19 ago 2026 (hecho verificado) |

### 4.3 Plazos de la Normativa del Procedimiento Administrativo Sancionador (ACE, 2026) y Ley de Ciberseguridad

| Norma / Art. | Plazo | Unidad | Evento que lo inicia | Suspension / prorroga | Regla propuesta |
|---|---|---|---|---|---|
| Normativa 12 | 90 | dh | "dia siguiente habil a la emision del informe" de apertura de diligencias preliminares | Prorrogable "de conformidad a lo establecido en la LPA" (Art. 83: hasta la mitad) | Registrar la fecha del informe si la empresa lo conoce |
| Normativa 19 y 21 | 5 | dh | "dia siguiente habil a la notificacion de la resolucion de inicio" | Art. 25: suspension del plazo para concluir si hay inspecciones, peritajes | Contestar el emplazamiento; presentar alegatos, documentos y proponer prueba; silencio = hechos contestados negativamente |
| Normativa 23 | 5 y 15 | dh | Allanamiento | - | Remision del expediente en 5 dh; resolucion final en 15 dh |
| Normativa 29 | 10 | dh | Apertura de alegatos finales (solo via ordinaria) | - | Ampliar prueba y alegatos |
| Normativa 30 | 8 | dh | "dia siguiente habil" al cierre de prueba o alegatos | - | Plazo interno de la ACE |
| Normativa 31 | 5 | dh | Notificacion del cambio a via ordinaria | - | Alegaciones |
| Normativa 32 | 15 | dh | Recepcion del expediente por el Director | Art. 39: suspension segun LPA 90; Art. 40: suspension por caso fortuito o fuerza mayor (LPA 94) | Resolucion final; sin recurso en via simplificada (queda contencioso administrativo); en via ordinaria, recursos LPA (Art. 33) |
| Normativa 34 | 72 | horas | Resolucion final sancionatoria | - | Aviso de la ACE a la FGR |
| Normativa 35 | 15 | dias calendario | Adopcion de medidas provisionales previas | - | Auto de inicio debe emitirse en ese plazo o las medidas caducan (imagen page-08 confirma "dias calendario") |
| Normativa 44 | 15 | dh | Notificacion de la multa | - | Pago en Colecturia Central o DGT; si no, cobro ejecutivo via FGR (Art. 45) |
| Normativa 47 | 5 | anos | Segun LPA 149 (dia siguiente a la infraccion; en continuadas, ultimo hecho) | Interrupcion por inicio del procedimiento con conocimiento del presunto responsable | Base de la retencion de evidencia (seccion 7) |
| Normativa 49 | 8 | dias | Publicacion en D.O. (11 ago 2026) | - | Vigente 19 ago 2026 |
| Ley de Ciberseguridad (D.L. 143) Art. 28 | - | - | Procedimiento simplificado de la LPA (Art. 158) | - | Concordante con Normativa Art. 4 |
| Ley de Ciberseguridad Art. 29 | 5 | anos | "Las infracciones y sanciones contempladas en la presente ley prescribiran a los cinco anos" | LPA 149 | Igual que Normativa 47 |
| LPA 158 num. 2 y 4 | 5 y 15 | dias (habiles por Art. 82) | Notificacion del acuerdo de inicio; ultima actuacion | LPA 90 | Referencia supletoria |
| LPA 89 | 9 meses / 20 dias | meses / dias | Inicio del procedimiento / presentacion de peticion simple | LPA 90 | Plazo maximo de la ACE para concluir |

Fuente Ley de Ciberseguridad: https://www.asamblea.gob.sv/sites/default/files/documents/decretos/D056D9A1-299D-4188-941A-9C3B5898D3F3.pdf (2026-09-23), Arts. 28 y 29 transcritos del PDF oficial.

### 4.4 La prevencion suspende el plazo de 20 dias?

La LPDP no lo dice. Art. 18 solo regula la prevencion y su efecto de archivo. Argumentos para sostener que SI suspende: (a) LPA Art. 90 num. 1, supletoria por Art. 62 LPDP, suspende el plazo maximo para resolver "cuando deba requerirse a cualquier interesado para la subsanacion de deficiencias ... por el tiempo que medie entre la notificacion del requerimiento y su efectivo cumplimiento ... o, en su defecto, el transcurso del plazo concedido"; (b) los Lineamientos Art. 33 enumeran "admision, prevencion, subsanacion" como actuaciones del mismo procedimiento, lo que presupone que el procedimiento sigue vivo durante la prevencion; (c) la Normativa sancionadora Art. 39 aplica expresamente el Art. 90 LPA a sus propios plazos, mostrando el criterio de la ACE. Argumento en contra: Art. 56 lit. b num. 2 sanciona no atender "en el tiempo y forma establecidos por la presente ley", y la ley no menciona suspension; un titular podria alegar que los 20 dh corren desde la recepcion original.

Regla propuesta (CONDICIONAL, requiere abogado): el motor computa dos fechas: "vencimiento con suspension" (los 20 dh se detienen desde la notificacion de la prevencion hasta la subsanacion o hasta el vencimiento de los 10 dh) y "vencimiento sin suspension" (20 dh desde la recepcion original). Por defecto planifica el trabajo con la fecha mas exigente (sin suspension) y documenta la decision del cliente si elige la otra; en ambos casos guarda el fundamento.

### 4.5 Prorroga del Art. 20

Requisitos acumulados: "causas justificadas"; no exceder "otros veinte dias habiles"; decision motivada; notificacion al interesado en 3 dh "siempre que dicha notificacion se realice dentro del plazo ordinario de respuesta" (Lineamientos 34 inc. 2, imagen page-10 confirma). Por analogia con LPA 83, la prorroga debe acordarse antes del vencimiento. Regla: el software impide registrar una prorroga despues del dia 20 y exige el texto de la justificacion.

---

## 5. Periodos de retencion legal en leyes conexas

Estos plazos condicionan la eliminacion de datos por dos vias de la LPDP: Art. 10 inc. 2 lit. b ("no procedera la solicitud de cancelacion ... si contraviene lo establecido por una obligacion legal") y lit. f (archivo en interes publico o "formulacion, ejercicio o defensa de reclamaciones"); Art. 11 (bloqueo: conservar los datos "unicamente ... a disposicion de la Administracion Publica, Jueces y Tribunales ... en los plazos establecidos para el resguardo segun las leyes aplicables"); Art. 5 lit. h (temporalidad); Art. 5 lit. g num. 3 (obligacion legal como base de licitud).

### 5.1 Codigo de Comercio

Fuente: texto oficial, https://www.asamblea.gob.sv/sites/default/files/documents/decretos/171117_072920482_archivo_documento_legislativo.pdf (2026-09-23).

- Art. 451: "Los comerciantes y sus herederos o sucesores conservaran los registros de su giro en general por diez anos y hasta cinco anos despues de la liquidacion de todos sus negocios mercantiles. Todo sin perjuicio de lo dispuesto en el Art. 455. El Registrador no concedera matricula de empresa, o cancelara la ya concedida, al que haya infringido lo dispuesto en este articulo."
- Art. 454: "Las cartas, telegramas y facturas que reciban y las copias de las que expidan los comerciantes, que sirvan de comprobantes para los aspectos contables, se consideraran anexas a la contabilidad y deberan conservarse durante el tiempo indicado en el Art. 451."
- Art. 455: los comerciantes pueden usar microfilm, discos opticos u otro medio de archivo "una vez transcurridos por lo menos veinticuatro meses desde la fecha de su emision"; las reproducciones certificadas por notario tienen el mismo valor probatorio.

**Norma:** Codigo de Comercio
**Articulo:** 451, 454, 455
**Obligacion:** conservar registros del giro 10 anos (y hasta 5 anos tras la liquidacion) y la correspondencia y facturas que sirvan de comprobante contable por el mismo plazo.
**A quien aplica:** comerciantes (individuales y sociales).
**Implicacion para el software:** los datos personales contenidos en facturas, contratos, correspondencia comercial y registros contables tienen un "bloqueo por obligacion legal" de 10 anos; una solicitud de cancelacion sobre esos datos debe resolverse como bloqueo (Art. 11 LPDP), no como borrado; el motor debe permitir etiquetar cada categoria de dato con su periodo legal y calcular la fecha de elegibilidad para borrado.
**Fuente oficial:** enlace citado (2026-09-23)
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (para datos que integran registros o comprobantes mercantiles)

### 5.2 Codigo Tributario

Fuente: texto oficial consolidado, https://elsalvador.eregulations.org/media/Codigo%20Tributario.pdf y https://www.asamblea.gob.sv/taxonomy/term/2291 (2026-09-23).

- Art. 147: "Las personas o entidades, tengan o no el caracter de contribuyentes, responsables, agentes de retencion o percepcion, auditores o contadores, deberan conservar en buen orden y estado, por un periodo de diez anos contados a partir de su emision o recibo, la siguiente documentacion, informacion y pruebas: a) Los libros de contabilidad y los comprobantes de orden interno y externo, registros especiales, inventarios, libros del IVA ... Cuando la contabilidad sea llevada en forma computarizada, deberan conservarse los medios magneticos que contengan la informacion, al igual que los respectivos programas para su manejo ...; b) Las informaciones y documentacion que este Codigo exija y aquella relacionada con la concesion de algun beneficio fiscal; c) Las pruebas del entero de las retenciones, percepciones y anticipos a cuenta realizados; d) Copia de las declaraciones tributarias presentadas y de los recibos de pago efectuados; e) La documentacion de las operaciones realizadas con sujetos relacionados ...". El texto lleva la marca de reforma (9); la reforma que amplio el plazo de cinco a diez anos se atribuye al D.L. 233 de 2009 segun fuentes secundarias (confianza baja sobre el numero de decreto; el plazo de diez anos si esta en el texto vigente).
- Art. 84: "La obligacion tributaria sustantiva prescribe en diez anos. Las multas y demas accesorios prescriben junto con la obligacion a que acceden. Las multas impuestas aisladamente prescriben en diez anos. El computo del plazo de prescripcion comenzara a contar a partir del dia siguiente a aquel en que concluyo el termino legal o el de su prorroga para pagar ..."
- Art. 175: caducidad de la facultad fiscalizadora: 3 anos para liquidaciones presentadas en plazo (5 anos si no se presento liquidacion); 3 anos para sanciones aisladas "contados desde el dia siguiente al que se cometio la infraccion" (5 anos sin liquidacion).

La Ley de Impuesto sobre la Renta no contiene un plazo propio de conservacion distinto del CTrib en los textos revisados; los comprobantes de renta, retenciones (incluidas las de salarios) y planillas como soporte de deducciones quedan cubiertos por el Art. 147 CTrib (10 anos desde emision o recibo). Confianza media (no se hizo lectura articulo por articulo de la Ley ISR).

**Norma:** Codigo Tributario
**Articulo:** 147 (conservacion), 84 (prescripcion), 175 (caducidad)
**Obligacion:** conservar 10 anos desde emision o recibo la documentacion contable, comprobantes, retenciones, declaraciones y medios magneticos y programas.
**A quien aplica:** toda persona o entidad, sea o no contribuyente.
**Implicacion para el software:** categoria de datos "soporte tributario" con retencion de 10 anos desde la fecha del documento; las nominas, recibos de pago y retenciones de empleados quedan comprendidas; bloquear borrado hasta la fecha calculada; el software debe conservar tambien los programas o formatos necesarios para leer los medios (Art. 147 lit. a).
**Fuente oficial:** enlaces citados (2026-09-23)
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 5.3 Codigo de Trabajo

Fuente: PDF oficial de la Asamblea citado en 3.1.

- Art. 18: el contrato individual "debera constar por escrito, en tres ejemplares; cada parte contratante conservara uno de estos y el patrono remitira el tercero a la Direccion General de Trabajo, dentro de los ocho dias siguientes". No fija plazo de conservacion.
- Art. 138: "Todo patrono esta obligado a llevar planillas o recibos de pago en que consten ... los salarios ordinarios y extraordinarios ...; las horas ordinarias y extraordinarias ...; y los dias habiles, de asueto y de descanso en que laboren." No fija plazo de conservacion.
- Prescripcion (Arts. 610 a 616): 60 dias para acciones por terminacion de contrato y despido (Art. 610), prestaciones por enfermedad, accidente y maternidad (Art. 611) y acciones residuales (Art. 616); 180 dias para salarios, descanso semanal, asuetos, vacaciones y aguinaldos (Art. 613) y devolucion de anticipos (Art. 614); 2 anos para indemnizacion por riesgo profesional "contados a partir de la fecha del accidente o de la primera constatacion medica de la enfermedad" (Art. 615).

No se localizo en el CT un plazo expreso de conservacion de planillas, contratos o expedientes del trabajador. Criterio practico: (a) mientras dure la relacion laboral, obligacion de llevar y exhibir (Art. 138); (b) tras el cese, al menos hasta que prescriban las acciones laborales (60 a 180 dias; 2 anos para riesgo profesional; sin perjuicio de plazos de seguridad social) y, para las planillas como comprobante de gasto y de retenciones, 10 anos por CTrib 147. El expediente laboral puede contener datos sensibles (salud); su retencion debe justificarse por obligacion legal o defensa de reclamaciones (Art. 10 inc. 2 lit. b y f LPDP).

**Norma:** Codigo de Trabajo
**Articulo:** 18, 138, 610 a 616
**Obligacion:** llevar contratos escritos y planillas; sin plazo de conservacion expreso; prescripciones de 60 y 180 dias y 2 anos.
**A quien aplica:** patronos.
**Implicacion para el software:** categoria "expediente laboral" con retencion minima recomendada = duracion de la relacion + 2 anos (riesgo profesional) y, para nomina y retenciones, 10 anos (CTrib 147); marcar como RECOMENDADO el exceso sobre lo tributario.
**Fuente oficial:** PDF de la Asamblea (2026-09-23)
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (llevar planillas y contratos); RECOMENDADO (plazo de retencion post cese, salvo lo tributario)

### 5.4 Ley Contra el Lavado de Dinero y de Activos (D.L. 498/1998 y reformas) e Instructivo UIF

Fuente: texto consolidado publicado por la SSF, https://ssf.gob.sv/wp-content/uploads/2022/07/Ley-contra-el-lavado-de-dinero-y-de-Activos-D498.pdf (2026-09-23); Instructivo de la UIF para la Prevencion del Lavado de Dinero y de Activos, Acuerdo No. 380 del Fiscal General, version con reformas de septiembre de 2023, https://www.uif.gob.sv/wp-content/uploads/instructivos/Instructivo_UIF_Reformas_Septiembre_2023.pdf (2026-09-23). Segun fuente secundaria (Lexology, Central Law) el instructivo se publico en el D.O. el 27 oct 2021.

- LCLDA Art. 10 lit. b: los sujetos obligados deben "archivar y conservar la documentacion de las operaciones por un plazo de cinco anos, contados a partir de la fecha de la finalizacion de cada operacion. Por igual plazo deberan archivar y conservar datos de identificacion, archivos de cuentas y correspondencia comercial de sus clientes, a partir de la terminacion de una cuenta o relacion comercial."
- LCLDA Art. 12: "Los sujetos obligados deben mantener por un periodo no menor de quince anos los registros necesarios sobre transacciones realizadas, tanto nacionales como internacionales, que permitan responder con prontitud a las solicitudes de informacion de los organismos de fiscalizacion o supervision correspondientes, de la Fiscalia General de la Republica y de los tribunales competentes ... Tales registros serviran para reconstruir cada transaccion".
- Instructivo UIF Art. 57 y 58: los reportes de operaciones sospechosas, comunicaciones de la UIF y la documentacion aclaratoria de inusualidades "se conservara por un periodo no menor a quince anos, en los terminos previstos en el Articulo 12 de la LCLDA". Art. 59 (Tiempo de conservacion de la documentacion): "El sujeto obligado debe mantener a traves de medios impresos, digitales o electronicos, toda la documentacion e informacion que ampara la apertura de cuentas o relaciones contractuales, copia de documentos de identificacion y transacciones, los cuales se conservaran por un periodo no menor a quince anos". Los fiduciarios conservan la informacion basica del fideicomiso "al menos quince (15) anos luego de que cese su vinculacion".

Observacion: hay una aparente dualidad 5 anos (Art. 10 lit. b, datos de identificacion y correspondencia) frente a 15 anos (Art. 12, registros de transacciones; el Instructivo extiende los 15 anos a la documentacion de apertura e identificacion). El criterio prudente para un sujeto obligado es 15 anos. Los "sujetos obligados" del Art. 2 LCLDA incluyen a instituciones financieras y a un catalogo amplio de actividades y profesiones no financieras designadas; determinar si un cliente concreto es sujeto obligado requiere abogado.

**Norma:** LCLDA e Instructivo UIF (Acuerdo 380)
**Articulo:** LCLDA 10 lit. b y 12; Instructivo 57, 58, 59
**Obligacion:** conservar 5 anos la documentacion de operaciones y datos de identificacion desde el fin de la relacion, y no menos de 15 anos los registros de transacciones y, segun el Instructivo, la documentacion KYC de apertura e identificacion.
**A quien aplica:** sujetos obligados del Art. 2 LCLDA.
**Implicacion para el software:** si el cliente se marca como sujeto obligado LCLDA, la categoria "KYC y transacciones" recibe retencion de 15 anos desde el fin de la relacion o de la transaccion; las solicitudes de cancelacion sobre esos datos se resuelven como bloqueo.
**Fuente oficial:** enlaces citados (2026-09-23)
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (solo sujetos obligados LCLDA); dentro de ellos, OBLIGATORIO

### 5.5 Ley de Bancos y normas del sistema financiero

En el texto de la Ley de Bancos (D.L. 697/1999, version SSF, https://www.ssf.gob.sv/descargas/Leyes/Leyes%20Financieras/Ley%20de%20Bancos.pdf) no se localizo un articulo que fije un plazo de conservacion de documentos en anos; las coincidencias con "conservar" se refieren a bienes y acciones. Segun fuente secundaria, el Art. 32 inciso final de la Ley de Supervision y Regulacion del Sistema Financiero autoriza a los integrantes del sistema a archivar por microfilm, discos opticos y medios electronicos, y el Banco Central de Reserva aprueba normas tecnicas sobre "conservacion y archivo de documentacion" (considerando V de la NRP-23, Normas Tecnicas para la Gestion de la Seguridad de la Informacion, CNBCR-07/2020, vigente 1 jul 2020, https://ssf.gob.sv/descargas/upload/NRP-23.pdf). La NRP-23 no fija anos de retencion. No se identifico la norma tecnica especifica con plazos. INCERTIDUMBRE: para clientes del sector financiero, el periodo de retencion regulatorio debe confirmarse con la normativa BCR/SSF aplicable a cada tipo de entidad, ademas de LCLDA (15 anos) y CTrib (10 anos).

**Clasificacion:** CONDICIONAL (solo entidades supervisadas); plazo especifico NO VERIFICADO.

### 5.6 Expediente clinico: Ley de Deberes y Derechos de los Pacientes y Norma Tecnica del Expediente Clinico

Fuente primaria: Norma Tecnica del Expediente Clinico (MINSAL), publicada en D.O. Tomo 444, No. 158, 22 ago 2024, con reforma publicada en D.O. No. 55, Tomo 450, 19 mar 2026, https://asp.salud.gob.sv/regulacion/pdf/norma/normatecnicadelexpedienteclinico-Acuerdo-Ejecutivo-1616-30052024_v1-reforma1.pdf (2026-09-23). La Ley de Deberes y Derechos de los Pacientes y Prestadores de Servicios de Salud (a la que remite el Art. 39 LPDP) atribuye al MINSAL la emision de la norma tecnica del expediente (segun fuente secundaria, Art. 5; no transcrito de fuente primaria).

- Definiciones 15 y 16: expediente activo (registros continuos) y pasivo ("en los ultimos 5 anos posteriores a la ultima consulta, no ha tenido ningun registro de atencion"), en el "ambito publico y privado".
- Art. 34 (Disposicion final): "a) Los expedientes clinicos deben ser revisados, como minimo una vez al ano, para identificar aquellos que no han tenido movimiento en los ultimos cinco anos, contados a partir de la ultima fecha de atencion en salud, estos deben conservarse cinco anos mas en archivo pasivo. ... a) Todas las instituciones del SNIS deben conservar durante diez anos los expedientes clinicos, considerando el tiempo que el expediente permanece en activo y en pasivo. b) Si el paciente no asiste al establecimiento despues de haber estado su expediente clinico en archivo pasivo por cinco anos, estos deben ser eliminados ... c) Los expedientes clinicos sujetos a investigacion o procesos judiciales deben conservarse integramente mientras dure el proceso ... d) La eliminacion de los expedientes clinicos se documentara por medio de actas".
- Art. 35: fallecidos por causa natural, 5 anos en archivo pasivo desde la defuncion; por violencia, accidentes de transito o en investigacion, 10 anos.

**Norma:** Norma Tecnica del Expediente Clinico (MINSAL) en desarrollo de la Ley de Deberes y Derechos de los Pacientes
**Articulo:** definiciones 15 y 16; Arts. 34 y 35
**Obligacion:** conservar el expediente clinico 10 anos (5 activo + 5 pasivo desde la ultima atencion); eliminacion documentada por acta; conservacion integra durante procesos judiciales.
**A quien aplica:** establecimientos del Sistema Nacional Integrado de Salud, publicos y privados.
**Implicacion para el software:** categoria "expediente clinico" (datos sensibles) con retencion de 10 anos desde la ultima atencion, bloqueo durante procesos judiciales y generacion de acta de eliminacion; el ejercicio de cancelacion por el paciente se resuelve como improcedente o bloqueo mientras corre el plazo.
**Fuente oficial:** enlace MINSAL (2026-09-23)
**Vigencia:** VIGENTE (MODIFICADA en 2026)
**Clasificacion:** CONDICIONAL (solo prestadores de salud); dentro de ellos, OBLIGATORIO

### 5.7 Sistema de pensiones

La Ley del Sistema de Ahorro para Pensiones (D.L. 927/1996) fue derogada por la Ley Integral del Sistema de Pensiones (D.L. 614/2022), Art. 162, texto en https://ssf.gob.sv/wp-content/uploads/2023/02/Ley-Integral-del-Sistema-de-Pensiones.pdf (2026-09-23). En la LISP no se localizo un plazo expreso de conservacion de expedientes de afiliados o planillas previsionales para empleadores o AFP; el unico plazo de conservacion hallado es el Art. 63 (el BCR conserva 10 anos los valores no reclamados de una AFP en liquidacion). INCERTIDUMBRE: los plazos de conservacion de planillas previsionales pueden estar en reglamentos o normas tecnicas de la SSF no revisados. Recomendacion: para planillas de cotizacion previsional y de ISSS, retener al menos 10 anos por su caracter de comprobante tributario (CTrib 147) y hasta confirmar la norma previsional.

**Clasificacion:** INCERTIDUMBRE (plazo no localizado); RECOMENDADO 10 anos por analogia tributaria.

### 5.8 Ley de Firma Electronica (D.L. 133/2015, reformada) y Ley de Comercio Electronico (D.L. 463/2019)

Fuente: Ley de Firma Electronica, https://factura.gob.sv/wp-content/uploads/2022/10/Ley_de_Firma_Electr%C3%B3nica.pdf; Ley de Comercio Electronico, https://www.jurisprudencia.gob.sv/DocumentosBoveda/D/2/2020-2029/2020/02/DB418.PDF (2026-09-23).

- Ley de Firma Electronica Art. 13: "Si la ley exige que la informacion contenida en un mensaje de datos conste por escrito y que sea conservada por un periodo determinado de tiempo, ese requisito se dara por cumplido si la informacion que contiene el mensaje de datos, se conserva en un proveedor de almacenamiento de documentos electronicos. En cuanto a la conservacion realizada por cuenta propia, se tendra por cumplida la exigencia ... cuando se cumplan los requisitos minimos ... previstos en el articulo 13-A".
- Art. 13-A: requisitos minimos: "a) Que la informacion que contenga pueda ser consultada en cualquier momento; b) Que se garantice la conservacion del formato en que se genero, archivo o recibio, o en algun formato que sea demostrable que reproduce con exactitud la informacion generada o recibida; y, c) Que se mantenga integro, legible, completo y sin alteraciones."
- Art. 14: el almacenamiento debe garantizar legibilidad, integridad, seguridad, autenticidad, fecha y hora de almacenamiento, recuperacion y cumplimiento de reglamentos de la Unidad de Firma Electronica; la omision hace "perder el valor legal" del documento almacenado.
- Ley de Comercio Electronico Art. 26 (Conservacion de los mensajes de datos): "Los proveedores de bienes y servicios estan obligados a conservar la informacion por el plazo que de acuerdo a la normativa aplicable al giro de su actividad les corresponda."

**Norma:** Ley de Firma Electronica y Ley de Comercio Electronico
**Articulo:** LFE 12, 13, 13-A, 14; LCE 26
**Obligacion:** no fijan anos; remiten al plazo que exija la ley del giro; imponen requisitos de forma para que la conservacion electronica valga como conservacion legal.
**A quien aplica:** todo el que conserve electronicamente documentos que la ley exige conservar; proveedores de bienes y servicios en linea.
**Implicacion para el software:** los registros de evidencia (consentimientos electronicos, avisos, resoluciones ARCO-POL, logs) deben almacenarse cumpliendo 13-A y 14: consultables en cualquier momento, formato original o reproduccion exacta demostrable, integridad verificable, sello de fecha y hora; de lo contrario pueden perder valor probatorio ante la ACE (Art. 54 LPDP, carga de la prueba del consentimiento).
**Fuente oficial:** enlaces citados (2026-09-23)
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (requisitos de forma) / CONDICIONAL (plazo, segun ley del giro)

### 5.9 Ley de Acceso a la Informacion Publica

Fuente: texto reformado 2025 publicado por el IAIP, https://www.iaip.gob.sv/wp-content/uploads/2025/03/LAIP-REFORMADA-2025.pdf (2026-09-23). Arts. 40 a 44: el IAIP emite lineamientos de "administracion, catalogacion, conservacion y proteccion" de informacion publica; los entes obligados crean sistemas de archivo y designan un responsable de archivos; la informacion del ano en curso y del ano anterior debe estar disponible. La ley no fija anos de conservacion; los plazos estan en los lineamientos y tablas de plazos de conservacion documental de cada institucion. El Art. 63 LPDP derogo las disposiciones de la LAIP sobre datos personales. Relevancia para el producto: solo para clientes que sean entes obligados LAIP (sector publico, fuera del alcance principal) o encargados que traten datos por cuenta de ellos.

**Clasificacion:** CONDICIONAL (sector publico); plazo no fijado en la ley.

### 5.10 Retenciones impuestas por la propia LPDP y la ACE

- Lineamientos ACE Art. 31 inc. 2: "La autorizacion y cualquier operacion relacionada con su publicacion [del aviso de privacidad] seran documentadas por el Delegado. Esta documentacion se conservara por el responsable, en formato fisico o digital, durante un plazo minimo de diez anos, sin perjuicio de lo que dispongan otras leyes o tratados internacionales aplicables." Confirmado en imagen page-09.
- LPDP Art. 25 inc. final: documentar toda vulneracion "la cual estara a disposicion de la autoridad encargada de la materia" (sin plazo).
- LPDP Art. 54: carga de la prueba del consentimiento y de la comunicacion del aviso recae en el responsable (sin plazo; el plazo util es el de prescripcion, seccion 6).
- Lineamientos Art. 8 inc. 2: conservar constancia de la notificacion del nombramiento al delegado (sin plazo). Art. 22: conservar documentacion de la capacitacion (sin plazo).

**Norma:** Lineamientos para el Delegado (ACE)
**Articulo:** 31
**Obligacion:** conservar 10 anos la documentacion de autorizacion y publicacion del aviso de privacidad.
**A quien aplica:** responsables (hasta la reforma, a traves del delegado).
**Implicacion para el software:** versionado del aviso de privacidad con evidencia de autorizacion, publicacion y retiro, retenido 10 anos desde cada operacion.
**Fuente oficial:** `lineamientos_dpo_OCR.txt` y `ocr/lineamientos_dpo/page-09.png`; D.O. 146 Tomo 452, 11 ago 2026
**Vigencia:** VIGENTE (CONDICIONAL tras la reforma que suprime el delegado privado; la obligacion de conservar es del responsable y deberia subsistir)
**Clasificacion:** OBLIGATORIO

### 5.11 Tabla resumen de retencion legal

| Norma | Art. | Periodo | Desde | Datos afectados | Fuente |
|---|---|---|---|---|---|
| Codigo de Comercio | 451, 454 | 10 anos; hasta 5 tras liquidacion | Cada registro o documento | Registros del giro, cartas, facturas, comprobantes contables | asamblea.gob.sv |
| Codigo Tributario | 147 | 10 anos | Emision o recibo | Contabilidad, comprobantes, retenciones, declaraciones, medios magneticos y programas | eregulations / asamblea |
| Codigo de Trabajo | 18, 138 | Sin plazo expreso | - | Contratos, planillas, recibos | asamblea.gob.sv |
| LCLDA | 10 lit. b | 5 anos | Fin de operacion o relacion | Documentacion de operaciones, identificacion, cuentas, correspondencia | ssf.gob.sv |
| LCLDA | 12 | No menos de 15 anos | Cada transaccion | Registros de transacciones | ssf.gob.sv |
| Instructivo UIF | 57 a 59 | No menos de 15 anos | Apertura, transaccion, reporte | KYC, ROS, inusualidades | uif.gob.sv |
| Norma Tecnica Expediente Clinico | 34, 35 | 10 anos (5 activo + 5 pasivo); fallecidos 5 o 10 | Ultima atencion; defuncion | Expediente clinico | asp.salud.gob.sv |
| LISP | 63 | 10 anos (solo BCR, valores no reclamados) | Liquidacion de AFP | No aplica al empleador | ssf.gob.sv |
| Ley de Firma Electronica | 13, 13-A, 14 | El que exija la ley del giro | - | Cualquier mensaje de datos que deba conservarse | factura.gob.sv |
| Ley de Comercio Electronico | 26 | El del giro | - | Informacion de proveedores en linea | jurisprudencia.gob.sv |
| LAIP | 40 a 44 | Segun lineamientos IAIP | - | Informacion publica | iaip.gob.sv |
| Lineamientos ACE | 31 | Minimo 10 anos | Cada operacion sobre el aviso | Documentacion del aviso de privacidad | D.O. 11 ago 2026 |
| Lineamientos ACE | 36 | 5 anos | Cese del delegado | Deber de confidencialidad (no es retencion) | D.O. 11 ago 2026 |

---

## 6. Prescripcion de acciones como criterio de retencion

| Materia | Norma / Art. | Plazo | Computo | Fuente |
|---|---|---|---|---|
| Sancionadora LPDP | Ley de Ciberseguridad Art. 29; Normativa ACE Art. 47 | 5 anos (infracciones y sanciones) | LPA 149: dia siguiente a la infraccion; continuadas: ultimo hecho; interrupcion por inicio del procedimiento; sanciones: desde firmeza | asamblea.gob.sv; D.O. 11 ago 2026 |
| Civil, accion ejecutiva | CC 2254 | 10 anos | Desde que la accion nace (CC 2253) | oas.org (texto CC) |
| Civil, accion ordinaria | CC 2254 | 20 anos (10 si concurre con ejecutiva ya prescrita) | Idem | Idem |
| Civil, dano o dolo (responsabilidad extracontractual) | CC 2083 | 3 anos | "desde la perpetracion del acto" | Idem |
| Mercantil | C.Com 995 | 6 meses (rectificacion de saldos); 1 ano (nulidad de acuerdos sociales, cheque, vicios de la cosa, transporte, responsabilidad de administradores); 2 anos (compraventa, suministro, deposito, comision, hospedaje, garantia y otros contratos); 5 anos (contratos de credito, desde el ultimo reconocimiento) | Segun cada ordinal | asamblea.gob.sv |
| Laboral | CT 610, 611, 616 | 60 dias | Desde la causa | asamblea.gob.sv |
| Laboral, salarios y prestaciones | CT 613, 614 | 180 dias | Desde que debio pagarse | Idem |
| Laboral, riesgo profesional | CT 615 | 2 anos | Accidente o primera constatacion medica | Idem |
| Tributaria, obligacion sustantiva y multas | CTrib 84 | 10 anos | Dia siguiente al vencimiento del plazo de pago | eregulations |
| Tributaria, caducidad de fiscalizacion | CTrib 175 | 3 anos (5 sin liquidacion) | Segun literal | Idem |

Como usar estos plazos: un registro que sirve de prueba de cumplimiento (consentimiento, aviso, resolucion ARCO-POL, notificacion de incidente) debe conservarse al menos mientras la ACE pueda sancionar (5 anos desde el ultimo hecho relevante, mas la duracion de un eventual procedimiento) y mientras el titular pueda reclamar civilmente (3 anos por dano extracontractual; hasta 10 anos si la reclamacion es contractual ejecutiva). Los expedientes clinicos y KYC tienen ademas su plazo sectorial. Los datos que no son evidencia de cumplimiento se rigen por el principio de temporalidad (Art. 5 lit. h) y deben eliminarse al cumplirse la finalidad y el plazo legal aplicable.

---

## 7. Reglas propuestas para el motor de plazos (resumen operativo)

1. Unidad y calendario: todo plazo "dias habiles" usa capas 0 a 3 (empresa frente a titular) o capa 5 (empresa frente a ACE). Los plazos en "dias" sin calificativo de la LPA se tratan como habiles (Art. 82). Los plazos en meses o anos van de fecha a fecha. Los "dias calendario" (Normativa Art. 35) se cuentan corridos.
2. Inicio: el dia habil siguiente al evento (notificacion, recepcion, emision, decision, conocimiento) salvo que la norma diga "a partir de la recepcion", en cuyo caso el motor muestra tambien la fecha mas exigente.
3. Vencimiento: si cae en inhabil, se traslada al siguiente habil; el plazo vence a la hora de cierre del horario habil configurado o, por defecto, a la medianoche (CC 47), mostrando ambas.
4. Horas: 72 horas corridas por defecto; opcion configurable a horas habiles con constancia del criterio.
5. Suspension: solo por prevencion (Art. 18 LPDP) y solo si el cliente activa la regla "LPA 90.1"; se muestran ambas fechas.
6. Prorroga: unica, hasta 20 dh, motivada, acordada antes del vencimiento y notificada en 3 dh dentro del plazo ordinario.
7. Subplazos: cada actuacion genera un subplazo de notificacion de 3 dh (Lineamientos 33) y, si procede, tareas derivadas de 5 dh (Arts. 21 y 30 LPDP).
8. Evidencia: cada calculo guarda evento, marca de tiempo, calendario aplicado, criterio de computo, usuario y fecha; el registro se conserva segun la seccion 8.
9. Asuetos: el proveedor mantiene capas 1 y 2; el cliente mantiene capas 3 y 4 con fuente y fecha; los cambios de calendario recalculan plazos abiertos y registran el recalculo.
10. Ninguna regla del motor afirma cumplimiento legal; toda fecha se presenta como "fecha limite estimada segun criterio X" con enlace a la norma.

---

## 8. Tabla de retencion propuesta para los registros del propio software

| Registro | Retencion minima propuesta | Fundamento | Clasificacion |
|---|---|---|---|
| Expediente ARCO-POL (solicitud, prevencion, resoluciones, notificaciones, evidencia de entrega) | 5 anos desde el cierre del expediente; recomendado 10 anos | Prescripcion sancionadora 5 anos (Ley de Ciberseguridad 29; Normativa 47; LPA 149); infraccion grave Art. 56 lit. b num. 2 y muy grave lit. c num. 2 LPDP; reclamacion civil CC 2083 (3 anos) y 2254 (10 anos); analogia Lineamientos 31 (10 anos) | RECOMENDADO (5 anos); el exceso a 10 es buena practica |
| Registro de incidentes y notificaciones a ACE, FGR y titulares | 5 anos desde el cierre del incidente; recomendado 10 anos | LPDP 25 inc. final (documentar y tener a disposicion de la autoridad); infraccion leve Art. 56 lit. a num. 3; prescripcion 5 anos; responsabilidad civil | OBLIGATORIO documentar (sin plazo); RECOMENDADO el plazo |
| Consentimientos (texto presentado, version del aviso, marca de tiempo, medio, identificador del titular, revocaciones) | Vigencia del tratamiento + 5 anos desde el cese o revocacion; 10 anos si el mismo registro prueba la comunicacion del aviso | LPDP 54 (carga de la prueba); 56 lit. c num. 1, 9 y 10; prescripcion 5 anos; Lineamientos 31 (10 anos para documentacion del aviso); LFE 13-A y 14 (forma) | OBLIGATORIO conservar prueba (sin plazo legal); RECOMENDADO el plazo |
| Versiones del aviso y de la politica de privacidad, autorizaciones y publicaciones | 10 anos desde cada operacion | Lineamientos ACE 31 | OBLIGATORIO |
| Logs de auditoria del sistema (accesos, cambios, calculos de plazos, recalculos de calendario) | 5 anos; recomendado 10 anos para logs vinculados a expedientes y consentimientos | Principio de responsabilidad demostrada (Art. 5 lit. i); Politica ACE Art. 4 (control de acceso, auditorias) y Art. 8 lit. b (auditorias anuales); prescripcion 5 anos | RECOMENDADO |
| Nombramiento, notificacion y registro del delegado o del responsable interno; capacitaciones | 10 anos desde la cesacion; capacitaciones 5 anos | Lineamientos 8, 10, 22 (conservar constancias, sin plazo); analogia Art. 31; prescripcion 5 anos | CONDICIONAL (reforma 2026) / RECOMENDADO |
| Registro de actividades de tratamiento y EIPD | Vida del tratamiento + 5 anos | Politica ACE Art. 4 medidas organizativas d) y e); prescripcion 5 anos | RECOMENDADO |
| Contratos con encargados y receptores, evidencia de transferencias | Vigencia del contrato + 10 anos | LPDP 41 y 44; C.Com 451 y 454 (correspondencia y contratos como registros del giro); CC 2254 | OBLIGATORIO (mercantil) |
| Comunicaciones a la ACE (flujo transfronterizo Art. 45, requerimientos Art. 50 lit. t) | 10 anos | Analogia Art. 31; prescripcion 5 anos; C.Com 454 | RECOMENDADO |
| Datos personales del titular dentro del expediente ARCO-POL una vez cerrado | Minimizar: conservar solo lo necesario para probar el tramite; seudonimizar cuando sea posible | LPDP 5 lit. d y h; 4 lit. q | RECOMENDADO |

Regla de eliminacion: al vencer la retencion, el software propone eliminacion o anonimizacion con acta (analogia Norma Expediente Clinico Art. 34 lit. d), salvo bloqueo por proceso judicial o administrativo en curso (LPDP 11; Norma Expediente Clinico 34 lit. c).

---

## 9. Incertidumbres y puntos que requieren abogado

1. Aplicabilidad de la LPA a la relacion titular-empresa privada (Art. 62 LPDP frente a Art. 2 LPA). Recomendacion: aplicar Art. 82 LPA; confirmar con abogado y, si es posible, con consulta a la ACE (Art. 50 lit. o y s).
2. Computo de las 72 horas del Art. 25: corridas o habiles; efecto de que el conocimiento ocurra en dia inhabil. Recomendacion: corridas.
3. Sabado: inhabil por defecto. Confirmar si una empresa que labora sabados puede o debe contarlo como habil frente al titular.
4. Efecto suspensivo de la prevencion sobre los 20 dias del Art. 20 (LPA 90.1 por supletoriedad). El motor debe ofrecer ambas fechas hasta que exista criterio de la ACE o del abogado.
5. Dies a quo del plazo de 3 meses del Art. 60 inc. 2 LPDP respecto de cada nuevo instrumento de la ACE (emision 24 jul 2026 o vigencia 19 ago 2026).
6. Reforma D.L. 659 (sep 2026): vigencia pendiente de publicacion; todos los plazos y deberes ligados al delegado privado (Lineamientos 8, 10, 12, 17, 19, 22, 30, 33, 34, 36, 40) deben reevaluarse con el texto oficial; posible derogacion o modificacion de los Lineamientos por la ACE.
7. Fiestas patronales: no hay lista oficial; el software debe exigir fuente por sede. Reglamento de la Ley de Asuetos (Art. 3) no localizado.
8. Asuetos ad hoc 2025 y 2026: la lista oficial de decretos no muestra titulos con "asueto"; verificar por otros titulos ("Disposiciones especiales", "licencia remunerada").
9. Reforma LPA 2026 (D.L. 523): datos de D.O. y fecha de vigencia tomados de fuente secundaria y del titulo de un documento oficial; texto del Art. 4-A no transcrito.
10. Fecha de publicacion en D.O. de la LPA (13 feb 2018) y del Instructivo UIF (27 oct 2021): fuentes secundarias.
11. Ley de Bancos y normas BCR/SSF: no se localizo plazo de conservacion documental; confirmar la norma tecnica aplicable a cada entidad supervisada.
12. LISP y planillas previsionales: sin plazo localizado; posible regulacion en reglamentos o normas SSF.
13. Codigo de Trabajo: sin plazo de conservacion de planillas y contratos; el plazo propuesto es practico.
14. Reforma que llevo a 10 anos el Art. 147 CTrib: numero de decreto no verificado en fuente primaria (el plazo de 10 anos si esta en el texto vigente).
15. Ley de Deberes y Derechos de los Pacientes: fundamento de la norma tecnica (Art. 5) tomado de fuente secundaria; aplicabilidad de la Norma Tecnica a prestadores privados debe confirmarse (la norma habla de "instituciones del SNIS" y las definiciones incluyen el ambito privado).
16. Calidad de sujeto obligado LCLDA de cada cliente: determinacion caso por caso.
17. Horario habil: sin definicion legal; el criterio de "recepcion fuera de horario = siguiente dia habil" es propuesta, no norma.

---

## 10. Fuentes consultadas (todas al 2026-09-23)

Corpus local:
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt` (LPDP, D.L. 144/2024)
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\diario_oficial_2024-11-15_mh.txt` (D.O. 219, Tomo 445)
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_politicas_protecciondatos.txt` (Politicas N. 001-0309025-DPDP)
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\lineamientos_dpo_OCR.txt` y `ocr\lineamientos_dpo\page-09.png`, `page-10.png` (Lineamientos para el Delegado, D.O. 146 Tomo 452, 11 ago 2026)
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\normativa_sancionadora_OCR.txt` y `ocr\normativa_sancionadora\page-03.png`, `page-08.png` (Normativa PAS, mismo D.O.)
- `C:\Proyects\PRIV-SV\analisis\00_contexto_para_agentes.md` (hechos verificados)

Fuentes primarias en linea:
- LPA (D.L. 856/2017): https://www.asamblea.gob.sv/sites/default/files/documents/decretos/361DDB77-97E7-4EFF-B353-C6D872547E7C.pdf
- LPA consolidada con reforma 2026 (Direccion General de Aduanas): https://sitio.aduana.gob.sv/download/ley-de-procedimientos-administrativos-actualizada-con-el-d-o-no-41-t-450-27-de-febrero-de-2026/
- Decretos 2026 y 2025 de la Asamblea: https://www.asamblea.gob.sv/leyes-y-decretos/decretos-por-anios/2026/0 y /2025/0
- Ley de Ciberseguridad y Seguridad de la Informacion (D.L. 143/2024): https://www.asamblea.gob.sv/sites/default/files/documents/decretos/D056D9A1-299D-4188-941A-9C3B5898D3F3.pdf
- Codigo de Trabajo: https://www.asamblea.gob.sv/sites/default/files/documents/decretos/AD778A29-F1B3-495E-AE19-E2B05D93685D.pdf y extracto CSJ https://www.csj.gob.sv/wp-content/uploads/2021/06/11-Co%CC%81digo-de-Trabajo-de-El-Salvador-Di%CC%81as-de-asueto.pdf
- D.L. 339/2016 (Dia de la Madre): https://www.jurisprudencia.gob.sv/DocumentosBoveda/D/2/2010-2019/2016/04/B815C.PDF; listado de dias conmemorativos: https://www.asamblea.gob.sv/leyes-y-decretos/legislacion-genero/decretos-de-dias-conmemorativos
- D.L. 208/2012 (Dia del Padre), segun MTPS: https://www.mtps.gob.sv/2019/06/14/mtps-17-de-junio-asueto-remunerado-para-las-personas-trabajadoras/
- Ley de Asuetos, Vacaciones y Licencias de los Empleados Publicos: https://www.transparenciafiscal.gob.sv/downloads/pdf/DC5091_9_Ley_de_Asuetos_Vacaciones_y_Licencias_de_los_Empleados_Publicos.pdf y version con reformas 2022 https://www.andes21dejunio.com/wp-content/uploads/2024/04/LEY-DE-ASUETOS-VACACIONES-Y-LICENCIAS-EMPLEADOS-PUBLICO-CON-REFORMAS-2022.pdf
- Asuetos ad hoc: https://www.asamblea.gob.sv/node/12407 (16 sep 2022), https://www.asamblea.gob.sv/node/12612 (26 dic 2022 y 2 ene 2023), https://www.asamblea.gob.sv/node/13205 (18 jun 2024)
- Instructivo de Asuetos del Organo Judicial (2019): https://www.jurisprudencia.gob.sv/DocumentosBoveda/D/2/1900-1909/1900/01/E88E5.PDF
- Codigo de Comercio: https://www.asamblea.gob.sv/sites/default/files/documents/decretos/171117_072920482_archivo_documento_legislativo.pdf
- Codigo Tributario: https://elsalvador.eregulations.org/media/Codigo%20Tributario.pdf ; https://www.asamblea.gob.sv/taxonomy/term/2291
- Codigo Civil: https://www.oas.org/dil/esp/codigo_civil_el_salvador.pdf
- LCLDA: https://ssf.gob.sv/wp-content/uploads/2022/07/Ley-contra-el-lavado-de-dinero-y-de-Activos-D498.pdf
- Instructivo UIF (Acuerdo 380, reformas sep 2023): https://www.uif.gob.sv/wp-content/uploads/instructivos/Instructivo_UIF_Reformas_Septiembre_2023.pdf
- Ley de Bancos: https://www.ssf.gob.sv/descargas/Leyes/Leyes%20Financieras/Ley%20de%20Bancos.pdf ; NRP-23: https://ssf.gob.sv/descargas/upload/NRP-23.pdf
- Norma Tecnica del Expediente Clinico (MINSAL, 2024, reforma 2026): https://asp.salud.gob.sv/regulacion/pdf/norma/normatecnicadelexpedienteclinico-Acuerdo-Ejecutivo-1616-30052024_v1-reforma1.pdf
- Ley Integral del Sistema de Pensiones (D.L. 614/2022): https://ssf.gob.sv/wp-content/uploads/2023/02/Ley-Integral-del-Sistema-de-Pensiones.pdf
- Ley de Firma Electronica: https://factura.gob.sv/wp-content/uploads/2022/10/Ley_de_Firma_Electr%C3%B3nica.pdf
- Ley de Comercio Electronico (D.L. 463/2019): https://www.jurisprudencia.gob.sv/DocumentosBoveda/D/2/2020-2029/2020/02/DB418.PDF
- LAIP reformada 2025: https://www.iaip.gob.sv/wp-content/uploads/2025/03/LAIP-REFORMADA-2025.pdf

Fuentes secundarias (orientacion; marcadas como tales en el texto):
- Consortium Legal, "Reforma a la Ley de Procedimientos Administrativos en El Salvador", 11 mar 2026: https://consortiumlegal.com/2026/03/11/reforma-a-la-ley-de-procedimientos-administrativos-en-el-salvador/
- La Prensa Grafica, asueto 1 jun 2024: https://www.laprensagrafica.com/elsalvador/Aprueban-asueto-para-el-1-de-junio-por-toma-de-posesion-presidencial-20240522-0071.html
- El Diario de Hoy, "Asi quedan los asuetos de 2026", 2 ene 2026: https://www.eldiariodehoy.com/noticias/nacionales/asi-quedan-los-asuetos-de-2026-y-fines-de-semana-largos-en-el-salvador/55182/2026/
- elsalvador.com, vacaciones agostinas 2026 (21 jul 2026): https://www.elsalvador.com/noticias/nacional/vacaciones-fiestas-agostinas-el-salvador-asueto-nacional/1284556/2026/
- diario.elmundo.sv, asuetos de Navidad (22 nov 2024): https://diario.elmundo.sv/economia/que-dias-son-los-asuetos-remunerados-en-navidad-y-ano-nuevo
- Legal Spot SV, vacaciones agostinas 2026: https://legalspotsv.com/en/vacaciones-agostinas-2026-que-dias-son-asueto-y-como-debe-pagarse-si-se-trabaja/
- Lexology / Central Law sobre el Instructivo UIF 2021: https://www.lexology.com/library/detail.aspx?g=e8394f25-fb3c-4c69-a07d-85e7d7294d03
- TopTrabajos, feriados 2026: https://www.toptrabajos.com/sv/blog/pago-feriados-el-salvador/
