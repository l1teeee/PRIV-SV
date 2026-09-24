# Sweep juridico: medidas de seguridad, documentacion obligatoria, RAT, EIPD, auditorias, capacitacion y delegado

Proyecto: PRIV-SV. Lente: seguridad, documentacion y delegado.
Fecha de consulta de todas las fuentes: 2026-09-23.
Autor: investigador juridico (agente). Este informe no sustituye asesoria legal.

Convenciones:
- LPDP = Ley para la Proteccion de Datos Personales, Decreto Legislativo N. 144 (D.O. N. 219, Tomo 445, 15 nov 2024, vigente desde 23 nov 2024).
- Politicas ACE = Politicas N. 001-0309025-DPDP "Politicas de Actuacion y Manejo de Datos Personales" (ACE).
- Lineamientos DPO = Lineamientos para el Delegado de Proteccion de Datos Personales (ACE, D.O. N. 146, Tomo 452, 11 ago 2026).
- Normativa PAS = Normativa para el Desarrollo del Procedimiento Administrativo Sancionador en el Ambito de la LPDP (ACE, mismo D.O.).
- Reforma 659 = Decreto Legislativo N. 659 aprobado el 17 sep 2026, publicacion en D.O. no confirmada al 23 sep 2026. Todo su contenido se cita "segun fuentes secundarias".
- Clasificacion: OBLIGATORIO, RECOMENDADO, CONDICIONAL. Se usa ademas la etiqueta OBLIGATORIO-DE-ALCANCE-INDETERMINADO (subtipo de OBLIGATORIO) cuando la norma manda algo pero no define contenido, formato, periodicidad ni umbral.

---

## 1. Resumen ejecutivo

1. Las Politicas ACE N. 001-0309025-DPDP son la unica norma secundaria vigente que concreta las "medidas de seguridad" de los Arts. 34 lit. b, 35 y 36 LPDP. Fueron emitidas por el Director General de la ACE; segun prensa (Diario El Mundo, 12 sep 2025) se emitieron el 2 de septiembre de 2025 y estan vigentes desde el 3 de septiembre de 2025. El numero del documento (03-09-025) y los metadatos del PDF oficial (creado el 4 sep 2025) son consistentes con esa fecha. No se ha podido confirmar su publicacion en el Diario Oficial; el documento no contiene clausula "DADO EN" ni fecha en su cuerpo.

2. Son juridicamente imperativas: el Art. 35 LPDP dice que las politicas de actuacion "seran imperativas a los sujetos obligados"; el Art. 34 lit. b obliga a "implementar las medidas de seguridad y cumplir con las politicas de actuacion"; el Art. 36 obliga a "acatar y mantener las medidas de seguridad establecidas por la Entidad Rectora" y extiende esa obligacion al encargado; y el Art. 56 lit. b numerales 5 y 7 tipifican como infraccion grave (multa de 11 a 25 salarios minimos del comercio, Art. 57 lit. b) no implementar las medidas o lineamientos de la ACE y no cumplir las medidas de seguridad de las politicas de actuacion.

3. El problema es su generalidad: las Politicas enumeran medidas en una o dos lineas cada una (RAT, EIPD, auditorias de cumplimiento, politica de proteccion de datos, capacitacion, 2FA, cifrado, backups, pentesting, "digitalizacion: usar sistemas especializados") sin definir contenido, formato, periodicidad, umbral de riesgo ni criterio de proporcionalidad. Por eso este informe las trata como OBLIGATORIO-DE-ALCANCE-INDETERMINADO: el mandato existe y es sancionable, pero el estandar de cumplimiento lo fijara la ACE caso por caso en inspecciones y procedimientos sancionadores. La unica medida con periodicidad expresa es la auditoria: "anuales" (Politicas Art. 8 lit. b). Para el software esto significa que debe ayudar a la empresa a documentar que hizo algo razonable y demostrable en cada rubro, sin afirmar que ese algo es "suficiente".

4. Los Lineamientos DPO (emitidos 24 jul 2026, D.O. 11 ago 2026, vigentes desde el 19 ago 2026 segun fuentes secundarias y contexto del proyecto) desarrollan en 42 articulos el perfil, nombramiento, registro, certificacion, formacion, independencia, informes y deberes ARCO-POL del delegado. Plazos verificados contra imagen del D.O.: 3 dias habiles para notificar al delegado su nombramiento (Art. 8); 15 dias habiles para comunicar el nombramiento a la ACE (Art. 10); 10 dias habiles para actualizar cambios en la plataforma (Art. 10); 15 dias habiles para que la ACE emita la credencial (Art. 12); 10 dias habiles para nombrar otro delegado si la ACE deniega la inscripcion (Art. 12) o ante cesacion (Art. 19); verificacion del perfil al menos cada 3 anos (Art. 18); capacitacion del delegado al menos una vez al ano y plan anual de capacitacion para el personal (Art. 22); informe al responsable al menos dos veces al ano (Art. 30); conservacion de la documentacion del aviso de privacidad por minimo 10 anos (Art. 31); notificacion de cada actuacion ARCO-POL en 3 dias habiles (Art. 33); confidencialidad que subsiste 5 anos tras el cese (Art. 36); comunicacion transitoria de nombramientos en 20 dias habiles desde la vigencia (Art. 40). La ACE dejo sin efecto la fecha limite del 16 sep 2026 (segun prensa del 12 sep 2026 que cita un comunicado de la ACE).

5. La reforma 659, si entra en vigencia, deroga los Arts. 15 y 17 LPDP y reforma el Art. 16: el delegado deja de ser obligatorio para el sector privado y sus funciones pasan a los "sujetos obligados". Los Lineamientos DPO fueron dictados sobre el Art. 15; para una empresa privada que no nombre delegado, el regimen de nombramiento, registro y certificacion pierde base. Sobreviven, porque descansan en articulos que la reforma no toca, las obligaciones de fondo: medidas de seguridad (Arts. 34-36), procedimientos ARCO-POL documentados (Art. 33), aviso y politica de privacidad (Art. 24), notificacion y registro de vulneraciones (Art. 25), contratos de transferencia (Art. 41), informacion a la ACE de flujos transfronterizos (Art. 45), publicacion de costos (Art. 23), carga de la prueba (Art. 54) y, por reenvio del Art. 16 reformado, formacion del personal, mecanismos de entrega segura y publicacion del aviso. La designacion voluntaria de un responsable interno de privacidad pasa a ser RECOMENDADO y ademas sigue siendo una medida organizativa de las Politicas ACE (Art. 4 lit. b y Art. 8 lit. a), cuyo destino tras la reforma requiere abogado.

6. Certificaciones, sellos y marcas (Art. 50 lit. j, k, l LPDP): no existen todavia. Lo unico publicado es el "Programa de Certificacion de Delegados de Proteccion de Datos Personales", que los Lineamientos anuncian pero que no ha entrado en vigencia. No se localizaron guias de implementacion (lit. n), clausulas contractuales modelo (lit. p) ni formulario de revocacion del consentimiento (lit. q). El inventario completo de lo publicado en ace.gob.sv esta en la seccion 8.

7. Para el diseno funcional, el activo central es el "expediente de evidencia": la Normativa PAS (Art. 24) reconoce como prueba en el procedimiento sancionador los instrumentos privados, los informes de auditoria internos o externos y cualquier informacion aportada a la ACE; el Art. 10 permite a la ACE requerir informes, inspecciones y verificaciones tecnicas; el Art. 38 da seguimiento a medidas correctivas mediante inspecciones o auditorias; el Art. 50 lit. t LPDP faculta a la ACE a pedir "antecedentes, documentos, programas u otros elementos relativos al tratamiento"; y el Art. 54 LPDP pone la carga de la prueba del consentimiento, del aviso y de las transferencias internacionales en el responsable.

---

## 2. Jerarquia de fuentes usada en este informe

```
LPDP (Decreto 144)                 -> ley, vigente desde 23 nov 2024
   |
   +-- Politicas ACE 001-0309025-DPDP  -> politica de actuacion, imperativa (Art. 35), vigente desde 3 sep 2025 (fuente secundaria)
   +-- Lineamientos DPO                -> lineamiento, obligatorio para delegado, encargado y responsable (Art. 3), vigente 19 ago 2026
   +-- Normativa PAS                   -> normativa procedimental sancionadora, vigente 19 ago 2026
   +-- Formularios ARCO-POL y de nombramiento (07-07-2025) -> modelos oficiales, estandar minimo (Lineamientos Art. 32)
   |
Reforma 659 (17 sep 2026)          -> APROBADA-PENDIENTE-PUBLICACION; contenido segun fuentes secundarias
Buenas practicas (ISO 27001, etc.) -> referencia citada por las Politicas, no obligatoria por si misma
```

---

## 3. Politicas N. 001-0309025-DPDP (Politicas de Actuacion y Manejo de Datos Personales)

### 3.1 Identificacion, fecha, publicacion y vigencia

| Dato | Valor | Fuente | Confianza |
|---|---|---|---|
| Titulo | "Politicas de Actuacion y Manejo de Datos Personales de la Ley para la Proteccion de Datos Personales" | ace_politicas_protecciondatos.txt, pag. 1 | Alta |
| Numero | 001-0309025-DPDP | Idem | Alta |
| Emisor | Director General de la ACE (Eduardo Alexis Rodriguez Rodriguez, segun prensa) | Idem pag. 1; Diario El Mundo 12 sep 2025 | Alta / media |
| Base legal invocada | Art. 50 lit. i LPDP (considerando II) | Idem pag. 1 | Alta |
| Fecha de emision | 2 de septiembre de 2025 | Diario El Mundo, 12 sep 2025 (fuente secundaria) | Media |
| Inicio de vigencia | 3 de septiembre de 2025 | Diario El Mundo, 12 sep 2025 (fuente secundaria); numero del documento "0309025" | Media |
| Metadatos del PDF oficial | CreationDate 2025-09-04 23:02 (hora -06:00), autor "Michelle Acosta", MS Word | ace_politicas_protecciondatos.pdf (lectura de metadatos) | Alta como dato tecnico |
| Publicacion en Diario Oficial | NO CONFIRMADA. El texto no tiene clausula "DADO EN", fecha ni numero de registro. Art. 9 dice "entraran en vigencia a partir de su publicacion" sin decir donde | ace_politicas_protecciondatos.txt pag. 6; busquedas web sin resultado | Baja |
| URL oficial | https://ace.gob.sv/documentos/politicas/politicas_protecciondatos.pdf (enlazado desde https://ace.gob.sv/politicas.php) | WebFetch 2026-09-23 | Alta |
| Plazo Art. 60 LPDP | La ACE debia dictarlas a mas tardar 3 meses desde la vigencia de la ley (aprox. 23 feb 2025); se emitieron con unos seis meses de retraso (La Prensa Grafica, 12 sep 2025, titular "con atraso segun expertos"; no se pudo leer el cuerpo, HTTP 403) | ace_decreto_144.txt Art. 60; titular de prensa | Media |
| Plazo de adecuacion de los sujetos obligados | 3 meses "a partir de la emision de las referidas disposiciones" (Art. 60 inc. 2): aproximadamente 2-3 de diciembre de 2025 si se toma el 2-3 sep 2025 como emision. Calculo propio, no confirmado por la ACE | ace_decreto_144.txt Art. 60 | Media |

Lectura del numero: "001" (primera politica), "0309025" (03-09-2025), "DPDP" (Direccion de Proteccion de Datos Personales). Es una interpretacion razonable y coincide con la fecha de prensa, pero no esta explicada en el documento.

### 3.2 Naturaleza juridica y fuerza vinculante

**Norma:** LPDP
**Articulo:** Art. 35; Art. 34 lit. b; Art. 36; Art. 56 lit. b num. 5 y 7; Art. 57 lit. b; Art. 50 lit. i; Art. 60
**Obligacion:** Cumplir las politicas de actuacion y las medidas de seguridad que dicte la ACE. Texto del Art. 35: "La Entidad Rectora dictara las politicas de actuacion y manejo de datos personales, las cuales seran imperativas a los sujetos obligados por la presente ley." Texto del Art. 36 inc. 1: "El responsable debera acatar y mantener las medidas de seguridad establecidas por la Entidad Rectora para el resguardo y el tratamiento de los datos personales y que garanticen el cumplimiento de las caracteristicas minimas de seguridad de la informacion, tales como integridad, disponibilidad y confidencialidad." Inc. 2: "El responsable debera aplicar los mecanismos tecnologicos, regulatorios y procedimentales que garanticen el cumplimiento de las caracteristicas de seguridad de informacion. Lo dispuesto en este articulo tambien sera de obligatorio cumplimiento para el encargado del tratamiento de datos personales." Infracciones graves Art. 56 lit. b: "5. No implementar las medidas, controles tecnicos o lineamientos que establezca la ACE en materia de proteccion de datos." y "7. No cumplir con las medidas de seguridad establecida en las politicas de actuacion emitidas por la Agencia."
**A quien aplica:** Responsables y encargados, publicos y privados (Art. 2 LPDP; Politicas Art. 2 y Art. 4).
**Implicacion para el software:** El modulo de cumplimiento debe tratar cada medida de las Politicas como un requisito con dueno, estado y evidencia, y mostrar la consecuencia sancionatoria (grave, 11-25 salarios minimos) como informacion, no como amenaza. Debe permitir que la empresa registre "no aplica" con justificacion, porque la ACE reconoce la implementacion "en lo que fuera aplicable" (Art. 50 lit. i y Politicas Art. 1).
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (Arts. 34-36, 56, 57), consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

Observacion sobre el rango: las Politicas son un acto administrativo normativo de la ACE, subordinado a la ley. No pueden crear obligaciones que la ley no habilite. La ley las habilita ampliamente (Arts. 35, 36, 50 lit. i, 60), pero un abogado debe evaluar si medidas como "nombrar delegado" sobreviven cuando la propia ley deje de exigir delegado al sector privado (seccion 4.14).

### 3.3 Estructura y transcripcion de los pasajes clave

Estructura: Considerandos I y II; Capitulo I Disposiciones generales (Art. 1 objeto, Art. 2 ambito, Art. 3 principios); Capitulo II Seguridad y proteccion (Art. 4 medidas, Art. 5 cumplimiento y supervision, Art. 6 resumen); Capitulo III Infracciones (Art. 7); Capitulo IV Implementacion y supervision (Art. 8 supervision y monitoreo, Art. 9 vigencia y actualizacion). Cada articulo lleva una referencia a controles ISO 27001 (numeracion de la version 2013).

Art. 2 (transcripcion): "Estas politicas son de cumplimiento obligatorio para todas las entidades publicas y privadas que recolecten, almacenen, procesen o transfieran datos personales en El Salvador. Tambien aplican a operaciones internacionales vinculadas a ciudadanos salvadorenos."

Art. 4 inc. 1 (transcripcion): "Segun la Ley para la Proteccion de Datos Personales de El Salvador, las medidas de seguridad buscan garantizar la integridad, disponibilidad y confidencialidad de la informacion. Estas medidas deben ser implementadas por los responsables y encargados del tratamiento de datos, y su incumplimiento puede llevar a sanciones."

Art. 4, Medidas Organizativas (transcripcion literal):
- "a) Politica de Proteccion de Datos: Establecer normas internas que regulen el manejo de los datos personales."
- "b) Delegado de Proteccion de Datos Personales (DPDP): Nombramiento de un responsable encargado de garantizar el cumplimiento de la normativa."
- "c) Capacitacion del Personal: Formacion continua sobre seguridad de datos."
- "d) Registro de Actividades de Tratamiento: Mantener un registro detallado de como se recopilan, almacenan y utilizan los datos personales."
- "e) Evaluaciones de Impacto en la Privacidad (EIPD): Identificacion y mitigacion de riesgos."
- "f) Auditorias de Cumplimiento: Verificacion periodica del cumplimiento de las medidas de seguridad."

Art. 4, Medidas Tecnicas (transcripcion literal):
- "a) Control de Acceso: Implementacion de contrasenas seguras, autenticacion en dos pasos (2FA) y acceso restringido."
- "b) Cifrado de Datos: Proteccion de la informacion tanto en almacenamiento como en transito."
- "c) Gestion de Identidades y Perfiles: Definicion de roles y niveles de acceso segun la necesidad del usuario."
- "d) Copias de Seguridad y Recuperacion: Mecanismos de respaldo periodico para garantizar disponibilidad."
- "e) Proteccion de Infraestructura: Uso de firewalls, antivirus y sistemas de deteccion de intrusos (IDS/IPS)."
- "f) Analisis de Vulnerabilidades y Pruebas de Penetracion: Evaluaciones regulares de seguridad en sistemas."
- "g) Digitalizacion: Usar sistemas especializados que permitan gestionar y documentar el tratamiento de datos."

Art. 4, Medidas Fisicas: a) control de acceso a instalaciones con documentos fisicos o servidores; b) monitoreo y vigilancia (camaras y registros de ingreso); c) almacenamiento seguro (cajas fuertes o gabinetes con llave); d) proteccion ante desastres naturales; e) eliminacion segura de documentos (trituradoras y borrado seguro de dispositivos).

Art. 4, Medidas de Seguridad en Transferencias: a) SSL/TLS; b) "Contratos de Confidencialidad y Contratos para la Transferencia de Datos: Acuerdos legales con terceros que tratan datos."; c) transferencias internacionales solo a paises con proteccion equivalente; d) notificacion de brechas a ACE, FGR y titulares en maximo 72 horas.

Art. 5 (transcripcion): "Con el fin de garantizar la eficacia de la presente Politica, se establecen los siguientes mecanismos de cumplimiento y supervision: a) Auditorias Periodicas: Para verificar el cumplimiento de las medidas de seguridad. b) Actualizacion de Politicas: Adaptacion a nuevas amenazas y regulaciones. c) Mecanismos de Denuncia: Vias para que los titulares reporten incumplimientos o violaciones de seguridad."

Art. 8 (transcripcion): "Todas las entidades obligadas deben actualizar sus procedimientos internos para cumplir con esta normativa (Art. 60 LPDP) a) El Delegado de Proteccion de Datos Personales sera responsable de la supervision interna. (Art. 15 y 16 LPDP) b) Se realizaran auditorias anuales para evaluar el cumplimiento de estas politicas. (Art. 50 literal l) LPDP) c) Se fomentara la certificacion en normas internacionales de privacidad y seguridad de datos."

Art. 9 (transcripcion): "Estas politicas entraran en vigencia a partir de su publicacion y seran actualizadas periodicamente para garantizar su adecuacion a nuevas regulaciones (Art. 24 literal g) LPDP)."

### 3.4 Errores o imprecisiones de referencia cruzada detectados

Estos puntos importan porque afectan la solidez de exigir cada medida:

1. Politicas Art. 8 lit. b apoya las "auditorias anuales" en el Art. 50 lit. l LPDP. Ese literal dice: "Realizar auditorias anuales de las certificaciones expedidas", que es una atribucion de la ACE sobre certificaciones, no un deber de los sujetos obligados de auditarse. La periodicidad anual para empresas nace, por tanto, solo de las Politicas, no de la ley.
2. Politicas Art. 3 lit. h dice que las entidades deben "someterse a auditorias" citando el Art. 5 lit. i LPDP (responsabilidad demostrada). El texto legal habla de ser "responsable del cumplimiento efectivo de las medidas", sin mencionar auditorias.
3. Politicas Art. 9 cita el Art. 24 lit. g LPDP para la actualizacion de politicas; ese literal se refiere a los medios para comunicar cambios del aviso de privacidad.
4. Politicas Art. 3 lit. c y Art. 8 lit. a citan los Arts. 15 y 16 LPDP para el delegado; si la reforma 659 deroga el Art. 15, la base legal del lit. b de las medidas organizativas queda cuestionada para el sector privado.
5. Politicas Art. 4 lit. c de transferencias exige compartir datos solo con paises de "proteccion equivalente"; el Art. 44 LPDP admite ademas transferencias a paises sin nivel adecuado si el emisor garantiza el tratamiento conforme a la ley, y la excepcion centroamericana. La Politica es mas estricta que la ley en su redaccion.

Implicacion: el software debe citar siempre la fuente exacta (ley o politica) de cada exigencia y no atribuir a la ley lo que solo dicen las Politicas.

### 3.5 Inventario de medidas y clasificacion

| # | Medida (Politicas Art. 4, 5, 8) | Tipo | Texto define contenido, formato o periodicidad? | Clasificacion propuesta | Base adicional en la LPDP |
|---|---|---|---|---|---|
| O1 | Politica de Proteccion de Datos (normas internas) | Organizativa | No | OBLIGATORIO-DE-ALCANCE-INDETERMINADO | Art. 24 (politica de privacidad), Art. 33 (procedimientos), Art. 25 inc. 2 ("politicas de seguridad del responsable") |
| O2 | Delegado de Proteccion de Datos | Organizativa | Remite a Arts. 15-16 LPDP y Lineamientos DPO | OBLIGATORIO hoy; CONDICIONAL si la reforma 659 entra en vigencia (sector privado) | Arts. 15-17 LPDP (a derogar/reformar) |
| O3 | Capacitacion del personal ("formacion continua") | Organizativa | No (los Lineamientos DPO Art. 22 anaden plan anual) | OBLIGATORIO-DE-ALCANCE-INDETERMINADO | Art. 16 lit. f LPDP |
| O4 | Registro de Actividades de Tratamiento (RAT) | Organizativa | No | OBLIGATORIO-DE-ALCANCE-INDETERMINADO | Art. 45 ("registro de banco de datos" para flujos transfronterizos), Art. 50 lit. t |
| O5 | Evaluaciones de Impacto en la Privacidad (EIPD) | Organizativa | No (no hay umbral de "alto riesgo") | OBLIGATORIO-DE-ALCANCE-INDETERMINADO | Art. 5 lit. i (responsabilidad demostrada) |
| O6 | Auditorias de cumplimiento "periodicas" | Organizativa | Periodicidad "anual" en Art. 8 lit. b; alcance: "cumplimiento de estas politicas" | OBLIGATORIO (periodicidad anual) con alcance indeterminado | Art. 5 lit. i |
| T1 | Control de acceso: contrasenas seguras, 2FA, acceso restringido | Tecnica | Menciona 2FA expresamente, sin decir en que sistemas | OBLIGATORIO-DE-ALCANCE-INDETERMINADO | Art. 36 |
| T2 | Cifrado en reposo y en transito | Tecnica | No define algoritmos ni alcance | OBLIGATORIO-DE-ALCANCE-INDETERMINADO | Art. 36 |
| T3 | Gestion de identidades y perfiles (roles, niveles de acceso) | Tecnica | No | OBLIGATORIO-DE-ALCANCE-INDETERMINADO | Art. 36 |
| T4 | Copias de seguridad y recuperacion (respaldo periodico) | Tecnica | "periodico", sin frecuencia | OBLIGATORIO-DE-ALCANCE-INDETERMINADO | Art. 36 (disponibilidad) |
| T5 | Firewalls, antivirus, IDS/IPS | Tecnica | No | OBLIGATORIO-DE-ALCANCE-INDETERMINADO | Art. 36 |
| T6 | Analisis de vulnerabilidades y pentesting "regulares" | Tecnica | "regulares", sin frecuencia | OBLIGATORIO-DE-ALCANCE-INDETERMINADO | Art. 36 |
| T7 | Digitalizacion: sistemas especializados para gestionar y documentar el tratamiento | Tecnica | No | OBLIGATORIO-DE-ALCANCE-INDETERMINADO (ver nota) | Art. 5 lit. i |
| F1 | Control de acceso a instalaciones con documentos o servidores | Fisica | No | OBLIGATORIO-DE-ALCANCE-INDETERMINADO, CONDICIONAL a que existan tales areas | Art. 36 |
| F2 | Camaras y registros de ingreso | Fisica | No | OBLIGATORIO-DE-ALCANCE-INDETERMINADO, CONDICIONAL | Art. 36 |
| F3 | Almacenamiento seguro de archivos fisicos | Fisica | No | CONDICIONAL a que existan archivos fisicos | Art. 36 |
| F4 | Proteccion ante desastres | Fisica | No | OBLIGATORIO-DE-ALCANCE-INDETERMINADO | Art. 36 |
| F5 | Eliminacion segura (trituradoras, borrado seguro) | Fisica | No | OBLIGATORIO-DE-ALCANCE-INDETERMINADO | Art. 5 lit. h (temporalidad), Arts. 10-11 |
| X1 | SSL/TLS en comunicaciones | Transferencia | Menciona el protocolo | OBLIGATORIO-DE-ALCANCE-INDETERMINADO | Art. 36 |
| X2 | Contratos de confidencialidad y de transferencia con terceros | Transferencia | No define clausulas | OBLIGATORIO | Art. 41 (contrato con receptor), Art. 33 inc. 2 (proveedores), Art. 34 lit. c |
| X3 | Transferencias internacionales solo a paises con proteccion equivalente | Transferencia | No hay lista de paises adecuados | OBLIGATORIO, CONDICIONAL a que haya transferencias internacionales | Arts. 44, 45, 54 inc. 2 |
| X4 | Notificacion de brechas en 72 horas a ACE, FGR y titulares | Transferencia | Si (plazo) | OBLIGATORIO | Art. 25 |
| S1 | Auditorias periodicas (mecanismo de supervision) | Supervision | Ver O6 | OBLIGATORIO (anual) | - |
| S2 | Actualizacion de politicas ante nuevas amenazas y regulaciones | Supervision | No | OBLIGATORIO-DE-ALCANCE-INDETERMINADO | Art. 25 inc. 2 |
| S3 | Mecanismos de denuncia para titulares | Supervision | No | OBLIGATORIO-DE-ALCANCE-INDETERMINADO | Art. 24 lit. e (mecanismos ARCO-POL), Art. 31 |
| S4 | Fomentar certificacion en normas internacionales | Supervision | "se fomentara" | RECOMENDADO | Art. 50 lit. j |

Nota sobre T7 ("Digitalizacion: usar sistemas especializados"): es la medida que mas directamente legitima un producto como PRIV-SV. Su redaccion es un mandato ("Usar sistemas especializados que permitan gestionar y documentar el tratamiento de datos"), pero no exige un tipo concreto de sistema ni certificacion alguna. El software no debe afirmar que "cumple la medida g)" por si mismo; puede decir que es una herramienta para gestionar y documentar el tratamiento, que es lo que la medida describe.

### 3.6 Evaluacion: OBLIGATORIO u OBLIGATORIO-DE-ALCANCE-INDETERMINADO, y riesgo

Argumentos para tratarlas como OBLIGATORIO pleno:
- Art. 35 LPDP: "imperativas". Art. 34 lit. b y Art. 36: deber de implementar y acatar. Art. 56 lit. b num. 5 y 7: sancion grave por no implementar. Politicas Art. 2: "cumplimiento obligatorio". Lineamientos DPO Art. 3 y Normativa PAS confirman que la ACE ejerce control, inspeccion y potestad sancionadora.

Argumentos para tratarlas como OBLIGATORIO-DE-ALCANCE-INDETERMINADO:
- Ninguna medida organizativa o tecnica define contenido minimo, formato, umbral, periodicidad (salvo "anual" en auditorias) ni proporcionalidad por tamano de empresa. Un RAT de una hoja y uno de cien campos "cumplen" literalmente. Una EIPD no tiene criterio de cuando se hace.
- El Art. 50 lit. i LPDP y Politicas Art. 1 hablan de implementar buenas practicas "en lo que fuera aplicable", lo que abre una valvula de proporcionalidad no reglada.
- Principio de tipicidad sancionadora: sancionar por "no tener RAT" es defendible; sancionar por "RAT insuficiente" sin estandar publicado es discutible y requerira motivacion de la ACE (Normativa PAS Art. 24: valoracion "conforme a las reglas de la sana critica").

Conclusion adoptada para el diseno: tratar cada medida como requisito obligatorio de existencia (hay o no hay RAT, EIPD, politica, plan de capacitacion, evidencia de backup, etc.) y como requisito de calidad indeterminado (el software propone un contenido de referencia basado en buenas practicas, marcado como "referencia, no estandar oficial"). El riesgo principal es doble: (a) para la empresa, que la ACE fije en inspeccion un estandar mas alto del que la empresa adopto, sin aviso previo; (b) para el producto, que si presenta sus plantillas como "el estandar de la ACE" incurra en una afirmacion falsa. Mitigacion: cada plantilla debe declarar su origen (ley, politica, buena practica) y el software debe permitir versionar y actualizar los contenidos cuando la ACE publique guias (Art. 50 lit. n) o actualice las Politicas (Politicas Art. 5 lit. b y Art. 9).

### 3.7 Bloques de obligacion por medida organizativa

**Norma:** Politicas ACE 001-0309025-DPDP
**Articulo:** Art. 4, Medidas Organizativas, lit. a; Art. 5 lit. b; Art. 8 inc. 1
**Obligacion:** Contar con una Politica de Proteccion de Datos ("normas internas que regulen el manejo de los datos personales"), actualizarla ante nuevas amenazas y regulaciones, y actualizar los procedimientos internos.
**A quien aplica:** Entidades publicas y privadas que traten datos personales (Politicas Art. 2); responsables y encargados (Art. 4 inc. 1).
**Implicacion para el software:** Modulo de documentos con plantilla de Politica interna de proteccion de datos, control de versiones, fecha de aprobacion, aprobador, evidencia de difusion al personal, recordatorio de revision periodica (la norma no fija plazo; se propone anual alineado con la auditoria del Art. 8 lit. b, marcado como recomendacion).
**Fuente oficial:** C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_politicas_protecciondatos.txt pags. 3-6, consultado 2026-09-23; https://ace.gob.sv/documentos/politicas/politicas_protecciondatos.pdf
**Vigencia:** VIGENTE (desde 3 sep 2025 segun fuente secundaria).
**Clasificacion:** OBLIGATORIO (existencia) / OBLIGATORIO-DE-ALCANCE-INDETERMINADO (contenido).

**Norma:** Politicas ACE; LPDP
**Articulo:** Politicas Art. 4 Org. lit. b y Art. 8 lit. a; LPDP Arts. 15, 16, 17
**Obligacion:** Nombrar un Delegado de Proteccion de Datos responsable de la supervision interna y de gestionar ARCO-POL.
**A quien aplica:** Todos los sujetos obligados (Art. 15 LPDP vigente). Tras la reforma 659: solo sector publico (segun fuentes secundarias).
**Implicacion para el software:** Ficha de "responsable de privacidad" con dos modos: "Delegado formal" (aplica regimen de Lineamientos DPO: nombramiento, plazos, registro, certificacion) y "Responsable interno designado" (sin efectos registrales, modo esperado para el sector privado si la reforma entra en vigencia). El software debe registrar la fecha y fuente del cambio de regimen.
**Fuente oficial:** ace_politicas_protecciondatos.txt pag. 3 y 6; ace_decreto_144.txt Arts. 15-17; https://www.asamblea.gob.sv/node/14116 (reforma), consultado 2026-09-23.
**Vigencia:** VIGENTE; MODIFICADA-PENDIENTE (reforma 659 aprobada, publicacion no confirmada).
**Clasificacion:** OBLIGATORIO hoy; CONDICIONAL tras la reforma (solo sector publico).

**Norma:** Politicas ACE; LPDP; Lineamientos DPO
**Articulo:** Politicas Art. 4 Org. lit. c; LPDP Art. 16 lit. f; Lineamientos Art. 22 inc. 3
**Obligacion:** Formacion continua del personal en seguridad de datos; actividades de formacion sobre derechos y obligaciones de la ley; plan anual de capacitacion al personal con induccion para personal nuevo que trate datos.
**A quien aplica:** Responsables (Politicas); delegado como ejecutor (LPDP Art. 16 lit. f, Lineamientos Art. 22). Tras la reforma, la funcion pasa al sujeto obligado (segun fuentes secundarias).
**Implicacion para el software:** Plan anual de capacitacion con sesiones, asistentes, contenido, fecha, material y constancia; induccion obligatoria marcada para nuevos ingresos con acceso a datos; reporte de cobertura por area; alerta cuando un rol con acceso a datos no tiene formacion en los ultimos 12 meses (periodicidad propuesta a partir de "anual" de los Lineamientos; para el personal general la norma solo dice "continua").
**Fuente oficial:** ace_politicas_protecciondatos.txt pag. 3; ace_decreto_144.txt Art. 16; lineamientos_dpo_OCR.txt Art. 22 (verificado en ocr/lineamientos_dpo/page-07.png), consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (existencia de formacion) / OBLIGATORIO-DE-ALCANCE-INDETERMINADO (contenido y frecuencia para el personal general); el plan anual es OBLIGATORIO mientras exista delegado (Lineamientos Art. 22) y CONDICIONAL para el sector privado tras la reforma.

**Norma:** Politicas ACE
**Articulo:** Art. 4 Org. lit. d
**Obligacion:** "Mantener un registro detallado de como se recopilan, almacenan y utilizan los datos personales" (Registro de Actividades de Tratamiento).
**A quien aplica:** Responsables y encargados.
**Implicacion para el software:** Inventario de tratamientos con, como minimo, campos que respondan a "como se recopilan, almacenan y utilizan": finalidad, base de licitud (Art. 5 lit. g), categorias de datos y de titulares, datos sensibles (Art. 24 lit. b), fuente de recoleccion, sistemas y ubicacion de almacenamiento, plazo de conservacion (Art. 5 lit. h), encargados y proveedores con acceso (Art. 33 inc. 2), transferencias nacionales e internacionales (Arts. 40-45), medidas de seguridad aplicadas (Art. 36), responsable interno. Debe poder exportarse como documento fechado y versionado, porque la ACE puede pedir "antecedentes, documentos, programas" (Art. 50 lit. t) y el Art. 45 pide "registro de banco de datos" para flujos transfronterizos. Los campos concretos son propuesta del producto, no lista oficial.
**Fuente oficial:** ace_politicas_protecciondatos.txt pag. 3, consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (existencia) / OBLIGATORIO-DE-ALCANCE-INDETERMINADO (contenido).

**Norma:** Politicas ACE
**Articulo:** Art. 4 Org. lit. e
**Obligacion:** Evaluaciones de Impacto en la Privacidad: "Identificacion y mitigacion de riesgos".
**A quien aplica:** Responsables y encargados.
**Implicacion para el software:** Modulo de EIPD por tratamiento con: descripcion, necesidad y proporcionalidad, riesgos para titulares, probabilidad e impacto, medidas de mitigacion, riesgo residual, aprobador y fecha. Como la norma no fija umbral, el software debe ofrecer un criterio orientativo (datos sensibles, menores, perfilado, transferencias internacionales, gran volumen, nuevas tecnologias) marcado como recomendacion y dejar que la empresa decida y documente por que hace o no hace una EIPD. Los Lineamientos DPO Art. 24 inc. 2 refuerzan la idea de participacion "desde la etapa mas temprana posible en el diseno de cualquier nuevo tratamiento, producto o servicio".
**Fuente oficial:** ace_politicas_protecciondatos.txt pag. 3; lineamientos_dpo_OCR.txt Art. 24, consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (existencia de la practica) / OBLIGATORIO-DE-ALCANCE-INDETERMINADO (cuando y como).

**Norma:** Politicas ACE
**Articulo:** Art. 4 Org. lit. f; Art. 5 lit. a; Art. 8 lit. b
**Obligacion:** Auditorias de cumplimiento: "verificacion periodica del cumplimiento de las medidas de seguridad"; "auditorias periodicas"; "se realizaran auditorias anuales para evaluar el cumplimiento de estas politicas".
**A quien aplica:** Todas las entidades obligadas (Art. 8 inc. 1).
**Implicacion para el software:** Programa de auditoria con ciclo anual, alcance (las medidas de las Politicas), auditor (interno o externo; la norma no exige externo ni certificado), hallazgos, plan de accion, cierre y evidencia. El informe de auditoria interno o externo es prueba admisible en el procedimiento sancionador (Normativa PAS Art. 24). Alerta de vencimiento a los 12 meses de la ultima auditoria. El software no realiza la auditoria ni la firma.
**Fuente oficial:** ace_politicas_protecciondatos.txt pags. 3, 4 y 6; normativa_sancionadora_OCR.txt Art. 24, consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (periodicidad anual expresa) / alcance y metodo indeterminados.

**Norma:** Politicas ACE
**Articulo:** Art. 5 lit. c
**Obligacion:** Mecanismos de denuncia para que los titulares reporten incumplimientos o violaciones de seguridad.
**A quien aplica:** Responsables.
**Implicacion para el software:** Canal de recepcion de reportes de titulares (formulario web o registro manual de reportes recibidos por otros canales), con trazabilidad, vinculo con el modulo de incidentes (Art. 25) y con ARCO-POL. Evidencia de que el canal esta publicado (captura, URL, fecha).
**Fuente oficial:** ace_politicas_protecciondatos.txt pag. 5, consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO-DE-ALCANCE-INDETERMINADO.

**Norma:** Politicas ACE
**Articulo:** Art. 8 lit. c
**Obligacion:** "Se fomentara la certificacion en normas internacionales de privacidad y seguridad de datos."
**A quien aplica:** Entidades obligadas.
**Implicacion para el software:** Campo opcional para registrar certificaciones (ISO 27001, ISO 27701, etc.) con vigencia y alcance; no afecta el estado de cumplimiento.
**Fuente oficial:** ace_politicas_protecciondatos.txt pag. 6, consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** RECOMENDADO.

---

## 4. Lineamientos para el Delegado de Proteccion de Datos Personales

### 4.1 Identificacion, fechas y vigencia

| Dato | Valor | Fuente |
|---|---|---|
| Emisor | Director General de la ACE, Eduardo Alexis Rodriguez Rodriguez | page-11.png |
| Base legal invocada | Art. 60 LPDP y Art. 159 de la Ley de Procedimientos Administrativos (Por tanto); considerando II cita Art. 15 LPDP | page-02.png |
| Fecha de emision | 24 de julio de 2026 ("a los veinticuatro dias del mes de julio del ano dos mil veintiseis") | page-11.png |
| Publicacion | Diario Oficial N. 146, Tomo 452, martes 11 de agosto de 2026, pags. 12-21, Registro No. F40427 | page-01.png, page-11.png |
| Vigencia (Art. 42) | "ocho dias despues contados a partir del dia siguiente de su publicacion": 19 de agosto de 2026 segun prensa (Diario El Mundo 28 ago 2026; elsalvador.com 12 sep 2026) y contexto del proyecto. Computo literal ambiguo: podria leerse 20 ago 2026. Se adopta 19 ago 2026 | page-11.png; fuentes secundarias |
| URL oficial | https://ace.gob.sv/page/documentos/politicas/NDPDDP.pdf | WebFetch ace.gob.sv/politicas.php 2026-09-23 |
| Extension | 42 articulos en 10 capitulos | OCR completo |

### 4.2 Estructura

```
Cap. I    Disposiciones generales            Arts. 1-3  (definiciones, objeto, sujetos obligados)
Cap. II   Perfil, nombramiento y registro    Arts. 4-12 (rol, perfil, nombramiento, contenido, notificacion 3 dias,
                                                        declaracion jurada, registro ACE 15 dias, registro publico, credencial 15 dias)
Cap. III  Interno o externo y modalidades    Arts. 13-17 (interno/externo, persona juridica, extranjero, grupo, varios y sustitutos)
Cap. IV   Evaluacion, cesacion o suspension  Arts. 18-19 (verificacion cada 3 anos, reemplazo en 10 dias)
Cap. V    Formacion y certificacion          Arts. 20-22 (programa, certificacion, capacitacion anual y plan anual)
Cap. VI   Independencia y atribuciones       Arts. 23-28 (autonomia, atribuciones, garantias, otras funciones, prohibiciones, conflicto)
Cap. VII  Informes y aviso de privacidad     Arts. 29-31 (enlace institucional, informe 2 veces al ano, aviso y conservacion 10 anos)
Cap. VIII Ejercicio de derechos ARCO-POL     Arts. 32-38 (formularios, resolver y documentar 3 dias, plazos, incompetencia,
                                                         confidencialidad 5 anos, asistencia, costos)
Cap. IX   Normativa interna                  Art. 39
Cap. X    Transitorias y finales             Arts. 40-42 (transitoria 20 dias, remisiones, vigencia)
```

Art. 3 (verificado en page-02.png): "Las disposiciones contenidas en los presentes lineamientos, seran de obligatorio cumplimiento para el Delegado, el encargado y el responsable; este ultimo, en su calidad de sujeto obligado, ya sea como persona natural o juridica, de caracter publico o privado, conforme a lo dispuesto en el articulo 2 de la LPDP."

### 4.3 Requisitos del delegado (Art. 5, verificado en OCR)

a) Grado universitario, "de preferencia profesionales graduados en Ciencias Juridicas".
b) Mayor de 21 anos.
c) Experiencia profesional y/o laboral en una o varias de: proteccion de datos, procedimientos administrativos juridicos, cumplimiento normativo, gestion de riesgos, tecnologias de la informacion, seguridad de la informacion o ciberseguridad.
d) No condenado por delitos dolosos (en especial relacionados con uso indebido de informacion, seguridad de datos, administracion publica, fe publica); no sancionado por infracciones a la LPDP; sector publico: no sancionado por la Ley de Etica Gubernamental en los 5 anos previos.
e) Someterse y aprobar el "Programa de Certificacion de Delegados de Proteccion de Datos Personales" de la ACE, exigible "a partir de la entrada en vigencia del referido programa"; los ya nombrados lo cumpliran "en el plazo y condiciones que la Agencia establezca". El programa sera gratuito para el delegado debidamente nombrado.

Ademas: declaracion jurada simple previa a la aceptacion sobre conflictos de interes reales, potenciales o aparentes (Art. 9); verificacion previa del perfil por el responsable y re-verificacion al menos cada 3 anos con atestados de capacitacion o certificaciones (Art. 18).

### 4.4 Nombramiento y registro: bloques de obligacion

**Norma:** Lineamientos DPO
**Articulo:** Arts. 6 y 7
**Obligacion:** Nombramiento formal. Sector privado persona juridica: acuerdo o acta del Administrador Unico, Junta Directiva, Consejo u organo maximo; persona natural responsable: acta con firma legalizada por notario o firma electronica certificada. Contenido minimo (Art. 7): numero de acuerdo, fecha, nombre del responsable, fundamento legal, generales del delegado (o razon social y NIT si es persona juridica), fecha de inicio, plazo o caracter indefinido, atribuciones, nombre y firma de quien nombra (sector privado: firma legalizada por notario), sello si lo hubiere. Firma electronica extranjera: cumplir Art. 45 Ley de Firma Electronica y Art. 24 de su Reglamento; el responsable acredita su validez ante la ACE. El responsable entrega al delegado certificacion del acuerdo.
**A quien aplica:** Responsables que nombren delegado.
**Implicacion para el software:** Generador de acta o acuerdo de nombramiento con los 10 campos del Art. 7 como checklist; repositorio del documento firmado; el software no legaliza ni firma.
**Fuente oficial:** lineamientos_dpo_OCR.txt Arts. 6-7 (page-03.png, page-04.png), consultado 2026-09-23.
**Vigencia:** VIGENTE. Para el sector privado: CONDICIONAL a que nombre delegado si la reforma 659 entra en vigencia.
**Clasificacion:** OBLIGATORIO (mientras exista deber de nombrar delegado).

**Norma:** Lineamientos DPO
**Articulo:** Art. 8
**Obligacion:** Notificar al delegado su nombramiento "dentro de los tres dias habiles siguientes a su designacion", indicando fecha de inicio y alcance de atribuciones; conservar copia o constancia de la notificacion.
**A quien aplica:** Responsable.
**Implicacion para el software:** Tarea con plazo de 3 dias habiles desde la fecha del acuerdo; constancia adjunta; calendario de dias habiles de El Salvador.
**Fuente oficial:** page-04.png, consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (condicionado a la existencia del delegado).

**Norma:** Lineamientos DPO
**Articulo:** Art. 10
**Obligacion:** Comunicar el nombramiento a la Direccion de Proteccion de Datos Personales de la ACE mediante la plataforma del Registro de Delegados "dentro del plazo maximo de quince dias habiles contados a partir del dia siguiente del nombramiento", remitiendo certificacion del acuerdo; si es delegado por servicios profesionales, fotocopia certificada por notario del contrato; sector privado: documentos de existencia legal de la persona juridica y personeria del representante legal, certificados por notario. Mantener la informacion actualizada, incorporando modificaciones "dentro del plazo maximo de diez dias habiles".
**A quien aplica:** Responsable.
**Implicacion para el software:** Tareas de 15 dias habiles (registro inicial) y 10 dias habiles (cada modificacion); checklist documental; registro del acuse de la ACE. Nota operativa: la plataforma no esta habilitada; el Art. 40 preve comunicacion por oficio o correo institucional, y la ACE dejo sin efecto la fecha limite (seccion 4.12).
**Fuente oficial:** page-04.png, consultado 2026-09-23.
**Vigencia:** VIGENTE; aplicacion practica suspendida por comunicado de la ACE (fuente secundaria).
**Clasificacion:** OBLIGATORIO (condicionado).

**Norma:** Lineamientos DPO
**Articulo:** Arts. 11 y 12
**Obligacion:** La ACE lleva un Registro Publico de Delegados, emite credenciales y constancias, y publica una lista consultable por la ciudadania. Emite la credencial en maximo 15 dias habiles si se cumplen los requisitos. Si no inscribe, notifica el incumplimiento y el responsable nombra otro delegado "dentro del plazo de diez dias habiles contados a partir de la no inscripcion". La inscripcion no valida automaticamente la idoneidad.
**A quien aplica:** ACE (registro) y responsable (reemplazo).
**Implicacion para el software:** Estados del delegado: nombrado, notificado, comunicado a ACE, inscrito/credencial, denegado (dispara tarea de 10 dias habiles), cesado.
**Fuente oficial:** page-04.png, page-05.png, consultado 2026-09-23.
**Vigencia:** VIGENTE (registro no operativo aun).
**Clasificacion:** OBLIGATORIO (condicionado).

### 4.5 Modalidades (Arts. 13-17)

- Interno (en planilla) o externo (contrato de servicios profesionales de derecho comun); indefinido o a plazo; entra en funciones desde la notificacion o la suscripcion del contrato (Art. 13).
- Persona juridica como delegado (Art. 14): debe designar una persona natural que cumpla el perfil y sea punto de contacto; la persona juridica debe tener experiencia comprobable en proteccion de datos, riesgos, auditorias, TI, seguridad o privacidad; equipo multidisciplinario con al menos un profesional en ciencias juridicas y un experto en ciberseguridad, sistemas o gestion de riesgos; estructura para gestionar ARCO-POL, consultas, incidentes y cooperacion con la autoridad; no estar inhabilitado para contratar con la Administracion Publica.
- Delegado extranjero (Art. 15): mismos requisitos, declaracion jurada de sometimiento a la legislacion salvadorena y colaboracion con autoridades, funciones en horario y calendario de El Salvador, contrato con clausulas de confidencialidad, responsabilidad y garantia; el responsable asume toda responsabilidad frente a titulares y ACE.
- Delegado comun en grupos de sociedades o entidades vinculadas del sector privado (Art. 16): cada entidad garantiza medios, accesibilidad a traves de los canales de su aviso de privacidad, y el delegado resuelve ARCO-POL de manera separada por entidad.
- Mas de un delegado segun naturaleza de datos, dimension, estructura, volumen ARCO-POL y nivel de riesgo; delegados sustitutos hasta un numero igual al de propietarios; al asumir un sustituto se informa a la ACE en 15 dias habiles (Art. 17).

Implicacion para el software: modelo multi-entidad (grupo) con un delegado comun y expedientes ARCO-POL separados por entidad; soporte de delegado persona juridica con persona natural designada; sustitutos; alerta de 15 dias habiles al activar un sustituto.

### 4.6 Certificacion (Arts. 5 lit. e, 20, 21, 40)

- El delegado "debera cumplir y aprobar el contenido del Programa de estudios que habilite su certificacion" (Art. 20). Los aspirantes suben a la plataforma: formulario de solicitud, curriculum, certificacion del nombramiento, acta de notificacion, y documentacion de requisitos; declaran conocer el proceso (verificado en page-07.png). Si el delegado es persona juridica, el designado obtiene la certificacion.
- Art. 21: una vez iniciado el programa, cursarlo y aprobarlo "como condicion para la validez de su nombramiento"; segunda oportunidad limitada al examen; si reprueba de nuevo, el responsable designa a otra persona y el aspirante puede reintentar pasados 6 meses; nota minima 7 sobre 10; la ACE expide la certificacion.
- Art. 40: nombramientos previos que no cumplan requisitos se tienen por validos, pero deben someterse y aprobar el programa.
- Estado al 23 sep 2026: el programa no ha entrado en vigencia (Diario El Mundo 28 ago 2026; El Diario de Hoy 12 sep 2026: "entrada en vigencia aun pendiente"). La ACE realizo dos webinars sobre el delegado el 9 y 11 de septiembre de 2026 (https://ace.gob.sv/noticia/webinar y https://ace.gob.sv/noticia/segundo-webinar-delegado-de-proteccion-de-datos).

Clasificacion: CONDICIONAL (a la entrada en vigencia del programa y a que la entidad tenga delegado). Software: campo de estado de certificacion (no exigible aun / en curso / aprobado / reprobado con fecha de reintento a 6 meses), sin bloquear otras funciones.

### 4.7 Capacitacion del delegado y plan anual (Art. 22)

**Norma:** Lineamientos DPO
**Articulo:** Art. 22
**Obligacion:** El responsable garantiza que el delegado reciba "al menos una vez al ano" capacitacion en proteccion de datos y ejercicio ARCO-POL, asigna recursos "conforme a la disponibilidad presupuestaria" y "debera conservar la documentacion que acredite haber recibido la formacion". El delegado "elaborara un plan anual de capacitacion dirigido al personal del ente obligado, el cual tambien incluira programas de induccion para el personal nuevo que desempene funciones relacionadas al tratamiento de datos personales".
**A quien aplica:** Responsable (garantizar y conservar) y delegado (plan anual).
**Implicacion para el software:** Ver bloque de capacitacion en 3.7. Anadir: registro de la capacitacion anual del propio delegado con constancia; plan anual con estado de ejecucion; induccion vinculada a altas de personal con acceso a datos.
**Fuente oficial:** page-07.png, consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO mientras exista delegado; para el sector privado sin delegado tras la reforma, la formacion del personal sigue siendo OBLIGATORIA por Politicas Art. 4 lit. c y por el Art. 16 reformado (segun fuentes secundarias), pero el "plan anual" formal pasa a RECOMENDADO.

### 4.8 Independencia, garantias, prohibiciones y conflicto de intereses (Arts. 23-28)

- Autonomia e independencia funcional; puede informar a la ACE de hechos del responsable que constituyan infraccion o menoscaben su independencia (Art. 23).
- Atribuciones del Art. 16 LPDP; participacion desde el diseno de todo nuevo tratamiento, producto o servicio; miembro de comites de tratamiento; reporta al mas alto nivel de direccion; no responde por decisiones finales del responsable si demuestra diligencia; puede pedir un equipo de apoyo (Art. 24).
- Garantias minimas del responsable (Art. 25, verificado en page-08.png): a) recursos, infraestructura, herramientas tecnicas y formacion continua; b) no dar instrucciones sobre su criterio tecnico, juridico o procedimental; c) acceso oportuno a informacion y documentacion; d) participacion o consulta oportuna en decisiones que incidan en el tratamiento.
- Otras funciones compatibles si no generan conflicto (Art. 26).
- Prohibiciones (Art. 27, verificado): tomar decisiones sobre finalidad o medios del tratamiento; representar a la organizacion ante la ACE como responsable o encargado.
- Conflicto de intereses (Art. 28): ejecutar tratamientos, asesorar para salvaguardar intereses de la entidad, decidir sobre la organizacion; en el sector privado se considera en conflicto al personal con funciones de gerente, subgerente, jefe, coordinador o cualquier puesto ejecutivo, de direccion o maxima autoridad; excepcion: puede ser delegado quien ostente tales cargos si sus funciones se limitan exclusivamente a las del delegado y cuenta con equipo tecnico de apoyo.

Implicacion para el software: cuestionario de conflicto de intereses al designar (cargo, funciones, participacion en tratamientos) que genere la declaracion jurada del Art. 9 como borrador; registro de recomendaciones del delegado y de su acatamiento o no (Art. 30 lit. a: cuando no se acaten "dejara constancia expresa de ello").

### 4.9 Enlace, informes y aviso de privacidad (Arts. 29-31)

**Norma:** Lineamientos DPO
**Articulo:** Art. 30
**Obligacion:** El delegado informa al responsable "cuando sea necesario y al menos dos veces al ano" sobre sus funciones, la gestion del tratamiento, estadisticas ARCO-POL y otra informacion relevante; la ACE puede requerir informes. Puede emitir recomendaciones y dejar constancia cuando no se acaten; dar seguimiento; informar sobre efectividad de procedimientos ARCO-POL. No existe un "informe anual a la ACE" en los Lineamientos; lo que existe es el informe semestral interno al responsable y la posibilidad de requerimientos de la ACE.
**A quien aplica:** Delegado (emite), responsable (recibe).
**Implicacion para el software:** Generador de informe semestral con estadisticas ARCO-POL, incidentes, capacitaciones, auditorias, recomendaciones y su estado; archivo con fecha de presentacion a direccion.
**Fuente oficial:** page-09.png, consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO mientras exista delegado; RECOMENDADO como practica de gobierno para el sector privado sin delegado.

**Norma:** Lineamientos DPO; LPDP
**Articulo:** Lineamientos Art. 31; LPDP Art. 16 lit. g y Art. 24
**Obligacion:** El delegado publica el aviso de privacidad (web o establecimiento) previa autorizacion del responsable; "La autorizacion y cualquier operacion relacionada con su publicacion seran documentadas por el Delegado. Esta documentacion se conservara por el responsable, en formato fisico o digital, durante un plazo minimo de diez anos".
**A quien aplica:** Delegado (documenta), responsable (conserva 10 anos).
**Implicacion para el software:** Historial de versiones del aviso con autorizacion, fecha y medio de publicacion, capturas o evidencia, y retencion minima de 10 anos con bloqueo de borrado antes de ese plazo.
**Fuente oficial:** page-09.png; ace_decreto_144.txt Arts. 16 y 24, consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO (la publicacion del aviso es obligatoria por ley; la retencion de 10 anos nace del lineamiento).

### 4.10 Deberes ARCO-POL con impacto documental (Arts. 32-39)

- Art. 32: promover los formularios de la ACE como estandar minimo; pueden anadirse elementos justificados que no obstaculicen; los formularios oficiales deben aceptarse siempre; los responsables, publicos o privados, "pondran a disposicion del publico los formularios" en sitios web, plataformas, oficinas u otros medios, garantizando formato fisico en todas sus sedes cuando se requiera. Este inciso esta dirigido a los responsables, no solo al delegado.
- Art. 33: resolver todas las solicitudes con resolucion de admision, prevencion, subsanacion, reconocimiento, incompetencia, denegatoria o final; "Todas las actuaciones ... se documentaran y notificaran al interesado ... dentro del plazo de tres dias habiles contados a partir de su emision"; en resolucion procedente se fija la fecha en que se hara efectivo el derecho; el titular agraviado puede acudir a la ACE en 10 dias habiles desde la notificacion; la ACE pide informe al delegado o responsable.
- Art. 34: respuesta en 20 dias habiles (Art. 20 LPDP); si hay prorroga, motivarla y notificarla en 3 dias habiles dentro del plazo ordinario.
- Art. 35: incompetencia cuando no se posee la informacion o no se esta legalmente habilitado.
- Art. 36: confidencialidad del delegado, subsiste 5 anos tras el cese.
- Art. 37: deber de asistencia, recurso humano, tecnico y material, acceso a datos y operaciones.
- Art. 38: "El responsable publicara, preferentemente en formato electronico o en su sitio web, los costos aplicables a la reproduccion, certificacion y envio" y los comunicara antes de la entrega.
- Art. 39: los sujetos obligados "podran" elaborar manuales, guias y procedimientos internos (facultativo); el delegado propondra mecanismos y su actualizacion.

Implicacion para el software: expediente ARCO-POL con tipos de resolucion del Art. 33, tarea de notificacion en 3 dias habiles por cada actuacion, aviso de prorroga en 3 dias habiles, fecha de efectividad del derecho, registro de reclamos ante la ACE; publicacion de formularios y de tabla de costos como evidencias fechadas.

### 4.11 Tabla de plazos verificados

| Plazo | Que | Articulo | Verificado en imagen |
|---|---|---|---|
| 3 dias habiles | Notificar al delegado su nombramiento | Art. 8 | page-04.png |
| 15 dias habiles (desde el dia siguiente al nombramiento) | Comunicar nombramiento a la ACE via plataforma | Art. 10 | page-04.png |
| 10 dias habiles | Actualizar modificaciones en la plataforma | Art. 10 | page-04.png |
| 15 dias habiles | ACE emite credencial | Art. 12 | page-04.png |
| 10 dias habiles | Nombrar otro delegado si la ACE no inscribe | Art. 12 | page-05.png |
| 15 dias habiles | Informar a la ACE nombramiento de nuevo delegado cuando asume un sustituto | Art. 17 | page-06.png |
| Al menos cada 3 anos | Re-verificar perfil del delegado | Art. 18 | page-06.png |
| 10 dias habiles | Designar nuevo delegado ante cesacion o suspension | Art. 19 | page-06.png |
| 6 meses | Reintento de certificacion tras reprobar dos veces | Art. 21 | page-07.png |
| Al menos 1 vez al ano | Capacitacion del delegado | Art. 22 | page-07.png |
| Anual | Plan de capacitacion al personal | Art. 22 | page-07.png |
| Al menos 2 veces al ano | Informe del delegado al responsable | Art. 30 | page-09.png |
| Minimo 10 anos | Conservar documentacion del aviso de privacidad | Art. 31 | page-09.png |
| 3 dias habiles | Documentar y notificar cada actuacion ARCO-POL | Art. 33 | page-10.png |
| 10 dias habiles | Titular reclama ante la ACE contra resolucion del delegado | Art. 33 | page-10.png |
| 20 dias habiles | Respuesta ARCO-POL (remite a Art. 20 LPDP) | Art. 34 | page-10.png |
| 3 dias habiles | Notificar prorroga motivada | Art. 34 | page-10.png |
| 5 anos | Confidencialidad del delegado tras el cese | Art. 36 | page-10.png |
| 20 dias habiles desde la vigencia | Comunicacion transitoria de nombramientos por oficio o correo | Art. 40 | page-11.png |
| 8 dias desde el dia siguiente a la publicacion | Entrada en vigencia | Art. 42 | page-11.png |

### 4.12 Disposicion transitoria y comunicado de la ACE

Art. 40 inc. 3 (verificado): "Mientras no se encuentre habilitada la plataforma informatica del registro de Delegados, las comunicaciones de nombramiento, modificacion o cesacion se realizaran mediante oficio, escrito o correo institucional dirigido a la Direccion de Proteccion de Datos Personales de la ACE, dentro de los veinte dias habiles de la entrada en vigencia de estos lineamientos." Con vigencia el 19 ago 2026, la prensa y firmas legales situaron el vencimiento el 16 sep 2026 (ContraPunto 13 sep 2026; BLP).

Segun El Diario de Hoy y elsalvador.com (ambos 12 sep 2026), la ACE publico en su sitio web un comunicado: "Queda sin efecto la fecha limite establecida para el nombramiento del delegado de proteccion de datos personales" y "no sera necesario realizar ninguna accion al respecto", anadiendo que cualquier nueva disposicion sera comunicada oportunamente. No se localizo el comunicado en ace.gob.sv al 23 sep 2026 (la seccion de noticias solo muestra los dos webinars). Confianza: media (dos medios coincidentes citando texto del comunicado).

### 4.13 Formulario oficial de nombramiento (07-07-2025)

El formulario de la ACE (ace_form_nombramiento_delegado.txt) es anterior a los Lineamientos: se funda en Arts. 15 y 16 LPDP, recoge datos del sujeto obligado (nombre, NIT, domicilio, correo, telefono), datos del delegado (nombre, domicilio, correo, telefono, documento de identidad, fecha de nombramiento), transcribe las atribuciones del Art. 16 y exige firmas del delegado y del representante legal, sello, y nota: "Para formalizacion del nombramiento se debera emitir un Acuerdo Institucional Suscrito por el titular de la Institucion." Los Lineamientos (Art. 7) exigen mas campos (fundamento legal, plazo, fecha de inicio, firma legalizada por notario en el sector privado). El software debe usar el Art. 7 como lista maestra y el formulario como plantilla compatible.

### 4.14 Que sobrevive para el sector privado si la reforma 659 entra en vigencia

Premisas (segun fuentes secundarias: https://www.asamblea.gob.sv/node/14116; El Diario de Hoy 17 sep 2026; elsalvador.com 17 sep 2026): se derogan Arts. 15 y 17; se reforma el Art. 16 para que "los sujetos obligados deberan auxiliar a sus dependencias o proveedores y fijar lineamientos internos para gestionar las solicitudes ARCO-POL"; las solicitudes se presentan directamente ante la empresa; plazos 20 + 20 dias habiles; el sector publico mantiene delegado (Art. 47) que puede ser el Oficial de Informacion; el Presidente nombra al Director de Proteccion de Datos por 3 anos (Art. 51). Vigencia: 8 dias tras publicacion en D.O., no confirmada al 23 sep 2026. El texto oficial del decreto no ha sido localizado.

| Elemento de los Lineamientos DPO | Sector privado sin delegado tras la reforma | Razon |
|---|---|---|
| Obligacion de nombrar delegado, nombramiento formal, notificacion 3 dias, registro 15/10 dias, credencial, sustitutos, cesacion 10 dias (Arts. 6-19) | NO APLICA (salvo nombramiento voluntario) | Descansan en Art. 15 LPDP derogado |
| Certificacion del delegado (Arts. 5 e, 20, 21, 40) | NO APLICA salvo delegado voluntario; incierto si la ACE exigira certificacion a delegados voluntarios | Lineamientos Art. 3 obliga "al Delegado" sin distinguir origen; requiere abogado |
| Capacitacion anual del delegado (Art. 22 inc. 1-2) | NO APLICA sin delegado | Idem |
| Plan anual de capacitacion al personal e induccion (Art. 22 inc. 3) | SOBREVIVE como obligacion de fondo (Politicas Art. 4 lit. c "formacion continua"; Art. 16 lit. f reformado, segun fuentes secundarias, atribuido al sujeto obligado); el formato "plan anual" pasa a RECOMENDADO | Cambia el sujeto, no el deber |
| Independencia, garantias, prohibiciones, conflicto (Arts. 23-28) | NO APLICA sin delegado; RECOMENDADO si se designa responsable interno | Regulan la figura del delegado |
| Informe semestral al responsable (Art. 30) | RECOMENDADO | Gobierno interno |
| Aviso de privacidad: publicacion y conservacion 10 anos (Art. 31) | Publicacion SOBREVIVE (Art. 24 LPDP y Art. 16 lit. g reformado); conservacion de 10 anos: INCIERTA, porque el deber de documentar se asigna al delegado; RECOMENDADO conservarla igual por Art. 54 LPDP (carga de la prueba) | Art. 24 no se toca |
| Formularios oficiales a disposicion del publico (Art. 32 inc. 4) | SOBREVIVE: la obligacion esta dirigida a "los responsables sean estos publicos o privados" | Redaccion propia del Art. 32 |
| Resolver y documentar actuaciones, notificar en 3 dias habiles (Art. 33) | INCIERTO: las actuaciones y plazos legales (Arts. 18-22 LPDP) sobreviven; el plazo de 3 dias por actuacion es del lineamiento y esta dirigido al delegado. Tratar como RECOMENDADO (buena practica) y como OBLIGATORIO la denegatoria motivada en 3 dias (Art. 22 LPDP) | - |
| Plazos 20 dias, prorroga motivada (Art. 34) | SOBREVIVEN por Art. 20 LPDP; la notificacion de prorroga en 3 dias: RECOMENDADO | - |
| Incompetencia (Art. 35) | SOBREVIVE por Art. 19 LPDP | - |
| Confidencialidad 5 anos (Art. 36) | NO APLICA sin delegado; RECOMENDADO en contratos del responsable interno | - |
| Publicar costos (Art. 38) | SOBREVIVE por Art. 23 LPDP, dirigido al responsable | - |
| Normativa interna (Art. 39) | Facultativo ("podran"); RECOMENDADO. Segun fuentes secundarias el Art. 16 reformado exige "fijar lineamientos internos" ARCO-POL, lo que se solaparia con Art. 33 LPDP (OBLIGATORIO) | - |

Riesgo transversal: las Politicas ACE (Art. 4 lit. b, Art. 8 lit. a) siguen exigiendo delegado con supervision interna. Un abogado debe opinar si la ACE actualizara las Politicas o si, por jerarquia, la derogacion legal deja sin efecto esa medida para el sector privado. El software debe modelar la reforma como un "evento normativo" con fecha, que cambia el estado de las tareas relacionadas (de OBLIGATORIO a CONDICIONAL/RECOMENDADO) y deja rastro.

---

## 5. Inventario de documentos: obligatorio, recomendado o condicional

| # | Documento | Norma y articulo | Clasificacion | Notas para el software |
|---|---|---|---|---|
| D1 | Politica de Privacidad | LPDP Art. 24 inc. 1 ("politica de privacidad que debera elaborar el responsable"); Art. 54 (carga de la prueba de su comunicacion) | OBLIGATORIO | Documento base del aviso; versionado; evidencia de comunicacion |
| D2 | Aviso de Privacidad | LPDP Art. 24 (contenido minimo lit. a-i), Art. 7, Art. 16 lit. g; Lineamientos Art. 31 | OBLIGATORIO | Checklist de los 9 literales; nombre del delegado (lit. f) pasa a "punto de contacto" tras la reforma, pendiente de texto oficial; comunicacion por escrito al otorgar consentimiento |
| D3 | Politica de Proteccion de Datos (normas internas) | Politicas ACE Art. 4 Org. lit. a; Art. 25 inc. 2 LPDP ("politicas de seguridad del responsable") | OBLIGATORIO (alcance indeterminado) | Puede fusionarse con D1 en empresas pequenas, pero es distinta: D1 mira al titular, D3 mira al personal |
| D4 | Procedimiento ARCO-POL documentado | LPDP Art. 33 inc. 1 ("establecera y documentara procedimientos"); Art. 61 inc. 2 (mecanismos en 6 meses) | OBLIGATORIO | Debe basarse en las Politicas ACE y en medidas de seguridad minimas |
| D5 | Procedimiento de gestion de incidentes y vulneraciones | LPDP Art. 25 inc. 1-2 (notificar en 72 h; iniciar revision exhaustiva; actualizar politicas de seguridad); Politicas Art. 4 Transf. lit. d | OBLIGATORIO (la ley obliga a actuar; el "procedimiento" escrito es la forma de demostrarlo) | Plantillas de notificacion a ACE, FGR (contenido a-e) y titulares (a, b, d, e) |
| D6 | Registro de vulneraciones | LPDP Art. 25 inc. final ("documentara toda vulneracion ... fecha, motivo, hechos, efectos, medidas correctivas inmediatas y definitivas ... a disposicion de la autoridad") | OBLIGATORIO | Incluye vulneraciones no notificadas; campos minimos legales |
| D7 | Registro de Actividades de Tratamiento (RAT) | Politicas ACE Art. 4 Org. lit. d; LPDP Art. 45 ("registro de banco de datos"), Art. 50 lit. t | OBLIGATORIO (alcance indeterminado) | Ver 3.7 |
| D8 | Evaluacion de Impacto (EIPD) | Politicas ACE Art. 4 Org. lit. e | OBLIGATORIO (alcance indeterminado); en la practica CONDICIONAL al riesgo del tratamiento segun criterio de la empresa | Sin umbral oficial |
| D9 | Politica de retencion y eliminacion | LPDP Art. 5 lit. h (temporalidad), Art. 5 lit. c (consentimiento fija "periodo de almacenamiento"), Arts. 10-11 (cancelacion y bloqueo); Politicas Art. 4 Fis. lit. e (eliminacion segura) | OBLIGATORIO en cuanto al deber de limitar la conservacion; el documento "politica de retencion" es la forma de demostrarlo | Plazos por tratamiento en el RAT; evidencia de eliminacion |
| D10 | Contratos con encargados y proveedores con acceso a datos | LPDP Art. 33 inc. 2, Art. 34 lit. c, Art. 36 inc. 2; Politicas Art. 4 Transf. lit. b | OBLIGATORIO | Registro de proveedores con estado contractual y clausulas minimas; no hay clausulas modelo de la ACE |
| D11 | Contrato de transferencia con responsable receptor | LPDP Art. 41 ("debera suscribir un contrato ... como minimo las mismas obligaciones") | OBLIGATORIO, CONDICIONAL a que exista transferencia a otro responsable | Vinculado al RAT |
| D12 | Registro e informacion a la ACE de transferencias internacionales | LPDP Art. 45 inc. 2 ("se pondra en conocimiento" incluyendo informacion de la transferencia y registro de banco de datos), Art. 44, Art. 54 inc. 2 (carga de la prueba) | OBLIGATORIO, CONDICIONAL a que existan flujos transfronterizos | No hay formulario ni canal publicado por la ACE; el software genera el expediente y registra el envio |
| D13 | Evidencia de capacitacion | LPDP Art. 16 lit. f; Politicas Art. 4 Org. lit. c; Lineamientos Art. 22 | OBLIGATORIO | Constancias, asistencia, contenido, plan anual |
| D14 | Informes de auditoria | Politicas Art. 4 Org. lit. f, Art. 5 lit. a, Art. 8 lit. b (anual); Normativa PAS Art. 24 (prueba) | OBLIGATORIO (anual) | Interna o externa |
| D15 | Matriz de riesgos | No exigida con ese nombre; se deriva de EIPD (Politicas Art. 4 Org. lit. e "identificacion y mitigacion de riesgos") y de la referencia a ISO 27001 | RECOMENDADO | Util como insumo de EIPD y auditoria |
| D16 | Registro de consentimientos | LPDP Art. 54 (carga de la prueba en el responsable), Arts. 26-27 (expreso; sensibles por escrito con firma), Art. 29-30 (revocacion) | OBLIGATORIO en cuanto a poder demostrar; el "registro" es el medio | Fecha, medio, finalidad, version del aviso, revocacion |
| D17 | Publicacion de costos de reproduccion y envio | LPDP Art. 23; Lineamientos Art. 38 | OBLIGATORIO | Tabla publicada con fecha y evidencia |
| D18 | Formularios ARCO-POL a disposicion del publico | Lineamientos Art. 32 inc. 4; LPDP Art. 18 (requisitos) | OBLIGATORIO | Aceptar siempre los formularios oficiales |
| D19 | Acta de nombramiento del delegado, notificacion, declaracion jurada, constancia de registro | Lineamientos Arts. 6-10 | OBLIGATORIO mientras exista delegado; CONDICIONAL tras la reforma | Ver 4.4 |
| D20 | Informe semestral del delegado | Lineamientos Art. 30 | OBLIGATORIO con delegado; RECOMENDADO sin el | Ver 4.9 |
| D21 | Documentacion de publicacion del aviso (10 anos) | Lineamientos Art. 31 | OBLIGATORIO con delegado; RECOMENDADO sin el | Ver 4.9 |
| D22 | Manuales y procedimientos internos de apoyo | Lineamientos Art. 39 ("podran") | RECOMENDADO | - |
| D23 | Registro de certificaciones internacionales | Politicas Art. 8 lit. c | RECOMENDADO | - |

Bloques de obligacion para los documentos que nacen directamente de la ley y no fueron cubiertos arriba:

**Norma:** LPDP
**Articulo:** Art. 33 inc. 1
**Obligacion:** "El responsable establecera y documentara procedimientos para el ejercicio de los derechos ARCO-POL sobre los datos personales objetos de tratamiento, con base en las politicas de actuacion emitidas por la Entidad Rectora y las medidas de seguridad minimas necesarias."
**A quien aplica:** Responsable.
**Implicacion para el software:** Procedimiento ARCO-POL versionado, con flujo (recepcion, verificacion de identidad, prevencion 10 dias, incompetencia 5 dias, respuesta 20 + 20, notificacion a receptores 5 dias, denegatoria 3 dias) y evidencia de aprobacion y difusion.
**Fuente oficial:** ace_decreto_144.txt Art. 33, consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

**Norma:** LPDP
**Articulo:** Art. 25 inc. final
**Obligacion:** Documentar toda vulneracion que ocasione riesgo, con al menos fecha, motivo, hechos, efectos o implicaciones y medidas correctivas inmediatas y definitivas, a disposicion de la autoridad.
**A quien aplica:** Responsable.
**Implicacion para el software:** Registro de incidentes con esos campos como obligatorios, cronologia (conocimiento, notificaciones dentro de 72 h), enlace a notificaciones enviadas y a la actualizacion de politicas de seguridad (Art. 25 inc. 2). Exportable para la ACE.
**Fuente oficial:** ace_decreto_144.txt Art. 25, consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

**Norma:** LPDP
**Articulo:** Art. 41; Art. 45 inc. 2; Art. 54 inc. 2
**Obligacion:** Contrato con el responsable receptor con al menos las mismas obligaciones; poner en conocimiento de la ACE el flujo transfronterizo con la informacion de la transferencia y el registro de banco de datos; carga de la prueba de la licitud de la transferencia internacional en el responsable.
**A quien aplica:** Responsable de la transferencia.
**Implicacion para el software:** Registro de transferencias (receptor, pais, base, garantias, contrato, fecha de comunicacion a la ACE y acuse). Sin formato oficial de la ACE: el software genera el escrito y registra el envio. Alerta de que la ACE no ha publicado lista de paises adecuados.
**Fuente oficial:** ace_decreto_144.txt Arts. 41, 44, 45, 54, consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO, CONDICIONAL a la existencia de transferencias.

**Norma:** LPDP
**Articulo:** Art. 54 inc. 1; Arts. 26, 27, 29, 30
**Obligacion:** Demostrar la obtencion del consentimiento y la comunicacion de la politica o aviso de privacidad; datos sensibles con consentimiento por escrito y firma autografa o equivalente; revocacion ejecutada en 5 dias habiles e informada al encargado en 5 dias habiles.
**A quien aplica:** Responsable (carga de la prueba).
**Implicacion para el software:** Registro de consentimientos por titular y finalidad, con medio, fecha, version del aviso comunicada, evidencia (archivo, hash, log), estado (vigente/revocado) y tareas de 5 dias habiles al revocar.
**Fuente oficial:** ace_decreto_144.txt Arts. 26-30, 54, consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

**Norma:** LPDP; Lineamientos DPO
**Articulo:** LPDP Art. 23; Lineamientos Art. 38
**Obligacion:** Publicar y comunicar los costos de reproduccion, certificacion y envio; el envio electronico no tiene costo; el valor no puede superar el de materiales o remision.
**A quien aplica:** Responsable.
**Implicacion para el software:** Tabla de costos publicada (preferentemente web), fecha, evidencia de publicacion; validacion de que el envio electronico sea gratuito.
**Fuente oficial:** ace_decreto_144.txt Art. 23; page-11.png, consultado 2026-09-23.
**Vigencia:** VIGENTE.
**Clasificacion:** OBLIGATORIO.

---

## 6. Medidas de seguridad tecnicas: base normativa y evidencia que el software registra sin ejecutar el control

Principio de diseno: PRIV-SV no ejecuta controles de seguridad (no configura 2FA, no cifra bases de datos de terceros, no hace backups del cliente). Registra que el control existe, quien lo opera, con que evidencia y desde cuando, y alerta cuando la evidencia caduca. Toda periodicidad propuesta es sugerencia del producto salvo donde se indique fuente.

| Control | Base normativa | Que registra el software (evidencia) | Periodicidad de revision (origen) |
|---|---|---|---|
| Contrasenas seguras, 2FA, acceso restringido | Politicas Art. 4 Tec. lit. a; LPDP Art. 36 | Inventario de sistemas que tratan datos personales; por sistema: politica de contrasenas vigente (documento), 2FA habilitado (si/no/parcial, captura de configuracion o declaracion del administrador), listado de usuarios con acceso, fecha de ultima revision | Sugerida: semestral (producto); la norma no fija |
| Cifrado en reposo y en transito | Politicas Art. 4 Tec. lit. b y Transf. lit. a (SSL/TLS); Art. 36 | Por sistema y por canal: cifrado en reposo (si/no, tecnologia declarada), TLS en sitios y APIs (evidencia: informe de escaneo o declaracion), certificados y vencimiento | Sugerida: anual o al cambiar sistema |
| Gestion de identidades y perfiles | Politicas Art. 4 Tec. lit. c | Matriz de roles por sistema y area; revision de accesos (fecha, revisor, altas/bajas); evidencia de baja de usuarios al cesar personal | Sugerida: trimestral o semestral |
| Copias de seguridad y recuperacion | Politicas Art. 4 Tec. lit. d ("respaldo periodico") | Plan de respaldo por sistema (frecuencia, ubicacion, cifrado, retencion), evidencia de ultima copia y de ultima prueba de restauracion | La norma dice "periodico"; sugerida: prueba de restauracion anual |
| Firewall, antivirus, IDS/IPS | Politicas Art. 4 Tec. lit. e | Inventario de controles de infraestructura: producto, alcance, responsable, fecha de ultima actualizacion o informe del proveedor | Sugerida: semestral |
| Analisis de vulnerabilidades y pentesting | Politicas Art. 4 Tec. lit. f ("regulares") | Informe (interno o de proveedor), fecha, alcance, hallazgos criticos, plan de remediacion y cierre | La norma dice "regulares"; sugerida: anual, y tras cambios mayores |
| Registros de actividad (logs) | No mencionados literalmente en las Politicas; se derivan de LPDP Art. 5 lit. f ("detectar desviaciones de informacion, intencionales o no") y Art. 25 (documentar vulneraciones); Politicas Fis. lit. b "registros de ingreso" | Declaracion de que sistemas conservan logs de acceso y cambios, plazo de retencion, responsable; el software conserva su propia bitacora de acciones de usuarios | RECOMENDADO en cuanto a alcance; sugerida revision anual |
| Seguridad fisica (acceso, camaras, gabinetes, desastres) | Politicas Art. 4 Fis. lit. a-d | Inventario de ubicaciones con datos fisicos o servidores; controles por ubicacion; evidencia (fotos, procedimientos, bitacoras de ingreso) | Sugerida: anual |
| Eliminacion segura | Politicas Art. 4 Fis. lit. e; LPDP Art. 5 lit. h, Arts. 10-11 | Actas de destruccion o borrado (fecha, metodo, responsable, tratamiento afectado), vinculadas a la politica de retencion y a cancelaciones ARCO-POL | Por evento |
| Contratos y clausulas de confidencialidad con terceros | Politicas Art. 4 Transf. lit. b; LPDP Arts. 33 inc. 2, 34 lit. c, 41 | Registro de proveedores y receptores con contrato adjunto, fecha, clausulas minimas verificadas por checklist | Revision anual sugerida |
| Notificacion de brechas 72 h | Politicas Art. 4 Transf. lit. d; LPDP Art. 25 | Cronologia del incidente con sello de tiempo de conocimiento y de cada notificacion (ACE, FGR, titulares), contenido enviado, acuses | Por evento |
| Digitalizacion: sistemas especializados | Politicas Art. 4 Tec. lit. g | El propio uso de PRIV-SV es evidencia documental de la medida; el software debe generar un reporte de "estado de documentacion del tratamiento" fechado | Continuo |

Regla de honestidad del producto: cada evidencia debe tener tipo (documento, captura, declaracion del responsable, informe de tercero) y el reporte debe distinguir "evidencia aportada" de "control verificado por un tercero". El software nunca marca un control como "cumplido" por si mismo; marca "evidencia registrada" y la fecha.

---

## 7. Certificaciones, sellos y marcas (Art. 50 lit. j, k, l LPDP)

Texto legal: "j) Crear mecanismos de certificacion de la proteccion de datos y de sellos y marcas para los mismos efectos, asi como aprobar que terceros emitan certificaciones sobre dicha materia. k) Realizar una revision periodica de las certificaciones expedidas ... l) Realizar auditorias anuales de las certificaciones expedidas."

Estado al 23 sep 2026:
- No existe ningun mecanismo de certificacion, sello o marca de proteccion de datos para empresas creado por la ACE. No aparece en ace.gob.sv (politicas.php, page/politicas, page/formularios, page/noticias) ni en prensa o firmas legales.
- No existe autorizacion a terceros certificadores.
- Lo unico existente es el "Programa de Certificacion de Delegados de Proteccion de Datos Personales" (Lineamientos Arts. 5 lit. e, 20, 21, 40), que certifica personas, no organizaciones, y que no ha entrado en vigencia.
- Las Politicas Art. 8 lit. c "fomentan" certificaciones internacionales, sin efecto juridico.

Implicacion: el software no debe ofrecer, sugerir ni simular "sello de cumplimiento ACE". Puede registrar certificaciones ISO u otras como informacion. Clasificacion: HECHO (no existen), fuente: ace.gob.sv y ace_decreto_144.txt Art. 50, consultado 2026-09-23.

---

## 8. Inventario de lo publicado por la ACE (Art. 50 lit. n, p, q)

| Publicacion | URL | Fecha | Tipo | Relacion con Art. 50 |
|---|---|---|---|---|
| Decreto 144 LPDP (copia) | https://ace.gob.sv/documentos/decretos/decreto_144_proteccion_datos.pdf | s/f | Ley | - |
| Politicas de Proteccion de Datos 001-0309025-DPDP | https://ace.gob.sv/documentos/politicas/politicas_protecciondatos.pdf | PDF creado 4 sep 2025; vigente 3 sep 2025 (prensa) | Politica de actuacion | lit. i |
| Lineamientos para el Delegado | https://ace.gob.sv/page/documentos/politicas/NDPDDP.pdf | D.O. 11 ago 2026 | Lineamiento | Art. 60 |
| Normativa Procedimiento Administrativo Sancionador | https://ace.gob.sv/page/documentos/politicas/PASDPDP.pdf | D.O. 11 ago 2026 | Normativa procedimental | Art. 53 |
| Formulario de Acceso | https://ace.gob.sv/documentos/formularios/FORMULARIODEACCESOADATOSPERSONALES07072025.pdf | 07-07-2025 | Formulario | lit. q |
| Formulario de Rectificacion | https://ace.gob.sv/documentos/formularios/FORMULARIODERECTIFICACI%C3%93NDEDATOSPERSONALES07072025.pdf | 07-07-2025 | Formulario | lit. q |
| Formulario de Cancelacion o Supresion | https://ace.gob.sv/documentos/formularios/FORMULARIODESOLICITUDDECANCELACI%C3%93NOSUPRESI%C3%93NDEDATOSPERSONALES07072025.pdf | 07-07-2025 | Formulario | lit. q |
| Formulario de Oposicion | https://ace.gob.sv/documentos/formularios/FORMULARIODELDERECHODEOPOSICI%C3%93N07072025.pdf | 07-07-2025 | Formulario | lit. q |
| Formulario de Portabilidad | https://ace.gob.sv/documentos/formularios/FORMULARIODELDERECHODEPORTABILIDAD07072025.pdf | 07-07-2025 | Formulario | lit. q |
| Formulario de Olvido | https://ace.gob.sv/documentos/formularios/FORMULARIODELDERECHOALOLVIDO07072025.pdf | 07-07-2025 | Formulario | lit. q |
| Formulario de Limitacion | https://ace.gob.sv/documentos/formularios/FORMULARIODELDERECHOALALIMITACI%C3%93NDELTRATAMIENTODEDATOSPERSONALES07072025.pdf | 07-07-2025 | Formulario | lit. q |
| Formulario de Nombramiento de Delegado | https://ace.gob.sv/documentos/formularios/FORMULARIODENOMBRAMIENTODEDELEGADODEPROTECCI%C3%93NDEDATOSPERSONALES07072025.pdf | 07-07-2025 | Formulario | Arts. 15-16 |
| Noticia: Primer Webinar Delegado | https://ace.gob.sv/noticia/webinar | 09-09-2026 | Evento | lit. m |
| Noticia: Segundo Webinar Delegado | https://ace.gob.sv/noticia/segundo-webinar-delegado-de-proteccion-de-datos | 11-09-2026 | Evento | lit. m |
| Politica Web y Carta de Derechos del sitio | https://ace.gob.sv/page/politica-web ; https://ace.gob.sv/page/carta-derechos | s/f | Institucional | - |

No localizado en ace.gob.sv al 23 sep 2026:
- Guias de implementacion de la ley (Art. 50 lit. n): ninguna.
- Clausulas contractuales recomendadas (Art. 50 lit. p): ninguna.
- Formulario de revocacion del consentimiento (Art. 50 lit. q): ninguno; solo existen los 7 formularios ARCO-POL y el de nombramiento. Las URL de los formularios se obtuvieron de la pagina https://ace.gob.sv/page/formularios; las que no estan en el corpus local (rectificacion, oposicion, olvido, limitacion) no fueron descargadas ni verificadas en contenido.
- Comunicado que deja sin efecto el plazo del 16 sep 2026: no visible en la seccion de noticias; conocido por prensa.
- Plataforma del Registro de Delegados y lista publica de delegados: no habilitadas.
- Programa de Certificacion de Delegados: no publicado.

Implicacion: el software debe traer los 8 formularios oficiales como plantillas de recepcion (Lineamientos Art. 32) y ofrecer un formulario propio de revocacion del consentimiento marcado como "modelo del producto, la ACE no ha publicado uno".

---

## 9. Modelo de evidencia frente a la ACE

Fundamentos:
- LPDP Art. 50 lit. a (control, inspeccion y supervision), lit. t (solicitar "antecedentes, documentos, programas u otros elementos relativos al tratamiento"), Art. 56 lit. a num. 9 (infraccion leve no atender solicitudes de la ACE) y lit. b num. 4 (grave obstaculizar auditorias o inspecciones).
- LPDP Art. 54: carga de la prueba del consentimiento, del aviso y de las transferencias internacionales en el responsable.
- Normativa PAS Art. 10: en diligencias preliminares la ACE puede requerir informes o antecedentes, inspecciones o verificaciones tecnicas, entrevistas, analisis documental o pericial. Art. 24: constituyen prueba "los instrumentos publicos, los autenticos, los instrumentos privados, las declaraciones de testigos, los resultados de peritajes, la inspeccion de los lugares o de las cosas, la confesion, los informes de auditoria internos o externos, cualquier otra informacion que hubiese sido proporcionada por el presunto infractor". Art. 38: seguimiento de medidas correctivas "mediante requerimientos de cumplimiento, inspecciones o auditorias".

Diseno funcional derivado:

```
Requisito (ley / politica / lineamiento)
   |
   v
Control o documento asignado a un responsable interno
   |
   v
Evidencia (tipo, fecha, autor, archivo o declaracion, version)
   |
   v
Expediente exportable por periodo -> respuesta a requerimiento de la ACE
   |
   v
Bitacora inalterable de quien registro que y cuando
```

El expediente debe poder generarse para: un tratamiento, un incidente, una solicitud ARCO-POL, una transferencia internacional, una auditoria anual, o un periodo completo.

---

## 10. Incertidumbres y puntos que requieren abogado

1. Publicacion de las Politicas ACE en el Diario Oficial: no confirmada. Si nunca se publicaron en el D.O., un abogado debe opinar sobre su eficacia frente a terceros (la LPA exige publicidad de disposiciones de caracter general) y sobre la defensa posible en un procedimiento sancionador. Las fechas de emision (2 sep 2025) y vigencia (3 sep 2025) provienen de prensa.
2. Alcance indeterminado de RAT, EIPD, auditorias, politica interna, capacitacion y medidas tecnicas: la ACE no ha publicado guias (Art. 50 lit. n). Riesgo de que fije el estandar en inspeccion. Toda plantilla del producto debe presentarse como referencia.
3. Referencias cruzadas erroneas en las Politicas (Art. 8 lit. b a Art. 50 lit. l; Art. 9 a Art. 24 lit. g; Art. 3 lit. h a Art. 5 lit. i): debilitan la base legal de la "auditoria anual" como obligacion legal; sigue siendo obligacion por la Politica misma.
4. Reforma 659: texto oficial no localizado; publicacion en D.O. no confirmada; se desconoce la redaccion exacta del Art. 16 reformado y si conserva las funciones de formacion (lit. f) y publicacion del aviso (lit. g) como deberes del sujeto obligado. Se desconoce si el Art. 24 lit. f (nombre del delegado en el aviso) fue ajustado.
5. Destino de los Lineamientos DPO para el sector privado tras la reforma: no derogados formalmente; su Art. 3 los declara obligatorios para delegado, encargado y responsable. Un delegado voluntario privado podria quedar sujeto a certificacion y registro. Requiere criterio de la ACE o abogado.
6. Destino de la medida organizativa "Delegado" de las Politicas ACE (Art. 4 lit. b, Art. 8 lit. a) para el sector privado tras la reforma.
7. Comunicado de la ACE que deja sin efecto el 16 sep 2026: conocido por prensa; no se localizo en ace.gob.sv. No se sabe si tambien suspende la obligacion de comunicar nombramientos (Art. 10) o solo la fecha transitoria (Art. 40).
8. Computo de la vigencia de los Lineamientos: "ocho dias despues contados a partir del dia siguiente de su publicacion" admite 19 o 20 ago 2026; la practica reportada es 19 ago.
9. Plazo de adecuacion del Art. 60 inc. 2 (3 meses desde la emision de las Politicas, aprox. 2-3 dic 2025): la ACE no ha comunicado si considera vencido el periodo de gracia. Las empresas deben asumir que ya es exigible.
10. Retencion de 10 anos de la documentacion del aviso (Lineamientos Art. 31) y de 5 anos de confidencialidad del delegado (Art. 36): plazos que un abogado debe armonizar con otras normas (mercantil, tributaria, laboral) para una politica de retencion unica.
11. Lista de paises con nivel adecuado de proteccion (Art. 44): no existe. La Politica exige "proteccion equivalente"; la ley admite garantias del emisor. Riesgo de infraccion muy grave (Art. 56 lit. c num. 5). Toda transferencia internacional requiere revision legal.
12. Canal y formato para "poner en conocimiento" de la ACE los flujos transfronterizos (Art. 45): no publicado.
13. Ley de Ciberseguridad (Decreto 143) y sus Politicas de Ciberseguridad de la ACE: no analizadas en este lente; podrian imponer controles adicionales a ciertos sujetos (infraestructura critica, sector publico). Verificar en otro sweep si el cliente pertenece a esos sectores.
14. Aplicacion de la normativa sancionadora y del catalogo de infracciones al encargado (Art. 36 inc. 2 lo obliga a las medidas de seguridad): la sancion recae sobre "sujetos obligados"; un abogado debe aclarar la exposicion del encargado.

---

## 11. Fuentes consultadas (fecha de consulta 2026-09-23)

Fuentes primarias locales:
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt (LPDP, Arts. 5, 15-17, 23-25, 30, 33-36, 41, 44-45, 50, 54, 56-57, 60-61).
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_politicas_protecciondatos.txt y .pdf (Politicas 001-0309025-DPDP; metadatos del PDF leidos con pypdf).
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\lineamientos_dpo_OCR.txt, verificado contra C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ocr\lineamientos_dpo\page-02.png, page-04.png, page-06.png, page-07.png, page-08.png, page-09.png, page-10.png, page-11.png.
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\normativa_sancionadora_OCR.txt (Arts. 10, 24, 37, 38).
- C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_form_nombramiento_delegado.txt.
- C:\Proyects\PRIV-SV\analisis\00_contexto_para_agentes.md (hechos verificados por el equipo).

Fuentes primarias en linea:
- https://ace.gob.sv/politicas.php y https://ace.gob.sv/page/politicas (inventario de documentos).
- https://ace.gob.sv/page/formularios (8 formularios, version 07-07-2025).
- https://ace.gob.sv/page/noticias , https://ace.gob.sv/noticia/webinar , https://ace.gob.sv/noticia/segundo-webinar-delegado-de-proteccion-de-datos
- https://www.asamblea.gob.sv/node/14116 (nota oficial sobre la reforma, 17 sep 2026).

Fuentes secundarias (prensa y firmas legales):
- Diario El Mundo, "Vigentes politicas de actuacion y manejo de datos personales de los salvadorenos", 12 sep 2025: https://diario.elmundo.sv/politica/vigentes-politicas-de-actuacion-y-manejo-de-datos-personales-en-el-salvador
- La Prensa Grafica, "La Agencia de Ciberseguridad del Estado emite politica de manejo de datos personales con atraso segun expertos", 12 sep 2025 (solo titular; cuerpo inaccesible, HTTP 403): https://www.laprensagrafica.com/elsalvador/La-Agencia-de-Ciberseguridad-del-Estado-emite-politica-de-manejo-de-datos-personales-con-atraso-segun-expertos-20250912-0095.html
- Diario El Mundo, "Delegados de proteccion de datos personales deberan ser certificados por la ACE", 28 ago 2026: https://diario.elmundo.sv/politica/delegados-de-proteccion-de-datos-personales-deberan-ser-certificados-por-la-agencia-de-ciberseguridad-del-estado-ace
- EY, "La ACE desarrolla aspectos relevantes de la Ley de Proteccion de Datos Personales": https://www.ey.com/es_ce/technical/tax/tax-alerts/el-salvador-la-agencia-de-ciberseguridad-del-estado-desarrolla-aspectos-relevantes-de-la-ley-de-proteccion-de-datos-personales
- El Diario de Hoy, "Sin fecha para nombrar delegados de proteccion de datos personales", 12 sep 2026: https://www.eldiariodehoy.com/noticias/nacionales/sin-fecha-para-nombrar-delegados-de-proteccion-de-datos-personales/93083/2026/
- elsalvador.com, "Cambia plazo para nombrar delegado de proteccion de datos", 12 sep 2026: https://www.elsalvador.com/dinero-y-negocios/entorno-economico/empresas-ley-de-proteccion-datos-el-salvador/1292968/2026/
- ContraPunto, "Sin fecha para nombrar a los delegados ... la ACE establece el registro obligatorio", 13 sep 2026: https://www.contrapunto.com.sv/sin-fecha-para-nombrar-a-los-delegados-de-proteccion-de-datos-personales-la-ace-establece-el-registro-obligatorio/
- El Diario de Hoy, "Asamblea deroga obligatoriedad de empresas privadas de nombrar delegados", 17 sep 2026: https://www.eldiariodehoy.com/noticias/nacionales/asamblea-legislativa-deroga-obligatoriedad-de-las-empresas-privadas-de-nombrar-delegados-de-proteccion-de-datos-personales/93615/2026/
- elsalvador.com, "Aprueban reforma a la Ley de Proteccion de Datos Personales, que cambia?", 17 sep 2026: https://www.elsalvador.com/noticias/nacional/reforma-proteccion-datos-personales/1293875/2026/
- El Diario de Hoy (opinion), "Se elimina el delegado de las empresas, pero no la responsabilidad", 18 sep 2026: https://www.eldiariodehoy.com/opinion/se-elimina-el-delegado-de-las-empresas-pero-no-la-responsabilidad-de-proteger-los-datos-de-las-personas/93642/2026/
- BLP Legal, "Registro obligatorio del delegado" (cuerpo inaccesible, HTTP 403): https://blplegal.com/es/delegado-proteccion-datos-el-salvador-ace/
- Consortium Legal, "Delegado de Proteccion de Datos en El Salvador: actualizaciones", 2 sep 2026 (sin fechas concretas): https://consortiumlegal.com/2026/09/02/delegado-proteccion-datos-el-salvador/
