# HALLAZGOS REGULATORIOS - Proteccion de Datos Personales en El Salvador

Documento definitivo del blueprint funcional. Fecha de consulta base: 2026-09-23 (con reverificaciones puntuales al 2026-09-24, indicadas donde corresponde).

Fuentes: nueve informes sweep_*.md de C:\Proyects\PRIV-SV\analisis\01_legal\ y su verificacion adversarial consolidada en C:\Proyects\PRIV-SV\analisis\01_legal\_verificacion_consolidada.json. Regla aplicada: solo se usan afirmaciones con veredicto CONFIRMADA o CORREGIDA (en su version corregida). Las REFUTADAS se descartaron (no se encontro ninguna en este corpus). Las NO_VERIFICABLES solo aparecen en la seccion 9, marcadas como tales.

Este documento describe obligaciones juridicas para orientar el diseno funcional de un software. No es asesoria legal. Toda decision juridica final requiere abogado.

---

## 1. Marco normativo vigente al 2026-09-23

| Instrumento | Tipo | Emisor | Fecha de publicacion | Vigencia (fecha) | Estado | Fuente |
|---|---|---|---|---|---|---|
| Ley para la Proteccion de Datos Personales, D.L. 144 | Ley | Asamblea Legislativa | D.O. 219, Tomo 445, 15-nov-2024 | 23-nov-2024 (Art. 64) | VIGENTE | ace_decreto_144.txt |
| Ley de Ciberseguridad y Seguridad de la Informacion, D.L. 143 | Ley | Asamblea Legislativa | D.O. 219, Tomo 445, 15-nov-2024 | 23-nov-2024 | VIGENTE (aplica solo a sector publico e infraestructura critica calificada; a la LPDP le aporta por remision del Art. 53 LPDP el procedimiento sancionador y la prescripcion) | asamblea_decreto_143_ciberseguridad.txt |
| Ley de Procedimientos Administrativos, D.L. 856 | Ley | Asamblea Legislativa | D.O. 30, Tomo 418, 13-feb-2018 | 13-feb-2019 | VIGENTE (supletoria de la LPDP por Art. 62; su aplicacion a la relacion titular-empresa privada es discutible porque su Art. 2 limita el ambito subjetivo a la Administracion Publica) | asamblea_decreto_856_lpa.txt |
| Politicas de Actuacion y Manejo de Datos Personales, N. 001-0309025-DPDP | Politica administrativa (ACE) | Agencia de Ciberseguridad del Estado | No confirmada en Diario Oficial; emision 2-sep-2025 y vigencia 3-sep-2025 segun prensa | 3-sep-2025 (segun prensa) | VIGENTE (declaradas de cumplimiento obligatorio en su propio Art. 2; fecha de publicacion oficial no verificada en fuente primaria) | ace_politicas_protecciondatos.txt; diario.elmundo.sv (secundaria) |
| Lineamientos para el Delegado de Proteccion de Datos Personales (ACE) | Normativa/lineamiento (ACE) | Agencia de Ciberseguridad del Estado | D.O. 146, Tomo 452, 11-ago-2026 | 19-ago-2026 | VIGENTE | lineamientos_dpo_OCR.txt |
| Normativa para el Desarrollo del Procedimiento Administrativo Sancionador (ACE) | Normativa/reglamento (ACE) | Agencia de Ciberseguridad del Estado | D.O. 146, Tomo 452, 11-ago-2026 | 19-ago-2026 | VIGENTE | normativa_sancionadora_OCR.txt |
| Decreto Legislativo N. 659 (reforma a la LPDP) | Ley (reforma) | Asamblea Legislativa | No publicado en Diario Oficial al 2026-09-24 | Pendiente (8 dias despues de publicacion, segun formula habitual de la LPDP) | APROBADA-PENDIENTE-PUBLICACION | asamblea.gob.sv/leyes-y-decretos/view/7022; asamblea.gob.sv/node/14116 |
| Decreto Legislativo N. 523 (reforma a la LPA, Art. 4-A documentos extranjeros) | Ley (reforma) | Asamblea Legislativa | D.O. 41, Tomo 450, 27-feb-2026 | 7-mar-2026 | VIGENTE (no afecta el computo de plazos del Art. 82 LPA) | asamblea_decreto_523_reforma_lpa.txt |
| Decreto Legislativo N. 332 (reforma a la Ley Especial contra los Delitos Informaticos y Conexos) | Ley (reforma) | Asamblea Legislativa | Segun fuentes secundarias/prensa oficial de la Asamblea, 25-jun-2025 | 3-jul-2025 (segun fuentes secundarias) | VIGENTE (numero de decreto y fechas de D.O./vigencia con confianza media, no confirmadas contra el texto integro del decreto) | asamblea.gob.sv/node/13592 y /node/13595 |
| Ley Crecer Juntos, D.L. 431 (deroga LEPINA) | Ley | Asamblea Legislativa | No verificada en esta ronda | 1-ene-2023 | VIGENTE | crecerjuntos.gob.sv/dist/documents/DECRETO_LEY.pdf |

Nota sobre el numero de decreto de la reforma de septiembre de 2026: el sweep de encargados_transferencias documenta con mayor cautela que, al 2026-09-24, el numero "659" no esta confirmado contra el listado oficial de decretos de la Asamblea (que en la verificacion llegaba solo hasta el Decreto 649) y que dos busquedas web independientes devolvieron numeros distintos e inconsistentes (659 y 660) para la misma reforma. El resto de los sweeps usa "Decreto 659" siguiendo la nota oficial de la Asamblea (node/14116) y multiples notas de prensa convergentes, por lo que este documento tambien lo usa, pero el numero exacto debe confirmarse contra el texto que finalmente publique el Diario Oficial antes de fijarlo en cualquier entregable posterior.

---

## 2. Linea de tiempo

```
2024
 |-- 12-nov-2024  Aprobacion D.L. 144 (LPDP) y D.L. 143 (Ciberseguridad)
 |-- 14-nov-2024  Sancion presidencial de ambos decretos
 |-- 15-nov-2024  Publicacion D.O. 219, Tomo 445
 |-- 23-nov-2024  VIGENCIA de la LPDP y de la Ley de Ciberseguridad (Art. 64 / Art. 32)
 v
2025
 |-- 23-feb-2025  Vencimiento del plazo de 3 meses del Art. 60 inc. 1 para que la ACE
 |                dictara politicas, medidas y guias (vencido sin cumplirse a tiempo)
 |-- 23-may-2025  Vencimiento del plazo de 6 meses del Art. 61 inc. 2 para que los
 |                sujetos obligados establecieran mecanismos ARCO-POL
 |-- 3-jul-2025   Vigencia (segun fuentes secundarias) de la reforma a la Ley Especial
 |                contra los Delitos Informaticos y Conexos (D.L. 332)
 |-- 2/3-sep-2025 Emision y vigencia (segun prensa) de las Politicas de Actuacion ACE
 |                N. 001-0309025-DPDP
 |-- 2/3-dic-2025 Vencimiento del plazo de 3 meses del Art. 60 inc. 2 para que los
 |                sujetos obligados se adecuaran a las Politicas ACE
 v
2026
 |-- 24-jul-2026  Emision de los Lineamientos para el Delegado (ACE)
 |-- 11-ago-2026  Publicacion D.O. 146, Tomo 452: Lineamientos DPO y Normativa PAS
 |-- 19-ago-2026  VIGENCIA de los Lineamientos DPO y de la Normativa PAS
 |-- 16-sep-2026  Fecha limite original (20 dias habiles desde la vigencia de los
 |                Lineamientos) para el registro transitorio de delegados; la ACE la
 |                dejo sin efecto segun prensa tras el anuncio de la reforma
 |-- 17-sep-2026  Aprobacion del Decreto Legislativo de reforma a la LPDP (57 votos),
 |                que elimina la obligatoriedad del delegado en el sector privado
 |-- 23/24-sep-2026  Fecha de consulta de este analisis; la reforma sigue
 |                APROBADA-PENDIENTE-PUBLICACION, sin texto oficial localizado
 v
FUTURO (sin fecha cierta)
 |-- Publicacion en el Diario Oficial de la reforma de septiembre de 2026 y su
 |   entrada en vigencia (8 dias despues, formula habitual de la LPDP)
```

---

## 3. La reforma de septiembre de 2026 (Decreto Legislativo N. 659)

**Estado:** APROBADA-PENDIENTE-PUBLICACION. Aprobada por la Asamblea Legislativa el 17-sep-2026 con 57 votos a favor (Infobae precisa 57 a favor y 1 en contra), iniciativa del Organo Ejecutivo por medio del Ministro de Justicia y Seguridad Publica. Al 2026-09-24 (un dia despues de la fecha de consulta base) se reverifico en vivo contra asamblea.gob.sv/leyes-y-decretos/view/7022 y asamblea.gob.sv/node/14116: el estado seguia siendo "Pendiente de Publicacion Material en el Diario Oficial y de Entrada en Vigencia", sin numero de Diario Oficial ni documento adjunto. El texto oficial completo del decreto no ha sido localizado por ningun sweep; todo su contenido articulo por articulo proviene de la nota oficial de la Asamblea (que describe el efecto general pero no cita el texto completo) y de prensa secundaria convergente (El Diario de Hoy, Infobae, elsalvador.com).

**Cambios reportados (segun fuente secundaria, no verificados contra texto oficial):**
- Deroga los Arts. 15 y 17 LPDP: elimina la obligatoriedad de nombrar delegado de proteccion de datos en las empresas privadas.
- Reforma el Art. 16: las funciones que hoy cumple el delegado pasarian a los "sujetos obligados" (la empresa misma), con lineamientos internos propios.
- Las solicitudes ARCO-POL se presentarian directamente ante la empresa (el "sujeto obligado"), no ante un delegado nombrado y certificado por la ACE.
- Reforma el Art. 47: el sector publico mantiene la figura del delegado, que puede recaer en el Oficial de Informacion.
- Reforma el Art. 51: el Presidente de la Republica nombra a un Director de Proteccion de Datos Personales dentro de la ACE, por un periodo de 3 anos.
- Segun la nota oficial de la Asamblea, se mantienen sin cambio los plazos existentes: 20 mas 20 dias habiles de respuesta, prevencion unica de 10 dias habiles, devolucion por incompetencia en 5 dias habiles, notificacion a terceros en 5 dias habiles y plazo de 5 dias habiles para atender la revocacion del consentimiento.

**Diseno de doble estado recomendado para el software:** dado que la reforma esta aprobada pero no vigente, el motor de reglas del producto debe modelar dos configuraciones activables por fecha de vigencia real (no por fecha de aprobacion):
1. Estado ACTUAL (vigente al 2026-09-24): delegado de proteccion de datos obligatorio en el sector privado (Arts. 15 y 17 LPDP), con las funciones de recepcion, prevencion, resolucion y notificacion ARCO-POL centralizadas en esa figura conforme al texto hoy vigente.
2. Estado FUTURO (activable solo cuando se confirme la publicacion en el Diario Oficial y transcurran los 8 dias de vacatio legis): delegado no obligatorio para el sector privado, funciones ARCO-POL asignadas al "sujeto obligado" (rol interno configurable por el cliente, no necesariamente un delegado certificado por la ACE).

El producto no debe activar el estado FUTURO automaticamente por la sola aprobacion legislativa; debe existir un control administrativo (bandera de configuracion) que el equipo del proyecto active manualmente cuando se confirme la publicacion oficial, y el sistema debe registrar la fecha de ese cambio para trazabilidad.

**Incertidumbres de la reforma:** (a) el numero exacto del decreto no esta confirmado en fuente primaria segun la verificacion mas cautelosa (sweep de encargados_transferencias); (b) no se sabe si la reforma toca tambien los Arts. 18 a 22, 24 lit. f o 30, que hoy atribuyen actos procedimentales al "delegado" en sentido literal; (c) no hay disposicion transitoria conocida para delegados ya nombrados y certificados bajo el regimen actual; (d) no esta claro si los Lineamientos para el Delegado (ACE) quedaran derogados, vigentes solo para el sector publico, o subsistentes como guia voluntaria para el sector privado.

---

## 4. Catalogo de obligaciones

Cada obligacion tiene un ID estable con formato OBL-<AREA>-<NN> para que los modulos del software lo referencien. Areas: AMBITO, PRIN, ARCO, DPO, AVISO, CONSENT, SENS, ENC, TRANSF, SEG, DOC, INC, CAP, AUD, SANC, RET.

### 4.1 Ambito y sujetos

#### OBL-AMBITO-01
**Norma:** Ley para la Proteccion de Datos Personales (D.L. 144)
**Articulo:** Art. 2
**Obligacion:** Toda persona natural o juridica, publica o privada, que trate datos personales de forma manual o automatizada, directamente o a traves de terceros, queda sujeta a la ley, incluso si no cumple sus requisitos y limites.
**A quien aplica:** Toda empresa privada cliente del software que trate datos personales de personas naturales en El Salvador.
**Implicacion para el software:** No existe un umbral de tamano de empresa o volumen de datos que exima de la ley; el producto no debe ofrecer una ruta de "no aplica" por tamano de empresa.
**Fuente oficial:** ace_decreto_144.txt (Art. 2); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-AMBITO-02
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 3 lit. a)
**Obligacion:** Se excluye el tratamiento de historial crediticio bajo la ley especial de buros de credito, pero esa exclusion NO aplica a integrantes del Sistema Financiero supervisados por la SSF respecto de datos que no sean historial crediticio: a ellos la LPDP les aplica plenamente sobre el resto de su informacion.
**A quien aplica:** Bancos, aseguradoras y demas supervisados por la SSF.
**Implicacion para el software:** El modulo de alcance debe permitir marcar "sujeto SSF" y excluir solo el modulo de historial crediticio, no el resto del tratamiento.
**Fuente oficial:** ace_decreto_144.txt (Art. 3 lit. a); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica solo a sujetos del sistema financiero, y solo respecto de historial crediticio)

#### OBL-AMBITO-03
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 3 lit. b)
**Obligacion:** Se excluye el tratamiento destinado exclusivamente a actividades de vida familiar o domestica, mientras no tenga proposito de divulgacion o utilizacion comercial.
**A quien aplica:** No aplica a empresas en el giro de su actividad comercial; es una exclusion pensada para personas naturales en su ambito privado.
**Implicacion para el software:** El producto, al ser B2B, no debe ofrecer esta exclusion como opcion de configuracion de un cliente empresarial.
**Fuente oficial:** ace_decreto_144.txt (Art. 3 lit. b); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

#### OBL-AMBITO-04
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 3 lit. c) y d)
**Obligacion:** Se excluyen el tratamiento con objeto de seguridad publica, defensa y persecucion del delito, y el realizado en registros publicos, registro del estado familiar y emision del DUI.
**A quien aplica:** Entidades publicas con esas competencias; no aplica por analogia a seguridad privada o prevencion de fraude de empresas.
**Implicacion para el software:** No ofrecer esta exclusion a clientes privados que hagan prevencion de fraude o seguridad privada, salvo confirmacion de abogado.
**Fuente oficial:** ace_decreto_144.txt (Art. 3 lit. c-d); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

### 4.2 Principios

#### OBL-PRIN-01
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 5 lit. g)
**Obligacion:** Todo tratamiento debe apoyarse en al menos una de seis bases de licitud: consentimiento expreso, ejecucion de contrato o medidas precontractuales, cumplimiento de obligacion legal, proteccion de intereses vitales, cumplimiento de un fin de interes publico, o intereses legitimos que no atenten contra los derechos del titular.
**A quien aplica:** Toda empresa que trate datos personales, para cada actividad de tratamiento.
**Implicacion para el software:** El modulo de RAT debe exigir, para cada actividad de tratamiento registrada, la seleccion de una base de licitud entre las seis, mas una justificacion textual.
**Fuente oficial:** ace_decreto_144.txt (Art. 5 lit. g); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-PRIN-02
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 5 lit. c)
**Obligacion:** Principio de consentimiento y finalidad: en el tratamiento y recoleccion de datos personales debe existir un consentimiento libre, especifico, informado, expreso e individualizado del titular, que establezca el fin, proposito y periodo de almacenamiento y tratamiento.
**A quien aplica:** Toda empresa; existe una tension no resuelta con OBL-PRIN-01 (ver seccion 8).
**Implicacion para el software:** El producto debe permitir registrar consentimiento incluso cuando la base de licitud elegida no sea el consentimiento, dado que este principio exige de todos modos una comunicacion clara de fin, proposito y periodo.
**Fuente oficial:** ace_decreto_144.txt (Art. 5 lit. c); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-PRIN-03
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 5 lit. i)
**Obligacion:** Principio de responsabilidad demostrada: la entidad que trata datos personales debe ser capaz de demostrar que ha implementado las medidas necesarias para cumplir la ley.
**A quien aplica:** Toda empresa.
**Implicacion para el software:** Fundamenta la necesidad de que el producto genere evidencia (logs, documentos firmados, registros con fecha) de cada control implementado, no solo texto declarativo.
**Fuente oficial:** ace_decreto_144.txt (Art. 5 lit. i); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-PRIN-04
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 5 lit. j)
**Obligacion:** Principio de ejercicio progresivo de facultades: los derechos de ninas, ninos y adolescentes se ejercen de forma progresiva segun su desarrollo evolutivo.
**A quien aplica:** Empresas que traten datos de menores de edad.
**Implicacion para el software:** El modulo de titulares debe permitir marcar a un titular como NNA y activar reglas especiales de consentimiento e informacion, sin fijar una edad numerica de corte porque la ley no la establece.
**Fuente oficial:** ace_decreto_144.txt (Art. 5 lit. j); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica solo cuando el titular es NNA)

#### OBL-PRIN-05
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 32
**Obligacion:** El tratamiento de datos personales por toda institucion o empresa privada solo puede efectuarse respecto de los fines previamente informados al titular; la empresa unicamente debe tratar los datos con relacion directa a la naturaleza de los servicios que presta o presto al titular, y en ningun caso puede transferir o tratar datos de terceros para ofrecer un servicio distinto o con una finalidad diferente a la que fueron recabados, sin autorizacion previa del titular.
**A quien aplica:** Toda empresa privada que trate datos personales.
**Implicacion para el software:** El RAT debe vincular cada tratamiento a la finalidad originalmente informada; el sistema debe alertar cuando se declare un uso de datos para un fin distinto al registrado, exigiendo nueva autorizacion del titular antes de continuar (coherente con el Art. 7 sobre finalidad ulterior).
**Fuente oficial:** ace_decreto_144.txt (Art. 32); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 4.3 Derechos ARCO-POL y procedimiento

#### OBL-ARCO-01
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 18 lit. a-g)
**Obligacion:** La solicitud ARCO-POL debe contener: identificacion y domicilio del titular; documentos de identidad; area que trata los datos (si se conoce); descripcion de los datos; derecho ejercido; elementos para localizar los datos; y firma o medio equivalente.
**A quien aplica:** Titular que ejerce un derecho ARCO-POL ante la empresa.
**Implicacion para el software:** El formulario de intake de solicitudes debe validar la presencia de estos siete campos antes de considerar la solicitud completa.
**Fuente oficial:** ace_decreto_144.txt (Art. 18); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-ARCO-02
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 18 inciso final
**Obligacion:** Si la solicitud es incompleta, el delegado debe prevenir por una sola ocasion, con 10 dias habiles para subsanar desde el dia siguiente a la notificacion; si no se subsana, se archiva sin mas tramite.
**A quien aplica:** El delegado (bajo el texto hoy vigente; ver seccion 3 sobre el estado futuro).
**Implicacion para el software:** El motor de plazos debe generar automaticamente la prevencion y el contador de 10 dias habiles, con archivo automatico si vence sin respuesta.
**Fuente oficial:** ace_decreto_144.txt (Art. 18 inciso final); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-ARCO-03
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 19
**Obligacion:** Si el delegado advierte que el responsable no es competente, debe comunicarlo al titular y devolver la peticion en 5 dias habiles posteriores a la recepcion.
**A quien aplica:** El delegado, cuando la solicitud no corresponde a esa empresa.
**Implicacion para el software:** Debe existir una accion de "declarar incompetencia" que dispare el contador de 5 dias habiles y notifique al titular.
**Fuente oficial:** ace_decreto_144.txt (Art. 19); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica solo cuando la empresa no es la competente)

#### OBL-ARCO-04
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 20
**Obligacion:** El plazo general de respuesta a una solicitud ARCO-POL es de 20 dias habiles, prorrogable por causas justificadas hasta otros 20 dias habiles adicionales.
**A quien aplica:** Toda empresa que reciba una solicitud ARCO-POL.
**Implicacion para el software:** Es el plazo maestro del motor de calendario; debe calcularse en dias habiles con la logica del Art. 82 LPA (ver seccion 5) y permitir registrar y justificar una unica prorroga.
**Fuente oficial:** ace_decreto_144.txt (Art. 20); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-ARCO-05
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 21 inciso 3
**Obligacion:** Si hubo comunicacion o transferencia de los datos, el delegado debe notificar la rectificacion, actualizacion o eliminacion a quienes los recibieron dentro de los 5 dias habiles posteriores a la determinacion de procedencia.
**A quien aplica:** Empresas que hayan transferido o comunicado los datos objeto de la solicitud a un tercero.
**Implicacion para el software:** El modulo de solicitudes debe cruzar con el registro de transferencias/receptores para generar automaticamente la lista de notificaciones pendientes.
**Fuente oficial:** ace_decreto_144.txt (Art. 21 inc. 3); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica solo si hubo transferencia previa de esos datos)

#### OBL-ARCO-06
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 22
**Obligacion:** La denegatoria (total o parcial) solo procede en los ocho supuestos tasados del articulo y debe notificarse motivada, con pruebas, en 3 dias habiles desde la decision, por el mismo medio senalado por el titular.
**A quien aplica:** Toda empresa que deniegue una solicitud ARCO-POL.
**Implicacion para el software:** El flujo de denegatoria debe forzar la seleccion de una causal tasada (no texto libre) y generar el contador de 3 dias habiles para notificar.
**Fuente oficial:** ace_decreto_144.txt (Art. 22); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-ARCO-07
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 23
**Obligacion:** El ejercicio de los derechos ARCO-POL es gratuito; solo pueden cobrarse costos de reproduccion, certificacion o envio, previamente publicados por el responsable.
**A quien aplica:** Toda empresa.
**Implicacion para el software:** No debe existir ninguna pantalla de cobro por atender una solicitud, salvo un modulo opcional de tarifas de reproduccion previamente publicadas.
**Fuente oficial:** ace_decreto_144.txt (Art. 23); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-ARCO-08
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 8
**Obligacion:** El derecho de acceso obliga a entregar al titular sus datos, quienes los consultaron y con que proposito, y si hubo intercambio con otras instituciones; en ningun caso puede revelarse datos de terceros aunque se vinculen con el titular.
**A quien aplica:** Toda empresa que responda una solicitud de acceso.
**Implicacion para el software:** El generador del informe de acceso debe filtrar automaticamente cualquier dato de un tercero distinto del titular antes de exportar la respuesta.
**Fuente oficial:** ace_decreto_144.txt (Art. 8); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-ARCO-09
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 9
**Obligacion:** La rectificacion debe resolverse en 20 dias habiles de forma gratuita; durante la verificacion, el responsable debe bloquear los datos en analisis y dar a conocer que estan en revision.
**A quien aplica:** Toda empresa que reciba una solicitud de rectificacion.
**Implicacion para el software:** El registro del dato debe soportar un estado "en revision/bloqueado" visible en el sistema mientras dura el tramite.
**Fuente oficial:** ace_decreto_144.txt (Art. 9); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-ARCO-10
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 10 incisos 1 y 2
**Obligacion:** La cancelacion procede solo en 7 causales tasadas (datos innecesarios, retiro de consentimiento, oposicion sin motivo legitimo prevalente, datos ilicitos, obligacion legal de suprimir, oferta directa a ninos, oferta de servicios de entidades publicas o privadas) y no procede en 6 supuestos (entre otros, perjuicio a terceros con orden de conservar, obligacion legal, libertad de expresion, datos disociados).
**A quien aplica:** Toda empresa que reciba una solicitud de cancelacion.
**Implicacion para el software:** El flujo de cancelacion debe forzar la seleccion de una causal de procedencia tasada y verificar contra las causales de improcedencia antes de ejecutar la supresion.
**Fuente oficial:** ace_decreto_144.txt (Art. 10); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

#### OBL-ARCO-11
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 10 inciso final
**Obligacion:** Ante una solicitud de olvido procedente sobre datos publicados en entorno electronico, el responsable debe suprimirlos e informar a otros responsables para que eliminen enlaces, copias o replicas.
**A quien aplica:** Empresas que hayan publicado los datos del titular en internet.
**Implicacion para el software:** El modulo de olvido debe generar una lista de "responsables terceros a notificar" ademas de ejecutar la supresion propia.
**Fuente oficial:** ace_decreto_144.txt (Art. 10 inciso final); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

#### OBL-ARCO-12
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 12
**Obligacion:** El derecho de oposicion no puede ejercerse cuando el tratamiento es necesario por interes publico o por interes legitimo prevalente del responsable o de un tercero, con especial cuidado si el titular es nino o nina.
**A quien aplica:** Empresas que reciban una solicitud de oposicion, incluida la oposicion a perfilado con fines de mercadotecnia directa.
**Implicacion para el software:** El flujo de oposicion debe permitir registrar la ponderacion de interes legitimo como motivacion de una eventual denegatoria.
**Fuente oficial:** ace_decreto_144.txt (Art. 12); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

#### OBL-ARCO-13
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 13
**Obligacion:** La limitacion procede solo en 4 supuestos: impugnacion de exactitud en verificacion, tratamiento ilicito con oposicion a la supresion, necesidad del titular para reclamaciones, y oposicion pendiente de ponderacion.
**A quien aplica:** Empresas que reciban una solicitud de limitacion.
**Implicacion para el software:** El dato limitado debe pasar a un estado de "solo conservacion, sin uso activo" distinguible del bloqueo cautelar de la rectificacion.
**Fuente oficial:** ace_decreto_144.txt (Art. 13); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

#### OBL-ARCO-14
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 14
**Obligacion:** La portabilidad exige que el tratamiento se base en consentimiento y sea automatizado; el responsable debe migrar los datos a otro responsable sin costo cuando el titular lo pida.
**A quien aplica:** Empresas cuyo tratamiento del dato solicitado se apoye en consentimiento y sea automatizado.
**Implicacion para el software:** El motor de portabilidad debe verificar ambos requisitos (base = consentimiento, tratamiento = automatizado) antes de habilitar la exportacion.
**Fuente oficial:** ace_decreto_144.txt (Art. 14); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

#### OBL-ARCO-15
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 6
**Obligacion:** La solicitud puede presentarla el titular, su representante con facultades especiales, o, si el titular fallecio, sus herederos o sucesores acreditando esa calidad con documentacion.
**A quien aplica:** Toda empresa, al recibir una solicitud.
**Implicacion para el software:** El intake debe soportar tres tipos de solicitante (titular, representante, heredero) con requisitos documentales distintos por tipo.
**Fuente oficial:** ace_decreto_144.txt (Art. 6); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-ARCO-16
**Norma:** Lineamientos para el Delegado de Proteccion de Datos Personales (ACE)
**Articulo:** Art. 32
**Obligacion:** Los responsables y delegados deben aceptar los formularios oficiales de la ACE aunque cuenten con modelos propios; no pueden rechazar una solicitud presentada en formulario oficial.
**A quien aplica:** Toda empresa con delegado nombrado bajo el regimen vigente.
**Implicacion para el software:** El intake debe permitir cargar directamente los 7 formularios oficiales ARCO-POL de la ACE (version 07-07-2025) ademas de un formulario propio del cliente.
**Fuente oficial:** lineamientos_dpo_OCR.txt (Art. 32); ace.gob.sv/page/formularios; fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-ARCO-17
**Norma:** Lineamientos para el Delegado de Proteccion de Datos Personales (ACE)
**Articulo:** Art. 33 inc. 4
**Obligacion:** Cuando un titular se considere agraviado por la resolucion que el delegado emita dentro de un procedimiento ARCO-POL, puede presentar un escrito ante la Direccion de Proteccion de Datos Personales de la ACE, senalando motivos y pruebas, dentro de los 10 dias habiles siguientes a la notificacion. Recibido el escrito, la ACE solicita informe al delegado o responsable para verificar sus actuaciones dentro del procedimiento administrativo.
**A quien aplica:** Empresas con delegado nombrado, cuando un titular reclame contra una resolucion ARCO-POL ante la Direccion de Proteccion de Datos de la ACE.
**Implicacion para el software:** El expediente de cada solicitud ARCO-POL debe permitir registrar un reclamo del titular ante la ACE como un estado posterior a la resolucion, con un campo para el informe de actuaciones que el delegado o responsable debe remitir a la ACE cuando esta lo requiera.
**Fuente oficial:** lineamientos_dpo_OCR.txt (Art. 33 inc. 4); fecha de consulta 2026-09-24 (ya citado en la tabla de plazos, seccion 5).
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica solo si el titular presenta el reclamo ante la Direccion de Proteccion de Datos y la ACE requiere informe)

### 4.4 Delegado y responsables internos

#### OBL-DPO-01
**Norma:** LPDP (D.L. 144)
**Articulo:** Arts. 15 y 17
**Obligacion:** Bajo el texto hoy vigente, la empresa privada esta obligada a nombrar un delegado de proteccion de datos personales.
**A quien aplica:** Toda empresa privada sujeta a la ley, mientras la reforma de septiembre de 2026 no entre en vigencia.
**Implicacion para el software:** El producto debe modelar esta obligacion como activa hoy, con una bandera de configuracion que la desactive automaticamente solo cuando se confirme la publicacion oficial de la reforma (ver seccion 3).
**Fuente oficial:** ace_decreto_144.txt (Arts. 15 y 17); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE (aprobada su derogacion, pendiente de publicacion; ver seccion 3)
**Clasificacion:** OBLIGATORIO

#### OBL-DPO-02
**Norma:** Lineamientos DPO (ACE)
**Articulo:** Art. 10
**Obligacion:** El nombramiento del delegado debe comunicarse a la ACE en un plazo maximo de 15 dias habiles contados a partir del dia siguiente al nombramiento.
**A quien aplica:** Empresas obligadas a nombrar delegado.
**Implicacion para el software:** El modulo de gestion del delegado debe generar el contador de 15 dias habiles al registrar un nuevo nombramiento.
**Fuente oficial:** lineamientos_dpo_OCR.txt (Art. 10); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica mientras el delegado sea obligatorio o la empresa mantenga uno voluntariamente; ver nota de reclasificacion en el registro de cambios)

#### OBL-DPO-03
**Norma:** Lineamientos DPO (ACE)
**Articulo:** Art. 8
**Obligacion:** El responsable debe notificar al delegado su nombramiento dentro de los 3 dias habiles siguientes a su designacion.
**A quien aplica:** Empresas obligadas a nombrar delegado.
**Implicacion para el software:** Generar recordatorio de 3 dias habiles a la persona designada como delegado.
**Fuente oficial:** lineamientos_dpo_OCR.txt (Art. 8); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica mientras el delegado sea obligatorio o la empresa mantenga uno voluntariamente; ver nota de reclasificacion en el registro de cambios)

#### OBL-DPO-04
**Norma:** Lineamientos DPO (ACE)
**Articulo:** Art. 10 inciso final
**Obligacion:** Toda modificacion de la informacion del delegado debe incorporarse en la plataforma de la ACE dentro de un plazo maximo de 10 dias habiles.
**A quien aplica:** Empresas con delegado registrado ante la ACE.
**Implicacion para el software:** Cualquier edicion del perfil del delegado en el sistema debe disparar un recordatorio de actualizacion ante la ACE en 10 dias habiles.
**Fuente oficial:** lineamientos_dpo_OCR.txt (Art. 10); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-DPO-05
**Norma:** Lineamientos DPO (ACE)
**Articulo:** Art. 18
**Obligacion:** El perfil del delegado debe reverificarse al menos cada 3 anos, con atestados de capacitacion o certificaciones.
**A quien aplica:** Empresas con delegado nombrado.
**Implicacion para el software:** Modulo de vencimientos de largo plazo (3 anos) con generacion automatica de tarea de reverificacion.
**Fuente oficial:** lineamientos_dpo_OCR.txt (Art. 18); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica mientras subsista la figura del delegado; ver nota de reclasificacion en el registro de cambios)

#### OBL-DPO-06
**Norma:** Lineamientos DPO (ACE)
**Articulo:** Art. 22
**Obligacion:** El responsable debe garantizar que el delegado reciba capacitacion al menos una vez al ano; el delegado debe elaborar un plan anual de capacitacion para el personal, incluida induccion para personal nuevo que trate datos.
**A quien aplica:** Empresas con delegado nombrado.
**Implicacion para el software:** Generar el evento anual de capacitacion del delegado y un plan de capacitacion documentable en el modulo de documentos.
**Fuente oficial:** lineamientos_dpo_OCR.txt (Art. 22); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica mientras subsista la figura del delegado; ver nota de reclasificacion en el registro de cambios)

#### OBL-DPO-07
**Norma:** Lineamientos DPO (ACE)
**Articulo:** Art. 36
**Obligacion:** El deber de confidencialidad del delegado subsiste durante 5 anos despues de su cese en el cargo.
**A quien aplica:** Delegados que cesen en el cargo.
**Implicacion para el software:** El registro de historial de delegados debe conservar el vinculo de confidencialidad por 5 anos tras el cese, para efectos de evidencia.
**Fuente oficial:** lineamientos_dpo_OCR.txt (Art. 36); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica al cesar el delegado en el cargo; ver nota de reclasificacion en el registro de cambios)

#### OBL-DPO-08
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 17
**Obligacion:** Cada dependencia, empleado o proveedor del responsable debe asistir y atender las peticiones canalizadas por el delegado en el ejercicio de sus funciones.
**A quien aplica:** Empleados y proveedores de la empresa, mientras el Art. 17 este vigente.
**Implicacion para el software:** El sistema debe poder registrar y auditar las peticiones internas del delegado a otras areas de la empresa, como evidencia de colaboracion interna.
**Fuente oficial:** ace_decreto_144.txt (Art. 17); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE (en riesgo de derogacion; ver seccion 3)
**Clasificacion:** OBLIGATORIO

#### OBL-DPO-09
**Norma:** Lineamientos DPO (ACE)
**Articulo:** Art. 30
**Obligacion:** El delegado debe informar al responsable, cuando sea necesario y al menos dos veces al ano, sobre el desarrollo de sus funciones y estadisticas ARCO-POL. No existe un informe anual obligatorio dirigido a la ACE (la ACE puede requerir informes cuando lo estime necesario).
**A quien aplica:** Empresas con delegado nombrado.
**Implicacion para el software:** El modulo de organizacion debe generar recordatorios semestrales para que el delegado produzca su informe de gestion, con estadisticas ARCO-POL extraidas automaticamente del propio sistema.
**Fuente oficial:** lineamientos_dpo_OCR.txt (Art. 30); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica mientras subsista la figura del delegado)

### 4.5 Aviso y politica de privacidad

#### OBL-AVISO-01
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 24 inc. 1
**Obligacion:** El responsable debe elaborar una politica de privacidad, con la cual el aviso de privacidad debe ser consistente.
**A quien aplica:** Toda empresa.
**Implicacion para el software:** El producto debe ofrecer una plantilla editable de politica de privacidad como documento base, previa a la generacion del aviso.
**Fuente oficial:** ace_decreto_144.txt (Art. 24); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-AVISO-02
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 24 lit. a-i)
**Obligacion:** El aviso de privacidad debe contener un contenido minimo de nueve elementos, incluidos identidad del responsable, finalidades, derechos ARCO-POL, uso de cookies y datos de contacto del encargado subcontratado (si existe).
**A quien aplica:** Toda empresa que recolecte datos personales.
**Implicacion para el software:** El generador de avisos debe validar la presencia de los nueve literales antes de permitir publicar el aviso.
**Fuente oficial:** ace_decreto_144.txt (Art. 24); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-AVISO-03
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 24 inciso final
**Obligacion:** El responsable no puede eximirse de comunicar el aviso de privacidad por escrito al titular en el momento en que este otorgue su consentimiento informado.
**A quien aplica:** Toda empresa que recolecte consentimiento.
**Implicacion para el software:** Todo formulario de captura de consentimiento debe mostrar u ofrecer el aviso de privacidad vigente en el mismo momento de la captura, no despues.
**Fuente oficial:** ace_decreto_144.txt (Art. 24 inciso final); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-AVISO-04
**Norma:** Lineamientos DPO (ACE)
**Articulo:** Art. 31
**Obligacion:** La documentacion de la autorizacion y publicacion del aviso de privacidad debe conservarse por el responsable durante un plazo minimo de 10 anos.
**A quien aplica:** Toda empresa con delegado nombrado bajo el regimen vigente.
**Implicacion para el software:** El modulo documental debe marcar cada version publicada del aviso con retencion minima de 10 anos, sin permitir su borrado antes de ese plazo.
**Fuente oficial:** lineamientos_dpo_OCR.txt (Art. 31); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-AVISO-05
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 7
**Obligacion:** El titular tiene derecho a conocer quienes resguardan sus datos personales, incluidos los proveedores de almacenamiento tercerizados (encargados) que usan la nube u otra infraestructura. Al recolectar datos, debe informarse previamente y de forma expresa, precisa e inequivoca: el proposito de la recoleccion y sus destinatarios; la existencia de la base de datos, respaldos y sitios de contingencia; la identidad y datos de contacto del responsable y del encargado; el contenido de los derechos ARCO-POL y los mecanismos para ejercerlos; y las medidas de seguridad que el responsable mantiene activas. Esta informacion no tiene costo y puede darse mediante la politica de privacidad. Si se proyecta un tratamiento con finalidad distinta a la original, debe informarse al titular, quien puede revocar la autorizacion inicial y debe otorgar una nueva.
**A quien aplica:** Toda empresa que recolecte datos personales.
**Implicacion para el software:** El generador de avisos/politicas de privacidad debe validar la presencia de estos cinco elementos (proposito y destinatarios, existencia de la base de datos, identidad y contacto de responsable/encargado, contenido de ARCO-POL, medidas de seguridad) de forma independiente al contenido minimo del Art. 24 (OBL-AVISO-02), y el modulo de RAT debe disparar una alerta de "nueva autorizacion requerida" cuando se declare un cambio de finalidad sobre datos ya recolectados.
**Fuente oficial:** ace_decreto_144.txt (Art. 7); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 4.6 Consentimiento y bases de licitud

#### OBL-CONSENT-01
**Norma:** LPDP (D.L. 144)
**Articulo:** Arts. 26 y 27
**Obligacion:** El consentimiento debe ser expreso, manifestado de forma verbal, escrita o por signos inequivocos, y ademas libre, especifico, informado, expreso e individualizado.
**A quien aplica:** Toda empresa cuyo tratamiento se apoye en consentimiento.
**Implicacion para el software:** El modulo de consentimiento debe registrar el medio de captura, el texto exacto presentado y la fecha, para poder demostrar los cinco atributos exigidos.
**Fuente oficial:** ace_decreto_144.txt (Arts. 26-27); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-CONSENT-02
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 26 inc. 4
**Obligacion:** Para datos personales sensibles, el consentimiento debe obtenerse por escrito mediante firma autografa del titular o su equivalente.
**A quien aplica:** Empresas que traten datos sensibles con base en consentimiento.
**Implicacion para el software:** El flujo de consentimiento para datos sensibles debe exigir firma (fisica o electronica valida) y no aceptar un simple clic de aceptacion.
**Fuente oficial:** ace_decreto_144.txt (Art. 26 inc. 4); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-CONSENT-03
**Norma:** LPDP (D.L. 144)
**Articulo:** Arts. 29 y 30
**Obligacion:** El titular puede revocar su consentimiento en cualquier momento, sin efecto retroactivo, mediante mecanismos expeditos, sencillos y gratuitos; el delegado cuenta con 5 dias habiles desde la recepcion de la solicitud para proceder.
**A quien aplica:** Toda empresa que trate datos con base en consentimiento.
**Implicacion para el software:** Debe existir un canal de revocacion tan simple como el de otorgamiento, con contador automatico de 5 dias habiles.
**Fuente oficial:** ace_decreto_144.txt (Arts. 29-30); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-CONSENT-04
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 30
**Obligacion:** Si los datos tambien son tratados por un encargado, el delegado debe informarle de la revocacion en el plazo de 5 dias habiles desde la emision de la resolucion, para que la ejecute de inmediato.
**A quien aplica:** Empresas que hayan subcontratado el tratamiento de esos datos a un encargado.
**Implicacion para el software:** El modulo de revocacion debe disparar automaticamente una notificacion al encargado registrado para ese tratamiento.
**Fuente oficial:** ace_decreto_144.txt (Art. 30); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

#### OBL-CONSENT-05
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 28
**Obligacion:** No se requiere consentimiento previo en ocho supuestos tasados (entre ellos fuentes de acceso publico, que no aplica si los datos son sensibles).
**A quien aplica:** Empresas que invoquen una excepcion al consentimiento.
**Implicacion para el software:** El modulo de bases de licitud debe listar las ocho excepciones como opciones seleccionables con su fundamento, distintas de las seis bases de licitud del Art. 5 lit. g.
**Fuente oficial:** ace_decreto_144.txt (Art. 28); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

#### OBL-CONSENT-06
**Norma:** Diseno funcional propio a partir del Art. 5 lit. i LPDP (principio de responsabilidad demostrada)
**Articulo:** Art. 5 lit. i
**Obligacion:** No existe un articulo que obligue expresamente a "registrar" la base de licitud en un sistema; esta es una recomendacion de diseno para poder demostrar cumplimiento.
**A quien aplica:** Toda empresa usuaria del software.
**Implicacion para el software:** El producto debe registrar, para cada actividad de tratamiento, la base de licitud elegida y una justificacion escrita, sin validar automaticamente si la base es juridicamente correcta (esa decision es de la empresa).
**Fuente oficial:** ace_decreto_144.txt (Art. 5 lit. i); analisis propio del sweep consentimiento_bases_sensibles; fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** RECOMENDADO

### 4.7 Datos sensibles, menores, salud, biometria

#### OBL-SENS-01
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 59 lit. a)
**Obligacion:** Esta prohibido crear bases de datos que contengan datos personales sensibles en contravencion a la ley.
**A quien aplica:** Toda empresa.
**Implicacion para el software:** El modulo de RAT debe forzar una justificacion de base legal cada vez que se declare una categoria de dato como sensible.
**Fuente oficial:** ace_decreto_144.txt (Art. 59 lit. a); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-SENS-02
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 37 inc. 1
**Obligacion:** Ninguna persona puede ser obligada a proporcionar sus datos sensibles; el responsable debe advertir al titular sobre su derecho a no prestarlos.
**A quien aplica:** Toda empresa que recolecte datos sensibles.
**Implicacion para el software:** Los formularios de captura de datos sensibles deben incluir una advertencia visible de que el dato es opcional, salvo excepcion aplicable.
**Fuente oficial:** ace_decreto_144.txt (Art. 37 inc. 1); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-SENS-03
**Norma:** LPDP (D.L. 144)
**Articulo:** Arts. 37 inc. 2-3 y 38 inc. 1
**Obligacion:** Existen tres excepciones al consentimiento para datos sensibles: salvaguarda de la vida del titular u otra persona cuando no puede consentir, tratamiento de datos de salud por profesional sujeto a secreto, y tratamiento amparado en interes general autorizado por ley.
**A quien aplica:** Empresas que invoquen alguna de estas excepciones (por ejemplo, clinicas empresariales, servicios medicos internos).
**Implicacion para el software:** El modulo de datos sensibles debe listar estas tres excepciones como alternativas al consentimiento escrito con firma.
**Fuente oficial:** ace_decreto_144.txt (Arts. 37-38); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

#### OBL-SENS-04
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 39
**Obligacion:** El tratamiento de datos de salud por establecimientos y profesionales sanitarios se remite a la Ley de Deberes y Derechos de los Pacientes y Prestadores de Servicios de Salud.
**A quien aplica:** Empresas del sector salud o con servicios medicos internos (clinicas empresariales).
**Implicacion para el software:** Para clientes del sector salud, el producto debe advertir que existe normativa sectorial adicional no cubierta por este analisis, sujeta a revision especifica.
**Fuente oficial:** ace_decreto_144.txt (Art. 39); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

#### OBL-SENS-05
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 56 lit. c num. 3
**Obligacion:** Usar datos personales de ninos, ninas y adolescentes sin el previo consentimiento de sus padres, representantes o tutores es infraccion muy grave; existe tension con el Art. 77 de la Ley Crecer Juntos, que permite a un adolescente (12 a 18 anos) consentir por si solo publicaciones de imagen con fines comerciales.
**A quien aplica:** Empresas que traten datos de NNA, en especial en marketing y publicaciones.
**Implicacion para el software:** El modulo de NNA debe distinguir entre "nino" (requiere consentimiento parental reforzado) y "adolescente" (podria consentir solo, segun la Ley Crecer Juntos), y marcar esta distincion como pendiente de confirmacion de abogado.
**Fuente oficial:** ace_decreto_144.txt (Art. 56 lit. c num. 3); crecerjuntos.gob.sv/dist/documents/DECRETO_LEY.pdf (Art. 77); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica solo cuando el titular es NNA; ver nota de reclasificacion en el registro de cambios)

#### OBL-SENS-06
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 42
**Obligacion:** Debe informarse previamente a NNA y a sus progenitores o tutores, en lenguaje adaptado a su edad, antes de que ejerzan los derechos ARCO-POL.
**A quien aplica:** Empresas que traten datos de NNA.
**Implicacion para el software:** Las plantillas de comunicacion dirigidas a titulares NNA deben tener una version de lenguaje simplificado, distinta de la version estandar para adultos.
**Fuente oficial:** ace_decreto_144.txt (Art. 42); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-SENS-07
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 4 lit. g)
**Obligacion:** La informacion biometrica (huella dactilar, reconocimiento facial, iris u otro identificador biometrico) esta incluida de forma expresa en la definicion legal de dato personal sensible. El responsable debe aplicarle el mismo regimen reforzado que a las demas categorias sensibles: consentimiento por escrito (Art. 26 inc. 4), advertencia del derecho a no prestarlo (Art. 37) y prohibicion de crear bases de datos sensibles fuera de la ley (Art. 59 lit. a). No existe lineamiento especifico de la ACE sobre biometria; verificado en ace.gob.sv/politicas.php el 2026-09-23, sin resultado (ver sweep_consentimiento_bases_sensibles.md, seccion 4.5, lineas 359-367).
**A quien aplica:** Empresas que traten datos biometricos, por ejemplo para control de asistencia o control de acceso a instalaciones.
**Implicacion para el software:** El catalogo de categorias de datos del RAT debe marcar automaticamente como "sensible" cualquier campo declarado como biometrico, disparando los mismos controles que el resto de datos sensibles (EIPD, consentimiento reforzado).
**Fuente oficial:** ace_decreto_144.txt (Art. 4 lit. g); sweep_consentimiento_bases_sensibles.md (seccion 4.5); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-SENS-08
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 26 inc. 4 y Art. 37
**Obligacion:** Cuando el tratamiento de datos biometricos se apoye en consentimiento (por ejemplo, control de asistencia con huella o rostro), este debe constar por escrito con firma autografa o equivalente, con advertencia expresa del derecho a no prestarlo; no existe mandato legal que imponga la biometria como metodo en el sector privado. El sweep recomienda ofrecer una alternativa no biometrica (tarjeta, PIN) para reforzar la libertad del consentimiento, especialmente en la relacion laboral, donde la subordinacion pone en duda esa libertad (Art. 27 lit. a); este punto en concreto requiere confirmacion de abogado.
**A quien aplica:** Empresas que recolecten datos biometricos con base en consentimiento, incluido el ambito laboral.
**Implicacion para el software:** El flujo de consentimiento biometrico debe exigir firma (no un simple clic) y debe permitir registrar, como campo separado, si se ofrecio una alternativa no biometrica al titular, dejando constancia de que este punto es una recomendacion de diseno y no un requisito legal expreso.
**Fuente oficial:** ace_decreto_144.txt (Art. 26 inc. 4, Art. 37); sweep_consentimiento_bases_sensibles.md (lineas 366, 690, 706); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica solo si la empresa recolecta datos biometricos; la alternativa no biometrica es una recomendacion de diseno, no un mandato legal expreso)

#### OBL-SENS-09
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 4 lit. f) y lit. g), Art. 7, Art. 12 lit. b), Art. 16 lit. g)
**Obligacion:** La imagen captada por camaras de seguridad es dato personal (Art. 4 lit. f) pero no es sensible por si misma, salvo que el sistema use reconocimiento facial, caso en el que se convierte en dato biometrico sensible (Art. 4 lit. g). La videovigilancia requiere aviso visible en el establecimiento (Art. 7 y Art. 16 lit. g, este ultimo referido a la funcion del delegado de publicar el aviso en lugares visibles) y una base de licitud, tipicamente interes legitimo ponderado frente al derecho de oposicion (Art. 12 lit. b), o consentimiento. Las Politicas ACE reconocen las camaras de seguridad como medida fisica de seguridad (Art. 4, Medidas Fisicas lit. b) pero no regulan su tratamiento como dato personal. No existe lineamiento especifico de la ACE sobre videovigilancia ni reconocimiento facial al 2026-09-23 (verificado en ace.gob.sv/politicas.php).
**A quien aplica:** Empresas que usen camaras de seguridad, en especial si incorporan reconocimiento facial.
**Implicacion para el software:** El RAT debe tratar la videovigilancia como una actividad de tratamiento propia, con su base de licitud declarada y su aviso especifico; si se marca "usa reconocimiento facial", el sistema debe reclasificar automaticamente el tratamiento como dato sensible y activar los controles de OBL-SENS-07/08 y una EIPD.
**Fuente oficial:** ace_decreto_144.txt (Arts. 4, 7, 12, 16); ace_politicas_protecciondatos.txt (Art. 4, Medidas Fisicas); sweep_consentimiento_bases_sensibles.md (linea 689); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica solo si la empresa usa videovigilancia; el regimen de dato sensible aplica solo si hay reconocimiento facial u otro identificador biometrico)

### 4.8 Tratamiento, encargados y proveedores

#### OBL-ENC-01
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 33 inc. 2
**Obligacion:** Los proveedores subcontratados con acceso a datos personales deben someterse a la LPDP y a los lineamientos que establezcan el responsable y la ACE.
**A quien aplica:** Empresas que subcontraten proveedores con acceso a datos personales.
**Implicacion para el software:** El modulo de proveedores debe exigir la vinculacion de cada proveedor con al menos un documento de sometimiento a la ley (contrato o adenda).
**Fuente oficial:** ace_decreto_144.txt (Art. 33 inc. 2); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-ENC-02
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 34
**Obligacion:** El responsable y, en su caso, el encargado deben limitar el tratamiento a la finalidad consentida, implementar medidas de seguridad y politicas de actuacion, y guardar confidencialidad.
**A quien aplica:** Toda empresa y sus encargados.
**Implicacion para el software:** El perfil de cada encargado debe registrar el alcance de finalidad autorizado, las medidas de seguridad exigidas y el compromiso de confidencialidad.
**Fuente oficial:** ace_decreto_144.txt (Art. 34); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-ENC-03
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 36
**Obligacion:** Las medidas de seguridad que la ACE determine para el responsable son tambien de obligatorio cumplimiento para el encargado del tratamiento.
**A quien aplica:** Encargados que traten datos por cuenta de la empresa.
**Implicacion para el software:** El checklist de medidas de seguridad de las Politicas ACE (seccion 4.10) debe aplicarse tambien a la evaluacion de proveedores/encargados, no solo a la empresa misma.
**Fuente oficial:** ace_decreto_144.txt (Art. 36); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-ENC-04
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 24 lit. h)
**Obligacion:** El aviso de privacidad debe contener los datos de contacto de la entidad subcontratada encargada del tratamiento, en caso de existir.
**A quien aplica:** Empresas con al menos un encargado del tratamiento.
**Implicacion para el software:** El generador de avisos debe insertar automaticamente los datos de contacto de los encargados registrados en el modulo de proveedores.
**Fuente oficial:** ace_decreto_144.txt (Art. 24 lit. h); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica solo si la empresa tiene al menos un encargado subcontratado; ver nota de reclasificacion en el registro de cambios)

#### OBL-ENC-05
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 41
**Obligacion:** El responsable que transfiere datos debe suscribir un contrato con el responsable receptor que prevea, como minimo, las mismas obligaciones a las que esta sujeto el transferente.
**A quien aplica:** Empresas que transfieran datos a otro responsable (no a un encargado).
**Implicacion para el software:** El modulo de transferencias debe exigir la vinculacion de un contrato antes de habilitar el registro de una transferencia a otro responsable.
**Fuente oficial:** ace_decreto_144.txt (Art. 41); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

#### OBL-ENC-06
**Norma:** Politicas de Actuacion ACE (N. 001-0309025-DPDP)
**Articulo:** Art. 4, bloque Medidas de Seguridad en Transferencias de Datos, lit. b)
**Obligacion:** Deben existir contratos de confidencialidad y contratos para la transferencia de datos como acuerdos legales obligatorios con terceros que tratan datos; su incumplimiento es infraccion grave por remision del Art. 56 lit. b num. 7 LPDP.
**A quien aplica:** Toda empresa con proveedores o receptores que traten datos.
**Implicacion para el software:** El modulo de proveedores debe bloquear la activacion de un encargado o receptor sin contrato de confidencialidad vinculado.
**Fuente oficial:** ace_politicas_protecciondatos.txt (Art. 4); ace_decreto_144.txt (Art. 56 lit. b num. 7); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-ENC-07
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 33 inc. 2 (lectura extensiva)
**Obligacion:** Cuando un encargado subcontrata a su vez a otro proveedor (subencargado) con acceso a los datos personales, ese subencargado tambien queda sometido a la LPDP y a los lineamientos que establezcan el responsable y la ACE, por tratarse igualmente de un "proveedor subcontratado con acceso a datos personales" en el sentido del Art. 33 inc. 2. La LPDP no usa el termino "subencargado" ni distingue niveles de subcontratacion; no se localizo lineamiento especifico de la ACE sobre cadenas de subcontratacion al 2026-09-23. Esta lectura es una interpretacion extensiva y requiere confirmacion de abogado.
**A quien aplica:** Empresas cuyo encargado subcontrate a su vez el tratamiento a un tercero.
**Implicacion para el software:** El modulo de proveedores debe permitir modelar cadenas de subcontratacion (proveedor de segundo nivel o subsiguientes), exigiendo que cada eslabon de la cadena tenga su propio documento de sometimiento a la ley, con una nota visible de que la base legal de esta exigencia es una interpretacion extensiva, no un articulo que use el termino "subencargado".
**Fuente oficial:** ace_decreto_144.txt (Art. 33 inc. 2); interpretacion extensiva, sin lineamiento ACE especifico sobre subencargados al 2026-09-23; fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica solo si existe una cadena de subcontratacion)

#### OBL-ENC-08
**Norma:** Diseno funcional propio a partir del Art. 34 lit. a) y Art. 5 lit. i) LPDP
**Articulo:** Art. 34 lit. a), en relacion con Art. 5 lit. i)
**Obligacion:** No existe un articulo expreso de la LPDP, las Politicas ACE, los Lineamientos DPO ni la Normativa Sancionadora que obligue a documentar por escrito las instrucciones que el responsable da al encargado sobre el tratamiento. Una busqueda web complementaria (ECIJA, BLP, Central Law, 2026-09-24) describe en terminos generales que el encargado debe seguir las instrucciones del responsable, sin citar un articulo especifico para esa obligacion de documentarlas. Se recomienda documentar las instrucciones como buena practica, apoyada en el deber del encargado de limitar el tratamiento a la finalidad consentida (Art. 34 lit. a) y en el principio de responsabilidad demostrada (Art. 5 lit. i).
**A quien aplica:** Empresas con al menos un encargado del tratamiento.
**Implicacion para el software:** El perfil de cada encargado en el modulo de proveedores debe incluir un campo de "instrucciones documentadas de tratamiento" (alcance, finalidad autorizada, tipos de datos, medidas de seguridad exigidas), presentado como buena practica recomendada y no como obligacion legal expresa.
**Fuente oficial:** ace_decreto_144.txt (Art. 34, Art. 5 lit. i); sin norma expresa localizada; fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** RECOMENDADO

#### OBL-ENC-09
**Norma:** Diseno funcional propio a partir del Art. 34 lit. a) y Art. 5 lit. h) LPDP
**Articulo:** Art. 34 lit. a), en relacion con Art. 5 lit. h)
**Obligacion:** No existe un articulo expreso de la LPDP, las Politicas ACE, los Lineamientos DPO ni la Normativa Sancionadora que obligue al encargado a devolver o eliminar los datos personales al finalizar la relacion contractual con el responsable. Se recomienda pactarlo contractualmente como buena practica, apoyada en el principio de temporalidad (Art. 5 lit. h: la conservacion debe limitarse al periodo necesario para el fin del tratamiento) y en el deber del encargado de limitar el tratamiento a la finalidad consentida (Art. 34 lit. a), finalidad que deja de existir al terminar el contrato.
**A quien aplica:** Empresas con al menos un encargado del tratamiento, al finalizar la relacion contractual.
**Implicacion para el software:** El modulo de proveedores debe generar, al marcar un encargado como "relacion finalizada", una tarea de verificacion de devolucion o eliminacion de datos, con campo de evidencia (constancia de devolucion o de borrado), presentado como buena practica recomendada y no como obligacion legal expresa.
**Fuente oficial:** ace_decreto_144.txt (Art. 34, Art. 5 lit. h); sin norma expresa localizada; fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** RECOMENDADO

### 4.9 Transferencias nacionales e internacionales y Art. 45

#### OBL-TRANSF-01
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 40
**Obligacion:** Toda transferencia de datos personales exige consentimiento previo del titular, informacion sobre la finalidad de la transferencia e identificacion del cesionario o de elementos que permitan identificarlo.
**A quien aplica:** Toda empresa que transfiera datos a otro responsable.
**Implicacion para el software:** El modulo de transferencias debe exigir estos tres elementos antes de registrar una transferencia como valida.
**Fuente oficial:** ace_decreto_144.txt (Art. 40); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-TRANSF-02
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 44 inc. 1
**Obligacion:** La transferencia internacional solo se permite cuando el pais receptor cumpla como minimo los principios de la LPDP o los estandares internacionales en la materia; las garantias nunca pueden ser menores a las exigidas en El Salvador.
**A quien aplica:** Empresas que transfieran datos fuera de El Salvador (incluye proveedores cloud extranjeros tratados como receptores, segun la lectura conservadora del sweep).
**Implicacion para el software:** El modulo de transferencias internacionales debe exigir una evaluacion documentada del nivel de proteccion del pais destino, dado que la ACE no ha publicado una lista de paises adecuados.
**Fuente oficial:** ace_decreto_144.txt (Art. 44 inc. 1); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica solo a empresas que realicen transferencias internacionales de datos; ver nota de reclasificacion en el registro de cambios)

#### OBL-TRANSF-03
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 44 inciso final
**Obligacion:** Toda transferencia internacional requiere consentimiento previo del titular, salvo excepciones establecidas en instrumentos internacionales que operen reciprocamente.
**A quien aplica:** Empresas con transferencias internacionales.
**Implicacion para el software:** El flujo de transferencia internacional debe exigir la captura de consentimiento especifico para ese destino, salvo que se documente una excepcion por instrumento internacional.
**Fuente oficial:** ace_decreto_144.txt (Art. 44 inciso final); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-TRANSF-04
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 44 inc. 4
**Obligacion:** Se exceptuan de las reglas generales los tratados de Integracion Economica Centroamericana; sin embargo no se localizo ningun reglamento o resolucion del COMIECO/SICA/SIECA que desarrolle esta excepcion para datos personales.
**A quien aplica:** Empresas con transferencias dentro de Centroamerica que pretendan invocar esta excepcion.
**Implicacion para el software:** No activar esta excepcion como opcion automatica; debe requerir validacion manual de abogado caso por caso.
**Fuente oficial:** ace_decreto_144.txt (Art. 44 inc. 4); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

#### OBL-TRANSF-05
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 45 inciso 2
**Obligacion:** En cualquier caso, el flujo transfronterizo de datos personales debe ponerse en conocimiento de la ACE, incluyendo la informacion requerida para la transferencia y el registro de banco de datos; la ACE no ha habilitado ningun formulario, plataforma ni procedimiento para cumplir esta obligacion.
**A quien aplica:** Toda empresa con flujos transfronterizos de datos.
**Implicacion para el software:** El producto debe registrar internamente esta obligacion como pendiente de cumplimiento por falta de canal habilitado por la autoridad, y alertar al cliente de que existe un riesgo de incumplimiento tecnico ajeno a su control.
**Fuente oficial:** ace_decreto_144.txt (Art. 45 inc. 2); ace.gob.sv/page/formularios y ace.gob.sv/politicas.php (verificado sin resultado, 2026-09-23 y 2026-09-24); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-TRANSF-06
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 45 inciso 1
**Obligacion:** El responsable puede (no debe) solicitar la opinion previa de la ACE sobre si un flujo transfronterizo cumple con la ley.
**A quien aplica:** Empresas con transferencias internacionales de alto riesgo o duda juridica.
**Implicacion para el software:** Ofrecer como funcionalidad opcional la generacion de una solicitud de opinion previa a la ACE, sin presentarla como obligatoria.
**Fuente oficial:** ace_decreto_144.txt (Art. 45 inc. 1); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** RECOMENDADO

#### OBL-TRANSF-07
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 54 inc. 2
**Obligacion:** En transferencias internacionales, la carga de la prueba recae en el responsable, quien debe demostrar que el tratamiento o la transferencia se realizo conforme a la ley o a estandares internacionales.
**A quien aplica:** Empresas con transferencias internacionales.
**Implicacion para el software:** El expediente de cada transferencia internacional debe conservar evidencia suficiente (contrato, evaluacion de pais destino, consentimiento) para sostener la carga de la prueba.
**Fuente oficial:** ace_decreto_144.txt (Art. 54 inc. 2); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-TRANSF-08
**Norma:** Politicas de Actuacion ACE
**Articulo:** Art. 4, bloque Medidas de Seguridad en Transferencias de Datos
**Obligacion:** Las transferencias deben usar protocolos de comunicacion segura (SSL/TLS), contar con contratos de confidencialidad y de transferencia, limitarse a paises con proteccion equivalente, y notificar brechas de seguridad en maximo 72 horas a la ACE, la Fiscalia y los titulares.
**A quien aplica:** Toda empresa con transferencias de datos, nacionales o internacionales.
**Implicacion para el software:** El checklist tecnico de transferencias debe incluir cifrado en transito como requisito no negociable antes de activar un flujo de transferencia.
**Fuente oficial:** ace_politicas_protecciondatos.txt (Art. 4 y Art. 6 lit. d); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 4.10 Seguridad (medidas ACE)

#### OBL-SEG-01
**Norma:** Politicas de Actuacion ACE
**Articulo:** Art. 4, Medidas Organizativas lit. a-f)
**Obligacion:** Deben existir seis medidas organizativas: Politica de Proteccion de Datos, Delegado de Proteccion de Datos, Capacitacion del Personal, Registro de Actividades de Tratamiento, Evaluaciones de Impacto en la Privacidad y Auditorias de Cumplimiento.
**A quien aplica:** Toda empresa privada sujeta a la LPDP.
**Implicacion para el software:** Estas seis medidas son el esqueleto de los modulos principales del producto (politica, delegado, capacitacion, RAT, EIPD, auditorias); ninguna tiene formato ni contenido definido por la ACE, por lo que el producto puede proponer un formato razonable y documentarlo como tal.
**Fuente oficial:** ace_politicas_protecciondatos.txt (Art. 4); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-SEG-02
**Norma:** Politicas de Actuacion ACE
**Articulo:** Art. 4, Medidas Tecnicas lit. a)
**Obligacion:** Control de acceso: implementacion de contrasenas seguras, autenticacion en dos pasos (2FA) y acceso restringido.
**A quien aplica:** Toda empresa privada sujeta a la LPDP, respecto de sus propios sistemas de tratamiento.
**Implicacion para el software:** El checklist de medidas tecnicas debe incluir 2FA como control verificable, con evidencia de configuracion (no ejecucion del control por el propio software del cliente, sino registro de que existe).
**Fuente oficial:** ace_politicas_protecciondatos.txt (Art. 4); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-SEG-03
**Norma:** Politicas de Actuacion ACE
**Articulo:** Art. 4, Medidas Tecnicas
**Obligacion:** Deben implementarse cifrado en reposo y transito, gestion de identidades y accesos, copias de respaldo, firewall/antivirus/IDS-IPS, y analisis de vulnerabilidades y pentesting periodicos.
**A quien aplica:** Toda empresa privada sujeta a la LPDP.
**Implicacion para el software:** El checklist tecnico debe listar cada control como item verificable con campo de evidencia adjunta (politica, contrato con proveedor de seguridad, reporte de pentest).
**Fuente oficial:** ace_politicas_protecciondatos.txt (Art. 4); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-SEG-04
**Norma:** Politicas de Actuacion ACE
**Articulo:** Art. 4, Medidas Tecnicas lit. g)
**Obligacion:** Digitalizacion: usar sistemas especializados que permitan gestionar y documentar el tratamiento de datos.
**A quien aplica:** Toda empresa privada sujeta a la LPDP.
**Implicacion para el software:** Esta clausula es, en efecto, el fundamento normativo directo de la existencia del producto: el propio software satisface este literal cuando se usa correctamente.
**Fuente oficial:** ace_politicas_protecciondatos.txt (Art. 4 lit. g); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-SEG-05
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 56 lit. b num. 5 y 7
**Obligacion:** No implementar las medidas, controles tecnicos o lineamientos de la ACE, o no cumplir las medidas de seguridad de las Politicas de Actuacion, son infracciones graves.
**A quien aplica:** Toda empresa privada sujeta a la LPDP.
**Implicacion para el software:** El estado de cumplimiento de cada medida de seguridad (OBL-SEG-01 a 04) debe vincularse a este riesgo sancionador especifico en la vista de riesgo del cliente.
**Fuente oficial:** ace_decreto_144.txt (Art. 56 lit. b num. 5 y 7); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-SEG-06
**Norma:** Politicas de Actuacion ACE
**Articulo:** Art. 4, Medidas Fisicas lit. e)
**Obligacion:** Debe implementarse eliminacion segura de documentos: uso de trituradoras de papel para documentos fisicos, y borrado seguro de dispositivos electronicos que contengan datos personales.
**A quien aplica:** Toda empresa privada sujeta a la LPDP.
**Implicacion para el software:** El checklist de medidas fisicas debe incluir "eliminacion segura" como control verificable, con campo de evidencia (politica de destruccion, contrato con proveedor certificado de destruccion, o constancia de borrado seguro de dispositivos).
**Fuente oficial:** ace_politicas_protecciondatos.txt (Art. 4, Medidas Fisicas lit. e); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-SEG-07
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 35
**Obligacion:** Las politicas de actuacion y manejo de datos personales que dicte la ACE tienen caracter imperativo para los sujetos obligados por la LPDP, incluidas las entidades privadas.
**A quien aplica:** Toda empresa privada sujeta a la LPDP.
**Implicacion para el software:** Este articulo es el fundamento legal directo (en la Ley, no solo en la propia Politica) de que las Politicas de Actuacion ACE (base de OBL-SEG-01 a 06 y de otras obligaciones de esta seccion) sean de cumplimiento obligatorio y no solo una recomendacion administrativa; el producto puede citarlo junto al Art. 4 de las Politicas ACE para reforzar la base legal de cada control tecnico u organizativo.
**Fuente oficial:** ace_decreto_144.txt (Art. 35); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 4.11 Documentacion (RAT, EIPD, politicas, procedimientos, registros)

#### OBL-DOC-01
**Norma:** Politicas de Actuacion ACE
**Articulo:** Art. 4, Medidas Organizativas lit. d)
**Obligacion:** Debe mantenerse un Registro de Actividades de Tratamiento (RAT) que documente como se recopilan, almacenan y utilizan los datos personales.
**A quien aplica:** Toda empresa privada sujeta a la LPDP.
**Implicacion para el software:** El RAT es el modulo central del producto; debe permitir registrar por cada actividad de tratamiento: finalidad, base de licitud, categorias de datos, encargados involucrados, transferencias y plazo de conservacion, dado que la ACE no ha fijado un formato oficial.
**Fuente oficial:** ace_politicas_protecciondatos.txt (Art. 4 lit. d); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-DOC-02
**Norma:** Politicas de Actuacion ACE
**Articulo:** Art. 4, Medidas Organizativas lit. e)
**Obligacion:** Deben realizarse Evaluaciones de Impacto en la Privacidad (EIPD) para identificacion y mitigacion de riesgos.
**A quien aplica:** Toda empresa privada sujeta a la LPDP; la ACE no fija un umbral de riesgo que determine cuando es obligatoria una EIPD especifica.
**Implicacion para el software:** El producto debe ofrecer una plantilla de EIPD y un criterio de activacion (por ejemplo: tratamiento de datos sensibles, uso de biometria, perfilado a gran escala) documentado como criterio propio, no legal.
**Fuente oficial:** ace_politicas_protecciondatos.txt (Art. 4 lit. e); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-DOC-03
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 33 inc. 1
**Obligacion:** El responsable debe establecer y documentar procedimientos para el ejercicio de los derechos ARCO-POL, con base en las politicas de actuacion de la ACE y las medidas de seguridad minimas necesarias.
**A quien aplica:** Toda empresa privada sujeta a la LPDP.
**Implicacion para el software:** El modulo de procedimientos debe generar un documento formal de "procedimiento ARCO-POL" versionado y fechado, distinto del flujo operativo del sistema.
**Fuente oficial:** ace_decreto_144.txt (Art. 33 inc. 1); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-DOC-04
**Norma:** Politicas de Actuacion ACE
**Articulo:** Art. 4, Medidas Organizativas lit. a)
**Obligacion:** Debe existir una Politica de Proteccion de Datos interna de la empresa.
**A quien aplica:** Toda empresa privada sujeta a la LPDP.
**Implicacion para el software:** Ofrecer una plantilla editable de politica interna, distinta de la politica de privacidad orientada al titular (OBL-AVISO-01).
**Fuente oficial:** ace_politicas_protecciondatos.txt (Art. 4 lit. a); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-DOC-05
**Norma:** Politicas de Actuacion ACE
**Articulo:** Art. 8 lit. b)
**Obligacion:** Deben realizarse auditorias anuales para evaluar el cumplimiento de las Politicas de Actuacion. La propia Politica cita como base el Art. 50 lit. l LPDP, pero ese literal en realidad solo faculta a la ACE para auditar las certificaciones que ella misma expide, no impone un deber de autoauditoria a las empresas; esto no invalida la obligacion (que nace directamente de la Politica ACE, declarada de cumplimiento obligatorio), pero es una referencia cruzada erronea que conviene no repetir en materiales del cliente.
**A quien aplica:** Toda empresa privada sujeta a la LPDP.
**Implicacion para el software:** El modulo de auditorias debe generar un evento anual recurrente, con generacion de un informe de auditoria interna como evidencia.
**Fuente oficial:** ace_politicas_protecciondatos.txt (Art. 8 lit. b); ace_decreto_144.txt (Art. 50 lit. l); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 4.12 Incidentes

#### OBL-INC-01
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 25, primer inciso
**Obligacion:** Toda vulneracion de seguridad de datos personales (dano, perdida, alteracion, destruccion, acceso ilegitimo o uso ilicito/no autorizado, incluso accidental) debe notificarse a la ACE, a la Fiscalia General de la Republica y a los titulares afectados en un plazo maximo de 72 horas desde que se tuvo conocimiento.
**A quien aplica:** Toda empresa privada sujeta a la LPDP.
**Implicacion para el software:** Es el modulo de respuesta a incidentes; debe iniciar un contador de 72 horas desde el momento en que se registra el "conocimiento" del incidente (campo capturado por el usuario, no inferido automaticamente).
**Fuente oficial:** ace_decreto_144.txt (Art. 25); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-INC-02
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 25, tercer inciso, lit. a-e)
**Obligacion:** La notificacion a la ACE debe contener, al menos: naturaleza del incidente, datos comprometidos, acciones correctivas inmediatas, recomendaciones al titular y medios para obtener mas informacion.
**A quien aplica:** Toda empresa que notifique una vulneracion a la ACE.
**Implicacion para el software:** El formulario de notificacion a la ACE debe forzar el llenado de estos cinco campos antes de generar el documento de notificacion.
**Fuente oficial:** ace_decreto_144.txt (Art. 25); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-INC-03
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 25, cuarto inciso
**Obligacion:** La notificacion a los titulares afectados unicamente debe contener naturaleza del incidente, datos comprometidos, recomendaciones al titular y medios para mas informacion (se omite el detalle de acciones correctivas internas).
**A quien aplica:** Toda empresa que notifique una vulneracion a titulares.
**Implicacion para el software:** Generar automaticamente dos plantillas distintas de notificacion (una para la ACE con 5 campos, otra para titulares con 4 campos) a partir del mismo registro de incidente.
**Fuente oficial:** ace_decreto_144.txt (Art. 25); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-INC-04
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 25, segundo inciso
**Obligacion:** Dentro del mismo plazo de 72 horas, el responsable debe iniciar (no necesariamente concluir) un proceso de revision exhaustiva para determinar la magnitud de la afectacion, las medidas correctivas y preventivas, y actualizar las politicas de seguridad.
**A quien aplica:** Toda empresa con un incidente en curso.
**Implicacion para el software:** El expediente de incidente debe registrar la fecha de inicio de la revision exhaustiva como un hito distinto de la notificacion misma.
**Fuente oficial:** ace_decreto_144.txt (Art. 25); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-INC-05
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 25, ultimo inciso
**Obligacion:** El responsable debe documentar toda vulneracion que ocasione un riesgo en la seguridad de los datos, incluyendo al menos fecha, motivo, hechos, efectos y medidas correctivas inmediatas y definitivas, a disposicion de la ACE.
**A quien aplica:** Toda empresa con incidentes que impliquen riesgo, hayan sido notificados o no a la ACE (por ejemplo, incidentes de bajo riesgo).
**Implicacion para el software:** El registro de incidentes debe ser obligatorio incluso para incidentes que la empresa decida no notificar por considerarlos de riesgo minimo, como evidencia preventiva.
**Fuente oficial:** ace_decreto_144.txt (Art. 25); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 4.13 Capacitacion

#### OBL-CAP-01
**Norma:** Lineamientos DPO (ACE)
**Articulo:** Art. 22
**Obligacion:** El delegado debe elaborar un plan anual de capacitacion dirigido al personal, incluyendo programas de induccion para el personal nuevo que trate datos personales.
**A quien aplica:** Empresas con delegado nombrado.
**Implicacion para el software:** El modulo de capacitacion debe permitir crear un plan anual con seguimiento de participacion, distinto del evento de capacitacion del propio delegado (OBL-DPO-06).
**Fuente oficial:** lineamientos_dpo_OCR.txt (Art. 22); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica mientras la empresa tenga delegado nombrado; ver nota de reclasificacion en el registro de cambios)

#### OBL-CAP-02
**Norma:** Politicas de Actuacion ACE
**Articulo:** Art. 4, Medidas Organizativas lit. c)
**Obligacion:** La capacitacion del personal es una de las seis medidas organizativas obligatorias de las Politicas ACE.
**A quien aplica:** Toda empresa privada sujeta a la LPDP.
**Implicacion para el software:** Esta obligacion es el fundamento independiente (fuera de los Lineamientos DPO) de la existencia del modulo de capacitacion, relevante incluso si el delegado deja de ser obligatorio tras la reforma.
**Fuente oficial:** ace_politicas_protecciondatos.txt (Art. 4 lit. c); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

### 4.14 Auditorias y certificaciones

#### OBL-AUD-01
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 50 lit. j, k, l
**Obligacion:** La ACE tiene la facultad de crear certificaciones o sellos de proteccion de datos y de auditar las que ella misma expida; al 2026-09-23/24 no existe ningun mecanismo de certificacion o sello para organizaciones habilitado por la ACE (solo un Programa de Certificacion de Delegados, personas, no organizaciones, que tampoco habia entrado en vigencia).
**A quien aplica:** Informativo para toda empresa; no genera una obligacion activa por ahora.
**Implicacion para el software:** El producto no debe ofrecer hoy un modulo de "certificacion ACE" para clientes, mas alla de dejar preparado el espacio para cuando la ACE lo habilite.
**Fuente oficial:** ace.gob.sv/politicas.php (verificado 2026-09-23 y 2026-09-24, sin resultado); ace_decreto_144.txt (Art. 50 lit. j-l); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE (facultad de la ACE, sin desarrollo)
**Clasificacion:** RECOMENDADO (no hay obligacion activa de certificarse; la referencia es informativa)

Nota: la obligacion de auditorias internas anuales ya esta catalogada como OBL-DOC-05 (Politicas ACE Art. 8 lit. b) para evitar duplicidad de ID.

### 4.15 Sanciones y evidencia

#### OBL-SANC-01
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 56
**Obligacion:** El catalogo de infracciones clasifica 9 leves, 7 graves y 10 muy graves.
**A quien aplica:** Toda empresa privada sujeta a la LPDP (referencia general, ver tabla de la seccion 6 para el detalle).
**Implicacion para el software:** Cada obligacion de este catalogo (seccion 4) debe poder vincularse a la infraccion especifica que su incumplimiento configuraria, para mostrar el riesgo asociado.
**Fuente oficial:** ace_decreto_144.txt (Art. 56); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-SANC-02
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 57
**Obligacion:** Las multas son de 1 a 10 salarios minimos mensuales del sector comercio para infracciones leves, 11 a 25 para graves y 26 a 40 para muy graves. Con el salario minimo vigente (US$408.80, Decreto Ejecutivo 11/2025 MTPS), los rangos en dolares son: leves US$408.80 a US$4,088.00; graves US$4,496.80 a US$10,220.00; muy graves US$10,628.80 a US$16,352.00.
**A quien aplica:** Toda empresa sancionada.
**Implicacion para el software:** El modulo de riesgo debe mostrar el rango de multa en dolares junto a cada obligacion incumplida, usando el salario minimo vigente como parametro configurable (no hardcodeado, porque puede cambiar).
**Fuente oficial:** ace_decreto_144.txt (Art. 57); jurisprudencia.gob.sv/DocumentosBoveda/D/2/2020-2029/2025/05/10A4DA.PDF (Decreto Ejecutivo 11/2025); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica solo a empresas efectivamente sancionadas; ver nota de reclasificacion en el registro de cambios)

#### OBL-SANC-03
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 58
**Obligacion:** Determinada la procedencia de la sancion, la ACE puede ordenar al infractor que adopte las medidas necesarias para restablecer la legalidad alterada; las sanciones no eximen de responsabilidades civiles o penales.
**A quien aplica:** Empresas sancionadas.
**Implicacion para el software:** El expediente de sancion debe permitir registrar medidas correctivas ordenadas por la ACE como tareas de seguimiento adicionales a la multa.
**Fuente oficial:** ace_decreto_144.txt (Art. 58); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

#### OBL-SANC-04
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 59
**Obligacion:** Se prohibe crear bases con datos sensibles en contravencion de la ley, tratar categorias especiales sin observar el Titulo respectivo, revelar o comercializar datos conocidos por razon del cargo, y utilizar/transferir/compartir/comercializar informacion de las bases en contravencion de la ley.
**A quien aplica:** Toda empresa y su personal.
**Implicacion para el software:** Estas cuatro prohibiciones deben aparecer como reglas de "nunca hacer" en la capacitacion del personal (OBL-CAP-01/02).
**Fuente oficial:** ace_decreto_144.txt (Art. 59); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-SANC-05
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 54 inc. 1
**Obligacion:** La carga de la prueba de haber obtenido el consentimiento y de haber comunicado el aviso de privacidad recae especificamente en el responsable.
**A quien aplica:** Toda empresa.
**Implicacion para el software:** Justifica que el producto conserve como evidencia probatoria (no solo operativa) cada registro de consentimiento y cada version publicada del aviso, con sello de fecha inalterable.
**Fuente oficial:** ace_decreto_144.txt (Art. 54 inc. 1); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-SANC-06
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 50 lit. t)
**Obligacion:** La ACE puede solicitar a entidades publicas y privadas informacion sobre antecedentes, documentos, programas u otros elementos relativos al tratamiento de datos personales.
**A quien aplica:** Toda empresa requerida por la ACE.
**Implicacion para el software:** El producto debe poder generar rapidamente un paquete de evidencia exportable (RAT, politicas, contratos, registros de incidentes y de solicitudes ARCO-POL) ante un requerimiento de la ACE.
**Fuente oficial:** ace_decreto_144.txt (Art. 50 lit. t); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-SANC-07
**Norma:** LPDP (D.L. 144)
**Articulo:** Art. 53, en relacion con la Ley de Ciberseguridad (D.L. 143) Art. 28-29
**Obligacion:** El procedimiento sancionador y la prescripcion de infracciones y sanciones de la LPDP se rigen por la Ley de Ciberseguridad; las infracciones prescriben a los 5 anos.
**A quien aplica:** Toda empresa sujeta a un procedimiento sancionador.
**Implicacion para el software:** El plazo de retencion minima de evidencia de descargo (OBL-RET-07) debe alinearse con este plazo de prescripcion de 5 anos como referencia, no como regla legal expresa de retencion.
**Fuente oficial:** ace_decreto_144.txt (Art. 53); asamblea_decreto_143_ciberseguridad.txt (Art. 29); normativa_sancionadora_OCR.txt (Art. 47); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica solo cuando existe un procedimiento sancionador en curso; ver nota de reclasificacion en el registro de cambios)

### 4.16 Retencion en leyes conexas

#### OBL-RET-01
**Norma:** Codigo de Comercio
**Articulo:** Arts. 451 y 454
**Obligacion:** Los comerciantes deben conservar los registros de su giro por 10 anos, y hasta 5 anos despues de la liquidacion de sus negocios mercantiles; esto incluye cartas, telegramas y facturas que sirvan de comprobante contable.
**A quien aplica:** Toda empresa comerciante.
**Implicacion para el software:** Los registros contables/comerciales vinculados a titulares (facturas, comprobantes) deben tener retencion minima de 10 anos, distinta de la retencion del expediente ARCO-POL.
**Fuente oficial:** Codigo de Comercio (Arts. 451 y 454), texto oficial de asamblea.gob.sv; fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica a documentacion mercantil, no a todo dato personal)

#### OBL-RET-02
**Norma:** Codigo Tributario
**Articulo:** Art. 147
**Obligacion:** Los libros de contabilidad, comprobantes, registros especiales, declaraciones tributarias y pruebas de retenciones deben conservarse por 10 anos desde su emision o recibo.
**A quien aplica:** Toda empresa contribuyente.
**Implicacion para el software:** Los documentos fiscales con datos personales (por ejemplo, de empleados o clientes) deben marcarse con retencion tributaria de 10 anos, independiente de cualquier solicitud de cancelacion ARCO-POL.
**Fuente oficial:** Codigo Tributario (Art. 147), texto oficial; fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica a documentacion tributaria)

#### OBL-RET-03
**Norma:** Ley Contra el Lavado de Dinero y de Activos (LCLDA)
**Articulo:** Arts. 10 lit. b y 12
**Obligacion:** Los sujetos obligados deben conservar la documentacion de operaciones por 5 anos desde la finalizacion de cada operacion, y mantener por no menos de 15 anos los registros que permitan reconstruir transacciones nacionales e internacionales.
**A quien aplica:** Sujetos obligados bajo la LCLDA (Art. 2): entre otros, bancos, aseguradoras, casas de cambio, notarios en ciertas operaciones. No aplica a toda empresa.
**Implicacion para el software:** Para clientes que sean sujetos obligados LCLDA, el modulo de retencion debe permitir marcar registros con retencion extendida de 15 anos, mas alla del plazo general de prescripcion sancionadora de la LPDP.
**Fuente oficial:** LCLDA (Arts. 10 y 12), texto oficial ssf.gob.sv; fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica solo a sujetos obligados LCLDA)

#### OBL-RET-04
**Norma:** Instructivo de la UIF (Acuerdo 380)
**Articulo:** Art. 59
**Obligacion:** Debe conservarse por no menos de 15 anos toda la documentacion que ampara la apertura de cuentas o relaciones contractuales, copias de identificacion y transacciones.
**A quien aplica:** Sujetos obligados bajo la LCLDA.
**Implicacion para el software:** Refuerza OBL-RET-03 con una fuente reglamentaria adicional; mismo alcance de aplicacion condicionada.
**Fuente oficial:** Instructivo UIF, uif.gob.sv (Art. 59); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL

#### OBL-RET-05
**Norma:** Norma Tecnica del Expediente Clinico (MINSAL)
**Articulo:** Art. 34
**Obligacion:** El expediente clinico debe conservarse durante 10 anos en total (5 anos en archivo activo mas 5 en archivo pasivo desde la ultima atencion), con eliminacion documentada por actas.
**A quien aplica:** Clientes del sector salud o con servicios medicos internos.
**Implicacion para el software:** Para ese segmento, el modulo de retencion debe ofrecer este plazo especifico distinto del plazo general de datos sensibles de salud.
**Fuente oficial:** Norma Tecnica del Expediente Clinico, asp.salud.gob.sv (Art. 34); fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** CONDICIONAL (aplica al sector salud)

#### OBL-RET-06
**Norma:** Ley de Firma Electronica
**Articulo:** Art. 13-A
**Obligacion:** Para que la conservacion electronica de un documento cumpla la exigencia legal, la informacion debe ser consultable en cualquier momento, conservarse en el formato original o uno que la reproduzca con exactitud, y mantenerse integra, legible, completa y sin alteraciones.
**A quien aplica:** Toda empresa que conserve electronicamente documentos con relevancia legal (consentimientos, avisos, contratos).
**Implicacion para el software:** El motor de almacenamiento documental del producto debe garantizar estos cuatro requisitos (consultabilidad, formato fiel, integridad, no alteracion) como requisito tecnico transversal.
**Fuente oficial:** Ley de Firma Electronica (Art. 13-A), factura.gob.sv; fecha de consulta 2026-09-24.
**Vigencia:** VIGENTE
**Clasificacion:** OBLIGATORIO

#### OBL-RET-07
**Norma:** Normativa para el Procedimiento Administrativo Sancionador (ACE)
**Articulo:** Art. 47
**Obligacion:** Las infracciones y sanciones de la LPDP prescriben en 5 anos; este plazo se usa como referencia de retencion minima recomendada para el expediente de descargo de cada obligacion (evidencia de cumplimiento), sin que exista una norma expresa que fije el plazo de conservacion del expediente ARCO-POL u otros expedientes de cumplimiento.
**A quien aplica:** Toda empresa que use el producto como repositorio de evidencia de cumplimiento.
**Implicacion para el software:** Fijar como retencion minima por defecto (configurable) 5 anos para todo expediente de evidencia de cumplimiento, con opcion de extenderlo si aplica otra norma conexa (por ejemplo, OBL-RET-01 a 05).
**Fuente oficial:** normativa_sancionadora_OCR.txt (Art. 47); fecha de consulta 2026-09-23.
**Vigencia:** VIGENTE
**Clasificacion:** RECOMENDADO

---

## 5. Tabla de plazos

| Norma | Articulo | Plazo | Unidad | Inicio del computo | Suspension/prorroga | Regla para el software |
|---|---|---|---|---|---|---|
| LPDP | Art. 18 inc. final | 10 | dias habiles | Dia siguiente a la notificacion de la prevencion | Prorroga no prevista; una sola prevencion | Archivo automatico si vence sin subsanacion |
| LPDP | Art. 19 | 5 | dias habiles | Recepcion de la solicitud | No prevista | Generar devolucion motivada al titular |
| LPDP | Art. 20 | 20 (+20) | dias habiles | Recepcion de la solicitud (Actualizacion 2026-09-24, fase 3: igual que matriz_obligaciones.json OBL-ARCO-10; no resuelto si la prevencion del Art. 18 suspende este computo, ver incertidumbre 16) | Una prorroga de hasta 20 dias habiles adicionales, por causa justificada | Plazo maestro; requiere motivo documentado para prorrogar |
| LPDP | Art. 21 inc. 3 | 5 | dias habiles | Determinacion de procedencia de la solicitud | No prevista | Solo si hubo transferencia previa de esos datos |
| LPDP | Art. 22 | 3 | dias habiles | Adopcion de la decision de denegar | No prevista | Notificar por el medio senalado por el titular |
| LPDP | Art. 9 | 20 | dias habiles | Recepcion de la solicitud de rectificacion | No prevista expresamente | Bloqueo cautelar del dato durante el tramite |
| LPDP | Art. 25 | 72 | horas | Conocimiento de la vulneracion | No hay excepcion prevista; ambiguo si corridas u horas habiles (Art. 82 LPA) | Adoptar por defecto horas corridas (criterio conservador) con nota de incertidumbre visible |
| LPDP | Art. 29-30 | 5 | dias habiles | Recepcion de la solicitud de revocacion | No prevista | Notificar al encargado en otros 5 dias habiles desde la resolucion |
| LPDP | Art. 60 inc. 1 | 3 | meses | Vigencia de la ley (23-nov-2024) | Ninguna (plazo para la ACE, ya vencido: 23-feb-2025) | Solo referencia historica |
| LPDP | Art. 60 inc. 2 | 3 | meses | Emision de cada disposicion de la ACE | No resuelto si cada nueva disposicion reabre el plazo | Tratar cada politica/lineamiento nuevo como potencial reapertura, pendiente de confirmar |
| LPDP | Art. 61 inc. 2 | 6 | meses | Vigencia de la ley (23-nov-2024) | Ninguna (ya vencido: 23-may-2025) | Solo referencia historica |
| Lineamientos DPO | Art. 8 | 3 | dias habiles | Designacion del delegado | No prevista | Recordatorio al delegado designado |
| Lineamientos DPO | Art. 10 inc. 1 | 15 | dias habiles | Dia siguiente al nombramiento | No prevista | Comunicacion a la ACE |
| Lineamientos DPO | Art. 10 inc. final | 10 | dias habiles | Modificacion de datos del delegado | No prevista | Actualizacion en plataforma ACE |
| Lineamientos DPO | Art. 12 | 15 | dias habiles | Solicitud de credencial | No prevista | Emision de credencial por la ACE |
| Lineamientos DPO | Art. 12 | 10 | dias habiles | No inscripcion del delegado | No prevista | Nombrar otro delegado |
| Lineamientos DPO | Art. 18 | 3 | anos | Nombramiento del delegado | No prevista | Reverificacion periodica del perfil |
| Lineamientos DPO | Art. 22 | 1 | ano | Nombramiento/inicio del periodo | No prevista | Capacitacion anual del delegado |
| Lineamientos DPO | Art. 33 | 3 | dias habiles | Emision de la resolucion del delegado | No prevista | Notificacion al interesado |
| Lineamientos DPO | Art. 33 inc. 4 | 10 | dias habiles | Notificacion de la resolucion | No prevista | Reclamo del titular ante la Direccion de Proteccion de Datos de la ACE |
| Lineamientos DPO | Art. 36 | 5 | anos | Cese del delegado en el cargo | No prevista | Confidencialidad subsistente |
| Normativa PAS (ACE) | Art. 12 | 90 | dias habiles | Dia siguiente al informe de apertura | Prorrogable por resolucion motivada segun la LPA | Diligencias preliminares de investigacion |
| Normativa PAS (ACE) | Art. 21 | 5 | dias habiles | Dia siguiente a la notificacion del emplazamiento | No prevista; si no comparece, hechos contestados negativamente | Contestacion del presunto infractor |
| Normativa PAS (ACE) | Art. 29 | 10 | dias habiles | Solo en via ordinaria, antes de la resolucion final | No prevista | Alegatos finales |
| Normativa PAS (ACE) | Art. 30 | 8 | dias habiles | Conclusion de la instruccion | No prevista | Remision del expediente al Director de Proteccion de Datos |
| Normativa PAS (ACE) | Art. 32 | 15 | dias habiles | Recepcion del expediente por el Director | No prevista | Resolucion final |
| Normativa PAS (ACE) | Art. 34 | 72 | horas | Dictada la resolucion final sancionatoria | No prevista | Aviso de la ACE a la Fiscalia si hay indicio penal |
| Normativa PAS (ACE) | Art. 35 | 15 | dias calendario | Adopcion de medidas provisionales previas | Caducidad si no se inicia el procedimiento en ese plazo | Confirmar/modificar/dejar sin efecto en el auto de inicio |
| Normativa PAS (ACE) | Art. 44 | 15 | dias habiles | Notificacion de la sancion | No prevista | Pago de la multa en Tesoreria del Ministerio de Hacienda |
| Normativa PAS (ACE) | Art. 47 | 5 | anos | Comision de la infraccion | Computo segun Art. 149 LPA | Prescripcion de infracciones y sanciones |
| Ley de Ciberseguridad | Art. 8 lit. v | 72 | horas | Advertencia de indicios de delito por la ACE | No prevista | Obligacion de la ACE hacia la FGR, no de la empresa |
| LPA (supletoria) | Art. 82 | - | dias/horas habiles | Dia siguiente a la notificacion o publicacion | Prorroga al primer dia habil si el vencimiento cae en inhabil | Regla general de computo cuando la LPDP no lo resuelve |
| LPA (supletoria) | Art. 83 | hasta la mitad del plazo original | dias | Solicitud de ampliacion | No aplica a plazo de conclusion del procedimiento ni de recursos | Prorrogas administrativas discrecionales de la ACE |

---

## 6. Tabla de infracciones y multas

| Clasificacion (Art. 56) | Ejemplo de conducta | Multa (Art. 57) | Rango en USD (SM US$408.80) | Obligacion relacionada (ver catalogo) | Evidencia preventiva |
|---|---|---|---|---|---|
| Leve | No publicar datos de contacto del encargado | 1 a 10 SM | US$408.80 a US$4,088.00 | OBL-ENC-04 | Aviso de privacidad publicado con historial de versiones |
| Leve | Omitir notificar una vulneracion (Art. 25) | 1 a 10 SM | US$408.80 a US$4,088.00 | OBL-INC-01 | Registro de incidente con hora de conocimiento y notificacion |
| Leve | Exigir pago por solicitudes que deben ser gratuitas | 1 a 10 SM | US$408.80 a US$4,088.00 | OBL-ARCO-07 | Tarifario publicado (si aplica) y registro de cobros |
| Grave | No implementar medidas/controles/lineamientos de la ACE | 11 a 25 SM | US$4,496.80 a US$10,220.00 | OBL-SEG-01 a 05 | Checklist de medidas tecnicas con evidencia adjunta |
| Grave | No cumplir medidas de seguridad de las Politicas de Actuacion | 11 a 25 SM | US$4,496.80 a US$10,220.00 | OBL-SEG-05, OBL-ENC-06, OBL-TRANSF-08 | Contratos de confidencialidad y transferencia vigentes |
| Grave | No atender solicitudes ARCO-POL en tiempo y forma | 11 a 25 SM | US$4,496.80 a US$10,220.00 | OBL-ARCO-04 | Bitacora de plazos con alertas automaticas |
| Grave | Crear bases con datos sensibles en contravencion de la ley (Art. 59 lit. a, remitido por Art. 56 lit. b num. 6) | 11 a 25 SM | US$4,496.80 a US$10,220.00 | OBL-SENS-01 | RAT con justificacion de base legal por categoria sensible |
| Muy grave | Tratar datos sin el consentimiento previo (Art. 26) | 26 a 40 SM | US$10,628.80 a US$16,352.00 | OBL-CONSENT-01, OBL-CONSENT-02 | Registro de consentimiento con medio, texto y fecha |
| Muy grave | Tratar datos pese a la revocacion del consentimiento | 26 a 40 SM | US$10,628.80 a US$16,352.00 | OBL-CONSENT-03 | Bitacora de revocaciones con corte automatico del tratamiento |
| Muy grave | No hacer efectiva la revocacion cuando proceda | 26 a 40 SM | US$10,628.80 a US$16,352.00 | OBL-CONSENT-03, OBL-CONSENT-04 | Contador de 5 dias habiles con alerta de vencimiento |
| Muy grave | Denegar solicitudes ARCO-POL en contravencion de la ley | 26 a 40 SM | US$10,628.80 a US$16,352.00 | OBL-ARCO-06 | Registro de causal de denegatoria tasada y motivacion |
| Muy grave | Uso de datos de NNA sin consentimiento parental | 26 a 40 SM | US$10,628.80 a US$16,352.00 | OBL-SENS-05 | Registro diferenciado de titular NNA con evidencia de consentimiento parental |
| Muy grave | Transferencia internacional a pais sin nivel de proteccion adecuado | 26 a 40 SM | US$10,628.80 a US$16,352.00 | OBL-TRANSF-02 | Evaluacion documentada del pais destino |
| Muy grave | Transferencia sin consentimiento del titular | 26 a 40 SM | US$10,628.80 a US$16,352.00 | OBL-TRANSF-01, OBL-TRANSF-03 | Registro de consentimiento especifico por transferencia |

Nota: el catalogo completo del Art. 56 tiene 9 infracciones leves, 7 graves y 10 muy graves; esta tabla resume las mas relevantes para el diseno del producto. Ademas, por remision del Art. 53 LPDP a la Ley de Ciberseguridad (Art. 27), existe una multa coercitiva de 1 a 10 salarios minimos por cada dia habil de incumplimiento de lo ordenado por la autoridad, cuya aplicabilidad directa a infracciones de la LPDP es una incertidumbre (ver seccion 9).

---

## 7. Listas resumen: OBLIGATORIO, RECOMENDADO, CONDICIONAL

Listas recalculadas en la ronda de relleno del 2026-09-24 (ver seccion 12, "Registro de cambios de la ronda de relleno", para el detalle de que cambio y por que). OBL-ARCO-10 a OBL-ARCO-14 en la lista CONDICIONAL corresponde, tras la renumeracion, a las causales tasadas de cancelacion, olvido, oposicion, limitacion, portabilidad y el reclamo del Art. 33 inc. 4 de los Lineamientos DPO (OBL-ARCO-14 es el nuevo ID del recurso ante la Direccion de Proteccion de Datos; no confundir con el ID OBL-ARCO-14 usado en la matriz para el mismo hecho, ver tabla de equivalencia seccion 11).

**OBLIGATORIO** (61 obligaciones - deben cumplirse siempre, sin condicion adicional):
OBL-AMBITO-01; OBL-PRIN-01 a OBL-PRIN-03 (3); OBL-PRIN-05; OBL-ARCO-01 a OBL-ARCO-02 (2); OBL-ARCO-04; OBL-ARCO-06 a OBL-ARCO-09 (4); OBL-ARCO-15 a OBL-ARCO-16 (2); OBL-DPO-01; OBL-DPO-04; OBL-DPO-08; OBL-AVISO-01 a OBL-AVISO-05 (5); OBL-CONSENT-01 a OBL-CONSENT-03 (3); OBL-SENS-01 a OBL-SENS-02 (2); OBL-SENS-06 a OBL-SENS-07 (2); OBL-ENC-01 a OBL-ENC-03 (3); OBL-ENC-06; OBL-TRANSF-01; OBL-TRANSF-03; OBL-TRANSF-05; OBL-TRANSF-07 a OBL-TRANSF-08 (2); OBL-SEG-01 a OBL-SEG-07 (7); OBL-DOC-01 a OBL-DOC-05 (5); OBL-INC-01 a OBL-INC-05 (5); OBL-CAP-02; OBL-SANC-01; OBL-SANC-04 a OBL-SANC-06 (3); OBL-RET-06.

**RECOMENDADO** (6 obligaciones - buena practica sin mandato legal expreso, o facultad sin deber correlativo):
OBL-CONSENT-06 (registrar base de licitud como diseno de producto); OBL-ENC-08 a OBL-ENC-09 (2) (instrucciones documentadas al encargado y devolucion/eliminacion de datos al finalizar la relacion, sin norma expresa); OBL-TRANSF-06 (solicitar opinion previa a la ACE, facultad no deber); OBL-AUD-01 (certificacion ACE, sin desarrollo aun); OBL-RET-07 (retencion de 5 anos por analogia con la prescripcion sancionadora, sin norma expresa de retencion del expediente).

**CONDICIONAL** (39 obligaciones - aplican solo bajo circunstancias especificas, indicadas en cada bloque):
OBL-AMBITO-02 a OBL-AMBITO-04 (3) (sujetos SSF, ambito domestico, seguridad publica/registros); OBL-PRIN-04 (titular NNA); OBL-ARCO-03 (incompetencia); OBL-ARCO-05 (hubo transferencia previa); OBL-ARCO-10 a OBL-ARCO-14 (5) (causales tasadas de cancelacion, olvido, oposicion, limitacion, portabilidad); OBL-ARCO-17 (reclamo del titular ante la Direccion de Proteccion de Datos); OBL-DPO-02 a OBL-DPO-03 (2); OBL-DPO-05 a OBL-DPO-07 (3); OBL-DPO-09 (reclasificadas de OBLIGATORIO a CONDICIONAL en esta ronda, ver seccion 12); OBL-CONSENT-04 a OBL-CONSENT-05 (2) (existe encargado; excepcion invocada); OBL-SENS-03 a OBL-SENS-05 (3) (excepciones de salud, sector salud, consentimiento parental NNA -- SENS-05 reclasificada en esta ronda); OBL-SENS-08 a OBL-SENS-09 (2) (biometria laboral y videovigilancia, nuevas de esta ronda); OBL-ENC-04 a OBL-ENC-05 (2) (datos de contacto del encargado en el aviso -- reclasificada en esta ronda -- y transferencia a otro responsable); OBL-ENC-07 (subcontratacion en cadena, nueva de esta ronda); OBL-TRANSF-02 (nivel de proteccion en transferencias internacionales -- reclasificada en esta ronda); OBL-TRANSF-04 (invocacion de tratado centroamericano); OBL-CAP-01 (plan anual de capacitacion -- reclasificada en esta ronda); OBL-SANC-02 a OBL-SANC-03 (2) (multas y medidas adicionales -- SANC-02 reclasificada en esta ronda); OBL-SANC-07 (remision del procedimiento a la Ley de Ciberseguridad -- reclasificada en esta ronda); OBL-RET-01 a OBL-RET-05 (5) (segun giro/sector del cliente: comerciante, contribuyente, sujeto LCLDA, salud).

Total de obligaciones catalogadas: 106 (94 de la version original mas 12 obligaciones nuevas agregadas en la ronda de relleno del 2026-09-24; ver seccion 12).

---

## 8. Contradicciones entre fuentes y ambiguedades de la ley

1. **Consentimiento como regla general vs. pluralidad de bases de licitud.** El Art. 5 lit. c ("principio de consentimiento y finalidad") y el Art. 27 inc. 1 ("sera necesaria la obtencion del consentimiento") leen como si el consentimiento fuera la regla general, mientras que el Art. 5 lit. g reconoce seis bases de licitud alternativas (contrato, obligacion legal, intereses vitales, interes publico, interes legitimo, ademas del consentimiento) y el Art. 28 anade ocho excepciones adicionales al consentimiento. La ACE no ha emitido guia que resuelva esta tension. Diseno recomendado: el software debe permitir registrar cualquiera de las seis bases sin bloquear el flujo, dejando expresamente a criterio de la empresa (con nota de riesgo) la decision de si usar una base distinta del consentimiento es defendible para cada tratamiento.

2. **Alcance indeterminado de las medidas de las Politicas ACE.** Las Politicas de Actuacion enumeran controles obligatorios (RAT, EIPD, auditorias, 2FA, cifrado, etc.) sin fijar formato, contenido minimo, ni umbral de riesgo que dispare cada uno. El software debe proponer un estandar razonable y documentarlo explicitamente como "criterio propio del producto, no un formato oficial de la ACE", para no inducir al cliente a creer que existe un formato legal unico.

3. **Registro de bancos de datos del Art. 45.** El Art. 45 inciso 2 exige poner en conocimiento de la ACE "el registro de banco de datos" en todo flujo transfronterizo, pero la ACE no ha creado ningun registro general de bases de datos ni ha habilitado ningun canal o formulario para cumplir esta obligacion. Existe una obligacion legal sin medio practico de cumplimiento; el software debe registrar internamente el intento de cumplimiento (o su imposibilidad) como evidencia de buena fe.

4. **Aviso con nombre del delegado tras la reforma.** El Art. 24 lit. h exige incluir en el aviso de privacidad los datos de contacto del "encargado del tratamiento" subcontratado; los formularios y practicas actuales tambien asocian el aviso a los datos del delegado. Si la reforma de septiembre de 2026 entra en vigencia y elimina la obligatoriedad del delegado en el sector privado, no esta claro si el aviso debera seguir mencionando a una persona de contacto interna (el "sujeto obligado") en lugar del delegado, ni si los avisos ya publicados con datos del delegado quedaran desactualizados de forma automatica. El producto debe anticipar un flujo de "actualizacion masiva de avisos" activable cuando el estado FUTURO de la reforma (seccion 3) se confirme.

5. **Atribucion de actos procedimentales: "el delegado" vs. "el responsable".** El texto vigente de los Arts. 18 (prevencion), 19 (incompetencia), 21 (notificacion a receptores) y 30 (revocacion) atribuye literalmente los actos al "delegado", no al "responsable" en terminos generales. Esto es coherente mientras el delegado sea obligatorio, pero genera una ambiguedad de diseno: el software debe modelar un rol "responsable del tramite ARCO-POL" configurable, que hoy se asigna por defecto al delegado y que, tras la reforma, deberia poder asignarse a cualquier persona interna designada como "sujeto obligado".

6. **Divergencia en el catalogo de datos sensibles.** El Art. 4 lit. g (definicion general) y el Art. 59 lit. b (prohibiciones) no listan exactamente las mismas categorias: el Art. 59 lit. b incluye "nacionalidad" y "convicciones filosoficas", ausentes del Art. 4 lit. g. El software debe usar el catalogo mas amplio (union de ambos listados) para no subestimar el alcance de "dato sensible".

7. **Numero exacto del decreto de reforma de septiembre de 2026.** La mayoria de los sweeps usa "Decreto 659" siguiendo la nota oficial de la Asamblea y prensa convergente, pero la verificacion mas cautelosa (sweep de encargados_transferencias) documenta que, al 2026-09-24, el listado oficial de decretos de la Asamblea no llegaba a ese numero y que busquedas web devolvieron numeros distintos (659 y 660) para la misma reforma. Este documento usa "659" por ser la referencia mas repetida, pero el numero debe confirmarse contra el texto que efectivamente publique el Diario Oficial.

---

## 9. Incertidumbres y preguntas que requieren abogado

1. Computo de las 72 horas del Art. 25 (vulneraciones): ¿corridas u horas habiles? Argumento en ambos sentidos usando la LPA (Art. 82) como supletoria; sin resolucion de la ACE ni doctrina local conocida.
2. ¿Es aplicable el Art. 82 LPA (computo de plazos en dias/horas habiles) a la relacion titular-empresa privada, dado que el Art. 2 LPA limita expresamente su ambito subjetivo a la Administracion Publica? El Art. 62 LPDP remite a la LPA "en todo lo no previsto", pero esa remision podria no extender el ambito subjetivo de la LPA misma.
3. ¿Debe tratarse el sabado como dia inhabil para los plazos de la LPDP frente a una empresa privada? No hay norma expresa que lo declare inhabil para el sector privado (el Codigo de Trabajo trata el sabado como laborable en principio).
4. Texto oficial completo del Decreto Legislativo de reforma de septiembre de 2026: no localizado en ninguna fuente primaria al 2026-09-24. Todo el contenido articulo por articulo (Arts. 15-17, 16, 47, 51) depende de fuentes secundarias.
5. Fecha exacta y numero de Diario Oficial de publicacion de las Politicas de Actuacion ACE N. 001-0309025-DPDP: no confirmada en fuente primaria, solo por prensa (2 y 3 de septiembre de 2025).
6. Aplicabilidad de la multa coercitiva del Art. 27 de la Ley de Ciberseguridad (1 a 10 salarios minimos por dia habil de incumplimiento) a infracciones de la LPDP por la remision del Art. 53: no mencionada expresamente en la Normativa PAS de la ACE.
7. ¿Cada nueva disposicion de la ACE (politica, lineamiento) reabre el plazo de 3 meses de adecuacion del Art. 60 inc. 2 para los sujetos obligados? No es expreso en el texto.
8. Edad de consentimiento digital de ninas, ninos y adolescentes: la LPDP remite al "ejercicio progresivo de facultades" sin edad numerica; existe tension con el Art. 77 de la Ley Crecer Juntos (adolescentes de 12 a 18 anos pueden consentir solos publicaciones de imagen con fines comerciales) frente al Art. 56 lit. c num. 3 LPDP (exige consentimiento parental para el uso de datos de NNA en general). Requiere criterio de abogado sobre como coordinar ambas normas.
9. Ambito territorial de la LPDP: el Art. 2 no fija un criterio territorial expreso; las Politicas ACE extienden la aplicacion a "operaciones internacionales vinculadas a ciudadanos salvadorenos", pero una politica administrativa no puede ampliar el ambito de una ley segun el Art. 161 LPA. Aplicacion a empresas extranjeras sin presencia local: sin resolver.
10. Si un encargado ubicado fuera de El Salvador (nube, SaaS) debe tratarse como "transferencia" (Art. 4 lit. u, que excluye al encargado de esa definicion) o como "flujo transfronterizo" sujeto a los Arts. 44 y 45 (cuyas definiciones de emisor/receptor, Art. 4 lit. k y o, si incluyen al encargado). El sweep recomienda la lectura conservadora (tratarlo como flujo transfronterizo), pero requiere confirmacion de abogado.
11. Quien esta facultado para declarar que un pais tiene "nivel de proteccion adecuado" bajo el Art. 44: la ley no lo atribuye a ningun organo y la ACE no ha publicado lista ni criterios.
12. Mecanismo, plazo, forma y contenido exacto para "poner en conocimiento" de la ACE el flujo transfronterizo del Art. 45 inciso 2, y consecuencia sancionatoria de omitirlo (no tipificada de forma especifica en el Art. 56).
13. Numero exacto del decreto legislativo de la reforma de septiembre de 2026 ("659" vs otras cifras reportadas en busquedas): no confirmado en fuente primaria.
14. Destino de los Lineamientos para el Delegado y de la medida "Delegado" de las Politicas ACE para el sector privado si la reforma entra en vigencia: no hay derogacion formal conocida de esos instrumentos.
15. Plazo especifico de conservacion documental para entidades supervisadas por la SSF (Ley de Bancos, NRP-23) y para planillas previsionales bajo la Ley Integral del Sistema de Pensiones: no localizado en los textos revisados.
16. Si la prevencion del Art. 18 suspende el plazo de 20 dias habiles del Art. 20, por aplicacion analogica del Art. 90.1 LPA: no resuelto expresamente.

Las afirmaciones marcadas NO_VERIFICABLE en el JSON de verificacion (por ejemplo, la exhaustividad de que el Decreto 659 es la unica reforma a la LPDP entre 2024 y 2026, o la ausencia de plazo de conservacion en la Ley de Bancos) se citan aqui unicamente como incertidumbres, nunca como hechos confirmados.

---

## 10. Fuentes consultadas

**Fuentes primarias (corpus local, C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\):** ace_decreto_144.txt; diario_oficial_2024-11-15_mh.txt; asamblea_decreto_143_ciberseguridad.txt; asamblea_decreto_856_lpa.txt; ace_politicas_protecciondatos.txt; lineamientos_dpo_OCR.txt (y ocr/lineamientos_dpo/page-01 a 11.png); normativa_sancionadora_OCR.txt (y ocr/normativa_sancionadora/page-01 a 09.png); asamblea_decreto_523_reforma_lpa.txt; ace_form_acceso.txt, ace_form_cancelacion.txt, ace_form_portabilidad.txt, ace_form_nombramiento_delegado.txt y demas formularios ACE version 07-07-2025.

**Fuentes primarias en linea (verificadas por WebFetch/WebSearch en las rondas de verificacion, 2026-09-23 y 2026-09-24):** asamblea.gob.sv/leyes-y-decretos/view/7022; asamblea.gob.sv/node/14116; asamblea.gob.sv/node/13592 y /13595; asamblea.gob.sv/leyes-y-decretos/decretos-por-anios/2025/0 y /2026/0; ace.gob.sv/page/formularios; ace.gob.sv/politicas.php; ace.gob.sv/contacto; jurisprudencia.gob.sv (Decreto Ejecutivo 11/2025 MTPS, Ley de Comercio Electronico, Ley Especial contra los Delitos Informaticos); ssf.gob.sv (LCLDA, Ley Integral del Sistema de Pensiones); uif.gob.sv (Instructivo Acuerdo 380); asp.salud.gob.sv (Norma Tecnica del Expediente Clinico); factura.gob.sv (Ley de Firma Electronica); defensoria.gob.sv (Ley de Proteccion al Consumidor); crecerjuntos.gob.sv (Ley Crecer Juntos); oas.org/dil/esp/codigo_civil_el_salvador.pdf; diariooficial.gob.sv; imprentanacional.gob.sv.

**Fuentes secundarias (prensa y firmas legales, usadas solo para orientacion y marcadas como tales en el texto):** diario.elmundo.sv; eldiariodehoy.com; elsalvador.com; infobae.com; consortiumlegal.com; mtps.gob.sv (nota sobre asueto del 17 de junio); ecija.com, blplegal.com y central-law.com (busqueda web complementaria del 2026-09-24 sobre subencargados e instrucciones documentadas del encargado, sin cita a articulo especifico, ver OBL-ENC-07/08/09 en la seccion 4.8).

Fecha de consulta base: 2026-09-23. Reverificaciones puntuales: 2026-09-24 (senaladas explicitamente en el texto donde corresponde).

---

## 11. Tabla de equivalencia de IDs (03_hallazgos_regulatorios.md <-> matriz_obligaciones)

Esta tabla resuelve la inconsistencia detectada por el critico de completitud: los dos documentos usan esquemas de ID distintos (hallazgos: OBL-AMBITO, OBL-CONSENT, OBL-ENC; matriz: OBL-AMB, OBL-CONS, OBL-PROV) y renumeran cada obligacion dentro de su area en orden propio. Un modulo del software que reciba un ID de cualquiera de los dos documentos debe consultar esta tabla para encontrar su contraparte, o para confirmar que ese ID no tiene contraparte (marcado "sin equivalente" con la razon).

Reglas de lectura:
- "=" significa el mismo hecho juridico, mismo alcance.
- "fusiona con" significa que un documento junta en un solo ID lo que el otro documento separa en varios; el ID que aparece a la derecha del signo queda absorbido dentro del ID principal.
- "area distinta" significa que el mismo Articulo aparece catalogado bajo una familia de area diferente en cada documento (por ejemplo ENC en hallazgos y AVISO o TRANSF en matriz).
- "nueva de esta ronda" senala los IDs agregados en la ronda de relleno del 2026-09-24 (ver seccion 12) para cerrar una asimetria detectada al construir esta tabla.
- "sin equivalente" significa que, tras la verificacion, ese ID no tiene contraparte catalogada en el otro documento; se indica la razon y si se considero de bajo riesgo dejarlo asi (por diseno o por alcance fuera de foco) en lugar de forzar una obligacion nueva sin base clara.

### 11.1 AMBITO / AMB (igual numeracion)

| hallazgos | matriz | Articulo |
|---|---|---|
| OBL-AMBITO-01 | OBL-AMB-01 | Art. 2 |
| OBL-AMBITO-02 | OBL-AMB-02 | Art. 3 lit. a) |
| OBL-AMBITO-03 | OBL-AMB-03 | Art. 3 lit. b) |
| OBL-AMBITO-04 | OBL-AMB-04 | Art. 3 lit. c) y d) |

### 11.2 PRIN / PRIN / TRAT

| hallazgos | matriz | Articulo | Nota |
|---|---|---|---|
| OBL-PRIN-01 | OBL-PRIN-02 | Art. 5 lit. g) | numeracion invertida entre documentos |
| OBL-PRIN-02 | OBL-PRIN-01 | Art. 5 lit. c) | numeracion invertida entre documentos |
| OBL-PRIN-03 | OBL-PRIN-03 | Art. 5 lit. i) | = |
| OBL-PRIN-04 | OBL-PRIN-04 | Art. 5 lit. j) | = |
| OBL-PRIN-05 | OBL-TRAT-01 | Art. 32 | area distinta (matriz: TRAT); PRIN-05 nueva de esta ronda |

### 11.3 ARCO / ARCO

| hallazgos | matriz | Articulo | Nota |
|---|---|---|---|
| OBL-ARCO-01 + OBL-ARCO-02 | OBL-ARCO-08 | Art. 18 | matriz fusiona contenido de la solicitud y prevencion en un solo ID |
| OBL-ARCO-03 | OBL-ARCO-09 | Art. 19 | = |
| OBL-ARCO-04 | OBL-ARCO-10 | Art. 20 | = |
| OBL-ARCO-05 | OBL-ARCO-11 | Art. 21 inc. 3 | = |
| OBL-ARCO-06 | OBL-ARCO-12 | Art. 22 | = |
| OBL-ARCO-07 | OBL-ARCO-13 | Art. 23 | = |
| OBL-ARCO-08 | OBL-ARCO-02 | Art. 8 | = |
| OBL-ARCO-09 | OBL-ARCO-03 | Art. 9 | = |
| OBL-ARCO-10 + OBL-ARCO-11 | OBL-ARCO-04 | Art. 10 | matriz fusiona cancelacion (incisos 1-2) y olvido (inciso final) en un solo ID |
| OBL-ARCO-12 | OBL-ARCO-05 | Art. 12 | = |
| OBL-ARCO-13 | OBL-ARCO-06 | Art. 13 | = |
| OBL-ARCO-14 | OBL-ARCO-07 | Art. 14 | = |
| OBL-ARCO-15 | OBL-ARCO-01 | Art. 6 | = |
| OBL-ARCO-16 | OBL-ARCO-15 | Art. 32 (Lineamientos DPO) | ARCO-15 nueva de esta ronda en matriz |
| OBL-ARCO-17 | OBL-ARCO-14 | Art. 33 inc. 4 (Lineamientos DPO) | ambos IDs nuevos de esta ronda; no confundir OBL-ARCO-14 de hallazgos (Art. 14 LPDP, portabilidad) con OBL-ARCO-14 de matriz (Art. 33 inc. 4 Lineamientos, recurso) |

### 11.4 DPO / DPO

| hallazgos | matriz | Articulo | Nota |
|---|---|---|---|
| OBL-DPO-01 | OBL-DPO-01 | Arts. 15 y 17 | = |
| OBL-DPO-02 | OBL-DPO-03 | Art. 10 | reclasificada a CONDICIONAL en hallazgos esta ronda, ver seccion 12 |
| OBL-DPO-03 | OBL-DPO-02 | Art. 8 | reclasificada a CONDICIONAL en hallazgos esta ronda |
| OBL-DPO-04 | incluida en OBL-DPO-03 | Art. 10 inciso final | matriz funde esta regla dentro del mismo ID que la comunicacion a la ACE |
| OBL-DPO-05 | OBL-DPO-04 | Art. 18 | reclasificada a CONDICIONAL en hallazgos esta ronda |
| OBL-DPO-06 | OBL-DPO-05 | Art. 22 | reclasificada a CONDICIONAL en hallazgos esta ronda |
| OBL-DPO-07 | OBL-DPO-06 | Art. 36 | reclasificada a CONDICIONAL en hallazgos esta ronda |
| OBL-DPO-08 | OBL-DPO-08 | Art. 17 | OBL-DPO-08 nueva de esta ronda en matriz |
| OBL-DPO-09 | OBL-DPO-07 | Art. 30 | OBL-DPO-09 nueva de esta ronda en hallazgos |

### 11.5 AVISO / AVISO / RET

| hallazgos | matriz | Articulo | Nota |
|---|---|---|---|
| OBL-AVISO-01 | OBL-AVISO-05 | Art. 24 inc. 1 | numeracion distinta |
| OBL-AVISO-02 | OBL-AVISO-01 | Art. 24 lit. a-i) | numeracion distinta; el literal h) tambien se cataloga por separado como OBL-ENC-04/OBL-AVISO-02(matriz), y el literal i) (cookies) solo existe como ID propio en matriz (OBL-AVISO-03), incluido sin ID separado dentro de este bloque en hallazgos |
| OBL-AVISO-03 | sin equivalente | Art. 24 inciso final | matriz no separa esta subregla en un ID propio; queda implicita en OBL-AVISO-01(matriz) |
| OBL-AVISO-04 | OBL-RET-04 | Art. 31 (Lineamientos DPO) | area distinta (matriz: RET) |
| OBL-AVISO-05 | OBL-AVISO-04 | Art. 7 | OBL-AVISO-05 nueva de esta ronda en hallazgos |

### 11.6 CONSENT / CONS / TRAT

| hallazgos | matriz | Articulo | Nota |
|---|---|---|---|
| OBL-CONSENT-01 | OBL-CONS-01 | Arts. 26 y 27 | = |
| OBL-CONSENT-02 | OBL-CONS-04 | Art. 26 inc. 4 | = |
| OBL-CONSENT-03 | OBL-CONS-02 + OBL-CONS-03 | Arts. 29 y 30 | matriz separa Art. 29 (CONS-02) de Art. 30 (CONS-03); ver tambien CONSENT-04 |
| OBL-CONSENT-04 | incluida en OBL-CONS-03 | Art. 30 | matriz funde el deber de informar al encargado dentro del mismo ID que el plazo de revocacion |
| OBL-CONSENT-05 | OBL-TRAT-02 | Art. 28 | area distinta (matriz: TRAT) |
| OBL-CONSENT-06 | sin equivalente | Art. 5 lit. i (diseno propio) | recomendacion de diseno del sweep, no una obligacion legal catalogable; matriz no la reproduce por ese motivo |

### 11.7 SENS / SENS / CONS

| hallazgos | matriz | Articulo | Nota |
|---|---|---|---|
| sin equivalente | OBL-SENS-01 | Art. 4 lit. g) (definicion general) | matriz cataloga la definicion como obligacion propia; hallazgos trata las definiciones del Art. 4 como contexto transversal, no como obligacion catalogada |
| OBL-SENS-01 | incluida en OBL-SENS-05 | Art. 59 lit. a) | matriz funde toda la prohibicion del Art. 59 en un solo ID |
| OBL-SENS-02 | OBL-SENS-02 | Art. 37 inc. 1 | = |
| OBL-SENS-03 | OBL-SENS-03 | Art. 37 inc. 2-3 y 38 inc. 1 | = |
| OBL-SENS-04 | OBL-SENS-04 | Art. 39 | = |
| OBL-SENS-05 | OBL-CONS-06 | Art. 56 lit. c num. 3 | area distinta (matriz: CONS); reclasificada a CONDICIONAL en hallazgos esta ronda |
| OBL-SENS-06 | citado solo como referencia dentro de OBL-CONS-06 | Art. 42 | matriz no desarrolla el contenido propio del Art. 42 (informar a NNA en lenguaje adaptado), solo lo cita como articulo relacionado |
| OBL-SENS-07 | OBL-SENS-06 | Art. 4 lit. g) (biometria) | ambos nuevos de esta ronda |
| OBL-SENS-08 | OBL-SENS-07 | Art. 26 inc. 4 y Art. 37 (biometria) | ambos nuevos de esta ronda |
| OBL-SENS-09 | OBL-SENS-08 | Arts. 4, 7, 12, 16 (videovigilancia) | ambos nuevos de esta ronda |

### 11.8 ENC / PROV / AVISO / TRANSF / SEG

| hallazgos | matriz | Articulo | Nota |
|---|---|---|---|
| OBL-ENC-01 | OBL-PROV-01 | Art. 33 inc. 2 | = |
| OBL-ENC-02 | OBL-PROV-02 | Art. 34 | = |
| OBL-ENC-03 | OBL-PROV-03 | Art. 36 | = |
| OBL-ENC-04 | OBL-AVISO-02 | Art. 24 lit. h) | area distinta (matriz: AVISO); reclasificada a CONDICIONAL en hallazgos esta ronda |
| OBL-ENC-05 | OBL-TRANSF-02 | Art. 41 | area distinta (matriz: TRANSF) |
| OBL-ENC-06 | incluida en OBL-SEG-04 | Art. 4, Medidas de Seguridad en Transferencias, lit. b) | area distinta (matriz: SEG), fusionada con el resto del bloque de transferencias |
| OBL-ENC-07 | OBL-PROV-05 | Art. 33 inc. 2 (lectura extensiva, subencargados) | ambos nuevos de esta ronda |
| OBL-ENC-08 | OBL-PROV-06 | Art. 34 / Art. 5 lit. i) (instrucciones documentadas) | ambos nuevos de esta ronda |
| OBL-ENC-09 | OBL-PROV-07 | Art. 34 / Art. 5 lit. h) (devolucion/eliminacion) | ambos nuevos de esta ronda |
| sin equivalente | OBL-PROV-04 | Art. 56 lit. a num. 2 | matriz cataloga la infraccion leve como obligacion propia; hallazgos la deja solo en la tabla de infracciones (seccion 6), ligada a OBL-ENC-04 |

### 11.9 TRANSF / TRANSF / SEG

| hallazgos | matriz | Articulo | Nota |
|---|---|---|---|
| OBL-TRANSF-01 | OBL-TRANSF-01 | Art. 40 | = |
| OBL-TRANSF-02 | OBL-TRANSF-03 | Art. 44 inc. 1 | reclasificada a CONDICIONAL en hallazgos esta ronda |
| OBL-TRANSF-03 + OBL-TRANSF-04 | OBL-TRANSF-04 | Art. 44 inciso final / inc. 4 | matriz funde la excepcion centroamericana dentro del mismo ID que el consentimiento previo |
| OBL-TRANSF-05 + OBL-TRANSF-06 | OBL-TRANSF-05 | Art. 45 | matriz funde la puesta en conocimiento obligatoria y la opinion previa opcional en un solo ID |
| OBL-TRANSF-07 | OBL-TRANSF-06 | Art. 54 inc. 2 | = |
| OBL-TRANSF-08 | incluida en OBL-SEG-04 | Art. 4, Medidas de Seguridad en Transferencias | area distinta (matriz: SEG) |

### 11.10 SEG / SEG / DOC

| hallazgos | matriz | Articulo | Nota |
|---|---|---|---|
| OBL-SEG-01 | OBL-SEG-02 | Art. 4, Medidas Organizativas | = |
| OBL-SEG-02 + OBL-SEG-03 + OBL-SEG-04 | OBL-SEG-03 | Art. 4, Medidas Tecnicas | matriz funde control de acceso, cifrado/backups/firewall/pentest y digitalizacion en un solo ID |
| OBL-SEG-05 | OBL-SEG-06 | Art. 56 lit. b num. 5 y 7 | ambos nuevos de esta ronda (SEG-06 en matriz) |
| OBL-SEG-06 | OBL-SEG-05 | Art. 4, Medidas Fisicas lit. e) (eliminacion segura) | ambos nuevos de esta ronda |
| OBL-SEG-07 | OBL-SEG-01 | Art. 35 | SEG-07 nueva de esta ronda en hallazgos |

### 11.11 DOC / DOC / SEG / AUD

| hallazgos | matriz | Articulo | Nota |
|---|---|---|---|
| OBL-DOC-01 | OBL-DOC-02 | Art. 4, Medidas Organizativas lit. d) (RAT) | = |
| OBL-DOC-02 | OBL-DOC-03 | Art. 4, Medidas Organizativas lit. e) (EIPD) | = |
| OBL-DOC-03 | OBL-DOC-01 | Art. 33 inc. 1 | = |
| OBL-DOC-04 | incluida en OBL-SEG-02 | Art. 4, Medidas Organizativas lit. a) | area distinta (matriz: SEG), fusionada con las seis medidas organizativas |
| OBL-DOC-05 | OBL-AUD-01 | Art. 8 lit. b) | area distinta (matriz: AUD) |
| sin equivalente | OBL-DOC-04 | Art. 61 inc. 2 | matriz cataloga el plazo transitorio como obligacion propia; hallazgos lo trata solo como hecho de linea de tiempo (secciones 2 y 5), no como OBL catalogada |

### 11.12 INC / INC

| hallazgos | matriz | Articulo | Nota |
|---|---|---|---|
| OBL-INC-01 | OBL-INC-01 | Art. 25, primer inciso | = |
| OBL-INC-02 + OBL-INC-03 | OBL-INC-03 | Art. 25, incisos 3-4 | matriz funde contenido de la notificacion a la ACE y a titulares en un solo ID |
| OBL-INC-04 | OBL-INC-02 | Art. 25, segundo inciso | = |
| OBL-INC-05 | OBL-INC-04 | Art. 25, ultimo inciso | = |
| sin equivalente | OBL-INC-05 | Art. 6 lit. f-g Ley de Ciberseguridad | norma distinta a la LPDP (Ley de Ciberseguridad), aplica solo a operadores de infraestructura critica; fuera del foco central de hallazgos, que se concentra en la LPDP y sus normas ACE conexas |

### 11.13 CAP / CAP, AUD / AUD

| hallazgos | matriz | Articulo | Nota |
|---|---|---|---|
| OBL-CAP-01 | OBL-CAP-02 | Art. 22 (Lineamientos DPO) | numeracion distinta; reclasificada a CONDICIONAL en hallazgos esta ronda |
| OBL-CAP-02 | OBL-CAP-01 | Art. 4, Medidas Organizativas lit. c) | numeracion distinta |
| OBL-AUD-01 | OBL-AUD-02 | Art. 50 lit. j, k, l | AUD-02 nueva de esta ronda en matriz |

### 11.14 SANC / SANC / SENS / CONS

| hallazgos | matriz | Articulo | Nota |
|---|---|---|---|
| OBL-SANC-01 | OBL-SANC-01 | Art. 56 | = |
| OBL-SANC-02 | OBL-SANC-02 | Art. 57 | reclasificada a CONDICIONAL en hallazgos esta ronda |
| OBL-SANC-03 | OBL-SANC-03 | Art. 58 | = |
| OBL-SANC-04 | incluida en OBL-SENS-05 | Art. 59 | area distinta (matriz: SENS) |
| OBL-SANC-05 | OBL-CONS-05 | Art. 54 inc. 1 | area distinta (matriz: CONS) |
| OBL-SANC-06 | sin equivalente | Art. 50 lit. t) | no se localizo articulo equivalente catalogado en matriz; facultad de la ACE de requerir informacion, de bajo riesgo de omision practica |
| OBL-SANC-07 | OBL-SANC-04 | Art. 53 | reclasificada a CONDICIONAL en hallazgos esta ronda |
| sin equivalente | OBL-SANC-05 | Art. 21 (Normativa PAS) | procedimiento sancionador; hallazgos solo lo documenta en la tabla de plazos (seccion 5), no como OBL catalogada |
| sin equivalente | OBL-SANC-06 | Art. 44 (Normativa PAS) | idem, solo en tabla de plazos (seccion 5) |
| sin equivalente | OBL-SANC-08 | Art. 55 | publicidad de resoluciones; mencionada en el marco normativo (seccion 1) pero no catalogada en hallazgos |
| sin equivalente | OBL-SANC-09 | Art. 9 inc. 3 y Art. 31 | derecho de denuncia del titular ante la ACE; no localizado como ID propio en hallazgos |

Nota de correccion adicional: en la tabla resumen de `matriz_obligaciones.md` (seccion "Tabla resumen", area SANC), las filas de OBL-SANC-05 y OBL-SANC-06 citaban solo "Art. 21" y "Art. 44" sin indicar la norma. Se corrigio en esta ronda para que ambas filas digan explicitamente "(Normativa PAS)", evitando que se lean como el Art. 21 o el Art. 44 de la LPDP (que tienen contenido distinto: notificacion a receptores tras rectificacion, y transferencias internacionales, respectivamente).

### 11.15 RET / RET / AVISO

| hallazgos | matriz | Articulo | Nota |
|---|---|---|---|
| OBL-RET-01 | OBL-RET-01 | Arts. 451 y 454 (Codigo de Comercio) | = |
| OBL-RET-02 | OBL-RET-02 | Art. 147 (Codigo Tributario) | = |
| OBL-RET-03 | OBL-RET-03 | Arts. 10 lit. b y 12 (LCLDA) | = |
| OBL-RET-04 | sin equivalente | Art. 59 (Instructivo UIF) | refuerza OBL-RET-03 con una fuente reglamentaria adicional del mismo alcance (sujetos LCLDA); matriz no la cataloga por separado |
| OBL-RET-05 | sin equivalente | Art. 34 (Norma Tecnica del Expediente Clinico) | especifica del sector salud; matriz no la cataloga por separado |
| OBL-RET-06 | OBL-RET-06 | Art. 13-A (Ley de Firma Electronica) | ambos nuevos de esta ronda (RET-06 en matriz) |
| OBL-RET-07 | OBL-RET-05 | Art. 47 (Normativa PAS) | numeracion distinta |
| OBL-AVISO-04 | OBL-RET-04 | Art. 31 (Lineamientos DPO) | ver seccion 11.5; area distinta |

### 11.16 PLAZO (area exclusiva de matriz, sin contraparte catalogada en hallazgos)

matriz cataloga cinco obligaciones bajo el area PLAZO (OBL-PLAZO-01 a 05: Art. 82 LPA sobre computo de plazos, Art. 190 Codigo de Trabajo sobre dias inhabiles, Art. 60 inc. 2 y Art. 61 inc. 2 sobre plazos transitorios vencidos, y el seguimiento de la reforma 659). Esta es una diferencia estructural deliberada y no un error: hallazgos trata estos mismos hechos de forma narrativa en la seccion 2 (linea de tiempo), la seccion 3 (la reforma de septiembre de 2026) y la tabla de plazos de la seccion 5, en lugar de convertirlos en obligaciones catalogadas independientes con bloque Norma/Articulo/Clasificacion. No se fuerza su conversion a IDs OBL- en esta ronda porque duplicarian contenido ya cubierto en esas secciones sin agregar un hecho juridico nuevo.

### 11.17 Conciliacion del conteo total

| Documento | Total antes de esta ronda | Nuevas agregadas | Total despues de esta ronda |
|---|---|---|---|
| 03_hallazgos_regulatorios.md | 94 | 12 (OBL-PRIN-05, OBL-ARCO-17, OBL-DPO-09, OBL-AVISO-05, OBL-SENS-07/08/09, OBL-ENC-07/08/09, OBL-SEG-06/07) | 106 |
| matriz_obligaciones (.json y .md) | 92 | 13 (OBL-SENS-06/07/08, OBL-PROV-05/06/07, OBL-ARCO-14/15, OBL-SEG-05/06, OBL-DPO-08, OBL-AUD-02, OBL-RET-06) | 105 |

La diferencia final de 1 (106 vs. 105) no es un error de conciliacion: queda documentada obligacion por obligacion en las secciones 11.1 a 11.16 anteriores. Se compone de un remanente de items con contraparte deliberadamente no catalogada en el otro documento (por ejemplo, las 5 obligaciones del area PLAZO exclusivas de matriz, las 4 obligaciones del procedimiento sancionador exclusivas de matriz -- SANC-05, SANC-06, SANC-08, SANC-09 --, y OBL-INC-05 de matriz por pertenecer a la Ley de Ciberseguridad; frente a OBL-RET-04, OBL-RET-05 y OBL-SANC-06 exclusivas de hallazgos, y OBL-CONSENT-06 sin equivalente por ser una recomendacion de diseno). Antes de esta ronda la brecha real era mayor (94 vs. 92, con 26 obligaciones OBLIGATORIO de diferencia) porque, ademas de esta asimetria estructural, existia un patron de reclasificacion no explicado en 7 pares de IDs (ver seccion 12); ese patron quedo corregido en esta ronda.

---

## 12. Registro de cambios de la ronda de relleno (2026-09-24)

Ronda ejecutada en respuesta a los gaps e inconsistencias reportados por el critico de completitud sobre este documento y sobre `matriz_obligaciones.json`/`.md`. No se borro contenido verificado existente; todos los cambios fueron adiciones o correcciones de clasificacion con nota explicita.

### 12.1 Gaps cerrados (contenido nuevo agregado)

1. **Biometria (prioridad alta).** Se agregaron OBL-SENS-07, OBL-SENS-08 y OBL-SENS-09 en la seccion 4.7, convirtiendo en obligaciones catalogadas el contenido que ya existia en `sweep_consentimiento_bases_sensibles.md` (seccion 4.5) sobre biometria de asistencia, videovigilancia y reconocimiento facial, incluida la confirmacion de que no existe lineamiento especifico de la ACE sobre esta materia al 2026-09-23. Se agregaron las mismas tres obligaciones a la matriz como OBL-SENS-06, OBL-SENS-07 y OBL-SENS-08.
2. **Consistencia estructural de IDs (prioridad alta).** Se agrego la seccion 11 completa (tabla de equivalencia de IDs hallazgos <-> matriz, area por area) y la conciliacion explicita del conteo total (seccion 11.17).
3. **Encargados y subencargados (prioridad media).** Se agregaron OBL-ENC-07 (subcontratacion en cadena), OBL-ENC-08 (instrucciones documentadas) y OBL-ENC-09 (devolucion/eliminacion de datos al finalizar la relacion) en la seccion 4.8, dejando explicito que la LPDP y la normativa ACE no regulan expresamente estos tres puntos (se investigo en el corpus local y en fuentes secundarias -- ECIJA, BLP, Central Law, 2026-09-24 -- sin encontrar articulo especifico), por lo que se catalogaron como CONDICIONAL (subencargados, por interpretacion extensiva del Art. 33 inc. 2) y RECOMENDADO (instrucciones y devolucion/eliminacion, buena practica sin mandato expreso). Se agregaron las mismas tres obligaciones a la matriz como OBL-PROV-05, OBL-PROV-06 y OBL-PROV-07.
4. **Recurso en el ciclo ARCO-POL (prioridad media).** Se agrego OBL-ARCO-17 en la seccion 4.3, catalogando el reclamo del titular ante la Direccion de Proteccion de Datos de la ACE contra una resolucion del delegado (Lineamientos DPO Art. 33 inc. 4, 10 dias habiles), que antes solo aparecia en la tabla de plazos de la seccion 5. Se agrego la misma obligacion a la matriz como OBL-ARCO-14.
5. **Eliminacion segura (prioridad baja).** Se agrego OBL-SEG-06 en la seccion 4.10, catalogando el control de "Eliminacion Segura de Documentos" de las Politicas ACE (Art. 4, Medidas Fisicas lit. e: trituradoras de papel y borrado seguro de dispositivos electronicos). Se agrego la misma obligacion a la matriz como OBL-SEG-05.

### 12.2 Simetrias adicionales cerradas (detectadas al construir la tabla de equivalencia, no reportadas por el critico)

Al construir la tabla de la seccion 11 se detectaron 7 obligaciones que existian en un documento pero no en el otro, sin ser parte de los gaps reportados. Se cerraron por ser de alcance general y bajo costo de documentar en ambos lados:

6. OBL-PRIN-05 (hallazgos, Art. 32 LPDP, prohibicion de desviacion de finalidad) agregada para igualar a OBL-TRAT-01 de matriz, que no tenia contraparte en hallazgos.
7. OBL-DPO-09 (hallazgos, Art. 30 Lineamientos DPO, informe periodico del delegado al responsable) agregada para igualar a OBL-DPO-07 de matriz, que no tenia contraparte en hallazgos.
8. OBL-AVISO-05 (hallazgos, Art. 7 LPDP, derecho de informacion en la recoleccion) agregada para igualar a OBL-AVISO-04 de matriz, que no tenia contraparte en hallazgos.
9. OBL-SEG-07 (hallazgos, Art. 35 LPDP, caracter imperativo de las Politicas ACE) agregada para igualar a OBL-SEG-01 de matriz, que no tenia contraparte en hallazgos.
10. OBL-DPO-08 (matriz, Art. 17 LPDP, deber de asistencia al delegado) agregada para igualar a OBL-DPO-08 de hallazgos, que no tenia contraparte en matriz.
11. OBL-ARCO-15 (matriz, Art. 32 Lineamientos DPO, formularios oficiales) agregada para igualar a OBL-ARCO-16 de hallazgos, que no tenia contraparte en matriz.
12. OBL-AUD-02 (matriz, Art. 50 lit. j-l LPDP, facultad de certificacion de la ACE) agregada para igualar a OBL-AUD-01 de hallazgos, que no tenia contraparte en matriz.
13. OBL-SEG-06 (matriz, Art. 56 lit. b num. 5 y 7 LPDP, infraccion grave por no implementar medidas) agregada para igualar a OBL-SEG-05 de hallazgos, que no tenia contraparte en matriz.
14. OBL-RET-06 (matriz, Art. 13-A Ley de Firma Electronica) agregada para igualar a OBL-RET-06 de hallazgos, que no tenia contraparte en matriz.

Las demas asimetrias detectadas (area PLAZO completa de matriz; OBL-SANC-05/06/08/09 de matriz; OBL-INC-05 de matriz por pertenecer a la Ley de Ciberseguridad; OBL-RET-04/05 de hallazgos; OBL-CONSENT-06 de hallazgos; OBL-SENS-01 y OBL-DOC-04 de matriz; OBL-PROV-04 de matriz; OBL-AVISO-03 de matriz) se dejaron documentadas en la tabla de la seccion 11 sin forzar una obligacion nueva, por ser diferencias estructurales de alcance (narrativa vs. catalogo, o norma distinta a la LPDP) y no gaps de investigacion.

### 12.3 Inconsistencias de clasificacion corregidas

Se detecto un patron sistematico: 7 pares de IDs (reportados por el critico) y 4 pares adicionales (detectados al construir la tabla de equivalencia) donde hallazgos clasificaba como OBLIGATORIO una obligacion que matriz ya clasificaba correctamente como CONDICIONAL, porque el hecho generador solo se activa cuando la empresa incurre en una circunstancia especifica (tener delegado, hacer transferencias internacionales, tener un encargado, ser NNA el titular, haber sido sancionada, tener un procedimiento sancionador en curso). Se corrigio hallazgos en los 11 casos para que ambos documentos coincidan, dejando la nota "ver nota de reclasificacion en el registro de cambios" en cada bloque afectado:

- OBL-DPO-02 (Art. 10 Lineamientos DPO) y OBL-DPO-03 (Art. 8 Lineamientos DPO): OBLIGATORIO -> CONDICIONAL.
- OBL-DPO-05 (Art. 18), OBL-DPO-06 (Art. 22) y OBL-DPO-07 (Art. 36) Lineamientos DPO: OBLIGATORIO -> CONDICIONAL.
- OBL-TRANSF-02 (Art. 44 inc. 1 LPDP, nivel de proteccion en transferencias internacionales): OBLIGATORIO -> CONDICIONAL.
- OBL-ENC-04 (Art. 24 lit. h LPDP, datos de contacto del encargado en el aviso): OBLIGATORIO -> CONDICIONAL.
- OBL-SENS-05 (Art. 56 lit. c num. 3 LPDP, consentimiento parental NNA), detectada al mapear contra OBL-CONS-06 de matriz: OBLIGATORIO -> CONDICIONAL.
- OBL-CAP-01 (Art. 22 Lineamientos DPO, plan anual de capacitacion), detectada al mapear contra OBL-CAP-02 de matriz: OBLIGATORIO -> CONDICIONAL.
- OBL-SANC-02 (Art. 57 LPDP, multas), detectada al mapear contra OBL-SANC-02 de matriz: OBLIGATORIO -> CONDICIONAL.
- OBL-SANC-07 (Art. 53 LPDP, remision del procedimiento a la Ley de Ciberseguridad), detectada al mapear contra OBL-SANC-04 de matriz: OBLIGATORIO -> CONDICIONAL.

Criterio aplicado (documentado aqui para que futuras rondas lo sigan): una obligacion se clasifica CONDICIONAL cuando su "a quien aplica" esta acotado a empresas que incurren en una circunstancia o actividad especifica (tener delegado, transferir datos internacionalmente, tener un encargado, tratar datos de un titular NNA, haber sido sancionada, tener un procedimiento sancionador abierto), aunque esa circunstancia sea hoy casi universal por otro mandato legal independiente (como la obligatoriedad actual del delegado). Se OBLIGATORIO cuando el "a quien aplica" es "toda empresa" sin un disparador de actividad especifico. No se aplico este criterio en retroactivo a obligaciones donde ambos documentos ya coincidian (por ejemplo OBL-SENS-01/02, tambien acotadas a empresas con datos sensibles pero clasificadas OBLIGATORIO en ambos documentos desde el origen), para no introducir una inconsistencia nueva donde antes no la habia.

Ademas, en `matriz_obligaciones.md` se corrigio la ambiguedad de norma en la tabla resumen del area SANC: las filas de OBL-SANC-05 y OBL-SANC-06 ahora indican explicitamente "(Normativa PAS)" junto al articulo, para no confundirse con el Art. 21 o el Art. 44 de la LPDP.

### 12.4 Recuento final

- 03_hallazgos_regulatorios.md: 94 -> 106 obligaciones catalogadas (61 OBLIGATORIO, 39 CONDICIONAL, 6 RECOMENDADO). Ver lista recalculada en la seccion 7.
- matriz_obligaciones (.json y .md): 92 -> 105 obligaciones catalogadas. Ver conteo recalculado en `matriz_obligaciones.md`.
- 11 clasificaciones corregidas en hallazgos para eliminar divergencias con matriz (seccion 12.3).
- Ninguna obligacion previamente verificada fue eliminada; todos los cambios fueron adiciones o correcciones de clasificacion con nota explicita.
- Puntos que siguen sin resolverse por falta de norma expresa (no inventados): el deber de instrucciones documentadas y de devolucion/eliminacion de datos por el encargado (OBL-ENC-08/09, OBL-PROV-06/07) se catalogaron como RECOMENDADO, no OBLIGATORIO, porque ni el corpus local ni la busqueda web complementaria del 2026-09-24 encontraron un articulo que los exija de forma expresa; esto debe advertirse al equipo de producto y confirmarse con abogado antes de presentarlo como obligacion legal en materiales para el cliente.
