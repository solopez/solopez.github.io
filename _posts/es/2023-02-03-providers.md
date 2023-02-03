---
date: 2023-02-03 17:00:00
layout: post
title: Inyección de dependencias
description: Conceptos, teoría y ejemplos prácticos de providers en Angular.
language: es
image: "../assets/img/di.jpg"
category: CODE
tags:
  - coding
  - providers
  - dependency injection
  - humor
author: sol lopez
---

Buenas! Feliz viernes! El post de hoy va dedicado a la inyección de dependencias en Angular y cómo podemos proveer estas dependencias en módulos y componentes. Como siempre la docu oficial por [acá](https://angular.io/guide/providers)

## Inyectando un servicio en root

Supongamos el siguiente servicio:

```typescript
import { Injectable } from "@angular/core";

@Injectable({
  providedIn: "root",
})
export class UserService {}
```

Cuando usamos el `providedIn: 'root'` , significa que este servicio lo vamos a poder inyectar en cualquier lugar de nuestra app. Y además, que la instancia de éste es única y compartida ([singleton](https://angular.io/guide/singleton-services)), para quienes invoquen el servicio.

## Inyectando un servicio en un módulo

También podemos inyectar un servicio a nivel modular así:

```typescript
import { Injectable } from "@angular/core";
import { UserModule } from "./user.module";

@Injectable({
  providedIn: UserModule,
})
export class UserService {}
```

O también asi

```typescript
import { NgModule } from "@angular/core";

import { UserService } from "./user.service";

@NgModule({
  providers: [UserService],
})
export class UserModule {}
```

Si bien ambas formas son válidas, la primer opción es la más recomendada porque habilita el **tree-shaking** (el cual permite que Angular optimice la app removiendo el servicio de la app ya compilada si no es usado, mas info [acá](https://angular.io/guide/architecture-services#introduction-to-services-and-dependency-injection)).

## Instancias

En Angular existen dos tipos de carga de módulos, la carga eagerly (ansiosa) y la lazy. (Si queres repasar lazy modules te dejo el [link oficial](https://angular.io/guide/lazy-loading-ngmodules))
En la eagerly, los módulos se cargan al iniciar la app, sin importar nada, mientras que la carga lazy funciona a demanda, bajo una condición, es decir, si no se navega a cierta ruta por ejemplo, esos módulos no se cargan.

Entonces, para el caso de una app que carga eagerly, se preparan y disponibilizan toooodoooos los providers de los modules que no son lazy.

Pero esto funciona diferente para el caso de los lazy. Cuando Angular carga un lazy module, crea un nuevo **injector**, que no es mas que un hijo del root injector.

![enter image description here](https://i.pinimg.com/originals/78/8f/83/788f83c6a233753079a45fdc4a45cbf4.jpg)

Imaginemos un arbolito de inyectores. Tenemos el root injector y luego los child injectors por **cada** lazy module. Estos child injectors serán los encargados de preparar y disponibilizar los providers de su lazy module correspondiente. Y cada componente de ese lazy module, tendrá su propia instancia local de los servicios child indicados en los providers del mismo.

_Nota_: Esto se puede poner heavy si hablamos de jerarquías de los injectors, pero vamos a dejarlo para otro post.

Por lo tanto destacamos por un lado, la instancia única y compartida ([singleton](https://angular.io/guide/singleton-services)) de un servicio (para los modulos eagerly), y por otro, que cada modulo lazy tiene su propia instancia del servicio como vemos aca:

![enter image description here](https://angular.io/generated/images/guide/providers/any-provider.svg)

## Scopeando providers en componentes

Es posible limitar el alcance (scope) del provider agregando el servicio que queremos limitar al **array de providers del componente**.
Los providers de componentes y los proveedores de _NgModule_ son independientes entre sí.

Este método para inyectar en el componente, sirve más que nada cuando queremos en un módulo (eagerly) inyectar un servicio **sólo** para sí mismo.

De esta forma, podemos **limitar** el servicio e instancia sólo a ese componente y sus descendientes.

```typescript
    @Component({
      /* . . . */
      providers: [UserService]
    })
```

Happy coding!
![enter image description here](https://i.imgflip.com/1z6225.jpg)
