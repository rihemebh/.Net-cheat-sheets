# ASP.NET

ASP stands for : **A**ctive **S**erver **P**ages


    ASP.NET is a popular web-development framework for building web apps on the .NET platform.

    

# ASP.NET Core 

    ASP.NET Core is the open-source version of ASP.NET
    
 # ASP.NET Core MVC.
<img src="https://github.com/rihemebh/.Net-cheat-sheets/blob/main/ASP.net/mvc.PNG" alt="archi" width="480" height="300"/>
 
 

 
## Controllers 

### Actions : 
Actions are the Methods within a controller <br/>
Every method could return an object that implements the **IActionResult** : 

 |ViewResult|ContentResult|RedirectToActionResult|RedirectToRouteResult|StatusCodeResult|
 |---|---|---|---|---|
 |Rendering the HTMLfile <br /> returns view|Returns a message and not all the HTML page|Redirect to specified action instead of rendering the HTML <br /> returns RedirectToAction(ActionName:["name"] , ControllerName : ["name"]) |Redirect to action from the specified URL defined in RouteConfig file <br/>returns RedirectToRoute(new{controller = ["controllename"], action = ["About"] })|returns http status code like 200 / 404 / 500|
 
We could Pass parameters to actions by : 

 |The Request property|The FormCollection object|The Request Body|Routing -RouteData Property|
 |---|---|---|---|



 

## Passing data to the view: 

### Adding Information: (In the controller)
  
 #### ViewBag 
     ViewBag.Message = “some text”;
     ViewBag.ServerTime = DateTime.Now;
  #### ViewData 
  
      ViewData["Message"] = "some text";
      ViewData["ServerTime"] = DateTime.Now;
      

### Retrieving Information: (In the view)
 #### ViewBag 
     <p>
    Message is: @ViewBag.Message

    Server time is: @ViewBag.ServerTime.ToString()
    </p>
 #### ViewData 
    <p>
      Message is: @ViewData["Message"] //ViewBag.Message
      Server time is: @((DateTime)ViewData["ServerTime"])
    </p>

  *Ps : @ in the html file means server-side code * [see more]()
  
  ### Routing

   Routing is responsible for matching incoming HTTP requests and dispatching those requests to the app's executable endpoints.
   




#### Route Stucture : 

``/{controller}/{action}/{id}``

#### Declaration: 
In startups.cs file : 

```C#
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }

    app.UseRouting();

    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllerRoute(
        name: "default",
        pattern: "{action: <actionname>}/{controller:<controllername>}/{id?}");
    });
}
```
**We can use annotaions instead of the declation   ** 
Example:

```C#
   [Route("api/[action]")]
   public class ProductsController : Controller
      {
         [HttpGet("{id}")]
         public IActionResult GetProduct(int id)
      {
        ...
    
      
    }
    
    [Route("api")]
   public class CtegoryController : Controller
      {
         [Route("route")]
         [ActionName("get")]
         [HttpGet("{id}")]
         public IActionResult GetCategories(int id)
      {
        ...
    
      
    }
        
```
## Passing Data from the request to the controller
### Model binding 
    ASP.NET Core MVC model binding converts client request data (form values, route data, query string parameters, HTTP headers) 
    into objects that the controller can handle
## View Component

### Razor

**@ code**: C# code 
<br/>
**@ comment @**

**@ \* Multiple <br/> lines comment \* @**

### Helpers 

@HTML.ActionLink()

@URL.Action() 

...

