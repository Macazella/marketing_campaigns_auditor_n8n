### 📌 Proyecto: Automatización de Solicitudes de Marketing – Grupo Olmos

Este repositorio contiene un flujo automatizado desarrollado en **n8n**, utilizado por el equipo de **Marketing de Grupo Olmos** para gestionar solicitudes internas recibidas mediante un formulario. El flujo valida los datos, crea tarjetas en Trello, guarda registros para auditoría y responde automáticamente a quienes completan el formulario.

---

### 🔄 Funcionalidad del flujo

El flujo automatizado realiza los siguientes pasos:

1. **Recepción del formulario**

   * Se activa mediante un **Webhook** (`POST`) conectado a un formulario en línea.

2. **Validación del correo electrónico**

   * El nodo `Validar Email` comprueba que el campo `email` tenga un formato válido.

3. **Email inválido**

   * Si el correo no es válido:

     * Se envía una **alerta automática al solicitante** indicando el error.
     * Se devuelve una **respuesta HTTP de error (400)**.

4. **Email válido**

   * Si el correo es válido:

     * Se **crea una tarjeta en Trello** en el tablero de Marketing, con los detalles de la solicitud.
     * Se **guarda el registro en Google Sheets** (auditoría).
     * Se envía una **confirmación por correo electrónico** al solicitante.
     * Se devuelve una **respuesta HTTP de éxito (200)**.

---

### ⚙️ Requisitos

* n8n instalado y corriendo localmente o en servidor.
* Accesos autorizados a:

  * **Trello API**
  * **Google Sheets API**
  * **SMTP o Gmail API**
* Un formulario conectado al webhook (por ejemplo, Google Forms o Typeform con integración).

---

### 📁 Estructura del repositorio

```
📦 n8n_marketing_workflow/
 ┣ 📄 README.md
 ┣ 📄 LICENSE
 ┣ 📄 .env.example
 ┣ 📄 workflow_marketing_integrado.json
 ┗ 📁 docs/
     ┗ 📄 estructura_flujo.png
```

---

### 🔐 Variables de entorno (`.env.example`)

```env
# Trello
TRELLO_KEY=
TRELLO_TOKEN=
TRELLO_LIST_ID=

# Google Sheets
GOOGLE_SHEETS_SPREADSHEET_ID=
GOOGLE_SHEETS_ACCESS_TOKEN=

# Email SMTP / Gmail API
EMAIL_SERVICE=
EMAIL_USER=
EMAIL_PASS=
```

---

### 📝 Notas

* Se recomienda integrar el webhook con un **formulario de Google** mediante App Script o Zapier si no se usa Typeform.
* El Google Sheet debe tener encabezados definidos con los mismos nombres que los campos del formulario.

---

## 📄 Licencia

MIT © Magalí Cazella
