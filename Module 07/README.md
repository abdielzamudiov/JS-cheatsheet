## Module 07:
- ### Prototype, prototype chaining
	- Prototypes are the mechanism by which JavaScript objects inherit features from one another. Prototypes can be used to add properties and methods into existing constructor.Prototypes are the mechanism by which JavaScript objects inherit features from one another. Prototypes can be used to add properties and methods into existing constructor.
	- In the case you want to add one property into an existing constructor, you can’t add it directly like this.
	```js
		Person.gender = ‘Male’;
	```
	- It will give you undefined when you try to access it. Instead, use a prototype to add properties and methods in the constructor.
	```js
		Person.prototype.gender = 'male'
	```
	- The methods that are defined in Object’s prototype property are called **prototype chaining**.
	- JavaScript objects inherit properties and methods from prototype.
	
	
- ### __proto__
	- `__proto__` is a way to inherit properties from an object in JavaScript.
	- The `__proto__` property of `Object.prototype` is an accessor property (a getter function and a setter function) that exposes the internal `[[Prototype]]` (either an object or `null`) of the object through which it is accessed.
	- The `__proto__` getter function exposes the value of the internal `[[Prototype]]` of an object.
	- The `__proto__` property is a simple accessor property on `Object.prototype` consisting of a getter and setter function. A property access for `__proto__` that eventually consults `Object.prototype` will find this property, but an access that does not consult `Object.prototype` will not. If some other `__proto__` property is found before `Object.prototype` is consulted, that property will hide the one found on `Object.prototype`.
	```js
		const l = console.log
		
		const obj = {  
			method: function() {  
				l("method in obj")  
			}  
		}  
		const obj2 = {}
		
		obj2.__proto__ = obj  
		obj2.method()
	```
	- If you care about performance you should avoid setting the `[[Prototype]]` of an object. Instead, create a new object with the desired `[[Prototype]]` using `Object.create()`.
	- `__proto__` is the actual object that is used in the lookup chain to resolve methods, etc. `prototype` is the object that is used to build `__proto__` when you create an object with `new`:
	```js
		( new Foo ).__proto__ === Foo.prototype;
		( new Foo ).prototype === undefined;
	```

- ### ES6 inheritance
	- Classes support prototype-based **inheritance**, **super calls**, **instance** and **static methods** and **constructors**.
	```js
		class Vehicle {  
   
		  constructor (name, type) {  
			this.name = name;  
			this.type = type;  
		  }  

		  getName () {  
			return this.name;  
		  }  

		  getType () {  
			return this.type;  
		  }  

		}class Car **extends** Vehicle {  

		  constructor (name) {  
			**super**(name, 'car');  
		  }  

		  getName () {  
			return 'It is a car: ' + **super**.getName();  
		  }  

		}let car = new Car('Tesla');  
		console.log(car.getName()); // It is a car: Tesla  
		console.log(car.getType()); // car
	```
	- We use **extends** to inherit from another class and the **super** keyword to call the parent class (function). Moreover, **getName()** method was overridden in subclass **Car**.

- ### Prototypal inheritance
	- When we read a property from `object`, and it’s missing, JavaScript automatically takes it from the prototype. In programming, this is called “prototypal inheritance”.
	```js
	let animal = { 
		eats: true, 
		walk() { 
			alert("Animal walk"); 
		} 
	}; 
	
	let rabbit = { 
		jumps: true, 
		___proto__: animal_ 
	}; 
	
	let longEar = { 
		earLength: 10, 
		___proto__: rabbit_ 
	}; // walk is taken from the prototype chain 
	
	longEar.walk(); // Animal walk 
	alert(longEar.jumps); // true (from rabbit)
	```
	- Here we can say that "`animal` is the prototype of `rabbit`" or "`rabbit` prototypically inherits from `animal`".
	- So if `animal` has a lot of useful properties and methods, then they become automatically available in `rabbit`. Such properties are called “inherited”.
	- There are only two limitations:
		1.  The references can’t go in circles. JavaScript will throw an error if we try to assign `__proto__` in a circle.	
		2.  The value of `__proto__` can be either an object or `null`. Other types are ignored.
	- Also it may be obvious, but still: there can be only one `[[Prototype]]`. An object may not inherit from two others.
	- In prototypal inheritance, objects are created using the `new` keyword, and inheritance is achieved by linking the object’s prototype to another object’s prototype.
	```js
		// Function wiring prototypes to achieve inheritance
		function inherits(Parent, Child) {
			function F() {}
			F.prototype = Parent;
			Child.prototype = new F();
		}

		// Base class
		function Base(spec) {
			this.name = spec.name; // Define the "name" property
		}

		// Child class
		function Child(spec) {
			Base.call(this, spec); // Call the base class constructor
		}
		inherits(Base, Child); // Wire prototypes
		Child.prototype.sayHello = function () { // Define the "sayHello" method
			return 'Hello, I\'m ' + this.name;
		};

		// Usage
		var object = new Child({ name: 'a prototypal object' });
		result.textContent = object.sayHello();
	```
	- I see the following advantages of the use of the prototypal inheritance pattern:
		-   **performance**: prototypal object creation involves less steps than functional objects creation, thus prototypal object creation is faster than functional object creation (**by several orders of magnitude**, as you’ll see below) ;
		-   **dynamsim**: one can add methods to a prototype at any time and these methods will automatically be available on all objects inheriting this prototype ;
		-   **reflection**: though this is not very important, you can test if an object is of some type by using the `instanceof` operator, which is not feasible with functional inheritance.

- ### Functional inheritance
	- Functional inheritance is the process of inheriting features by applying an augmenting function to an object instance. The function supplies a closure scope which you can use to keep some data private. The augmenting function uses dynamic object extension to extend the object instance with new properties and methods.
	```js
		// Base object constructor function
		function base(spec) {
			var that = {}; // Create an empty object
			that.name = spec.name; // Add it a "name" property
			return that; // Return the object
		}

		// Construct a child object, inheriting from "base"
		function child(spec) {
			var that = base(spec); // Create the object through the "base" constructor
			that.sayHello = function() { // Augment that object
				return 'Hello, I\'m ' + that.name;
			};
			return that; // Return it
		}

		// Usage
		var object = child({ name: 'a functional object' });
		result.textContent = object.sayHello();
	```
	- Basically, an object constructor function creates an empty object and adds it some methods before returning it. Inheritance is achieved in this object constructor function by getting the object through another object constructor function instead of creating an empty one.
	- Is see the following advantages of the use of the functional inheritance pattern:
		-   **simplicity**: a few steps are required to achieve inheritance ;
		-   **“this”-free**: you don’t have to care with the context variable “this”, meaning that **you can freely pass any method of a functional object as a callback parameter** and everything will work as expected;
		-   **encapsulation**: objects can have private (and even protected) members.