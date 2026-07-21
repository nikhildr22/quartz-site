Middleware in `.NET Core` forms the HTTP request pipeline, consisting of sequential components that inspect, route, or modify incoming requests and outgoing responses. Each component chooses whether to pass the request to the next component in the chain or short-circuit the pipeline entirely.

## ⚙️ Core Mechanics

- **Delegates:** Middleware components are fundamentally request delegates configured via the `IApplicationBuilder` during application startup.
    
- **The `next` Action:** A middleware component invokes `await next(context)` to pass execution to the subsequent component in the pipeline.
    
- **Short-Circuiting:** If a middleware does _not_ call `next()`, the pipeline halts, and the response flows back out immediately.
    

## 🧰 Common Built-In Middleware

|**Middleware**|**Extension Method**|**Primary Responsibility**|
|---|---|---|
|**Exception Handling**|`UseExceptionHandler`|Catches global unhandled exceptions and formats standard API error responses.|
|**Routing**|`UseRouting`|Matches the incoming HTTP request URI to a specific controller endpoint.|
|**CORS**|`UseCors`|Applies Cross-Origin Resource Sharing policies to allow external frontend domains to access the API.|
|**Authentication**|`UseAuthentication`|Validates user identity, typically by extracting and validating a JWT token.|

## 💻 Custom Middleware Example

Implementing a custom Global Exception Handler is a frequent `.NET Core` interview requirement. It eliminates the need for repetitive `try-catch` blocks inside your API controllers.

C#

```cs
public class GlobalExceptionMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger<GlobalExceptionMiddleware> _logger;

    public GlobalExceptionMiddleware(RequestDelegate next, ILogger<GlobalExceptionMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        try
        {
            // Pass the request forward in the pipeline
            await _next(context);
        }
        catch (Exception ex)
        {
            // Intercept unhandled exceptions bubbling back up
            _logger.LogError(ex, "An unhandled exception occurred.");
            await HandleExceptionAsync(context);
        }
    }

    private static Task HandleExceptionAsync(HttpContext context)
    {
        context.Response.ContentType = "application/json";
        context.Response.StatusCode = StatusCodes.Status500InternalServerError;
        return context.Response.WriteAsJsonAsync(new { Error = "A server error occurred." });
    }
}
```

**Pro-Tip:** ⚠️ Pipeline execution order is strictly sequential and highly prone to developer error. If you place `UseAuthorization` _before_ `UseRouting` in your startup configuration, the application will fail because the route parameters required to calculate authorization boundaries have not yet been evaluated.

Custom middleware is registered via an `IApplicationBuilder` extension method to keep `Program.cs` clean and modular. Built-in middleware components handle cross-cutting infrastructure concerns and must be registered in a highly specific sequence.

## 🔌 Registering Custom Middleware

Create a static extension class for your middleware. This encapsulates the registration logic and mimics the syntax of native `.NET` methods.

C#

```cs
// 1. Define the extension method
public static class MiddlewareExtensions
{
    public static IApplicationBuilder UseGlobalExceptionHandler(this IApplicationBuilder builder)
    {
        return builder.UseMiddleware<GlobalExceptionMiddleware>();
    }
}
```

Invoke this extension method in your `Program.cs` file. Place error-handling middleware at the very top of the pipeline so it wraps all subsequent operations.

C#

```cs
// 2. Register in Program.cs
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

// Custom middleware registered first to catch all downstream exceptions
app.UseGlobalExceptionHandler(); 

app.Run();
```

## 🧱 Common Built-In Middleware & Execution Order

The order in which middleware is added to `Program.cs` dictates the exact execution order for requests and the reverse order for responses. Deviating from the standard order causes severe routing and security failures.

|**Standard Order**|**Middleware**|**Purpose**|
|---|---|---|
|**1**|`UseExceptionHandler`|Catches global errors. (Replaced by your custom handler above).|
|**2**|`UseHttpsRedirection`|Redirects HTTP requests to HTTPS.|
|**3**|`UseStaticFiles`|Serves files like HTML, CSS, and images directly, short-circuiting the rest of the pipeline.|
|**4**|`UseRouting`|Analyzes the URL to determine which endpoint should handle the request.|
|**5**|`UseCors`|Applies Cross-Origin Resource Sharing rules to allow/block frontend domains.|
|**6**|`UseAuthentication`|Identifies **who** the user is (e.g., validates a JWT token).|
|**7**|`UseAuthorization`|Determines **what** the authenticated user is allowed to do.|
|**8**|`MapControllers`|The terminal middleware that actually executes your API Controller logic.|

**Pro-Tip:** 💡 Always register `app.UseCors()` explicitly _after_ `UseRouting()` but _before_ `UseAuthorization()`. If CORS is evaluated too late, preflight `OPTIONS` requests from the browser will be blocked by the authorization layer, resulting in opaque CORS errors on the frontend.