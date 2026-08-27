# Migración SEO de orvis.com.ar a eflyshop.com.ar

Guía para transferir el posicionamiento de las páginas de `orvis.com.ar` a sus nuevas ubicaciones en `eflyshop.com.ar` mediante redirecciones permanentes 301.

## 1. Mapeo definitivo de URLs

| URL anterior | URL nueva |
| --- | --- |
| `https://www.orvis.com.ar/` | `https://www.eflyshop.com.ar/ag/content/orvis-argentina/9` |
| `https://www.orvis.com.ar/canas-orvis-made-in-usa.html` | `https://www.eflyshop.com.ar/ag/content/canas-orvis-hechas-en-usa/11` |
| `https://www.orvis.com.ar/orvis-helios-4-argentina.html` | `https://www.eflyshop.com.ar/ag/content/orvis-helios-4-argentina/10` |

Cada URL anterior debe redirigir directamente a su equivalente. No se debe enviar todo el dominio antiguo a una única portada.

## 2. Preparar eflyshop antes de activar la migración

Comprobar en las tres páginas nuevas:

- Que estén activas y respondan directamente con estado HTTP `200`.
- Que no tengan una etiqueta `noindex`.
- Que no estén bloqueadas por `robots.txt`.
- Que cada una tenga un título, una metadescripción y un único título principal coherente.
- Que cada canonical apunte a su propia URL de `eflyshop.com.ar`.
- Que estén incluidas en el sitemap de PrestaShop.
- Que las imágenes y los enlaces internos funcionen.
- Que las versiones en español e inglés estén correctamente relacionadas.

### Enlaces internos de la página Orvis Argentina

En:

```text
https://www.eflyshop.com.ar/ag/content/orvis-argentina/9
```

El botón de fabricación debe apuntar directamente a:

```text
https://www.eflyshop.com.ar/ag/content/canas-orvis-hechas-en-usa/11
```

El botón de Helios debe apuntar directamente a:

```text
https://www.eflyshop.com.ar/ag/content/orvis-helios-4-argentina/10
```

Buscar en las tres páginas nuevas cualquier enlace que todavía contenga `orvis.com.ar` y reemplazarlo por su URL definitiva de eflyshop.

## 3. Hacer una copia de seguridad

Antes de modificar el dominio anterior:

1. Descargar una copia del `.htaccess` actual.
2. Guardar una copia de `robots.txt` y `sitemap.xml`, si existen.
3. Confirmar que se puede volver a la configuración anterior si aparece un error 500.

## 4. Archivo `.htaccess` para orvis.com.ar

Colocar estas reglas al principio del `.htaccess` de la carpeta raíz de `orvis.com.ar`, antes de cualquier otra regla existente.

```apache
RewriteEngine On

# =========================================================
# PÁGINAS HTML: ORVIS.COM.AR → EFLYSHOP.COM.AR
# =========================================================

# Cañas Orvis hechas en Estados Unidos
RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^canas-orvis-made-in-usa\.html/?$ https://www.eflyshop.com.ar/ag/content/canas-orvis-hechas-en-usa/11 [R=301,L,NE,QSD]

# Orvis Helios 4 en Argentina
RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^orvis-helios-4-argentina\.html/?$ https://www.eflyshop.com.ar/ag/content/orvis-helios-4-argentina/10 [R=301,L,NE,QSD]

# Portada principal
RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^$ https://www.eflyshop.com.ar/ag/content/orvis-argentina/9 [R=301,L,NE,QSD]

# Posibles accesos antiguos a archivos index
RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^index\.(?:html?|php)$ https://www.eflyshop.com.ar/ag/content/orvis-argentina/9 [R=301,L,NE,QSD]

# =========================================================
# IMÁGENES DE LA PORTADA
# =========================================================

RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^img/hero-orvis-argentina\.webp$ https://www.eflyshop.com.ar/img/cms/orvis/hero-orvis-argentina.webp [R=301,L,NE,QSD]

# =========================================================
# IMÁGENES DE FABRICACIÓN DE CAÑAS
# =========================================================

RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^img/hero-fabrica-orvis\.webp$ https://www.eflyshop.com.ar/img/cms/orvis/hero-fabrica-orvis.webp [R=301,L,NE,QSD]

RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^img/fabricacion-canas-orvis\.webp$ https://www.eflyshop.com.ar/img/cms/orvis/fabricacion-canas-orvis.webp [R=301,L,NE,QSD]

RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^img/proceso-cana-orvis\.webp$ https://www.eflyshop.com.ar/img/cms/orvis/proceso-cana-orvis.webp [R=301,L,NE,QSD]

RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^img/detalle-cana-orvis\.webp$ https://www.eflyshop.com.ar/img/cms/orvis/detalle-cana-orvis.webp [R=301,L,NE,QSD]

# =========================================================
# IMÁGENES DE HELIOS 4
# =========================================================

RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^img/helios-hero\.webp$ https://www.eflyshop.com.ar/img/cms/orvis/helios-hero.webp [R=301,L,NE,QSD]

RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^img/helios-2024-lp-tracking\.webp$ https://www.eflyshop.com.ar/img/cms/orvis/helios-2024-lp-tracking.webp [R=301,L,NE,QSD]

RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^img/4X_accurate_graphic_long\.webp$ https://www.eflyshop.com.ar/img/cms/orvis/4X_accurate_graphic_long.webp [R=301,L,NE,QSD]

RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^img/helios-2024-tip-3\.webp$ https://www.eflyshop.com.ar/img/cms/orvis/helios-2024-tip-3.webp [R=301,L,NE,QSD]

RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^img/helios-2024-lp-deflection\.webp$ https://www.eflyshop.com.ar/img/cms/orvis/helios-2024-lp-deflection.webp [R=301,L,NE,QSD]

RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^img/25_stronger_graphic\.webp$ https://www.eflyshop.com.ar/img/cms/orvis/25_stronger_graphic.webp [R=301,L,NE,QSD]

RewriteCond %{HTTP_HOST} ^(?:www\.)?orvis\.com\.ar$ [NC]
RewriteRule ^img/helios-2024-lp-f-d-3\.webp$ https://www.eflyshop.com.ar/img/cms/orvis/helios-2024-lp-f-d-3.webp [R=301,L,NE,QSD]
```

No agregar una regla general que redirija cualquier URL desconocida a la nueva portada. Las URLs antiguas sin un equivalente relevante deben devolver un `404` o `410` real para evitar errores de tipo `soft 404`.

## 5. Archivo `robots.txt` de orvis.com.ar

Contenido recomendado:

```text
User-agent: *
Disallow:

Sitemap: https://www.orvis.com.ar/sitemap.xml
```

No bloquear Googlebot. Google necesita volver a visitar las URLs antiguas para descubrir y procesar las redirecciones 301.

## 6. Archivo `sitemap.xml` de orvis.com.ar

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">

  <url>
    <loc>https://www.orvis.com.ar/</loc>
  </url>

  <url>
    <loc>https://www.orvis.com.ar/canas-orvis-made-in-usa.html</loc>
  </url>

  <url>
    <loc>https://www.orvis.com.ar/orvis-helios-4-argentina.html</loc>
  </url>

</urlset>
```

Es normal que Search Console indique posteriormente que estas URLs están redireccionadas.

## 7. Orden para activar la migración

1. Corregir todos los enlaces internos de las páginas nuevas.
2. Regenerar el sitemap de PrestaShop.
3. Confirmar que las tres páginas nuevas aparecen en el sitemap.
4. Verificar que no tengan `noindex`.
5. Verificar los canonical autorreferenciales.
6. Guardar una copia del `.htaccess` anterior.
7. Subir las nuevas reglas al `.htaccess` de `orvis.com.ar`.
8. Subir `robots.txt` y `sitemap.xml`.
9. Purgar la caché si `orvis.com.ar` utiliza Cloudflare.
10. Probar todas las redirecciones.
11. Realizar el Cambio de dirección en Google Search Console.

## 8. Pruebas necesarias

Probar en una ventana privada:

```text
http://orvis.com.ar/
https://orvis.com.ar/
http://www.orvis.com.ar/
https://www.orvis.com.ar/

https://www.orvis.com.ar/canas-orvis-made-in-usa.html
https://www.orvis.com.ar/orvis-helios-4-argentina.html
```

Todas deben llegar directamente a su equivalente en eflyshop, sin páginas intermedias ni cadenas de redirecciones.

### Pruebas desde una terminal

```bash
curl -I https://www.orvis.com.ar/
curl -I https://www.orvis.com.ar/canas-orvis-made-in-usa.html
curl -I https://www.orvis.com.ar/orvis-helios-4-argentina.html
```

El resultado esperado para la portada es similar a:

```text
HTTP/2 301
location: https://www.eflyshop.com.ar/ag/content/orvis-argentina/9
```

Comprobar además que las URLs finales de eflyshop respondan con `200` y no generen otra redirección inesperada.

## 9. Google Search Console

Verificar con la misma cuenta:

- La propiedad de dominio `orvis.com.ar`.
- La propiedad de dominio `eflyshop.com.ar`.
- Las variantes `www` y sin `www`, si existen como propiedades separadas.

Después de activar y comprobar los 301:

1. Entrar en la propiedad `orvis.com.ar`.
2. Abrir **Configuración**.
3. Seleccionar **Cambio de dirección**.
4. Elegir `eflyshop.com.ar` como destino.
5. Ejecutar las comprobaciones de Google.
6. Confirmar la migración.
7. Enviar `https://www.orvis.com.ar/sitemap.xml` desde la propiedad anterior.
8. Regenerar y enviar el sitemap de eflyshop desde la propiedad nueva.
9. Inspeccionar las tres URLs nuevas y solicitar su indexación.
10. Inspeccionar las tres URLs antiguas y confirmar que Google detecta los 301.

La herramienta Cambio de dirección funciona a nivel de propiedad de dominio. Las redirecciones individuales son las que informan la correspondencia concreta entre cada URL anterior y su destino.

## 10. Seguimiento posterior

Durante las semanas siguientes:

- Revisar impresiones y clics de ambos dominios en Search Console.
- Comprobar que disminuyan las URLs indexadas de `orvis.com.ar`.
- Comprobar que aumenten las impresiones de las páginas nuevas.
- Revisar errores `404`, redirecciones y canonical seleccionados por Google.
- Actualizar enlaces de redes sociales, Google Business Profile, anuncios y perfiles externos.
- Solicitar la actualización de backlinks importantes que todavía apunten a `orvis.com.ar`.
- No cambiar nuevamente títulos, contenidos o estructura durante las primeras semanas.
- Mantener activo el dominio anterior, el certificado SSL y el servicio que genera los 301.

Google recomienda conservar las redirecciones durante al menos un año. Para los usuarios y los enlaces antiguos, es preferible mantenerlas indefinidamente.

## 11. Fuentes oficiales

- [Migraciones de sitios con cambio de URL — Google Search Central](https://developers.google.com/search/docs/crawling-indexing/site-move-with-url-changes)
- [Redirecciones y Google Search](https://developers.google.com/search/docs/crawling-indexing/301-redirects)
- [Herramienta Cambio de dirección — Search Console](https://support.google.com/webmasters/answer/9370220?hl=es)
- [Cómo especificar una URL canonical](https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls)
- [Solicitar un nuevo rastreo de URLs](https://developers.google.com/search/docs/crawling-indexing/ask-google-to-recrawl)

