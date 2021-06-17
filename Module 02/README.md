## Module 02:
- ### Creating an array
	1. Using the assignment operator ```=```
	```js
		const arr = [];
		const arr2 = [1, 2, 3, 4, 5];
	```
	2. Using the array constructor ```Array()```
	```js
		const arr = new Array(5); // will create a 5 slot empty array
		const arr1 = new Array(1,2,3,4) // [1, 2, 3, 4]
		
		// you can also skip then new operator
		const arr2 = Array(5); // will create a 5 slot empty array
		const arr3 = Array(1,2,3,4) // [1, 2, 3, 4]
	```
	3. Using ```Array.of``` it is similar to array constructor, except that when passing only one number doesn't represent the length.
	```js
		const array = Array.of(5); // [5]
	```
	4. Using ```Array.from()```: static method creates a new, shallow-copied Array instance from an array-like or iterable object.
	```
		console.log(Array.from('foo'));
		// expected output: Array ["f", "o", "o"]
	```
- ### Creating an object
	
- ### Array methods
- ### Sorting arrays
- ### Object methods
- ### Object to primitive conversion
- ### Object property flags and descriptors
- ### Object static methods
- ### Looping through object values
- ### Getters and Setters
- ### Deleting object properties
- ### Comparing objects