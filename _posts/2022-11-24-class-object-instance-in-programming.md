---
title: Class vs Object vs Instance in Programming
date: 2022-11-24 18:57:00 +0800
categories: [Blogging, Technology, Software Development]
tags: [programming]
---

## Overview

> "A blueprint for a car design is like `Class` description, All the car built from that blueprint are called `Object` of that `Class`. A given car is an `Instance`."

## Definition

> - [Object](https://stackoverflow.com/questions/8550130/what-is-the-difference-between-objects-and-classes-in-c) (Programming) is an **instance of a class.** The actual thing that is build based on the blueprint or class  (Car)
> - [Class](https://stackoverflow.com/questions/8550130/what-is-the-difference-between-objects-and-classes-in-c) (Programming) **definition/description of an object**, does not become object until it is instantiated.  (Blueprint)
> - [instance](https://www.techtarget.com/whatis/definition/instance) (Programming) is a specific realization of any object or virtual copy of an object (not the real copy).
> - [instantiation](https://www.techtarget.com/whatis/definition/instantiation) (Programming) act of creating a real object/class, it can also be an act of creating an abstraction/template of an object/class.

## Deep dive: Instance

- Instance can be known as a `memory reference` or `reference variable`.
- **Instance is a variable created in memory (`memory reference/reference variable`) that only holds memory address of an object in it.**
- The object it addresses is the the same object the instance is said to be `an instance of`.
- If have many instance of one object, this mean it will also have many variables in different places in the memory that hold the exact same memory address (that represent a single object).
- Can't ever change instance. programmatically in code it may looks like the instance can be change, but what actually happen is that you're changing the original object directly.

## Deep dive: Class & Object

- Details about an Object and Class is store in the memory.
- Object is actually an exact copy of the Class. Class variable is store elsewhere in the memory which holds the exact same details as the Object.
- **Object is a copy of the class, Instance is a variable that holds the memory address of the object.**
- Inside class contain `behavior` or functionalities that define how the class should operates.

You can have multiple Object of the same Class and can then have multiple Instances of each of those objects, Meaning each object's set of instances holds similar value but the instances between object are not. Example:

> Class A let Object 1, Object 2, Object 3

- *Object 1 has the exact value as Object 2 and Object 3 but are different placement in the memory*

> From Object 1 >> let obj1_instance1, obj1_instance2, obj1_instance3

- *All of these instance hold similar value and in different placement in memory. Their values is `Object1.MemoryAddress`*

## Messier with C# type?

```C#
Car ferrary;
ferrary = new Car();
```

- The first line `Car ferrary;` declare variable of type `Car`. The declaration cause an empty variable that can hold `Car` object to be created. This shows that nothing changes with the variable until its either becomes an object or is set to memory address of an object.
- The second line, right side `new Car();` created a new copy of the `Car` class, creating a new object, this object is created inside **heap memory** and some address is allocated to it.
- The Second Line, left side `ferrary =`. This turn `ferrary` into a `reference variable/memory reference` (hold references to that memory address of the object on the heap memory), giving it the memory address of the object that was just created at the right side of the second line.
- `Ferrary` only holds reference to the memory address of the object in the heap and not the object itself.

> If you want to become a good developer, its important to understand that no computer environment ever works based on philosophic ideals. Computers aren't even that logical - they're really just a big collection of wires that are glued together using basic Boolean circuits (mostly NAND and OR). - [*Rambly John*](https://stackoverflow.com/a/14802302/14163916)

---

## Sources

1. [What is an instantiation in computer programming?](https://www.techtarget.com/whatis/definition/instantiation)
2. [What is the meaning of instance?](https://www.techtarget.com/whatis/definition/instance)
3. [oop - Difference between object and instance - Stack Overflow](https://stackoverflow.com/a/14802302/14163916)
