---
date: 2020-05-31 12:26:40
layout: post
title: Armando unit tests en Jasmine!
description: Errores frecuentes
image: 'assets/img/karma.jpg'
category: test
tags:
  - jasmine
  - humor
  - karma
  - errors
author: sol lopez

---
# Armando unit tests en Jasmine!
## Errores frecuentes 

Hola amigos! Hoy quisiera compartir con ustedes los errores mas frecuentes que suelen suceder a medida que escribimos nuestros unit tests y sus respectivas soluciones.
Si bien la mayoria son bastante intuitivos, algunos son tipo

![enter image description here](https://i.pinimg.com/736x/d6/3e/dd/d63edd9af879f866baea5e3c5b506959.jpg)

A esos quiero apuntar esta vez y tambien menciono algunos intuitivos level "medium", quizas sirva tenerlos a mano como una especie de machete, no lo se, todavia no soy grande voy a esperar
```
Uncaught Error: Cannot find module "tslib".
    at webpackEmptyContext (VM2488 main.js:11)
```
y sigueee, el error es bastaaaneete largo pero imposible de saber exactamente de antemano cual es la falla en nuestro codigo, asi que bueno cuando nos pase esto solo nos interesa el **cannot find module bla bla**. La solucion es mas simple de lo que parece, solo debemos fijarnos en nuestros @imports del .spec en cuestión que estamos corriendo, y veamos que los imports sean lo mas *puros* posibles, que no tengan un compiler/operators/internal ni rutas extensas raras, por ejemplo:
```
import { Type } from '@angular/compiler/src/core';
``` 
Solucion:
```
import { Injectable, Type } from '@angular/core';
```
Este error por lo general sucede porque importamos automaticamente haciendo uso de nuestro IDE (VSCode <3) y bueno, el IDE encuentra similitudes y lo importa, pero no es la ruta correcta para que jasmine no explote :)

Otras veces vemos otros errores como "cannot read property bla bla of undefined" o "cannot read property subscribe of undefined".
Estos si son mas intuitivos, basicamente tenemos queeee mockear, el arte de mockear.. 

![enter image description here](/assets/img/magic.jpg)


Para el primer error, nos fijamos en nuestro ngOnInit si tenemos datos que no hayamos mockeado en el spec, si no esta ahi nos deberemos fijar en los datos que el componente puede estar recibiendo mediante @Inputs, y tambien fijarnos en el template del componente si esta tratando de renderizar N datos que todavia no mockeamos en nuestro .spec. 
Para el segundo error, es similar al anterior solo que ademas, el dato que nuestro componente esta esperando manipular/renderizar tiene que ser de tipo **Observable**, por lo que nuestro mock debe respetar eso, podemos hacer un of({mock: 'mock'}) y tenemos nuestro objeto de tipo obs al cual es posible subscribirse en el .spec.

Otro error que veo mucho es el 
```
Uncaught Error: Uncaught (in promise): Error: No value accessor for form control
```
Puede ser algo intuitivo, y nos indica que en nuestro componente tenemos un formulario, pero que el test no logra acceder al control. Por ejemplo, si tenemos un input o un select no logra encontrarlo en nuestro form, esto puede ser porque lo estamos mockeando en otra parte o bien, porque tenemos que importar el módulo si es un componente select custom.

Otro error frecuente es cuando corremos nuestro test suite por ejemplo usando fdescribe y los tests pasan, pero cuando quitamos el fdescribe y corremos todos los tests de la app empiezan a fallar, y no solo eso, sino que a veces fallan unos, y otras veces otros. Esto por lo general nos indica que tenemos errores de sincronia (async tests quizas) y problemas de dependency injection, es por eso que van mutando los errores y muchas veces nos cuesta encontrar cual es el que efectivamente necesitamos resolver. Para encontrar la solucion lo mejor usar el modo debug y revisar nuestra cadena de imports y declarations que podria ser innecesariamente extensa, haciendo que nuestros tests dependan unos de otros. Lo ideal es la **isolationnnn** asi que tratemos de evitar esto al maximo posible, solo testeemos nuestros componentes, no declaremos e importemos innecesariamente, asi vamos a lograr no solo optimizar nuestros tests sino tambien nos aseguramos de testear aisladamente cada componente. 
Para esto, podemos hacer uso del schemas: [CUSTOM_ELEMENTS_SCHEMA], que nos sirve para indicar que tenemos elementos y componentes custom en nuestro componente y no necesitamos importar cada uno. 
Evitemos el [NO_ERRORS_SCHEMA], este sólo sirve para ocultar errores e indica que podemos tener cualquier verdura en nuestros templates y el test va a pasar OK, sin resolverlos.

Por lo general cuando hacemos ng test --watch ya podemos correr con Karma por ej los tests y ver los errores. Si no es suficiente, es posible abrir los tests desde localhost:9876 por lo general y encender el modo debug. Muchas veces consologueando tambien nos damos cuenta rapidamente si el problema es meramente del componente o de un metodo que no esta siendo mockeado del todo o si ni siquiera accede al mismo etc.

By Sol López, frontend, rosarina, baterista, rock & metal.
