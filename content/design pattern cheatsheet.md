If you only have **5 minutes**, don't try to learn all 23 GoF patterns. For a typical .NET interview, you only need to know the ones you see in real ASP.NET Core projects.

Here's the cheat sheet.

---

# 1. Singleton ⭐⭐⭐⭐⭐

### Problem

You only want **one instance** of an object.

Example

* Logger
* Configuration
* Cache

```csharp
public sealed class Logger
{
    private static readonly Logger _instance = new Logger();

    private Logger() { }

    public static Logger Instance => _instance;
}
```

Usage

```csharp
Logger.Instance;
```

### Real ASP.NET Core

```csharp
builder.Services.AddSingleton<IMyService, MyService>();
```

Interview answer

> Singleton ensures only one instance of a class exists throughout the application's lifetime.

---

# 2. Factory ⭐⭐⭐⭐⭐

Instead of

```csharp
Car car = new Car();
```

Use

```csharp
VehicleFactory.Create("Car");
```

Example

```csharp
interface IVehicle
{
    void Drive();
}

class Car : IVehicle
{
    public void Drive() => Console.WriteLine("Car");
}

class Bike : IVehicle
{
    public void Drive() => Console.WriteLine("Bike");
}

class VehicleFactory
{
    public static IVehicle Create(string type)
    {
        return type switch
        {
            "Car" => new Car(),
            "Bike" => new Bike(),
            _ => throw new Exception()
        };
    }
}
```

Interview answer

> Factory encapsulates object creation so clients don't need to know which concrete class to instantiate.

---

# 3. Dependency Injection ⭐⭐⭐⭐⭐

Probably the most important one.

Instead of

```csharp
class UserService
{
    EmailService email = new EmailService();
}
```

Do

```csharp
class UserService
{
    private readonly IEmailService _email;

    public UserService(IEmailService email)
    {
        _email = email;
    }
}
```

ASP.NET Core

```csharp
builder.Services.AddScoped<IEmailService, EmailService>();
```

Interview answer

> Dependency Injection follows the Dependency Inversion Principle by injecting dependencies instead of creating them inside the class, making the code loosely coupled and easier to test.

---

# 4. Repository ⭐⭐⭐⭐☆

Instead of controller talking directly to EF Core.

```text
Controller

↓

Repository

↓

DbContext

↓

Database
```

Example

```csharp
public interface IUserRepository
{
    User Get(int id);
}
```

Interview answer

> Repository abstracts data access so business logic doesn't depend directly on the database implementation.

---

# 5. Strategy ⭐⭐⭐⭐☆

Very common interview question.

Problem

Different algorithms.

Example

Payment

```text
Credit Card

UPI

PayPal
```

Interface

```csharp
interface IPayment
{
    void Pay();
}
```

Implementations

```csharp
class CardPayment : IPayment { }

class UpiPayment : IPayment { }
```

Usage

```csharp
IPayment payment = new CardPayment();

payment.Pay();
```

Interview answer

> Strategy lets you switch algorithms at runtime without changing the client code.

---

# 6. Builder ⭐⭐⭐⭐☆

Problem

Constructor has 15 parameters.

Instead of

```csharp
new Employee(a,b,c,d,e,f,g,h...)
```

Use

```csharp
EmployeeBuilder
    .SetName("John")
    .SetAge(25)
    .SetSalary(50000)
    .Build();
```

Interview answer

> Builder constructs complex objects step by step.

---

# 7. Observer ⭐⭐⭐⭐☆

This is basically **events**.

```text
Publisher

↓

Subscribers
```

Example

```csharp
public event Action OnCompleted;
```

When event occurs

```csharp
OnCompleted?.Invoke();
```

Interview answer

> Observer notifies multiple subscribers automatically when an event occurs.

---

# 8. Decorator ⭐⭐⭐☆☆

Add behavior without modifying the class.

Example

```text
Coffee

↓

Milk

↓

Sugar
```

ASP.NET Core Middleware is similar.

Request

```text
Request

↓

Logging

↓

Authentication

↓

Exception Handling

↓

Controller
```

Each middleware decorates the next.

---

# 9. Adapter ⭐⭐⭐☆☆

Makes incompatible classes work together.

Example

```text
USB-C

↓

Adapter

↓

HDMI
```

Interview answer

> Adapter converts one interface into another expected by the client.

---

# 10. MVC (Kind of a Pattern)

Controller

↓

Service

↓

Repository

↓

Database

Know this because interviewers often ask about architecture patterns alongside design patterns.

---

# Design Patterns Used in ASP.NET Core

| Pattern              | Example                                   |
| -------------------- | ----------------------------------------- |
| Singleton            | `AddSingleton()`                          |
| Factory              | `ILoggerFactory`, `IHttpClientFactory`    |
| Dependency Injection | Built-in DI container                     |
| Repository           | Data access layer                         |
| Strategy             | Authentication schemes, payment providers |
| Observer             | Events and delegates                      |
| Decorator            | Middleware pipeline                       |
| Builder              | `WebApplicationBuilder`, `HostBuilder`    |

---

# 30-Second Interview Answer

If they ask:

> **Tell me some design patterns you've used.**

You can say:

> "In ASP.NET Core, I commonly use Dependency Injection for loose coupling, the Repository pattern to abstract data access, Singleton for shared services like caching or configuration, Strategy when different implementations are selected at runtime, such as payment providers, and Factory for object creation. The middleware pipeline is also an example of the Decorator pattern because each middleware wraps the next component in the request pipeline."

---

# If you have only 5 minutes, memorize these 5

| Pattern                  | One-line definition                           |
| ------------------------ | --------------------------------------------- |
| **Dependency Injection** | Inject dependencies instead of creating them. |
| **Singleton**            | Only one instance exists.                     |
| **Factory**              | Encapsulates object creation.                 |
| **Repository**           | Abstracts data access from business logic.    |
| **Strategy**             | Swap algorithms at runtime.                   |

These five cover the majority of design pattern discussions in .NET backend interviews, especially for junior to mid-level roles.
