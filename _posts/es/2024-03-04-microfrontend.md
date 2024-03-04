---
date: 2024-03-04 11:00:00
layout: post
title: Micro Frontend
description: Micro Frontends en Angular
language: es
image: "../assets/img/microfrontend.png"
category: CODE
tags:
  - coding
  - microfrontend
  - humor
author: sol lopez
---

# Micro Frontends

Buenasss como andan? Primer post del 2024 y volvemos con magia sobre Micro Frontends en Angular! Como siempre acerco docu complementaria por [acá](https://www.angulararchitects.io/en/blog/micro-frontends-with-modern-angular-part-1-standalone-and-esbuild/)

El post de hoy va dedicado a experiencias y algunos ejemplos para empezar a implementar Micro Frontends en nuestros proyectos con esta arquitectura.

![MicroFrontend](https://solopez.github.io/assets/img/micro.png)

## Cuál es el enfoque Micro Frontend?
El enfoque de Micro Frontend es una arquitectura de desarrollo web que busca dividir una aplicación frontend en unidades más pequeñas e independientes.


## A codear!
![50 Ridiculously Funny Programming Memes that Every Developer HAS to See!](https://uploads-ssl.webflow.com/5f3c19f18169b62a0d0bf387/60d33be8cf4ba7565123c8bc_YPD3ulQQAGQpOcnqIm3QzSTRgzmr1SexpW9ZjMpJ1mAnUxx4iF05XOTu44sk0qQG-8XgBcYmGZGAD-5SAZvJl3TjtmhgWnn-w0C2XKwhBscV78RVvhwZfyp0v_Pa6sNj5zxpOvRW.png)

### Instalación
En nuestras dos aplicaciones, app proyecto (shell) y app-microfront que será consumida por el proyecto (remote), vamos a instalar module federation:
```
ng add @angular-architects/module-federation --project=remote
```

```
ng add @angular-architects/module-federation --project=shell
```
### Module y components
Creamos el module y ruteo que vamos a exponer como microfront (abc)

```
ng generate module abc --project=remote --routing
```
Creamos un component
```
ng generate component abc --project=remote
```

Ruteamos en routing module

```typescript
const routes: Routes = [
  {
    path: '',
    component: AbcComponent
  }
];
```


Cargamos el module de forma lazy:

```typescript
const routes: Routes = [
  {
    path: '',
    loadChildren: () => import('./abc/abc.module').then(m => m.AbcModule)
  }
];
```

### Webpack.config.js
Configuramos el webpack.config.js para poder exponer el módulo del Micro Frontend mediante un archivo llamado "remoteEntry.js", y los packs que son requeridos y dependientes del módulo (shared libraries), quedando así:


```typescript
const ModuleFederationPlugin = require("webpack/lib/container/ModuleFederationPlugin");
const mf = require("@angular-architects/module-federation/webpack");
const path = require("path");
const share = mf.share;

const sharedMappings = new mf.SharedMappings();
sharedMappings.register(
  path.join(__dirname, '../../tsconfig.base.json'),
  [/* mapped paths to share */]);

module.exports = {
  output: {
    uniqueName: "remote",
    publicPath: "auto"
  },
  optimization: {
    runtimeChunk: false
  },
  resolve: {
    alias: {
      ...sharedMappings.getAliases(),
    }
  },
  experiments: {
    outputModule: true
  },
  plugins: [
    new ModuleFederationPlugin({
        library: { type: "module" },

        // here you can expose your components and modules:
        name: "remote",
        filename: "remoteEntry.js",
        exposes: {
            './Module': './apps/remote/src/app/abc/abc.module.ts',
        },

        // this specifies the shared libraries so that these libraries are singelon instances -
        // meaning that every application consumes the same:
        shared: share({
          "@angular/core": { singleton: true, strictVersion: true, requiredVersion: 'auto' },
          "@angular/common": { singleton: true, strictVersion: true, requiredVersion: 'auto' },
          "@angular/common/http": { singleton: true, strictVersion: true, requiredVersion: 'auto' },
          "@angular/router": { singleton: true, strictVersion: true, requiredVersion: 'auto' },

          ...sharedMappings.getDescriptors()
        })

    }),
    sharedMappings.getPlugin()
  ],
};
```

El archivo `remoteEntry.js` se autogenera y éste va a ser necesario para dar instrucciones a las apps externas que contienen las configs de **webpackconfig.** 
Si quisiéramos accederlo, podemos desde la url [https://localhost:port/remoteEntry.js](https://localhost:port/remoteEntry.js) (siendo port el puerto que estemos usando para esa app).

## Shell
Ahora lo único que falta es el **consumo del Micro Frontend**. Hay básicamente dos formas de hacerlo: _Estática y Dinámica._
En este ejemplo vamos a ir por la dinámica, que nos da mayor flexibilidad en caso de que quisieramos cargar las configuraciones Micro Frontends de forma dinámica y desde el mas allá (backends).

Para consumir el microfront, vamos a implementar lazy loading para cargarlo, desde nuestra app (Shell), de esta manera:


```typescript
  {
    path: 'microfrontend',
    loadChildren: () => loadRemoteModule({
      remoteEntry: 'http://localhost:4400/remoteEntry.js',
      type: 'module',
      exposedModule: './Module'
    })
    .then(m => m.AbcModule)
  }
```

Ahora sí sin mas, probamos la carga del microfront desde nuestro componente

```html
<a routerLink="microfrontend">click me to load remote</a>

<router-outlet></router-outlet>
```

Nota: Es importante que primero demos start (ng serve) al microfront antes que al shell!

De esta manera estamos renderizando y consumiendo modulos que no existen en nuestra app, sino que existen y se consumen desde su propia app y proyecto.

## Conclusión

Como todo en esta vida (?? es necesario que consideremos las ventajas y desventajas que podemos obtener al enfocar nuestros proyectos con esta arquitectura.

### Ventajas:

1.  **Desarrollo Independiente:** Con Micro Frontend, diferentes equipos pueden trabajar de manera independiente en módulos o Micro Frontends específicos. Esto permite un desarrollo paralelo acelerando tiempos y evitando dependencias entre equipos y features.
    
2.  **Escalabilidad:** Al dividir la aplicación en Micro Frontends, es más fácil escalar y mantener áreas específicas de la aplicación. Se pueden asignar recursos según las necesidades de cada Micro Frontend, lo que mejora la escalabilidad de la aplicación en general.
    
3.  **Tecnologías Diversas:** Diferentes Micro Frontends pueden utilizar tecnologías frontend distintas. Esto facilita la adopción de nuevas tecnologías o la actualización de las existentes sin afectar a toda la aplicación.
    
4.  **Facilita la Colaboración:** Equipos diferentes pueden trabajar en paralelo en Micro Frontends específicos, lo que facilita la colaboración y la gestión de proyectos más grandes.
    
5.  **Mantenimiento Simplificado:** Al ser unidades independientes, el mantenimiento y la actualización de un Micro Frontend específico no afectan a otras partes de la aplicación. Esto hace que el proceso de mantenimiento sea más simple y menos propenso a errores.
    
6.  **Reusabilidad de Componentes:** Se pueden reutilizar componentes específicos en diferentes Micro Frontends, lo que contribuye a la consistencia visual y funcional en toda la aplicación.
    
7.  **Despliegue Incremental:** Se pueden implementar cambios de manera incremental y por partes, en lugar de tener que lanzar actualizaciones masivas de toda la aplicación.
    
8.  **Mejora la Experiencia del Usuario:** La carga inicial de la aplicación puede ser más rápida, ya que solo se cargan los Micro Frontends necesarios para una página específica, a demanda. Esto mejora la experiencia del usuario al reducir los tiempos de carga.
    
9.  **Aislamiento de Errores:** Los errores en un Micro Frontend no se propagan a otras partes de la aplicación, ya que están encapsulados. Esto facilita la identificación y corrección de problemas.
    
10.  **Facilita la Adopción de Tecnologías Emergentes:** Al permitir la adopción de nuevas tecnologías en módulos específicos, podes mantener tu aplicación al día con las últimas tendencias y tecnologías del desarrollo web.


### Desventajas:

1.  **Complejidad:** La gestión de la comunicación entre Micro Frontends y la sincronización de estados puede volverse compleja.
    
2.  **Coordinación Necesaria:** Se requiere una coordinación cuidadosa entre equipos para asegurar la coherencia en la interfaz de usuario y la experiencia del usuario final.
    
3.  **Overhead de Comunicación:** La comunicación entre Micro Frontends puede generar un overhead adicional, especialmente en aplicaciones grandes.
    
4.  **Curva de Aprendizaje:** La adopción de esta arquitectura puede requerir tiempo para que los equipos se adapten y comprendan la implementación.
    
5.  **Gestión de Estado Global:** Mantener un estado global coherente puede ser un desafío, ya que cada Micro Frontend tiene su propio estado.
    
6.  **Seguridad:** La seguridad debe ser gestionada cuidadosamente para evitar vulnerabilidades entre Micro Frontends.
    
7.  **Problemas de Rendimiento:** Dependiendo de la implementación, podría haber problemas de rendimiento debido a la carga de múltiples Micro Frontends en una sola página.
    
8.  **Necesidad de Herramientas Específicas:** Puede requerir herramientas y frameworks específicos para facilitar la implementación y gestión de Micro Frontends.

Es importante tener en cuenta que, si bien hay beneficios significativos, también existen desafíos asociados con la implementación de la arquitectura de Micro Frontend, como la complejidad en la gestión del estado global y la comunicación entre Micro Frontends. 
Por lo tanto, podemos decir que la elección de adoptar esta arquitectura debe basarse siempre en las necesidades específicas del proyecto y las capacidades del equipo de desarrollo.

Happy coding!



![Beer!](https://solopez.github.io/assets/img/beer-code.jpg)