---
title: MVC with ASP.NET Core
date: 2022-10-11 18:00:00 +0800
categories: [Blogging, Technology, Software Development]
tags: [browser, ASP.NET Core, design-pattern]
---

## Definition

- **MVC (Model View Controller)** is a design pattern that used for building web application. This pattern commonly used within the web framework like Ruby on rails, Express, Angular and many more).
- This pattern separated into three components which includes **Model, View and Controller**, this separation between component is to decouples parts of application and helps application achieves Dependency Injection.
- User request will be send to a Controller, Controller will then handle the user request and/or retrieve the results of queries from the database along with the helps of Model. The controller then bind model containing the queries results with the View to display it to the user.

## Model Definition

- **Represent the state of the application, business logic and operation** that should be executed by Model. Business logic should be encapsulated inside the Model along with business logic that responsible retaining the state of the application.
- `ViewModel` types is responsible to hold a data to display on a View. The controller responsible in creating and populating these `ViewModel` instances from the Model.

## View Definition

- Viewing content for the user interface. Using Razor view engine to embed .NET code in HTML code.
- Contain minimal logic within the view, logic only focuses on presenting the data for the View. For complex logic it's suggested to use `ViewModel` instead.

## Controller Definition

- Responsible to handle user interaction, working with Model and rendering View with data.

## Common MVC use case

- Controller receive request, process and fetch the requested info from the database.
- Controller create model and bind the received information from the database into a View.
- View is rendered and displayed in the user's browser.
- User submit a filled form, which create a new request to the controller, and the cycle will repeat.

## MVC Implementations

For the next section, I'll be explaining about each of these three component  (Model, View & Controller), this is only a brief and basic example, go to [Learn MVC ASP Net Core](https://learn.microsoft.com/en-us/aspnet/core/mvc/overview?WT.mc_id=dotnet-35129-website&view=aspnetcore-6.0) for more details:

### Model Creation

- Require two separated model classes that are essential in implementing MVC pattern with ASP.NET Core.
  - The first one is model that represent a data stored in the database or can also be known as **Entity Model**. (This model define what the database row  will look like) Below is an example:

 ```c#
  // Models/TodoItem.cs
  // Imported library sit here..
  namespace AspNetCoreTodo.Controllers
  {
   public class TodoItem 
   {
    // Globally Unique Identifier that contains unique long random character
    // If use interger as ID need to configure DB to increment number when new row is added
    // Guid generated randomly no need incrementing.
    public Guid Id { get; set; } 
    
    public bool IsDone { get; set; } 
    
    [Required] 
    public string Title { get; set; } 
    
    public DateTimeOffset? DueAt { get; set; }
   }
  }
 ```

- The latter model is called **View Model**. This model will be combined with a view and will be display to the user's browser.
  - This model might be similar with the Entity Model but it's not exactly the same, this model is defined based on the view's requirement.
  - For the View component, the data is needed to be display might be more than one, thus, separate class that holds an array of TodoItem (Entity Model) is needed. Below is an example:

  ```c#
  // Models/TodoViewModel.cs
  // Imported library sit here..
  namespace AspNetCoreTodo.Models 
  { 
   public class TodoViewModel 
   { 
    public TodoItem[] Items { get; set; } 
   } 
  }
  ```

### View Creation

- View in ASP.NET Core are built using Razor templating language which enable the combination of HTML markup and also C# code.
- With the implementation of C#, user can use and bind View Model into the HTML markup, thus able to preview data  from the database. Below is an example:

```html
<!-- Views/Todo/Index.cshtml -->
<!-- model directive tells Razor which model will this view bound to -->
@model TodoViewModel

@{
    ViewData["Title"] = "Manage your todo list";
}

<div class="panel panel-default todo-panel">
    <div class="panel-heading">@ViewData["Title"]</div>

    <table class="table table-hover">
        <thead>
            <tr>
                <td>&#x2714;</td>
                <td>Item</td>
                <td>Due</td>
            </tr>
        </thead>

        @foreach (var item in Model.Items)
        {
            <tr>
                <td>
                    <input type="checkbox" class="done-checkbox">
                </td>
                <td>@item.Title</td>
                <td>@item.DueAt</td>
            </tr>
        }
    </table>

    <div class="panel-footer add-item-form">
        <!-- TODO: Add item form -->
    </div>
</div>
```

### Controller Creation

- **URL Routes** that being handled by Controller is called **Actions** and this **Actions** are represented as **Methods** in the controller class. Below shows three **action methods** which are mapped for each of these URL Routes:

```markdown
localhost:5000/Home           -> Index()
localhost:5000/Home/About     -> About()
localhost:5000/Home/Contact   -> Contact()
```

- **Action Methods** able to return JSON Data, HTTP status code (200 OK and 404 Not Found) and Views. This return value is handled by the `IActionResult`.
- Below shows a implementation of Action Methods within the Controller:

```C#
// Controllers/TodoController.cs
// Imported library sit here..

namespace AspNetCoreTodo.Controllers 
{ 
 public class TodoController : Controller 
 { 
  public IActionResult Index() {
   // Able to return JSON, HTTP Status code and Views
  }
 } 
}
```

### Summarize MVC creation

- Model is a representation state of the application, for this representation to work, model is divided into two types which is **Entity Model** and **View Model**. Entity Model represent the structure of the database like its row while View Model represent the structure of how the data from the model is define  to the user's interface.
- View component in ASP NET Core enable the implementation of C# within the HTML markup to display View Model.
- Controller in the other hands, its like a handler for both Model and View component. Controller will handle the user request, creating Model, querying data from the database. For me, controller is like a bridge that connect between all component of MVC.

### Separation layer

- For this section, will be focusing on the connection between controller with database and also controller with other components.
- To define the connection between Controller and database, it's possible to write all down into one big controller, but it defeat the purpose of implementing MVC into our application. Which strongly emphasized on Separation of Concerns.
- By decoupling business logic to another classes, Testing and updating the business logic and database code can become much easier.
- MVC application can be separated into two layers: a **presentation layer** (Controllers and Views for user interaction) and **service layer** (Business logic and Database Code). But can be separated into another layer called **data repository layer** (focused on database code (no business logic)).

#### Service Layer

##### Interface creation

- Holds the separated definition of an Object's method and properties from their actual classes. Interface is use to keep the classes decoupled and easier to test.
- Interfaces are prefixes with "I". Below is an example of interface:

```c#
// Services/ITodoItemServices.cs
using System; 
using System.Collections.Generic; 
using System.Threading.Tasks; 
using AspNetCoreTodo.Models;

namespace AspNetCoreTodo.Services 
{ 
 public interface ITodoItemService 
 { 
  // Interface doesn't contect actual code
  // Only content the definition (or method signature) of GetIncompleteItemsAsync method
  // Method doesn't require parameter and return Task<TodoItem[]>
  // Task that contains an array of TodoItems
  Task<TodoItem[]> GetIncompleteItemsAsync(); 
  
  // Task type is similar to promise...
  // ..used here is to define that the definition method above will be asynchronous...
  // ..meaning the method may not be able to return to-items right away
  // Have to use await when try to consume task, so that the code waits until the result is ready first
 }
}
```

##### Service Creation

- After defining an interface, services can now be created. By creating services, connecting the controller with the database will be possible. But for this guide hard coded database value is used for the sake of simplicity.

```c#
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using AspNetCoreTodo.Models;

namespace AspNetCoreTodo.Services
{
 // This FakeTodoItemService implement the ITodoItemServcie interface...
 //..always returning the same array of two TodoItems
    public class FakeTodoItemService : ITodoItemService
    {
        public Task<TodoItem[]> GetIncompleteItemsAsync()
        {
            var item1 = new TodoItem
            {
                Title = "Learn ASP.NET Core",
                DueAt = DateTimeOffset.Now.AddDays(1)
            };

            var item2 = new TodoItem
            {
                Title = "Build awesome apps",
                DueAt = DateTimeOffset.Now.AddDays(2)
            };

            return Task.FromResult(new[] {item1, item2 });
        }
    }
}
```

##### Dependency Injection

- After configuring the interface and connecting it to the service. This is where the connection between the Controller and "database" happen. By consuming the interface controller will now be able to communicate with the database.
- Below shows an example, to setup services into the controller:

```c#
    public class TodoController : Controller
    {
        private readonly ITodoItemService _todoItemService;
        
        public TodoController(ITodoItemService todoItemService)
        {
            _todoItemService = todoItemService;
        }

        // Routes that are handled by controllers are called actions,
        // and are represented by methods in the controller class. thus action methods.
        public async Task<IActionResult> Index()
        {
            // IActionResult can return views, JSON data, HTTP status codes
            // Get to-do items from database

            // Put items into a model

            // Render view using the model

            return View();
        }
    }
```

- As you can see above, at the first line of the class contains a private variable that hold reference to the `ITodoItemService`, this variable enable its usage within another scope.
- The `public TodoController(ITodoItemService _todoItemService)` line is a special method called `constructor`, this constructor is called whenever a new instance of a class is require, in this case the class which is needed to be instantiate is `TodoController`.
- By adding `ITodoItemService` within the instance of  `TodoController` , it strictly imply that in order to create the `Todocontroller`  a specific object that matches the `ITodoItemService` interface is require as its parameter.
- With interface, we can replace and use any classes that uses the same interface as the parameter's of the constructor. This is because interface helps decouple the logic of the application.
- After setting up service into the controller, the service can now be use within the action method to fetch data from the service layer, below is an example:

```c#
 // ..Setting Up Service..
 
 public async Task<IActionResult> Index()
 {
  // IActionResult can return views, JSON data, HTTP status codes
  // Get to-do items from database
  var items = await _todoItemService.GetIncompleteItemAsync();

  var model = new TodoViewModel()
  {
   Items = items;
  };
  
  return View(model);
 }
```

- In order to tell ASP.NET Core to use `FakeTodoItemService` whenever `ITodoItemService` interface is requested in a constructor or anywhere else, implement a code like an example below within the `Program.cs`:

```c#
 builder.Services.AddSingleton<ITodoItemService, FakeTodoItemService>();
```

- `AddSingleton` will tells that only one copy of the `FakeTodoItemService` is created, and it's reused whenever this service is requested.
- Thus, whenever a request comes in and is routed to the `TodoController`, ASP.NET Core will automatically check all the service available and automatically supply the `FakeToDoItemService`  whenever the controller ask for `ITodoItemService`. `FakeToDoItemService` is being injected whenever `ITodoItemService` is called. (Dependency Injection).

---

## Sources

1. [Little ASP Net Core Book](https://recaffeinate.co/book/)
2. [Learn MVC ASP Net Core](https://learn.microsoft.com/en-us/aspnet/core/mvc/overview?WT.mc_id=dotnet-35129-website&view=aspnetcore-6.0)
