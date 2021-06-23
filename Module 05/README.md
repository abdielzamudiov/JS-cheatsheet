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
	
- #### Recursion
- #### Anonymous functions
- #### Currying, High order functions
- #### Pure functions
- #### Functional programming
- #### Context, global context
- #### this
- #### call/apply/bind
- #### Immutable

