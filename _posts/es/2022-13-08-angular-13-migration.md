---
date: 2022-07-13 15:00:40
layout: post
title: Angular 13!
description: Migración a Angular 13!
language: es
image: '../assets/img/angular13.png'
category: CODE
tags:
  - coding
  - migration
  - humor
author: sol lopez
---

# Migración Angular 13

Buenasss como andan? Volvemos con nueva migra de angular!!!

El post de hoy va dedicado a las experiencias durante una migración específica desde nuestro previo Angular 12 hacia Angular 13, con novedades, tips, errores, warnings y sus respectivos fixes para renovarnos y sacarlo con fritas!

![enter image description here](https://media.makeameme.org/created/Needs-to-upgrade.jpg)

## Guía
Para empezar vamos a la guía oficial [aquí](https://update.angular.io/?l=3&v=12.0-13.0). En este caso, viniendo de la versión 12, no necesitamos aplicar cambios en nuestro código ANTES de ejecutar el comando para poder migrar. Por lo tanto, podemos arrancar:

    ng update @angular/core@13 @angular/cli@13

Nota: agregar el --force si es necesario! Hasta ahora en cada migra parece que lo pide a gritos!
![enter image description here](https://media.makeameme.org/created/the-force-is-3cdf009ad5.jpg)

La mayoría de cambios requeridos los aplicamos con el comando. 
El resto de posibles cambios que tengas que hacer, dependerán como siempre del proyecto en el que estés trabajando y esta guía es para esos cambios manuales, allá vamos!
También vas a ver diferencias en cuanto a si estás trabajando en una app, o en una librería publicable por el tipo de compilación, que vamos a ver más adelante.

### ModuleWithProviders migration
Si tenés modulos con providers implementando ModuleWithProviders, puede que el schematic no pueda determinar el type, por lo cual es necesario migrar aquellos que requieran el type así:

    @NgModule({…})
    export class MyModule {
      static forRoot(config: SomeConfig): ModuleWithProviders<SomeModule> {
	    return {
	      ngModule: SomeModule,
	      providers: [
	        {provide: SomeConfig, useValue: config }
	      ]
	    };
      }
    }

Más detalles e info [acá](https://angular.io/guide/migration-module-with-providers)!

### Rxjs
![enter image description here](https://miro.medium.com/max/1400/1*ZUENlsi796hIv9TNeqJ3bA.png)
Si estabas usando RxJS v6.x, hay que instalar manualmente la 7.4: 

    npm install rxjs@7.4
Para proyectos y apps fresh en esta versión de Angular, instalarán por defecto el rxjs 7.4. 
Qué hay de nuevo en Rxjs [acá](https://rxjs.dev/6-to-7-change-summary)!

Por supuesto esto no termina acá, hay algunos breaking changes y algunas deprecaciones que pueden impactar en tu proyecto, suelen resolverse en poco tiempo. 
Ejemplo :

    RxJS 7 allow to call 'next' without parameters (Typescript checks).
    
Si estás haciendo un next en un Subject sin params así:

    const updateSubject = new Subject();
    updateSubject.next();

se puede resolver agregando el type <void> en la declaración de ese Subject:

    private subject$ = new Subject<void>();
Más info [acá](https://github.com/ReactiveX/rxjs/issues/6324)!

### Compilermode

### Angular library 
![enter image description here](https://miro.medium.com/max/1000/1*rCgtilQLYXaua4FH4vxROg.png)
Si estás trabajando en una library publicable npm, podes encontrar este error:

    Unsupported private class

> This class is visible to consumers via SomeModule -> SomeComponent,
> but is not exported from the top-level library entrypoint

Para resolverlo, tendrás que buscar los componentes y módulos que no están debidamente exportados en la public_api.ts.

Esto puede pasar porque con Ivy, es un requerimiento si queremos exportar un modulo desde una library endpoint, debemos re-exportar manualmente todos los elementos involucrados también (componentes, pipes, directivas, todooo!).
Antes con View Engine, esto era automático. Pero con Ivy debemos explícitamente hacerlo, recordemos que Ivy llegó para quedarse y View Engine en esta versión ya queda oficialmente deprecado.
Más info de estos errores [acá](https://stackoverflow.com/questions/60121962/this-class-is-visible-to-consumers-via-somemodule-somecomponent-but-is-not-e)!
Info oficial sobre Angular libraries [acá](https://angular.io/guide/creating-libraries)!

#### Error para Angular library: NG3003: Import cycles would need to be created to compile this component
O también conocido como

    One or more import cycles would need to be created to compile this component, which is not supported by the current compiler configuration.
    is used in the template but importing it would create a cycle

Si te topaste con este error cíclico, sólo se da en **angular library**, si no estás trabajando en una library publicable, safaste y te ganaste el pase directo a la próxima sección, fuera! 
Este error podría significar un cambio de complejidad baja/media según el caso, ya que deberemos tener en cuenta si se trata de un tema de imports con dependencias circulares (complejidad baja) o si necesitamos aplicar refactor (complejidad media no tan barata). 
Por ejemplo en un caso donde ante ciertas situaciones, componente A embebe a componente B, y donde componente B puede embeber a componente A. 
Lo más probable es que tengamos que refactorizar si tenemos este último caso.
La explicación del error y posibles sugerencias para fixearlo desde Angular oficial [acá](https://angular.io/errors/NG3003)!

Esto ocurre por el tipo de compilación, pudiendo ser "partial" o "full" en nuestra   
**tsconfig.lib.prod.json.**
Estando en una library, debemos usar "partial" ya que necesitamos la retrocompatibilidad de los consumidores con o sin Ivy.
En una app (no library), el tipo de compilación será "full" y no verás este hermoso error jamás.
Ahora, qué pasaría si estamos trabajando en una Angular library, y manualmente modificamos a modo compilación "full"? Engañamos al npm publish sí o no?

![enter image description here](https://i.imgflip.com/6mp8ce.jpg)

    ERROR: Trying to publish a package that has been compiled by Ivy in full compilation mode. This is not allowed.
    Please delete and rebuild the package with Ivy partial compilation mode, before attempting to publish.	

La build te va a decir si si dale y cuando corras el `npm publish` te da la bienvenida con ese error de arriba... asi que no, ni lo intentes, compila en "partial" y no pierdas tiempo valioso en esto.

![enter image description here](data:image/png;base64,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)

Salvo que quieras super investigar estos tipos de compilación y los por qué, te dejo este [artículo](https://blog.lacolaco.net/2021/02/angular-ivy-library-compilation-design-in-depth-en/) que esta buenísimo, con gráficos y todo más que claro.

### Errores/Warnings
Por lo general y en cada nueva versión de Angular, los errores y/o warnings cada vez son más restrictivos en varios puntos pero también son cada vez más descriptivos, por lo que podrían resolverse desde las mismas sugerencias que ellos nos ofrecen. Es por eso, que preferí enfocar este post a los errores que no son tan fáciles de resolver y también a aquellos que nos lleva más tiempo de análisis e investigación para su resolución. 
Recordá siempre correr y compilar el build de production para exterminar los errores que queden pendientes.

## Storybook
![enter image description here](https://pbs.twimg.com/tweet_video_thumb/FFiP-v7WYAQW2cP.jpg)

Si en tu proyecto estás usando Storybook, hay una gran migra también con varios ajustes manuales para mantener Storybook actualizado. Lo más importante en esta versión: Habemus compilador de Angular para storybook, asi que desde nuestro angular.json lo vamos a dejar configurado.
Como siempre sugiero la guía oficial de migración de Storybook:

 - Para migrar de 6.3.x a 6.4.x [acá](https://github.com/storybookjs/storybook/blob/next/MIGRATION.md#from-version-63x-to-640)
 - Para configurar los angular builder y otros cambios de angular 13 [acá](https://github.com/storybookjs/storybook/blob/next/MIGRATION.md#sb-angular-builder)

Otra cuestión que me pasó, fue uno de los problemas en la compilación de storybook, de este estilo:

    preview.ts is missing from the TypeScript compilation. Please make sure it is in your tsconfig via the 'files' or 'include' property.

Por lo cual tuve que aplicar cambios en el `.storybook/tsconfig.json` para los includes, como [acá](https://github.com/storybookjs/storybook/issues/17039)!

Y si te surge este caso: `can only be default-imported using the'allowSyntheticDefaultImports' flag`

Podes resolverlo agregando esa flag en el tsconfig del proyecto raíz (no storybook como el anterior):

    "allowSyntheticDefaultImports": true,
	
Si los problemas de compilation persisten y vemos esto:
        ```
    UnhandledPromiseRejectionWarning: TypeError: The 'compilation' argument must be an instance of Compilation
    ```

podés revisar de no tener prendido el sourceMap para debugging, en  el angular.json debería quedar así:

    "sourceMap": false,

Más info [acá](https://github.com/storybookjs/storybook/discussions/17232)!

Si aún vemos este maldito:

    UnhandledPromiseRejectionWarning: TypeError: The 'compilation' argument must be an instance of Compilation
Vamos a tener que revisar y verificar las versiones de webpack de angular y webpack de storybook, para eso seguimos estos pasos:

    1.  `npm ls webpack`
    2.  Buscamos la version de webpack para `@angular-devkit/build-angular`
    3.  `npm install`  la version exacta en dev dependencies
    4.  `npm dedupe` // WTF? si, esto intenta simplificar el arbol de dependencias de los paquetes cambiando su estructura y también elimina duplicados

Más info de este error y los pasos que vimos arriba [acá](https://github.com/storybookjs/storybook/issues/16977)!

## Jest
![enter image description here](https://i.ytimg.com/vi/2Y_symiajsc/maxresdefault.jpg)

Si te animaste a decirle adiós a Jasmine y Karma, y empezaste a indagar en el mágico mundo de Jest, ahí van los ajustes necesarios para esta versión!

![enter image description here](https://www.meme-arsenal.com/memes/1622805b4aa6884f82677b8d3ea81568.jpg)

Para empezar, en mi experiencia migré todo jest a estas nuevas versiones:

    "@types/jest": "27.4.1",
    "jest": "^27.4.7",
    "jest-preset-angular": "^11.0.1",
    "ts-jest": "^27.1.2",

Para migrar y actualizar nuestro jest.config.js por comando npm ejecutamos: 

    npx ts-jest config:migrate jest.config.js
Otras formas de ejecutarlo [acá](https://kulshekhar.github.io/ts-jest/docs/migration/):

En mi experiencia tuve este error:
`Need to call TestBed.initTestEnvironment() first`

y este otro:

    Zone is needed for the waitForAsync() test helper but could not be found. Please make sure that your environment includes zone.js

A ambos los resolví fixeando el **test.ts** (donde importamos el jest-preset-angular) así:

```javascript
import  'jest-preset-angular';
import  'zone.js';
import  'zone.js/testing';
import { TestBed } from "@angular/core/testing";
import { BrowserDynamicTestingModule, platformBrowserDynamicTesting } from "@angular/platform-browser-dynamic/testing";

TestBed.initTestEnvironment(BrowserDynamicTestingModule, platformBrowserDynamicTesting());
```
Más info de ese error [acá](https://stackoverflow.com/questions/65397145/error-need-to-call-testbed-inittestenvironment-first)!

Algunos cambios únicamente podrían afectarte según la versión de Jest y de jest-preset-angular que estés usando actualmente, por las dudas podés chequearlos [acá](https://thymikee.github.io/jest-preset-angular/docs/guides/angular-13+/).

Si encontrás este otro error:

    [Package subpath './src/ngtsc/reflection' is not defined by "exports" in /node_modules/@angular/compiler-cli/package.json](https://stackoverflow.com/questions/70306517/package-subpath-src-ngtsc-reflection-is-not-defined-by-exports-in-node-mo)

Podrías revisar si las versiones de jest necesitan otro cambio como indican [acá](https://stackoverflow.com/questions/70306517/package-subpath-src-ngtsc-reflection-is-not-defined-by-exports-in-node-mo).


## Ventajas y cambios en esta versión
![enter image description here](https://res.cloudinary.com/practicaldev/image/fetch/s--qTBd8CiH--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3dtliaqu22w3ryjyomkb.jpg)
Desde el [blog oficial](https://blog.angular.io/angular-v13-is-now-available-cce66f7bc296) tenemos toooda la data de los cambios que llegan con Angular 13, así que destaco y ultra resumo algunos puntos muy interesantes:

 - Ivy everywhere, se depreca View Engine.
 - Component API updates: para crear componentes dinámicos, se redujo el boilerplate y se depreca el component factory resolver que usábamos, logrando que sólo usemos el viewContainerRef y el createComponent para tal fin!
 - End of IE11 support: hermosa noticia aunque también podemos decir algo melancólica para algunos, unas últimas palabras: somos varios quienes todavía seguramente recordamos cuando dábamos soporte a los antiguos IE con esos condicionales y no se cuantos hacks en CSS para lograr que se visualice apenitas parecido a lo que queríamos, no era mucho pedir, pero les aseguro que era más difícil que un boss de Cuphead.
 ![enter image description here](https://i.pinimg.com/736x/8b/d7/5c/8bd75c41f1c446bb7139041bb31cc6f3.jpg)
 - Improvements to the Angular CLI: cache build por defecto!
 - RxJS: ahora en las nuevas apps con Angular 13, la versión 7.4 de RxJS va a instalarse por defecto, para la migra manualmente se debe instalar `npm install rxjs@7.4`
 - TypeScript 4.4: Cambios [acá](https://devblogs.microsoft.com/typescript/announcing-typescript-4-4/) y breaking changes [acá](https://devblogs.microsoft.com/typescript/announcing-typescript-4-4/#breaking-changes)!
 - Mejoras en Angular tests: usando Jasmine, ahora mejoraron y se hace una limpieza del DOM en cada test, optimizándolos:
 
	`teardown: {  destroyAfterEach: true  }`
   

 - Temas de accesibilidad: si usas Angular Material, hay varias mejoras de accesibilidad! Todos los detalles [acá](https://blog.angular.io/improving-angular-components-accessibility-89b8ae904952)
 - Inline Fonts: Desde Angular 11 se le dio soporte inline a Google Fonts. En esta versión 13, extienden el soporte a Adobe Fonts.
 - Cambios y contribuciones de la comunidad: entre ellos cambios para activar/desactivar validators en dynamic forms, y la restauración del history del browser en el RouterModule mediante `  {  canceledNavigationResolution: 'computed'  },`
 
Espero les haya servido, happy coding!!!
![enter image description here](https://images-na.ssl-images-amazon.com/images/I/517S+mNAxOL.jpg)
  
