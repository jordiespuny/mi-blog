# Publicar en la web sin WordPress: un flujo editorial con Cursor, GitHub y Netlify

**Fecha:** 19 de febrero de 2025  
**Categoría:** CMS · Flujos editoriales · Herramientas

---

Cuando hablamos de gestión de contenidos en clase, WordPress aparece casi inevitablemente como referencia. Y tiene sentido: es el CMS más usado del mundo, alimenta más del 40% de los sitios web y tiene una comunidad enorme. Pero precisamente por su éxito, WordPress ha acumulado capas: base de datos, temas, plugins, editor de bloques, panel de administración... Capas que resuelven problemas reales, pero que también pueden dificultar ver qué es, en el fondo, un sistema de gestión de contenidos.

Este artículo documenta un ejercicio de clase cuyo objetivo no es técnico sino editorial: proponer un flujo de publicación diferente, más desnudo, que permita entender qué ocurre realmente cuando publicamos contenido en la web.

---

## La pregunta de partida

¿Qué necesita, como mínimo, un sistema para publicar artículos en la web?

Si lo pensamos sin asumir ninguna tecnología concreta, la respuesta es bastante simple:

1. Un lugar donde escribir y guardar el contenido
2. Una forma de darle estructura y presentación
3. Un servidor que lo sirva al navegador

WordPress responde a esto con: base de datos + editor visual + servidor PHP. Pero no es la única respuesta posible. La misma necesidad puede cubrirse con: archivos HTML + un editor de texto + Netlify.

El ejercicio propone exactamente eso.

---

## Las herramientas del flujo

### Cursor

[Cursor](https://www.cursor.com) es un editor de código que integra un asistente de inteligencia artificial. En este ejercicio lo usamos como si fuera el "panel de administración": el lugar desde donde se crea y edita el contenido. La diferencia respecto a WordPress es que en lugar de rellenar formularios en un navegador, describimos en lenguaje natural lo que queremos publicar y Cursor genera el archivo.

### GitHub

GitHub actúa como el repositorio central del blog: el lugar donde viven todos los archivos y donde queda registrado cada cambio. Cada vez que publicamos un artículo nuevo, hacemos un `git push` que envía los cambios al repositorio remoto. Este paso es el equivalente a pulsar "Publicar" en WordPress, con una diferencia importante: el historial de cambios queda guardado y es reversible.

### Netlify

Netlify es el servidor. Está conectado al repositorio de GitHub y monitoriza cada nuevo `push`. Cuando detecta un cambio, regenera y publica el sitio automáticamente en cuestión de segundos. No hay que configurar servidores, ni gestionar hosting, ni preocuparse por actualizaciones. Para proyectos estáticos como este, el plan gratuito es más que suficiente.

---

## La estructura del blog

El blog es un conjunto de archivos HTML organizados en carpetas:

```
mi-blog/
├── index.html              ← Página de inicio con la lista de artículos
├── css/
│   └── style.css           ← Estilos tipográficos del blog
└── posts/
    ├── _plantilla.html     ← Plantilla base para nuevos artículos
    ├── bienvenida.html     ← Primer artículo
    └── ia-y-periodismo.html← Segundo artículo
```

No hay base de datos. No hay servidor de aplicaciones. Cada artículo es un archivo `.html` dentro de la carpeta `posts/`. La página de inicio es otro archivo HTML que enlaza manualmente a cada artículo.

Esto expone algo que los CMS ocultan: el índice de contenidos no se genera solo. Alguien —o algo— tiene que mantenerlo actualizado. En WordPress lo hace automáticamente el sistema. En este blog, lo hace Cursor cuando le pedimos que añada el enlace del nuevo artículo en `index.html`.

---

## El flujo editorial, paso a paso

### Antes de la primera publicación: configuración inicial

Este paso se hace una sola vez. Desde la Terminal del Mac:

```bash
# Entrar en la carpeta del proyecto
cd ~/Desktop/mi-blog

# Iniciar el repositorio Git
git init

# Añadir todos los archivos
git add .

# Primer commit
git commit -m "Primer commit: estructura del blog"
```

Después, en GitHub se crea un repositorio vacío llamado `mi-blog` y se conecta con el proyecto local:

```bash
git remote add origin https://github.com/TU_USUARIO/mi-blog.git
git push -u origin main
```

En Netlify, se accede al panel, se pulsa *Add new site → Import an existing project*, se selecciona el repositorio de GitHub y se despliega. Sin configuración adicional: no hay proceso de compilación porque los archivos ya son HTML puro.

El blog está publicado. Tiene una URL del tipo `https://nombre-aleatorio.netlify.app`.

### Publicar un artículo nuevo

A partir de aquí, el flujo para cada nuevo artículo tiene tres momentos:

**1. Crear el contenido con Cursor**

Se abre el proyecto en Cursor y se escribe en el chat del asistente:

> *"Crea un nuevo post sobre el futuro de las redes sociales. Usa la plantilla `_plantilla.html`, guárdalo como `posts/redes-sociales.html` con fecha de hoy, y añade el enlace al inicio de la lista en `index.html`."*

Cursor lee la plantilla existente, genera el nuevo archivo con el contenido solicitado y actualiza el índice. El proceso tarda menos de un minuto.

**2. Revisar**

Antes de publicar, se puede abrir el archivo HTML en el navegador directamente desde el Mac (sin necesidad de servidor local) para revisar que el contenido y los enlaces están correctos.

**3. Publicar**

```bash
git add .
git commit -m "Nuevo post: el futuro de las redes sociales"
git push
```

Netlify detecta el push en segundos y publica automáticamente. El artículo está en línea.

---

## Qué enseña este flujo sobre los CMS

El ejercicio no pretende proponer una alternativa seria a WordPress para proyectos complejos. Pretende hacer visible lo que los CMS normalmente ocultan.

### El contenido es datos

En WordPress, los artículos viven en una base de datos MySQL. Cuando cargas una página, PHP consulta esa base de datos, recupera el contenido, lo combina con la plantilla del tema y genera el HTML que recibe el navegador. Todo esto ocurre en milisegundos y de forma invisible.

En este blog, el HTML ya existe como archivo. No hay consulta, no hay generación dinámica. El navegador recibe exactamente lo que hay en disco.

Ambos enfoques tienen ventajas y limitaciones. La base de datos permite buscar, filtrar, categorizar y relacionar contenidos a escala. Los archivos estáticos son más rápidos, más baratos de servir y más fáciles de versionar.

### El índice no se actualiza solo

Una de las tareas que los CMS automatizan es la generación de índices: la portada del blog, los archivos por categoría, las páginas de etiquetas. En este blog, esa tarea la delega en Cursor. Es un detalle pequeño, pero ilustra bien por qué los CMS existen: para automatizar las partes repetitivas de gestionar contenido.

### El flujo editorial tiene forma

En WordPress el flujo es: panel → nuevo post → editor → publicar. En este blog es: Cursor → HTML → git push → Netlify. Ambos son flujos editoriales. La diferencia está en las herramientas, en la curva de aprendizaje y en el nivel de abstracción.

Ninguno es universalmente mejor. Depende del contexto, del equipo y del tipo de contenido.

---

## Limitaciones del enfoque

Este sistema no escala bien para equipos. No tiene sistema de usuarios ni roles. No tiene búsqueda interna. No tiene gestión de medios. No tiene comentarios. No permite previsualizar borradores online antes de publicar.

Todo eso lo resuelve WordPress —y lo resuelve bien. La pregunta interesante no es cuál es mejor en abstracto, sino cuándo merece la pena la complejidad adicional de un CMS completo.

Para un blog personal, un portfolio, la documentación de un proyecto pequeño o un prototipo de publicación, este flujo puede ser más que suficiente. Para un periódico digital con múltiples redactores, secciones, suscriptores y publicidad, evidentemente no.

---

## Para seguir explorando

Este ejercicio es una versión muy simplificada de lo que hacen sistemas como [Eleventy](https://www.11ty.dev/), [Hugo](https://gohugo.io/) o [Astro](https://astro.build/): generadores de sitios estáticos que automatizan la parte de crear el HTML a partir de archivos de contenido, normalmente escritos en Markdown.

El artículo de Nick Diego [*Migrating from WordPress to MDX*](https://nickdiego.com/migrating-from-wordpress-to-mdx) documenta exactamente ese camino: de WordPress a archivos de texto plano gestionados con IA, para un sitio personal donde la velocidad de iteración importa más que la interfaz visual.

La conclusión que se puede extraer no es que WordPress sea obsoleto —no lo es— sino que la elección de herramientas debería responder siempre a una pregunta concreta: ¿qué necesita este proyecto para funcionar bien? A veces la respuesta es un CMS con todas sus capas. A veces es una carpeta de archivos HTML y tres comandos de terminal.

---

*Este artículo forma parte de los materiales de la asignatura de CMS. El proyecto completo —estructura del blog, plantilla y guía de instalación— está disponible para descarga en el repositorio del curso.*
