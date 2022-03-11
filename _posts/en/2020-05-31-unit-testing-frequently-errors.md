---
date: 2020-05-31 12:26:40
layout: post
title: Jasmine unit testing!
description: Frequent errors
image: '../assets/img/karma.jpg'
category: test
language: en
tags:
  - jasmine
  - humor
  - karma
  - errors
author: sol lopez

---
# Building unit tests with Jasmine!
## Frequent errors

Hi friends! Today I would like to share with you the most frequent errors that usually happen as we write our unit tests and their respective solutions.
While most are fairly intuitive, some are kind of
![enter image description here](https://i.pinimg.com/736x/d6/3e/dd/d63edd9af879f866baea5e3c5b506959.jpg)

I want to aim at those this time and I also mention some intuitive level "medium", maybe it will be useful to have them at hand as a kind of machete, I don't know, I'm not big yet I'll wait
```
Uncaught Error: Cannot find module "tslib".
    at webpackEmptyContext (VM2488 main.js:11)
```
and it goes on and on, the error is quite long but impossible to know exactly what is wrong in our code beforehand, so when this happens we are only interested in the **cannot find module blah blah**. The solution is simpler than it seems, we just have to look at our @imports of the .spec in question that we are running, and see that the imports are as *pure* as possible, that they do not have a compiler/operators/internal or routes rare extensive, for example:
```
import { Type } from '@angular/compiler/src/core';
``` 
Solucion:
```
import { Injectable, Type } from '@angular/core';
```
This error usually happens because we import automatically using our IDE (VSCode <3) and well, the IDE finds similarities and imports it, but it's not the right path so that jasmine doesn't explode :)

Other times we see other errors like "cannot read property blah blah of undefined" or "cannot read property subscribe of undefined".
These are more intuitive, basically we have to mock, the art of mocking...

![enter image description here](/assets/img/magic.jpg)


For the first error, we look at our ngOnInit if we have data that we have not mocked in the spec, if it is not there we should look at the data that the component may be receiving through @Inputs, and also look at the component template if is trying to render N data that we haven't mocked yet in our .spec.
For the second error, it is similar to the previous one, only in addition, the data that our component is waiting to manipulate/render has to be of type **Observable**, so our mock must respect that, we can do an of({mock : 'mock'}) and we have our object of type obs which can be subscribed to in the .spec.

Another error that I encounter a lot is:
```
Uncaught Error: Uncaught (in promise): Error: No value accessor for form control
```
It can be something intuitive, and it tells us that we have a form in our component, but that the test cannot access the control. For example, if we have an input or a select cannot find it in our form, this may be because we are mocking it elsewhere or because we have to import the module if it is a select custom component.

Another frequent error is when we run our test suite, for example, using fdescribe and the tests pass, but when we remove fdescribe and run all the tests of the app they start to fail, and not only that, but sometimes some fail, and other times others. This usually indicates that we have synchrony errors (async tests perhaps) and dependency injection problems, that is why the errors are mutating and many times we have a hard time finding which one we really need to solve. To find the solution it is best to use debug mode and review our import and declaration chain which could be unnecessarily long, making our tests depend on each other. The ideal is **isolationnnn** so let's try to avoid this as much as possible, let's only test our components, don't declare and import unnecessarily, this way we will not only optimize our tests but also make sure to test each component in isolation.
For this, we can make use of the schemas: [CUSTOM_ELEMENTS_SCHEMA], which is used to indicate that we have custom elements and components in our component and we do not need to import each one.
Let's avoid the [NO_ERRORS_SCHEMA], this only serves to hide errors and indicates that we can have any vegetable in our templates and the test will pass OK, without resolving them.

Usually when we do ng test --watch we can already run with Karma for example the tests and see the errors. If that's not enough, it's possible to open tests from localhost:9876 usually and turn on debug mode. Many times when consologueing we also quickly realize if the problem is merely with the component or with a method that is not being mocked at all or if it does not even access it, etc.

By Sol López, frontend, rosarina, drummer, rock & metal.