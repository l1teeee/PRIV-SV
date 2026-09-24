# Sweep juridico: infracciones, multas, procedimiento sancionador y denuncias (LPDP El Salvador)

Proyecto PRIV-SV. Lente: "Infracciones, multas, procedimiento sancionador y denuncias".
Fecha de consulta de todas las fuentes: 2026-09-23.
Autor: investigador juridico (agente). Este documento no es asesoria legal; senala expresamente los puntos que requieren abogado.

Convenciones: LPDP = Ley para la Proteccion de Datos Personales (Decreto Legislativo 144). LCSI = Ley de Ciberseguridad y Seguridad de la Informacion (Decreto Legislativo 143). LPA = Ley de Procedimientos Administrativos (Decreto Legislativo 856). "Normativa PAS" = Normativa para el Desarrollo del Procedimiento Administrativo Sancionador en el Ambito de la LPDP (ACE). SM = salario minimo mensual vigente del sector comercio. ACE = Agencia de Ciberseguridad del Estado. DPDP = Director de Proteccion de Datos Personales de la ACE.

---

## 1. Resumen ejecutivo del lente

1. El regimen sancionador de la LPDP tiene tres capas normativas que el software debe distinguir: (a) la LPDP (Arts. 50 a 59) fija infracciones, multas, medidas adicionales, prohibiciones, carga de la prueba y publicidad; (b) el Art. 53 LPDP remite el procedimiento y la prescripcion a la LCSI, cuyo Art. 28 remite a su vez al procedimiento simplificado de la LPA y cuyo Art. 29 fija la prescripcion en cinco anos; (c) la ACE desarrollo todo eso en la Normativa PAS, publicada en el Diario Oficial No. 146, Tomo 452, del 11 de agosto de 2026 y vigente desde el 19 de agosto de 2026. La LPA es supletoria en todo (LPDP Art. 62, LCSI Art. 30, Normativa PAS Art. 48).

2. Catalogo de infracciones (LPDP Art. 56): 9 leves, 7 graves y 10 muy graves. Cada una se mapea a una obligacion concreta de la ley y a un control del software (seccion 3). Las infracciones que mas dependen de evidencia documental son: no informar antes de recolectar (leve 1 y 8), no notificar vulneraciones (leve 3), no atender requerimientos de la ACE (leve 9), no atender ARCO-POL en tiempo y forma (grave 2), desvio de finalidad (grave 3), no implementar medidas y lineamientos de la ACE (graves 5 y 7), tratar sin consentimiento (muy grave 1), denegar ARCO-POL indebidamente (muy grave 2), transferencias sin consentimiento o a paises sin nivel adecuado (muy graves 5 y 6) y no hacer efectiva la revocacion (muy graves 9 y 10).

3. Multas (LPDP Art. 57): leves 1 a 10 SM, graves 11 a 25 SM, muy graves 26 a 40 SM. El SM del sector comercio y servicios vigente el 2026-09-23 es US$408.80 mensuales (Decreto Ejecutivo No. 11 del Ramo de Trabajo, 22 de mayo de 2025, vigente desde el 1 de junio de 2025, reformado por Decreto Ejecutivo No. 12 del 24 de mayo de 2025). No existe un nuevo decreto de salario minimo para 2026. Rangos actuales: leves US$408.80 a US$4,088.00; graves US$4,496.80 a US$10,220.00; muy graves US$10,628.80 a US$16,352.00. Las cifras de prensa divergen porque usan el salario anterior de US$365 (rango US$365 a US$3,650 para leves, hasta US$14,600 para muy graves), o el salario actual (US$408.80 a US$16,352), o se refieren a un proyecto de ley distinto de 2021 (la cifra de "hasta $152,000" no corresponde al Art. 57 de la ley vigente).

4. Procedimiento (Normativa PAS): diligencias preliminares de investigacion de hasta 90 dias habiles prorrogables; inicio de oficio, por denuncia, por aviso o por cualquier otro medio; via simplificada por regla general (LPA Art. 158) y via ordinaria por excepcion; emplazamiento personal y 5 dias habiles para contestar, alegar y proponer prueba; alegatos finales de 10 dias habiles solo en via ordinaria; remision del expediente por el delegado instructor en maximo 8 dias habiles; resolucion final en 15 dias habiles; pago de la multa en 15 dias habiles; aviso a la FGR en 72 horas si hay ilicito penal; en via simplificada no hay recurso administrativo y queda abierta la via contencioso-administrativa; en via ordinaria caben reconsideracion, apelacion y revision de la LPA. Prescripcion de infracciones y sanciones: cinco anos, computados segun LPA Art. 149.

5. Criterios de graduacion (Normativa PAS Art. 43): gravedad del dano o del probable peligro, efecto disuasivo, duracion de la conducta, caracter intencional o negligente, naturaleza o categoria de los datos afectados (con proteccion especial para datos sensibles, Art. 32 inc. 2) y capacidad economica del infractor. IMPORTANTE: los criterios "tamano de la empresa, participacion, condicion del afectado y reincidencia en 2 anos" que aparecian en el encargo de investigacion NO se encontraron en la LPDP, en la LCSI, en la Normativa PAS ni en la LPA. No deben incorporarse al software como si fueran ley. Lo unico cercano es: la LPA Art. 157 (apercibimiento en lugar de sancion para infracciones leves solo si el infractor "no hubiese sido sancionado o apercibido con anterioridad"), la LPA Art. 156 (aceptacion de responsabilidad como atenuante, con reduccion de hasta una cuarta parte de la multa) y la LPA Art. 145 (sancion previa como atenuante en caso de identidad parcial de fundamento).

6. Denuncias: el titular puede denunciar ante la ACE cuando no se resuelve su rectificacion en 20 dias habiles (LPDP Art. 9 inc. 3), cuando se le niega la revocacion del consentimiento (Art. 31) y, en general, por cualquier infraccion (Normativa PAS Arts. 8 lit. b, 15 lit. b y 16). La ACE no publica al 2026-09-23 un formulario especifico de denuncia; publica ocho formularios ARCO-POL y de nombramiento de delegado (version 07-07-2025). La denuncia puede presentarse por escrito o por cualquier medio tecnologico que la ACE habilite, con los requisitos del Art. 16 de la Normativa PAS y del Art. 150 LPA.

7. Paquete de evidencia: la ACE puede pedir "antecedentes, documentos, programas u otros elementos relativos al tratamiento" (LPDP Art. 50 lit. t), practicar inspecciones, verificaciones tecnicas, entrevistas y analisis documental o pericial (Normativa PAS Art. 10), y admite como prueba los informes de auditoria internos o externos (Art. 24). La carga de la prueba del consentimiento y de la comunicacion del aviso de privacidad recae en el responsable (LPDP Art. 54). El software debe poder producir, con trazabilidad y fechas ciertas, ese paquete en un plazo compatible con los 5 dias habiles del emplazamiento.

8. Retencion de evidencia: como las infracciones prescriben a los cinco anos contados desde el dia siguiente a la comision (o desde el ultimo hecho en infracciones continuadas) y la prescripcion se interrumpe con el inicio del procedimiento, la evidencia de cumplimiento debe conservarse al menos cinco anos y, si hay procedimiento abierto, hasta su firmeza (RECOMENDADO, derivado de la regla de prescripcion; no es un plazo de conservacion expreso).

---

## 2. Instrumentos normativos del lente y su vigencia

| Instrumento | Identificacion | Publicacion | Vigencia | Fuente |
|---|---|---|---|---|
| LPDP | Decreto Legislativo 144, 12 nov 2024 | D.O. 219, Tomo 445, 15 nov 2024 | VIGENTE desde 23 nov 2024 (Art. 64) | `fuentes/ace_decreto_144.txt`; `fuentes/diario_oficial_2024-11-15_mh.txt` |
| Reforma LPDP (DL 659) | Aprobada 17 sep 2026, 57 votos | Publicacion en D.O. no confirmada al 2026-09-23 | APROBADA-PENDIENTE-PUBLICACION. La nota oficial de la Asamblea no menciona cambios a los Arts. 53 a 59 ni a denuncias | https://www.asamblea.gob.sv/node/14116 |
| LCSI | Decreto Legislativo 143, 12 nov 2024 | D.O. 219, Tomo 445, 15 nov 2024 | VIGENTE desde 23 nov 2024 (Art. 32) | https://www.asamblea.gob.sv/sites/default/files/documents/decretos/D056D9A1-299D-4188-941A-9C3B5898D3F3.pdf |
| LPA | Decreto Legislativo 856, 15 dic 2017 | D.O. 30, Tomo 418, 13 feb 2018 | VIGENTE desde 13 feb 2019 (Art. 168: doce meses despues de su publicacion) | https://www.asamblea.gob.sv/sites/default/files/documents/decretos/361DDB77-97E7-4EFF-B353-C6D872547E7C.pdf |
| Normativa PAS (ACE) | Emitida 24 jul 2026 por el Director General de la ACE, Registro F40430, 49 articulos | D.O. 146, Tomo 452, 11 ago 2026, paginas 22 a 29 | VIGENTE desde 19 ago 2026 (Art. 49: ocho dias despues de su publicacion) | `fuentes/normativa_sancionadora_OCR.txt`, verificado contra `fuentes/ocr/normativa_sancionadora/page-02.png` a `page-09.png` |
| Politicas de Actuacion ACE N. 001-0309025-DPDP | Politica de actuacion (LPDP Arts. 35 y 50 lit. i) | Fecha pendiente de verificar | VIGENTE (Art. 9 de la politica: desde su publicacion) | `fuentes/ace_politicas_protecciondatos.txt`; https://ace.gob.sv/politicas.php |
| Lineamientos para el Delegado (ACE) | Lineamiento | D.O. 146, Tomo 452, 11 ago 2026 | VIGENTE desde 19 ago 2026; parcialmente afectado por la reforma pendiente | `fuentes/lineamientos_dpo_OCR.txt` |
| Decreto Ejecutivo 11 (salario minimo) | Ramo de Trabajo y Prevision Social, 22 may 2025; reformado por D.E. 12 de 24 may 2025 (D.O. 96, Tomo 447, 26 may 2025) | D.O. 95, Tomo 447, 23 may 2025 (numero segun fuentes secundarias) | VIGENTE desde 1 jun 2025 (Art. 15). Sin decreto nuevo para 2026 | https://www.jurisprudencia.gob.sv/DocumentosBoveda/D/2/2020-2029/2025/05/10A4DA.PDF |

Nota sobre el corpus local: el archivo `diario_oficial_2024-11-15_mh.txt` contiene solo el Decreto 144 (paginas 24 a 62 del D.O.). El Decreto 143 se cito desde el PDF oficial de la Asamblea Legislativa.

---

## 3. (a) Catalogo completo de infracciones del Art. 56 LPDP y mapeo al software

Texto de encabezado (LPDP Art. 56): "Las infracciones se clasificaran en leves, graves y muy graves". Los numerales se transcriben literalmente; el resto de columnas es analisis.

### 3.1 Infracciones leves (Art. 56 lit. a), numerales 1 a 9)

| N. | Texto legal (literal) | Obligacion incumplida | Modulo o control del software que previene o prueba cumplimiento |
|---|---|---|---|
| a.1 | "No informar al titular de los datos personales acerca de sus derechos antes de ser recolectados." | Derecho de informacion en la recoleccion (Art. 7) y contenido del aviso de privacidad (Art. 24 lit. e y siguientes) | Modulo Aviso de privacidad: versionado del aviso, registro de en que punto de captura se mostro, fecha y version entregada a cada titular. Evidencia: constancia de comunicacion por titular (Art. 54) |
| a.2 | "No publicar los datos de contacto del encargado del tratamiento." | Publicidad de datos de contacto (Art. 24 lit. a y b: identidad y domicilio del responsable y, por extension, de quien atiende derechos). Redaccion legal ambigua ("encargado") | Modulo Aviso de privacidad: campo obligatorio de contacto y canal de derechos; verificacion periodica de que el aviso publicado contiene el contacto vigente. Ver incertidumbre I-3 |
| a.3 | "Omitir notificar respecto de las vulneraciones a la seguridad de los datos personales acaecidas a los sujetos pertinentes, de conformidad con lo dispuesto en el articulo 25 de la presente ley." | Notificar a la ACE, a la FGR y a los titulares en maximo 72 horas desde el conocimiento (Art. 25) | Modulo Incidentes: reloj de 72 horas desde la fecha y hora de conocimiento, tres destinatarios con constancia de envio, contenido minimo a) a e), y bitacora de la vulneracion (fecha, motivo, hechos, efectos, medidas) exigida por el Art. 25 inc. final |
| a.4 | "Acceder a un banco de datos, base de datos, repositorio, sistemas o registros, tanto manuales como informaticos, sin autorizacion del responsable de estos." | Control de acceso y confidencialidad (Art. 5 lit. f; Politicas ACE, medidas tecnicas: control de acceso, gestion de identidades) | Modulo Inventario de bases de datos y accesos: matriz de autorizaciones por base de datos y por rol, registro de altas y bajas de acceso, revisiones periodicas de acceso con firma del responsable. Esta infraccion tambien la comete un tercero que accede sin autorizacion; para la empresa, la matriz prueba quien estaba autorizado |
| a.5 | "Dar un tratamiento a los datos personales de forma inexacta o falsa." | Principio de exactitud (Art. 5 lit. a); rectificacion (Art. 9) | Modulo ARCO-POL (rectificacion) y controles de calidad de datos: registro de rectificaciones aplicadas, bloqueo de datos en revision (Art. 9 inc. final), notificacion a receptores (Art. 21) |
| a.6 | "Modificar los datos suministrados en el documento que autoriza el tratamiento de datos personales." | Integridad del documento de consentimiento (Arts. 26 y 27) | Modulo Consentimientos: consentimiento inmutable una vez otorgado (sello de tiempo, hash o equivalente funcional), cambios solo mediante nuevo consentimiento, historial completo |
| a.7 | "Exigir pago para atender las solicitudes que en la presente ley se establecen como gratuitas." | Gratuidad de ARCO-POL, solo costos de reproduccion, certificacion y envio previamente publicados (Art. 23); revocacion gratuita (Art. 29) | Modulo ARCO-POL: tarifario publicado de costos de reproduccion con fecha de publicacion; prohibicion de cobros distintos; constancia de que la solicitud se tramito sin cobro |
| a.8 | "Incumplir con el Derecho de Informacion frente a la Recoleccion de Datos contenido en el articulo 7 o la obligacion de informar del articulo 48, ambos de la presente ley." | Art. 7 (informar quien resguarda, finalidad, etc.) y Art. 48 (deber de informar de los sujetos del inciso 2 del Art. 2, sector publico) | Modulo Aviso de privacidad y puntos de captura: inventario de formularios y canales de recoleccion con el texto informativo asociado y su version; evidencia de comunicacion por titular |
| a.9 | "No atender las solicitudes realizadas por parte de la ACE en materia de proteccion de datos personales." | Deber de colaboracion con la autoridad (Art. 50 lit. a y t) | Modulo Requerimientos de autoridad (expediente ACE): registro de cada requerimiento, plazo otorgado, responsable interno, respuesta enviada y acuse; alertas de vencimiento |

### 3.2 Infracciones graves (Art. 56 lit. b), numerales 1 a 7)

| N. | Texto legal (literal) | Obligacion incumplida | Modulo o control del software |
|---|---|---|---|
| b.1 | "Proporcionar de forma incompleta o inexacta la informacion relativa a los datos personales que del titular se traten, ya sean recolectados o inferidos, cuando este ejerza su derecho de acceso." | Derecho de acceso completo (Art. 8), incluidos datos inferidos | Modulo ARCO-POL (acceso): plantilla de respuesta que recorre todas las bases de datos del inventario (RAT), incluye datos inferidos y el intercambio con otras entidades (Art. 8 inc. final); lista de verificacion de completitud firmada antes de enviar |
| b.2 | "No atender las solicitudes de derechos ARCO-POL, en el tiempo y forma establecidos por la presente ley." | Arts. 18 a 22 (requisitos, prevencion unica de 10 dias habiles, devolucion en 5, respuesta en 20 + 20 dias habiles, notificacion a receptores en 5, denegatoria motivada en 3) y Art. 33 (procedimientos documentados) | Modulo ARCO-POL: reloj por solicitud con dias habiles, estados (recibida, prevenida, subsanada, prorrogada con causa, resuelta, notificada), evidencia de cada notificacion. Procedimiento interno documentado y versionado (Art. 33) |
| b.3 | "Procesar, recopilar o destinar datos personales con finalidad diferente para la que se otorgo el consentimiento o se habilito su tratamiento." | Principio de finalidad y consentimiento especifico (Art. 5, Arts. 26 y 27) | Modulo RAT + Consentimientos: cada actividad de tratamiento declara finalidad y base de licitud; cada consentimiento se vincula a finalidades concretas; alerta cuando se crea un uso nuevo sobre datos ya recolectados sin nueva base |
| b.4 | "Obstaculizar el desarrollo de las auditorias o inspecciones que realice la ACE." | Deber de colaboracion (Art. 50 lit. a); inspecciones y verificaciones tecnicas (Normativa PAS Art. 10) y seguimiento de medidas (Art. 38) | Modulo Requerimientos de autoridad: protocolo de atencion de inspecciones, designacion de interlocutor, acta interna de la visita, entrega documentada de lo requerido |
| b.5 | "No implementar las medidas, controles tecnicos o lineamientos que establezca la ACE en materia de proteccion de datos." | Politicas, medidas, guias y lineamientos de la ACE (Arts. 35, 50 lit. i y n, 60) | Modulo Cumplimiento de disposiciones ACE: catalogo de disposiciones vigentes (politicas, lineamientos, guias) con fecha, controles derivados, responsable, estado de implementacion y evidencia por control |
| b.6 | "Incurrir en las prohibiciones establecidas en el articulo 59 de la presente ley." | Prohibiciones del Art. 59 (ver seccion 5.2) | Modulo Datos sensibles y Transferencias: bloqueo de creacion de bases con datos sensibles sin base juridica registrada; control de comercializacion y comunicacion de datos; ver seccion 5.2 |
| b.7 | "No cumplir con las medidas de seguridad establecida en las politicas de actuacion emitidas por la Agencia." | Art. 36 (acatar y mantener las medidas de seguridad de la ACE) y Politicas ACE N. 001-0309025-DPDP (medidas organizativas, tecnicas, fisicas y de transferencia; auditorias anuales) | Modulo Medidas de seguridad: lista de verificacion de las medidas de la Politica ACE (2FA, cifrado, backups, gestion de identidades, pentesting, capacitacion, RAT, EIPD, auditorias) con evidencia adjunta y fecha de ultima verificacion; plan de auditoria anual |

### 3.3 Infracciones muy graves (Art. 56 lit. c), numerales 1 a 10)

| N. | Texto legal (literal) | Obligacion incumplida | Modulo o control del software |
|---|---|---|---|
| c.1 | "Tratar datos personales sin el consentimiento previo, de conformidad con lo establecido en el articulo 26 de la presente ley." | Consentimiento expreso previo (Art. 26), requisitos (Art. 27), salvo excepciones del Art. 28 | Modulo Consentimientos + RAT: ninguna actividad de tratamiento puede quedar sin base de licitud registrada; cuando la base es consentimiento, existe registro por titular con fecha, medio, texto aceptado y version del aviso; para datos sensibles, consentimiento escrito con firma autografa o equivalente (Art. 26 inc. 4) |
| c.2 | "Denegar las solicitudes realizadas para el ejercicio de los derechos ARCO-POL en contravencion a lo establecido en esta ley." | Causales tasadas de denegatoria y motivacion (Art. 22); derechos Arts. 6 a 14 | Modulo ARCO-POL: la denegatoria exige seleccionar una causal legal y redactar motivacion; revision de segundo nivel antes de notificar; constancia de notificacion en 3 dias habiles |
| c.3 | "El uso de los datos personales de ninos, ninas y adolescentes sin el previo consentimiento de sus padres, representantes o tutores, de conformidad con las leyes vigentes o tratados internacionales debidamente suscritos y ratificados por El Salvador." | Art. 26 inc. 2 (principio de ejercicio progresivo de las facultades) y Art. 42 (interes superior de NNA, informacion adaptada a la edad) | Modulo Consentimientos: marcador de titular menor de edad, captura del consentimiento del progenitor o tutor con identificacion, y texto informativo adaptado (Art. 42). Los formularios ACE ya preven la casilla "Ninez y Adolescencia" |
| c.4 | "Tratar datos personales de personas declaradas incapaces sin el consentimiento de su titular o su representante." | Art. 26 inc. 3 (remision al derecho comun) y Art. 43 (grupos en situacion de desventaja) | Modulo Consentimientos: marcador de representacion legal y documento que la acredita |
| c.5 | "Realizar transferencia internacional de datos personales a paises que no cumplan como minimo con el nivel de proteccion exigido por la presente ley." | Art. 44 (nivel adecuado, consentimiento previo salvo excepciones) y Art. 45 (poner en conocimiento de la ACE) | Modulo Transferencias: registro de cada flujo internacional con pais, receptor, analisis de nivel de proteccion, base juridica, contrato (Art. 41) y constancia de comunicacion a la ACE (Art. 45). La carga de la prueba de la transferencia internacional recae en el responsable (Art. 54 inc. 2) |
| c.6 | "Realizar transferencia de datos personales sin el consentimiento de su titular o su representante, o en contravencion de las excepciones que establezca la ley." | Art. 40 (consentimiento previo e informacion), Art. 41 (contrato con el receptor) | Modulo Transferencias y Encargados: cada transferencia vinculada a la base de licitud y al consentimiento o excepcion aplicable; inventario de contratos con encargados y receptores |
| c.7 | "Comercializar datos personales a cualquier titulo sin el consentimiento de su titular." | Prohibicion de comercializar sin consentimiento (Art. 59 lit. c y d; Art. 40) | Modulo Transferencias: tipificacion de la transferencia como onerosa o gratuita; bloqueo de flujos onerosos sin consentimiento especifico registrado |
| c.8 | "Revertir la seudonimizacion de los datos personales sin el consentimiento del titular." | Definicion de seudonimizacion (Art. 4 lit. q) y garantias asociadas | Modulo Inventario de bases de datos: identificacion de conjuntos seudonimizados, custodia separada de la clave de reidentificacion, registro de cada reidentificacion con base juridica |
| c.9 | "Tratar datos personales a pesar de la revocacion del consentimiento otorgado por el titular." | Art. 29 (revocacion en cualquier momento, sin efecto retroactivo) y Art. 30 (5 dias habiles para proceder; 5 dias habiles para informar al encargado) | Modulo Revocaciones: la revocacion cambia el estado del consentimiento y genera tareas de cese a las areas y encargados con plazo de 5 dias habiles y constancia de ejecucion |
| c.10 | "No hacer efectiva la revocacion del consentimiento ante la solicitud del titular cuando esta proceda." | Arts. 29, 30 y 31 (negativa injustificada habilita denuncia ante la ACE) | Modulo Revocaciones: mecanismo "expedito, sencillo y gratuito" (Art. 29) con acuse al titular; analisis de procedencia documentado; si se mantiene el tratamiento por otra base de licitud (Art. 29 inc. 2), esa base queda registrada |

### 3.4 Lectura transversal para el producto

- Cada infraccion tiene un "lugar de prueba" claro: aviso y consentimiento (a.1, a.6, a.8, c.1, c.3, c.4), ARCO-POL y revocaciones (a.5, a.7, b.1, b.2, c.2, c.9, c.10), incidentes (a.3), accesos y bases de datos (a.4, c.8), finalidad y RAT (b.3), relacion con la ACE (a.9, b.4), disposiciones y medidas de seguridad ACE (b.5, b.7), transferencias (c.5, c.6, c.7) y prohibiciones (b.6).
- La Normativa PAS Art. 41 aclara que tambien se sancionan las prohibiciones del Art. 59 LPDP, y que la clasificacion en leves, graves y muy graves se hace "segun la gravedad del dano ocasionado". Ademas, el Art. 32 inc. 2 obliga a la autoridad a considerar "la especial proteccion juridica" de los datos sensibles al calificar la falta y graduar la sancion.
- Ninguna infraccion del Art. 56 sanciona por si misma la falta de delegado, de RAT o de EIPD; esas omisiones entran por la via de b.5 y b.7 (no implementar medidas, lineamientos o medidas de seguridad de la ACE), lo que hace critica la trazabilidad de que disposicion de la ACE exige cada control.

---

## 4. (b) Multas del Art. 57 LPDP y salario minimo vigente

### 4.1 Texto legal

LPDP Art. 57 (literal): "Sin perjuicio de las responsabilidades penales a que diere lugar, las infracciones determinadas en la presente ley seran sancionadas con las siguientes multas: a) Las infracciones leves se sancionaran con multa de uno hasta un maximo de diez salarios minimos mensuales vigentes del sector comercio. b) Las infracciones graves se sancionaran con multa de once hasta un maximo de veinticinco salarios minimos mensuales vigentes del sector comercio. c) Las infracciones muy graves se sancionaran con multa de veintiseis hasta un maximo de cuarenta salarios minimos mensuales vigentes del sector comercio."

La Normativa PAS Art. 42 se remite a esas mismas multas y el Art. 43 fija los parametros de graduacion (seccion 6.10).

### 4.2 Salario minimo del sector comercio y servicios vigente en 2026

- Instrumento: Decreto Ejecutivo No. 11, Organo Ejecutivo en el Ramo de Trabajo y Prevision Social, "Tarifas de Salarios Minimos para la Republica de El Salvador", dado el 22 de mayo de 2025, con base en la propuesta del Consejo Nacional de Salario Minimo (organo tripartito, Codigo de Trabajo Arts. 144 y 149). Reformado por Decreto Ejecutivo No. 12 del 24 de mayo de 2025, publicado en el D.O. No. 96, Tomo 447, del 26 de mayo de 2025 (dato que consta en el texto consolidado oficial). Publicacion del D.E. 11: D.O. No. 95, Tomo 447, 23 de mayo de 2025 (numero de D.O. segun fuentes secundarias: Consortium Legal, Contaportable).
- Art. 2 (tabla unica): "Comercio y servicios: $408.80" mensual, "$13.440" por jornada diaria, "$1.680" por hora. Industria, ingenios azucareros y agroindustria tambien $408.80; maquila textil y confeccion $402.32; beneficios de cafe $305.23; sector agropecuario $272.53.
- Art. 15: "El presente Decreto entrara en vigencia el dia uno de junio de dos mil veinticinco, previa su publicacion en el Diario Oficial, el cual debera ser revisado posteriormente conforme a lo establecido en el Art. 159 del Codigo de Trabajo". Art. 14 deroga los Decretos Ejecutivos 9 y 10 del 7 de julio de 2021 (que fijaban US$365.00 para comercio y servicios desde el 1 de agosto de 2021).
- 2026: no se localizo ningun decreto de salario minimo emitido en 2026. Fuentes secundarias (EY, alerta "El Salvador Salario minimo 2026"; MTPS, nota del 25 de abril de 2025) confirman que en 2026 continuan vigentes los montos de junio de 2025 y que la siguiente revision ordinaria seria en 2028. Fuente oficial del valor: PDF del Decreto 11 en https://www.jurisprudencia.gob.sv/DocumentosBoveda/D/2/2020-2029/2025/05/10A4DA.PDF (consultado 2026-09-23).

### 4.3 Rangos en dolares con el salario vigente (US$408.80)

| Categoria | Salarios minimos | Minimo USD | Maximo USD |
|---|---|---|---|
| Leve (Art. 57 lit. a) | 1 a 10 | 408.80 | 4,088.00 |
| Grave (Art. 57 lit. b) | 11 a 25 | 4,496.80 | 10,220.00 |
| Muy grave (Art. 57 lit. c) | 26 a 40 | 10,628.80 | 16,352.00 |

Calculo: 408.80 x 1 = 408.80; x 10 = 4,088.00; x 11 = 4,496.80; x 25 = 10,220.00; x 26 = 10,628.80; x 40 = 16,352.00.

Rangos con el salario anterior (US$365.00, vigente del 1 de agosto de 2021 al 31 de mayo de 2025): leves 365.00 a 3,650.00; graves 4,015.00 a 9,125.00; muy graves 9,490.00 a 14,600.00.

### 4.4 Por que difieren las cifras de prensa y cual es correcta

| Cifra que circula | Origen verificado | Explicacion |
|---|---|---|
| "$365 a $3,650" | Editorial de elsalvador.com del 22 de enero de 2025 (fuente secundaria): "Las sanciones por infracciones leves oscilan entre 1 y 10 salarios minimos del sector comercio, lo que equivale a un rango de $365 a $3,650"; graves "$4,015 y $9,125"; muy graves "$9,490 y $14,600". Tambien nota de elsalvador.com de noviembre de 2024 titulada "Hasta $14,600 de multa" | Correcta para su fecha: usa el SM de US$365 vigente hasta el 31 de mayo de 2025 y se limita a las leves en la primera frase. Hoy esta desactualizada |
| "$408 a $16,352" | Aritmetica con el SM actual: 1 x 408.80 = 408.80 y 40 x 408.80 = 16,352.00. No se localizo una nota de prensa con esa cifra exacta; corresponde al rango completo de la ley (leve minima a muy grave maxima) con el SM de junio de 2025 | Correcta al 2026-09-23 (el "$408" redondea los centavos). Es la que debe usar el software mientras no cambie el decreto de salario minimo |
| "hasta $152,000" | Nota de elsalvador.com del 9 de marzo de 2021 sobre un proyecto de ley de proteccion de datos discutido por la legislatura anterior (fuente secundaria) | No corresponde al Art. 57 del Decreto 144 de 2024. Con el tope legal de 40 SM la multa maxima es US$16,352.00; US$152,000 equivaldria a unos 372 SM actuales o 416 SM de 2021, muy por encima del tope. Tampoco coincide con la LCSI (maximo 100 SM = US$40,880.00). Debe descartarse |

Conclusion: la escala correcta es la del Art. 57 LPDP expresada en salarios minimos, y su valor monetario depende del decreto de salario minimo vigente. Al 2026-09-23: US$408.80 a US$16,352.00. El software debe almacenar la tabla de salarios minimos con fechas de vigencia y recalcular automaticamente, y no debe presentar cifras fijas en dolares como si fueran la ley.

Punto para abogado (I-1): la ley dice "salarios minimos mensuales vigentes"; no precisa si se toma el SM vigente al momento de la infraccion o al momento de la resolucion. El principio de irretroactividad de la LPA (Art. 139 num. 3) apunta a las normas vigentes al producirse los hechos, pero el SM es un valor de referencia, no una norma sancionadora. El software deberia mostrar ambas cifras cuando difieran.

### 4.5 Comparativa con la LCSI (por si el mismo hecho se investiga bajo ambas leyes)

LCSI Art. 22: leves, amonestacion escrita o multa de 1 a 10 SM. Art. 23: graves, multa de 11 a 50 SM (para el sector privado). Art. 24: muy graves, multa de 51 a 100 SM (para el sector privado; el texto oficial dice por error "Las infracciones graves"). Art. 27: multa coercitiva de 1 a 10 SM "por cada dia habil que transcurra sin que se cumpla con lo ordenado", independiente y compatible con las demas sanciones. La LPDP no contiene multa coercitiva propia; la Normativa PAS tampoco la menciona. Si la ACE pretendiera aplicarla por remision del Art. 53 LPDP, es un punto para abogado (I-2). La LPA Art. 145 prohibe la doble sancion cuando hay identidad de sujeto, hecho y fundamento.

---

## 5. (c) Medidas adicionales, prohibiciones, publicidad, responsabilidad civil y penal

### 5.1 Medidas adicionales (LPDP Art. 58; Normativa PAS Arts. 37 y 38)

LPDP Art. 58 (literal): "Determinada la procedencia de la sancion, la Agencia podra ordenar al infractor o el sujeto obligado relacionado que adopte las medidas que fueren necesarias para restablecer la legalidad alterada por la infraccion o que permita la correccion de los derechos o las situaciones vulneradas. Todas las sanciones determinadas en la presente ley no eximen al infractor de las responsabilidades civiles o penales derivadas de las investigaciones correspondientes a que dieren lugar."

Normativa PAS Art. 37 repite la facultad y Art. 38 (literal): "La ACE, a traves de la Direccion de Proteccion de Datos Personales, dara seguimiento a la ejecucion de las medidas correctivas ordenadas, mediante requerimientos de cumplimiento, inspecciones o auditorias, segun corresponda." El Art. 32 inc. 1 exige que la resolucion final incluya "las medidas correctivas que permitan el restablecimiento de derechos o situaciones vulneradas de conformidad a lo senalado en el articulo 58 de la LPDP".

Notese que la medida puede dirigirse tambien al "sujeto obligado relacionado" (por ejemplo, un encargado o receptor), no solo al infractor.

Implicacion: el software necesita un "plan de medidas correctivas ordenadas por la ACE" con tareas, responsables, plazos, evidencia de ejecucion y preparacion de respuestas a requerimientos de seguimiento e inspecciones.

### 5.2 Prohibiciones (LPDP Art. 59)

Texto literal: "Queda prohibido a los sujetos obligados por la presente ley lo siguiente: a) Crear bases de datos que contengan datos personales sensibles, en contravencion a lo dispuesto en la presente ley o la normativa aplicable para tales efectos. b) El tratamiento de datos personales que revelen el origen racial o etnico, nacionalidad, afiliacion partidaria, convicciones religiosas, espirituales o filosoficas, asi como los relativos a la salud, la vida y la orientacion sexual, sin observar lo establecido en el capitulo IV del Titulo II de esta ley o la normativa aplicable para tales efectos. c) Revelar, difundir o comercializar por cualquier medio los datos personales que ha tenido acceso con ocasion de su cargo, sin observar los requisitos que establece esta ley o la normativa aplicable para tales efectos. d) Utilizar, transferir, compartir y comercializar a cualquier titulo y destino la informacion de las personas que conste en sus bancos de datos, bases de datos, repositorios, sistemas o registros, tanto manuales como informaticos, en contravencion a lo dispuesto en la presente ley o la normativa aplicable para tales efectos."

Incurrir en cualquiera de ellas es infraccion grave (Art. 56 lit. b num. 6), aunque varias conductas coinciden con muy graves (c.6 y c.7); la LPA Arts. 143 y 144 (concurso de normas y de infracciones) resuelven la calificacion. Mapeo al software: lit. a) y b) al modulo Datos sensibles (inventario de bases con datos sensibles, base juridica y consentimiento escrito, Arts. 37 y 38); lit. c) a la politica de confidencialidad del personal, acuerdos de confidencialidad y bitacora de accesos; lit. d) al modulo Transferencias y a la matriz de usos permitidos por base de datos.

### 5.3 Publicidad de las resoluciones (LPDP Art. 55; Normativa PAS Art. 46)

LPDP Art. 55 (literal): "Todas las resoluciones emitidas por la ACE respecto a la imposicion de sanciones de conformidad con la presente ley seran difundidas publicamente en su sitio web, en versiones publicas, siempre y cuando los datos personales sean disociados o anonimizados." La Normativa PAS Art. 46 precisa que se trata de las "resoluciones finales". Al 2026-09-23 no se localizo en ace.gob.sv ninguna resolucion sancionatoria publicada (busqueda web; la ACE es de creacion reciente y la Normativa PAS entro en vigencia el 19 de agosto de 2026).

Implicacion: riesgo reputacional adicional a la multa. El software puede mantener un observatorio de resoluciones publicadas por la ACE para calibrar riesgos (RECOMENDADO), y preparar a la empresa para que la version publica no contenga datos personales de titulares.

### 5.4 Responsabilidad civil y penal

- LPDP Art. 57 inc. 1 ("Sin perjuicio de las responsabilidades penales") y Art. 58 inc. 2 (las sanciones "no eximen al infractor de las responsabilidades civiles o penales").
- Normativa PAS Art. 34 (literal): "Dictada la resolucion final que imponga una sancion por la autoridad competente, esta se ejecutara sin perjuicio que la ACE interponga aviso a la Fiscalia General de la Republica por el cometimiento de un ilicito penal. El aviso debera interponerse en el plazo de setenta y dos horas."
- LPA Art. 145 inc. final: si durante el procedimiento el instructor considera que los hechos pueden ser ilicito penal, se ponen en conocimiento de la FGR. LPA Art. 155: la resolucion puede ademas ordenar la reposicion de la situacion alterada y declarar la indemnizacion por danos y perjuicios a la Administracion o a terceros, determinable por el mismo organo o, si no, por la via judicial.
- LPA Art. 142 inc. final: cuando el responsable es persona juridica, el juicio de culpabilidad se hace respecto de las personas fisicas que formaron su voluntad, sin que estas puedan ser sancionadas por la misma infraccion.
- No se analizaron los tipos penales del Codigo Penal ni de la Ley Especial contra Delitos Informaticos: fuera del alcance de este lente (I-6).

Implicacion: la evidencia generada por el software puede servir tambien en sede civil o penal; debe ser integra, fechada y atribuible a personas.

---

## 6. (d) Normativa para el Desarrollo del Procedimiento Administrativo Sancionador (ACE)

Fuente primaria: D.O. No. 146, Tomo 452, 11 de agosto de 2026, paginas 22 a 29. OCR local `fuentes/normativa_sancionadora_OCR.txt`; todos los plazos y textos citados abajo fueron cotejados contra las imagenes `page-03.png`, `page-04.png`, `page-06.png`, `page-08.png` y `page-09.png`. Fecha de emision: 24 de julio de 2026. Firmante: Eduardo Alexis Rodriguez Rodriguez, Director General de la ACE. Base habilitante invocada: LPDP Arts. 50 lit. a), b) y c) y 60; LPA Art. 159 (potestad normativa).

### 6.1 Estructura

```
CAPITULO I    Disposiciones generales                         Arts. 1-3
CAPITULO II   Principios, derechos y etapas                   Arts. 4-6
CAPITULO III  Diligencias preliminares de investigacion       Arts. 7-12
CAPITULO IV   Autoridad competente y delegacion               Arts. 13-14
CAPITULO V    Del inicio del procedimiento                    Arts. 15-23
CAPITULO VI   De la prueba                                    Arts. 24-28
CAPITULO VII  Alegatos finales, resolucion final y recursos   Arts. 29-34
CAPITULO VIII De las medidas provisionales                    Arts. 35-38
CAPITULO IX   Suspension del plazo y del procedimiento        Arts. 39-40
CAPITULO X    De las infracciones y sanciones                 Arts. 41-46
CAPITULO XI   Disposiciones finales                           Arts. 47-49
```

Objeto (Art. 1): desarrollar el procedimiento del Art. 53 LPDP "sin perjuicio de lo prescrito en la LPA, en lo aplicable". Ambito (Art. 2): todos los sujetos obligados del Art. 2 LPDP que incurran en las infracciones del "Titulo IV, Capitulo II" de la ley (sic; las infracciones estan en el Capitulo III del Titulo IV; error de cita menor, I-4).

### 6.2 Principios y etapas (Arts. 4 a 6)

Art. 4 (literal, verificado en imagen): "El procedimiento administrativo sancionador para la determinacion de las infracciones y sanciones previstas en la LPDP se llevara a cabo mediante el procedimiento simplificado contemplado en el articulo 158 de la LPA y, excepcionalmente, por la via del procedimiento ordinario previsto en la misma normativa."

Art. 5: garantias de audiencia, defensa y debido proceso; principios de legalidad, tipicidad, proporcionalidad y responsabilidad; principios generales de la LPA.

Art. 6: etapas: resolucion de inicio, contestacion, termino de prueba y resolucion final; conclusion extraordinaria posible; en via ordinaria se agrega la etapa de alegatos finales.

### 6.3 Diligencias preliminares de investigacion (Arts. 7 a 12)

- Finalidad (Art. 7): verificar indicios razonables, identificar posibles infractores; de ellas no puede derivar por si misma una sancion.
- Presupuestos (Art. 8): a) de oficio; b) por denuncia o aviso; c) "por haber sido solicitadas por los sujetos obligados como consecuencia de un incidente"; d) de forma preventiva, con base en riesgos. El DPDP prescinde de la investigacion preliminar cuando la denuncia ya provee elementos suficientes.
- Informe de apertura (Art. 9) y facultades (Art. 10, literal): "la Agencia podra requerir informes o antecedentes, el requerimiento de informacion a otras dependencias, inspecciones o verificaciones tecnicas, entrevistas o declaraciones informativas, el analisis documental o pericial y cualquier otra diligencia [...] De cada acto de investigacion realizado quedara un registro en audio, video o por escrito."
- Informe de resultados (Art. 11): apertura del procedimiento o archivo.
- Plazo (Art. 12, verificado): "maximo de noventa dias habiles, prorrogables de conformidad a lo establecido en la LPA, mediante resolucion motivada", contados desde el dia habil siguiente al informe de apertura.

Observacion para el producto: el literal c) del Art. 8 abre la posibilidad de que la propia empresa solicite diligencias tras un incidente; es una decision juridica que debe tomar con abogado, pero el software debe poder documentar el incidente con la calidad necesaria para esa eventualidad.

### 6.4 Autoridad competente y delegacion (Arts. 13 y 14)

Autoridad: el Director de Proteccion de Datos Personales (Art. 13; LPDP Art. 51). Puede delegar la instruccion y sustanciacion en el Director Juridico u otro empleado o funcionario de la ACE distinto del Director General, reservandose la imposicion de la sancion (Art. 14). La delegacion se formaliza por acuerdo o resolucion y las resoluciones del delegado deben ir precedidas por las frases "[...] actuando por delegacion de [...]" y "Mediante acuerdo o resolucion administrativa [...]". Utilidad practica: permite a la empresa verificar la competencia de quien firma cada acto.

### 6.5 Inicio del procedimiento y denuncia (Arts. 15 a 18)

- Formas de inicio (Art. 15): de oficio, por denuncia, por aviso, por cualquier otro medio. Si la informacion se recibe verbalmente, la ACE levanta acta.
- Requisitos de la denuncia (Art. 16): a) organo o funcionario al que se dirige; b) nombre y generales del titular, domicilio, lugar y medio tecnico para notificaciones y, en su caso, del representante (si la presenta un particular, sus datos personales); c) relacion de los hechos tipificados como infraccion; d) identificacion de los presuntos responsables, si fuera posible; e) peticion en terminos precisos; f) firma por cualquier medio legalmente permitido; g) lugar y fecha; h) demas exigencias legales. Puede presentarse personalmente o por apoderado, "ya sea por escrito o a traves de cualquier medio tecnologico habilitado por la Agencia". Si actua apoderado, se acompanan los documentos de personeria.
- Resolucion de inicio (Art. 17) y contenido minimo (Art. 18): identificacion de denunciantes y presuntos responsables, relacion sucinta de hechos y elementos recabados, calificacion preliminar de la infraccion con su base legal y sancion correspondiente, indicacion del derecho a alegar y probar, requerimiento de senalar lugar y correo electronico para notificaciones. Coincide con la LPA Art. 151.

### 6.6 Emplazamiento, contestacion, actuaciones preliminares y allanamiento (Arts. 19 a 23)

- Emplazamiento personal (Art. 19): a la persona juridica, por medio de su titular, representante legal o apoderado en sus sedes; si no se encuentran, por esquela dejada con cualquier empleado. Se busca a la persona juridica "en la direccion de sus oficinas principales registradas en la base de datos de la Agencia" o en cualquier otra fuente idonea. Notificaciones posteriores en la direccion o medio electronico designado; supletoriamente LPA Art. 98. Notificacion por edicto en diario de circulacion nacional y tablero de la ACE si no es posible de otro modo (Art. 20).
- Contestacion (Art. 21, verificado): "en el plazo de cinco dias habiles contados a partir del dia siguiente habil de la notificacion"; en ese termino se presentan alegatos, documentos y la proposicion de prueba. Si no comparece, "se tendran por contestados negativamente los hechos" y el procedimiento continua.
- Actuaciones preliminares (Art. 22, verificado en imagen): subsanacion de deficiencias, aportacion de documentos u otros elementos, "dentro del plazo de cinco dias habiles contados a partir del dia siguiente habil de la notificacion de inicio del procedimiento".
- Aceptacion de los hechos y allanamiento (Art. 23): en cualquier etapa; se omiten las etapas no agotadas; el delegado remite el expediente al DPDP en 5 dias habiles y este dicta resolucion final en maximo 15 dias habiles. Concuerda con LPA Art. 156: la aceptacion expresa y por escrito es atenuante y, si la sancion es pecuniaria, "se podran aplicar reducciones de hasta una cuarta parte de su importe".

### 6.7 Prueba (Arts. 24 a 28)

- Art. 24 (literal en lo esencial): el presunto infractor "podra aportar cualquier elemento probatorio de descargo admisible en derecho", con aplicacion supletoria del Codigo Procesal Civil y Mercantil; valoracion conforme a la sana critica. Son prueba "los instrumentos publicos, los autenticos, los instrumentos privados, las declaraciones de testigos, los resultados de peritajes, la inspeccion de los lugares o de las cosas, la confesion, los informes de auditoria internos o externos, cualquier otra informacion que hubiese sido proporcionada por el presunto infractor a la Agencia u obtenida por esta ultima en el transcurso de las investigaciones y actuaciones preliminares, las presunciones legales y cualquier otro medio admisible en derecho".
- Art. 25 (verificado): en via ordinaria, inspeccion, compulsa, peritaje o agregacion de prueba por instrumentos se ordenan de inmediato en el termino probatorio, con posible suspension del plazo (LPA Art. 90). En via simplificada, el presunto infractor puede pedir inspeccion o peritaje "al momento de la contestacion". Peritos propuestos por los interesados, nombrados y juramentados por la autoridad.
- Arts. 26 y 27: actuaciones oportunas (informes preceptivos, pruebas y consultas tecnicas) y consulta tecnica a otros organos.
- Art. 28: consulta del expediente en la sede de la ACE, con acta; fotocopias solo con autorizacion; en cualquier etapa previa a los alegatos finales.

### 6.8 Alegatos finales, resolucion final, recursos y acciones posteriores (Arts. 29 a 34)

- Alegatos finales (Art. 29): solo en via ordinaria, 10 dias habiles, limitados a los hechos e infracciones de la resolucion de inicio.
- Remision del expediente (Art. 30): el delegado instructor remite el expediente con informe al DPDP "dentro del plazo maximo de ocho dias habiles".
- Cambio a via ordinaria (Art. 31): por resolucion motivada, "debido a la complejidad de las infracciones o de las alegaciones", con 5 dias habiles para alegaciones; se sujeta a la LPA.
- Resolucion final (Art. 32): "en el plazo de quince dias habiles posteriores a la recepcion del expediente"; motivada; resuelve todas las cuestiones, valora la prueba, fija la sancion "de acuerdo con la gravedad y proporcionalidad" y las medidas correctivas del Art. 58 LPDP. Datos sensibles: consideracion especial. En via simplificada: "no habra recurso alguno y quedara habilitada la via contencioso-administrativa".
- Recursos (Art. 33): en via ordinaria, reconsideracion, apelacion y revision "dentro de los plazos senalados y conforme a lo establecido en la LPA"; contra la resolucion final de apelacion y revision no cabe recurso y queda la via contencioso-administrativa.
- Acciones posteriores (Art. 34): ejecucion de la sancion y aviso a la FGR en 72 horas si hay ilicito penal.

### 6.9 Medidas provisionales y suspension (Arts. 35, 36, 39, 40)

- Art. 35 (verificado): en caso de urgencia o riesgo grave, medidas provisionales antes de iniciar el procedimiento o durante el, por resolucion motivada (urgencia, necesidad, razonabilidad, proporcionalidad, temporalidad). Las previas "deberan ser confirmadas, modificadas o dejadas sin efecto al dictarse el auto de inicio correspondiente, el cual debera emitirse dentro de los quince dias calendario siguientes a la adopcion de dichas medidas. Estas ultimas, quedaran sin efecto si no se inicia el procedimiento en el plazo senalado o cuando en la resolucion de inicio no se realice ningun pronunciamiento expreso acerca de ellas."
- Art. 36: en cualquier etapa; modificables de oficio o a instancia de parte; se extinguen con la resolucion que pone fin al procedimiento. Base legal: LPDP Art. 50 lit. c) y LPA Art. 152.
- Art. 39: suspension del plazo maximo para resolver en los casos del LPA Art. 90 (requerimiento de subsanacion al interesado; informes preceptivos de otro organo, maximo dos meses; pruebas tecnicas o analisis, maximo dos meses; actuaciones complementarias); la resolucion de suspension no admite recurso. Art. 40: suspension del procedimiento por caso fortuito o fuerza mayor (LPA Art. 94).

### 6.10 Infracciones, multas, criterios de graduacion, pago y ejecucion (Arts. 41 a 46)

- Art. 41: infracciones y prohibiciones son las de los Arts. 56 y 59 LPDP, clasificadas "segun la gravedad del dano ocasionado".
- Art. 42: multas del Art. 57 LPDP, sin perjuicio de responsabilidad penal.
- Art. 43 (literal, verificado en imagen page-09.png): "Para la imposicion de una multa, la autoridad competente debera tener en cuenta los siguientes aspectos: a) la gravedad del dano o del probable peligro a quienes resulten afectados por la infraccion cometida, b) el efecto disuasivo en el infractor respecto de la conducta infractora, c) la duracion de la conducta infractora, d) caracter intencional o negligente del infractor, e) naturaleza o categoria de los datos personales afectados y f) la capacidad economica del infractor, considerando para ello cualquier medio idoneo."
- Art. 44: pago en la Colecturia Central u oficinas regionales de la Direccion General de Tesoreria del Ministerio de Hacienda "dentro de los quince dias habiles siguientes a la notificacion respectiva", con mandamiento de pago del DPDP.
- Art. 45: si no paga, la FGR, a peticion del DPDP, la hace efectiva por la via ejecutiva (Ley Organica de la FGR Art. 18 lit. i); la certificacion de la resolucion tiene fuerza ejecutiva.
- Art. 46: versiones publicas en el sitio web (ver 5.3).

### 6.11 Prescripcion, supletoriedad y vigencia (Arts. 47 a 49)

- Art. 47 (literal, verificado): "Las infracciones y sanciones contempladas en la LPDP prescribiran en el plazo de cinco anos y las reglas para determinar el computo de la prescripcion se regiran de acuerdo con lo senalado en el articulo 149 de la LPA."
- Art. 48: supletoriedad de la LPDP, la LCSI, la LPA y otras leyes especiales.
- Art. 49: vigencia ocho dias despues de su publicacion en el Diario Oficial (publicada el 11 de agosto de 2026; vigente desde el 19 de agosto de 2026).

### 6.12 Linea de tiempo consolidada del procedimiento

```
Hecho -> denuncia / aviso / oficio / solicitud del propio sujeto obligado (Art. 8 y 15)
   |
   v
Informe de apertura de diligencias preliminares (Art. 9)   [se omite si la denuncia basta, Art. 8 inc. final]
   |   requerimientos, inspecciones, entrevistas, pericias (Art. 10)
   |   maximo 90 dias habiles, prorrogables (Art. 12)
   v
Informe de resultados (Art. 11) ----> archivo
   |
   v
Resolucion de inicio + emplazamiento personal (Arts. 17 a 19)
   |   [medidas provisionales previas deben confirmarse aqui; auto de inicio en 15 dias calendario, Art. 35]
   |   5 dias habiles: contestar, alegar, proponer prueba, actuaciones preliminares (Arts. 21 y 22)
   |   [en via simplificada, pedir inspeccion o peritaje al contestar, Art. 25]
   v
Actuaciones oportunas y prueba (Arts. 24 a 27)   [suspension del plazo: LPA Art. 90]
   |
   |-- via ordinaria (Art. 31): alegatos finales 10 dias habiles (Art. 29)
   |
   |-- allanamiento en cualquier etapa (Art. 23): remision 5 dias habiles, resolucion 15 dias habiles
   v
Remision del expediente por el delegado: maximo 8 dias habiles (Art. 30)
   |
   v
Resolucion final del DPDP: 15 dias habiles (Art. 32)  -> medidas adicionales (Arts. 37 y 38)
   |                                                    -> version publica (Art. 46)
   |                                                    -> aviso a FGR en 72 horas si hay delito (Art. 34)
   |
   |-- via simplificada: sin recurso administrativo; contencioso-administrativo (Art. 32 inc. 3)
   |-- via ordinaria: reconsideracion 10 dias (LPA 133), apelacion 15 dias (LPA 135),
   |                  revision extraordinaria (LPA 136 y 137) (Art. 33)
   v
Pago de la multa: 15 dias habiles (Art. 44) -> si no, FGR via ejecutiva (Art. 45)
```

Tabla de plazos para el motor de plazos del software:

| Evento | Plazo | Tipo de dias | Fuente |
|---|---|---|---|
| Diligencias preliminares | 90, prorrogables | habiles | Normativa PAS Art. 12 |
| Auto de inicio tras medidas provisionales previas | 15 | calendario | Art. 35 |
| Contestar emplazamiento, alegar, proponer prueba | 5 | habiles | Arts. 19 y 21; LPA Art. 158 num. 2 |
| Actuaciones preliminares (subsanar, aportar) | 5 | habiles | Art. 22 |
| Alegaciones tras cambio a via ordinaria | 5 | habiles | Art. 31; LPA Art. 158 num. 4 |
| Alegatos finales (solo via ordinaria) | 10 | habiles | Art. 29 |
| Remision del expediente por el delegado | 8 | habiles | Art. 30 |
| Remision en caso de allanamiento | 5 | habiles | Art. 23 |
| Resolucion final | 15 | habiles | Arts. 23 y 32; LPA Art. 158 num. 4 ("quince dias") |
| Aviso a la FGR | 72 horas | horas | Art. 34 |
| Pago de la multa | 15 | habiles | Art. 44 |
| Recurso de reconsideracion (via ordinaria) | 10 | dias (LPA) | LPA Art. 133 |
| Recurso de apelacion (via ordinaria) | 15 | dias (LPA) | LPA Art. 135 |
| Revision extraordinaria | 1 ano (error de hecho) o 3 meses (documentos nuevos) | segun LPA | LPA Art. 137 |
| Suspension por informes o pruebas tecnicas | maximo 2 meses cada causa | meses | LPA Art. 90 |
| Prescripcion de infracciones y sanciones | 5 anos | anos | Normativa PAS Art. 47; LCSI Art. 29 |

Punto para abogado (I-5): los plazos de la LPA se expresan en "dias" sin calificar; el computo de dias habiles o calendario para los recursos debe confirmarse con la regla general de computo de plazos de la LPA.

---

## 7. (e) Reglas que aporta la LCSI por remision del Art. 53 LPDP, y la LPA supletoria

LPDP Art. 53 (literal): "Para el ejercicio de potestad sancionadora, el desarrollo del procedimiento y las reglas de prescripcion de las infracciones y sanciones contemplada en la presente ley se aplicara lo dispuesto en la Ley de Ciberseguridad y Seguridad de la Informacion."

Contenido relevante de la LCSI (Decreto 143), Capitulo III "Infracciones, sanciones, procedimientos y recursos":

- Art. 17: responsabilidad por accion u omision, a titulo de dolo, culpa o cualquier otro titulo; aplicacion de los principios de la potestad sancionadora de la LPA, "especialmente el de proporcionalidad".
- Art. 26: medidas adicionales, identico al Art. 58 LPDP.
- Art. 27: multa coercitiva de 1 a 10 SM por dia habil de incumplimiento de lo ordenado (ver I-2 sobre su aplicabilidad a la LPDP).
- Art. 28 (literal): "El procedimiento para la determinacion de las infracciones y sanciones que establece la presente ley debera realizarse de conformidad con el procedimiento simplificado contemplado en la Ley de Procedimientos Administrativos. El procedimiento podra iniciarse de oficio, por aviso, por denuncia o por cualquier otro medio. Cuando la informacion sobre la presunta comision de la infraccion se recibiera de forma verbal o de tal manera que no hubiera un respaldo escrito de la misma, la Agencia levantara un acta con todos los datos pertinentes para la tramitacion del procedimiento."
- Art. 29 (literal): "Las infracciones y sanciones contempladas en la presente ley prescribiran a los cinco anos."
- Art. 30: la LPA es supletoria.

La LCSI NO contiene criterios de graduacion propios (ni tamano de empresa, ni reincidencia), ni reglas de computo de la prescripcion, ni regimen de recursos propio. Por eso la Normativa PAS toma el plazo de cinco anos y remite el computo a la LPA Art. 149.

Reglas de la LPA que completan el sistema (texto oficial consolidado de la Asamblea Legislativa):

- Art. 139: principios de reserva de ley, tipicidad (los reglamentos pueden "desarrollar o introducir especificaciones" pero no crear infracciones ni alterar limites), irretroactividad, presuncion de inocencia, responsabilidad, prohibicion de doble sancion y proporcionalidad ("de las infracciones tipificadas no resulte mas beneficio para el infractor que el cumplimiento de las normas infringidas").
- Art. 140: derechos del presunto responsable (ser informado de la imputacion, alegar y probar, no declarar contra si mismo).
- Art. 142: autoria de personas naturales o juridicas; cooperadores necesarios; quienes incumplen un deber legal de prevenir la infraccion de otro.
- Arts. 143 y 144: concurso de normas y de infracciones.
- Art. 145: non bis in idem y comunicacion a la FGR.
- Art. 148: plazos de prescripcion por defecto (muy graves 3 anos, graves 2, leves 6 meses; sanciones 3, 2 y 1) que NO aplican a la LPDP porque la norma especial fija cinco anos.
- Art. 149 (literal): "El plazo de prescripcion de las infracciones comenzara a contarse desde el dia siguiente a aquel en que se hubiera cometido la infraccion. En los casos de infraccion realizada de forma continuada o permanente, tal plazo se comenzara a contar desde el dia en que se realizo el ultimo hecho constitutivo de la infraccion o desde que se elimino la situacion ilicita. Interrumpira la prescripcion de la infraccion la iniciacion, con conocimiento del presunto responsable, del procedimiento administrativo. La prescripcion se reanudara, por la totalidad del plazo, desde el dia siguiente a aquel en que se cumpla un mes de paralizacion del procedimiento por causa no imputable al presunto responsable. El plazo de prescripcion de las sanciones comenzara a contarse desde el dia siguiente a aquel en que adquiera firmeza, en via administrativa, la resolucion por la que se impone la sancion. Interrumpira la prescripcion de la sancion la iniciacion, con conocimiento del sancionado, del procedimiento de ejecucion."
- Art. 150: contenido de la denuncia de particular (datos personales del denunciante, relato sucinto de los hechos, identificacion de presuntos responsables).
- Art. 151: auto de inicio. Art. 152: medidas provisionales. Art. 153: prueba. Art. 154: resolucion motivada y congruente. Art. 155: reposicion e indemnizacion. Art. 156: aceptacion de responsabilidad como atenuante, reduccion de hasta una cuarta parte de la multa. Art. 157: apercibimiento en lugar de procedimiento, solo si una ley lo autoriza, para infracciones leves y si el infractor "no hubiese sido sancionado o apercibido con anterioridad" (la LPDP no contiene esa autorizacion expresa, I-7).
- Art. 158: procedimiento simplificado (inicio por resolucion; 5 dias para actuaciones preliminares, alegaciones y proposicion de prueba; actuaciones oportunas y prueba; resolucion definitiva en 15 dias desde la ultima actuacion; posible paso a ordinario con 5 dias de alegaciones; sin recurso administrativo, via contencioso-administrativa).
- Arts. 132 a 137: reconsideracion (10 dias, resuelve en un mes), apelacion (15 dias ante el superior jerarquico, admision en 5 dias, prueba 5 dias, resuelve en un mes) y revision extraordinaria (causales tasadas; 1 ano o 3 meses segun causal).
- Art. 90: causas de suspension del plazo para resolver. Art. 94: suspension del procedimiento por caso fortuito o fuerza mayor. Art. 98: reglas de notificacion (cualquier medio con constancia de recepcion, fecha y contenido; acreditacion en el expediente).

Consecuencia practica de la infraccion continuada (LPA Art. 149): una omision que persiste (por ejemplo, un aviso de privacidad incompleto que sigue publicado, o un tratamiento que continua tras la revocacion) no empieza a prescribir hasta que cesa. El software debe registrar la fecha de cese o correccion de cada incumplimiento detectado, porque esa fecha es la que inicia el computo.

---

## 8. (f) Como denuncia un titular y que documentacion pedira la ACE a la empresa

### 8.1 Vias de denuncia previstas en la LPDP

- Art. 9 inc. 3 (rectificacion): "El incumplimiento de esta obligacion dentro del plazo determinado habilitara al interesado para presentar la denuncia correspondiente ante la Entidad Rectora a efecto de que se garanticen sus derechos."
- Art. 31 (revocacion): "En caso de negativa por parte del responsable a tramitar la revocacion del consentimiento, el titular, sin perjuicio de otras acciones que conforme al ordenamiento juridico pudiera ejercer, podra presentar su denuncia ante la Entidad Rectora de la presente ley."
- Art. 50 lit. s): la ACE asiste y asesora a los ciudadanos sobre los medios legales de defensa. Art. 50 lit. f): resuelve controversias sobre clasificacion de datos sensibles.
- Con caracter general, cualquier infraccion del Art. 56 puede denunciarse (Normativa PAS Arts. 8 lit. b, 15 lit. b y 16; LCSI Art. 28; LPA Art. 150). El delegado de proteccion de datos tambien puede poner en conocimiento de la ACE hechos del responsable o del encargado que pudieran constituir infraccion (Lineamientos del Delegado Art. 23; OCR, confianza media).
- Reforma DL 659 (pendiente de publicacion): segun la nota oficial de la Asamblea, las solicitudes ARCO-POL se presentan directamente ante la empresa y la ACE conserva la supervision; no se menciona ningun cambio al regimen de denuncias ni de sanciones.

### 8.2 Canal y formularios de la ACE

- Pagina de formularios (https://ace.gob.sv/page/formularios, consultada 2026-09-23): ocho formularios, todos con fecha 07/07/2025: Acceso, Rectificacion, Cancelacion o Supresion, Oposicion, Portabilidad, Olvido, Limitacion del Tratamiento y Nombramiento de Delegado. No existe un formulario de denuncia ante la ACE por incumplimiento de la LPDP.
- Los formularios ARCO-POL de la ACE (por ejemplo `fuentes/ace_form_acceso.txt`) incluyen esta advertencia: "En caso de que se inicie la sustanciacion de un proceso ante la Agencia de Ciberseguridad del Estado, dicha entidad podra requerir informacion adicional a las partes involucradas, con el fin de contar con los elementos necesarios para el adecuado analisis y resolucion de este." Es decir, la solicitud ARCO-POL y su tramitacion interna son el primer documento que la ACE pedira.
- Pagina de contacto (https://ace.gob.sv/page/contacto): telefono (503) 7530-6114, horario lunes a viernes 8:00 a 16:00 y emergencias 24/7, correos institucionales de contacto general, emergencias ciberneticas y soporte (las direcciones exactas no pudieron capturarse con las herramientas disponibles; verificar en la pagina) y un formulario web con opciones "Reporte de Incidente", "Vulnerabilidad Detectada", "Solicitud de Capacitacion", "Asesoria Tecnica" y "Cooperacion Interinstitucional". La Normativa PAS Art. 16 permite la denuncia "a traves de cualquier medio tecnologico habilitado por la Agencia", por lo que ese formulario o correo puede ser la via mientras no exista formulario especifico.
- Politicas de Actuacion ACE Art. 5 lit. c): las entidades deben tener "Mecanismos de Denuncia: Vias para que los titulares reporten incumplimientos o violaciones de seguridad". Es una obligacion interna de la empresa (canal propio de quejas), distinta de la denuncia ante la ACE.

### 8.3 Que pedira la ACE a la empresa: el paquete de evidencia

Base legal: LPDP Art. 50 lit. t) (literal): "Solicitar a las entidades publicas y privadas la informacion referida a los antecedentes, documentos, programas u otros elementos relativos al tratamiento de los datos personales, garantizando la integridad, seguridad y confidencialidad de la informacion y elementos suministrados." Complementos: Art. 50 lit. a) (controlar, inspeccionar, supervisar), Art. 54 (carga de la prueba), Art. 25 inc. final (documentacion de vulneraciones "a disposicion de la autoridad"), Art. 33 (procedimientos ARCO-POL documentados), Normativa PAS Arts. 10, 24 y 38, y Art. 56 lit. a) num. 9 y lit. b) num. 4 (sancion por no atender u obstaculizar).

Contenido probable del requerimiento, derivado de esas normas (no existe una lista oficial publicada; esto es inferencia razonada):

| Bloque de evidencia | Norma que lo hace exigible | Que debe poder generar el software |
|---|---|---|
| Solicitud ARCO-POL o revocacion origen de la denuncia y su expediente interno completo | Arts. 9, 18 a 23, 29 a 31, 33 | Expediente por solicitud: fecha y hora de recepcion, canal, documentos del titular, prevencion, prorroga motivada, resolucion, notificaciones con acuse, costos cobrados, comunicaciones a receptores y encargados |
| Prueba del consentimiento del titular y de la comunicacion del aviso de privacidad | Arts. 24, 26, 27, 54 | Registro de consentimiento por titular: fecha, medio, texto, version del aviso, firma o equivalente; para datos sensibles, documento firmado |
| Aviso y politica de privacidad vigentes en la fecha de los hechos | Arts. 7 y 24 | Historial de versiones con fechas de publicacion y puntos de captura donde se mostro |
| Procedimientos ARCO-POL documentados | Art. 33 | Documento versionado y aprobado, con fecha |
| Registro de actividades de tratamiento, bases de licitud y finalidades | Politicas ACE Art. 4 lit. d); Art. 5 lit. c) LPDP (finalidad) | RAT exportable con fecha de corte |
| Contratos con encargados y receptores; registro de transferencias; comunicaciones a la ACE de flujos transfronterizos | Arts. 34, 41, 44, 45, 54 inc. 2 | Inventario de contratos y transferencias con documentos adjuntos |
| Documentacion de vulneraciones de seguridad y notificaciones realizadas | Art. 25 | Bitacora de cada incidente y constancias de notificacion a la ACE, FGR y titulares con fecha y hora |
| Medidas de seguridad implementadas y su verificacion | Art. 36; Politicas ACE Arts. 4, 5 y 8 | Lista de controles con evidencia (capturas, certificados, informes de pentesting, backups, capacitaciones) y fecha de ultima verificacion |
| Informes de auditoria internos o externos | Normativa PAS Art. 24; Politicas ACE Art. 8 lit. b) | Informes de auditoria anual y planes de accion |
| Nombramiento y actuaciones del delegado (mientras la reforma no derogue la obligacion en el sector privado) | Arts. 15 y 16; Lineamientos del Delegado | Acuerdo de nombramiento, comunicacion a la ACE, registro de actuaciones |
| Matriz de accesos autorizados a bases de datos | Art. 5 lit. f); Art. 56 lit. a) num. 4 | Listado de accesos autorizados y bitacora de cambios |
| Registro de requerimientos anteriores de la ACE y respuestas | Art. 50 lit. t); Art. 56 lit. a) num. 9 | Expediente de relacion con la autoridad |

Plazo de referencia: los 5 dias habiles del emplazamiento (Normativa PAS Arts. 19 y 21) son el limite realista para reunir el paquete; en las diligencias preliminares (Art. 10) el plazo lo fija cada requerimiento. El software debe permitir generar el paquete "a una fecha" (estado de la evidencia en la fecha de los hechos) y no solo el estado actual.

---

## 9. (g) Reincidencia y agravantes: que existe y que registros conviene mantener

Hallazgo principal: ni la LPDP, ni la LCSI, ni la Normativa PAS ni la LPA contienen una regla de "reincidencia en 2 anos" ni criterios de "tamano de la empresa", "participacion" o "condicion del afectado" como agravantes tasados. Lo que si existe:

1. Normativa PAS Art. 43: gravedad del dano o peligro, efecto disuasivo, duracion de la conducta, caracter intencional o negligente, naturaleza o categoria de los datos (datos sensibles con proteccion especial, Art. 32 inc. 2) y capacidad economica. El "efecto disuasivo" y la "capacidad economica" permiten a la autoridad ponderar el historial y el tamano economico del infractor sin que sean criterios expresos.
2. LPA Art. 156: aceptacion expresa y escrita de responsabilidad como atenuante, con reduccion de hasta una cuarta parte de la multa.
3. LPA Art. 157: apercibimiento en lugar de procedimiento solo para infracciones leves y solo si el infractor "no hubiese sido sancionado o apercibido con anterioridad" (requiere autorizacion legal expresa, que la LPDP no contiene; I-7).
4. LPA Art. 145: una sancion o pena previa por los mismos hechos con fundamento parcialmente coincidente se toma en cuenta "para graduar en sentido atenuante".
5. Lineamientos del Delegado (OCR): no puede ser delegado quien haya sido "sancionado, mediante resolucion firme, por infracciones a la LPDP" (requisito del cargo; confianza media por OCR). Un historial de sanciones afecta por tanto la elegibilidad de personas para el rol.
6. LCSI Art. 22 inc. 2: tres o mas amonestaciones escritas en menos de un ano provocan la desvinculacion del funcionario o empleado publico (solo sector publico; no aplica a la LPDP).
7. LPA Art. 149: la infraccion continuada o permanente prolonga el inicio del computo de la prescripcion; y Art. 43 lit. c) de la Normativa PAS convierte la "duracion de la conducta" en agravante. Corregir rapido reduce la exposicion.

Registros que la empresa deberia mantener (RECOMENDADO, salvo donde se indica base expresa):

- Registro de sanciones firmes, apercibimientos, medidas provisionales y medidas adicionales recibidas de la ACE, con fecha de firmeza, infraccion, monto, medidas ordenadas y evidencia de cumplimiento (sirve para LPA Arts. 145, 156 y 157 y para acreditar cumplimiento de medidas, Normativa PAS Art. 38).
- Registro de requerimientos e inspecciones de la ACE con fechas de respuesta (evita a.9 y b.4).
- Fechas de deteccion y de cese de cada incumplimiento detectado internamente (para acreditar "duracion" corta e intencionalidad ausente; LPA Art. 149).
- Evidencia de diligencia: capacitaciones, auditorias, planes de accion cerrados, EIPD, actualizaciones de politicas (acredita caracter negligente vs. diligente; Politicas ACE Arts. 4 y 8).
- Categorizacion de datos por sensibilidad en el RAT (criterio e) del Art. 43).
- Informacion financiera basica que la empresa este dispuesta a acreditar como "capacidad economica" (criterio f), decision del cliente con abogado.

---

## 10. (h) Implicaciones para el diseno de la evidencia y la auditoria del software

1. Evidencia con fecha cierta y trazabilidad de autor: cada registro relevante (consentimiento, aviso mostrado, solicitud ARCO-POL, notificacion, incidente, acceso autorizado) debe tener fecha y hora, usuario que lo creo, y no poder alterarse sin dejar rastro (Art. 56 a.6 sanciona modificar el documento de consentimiento; Art. 54 pone la carga de la prueba en el responsable; Normativa PAS Art. 24 admite instrumentos privados y "cualquier otra informacion" aportada por el presunto infractor, cuya credibilidad dependera de su integridad).
2. Vista "a fecha": la ACE juzgara los hechos con las normas y versiones vigentes en ese momento (LPA Art. 139 num. 3). El software debe reconstruir que aviso, que politica, que procedimiento, que matriz de accesos y que consentimiento estaban vigentes en una fecha dada.
3. Paquete de evidencia exportable: generacion en horas, no en dias, del conjunto descrito en 8.3, con indice, fechas y responsable, para responder en 5 dias habiles. Incluir la posibilidad de marcar que documentos son confidenciales (Art. 50 lit. t) obliga a la ACE a garantizar confidencialidad).
4. Motor de plazos del procedimiento sancionador: cuando la empresa reciba un emplazamiento, el software debe crear un expediente con los plazos de la seccion 6.12 (dias habiles salvadorenos, con calendario de feriados mantenido), tareas para el abogado externo y bitacora de cada notificacion recibida (LPA Art. 98: la acreditacion de la notificacion va al expediente; conviene guardar copia).
5. Verificacion de competencia y forma: campo para registrar quien firma cada acto de la ACE y si actua por delegacion (Normativa PAS Art. 14), util para el abogado.
6. Registro de decisiones juridicas del cliente: allanamiento (Normativa PAS Art. 23; LPA Art. 156), solicitud de inspeccion o peritaje al contestar (Art. 25 inc. final), solicitud de diligencias tras un incidente (Art. 8 lit. c), recursos (Art. 33). El software no decide; documenta la decision, quien la tomo y cuando.
7. Calculo de exposicion: tabla de salarios minimos con vigencias (hoy US$408.80 desde el 1 de junio de 2025), rangos por categoria, y "estimacion orientativa" por infraccion detectada, siempre etiquetada como orientativa y nunca como determinacion de la sancion, porque la graduacion es de la ACE (Art. 43). Mostrar ambos valores si el SM cambio entre la fecha del hecho y la fecha actual (I-1).
8. Retencion: conservar la evidencia de cumplimiento al menos 5 anos desde el ultimo hecho relevante (prescripcion; Normativa PAS Art. 47; LPA Art. 149) y, si hay procedimiento, hasta la firmeza y ejecucion completa (LPA Art. 147). Coordinar con el principio de temporalidad (LPDP Art. 5 lit. h): se conserva la evidencia de cumplimiento, no necesariamente los datos personales tratados; cuando la evidencia contenga datos personales, valorar seudonimizacion.
9. Auditoria interna y externa como prueba: la Normativa PAS Art. 24 nombra expresamente "los informes de auditoria internos o externos". El modulo de auditoria debe producir informes fechados, con alcance, hallazgos, plan de accion y cierre, alineados con las auditorias anuales de la Politica ACE Art. 8 lit. b).
10. Medidas correctivas ordenadas: modulo de seguimiento de medidas adicionales (Art. 58 LPDP; Normativa PAS Arts. 37 y 38) con evidencia de cumplimiento lista para "requerimientos de cumplimiento, inspecciones o auditorias".
11. Observatorio normativo: la version publica de las resoluciones de la ACE (Art. 55; Normativa PAS Art. 46) sera la principal fuente de criterio practico sobre graduacion; el producto deberia incorporarlas como contenido orientativo cuando existan.
12. Limites del software: nunca afirmar "cumple" o "no cumple" con valor juridico; cada control se muestra como "evidencia disponible / no disponible" y "plazo cumplido / vencido", con enlace a la norma.

---

## 11. Bloques de obligaciones

### B-01 Prohibiciones del Art. 59
**Norma:** LPDP. **Articulo:** 59 (con 56 lit. b num. 6). **Obligacion:** No crear bases con datos sensibles en contravencion de la ley; no tratar datos sensibles sin observar el Capitulo IV del Titulo II; no revelar, difundir ni comercializar datos conocidos por el cargo; no usar, transferir, compartir ni comercializar la informacion de sus bases en contravencion de la ley. **A quien aplica:** todos los sujetos obligados. **Implicacion para el software:** modulo Datos sensibles y Transferencias con base juridica registrada antes de crear una base o autorizar un flujo; bitacora de comunicaciones de datos. **Fuente oficial:** `fuentes/ace_decreto_144.txt` (2026-09-23). **Vigencia:** VIGENTE. **Clasificacion:** OBLIGATORIO.

### B-02 Atender los requerimientos de informacion de la ACE
**Norma:** LPDP. **Articulo:** 50 lit. t) y 56 lit. a) num. 9. **Obligacion:** Entregar a la ACE antecedentes, documentos, programas y otros elementos relativos al tratamiento cuando los solicite. **A quien aplica:** entidades publicas y privadas. **Implicacion para el software:** expediente de requerimientos con plazo, responsable, respuesta y acuse; generador del paquete de evidencia. **Fuente oficial:** `fuentes/ace_decreto_144.txt`. **Vigencia:** VIGENTE. **Clasificacion:** OBLIGATORIO.

### B-03 No obstaculizar auditorias, inspecciones y seguimiento de la ACE
**Norma:** LPDP y Normativa PAS. **Articulo:** LPDP 50 lit. a) y 56 lit. b) num. 4; Normativa PAS Arts. 10 y 38. **Obligacion:** Permitir y facilitar auditorias, inspecciones, verificaciones tecnicas y requerimientos de cumplimiento. **A quien aplica:** sujetos obligados. **Implicacion para el software:** protocolo de atencion de inspecciones, interlocutor designado, acta interna y entrega documentada. **Fuente oficial:** `fuentes/ace_decreto_144.txt`; `fuentes/ocr/normativa_sancionadora/page-03.png` y `page-08.png`. **Vigencia:** VIGENTE. **Clasificacion:** OBLIGATORIO.

### B-04 Conservar la prueba del consentimiento y de la comunicacion del aviso
**Norma:** LPDP. **Articulo:** 54 (con 26, 27 y 24). **Obligacion:** El responsable carga con la prueba del consentimiento y de la comunicacion de la politica o aviso de privacidad; en transferencias internacionales, con la prueba de que se hicieron conforme a la ley. **A quien aplica:** responsables. **Implicacion para el software:** registro inmutable de consentimientos y de avisos comunicados por titular; registro de transferencias con analisis y contrato. **Fuente oficial:** `fuentes/ace_decreto_144.txt`. **Vigencia:** VIGENTE. **Clasificacion:** OBLIGATORIO.

### B-05 Documentar y notificar vulneraciones (72 horas)
**Norma:** LPDP. **Articulo:** 25 (sancion en 56 lit. a num. 3). **Obligacion:** Notificar a la ACE, la FGR y los titulares en maximo 72 horas y documentar toda vulneracion a disposicion de la autoridad. **A quien aplica:** responsables. **Implicacion para el software:** modulo de incidentes con reloj de 72 horas, constancias de envio y bitacora de la vulneracion. **Fuente oficial:** `fuentes/ace_decreto_144.txt`. **Vigencia:** VIGENTE. **Clasificacion:** OBLIGATORIO (detalle en el lente de incidentes).

### B-06 Implementar medidas, lineamientos y medidas de seguridad de la ACE
**Norma:** LPDP y Politicas de Actuacion ACE N. 001-0309025-DPDP. **Articulo:** LPDP 35, 36, 50 lit. i) y n), 60; 56 lit. b) num. 5 y 7; Politicas ACE Arts. 4, 5 y 8. **Obligacion:** Acatar y mantener las medidas de seguridad y lineamientos de la ACE (organizativas, tecnicas, fisicas, de transferencia; auditorias anuales). **A quien aplica:** responsables y encargados. **Implicacion para el software:** catalogo de disposiciones ACE con controles derivados y evidencia por control. **Fuente oficial:** `fuentes/ace_decreto_144.txt`; `fuentes/ace_politicas_protecciondatos.txt`; https://ace.gob.sv/politicas.php. **Vigencia:** VIGENTE (fecha de emision de la politica pendiente de verificar). **Clasificacion:** OBLIGATORIO.

### B-07 Mecanismo interno de denuncia para titulares
**Norma:** Politicas de Actuacion ACE. **Articulo:** Art. 5 lit. c). **Obligacion:** Disponer de vias para que los titulares reporten incumplimientos o violaciones de seguridad. **A quien aplica:** entidades obligadas. **Implicacion para el software:** canal de quejas del titular integrado al modulo ARCO-POL e Incidentes, con acuse y seguimiento. **Fuente oficial:** `fuentes/ace_politicas_protecciondatos.txt`. **Vigencia:** VIGENTE. **Clasificacion:** OBLIGATORIO segun politica de actuacion (no es texto de ley; su exigibilidad se canaliza por el Art. 56 lit. b num. 5 y 7).

### B-08 Contestar el emplazamiento en 5 dias habiles
**Norma:** Normativa PAS (y LPA). **Articulo:** Normativa PAS Arts. 19, 21 y 22; LPA Art. 158 num. 2. **Obligacion:** Contestar, alegar, aportar documentos, proponer prueba y realizar actuaciones preliminares dentro de 5 dias habiles desde el dia habil siguiente a la notificacion; si no, los hechos se tienen por contestados negativamente. **A quien aplica:** presunto infractor emplazado. **Implicacion para el software:** expediente sancionador con reloj de 5 dias habiles y generacion del paquete de evidencia. **Fuente oficial:** `fuentes/ocr/normativa_sancionadora/page-05.png` y `page-06.png`. **Vigencia:** VIGENTE desde 19 ago 2026. **Clasificacion:** CONDICIONAL (solo si se abre procedimiento).

### B-09 Pedir inspeccion o peritaje al contestar (via simplificada)
**Norma:** Normativa PAS. **Articulo:** 25 inc. final. **Obligacion:** En via simplificada, la solicitud de inspeccion o peritaje debe hacerse "al momento de la contestacion". **A quien aplica:** presunto infractor. **Implicacion para el software:** recordatorio en la tarea de contestacion; registro de la decision. **Fuente oficial:** `page-06.png`. **Vigencia:** VIGENTE. **Clasificacion:** CONDICIONAL.

### B-10 Cumplir medidas provisionales
**Norma:** LPDP, Normativa PAS, LPA. **Articulo:** LPDP 50 lit. c); Normativa PAS Arts. 35 y 36; LPA Art. 152. **Obligacion:** Acatar las medidas provisionales dictadas antes o durante el procedimiento hasta que se modifiquen, se dejen sin efecto o se extingan con la resolucion final. **A quien aplica:** sujeto obligado destinatario. **Implicacion para el software:** registro de la medida, fecha, alcance, tareas de cumplimiento y control del plazo de 15 dias calendario para el auto de inicio cuando la medida fue previa. **Fuente oficial:** `page-08.png`; LPA texto oficial Asamblea. **Vigencia:** VIGENTE. **Clasificacion:** CONDICIONAL.

### B-11 Pagar la multa en 15 dias habiles
**Norma:** Normativa PAS. **Articulo:** 44 y 45. **Obligacion:** Pagar en la Colecturia Central u oficinas regionales de la DGT del Ministerio de Hacienda dentro de 15 dias habiles desde la notificacion; si no, cobro ejecutivo por la FGR. **A quien aplica:** sujeto sancionado. **Implicacion para el software:** tarea con plazo y adjunto del mandamiento de pago y comprobante. **Fuente oficial:** `page-09.png`. **Vigencia:** VIGENTE. **Clasificacion:** CONDICIONAL.

### B-12 Ejecutar medidas adicionales y someterse al seguimiento
**Norma:** LPDP y Normativa PAS. **Articulo:** LPDP 58; Normativa PAS 32, 37 y 38. **Obligacion:** Adoptar las medidas ordenadas para restablecer la legalidad o corregir derechos vulnerados; atender requerimientos de cumplimiento, inspecciones o auditorias de seguimiento. **A quien aplica:** infractor o sujeto obligado relacionado. **Implicacion para el software:** plan de medidas correctivas con evidencia de ejecucion. **Fuente oficial:** `fuentes/ace_decreto_144.txt`; `page-08.png`. **Vigencia:** VIGENTE. **Clasificacion:** CONDICIONAL.

### B-13 Interponer recursos en plazo (via ordinaria)
**Norma:** Normativa PAS y LPA. **Articulo:** Normativa PAS 33; LPA 133 (10 dias), 135 (15 dias), 136 y 137. **Obligacion:** Si se quiere impugnar en sede administrativa una resolucion dictada en via ordinaria, hacerlo en los plazos de la LPA; en via simplificada no hay recurso administrativo y queda la via contencioso-administrativa (Normativa PAS 32 inc. 3; LPA 158 num. 5). **A quien aplica:** sancionado. **Implicacion para el software:** alertas de plazo y registro de la decision del cliente con su abogado; el plazo contencioso-administrativo debe confirmarse con abogado (I-5). **Fuente oficial:** `page-08.png`; LPA texto oficial. **Vigencia:** VIGENTE. **Clasificacion:** CONDICIONAL.

### B-14 Registro de sanciones, apercibimientos y medidas previas
**Norma:** LPA (y Lineamientos del Delegado). **Articulo:** LPA 145, 156 y 157; Lineamientos del Delegado, requisito de no haber sido sancionado por infracciones a la LPDP. **Obligacion:** No existe obligacion expresa de llevar este registro; es la base factica de atenuantes y de elegibilidad del delegado. **A quien aplica:** empresa. **Implicacion para el software:** registro de antecedentes con la ACE. **Fuente oficial:** LPA texto oficial; `fuentes/lineamientos_dpo_OCR.txt`. **Vigencia:** VIGENTE. **Clasificacion:** RECOMENDADO.

### B-15 Conservar la evidencia de cumplimiento al menos cinco anos
**Norma:** Normativa PAS, LCSI y LPA. **Articulo:** Normativa PAS 47; LCSI 29; LPA 147 y 149. **Obligacion:** No es un plazo de conservacion expreso; deriva de que las infracciones y sanciones prescriben a los cinco anos, computados desde el dia siguiente a la comision o desde el cese de la conducta continuada, con interrupcion por el inicio del procedimiento. **A quien aplica:** empresa. **Implicacion para el software:** politica de retencion de evidencia de 5 anos desde el ultimo hecho, extendida durante procedimientos abiertos; seudonimizar datos personales contenidos en la evidencia cuando sea posible. **Fuente oficial:** `page-09.png`; Decreto 143 PDF Asamblea; LPA texto oficial. **Vigencia:** VIGENTE. **Clasificacion:** RECOMENDADO.

### B-16 Cesar el tratamiento tras la revocacion (5 dias habiles)
**Norma:** LPDP. **Articulo:** 29, 30 y 31 (sancion en 56 lit. c num. 9 y 10). **Obligacion:** Habilitar mecanismos expeditos, sencillos y gratuitos de revocacion; proceder en 5 dias habiles e informar al encargado en 5 dias habiles. **A quien aplica:** responsables (y el delegado mientras no rija la reforma). **Implicacion para el software:** modulo de revocaciones con tareas de cese y constancia. **Fuente oficial:** `fuentes/ace_decreto_144.txt`. **Vigencia:** VIGENTE (Art. 30 podria verse afectado por la reforma pendiente en cuanto al sujeto que tramita). **Clasificacion:** OBLIGATORIO.

### B-17 Requisitos de la denuncia del titular
**Norma:** Normativa PAS y LPA. **Articulo:** Normativa PAS 15 y 16; LPA 150. **Obligacion:** (Hecho relevante para la empresa, no obligacion propia) La denuncia debe identificar al denunciante, relatar los hechos tipificados, identificar a los presuntos responsables si es posible, formular peticion precisa y estar firmada; puede presentarse por escrito o por medio tecnologico habilitado por la ACE. **A quien aplica:** titular o particular denunciante. **Implicacion para el software:** el modulo ARCO-POL debe dejar al titular y a la empresa un expediente que, si termina en denuncia, ya contenga esos elementos de forma ordenada. **Fuente oficial:** `page-05.png`; LPA texto oficial. **Vigencia:** VIGENTE. **Clasificacion:** HECHO (informativo).

### B-18 Calculo de la multa en salarios minimos
**Norma:** LPDP y Decreto Ejecutivo 11 de 2025. **Articulo:** LPDP 57; D.E. 11 Art. 2 y 15. **Obligacion:** (Hecho) Las multas se expresan en SM del sector comercio; el SM vigente es US$408.80 desde el 1 de junio de 2025 y no hay decreto nuevo en 2026. **A quien aplica:** todos. **Implicacion para el software:** tabla de SM con vigencias y recalculo automatico; etiquetar toda estimacion como orientativa. **Fuente oficial:** `fuentes/ace_decreto_144.txt`; https://www.jurisprudencia.gob.sv/DocumentosBoveda/D/2/2020-2029/2025/05/10A4DA.PDF. **Vigencia:** VIGENTE. **Clasificacion:** HECHO.

---

## 12. Incertidumbres y puntos que requieren abogado

- I-1. "Salarios minimos mensuales vigentes": si se toma el SM vigente al momento del hecho o al de la resolucion. Recomendar mostrar ambos valores.
- I-2. Multa coercitiva de la LCSI (Art. 27): no esta en la LPDP ni en la Normativa PAS; su aplicabilidad por remision del Art. 53 LPDP es dudosa (principio de tipicidad, LPA Art. 139 num. 2). Requiere criterio juridico.
- I-3. Art. 56 lit. a) num. 2 sanciona "no publicar los datos de contacto del encargado del tratamiento"; la redaccion es ambigua (encargado, responsable o delegado). Con la reforma DL 659 (delegado ya no obligatorio en el sector privado, segun fuentes secundarias) el contacto exigible sera el de la empresa; confirmar con el texto oficial del decreto cuando se publique.
- I-4. Normativa PAS Art. 2 cita el "Titulo IV, Capitulo II" de la LPDP para las infracciones, cuando estas estan en el Capitulo III. Error de cita sin efectos practicos previsibles, pero conviene tenerlo presente en una eventual defensa.
- I-5. Computo de los plazos de la LPA para recursos (dias habiles o calendario) y plazo para acudir a la jurisdiccion contencioso-administrativa (Ley de la Jurisdiccion Contencioso Administrativa, no analizada aqui).
- I-6. Tipos penales aplicables (Codigo Penal, Ley Especial contra Delitos Informaticos y Conexos): no analizados; el Art. 34 de la Normativa PAS obliga a la ACE a avisar a la FGR en 72 horas cuando aprecie un ilicito penal.
- I-7. Apercibimiento del LPA Art. 157: requiere que "una Ley lo autorice"; la LPDP no lo hace expresamente. Si la ACE lo usara como practica, seria una via de salida para infracciones leves de primerizos. Confirmar criterio de la ACE cuando existan resoluciones publicadas.
- I-8. Criterios de graduacion mencionados en el encargo (tamano de empresa, participacion, condicion del afectado, reincidencia en 2 anos): no existen en fuente primaria. Si provienen de una guia o borrador de la ACE no publicado, debe localizarse; mientras tanto no se incorporan.
- I-9. Reforma DL 659: texto oficial no localizado; publicacion en el D.O. no confirmada al 2026-09-23. Todo lo relativo a delegado, Art. 16, 30 y 51 debe releerse cuando se publique. La nota oficial no anuncia cambios en sanciones ni procedimiento.
- I-10. Numero exacto del Diario Oficial de publicacion del D.E. 11 de 2025 (No. 95, Tomo 447, 23 de mayo de 2025) se tomo de fuentes secundarias; el valor de US$408.80 y la vigencia desde el 1 de junio de 2025 constan en el texto oficial consolidado.
- I-11. Correos electronicos de la ACE para denuncias: existen en la pagina de contacto pero no pudieron transcribirse con las herramientas usadas; la ACE no ha publicado formulario de denuncia. Verificar el canal antes de orientar a un titular.
- I-12. Fecha de emision y publicacion de las Politicas de Actuacion N. 001-0309025-DPDP: pendiente (lente de politicas ACE).
- I-13. Todo lo citado de `lineamientos_dpo_OCR.txt` y de `normativa_sancionadora_OCR.txt` que no se verifico contra imagen (Arts. 16 a 21, 23, 26 a 34, 36 a 46 de la Normativa PAS se leyeron en OCR y en las imagenes de las paginas 5, 6, 8 y 9; los Arts. 1 a 3 en OCR y pagina 2) tiene confianza alta; el pasaje de los Lineamientos sobre el requisito de no haber sido sancionado tiene confianza media.

---

## 13. Fuentes consultadas (todas al 2026-09-23)

Fuentes primarias:
- LPDP, Decreto Legislativo 144: `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt` (copia ACE) y `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\diario_oficial_2024-11-15_mh.txt` (D.O. 219, Tomo 445). Tambien https://www.asamblea.gob.sv/sites/default/files/documents/decretos/7A4FBD85-7E1B-46BE-9408-6FC549E53E00.pdf
- LCSI, Decreto Legislativo 143: https://www.asamblea.gob.sv/sites/default/files/documents/decretos/D056D9A1-299D-4188-941A-9C3B5898D3F3.pdf (texto extraido localmente del PDF oficial).
- LPA, Decreto Legislativo 856, texto consolidado: https://www.asamblea.gob.sv/sites/default/files/documents/decretos/361DDB77-97E7-4EFF-B353-C6D872547E7C.pdf (texto extraido localmente).
- Normativa PAS (ACE), D.O. 146, Tomo 452, 11 ago 2026: `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\normativa_sancionadora_OCR.txt` e imagenes `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ocr\normativa_sancionadora\page-02.png` a `page-09.png`.
- Lineamientos para el Delegado (ACE): `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\lineamientos_dpo_OCR.txt`.
- Politicas de Actuacion ACE N. 001-0309025-DPDP: `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_politicas_protecciondatos.txt`; https://ace.gob.sv/politicas.php
- Formularios ACE: https://ace.gob.sv/page/formularios ; `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_form_acceso.txt`, `ace_form_cancelacion.txt`, `ace_form_portabilidad.txt`, `ace_form_nombramiento_delegado.txt`.
- Contacto ACE: https://ace.gob.sv/page/contacto
- Decreto Ejecutivo 11 de 2025 (salario minimo), texto consolidado con reforma del D.E. 12: https://www.jurisprudencia.gob.sv/DocumentosBoveda/D/2/2020-2029/2025/05/10A4DA.PDF
- Nota oficial de la Asamblea sobre la reforma de septiembre de 2026: https://www.asamblea.gob.sv/node/14116
- Dictamen 11 de 2024 (historia legislativa; confirma que la escala de multas del Art. 57 viene del proyecto original): `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\dictamen_11_2024_ley_original_OCR.txt`.

Fuentes secundarias (orientacion; marcadas como tales en el texto):
- EY, "El Salvador | Salario minimo 2026": https://www.ey.com/es_ce/technical/tax/tax-alerts/el-salvador-salario-minimo-2026
- MTPS, nota del 25 de abril de 2025 sobre el aumento del 12%: https://www.mtps.gob.sv/2025/04/25/408-80-seria-nuevo-salario-minimo-en-industria-y-servicio-tras-incremento-del-12-anunciado-por-el-presidente-nayib-bukele/
- Consortium Legal, "Aprobacion de nuevos salarios minimos en El Salvador" (13 jun 2025): https://consortiumlegal.com/2025/06/13/aprobacion-de-nuevos-salarios-minimos-en-el-salvador/
- elsalvador.com, editorial "La Ley de Proteccion de Datos Personales" (22 ene 2025): https://elsalvador.com/opinion/editoriales/organizaciones-laborales-/1195558/2025
- elsalvador.com, "Hasta $14,600 de multa por infringir ley de datos personales" (nov 2024): https://www.elsalvador.com/h-noticias/h-nacional/hasta-14600-de-multa-por-infringir-ley-datos-personales/1182019/2024/
- elsalvador.com (historico), "Manejar datos personales sin consentimiento sera multado hasta con $152,000" (9 mar 2021): https://historico.elsalvador.com/historico/815034/tecnologia-asamblea-diputados-multas-ley-proteccion-datos.html
- Infobae, "Entran en vigor las multas por infraccion de datos en El Salvador..." (26 ago 2026): https://www.infobae.com/el-salvador/2026/08/26/entran-en-vigor-las-multas-por-infraccion-de-datos-en-el-salvador-calculadas-segun-la-gravedad-y-capacidad-economica/
- ECIJA, "Ley de proteccion de datos en El Salvador" (20 nov 2024): https://www.ecija.com/actualidad-insights/ley-de-proteccion-de-datos-en-el-salvador/
- Consortium Legal, "Delegado de Proteccion de Datos en El Salvador" (2 sep 2026): https://consortiumlegal.com/2026/09/02/delegado-proteccion-datos-el-salvador/
