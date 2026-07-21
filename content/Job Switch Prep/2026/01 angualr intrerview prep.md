1. Life cycle hooks
	1. implement onInit, onDestroy
	2. ngonChnages
		1. input property is just to pass the data in beginning, we can use the value in ngOnInit to trigger any logic
		2. but if we need to listen to any change in input and perform a logic in ts, we can use ngOnChanges
		3. we can use signals as alternative for it, and use `effect` inside a constructor
			1. we can have multiple effects within a constructure, effect only run when we use a signal inside that effect, this way all effect blocks wont be triggered
	3. ngOnInit
		1. runs only once during life cycle of component initially
		2. 
	4. ngDoChecked
	5. ngAfterContentInit
	6. ngAfterContentChecked
	7. ngAfterViewInit
	8. ngAfterViewChecked
	9. ngOnDestroy
2. [[Tempolate driven vs reactive driven forms]]
3. [[pure and impure pipes]]
4. 3 main structure of angualkr component
	1. html
	2. css
	3. ts
5. 4 types of data binding
	1. interpolation
		1. use double braches {{}} to show varible directly on html
	2. property binding
		1. used to control the `[]` to bind a html propertly like `disabled` mapped to a ts variable
	3. event binding
		1. wrapped in `()` open braces, then a method to handle the logic when a event like (click) happens
	4. 2 way binding
		1. `[(ngModel)]` is used
			1. its mainly for forms
			2. this syntax is called banana in a box
			3. in ts there'll be property
6. Directives
	1. 3 types
		1. component directives
			1. just component
			2. uses @Component directive
		2. attribute directive
			1. ngclass, ngStyle
			2. custom directives
				1. use @Directive decorator
				2. use @HostListener to configure the logic
		3. structural directives
			1. ngif and ngfor
			2. custom structural directive
				1. we can research later
7. Services in angualr
	1. decorate with @Injectable decorator
	2. use providedIn: 'root'
		1. singleTon dependency injection
	3. if you want to provide a service at component level user `providers` array, 
		1. if provider is mentioned, angular will ignore the root instance and use the fresh instance of a service for this specific component
	4. Resolution modifiers
		1. @Host
		2. @Self
		3. @SkipSelf
			1. check gemini code on why we need it
		4. @Optional
8. routing
	1. more like internal map of application
	2. route to a page without refreshing the entire page
	3. routes.ts will have code for it
		1. single array Routes
			1. path
			2. component
			3. redirectTo
			4. children
				1. mainly used for Lazy loading
		2. route guards
			1. AuthGuard
				1. general guard
					1. [[syntax on how to create a custom guard]]
			2. CanActivate
				1. used to actually activate the guard
			3. CanDeactivate
				1. activates when you are trying to leave a component or route
9. [[change detection in angular]]
	1. decides how inputs should trigger change detection
	2. onPush strategy
		1. change detection wont be triggered unless new object is assigned
		2. but value can be changed, but change detector wont update the view
		3. use cdr.MarkForCheck when you know the value is changed but the reference isnt, this way from parent we can trigger a change detection even with onPush strategy
	3. default strategy
		1. simply updates the view whenever the value changes
10. RxJs
	1. reactive extension for angular
	2. Promise
		1. single event
	3. Observable
		1. continous data stream
	4. they are like processing stations, they allow us to transform or manipulate data
	5. we use Pipe fucntion to use the rxJs operator
	6. Map
		1. maps the response to a function which transforms the data
	7. switchmap
		1. prevents unnessary network traffic
		2. mainly used for search bar inputs
	8. filter
		1. filter logic
	9. debounceTime
		1. makes sure we dont send request too often over a network
	10. combineLatest
		1. combining the outputs of multiple outputs
		2. lets say 3 sources
			1. first it'll wait for all 3 sources to emit atleast 1 value each
			2. it'll take latest values when all 3 are ready and emit a final value
			3. after first emission, even if single a single value is emitted there'll be emissiion from combineLatest
	11. forkJoin
		1. waits for all service calls are completed
	12. Mergemap
		1. unlike switchMap, it wont cancel the last request
		2. best use case is uploading files or collecting some data,
	13. CatchError
		1. it intercepts any error and apply custom logic
11. State management
	1. Component state -  basic is using input output betweeen parent children
		1. use @Input and @Output decorator coupled with eventEmitter
	2. service with RxJs, used a service to manage state between unrelated components using Behaviorsubject
		1. subject vs behaviorSubject
		2. subject does not need a initial value
			1. example - global notification. it does not need a past data, all it cares about is current latest data emitted.
		3. Behavior subject needs a initial value
			1. for example, to decide whther the page should load in dark or light mode we need a initial data
	3. Dedicated libraries like NgRx or Akita
		1. check the code in gemini chat on how we can use NgRx 
	4. Angular signals
		1. they eliminate the complexity of behavior subject entirely
			1. we dont need to subscribe first etc
			2. just access the variable directly, as if its a local variable of current component, angular automatically handles the behind the scenes stuff
			3. refer code example of counter
		2. computed signals
			1. learn again and see why we need these, because behavior subject subscription had flexibility to use RxJs operator
