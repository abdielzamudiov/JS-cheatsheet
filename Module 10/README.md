### Module 10

#### Event types
These are the top 8 types of JavaScript Events:
1.  ##### User Interface events
2.  ##### Focusand blur events
3.  ##### Mouse events
4.  ##### Keyboard events 
5.  ##### Form events
6.  ##### Mutation events and observers
7.  ##### HTML5 events
8.  ##### CSS events
#### Event phases
There are three different phases during lifecycle of an JavaScript event in that order.
1. Capturing Phase - the event goes down to the element.
2. Target Phase - the event reached the target element.
3. Bubbling Phase -  the event bubbles up from the element.
#### Bubbling, capturing, targeting
1. ##### Bubbling
	Event bubbling is a method of event propagation in the HTML DOM API when an event is in an element inside another element, and both elements have registered a handle to that event. It is a process that starts with the element that triggered the event and then bubbles up to the containing elements in the hierarchy. In event bubbling, the event is first captured and handled by the innermost element and then propagated to outer elements.
	```html
	<div class="container">
		<div class="father">
	  		<div class="child"></div>
		</div>
	</div>
	```
	```js
	const father = document.querySelector('.father');
	const child = document.querySelector('.child');
	father.addEventListener('click',function (e) {
		console.log(e.eventPhase,e.currentTarget.className)
	});
	child.addEventListener('click',function (e) {
		console.log(e.eventPhase,e.currentTarget.className);
	});
	```
	If the element child is clicked:
	```
	2 'child'	//2 = target phase
	3 'father'	//3 = bubbling phase
	```
	If the father element is clicket
	```
	2 'father' //target phase
	```
2. ##### Capturing
	Event Capturing is the first to occur. The event first goes through the ancestors chain down to the element (capturing phase), then it reaches the target and triggers there (target phase), and then it goes up (bubbling phase), calling handlers on its way.
	The `addEventListener` method only executes on the targeting and the bubbling phase -as we saw on the example above- by natural behavior, but we can execute it in the Capturing phase, by adding `true` or `{capture: true}` as a third parameter.
	```
	<div class="container">
		<div class="father">
	  		<div class="child"></div>
		</div>
	</div>
	```
	```js
	const father = document.querySelector('.father');
	const child = document.querySelector('.child');
	father.addEventListener('click',function (e) {
		console.log(e.eventPhase,e.currentTarget.className)
	},true);
	child.addEventListener('click',function (e) {
		console.log(e.eventPhase,e.currentTarget.className);
	}.true);
	```
	If the element child is clicked:
	```
	1 'father'	//1 = capturing phase
	2 'child'	//2 = target phase
	```
	If the father element is clicket
	```
	2 'father' //target phase
	```
3. The event has arrived at the event's target. Event listeners registered for this phase are called at this time. If` Event.bubbles` is false, processing the event is finished after this phase is complete.
#### Event delegation
The idea is that if we have a lot of elements handled in a similar way, then instead of assigning a handler to each of them – we put a single handler on their common ancestor. It’s often used to add the same handling for many similar elements, but not only for that.

In the handler we get `event.target` to see where the event actually happened and handle it.
Benefits: 
1.  Simplifies initialization and saves memory: no need to add many handlers.
2. Less code: when adding or removing elements, no need to add/remove handlers.
3. DOM modifications: we can mass add/remove elements with `innerHTML` and the like.
#### Custom events
Custom events can be used to create “graphical components”. For instance, a root element of our own JS-based menu may trigger events telling what happens with the menu: open (menu open), select (an item is selected) and so on. Another code may listen for the events and observe what’s happening with the menu.

We can generate not only completely new events, that we invent for our own purposes, but also built-in ones, such as click, mousedown etc. That may be helpful for automated testing.

##### Event constructor

Built-in event classes form a hierarchy, similar to DOM element classes. The root is the built-in Event class.

We can create `Event` objects like this:
```js
let event = new Event(type[, options]);
```
Arguments:
-   _type_ – event type, a string like `"click"` or our own like `"my-event"`. 
-   _options_ – the object with two optional properties: 
    -   `bubbles: true/false` – if `true`, then the event bubbles.
    -   `cancelable: true/false` – if `true`, then the “default action” may be prevented. 
    
    By default both are false: `{bubbles: false, cancelable: false}`.
##### dispatchEvent
After an event object is created, we should “run” it on an element using the call elem.dispatchEvent(event).

Then handlers react on it as if it were a regular browser event. If the event was created with the bubbles flag, then it bubbles.
```html
<button id="elem" onclick="alert('Click!');">Autoclick</button>

<script>
	let event = new Event("click");
	elem.dispatchEvent(event);
</script>
```
_notes_: 
1. There is a way to tell a “real” user event from a script-generated one.
The property `event.isTrusted` is true for events that come from real user actions and false for script-generated events.
2. We should use MouseEvent instead of new Event if we want to create Mouse or Keyboard events. For instance, new MouseEvent("click"). The right constructor allows to specify standard properties for that type of event. Like clientX/clientY for a mouse event.
##### Custom events
For our own, completely new events types like "hello" we should use new CustomEvent. Technically CustomEvent is the same as Event, with one exception.
In the second argument (object) we can add an additional property detail for any custom information that we want to pass with the event.
```js// additional details come with the event to the handler
elem.addEventListener("hello", function(event) {
	alert(event.detail.name);
});

elem.dispatchEvent(new CustomEvent("hello", {
	detail: { name: "John" }
}));
```
#### Event prevention
Many events automatically lead to certain actions performed by the browser.
For instance:
-   A click on a link – initiates navigation to its URL.
-   A click on a form submit button – initiates its submission to the server.
-   Pressing a mouse button over a text and moving it – selects the text.

There are two ways to tell the browser we don’t want it to act:
-   The main way is to use the `event` object. There’s a method `event.preventDefault()`.
-   If the handler is assigned using `on<event>` (not by `addEventListener`), then returning `false` also works the same.
