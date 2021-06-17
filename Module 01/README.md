## Module 01:
- #### How to run JS
	1. Command line: with nodejs
	```
	node index.js
	```
	2. From the browser: Create a HTML file that references to JS script.
	```
	<html>
    	<head>
        	<script defer src="./index.js"></script>
    	</head>
	</html>
	```
	3. From the Browser console: ```ctrl+shift+J```
- #### JS syntax
	1. Variable Asignment:
	```
		//Variable asignment
		var x,y,z;
		x = 7; y = y;
		z = x + y;
	```
	2. Literals:
	```
		//Two most important syntax rules for fixed values are
		10.50 //Numbers type can be with decimal
		12938 //Numbers type can be without decimal
		"Strings can be double quote"
		'or can be single quote'
	```
	3. Operators:
	```
		//Asignment operator
		var x = 4 * 5;
		
		//Arithmetic operators "( + - * / )" (just like algebra)
		(5 + 6) * 10
	```
	4. Expresions: an expression is a combination of values, variables, and operators, which computes to a value.
	```
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
		```
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
		```
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
		```
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
		```
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
		```
		// Example
		for (i = 0; i < 10; i++){
			doStuff();
			if (eo)
				break;
			console.log("if break is executed, this won´t appear and the loop is terminated");
		}
		```
		- ```continue``` statement: can be used to skip to the next iteration.
		```
		// Example
		for (i = 0; i < 10; i++){
			doStuff();
			if (eo)
				continue;
			console.log("if break is executed, this won´t appear only in the iteration that 'continue' was called, it won't end the loop like 'break' does");
		}
		```
		- ```for...in``` statement: iterates a specified variable over all de properties of an **object**. supports (continue, break). It iterates over property names.
		```
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
		```
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
	```
	alert(message) // only parameter is message, it is of string type
	```
		
	2. Console: is an object that provides access to the browser's debugging console, it has a lot of [methods](https://developer.mozilla.org/en-US/docs/Web/API/console#methods). Most used methods are [```console.log()```](https://developer.mozilla.org/en-US/docs/Web/API/Console/log), [```console.info()```](https://developer.mozilla.org/en-US/docs/Web/API/Console/info), [```console.warn()```](https://developer.mozilla.org/en-US/docs/Web/API/Console/warn), [```console.error()```](https://developer.mozilla.org/en-US/docs/Web/API/Console/error)
	```
	console.log("here goes whatever you wanna log in the console");
	```
- #### Variables
	In JS we use ```var``` or ```let``` keyword to declare variables.
	```
	let x;
	var y;
	```
	We use the assignment operator ```=``` to assign a value to a variable.
	```
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
	```
	const x = 5; //initialize when declaration, otherwise will throw error
	```
- #### Data types, typeof
	-```String``` : represents textual data
	```
	"hello"
	'hello world'
	```
	- ```Number```: an integer or a floating number. Represents numeber less than (2^53 -1) and more dan -(2^53 -1)
	```
	3
	3.1416
	3e-2
	+Infinity
	-Infinity
	NaN
	```
	- ```BigInt```: an integer with arbitrary precision. Is created by appending n to the end of an integer. Can store a larger number tan ```Number```. BigInt and Number cannot be added.
	```
	const value = 900719925124740999n
	const result2 = value + 1 ///this will throw error
	
	```
	- ```Boolean```: Any of two values: ```true``` or ```false```
	- ```undefined```: a data type whose variable is not initialized. It can also be explicitly assigned, but is recommended to assign null instead of undefined to an unknown or empty variable.
	- ```null```: denotes a ```null``` value.
	- ```Symbol```:  data type whose instances are unique and inmutable. 
	```
	let value1 = Symbol('hello');
	let value2 = Symbol('hello');
	value1 === value2 //this evaluate to false 
	```
	- ```Object```: key-value pairs of collection of data.
	```
	let student = {
		firstName: "Juan",
		lastName: null,
		class: 10
	};
	```
	**typeof**
	To find the type of a variable, you can use the ```typeof``` operator.
	```
	const name = "ram";
	typeof(name); // returns "string"
	```
- #### Functions: basics
	- Declaring a function:
		- A function is declared using the function keyword.
		- Naming a function is similar to name a variable. You should write descriptive names for your functions.
		- The body of the function is written within ```{}```
	```
	function nameOfFunction () {
    	// function body   
	}
	```
	- Calling a Function: we can call a function by writing the name followed by parentheses.
	```
	function hello(){
		console.log("hello")
	}
	hello() // calling the function hello
	```
	- Functions Parameters: a function can also be declared with parameters. A parameter is a value that is passed when declaring a function.
	```
	function hello(parameter){
		console.log(parameter) 
	}
	hello("hello world") // calling the function hello
	```
- #### Returning value from a function
- #### Types convertions
- #### Comparisons
- #### Operators: Logical, Conditional
- #### Objects: basics
- #### Array: basics
- #### setTimeout, setInterval
- #### Date and time
- #### Math
- #### Window