## BLUF

MSTest is the native, attribute-driven testing framework for .NET applications used to validate code behavior and enforce structural integrity. It isolates logic into test classes and methods, utilizing assertions to verify expected outcomes.

## 🧠 Core Analogy

Think of MSTest as an automotive quality assurance facility.

- **`[TestClass]`** is the specific testing hangar (e.g., Engine Testing).
    
- **`[TestMethod]`** is an individual test protocol (e.g., `StartEngine_WithFuel_Runs`).
    
- **`Assert`** is the inspector's clipboard verifying the results (e.g., RPM > 1000).
    
- **`[TestInitialize]`** is the crew resetting the car before _every_ test protocol to avoid contamination.
    

## 🏗️ Core Attributes & Mechanics

|**Attribute**|**Execution Scope**|**Purpose**|
|---|---|---|
|`[TestClass]`|Class Level|Marks a class that contains executable test methods.|
|`[TestMethod]`|Method Level|Defines a parameterless method as a test case.|
|`[DataTestMethod]`|Method Level|Defines a test method that accepts parameterized inputs.|
|`[DataRow]`|Method Level|Provides inline data arguments for a `[DataTestMethod]`.|
|`[TestInitialize]`|Pre-Test|Runs before _each_ `[TestMethod]` to instantiate a clean state.|
|`[ClassInitialize]`|Pre-Class|Runs _once_ before any tests in the class (requires a `TestContext` parameter).|

## 💻 Implementation Example

Below is a standard implementation testing a domain service, utilizing the Arrange-Act-Assert (AAA) pattern.

C#

```cs
using Microsoft.VisualStudio.TestTools.UnitTesting;

[TestClass]
public class InvoiceServiceTests
{
    private InvoiceService _service;

    [TestInitialize]
    public void Setup()
    {
        // Instantiated fresh before every test to prevent state bleeding
        _service = new InvoiceService();
    }

    [TestMethod]
    public void ApplyTax_StandardRate_IncreasesTotal()
    {
        // Arrange
        decimal baseAmount = 100m;

        // Act
        decimal result = _service.ApplyTax(baseAmount);

        // Assert
        Assert.AreEqual(110m, result);
    }

    [DataTestMethod]
    [DataRow(100, "EXEMPT", 100)]
    [DataRow(100, "STANDARD", 110)]
    public void ApplyTax_VariousTaxCodes_ReturnsExpectedTotal(double amount, string code, double expected)
    {
        // Act
        decimal result = _service.ApplyTax((decimal)amount, code);

        // Assert
        Assert.AreEqual((decimal)expected, result);
    }
}
```

## 🎙️ Interview Questions & Answers

**Q: What is the difference between `[TestInitialize]` and `[ClassInitialize]` in MSTest?**

**A:** `[TestInitialize]` executes before _every single_ `[TestMethod]` in the class, ensuring strict state isolation between tests. `[ClassInitialize]` executes exactly _once_ per class instantiation, making it ideal for heavy, read-only operations like database schema seeding.

**Q: How do you assert that a specific exception is thrown during execution?**

**A:** You use `Assert.ThrowsException<T>()`. This method wraps the executing code and allows you to validate both the exception type and specific properties of the thrown exception, replacing the older `[ExpectedException]` attribute.

C#

```
var ex = Assert.ThrowsException<ArgumentNullException>(() => _service.Process(null));
Assert.AreEqual("Value cannot be null. (Parameter 'userId')", ex.Message);
```

**Q: Explain the technical difference between `Assert.AreEqual` and `Assert.AreSame`.**

**A:** `Assert.AreEqual` evaluates value equality, typically invoking the object's overridden `.Equals()` method. `Assert.AreSame` evaluates reference equality, verifying that two variables point to the exact same memory address on the heap.

**Pro-Tip:** ⚠️ Never use shared state (like static variables or `[ClassInitialize]`) for mutable test data in MSTest. Tests run in parallel by default in modern .NET, and modifying shared state will cause intermittent, impossible-to-debug race conditions in your CI/CD pipelines.

Would you like to review how to integrate Moq with MSTest to stub database dependencies for your web APIs?