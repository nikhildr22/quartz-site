[[4 important design patterns]]
1. creational patterns
	1. singleton
		1. ensure the class has only one instance
		2. example: logger and configuration
		3. this is not same as singleton DI, but similar
		4. sealed and readonly class
			1. refer gemini for code example
		5. we can prevent inheritence, also only once instance can be created in entire application
	2. factory pattern
		1. provides interface for creating objects in a superclass but allows the subclass the ovverride. we use abstarct class and abstract methods to force implementation to subclasses
2. structural patterns
	1. decorators
		1. add new behavior by placing them within a decorator
		2. we can add feature dynamically at runtime 
		3. ![[decorator example]]
	2. adapter
		1. brigde between 2 incompatible interfaces
		2. example: travel adapter
		3. [[example code]]
	3. bridge
		1. decouples a an abstraction from its implementation
	4. composite
	5. fascade
	6. flyweight
	7. proxy
3. behavioral patterns
	1. observer
	2. strategy patterns