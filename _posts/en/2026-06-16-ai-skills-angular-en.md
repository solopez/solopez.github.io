---
date: 2026-06-16 2:30:00
layout: post
title: AI + Angular, Skills and Agents for frontend!
description: Intro to AI development in Angular projects
language: en
image: "../assets/img/AI.png"
category: CODE
tags:
  - coding
  - ai
  - angular
  - humor
author: sol lopez
---

# AI + Angular, Skills and Agents for frontend!
Short post this time: how to bring AI Skills and Agents into an Angular project, so the bot actually respects your conventions and architecture instead of throwing Angular 8 NgModule code at you.

----------

### **The usual problem**

AI agents know Angular... but sometimes it's the Angular from 3 years ago. They suggest modules when your team went full standalone, or `*ngIf` when you already migrated to `@if`. Skills exist exactly for this: they package conventions and architecture into a file the agent loads only when needed.

----------

### **Ready-made Skills for Angular**

1.  **angular/skills (official)**:  
    The Angular team itself maintains a repo with skills for architecture, signals, forms, routing, SSR and testing, all aligned with modern versions. [Repo](https://github.com/angular/skills)
    
2.  **AnalogJS angular-skills**:  
    Another solid collection, split by topic (`angular-component`, `angular-signals`, `angular-forms`, etc) and installable via `npx`. [Repo](https://github.com/analogjs/angular-skills)

----------

### **Your own convention, as a Skill**

The most useful one isn't the generic skill, it's yours: how your team organizes folders, names services, or structures state management. Anthropic's [best practices guide](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) walks through writing a short, effective `SKILL.md` instead of an endless manual the agent ends up ignoring.
![Jason](/assets/img/jason.webp)

----------

### **And for something more autonomous**

For an agent that doesn't just suggest code but actually runs it, executes tests and checks the build on its own, that's where the [Agent SDK](https://code.claude.com/docs/en/agent-sdk/overview) comes in: it gives Claude the full tool loop without you handling every step by hand.

The idea: start with one small skill (your component convention, for instance), test it on a real task, and keep adding from there.

Happy coding (and prompting)!

![Horror icons enjoying a beer : r/midjourney](/assets/img/beer.webp)

