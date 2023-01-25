---
date: 2021-09-15 15:00:40
layout: post
title: Angular 11!
description: Angular 11 migration!
image: "../assets/img/angular11.png"
category: CODE
language: en
tags:
  - coding
  - migration
  - humor
author: sol lopez
---

# Migration to Angular 11

How are you doing? Recently I had to do some Angular migrations, so I thought it could be useful and interesting for those who must carry out migrations.
Here are the possible errors and their solutions
![enter image description here](https://www.memecreator.org/static/images/memes/5203791.jpg)
Angular is updated frequently [see roadmap](https://angular.io/guide/roadmap) and in order not to lose pace, we must update our code in each version.
Today's post is dedicated to a specific migration from Angular 10 to Angular 11.

## Guide

As a guide we can use the official one [here](https://update.angular.io/?l=3&v=10.2-11.0).
In this particular case, no previous code preparation is required to migrate. So we can start from our repo with the migration command

    ng update @angular/core@11 @angular/cli@11

## PostCSS

If when building (ng build --prod), you encounter the following error:

> [object Object] is not a PostCSS plugin.

You can fix it by manually installing the package that imports the CSS files:

    npm i postcss -D

More info about the issue [here](https://github.com/postcss/autoprefixer/issues/1358).

## allowedNonPeerDependencies

If you have **whitelistedNonPeerDependencies** references in your repo, they are deprecated and you should change them to -> **allowedNonPeerDependencies**.

## Karma

If you are using Karma as test runner in your project, you may need to modify the configuration, since the **coverage-istanbul-reporter** package was deprecated.

We change package:

    npm uninstall karma-coverage-istanbul-report
    npm install karma karma-coverage

And in **karma.conf.js** the following:

We change the

`require('karma-coverage-istanbul-report')`
to ->
`require('karma-coverage')`;

`coverageIstanbulReporter` to -> `coverageReporter`; `coverageIstanbulReporter` to -> `coverageReporter`.
And the parameter `reports` by -> `reporters`.

Reference these changes [here](https://mrjean.be/posts/update-karma-coverage-reporting-for-use-in-angular-11/).

## Tests

And yessssss, if you have been migrating for a while you will have noticed that there are almost always tests to fix :D
This time is no exception BUT you don't have to modify so much either, if you are lucky... A little bit more restrictions in terms of typing and it comes out with
![enter image description here](https://cdn.recetas360.com/wp-content/uploads/2019/07/como-hacer-papas-fritas-de-mcdonals.jpg)

## Core-js

If at the time of building (ng build --prod), you encounter this other error:

> Module not found: Error: Can't resolve 'core-js/es6/reflect' in.
> 'C:\Users' resolve 'core-js/es6/reflect'.

You can look at the angular polyfills, and the imports you have in your project, to go from these:
`import 'core-js/es6/array';`
`import 'core-js/es7/array';`

to these:
`import 'core-js/es/es7/array';`.

Note: we modified only the first part (core-js/es).

If the error persists, you may need to modify the core-js package version. In my case I upgraded from version 2.6.12 to 3.6.5.

## Typescript

If you encounter TS versioning error, you should update it as well. In my case, I upgraded from 3.9.9 to 4.1.5.

    npm i -D typescript@4.1.5

## Bonus!

If you happened to have **@angular-devkit/build-ng-packagr** as a dependency, it was also deprecated and you would only need this one: **@angular-devkit/build-angular**, so you could uninstall it and remove it from the package.json, keeping only the _@angular-devkit/build-angular._.
[package specified here](https://www.npmjs.com/package/@angular-devkit/build-ng-packagr)

Short and to the point post, but I hope it can be useful for you!

![enter image description here](https://pics.me.me/thumb_adios-memecrunch-com-adi%C3%B3s-51915832.png)
