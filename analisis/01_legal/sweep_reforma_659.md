# Sweep juridico: Reforma de septiembre 2026 a la LPDP (Decreto Legislativo N. 659)

Proyecto: PRIV-SV. Lente: reforma aprobada el 17 de septiembre de 2026.
Fecha de consulta de todas las fuentes: 2026-09-23.
Autor: investigador juridico (subagente). Este documento orienta el diseno funcional; no es asesoria legal.

---

## 1. Resumen ejecutivo

1. El Decreto Legislativo N. 659, "REFORMASE LA LEY PARA LA PROTECCION DE DATOS PERSONALES", fue emitido por la Asamblea Legislativa el 17 de septiembre de 2026. Esto esta confirmado en fuente primaria: el buscador oficial de leyes y decretos de la Asamblea (ficha /leyes-y-decretos/view/7022) registra numero 659, fecha de emision 17/09/2026 y el estado "Pendiente de Publicacion Material en el Diario Oficial y de Entrada en Vigencia". El Decreto 660 de la misma fecha es la ratificacion de un acuerdo con Estados Unidos sobre el Cuerpo de Paz; no debe confundirse.

2. Al 2026-09-23 el decreto NO esta publicado en el Diario Oficial y NO esta vigente. Verificado contra el archivo digital oficial del Diario Oficial (API de diariooficial.gob.sv): las unicas ediciones de septiembre 2026 disponibles son las del 1, 2, 3, 4 y 7 de septiembre; la Imprenta Nacional informa que el ultimo Diario Oficial a la venta es el del 07-09-2026. Ninguna edicion posterior a la aprobacion existe todavia en el archivo. Segun todas las fuentes secundarias, la reforma entrara en vigencia ocho dias despues de su publicacion.

3. El TEXTO OFICIAL del decreto no ha sido localizado. La Asamblea no adjunta PDF en la ficha del decreto; no hay dictamen de comision porque se aprobo con dispensa de tramites; la pieza de correspondencia (iniciativa del Ejecutivo) no aparece en las paginas publicas consultadas; no existe edicion del Diario Oficial que lo contenga. Todo lo que se afirma sobre el contenido articulo por articulo proviene de la nota oficial de la Asamblea (asamblea.gob.sv/node/14116) y de prensa (El Diario de Hoy, elsalvador.com, Infobae, La Noticia SV, hoy.com.sv). Debe tratarse como "segun fuentes secundarias" hasta obtener el texto.

4. Contenido segun esas fuentes: se derogan los Arts. 15 y 17 (delegado obligatorio y deber de asistencia al delegado); se reforma el Art. 16 (las funciones pasan a los "sujetos obligados", que deberan auxiliar a sus dependencias o proveedores y fijar lineamientos internos para gestionar solicitudes ARCO-POL); se reforma el Art. 47 (el sector publico mantiene expresamente el delegado, que puede ser el Oficial de Informacion); se reforma el Art. 51 (el Presidente de la Republica nombra al Director de Proteccion de Datos Personales por tres anos; conoce los procedimientos sancionadores y puede delegar la instruccion pero no la imposicion de la sancion). Las solicitudes ARCO-POL se presentan directamente ante la empresa u organizacion. Los plazos se mantienen: 20 dias habiles prorrogables por otros 20, prevencion unica de 10, devolucion por incompetencia en 5, notificacion a receptores en 5, denegatoria motivada en 3, revocacion de consentimiento en 5 y aviso al encargado en 5.

5. Consecuencia central para el producto: hasta que el decreto se publique y transcurran ocho dias, sigue vigente el regimen original del Decreto 144 (delegado obligatorio para todo sujeto obligado, Art. 15; solicitudes presentadas al delegado, Art. 18 inc. 2). Despues de la vigencia, en el sector privado el delegado deja de ser obligacion legal y la empresa asume directamente la recepcion, tramite y resolucion de las solicitudes ARCO-POL con los mismos plazos. El software debe operar en doble estado, gobernado por una fecha de vigencia configurable, con trazabilidad del regimen aplicado a cada expediente.

6. Efectos colaterales que deben modelarse como incertidumbre: (a) el Art. 24 lit. f de la LPDP sigue exigiendo en el aviso de privacidad "el nombre del delegado" y no consta que se haya reformado; (b) los Lineamientos para el Delegado de la ACE (D.O. N. 146, Tomo 452, 11 ago 2026, vigentes desde 19 ago 2026) se fundan expresamente en el Art. 15 y quedarian sin objeto para el sector privado, pero no han sido derogados formalmente; (c) las Politicas de Actuacion de la ACE (N. 001-0309025-DPDP) siguen listando el delegado como medida organizativa obligatoria; (d) la ACE dejo sin efecto el 12 de septiembre de 2026 la fecha limite del 16 de septiembre para comunicar el nombramiento del delegado, pero el comunicado no fue localizado en ace.gob.sv y solo consta por prensa; (e) el formulario oficial de nombramiento de delegado y el formulario de acceso de la ACE mencionan al delegado y quedarian desactualizados.

---

## 2. Metodologia: que se busco y que se encontro

| Fuente | Que se busco | Resultado (2026-09-23) |
|---|---|---|
| asamblea.gob.sv, buscador de leyes y decretos (POST a /leyes-y-decretos/resultado-busqueda/) | Decreto N. 659 y 660, emision sep 2026 | 659 = "REFORMASE LA LEY PARA LA PROTECCION DE DATOS PERSONALES", emision 17/09/2026, ficha view/7022, sin PDF, estado "Pendiente de Publicacion Material en el Diario Oficial y de Entrada en Vigencia". 660 = ratificacion acuerdo Cuerpo de Paz EE.UU. |
| asamblea.gob.sv/node/14116 | Nota oficial de la reforma | Texto integro obtenido (ver seccion 4.1) |
| asamblea.gob.sv, "Ultimos decretos aprobados", "Decretos por anos 2026", agenda, correspondencia, votaciones, resumen plenaria | PDF del decreto, dictamen o iniciativa | Paginas dinamicas; solo exponen la agenda y correspondencia de la sesion 127 del 23 sep 2026, que no contienen la reforma. No hay dictamen porque fue aprobada con dispensa de tramites. |
| PDFs de asamblea.gob.sv encontrados por buscador (dictamenes/498798FA..., correspondencia/2A326CE8..., correspondencia/EFBA7BEE...) | Posible texto de la reforma | Descargados y revisados: son documentos historicos (iniciativa ARENA 2019, Dictamen 46 Comision de Economia 2021, veto presidencial al Decreto 875 de 2021). No son la reforma. |
| diariooficial.gob.sv (API /api/v1/diarios-disponibles, year=2026, month=9) | Edicion que contenga el decreto | Solo ediciones 01, 02, 03, 04 y 07 de septiembre de 2026. Agosto 2026 completo (incluye 11-08-2026, coherente con la publicacion de los lineamientos ACE). |
| imprentanacional.gob.sv | Ultimo D.O. a la venta | 07-09-2026 |
| ace.gob.sv (inicio, noticias, politicas, formularios) | Comunicado sobre el registro de delegados y la reforma | No localizado. La seccion de noticias solo muestra dos webinars sobre el delegado (09/09/2026). La pagina de politicas lista NDPDDP.pdf (lineamientos) y PASDPDP.pdf (normativa sancionadora) sin fechas. |
| Prensa y firmas legales | Contenido de la reforma y comunicado ACE | El Diario de Hoy (17 y 18 sep), elsalvador.com (12 y 17 sep), Infobae (17 sep), La Noticia SV, hoy.com.sv (23 sep), ContraPunto (13 sep), EY (26 ago), Consortium (2 sep), BLP (bloqueado 403), La Prensa Grafica (solo via PressReader, de pago). |
| Corpus local | Texto vigente de los articulos afectados, lineamientos, normativa sancionadora, politicas, formularios | Consultado integramente (rutas en seccion 9). |

Archivo `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\decreto_659.pdf`: NO creado, porque no existe texto oficial descargable. El archivo `dictamen_reforma_lpdp.txt` del corpus esta vacio por la misma razon.

---

## 3. Estado del Decreto 659 al 2026-09-23

| Hito | Dato | Fuente | Confianza |
|---|---|---|---|
| Ingreso de la iniciativa | 16 sep 2026, iniciativa del Presidente de la Republica por medio del Ministro de Justicia y Seguridad Publica, Hector Gustavo Villatoro; presentada por la bancada Nuevas Ideas con dispensa de tramites | El Diario de Hoy 17 sep 2026; Infobae 17 sep 2026 | Media (secundaria) |
| Aprobacion | 17 sep 2026, 57 votos a favor (Infobae agrega 1 en contra), dispensa de tramites | asamblea.gob.sv/node/14116 (57 votos); Infobae | Alta para 57 votos; media para el voto en contra |
| Numero y titulo | Decreto N. 659, "REFORMASE LA LEY PARA LA PROTECCION DE DATOS PERSONALES" | asamblea.gob.sv/leyes-y-decretos/view/7022 | Alta |
| Fecha de emision | 17/09/2026 | Misma ficha | Alta |
| Sancion presidencial | Sin informacion publica | - | - |
| Publicacion en Diario Oficial | NO publicada al 2026-09-23 (archivo digital termina en la edicion del 07-09-2026) | diariooficial.gob.sv API; imprentanacional.gob.sv | Alta |
| Vigencia | NO vigente. Clausula de vigencia segun prensa: 8 dias despues de su publicacion en el D.O. | El Diario de Hoy; Infobae; La Noticia SV | Media (secundaria) |
| Estado registrado por la Asamblea | "Pendiente de Publicacion Material en el Diario Oficial y de Entrada en Vigencia" | asamblea.gob.sv/leyes-y-decretos/view/7022 | Alta |

Clasificacion de vigencia para todo el sweep: APROBADA-PENDIENTE-PUBLICACION.

**Re-verificacion posterior (2026-09-24):** siguiendo la recomendacion de monitoreo diario de la seccion 8 punto 2, se repitio la consulta un dia despues. Sin cambios: la ficha https://www.asamblea.gob.sv/leyes-y-decretos/view/7022 sigue mostrando "Pendiente de Publicacion Material en el Diario Oficial y de Entrada en Vigencia"; la API de diariooficial.gob.sv (year=2026, month=9) sigue devolviendo solo las ediciones del 01, 02, 03, 04 y 07 de septiembre de 2026; imprentanacional.gob.sv sigue anunciando el 07-09-2026 como ultimo Diario Oficial a la venta. El decreto continua NO publicado y NO vigente.

### 3.1 Ventana temporal estimada (orientativa, requiere abogado)

La Constitucion regula el tramite posterior a la aprobacion: traslado del proyecto al Presidente (Art. 135 Cn), veto u observaciones dentro de ocho dias habiles (Art. 137 Cn; el veto de 2021 al Decreto 875 cita expresamente "articulo 137, inciso primero" como fundamento del veto) y publicacion (Art. 139 Cn). No se ha verificado en esta pasada el texto exacto de esos articulos constitucionales; se citan como orientacion de calendario, no como afirmacion juridica cerrada. Consecuencia practica: la publicacion puede ocurrir en cualquier momento a partir de finales de septiembre de 2026 y la vigencia ocho dias despues. El software no debe asumir ninguna fecha; debe esperar la publicacion (numero, tomo y fecha del D.O.) y calcular la vigencia a partir de ella.

---

## 4. Contenido de la reforma

### 4.1 Nota oficial de la Asamblea (transcripcion integra, fuente primaria)

Fuente: https://www.asamblea.gob.sv/node/14116, consultada 2026-09-23. Titulo: "Reformas a la Ley de Proteccion de Datos Personales agilizaran la gestion de solicitudes". Fecha: jueves 17 de septiembre de 2026. Tag: Comision de Tecnologia.

"Los cambios facilitaran a las personas ejercer sus derechos sobre sus datos personales y permitiran que las instituciones, empresas y organizaciones gestionen estas solicitudes de acuerdo con su organizacion interna.

La Asamblea Legislativa reformo, con 57 votos, la Ley para la Proteccion de Datos Personales que modifica la forma en que las personas pueden solicitar el acceso, correccion, eliminacion u otras acciones relacionadas con sus datos personales.

La normativa vigente establece que el encargado de velar por los derechos ARCO-POL (Acceso, Rectificacion, Cancelacion, Oposicion, Portabilidad, Olvido y Limitacion) es el delegado de proteccion de datos, pero con las reformas las personas podran presentar directamente ante la institucion, empresa u organizacion que tiene o utiliza sus datos personales las solicitudes para consultar, corregir, eliminar o ejercer otros derechos sobre su informacion.

La diputada de Nuevas Ideas, Dania Gonzalez, explico que las modificaciones haran mas eficiente la aplicacion de la Ley para la Proteccion de Datos Personales, sin alterar los derechos y garantias que esta reconoce.

En el caso de las instituciones publicas, se mantendra expresamente la obligacion de tener un delegado de proteccion de datos, cargo que podra ser desempenado por el mismo Oficial de Informacion de la institucion.

Gonzalez tambien afirmo que la Agencia de Ciberseguridad del Estado (ACE) mantendra la rectoria y las funciones de supervision, control e inspeccion establecidas en la normativa. Ademas, se creara el cargo de Director de Proteccion de Datos Personales, quien se encargara de asistir al director general de la ACE y conocera los procedimientos administrativos sancionadores.

'En sintesis, nosotros mantenemos los derechos, mantenemos todas las garantias, mantenemos la rectoria y lo que estamos modernizando es el mecanismo de cumplimiento. Por que? porque la reforma significa menos rigidez administrativa, mayor eficiencia institucional y la misma proteccion de datos personales para todos los salvadorenos.', apunto Gonzalez.

Tambien se regula la correccion de informacion. Las enmiendas a la ley tambien contemplan que cuando una persona solicite corregir sus datos se debera dejar constancia de que esa informacion esta en proceso de rectificacion. Si esos datos ya fueron compartidos con otras personas o entidades el sujeto obligado debera informarles sobre la correccion, actualizacion o eliminacion dentro de los cinco dias habiles posteriores a determinar que la solicitud procede.

Tambien, establecen un plazo de cinco dias habiles para atender las solicitudes mediante las cuales una persona retire su consentimiento para el tratamiento de sus datos."

Observacion: la nota dice que "se creara" el cargo de Director de Proteccion de Datos Personales, pero el Art. 51 inc. 2 del Decreto 144 ya preveia ese cargo desde 2024 ("sera nombrado un Director de Proteccion de Datos Personales"). La novedad, segun prensa, es quien lo nombra y por cuanto tiempo.

### 4.2 Tabla articulo por articulo (texto vigente verificado vs. cambio segun fuentes secundarias)

| Art. LPDP | Accion segun fuentes secundarias | Texto vigente (Decreto 144, corpus local) | Texto nuevo o descripcion del cambio | Fuente del cambio |
|---|---|---|---|---|
| 15 | DEROGADO | "Los sujetos obligados por la presente ley deberan de nombrar un delegado de proteccion de datos personales, en adelante delegado, quien se encargara de gestionar y tramitar las solicitudes para el ejercicio de los derechos ARCO-POL." | Desaparece la obligacion legal de nombrar delegado para todo sujeto obligado. Para el sector publico la obligacion se conserva via Art. 47 reformado. | El Diario de Hoy 17 sep; Infobae 17 sep; La Noticia SV; opinion EDH 18 sep |
| 16 | REFORMADO | "El delegado tendra las siguientes atribuciones: a) Recibir, tramitar y resolver las solicitudes ARCO-POL. b) Auxiliar y orientar al responsable... c) Establecer mecanismos para asegurar que los datos solo se entreguen a su titular o representante acreditado. d) Proponer procedimientos internos... e) Asesorar a las areas... f) Realizar actividades de formacion... g) Publicar el aviso de privacidad en el sitio web del responsable o en lugares visibles..." | Texto nuevo no disponible. Descripcion: las funciones pasan a los "sujetos obligados", que "deberan auxiliar a sus dependencias o proveedores y fijar lineamientos internos para gestionar las solicitudes ARCO-POL". | El Diario de Hoy 17 sep (unica fuente con ese detalle) |
| 17 | DEROGADO | "Sera obligacion de cada dependencia, empleado o proveedor del responsable del tratamiento de datos de asistir y atender a las peticiones canalizadas por el delegado en el ejercicio de sus funciones." | Desaparece el deber de asistencia al delegado (sin delegado no tiene objeto). | El Diario de Hoy; Infobae; La Noticia SV |
| 47 | REFORMADO | "Para el ejercicio de los derechos contemplados en el articulo anterior, se debera cumplir con lo dispuesto en la Seccion B, Capitulo III del Titulo I de la presente ley. Para tales efectos, el nombramiento del delegado podra recaer en el Oficial de Informacion de la institucion pertinente." | Texto nuevo no disponible. Descripcion: las instituciones publicas "mantendran la obligacion de nombrar un delegado de proteccion de datos personales, funcion que podra recaer en el mismo oficial de informacion de cada entidad". Se entiende que la obligacion, que antes derivaba del Art. 15 general, se reubica expresamente en el Art. 47. | asamblea.gob.sv/node/14116; El Diario de Hoy; opinion EDH |
| 51 | REFORMADO | Inc. 1: el Director General de la ACE ejerce las atribuciones salvo la potestad sancionadora. Inc. 2: "Para asistir al Director General en el ejercicio de sus funciones, sera nombrado un Director de Proteccion de Datos Personales. Este funcionario tambien conocera de los procedimientos administrativos para imponer las sanciones que establece la presente ley, y podra delegar la instruccion y sustanciacion de estos procedimientos, no asi la imposicion de la sancion, en un empleado o funcionario de la ACE distinto del Director General." Inc. 3: la Agencia establecera las dependencias necesarias. | Texto nuevo no disponible. Descripcion: "facultan al presidente de la Republica para nombrar por un periodo de tres anos al director de Proteccion de Datos Personales, funcionario enmarcado en la ACE que asistira al director general de dicha entidad. Este director estara a cargo de los procedimientos administrativos sancionatorios y podra delegar la instruccion de los expedientes en personal de la ACE, reservandose la facultad de imponer las sanciones." | El Diario de Hoy; Infobae; hoy.com.sv |
| 18, 19, 20, 21, 22, 30 | INCIERTO | Todos mencionan al "delegado" como quien recibe (18 inc. 2), previene (18 inc. 3), devuelve por incompetencia (19), responde (20), deja constancia y notifica a receptores (21), deniega (22) y atiende la revocacion (30). | Las fuentes secundarias describen los plazos con el sujeto "sujeto obligado" o "entidad" y la nota oficial habla de "enmiendas" sobre la constancia de rectificacion (Art. 21) y la revocacion (Art. 30). Es plausible que estos articulos hayan sido ajustados para sustituir "delegado" por "sujeto obligado" o "responsable", manteniendo los plazos, pero NINGUNA fuente lo afirma expresamente y El Diario de Hoy solo lista como reformados los Arts. 16, 47 y 51. | Inferencia; ver seccion 8 |
| 24 lit. f | NO MENCIONADO | "Indicacion del nombre del delegado y lugar o medios para presentar la solicitud de derechos ARCO-POL." | Ninguna fuente menciona reforma del Art. 24. Queda un literal que exige el nombre de una figura que ya no es obligatoria en el sector privado. | Ver seccion 5.4 |
| 48 | NO MENCIONADO | Sector publico: informar "la informacion de contacto del delegado y los medios para ejercer sus derechos". | Coherente con el Art. 47 reformado (el sector publico mantiene delegado). | - |
| 52 | NO MENCIONADO | Requisitos del Director de Proteccion de Datos Personales. | Sin informacion de cambio. | - |
| 53 | NO MENCIONADO | Procedimiento sancionador remite a la Ley de Ciberseguridad y Seguridad de la Informacion. | Sin informacion de cambio. | - |
| 56 | NO MENCIONADO | Infracciones. Ninguna infraccion tipifica "no nombrar delegado"; las relevantes son b.2 (no atender ARCO-POL en tiempo y forma, grave) y c.2 (denegar en contravencion a la ley, muy grave). | Sin informacion de cambio. | - |

### 4.3 Plazos ARCO-POL: comparativa

| Tramite | Texto vigente (Decreto 144) | Segun reforma (fuentes secundarias) | Cambia? |
|---|---|---|---|
| Prevencion por requisitos incompletos | Una sola vez, 10 dias habiles desde el dia siguiente a la notificacion (Art. 18 inc. 3) | 10 dias habiles, una unica vez | No |
| Devolucion por incompetencia | 5 dias habiles posteriores a la recepcion (Art. 19) | 5 dias habiles | No |
| Respuesta | 20 dias habiles, prorrogables por causas justificadas hasta otros 20 (Art. 20) | 20 + 20 dias habiles | No |
| Constancia de datos en rectificacion | Obligacion sin plazo (Art. 21 inc. 2) | Se mantiene ("se debera dejar constancia") | No |
| Notificacion a receptores de rectificacion, actualizacion o eliminacion | 5 dias habiles desde la determinacion de procedencia (Art. 21 inc. 3) | 5 dias habiles | No |
| Denegatoria motivada | 3 dias habiles desde la adopcion de la decision (Art. 22 inc. final) | 3 dias habiles | No |
| Revocacion del consentimiento | 5 dias habiles para proceder; 5 dias habiles para informar al encargado (Art. 30) | 5 dias habiles; 5 al encargado | No |
| Quien recibe y resuelve | El delegado (Arts. 16 lit. a y 18 inc. 2) | El sujeto obligado (institucion, empresa u organizacion) directamente, "de acuerdo con su organizacion interna" | SI |

Conclusion para el motor de plazos del software: ningun plazo cambia; cambia el actor. El calculo de vencimientos puede ser identico en ambos regimenes.

---

## 5. Impacto por tema, con bloques de obligacion

Convencion de vigencia usada en los bloques: "VIGENTE" = regimen actual del Decreto 144; "APROBADA-PENDIENTE-PUBLICACION" = regla que solo aplicara cuando el Decreto 659 entre en vigencia.

### 5.1 Figura del delegado en el sector privado

**Norma:** Ley para la Proteccion de Datos Personales (Decreto Legislativo 144)
**Articulo:** Art. 15
**Obligacion:** Nombrar un delegado de proteccion de datos personales encargado de gestionar y tramitar las solicitudes ARCO-POL.
**A quien aplica:** Todos los sujetos obligados (Art. 2), publicos y privados.
**Implicacion para el software:** Mientras la reforma no este vigente, el modulo "Delegado" debe seguir tratando el nombramiento como obligacion pendiente, con acta de nombramiento (Lineamientos ACE Arts. 6 y 7), notificacion al delegado en 3 dias habiles (Art. 8), declaracion jurada de conflicto de intereses (Art. 9) y comunicacion a la ACE en 15 dias habiles (Art. 10), esta ultima con la advertencia de que la ACE dejo sin efecto la fecha limite transitoria.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (lineas 565-569), consultado 2026-09-23.
**Vigencia:** VIGENTE (sera DEROGADA cuando el Decreto 659 entre en vigencia).
**Clasificacion:** OBLIGATORIO (hasta la vigencia de la reforma).

**Norma:** Decreto Legislativo 659 (reforma a la LPDP)
**Articulo:** Derogatoria de los Arts. 15 y 17 LPDP; reforma del Art. 16 LPDP
**Obligacion:** Deja de existir la obligacion legal de nombrar delegado en el sector privado. Las funciones del Art. 16 (recibir, tramitar y resolver ARCO-POL; auxiliar a dependencias o proveedores; fijar lineamientos internos) recaen en el sujeto obligado.
**A quien aplica:** Sujetos obligados del sector privado (personas naturales y juridicas). El sector publico conserva el delegado (Art. 47 reformado).
**Implicacion para el software:** Tras la vigencia, el nombramiento de delegado en clientes privados pasa a ser opcional. El sistema debe exigir en su lugar la designacion de al menos un rol interno "responsable de atencion de derechos ARCO-POL" (nombre funcional a definir por producto; no es una figura legal) y la documentacion de lineamientos internos de gestion de solicitudes (Art. 16 reformado, segun prensa; Art. 33 inc. 1 vigente, que ya obliga a establecer y documentar procedimientos ARCO-POL).
**Fuente oficial:** https://www.asamblea.gob.sv/leyes-y-decretos/view/7022 (existencia y estado del decreto) y https://www.asamblea.gob.sv/node/14116 (contenido general); detalle de articulos segun fuente secundaria: https://www.eldiariodehoy.com/noticias/nacionales/asamblea-legislativa-deroga-obligatoriedad-de-las-empresas-privadas-de-nombrar-delegados-de-proteccion-de-datos-personales/93615/2026/ . Consultadas 2026-09-23.
**Vigencia:** APROBADA-PENDIENTE-PUBLICACION.
**Clasificacion:** CONDICIONAL (aplica solo desde la vigencia de la reforma; el delegado voluntario sigue siendo posible).

**Norma:** Politicas de Actuacion y Manejo de Datos Personales N. 001-0309025-DPDP (ACE)
**Articulo:** Art. 4 (Medidas organizativas, lit. b), Art. 6 lit. a y Art. 8 lit. a
**Obligacion:** Lista al "Delegado de Proteccion de Datos Personales (DPDP): nombramiento de un responsable encargado de garantizar el cumplimiento de la normativa" como medida organizativa de cumplimiento obligatorio y le asigna "la supervision interna (Art. 15 y 16 LPDP)".
**A quien aplica:** Entidades publicas y privadas (Art. 2 de las Politicas).
**Implicacion para el software:** Tras la vigencia de la reforma existe un conflicto entre una politica administrativa (rango inferior) que exige delegado y una ley que ya no lo exige en el privado. Prudencialmente, el software debe mostrar la designacion de una persona responsable de la supervision interna como RECOMENDADO fuerte (con referencia a la politica ACE y a la infraccion grave del Art. 56 lit. b.7 por no cumplir medidas de seguridad de las politicas), sin afirmar que sea obligatorio nombrar "delegado" en sentido legal. Marcar el punto para revision de abogado y para seguimiento de una eventual actualizacion de las politicas por la ACE.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_politicas_protecciondatos.txt; https://ace.gob.sv/page/politicas . Consultadas 2026-09-23.
**Vigencia:** VIGENTE (no consta modificacion).
**Clasificacion:** RECOMENDADO tras la reforma; hasta la reforma, coincide con la obligacion legal del Art. 15.

### 5.2 Figura del delegado en el sector publico

**Norma:** LPDP reformada por Decreto 659
**Articulo:** Art. 47 (reformado) y Art. 48 (vigente)
**Obligacion:** Las instituciones publicas mantienen expresamente la obligacion de nombrar delegado de proteccion de datos personales; el cargo puede recaer en el Oficial de Informacion. Deben informar la informacion de contacto del delegado y los medios para ejercer derechos (Art. 48).
**A quien aplica:** Sujetos del inciso segundo del Art. 2 LPDP (sector publico).
**Implicacion para el software:** El producto se dirige al sector privado, pero el modelo de datos debe distinguir "tipo de sujeto obligado" (privado / publico) porque el regimen del delegado diverge tras la reforma. Si se atienden entidades publicas, el modulo de delegado completo (lineamientos ACE, registro, certificacion) permanece aplicable.
**Fuente oficial:** https://www.asamblea.gob.sv/node/14116 (fuente primaria de la descripcion); texto vigente en ace_decreto_144.txt lineas 1155-1164. Consultadas 2026-09-23.
**Vigencia:** Art. 47 vigente en su texto actual; version reformada APROBADA-PENDIENTE-PUBLICACION.
**Clasificacion:** OBLIGATORIO (solo sector publico).

### 5.3 Quien recibe y resuelve las solicitudes ARCO-POL, y plazos

**Norma:** LPDP (Decreto 144)
**Articulo:** Arts. 16 lit. a, 18 inc. 2, 19, 20, 21, 22 y 30
**Obligacion:** Regimen vigente: la solicitud "debera realizarse al delegado" (Art. 18 inc. 2); el delegado previene (10 dias habiles, una vez), devuelve por incompetencia (5), responde (20 + 20), deja constancia de rectificacion en curso, notifica a receptores (5), deniega con resolucion motivada (3) y atiende la revocacion (5, mas 5 para informar al encargado).
**A quien aplica:** Responsables (a traves del delegado) de cualquier sector.
**Implicacion para el software:** En el regimen vigente, el flujo ARCO-POL debe asignar el expediente al delegado registrado como responsable de resolucion, y las plantillas de resolucion deben firmarse por el delegado (Lineamientos ACE Art. 33: admision, prevencion, subsanacion, reconocimiento, incompetencia, denegatoria o resolucion final, notificadas en 3 dias habiles).
**Fuente oficial:** ace_decreto_144.txt (lineas 609-725 y 925-930); lineamientos_dpo_OCR.txt (Arts. 32 a 35). Consultados 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

**Norma:** LPDP reformada por Decreto 659
**Articulo:** Art. 16 reformado y, segun descripcion de prensa, los articulos de la Seccion B leidos con el sujeto "sujeto obligado"
**Obligacion:** Las personas presentan las solicitudes directamente ante la institucion, empresa u organizacion; el sujeto obligado las gestiona "de acuerdo con su organizacion interna" y responde en los mismos plazos: 20 dias habiles ampliables por otros 20, prevencion unica de 10, devolucion en 5, notificacion a receptores en 5, denegatoria motivada en 3, revocacion en 5 y aviso al encargado en 5.
**A quien aplica:** Todos los sujetos obligados; en el sector publico, a traves del delegado.
**Implicacion para el software:** Tras la vigencia, el flujo ARCO-POL debe permitir asignar cada expediente a cualquier rol interno configurado por la empresa (no exclusivamente al delegado); las plantillas deben firmarse por "el responsable" o por la persona designada; los canales de recepcion (sitio web, correo, oficinas) se publican a nombre de la empresa. El motor de plazos no cambia. Debe conservarse la posibilidad de que la empresa mantenga un delegado voluntario como asignatario por defecto.
**Fuente oficial:** https://www.asamblea.gob.sv/node/14116 (primaria, plazos de 5 dias); detalle completo de plazos segun fuentes secundarias: El Diario de Hoy 17 sep 2026 e Infobae 17 sep 2026. Consultadas 2026-09-23.
**Vigencia:** APROBADA-PENDIENTE-PUBLICACION.
**Clasificacion:** OBLIGATORIO (desde la vigencia de la reforma).

**Norma:** LPDP (Decreto 144)
**Articulo:** Art. 33 inc. 1
**Obligacion:** El responsable establecera y documentara procedimientos para el ejercicio de los derechos ARCO-POL con base en las politicas de actuacion de la ACE.
**A quien aplica:** Responsables del tratamiento.
**Implicacion para el software:** Es la base legal, vigente en ambos regimenes, para exigir al cliente un procedimiento ARCO-POL documentado. Tras la reforma, ese procedimiento absorbe lo que antes hacia el delegado (recepcion, verificacion de identidad, tramite, resolucion, notificacion, registro). El Art. 16 reformado, segun prensa, refuerza esto con "lineamientos internos".
**Fuente oficial:** ace_decreto_144.txt (lineas 955-963). Consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

### 5.4 Aviso de privacidad (Art. 24 lit. f)

**Norma:** LPDP (Decreto 144)
**Articulo:** Art. 24 lit. f
**Obligacion:** El aviso de privacidad debe contener "indicacion del nombre del delegado y lugar o medios para presentar la solicitud de derechos ARCO-POL".
**A quien aplica:** Responsables del tratamiento.
**Implicacion para el software:** Regimen vigente: el generador del aviso debe tomar el nombre del delegado nombrado y los canales de solicitud; si no hay delegado nombrado, el aviso queda marcado como incompleto. Regimen tras la reforma: ninguna fuente indica que el Art. 24 se haya reformado, de modo que el literal f seguiria exigiendo textualmente "el nombre del delegado" aunque el delegado ya no sea obligatorio en el privado. Interpretacion prudente para el software: (i) si el cliente nombro delegado voluntario, incluir su nombre; (ii) si no, incluir de forma destacada el nombre o denominacion de la persona, area o punto de contacto responsable de atender los derechos ARCO-POL y los lugares o medios de presentacion, y registrar en el expediente del aviso una nota de "literal f aplicado por analogia por derogacion del Art. 15", con recomendacion de validacion por abogado. La segunda parte del literal (lugar o medios para presentar la solicitud) es plenamente exigible en ambos regimenes. Ademas, el Art. 16 lit. g (publicar el aviso) deja de ser funcion del delegado y pasa al sujeto obligado; el Lineamiento ACE Art. 31 (delegado publica y documenta el aviso; conservacion minima de 10 anos) pierde su sujeto en el privado, pero la conservacion documental de 10 anos es una buena practica que el software puede mantener como RECOMENDADO.
**Fuente oficial:** ace_decreto_144.txt (lineas 745-790); lineamientos_dpo_OCR.txt (Art. 31, pagina 9 del OCR). Consultados 2026-09-23.
**Vigencia:** VIGENTE (no consta reforma).
**Clasificacion:** OBLIGATORIO en cuanto a medios y lugar de presentacion; CONDICIONAL en cuanto al nombre del delegado (aplica si existe delegado; si no, incertidumbre juridica documentada).

### 5.5 Lineamientos para el Delegado de Proteccion de Datos Personales (ACE)

Datos verificados en el OCR local y su imagen (page-01.png y page-11.png): publicados en el Diario Oficial N. 146, Tomo 452, martes 11 de agosto de 2026, paginas 12 a 21; dados en la ACE el 24 de julio de 2026 por el Director General Eduardo Alexis Rodriguez Rodriguez; Art. 42: vigencia ocho dias despues contados a partir del dia siguiente de su publicacion (por lo tanto vigentes desde el 19 u 20 de agosto de 2026 segun como se compute; el contexto del proyecto y la prensa usan 19 de agosto). Considerando II: "de acuerdo con el articulo 15 de la citada Ley, los sujetos obligados nombraran un Delegado...". Considerando III y Art. 2: desarrollan "el perfil, nombramiento, certificacion y facultades del Delegado".

**Norma:** Lineamientos para el Delegado de Proteccion de Datos Personales (ACE)
**Articulo:** Considerandos II y III; Arts. 2, 5, 6, 7, 8, 9, 10, 12, 13 a 17, 18, 19, 20 a 22, 23 a 29, 30, 31, 32 a 38, 40 y 42
**Obligacion:** Perfil minimo (grado universitario, mayor de 21 anos, experiencia, sin condenas ni sanciones, certificacion ACE cuando el programa entre en vigencia); nombramiento formal por la maxima autoridad con contenido minimo; notificacion al delegado en 3 dias habiles; declaracion jurada de conflicto de intereses; comunicacion a la ACE en 15 dias habiles y actualizacion de cambios en 10 dias habiles; credencial de la ACE en 15 dias habiles; sustitucion en 10 dias habiles ante cesacion; verificacion de idoneidad al menos cada 3 anos; capacitacion anual; independencia, prohibiciones y conflictos de interes; informe al responsable al menos dos veces al ano; publicacion del aviso; formularios ACE como estandar minimo; resolucion y notificacion de actuaciones en 3 dias habiles; recurso del titular ante la ACE en 10 dias habiles; confidencialidad 5 anos tras el cese; publicacion de costos; transitorio de 20 dias habiles para comunicar nombramientos mientras no exista la plataforma.
**A quien aplica:** Responsables y encargados, publicos y privados (Art. 3), en cuanto nombren delegado.
**Implicacion para el software:** Regimen vigente: los lineamientos son la especificacion mas detallada del modulo Delegado y deben implementarse como tareas, plazos y evidencias (con la fecha limite transitoria suspendida por la ACE). Tras la vigencia de la reforma: los lineamientos no han sido derogados formalmente, pero su fundamento (Art. 15) desaparece para el privado; quedarian sin objeto para las empresas que no nombren delegado y de aplicacion dudosa para las que lo nombren voluntariamente (no esta claro si la ACE exigira registro y certificacion a delegados voluntarios). El software debe: (a) marcar todo el modulo como CONDICIONAL a "existe delegado nombrado"; (b) no generar alertas de incumplimiento por ausencia de delegado en clientes privados tras la vigencia; (c) conservar los expedientes de nombramiento ya realizados; (d) seguir aplicando las reglas de los lineamientos a clientes del sector publico; (e) prever un interruptor para "lineamientos derogados o reformados por la ACE" con fecha.
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\lineamientos_dpo_OCR.txt e imagenes en ...\fuentes\ocr\lineamientos_dpo\page-NN.png; https://ace.gob.sv/documentos/politicas/NDPDDP.pdf ; D.O. N. 146, Tomo 452, 11 ago 2026. Consultados 2026-09-23.
**Vigencia:** VIGENTE (sin derogatoria formal conocida; quedarian materialmente sin objeto en el privado tras la reforma).
**Clasificacion:** OBLIGATORIO hoy para quien deba o decida nombrar delegado; CONDICIONAL tras la reforma.

### 5.6 Registro de delegados ante la ACE y fecha limite dejada sin efecto

**Norma:** Lineamientos para el Delegado (ACE)
**Articulo:** Art. 10 (comunicacion a la ACE en 15 dias habiles desde el nombramiento; actualizacion en 10 dias habiles), Art. 11 (Registro Publico de Delegados), Art. 12 (credencial en 15 dias habiles), Art. 40 (transitorio: mientras no exista la plataforma, comunicacion por oficio, escrito o correo institucional "dentro de los veinte dias habiles de la entrada en vigencia de estos lineamientos")
**Obligacion:** Comunicar y mantener actualizado el nombramiento del delegado ante la Direccion de Proteccion de Datos Personales de la ACE. El transitorio fijaba un plazo de 20 dias habiles desde la vigencia, que las fuentes secundarias situan con vencimiento el 16 de septiembre de 2026.
**A quien aplica:** Responsables que nombren delegado.
**Implicacion para el software:** Segun elsalvador.com (12 sep 2026) y El Diario de Hoy (12 sep 2026), la ACE comunico en su sitio web: "Queda sin efecto la fecha limite establecida para el nombramiento del delegado de proteccion de datos personales" y que "no sera necesario realizar ninguna accion al respecto" por el momento. El comunicado NO fue localizado en ace.gob.sv al 2026-09-23 (la seccion de noticias solo muestra los webinars del 9 de septiembre). El software no debe mostrar el 16 de septiembre de 2026 como fecha limite ni generar alertas de vencimiento; debe registrar como evidencia cualquier comunicacion ya enviada a la ACE; y debe mantener configurable una futura fecha o mecanismo de registro que la ACE anuncie. El plazo ordinario de 15 dias habiles del Art. 10 sigue formalmente en el texto para nombramientos nuevos; dado el comunicado de la ACE y la reforma en curso, mostrarlo como "plazo previsto en lineamientos, aplicacion suspendida segun comunicado ACE del 12 sep 2026 (fuente secundaria)".
**Fuente oficial:** lineamientos_dpo_OCR.txt (Arts. 10, 11, 12 y 40); comunicado ACE segun fuentes secundarias: https://www.elsalvador.com/dinero-y-negocios/entorno-economico/empresas-ley-de-proteccion-datos-el-salvador/1292968/2026/ y https://www.eldiariodehoy.com/noticias/nacionales/sin-fecha-para-nombrar-delegados-de-proteccion-de-datos-personales/93083/2026/ . Consultadas 2026-09-23.
**Vigencia:** VIGENTE en el texto; fecha limite transitoria SIN EFECTO segun la ACE (fuente secundaria).
**Clasificacion:** CONDICIONAL (aplica si hay delegado nombrado y cuando la ACE reactive el mecanismo).

Nota sobre el formulario oficial de nombramiento: el "Formulario de Nombramiento de Delegado de Proteccion de Datos Personales" de la ACE (version 07-07-2025) invoca "los articulos 15 y 16 de la Ley" y reproduce las atribuciones del Art. 16. Tras la reforma queda desactualizado en el sector privado. Igualmente, el formulario de acceso de la ACE incluye la opcion "Acudir con el delegado de Proteccion de Datos Personales" como modalidad de entrega; el software debe permitir sustituir esa opcion por "acudir a la oficina o punto de atencion del responsable" cuando no exista delegado, sin dejar de aceptar el formulario oficial (Lineamientos Art. 32).

### 5.7 Director de Proteccion de Datos Personales (Art. 51)

**Norma:** LPDP (Decreto 144) y Decreto 659
**Articulo:** Art. 51 (reformado), Art. 52 (requisitos, sin informacion de cambio)
**Obligacion:** No impone obligaciones a los sujetos obligados. Define la autoridad: hoy, "sera nombrado" un Director de Proteccion de Datos Personales que conoce de los procedimientos sancionadores y puede delegar instruccion pero no la sancion; tras la reforma, segun prensa, lo nombra el Presidente de la Republica por tres anos, con las mismas funciones sancionadoras.
**A quien aplica:** ACE.
**Implicacion para el software:** Impacto operativo minimo: el "Director de Proteccion de Datos Personales" es la autoridad que emite la resolucion de inicio, impone sanciones, extiende mandamientos de pago y ante quien el titular puede quejarse de una resolucion ARCO-POL (Lineamientos Art. 33 inc. 4, 10 dias habiles). El modulo de "autoridad" debe nombrarlo correctamente y permitir actualizar el titular del cargo y su fecha de nombramiento como dato de referencia.
**Fuente oficial:** ace_decreto_144.txt (lineas 1305-1340); descripcion del cambio: El Diario de Hoy 17 sep 2026 e Infobae 17 sep 2026. Consultados 2026-09-23.
**Vigencia:** Texto actual VIGENTE; reforma APROBADA-PENDIENTE-PUBLICACION.
**Clasificacion:** HECHO (no es obligacion del cliente).

### 5.8 Procedimiento sancionador

**Norma:** LPDP Art. 53 y Normativa para el Desarrollo del Procedimiento Administrativo Sancionador en el Ambito de la LPDP (ACE), D.O. N. 146, Tomo 452, 11 ago 2026, paginas 22 a 29, vigente ocho dias despues de su publicacion (Art. 49)
**Articulo:** Normativa ACE Arts. 4, 6, 8, 12, 13, 14, 19, 21, 23, 29, 30, 32, 33, 34, 35, 43, 44, 45, 46 y 47
**Obligacion:** El procedimiento se tramita por la via simplificada del Art. 158 LPA y excepcionalmente por la ordinaria (Art. 4); etapas: resolucion de inicio, contestacion, prueba y resolucion final, mas alegatos finales en la via ordinaria (Art. 6); diligencias preliminares de investigacion de oficio, por denuncia, a solicitud del sujeto obligado tras un incidente o de forma preventiva basada en riesgos, con plazo maximo de 90 dias habiles prorrogables (Arts. 8 y 12); autoridad competente: el Director de Proteccion de Datos Personales, que puede delegar la instruccion en el Director Juridico u otro funcionario distinto del Director General (Arts. 13 y 14); emplazamiento y contestacion en 5 dias habiles (Arts. 19 y 21); allanamiento con resolucion final en 15 dias habiles (Art. 23); alegatos finales 10 dias habiles en via ordinaria (Art. 29); remision del expediente en 8 dias habiles (Art. 30); resolucion final en 15 dias habiles desde la recepcion del expediente (Art. 32); sin recurso en via simplificada (queda la via contencioso administrativa) y con reconsideracion, apelacion y revision en via ordinaria (Arts. 32 y 33); aviso a la FGR en 72 horas si hay ilicito penal (Art. 34); medidas provisionales incluso antes del inicio, confirmadas en 15 dias calendario (Art. 35); parametros de la multa: gravedad, disuasion, duracion, intencionalidad, categoria de datos y capacidad economica (Art. 43); pago en 15 dias habiles en la Direccion General de Tesoreria (Art. 44); cobro ejecutivo por la FGR (Art. 45); versiones publicas de resoluciones (Art. 46); prescripcion de infracciones y sanciones en 5 anos (Art. 47).
**A quien aplica:** Todos los sujetos obligados del Art. 2 LPDP.
**Implicacion para el software:** La reforma, segun las fuentes, no toca el Art. 53 ni la normativa sancionadora; solo reubica quien nombra al Director. Lo que si cambia materialmente en el privado es que desaparece el delegado como gestor con responsabilidad propia (Lineamientos Art. 24 inc. 2: el delegado respondia si no demostraba diligencia); toda la exposicion sancionadora por ARCO-POL recae en el responsable. El software debe mantener el modulo de "gestion de requerimientos e inspecciones de la ACE" (plazos de 5 dias habiles para contestar emplazamientos, 10 para alegatos, 15 para pagar multas) y reforzar la evidencia de cumplimiento de plazos ARCO-POL, porque "no atender las solicitudes ARCO-POL en el tiempo y forma establecidos" es infraccion grave (Art. 56 lit. b.2: 11 a 25 salarios minimos del comercio) y "denegar en contravencion a la ley" es muy grave (Art. 56 lit. c.2: 26 a 40 salarios minimos).
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\normativa_sancionadora_OCR.txt e imagenes en ...\fuentes\ocr\normativa_sancionadora\page-NN.png; https://ace.gob.sv/documentos/politicas/PASDPDP.pdf ; ace_decreto_144.txt (Arts. 53, 56 y 57). Consultados 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (los plazos de defensa aplican cuando la ACE abre diligencias o procedimiento: CONDICIONAL al inicio de la actuacion).

### 5.9 Otros efectos que conviene registrar

- Deber de asistencia interna (Art. 17 derogado): el software ya no puede fundar en el Art. 17 las tareas de "atender requerimientos del delegado" que se asignan a areas y proveedores. Tras la reforma, esas tareas se fundan en el Art. 16 reformado ("auxiliar a sus dependencias o proveedores", segun prensa), en el Art. 33 inc. 2 (proveedores sometidos a los lineamientos del responsable) y en el Art. 34 (obligaciones de responsable y encargado). Clasificacion: OBLIGATORIO con base cambiada.
- Recurso del titular ante la ACE (Lineamientos Art. 33 inc. 4, 10 dias habiles desde la notificacion de la resolucion del delegado): en el privado sin delegado, el fundamento formal desaparece, pero el titular conserva la denuncia ante la ACE (Normativa sancionadora Arts. 15 y 16). El software debe seguir advirtiendo que toda resolucion ARCO-POL puede ser revisada por la ACE.
- Delegado comun de grupo, sustitutos, delegado externo o persona juridica (Lineamientos Arts. 13 a 17): pasan a ser opciones de diseno organizativo voluntario en el privado.
- Costos (LPDP Art. 23; Lineamientos Art. 38): sin cambios; la publicacion de costos de reproduccion y envio la hace el responsable en ambos regimenes.

---

## 6. Diseno de doble estado

### 6.1 Principio

El software no decide cuando entra en vigencia la reforma: lo hace un parametro administrado con evidencia. Mientras el parametro este vacio, rige el regimen A (Decreto 144 original). Cuando el administrador registre la publicacion en el Diario Oficial (numero, tomo, fecha y enlace o archivo), el sistema calcula la fecha de vigencia y activa el regimen B a partir de ella. Nada se borra: los expedientes conservan el regimen bajo el cual se tramitaron.

```
+---------------------------+        +----------------------------------+
| Parametro global          |        | Evidencia requerida              |
| reforma_659.vigencia      | <----- | numero D.O., tomo, fecha         |
| (fecha o vacio)           |        | publicacion, archivo/enlace,     |
+-------------+-------------+        | quien lo registro, cuando        |
              |                      +----------------------------------+
              v
   fecha_vigencia = fecha_publicacion + 8 dias (clausula segun prensa;
   confirmar en el texto oficial; permitir sobrescribir manualmente)
              |
   +----------+-----------+
   |                      |
   v                      v
 hoy < vigencia         hoy >= vigencia
 REGIMEN A              REGIMEN B
 (Decreto 144)          (Decreto 144 + Decreto 659)
```

### 6.2 Comportamiento por modulo

| Modulo | Regimen A (hoy, reforma no vigente) | Regimen B (reforma vigente), cliente privado | Regimen B, cliente publico |
|---|---|---|---|
| Delegado | Obligatorio (Art. 15). Tarea "nombrar delegado" abierta; checklist de lineamientos ACE (perfil, acta, notificacion 3 dh, declaracion jurada, comunicacion ACE 15 dh sin fecha limite transitoria, certificacion cuando exista programa). Alerta de incumplimiento si no hay delegado. | Opcional. Tarea se convierte en "designar responsable(s) de atencion ARCO-POL" (obligatorio funcional). Si el cliente mantiene o nombra delegado voluntario, el checklist de lineamientos se ofrece como RECOMENDADO con nota de incertidumbre sobre registro y certificacion. Sin alertas de incumplimiento por ausencia de delegado. | Obligatorio (Art. 47 reformado). Checklist de lineamientos completo. Puede ser el Oficial de Informacion. |
| Recepcion ARCO-POL | Canal "al delegado" (Art. 18 inc. 2). Asignacion automatica al delegado. | Canal "a la empresa". Asignacion al rol o persona configurada; el delegado voluntario puede ser el asignatario por defecto. | Canal "al delegado". |
| Plazos ARCO-POL | 10 / 5 / 20 + 20 / 5 / 3 / 5 + 5 dias habiles. | Identicos. | Identicos. |
| Plantillas de resolucion | Firma: delegado. Fundamento: Arts. 16, 18 a 22, 30 y Lineamientos Art. 33. | Firma: responsable o persona designada. Fundamento: Arts. 16 (reformado), 18 a 22, 30 y 33. Sin cita al Art. 17 ni a los lineamientos salvo delegado voluntario. | Como en A. |
| Aviso de privacidad, Art. 24 lit. f | Campo obligatorio "nombre del delegado" + medios y lugar. | Campo "nombre del delegado" pasa a condicional: si hay delegado, se incluye; si no, se incluye "persona, area o punto de contacto responsable de atender derechos ARCO-POL" + medios y lugar, con nota juridica de incertidumbre. Regenerar y republicar el aviso al cambiar de regimen (Art. 24 lit. g: medios de comunicacion de cambios). | Campo obligatorio "nombre del delegado". |
| Deber de asistencia interna | Tareas a areas y proveedores fundadas en Art. 17. | Mismas tareas fundadas en Art. 16 reformado, 33 inc. 2 y 34. | Art. 17 derogado tambien para el publico; fundar en Art. 16 reformado y 47. |
| Registro ACE de delegados | Tarea "comunicar nombramiento a la ACE" visible con estado "fecha limite sin efecto (ACE, 12 sep 2026, fuente secundaria)". Registrar evidencia de envios ya hechos. | Tarea oculta salvo delegado voluntario; se reactiva si la ACE publica nuevo mecanismo (parametro con fecha). | Tarea visible; plazos de lineamientos. |
| Politicas de actuacion ACE (delegado como medida organizativa) | Coincide con la ley: obligatorio. | RECOMENDADO con nota de conflicto normativo pendiente de actualizacion por la ACE. | Obligatorio. |
| Procedimiento sancionador | Sin cambios. | Sin cambios; mensaje de que la responsabilidad por ARCO-POL recae integramente en el responsable. | Sin cambios. |
| Formularios ACE | Aceptar formularios oficiales (Lineamientos Art. 32); formulario de nombramiento de delegado disponible. | Aceptar formularios oficiales ARCO-POL; ocultar o marcar como "referencia historica" el formulario de nombramiento; adaptar la opcion "acudir con el delegado". | Como en A. |

### 6.3 Reglas de transicion

1. Expedientes ARCO-POL abiertos antes de la fecha de vigencia se terminan bajo el regimen A (plazos identicos, por lo que solo cambia el asignatario y la plantilla); el sistema ofrece reasignar al nuevo rol pero conserva la traza del regimen original.
2. La fecha de vigencia se calcula automaticamente pero es sobrescribible con justificacion, porque la clausula "ocho dias despues de su publicacion" consta solo por prensa y porque el computo (dias calendario, desde el dia siguiente o no) debe confirmarse con el texto oficial. Los Lineamientos ACE, por ejemplo, computan "ocho dias despues contados a partir del dia siguiente de su publicacion".
3. Entre la aprobacion (17 sep 2026) y la vigencia, mostrar un aviso informativo en el modulo Delegado y en el generador de avisos de privacidad: "Reforma aprobada, pendiente de publicacion; el regimen actual sigue vigente". No ocultar ni eliminar tareas.
4. Cada regla juridica debe versionarse (conjunto de reglas v1 = Decreto 144; v2 = Decreto 144 + Decreto 659) y cada expediente, documento generado y alerta debe registrar la version aplicada y la fecha de calculo, para auditoria.
5. Al obtener el texto oficial del Decreto 659 debe ejecutarse una lista de verificacion: (a) confirmar articulos derogados, reformados y adicionados; (b) confirmar si los Arts. 18 a 22, 24, 30 y 48 fueron tocados; (c) confirmar la clausula de vigencia y su computo; (d) confirmar si hay disposiciones transitorias (por ejemplo sobre delegados ya nombrados o registrados); (e) actualizar textos de plantillas y fundamentos legales; (f) registrar la fecha de esa verificacion.
6. Interruptores adicionales, con fecha y evidencia: "lineamientos ACE derogados o reformados", "politicas ACE actualizadas", "nuevo mecanismo de registro ACE", "programa de certificacion ACE vigente".
7. El parametro de tipo de sujeto obligado (privado o publico) debe capturarse en el alta del cliente porque determina el regimen del delegado en B.

---

## 7. Transcripciones de pasajes clave del corpus (texto vigente)

Art. 15 LPDP: "Los sujetos obligados por la presente ley deberan de nombrar un delegado de proteccion de datos personales, en adelante delegado, quien se encargara de gestionar y tramitar las solicitudes para el ejercicio de los derechos ARCO-POL."

Art. 17 LPDP: "Sera obligacion de cada dependencia, empleado o proveedor del responsable del tratamiento de datos de asistir y atender a las peticiones canalizadas por el delegado en el ejercicio de sus funciones."

Art. 18 inc. 2 LPDP: "La presentacion de la solicitud de derechos ARCO-POL debera realizarse al delegado. Cuando se trate de una solicitud de acceso a datos personales, el titular debera senalar la modalidad en la que prefiere que estos se reproduzcan..."

Art. 18 inc. 3 LPDP: "...el delegado debera realizar la prevencion respectiva por una sola ocasion, para que subsane las omisiones dentro de un plazo de diez dias habiles contados a partir del dia siguiente al de la notificacion. Si el interesado no realiza la actuacion requerida en el plazo previsto o la realiza sin atender a las prevenciones realizadas, se archivara su escrito sin mas tramite y quedara a salvo su derecho de presentar una nueva solicitud."

Art. 19 LPDP: "Si de la verificacion de la solicitud de derechos ARCO-POL, el delegado advirtiera que el responsable no es el competente para atenderla o que la solicitud corresponde a un derecho diferente de los previstos en la presente ley, debera hacerlo del conocimiento del titular y le devolvera la peticion dentro de los cinco dias habiles posteriores a su recepcion."

Art. 20 LPDP: "El delegado debera entregar al titular o su representante la respuesta respectiva a la solicitud de derechos ARCO-POL en el plazo de veinte dias habiles, pudiendo prorrogarse este plazo por causas justificadas y sin que dicha prorroga exceda otros veinte dias habiles."

Art. 21 inc. 2 y 3 LPDP: "Durante el proceso de rectificacion de datos personales, el delegado debera dejar constancia que dicha informacion se encuentra sometida a un proceso de rectificacion ante el requerimiento de terceros para acceder a la misma. En el supuesto de comunicacion o transferencia de datos personales, el delegado debera notificar la rectificacion, actualizacion o eliminacion de dichos datos a quienes hayan recibido los mismos, dentro de los cinco dias habiles posteriores a la determinacion de la procedencia de la solicitud del titular."

Art. 22 inc. final LPDP: "En todos los casos anteriores, el delegado debera notificar a traves de una resolucion motivada, las razones de su decision y comunicarla al titular, o en su caso, al representante, en los plazos de tres dias habiles a la adopcion de la decision..."

Art. 24 lit. f LPDP: "Indicacion del nombre del delegado y lugar o medios para presentar la solicitud de derechos ARCO-POL."

Art. 47 LPDP: "Para el ejercicio de los derechos contemplados en el articulo anterior, se debera cumplir con lo dispuesto en la Seccion B, Capitulo III del Titulo I de la presente ley. Para tales efectos, el nombramiento del delegado podra recaer en el Oficial de Informacion de la institucion pertinente."

Art. 51 inc. 2 LPDP: "Para asistir al Director General en el ejercicio de sus funciones, sera nombrado un Director de Proteccion de Datos Personales. Este funcionario tambien conocera de los procedimientos administrativos para imponer las sanciones que establece la presente ley, y podra delegar la instruccion y sustanciacion de estos procedimientos, no asi la imposicion de la sancion, en un empleado o funcionario de la ACE distinto del Director General."

Lineamientos ACE, Considerando II (OCR, pagina 2): "Que de acuerdo con el articulo 15 de la citada Ley, los sujetos obligados nombraran un Delegado de Proteccion de Datos Personales, quien posee atribuciones especificas contempladas en dicha normativa y desarrolladas en los presentes lineamientos..."

Lineamientos ACE, Art. 40 (OCR, pagina 11): "Mientras no se encuentre habilitada la plataforma informatica del registro de Delegados, las comunicaciones de nombramiento, modificacion o cesacion se realizaran mediante oficio, escrito o correo institucional dirigido a la Direccion de Proteccion de Datos Personales de la ACE, dentro de los veinte dias habiles de la entrada en vigencia de estos lineamientos."

Lineamientos ACE, Art. 42 (OCR, pagina 11): "Los presentes lineamientos entraran en vigencia ocho dias despues contados a partir del dia siguiente de su publicacion en el Diario Oficial."

Descripcion del Art. 16 reformado segun El Diario de Hoy (17 sep 2026, fuente secundaria): "Entre las reformas aprobadas al articulo 16, se establece que los sujetos obligados deberan auxiliar a sus dependencias o proveedores y fijar lineamientos internos para gestionar las solicitudes ARCO-POL."

Descripcion del Art. 51 reformado segun El Diario de Hoy (17 sep 2026, fuente secundaria): "las modificaciones al articulo 51 facultan al presidente de la Republica para nombrar por un periodo de tres anos al director de Proteccion de Datos Personales, funcionario enmarcado en la Agencia de Ciberseguridad del Estado (ACE) que asistira al director general de dicha entidad. Este director estara a cargo de los procedimientos administrativos sancionatorios y podra delegar la instruccion de los expedientes en personal de la ACE, reservandose la facultad de imponer las sanciones."

Comunicado ACE segun elsalvador.com (12 sep 2026, fuente secundaria): "Queda sin efecto la fecha limite establecida para el nombramiento del delegado de proteccion de datos personales" y "no sera necesario realizar ninguna accion al respecto".

---

## 8. Incertidumbres y puntos que requieren abogado

1. Texto oficial del Decreto 659: no localizado. Toda la descripcion de articulos reformados es de fuente secundaria. Riesgo: que existan articulos reformados o transitorios no reportados por la prensa (por ejemplo, sobre delegados ya nombrados o comunicados a la ACE, o sobre el Art. 24 lit. f).
2. Fecha de publicacion en el Diario Oficial y fecha de vigencia: desconocidas. El archivo digital del D.O. llega solo al 07-09-2026. Debe monitorearse diariamente la API de diariooficial.gob.sv (year=2026, month=9 y siguientes) y la ficha view/7022 de la Asamblea.
3. Clausula de vigencia "ocho dias despues de su publicacion": consta solo por prensa. El computo exacto (desde la publicacion o desde el dia siguiente; dias calendario) requiere el texto.
4. Alcance de la reforma sobre los Arts. 18 a 22 y 30: las fuentes describen los plazos con "sujeto obligado", y la nota oficial habla de "enmiendas" sobre constancia de rectificacion y revocacion, pero solo se listan como reformados los Arts. 16, 47 y 51. Si esos articulos no fueron reformados, seguiran diciendo "delegado" en un regimen sin delegado obligatorio en el privado; la interpretacion sistematica (el responsable asume esas funciones) es razonable pero debe validarla un abogado.
5. Art. 24 lit. f (nombre del delegado en el aviso de privacidad): sin noticia de reforma. Requiere criterio juridico sobre como cumplir el literal sin delegado (propuesta: persona o punto de contacto responsable) y sobre si un aviso sin "nombre del delegado" podria considerarse incompleto por la ACE.
6. Lineamientos ACE para el Delegado: vigentes formalmente; fundamento (Art. 15) derogado en cuanto a obligatoriedad. Se desconoce si la ACE los derogara, los reformara para limitarlos al sector publico y a delegados voluntarios, o los mantendra. Tambien se desconoce si un delegado voluntario del privado debera registrarse y certificarse.
7. Politicas de Actuacion ACE N. 001-0309025-DPDP: siguen exigiendo delegado como medida organizativa. Conflicto normativo con la ley reformada; no hay noticia de actualizacion. Ademas, el contexto del proyecto senala que su fecha de emision y publicacion siguen pendientes de verificar.
8. Comunicado de la ACE del 12 de septiembre de 2026 (fecha limite sin efecto): no localizado en ace.gob.sv; consta por elsalvador.com, El Diario de Hoy y Contaxtern. Se desconoce su alcance exacto (solo la fecha limite transitoria, o tambien el plazo ordinario de 15 dias habiles del Art. 10).
9. Delegados ya nombrados y comunicados a la ACE antes de la reforma: no hay disposicion conocida sobre su situacion (cesan, se mantienen como voluntarios, deben comunicar la cesacion). Requiere el texto del decreto y criterio de la ACE.
10. Responsabilidad y evidencia: en el privado desaparece el delegado como figura con deber de diligencia propio (Lineamientos Art. 24); conviene que un abogado confirme como documentar la asignacion interna de responsabilidades para efectos de la carga de la prueba (LPDP Art. 54) y de un eventual procedimiento sancionador.
11. Calendario constitucional (Arts. 135, 137 y 139 Cn) citado en la seccion 3.1 solo como orientacion; no verificado en esta pasada contra el texto constitucional.
12. Formularios oficiales de la ACE (nombramiento de delegado y ARCO-POL con la opcion "acudir con el delegado"): se desconoce si la ACE publicara versiones actualizadas.
13. Materia registrada en la ficha de la Asamblea ("Sistema Judicial", "Penal y Procedimientos", "Derecho Penal"): parece un error de catalogacion; no afecta el contenido pero puede dificultar busquedas futuras por materia.
14. La nota oficial dice que "se creara" el cargo de Director de Proteccion de Datos Personales, aunque el Art. 51 ya lo preveia; un abogado debe confirmar si la reforma crea algo nuevo (por ejemplo, rango o forma de nombramiento) o solo ajusta la designacion.

---

## 9. Fuentes consultadas (fecha de consulta: 2026-09-23)

Fuentes primarias:
- Asamblea Legislativa, ficha del Decreto 659: https://www.asamblea.gob.sv/leyes-y-decretos/view/7022 (obtenida via POST a https://www.asamblea.gob.sv/leyes-y-decretos/resultado-busqueda/ con no_decreto=659; el mismo buscador devuelve 660 = ratificacion de acuerdo con EE.UU. sobre el Cuerpo de Paz).
- Asamblea Legislativa, nota oficial de la reforma: https://www.asamblea.gob.sv/node/14116
- Asamblea Legislativa, buscador: https://www.asamblea.gob.sv/leyes-y-decretos/busqueda-decretos ; ultimos aprobados: https://www.asamblea.gob.sv/leyes-y-decretos/ultimos-aprobados ; agenda y correspondencia de la sesion 127 (23 sep 2026): https://www.asamblea.gob.sv/sites/default/files/documents/agenda/8C06F786-F882-4FC7-BFDB-F880410060C8.pdf y https://www.asamblea.gob.sv/sites/default/files/documents/correspondencia/02FD2FD0-EED1-4695-BCC9-9A6E521178AE.pdf (no contienen la reforma).
- Diario Oficial, archivo digital: https://www.diariooficial.gob.sv/ y API https://www.diariooficial.gob.sv/api/v1/diarios-disponibles (POST year=2026&month=9: ediciones 01, 02, 03, 04 y 07 de septiembre; month=8: incluye 11-08-2026).
- Imprenta Nacional: https://imprentanacional.gob.sv/ultima-publicacion-a-la-venta-del-diario-oficial/ (ultimo D.O. a la venta: 07-09-2026).
- Ley para la Proteccion de Datos Personales, Decreto 144: C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt y ...\diario_oficial_2024-11-15_mh.txt
- Lineamientos para el Delegado (ACE), D.O. N. 146, Tomo 452, 11 ago 2026: C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\lineamientos_dpo_OCR.txt e imagenes ...\fuentes\ocr\lineamientos_dpo\page-01.png a page-11.png; https://ace.gob.sv/documentos/politicas/NDPDDP.pdf
- Normativa para el Procedimiento Administrativo Sancionador (ACE), mismo D.O.: C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\normativa_sancionadora_OCR.txt e imagenes ...\fuentes\ocr\normativa_sancionadora\ ; https://ace.gob.sv/documentos/politicas/PASDPDP.pdf
- Politicas de Actuacion ACE N. 001-0309025-DPDP: C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_politicas_protecciondatos.txt ; https://ace.gob.sv/page/politicas
- Formularios ACE (07-07-2025): C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_form_nombramiento_delegado.txt, ace_form_acceso.txt, ace_form_cancelacion.txt, ace_form_portabilidad.txt ; https://ace.gob.sv/page/formularios
- ACE, noticias: https://ace.gob.sv/page/noticias (solo webinars del 09/09/2026: /noticia/webinar y /noticia/segundo-webinar-delegado-de-proteccion-de-datos)
- Documentos historicos descartados (no son la reforma): https://www.asamblea.gob.sv/sites/default/files/documents/dictamenes/498798FA-A563-4830-A0C8-306AFBC71497.pdf (Dictamen 46, Comision de Economia, 13 abr 2021); https://www.asamblea.gob.sv/sites/default/files/documents/correspondencia/2A326CE8-F13A-4828-8640-648235C228BF.pdf (iniciativa ARENA, 24 jun 2019); https://www.asamblea.gob.sv/sites/default/files/documents/correspondencia/EFBA7BEE-871B-40BE-BD0A-5BD80237CA90.pdf (veto al Decreto 875, 7 may 2021).

Fuentes secundarias:
- El Diario de Hoy, 17 sep 2026: https://www.eldiariodehoy.com/noticias/nacionales/asamblea-legislativa-deroga-obligatoriedad-de-las-empresas-privadas-de-nombrar-delegados-de-proteccion-de-datos-personales/93615/2026/
- El Diario de Hoy, opinion, 18 sep 2026 (Jaime Ramirez Ortega): https://www.eldiariodehoy.com/opinion/se-elimina-el-delegado-de-las-empresas-pero-no-la-responsabilidad-de-proteger-los-datos-de-las-personas/93642/2026/
- El Diario de Hoy, 12 sep 2026: https://www.eldiariodehoy.com/noticias/nacionales/sin-fecha-para-nombrar-delegados-de-proteccion-de-datos-personales/93083/2026/
- elsalvador.com, 17 sep 2026: https://www.elsalvador.com/noticias/nacional/reforma-proteccion-datos-personales/1293875/2026/
- elsalvador.com, 12 sep 2026: https://www.elsalvador.com/dinero-y-negocios/entorno-economico/empresas-ley-de-proteccion-datos-el-salvador/1292968/2026/
- Infobae, 17 sep 2026: https://www.infobae.com/el-salvador/2026/09/17/el-salvador-la-asamblea-legislativa-elimina-la-obligacion-del-delegado-de-proteccion-de-datos-para-las-empresas/
- La Noticia SV: https://lanoticiasv.com/eliminan-obligatoriedad-de-delegado-de-proteccion-de-datos-para-empresas/
- hoy.com.sv, 23 sep 2026: https://www.hoy.com.sv/tegnologia/reforman-ley-de-proteccion-de-datos-personales-para-facilitar-solicitudes-de-los-ciudadanos/
- ContraPunto, 13 sep 2026: https://www.contrapunto.com.sv/sin-fecha-para-nombrar-a-los-delegados-de-proteccion-de-datos-personales-la-ace-establece-el-registro-obligatorio/
- EY Law Alert, 26 ago 2026: https://www.ey.com/es_ce/technical/tax/tax-alerts/el-salvador-la-agencia-de-ciberseguridad-del-estado-desarrolla-aspectos-relevantes-de-la-ley-de-proteccion-de-datos-personales
- Consortium Legal, 2 sep 2026: https://consortiumlegal.com/2026/09/02/delegado-proteccion-datos-el-salvador/
- Contaxtern (guia comercial, actualizada 12 sep 2026): https://contaxtern.com/delegado-de-proteccion-de-datos-el-salvador/
- La Prensa Grafica (18 y 21 sep 2026, solo via PressReader, de pago, no leidas): https://www.pressreader.com/el-salvador/la-prensa-grafica/20260918/281552297762828 ; .../20260921/281749866264066 ; .../20260921/281835765609986
- BLP Legal (bloqueado, HTTP 403): https://blplegal.com/es/delegado-proteccion-datos-el-salvador-ace/
