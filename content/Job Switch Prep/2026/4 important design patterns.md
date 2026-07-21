
**SOLID** principles are the _rules_ of clean architecture; **Design Patterns** are the standardized _templates_ (solutions) used to follow those rules. In modern full-stack development, mastering four specific patterns will allow you to navigate 90% of architectural interview questions confidently.

## 🏛️ The Full-Stack Pattern Matrix

|**Pattern Name**|**Category**|**The Core Problem It Solves**|
|---|---|---|
|**Strategy**|Behavioral|Eliminates massive `if/else` or `switch` statements, satisfying the Open/Closed Principle.|
|**Repository**|Structural|Decouples your C# business logic from direct SSMS/Entity Framework database calls.|
|**Factory**|Creational|Centralizes the complex `new Object()` creation logic into one manageable location.|
|**Observer**|Behavioral|Allows UI components to react to data changes instantly (the foundation of Angular RxJS).|

## 💻 1. The Strategy Pattern (C#)

**When to use it:** When you have multiple ways to do the exact same task (e.g., calculating shipping, processing payments) and you want to swap them dynamically at runtime.

Instead of writing a massive `switch(paymentMethod)` block inside your controller, you extract the logic into separate classes that share a common interface.

C#

```cs
// 1. The unified contract
public interface IPaymentStrategy 
{
    void ProcessPayment(decimal amount);
}

// 2. Concrete implementations
public class CreditCardStrategy : IPaymentStrategy 
{
    public void ProcessPayment(decimal amount) => Console.WriteLine($"Charging CC: {amount}");
}

public class UpiStrategy : IPaymentStrategy 
{
    public void ProcessPayment(decimal amount) => Console.WriteLine($"Charging UPI: {amount}");
}

// 3. The Execution Context (Controller)
public class CheckoutService 
{
    private readonly IPaymentStrategy _strategy;
    
    // The specific strategy is injected dynamically
    public CheckoutService(IPaymentStrategy strategy) 
    {
        _strategy = strategy;
    }

    public void Checkout(decimal amount) => _strategy.ProcessPayment(amount);
}
```

## 🗂️ 2. The Repository Pattern (C#)

**When to use it:** When you need to hide the complexity of data access. It acts as an in-memory collection of domain objects, shielding your APIs from raw SQL or EF Core `DbContext` mutations.

C#

```cs
public interface IUserRepository 
{
    Task<User> GetUserByIdAsync(int id);
}

public class SqlUserRepository : IUserRepository 
{
    private readonly ApplicationDbContext _context;

    public SqlUserRepository(ApplicationDbContext context) 
    {
        _context = context;
    }

    public async Task<User> GetUserByIdAsync(int id) 
    {
        // All SSMS/EF Core specific logic is quarantined here
        return await _context.Users.FindAsync(id);
    }
}
```

## 🏗️ 3. The Factory Method (C#)

**When to use it:** When the creation of an object requires significant configuration, or when you don't know the exact type of object you need until runtime.

C#

```cs
public abstract class DocumentFactory 
{
    public abstract IDocument CreateDocument();
}

public class PdfFactory : DocumentFactory 
{
    public override IDocument CreateDocument() 
    {
        // Encapsulates complex initialization
        var pdf = new PdfDocument();
        pdf.SetSecurityMode(true);
        return pdf;
    }
}
```

## 📡 4. The Observer Pattern (Angular / TypeScript)

**When to use it:** When one part of your application updates, and multiple other separate parts need to know about it immediately without being tightly coupled. In Angular, this is managed almost entirely by `Observables` and `Subjects` in RxJS.

TypeScript

```ts
import { Subject } from 'rxjs';

export class NotificationService {
  // The Subject acts as the publisher
  private alertSource = new Subject<string>();
  
  // The Observable is what components 'subscribe' to
  public alert$ = this.alertSource.asObservable();

  // Triggers the broadcast to all listening components
  broadcastAlert(message: string) {
    this.alertSource.next(message);
  }
}
```

**Pro-Tip:** ⚠️ If an interviewer asks you about the **Singleton** pattern in .NET Core, explain that while you understand the pattern (restricting a class to a single instance), you rarely write them manually. The built-in Dependency Injection container (`builder.Services.AddSingleton<T>()`) handles this lifecycle flawlessly, making manual Singletons an anti-pattern in modern C#.

Would you like to drill into how the Strategy pattern specifically enforces the SOLID Open/Closed Principle using Dependency Injection?