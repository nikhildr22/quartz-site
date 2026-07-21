LINQ is another area where interviewers love asking **small but tricky questions**. They usually aren't testing whether you know the method name—they're testing whether you understand what it does and its edge cases.

---

# 1. First record

```csharp
employees.First();
```

Returns the first item.

⚠️ Throws an exception if the collection is empty.

---

# 2. FirstOrDefault

```csharp
employees.FirstOrDefault();
```

Returns

* First item if present
* `null` (reference types) or the default value (value types) if empty

Interview question:

> **Difference between `First()` and `FirstOrDefault()`?**

Answer:

| First()         | FirstOrDefault() |
| --------------- | ---------------- |
| Throws if empty | Returns default  |

---

# 3. Last record

```csharp
employees.Last();
```

Returns last record.

Throws if empty.

---

# 4. LastOrDefault

```csharp
employees.LastOrDefault();
```

Safe version.

---

# 5. Single()

Very popular.

```csharp
employees.Single(e => e.Id == 10);
```

Means

> "Exactly one record must exist."

Throws if

* none exist
* more than one exists

---

# 6. SingleOrDefault()

```csharp
employees.SingleOrDefault(e => e.Id == 10);
```

Returns

* one record
* default if none

Throws if multiple exist.

---

Interview question

> Why use Single instead of First?

Suppose EmployeeId is unique.

```text
Id

1

2

2
```

`First()`

Returns

```text
2
```

No complaint.

`Single()`

Throws.

It detects bad data.

---

# 7. Take()

Top N records

```csharp
employees.Take(5);
```

SQL equivalent

```sql
TOP 5
```

---

# 8. Skip()

```csharp
employees.Skip(5);
```

Skips first five.

Useful for pagination.

---

# 9. Skip + Take

Classic interview question.

Page size

```text
10
```

Page

```text
3
```

```csharp
employees
    .Skip((page - 1) * pageSize)
    .Take(pageSize);
```

---

# 10. Second Highest Salary

Very common.

```csharp
employees
    .OrderByDescending(e => e.Salary)
    .Skip(1)
    .First();
```

---

But here's the trick.

What if

```text
100
90
90
80
```

Do you want

```text
90
```

or

```text
80
```

If you mean the **second distinct highest** salary:

```csharp
employees
    .Select(e => e.Salary)
    .Distinct()
    .OrderByDescending(s => s)
    .Skip(1)
    .First();
```

Interviewers love this follow-up.

---

# 11. Third Highest

```csharp
.OrderByDescending(x => x.Salary)
.Skip(2)
.First()
```

---

# 12. Top 3

```csharp
.OrderByDescending(x => x.Salary)
.Take(3)
```

---

# 13. Any()

```csharp
employees.Any();
```

Returns

```text
true/false
```

Efficient.

Stops after finding the first item.

---

# 14. Count()

```csharp
employees.Count();
```

Counts every item.

Interview question

Which is better?

```csharp
Count() > 0
```

or

```csharp
Any()
```

Answer

```text
Any()
```

because it stops immediately after finding one item, whereas `Count()` may need to evaluate the entire sequence.

---

# 15. Where()

Returns multiple records.

```csharp
employees.Where(e => e.Salary > 50000);
```

---

# 16. Select()

Projects data.

```csharp
employees.Select(e => e.Name);
```

---

# 17. Select vs SelectMany

Another favourite.

Suppose

```text
Department

Employees
```

Each department has many employees.

Using

```csharp
Select(d => d.Employees)
```

returns

```text
List<List<Employee>>
```

Using

```csharp
SelectMany(d => d.Employees)
```

returns

```text
List<Employee>
```

Flattening.

---

# 18. Distinct()

```csharp
numbers.Distinct();
```

Removes duplicates.

---

# 19. GroupBy()

```csharp
employees.GroupBy(e => e.Department);
```

Interview question

Find number of employees in each department.

```csharp
employees
    .GroupBy(e => e.Department)
    .Select(g => new
    {
        Department = g.Key,
        Count = g.Count()
    });
```

---

# 20. Max()

Highest salary

```csharp
employees.Max(e => e.Salary);
```

---

# 21. Min()

```csharp
employees.Min(e => e.Salary);
```

---

# 22. Average()

```csharp
employees.Average(e => e.Salary);
```

---

# 23. Sum()

```csharp
employees.Sum(e => e.Salary);
```

---

# 24. OrderBy

Ascending

```csharp
.OrderBy(e => e.Name)
```

Descending

```csharp
.OrderByDescending(e => e.Name)
```

---

# 25. ThenBy

Multiple sorting

```csharp
employees
.OrderBy(e => e.Department)
.ThenByDescending(e => e.Salary);
```

---

# 26. Find Duplicate Names

```csharp
employees
.GroupBy(e => e.Name)
.Where(g => g.Count() > 1)
.Select(g => g.Key);
```

---

# 27. Youngest Employee

```csharp
employees
.OrderBy(e => e.Age)
.First();
```

or

```csharp
employees.MinBy(e => e.Age);
```

(.NET 6+)

---

# 28. Highest Salary Employee

```csharp
employees.MaxBy(e => e.Salary);
```

Older versions

```csharp
employees
.OrderByDescending(e => e.Salary)
.First();
```

---

# 29. Deferred Execution (Very Common)

```csharp
var query = employees.Where(e => e.Age > 30);
```

Does it execute?

No.

Execution happens only when enumerated.

```csharp
query.ToList();
```

or

```csharp
foreach(var e in query)
```

---

# 30. Immediate Execution

These execute immediately:

```csharp
ToList()

ToArray()

Count()

Sum()

Average()

Max()

Min()

First()

Single()
```

---

# Most Asked LINQ Interview Questions

| Question                | Answer                           |
| ----------------------- | -------------------------------- |
| First vs FirstOrDefault | Exception vs default             |
| Single vs First         | Single ensures exactly one match |
| Any vs Count            | `Any()` for existence checks     |
| Select vs SelectMany    | Projection vs flattening         |
| Where vs Select         | Filter vs transform              |
| OrderBy vs ThenBy       | Primary vs secondary sorting     |
| Take                    | Top N                            |
| Skip                    | Pagination                       |
| Distinct                | Remove duplicates                |
| GroupBy                 | Aggregation                      |
| Deferred execution      | Query runs only when enumerated  |

## Bonus: Tricky LINQ Questions

These are the kinds of follow-ups interviewers often ask after you've answered the basics:

### Q1. Find the second highest **distinct** salary

```csharp
employees
    .Select(e => e.Salary)
    .Distinct()
    .OrderByDescending(s => s)
    .Skip(1)
    .FirstOrDefault();
```

### Q2. Find duplicate employees by email

```csharp
employees
    .GroupBy(e => e.Email)
    .Where(g => g.Count() > 1)
    .Select(g => g.Key);
```

### Q3. Get one employee from each department (highest salary)

```csharp
employees
    .GroupBy(e => e.Department)
    .Select(g => g.OrderByDescending(e => e.Salary).First());
```

### Q4. Remove duplicate employees by email

```csharp
employees
    .GroupBy(e => e.Email)
    .Select(g => g.First());
```

### Q5. Difference between `IEnumerable<T>` and `IQueryable<T>`

This is one of the most common LINQ interview questions.

* `IEnumerable<T>` executes LINQ in memory after the data has been loaded.
* `IQueryable<T>` builds an expression tree so providers like Entity Framework can translate the query into SQL and execute it in the database.

Knowing this distinction is particularly valuable for ASP.NET Core and Entity Framework interviews.
