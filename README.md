# Sitio ECCSA

Landing de una sola página para Electro Control Coatzacoalcos (ECCSA). El repo completo es
lo que debe quedar dentro de `public_html/eccsa` en Hostinger.

## Antes de publicar: reemplazar el dominio

El archivo usa `https://tudominio.com/eccsa/` como marcador en 4 lugares. Reemplázalo por la
URL real antes del primer deploy:

- [index.html](index.html): `<link rel="canonical">`, `og:url`, `og:image` (líneas ~8, 15, 16)
- [sitemap.xml](sitemap.xml): `<loc>`

Búsqueda rápida: `grep -rn "tudominio.com" .`

Si la ruta final no es `/eccsa/` sino otra subcarpeta, ajusta esas mismas 4 líneas.

## Desplegar con Git en hPanel

1. Crea un repositorio en GitHub y sube este contenido:
   ```
   git remote add origin <URL-de-tu-repo>
   git push -u origin main
   ```
2. En hPanel → tu dominio → **Git**: pega la URL del repo, rama `main` y como directorio de
   instalación `public_html/eccsa`. Da clic en **Crear** y luego **Deploy**.
3. Opcional: copia la URL de webhook que muestra hPanel y agrégala en GitHub →
   *Settings → Webhooks* para que cada `git push` dispare un deploy automático.

Si hPanel no puede clonar el repo (pasa con repos privados sin llave SSH configurada), como
alternativa sube el contenido de esta carpeta por el Administrador de archivos de hPanel
(comprime todo en un .zip, súbelo a `public_html/eccsa` y descomprime ahí).

## robots.txt y sitemap

Este sitio vive en una subcarpeta, así que no lleva su propio `robots.txt` (los buscadores solo
leen el de la raíz del dominio). Añade esta línea al `robots.txt` que ya exista en la raíz del
sitio principal:

```
Sitemap: https://tudominio.com/eccsa/sitemap.xml
```

O da de alta `sitemap.xml` directamente en Google Search Console para esa propiedad.

## Verificación antes y después de publicar

- Abrir [index.html](index.html) local en el navegador: la fuente Archivo debe cargar, sin
  errores en consola, y el botón de menú (ícono de tres líneas) debe abrir/cerrar el menú por
  debajo de 860px de ancho.
- Recorrer la página con Tab desde el principio: debe aparecer primero el enlace "Saltar al
  contenido" y cada elemento enfocable debe mostrar un contorno naranja.
- Probar los 2 `tel:`, los 2 `mailto:` y los 3 enlaces de WhatsApp — cada botón debe abrir el
  número que muestra en su texto.
- Pegar el bloque `<script type="application/ld+json">` del `<head>` en
  https://validator.schema.org y confirmar que no marca errores.
- Ya publicado: cargar la URL real en un teléfono, revisar que aparece el favicon y que al
  compartir el enlace por WhatsApp se ve el título y la imagen de vista previa (`og:image`).

## Fuera de alcance de esta versión

Sin fotos del negocio, sin mapa de ubicaciones, sin páginas propias por línea de catálogo
(las 6 tarjetas de "Catálogo" enlazan a la sección de cotización) y sin formulario propio — el
contacto es por WhatsApp y correo.
