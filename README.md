# Landing · Dotación, EPP y abrasivos para empresas — Abrasivos Industriales

Landing de una sola página para campañas de Google Ads (Demand Gen) dirigidas a empresas de
Medellín y Antioquia. Cada botón lleva a WhatsApp con un mensaje prellenado y registra una conversión.

> La landing del Aniversario 59 años quedó en el historial de Git (commit `0041ea7`).

## Estructura

- `index.html` — toda la página (HTML, CSS y JS en un solo archivo, sin frameworks).
- `assets/kits/` — fotos de los productos de los kits y del encabezado (WebP, cuadradas, fondo blanco).
- `assets/` — logos (`logo-abrasivos-blanco.png`, `logo-abrasivos-azul.png`), favicon e imagen para compartir.
- `server.js` — servidor estático mínimo en Node (sin dependencias) para Railway. `railway.json` define el chequeo de salud.

## Publicar en Railway

El servicio está conectado a este repositorio con despliegue automático: cada commit a `main` se publica solo.

### Cambiar el dominio
Railway → servicio → **Settings → Networking → Custom Domain**. Agrega el dominio o subdominio
(por ejemplo `empresas.abrasivosindustriales.com.co`) y crea en el DNS el registro que Railway indique (CNAME).

## Configuración rápida

Al inicio del `<script>` en `index.html` está el objeto `CONFIG`:

| Campo | Para qué sirve |
| --- | --- |
| `whatsapp` | Número de WhatsApp (formato internacional sin `+`). |
| `videos` | Lista de videos de YouTube. Ej.: `[{id:'ID_DEL_VIDEO'}, {id:'ID_SHORT', vertical:true}]`. Vacía = la sección no se muestra. Máximo 3. |
| `googleAdsId` / `googleAdsLabel` | Conversión de Google Ads. Cada clic a WhatsApp se registra. |
| `ga4Id` | ID de medición de Google Analytics 4 (`G-XXXXXXXXXX`). Envía `generate_lead` en cada clic a WhatsApp. |
| `mensajes` | Mensajes prellenados de WhatsApp (general, categoría, kit y lista propia). |

Cada clic a WhatsApp también envía el evento `whatsapp_click` al `dataLayer`, con `ubicacion` (hero, kit, categoria, etc.) y `detalle`.

## Cambiar una foto

1. Foto **cuadrada** (ideal 800 × 800 px), fondo blanco, producto centrado.
2. En GitHub entra a `assets/kits/` → **Add file → Upload files** y sube la foto con **el mismo nombre** del archivo que reemplaza.
3. *Commit changes*. Las fotos se guardan en el navegador hasta 1 hora.

## Textos que conviene verificar

- "Más de 400 productos": conteo del catálogo en la web (abrasivos + seguridad industrial).
- "20 de diciembre" (entrega de dotación): confirmar con el área legal/contable antes de usarlo en anuncios.
