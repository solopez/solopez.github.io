---
date: 2020-08-12 17:28:40
layout: post
title: Angular Universal
description: Server side rendering world
image: "../assets/img/universal.jpg"
category: CODE
language: en
tags:
  - angular
  - universal
  - ssr
  - humor
author: sol lopez
---

Hello, how are you? Today I want to dedicate this post to our friend Angular Universal. If you already worked with Angular Universal and you are thinking to migrate, or if you want to know what it is to decide whether or not to apply it in your app orooooooo if you are making you renegade because they tell you it's easy but it's not soooo soooo this post is for you!

![enter image description here](https://i.imgflip.com/433lvu.jpg)

## What it is

Angular Universal is the technology that allows us to run our Angular apps in server-side Angular, SSR (_Server Side Rendering_). Yes, you read that right. We are used all our lives (all our lives? what's wrong with it?) to build and serve applications on the client side (Javascript, with or without your favorite framework). BUT, Angular Universal promises us to build our application and serve it directly from the server.

**How?
Well basically it helps us to implement certain features to apply in our app and we can **prerender\*\*, that is, we generate static HTML with all the data ready (for example with the responses of the services already mocketed and other herbs) and that we serve it in one!

\*\*What do we achieve with this?
Our application will have high speed in the initial loading of those pages and routes where we apply the prerendering and static HTML. As we are already serving the HTML, we are not waiting for the execution of calls to services, or their responses, no promises or observables, nothing at all, HTML and bye-bye).

**What do we do with dynamic data?
You don't have to worry about that, because once you load the app, you see the Angular Universal prerendering but then in case of an event, ANGULAR **takes full control\*\* and your app continues working as usual (with calls to services, dynamic content, data binding, dynamic loading and rendering, everything normal as usual).
You can choose whether to only prerender the index.html of the initial load of your app, and also choose which paths you want to have that prerendering and which not.

## Fresh Starter Configuration

![enter image description here](https://i.pinimg.com/474x/1e/13/69/1e136976ac0fcb96775cf21957c5c6f9.jpg)
If you want to build an app from scratch in Angular and put Universal, or if you already have an Angular app but never had Universal, the configuration should be simple and we detail it here. If you are complaining about other migrations, go straight to the next section!

Well let's start with the initial command

    ng add @nguniversal/express-engine

This will generate a few base configuration files of our server to build our SSR app.
Once finished, it takes the configuration of our angular cli to configure the server based on our app. To run it we use

    npm run dev:ssr

If we open our local [http://localhost:4200](http://localhost:4200/) we will see our usual app, BUT let's see if the magic is there, we open the source code (ctrl + u) and check the HTML. If we can see it is that it works, in fact the newest versions of universal add a comment: _This page was prerendered with Angular Universal_.
What is the difference?
If you look at the source code of a normal Angular app you will see only the meta tags, scripts, links etc BUT you will see the

    <sc-root></sc-root>

where the Angular app rests (?) so you won't see anything.
If we look at the source code of an app with Angular Universal, we will be able to see what is inside the root, we will see body, divs, span, p, etc all our HTML content we will be able to see it!

## Advanced Configuration

![enter image description here](https://static01.nyt.com/images/2016/08/05/us/05onfire1_xp/05onfire1_xp-articleLarge-v2.jpg?quality=75&auto=webp&disable=upscale)

In this section I want to detail some tips and tricks to get Universal working with the arrival of **Ivy**, the new Angular 9 compiling and rendering engine. If we have our Angular app with Universal installed and configured BUT we are going to migrate to another version of Angular (9 or more) things start to fail and the Universal migration is not so easy.
In fact, the Universal commands you were using before are going to fail.

To go a little deeper, the problem of all this lies in the compatibility of migration, from Angular 9 the **Ivy** compiler is introduced, and this affects Universal too, especially in the way it searches and compiles the modules, which is not the same as before.
So, the **_way_** in which we were implementing Universal changed.
If you are in Angular 8 or earlier, the way to implement Universal was more complex and more or less like this, you had _server.ts_ and _prerender.ts_ files that you could tune a little by hand, and also you had your webpack file with your config and your command to get the server to raise and prerender everything accordingly.

Now, from Angular 9 onwards, Universal needs to adapt to **Ivy**, so we will probably have compatibility issues. So...

There is no longer a prerender.ts, nor is there a custom webpack configuration. All this is delegated and who is in charge now is the package we installed from Universal BUT we need to adapt and confirm some configurations so that the changes really take effect and we can continue with Universal in our migrated app.

Here are the most important points, check all of this to get it running

![enter image description here](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTc5bACPeIWofEypyqv3XASoCcZQsbxQVbg1w&usqp=CAU)

**1-** In **app.server.module.ts** before you had this

          @NgModule({
           imports: [
                AppModule,
                ServerModule,
                ModuleMapLoaderModule

Now it looks like this:

          @NgModule({
           imports: [
                AppModule,
                ServerModule

And also delete the import

     import { ModuleMapLoaderModule } from '@nguniversal/module-map-ngfactory-loader';

Yes, we blow up the **ModuleMapLoaderModule**, because it is no longer Ivy compatible.

**2-** The **server.ts** that generates you new (with the _nguniversal_ command) has most of the changes done, but you will need to add this if you have errors due to window and/or document issue

    const domino = require('domino');
    const template = join(process.cwd(), 'dist/browser', 'index.html').toString();
    const win = domino.createWindow(template);
    global['window'] = win;
    global['document'] = win.document;

**3-** In **main.server.ts** you need to delete the following

    export { provideModuleMap } from '@nguniversal/module-map-ngfactory-loader';

as we said before, the moduleMapper is no longer compatible with Ivy.

By the way check and confirm that in this file you have this line that works with the new module render:

    export { renderModule, renderModuleFactory } from '@angular/platform-server';

**4-** In **tsconfig.server.json** you have to keep:

    "files": [
     "src/main.server.ts",
     "server.ts"

**5-** En Angular cli, verificar la config del serve local
**"serve-ssr"**

    "serve-ssr": {
    "builder": "@nguniversal/builders:ssr-dev-server",
    "options": {
    "browserTarget": "{{APP_NAME}}:build", //este va a tomar las configs de nuestro objeto build
    "serverTarget": "{{APP_NAME}}:server" //este tomara la config de nuestro objeto server que veremos mas abajo
    },
    "configurations": {
        "production": {
    	    "browserTarget": "{{APP_NAME}}:build:production",
    	    "serverTarget": "{{APP_NAME}}:server:production"
        }
    }

Note: For each environment you need to adapt the object configurations according to your environments and thus have 2, 3 or as many environment objects as you have, for example:\* \*.

    "production": {
        "browserTarget": "{{APP_NAME}}:build:{{ENVIRONMENT_BUILD_OBJECT}}",
        "serverTarget": "{{APP_NAME}}:server:{{ENVIRONMENT_BUILD_OBJECT}}"
    }

**6-** In Angular cli, verify the **"server "** configuration.

    "server": {
    "builder": "@angular-devkit/build-angular:server",
    "options": {
    "outputPath": "dist/server",
    "main": "{{APP_NAME}}/server.ts",
    "tsConfig": "{{APP_NAME}}/tsconfig.server.json"
    },
    "configurations": {
    "dev": {
    "fileReplacements": [
    {
    "replace": "src/environments/environment.ts",
    "with": "src/environments/environment.dev.ts"
    }
    ],
    "sourceMap": true,
    "optimization": true
    ...
    },

**7-** In Angular cli, verify **"prerender "** config.

    "prerender": {
    "builder":"@nguniversal/builders:prerender",
    "options": {
        "browserTarget":"{{APP_NAME}}:build:production",
        "serverTarget":"{{APP_NAME}}:server:production",
        "routes": [
    	    "/"
        ]
    },
    "configurations": {
    "dev": {
        "browserTarget":"{{APP_NAME}}:build:{{TU_ENVIRONMENT}}",
        "serverTarget":"{{APP_NAME}}:server:{{TU_ENVIRONMENT}}",
        "routes": [
    	    "/"
        ]
    },

**8-** If you get some typing problems or errors when running server.ts, you can try these versions of universal and express which currently work without errors:

    "@nguniversal/builders":"^10.0.0-rc.1",
    "@types/express": "^4.17.0"

## Deploys

To deploy SSR you will need to run the SSR build, SSR server and also the prerender commands.

If you have more than one environment configured, you need to add in the config of those operations (build, server and prerender) mentioned above for each environment, and in the commands make use of those variables to deploy the corresponding build.

If you can move the files left in _dist/browser_ to the folder where your app is deployed, that's all. In case you can't, you will have to run node dist/server/main.js on a node server to get it up.

Finally, in case you need your build (SSR or not) to compile and deploy to an x folder, remember that you can configure it in Angular cli like this:

    "architect": {
      "build": {
        "options": {
          "baseHref":"/app_folder/",
          "deployUrl":"/app_folder/",

![enter image description here](https://i.pinimg.com/originals/47/96/9a/47969afc2fc6f92c18c5b075b7a0fabd.jpg)

## Conclusion

If we have an Angular app and we want it to load fast the first page load and/or the loading of certain specific paths, that we give priority to SEO and that Google indexes our app correctly, **Angular Universal** is the option!
Angular Universal is easy mmmmmm
![enter image description here](https://www.lifeder.com/wp-content/uploads/2018/06/no-lo-s%C3%A9-rick.jpg)

If you've never implemented it, you probably did, because it practically automated everything that used to be manual. But, if you already had one and you got the Ivy bug, you have to migrate and configure by hand everything that the migration could not do automatically.

It can also happen that you have more than one application (project type) running in the same repository, if you configure the variables mentioned above, with the names of those projects in app_name and the environments you need, all the solutions apply to this scenario as well.
During this migration of compatibility between Universal and Ivy, I did not find so much documentation so I hope this post will serve as a guide.

![enter image description here](data:image/jpeg;base64,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)

## Recommended readings

[Angular Universal Oficial](https://angular.io/guide/universal)

[Blog Angular University](https://blog.angular-university.io/angular-universal/)

[NgDevelop](https://www.ngdevelop.tech/prerender-angular-application-using-angular-universal-prerenderer/)

[Blog Universal y Angular 9](https://medium.com/@mugan86/server-side-rendering-con-angular-universal-9-9fdf33d03f4d)

By Sol López, frontend, rosarina, drummer, rock & metal.
