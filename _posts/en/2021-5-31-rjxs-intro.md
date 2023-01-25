---
date: 2021-05-31 15:00:40
layout: post
title: RxJS!
description: Intro!
image: "../assets/img/rxjs_pic.png"
category: CODE
language: en
tags:
  - coding
  - rxjs
  - humor
author: sol lopez
---

# RxJS

How are you doing? In today's post I want us to start to see and share full concepts about this library.

I think this post will be the first of many more ... and yes! RxJS is worthy and deserving of a good space, as I think it is a topic that more than once has made us want to cry. ![enter image description here](https://external-preview.redd.it/N_bB0Oszfuks9wLTax6viC4Hh9FzHgpMcpYiuUHoQQU.jpg?auto=webp&s=22d6a707521ffee7ea809ec405a10477ee7bd2b8)
![enter image description here](https://pics.me.me/programming-javascript-lie-down-try-not-to-cry-cry-a-38119635.png)

Well, and yes, the 2 memes were necessary, we suffered a lot!
Anyway, I'll put it in Creole, something like a version of "[te lo resumo asi nomas](https://www.youtube.com/channel/UCw7Bz6EHxlnOoBUBlJZCWCw)" but to rub elbows? And... hopefully yes, I'll keep insisting on super short posts that make you want to read.
The official RxJS guide [here](https://rxjs.dev).
Well here we go!

## What is it?

![enter image description here](data:image/jpeg;base64,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)
It's a reactive programming library for JS, in Creole, everything we have always done to work with asynchrony (future data, that doesn't exist yet) has been a huge hassle to handle in our apps (promises and among others), and this will come to save us. So no matter what framework you are developing in, there is no excuse! I'm not going to lie to you, there is a lot of stuff going around and it's just because of this crazy thing. So let's try to win the battle.

## Introduction

Let's imagine that we have a lot of information that we must process and show in our app, a collection (an array so to speak), we process it a little bit to show it in some HTML and that's it. If we are talking about something synchronous, something like this in our front end code:

    const array = [
        {name: 'sol', lastName: 'lopez'},
        {name: 'dario', lastName: 'barassi'}
    ]

we have no problem, because we have this collection static and always available in our app to have a h1 with the name of the best one
![enter image description here](https://fotos.perfil.com/2021/04/21/cropped/1200/1200/center/dario-barassi-2104-1161980.jpg)

NOW the issue is when we talk about asynchrony, and it is when, for example, we make use of some external service that has to bring us info and we have to wait for that info to process and display it somewhere in our app.

That is exactly the job that our little friend RxJS comes to solve. In fact, if we want to give certain form to our sync or static array that we would do? we would use some operator (of the same Array.prototype) some map, filter, reduce blah blah blah.......

Well, exactly that also comes to solve this lib. We will be able to use many operators, including map, filter, reduce for these asynchronous arrays/future arrays that do not exist yet.

We call this flow of data and future collections streaming, as if it were Netflix, data will be arriving at different times and at different rates, in fact we will not even know the amount of them and our app should know how to manage and handle that data when it arrives to our app. And in fact, this way of representing those streamings is through marbles (marble). But don't worry, we'll see that later.

To install the lib is super easy, the steps [here](https://rxjs.dev/guide/installation)

## Observable

Now, with this mini intro in mind, we have to start talking about observables and other related concepts, to understand how we are going to deal with this asynchronous future data.

The observable then represents the idea of a collection of future data/values/events whatever you want to call it, that can be invoked.

As any function, by itself it does nothing if you don't invoke it, so if you don't **subscribe** to the observable, nothing will happen!

You can also CREATE observables, that is, "future data" to process and manipulate.
If we follow the previous example, having an array with first and last names, if we use the **from** operator or the **of** operator we create our observable and then we subscribe to see our data:

    import { from } from 'rxjs';

    import { from } from 'rxjs';

    const observable = from([{name: 'sol', lastName: 'lopez'}, {name: 'dario', lastName: 'barassi'}]);

    const subscribe = observable.subscribe(val => console.log(val));

    const observable2 = of([{name: 'sol', lastName: 'lopez'}, {name: 'dario', lastName: 'barassi'}]);

    const subscribe2 = observable.subscribe(val => console.log(val));

Already with that we would be using our first operators that this library gives us (of type **Creation**, because we are creating the observable).
Of course there are several more operators, of this type and also of other categories that we will begin to see in the next posts.

## Observer and Subscription

**_Subscription_** indicates the **execution** of an observable. As we said just now, the observables are **_lazy_**, yes tremendous bums!!!! so if we don't subscribe to them, forget it, they don't even emit a sandwich.
![enter image description here](https://pbs.twimg.com/media/Etev4m4WgAE2N8Z.jpg)

**_Observer_** is an object that **reacts** to the values delivered by the observable.

For the sake of clarity, it all boils down to:

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

## Operators

As we were talking about before the of operator, the from operator, and we're going to have a few more that we're going to see here, but what is it? Well as everything in JS, it is a **function** yes, that takes an observable as **input** and generates **another** observable as **output**.

**Classification**: creative, transform, filtering, conditional, combinational, multicast, error handling, and utility. (yep, in the next posts we are going to see these crazy little ones)
