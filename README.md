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

## Cambiar la foto de un producto

1. Prepara la foto: **cuadrada** (ideal 800 × 800 px o más), **fondo blanco** y el producto centrado ocupando casi todo el recuadro. Formatos: `.webp`, `.jpg` o `.png`.
2. Opción rápida (mismo nombre): en GitHub entra a `assets/productos/`, pulsa **Add file → Upload files** y sube la foto con **exactamente el mismo nombre** del archivo actual (ej. `guante-anticorte-m37.webp`). Si la foto nueva es `.jpg` o `.png`, súbela con su nombre y cambia el campo `img` de ese producto en `index.html` (ej. `img:'guante-anticorte-m37.jpg'`).
3. Si el producto se ve pequeño dentro de la tarjeta, agrega `zoom` al producto en `index.html`, por ejemplo `img:'gafa-monogafa-om.webp', zoom:1.2`.
4. En `index.html` sube en 1 el valor de `FOTOS_VERSION` para que los navegadores no muestren la foto anterior en caché.
5. Al hacer *Commit changes*, Railway publica el cambio automáticamente en 1–2 minutos.

## Pendientes

### 1. Medición de conversiones en Google Ads (cuenta 409-926-5471)

El número `409-926-5471` es el ID de la **cuenta** de Google Ads; para medir conversiones se necesita
el **ID de conversión** y la **etiqueta**:

1. Google Ads → **Objetivos → Conversiones → Resumen → + Nueva acción de conversión → Sitio web**.
2. Ingresar la URL de la landing y elegir **Agregar una acción de conversión manualmente**.
   - Objetivo: *Contacto* (o *Cliente potencial*). Nombre sugerido: `Clic WhatsApp – Landing Aniversario`.
   - Valor: sin valor o un valor fijo estimado por lead. Recuento: **Uno** (un lead por clic/sesión).
3. Guardar → **Configuración de la etiqueta → Usar Google Tag Manager**. Allí aparecen:
   - **ID de conversión** → va en `CONFIG.googleAdsId` con el prefijo `AW-` (ej. `AW-123456789`).
   - **Etiqueta de conversión** → va en `CONFIG.googleAdsLabel`.
4. Desplegar y verificar con *Google Tag Assistant* que el clic a WhatsApp dispare la conversión.
5. En la campaña de video, usar esa acción como objetivo de conversión principal.

### 2. Video de la campaña

Poner el ID de YouTube en `CONFIG.youtubeId` para que aparezca la sección de video.

## Logos

En `assets/`: `logo-abrasivos-azul.png` (principal, sobre fondos claros) y `logo-abrasivos-blanco.png`
(sobre fondos oscuros: encabezado y pie de página).
