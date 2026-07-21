Here is a classic example using coffee.

First, we define an interface for the base component:

C#

```cs
public interface ICoffee
{
    string GetDescription();
    double GetCost();
}
```

Next, a concrete implementation:

C#

```cs
public class SimpleCoffee : ICoffee
{
    public string GetDescription() => "Simple Coffee";
    public double GetCost() => 2.0;
}
```

Then, we create an abstract decorator that also implements the interface:

C#

```cs
public abstract class CoffeeDecorator : ICoffee
{
    protected readonly ICoffee _decoratedCoffee;

    public CoffeeDecorator(ICoffee coffee)
    {
        _decoratedCoffee = coffee;
    }

    public virtual string GetDescription() => _decoratedCoffee.GetDescription();
    public virtual double GetCost() => _decoratedCoffee.GetCost();
}
```

Finally, we can create concrete decorators to add specific features:

C#

```cs
public class MilkDecorator : CoffeeDecorator
{
    public MilkDecorator(ICoffee coffee) : base(coffee) { }

    public override string GetDescription() => _decoratedCoffee.GetDescription() + ", Milk";
    public override double GetCost() => _decoratedCoffee.GetCost() + 0.5;
}

public class SugarDecorator : CoffeeDecorator
{
    public SugarDecorator(ICoffee coffee) : base(coffee) { }

    public override string GetDescription() => _decoratedCoffee.GetDescription() + ", Sugar";
    public override double GetCost() => _decoratedCoffee.GetCost() + 0.25;
}
```

Now, you can wrap objects dynamically:

C#

```cs
ICoffee myCoffee = new SimpleCoffee();
myCoffee = new MilkDecorator(myCoffee);
myCoffee = new SugarDecorator(myCoffee);

Console.WriteLine(myCoffee.GetDescription() + " costs $" + myCoffee.GetCost());
```

This will output: "Simple Coffee, Milk, Sugar costs $2.75." 



---
Let's look at a practical notification system.

First, we have an interface for sending messages:

C#

```
public interface INotification
{
    void Send(string message);
}
```

Next, a basic email notification class that implements the interface:

C#

```
public class EmailNotification : INotification
{
    public void Send(string message)
    {
        Console.WriteLine($"Sending email: {message}");
    }
}
```

Now, we create an abstract decorator class that also implements `INotification` and holds a reference to another notification:

C#

```
public abstract class NotificationDecorator : INotification
{
    protected readonly INotification _notification;

    public NotificationDecorator(INotification notification)
    {
        _notification = notification;
    }

    public virtual void Send(string message)
    {
        _notification.Send(message);
    }
}
```

Finally, we can add specific decorators to add features like SMS or Slack messaging:

C#

```
public class SmsDecorator : NotificationDecorator
{
    public SmsDecorator(INotification notification) : base(notification) { }

    public override void Send(string message)
    {
        base.Send(message);
        Console.WriteLine($"Sending SMS: {message}");
    }
}

public class SlackDecorator : NotificationDecorator
{
    public SlackDecorator(INotification notification) : base(notification) { }

    public override void Send(string message)
    {
        base.Send(message);
        Console.WriteLine($"Sending Slack message: {message}");
    }
}
```

By putting these together, you can create a notification that sends an email and a text message dynamically at runtime:

C#

```
INotification notify = new EmailNotification();
notify = new SmsDecorator(notify);
notify = new SlackDecorator(notify);

notify.Send("System alert!");
```

This will send the alert via email, then SMS, and finally