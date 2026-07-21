SOLID is a set of five architectural principles designed to reduce code coupling, increase maintainability, and isolate failure domains. Implementing these in a `.NET` backend transforms brittle monolithic architectures into scalable, testable systems.

## 🧠 The Mnemonic Table

| Letter | Principle | Quick Definition (The "Easy Way") |
| --- | --- | --- |
| **S** | **Single Responsibility Principle (SRP)** | A class should have only one reason to change. *(Do one thing).* |
| **O** | **Open/Closed Principle (OCP)** | Open for extension, closed for modification. *(Add features via new classes, not by editing old ones).* |
| **L** | **Liskov Substitution Principle (LSP)** | Derived classes must be substitutable for their base classes. *(Don't break expected behavior in inheritance).* |
| **I** | **Interface Segregation Principle (ISP)** | Clients shouldn't be forced to depend on methods they don't use. *(Keep interfaces lean).* |
| **D** | **Dependency Inversion Principle (DIP)** | High-level modules should not depend on low-level modules; both should depend on abstractions. *(Rely on interfaces/DI).* |

## 💻 C# .NET Backend Examples

### Single Responsibility Principle (SRP)

**Bad:** A `UserController` that handles HTTP routing, validates passwords, and directly executes `SMTP` logic to send welcome emails.
**Good:** Delegate to dedicated services.

```csharp
public class UserController : ControllerBase
{
    private readonly IUserService _userService;
    private readonly IEmailService _emailService;

    // Controller only routes data. Business logic and email execution are segregated.
    public UserController(IUserService userService, IEmailService emailService)
    {
        _userService = userService;
        _emailService = emailService;
    }
}

```

### Open/Closed Principle (OCP)

**Bad:** Using a massive `switch` statement to calculate billing discounts based on user tier, forcing you to modify the method every time a new tier is added.
**Good:** Implement an interface so new tiers can be added without modifying existing code.

```csharp
public interface IDiscountStrategy
{
    decimal CalculateDiscount(decimal total);
}

public class PremiumDiscount : IDiscountStrategy
{
    public decimal CalculateDiscount(decimal total) => total * 0.8m;
}
// To add a 'VIP' discount later, simply create a new class implementing IDiscountStrategy.

```

### Liskov Substitution Principle (LSP)

**Bad:** Creating a `ReadOnlyDatabaseConnection` class that inherits from `DatabaseConnection` but throws a `NotImplementedException` when `.Write()` is called.
**Good:** Ensure the base contract is honored universally.

```csharp
public abstract class DocumentCache
{
    public abstract string GetCachedDocument(string id);
}

public class RedisDocumentCache : DocumentCache
{
    // Must behave exactly as the consuming client expects from DocumentCache without throwing unexpected exceptions.
    public override string GetCachedDocument(string id) => RedisDb.GetString(id);
}

```

The **Liskov Substitution Principle (LSP)** states that objects of a superclass must be replaceable with objects of a subclass without breaking the application. We need it to guarantee predictable system behavior, prevent unexpected runtime crashes, and ensure `.NET Core` dependency injection can safely supply any derived implementation.

## ⚠️ Why We Need LSP

* **Contract Integrity:** Subclasses must honor the exact input/output rules and side effects defined by the parent abstraction.
* **Safe Polymorphism:** A consumer calling a method on a base type should not need to know the specific derived type executing the logic.
* **Exception Prevention:** Prevents runtime errors like `NotSupportedException` when a derived class refuses to implement inherited base behaviors.

## ❌ LSP Violation: EF Core & MSSQL View

In this scenario, a repository mapping to a read-only `MSSQL` View inherits from a base repository designed for standard tables. It breaks LSP because any service expecting the base `Repository<T>` contract will crash when calling `AddAsync`.

```csharp
// Base class expecting read/write capability to MSSQL tables
public class Repository<T> where T : class
{
    protected readonly ApplicationDbContext _context;
    public Repository(ApplicationDbContext context) => _context = context;

    public virtual async Task AddAsync(T entity)
    {
        await _context.Set<T>().AddAsync(entity);
        await _context.SaveChangesAsync();
    }
}

// Derived class mapping to an MSSQL View
public class ReportViewRepository : Repository<ReportView>
{
    public ReportViewRepository(ApplicationDbContext context) : base(context) {}

    // LSP VIOLATION: The subclass alters expected behavior by throwing an exception.
    public override async Task AddAsync(ReportView entity)
    {
        throw new NotSupportedException("Cannot insert into a read-only MSSQL View.");
    }
}

```

## ✅ LSP Compliant Solution

To fix this, segregate the inheritance hierarchy. The base class only defines behaviors common to all derived classes (reading data). Write operations are isolated to a more specific subclass.

```csharp
// Base contract strictly for reading (applies to both Tables and Views)
public abstract class ReadRepository<T> where T : class
{
    protected readonly ApplicationDbContext _context;
    public ReadRepository(ApplicationDbContext context) => _context = context;

    public virtual async Task<List<T>> GetAllAsync() 
    {
        return await _context.Set<T>().AsNoTracking().ToListAsync();
    }
}

// Writable repository safely inherits read capabilities and adds writes
public class WriteRepository<T> : ReadRepository<T> where T : class
{
    public WriteRepository(ApplicationDbContext context) : base(context) {}

    // No exceptions thrown; contract is fully honored.
    public virtual async Task AddAsync(T entity)
    {
        await _context.Set<T>().AddAsync(entity);
        await _context.SaveChangesAsync();
    }
}

```

**Pro-Tip:** 💡 When using EF Core's `Table-per-Hierarchy (TPH)` inheritance structure in `MSSQL`, an LSP violation often manifests when querying a base entity type but attempting to update a column that only exists on a specific discriminator subtype, causing silent data truncation or `DbUpdateException`. Ensure your base entity definitions strictly contain universally shared properties.
#### how to answer interviwer
Explain LSP as a guarantee of architectural predictability and contract integrity. Interviewers look for you to connect the theoretical definition to real-world .NET runtime safety, specifically concerning Dependency Injection.

🗣️ The 3-Step Interview Script
1. The Formal Definition: "LSP means that a derived class must be seamlessly substitutable for its base class without altering the correctness of the program."

2. The Practical Translation: "In practice, it means subclasses must honor the behavioral contract of their parents. They cannot throw unexpected exceptions or require the consumer to check their specific type before calling a method."

3. The .NET Context: "This is critical in .NET Core because of Dependency Injection. If a consumer requests an IRepository from the DI container, it must be able to safely use any registered implementation without knowing the concrete type."

🛑 The "Red Flag" Example to Share
Use the NotImplementedException anti-pattern as your core example; it proves you understand how LSP fails in enterprise codebases.

The Scenario: "Imagine a base SqlRepository with a Delete() method. A developer creates a SqlArchiveRepository inheriting from it, but overrides Delete() to throw a NotSupportedException because archives shouldn't be deleted."

The Consequence: "When the DI container injects SqlArchiveRepository into a background cleanup service expecting the base type, the service crashes at runtime."

The Solution: "I would fix this by segregating the interfaces into IReadRepository and IWriteRepository so the archive class never inherits a Delete() method it cannot fulfill."

Pro-Tip: 💡 If the interviewer brings up the classic "Square/Rectangle" or "Bird/Penguin" examples, acknowledge them but pivot quickly. State that while analogies are fine for textbooks, in your professional .NET experience, LSP violations almost always manifest as a NotImplementedException injected into an unsuspecting service.

### Interface Segregation Principle (ISP)

**Bad:** A monolithic `IUserRepository` containing `Get()`, `Add()`, and `Delete()` forced onto a reporting microservice that only needs to read data.
**Good:** Split into granular interfaces.

```csharp
public interface IReadRepository<T>
{
    Task<T> GetByIdAsync(int id);
}

public interface IWriteRepository<T>
{
    Task AddAsync(T entity);
}
// A reporting service only needs to inject IReadRepository, minimizing its dependency footprint.

```

### Dependency Inversion Principle (DIP)

**Bad:** Hardcoding a database connection instantiation (`new SqlConnection()`) directly inside a repository method.
**Good:** Injecting abstractions via the `.NET Core` built-in Dependency Injection container.

```csharp
public class OrderProcessor
{
    private readonly IMessageQueue _queue;

    // Depends on the abstraction (IMessageQueue), not a concrete RabbitMQ or Azure Service Bus instance.
    public OrderProcessor(IMessageQueue queue)
    {
        _queue = queue;
    }
}

```

**Pro-Tip:** ⚠️ Over-engineering SOLID principles (especially OCP and ISP) prematurely can lead to "interface explosion" where you have more files than actual logic. Apply these heavily at system boundaries (e.g., WebAPIs, database access layers) and refactor internal logic into SOLID patterns only when that specific code begins to change frequently.