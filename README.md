Madrid, Cundinamarca — frizo interactivo
Línea de tiempo territorial interactiva, en un solo archivo HTML (sin dependencias de build, sin frameworks). Lista para publicarse en GitHub Pages.
Publicar en GitHub Pages (5 minutos)
Crea un repositorio nuevo en GitHub (puede ser público o privado, pero Pages gratuito requiere público a menos que tengas GitHub Pro).
Sube el archivo `index.html` a la raíz del repositorio (arrástralo en la interfaz web de GitHub, o usa `git add / commit / push`).
Ve a Settings → Pages en el repositorio.
En "Build and deployment", elige Deploy from a branch, rama `main`, carpeta `/ (root)`.
Guarda. GitHub te da la URL pública en 1-2 minutos (algo como `https://tuusuario.github.io/nombre-repo/`).
No necesitas nada más — no hay paso de compilación, ni `npm install`, ni carpeta `dist`.
Cómo editar el contenido
Todo el contenido vive en el arreglo `hojas` dentro de la etiqueta `<script>` al final de `index.html`. Cada hoja tiene un `title` y una lista de `nodes`. Cada nodo tiene:
`id`: identificador único (no lo repitas entre nodos)
`type`: `'node'` (círculo rojo, periodo normal), `'milestone'` (rombo morado, hito especial) o `'finale'` (estrella, cierre)
`top` / `left`: posición dentro de la hoja, en porcentaje (0-100). Ajusta estos números a mano si quieres mover un punto.
`date`, `label`, `summary`: textos cortos
`bullets`: lista de `{tag, text}` — `tag` debe ser uno de `localizacion`, `toponimia`, `jurisdiccion`, `productivo`, `sociocultural`. `text` acepta HTML simple como `<b>negrita</b>`.
`media`: texto del marcador de foto/mapa, o `null` si el momento no lleva imagen.
Reemplazar los marcadores verdes por fotos reales
Cada tarjeta desplegada tiene un bloque verde con el texto "— foto/mapa pendiente". Para poner una imagen real:
Crea una carpeta `img/` junto a `index.html` y copia ahí tus fotos.
En el arreglo de datos, cambia por ejemplo:
```js
   media: 'Laguna de la Herrera — foto/mapa pendiente'
   ```
por:
```js
   media: '<img src="img/laguna-herrera.jpg" alt="Laguna de la Herrera" style="width:100%;height:100%;object-fit:cover;border-radius:inherit;">'
   ```
Busca el bloque `.media-placeholder` en el JavaScript (función que arma el `drawer`) y cambia `ph.textContent = n.media;` por `ph.innerHTML = n.media;` para que el HTML de la imagen se renderice en vez de mostrarse como texto plano.
Notas técnicas
Un solo archivo, sin dependencias salvo la tipografía de Google Fonts (Kalam + Work Sans), cargada por CDN — funciona sin conexión igual, solo se ven las tipografías de respaldo del sistema.
El hilo rojo se dibuja en JavaScript conectando los centros reales de los puntos (no son coordenadas fijas), así que se recalcula solo si cambias el contenido, el ancho de pantalla, o agregas/quitas nodos.
Funciona con teclado (Tab + Enter/Espacio) y respeta `prefers-reduced-motion`.
