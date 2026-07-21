## BLUF

In modern Angular (v15+), **Functional Auth Guards** have completely replaced legacy class-based guards. You create a custom guard by writing a pure JavaScript function that satisfies the `CanActivateFn` signature, injecting dependencies directly via the `inject()` token instead of using constructor dependency injection.

## 💻 The Functional Auth Guard Blueprint

This production-grade pattern intercepts routes, checks if a token exists in local storage, and redirects unauthorized users using the router engine.

TypeScript

```ts
// auth.guard.ts
import { inject } from '@angular/core';
import { CanActivateFn, Router } from '@angular/router';

export const authGuard: CanActivateFn = (route, state) => {
  const router = inject(Router);

  // Replace this placeholder with your actual auth state evaluation logic 
  // (e.g., calling an injected AuthService token validation method)
  const isAuthenticated = !!localStorage.getItem('authToken');

  if (isAuthenticated) {
    return true; // Allows execution path to proceed to the route
  }

  // Redirect unauthorized users back to the login page
  // parseUrl returns a UrlTree which Angular safely navigates to
  return router.parseUrl('/login');
};
```

## 🚦 Route Registration Architecture

To activate the guard, you attach it directly to your application's route configuration layout inside the `canActivate` array.

TypeScript

```ts
// app.routes.ts
import { Routes } from '@angular/router';
import { DashboardComponent } from './dashboard/dashboard.component';
import { LoginComponent } from './login/login.component';
import { authGuard } from './auth.guard';

export const routes: Routes = [
  { 
    path: 'login', 
    component: LoginComponent 
  },
  { 
    path: 'dashboard', 
    component: DashboardComponent,
    canActivate: [authGuard] // Active guard interceptor protects this route and its children
  }
];
```

## 🎙️ Tricky Interview Questions to Master

**Q: Why did the Angular team deprecate Class-based guards (implementing `CanActivate`) in favor of Functional Guards?**

**A:** Functional guards dramatically reduce boilerplate code and maximize optimization opportunities. Class-based guards require spinning up heavy class declarations, manual constructor configurations, and explicit module registrations. Functional guards are tree-shakable, pure functions, which significantly cuts down the final application bundle size.

**Q: How do you pass dynamic parameter data (like specific roles) to a Functional Auth Guard?**

**A:** Since functional guards are just functions, you use a **Higher-Order Function** (a factory function that returns a `CanActivateFn`). You pass configuration metadata parameters to the outer factory function, which the inner guard function reads via standard JavaScript closure mechanics.

TypeScript

```ts
// role.guard.ts
import { inject } from '@angular/core';
import { CanActivateFn, Router } from '@angular/router';

export const roleGuard = (allowedRoles: string[]): CanActivateFn => {
  return (route, state) => {
    const router = inject(Router);
    const userRole = localStorage.getItem('userRole'); // Example storage lookup

    if (userRole && allowedRoles.includes(userRole)) {
      return true;
    }

    return router.parseUrl('/unauthorized');
  };
};

// Registered in app.routes.ts like this:
// canActivate: [roleGuard(['Admin', 'Manager'])]
```

**Pro-Tip:** 🚀 Functional guards do not require you to return a primitive boolean value synchronously. If your application validates JWT status against an API server backend, you can return an `Observable<boolean | UrlTree>` stream. The Angular routing engine will pause navigation automatically and wait for the asynchronous HTTP stream to resolve before rendering the view layout.