### Module 08:
- #### Async Javascript
	Normally, a given program's code runs straight along, with only one thing happening at once. If a function relies on the result of another function, it has to wait for the other function to finish and return, and until that happens, the entire program is essentially stopped from the perspective of the user.
	
	JavaScript is traditionally single-threaded. Even with multiple cores, you could only get it to run tasks on a single thread, called the **main thread**.
	To fix such problems, browsers allow us to run certain operations asynchronously. Features like [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) allow you to set an operation running (e.g. the fetching of an image from the server), and then wait until the result has returned before running another operation.
	For reasons illustrated earlier (e.g. related to blocking), many Web API features now use asynchronous code to run, especially those that access or fetch some kind of resource from an external device, such as fetching a file from the network, accessing a database and returning data from it, accessing a video stream from a web cam, or broadcasting the display to a VR headset.
	
	There are two main types of asynchronous code style you'll come across in JavaScript code, `old-style callbacks` and `newer promise-style code`.
- #### Callback hell
	This is a big issue caused by coding with complex nested callbacks. Here, each and every callback takes an argument that is a result of the previous callbacks. In this manner, The code structure looks like a pyramid, making it difficult to read and maintain. Also, if there is an error in one function, then all other functions get affected. 
	Example:   
	```js
		firstFunction(args, function() {
  			secondFunction(args, function() {
    			thirdFunction(args, function() {
      				// And so on…
    			});
 	 		});
		});
	```
	##### **How to escape from a callback hell?**
	1. JavaScript provides an easy way of escaping from a callback hell. This is done by event queue and promises.
	2. Promises use .then() method to call async callbacks. We can chain as many callbacks as we want and the order is also strictly maintained.
	3. Promises use .fetch() method to fetch an object from the network. It also uses .catch() method to catch any exception when any block fails.
	4. So these promises are put in event queue so that they don’t block subsequent JS code. Also once the results are returned, the event queue finishes its operations.
	5. There are also other helpful keywords and methods like *async*, *wait*, *settimeout()* to simplify and make better use of callbacks.
- #### Promises
	Promises are the new style of async code that you'll see used in modern Web APIs. A good example is the `[fetch()](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch)` API, which is basically like a modern, more efficient version of [`XMLHttpRequest`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest). Let's look at a quick example, from our [Fetching data from the server](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Fetching_data) article:
	```js
		fetch('products.json').then(function(response) {
  			return response.json();
		}).then(function(json) {
  			let products = json;
  			initialize(products);
		}).catch(function(err) {
  			console.log('Fetch problem: ' + err.message);
		});
	```
	Here we see `fetch``()` taking a single parameter — the URL of a resource you want to fetch from the network — and returning a [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). The promise is an object representing the completion or failure of the async operation. It represents an intermediate state, as it were. In essence, it's the browser's way of saying "I promise to get back to you with the answer as soon as I can," hence the name "promise."
	
	We've then got three further code blocks chained onto the end of the `fetch()`:
	-   Two `[then()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)` blocks. Both contain a callback function that will run if the previous operation is successful, and each callback receives as input the result of the previous successful operation, so you can go forward and do something else to it. Each `.then()` block returns another promise, meaning that you can chain multiple `.then()` blocks onto each other, so multiple asynchronous operations can be made to run in order, one after another.
	-   The `[catch()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)` block at the end runs if any of the `.then()` blocks fail — in a similar way to synchronous `[try...catch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch)` blocks, an error object is made available inside the `catch()`, which can be used to report the kind of error that has occurred. Note however that synchronous `try...catch` won't work with promises, although it will work with [async/await](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await), as you'll learn later on.   
	
	Example:    
	```js
		console.log ('Starting');
		let image;

		fetch('coffee.jpg').then((response) => {
  			console.log('fetch 1');
  			return response.blob();
		}).then((myBlob) => {
			console.log('fetch 2');
  			let objectURL = URL.createObjectURL(myBlob);
  			image = document.createElement('img');
  			image.src = objectURL;
  			document.body.appendChild(image);
		}).catch((error) => {
  			console.log('There has been a problem with your fetch operation: ' + error.message);
		});

		console.log ('All done!');
	```
	So the messages have appeared in a different order to what you might expect:
	-   Starting
	-   All done!
	-   fetch 1
	-   fetch 2
- #### Async await
	##### Async
	First of all we have the `async` keyword, which you put in front of a function declaration to turn it into an [async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function). An async function is a function that knows how to expect the possibility of the `await` keyword being used to invoke asynchronous code.   
	Example:
	```js
		async function hello() { return "Hello" };
		hello();
	```
	Invoking the function now returns a promise. This is one of the traits of async functions — their return values are guaranteed to be converted to promises.
	You can also create an [async function expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/async_function), like so:
	```js
		let hello = async function() { return "Hello" };
		hello();
	```
	And you can use arrow functions:
	```js
		let hello = async () => { return "Hello" };
	```
	To actually consume the value returned when the promise fulfills, since it is returning a promise, we could use a `.then()` block:
	```js
		hello().then((value) => console.log(value))
	```
	or even just shorthand such as
	```js
		hello().then(console.log)
	```
	##### Await
	The advantage of an async function only becomes apparent when you combine it with the [await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await) keyword. `await` only works inside async functions within regular JavaScript code, however it can be used on its own with [JavaScript modules.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)
	`await` can be put in front of any async promise-based function to pause your code on that line until the promise fulfills, then return the resulting value.
	
	You can use `await` when calling any function that returns a Promise, including web API functions.   
	Example 1:   
	```js
		async function hello() {
  			return greeting = await Promise.resolve("Hello");
		};

		hello().then(alert);
	```
	
	Example 2:   
	```js
		async function f() { 
			let promise = new Promise((resolve, reject) => { 
				setTimeout(() => resolve("done!"), 1000) 
			}); 
			
			let result = await promise; // wait until the promise resolves (*) 		
			alert(result); // "done!" 
		} 
			
		f();
	```
	The function execution “pauses” at the line `(*)` and resumes when the promise settles, with `result` becoming its result. So the code above shows “done!” in one second.
	Let’s emphasize: `await` literally suspends the function execution until the promise settles, and then resumes it with the promise result. That doesn’t cost any CPU resources, because the JavaScript engine can do other jobs in the meantime: execute other scripts, handle events, etc.

	It’s just a more elegant syntax of getting the promise result than `promise.then`. And, it’s easier to read and write.
- #### Promise static methods
	There are 6 static methods of `Promise` class:

	1.  `Promise.all(promises)` – waits for all promises to resolve and returns an array of their results. If any of the given promises rejects, it becomes the error of `Promise.all`, and all other results are ignored.
	2.  `Promise.allSettled(promises)` (recently added method) – waits for all promises to settle and returns their results as an array of objects with:
		-   `status`: `"fulfilled"` or `"rejected"`
		-   `value` (if fulfilled) or `reason` (if rejected).
	3.  `Promise.race(promises)` – waits for the first promise to settle, and its result/error becomes the outcome.
	4.  `Promise.any(promises)` (recently added method) – waits for the first promise to fulfill, and its result becomes the outcome. If all of the given promises are rejected, [`AggregateError`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/AggregateError) becomes the error of `Promise.any`.
	5.  `Promise.resolve(value)` – makes a resolved promise with the given value.
	6.  `Promise.reject(error)` – makes a rejected promise with the given error.

	Of all these, `Promise.all` is probably the most common in practice.
- #### Handing error in Promises, async await
	If a promise resolves normally, then `await promise` returns the result. But in the case of a rejection, it throws the error, just as if there were a `throw` statement at that line.

	This code:
	```js
		async function f() { 
			await Promise.reject(new Error("Whoops!"));
		}
	```
	…is the same as this:
	```js
		async function f() { 
			throw new Error("Whoops!"); 
		}
	```
	In real situations, the promise may take some time before it rejects. In that case there will be a delay before `await` throws an error.

	We can catch that error using `try..catch`, the same way as a regular `throw`:
	```js
		async function f() { 
		
			try { 
				let response = await fetch('http://no-such-url'); 
				let user = await response.json();
			} 
			catch(err) { 
				// catches errors both in fetch and response.json
				alert(err); // TypeError: failed to fetch 
			} 
		} 
			
		f();
	```
	If we don’t have `try..catch`, then the promise generated by the call of the async function `f()` becomes rejected. We can append `.catch` to handle it:
	```js
		async function f() { 
			let response = await fetch('http://no-such-url'); 
		} 
		
		// f() becomes a rejected promise 
		f().catch(alert); // TypeError: failed to fetch // (*)
	```
	If we forget to add `.catch` there, then we get an unhandled promise error (viewable in the console). We can catch such errors using a global `unhandledrejection` event handler as described in the chapter [Error handling with promises](https://javascript.info/promise-error-handling).
- #### Event Loop
	JavaScript has a concurrency model based on an **event loop**, which is responsible for executing the code, collecting and processing events, and executing queued sub-tasks. This model is quite different from models in other languages like C and Java.
	Browser JavaScript execution flow, as well as in Node.js, is based on an _event loop_.

	Understanding how event loop works is important for optimizations, and sometimes for the right architecture.
	The _event loop_ concept is very simple. There’s an endless loop, where the JavaScript engine waits for tasks, executes them and then sleeps, waiting for more tasks.

	A more detailed event loop algorithm (though still simplified compared to the [specification](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop-processing-model)):
	1.  Dequeue and run the oldest task from the _macrotask_ queue (e.g. “script”).
	2.  Execute all _microtasks_:
    	-   While the microtask queue is not empty:
        -   Dequeue and run the oldest microtask.
	3.  Render changes if any.
	4.  If the macrotask queue is empty, wait till a macrotask appears.
	5.  Go to step 1.

	Examples of tasks:
	-   When an external script `<script src="...">` loads, the task is to execute it.
	-   When a user moves their mouse, the task is to dispatch `mousemove` event and execute handlers.
	-   When the time is due for a scheduled `setTimeout`, the task is to run its callback.
	-   …and so on.

	Tasks are set – the engine handles them – then waits for more tasks (while sleeping and consuming close to zero CPU).
	It may happen that a task comes while the engine is busy, then it’s enqueued.
	
	To schedule a new _macrotask_:
	-   Use zero delayed `setTimeout(f)`.

	That may be used to split a big calculation-heavy task into pieces, for the browser to be able to react to user events and show progress between them.

	Also, used in event handlers to schedule an action after the event is fully handled (bubbling done).

	To schedule a new _microtask_
	-   Use `queueMicrotask(f)`.
	-   Also promise handlers go through the microtask queue.

	There’s no UI or network event handling between microtasks: they run immediately one after another.

	So one may want to `queueMicrotask` to execute a function asynchronously, but within the environment state.
- #### Stack, Heap, Queue
	So, How JavaScript simulate like it’s running our commands in a multi-thread environment? To answer this question let’s deep into how JavaScript environment.
	Although JavaScript is a single thread language, we have a strong helper which is browser that has ability to manage complex operations.
	Let’s dig into some details of each part.
	
	##### Stack
	Stacks holds our function calls. On each new function call, it’s pushed on top of the stack. You can see your stack when you have an exception on JavaScript by stack trace.
	
	##### Heap
	Heap is the place (memory) where objects are stored when we define variables.
	
	##### Callback Queue
	When a process finished its job, such as a xhr call, it’s dropped in a callback queue. Callback queue is triggered by event loop process after our stack is empty which means the process waits in that queue until our stack is empty. Once our stack has no function call, then a process is popped-out from callback queue and pushed in to stack.
	
	##### Web API
	Browsers have defined API’s which developers can be used to make complex processes such as to get location of visitor, GeoLocation is defined.
	
	##### Event Loop
	A process which is responsible to check our stack and then trigger our callback queue continuously.
	