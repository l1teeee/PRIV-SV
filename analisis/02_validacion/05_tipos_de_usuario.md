# 5. Tipos de usuario

Fecha: 2026-09-24. Fase: analisis funcional (sin codigo, sin stack, sin base de datos).

Fuentes base: `00_contexto_para_agentes.md`, `00_prompt_analisis_funcional.md`, `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md`, `01_legal\matriz_obligaciones.md` / `matriz_obligaciones.json` (105 obligaciones, IDs canonicos OBL-AREA-NN) y `01_legal\03_hallazgos_regulatorios.md`. Alineado con las decisiones de alcance de `02_validacion_de_la_idea.md`, seccion 2.7, en particular la decision 7 (rol Delegado explicito) y la decision 30 (ARCO-POL del MVP sin portal publico dedicado).

Nota de alcance: donde una afirmacion es decision u opinion de producto, se marca "[opinion de producto]". Donde es juridica, se cita el OBL-ID y el articulo.

---

## 5.1 Personas (perfiles representativos)

Cada perfil incluye: nombre ficticio, cargo real, tipo y tamano de empresa, nivel de conocimiento legal, que necesita del sistema, frecuencia de uso, dispositivos y miedos/objeciones.

### Pyme (aprox. 30 empleados) - "Ferreteria y Suministros El Roble, S.A. de C.V."

**1. Karla Beatriz Hernandez Mejia - Gerente Administrativa y Financiera**
- Conocimiento legal: bajo-medio. No es abogada; ha leido resumenes de la ley porque le asignaron el tema.
- Rol en el sistema: Administradora de la organizacion y, ademas, Delegada de Proteccion de Datos interna (acumula roles por ser pyme; ver seccion 5.3).
- Necesita: un diagnostico guiado que le diga en lenguaje simple que le aplica, plantillas listas para usar, alertas claras de plazos.
- Frecuencia de uso: 2 a 3 veces por semana; mas intensivo durante el diagnostico inicial.
- Dispositivos: laptop Windows en la oficina, celular Android para notificaciones.
- Miedos y objeciones: teme una multa por desconocimiento y quedar personalmente expuesta al ser la designada; objeta que "esto es cosa de abogados, no mia" y que no tiene tiempo para aprender otra plataforma; el costo mensual le preocupa por el margen ajustado de la pyme.

### Empresa mediana (aprox. 300 empleados) - "Avicola San Andres, S.A. de C.V."

**2. Jorge Alberto Menendez Rauda - Jefe de Cumplimiento y Riesgo**
- Conocimiento legal: medio-alto; ha llevado cumplimiento de otras normativas (laborales, ambientales), no es abogado litigante.
- Rol en el sistema: Delegado de Proteccion de Datos interno, en proceso de certificacion ante la ACE bajo el regimen vigente.
- Necesita: un RAT robusto, reportes para la Gerencia y la Junta, trazabilidad completa para la auditoria anual de cumplimiento (OBL-AUD-01), coordinacion de plazos ARCO-POL entre varias areas.
- Frecuencia de uso: diaria.
- Dispositivos: laptop corporativa, tablet en reuniones de comite.
- Miedos y objeciones: teme una sancion grave o muy grave por un incidente mal documentado y quedar mal ante la Junta Directiva; pide integraciones con sistemas que ya usa (HRIS, camaras de planta) y le preocupa la curva de aprendizaje de su equipo.

**3. Daniela Patricia Cornejo Lazo - Coordinadora de Recursos Humanos**
- Conocimiento legal: bajo.
- Rol en el sistema: Responsable de area (RRHH); registra el tratamiento de datos biometricos de marcaje y de curriculums recibidos.
- Necesita: saber que debe hacer al implementar un lector biometrico o al recibir CVs (OBL-SENS-06, OBL-SENS-07), plantillas de aviso, tareas simples y accionables. El diagnostico le pregunta especificamente por biometria de control de acceso, no por "datos laborales" de forma generica.
- Frecuencia de uso: al implementar un proceso nuevo y en consultas puntuales.
- Dispositivos: celular y laptop.
- Miedos y objeciones: teme que su decision de instalar el biometrico genere un problema legal para toda la empresa; objeta que "esto es del area legal, no mia" si el lenguaje del sistema es muy tecnico.

**4. Roberto Antonio Villalta - Gerente de Tecnologia**
- Conocimiento legal: bajo en la ley, alto en seguridad tecnica.
- Rol en el sistema: Responsable de Seguridad / IT; registra controles tecnicos y gestiona incidentes.
- Necesita: catalogo de controles con evidencia, cronometro y checklist para las 72 horas de notificacion de incidentes (OBL-INC-01, OBL-INC-02), con los dos hitos de notificacion externa y revision interna mostrados por separado.
- Frecuencia de uso: constante durante un incidente, mensual en operacion normal.
- Dispositivos: laptop, acceso remoto desde celular durante guardias.
- Miedos y objeciones: teme que un incidente se le escape del plazo de 72 horas sin darse cuenta; no quiere que el sistema le exija instalar software adicional ni acceso amplio a su infraestructura.

### Corporativo con varias sociedades - "Grupo Financiero Itzalco" (banco, aseguradora y financiera bajo una misma holding)

**5. Licda. Ana Gabriela Reyes Portillo - Directora de Cumplimiento Corporativo**
- Conocimiento legal: alto (abogada interna).
- Rol en el sistema: Responsable Legal / Compliance a nivel de grupo, con visibilidad sobre varias sociedades. La vision consolidada multi-sociedad es funcionalidad V1/Enterprise, no MVP (ver `02_validacion_de_la_idea.md`, decision 2.7.31).
- Necesita: comparar el estado entre sociedades, exportar evidencia tanto para la ACE como para el regulador financiero sectorial.
- Frecuencia de uso: diaria o semanal segun la sociedad.
- Dispositivos: laptop, acceso desde la oficina central del grupo.
- Miedos y objeciones: teme que una sociedad del grupo quede desalineada y arrastre riesgo reputacional a todo el grupo; exige separacion estricta de datos entre sociedades y control fino de quien ve que.

**6. Lic. Mauricio Ernesto Aguilar Sandoval - Delegado de Proteccion de Datos certificado ante la ACE (interno, dedicado al banco del grupo)**
- Conocimiento legal: alto, con certificacion del Programa de Certificacion de Delegados de la ACE.
- Rol en el sistema: Delegado de Proteccion de Datos, dedicado exclusivamente a una sociedad regulada.
- Necesita: gestionar ARCO-POL de esa sociedad, generar el informe periodico al responsable (OBL-DPO-07, minimo dos veces al ano), mantener el enlace con la Direccion de Proteccion de Datos de la ACE (Art. 29 Lineamientos DPO).
- Frecuencia de uso: diaria.
- Dispositivos: laptop, VPN corporativa.
- Miedos y objeciones: le preocupa la incertidumbre de la reforma 659: si se publica, su cargo deja de ser obligatorio y su rol podria diluirse; pide que el sistema distinga claramente lo que hace por obligacion legal de lo que haria de todas formas por buena practica (ver seccion 5.2).

### Roles externos (no son personal interno de la empresa cliente)

**7. Sra. Cecilia Marroquin - Titular externo (cliente o ex empleada de una empresa cliente)**
- Conocimiento legal: ninguno o bajo (publico general).
- Rol en el sistema: Titular; presenta una solicitud ARCO-POL. En el MVP, el canal es un formulario interno seguro (no un portal publico con autoregistro; ver `02_validacion_de_la_idea.md`, decision 2.7.30), con verificacion de identidad segun el tipo de solicitante que reconoce el Art. 6 (titular, representante, herederos).
- Necesita: un formulario simple, saber el estado de su solicitud sin tener que crear una cuenta compleja.
- Frecuencia de uso: esporadica, tipicamente una o dos veces.
- Dispositivos: celular, casi siempre.
- Miedos y objeciones: desconfia de entregar su DUI u otros datos de verificacion de identidad en un sitio que no conoce; preferiria llamar o ir en persona (canal fisico/presencial, OBL-ARCO-15).

**8. Ing. Francisco Javier Bonilla - Auditor externo**
- Conocimiento legal: alto en controles y auditoria, no necesariamente abogado.
- Rol en el sistema: Auditor externo (invitado), con acceso temporal de solo lectura al paquete de evidencias de la empresa mediana o corporativa, para la auditoria anual de cumplimiento de las Politicas ACE (OBL-AUD-01).
- Necesita: exportar evidencia en un formato estandar, sin depender de que el cliente le envie archivos sueltos por correo.
- Frecuencia de uso: intensiva durante la semana de la auditoria, nula el resto del ano.
- Dispositivos: laptop propio, acceso temporal por invitacion.
- Miedos y objeciones: necesita garantias de que la evidencia mostrada es integra y no fue editada despues de generada (paquete exportado con verificacion de integridad, ver `02_validacion_de_la_idea.md`, decision 2.7.24).

**9. Lic. Douglas Ivan Quintanilla - Abogado externo ocasional**
- Conocimiento legal: alto.
- Rol en el sistema: Asesor externo invitado, con acceso puntual y acotado a un caso o modulo especifico (por ejemplo, revisar una denegatoria ARCO-POL compleja o dictaminar sobre una base juridica dudosa), no a toda la organizacion.
- Necesita: ver el fundamento normativo que el sistema ya aplico y el expediente completo del caso puntual; dejar su opinion registrada como evidencia.
- Frecuencia de uso: muy baja, por invitacion puntual a un caso concreto.
- Dispositivos: laptop.
- Miedos y objeciones: no quiere opinar sobre un caso sin ver el expediente completo; no quiere una licencia de usuario permanente ni que se le facture como usuario fijo del sistema.

**10. Licda. Silvia Carolina Melendez - Delegada de Proteccion de Datos externa (persona natural contratada por varias empresas, entre ellas la pyme Ferreteria El Roble)**
- Conocimiento legal: alto; atiende a varios clientes al mismo tiempo, cada uno con su propia organizacion en el sistema.
- Rol en el sistema: Delegada de Proteccion de Datos, en calidad de delegada externa (Art. 13 Lineamientos DPO permite que el delegado externo sea persona natural o juridica).
- Necesita: cambiar entre las organizaciones de sus distintos clientes dentro de una misma cuenta, viendo unicamente los datos del cliente activo en cada momento.
- Frecuencia de uso: variable segun el cliente; algunos dias atiende a varias organizaciones.
- Dispositivos: laptop.
- Miedos y objeciones: la reforma 659, si se publica, eliminaria la base regulatoria de su modelo de negocio como delegada externa obligatoria del sector privado; su servicio tendria que reconvertirse en asesoria voluntaria. Pide que el sistema le permita demostrar a sus clientes que cumplio sus funciones (informes periodicos, Art. 30 Lineamientos DPO) independientemente de si el cargo sigue siendo obligatorio.

**11. Sr. Oscar Rene Handal - Gerente General (perspectiva Gerencia del dashboard)**
- Conocimiento legal: bajo; orientado a negocio y riesgo reputacional y financiero.
- Rol en el sistema: consumidor de la vista de Gerencia del dashboard (no gestiona tareas el mismo).
- Necesita: un resumen ejecutivo simple (semaforos, sin jerga legal), saber si hay algo urgente que decidir.
- Frecuencia de uso: mensual, o inmediata cuando hay una alerta critica (por ejemplo, un incidente en curso).
- Dispositivos: celular para notificaciones, revisa el dashboard en la reunion de comite.
- Miedos y objeciones: teme las multas y el dano reputacional; no quiere aprender el sistema a fondo, solo necesita el resumen.

---

## 5.2 La figura del Delegado y el efecto de la reforma 659

El Delegado de Proteccion de Datos, bajo el regimen hoy vigente (Arts. 15 y 17 LPDP, Lineamientos para el Delegado de la ACE), puede ser:
- **Interno**, persona natural empleada de la empresa (perfiles 2 y 6 de la seccion 5.1).
- **Externo**, persona natural o juridica contratada (Art. 13 Lineamientos DPO; perfil 10). Cuando el delegado externo es persona juridica, esta debe designar expresamente a una persona natural responsable de atender las funciones (Art. 14 Lineamientos DPO).
- En cualquier caso, debe cumplir requisitos minimos (grado universitario, preferentemente en ciencias juridicas; mayor de 21 anos; experiencia acreditada en materias afines, Art. 5 Lineamientos DPO), someterse al Programa de Certificacion de Delegados de la ACE, y su nombramiento debe comunicarse a la ACE dentro de 15 dias habiles (OBL-DPO-03).

Hoy, el Delegado concentra funciones que el software refleja en un solo rol por defecto: recepcion y resolucion de solicitudes ARCO-POL, prevencion (Art. 18, OBL-ARCO-08), devolucion por incompetencia (Art. 19, OBL-ARCO-09), notificacion a receptores tras rectificacion o eliminacion (Art. 21, OBL-ARCO-11), tramite de revocacion del consentimiento (Art. 30, OBL-CONS-03), informe periodico al responsable al menos dos veces al ano (OBL-DPO-07), enlace institucional con la Direccion de Proteccion de Datos de la ACE (Art. 29 Lineamientos DPO), y confidencialidad durante 5 anos tras el cese (OBL-DPO-06). Todo acto de esta lista que el sistema calcule o redacte queda pendiente de una aprobacion explicita de la persona con el rol Delegado antes de emitirse; el sistema nunca lo envia de forma automatica.

**Si la reforma 659 se publica y entra en vigencia** (estado FUTURO, ver `04_objetivo_exacto_del_producto.md`, seccion 1.1.1): se derogarian los Arts. 15 y 17, el delegado dejaria de ser obligatorio en el sector privado, y esas funciones pasarian al "sujeto obligado" (la empresa misma), mediante lineamientos internos propios (reforma al Art. 16). Las solicitudes ARCO-POL se presentarian directamente ante la empresa. El sector publico mantendria la figura del delegado (reforma al Art. 47), que podria recaer en el Oficial de Informacion. Segun fuentes secundarias, los plazos (20+20, prevencion de 10 dias, devolucion en 5, notificacion a terceros en 5, revocacion en 5) no cambiarian. Ninguna de estas afirmaciones sobre el contenido articulado de la reforma esta verificada contra el texto oficial del decreto, que no ha sido localizado (OBL-PLAZO-05); el numero mismo del decreto (659) debe citarse como pendiente de confirmar.

Consecuencia de diseno: el sistema modela un rol "Responsable del tramite ARCO-POL / Delegado de Proteccion de Datos" configurable, que hoy se asigna por defecto a quien ocupe el rol Delegado (interno o externo, perfiles 2, 6 y 10), y que el sistema permite reasignar sin friccion el dia que el estado FUTURO se active, sin perder el historial de que version de la regla aplicaba a cada expediente.

---

## 5.3 Roles estandar del sistema

[opinion de producto para el nombre y alcance exacto de cada rol; el fundamento de la obligatoriedad de la figura Delegado si es legal y esta citado en 5.2]

| Rol | Proposito | Quien lo suele ocupar | Acumulable en pyme |
|---|---|---|---|
| Administrador de la organizacion | Configura estructura, usuarios, permisos e integraciones; no necesariamente revisa contenido legal en detalle | Dueno o gerente general/administrativo | Si, con casi todos los demas roles |
| Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | Concentra hoy las funciones legales del Delegado (ARCO-POL, informes, enlace ACE); en el estado FUTURO coordina la funcion sin investidura legal obligatoria | Persona designada internamente, o Delegado/DPO externo contratado | Si, una sola persona puede ocuparlo junto con Administrador |
| Responsable ARCO-POL / Responsable del tramite | Ejecuta el dia a dia de las solicitudes de titulares dentro de los plazos legales | El mismo Delegado en pyme, o personal de atencion al cliente/legal en empresa mediana | Si |
| Responsable Legal / Compliance | Revisa bases juridicas, documentos, denegatorias y contratos | Abogado interno, o gerente administrativo con apoyo externo en pyme | Si en pyme |
| Responsable de Seguridad / IT | Registra controles tecnicos y evidencia, gestiona incidentes y el cronometro de 72 horas | Jefe de TI, o el proveedor externo de TI si la pyme no tiene TI interno | Si en pyme |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Registra y mantiene actualizados los tratamientos de su area en el RAT, ejecuta las tareas que le asignan | Jefes de cada area | No aplica: por diseno son varios usuarios distintos |
| Aprobador | Aprueba documentos, decisiones de riesgo y cierres de casos sensibles antes de publicarse o enviarse, segun la cadena de aprobacion configurada por tipo de documento | Gerencia, o el mismo Delegado en pyme | Si en pyme; en mediana/corporativo se recomienda separarlo (ver 5.4) |
| Auditor (interno) | Solo lectura y exportacion de evidencia; no crea ni aprueba nada | Auditoria interna corporativa; en pyme puede recaer en el mismo Delegado con advertencia de autorrevision | Con advertencia visible en pyme |
| Auditor externo (invitado) | Acceso temporal de solo lectura para una auditoria puntual | Firma auditora externa | No aplica, siempre es un tercero |
| Usuario de consulta / Colaborador | Ve y completa unicamente las tareas que se le asignan | Empleados operativos que ejecutan una tarea puntual | Se acumula naturalmente en pyme al ser pocos empleados |
| Titular (formulario externo) | Presenta y da seguimiento a su propia solicitud ARCO-POL | Cliente, empleado, ex empleado o candidato de la empresa cliente | No aplica, no es usuario interno de la organizacion |
| Asesor externo invitado | Acceso acotado en tiempo a un caso o modulo especifico | Abogado externo ocasional, consultor de seguridad puntual | No aplica, siempre externo y temporal |

---

## 5.4 Reglas minimas de separacion de funciones

[mayoria opinion de producto; se indica cuando hay un fundamento legal parcial]

- El rol Auditor (interno o externo) debe ser siempre de solo lectura: nunca debe coincidir con el usuario que carga evidencia o aprueba una accion, para que su verificacion sea independiente. [opinion de producto]
- En organizaciones con areas separadas (a partir de empresa mediana), quien registra o ejecuta una accion sobre datos sensibles o un tratamiento de riesgo alto segun la EIPD no deberia ser la unica persona que la aprueba. [opinion de producto]
- Cuando una solicitud ARCO-POL involucra datos sensibles o existe riesgo de reclamo ante la Direccion de Proteccion de Datos de la ACE (OBL-ARCO-14), el sistema debe permitir escalar la decision de denegatoria a un segundo revisor antes de notificar al titular. [opinion de producto, apoyada en la exigencia de motivacion del Art. 22 y en que la denegatoria indebida es infraccion muy grave segun el catalogo del Art. 56]
- Un mismo usuario no deberia acumular simultaneamente Administrador y Auditor sobre el mismo periodo de evidencia, salvo en pyme, donde el sistema lo permite mostrando siempre una advertencia visible de "autorrevision". [opinion de producto]
- Todo cierre de un incidente de seguridad debe dejar registrada la evidencia de la decision (quien decidio, cuando, con que fundamento), aunque la misma persona haya gestionado todo el caso; esto no exige dos personas distintas por ley, pero si una trazabilidad verificable, en linea con la documentacion obligatoria de toda vulneracion (OBL-INC-04, Art. 25 inciso final) y el principio de responsabilidad demostrada (OBL-PRIN-03, Art. 5 lit. i).
- Umbral configurable de tamano: por debajo de un numero de empleados definido por producto (propuesta inicial: 50), el sistema no exige separacion de funciones, solo la recomienda; por encima de ese umbral, advierte y permite al Administrador activar el bloqueo de la acumulacion Aprobador + Auditor en la misma persona. [opinion de producto, umbral sin respaldo legal]

---

## Resumen de decisiones que quedan como opinion de producto (no exigidas expresamente por la ley)

- El umbral de 50 empleados para activar la exigencia de separacion de funciones.
- El nombre y alcance exacto de los roles estandar (Aprobador, Usuario de consulta, Asesor externo invitado, etc.); la ley solo exige de forma expresa la figura del Delegado (mientras este vigente el regimen actual).
- Las metricas de exito del producto (cobertura, adopcion, retencion comercial), detalladas en `04_objetivo_exacto_del_producto.md`.
- El criterio conservador de "horas corridas" para el plazo de 72 horas del Art. 25, mientras no exista pronunciamiento oficial.
