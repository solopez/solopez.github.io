---
date: 2024-06-27 11:00:00
layout: post
title: Clean Code
description: Clean code practices
language: en
image: "../assets/img/cleancode.webp"
category: CODE
tags:
  - coding
  - clean code
  - humor
author: sol lopez
---
# Clean code

Howdyyy? Today's post is dedicated to Clean Code, let's review some practices and principles. While we probably already know why it is important, let's take a look at some of its advantages:

 - Readability and maintainability: to be able to read, understand and modify more easily and safely code that has not been written by us. It is good to rethink if what we write could be interpreted and modified by someone else. 
 - Team collaboration: facilitates communication and cooperation between teams. If we establish code standards, and write code that is easy to interpret, understanding the work of different devs is easier and promotes more effective collaboration.
 - Debbugging + bug fixes: allows us to locate and interpret better, if we name variables in a meaningful and representative way, if we have a clear structure in the code, we facilitate the identification and detection of errors and their resolution.

![code](https://solopez.github.io/assets/img/memes/buttons.png)
Now that we have seen some advantages, let's get to it!
 

## Comments in the code
Good code does not need comments. Variables, methods and any other code components, such as attributes, should have easily identifiable and descriptive names.
![clear](https://solopez.github.io/assets/img/memes/batman.png)

## Conditionals
Positive conditionals are easier to read than negative conditionals, so we must consider their interpretation as easy as possible. In case of evaluating more than one condition, we can help that readability, generating a constant with a meaningful name about what we are evaluating and apply it directly in the condition.

## Magic numbers
We can avoid "magic numbers" or hardcoding of numbers if we store them in constants that represent what that number refers to or what is the purpose of using it in our code.

## Functions and cyclomatic complexity
We can avoid huge functions with a lot of logic if we divide them into smaller functions that only take care of a single task (remember the single responsibility principle).

## DRY Principle
Don't Repeat Yourself. Avoid duplicating and writing the same code more than once. Instead, it is more convenient to reuse, share that code through functions, methods or modules depending on how much we need to abstract. It also helps us to be more consistent and reduce the risk of bugs, since if we need to modify or update something, it is only done once and in one place.
![dont](https://miro.medium.com/v2/resize:fit:1024/1*uywKrvOm4CKZTI6v3a9TjA.jpeg)

## KISS Principle
![kiss](https://image.spreadshirtmedia.net/image-server/v1/mp/products/T1459A839PA4459PT28D187302122W10000H4668/views/1,width=1200,height=630,appearanceId=839,backgroundColor=F2F2F2/kiss-keep-it-simple-stupid-sticker.jpg)
Keep it simple, avoid unnecessary complexity, promote simplicity. Often less is more. It is important that we keep our classes and methods optimally.

## Boy scout principle:
![scout](https://miro.medium.com/v2/resize:fit:530/1*k5xb9ckAsX8rVZgvXiI5bQ.jpeg)
"Always leave code cleaner than you found it." Whenever we detect code that we can improve, even if it is not part of our changes, either for simplicity or for readability issues, go for it. Today for you, tomorrow for me.



References [here](https://blog.codacy.com/what-is-clean-code) and by [here](https://blog.stackademic.com/top-10-clean-code-rules-831fb34caff7)

Happy coding!



![Beer!](https://solopez.github.io/assets/img/beer-code.jpg)