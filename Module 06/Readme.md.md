### Module 06:
- #### ES6 vs ES5 classes
 	ES6 provides new features as well as a cleaner approach for some of the existing features in ES5.
	1. **Improved getter/setter property syntax.** The object properties require get/set methods to be called on them to access/modify their values. In the ES5 version, they were not widely used because the syntax was not that clean.
	2. **Improved syntax for prototype inheritance.**  In the ES5 version, _prototypal inheritance_ is not an easy task. The code is hard to follow and takes a lot of effort to write as well as understand.
	3. **Class keyword added.** In the ES5 version, there are no classes; a _function_ is used to make an object directly. However, the ES6 version uses the keyword `class` to define a class.
	4. **Cleaner constructor function syntax.** In the ES5 version, constructor functions are declared using the `function` keyword, with the body of the code initializing the object properties upon its creation. The ES6 version, on the other hand, uses the `constructor` keyword to declare the constructor function which runs on object creation:
		```js
			class Car {  
 				constructor(name, year) {  // constructor
 					this.name = name;  
 					this.year = year;  
 				}  
				
 				get age() { // getter property syntax
 					let date = new Date();  
 					return date.getFullYear() - this.year;  
 				}  
			}  
  
			let myCar = new Car("Ford", 2014);    
			console.log(`My car is ${myCar.age} years old.`);  
		```
	1. **Extends and super keywords added.** The ES6 version offers an improved and cleaner syntax by using the _keyword_ `extends` for setting up the inheritance relationship between parent and child.   
		```js
			class Animal { 
				constructor(name) { 
					this.speed = 0; 
					this.name = name; 
				} 
				run(speed) { 
					this.speed = speed; 
					alert(`${this.name} runs with speed ${this.speed}.`); 
				} 
				stop() { 
					this.speed = 0; 
					alert(`${this.name} stands still.`); 
				} 
			}
			
			class Rabbit extends Animal { 
				hide() { 
					alert(`${this.name} hides!`); 
				} 
			}
			
			let rabbit = new Rabbit("White Rabbit");
			rabbit.run(5); // White Rabbit runs with speed 5. 
			rabbit.hide(); // White Rabbit hides!
		```
		This is a new feature introduced in the ES6 version. `super` is used to call the constructor on the parent object that is being inherited by the child. It is used to avoid duplication of the parts of the constructor that are present in both the parent and child class.
	6. **Static keyword added.** JavaScript did allow for static members to be declared in the ES5 version. However, the ES6 version formalizes this by introducing the _keyword_ `static`.
		```js
			class Tripple {
  				static tripple(n) {
    					n = n || 1;
    					return n * 3;
  				}
			}

			class BiggerTripple extends Tripple {
  				static tripple(n) {
    					return super.tripple(n) * super.tripple(n);
  				}
			}

			console.log(Tripple.tripple()); // output: 3
			console.log(Tripple.tripple(6)); // output: 18
			console.log(BiggerTripple.tripple(3)); // output: 81
			var tp = new Tripple(); console.log(tp.tripple()); //Logs 'tp.tripple is not a function'.
		```
- #### Operator "new"
	The regular `{...}` syntax allows to create one object. But often we need to create many similar objects, like multiple users or menu items and so on.
	That can be done using constructor functions and the `"new"` operator. It lets developers create an instance of a user-defined object type or of one of the built-in object types that has a constructor function.
	##### Constructor function
	Constructor functions technically are regular functions. There are two conventions though:
	1.  They are named with capital letter first.
	2.  They should be executed only with `"new"` operator.   

	For instance:
	```js
		function User(name) { 
			this.name = name; 
			this.isAdmin = false; 
		} 
		let user = new User("Jack");
		
		console.log(user.name); // output: Jack 
		console.log(user.isAdmin); // output: false
	```
    When a function is executed with `new`, it does the following steps:
	1. A new empty object is created and assigned to `this`.
	2.  The function body executes. Usually it modifies `this`, adds new properties to it.
	3.  The value of `this` is returned.

	In other words, `new User(...)` does something like:
	```js
		function User(name) { 
			// this = {}; (implicitly) 
			// add properties to this 
			this.name = name; 
			this.isAdmin = false; 
			// return this; (implicitly) 
		}
	```
	Now if we want to create other users, we can call `new User("Ann")`, `new User("Alice")` and so on. Much shorter than using literals every time, and also easy to read.
	That’s the main purpose of constructors – to implement reusable object creation code.
- #### Operator "super"
	Usually, in inheritance we don’t want to totally replace a parent method, but rather to build on top of it to tweak or extend its functionality. We do something in our method, but call the parent method before/after it or in the process.
	Classes provide `"super"` keyword for that.
	-   `super.method(...)` to call a parent method.
	-   `super(...)` to call a parent constructor (inside our constructor only).   
	
	For instance, let's create a rabbit that automatically hides when stopped:
	```js
		class Animal { 
			constructor(name) { 
				this.speed = 0; 
				this.name = name; 
			} 
			
			run(speed) { 
				this.speed = speed; 
				alert(`${this.name} runs with speed ${this.speed}.`); 
			} 
			
			stop() { 
				this.speed = 0; 
				alert(`${this.name} stands still.`); 
			} 
		} 
		
		class Rabbit extends Animal { 
			hide() { 
				alert(`${this.name} hides!`); 
			} 
			
			stop() { 
				super.stop(); // call parent stop 
				this.hide(); // and then hide 
			} 
		} 
		
		let rabbit = new Rabbit("White Rabbit"); 
		rabbit.run(5); // White Rabbit runs with speed 5. 
		rabbit.stop(); // White Rabbit stands still. White Rabbit hides!
	```
	Now `Rabbit` has the `stop` method that calls the parent `super.stop()` in the process.
- #### Return from constructor
	The `constructor` method is a special method of a [`class`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/class) for creating and initializing an object of that class.
	Syntax:
	```js
		constructor() { ... }
		constructor(argument0) { ... }
		constructor(argument0, argument1) { ... }
		constructor(argument0, argument1, ... , argumentN) { ... }
	```
	If you don't provide your own constructor, then a default constructor will be supplied for you. If your class is a base class, the default constructor is empty:
	```js
		constructor() {}
	```
	If your class is a derived class, the default constructor calls the parent constructor, passing along any arguments that were provided:
	```js
		constructor(...args) {
  			super(...args);
		}
	```
	And the constructor returns the `this` object.
	```js
		function Car() {
   			this.num_wheels = 4;
		}

		let car = new Car(); // output: Car { num_wheels: 4 };
	```
	By the Javascript spec, when a function is invoked with `new`, Javascript creates a new object, then sets the "constructor" property of that object to the function invoked, and finally assigns that object to the name `this`. You then have access to the `this` object from the body of the function. 
	Once the function body is executed, Javascript will return **ANY object** if the type of the returned value is `object`:
	```js
		function Car() {
  			this.num_wheels = 4;
  			return { num_wheels: 37 };
		}

		let car = new Car();
		console.log(car.num_wheels); // output: 37
	```
	The `this` object if the function has no `return` statement OR if the function returns a value of a type other than `object`:
	```js 
		function Car() {
  			this.num_wheels = 4;
  			return 'VROOM';
		}

		let car = new Car();
		console.log(car.num_wheels); // output: 4
		console.log(Car()); // No 'new', so the alert will show 'VROOM'
		console.log(new Car()); // output: Car { num_wheels: 4 };
	```
- #### Operator "instance of"
	The `instanceof` operator allows to check whether an object belongs to a certain class. It also takes inheritance into account.
	Such a check may be necessary in many cases. For example, it can be used for building a _polymorphic_ function, the one that treats arguments differently depending on their type.   
	Syntax:
	```js
		obj instanceof Class
	```
	It returns `true` if `obj` belongs to the `Class` or a class inheriting from it.   
	For instance:
	```js
		class Rabbit {}
		let rabbit = new Rabbit();
		
		// is it an object of Rabbit class?
		alert( rabbit instanceof Rabbit ); // true
	```
	It also works with constructor functions:
	```js
		// instead of class
		function Rabbit() {}
		alert( new Rabbit() instanceof Rabbit ); // true
	```
	…And with built-in classes like `Array`:
	```js
		let arr = [1, 2, 3];
		alert( arr instanceof Array ); // true
		alert( arr instanceof Object ); // true
	```
	Please note that `arr` also belongs to the `Object` class. That’s because `Array` prototypically inherits from `Object`.
	Normally, `instanceof` examines the prototype chain for the check. We can also set a custom logic in the static method `Symbol.hasInstance`.
- #### Static properties
	Static properties are used when we’d like to store class-level data, also not bound to an instance. They look like regular class properties, but prepended by `static`.
	Syntax:
	```js
		class MyClass {
			static property = ...;
			
			static method() {
				...
			}
		}
	```
	Technically, static declaration is the same as assigning to the class itself:
	```js
		MyClass.property = ...
		MyClass.method = ...
	```
	Static properties and methods are inherited.
	For `class B extends A` the prototype of the class `B` itself points to:
	`A`: `B.[[Prototype]] = A`.
	So if a field is not found in `B`, the search continues in `A`.
	Example:   
	```js
		class Article {
			static publisher = "Ilya Kantor";
		}
		alert( Article.publisher ); // Ilya Kantor
	```
	That is the same as a direct assignment to `Article`:
	```js
		Article.publisher = "Ilya Kantor";
	```
- #### Private properties
	There’s a finished JavaScript proposal, almost in the standard, that provides language-level support for private properties and methods.
	
	Privates should start with `#`. They are only accessible from inside the class.
	For instance, here’s a private `#waterLimit` property and the water-checking private method `#fixWaterAmount`:
	```js
		class CoffeeMachine { 
			#waterLimit = 200;
			
			#fixWaterAmount(value) { 
				if (value < 0) return 0; 
				if (value > this.#waterLimit) return this.#waterLimit; 
			} 
			
			setWaterAmount(value) { 
				this.#waterLimit = this.#fixWaterAmount(value); 
			} 
		
		} 
		let coffeeMachine = new CoffeeMachine(); 
		
		// can't access privates from outside of the class
		coffeeMachine.#fixWaterAmount(123); // Error 
		coffeeMachine.#waterLimit = 1000; // Error
	```
	On the language level, `#` is a special sign that the field is private. We can’t access it from outside or from inheriting classes.

	Private fields do not conflict with public ones. We can have both private `#waterAmount` and public `waterAmount` fields at the same time.
	For instance, let’s make `waterAmount` an accessor for `#waterAmount`:
	```js
		class CoffeeMachine { 
			#waterAmount = 0; 
			get waterAmount() { 
				return this.#waterAmount; 
			} 
			
			set waterAmount(value) { 
				if (value < 0) value = 0; 
				this.#waterAmount = value; 
			} 
			
		} 
		let machine = new CoffeeMachine(); 
		machine.waterAmount = 100; 
		alert(machine.#waterAmount); // Error
	```
	Unlike protected ones, private fields are enforced by the language itself. That’s a good thing.

	But if we inherit from `CoffeeMachine`, then we’ll have no direct access to `#waterAmount`. We’ll need to rely on `waterAmount` getter/setter:
	```js
		class MegaCoffeeMachine extends CoffeeMachine { 
			method() { 
				alert( this.#waterAmount ); // Error: can only access from CoffeeMachine 
			} 
		}
	```
	In many scenarios such limitation is too severe. If we extend a `CoffeeMachine`, we may have legitimate reasons to access its internals. That’s why protected fields are used more often, even though they are not supported by the language syntax.
	As we know, usually we can access fields using `this[name]`:
	```js
		class User { 
			... 
			
			sayHi() { 
				let fieldName = "name"; 
				alert(`Hello, ${this[fieldName]}`); 
			} 
		}
	```
	With private fields that’s impossible: `this['#name']` doesn’t work. That’s a syntax limitation to ensure privacy.