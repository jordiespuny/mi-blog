# El Blog — Guía paso a paso

Blog estático de ejemplo para la asignatura de CMS.  
Flujo editorial: **Cursor → GitHub → Netlify**

---

## Estructura del proyecto

```
mi-blog/
├── index.html              ← Página de inicio (lista de posts)
├── css/
│   └── style.css           ← Estilos del blog
└── posts/
    ├── _plantilla.html     ← Plantilla para nuevos posts
    ├── bienvenida.html     ← Post de ejemplo
    └── ia-y-periodismo.html← Post de ejemplo
```

---

## PASO 1 — Subir el proyecto a GitHub

Abre la Terminal y ejecuta estos comandos uno a uno:

```bash
# 1. Entra en la carpeta del proyecto
cd ~/Desktop/mi-blog      # ajusta la ruta si es necesario

# 2. Inicia Git
git init

# 3. Añade todos los archivos
git add .

# 4. Primer commit
git commit -m "Primer commit: estructura del blog"
```

Ahora ve a **github.com**, crea un repositorio nuevo (llámalo `mi-blog`, sin README), y copia los dos comandos que te da GitHub para "push an existing repository":

```bash
git remote add origin https://github.com/TU_USUARIO/mi-blog.git
git push -u origin main
```

---

## PASO 2 — Conectar Netlify con GitHub

1. Ve a **netlify.com** e inicia sesión
2. Pulsa **"Add new site" → "Import an existing project"**
3. Elige **GitHub** y autoriza el acceso
4. Selecciona el repositorio `mi-blog`
5. En la configuración de despliegue, deja todo en blanco (no hay proceso de build)
6. Pulsa **"Deploy site"**

En 30 segundos tu blog estará publicado en una URL del tipo `https://nombre-aleatorio.netlify.app`.  
Puedes cambiar ese nombre en *Site settings → Domain management*.

---

## PASO 3 — Publicar un nuevo post (el ejercicio de clase)

### Opción A: tú escribes el HTML manualmente

1. Duplica `posts/_plantilla.html` y dale un nombre descriptivo (ej: `redes-sociales.html`)
2. Edita el contenido: título, fecha, categoría, autor, texto
3. Abre `index.html` y añade un nuevo `<li>` en la lista, apuntando al nuevo archivo
4. Guarda los cambios

### Opción B: Cursor lo hace por ti (demo en clase)

Abre el proyecto en **Cursor** y escribe en el chat:

> *"Crea un nuevo post sobre el futuro de las redes sociales. Usa la plantilla `_plantilla.html`, guárdalo como `posts/redes-sociales.html`, y añade el enlace correspondiente en `index.html` al principio de la lista."*

Cursor creará el archivo y actualizará el índice automáticamente.

### Subir y publicar

```bash
git add .
git commit -m "Nuevo post: redes sociales"
git push
```

Netlify detecta el push y publica en **menos de 30 segundos**.  
Abre la URL de tu sitio — el nuevo post ya está en línea.

---

## Analogía con WordPress

| Acción en WordPress | Equivalente en este blog |
|---|---|
| Entrar al panel de admin | Abrir el proyecto en Cursor |
| Crear nuevo post | Crear un archivo `.html` |
| Escribir en el editor de bloques | Editar el HTML (o pedírselo a Cursor) |
| Publicar | `git push` |
| Servidor de WordPress | Netlify |
| Base de datos | Los propios archivos `.html` |

---

## Pregunta para debatir en clase

> ¿Qué ventajas y limitaciones tiene este flujo respecto a WordPress?  
> ¿Para qué tipo de proyecto tiene sentido? ¿Para cuál no?
