# FRONTEND (con Svelte)
En este repositorio solo se encuentra el frontend de la aplicación. Si deseas ver el backend puedes ir aquí.
[backend](https://github.com/josefilter/ProyectoHospital)

## Introducción

Actualmente (año 2020), en el mundo del desarrollo web se vive una efervescencia de nuevas tecnologías. 

Como base tenemos a los 3 pilares fundamentales:

- **HTML 5**
- **CSS 3**
- **Javascript (EcmaScript 6)**

Son lenguajes que todo desarrollador web debería conocer con cierta soltura.

Tanto HTML 5 como CSS 3 han crecido mucho y actualmente cada uno de estos estándares se organiza en distintas partes. 

En cuanto a Javascript, es a partir de 2015 (estándar ECMAScript 6), que  llegó con un montón de nuevas características después de muchos años de indefinición, cuando ha resurgido un gran interés por este lenguaje, ya no sólo para desarrollo de scripts web, sino también como lenguaje a tener en cuenta para el desarrollo de aplicaciones.


## ¿Qué es svelte?

Existen muchas bibliotecas y frameworks para desarrollo en Javascript, tanto para su uso en el **backend** con node.js, como en el **frontend**.

En cuanto al **frontend**, tenemos a **Angular**, **React** y **Vue** como las bibliotecas/frameworks más usadas/os. 

Svelte es un **compilador** (también puede calificarse como framework), que toma muchas ideas prestadas de los frameworks anteriores, sobre todo de React. Sin embargo hay una característica que lo diferencia de los anteriores: 

- Svelte **realiza una compilación** de nuestro código, convirtiendo sus componentes en código imperativo altamente eficiente.

Proporcionando las siguientes ventajas:

- Tenemos que escribir mucho menos código frente a otros frameworks.
- El código final se ejecuta de forma muy eficiente y rápida.
- El peso (cantidad de KB) de la aplicación final es muy pequeño.
- Facilita la programación reactiva.

Un ventaja añadida es que su sintaxis es más simple, lo cual hace que su curva de aprendizaje sea menos pronunciada que la de otros frameworks. Por este motivo es un buen candidato para su uso con fines didácticos.


## Inicio de un proyecto de svelte

Para iniciar un proyecto de svelte, ejecutamos:

```console
npx  degit  sveltejs/template   nombre-proyecto
```

> Nota: Sustituimos *nombre-proyecto* por el nombre concreto que queramos dar.


## Examinar el proyecto creado

Entramos en el directorio del proyecto, ejecutando:

```console
cd   nombre-proyecto  &&  ls 
```

> Nota: Sustituimos *nombre-proyecto* por el nombre concreto.

Para ver todo el contenido podemos ejecutar el comando `tree`:

```
├── package.json
├── public
│   ├── favicon.png
│   ├── global.css
│   └── index.html
├── README.md
├── rollup.config.js
└── src
    ├── App.svelte
    └── main.js
```

El archivo `package.json` es el archivo de gestión de proyecto y dependencias. En él. podremos editar el nombre del autor, la versión, el tipo de licencia, etc.

La carpeta `public` contiene el frontend en forma de contenido estático, el cual deberemos subir a nuestro servidor de producción una vez finalizado el proyecto.

El archivo `README.md` puede eliminarse o podemos editarlo a nuestro gusto. No es necesario para el funcionamiento de la aplicación, aunque pudiera ser interesante para fines de documentación.

El archivo `rollup.config.js` contiene la configuración del empaquetador, que en este caso es **Rollup**. Otros frameworks utilizan otros empaquetadores como Webpack o Parcel. No debemos borrar este archivo. Tampoco lo editaremos, por ahora.

Finalmente, la carpeta `src` va a contener **nuestro código y todos los componentes web que vayamos creando**. Cada vez que realicemos un cambio en los archivos de dicha carpeta, rollup volverá a compilar y pondrá el resultado en `public/build/bundle.css` y `public/build/bundle.js`. 

El archivo `public/index.html` tiene enlaces a los anteriores. Su código lo podemos ver en el código fuente en este repositorio.
[index.html](https://github.com/josefilter/ProyectoHospitalFrontend/blob/master/public/index.html)


## Empezar a trabajar en el proyecto

Abriremos nuestro editor favorito y comenzaremos a editar los archivos que están en la carpeta `src`.

El contenido de los archivos `src/main.js` y `src/App.svelte` es el que se muestra a continuación:

**`src/main.js`**

```javascript
import App from './App.svelte';

const app = new App({
        target: document.body,
        props: {
                name: 'world'
        }
});

export default app;
```

**`src/App.svelte`**

```html
<script>
        export let name;
</script>

<main>
        <h1>Hello {name}!</h1>
        <p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
</main>

<style>
        main {
                text-align: center;
                padding: 1em;
                max-width: 240px;
                margin: 0 auto;
        }

        h1 {
                color: #ff3e00;
                text-transform: uppercase;
                font-size: 4em;
                font-weight: 100;
        }

        @media (min-width: 640px) {
                main {
                        max-width: none;
                }
        }
</style>
```

Para ejecutar la aplicación deberemos ejecutar:

```console
npm  run  dev
```

La ejecución del script anterior dará error. El motivo es que no hemos instalado las dependencias que aparecen indicadas en el archivo `package.json`.

Para instalar dichas dependencias, ejecutamos:

```
npm  install
```

Dicho comando, leerá el archivo `package.json`, e instalará todas las dependencias que aparecen ahí. Ahora ya podemos volver a ejecutar `npm  run  dev`.

Podrás ver la aplicación en [localhost:5000](http://localhost:5000).


## Simplificando antes de comenzar

El archivo `src/main.js` podemos simplicarlo eliminando algunas líneas. Quedaría de esta manera:
[main.js](https://github.com/josefilter/ProyectoHospitalFrontend/blob/master/src/main.js)

Este archivo es el punto de entrada a la aplicación. Se genera un objeto `app` que se instancia a partir del componente `App.svelte`.


## Desarrollando nuestro primer componente

Vamos a modificar el componente `App.svelte`.

El contenido que tendrá sera el siguiente:

[App.svelte](https://github.com/josefilter/ProyectoHospitalFrontend/blob/master/src/App.svelte)

En la sección de `script` importamos los paquetes y componentes que vayamos a usar. En este caso importamos el componente `Router` que está en el paquete `svelte-routing`. Este paquete nos proporciona los componentes necesarios para crear enrutatodores (`Router`), enlaces (`Link`) y rutas (`Route`). Necesitaremos tener instalado dicho paquete, por lo que debemos ejecutar en el terminal:

```console
npm  install  svelte-routing
```

Vamos a importar también los componentes `Nav` y `Contenido`, que van a estar en la misma carpeta que `App`, y que vamos a crear más adelante.

## Componentes de navegación y contenido

Crearemos dos componentes llamados `Nav.svelte` y `Contenido.svelte`. Debe estar en la misma carpeta que el componente `App.svelte`.

**`Nav.svelte`**
[Nav.svelte](https://github.com/josefilter/ProyectoHospitalFrontend/blob/master/src/Nav.svelte)

**`Contenido.svelte`**
[Contenido.svelte](https://github.com/josefilter/ProyectoHospitalFrontend/blob/master/src/Contenido.svelte)

El componente `Nav`, que tendrá los enlaces (`Link`) necesarios para la navegación, y el componente `Contenido`, que tendrá las rutas (`Routes`) a los componentes necesarios.


## Componentes para el contenido

Dentro del componente anterior `Contenido` podrán renderizarse distintos componentes, dependiendo del `Link` que pulsemos en la barra de navegación. Los componentes que podrán aparecer en `Contenido` son:

- **Inicio**
- **Doctores**
- **Pacienes**

**`Inicio.svelte`**
[Inicio.svelte](https://github.com/josefilter/ProyectoHospitalFrontend/blob/master/src/Inicio.svelte)

Este componente mostrará información acerca de la aplicación. Sólo posee código HTML y CSS. No necesita solicitar datos al servidor. Por tanto su carga es inmediata, y por este motivo lo mostraremos nada más iniciarse la aplicación.

**`Doctores.svelte`**
[Doctores.svelte](https://github.com/josefilter/ProyectoHospitalFrontend/blob/master/src/Doctores.svelte)

**`Pacientes.svelte`**
[Pacientes.svelte](https://github.com/josefilter/ProyectoHospitalFrontend/blob/master/src/Pacietes.svelte)


## Otros componentes

**`Doctor.svelte`**
[Doctor.svelte](https://github.com/josefilter/ProyectoHospitalFrontend/blob/master/src/Doctor.svelte)

**`Paciente.svelte`**
[Paciente.svelte](https://github.com/josefilter/ProyectoHospitalFrontend/blob/master/src/Paciente.svelte)

**`Boton.svelte`**
[Boton.svelte](https://github.com/josefilter/ProyectoHospitalFrontend/blob/master/src/Boton.svelte)

**`Buscar.svelte`**
[Buscar.svelte](https://github.com/josefilter/ProyectoHospitalFrontend/blob/master/src/Buscar.svelte)

**`store.js`**
[store.js](https://github.com/josefilter/ProyectoHospitalFrontend/blob/master/src/store.js)


## Construir la aplicación para el entorno de producción

Para crear una versión optimizada de la aplicación, ejecutamos:

```bash
npm run build
```

Puedes ejecutar la aplicación recién creada con `npm run start`. Esto utiliza [sirv](https://github.com/lukeed/sirv), que se incluye en las `dependencias` de `package.json` para que la aplicación funcione cuando se implemente en plataformas como [Heroku](https://heroku.com).


## Single-Page App

**Esta es una aplicación de página única (SPA)**.

Por defecto, sirv solo responderá a las solicitudes que coincidan con los archivos en `public`. Esto es para maximizar la compatibilidad con los servidores de archivos estáticos, lo que le permite implementar su aplicación en cualquier lugar.

Si estás creando una aplicación de una sola página (SPA) con varias rutas, sirv debe poder responder a las solicitudes de *cualquier* ruta. Puedes hacerlo editando el comando `"start"` en package.json:

```js
"start": "sirv public --single"
```

> NOTA: sirv es el módulo de node que permite ejecutar un servidor web y mostrar nuestra app.


## Despliegue en la web

Este frontend no contiene código de servidor, es decir, no contiene código para backend. Por tanto podemos desplegarlo como hariamos con cualquier página html. Cualquier sitio que permita **contenido estático** nos vale. 

Existen muchos sitios que ofrecen esta opción, pero nosotros usaremos Now. Para desplegarlo seguiremos los siguientes pasos:

**[now](https://zeit.co/now)**

Instala `now` si aún no lo has hecho:

```bash
npm install -g now
```

Luego, desde la carpeta de tu proyecto:

```bash
cd  public
now  deploy  --name my-project
```

> NOTA: Sustituye *my-project* por el nombre de tu proyecto.

---

## Progressive Web Application

**Esta es una aplicación web progresiva (PWA)**.

La tecnología PWA es relativamente nueva, iniciandose en el año 2015 bajo el auspicio de **Google**.

Dicha tecnología pretende, mediante la aplicación de pequeñas adaptaciones, usar las **tecnologías web (HTML + CSS + Javascript)** para el **desarrollo de aplicaciones de escritorio y móviles**.

Como el lector entendido en el asunto comprenderá rápidamente, las implicaciones de tal tecnología son enormes:

- **Desarrollo para web, para escritorio y para móvil. Todo en uno.**
- **Simplificación del desarrollo**. 
  - "No es necesario" aprender lenguajes como Java o Swift.
  - "No es necesario" desarrollar de forma nativa (SDKs para Android e iOS).
  - "No es necesario" desarrollar de forma híbrida (Frameworks Cordova, React Native, Angular Ionic. Electron para el escritorio)
- **Uso de Web APIs**, las cuales [son bastantes, muchas de ellas aún en desarrollo](https://developer.mozilla.org/en-US/docs/Web/API): fetch, websockets, geolocalización, audio, speech, ... 
 

**Requisitos para considerar progresiva a una aplicación web**

Una PWA debe cumplir, en esencia, 2 requisitos:

- Debe servirse desde un servidor **HTTPS**. Excepción: `localhost`.
- Debe disponer de un archivo **manifest.json** o similar con metadata de la applicación.
- Debe tener capacidad de funcionar **offline**. Para ello es necesario disponer de un *Service Worker*.


Los archivos necesarios para hacer que una aplicación web sea progresiva son:

- `public/manifest.json` 
- `public/images/icons/*`  
- `public/service-worker.js`   

Tanto el archivo `manifest.json` como la carpeta `images` y todos sus iconos, podemos generarlos de manera sencilla con [Web App Manifest Generator](https://app-manifest.firebaseapp.com/).

El archivo `service-worker.js` se encarga de funcionar como intermediario entre nuestro frontend y el backend, y tiene la siguiente apariencia:

```javascript
//------  Este código está simplificado para resaltar la estructura
//------  Para ver todo el código consulta el archivo correspondiente
const CACHE_NAME = 'tiendafrontend-v1';

// Archivos necesarios para el funcionamiento offline
const CACHE_ASSETS = [
  '/',
  '/index.html',
  '/offline.html',
  '/favicon.png'
];

// INSTALL
// Realizamos el cacheo de la APP SHELL
self.addEventListener('install', funcionDeInstalacion);


// ACTIVATE
// Eliminamos cachés antiguas.
self.addEventListener('activate', funcionDeActivacion);


// FETCH
// Hacemos peticiones a recursos.
self.addEventListener('fetch', funcionDeFetch);


// PUSH
self.addEventListener('push', funcionDePush);
```

El código fuente completo puede verse en [public/service-worker.js](./public/service-worker.js)

Además de todo lo anterior, deberemos modificar el archivo **`index.html`** para que aparezcan las siguientes líneas:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <!-- Se eliminan etiquetas html para resaltar lo esencial -->
  <!-- Consulta el código fuente. --> 

	<link rel="icon" type="image/png" href="/favicon.png">
  
	<!-- PWA: Para habilitar Progressive Web Application -->
	<link rel="manifest" href="manifest.json">  <!--                  IMPORTANTE -->
  
	<!-- PWA: Añadir a pantalla de inicio para Safari en iOS -->
	<meta name="apple-mobile-web-app-capable" content="yes">
	<meta name="apple-mobile-web-app-status-bar-style" content="black">
	<meta name="apple-mobile-web-app-title" content="Tienda">
	<link rel="apple-touch-icon" sizes="152x152" href="/images/icons/icon-152x152.png">
	<meta name="msapplication-TileImage" content="/images/icons/icon-144x144.png">
	<meta name="msapplication-TileColor" content="#fdebc9">
  
  <!-- Chrome, Firefox OS and Opera -->
  <meta name="theme-color" content="#fdebc9">

  <!-- Se eliminan etiquetas html para resaltar lo esencial -->
  <!-- Consulta el código fuente. --> 
</head>

<body>
	<noscript>
		<p> Este sitio necesita Javascript para funcionar. </p>
	</noscript>
	<script>
		// Si está soportado serviceWorker por el navegador
		if ('serviceWorker' in navigator) {
		  window.addEventListener('load', () => {
			navigator.serviceWorker
			  .register('./service-worker.js')
			  .then(reg => console.log('[Service Worker] * Registrado.'))
			  .catch(err => console.log(`[Service Worker] * Error: ${err}`));
		  });
		}
	  </script>
	
	  <script src="service-worker.js"></script> <!-- Gestión de eventos del ServiceWorker -->
</body>
</html>
```

Lo que hacemos es **añadir un enlace al archivo `manifest.json`** e indicar los iconos y colores que usaremos.

Además en el `body` de la página, registramos el `service-worker.js` y lo cargamos.

El código fuente completo puede verse en [public/index.html](./public/index.html)

Por último, es recomendable tener un archivo llamado *`offline.html`* o similar, que mostraremos cuando no haya conexión. 

```html
<!DOCTYPE html>
<html lang="es">
<head>
</head>
  <!-- Se eliminan etiquetas html para resaltar lo esencial -->
  <!-- Consulta el código fuente. --> 
<body>
    Estamos sin conexión
    
    <script>
        // Este código detecta cuando volvemos a tener conexión
        // y en ese caso se carga automáticamente la página principal.
        // El usuario no necesita refrescar la página.
        window.addEventListener("online", () => (window.location.href = "/"));
    </script>
</body>
</html>
```

## Auditoría de la aplicación

Podemos realizar una auditoría de la aplicación, haciendo uso de la extensión **Lighthouse** de Chrome. Para instalar dicha extensión en el navegador chrome escribimos la URL chrome://extensions/.

Si pulsamos la tecla `F12` para mostrar las `Dev Tools` podremos ver una pestaña con el nombre `Audits`. Desde ahí realizaremos la auditoría.


![ScreenCast](screencast.gif)


> NOTA: Algunas extensiones activas en el navegador pueden ralentizar las pruebas y provocar que el *score* obtenido sea menor. Para evitar esto podemos lanzar la auditoría desde el `modo incógnito` del navegador o, una solución más drástica, desactivar las extensiones.
