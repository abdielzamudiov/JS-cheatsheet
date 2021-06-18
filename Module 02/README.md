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
	Object properties, besides a value they have flags.
	- Enumerable flag defines if the property is enumerable and show up un for ... in loops, unless the property's key is a Symbol. If it’s set to false then it also won’t be picked by Object.assign() or spread operator.
	```js
		var obj = {};
		Object.defineProperty(obj, 'a', {
			value: 1,
			enumerable: true
		});
		
		Object.defineProperty(obj, 'b', {
			value: 2, 
			enumerable: false
		});
		
		for (var i in obj) {
			console.log(i);
		} //'a'
		
		Object.keys(obj); // ['a']
	```
	- Writable flag is to set if a property can be reassigned or not.
	```js
		'use strict'
		var obj = {}; 
		
		Object.defineProperty(obj, 'a', { 
			value: 37,
			writable: false
		});
		
		console.log(obj.a); // 37
		obj.a = 25; // throws a TypeError
	```
	- Configurable flag controls at the same time whether the property can be deleted and whether its attributes(other than value and writable) can be changed.
	```js
		var obj = {};
		
		Object.defineProperty(obj, 'a', {
			get() { return 1; },
			configurable: false
		});
		
		Object.defineProperty(obj, 'a', {
			set() {}
		}); // throws a TypeError (set was undefined previously)
		
		Object.defineProperty(obj, 'a', {
			get() { return 1; }
		}); // throws a TypeError
		
		// (even though the new get does exactly the same thing)
			Object.defineProperty(obj, 'a', {
			value: 12
		}); // throws a TypeError // ('value' can be changed when 'configurable' is false but not in this case due to 'get' accessor)
	```
	All of them are descriptors. They are 2 types of descriptors:
		- Data descriptor.
			Mandatory Properties:
				- value
			Optional properties:
				- configurable
				- enumerable
				- writable
		- Accessor descriptor.
			Mandatory properties:
				- Either ```get``` or ```set``` or both
			Optional properties:
				- configurable
				- enumerable
		
- ### Object static methods
	JavaScript static methods are generally used to create utility functions. The static methods are not called on the instance of class they are made to call directly on the class.
	```js
		class Demo {
			static staticMethod() {
    			console.log("Hi Im a static method");
  			}
		}
		const instanceDemo = new Demo();
		
		Demo.prototype.staticMethod();	//Hi Im a static method
		instanceDemo.staticMethod();	// Throw Error!
	```
	The Object class has static methods that are available in all JS.
	Here are some of them
	```js
		Object.create();	//Creates a new object
		
		Object.defineProperty();	//Adds the named property described by a given descriptor to an object
		
		Object.entries();	// returns an array containing all of the [key, value]
		
		Object.fromEntries();	// returns a new object from an iterable of [key, value] this is the reverse of Object.entries();
		
		Object.keys();	//Returns an array containing the keys
		
		Object.values()	//Returns an array containing the values
	```
- ### Looping through object values
	There are many ways to loop through an object
	```js
		const fruits = {
		  apple: 45,
		  banana: 14,
		  grapes: 34
		}

		//This print the same
		for (let fruit in fruits)
			console.log(fruit + ", " + fruits[fruit]) 

		for (let [fruit, quantity] of Object.entries(fruits))
			console.log(fruit + ", " + quantity)

		//This only can print the values o the keys
		for (let value of Object.values(fruits))
			console.log(value);

		for (let key of Object.keys(fruits))
			console.log(key);
	```
- ### Getters and Setters
	In JavaScript, accessor properties are methods that get or set the value of an object. For that, we use these two keywords:
	- ```get``` - to define a getter method to get the property value
	```js
		const student = {
			firstName: "Monica",
			get getName() {
			return this.firstName;
			}
		};
		
		console.log(student.getName);	//logs "Monica"
		console.log(student.getName());	//Throws Error!
	```
	- ```set``` - to define a setter method to set the property value.
	```js
		const student = {
			firstName: "Monica",

			set setName(newName) {
				return this.firstName = newName;
			}
		}
		
		student.setName = "Mariana";  //{ firstName: 'Mariana', setName: [Setter] }
		student.setName("Mario"); //Throws Error!
	```
- ### Deleting object properties
	In order to delete an object property you must use the ```delete``` keyword.
	```js
		const fruits = {
			apple: 45,
			banana: 14,
			grapes: 34
	  	}
		console.log(fruits.apple);	// logs 45
		delete fruits.apple;
		console.log(fruits.apple);	// logs undefined
	```
- ### Comparing objects
	We can't compare objects with the ```==``` or the ```===```, because of objects are assigned by reference, not by value like primitive values on JS.
	```js
		const str1 = "To compare";
		const str2 = "To compare";

		const obj1 = {name: "Joseph", lastName: "Joestar"};
		const obj2 = {name: "Joseph", lastName: "Joestar"};

		const obj3 = obj1;

		console.log(str1 === str2);	// logs true
		console.log(obj1 === obj2);	// logs false, same keys and values, but different reference

		console.log(obj1 === obj3);	// logs true, same reference
		console.log(obj1.name === obj2.name);	// logs true, because properties are primitive
	```
	But we can compare them in deep by converting them into JSON with ```JSON.stringify()```.
	```js
		const obj1 = {name: "Joseph", lastName: "Joestar"};
		const obj2 = {name: "Joseph", lastName: "Joestar"}
		
		console.log(JSON.stringify(obj1) === JSON.stringify(obj2));	// logs true
		obj2.nickname = "JoJo";
		console.log(JSON.stringify(obj1) === JSON.stringify(obj2));	// logs false
	```
	
	
	