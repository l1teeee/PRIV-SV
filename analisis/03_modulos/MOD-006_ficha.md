# MODULO: RAT y Mapa de Datos

Codigo corto del modulo: MOD-006
Clasificacion global del modulo: MUST HAVE (para el MVP)
Obligaciones que cubre:
- Propietarias (8): OBL-DOC-02, OBL-PRIN-02, OBL-SENS-01, OBL-SENS-04, OBL-SENS-06, OBL-SENS-08, OBL-TRAT-01, OBL-TRAT-03
- Colaboradoras (6, propiedad de otro modulo pero alimentadas o consultadas por MOD-006): OBL-ARCO-03, OBL-PRIN-01, OBL-SEG-02, OBL-SENS-03, OBL-SENS-05, OBL-TRAT-02

---

## A. Proposito

**Por que existe.** Toda empresa sujeta a la Ley para la Proteccion de Datos Personales (Decreto Legislativo 144, en adelante LPDP) necesita saber, de forma concreta y verificable, que datos personales trata, para que los trata, con que base juridica, quien los administra internamente y en que sistema viven. Sin esa foto ordenada, ningun otro proceso del programa de proteccion de datos tiene donde apoyarse: no se puede pedir consentimiento sin saber para que finalidad, no se puede resolver una solicitud ARCO-POL sin saber en que sistema esta el dato, no se puede evaluar un incidente sin saber que actividad de tratamiento se vio afectada, ni se puede clasificar un proveedor como encargado sin saber que tratamiento le fue delegado. MOD-006 existe para ser esa fuente unica de verdad: el Registro de Actividades de Tratamiento (RAT), con el Mapa de Datos como una vista visual sobre la misma informacion, nunca como una segunda base de datos independiente (decision 2.7.1 de `02_validacion_de_la_idea.md`, inconsistencia 1: "Inventario de datos vs RAT vs Mapa de datos").

**Que problema resuelve para la empresa.** Resuelve la pregunta que casi ninguna pyme o empresa mediana salvadorena puede responder hoy sin ayuda: "que datos personales tratamos, donde estan, por que los tenemos y quien es responsable de cada uno". Convierte esa pregunta dispersa (en la cabeza de varios jefes de area, en contratos sueltos, en sistemas que nadie documento) en un registro estructurado, por actividad de tratamiento, que se mantiene vivo con el tiempo.

**Que obligacion u obligaciones cubre (IDs y articulos).**

| OBL-ID | Titulo | Norma y articulo | Clasificacion |
|---|---|---|---|
| OBL-DOC-02 | Registro de Actividades de Tratamiento (RAT) | Politicas de Actuacion ACE N. 001-0309025-DPDP, Art. 4 (Medidas Organizativas, lit. d) | OBLIGATORIO |
| OBL-PRIN-02 | Principio de licitud: seis bases de tratamiento | LPDP Art. 5 lit. g) | OBLIGATORIO |
| OBL-SENS-01 | Identificacion de datos personales sensibles | LPDP Art. 4 lit. g) | OBLIGATORIO |
| OBL-SENS-04 | Tratamiento de datos de salud | LPDP Art. 39 | CONDICIONAL (giro de salud) |
| OBL-SENS-06 | Informacion biometrica como dato sensible | LPDP Art. 4 lit. g) | OBLIGATORIO |
| OBL-SENS-08 | Videovigilancia y reconocimiento facial | LPDP Art. 4 lit. f) y g), Art. 7, Art. 12 lit. b), Art. 16 lit. g) | CONDICIONAL (si usa camaras) |
| OBL-TRAT-01 | Prohibicion de desviacion de finalidad | LPDP Art. 32 | OBLIGATORIO |
| OBL-TRAT-03 | Definicion estricta de fuentes de acceso publico | LPDP Art. 4 lit. l) | CONDICIONAL (si invoca esta excepcion) |

Como colaborador (el modulo propietario es otro, pero MOD-006 alimenta o consulta el dato): OBL-ARCO-03 (rectificacion, Art. 9, propietario MOD-011: el RAT indica en que sistema esta el dato a rectificar), OBL-PRIN-01 (consentimiento y finalidad, Art. 5 lit. c, propietario MOD-007: el RAT declara la finalidad que despues respalda cada consentimiento), OBL-SEG-02 (medidas organizativas minimas de las Politicas ACE, Art. 4, propietario MOD-015: el RAT es una de las seis medidas organizativas exigidas), OBL-SENS-03 (excepciones al consentimiento para datos sensibles, Art. 37 y 38, propietario MOD-007: el RAT es donde se documenta la excepcion invocada), OBL-SENS-05 (prohibiciones sobre datos sensibles, Art. 59, propietario MOD-015: el RAT es la evidencia de que categoria de dato se trata para verificar que no se incurre en una prohibicion) y OBL-TRAT-02 (excepciones al consentimiento previo, Art. 28, propietario MOD-007: el RAT documenta la excepcion aplicable por tratamiento).

**Que valor aporta.**
- Operativo: es el mapa de referencia que consultan por lectura MOD-007 (Consentimiento), MOD-008 (Documentos: el Aviso de Privacidad se redacta a partir de las finalidades y categorias del RAT), MOD-009 (Proveedores: que tratamiento delega la empresa a cada encargado), MOD-010 (Transferencias: que tratamiento cruza frontera), MOD-013 (Incidentes: que actividad de tratamiento se vio afectada), MOD-014 (Riesgos/EIPD: que tratamiento dispara una evaluacion de impacto), MOD-015 (Controles: que controles cubren que tratamiento), MOD-016 (Retencion: el plazo declarado en el RAT alimenta el motor de retencion) y MOD-018 (Auditoria).
- Probatorio: demuestra el principio de responsabilidad demostrada (OBL-PRIN-03, Art. 5 lit. i, propietario del Centro de Evidencias MOD-019) porque cada tratamiento queda documentado con quien lo registro, cuando y con que base.
- De reduccion de riesgo: al forzar la seleccion explicita de una base de licitud y la clasificacion de sensibilidad por categoria de dato, evita que la empresa trate datos sensibles (biometria, salud, afiliacion sindical) sin darse cuenta de que activo un regimen reforzado.

**Que NO hace este modulo (limites explicitos).**
- No copia ni centraliza la base de datos real de clientes, empleados o proveedores de la empresa; registra metadatos del tratamiento (que categoria de dato, en que sistema, con que finalidad), nunca los datos personales mismos (anti-feature 1 y 8 de `22_anti_features.md`).
- No decide si una base de licitud es valida para un tratamiento concreto; solo exige que se declare una de las seis del Art. 5 lit. g) con su justificacion, y muestra la nota "Requiere validacion de la organizacion o asesoria especializada" cuando la base elegida requiere criterio juridico (anti-feature 6).
- No ejecuta ni certifica controles de seguridad; solo referencia por enlace los controles que MOD-015 ya tiene registrados para ese tratamiento.
- No es el modulo que gestiona el consentimiento, los contratos con proveedores, las transferencias internacionales ni las EIPD; es la fuente que esos modulos consultan por referencia, nunca el lugar donde esos procesos se ejecutan.
- No emite ningun dictamen sobre si una fuente califica como "acceso publico" bajo el Art. 4 lit. l); solo exige que, si se invoca esa excepcion, quede un analisis documentado (OBL-TRAT-03).

**Por que el RAT es (o no) el nucleo funcional del sistema.** El RAT es el nucleo funcional de la plataforma, con dos matices. Primero, es el unico modulo de registro cuya obligacion propietaria (OBL-DOC-02) es una de las seis medidas organizativas obligatorias segun las Politicas ACE, y la unica de esas seis que, a su vez, es insumo de todas las demas (no se puede hacer una EIPD, un aviso de privacidad ni evaluar un incidente sin saber que tratamiento esta en juego). Segundo matiz, el RAT no es el unico modulo "core": comparte ese papel con MOD-009 (Proveedores) y MOD-011 (ARCO-POL), identificados igualmente como nucleo en `02_validacion_de_la_idea.md` seccion 2.1; la diferencia es que el RAT es estructuralmente anterior a los otros dos, porque ambos lo consultan por referencia (un proveedor se enlaza a que tratamiento le fue delegado; una solicitud ARCO-POL se resuelve consultando en que sistema, segun el RAT, esta el dato del titular). En ese sentido especifico (ser la base de la que dependen los demas modulos de registro), el RAT si es el nucleo funcional del producto.

---

## B. Usuarios

| Rol | Para que usa MOD-006 |
|---|---|
| Administrador de la organizacion | Da de alta el modulo, configura el catalogo de sistemas inicial y revisa el avance global del RAT, sin necesariamente completar el contenido legal de cada ficha. |
| Delegado de Proteccion de Datos (o Responsable interno, segun el estado de la reforma 659) | Revisa y aprueba las actividades de tratamiento de mayor riesgo antes de que pasen a estado Vigente, usa el RAT como base de sus informes periodicos a la Gerencia (OBL-DPO-07) y como insumo directo de las funciones que hoy la ley le atribuye. |
| Responsable ARCO-POL / Responsable del tramite | Consulta el RAT y el Mapa de Datos para saber en que sistema esta el dato de un titular al resolver una solicitud ARCO-POL. |
| Responsable Legal / Compliance | Revisa que la base de licitud declarada sea razonable, redacta o valida la justificacion textual de cada base, y decide cuando una actividad requiere EIPD. |
| Responsable de Seguridad / IT | Da de alta y mantiene el Catalogo de Sistemas (nombre tecnico, tipo, ubicacion, proveedor asociado), y enlaza los controles de seguridad de MOD-015 a cada tratamiento. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Es quien mas usa el modulo en el dia a dia: registra y mantiene actualizadas las actividades de tratamiento de su propia area (por ejemplo, RRHH registra nomina y reclutamiento; Marketing registra campanas). |
| Aprobador | Aprueba formalmente el paso de una ficha de tratamiento de "En revision" a "Vigente" cuando el tratamiento es de riesgo alto o involucra datos sensibles, sin ser necesariamente quien lo registro. |
| Auditor (interno) | Consulta en modo lectura el RAT completo y su historial de cambios para la auditoria anual de cumplimiento (OBL-AUD-01, propietario MOD-018). |
| Auditor externo (invitado) | Recibe acceso temporal de solo lectura al RAT exportado como parte del paquete de evidencia de una auditoria puntual. |
| Usuario de consulta / Colaborador | Completa unicamente los campos de una tarea puntual que se le asigno (por ejemplo, "confirmar el sistema donde vive el dato de nomina"), sin ver el RAT completo de otras areas salvo que se le habilite. |
| Titular (formulario externo) | No usa MOD-006 directamente; es el sujeto de los tratamientos registrados. El Mapa de Datos nunca es visible desde el Portal del Titular (MOD-012). |
| Asesor externo invitado | Recibe acceso puntual de lectura a una o varias fichas de tratamiento cuando se le pide opinion sobre una base de licitud dudosa, sin ver el RAT completo de la organizacion. |

---

## C. Permisos

| Accion | Administrador | Delegado / Resp. interno | Resp. ARCO-POL | Legal / Compliance | Seguridad / IT | Resp. de area | Aprobador | Auditor interno | Auditor externo | Usuario de consulta | Asesor externo |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver RAT completo de la organizacion | Si | Si | Solo lectura | Si | Si (solo campos de sistema/seguridad) | No (solo su area) | Si | Solo lectura | Solo lectura (exportado) | No | No (solo lo invitado) |
| Crear ficha de tratamiento | Si | Si | No | Si | No | Si (su area) | No | No | No | No | No |
| Modificar ficha (estado Borrador o En revision) | Si | Si | No | Si | Solo campos de sistema | Si (su area, mientras no este Vigente) | No | No | No | No | No |
| Aprobar (Vigente) | No (salvo que tambien tenga rol Aprobador) | Si (recomendado por defecto) | No | Si (si es tratamiento sensible) | No | No | Si | No | No | No | No |
| Cerrar / archivar tratamiento | Si | Si | No | Si | No | No | No | No | No | No | No |
| Eliminar ficha (solo Borrador sin historial) | Si | No | No | No | No | No | No | No | No | No | No |
| Exportar RAT / paquete de evidencia | Si | Si | No | Si | No | No | No | Si | Si (solo lo compartido) | No | No |
| Asignar tarea de completar campo | Si | Si | No | Si | No | No | No | No | No | No | No |
| Comentar en una ficha | Si | Si | Si | Si | Si | Si | Si | No | No | No | Si (en la ficha invitada) |
| Adjuntar evidencia (analisis de base legal, matriz de riesgo) | Si | Si | No | Si | Si | Si | Si | No | No | No | Si |
| Dar de alta un sistema en el Catalogo de Sistemas | Si | No | No | No | Si | No | No | No | No | No | No |

**Separacion de funciones.** Quien registra una ficha de tratamiento de riesgo alto o con datos sensibles (Responsable de area) no puede a la vez aprobarla; la aprobacion exige el rol Aprobador o Legal/Compliance (regla heredada de `05_tipos_de_usuario.md` seccion 5.4, "quien registra o ejecuta una accion sobre datos sensibles o un tratamiento de riesgo alto no deberia ser la unica persona que la aprueba" [opinion de producto]). En pyme (por debajo del umbral configurable, propuesta inicial 50 empleados), el sistema permite que la misma persona registre y apruebe, pero muestra siempre la advertencia visible de autorrevision. La exportacion del RAT completo para auditoria (doble control) exige rol Administrador, Delegado o Legal, nunca un Responsable de area por si solo, para evitar que una sola persona decida que se muestra a un auditor.

---

## D. Informacion de entrada

### D.1 Ficha de actividad de tratamiento (entidad Treatment)

| Campo | Tipo | Obligatorio / opcional | Opciones o catalogo | Validacion | Texto de ayuda al usuario | Fundamento |
|---|---|---|---|---|---|---|
| Nombre del tratamiento | Texto | Obligatorio desde Borrador | Libre, con sugerencias de la biblioteca de plantillas (ver seccion D.6) | Minimo 5 caracteres, unico dentro de la organizacion | "Dele un nombre que cualquier persona de la empresa entienda, por ejemplo 'Nomina y pago de salarios', no 'Proceso 3'." | Buena practica |
| Descripcion breve | Texto largo | Obligatorio para pasar a En revision | Libre | Maximo 1000 caracteres | "Explique en dos o tres frases que se hace con estos datos, como si se lo contara a alguien que no conoce la empresa." | Buena practica |
| Area responsable | Referencia a Departamento (MOD-001) | Obligatorio desde Borrador | Catalogo de areas de la organizacion | Debe existir en MOD-001 | "Elija el area que administra este tratamiento en el dia a dia, no necesariamente quien lo esta registrando." | Buena practica |
| Responsable interno del tratamiento | Referencia a Usuario (MOD-001) | Obligatorio para pasar a En revision | Usuarios activos de la organizacion | Debe tener rol Responsable de area o superior | "Es la persona que puede responder preguntas sobre este tratamiento si la ACE o un titular las hace." | Buena practica, apoya OBL-PRIN-03 |
| Finalidad | Texto largo | Obligatorio desde Borrador | Libre, con sugerencias precargadas por plantilla | Minimo 15 caracteres, no puede ser identica a la descripcion | "Diga para que se usan estos datos, no que datos son. Ejemplo: 'pagar el salario mensual y cumplir obligaciones tributarias y de seguridad social'." | OBL-TRAT-01, Art. 32; OBL-PRIN-02, Art. 5 lit. g) |
| Base de licitud | Seleccion unica | Obligatorio para pasar a En revision | Consentimiento expreso / Ejecucion de contrato o medidas precontractuales / Cumplimiento de obligacion legal / Proteccion de intereses vitales / Cumplimiento de un fin de interes publico / Intereses legitimos | Debe elegirse una de las seis; si se elige "Intereses legitimos" el sistema exige el campo siguiente | "La ley exige elegir una razon valida para tratar estos datos. Si duda, consulte con Legal o con su Delegado antes de continuar." | OBL-PRIN-02, Art. 5 lit. g) |
| Justificacion de la base de licitud | Texto largo | Obligatorio si la base no es "Consentimiento expreso" | Libre | Minimo 30 caracteres | "Explique por escrito por que esta base aplica a este tratamiento especifico. Si eligio 'Intereses legitimos', explique tambien por que no afecta de forma desproporcionada al titular." | OBL-PRIN-02; muestra advertencia "Requiere validacion de la organizacion o asesoria especializada" |
| Excepcion invocada (si no hay consentimiento ni otra base evidente) | Seleccion unica | Condicional: visible solo si se marca "excepcion del Art. 28" | Los 8 supuestos del Art. 28 lit. a) a h) | Debe seleccionarse una opcion de la lista | "Marque unicamente si el tratamiento no requiere pedir autorizacion previa por una de las excepciones que reconoce la ley." | OBL-TRAT-02, Art. 28 (colaboradora, propietario MOD-007) |
| Categorias de titulares | Seleccion multiple | Obligatorio desde Borrador | Catalogo de categorias de titulares (ver D.2) | Al menos una categoria | "Seleccione a quien pertenecen estos datos: empleados, clientes, candidatos, proveedores, visitantes, etc." | Buena practica, apoya OBL-DOC-02 |
| Incluye menores de edad | Booleano | Obligatorio desde Borrador | Si / No | - | "Marque si entre los titulares puede haber personas menores de 18 anos, por ejemplo hijos de empleados en beneficios, o usuarios de una app." | OBL-CONS-05 (colaboradora, propietario MOD-007) |
| Categorias de datos tratados | Seleccion multiple con submenu | Obligatorio desde Borrador | Catalogo de categorias de datos (ver D.3), organizado en ordinarios y sensibles | Al menos una categoria; si se marca una categoria sensible, el sistema exige los campos de la seccion D.4 | "Marque que tipo de informacion se recopila. Si marca una categoria de la lista 'Sensible', el sistema le pedira informacion adicional obligatoria por ley." | OBL-DOC-02; dispara OBL-SENS-01 |
| Origen del dato | Seleccion unica | Obligatorio para pasar a En revision | Directamente del titular / Formulario web o app / Fuente de acceso publico / Recibido de un tercero o proveedor / Generado internamente (por ejemplo, evaluacion de desempeno) / Otro (especificar) | Si se elige "Fuente de acceso publico" se activa el campo de analisis del catalogo D.5 | "Indique de donde viene el dato: si lo dio el titular, si lo genera la empresa, o si lo recibio de otra empresa." | Buena practica, apoya OBL-TRAT-03 si se elige acceso publico |
| Sistema o sistemas donde se procesa | Referencia multiple al Catalogo de sistemas (ver D.7) | Obligatorio para pasar a En revision | Catalogo de sistemas de la organizacion, con opcion "Agregar sistema nuevo" | Al menos un sistema | "Elija en que programa, aplicacion o archivo vive este dato. Si el sistema no esta en la lista, puede agregarlo." | Buena practica; base del Mapa de Datos |
| Encargados del tratamiento involucrados | Referencia multiple a Proveedor (MOD-009, tipo Encargado) | Opcional en Borrador, obligatorio si algun sistema es externo | Catalogo de proveedores tipo Encargado de MOD-009 | Si el sistema seleccionado es de tipo SaaS externo, se sugiere automaticamente el proveedor asociado | "Si una empresa externa procesa estos datos por cuenta suya (por ejemplo, el proveedor de planillas), enlacela aqui." | OBL-PROV-01 a 04 (colaboradora, propietario MOD-009) |
| Terceros o destinatarios que reciben el dato | Texto largo o referencia | Opcional | Libre o referencia a Proveedor tipo Tercero/Receptor | - | "Indique si el dato se comparte con alguien fuera de la empresa que no es su encargado (por ejemplo, una aseguradora, una entidad publica)." | OBL-TRAT-01 |
| Hay transferencia fuera de El Salvador | Booleano | Obligatorio para pasar a En revision | Si / No | Si es Si, se recomienda crear el registro correspondiente en MOD-010 | "Marque si el sistema o el encargado que eligio esta ubicado fuera de El Salvador, o si el dato viaja fuera del pais por cualquier motivo." | OBL-TRANSF-01 a 06 (colaboradora, propietario MOD-010) |
| Pais de alojamiento o destino (si aplica) | Texto o catalogo de paises | Condicional: obligatorio si "Hay transferencia" es Si | Lista de paises | - | "Indique el pais donde esta el proveedor o donde se aloja el sistema." | Alimenta el Mapa de Datos y MOD-010 |
| Plazo de conservacion / retencion | Texto estructurado (numero + unidad) o referencia a regla de MOD-016 | Obligatorio para pasar a En revision | Anios / Meses / Mientras dure la relacion + N anios adicionales / Indefinido con justificacion | Si se elige "Indefinido" el sistema exige justificacion obligatoria | "Indique cuanto tiempo se conservan estos datos y por que. Ejemplo: 'mientras dure la relacion laboral y 10 anios mas, por retencion tributaria'." | Alimenta OBL-RET-01 a 06 (colaboradora, propietario MOD-016) |
| Controles de seguridad aplicados | Referencia multiple al Catalogo de controles (MOD-015) | Opcional en Borrador, obligatorio para pasar a Vigente | Catalogo de controles de MOD-015 | Si el tratamiento incluye datos sensibles, se exige al menos un control de tipo "cifrado" o "control de acceso" | "Enlace los controles de seguridad que protegen este dato (por ejemplo, cifrado, control de acceso, copias de respaldo)." | OBL-SEG-01 a 06 (colaboradora, propietario MOD-015) |
| Riesgo inicial estimado | Seleccion unica (calculada con posibilidad de ajuste manual) | Se calcula automaticamente al guardar, editable por Legal o Delegado | Bajo / Medio / Alto | El calculo automatico no puede bajarse sin dejar un comentario obligatorio de justificacion | "El sistema sugiere un nivel de riesgo segun el tipo de dato y el volumen declarado. Es un apoyo, no una conclusion legal; usted puede ajustarlo dejando su razon." | Buena practica, alimenta OBL-DOC-03 (colaboradora, propietario MOD-014) |
| Requiere EIPD | Booleano (sugerido automaticamente, confirmable) | Se sugiere automaticamente | Si / No | Si el riesgo inicial es Alto o hay datos sensibles de biometria/salud/menores, se sugiere Si por defecto | "El sistema marca esta casilla cuando detecta un tratamiento de alto riesgo. Confirme si en efecto se necesita una Evaluacion de Impacto." | OBL-DOC-03 (colaboradora, propietario MOD-014) |
| Fecha de proxima revision | Fecha | Obligatorio para pasar a Vigente | Calculada por defecto a 12 meses desde la aprobacion, editable | No puede ser anterior a la fecha de aprobacion | "El sistema propone revisar esta ficha una vez al ano. Puede acortar el plazo si el tratamiento cambia con frecuencia." | Buena practica, apoya OBL-PRIN-03 |
| Documentos asociados | Referencia multiple a Documento (MOD-008) | Opcional | Aviso de privacidad vigente, Politica de privacidad, contrato/DPA del encargado | - | "Enlace el aviso de privacidad o el contrato que respalda este tratamiento, si ya existe." | OBL-AVISO-01 a 05 (colaboradora, propietario MOD-008) |
| Estado | Seleccion unica (controlado por el workflow) | Gestionado por el sistema | Ver seccion F | No editable directamente por el usuario | "Este campo cambia solo, segun el flujo de revision y aprobacion." | - |
| Historial de modificaciones | Solo lectura, generado por el sistema | Automatico | - | - | "Aqui puede ver todos los cambios que ha tenido esta ficha desde que se creo." | OBL-PRIN-03 |

### D.2 Catalogo de categorias de titulares [opinion de producto, no existe catalogo legal cerrado]

Empleados actuales | Ex empleados | Candidatos a un puesto (aplicantes) | Clientes | Ex clientes | Proveedores (personas naturales o contactos de proveedores) | Visitantes de instalaciones | Usuarios de sitio web o app movil | Menores de edad (dependientes de empleados o clientes) | Accionistas o socios | Contactos de emergencia de empleados | Beneficiarios de programas de fidelizacion | Otro (especificar).

### D.3 Catalogo de categorias de datos

Ordinarios: Identificativos (nombre, DUI, NIT) | Contacto (telefono, correo, direccion) | Laborales (puesto, salario, historial) | Financieros (cuentas, ingresos) | Comerciales (historial de compra) | Digitales / de navegacion (cookies, IP) | Ubicacion / geolocalizacion | Imagen no biometrica (fotografia simple) | Otros ordinarios (especificar).

Sensibles (union del catalogo enunciativo del Art. 4 lit. g y de las categorias listadas en el Art. 59 lit. b, ver seccion D.4): el sistema los marca automaticamente en rojo dentro del catalogo y no permite ocultarlos bajo una categoria "otros".

### D.4 Catalogo de datos sensibles (union Art. 4 lit. g y Art. 59 lit. b)

Esta union es una decision de diseno explicita del modulo: el Art. 4 lit. g) define "datos personales sensibles" de forma enunciativa y no limitativa; el Art. 59 lit. b) prohibe tratar sin las salvaguardas del Capitulo IV del Titulo II una lista parcialmente distinta (agrega "origen racial", separado de "origen etnico", y "nacionalidad" y "afiliacion partidaria", que el Art. 4 lit. g no menciona de forma expresa). Para no dejar un vacio de proteccion, el catalogo del RAT usa la union de ambas listas.

| Categoria sensible | Fuente | Efecto automatico en el RAT |
|---|---|---|
| Origen etnico | Art. 4 lit. g) | Marca sensible; exige justificacion de base legal (OBL-SENS-03 o consentimiento por escrito) |
| Origen racial | Art. 59 lit. b) | Marca sensible; mismo efecto |
| Nacionalidad | Art. 59 lit. b) | Marca sensible (nota: el DUI y pasaporte identificativos ordinarios no se remarcan como sensibles solo por incluir nacionalidad; el sistema pide confirmacion humana cuando el campo se declare como atributo de tratamiento diferenciado, ver seccion H) |
| Creencias o convicciones religiosas, espirituales o filosoficas | Art. 4 lit. g) y Art. 59 lit. b) | Marca sensible |
| Afiliacion o ideologia politica | Art. 4 lit. g) | Marca sensible |
| Afiliacion partidaria | Art. 59 lit. b) | Marca sensible (tratada junto con ideologia politica en el catalogo) |
| Afiliacion sindical | Art. 4 lit. g) | Marca sensible |
| Preferencias u orientacion sexual | Art. 4 lit. g) y Art. 59 lit. b) | Marca sensible |
| Salud fisica y mental | Art. 4 lit. g) y Art. 59 lit. b) | Marca sensible; dispara OBL-SENS-04 si el giro es de salud |
| Informacion biometrica | Art. 4 lit. g) | Marca sensible; dispara OBL-SENS-06 y OBL-SENS-07 (consentimiento escrito y alternativa no biometrica) |
| Informacion genetica | Art. 4 lit. g) | Marca sensible |
| Situacion moral y familiar | Art. 4 lit. g) | Marca sensible |
| Habitos personales | Art. 4 lit. g) | Marca sensible |
| Vida privada o intima (residual) | Art. 59 lit. b), "la vida" | Marca sensible; exige descripcion adicional porque es la categoria mas abierta |
| Otras informaciones intimas de similar naturaleza (clausula abierta, enunciativa) | Art. 4 lit. g) | El sistema no puede precalificar esta clausula; si el usuario marca "otro dato sensible no listado", el campo queda pendiente con la nota "Requiere validacion de la organizacion o asesoria especializada" (ver seccion H) |

Cuando se marca cualquiera de estas categorias, el sistema exige: (a) una justificacion escrita de la base de licitud (no basta elegir "Consentimiento" sin mas), (b) evaluar si aplica alguna de las tres excepciones del Art. 37 y 38 (OBL-SENS-03), (c) enlazar el control de seguridad correspondiente, y (d) sugerir automaticamente la EIPD.

### D.5 Catalogo "Analisis de fuente de acceso publico" (activado si origen = Fuente de acceso publico)

Campo de texto largo obligatorio con la pregunta guiada: "Explique por que esta fuente puede consultarse por disposicion de ley por cualquier persona (no basta con que sea publica o abierta en internet, por ejemplo una red social)". Fundamento: OBL-TRAT-03, Art. 4 lit. l). El sistema no valida el contenido; solo exige que exista el analisis, y muestra la advertencia "Requiere validacion de la organizacion o asesoria especializada".

### D.6 Biblioteca inicial de tratamientos plantilla

La biblioteca no reemplaza el registro real de la empresa: son fichas precargadas, editables, que aceleran la creacion de una actividad de tratamiento comun. Al elegir una plantilla, el sistema copia los valores sugeridos a una ficha nueva en estado Borrador; nada queda en estado Vigente sin que la empresa revise y confirme cada campo.

| # | Tratamiento plantilla | Area tipica | Finalidad sugerida | Categorias de titulares | Categorias de datos (sensibles en negrita) | Base de licitud sugerida | Origen tipico | Sistema tipico | Retencion sugerida | Riesgo inicial sugerido |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Nomina y pago de salarios | RRHH / Finanzas | Pagar el salario y cumplir obligaciones tributarias y de seguridad social | Empleados, ex empleados | Identificativos, contacto, laborales, financieros | Ejecucion de contrato / obligacion legal | Directamente del titular | Sistema de planillas | Duracion de la relacion + 10 anios (retencion tributaria, OBL-RET-02) | Medio |
| 2 | Reclutamiento y seleccion (CV) | RRHH | Evaluar candidatos para una vacante | Candidatos | Identificativos, contacto, laborales, **habitos personales (si el CV los incluye)** | Consentimiento expreso o medidas precontractuales | Formulario web o correo | Sistema de reclutamiento / correo | 6 a 12 meses tras el cierre del proceso | Bajo-Medio |
| 3 | Gestion de clientes (CRM) | Comercial / Ventas | Administrar la relacion comercial y dar seguimiento a oportunidades | Clientes, ex clientes | Identificativos, contacto, comerciales, financieros | Ejecucion de contrato / interes legitimo | Directamente del titular | CRM | Duracion de la relacion + plazo de prescripcion mercantil | Medio |
| 4 | Facturacion y contabilidad | Finanzas | Emitir comprobantes y cumplir obligaciones fiscales | Clientes, proveedores | Identificativos, contacto, financieros | Obligacion legal | Generado internamente / recibido del cliente | Sistema contable / facturacion electronica | 10 anios (OBL-RET-02) | Bajo |
| 5 | Marketing y campanas digitales | Marketing | Enviar promociones y medir campanas | Clientes, usuarios de sitio web | Identificativos, contacto, digitales/cookies | Consentimiento expreso | Formulario web, redes sociales | Plataforma de email marketing / CRM | Hasta revocacion del consentimiento | Medio |
| 6 | Videovigilancia de instalaciones | Seguridad / Operaciones | Proteger personas y bienes en las instalaciones | Empleados, visitantes, clientes | Imagen, **biometrico si hay reconocimiento facial** | Interes legitimo | Generado internamente (camaras) | Sistema de video (DVR/NVR o nube) | 30 a 90 dias salvo incidente en investigacion | Medio-Alto (Alto si hay reconocimiento facial) |
| 7 | Control de asistencia biometrico | RRHH | Registrar entrada y salida del personal | Empleados | **Biometrico (huella o rostro)** | Consentimiento expreso por escrito | Directamente del titular (captura biometrica) | Sistema de control de asistencia | Duracion de la relacion laboral | Alto |
| 8 | Aplicacion movil de la empresa | TI / Producto | Prestar el servicio o funcionalidad de la app | Clientes, usuarios | Identificativos, contacto, ubicacion, digitales | Ejecucion de contrato / consentimiento | Directamente del titular (registro en la app) | Backend de la app / proveedor cloud | Duracion de la cuenta activa + periodo de gracia | Medio |
| 9 | Atencion al cliente (call center / chat) | Servicio al cliente | Resolver consultas, quejas y solicitudes | Clientes | Identificativos, contacto, comerciales | Ejecucion de contrato | Directamente del titular | Sistema de mesa de ayuda / chat | 2 anios desde el ultimo contacto | Bajo |
| 10 | Cobranza y gestion de mora | Finanzas / Cobranza | Gestionar cuentas por cobrar vencidas | Clientes | Identificativos, contacto, financieros | Ejecucion de contrato / interes legitimo | Generado internamente | Sistema de cobranza / CRM | Duracion de la relacion + plazo de prescripcion | Medio |
| 11 | Salud ocupacional y examenes medicos | RRHH / Seguridad ocupacional | Cumplir obligaciones de salud y seguridad laboral | Empleados | **Salud fisica y mental** | Obligacion legal | Recibido de un tercero (clinica) o directamente del titular | Expediente medico ocupacional (fisico o sistema restringido) | Duracion de la relacion laboral + plazo sectorial de salud | Alto |
| 12 | Gestion de proveedores y contratistas | Compras | Administrar la relacion con proveedores | Contactos de proveedores | Identificativos, contacto, comerciales | Ejecucion de contrato | Directamente del titular | Sistema de compras / ERP | Duracion de la relacion + 10 anios (retencion mercantil, OBL-RET-01) | Bajo |
| 13 | Registro de visitantes | Seguridad / Recepcion | Controlar el acceso de personas externas a las instalaciones | Visitantes | Identificativos, contacto, imagen (si hay foto en bitacora) | Interes legitimo | Directamente del titular | Bitacora de recepcion (fisica o digital) | 30 a 90 dias | Bajo |
| 14 | Onboarding y expediente laboral del empleado | RRHH | Formalizar la contratacion y mantener el expediente laboral | Empleados | Identificativos, contacto, laborales, financieros | Ejecucion de contrato / obligacion legal | Directamente del titular | Sistema de RRHH / expediente fisico | Duracion de la relacion + 10 anios | Medio |
| 15 | Evaluacion de desempeno | RRHH | Medir el rendimiento del personal | Empleados | Laborales, **habitos personales (si se evaluan conductas)** | Ejecucion de contrato | Generado internamente | Sistema de RRHH | Duracion de la relacion + 2 anios | Bajo-Medio |
| 16 | Beneficios, planilla previsional y seguridad social | RRHH / Finanzas | Administrar AFP, ISSS y otros beneficios | Empleados | Identificativos, financieros, **salud (si hay seguro medico)** | Obligacion legal | Directamente del titular | Sistema de planillas / portal de la AFP-ISSS | Duracion de la relacion + 10 anios | Medio |
| 17 | Control de acceso fisico con tarjetas o codigos | Seguridad | Controlar el ingreso a areas restringidas | Empleados, visitantes | Identificativos, **biometrico si el lector usa huella** | Interes legitimo | Directamente del titular | Sistema de control de acceso | Duracion de la relacion o vigencia de la tarjeta | Bajo (Alto si es biometrico) |
| 18 | Programa de fidelizacion / lealtad | Marketing / Comercial | Administrar puntos y beneficios de clientes frecuentes | Clientes | Identificativos, contacto, comerciales | Consentimiento expreso | Directamente del titular (inscripcion) | Sistema de fidelizacion / CRM | Duracion de la membresia + 1 anio | Bajo |
| 19 | Encuestas de satisfaccion | Marketing / Calidad | Medir la satisfaccion de clientes o empleados | Clientes, empleados | Identificativos (opcional), contacto (opcional) | Consentimiento expreso o interes legitimo | Directamente del titular | Herramienta de encuestas | 12 meses | Bajo |
| 20 | Mesa de ayuda / soporte tecnico interno | TI | Resolver incidencias tecnicas del personal | Empleados | Identificativos, contacto, laborales | Ejecucion de contrato (relacion laboral) | Directamente del titular | Sistema de tickets internos | Duracion de la relacion + 1 anio | Bajo |
| 21 | Capacitaciones y evaluaciones de personal | RRHH | Registrar la formacion recibida por el personal | Empleados | Identificativos, laborales | Ejecucion de contrato / obligacion legal (OBL-CAP-01) | Generado internamente | Sistema de capacitacion (MOD-017) | Duracion de la relacion + 5 anios | Bajo |
| 22 | Gestion de flotas vehiculares (GPS / camaras a bordo) | Operaciones / Logistica | Monitorear vehiculos de la empresa por seguridad y eficiencia | Empleados (conductores) | Ubicacion, imagen, **biometrico si hay reconocimiento facial del conductor** | Interes legitimo | Generado internamente (dispositivo GPS/dashcam) | Plataforma de rastreo vehicular | 90 dias salvo incidente | Medio-Alto |

Nota de uso: cada fila de esta biblioteca es un punto de partida editable, no una obligacion de usar exactamente ese texto; el usuario debe ajustar finalidad, base de licitud y retencion a su caso real antes de pasar la ficha a "En revision". El sistema deja constancia en el historial de que la ficha se origino desde una plantilla y cual, para trazabilidad.

### D.7 Catalogo de sistemas (submodulo, fuente unica de alta)

| Campo | Tipo | Obligatorio | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Nombre del sistema | Texto | Obligatorio | Libre | Unico dentro de la organizacion | "Nombre con el que su equipo conoce el sistema, por ejemplo 'CRM Comercial' o 'Excel de nomina'." | Buena practica, evita duplicados (decision 2.7.17 de `02_validacion_de_la_idea.md`) |
| Tipo de sistema | Seleccion unica | Obligatorio | Interno (desarrollado o administrado por la empresa) / SaaS de un proveedor / Archivo fisico / Hoja de calculo u ofimatica / Otro | - | "Indique si el sistema lo administra su empresa, si es un servicio contratado, o si en realidad son documentos fisicos o una hoja de Excel." | Buena practica |
| Proveedor asociado (si es SaaS) | Referencia a Proveedor (MOD-009) | Condicional | Catalogo de proveedores de MOD-009 | Obligatorio si tipo = SaaS | "Si es un servicio contratado, enlacelo con el proveedor registrado en el modulo de Proveedores." | OBL-PROV-01 a 04 |
| Pais de alojamiento | Catalogo de paises | Obligatorio | Lista de paises, incluye "El Salvador" y "No se sabe / pendiente de confirmar" | - | "Indique en que pais estan los servidores. Si no lo sabe, marque 'pendiente de confirmar' y el sistema creara una tarea para averiguarlo." | Alimenta el Mapa de Datos y OBL-TRANSF-05 |
| Responsable tecnico interno | Referencia a Usuario | Obligatorio | Usuarios de la organizacion con rol Seguridad/IT o Administrador | - | "Quien administra el acceso y la configuracion de este sistema dentro de la empresa." | Buena practica |
| Estado | Seleccion unica | Gestionado por el sistema | Activo / En baja / Dado de baja | - | "Se actualiza cuando un sistema deja de usarse; los tratamientos que lo referencian reciben una alerta." | Buena practica |

**Minimizacion de datos personales.** El RAT y el Catalogo de Sistemas almacenan metadatos y referencias (categorias, nombres de sistemas, nombres de responsables internos), nunca los datos personales de los titulares del cliente ni copias de sus bases de datos (anti-feature 1 y 8). La unica excepcion es un adjunto puntual y estrictamente necesario para respaldar un analisis (por ejemplo, una captura anonimizada de un formulario), que debe marcarse explicitamente como tal y queda sujeto a control reforzado de acceso. Los campos que "podrian" contener datos personales si el usuario los llena mal (por ejemplo, "Descripcion breve" o "Justificacion de la base de licitud", si alguien pega ahi el nombre real de un titular por error) llevan una validacion de ayuda ("no escriba aqui nombres de personas concretas, describa el tratamiento en general") y quedan sujetos a revision antes de pasar a Vigente.

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Ficha de actividad de tratamiento | Todos los campos de la seccion D.1, con su historial | Pantalla / PDF exportable | Al crear o editar una ficha | Responsable de area, Delegado, Legal, Auditor |
| RAT consolidado | Listado de todas las actividades de tratamiento de la organizacion, filtrable por area, estado, base de licitud, riesgo | Tabla en pantalla / exportable a PDF y CSV | Bajo demanda o en la exportacion de evidencia | Delegado, Legal, Administrador, Auditor |
| Mapa de Datos (vista) | Visualizacion del RAT en la secuencia origen -> sistema -> area -> proveedor -> pais -> eliminacion, sin ser una base independiente | Diagrama interactivo en pantalla / exportable como imagen o PDF | Se recalcula en tiempo real a partir del RAT | Delegado, Legal, Gerencia (vista simplificada), Auditor |
| Alerta de tratamiento pendiente de revision | Notificacion cuando se vence la fecha de proxima revision o cuando un sistema referenciado se marca "Dado de baja" | Notificacion + tarea en MOD-021 | Automatico (ver seccion G) | Responsable de area, Delegado |
| Tarea "completar ficha de tratamiento" | Tarea con campos faltantes senalados | Tarea en MOD-021 | Al crear una ficha desde el diagnostico (MOD-004) o desde la biblioteca de plantillas | Responsable de area asignado |
| Indicador de riesgo por tratamiento | Bajo / Medio / Alto, con factores que lo explican | Etiqueta visible en la ficha y en el listado | Al guardar cambios en categorias de datos, volumen o base de licitud | Legal, Delegado, Gerencia (agregado) |
| Senal de tratamiento sin ficha de transferencia | Lista de tratamientos marcados "Hay transferencia: Si" sin registro correspondiente en MOD-010 | Alerta + tarea | Automatico, al cruzar RAT con MOD-010 (ver seccion G) | Delegado, Legal |
| Evento de auditoria | Registro de creacion, cambio de campo, cambio de estado, aprobacion, exportacion | Entrada en el historial y en el AuditLog transversal | En cada accion | Auditor, Administrador |
| Paquete de evidencia del RAT | RAT exportado con hash de integridad, historial de cambios y aprobaciones | ZIP con PDF/CSV + archivo de verificacion | Bajo demanda, para auditoria o requerimiento de la ACE | Auditor externo, ACE (a criterio de la empresa) |

---

## F. Workflow

### F.1 Diagrama ASCII de estados

```
                    +-------------+
                    |   BORRADOR  |<---------------------------+
                    +-------------+                            |
                          |                                     |
             (completa campos minimos)                          |
                          v                                     |
                    +--------------+                            |
                    | EN REVISION  |----(rechazada)--------------+
                    +--------------+
                          |
              (aprobador confirma, campos obligatorios OK)
                          v
                    +-------------+
                    |   VIGENTE   |<----------------------------+
                    +-------------+                             |
                       |      |                                 |
        (llega fecha   |      | (cambio material: base,          |
         de revision)  |      |  categoria sensible, sistema)    |
                       v      v                                 |
              +-------------------+                             |
              | REQUIERE REVISION |-----(se revisa y confirma)---+
              +-------------------+
                       |
            (deja de usarse el tratamiento)
                       v
              +-------------+
              |  ARCHIVADO  |
              +-------------+
                       |
          (se reactiva el mismo tratamiento)
                       v
                 vuelve a EN REVISION
```

### F.2 Tabla de transiciones

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (nuevo) | Crear ficha manualmente o desde plantilla/diagnostico | Nombre y area responsable definidos | Borrador | Responsable de area, Legal, Delegado, Administrador | Crea evento de auditoria "ficha creada"; si viene de MOD-004, enlaza el disparador del diagnostico |
| Borrador | Completar campos obligatorios de Borrador y enviar a revision | Todos los campos marcados "obligatorio desde Borrador" completos | En revision | Quien creo la ficha o el Responsable de area asignado | Crea tarea de revision para Legal/Delegado; notifica al Aprobador si el riesgo es Alto |
| En revision | Aprobar | Todos los campos "obligatorio para pasar a En revision" y los de Vigente completos; si hay dato sensible, debe existir justificacion; si el riesgo es Alto, debe existir decision explicita sobre EIPD | Vigente | Aprobador, Legal/Compliance (si es sensible), Delegado (recomendado por defecto para tratamientos de riesgo Alto) | Bloquea edicion directa de campos criticos (finalidad, base de licitud) sin pasar de nuevo por revision; registra aprobacion con identidad y fecha; dispara alertas a MOD-007/008/009/010/014/015/016 segun corresponda |
| En revision | Rechazar / devolver | El revisor deja un comentario obligatorio explicando que falta | Borrador | Aprobador, Legal/Compliance, Delegado | Crea tarea para el Responsable de area con el motivo del rechazo |
| Vigente | Llega la fecha de proxima revision | Automatico, disparado por el motor de plazos (MOD-023) | Requiere revision | Sistema (automatico) | Crea alerta y tarea al Responsable de area y al Delegado |
| Vigente | Cambio material detectado (nueva categoria sensible, cambio de base de licitud, nuevo sistema con pais distinto) | Automatico al guardar un cambio de esos campos | Requiere revision | Sistema (automatico) | La ficha sigue visible como referencia pero queda marcada "en revision" hasta reconfirmar; no bloquea a los modulos que la consultan, pero les muestra la marca de "pendiente de reconfirmacion" |
| Requiere revision | Confirmar sin cambios o con cambios menores | El revisor confirma que la informacion sigue siendo correcta o la actualiza | Vigente | Aprobador, Legal/Compliance, Delegado | Actualiza la fecha de proxima revision; registra evento de auditoria |
| Requiere revision | Actualizar con cambios materiales | Debe repetirse el flujo de aprobacion completo | En revision | Responsable de area | Igual que el flujo normal de En revision |
| Vigente / Requiere revision | Archivar (el tratamiento dejo de existir) | Debe declararse el motivo y la fecha de cese | Archivado | Administrador, Delegado, Legal/Compliance | No se elimina la ficha ni su historial; queda visible como referencia historica para auditoria; dispara revision en MOD-016 (retencion) sobre los datos ya tratados |
| Archivado | Reactivar (el tratamiento vuelve a ejecutarse) | - | En revision | Administrador, Delegado, Legal/Compliance | Conserva el historial anterior, agrega un nuevo periodo de vigencia |
| Borrador (sin historial de cambios de otro usuario) | Eliminar | Solo si nunca paso a En revision y nadie mas la edito | (eliminada) | Administrador | Solo estado permitido para borrado fisico; cualquier ficha que ya paso por revision no puede eliminarse, solo archivarse |

**Estados terminales y registros vinculados.** No existe un estado que elimine el historial. Archivado es el unico estado que representa "esto ya no se hace", pero conserva toda la ficha y su historial de forma indefinida como evidencia de responsabilidad demostrada (OBL-PRIN-03). Los modulos que referencian una ficha archivada (por ejemplo, un proveedor enlazado en MOD-009) reciben una alerta de que el tratamiento de origen se archivo, sin que eso borre la referencia historica.

---

## G. Automatizaciones

| # | Disparador | Condicion | Accion | Configurable por la empresa |
|---|---|---|---|---|
| 1 | Se marca una categoria de dato del catalogo sensible (seccion D.4) | Categoria pertenece a la union Art. 4 lit. g / Art. 59 lit. b | El sistema exige justificacion de base legal, sugiere revisar excepciones del Art. 37-38, y marca la ficha con la etiqueta "Dato sensible" visible en todo listado | No (regla legal fija); si es configurable el texto de ayuda mostrado |
| 2 | Se marca "Informacion biometrica" | - | Se sugiere automaticamente "Requiere EIPD: Si" y se crea una tarea "confirmar consentimiento escrito y alternativa no biometrica" enlazada a MOD-007 | No |
| 3 | Se marca "Salud fisica y mental" y el sector de la empresa (MOD-001) es salud | - | Se activa el aviso "revisar Ley de Deberes y Derechos de los Pacientes" con nota "Requiere validacion de la organizacion o asesoria especializada" (OBL-SENS-04) | No |
| 4 | Se registra un tratamiento con origen "camaras de seguridad" o categoria de dato "videovigilancia" | - | Se crea automaticamente el tratamiento con base de licitud sugerida "Interes legitimo" pendiente de confirmar, se enlaza a MOD-014 para EIPD si se marca reconocimiento facial, y se crea tarea en MOD-008 para verificar el aviso de videovigilancia visible | Si, la empresa puede editar la base sugerida antes de confirmar |
| 5 | Se marca "Hay transferencia fuera de El Salvador: Si" o el pais del sistema referenciado no es El Salvador | El tratamiento pasa a Vigente sin ficha correspondiente en MOD-010 | Se genera la alerta "Transferencia posiblemente no documentada" y una tarea para crear el registro en MOD-010 | No (control de deteccion), si es configurable el plazo de la tarea |
| 6 | Se elige base de licitud "Intereses legitimos" | - | Se exige el campo "Justificacion de la base de licitud" con la pregunta guiada de ponderacion frente al derecho del titular, y se muestra la advertencia de la seccion H | No |
| 7 | Llega la fecha de proxima revision (calculada por MOD-023) | Ficha en estado Vigente | Cambia el estado a "Requiere revision", crea tarea al Responsable de area y notifica al Delegado | Si, la empresa puede ajustar la periodicidad por defecto (12 meses) |
| 8 | Un sistema del Catalogo de Sistemas cambia a estado "Dado de baja" | Existen fichas Vigentes que lo referencian | Esas fichas pasan a "Requiere revision" con la nota "sistema dado de baja, confirme donde estan ahora estos datos" | No |
| 9 | Se completa el diagnostico (MOD-004) y una respuesta corresponde a una plantilla de la biblioteca (seccion D.6) | Existe correspondencia entre la respuesta y una plantilla | Se crea automaticamente una ficha en Borrador a partir de la plantilla y se asigna tarea al Responsable de area sugerido | Si, la empresa puede desactivar la creacion automatica y crear manualmente |
| 10 | Una ficha pasa a Vigente | El tratamiento involucra un encargado (proveedor tipo Encargado) | Se notifica a MOD-009 para verificar que exista contrato/DPA vigente; si no existe, se crea tarea | No |
| 11 | Una ficha pasa a Vigente con "Requiere EIPD: Si" confirmado | - | Se crea tarea en MOD-014 "elaborar EIPD para este tratamiento" | No |
| 12 | Se declara plazo de conservacion "Indefinido" | - | Se exige justificacion obligatoria y se marca la ficha con alerta permanente "revisar plazo de conservacion" hasta que se defina un plazo concreto o se confirme la excepcion | No |

---

## H. Decisiones que NO debe automatizar

| Decision | Por que exige criterio humano | Texto de advertencia que muestra el sistema |
|---|---|---|
| Si la base de licitud elegida (en particular "Intereses legitimos") es valida y proporcional para el tratamiento concreto | La ponderacion entre el interes de la empresa y los derechos del titular es un juicio juridico caso por caso; el sistema no puede medir "afectacion desproporcionada" (Art. 5 lit. g) | "La eleccion de esta base requiere el criterio de su organizacion sobre si es defendible para este tratamiento especifico. Requiere validacion de la organizacion o asesoria especializada." |
| Si un dato encaja o no en la clausula abierta "otras informaciones intimas de similar naturaleza" del Art. 4 lit. g) | Es una clausula enunciativa y no limitativa; solo un analisis humano puede decidir si un dato nuevo, no listado, cae dentro de esa categoria | "Este dato no esta en el catalogo cerrado de categorias sensibles. Requiere validacion de la organizacion o asesoria especializada antes de decidir si aplica el regimen reforzado." |
| Si una fuente califica como "fuente de acceso publico" bajo la definicion estricta del Art. 4 lit. l) | La ley exige que la consulta sea posible "por disposicion de ley", una condicion legal, no tecnica; una red social abierta no califica aunque sea publica | "El sistema no determina si esta fuente cumple la definicion legal de acceso publico. Requiere validacion de la organizacion o asesoria especializada." |
| Si el nivel de riesgo calculado automaticamente (Bajo/Medio/Alto) refleja el riesgo real del tratamiento | El calculo es un apoyo basado en factores declarados (tipo de dato, volumen, sensibilidad); no sustituye un analisis de riesgo completo | "Este resultado es un calculo de apoyo interno basado en los factores que usted registro. No es una conclusion juridica sobre el riesgo del tratamiento." |
| Si corresponde o no elaborar una EIPD para un tratamiento especifico | El sistema sugiere segun reglas simples (biometria, salud, menores, riesgo Alto); la decision final de necesidad y alcance de la EIPD es de MOD-014 y de la persona responsable | "El sistema sugirio esta EIPD segun reglas generales. La decision final sobre si se necesita, y su alcance, requiere validacion de la organizacion o asesoria especializada." |
| Si un tratamiento con datos de nacionalidad, etnia u origen debe tratarse como sensible en un caso concreto (por ejemplo, un campo "pais de nacimiento" en un formulario de RRHH que no busca perfilar) | El catalogo marca la categoria por default, pero el contexto de uso (perfilar vs. identificar) puede cambiar la calificacion | "El sistema marco este dato como potencialmente sensible por su categoria. Confirme con su organizacion si, en este caso concreto, aplica el regimen reforzado." |
| Si el plazo de conservacion declarado "Indefinido" tiene una justificacion legal suficiente | Requiere conocer la norma sectorial aplicable (tributaria, mercantil, laboral) que respalde ese plazo | "Un plazo de conservacion indefinido requiere una justificacion legal especifica. Requiere validacion de la organizacion o asesoria especializada." |

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Ficha de tratamiento pendiente de completar | Ficha en Borrador mas de 15 dias sin avanzar (configurable) | INFO | Responsable de area asignado | Plataforma + resumen semanal por correo | Semanal mientras siga pendiente | A los 30 dias, copia al Delegado | La ficha avanza a En revision o se archiva |
| Ficha esperando aprobacion | Ficha en En revision mas de 5 dias habiles sin decision | WARNING | Aprobador o Legal/Compliance asignado | Plataforma + correo | Cada 3 dias habiles | A los 10 dias habiles, escala al Delegado | La ficha pasa a Vigente o se rechaza |
| Revision periodica vencida | Fecha de proxima revision alcanzada y la ficha sigue "Requiere revision" sin confirmar | WARNING | Responsable de area y Delegado | Plataforma + correo | Semanal | A los 30 dias sin confirmar, al Administrador | La ficha se confirma o se actualiza |
| Tratamiento con dato sensible sin justificacion de base | Se intenta guardar una ficha con categoria sensible marcada y el campo de justificacion vacio | HIGH | Responsable de area | Bloqueo en pantalla (no permite guardar como En revision) | Inmediata | No aplica, es bloqueo, no notificacion diferida | Se completa el campo |
| Transferencia posiblemente no documentada | Regla G.5: tratamiento con transferencia declarada sin ficha correspondiente en MOD-010 | HIGH | Delegado y Legal/Compliance | Plataforma + correo | Al detectarse, luego semanal hasta resolver | A los 15 dias, al Administrador | Se crea la ficha en MOD-010 o se corrige la declaracion de transferencia |
| Sistema dado de baja con tratamientos vigentes enlazados | Cambio de estado de un sistema del catalogo | HIGH | Responsable de area y Seguridad/IT | Plataforma + correo | Inmediata al detectarse | A los 10 dias sin resolver, al Delegado | Todas las fichas afectadas se reconfirman con el sistema correcto |
| Dato biometrico sin control de seguridad enlazado | Ficha con categoria "Informacion biometrica" que intenta pasar a Vigente sin al menos un control de MOD-015 enlazado | HIGH | Responsable de area y Seguridad/IT | Plataforma | Inmediata (bloqueo de aprobacion) | No aplica, es bloqueo | Se enlaza el control |
| Plazo de conservacion indefinido sin justificacion | Regla D.1 / G.12 | WARNING | Responsable de area | Plataforma | Al guardar | A los 15 dias sin justificar, al Legal/Compliance | Se define un plazo o se justifica |
| RAT sin ninguna ficha Vigente 30 dias despues del diagnostico | Empresa completo el diagnostico (MOD-004) pero no tiene ninguna ficha en estado Vigente | CRITICAL | Administrador y Delegado | Plataforma + correo + resumen en dashboard Gerencia | Una vez, luego recordatorio quincenal | A los 45 dias, aparece en el resumen ejecutivo de Gerencia | Existe al menos una ficha Vigente |

---

## J. Evidencia

| Evidencia | Como se registra | Obligacion que prueba | Retencion |
|---|---|---|---|
| Ficha de tratamiento con historial completo de cambios | Registro con fecha, hora y usuario en cada edicion; version anterior y nueva de cada campo modificado | OBL-DOC-02 (RAT), OBL-PRIN-03 (responsabilidad demostrada) | Mientras el tratamiento este activo, y de forma indefinida tras archivarse (no se elimina el historial) |
| Justificacion escrita de la base de licitud | Campo de texto obligatorio, versionado, con autor y fecha | OBL-PRIN-02 (seis bases de licitud) | Igual que la ficha del tratamiento |
| Clasificacion de categoria de dato sensible | Marca automatica en el catalogo, con registro de quien confirmo la categoria | OBL-SENS-01, OBL-SENS-06, OBL-SENS-08 | Igual que la ficha del tratamiento |
| Registro de aprobacion (paso a Vigente) | Identidad del aprobador, fecha y hora, comentario si existe | OBL-PRIN-03 | Igual que la ficha del tratamiento |
| Analisis documentado de fuente de acceso publico | Campo de texto obligatorio, con autor y fecha, de la seccion D.5 | OBL-TRAT-03 | Igual que la ficha del tratamiento |
| Enlace a controles de seguridad de MOD-015 por tratamiento | Referencia con fecha de enlace | OBL-SEG-02 (colaboradora) | Igual que la ficha del tratamiento |
| Registro de deteccion de transferencia no documentada y su resolucion | Alerta generada, tarea creada, fecha de cierre | OBL-TRANSF-05, OBL-TRANSF-06 (colaboradoras, propietario MOD-010) | Igual que la ficha del tratamiento |
| Exportacion del RAT (paquete de evidencia) | Archivo exportado con hash o firma verificable, fecha de exportacion, usuario que exporto | OBL-PRIN-03; insumo de OBL-AUD-01 (propietario MOD-018) | 5 anios como minimo por defecto (regla general de retencion de evidencia de cumplimiento de `03_hallazgos_regulatorios.md`, seccion "expediente de descargo"), configurable si aplica otra norma conexa |
| Evento de auditoria por cada accion (creacion, edicion, cambio de estado, aprobacion, exportacion, acceso de lectura a ficha con datos sensibles) | Entrada append-only en el AuditLog transversal (MOD-019) | OBL-PRIN-03 | Segun la politica de retencion del AuditLog (MOD-019), nunca inferior a la de la ficha que documenta |

---

## K. Documentos asociados

- **Documentos requeridos como entrada:** ninguno es estrictamente obligatorio para crear una ficha en Borrador; para pasar a Vigente se recomienda, cuando exista, enlazar el Aviso de Privacidad vigente (MOD-008) y, si hay encargado externo, el contrato/DPA correspondiente (MOD-009).
- **Documentos generados:** ficha de tratamiento exportable en PDF; RAT consolidado exportable en PDF y CSV; Mapa de Datos exportable como imagen o PDF; paquete de evidencia del RAT (ZIP con verificacion de integridad).
- **Plantillas que el sistema provee:**
  - Biblioteca de 22 tratamientos plantilla (seccion D.6), cada una con nombre, area, finalidad sugerida, base de licitud sugerida y demas campos precargados; requiere revision y confirmacion de la organizacion antes de pasar a Vigente.
  - Plantilla de "Analisis de base de interes legitimo" (pregunta guiada de ponderacion), asociada al campo de justificacion cuando se elige esa base; requiere validacion de la organizacion o asesoria especializada.
  - Plantilla de "Analisis de fuente de acceso publico" (seccion D.5); requiere validacion de la organizacion o asesoria especializada.
- **Anexos y evidencias documentales:** adjuntos puntuales estrictamente necesarios (por ejemplo, una captura anonimizada de un formulario de captura de datos), sujetos a control reforzado de acceso segun la seccion D.7.

---

## L. Dependencias

```
MOD-004 Diagnostico ------------------> MOD-006 RAT y Mapa de Datos
   (respuestas disparan tratamientos)        |
                                              |------> MOD-007 Consentimiento (finalidad y base declaradas)
                                              |------> MOD-008 Documentos (Aviso de Privacidad usa categorias/finalidades)
                                              |------> MOD-009 Proveedores (que tratamiento delega a cada encargado)
                                              |------> MOD-010 Transferencias (deteccion de transferencia no documentada)
                                              |------> MOD-013 Incidentes (que tratamiento se vio afectado)
                                              |------> MOD-014 Riesgos / EIPD (que tratamiento dispara evaluacion)
                                              |------> MOD-015 Controles (que control protege que tratamiento)
                                              |------> MOD-016 Retencion (plazo declarado alimenta el motor)
                                              |------> MOD-018 Auditoria (RAT como evidencia central)

Capa transversal consultada: MOD-001 (organizacion, areas, usuarios), MOD-021 (tareas),
MOD-022 (notificaciones), MOD-023 (plazos y fecha de revision), MOD-024 (estado normativo),
MOD-025 (busqueda), MOD-026 (ayuda contextual). MOD-006 escribe eventos hacia ellos, nunca al reves.
```

- **De que modulos recibe datos:** MOD-004 (Diagnostico) crea fichas Borrador a partir de las respuestas del cuestionario guiado; MOD-001 provee el catalogo de areas y usuarios; MOD-009 provee el catalogo de proveedores tipo Encargado; MOD-015 provee el catalogo de controles.
- **A que modulos envia datos o eventos:** los nueve modulos listados en `mapa_modulos.json` como `alimenta_a` (MOD-007 a MOD-010, MOD-013 a MOD-016, MOD-018), todos por lectura de referencia, nunca por escritura duplicada (regla 6 de la seccion 2 de `06_mapa_definitivo_de_modulos.md`).
- **Que catalogos comparte:** el Catalogo de Sistemas (seccion D.7) es propio de MOD-006 pero se consulta por referencia desde MOD-009 (Proveedores) y MOD-013 (Incidentes), evitando que cada modulo mantenga su propia lista de sistemas con texto libre (decision 2.7.17, faltante 19).
- **Que ocurre si el modulo dependiente no existe en el MVP:** todos los modulos que alimenta MOD-006 (MOD-007, MOD-008, MOD-009, MOD-015, MOD-016, MOD-018) son MUST HAVE o SHOULD HAVE con cobertura parcial declarada en `06_mapa_definitivo_de_modulos.md`, por lo que ninguno esta ausente del MVP. La unica dependencia SHOULD HAVE completa es MOD-010 (Transferencias): mientras no exista el modulo completo, la alerta "transferencia posiblemente no documentada" de MOD-006 sigue funcionando (cruza el campo "Hay transferencia" del RAT con el pais del sistema del Catalogo), pero en vez de crear una ficha formal en MOD-010 crea una tarea manual en MOD-021 con evidencia suelta en MOD-019, igual que describe la cobertura parcial de MOD-010.

---

## M. Dashboard

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Cobertura del RAT | Tratamientos detectados por el diagnostico con ficha Vigente / total de tratamientos detectados por el diagnostico | Verde mayor a 80%, amarillo 50-80%, rojo menor a 50% | Gerencia (resumen), Responsable (detalle por area), Legal (detalle completo), Auditor (historico) |
| Tratamientos por base de licitud | Conteo de fichas Vigentes agrupado por base de licitud elegida | Sin semaforo, grafico de distribucion | Legal, Delegado |
| Tratamientos con dato sensible | Conteo de fichas Vigentes con al menos una categoria sensible marcada | Amarillo si mas del 30% del total no tiene EIPD confirmada, rojo si mas del 50% | Legal, Delegado, Gerencia (agregado) |
| Fichas pendientes de revision periodica | Conteo de fichas en estado "Requiere revision" | Verde 0, amarillo 1-5, rojo mas de 5 | Responsable (su area), Delegado (toda la organizacion) |
| Transferencias posiblemente no documentadas | Conteo de alertas activas de la regla G.5 sin resolver | Verde 0, rojo mayor a 0 | Delegado, Legal, Auditor |
| Sistemas sin pais confirmado | Conteo de sistemas del catalogo con pais "pendiente de confirmar" | Amarillo si hay alguno, rojo si supera 3 | Seguridad/IT, Delegado |
| Antiguedad promedio del RAT | Dias transcurridos desde la ultima revision confirmada, promedio de todas las fichas Vigentes | Verde menor a 180 dias, amarillo 180-365, rojo mayor a 365 | Gerencia, Auditor |

Ningun indicador se expresa como "porcentaje de cumplimiento legal"; todos describen estado del programa (cobertura del registro, madurez de revision, evidencia disponible), conforme al principio de `04_objetivo_exacto_del_producto.md` seccion "Como se mide el exito".

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| RAT consolidado | Todas las fichas con sus campos principales | Area, estado, base de licitud, sensibilidad, riesgo | PDF, XLSX/CSV | Delegado, Legal, Gerencia, Auditor | Si |
| RAT de datos sensibles | Solo fichas con categoria sensible marcada, con su justificacion y controles enlazados | Categoria sensible, area | PDF | Legal, Delegado, Auditor | Si |
| Mapa de Datos exportado | Visualizacion origen -> sistema -> area -> proveedor -> pais -> eliminacion | Area, pais, tipo de sistema | PDF / imagen | Gerencia, Delegado, Auditor externo | Si |
| Reporte de transferencias no documentadas | Lista de alertas de la regla G.5, con fecha de deteccion y estado de resolucion | Estado (abierta/cerrada), fecha | PDF / CSV | Delegado, Legal | Si |
| Historial de cambios de una ficha | Version anterior y nueva de cada campo, autor y fecha | Rango de fechas | PDF | Auditor, Legal | Si |
| Paquete de evidencia del RAT | RAT consolidado + historial + aprobaciones + verificacion de integridad | - | ZIP con archivo de verificacion (hash) | Auditor externo, ACE (a criterio de la empresa) | Es el paquete mismo |

---

## O. Historial

Eventos que quedan en el historial de la ficha de tratamiento y en el AuditLog transversal (MOD-019):

| Evento | Que OBL-ID ayuda a probar |
|---|---|
| Creacion de la ficha (manual, desde plantilla o desde el diagnostico) | OBL-DOC-02 |
| Cambio de cualquier campo, con valor anterior y nuevo, autor y fecha | OBL-PRIN-03 |
| Cambio de estado (Borrador -> En revision -> Vigente -> Requiere revision -> Archivado) | OBL-PRIN-03 |
| Asignacion de responsable interno o de tarea de completar campo | OBL-PRIN-03 |
| Aprobacion (paso a Vigente), con identidad, fecha y comentario si existe | OBL-PRIN-02, OBL-PRIN-03 |
| Adjunto de evidencia (analisis de base legal, analisis de acceso publico) | OBL-PRIN-02, OBL-TRAT-03 |
| Exportacion del RAT o de una ficha individual, con identidad de quien exporto | OBL-PRIN-03 |
| Acceso de lectura a una ficha con datos sensibles por un rol distinto al Responsable de area o Legal/Delegado (por ejemplo, un Asesor externo invitado) | OBL-SENS-05 (evita revelar datos conocidos por razon del cargo sin control) |
| Eliminacion (solo posible en Borrador sin historial previo) | OBL-PRIN-03 (transparencia de que no hay borrado de fichas ya revisadas) |
| Archivado, con motivo declarado | OBL-PRIN-03 |
| Deteccion y cierre de una alerta de transferencia no documentada | OBL-TRANSF-05, OBL-TRANSF-06 |

---

## P. Riesgos

| Tipo | Riesgo | Mitigacion de diseno |
|---|---|---|
| Legal | Que el sistema, al sugerir automaticamente una base de licitud (por ejemplo "Interes legitimo" para videovigilancia), sea interpretado como una validacion legal de esa base | Toda sugerencia automatica queda etiquetada como sugerencia editable, con la advertencia de la seccion H, y exige justificacion humana antes de pasar a Vigente |
| Legal | Que la clausula abierta de datos sensibles (Art. 4 lit. g, "otras informaciones intimas de similar naturaleza") quede sin cubrir porque el catalogo cerrado no la contempla | Opcion explicita "otro dato sensible no listado" en el catalogo D.3, que fuerza la advertencia de validacion especializada en vez de dejarlo fuera del RAT |
| UX | Que el formulario de alta de una ficha de tratamiento sea tan extenso (mas de 25 campos posibles) que el Responsable de area lo abandone | Solo un subconjunto reducido de campos es obligatorio para Borrador; el resto se exige progresivamente al avanzar de estado, y la biblioteca de plantillas precarga la mayoria de los campos |
| UX | Que un usuario no especialista no entienda la diferencia entre "categoria de dato" y "base de licitud" y mezcle ambos conceptos | Textos de ayuda con ejemplos concretos en cada campo (seccion D), mas la Ayuda contextual (seccion R) |
| Operativo | Que la fecha de proxima revision se calcule mal por un calendario de plazos desactualizado | El calculo de la fecha usa el motor de plazos compartido (MOD-023), nunca una fecha calculada localmente dentro de MOD-006 |
| Operativo | Que un tratamiento quede huerfano porque su Responsable de area sale de la empresa y nadie reasigna la ficha | Alerta automatica cuando un usuario referenciado como responsable se desactiva en MOD-001, con tarea de reasignacion al Administrador |
| Seguridad y privacidad | Que un adjunto puntual (por ejemplo, una captura de pantalla de un formulario) termine conteniendo datos personales reales de un titular, en contra del principio de minimizacion | Validacion de ayuda visible en el campo de adjuntos ("no suba aqui datos reales de un titular"), mas control de acceso reforzado y revision del Aprobador antes de Vigente |
| Seguridad y privacidad | Que el Mapa de Datos, al mostrar pais y proveedor de cada sistema, exponga informacion sensible de la infraestructura de la empresa a un usuario con permisos insuficientes | Los permisos de lectura del Mapa de Datos siguen exactamente los mismos roles que el RAT (seccion C); nunca es visible desde el Portal del Titular (MOD-012) ni desde el rol Usuario de consulta |

---

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Ficha de actividad de tratamiento (campos basicos: nombre, area, finalidad, base de licitud, categorias, sistema) | X | | | | Es la obligacion OBLIGATORIO directa (OBL-DOC-02) y la base de la que dependen 9 modulos |
| Catalogo cerrado de categorias de datos sensibles (union Art. 4 lit. g / Art. 59 lit. b) con marcado automatico | X | | | | Obligacion directa OBL-SENS-01, OBL-SENS-06; sin esto el resto de reglas de datos sensibles no puede dispararse |
| Seleccion obligatoria de una de las seis bases de licitud con justificacion | X | | | | OBL-PRIN-02, riesgo de infraccion (Art. 56 lit. c num. 1) |
| Workflow de estados (Borrador, En revision, Vigente, Requiere revision, Archivado) con aprobacion | X | | | | Evidencia de responsabilidad demostrada (OBL-PRIN-03) y de doble control en datos sensibles |
| Catalogo de sistemas (alta y edicion unica) | X | | | | Dependencia estructural: sin el, RAT, Proveedores e Incidentes duplicarian el mismo dato de sistema en texto libre |
| Biblioteca inicial de tratamientos plantilla (minimo 20) | X | | | | Reduce drasticamente el esfuerzo de alta manual, clave para adopcion por usuarios no especialistas; sin ella el riesgo de abandono del RAT es alto |
| Deteccion de transferencia posiblemente no documentada (cruce RAT-Catalogo de Sistemas por pais) | | X | | | Depende de la existencia de MOD-010 completo para convertirse en ficha formal; en el MVP genera solo alerta y tarea manual, cobertura parcial ya declarada en el mapa de modulos |
| Mapa de Datos como visualizacion interactiva completa (diagrama navegable) | | X | | | La informacion ya existe desde el MVP en el RAT tabular; la vista grafica interactiva agrega valor de UX pero no es indispensable para cumplir OBL-DOC-02 |
| Exportacion de RAT con verificacion de integridad (hash) | X | | | | Requisito transversal de anti-feature 25 y de la funcion probatoria del modulo; sin integridad verificable el paquete de evidencia pierde valor ante una auditoria |
| Calculo automatico de riesgo inicial (Bajo/Medio/Alto) | | X | | | Utilidad real desde el MVP, pero puede lanzarse con una regla simple (basada solo en presencia de dato sensible) y refinarse despues sin romper compatibilidad |
| Recalculo dinamico de riesgo con factores de volumen y ponderacion configurable por la empresa | | | X | | Mejora de precision del calculo de riesgo, no indispensable para el MVP, util en V1 |
| Version multi-sociedad del RAT (comparar RAT entre varias empresas de un mismo grupo) | | | | X | Declarado Enterprise en `05_tipos_de_usuario.md` (perfil Directora de Cumplimiento Corporativo), no forma parte del MVP |
| Sugerencia automatica de riesgo por aprendizaje sobre el historico de tratamientos de la industria | | | | X | Funcionalidad especulativa sin base normativa ni de producto validada; queda fuera de todo alcance previsible |
| Integracion tecnica que descubra automaticamente sistemas y bases de datos de la empresa (escaneo de red o de esquemas) | | | | X | Fuera del alcance funcional de la fase actual y del principio de no ejecutar herramientas tecnicas de descubrimiento (mas cercano a un SIEM que a este producto, ver anti-feature 2) |

**Version minima vendible del modulo (MVP).** El RAT con ficha completa de tratamiento (campos basicos, catalogo de datos sensibles, seis bases de licitud con justificacion, workflow de aprobacion), el Catalogo de Sistemas y la biblioteca de al menos 20 tratamientos plantilla, mas la exportacion con verificacion de integridad. Esto ya es vendible de forma independiente porque cubre por si solo la obligacion OBLIGATORIO mas transversal del corpus (OBL-DOC-02) y desbloquea el uso de otros ocho modulos MUST HAVE. El Mapa de Datos como diagrama interactivo y el motor de deteccion automatica de transferencias con ficha formal en MOD-010 pueden diferirse a V1 sin dejar un vacio legal, porque la misma informacion ya es consultable en el RAT tabular desde el primer dia.

---

## R. Ayuda contextual (complemento obligatorio)

**1. Que es el RAT (Registro de Actividades de Tratamiento)**
- Que es: es la lista ordenada de todo lo que su empresa hace con datos personales, actividad por actividad (por ejemplo, "pagar nomina" es una actividad, "atender clientes por chat" es otra).
- Por que tengo que hacer esto: porque es la unica forma de saber, en cualquier momento, que datos tiene su empresa, para que los usa y si los esta cuidando bien; sin esto, no puede responder ni a un titular ni a una auditoria.
- Fundamento: OBL-DOC-02, Politicas de Actuacion ACE Art. 4 (Medidas Organizativas, lit. d).
- Cuando necesito ayuda juridica: cuando no este seguro de si un tratamiento nuevo necesita una base de licitud distinta a la que ya usa para otros, o si dos actividades parecidas deben registrarse por separado.

**2. Que es una base de licitud**
- Que es: es la razon legal por la que su empresa puede tratar un dato personal sin cometer una infraccion. La ley reconoce seis razones validas: consentimiento, contrato, obligacion legal, proteccion de la vida, interes publico, o interes legitimo.
- Por que tengo que hacer esto: porque tratar datos personales sin una razon valida es una infraccion sancionable; elegir la base correcta tambien le dice que otras obligaciones se activan (por ejemplo, si elige consentimiento, debe poder demostrarlo).
- Fundamento: OBL-PRIN-02, Art. 5 lit. g) LPDP.
- Cuando necesito ayuda juridica: cuando duda entre "interes legitimo" y "consentimiento", o cuando su empresa quiere usar una base distinta a la que uso para un tratamiento parecido en el pasado.

**3. Que es un dato personal sensible**
- Que es: es un tipo de dato que, si se usa mal, puede afectar gravemente a la persona: su salud, sus creencias, su origen etnico, su orientacion sexual, su informacion biometrica (huella o rostro), entre otros. La ley exige cuidados adicionales para estos datos.
- Por que tengo que hacer esto: porque tratarlos sin las salvaguardas adecuadas (por ejemplo, sin consentimiento por escrito) es una de las infracciones mas graves de la ley.
- Fundamento: OBL-SENS-01, Art. 4 lit. g) y Art. 59 lit. b) LPDP.
- Cuando necesito ayuda juridica: cuando no esta seguro de si un dato nuevo (por ejemplo, "pais de nacimiento" o "estado civil") cae dentro de esta categoria en su caso concreto.

**4. Que es el Mapa de Datos**
- Que es: es una forma visual de ver la misma informacion del RAT, mostrando el recorrido de un dato: de donde viene, en que sistema esta, que area lo administra, si pasa por un proveedor, en que pais termina, y cuando se elimina.
- Por que tengo que hacer esto: porque a veces es mas facil detectar un problema (por ejemplo, un dato que termina en un servidor fuera de El Salvador sin que nadie lo haya documentado formalmente) viendolo en un diagrama que leyendo una tabla.
- Fundamento: buena practica de producto, apoyada indirectamente en OBL-TRANSF-05 (deteccion de transferencias no documentadas, Art. 45) y en el principio de responsabilidad demostrada (OBL-PRIN-03).
- Cuando necesito ayuda juridica: cuando el Mapa de Datos le senale una transferencia posiblemente no documentada; antes de decidir que hacer, consulte con Legal o con su Delegado.

**5. Que es el Catalogo de Sistemas**
- Que es: es la lista unica de todos los programas, aplicaciones, archivos o servicios donde su empresa guarda o procesa datos personales (por ejemplo, el CRM, el sistema de planillas, o incluso un archivo de Excel).
- Por que tengo que hacer esto: porque si cada area describe sus sistemas con nombres distintos y sueltos, nadie puede saber realmente cuantos sistemas hay ni donde estan los datos; tener una sola lista evita duplicados y confusiones.
- Fundamento: buena practica de producto, apoyada en la exigencia de mantener el RAT actualizado (OBL-DOC-02).
- Cuando necesito ayuda juridica: no suele requerirla; es una decision operativa. Si surge duda sobre si un sistema esta fuera de El Salvador, consulte con Legal antes de confirmar el pais.

**6. Que significa "requiere revision periodica"**
- Que es: es el estado que toma automaticamente una ficha de tratamiento cuando se cumple un anio desde su ultima confirmacion, o cuando cambia algo importante (por ejemplo, se agrega un dato sensible nuevo o se da de baja el sistema donde vivia el dato).
- Por que tengo que hacer esto: porque un RAT desactualizado deja de ser evidencia confiable; la ley espera que la empresa mantenga esta informacion viva, no que la llene una sola vez y la olvide.
- Fundamento: OBL-PRIN-03 (responsabilidad demostrada, Art. 5 lit. i), que exige mantener evidencia vigente del cumplimiento, no solo evidencia historica.
- Cuando necesito ayuda juridica: si el cambio detectado modifica la base de licitud o la clasificacion de sensibilidad del tratamiento, revise con Legal antes de confirmar la ficha como vigente de nuevo.

---

## Nota final de desacuerdos o hallazgos frente a las fuentes de diseno

1. **Union de catalogos Art. 4 lit. g) y Art. 59 lit. b) para datos sensibles.** El mapa definitivo de modulos y la matriz de obligaciones no especifican explicitamente que el catalogo de categorias sensibles del RAT deba construirse como la union de ambos articulos; esta ficha lo hace por instruccion directa de la tarea asignada. Se senala como decision de diseno explicita (no como hallazgo de error), documentada en la seccion D.4, porque el Art. 59 lit. b) agrega "origen racial", "nacionalidad" y "afiliacion partidaria" que el Art. 4 lit. g) no menciona de forma literal.
2. **Retencion del paquete de evidencia del RAT.** `03_hallazgos_regulatorios.md` fija 5 anios como retencion minima por defecto para "todo expediente de evidencia de cumplimiento", por analogia con el plazo de prescripcion sancionadora (OBL-RET-07, sin norma expresa). Esta ficha aplica ese mismo criterio al paquete de evidencia exportado del RAT (seccion J), pero senala que, a diferencia del expediente ARCO-POL o de incidentes (que sí tienen un limite de vida util claro: el caso se cierra), el RAT mismo es un documento vivo que se sigue actualizando indefinidamente; lo que prescribe a los 5 anios es cada version exportada como evidencia puntual, no el registro activo. No se identifico ninguna fuente que resuelva esta distincion de forma expresa; se deja constancia por si el equipo de producto o legal prefiere un criterio distinto.
3. **Nombre exacto de las 12 obligaciones colaboradoras.** `mapa_modulos.json` lista a OBL-ARCO-03 como colaboradora de MOD-006 (el RAT ayuda a saber en que sistema esta el dato a rectificar), pero su texto en `matriz_obligaciones.json` no menciona al RAT de forma expresa; la relacion es una inferencia funcional razonable (para rectificar, hay que saber donde esta el dato), no una obligacion textual que cite al RAT. Se deja constancia para que quede claro que ese enlace es interpretativo, no literal del articulo.
4. **Biblioteca de tratamientos plantilla.** La instruccion pidio un minimo de 20 tratamientos; esta ficha entrega 22, incluyendo control de acceso fisico, programa de fidelizacion, encuestas de satisfaccion, mesa de ayuda, capacitaciones y flotas vehiculares ademas de los 13 ejemplos explicitos de la tarea, para dar una biblioteca mas representativa de una pyme o empresa mediana salvadorena. Ningun valor de esa biblioteca esta verificado contra un caso real; son plantillas de referencia editables, marcadas como tales en la seccion D.6.
