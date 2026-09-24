# MODULO: Portal del Titular

Codigo corto del modulo: MOD-012
Clasificacion global del modulo: SHOULD HAVE (queda fuera del MVP; se activa en V1/Enterprise)
Obligaciones que cubre: OBL-DOC-04 (Art. 61 inc. 2) y OBL-PLAZO-04 (Art. 61 inc. 2), como propietario. Colabora, sin ser propietario, con OBL-ARCO-15 (Art. 32, Lineamientos DPO), propiedad de MOD-011 ARCO-POL, y de forma indirecta con el resto de la matriz de obligaciones ARCO-POL (OBL-ARCO-01 a OBL-ARCO-15), porque el Portal es uno de los canales de entrada de esas solicitudes, nunca su dueno.

---

## A. Proposito

- **Por que existe.** La LPDP obliga a toda empresa privada a mantener mecanismos operativos, permanentes y accesibles para que un titular ejerza sus derechos ARCO-POL (Art. 61 inc. 2; OBL-DOC-04 y OBL-PLAZO-04; plazo transitorio de adecuacion ya vencido el 23 de mayo de 2025). Esa obligacion legal ya queda satisfecha desde el MVP con el formulario interno seguro de MOD-011 (decision 2.7.30 de `02_validacion_de_la_idea.md`). El Portal del Titular existe para dar a esa misma obligacion un canal adicional de autoservicio publico: un sitio al que el titular llega sin necesidad de que personal interno lo atienda, donde puede leer el Aviso y la Politica de Privacidad vigentes, presentar su solicitud ARCO-POL y, cuando la funcionalidad de consulta este activa, ver el estado de esa solicitud sin llamar ni escribir a la empresa.
- **Que problema resuelve para la empresa.** Reduce la carga de recibir solicitudes por canales informales (correo suelto, redes sociales, llamadas) dificiles de documentar y de medir contra el plazo legal; entrega a la empresa una prueba fechada de que mantiene un mecanismo accesible mas alla del minimo interno; y ofrece al titular una experiencia de autoservicio que reduce reclamos por falta de canal o de respuesta.
- **Que obligacion u obligaciones cubre.** OBL-DOC-04 (Art. 61 inc. 2, elaboracion y publicacion de mecanismos ARCO-POL propios) y OBL-PLAZO-04 (Art. 61 inc. 2, la misma obligacion vista como deber continuo de mantener esos mecanismos operativos). Colabora con OBL-ARCO-15 (Art. 32 Lineamientos DPO, aceptar los formularios oficiales de la ACE) al ofrecerlos como opcion de descarga dentro del Portal.
- **Que valor aporta.** Operativo: llega a MOD-011 una solicitud ya estructurada con los campos minimos del Art. 18 completos, en vez de un correo incompleto. Probatorio: cada visita al Aviso, cada solicitud presentada y cada verificacion de identidad queda con fecha y hora, alimentando el Centro de Evidencias (MOD-019). De reduccion de riesgo: aleja al titular de canales no controlados y dirige toda solicitud hacia el expediente unico que administra MOD-011, evitando duplicados.
- **Que NO hace este modulo (limites explicitos).** No resuelve ninguna solicitud ARCO-POL, no decide causales de procedencia ni redacta la respuesta final: eso es exclusivo de MOD-011. No sustituye al formulario interno seguro que ya cumple la obligacion legal desde el MVP; es una capa adicional posterior, no un reemplazo. No verifica identidad con criterio juridico definitivo por si solo, solo ejecuta el subproceso de verificacion de identidad definido por MOD-011 (decision 2.7.18). No almacena una segunda copia del expediente ni del documento de identidad adjuntado, solo referencias (ver seccion D). No es una mesa de ayuda general de la empresa ni un canal de atencion al cliente.

**Nota sobre el doble estado de la reforma 659.** Este modulo no tiene ninguna obligacion propia afectada por la reforma: el mapa de modulos lo marca explicitamente como "No aplica directamente". La obligacion de mantener mecanismos de ejercicio de derechos (OBL-DOC-04, OBL-PLAZO-04) no depende de quien resuelva la solicitud, sino de que exista el canal, y eso no cambia entre el estado ACTUAL y el estado FUTURO. El unico efecto indirecto, heredado de MOD-011 y de MOD-008, es de contenido: si el estado FUTURO se activa, el nombre y contacto de la persona responsable del tramite que el Portal muestra al titular (hoy derivado del rol Delegado, manana del "responsable interno") debe actualizarse junto con el Aviso de Privacidad, sin que el Portal necesite logica propia adicional para eso: solo refleja lo que MOD-008 publique como vigente.

---

## B. Usuarios

| Rol | Para que usa el Portal del Titular |
|---|---|
| Titular (formulario externo) | Consulta el Aviso y la Politica de Privacidad vigentes, presenta una solicitud ARCO-POL y, cuando la consulta de estado este activa, verifica su identidad para ver el estado de su expediente y descargar la resolucion final. Es el unico usuario que entra sin cuenta interna de la organizacion. |
| Administrador de la organizacion | Activa o desactiva el Portal, configura el dominio o subdominio publico, la marca visible (nombre, logo, colores basicos) y los metodos de verificacion habilitados. |
| Delegado de Proteccion de Datos (o Responsable interno, si aplica el estado FUTURO) | Supervisa que el Portal siga siendo un mecanismo operativo de ejercicio de derechos (OBL-DOC-04, OBL-PLAZO-04); revisa los casos de verificacion de identidad dudosa que el sistema escale. |
| Responsable ARCO-POL / Responsable del tramite | Recibe el aviso de cada nueva solicitud presentada por el Portal, la revisa dentro del expediente que MOD-011 crea automaticamente, y es la persona que el Portal muestra como contacto del tramite. |
| Responsable Legal / Compliance | Revisa los textos de descargo y los terminos de uso del Portal, y los casos donde la legitimacion del solicitante (representante o heredero) requiere criterio juridico antes de aceptar el acceso al expediente. |
| Responsable de Seguridad / IT | Monitorea los intentos de verificacion fallidos y las alertas de seguridad del Portal (posible enumeracion de expedientes, fuerza bruta sobre codigos de acceso), y valida la configuracion de exposicion publica del canal. |
| Responsable de area (RRHH, Marketing, Operaciones, etc.) | Uso indirecto: dentro de MOD-011 puede ver si una solicitud recibida por el Portal involucra datos que administra su area; no interactua directamente con el Portal. |
| Aprobador | Aprueba cambios de configuracion sensibles (activacion inicial del Portal, cambio del metodo de verificacion de identidad exigido), segun el flujo de aprobacion configurado para ese tipo de cambio. |
| Auditor (interno) | Consulta en modo de solo lectura el historial de accesos y solicitudes originadas en el Portal, como parte de la auditoria anual de cumplimiento (OBL-AUD-01). |
| Auditor externo (invitado) | Igual que el Auditor interno, con acceso temporal y acotado al periodo de una auditoria puntual. |
| Usuario de consulta / Colaborador | No interactua directamente con el Portal; puede ver, dentro de MOD-011, que una tarea asignada proviene de una solicitud recibida por este canal. |
| Asesor externo invitado | Accede de forma puntual si se le invita a dictaminar sobre un caso de legitimacion compleja (por ejemplo, la validez de un poder de representacion) que llego por el Portal. |

---

## C. Permisos

| Accion | Admin. org. | DPO / Resp. interno | Resp. ARCO-POL | Legal | Seg./IT | Resp. area | Aprobador | Auditor int. | Auditor ext. | Consulta | Titular | Asesor ext. |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Ver Aviso/Politica publicados | X | X | X | X | X | X | X | X | X | X | X | X |
| Ver configuracion del Portal | X | X (lectura) | X (lectura) | X (lectura) | X | - | X (lectura) | X (lectura) | X (lectura) | - | - | - |
| Crear/presentar solicitud ARCO-POL | - | - | - | - | - | - | - | - | - | - | X | - |
| Adjuntar documento de identidad | - | - | - | - | - | - | - | - | - | - | X | - |
| Modificar configuracion (marca, metodo de verificacion) | X | - | - | - | X (aspectos tecnicos) | - | - | - | - | - | - | - |
| Aprobar activacion o cambio sensible | - | X | - | X | - | - | X | - | - | - | - | - |
| Cerrar/archivar acceso de consulta vencido | X | - | - | - | X | - | - | - | - | - | - | - |
| Eliminar/purgar registros segun retencion | X | - | - | - | - | - | - | - | - | - | - | - |
| Exportar reporte de accesos o de solicitudes | X | X | X | X | X | - | - | X | X (temporal) | - | - | - |
| Asignar la solicitud (se ejecuta dentro de MOD-011) | - | - | X | - | - | - | - | - | - | - | - | - |

Separacion de funciones: quien configura o activa el Portal (Administrador) no deberia ser tambien quien aprueba esa activacion en empresa mediana o corporativa, a partir del umbral de tamano que usa el sistema para exigir separacion de funciones (05_tipos_de_usuario.md, seccion 5.4); en pyme el sistema permite que la misma persona lo haga, mostrando siempre la advertencia de autorrevision. Ningun rol interno puede editar ni eliminar lo que el titular presento: el formulario y el documento adjunto quedan de solo lectura para el personal en cuanto se envian, igual que dentro de MOD-011; solo el propio titular, mientras su solicitud siga en estado Borrador sin enviar, puede corregir sus datos. El Auditor (interno o externo) nunca aprueba ni modifica, solo consulta y exporta, para que su verificacion sea independiente.

---

## D. Informacion de entrada

El Portal recoge datos en tres momentos distintos, con reglas de minimizacion distintas para cada uno.

**Nota sobre minimizacion.** El principio general de minimizacion del sistema (guardar solo metadatos y referencias, nunca copias) no aplica de forma plena a este modulo: segun la decision 2.7.21 de `02_validacion_de_la_idea.md`, el Portal, igual que ARCO-POL, Incidentes y Consentimiento, procesa datos personales directos del titular como objeto legitimo de su propio proceso (identificarlo, verificarlo, contactarlo). Lo que si minimiza el diseno es la duplicacion: el documento de identidad y el expediente completo se guardan una sola vez, como parte de la Solicitud ARCO-POL que administra MOD-011; el Portal conserva unicamente la referencia a ese expediente y los metadatos propios de cada sesion de consulta (codigo, fecha, resultado de la verificacion), nunca una copia paralela del archivo.

### D.1 Consulta publica (sin autenticacion)

| Campo | Tipo | Obligatorio/opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Documento a consultar | Seleccion unica | Opcional (por defecto muestra la version vigente) | Aviso de Privacidad vigente, Politica de Privacidad vigente, Historial de versiones anteriores | Debe existir al menos una version publicada en MOD-008 para poder mostrarla | "Aqui puede leer que datos trata la empresa y como los protege. Tambien puede ver versiones anteriores si quiere comparar que cambio." | OBL-DOC-04, buena practica de transparencia (Art. 5 lit. e) |

### D.2 Presentacion de una solicitud ARCO-POL

| Campo | Tipo | Obligatorio/opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Tipo de derecho ejercido | Seleccion unica | Obligatorio | Acceso, Rectificacion, Cancelacion, Oposicion, Portabilidad, Olvido, Limitacion | Debe elegir exactamente una opcion | "Elija que quiere hacer con sus datos. Por ejemplo, si quiere saber que informacion tiene la empresa sobre usted, elija Acceso." | OBL-ARCO-02 (propiedad de MOD-011), Arts. 6 a 14 |
| Tipo de solicitante | Seleccion unica | Obligatorio | Titular, Representante con poder, Heredero o sucesor | Si elige Representante o Heredero, se vuelve obligatorio el campo "Acreditacion de representacion" | "Indique si usted es el dueno de los datos o si actua en nombre de otra persona." | OBL-ARCO-01, Art. 6 |
| Nombre completo del solicitante | Texto | Obligatorio | - | Minimo dos palabras | "Escriba su nombre tal como aparece en su documento de identidad." | OBL-ARCO-08, Art. 18 lit. a |
| Tipo de documento de identidad | Seleccion unica | Obligatorio | DUI, Pasaporte, Carnet de residente, Partida de nacimiento (si es heredero), Otro | - | "Elija el tipo de documento que va a adjuntar." | OBL-ARCO-08, Art. 18 lit. b |
| Numero de documento de identidad | Texto | Obligatorio | - | Formato segun el tipo de documento elegido | - | OBL-ARCO-08, Art. 18 lit. b |
| Copia del documento de identidad | Archivo | Obligatorio | PDF, JPG o PNG, tamano maximo configurable por la organizacion | Archivo legible, no vacio | "Adjunte una foto o escaneo legible de su documento. Este archivo se usa unicamente para verificar su identidad." | OBL-ARCO-08; subproceso Verificacion de identidad del titular (decision 2.7.18) |
| Acreditacion de representacion o de la calidad de heredero | Archivo | Condicional: obligatorio si el tipo de solicitante no es Titular | PDF, JPG o PNG | Archivo legible, no vacio | "Adjunte el poder, la resolucion o el documento que demuestre que puede actuar en nombre de esta persona." | OBL-ARCO-01, Art. 6 |
| Area o sistema que trata los datos, si lo conoce | Texto largo | Opcional | - | - | "Si sabe en que area o servicio de la empresa dejo sus datos (por ejemplo, Recursos Humanos o la tienda en linea), escribalo aqui; si no lo sabe, puede dejarlo en blanco." | OBL-ARCO-08, Art. 18 lit. c |
| Descripcion de los datos y de lo que pide | Texto largo | Obligatorio | - | Minimo de caracteres configurable | "Describa que informacion quiere y por que." | OBL-ARCO-08, Art. 18 lit. d y e |
| Correo electronico de contacto | Texto (correo) | Obligatorio | - | Formato de correo valido | "A este correo le enviaremos la confirmacion de recibido y el codigo para consultar el estado de su solicitud." | Soporte del plazo (OBL-ARCO-10) y del subproceso de verificacion |
| Telefono de contacto | Texto | Opcional | - | - | "Solo si prefiere que tambien lo contactemos por telefono." | Buena practica |
| Canal preferido de respuesta | Seleccion unica | Opcional | Correo electronico, Portal, Canal fisico o presencial | - | "Elija como prefiere recibir la respuesta." | OBL-ARCO-15 (disponibilidad de canales alternativos) |
| Aceptacion de los terminos de uso del Portal | Booleano | Obligatorio | - | Debe ser verdadero para poder enviar | Explica que sus datos se usan solo para tramitar esta solicitud. | Transparencia, Art. 5 lit. e |
| Firma o medio equivalente | Captura de firma o casilla de confirmacion | Obligatorio | - | - | "Confirme que la informacion que envio es suya y es correcta." | OBL-ARCO-08, Art. 18 lit. g |

### D.3 Consulta de estado de una solicitud ya presentada

| Campo | Tipo | Obligatorio/opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Numero de expediente o codigo de referencia | Texto | Obligatorio | - | Debe existir un expediente con ese numero en MOD-011 | "Es el numero que le dimos en su comprobante de recepcion." | Mecanismo propio de producto; evita busqueda libre de expedientes (mitiga anti-feature 20) |
| Correo electronico registrado en la solicitud | Texto (correo) | Obligatorio | - | Debe coincidir con el correo del expediente | "Escriba el mismo correo que usó cuando presento la solicitud." | Base del subproceso de verificacion, decision 2.7.18 |
| Codigo de verificacion recibido | Texto o numero | Obligatorio | - | Un solo uso, expira segun tiempo configurable (por defecto 15 minutos) | "Revise su correo, incluyendo la carpeta de spam, y escriba el codigo que le enviamos." | Mitiga el anti-feature 20 (no exponer el canal sin verificacion minima) |

### D.4 Cuenta persistente del titular (funcionalidad COULD HAVE, ver seccion Q)

| Campo | Tipo | Obligatorio/opcional | Opciones o catalogo | Validacion | Texto de ayuda | Fundamento |
|---|---|---|---|---|---|---|
| Correo y contrasena, o enlace de acceso sin contrasena | Texto/booleano | Opcional, solo si la organizacion activa esta funcionalidad | - | Reglas de complejidad de contrasena configurables | "Cree una cuenta si quiere ver todas sus solicitudes anteriores en un solo lugar." | Buena practica de producto, no exigencia legal |

Precarga: en la version base del modulo (D.2 y D.3) no hay precarga, cada solicitud se llena desde cero. Si la organizacion activa la cuenta persistente (D.4), los campos de identificacion del bloque D.2 pueden precargarse desde el perfil del titular en solicitudes posteriores, siempre dejando visible al titular la posibilidad de corregirlos antes de enviar.

---

## E. Informacion generada

| Salida | Contenido | Formato | Cuando se genera | Quien la recibe |
|---|---|---|---|---|
| Comprobante de recepcion | Numero de expediente, tipo de derecho, fecha y hora exactas, plazo legal aplicable, version del Aviso vigente en ese momento | PDF descargable y envio por correo | Al enviar exitosamente el formulario de la seccion D.2 | Titular; copia queda enlazada al expediente en MOD-011 |
| Solicitud ARCO-POL (registro en MOD-011) | Todos los campos de D.2, con origen = Portal | Registro estructurado | Automatico, al enviar el formulario | Responsable ARCO-POL / Responsable del tramite |
| Evento de auditoria "Solicitud recibida via Portal" | Fecha, hora, expediente, resultado de la validacion de campos | Registro de auditoria | Automatico, junto con el punto anterior | MOD-019 (Centro de Evidencias) |
| Codigo de verificacion de un solo uso | Codigo numerico o alfanumerico, tiempo de expiracion | Correo electronico | Al solicitar consultar el estado (D.3) | Titular |
| Vista de estado del expediente | Estado actual (espejo de solo lectura del estado real en MOD-011), fecha de ultima sincronizacion, dias restantes segun MOD-023 | Vista en pantalla | Al verificarse exitosamente una consulta de estado | Titular |
| Reporte de accesos y solicitudes del Portal | Ver seccion N | XLSX, CSV, PDF | Bajo demanda | Administrador de la organizacion, Responsable ARCO-POL, Auditor |
| Alerta de intentos de verificacion fallidos | Ver seccion I | Notificacion en plataforma y correo | Automatico, al superar el umbral configurado | Responsable de Seguridad / IT, Responsable ARCO-POL |

---

## F. Workflow

El Portal tiene dos flujos propios, distintos entre si y ambos distintos del flujo de resolucion del expediente, que pertenece integramente a MOD-011.

### F.1 Presentacion de una nueva solicitud

```
   [Visitante anonimo]
          |
          v
   Consulta Aviso / Politica (lee, no genera registro personal)
          |
          | elige "Presentar solicitud ARCO-POL"
          v
      BORRADOR ------------------------+
          |                            | abandona sin enviar
          | completa formulario D.2    v
          | y adjunta identificacion   (se descarta; solo queda un
          v                             conteo agregado, sin datos
       ENVIADA                          personales del visitante)
          |
          | crea automaticamente una Solicitud
          | en MOD-011 (estado Recibida)
          v
     SINCRONIZADA  <-------- refleja en solo lectura el estado real
          |                  del expediente en MOD-011:
          |                  Recibida -> En prevencion -> En analisis
          |                  -> Prorrogada -> Resuelta / Denegada
          |                  -> Notificada
          v
       CERRADA  (el expediente se resolvio en MOD-011; el Portal
          |       conserva el acceso de consulta de solo lectura)
          v
     ARCHIVADA  (vencido el plazo de retencion documental del
                  expediente, MOD-016; el acceso de consulta se
                  revoca, la evidencia permanece en MOD-019)
```

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (inicio) | Titular abre el formulario | Ninguna | BORRADOR | Titular | Ninguno, no hay registro con datos personales todavia |
| BORRADOR | Titular envia el formulario | Todos los campos obligatorios de D.2 validos; documento de identidad adjuntado | ENVIADA | Titular | Se crea la Solicitud ARCO-POL en MOD-011; se genera el comprobante de recepcion; evento de auditoria |
| BORRADOR | Titular abandona sin enviar | Ninguna | (descartado) | Titular (por inaccion) | Solo se conserva un conteo agregado de abandonos, sin datos personales |
| ENVIADA | MOD-011 confirma la creacion del expediente | Automatico | SINCRONIZADA | Sistema | Notificacion al Responsable ARCO-POL (ver seccion I) |
| SINCRONIZADA | MOD-011 cambia el estado del expediente | Automatico, en cada cambio de estado registrado por MOD-011 | SINCRONIZADA (refleja el nuevo estado) | Sistema | Notificacion al titular si el cambio es relevante (ver Automatizaciones) |
| SINCRONIZADA | MOD-011 cierra el expediente (Resuelta, Denegada o Archivada por incompetencia/falta de subsanacion) | El expediente en MOD-011 llega a un estado terminal | CERRADA | Sistema | El Portal muestra el resultado final y, si aplica, habilita la descarga de la resolucion (ver seccion Q) |
| CERRADA | Se cumple el plazo de retencion documental del expediente (5 anios, MOD-016) | Automatico | ARCHIVADA | Sistema | Se revoca el acceso de consulta desde el Portal; la evidencia permanece en MOD-019 |

### F.2 Verificacion de acceso para consultar el estado

```
   [Titular con numero de expediente]
             |
             v
     SOLICITUD_DE_ACCESO  (ingresa numero de expediente + correo)
             |
             v
     CODIGO_ENVIADO  (codigo de un solo uso al correo del expediente)
             |
        +----+----+
        |         |
        v         v
   VERIFICADO   NO_VERIFICADO (intentos agotados dentro del tiempo)
        |             |
        v             v
  SESION_ACTIVA   BLOQUEADO_TEMPORAL (ver alerta de seguridad)
        |
        v
  SESION_EXPIRADA  (cierre automatico por inactividad o por
                     alcanzar la duracion maxima configurada)
```

| Estado origen | Evento o accion | Condiciones y validaciones | Estado destino | Quien puede ejecutarla | Efectos |
|---|---|---|---|---|---|
| (inicio) | Titular ingresa numero de expediente y correo | Debe existir un expediente con ese numero y ese correo en MOD-011 | SOLICITUD_DE_ACCESO | Titular | Ninguno todavia |
| SOLICITUD_DE_ACCESO | Sistema genera el codigo | Coinciden numero de expediente y correo | CODIGO_ENVIADO | Sistema | Se envia el codigo por correo; evento de auditoria |
| CODIGO_ENVIADO | Titular ingresa el codigo correcto dentro del tiempo de validez | Codigo valido y no expirado | VERIFICADO | Titular | Se abre la sesion de consulta |
| CODIGO_ENVIADO | Titular agota los intentos permitidos o deja expirar el codigo | Umbral de intentos alcanzado | NO_VERIFICADO | Sistema | Alerta de seguridad si se repite (ver seccion I) |
| VERIFICADO | Sistema habilita la vista de estado | Automatico | SESION_ACTIVA | Sistema | El titular ve el estado, sin ver el contenido completo del expediente |
| NO_VERIFICADO | Umbral de bloqueo configurado se supera | Automatico | BLOQUEADO_TEMPORAL | Sistema | Notificacion a Responsable de Seguridad / IT |
| SESION_ACTIVA | Vence el tiempo maximo de sesion o el titular cierra sesion | Automatico o manual | SESION_EXPIRADA | Sistema o titular | Ninguno adicional; el titular puede volver a solicitar acceso |

Estados terminales, reapertura y registros vinculados: ARCHIVADA (F.1) y SESION_EXPIRADA (F.2) son los estados finales del Portal; ninguno de los dos es terminal para el expediente, cuya reapertura (por ejemplo, tras un reclamo ante la ACE, OBL-ARCO-14) se gestiona y se refleja siempre dentro de MOD-011, y el Portal simplemente vuelve a sincronizar el estado si el titular consulta de nuevo con un acceso valido.

---

## G. Automatizaciones

1. **Disparador:** titular envia el formulario de solicitud completo. **Condicion:** todos los campos obligatorios de D.2 son validos y el documento de identidad esta adjuntado. **Accion:** crear automaticamente una Solicitud ARCO-POL en MOD-011 en estado Recibida, con origen = Portal, y generar el comprobante de recepcion. Configurable por la empresa: no, es el nucleo legal del modulo.
2. **Disparador:** titular pide consultar el estado de un expediente. **Condicion:** numero de expediente y correo coinciden con el registro en MOD-011. **Accion:** generar y enviar un codigo de verificacion de un solo uso, valido por un tiempo configurable (por defecto 15 minutos). Configurable: si, el tiempo de expiracion.
3. **Disparador:** verificacion exitosa. **Condicion:** codigo correcto dentro del tiempo de validez. **Accion:** abrir una sesion de consulta de solo lectura sobre el estado actual del expediente en MOD-011, nunca sobre su contenido completo. Configurable: si, la duracion maxima de la sesion.
4. **Disparador:** cambio de estado del expediente en MOD-011. **Condicion:** el expediente tiene origen Portal. **Accion:** reflejar el nuevo estado en la vista de consulta y notificar al titular por correo que hay una actualizacion disponible. Configurable: si, que cambios de estado disparan notificacion.
5. **Disparador:** intentos de verificacion fallidos consecutivos superan el umbral. **Condicion:** umbral configurable (por defecto 5). **Accion:** bloquear temporalmente nuevos intentos desde ese origen y generar la alerta de seguridad de la seccion I. Configurable: si, umbral y duracion del bloqueo.
6. **Disparador:** el expediente cerrado en MOD-011 supera el plazo de retencion documental (5 anios, ver MOD-016). **Condicion:** el acceso de consulta del Portal sigue activo. **Accion:** revocar el acceso de consulta y dejar solo el registro de evidencia en MOD-019. Configurable: no, sigue la regla central de retencion.
7. **Disparador:** MOD-008 publica una nueva version del Aviso o de la Politica. **Condicion:** el documento esta marcado como publicado. **Accion:** actualizar de inmediato lo que el Portal muestra al publico, conservando el historial de versiones anteriores disponible. Configurable: no.

---

## H. Decisiones que NO debe automatizar

1. **Aceptar como valida la acreditacion de representacion o de la calidad de heredero.** El sistema solo verifica que el archivo fue adjuntado, nunca su validez juridica. Texto de advertencia: "Requiere validacion de la organizacion o asesoria especializada." Por que: una legitimacion indebida abre el acceso a datos de un tercero (Art. 6, OBL-ARCO-01), riesgo alto de exposicion.
2. **Decidir si una solicitud presentada por el Portal cumple los 7 requisitos del Art. 18 sin necesidad de prevencion.** El sistema valida formato de campo, no completitud sustantiva; esa revision sigue siendo del Responsable ARCO-POL dentro de MOD-011. Texto de advertencia: el mismo. Por que: una prevencion indebida u omitida es fuente de infraccion (Art. 56).
3. **Confirmar que el documento de identidad adjuntado corresponde efectivamente a quien presenta la solicitud.** El Portal no ejecuta verificacion biometrica ni de terceros (anti-feature 9 de `22_anti_features.md`); la confirmacion de identidad queda como tarea humana dentro de MOD-011. Texto de advertencia: el mismo. Por que: evita transmitir al titular o al personal una falsa sensacion de verificacion fuerte cuando solo hay verificacion documental basica.
4. **Decidir si el Portal debe mostrar el contenido completo de una resolucion, cuando esta menciona datos de terceros.** Requiere revision del Responsable Legal antes de publicar cualquier documento descargable en el Portal. Texto de advertencia: el mismo. Por que: la resolucion puede contener datos de otro titular (por ejemplo, un tercero mencionado en un tratamiento compartido).
5. **Determinar que el Portal, por si solo, ya es suficiente y por lo tanto se pueden ocultar otros canales.** El sistema nunca debe desactivar ni ocultar el canal fisico o presencial u otro canal alternativo solo porque el Portal esta activo. Texto de advertencia: el mismo. Por que: la practica de la ACE (OBL-ARCO-15) espera disponibilidad de canales, no un canal unico, y no todo titular puede o quiere usar un canal digital (ver persona Cecilia Marroquin, `05_tipos_de_usuario.md`).

---

## I. Alertas

| Alerta | Disparador | Nivel | Destinatario | Canal por defecto | Frecuencia | Escalamiento | Se apaga cuando |
|---|---|---|---|---|---|---|---|
| Nueva solicitud recibida via Portal | Envio exitoso del formulario D.2 | INFO | Responsable ARCO-POL / Responsable del tramite | Plataforma + correo | Inmediata, una vez por solicitud | Si no se triagea en 24 horas, escala al Delegado / Responsable interno | Cuando el Responsable ARCO-POL abre el expediente en MOD-011 |
| Codigo de verificacion generado | Titular solicita consultar estado | INFO | Titular | Correo | Una vez, expira segun configuracion | No aplica | Al usarse o al expirar |
| Intentos de verificacion fallidos superan el umbral | 5 intentos fallidos consecutivos (configurable) desde el mismo origen | WARNING | Responsable de Seguridad / IT, Responsable ARCO-POL | Plataforma + correo | Inmediata | Si se repite en menos de 24 horas desde el mismo origen, escala a HIGH y notifica al Delegado / Responsable interno | Cuando el Responsable de Seguridad revisa y cierra la alerta |
| Solicitud del Portal sin triage cerca del vencimiento de la prevencion | Expediente creado por el Portal sigue en Recibida a 2 dias habiles del vencimiento de los 10 dias habiles de prevencion (OBL-ARCO-08) | HIGH | Responsable ARCO-POL, Delegado / Responsable interno | Plataforma + correo | Diaria mientras persista | Escala al Aprobador si no hay accion | Cuando el expediente cambia de estado en MOD-011 |
| Cambio de version del Aviso o la Politica publicados en el Portal | MOD-008 publica una nueva version | INFO | Administrador de la organizacion, Responsable Legal | Plataforma | Una vez por publicacion | No aplica | Confirmacion de revision del Responsable Legal |
| Acceso de consulta proximo a revocarse por vencimiento de retencion | Expediente cerrado hace (retencion menos 30 dias) | INFO | Responsable ARCO-POL | Plataforma | Una vez | No aplica | Al revocarse el acceso |

---

## J. Evidencia

| Evidencia | Que prueba (OBL-ID) | Como se conserva |
|---|---|---|
| Comprobante de recepcion con fecha, hora, version del Aviso vigente y version del formulario usado | OBL-DOC-04, OBL-PLAZO-04 (el mecanismo estaba operativo en esa fecha) | Igual que el expediente ARCO-POL asociado: 5 anios (MOD-016, decision 2.7.13) |
| Registro con fecha, hora y resultado de cada intento de verificacion de identidad para consultar estado | OBL-DOC-04, OBL-PLAZO-04 (el mecanismo exige verificacion antes de exponer datos, mitigando el anti-feature 20) | Alineado al periodo de retencion del expediente relacionado; el codigo mismo no se conserva en texto claro una vez usado o expirado |
| Historial inmutable (append-only, anti-feature 19) de cambios de configuracion del Portal | OBL-DOC-04, OBL-PLAZO-04 (el mecanismo se mantiene bajo control formal de la organizacion) | Sin plazo de vencimiento, historia tecnica del programa |
| Hash del documento de identidad recibido, enlazado al expediente de MOD-011 | Integridad del anexo que sustenta OBL-ARCO-08 (propiedad de MOD-011) | Igual que el expediente relacionado; sin duplicar el archivo en el Portal |
| Bitacora de que version del Aviso y la Politica estuvo publicada en el Portal en cada fecha (version, fecha de publicacion, fecha de retiro) | OBL-DOC-04, OBL-PLAZO-04 como obligacion continua, no solo puntual | Historico completo, sin vencimiento |
| Exportacion firmada o con hash del reporte de accesos del Portal | OBL-PRIN-03 (responsabilidad demostrada), disponible para el paquete de MOD-019 (decision 2.7.24) | Se conserva la exportacion misma como evidencia adicional, con su propio hash |

---

## K. Documentos asociados

- **Documentos requeridos como entrada:** Aviso de Privacidad vigente y Politica de Privacidad vigente, ambos gestionados y versionados en MOD-008; el Portal solo los muestra, nunca los edita. Los siete formularios oficiales ARCO-POL de la ACE (version 07-07-2025), disponibles para descarga y tambien aceptados si el titular sube uno de ellos ya lleno (OBL-ARCO-15).
- **Documentos generados:** Comprobante de recepcion de la solicitud (PDF descargable y enviado por correo); Terminos de uso del Portal (documento fijo, versionado, aprobado como cualquier otro documento en MOD-008).
- **Plantillas que el sistema provee:** plantilla de Comprobante de recepcion (variables: numero de expediente, tipo de derecho, fecha, plazo aplicable, articulo); plantilla de correo de verificacion (variables: codigo, tiempo de expiracion). Ninguna requiere validacion de la organizacion para su uso operativo diario, pero su contenido base si se revisa una vez, al activar el modulo.
- **Anexos y evidencias documentales:** copia del documento de identidad y, si aplica, de la acreditacion de representacion o de heredero, ambos anexados al expediente que administra MOD-011; el Portal no conserva copia propia (ver seccion D).

---

## L. Dependencias

```
MOD-008 (Documentos y Politicas)
   | Aviso y Politica vigentes (solo lectura)
   v
MOD-012 (Portal del Titular)
   |-----------------> MOD-011 (ARCO-POL): crea la Solicitud; el Portal
   |                    nunca resuelve ni modifica el expediente
   |-----------------> MOD-019 (Centro de Evidencias): comprobantes,
   |                    bitacora de accesos, hash de verificacion
   v-----------------> MOD-023 (Calendario y Motor de Plazos): lectura
                        del plazo aplicable, para mostrarlo al titular
                        junto al estado; el Portal nunca calcula el
                        plazo por su cuenta
```

- **Entra desde:** MOD-008 (contenido del Aviso y la Politica que se muestran publicamente).
- **Sale hacia:** MOD-011 (crea una nueva Solicitud ARCO-POL por cada formulario enviado; el Portal es lector, no editor, de todo lo que sigue), MOD-019 (evidencia de recepcion, accesos y verificaciones), MOD-023 (lectura del plazo vigente para mostrar al titular cuantos dias habiles restan).
- **Que ocurre si el modulo dependiente no existe en el MVP:** si MOD-008 aun no tiene un Aviso publicado, el Portal no puede activarse; en vez de un Portal vacio, muestra el mensaje "Aviso de privacidad pendiente de publicar". Si MOD-011 no estuviera activo, el Portal no tendria a donde enviar la solicitud, por lo que MOD-012 requiere a MOD-011 como dependencia estructural (coherente con que MOD-011 es MUST HAVE y MOD-012 es SHOULD HAVE posterior). Si MOD-019 no estuviera disponible, el Portal seguiria funcionando pero sin que la evidencia quedara centralizada, lo que se marca como riesgo (ver seccion P). Si MOD-023 no estuviera disponible, el Portal deja de mostrar el conteo de dias restantes y muestra solo el estado, sin calcular el plazo por su cuenta.

---

## M. Dashboard

| Indicador | Formula | Semaforo | Vista por rol |
|---|---|---|---|
| Solicitudes recibidas por canal | Conteo de Solicitudes con origen = Portal, sobre el total de Solicitudes del periodo | No aplica (informativo) | Gerencia (adopcion del canal), Responsable ARCO-POL (volumen a atender) |
| Tiempo promedio hasta el primer triage | Promedio de horas entre envio en el Portal y apertura del expediente por el Responsable ARCO-POL | Verde: menos de 1 dia habil. Amarillo: 1 a 2. Rojo: mas de 2 (umbral de producto) | Responsable ARCO-POL, Legal |
| Tasa de intentos de verificacion fallidos | Intentos fallidos / total de intentos de verificacion del periodo | Verde: menos de 5%. Amarillo: 5 a 15%. Rojo: mas de 15% (umbral de producto) | Seguridad / IT, Auditor |
| Disponibilidad del contenido publicado | Si el Aviso y la Politica mostrados corresponden a la version vigente en MOD-008 | Verde: al dia. Rojo: hay una version vencida mostrandose | Legal, Auditor |
| Cobertura de evidencia | Porcentaje de solicitudes originadas en el Portal con comprobante y verificacion documentados en MOD-019 | No aplica (se muestra como evidencia disponible, nunca como cumplimiento legal) | Auditor |

Ninguno de estos indicadores se expresa como "porcentaje de cumplimiento legal"; siempre como estado del programa, controles configurados o evidencia disponible, segun corresponda.

---

## N. Reportes

| Reporte | Contenido | Filtros | Formato | Destinatario tipico | Parte del paquete de evidencia |
|---|---|---|---|---|---|
| Solicitudes recibidas por el Portal | Fecha, tipo de derecho, tipo de solicitante, estado actual, tiempo hasta triage | Rango de fechas, tipo de derecho, estado | XLSX, CSV | Responsable ARCO-POL, Gerencia | Si, para auditoria interna (MOD-019) |
| Accesos y verificaciones del Portal | Fecha y hora, resultado de la verificacion, expediente relacionado (sin exponer el documento de identidad) | Rango de fechas, resultado | CSV, PDF firmado | Responsable de Seguridad / IT, Auditor | Si, para auditoria y para una eventual revision de la ACE |
| Constancia de mecanismo operativo | Desde cuando el Portal esta activo, versiones del Aviso mostradas, disponibilidad en el periodo | Rango de fechas | PDF | Delegado / Responsable interno, Gerencia | Si, evidencia directa de OBL-DOC-04 y OBL-PLAZO-04 |

---

## O. Historial

Eventos que quedan en el historial del modulo y en la auditoria transversal (MOD-019 / AuditLog), con la obligacion que cada uno ayuda a probar:

- Activacion o desactivacion del Portal, con fecha (OBL-DOC-04, OBL-PLAZO-04: prueba el periodo exacto en que el mecanismo estuvo operativo).
- Publicacion de una nueva version del Aviso o la Politica en el Portal, y retiro de la version anterior (OBL-DOC-04).
- Envio de cada formulario de solicitud, exitoso o abandonado en Borrador (el abandono solo queda como conteo agregado, sin datos personales).
- Creacion del expediente correspondiente en MOD-011 y su identificador, con enlace bidireccional (OBL-PLAZO-04, trazabilidad del canal de origen).
- Cada solicitud de codigo de verificacion, con resultado: exitoso, fallido o expirado sin uso (OBL-DOC-04, prueba de que el acceso exige verificacion).
- Apertura y cierre de cada sesion de consulta de estado.
- Cambios de configuracion sensible (metodo de verificacion, umbral de bloqueo, marca visible), con valor anterior, valor nuevo y usuario responsable.
- Revocacion de un acceso de consulta por cierre del expediente o vencimiento de la retencion.
- Exportacion de cualquiera de los reportes de la seccion N, con usuario y fecha.
- Accesos de lectura al documento de identidad, aunque el archivo viva en MOD-011: el acceso se origina desde una referencia creada por el Portal y debe quedar trazado igual.

---

## P. Riesgos

- **Riesgo legal:** que el Portal, por estar disponible en linea, de al titular la impresion de que su solicitud se resuelve de forma automatica o instantanea. **Mitigacion de diseno:** mostrar siempre, junto al comprobante de recepcion, el texto de descargo de plazos (`04_objetivo_exacto_del_producto.md`, seccion 1.3) y el plazo legal aplicable (20 mas 20 dias habiles), nunca un mensaje de "solicitud completada".
- **Riesgo legal:** aceptar como suficiente una acreditacion de representacion o herencia sin revision humana, exponiendo datos de un tercero a quien no tiene derecho. **Mitigacion:** bloqueo explicito de automatizacion en ese punto (seccion H, punto 1), mas aviso visible al titular de que la revision de esa calidad toma tiempo adicional.
- **Riesgo de UX:** abandono del formulario por la exigencia de adjuntar documentos de identidad desde un celular, especialmente para un titular con desconfianza hacia canales digitales (persona Cecilia Marroquin, `05_tipos_de_usuario.md`). **Mitigacion:** mantener siempre visible, junto al formulario en linea, la opcion del canal fisico o presencial y un contacto directo, sin forzar el uso exclusivo del Portal.
- **Riesgo de UX:** que el codigo de verificacion no llegue por filtros de spam o un correo mal escrito, dejando al titular sin poder consultar su estado. **Mitigacion:** ofrecer un metodo de verificacion alternativo (por ejemplo, los ultimos digitos del documento de identidad) y mostrar instrucciones claras sobre que hacer si el codigo no llega.
- **Riesgo operativo:** que el estado mostrado en el Portal quede desincronizado del estado real del expediente en MOD-011 por una falla tecnica, generando confusion o reclamos. **Mitigacion:** mostrar siempre la fecha y hora de la ultima sincronizacion junto al estado, y bloquear la vista con un aviso claro si la sincronizacion supera un umbral de tiempo configurable, en vez de mostrar un estado potencialmente desactualizado sin advertencia.
- **Riesgo de seguridad y privacidad:** exposicion de datos de un titular a otra persona por enumeracion de numeros de expediente o por fuerza bruta sobre el codigo de verificacion. **Mitigacion:** numeros de expediente no correlativos ni adivinables, limite de intentos con bloqueo temporal (seccion I), codigo de un solo uso con expiracion corta, y ninguna informacion del expediente visible antes de completar la verificacion.
- **Riesgo de seguridad y privacidad:** que el Portal, al ser publico, se convierta en superficie de phishing (sitios falsos que imitan el Portal para robar documentos de identidad). **Mitigacion:** identidad visual clara y verificable de la organizacion, y advertencia visible en el Portal y en los correos de verificacion de que la empresa nunca pedira el documento de identidad completo por un medio distinto del Portal oficial.
- **Riesgo de producto:** que activar el Portal sin haber probado antes el formulario interno de MOD-011 genere un volumen de solicitudes que la empresa no sabe atender a tiempo. **Mitigacion:** el Portal solo puede activarse si MOD-011 ya esta configurado con un Responsable ARCO-POL asignado (dependencia estructural, seccion L), y la alerta HIGH de la seccion I cubre el riesgo de un expediente sin triage.

---

## Q. MVP

| Funcionalidad del modulo | MUST HAVE | SHOULD HAVE | COULD HAVE | FUTURE | Justificacion |
|---|---|---|---|---|---|
| Consulta publica del Aviso de Privacidad vigente | | X | | | Obligacion legal (OBL-DOC-04) ya cubierta desde el MVP por MOD-011; el Portal es el canal adicional, coherente con la clasificacion SHOULD HAVE del modulo completo |
| Consulta publica de la Politica de Privacidad vigente | | X | | | Misma razon; complementa el Aviso sin obligacion propia adicional |
| Formulario de presentacion de solicitud ARCO-POL sin cuenta persistente | | X | | | Nucleo funcional del modulo: sin el, el Portal no aporta valor nuevo sobre el canal interno |
| Verificacion basica de identidad al presentar (documento adjunto) | | X | | | Necesaria para que la solicitud llegue a MOD-011 sin reproceso manual de verificacion |
| Consulta de estado por numero de expediente y codigo de verificacion | | X | | | Funcion que justifica el modulo frente al canal interno: autoservicio de estado sin cuenta persistente |
| Notificacion por correo de cambios de estado relevantes | | X | | | Se apoya en las dependencias de solo lectura ya previstas con MOD-011 y MOD-023; valor alto con complejidad moderada |
| Descarga de la resolucion final desde el Portal | | | X | | Anade autoservicio, pero exige revision previa del Responsable Legal por posibles datos de terceros (seccion H); se difiere |
| Cuenta persistente del titular (historial de solicitudes propias) | | | X | | Simplifica solicitudes repetidas, pero suma superficie de ataque y gestion de credenciales |
| Marca visible personalizada por organizacion (logo, colores) | | | X | | Valor comercial y de confianza, sin relacion con ninguna obligacion legal |
| Portal en mas de un idioma | | | X | | Util para empresas con titulares o clientes extranjeros, sin urgencia regulatoria |
| Mensajeria o chat con el Responsable ARCO-POL dentro del Portal | | | | X | Anade complejidad de moderacion y de conservacion de evidencia de conversaciones, sin obligacion legal que lo exija |
| Verificacion de identidad biometrica o KYC electronico de terceros | | | | X | Anti-feature 9: el sistema no almacena datos biometricos de titulares; cualquier integracion seria con un proveedor externo, fuera del alcance actual |
| Aplicacion movil nativa del Portal | | | | X | El Portal web responsivo cubre el caso de uso principal; una app nativa es decision comercial futura, sin valor legal adicional |
| Kiosco fisico de autoservicio en sucursal | | | | X | Fuera del alcance de un producto SaaS de autogestion; implicaria integracion de hardware propia de cada cliente |

**Version minima vendible del modulo.** Es la combinacion de consulta publica del Aviso y la Politica, el formulario de presentacion de solicitud sin cuenta persistente, la verificacion basica por documento adjunto y la consulta de estado por codigo de un solo uso. Esa combinacion ya reemplaza operativamente la necesidad de que el titular llame o escriba para presentar o dar seguimiento a su solicitud, sin exigir todavia cuentas persistentes, marca personalizada ni canales enriquecidos, que quedan para versiones posteriores. Ninguna pieza de este modulo es indispensable para el MVP del producto, porque la obligacion legal que le da origen (OBL-DOC-04, OBL-PLAZO-04) ya esta cubierta desde el primer dia por el formulario interno seguro de MOD-011 (decision 2.7.30 de `02_validacion_de_la_idea.md`).

---

## R. Ayuda contextual

Los conceptos 1 y 2 se muestran al titular dentro del propio Portal; los conceptos 3 a 5 se muestran al personal interno en el panel de configuracion, a traves de MOD-026.

**1. Que es el Portal del Titular**
- Que es: un sitio donde usted puede leer como esta empresa trata sus datos, pedir que le muestren, corrijan o eliminen su informacion, y revisar en que va su solicitud.
- Por que tengo que hacer esto: si quiere ejercer sus derechos sobre sus datos personales, este es uno de los canales disponibles para hacerlo, ademas del canal fisico o presencial de la empresa.
- Fundamento: OBL-DOC-04 y OBL-PLAZO-04, Art. 61 inc. 2 de la LPDP.
- Cuando necesito ayuda juridica: si su caso involucra a otra persona (por ejemplo, usted actua como representante o heredero) y no esta seguro de que documentos presentar, consulte con un abogado antes de continuar.

**2. Que es el codigo de verificacion**
- Que es: un numero que le enviamos a su correo, valido por un tiempo corto, para confirmar que es usted quien consulta el estado de su solicitud.
- Por que tengo que hacer esto: protege su informacion para que nadie mas pueda ver el estado de su caso solo con el numero de expediente.
- Fundamento: buena practica de seguridad que respalda el mecanismo exigido por OBL-DOC-04 y OBL-PLAZO-04.
- Cuando necesito ayuda juridica: no aplica; si tiene problemas tecnicos para recibir el codigo, contacte directamente a la empresa por el canal alternativo indicado en el Portal.

**3. Por que se pide un documento de identidad al presentar la solicitud**
- Que es: un requisito para comprobar que quien pide acceso, correccion o eliminacion de datos es la persona duena de esos datos, o alguien autorizado.
- Por que tengo que hacer esto: sin verificar la identidad del solicitante, la empresa arriesga entregar informacion de una persona a alguien mas.
- Fundamento: OBL-ARCO-08 (Art. 18) y el subproceso de verificacion de identidad de MOD-011 (decision 2.7.18 de `02_validacion_de_la_idea.md`).
- Cuando necesito ayuda juridica: si el documento adjuntado genera dudas sobre su validez o vigencia, consulte con el Responsable Legal antes de continuar con el tramite.

**4. Diferencia entre el Portal y el formulario interno de la empresa**
- Que es: el formulario interno (MOD-011) ya es, por si solo, un mecanismo legal suficiente para recibir solicitudes ARCO-POL; el Portal es un canal adicional de autoservicio que ademas permite consultar el estado sin ayuda de personal.
- Por que tengo que hacer esto: activar el Portal es una decision de producto de la empresa, no una obligacion legal adicional a lo que ya cumple el formulario interno.
- Fundamento: decision 2.7.30 de `02_validacion_de_la_idea.md`.
- Cuando necesito ayuda juridica: no aplica; es una decision operativa de la organizacion, no una decision juridica.

**5. Que significa que mi solicitud este "en revision" en el Portal**
- Que es: el Portal muestra el mismo estado que tiene su expediente dentro del sistema interno de la empresa (MOD-011); "en revision" quiere decir que el responsable del tramite ya la recibio y la esta analizando.
- Por que tengo que hacer esto: el Portal no decide ni acelera la resolucion, solo refleja en que paso esta su caso.
- Fundamento: OBL-ARCO-10 (Art. 20), plazo de 20 mas 20 dias habiles.
- Cuando necesito ayuda juridica: si el plazo legal esta por vencer sin respuesta, o si no esta de acuerdo con la resolucion final, puede presentar un reclamo ante la Direccion de Proteccion de Datos de la ACE (OBL-ARCO-14); en ese caso, consulte a un abogado si lo necesita.

---

## Notas finales (desacuerdos y observaciones sobre el mapa)

1. **Arista faltante hacia MOD-022 (Notificaciones).** El mapa de dependencias en `mapa_modulos.json` no declara ninguna salida de MOD-012 hacia MOD-022, y la ficha de MOD-022 en `06_mapa_definitivo_de_modulos.md` tampoco lista a MOD-012 entre sus entradas. Sin embargo, el Portal necesita funcionalmente enviar al menos dos tipos de correo propios del canal (el codigo de verificacion de un solo uso y el aviso de actualizacion de estado al titular), que en este documento se modelan en las secciones G e I. Se sugiere que la version definitiva del mapa aclare si ese envio se considera un evento generado por MOD-011 (ya que el expediente le pertenece) y por eso no requiere una arista propia desde MOD-012, o si conviene anadir explicitamente esa arista para que MOD-022 sea consistente con todos los modulos que efectivamente disparan notificaciones al titular.
2. **Clasificacion SHOULD HAVE del modulo completo frente a la obligacion legal que cita.** OBL-DOC-04 y OBL-PLAZO-04 estan clasificadas como OBLIGATORIO en `matriz_obligaciones.json`, lo que podria leerse en tension con que su modulo propietario (MOD-012) sea SHOULD HAVE. La ficha de MOD-012 en `06_mapa_definitivo_de_modulos.md` ya resuelve esta tension de forma explicita: ambas obligaciones quedan cubiertas desde el MVP por el canal de MOD-011, y este documento sigue esa misma logica sin contradecirla; se deja constancia aqui unicamente para que quede claro que la clasificacion SHOULD HAVE del modulo no significa que la obligacion en si sea opcional.
