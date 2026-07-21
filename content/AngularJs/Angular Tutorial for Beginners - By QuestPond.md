this covers the fundamentals
![[Pasted image 20231104093106.png]]
![[Pasted image 20231104093117.png]]

Angular.io
official site
angular was created by google
its a development platform built on typescript

features:
![[Pasted image 20231104093344.png]]
# pre requisites
![[Pasted image 20231104093456.png]]

- installation
- Node and npm installation
- typescript basics
- angular basics

# installation

run VS code as admin for angular and react projects to avoid some common issues

install nodejs

`node -v` to check node version
`npm -v` to check npm version

node and npm versions will be different.

Inside vs code,
prefer to use cmd as terminal, not powershell
![[Pasted image 20231104094814.png]]

## install angular CLI

`npm install -g @angular/cli`

`ng version` --> to check if cli is installed
`Warning: The current version of Node (20.9.0) is not supported by Angular.`-> as i got this version error, i've installed lower version of node.
v18.18.2
`ng new my-app`
```
cd my-app
ng serve --open
```
`ng serve` -> to start the angular app
The `--open` (or just `-o`) option automatically opens your browser to `http://localhost:4200/`.

## summary of installation
![[Pasted image 20231104112200.png]]

chrome v8 engine, js is compiled to machine code using v8 engine

nodeJs is a build upon v8 engine
![[Pasted image 20231104112335.png]]

Node helps us We can run Javascript outside the browser.
thus we can use chrome to debug node.
## js running out of browser:
![[Pasted image 20231104113134.png]]

## npm to install other packages
```
npm install --prefix ./ jquery

```

package.json -> contain the packages installed


# Typescript
https://www.typescriptlang.org/

TypeScript is a strongly typed programming language that builds on JavaScript, giving you better tooling at any scale.

![[Pasted image 20231104125510.png]]

js is loosely typed language, but Ts is strongly typed language.

![[Pasted image 20231104125613.png]]

![[Pasted image 20231104125624.png]]

```
npm install typescript -g
```
install typescript on a global scope using npm

```
tsc -v
Version 5.2.2
```

first we need to compile the Ts file using tsc command
`tsc testprog.ts`

then run the final js file using node
`node testprog.js`

## Why typescript?
it increases productivity
OOPs programmer will be inefficient with pure js.

![[Pasted image 20231104130223.png]]
```ts
class Customer {
    name:string="";
    code:string="";
}

class CustomerChild extends Customer{
    
}
```

after compiling:
```js
var __extends = (this && this.__extends) || (function () {
    var extendStatics = function (d, b) {
        extendStatics = Object.setPrototypeOf ||
            ({ __proto__: [] } instanceof Array && function (d, b) { d.__proto__ = b; }) ||
            function (d, b) { for (var p in b) if (Object.prototype.hasOwnProperty.call(b, p)) d[p] = b[p]; };
        return extendStatics(d, b);
    };
    return function (d, b) {
        if (typeof b !== "function" && b !== null)
            throw new TypeError("Class extends value " + String(b) + " is not a constructor or null");
        extendStatics(d, b);
        function __() { this.constructor = d; }
        d.prototype = b === null ? Object.create(b) : (__.prototype = b.prototype, new __());
    };
})();
var Customer = /** @class */ (function () {
    function Customer() {
        this.name = "";
        this.code = "";
    }
    return Customer;
}());
var CustomerChild = /** @class */ (function (_super) {
    __extends(CustomerChild, _super);
    function CustomerChild() {
        return _super !== null && _super.apply(this, arguments) || this;
    }
    return CustomerChild;
}(Customer));

```

![[Pasted image 20231104130620.png]]

![[Pasted image 20231104130647.png]]
![[Pasted image 20231104130732.png]]

rather than compile, the right word is transpile

![[Pasted image 20231104130756.png]]

tsconfig.json can be used to control the compilation/transpilation process.

`tsc --init`

`tsc` command will help us find compilation errors.

![[Pasted image 20231104131456.png]]
you can also disable strict type checking -> this will help us assign null to the strongly typed variables.


once we create a new angular project, there are 3 important config files
angular.json --> configure angular
package.json

tsconfig.json

spec files are for unit testing purposes.


![[Pasted image 20231104132447.png]]

AngularJs is 1.x family of angular

Angular is new family

angularjs is out of support, but it's still being used in industry.


# src folder
this is where out dev files go
## app folder
this has our angular code

- A component-based framework for building scalable web applications
- A collection of well-integrated libraries that cover a wide variety of features, including routing, forms management, client-server communication, and more
- A suite of developer tools to help you develop, build, test, and update your code
![[Pasted image 20231104135311.png]]

component = HTML+CSS+Logic
![[Pasted image 20231104135929.png]]


![[Pasted image 20231104135939.png]]

![[Pasted image 20231104135949.png]]


what does a simple Ts class become a Component?
this feature is imported from angular module
![[Pasted image 20231104140131.png]]/

This is a decorator:
![[Pasted image 20231104140148.png]]
![[Pasted image 20231104140430.png]]

component will map view and js with selector.
here, it'll take the html and css and js and enter them inside the app-root tag in index.html file

![[Pasted image 20231104140646.png]]
![[Pasted image 20231104140659.png]]
![[Pasted image 20231104140719.png]]
![[Pasted image 20231104140734.png]]
template is file containing angular+html code.

## module
a grouping of components
![[Pasted image 20231104140957.png]]
has 2 parts:
1. declaration
	1. contain list of all components
2. bootstrap
	1. contain the startup component among the declaration components
3. 

Binding:
we can bind a element's value to a typescript variable in a component
by using both brackets `[()]` in bind, we are saying data Binding is bidirectional.

![[Pasted image 20231104141458.png]]

Expressions:
![[Pasted image 20231104141513.png]]


`"@angular/forms"` this module has Binding logic
![[Pasted image 20231104142924.png]]


`*ngFor` this is a directive to make for loop

you can search for different directives to use in your code
![[Pasted image 20231104144445.png]]![[Pasted image 20231104144550.png]]


Angular is very big
![[Pasted image 20231104184405.png]]