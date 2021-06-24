### Module 05:
- #### Creating functions
	- As a Statement: A function statement starts with the function keyword. It can return a primitive type value, object, or another function. The main characteristic of a function statement is it is hoisted at the top of the execution context. Therefore, you can call a function statement before it is declared
	```js
		function Add(num1,num2){
			let sum = num1+ num2; 
			return sum; 
		}
		console.log(Add(1,2));	// 3
	```
	- As an Expression: In a function expression, you assign a function to a variable. A function expression can also be created as anonymous without a name. And this is not hoisted on the top of the execution context.
	```js
		let add = function (num1,num2){
			let sum = num1+ num2; 
			return sum;
		}
		
		console.log(add(1,3));	// 3
		console.log(add);	//Note that if we don't call it with "()" will log 
							//ƒ (num1,num2){
							//let sum = num1+ num2; 
							//	return sum;
							//}
	```
	- As an Arrow Function: Besides providing shorter syntax, which increases the readability of the code, it does not have its own value of the `this` object.
	```js
		var add = (num1, num2)=> num1+num2; 
		
		let res = add(5,2);
		console.log(res); // 7 
	```
	- Using Function Constructor: A function can be dynamically created using the Function constructor, but it suffers from security and performance issues and is not advisable to use. In the Function constructor, you pass parameters and function body as a string. 
	```js
		var add = Function('num1','num2','return num1+num2');
		let res = add (7,8);
		console.log(res); // 15
	```
- #### Arrow functions
	Its a shorthanded arternative to traditional function expressions, but is limited and cant be used in all situations.
	Differences and limitations:
	- Does not have its own bindings to `this` or `super`, and should not be used as methods.
	- Does not have `arguments` or `new.target`
	- Not suitable for `call`, `apply` and `bind` methods, which generally rely on establishing a scope
	- Can not be used as constructors.
	- Can not use `yield`, within its body.
	```js
		const aPlusHundred(a) => {
 			return a + 100;
  		}
	```
	Some syntax rules for an arrow function are:
	- Parameters should be passed in a small bracket
	```js
		const sum = (firstParameter, secondParameter) => {
			return firstParameter + secondParameter;
		}
	```
	- If there is only one parameter, then the bracket is optional
	```js
		const print = printable => {
			return console.log(printable);
		}
	```
	- If there is no parameter, then it must have a small empty bracket
	```js
		const printHi = () => {
			return console.log("Hi");
		}
	```
	- If there is only a single expression in the function body, then using parentheses is optional
	```js
		const printHi = () => return console.log("Hi");
	```
	- If there is only a single expression in the function body, then using the return statement is optional
	```js
		const sum = (a, b) =>  a + b;
	```
- #### Self-invoked functions
	A JavaScript function that runs as soon as it is defined. Also known as an IIFE (Immediately Invoked Function Expression).
	```js
		(function () {
			statements
		})();
	```
	It can also be a function expression.
	```js
		let add = function (num1,num2){
			let sum = num1+ num2; 
			return sum;
		}(8,9);
		console.log(add); // 17 
	```
	##### Use cases:
	- Avoiding polluting the global namespace:
		If we have some initiation code that we don't need to use again, we could use the IIFE pattern. As we will not reuse the code again, using IIFE in this case is better than using a function declaration or a function expression.
- #### Callbacks
	A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.
	```js
		function greeting(name) {
 			alert('Hello ' + name);
  		}
		
  		function processUserInput(callback) {
			var name = prompt('Please enter your name.');
			callback(name);
  		}
		
  		processUserInput(greeting);
	```
	A simple example of a callback function in JavaScript is an ordinary button:
	```js
		document.getElementById("Button1").addEventListener("click", function() {
			console.log("Button was clicked");
		}, false);	
	```
- #### Recursion
	Recursion is a process of calling itself. A function that calls itself is called a recursive function. 
	A recursive function must have a condition to stop calling itself. Otherwise, the function is called indefinitely. Once the condition is met, the function stops calling itself. This is called a base condition.
	```js
		function recurse() {
			if(condition) {
				recurse();
			}
			else {
				// stop calling recurse()
			}
		}
		
		recurse();
	```
- #### Anonymous functions
	Anonymous Function is a function that does not have any name associated with it. Normally we use the function keyword before the function name to define a function in JavaScript, however, in anonymous functions in JavaScript, we use only the function keyword without the function name.
	An anonymous function is not accessible after its initial creation, it can only be accessed by a variable it is stored in as a _function as a value_.
	```js
		// With the function statement
		let greet = function (platform) {
    		console.log("Welcome to ${platform}!");
		};
		
		//Or with an Arrow Function
		let greet = (platform) => {
			console.log("Welcome to ${platform}!");
		};
		
		greet("GeeksforGeeks");	// "Welcome to GeekforGeeks"
	```
	We can also pass anonymous functions as paremeters into another function (callbacks).
	```js
		setTimeout(function () {
    		console.log("Welcome to GeeksforGeeks!");
		}, 2000);
	```
	We use them also in IIFE.
- #### Currying, High order functions
	- ##### High Order Functions: 
		High-order functions are functions that take another function as an argument, and/or returns another function.
		```js
			// High-order function no.1:
			// Function that takes a function as a argument
			function myHighOrderFuncOne(myFunc) {
				// some code
			}
			
			// High-order function no.2:
			// Function that returns a function
			function myHighOrderFuncTwo() {
				// some code
				// Return a function
				return function() {
					// some code
				}
			}
			
			// High-order function no.3:
			// Function that takes a function as a argument
			// and also returns a function
			function myHighOrderFuncThree(myFunc) {
				// some code
				// Return a function
				return function() {
					// some code
				}
			}
		```
		##### Built-in JavaScript high-order functions:
		- `map()`
		- `filter()`
		- `reduce()`
	- ##### Currying
		Currying is an advanced technique of working with functions. Currying is a transformation of functions that translates a function from callable as f(a, b, c) into callable as f(a)(b)(c).
		```js
			function sum (a){
				return function (b){
					return a + b;
				}
			}
			const result = sum(1)(2);
			console.log(result);	// 3
		```
		How to curry a normal function?
		```js
			function curry(func) {
				return function curried(...args) {
					if (args.length >= func.length) {
						return func.apply(this, args);
					} else {
						return function(...args2) {
							return curried.apply(this, args.concat(args2));
					  	}
				  	}
			  	};
		  	}
			function date (year, month, day){
				return `${year} ${month} ${day}`;
			}
				
			const curriedDate = curry(date);
			
			console.log(curriedDate(2000,12,1));	//2000 12 1
			console.log(curriedDate(2000)(12)(1));	//2000 12 1
			console.log(curriedDate(2000,12)(1));	//2000 12 1

		```
		What is Currying for?
		To explain this lets see the example above. We can create a function that has a fixed year, that can take any month and day but cannot change the year, lets see:
		```js
		//
			const year2000 = curriedDate(2000);	//this function has year fixed to 2000
			
			console.log(year2000(12,06)); // 2000 12 6
			console.log(year2000(3,7)); // 2000 3 5
			
			//lets create another func but with the month fixed from the year2000 function
			const year2000January = year2000(1);
			
			console.log(year2000January(31));	// 2000 1 31
			console.log(year2000January(16));	// 2000 1 16
			
		```
- #### Pure functions
	Pure Function is a function (a block of code ) that always returns the same result if the same arguments are passed. It does not depend on any state, or data change during a program’s execution rather it only depends on its input arguments. And this functions does not have side effects.
	```js
		function calculateGST( productPrice ) {
    		return productPrice * 0.05;
		}
	```
	Below are the some side effects (but not limited to) which a function should not produce in order to be considered as a pure function.
	-   Making a HTTP request
	-   Mutating data
	-   Printing to a screen or console
	-   DOM Query/Manipulation
	-   Math.random()
	-   Getting the current time
- #### Functional programming
	Functional programming is a programming paradigm or style of programming that relies heavily on the use of pure and isolated functions. In functional programming, we use pure functions, which are functions that don't have side effects.
	- Avoid mutations and side effects: 
		Avoid changing things, such as a global variable, otherwise it could lead into a bug, or an unexpected behavior. Also functions must be pure functions.
		If a function depends on a global variable, that variable should be passed to the function as an argument.
	- Abstraction:
		Abstractions hide details and allow us to talk about problems at a higher level without describing all the implementation details of the problem.
		We say _**sort**_ instead of _"put a number of things in an order"_
		Functions allows us to create our own abstractions.
- #### Context, global context
	In JavaScript, “context” refers to an object. Within an object, the keyword “this” refers to that object (i.e. “self”), and provides an interface to the properties and methods that are members of that object. When a function is executed, the keyword “this” refers to the object that the function is executed in.
	Global context refers to the window object (in browser).
	```js
		console.log(this);
		// Window {window: Window, self: Window, document: document, name: "", location: Location, …}
	```
- #### `this`
	A property of an execution context, that, in non–strict mode, is always a reference to an object and in strict mode can be any value. The value depends on where the function was called.
	```js
		const test = {
			prop: 42,
			func: function() {
				return this.prop;
			},
  		};
		console.log(test.func())	//42
	```
	- In the global execution context (outside of any function), this refers to the global object whether in strict mode or not.
	```js
		console.log(this === window);	//true in browser
		console.log(this === globalThis);	//true in node
		var a = 37;
		console.log(window.a);	// 37
	```
	- Inside a function `this` is determinated by where was the function called.
	```js
		function func() {
			console.log(this);
		}
		
		func();	// logs window
		
		// if we use "use strict"
		"use strict"; 
		function func() {
			console.log(this);
		}
		
		func();	// logs undefined
	```
	If we forget to use the `new` keyword while we use constructor functions we will refer to the global context (window).
	```js
		function Cat (breed, color){
			this.breed = breed;
			this.color = color;
		}
		
		const myCat = Cat("European", "Black");
		console.log(myCat);	//undefined
		
		//However properties will be added to the this object that referenced in the function, the window object.
		console.log(window.breed);	// "European" in browser
		console.log(globalThis.breed);	// "European" in node
	```
	If we use the `new` keyword, `this` will reference to the new object created.
	```js
		function Cat (breed, color){
			this.breed = breed;
			this.color = color;
		}
		
		const myCat = new Cat("European", "Black");
		console.log(myCat);	// {breed: "European", color: "Black"}
	```
- #### call/apply/bind
	##### Explicit binding: 
	We can force a function to use a specific value of `this`with the `apply()` and `call` methods that has the function prototype.
	Both take as a parameter the value `this` that we want them to use, that's why it's called explicit binding. They differ on the way the handle arguments, `call()` takes them individually, and `apply()` takes an array of arguments.
	```js
		var obj = {a: 'Custom'};
		
		var a = 'Global';
		
		function whatsThis() {
  			return this.a;  // The value of this is dependent on how the function is called
  		}
		
		whatsThis();	//returns 'Global'
		whatsThis.call(obj); 	// returns 'Custom'
		whatsThis.apply(obj);	// returns 'Custom'
	```
	- `call()`: takes the `this` value as first argument, and takes the function arguments individually.
	```js
		var obj = {a: 'Custom'};
		var a = 'Global';
		
		function whatsThis(f,b,c) {
			return this.a + f + b + c;  
		 }
		 
  		console.log(whatsThis.call(obj,1,2,3));	// Custom123
	```
	- `apply()`:  takes the `this` value as first argument, and takes a second value that must be an array of the arguments.
	```js
		var obj = {a: 'Custom'};
		var a = 'Global';
		
		function whatsThis(f,b,c) {
			return this.a + f + b + c;  
		 }
		 
  		console.log(whatsThis.call(obj,[1,2,3]));	// Custom123
	```
	But what the this value it still depends on where is the function called.
	```js
		var obj = {a: 'Custom'};	
		var a = 'Global';
		
		function tobeCalled(func) {
			return func()
		}
		
		function whatsThis() {
			return this.a;  
		}
		
		console.log(tobeCalled.call(obj,whatsThis)); 	// returns 'Custom'
	```
	##### Hard Binding
	There is a way to bind permanently a context to `this` no matter where was called.
	All functions have a method called `bind()` from the function prototype, this method returns a function that is binded with the `this` value you want, no matter where context you called it.
	```js
		function sayHi() {
			return 'Hi, my name is ' + this.name;
		}
		
		var person =  {
			name: 'Juan',
		};
		
		var greeting = sayHi.bind(person);	//hard binding into person context
		
		greeting(); // "Hola, me llamo Juan"
		
		function Person(greet) {
			this.name = "Pedro";
			this.greeting1 = sayHi.call(this);  
			this.greeting2 = greet.call(this);  
		}
		
		const nPerson = new Person(greeting)
		console.log(nPerson.greeting1);  //binds it to this obj and logs Pedro
		console.log(nPerson.greeting2);  //cannot re-bind, and logs Juan
	```
- #### Immutable
	

