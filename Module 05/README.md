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
- #### Self-invoked functions
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

