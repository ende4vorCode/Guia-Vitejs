# VITE.js

- Nota: Antes de revisar esto, es necesario que tengas ciertos conocimientos previos sobre desarrollo web, aunque la guía esta hecha para ser entendida sencillamente.

## Que es VITE.js

- Vite es una herramienta para encapsular todas las otras herramientas que utilizamos hoy en dia en el desarrollo de software standard. Lo cual nos permite tener una mejor experiencia de desarrollo, mas rápida y fácil.
- Como su característica principal es la velocidad, no importa cuanto crezca el proyecto, siempre sera muy rápido.

### Características de VITE.js

- Pre-bundling: Agrega compatibilidad adaptando módulos en CommonJs o UMD al formato estándar de ECMAScript(ES Modules).
- Dependency Resolving: Ayuda a optimizar el "como" se obtienen las librerías o módulos ya estandarizados.
  - Genera un servidor de archivos estáticos a traves de URL.
  - Reemplaza los imports via NodeJs por imports de URL.
  - Sirve los archivos de forma inteligente y con cache, para optimizar tiempo y procesamiento.
- Hot Module Replacement: Al hacer cambios en el código puedes verlos reflejados inmediatamente en el navegador, sin perder el estado de carga del navegador.
- Integración simple con Typescript.
- Integración con frameworks.
- Soporte para JSX.
- Importación de archivos simplificada, no requiere configuración excesiva.
- Build optimization.
- Soporte a Web Workers y Web Assembly.

## Como iniciar un proyecto con VITE.js?

- La documentación de [VITE.js](https://vitejs.dev/)
- `sudo su` Entramos en modo super usuario.
- `apt update && apt upgrade` Actualizamos los paquetes.
- `apt install nodejs npm` Instalamos Nodejs y NPM. Puedes ver mi guía de [NPM](https://github.com/ende4vorCode/Guia-NPM/blob/master/README.md).
- Debes estar dentro de la carpeta de tu proyecto.
- `npm create vite@latest` Iniciamos el proyecto de vite con NPM.
- Posteriormente nos mostrara una serie de opciones, como Nombre del proyecto, tipo de proyecto y el lenguaje (Javascript o Typescript) Todo eso lo configuras de acuerdo a tus necesidades.
- Ahora podemos entrara a la carpeta que creamos `cd proyecto`
- `npm install` Instalamos los paquetes ya predefinidos. [Mas Info](https://github.com/ende4vorCode/Guia-NPM/blob/master/README.md).
- `npm run dev` Levantamos el servidor de desarrollo de NPM. No te voy a mentir, lo rápido que es esto, es absurdo.

## Que instalamos? Boilerplate

- Index.html -> Nos crea nuestro punto de entrada de la web con una configuración sencilla.
- Favicon -> Nos crea el favicon del proyecto.
- Style.css -> Estilos del Hola Mundo del template.
- Main.js -> Archivo de javascript. La estructura cambiara de acuerdo al tipo de proyecto.
- Package.json
- Package-lock.json
- Vite.config.js -> Configuraciones de Vite.

## Importar Css

- `import './style.css'` En el Javascript podemos importar esto sin la necesidad de configurar todo.
- `@import './style.css'` En el CSS también podemos importar sin la necesidad de configurar.
- En caso que los archivos css sea pequeño vite juntara todos en uno, de lo contrario los interpretara como varios.

### Pre-Procesadores Css

- Creamos un archivo y vite lo interpretara inmediatamente.
- `ejemplo.sass` Y lo detectara automáticamente.
- `@import ./ejemplo.sass` Importamos el archivo.

### Css modules

- `element.module.css` Creamos un modulo css para un elemento de html.
- `import style from './style/element.module.css'` Importamos el elemento.
- Por ejemplo:

```javascript
import "import ./styles.css";
import elementStyle from "./styles/element.module.css";

document.querySelector("#app").innerHTML = `
        <button id='btn'>Click me</button>
    `;
document.getElementById("btn").className = elementStyle.class;
//Al id btn le asignamos la clase elementStyle y a esa clase se le agrega el estilo de css que le hayamos creado.
```

## Archivos estáticos

- `import img form './img/archivo.jpg'` Importamos la imagen a javascript. Esto es valido para otros archivos estáticos.
- Importar Json:

```json
    "user" : {
        "hero-id" : 1,
        "name" : "Ende4vor"
    },
    "status" : true
```

```javascript
import data from "hero.json"; //Traerá todos los datos desde el archivo json. Forma tradicional.
import { user } from "hero.json"; //Traerá solo los datos de user.
<pre>${JSON.stringify(user)}</pre>;
```

- Como se ve Vite nos permite importar datos desde un json según se lo pidamos, evitando asi mismo traer toda la data del archivo JSON. Lo cual ayuda radicalmente a optimizar el código, sobre todo en producción.

## Importación global

- Podemos importar módulos desde distintas zonas del proyecto.
- Para poder importar archivos globales, lo hacemos con el siguiente código:

```javascript
import.meta.glob("./ruta/moduloGlobal.js"); // Importamos un archivo especifico
import.meta.glob("./ruta/*.js"); // Importamos todos los archivos de extension .js
```

## Typescript

- Podemos importar typescript son problemas.
  `import tscript from './tscript.ts'`
- Si quieres crear un archivo de configuración puedes hacerlo sin problemas.
- Creamos un archivo de config. Ejemplo.`tsconfig.json`

```json
{
  "compilerOptions": {
    "target": "es2015" // Hacer que typescript sea compatible con Es2015
  }
}
```

# Vite config

- Creamos un archivo de configuración de vite `vite.config.js` [mas info](https://vitejs.dev/config/#config-file-resolving)

```js
export default {
  // Javascript
  server: {
    port: 3001, // Cambiamos el puerto
  },
};
```

```javascript
import { defineConfig } from "vite"; // Configuración mediante defineConfig

export default defineConfig({
  server: {
    port: 3001, // Cambiamos el puerto
  },
});
```

```javascript
    import { defineConfig } from 'vite'

    export defineConfig ( () => { // Configuraciones mediante funciones
        const port = 3001

        return {
            server: {
                port
            }
        }
    })
```

## Build para producción

- Ya en producción, hay que preocuparse de que el proyecto este optimizado.
- Variables de entorno: Son variables del sistema operativo o un archivo .env, que al ejecutarse se leen y se ejecutan, pero separado del código.
- Como se hace con vite?
  - Modo producción:
    `vite.config.js` Mismo archivo anterior, pero con unas modificaciones

```javascript
   import { defineConfig } from 'vite'

    export defineConfig ( ({ command, mode }) => { //Le entregamos 2 parámetros a la función para que detecte si esta en modo desarrollo o modo producción
    // Como esta en una función, podemos tomar decisiones

    if (mode === "development") { //Ejemplo básico de una decision
        const port = 3001
        console.log("Server is running in development mode")
    } else {
        const port = 3000
        console.log("Server is running in production mode")
    }

    return {
        server: {
            port
        }}})
```

- Variables de entorno por defecto `.env`
- Variables de entorno para desarrollo `.env.development`
- Variables de entorno para producción `.env.production`
- Como en el archivo `.env` suelen existir datos sensibles, para que se puedan ver se deben escribir de la siguiente forma -> `VITE_NAME="vite example"` entonces podemos llamar al archivo env en nuestro config.

```javascript
   import { defineConfig, loadEnv } from 'vite' //Ahora agregamos el archivo .env
    export defineConfig ( ({ command, mode }) => {
    const env = loadEnv(mode, process.cwd()) // Al existir posibles distintos tipos del .env, es posible darle mas de un argumento. En este caso mode y process.cwd(Donde esta el archivo)\

    console.log(env.VITE_NAME)//Muestra por pantalla vite example -> Que es el valor que escribimos dentro de .env
    if (mode === "development") {
        const port = 3001
        console.log("Server is running in development mode")
    } else {
        const port = 3000
        console.log("Server is running in production mode")
    }

    return {
        server: {
            port
        }
```

## Sitios multi-pagina

- Puedes hacer que la pagina se inicie desde distintos sectores.(No solo del index.html)
- Dentro del `vite.config.js` Configuramos lo siguiente:

```js
    import { defineConfig, loadEnv } from 'vite'
    import { resolve } from 'path' //Importamos la función para buscar carpetas con NODEJS
    export defineConfig ( ({ command, mode }) => {
    const env = loadEnv(mode, process.cwd())

    console.log(env.VITE_NAME)
    if (mode === "development") {
      let port = 3001
      console.log("Server is running in development mode")
      return {
        server: {
          port
        }
      }
    } else {
      let port = 3000
      console.log("Server is running in production mode")
      return { //Modificamos la configuración de Rollup a traves de build, para que exista mas de un punto de entrada en el sitio
        build : {
          rollupOptions: {
            input: {
              main: resolve(__dirname, 'index.html') //Inicio principal de la web,
              other: resolve(__dirname, './otherThings/other.html') //Otra zona de entrada
            }
          }
        }
      }
    }}})
```

- Posteriormente por url encontramos el archivo en `ip:port/otherThings/other.html` (ip:port se refiere a donde se monta el sitio) Esta característica de vite se conoce como "micro frontend"

## Construir librerías

- Creamos una carpeta `lib` dentro tendrá un archivo `main.js`
- Dentro puede tener

```javascript
console.log("Hola soy una biblioteca");
```

- En nuestro archivo de configuración haremos la siguiente modificación.

```javascript
  //Donde se encontraba rollup lo reemplazaremos por lib
    build : {
      lib : {
        entry: resolve(__dirname, 'lib', 'main.js')// Carpeta, archivo
        name: 'example',//Nombre de la librería
        fileName: (format) => `demo.${format}.js`
      }
    }
```

# Soporte Frameworks

- Vite soporta gran variedad de frameworks, incluidos React y Vue(Vue es la empresa que creo Vite, por ello es como si estuviera en casa)

[Ende4vor](https://github.com/ende4vorCode)
