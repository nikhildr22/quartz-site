## BLUF

A **Database Trigger** is a specialized, stored procedure that automatically executes ("fires") in response to a specific Data Manipulation Language (DML) event—`INSERT`, `UPDATE`, or `DELETE`—on a designated table. In enterprise full-stack development, triggers are a powerful but double-edged sword used primarily to enforce strict data integrity or maintain low-level audit trails.

## 🧠 The "Security Camera & Automated Tripwire" Analogy

Think of a database table as a secure bank vault room.

- **The Operation:** Customers walk in and deposit money (`INSERT`), move cash around (`UPDATE`), or withdraw funds (`DELETE`).
    
- **The Trigger:** A security sensor is hardwired directly to the vault door.
    
- **The Execution:** The moment someone tries to perform an action, the sensor trips and instantly runs an automated script.
    
    - If it is an **AFTER Trigger**, it waits until the cash is moved, then automatically logs the transaction name, timestamps it, and writes it to an un-editable audit ledger book in the corner.
        
    - If it is an **INSTEAD OF Trigger**, it blocks the user at the door, intercepts the cash, runs a custom compliance check, and decides whether to deposit it manually or throw an immediate alarm (Exception).

## 🏛️ Trigger Architecture & The Logical Tables

When a trigger fires in SQL Server, the system instantiates two virtual, memory-resident tables called **`INSERTED`** and **`DELETED`**. You use these tables to see exactly what data is changing.

|**DML Operation**|**INSERTED Table State**|**DELETED Table State**|
|---|---|---|
|**`INSERT`**|Contains the brand-new rows being added.|Completely Empty (`null`/zero rows).|
|**`DELETE`**|Completely Empty (`null`/zero rows).|Contains the original rows that are being wiped out.|
|**`UPDATE`**|Contains the new, modified version of the rows.|Contains the old, pre-updated version of the rows.|

## 💻 Technical Implementation: SSMS (T-SQL)

Imagine an enterprise `Employee` table. Business requirements state that whenever an employee's salary is modified, the system must log the historical tracking data into an audit table automatically.

### Step 1: The Audit Ledger Table

SQL

```sql
CREATE TABLE EmployeeSalaryAudit (
    AuditId INT IDENTITY(1,1) PRIMARY KEY,
    EmployeeId INT,
    OldSalary DECIMAL(18,2),
    NewSalary DECIMAL(18,2),
    ChangedAt DATETIME DEFAULT GETDATE(),
    ChangedBy NVARCHAR(100) DEFAULT SUSER_NAME()
);
```

### Step 2: The `AFTER UPDATE` Trigger Implementation

This trigger intercepts the data change, evaluates if the salary column was touched, and processes a set-based migration to the audit log.

SQL

```sql
CREATE TRIGGER TR_Employees_AfterUpdateSalary
ON Employees
AFTER UPDATE
AS
BEGIN
    -- Performance Optimization: Exit early if the Salary column wasn't altered
    IF UPDATE(Salary)
    BEGIN
        SET NOCOUNT ON; -- Prevents extra row-count messages from polluting API channels

        -- CRITICAL: Triggers are set-based! This handles bulk updates perfectly.
        INSERT INTO EmployeeSalaryAudit (EmployeeId, OldSalary, NewSalary)
        SELECT 
            i.EmployeeId,
            d.Salary, -- The old value from DELETED
            i.Salary  -- The new value from INSERTED
        FROM INSERTED i
        JOIN DELETED d ON i.EmployeeId = d.EmployeeId
        WHERE i.Salary <> d.Salary; -- Only log if the value actually changed
    END
END;
```

## ⚙️ Trigger Integration with EF Core

Entity Framework Core **does not** natively generate T-SQL Triggers via basic LINQ statements. Triggers are strictly database-side logic. However, if you add a trigger in SSMS, **EF Core must be informed** so it doesn't break during state synchronization.

When a trigger modifies data on an `INSERT` or `UPDATE`, it messes with EF Core’s state tracking. You must explicitly register the trigger in your Fluent API configuration so EF Core appends an `OUTPUT` clause to its internal SQL calls.

C#

```cs
public class EmployeeConfiguration : IEntityTypeConfiguration<Employee>
{
    public void Configure(EntityTypeBuilder<Employee> builder)
    {
        // Warn EF Core that a trigger exists on this table
        // This ensures EF Core safely reads mutated states back from SQL Server
        builder.ToTable(t => t.HasTrigger("TR_Employees_AfterUpdateSalary"));
    }
}
```

## 🎙️ Tricky Interview Questions to Master

**Q: Does a trigger fire once per modified row, or once per execution statement?**

**A:** This is a classic trap. Triggers in SQL Server fire **once per statement**. If your API executes a bulk update statement that modifies 10,000 rows at the exact same millisecond, the trigger executes exactly **once**. The virtual `INSERTED` and `DELETED` tables will contain all 10,000 rows simultaneously. If you write your trigger code assuming it only processes one row at a time (e.g., using cursors or scalar variables), your trigger will break or cause massive performance degradation.

**Q: What happens to the main `UPDATE` or `INSERT` statement if a trigger throws a runtime exception?**

**A:** Triggers run inside the **same transaction** as the statement that fired them. If a trigger encounters a runtime error or explicitly invokes a `RAISERROR` / `THROW` command, the entire transaction is instantly rolled back. The original data insertion or modification fails completely, and the database reverts to its pre-statement state.

**Q: Why do Senior Architects heavily discourage using triggers for core business logic?**

**A:** Triggers introduce **hidden side effects**. Because they execute implicitly inside the database engine, developers looking at the C# application code cannot see them running. This makes debugging, logging, and unit testing highly complex. Furthermore, long-running processes inside a trigger hold exclusive database locks longer, which often leads to severe system deadlocks under high multi-threaded enterprise traffic.

**Pro-Tip:** 🚀 If an interviewer asks you how to handle audit logging in a modern full-stack application, tell them: _"While database triggers work for low-level DBA auditing, I prefer implementing audit trails inside the application tier by overriding `SaveChangesAsync()` in EF Core, or using dedicated change tracking frameworks. This keeps our business architecture visible, maintainable, and significantly cuts down on structural database locking overhead."_