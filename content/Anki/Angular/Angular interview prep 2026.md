STARTanki
Basic
What is Angular?

Back: 
Angular is a structured front-end framework developed by Google for building scalable, enterprise-grade web applications.
Managing large applications with plain JavaScript/DOM manipulation is complex and error-prone, so Angular solves this by providing a unified architecture.

![[Pasted image 20260705083245.png]]
<!--ID: 1783230033558-->
ENDanki


STARTanki
Basic
What are components in Angular?

Back: 
A component is a **reusable building block** used to create user interfaces in single-page applications.
Each logical section of a web page (e.g., menu, search box, footer) is encapsulated as a component containing its own TS logic, HTML, and CSS.

![[Pasted image 20260705083410.png]]
<!--ID: 1783230033563-->
ENDanki


STARTanki
Basic
What is a Single Page Application (SPA)?

Back: 
A **Single Page Application (SPA)** is a web application that loads only one HTML page initially.
Instead of reloading the entire page during navigation, it dynamically updates the DOM by rendering different components in-memory for a native-app feel.

![[Pasted image 20260705083552.png]]
<!--ID: 1783230033565-->
ENDanki


STARTanki
Basic
What are the Top 7 Features of Angular?

Back: 
1. **Component-based architecture**
2. **Open source**
3. **Two-way data binding**
4. **Routing**
5. **Directives**
6. **Dependency injection**
7. **Angular CLI**

![[Pasted image 20260705083633.png]]
<!--ID: 1783230033567-->
ENDanki


STARTanki
Basic
What are the software prerequisites for setting up an Angular environment?

Back: 
1. **Node.js**: JavaScript runtime required to run npm and Angular CLI.
2. **Angular CLI**: Command-line interface for scaffolding.
3. **VS Code**: Recommended code editor.
Download and install Node.js first, then install the Angular CLI via npm.
<!--ID: 1783230033569-->
ENDanki


STARTanki
Basic
Which VS Code extensions are required/recommended for Angular development?

Back: 
1. **Prettier - Code formatter**: Enforces consistent code styling.
2. **Angular Language Service**: Provides autocomplete, error checking, and hinting inside HTML templates.
3. **ESLint**: Linter for identifying patterns in TS code.
<!--ID: 1783230033572-->
ENDanki


STARTanki
Basic
What is the role of NPM in Angular?

Back: 
**NPM (Node Package Manager)** manages dependencies and third-party libraries, similar to NuGet packages in `.NET`.
It consists of an online registry and a CLI tool. Installed packages are stored in the `node_modules` folder.
<!--ID: 1783230033574-->
ENDanki


STARTanki
Basic
What is the Angular CLI and how is it installed?

Back: 
The **Angular CLI** is a command-line tool that helps you create, build, and manage Angular projects easily.
Install it globally using: `npm install -g @angular/cli`
Verify the version using: `ng version`

![[Pasted image 20260705093848.png]]
<!--ID: 1783230033576-->
ENDanki


STARTanki
Basic
How do you create your first Angular project using the CLI?

Back: 
Run the following command in your terminal:
`ng new my-first-app`
Initially, `app.component.html` will contain generated template code, which you delete to add custom logic.

![[Pasted image 20260705094009.png]]
![[Pasted image 20260705094258.png]]
<!--ID: 1783230033579-->
ENDanki


STARTanki
Basic
What is Live Reload in Angular?

Back: 
**Live Reload** automatically recompiles the application and refreshes the browser whenever a source file is modified and saved.
This accelerates development by providing instant visual feedback.

![[Pasted image 20260705094343.png]]
<!--ID: 1783230033581-->
ENDanki


STARTanki
Basic
What is the purpose of the `package.json` file in Angular?

Back: 
The `package.json` file acts as the project manifest.
It contains installed package lists, project metadata, and scripts required to run or build the application.

![[Pasted image 20260705094403.png]]
![[Pasted image 20260705094447.png]]
<!--ID: 1783230033583-->
ENDanki


STARTanki
Basic
What does the `node_modules` folder contain?

Back: 
The `node_modules` folder contains the physical files for all external libraries and dependencies listed in `package.json`.
It is automatically populated when running `npm install`.

![[Pasted image 20260705094504.png]]
<!--ID: 1783230033585-->
ENDanki


STARTanki
Basic
Summarize how Node.js, NPM, Angular CLI, package.json & node_modules work together.

Back: 
**Node.js** provides the runtime environment for **NPM**, which reads dependencies from **`package.json`**.
NPM downloads these into **`node_modules`**. Finally, the **Angular CLI** utilizes Node and these packages to build and manage the application.

![[Pasted image 20260705094530.png]]
<!--ID: 1783230033588-->
ENDanki


STARTanki
Basic
What is the basic folder structure inside an Angular app directory?

Back: 
The `src/app` folder holds the root files required to load the application page.
Standard files include `app.component.css`, `app.component.html`, and `app.component.ts`.

![[Pasted image 20260705094701.png]]
<!--ID: 1783230033590-->
ENDanki


STARTanki
Basic
What is the purpose of the `ng serve` command and how do you stop it?

Back: 
The `ng serve` command compiles the application into memory, starts the local development server, and enables live reloading.
Press `Ctrl + C` in the terminal to stop the running application.
<!--ID: 1783230033592-->
ENDanki


STARTanki
Basic
What constitutes a component in Angular?

Back: 
A component encapsulates three core elements for a specific UI section:
1. **TypeScript (`.ts`)**: Business logic and data.
2. **HTML (`.html`)**: View template.
3. **CSS/SCSS (`.css`)**: Component-scoped styling.

![[Pasted image 20260705094941.png]]
<!--ID: 1783230033596-->
ENDanki


STARTanki
Basic
What is the App Component in Angular?

Back: 
The **App Component** (`AppComponent`) is the main root component of your Angular application.
It serves as the shell for the application and is the very first component loaded at startup.
<!--ID: 1783230033598-->
ENDanki


STARTanki
Basic
How do you generate a new component using the Angular CLI?

Back: 
Use the generate command to automatically create the component files and link them:
`ng generate component [name]`
Or the shorthand: `ng g c [name]`

![[Pasted image 20260705095233.png]]
<!--ID: 1783230033600-->
ENDanki


STARTanki
Basic
What are Parent-Child Components in Angular?

Back: 
A **Parent-Child** relationship means one component (parent) includes another component (child) inside its HTML template.
This is achieved by using imports to reference the child, and then placing the child component's **selector** inside the parent's HTML.

![[Pasted image 20260705095425.png]]
<!--ID: 1783230033602-->
ENDanki


STARTanki
Basic
What is the purpose of the `export` keyword in an Angular component?

Back: 
The `export` keyword applied to the component's TypeScript `class` allows the component to be imported and used by other files in the application scope.

![[Pasted image 20260705095711.png]]
<!--ID: 1783230033604-->
ENDanki


STARTanki
Basic
What is the role of the `index.html` file in the startup flow?

Back: 
`index.html` is the primary page loaded by the browser for the SPA.
It contains the `<app-root>` tag inside the body, which Angular targets to inject the initial application component.

![[Pasted image 20260705095838.png]]
![[Pasted image 20260705100056.png]]
<!--ID: 1783230033606-->
ENDanki


STARTanki
Basic
What is the role of the `main.ts` file and `bootstrapApplication()`?

Back: 
`main.ts` is the entry point of your Angular app. It tells Angular which component to load first and boots up the framework in the browser.
The `bootstrapApplication(App, appConfig)` method triggers this process by loading the root `AppComponent`.

![[Pasted image 20260705100300.png]]
<!--ID: 1783230033607-->
ENDanki


STARTanki
Basic
What is the role of the `angular.json` file?

Back: 
`angular.json` is the central configuration file for the Angular CLI workspace.
It manages project-specific settings, build path definitions, and environment configurations.

![[Pasted image 20260705100410.png]]
<!--ID: 1783230033609-->
ENDanki


STARTanki
Basic
Summarize the Angular application loading flow.

Back: 
1. `angular.json` directs the build to the entry points (`main.ts` and `index.html`).
2. The browser loads `index.html`.
3. `main.ts` executes and calls `bootstrapApplication()`.
4. The root `AppComponent` is rendered inside the `<app-root>` tag in the index DOM.
<!--ID: 1783230033611-->
ENDanki


STARTanki
Basic
What are Class Decorators and the `@Component` decorator?

Back: 
Decorators attach metadata to TypeScript classes.
The `@Component` decorator specifically flags a class as an Angular component and passes a configuration object defining its `selector`, `templateUrl`, `styleUrl`, and required `imports`.

![[Pasted image 20260705100558.png]]
![[Pasted image 20260705100749.png]]
![[Pasted image 20260705100816.png]]
<!--ID: 1783230033613-->
ENDanki


STARTanki
Basic
What is Data Binding in Angular?

Back: 
Data binding defines how data moves between the TypeScript logic files and the HTML view files.
It synchronizes the UI state and model state seamlessly.

![[Pasted image 20260705102858.png]]
![[Pasted image 20260705103114.png]]
<!--ID: 1783230033616-->
ENDanki


STARTanki
Basic
What is Interpolation in Angular?

Back: 
**Interpolation** is a one-way data binding technique used to transfer data from a component (TypeScript) to an HTML template (view).
It uses double curly braces: `{{ variableName }}`.
Flow: **TS $\rightarrow$ HTML**
<!--ID: 1783230033617-->
ENDanki


STARTanki
Basic
What is Property Binding in Angular?

Back: 
**Property Binding** dynamically sets the property of an HTML element based on a variable in the component.
It uses square brackets: `[property]="variableName"`.
Flow: **TS $\rightarrow$ HTML**

![[Pasted image 20260705103536.png]]
<!--ID: 1783230033619-->
ENDanki


STARTanki
Basic
What is Event Binding in Angular?

Back: 
**Event Binding** handles the reverse flow—listening for user actions in the HTML (clicks, typing) and triggering methods in the TypeScript logic.
It uses round parentheses: `(event)="methodName()"`.
Flow: **HTML $\rightarrow$ TS**

![[Pasted image 20260705103710.png]]
<!--ID: 1783230033621-->
ENDanki


STARTanki
Basic
What is Two-Way Data Binding in Angular?

Back: 
**Two-Way Data Binding** continuously synchronizes data between the HTML input and the TS component class.
It uses the "banana in a box" syntax: `[(ngModel)]="variable"`.
Requires the `FormsModule` to function.

![[Pasted image 20260705103926.png]]
<!--ID: 1783230033623-->
ENDanki