---
date: 2020-06-18 12:26:40
layout: post
title: Unit testing con Jasmine!
description: Reactive forms
image: "../assets/img/tests2.png"
category: test
language: es
tags:
  - jasmine
  - reactiveforms
  - humor
author: sol lopez
---

# Unit testing con Jasmine!

## Metele tests!

Hola! Siguiendo con unit testing.. alguna vez les pasó que los tests que contienen un reactive form no instancian correctamente los controles? Bueno, ya les va a pasar :O

A veces nos vamos a encontrar con esta maravilla:

```typescript
    formGroup expects a FormGroup instance, please pass one in bla bla bla
```

Bueno, muchas veces no vas a ver este error si mockeaste todo joya de una, pero sino... holis

Qué significa este error?

Si nos topamos con este error, significa simplemente que el test no llega a reconocer ninguna instancia de formulario de nuestro componente, es decir, no logra ver que existe un formulario en nuestro template y su asociacion en TS.
![enter image description here](https://www.generadormemes.com/download/82iu845i7eevh1my3la94t5thtcbgwhkrp9fazs6m8pfdrq6ck21t0hjshlz0b9)

Para empezar, repasemos lo básico que debemos contemplar a la hora de construir la base de nuestro .spec de un componente con formulario:

En los imports, aseguarnos que contamos con los siguientes:

```typescript
    imports: [
        ReactiveFormsModule,
        FormsModule
```

Y si tenemos controles custom, agregar esos modulos tambien, por ej

```typescript
    imports: [
        SelectModule
        InputModule
```

Segundo, mockeemos los valores de las variables/arrays o de donde sea que esos controles consuman para poder inicializarse. Si no necesitamos inicializar, podemos dejarlos empty o nulos, pero siempre mockeando el null desde nuestro .spec.

Por ejemplo, en el caso de un select, tomará los items de un array, podemos mockear el array o pasarle [] al mismo para que el control pueda instanciarse correctamente.

Finalmente, necesitamos llamar a nuestro querido

```typescript
    fixture.detectChanges();
```

Esto es necesario para que nuestros tests corran el ciclo de init de angular y el init del template, donde tenemos nuestro form.

![enter image description here](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSBjIp1tH1msYRzKrod0BjyHJbnwNhmMBO0WzHhXcZd3cAEZt3H&usqp=CAU)

Siii tenemos un BONUS!

Si queremos no solo mockear los valores para instanciar nuestro form, sino tambien armar nuestro form builder a gusto en el .spec, es posible:

```typescript
    let fixture: ComponentFixture<ChildComponent>;

    const formBuilder: FormBuilder = new FormBuilder();
```

y luego:

```typescript
    providers: [{ provide: FormBuilder, useValue: formBuilder }]
```

y en el beforeEach:

```typescript
    component.form = formBuilder.group({
        firstName: null,
        lastName: null
    });

    fixture.detectChanges();
```

![enter image description here](https://i.pinimg.com/originals/39/46/07/394607fdeea1f286afe8a4a0a28ec9fe.png)

By Sol López, frontend, rosarina, baterista, rock & metal.
