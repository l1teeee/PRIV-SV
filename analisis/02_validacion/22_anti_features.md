# 22. Anti-features

Fecha: 2026-09-24. Fase: analisis funcional (sin codigo, sin stack, sin base de datos).

Fuentes base: `00_contexto_para_agentes.md`, `00_prompt_analisis_funcional.md`, `PROMPT_BASE_SISTEMA_PROTECCION_DATOS_EL_SALVADOR.md`, `01_legal\matriz_obligaciones.md` / `matriz_obligaciones.json` (105 obligaciones, IDs canonicos OBL-AREA-NN) y `01_legal\03_hallazgos_regulatorios.md`. Alineado con las decisiones de alcance de `02_validacion_de_la_idea.md`, seccion 2.7.

Lista razonada de lo que el producto no debe ser ni hacer. Cada item indica su razon (legal, de producto, de seguridad o de privacidad) y la alternativa que si se ofrece.

| # | El producto NO debe... | Razon | Alternativa que si se ofrece |
|---|---|---|---|
| 1 | Ser un CRM de los clientes de la empresa que lo usa | Producto | Registrar metadatos del tratamiento (que sistema, quien lo administra, categorias, retencion), sin duplicar la base de clientes del cliente |
| 2 | Ser un SIEM ni una herramienta de monitoreo de seguridad en tiempo real | Seguridad, Producto | Catalogo de controles donde la empresa registra evidencia de que el control existe, su responsable y su vigencia |
| 3 | Sustituir al abogado ni emitir dictamenes juridicos vinculantes | Legal | Mostrar el fundamento normativo (OBL-ID y articulo) y marcar la decision como "requiere validacion de asesoria especializada" cuando sea juridica |
| 4 | Actuar como el Delegado de Proteccion de Datos del cliente ni ejercer sus funciones legales (Arts. 15, 17, 29 Lineamientos DPO) | Legal | Ser la herramienta que usa la persona (interna o externa) designada formalmente como Delegado; el nombramiento y la investidura legal son del cliente, no del proveedor del software |
| 5 | Declarar un porcentaje de cumplimiento legal (0 a 100%) | Legal, Producto | Mostrar estado del programa: controles configurados, tareas pendientes, evidencia disponible |
| 6 | Decidir automaticamente si una base juridica es valida para un tratamiento concreto | Legal | Registrar la base elegida por la empresa y mostrar una nota de riesgo cuando exista ambiguedad legal conocida, dejando la decision al usuario |
| 7 | Resolver automaticamente (aceptar o denegar) solicitudes ARCO-POL sin intervencion humana | Legal | Calcular plazos, mostrar las causales tasadas por la ley y preparar el borrador de respuesta; el responsable interno decide y aprueba |
| 8 | Copiar o centralizar la base de datos completa del cliente (por ejemplo, toda la base de un CRM o un ERP) | Privacidad, Seguridad | Registrar solo metadatos del tratamiento: donde esta el dato, quien lo administra, categorias y retencion |
| 9 | Almacenar dentro del sistema los datos biometricos, de salud u otros datos sensibles de los titulares del cliente | Privacidad, Seguridad | Registrar la existencia del tratamiento, su base legal (OBL-SENS-06, OBL-SENS-07) y su ubicacion, no el dato sensible en si, salvo un adjunto puntual estrictamente necesario para un expediente ARCO-POL, con controles reforzados |
| 10 | Operar como plataforma de videovigilancia ni almacenar las grabaciones de camaras | Seguridad, Producto | Registrar el tratamiento de videovigilancia (OBL-SENS-08), su base legal y su EIPD, nunca las imagenes mismas |
| 11 | Ejecutar controles tecnicos de seguridad en los sistemas del cliente (parchear, cifrar, hacer backups, configurar firewalls) | Seguridad, Producto | Ofrecer el catalogo de controles donde la empresa registra la evidencia de que el control existe y quien lo administra |
| 12 | Emitir la certificacion oficial de Delegado de Proteccion de Datos | Legal | Recordar el tramite y sus plazos (por ejemplo, 15 dias habiles de comunicacion a la ACE) y enlazar al canal oficial de la ACE |
| 13 | Presentar tramites o comunicaciones directamente ante la ACE en nombre de la empresa sin que esta lo autorice y ejecute (por ejemplo, la puesta en conocimiento del Art. 45) | Legal, Seguridad | Preparar el contenido y dejar evidencia del intento de cumplimiento; la empresa presenta el tramite por el canal oficial (que, a la fecha de este analisis, la ACE aun no ha habilitado formalmente) |
| 14 | Asumir que la reforma 659 esta vigente antes de que se confirme su publicacion en el Diario Oficial | Legal | Doble estado configurable (ACTUAL / FUTURO) con activacion manual y registro de la fecha del cambio |
| 15 | Dar consultoria general de seguridad informatica (pentesting, hardening de servidores) | Producto, Seguridad | Recomendar contratar un proveedor especializado y registrar el resultado de ese trabajo como evidencia dentro del catalogo de controles |
| 16 | Ser una plataforma multipais de talla unica que aplique reglas de otras jurisdicciones (por ejemplo GDPR) al caso salvadoreno | Legal, Producto | Motor de reglas separado por pais (nucleo comun mas "paquete regulatorio" de El Salvador), sin mezclar plazos ni catalogos de otra jurisdiccion mientras el analisis se limite a El Salvador |
| 17 | Sustituir la firma o aprobacion formal de un contrato o DPA por parte de las personas legalmente facultadas de la empresa | Legal | Generar el borrador y dejar el flujo de aprobacion interna a cargo del responsable designado por la empresa |
| 18 | Calificar por si mismo si un tercero o un pais representa "nivel de proteccion adecuado" bajo el Art. 44 | Legal | Mostrar un cuestionario de factores de riesgo y dejar la conclusion marcada como "pendiente de validacion por la organizacion o por asesoria legal" |
| 19 | Permitir que un usuario borre o modifique el historial de auditoria | Seguridad | Bitacora de solo escritura por adicion (append-only), visible para Auditor y Administrador, sin funcion de edicion ni borrado para ningun rol |
| 20 | Exponer un canal de solicitudes ARCO-POL sin ninguna verificacion minima de identidad | Seguridad, Privacidad | Flujo de verificacion de identidad configurable segun el canal (por ejemplo, adjuntar DUI o verificar por el correo previamente registrado), documentado como parte del expediente, distinguiendo los tres tipos de solicitante del Art. 6 |
| 21 | Convertirse en un servicio donde el proveedor administra las solicitudes ARCO-POL del cliente ("outsourcing de privacidad") como parte del producto base | Producto, Legal | Mantenerse como herramienta de autogestion; cualquier servicio de asesoria externa se ofreceria por separado, fuera del software y prestado por terceros claramente identificados como tales |
| 22 | Usar en su comunicacion comercial frases como "cumplimiento garantizado" o "blindaje legal 100%" | Legal, Producto | Comunicar la propuesta de valor como organizacion, evidencia y trazabilidad, nunca como garantia de un resultado legal |
| 23 | Tratar datos de distinta sensibilidad de forma identica dentro de un mismo formulario o tratamiento (por ejemplo, equiparar datos de salud con datos de contacto, o marcar toda la categoria RRHH/laboral como sensible sin distincion) | Legal, Privacidad | Catalogo de categorias de datos con el nivel de sensibilidad marcado explicitamente por subconjunto (salud, biometria, afiliacion sindical), y reglas de consentimiento reforzado cuando corresponda (OBL-SENS-01 a OBL-SENS-08) |
| 24 | Comprometer el diseno de navegacion a un modelo fijo de niveles de usuario (por ejemplo, tres niveles Basico/Intermedio/Especialista) sin haberlo validado con usuarios reales no juristas | Producto | Probar la segmentacion de complejidad con usuarios reales antes de fijarla; mientras tanto, todo texto de cara al usuario cumple el principio de transparencia del Art. 5 lit. e (sin textos extensos, terminologia tecnica ni letra pequena) |
| 25 | Exportar un paquete de evidencias sin ningun mecanismo que permita verificar despues que no fue alterado | Seguridad, Legal | Todo paquete de evidencias exportado incluye un mecanismo propio de verificacion de integridad (hash o firma validable de forma independiente) |

---

## Resumen de decisiones que quedan como opinion de producto (no exigidas expresamente por la ley)

- El umbral de 50 empleados para activar la exigencia de separacion de funciones (ver `05_tipos_de_usuario.md`, seccion 5.4).
- El nombre y alcance exacto de los roles estandar; la ley solo exige de forma expresa la figura del Delegado mientras este vigente el regimen actual.
- Las metricas de exito del producto (cobertura, adopcion, retencion comercial).
- Los textos de descargo propuestos en `04_objetivo_exacto_del_producto.md`, seccion 1.3: la redaccion es una propuesta de producto, no un formato exigido por la ACE.
- El criterio conservador de "horas corridas" para el plazo de 72 horas del Art. 25, mientras no exista pronunciamiento oficial.
- Los items 24 y 25 de esta lista, anadidos en la consolidacion: el item 24 refleja el supuesto que requiere validacion de producto sobre la segmentacion de UX en tres niveles (`02_validacion_de_la_idea.md`, seccion 2.3.4); el item 25 refleja la decision de alcance 2.7.24 (integridad del paquete de evidencias) del mismo documento.
