---
date: 2024-06-27 11:00:00
layout: post
title: Clean Code
description: Ventajas y prácticas de clean code
language: es
image: "../assets/img/cleancode.webp"
category: CODE
tags:
  - coding
  - clean code
  - humor
author: sol lopez
---
# Clean code

Buenasss como andan? El post de hoy va dedicado a Clean Code, repasemos algunas prácticas y principios. Si bien seguramente ya sabemos por qué es importante, veamos algunas de sus ventajas:

 - Legibilidad y mantenimiento: para poder leer, entender y modificar de manera más facil y segura código que no ha sido escrito por nosotros. Está bueno replantearnos si lo que escribimos, podría ser interpretado y modificado por alguien 
 - Team collaboration: facilita la comunicación y cooperación entre equipos. Si establecemos estándares de código, y escribimos código simple de interpretar, comprender el trabajo de distintos devs es más fácil y promueve una colaboración más efectiva.
 - Debbuging + bug fixes: nos permite localizar e interpretar mejor, si nombramos variables de manera significativa y representativa, si tenemos una estructura clara en el código, facilitamos la identificación y detección de errores junto a su resolución.

![code](https://solopez.github.io/assets/img/memes/buttons.png)
Ahora que vimos algunas ventajas, vamos a eso!
 

## Comentarios en el código
Un buen código no necesita comentarios. Las variables, métodos y cualquier otro componente del código, como los atributos, deberían tener nombres fáciles de identificar y descriptivos.
![clear](https://solopez.github.io/assets/img/memes/batman.png)


## Condicionales
Las condicionales positivas son más fáciles de leer que las condicionales negativas, tengamos en cuenta que debemos considerar su interpretación lo más fácil posible. En caso de evaluar más de una condición, podemos ayudar esa legibilidad, generando una constante con nombre significativo sobre lo que estamos evaluando y aplicarla directamente en la condición.

## Magic numbers
Podemos evitar "magic numbers" o hardcodeo de números si los guardamos en constantes que representen a qué hace referencia ese número o cuál es el objetivo de utilizarlo en nuestro código.

## Funciones y complejidad ciclomática
Podemos evitar funciones enormes con mucha lógica si las dividimos en funciones mas chicas que sólo se encarguen de una sola tarea (recordemos el principio de responsabilidad única).

## Principio DRY
Don't Repeat Yourself. Evitemos duplicar y escribir el mísmo código más de una vez. En lugar de eso, es más conveniente reutilizar, compartir ese código a través de funciones, métodos o módulos según cuánto necesitemos abstraer. También nos ayuda a ser mas consistentes y reducir el riesgo de bugs, ya que si necesitamos modificar o actualizar algo, sólo se hace una vez y en un sólo lugar.
![dont](https://miro.medium.com/v2/resize:fit:1024/1*uywKrvOm4CKZTI6v3a9TjA.jpeg)

## Principio KISS
![kiss](https://image.spreadshirtmedia.net/image-server/v1/mp/products/T1459A839PA4459PT28D187302122W10000H4668/views/1,width=1200,height=630,appearanceId=839,backgroundColor=F2F2F2/kiss-keep-it-simple-stupid-sticker.jpg)
Keep it simple, evitemos la complejidad innecesaria, promovamos la simpleza. Muchas veces menos es más. Es importante que conservemos nuestras clases y métodos de manera óptima.

## Principio de boy scout:
![scout](https://miro.medium.com/v2/resize:fit:530/1*k5xb9ckAsX8rVZgvXiI5bQ.jpeg)
"Always leave code cleaner than you found it." Siempre que detectemos código que podemos mejorar, aunque no forme parte de nuestros cambios, ya sea para simplificar o por cuestiones de legibilidad, go for it. Hoy por tí, mañana por mí.



Referencias [acá](https://blog.codacy.com/what-is-clean-code) y por [acá](https://blog.stackademic.com/top-10-clean-code-rules-831fb34caff7)

Happy coding!



![Beer!](https://solopez.github.io/assets/img/beer-code.jpg)