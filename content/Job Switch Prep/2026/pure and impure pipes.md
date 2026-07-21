## BLUF

An **Angular Pipe** is a declarative template class that accepts an input value, processes it through a transform function, and returns a formatted string or object directly within the HTML view. Pipes are used exclusively for UI data transformation, keeping formatting logic decoupled from your core TypeScript business code.

## 🧱 Standard Built-In Examples

Angular provides several pre-built pipes. They are applied inside interpolation brackets using the pipe symbol (`|`).

HTML

```html
<p>Today is: {{ todayDate | date:'longDate' }}</p> 
<p>Total Cost: {{ price | currency:'INR':'symbol' }}</p>
<pre>{{ userProfileObject | json }}</pre>
```

## ⚖️ Pure vs. Impure Pipes

The fundamental difference lies in **how frequently Angular executes the transform method** during change detection cycles.

### 1. Pure Pipes (Default Behavior)

Angular optimizes performance by executing a pure pipe **only when it detects a change to the reference or primitive value** of the input argument.

- **Primitives (`string`, `number`, `boolean`):** Executes if the value itself changes.
    
- **Objects/Arrays:** Executes **only if the reference changes** (e.g., a brand new array is allocated). If you simply push an item into an existing array (`arr.push(newItem)`), a pure pipe will **not** re-run because the array reference on the heap remains identical.
    

TypeScript

```ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'square',
  standalone: true,
  pure: true // Default behavior
})
export class SquarePipe implements PipeTransform {
  transform(value: number): number {
    console.log('Pure Pipe executed!');
    return value * value;
  }
}
```

### 2. Impure Pipes

An impure pipe executes **on every single change detection cycle**, regardless of whether the input data has changed. This includes mouse clicks, keystrokes, HTTP responses, or timer ticks anywhere on the page.

- **Use Case:** When you need a pipe to filter an array in place, reacting immediately when elements inside that array mutate.
    
- **The Penalty:** High performance overhead. If your transform function contains heavy loops, an impure pipe can easily degrade UI rendering performance.
    

TypeScript

```ts
@Pipe({
  name: 'filterArray',
  standalone: true,
  pure: false // Tells Angular to execute this on every single change cycle
})
export class FilterArrayPipe implements PipeTransform {
  transform(items: any[], filterText: string): any[] {
    console.log('Impure Pipe executed!');
    if (!items || !filterText) return items;
    return items.filter(item => item.name.includes(filterText));
  }
}
```

## 🎙️ Tricky Interview Questions to Master

**Q: Why does Angular explicitly recommend against creating a custom pipe to filter or sort data arrays?**

**A:** If you make the filtering pipe **pure**, it won't update when you append elements to the list (since array mutations don't alter the reference pointer), making the UI buggy. If you fix this by making the pipe **impure**, it will recalculate the entire filtering/sorting algorithm on every single change detection cycle across the app, degrading application performance. The correct architectural pattern is to move sorting/filtering logic into the TypeScript component or a state-managed pipeline.

**Q: What is the built-in `async` pipe, and why is it considered critical for memory management?**

**A:** The `async` pipe automatically subscribes to an RxJS `Observable` or JavaScript `Promise` directly within the HTML template and returns the latest emitted value. More importantly, **it automatically unsubscribes** from that stream when the component is destroyed. This completely eliminates the risk of memory leaks without requiring manual `.unsubscribe()` calls or `takeUntil()` operators inside the TypeScript class.

HTML

```
<ul>
  @for (user of users$ | async; track user.id) {
    <li>{{ user.name }}</li>
  }
</ul>
```

**Pro-Tip:** 🚀 When building reusable formatting elements, default to **Pure Pipes** to maximize performance through caching mechanisms. If you find yourself changing `pure: false`, pause and evaluate whether that logic belongs inside your component class or an RxJS stream instead.