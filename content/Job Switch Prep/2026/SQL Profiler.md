## 🔍 SQL Profiler

`SQL Profiler` is a graphical tracing tool built into SQL Server Management Studio (`SSMS`) that monitors database engine events in real-time. When an ORM like `Entity Framework Core` generates complex, inefficient queries behind the scenes, you use this tool to intercept and read the actual `T-SQL` hitting the database.

**Key Metrics to Monitor (Mention these in the interview):**

- **TextData:** The raw `T-SQL` query string that was executed.
    
- **Duration:** How many milliseconds the query took to execute (sort your trace by this to immediately find the bottleneck).
    
- **Reads:** The number of logical disk reads performed; unusually high reads indicate a missing database index.
    

**Your Interview Script:** "If a specific API endpoint is lagging, I start a trace in `SQL Profiler` and trigger the endpoint to capture the underlying queries. I filter the trace to isolate queries with a high `Duration` or massive logical `Reads`, extract the raw `T-SQL`, and analyze its Execution Plan to see if we need to add an index or optimize the `Entity Framework` LINQ statement."

**Pro-Tip:** 💡 Microsoft has officially deprecated `SQL Profiler` in favor of **Extended Events (XEvents)**. Mentioning in the interview that you understand `Profiler` but prefer setting up an `Extended Events` session because it requires significantly less server overhead will instantly elevate your perceived seniority.