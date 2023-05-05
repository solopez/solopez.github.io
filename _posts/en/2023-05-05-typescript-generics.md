---
date: 2023-05-05 8:00:00
layout: post
title: TypeScript Generics
description: Fundamentals and samples
language: en
image: "../assets/img/ts-generics.jpg"
category: CODE
tags:
  - typescript
  - humor
author: sol lopez
---

# TypeScript Generics

Howdy? Today's post is dedicated to Typescript Generics. As always I leave the official docu [here].(https://www.typescriptlang.org/docs/handbook/2/generics.html).

## Intro

A generic TypeScript is a tool that allows us to create functions, classes or interfaces that work with different types of data.
The jewel of this tool: writing more flexible and reusable code.

We can create functions that accept for example arrays of string type, simple objects, complex objects, etc etc. Or even to create classes that can manipulate any type of data that we pass to them.

It is important that we keep in mind that, if we are working only with a single data type, we are going to define it directly and that's it, there is no need to apply generics for everything, that would only complicate our code and we do not want that, _KISS_
![enter image description here](https://media.designrush.com/agencies/262188/conversions/.K.I.S.S.-Software-logo-profile.jpg)

## Problem

To better understand what a TypeScript Generic solves, let's look at the following problem:

```typescript
function addTodo(item: string): void {
  todoList.push({ taskId: id++, task: item, done: false });
}

function addTodoNumber(item: number): void {
  todoList.push({ taskId: id++, task: item, done: false });
}
```

In the example, we can see that we have 2 methods ALMOST the same, the only thing that makes them different is that the parameter that we pass is string in the first one and number in the second one.
And not only that, but having those 2 methods, we are going against the **DRY: Don't-Repeat-Yourself** principle, according to which "all knowledge or logic must have a unique and unequivocal representation within a system".
![DRY Principle](https://solopez.github.io/assets/img/dry.jpg)

So, how can we do, to unify and adapt both methods so that you can have the power to manipulate both types?

First answer that comes to our minds: ANY

![enter image description here](https://i.pinimg.com/736x/11/81/07/118107c3d36f9e5fd9481fce48dd56df.jpg)

```typescript
function addTodo(item: any): void {
  todoList.push({ taskId: id++, task: item, done: false });
}
```

While we can say that with the evil and forbidden any, we are applying the DRY principle, we are also generating a new problem: that method accepts anything, which means that we will not **control** the types we accept or return. Not to mention that we are losing the powers and benefits of typing our code.
So let's apply DRY and type-safe, to make sure we still control the types of data accepted/returned. **TS Generics**, to the rescue!
![enter image description here](https://www.meme-arsenal.com/memes/dbbb12279c0e4e7b07c6d822efab1d30.jpg)

## TypeScript Generics: Functions

```typescript
function addTodo<Type>(item: Type): void {
  todoList.push({ taskId: id++, task: item, done: false });
}
```

Let's analyze a little bit the solution that we apply with TS Generic. The `<Type>`, is simply a placeholder that is going to be replaced by the type when we execute the function, ensuring making it type-safe.
For example: `addAll<string>('Sama');`.
By declaring the string, we avoid the possibility of passing a param that is not a string.

We can also set our function to already have the default type, so that we don't have to specify it every time we invoke it, in this way:

```typescript
function addTodo<Type = string>(item: Type): void {
  todoList.push({ taskId: id++, task: item, done: false });
}
```

In the examples we saw a param, but we could also scale this Generic to work with 2 params, like this:

```typescript
function addTodo<T, S>(item: T, status: S): void {
  todoList.push({ taskId: id++, task: item, done: status });
}
```

We can pass multiple parameters as placeholders `<T,S>` in the definition of our Generic function, and then specify them when we invoke:

```typescript
addTodo<string, boolean>("Learn TypeScript", true);
```

## TypeScript Generics: Clases

We can create not only Generics functions but also classes. For example:

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

The most important thing to remember is that the difference between classes and _Generics_ functions is that in a Generic **function**, we take the type parameter at the point of execution `addTodo<string>('Holis')`, while in the Generic **class**, we take the type parameter at the time of instantiation `new Todo<TodoItem>();`.

## Constraints

We can restrict our functions and classes in cases where we do not want to accept a particular type.
For example, we might want to accept strings and numbers, but NOT booleans.
In this case we can do it using the `extends` word as follows:

```typescript
function addTodo<Type extends string | number>(item: Type): void {
  todoList.push({ taskId: id++, task: item, done: false });
}
```

In this way we are applying controlling and restricting the types in order to limit and avoid possible errors (due to unsupported types) within our implementations.

## Conclusion

We can say then, that the use of generics in TypeScript is a powerful tool that allows us to write flexible and reusable code. By using generics, we can define functions, classes, interfaces that accept different data types as arguments and generate code that works with those types in a safe and efficient way.

We simplify development and can also improve code quality and reduce the number of errors.
In addition, the use of generics also improves the readability of the code by making it more explicit and easier to understand.

References and further reading [here](https://blog.openreplay.com/keeping-your-typescript-code-dry-with-generics/)

Happy coding!

![enter image description here](https://www.digitalmomblog.com/wp-content/uploads/2019/04/happy-friday-meme-work-from-home.jpeg)
