# 11. Sistema de roles y permisos

Fecha de elaboracion: 2026-09-24. Fase: analisis funcional (prohibido codigo, SQL, APIs, esquemas de base de datos, nombres de tecnologias, stack o infraestructura).

Esta seccion consolida y cruza lo ya decidido en `02_validacion/05_tipos_de_usuario.md` (los 12 roles estandar y las reglas minimas de separacion de funciones, secciones 5.3 y 5.4), en `02_validacion/06_mapa_definitivo_de_modulos.md` (el mapa de 26 modulos y el doble estado de la reforma 659) y en la seccion C ("Permisos") y otras secciones relevantes (B, D, F, H, J, O) de las 26 fichas funcionales de `03_modulos/MOD-001_ficha.md` a `MOD-026_ficha.md`. No inventa funcionalidades que ninguna ficha define. Donde el prompt del cliente exige un contenido que ninguna ficha cubre, se marca explicitamente "propuesta de esta seccion, no presente en las fichas". Toda obligacion legal se cita con su ID canonico de `01_legal/matriz_obligaciones.json` (formato OBL-AREA-NN) junto con norma y articulo; los IDs preliminares de `01_legal/03_hallazgos_regulatorios.md` (OBL-AMBITO-xx, OBL-CONSENT-xx y similares) no se usan aqui, conforme a la equivalencia de la seccion 11 de ese documento.

Jerarquia usada para resolver cualquier discrepancia entre fuentes: fuente legal primaria y `matriz_obligaciones.json` sobre `mapa_modulos.json` y `06_mapa_definitivo_de_modulos.md`, estos sobre `05_tipos_de_usuario.md` para lo relativo a roles, y estos sobre la ficha del modulo propietario de la obligacion, y esta sobre cualquier otra ficha que mencione el mismo tema de forma colaboradora. Las contradicciones detectadas al aplicar esta jerarquia y los huecos (piezas que ninguna ficha define) se listan al final, en "Contradicciones y huecos detectados".

El software nunca decide cuestiones juridicas ni afirma cumplimiento: lo que este documento llama "aprobar" es siempre una confirmacion humana registrada, nunca una conclusion automatica del sistema. El sistema calcula, redacta borradores, alerta, organiza y registra evidencia; la persona con el rol correspondiente decide.

---

## 11.1 Los 12 roles estandar del sistema

Fuente primaria de esta subseccion: `02_validacion/05_tipos_de_usuario.md`, secciones 5.1 y 5.3. Ningun nombre ni alcance de rol tiene respaldo legal expreso salvo el Delegado de Proteccion de Datos (Arts. 15 y 17 LPDP vigentes, ver 11.8); el resto es **[opinion de producto]**, tal como esa misma fuente lo declara en su seccion "Resumen de decisiones que quedan como opinion de producto".

| Rol | Proposito | Quien lo ocupa en pyme (aprox. 30 empleados) | Quien lo ocupa en empresa mediana (aprox. 300 empleados) | Quien lo ocupa en corporativo (varias sociedades) | Acumulable |
|---|---|---|---|---|---|
| Administrador de la organizacion | Configura estructura, usuarios, permisos e integraciones; no necesariamente revisa contenido legal en detalle | El dueno o gerente administrativo/financiero (perfil Karla Hernandez); casi siempre la misma persona que el Delegado | Un cargo especifico (por ejemplo Jefe de TI o de Administracion), distinto del Delegado | Un rol tecnico dedicado por sociedad, coordinado por la Direccion de Cumplimiento Corporativo a nivel de grupo (visibilidad multi-sociedad consolidada es funcionalidad V1/Enterprise, no MVP, ver `02_validacion_de_la_idea.md` decision 2.7.31) | Si, con casi todos los demas roles |
| Delegado de Proteccion de Datos (o Responsable interno, si el estado FUTURO de la reforma 659 esta activo, ver 11.8) | Concentra hoy las funciones legales del Delegado (ARCO-POL, informes, enlace con la ACE); en estado FUTURO coordina la funcion sin investidura legal obligatoria | La misma Gerente Administrativa (perfil Karla); acumula con Administrador | Un cargo dedicado, por ejemplo Jefe de Cumplimiento y Riesgo (perfil Jorge Menendez), en proceso de certificacion ACE | Un Delegado certificado por sociedad regulada (perfil Lic. Mauricio Aguilar) o un Delegado externo comun a varias sociedades del grupo si la normativa sectorial lo permite | Si, una sola persona puede ocuparlo junto con Administrador |
| Responsable ARCO-POL / Responsable del tramite | Ejecuta el dia a dia de las solicitudes de titulares dentro de los plazos legales | El mismo Delegado (o Administrador) atiende los casos, dado el bajo volumen esperado | Personal de atencion al cliente o del area legal, distinto del Delegado | Un equipo dedicado por sociedad, o centralizado a nivel de grupo segun el volumen | Si |
| Responsable Legal / Compliance | Revisa bases juridicas, documentos, denegatorias y contratos | El mismo Administrador/Delegado, con apoyo puntual de un abogado externo (perfil Douglas Quintanilla) cuando el caso lo exige | Un abogado interno o el mismo Jefe de Cumplimiento con apoyo externo | La Directora de Cumplimiento Corporativo (perfil Ana Reyes), abogada interna, con visibilidad sobre varias sociedades | Si en pyme |
| Responsable de Seguridad / IT | Registra controles tecnicos y evidencia, gestiona incidentes y el cronometro de 72 horas | El proveedor externo de TI de la pyme, si no hay TI interno, o el mismo Administrador | El Gerente de Tecnologia (perfil Roberto Villalta), con equipo propio | Un area de Seguridad de la Informacion dedicada, coordinada con la Ley de Ciberseguridad a nivel de grupo | Si en pyme |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Registra y mantiene actualizados los tratamientos de su area en el RAT, ejecuta las tareas que le asignan | Un solo empleado puede cubrir varias areas a la vez (por ejemplo, la misma Gerente Administrativa cubre RRHH) | Jefes de cada area por separado (por ejemplo, Coordinadora de RRHH, perfil Daniela Cornejo) | Jefes de area por sociedad, sin consolidacion automatica entre sociedades | No aplica: por diseno son varios usuarios distintos |
| Aprobador | Aprueba documentos, decisiones de riesgo y cierres de casos sensibles antes de publicarse o enviarse, segun la cadena de aprobacion configurada por tipo de documento o accion | El mismo Administrador o Delegado, con advertencia visible de autorrevision | Gerencia, o el mismo Delegado si la empresa aun no separa funciones | Gerencia de cada sociedad o la Direccion de Cumplimiento Corporativo, segun el tipo de acto | Si en pyme; en mediana/corporativo se recomienda separarlo (ver 11.3) |
| Auditor (interno) | Solo lectura y exportacion de evidencia; no crea ni aprueba nada | Puede recaer en el mismo Delegado, con advertencia visible de autorrevision | Auditoria interna corporativa o un cargo de control interno distinto del Delegado | Auditoria interna corporativa a nivel de grupo | Con advertencia visible en pyme |
| Auditor externo (invitado) | Acceso temporal de solo lectura para una auditoria puntual | Un contador o consultor externo contratado para la auditoria anual de cumplimiento (OBL-AUD-01) | Una firma auditora externa (perfil Francisco Bonilla) | Una firma auditora externa, a veces distinta por sociedad segun el regulador sectorial | No aplica, siempre es un tercero |
| Usuario de consulta / Colaborador | Ve y completa unicamente las tareas que se le asignan | Cualquier empleado operativo de la pyme que ejecuta una tarea puntual | Empleados operativos de cualquier area | Empleados operativos de cualquier sociedad del grupo | Se acumula naturalmente en pyme al ser pocos empleados |
| Titular (formulario externo) | Presenta y da seguimiento a su propia solicitud ARCO-POL | Cliente, empleado, ex empleado o candidato de la pyme (perfil Cecilia Marroquin) | Igual, a escala de empresa mediana | Igual, a escala de cada sociedad del grupo | No aplica, no es usuario interno de la organizacion |
| Asesor externo invitado | Acceso acotado en tiempo a un caso o modulo especifico | Un abogado externo ocasional (perfil Douglas Quintanilla) o un Delegado externo que atiende a varios clientes (perfil Silvia Melendez) | Un consultor de seguridad o abogado externo puntual | Un asesor externo especializado por sociedad o por materia (por ejemplo, regulacion financiera sectorial) | No aplica, siempre externo y temporal |

Nota sobre la columna "empresa mediana" y "corporativo": la asignacion de personas concretas a estos dos tamanos de empresa no esta desarrollada como tal en ninguna ficha de modulo (que solo distinguen "pyme" de "empresa mediana o corporativo" de forma conjunta al describir separacion de funciones); esta columna adicional que separa mediana de corporativo es una elaboracion de esta seccion a partir de los perfiles de `05_tipos_de_usuario.md` seccion 5.1, marcada aqui como **[propuesta de esta seccion, no presente literalmente en las fichas de modulo, consistente con los perfiles de 5.1]**.

---

## 11.2 Matriz consolidada modulo por rol

Consolida la seccion C ("Permisos") de las 26 fichas funcionales, modulo por modulo, agrupadas por las 6 etapas del recorrido mas la capa transversal (mismo orden y agrupacion que `06_mapa_definitivo_de_modulos.md`, seccion 1). Se usa siempre el mismo conjunto de 12 roles y el mismo conjunto de acciones para que las 26 tablas sean comparables entre si; donde una ficha detalla una accion con mas granularidad (por ejemplo, "aprobar la prevencion" y "aprobar la resolucion final" por separado en MOD-011), esta tabla usa la fila generica "Aprobar" y el detalle fino se remite a la ficha del modulo y al catalogo de doble control de la seccion 11.3.

Columnas (roles, mismas siglas en las 26 tablas):

| Sigla | Rol |
|---|---|
| ADM | Administrador de la organizacion |
| DEL | Delegado de Proteccion de Datos / Responsable interno |
| ARC | Responsable ARCO-POL / Responsable del tramite |
| LEG | Responsable Legal / Compliance |
| SEG | Responsable de Seguridad / IT |
| ARE | Responsable de area |
| APR | Aprobador |
| AUI | Auditor (interno) |
| AUE | Auditor externo (invitado) |
| COL | Usuario de consulta / Colaborador |
| TIT | Titular (formulario externo) |
| ASE | Asesor externo invitado |

Filas (acciones estandar de la plantilla de ficha, seccion C): Ver, Crear, Modificar, Aprobar, Cerrar/archivar, Exportar, Asignar, Comentar, Adjuntar evidencia.

Simbologia: **Si** = permitido; **Si\*** = permitido solo dentro del alcance propio (su caso, su area, su tarea asignada, o con la condicion que indica la nota); **Doble** = la accion exige doble control segun 11.3 (no la ejecuta una sola persona); **No** = no permitido; **-** = no aplica al modulo o al rol.

### ETAPA 1: EMPEZAR

#### MOD-001 Organizacion y Personas

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver | Si | Si | Si\* | Si | Si\* | Si\* | Si\* | Si | Si\* | Si\* | - | Si\* |
| Crear (organizacion, usuario, rol personalizado) | Si | Si\* (solo invita, si ademas tiene Administrador) | No | No | No | No | No | No | No | No | - | No |
| Modificar (datos societarios, rol de un usuario) | Si | No | No | No | No | No | No | No | No | No | - | No |
| Aprobar (cambio de rol sensible) | Doble | No | No | Si\* | No | No | No | No | No | No | - | No |
| Cerrar/archivar (suspender o dar de baja usuario, archivar sucursal) | Si | No | No | No | No | No | No | No | No | No | - | No |
| Exportar (listado de usuarios y roles) | Si | Si | No | Si | Si | No | No | Si | Si\* | No | - | No |
| Asignar (rol a un usuario) | Si | No | No | No | No | No | No | No | No | No | - | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | No | No | No | - | No |
| Adjuntar evidencia | Si | No | No | Si | No | No | No | No | No | No | - | No |

Nota especifica del modulo: el Titular no tiene ninguna visibilidad de la estructura interna de la empresa (columna TIT = "-" en todas las filas), a diferencia del resto de modulos donde a veces conserva una fila propia.

#### MOD-002 Delegado / Responsable Interno de Datos

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver | Si | Si\* (su expediente) | Si | Si | No (solo dato publico) | No (solo dato publico) | Si | Si | Si\* | No (solo dato publico) | No (solo dato publico) | Si\* |
| Crear (registro de nombramiento) | Si | No | No | Si | No | No | No | No | No | No | No | No |
| Modificar (perfil/contacto propio) | No | Si\* | No | No | No | No | No | No | No | No | No | No |
| Aprobar (acta, reverificacion, cambio de tipo_rol) | Si\* | No | No | Si | No | No | Si | No | No | No | No | No |
| Cerrar/archivar (registrar cese) | Si | No | No | Si | No | No | Si | No | No | No | No | No |
| Exportar | Si | Si\* | No | Si | No | No | No | Si | Si\* | No | No | No |
| Asignar (sustituto o delegado comun) | Si | No | No | No | No | No | Si | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | No | No | Si | No | No | No | No | Si\* |
| Adjuntar evidencia (atestados, credencial, informes) | Si | Si | No | Si | No | No | No | No | No | No | No | No |

Nota especifica del modulo: existe ademas la accion "registrar atencion de una peticion canalizada por el Delegado", exclusiva de SEG y ARE (Si), sin equivalente en el resto de modulos.

#### MOD-003 Onboarding

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver (wizard en curso o su historial) | Si | - | - | - | - | - | - | Si\* (solo historial) | No | No | - | No |
| Crear (organizacion, usuarios, respuestas) | Si | No | No | No | No | No | No | No | No | No | - | No |
| Modificar (mientras EN_PROGRESO) | Si | No | No | No | No | No | No | No | No | No | - | No |
| Aprobar | - | - | - | - | - | - | - | - | - | - | - | - |
| Cerrar/archivar (confirmar y finalizar; retirar invitacion pendiente) | Si | No | No | No | No | No | No | No | No | No | - | No |
| Exportar (resumen de configuracion inicial) | Si | No | No | No | No | No | No | Si | No | No | - | No |
| Asignar (rol a usuario invitado) | Si | No | No | No | No | No | No | No | No | No | - | No |
| Comentar | - | - | - | - | - | - | - | - | - | - | - | - |
| Adjuntar evidencia | - | - | - | - | - | - | - | - | - | - | - | - |

Nota especifica del modulo: MOD-003 no tiene flujo de aprobacion ni hilos de comentarios propios (es autoservicio de una sola sesion del Administrador); las filas "Aprobar", "Comentar" y "Adjuntar evidencia" no aplican a ningun rol.

### ETAPA 2: DIAGNOSTICAR Y ETAPA 3: PLANIFICAR

#### MOD-004 Diagnostico de Cumplimiento

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver resultado completo | Si | Si | - | Si | Si\* | Si\* | Si | Si\* (lectura) | Si\* (lectura) | - | - | Si\* |
| Crear (iniciar sesion) | Si | Si | - | No | No | No | No | No | No | - | - | No |
| Modificar (responder) | Si | Si | - | No | Si\* | Si\* | No | No | No | - | - | No |
| Aprobar (cierre cuando hay accion critica) | Si | Si | - | Doble | No | No | Doble | No | No | - | - | No |
| Cerrar/archivar (cerrar sesion / archivar) | Si | Si | - | No | No | No | No | No | No | - | - | No |
| Exportar | Si | Si | - | Si | No | No | No | Si\* | Si\* | - | - | No |
| Asignar (bloques a responsables) | Si | Si | - | No | No | No | No | No | No | - | - | No |
| Comentar | Si | Si | - | Si | Si\* | Si\* | No | No | No | - | - | Si\* |
| Adjuntar evidencia | Si | Si | - | No | Si\* | Si\* | No | No | No | - | - | No |

#### MOD-005 Plan de Cumplimiento

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver | Si | Si | Si\* | Si | Si\* | Si\* | Si | Si\* (lectura) | Si\* (lectura) | Si\* | - | Si\* |
| Crear (generar/recalcular el plan) | Si | Si | No | No | No | No | No | No | No | No | - | No |
| Modificar (campos de una accion, reclasificar prioridad) | Si | Si | No | Si | No | No | No | No | No | No | - | No |
| Aprobar (version Vigente) | No (propone) | No (propone) | No | No | No | No | Si | No | No | No | - | No |
| Cerrar/archivar (completar accion propia; archivar version) | Si | Si\* | Si\* | Si\* | Si\* | Si\* | No | No | No | Si\* | - | No |
| Exportar | Si | Si | No | Si | No | No | Si | Si | Si\* | No | - | No |
| Asignar (responsable de una accion) | Si | Si | No | Si | No | No | No | No | No | No | - | No |
| Comentar | Si | Si | Si\* | Si | Si\* | Si\* | Si | Si\* (lectura) | No | Si\* | - | Si\* |
| Adjuntar evidencia | Si | Si | Si\* | Si | Si\* | Si\* | No | No | No | Si\* | - | No |

### ETAPA 4: REGISTRAR

#### MOD-006 RAT y Mapa de Datos

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver RAT completo | Si | Si | Si\* (lectura) | Si | Si\* | No (solo su area) | Si | Si\* (lectura) | Si\* (exportado) | No | - | Si\* |
| Crear ficha de tratamiento | Si | Si | No | Si | No | Si\* | No | No | No | No | - | No |
| Modificar (Borrador/En revision) | Si | Si | No | Si | Si\* | Si\* | No | No | No | No | - | No |
| Aprobar (paso a Vigente) | No\* | Si | No | Si\* | No | No | Si | No | No | No | - | No |
| Cerrar/archivar (archivar tratamiento; eliminar solo Borrador sin historial) | Si | Si | No | Si | No | No | No | No | No | No | - | No |
| Exportar (RAT / paquete de evidencia) | Si | Si | No | Si | No | No | No | Si | Si\* | No | - | No |
| Asignar (tarea de completar campo) | Si | Si | No | Si | No | No | No | No | No | No | - | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | No | No | No | - | Si\* |
| Adjuntar evidencia | Si | Si | No | Si | Si | Si | Si | No | No | No | - | Si\* |

Nota especifica del modulo: dar de alta un sistema en el Catalogo de Sistemas es exclusivo de ADM y SEG (Si); el Titular nunca tiene acceso a este modulo (el Mapa de Datos nunca es visible desde MOD-012).

#### MOD-007 Consentimiento

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver | Si | Si | Si | Si | Si\* | Si\* | Si | Si\* (lectura) | Si\* (lectura, temporal) | Si\* | No (sin pantalla propia en MVP) | Si\* |
| Crear (registrar consentimiento) | No | Si | Si | No | Si\* | Si\* | No | No | No | No | No | No |
| Modificar (antes de vigente) | No | Si | Si | No | Si\* | Si\* | No | No | No | No | No | No |
| Aprobar (plantilla o notificacion) | No | Si | No | Si\* | No | No | Si\* | No | No | No | No | No |
| Cerrar/archivar (cerrar revocacion; el registro es append-only, nadie elimina) | No | Si | Si | No | No | No | No | No | No | No | No | No |
| Exportar | Si\* | Si | Si | Si | No | No | No | Si | Si\* | No | No | No |
| Asignar (tarea de captura o revocacion) | Si | Si | Si | No | No | No | No | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | No | No | No | No | Si\* |
| Adjuntar evidencia (firma, documento) | No | Si | Si | No | Si | Si | No | No | No | Si\* | No | No |

#### MOD-008 Documentos y Politicas

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver documentos publicados | Si | Si | Si\* | Si | Si | Si\* | Si | Si | Si\* | Si\* | Si\* (el Aviso publicado, fuera del modulo) | Si\* |
| Crear (documento o nueva version) | Si | Si | No | Si | No | No (solicita) | No | No | No | No | - | No |
| Modificar (editar borrador) | Si | Si | No | Si | No | No | No | No | No | No | - | No |
| Aprobar / publicar (segun cadena) | Si\* | Si\* | No | Si\* | No | No | Si | No | No | No | - | No |
| Cerrar/archivar (Aviso o Politica de Privacidad: doble aprobacion) | Si\* | Doble | No | No | No | No | No | No | No | No | - | No |
| Exportar (paquete con hash) | Si | Si | No | Si | No | No | No | Si | Si\* | No | - | No |
| Asignar (tarea de revision) | Si | Si | No | Si | No | No | No | No | No | No | - | No |
| Comentar | Si | Si | No | Si | Si | Si | No | No | No | No | - | Si\* |
| Adjuntar evidencia de publicacion | Si | Si | No | Si | No | No | No | No | No | No | - | No |

#### MOD-009 Proveedores y Encargados

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver | Si | Si | Si\* | Si | Si | Si\* | Si\* | Si\* (lectura) | Si\* (acotado) | Si\* | - | Si\* |
| Crear (alta) | Si | Si | No | Si | No | Si | No | No | No | No | - | No |
| Modificar | Si | Si | No | Si | Si\* | Si\* | No | No | No | No | - | No |
| Aprobar (activacion; doble control si riesgo alto o pais distinto de El Salvador) | No\* | Si | No | Si | No | No | Si | No | No | No | - | No |
| Cerrar/archivar (nunca eliminar, solo archivar con justificacion) | No\* | No\* | No | No | No | Si\* (propone) | No | No | No | No | - | No |
| Exportar | Si | Si | No | Si | Si\* | No | No | Si | Si\* | No | - | No |
| Asignar | Si | Si | No | No | No | No | No | No | No | No | - | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si | - | Si |
| Adjuntar evidencia | Si | Si | Si\* | Si | Si | Si | No | No | No | Si\* | - | No |

#### MOD-010 Transferencias Internacionales

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver | Si | Si | Si\* | Si | Si | Si\* | Si | Si\* (lectura) | Si\* (lectura) | No | No | Si\* |
| Crear (transferencia manual) | No | Si | No | Si | Si\* | Si\* (borrador) | No | No | No | No | No | No |
| Modificar | No | Si | No | Si | Si\* | Si\* (su borrador) | No | No | No | No | No | No |
| Aprobar (paso a ACTIVA; puesta en conocimiento a la ACE) | No | Si\* (ejecuta) | No | No\* | No | No | Doble | No | No | No | No | No |
| Cerrar/archivar (suspender; archivar, nunca eliminar) | No | Si | No | Si | No | No | Si | No | No | No | No | No |
| Exportar | Si | Si | No | Si | No | No | No | Si | Si\* | No | No | No |
| Asignar | Si | Si | No | Si | No | No | No | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | No (lectura) | No | Si\* | No | Si |
| Adjuntar evidencia | Si | Si | No | Si | Si | Si\* | No | No | No | Si\* | No | Si |

### ETAPA 5: OPERAR

#### MOD-011 ARCO-POL

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver (todos los expedientes / el propio para TIT) | Si | Si | Si | Si | Si\* (lectura) | No | Si\* (lectura) | Si\* (lectura) | Si\* (invitacion) | No | Si\* (solo el suyo) | Si\* |
| Crear (registrar solicitud nueva) | Si | Si | Si | No | No | No | No | No | No | No | Si\* (la presenta) | No |
| Modificar (verificar identidad; redactar borradores) | No | No | Si | Si\* (revision) | No | No | No | No | No | No | No | No |
| Aprobar (prevencion, incompetencia, resolucion final) | No | Si | No | No | No | No | Si\* (segundo revisor si aplica) | No | No | No | No | No |
| Cerrar/archivar (cerrar expediente; archivado automatico por vencimiento de retencion) | No | Si | Si\* (propone) | No | No | No | No | No | No | No | No | No |
| Exportar (expediente / paquete de evidencia) | Si | Si | Si | Si | No | No | No | Si | Si\* | No | No | No |
| Asignar (responsable / reasignar) | Si | Si | No | No | No | No | No | No | No | No | No | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | No | No | Si\* | No | Si\* |
| Adjuntar evidencia | Si | Si | Si | Si | Si | Si\* | No | No | No | Si\* | Si\* (en su solicitud) | No |

Nota especifica del modulo: **eliminar un expediente o su historial no existe como accion para ningun rol** (solo archivado por vencimiento de retencion, ejecutado por el sistema con aprobacion del Administrador). Reabrir por reclamo ante la ACE: DEL Si, LEG Si, resto No.

#### MOD-012 Portal del Titular

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver (Aviso/Politica publicados; configuracion) | Si | Si\* (lectura) | Si\* (lectura) | Si\* (lectura) | Si | - | Si\* (lectura) | Si\* (lectura) | Si\* (lectura) | - | Si | - |
| Crear (presentar solicitud ARCO-POL; adjuntar identidad) | No | No | No | No | No | - | No | No | No | - | Si | - |
| Modificar (configuracion del Portal) | Si | No | No | No | Si\* | - | No | No | No | - | No | - |
| Aprobar (activacion o cambio sensible) | No | Si | No | Si | No | - | Si | No | No | - | No | - |
| Cerrar/archivar (acceso de consulta vencido; purgar segun retencion) | Si | No | No | No | Si | - | No | No | No | - | No | - |
| Exportar (reporte de accesos o solicitudes) | Si | Si | Si | Si | Si | - | No | Si | Si\* | - | No | - |
| Asignar (se ejecuta dentro de MOD-011) | No | No | Si | No | No | - | No | No | No | - | No | - |
| Comentar | - | - | - | - | - | - | - | - | - | - | - | - |
| Adjuntar evidencia | - | - | - | - | - | - | - | - | - | - | - | - |

Nota especifica del modulo: el Responsable de area y el Asesor externo no interactuan directamente con el Portal (columna "-"); solo el propio Titular, mientras su solicitud siga en Borrador sin enviar, puede corregir sus propios datos.

#### MOD-013 Incidentes de Seguridad

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver | Si | Si | - | Si | Si | Si\* (si reporto o le asignaron) | Si\* (si le corresponde aprobar) | Si\* (lectura) | Si\* (invitado a un periodo) | Si\* | - | Si\* |
| Crear (reportar incidente) | Si | Si | - | Si | Si | Si | No | No | No | No | - | No |
| Modificar (datos del expediente) | No | Si\* | - | Si\* | Si | No | No | No | No | No | - | No |
| Aprobar (notificacion a ACE/FGR/titulares) | No | Si | - | Si\* (co-revisa) | No (prepara borrador) | No | No | No | No | No | - | No |
| Cerrar/archivar (nunca se elimina, solo se archiva tras retencion vencida) | No | Si | - | Si | Si\* (si bajo el umbral) | No | Si\* (segunda firma si sobre el umbral) | No | No | No | - | No |
| Exportar | Si | Si | - | Si | Si | No | No | Si | Si\* | No | - | Si\* (solo su caso) |
| Asignar (tareas del incidente) | Si | Si | - | Si | Si | No | No | No | No | No | - | No |
| Comentar | Si | Si | - | Si | Si | Si\* | Si | No | No | Si\* | - | Si\* |
| Adjuntar evidencia | No | Si | - | Si | Si | Si\* | No | No | No | Si\* | - | Si\* |

Nota especifica del modulo: el Titular no tiene acceso a este modulo (solo recibe la notificacion externa, OBL-INC-03); ninguna norma exige que dos personas distintas gestionen y cierren un incidente, pero toda decision de cierre debe dejar evidencia de quien decidio, cuando y con que fundamento (OBL-INC-04, Art. 25 inciso final).

#### MOD-014 Riesgos y EIPD

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver | Si | Si | Si\* (si relacionado) | Si | Si | Si\* (su area) | Si | Si | Si\* (asignado) | - | - | Si\* |
| Crear (EIPD manual, fuera del disparo automatico) | Si | Si | No | Si | No | Si\* | No | No | No | - | - | No |
| Modificar (completar cuestionario, registrar mitigacion) | No | Si | No | No | Si\* (tecnica) | Si\* (no tecnica) | No | No | No | - | - | No |
| Aprobar (pasar a Vigente; riesgo residual aceptado) | No | Si\* (salvo doble control) | No | Si\* (corresponsable en riesgo Alto/Critico) | No | No | Si | No | No | - | - | No |
| Cerrar/archivar (nadie elimina, solo archiva) | No | Si | No | No | No | No | Si | No | No | - | - | No |
| Exportar | Si | Si | No | Si | No | No | Si | Si | Si\* | - | - | No |
| Asignar (tarea de mitigacion) | No | Si | No | No | Si | No | No | No | No | - | - | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | Si | Si | - | - | Si\* |
| Adjuntar evidencia | No | Si | No | Si | Si | Si\* | No | No | No | - | - | Si\* |

Nota especifica del modulo: cuando el riesgo calculado es Alto o Critico, quien completo el cuestionario nunca puede ser quien da la aprobacion final (doble control sin excepcion de tamano de empresa para este paso, ver 11.3).

#### MOD-015 Controles de Seguridad

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver (catalogo completo) | Si | Si | - | Si | Si | Si\* (su area) | Si | Si\* (lectura) | Si\* (lectura, temporal) | - | - | Si\* |
| Crear (control) | Si | No | - | No | Si | No | No | No | No | - | - | No |
| Modificar / marcar Implementado | Si | No | - | No | Si | No | Si\* (si el control lo exige) | No | No | - | - | No |
| Aprobar (excepcion "No aplica") | Si\* (con advertencia si la creo) | No | - | Si | No | No | Si | No | No | - | - | No |
| Cerrar/archivar (nunca eliminar) | Si | No | - | No | Si | No | No | No | No | - | - | No |
| Exportar | Si | Si | - | Si | Si | No | No | Si | Si\* | - | - | No |
| Asignar (tarea derivada) | Si | No | - | No | Si | No | No | No | No | - | - | No |
| Comentar | Si | Si | - | Si | Si | Si\* | Si | Si | Si | Si\* | - | Si\* |
| Adjuntar evidencia | Si | No | - | No | Si | Si\* | No | No | No | Si\* | - | Si\* |

#### MOD-016 Retencion y Eliminacion

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver (reglas e inventario) | Si | Si | Si\* (estado del dato consultado) | Si | Si\* (tecnicas de su area) | Si\* (su area) | Si | Si\* (lectura) | Si\* (invitado) | Si\* (su tarea) | - | Si\* |
| Crear (regla) | Si (config general) | Si | No | Si | No | No | No | No | No | No | - | No |
| Modificar (plazo, fundamento) | Si (con motivo) | Si | No | Si | No | No | No | No | No | No | - | No |
| Aprobar (regla nueva o eliminacion) | No\* | Si | No | Doble (excepciones documentales, siempre) | No | No | Si | No | No | No | - | No |
| Cerrar/archivar (confirmar ejecucion tecnica) | No | Si | No | No | Si | Si | No | No | No | Si\* | - | No |
| Exportar | Si | Si | No | Si | No | No | No | Si | Si\* | No | - | No |
| Asignar (tarea de revision/ejecucion) | Si | Si | No | Si | No | No | No | No | No | No | - | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si | - | Si |
| Adjuntar evidencia de eliminacion | No | Si | No | No | Si | Si | No | No | No | Si\* | - | No |

Nota especifica del modulo: toda excepcion de eliminacion anticipada de un documento de cumplimiento (OBL-RET-04/05) exige doble aprobacion (Delegado y Responsable Legal) sin excepcion de tamano de empresa.

#### MOD-017 Capacitacion

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver (segun alcance del rol) | Si | Si | Si\* (su capacitacion por rol) | Si | Si\* | Si\* (su area) | Si | Si\* (lectura) | Si\* (invitado) | Si\* (lo propio) | - | Si\* |
| Crear (programa: General, Induccion, Por rol) | Si (config general) | Si | No | Si | Si\* (tecnicos) | No | No | No | No | No | - | No |
| Elaborar/editar el Plan anual | No\* | Si | No | Si\* (co-edicion) | No | No | No | No | No | No | - | No |
| Aprobar / publicar el Plan anual | No | Si\* (propone) | No | No | No | No | Si | No | No | No | - | No |
| Cerrar/archivar (registrar asistencia propia; archivar programa) | Si\* | Si | Si\* | Si\* | Si\* | Si\* | No | No | No | Si\* | - | No |
| Exportar | Si | Si | No | Si | Si\* | Si\* | Si | Si | Si\* | No | - | No |
| Asignar (programar induccion o capacitacion por rol) | Si | Si | No | Si | Si\* | Si\* | No | No | No | No | - | No |
| Comentar | Si | Si | Si | Si | Si | Si | Si | Si | Si\* | Si\* | - | Si\* |
| Adjuntar evidencia (constancia, acuse) | Si | Si | Si\* | Si | Si\* | Si\* | No | No | No | Si\* | - | No |

### ETAPA 6: DEMOSTRAR

#### MOD-018 Auditoria de Cumplimiento

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver (lista y detalle) | Si | Si | - | Si | Si\* | - | Si | Si\* (lectura) | Si\* (invitado) | No (salvo su tarea) | - | Si\* |
| Crear / planificar auditoria | Si | Si | - | Si | No | - | No | No | No | No | - | No |
| Modificar (alcance, fechas, tipo antes de ejecutar) | Si | Si | - | Si | No | - | No | No | No | No | - | No |
| Aprobar ("riesgo aceptado" en vez de corregir un hallazgo) | Si\* (pyme) | No | - | No | No | - | Si | No | No | No | - | No |
| Cerrar/archivar (informe final; cancelar planificada) | Si\* (pyme) | Si\* (cancela) | - | No\* | No | - | Si | No | No | No | - | No |
| Exportar | Si | Si | - | Si | Si\* | - | Si | Si | Si\* | No | - | No |
| Asignar (responsable de accion correctiva) | Si | Si | - | Si | No | - | No | No | No | No | - | No |
| Comentar | Si | Si | - | Si | Si\* | - | Si | Si | Si\* | Si\* | - | Si\* |
| Adjuntar evidencia (registrar/editar hallazgo) | Si\* (pyme) | Si | - | Si | Si\* | - | No | No | Si\* (su propio informe) | Si\* | - | Si\* |

#### MOD-019 Centro de Evidencias

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver (evidencia por obligacion, modulo o periodo; huecos de evidencia) | Si | Si | Si\* (sus expedientes) | Si | Si\* (sus controles) | Si\* (su area) | Si | Si\* (lectura) | Si\* (paquete invitado) | No | - | Si\* |
| Crear (cargar evidencia suelta; generar EvidencePackage borrador) | Si | Si | Si\* | Si | Si\* | No | No | No | No | Si\* (su tarea) | - | No |
| Modificar (marcar vigente/renovada) | No | Si | No | No | Si\* | No | No | No | No | No | - | No |
| Aprobar (evidencia cargada; exportacion con destino interno) | No\* | Si | No | Si | No | No | Si | No | No | No | - | No |
| Aprobar exportacion con destino externo (doble control obligatorio, sin excepcion pyme) | No\* | Si (primer control) | No | Si (primer control) | No | No | Si (segundo control) | No | No | No | - | No |
| Cerrar/archivar (nunca eliminar) | Si | Si | No | Si | No | No | No | No | No | No | - | No |
| Exportar / descargar paquete ya aprobado | Si | Si | Si\* | Si | Si\* | No | Si | Si | Si\* (el suyo) | No | - | No |
| Asignar | - | - | - | - | - | - | - | - | - | - | - | - |
| Comentar | Si | Si | Si | Si | Si | Si | Si | Si | Si\* | Si\* | - | Si\* |

#### MOD-020 Dashboard y Reportes

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver perspectiva Gerencia | Si | Si\* (lectura) | No | Si\* (lectura) | No | No | No | Si\* (lectura) | No | No | - | No |
| Ver perspectiva Responsable (la propia) | Si | Si | Si\* | Si\* | Si\* | Si\* (su area) | Si\* (aprobaciones) | Si\* (lectura) | No | Si\* (vista reducida) | - | No |
| Ver perspectiva Legal/Delegado (8 clusters legales) | Si | Si | No | Si | No | No | No | Si\* (lectura) | No | No | - | No |
| Ver perspectiva Auditor (evidencia, huecos, vencimientos) | Si | Si\* | No | Si\* | No | No | No | Si | Si\* (acotado) | No | - | Si\* (su caso) |
| Crear / modificar / eliminar registro desde un indicador | No (redirige al modulo de origen) | No | No | No | No | No | No | No | No | No | - | No |
| Exportar reporte | Si | Si | Si\* | Si | Si\* | No | No | Si | Si\* (acotado) | No | - | No |
| Exportar Informe para Junta Directiva | Si | Si\* | No | No | No | No | No | No | No | No | - | No |
| Configurar umbrales, sucursales/unidades, calendario de fotos | Si | No | No | No | No | No | No | No | No | No | - | No |

Nota especifica del modulo: "Junta Directiva" no es un rol del sistema, es solo un destinatario de un reporte exportado (ver seccion 11.9); MOD-020 no crea ni aprueba ningun registro de negocio, la separacion de funciones sustantiva ya esta resuelta en el modulo de origen de cada indicador.

### CAPA TRANSVERSAL

#### MOD-021 Centro de Tareas

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver | Si | Si | Si\* | Si\* | Si\* | Si\* | Si\* | Si (lectura) | Si\* (lectura, temporal) | Si\* | - (ve su solicitud via MOD-011) | Si\* |
| Crear (tarea manual) | Si | Si | Si\* | Si | Si\* | Si\* | No | No | No | No | - | No |
| Modificar (titulo, fecha, responsable) | Si | Si\* | Si\* | Si\* | Si\* | Si\* (no legales) | No | No | No | No | - | No |
| Aprobar (Approval) | Doble | Si\* (solo actos DEL) | No | Si\* | No | No | Si\* | No | No | No | - | Si\* (caso invitado) |
| Cerrar/archivar (completar; archivar "no aplica" tras cambio de regimen, solo automatico) | Si | Si\* | Si\* | Si\* | Si\* | Si\* | No | No | No | Si\* | - | No |
| Exportar | Si | Si\* | Si\* | Si\* | Si\* | No | No | Si | Si\* | No | - | No |
| Asignar / reasignar | Si | Si\* | Si\* | Si\* | Si\* | No | No | No | No | No | - | No |
| Comentar | Si | Si | Si\* | Si | Si\* | Si\* | Si\* | No | No | Si\* | - | Si\* |
| Adjuntar evidencia | Si | Si | Si\* | Si | Si\* | Si\* | Si\* | No | No | Si\* | - | Si\* |

Nota especifica del modulo: **eliminar no existe para ningun rol** (solo archivar; el historial nunca se borra, `22_anti_features.md` item 19).

#### MOD-022 Notificaciones

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver (propias) | Si | Si | Si | Si | Si | Si | Si | Si (todas, lectura) | Si\* (acotado) | Si\* | - (su comunicacion vive en MOD-011/012) | Si\* |
| Crear regla de notificacion | Si | No | No | No | No | No | No | No | No | No | - | No |
| Modificar regla no obligatoria | Si | Si\* (su ambito) | No | No | No | No | No | No | No | No | - | No |
| Modificar el piso minimo de alertas de plazos legales | No (bloqueado por diseno) | No | No | No | No | No | No | No | No | No | - | No |
| Aprobar (ampliar/reducir umbral de escalamiento CRITICAL en curso, doble control) | Doble (propone) | Doble | No | Doble | No | No | No | No | No | No | - | No |
| Cerrar/archivar (automatico al completar el ciclo, ningun rol lo hace manualmente) | - | - | - | - | - | - | - | - | - | - | - | - |
| Exportar (reporte de notificaciones) | Si | Si\* | Si\* | Si\* | Si\* | No | No | Si | Si\* | No | - | No |
| Asignar | - | - | - | - | - | - | - | - | - | - | - | - |
| Comentar | - (no tiene hilo propio, vive en la tarea de MOD-021) | - | - | - | - | - | - | - | - | - | - | - |
| Adjuntar evidencia (constancia de aviso fallido) | Si | Si\* | Si\* | No | No | No | No | No | No | No | - | No |

#### MOD-023 Calendario y Motor de Plazos

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver calendario vigente y desglose de un calculo | Si | Si | Si\* | Si | Si\* | Si\* (su area) | Si\* | Si (lectura) | Si\* (lectura) | Si\* | No (ve dias restantes via MOD-012) | Si\* |
| Configurar calendario nacional base, asuetos ad hoc, calendario de la autoridad | No (lo mantiene el equipo del producto, no un rol de la organizacion cliente) | No | No | No | No | No | No | No | No | No | - | No |
| Configurar asuetos locales por sede / calendario propio de la empresa | Si | No | No | No | No | No | No | No | No | No | - | No |
| Aprobar (cambiar criterio de computo por defecto en plazo ambiguo) | No (solo lo solicita) | Doble | No | Doble | No | No | Si\* (si designado segundo revisor) | No | No | No | - | No |
| Cerrar/archivar (nadie elimina un calculo o calendario, solo se archiva como historico) | - | - | - | - | - | - | - | - | - | - | - | - |
| Exportar (reporte de calendario / historial de calculos) | Si | Si | No | Si | Si | No | No | Si | Si\* | No | - | No |
| Comentar (nota sobre fuente dudosa) | Si | Si | No | Si | No | Si\* | No | No | No | No | - | No |
| Adjuntar evidencia (decreto, comunicado, aviso oficial) | Si | No | No | No | No | Si\* (su sucursal) | No | No | No | No | - | No |

#### MOD-024 Centro Regulatorio

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver marco normativo y catalogo de infracciones (informativo) | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si | - | Si\* |
| Ver expediente de un procedimiento sancionador propio | Si | Si | No\* | Si | Si\* | No | Si | Si | Si\* (temporal) | No | - | Si\* |
| Crear expediente de procedimiento sancionador | Si | No | No | Si | No | No | No | No | No | No | - | No |
| Redactar/editar contestacion, pruebas y decisiones | No | Colabora | No | Si | Colabora | No | No | No | No | No | - | Colabora |
| Aprobar y enviar contestacion, recurso o tramite ante la ACE (doble control) | Si\* | No | No | Si | No | No | Si | No | No | No | - | No |
| Cerrar/archivar (nunca eliminar historial) | Si | No | No | Si | No | No | Si | No | No | No | - | No |
| Exportar (paquete de evidencia del expediente) | Si | Si\* | No | Si | No | No | No | Si | Si\* | No | - | No |
| Confirmar "toma de conocimiento" de un cambio normativo | Si | Si | Si | Si | Si | Si | Si | No | No | No | - | No |
| Recomendar (no activar) el cambio de bandera regimen_reforma_659 | No | No | No | Si | No | No | No | No | No | No | - | No |
| Comentar | Si | Si | Si | Si | Si | No | Si | No | No | No | - | Si\* |
| Adjuntar evidencia | Si | Si | No | Si | Si\* | No | No | No | No | No | - | Si\* |

Nota especifica del modulo: **ningun rol de la organizacion cliente edita la bandera `regimen_reforma_659` ni el contenido versionado del marco normativo**; eso lo hace exclusivamente el "Editor de contenido regulatorio" del proveedor del software (ver 11.7). Responsable Legal solo puede recomendar, nunca activar el cambio de estado.

#### MOD-025 Busqueda Global

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver (ejecutar una busqueda) | Si | Si | Si | Si | Si | Si | Si | Si | Si\* (acotado) | Si | No (usa el buscador propio de MOD-012) | Si\* |
| Ver expedientes ARCO-POL por nombre del titular | Si | Si | Si | Si\* | No | No | No | No | No | No | No | No |
| Crear, modificar o eliminar un registro desde un resultado | No (redirige siempre al modulo de origen) | No | No | No | No | No | No | No | No | No | - | No |
| Exportar listado de resultados | No (no existe exportacion propia; se exporta desde el modulo de origen) | No | No | No | No | No | No | No | No | No | - | No |
| Configurar sinonimos y catalogo de busqueda | Si | No | No | No | No | No | No | No | No | No | - | No |
| Consultar el registro de consultas de busqueda (Search Log) | Si\* (con justificacion) | No | No | No | No | No | No | Si (lectura, evidencia de minimizacion) | No | No | - | No |

Nota especifica del modulo: toda separacion de funciones relevante ya esta resuelta en el modulo de origen del resultado; MOD-025 no crea, aprueba ni cierra nada.

#### MOD-026 Centro de Ayuda

| Accion | ADM | DEL | ARC | LEG | SEG | ARE | APR | AUI | AUE | COL | TIT | ASE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver (tarjeta de ayuda y Glosario) | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si | Limitado (solo 2 conceptos embebidos en MOD-012) | Si\* |
| Buscar dentro del Centro de Ayuda | Si | Si | Si | Si | Si | Si | Si | Si | Si | Si | No | Si\* |
| Crear / modificar / aprobar (publicar) un articulo | No (ningun rol de la organizacion cliente; ver 11.7) | No | No | No | No | No | No | No | No | No | No | No |
| Exportar (Glosario o catalogo por modulo en PDF) | Si | Si | Si | Si | Si | Si | Si | Si | Si\* (lectura) | Si | - | Si\* |
| Comentar (retroalimentacion "fue util / no fue util") | Si | Si | Si | Si | Si | Si | Si | No (protege su independencia) | No | Si | No | Si\* |

---

