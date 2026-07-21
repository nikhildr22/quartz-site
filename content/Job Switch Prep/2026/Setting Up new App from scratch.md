1. create empty solution
2. create multiple projects
	1. api
		1. asp net core web api
	2. domain
		1. class library
	3. application
		1. class library
	4. infrastructure
		1. class library


### Step 3 — Set Up Project References

The dependency flow is one-way:

```
Api → Application → Domain
Infrastructure → Domain
Api → Infrastructure (for DI registration)
```

In VS: right-click a project → **Add → Project Reference** → check the appropriate project.

Starting: *Generate Domain layer code* (2/5)

I now have a clear picture of the exact patterns. Here is the complete final code for TaskTracker, mirroring this project's conventions exactly.

---

## Domain Layer — `TaskTracker.Domain`

### `Entities/TodoEntity.cs`
```csharp
namespace TaskTracker.Domain.Entities
{
    public class TodoEntity
    {
        /// <summary>
        /// Gets or sets the Id of the Todo.
        /// </summary>
        public Guid Id { get; set; }

        /// <summary>
        /// Gets or sets the title of the Todo.
        /// </summary>
        public string Title { get; set; } = string.Empty;

        /// <summary>
        /// Gets or sets whether the Todo is completed.
        /// </summary>
        public bool IsCompleted { get; set; }

        /// <summary>
        /// Gets or sets the date the Todo was created.
        /// </summary>
        public DateTime CreatedAt { get; set; }
    }
}
```

### `Models/Services/Todo/TodoBaseModel.cs`
```csharp
namespace TaskTracker.Domain.Models.Services.Todo
{
    public class TodoBaseModel
    {
        public string Title { get; set; } = string.Empty;
        public bool IsCompleted { get; set; }
    }
}
```

### `Models/Services/Todo/TodoModel.cs`
```csharp
namespace TaskTracker.Domain.Models.Services.Todo
{
    public class TodoModel : TodoBaseModel
    {
        public Guid Id { get; set; }
        public DateTime CreatedAt { get; set; }
    }
}
```

### `Models/Services/Todo/TodoSaveModel.cs`
```csharp
namespace TaskTracker.Domain.Models.Services.Todo
{
    public class TodoSaveModel : TodoBaseModel
    {
        public Guid? Id { get; set; }
    }
}
```

### `Interfaces/Services/ITodoService.cs`
```csharp
using TaskTracker.Domain.Models.Services.Todo;

namespace TaskTracker.Domain.Interfaces.Services
{
    /// <summary>
    /// Service with all functionality for Todos
    /// </summary>
    public interface ITodoService
    {
        /// <summary>
        /// Gets all Todos
        /// </summary>
        /// <param name="cancellationToken">Token to cancel the request</param>
        /// <returns>All Todos</returns>
        Task<List<TodoModel>> GetAllAsync(CancellationToken cancellationToken = default);

        /// <summary>
        /// Gets a single Todo by id
        /// </summary>
        /// <param name="id">Identifier of the Todo</param>
        /// <param name="cancellationToken">Token to cancel the request</param>
        /// <returns>Todo with the specified id</returns>
        Task<TodoModel> GetAsync(Guid id, CancellationToken cancellationToken = default);

        /// <summary>
        /// Saves a single Todo to the database
        /// </summary>
        /// <param name="model">Model with new values for the Todo</param>
        /// <param name="cancellationToken">Token to cancel the request</param>
        /// <returns>Entity of the saved Todo</returns>
        Task<TodoEntity> SaveAsync(TodoSaveModel model, CancellationToken cancellationToken = default);

        /// <summary>
        /// Deletes a Todo
        /// </summary>
        /// <param name="id">Identifier of the Todo</param>
        /// <param name="cancellationToken">Token to cancel the request</param>
        /// <returns>Nothing</returns>
        Task DeleteAsync(Guid id, CancellationToken cancellationToken = default);
    }
}
```

### `Interfaces/Data/ITaskTrackerDbContext.cs`
```csharp
using Microsoft.EntityFrameworkCore;
using TaskTracker.Domain.Entities;

namespace TaskTracker.Domain.Interfaces.Data
{
    public interface ITaskTrackerDbContext
    {
        DbSet<TodoEntity> Todos { get; }
        Task<int> SaveChangesAsync(CancellationToken cancellationToken = default);
    }
}
```

---

## Infrastructure Layer — `TaskTracker.Infrastructure`

> Install NuGet: `Microsoft.EntityFrameworkCore.SqlServer`, `Microsoft.EntityFrameworkCore.Tools`

### `Data/TaskTrackerDbContext.cs`
```csharp
using Microsoft.EntityFrameworkCore;
using TaskTracker.Domain.Entities;
using TaskTracker.Domain.Interfaces.Data;

namespace TaskTracker.Infrastructure.Data
{
    public class TaskTrackerDbContext : DbContext, ITaskTrackerDbContext
    {
        public TaskTrackerDbContext(DbContextOptions<TaskTrackerDbContext> options)
            : base(options)
        {
        }

        public DbSet<TodoEntity> Todos { get { return Set<TodoEntity>(); } }
    }
}
```

---

## Application Layer — `TaskTracker.Application`

### `Projections/TodoEntityProjections.cs`
```csharp
using System.Linq.Expressions;
using TaskTracker.Domain.Entities;
using TaskTracker.Domain.Models.Services.Todo;

namespace TaskTracker.Application.Projections
{
    public static class TodoEntityProjections
    {
        /// <summary>
        /// Projection to get a TodoModel from a TodoEntity
        /// </summary>
        public static Expression<Func<TodoEntity, TodoModel>> GetTodoModelProjection()
        {
            return todo => new TodoModel
            {
                Id = todo.Id,
                Title = todo.Title,
                IsCompleted = todo.IsCompleted,
                CreatedAt = todo.CreatedAt
            };
        }
    }
}
```

### `Services/TodoService.cs`
```csharp
using Microsoft.EntityFrameworkCore;
using TaskTracker.Application.Projections;
using TaskTracker.Domain.Entities;
using TaskTracker.Domain.Interfaces.Data;
using TaskTracker.Domain.Interfaces.Services;
using TaskTracker.Domain.Models.Services.Todo;

namespace TaskTracker.Application.Services
{
    /// <inheritdoc />
    public class TodoService : ITodoService
    {
        private readonly ITaskTrackerDbContext dbContext;

        public TodoService(ITaskTrackerDbContext dbContext)
        {
            this.dbContext = dbContext;
        }

        /// <inheritdoc />
        public async Task<List<TodoModel>> GetAllAsync(CancellationToken cancellationToken = default)
        {
            return await dbContext.Todos
                .Select(TodoEntityProjections.GetTodoModelProjection())
                .OrderBy(todo => todo.CreatedAt)
                .ToListAsync(cancellationToken);
        }

        /// <inheritdoc />
        public async Task<TodoModel> GetAsync(Guid id, CancellationToken cancellationToken = default)
        {
            return await dbContext.Todos
                .Select(TodoEntityProjections.GetTodoModelProjection())
                .SingleAsync(todo => todo.Id == id, cancellationToken);
        }

        /// <inheritdoc />
        public async Task<TodoEntity> SaveAsync(TodoSaveModel model, CancellationToken cancellationToken = default)
        {
            TodoEntity? entity = null;

            if (model.Id.HasValue)
            {
                entity = await dbContext.Todos
                    .SingleOrDefaultAsync(todo => todo.Id == model.Id, cancellationToken);
            }

            if (entity == null)
            {
                entity = new TodoEntity
                {
                    Id = Guid.NewGuid(),
                    CreatedAt = DateTime.UtcNow
                };
                await dbContext.Todos.AddAsync(entity, cancellationToken);
            }

            entity.Title = model.Title;
            entity.IsCompleted = model.IsCompleted;

            await dbContext.SaveChangesAsync(cancellationToken);

            return entity;
        }

        /// <inheritdoc />
        public async Task DeleteAsync(Guid id, CancellationToken cancellationToken = default)
        {
            var entity = await dbContext.Todos
                .SingleAsync(todo => todo.Id == id, cancellationToken);

            dbContext.Todos.Remove(entity);
            await dbContext.SaveChangesAsync(cancellationToken);
        }
    }
}
```

---

## API Layer — `TaskTracker.Api`

> Install NuGet in `TaskTracker.Infrastructure`: `Microsoft.EntityFrameworkCore.Design`  
> Install NuGet in `TaskTracker.Api`: `Microsoft.EntityFrameworkCore.Design`

### `Controllers/TodoController.cs`
```csharp
using Microsoft.AspNetCore.Mvc;
using TaskTracker.Domain.Interfaces.Services;
using TaskTracker.Domain.Models.Services.Todo;

namespace TaskTracker.Api.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class TodoController : ControllerBase
    {
        private readonly ITodoService todoService;

        public TodoController(ITodoService todoService)
        {
            this.todoService = todoService;
        }

        /// <summary>
        /// Gets all Todos
        /// </summary>
        /// <param name="cancellationToken">Token to cancel request</param>
        /// <returns>List of all Todos</returns>
        [HttpGet("[action]")]
        public async Task<ActionResult<List<TodoModel>>> GetAllAsync(CancellationToken cancellationToken)
        {
            return await todoService.GetAllAsync(cancellationToken);
        }

        /// <summary>
        /// Gets a single Todo by id
        /// </summary>
        /// <param name="id">Id of the Todo</param>
        /// <param name="cancellationToken">Token to cancel request</param>
        /// <returns>Model of the specific Todo</returns>
        [HttpGet("{id:guid}")]
        public async Task<ActionResult<TodoModel>> GetAsync(Guid id, CancellationToken cancellationToken)
        {
            return await todoService.GetAsync(id, cancellationToken);
        }

        /// <summary>
        /// Saves a Todo (create or update)
        /// </summary>
        /// <param name="model">Model with values to save</param>
        /// <param name="cancellationToken">Token to cancel request</param>
        /// <returns>The saved Todo model</returns>
        [HttpPost("[action]")]
        public async Task<ActionResult<TodoModel>> SaveAsync([FromBody] TodoSaveModel model, CancellationToken cancellationToken)
        {
            var entity = await todoService.SaveAsync(model, cancellationToken);
            return await todoService.GetAsync(entity.Id, cancellationToken);
        }

        /// <summary>
        /// Deletes a Todo by id
        /// </summary>
        /// <param name="id">Id of the Todo to delete</param>
        /// <param name="cancellationToken">Token to cancel request</param>
        /// <returns>Status code 200 if successful</returns>
        [HttpDelete("{id:guid}")]
        public async Task<ActionResult> DeleteAsync(Guid id, CancellationToken cancellationToken)
        {
            await todoService.DeleteAsync(id, cancellationToken);
            return Ok();
        }
    }
}
```

### `Program.cs`
```csharp
using Microsoft.EntityFrameworkCore;
using TaskTracker.Application.Services;
using TaskTracker.Domain.Interfaces.Data;
using TaskTracker.Domain.Interfaces.Services;
using TaskTracker.Infrastructure.Data;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

// Register DbContext
builder.Services.AddDbContext<TaskTrackerDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));

// Register DbContext interface
builder.Services.AddScoped<ITaskTrackerDbContext>(provider =>
    provider.GetRequiredService<TaskTrackerDbContext>());

// Register services
builder.Services.AddScoped<ITodoService, TodoService>();

var app = builder.Build();

app.UseSwagger();
app.UseSwaggerUI();

app.UseAuthorization();
app.MapControllers();
app.Run();
```

### `appsettings.json` — add connection string
```json
"ConnectionStrings": {
  "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=TaskTrackerDb;Trusted_Connection=True;"
}
```

---

## Migration

Open **Package Manager Console**, set Default Project to `TaskTracker.Infrastructure`, run:
```
Add-Migration InitialCreate -StartupProject TaskTracker.Api
Update-Database -StartupProject TaskTracker.Api
```

Then press **F5** — Swagger opens at `/swagger` with all endpoints ready to test.

--- 

Completed: *Generate Domain layer code* (2/5)

**Key patterns this mirrors from the real project:**

| Pattern | Source project | Your TaskTracker |
|---|---|---|
| Namespace with `{ }` braces | ✓ | ✓ |
| `TodoBaseModel` → `TodoModel` / `TodoSaveModel` | ✓ | ✓ |
| Interface `ITaskTrackerDbContext` abstracted | ✓ | ✓ |
| `DbSet` via `get { return Set<>() }` | ✓ | ✓ |
| Constructor injection with `this.field = param` | ✓ | ✓ |
| Static `Projections` class with `Expression<Func<>>` | ✓ | ✓ |
| XML `<summary>` comments on interface + controller | ✓ | ✓ |
| `[HttpPost("[action]")]` route style | ✓ | ✓ |
| `CancellationToken` on all async methods | ✓ | ✓ |
| `SaveAsync` returns entity, controller re-fetches model | ✓ | ✓ |

This is because `(localdb)\mssqllocaldb` is a **LocalDB** instance — it's separate from the regular SQL Server instance shown in SSMS by default.

## How to Connect to LocalDB in SSMS

1. Open SSMS
2. In the **Connect to Server** dialog, enter exactly:
   ```
   (localdb)\mssqllocaldb
   ```
3. Authentication: **Windows Authentication**
4. Click **Connect**

You should then see `TaskTrackerDb` under **Databases**.

---

## If You Prefer a Regular SQL Server Instance

Change your connection string in `appsettings.json` to point to your actual SQL Server instance:

```json
"ConnectionStrings": {
  "DefaultConnection": "Server=localhost;Database=TaskTrackerDb;Trusted_Connection=True;TrustServerCertificate=True;"
}
```

Then in PMC run:
```
Update-Database -StartupProject TaskTracker.Api
```

This creates the database on your main SQL Server instance which is visible in SSMS under the default connection.

---

**Quick check** — to confirm LocalDB is working, run this in PMC:
```
dotnet ef database update --project TaskTracker.Infrastructure --startup-project TaskTracker.Api
```
If it says `Done` with no errors, the DB exists — you just need to connect via `(localdb)\mssqllocaldb` in SSMS.

## How Dependency Injection Works in Your `Program.cs`

```csharp
// Register DbContext
builder.Services.AddDbContext<TaskTrackerDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));

// Register DbContext interface
builder.Services.AddScoped<ITaskTrackerDbContext>(provider =>
    provider.GetRequiredService<TaskTrackerDbContext>());

// Register services
builder.Services.AddScoped<ITodoService, TodoService>();
```

### What's happening line by line

**`builder.Services`** is the **DI container** — a dictionary that maps "I need X" → "give them Y".

**`AddDbContext<TaskTrackerDbContext>`** tells the container:
> "When anyone needs a `TaskTrackerDbContext`, create one using SQL Server with this connection string."

**`AddScoped<ITaskTrackerDbContext>(...)`** tells the container:
> "When anyone asks for the **interface** `ITaskTrackerDbContext`, resolve it by getting the already-registered `TaskTrackerDbContext`."

This is why your `TodoService` constructor takes `ITaskTrackerDbContext` (the interface) not the concrete class — it never depends on the implementation directly.

**`AddScoped<ITodoService, TodoService>`** tells the container:
> "When anyone asks for `ITodoService`, create a `TodoService` and inject its constructor dependencies automatically."

So when `TodoController` asks for `ITodoService`, the container:
1. Creates `TodoService`
2. Sees its constructor needs `ITaskTrackerDbContext`
3. Resolves that to `TaskTrackerDbContext`
4. Injects it — all automatically

---

## The 3 Lifetime Options (Important for Interviews)

| Lifetime | Method | Created | Destroyed |
|---|---|---|---|
| **Transient** | `AddTransient` | Every time it's requested | Immediately after use |
| **Scoped** | `AddScoped` | Once per HTTP request | End of request |
| **Singleton** | `AddSingleton` | Once ever | App shutdown |

**Rule of thumb:** Services with database access → `Scoped`. Stateless helpers → `Transient`. App-wide shared state → `Singleton`.

---

## Full `Program.cs` Explained — What Every Line Does

```csharp
var builder = WebApplication.CreateBuilder(args);
```
Creates the **app builder** — sets up configuration (reads `appsettings.json`, env vars, command-line args) and prepares the DI container.

---

```csharp
builder.Services.AddControllers();
```
Registers support for `[ApiController]` classes. Without this, your `TodoController` would never be found.

---

```csharp
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();
```
Registers Swagger — `AddEndpointsApiExplorer` lets Swagger discover your endpoints, `AddSwaggerGen` generates the JSON spec from them.

---

```csharp
builder.Services.AddDbContext<TaskTrackerDbContext>(...);
builder.Services.AddScoped<ITaskTrackerDbContext>(...);
builder.Services.AddScoped<ITodoService, TodoService>();
```
Your DI registrations — covered above.

---

```csharp
var app = builder.Build();
```
**Builds** the app from all the registrations. After this line, the DI container is locked — you can no longer register services.

---

```csharp
app.UseSwagger();
app.UseSwaggerUI();
```
Adds Swagger to the **middleware pipeline**. Middleware runs on every request in order — this makes `/swagger` available.

---

```csharp
app.UseAuthorization();
```
Adds the authorization middleware. Checks `[Authorize]` attributes on controllers. Must come after `UseAuthentication()` if you add auth later.

---

```csharp
app.MapControllers();
```
Tells the app to route HTTP requests to your controller actions based on `[Route]` and `[Http*]` attributes.

---

```csharp
app.Run();
```
Starts the web server and blocks until the app shuts down.

---

## The Mental Model for Interviews

```
Program.cs has two phases:

PHASE 1 — builder.*    → Register everything (DI, middleware config)
                        └── builder.Services.*  = DI registrations
                        └── builder.Configuration.* = read config

PHASE 2 — app.*        → Build the request pipeline
                        └── app.Use*()  = add middleware (runs on every request)
                        └── app.Map*()  = add routing
                        └── app.Run()   = start the server
```


The app is running but you're hitting the root `/` which has no route. You need to navigate to `/swagger` explicitly.

Try this URL in your browser:
```
https://localhost:44360/swagger
```

---

## Why the Root URL Returns 404

Your `Program.cs` only maps controllers and Swagger — there is no route registered for `/`. This is normal for a Web API project. The valid URLs are:

| URL | What it does |
|---|---|
| `https://localhost:44360/swagger` | Swagger UI |
| `https://localhost:44360/api/Todo/GetAll` | Your API endpoint |

---

## Optional — Redirect Root to Swagger

If you want `https://localhost:44360/` to automatically open Swagger, add this to `Program.cs` before `app.Run()`:

```csharp
app.MapGet("/", () => Results.Redirect("/swagger"));
```

