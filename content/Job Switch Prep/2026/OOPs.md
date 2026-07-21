## BLUF

For a C# Full-Stack interview, you don't need to recite textbook definitions. You need to explain the **4 Pillars of OOP** through their real-world purpose (why we use them) and their C#-specific mechanics (how we code them).

## 🧠 The "Smart Factory" Analogy

To easily remember OOP, think of your code as a **Smart Automated Factory**:

1. **Encapsulation:** The internal gears of a machine are sealed inside a safety capsule. Users only interact with a dashboard, preventing them from breaking the machine.
    
2. **Abstraction:** The factory floor has a simple "Start Engine" button. You don't need to know the thermodynamics of the engine to turn it on.
    
3. **Inheritance:** The factory designs a "Standard Conveyor Belt" blueprint. When they need a "Chilled Conveyor Belt," they just copy the standard blueprint and add a cooling fan instead of designing it from scratch.
    
4. **Polymorphism:** The factory outlet has a universal power socket. Whether you plug in a drill, a fan, or a laptop, they all react differently to the same power supply.
    

## 🏛️ The 4 Pillars: Deep Dive for Interviews

### 1. Encapsulation (Data Hiding & Protection)

- **What it means:** Grouping data (properties) and methods into a single unit (class) and restricting direct access to prevent corruption.
    
- **How C# does it:** Using **Access Modifiers** (`private`, `public`, `protected`, `internal`) and **Properties** with `get` and `set` accessors.
    

C#

```csharp
public class BankAccount
{
    // Hidden from outside world to prevent fraud
    private decimal _balance; 

    // Controlled gateway
    public decimal Balance 
    {
        get => _balance;
        // Enforces business rules before mutating state
        set 
        {
            if (value >= 0) _balance = value; 
        }
    }
}
```

### 2. Abstraction (Hiding Complexity)

- **What it means:** Showing only essential features to the outside world and hiding the messy implementation details.
    
- **How C# does it:** Using **Interfaces** and **Abstract Classes**.
    

C#

```csharp
// The caller only cares THAT an email can be sent, not HOW.
public interface IEmailService
{
    Task SendEmailAsync(string to, string subject, string body);
}

public class SendGridEmailService : IEmailService
{
    public async Task SendEmailAsync(string to, string subject, string body)
    {
        // 50 lines of complex SendGrid API connection logic hidden away here...
    }
}
```

### 3. Inheritance (Code Reuse)

- **What it means:** Allowing a new class (child) to adopt the properties and behaviors of an existing class (parent).
    
- **How C# does it:** Using the `:` operator. C# only supports **single inheritance** for classes (a class can only inherit from one parent class, but can implement multiple interfaces).
    

C#

```csharp
// Parent Class
public class Employee
{
    public string Name { get; set; }
    public decimal BaseSalary { get; set; }
}

// Child Class inherits Name and BaseSalary automatically
public class Consultant : Employee
{
    public decimal HourlyRate { get; set; }
}
```

### 4. Polymorphism (Many Forms)

- **What it means:** The ability of different types to be treated as the same base type, yet execute their own specific behaviors.
    
- **How C# does it:** 
	* **Static (Compile-time):** ==Method Overloading== (same name, different parameters).
    
    - **Dynamic (Runtime):** ==Method Overriding== (using `virtual` in the parent and `override` in the child).



C#

```csharp
public class PaymentProcessor
{
    // Virtual allows child classes to change this behavior
    public virtual void Process() => Console.WriteLine("Processing standard payment.");
}

public class CreditCardProcessor : PaymentProcessor
{
    // Override replaces the parent behavior at runtime
    public override void Process() => Console.WriteLine("Processing secure Credit Card transaction.");
}
```

## 🎙️ Tricky Interview Questions to Master

**Q: What is the difference between Method Overriding and Method Hiding (`new` keyword)?** **A:** **Overriding** utilizes virtual dispatch; if you store a child object in a parent reference variable (e.g., `Notification alert = new EmailNotification();`), calling `.Send()` will still run the _child's_ overridden version. **Method Hiding** breaks this link. If you use the `new` keyword in the child class instead of `override`, calling the method on a parent reference variable will execute the _parent's_ base version instead of the child's.

**Q: What is the relationship between Polymorphism and Dependency Inversion?** **A:** Polymorphism is the technical engine that makes Dependency Inversion (the D in SOLID) work. By writing controllers or classes that depend on an interface abstract definition (like `IEmailService`), polymorphism allows us to swap the real runtime object instance seamlessly during dependency injection without changing a single line of code in our business controller.

**Pro-Tip:** 🚀 If an interviewer asks you how to optimize a piece of code that has a giant `switch` statement checking an enum type (like `switch(paymentType)`), tell them: _"That is a code smell violating the Open/Closed Principle. I would refactor that switch statement away by implementing **Runtime Polymorphism**, moving each block of switch logic into its own derived strategy class overriding a base method."_

## 🎯 What Interviewers Look For (Baseline Checklist)

To clear the technical screening, you must be ready to talk about:

- **Classes vs. Objects:** A class is the blueprint (the blueprint of a car); an object is the instance created in memory (the physical car parked in the driveway).
    
- **The `virtual` keyword:** Interviewers love asking this. It tells the compiler, _"Hey, look downstream at runtime to see if a child class has a better version of this method."_
    
- **Interface vs. Abstract Class:** * An **Interface** is a contract ("What a class can do"). It cannot store state (no fields).
    
    - An **Abstract Class** defines an identity ("What a class is"). It _can_ store state, have constructors, and supply default logic.
        

## 🎙️ Tricky Interview Questions to Master

**Q: Can you create an instance of an Abstract Class or an Interface?**

**A:** No. They are incomplete blueprints. You can only instantiate concrete classes that implement or inherit them. However, you _can_ create a reference variable of their type (e.g., `IEmailService service = new SendGridEmailService();`).

**Q: What is the difference between Method Overloading and Method Overriding?**

**A:** Overloading happens at **compile-time** within the same class (changing parameters). Overriding happens at **runtime** across parent-child inheritance boundaries (using `virtual` and `override` to swap execution logic).

**Pro-Tip:** 🚀 When discussing OOP, always mention that you favor **Composition over Inheritance** where appropriate. Tell the interviewer: _"Inheritance creates a rigid IS-A relationship, whereas Composition creates a flexible HAS-A relationship by injecting components via interfaces, making the code vastly easier to unit test."_


**To restrict object instantiation to a maximum of 3 times and throw an exception on the 4th attempt, you must use a static counter inside the class constructor combined with a thread-safe locking mechanism.**

Here is how you implement this cleanly and safely in C#.

C#

```cs
using System;

public class RestrictedClass
{
    // Static fields are shared across ALL instances of the class
    private static int _instanceCount = 0;
    
    // Lock object to guarantee thread-safety in multi-threaded environments
    private static readonly object _lock = new object();

    public RestrictedClass()
    {
        // Thread-safe block prevents race conditions
        lock (_lock)
        {
            _instanceCount++;

            if (_instanceCount > 3)
            {
                throw new InvalidOperationException("Instance limit exceeded. Maximum allowed instances of this class is 3.");
            }
        }

        Console.WriteLine($"Instance #{_instanceCount} successfully created.");
    }
}
```

### How to test execution:

C#

```cs
public class Program
{
    public static void Main()
    {
        try
        {
            var obj1 = new RestrictedClass(); // Works (Count = 1)
            var obj2 = new RestrictedClass(); // Works (Count = 2)
            var obj3 = new RestrictedClass(); // Works (Count = 3)
            
            Console.WriteLine("Attempting to create 4th object...");
            var obj4 = new RestrictedClass(); // CRASHES HERE
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine($"Caught Expected Error: {ex.Message}");
        }
    }
}
```