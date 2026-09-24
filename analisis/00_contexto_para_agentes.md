# CONTEXTO COMPARTIDO PARA AGENTES - PROYECTO PRIV-SV

Fecha de referencia del analisis: 2026-09-23.

## 1. Que es el proyecto

Plataforma SaaS B2B de autogestion de proteccion de datos personales para empresas de El Salvador.
La empresa cliente designa personas internas (no necesariamente abogados) y el software convierte
la Ley para la Proteccion de Datos Personales en procesos, responsables, tareas, plazos, controles,
documentos, evidencia y auditoria. El software NO sustituye asesoria juridica ni actua como delegado,
abogado, auditor o responsable del tratamiento del cliente.

Documento maestro (hipotesis de producto, NO verdad establecida):
`C:\Proyects\PRIV-SV\PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md`

Fase actual: ANALISIS FUNCIONAL. Prohibido escribir codigo, SQL, APIs, componentes, migraciones o
arquitectura tecnica. El entregable es un blueprint funcional.

## 2. Corpus juridico local ya descargado (usar antes que la web)

Carpeta: `C:\Proyects\PRIV-SV\analisis\01_legal\fuentes\`

| Archivo | Que es | Estado |
|---|---|---|
| `ace_decreto_144.txt` | Texto integro de la Ley para la Proteccion de Datos Personales (Decreto Legislativo 144), 64 articulos, copia publicada por la ACE | Texto limpio UTF-8, 28 paginas |
| `diario_oficial_2024-11-15_mh.txt` | Diario Oficial Tomo 445, Numero 219, 15 nov 2024, contiene Decreto 143 (Ley de Ciberseguridad y Seguridad de la Informacion) y Decreto 144 | Texto extraido, 40 paginas |
| `ace_politicas_protecciondatos.txt` | Politicas N. 001-0309025-DPDP "Politicas de Actuacion y Manejo de Datos Personales" emitidas por la ACE (Art. 35 y 50 lit. i LPDP) | Texto limpio, 6 paginas. Fecha de emision y publicacion PENDIENTE de verificar |
| `lineamientos_dpo_OCR.txt` | Lineamientos para el Delegado de Proteccion de Datos Personales (ACE), publicados en D.O. 11 ago 2026, vigentes desde 19 ago 2026 | OCR de PDF escaneado, 11 paginas, puede tener errores de reconocimiento. Imagenes en `ocr/lineamientos_dpo/page-NN.png` |
| `normativa_sancionadora_OCR.txt` | Normativa para el Procedimiento Administrativo Sancionador en el ambito de la LPDP (ACE), D.O. 11 ago 2026, vigente desde 19 ago 2026 | OCR, 9 paginas. Imagenes en `ocr/normativa_sancionadora/page-NN.png` |
| `dictamen_11_2024_ley_original_OCR.txt` | Dictamen N. 11 de la Comision de Seguridad Nacional y Justicia, 11 nov 2024, sobre la ley original | OCR, 44 paginas. Solo historia legislativa |
| `ace_form_acceso.txt`, `ace_form_cancelacion.txt`, `ace_form_portabilidad.txt`, `ace_form_nombramiento_delegado.txt` | Formularios oficiales ARCO-POL y de nombramiento de delegado publicados por la ACE (version 07-07-2025) | Texto limpio |

Fuentes oficiales en linea:
- ACE: https://ace.gob.sv/ , formularios: https://ace.gob.sv/page/formularios , politicas: https://ace.gob.sv/politicas.php
- Asamblea Legislativa: https://www.asamblea.gob.sv/ (buscador de decretos: /leyes-y-decretos/busqueda-decretos)
- Noticia oficial de la reforma: https://www.asamblea.gob.sv/node/14116
- Diario Oficial / Imprenta Nacional: https://www.diariooficial.gob.sv/ y https://imprentanacional.gob.sv/

## 3. Hechos ya verificados contra fuente primaria (no volver a investigar, si citar)

- Ley: "Ley para la Proteccion de Datos Personales", Decreto Legislativo N. 144. Aprobada 12 nov 2024,
  sancionada 14 nov 2024, publicada en D.O. N. 219, Tomo 445, 15 nov 2024. Art. 64: vigencia ocho dias
  despues de su publicacion (es decir, vigente desde el 23 de noviembre de 2024).
- Entidad rectora: Agencia de Ciberseguridad del Estado (ACE), Art. 50. Director de Proteccion de Datos
  Personales, Art. 51 y 52.
- Art. 60: la ACE debia dictar politicas, medidas y guias en 3 meses desde la vigencia; los sujetos
  obligados tienen 3 meses desde la emision de esas disposiciones para adecuarse. Art. 61: 6 meses desde
  la vigencia para establecer mecanismos de ejercicio de derechos.
- ARCO-POL = Acceso, Rectificacion, Cancelacion, Oposicion, Portabilidad, Olvido, Limitacion (Art. 4 lit. i,
  Arts. 6 a 14). Solicitud: requisitos Art. 18. Prevencion: una sola vez, 10 dias habiles para subsanar
  (Art. 18). Incompetencia: devolver en 5 dias habiles (Art. 19). Plazo de respuesta: 20 dias habiles,
  prorrogable por causas justificadas hasta otros 20 dias habiles (Art. 20). Rectificacion: resolver en 20
  dias habiles y bloquear datos en revision (Art. 9). Notificar a receptores la rectificacion/eliminacion en
  5 dias habiles desde la procedencia (Art. 21). Denegatoria motivada notificada en 3 dias habiles desde la
  decision (Art. 22). Gratuidad, solo costos de reproduccion/envio publicados (Art. 23).
- Revocacion del consentimiento: 5 dias habiles para proceder, y 5 dias habiles para informar al encargado
  (Art. 30).
- Vulneraciones de seguridad (Art. 25): notificar a la ACE, a la Fiscalia General de la Republica y a los
  titulares afectados en un plazo maximo de 72 horas desde que se tuvo conocimiento. Contenido minimo a) a
  e). A titulares solo a), b), d), e). Obligacion de documentar toda vulneracion (fecha, motivo, hechos,
  efectos, medidas correctivas inmediatas y definitivas) a disposicion de la autoridad.
- Aviso de privacidad (Art. 24): contenido minimo a) a i), debe ser consistente con la politica de
  privacidad que el responsable debe elaborar. Derecho de informacion en la recoleccion (Art. 7).
- Consentimiento: expreso, libre, especifico, informado, individualizado (Arts. 26 y 27). Datos sensibles:
  consentimiento por escrito con firma autografa o equivalente (Art. 26 inc. 4, Art. 37). Excepciones al
  consentimiento Art. 28. Bases de licitud Art. 5 lit. g (consentimiento, contrato, obligacion legal,
  intereses vitales, interes publico, interes legitimo).
- Carga de la prueba del consentimiento y de la comunicacion del aviso recae en el responsable (Art. 54).
- Transferencias: Art. 40 (consentimiento previo e informacion al titular), Art. 41 (contrato con el
  receptor con al menos las mismas obligaciones), Art. 44 (internacionales: nivel adecuado; consentimiento
  previo salvo excepciones; excepcion de integracion economica centroamericana), Art. 45 (el flujo
  transfronterizo "se pondra en conocimiento" de la ACE, incluyendo informacion de la transferencia y
  "registro de banco de datos"; opinion previa opcional).
- Encargados/proveedores: Art. 33 inc. 2 (proveedores subcontratados sometidos a la ley y lineamientos),
  Art. 34 (obligaciones de responsable y encargado), Art. 36 (medidas de seguridad tambien obligatorias
  para el encargado).
- Procedimientos ARCO-POL documentados: Art. 33 inc. 1 (obligacion expresa de establecer y documentar).
- Infracciones: Art. 56 (leves, graves, muy graves, con lista). Multas Art. 57: leves 1 a 10, graves 11 a 25,
  muy graves 26 a 40 salarios minimos mensuales del sector comercio. Medidas adicionales Art. 58.
  Prohibiciones Art. 59. Procedimiento sancionador remite a la Ley de Ciberseguridad (Art. 53). LPA supletoria
  (Art. 62). Resoluciones sancionatorias se publican en version publica (Art. 55).
- Sector publico: Titulo III (Arts. 46 a 49). Este producto se dirige al sector privado.
- Exclusiones Art. 3 (historial crediticio bajo su ley especial, ambito domestico, seguridad publica,
  registros publicos y DUI).
- Politicas de Actuacion ACE (N. 001-0309025-DPDP): declaran de cumplimiento obligatorio para entidades
  publicas y privadas medidas organizativas (Politica de Proteccion de Datos, Delegado, capacitacion,
  Registro de Actividades de Tratamiento, EIPD, auditorias de cumplimiento), tecnicas (control de acceso con
  2FA, cifrado en reposo y transito, gestion de identidades, backups, firewall/antivirus/IDS-IPS, analisis de
  vulnerabilidades y pentesting, "digitalizacion: usar sistemas especializados que permitan gestionar y
  documentar el tratamiento"), fisicas y de transferencia; auditorias anuales (Art. 8 lit. b). Referencia
  cruzada a ISO 27001.
- Reforma de septiembre de 2026 (Decreto Legislativo N. 659, aprobado el 17 sep 2026 con 57 votos, iniciativa
  del Ejecutivo): segun prensa y nota oficial de la Asamblea, deroga Arts. 15 y 17 (delegado obligatorio en el
  sector privado), reforma Art. 16 (las funciones pasan a los "sujetos obligados"), Art. 47 (sector publico
  mantiene delegado, puede ser el Oficial de Informacion) y Art. 51 (Presidente nombra Director de Proteccion
  de Datos por 3 anos); las solicitudes ARCO-POL se presentan directamente ante la empresa; se mantienen los
  plazos de 20+20 dias habiles, prevencion unica de 10 dias, devolucion en 5, notificacion a terceros en 5,
  revocacion en 5. Vigencia: 8 dias despues de su publicacion en el Diario Oficial. AL 23 SEP 2026 NO ESTA
  CONFIRMADA LA PUBLICACION EN EL DIARIO OFICIAL: tratar la reforma como APROBADA PERO DE VIGENCIA PENDIENTE
  DE VERIFICACION. El texto oficial del decreto no ha sido localizado; toda afirmacion sobre su contenido
  exacto debe marcarse como "segun fuentes secundarias" hasta obtener el texto.
- Lineamientos para el Delegado (ACE): publicados D.O. 11 ago 2026, vigentes 19 ago 2026. Segun fuentes
  secundarias: delegado puede ser persona natural interna o externa o persona juridica; requisitos (grado
  universitario, mayor de 21, experiencia); certificacion ACE; comunicacion del nombramiento a la ACE en 15
  dias habiles; registro transitorio en 20 dias habiles desde la vigencia (fecha limite 16 sep 2026), que la
  ACE dejo sin efecto tras el anuncio de la reforma. Verificar contra el OCR local.

## 4. Reglas de redaccion para todo entregable

- Idioma: espanol. Registro profesional, claro, sin lenguaje juridico innecesario cuando el lector es un
  usuario empresarial.
- Formato: Markdown. Sin guiones largos (em dash), sin comillas tipograficas, sin simbolos Unicode
  decorativos. Usar guion simple "-" y comillas rectas. Diagramas en bloques de codigo con ASCII puro
  (flechas "->" y "|", "v"). Acentos y enie del espanol si estan permitidos.
- Toda afirmacion juridica: indicar Norma, Articulo, Fuente oficial (URL o archivo local), fecha de consulta
  2026-09-23 y estado de vigencia. Clasificar cada obligacion como OBLIGATORIO, RECOMENDADO o CONDICIONAL.
- No inventar articulos ni obligaciones. Si hay duda, decirlo explicitamente. Si una conclusion requiere
  abogado, indicarlo.
- Diferenciar ley, reglamento/normativa ACE, lineamiento, politica de actuacion y buena practica.
- El software orienta, explica, organiza, alerta, calcula, registra, documenta y genera evidencia. Nunca
  afirma cumplimiento legal ni toma decisiones juridicas por la empresa.
