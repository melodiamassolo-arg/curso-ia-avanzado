# Pre Entrega - Módulo 4
## Automatización inteligente de respuesta a correos con n8n

### Objetivo

Este workflow automatiza el procesamiento de correos electrónicos entrantes utilizando n8n e integra múltiples servicios externos para asistir en la preparación de una respuesta.

El flujo no envía correos automáticamente: genera un borrador para revisión humana (Human in the Loop).

---

## Arquitectura

1. Gmail Trigger recibe un nuevo correo.
2. Se valida que el remitente no corresponda a respuestas automáticas.
3. Se busca el contacto en HubSpot.
4. Si el contacto no existe, se crea automáticamente.
5. Se consulta la agenda de Google Calendar para los próximos 7 días.
6. Se consolida la información relevante de la agenda.
7. Un AI Agent analiza el correo y la disponibilidad.
8. Se genera un borrador en Gmail para revisión humana antes del envío.

---

## Integraciones utilizadas

- Gmail
- HubSpot
- Google Calendar
- Groq (LLM)

Todas las integraciones utilizan autenticación OAuth2 o API Key según corresponda.

---

## Controles implementados

### Prevención de bucles

Se filtran correos automáticos mediante validaciones sobre:

- noreply
- no-reply
- mailer-daemon
- auto-reply
- out of office
- undeliverable

---

### Prevención de errores

Antes de crear un contacto se realiza una búsqueda en HubSpot para evitar duplicados.

---

### Human in the Loop

El resultado del análisis de IA no se envía automáticamente.

El workflow crea un borrador en Gmail que debe ser revisado y aprobado manualmente por el usuario.

---

## Archivos incluidos

- checkpoint4_melodia_massolo.json
- Capturas del funcionamiento del workflow
