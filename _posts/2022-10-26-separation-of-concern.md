---
title: Separation of Concern (SoC)
date: 2022-10-26 18:00:00 +0800
categories: [Blogging, Technology, Software Development, Design Principle]
tags: [design principle, soc]
---

> **Separation of Concerns** is an action of splitting computer's program into a different features without/with less overlapping in functionality as possible.

## Concern

- Concern are **features** or **behaviors**. Basically functionality or methods.

## Domain

- SoC suggested that website's inner structure should be divided into separated domains, these domains define the application as a whole.
- Possibly, these domains should be separated into different source/files so that it can be easily identified later in the future.

### Why domain is essential for SoC

- Often times, each section in the website will have to make changes uniquely, for example: as developer you maybe want to make/use different **presentation** or user interface, but want to keep using the same business logic. By separating this section into domains, it will make it easier to "make changes/convert to a new" without affecting the others part of your website.
- By splitting website into domains, it will make the navigation within the website's inner structure easier. For example, if you want to make changes related to the user's interaction, then you will only need to navigate to the **business logic** section
- . With domains, other people can work on individual domains/pieces in isolation without worrying affecting other people's works.

### SoC domains for client's side

Based on the details below, separation in SoC is needed to avoid overlapping between 'concern' such as; between **business logic** and **presentation** or **data** and **business logic** and etc.

- **Presentation** - Visual appearance of the website.
- **Business Logic** - Website's behavior based on user actions.
- **Data** - Data that being displayed to the user.

> Separation into these three domain doesn't have to be the only one. Let say if you have login page, profile page and account management page, you can separate all these pages from each other; where each of these page will have their own **Presentation, Business Logic and data** domains, separated from other pages.

### SoC domains for web server

- **Input Layer** -  Handling HTTP Request. By validating the request to determine which is the right **logic's function** before sending them to that function.
- **Logic Layer** - Process on the data based on user's input/request.
- **Data Access Layer** - Responsible for perform complex query to database, reading/writing in-memory representations of data to/from the database,. This layer is like mediary between database and logic layer.

### Cross-cutting concerns

- Sometime 'concern' can't be separated easily, for example when dealing with `logging` and `error handling` concerns, both of this can be consider as separate concern but during its implementation this two concerns tend to bind tightly with other code. This is what we called **cross-cutting concerns** because they're overlapping with the boundary of the other concerns.

## Different between SoC and SRP

- Basically both of this principle promotes decoupling where both of this principle suggested that every objects, modules and classes should be loosely couples as possible.

>It can be confusing when try to understand the meaning behind "Concern" and "Responsibility". Instead focusing on the meaning, we should know that both of these share the same purpose and idea, which is to make the application become 'loosely couples' as possible - [source](https://stackoverflow.com/a/25012230/14163916) .  

- But based on my understanding, [SRP](/posts/solid-srp/) is for classes, where each classes and its properties must only holds one responsibility only. While SoC is to separate any object, modules, class from being tightly coupled with one another. **SoC is like DLC to a games (SRP**).

### Example: SoC but without SRP

- As you can the snippet below, the classes is not tightly coupled with one another because it uses interface as abstraction to prevent coupling. In SoC rules, this is valid implementation.
- In SRP point of view this is not valid, this is because of the three private methods inside `Customer` class, these method could be separated into its own classes; where two method that are related to navigation could be place into `INavigation` class while the other method that do some calculation to the purchase could be place into `IPurchaseLogic` class.

```c#
public class Customer
{
 private readonly IDataValidator _dataValidator;
 private readonly IDataFetcher _dataFetcher;

 public Customer(IDataValidator dataValidator, IDataFetcher dataFetcher)
 {
  _dataValidator = _dataValidator;
  _dataFetcher = _dataFetcher;
 }

 public NavigationObj GetCustomerPurchaseData()
 {
  var purchaseData = _dataFetcher.GetAllCustomerPurchase();

  if (_dataValidator.isCustomerActive(purchaseData))
  {
   purchaseObj z = null;
   
   foreach(var element in purchaseData.Items)
   {
    z = CalculatePurchase(element);
   }

   if(_dataValidator.IsPurchaseValid(z))
   {
    return ValidPurchaseLogic();
   }
  }

  return InvalidPurchase();
 }

 private purchaseObj CalculatePurchase(purchaseObj element)
 {
  return new purchaseObj();
 }

 private NavigationObj ValidPurchaseLogic()
 {
  return new NavigationObj();
 }

 private NavigationObj InvalidPurchase()
 {
  return new NavigationObj();
 }
}
```

### Example: SoC with SRP

- Snippet below will show how the SRP is being implemented, This snippet is based on the previous section.
- By separating the three private methods (previous snippet) into their own classes which have their own responsibility. Making the below snippet is correct in the point of SRP.

```c#
public class Customer
{
 private readonly IDataValidator _dataValidator;
 private readonly IDataFetcher _dataFetcher;
 private readonly INavigation _navigation;
 private readonly IPurchaseLogic _purchaseLogic;
 
 public Customer(IDataValidator dataValidator, IDataFetcher dataFetcher, 
     INavigation navigation, IPurchaseLogic purchaseLogic)
 {
  _dataValidator = _dataValidator;
  _dataFetcher = _dataFetcher;
  _navigation = navigation;
  _purchaseLogic = purchaseLogic;
 }

 public NavigationObj GetCustomerPurchaseData()
 {
  var purchaseData = _dataFetcher.GetAllCustomerPurchase();

  if (_dataValidator.isCustomerActive(purchaseData))
  {
   purchaseObj z = null;
   
   foreach(var element in purchaseData.Items)
   {
    z = _purchaseLogic.CalculatePurchase(element);
   }

   if(_dataValidator.IsPurchaseValid(z))
   {
    return _navigation.ValidPurchaseLogic();
   }
  }

  return _navigation.InvalidPurchase();
 }
}
```

---

## Sources

1. [Stack Overflow - SoC VS SRP](https://stackoverflow.com/questions/1724469/difference-between-single-responsibility-principle-and-separation-of-concerns)
2. [Stack Exchange - what is the difference between SRP and SoC](https://softwareengineering.stackexchange.com/questions/155628/what-is-the-difference-between-single-responsibility-principle-and-separation-of)
3. [Artur Trosin's Blog - SoC VS SRP](https://weblogs.asp.net/arturtrosin/separation-of-concern-vs-single-responsibility-principle-soc-vs-srp)
4. [Talin - Separation of Concern](https://medium.com/machine-words/separation-of-concerns-1d735b703a60)
5. [Single Responsibility Principle (SRP)](/posts/solid-srp/)
