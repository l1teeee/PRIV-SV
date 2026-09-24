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

## 11.3 Separacion de funciones y doble control

Regla general (`05_tipos_de_usuario.md`, seccion 5.4): el rol Auditor (interno o externo) es siempre de solo lectura en los 26 modulos, sin excepcion; nunca coincide con quien carga evidencia, aprueba o cierra la accion que audita. Por debajo de un umbral configurable de tamano de empresa (propuesta inicial: 50 empleados, **[opinion de producto, umbral sin respaldo legal expreso]**), el sistema permite que una misma persona acumule roles que en empresa mediana o corporativo estarian separados, pero siempre muestra una advertencia visible de "autorrevision"; por encima del umbral, el sistema bloquea la acumulacion para las combinaciones marcadas como "sin excepcion de tamano" en la tabla siguiente. Ninguna de las dos filas de "Eliminar" existe realmente en el sistema: los 26 modulos son de historial append-only (archivar, nunca eliminar un registro con historial), conforme al anti-feature 19 de `22_anti_features.md`.

Catalogo de acciones que exigen doble control o que quien las creo no puede aprobar, por modulo:

| Modulo | Accion | Quien no puede aprobar lo que creo / quien exige segunda firma | Justificacion | Excepcion de tamano (pyme) |
|---|---|---|---|---|
| MOD-001 | Cambio de rol propio del Administrador | El Administrador no se aprueba a si mismo; exige un segundo Administrador o el Responsable Legal | Control de acceso al modulo que gobierna todos los demas | No hay excepcion: si no existe un segundo Administrador, decide el Responsable Legal |
| MOD-001 | Cambio de rol a Aprobador o Auditor por encima del umbral | Quien crea o modifica el rol no puede ser quien lo aprueba | Evitar que una sola persona se autoasigne un rol de control | Si, con advertencia de autorrevision por debajo del umbral |
| MOD-002 | Aprobar el acta de nombramiento del Delegado y cada reverificacion periodica | Quien registro el nombramiento (Administrador) no deberia ser el unico que lo aprueba en empresa mediana/corporativo | Investidura formal de la figura que hoy la ley exige (Arts. 15 y 17) | Si, con advertencia de autorrevision |
| MOD-002 | Aprobar el cambio de `tipo_rol` (mantener Delegado voluntariamente o migrar a Responsable Interno bajo el estado FUTURO) | Quien lo propone (Delegado o Administrador) no puede ser la unica firma; exige ademas Aprobador o Responsable Legal | Decision estrategica sobre el regimen aplicable a la empresa | No, doble control siempre |
| MOD-004 | Aprobar el cierre de una sesion de diagnostico con al menos una accion CRITICA | Segunda confirmacion (Legal/Compliance o Aprobador) distinta de quien respondio el cuestionario | El resultado alimenta directamente el Plan de Cumplimiento (MOD-005) | Si, se recomienda pero no se bloquea por debajo del umbral |
| MOD-005 | Aprobar una version del plan como "Vigente" | Quien genera o propone el plan (Administrador, Delegado) nunca es quien la aprueba; exige el rol Aprobador | El plan dispara tareas y compromisos con plazo legal | No, doble control siempre (con advertencia de autorrevision si el Aprobador coincide con quien propuso) |
| MOD-005 | Descartar una accion ligada a una obligacion OBLIGATORIO | Quien la propone (responsable o Delegado) y quien la valida (Legal o Delegado, si no fue quien la propuso) | Evitar que una obligacion legal se descarte sin segundo criterio | No, doble control siempre |
| MOD-006 | Aprobar el paso de una ficha de tratamiento de riesgo alto o con datos sensibles a "Vigente" | Quien la registro (Responsable de area) no puede aprobarla; exige Aprobador o Legal/Compliance | Evitar que una sola persona valide su propio registro de un tratamiento sensible | Si, con advertencia de autorrevision |
| MOD-006 | Exportar el RAT completo para auditoria | Exige rol Administrador, Delegado o Legal; nunca un Responsable de area por si solo | Evitar que una sola persona decida que se muestra a un auditor | No aplica excepcion (regla de rol, no de doble firma) |
| MOD-007 | Aprobar una plantilla de consentimiento reforzado (sensible, biometrico, parental) | Quien captura el consentimiento (Responsable de area, IT) no puede aprobar la plantilla que uso | Evitar que quien recolecta valide su propio instrumento de recoleccion | No indicado como excepcion pyme en la ficha |
| MOD-007 | Cierre de una revocacion con datos sensibles o riesgo de reclamo ante la ACE | Exige aprobacion explicita del Delegado/Responsable interno antes de notificar | El sistema nunca emite la notificacion de forma automatica | No aplica (regla de aprobacion humana, no de doble firma entre pares) |
| MOD-008 | Aprobar/publicar un Aviso de Privacidad o Politica de Privacidad | Quien redacta o edita el borrador no debe ser la unica persona que lo aprueba; exige un aprobador distinto del autor | Son los dos documentos que la ley exige tener siempre vigentes | Si, con advertencia de autorrevision |
| MOD-008 | Archivar un Aviso de Privacidad o Politica de Privacidad | Doble aprobacion (quien lo solicita y una segunda persona con rol Delegado/Responsable interno o Administrador) | Descontinuar estos documentos sin sustituto deja a la empresa sin el documento exigido | No, doble aprobacion siempre |
| MOD-009 | Aprobar la activacion de un proveedor de riesgo Alto | Quien ejecuta la evaluacion tecnica (Seguridad/IT) no puede ser quien aprueba (Aprobador o Delegado) | Evitar que quien evalua tecnicamente valide tambien la activacion | Si, con advertencia de autorrevision |
| MOD-010 | Aprobar el paso de una transferencia a ACTIVA y aprobar el envio de la puesta en conocimiento a la ACE | Quien crea o redacta (Legal/Compliance o Delegado) no aprueba; exige rol Aprobador; a partir del umbral, bloqueo total | El envio a la ACE y la activacion de un flujo internacional son actos de riesgo regulatorio | Si por debajo del umbral (con advertencia); bloqueo total por encima del umbral |
| MOD-011 | Aprobar y emitir la prevencion, la incompetencia, la resolucion final o la notificacion a receptores | Quien redacta el borrador (Responsable ARCO-POL) nunca es quien aprueba y emite (Delegado/Responsable interno), sin excepcion, ni siquiera en pyme (ahi exige una segunda confirmacion explicita del mismo usuario en dos roles distintos, con advertencia) | Todo acto legalmente atribuido hoy a la figura del Delegado (Arts. 15, 17-22) | No hay excepcion real: incluso en pyme se exige una segunda confirmacion explicita separada del guardado del borrador |
| MOD-011 | Escalar a un segundo revisor una denegatoria con datos sensibles o riesgo de reclamo ante la ACE | Aprobador como segundo revisor, distinto de quien resolvio | Denegatoria indebida es infraccion muy grave (Art. 56) | Disponible a partir de empresa mediana; en pyme queda como opcion |
| MOD-012 | Aprobar la activacion del Portal o el cambio del metodo de verificacion de identidad | Quien configura (Administrador) no deberia ser quien aprueba, a partir del umbral | Cambios de superficie de exposicion publica de datos | Si, con advertencia de autorrevision |
| MOD-013 | Cerrar un incidente investigado y gestionado por una sola persona | Exige segunda firma del Aprobador por encima del umbral | Ninguna norma exige dos personas, pero la decision de cierre debe quedar evidenciada (OBL-INC-04) | Si, con advertencia de autorrevision por debajo del umbral |
| MOD-013 | Aprobar la notificacion externa (ACE, FGR, titulares) | Exige accion explicita del Delegado/Responsable interno, distinta de quien redacto el borrador | El sistema nunca envia una notificacion externa sin esa aprobacion humana | No aplica excepcion de tamano (es aprobacion humana obligatoria, no doble firma de pares) |
| MOD-014 | Aprobar una EIPD de riesgo Alto o Critico | Quien completo el cuestionario y registro mitigaciones (Responsable de area o Seguridad/IT) no puede dar la aprobacion final; exige un segundo revisor (Aprobador) | No existe mandato legal expreso de "cuatro ojos", pero es la unica forma de que el riesgo residual no se autoapruebe | No, doble control siempre para riesgo Alto/Critico |
| MOD-015 | Aprobar una excepcion de control ("No aplica / Exceptuado") | Quien crea o adjunta la evidencia del control no debe ser la unica persona que aprueba la excepcion; exige Aprobador | Una excepcion mal justificada es la puerta de entrada al riesgo de infraccion grave (Art. 56 lit. b) | Si, con advertencia de autorrevision |
| MOD-016 | Aprobar una regla de retencion o una eliminacion | Exige Aprobador, distinto de quien la solicito | Evitar que la misma persona decida y ejecute la eliminacion de datos | Si, con advertencia de autorrevision |
| MOD-016 | Aprobar una excepcion de eliminacion anticipada de un documento de cumplimiento (OBL-RET-04/05) | Doble aprobacion siempre (Delegado y Responsable Legal) | Protege la capacidad probatoria minima del programa | No, doble control siempre, sin excepcion de tamano |
| MOD-017 | Aprobar/publicar el Plan anual de capacitacion | Exige un Aprobador distinto de quien lo elaboro (Delegado o Legal) | Separacion entre quien redacta el plan y quien lo valida | Si, con advertencia de autorrevision |
| MOD-018 | Aprobar el cierre de una auditoria (informe final) o un "riesgo aceptado" en vez de corregir un hallazgo | Exige Aprobador, distinto de quien registro los hallazgos (Delegado o Legal) | Sobre todo relevante cuando la auditoria encontro hallazgos criticos | Si, con advertencia de autorrevision |
| MOD-019 | Aprobar evidencia cargada manualmente antes de "Disponible" | Quien la carga no debe ser la unica persona que la aprueba | Integridad del Centro de Evidencias | Si, con advertencia de autorrevision |
| MOD-019 | Aprobar la exportacion de un EvidencePackage con destino externo a la organizacion | Doble control obligatorio: quien genera propone, y una segunda persona (Aprobador, o Delegado/Legal actuando como primer control) aprueba antes de que el archivo quede disponible | El riesgo de un envio irreversible a un tercero (ACE, auditor externo, cliente) es distinto del riesgo de una autorrevision interna | No, doble control siempre, sin excepcion de pyme para este paso especifico |
| MOD-021 | Aprobar (Approval) una tarea que la misma persona dejo en "En revision" | El sistema bloquea que el mismo usuario apruebe su propio trabajo | Regla general de separacion de funciones aplicada al motor transversal de tareas | Si, con advertencia de autorrevision |
| MOD-022 | Ampliar o reducir el umbral de escalamiento de una alerta CRITICAL ya en curso | El Administrador propone, requiere confirmacion de una segunda persona (Delegado/Responsable interno o Legal/Compliance) | Evitar que se relaje unilateralmente el escalamiento de un plazo legal critico (por ejemplo, las 72 horas) | No, doble control siempre |
| MOD-023 | Cambiar el criterio de computo por defecto de un plazo con ambiguedad juridica documentada (por ejemplo, horas corridas vs. habiles para las 72 horas) | Doble control entre Delegado/Responsable interno y Legal/Compliance (o un Aprobador designado); nunca lo decide el Administrador por si solo | Es la unica decision de este modulo con impacto legal directo sobre todos los casos abiertos de ese tipo | No, doble control siempre |
| MOD-024 | Aprobar y enviar cualquier tramite ante la ACE (contestacion, recurso, comprobante de pago, ACEFiling) | Quien redacta no puede ser la unica firma; exige Aprobador o un segundo Responsable Legal | Actos con efecto directo ante la autoridad sancionadora | Si por debajo del umbral (con advertencia); a partir de empresa mediana se exige segundo firmante |
| MOD-026 | Publicar un `HelpArticle` (fuera del RBAC de la organizacion cliente) | Quien redacta el contenido (autor) no puede ser quien lo revisa juridicamente, ni quien lo publica; tres roles distintos del equipo del proveedor | Protege al usuario final de recibir contenido sin revision juridica | No aplica al cliente: gobernanza interna del proveedor, ver 11.7 |

En todos los casos donde la tabla dice "Si, con advertencia de autorrevision" la mecanica es identica: por debajo del umbral configurable de tamano de empresa, el sistema permite que una misma persona ocupe ambos roles de la cadena, pero muestra siempre una advertencia visible de "autorrevision" y dicha advertencia queda registrada en el historial de la accion (no es una advertencia silenciosa). Ninguna fila de la tabla anterior habilita eliminar un registro: "aprobar" o "cerrar" siempre significa cambiar de estado con historial preservado, nunca borrar.

**Modo pyme: acumulacion de roles con advertencia de autorrevision y umbral de separacion de funciones.** El umbral propuesto (50 empleados) y el propio mecanismo de advertencia visible en vez de bloqueo duro son, en conjunto, **[opinion de producto, sin respaldo legal expreso, `05_tipos_de_usuario.md` seccion 5.4 y notas finales de MOD-001]**. Debajo del umbral, la pyme tipica (perfil Karla Hernandez, `05_tipos_de_usuario.md` seccion 5.1) opera con una sola persona ocupando Administrador, Delegado y, con frecuencia, tambien Aprobador; el sistema no le impide operar, pero en cada accion de la tabla anterior que le corresponda aprobar sobre su propio trabajo, muestra el texto de advertencia y dicha aprobacion queda marcada como "autorrevision" en el historial y en los reportes de auditoria (MOD-018) y de evidencia (MOD-019), para que un auditor externo o la propia ACE puedan identificarla sin ambiguedad. Al cruzar el umbral configurable, el Administrador recibe la alerta "Umbral de separacion de funciones alcanzado" (MOD-001, seccion I) y debe activar explicitamente el bloqueo, o dejar registrada su decision de mantenerlo desactivado.

---

## 11.4 Roles personalizados, suplencias y ausencias, alta y baja de usuarios, revision periodica de accesos

### 11.4.1 Roles personalizados

Fuente: `MOD-001_ficha.md`, seccion D.3. Cuando los 12 roles estandar no dan suficiente granularidad (tipico en empresa mediana o corporativo), el Administrador puede crear un rol personalizado con estos campos:

| Campo | Que permite | Que no permite |
|---|---|---|
| Nombre del rol | Texto libre, unico dentro de la cuenta (por ejemplo, "Coordinador de Marketing Digital") | No puede duplicar el nombre de uno de los 12 roles estandar |
| Basado en rol estandar (opcional) | Tomar como punto de partida los permisos de uno de los 12 roles estandar y ajustarlos | No cambia el nombre ni el proposito del rol estandar original; el rol estandar sigue existiendo aparte |
| Permisos por modulo y por accion | Marcar exactamente que puede ver y hacer esa persona en cada modulo, con el mismo catalogo de acciones de la seccion 11.2 (ver, crear, modificar, aprobar, eliminar/archivar, exportar, asignar) | Debe tener al menos un permiso marcado; no puede otorgar una accion que ningun modulo ofrezca a ningun rol (por ejemplo, "eliminar" un expediente ARCO-POL, que no existe para nadie, ver 11.3) |
| Descripcion | Texto libre para explicar el uso del rol | No sustituye la matriz de permisos; es solo documentacion |

**Que nunca se puede personalizar (permisos que nunca se delegan).** Ninguna ficha admite que un rol personalizado adquiera alguno de los siguientes puntos, porque son reglas de diseno fijas del sistema, no configuraciones de permisos:

- La condicion de que el rol Auditor (interno o externo) sea siempre de solo lectura (11.3): un rol personalizado no puede combinar capacidad de auditoria con capacidad de crear, aprobar o adjuntar evidencia sobre lo mismo que audita.
- Las acciones que este documento marca "Doble" en 11.2 y 11.3 (por ejemplo, aprobar el cambio de `tipo_rol` del Delegado, aprobar la exportacion de un paquete de evidencia con destino externo, aprobar el cambio de criterio de computo de un plazo ambiguo): estas exigen siempre una segunda persona distinta, sin que un rol personalizado pueda saltarse esa segunda firma.
- Los actos que la ley atribuye hoy a la figura del Delegado / Responsable interno mientras el estado sea ACTUAL (aprobar y emitir la prevencion, la incompetencia, la resolucion final y la notificacion a receptores en MOD-011; aprobar la notificacion externa de un incidente en MOD-013; el enlace institucional con la ACE): un rol personalizado no puede asumir estos actos por si mismo, solo puede ejecutarlos si a esa misma persona tambien se le asigna el rol estandar Delegado / Responsable interno.
- La activacion de la bandera `regimen_reforma_659` y la edicion del contenido del Centro Regulatorio (MOD-024) y del Centro de Ayuda (MOD-026): estas quedan siempre fuera del catalogo de roles de la organizacion cliente, sea estandar o personalizado (ver 11.7).
- El acceso de solo lectura del Titular a su propio expediente (MOD-011, MOD-012): un rol personalizado de la organizacion cliente no puede sustituir ni ampliar el acceso del Titular externo.

Esta lista es una consolidacion de reglas ya dispersas en las fichas (11.2 y 11.3); no agrega ninguna restriccion nueva, solo las agrupa en un solo lugar como exige el punto 4 de esta tarea.

### 11.4.2 Suplencias y ausencias

Ninguna ficha modela un mecanismo generico de "suplente" aplicable a los 12 roles estandar como tal; el unico mecanismo de suplencia explicito en el corpus es especifico del Delegado de Proteccion de Datos:

- **MOD-002, campo `delegado_sustituto`** (referencia opcional a otro registro, fundamento Art. 17 Lineamientos DPO): permite designar una o mas personas que suplan al Delegado en caso de ausencia, exigiendo que el sustituto cumpla el mismo perfil minimo del Art. 5 Lineamientos DPO (grado universitario, mayor de 21 anos, experiencia acreditada).
- Para el resto de roles (Aprobador, Responsable de area, Responsable de Seguridad/IT, etc.), ninguna ficha define un campo o flujo equivalente de suplencia formal; lo mas cercano es la reasignacion manual de tareas y aprobaciones que ya prevé MOD-021 ("Asignar / reasignar") y la reasignacion de un destinatario de alerta en MOD-022 ("Reasignar el destinatario resuelto de una regla, por ejemplo, activar un suplente"), pero ambas son mecanismos generales de reasignacion de trabajo, no un concepto formal de "suplencia de rol" con vigencia y reversion automatica.

**Hueco detectado:** un mecanismo generico de "suplente temporal de un rol" (por ejemplo, para vacaciones o incapacidad del Responsable ARCO-POL o del Aprobador, con fecha de inicio y fin y reversion automatica) no esta definido en ninguna ficha fuera del caso especifico del Delegado. Se marca en "Contradicciones y huecos detectados" al final de este documento.

### 11.4.3 Alta y baja de usuarios

Fuente: `MOD-001_ficha.md`, secciones F.2 y F.3 (ciclo de vida del Usuario). Estados: INVITADO -> ACTIVO -> SUSPENDIDO -> DADO DE BAJA (terminal), mas EXPIRADO como rama de INVITADO.

```
   [Administrador invita]
            |
            v
      +-----------+   acepta invitacion   +----------+
      | INVITADO  | ---------------------> |  ACTIVO  |
      +-----------+                        +----------+
            |                                  |    ^
            | vence invitacion (30 dias)        |    |
            v                                  |    | reactivar
      +-----------+                             |    |
      | EXPIRADO  |                             v    |
      +-----------+                       +------------+
      (Administrador puede reenviar)       | SUSPENDIDO |
                                            +------------+
                                                  |
                                                  | dar de baja
                                                  v
                                          +----------------+
                                          | DADO DE BAJA   |  (estado terminal,
                                          +----------------+   historial preservado)
```

Reglas clave:

- El alta exige correo valido y no duplicado, y al menos un rol seleccionado; genera una tarea "completar perfil" en MOD-021.
- La invitacion vence a los 30 dias (**[opinion de producto, sin respaldo legal expreso, valor propuesto pendiente de validacion por el equipo del producto]**); el Administrador puede reenviarla.
- Suspender o dar de baja exige siempre un motivo declarado; si el usuario es titular unico de un rol critico (por ejemplo, el unico Delegado o el unico Administrador), el sistema exige asignar reemplazo o confirmar una advertencia explicita antes de completar la baja.
- Dar de baja es un estado terminal: el usuario deja de poder iniciar sesion, pero su historial de acciones pasadas permanece intacto y vinculado a su identidad; nunca se elimina ni se reasigna a otra persona (coherente con el anti-feature 19 y con la regla general de preservacion de historial de `06_mapa_definitivo_de_modulos.md`, seccion 2, principio 8).
- Un cambio de rol hacia un rol sensible (Aprobador, Auditor) exige, a partir del umbral configurable de separacion de funciones, la aprobacion de un segundo Administrador o del Responsable Legal (ver 11.3).

### 11.4.4 Revision periodica de accesos

Fuente: `MOD-001_ficha.md`, seccion I (Alertas). El sistema no ejecuta una revision periodica de accesos por si mismo (eso exigiria una decision organizativa), pero genera dos alertas que la disparan:

| Alerta | Disparador | Nivel | Destinatario | Se apaga cuando |
|---|---|---|---|---|
| Invitacion pendiente de aceptar | Un usuario invitado no activo su cuenta | INFO | Administrador | El usuario acepta, o el Administrador cancela la invitacion |
| Estructura sin actualizar | Ningun cambio de usuarios, roles o sucursales en un periodo prolongado (por ejemplo, 6 meses) | INFO | Administrador, Responsable de Seguridad | Se realiza cualquier cambio, o el Administrador confirma explicitamente que reviso y no hay cambios pendientes |
| Umbral de separacion de funciones alcanzado | El numero de empleados declarado supera el umbral configurable sin que la separacion de funciones este activada | WARNING (escala a Legal a los 30 dias) | Administrador | Se activa la separacion de funciones, o el Administrador confirma su decision de mantenerla desactivada |

La confirmacion de que se revisaron los accesos vigentes ("el Administrador confirma que reviso y no hay cambios pendientes") queda registrada en el historial del modulo (MOD-001, seccion O) y es, junto con el listado exportable de usuarios y roles con hash de integridad, la evidencia principal que MOD-018 y MOD-019 usan para acreditar que la organizacion revisa sus accesos, sin que exista un modulo o expediente propio de "revision periodica de accesos" mas alla de estas alertas y de la exportacion firmada.

**Hueco detectado:** ninguna ficha define una periodicidad recomendada de la revision de accesos (por ejemplo, "cada 6 meses" o "cada cambio de personal"), ni un formulario o checklist especifico para esa revision (a diferencia de la reverificacion periodica que si esta bien definida para el Delegado en MOD-002). Se marca en "Contradicciones y huecos detectados".

---

## 11.5 Roles externos y temporales

Tres roles del catalogo estandar no son personal interno de la empresa cliente: Auditor externo (invitado), Asesor externo invitado y Titular (formulario externo). Fuente: `05_tipos_de_usuario.md`, seccion 5.1, perfiles 7 a 10, y seccion C de las fichas de modulo citadas en 11.2.

### 11.5.1 Auditor externo (invitado)

- **Alcance.** Acceso de solo lectura al paquete de evidencias exportado (MOD-019) y, segun el modulo, a expedientes o registros especificos habilitados para su auditoria puntual (RAT en MOD-006, proveedores en MOD-009, incidentes en MOD-013, EIPD en MOD-014, controles en MOD-015, documentos en MOD-008, plan de cumplimiento en MOD-005, procedimiento sancionador en MOD-024). Nunca crea, modifica, aprueba, comenta con capacidad de decision ni adjunta evidencia salvo la excepcion puntual de MOD-018, donde puede adjuntar su propio informe de auditoria como evidencia de la auditoria concreta para la que fue invitado.
- **Vigencia.** Siempre acotada en el tiempo ("ventana de auditoria" o "periodo de la auditoria puntual"); el acceso vence al cerrarse esa ventana. Ninguna ficha fija una duracion maxima en dias; el criterio queda en manos de quien invita (Administrador o Delegado), marcado aqui como **hueco**: no hay un plazo maximo por defecto ni una alerta automatica de "acceso de auditor externo por vencer" en el catalogo de alertas de MOD-022.
- **Restricciones sobre datos personales.** Solo ve los datos personales de titulares estrictamente necesarios para verificar la evidencia del alcance acordado (por ejemplo, que un expediente ARCO-POL se resolvio a tiempo), nunca el listado completo de titulares de la organizacion ni datos de otras auditorias. En MOD-019, el paquete de evidencia le llega ya generado y aprobado por doble control (ver 11.3); no puede generar sus propios paquetes.

### 11.5.2 Asesor externo invitado

- **Alcance.** Acceso puntual y acotado a un caso o modulo especifico para el que fue invitado (por ejemplo, dictaminar sobre una denegatoria ARCO-POL compleja, una base juridica dudosa, un conflicto de intereses del Delegado, o una transferencia internacional en disputa). Puede comentar y dejar su opinion registrada como evidencia del expediente puntual, y en algunos modulos (MOD-024) puede "colaborar" en la redaccion de una contestacion sin ser quien la aprueba. Nunca ve el resto de la organizacion fuera del caso asignado.
- **Vigencia.** Por invitacion puntual a un caso concreto, sin licencia permanente ni facturacion como usuario fijo del sistema (perfil Douglas Quintanilla, `05_tipos_de_usuario.md` seccion 5.1: "no quiere una licencia de usuario permanente ni que se le facture como usuario fijo del sistema"). Ninguna ficha fija automaticamente cuando expira el acceso al cerrarse el caso; se infiere que el acceso deberia cerrarse cuando el expediente que motivo la invitacion se cierra o archiva, pero ninguna ficha lo declara como una transicion automatica explicita, lo que se marca como **hueco**.
- **Restricciones sobre datos personales.** Ve unicamente el expediente o los datos del caso puntual para el que fue invitado (por ejemplo, el contenido de una solicitud ARCO-POL especifica), nunca el RAT completo, el listado de titulares ni otros expedientes de la misma organizacion.

### 11.5.3 Titular (formulario externo)

- **Alcance.** Presenta y da seguimiento a su propia solicitud ARCO-POL (MOD-011) y, cuando el Portal del Titular este activo (MOD-012, SHOULD HAVE), consulta el Aviso y la Politica de Privacidad vigentes y el estado de su expediente. No tiene cuenta interna de la organizacion, no ve la estructura, los usuarios ni ningun otro modulo (MOD-001, MOD-006, MOD-009, MOD-013 a MOD-019, MOD-024 le son opacos por completo).
- **Vigencia.** Esporadica: tipicamente una o dos veces por titular (perfil Cecilia Marroquin, `05_tipos_de_usuario.md` seccion 5.1). En el MVP, el canal es un formulario interno seguro (no un portal publico con autoregistro, decision 2.7.30 de `02_validacion_de_la_idea.md`), con verificacion de identidad segun el tipo de solicitante que reconoce el Art. 6 (titular, representante, herederos).
- **Restricciones sobre datos personales.** Es el unico rol que SI procesa datos personales directos como objeto legitimo del proceso (nombre, documento de identidad, domicilio, contenido de su solicitud); mientras su solicitud siga en Borrador sin enviar, es tambien el unico que puede corregir sus propios datos. Una vez enviada, el formulario y los documentos adjuntos quedan de solo lectura para el propio Titular y para el personal interno solo dentro del expediente correspondiente; el acceso de lectura del personal a sus documentos de identidad queda restringido a Responsable ARCO-POL y Delegado/Responsable interno, y cada lectura se registra (ver 11.6).

---

## 11.6 Acceso a datos sensibles y de titulares (necesidad de saber) y registro de accesos de lectura

Ninguna ficha usa literalmente la expresion "necesidad de saber" como principio general codificado en un solo lugar; el criterio aparece de forma consistente, modulo por modulo, restringiendo el acceso de lectura a datos personales sensibles o de titulares a los roles que efectivamente los necesitan para su funcion, con registro obligatorio de cada lectura. Esta subseccion consolida esas reglas dispersas.

### 11.6.1 Catalogo de datos con acceso restringido y registro de lectura obligatorio

| Modulo | Dato restringido | Roles con acceso de lectura | Registro de cada lectura |
|---|---|---|---|
| MOD-002 | Documento de identidad de la persona designada como Delegado / Responsable interno | Administrador de la organizacion, Aprobador, Responsable Legal | Si, en el historial (seccion O de la ficha) |
| MOD-006 | Ficha de tratamiento con datos sensibles | Todo acceso de lectura a una ficha con datos sensibles queda como evento de auditoria (no se restringe el rol, se registra el acceso) | Si, entrada append-only en el AuditLog transversal (MOD-019) |
| MOD-007 | Archivo de firma o documento de relacion parental (casos de menores, NNA) | Acceso restringido por rol a los archivos adjuntos sensibles | Si, obligatorio en el historial (seccion O) |
| MOD-011 | Documentos de identidad del titular (DUI, partidas, poderes) adjuntos a una solicitud ARCO-POL | Exclusivamente Responsable ARCO-POL y Delegado/Responsable interno; nunca Colaboradores ni Responsables de area | Si, registro de quien vio el documento y cuando, conservado 5 anos desde el cierre del expediente |
| MOD-014 | Expediente completo de una EIPD, para Auditor externo o Asesor externo invitado | Se registra el acceso de lectura de estos dos roles externos (los roles internos con acceso permanente no generan un registro adicional, mas alla del evento general de apertura de sesion) | Si, para roles externos |
| MOD-015 | Evidencia tecnica sensible (por ejemplo, un reporte de pentest que detalla vulnerabilidades reales) | Responsable de Seguridad/IT, Administrador y Auditor con acceso concedido explicitamente | Si, registro de quien la consulto y cuando **[opinion de producto, buena practica de seguridad, no exigida expresamente por la LPDP]** |
| MOD-019 | Evidencia sensible en general (cadena de custodia de MOD-013) | Segun el rol y el alcance de cada obligacion (ver 11.2) | Si, evento de auditoria en cada acceso de lectura a evidencia sensible |
| MOD-024 | Numero de expediente y datos de la persona natural del presunto infractor en un procedimiento sancionador | Administrador, Responsable Legal, Aprobador | Si, en el historial (seccion O) |
| MOD-025 | Registro de consultas de busqueda (Search Log) | Administrador (con justificacion registrada) y Auditor interno (solo lectura, como evidencia de minimizacion) | Si, la propia consulta al Search Log se registra igual que un acceso de lectura de nivel reforzado, para que el mecanismo de minimizacion no se convierta en una nueva via de exposicion |

### 11.6.2 Principio de necesidad de saber aplicado por rol

- **Responsable de area:** por diseno, ve solo los tratamientos, proveedores, controles, incidentes y evidencia de su propia area o sucursal (columna "Si\*, solo su area" repetida en 11.2 para MOD-006, MOD-009, MOD-013 a MOD-017, MOD-021), nunca el agregado de otras areas.
- **Auditor (interno y externo):** ve el contenido necesario para verificar de forma independiente, pero nunca puede coincidir con quien carga la evidencia, aprueba o cierra la accion que audita (regla transversal de 11.3).
- **Asesor externo invitado:** ve unicamente el caso o expediente puntual para el que fue invitado (11.5.2), nunca el resto de la organizacion.
- **Responsable ARCO-POL:** en MOD-009 y MOD-010, su visibilidad de receptores, encargados o transferencias queda filtrada a los que estan vinculados a un caso ARCO-POL propio, no al catalogo completo.
- **Titular:** nunca ve el RAT, el Mapa de Datos, el catalogo de proveedores, los controles de seguridad ni el listado de otros titulares; su acceso se limita a su propio expediente y, cuando exista, a los documentos publicados (Aviso, Politica).

### 11.6.3 Minimizacion como regla de diseno del dato mismo, no solo del acceso

Ademas de restringir quien lee un dato, varias fichas minimizan el dato mismo antes de que exista una decision de acceso que tomar: MOD-006 y MOD-009 solo referencian el Tratamiento o el registro de origen (no copian bases de datos completas del cliente); MOD-011 guarda los documentos de identidad como adjuntos cifrados en vez de campos de texto libre replicados en otros modulos; MOD-001 declara una excepcion explicita e intencional a este principio (si necesita datos reales de personas reales para el control de acceso del propio sistema, decision de alcance 2.7.21 de `02_validacion_de_la_idea.md`).

**Hueco detectado:** ninguna ficha consolida un catalogo unico y transversal de "necesidad de saber" (una matriz dato sensible x rol x justificacion, mantenida en un solo modulo, por ejemplo MOD-019 o MOD-025); el criterio existe pero esta repartido modulo por modulo, como se muestra en la tabla 11.6.1. Se marca en "Contradicciones y huecos detectados".

---

## 11.7 Roles internos del proveedor del software

Fuente: `MOD-024_ficha.md` (seccion B) y `MOD-026_ficha.md` (secciones B, C y F). Ninguno de estos roles pertenece a los 12 roles estandar de `05_tipos_de_usuario.md` seccion 5.3 porque no son usuarios de ninguna organizacion cliente: son personal del proveedor del software, documentados aqui unicamente porque gobiernan contenido centralizado que todas las organizaciones clientes consultan. Ninguna accion de estos roles se ejecuta dentro de una cuenta de cliente ni aparece en las tablas de permisos de la seccion 11.2, que solo cubren roles de la organizacion cliente.

| Rol interno del proveedor | Que gobierna | Que puede ver | Que NUNCA puede ver de los datos del cliente |
|---|---|---|---|
| Editor de contenido regulatorio (MOD-024) | El catalogo de instrumentos normativos (RegulatoryInstrument, RegulatoryRuleVersion), incluida la version de cada regla, y es quien activa el cambio de la bandera `regimen_reforma_659` de ACTUAL a FUTURO, con revision juridica y de forma consultiva junto con el Responsable Legal de cada organizacion cliente (que solo puede recomendar, nunca activar, ver 11.2) | El contenido normativo mismo (leyes, normativa ACE, lineamientos, catalogo de infracciones y multas), identico para todas las organizaciones clientes | Ningun expediente de procedimiento sancionador de un cliente especifico, ningun tratamiento del RAT, ningun expediente ARCO-POL, ninguna evidencia, ningun dato personal de titulares ni de personal interno de ninguna organizacion cliente. La ficha es explicita: "ninguna accion de este rol se ejecuta dentro de una cuenta de cliente" |
| Equipo de contenido del producto: autor, revisor legal y responsable de contenido/publicador (MOD-026) | El ciclo de vida de cada `HelpArticle` (Glosario y tarjetas de ayuda de 4 partes), con separacion de funciones propia: quien redacta nunca es quien revisa juridicamente, ni quien publica | El texto de ayuda generico y, cuando exista, retroalimentacion agregada y anonima de uso ("fue util / no fue util") | Ningun dato personal de titulares con los que trata la empresa cliente (la propia ficha lo declara expresamente: "no recopila ni conserva datos personales de los titulares"); ningun registro de negocio de ningun modulo (MOD-026 es de solo lectura sobre el resto del sistema, igual que MOD-025); ninguna evidencia legal de ninguna obligacion (MOD-026 "no genera evidencia que pruebe el cumplimiento de ninguna obligacion") |
| Equipo de soporte del producto (canal comercial/postventa) | Consultas de uso de la plataforma que la ayuda contextual no resuelve ("Solicitud de escalamiento a soporte del producto sin resolver", MOD-026 seccion I) | **[Hueco: ninguna ficha define el alcance de este rol]**, ver nota abajo | **[Hueco]** |

**Nota sobre el equipo de soporte del producto.** `MOD-026_ficha.md` (seccion I, tabla de alertas) menciona explicitamente a este actor una sola vez, y lo declara "fuera del alcance funcional de este analisis" (textual: "canal de soporte del proveedor... Segun la politica de soporte del proveedor (fuera de esta ficha)"). Ninguna otra ficha desarrolla que puede ver o no ver el personal de soporte de los datos de un cliente (por ejemplo, si puede entrar a una cuenta cliente para depurar un problema, si necesita el consentimiento explicito del Administrador de esa cuenta cada vez, o si tiene acceso de solo lectura a metadatos tecnicos pero nunca a datos personales de titulares). Esto es un **hueco real del corpus**, no una omision de esta seccion: el propio documento fuente lo declara fuera de su alcance. Se listan como propuesta de esta seccion, marcada explicitamente como tal y sujeta a validacion del equipo de producto y, en lo que toca a datos personales, a validacion legal:

**[Propuesta de esta seccion, no presente en las fichas]** Reglas minimas que deberia cumplir cualquier acceso de soporte a una cuenta cliente, coherentes con el resto del sistema:
1. Todo acceso de una persona del equipo de soporte a una cuenta cliente especifica requiere autorizacion explicita y registrada del Administrador de esa cuenta (analoga a la invitacion temporal de un Auditor externo o Asesor externo invitado, 11.5).
2. El acceso queda acotado en el tiempo y se registra en el historial de la organizacion cliente (visible para su Administrador y su Auditor interno), igual que cualquier acceso de lectura reforzado (11.6).
3. El acceso de soporte nunca sustituye ni ejecuta un acto que la ley atribuye a un rol de la organizacion cliente (por ejemplo, nunca aprueba ni emite una resolucion ARCO-POL, nunca activa la bandera `regimen_reforma_659` en nombre del cliente, ver 11.7).
4. Requiere validacion de la organizacion o asesoria especializada antes de fijarse como regla de producto definitiva, porque el alcance final depende de decisiones contractuales y de seguridad del proveedor que exceden el analisis funcional.

---

## 11.8 Efecto de la reforma 659 sobre el rol Delegado / Responsable interno

Fuente: `05_tipos_de_usuario.md` seccion 5.2, `06_mapa_definitivo_de_modulos.md` seccion 5, y `MOD-002_ficha.md`. Estado al 2026-09-24: el Decreto Legislativo 659 fue aprobado el 17-sep-2026, pero su publicacion en el Diario Oficial no esta confirmada; mientras no se publique y transcurran los 8 dias de vacatio legis, rige el regimen ACTUAL (Arts. 15 y 17 LPDP vigentes, Delegado obligatorio en el sector privado). Todo lo que sigue sobre el contenido articulado de la reforma se basa en fuentes secundarias, no en el texto oficial del decreto, que no ha sido localizado (OBL-PLAZO-05); se marca "requiere validacion de asesoria juridica" donde corresponda.

### 11.8.1 Modelo de una sola entidad, un atributo y una bandera

El rol no se duplica en dos modulos ni en dos roles del catalogo: existe un unico modulo (MOD-002) y una unica entidad conceptual ("Responsable del Programa de Datos") con:

1. Un atributo `tipo_rol` en el registro de la persona designada, que toma el valor `DELEGADO` (regimen ACTUAL) o `RESPONSABLE_INTERNO` (regimen FUTURO). El formulario de alta, el historial, las tareas asociadas y la capacitacion (MOD-017) son los mismos campos y pantallas; solo cambia la etiqueta y el conjunto de obligaciones activas.
2. Una bandera global `regimen_reforma_659` (ACTUAL | FUTURO), alojada en MOD-024, activada manualmente solo por el Editor de contenido regulatorio del proveedor (11.7) tras confirmar la publicacion oficial; el sistema nunca la activa por la sola fecha de aprobacion legislativa.

### 11.8.2 Que cambia en el rol para cada regimen

| Aspecto del rol | Regimen ACTUAL (vigente al 2026-09-24) | Regimen FUTURO (si la reforma se confirma y activa) |
|---|---|---|
| Obligatoriedad de la figura | Obligatoria en el sector privado (Arts. 15 y 17 vigentes) | Dejaria de ser obligatoria en el sector privado; las funciones pasarian al "sujeto obligado" (la empresa misma), segun fuentes secundarias (reforma al Art. 16) |
| Nombramiento formal ante la ACE | Exige comunicacion a la ACE en 15 dias habiles (OBL-DPO-03) y reverificacion periodica | Ya no exigiria nombramiento formal ante la ACE; el sistema deja de solicitar los pasos que la reforma volveria opcionales |
| Recepcion de solicitudes ARCO-POL | El Delegado o Responsable del tramite tramita el caso; el Delegado aprueba y emite todo acto legalmente atribuido a esa figura (prevencion, incompetencia, resolucion, notificacion a receptores) | Las solicitudes ARCO-POL se presentarian directamente ante la empresa; el rol configurable "Responsable del tramite ARCO-POL / Delegado de Proteccion de Datos" sigue existiendo, pero sin investidura legal obligatoria |
| Continuidad voluntaria | No aplica (la figura es obligatoria) | Una empresa que ya nombro Delegado certificado bajo ACTUAL puede mantenerlo voluntariamente bajo FUTURO; el sistema no fuerza el cese |
| Capacitacion especifica anual (OBL-CAP-02, MOD-017) | Obligatoria | Pasa a buena practica voluntaria si la empresa mantiene al Responsable Interno |
| Notificacion de revocacion de consentimiento (OBL-CONS-03, MOD-007) | El destinatario de la notificacion es el Delegado | El destinatario depende del estado vigente del responsable del tramite (mismo campo, distinto valor) |
| Conservacion del aviso de privacidad (OBL-RET-04, MOD-016) | El aviso vigente cita al Delegado como contacto (Art. 24 lit. h) | El contenido del aviso a conservar puede versionar segun el estado vigente al momento de su publicacion; MOD-024 dispara una tarea de revision, nunca reescribe el aviso ya publicado automaticamente |
| Obligaciones DPO propias (OBL-DPO-01 a 08, MOD-002) | Las 8 estan activas | Las 8 cambian de clasificacion segun el nuevo articulado (no se eliminan del sistema, se marcan "no aplica bajo el estado regulatorio actual, ver historial") |

En total, 17 obligaciones de la matriz cambian de estado con el cambio de bandera (OBL-DPO-01 a 08, OBL-ARCO-01/08/10/11/14, OBL-CONS-03, OBL-CAP-02, OBL-RET-04, OBL-PLAZO-05), sin cambiar nunca de modulo propietario (ver `06_mapa_definitivo_de_modulos.md`, seccion 5).

### 11.8.3 Preservacion de historial

Cuando la bandera pasa de ACTUAL a FUTURO, las tareas y registros de MOD-021 que dependian de pasos exclusivos del regimen ACTUAL (reverificacion trienal, informes semestrales, comunicacion formal a la ACE) no se eliminan: se marcan "no aplica bajo el estado regulatorio actual, ver historial". Un expediente ARCO-POL o un registro del Delegado ya cerrado antes del cambio de bandera conserva las reglas vigentes en el momento de su cierre; un nombramiento certificado bajo ACTUAL no se reinterpreta retroactivamente.

**Nota de incertidumbre juridica, requiere validacion de asesoria juridica:** el numero mismo del decreto (659), su fecha de publicacion y el contenido articulado exacto de la reforma (que articulos deroga o modifica en detalle) provienen de fuentes secundarias (prensa y nota oficial de la Asamblea Legislativa), no del texto oficial del decreto, que no ha sido localizado. Ninguna afirmacion de esta seccion sobre el contenido especifico de la reforma debe tratarse como un hecho verificado contra fuente primaria.

---

## 11.9 Quien aprueba cada acto critico (tabla consolidada)

Consolida, en una sola tabla, quien tiene la aprobacion final de los actos criticos que el prompt del cliente exige revisar de forma transversal. "Aprueba" significa siempre una confirmacion humana registrada; el sistema calcula, redacta el borrador o alerta, pero nunca ejecuta el acto sin esa confirmacion (seccion H de cada ficha, "Decisiones que NO debe automatizar").

| Acto critico | Modulo | Quien aprueba (regimen ACTUAL) | Segundo control / doble firma | Fundamento (OBL-ID, articulo) |
|---|---|---|---|---|
| Denegatoria motivada de una solicitud ARCO-POL | MOD-011 | Delegado de Proteccion de Datos / Responsable interno | Aprobador, como segundo revisor, si hay datos sensibles o riesgo de reclamo ante la ACE (a partir de empresa mediana) | OBL-ARCO-12, Art. 22 |
| Prevencion unica de una solicitud ARCO-POL | MOD-011 | Delegado de Proteccion de Datos / Responsable interno | Ninguno adicional; quien redacta el borrador (Responsable ARCO-POL) nunca es quien aprueba y emite | OBL-ARCO-08, Art. 18 |
| Notificacion de vulneracion de seguridad (a la ACE, la FGR y los titulares) | MOD-013 | Delegado de Proteccion de Datos / Responsable interno | Responsable Legal/Compliance puede co-revisar segun politica interna; el Responsable de Seguridad/IT solo prepara el borrador, nunca aprueba | OBL-INC-01, OBL-INC-02, OBL-INC-03, Art. 25 |
| Cierre de un incidente de seguridad | MOD-013 | Responsable de Seguridad/IT o Delegado (quien gestiono el caso) | Aprobador, como segunda firma, por encima del umbral configurable de separacion de funciones; por debajo, advertencia de autorrevision | OBL-INC-04, Art. 25 inciso final; OBL-PRIN-03, Art. 5 lit. i |
| Aprobacion de documentos regulatorios (Aviso de Privacidad, Politica de Privacidad) | MOD-008 | Segun la cadena de aprobacion configurada, tipicamente Aprobador | Doble aprobacion obligatoria para archivar estos dos tipos de documento (quien lo solicita y una segunda persona con rol Delegado/Responsable interno o Administrador) | OBL-AVISO-01 a 05, Art. 24; OBL-DOC-01 |
| EIPD (paso a estado Vigente) | MOD-014 | Aprobador, distinto de quien completo el cuestionario | Responsable Legal/Compliance es corresponsable cuando el riesgo calculado es Alto o Critico (doble control sin excepcion de tamano) | OBL-DOC-03, Art. 4 Medidas Organizativas lit. e |
| Aceptacion de riesgo residual (en vez de corregir un hallazgo de auditoria, o en una EIPD) | MOD-014, MOD-018 | Aprobador | Ninguno adicional mas alla del rol Aprobador, distinto de quien registro el hallazgo o el riesgo | Sin OBL-ID propio (decision de gestion de riesgo); MOD-018 propietario OBL-AUD-01 |
| Exportacion de un paquete de evidencia con destino externo a la organizacion | MOD-019 | Delegado/Responsable interno o Responsable Legal (primer control) | Aprobador (segundo control, obligatorio, sin excepcion de tamano de empresa) | OBL-PRIN-03, Art. 5 lit. i (responsabilidad demostrada) |
| Activacion de la bandera `regimen_reforma_659` (ACTUAL -> FUTURO) | MOD-024 | Editor de contenido regulatorio del proveedor del software (rol interno del proveedor, ver 11.7); ningun rol de la organizacion cliente la activa | Responsable Legal/Compliance de cada organizacion cliente solo puede recomendar, de forma consultiva y no vinculante | OBL-PLAZO-05 (requiere validacion de asesoria juridica sobre el contenido exacto de la reforma) |
| Aprobar y enviar cualquier tramite ante la ACE (contestacion de un emplazamiento, recurso, comprobante de pago) | MOD-024 | Responsable Legal/Compliance | Aprobador o un segundo Responsable Legal (doble control; en pyme, Administrador con advertencia de autorrevision) | Procedimiento sancionador, Art. 53 (remite a la Ley de Ciberseguridad) |
| Cambio de tipo_rol del Delegado (mantenerlo voluntariamente o migrar a Responsable Interno bajo estado FUTURO) | MOD-002 | Aprobador o Responsable Legal | Doble control siempre; nunca lo decide una sola persona | OBL-DPO-01 a 08 (afectadas por la reforma 659) |

---

## Contradicciones y huecos detectados

### Contradicciones resueltas (fuente en conflicto, version adoptada y por que)

1. **Numero y nombres de los roles estandar citados por las fichas de modulo.** Algunas fichas (por ejemplo, la plantilla `00_plantilla_ficha_modulo.md`, seccion B) listan un catalogo de ejemplo distinto y mas corto ("Administrador de organizacion, Responsable de privacidad, Gestor ARCO-POL, Legal, IT/Seguridad, RRHH, Marketing, Responsable de area, Aprobador, Auditor/Lectura, Titular externo") que no incluye separadamente al Delegado, al Auditor externo, al Asesor externo invitado ni distingue Auditor interno de Auditor externo. Se adopto el catalogo de 12 roles estandar de `05_tipos_de_usuario.md` seccion 5.3, que es la fuente jerarquicamente superior para roles y la que efectivamente usan las 26 fichas en sus propias secciones B y C (la nota final de `MOD-001_ficha.md` ya deja esta misma aclaracion por escrito: la plantilla es una version anterior, no un error a corregir en cada ficha).
2. **Rol interno del proveedor para el Centro Regulatorio y el Centro de Ayuda.** `MOD-024_ficha.md` documenta un "Editor de contenido regulatorio" y `MOD-026_ficha.md` documenta un "equipo de contenido del producto" (autor, revisor legal, publicador) como roles separados, cada uno propio de su modulo, sin unificarlos explicitamente en un solo catalogo de "roles del proveedor". Para esta seccion se adopto tratarlos como dos funciones de gobernanza de contenido distintas pero analogas (11.7), sin fusionarlas en un rol unico, porque ninguna ficha los declara equivalentes y cada uno gobierna un catalogo de datos distinto (normativo vs. de ayuda); fusionarlos habria sido una invencion no sustentada por las fichas.
3. **Alcance temporal del acceso del Auditor externo y del Asesor externo invitado.** Las fichas describen el acceso como "temporal", "acotado a una ventana de auditoria" o "acotado al caso", pero ninguna fija un numero de dias por defecto ni un mecanismo de expiracion automatica explicito (a diferencia de la invitacion de un usuario interno en MOD-001, que si expira a los 30 dias). No se adopto un plazo por defecto no sustentado por ninguna ficha; en su lugar, se documenta como hueco (ver mas abajo) en vez de inventar una cifra.

### Huecos detectados (piezas que ninguna ficha define)

1. **Mecanismo generico de suplencia de rol.** Fuera del campo `delegado_sustituto` de MOD-002 (especifico del Delegado), ninguna ficha define un mecanismo formal de "suplente temporal" para el resto de los 12 roles (por ejemplo, para vacaciones o incapacidad del Aprobador o del Responsable ARCO-POL), con fecha de inicio, fecha de fin y reversion automatica del rol al titular original. Ver 11.4.2.
2. **Periodicidad y checklist de la revision periodica de accesos.** MOD-001 genera alertas que sugieren revisar accesos ("Estructura sin actualizar"), pero ninguna ficha fija una periodicidad recomendada (por ejemplo, semestral) ni un formulario o checklist especifico de esa revision, a diferencia de la reverificacion periodica bien definida para el Delegado en MOD-002. Ver 11.4.4.
3. **Plazo maximo por defecto del acceso de un Auditor externo o un Asesor externo invitado, y su expiracion automatica.** Ninguna ficha fija cuantos dias dura por defecto una invitacion externa ni declara una transicion automatica que cierre el acceso cuando el caso o la auditoria concluyen; queda a criterio de quien invita, sin alerta propia en el catalogo de MOD-022 para "acceso externo por vencer". Ver 11.5.1 y 11.5.2.
4. **Alcance funcional del equipo de soporte del producto sobre los datos del cliente.** `MOD-026_ficha.md` (seccion I) menciona al "equipo de soporte del producto" y lo declara textualmente "fuera del alcance funcional de este analisis"; ninguna ficha del corpus define que puede o no puede ver este rol de los datos de un cliente, si necesita autorizacion explicita del Administrador de la cuenta, ni como queda registrado ese acceso. Esta seccion propone reglas minimas marcadas explicitamente como "propuesta de esta seccion, no presente en las fichas" (11.7), pendientes de validacion del equipo de producto y, en lo referente a datos personales, de asesoria juridica.
5. **Catalogo unico y transversal de "necesidad de saber".** El principio de necesidad de saber se aplica de forma consistente pero esta repartido modulo por modulo (tabla 11.6.1); ninguna ficha lo consolida en una sola matriz dato-sensible x rol x justificacion mantenida en un modulo especifico. Ver 11.6.3.
6. **Diferenciacion explicita de ocupantes tipicos del rol por tamano de empresa (mediana vs. corporativo).** `05_tipos_de_usuario.md` seccion 5.3 diferencia solo "pyme" de "quien lo suele ocupar" en general; la columna que separa "empresa mediana" de "corporativo" en la tabla de 11.1 es una elaboracion de esta seccion a partir de los perfiles narrativos de la seccion 5.1, marcada explicitamente como propuesta y no como una tabla que ya existiera en esa forma en el corpus.


