---
date: 2024-08-27 11:00:00
layout: post
title: Playwright
description: Automation
language: en
image: "../assets/img/playwright.png"
category: CODE
tags:
  - coding
  - automation testing
  - humor
author: sol lopez
---

# Playwright

How are you doing? Today's post is dedicated to frontend automation with Playwright, as always the official docu [here](https://playwright.dev)

### What is it?

**Playwright** is a tool for web browser automation. It allows us to test web applications, interact with pages, simulate user actions and more. In this short reading we are going to review concepts, basics and how to start automating using Playwright.

### 1. **Installation

Node.js is a must, so if you don't already have it [here goes](https://nodejs.org).

Once you have Node.js installed, you can install Playwright globally (-g) or in your local project. To install it in a local project, follow these steps:


    
    `npm install playwright`. 
    

This command will download and install the necessary browsers (Chromium, Firefox and WebKit).

### 2. **First Script in Playwright**.

Now that Playwright is installed, let's create a simple script to open a web page.

Create an `index.js` file with the following code:

    
```typescript
    const { chromium } = require('playwright');
    
    (async () => {
      // Inicia el navegador Chromium
      const browser = await chromium.launch({ headless: false }); // headless: false abre la ventana del navegador
      
      // Abre una nueva página
      const page = await browser.newPage();
      
      // Navega a una URL
      await page.goto('https://example.com');
      
      // Toma una captura de pantalla
      await page.screenshot({ path: 'example.png' });
      
      // Cierra el navegador
      await browser.close();
    })();
```

This script will do the following:

- It will start the Chromium browser (without headless mode so you can see what happens).
- Navigate to `https://example.com`.
- It will take a screenshot and save it as `example.png`.
- Finally, it will close the browser.

2.  Run the script:
    

    
    `node index.js` 
    

You will see a browser open, visit the page and take a screenshot.

### 3. **Interacting with Elements**.

To interact with the web page, Playwright has methods like `click`, `type`, `fill`, among others. Let's see how to use them in a form:

    
```typescript
    const { chromium } = require('playwright');
    
    (async () => {
      const browser = await chromium.launch({ headless: false });
      const page = await browser.newPage();
      
      // Navega a un formulario de ejemplo
      await page.goto('https://www.w3schools.com/howto/howto_css_login_form.asp');
      
      // Interactúa con el formulario
      await page.fill('input[name="uname"]', 'mi_usuario');
      await page.fill('input[name="psw"]', 'mi_contraseña');
      
      // Simula un clic en el botón de login
      await page.click('button[type="submit"]');
      
      // Cierra el navegador
      await browser.close();
        })();
    
```

### 4. **Waiting**.

Sometimes it is necessary to wait for certain elements to become available or for the page to finish loading. Playwright handles this automatically, but you could also apply `page.waitForSelector` (note, this is not recommended, only for some exceptions).



`await page.waitForSelector('input[name="uname"]');` 

### 5. **Running Tests

Playwright can be used for automated testing. It integrates nicely with tools like **Jest** or **Mocha**, but Playwright has its own testing framework called **Playwright Test**. Vamooooooo

To get started with Playwright Test, install its package:

`npm install @playwright/test` 

Generate file `test.js`:



```typescript
    const { test, expect } = require('@playwright/test');
    
    test('mi primera prueba', async ({ page }) => {
      await page.goto('https://example.com');
      const title = await page.title();
      expect(title).toBe('Example Domain');
    });
    ```

Run:

`npx playwright test` 

```

### **BONUS: Code Recorder**

Playwright has a built-in tool to record interactions and generate the code automatically (im sorry what?? yeappp, this is real). 
Run the following command to start the recorder:


`npx playwright codegen https://example.com` 

This will open a browser that will record every action you perform on the page (in this case example.com) and will generate the necessary code according to the interaction we have with that website.




Happy coding!



![Beer!](https://solopez.github.io/assets/img/beer-code.jpg)