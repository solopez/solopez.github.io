---
date: 2023-01-23 9:00:40
layout: post
title: Typescript decorators!
description: Concepts, theory and simple samples of TS decorators.
language: en
image: "../assets/img/decorators.jpg"
category: CODE
tags:
  - coding
  - typescript
  - decorators
  - humor
author: sol lopez
---

# Typescript Decorators

How are you doing? First post January 2023!
Today's post is dedicated to the TS decorators. As always I'm sharing the official documentation [here](https://www.typescriptlang.org/docs/handbook/decorators.html)

## What are they?

![enter image description here](data:image/jpeg;base64,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)
Functions.
Nothing more and nothing less than functions that we can apply in our classes:

1.  Class
2.  Class Property
3.  Class Method
4.  Class Accessor
5.  Class Method Parameter

Where did they come from? Well, thanks to the class management in TS and ES6, we can now talk about decorators. They are an experimental feature in TS, and in ES they are still in stage 2 [here](https://www.proposals.es/proposals/Decorators)

## Syntax

Let's look at the most basic example of a decorator:

```typescript
function decorator() {
  console.log("I am a decorator!");
}

@Decorator
class A {}
```

## Decorator types

We can implement 5 types of decorators:

1.  Class Decorators
2.  Property Decorators
3.  Method Decorators
4.  Accessor Decorators
5.  Parameter Decorators

Let's see an example where these 5 decorators are reflected:

```typescript
@classDecorator
class User {
  @propertyDecorator
  name: string;

  @methodDecorator
  walk(
    @parameterDecorator
    speed: number
  ) {}

  @accessorDecorator
  get age() {}
}
```

## Decorators Composition

We can apply multiple decorators to the same target. In that case, we will have to take into account the order of evaluation of these compound decorators, similar to the composition of functions in mathematics, to see the order of evaluation [here](https://www.typescriptlang.org/docs/handbook/decorators.html#decorator-factories)
We can decorate on one or multiple lines:

```typescript
    @f @g x

    @f
    @g
    x
```

## Method decorator

Let's take a look at its structure:

```typescript
type MethodDecorator = <T>(
  target: Object,
  propertyKey: string | symbol,
  descriptor: TypedPropertyDescriptor<T>
) => TypedPropertyDescriptor<T> | void;
```

The params it receives:

1.  target: the constructor function of the class or instance.
2.  propertyKey: the name of the property.
3.  descriptor: the property [descriptor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptor), the config of the object.

So, we can say that what differentiates the methods decorators from, for example, the property decortators, in principle, is this param **descriptor**. This descriptor is what will allow us to overwrite the original implementation in order to inject our logic.

### Sample 1:

```typescript
//Decorator
function logger(
  target: any,
  propertyKey: string,
  descriptor: PropertyDescriptor
) {
  const original = descriptor.value;

  descriptor.value = function (...args) {
    console.log("params: ", ...args);
    const result = original.call(this, ...args);
    console.log("result: ", result);
    return result;
  };
}

// method decorator
class C {
  @logger
  add(x: number, y: number) {
    return x + y;
  }
}

const c = new C();
c.add(1, 2);
// -> params: 1, 2
// -> result: 3
```

In this example we see that by applying the @logger decorator to the add() method of the C class, every time we invoke that method, the params and the result of the operation will be logged.

### Sample 2:

Decorator:

```typescript
function enumerable(value: boolean) {
  return function (
    target: any,
    propertyKey: string,
    descriptor: PropertyDescriptor
  ) {
    descriptor.enumerable = value;
  };
}
```

The only thing we do is to modify the enumerable prop of the property descriptor.
We apply the decorator to the method of our class:

```typescript
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }
  @enumerable(false)
  greet() {
    return "Hello, " + this.greeting;
  }
}
```

### Sample 3:

Another case that I personally found very interesting to apply, is for example, to add a cache for some method requests.
In this case, we not only apply the structure and logic that corresponds to the method decorator, but we are also going to combine everything with some rxjs magic to transmit values and store them for a certain amount of time. I share with you a post with the guide to review it and/or implement it [here](https://dev.to/davidecavaliere/rxjs-caching-observables-with-a-decorator-12fe)

## Composition: Parameter + Method decorators

In the example we are going to apply 2 decorators to mark params as required (@required) and to validate the args before invoking the original method (@validate) .

Example of both decorators:

```typescript
import "reflect-metadata";
const requiredMetadataKey = Symbol("required");
function required(
  target: Object,
  propertyKey: string | symbol,
  parameterIndex: number
) {
  let existingRequiredParameters: number[] =
    Reflect.getOwnMetadata(requiredMetadataKey, target, propertyKey) || [];
  existingRequiredParameters.push(parameterIndex);
  Reflect.defineMetadata(
    requiredMetadataKey,
    existingRequiredParameters,
    target,
    propertyKey
  );
}

function validate(
  target: any,
  propertyName: string,
  descriptor: TypedPropertyDescriptor<Function>
) {
  let method = descriptor.value!;
  descriptor.value = function () {
    let requiredParameters: number[] = Reflect.getOwnMetadata(
      requiredMetadataKey,
      target,
      propertyName
    );
    if (requiredParameters) {
      for (let parameterIndex of requiredParameters) {
        if (
          parameterIndex >= arguments.length ||
          arguments[parameterIndex] === undefined
        ) {
          throw new Error("Missing required argument.");
        }
      }
    }
    return method.apply(this, arguments);
  };
}
```

Implementation:

```typescript
class BugReport {
  type = "report";
  title: string;
  constructor(t: string) {
    this.title = t;
  }

  @validate // method decorator
  print(@required verbose: boolean) {
    // param decorator
    if (verbose) {
      return `type: ${this.type}\ntitle: ${this.title}`;
    } else {
      return this.title;
    }
  }
}
```

## Advantages

Decorators help us to improve our code with a declarative, easy to read syntax. With a single line we can apply logic and functions without the need to write additional code.

It is interesting to analyze which cases and scenarios of our projects, may be candidates to implement these decorators, especially when we notice some logic that we can abstract and reuse.

![enter image description here](https://img.memegenerator.net/images/16813474.jpg)

## References

Post and complementary info with more examples [here](https://saul-mirone.github.io/a-complete-guide-to-typescript-decorator/)
Happy coding!

![enter image description here](http://images7.memedroid.com/images/UPLOADED807/5b7ac8533206b.jpeg)
