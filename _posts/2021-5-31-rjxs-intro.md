---
date: 2021-05-31 15:00:40
layout: post
title: RxJS!
description: Intro!
image: 'assets/img/rxjs_pic.png'
category: CODE
tags:
  - coding
  - rxjs
  - humor
author: sol lopez
---
# RxJS
Buenasss como andann?? En el post de hoy quiero que empecemos a ver y compartir conceptos a full sobre esta librería. 

Creo que este post será el primero de algunos mas seguramente.. y si! RxJS es digno y merecedor de un buen espacio, ya que creo es un tema que mas de una vez nos ha dado ganas de llorar. ![enter image description here](https://external-preview.redd.it/N_bB0Oszfuks9wLTax6viC4Hh9FzHgpMcpYiuUHoQQU.jpg?auto=webp&s=22d6a707521ffee7ea809ec405a10477ee7bd2b8)
![enter image description here](https://pics.me.me/programming-javascript-lie-down-try-not-to-cry-cry-a-38119635.png)

Bueno y si, eran necesarios los 2 memes, sufrimos mucho!
En fin, te lo explico en criollo, algo asi como una version de "[te lo resumo asi nomas](https://www.youtube.com/channel/UCw7Bz6EHxlnOoBUBlJZCWCw)" pero para codear? Y... ojala que si, seguire insistiendo en posts super cortos que den ganas de leer. 
La guía oficial de RxJS [aquí](https://www.learnrxjs.io/).
Bueno ahi vamos!

## Que és?
![enter image description here](data:image/jpeg;base64,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)
Es una librería de programacion reactiva para JS, en criollo, todo lo que hemos hecho desde siempre para trabajar con asincronía (datos futuros, que aun no existen) ha sido un quilombo barbaro para manejar en nuestras apps (promises y entre otros manejes), y esto vendria para salvarnos. Asi que no importa en que framework estas desarrollando no hay excusasssss! No te voy a mentir, hay mucho material dando vueltas y es justamente por esta locurita que provoca. Asi que vamos a tratar de ganar la batalla.

## Introducción

Imaginemos que tenemos mucha info que debemos procesar y mostrar en nuestra app, una colección (un array ponele), lo procesamos un poquito para mostrarlo en algun HTML y listo. Si estamos hablando de algo síncrono, onda algo asi en nuestro codigo del front: 

    const array = [
	    {name: 'sol', lastName: 'lopez'}, 
	    {name: 'dario', lastName: 'barassi'}
    ]

 
no tenemos problemas, porque tenemos esta coleccion estatica y siempre disponible en nuestra app para tener un h1 con el nombre del mejor
![enter image description here](https://fotos.perfil.com/2021/04/21/cropped/1200/1200/center/dario-barassi-2104-1161980.jpg)

AHORA el tema es cuando hablamos de asincronía, y es cuando, por ejemplo, hacemos uso de algun servicio externo que nos tiene que traer info y nosotros tenemos que esperar esa info para procesarla y mostrarla en algun lado de nuestra app.

Eso es justamente el trabajo que viene a resolver nuestro amiguito RxJS. De hecho, si queremos darle cierta forma a nuestro sync o array estatico que hariamos? usariamos algun operador (del mismisimo Array.prototype) algun map, filter, reduce bla bla....... 

BUENO, exactamente eso tambien viene a resolver esta lib. Vamos a poder usar muchisimos operadores, incluso map, filter, reduce para estos arrays asíncronos/arrays futuros que todavia no existen.

A ese flujo de datos y colecciones futuras le llamamos streaming, como si fuera Netflix, van a ir llegando datos en diferentes momentos y a distintos ritmos, de hecho hasta vamos a desconocer la cantidad de ellos y nuestra app deberá saber como gestionar y manejar esos datos cuando arriben a nuestra app. Y de hecho, esta manera de representar esos streamings es mediante canicas (marble). Pero tranqui, eso lo vamos a ver despues.

Para instalar la lib es super facil, los pasos [aquí](https://rxjs.dev/guide/installation)

## Observable
Ahora bien, con esta mini intro en mente, tenemos que empezar a hablar de observables y otros conceptos relacionados, para entender como nos vamos a manejar con estos datos futuros asíncronos.

El observable entonces representa la idea de una coleccion de datos/valores/eventos futuros como quieras llamarle, que puede ser invocada. 

Como toda funcion, por si sola no hace nada si no la invocas, asi que si no te **suscribís** al observable, nada pasará!

Vos tambien podes CREAR observables, es decir, "datos futuros" para procesarlos y manipularlos.
Si seguimos el ejemplo anterior, teniendo un array con nombres y apellidos, si usamos el operador **from** o el operador **of** creamos nuestro observable y luego nos subscribimos para ver nuestros datos:

    import { from } from  'rxjs';
    
    import { of } from  'rxjs';
             
    const  observable = from([{name:  'sol', lastName:  'lopez'}, {name:  'dario', lastName:  'barassi'}]);      
    
    const  subscribe = observable.subscribe(val  =>  console.log(val));        
    
    const  observable2 = of([{name:  'sol', lastName:  'lopez'}, {name:  'dario', lastName:  'barassi'}]);       
    
    const  subscribe2 = observable.subscribe(val  =>  console.log(val));

Ya con eso estariamos usando nuestros primeros operadores que nos entrega esta librería (de tipo **Creation**, porque estamos creando el observable).
Por supuesto que hay varios operadores mas, de este tipo y tambien de otras categorías que vamos a empezar a ver en los proximos posts.


## Observer y Suscription

**_Subscription_**  nos indica la **ejecución** de un observable. Como dijimos recien, los observables son  **_lazy_**, si tremenos vagos!!!! asi que si no nos suscribimos a ellos, olvidate, no emiten ni un sandwich.
![enter image description here](https://pbs.twimg.com/media/Etev4m4WgAE2N8Z.jpg)

**_Observer_**  es un objeto que **reacciona** a los valores entregados por el observable. 

Para que nos quede claro, todo se resume en:

    interface Observable {  
      subscribe(observer: Observer): Subscription  
    }
    interface Observer {  
      next(v: any): void;  
      error(e: Error): void;  
      complete(): void;  
    }
    interface Subscription {  
      unsubscribe(): void;  
    }


## Operadores

Como veniamos hablando antes el operador of, el from, y vamos a tener unos cuaaaantos mas que vamos a ver aquiiii, pero qué es??? Bueno como todo en JS, es una **función** si, que toma un observable como **entrada** y genera **otro** observable como **salida**. 

**Clasificación**: creacionales, de transformación, de filtrado, condicionales, de combinación, multidifusión, manejo de errores y de utilidad. (sip, en el proximos posts vamos a ver estos loquillossss)







