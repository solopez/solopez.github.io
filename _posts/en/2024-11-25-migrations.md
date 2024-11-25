---
date: 2024-11-25 10:00:00
layout: post
title: Migrando a Angular 15, 16 y 17!
description: Migrando
language: en
image: "../assets/img/ng17.svg"
category: CODE
tags:
  - coding
  - migrating
  - humor
author: sol lopez
---

# Migrating to Angular 15, 16 and 17!
How are you doing? Today's post is dedicated to angular migrations, sharing the news, changes and improvements of these three versions, as to close this 2024. 
I also leave the docu and official guide to migrate and commands [here](https://angular.dev/update-guide).




### **Angular 15**

1.  **Standalone Components (introduction)**:  
    Although in Angular 16 they became the standard, in Angular 15 you could already start using them to create applications without relying on modules (in a somewhat experimental way). It was the first step towards a simpler way of working with Angular. 
If you still haven't seen how the standalone work, I tell you that they come to replace the modules that we used to build before, by independent components (standalone) that already have their own imports and metadata necessary to work by themselves, making that these components can be imported directly into others, without the need to create or belong to any module for that. 
For more info and videos, I recommend to check it [revised](https://v17.angular.io/guide/standalone-components)
    
2.  **Improvements in Material Design**:  
    Angular Material received updates to align with Material Design 3 guidelines. New components and visual improvements were included.
    
3.  **Directives as standalone**:  
    We can now declare directives and pipes as standalone, making them independent of NgModules, just like components.
Non merci! France issues rare ban for horror film 'Terrifier 3' - the first -18 rating since 2006 | Euronews](https://static.euronews.com/articles/stories/08/78/01/90/1200x675_cmsv2_60ff6e18-32fc-5f9b-a9a2-61b32e94caa0-8780190.jpg)
    
4.  **Router improvements**:  
    The router became more powerful, with improved support for routing configurations and dynamic data handling.
    
5.  **Improved TypeScript support**:  
    Support for TypeScript 4.8, allowing to take advantage of modern language features.
    
6.  **Optimized performance**:  
    Angular 15 included several internal improvements to make applications faster and lighter.


----------

### **Angular 16**

1.  **Standalone Components as standard:  
    We no longer need modules (NgModules) to work. Everything is more direct (and not so experimental).
    
2.  **Signals**:  
    Introduction of a new way of handling reactive data that is simple, efficient and predictable. If you haven't seen or worked with signals yet, I recommend you to have a look around [here](https://angular.dev/guide/signals)
    
3.  **Improved SSR (Hydration)**:  
    More efficiency by combining the server's HTML with the browser. This speeds up the apps.
    Meme Drunk Baby - when they tell me I have to hydrate - 19445555](https://cdn.memegenerator.es/descargar/19445555)
    
4.  **More flexible router**:  
    New APIs for working with dynamic routes and better handling of components.
    
5.  **Improved performance**:  
    Optimization in how views are rendered and updated.

    

----------

### **Angular 17**

1.  **Signals integrated in more parts of the framework**:  
    They are now better connected with other elements such as forms and router.
    For example, before we had to subscribe to the observable of the form control to implement logic and unsubscribe to avoid leaks, now, with signals in the form natively, we no longer need to worry about that or subscribe.
    Terrifier 3: What you need to know before watching a horror movie - Observatório do Cinema](https://media.tenor.com/iHa8Q3BQsYgAAAAe/terrifier-clown-meme.png)
    
2.  **Simpler and faster tests:  
    The testing APIs were optimized to make everything easier and faster.
    
3.  **TypeScript upgrade**:  
    Support for the latest versions of TypeScript, with new features. We are talking about [typescript 5.x.x](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-5-0.html) and just in case I share the [versioning matrix](https://angular.dev/reference/versions) as well. 

    
4.  **Simplified policies:  
    Creating directives is faster, especially for basic cases.
    
5.  **CLI more efficient**:  
    Command-line tools now generate faster and lighter projects.

### Storybook
If you have Storybook in any of your projects, we have version 8 available to deploy with several enhancements:


📸 Built-in visual testing  
⚛️ React Server Component support  
🎛️ Upgraded Vue and React control autogeneration  
⚡️ Rearchitected Vite support, Vitest testing, and Vite 5 support  
🧪 2-4x faster test builds  
✨ Refreshed desktop UI  
📲 Rebuilt mobile UX  
🙅‍♀️ Removed React dependency for non-React projects

More info and details [here!](https://storybook.js.org/blog/storybook-8/)


Happy coding!



![Horror icons enjoying a beer : r/midjourney](https://preview.redd.it/horror-icons-enjoying-a-beer-v0-s5yqa6o66isb1.jpg?width=640&crop=smart&auto=webp&s=01e8df3068dc16a1d4016371988c1c77809a5e70)
