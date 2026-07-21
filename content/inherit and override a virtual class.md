```cs
using System;
					
public class Program
{
	public static void Main()
	{
		A obj1 = new B();
		obj1.SomeMethod();
	}
	
	
}

public class A{
	public void SomeMethod()
	{
		Console.WriteLine("Implementted Using BaseClass Logic");
	}
}

public class B : A {
	public void SomeMethod()
	{
		Console.WriteLine("Implementted Using Subclass Logic");
	}
}
```