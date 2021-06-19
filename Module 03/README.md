## Module 03:
- ### Block-scopes
    ##### What is Scope?
    Scope determines the visibility or accessibility of a variable or other resource in the area of your code.
	
	A block scope is the area within **if**, **switch** conditions or **for** and **while** loops. Generally speaking, whenever you see **{curly brackets}**, it is a block. In ES6, **const** and **let** keywords allow developers to declare variables in the block scope, which means those variables exist only within the corresponding block.
	Example:
	```js
		function food() {
    		if(true) {
        		var fruit1 = 'apple';        // exist in function scope
        		const fruit2 = 'banana';     // exist in block scope
        		let fruit3 = 'strawberry';   // exist in block scope
    		}
    		console.log(fruit1);
    		console.log(fruit2);
    		console.log(fruit3);
		}
		food();
		// output: apple
		// error: fruit2 is not defined
		// error: fruit3 is not defined
	```
- ### Function default parameters
	It allows you to set default values for your function parameters if no value is passed or if undefined is passed.
	Example:
	```js
		function add(a = 3, b = 5) {
        	return a + b; 
    	}

    	add(4,2); // 6
    	add(4); // 9
    	add(); // 8
	```
	It is **important to note** that parameters are set from **left to right**. So the overwriting of default values will occur based on the position of the your input value when you call the function:
	```js
		function createArray(a = 10, b) {
        	return [a,b]; 
    	}

    	createArray(); // [10, undefined]
    	createArray(5); // [5, undefined]
	```
	You can also set a function as the default parameter:
	```js
 		function createA() {
        	return 10;
    	}

    	function add(a = createA(), b=5) {
        	return a + b; 
    	}

    	add(); // 15
	```
	**Note:** The function cannot be an internal function because the default arguments are evaluated when the function is called. Therefore the following will not work:
	```js
		function add(a = createA(), b = 5) {
        	function createA() {
        		return 10;
        	}
        	return a + b; 
    	}

    	add(); // error: createA is not defined
	```
- ### Function rest parameter
	Is an improved way to handle function parameter, allowing us to more easily handle various input as parameters in a function. The rest parameter syntax allows us to represent an indefinite number of arguments as an array.
	
	**Note:** The rest parameter have to be the **last argument,** as its job is to collect all the remaining arguments into an array.
	```js
		function functionname(...parameters) { //... is the rest parameter
			statement;
		}
	```
	Example:
	```js
		// rest with function and other arguments
		function fun(a,b,...c) {
			console.log(`${a} ${b}`); // output: Mukul Latiyan
			console.log(c); // output: [ 'Lionel', 'Messi', 'Barcelona' ]
			console.log(c[0]); // output: Lionel
			console.log(c.length); // output: 3
			console.log(c.indexOf('Lionel')); // output: 0
		}
		
		fun('Mukul','Latiyan','Lionel','Messi','Barcelona');
	```
- ### Spread operator ```(...)```
	Allows an iterable such as an array expression or string to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected, or an object expression to be expanded in places where zero or more key-value pairs (for object literals) are expected.
	Example:
	```js
		function sum(x, y, z) {
  			return x + y + z;
		}

		const numbers = [1, 2, 3];
		console.log(sum(...numbers)); // output: 6
	```
	1. Spred operator for create an array's copy:
		```js
			let arr = ['a','b','c'];
			let arr2 = [...arr];

			console.log(arr); // output: [ 'a', 'b', 'c' ]
			arr2.push('d'); //inserting an element at the end of arr2
			console.log(arr2); // output: [ 'a', 'b', 'c', 'd' ]
			console.log(arr); // output: [ 'a', 'b', 'c' ]
		```
		By using the spread operator we made sure that the **original array is not affected** whenever we alter the new array.
	2. Expand using spread operator:
		```js
			let arr = ['a','b'];
			let arr2 = [...arr,'c','d'];

			console.log(arr2); // output: [ 'a', 'b', 'c', 'd' ]
		```
- ### String interpolation
	The string interpolation in JavaScript is performed by template literals (strings wrapped in backticks `` ` ``) and `${expression}` as a placeholder. 
	 Example:
	 ```js
		const number = 42;
		const message = `The number is ${number}`;

		console.log(message); // output: 'The number is 42'
	```
	1. You can put any expression inside the placeholder: either an operator, a function call, or even more complex expressions:
		```js
			const n1 = 2;
			const n2 = 3;
			const message1 = `The sum is ${n1 + n2}`; // message1 = 'The sum is 5'

			function sum(num1, num2) {
  				return num1 + num2;
			}
			// message2 = 'The sum is 5'
			const message2 = `The sum is ${sum(n1, n2)}`;
		```
	1. Because the placeholder format `${expression}` has a special meaning in the template literals, you cannot use the sequence of characters `"${someCharacters}"` without escaping.

		A backslash `\` before the placeholder-like sequence of characters `\${abc}` solves the problem:
		```js
			const message = `Some weird characters: \${abc}`;
			console.log(message); // output: 'Some weird characters follow: ${abc}'
		```
	1. Use single quotes `'` rather than backticks `` ` `` in the expressions inside the placeholder:
		```js
			function getLoadingMessage(isLoading) {
  				return `Data is ${isLoading ? 'loading...' : 'done!'}`;
			}
		```
- ### Property shorthand
	New in JavaScript with ES6/ES2015, if you want to define an object who's keys have the same name as the variables passed-in as properties, you can use the shorthand and simply pass the key name.

	Here’s how you can declare an object with the new ES6 / ES2015 syntax:
	```js
		let cat = 'Miaow';
		let dog = 'Woof';
		let bird = 'Peet peet';
		
		let someObject = { cat, dog, bird };
		console.log(someObject);
		// output: {
		// cat: "Miaow",
		// dog: "Woof",
		// bird: "Peet peet"
		// }
	```
	And here’s how to do the same thing with the older ***ES5 syntax***:
	```js
		var cat = 'Miaow';
		var dog = 'Woof';
		var bird = 'Peet peet';
		
		var someObject = {
			cat: cat,
			dog: dog,
			bird: bird
		}
	```
- ### Computed property names
	Allows the names of object properties in JavaScript object literal notation to be determined dynamically, i.e. computed.
	JavaScript objects are really **dictionaries**, so it was always possible to dynamically create a string and use it as a key with the syntax: ```object[‘property’] = value```
	Example 1:
	```js
		const myPropertyName = 'c';
		const myObject = {
			a: 5,
			b: 10,
			[myPropertyName]: 15
		}
		console.log(myObject.c); // output 15
	```
	Example 2:
	```js
		const fieldNumber = 3;
		const myObject = {
			field1: 5,
			field2: 10,
			[`field${fieldNumber}`]: 15
		}
		console.log(myObject.field3); // output 15
	```
- ### Method properties
	A *method* is a function associated with an object, or, put differently, a method is a property of an object that is a function. Methods are defined the way normal functions are defined, except that they have to be assigned as the property of an object. See also [method definitions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Method_definitions) for more details. An example is:
	```js
		objectName.methodname = functionName;
		var myObj = {
  			myMethod: function(params) {
    			// ...do something
  			}
  			// OR THIS WORKS TOO
  			myOtherMethod(params) {
    			// ...do something else
  			}
		};
	```
	Where `objectName` is an existing object, `methodname` is the name you are assigning to the method, and `functionName` is the name of the function.

	You can then call the method in the context of the object as follows:
	```js
		object.methodname(params);
	```
- ### Array matching
	Intuitive and flexible destructuring of Arrays into individual variables during assignment.
	```js
	let list = [ 1, 2, 3 ]; 
	let [ a, , b ] = list;
	
	cosole.log(a); //output: 1
	cosole.log(b); //output: 3
	
	[ b, a ] = [ a, b ]; // swipe values
	cosole.log(a); //output: 3
	cosole.log(b); //output: 1
	```
- ### Destructuring
	The **destructuring assignment** syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.
	Example:
	```js
		let a, b, rest;

		[a, b, ...rest] = [10, 20, 30, 40, 50];
		console.log(rest); // output: [30, 40, 50]
	```
- ### Symbol
	Symbol is a primitive data type of JavaScript, along with [string](https://flaviocopes.com/javascript-string/), [number](https://flaviocopes.com/javascript-number/), boolean, null and undefined.
	It’s a very peculiar data type. Once you create a symbol, its value is kept private and for internal use.
	All that remains after the creation is the symbol reference.
	You create a symbol by calling the `Symbol()` global factory function:
	```js
		const mySymbol = Symbol();
	```
	Every time you invoke `Symbol()` we get a new and unique symbol, guaranteed to be different from all other symbols:
	```js
		Symbol() === Symbol() // false
	```
	You can pass a parameter to `Symbol()`, and that is used as the symbol _description_, useful just for debugging purposes:
	```js
		console.log(Symbol()); // output: Symbol()
		console.log(Symbol('Some Test')); // output: Symbol(Some Test)
	```
	Symbols are often used to identify object properties.
	Often to avoid name clashing between properties, since no symbol is equal to another.
	Or to add properties that the user cannot overwrite, intentionally or without realizing.
	Example:
	```js
		const NAME = Symbol();
		const person = {
  			[NAME]: 'Pepe'
		}

		person[NAME]; // 'Pepe'

		const RUN = Symbol();
		person[RUN] = () => 'Person is running';
		console.log(person[RUN]()); // output: 'Person is running'
	```
	**Note:**
		1. Symbols are not enumerated, which means that they do not get included in a [`for..of` or `for..in` loop](https://flaviocopes.com/javascript-loops/) ran upon an object.
		2. Symbols are not part of the [`Object.keys()`](https://flaviocopes.com/javascript-object-keys/) or [`Object.getOwnPropertyNames()`](https://flaviocopes.com/javascript-object-getownpropertynames/) result.
		3. You can access all the symbols assigned to an object using the [`Object.getOwnPropertySymbols()`](https://flaviocopes.com/javascript-object-getownpropertysymbols/) method.
- ### Map/Set
	Till now, we’ve learned about the following complex data structures:
		-   Objects are used for storing keyed collections.
		-   Arrays are used for storing ordered collections.

	But that’s not enough for real life. That’s why `Map` and `Set` also exist.
	#### Map
     [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) is a collection of keyed data items, just like an `Object`. But the main difference is that `Map` allows keys of any type.
	
	 Methods and properties are:
		-   `new Map()` – creates the map.
		-   `map.set(key, value)` – stores the value by the key.
		-   `map.get(key)` – returns the value by the key, `undefined` if `key` doesn’t exist in map.
		-   `map.has(key)` – returns `true` if the `key` exists, `false` otherwise.
		-   `map.delete(key)` – removes the value by the key.
		-   `map.clear()` – removes everything from the map.
		-   `map.size` – returns the current element count.
	 Example: 
	```js
		let map = new Map();
		map.set('1', 'str1'); // a string key
		map.set(1, 'num1'); // a numeric key
		map.set(true, 'bool1'); // a boolean key
		
		// remember the regular Object? it would convert keys to string
		// Map keeps the type, so these two are different:
		alert( map.get(1) ); // output: 'num1'
		alert( map.get('1') ); // output: 'str1'
		alert( map.size ); // output: 3
	```
	##### Iteration over Map
	For looping over a `map`, there are 3 methods:
		-   `map.keys()` – returns an iterable for keys,
		-   `map.values()` – returns an iterable for values,
		-   `map.entries()` – returns an iterable for entries `[key, value]`, it’s used by default in `for..of`.
	Example:
	```js
		let recipeMap = new Map([
			['cucumber', 500],
			['tomatoes', 350],
			['onion', 50]
		]);
		// iterate over keys (vegetables)
		for (let vegetable of recipeMap.keys()) {
			alert(vegetable); // output: cucumber, tomatoes, onion
		}
		
		// iterate over values (amounts)
		for (let amount of recipeMap.values()) {
			alert(amount); // output: 500, 350, 50
		}
		
		// iterate over [key, value] entries
		for (let entry of recipeMap) { // the same as of recipeMap.entries()
			alert(entry); // output: cucumber,500 (and so on)
		}
	```
	#### Set
	A `Set` is a special type collection – “set of values” (without keys), where each value may occur only once.
	
	Its main methods are:
		-   `new Set(iterable)` – creates the set, and if an `iterable` object is provided (usually an array), copies values from it into the set.
		-   `set.add(value)` – adds a value, returns the set itself.
		-   `set.delete(value)` – removes the value, returns `true` if `value` existed at the moment of the call, otherwise `false`.
		-   `set.has(value)` – returns `true` if the value exists in the set, otherwise `false`.
		-   `set.clear()` – removes everything from the set.
		-   `set.size` – is the elements count.
	The main feature is that repeated calls of `set.add(value)` with the same value don’t do anything. That’s the reason why each value appears in a `Set` only once.

	**For example:** We have visitors coming, and we’d like to remember everyone. But repeated visits should not lead to duplicates. A visitor must be “counted” only once.
	`Set` is just the right thing for that:
	```js
		let set = new Set();
		let john = { name: "John" };
		let pete = { name: "Pete" };
		let mary = { name: "Mary" };
	
		// visits, some users come multiple times
		set.add(john); 
		set.add(pete); 
		set.add(mary); 
		set.add(john); 
		set.add(mary);
	
		// set keeps only unique values 
		alert( set.size ); // output: 3
	
		for (let user of set) { 
			alert(user.name); // output: John (then Pete and Mary) 
		}
	```
	##### Iteration over Set
	We can loop over a set either with `for..of` or using `forEach`:
	```js
		let set = new Set(["oranges", "apples", "bananas"]);
		for (let value of set) alert(value);
	```
	The same methods `Map` has for iterators are also supported:
		-   `set.keys()` – returns an iterable object for values,
		-   `set.values()` – same as `set.keys()`, for compatibility with `Map`,
		-   `set.entries()` – returns an iterable object for entries `[value, value]`, exists for compatibility with `Map`.
- ### Intl object
	The **`Intl`** object is the namespace for the ECMAScript Internationalization API, which provides language sensitive string comparison, number formatting, and date and time formatting. The **`Intl`** object provides access to several constructors as well as functionality common to the internationalization constructors and other language sensitive functions.
	#### Constructor properties
	- [`Intl.Collator()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Collator/Collator) Constructor for collators, which are objects that enable language-sensitive string comparison.
	- [`Intl.DateTimeFormat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat) Constructor for objects that enable language-sensitive date and time formatting.
	- [`Intl.DisplayNames()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DisplayNames/DisplayNames) Constructor for objects that enable the consistent translation of language, region and script display names.
	-	[`Intl.ListFormat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/ListFormat/ListFormat) Constructor for objects that enable language-sensitive list formatting.
	- [`Intl.Locale()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Locale/Locale) Constructor for objects that represents a Unicode locale identifier.
	- [`Intl.NumberFormat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat/NumberFormat) Constructor for objects that enable language-sensitive number formatting.
	- [`Intl.PluralRules()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/PluralRules/PluralRules) Constructor for objects that enable plural-sensitive formatting and language-specific rules for plurals.
	- [`Intl.RelativeTimeFormat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/RelativeTimeFormat/RelativeTimeFormat)Constructor for objects that enable language-sensitive relative time formatting.
	#### Static methods
	- [`Intl.getCanonicalLocales()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/getCanonicalLocales) Returns canonical locale names.
	
	Example:
	```js
		const count = 26254.39;
		const date = new Date("2012-05-24");

		function log(locale) {
  			console.log(`${new Intl.DateTimeFormat(locale).format(date)} ${new Intl.NumberFormat(locale).format(count)}`);
		}

		log("en-US"); // output: 5/24/2012 26,254.39

		log("de-DE"); // output: 24.5.2012 26.254,39
	```
		
	