---
date: 2023-02-03 17:00:00
layout: post
title: Dependency Injection
description: Theory and samples!
language: en
image: "../assets/img/di.jpg"
category: CODE
tags:
  - coding
  - providers
  - dependency injection
  - humor
author: sol lopez
---

Happy Friday! Today's post is dedicated to dependency injection in Angular and how we can provide these dependencies in modules and components. As usual the official docu by [here](https://angular.io/guide/providers)

## Injecting a service in root

Let's assume the following service:

```typescript
import { Injectable } from "@angular/core";

@Injectable({
  providedIn: "root",
})
export class UserService {}
```

When we use the `providedIn: 'root'` , it means that we will be able to inject this service anywhere in our app. And also, that the instance of it is unique and shared ([singleton](https://angular.io/guide/singleton-services)), for those who invoke the service.

## Injecting a service in a module

We can also inject a service at the module level like this:

```typescript
import { Injectable } from "@angular/core";
import { UserModule } from "./user.module";

@Injectable({
  providedIn: UserModule,
})
export class UserService {}
```

Or also like this

```typescript
import { NgModule } from "@angular/core";

import { UserService } from "./user.service";

@NgModule({
  providers: [UserService],
})
export class UserModule {}
```

While both ways are valid, the first option is the most recommended because it enables **tree-shaking** (which allows Angular to optimize the app by removing the service from the already compiled app if it is not used, more info [here](https://angular.io/guide/architecture-services#introduction-to-services-and-dependency-injection)).

## Instances

In Angular there are two types of module loading, eagerly loading and lazy loading (if you want to review lazy modules I leave you the [official link](https://angular.io/guide/lazy-loading-ngmodules))
In the eagerly, the modules are loaded when the app starts, no matter what, while the lazy loading works on demand, under a condition, that is, if you don't navigate to a certain path for example, those modules are not loaded.

So, for the case of an app that loads eagerly, all the providers of the modules that are not lazy are prepared and made available.

But this works differently for the lazy case. When Angular loads a lazy module, it creates a new **injector**, which is just a child of the root injector.

![enter image description here](https://i.pinimg.com/originals/78/8f/83/788f83c6a233753079a45fdc4a45cbf4.jpg)

Let's imagine a tree of injectors. We have the root injector and then the child injectors for **each** lazy module. These child injectors will be in charge of preparing and making available the providers of their corresponding lazy module. And each component of that lazy module, will have its own local instance of the child services indicated in the providers of it.

Note\_: This could be heavy if we talk about injector hierarchies, but we will leave it for another post.

Therefore we highlight on the one hand, the single and shared instance ([singleton](https://angular.io/guide/singleton-services)) of a service (for eagerly modules), and on the other hand, that each lazy module has its own instance of the service as we see here:

![enter image description here](https://angular.io/generated/images/guide/providers/any-provider.svg)

## Scoping providers in components

It is possible to limit the scope of the provider by adding the service we want to limit to the **component providers array**.
Component providers and _NgModule_ providers are independent of each other.

This method to inject in the component, serves more than anything when we want in a module (eagerly, not lazy) to inject a service only for itself.
That is to say, injecting a service in the component limits the service only to that component and its descendants.

```typescript
    @Component({
      /* . . . */
      providers: [UserService]
    })
```

Happy coding!
![enter image description here](https://i.imgflip.com/1z6225.jpg)
