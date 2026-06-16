---
date: 2026-06-16 2:30:00
layout: post
title: IA + Angular, Skills y Agentes para frontend!
description: Intro a desarrollo con IA en proyectos Angular
language: es
image: "../assets/img/AI.png"
category: CODE
tags:
  - coding
  - ai
  - angular
  - humor
author: sol lopez
---

# IA + Angular, Skills y Agentes para frontend!
Posteo cortito esta vez: cómo meterle Skills y Agentes de IA a un proyecto Angular, para que respete tus convenciones y arquitectura en vez de tirarte código de Angular 8 con NgModules.

----------

### **El problema de siempre**

Los agentes de IA conocen Angular... pero a veces conocen el Angular de hace 3 años. Te sugieren módulos cuando ya laburás full standalone, o `*ngIf` cuando tu equipo migró a `@if`. Las Skills existen justo para esto: empaquetan convenciones y arquitectura en un archivo que el agente carga solo cuando hace falta.

----------

### **Skills ya armadas para Angular**

1.  **angular/skills (oficial)**:  
    El propio equipo de Angular mantiene un repo con skills para arquitectura, signals, forms, routing, SSR y testing, todo alineado a las versiones modernas. [Repo](https://github.com/angular/skills)
    
2.  **angular-skills de AnalogJS**:  
    Otra colección sólida, con skills separadas por tema (`angular-component`, `angular-signals`, `angular-forms`, etc) e instalación por `npx`. [Repo](https://github.com/analogjs/angular-skills)

----------

### **Tu propia convención, como Skill**

Lo más útil no es la skill genérica, es la tuya: la forma en que tu equipo organiza carpetas, nombra servicios, o estructura el state management. La [guía de buenas prácticas](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) de Anthropic te tira cómo escribir un `SKILL.md` corto y efectivo en vez de un manual interminable que el agente ignora.
![Jason](/assets/img/jason.webp)

----------

### **Y si querés algo más autónomo**

Para que el agente no solo sugiera código sino que ejecute, corra tests y verifique el build solo, ahí entra el [Agent SDK](https://code.claude.com/docs/en/agent-sdk/overview): le da a Claude el loop completo de herramientas sin que vos manejes cada paso a mano.

La idea: empezar con una skill chica (tu convención de componentes, por ejemplo), probarla en una tarea real, y de ahí ir sumando.

Happy coding (and prompting)!

![Horror icons enjoying a beer : r/midjourney](/assets/img/beer.webp)
