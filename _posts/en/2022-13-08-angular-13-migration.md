---
date: 2022-07-13 15:00:40
layout: post
title: Angular 13!
description: Angular 13 migration
language: en
image: '../assets/img/angular13.png'
category: CODE
tags:
  - coding
  - migration
  - humor
author: sol lopez
---

# Angular 13 Migration

How are you doing? We are back with a new angular migration!!!

Today's post is dedicated to the experiences during a specific migration from our previous Angular 12 to Angular 13, with news, tips, errors, warnings and their respective fixes to renew us and get it out with fries!

![enter image description here](https://media.makeameme.org/created/Needs-to-upgrade.jpg)

## Guide
 To begin with, let's go to the official guide [here](https://update.angular.io/?l=3&v=12.0-13.0). In this case, coming from version 12, we do not need to apply changes to our code BEFORE executing the command in order to migrate. Therefore, we can start:

    ng update @angular/core@13 @angular/cli@13

Note: add the --force if necessary! So far in every migra it seems to cry out for it!

![enter image description here](https://media.makeameme.org/created/the-force-is-3cdf009ad5.jpg)

Most of the required changes we apply with the command. 
The rest of the possible changes you have to make, will depend as always on the project you are working on and this guide is for those manual changes, here we go!
You will also see differences as to whether you are working on an app, or a publishable library by the type of compilation, which we will see later.

### ModuleWithProviders migration
If you have modules with providers implementing ModuleWithProviders, the schematic may not be able to determine the type, so it is necessary to migrate those that require the type like this:

    @NgModule({…})
    export class MyModule {
      static forRoot(config: SomeConfig): ModuleWithProviders<SomeModule> {
	    return {
	      ngModule: SomeModule,
	      providers: [
	        {provide: SomeConfig, useValue: config }
	      ]
	    };
      }
    }

More info [here](https://angular.io/guide/migration-module-with-providers)!

### Rxjs
![enter image description here](https://miro.medium.com/max/1400/1*ZUENlsi796hIv9TNeqJ3bA.png)
If you were using RxJS v6.x, you must manually install 7.4: 

    npm install rxjs@7.4

For fresh projects and apps in this version of Angular, they will install rxjs 7.4 by default. 
What's new in Rxjs [here](https://rxjs.dev/6-to-7-change-summary)!

Of course this does not end here, there are some breaking changes and some deprecations that can impact your project, usually resolved in a short time. 
Example :

    RxJS 7 allow to call 'next' without parameters (Typescript checks).
    
If you are doing a next in a Subject without params like this:

    const updateSubject = new Subject();
    updateSubject.next();

can be solved by adding the type <void> in the declaration of that Subject:

    private subject$ = new Subject<void>();

More info [here](https://github.com/ReactiveX/rxjs/issues/6324)!

### Compilermode

### Angular library 
![enter image description here](https://miro.medium.com/max/1000/1*rCgtilQLYXaua4FH4vxROg.png)
If you are working on an npm publishable library, you may encounter this error:

    Unsupported private class

> This class is visible to consumers via SomeModule -> SomeComponent,
> but is not exported from the top-level library entrypoint

To solve it, you will have to look for components and modules that are not properly exported in the public_api.ts.

This can happen because with Ivy, it is a requirement that if we want to export a module from a library endpoint, we must manually re-export all the elements involved as well (components, pipes, directives, everything!).
Before with View Engine, this was automatic. But with Ivy we must explicitly do it, remember that Ivy is here to stay and View Engine in this version is officially deprecated.

More info [here](https://stackoverflow.com/questions/60121962/this-class-is-visible-to-consumers-via-somemodule-somecomponent-but-is-not-e)!
Angular libraries official docs [here](https://angular.io/guide/creating-libraries)!

#### Error para Angular library: NG3003: Import cycles would need to be created to compile this component
Also known as:

    One or more import cycles would need to be created to compile this component, which is not supported by the current compiler configuration.
    is used in the template but importing it would create a cycle

If you ran into this cyclic error, it only occurs in **angular library**, if you are not working in a publishable library, you are safe and you earned the direct pass to the next section, get out of here! 
This error could mean a change of low/medium complexity depending on the case, since we must take into account if it is a matter of imports with circular dependencies (low complexity) or if we need to apply refactor (medium complexity not so cheap). 
For example in a case where in certain situations, component A embeds component B, and where component B may embed component A. 
Most likely we will have to refactor if we have the latter case.
The explanation of the error and possible suggestions to fix it from official Angular [here](https://angular.io/errors/NG3003)!

This occurs because of the type of compilation, being either "partial" or "full" in our   
**tsconfig.lib.prod.json.**

Being in a library, we must use "partial" because we need the backward compatibility of consumers with or without Ivy.
In an app (no library), the compilation type will be "full" and you won't see this beautiful error ever.
Now, what if we are working on an Angular library, and we manually modify to "full" compilation mode? Do we cheat the npm publish yes or no?

![enter image description here](https://i.imgflip.com/6mp8ce.jpg)

    ERROR: Trying to publish a package that has been compiled by Ivy in full compilation mode. This is not allowed.
    Please delete and rebuild the package with Ivy partial compilation mode, before attempting to publish.	

The build will tell you yes yes yes and when you run the `npm publish` it will welcome you with that error above... so no, don't even try, compile in `partial` and don't waste valuable time on this.

![enter image description here](data:image/png;base64,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)

Unless you want to super investigate these types of compilation and why, I leave you with this one. [artículo](https://blog.lacolaco.net/2021/02/angular-ivy-library-compilation-design-in-depth-en/) which is very good, with graphics and everything is clear.

### Errors/Warnings
In general and in each new version of Angular, errors and/or warnings are becoming more restrictive in several points but they are also becoming more descriptive, so they could be solved from the same suggestions that they offer us. That is why, I preferred to focus this post to the errors that are not so easy to solve and also to those that take us more time of analysis and investigation for its resolution. 
Remember to always run and compile the production build to exterminate the remaining bugs.

## Storybook
![enter image description here](https://pbs.twimg.com/tweet_video_thumb/FFiP-v7WYAQW2cP.jpg)

If you are using Storybook in your project, there is a great migra also with several manual settings to keep Storybook up to date. The most important thing in this version: We have Angular compiler for storybook, so from our angular.json we are going to leave it configured.
As always I suggest the official Storybook migration guide:

 - From 6.3.x to 6.4.x [here](https://github.com/storybookjs/storybook/blob/next/MIGRATION.md#from-version-63x-to-640)
 - Angular builder and changes for angular 13 [here](https://github.com/storybookjs/storybook/blob/next/MIGRATION.md#sb-angular-builder)

Another issue that happened to me, was one of the problems in storybook compilation, of this style:

    preview.ts is missing from the TypeScript compilation. Please make sure it is in your tsconfig via the 'files' or 'include' property.

So I had to apply changes to the `.storybook/tsconfig.json` for the includes, such as [here](https://github.com/storybookjs/storybook/issues/17039)!

And if you see this: `can only be default-imported using the'allowSyntheticDefaultImports' flag`

You can solve it by adding that flag in the tsconfig of the root project (not storybook like the previous one):

    "allowSyntheticDefaultImports": true,
	
If the compilation problems persist and we see this:

        ```
    UnhandledPromiseRejectionWarning: TypeError: The 'compilation' argument must be an instance of Compilation
    ```

you can check that you don't have the sourceMap on for debugging, in the angular.json it should look like this:


    "sourceMap": false,

More info [here](https://github.com/storybookjs/storybook/discussions/17232)!

If we still see this evil:

    UnhandledPromiseRejectionWarning: TypeError: The 'compilation' argument must be an instance of Compilation
Vamos a tener que revisar y verificar las versiones de webpack de angular y webpack de storybook, para eso seguimos estos pasos:

    1.  `npm ls webpack`
    2.  search for the version of webpack for `@angular-devkit/build-angular`
    3.  `npm install`  exact version at dev dependencies
    4.  `npm dedupe` // WTF? yup, this tries to simplify the package deps tree

More info [here](https://github.com/storybookjs/storybook/issues/16977)!

## Jest
![enter image description here](https://i.ytimg.com/vi/2Y_symiajsc/maxresdefault.jpg)

If you've decided to say goodbye to Jasmine and Karma, and started to delve into the magical world of Jest, here are the necessary adjustments for this version!

![enter image description here](https://www.meme-arsenal.com/memes/1622805b4aa6884f82677b8d3ea81568.jpg)

To begin with, in my experience I migrated all of Jest to these new versions:

    "@types/jest": "27.4.1",
    "jest": "^27.4.7",
    "jest-preset-angular": "^11.0.1",
    "ts-jest": "^27.1.2",

To migrate and update our jest.config.js by npm command we execute: 

    npx ts-jest config:migrate jest.config.js

Other ways [here](https://kulshekhar.github.io/ts-jest/docs/migration/):

I've seen this one:

`Need to call TestBed.initTestEnvironment() first`

and this other one too:

    Zone is needed for the waitForAsync() test helper but could not be found. Please make sure that your environment includes zone.js

Both fixed at **test.ts** like this:

```javascript
import  'jest-preset-angular';
import  'zone.js';
import  'zone.js/testing';
import { TestBed } from "@angular/core/testing";
import { BrowserDynamicTestingModule, platformBrowserDynamicTesting } from "@angular/platform-browser-dynamic/testing";

TestBed.initTestEnvironment(BrowserDynamicTestingModule, platformBrowserDynamicTesting());
```
More info [here](https://stackoverflow.com/questions/65397145/error-need-to-call-testbed-inittestenvironment-first)!

Some changes may only affect you depending on the version of Jest and jest-preset-angular you are currently using, just in case you check them out [here](https://thymikee.github.io/jest-preset-angular/docs/guides/angular-13+/).

If you see this:

    [Package subpath './src/ngtsc/reflection' is not defined by "exports" in /node_modules/@angular/compiler-cli/package.json](https://stackoverflow.com/questions/70306517/package-subpath-src-ngtsc-reflection-is-not-defined-by-exports-in-node-mo)

You could check if the jest versions need another change as they indicate [here](https://stackoverflow.com/questions/70306517/package-subpath-src-ngtsc-reflection-is-not-defined-by-exports-in-node-mo).


## Advantages and changes in this version
![enter image description here](https://res.cloudinary.com/practicaldev/image/fetch/s--qTBd8CiH--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3dtliaqu22w3ryjyomkb.jpg)
From [Official Blog](https://blog.angular.io/angular-v13-is-now-available-cce66f7bc296) we have all the data of the changes coming with Angular 13, so I highlight and summarize some very interesting points:

 - Ivy everywhere, View Engine is deprecated.
 - Component API updates: to create dynamic components, the boilerplate was reduced and the component factory resolver we used was deprecated, so we can only use the viewContainerRef and the createComponent for this purpose!
 - End of IE11 support: beautiful news although we can also say something melancholic for some, a few last words: there are many of us who still surely remember when we supported the old IE with those conditionals and I don't know how many hacks in CSS to make it look just like what we wanted, it was not much to ask, but I assure you that it was harder than a Cuphead boss.

 ![enter image description here](https://i.pinimg.com/736x/8b/d7/5c/8bd75c41f1c446bb7139041bb31cc6f3.jpg)

 - Improvements to the Angular CLI: cache build by default!
 - RxJS: now in new apps with Angular 13, RxJS version 7.4 will be installed by default, for manual migration you must install `npm install rxjs@7.4`.
 - TypeScript 4.4: Changes [here](https://devblogs.microsoft.com/typescript/announcing-typescript-4-4/) and breaking changes [here](https://devblogs.microsoft.com/typescript/announcing-typescript-4-4/#breaking-changes)!
 - Improvements in Angular tests: using Jasmine, now improved and a DOM cleanup is done in each test, optimizing them:
 
	`teardown: {  destroyAfterEach: true  }`
   

 - Accessibility issues: if you use Angular Material, there are several accessibility improvements! All the details [here](https://blog.angular.io/improving-angular-components-accessibility-89b8ae904952)
 - Inline Fonts: Since Angular 11 they gave inline support to Google Fonts. In this version 13, they extend the support to Adobe Fonts.
 - Changes and contributions from the community: among them changes to enable/disable validators in dynamic forms, and the restoration of the browser history in the RouterModule by ` { canceledNavigationResolution: 'computed' },`.
 
Happy coding!!!
![enter image description here](https://images-na.ssl-images-amazon.com/images/I/517S+mNAxOL.jpg)
  
