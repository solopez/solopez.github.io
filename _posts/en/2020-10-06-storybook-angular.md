---
date: 2020-10-06 17:30:40
layout: post
title: Storybook
description: UI DevTool!
image: "../assets/img/storybook.png"
category: CODE
language: en
tags:
  - storybook
  - angular
  - humor
author: sol lopez
---

Helloooo how are you? Today I bring you a little jewel, yeeeeee! It is [Storybook](https://storybook.js.org/docs/react/get-started/introduction) !!!!

## What is it

As always the idea is to summarize, so here goes!
Storybook is another tool for frontend/UI development.
It helps us to develop with more speed our components.
Basically it allows us to develop and keep our visual components isolated! Cool, isn't it?

![enter image description here](https://i.pinimg.com/originals/e5/39/d3/e539d3bdfcb1124ebf599a7d37054947.jpg)

## Installation and Configuration

The cool thing about Storybook is its compatibility with Angular, React, Vue... so no excuses, go for it!

As always, I'm going to focus on the installation and configuration for our beloved Angular! :)

To install we go with

     npx -p @storybook/cli sb init --type angular

This installation will create a .storybook folder in our root directory, with some _stories_ and small base components so we can see how everything works. It will also generate some commands in our package.json to make use of the tool.

Watch out for the louse! With the latest version to date of Storybook (6), we may have compatibility problems with the **core-js** package, one of the workarounds is to upgrade the core-js version to 3.

Other alternatives [here](https://github.com/storybookjs/storybook/issues/11255)

![enter image description here](data:image/jpeg;base64,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)

## Compilation and use

Once everything is installed, we send the magic with

    npm run storybook

We will get something like this in chrome http://localhost:6006/ with all the base.

![enter image description here](https://admin.indepth.dev/content/images/2019/08/storybook-example.png)

Now that we have everything ready, the only thing we have to do, is to create the stories for our components!

The stories are nothing more than files named as ourcomponent.stories.ts, where we are going to export on the one hand, the configuration and dependencies that we need to instantiate our component, and on the other hand, the constants that we want to make use of our component in different situations, parameters and contexts.

This will be easier to see with an example, here is a simple template for our first story:

    import { moduleMetadata } from '@storybook/angular';
    import { MyComponent } from './my-component.component';


    export default {
      title: 'MyComponent',
      decorators: [moduleMetadata({
        imports: [],
        declarations: [MyComponent],
        entryComponents: [MyComponent]
      })]
    };

    export const Holis = () => ({
      template: `
        <my-component></my-component>
    `});

We save, and Storybook will automatically refresh our browser to reflect the changes.

Later we can grow the story of our component, adding new constants to see how our component behaves to certain parameters and events.

## Advantages

One of the reasons why storybook is chosen is because it not only helps us to create our app with greater speed, but also allows us to give us a quick visualization of the components we have in a repo, let alone if we work in a monorepo, where the app grows and grows and we do not even know that there is! So it helps us to avoid duplication of code and / or components, even when we create new ones it gives us some information so we can develop thinking in scale.

Another very cool advantage is that it helps us to prevent bugs. When something breaks, we can quickly know if the component is the one who needs the fix or if there are problems in the implementation of the component/context.

We can also highlight as an advantage that between developers and designers we can improve coordination and communication by having this tool, generating a unified design system right here.

Clearly there are many other advantages, in the official link that I left above you can see them, and if you dare the truth is that you invest little time to give it a try and you will see that it's great!

## Conclusion

In summary, Storybook not only allows us to manage our visual components, but also screens, data, testing, complex features, always in the contexts that we decide to define them.

BONUSSSSSSS! Yes, having Storybook we can go further and implement Chromatic, BackStopJS and other tools of choice for testing and visual regression.

![enter image description here](https://ep01.epimg.net/verne/imagenes/2019/05/20/articulo/1558347754_694065_1558348027_noticia_normal.jpg)

Seeing all these advantages I invite you to give it a try.

Happy cooooooding!

By Sol López, frontend, rosarina, drummer, rock & metal.
