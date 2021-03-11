﻿---
date: 2020-09-21 11:00:40
layout: post
title: NX
description: Dev Tool para monorepos!
image: 'assets/img/nx.jpg'
category: CODE
tags:
  - nx
  - monorepo
  - humor
author: sol lopez

---

# NX en Monorepos

![Loading primavera - Meme subido por loko2530 :) Memedroid](https://images7.memedroid.com/images/UPLOADED115/550445c766c2d.jpeg)

Buenas!! como andan? Felizzz primaveraaaa! Hoy les traigo un nuevo post para presentarles una joyita: [NX](https://nx.dev/).
## Qué es
Bueno para empezar, tenemos las arquitecturas multirepo donde cada app tiene su repo, y las monorepo, donde compartimos el mismo repositorio para distintas apps. 
Como suelo hacer hincapié en desarrollos con Angular, puedo destacar que desde las últimas versiones de Angular, esto ya es posible, tanto la gestión como configuración de monorepos, se pueden construir aplicaciones como *projects* compartiendo código y módulos entre sí. Basta con setear el angular CLI nuestros diferentes proyectos y configuraciones para que puedan buildearse y deployarse independientemente.

NX surge de algunos colaboradores de Angular, y actualmente es usada por Google, Facebook, Microsoft etc en sus proyectos. NX permite esta gestión sin importar si usas Angular, React, etc, es una herramienta que nos ayuda en la gestión de monorepos, brindando una serie de características, ventajas y formas de trabajo diferente.
## NX: Empecemos

Podemos crear un workspace desde cero

    npx create-nx-workspace myorg

 o migrar una aplicación existente con el siguiente comando:

    ng add @nrwl/workspace

*Ojo al piojo*: al momento de migrar sólo podemos tener una sola app configurada en nuestro repo para poder usar este comando de migración.
Si tenemos más de una app en nuestro repo, deberemos migrar manually cada una
![enter image description here](data:image/jpeg;base64,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)

Con NX podemos no sólo presetear la tecnología usada (Angular, React etc) sino también otras configuraciones, por ejemplo nos propone Jest como framework de testing y Cypress para nuestros e2e tests. Esto se puede modificar por otros frameworks y tecnologías de nuestro proyecto, en la config de cli y en los nuevos @schematics que tendremos de ahora en adelante. Todos los pasos para empezar a migrar [acá](https://nx.dev/angular/migration/migration-angular)

*Otra nota super importante:* Si estamos trabajando con una versión de Angular inferior a 10, deberemos igualar la version del paquete  **@nrwl/angular** para utilizar ambas. Por ejemplo tenemos Angular 9 en nuestro proyecto, la version de @nrwl/angular deberá ser la última del 9, en este caso 9.6.0.-

## Qué ventajas ofrece
Algunas ventajas que me gustaría resaltar de esta tecnología es que te brinda ayuda y te ahorra tiempo al momento de verificar y confirmar qué módulos/librerías/apps se vieron **afectados** por nuestros cambios en X componentes/módulos. 

Y con afectados me refiero que tenemos muuuuuchooooos comandos para correr estas verificaciones.

Builds más rapidos (corriendo lo afectado)
Tests más rapidos (corriendo afectados)
Lint y más, sin olvidar que además, genera mucha más **confianza** al momento de modificar un módulo, porque tenemos transparencia y visibilidad de los posibles impactos de nuestro cambio.

NX se banca muchas tecnologías para configurar sus correspondientes @schematics, entre ellas: Angular, React, Nest, Node, Next, etccc. Y si te copa **Storybook**, también lo podes configurar [así](https://nx.dev/angular/plugins/storybook/overview#how-to-use-storybook-in-an-nx-repo)

Recordemos que NX **NO** reemplaza a Angular Cli, sino que lo usa behind de scenes para generar código y correr tasks!

Les comparto todos los comandos que nos ofrece la guía oficial para estas verificaciones [acá](https://nx.dev/angular/cli/affected) y la [guía](https://nx.dev/angular/guides/ci/monorepo-affected) 

También nos brinda un gráfico muy copado haciendo:

    nx dep-graph

Donde nos muestra un lindo diagrama de nuestras apps, librerías y como se comunican entre sí.

Otra ventaja muy *pro* es que si tenés tanto frontend como backend en el mismo repo, es un golazoooo de media cancha, porque podemos reutilizar y compartir interfaces, clases, validaciones etc de ambos.

Si hay varios devs en el team o si el monorepo es cross-team y se desconoce el scope de cada app, NX resulta bastaaneeeteee conveniente para este escenario. 

También podemos saber y recordar dónde se usa cada componente, pero no siempre es así, y si encima tenemos que verificar la existencia de efectos colaterales de todo lo que modificamos no es tan divertido o si? 
![enter image description here](https://i.imgflip.com/5xoxd.jpg)

Además de crear y exportar librerías independientes, hacerlas publicables para otros repos, también se pueden agrupar según conveniencia para que cada app tenga su "set" de librerías predefinidas. Piola.

Qué estás esperando para darle una chance? Si estas ventajas no te convencieron, aca tene [ma](https://nx.dev/angular/getting-started/why-nx) 



Espero les sirva y happy codinggggg!!!

By Sol López, frontend, rosarina, baterista, rock & metal.