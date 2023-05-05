---
date: 2023-05-05 8:00:00
layout: post
title: Typescript Generics
description: Conceptos y ejemplos!
language: es
image: "../assets/img/ts-generics.jpg"
category: CODE
tags:
  - typescript
  - humor
author: sol lopez
---

# Typescript Generics

Buenas!! como andan? El post de hoy lo dedicamos a Typescript Generics. Como siempre dejo la docu oficial por [aquí](https://www.typescriptlang.org/docs/handbook/2/generics.html).

## Intro: ¿Qué son?

Un TypeScript generic es una herramienta que nos permite crear funciones, clases o interfaces que trabajan con diferentes tipos de datos.
La joyita de esta herramienta: escribir código más flexible y reutilizable.

Podemos crear funciones que acepten por ejemplo arrays de tipo string, objetos simples, complejos, etc etc. O incluso para crear clases que puedan manipular cualquier tipo de dato que le pasemos.

Es importante que tengamos en cuenta que, si estamos laburando únicamente con un solo tipo de dato, lo vamos a definir directamente y chaucito, no hace falta aplicar generics para todo, eso sólo complicaría nuestro código y no queremos eso, _KISS_
![enter image description here](https://media.designrush.com/agencies/262188/conversions/.K.I.S.S.-Software-logo-profile.jpg)

## Problema

Para entender mejor qué es lo que viene a resolver un TypeScript Generic, veamos el siguiente problema:

```typescript
function addTodo(item: string): void {
  todoList.push({ taskId: id++, task: item, done: false });
}

function addTodoNumber(item: number): void {
  todoList.push({ taskId: id++, task: item, done: false });
}
```

En el ejemplo, podemos ver que tenemos 2 métodos CASI igualitos, lo único que los hace diferentes es que el parámetro que le pasamos es string en el primero y number en el segundo.
Y no sólo eso, sino que teniendo esos 2 métodos, estamos yendo en contra del principio **DRY: Don’t-Repeat-Yourself**, según el cual "todo conocimiento o lógica debe tener una representación única e inequívoca dentro de un sistema".

Entonces, cómo podemos hacer, para unificar y adaptar ambos métodos para que pueda tener el poder de manipular ambos tipos?

Primer respuesta que llega a nuestras mentes: ANY
![enter image description here](https://i.pinimg.com/736x/11/81/07/118107c3d36f9e5fd9481fce48dd56df.jpg)

```typescript
function addTodo(item: any): void {
  todoList.push({ taskId: id++, task: item, done: false });
}
```

Si bien podemos decir que con el malvado y prohibido any, estamos aplicando el principio DRY, también estamos generando un nuevo problema: que ese método acepta cualquier cosa, lo que significa que no vamos a **controlar** los tipos que aceptamos ni que retornamos. Ni hablar de que estamos perdiendo los poderes y beneficios de tipar nuestro código.
Así queeeee pues, vamos a aplicar DRY y type-safe, para asegurarnos de seguir controlando los tipos de datos aceptados/retornados. **TS Generics**, al rescate!

![enter image description here](https://www.meme-arsenal.com/memes/dbbb12279c0e4e7b07c6d822efab1d30.jpg)

## TypeScript Generics: Funciones

```typescript
function addTodo<Type>(item: Type): void {
  todoList.push({ taskId: id++, task: item, done: false });
}
```

Analicemos un poco la solución que aplicamos con TS Generic. El `<Type>`, es simplemente un placeholder que va a ser reemplazado por el tipo cuando ejecutemos la función, asegurando haciendo la misma type-safe.
Por ejemplo: `addTodo<string>('Sama');`
Declarando el string, evitamos que se pueda pasar un param que no sea string.

También podemos poner que nuestra función ya tenga el type por default, para no tener que especificarlo cada vez que la invoquemos, de esta manera:

```typescript
function addTodo<Type = string>(item: Type): void {
  todoList.push({ taskId: id++, task: item, done: false });
}
```

En los ejemplos vimos un param, pero también podríamos escalar este Generic para que funcione con 2 params, así:

```typescript
function addTodo<T, S>(item: T, status: S): void {
  todoList.push({ taskId: id++, task: item, done: status });
}
```

Podemos pasar múltiples parámetros como placeholders `<T,S>`en la definición de nuestra Generic function, para luego especificarlos cuando invocamos:

```typescript
addTodo<string, boolean>("Learn TypeScript", true);
```

## TypeScript Generics: Clases

No sólo podemos crear funciones Generics sino también clases. Por ejemplo:

```typescript
let id: number = 0;

type TodoListItem = {
  taskId: number;

  task: string;

  done: boolean;
};

class Todo<Type> {
  _todoList: Array<Type> = [];

  addTodo(item: Type): void {
    this._todoList.push(item);
  }

  printTodos(): void {
    console.log(this._todoList);
  }
}

const Todos = new Todo<TodoListItem>();

Todos.addTodo({ taskId: id++, task: "learn TypeScript", done: true });

Todos.addTodo({ taskId: id++, task: "Practice TypeScript", done: false });

Todos.printTodos();
```

Lo más importante de recordar, es que la diferencia entre clases y funciones _Generics_ es que en una **función** Generic, tomamos el tipo de parametro en el punto de ejecución `addTodo<string>('Holis')`, mientras quen en la **clase** Generic, tomamos el tipo de parametro al momento de instanciarla `new Todo<TodoItem>();`

## Restricciones

Podemos restringir nuestras funciones y clases en casos donde no queremos aceptar algun tipo en particular.
Por ejemplo, podríamos querer aceptar strings y numeros, pero NO booleanos.
En este caso podemos hacerlo usando la palabra `extends` de la siguiente manera:

```typescript
function addTodo<Type extends string | number>(item: Type): void {
  todoList.push({ taskId: id++, task: item, done: false });
}
```

De esta forma estamos aplicando controlando y restringiendo los tipos para acotar y evitar posibles errores (por tipos no soportados) dentro de nuestras implementaciones.

## Conclusión

Podemos decir entonces, que el uso de generics en TypeScript es una herramienta poderosa que nos permite escribir código flexible y reutilizable. Al usar generics, se pueden definir funciones, clases, interfaces que acepten diferentes tipos de datos como argumentos y generar código que funciona con esos tipos de manera segura y eficiente.

Simplificamos desarrollos y también podemos mejorar la calidad del código y reducir el número de errores.
Además, el uso de generics también mejora la legibilidad del código al hacerlo más explícito y fácil de entender.

Referencias y lectura complementaria [aquí](https://blog.openreplay.com/keeping-your-typescript-code-dry-with-generics/)

Happy coding!

![enter image description here](https://www.digitalmomblog.com/wp-content/uploads/2019/04/happy-friday-meme-work-from-home.jpeg)
