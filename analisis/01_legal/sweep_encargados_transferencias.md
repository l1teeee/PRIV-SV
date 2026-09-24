# Sweep juridico: responsable, encargado, proveedores, contratos y transferencias nacionales e internacionales

Proyecto: PRIV-SV (plataforma SaaS B2B de autogestion de proteccion de datos, El Salvador)
Lente: Responsable, encargado, proveedores, contratos y transferencias nacionales e internacionales
Fecha de consulta de todas las fuentes: 2026-09-23 (verificacion adicional sobre el numero de decreto de la reforma LPDP realizada el 2026-09-24, ver seccion 11.1)
Norma principal: Ley para la Proteccion de Datos Personales (LPDP), Decreto Legislativo N. 144, D.O. N. 219, Tomo 445, 15 nov 2024, vigente desde el 23 nov 2024 (Art. 64).

Convenciones: "LPDP" = la ley; "Politicas ACE" = Politicas N. 001-0309025-DPDP de Actuacion y Manejo de Datos Personales; "Lineamientos DPO" = Lineamientos para el Delegado de Proteccion de Datos Personales (D.O. 11 ago 2026); "Normativa PAS" = Normativa para el Desarrollo del Procedimiento Administrativo Sancionador (D.O. 11 ago 2026). Rutas locales apuntan a `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\`.

---

## 1. Resumen ejecutivo

1. La LPDP distingue con claridad al **responsable** (quien decide finalidad y medios, Art. 4 lit. p) del **encargado** (quien trata por cuenta del responsable, Art. 4 lit. j). La **transferencia** (Art. 4 lit. u) es, por definicion, una comunicacion a persona **distinta** del responsable o del encargado, hecha con consentimiento previo e informado del titular. Por tanto, el acceso a datos por un encargado (proveedor que trata por cuenta del responsable) no es, en el texto legal, una "transferencia" en sentido estricto. Esta distincion es la piedra angular del modelo de datos del producto.

2. Sin embargo, la ley no es del todo coherente: las definiciones de **emisor** (Art. 4 lit. k) y **receptor** (Art. 4 lit. o) de datos en transferencias internacionales incluyen expresamente al encargado, y el Art. 45 habla de "flujo transfronterizo" sin distinguir entre transferencia y encargo. La lectura conservadora, que se recomienda para el diseno, es que **todo envio de datos personales a un proveedor situado fuera de El Salvador (incluida la nube) debe tratarse como flujo transfronterizo sujeto a los Arts. 44 y 45**, aunque juridicamente sea un encargo y no una transferencia. Este punto requiere confirmacion de abogado.

3. Obligaciones del encargado: la ley le impone directamente las obligaciones del Art. 34 (limitar el tratamiento a la finalidad, implementar medidas de seguridad y politicas de actuacion, confidencialidad), el Art. 36 (medidas de seguridad de la ACE, de "obligatorio cumplimiento para el encargado") y, via Art. 33 inc. 2, el sometimiento a la ley y a los lineamientos del responsable y de la ACE. Los Lineamientos DPO (Art. 3) y las Politicas ACE (Art. 4) confirman que son de cumplimiento obligatorio tambien para el encargado.

4. Contratos: el unico contrato exigido expresamente por la LPDP para el sector privado es el del Art. 41 (contrato del responsable de la transferencia con el "responsable receptor", con al menos las mismas obligaciones). No existe en la ley un articulo que exija un contrato escrito responsable-encargado con contenido minimo tipo GDPR Art. 28. No obstante, las Politicas ACE (Art. 4, "Medidas de Seguridad en Transferencias de Datos", lit. b) exigen "Contratos de Confidencialidad y Contratos para la Transferencia de Datos: Acuerdos legales con terceros que tratan datos", y el incumplimiento de las medidas de seguridad de las politicas es infraccion grave (Art. 56 lit. b num. 7). Conclusion practica: un contrato o DPA con cada proveedor con acceso a datos es exigible como medida de seguridad obligatoria, aunque su contenido minimo no esta definido por norma.

5. Clausulas modelo: la ACE tiene la atribucion de "recomendar clausulas contractuales" (Art. 50 lit. p). Al 2026-09-23 **no se ha localizado ninguna clausula modelo, contrato tipo ni guia de contratacion publicada por la ACE** (verificado en https://ace.gob.sv/page/formularios y https://ace.gob.sv/politicas.php). El producto debe suministrar su propia plantilla de contenido minimo, marcada como buena practica.

6. Transferencias nacionales (Art. 40): requieren consentimiento previo del titular, informacion sobre la finalidad de la transferencia e identificacion del cesionario (o elementos que permitan identificarlo), fines directamente relacionados con el interes legitimo del titular o del responsable, y contrato con el receptor (Art. 41). Transferir sin consentimiento es infraccion muy grave (Art. 56 lit. c num. 6). Ademas, el Art. 21 inc. 3 obliga a notificar a quienes hayan recibido los datos toda rectificacion, actualizacion o eliminacion dentro de los 5 dias habiles siguientes a la procedencia de la solicitud, y el Art. 8 obliga a comunicar al titular si se ha intercambiado su informacion con otras entidades. Esto exige que el software lleve un **registro de receptores por titular o por conjunto de datos**.

7. Transferencias internacionales (Art. 44): solo se permiten a paises u organismos que cumplan "como minimo" los principios de la LPDP o los estandares internacionales; la ley **no dice quien declara el nivel adecuado** y la ACE **no ha publicado ninguna lista de paises adecuados** (no localizada en fuentes oficiales al 2026-09-23). Si el pais no tiene nivel adecuado, "el pais emisor" (en la practica, el responsable) debe garantizar que el tratamiento se haga conforme a la LPDP. Siempre debe mediar consentimiento previo del titular salvo excepciones en instrumentos internacionales reciprocos. Hay excepcion para los tratados de Integracion Economica Centroamericana, pero no se ha localizado ningun instrumento regional que regule transferencias de datos personales, por lo que la excepcion carece hoy de desarrollo practico. La carga de la prueba recae en el responsable de la transferencia (Art. 54 inc. 2). Transferir a pais sin nivel de proteccion es infraccion muy grave (Art. 56 lit. c num. 5).

8. Art. 45: la opinion previa de la ACE es opcional ("podran solicitar"), pero "en cualquier caso, el flujo transfronterizo de datos personales se pondra en conocimiento" de la ACE, "incluyendo la informacion que se requiere para la transferencia de datos personales y el registro de banco de datos". **Hallazgo critico: al 2026-09-23 la ACE no ha habilitado ningun formulario, plataforma, procedimiento ni registro de bancos de datos para cumplir esta obligacion.** Tampoco existe en la LPDP una obligacion general de inscribir bases de datos ante la ACE: el unico registro creado hasta la fecha es el Registro de Delegados (Lineamientos DPO Arts. 10 y 11), cuya plataforma no esta habilitada y cuya fecha limite transitoria fue dejada sin efecto por la ACE tras el anuncio de la reforma. La obligacion del Art. 45 esta vigente pero es hoy de cumplimiento indeterminado; el producto debe generar el expediente listo para remitir y dejar constancia del intento o de la imposibilidad.

9. Reforma de septiembre de 2026 (decreto legislativo aprobado el 17 sep 2026 con 57 votos; **numero de decreto no confirmado en fuente oficial primaria al 2026-09-24** -- ver nota de verificacion en la seccion 11.1 --, texto oficial no localizado, publicacion en D.O. no confirmada): segun prensa, deroga el Art. 17 (deber de asistencia de "cada dependencia, empleado o proveedor" al delegado) y reforma el Art. 16 de modo que los sujetos obligados "deberan auxiliar a sus dependencias o proveedores y fijar lineamientos internos" para gestionar solicitudes ARCO-POL, y, "de existir un encargado del tratamiento, informarle en un plazo identico de 5 dias habiles" (revocacion). Ningun reporte menciona cambios a los Arts. 4, 7, 24, 33, 34, 36, 40, 41, 44, 45 o 54. Este lente, por tanto, no cambia sustancialmente con la reforma, salvo la referencia al delegado en los Arts. 21 y 30 (que pasaria al sujeto obligado).

10. Medidas de seguridad en transferencias (Politicas ACE Art. 4 y Art. 6 lit. d): protocolos seguros SSL/TLS, contratos de confidencialidad y de transferencia, transferencias internacionales solo a paises con proteccion equivalente y notificacion de brechas en 72 horas. Son de cumplimiento obligatorio (Politicas Art. 2; LPDP Arts. 35 y 36) y su incumplimiento es infraccion grave (Art. 56 lit. b num. 7).

---

## 2. Marco normativo aplicable a este lente y estado de vigencia

| Instrumento | Tipo | Articulos relevantes para este lente | Vigencia al 2026-09-23 | Fuente |
|---|---|---|---|---|
| Ley para la Proteccion de Datos Personales, D.L. 144 | Ley | 2, 4 lit. b, j, k, n, o, p, r, t, u; 5 lit. f, i; 7; 8; 17; 21; 24 lit. c, h; 25; 30; 32; 33; 34; 35; 36; 40; 41; 44; 45; 49; 50 lit. a, i, n, p, t; 54; 56; 57; 59 | VIGENTE (desde 23 nov 2024) | `ace_decreto_144.txt`; `diario_oficial_2024-11-15_mh.txt`; https://www.asamblea.gob.sv/sites/default/files/documents/decretos/7A4FBD85-7E1B-46BE-9408-6FC549E53E00.pdf |
| Politicas N. 001-0309025-DPDP, Politicas de Actuacion y Manejo de Datos Personales | Politica de actuacion de la ACE (imperativa, Art. 35 LPDP) | 2 (ambito, incluye operaciones internacionales), 4 (medidas organizativas, tecnicas, fisicas y de transferencia), 6 lit. d, 8 | VIGENTE. Segun prensa (diario.elmundo.sv, 12 sep 2025) emitidas el 2 sep 2025 y vigentes desde el 3 sep 2025; la fecha no consta en el texto local | `ace_politicas_protecciondatos.txt`; https://ace.gob.sv/politicas.php |
| Lineamientos para el Delegado de Proteccion de Datos Personales | Lineamiento de la ACE | 1, 2, 3 (obligatorios para el encargado), 10, 11 (Registro de Delegados), 15 inc. final (contrato con delegado extranjero), 23, 27, 37, 39, 40 | VIGENTE (D.O. 11 ago 2026, Tomo 452, N. 146; vigencia 8 dias despues, 19 ago 2026). Parcialmente afectados por la reforma pendiente | `lineamientos_dpo_OCR.txt`; `ocr/lineamientos_dpo/page-02.png`; https://ace.gob.sv/page/documentos/politicas/NDPDDP.pdf |
| Normativa para el Desarrollo del Procedimiento Administrativo Sancionador (LPDP) | Normativa de la ACE | 2 (aplicable a todos los sujetos obligados del Art. 2 LPDP) | VIGENTE (D.O. 11 ago 2026, vigente 19 ago 2026) | `normativa_sancionadora_OCR.txt`; https://ace.gob.sv/page/documentos/politicas/PASDPDP.pdf |
| Decreto legislativo de reforma LPDP (numero no confirmado; ver 11.1) | Ley (reforma) | Segun prensa: deroga 15 y 17; reforma 16, 47 y 51 | APROBADA-PENDIENTE-PUBLICACION (aprobada 17 sep 2026; vigencia 8 dias despues de publicacion en D.O.; publicacion no confirmada; texto no localizado) | https://www.asamblea.gob.sv/node/14116; https://www.eldiariodehoy.com/noticias/nacionales/asamblea-legislativa-deroga-obligatoriedad-de-las-empresas-privadas-de-nombrar-delegados-de-proteccion-de-datos-personales/93615/2026/ |
| Tratado General de Integracion Economica Centroamericana (1960) y Protocolo de Guatemala (1993) | Tratados internacionales | Referidos por el Art. 44 inc. 4 LPDP | VIGENTES, pero no contienen (segun lo localizado) reglas sobre transferencia de datos personales | https://www.sica.int/documentos/protocolo-al-tratado-general-de-integracion-economica-centroamericana-protocolo-de-guatemala_1_116843.html |

Nota sobre el corpus: el archivo `diario_oficial_2024-11-15_mh.txt` contiene el texto del Decreto 144 tal como fue publicado (paginas 24 a 62 del D.O.); el texto de `ace_decreto_144.txt` (copia de la ACE) coincide en todos los articulos citados en este informe.

---

## 3. Definiciones del Art. 4 relevantes para este lente

### 3.1 Transcripcion textual (Art. 4 LPDP, copia ACE)

> b) Base de datos o repositorio: conjunto organizado de datos personales que sean objeto de tratamiento o procesamiento, electrónico o no, cualquiera que fuere la modalidad de su formación, almacenamiento, organización o acceso.

> j) Encargado del tratamiento (Encargado): persona natural o jurídica, pública o privada, que sola o en conjunto con otros, realice el tratamiento de datos personales por cuenta del responsable del tratamiento.

> k) Emisor de datos personales: titular del banco de datos personales, o aquel que resulte encargado de su tratamiento en El Salvador, que realice una transferencia de datos personales a otro país de conformidad a lo dispuesto en la presente ley.

> n) Medidas de Seguridad: políticas, acciones o procedimientos de control o grupo de controles que garanticen la protección de los datos personales contenidos en registros o archivos físicos o electrónicos, de accesos no autorizados garantizando la confidencialidad, integridad y disponibilidad.

> o) Receptor de datos personales: toda persona natural o jurídica, pública o privada, que recibe los datos en caso de transferencia internacional, ya sea como titular, encargado de datos personales o tercero.

> p) Responsable de tratamiento (Responsable): persona natural o jurídica, pública o privada, administradora de la base de datos y/o repositorio, o quien decida sobre la finalidad y medios del tratamiento de los datos personales que administre o posea.

> r) Sitios de Contingencia: sitio alterno o secundario en el cual se replican de forma continua o discontinua los datos almacenados en servidores informáticos físico o virtuales que residen en un lugar principal.

> t) Tratamiento de datos: cualquier operación o conjunto de operaciones efectuadas mediante procedimientos automatizados o manuales y aplicadas a datos personales. Estas se relacionan con la obtención, uso, registro, organización, conservación, difusión, almacenamiento, posesión, acceso, manejo y divulgación de datos personales.

> u) Transferencia de datos personales: toda comunicación de datos personales realizada a persona distinta del responsable o encargado del tratamiento, con el consentimiento previo e informado de su titular.

Fuente: `ace_decreto_144.txt`, paginas 3 y 4; confirmado con `diario_oficial_2024-11-15_mh.txt` lineas 268 a 320. Consulta 2026-09-23. Vigencia: VIGENTE.

### 3.2 Analisis de las definiciones

| Concepto | Que dice la ley | Observaciones para el producto |
|---|---|---|
| Responsable | Administrador de la base de datos y/o repositorio, o quien decide finalidad y medios. Definicion doble: por administracion o por decision. | Una empresa que administra una base (aunque no haya decidido su finalidad, p. ej. una filial que hereda datos) puede ser responsable. El software debe permitir marcar mas de un responsable por base de datos (corresponsabilidad de hecho), aunque la ley no regula la corresponsabilidad. |
| Encargado | Trata por cuenta del responsable, "sola o en conjunto con otros". | Cubre proveedores de nube, SaaS, call centers, planillas externas, mensajeria, destruccion de documentos, etc. "En conjunto con otros" abre la puerta a subencargados, que la ley no regula expresamente. |
| Transferencia | Comunicacion a persona distinta del responsable o encargado, con consentimiento previo e informado. | La definicion incorpora el consentimiento como elemento constitutivo: una comunicacion sin consentimiento no es una "transferencia licita" sino una infraccion (Art. 56 lit. c num. 6). El envio a un encargado queda fuera de la definicion. |
| Emisor | Titular del banco de datos o encargado en El Salvador que transfiere a otro pais. | Aqui la ley admite que un encargado ubicado en El Salvador sea emisor de una transferencia internacional. Un proveedor salvadoreno que envia datos de su cliente a su propia nube extranjera puede ser "emisor". |
| Receptor | Quien recibe los datos en transferencia internacional "ya sea como titular, encargado de datos personales o tercero". | La ley considera que un encargado extranjero puede ser "receptor" de una transferencia internacional. Esto contradice parcialmente la definicion de transferencia (lit. u) y es la razon de la lectura conservadora del punto 3.3. |
| Base de datos / repositorio / banco de datos | La ley usa los tres terminos; solo define "base de datos o repositorio". "Banco de datos" aparece en Arts. 4 lit. k, 9, 18, 22, 45, 56 y 59 sin definicion. | El producto debe tratar los tres terminos como sinonimos y usar un unico objeto "base de datos / activo de datos". |
| Sitios de contingencia | Replica de datos en sitio alterno. | Los sitios de contingencia y respaldos deben informarse al titular (Art. 7 lit. b) y son, en la practica, encargados o infraestructura propia; si estan en el extranjero, son flujo transfronterizo. |
| Medidas de seguridad | Controles que garantizan confidencialidad, integridad y disponibilidad. | Su concrecion esta en las Politicas ACE Art. 4. |

### 3.3 Transferencia versus acceso por encargado

```
                           +-----------------------------+
                           |  Titular (persona natural)  |
                           +-------------+---------------+
                                         |
                       consentimiento / base de licitud (Art. 5 lit. g)
                                         |
                                         v
     +----------------------+  encargo   +--------------------------+
     |  RESPONSABLE         | ---------> |  ENCARGADO (proveedor)   |
     |  decide fin y medios |  Art.4 j   |  trata por cuenta del    |
     |  Art. 4 lit. p       | <--------- |  responsable             |
     +----------+-----------+  Arts. 33  |  Arts. 34, 36            |
                |              inc.2, 34 +------------+-------------+
                |                                     |
   transferencia (Art. 4 lit. u)           subencargado / nube propia
   consentimiento previo (Art. 40)         (no regulado expresamente;
   contrato (Art. 41)                       "en conjunto con otros")
                |                                     |
                v                                     v
     +----------------------+             +--------------------------+
     |  RESPONSABLE RECEPTOR|             |  Infraestructura en el   |
     |  o TERCERO           |             |  extranjero = flujo      |
     |  (cesionario)        |             |  transfronterizo         |
     +----------------------+             |  (Arts. 44 y 45, lectura |
                                          |  conservadora)           |
                                          +--------------------------+

   Si el receptor o el encargado esta fuera de El Salvador:
   Art. 44 (nivel adecuado, garantias, consentimiento) + Art. 45 (poner
   en conocimiento de la ACE) + Art. 54 inc. 2 (carga de la prueba).
```

Criterios operativos que el software puede ofrecer al usuario para clasificar cada flujo (orientacion, no decision juridica):

| Pregunta | Si la respuesta es SI | Si la respuesta es NO |
|---|---|---|
| El tercero decide para que y como usa los datos (fines propios)? | Es transferencia a otro responsable: Arts. 40, 41; consentimiento previo. | Sigue a la siguiente pregunta. |
| El tercero solo ejecuta instrucciones de la empresa (servicio) y no usa los datos para fines propios? | Es encargado: Arts. 33 inc. 2, 34, 36; contrato/DPA (Politicas ACE Art. 4); aviso Art. 24 lit. h; Art. 7 lit. c. | Es probablemente transferencia; consultar abogado. |
| El tercero o su infraestructura esta fuera de El Salvador? | Ademas: Arts. 44, 45, 54 inc. 2; expediente de flujo transfronterizo. | Solo reglas nacionales. |
| El tercero es un organo o entidad publica? | Aplican Arts. 46 a 49 al receptor; el privado que transfiere sigue sujeto a Arts. 40 y 41. | No aplica el Titulo III. |

---

## 4. Obligaciones del encargado y del responsable respecto de proveedores

### 4.1 Proveedores subcontratados sometidos a la ley y a lineamientos

**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 33 inciso 2
**Obligacion:** "En los casos en el que el responsable subcontrate servicios en los cuales se conceda acceso a los datos personales, estos proveedores deberán someterse a la presente ley y a los lineamientos que el responsable y la Entidad Rectora establezca para garantizar el adecuado tratamiento de los datos personales."
**A quien aplica:** Al responsable (debe establecer lineamientos y asegurar el sometimiento) y al proveedor con acceso a datos (debe someterse a la ley y a esos lineamientos).
**Implicacion para el software:** Inventario de proveedores con acceso a datos personales; para cada uno, evidencia de "sometimiento" (contrato, DPA, aceptacion de lineamientos internos); modulo de "lineamientos para proveedores" que la empresa pueda emitir y adjuntar; alerta si un proveedor con acceso no tiene evidencia de sometimiento.
**Fuente oficial:** `ace_decreto_144.txt` pagina 17; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (CONDICIONAL a que exista subcontratacion con acceso a datos)

### 4.2 Obligaciones comunes del responsable y del encargado

**Norma:** LPDP
**Articulo:** Art. 34
**Obligacion:** "El responsable, y en su caso el encargado del tratamiento de datos, además del cumplimiento de los principios establecidos en la presente ley, tendrá las obligaciones siguientes: a) Limitar el tratamiento de los datos personales de conformidad a la finalidad para la que se emitió el consentimiento por parte del titular. b) Implementar las medidas de seguridad y cumplir con las políticas de actuación conforme a la presente ley. c) Guardar confidencialidad en el tratamiento de los datos personales. d) Cualquier otra obligación que le atribuya la presente ley."
**A quien aplica:** Responsable y encargado, directamente. Es la unica norma de la LPDP que enumera obligaciones "del encargado" como tales.
**Implicacion para el software:** El contrato o DPA que el producto ayude a documentar debe reflejar al menos estas tres obligaciones (finalidad, seguridad y politicas de actuacion, confidencialidad). Cuando el cliente de PRIV-SV actua como encargado de otros (p. ej. un BPO), el software debe soportar el "modo encargado": registrar al responsable-cliente, la finalidad instruida y las medidas exigidas.
**Fuente oficial:** `ace_decreto_144.txt` pagina 17; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 4.3 Medidas de seguridad de la ACE, obligatorias tambien para el encargado

**Norma:** LPDP
**Articulo:** Art. 36
**Obligacion:** "El responsable deberá acatar y mantener las medidas de seguridad establecidas por la Entidad Rectora (...) El responsable deberá aplicar los mecanismos tecnológicos, regulatorios y procedimentales que garanticen el cumplimiento de las características de seguridad de información. Lo dispuesto en este artículo también será de obligatorio cumplimiento para el encargado del tratamiento de datos personales."
**A quien aplica:** Responsable y encargado.
**Implicacion para el software:** Checklist de medidas de las Politicas ACE (Art. 4) aplicable tanto a la empresa como a cada proveedor; el proveedor debe poder acreditar (documentalmente) las medidas tecnicas (2FA, cifrado en reposo y transito, gestion de identidades, backups, firewall/IDS, analisis de vulnerabilidades) y el software debe guardar la evidencia (certificaciones, informes, cuestionarios).
**Fuente oficial:** `ace_decreto_144.txt` pagina 17; Politicas ACE Art. 4 en `ace_politicas_protecciondatos.txt` paginas 3 y 4; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 4.4 Politicas de actuacion: medidas aplicables a responsables y encargados

**Norma:** Politicas N. 001-0309025-DPDP (ACE)
**Articulo:** Art. 2 (ambito) y Art. 4 (medidas)
**Obligacion:** Art. 2: "Estas políticas son de cumplimiento obligatorio para todas las entidades públicas y privadas que recolecten, almacenen, procesen o transfieran datos personales en El Salvador. También aplican a operaciones internacionales vinculadas a ciudadanos salvadoreños." Art. 4: "Estas medidas deben ser implementadas por los responsables y encargados del tratamiento de datos, y su incumplimiento puede llevar a sanciones."
**A quien aplica:** Responsables y encargados, publicos y privados; y "operaciones internacionales vinculadas a ciudadanos salvadorenos" (alcance extraterritorial declarado por la ACE, cuyo respaldo legal en la LPDP es discutible y requiere abogado).
**Implicacion para el software:** El perfil de cada proveedor debe registrar si "procesa o transfiere datos en El Salvador" o si es una "operacion internacional vinculada a ciudadanos salvadorenos"; en ambos casos el checklist de medidas ACE le es exigible.
**Fuente oficial:** `ace_politicas_protecciondatos.txt` paginas 2 y 3; https://ace.gob.sv/politicas.php; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 4.5 Derecho del titular a conocer a los proveedores de almacenamiento en la nube

**Norma:** LPDP
**Articulo:** Art. 7 inciso 1 y lit. c
**Obligacion:** "El titular de sus datos personales tendrá derecho a conocer quienes resguardarán éstos. Este derecho incluye también a los proveedores de servicios de almacenamiento tercerizados, como el encargado del tratamiento de datos personales que fue contratado por el responsable a tales efectos y que utiliza como medio de almacenamiento la nube u otra infraestructura." Al recabar datos debe informarse "c) La identidad, domicilio, correo electrónico, número telefónico y cualquier información que facilite contactar al responsable y al encargado del tratamiento, o a sus respectivos representantes", y "b) La existencia de la base de datos o repositorio, así como los respaldos y sitios de contingencia, en el caso que aplique".
**A quien aplica:** Responsable (obligacion de informar). Incumplir el Art. 7 es infraccion leve (Art. 56 lit. a num. 8).
**Implicacion para el software:** El generador de politica de privacidad y de aviso debe tomar automaticamente del inventario de proveedores la lista de encargados (incluida la nube) con sus datos de contacto, y la lista de respaldos y sitios de contingencia. Cambio de proveedor de nube = cambio de aviso y politica + comunicacion a titulares por el medio informado (Art. 24 lit. g).
**Fuente oficial:** `ace_decreto_144.txt` paginas 6 y 7; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 4.6 Datos de contacto del encargado en el aviso de privacidad

**Norma:** LPDP
**Articulo:** Art. 24 lit. h
**Obligacion:** El aviso de privacidad contendra al menos "h) Los datos de contacto de la entidad subcontratada encargada del tratamiento de datos personales, en caso de existir."
**A quien aplica:** Responsable.
**Implicacion para el software:** Campo obligatorio del aviso vinculado al inventario de encargados; validacion que impida marcar el aviso como "completo" si existen encargados registrados sin datos de contacto en el aviso.
**Fuente oficial:** `ace_decreto_144.txt` pagina 14; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (CONDICIONAL a la existencia de encargado)

### 4.7 Infraccion leve por no publicar datos de contacto del encargado

**Norma:** LPDP
**Articulo:** Art. 56 lit. a num. 2 y Art. 57 lit. a
**Obligacion:** Es infraccion leve "No publicar los datos de contacto del encargado del tratamiento." Multa de 1 a 10 salarios minimos mensuales del sector comercio.
**A quien aplica:** Responsable.
**Implicacion para el software:** Control de cumplimiento con severidad asociada (leve) y calculo orientativo de la multa; evidencia de publicacion (URL, captura fechada, version del aviso).
**Fuente oficial:** `ace_decreto_144.txt` paginas 24 y 26; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 4.8 Informar al encargado la revocacion del consentimiento

**Norma:** LPDP
**Articulo:** Art. 30
**Obligacion:** "Sí estos datos personales también son tratados por un encargado del tratamiento, el delegado deberá informarle de la resolución de revocación en el plazo de cinco días hábiles a partir de la fecha de emisión de esta, para que la ejecute inmediatamente."
**A quien aplica:** Responsable (a traves del delegado; segun prensa, tras la reforma la obligacion pasaria al sujeto obligado, manteniendo el plazo de 5 dias habiles).
**Implicacion para el software:** Flujo de revocacion con tarea automatica "informar a encargados" con plazo de 5 dias habiles desde la resolucion y registro de la respuesta del encargado (ejecucion inmediata). Requiere saber que encargados tratan los datos de cada titular o categoria.
**Fuente oficial:** `ace_decreto_144.txt` pagina 16; reforma segun https://www.eldiariodehoy.com/noticias/nacionales/asamblea-legislativa-deroga-obligatoriedad-de-las-empresas-privadas-de-nombrar-delegados-de-proteccion-de-datos-personales/93615/2026/; consulta 2026-09-23
**Vigencia:** VIGENTE (MODIFICADA en cuanto al sujeto que informa, pendiente de publicacion)
**Clasificacion:** OBLIGATORIO (CONDICIONAL a que exista encargado)

### 4.9 Deber de asistencia de los proveedores

**Norma:** LPDP
**Articulo:** Art. 17
**Obligacion:** "Sera obligación de cada dependencia, empleado o proveedor del responsable del tratamiento de datos de asistir y atender a las peticiones canalizadas por el delegado en el ejercicio de sus funciones."
**A quien aplica:** Proveedores (y dependencias y empleados) del responsable.
**Implicacion para el software:** Mientras este vigente, la clausula de "asistencia al delegado" debe estar en los contratos con proveedores. Tras la reforma (segun prensa: Art. 17 derogado y Art. 16 reformado para que los sujetos obligados "auxilien a sus dependencias o proveedores y fijen lineamientos internos"), la asistencia del proveedor dejaria de ser obligacion legal directa y pasaria a ser un deber de la empresa de organizar a sus proveedores mediante lineamientos internos. En cualquiera de los dos escenarios, la clausula contractual de cooperacion en ARCO-POL es la unica forma de hacerla exigible al proveedor.
**Fuente oficial:** `ace_decreto_144.txt` pagina 11; Lineamientos DPO Art. 37 (`lineamientos_dpo_OCR.txt` lineas 510 a 512); reforma segun eldiariodehoy.com (URL anterior); consulta 2026-09-23
**Vigencia:** VIGENTE al 2026-09-23; DEROGADA una vez publicada la reforma (segun fuentes secundarias)
**Clasificacion:** OBLIGATORIO hoy; tras la reforma, OBLIGATORIO para la empresa (fijar lineamientos internos) y RECOMENDADO como clausula contractual

### 4.10 Lineamientos DPO: obligatorios para el encargado; delegado como enlace con encargados

**Norma:** Lineamientos para el Delegado de Proteccion de Datos Personales (ACE)
**Articulo:** Art. 2 y Art. 3; Art. 23 inc. 2; Art. 27 lit. b; Art. 39 inc. 2
**Obligacion:** Art. 3: "Las disposiciones contenidas en los presentes lineamientos, serán de obligatorio cumplimiento para el Delegado, el encargado y el responsable" (confirmado contra la imagen `ocr/lineamientos_dpo/page-02.png`). Art. 23: el Delegado "podrá poner en conocimiento de la ACE cualquier hecho o situación atribuible al responsable o al encargado del tratamiento" que pudiera constituir infraccion. Art. 27 lit. b: el Delegado tiene prohibido "Representar a la institución u organización ante la ACE en calidad de responsable o de encargado, considerando que tales roles son inseparables de quienes legalmente los detentan". Art. 39: el Delegado "propondrá al responsable o al encargado mecanismos y procedimientos internos".
**A quien aplica:** Delegado, encargado y responsable.
**Implicacion para el software:** El rol de "responsable" y "encargado" son atributos de la persona juridica, no del usuario delegado; el software no debe permitir que un usuario con rol delegado firme o remita como responsable o encargado. Los Lineamientos seguiran aplicando al sector publico y a quien mantenga delegado voluntario tras la reforma.
**Fuente oficial:** `lineamientos_dpo_OCR.txt`; `ocr/lineamientos_dpo/page-02.png`; https://ace.gob.sv/page/documentos/politicas/NDPDDP.pdf; consulta 2026-09-23
**Vigencia:** VIGENTE (19 ago 2026); afectados por la reforma pendiente en lo relativo al delegado obligatorio privado
**Clasificacion:** OBLIGATORIO (CONDICIONAL: sector publico y privados que mantengan delegado)

### 4.11 Los encargados son sujetos obligados y pueden ser sancionados

**Norma:** LPDP y Normativa PAS
**Articulo:** LPDP Art. 2 inc. 1; Normativa PAS Art. 2
**Obligacion:** La LPDP "se aplicará a toda persona natural o jurídica, de carácter público o privado, que lleve a cabo actividades relativas o conexas al tratamiento de datos personales, ya sea de manera manual, parcial o totalmente automatizado o a través de terceros." La Normativa PAS "será aplicable a todos los sujetos obligados a que se refiere el artículo 2" de la LPDP. Los encargados realizan "actividades relativas o conexas al tratamiento", por lo que son sujetos obligados y sancionables.
**A quien aplica:** Responsables y encargados.
**Implicacion para el software:** Cuando el cliente actua como encargado, el software debe tratarlo como sujeto obligado pleno (medidas de seguridad, confidencialidad, notificacion de vulneraciones al responsable y, en su caso, a la ACE). Nota: el Art. 25 asigna la notificacion de vulneraciones al "responsable"; la ley no regula el plazo en que el encargado debe avisar al responsable. Debe pactarse en contrato (ver 5.4).
**Fuente oficial:** `ace_decreto_144.txt` pagina 2; `normativa_sancionadora_OCR.txt` linea 119; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

---

## 5. Contratos

### 5.1 Contrato para la transferencia de datos

**Norma:** LPDP
**Articulo:** Art. 41
**Obligacion:** "El responsable de la transferencia de datos personales deberá suscribir un contrato con el responsable receptor, en el cual se prevean como mínimo las mismas obligaciones a las que se encuentra sujeto el responsable de la transferencia de dichos datos."
**A quien aplica:** Responsable que transfiere (nacional o internacional) y responsable receptor. Literalmente exige contrato con el "responsable receptor"; no menciona al encargado.
**Implicacion para el software:** Toda transferencia registrada debe tener un contrato asociado (documento, fecha, partes, vigencia) o una justificacion de por que no existe; el contenido minimo debe replicar las obligaciones del transferente: finalidad limitada (Art. 32 y 34 lit. a), seguridad (Arts. 34 lit. b y 36), confidencialidad (Art. 34 lit. c), atencion ARCO-POL (Arts. 8 a 23), notificacion de vulneraciones (Art. 25), respeto al consentimiento y su revocacion (Arts. 26 a 31), temporalidad (Art. 5 lit. h), transferencias ulteriores (Arts. 40, 41, 44). El software debe generar una "lista de obligaciones espejo" a partir del perfil de cumplimiento de la empresa transferente.
**Fuente oficial:** `ace_decreto_144.txt` pagina 19; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (CONDICIONAL a que exista transferencia)

### 5.2 Contrato de confidencialidad y contratos de transferencia como medida de seguridad

**Norma:** Politicas N. 001-0309025-DPDP (ACE)
**Articulo:** Art. 4, "Medidas de Seguridad en Transferencias de Datos", lit. b; Art. 6 lit. d
**Obligacion:** "b) Contratos de Confidencialidad y Contratos para la Transferencia de Datos: Acuerdos legales con terceros que tratan datos." Art. 6: "d) Transferencias de datos: Comunicación cifrada, contratos de confidencialidad, notificación de brechas." Incumplir las medidas de seguridad de las politicas es infraccion grave (LPDP Art. 56 lit. b num. 7: "No cumplir con las medidas de seguridad establecida en las políticas de actuación emitidas por la Agencia").
**A quien aplica:** Responsables y encargados (Politicas Art. 4 inc. 1).
**Implicacion para el software:** Esta es la base juridica mas solida para exigir un contrato o DPA con cada proveedor que trate datos, aunque no sea "transferencia" en sentido estricto. Control: "todo tercero que trata datos tiene acuerdo legal de confidencialidad vigente"; severidad asociada: grave (11 a 25 salarios minimos, Art. 57 lit. b).
**Fuente oficial:** `ace_politicas_protecciondatos.txt` paginas 4 y 5; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 5.3 Acuerdo de confidencialidad con terceros en el sector publico

**Norma:** LPDP
**Articulo:** Art. 49 lit. e e inciso final
**Obligacion:** Las entidades publicas pueden transferir o difundir datos sin consentimiento "e) Cuando contraten o recurran a terceros para la prestación de un servicio que demande el tratamiento de datos personales. En el caso contemplado en el literal e), los terceros deberán suscribir un acuerdo de confidencialidad con la entidad pública involucrada y estarán sujetos a todas las obligaciones para la protección de datos personales contempladas en la presente ley."
**A quien aplica:** Entidades publicas (Titulo III) y sus contratistas privados.
**Implicacion para el software:** Aunque el producto se dirige al sector privado, muchas empresas privadas son contratistas del Estado: cuando el cliente actua como encargado de una entidad publica, el software debe exigir evidencia del acuerdo de confidencialidad y marcar al cliente como sujeto a "todas las obligaciones" de la ley respecto de esos datos. Es tambien el mejor indicio del contenido que la ley espera de un contrato responsable-encargado: confidencialidad y sometimiento integral a la LPDP.
**Fuente oficial:** `ace_decreto_144.txt` pagina 21; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (CONDICIONAL: solo cuando una entidad publica contrata a un tercero)

### 5.4 Atribucion de la ACE de recomendar clausulas: no hay clausulas modelo publicadas

**Norma:** LPDP
**Articulo:** Art. 50 lit. p (y lit. n, guias de implementacion)
**Obligacion:** La ACE tiene la atribucion de "p) Recomendar cláusulas contractuales que garanticen la protección de los datos personales de acuerdo con la presente ley." Es una facultad de la ACE, no una obligacion de los sujetos obligados.
**Hallazgo de verificacion:** Al 2026-09-23 la pagina de formularios de la ACE (https://ace.gob.sv/page/formularios) lista unicamente los formularios ARCO-POL (acceso, rectificacion, cancelacion, oposicion, portabilidad, olvido, limitacion) y el de nombramiento de delegado, todos version 07-07-2025; la pagina de politicas (https://ace.gob.sv/politicas.php) lista solo el Decreto 143 y sus politicas, el Decreto 144 y sus politicas, los Lineamientos DPO y la Normativa PAS. No existe ninguna clausula modelo, contrato tipo, guia de contratacion ni guia de transferencias. Las busquedas web (asamblea.gob.sv, ace.gob.sv, firmas legales, prensa) tampoco arrojaron ninguna.
**Implicacion para el software:** El producto debe (a) ofrecer su propia plantilla de contenido minimo de contrato/DPA marcada como "buena practica, no aprobada por la ACE"; (b) tener un mecanismo de actualizacion normativa para incorporar clausulas recomendadas cuando la ACE las publique; (c) nunca afirmar que un contrato "cumple" la ley.
**Fuente oficial:** `ace_decreto_144.txt` pagina 22; https://ace.gob.sv/page/formularios; https://ace.gob.sv/politicas.php; consulta 2026-09-23, re-verificado 2026-09-24 (mismo resultado: solo formularios ARCO-POL y de nombramiento de delegado; ningun documento contractual ni de transferencias)
**Vigencia:** VIGENTE (atribucion no ejercida)
**Clasificacion:** HECHO (no es obligacion del sujeto obligado)

### 5.5 Contrato con delegado extranjero (referencia analogica)

**Norma:** Lineamientos DPO (ACE)
**Articulo:** Art. 15 inciso final
**Obligacion:** "El responsable que designe a un Delegado de nacionalidad extranjera, deberá suscribir con este un contrato que contemple cláusulas de confidencialidad, responsabilidad y garantía, en el cual se regulen las obligaciones del Delegado en el ejercicio de sus funciones y las consecuencias jurídicas derivadas de su incumplimiento. Dicho contrato, deberá prever que el responsable asuma frente a los titulares de los datos personales y frente a la Agencia toda responsabilidad, o riesgo que se derive de las actuaciones del Delegado extranjero."
**A quien aplica:** Responsables que contraten delegado extranjero (persona natural o juridica).
**Implicacion para el software:** Es el unico contenido contractual minimo que la ACE ha regulado hasta hoy: confidencialidad, responsabilidad, garantia, obligaciones y consecuencias del incumplimiento, y asuncion de responsabilidad por el responsable frente a titulares y ACE. Sirve de patron para la plantilla de DPA con proveedores extranjeros: el responsable no puede trasladar su responsabilidad al proveedor.
**Fuente oficial:** `lineamientos_dpo_OCR.txt` lineas 271 a 274; consulta 2026-09-23
**Vigencia:** VIGENTE (sujeto a la reforma pendiente en el sector privado)
**Clasificacion:** OBLIGATORIO (CONDICIONAL: delegado extranjero); RECOMENDADO como patron para contratos con proveedores

### 5.6 Contenido minimo recomendable del contrato con encargado o DPA

No existe norma salvadorena que fije el contenido minimo de un contrato responsable-encargado. La siguiente tabla propone un contenido minimo, con la base legal salvadorena que justifica cada clausula. Clasificacion global: RECOMENDADO (buena practica), salvo donde se indica base obligatoria.

| Clausula | Base juridica salvadorena | Clasificacion | Que debe registrar el software |
|---|---|---|---|
| Identificacion de partes y roles (responsable / encargado / subencargado) | Art. 4 lit. j y p | RECOMENDADO | Rol de cada parte; datos de contacto (alimentan Art. 7 lit. c y Art. 24 lit. h) |
| Objeto, finalidad y limitacion del tratamiento a las instrucciones del responsable | Arts. 32, 34 lit. a; Art. 56 lit. b num. 3 (finalidad distinta: grave) | OBLIGATORIO en cuanto al fondo (Art. 34 lit. a) | Finalidades autorizadas vinculadas al Registro de Actividades de Tratamiento |
| Categorias de datos y de titulares; identificacion de datos sensibles | Art. 24 lit. b; Arts. 37 a 39 | RECOMENDADO | Categorias tratadas; bandera de datos sensibles |
| Duracion y conservacion; devolucion o eliminacion al terminar | Art. 5 lit. h (temporalidad); Art. 10 | RECOMENDADO | Fecha fin; accion al termino; evidencia de eliminacion |
| Confidencialidad del encargado y de su personal, subsistente tras el contrato | Art. 34 lit. c; Politicas ACE Art. 4 lit. b; Art. 49 inc. final (sector publico) | OBLIGATORIO (Politicas ACE) | Documento firmado; vigencia |
| Medidas de seguridad conforme a Politicas ACE (2FA, cifrado en reposo y transito, gestion de identidades, backups, IDS/IPS, pentesting) | Arts. 34 lit. b, 36; Politicas ACE Art. 4; Art. 56 lit. b num. 7 | OBLIGATORIO | Checklist de medidas acreditadas; certificaciones (ISO 27001, SOC 2) como evidencia |
| Subcontratacion: autorizacion previa, lista de subencargados, mismas obligaciones | Art. 4 lit. j ("en conjunto con otros"); Art. 33 inc. 2 | RECOMENDADO | Lista de subencargados con pais; alertas de cambio |
| Vulneraciones de seguridad: aviso del encargado al responsable en plazo que permita cumplir las 72 horas (se sugiere 24 horas), contenido minimo Art. 25 lit. a) a e), cooperacion en la revision exhaustiva y documentacion | Art. 25; Politicas ACE Art. 4 lit. d; Art. 56 lit. a num. 3 | RECOMENDADO (plazo interno); OBLIGATORIO el resultado (72 h) | Plazo pactado; canal; registro de incidentes del proveedor |
| Asistencia en derechos ARCO-POL, revocacion y limitacion; bloqueo de datos en revision; ejecucion inmediata de revocaciones | Arts. 9, 13, 17 (vigente), 21, 30 | OBLIGATORIO hoy (Art. 17); RECOMENDADO tras la reforma | SLA de respuesta del proveedor compatible con 20 dias habiles; tarea de 5 dias (Art. 30) |
| Derecho de auditoria e inspeccion por el responsable y por la ACE; deber de atender requerimientos de la ACE | Art. 50 lit. a y t; Art. 56 lit. a num. 9 y lit. b num. 4; Politicas ACE Art. 5 lit. a y Art. 8 lit. b (auditorias anuales) | RECOMENDADO (auditoria del responsable); OBLIGATORIO (colaborar con la ACE) | Fecha de ultima auditoria; hallazgos |
| Transferencias internacionales y ubicacion de los datos: paises, centros de datos, sitios de contingencia; prohibicion de transferir a terceros sin autorizacion | Arts. 4 lit. r, 7 lit. b, 40, 44, 45, 54 inc. 2 | OBLIGATORIO en cuanto al fondo (Arts. 40, 44) | Pais de cada ubicacion; expediente de flujo transfronterizo |
| Responsabilidad e indemnidad; el responsable mantiene la responsabilidad frente a titulares y ACE | Art. 5 lit. i (responsabilidad demostrada); Lineamientos DPO Art. 15 inc. final (analogia) | RECOMENDADO | Texto de la clausula |
| Sometimiento expreso a la LPDP, a las Politicas ACE y a los lineamientos internos del responsable | Art. 33 inc. 2 | OBLIGATORIO | Evidencia de aceptacion de lineamientos internos |
| Ley aplicable y jurisdiccion (para proveedores extranjeros) | Art. 44 inc. 2 (garantia de tratamiento conforme a la LPDP) | RECOMENDADO | Ley aplicable; mecanismo de resolucion |

---

## 6. Transferencias nacionales

### 6.1 Requisitos de toda transferencia

**Norma:** LPDP
**Articulo:** Art. 40
**Obligacion:** "Los datos personales objeto de tratamiento sólo pueden ser transferidos para el cumplimiento de los fines directamente relacionados con el interés legítimo del titular de los mismos o del responsable de la base de datos, y con el previo consentimiento del primero de éstos, a quien se deberá informar sobre la finalidad de la transferencia e identificar al cesionario o los elementos que permitan hacerlo. El consentimiento otorgado podrá revocarse cuando el titular de la información así lo decidiere."
**A quien aplica:** Responsable que transfiere.
**Implicacion para el software:** Cada transferencia (o categoria de transferencia) debe registrar: finalidad, vinculo con el interes legitimo del titular o del responsable, cesionario identificado (o "elementos que permitan hacerlo", p. ej. "empresas del grupo X" o "aseguradoras contratadas"), evidencia de consentimiento previo especifico para la transferencia (no basta el consentimiento general de tratamiento: el Art. 27 lit. b exige consentimiento especifico por finalidad y el Art. 24 lit. d exige distinguir las finalidades que requieren consentimiento) y mecanismo de revocacion. Alerta: transferencia sin consentimiento = infraccion muy grave (Art. 56 lit. c num. 6; multa 26 a 40 salarios minimos, Art. 57 lit. c).
**Fuente oficial:** `ace_decreto_144.txt` pagina 18; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

Punto que requiere abogado: la ley no aclara si las excepciones al consentimiento del Art. 28 (p. ej. datos de fuentes publicas, relacion contractual) o las bases de licitud del Art. 5 lit. g distintas del consentimiento (obligacion legal, contrato) eximen del consentimiento previo del Art. 40. El Art. 56 lit. c num. 6 sanciona transferir "sin el consentimiento de su titular o su representante, o en contravención de las excepciones que establezca la ley", lo que sugiere que existen excepciones aplicables, pero el Art. 40 no las enumera. El software debe permitir registrar una base distinta del consentimiento, marcandola como "requiere validacion juridica".

### 6.2 Prohibicion de transferir para finalidades distintas

**Norma:** LPDP
**Articulo:** Art. 32 y Art. 59 lit. d
**Obligacion:** Las empresas privadas "en ningún caso podrán transferir o tratar datos personales de terceros para ofrecer otro tipo de servicios o cualquier finalidad diferente a la que éstos fueron recabados, sin previa autorización del titular." Prohibido "Utilizar, transferir, compartir y comercializar a cualquier título y destino la información de las personas (...) en contravención a lo dispuesto en la presente ley". Incurrir en prohibiciones del Art. 59 es infraccion grave (Art. 56 lit. b num. 6); comercializar sin consentimiento es muy grave (Art. 56 lit. c num. 7).
**A quien aplica:** Responsables privados.
**Implicacion para el software:** Cada transferencia debe vincularse a una finalidad informada en el aviso; el software debe alertar si la finalidad de la transferencia no figura entre las finalidades del aviso vigente.
**Fuente oficial:** `ace_decreto_144.txt` paginas 17 y 26; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 6.3 Notificacion a receptores de rectificaciones y eliminaciones

**Norma:** LPDP
**Articulo:** Art. 21 inciso 3 (y Art. 10 inc. final para el derecho al olvido)
**Obligacion:** "En el supuesto de comunicación o transferencia de datos personales, el delegado deberá notificar la rectificación, actualización o eliminación de dichos datos a quienes hayan recibido los mismos, dentro de los cinco días hábiles posteriores a la determinación de la procedencia de la solicitud del titular." Para el olvido: "el responsable [debe] informar a otros responsables del tratamiento de dichos datos personales para que éstos sean suprimidos de los enlaces, copias o réplicas".
**A quien aplica:** Responsable (a traves del delegado; segun prensa, tras la reforma, la entidad directamente, con el mismo plazo de 5 dias habiles).
**Implicacion para el software:** Es imprescindible un registro de receptores (a quien se comunico que datos y cuando) por titular o por conjunto de datos; al resolver una rectificacion, actualizacion, cancelacion u olvido, el software genera tareas de notificacion a cada receptor con vencimiento de 5 dias habiles desde la procedencia y guarda la evidencia de envio. Nota: la ley usa "comunicación o transferencia", lo que abarca tambien a encargados que hayan recibido los datos.
**Fuente oficial:** `ace_decreto_144.txt` paginas 9 y 12; reforma segun https://www.asamblea.gob.sv/node/14116; consulta 2026-09-23
**Vigencia:** VIGENTE (MODIFICADA en cuanto al sujeto, pendiente de publicacion)
**Clasificacion:** OBLIGATORIO (CONDICIONAL a que haya habido comunicacion o transferencia)

### 6.4 Informar al titular los intercambios y los destinatarios

**Norma:** LPDP
**Articulo:** Art. 8 inciso final; Art. 7 lit. a; Art. 8 lit. a
**Obligacion:** En el acceso "se debe comunicar si se ha realizado un intercambio de su información personal con otras instituciones o entidades" y la informacion debe ir acompanada de "los sujetos que han consultado dicha información y con qué propósito". Al recolectar debe informarse "quiénes pueden ser sus destinatarios o clase de destinatarios".
**A quien aplica:** Responsable.
**Implicacion para el software:** La respuesta de acceso debe poder incluir, de forma automatica, el historial de transferencias y comunicaciones de los datos del titular (destinatario, fecha, proposito) y el registro de consultas. El aviso y la politica deben listar destinatarios o clases de destinatarios.
**Fuente oficial:** `ace_decreto_144.txt` paginas 6 y 7; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

---

## 7. Transferencias internacionales

### 7.1 Transcripcion del Art. 44

> Art. 44.- La transferencia de datos personales de cualquier tipo con países u organismos internacionales será permitida solamente cuando el país receptor o importador de datos personales cumpla como mínimo con los principios de protección de datos personales definidos en la presente ley o por los estándares internacionales en la materia. De ninguna manera, las garantías ofrecidas deberán ser menores a las exigidas por el ordenamiento jurídico vigente en El Salvador.
>
> En caso de que el país receptor o importador de datos personales no cuente con un nivel de protección adecuado, el país emisor deberá garantizar que el tratamiento de los datos personales se efectué conforme a lo dispuesto por la presente ley.
>
> Sin perjuicio de las transferencias de datos personales que se realicen a países que tienen un nivel adecuado de protección, los responsables, en virtud del principio de responsabilidad demostrada, deberán de implementar las medidas apropiadas y efectivas a fin de garantizar el adecuado tratamiento de los datos personales que transfieren al país receptor y la seguridad a los registros al momento de efectuar dicha transferencia.
>
> Queda exceptuado el caso de los tratados de Integración Económica Centroamericana, ya que por la naturaleza comercial en la región se podrá optar a la transferencia de datos conforme a lo adoptado y acordado legalmente entre los países miembros del mismo tratado.
>
> En todo caso deberá mediar el consentimiento previo del titular de los datos personales, salvo se establezcan excepciones en los instrumentos internacionales pertinentes y estas operen recíprocamente entre los países que los suscriban.

Fuente: `ace_decreto_144.txt` pagina 19. Consulta 2026-09-23. VIGENTE.

### 7.2 Nivel adecuado: quien lo determina y si existe lista

**Norma:** LPDP
**Articulo:** Art. 44 inc. 1 y 2; Art. 50 (atribuciones de la ACE)
**Hallazgo:** La ley fija el estandar (el pais receptor debe cumplir "como mínimo" los principios de la LPDP "o (...) los estándares internacionales en la materia", sin garantias menores a las salvadorenas), pero **no atribuye a ningun organo la facultad de declarar que un pais tiene nivel adecuado**: el Art. 50 no incluye entre las atribuciones de la ACE la de emitir decisiones de adecuacion ni listas de paises. La ACE tampoco ha publicado ninguna lista, guia o criterio de adecuacion (verificado en https://ace.gob.sv/politicas.php y https://ace.gob.sv/page/formularios al 2026-09-23; ninguna fuente secundaria consultada menciona una lista). En consecuencia, la evaluacion de adecuacion recae de facto en el responsable, bajo el principio de responsabilidad demostrada (Art. 5 lit. i y Art. 44 inc. 3) y con la carga de la prueba en su contra (Art. 54 inc. 2).
**Que son los "estandares internacionales":** la ley no los identifica. Candidatos razonables: el Convenio 108 y 108+ del Consejo de Europa (El Salvador no es parte, segun lo localizado), las Directrices de la OCDE sobre privacidad, los Estandares de Proteccion de Datos Personales para los Estados Iberoamericanos (RIPD, 2017) y el RGPD de la UE como referencia comparada. La Politicas ACE (Art. 1 y 3 lit. i) remiten a ISO 27001 como estandar de seguridad, no de adecuacion.
**A quien aplica:** Responsable de la transferencia (y, por Art. 4 lit. k, el encargado en El Salvador que actue como emisor).
**Implicacion para el software:** Modulo de "evaluacion de pais receptor" que documente, para cada pais destino: (a) si tiene ley general de proteccion de datos y autoridad de control; (b) si reconoce derechos equivalentes a ARCO-POL; (c) si sus garantias son al menos las salvadorenas; (d) las fuentes consultadas y la fecha; (e) la conclusion del usuario (nunca del software) y su justificacion. El software puede ofrecer fichas informativas de paises frecuentes (EE.UU., UE, Mexico, Colombia, Guatemala, Honduras, Costa Rica, Panama, etc.) marcadas como "referencia, no decision de adecuacion". Debe conservarse como evidencia para el Art. 54 inc. 2.
**Fuente oficial:** `ace_decreto_144.txt` paginas 19, 21 a 23; https://ace.gob.sv/politicas.php; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (evaluar y garantizar); INCERTIDUMBRE (quien declara la adecuacion)

### 7.3 Garantias cuando no hay nivel adecuado

**Norma:** LPDP
**Articulo:** Art. 44 inc. 2 y 3
**Obligacion:** Si el pais receptor "no cuente con un nivel de protección adecuado, el país emisor deberá garantizar que el tratamiento de los datos personales se efectué conforme a lo dispuesto por la presente ley"; y, en todo caso, los responsables "deberán de implementar las medidas apropiadas y efectivas a fin de garantizar el adecuado tratamiento de los datos personales que transfieren al país receptor y la seguridad a los registros al momento de efectuar dicha transferencia."
**A quien aplica:** La ley dice "el país emisor", expresion tecnicamente defectuosa; leida con el Art. 4 lit. k (emisor = titular del banco de datos o encargado en El Salvador que transfiere), la obligacion recae en el responsable (o encargado) emisor.
**Implicacion para el software:** La ley no enumera las garantias (a diferencia del RGPD: clausulas tipo, normas corporativas vinculantes, certificaciones). Las unicas herramientas con anclaje normativo salvadoreno son: contrato con obligaciones espejo (Art. 41), contratos de confidencialidad y de transferencia (Politicas ACE Art. 4 lit. b), medidas de seguridad de las Politicas ACE, cifrado en transito (SSL/TLS) y consentimiento previo del titular. El software debe exigir, para cada flujo a pais sin adecuacion documentada, al menos: contrato/DPA con obligaciones espejo, evidencia de medidas de seguridad, consentimiento previo del titular y expediente Art. 45.
**Fuente oficial:** `ace_decreto_144.txt` pagina 19; `ace_politicas_protecciondatos.txt` pagina 4; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO (CONDICIONAL: pais sin nivel adecuado)

### 7.4 Consentimiento previo del titular en transferencias internacionales

**Norma:** LPDP
**Articulo:** Art. 44 inc. final; Art. 40; Art. 56 lit. c num. 6
**Obligacion:** "En todo caso deberá mediar el consentimiento previo del titular de los datos personales, salvo se establezcan excepciones en los instrumentos internacionales pertinentes y estas operen recíprocamente entre los países que los suscriban."
**A quien aplica:** Responsable de la transferencia.
**Implicacion para el software:** El consentimiento debe ser previo, especifico e informado (Arts. 26 y 27), y el aviso debe informar la transferencia internacional como finalidad que requiere consentimiento (Art. 24 lit. d) e identificar al cesionario (Art. 40). No se ha localizado ningun instrumento internacional ratificado por El Salvador que establezca excepciones reciprocas al consentimiento para transferencias de datos personales; el software debe tratar la excepcion como no disponible salvo que el usuario documente el tratado con asesoria juridica.
**Fuente oficial:** `ace_decreto_144.txt` pagina 19; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 7.5 Excepcion de la Integracion Economica Centroamericana

**Norma:** LPDP
**Articulo:** Art. 44 inc. 4
**Obligacion:** "Queda exceptuado el caso de los tratados de Integración Económica Centroamericana, ya que por la naturaleza comercial en la región se podrá optar a la transferencia de datos conforme a lo adoptado y acordado legalmente entre los países miembros del mismo tratado."
**Hallazgo:** Los tratados aludidos son el Tratado General de Integracion Economica Centroamericana (Managua, 1960) y su Protocolo de Guatemala (1993), administrados por la SIECA en el marco del SICA (miembros del subsistema economico: Guatemala, El Salvador, Honduras, Nicaragua, Costa Rica y Panama). En las busquedas realizadas (sieca.int, sica.int y buscadores generales) **no se localizo ningun reglamento, resolucion del COMIECO ni acuerdo regional que regule transferencias de datos personales entre los Estados parte**. La excepcion permite transferir "conforme a lo adoptado y acordado legalmente entre los países miembros", y mientras no exista tal acuerdo, no hay un regimen alternativo al que acogerse. Ademas, el inciso final exige consentimiento previo "en todo caso" salvo excepciones reciprocas en instrumentos internacionales, que tampoco se han localizado.
**A quien aplica:** Responsables que transfieren a Guatemala, Honduras, Nicaragua, Costa Rica o Panama.
**Implicacion para el software:** No activar automaticamente ninguna "via centroamericana"; tratar estos paises como cualquier otro pais receptor (evaluacion de adecuacion + garantias + consentimiento + Art. 45), con una nota de que la ley preve una excepcion cuyo desarrollo regional no existe al 2026-09-23. Requiere abogado.
**Fuente oficial:** `ace_decreto_144.txt` pagina 19; https://www.sica.int/documentos/protocolo-al-tratado-general-de-integracion-economica-centroamericana-protocolo-de-guatemala_1_116843.html; https://www.sieca.int/integracion-economica-centroamericana/; consulta 2026-09-23
**Vigencia:** VIGENTE (sin desarrollo)
**Clasificacion:** CONDICIONAL (solo si existe acuerdo regional aplicable, hoy no localizado)

### 7.6 Responsabilidad demostrada y carga de la prueba

**Norma:** LPDP
**Articulo:** Art. 5 lit. i; Art. 44 inc. 3; Art. 54 inc. 2
**Obligacion:** "Tratándose de transferencias internacionales de datos personales, la carga de la prueba recaerá en el responsable de la transferencia, el cual deberá demostrar que el tratamiento o la transferencia fue realizado conforme a la presente ley o de acuerdo con los estándares internacionales en la materia."
**A quien aplica:** Responsable de la transferencia.
**Implicacion para el software:** Cada flujo internacional debe tener un **expediente probatorio** exportable: descripcion del flujo, pais y receptor, rol del receptor, base de licitud y consentimiento (con evidencia), evaluacion de adecuacion, contrato/DPA, medidas de seguridad, evidencia de comunicacion a la ACE (Art. 45), fecha y responsable interno. Es la funcionalidad central de este lente para el producto.
**Fuente oficial:** `ace_decreto_144.txt` paginas 6, 19 y 24; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 7.7 Infracciones muy graves en materia de transferencias

**Norma:** LPDP
**Articulo:** Art. 56 lit. c num. 5 y 6; Art. 57 lit. c
**Obligacion:** Son infracciones muy graves: "5. Realizar transferencia internacional de datos personales a países que no cumplan como mínimo con el nivel de protección exigido por la presente ley." y "6. Realizar transferencia de datos personales sin el consentimiento de su titular o su representante, o en contravención de las excepciones que establezca la ley." Multa de 26 a 40 salarios minimos mensuales del sector comercio, sin perjuicio de medidas adicionales (Art. 58) y responsabilidad civil o penal.
**A quien aplica:** Responsable de la transferencia (y, en su caso, encargado emisor).
**Implicacion para el software:** Riesgo maximo asociado a los controles "pais sin adecuacion documentada" y "transferencia sin consentimiento"; calculo orientativo de la multa; bloqueo de la marcacion "flujo documentado" mientras falten evidencias.
**Fuente oficial:** `ace_decreto_144.txt` paginas 25 y 26; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 7.8 Politicas ACE: ambito internacional y transferencias seguras

**Norma:** Politicas N. 001-0309025-DPDP
**Articulo:** Art. 2; Art. 4 "Medidas de Seguridad en Transferencias de Datos" lit. c
**Obligacion:** "c) Transferencias Internacionales Seguras: Solo compartir datos con países que garanticen protección equivalente." Y las politicas "aplican a operaciones internacionales vinculadas a ciudadanos salvadoreños".
**A quien aplica:** Responsables y encargados.
**Implicacion para el software:** La ACE eleva el estandar de "como mínimo los principios" (ley) a "protección equivalente" (politica). El modulo de evaluacion de pais debe usar el estandar mas exigente (equivalencia) para clasificar el riesgo.
**Fuente oficial:** `ace_politicas_protecciondatos.txt` paginas 2 y 4; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

---

## 8. Art. 45: participacion de la ACE, puesta en conocimiento del flujo transfronterizo y "registro de banco de datos"

### 8.1 Transcripcion

> Art. 45.- Los responsables de los bancos de datos, bases de datos, repositorios o de los sistemas o registros, tanto manuales como informáticos, podrán solicitar la opinión del Entidad Rectora, respecto a si el flujo transfronterizo de datos personales que realiza o realizará cumple con lo dispuesto por la presente ley.
>
> En cualquier caso, el flujo transfronterizo de datos personales se pondrá en conocimiento de dicho organismo, incluyendo la información que se requiere para la transferencia de datos personales y el registro de banco de datos.

Fuente: `ace_decreto_144.txt` pagina 20. Confirmado con `diario_oficial_2024-11-15_mh.txt` lineas 1165 a 1171 y con el Dictamen 11/2024 (`dictamen_11_2024_ley_original_OCR.txt` lineas 1018 a 1020), que contiene el mismo texto sin explicacion adicional. Consulta 2026-09-23. VIGENTE.

### 8.2 Opinion previa de la ACE (opcional)

**Norma:** LPDP
**Articulo:** Art. 45 inc. 1
**Obligacion:** Facultad ("podrán solicitar") del responsable de pedir opinion a la ACE sobre si un flujo transfronterizo actual o futuro cumple la ley.
**Hallazgo:** No existe formulario, servicio ni procedimiento publicado por la ACE para solicitar esta opinion (verificado en https://ace.gob.sv/page/formularios y en el sitio principal https://ace.gob.sv/ al 2026-09-23). La via general seria un escrito dirigido a la Direccion de Proteccion de Datos Personales de la ACE (canal usado por los Lineamientos DPO Art. 40 para el registro transitorio de delegados) al amparo de la Ley de Procedimientos Administrativos (supletoria, Art. 62 LPDP). La ley no fija plazo ni efecto vinculante de la opinion.
**Implicacion para el software:** Ofrecer la generacion de un "escrito de solicitud de opinion" con el expediente del flujo adjunto, marcado como opcional; registrar fecha de envio, canal y respuesta.
**Fuente oficial:** `ace_decreto_144.txt` pagina 20; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** RECOMENDADO (facultativo por ley)

### 8.3 Puesta en conocimiento obligatoria del flujo transfronterizo

**Norma:** LPDP
**Articulo:** Art. 45 inc. 2
**Obligacion:** "En cualquier caso, el flujo transfronterizo de datos personales se pondrá en conocimiento de dicho organismo, incluyendo la información que se requiere para la transferencia de datos personales y el registro de banco de datos."
**A quien aplica:** Responsables de bancos de datos, bases de datos, repositorios, sistemas o registros que realicen flujo transfronterizo.
**Hallazgo critico:** (1) La obligacion es imperativa ("se pondrá en conocimiento") y no depende de que se haya pedido opinion. (2) La ley no fija plazo, forma, contenido detallado ni momento (previo o posterior). (3) "La información que se requiere para la transferencia" no esta definida en ninguna norma; por analogia con los Arts. 40 y 44, seria: finalidad, cesionario o receptor, pais, categorias de datos, base de licitud y consentimiento, garantias y medidas de seguridad. (4) "El registro de banco de datos" no esta definido ni desarrollado: **la LPDP no crea un registro de bancos o bases de datos ante la ACE** (los Arts. 50, 60 y 61 no lo mencionan; la unica atribucion registral desarrollada por la ACE es el Registro de Delegados de los Lineamientos DPO Arts. 10 y 11). (5) La ACE no ha habilitado, al 2026-09-23, ningun formulario, plataforma ni procedimiento para esta comunicacion (verificado en https://ace.gob.sv/page/formularios, https://ace.gob.sv/politicas.php y https://ace.gob.sv/). (6) La omision de esta comunicacion no aparece tipificada de forma especifica en el Art. 56; podria encuadrarse como infraccion leve num. 9 ("No atender las solicitudes realizadas por parte de la ACE") solo si la ACE la requiere, o valorarse como incumplimiento de la responsabilidad demostrada. Este encuadre requiere abogado.
**Implicacion para el software (critico para el producto):** (a) No existe obligacion general de inscribir las bases de datos de la empresa ante la ACE; el software NO debe presentar un "registro ante la ACE" como tramite existente. (b) Si existe la obligacion de poner en conocimiento de la ACE cada flujo transfronterizo; como no hay canal, el software debe: generar un "expediente de comunicacion de flujo transfronterizo" con todos los datos del Art. 40, 44 y 45 y con la descripcion de la base de datos origen (inventario interno de bases de datos, que hace las veces del "registro de banco de datos"); ofrecer al usuario la opcion de remitirlo por escrito o correo institucional a la Direccion de Proteccion de Datos Personales de la ACE (canal transitorio usado por los Lineamientos DPO), registrando fecha y acuse; o, si la empresa decide esperar a que la ACE habilite el mecanismo, dejar constancia fechada de la decision, la imposibilidad material y la disposicion a comunicar (evidencia de responsabilidad demostrada). (c) Mantener un inventario interno de bases de datos (registro de bancos de datos) siempre listo para exportar, que coincide con el Registro de Actividades de Tratamiento exigido por las Politicas ACE Art. 4, medidas organizativas, lit. d. (d) Vigilancia normativa: alerta cuando la ACE publique el mecanismo.
**Fuente oficial:** `ace_decreto_144.txt` paginas 20 a 23 y 26 y 27; `lineamientos_dpo_OCR.txt` lineas 200 a 218 y 535 a 537; https://ace.gob.sv/page/formularios; https://ace.gob.sv/politicas.php; consulta 2026-09-23, re-verificado 2026-09-24 (mismo resultado: sin formulario ni mecanismo de registro de bancos de datos ni de comunicacion de flujo transfronterizo)
**Vigencia:** VIGENTE (sin mecanismo habilitado)
**Clasificacion:** OBLIGATORIO (de cumplimiento actualmente indeterminado; requiere abogado)

### 8.4 Estado del unico registro existente: Registro de Delegados

**Norma:** Lineamientos DPO (ACE)
**Articulo:** Arts. 10, 11 y 40
**Hecho:** Los Lineamientos crearon el Registro Publico de Delegados en una "plataforma informática" que se establecera; mientras no este habilitada, las comunicaciones se hacen "mediante oficio, escrito o correo institucional dirigido a la Dirección de Protección de Datos Personales de la ACE", con plazo transitorio de 20 dias habiles desde la vigencia (vencimiento calculado por fuentes secundarias: 16 sep 2026). Segun prensa (elsalvador.com, 12 sep 2026), la ACE comunico: "Queda sin efecto la fecha límite establecida para el nombramiento del delegado de protección de datos personales" y "no será necesario realizar ninguna acción al respecto", anunciando nuevas directrices por canales oficiales.
**Implicacion para el software:** Confirma que la ACE opera hoy por escrito o correo institucional para cualquier comunicacion (util como canal para el Art. 45) y que no existe plataforma registral en funcionamiento. No hay ningun registro de bases de datos ni de transferencias.
**Fuente oficial:** `lineamientos_dpo_OCR.txt` lineas 200 a 218 y 532 a 537; https://www.elsalvador.com/dinero-y-negocios/entorno-economico/empresas-ley-de-proteccion-datos-el-salvador/1292968/2026/; https://blplegal.com/es/delegado-proteccion-datos-el-salvador-ace/; https://www.contrapunto.com.sv/sin-fecha-para-nombrar-a-los-delegados-de-proteccion-de-datos-personales-la-ace-establece-el-registro-obligatorio/; consulta 2026-09-23
**Vigencia:** VIGENTE, plazo transitorio dejado sin efecto (segun fuente secundaria)
**Clasificacion:** HECHO

---

## 9. Cloud y SaaS extranjeros: encuadre juridico y documentacion a exigir

### 9.1 Encuadre general

1. **Rol:** Un proveedor de nube o SaaS que almacena o procesa datos personales siguiendo las instrucciones de la empresa es **encargado** (Art. 4 lit. j). El Art. 7 lo dice expresamente para "proveedores de servicios de almacenamiento tercerizados (...) que utiliza como medio de almacenamiento la nube u otra infraestructura".
2. **Consecuencias del rol de encargado:** debe someterse a la LPDP y a los lineamientos del responsable y de la ACE (Art. 33 inc. 2); le aplican los Arts. 34 y 36 y las Politicas ACE; debe figurar con datos de contacto en la politica de privacidad (Art. 7 lit. c) y en el aviso (Art. 24 lit. h); debe existir acuerdo legal de confidencialidad (Politicas ACE Art. 4 lit. b).
3. **Ubicacion en el extranjero:** Aunque la definicion de transferencia (Art. 4 lit. u) excluye la comunicacion al encargado, las definiciones de emisor (lit. k) y receptor (lit. o) contemplan expresamente al encargado en transferencias internacionales, y el Art. 45 habla de "flujo transfronterizo", termino mas amplio que "transferencia". Lectura conservadora recomendada: el alojamiento o procesamiento de datos personales en servidores fuera de El Salvador por un encargado es un flujo transfronterizo sujeto a los Arts. 44 (nivel adecuado, garantias, consentimiento previo), 45 (comunicacion a la ACE) y 54 inc. 2 (carga de la prueba). Lectura alternativa (menos conservadora): al no ser "transferencia", solo aplican los Arts. 33, 34, 36 y las Politicas ACE. **Este es el punto de mayor impacto practico del lente y debe resolverlo un abogado**; hasta entonces el software debe permitir configurar la postura de la empresa y, por defecto, aplicar la lectura conservadora.
4. **Consentimiento:** bajo la lectura conservadora, el uso de nube extranjera requiere consentimiento previo del titular (Art. 44 inc. final) y su informacion en el aviso (Art. 24 lit. d y h) y politica (Art. 7 lit. a, b y c). En la practica, esto implica que el aviso de privacidad de toda empresa que use Microsoft 365, Google Workspace o AWS debe mencionar al proveedor, la existencia de respaldos y sitios de contingencia y el pais o region de alojamiento, y el consentimiento debe cubrir esa finalidad.
5. **Politicas ACE Art. 2:** las politicas "aplican a operaciones internacionales vinculadas a ciudadanos salvadoreños", lo que refuerza que el proveedor extranjero debe acreditar las medidas del Art. 4.

### 9.2 Encuadre por proveedor (orientativo, buena practica)

Las descripciones de los productos y de sus acuerdos de tratamiento de datos provienen de la documentacion publica de los proveedores (Microsoft Products and Services DPA, Google Cloud Data Processing Addendum, AWS Data Processing Addendum) y no han sido verificadas contra fuentes oficiales salvadorenas; se marcan como "segun documentacion publica del proveedor". Ninguna de ellas menciona la LPDP de El Salvador.

| Servicio | Rol probable bajo LPDP | Flujo transfronterizo? | Documentacion que el software debe pedir y archivar | Riesgos y notas |
|---|---|---|---|---|
| Microsoft 365 (correo, OneDrive, SharePoint, Teams) | Encargado (Art. 4 lit. j; Art. 7) | Si, salvo que se contrate residencia de datos en region especifica; aun asi, soporte y subencargados pueden acceder desde otros paises | DPA de Microsoft vigente (version y fecha); lista de subencargados; region de alojamiento configurada; certificaciones ISO 27001 / SOC 2; descripcion de medidas de seguridad; politica de notificacion de incidentes; terminos de retencion y eliminacion al finalizar | El DPA es de adhesion (no negociable); no menciona la LPDP; el plazo de notificacion de incidentes del proveedor debe cotejarse con las 72 h del Art. 25 |
| Google Workspace | Encargado | Si (infraestructura global; regiones de datos configurables para algunos datos) | Cloud Data Processing Addendum aceptado; lista de subencargados; configuracion de region; certificaciones; medidas de seguridad; terminos de eliminacion | Igual que Microsoft |
| AWS (IaaS/PaaS) | Encargado (almacenamiento e infraestructura); la empresa sigue siendo responsable de lo que despliega | Depende de la region elegida; no hay region en El Salvador; Centroamerica se atiende desde regiones de EE.UU. u otras | AWS DPA (aplica automaticamente segun AWS); region y servicios usados; modelo de responsabilidad compartida documentado; certificaciones; subencargados | La empresa debe documentar sus propias medidas (cifrado, IAM) porque AWS solo cubre la infraestructura |
| Salesforce (CRM) | Encargado; contiene datos de clientes y prospectos, con frecuencia base de perfiles y marketing (Art. 12) | Si | DPA de Salesforce; ubicacion de la instancia; subencargados; certificaciones; funcionalidad de atencion ARCO-POL (exportacion, eliminacion) | Los usos de marketing exigen respetar la oposicion (Art. 12) y la revocacion (Arts. 29 a 31) |
| WhatsApp (Meta) | Distinguir: (a) WhatsApp Business Platform / API con Meta como proveedor: Meta actua como encargado segun sus terminos publicos; (b) uso de la app de consumo o WhatsApp Business App por empleados: Meta actua como responsable independiente de los metadatos y la empresa carece de DPA | Si (servidores de Meta fuera de El Salvador) | Para (a): terminos de tratamiento de datos de la plataforma, subencargados, medidas de seguridad; para (b): politica interna de uso, inventario de dispositivos y datos, evaluacion de riesgo | El caso (b) es el de mayor riesgo: no hay contrato con obligaciones espejo (Art. 41), no hay control de subencargados ni de conservacion; deberia documentarse como riesgo aceptado o migrar a (a) |

### 9.3 Checklist documental minimo por proveedor extranjero (RECOMENDADO)

1. Identificacion del proveedor, entidad contratante (matriz o filial), pais de constitucion y datos de contacto (alimenta Arts. 7 lit. c y 24 lit. h).
2. Contrato principal y DPA o clausulas de tratamiento de datos, con version y fecha; evidencia de aceptacion.
3. Descripcion del servicio, categorias de datos y de titulares, finalidad.
4. Ubicacion de los datos (paises o regiones), respaldos y sitios de contingencia (Art. 7 lit. b; Art. 4 lit. r).
5. Lista de subencargados y paises; mecanismo de aviso de cambios.
6. Evidencia de medidas de seguridad conforme a Politicas ACE Art. 4 (certificados ISO 27001, SOC 2, informes de pentesting, descripcion de cifrado y control de acceso).
7. Compromiso y plazo de notificacion de incidentes al cliente, compatible con las 72 h del Art. 25.
8. Herramientas o compromisos de asistencia para ARCO-POL, revocacion, bloqueo y limitacion (exportacion en formato estructurado para portabilidad, Art. 14; eliminacion, Art. 10).
9. Terminos de devolucion y eliminacion al finalizar el servicio; certificado de eliminacion.
10. Evaluacion de adecuacion del pais o paises de alojamiento (seccion 7.2) y garantias adicionales (seccion 7.3).
11. Consentimiento del titular que cubra el flujo (Art. 44 inc. final) y mencion en aviso y politica.
12. Expediente de comunicacion a la ACE del flujo transfronterizo (Art. 45) o constancia de imposibilidad (seccion 8.3).
13. Fecha de revision y proxima revision (las Politicas ACE Art. 8 lit. b preven auditorias anuales).

---

## 10. Medidas de seguridad en transferencias segun las Politicas de Actuacion ACE

**Norma:** Politicas N. 001-0309025-DPDP
**Articulo:** Art. 4 (bloque "Medidas de Seguridad en Transferencias de Datos") y Art. 6 lit. d
**Obligacion (transcripcion):** "a) Protocolos de Comunicación Segura: Uso de SSL/TLS para cifrar comunicaciones. b) Contratos de Confidencialidad y Contratos para la Transferencia de Datos: Acuerdos legales con terceros que tratan datos. c) Transferencias Internacionales Seguras: Solo compartir datos con países que garanticen protección equivalente. d) Notificación de Brechas de Seguridad: Reporte a la Agencia de Ciberseguridad del Estado, Fiscalía General de la República y titulares en un máximo de 72 horas." Art. 6: "d) Transferencias de datos: Comunicación cifrada, contratos de confidencialidad, notificación de brechas."
**A quien aplica:** Responsables y encargados (Art. 4 inc. 1); entidades publicas y privadas que "transfieran datos personales en El Salvador" y operaciones internacionales vinculadas a ciudadanos salvadorenos (Art. 2).
**Implicacion para el software:** Para cada transferencia o flujo a proveedor, cuatro controles verificables con evidencia: (1) canal cifrado (TLS, SFTP, cifrado de archivos) con descripcion tecnica; (2) contrato de confidencialidad o de transferencia vigente; (3) para flujos internacionales, evaluacion de "protección equivalente" del pais; (4) procedimiento de notificacion de brechas en 72 h que incluya al proveedor. Ademas, las medidas tecnicas generales del Art. 4 (cifrado en reposo y transito, 2FA, gestion de identidades, backups) deben acreditarse tambien en el proveedor (Art. 36 inc. final LPDP). Incumplir = infraccion grave (Art. 56 lit. b num. 7).
**Fuente oficial:** `ace_politicas_protecciondatos.txt` paginas 4 y 5; https://ace.gob.sv/politicas.php; consulta 2026-09-23
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

Otras medidas de las Politicas ACE relevantes para proveedores: medidas organizativas lit. d "Registro de Actividades de Tratamiento" (permite construir el inventario de bases de datos y de flujos) y lit. e "Evaluaciones de Impacto en la Privacidad (EIPD)" (recomendable exigir una EIPD antes de contratar un proveedor extranjero con datos sensibles o de gran volumen); medidas tecnicas lit. g "Digitalización: Usar sistemas especializados que permitan gestionar y documentar el tratamiento de datos" (respalda el uso de un software como PRIV-SV).

---

## 11. Impacto de la reforma de septiembre de 2026 en este lente

### 11.1 Verificacion adicional del numero de decreto (2026-09-24)

La nota oficial de la Asamblea (https://www.asamblea.gob.sv/node/14116) y la pagina de comunicado no indican numero de decreto. Se intento verificar el numero exacto el 2026-09-24 contra fuentes oficiales: (a) el listado oficial "Decretos Emitidos en 2026" (https://www.asamblea.gob.sv/leyes-y-decretos/decretos-por-anios/2026/0) llega unicamente hasta el Decreto N. 649 (26 ago 2026) y no incluye ningun decreto posterior a esa fecha ni ninguno relacionado con proteccion de datos; (b) la pagina "Ultimos Decretos Aprobados" (https://www.asamblea.gob.sv/leyes-y-decretos/ultimos-aprobados) indica expresamente que hay contenido "Pendiente de Publicacion Material en el Diario Oficial"; (c) resumenes automatizados de busqueda web (no fuente primaria) devolvieron numeros distintos y no verificables entre si para la reforma de la LPDP ("659" en un resumen, que otro resumen asocia a un decreto de exoneracion fiscal no relacionado, y "660" en otro resumen); ninguno de esos numeros pudo confirmarse contra el listado oficial de decretos ni contra el Diario Oficial. **Conclusion: al 2026-09-24 no es posible confirmar en fuente oficial primaria el numero exacto del decreto de reforma.** Este informe evita en adelante citar un numero de decreto especifico para la reforma y la identifica solo por fecha de aprobacion (17 sep 2026) y contenido reportado por prensa, hasta que el texto se publique en el Diario Oficial. Punto que requiere verificacion por abogado o seguimiento normativo antes de construir cualquier funcionalidad que dependa del numero de decreto.

Fuentes de la reforma en general: nota oficial https://www.asamblea.gob.sv/node/14116 (17 sep 2026, 57 votos, sin numero de decreto ni articulos), prensa (eldiariodehoy.com, elsalvador.com, infobae.com, hoy.com.sv). Texto oficial de la reforma no localizado: la busqueda en asamblea.gob.sv devolvio solo antecedentes de 2019 (iniciativa ARENA, expediente 991-6-2019-1) y 2021 (Dictamen N. 46 de la Comision de Economia, 13 abr 2021, proyecto de 77 articulos), que no corresponden al decreto de 2026. Publicacion en el Diario Oficial no confirmada al 2026-09-24. Todo lo siguiente es "segun fuentes secundarias".

| Cambio reportado | Efecto en este lente | Clasificacion |
|---|---|---|
| Derogacion del Art. 17 (deber de asistencia de dependencias, empleados y proveedores al delegado) | Desaparece la obligacion legal directa del proveedor de asistir; la cooperacion del proveedor en ARCO-POL pasa a depender del contrato y de los "lineamientos internos" de la empresa | RECOMENDADO (clausula contractual) |
| Reforma del Art. 16: los sujetos obligados "deberán auxiliar a sus dependencias o proveedores y fijar lineamientos internos" para gestionar solicitudes ARCO-POL | Nueva obligacion de la empresa de emitir lineamientos internos que alcancen a proveedores; coincide con el Art. 33 inc. 2 (lineamientos del responsable a proveedores) | OBLIGATORIO (una vez vigente) |
| Art. 16 reformado: "de existir un encargado del tratamiento, informarle en un plazo idéntico de 5 días hábiles" (revocacion) y 5 dias habiles para notificar a receptores rectificaciones y eliminaciones | Se mantienen los plazos de los Arts. 21 y 30, ahora a cargo del sujeto obligado y no del delegado | OBLIGATORIO |
| Derogacion del Art. 15 (delegado obligatorio en el privado) | Los Lineamientos DPO Art. 3 seguiran aplicando al encargado solo en la medida en que exista delegado (publico o voluntario) | CONDICIONAL |
| Sin cambios reportados en Arts. 4, 7, 24, 33, 34, 36, 40, 41, 44, 45, 54, 56 | El nucleo de este lente permanece igual | - |

Recomendacion para el producto: parametrizar la fecha de vigencia de la reforma; mientras no se confirme la publicacion, mostrar ambos regimenes (Art. 17 vigente / derogado) y exigir en todo caso la clausula contractual de asistencia.

---

## 12. Matriz resumen de obligaciones del lente

| # | Obligacion | Norma y articulo | Sujeto | Clasificacion | Sancion asociada |
|---|---|---|---|---|---|
| 1 | Someter a la ley y a lineamientos a proveedores con acceso a datos | LPDP 33 inc. 2 | Responsable y proveedor | OBLIGATORIO (condicional a subcontratacion) | Grave num. 5 (no implementar lineamientos ACE), por conexion |
| 2 | Limitar finalidad, seguridad y politicas, confidencialidad | LPDP 34 | Responsable y encargado | OBLIGATORIO | Grave num. 3 y 7 |
| 3 | Medidas de seguridad ACE, tambien para el encargado | LPDP 36; Politicas ACE 4 | Responsable y encargado | OBLIGATORIO | Grave num. 7 |
| 4 | Informar proveedores de nube, respaldos, contingencia y contacto del encargado en la politica | LPDP 7 | Responsable | OBLIGATORIO | Leve num. 8 |
| 5 | Contacto del encargado en el aviso de privacidad | LPDP 24 lit. h | Responsable | OBLIGATORIO (condicional) | Leve num. 2 |
| 6 | Informar al encargado la revocacion en 5 dias habiles | LPDP 30 | Responsable | OBLIGATORIO (condicional) | Muy grave num. 9 y 10, por conexion |
| 7 | Asistencia de proveedores al delegado | LPDP 17 | Proveedor | OBLIGATORIO hoy; derogacion pendiente | - |
| 8 | Contrato con el receptor con obligaciones espejo | LPDP 41 | Responsable transferente | OBLIGATORIO (condicional a transferencia) | Muy grave num. 6, por conexion |
| 9 | Contratos de confidencialidad y de transferencia con terceros | Politicas ACE 4 lit. b | Responsable y encargado | OBLIGATORIO | Grave num. 7 |
| 10 | Acuerdo de confidencialidad con contratistas de entidades publicas | LPDP 49 inc. final | Entidad publica y tercero | OBLIGATORIO (condicional) | - |
| 11 | Consentimiento previo, finalidad y cesionario identificado en transferencias | LPDP 40 | Responsable | OBLIGATORIO | Muy grave num. 6 |
| 12 | No transferir para finalidades distintas | LPDP 32, 59 lit. d | Responsable | OBLIGATORIO | Grave num. 3 y 6; muy grave num. 7 |
| 13 | Notificar a receptores rectificaciones y eliminaciones en 5 dias habiles | LPDP 21 inc. 3 | Responsable | OBLIGATORIO (condicional) | Grave num. 2, por conexion |
| 14 | Informar al titular intercambios y destinatarios | LPDP 7 lit. a, 8 | Responsable | OBLIGATORIO | Leve num. 8; grave num. 1 |
| 15 | Transferir solo a paises con nivel adecuado o garantizar tratamiento conforme a la LPDP | LPDP 44 inc. 1 a 3 | Responsable (emisor) | OBLIGATORIO | Muy grave num. 5 |
| 16 | Consentimiento previo en transferencias internacionales | LPDP 44 inc. final | Responsable | OBLIGATORIO | Muy grave num. 6 |
| 17 | Excepcion centroamericana | LPDP 44 inc. 4 | Responsable | CONDICIONAL (sin desarrollo) | - |
| 18 | Carga de la prueba en transferencias internacionales | LPDP 54 inc. 2 | Responsable | OBLIGATORIO (probar) | - |
| 19 | Poner en conocimiento de la ACE el flujo transfronterizo con informacion y registro de banco de datos | LPDP 45 inc. 2 | Responsable | OBLIGATORIO (sin mecanismo) | Leve num. 9, por conexion (incierto) |
| 20 | Solicitar opinion previa a la ACE | LPDP 45 inc. 1 | Responsable | RECOMENDADO | - |
| 21 | Transferencias internacionales solo a paises con proteccion equivalente; TLS; contratos; brechas 72 h | Politicas ACE 4 y 6 lit. d | Responsable y encargado | OBLIGATORIO | Grave num. 7 |
| 22 | Contenido minimo del DPA (finalidad, categorias, duracion, confidencialidad, seguridad, subcontratacion, incidentes, ARCO-POL, auditoria, devolucion, transferencias) | Sin norma especifica; bases indicadas en 5.6 | Responsable y encargado | RECOMENDADO (con partes OBLIGATORIAS) | - |

---

## 13. Requisitos funcionales derivados para PRIV-SV

1. Inventario de terceros con rol (encargado, subencargado, responsable receptor, tercero, entidad publica), pais, ubicaciones de datos, respaldos y contingencia, datos de contacto.
2. Inventario de bases de datos (registro de bancos de datos interno) vinculado al Registro de Actividades de Tratamiento (Politicas ACE Art. 4), exportable en formato apto para remitir a la ACE.
3. Asistente de clasificacion de flujos (transferencia vs encargo; nacional vs transfronterizo) con la postura configurable de la empresa (lectura conservadora por defecto) y advertencia de consulta juridica.
4. Repositorio de contratos y DPAs por tercero con contenido minimo verificado por checklist (seccion 5.6), fecha, version y vencimiento; alerta de terceros sin acuerdo de confidencialidad (Politicas ACE Art. 4 lit. b).
5. Generador de "lista de obligaciones espejo" (Art. 41) a partir del perfil de cumplimiento de la empresa.
6. Modulo de evaluacion de pais receptor con fichas de referencia, criterios, fuentes, fecha y conclusion documentada del usuario (Arts. 44 y 54 inc. 2).
7. Expediente probatorio de cada flujo internacional (consentimiento, contrato, adecuacion, seguridad, comunicacion a la ACE) exportable.
8. Generador del escrito de comunicacion del flujo transfronterizo a la ACE (Art. 45) y del escrito opcional de solicitud de opinion; registro de envio, acuse o constancia de imposibilidad.
9. Registro de receptores por titular o conjunto de datos, con generacion automatica de tareas de notificacion de 5 dias habiles (Art. 21 inc. 3) e informacion al encargado de revocaciones en 5 dias habiles (Art. 30).
10. Sincronizacion del inventario de encargados con el aviso de privacidad (Art. 24 lit. h) y la politica de privacidad (Art. 7), con alerta de inconsistencia y control de version.
11. Checklist de medidas de seguridad ACE aplicable a la empresa y a cada proveedor, con evidencias (certificaciones, informes) y fecha de revision anual (Politicas ACE Art. 8 lit. b).
12. Procedimiento de incidentes que incluya a proveedores, con plazo pactado de aviso del proveedor y cuenta regresiva de 72 h (Art. 25).
13. Modo "mi empresa como encargado": registro de responsables-clientes, instrucciones recibidas, medidas comprometidas, contratos, y obligaciones propias (Arts. 34, 36).
14. Vigilancia normativa: alertas sobre publicacion del decreto de reforma LPDP (numero por confirmar, ver 11.1), clausulas modelo de la ACE (Art. 50 lit. p), lista de paises adecuados o mecanismo del Art. 45.
15. Calculo orientativo de exposicion sancionatoria por control incumplido (Arts. 56 y 57), sin afirmar cumplimiento ni incumplimiento juridico.

---

## 14. Incertidumbres y puntos que requieren abogado

1. **Encargado extranjero = flujo transfronterizo?** La definicion de transferencia (Art. 4 lit. u) excluye al encargado, pero las de emisor y receptor (lit. k y o) lo incluyen y el Art. 45 usa "flujo transfronterizo". Debe definirse la postura juridica de la empresa para nube y SaaS extranjeros; este informe recomienda la lectura conservadora.
2. **Quien declara el nivel adecuado.** La ley no lo atribuye a nadie y la ACE no ha publicado lista ni criterios. Riesgo de infraccion muy grave (Art. 56 lit. c num. 5) con carga de la prueba en el responsable.
3. **Que son los "estandares internacionales" del Art. 44 y del Art. 54 inc. 2.** No definidos. Se propone documentar la referencia a Convenio 108+, Directrices OCDE, Estandares Iberoamericanos y RGPD como criterio de comparacion, previa validacion juridica.
4. **Mecanismo del Art. 45.** No existe formulario, plataforma ni plazo; no esta claro si la comunicacion debe ser previa o posterior, por flujo o por proveedor, ni cual es la consecuencia de omitirla. Decidir si se remite por escrito a la Direccion de Proteccion de Datos Personales o se espera al mecanismo, y documentar la decision.
5. **"Registro de banco de datos" del Art. 45.** No existe registro ante la ACE; confirmar con abogado que no hay obligacion general de inscripcion y que basta con el inventario interno (Registro de Actividades de Tratamiento).
6. **Excepciones al consentimiento en transferencias (Arts. 28, 5 lit. g frente a Arts. 40 y 44).** El Art. 56 lit. c num. 6 alude a "excepciones que establezca la ley" pero los Arts. 40 y 44 no las listan. Determinar si una transferencia necesaria para un contrato u obligacion legal (p. ej. envio de planillas a la AFP, reportes a autoridades, transferencias a aseguradoras) requiere consentimiento adicional.
7. **Contrato responsable-encargado.** El Art. 41 solo exige contrato con el "responsable receptor". La exigencia de contrato con encargados se apoya en las Politicas ACE Art. 4 lit. b y en el Art. 33 inc. 2; confirmar la suficiencia de DPAs de adhesion de proveedores globales (que no mencionan la LPDP) y si es necesario un anexo salvadoreno.
8. **Excepcion centroamericana.** Sin instrumento regional localizado; confirmar si existe algun acuerdo del COMIECO o del SICA sobre datos o comercio electronico aplicable, y si la excepcion exime del consentimiento.
9. **Alcance extraterritorial de las Politicas ACE Art. 2** ("operaciones internacionales vinculadas a ciudadanos salvadoreños"): su respaldo en la LPDP (Art. 2) es discutible; relevante para exigir cumplimiento a proveedores extranjeros.
10. **Notificacion de vulneraciones por el encargado.** El Art. 25 obliga al responsable; la ley no fija el plazo en que el encargado debe avisar al responsable ni si el encargado debe notificar directamente a la ACE. Pactar en contrato y validar.
11. **Reforma LPDP de sep. 2026.** Numero exacto de decreto no confirmado en fuente oficial primaria al 2026-09-24 (ver seccion 11.1); texto no localizado; publicacion no confirmada; alcance exacto de la reforma del Art. 16 respecto de "proveedores" y "encargado" pendiente de verificar contra el Diario Oficial.
12. **Fecha exacta de emision y publicacion de las Politicas ACE** (2 y 3 sep 2025 segun prensa) y si fueron publicadas en el Diario Oficial: relevante para el plazo de adecuacion de 3 meses del Art. 60.
13. **Subencargados.** La ley no los regula; solo "en conjunto con otros" (Art. 4 lit. j). Definir si el responsable debe autorizar previamente y si el subencargado debe figurar en el aviso.
14. **Responsabilidad del encargado frente a la ACE.** Aunque el Art. 2 lo convierte en sujeto obligado, la mayoria de tipos del Art. 56 se redactan desde el responsable; confirmar la sancionabilidad directa del encargado.

---

## 15. Fuentes consultadas

Fuentes primarias locales (todas consultadas el 2026-09-23):
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_decreto_144.txt` (LPDP, copia de la ACE; Arts. 2, 4, 5, 7, 8, 10, 12, 14, 17, 21, 24, 25, 26 a 34, 36, 40, 41, 44, 45, 49, 50, 54, 56 a 62).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\diario_oficial_2024-11-15_mh.txt` (D.O. N. 219, Tomo 445, 15 nov 2024; cotejo de Arts. 4, 7, 40, 41, 44, 45, 54, 56).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_politicas_protecciondatos.txt` (Politicas N. 001-0309025-DPDP, Arts. 1 a 9).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\lineamientos_dpo_OCR.txt` y `ocr\lineamientos_dpo\page-02.png` (Lineamientos DPO, D.O. Tomo 452, N. 146, 11 ago 2026; Arts. 1, 2, 3, 10, 11, 15, 23, 27, 37, 39, 40, 42).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\normativa_sancionadora_OCR.txt` (Normativa PAS, Art. 2).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\dictamen_11_2024_ley_original_OCR.txt` (Dictamen N. 11, 11 nov 2024; texto del Art. 45 en la iniciativa).
- `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\ace_form_nombramiento_delegado.txt` (formulario ACE version 07-07-2025).

Fuentes primarias en linea:
- Asamblea Legislativa, Decreto 144: https://www.asamblea.gob.sv/sites/default/files/documents/decretos/7A4FBD85-7E1B-46BE-9408-6FC549E53E00.pdf
- Asamblea Legislativa, nota oficial de la reforma (17 sep 2026): https://www.asamblea.gob.sv/node/14116
- Asamblea Legislativa, Dictamen N. 46 de la Comision de Economia (13 abr 2021, proyecto anterior, no vigente; consultado para descartar que fuera la reforma de 2026): https://www.asamblea.gob.sv/sites/default/files/documents/dictamenes/498798FA-A563-4830-A0C8-306AFBC71497.pdf
- Asamblea Legislativa, iniciativa ARENA 24 jun 2019 (antecedente, no vigente): https://www.asamblea.gob.sv/sites/default/files/documents/correspondencia/2A326CE8-F13A-4828-8640-648235C228BF.pdf
- Asamblea Legislativa, Decretos Emitidos en 2026 (verificacion del numero de decreto de la reforma, consultado 2026-09-24, llega solo hasta el Decreto N. 649 del 26 ago 2026): https://www.asamblea.gob.sv/leyes-y-decretos/decretos-por-anios/2026/0
- Asamblea Legislativa, Ultimos Decretos Aprobados (consultado 2026-09-24, indica contenido "Pendiente de Publicacion Material en el Diario Oficial"): https://www.asamblea.gob.sv/leyes-y-decretos/ultimos-aprobados
- ACE, formularios: https://ace.gob.sv/page/formularios (solo formularios ARCO-POL y nombramiento de delegado, version 07-07-2025; sin formularios de transferencia, registro de bases de datos ni clausulas modelo).
- ACE, politicas y normativa: https://ace.gob.sv/politicas.php (Decretos 143 y 144 con politicas, Lineamientos DPO NDPDDP.pdf, Normativa PAS PASDPDP.pdf).
- ACE, portal principal: https://ace.gob.sv/ (sin registro de bases de datos ni de transferencias).
- SICA, Protocolo de Guatemala al Tratado General de Integracion Economica Centroamericana: https://www.sica.int/documentos/protocolo-al-tratado-general-de-integracion-economica-centroamericana-protocolo-de-guatemala_1_116843.html
- SIECA, integracion economica centroamericana: https://www.sieca.int/integracion-economica-centroamericana/

Fuentes secundarias (prensa y firmas legales; usadas para orientacion y marcadas como tales):
- El Diario de Hoy, 17 sep 2026, reforma (Arts. 15 y 17 derogados; Art. 16 reformado con mencion a proveedores y encargado): https://www.eldiariodehoy.com/noticias/nacionales/asamblea-legislativa-deroga-obligatoriedad-de-las-empresas-privadas-de-nombrar-delegados-de-proteccion-de-datos-personales/93615/2026/
- elsalvador.com, 17 sep 2026, reforma: https://www.elsalvador.com/noticias/nacional/reforma-proteccion-datos-personales/1293875/2026/
- elsalvador.com, 12 sep 2026, comunicado ACE que deja sin efecto la fecha limite de nombramiento de delegado: https://www.elsalvador.com/dinero-y-negocios/entorno-economico/empresas-ley-de-proteccion-datos-el-salvador/1292968/2026/
- Infobae, 17 sep 2026: https://www.infobae.com/el-salvador/2026/09/17/el-salvador-la-asamblea-legislativa-elimina-la-obligacion-del-delegado-de-proteccion-de-datos-para-las-empresas/
- hoy.com.sv, 23 sep 2026: https://www.hoy.com.sv/tegnologia/reforman-ley-de-proteccion-de-datos-personales-para-facilitar-solicitudes-de-los-ciudadanos/
- Diario El Mundo, 12 sep 2025, vigencia de las Politicas ACE (emitidas 2 sep 2025, vigentes 3 sep 2025): https://diario.elmundo.sv/politica/vigentes-politicas-de-actuacion-y-manejo-de-datos-personales-en-el-salvador
- ContraPunto, 13 sep 2026, registro de delegados: https://www.contrapunto.com.sv/sin-fecha-para-nombrar-a-los-delegados-de-proteccion-de-datos-personales-la-ace-establece-el-registro-obligatorio/
- BLP Legal, registro obligatorio del delegado: https://blplegal.com/es/delegado-proteccion-datos-el-salvador-ace/
- BLP Legal, ley: https://blplegal.com/es/ley-para-la-proteccion-de-datos-personales-en-el-salvador/
- EY, lineamientos ACE (ago 2026): https://www.ey.com/es_ce/technical/tax/tax-alerts/el-salvador-la-agencia-de-ciberseguridad-del-estado-desarrolla-aspectos-relevantes-de-la-ley-de-proteccion-de-datos-personales
- Central Law, claves de cumplimiento: https://central-law.com/el-salvador-nueva-ley-de-proteccion-de-datos-personales-claves-para-su-cumplimiento-y-aplicacion/
- Consortium Legal, delegado (2 sep 2026): https://consortiumlegal.com/2026/09/02/delegado-proteccion-datos-el-salvador/
- Consortium Legal, fintech (12 feb 2025): https://consortiumlegal.com/2025/02/12/la-nueva-ley-de-proteccion-de-datos-personales-en-el-salvador-retos-y-oportunidades-para-el-sector-fintech/
- ECIJA, ley (2024/2025): https://www.ecija.com/actualidad-insights/ley-de-proteccion-de-datos-en-el-salvador/
- ECIJA, flujo transfronterizo (19 abr 2021, anterior a la ley): https://www.ecija.com/actualidad-insights/el-salvador-problematica-juridica-en-el-flujo-transfronterizo-de-datos-personales/
- ALTA, ley: https://altalegal.com/comunicacion/la-nueva-ley-salvadorena-de-proteccion-de-datos-personales/ y https://altalegal.com/comunicacion/proteccion-de-datos-en-el-salvador/
- Garcia Bodan, politicas ACE (3 oct 2025): https://garciabodan.com/en/el-salvador-strengthens-personal-data-protection/
- Documentacion publica de proveedores de nube (no verificada contra normativa salvadorena): Microsoft Products and Services DPA https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA ; Google Cloud Data Processing Addendum https://cloud.google.com/terms/data-processing-addendum ; AWS Data Processing Addendum https://docs.aws.amazon.com/whitepapers/latest/navigating-gdpr-compliance/aws-data-processing-addendum-dpa.html

Nota metodologica: ninguna de las fuentes secundarias consultadas contiene un analisis especifico de los Arts. 44 y 45 mas alla de parafrasear la ley; ninguna menciona una lista de paises adecuados, clausulas modelo de la ACE, un registro de bases de datos ni un mecanismo para comunicar flujos transfronterizos. La ausencia se toma como indicio, no como prueba, de que tales instrumentos no existen al 2026-09-23.
