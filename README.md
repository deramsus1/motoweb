# MecánicaMoto — sitio estático

Sitio de guías de mantenimiento de motos, listo para publicar en Cloudflare Pages
y monetizar con Google AdSense.

## Estructura

```
index.html          → portada
about.html           → sobre nosotros
contact.html         → contacto
privacy.html         → política de privacidad (rellenar datos entre [corchetes])
terms.html           → términos de uso (rellenar datos entre [corchetes])
guias/*.html         → 12 guías de mantenimiento
css/style.css        → estilos del sitio
robots.txt / sitemap.xml
```

## 1. Antes de publicar

1. Busca y reemplaza `nexusconverters.com` por tu dominio real en TODOS los archivos
   (aparece en las etiquetas `<link rel="canonical">`, en `sitemap.xml`,
   `robots.txt` y en las páginas de contacto/legales).
   En Linux/Mac puedes hacerlo con:
   ```
   grep -rl "nexusconverters.com" . | xargs sed -i '' 's/nexusconverters.com/tudominio-real.com/g'
   ```
   (en Linux sin macOS quita el `''` después de `-i`).
2. Rellena los datos entre `[corchetes]` en `privacy.html` y `terms.html`
   (tu nombre/razón social, país, correo de contacto). Son plantillas de
   partida, no asesoría legal — si vas a tener tráfico de la UE, revísalas
   bien o consulta a un profesional.
3. Cambia `contacto@nexusconverters.com` en `contact.html` por tu correo real.

## 2. Publicar en Cloudflare Pages

1. Sube esta carpeta a un repositorio de GitHub (o usa "Direct upload" en
   Cloudflare Pages, que te deja arrastrar la carpeta directamente sin Git).
2. En el panel de Cloudflare → **Workers & Pages** → **Create application** →
   **Pages** → conecta el repo (o sube los archivos directamente).
3. No necesitas comando de build: es HTML estático. Deja el "build command"
   vacío y el "output directory" como `/` (raíz).
4. Una vez desplegado, ve a **Custom domains** dentro del proyecto de Pages
   y añade tu dominio (el que ya tienes en Cloudflare). Se conecta con un
   clic porque el dominio ya vive en tu cuenta.

## 3. Solicitar Google AdSense

Google **no aprueba sitios sin contenido real**, así que antes de solicitar:

- Ten el sitio publicado y accesible desde tu dominio final (no localhost).
- Asegúrate de que las páginas de política de privacidad, términos y
  contacto están rellenas con datos reales (no lo genérico entre corchetes).
- Espera a tener el sitio indexado unos días en Google (puedes acelerarlo
  enviando `sitemap.xml` en Google Search Console).

Pasos:
1. Crea una cuenta en https://www.google.com/adsense
2. Añade tu sitio y pega el fragmento de verificación (un `<script>`) que
   Google te dé justo antes de `</head>` en TODAS las páginas — lo más
   fácil es añadirlo una vez en `css/style.css`... en realidad va en el
   `<head>` del HTML, así que si el sitio crece te conviene automatizarlo
   con una plantilla o un pequeño script (como hicimos aquí con `generate.py`
   si decides ampliarlo).
3. Cuando Google apruebe el sitio, sustituye los bloques marcados como
   `<div class="ad-slot">ESPACIO PUBLICITARIO (Google AdSense)</div>`
   por el código real de tus unidades de anuncio de AdSense.
4. Crea un archivo `ads.txt` en la raíz del sitio con la línea que
   AdSense te indique (algo como
   `google.com, pub-XXXXXXXXXXXXXXXX, DIRECT, f08c47fec0942fa0`) — es
   obligatorio para que los anuncios se muestren correctamente.

## 4. Cómo ganar tráfico (y por tanto dinero)

AdSense paga por impresiones y clics, así que sin tráfico no hay ingresos.
Las guías ya están escritas pensando en SEO (títulos claros, un H1 por
página, meta descripción), pero para crecer de verdad conviene:

- Publicar contenido nuevo con regularidad (más guías, o actualizaciones
  de las existentes).
- Usar títulos que la gente realmente busca en Google (long-tail:
  "cada cuánto cambiar el aceite de una moto 125" rinde mejor que
  términos genéricos).
- Compartir las guías en foros y comunidades de motos donde ya se
  discuten estos temas (aportando valor, no solo enlazando).
- Dar de alta el sitio en Google Search Console y enviar `sitemap.xml`.

## Añadir más guías

El sitio se generó con dos scripts Python (`generate.py` para las guías y
`build_index.py` para la portada) que ya no están en esta carpeta para
mantenerla limpia, pero si quieres que te genere más artículos con el
mismo formato y ficha técnica, solo pídemelo.
