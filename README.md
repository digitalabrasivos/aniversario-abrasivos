# Landing · Aniversario 59 años — Abrasivos Industriales

Landing page de una sola página para la campaña de Google Ads / YouTube del Aniversario 59 años
(promoción del 19 de octubre al 7 de noviembre de 2026).

## Estructura

- `index.html` — toda la página (HTML, CSS y JS en un solo archivo, sin frameworks).
- `assets/productos/` — fotos de los 24 productos del catálogo (WebP).
- `server.js` — servidor estático mínimo en Node (sin dependencias) para Railway.

## Publicar en Railway

1. En Railway: **New Project → Deploy from GitHub repo** y elige este repositorio.
2. Railway detecta Node y ejecuta `npm start` automáticamente.
3. En **Settings → Networking** pulsa **Generate Domain** (o conecta un dominio propio).

Health check opcional: `/health`.

## Configuración rápida

Al inicio del `<script>` en `index.html` está el objeto `CONFIG`:

| Campo | Para qué sirve |
| --- | --- |
| `whatsapp` | Número de WhatsApp (formato internacional sin `+`). |
| `fin` | Fecha y hora en que termina la promoción. Después se muestra “Promoción finalizada”. |
| `youtubeId` | ID del video de YouTube de la campaña. Vacío = la sección de video no se muestra. |
| `googleAdsId` / `googleAdsLabel` | ID de conversión (`AW-XXXXXXXXX`) y etiqueta de la acción de conversión. Cada clic a WhatsApp se registra como conversión. |
| `mensajes` | Mensajes prellenados de WhatsApp. |

Los productos y precios están en el arreglo `PRODUCTOS`, justo debajo de `CONFIG`.

Cada clic a WhatsApp también envía el evento `whatsapp_click` al `dataLayer` (útil si se usa Google Tag Manager).

Para ver cómo se verá la página cuando termine la promoción: agrega `?vista=finalizada` a la URL.
