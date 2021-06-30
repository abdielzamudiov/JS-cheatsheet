### Module 09
- #### `try...catch`
	The `try` statement consists of a `try` block, which contains one or more statements. `{}` must always be used, even for single statements. At least one `catch` block, or a `finally` block, must be present. This gives us three forms for the `try` statement:
	-   `try...catch`
	-   `try...finally`
	-   `try...catch...finally`
	A `catch`-block contains statements that specify what to do if an exception is thrown in the `try`-block. If any statement within the `try`-block (or in a function called from within the `try`-block) throws an exception, control is immediately shifted to the `catch`-block. If no exception is thrown in the `try`-block, the `catch`-block is skipped.
	The `finally`-block will always execute after the  `try` and `catch` block. No matter is an exceptin was caught or thrown.
	```js
		try {
			console.log("hi");
			throw "Exception was thrown"; //Will throw an exception
			console.log("GoodBye"); //And because the exception was founded before this statement
			//This statement will not be executed, instead will redirect to the catch-block
		}
		catch(e){ //specifies an identifier that holds the value of the exception
			//Here goes the statements we want to execute when foan exception is found
			console.log(e);  //Will log "Exception was thrown"
  		}
	```
	Output:
	```
		hi
		Exception was thrown
	```
	Example of `finally`. Finally exectues after try and catch block, regardless of whether a catch block throws a new error, it will be executed. 
	```js
		function handleTry () {
			try {
				console.log("Hi");
				try {
					throw "Eoo";
				}
				catch(e){
					console.log(e,"Inner Exception");
					throw "Exception was thrown";
				}
				finally{
					console.log("finally");
					return; //Will execute de return, bc this is a function, it will end the process
				}
			}
			catch(e){
				console.log(e,"Outer Exception"); 
			}
		}
		handleTry();
	```
	The `return` was executed inside the finally, and because the `return` statement ends a function, the next catch block is not executed. That is why the Outer Exception is not logged.
	Output: 
	```
		Hi
		Eoo Inner Exception
		finally
	```
- #### Custom errors
	In Javascript exists built-in errors that Javascript natively throws, here is the list of those [Errors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors#list_of_errors). Each of these errors are based upon the `Error` object, and has a `name` and a `message`.
	We can extend the Error class and create erros based on the Error class.
	Here is how the Error class should look like. So we can have an idea what we are extending
	```js
		// The "pseudocode" for the built-in Error class defined by JavaScript itself
		class Error{
			constructor(message){
				this.message = message;
				this.name = "Error";	// (different names for different built-in error classes)
				this.stack <call stack>;
			}
		}
	```
	Now let's create our own custom Error inherited from `Error` class.
	```js
		class CustomError extends Error{
			constructor(message){
				super(message);
				this.name = "CustomError";	//this may become tedious
				//this.name = this.constructor.name; would work too
			}
		}
		
		function handleTry () {
			try {
				console.log("Hi");
				throw new CustomError("This error is custom, you can put your error message here");
				console.log("GoodBye");
			}
			catch(e){
				console.log(`${e.name}: ${e.message}`);
			}
		}
		handleTry();
	```
	Output:
	```
		Hi
		CustomError: This error is custom, you can put your error message here
	```
- #### Debugging tools
	Debiggin in browser:
	- Using `console.log()`: You can use the console.log() method to debug the code. You can pass the value you want to check into the console.log() method and verify if the data is correct. Console.log() method opens the value in the debugger window, on the Console tab.
		```js
		const obj = { name: "pepe"};
		obj.name = "Luis";
		obj.lastName = "Peralta";

		console.log(obj);	//use to verify data 
		// { name: 'Luis', lastName: 'Peralta' }
		```
	- Using `debugger` keyword: invokes any available debugging functionality, such as setting a breakpoint. If no debugging functionality is available, this statement has no effect.
	- Setting Breakpoints: You can set breakpoints for the JavaScript code in the debugger window. JavaScript will stop executing at each breakpoint and lets you examine the values. Then, you can resume the execution of code.
- #### Console methods
	There are many methods that can be used to call the console API. Here are a few.
	- `console.assert()`: 
		```js
		// first parameter the assertion, second the message when error.
		console.assert(3 === 4, {number:3,errorMsg: "hahaha error"});
		```
		Output:
		```
		Assertion failed:{number: 3, errorMsg: "hahaha error"}
		```
	- `console.clear()`
		Clear the console.
	-  `console.count()` method logs the number of times that this particular call to `count()` has been called.
		```js
		let user = "";
		function greet() {
			console.count(user);
			return "hi " + user;
		}
		
		user = "bob";
		greet();
		user = "alice";
		greet();
		greet();
		console.count("alice");	
		```
		Output: 
		```
		"bob: 1"
		"alice: 1"
		"alice: 2"
		"alice: 3"
		```
	- The `console.countReset()` method resets counter used with `console.count()`.
		```js
		let user = "";
		function greet() {
			console.count(user);
			return "hi " + user;
		}
		user = "bob";
		greet();
		user = "alice";
		greet();
		greet();
		console.countReset("bob");
		console.count("alice");
		```
		Output:
		```
		"bob: 1"
		"alice: 1"
		"alice: 2"
		"bob: 0"
		"alice: 3"
		```
	-  `console.dir()` method displays an interactive list of the properties of the specified JavaScript object. The output is presented as a hierarchical listing with disclosure triangles that let you see the contents of child objects.
	- `console.error()` outputs an error message to the Web Console.
	- `console.group()` creates a new inline group in the Web Console log. This indents following console messages by an additional level, until console.groupEnd() is called.
	- `console.log()` outputs a message to the web console. The message may be a single string (with optional substitution values), or it may be any one or more JavaScript objects.
	- `console.table()` displays tabular data as a table. It logs data as a table. Each element in the array (or enumerable property if data is an object) will be a row in the table. The first column in the table will be labeled (index). If data is an array, then its values will be the array indices. If data is an object, then its values will be the property names.
	- `console.time()`starts a timer you can use to track how long an operation takes.  When you call console.timeEnd() with the same name, the browser will output the time, in milliseconds, that elapsed since the timer was started.
		```js
		console.time("Start of timer");
		console.timeLog("Start of timer");	//consults the timer without ending it
		console.timeEnd("Start of timer");
		```
		Output:
		```
		Start of timer: 14422.52587890625 ms
		Start of timer: 19178.788818359375 ms
		```
	- `console.trace()` method outputs a stack trace to the Web Console..
		```js
		function foo() {
			function bar() {
				console.trace();
			}
			bar();
		}
		
		foo();
		```
		Output:
		```
		bar
		foo
		<anonymous>
		```
	- `console.warn()` Outputs a warning message to the Web Console.
		```js
		console.warn("OMG a warning");
		```
		Output:
		```
		⚠️ OMG a warning
		```
	
	

  