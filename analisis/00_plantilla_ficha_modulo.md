# PLANTILLA OBLIGATORIA DE FICHA FUNCIONAL POR MODULO

Cada modulo del blueprint se documenta usando EXACTAMENTE esta estructura y este orden de secciones.
No omitir ninguna seccion. Si una seccion no aplica, escribir "No aplica" y explicar por que en una linea.

Regla de oro: el lector es una persona de la empresa que NO es especialista en proteccion de datos.
Cada campo, alerta y texto de ayuda debe poder entenderse sin conocer la ley. El fundamento legal se cita
siempre con el ID de obligacion (OBL-AREA-NN) y el articulo, pero en un segundo nivel (ayuda contextual),
no en el lenguaje principal de la pantalla.

Reglas de formato: Markdown, espanol, sin guiones largos, sin comillas tipograficas, sin simbolos Unicode
decorativos; guion simple y comillas rectas. Diagramas y workflows en bloques de codigo ASCII con "->",
"|" y "v". Tablas Markdown para campos y alertas.

---

# MODULO: [NOMBRE]

Codigo corto del modulo: [MOD-XXX]
Clasificacion global del modulo: MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE (para el MVP)
Obligaciones que cubre: lista de IDs OBL-... (de matriz_obligaciones.json)

## A. Proposito

- Por que existe.
- Que problema resuelve para la empresa.
- Que obligacion u obligaciones cubre (IDs y articulos).
- Que valor aporta (operativo, probatorio, de reduccion de riesgo).
- Que NO hace este modulo (limites explicitos).

## B. Usuarios

Lista de roles que lo usan (usar los roles estandar definidos en el sistema de roles: Administrador de
organizacion, Responsable de privacidad, Gestor ARCO-POL, Legal, IT/Seguridad, RRHH, Marketing,
Responsable de area, Aprobador, Auditor/Lectura, Titular externo cuando aplique) y para que lo usa cada uno.

## C. Permisos

Tabla con filas = acciones (ver, crear, modificar, aprobar, cerrar, eliminar/archivar, exportar, asignar,
comentar, adjuntar evidencia) y columnas = roles. Indicar separacion de funciones (quien no puede aprobar
lo que creo) y que acciones exigen doble control.

## D. Informacion de entrada

Definir CADA campo. Tabla con columnas:
Campo | Tipo (texto, texto largo, seleccion unica, seleccion multiple, fecha, numero, archivo, referencia a
otra entidad, booleano, lista) | Obligatorio u opcional (y en que estado del workflow pasa a ser
obligatorio) | Opciones o catalogo (listar valores o nombrar el catalogo) | Validacion | Texto de ayuda que
vera el usuario (lenguaje sencillo, con ejemplo) | Fundamento (OBL-ID o "buena practica").

Indicar que campos se precargan desde el diagnostico, desde plantillas o desde otros modulos.
Indicar que campos contienen o podrian contener datos personales y como se minimizan (privacy by design:
metadatos y referencias, no copias de bases de datos).

## E. Informacion generada

Que produce el sistema a partir de la entrada: registros, tareas, alertas, calculos (plazos, scores),
documentos o borradores, reportes, evidencias, indicadores, eventos de auditoria. Para cada salida:
nombre, contenido, formato, cuando se genera, quien la recibe.

## F. Workflow

Diagrama ASCII de estados. Tabla de transiciones: Estado origen | Evento o accion | Condiciones y
validaciones | Estado destino | Quien puede ejecutarla | Efectos (tareas, alertas, evidencia, auditoria).
Incluir estados terminales, reapertura, archivado y que pasa con los registros vinculados.

## G. Automatizaciones

Lista de reglas automaticas: disparador -> condicion -> accion. Ejemplos: calcular plazo, crear tarea,
crear recordatorio, solicitar aprobacion, generar borrador de documento, actualizar indicador, bloquear
accion, escalar. Indicar si son configurables por la empresa.

## H. Decisiones que NO debe automatizar

Lista de decisiones que exigen persona responsable, aprobacion interna o abogado, con el texto de
advertencia que mostrara el sistema ("Requiere validacion de la organizacion o asesoria especializada").
Explicar por que en cada caso.

## I. Alertas

Tabla: Alerta | Disparador | Nivel (INFO, WARNING, HIGH, CRITICAL) | Destinatario | Canal por defecto |
Frecuencia o repeticion | Escalamiento (a quien y cuando) | Se apaga cuando.

## J. Evidencia

Que evidencia genera o conserva el modulo y como: registro con fecha y hora, usuario, version, archivo
adjunto con hash, aprobacion con identidad y fecha, historial inmutable, exportacion firmada. Indicar
que obligacion prueba cada evidencia (OBL-ID) y cuanto tiempo se conserva (referenciar reglas de retencion
del sistema).

## K. Documentos asociados

- Documentos requeridos como entrada (por ejemplo contrato con proveedor).
- Documentos generados (borradores, resoluciones, notificaciones, actas).
- Plantillas que el sistema provee (nombre, variables, si requiere validacion de la organizacion).
- Anexos y evidencias documentales.

## L. Dependencias

Diagrama ASCII y lista: de que modulos recibe datos, a que modulos envia datos o eventos, que catalogos
comparte. Indicar que ocurre si el modulo dependiente no existe en el MVP.

## M. Dashboard

Indicadores que este modulo aporta al dashboard, con formula, semaforo y vista por rol (Gerencia,
Responsable, Legal, Auditor). Nunca expresar "porcentaje de cumplimiento legal"; usar estado del
programa, controles configurados, tareas pendientes, evidencia disponible.

## N. Reportes

Reportes que produce: nombre, contenido, filtros, formato (PDF, XLSX, CSV, ZIP), destinatario tipico,
si forma parte del paquete de evidencia para auditoria o para la ACE.

## O. Historial

Eventos que deben quedar en el historial del modulo y en la auditoria transversal: creacion, cambios de
campo (valor anterior y nuevo), cambios de estado, asignaciones, aprobaciones, adjuntos, exportaciones,
accesos de lectura a datos sensibles, eliminaciones o archivados, motivo.

## P. Riesgos

- Riesgos legales (por ejemplo dar por valida una base juridica).
- Riesgos de UX (por ejemplo abandono del formulario por complejidad).
- Riesgos operativos (por ejemplo plazos mal calculados por calendario desactualizado).
- Riesgos de seguridad y privacidad (por ejemplo exposicion de datos del titular en el portal).
Para cada riesgo: mitigacion de diseno.

## Q. MVP

Tabla: Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion
(obligacion, valor, complejidad, riesgo, dependencia). Concluir con la version minima del modulo que ya
puede venderse y la razon.

## R. Ayuda contextual (complemento obligatorio)

Para los 3 a 6 conceptos centrales del modulo, escribir el texto de ayuda en cuatro partes:
"Que es" (explicacion sencilla), "Por que tengo que hacer esto", "Fundamento" (articulo y OBL-ID),
"Cuando necesito ayuda juridica" (advertencia).
