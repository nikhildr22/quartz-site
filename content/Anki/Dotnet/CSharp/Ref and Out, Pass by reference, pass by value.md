STARTanki
Basic

Front: What is pass by value in C#?

Back:
A copy of the variable's value is passed to the method.
Changes made inside the method do not affect the original variable.

```csharp
void Increment(int x)
{
    x++;
}

int n = 5;
Increment(n);

Console.WriteLine(n); // 5
```
<!--ID: 1783329399082-->
ENDanki

STARTanki
Basic

Front: What is pass by reference in C#?

Back:
The method receives a reference to the caller's variable instead of a copy.
Changes made inside the method affect the original variable.

```csharp
void Increment(ref int x)
{
    x++;
}

int n = 5;
Increment(ref n);

Console.WriteLine(n); // 6
```
<!--ID: 1783329399084-->
ENDanki

STARTanki
Basic

Front: What is the ref keyword in C#?

Back:
`ref` passes an argument by reference.
The variable must already be initialized.
The method can read and modify the existing value.

```csharp
void Double(ref int x)
{
    x *= 2;
}

int n = 10;
Double(ref n);

Console.WriteLine(n); // 20
```
<!--ID: 1783329399085-->
ENDanki

STARTanki
Basic

Front: What is the out keyword in C#?

Back:
`out` passes an argument by reference for output.
The variable does not need to be initialized.
The method must assign it before returning.

```csharp
void GetNumber(out int number)
{
    number = 100;
}

int n;
GetNumber(out n);

Console.WriteLine(n); // 100
```
<!--ID: 1783329399087-->
ENDanki

STARTanki
Basic

Front: Why do we use ref in C#?

Back:
Use `ref` when a method needs to modify the caller's existing variable.

Example: Swapping two variables.

```csharp
void Swap(ref int a, ref int b)
{
    int temp = a;
    a = b;
    b = temp;
}

int x = 10;
int y = 20;

Swap(ref x, ref y);

// x = 20, y = 10
```
<!--ID: 1783329399089-->
ENDanki

STARTanki
Basic

Front: Why do we use out in C#?

Back:
Use `out` when a method needs to return additional values.

Example:

```csharp
void Divide(int a, int b,
            out int quotient,
            out int remainder)
{
    quotient = a / b;
    remainder = a % b;
}

Divide(10, 3, out int q, out int r);

// q = 3
// r = 1
```
<!--ID: 1783329399090-->
ENDanki

STARTanki
Basic

Front: What is the difference between ref and out?

Back:

| ref                     | out                           |
| ----------------------- | ----------------------------- |
| Must be initialized     | Need not be initialized       |
| Can read existing value | Cannot read before assignment |
| Assignment optional     | Assignment mandatory          |


Example:

```csharp
int a = 5;
Increment(ref a);

int b;
GetNumber(out b);
```
<!--ID: 1783329399092-->
ENDanki

STARTanki
Basic

Front: Must a variable be initialized before passing it with ref?

Back:
Yes.

✔ Valid

```csharp
int n = 5;
Increment(ref n);
```

❌ Invalid

```csharp
int n;
Increment(ref n); // Compile error
```
<!--ID: 1783329399093-->
ENDanki

STARTanki
Basic

Front: Must a variable be initialized before passing it with out?

Back:
No.

```csharp
int n;

GetNumber(out n);

Console.WriteLine(n);
```
<!--ID: 1783329399095-->
ENDanki

STARTanki
Basic

Front: Can a method read an out parameter before assigning it?

Back:
No.

❌ Invalid

```csharp
void Test(out int x)
{
    Console.WriteLine(x); // Compile error
    x = 10;
}
```

✔ Correct

```csharp
void Test(out int x)
{
    x = 10;
    Console.WriteLine(x);
}
```
<!--ID: 1783329399096-->
ENDanki

STARTanki
Basic

Front: Must an out parameter always be assigned?

Back:
Yes.

❌ Invalid

```csharp
void Test(out int x)
{
}
```

✔ Correct

```csharp
void Test(out int x)
{
    x = 100;
}
```
<!--ID: 1783329399098-->
ENDanki

STARTanki
Basic

Front: What happens if you modify a value type without ref or out?

Back:
Only the local copy changes.

```csharp
void AddFive(int x)
{
    x += 5;
}

int n = 10;

AddFive(n);

Console.WriteLine(n); // 10
```
<!--ID: 1783329399100-->
ENDanki

STARTanki
Basic

Front: Give a real-world example of out.

Back:
`TryParse` returns:
- bool (success/failure)
- parsed value using `out`

```csharp
string input = "123";

if (int.TryParse(input, out int number))
{
    Console.WriteLine(number); // 123
}
```
<!--ID: 1783329399101-->
ENDanki

STARTanki
Basic

Front: Why does TryParse use out?

Back:
A method can normally return only one value.

`TryParse` returns:
- bool → success/failure
- out int → parsed value

```csharp
bool success =
    int.TryParse("123", out int number);
```
<!--ID: 1783329399103-->
ENDanki

STARTanki
Basic

Front: Can ref parameters be read inside the method?

Back:
Yes.

```csharp
void AddTen(ref int x)
{
    Console.WriteLine(x); // Read
    x += 10;              // Modify
}

int n = 5;

AddTen(ref n);

// n = 15
```
<!--ID: 1783329399105-->
ENDanki

STARTanki
Basic

Front: Can ref and out be used with reference types?

Back:
Yes.

Without `ref`, only the object can be modified.

With `ref`, the object reference itself can be replaced.

```csharp
class Person
{
    public string Name = "";
}

void Replace(ref Person p)
{
    p = new Person
    {
        Name = "Alice"
    };
}

Person person = new Person
{
    Name = "Bob"
};

Replace(ref person);

// person.Name == "Alice"
```
<!--ID: 1783329399106-->
ENDanki

STARTanki
Basic

Front: What happens if you forget to assign an out parameter?

Back:
Compilation fails.

❌

```csharp
void Test(out int x)
{
    if (DateTime.Now.Day == 1)
        x = 10;
}
```

✔

```csharp
void Test(out int x)
{
    if (DateTime.Now.Day == 1)
        x = 10;
    else
        x = 20;
}
```
<!--ID: 1783329399108-->
ENDanki

STARTanki
Basic

Front: Interview definition of ref and out.

Back:
Both `ref` and `out` pass arguments by reference.

- `ref` → caller provides an existing value; method can read and modify it.
- `out` → method is responsible for producing the value; caller need not initialize it.

Typical uses:
- `ref` → Swap(), Update(), Replace()
- `out` → TryParse(), Divide(), GetValues()
<!--ID: 1783329399109-->
ENDanki