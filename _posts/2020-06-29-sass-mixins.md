---
date: 2020-06-29 21:28:40
layout: post
title: Mixins Mágicos!
description: Mixins, experiencias y ejemplos!
image: 'assets/img/mixins.jpg'
category: SCSS
tags:
  - mixins
  - sass
  - superpowers
  - humor
author: sol lopez

---

# Mixins
## Haciendo magia

Hola amigos! Como lo prometido es deuda acá estoy acercando el post  para compartir algunas #experiencias y #tips para mis queridos @***mixins*** poderosos que nos brinda [SASS ](https://sass-lang.com/) ... toma pa vo![enter image description here](data:image/jpeg;base64,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)

*¿Qué es un mixin?* Un mixin representa un bloque de código que nos permite agrupar declaraciones css que sabemos que vamos a reutilizar a lo largo de nuestro proyecto.

Entonces para crear nuestro primer mixin podríamos crear dentro de la carpeta styles, un archivo llamado **_mixins.scss** y escribir un bloque para un elemento determinado, por ejemplo un titulo:

    @mixin title {
	    font-size: 30px;
	    line-height: 22px;
	    color: $random-color-from-previous-post;
	    font-weight: bold;
    }

Entonces cada vez que necesitemos incluir un titulo en nuestro template, le agregaremos a la clase que lo contiene, el mixin, nuestro **html** podría ser algo como

    <h1 class="title">Title</h1>

y vamos a pedirle que renderice ese título con nuestra convención declarada en nuestro mixin en nuestro **.scss**:

    .title {
	    @include title;
    }

Con sólo esa linea ya estamos renderizando las 4 css rules que definimos en nuestro mixin. Cada vez que tengamos un elemento que deseemos renderizar con las características de ese title, solo escribimos *@include title;*  y la magia sucede 
![enter image description here](https://img.vixdata.io/pd/jpg-large/es/sites/default/files/s/smart-meme.jpg)
    
Ahora, podemos ir más allá y empezar a escalar o flexibilizar nuestro mixin. Siiii hay mas magia! 

Si por ejemplo queremos mantener nuestra estructura de títulos pero queremos que pequeñas cosas puedan variar, sin alterar esa estructura, podríamos modificar nuestro mixin para que sea parametrizable, entonces:

    @mixin title($color: blue) {
	    font-size: 30px;
	    line-height: 22px;
	    color: $color;
	    font-weight: bold;
    }

![enter image description here](https://i.pinimg.com/originals/b1/c7/2f/b1c72f820b855a5aa0c65840eb07fe37.jpg)

Alllllta magia ahí... con eso recien hicimos que nuestro mixin esté preparado que un color de título por defecto (azul). Y, si le pasamos otro color desde otra página con otro css seguiremos reutilizando nuestro mixin dinámico:

    .title {
        @include title(red);
    }

A su vez, podemos crear otro pequeño mixin de complemento:

    @mixin bottom-line($color: blue, $margin: 1rem, $padding: 1rem 0) {
	    margin: $margin;
        border-bottom: 3px solid  $color;
        padding: $padding;
    }


De esa forma si tenemos otro título que si queremos que dibuje una línea debajo del título, con nuestro mixin ya creado, solo debemos escribir:

    .title {
        @include title(red);
	    @include bottom-line(red, 2rem, 1rem);
    }

Nota: Si no le pasamos parametros, también funcionaría con los valores por default `@include bottom-line();`

## Nesting
Siiii satamente! Podemos anidar e incluir otros mixins dentro de nuestro mixin si así lo deseamos, por ejemplo creamos un mixin estilo link:


    @mixin special-link($hover-color: white) {
	    text-decoration:  underline;
	    cursor: pointer;
	    &:hover {  
		background-color:  $hover-color;  
	    }
	}
       
 Lo creamos como mixin porque la idea es usarlo estas reglas de link en cualquier elemento, no sólo en los títulos.


    @mixin title($color: blue, $hover-color) {
	    @include special-link($hover-color);
	    font-size: 30px;
	    line-height: 22px;
	    color: $color;
	    font-weight: bold;
    }


Entonces ahora, cada vez que usemos nuestro mixin title siempre va a tener incluido las caracteristicas de link, y no sólo eso, sino que también podremos definir el color del hover si deseamos uno diferente al que elegimos por defecto (el que casis siempre se aplica es el que vamos a elegir por defecto):

    .title {
        @include title(red, black);
    }

Con eso vamos a renderizar nuestro título con link y hover color negro. 

A medida que vamos definiendo las reglas de nuestro proyecto, podemos ver qué tanto nos conviene parametrizar y flexibilizar nuestros mixins, y que tanto nos conviene acoplar opciones dentro de los mismos. Por ejemplo la anidación no tiene límites, si queremos seguir el primer ejemplo, en vez de incluir 2 mixin podriamos agregar el mixin bottom-line y special-link dentro del mixin title principal:

    @mixin title($color: blue, $hover-color, $size: 30px) {
	    @include special-link($hover-color);
	    @include bottom-line(red, 2rem, 1rem);
	    font-size: $size...
	}

De esa manera solo invocaríamos al mixin title, si es que siempre queremos incluir por defecto los otros mixins (de special-link, bottom-line, etc) y nos evitamos agregar siempre los mismos 2 o 3 mixins cada vez que decoramos un título.

De hecho si empezamos a notar que casi siempre incluimos los mismos mixin a los mismos elementos, lo ideal es anidarlos directamente en el mixin y podemos meter una lógicaaaa para los casos en los que no los queremos... que pasó? te quedaste de cara????

![enter image description here](https://pbs.twimg.com/media/EPontr9W4AADjys.jpg)

## Argumentos

Veamos como quedaría!!!

    @mixin title($color: blue, $hover-color, $size: 30px, $include-specials: true) {
	    @if ($include-specials) {
	        @include special-link($hover-color);
	        @include bottom-line(red);
	    }
	    font-size: $size...
	    blabla...
	}

Ahora en nuestras clases nos queda elegir cuando deseemos que los special mixins para link y para bottom line NO sean agregados

    .title {
        @include title(red, black, 30px, false);
    }


![enter image description here](https://www.mememaker.net/api/bucket?path=static/img/memes/full/2017/Feb/4/0/beleza-boa-noite.jpg)

## @content
Así como en [ANGULAR](https://angular.io) tenemos ***content projection*** o ***transclusion*** con **ng-content**, aca tenemos algo parecido! con *@content* lo que hacemos es permitir proyectar otros bloques de código en un bloque css por ej, veamos:

    @mixin small($width: 320px) {
        @media only screen and (min-width: $width) {
            @content;
        }
    }
    
    @mixin tablet($width: 768px) {
        @media only screen and (min-width: $width) {
            @content;
        }
    }
    
    @mixin desktop($width: 992px) {
        @media only screen and (min-width: $width) {
            @content;
        }
    }
       
 Y lo invocamos:

    @include small(345px) {
	    font-size: 20px;
	    ...
    }

    @include tablet() {
	    bla bla
	    ...
    }

    @include desktop(360px) {
	    ble ble
	    ...
    }

Al tener nuestro **@content** en un mixin, podemos ahorrarnos las media queries que después de mucho tiempo pueden ser muy tediosas, tener que escribirlas en cada css, o en cada clase es un poco mucho jajajaja de esta forma solo escribimos include small..o lo que sea que le pongamos, eso es elección de tu dev favorito :D

Asimismo, como vinimos viendo hasta ahora, podríamos tranquilamente incluir estos mixins del tipo media query en nuestros propios mixins, para que una vez que invoquemos nuestros mixins, no debamos preocuparnos del breakpoint ya que el mixin automáticamente se adaptará a cada escenario.

![enter image description here](https://media2.giphy.com/media/ZF40pid2AozVC/giphy.gif)

## #experiencia

El otro día tuve que renderizar unas marcas muy visuales dentro de una pantalla, recuerdo que eran como 4 marcas, muy muuuuy similares, cassssi iguales pero que las diferenciaba la posicion de cada una, que hice? sale mixinnnn con fritas po favo 

![enter image description here](data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkGBxMTEhUQEhMWFRUWFhYVFRUYFRUVFhUXFRUWFhgVFRUYHSggGBolGxUVITEhJSkrLi4uFx8zODMtNygtLisBCgoKDg0OGhAQGy0mICUrLS0tLS8tLS0tLS0tLS0tLS0tKystLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLf/AABEIAMIBAwMBIgACEQEDEQH/xAAbAAABBQEBAAAAAAAAAAAAAAAFAAEDBAYCB//EAD4QAAEDAgUCAwYEBQIFBQAAAAEAAhEDBAUSITFBUWEicYEGE5GhsdEyQlLBFCNi4fAz8QcVFoLSF1OSssL/xAAaAQACAwEBAAAAAAAAAAAAAAABAwACBAUG/8QAKxEAAwACAgIBAwQBBQEAAAAAAAECAxEhMQQSQRMiUQVhgbEyQpGh0fEU/9oADAMBAAIRAxEAPwDJV6lRhhwI81A6+K9xxD2fo1PxMCzV7/w+ou/DokvFP4OsvMy/Fnlj70qu+uSvRa//AA46OVb/ANOndVFErpFazZb7o89cSkKZK9Hpf8PjyiVt7CNG6PPwL9YXNUeW0bBztgUdwz2Xe8gkL0609mKbPyonTsANgipfyUrNE8SjI4V7OtYBpqj1CyjhFm2ylbQV0jJVuihStlZZQVptJSNpolCFtJStYu4hDr7FQ3RupQb0EvPeG7rhlwDss7/Eue7UopZqvsRoLMZKk/h+64oFWmlXRUrG3KjdTI4RAlcFyhAelCvPYOQonUBxohsJWhJSOokd1FmRIdALoLiU8qEO065BTyoEdJMnUIOEkgkoQSSSSISQtXJapSE0KF2QFibIpyE0IA2yvkSyKctTZVAbIciWRTZU+VQqQhq6DVJlThqhDgNUdes1gklQYjiTaY6nosxdXjqhkn0VKtIKnZdxHFi7RugQtuqcMlTU6calJd/LGKedIntKSLWzYVexokiYjsiDAsmTzJUe2Nplvo17apaJaVZWW10Fu2HgwuqdwSNdOqRn/UbmE4Xfz+BuPxVXb/gs3vtAyl/qNcB2g/JR0MYp15NGpqPyxB+BQu8s21SST/ZCX4K6n/MpuM7iNFjfn5Mk+tP+Vwb58TDPK7NTXxF7fxD1Ce3xUOWPusfqM0qMMddJ+Ce1xFh1afTaE/D5uSf8uULy+HLW0tf0btl3KlzhyyNvicEAmQUatLpp1ldbFnm1tM5uTE47L76PT4KPNwk27UpyuC0J7FaOA5dAqB7S3fbqnDkSE4K6lQhy6BRISylK4lPKhDtJcSnRCW4ShdQkgXOCE0KSE0KFWcQmhdwlCgDiE8LuFy9wAkqAGKC4ti4b4Wb9VDiuLTLWbdUBdqkXlXSGTG+Wc1apcZOpXVNiTGK3QpJK5GPgenSV7C7UVIeZAGwOh+CmwkeInjbXT11RCpbA8fDRczzsv1E4T4/sfhfpz8/0cg5XbSI9QrAynVVWgtOpkbeSjuaTw7Mw6HcT9AuE05eh/r7fJYrW7TMoXiFgS2GPA8/pK4rXkAkuOm6pHGQdAQnRltJpdMfPjVtV+ClUbXY6C3NpMtMmOsbqS2xQjQnRXaN9r1n6Kao+nU0ewH0E/FV4H0m/gF3VGjW1cNeqq/8AT1MSWyJ5BkfBGzgTCJpvLT03H3VKpZ16eoEj+nXTyTpyORHu+tgVlsaZIMkDbXQ/HZTHFWsiJB5BRCniLHaPEdT/AGQvF7QkyyHN47a9E6MvO1wMXrfFoJUvaVgjNI7jVE7TG6Z/C8eWywFwWtMglukFp1HmCr9ldggS0EckLevOyT3yVrwMNdbR6TRvGuG64eI1G30WJpVmDx5iwRoQTr5hFbG5rj84e3iRrHmE+P1SP9aaMeX9Na5ml/Ro2uXYKGNuyBmyyOg4Vm1u2vGh9DutuLy8OV6muTFfj5IW2uC4CnlRgrsFaRJ3KS5lMrBCiSdJQJzCSeEoQKnKULqFDdXDWCSoQevWDBJKy+KYqXmBoFDimJF57dEPYFlyZfhDYx/klaJKkoWDC+QYdyJ39OV3Qpq06wZULcxc0jZzTBH7FcrzIdx30bvGzLHT/cpYhZOa0lsT16fdUsKvaw8TyxwHVpH0RTFMEeGkNrudvo8Dp1aB9F3g1rlp+6eGugzvmJHU8wuV9a8U6VHS3hrHukm9/jTIn+0jQJcw+hn6gKay9o6bjEnXgtII8js5SXFlSdpkA8tFVpYTSnQa/boqrPtFfp4KXTQWq3TXD8Xx0UVK/wDyncbdwoH2zh+Aie5PyCHXNncDVsnngj5jZUulZSMMvjZNiNVubaJ+BWXvaGpcNNTBBWktGOcB7xhDuSGuAPlqoq1Cm0HM6G7kwfoQpD0zXNKV6vZm23lRmm6sWWKCZdM9Dyq9/c02mW5i07GAOSNQTPxhQ1q7WxngAiddviNjqtn0VSB71Pa2jZYfezsd4RuhXleb2dZ7CH0znZExMmO36locMx9j/Pp/bdZ7xuTLn1fMmjrWtN05mNM9hPnKzmM4ayi33jHmP0nX0BRqncAxB4QPHrlrne6IkASfMpcputCY47AdSg2rzBQKrTqUHyDPUcFaF9kRq0yOnPx5UVUhwLHCDtJW2Kc8Po0RlKVzf5mthoPY8ei0GHYpDNQ1gGm+ixl9NPwdDIStsR2kE9pn6q1Y9rgdTXTPTbe5BbmkZY1PC6AaC2o3giY2I6/NYqljktDD4R8ERoYw4NyHUR/gKzxNTaaXyVrFuHybunUkSFKCszgd8Yg7fRaFj16+a9ls83U6ZPKS4zJK4A0knSRAMknUN1cBgk+gQb1yyHN5dCm2SsjiWIF5JO3AV7FKdV4z7/08hAnsMwQQe6w15M3xLHzia7IxqrNKmnoUVepU1VFm9D21KFcbRJT29FWKlUNClwvXddC1T3wWbeCyHbqC4e2mCRz9VxVqtptNR7g1o1JPCi/i2vZnY4PadiCCD6heazerb0uDoY5fyV2vbVmNDCF3TalPjM3pyPIrq6Iac7HGmf0xLDzxqP8ANF1Rv/eaOgHQR6xos7xrW0dGE110Na4noNfQxPp1Rahf9Rp1WcxPCyJqUhM6ls+F3kfyu78qlb4q4NLmAvy6Opnw1GHoR/kq842/8QXjm+j0CkQRou6luwiC0H0WSwX2op1dCAxwMFriAVp6dw07GfVX9XL0zDkxVDK9bBqDtHU2kHiBugOJ+xlB4cGjKBOxI7o/XxFrXFokuHCHY/i/uqDnkeIg6dDGmitNUmlPY3E821z2eX2dN1G4dRYZZqXA8RpmBGx2HeeyLXdqKgzDR45Gk+fdCKZc0moTJdqefhCK29WQNIJ27rfmyJvf/I6sFc1JXbe3FLQVHDzAP1XNLEi55NTRxMzwfsisNd4Xjt3Q/EMIhpe0ggddx91RKfwZ/b4YXtqynqhrhqPXlZW0qubsf+07f2V+4vXZDAObojr4KevIMxg535G6xzp8FSbZVG6hhcO2v0V2yIJ1BnlaHDy3yR93K0aapPgCWWR4giPMQQjVDC2kCCtDaUGnofgrwsWaeEeip76e5E1e+GB8GEHIdx8wj1s/dvT6FUru2Ywy0Q6IlNY3EucTuYgeS6/h+ZNv0fD/ALMObA0vZdBkOSUAemXTMhqE6S5q1A0EnYIsBxc1wxpcVnhcCs/V0a6DsquLYiajoGw2QozuNxssPlt3DlD8S09s2z2dFFc2DXbgT1QbDcX0h5gjrz6o7b3QcJBXDpNP8GjTXQMfhBH4DPmoizIfHp9EYqPA1mPVU7dzs7szg5pgs0Hh01aeuus9+yYvNrGvyD6XtyykcRA/CDHXZDX1i9/iMDhaK8w5tQRq3uDH0QirhhYCC6TwTE/Hokv9Suv8uhuPDj19r5LLg14yuEgftygrsEfQf72i9xpu/wBSm4z5Ob3GneFLTu3U/CYLdZI3B8uVep3QI0Oiwun7Nrpm6ZuF+wJL808qjVokTkM8wd/iiuL4Yaoz0nFjx0MZuxWXqXtRjslYbfnAgHzHBV5ja47HRzzLDlriZLQJI42mesqreWzKpDpNOp+V7eZ4I2I7FTYZVpuaQeeVHSMOIaZE6H79EfX1+6RuNzW0+wVieGEmagyvERVbLWu6ZoPhPnp3XFvideiMsF46nUgLXUKnvCWFh8IMO2B7T1QK7w4mXUvWm7QeQMS0/Lsne6r7cgn7pKjva2o6QGhp2kkk/NcgOrHM92frOoHfKOE1WwZUEQWvHBEHfrz6SomNfRMHb9Q/fomLHM8pCbvfC4JKuBPiaWuslv8A4lT4ewZg1wII4KK4dfAgAiCedtESubBlQSRDuHDceXXyQtKlwVnyKniirWwxtUAgw7g/sR0Wdxxr6ZFN4ieeHR0KMXV1UtCDU1p8PG0nh3Qqw/F7WuzK9zdevHcHgpU057XAtz8oxvu+VctT8FHidIMfFI5m9SR307qo64qU4cWy2fFHHdapr26BWNpchbEqNP3ZflhwG40PxWftMVqN0MFFr25D2ANO+/bzQ+hZyVpx4fZcifqNBnD8f/UI/wA2R3D/AGhpOO5B7grP22HhaTCrBlNpquG23dX/APhT6K1nX4Kl9iTvehgaXA7nbT1RGixubMBBQ+pXzvLj6dlet1qweBjxtU+WKy+VVr1nhBJrklG1OugZTYrM49iWY5GnQbonjd7kblG5WSfqZVMta4DE75OAVZpUlHSpK9SYs2tjm9Fd1subFjjnyktdwNR56dSilOjKa5pBsO2I+fZYPMw1Ubk0eNlSrTBrrKuI1gu1cZJ/7VapUn5Guk5vn6otYXHvGg6JVN/ILztM215FN6aR1h15mGV2jhuOvcLvE7EVWETBGx+/ZCrjMP5g0jXv2RPDcSbUEHRw3CMNPhme8dS/qR/4eWY/d1qVT3ZBa4HjUOHrurOG4s4fjgDkAzB6xwvRMRwplXWBmG0ifQjovP8A2hwaoHOcxgzDUtG5+89VpmopKWtfudTF5E5lr5NTaXAcAQd/n3lLEsPp12lr57OG48jz6rHYTij2O0Bgalp3Hdvf6rW0r9rxmBmdfP0S7lyIyY6itoyFeyq2jw1+rDs4fhI/by4Vp9fww0/Q+XqtZWcyo003gFp38uvms5eYB7szTcXDeCNvMj7J0ZU+we7p7+SzY4yA3LEdTuSPT6JquJAlxac0DeRM9J5QtrZnYOBg/DT0hd1sPIbLCcw1iSJ8u6v9JdjZywn9y5CFDJWZLtHany8iNRuoLhpbvLmfqAlzfMDceWvmhmHYrlcZeBx4gQdOCRoVBiGLvaJzTyXCSfLLyePSUYmk9Lol4Zrpl0W0DNSMj9M6ebTwiNli7tncabarDf8AU1RjszGzJ1aAYJ8uD3HzWqsqrbhgqhj6TtdHCDpp6jzTsmCpXsY64emaHEAyvRLCMzSCPlPyXmhtjSqFh1g/ELY/xTmCCNeCBusvi7iwte4aEkH66fBVwU+ijWixSoTq31H2RW0p5mxGvIQuyu2xmBEca7rqjiIFQO1A54UuKfKRaGtabCdzhMDMz1H2XNpbon/zKmW/iB+E/BR4TbucexOnZbPBy5KfrS/kzZolT7Jl3D7PMddhuosZxAEhjfwjb7qzi942kz3bTr+Y/sFnqMuMldiVowt7CFqEWtmofaU0Xt2JgCwAmUwakiA4xioXVHHpoFQDUSxmiWOcQJ1nz5VK7qe+AfT1DBJbGojRw+C5/lZnjpcGrDHsiSkArNE6CQQhFve+Lfbbui1O6zDKdCst+VSr7ehixJrkv04AQTFbouORquVXOiBqhlqzxEndNrNOVaRSIccsIYbcOOgHiGhOyLCsdQ6M3Tqs/WYQ9r2OLSDJjmET/iQRLjrz2+3quB5OFTbRsS90noixqnUNOKUy4+LrCHYPcCfdPnPw7gHf/CjOxDySew2PmpqrWN/mMYCT0AHzWfpaY+cuo9Nd/P7kttckeF+nGbr5ru9tQ/UjUag/t5KtaudUac7RHH90/wDEFmhkt+nkqO9LTMrlqvt7AGJYE2o4PAyvG57jg9UIq2r6LszOsPbwe63N4zM3O3f/AOw6LM4mD+Nhlp0I6f3CM01w+jbhyO1pnFG5n6Gdx5q5RfI/zRZXEMdYxgc6GkGO5I6dUS9lsZZdMLm+FzdHsJ18x1C0vFan21wLrh6J8RwnORUpkNeNJM5XDfK4fvx8kLrXTmVPdvEOiYncHkdQtY0QFHd4bSrNy1Gg66H8zdN2ngq+PPrhlfZPsw+LWYJzt5/EO/UKlRoa91p8SwurbDRhuKXLgR7xs9WR4h3Bnss+97S6WyBoRO60S98oHs18lug5jT4msY4fnAEHvMaLSYdUoO0dVpdvG2fqs37wQZWbxzEAAW0xvu7p5d0yYq3oXv5NvibG+8yscHDeQf3Giq3VJrhkqNDmEaz9R0WXwLFXkZc23J1IRy4bIEmeVWPHr6nrv+S2TIlOwRRw5rSQ38MmCenCuUbHMVZpU5RW0t12ZxIwPIzixw1ojSTwjtzXFCnxnI+ATU2Ci33j9/yhZfEbx1Vx1kTr3/snxjS5FOmyOrVNR0n0+6vWtJQWtFF7WinIoWbWmilBigtqSIUmIlRw1JTBqSsQK4lae8bPIWUos9xWDvyuOV4410B+MLbAobi+HCo0kDzCT5GH6kNfJbFfqzDYhQyVSB+EmW+R49ERtyCI54PK4uaoafd1hI2a/wC56q9h1BrYc0z6rzjen632jr+vCpdEby+mROoTaHUbrvFKBeHNzOZmBAc0kFp4II6ID7N4Vc1A9tSs8Fp/VJI11BeNQd5S1eud/wDY36c1O3wFnUS4OBOo1kfIBK1q54/VseCSNPVDsQ9n3sBeypV95+svcdOhbtHaIQdmLup1A2r4XTofyv8AI8Hss9T9R7T2aJlfT4ezSXVGrTE0zp+lxkek6hVqXtGWuyuGUnXI7QHqGu5U1HFmvYQSc0cLP3TqjiWvYKlM9dHD7qszzqiRi90+jc2eO03HLOUkbHvwCrFdsheeCxqMg0iXj/23gy3sDE7eav2GNvb4ZI/odr8O3kUMmFWvtZneH0e0ac33ugSZI6Dr2Q7FrljCKjT/ACq0g/0vA+Uqpd4gazAzRrjyCd+PJD/ae1c6zcQfEMr3gExIjM4c6b+QQwYHtTQ2PVNV/uYD2ipk1Jbrq7niVSsbitReKlPMxw2I+h6jstRa4E6pbMqx4nAu7jUx8d/VCxQLSQQZC7M5Up9PxwKyNVTaN17L+2lOqBTuIp1ZIBEhjtoMnYmSInjvC1rHid1417rt8kbwfHqtGGk52aaEmWj+k9OywZ/GT5x8fsK0en1bgZYiV5V7YVxTr5aboO5A6mdVtaV46owPBHfSYWP9q8Dl4r+LxQHHoQqeIlOT7i62k0gTQqOfo5xU/wDy2REf7KK1olvdaDC3AwDH+fRbapp8C29Gbp4caL5Ex36I7Sl8RsAtFd4OHskDTr07oZY0S05DuNFo8eld7fZmyP7Se0tuEftbdtNvvH6AbDqU9hZBjfeVNANfNAcfxgvdlbp0HQdT3XVmTG2V8bxN1VxA8vIdAq1tRUdtRRW2opiBsltaKLW1FR21FEqNNWKklGmrbGrimxTtCJB4SXUJIkDCcFMkrFGC8ZwltVpIE9QsLc0atu45CS39J/Yr04FUMUwttVpjdZPJ8Scy65NPj+TWN/sYq3x1r/C7Q9/uizbiMpbEjaORyEAxfCCww4eTvuhza1Wn+F0gbTquDl8Op4OrGaLR6Hb1w8TweqA4/gLXgkNDh+k6j06IFhuPVWv1gzv3/uttZ3jag0meQZB/v5rBkhy/3Ct437T0eW3dGpQPhlzeQfxCOAefIqzh+NscRrHyIW2x+wpOABIDzt38/kvP8fwgtJMQ7h0b/sQnY8iri+/ybJ1knaNPbX4J4P8AnVSXVtSrDX0J0WCsL57dNiOOD5I1a43sHE/QK+TBoTtphSrh9Sl4meNo6/SVcs74EwfCeWu2/wBlxaXwcIBnoCforj6LagAMSNj180v1aF1S/AVbasLRkAEACBoBAjZZT2jwEul7NCNSjltTqUtWnOOWkmfQ8KyLtlQw7+W/bK4xPrsVZVoz8p8HlclpggyOympVW8x/8VqMawshxMbbHqhTaAW7FM5F+5WraCHs5fta4UyRldpvMTtoj93bA0zTcZadlkhbCRA1nSPqjP8AFvMSyT5mFnz+HXsnHIzHmnX3AmhZalukgx0Tm1eyrliZAMDur1vh73OJJ1JnQaD4o9Z4VHiOp5JWzF4tvXuZsuWdv1O8LuiGxkdMRl0+MqxSwxoca9SG6aidP91ct6QaMx0aOVl/aTHcxyt24HX+o9lrxeFMX7iHmbn1I/aHGsxyt2/KP/0UCo0iTJ3SpUyTJ1JRO2oLdoSPbUUWtqC4tqCJ29FEqd0KSu02JqTFYa1EA7GqQBMAuwEQihJOnRIFEkydWKiTSnTKFSC8tGVQQ4CVicZwF9MktEt6fZbxJ4BEOEpeTFNrkZjy1DPIqtLWUbtL3M0amRv1+PTRH8Z9mmulzNCsdcWlS3dMGFw/M8W5pUls6/jeRFy5bCN9bvqO1qaH69kVbhTalL3VTxQNDyO4WTqe0I1adNdJBB3+Clw32wAf7msfDs2oOJ4f27/7rlVirfCN11fotNcA/H/ZcsM7jhw/dZ2rRyOyuEjh0nUeS9YFUOOQ6tdpM6EHkFAPaH2bABczb5t7hWxZ3PFdAWRX32ZrD6JHipuI6gmR8EUtsUc3Rw16jZCrAmnU92/Q6x0cOrftx80ZpW8v181opNsTkaSDFlf5vNXbtgePE3TqsJiddza00iRG/Qx2+KvUcZrRBAPxhMnA6RkqtcoNf6ek5m8tOvwJ2QWo9rqjhT1BMj13XI9/XMccwIHx5WhwfBMgk6lavG8WpexWTKtcnGG4bpJ3KJttBtCusoq1SoLpLHoyO2ypQtAOFcawAZnaNClMNGZ2gHKx3tFj2fwt/DwOvc9lf1Bsb2jx7N4G/h4HXueyzlOmXHMdSU7KZcZOpKI21ur6BsVtQRS2oJregidCioAVCir9KmmpU1ZY1EA7GqVoTNCkARIIBdAJALoBQIydOkiQIJJk6sVEkkkoASZOmUANKr3liyqIcNVZXJUa32DbXRhcc9jty0T/AJweFjL3AXMOxC9tlUrvDadQahZsniy+UasflVPDPI8MxF9D+W+XU59Wd2/ZbGzxDOACQ5p/NwVNifsqNwP3QA4VVozk1ad28eh4K43mfp7/AMpXJux+TNdlrHcBY9oe3cGQRweoQelfFoLXAh40PTzHZEmYiSQx0jqHCPgdiqWP1KcCptG/cHcFYMTqH6UadO1ofDsJbU8TtzrKN22B0xxPnqquCVWvY17CCCNCtBRK9LjiUlo5GSq29ioWjW7CFbYxMwKzTYnJfgUcspruo9rG5nGAE11ctptzOMdB1WNxvGHVDHHDeB3P2RIP7QY4XnKPw8N69z2WfZSLjJ1JU9OgSZO5V+hbIhIbe3RO3t1JQt1fo0VAHNCir1OmlSpqyxigBMYpmhM0LsBEg4CcBOAugFAiATgJwnRIMknSRIXUkkkSo6ZJJQAkkklACTFOkoA5K5KSSJDpqFYqwdAmSQvoM9gC8pgzIHwCx+I0x7yIEdI0+CSS5GRfcdHC3oP4UwAAAADoNEbpFJJbY6M2Tsv26u00kk1CzKY+4+9Ik6Aws9TSSRIXKQV+iEklCF6kFcpJJKALTFM1JJEiOwugkkoQ7TpJIhOgkkkoQSSSSsQ//9k=)

Pude renderizar las 4 marks con algo como:

    @include mark($top, $left);

y listooo, realmente me ahorré todo el css de las marcas en sí, y solo le pasaba como dinámica la posición. Tirate un mixin daaaale

## Conclusión
Como vemos los mixins son totalmente escalables y flexibles a cualquier elemento, tranquilamente podemos renderizar y dibujar estructuras que sabemos que venimos repitiendo o notamos en el proyecto que trabajamos que se empiezan a repetir mucho a lo largo de los estilos en general, ahí es cuando nos damos cuenta que es mejor aplicar **@mixins**. 

La idea es siempre manejar mixins no tan potentes o *bazooka* de entrada, tampoco queremos matar una mosca con un rifle o si? o no? o si? Tampoco seamos muy fanáticos de los argumentos porque después el mixin nos queda cualquier cosa y le tenemos que pasar 10 argumentos para que haga algo mmmmmmm no, ASI NO. La idea es pasarle 2 o 3 parametros nomas en lo posible, si vemos que necesitamos expandir, mas vale creemos otro mixin, simple, puro, que hasta podamos reutilizar en otro lado. 

Veamos siempre que podamos lo que realmente se usa y sirve, recordemos el principio [YAGNI](https://es.wikipedia.org/wiki/YAGNI)

De regalo por leer te ganaste la mosca con el rifle

![enter image description here](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSJHUZWR7dLPtLqkNYbTFVN4rysc-0bdwdpRw&usqp=CAU)


By Sol López, frontend, rosarina, baterista, rock & metal.
