### Module 11
- AJAX, XMLHTTPRequest
	What is AJAX?
	AJAX is a technique for accessing web servers from a web page. Stands for Asynchronous JavaScript And XML and is not a programming language.
	With AJAX you can:
	- Read data from a web server - after the page has loaded.
	- Update a web page without reloading the page.
	- Send data to a web server - in the background.
	
	AJAX just uses a combination of:
	- A browser built-in `XMLHttpRequest` object (to request data from a web server).
	- JavaScript and HTML DOM (to display or use the data).

	AJAX applications might use XML to transport data, but it is equally common to transport data as plain text or JSON text.
	#### How AJAX works
	[[pic_ajax.gif]]
	1. An event occurs in a web page (the page is loaded, a button is clicked).
	2. An XMLHttpRequest object is created by JavaScript.
	3. The XMLHttpRequest object sends a request to a web server.
	4. The server processes the request.
	5. The server sends a response back to the web page.
	6. The response is read by JavaScript.
	7. Proper action (like page update) is performed by JavaScript.
	
	#### XMLHTTPRequest
	To send an HTTP request, create an `XMLHttpRequest` object, open a URL, and send the request. After the transaction completes, the object will contain useful information such as the response body and the [HTTP status](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) of the result.
	```js
		function reqListener () {
  			console.log(this.responseText);
		}

		var oReq = new XMLHttpRequest();
		oReq.addEventListener("load", reqListener);
		oReq.open("GET", "http://www.example.org/example.txt");
		oReq.send();
	```
	A request made via `XMLHttpRequest` can fetch the data in one of two ways, asynchronously or synchronously. The type of request is dictated by the optional `async` argument (the third argument) that is set on the [`XMLHttpRequest.open()`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/open) method. If this argument is `true` or not specified, the `XMLHttpRequest` is processed asynchronously, otherwise the process is handled synchronously.
	
	#### Handling responses
	There are several types of [response attributes](https://xhr.spec.whatwg.org/) defined by the living standard specification for the [`XMLHttpRequest()`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/XMLHttpRequest "XMLHttpRequest()") constructor. These tell the client making the `XMLHttpRequest` important information about the status of the response.
	
	#### XMLHttpRequest.response
	The [`XMLHttpRequest`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) `**response**` property returns the response's body content as an [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer), [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob), [`Document`](https://developer.mozilla.org/en-US/docs/Web/API/Document), JavaScript [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object), or [`DOMString`](https://developer.mozilla.org/en-US/docs/Web/API/DOMString), depending on the value of the request's [`responseType`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/responseType "responseType") property.    
	Syntax:
	```js
		var body = XMLHttpRequest.response;
	```
	
- fetch
	JavaScript can send network requests to the server and load new information whenever it’s needed.

	For example, we can use a network request to:
	-   Submit an order,
	-   Load user information,
	-   Receive latest updates from the server,
	-   …etc.
	…And all of that without reloading the page!

	There are multiple ways to send a network request and get information from the server.
	The `fetch()` method is modern and versatile, so we’ll start with it. It’s not supported by old browsers (can be polyfilled), but very well supported among the modern ones.   
	Syntax:
	```js
		let promise = fetch(url, [options])
	```
	-   **`url`** – the URL to access.
	-   **`options`** – optional parameters: method, headers etc.
	
	Getting a response is usually a two-stage process.

	**First, the `promise`, returned by `fetch`, resolves with an object of the built-in [Response](https://fetch.spec.whatwg.org/#response-class) class as soon as the server responds with headers.**
	
	We can see HTTP-status in response properties:
	-   **`status`** – HTTP status code, e.g. 200.
	-   **`ok`** – boolean, `true` if the HTTP status code is 200-299.   
	Example:   
	```js
		let response = await fetch(url);
		
		if (response.ok) { // if HTTP-status is 200-299
			// get the response body (the method explained below)
			let json = await response.json();
		} else {
			alert("HTTP-Error: " + response.status);
		}
	```
	`Response` provides multiple promise-based methods to access the body in various formats:
	-   **`response.text()`** – read the response and return as text,
	-   **`response.json()`** – parse the response as JSON,
	-   **`response.formData()`** – return the response as `FormData` object (explained in the [next chapter](https://javascript.info/formdata)),
	-   **`response.blob()`** – return the response as [Blob](https://javascript.info/blob) (binary data with type),
	-   **`response.arrayBuffer()`** – return the response as [ArrayBuffer](https://javascript.info/arraybuffer-binary-arrays) (low-level representation of binary data),
	-   additionally, `response.body` is a [ReadableStream](https://streams.spec.whatwg.org/#rs-class) object, it allows you to read the body chunk-by-chunk, we’ll see an example later.
	
	**Important**
	We can choose only one body-reading method.
	If we’ve already got the response with `response.text()`, then `response.json()` won’t work, as the body content has already been processed.
	```js
		let text = await response.text(); // response body consumed
		let parsed = await response.json(); // fails (already consumed)
	```
	
- Request Headers
	To set a request header in `fetch`, we can use the `headers` option. It has an object with outgoing headers, like this:
	```js
		let response = fetch(protectedUrl, {
			headers: {
				Authentication: 'secret'
			}
		});
	```
	…But there’s a list of [forbidden HTTP headers](https://fetch.spec.whatwg.org/#forbidden-header-name) that we can’t set:
	-   `Accept-Charset`, `Accept-Encoding`
	-   `Access-Control-Request-Headers`
	-   `Access-Control-Request-Method`
	-   `Connection`
	-   `Content-Length`
	-   `Cookie`, `Cookie2`
	-   `Date`
	-   `DNT`
	-   `Expect`
	-   `Host`
	-   `Keep-Alive`
	-   `Origin`
	-   `Referer`
	-   `TE`
	-   `Trailer`
	-   `Transfer-Encoding`
	-   `Upgrade`
	-   `Via`
	-   `Proxy-*`
	-   `Sec-*`
	
	These headers ensure proper and safe HTTP, so they are controlled exclusively by the browser.
	
- JSONP
	JSONP is a method for sending JSON data without worrying about cross-domain issues. Does not use the `XMLHttpRequest` object. JSONP uses the `<script>` tag instead.
	JSONP stands for JSON with Padding.
	Requesting a file from another domain can cause problems, due to cross-domain policy.
	Requesting an external _script_ from another domain does not have this problem.
	JSONP uses this advantage, and request files using the script tag instead of the `XMLHttpRequest` object.
	```js
		<script src="demo_jsonp.php">
	```
	Example:
	```js
		function foo(payload_of_json_data) {
    		// do stuff with JSON
		}

		var script = document.createElement('script');
		script.src = '//example.com/path/to/jsonp?callback=foo'

		document.getElementsByTagName('head')[0].appendChild(script);
		// or document.head.appendChild(script) in modern browsers
	```
	
- REST
	REST, or REpresentational State Transfer, is an architectural style for providing standards between computer systems on the web, making it easier for systems to communicate with each other.
	Separating the user interface concerns from the data storage concerns, we improve the flexibility of the interface across platforms and improve scalability by simplifying the server components. Additionally, the separation allows each component the ability to evolve independently.
	
	#### Statelessness
	Systems that follow the REST paradigm are stateless, meaning that the server does not need to know anything about what state the client is in and vice versa.
	This constraint of statelessness is enforced through the use of _resources_, rather than _commands_. Resources are the nouns of the Web - they describe any object, document, or _thing_ that you may need to store or send to other services.
	
	#### Making Request
	REST requires that a client make a request to the server in order to retrieve or modify data on the server. A request generally consists of:
	- an HTTP verb, which defines what kind of operation to perform.
	- a _header_, which allows the client to pass along information about the request.
	- a path to a resource.
	- an optional message body containing data.
	
	#### HTTP Verbs
	There are 4 basic HTTP verbs we use in requests to interact with resources in a REST system:
	- GET — retrieve a specific resource (by id) or a collection of resources.
	- POST — create a new resource.
	- PUT — update a specific resource (by id).
	- DELETE — remove a specific resource by id.
	
	You can find more info on the [[Lectures 11]] doc.

- URL, Encoding strings
	With [Hypertext](https://developer.mozilla.org/en-US/docs/Glossary/Hypertext) and [HTTP](https://developer.mozilla.org/en-US/docs/Glossary/HTTP), **URL** is one of the key concepts of the Web. It is the mechanism used by [browsers](https://developer.mozilla.org/en-US/docs/Glossary/Browser) to retrieve any published resource on the web.
	
	**URL** stands for _Uniform Resource Locator_. A URL is nothing more than the address of a given unique resource on the Web. In theory, each valid URL points to a unique resource. Such resources can be an HTML page, a CSS document, an image, etc. In practice, there are some exceptions, the most common being a URL pointing to a resource that no longer exists or that has moved.   
	Example:
	- https://developer.mozilla.org
	- https://developer.mozilla.org/en-US/docs/Learn/

	Any of those URLs can be typed into your browser's address bar to tell it to load the associated page (resource).
	A URL is composed of different parts, some mandatory and others optional. The most important parts are highlighted on the URL below (details are provided in the following sections):
	[[mdn-url-all.png]]
	
- Cross-Origin Requests
	**Cross-site HTTP requests** are HTTP requests for resources from a **different domain** than the domain of the resource making the request. For instance, an HTML page from Domain A (`http://domaina.example/`) makes a request for an image on Domain B (`http://domainb.foo/image.jpg`) via the `img` element. Web pages today very commonly load cross-site resources, including CSS stylesheets, images, scripts, and other resources. 
	The CORS mechanism supports secure cross-origin requests and data transfers between browsers and servers. Modern browsers use CORS in APIs such as `XMLHttpRequest` or [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) to mitigate the risks of cross-origin HTTP requests. CORS allows web developers to control how their site reacts to cross-site requests.   
	Example:
 	[[cross-origin-resource-sharing-ablauf.png]]
	
- Long polling
	[Long polling](https://en.wikipedia.org/wiki/Push_technology#Long_polling) is essentially a more efficient form of the original polling technique. Making repeated requests to a server wastes resources, as each new incoming connection must be established, the HTTP headers must be parsed, a query for new data must be performed, and a response (usually with no new data to offer) must be generated and delivered. The connection must then be closed, and any resources cleaned up. Rather than having to repeat this process multiple times for every client until new data for a given client becomes available, long polling is a technique where the server elects to hold a client’s connection open for as long as possible, delivering a response only after data becomes available or a timeout threshold has been reached.
	
	Implementation is mostly a server-side concern. On the client side, only a single request to the server needs to be managed. When the response is received, the client can initiate a new request, repeating this process as many times as is necessary. The only difference to basic polling, as far as the client is concerned, is that a client performing basic polling may deliberately leave a small time window between each request so as to reduce its load on the server, and it may respond to timeouts with different assumptions than it would for a server that does not support long polling. With long polling, the client may be configured to allow for a longer timeout period (via a `Keep-Alive` header) when listening for a response – something that would usually be avoided seeing as the timeout period is generally used to indicate problems communicating with the server.
	[[long-polling.png]]
	
	Also, the server needs to manage the unresolved state of multiple connections, and it may need to implement strategies for preserving session state when multiple servers and load balancers are in use (commonly referred to as session “stickiness”). It also needs to gracefully handle connection timeout issues, which are much more likely to occur than with designed-for-purpose protocols such as [WebSockets](https://www.ably.io/topic/websockets), a standard which did not arrive until years after long polling was established as a conventional technique for pseudo-realtime communication.
	
- WebSockets API overview
	The `WebSocket` protocol, described in the specification [RFC 6455](http://tools.ietf.org/html/rfc6455) provides a way to exchange data between browser and server via a persistent connection. The data can be passed in both directions as “packets”, without breaking the connection and additional HTTP-requests.
	[[websocket-handshake.svg]]
	
	WebSocket is especially great for services that require continuous data exchange, e.g. online games, real-time trading systems and so on.   
	Example:
	To open a websocket connection, we need to create `new WebSocket` using the special protocol `ws` in the url:
	```js
		let socket = new WebSocket("_ws_://javascript.info");
	```
	There’s also encrypted `wss://` protocol. It’s like HTTPS for websockets.
	
	#### Always prefer wss://
	The `wss://` protocol is not only encrypted, but also more reliable.
	That’s because `ws://` data is not encrypted, visible for any intermediary. Old proxy servers do not know about WebSocket, they may see “strange” headers and abort the connection.
	On the other hand, `wss://` is WebSocket over TLS, (same as HTTPS is HTTP over TLS), the transport security layer encrypts the data at sender and decrypts at the receiver. So data packets are passed encrypted through proxies. They can’t see what’s inside and let them through.
	
	Once the socket is created, we should listen to events on it. There are totally 4 events:
	-   **`open`** – connection established,
	-   **`message`** – data received,
	-   **`error`** – websocket error,
	-   **`close`** – connection closed.
	
	…And if we’d like to send something, then `socket.send(data)` will do that.
	Here’s an example:
	```js
		let socket = new WebSocket("wss://javascript.info/article/websocket/demo/hello");
		
		socket.onopen = function(e) {
			alert("[open] Connection established");
			alert("Sending to server");
			socket.send("My name is John");
		};
		
		socket.onmessage = function(event) {
			alert(`[message] Data received from server: ${event.data}`);
		};
		
		socket.onclose = function(event) {
			if (event.wasClean) {
				alert(`[close] Connection closed cleanly, code=${event.code} reason=${event.reason}`);
			} else {
				// e.g. server process killed or network down
				// event.code is usually 1006 in this case
				alert('[close] Connection died');
			}
		};
		
		socket.onerror = function(error) { 
			alert(`[error] ${error.message}`); 
		};
	```
	
	#### Interfaces
	- [`WebSocket`](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket)
		The primary interface for connecting to a WebSocket server and then sending and receiving data on the connection.
	- [`CloseEvent`](https://developer.mozilla.org/en-US/docs/Web/API/CloseEvent)
		The event sent by the WebSocket object when the connection closes.
	- [`MessageEvent`](https://developer.mozilla.org/en-US/docs/Web/API/MessageEvent)
		The event sent by the WebSocket object when a message is received from the server.
	
- HTTP 2.0 overview
	Since its inception in the early nineties, HTTP has seen only a few major revisions. The most recent version, HTTP1.1 has served the cyber world for over 15 years. Web pages in today's era of dynamic information updates, resource-intensive media content formats, and excessive inclination toward web performance have placed older protocol technologies in the legacy category. These trends demand significant HTTP/2 changes to improve the internet experience.
	[[http-timeline.png]]
	
	In February 2015, the [ietf](https://www.ietf.org/) (Internet Engineering Working Group) an HTTP Working Group reviewed and developed the second version of the application in the form of an HTTP/2 protocol. In May 2015, the HTTP/2 application specification was officially standardized in response to the protocol [SPDY](https://es.wikipedia.org/wiki/SPDY) supports HTTP.
	
	The main goal of research and development of a new version of HTTP is centered around three qualities rarely associated with a single network protocol without requiring additional networking technologies of high performance, simplicity, and robustness. These goals are achieved by introducing features that reduce latency in processing browser requests with techniques such as multiplexing, compression, prioritization, and server push request.
	
- Window post messages
	The **`window.postMessage()`** method safely enables cross-origin communication between [`Window`](https://developer.mozilla.org/en-US/docs/Web/API/Window) objects; _e.g.,_ between a page and a pop-up that it spawned, or between a page and an iframe embedded within it.

	Normally, scripts on different pages are allowed to access each other if and only if the pages they originate from share the same protocol, port number, and host (also known as the "[same-origin policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)"). `window.postMessage()` provides a controlled mechanism to securely circumvent this restriction (if used properly).

	Broadly, one window may obtain a reference to another (_e.g.,_ via `targetWindow = window.opener`), and then dispatch a [`MessageEvent`](https://developer.mozilla.org/en-US/docs/Web/API/MessageEvent) on it with `targetWindow.postMessage()`. The receiving window is then free to [handle this event](https://developer.mozilla.org/en-US/docs/Web/Events/Event_handlers) as needed. The arguments passed to `window.postMessage()` (_i.e.,_ the “message”) are [exposed to the receiving window through the event object](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage#the_dispatched_event).   
	Syntax:
	```js
		targetWindow.postMessage(message, targetOrigin, [transfer]);
	```
	_targetWindow_
	A reference to the window that will receive the message. Methods for obtaining such a reference include:
	-   [`window.open`](https://developer.mozilla.org/en-US/docs/Web/API/Window/open) (to spawn a new window and then reference it),
	-   [`window.opener`](https://developer.mozilla.org/en-US/docs/Web/API/Window/opener) (to reference the window that spawned this one),
	-   [`HTMLIFrameElement.contentWindow`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLIFrameElement/contentWindow) (to reference an embedded [`<iframe>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) from its parent window),
	-   [`window.parent`](https://developer.mozilla.org/en-US/docs/Web/API/Window/parent) (to reference the parent window from within an embedded [`<iframe>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)), or
	-   [`window.frames`](https://developer.mozilla.org/en-US/docs/Web/API/Window/frames) + an index value (named or numeric).
	
	_message_
	Data to be sent to the other window. The data is serialized using [`the structured clone algorithm`](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Structured_clone_algorithm "the structured clone_algorithm"). This means you can pass a broad variety of data objects safely to the destination window without having to serialize them yourself.
	
	_targetOrigin_
	Specifies what the origin of `targetWindow` must be for the event to be dispatched, either as the literal string `"*"` (indicating no preference) or as a URI. If at the time the event is scheduled to be dispatched the scheme, hostname, or port of `targetWindow`'s document does not match that provided in `targetOrigin`, the event will not be dispatched; only if all three match will the event be dispatched.
	**Always provide a specific `targetOrigin`, not `*`, if you know where the other window's document should be located. Failing to provide a specific target discloses the data you send to any interested malicious site.**
	
	`_**transfer**_` Optional
	Is a sequence of [`Transferable`](https://developer.mozilla.org/en-US/docs/Web/API/Transferable) objects that are transferred with the message. The ownership of these objects is given to the destination side and they are no longer usable on the sending side.

- Cookie
	A cookie is **a data file that a web page sends to your computer** when you visit it. 
	Cookies are usually used mainly for two main purposes: **remembering access and knowing browsing habits.**
	The most important thing about cookies are their functions to remember accesses,  were invented to solve the problem "how to remember information about the user".
	
	Cookies are data, stored in small text files, on your computer.
	They are saved in name-value pairs like:
	```js
		username = John Doe
	```
	When a browser requests a web page from a server, cookies belonging to the page are added to the request. This way the server gets the necessary data to "remember" information about users.
	**None of the examples below will work if your browser has local cookies support turned off.**
	JavaScript can create, read, and delete cookies with the `document.cookie` property.
	
	With JavaScript, a cookie can be created like this:
	```js
		document.cookie = "username=John Doe";
	```
	You can also add an expiry date (in UTC time). By default, the cookie is deleted when the browser is closed:
	```js
		document.cookie = "username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC";
	```
	With a path parameter, you can tell the browser what path the cookie belongs to. By default, the cookie belongs to the current page.
	```js
		document.cookie = "username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC; path=/";
	```
	Read all cookies accesible from this location:
	```js
		allCookies = document.cookie;
	```
	
- Network basics
	For better purpose I let links to good links about the fundamentals of networking because this topic is too general and we can understand better in a separate document with images and graphs too.