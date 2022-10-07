---
title: Inversion of Control
date: 2022-10-06 17:05:00 +0800
categories: [Blogging, Technology, Software Development, Design Principle]
tags: [programming, design principle]
---
## Definition

- Inversion of Control (IoC) is a **Design Principle** that provide guidelines for classes to be **loosely coupled** and therefore easy to test and maintain.
- Classes that have minimum dependences is a good thing and considered to be one of the major principles of Software Engineer.
- IoC refers to **transferring the control of its object, dependencies from the main program to a framework or container**.
- IoC **provide a callback/function (which controls reaction/action)** to an external handler/controller, **instead of executing the action ourself (invert or redirect control to external handler/controller)** - [Source](https://stackoverflow.com/a/3140/14163916).

## IoC popular implementation

Inversion of Control and Dependency Injection are often used interchangeably.

1. Dependency Injection (DI)
2. Server Locator Pattern
3. Event-driven programs

## Dependency Injection (DI)

**Dependency Injection is a technique that give objects its instance variable or what it needs (dependencies)**. DI can also be implement using a framework, the most popular one is [Spring Framework](https://spring.io/projects/spring-framework) but it's not necessary to have for doing DI.

> Instantiating and passing object (dependencies) explicitly is just as good and injection as injection with framework. - [Source](https://stackoverflow.com/a/140655/14163916).
{: .prompt-info }

For DI there's several ways of injecting dependencies into an object. Below shows an example some of those injection methods:

- Constructor Injection
- Setter Injection
- Interface Injection

## Server Locator Pattern

- Server locator pattern is an implementation that provides server locator object that contains all the information about all the service that been provided by the application.
- Upon instantiation server locator object all the services register themselves with the server locator.
- After receives a request from a client, the service locator perform their task and return the requested value to the client.
- This pattern also reduce coupling between the dependent classes.

## Benefits of Inversion of Control

- Easy to test and maintain
- Decrease coupling between classes.
- Reduce code amount.

---

## Sources

1. [What is inversion control?](https://www.educative.io/answers/what-is-inversion-of-control)
2. [Discussion about inversion control on Stack Overflow](https://stackoverflow.com/questions/3058/what-is-inversion-of-control#3140)
3. [Dependency Injection made easy](https://www.jamesshore.com/v2/blog/2006/dependency-injection-demystified)
