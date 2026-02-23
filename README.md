# 📰 Automatización de Noticias Tech con n8n

Flujo automatizado creado en **n8n** que recopila noticias de tecnología desde múltiples fuentes RSS y las envía en un solo correo diario a Gmail.

---

## ¿Cómo funciona?

El flujo se ejecuta automáticamente cada día y sigue estos pasos:

1. **Schedule Trigger** — Dispara el flujo automáticamente a la hora configurada
2. **RSS Read** — Lee noticias de múltiples fuentes de tecnología
3. **Merge** — Une todas las noticias en un solo flujo
4. **Remove Duplicates** — Elimina noticias repetidas usando el campo `link`
5. **Aggregate** — Agrupa todas las noticias en un solo item
6. **Gmail** — Envía un correo con todas las noticias del día

---

## Fuentes de noticias

| Medio | URL del feed |
|---|---|
| Xataka | `https://www.xataka.com/index.xml` |
| Genbeta | `https://www.genbeta.com/index.xml` |

---

## Requisitos

- [n8n](https://n8n.io/) (self-hosted o cloud)
- Cuenta de Gmail conectada a n8n
- Docker (opcional, si usas n8n self-hosted)

---

## Instalación

### Con Docker

```bash
docker run -d --name n8n -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  n8nio/n8n
```

Luego abre `http://localhost:5678` en tu navegador.

### Importar el flujo

1. Descarga el archivo `envio de noticias por correo.json`
2. En n8n ve a **Workflows → Import**
3. Selecciona el archivo descargado
4. Configura tus credenciales de Gmail
5. Activa el flujo con **Publish**

---

## Configuración del correo

El correo se envía con el siguiente formato:

- **Subject:** `🗞️ Noticias Tech del día - DD/MM/YYYY`
- **Message:** Lista de noticias con título y link de cada una

---

## Estructura del flujo

```
⏰ Schedule Trigger
      ↓
📡 RSS Read (Xataka) ─┐
📡 RSS Read (Genbeta) ──► Merge
      ↓
🧹 Remove Duplicates
      ↓
📦 Aggregate
      ↓
📧 Gmail ✅
```

---

## Tecnologías usadas

- n8n
- RSS Feed
- Gmail API
- Docker

---

## Autor

Creado como proyecto de automatización personal con n8n.
