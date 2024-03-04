---
date: 2024-03-04 11:00:00
layout: post
title: Micro Frontend
description: Micro Frontends en Angular
language: en
image: "../assets/img/microfrontend.png"
category: CODE
tags:
  - coding
  - microfrontend
  - humor
author: sol lopez
---

# Micro Frontends

How are you doing? First post of 2024 and we are back with magic about Micro Frontends in Angular! As always I bring complementary docu [here](https://www.angulararchitects.io/en/blog/micro-frontends-with-modern-angular-part-1-standalone-and-esbuild/)

Today's post is dedicated to experiences and some first contact examples to start implementing Micro Frontends in our projects with this architecture.

Translated with DeepL.com (free version)
![Your First Angular Microfrontend. This is a step by step guide on how to… |  by Stefan Haas | Level Up Coding](https://miro.medium.com/v2/resize:fit:1051/1*p-ArC7CbZZzg6tXe9Gsh-Q.jpeg)

## Cuál es el enfoque Micro Frontend?
El enfoque de Micro Frontend es una arquitectura de desarrollo web que busca dividir una aplicación frontend en unidades más pequeñas e independientes.


## Let's code!
![50 Ridiculously Funny Programming Memes that Every Developer HAS to See!](https://uploads-ssl.webflow.com/5f3c19f18169b62a0d0bf387/60d33be8cf4ba7565123c8bc_YPD3ulQQAGQpOcnqIm3QzSTRgzmr1SexpW9ZjMpJ1mAnUxx4iF05XOTu44sk0qQG-8XgBcYmGZGAD-5SAZvJl3TjtmhgWnn-w0C2XKwhBscV78RVvhwZfyp0v_Pa6sNj5zxpOvRW.png)
### Setup
In our two applications, app-project (shell) and app-microfront which will be consumed by the project (remote), we will install module federation:

```
ng add @angular-architects/module-federation --project=remote
```

```
ng add @angular-architects/module-federation --project=shell
```
### Module y components
We create the module and routing that we are going to expose as microfront (abc)
```
ng generate module abc --project=remote --routing
```
Creamos un component
```
ng generate component abc --project=remote
```

Routing module

```typescript
const routes: Routes = [
  {
    path: '',
    component: AbcComponent
  }
];
```
Lady loading:

```typescript
const routes: Routes = [
  {
    path: '',
    loadChildren: () => import('./abc/abc.module').then(m => m.AbcModule)
  }
];
```

### Webpack.config.js
We configure the webpack.config.js to be able to expose the Micro Frontend module through a file called "remoteEntry.js", and the packs that are required and dependent of the module (shared libraries), being like this:


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

The `remoteEntry.js` file is auto generated and it will be needed to give instructions to the external apps that contain the **webpackconfig.** configs. 
If we want to access it, we can access it from the url [https://localhost:port/remoteEntry.js](https://localhost:port/remoteEntry.js) (port being the port we are using for that app).

## Shell
Now the only thing missing is the Micro Frontend **consumption**. There are basically two ways to do this: _Static and Dynamic.
In this example we are going to go for the dynamic one, which gives us more flexibility in case we want to load the Micro Frontends configurations dynamically and from the backends.

To consume the microfrontend, we are going to implement lazy loading to load it, from our app (Shell), in this way:

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

Now, we test the loading of the microfront from our component

```html
<a routerLink="microfrontend">click me to load remote</a>

<router-outlet></router-outlet>
```

Note: It is important that we first start (ng serve) the microfront before the shell!

This way we are rendering and consuming modules that do not exist in our app, but exist and are consumed from their own app and project.

## Conclusion

As everything in this life (???) it is necessary that we consider the advantages and disadvantages that we can obtain when approaching our projects with this architecture.

### Advantages:

1.  **Independent Development:** With Micro Frontend, different teams can work independently on specific modules or Micro Frontends. This allows a parallel development accelerating times and avoiding dependencies between teams and features.
    
2.  **Scalability:** By dividing the application into Micro Frontends, it is easier to scale and maintain specific areas of the application. Resources can be allocated according to the needs of each Micro Frontend, which improves the scalability of the application in general.
    
3.  **Diverse Technologies:** Different Micro Frontends can use different frontend technologies. This facilitates the adoption of new technologies or the upgrade of existing ones without affecting the entire application.
    
4.  **Facilitates Collaboration:** Different teams can work in parallel on specific Micro Frontends, which facilitates collaboration and management of larger projects.
    
5.  **Simplified Maintenance:** Being independent units, the maintenance and upgrade of a specific Micro Frontend does not affect other parts of the application. This makes the maintenance process simpler and less error prone.
    
6.  **Component Reusability:** Specific components can be reused in different Micro Frontends, contributing to visual and functional consistency throughout the application.
    
7.  **Incremental Deployment:** Changes can be implemented incrementally and piecemeal, instead of having to release massive updates of the entire application.
    
8.  **Improved User Experience:** The initial loading of the application can be faster, as only the Micro Frontends needed for a specific page are loaded on demand. This improves the user experience by reducing load times.
    
9.  **Error Isolation:** Errors in a Micro Frontend do not propagate to other parts of the application, as they are encapsulated. This makes it easier to identify and correct problems.
    
10.  **Facilitates the Adoption of Emerging Technologies:** By allowing the adoption of new technologies in specific modules, you can keep your application up to date with the latest trends and technologies in web development.


### Disadvantages:

1.  **Complexity:** Managing communication between Micro Frontends and state synchronization can become complex.
    
2.  **Coordination Required:** Careful coordination between teams is required to ensure consistency in the user interface and end-user experience.
    
3.  **Communication Overhead:** Communication between Micro Frontends can generate additional overhead, especially in large applications.
    
4.  **Learning curve:** Adoption of this architecture may require time for teams to adapt and understand the implementation.
    
5.  **Global State Management:** Maintaining a consistent global state can be a challenge, as each Micro Frontend has its own state.
    
6.  **Security:** Security must be carefully managed to avoid vulnerabilities between Micro Frontends.
    
7.  **Performance Issues:** Depending on the implementation, there could be performance issues due to loading multiple Micro Frontends on a single page.
    
8.  **Need for Specific Tools:** May require specific tools and frameworks to facilitate the implementation and management of Micro Frontends.

It is important to note that while there are significant benefits, there are also challenges associated with implementing the Micro Frontend architecture, such as the complexity in managing the overall state and communication between Micro Frontends. 
Therefore, we can say that the choice to adopt this architecture should always be based on the specific needs of the project and the capabilities of the development team.

Happy coding!



![Beer!](https://solopez.github.io/assets/img/beer-code.jpg)