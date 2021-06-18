## Module 02:
- ### Creating an array
	1. Using the array literals
	```js
		const arr = [];
		const arr2 = [1, 2, 3, 4, 5];
	```
	2. Using the array constructor ```Array()```
	```js
		const arr = new Array(5); // will create a 5 slot empty array
		const arr1 = new Array(1,2,3,4) // [1, 2, 3, 4]
		
	```
	3. Using ```Array.of``` it is similar to array constructor, except that when passing only one number doesn't represent the length.
	```js
		const array = Array.of(5); // [5]
	```
	4. Using ```Array.from()```: static method creates a new, shallow-copied Array instance from an array-like or iterable object.
	```js
		console.log(Array.from('foo'));
		// expected output: Array ["f", "o", "o"]
	```
- ### Creating an object
	1. With object literals.
	```js
		const object_name = {
			key1: value1,
			key2: value2
		}
	```
	2. With the object constructor ```Object()```
	```js
		let o = new Object()
		o.foo = 42 // {foo: 42}
		
		const obj = new Object("eo") //creates a String object
		const obj1 = new Object(123) //creates a Number object
	```
	3. With ```Object.create()``` method: creates a new object, using an existing object as the prototype of the newly created object.
	```js
		Object.create(proto) //proto is the object wich should be the prototype of the new object
		Object.create(proto, propertiesObject) //specify property descriptors to be added to the newly-created object
	```
- ### Array methods
	Every instance of an array has access to methods from the Array.prototype. Here we are going to see the most used methods of an array. For more [methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#instance_methods)
	- ```push()``` method: it adds an element at the end of the array and returns the new length of the array
	```js
		let arr = [1, 2, 3];
		console.log(arr.push(4)); // log 4 which is the new length
		console.log(arr); // logs [1, 2, 3, 4]
	```
	- ```pop()``` method: removes the last element of the array and returns the removed element
	```js
		const arr = ['a', 'b', 'c'];
		console.log(arr.pop());	// log c
		console.log(arr) // logs ['a', 'b']
	```
	- ```shift()``` method: removes the first element of an array and returns the removed element
	```js
		const arr = [1, 2, 3, 4];
		console.log(arr.shift());	//logs 1
		console.log(arr);	//logs [2, 3, 4]
	```
	- ```unshift()``` method: adds an element at the beginning of the array and returns the new length of the array.
	```js
		const arr = ['b', 'c'];
		console.log(arr.unshift('a'))	//logs 3
		console.log(arr)	//logs [1, 2, 3]
	```
- ### Sorting arrays
	JS has an Array.prototype method ```sort()```  to sort arrays. This method sorts the array and returns a new array sorted. It can recieve a compare function as a parameter.
	```js
		let arr = [8,3,1,6];
		let arrSorted = [...arr].sort(); // [1,3,6,8]
		
		arr = [123,89,9,0,11111];
		arrSorted = [...arr].sort(); // [0, 11111, 123, 89, 9]
	```
	The default sort() method converts elements into strings and sort them according to the UTF-16 code units values. If you dont need the default behavior you can use a copare function.
	```js
		arr = [123,89,9,0,11111];
		
		sort(compareFunction); 
		
		arrSorted = [...arr].sort((firstElement, secondElement) => { ... }); 
		
		arrSorted = [...arr].sort((a, b) => a - b ); // [0, 9, 89, 123, 11111]
	```
	- ```firstElement```: the first element of comparision.
	- ```secondElement```: the second element of comparision.
	- ```compareFunction```: defines de sort order. If is supplied all non-```undefined``` array elements are sorted according to the return value of the compare function (all undefined are sorted at the end of the array).
	We can sort an array however we want.
	- If compareFunction(a, b) returns a value > than 0, sort b before a.
	- If compareFunction(a, b) returns a value ≤ 0, leave a and b in the same order.
- ### Object methods
	There are static methods, and Instance methods, and also you can add your own methods.
	```js
		const socks = {
			mine: 3,
			yesi: 5,
			countSocks: function() {
				return this.mine + this.yesi
			}
		};
		//static methods
		const entries = Object.entries(socks); //entries = [["mine",3],["yesi",5]]
		
		//instance methods from prototype
		const string = socks.toString();	// string = "[object Object]"
		
		//define your own methods
		const allSocks = socks.countSocks();	// allSocks = 8
	```
	For all the methods available checkout [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object#static_methods)
- ### Object to primitive conversion
	You can convert an object to a primitive value by using methods from the prototype 	object, this methods must be overrided in order to convert it in whatever you want.
	```js
		const socks = {
			mine: 3,
			yesi: 5
		};
		//By default the methods behave like this
		const string = socks.toString();	// string = "[object Object]"
		const number = socks.valueOf();		// number = {mine: 3, yesi: 5}
		
		//Overriding the method
		socks.__proto__.valueOf = function () { return this.mine + this.yesi }
		socks.__proto__.toString = function () { 
			return "I have " + this.mine + ' ' + "Yesi has " + this.yesi 
		}
		
		console.log(socks.valueOf());	//logs 8
		console.log(socks + 2)	// logs 10
		console.log(socks.toString());	//logs "I have 3 Yesi has 5"
		
		
		function MyNumberType(n) {
			this.number = n;
		}
		
		MyNumberType.prototype.valueOf = function() {
			return this.number;
		};
		
		MyNumberType.prototype.toString = function() {
			return this.number + '';
		};
		
		var myObj = new MyNumberType(4);
		myObj + 3; // 7
		myObj.toString();	//"4"
	```
- ### Object property flags and descriptors
	
- ### Object static methods
- ### Looping through object values
- ### Getters and Setters
- ### Deleting object properties
- ### Comparing objects