# Test FrontEnd - MercadoLibre
Desarrollo del test para el puesto de Desarrollador FrontEnd en MercadoLibre.
### Resumen
La consigna consiste en desarrollar una aplicación web que permita buscar, listar y ver detalles de productos de MercadoLibre mediante su API.
## Tecnologías
Frontend:
- ReactJS (v16.3.2)
- Sass
- HTML

Backend:
- NodeJS (v8.11.1)
- ExpressJS

Tanto cliente como servidor fueron escritos en ECMAScript 6.
### Instalación y despliegue
Backend:
```
cd backend
npm install
npm start
```
Frontend:
```
cd frontend
npm install
npm run build
npm install -g http-server
cd build
http-server -a localhost -p 3003 -o
```
##### Nota
Por defecto el servidor corre en `localhost:3002`, en modo "dev" (desarrollo) y espera que el cliente corra en `localhost:3003`, que a su vez es la IP y puerto usados por el cliente por defecto.
Si es necesario hacer cambios para ejecutar los proyectos deben hacerse sobre los archivos ".env" en sus carpetas respectivas. En caso de ejecutar el build del cliente, los parámetros de IP y puerto deben ser especificados en el comando `http-server -a IP -p PUERTO -o`.
**Importante:** si se cambia la IP y puerto del servidor es necesario modificar manualmente la constante usada por el cliente (en el frontend) **antes de hacer el build** para conectarse correctamente. Esto se hace modificando la constante `const serverUrl = "http://localhost:3002";` en la línea 16 del archivo "frontend/src/utils/api.js".
## Estructura
Básicamente el proyecto está dividido en dos carpetas: "frontend" (aplicación ReactJS) y "backend" (servidor NodeJS).
Además, en la raíz del repositorio está el enunciado, un .json con los resultados de la auditoría de Google Lighthouse y el "README".
- **frontend**
  - public
    - favicon
  - src
    - assets
      - images
      - styles
        - sass
        - css
    - components
    - utils
- **backend**
  - bin
  - routes
  - utils
##### Breve explicación
###### Frontend
La carpeta "public" posee el index.html y los recursos necesarios para optimizar SEO (el index.html posee muchas etiquetas "meta" para este fin).
Dentro de "src" encontramos "assets" donde residen todos los recursos estáticos como ser lo archivos "sass" y sus archivos "css" resultantes procesados.
En "src/components" se encuentran todos los componentes React para la aplicación.
En "src/utils" se ubican utilidades, entre ellas funciones para acceder a la API del servidor, un módulo para *cachear* información en el cliente y otro para mejorar el SEO.
###### Backend
En la carpeta "bin" está el archivo para ejecutar el servidor.
En "routes" está la única ruta utilizada, en este caso la API en sí (donde están definidos los dos "endpoints": `/api/items?q=:query` y `/api/items/:id`).
En "utils" está definido el módulo que se encarga de generar los objetos JSONs para ser devueltos por los "endpoints" de la API.

## Consideraciones
A continuación se muestra una lista de tareas realizadas, consideraciones en cuanto a los requerimientos del enunciado y actividades pendientes que mejorarían aún más el producto resultante (no fueron implementadas pero sí contempladas al momento de entrega):
### Aspectos generales
* Se realizaron pruebas usando "Google Lighthouse Audit" para verificar performance, SEO, accesibilidad y buenas prácticas. Resultados adjuntos.
* Se agregó "ubicación" y mención de "envío gratis" en vista "detalle de item".
* Código comentado: tanto componentes, como módulos creados y API.
### Frontend
* Uso de caché usando API HTML5 "sessionStorage" sobre datos obtenidos por AJAX. La misma caduca tras 40 segundos.
* Uso de metodología "BEM" para organizar clases CSS y HTML.
* Diseño responsivo usando propiedades "flex-box" de CSS.
* Uso de propiedades CSS con prefijos "-moz-", "-webkit-", etc. para garantizar compatibilidad con navegadores.
* Uso de URLs amigables.
* Uso de íconos png con variaciones para dispositivos con mayor DPI, así como íconos vectoriales .svg.
* Uso de etiquetas "meta" para mejorar SEO.
* Cambio dinámicamente de etiquetas "meta" y "title" para contribuir a SEO.
* Uso de etiquetas y organización semántica de contenido.
* Uso de atributos AIRA para mejorar la accesibilidad.
* Mostrar componente "cargando" para informar al usuario.
* Uso de Sass para definir estilos.
* Uso de gulp para automatizar creación de .css a partir de .scss
* Creación de página "No encontrado" y sección genérica para mostrar mensajes para el usuario.
* Uso de etiquetas "meta" de OpenGraph.
* Se hizo uso de recursos "extra" como ser íconos, imágenes, etc. Sus fuentes están en el archivo "about.txt" en  la carpeta "assets".
* Uso de unidades "rem" en CSS para definir dimensiones.
* Para mejorar aún más la accesibilidad se usó un color de letra más oscuro que el sugerido en las especificaciones (para conseguir más contraste).
###### Pendientes en frontend:
* Hacer uso de componente propio "FloatingMessage" para mostrar alerta a usuarios de una forma más amigable.
* Crear "templates mockups" o "templates HTML vacíos" de los componentes para así tener una respuesta visual muy rápida para el usuario, y llenar el template cuando los datos estén disponibles.
* Agregar Google Analytics.
* Agregar botón "volver a listado" para permitir la fácil navegación con el teclado desde la vista de detalle hacia lista de items.
### Backend
* Uso de "Promises" para orquestar las peticiones y respuesta a la API de MercadoLibre.
* Definición de cabeceras HTTP de CORs por motivos de seguridad y habilitando sólo la dirección del cliente frontend consultar el backend.
* Al hacer petición a la API de MercadoLibre para obtener *thumbnails* de los items en el listado, se reemplaza un valor del nombre del recurso para mostrar una imagen de mejor calidad.
* La API desarrollada siempre devuelve **todos los campos** al cliente en su JSON, es decir, en caso de que la API de MercadoLibre no devuelva algún recurso o retorne un HTTP Status Code 404, la API desarrollada setea la propiedad en cuestión vacía para el JSON a retornar.
* Es posible modificar los parámetros de configuración antes de ejecutar el servidor en el archivo ".env" en la raíz del proyecto backend.
###### Pendientes en backend:
* Crear mecanismo de caché para datos devueltos por la API de MercadoLibre (específicamente las "monedas" o "currencies").
---
Desarrollado por Ing. Diego Barrionuevo. Fecha: 02/05/2018
