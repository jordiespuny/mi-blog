# Instrucciones para publicar un nuevo post

Cuando el usuario pida crear un nuevo post, sigue estos pasos en orden.

## 1. Crear el archivo del post

- Usa `posts/_plantilla.html` como base
- Guarda el nuevo archivo en `posts/` con un nombre en minúsculas, sin espacios ni tildes, descriptivo del tema (ej: `posts/redes-sociales.html`)
- Escribe el contenido en castellano
- Rellena todos los campos de la plantilla:
  - `TÍTULO DEL POST` — título claro y directo
  - `FECHA` — fecha de hoy en formato `DD de mes de AAAA` (ej: `19 de febrero de 2025`)
  - `CATEGORÍA` — una o dos palabras que describan el tema
  - `AUTOR` — usa `El Equipo` si el usuario no especifica autor
  - El cuerpo del artículo debe tener al menos tres párrafos, un subtítulo `<h2>` y, si encaja, un `<blockquote>` con una idea destacada

## 2. Actualizar el índice

- Abre `index.html`
- Añade un nuevo `<li>` al principio de la lista `<ul class="post-list">`, antes de los posts existentes
- Sigue exactamente este formato:

```html
<li>
  <div class="post-meta">FECHA &mdash; CATEGORÍA</div>
  <h2><a href="posts/NOMBRE-DEL-ARCHIVO.html">TÍTULO DEL POST</a></h2>
  <p class="post-excerpt">RESUMEN DE DOS LÍNEAS.</p>
</li>
```

- El resumen debe ser una frase corta que invite a leer, no el primer párrafo completo

## 3. Publicar

Ejecuta estos comandos en la terminal, en este orden:

```bash
git add .
git commit -m "Nuevo post: TÍTULO BREVE"
git push
```

Sustituye `TÍTULO BREVE` por dos o tres palabras que describan el post.

## 4. Confirmar

Cuando hayas terminado, indica al usuario:
- El nombre del archivo creado
- Que el enlace ya está en `index.html`
- Que el post está publicado (o que ejecute los comandos si prefiere hacerlo manualmente)
