---
date: 2021-09-15 15:00:40
layout: post
title: Angular 11!
description: Migración a Angular 11!
image: "../assets/img/angular11.png"
category: CODE
language: es
tags:
  - coding
  - migration
  - humor
author: sol lopez
---

# Migración a Angular 11

Buenasss como andan? Recientemente tuve que hacer algunas migraciones de Angular, por lo que me pareció podría ser útil e interesante para quienes deban llevar a cabo migraciones.
Ahi les van los posibles errores y sus soluciones
![enter image description here](https://www.memecreator.org/static/images/memes/5203791.jpg)
Angular se actualiza con cierta frecuencia [ver roadmap](https://angular.io/guide/roadmap) y para no perder ritmo, debemos actualizar nuestro código en cada versión.
El post de hoy va dedicado a una migración específica de Angular 10 hacia Angular 11.

## Guía

Como guía podemos usar la oficial [aquí](https://update.angular.io/?l=3&v=10.2-11.0).
En este caso en particular, no se requiere ninguna preparación previa del código para poder migrar. Por lo que podemos arrancar desde nuestro repo con el comando de migración
```typescript
    ng update @angular/core@11 @angular/cli@11
```
## PostCSS

Si al momento de buildear (ng build --prod), te encontrás con el siguiente error:
```typescript
> [object Object] is not a PostCSS plugin
```
Podés solucionarlo instalando manualmente el paquete que importa los archivos CSS:
```typescript
    npm i postcss -D
```
Más info del issue [aquí](https://github.com/postcss/autoprefixer/issues/1358).

## allowedNonPeerDependencies

Si en tu repo tenés referencias de **whitelistedNonPeerDependencies**, quedaron deprecadas y debés modificarlas por -> **allowedNonPeerDependencies**

## Karma

Si estás usando Karma como test runner en tu proyecto, podrías necesitar modificar la configuración, ya que se deprecó el paquete **coverage-istanbul-reporter**.

Cambiamos de package:
```typescript
    npm uninstall karma-coverage-istanbul-report
    npm install karma karma-coverage
```
Y en **karma.conf.js** lo siguiente:

Cambiamos el

`require('karma-coverage-istanbul-report')`
por ->
`require('karma-coverage')`;

`coverageIstanbulReporter` por -> `coverageReporter`
Y el parámetro `reports`por -> `reporters`

Referencia de estos cambios [aquí](https://mrjean.be/posts/update-karma-coverage-reporting-for-use-in-angular-11/).

## Tests

Y siiiii, si venis migrando desde hace un tiempo habras notado que casi siempre hay que arreglar tests :D
Esta vez no es la excepción PEEEERO tampoco hay que modificar tanto, si tenes algo de suerte... Un poco mas de restricciones en cuanto a tipados y sale con
![enter image description here](https://cdn.recetas360.com/wp-content/uploads/2019/07/como-hacer-papas-fritas-de-mcdonals.jpg)

## Core-js

Si al momento de buildear (ng build --prod), te encontrás con este otro error:

> Module not found: Error: Can't resolve 'core-js/es6/reflect' in
> 'C:\Users\User\Desktop\repos\core\src' resolve 'core-js/es6/reflect

Podes fijarte en el polyfills de angular, y los imports que tengas en tu proyecto, para pasar de estos:

`import 'core-js/es6/array';`
`import 'core-js/es7/array';`

a estos:
`import 'core-js/es/array';`

Nota: modificamos sólo la primer parte (core-js/es)

Si el error persiste, puede que tengas que modificar la versión del paquete de core-js. En mi caso actualicé de la versión 2.6.12 a la 3.6.5.

## Typescript

Si te encontrás con error de versionado del TS, deberías actualizarlo también. En mi caso, actualicé del 3.9.9 al 4.1.5.
```typescript
    npm i -D typescript@4.1.5
```
## Bonus!

Si por casualidad tenias como dependencia el paquete **@angular-devkit/build-ng-packagr**, también se deprecó y sólo necesitarías este: **@angular-devkit/build-angular**, asi que podrias desinstalarlo y quitarlo del package.json, manteniendo únicamente el _@angular-devkit/build-angular._
[Paquete deprecado aca](https://www.npmjs.com/package/@angular-devkit/build-ng-packagr)

Post cortito y al pie, pero que espero pueda serles de utilidad!

![enter image description here](https://pics.me.me/thumb_adios-memecrunch-com-adi%C3%B3s-51915832.png)
