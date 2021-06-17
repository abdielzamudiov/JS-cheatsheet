## Module 01:
- #### How to run JS
	1. Command line: with nodejs
	```js
		node index.js
	```
	2. From the browser: Create a HTML file that references to JS script.
	```html
		<html>
			<head>
				<script defer src="./index.js"></script>
			</head>
		</html>
	```
	3. From the Browser console: ```ctrl+shift+J```
- #### JS syntax
	1. Variable Asignment:
	```js
		//Variable asignment
		var x,y,z;
		x = 7; y = y;
		z = x + y;
	```
	2. Literals:
	```js
		//Two most important syntax rules for fixed values are
		10.50 //Numbers type can be with decimal
		12938 //Numbers type can be without decimal
		"Strings can be double quote"
		'or can be single quote'
	```
	3. Operators:
	```js
		//Asignment operator
		var x = 4 * 5;
		
		//Arithmetic operators "( + - * / )" (just like algebra)
		(5 + 6) * 10
	```
	4. Expresions: an expression is a combination of values, variables, and operators, which computes to a value.
	```js
		//Computes (Evaluate) to 50
		5 * 10
	
		//Expressions can also contain variables
		x * 5
	
		//The values can be of various types, numbers and strings
		"John" + " " + "Doe"
	```
	5. Keywords: Keywords are reserved words in JavaScript that you cannot use to indicate variable labels or function names. There are a total of 63 keywords that JavaScript provides to programmers. 
- #### Loops, switch case
	1. Loops: 
		- ```for``` statement: repeats until a specified condition evaluates to ```false```
		```js
			//                       |	specified condition	 |
			//                       |   if this is true     |  
			for ([initialExpression]; [conditionExpression]; [incrementExpression]) {
				// do this
				statement	
			}

			// Example
			for (let i = 0; i < selectObject.options.length; i++) {
				if (selectObject.options[i].selected) {	
					numberSelected++;
				}
			}
		```
		- ```do...while``` statement: repeats until a specified condition evaluates to false.
		```js
			do
				statement //this always excecuted ONCE before evaluate condition
			while (condition); // if condition is true, the statement executes again

			// Example
			let i = 0;
			do {
				i += 1;
				console.log(i);
			} while (i < 5);
		``` 
		- ```while``` statement: executes its statements as long as a specified condition evaluates to true.
		```js
			while (condition) // The condition test occurs before statement
				statement

			// Example: The following while loop iterates as long as n is less than 3:
			let n = 0;
			let x = 0;
			while (n < 3) {
				n++;
				x += n;
			}
		```
		- ```labeled``` statement: provides a statement with and identifier, that you can refer to identify a loop and use ```break``` or ```continue``` to interrupt that loop you are referring to.
		```js
			label :
				statement	

			// Example, the same goes with "break"
			loop1:
			for (i = 0; i < 3; i++) {  //The first for statement is labeled "loop1"
				loop2:
				for (j = 0; j < 3; j++) {  //The second for statement is labeled "loop2"
					if (i === 1 && j === 1) {
						continue loop1; //skip to the next iteration of the "loop1" loop
					}
					console.log('i = ' + i + ', j = ' + j);
				}
			}
		```
		- ```break``` statement: it is used to terminate a loop, switch or in conjuction with a labeled statement.
		```js
			// Example
			for (i = 0; i < 10; i++){
				doStuff();
				if (eo)
					break;
				console.log("if break is executed, this won´t appear and the loop is terminated");
			}
		```
		- ```continue``` statement: can be used to skip to the next iteration.
		```js
			// Example
			for (i = 0; i < 10; i++){
				doStuff();
				if (eo)
					continue;
				console.log("if break is executed, this won´t appear only in the iteration that 'continue' was called, it won't end the loop like 'break' does");
			}
		```
		- ```for...in``` statement: iterates a specified variable over all de properties of an **object**. supports (continue, break). It iterates over property names.
		```js
			const obj = {
				aKey: "value",
				anotherKey: "another value"
			}
			for (variable in object)
				statement
			// Example
			for (let i in obj){
				console.log(i); // key of the property of the obj
				console.log(obj[i]) // value of the property of the obj
			}
			// first iteration console res: aKey, "value"
			// second iteration console res: anotherKey, "another value"
		```
		- ```for...of``` statement: creates a loop iterating over [iterable objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols) ( [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array), [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map), [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set),[arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments) object). It iterates over property values:
		```js
			for (variable of object)
				statement
			const arr = [3, 5, 7];
			// Example
			for (let i in arr){
				console.log(i); //logs 3, 5, 7
			}
		```
- #### Alert, console
	1. Alert: The alert() method displays an alert box with a specified message and an OK button.

		An alert box is often used if you want to make sure information comes through to the user.
	```js
		alert(message) // only parameter is message, it is of string type
	```
		
	2. Console: is an object that provides access to the browser's debugging console, it has a lot of [methods](https://developer.mozilla.org/en-US/docs/Web/API/console#methods). Most used methods are [```console.log()```](https://developer.mozilla.org/en-US/docs/Web/API/Console/log), [```console.info()```](https://developer.mozilla.org/en-US/docs/Web/API/Console/info), [```console.warn()```](https://developer.mozilla.org/en-US/docs/Web/API/Console/warn), [```console.error()```](https://developer.mozilla.org/en-US/docs/Web/API/Console/error)
	```js
		console.log("here goes whatever you wanna log in the console");
	```
- #### Variables
	In JS we use ```var``` or ```let``` keyword to declare variables.
	```js
		let x;
		var y;
	```
	We use the assignment operator ```=``` to assign a value to a variable.
	```js
		let x = 6;
	```
	If you use a variable without initializing it, it will have an ```undefined``` value.
	Rules: 
	1. Variables must start with either alleter, an underscore ```_```or the ```$``` sign.
	2. Variable names cannot start with numbers.
	3. JS is case-sensitive. So ```x``` and ```X``` are different variables.
	4. Keywords cannot be used as variable names.
	**JS Constans**:
	The ```const``` keyword was introduced in the ES6(ES2015) version to create constants. As a constant his value can't be reasigned, and must be initializated when declarated.
	```js
		const x = 5; //initialize when declaration, otherwise will throw error
	```
- #### Data types, typeof
	-```String``` : represents textual data
	```js
		"hello"
		'hello world'
	```
	- ```Number```: an integer or a floating number. Represents numeber less than (2^53 -1) and more dan -(2^53 -1)
	```js
		3
		3.1416
		3e-2
		+Infinity
		-Infinity
		NaN
	```
	- ```BigInt```: an integer with arbitrary precision. Is created by appending n to the end of an integer. Can store a larger number tan ```Number```. BigInt and Number cannot be added.
	```js
		const value = 900719925124740999n
		const result2 = value + 1 ///this will throw error
	
	```
	- ```Boolean```: Any of two values: ```true``` or ```false```
	- ```undefined```: a data type whose variable is not initialized. It can also be explicitly assigned, but is recommended to assign null instead of undefined to an unknown or empty variable.
	- ```null```: denotes a ```null``` value.
	- ```Symbol```:  data type whose instances are unique and inmutable. 
	```js
		let value1 = Symbol('hello');
		let value2 = Symbol('hello');
		value1 === value2 //this evaluate to false 
	```
	- ```Object```: key-value pairs of collection of data.
		```js
		let student = {
			firstName: "Juan",
			lastName: null,
			class: 10
		};
	```
	**typeof**
	To find the type of a variable, you can use the ```typeof``` operator.
	```js
		const name = "ram";
		typeof(name); // returns "string"
	```
- #### Functions: basics
	- Declaring a function:
		- A function is declared using the function keyword.
		- Naming a function is similar to name a variable. You should write descriptive names for your functions.
		- The body of the function is written within ```{}```
	```js
		function nameOfFunction () {
			// function body   
		}
	```
	- Calling a Function: we can call a function by writing the name followed by parentheses.
	```js
		function hello(){
			console.log("hello")
		}
		hello() // calling the function hello
	```
	- Functions Parameters: a function can also be declared with parameters. A parameter is a value that is passed when declaring a function.
	```js
		function hello(parameter){
			console.log(parameter) 
		}
		hello("hello world") // calling the function hello
	```
- #### Returning value from a function
We can return values from a function when we use the ```return``` statement, this statement denotates that the function has ended. Any code after ```return``` is not executed.
```js
	function add(a, b) {
		return a + b;
	}
	console.log(add(3,6)) // this will log 9
```
- #### Types convertions
	There are two types of type conversion in JS: 
	1. Implicit Conversion: automatic type conversion.
	```js
	// Implicit conversion to string using + operator
		let result = "3" + 2; //result "32"
		result = '3' + true; // result "3true"
		result = '3' + undefined; // result 3undefined
		result = '3' + null; // result 3null
		//Implicit conversion to number with - , / , * operators
		result = '4' - '2'; // result 2
		result = '4' - 2; // result 2
		result = '4' * 2; // results 8
		result = '4' / 2; // results 2
		// If we use those operators on non numerical values we get NaN as result
		result = 'hello' - 'world'; // results NaN
		// Boolean conversion to number true = 1, false = 0
		result = '4' - true; // 3
		result = '4' + true; // 5
		result = '4' + false; // 4
	```
	2. Explicit Conversion: manual type conversion.
	```js
		// Convert to Number
		result = Number('324') // 324 
		// Empty strings and null values return 0
		result = Number(' ') // 0
		// If is an invalid number it will return NaN
		result = Number("hello") // NaN

		//Convert to String
		result = String(324) // "324", this way can turn undefined and null values
		result = (324).toString() // "324" while this way will trhow error when converting undefined or null

		//Convert to Boolean
		// undefined, null, 0, "", converts to false
		result = Boolean("") // false
		//All other values give true
		result = Boolean("Hello") //true
	```
- #### Comparisons
	Comparitionso operators compare two calues and give back a boolean value: either ```true``` or  ```false```
	- ```==```: Equal to, true if the operands are equal.
	- ```!=``` Not equal to; true if operands are nos equal.
	- ```===``` Strict equal to; true if the operands are equal and of the same type.
	- ```!==``` Strict not equal to; true if operands are equal but of different type or not equal at all.
	- ```>``` Greater than; true if the left operand is greater than the rigth operand.
	- ```>=``` Greater or equal to; true if the left operand is greater than or equal to the right operand.
	- ```<``` Less than; true if the left operand is less than the right operand.
	- ```<=``` Less than or equal to; true if the left operand is less than or equal to the right operand.
- #### Operators: Logical, Conditional
	1. Logical operators perform logical operations: AND, OR and NOT.
		- ```&&``` Logical AND
		- ```||``` Logical OR
		- ```!``` Logical NOT
	2. Conditional operator.
		- Ternary operator: is the only JS operator that takes three operands; a condition followed by a question mark (```?```), then an expression to execute if the condition is truthly. Followed by a colon (```:```), and finally the expression to execute if the condition is falsy. This is frequently used as a shortcut for the if statement.
		```js
			function getFee(isMember) {
				return (isMember ? '$2.00' : '$10.00');
			}
			console.log(getFee(true));
			// expected output: "$2.00"
			console.log(getFee(false));
			// expected output: "$10.00"
			console.log(getFee(null));
			// expected output: "$10.00"
		```
- #### Objects: basics
	An object is a collection of properties, and a property is an association between a name (or key) and a value.
	 The properties of an object define the characteristics of the object. You access the properties of an object with a simple dot-notation:
	 ```js
		 // creating with the new keyword
		 const coolCharacter = new Object({name : "Mia"});

		 // or creating by using an object initializer
		 const coolCharacter = {
			name: "Mia",
		 }

		 console.log(coolCharacter); // {name: "Mia"}
		 coolCharacter.lastName = "Wallace";
		 coolChatacter["hobbies"] = "Dancing";
		 console.log(coolCharacter); // {name: "Mia", lastName: "Wallace", hobbies: "Dancing"}
		 console.log(coolCharacter.lastName); // "Dancing"
	 ```
	- Iterating: you can iterate with a ```for...in``` statement
	- ```Object.keys(obj)```: returns an array with all the own enumerable properties names ("keys") of an object
- #### Array: basics
	The JavaScript Array class is a global object that is used in the construction of arrays; which are high-level, list-like objects.
	```js
	// Create an array
		const fruits = ["Apple", "Banana"]
		console.log(fruits.length)	// note that length is a property, not a method
	```
	- Iterating: you can do it with a simple ```for ``` statement, or with a ```for...of```, or with the protoptype method ```forEach()```:
	```js
		for (let i = 0; i < 10; i++)
			console.log(arr[i])

		for (let item of arr)
			consol.log(item)

		arr.forEach((item,index) => {
			console.log(item, index)
		});
	
	```
	- Add item at the end of the array with the ```push()``` method
	```js
		let newfruits = fruits.push('Orange'); // push method add new element and returns the new length of the array
	```
	- Remove the last item from the array with the ```pop()``` method
	```js
		let last = fruits.pop() //returns the element that just removed
	```
	-  See more [Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#instance_methods)
- #### setTimeout, setInterval
	- setTimeout()
		El método setTimeout() del mixin WindowOrWorkerGlobalScope establece un temporizador que ejecuta una función o una porción de código después de que transcurre un tiempo establecido.
		```js
			var timeoutID = setTimeout(function, delay, arg1, arg2);
		```
		- ```function``` a function to be excetuted after the timer expires.
		-```delay``` the time in miliseconds that the timer should wait before the specified function os executed.
		-```arg1, ..., argN``` this are optional, this arguments are passed through to the function specified by function.
	- clearTimeout()
		If you want to stop the function call of the setTimeout, you can use the ```setTimeout()``` method:
		```js
			clearTimeout(timeoutID); // timeoutID is what the setTimeout returns
		```
	- setInterval(): the method repeats a block of code at every given timing event.
		```js
			var intervalID = setInterval(function, delay, arg1, arg2);
		```
	- clearInterval()
		If you want to stop this function call, then you can use the ```clearInterval()``` method
- #### Date and time
	In JavaScript, date and time are represented by the ```Date``` object. The Date object provides the date and time information and also provides various methods. 
	There are 4 ways to create a date object: 
	1. ```new Date()```: creates a date object that shows the current date and time
		```js
			const timeNow = new Date();
			console.log(timeNow); // shows current date and time
		```
		Output
		```js
			Mon Jul 06 2020 12:03:49 GMT+0545 (Nepal Time)
		```
	2. ```new Date(miliseconds)```: the date object contains a number that represents milliseconds since 1 January 1970 UTC. Creates a new date object by adding the milliseconds to the zero time. For example:
		```js
		const time1 = new Date(0);
		console.log(time1); // 1970-01-01T00:00:00.000Z on nodejs
		```
	3. ```new Date(Date string)```: creates a new date object from a date string
		In JavaScript, there are generally three date input formats.
		1. You can create a date object by passing ISO date formats. For example:
		```js
			// ISO Date(International Standard)
			const date = new Date("2020-07-01");

			// the result date will be according to UTC
			console.log(date); // Wed Jul 01 2020 05:45:00 GMT+0545
		```
		2. You can also pass only the year and month or only the year.
		```js
			const date = new Date("2020-07");
			console.log(date); // Wed Jul 01 2020 05:45:00 GMT+0545
			const date1 = new Date("2020");
			console.log(date1); // Wed Jul 01 2020 05:45:00 GMT+0545
		```
		3. You can also pass specific time to ISO dates.
		```js
			const date = new Date("2020-07-01T12:00:00Z");
			console.log(date); // Wed Jul 01 2020 17:45:00 GMT+0545
		```
	4. ```new Date(year, month, day, hours, seconds, miliseconds)```:  creates a new date object by passing specific date and time. The passed argument has a specific order. If four numbers are passed, it represents year, month, day and hours
	```js
		const time1 = new Date(2020, 1, 20, 4, 12, 11, 0);
		console.log(time1); // Thu Feb 20 2020 04:12:11
	```
	_Note_: If you pass only one argument, it is treated as milliseconds. Hence, you have to pass two arguments to use this date format.
	More [methods](https://www.programiz.com/javascript/date-time#methods) of the Data object.
- #### Math
	Math is a built-in object that has properties and methods for mathematical constants and functions. It’s not a function object.
	Unlike many other global objects, Math is not a constructor. All properties and [methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math#static_properties) of Math are static.
	
	_Note_: Many Math functions have a precision that’s implementation-dependent.
	This means that different browsers can give a different result. Even the same JavaScript engine on a different OS or architecture can give different results!
- #### Window
	