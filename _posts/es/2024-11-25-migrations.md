---
date: 2024-11-25 10:00:00
layout: post
title: Migrando a Angular 15, 16 y 17!
description: Migrando
language: es
image: "../assets/img/ng17.svg"
category: CODE
tags:
  - coding
  - migrating
  - humor
author: sol lopez
---

# Migrando a Angular 15, 16 y 17!
Buenass como andan? El post de hoy va dedicado a migraciones de angular, compartiendo las novedades, cambios y mejoras de estas tres versiones, como para ir cerrando este 2024. 
También dejo la docu y guía oficial para migrar y los comandos por [acá](https://angular.dev/update-guide).




### **Angular 15**

1.  **Standalone Components (introducción)**:  
    Aunque en Angular 16 se hicieron el estándar, en Angular 15 ya se podía empezar a usarlos para crear aplicaciones sin depender de módulos (de modo un poco experimental). Fue el primer paso hacia una forma más simple de trabajar con Angular. 
Si todavía no viste como funcionan los standalone, te cuento que vienen a reemplazar los modules que armábamos antes, por componentes independientes (standalone) que ya cuentan con sus propios imports y metadata necesaria para funcionar por si solos, haciendo que puedan importarse directamente estos componentes en otros, sin necesidad de crear o pertenecer a algun module para eso. 
Para mas info y videos, recomiendo pegarle una [revisada](https://v17.angular.io/guide/standalone-components)
    
2.  **Mejoras en Material Design**:  
    Angular Material recibió actualizaciones para alinearse con las guías de Material Design 3. Se incluyeron nuevos componentes y mejoras visuales.
    
3.  **Directivas como standalone**:  
    Ahora podemos declarar directivas y pipes como standalone, haciéndolos independientes de NgModules, igual que los componentes.
![Non merci! France issues rare ban for horror film 'Terrifier 3' - the first  -18 rating since 2006 | Euronews](https://static.euronews.com/articles/stories/08/78/01/90/1200x675_cmsv2_60ff6e18-32fc-5f9b-a9a2-61b32e94caa0-8780190.jpg)
    
4.  **Mejoras en el router**:  
    El router se volvió más poderoso, con soporte mejorado para configuraciones de rutas y manejo dinámico de datos.
    
5.  **Mejor compatibilidad con TypeScript**:  
    Soporte para TypeScript 4.8, permitiendo aprovechar las características modernas del lenguaje.
    
6.  **Desempeño optimizado**:  
    Angular 15 incluyó varias mejoras internas para que las aplicaciones sean más rápidas y ligeras.
    

----------

### **Angular 16**

1.  **Standalone Components como estándar**:  
    Ya no necesitamos módulos (NgModules) para trabajar. Todo es más directo (y no tan experimental)
    
2.  **Signals**:  
    Introducción de una nueva forma de manejar datos reactivos que es simple, eficiente y predecible. Si todavía no viste o trabajaste con signals, te recomiendo chusmear por [acá](https://angular.dev/guide/signals)
    
3.  **SSR mejorado (Hydration)**:  
    Más eficiencia al combinar el HTML del servidor con el navegador. Esto acelera las apps.
    ![Meme Drunk Baby - cuando me dicen que me tengo que hidratar - 19445555](https://cdn.memegenerator.es/descargar/19445555)
    
4.  **Router más flexible**:  
    Nuevas APIs para trabajar con rutas dinámicas y mejor manejo de componentes.
    
5.  **Rendimiento mejorado**:  
    Optimización en cómo se renderizan y actualizan las vistas.
    

----------

### **Angular 17**

1.  **Signals integrados en más partes del framework**:  
    Ahora están mejor conectados con otros elementos como los formularios y el router.
    Por ejemplo, antes teníamos que subscribirnos al observable del control del form para implementar lógica y desuscribirnos para evitar fugas, ahora, con signals en form de manera nativa, ya no necesitamos preocuparnos por eso ni subscribirnos.
    ![Terrifier 3: O que você precisa saber antes de ver o filme de terror -  Observatório do Cinema](https://media.tenor.com/iHa8Q3BQsYgAAAAe/terrifier-clown-meme.png)
    
2.  **Tests más simples y rápidos**:  
    Las APIs de prueba fueron optimizadas para que todo sea más fácil y rápido.
    
3.  **Actualización en TypeScript**:  
    Soporte para las últimas versiones de TypeScript, con nuevas características. Estamos hablando de [typescript 5.x.x](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-5-0.html) y por las dudas comparto también la [matrix de versionado](https://angular.dev/reference/versions) 
    
4.  **Directivas simplificadas**:  
    Crear directivas es más rápido, sobre todo para casos básicos.
    
5.  **CLI más eficiente**:  
    Las herramientas de línea de comandos ahora generan proyectos más rápidos y ligeros.

### Storybook
Si contas con Storybook en alguno de tus proyectos, tenemos la versión 8 disponible para implementar con varias mejoras:


📸 Built-in visual testing  
⚛️ React Server Component support  
🎛️ Upgraded Vue and React control autogeneration  
⚡️ Rearchitected Vite support, Vitest testing, and Vite 5 support  
🧪 2-4x faster test builds  
✨ Refreshed desktop UI  
📲 Rebuilt mobile UX  
🙅‍♀️ Removed React dependency for non-React projects

Más info y detalles por [acá!](https://storybook.js.org/blog/storybook-8/)

Happy coding!



![Horror icons enjoying a beer : r/midjourney](https://preview.redd.it/horror-icons-enjoying-a-beer-v0-s5yqa6o66isb1.jpg?width=640&crop=smart&auto=webp&s=01e8df3068dc16a1d4016371988c1c77809a5e70)
