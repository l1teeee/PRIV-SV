# Sweep juridico: bases de licitud, consentimiento, datos sensibles, ninez, laboral y marketing

Proyecto: PRIV-SV. Lente asignado: bases de licitud, consentimiento, datos sensibles, menores, salud, laboral y marketing.
Fecha de consulta de todas las fuentes: 2026-09-23.
Norma principal: Ley para la Proteccion de Datos Personales (LPDP), Decreto Legislativo N. 144, D.O. N. 219, Tomo 445, 15 nov 2024, vigente desde el 23 nov 2024. Texto integro local: `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt`.

Advertencia de alcance: este informe describe lo que dicen las normas y como el software puede organizar, registrar y evidenciar su cumplimiento. No sustituye asesoria juridica. Donde la ley es ambigua se dice expresamente y se remite a abogado. La reforma aprobada el 17 sep 2026 (Decreto Legislativo N. 659) no altera, segun las fuentes secundarias disponibles, los articulos sobre bases de licitud, consentimiento, datos sensibles ni ninez; si altera quien recibe las solicitudes de revocacion (ya no el "delegado" sino el sujeto obligado). Al 2026-09-23 no esta confirmada su publicacion en el Diario Oficial, por lo que se trata como APROBADA-PENDIENTE-PUBLICACION.

---

## 1. Resumen ejecutivo del lente

1. La LPDP reconoce seis bases de licitud (Art. 5 lit. g: consentimiento, contrato o medidas precontractuales, obligacion legal, intereses vitales, interes publico o poderes publicos, interes legitimo). Pero el mismo Art. 5 lit. c enuncia un "principio de consentimiento y finalidad" que exige consentimiento "en el tratamiento y recoleccion de datos personales", el Art. 27 dice que "sera necesaria la obtencion del consentimiento", el Art. 32 prohibe tratar para fines distintos "sin previa autorizacion del titular" y la infraccion muy grave 1 del Art. 56 sanciona "tratar datos personales sin el consentimiento previo, de conformidad con lo establecido en el articulo 26". La ley es internamente ambigua: parece exigir consentimiento como regla y a la vez reconocer otras bases y excepciones (Art. 28). No hay lineamiento ni guia de la ACE que resuelva la ambiguedad al 2026-09-23.

2. Para el software, la consecuencia practica es: cada actividad de tratamiento debe tener registrada una base de licitud, una justificacion escrita y la evidencia asociada. El software nunca valida automaticamente que una base sea "correcta"; presenta las opciones de la ley, explica el riesgo de cada una y deja constancia de que la decision es de la empresa.

3. El consentimiento, cuando se usa, debe ser libre, especifico, informado, expreso e individualizado (Arts. 4 lit. d, 5 lit. c, 27), puede ser verbal, escrito o por signos inequivocos siempre que conste por medio fisico, electronico o tecnologico (Art. 26), la carga de probarlo y de probar que se comunico el aviso de privacidad es del responsable (Art. 54), y el aviso debe comunicarse por escrito al momento de otorgar el consentimiento (Art. 24 inc. final). Esto convierte al registro de evidencia de consentimiento en una funcion central del producto.

4. La revocacion es un derecho en cualquier momento, sin efecto retroactivo, por mecanismos expeditos, sencillos y gratuitos (Art. 29), con 5 dias habiles para proceder y 5 dias habiles para avisar al encargado (Art. 30). Tratar datos pese a la revocacion o no hacerla efectiva son infracciones muy graves 9 y 10 (26 a 40 salarios minimos del sector comercio, Art. 57 lit. c).

5. Los datos sensibles tienen definicion enunciativa (Art. 4 lit. g, incluye salud fisica y mental, biometria, genetica, origen etnico, religion, politica, afiliacion sindical, preferencias sexuales, habitos personales), consentimiento por escrito con firma autografa o equivalente (Art. 26 inc. 4), advertencia expresa del derecho a no prestarlo (Art. 37), prohibicion de crear bases de datos sensibles fuera de la ley (Art. 59 lit. a, infraccion grave 6) y son agravante en la Normativa Sancionadora de la ACE (Art. 32 y Art. 43 lit. e). La Ley de Firma Electronica equipara la firma electronica simple a la autografa en validez, con menor valor probatorio que la certificada (Art. 6). No existe lineamiento ACE sobre biometria, videovigilancia o cookies.

6. Ninez y adolescencia: la LPDP exige consentimiento de padres, representantes o tutores (infraccion muy grave 3) "de conformidad con las leyes vigentes", aplica el principio de ejercicio progresivo (Arts. 5 lit. j, 26 inc. 2) e informacion adaptada a la edad (Art. 42). La ley vigente es la Ley Crecer Juntos (D.L. 431, vigente desde 1 ene 2023, que derogo la LEPINA en su Art. 288): ninez hasta antes de los 12 anos, adolescencia de 12 a 18 (Art. 4); para uso de imagen y datos con fines comerciales el Art. 77 exige consentimiento del nino mas conocimiento y aprobacion de padres, y para adolescentes "bastara su consentimiento". Esa regla es mas flexible que la LPDP y genera una duda de coordinacion que requiere abogado. La LPDP no fija una edad de consentimiento digital.

7. Datos laborales: el Codigo de Trabajo (contrato escrito Art. 18 y 23, planillas o recibos Art. 138, registro de menores Art. 117), el Reglamento del ISSS (inscripcion en 10 dias, Art. 7; planillas, Art. 49), la Ley Integral del Sistema de Pensiones (afiliacion obligatoria Art. 8, cotizacion mensual Art. 13) y la LGPRLT (registro de accidentes Art. 8 num. 3, examenes medicos confidenciales Art. 63, aviso de accidentes en 72 horas Art. 66) obligan al patrono a tratar datos de empleados. La base natural es obligacion legal y contrato (Art. 5 lit. g num. 2 y 3, y Art. 28 lit. f). El consentimiento del empleado es debil como base por la subordinacion (Art. 27 lit. a exige que sea libre) y deberia reservarse para usos no necesarios (fotos, comunicaciones internas no laborales, biometria).

8. Marketing: el titular puede oponerse al tratamiento "incluida la elaboracion de perfiles o clasificaciones con fines comerciales o de mercadotecnia directa" (Art. 12); usar datos para un fin distinto al recabado sin previa autorizacion esta prohibido (Art. 32, infraccion grave 3); comercializar datos sin consentimiento es infraccion muy grave 7 y prohibicion del Art. 59 lit. d; el aviso de privacidad debe declarar el uso de cookies (Art. 24 lit. i). La Ley de Comercio Electronico (D.L. 463) permite enviar comunicaciones comerciales electronicas no solicitadas sin consentimiento previo solo si se identifican como tales, incluyen opcion de exclusion sencilla y gratuita y los datos se obtuvieron sin infringir la proteccion de datos (Art. 13). La Ley de Proteccion al Consumidor prohibe compartir informacion personal y crediticia sin autorizacion (Art. 18 lit. g) y la publicidad que vulnere intimidad e imagen es ilicita (Art. 31 lit. a, infraccion grave Art. 43 lit. g).

9. Fuentes de acceso publico: definidas de forma estricta como bases "cuya consulta puede ser realizada por disposicion de ley por cualquier persona" (Art. 4 lit. l); excepcion al consentimiento solo si no son datos sensibles (Art. 28 lit. a). Las redes sociales no encajan automaticamente en esa definicion; la excepcion distinta de "datos que el titular ha hecho manifiestamente publicos" (Art. 28 lit. g) es la que podria aplicarse, con criterio de abogado.

---

## 2. Bases de licitud y la convivencia con el principio de consentimiento y finalidad

### 2.1 Texto de las seis bases (Art. 5 lit. g)

Transcripcion textual (fuente local, pagina 5):

> g) Principio de Licitud: El tratamiento de datos personales debe realizarse en cumplimiento a lo establecido en la presente ley y la normativa aplicable, para lo cual debe cumplirse al menos una de las siguientes condiciones:
> 1. El tratamiento de los datos se base en el consentimiento expreso otorgado por el titular para una o varias finalidades.
> 2. El tratamiento sea necesario para la ejecucion de un contrato, del cual forma parte el titular, o para la ejecucion de medidas precontractuales.
> 3. El tratamiento sea necesario para el cumplimiento, por parte del responsable, de alguna obligacion legal.
> 4. El tratamiento sea necesario para garantizar la proteccion de los intereses vitales del titular u otra persona afectada.
> 5. El tratamiento sea necesario para el cumplimiento de un fin de interes publico o para que el responsable pueda ejercer los poderes publicos que le han sido conferidos.
> 6. El tratamiento sea necesario para que el responsable pueda satisfacer sus intereses legitimos, siempre y cuando esos intereses no atenten contra los derechos o libertades de los titulares de los datos personales.

| Num. | Base | Palabra clave del texto | Uso tipico en sector privado | Riesgo de interpretacion |
|---|---|---|---|---|
| 1 | Consentimiento expreso | "para una o varias finalidades" | marketing, cookies no necesarias, fotos, biometria, datos sensibles | requiere prueba (Art. 54) y revocabilidad (Art. 29) |
| 2 | Contrato o medidas precontractuales | "necesario para la ejecucion" | clientes, proveedores persona natural, empleados, candidatos | solo lo necesario para ejecutar el contrato |
| 3 | Obligacion legal | "necesario para el cumplimiento ... de alguna obligacion legal" | planillas, ISSS, AFP, facturacion, retenciones, prevencion de lavado | debe citarse la norma concreta |
| 4 | Intereses vitales | "proteccion de los intereses vitales" | emergencias medicas, salud ocupacional en accidente | uso excepcional |
| 5 | Interes publico o poderes publicos | "fin de interes publico" | entidades publicas (ver Art. 46) o privados con mision publica delegada | dificil de invocar por empresa privada comun |
| 6 | Interes legitimo | "siempre y cuando esos intereses no atenten contra los derechos o libertades" | videovigilancia de seguridad, prevencion de fraude, seguridad de red | exige ponderacion documentada; la ley no describe el test |

### 2.2 Las normas que apuntan al consentimiento como regla

- Art. 4 lit. d define el consentimiento como manifestacion "libre, especifica, informada, expresa e individualizada ... en los casos en que no exista otro fundamento legal para ello". Esta ultima frase es la unica que reconoce de modo expreso que el consentimiento es subsidiario a otros fundamentos.
- Art. 5 lit. c: "Principio de consentimiento y finalidad: en el tratamiento y recoleccion de datos personales debe existir un consentimiento libre, especifico, informado, expreso e individualizado del titular, que establezca el fin, proposito y periodo de almacenamiento y tratamiento."
- Art. 27 inc. 1: "Para el tratamiento de los datos personales, y en especial de los datos personales sensibles, sera necesaria la obtencion del consentimiento del titular o en su caso de su representante".
- Art. 24 lit. c y d: el aviso de privacidad debe indicar "el fundamento legal que faculta al responsable para realizar el tratamiento" y las finalidades "distinguiendo aquellas que requieren el consentimiento del titular". Esto presupone que hay finalidades que no requieren consentimiento.
- Art. 28: lista de casos en que "no sera necesario el previo consentimiento" (fuentes de acceso publico sin datos sensibles; salud cuando el titular no puede consentir y trata persona sujeta a secreto; emergencia o interes vital; disociacion previa; persona desaparecida; relacion contractual, cientifica o profesional cuando sean necesarios; datos manifiestamente publicos; archivo historico, investigacion o estadistica).
- Art. 32: "El tratamiento de datos personales por parte de todos los responsables solo podra efectuarse respecto de los fines previamente informados ... En el caso de las instituciones o empresa privada, unicamente debera realizar el tratamiento de los datos personales que tengan relacion directa con la naturaleza de los servicios que prestaran o prestaron al titular, en ningun caso podran transferir o tratar datos personales de terceros para ofrecer otro tipo de servicios o cualquier finalidad diferente a la que estos fueron recabados, sin previa autorizacion del titular."
- Art. 34 lit. a: obligacion de "limitar el tratamiento de los datos personales de conformidad a la finalidad para la que se emitio el consentimiento por parte del titular".
- Art. 56 lit. c num. 1: infraccion muy grave "tratar datos personales sin el consentimiento previo, de conformidad con lo establecido en el articulo 26 de la presente ley".
- Art. 10 lit. b y Art. 29 inc. 2 reconocen que la revocacion o retiro del consentimiento no afecta el tratamiento que se apoye en "otro supuesto de licitud" u "otras de las causales establecidas en la presente ley". Art. 14 condiciona la portabilidad a que el tratamiento "este fundado en el consentimiento". Art. 12 lit. a y b excluyen la oposicion cuando la base es interes publico o interes legitimo. Art. 46 permite al sector publico tratar "aun sin el consentimiento expreso".

### 2.3 Lectura de la ambiguedad

La ley contiene dos lineas normativas que no estan armonizadas:

```
Linea A (consentimiento como regla)          Linea B (pluralidad de bases)
-----------------------------------          -----------------------------
Art. 5 lit. c  principio de consentimiento   Art. 4 lit. d  "cuando no exista otro fundamento legal"
Art. 27 inc. 1 "sera necesaria la obtencion" Art. 5 lit. g  seis condiciones alternativas
Art. 32        "sin previa autorizacion"     Art. 24 lit. c y d fundamento legal y finalidades
Art. 34 lit. a finalidad del consentimiento  Art. 28       excepciones al consentimiento
Art. 56 c) 1   infraccion muy grave          Art. 10 b), 29 inc. 2, 12 a) b), 14, 46
```

Lo que si es seguro con el texto en mano:

1. Existe una lista de seis bases y una lista de excepciones al consentimiento; ambas estan en la ley y no han sido derogadas.
2. Cuando la base no es consentimiento, la ley igualmente exige informar (Art. 7 y 24), limitar el tratamiento a la finalidad informada (Art. 32) y respetar los derechos ARCO-POL con las modulaciones propias de cada base.
3. Cualquier finalidad nueva respecto de la informada requiere nueva autorizacion del titular (Art. 7 inc. 3 y Art. 32). En este punto la ley si usa un lenguaje de consentimiento sin alternativa.
4. La sancion muy grave 1 se refiere al consentimiento "de conformidad con el articulo 26", es decir, a las formas del consentimiento cuando este es la base. No hay un pronunciamiento de la ACE que diga si sanciona tambien a quien invoca otra base de forma razonada. Este es el riesgo principal que el abogado de la empresa debe evaluar.

Lo que no esta resuelto y requiere abogado: si una empresa privada puede apoyarse en interes legitimo o contrato sin consentimiento para tratamientos ordinarios (por ejemplo clientes y empleados) sin exponerse a la infraccion muy grave 1. Fuentes secundarias (ECIJA, articulo sobre relaciones laborales, consultado 2026-09-23) sostienen que el consentimiento es la base principal y que no puede inferirse del contrato de trabajo; otras firmas describen las seis bases como alternativas. No hay jurisprudencia ni resoluciones publicadas de la ACE al 2026-09-23 que zanjen el punto.

### 2.4 Como debe tratar la ambiguedad el software

Diseno funcional recomendado, sin validar juridicamente:

```
Actividad de tratamiento (RAT)
   |
   v
[Seleccionar base de licitud]  -> lista cerrada Art. 5 lit. g (1 a 6)
   |                              + campo "excepcion Art. 28 aplicable" (a-h, opcional)
   v
[Justificacion escrita obligatoria]  -> texto libre + norma citada si es obligacion legal
   |
   v
[Advertencia contextual, no bloqueante]
   |  - Si base = consentimiento: exigir vincular evidencia (seccion 3)
   |  - Si base = contrato / obligacion legal / interes legitimo: mostrar aviso
   |    "La LPDP contiene un principio de consentimiento (Art. 5 lit. c, 27, 56 c) 1).
   |     La eleccion de esta base es una decision juridica de su empresa. Documente la
   |     justificacion y considere revision por abogado."
   |  - Si base = interes legitimo: pedir ponderacion documentada (interes, necesidad,
   |    impacto en el titular, salvaguardas) porque Art. 5 lit. g num. 6 la condiciona
   |  - Si datos sensibles: exigir consentimiento escrito con firma o excepcion
   |    Art. 37/38 documentada
   v
[Registro inmutable con fecha, autor, version]  -> evidencia para Art. 5 lit. i y Art. 54
   |
   v
[Reflejo en aviso de privacidad]  -> Art. 24 lit. c (fundamento legal) y lit. d
                                     (finalidades que requieren consentimiento)
```

Reglas del producto:
- Registrar base y justificacion es OBLIGATORIO en el flujo (por Art. 24 lit. c y d, Art. 5 lit. i responsabilidad demostrada y Politicas ACE Art. 4 medidas organizativas lit. d "Registro de Actividades de Tratamiento").
- El software no marca una base como "valida" ni como "cumple". Muestra un indicador de "documentado / no documentado" y "con evidencia / sin evidencia".
- Toda base distinta del consentimiento se guarda con la leyenda "decision de la empresa, sujeta a revision juridica".
- Cambios de base o de finalidad generan version nueva y disparan la tarea "revisar aviso de privacidad y, si aplica, obtener nueva autorizacion" (Art. 7 inc. 3, Art. 32).

### 2.5 Bloques de obligacion (bases y finalidad)

**Norma:** LPDP, D.L. 144.
**Articulo:** Art. 5 lit. g.
**Obligacion:** Todo tratamiento debe cumplir al menos una de las seis condiciones de licitud.
**A quien aplica:** Responsables y encargados (Art. 2, Art. 34).
**Implicacion para el software:** Campo obligatorio "base de licitud" por actividad de tratamiento con lista cerrada de seis valores mas justificacion.
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pag. 5 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

**Norma:** LPDP, D.L. 144.
**Articulo:** Art. 5 lit. c, Art. 27 inc. 1, Art. 56 lit. c num. 1.
**Obligacion:** Principio de consentimiento y finalidad; el consentimiento debe establecer fin, proposito y periodo de almacenamiento; tratar sin consentimiento previo conforme al Art. 26 es infraccion muy grave.
**A quien aplica:** Responsables.
**Implicacion para el software:** Cuando la base sea consentimiento, exigir que el registro incluya finalidades concretas y periodo de conservacion; cuando no lo sea, mostrar advertencia de riesgo y exigir justificacion. No validar automaticamente.
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pags. 5, 15, 25 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (registro) / decision juridica de la empresa (eleccion de base).

**Norma:** LPDP, D.L. 144.
**Articulo:** Art. 28.
**Obligacion:** No se requiere consentimiento previo en los supuestos a) a h); el supuesto a) (fuentes de acceso publico) no aplica a datos sensibles.
**A quien aplica:** Responsables.
**Implicacion para el software:** Campo opcional "excepcion Art. 28" con lista a) a h) y texto de justificacion; bloqueo logico: si datos sensibles, no admitir la excepcion a).
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pags. 15 y 16 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** CONDICIONAL (solo si concurre el supuesto).

**Norma:** LPDP, D.L. 144.
**Articulo:** Art. 32; Art. 7 inc. 3; Art. 56 lit. b num. 3.
**Obligacion:** Tratar solo para los fines previamente informados; la empresa privada solo trata datos con relacion directa a los servicios que presta; toda finalidad distinta requiere previa autorizacion del titular; procesar con finalidad diferente es infraccion grave.
**A quien aplica:** Responsables privados.
**Implicacion para el software:** Finalidades declaradas por actividad; cualquier nueva finalidad crea tarea de "nueva autorizacion / actualizacion de aviso" y deja rastro.
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pags. 7, 17, 25 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

**Norma:** LPDP, D.L. 144.
**Articulo:** Art. 24 lit. c y d.
**Obligacion:** El aviso de privacidad debe indicar el fundamento legal del tratamiento y distinguir las finalidades que requieren consentimiento.
**A quien aplica:** Responsables.
**Implicacion para el software:** El generador de aviso toma la base y finalidades del RAT; si falta base, el aviso queda marcado incompleto.
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pag. 13 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

**Norma:** Politicas de Actuacion y Manejo de Datos Personales, ACE, N. 001-0309025-DPDP.
**Articulo:** Art. 2 (ambito obligatorio), Art. 3 lit. c (consentimiento y finalidad: "obtener autorizacion explicita del titular para la recoleccion y tratamiento"), Art. 4 medidas organizativas lit. d (Registro de Actividades de Tratamiento).
**Obligacion:** Las politicas se declaran de cumplimiento obligatorio para entidades publicas y privadas; reproducen el principio de consentimiento sin mencionar otras bases; exigen RAT.
**A quien aplica:** Entidades publicas y privadas que traten datos en El Salvador.
**Implicacion para el software:** El RAT es el nucleo; la formulacion de la ACE refuerza la lectura "consentimiento como regla", lo que debe reflejarse en la advertencia contextual.
**Fuente oficial:** `fuentes\ace_politicas_protecciondatos.txt` pags. 2 y 3; https://ace.gob.sv/politicas.php (2026-09-23). Fecha de emision pendiente de verificar.
**Vigencia:** VIGENTE (Art. 9: desde su publicacion).
**Clasificacion:** OBLIGATORIO (politica de actuacion imperativa por Art. 35 LPDP).

---

## 3. Consentimiento: requisitos, formas, prueba, evidencia y revocacion

### 3.1 Texto de los Arts. 26 y 27

> Art. 26.- El consentimiento debera ser expreso, y se podra manifestar de manera verbal, por escrito o a traves de signos inequivocos, siempre y cuando conste por medios fisicos, electronicos o cualquier otro medio tecnologico.
> En el caso del consentimiento de los ninos, ninas y adolescentes para proporcionar sus datos personales se tomara en cuenta el Principio de Ejercicio Progresivo de las Facultades, en lo pertinente y adecuado para la aplicacion de la presente ley.
> Cuando se trate de datos personales de personas declaradas incapaces se estara a lo dispuesto por el derecho comun.
> Tratandose de datos personales sensibles, el responsable debera obtener el consentimiento por escrito del titular para su tratamiento, a traves de su firma autografa o su equivalente.

> Art. 27.- ... debiendo ser dicho consentimiento:
> a) Libre: no debe mediar error, mala fe, dolo, violencia fisica, psicologica o cualquier otra forma de violencia ...
> b) Especifico: referido a una o varias finalidades determinadas y definidas que justifiquen el tratamiento.
> c) Informado: que el titular tenga conocimiento previo al tratamiento, a que seran sometidos sus datos personales y las consecuencias de otorgar su consentimiento.
> d) Expreso: debe ser inequivoco, de forma tal que pueda demostrarse su otorgamiento. El consentimiento puede ser obtenido por medios fisicos o electronicos.
> e) Individualizado: debe existir al menos un otorgamiento del consentimiento por parte de cada titular de los datos personales.

### 3.2 Formas validas

| Forma | Base legal | Datos ordinarios | Datos sensibles |
|---|---|---|---|
| Verbal registrada (grabacion, acta) | Art. 26 inc. 1 | valida si consta en medio fisico, electronico o tecnologico | no valida (se exige escrito con firma) |
| Escrito con firma autografa | Art. 26 inc. 1 y 4 | valida | valida |
| Escrito con firma electronica simple | Art. 26 inc. 4 "o su equivalente"; Ley de Firma Electronica Art. 6 | valida | valida en cuanto a validez juridica; menor valor probatorio que la certificada |
| Escrito con firma electronica certificada | Ley de Firma Electronica Art. 6 y 8 | valida | valida, documento privado fehaciente |
| Signos inequivocos (clic en casilla no premarcada, boton "acepto", accion afirmativa) | Art. 4 lit. d "clara accion afirmativa", Art. 26 inc. 1 | valida si queda registro | no recomendada para sensibles sin firma equivalente |
| Silencio, casillas premarcadas, inaccion | ninguna | no valida (Art. 27 lit. d "inequivoco") | no valida |

Sobre "firma autografa o su equivalente": la Ley de Firma Electronica (D.L. 133, D.O. N. 196, Tomo 409, 26 oct 2015, reformada por D.L. 100 de 2021) dice en su Art. 6: "La firma electronica simple tendra la misma validez juridica que la firma autografa. En cuanto a sus efectos juridicos, la firma electronica simple no tendra validez probatoria en los mismos terminos a los concedidos por esta ley a la firma electronica certificada; sin embargo, podra constituir un elemento de prueba conforme a las reglas de la sana critica." Art. 7: los actos suscritos con firma electronica "se reputaran como escritos, en los casos en que la ley exija que los mismos consten de ese modo". La Ley de Comercio Electronico (D.L. 463) Art. 8 confirma que el requisito de "constar por escrito" se cumple en soporte electronico accesible para consulta posterior y que la firma se cumple con firma electronica conforme a su ley. Conclusion: una firma electronica simple es un "equivalente" valido; para datos sensibles conviene firma certificada o autografa escaneada por su mayor valor probatorio. Decision de la empresa con abogado.

### 3.3 Carga de la prueba y evidencia minima a conservar

Art. 54 inc. 1: "Para efectos de demostrar la obtencion del consentimiento o la comunicacion de la politica o del aviso de privacidad, la carga de la prueba recaera especificamente en el responsable, conforme a las formas que se establecen en la presente Ley."

Art. 24 inc. final: "En ningun caso el responsable podra eximirse de la obligacion de comunicarlo [el aviso] por escrito al titular al momento de que este otorgue su consentimiento informado".

Art. 56 lit. a num. 6: infraccion leve "modificar los datos suministrados en el documento que autoriza el tratamiento de datos personales". Esto exige que el documento de consentimiento sea inalterable y versionado.

Normativa para el Procedimiento Administrativo Sancionador (ACE, D.O. 11 ago 2026, vigente 19 ago 2026), Art. 24: son prueba "los instrumentos publicos, los autenticos, los instrumentos privados, las declaraciones de testigos, los resultados de peritajes, la inspeccion de los lugares o de las cosas, la confesion, los informes de auditoria internos o externos, cualquier otra informacion que hubiese sido proporcionada por el presunto infractor a la Agencia ... las presunciones legales y cualquier otro medio admisible en derecho", valorados con sana critica y con aplicacion supletoria del Codigo Procesal Civil y Mercantil. Los registros del software son instrumentos privados y pueden complementarse con informes de auditoria.

La ley no enumera campos de evidencia. La siguiente lista es RECOMENDADA como estandar minimo derivado de Arts. 24, 26, 27 y 54:

| Campo de evidencia | Fundamento | Clasificacion |
|---|---|---|
| Identificacion del titular (nombre, documento o identificador de cuenta) | Art. 27 lit. e individualizado | OBLIGATORIO (demostrar que fue "cada titular") |
| Fecha y hora del otorgamiento | Art. 27 lit. c "previo al tratamiento", Art. 29 revocacion sin efecto retroactivo | OBLIGATORIO (demostrar anterioridad) |
| Texto exacto de la clausula de consentimiento y finalidades marcadas | Art. 27 lit. b especifico | OBLIGATORIO |
| Version e identificador del aviso de privacidad entregado y constancia de entrega por escrito | Art. 24 inc. final, Art. 54 | OBLIGATORIO |
| Canal (web, app, formulario papel, telefono, presencial) | Art. 26 "conste por medios fisicos, electronicos ..." | RECOMENDADO |
| Medio de manifestacion (firma autografa, firma electronica simple o certificada, clic, grabacion) | Art. 26, Art. 27 lit. d | OBLIGATORIO para sensibles (firma), RECOMENDADO en el resto |
| Periodo de almacenamiento declarado | Art. 5 lit. c | OBLIGATORIO cuando la base es consentimiento |
| Quien recabo (usuario o sistema) y hash o sello del documento | Art. 56 lit. a num. 6 | RECOMENDADO |
| Advertencia del derecho a no proporcionar datos sensibles y efectos de la negativa | Art. 37 inc. 1, Art. 7 inc. final | OBLIGATORIO cuando hay sensibles |
| Representante y prueba de vinculo cuando el titular es NNA o incapaz | Art. 26 inc. 2 y 3, Art. 56 lit. c num. 3 y 4 | OBLIGATORIO cuando aplica |
| Historial de revocaciones con fecha de recepcion, fecha de ejecucion y aviso al encargado | Arts. 29 a 31 | OBLIGATORIO |

### 3.4 Revocacion (Arts. 29 a 31)

> Art. 29.- En cualquier momento, el titular podra revocar de forma expresa su consentimiento ... sin efecto retroactivo, para lo cual el responsable debera establecer mecanismos expeditos, sencillos y gratuitos ... Esta revocacion no afectara la licitud del tratamiento posterior ... si este es ejecutado sobre la base de otras de las causales establecidas en la presente ley que lo justifiquen.
> Art. 30.- El delegado, ante la presentacion de la solicitud de revocacion del consentimiento, contara con un plazo de cinco dias habiles a partir de su recepcion para proceder conforme a la revocacion. Si estos datos personales tambien son tratados por un encargado del tratamiento, el delegado debera informarle de la resolucion de revocacion en el plazo de cinco dias habiles a partir de la fecha de emision de esta, para que la ejecute inmediatamente.
> Art. 31.- En caso de negativa ... el titular ... podra presentar su denuncia ante la Entidad Rectora.

Notas:
- El Art. 24 lit. e exige que el aviso informe "los mecanismos para revocar el consentimiento".
- El Art. 50 lit. q encarga a la ACE elaborar formularios "de solicitudes de los derechos ARCO-POL y la revocacion del consentimiento". Al 2026-09-23 la pagina https://ace.gob.sv/page/formularios publica siete formularios ARCO-POL (acceso, rectificacion, cancelacion, oposicion, portabilidad, olvido, limitacion) y uno de nombramiento de delegado (version 07-07-2025); no hay formulario oficial de revocacion. El software debe ofrecer su propio formulario y admitir cualquier medio.
- La reforma de sep 2026 (D.L. 659), segun nota oficial de la Asamblea (https://www.asamblea.gob.sv/node/14116) y prensa (elsalvador.com, 2026-09-23), mantiene "un plazo de cinco dias habiles para atender las solicitudes mediante las cuales una persona retire su consentimiento" y traslada la recepcion a la empresa u organizacion. Texto oficial no localizado; vigencia pendiente de publicacion.

### 3.5 Infracciones vinculadas al consentimiento

| Tipo | Numeral | Texto | Multa (Art. 57) |
|---|---|---|---|
| Muy grave | c) 1 | Tratar datos personales sin el consentimiento previo, de conformidad con el Art. 26 | 26 a 40 salarios minimos mensuales sector comercio |
| Muy grave | c) 9 | Tratar datos personales a pesar de la revocacion del consentimiento | 26 a 40 |
| Muy grave | c) 10 | No hacer efectiva la revocacion ante la solicitud del titular cuando esta proceda | 26 a 40 |
| Muy grave | c) 3 | Uso de datos de NNA sin consentimiento previo de padres, representantes o tutores | 26 a 40 |
| Muy grave | c) 4 | Tratar datos de personas declaradas incapaces sin consentimiento del titular o representante | 26 a 40 |
| Muy grave | c) 7 | Comercializar datos a cualquier titulo sin consentimiento | 26 a 40 |
| Grave | b) 3 | Procesar, recopilar o destinar datos con finalidad diferente para la que se otorgo el consentimiento o se habilito el tratamiento | 11 a 25 |
| Leve | a) 6 | Modificar los datos suministrados en el documento que autoriza el tratamiento | 1 a 10 |
| Leve | a) 1 y 8 | No informar derechos antes de recolectar; incumplir el Art. 7 | 1 a 10 |

Parametros de graduacion (Normativa Sancionadora ACE Art. 43): gravedad del dano, efecto disuasivo, duracion, intencionalidad o negligencia, naturaleza o categoria de los datos y capacidad economica.

### 3.6 Bloques de obligacion (consentimiento)

**Norma:** LPDP, D.L. 144.
**Articulo:** Arts. 26 y 27.
**Obligacion:** Consentimiento expreso, libre, especifico, informado e individualizado; verbal, escrito o por signos inequivocos siempre que conste en un medio; escrito con firma autografa o equivalente para sensibles.
**A quien aplica:** Responsables.
**Implicacion para el software:** Modulo de captura y registro de consentimientos con plantillas por finalidad, casillas no premarcadas, registro por titular, y modo "sensible" que exige firma.
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pag. 15 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (cuando la base es consentimiento).

**Norma:** LPDP, D.L. 144.
**Articulo:** Art. 54 inc. 1; Art. 24 inc. final; Art. 56 lit. a num. 6.
**Obligacion:** El responsable debe poder probar el consentimiento y la comunicacion escrita del aviso; el documento de autorizacion no puede alterarse.
**A quien aplica:** Responsables.
**Implicacion para el software:** Evidencia inmutable, versionada, exportable, con vinculo entre consentimiento y version del aviso.
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pags. 14 y 24 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

**Norma:** LPDP, D.L. 144.
**Articulo:** Arts. 29, 30, 31; Art. 24 lit. e; Art. 56 lit. c num. 9 y 10.
**Obligacion:** Mecanismo expedito, sencillo y gratuito de revocacion; proceder en 5 dias habiles; informar al encargado en 5 dias habiles desde la resolucion; informar el mecanismo en el aviso.
**A quien aplica:** Responsables (delegado segun texto vigente; sujeto obligado segun reforma pendiente); encargados deben ejecutar inmediatamente.
**Implicacion para el software:** Bandeja de revocaciones con contador de 5 dias habiles, segunda cuenta de 5 dias para aviso a encargados, bloqueo automatico de los tratamientos basados en ese consentimiento, y conservacion de lo que se apoye en otra base con justificacion.
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pags. 16 y 25 (2026-09-23).
**Vigencia:** VIGENTE (Art. 30 MODIFICADA en su sujeto por reforma APROBADA-PENDIENTE-PUBLICACION).
**Clasificacion:** OBLIGATORIO.

**Norma:** Ley de Firma Electronica, D.L. 133 (2015), reformada por D.L. 100 (2021).
**Articulo:** Arts. 6, 7 y 8.
**Obligacion:** La firma electronica simple tiene la misma validez que la autografa pero menor valor probatorio que la certificada; los actos con firma electronica se reputan escritos.
**A quien aplica:** Cualquier responsable que recabe consentimiento electronico.
**Implicacion para el software:** Registrar el tipo de firma usada; ofrecer nivel "certificada" como opcion para datos sensibles; no afirmar equivalencia probatoria plena.
**Fuente oficial:** https://factura.gob.sv/wp-content/uploads/2022/10/Ley_de_Firma_Electr%C3%B3nica.pdf (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** CONDICIONAL (cuando se use firma electronica).

---

## 4. Datos sensibles

### 4.1 Definicion enunciativa (Art. 4 lit. g)

> g) Datos personales sensibles: son los datos personales que se refieren a las caracteristicas fisicas o morales de las personas o a hechos o circunstancias de su vida privada o intimidad, que afectan a la esfera mas intima de su titular y cuya utilizacion indebida puedan dar origen a discriminacion, afectar gravemente el derecho al honor, a la intimidad personal y familiar y a la propia imagen. De manera enunciativa pero no limitativa, generalmente son los que revelan aspectos como creencias y convicciones religiosas, origen etnico, afiliacion o ideologias politicas, afiliacion sindical, preferencias sexuales, salud fisica y mental, informacion biometrica, genetica, situacion moral y familiar, habitos personales y otras informaciones intimas de similar naturaleza.

Observaciones:
- La lista es abierta ("enunciativa pero no limitativa"). "Situacion moral y familiar" y "habitos personales" son categorias mas amplias que las de otros ordenamientos y pueden abarcar, por ejemplo, habitos de consumo intimos. La clasificacion final la decide la empresa; la ACE resuelve controversias sobre "clasificacion y desclasificacion de datos personales sensibles" (Art. 50 lit. f).
- El Art. 59 lit. b usa una lista distinta: "origen racial o etnico, nacionalidad, afiliacion partidaria, convicciones religiosas, espirituales o filosoficas, asi como los relativos a la salud, la vida y la orientacion sexual". Incluye "nacionalidad" y "convicciones filosoficas", que no aparecen en el Art. 4 lit. g. El software debe tratar la union de ambas listas como catalogo sugerido de sensibles y advertir que "nacionalidad" aparece en el Art. 59 lit. b (prohibicion) aunque el Art. 4 lit. f la mencione como dato personal ordinario. Punto para abogado.

### 4.2 Reglas de tratamiento

> Art. 37.- Ninguna persona puede ser obligada a proporcionar sus datos personales sensibles. Estos solo podran ser objeto de tratamiento con el consentimiento expreso e inequivoco del titular de conformidad con lo establecido en la presente ley, advirtiendo en todo caso al titular de dichos datos sobre su derecho a no prestarlo.
> Excepcionalmente podran ser objeto de tratamiento ... cuando sea necesario para salvaguardar la vida del titular de los mismos o de otra persona, en el supuesto de que este se encuentre fisica o juridicamente incapacitado para dar su consentimiento.
> No obstante ... podran ser objeto de tratamiento los datos personales relativos a la salud, cuando dicho tratamiento resulte necesario para la prevencion o para el diagnostico medico, la prestacion de asistencia sanitaria o tratamientos medicos o la gestion de servicios sanitarios, siempre que dicho tratamiento de datos se realice por un profesional sanitario sujeto al secreto profesional o por otra persona sujeta a una obligacion equivalente al secreto ...

> Art. 38.- Los datos personales sensibles solo pueden ser recolectados y ser objeto de tratamiento en los casos establecidos por la presente ley, cuando medien razones de interes general autorizadas por otras disposiciones legales aplicables o cuando el responsable tenga un mandato legal para hacerlo.
> Tambien podran ser tratados con finalidades estadisticas o cientificas cuando se disocien de sus titulares.

> Art. 59.- Queda prohibido a los sujetos obligados ...: a) Crear bases de datos que contengan datos personales sensibles, en contravencion a lo dispuesto en la presente ley o la normativa aplicable ... b) El tratamiento de datos personales que revelen el origen racial o etnico, nacionalidad, afiliacion partidaria, convicciones religiosas, espirituales o filosoficas, asi como los relativos a la salud, la vida y la orientacion sexual, sin observar lo establecido en el capitulo IV del Titulo II de esta ley ...

Incurrir en las prohibiciones del Art. 59 es infraccion grave (Art. 56 lit. b num. 6). Ademas, la Normativa Sancionadora ACE Art. 32 inc. (pag. 28 D.O.) manda que "cuando la infraccion involucre el tratamiento indebido de datos personales sensibles, la autoridad competente debera considerar la especial proteccion juridica de estos datos al determinar la calificacion de la falta y la proporcionalidad de la sancion", y el Art. 43 lit. e incluye "naturaleza o categoria de los datos" entre los parametros de multa.

### 4.3 Cuadro de vias licitas para datos sensibles

| Via | Norma | Condiciones | Evidencia que el software debe pedir |
|---|---|---|---|
| Consentimiento escrito con firma autografa o equivalente | Art. 26 inc. 4, Art. 37 inc. 1 | expreso, inequivoco, con advertencia del derecho a no prestarlo | documento firmado (autografo escaneado o firma electronica), texto de la advertencia, fecha, identificacion |
| Salvaguarda de la vida | Art. 37 inc. 2, Art. 28 lit. c | titular incapacitado fisica o juridicamente para consentir | descripcion del hecho, fecha, quien decidio |
| Salud por profesional sujeto a secreto | Art. 37 inc. 3, Art. 28 lit. b, Art. 39 | necesario para prevencion, diagnostico, asistencia o gestion sanitaria; profesional o persona sujeta a secreto | identificacion del profesional o unidad, obligacion de secreto documentada |
| Interes general autorizado por ley o mandato legal | Art. 38 inc. 1 | norma concreta que lo autorice | cita de la norma (por ejemplo LGPRLT Art. 63 para examenes ocupacionales) |
| Disociacion para fines estadisticos o cientificos | Art. 38 inc. 2, Art. 28 lit. d, Art. 4 lit. h | procedimiento irreversible | descripcion del metodo de disociacion |

Nota: el Art. 28 lit. a (fuentes de acceso publico) excluye expresamente los datos sensibles; el Art. 28 lit. g (datos manifiestamente publicos) no contiene esa exclusion literal, pero el Art. 37 inc. 1 dice que los sensibles "solo podran" tratarse con consentimiento salvo las excepciones de ese articulo. Prevalece la lectura restrictiva; abogado.

### 4.4 Salud

- Art. 39 LPDP: los establecimientos de salud y profesionales de ciencias de la salud pueden recolectar y tratar datos de salud de sus pacientes "respetando el secreto profesional, los derechos de los pacientes establecidos en la Ley de Deberes y Derechos de los Pacientes y Prestadores de Servicios de Salud, la normativa especifica aplicable y lo establecido en la presente ley".
- Ley de Deberes y Derechos de los Pacientes y Prestadores de Servicios de Salud, D.L. 307, D.O. Tomo 411, 8 abr 2016 (fuente: https://asp.salud.gob.sv/regulacion/pdf/ley/ley_deberes_y_derechos_pacientes_y_prestadores_servicios_de_salud.pdf, 2026-09-23):
  - Art. 15: todo procedimiento de atencion medica se acuerda con el paciente o representante tras informacion adecuada, "lo que debera constar por escrito y firmado por el paciente o su representante, en el formulario autorizado para tal fin". Es un consentimiento clinico, distinto del consentimiento de datos de la LPDP.
  - Art. 16 lit. f: en investigacion medica el escrito debe garantizar confidencialidad y que los datos no se usen para propositos diferentes.
  - Art. 17: consentimiento por sustitucion (conyuge, familiares, padres o representante legal para NNA e incapaces).
  - Art. 18: excepciones al consentimiento informado (riesgo epidemiologico, incapacidad sin representante, emergencia, paciente abandonado).
  - Art. 20: "Los pacientes tendran derecho a que se respete el caracter confidencial de su expediente clinico y toda la informacion relativa al diagnostico, tratamiento, estancia, pronosticos y datos de su enfermedad o padecimiento, a menos que por autorizacion escrita del mismo o porque existan razones legales o medicas imperiosas, se deba divulgar tal informacion."
  - Art. 33 lit. c y d: deber del prestador de garantizar el secreto profesional y "custodiar los expedientes clinicos de los pacientes, adoptando las medidas tecnicas y procedimientos adecuados para el resguardo y proteccion de los datos contenidos en los mismos y evitar su destruccion o perdida".
  - Art. 42 lit. g: danar, alterar o extraer hojas del expediente clinico es infraccion grave de esa ley.
- Salud ocupacional: LGPRLT (D.L. 254, D.O. N. 82, Tomo 387, 5 may 2010) Art. 63: cuando la Direccion General de Prevision Social lo determine por el riesgo de la actividad, el empleador debe mandar a practicar examenes medicos y de laboratorio; "los resultados seran confidenciales y en ningun caso se utilizaran en perjuicio del trabajador". Art. 8 num. 3 y 6: el Programa de Gestion de Prevencion de Riesgos debe incluir "registro actualizado de accidentes, enfermedades profesionales y sucesos peligrosos" y "programa de examenes medicos". Art. 66: notificar accidentes a la Direccion en 72 horas. Codigo de Trabajo Art. 304 lit. f: el reglamento interno debe fijar "tiempo y forma en que los trabajadores deben someterse a los examenes medicos, previos o periodicos". Codigo de Trabajo Art. 117: examen medico previo obligatorio para menores de 18 y registro de menores.

Implicacion: para salud ocupacional la via del Art. 38 inc. 1 (mandato legal: LGPRLT Art. 8 y 63, CT Art. 117 y 304) es la que suele aplicar; el software debe exigir que el acceso a resultados este limitado al personal medico o de prevencion y que se registre el fundamento. Si la empresa quiere usar datos de salud para otros fines (por ejemplo bienestar o seguros voluntarios) necesita consentimiento escrito con firma (Art. 26 inc. 4).

### 4.5 Biometria y videovigilancia

Que dice la ley: solo el Art. 4 lit. g menciona "informacion biometrica" como dato sensible. No hay articulo sobre videovigilancia, reconocimiento facial, huella dactilar, control de asistencia o camaras. Las Politicas de Actuacion de la ACE incluyen, entre medidas fisicas de seguridad, "Monitoreo y Vigilancia: uso de camaras de seguridad y registros de ingreso" (Art. 4, Medidas Fisicas lit. b), lo que reconoce la videovigilancia como medida de seguridad, pero no regula su tratamiento como datos personales.

Verificacion realizada el 2026-09-23: la pagina https://ace.gob.sv/politicas.php lista unicamente el Decreto 143, el Decreto 144, las Politicas de Actuacion, los Lineamientos para el Delegado y la Normativa Sancionadora. Ninguno de esos documentos trata biometria, videovigilancia, reconocimiento facial o cookies. Busquedas web con esos terminos no arrojaron ningun lineamiento ACE. Conclusion: no existe lineamiento ACE sobre biometria ni videovigilancia al 2026-09-23.

Consecuencias practicas (analisis, no norma):
- Biometria de asistencia (huella, rostro, iris): es dato sensible por definicion expresa. Vias: consentimiento escrito con firma (Art. 26 inc. 4, Art. 37) con advertencia de que puede negarse y alternativa no biometrica; o mandato legal (Art. 38), que no existe para control de asistencia en el sector privado. Al ser el titular un empleado, la libertad del consentimiento (Art. 27 lit. a) es discutible; una alternativa real (tarjeta, PIN) refuerza la libertad. Requiere abogado.
- Videovigilancia: la imagen es dato personal (Art. 4 lit. f "informacion en texto, imagen o audio"). No es sensible por si misma salvo que revele categorias sensibles. Base posible: interes legitimo (seguridad de personas y bienes) o consentimiento; en ambos casos se exige informar (Art. 7 y 24: aviso visible en el establecimiento, Art. 16 lit. g publicacion del aviso en lugares visibles) y respetar oposicion salvo que prevalezca el interes legitimo (Art. 12 lit. b). Si se usa reconocimiento facial, pasa a biometria y a regla de sensibles.

### 4.6 Disociacion y seudonimizacion

- Art. 4 lit. h: disociacion o anonimizacion es "procedimiento irreversible" por el cual los datos dejan de asociarse al titular.
- Art. 4 lit. q: seudonimizacion mantiene informacion adicional separada y protegida; sigue siendo dato personal.
- Efectos: datos disociados no requieren consentimiento (Art. 28 lit. d), pueden tratarse con fines estadisticos o cientificos aunque sean sensibles (Art. 38 inc. 2), no procede cancelacion sobre datos disociados (Art. 10 exc. d) y las resoluciones de la ACE se publican disociadas (Art. 55). Revertir la seudonimizacion sin consentimiento es infraccion muy grave 8 (Art. 56 lit. c num. 8).
- Software: campo "estado del dato" (identificado, seudonimizado, disociado) por actividad, con registro del metodo, y bloqueo de la marca "disociado" si el proceso no es irreversible segun la declaracion de la empresa.

### 4.7 Bloques de obligacion (sensibles)

**Norma:** LPDP, D.L. 144.
**Articulo:** Art. 4 lit. g; Art. 24 lit. b.
**Obligacion:** Identificar que datos son sensibles; el aviso debe identificar los datos sensibles que se tratan.
**A quien aplica:** Responsables.
**Implicacion para el software:** Catalogo de categorias de datos con marca "sensible" (union de listas Art. 4 lit. g y Art. 59 lit. b), editable por la empresa con justificacion; el aviso hereda la marca.
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pags. 3, 13, 26 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

**Norma:** LPDP, D.L. 144.
**Articulo:** Art. 26 inc. 4; Art. 37 inc. 1.
**Obligacion:** Consentimiento escrito con firma autografa o equivalente, expreso e inequivoco, con advertencia del derecho a no prestarlo; nadie puede ser obligado a dar datos sensibles.
**A quien aplica:** Responsables.
**Implicacion para el software:** Flujo de consentimiento en modo sensible: documento firmado obligatorio, texto de advertencia obligatorio, campo "alternativa ofrecida si se niega".
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pags. 15 y 18 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (salvo excepciones Art. 37 inc. 2 y 3, Art. 38).

**Norma:** LPDP, D.L. 144.
**Articulo:** Art. 37 inc. 2 y 3; Art. 38; Art. 28 lit. b, c, d.
**Obligacion:** Excepciones al consentimiento para sensibles: vida del titular, salud por profesional sujeto a secreto, interes general o mandato legal, disociacion.
**A quien aplica:** Responsables.
**Implicacion para el software:** Campo "excepcion aplicable" con lista cerrada y justificacion; para salud, registro de la obligacion de secreto del personal.
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pags. 15, 16, 18 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** CONDICIONAL.

**Norma:** LPDP, D.L. 144.
**Articulo:** Art. 59 lit. a y b; Art. 56 lit. b num. 6.
**Obligacion:** Prohibido crear bases de datos sensibles o tratar categorias del Art. 59 lit. b fuera del capitulo IV del Titulo II; infraccion grave.
**A quien aplica:** Sujetos obligados.
**Implicacion para el software:** Toda actividad con datos sensibles sin via licita documentada se marca "riesgo alto: prohibicion Art. 59".
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pags. 25 y 26 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

**Norma:** Normativa para el Desarrollo del Procedimiento Administrativo Sancionador (ACE).
**Articulo:** Art. 32 inc. sobre sensibles; Art. 43 lit. e.
**Obligacion:** Los datos sensibles agravan la calificacion y proporcionalidad de la sancion.
**A quien aplica:** Sujetos obligados en procedimiento sancionador.
**Implicacion para el software:** Ponderar "sensible" como factor en la matriz de riesgo interna y en la priorizacion de tareas.
**Fuente oficial:** `fuentes\normativa_sancionadora_OCR.txt` (pags. 27 y 28 del D.O. 11 ago 2026); imagen `fuentes\ocr\normativa_sancionadora\page-08.png` (2026-09-23).
**Vigencia:** VIGENTE (desde 19 ago 2026).
**Clasificacion:** HECHO relevante para riesgo.

**Norma:** Ley de Deberes y Derechos de los Pacientes y Prestadores de Servicios de Salud, D.L. 307.
**Articulo:** Arts. 15, 17, 20, 33 lit. c y d.
**Obligacion:** Consentimiento clinico escrito y firmado; confidencialidad del expediente; custodia con medidas tecnicas.
**A quien aplica:** Prestadores de servicios de salud publicos y privados.
**Implicacion para el software:** Para clientes del sector salud, plantilla de actividad "expediente clinico" con base "mandato legal / secreto profesional", control de acceso y registro de divulgaciones autorizadas por escrito.
**Fuente oficial:** https://asp.salud.gob.sv/regulacion/pdf/ley/ley_deberes_y_derechos_pacientes_y_prestadores_servicios_de_salud.pdf (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** CONDICIONAL (solo prestadores de salud).

**Norma:** Ley General de Prevencion de Riesgos en los Lugares de Trabajo, D.L. 254.
**Articulo:** Art. 8 num. 3 y 6; Art. 63; Art. 66.
**Obligacion:** Registro de accidentes y enfermedades profesionales; programa de examenes medicos; examenes ordenados confidenciales y nunca en perjuicio del trabajador; notificar accidentes en 72 horas.
**A quien aplica:** Empleadores.
**Implicacion para el software:** Actividad "salud ocupacional" con base obligacion legal, acceso restringido, registro de a quien se comunican resultados.
**Fuente oficial:** https://natlex.ilo.org/dyn/natlex2/natlex2/files/download/84122/SLV84122.pdf (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (registro y confidencialidad) / CONDICIONAL (examenes segun riesgo determinado por la autoridad).

---

## 5. Ninez y adolescencia

### 5.1 LPDP

- Art. 5 lit. j: principio de ejercicio progresivo de las facultades: los derechos de NNA "seran ejercidos de manera progresiva tomando en consideracion el desarrollo evolutivo de sus facultades, su condicion o situacion individual, la direccion y orientacion apropiada de sus padres, madres o de quien ejerza la representacion legal, y las disposiciones establecidas en la legislacion vigente".
- Art. 26 inc. 2: el consentimiento de NNA "para proporcionar sus datos personales" se rige por ese principio "en lo pertinente y adecuado".
- Art. 42: en todo tratamiento se garantiza el interes superior; ejercer derechos implica informar previamente a NNA y a sus progenitores o tutores; informacion "en un lenguaje claro, sencillo y adaptado a su edad y capacidad de comprension", accesible en todo momento.
- Art. 10 lit. f: causal de cancelacion cuando los datos se obtuvieron "en relacion con la oferta de servicios de la sociedad de la informacion ... en el caso de oferta directa a ninos".
- Art. 12 lit. b: en la ponderacion de interes legitimo prevalecen los derechos del titular "en particular cuando el titular sea un nino o nina".
- Art. 50 lit. e: la ACE promueve divulgacion "con especial enfasis en la ninez, adolescencia y adultos mayores".
- Art. 56 lit. c num. 3: infraccion muy grave "el uso de los datos personales de ninos, ninas y adolescentes sin el previo consentimiento de sus padres, representantes o tutores, de conformidad con las leyes vigentes o tratados internacionales".
- Los formularios ACE de ARCO-POL incluyen la casilla "Los datos corresponden a: Ninez y Adolescencia" y piden "copia de certificacion de partida de nacimiento" o "carne de minoridad" para acreditar (`fuentes\ace_form_acceso.txt`, `fuentes\ace_form_cancelacion.txt`).

La LPDP no fija una edad a partir de la cual un adolescente puede consentir por si mismo el tratamiento de sus datos. Remite a "las leyes vigentes".

### 5.2 Ley Crecer Juntos (LEPINA derogada)

Ley Crecer Juntos para la Proteccion Integral de la Primera Infancia, Ninez y Adolescencia, D.L. 431, aprobada 22 jun 2022, vigente desde el 1 ene 2023 (Art. 308). Fuente: https://crecerjuntos.gob.sv/dist/documents/DECRETO_LEY.pdf (2026-09-23). Segun fuente secundaria (NATLEX) publicada en D.O. N. 117, Tomo 435; numero de D.O. pendiente de confirmar en fuente primaria.

- Art. 288: "Derogase el Decreto Legislativo n. 839, del 26 de marzo de 2009 ... que contiene la Ley de Proteccion Integral de la Ninez y Adolescencia, en adelante LEPINA". Confirmado: la LEPINA esta DEROGADA.
- Art. 3: derechos aplicables "desde el instante de la concepcion hasta que cumpla los dieciocho anos de edad, y seran ejercidos directamente por las ninas, ninos y adolescentes, tomando en consideracion el desarrollo evolutivo de sus facultades, la direccion y orientacion apropiada de su madre y padre o responsable y las limitaciones establecidas en la presente Ley".
- Art. 4: "La ninez comprende desde la concepcion hasta antes de cumplir los doce anos, y la adolescencia, desde los doce hasta cumplir los dieciocho anos." Primera infancia: hasta cumplir ocho anos.
- Art. 5: en caso de duda sobre la edad se presume nino antes que adolescente.
- Art. 77 (derechos al honor, imagen, vida privada e intimidad): "Se permitiran publicaciones que destaquen aspectos positivos de ninas, ninos y adolescentes en cualquier entorno siempre que no sea en contra de su voluntad. En el caso de las ninas y ninos, sera necesario su consentimiento ademas del conocimiento y aprobacion de sus padres, representantes o responsables. Cuando se trate de adolescentes bastara su consentimiento." Prohibe divulgar voz o imagen contrariando la ley y "publicar, compartir, enviar, distribuir, exponer o divulgar datos, informacion, voz e imagenes que lesionen el honor ... o que constituyan injerencias arbitrarias o ilegales en su vida privada o intimidad personal y familiar, incluidos aquellos con fines comerciales o proselitistas, sin el consentimiento expreso de sus madres, padres, representantes o responsables". Tambien prohibe intervenir comunicaciones de NNA salvo la supervision parental.

### 5.3 Coordinacion entre ambas leyes (punto para abogado)

```
LPDP Art. 56 c) 3          : datos de NNA sin consentimiento de padres/representantes = muy grave,
                             "de conformidad con las leyes vigentes"
Crecer Juntos Art. 77      : para publicaciones de imagen, adolescente (12-17) consiente por si solo;
                             nino (<12) consiente + aprobacion parental;
                             uso comercial de datos que afecte intimidad exige consentimiento
                             expreso de padres
LPDP Art. 5 j) y 26 inc. 2 : ejercicio progresivo
```

Lectura conservadora recomendada para el software (no es norma):
- Menores de 12 anos: consentimiento del padre, madre, representante o responsable siempre; ademas recabar la voluntad del nino cuando la finalidad sea publicacion de imagen.
- Adolescentes de 12 a 17: consentimiento del representante como regla (Art. 56 lit. c num. 3 LPDP) y del adolescente; solo un abogado puede validar si en casos concretos basta el del adolescente por aplicacion del Art. 77 Crecer Juntos.
- Uso comercial o de marketing dirigido a NNA: consentimiento expreso parental (Art. 77 lit. b Crecer Juntos) y evaluar la ponderacion agravada del Art. 12 lit. b LPDP.
- Siempre: aviso e informacion en lenguaje adaptado a la edad, dirigido tambien a padres (Art. 42), y causal de cancelacion reforzada (Art. 10 lit. f).

### 5.4 Bloques de obligacion (ninez)

**Norma:** LPDP, D.L. 144.
**Articulo:** Art. 56 lit. c num. 3; Art. 26 inc. 2; Art. 5 lit. j.
**Obligacion:** No usar datos de NNA sin consentimiento previo de padres, representantes o tutores conforme a las leyes vigentes; aplicar ejercicio progresivo.
**A quien aplica:** Responsables.
**Implicacion para el software:** Marca "titular NNA" por actividad; captura obligatoria de identidad y vinculo del representante; registro de la manifestacion del propio NNA cuando corresponda; alerta si la finalidad es comercial.
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pags. 6, 15, 25 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (cuando el titular es NNA).

**Norma:** LPDP, D.L. 144.
**Articulo:** Art. 42.
**Obligacion:** Garantizar el interes superior; informar a NNA y a sus progenitores o tutores en lenguaje adaptado a la edad; informacion accesible en todo momento.
**A quien aplica:** Responsables.
**Implicacion para el software:** Plantilla de aviso "version para NNA" y "version para representantes"; ambas vinculadas al mismo tratamiento.
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pag. 19 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (cuando hay NNA).

**Norma:** Ley Crecer Juntos, D.L. 431.
**Articulo:** Arts. 4, 77 y 288.
**Obligacion:** Rangos de edad (ninez hasta antes de 12, adolescencia 12 a 17); consentimiento para uso de imagen y datos con fines comerciales; LEPINA derogada.
**A quien aplica:** Toda persona natural o juridica que publique o use datos, voz o imagen de NNA.
**Implicacion para el software:** Calcular categoria de edad a partir de fecha de nacimiento; exigir consentimiento parental expreso para finalidades comerciales; registrar consentimiento del propio NNA para publicaciones.
**Fuente oficial:** https://crecerjuntos.gob.sv/dist/documents/DECRETO_LEY.pdf (2026-09-23).
**Vigencia:** VIGENTE (desde 1 ene 2023).
**Clasificacion:** OBLIGATORIO (cuando hay NNA) / CONDICIONAL (regla del adolescente segun finalidad).

---

## 6. Datos laborales

### 6.1 Normas que obligan al patrono a tratar datos de empleados

| Norma | Articulo | Que obliga | Datos implicados |
|---|---|---|---|
| Codigo de Trabajo | Art. 18 | Contrato individual por escrito en tres ejemplares; el patrono remite uno a la Direccion General de Trabajo en 8 dias | identidad, domicilio, salario |
| Codigo de Trabajo | Art. 23 | Contenido del contrato escrito: nombre, apellido, sexo, edad, estado civil, profesion, domicilio, residencia, nacionalidad, documento de identidad, trabajo, plazo, fecha de inicio, lugar, horario, salario, forma de pago, herramientas, "nombre y apellido de las personas que dependan economicamente del trabajador", firma o huella | datos de identificacion y de terceros (dependientes) |
| Codigo de Trabajo | Art. 138 | "Todo patrono esta obligado a llevar planillas o recibos de pago" con salarios, horas, dias, comisiones, firmados o con huella del trabajador; copia al trabajador con descuentos | salario, jornada, descuentos, huella dactilar |
| Codigo de Trabajo | Art. 117 | Registro de trabajadores menores de 18 (fecha de nacimiento, trabajo, horario, salario) y examen medico previo y periodico | datos de NNA y de salud |
| Codigo de Trabajo | Art. 29 num. 6 lit. b | Licencia por muerte o enfermedad grave de conyuge, ascendientes, descendientes o dependientes "que aparezcan nominadas en el respectivo contrato ... o en cualquier registro de la empresa" | datos familiares |
| Codigo de Trabajo | Art. 304 lit. f | Reglamento interno debe regular examenes medicos previos o periodicos | salud |
| Reglamento para la Aplicacion del Regimen del Seguro Social, D.E. 37 (1954) | Art. 7 | Patrono debe inscribirse en 5 dias e inscribir a los trabajadores en 10 dias desde su ingreso, con formularios del ISSS | identificacion, beneficiarios |
| Reglamento ISSS | Art. 49 | Remision de planillas dentro de los primeros 5 dias habiles del mes siguiente; multa por no remitir | salario, cotizaciones |
| Ley Integral del Sistema de Pensiones, D.L. 614 (D.O. N. 241, Tomo 437, 21 dic 2022) | Art. 8 | Afiliacion obligatoria al ingresar a trabajo subordinado; si en 20 dias el trabajador no elige AFP, el empleador lo afilia en la de mayor numero de trabajadores | identificacion, AFP elegida |
| Ley Integral del Sistema de Pensiones | Art. 13 y 16 | Cotizacion mensual obligatoria; 7.25 por ciento trabajador y 8.75 por ciento empleador | ingreso base, cotizaciones |
| LGPRLT, D.L. 254 | Art. 8 num. 3 y 6, Art. 63, Art. 66 | Registro de accidentes y enfermedades; examenes medicos; confidencialidad; aviso de accidentes en 72 horas | salud, accidentes |

No se localizo en el Codigo de Trabajo un articulo que fije un plazo general de conservacion del expediente laboral. Las fuentes secundarias mencionan plazos de conservacion para ciertos registros (por ejemplo cinco anos para registros del trabajo a domicilio), pero no se verifico un plazo general en fuente primaria. Los plazos de prescripcion laboral y tributaria son los que en la practica determinan la conservacion; punto para abogado.

### 6.2 Base de licitud para datos de empleados y candidatos

- Contrato y medidas precontractuales (Art. 5 lit. g num. 2) cubre reclutamiento, contratacion, gestion del contrato. Concuerda con la excepcion Art. 28 lit. f: "cuando deriven de una relacion contractual, cientifica o profesional del titular de los datos personales, y sean necesarios para su desarrollo o cumplimiento".
- Obligacion legal (Art. 5 lit. g num. 3) cubre planillas, ISSS, AFP, retenciones de renta, registro de menores, salud ocupacional, avisos al MTPS.
- Consentimiento (num. 1): fuente secundaria (ECIJA, 2026-09-23) sostiene que la LPDP exige consentimiento expreso del empleado y que "no puede inferirse del contrato de trabajo, ni considerarse tacito por la subordinacion". La lectura de este informe es que el consentimiento es inadecuado como base principal para tratamientos que la ley impone al patrono, porque el trabajador no puede negarse a ellos (no seria "libre" en el sentido del Art. 27 lit. a) ni revocarlos con efecto (Art. 29 inc. 2 preserva el tratamiento apoyado en otra causal). El consentimiento queda para usos adicionales: fotografia en redes, comunicaciones no laborales, beneficios voluntarios, biometria, referencias a terceros.
- Datos sensibles en el expediente (salud, afiliacion sindical, huella): via Art. 38 (mandato legal) cuando la ley lo exige; consentimiento escrito con firma en lo demas.
- Candidatos no contratados: la base contractual (medidas precontractuales) termina con el proceso; conservar CV para futuras vacantes requiere consentimiento o justificacion de interes legitimo y periodo definido (Art. 5 lit. h temporalidad).

### 6.3 Como documentarlo en el software

- Actividad "Gestion de personal" con sub-actividades: reclutamiento, contratacion, nomina y planillas, seguridad social (ISSS, AFP), salud ocupacional, control de asistencia, videovigilancia, capacitacion, terminacion. Cada una con base, norma citada y periodo de conservacion.
- Aviso de privacidad para empleados y candidatos (Art. 24), entregado por escrito y con constancia de recepcion (Art. 54); recomendable incorporar un capitulo de datos en el reglamento interno de trabajo (CT Art. 303 y 304) segun sugiere la fuente secundaria, marcandolo como buena practica.
- Consentimientos separados y revocables solo para usos no necesarios.
- Registro de encargados: proveedor de nomina, AFP, ISSS (estos ultimos actuan por mandato legal, no como encargados de la empresa; abogado).

### 6.4 Bloques de obligacion (laboral)

**Norma:** Codigo de Trabajo.
**Articulo:** Arts. 18, 23, 138, 117.
**Obligacion:** Contrato escrito con datos minimos y copia a la Direccion General de Trabajo; planillas o recibos firmados por el trabajador; registro de menores.
**A quien aplica:** Patronos.
**Implicacion para el software:** Plantilla RAT "empleados" con base obligacion legal y contrato, con la norma precargada; categoria "dependientes economicos" como datos de terceros.
**Fuente oficial:** https://webapps.ilo.org/public/spanish/region/ampro/mdtsanjose/papers/cod_elsa.htm (2026-09-23); texto oficial consolidado en asamblea.gob.sv.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

**Norma:** Reglamento para la Aplicacion del Regimen del Seguro Social, D.E. 37.
**Articulo:** Art. 7 y Art. 49.
**Obligacion:** Inscribir trabajadores en 10 dias desde su ingreso; remitir planillas mensuales en los primeros 5 dias habiles del mes siguiente.
**A quien aplica:** Patronos con trabajadores sujetos al regimen.
**Implicacion para el software:** Base obligacion legal para el flujo ISSS; el plazo de 10 dias no es un plazo de la LPDP, pero puede alimentar el calendario de la empresa como referencia.
**Fuente oficial:** https://sansalvador.eregulations.org/media/REGLAMENTO%20PARA%20LA%20APLICACION%20DEL%20REGIMEN%20DEL%20SEGURO%20SOCIAL%2009.pdf (2026-09-23).
**Vigencia:** VIGENTE (con reformas hasta 2007 segun la copia consultada; verificar reformas posteriores).
**Clasificacion:** OBLIGATORIO.

**Norma:** Ley Integral del Sistema de Pensiones, D.L. 614.
**Articulo:** Arts. 8, 13 y 16.
**Obligacion:** Afiliacion obligatoria, respeto a la eleccion de AFP, afiliacion por el empleador a los 20 dias si el trabajador no elige, cotizacion mensual.
**A quien aplica:** Empleadores publicos y privados.
**Implicacion para el software:** Base obligacion legal; transferencia de datos a la AFP como comunicacion legalmente exigida.
**Fuente oficial:** https://ssf.gob.sv/wp-content/uploads/2023/02/Ley-Integral-del-Sistema-de-Pensiones.pdf (2026-09-23).
**Vigencia:** VIGENTE (desde dic 2022).
**Clasificacion:** OBLIGATORIO.

---

## 7. Marketing directo y comunicaciones comerciales

### 7.1 LPDP

- Art. 12: "Es el derecho del interesado a solicitar el cese en el tratamiento de sus datos personales, incluida la elaboracion de perfiles o clasificaciones con fines comerciales o de mercadotecnia directa." No cabe oposicion cuando la base es interes publico (lit. a) o interes legitimo prevalente (lit. b), "en particular cuando el titular sea un nino o nina" prevalecen sus derechos.
- Art. 32: prohibido tratar o transferir datos "para ofrecer otro tipo de servicios o cualquier finalidad diferente a la que estos fueron recabados, sin previa autorizacion del titular". Usar datos de clientes para marketing de terceros o de productos ajenos a la relacion requiere autorizacion previa.
- Art. 56 lit. b num. 3 (finalidad distinta, grave) y lit. c num. 7 (comercializar datos sin consentimiento, muy grave); Art. 59 lit. d (utilizar, transferir, compartir y comercializar en contravencion a la ley).
- Cookies: Art. 4 lit. e las define como informacion almacenada en el navegador para "recordar accesos y conocer informacion sobre los habitos de navegacion"; Art. 24 lit. i exige que el aviso informe "el uso de cookies". La ley no dice que las cookies requieran consentimiento; pero si con ellas se identifican o perfilan personas, hay tratamiento y aplica el regimen general (base, finalidad, oposicion). "Habitos personales" es categoria sensible en el Art. 4 lit. g; abogado debe evaluar si el perfilado de habitos de navegacion entra en esa categoria.

### 7.2 Ley de Comercio Electronico (D.L. 463, sancionada 6 feb 2020, vigente un ano despues de su publicacion, Art. 29; segun fuentes secundarias D.O. 10 feb 2020, vigente 11 feb 2021)

> Art. 13.- Los proveedores de bienes y servicios que deseen enviar comunicaciones, de caracter publicitario o de promociones, y que no cuenten con el previo consentimiento del usuario para remitirle este tipo de comunicaciones, solo podran hacerlo si cumplen los siguientes requisitos: a) Indicar expresamente en las mismas, que constituyen una comunicacion comercial electronica publicitaria o promocional no solicitada. b) Incluir en el mensaje una opcion sencilla, gratuita y viable para solicitar la exclusion de las listas de destinatarios del mismo en cualquier momento. c) Que los datos de los destinatarios hayan sido obtenidos sin infringir los derechos de proteccion de datos personales.

Tension: esta ley (2020) admite envios sin consentimiento previo con etiqueta y opt-out; la LPDP (2024) exige base de licitud y autorizacion previa para finalidades distintas (Art. 32) y tiene caracter especial y derogatorio de lo que la contrarie (Art. 63). Lectura prudente: el Art. 13 lit. c remite a la proteccion de datos, por lo que el envio sin consentimiento solo es viable si la obtencion y el uso de los datos para marketing tienen base licita bajo la LPDP (por ejemplo, consentimiento al recabar, o interes legitimo documentado respecto de clientes existentes para productos propios). Requiere abogado.

### 7.3 Ley de Proteccion al Consumidor (D.L. 776, 2005, con reformas)

- Art. 18 lit. g: prohibido "compartir informacion personal y crediticia del consumidor, ya sea entre proveedores o a traves de entidades especializadas ... sin la debida autorizacion del consumidor". Practica abusiva; realizar practicas abusivas es infraccion muy grave (Art. 44 lit. e).
- Art. 18 lit. f: prohibido publicar por cualquier medio "nombres, datos personales o fotografias" por incumplimiento de obligaciones crediticias, y gestiones de cobro difamatorias.
- Art. 31 lit. a: es publicidad ilicita la que "vulnere el derecho al honor, a la intimidad y a la propia imagen ... especialmente en lo que se refiere a la mujer, juventud, infancia o grupos minoritarios"; lit. b publicidad enganosa. Difundir publicidad ilicita es infraccion grave (Art. 43 lit. g).
- La LPC no contiene una regla especifica sobre listas de marketing ni sobre comunicaciones no solicitadas por telefono o mensajeria; la regla operativa es la del Art. 18 lit. g (autorizacion para compartir datos) mas la LPDP.

### 7.4 WhatsApp, SMS y correo electronico

No hay norma salvadorena especifica por canal. Aplican: LPDP (base, finalidad, oposicion, revocacion), Ley de Comercio Electronico Art. 13 (etiqueta y exclusion en comunicaciones electronicas no solicitadas) y LPC Art. 18 lit. g. El uso de WhatsApp implica ademas un encargado o receptor extranjero (Meta) y transferencia internacional (Arts. 40, 44, 45 LPDP), fuera de este lente.

Implicacion para el software (marketing):
- Registro de origen de cada contacto (formulario propio, compra de lista, red social, referido) y de la base para marketing.
- Preferencias por canal y por finalidad, con registro de opt-in y opt-out, fecha y evidencia.
- Lista de supresion que persista tras la cancelacion de datos, con base "cumplimiento de la oposicion" (Art. 12, Art. 11 bloqueo).
- Plantillas de mensaje con etiqueta "comunicacion comercial no solicitada" y enlace de exclusion cuando no exista consentimiento previo.
- Marca "perfilado" en actividades que clasifiquen personas con fines comerciales, para gestionar la oposicion del Art. 12.
- Control de "finalidad diferente" al reutilizar datos de clientes para nuevos productos o terceros (Art. 32).

### 7.5 Bloques de obligacion (marketing)

**Norma:** LPDP, D.L. 144.
**Articulo:** Art. 12; Art. 32; Art. 56 lit. b num. 3 y lit. c num. 7; Art. 59 lit. d.
**Obligacion:** Atender la oposicion al marketing directo y al perfilado; no usar datos para finalidades distintas sin autorizacion previa; no comercializar datos sin consentimiento.
**A quien aplica:** Responsables privados.
**Implicacion para el software:** Gestion de preferencias y supresion; control de finalidad; alerta al reutilizar datos.
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pags. 9, 17, 25, 26 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

**Norma:** LPDP, D.L. 144.
**Articulo:** Art. 4 lit. e; Art. 24 lit. i.
**Obligacion:** Informar el uso de cookies en el aviso de privacidad.
**A quien aplica:** Responsables con sitios web o apps.
**Implicacion para el software:** Seccion "cookies" obligatoria en el generador de aviso; inventario de cookies por finalidad; el software no impone banner de consentimiento pero permite documentar la base elegida.
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pags. 3 y 14 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (informar) / decision juridica (consentimiento para cookies).

**Norma:** Ley de Comercio Electronico, D.L. 463.
**Articulo:** Art. 13.
**Obligacion:** Comunicaciones comerciales electronicas sin consentimiento previo solo con etiqueta expresa, opcion de exclusion sencilla y gratuita y datos obtenidos sin infringir la proteccion de datos.
**A quien aplica:** Proveedores de bienes y servicios que envian comunicaciones electronicas.
**Implicacion para el software:** Plantillas y checklist para campanas sin consentimiento previo; registro de exclusiones.
**Fuente oficial:** https://www.jurisprudencia.gob.sv/DocumentosBoveda/D/2/2020-2029/2020/02/DB418.PDF (2026-09-23).
**Vigencia:** VIGENTE (fecha de D.O. segun fuente secundaria).
**Clasificacion:** CONDICIONAL (solo si se envia sin consentimiento previo).

**Norma:** Ley de Proteccion al Consumidor, D.L. 776.
**Articulo:** Art. 18 lit. f y g; Art. 31 lit. a; Art. 43 lit. g; Art. 44 lit. e.
**Obligacion:** No compartir informacion personal y crediticia sin autorizacion; no publicar datos de deudores; publicidad que no vulnere intimidad e imagen.
**A quien aplica:** Proveedores frente a consumidores.
**Implicacion para el software:** Registro de autorizaciones para compartir datos con terceros comerciales; alerta en actividades de cobranza.
**Fuente oficial:** https://www.defensoria.gob.sv/wp-content/uploads/2021/09/Ley-de-Proteccion-al-Consumidor-AL.pdf (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (en relaciones de consumo).

---

## 8. Fuentes de acceso publico

- Art. 4 lit. l: "Fuentes de acceso publico: aquellas bases de datos o repositorios de administracion publica o privada cuya consulta puede ser realizada por disposicion de ley por cualquier persona o medio, por el abono de una contraprestacion o tarifa." Elementos: (1) base o repositorio, (2) consulta habilitada por disposicion de ley, (3) abierta a cualquier persona, con o sin tarifa.
- Art. 28 lit. a: no se requiere consentimiento "cuando los datos personales figuren en fuentes de acceso publico, siempre y cuando no constituyan datos personales sensibles".
- Art. 28 lit. g: tampoco "cuando se trate de datos personales que el titular ha hecho ya manifiestamente publicos". Es una excepcion distinta, basada en la conducta del titular y no en una disposicion legal.
- Art. 3 lit. d excluye de la ley el tratamiento realizado "en los registros publicos" (por el registro mismo); no excluye a la empresa que extrae datos de esos registros y los incorpora a sus bases.

Consecuencias:
- Registros publicos consultables por ley (registro de comercio, registro de la propiedad, boletines oficiales, listas profesionales) encajan en la definicion; los datos ahi obtenidos pueden tratarse sin consentimiento, con aviso e informacion al titular (Art. 7 y 24 siguen aplicando) y respetando finalidad y oposicion.
- Redes sociales y sitios web abiertos no son "fuentes de acceso publico" en sentido legal porque su consulta no esta habilitada "por disposicion de ley". Podria aplicar el Art. 28 lit. g si el titular hizo el dato manifiestamente publico, con criterio restrictivo; datos sensibles quedan fuera en todo caso por el Art. 37.
- Software: campo "origen del dato" con valores (titular directo, fuente de acceso publico con cita de la ley habilitante, dato manifiestamente publico con evidencia, tercero con base documentada, encargado); si la categoria es sensible, no admitir origen "fuente de acceso publico".

**Norma:** LPDP, D.L. 144.
**Articulo:** Art. 4 lit. l; Art. 28 lit. a y g.
**Obligacion:** Solo las bases consultables por disposicion de ley son fuentes de acceso publico; la excepcion no cubre datos sensibles.
**A quien aplica:** Responsables.
**Implicacion para el software:** Origen del dato con justificacion; bloqueo para sensibles.
**Fuente oficial:** `fuentes\ace_decreto_144.txt` pags. 4 y 15 (2026-09-23).
**Vigencia:** VIGENTE.
**Clasificacion:** CONDICIONAL.

---

## 9. Tratamientos tipicos: bases habituales y documentos exigidos

La decision final sobre la base es siempre de la empresa. La columna "bases habituales" refleja el analisis de este informe, no una regla de la ACE.

| Tratamiento | Bases habituales (Art. 5 lit. g) y excepciones | Documentos que la ley exige o presupone | Documentos recomendados | Alertas del software |
|---|---|---|---|---|
| Empleados (expediente, nomina, ISSS, AFP) | Obligacion legal (num. 3: CT 18, 23, 138; Regl. ISSS 7 y 49; LISP 8, 13; LGPRLT 8, 63) y contrato (num. 2; Art. 28 lit. f) | Contrato escrito (CT 23); planillas (CT 138); aviso de privacidad (Art. 24) con constancia escrita (Art. 54); RAT (Politicas ACE Art. 4) | Capitulo de datos en reglamento interno (CT 303-304); acuerdos de confidencialidad con proveedor de nomina (Art. 33 inc. 2, 41) | Sensibles en el expediente (salud, sindicato, huella en planilla) exigen via Art. 38 o consentimiento firmado |
| Candidatos | Medidas precontractuales (num. 2); consentimiento para conservar CV tras el proceso | Aviso de privacidad al recolectar (Art. 7 y 24) | Politica de retencion de CV con plazo (Art. 5 lit. h) | Datos sensibles en CV (foto, salud, religion): advertir de minimizacion (Art. 5 lit. d) |
| Clientes (contrato, facturacion, soporte) | Contrato (num. 2; Art. 28 lit. f); obligacion legal (facturacion, tributaria) | Aviso de privacidad (Art. 24); RAT; contratos con encargados (Art. 33 inc. 2) | Clausulas de datos en contratos de servicio | Reutilizar para marketing o terceros = finalidad distinta (Art. 32) |
| Videovigilancia | Interes legitimo (num. 6) con ponderacion, o consentimiento; Politicas ACE la reconocen como medida fisica | Aviso visible en el establecimiento (Art. 16 lit. g, Art. 24); RAT; periodo de conservacion (Art. 5 lit. h) | Registro de accesos a grabaciones; protocolo de entrega a autoridades | Reconocimiento facial = biometria = sensible; no hay lineamiento ACE |
| Biometria de asistencia | Consentimiento escrito con firma (Art. 26 inc. 4, 37) con alternativa no biometrica; no hay mandato legal para el sector privado | Documento firmado con advertencia del derecho a no prestarlo (Art. 37) y aviso (Art. 24 lit. b identificando sensibles) | Evaluacion de impacto (Politicas ACE Art. 4 lit. e); plantilla o cifrado (Art. 36) | Libertad del consentimiento del empleado discutible (Art. 27 lit. a); abogado |
| Marketing directo | Consentimiento (num. 1) como regla; interes legitimo solo con ponderacion y para clientes propios (abogado); Ley Comercio Electronico Art. 13 para envios sin consentimiento previo | Registro de consentimiento u opt-in (Art. 54); aviso con finalidad de marketing y mecanismo de revocacion (Art. 24 lit. d y e); mecanismo de oposicion (Art. 12) | Lista de supresion; etiqueta y enlace de exclusion (LCE Art. 13) | Perfilado, NNA (Art. 12 lit. b, Crecer Juntos Art. 77), compra de listas (LPC Art. 18 lit. g) |
| App movil y sitio web (cuentas, cookies, analitica) | Contrato para la cuenta (num. 2); consentimiento para cookies no necesarias y perfilado (decision de la empresa); informar cookies (Art. 24 lit. i) | Aviso de privacidad en la app y en la web (Art. 7 inc. 3, Art. 24); RAT; informacion sobre nube y respaldos (Art. 7 lit. b y c) | Inventario de cookies y SDK; registro de versiones del aviso | Proveedores cloud extranjeros = transferencia internacional (fuera de este lente) |
| Salud ocupacional | Obligacion legal o mandato legal (num. 3; Art. 38: LGPRLT 8, 63, 66; CT 117, 304 lit. f); intereses vitales en accidentes (num. 4; Art. 28 lit. c) | Registro de accidentes (LGPRLT 8 num. 3); resultados confidenciales (LGPRLT 63); aviso a empleados (Art. 24 lit. b identificando salud) | Acceso restringido a medico o comite; obligacion de secreto documentada (Art. 37 inc. 3) | Uso para fines distintos (despidos, seguros) prohibido por LGPRLT 63 y Art. 32 LPDP |

---

## 10. Incertidumbres y puntos que requieren abogado

1. Alcance real de la infraccion muy grave 1 (Art. 56 lit. c num. 1) frente a tratamientos apoyados en contrato, obligacion legal o interes legitimo sin consentimiento. La ley no lo aclara y la ACE no ha emitido guia. Es el riesgo central del lente.
2. Si el "principio de consentimiento y finalidad" del Art. 5 lit. c y la formulacion de las Politicas ACE (Art. 3 lit. c "autorizacion explicita del titular") desplazan en la practica a las bases 2 a 6 del Art. 5 lit. g.
3. Contenido del test de interes legitimo (Art. 5 lit. g num. 6): la ley no define como ponderar; el software puede ofrecer una plantilla, pero su validez depende de criterio juridico.
4. Consentimiento de empleados: si es "libre" (Art. 27 lit. a) dada la subordinacion; fuentes secundarias divergen.
5. Coordinacion entre LPDP Art. 56 lit. c num. 3 (consentimiento parental) y Ley Crecer Juntos Art. 77 (adolescente consiente por si solo para publicaciones de imagen). No hay edad de consentimiento digital en la LPDP.
6. Firma electronica simple como "equivalente" de la autografa para datos sensibles (Art. 26 inc. 4): valida en derecho (LFE Art. 6) pero con menor fuerza probatoria; conviene definir el estandar de la empresa.
7. Catalogo de sensibles: divergencia entre Art. 4 lit. g y Art. 59 lit. b ("nacionalidad", "convicciones filosoficas"); alcance de "habitos personales" y "situacion moral y familiar" frente a analitica y perfilado.
8. Biometria de asistencia en el sector privado: sin mandato legal, depende de consentimiento firmado y de alternativa real; no hay lineamiento ACE.
9. Videovigilancia: base (interes legitimo o consentimiento), plazo de conservacion y senalizacion; no hay lineamiento ACE.
10. Cookies: la ley solo exige informar (Art. 24 lit. i); si el perfilado por cookies requiere consentimiento y si "habitos de navegacion" son "habitos personales" sensibles.
11. Relacion entre Ley de Comercio Electronico Art. 13 (envios sin consentimiento con opt-out) y LPDP Art. 32 y 63 (especialidad y derogatoria de lo que la contrarie).
12. Fuentes de acceso publico: que registros salvadorenos cumplen "por disposicion de ley"; tratamiento de datos de redes sociales bajo Art. 28 lit. g.
13. Plazo general de conservacion del expediente laboral: no localizado en fuente primaria; depende de prescripciones laborales y tributarias.
14. Reforma D.L. 659: texto oficial no localizado; se asume que no toca Arts. 26 a 32 ni 37 a 39, pero solo el texto publicado lo confirmara. Vigencia pendiente de publicacion en el Diario Oficial (verificado el 2026-09-23 sin resultado).
15. Fecha de emision y publicacion de las Politicas de Actuacion ACE N. 001-0309025-DPDP: pendiente de verificar.
16. Numero y fecha del Diario Oficial de la Ley Crecer Juntos: dato de fuente secundaria (NATLEX: D.O. N. 117, Tomo 435, 22 jun 2022), pendiente de confirmar en fuente primaria.
17. Fecha de publicacion en D.O. de la Ley de Comercio Electronico: fuente secundaria (10 feb 2020); el texto consultado solo muestra sancion presidencial del 6 feb 2020 y vigencia un ano despues de la publicacion.

---

## 11. Fuentes consultadas (fecha de consulta 2026-09-23)

Fuentes primarias locales:
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt` (LPDP, D.L. 144, texto integro publicado por la ACE).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\diario_oficial_2024-11-15_mh.txt` (D.O. N. 219, Tomo 445).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_politicas_protecciondatos.txt` (Politicas N. 001-0309025-DPDP).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\normativa_sancionadora_OCR.txt` y `fuentes\ocr\normativa_sancionadora\page-07.png`, `page-08.png` (Normativa Sancionadora ACE, D.O. 11 ago 2026).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\lineamientos_dpo_OCR.txt` (Lineamientos para el Delegado, D.O. 11 ago 2026; no contiene reglas sobre consentimiento, sensibles ni menores).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_form_acceso.txt`, `ace_form_cancelacion.txt`, `ace_form_portabilidad.txt` (formularios ACE version 07-07-2025).

Fuentes primarias en linea:
- ACE, politicas y normativas: https://ace.gob.sv/politicas.php
- ACE, formularios: https://ace.gob.sv/page/formularios
- Asamblea Legislativa, nota oficial sobre la reforma (17 sep 2026): https://www.asamblea.gob.sv/node/14116
- Ley Crecer Juntos, D.L. 431: https://crecerjuntos.gob.sv/dist/documents/DECRETO_LEY.pdf
- Codigo de Trabajo (texto ILO): https://webapps.ilo.org/public/spanish/region/ampro/mdtsanjose/papers/cod_elsa.htm
- Reglamento para la Aplicacion del Regimen del Seguro Social, D.E. 37: https://sansalvador.eregulations.org/media/REGLAMENTO%20PARA%20LA%20APLICACION%20DEL%20REGIMEN%20DEL%20SEGURO%20SOCIAL%2009.pdf
- Ley Integral del Sistema de Pensiones, D.L. 614: https://ssf.gob.sv/wp-content/uploads/2023/02/Ley-Integral-del-Sistema-de-Pensiones.pdf
- Ley General de Prevencion de Riesgos en los Lugares de Trabajo, D.L. 254: https://natlex.ilo.org/dyn/natlex2/natlex2/files/download/84122/SLV84122.pdf
- Ley de Deberes y Derechos de los Pacientes y Prestadores de Servicios de Salud, D.L. 307: https://asp.salud.gob.sv/regulacion/pdf/ley/ley_deberes_y_derechos_pacientes_y_prestadores_servicios_de_salud.pdf
- Ley de Firma Electronica, D.L. 133: https://factura.gob.sv/wp-content/uploads/2022/10/Ley_de_Firma_Electr%C3%B3nica.pdf
- Ley de Comercio Electronico, D.L. 463: https://www.jurisprudencia.gob.sv/DocumentosBoveda/D/2/2020-2029/2020/02/DB418.PDF
- Ley de Proteccion al Consumidor, D.L. 776: https://www.defensoria.gob.sv/wp-content/uploads/2021/09/Ley-de-Proteccion-al-Consumidor-AL.pdf
- Diario Oficial (indice, sin resultado para D.L. 659): https://www.diariooficial.gob.sv/

Fuentes secundarias (orientacion; lo no confirmado en primaria se marca en el texto):
- elsalvador.com, "Aprueban reforma a la Ley de Proteccion de Datos Personales": https://www.elsalvador.com/noticias/nacional/reforma-proteccion-datos-personales/1293875/2026/
- Infobae, 17 sep 2026: https://www.infobae.com/el-salvador/2026/09/17/el-salvador-la-asamblea-legislativa-elimina-la-obligacion-del-delegado-de-proteccion-de-datos-para-las-empresas/
- ECIJA, "La Proteccion de Datos Personales y su Impacto en las Relaciones Laborales en El Salvador": https://www.ecija.com/actualidad-insights/la-proteccion-de-datos-personales-y-su-impacto-en-las-relaciones-laborales-en-el-salvador/
- NATLEX, ficha de la Ley Crecer Juntos (datos de D.O.): https://natlex.ilo.org/dyn/natlex2/r/natlex/fe/details?p3_isn=114454
- Lexology, entrada en vigencia de la Ley de Comercio Electronico: https://www.lexology.com/library/detail.aspx?g=70fb4210-ef35-45c7-8415-f95835c24673
- EY, alerta sobre lineamientos ACE (ago 2026): https://www.ey.com/es_ce/technical/tax/tax-alerts/el-salvador-la-agencia-de-ciberseguridad-del-estado-desarrolla-aspectos-relevantes-de-la-ley-de-proteccion-de-datos-personales
