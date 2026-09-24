# Matriz de obligaciones - PRIV-SV

Fecha de consulta / consolidacion: 2026-09-24.

Total de obligaciones: 105. Version legible por maquina: `matriz_obligaciones.json` (mismo directorio).

Fuente: nueve informes `sweep_*.md` en `C:\Proyects\PRIV-SV\analisis\01_legal\` mas verificacion adversarial consolidada (afirmaciones CONFIRMADAS o CORREGIDAS en su version corregida; las NO_VERIFICABLES se excluyeron salvo que aportaran contexto necesario, en cuyo caso quedan con `verificada: false`).

Ronda de relleno del 2026-09-24: se agregaron 13 obligaciones nuevas (areas SENS, PROV, ARCO, SEG, DPO, AUD, RET) para cerrar gaps de investigacion (biometria, subencargados, recurso ARCO-POL, eliminacion segura) y asimetrias frente a `03_hallazgos_regulatorios.md`. La tabla completa de equivalencia de IDs entre ambos documentos, con la conciliacion del conteo total y el criterio usado para las reclasificaciones, esta en `03_hallazgos_regulatorios.md`, seccion 11 ("Tabla de equivalencia de IDs") y seccion 12 ("Registro de cambios de la ronda de relleno"). Las clasificaciones de este documento (matriz) se tomaron como referencia; los ajustes de esa ronda se hicieron sobre `03_hallazgos_regulatorios.md`, no sobre esta matriz.

Clasificacion: **OBLIGATORIO** (obligacion juridica expresa) | **RECOMENDADO** (buena practica sin mandato expreso) | **CONDICIONAL** (aplica solo bajo ciertas circunstancias, ver columna Condicion en el JSON).

Nota sobre el Decreto Legislativo 659 (reforma a la LPDP, aprobado 17-sep-2026, 57 votos): al 24-sep-2026 no esta confirmada su publicacion en el Diario Oficial. Se trata como APROBADA-PENDIENTE-PUBLICACION. Toda obligacion que la reforma podria alterar (sobre todo las del area DPO, ligadas a los Arts. 15 y 17 vigentes) queda marcada con `afectada_por_reforma_659.afectada = true` en el JSON, con una nota que explica el impacto esperado segun fuentes secundarias. Mientras el decreto no se publique, el texto vigente del Decreto 144 (con delegado obligatorio en el sector privado) sigue siendo exigible.

## Tabla resumen

Columnas: id, titulo, articulo, clasificacion, plazo, modulos candidatos. El detalle completo (texto_obligacion, a_quien_aplica, condicion, vigencia, afectada_por_reforma_659, evidencia_esperada, documentos_relacionados, infracciones_asociadas, fuente, verificada) esta solo en el JSON.

### AMB - Ambito de aplicacion (4)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-AMB-01 | Ambito de aplicacion universal de la LPDP | Art. 2 inc. 1 | OBLIGATORIO | - | Organizacion, Diagnostico |
| OBL-AMB-02 | Exclusion de historial crediticio (con excepcion para sector financiero) | Art. 3 lit. a) | CONDICIONAL | - | Organizacion, Diagnostico |
| OBL-AMB-03 | Exclusion de ambito domestico | Art. 3 lit. b) | CONDICIONAL | - | Diagnostico |
| OBL-AMB-04 | Exclusiones por seguridad publica y registros publicos | Art. 3 lit. c) y d) | CONDICIONAL | - | Diagnostico |

### PRIN - Principios rectores (4)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-PRIN-01 | Principio de consentimiento y finalidad | Art. 5 lit. c) | OBLIGATORIO | - | Consentimiento, RAT, Plan |
| OBL-PRIN-02 | Principio de licitud: seis bases de tratamiento | Art. 5 lit. g) | OBLIGATORIO | - | RAT, Consentimiento, Plan |
| OBL-PRIN-03 | Principio de responsabilidad demostrada | Art. 5 lit. i) | OBLIGATORIO | - | Evidencias, Controles, Auditoria |
| OBL-PRIN-04 | Principio de ejercicio progresivo de facultades (NNA) | Art. 5 lit. j) | CONDICIONAL | - | Consentimiento, ARCO-POL |

### ARCO - Derechos ARCO-POL (procedimiento) (15)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-ARCO-01 | Legitimacion para ejercer derechos ARCO-POL | Art. 6 | OBLIGATORIO | - | ARCO-POL |
| OBL-ARCO-02 | Contenido de la respuesta al derecho de acceso | Art. 8 | OBLIGATORIO | - | ARCO-POL |
| OBL-ARCO-03 | Rectificacion: plazo, gratuidad y bloqueo cautelar | Art. 9 | OBLIGATORIO | 20 dias habiles | ARCO-POL, Tareas |
| OBL-ARCO-04 | Cancelacion: causales de procedencia e improcedencia | Art. 10 | CONDICIONAL | - | ARCO-POL |
| OBL-ARCO-05 | Oposicion al tratamiento, incluido marketing directo | Art. 12 | CONDICIONAL | - | ARCO-POL, Consentimiento |
| OBL-ARCO-06 | Limitacion del tratamiento | Art. 13 | CONDICIONAL | - | ARCO-POL |
| OBL-ARCO-07 | Portabilidad de datos | Art. 14 | CONDICIONAL | - | ARCO-POL |
| OBL-ARCO-08 | Requisitos de la solicitud ARCO-POL y prevencion unica | Art. 18 | OBLIGATORIO | 10 dias habiles | ARCO-POL |
| OBL-ARCO-09 | Devolucion de solicitud por incompetencia | Art. 19 | CONDICIONAL | 5 dias habiles | ARCO-POL |
| OBL-ARCO-10 | Plazo general de respuesta ARCO-POL y prorroga | Art. 20 | OBLIGATORIO | 20 dias habiles (prorrogable hasta 20 dias habiles adicionales) | ARCO-POL, Tareas |
| OBL-ARCO-11 | Notificacion a receptores de datos tras rectificacion, actualizacion o eliminacion | Art. 21 inc. 3 | CONDICIONAL | 5 dias habiles | ARCO-POL, Transferencias |
| OBL-ARCO-12 | Denegatoria motivada de solicitudes ARCO-POL | Art. 22 | OBLIGATORIO | 3 dias habiles | ARCO-POL |
| OBL-ARCO-13 | Gratuidad del ejercicio de derechos ARCO-POL | Art. 23 | OBLIGATORIO | - | ARCO-POL |
| OBL-ARCO-14 | Atencion al reclamo del titular ante la Direccion de Proteccion de Datos de la ACE | Art. 33 inc. 4 (Lineamientos DPO) | CONDICIONAL | 10 dias habiles (plazo del titular para reclamar) | ARCO-POL, Regulatorio |
| OBL-ARCO-15 | Aceptacion de los formularios oficiales ARCO-POL de la ACE | Art. 32 (Lineamientos DPO) | OBLIGATORIO | - | ARCO-POL |

### DPO - Delegado de Proteccion de Datos (8)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-DPO-01 | Obligatoriedad de nombrar delegado en el sector privado | Art. 15 y 17 | OBLIGATORIO | - | Organizacion, Tareas |
| OBL-DPO-02 | Notificacion interna del nombramiento del delegado | Art. 8 | CONDICIONAL | 3 dias habiles | Organizacion, Tareas |
| OBL-DPO-03 | Comunicacion del nombramiento del delegado a la ACE | Art. 10 | CONDICIONAL | 15 dias habiles | Organizacion, Regulatorio |
| OBL-DPO-04 | Reverificacion periodica del perfil del delegado | Art. 18 | CONDICIONAL | 3 anos | Organizacion, Capacitacion |
| OBL-DPO-05 | Capacitacion anual del propio delegado | Art. 22 | CONDICIONAL | 1 ano (periodicidad) | Capacitacion, Organizacion |
| OBL-DPO-06 | Confidencialidad del delegado tras el cese | Art. 36 | CONDICIONAL | 5 anos | Organizacion, Documentos |
| OBL-DPO-07 | Informe periodico del delegado al responsable | Art. 30 | CONDICIONAL | 2 veces al ano (minimo) | Organizacion, Auditoria |
| OBL-DPO-08 | Deber de asistencia de dependencias, empleados y proveedores al delegado | Art. 17 | OBLIGATORIO | - | Organizacion |

### AVISO - Aviso y politica de privacidad (5)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-AVISO-01 | Contenido minimo del aviso de privacidad | Art. 24 | OBLIGATORIO | - | Documentos, Consentimiento |
| OBL-AVISO-02 | Datos de contacto del encargado en el aviso de privacidad | Art. 24 lit. h) | CONDICIONAL | - | Documentos, Proveedores |
| OBL-AVISO-03 | Informar el uso de cookies | Art. 24 lit. i) | CONDICIONAL | - | Documentos |
| OBL-AVISO-04 | Derecho de informacion en la recoleccion | Art. 7 | OBLIGATORIO | - | Documentos, Proveedores |
| OBL-AVISO-05 | Elaboracion de la politica de privacidad | Art. 24 inc. 1 | OBLIGATORIO | - | Documentos |

### CONS - Consentimiento (6)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-CONS-01 | Requisitos del consentimiento | Art. 26 y 27 | OBLIGATORIO | - | Consentimiento |
| OBL-CONS-02 | Revocacion del consentimiento en cualquier momento | Art. 29 | OBLIGATORIO | - | Consentimiento |
| OBL-CONS-03 | Plazo para procesar la revocacion del consentimiento | Art. 30 | OBLIGATORIO | 5 dias habiles | Consentimiento, Proveedores |
| OBL-CONS-04 | Consentimiento por escrito para datos sensibles | Art. 26 inc. 4 | OBLIGATORIO | - | Consentimiento |
| OBL-CONS-05 | Carga de la prueba del consentimiento y del aviso de privacidad | Art. 54 | OBLIGATORIO | - | Consentimiento, Evidencias |
| OBL-CONS-06 | Consentimiento parental para datos de ninez y adolescencia | Art. 56 lit. c num. 3, en relacion con Art. 5 lit. j y Art. 42 | CONDICIONAL | - | Consentimiento |

### SENS - Datos sensibles (8)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-SENS-01 | Identificacion de datos personales sensibles | Art. 4 lit. g) | OBLIGATORIO | - | RAT, Consentimiento |
| OBL-SENS-02 | Advertencia del derecho a no proporcionar datos sensibles | Art. 37 inc. 1 | OBLIGATORIO | - | Consentimiento |
| OBL-SENS-03 | Excepciones al consentimiento para datos sensibles | Art. 37 inc. 2-3 y Art. 38 inc. 1 | CONDICIONAL | - | RAT, Consentimiento |
| OBL-SENS-04 | Tratamiento de datos de salud | Art. 39 | CONDICIONAL | - | RAT, Consentimiento |
| OBL-SENS-05 | Prohibiciones sobre datos sensibles y comercializacion indebida | Art. 59 | OBLIGATORIO | - | RAT, Controles |
| OBL-SENS-06 | Informacion biometrica como dato personal sensible | Art. 4 lit. g) | OBLIGATORIO | - | RAT, Consentimiento, Riesgos-EIPD |
| OBL-SENS-07 | Consentimiento escrito y alternativa no biometrica para datos biometricos | Art. 26 inc. 4 y Art. 37 | CONDICIONAL | - | Consentimiento, RAT |
| OBL-SENS-08 | Videovigilancia y reconocimiento facial | Art. 4, 7, 12, 16 | CONDICIONAL | - | RAT, Documentos, Riesgos-EIPD |

### TRAT - Tratamiento general (3)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-TRAT-01 | Prohibicion de desviacion de finalidad | Art. 32 | OBLIGATORIO | - | RAT, Consentimiento |
| OBL-TRAT-02 | Excepciones al consentimiento previo | Art. 28 | CONDICIONAL | - | RAT, Consentimiento |
| OBL-TRAT-03 | Definicion estricta de fuentes de acceso publico | Art. 4 lit. l) | CONDICIONAL | - | RAT |

### PROV - Proveedores / Encargados (7)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-PROV-01 | Sometimiento de proveedores subcontratados a la LPDP | Art. 33 inc. 2 | OBLIGATORIO | - | Proveedores |
| OBL-PROV-02 | Obligaciones directas del encargado del tratamiento | Art. 34 | OBLIGATORIO | - | Proveedores |
| OBL-PROV-03 | Medidas de seguridad tambien obligatorias para el encargado | Art. 36 | OBLIGATORIO | - | Proveedores |
| OBL-PROV-04 | No publicar datos de contacto del encargado (infraccion leve) | Art. 56 lit. a num. 2 | OBLIGATORIO | - | Proveedores, Documentos |
| OBL-PROV-05 | Subcontratacion en cadena por el encargado (subencargados) | Art. 33 inc. 2 (lectura extensiva) | CONDICIONAL | - | Proveedores |
| OBL-PROV-06 | Instrucciones documentadas del responsable al encargado | Art. 34 lit. a) / Art. 5 lit. i) | RECOMENDADO | - | Proveedores, Documentos |
| OBL-PROV-07 | Devolucion o eliminacion de datos por el encargado al finalizar la relacion | Art. 34 lit. a) / Art. 5 lit. h) | RECOMENDADO | - | Proveedores, Retencion |

### TRANSF - Transferencias de datos (6)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-TRANSF-01 | Requisitos de la transferencia nacional de datos | Art. 40 | OBLIGATORIO | - | Transferencias |
| OBL-TRANSF-02 | Contrato con el responsable receptor de la transferencia | Art. 41 | CONDICIONAL | - | Transferencias |
| OBL-TRANSF-03 | Nivel de proteccion exigido para transferencias internacionales | Art. 44 inc. 1 | CONDICIONAL | - | Transferencias |
| OBL-TRANSF-04 | Consentimiento previo para transferencias internacionales | Art. 44 inc. final | OBLIGATORIO | - | Transferencias, Consentimiento |
| OBL-TRANSF-05 | Puesta en conocimiento de la ACE del flujo transfronterizo | Art. 45 | OBLIGATORIO | - | Transferencias, Regulatorio |
| OBL-TRANSF-06 | Carga de la prueba en transferencias internacionales | Art. 54 inc. 2 | OBLIGATORIO | - | Transferencias, Evidencias |

### SEG - Seguridad (medidas tecnicas/organizativas) (6)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-SEG-01 | Caracter imperativo de las politicas de actuacion de la ACE | Art. 35 LPDP | OBLIGATORIO | - | Controles, Regulatorio |
| OBL-SEG-02 | Medidas organizativas minimas de las Politicas ACE | Art. 4 (Medidas Organizativas, lit. a-f) | OBLIGATORIO | - | Controles, RAT, Riesgos-EIPD, Capacitacion, Auditoria |
| OBL-SEG-03 | Medidas tecnicas minimas de las Politicas ACE | Art. 4 (Medidas Tecnicas) | OBLIGATORIO | - | Controles |
| OBL-SEG-04 | Medidas de seguridad especificas para transferencias de datos | Art. 4 (bloque Medidas de Seguridad en Transferencias de Datos) y Art. 6 lit. d) | OBLIGATORIO | - | Transferencias, Controles |
| OBL-SEG-05 | Eliminacion segura de documentos y dispositivos | Art. 4 (Medidas Fisicas, lit. e) | OBLIGATORIO | - | Controles, Retencion |
| OBL-SEG-06 | Infraccion grave por no implementar medidas o controles de la ACE | Art. 56 lit. b num. 5 y 7 | OBLIGATORIO | - | Controles, Regulatorio |

### DOC - Documentacion (4)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-DOC-01 | Establecer y documentar procedimientos ARCO-POL | Art. 33 inc. 1 | OBLIGATORIO | - | Documentos, ARCO-POL |
| OBL-DOC-02 | Registro de Actividades de Tratamiento (RAT) | Art. 4 (Medidas Organizativas, lit. d) | OBLIGATORIO | - | RAT |
| OBL-DOC-03 | Evaluaciones de Impacto en la Privacidad (EIPD) | Art. 4 (Medidas Organizativas, lit. e) | OBLIGATORIO | - | Riesgos-EIPD |
| OBL-DOC-04 | Elaboracion y publicacion de formularios/mecanismos ARCO-POL propios | Art. 61 inc. 2 | OBLIGATORIO | 6 meses (plazo transitorio, ya vencido el 23-may-2025) | Portal, ARCO-POL |

### INC - Incidentes / vulneraciones (5)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-INC-01 | Notificacion de vulneraciones de seguridad en 72 horas | Art. 25 | OBLIGATORIO | 72 horas (computo en horas corridas u habiles no resuelto por la ley; requiere criterio de abogado) | Incidentes, Tareas |
| OBL-INC-02 | Revision exhaustiva del incidente dentro de las 72 horas | Art. 25 inc. 2 | OBLIGATORIO | 72 horas (para iniciar, no concluir, la revision) | Incidentes |
| OBL-INC-03 | Contenido minimo de la notificacion de vulneracion | Art. 25 inc. 3-4 | OBLIGATORIO | - | Incidentes |
| OBL-INC-04 | Documentacion obligatoria de toda vulneracion con riesgo | Art. 25 inc. final | OBLIGATORIO | - | Incidentes, Evidencias |
| OBL-INC-05 | Reporte de incidentes de ciberseguridad a la ACE (operadores de infraestructura critica) | Art. 6 lit. f-g, en relacion con Art. 2 y Art. 8 lit. f-g | CONDICIONAL | - | Incidentes, Regulatorio |

### CAP - Capacitacion (2)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-CAP-01 | Capacitacion del personal como medida organizativa obligatoria | Art. 4 (Medidas Organizativas, lit. c) | OBLIGATORIO | - | Capacitacion |
| OBL-CAP-02 | Plan anual de capacitacion del personal e induccion | Art. 22 | CONDICIONAL | 1 ano (periodicidad del plan) | Capacitacion, Organizacion |

### AUD - Auditoria (2)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-AUD-01 | Auditorias anuales de cumplimiento de las Politicas ACE | Art. 8 lit. b) | OBLIGATORIO | 1 ano (periodicidad) | Auditoria |
| OBL-AUD-02 | Facultad de la ACE de crear certificaciones o sellos de proteccion de datos | Art. 50 lit. j, k, l | RECOMENDADO | - | Regulatorio |

### SANC - Sanciones y procedimiento (9)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-SANC-01 | Catalogo de infracciones leves, graves y muy graves | Art. 56 | OBLIGATORIO | - | Regulatorio, Controles |
| OBL-SANC-02 | Multas por clasificacion de infraccion | Art. 57 | CONDICIONAL | - | Regulatorio |
| OBL-SANC-03 | Medidas adicionales tras la sancion | Art. 58 | CONDICIONAL | - | Regulatorio, Tareas |
| OBL-SANC-04 | Remision del procedimiento sancionador y prescripcion a la Ley de Ciberseguridad | Art. 53 | CONDICIONAL | - | Regulatorio |
| OBL-SANC-05 | Contestacion del emplazamiento en el procedimiento sancionador | Art. 21 (Normativa PAS) | CONDICIONAL | 5 dias habiles | Regulatorio, Tareas |
| OBL-SANC-06 | Pago de la multa impuesta | Art. 44 (Normativa PAS) | CONDICIONAL | 15 dias habiles | Regulatorio |
| OBL-SANC-07 | Prescripcion de infracciones y sanciones | Art. 29 D.L. 143; Art. 47 Normativa PAS | RECOMENDADO | 5 anos | Evidencias, Retencion |
| OBL-SANC-08 | Publicidad de las resoluciones sancionatorias | Art. 55 | CONDICIONAL | - | Regulatorio |
| OBL-SANC-09 | Derecho de denuncia del titular ante la ACE | Art. 9 inc. 3 y Art. 31 | CONDICIONAL | - | ARCO-POL, Regulatorio |

### PLAZO - Plazos y calendario (5)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-PLAZO-01 | Regla de computo de plazos (dias y horas habiles) | Art. 82 LPA | OBLIGATORIO | - | Plazos, Tareas |
| OBL-PLAZO-02 | Calendario de dias inhabiles (asuetos nacionales) | Art. 190 Codigo de Trabajo, y D.L. 339/2016, D.L. 208/2012 | OBLIGATORIO | - | Plazos |
| OBL-PLAZO-03 | Plazo transitorio vencido: adecuacion de sujetos obligados tras las Politicas ACE | Art. 60 inc. 2 | OBLIGATORIO | 3 meses (plazo transitorio, ya vencido el 2/3-dic-2025) | Plan, Diagnostico |
| OBL-PLAZO-04 | Plazo transitorio vencido: mecanismos de ejercicio de derechos ARCO-POL | Art. 61 inc. 2 | OBLIGATORIO | 6 meses (plazo transitorio, ya vencido el 23-may-2025) | Portal, ARCO-POL |
| OBL-PLAZO-05 | Seguimiento de la reforma 659 a la LPDP (pendiente de publicacion) | Segun fuentes secundarias: deroga Arts. 15 y 17; reforma Arts. 16, 47 y 51 | CONDICIONAL | - | Regulatorio, Organizacion |

### RET - Retencion / conservacion documental (6)

| id | titulo | articulo | clasificacion | plazo | modulos candidatos |
|---|---|---|---|---|---|
| OBL-RET-01 | Conservacion de registros mercantiles | Art. 451 y 454 | CONDICIONAL | 10 anos (hasta 5 anos adicionales tras liquidacion del negocio) | Retencion, Documentos |
| OBL-RET-02 | Conservacion de documentacion tributaria | Art. 147 | CONDICIONAL | 10 anos | Retencion, Documentos |
| OBL-RET-03 | Conservacion de documentacion bajo la Ley Contra el Lavado de Dinero | Art. 10 lit. b) y Art. 12 | CONDICIONAL | 15 anos (minimo, para registros de transacciones); 5 anos para documentacion de operaciones | Retencion |
| OBL-RET-04 | Conservacion de la documentacion del aviso de privacidad | Art. 31 | OBLIGATORIO | 10 anos (minimo) | Retencion, Documentos |
| OBL-RET-05 | Criterio de retencion del expediente ARCO-POL e incidentes como prueba de descargo | Art. 47 Normativa PAS; Art. 5 lit. i LPDP (responsabilidad demostrada) | RECOMENDADO | 5 anos (minimo recomendado) | Retencion, Evidencias |
| OBL-RET-06 | Requisitos de la conservacion electronica de documentos con relevancia legal | Art. 13-A Ley de Firma Electronica | OBLIGATORIO | - | Retencion, Documentos |

## Conteo por clasificacion

| Clasificacion | Cantidad |
|---|---|
| OBLIGATORIO | 58 |
| CONDICIONAL | 42 |
| RECOMENDADO | 5 |
| **Total** | **105** |

## Conteo por area

| Area | Nombre | Cantidad |
|---|---|---|
| AMB | Ambito de aplicacion | 4 |
| PRIN | Principios rectores | 4 |
| ARCO | Derechos ARCO-POL (procedimiento) | 15 |
| DPO | Delegado de Proteccion de Datos | 8 |
| AVISO | Aviso y politica de privacidad | 5 |
| CONS | Consentimiento | 6 |
| SENS | Datos sensibles | 8 |
| TRAT | Tratamiento general | 3 |
| PROV | Proveedores / Encargados | 7 |
| TRANSF | Transferencias de datos | 6 |
| SEG | Seguridad (medidas tecnicas/organizativas) | 6 |
| DOC | Documentacion | 4 |
| INC | Incidentes / vulneraciones | 5 |
| CAP | Capacitacion | 2 |
| AUD | Auditoria | 2 |
| SANC | Sanciones y procedimiento | 9 |
| PLAZO | Plazos y calendario | 5 |
| RET | Retencion / conservacion documental | 6 |
| **Total** | | **105** |

## Conteo por modulo candidato

| Modulo candidato | Cantidad de obligaciones |
|---|---|
| ARCO-POL | 20 |
| Consentimiento | 20 |
| Regulatorio | 16 |
| Documentos | 14 |
| RAT | 14 |
| Organizacion | 12 |
| Proveedores | 10 |
| Controles | 9 |
| Retencion | 9 |
| Tareas | 8 |
| Transferencias | 8 |
| Evidencias | 6 |
| Capacitacion | 5 |
| Diagnostico | 5 |
| Incidentes | 5 |
| Auditoria | 4 |
| Riesgos-EIPD | 4 |
| Plan | 3 |
| Plazos | 2 |
| Portal | 2 |

## Obligaciones afectadas por la reforma 659

Total: 17 (15 originales mas OBL-DPO-08 y OBL-ARCO-14, agregadas en la ronda de relleno del 2026-09-24). Todas corresponden a la obligatoriedad del delegado de proteccion de datos en el sector privado (area DPO) y a obligaciones conexas (capacitacion del delegado, conservacion documental ligada a los Lineamientos del Delegado, el recurso ante la Direccion de Proteccion de Datos, y el propio seguimiento regulatorio de la reforma).

| id | titulo | nota |
|---|---|---|
| OBL-ARCO-01 | Legitimacion para ejercer derechos ARCO-POL | La reforma 659 no altera la legitimacion del Art. 6, solo el canal de recepcion (directo ante la empresa en vez de via delegado obligatorio). |
| OBL-ARCO-08 | Requisitos de la solicitud ARCO-POL y prevencion unica | El texto vigente atribuye la prevencion al delegado; la reforma 659 trasladaria esta funcion al sujeto obligado si deroga el delegado obligatorio en el sector privado. |
| OBL-ARCO-10 | Plazo general de respuesta ARCO-POL y prorroga | Segun fuentes secundarias, la reforma 659 mantiene este plazo de 20+20 dias habiles sin modificacion. |
| OBL-ARCO-11 | Notificacion a receptores de datos tras rectificacion, actualizacion o eliminacion | Segun fuentes secundarias, la reforma 659 mantiene el plazo de 5 dias habiles para notificar a terceros. |
| OBL-CAP-02 | Plan anual de capacitacion del personal e induccion | Si la reforma 659 elimina la obligatoriedad del delegado en el sector privado, esta obligacion especifica dejaria de ser exigible salvo que la empresa mantenga delegado voluntariamente. |
| OBL-CONS-03 | Plazo para procesar la revocacion del consentimiento | El texto vigente atribuye el tramite al delegado; la reforma 659 trasladaria la funcion al sujeto obligado. Segun fuentes secundarias, el plazo de 5 dias habiles para revocacion no cambia. |
| OBL-DPO-01 | Obligatoriedad de nombrar delegado en el sector privado | Segun fuentes secundarias (prensa y nota oficial de la Asamblea), el Decreto 659 deroga los Arts. 15 y 17, eliminando la obligatoriedad del delegado en el sector privado; texto oficial no localizado, publicacion en Diario Oficial no confirmada al 24-sep-2026. |
| OBL-DPO-02 | Notificacion interna del nombramiento del delegado | Si la reforma 659 entra en vigencia y elimina la obligatoriedad en el sector privado, este plazo pasaria a ser relevante solo para quien mantenga delegado voluntariamente. |
| OBL-DPO-03 | Comunicacion del nombramiento del delegado a la ACE | Ver nota en OBL-DPO-01 sobre la reforma 659. |
| OBL-DPO-04 | Reverificacion periodica del perfil del delegado | Ver nota en OBL-DPO-01. |
| OBL-DPO-05 | Capacitacion anual del propio delegado | Ver nota en OBL-DPO-01. |
| OBL-DPO-06 | Confidencialidad del delegado tras el cese | Ver nota en OBL-DPO-01. |
| OBL-DPO-07 | Informe periodico del delegado al responsable | Ver nota en OBL-DPO-01. |
| OBL-PLAZO-05 | Seguimiento de la reforma 659 a la LPDP (pendiente de publicacion) | Esta ficha ES la reforma 659; su contenido detallado proviene solo de fuentes secundarias (prensa) y de la nota oficial de la Asamblea, que no reproduce el texto articulado. Debe revalidarse en cuanto se publique el Decreto en el Diario Oficial. |
| OBL-RET-04 | Conservacion de la documentacion del aviso de privacidad | Este articulo pertenece a los Lineamientos del Delegado; si la reforma 659 elimina el delegado obligatorio en el sector privado, deberia confirmarse si la obligacion de conservacion documental subsiste bajo otra norma. |
| OBL-DPO-08 | Deber de asistencia de dependencias, empleados y proveedores al delegado | El Decreto 659 derogaria el Art. 17 junto con el Art. 15, eliminando la obligatoriedad del delegado y, con ella, este deber de asistencia especifico hacia el delegado. |
| OBL-ARCO-14 | Atencion al reclamo del titular ante la Direccion de Proteccion de Datos de la ACE | Si la reforma 659 elimina el delegado obligatorio, el reclamo se dirigiria contra la resolucion del sujeto obligado en lugar del delegado; se desconoce si el mecanismo ante la Direccion de Proteccion de Datos subsiste igual. |

## Obligaciones no verificadas de forma independiente (verificada: false)

| id | titulo | motivo |
|---|---|---|
| OBL-PLAZO-05 | Seguimiento de la reforma 659 a la LPDP (pendiente de publicacion) | Contenido articulado del Decreto 659 basado en fuentes secundarias; texto oficial no localizado al 24-sep-2026 |
| OBL-PROV-05 | Subcontratacion en cadena por el encargado (subencargados) | Interpretacion extensiva del Art. 33 inc. 2; la LPDP no usa el termino "subencargado" ni distingue niveles de subcontratacion; sin lineamiento ACE especifico al 24-sep-2026 |
| OBL-PROV-06 | Instrucciones documentadas del responsable al encargado | No se localizo articulo expreso en la LPDP, Politicas ACE, Lineamientos DPO ni Normativa Sancionadora; recomendacion de diseno apoyada en Art. 34 y Art. 5 lit. i |
| OBL-PROV-07 | Devolucion o eliminacion de datos por el encargado al finalizar la relacion | No se localizo articulo expreso; recomendacion de diseno apoyada en Art. 34 y Art. 5 lit. h |
