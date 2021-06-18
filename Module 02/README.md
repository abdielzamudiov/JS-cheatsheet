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
	
- ### Object methods
- ### Object to primitive conversion
- ### Object property flags and descriptors
- ### Object static methods
- ### Looping through object values
- ### Getters and Setters
- ### Deleting object properties
- ### Comparing objects