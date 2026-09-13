# Sitio ECCSA

Landing de una sola página para Electro Control Coatzacoalcos (ECCSA).

Actualmente en producción en **https://eccsa-site.vercel.app**, con repo en GitHub
(`cabragonzalez12-lab/eccsa-site`) enlazado a un proyecto de Vercel: cada `git push` a `main`
despliega solo. El canonical, `og:url`, `og:image` y `sitemap.xml` ya apuntan a esa URL.

Este mismo repo también sirve para subir a Hostinger como subcarpeta (`public_html/eccsa`) si se
prefiere ese camino — ver la sección de Git en hPanel más abajo.

## Si cambia el dominio (Hostinger o dominio propio)

Si más adelante el sitio se mueve a `tudominio.com/eccsa/` o a otra URL, actualiza:

- [index.html](index.html): `<link rel="canonical">`, `og:url`, `og:image`
- [sitemap.xml](sitemap.xml): `<loc>`

Búsqueda rápida: `grep -rn "eccsa-site.vercel.app" .`

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

Como el sitio vive en la raíz de `eccsa-site.vercel.app`, lleva su propio `robots.txt` apuntando a
`sitemap.xml`. Si en el futuro se mueve a una subcarpeta de otro dominio (por ejemplo
`tudominio.com/eccsa/`), hay que quitar este `robots.txt` (los buscadores solo leen el de la raíz
del dominio) y en su lugar añadir la línea `Sitemap: https://tudominio.com/eccsa/sitemap.xml` al
`robots.txt` del sitio principal, o dar de alta `sitemap.xml` directamente en Search Console.

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
