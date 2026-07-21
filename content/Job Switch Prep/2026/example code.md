Alright, let's look at the code for that payment system example.

C#

```cs
// The Target Interface that the modern application expects
public interface ICreditCardPayment
{
    void Pay(decimal amount);
}

// The Adaptee, which is the legacy system with a different interface
public class LegacyPaymentSystem
{
    public void MakePayment(double totalAmount)
    {
        Console.WriteLine($"Processing legacy payment of ${totalAmount}");
    }
}

// The Adapter that bridges the gap
public class PaymentAdapter : ICreditCardPayment
{
    private readonly LegacyPaymentSystem _legacySystem;

    public PaymentAdapter(LegacyPaymentSystem legacySystem)
    {
        _legacySystem = legacySystem;
    }

    public void Pay(decimal amount)
    {
        // Translating the method call to match the legacy system
        double amountInDouble = (double)amount;
        _legacySystem.MakePayment(amountInDouble);
    }
}
```

Now, the client code can use the adapter without needing to know the details of the legacy system.

C#

```
LegacyPaymentSystem legacySystem = new LegacyPaymentSystem();
ICreditCardPayment paymentProcessor = new PaymentAdapter(legacySystem);

paymentProcessor.Pay(100.50m);
```

This ensures the modern system interacts smoothly with the older one. Does this code example help make the Adapter pattern's function clearer?


---

Here is the code for the logging adapter example.

C#

```
// The Target Interface that the modern application expects
public interface IAppLogger
{
    void LogInfo(string message);
    void LogError(string message);
}

// The Adaptee, which is the third-party logging library with a different interface
public class ThirdPartyLogger
{
    public void WriteLog(string type, string logData)
    {
        Console.WriteLine($"[{type.ToUpper()}] Third-party log: {logData}");
    }
}

// The Adapter that bridges the gap
public class LoggerAdapter : IAppLogger
{
    private readonly ThirdPartyLogger _thirdPartyLogger;

    public LoggerAdapter(ThirdPartyLogger thirdPartyLogger)
    {
        _thirdPartyLogger = thirdPartyLogger;
    }

    public void LogInfo(string message)
    {
        // Translating the method call to match the third-party library
        _thirdPartyLogger.WriteLog("info", message);
    }

    public void LogError(string message)
    {
        // Translating the method call to match the third-party library
        _thirdPartyLogger.WriteLog("error", message);
    }
}
```

Now, your application can use the adapter seamlessly without relying directly on the third-party library's specific methods.

C#

```
ThirdPartyLogger thirdPartyLogger = new ThirdPartyLogger();
IAppLogger appLogger = new LoggerAdapter(thirdPartyLogger);

appLogger.LogInfo("Application started successfully.");
appLogger.LogError("An unexpected error occurred in the system.");
```

This ensures your application code remains clean and decoupled from the specific implementation details of the logging framework. Does this example help demonstrate how the Adapter pattern works with different interfaces?