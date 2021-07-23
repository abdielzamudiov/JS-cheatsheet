### Creational patterns
Provide object creation mechanisms that increase flexibility and reuse of existing code.
Are geneal solutions to common object-oriented problems.

1. Factory method: Provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.
2. Abstract factory: Lets you produce families or related objects without specifying their concrete classes.
3. Builder: Lets you construct complex objects step by step. The pattern allows you to produce different types and representation of an object using the same construction code.
4. Prototype: Lets you copy existing objects without making your code dependent on their classes.
5. Singleton: Lets you ensure that a class has only one instance, while providing a global access point to this instance.

### Structural patterns
Explain how to assemble objects and classes into larger structures, while keeping the structures flexible and efficient.
1. Adapter: Allow objects with incompatible interfaces to collaborate.
2. Bridge: Lets you split a large class or a set of closely related classes into two sepatate hierarchies - abstraction and implementation - which can be developed independently of each other.
3. Composite: Lets you compose objects into tree structures and then work with these structures as if they were individual objects.
4. Decorator: Lets you attach new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors.
5. Facade: Provides a simplified interface to a library, a framework, or any other complex set of classes.
6. Flyweight: Lest you fit more objects into the available amount of RAM by sharing common parts of state between multiple objects instead of keeping all of the data in each object.
7. Proxy: Lets you provide a substitude or placeholder for another object. A proxy controls access to the original object, allowing you to perform something either before or after the request gets through to the original object.

### Behavioral patterns
Take care of the effective communication and the assigment of responsabilities between objects.
1. Chain of responsability: Lets you pass requests along a chain of handlers. Upon receiving a request, each handler decides either to process the request or to pass it to the next handler in the chain.
2. Command: Turns a request into a stand-alone object that contains all information about the request. This transformation lets you pass request as a method arguments, delay or queue a request's execution, and support undoable operations.
3. Iterator: Lets you traverse elements of a collection without exposing its underlying representation (list, stack, tree, etc.).
4. Mediator: Lets you reduce chaotic dependencies between objects. The patern restricts direct communications between the object and forces them to collaborate only via a mediator object.
5. Memento: Lets you save and restore the previous state of an object without revealing the details of its implementation.
6. Observer: Lets you define a subscription mechanism to notify multiple objects about   
	any events that happen to the object they're observing.
7. State: Lets an object alter its behavior when its internal state changes. It appears as if the object changed its class.
8. Strategy: Lets you define a family of algorithms, put each of them into a separate class, and make their objects interchangeable.
9. Template method: Defines the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure.
10. Visitor: Lets you separate algorithms from the objects on wich they operate. 
	
Erich Gamma, John Vlissides, Ralph Johnson, and Richard Helm. In 1994, they published Design Patterns: Elements of Reusable Object-Oriented Software.

### AntiPatterns
AntiPatterns highlight the most common problems that face the software industry and provide the tools to enable you to recognize these problems and to determine their underlying causes.
There are three diferent categories:
-	[Software Development AntiPatterns (sourcemaking.com)](https://sourcemaking.com/antipatterns/software-development-antipatterns)
	1. [The Blob](https://sourcemaking.com/antipatterns/the-blob)
	2. [Continuous Obsolescence](https://sourcemaking.com/antipatterns/continuous-obsolescence)
	3. [Lava Flow](https://sourcemaking.com/antipatterns/lava-flow)
	4. [Ambiguous Viewpoint](https://sourcemaking.com/antipatterns/ambiguous-viewpoint)
	5. [Functional Decomposition](https://sourcemaking.com/antipatterns/functional-decomposition)
	6. [Poltergeists](https://sourcemaking.com/antipatterns/poltergeists)
	7. [Boat Anchor](https://sourcemaking.com/antipatterns/boat-anchor)
	8. [Golden Hammer](https://sourcemaking.com/antipatterns/golden-hammer)
	9. [Dead End](https://sourcemaking.com/antipatterns/dead-end)
	10. [Spaghetti Code](https://sourcemaking.com/antipatterns/spaghetti-code)
	11. [Input Kludge](https://sourcemaking.com/antipatterns/input-kludge)
	12. [Walking through a Minefield](https://sourcemaking.com/antipatterns/walking-through-minefield)
	13. [Cut-and-Paste Programming](https://sourcemaking.com/antipatterns/cut-and-paste-programming)
	14. [Mushroom Management](https://sourcemaking.com/antipatterns/mushroom-management)

-	[Software Architecture AntiPatterns (sourcemaking.com)](https://sourcemaking.com/antipatterns/software-architecture-antipatterns)
-	[Project Management AntiPatterns (sourcemaking.com)](https://sourcemaking.com/antipatterns/software-project-management-antipatterns)

### Singleton - Creational
The Singleton pattern solves two problems at the same time, violating the Single Responsibility Principle:
1. Ensure that a class has just a single instance. Why would anyone want to control how many instances a class has? The most common reason for this is to control access to some shared resource—for example, a database or a file.
2. Provide a global access point to that instance. Just like a global variable, the Singleton pattern lets you access some object from anywhere in the program. However, it also protects that instance from being overwritten by other code.

All implementations of the Singleton have these two steps in common:
- Make the default constructor private, to prevent other objects from using the new operator with the Singleton class. 
- Create a static creation method that acts as a constructor. Under the hood, this method calls the private constructor to create an object and saves it in a static field. All following calls to this method return the cached object.
           
### Factory - Creational
The Factory Method pattern suggests that you replace direct object construction calls (using the new operator) with calls to a special factory method. Don’t worry: the objects are still created via the new operator, but it’s being called from within the factory method. Objects returned by a factory method are often referred to as products.

Use the Factory Method when you don’t know beforehand the exact types and dependencies of the objects your code should work with.

Use the Factory Method when you want to save system resources by reusing existing objects instead of rebuilding them each time.

Therefore, you need to have a regular method capable of creating new objects as well as reusing existing ones. That sounds very much like a factory method.

### Facade - Structural
A facade is a class that provides a simple interface to a complex subsystem which contains lots of moving parts. A facade might provide limited functionality in comparison to working with the subsystem directly. However, it includes only those features that clients really care about.

Having a facade is handy when you need to integrate your app with a sophisticated library that has dozens of features, but you just need a tiny bit of its functionality

Use the Facade when you want to structure a subsystem into layers.

### Modules definitions overview
#### Named exports
It has therefore made sense in recent years to start thinking about providing mechanisms for splitting JavaScript programs up into separate modules that can be imported when needed. Node.js has had this ability for a long time, and there are a number of JavaScript libraries and frameworks that enable module usage (for example, other [CommonJS](https://en.wikipedia.org/wiki/CommonJS) and [AMD](https://github.com/amdjs/amdjs-api/blob/master/AMD.md)-based module systems like [RequireJS](https://requirejs.org/), and more recently [Webpack](https://webpack.github.io/) and [Babel](https://babeljs.io/)).

The good news is that modern browsers have started to support module functionality natively, and this is what this article is all about. This can only be a good thing — browsers can optimize loading of modules, making it more efficient than having to use a library and do all of that extra client-side processing and extra round trips.   

Exporting:   
```js
	export const name = 'square';

	export function draw(ctx, length, x, y, color) {
  		ctx.fillStyle = color;
  		ctx.fillRect(x, y, length, length);

  		return {
    			length: length,
    			x: x,
    			y: y,
    			color: color
  		};
	}
```
You can export functions, `var`, `let`, `const`, and — as we'll see later — classes. They need to be top-level items; you can't use `export` inside a function, for example.

Importing:   
```js
	import { name, draw, reportArea, reportPerimeter } from './modules/square.js';
```
However, we've written the path a bit differently — we are using the dot (`.`) syntax to mean "the current location", followed by the path beyond that to the file we are trying to find.

#### Applying the module to your HTML
First of all, you need to include `type="module"` in the [`<script>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script "The HTML <script> element is used to embed or reference executable code; this is typically used to embed or refer to JavaScript code.") element, to declare this script as a module. To import the `main.js` script, we use this:
```html
	<script type="module" src="main.js"></script>
```

You can also embed the module's script directly into the HTML file by placing the JavaScript code within the body of the `<script>` element:
```html
	<script type="module">
  		/* JavaScript module code here */
		import {func1} from 'my-lib';
		func1();
	</script>
```
The script into which you import the module features basically acts as the top-level module. If you omit it, Firefox for example gives you an error of "SyntaxError: import declarations may only appear at top level of a module".

You can only use `import` and `export` statements inside modules, not regular scripts.

### UMD, AMD, CommonJS
#### CommonJS (CJS)
This is one of the first format created. I'm pretty sure you've already used it. It's the module system that initially inspired NodeJS.

This system relies on importing and exporting modules thanks to some well-known keywords: `require` and `exports`. The `module.exports` object is really specific to NodeJS.
```js
	// utils.js
  	// we create a function 
  	function add(r) {
    		return r + r;
  	}
  	// export (expose) add to other modules
  	exports.add = add;


  	// index.js
  	var utils = require('./utils.js');
  	utils.add(4); // = 8
```
The commonJS team created this API as a **synchronous** one which is not that good for browsers... Moreover, **Commonjs isn't natively understood by browsers**; it requires either a loader library or some transpiling.

#### Asynchronous Module Definition (AMD)
AMD is some kind of a split of CommonJS. It has been created by members of the CJS team that disagreed with the direction taken by the rest of the team.

They've decided to create AMD to support **asynchronous** module loading. This is the module system used by [RequireJS](https://requirejs.org/) and that is working client-side (in browsers).
```js
	// add.js
  	define(function() {
    		return add = function(r) {
      			return r + r;
    		}
  	});


  	// index.js
  	define(function(require) {
    		require('./add');
    		add(4); // = 8
  	}
```
This example works only if you have requirejs on your website. You can find some other [AMD examples](https://clubmate.fi/requirejs-from-scratch-and-the-amd-module-patterns/).

#### Universal Module Definition (UMD)
As you may have understood those 2 formats are unfortunately mutually unintelligible to each other. This is why the [UMD](https://github.com/umdjs/umd) has been created. It is based on AMD but with some special cases included to handle CommonJS compatibility.

Unfortunately, this compatibility adds some complexity that makes it complicated to read / write. If you want, you can find multiple templates of UMD code on this [github](https://github.com/umdjs/umd/tree/master/templates) repository.

#### ES2015 Modules (ESM)
As those 3 formats are not that easy to read, hard to analyze for static code analyzer and not supported everywhere, The ECMA team (the team behind the standardization of Javascript) decided to create the ECMAScript 2015 (also known as ES6) standard. This format is really simple to read and write and supports both synchronous and asynchronous modes of operation.
```js
 	// add.js
  	export function add(r) {
    		return r + r;
  	}


  	// index.js
  	import add from "./add";
  	add(4); // = 8
```
Moreover, es modules can be statically analyze which allow build tools (like Webpack or Rollup) to perform tree-shaking on the code. Tree-shaking is a process that removes unused code from bundles.

Unfortunately, this format still have 2 cons (but they're improving):

-   ESM doesn't supports dynamically imported modules but there is a [proposal](https://github.com/tc39/proposal-dynamic-import) for months now that has started to be implemented on some [browsers](https://caniuse.com/#feat=es6-module-dynamic-import).
-   It [isn't supported](https://caniuse.com/#feat=es6-module) on all the browsers but fortunately, this can be "fixed" thanks to... transpiling!

#### Transpiling
Transpiling is the process of translating one language or version of a language to another. So here, the idea is to transpile ES6 to ES5 to get a better browser support. Unfortunately, this transpilation has a cost as it adds some extra code to patch the missing features of ES6 that don't exist in ES5.

The most famous transpiler that is usually used in this case is [Babel](https://babeljs.io/).

#### Summary
-   ESM is the best module format thanks to its simple syntax, async nature, and tree-shakeability.
-   UMD works everywhere and usually used as a fallback in case ESM does not work
-   CJS is synchronous and good for back end.
-   AMD is asynchronous and good for front end.
