---
date: 2024-08-27 11:00:00
layout: post
title: Playwright
description: Automatizando
language: es
image: "../assets/img/playwright.png"
category: CODE
tags:
  - coding
  - automation testing
  - humor
author: sol lopez
---

# Playwright

Buenasss como andan? El post de hoy va dedicado a un nuevo mundo: end-to-end test automation, en frontend, y con Playwright, como siempre la docu oficial por [acá](https://playwright.dev)

### Qué es?

**Playwright** es una herramienta para la automatización de navegadores web. Nos permite realizar pruebas en aplicaciones web, interactuar con páginas, simular acciones del usuario y más. En esta pequeña lectura vamos a repasar conceptos, fundamentos y como arrancar a automarizar mediante Playwright.

### 1. **Instalación**

Node.js es un must, asi que si todavia no lo tenes [ahi va](https://nodejs.org).

Una vez que tengas Node.js instalado, podes instalar Playwright globalmente (-g) o en tu proyecto local. Para instalarlo en un proyecto local, sigue estos pasos:

`npm install playwright`

Este comando descargará e instalará los navegadores necesarios (Chromium, Firefox y WebKit).

### 2. **Primer Script en Playwright**

Ahora que Playwright está instalado, vamos a crear un simple script para abrir una página web.

1.  Crea un archivo `index.js` con el siguiente código:

    ```typescript
    const { chromium } = require("playwright");
    (async () => {
      // Inicia el navegador Chromium
      const browser = await chromium.launch({ headless: false }); // headless: false abre la ventana del navegador
      // Abre una nueva página
      const page = await browser.newPage();
      // Navega a una URL
      await page.goto("https://example.com");
      // Toma una captura de pantalla
      await page.screenshot({ path: "example.png" });
      // Cierra el navegador
      await browser.close();
    })();
    ```

Este script hará lo siguiente:

- Iniciará el navegador Chromium (sin modo headless para que puedas ver lo que ocurre).
- Navegará a `https://example.com`.
- Tomará una captura de pantalla y la guardará como `example.png`.
- Finalmente, cerrará el navegador.

2.  Ejecuta el script:


    `node index.js`


Verás que se abre un navegador, visita la página y toma una captura de pantalla.

![Funny Cat Memes Images - Free Download on Freepik](https://img.freepik.com/free-vector/simple-vibing-cat-square-meme_742173-4493.jpg?size=338&ext=jpg&ga=GA1.1.2008272138.1724716800&semt=ais_hybrid)

### 3. **Interactuando con Elementos**

Para interactuar con la página web, Playwright tiene métodos como `click`, `type`, `fill`, entre otros. Vamos a verrrr como usarlos en un formulario:

```typescript
const { chromium } = require("playwright");

(async () => {
  const browser = await chromium.launch({ headless: false });
  const page = await browser.newPage();

  // Navega a un formulario de ejemplo
  await page.goto("https://www.w3schools.com/howto/howto_css_login_form.asp");

  // Interactúa con el formulario
  await page.fill('input[name="uname"]', "mi_usuario");
  await page.fill('input[name="psw"]', "mi_contraseña");

  // Simula un clic en el botón de login
  await page.click('button[type="submit"]');

  // Cierra el navegador
  await browser.close();
})();
```

### 4. **Esperas**

A veces es necesario esperar a que ciertos elementos estén disponibles o que la página termine de cargarse. Playwright maneja esto automáticamente, pero tambien se podria aplicar `page.waitForSelector` (ojooooo, no es lo recomendable, solo para algunas excepciones su uso). Ejemplo de uso:

`await page.waitForSelector('input[name="uname"]');`

![The best Be Careful memes :) Memedroid](https://images3.memedroid.com/images/UPLOADED325/6511da63da24d.jpeg)

### 5. **Ejecutando Pruebas**

Playwright puede ser usado para pruebas automatizadas. Se integra muy bien con herramientas como **Jest** o **Mocha**, pero Playwright tiene su propio marco de pruebas llamado **Playwright Test**. Vamoooooo

![cats](https://i.pinimg.com/1200x/ea/de/1f/eade1feca67faed06570cf5495621746.jpg)

Para empezar con Playwright Test, instala su paquete:

`npm install @playwright/test`

Crea un archivo `test.js`:

```typescript
    const { test, expect } = require('@playwright/test');

    test('mi primera prueba', async ({ page }) => {
      await page.goto('https://example.com');
      const title = await page.title();
      expect(title).toBe('Example Domain');
    });`

```

Ejecutamos la prueba con:

`npx playwright test`

### **BONUS: Recording**

Playwright tiene una herramienta integrada para grabar las interacciones y generar el código automáticamente (im sorry what?? siiii esto es realllllll).
Ejecutá el siguiente comando para iniciar el grabador:

`npx playwright codegen https://example.com`

Esto abrirá un navegador que grabará cada acción que realices en la página (en este caso example.com) y generará el código necesario de acuerdo a la interacción que vayamos teniendo con esa web. Si bien manualmente tengamos que ajustar nuestro código para que sea dinámico y se adapte a las necesidades, para agilizar el proceso es un golazo!

Nota: También es posible configurar y adaptar (desde nuestra playwright.config) los reportes, para que los resultados tambien generen y guarden screenshots y/o videos de las pruebas ejecutadas (sí, magia pura).

![happy](https://i.pinimg.com/736x/dc/ae/89/dcae89ba0987641157f54e5f34eeeb5c.jpg)

Happy coding!

![Beer!](https://solopez.github.io/assets/img/beer-code.jpg)
