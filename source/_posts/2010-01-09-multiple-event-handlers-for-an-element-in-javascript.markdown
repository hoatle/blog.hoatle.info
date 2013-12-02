---
layout: post
title: "Multiple event handlers for an element in JavaScript"
author: hoatle
date: 2010-01-09 01:55
comments: true
categories:
    - "en"
tags:
    - "JavaScript"
cover:
description: Multiple event handlers for an element in JavaScript
keywords: Multiple event handlers for an element in JavaScript
published: true
---

This afternoon I caught a question posted in phpvietnam group:

**"I have an input element with the property onclick="doSomeFunction();". Now I want to add another
function, ie onclick="doSomeFunction(); doSomeFunction2();", can I do this with JavaScript? Thanks
in advance!" (translated)**

*Source (in Vietnamese)*:
http://groups.google.com/group/phpvietnam/browse_thread/thread/c7a8688875a320c3

<!-- more -->

After answering his question, I just want to share my experience when working with JavaScript event
handler. I will show you 4 event registration models for the time beings of its use; the way to use
context and this keyword in function handler. My approach is that the event object will be passed
as 1st parameter to the function handler and this has to refer to the element triggering that event.

**1. Inline Event Registration Model**

From the first days of JavaScript, there is only one way of registering event handler and nowadays
this approach is still being used. Here we call the primitive approach:

```html
<a href="#" onclick="doSomething();">link</a>
```

People are so familiar with this event registration model, especially from the days of writing the
first lines of JavaScript code. There is nothing wrong with this kind of model, even it's
convenient, fast, easy to understand and people are still using this way :P. However, when
JavaScript evolves, the event registration approach changes because some problems arise: this
approach does not separate structure (html) and behaviour (JavaScript); this makes code more
complex, not very flexible to edit html. Just imagine when creating dom on the fly and constructing
new html fragment code to insert to html document? This approach does not seem fit well in this case.

Now working with event object and this keyword. We have the event handler function:

```javascript
function doSomething(evt) {
  alert(arguments[0]); // arguments[0] the same as evt
  alert(this);
}
```

In this case, when the link element is clicked, the `doSomething` handler function will be called
and `evt` will get `undefined (null)` value and `this` will refer to `window` object. This is not my
intention, I want the event has to be event object and this has to refer to the link element. So I
have to modify the code a little bit:

```html
<a href="#" onclick="doSomething(event);">link</a>
```

With above code, the event object is passed to `doSomething` handler function. In my assumption,
when link element is clicked, the `onclick` event is triggered from the browser native code:

```javascript
//[Native Code]
onclick(event) {
  //event handler is called
  doSomething(event);
}
```

Remember that we pass `event` as parameter to `doSomething` function but not any other name. If we
pass `evt` for example, the exception occurs:

```javascript
[Native Code]
onclick(event) {
  //call event handler and pass evt as parameter
  doSomething(evt); //exception occured because evt is undefined (null).
}
```

Because this is the browser native code, it does not allow to use `undefined (null)` value there.
However, we can pass any `undefined` or `null` parameter to any our JavaScript functions as normal,
there is no exception in this case. Note that the above code is tested with chrome and it just
works (?). No exception at all but not the case for IE, Firefox, Opera, Safari. Well, in this case
I don't know if google chrome is good or bad?

By using the event parameter passed to `doSomething` function, now we can get the event object to
get many useful properties there. For example, event type, cursor location, charCode, etc.,

Now we have to make sure `this` in `doSomething` function has to refer to link element, not
`window` object with the following code:

```html
<a href="#" onclick="doSomething.call(this, event)">link</a>
```

From the browser native code will trigger the `onclick` event as follows:

```javascript
onclick(event) {
  //this is the triggred element
  doSomething.call(this, event);
}
```

The above inline event registration code now works as my intention. I just explain in details in
this part only.

**2. Traditional Event Registration Model**

This is the model many developers use to separate structure and behaviour in the html document.
Html contains html only, and in JavaScript traditional event registration model will be used:

```html
<a href="#" id="mylink">link</a>
```

Make sure after the dom is loaded, this code will execute:

```javascript
var linkEl = document.getElementById('myLink');
linkEl.onclick = function() {
  doSomething();
}
```

This way of event registration is compatible with all major browsers. In this model, event object
is passed as the only parameter to the handler function and `this` in the handler function block
refer to linkEl.

Code this way to make sure `doSomething` function still has access to event object and `this` refers
to element triggering the event.

```javascript
linkEl.onclick = function(evt) {
  doSomething.call(this,evt);
}
```

In case the `doSomething` function has more than 1 arguments:

```javascript
function doSomething(evt, param1, param2) {
//code implementation
}

linkEl.onclick = function(evt) {
  var param1, param2;
  doSomething.call(this, evt, param1, param2);
  // same as: doSomething.apply(this, [evt, param1, param2]);
}
```

And then we come up with 3rd and 4th event registration model: W3C model and Microsof (IE) model.
By combining these 2 models, we got the solution for event registration compatible with all major
browsers:

**3. W3C Event Registration Model**

This is the specification of W3C to register event listener (handler). By using it, we can register
as many listeners as possible.

```javascript
element.addEventListener(eventType, listener, useCapture);
```

`eventType`: click, mouseover, mouseout, etc.,

`listener`: event handler function, it will be called when the element triggered eventType event.

`useCapture`: you should always pass false to make it compatible with IE. This relates to event
phases which I will make another blog post about.

We can apply as:

```html
<a href="#" id="mylink">link</a>
```

```javascript
//javascript, run only on Firefox, Opera, Chrome, Safari
// can not run on IE
var linkEl = document.getElementById('myLink');
linkEl.addEventListener('click', function() {
    alert(arguments[0]); //event object
    alert(this); //linkEl
}, false);
event object is passed as parameter and this refers to linkEl in event handler:


linkEl.addEventListener('click', function(evt) {
    doSomething.call(this, evt);
}, false);
```

By using this approach, you can add as many listeners as possible. When an eventType triggered, all
registered listeners will be executed. Note that W3C DOM specification does not require that the
first listener registered will be executed first, these listeners can be executed by random. And
till now, there is no way to check how many listeners registered in an element.

*How about removing an event listener?*

```javascript
element.removeEventListener(eventType, listener, useCapture);
```

I rarely use `removeEventListener`. You can not remove an anonymous function. From the above code,
I use anonymous function as listener, as the result, I can not find the way to remove it. Assigning
it a name and the problem solved:

```javascript
var myListener = function() {
  alert(arguments[0]);
  alert(this);
 //first run and then remove listener, no event triggered from now anymore
  this.removeEventListener('click', myListener, false);
}
linkEl.addEventListener('click', myListener, false);
```

This is the W3C way and M$ follows an other way.

**4. Microsoft Event Registration Model**

IE does not use `addEventListener` but `attachEvent`:

```javascript
    element.attachEvent(onEventType, handler);
```

For example:

```javascript
var linkEl = document.getElementById('myLink');
//run on IE only
linkEl.attachEvent('onclick', function() {
  alert(arguments[0]); //event object
  alert(this); //linkEl
})
```

Wanna remove a handler (listener)? Use `detachEvent`:

```javascript
var myListener = function(evt) {
  alert(evt);
  alert(this);
  this.detachEvent('onclick', myListener);
}
```

Note that IE does not have 2 event phases (capture and bubble) but bubble phase only. So when using
W3C, you should always use `false` for `useCapture` for safety purpose :d. If you fully understand
these 2 event phases, you can pass true for `useCapture` but intentionally.

**5. At last, combine these 2 models for simple and compatible api:**

```javascript
//api design
addEventListener(element, eventType, listener, useCapture);
removeEventListener(element, eventType, listener, useCapture);
```

My intention is that event object has to be passed as 1st parameter to listener and this has to
refer to the element in the block code. Here we come the solution:

```javascript
/**
 * Cross browser add event listener method. For 'evt' pass a string value with the leading "on" omitted
 * e.g. addEventListener(window,'load',myFunctionNameWithoutParenthesis,false);
 * @param    obj object to attach event
 * @param    evt event name: click, mouseover, focus, blur...
 * @param    func    function name
 * @param    useCapture    true or false; if false => use bubbling
 * @static
 * @see        http://phrogz.net/JS/AttachEvent_js.txt
 */
function addEventListener(obj, evt, fnc, useCapture) {
    if (obj === null || evt === null || fnc ===  null || useCapture === null) {
       alert('all params are required for addEventListener');
        return;
    }
    if (!useCapture) useCapture = false;
    if (obj.addEventListener){
        obj.addEventListener(evt, fnc, useCapture);
    } else if (obj.attachEvent) {
        obj.attachEvent('on'+evt, function(evt) {
            fnc.call(obj, evt);
        });
    } else{
        myAttachEvent(obj, evt, fnc);
        obj['on'+evt] = function() { myFireEvent(obj,evt) };
    }

    //The following are for browsers like NS4 or IE5Mac which don't support either
    //attachEvent or addEventListener
    var myAttachEvent = function(obj, evt, fnc) {
        if (!obj.myEvents) obj.myEvents={};
        if (!obj.myEvents[evt]) obj.myEvents[evt]=[];
        var evts = obj.myEvents[evt];
        evts[evts.length] = fnc;
    }

    var myFireEvent = function(obj, evt) {
        if (!obj || !obj.myEvents || !obj.myEvents[evt]) return;
        var evts = obj.myEvents[evt];
        for (var i=0,len=evts.length;i<len;i++) evts[i]();
    }
}

/**
 * removes event listener.
 * @param    obj element
 * @param    evt event name, 'click', 'blur'. 'focus'...
 * @func    function name to be removed if found
 * @static
 * //TODO make sure method cross-browsered
 */
function removeEventListener(obj, evt, func, useCapture) {
    if (obj.removeEventListener) {
        obj.removeEventListener(evt, func, useCapture);
    } else if (obj.detachEvent) {//IE
        obj.detachEvent('on'+evt, func);
    }
}
```

Use this api as simple as:

```javascript
  var linkEl = document.getElementById('myLink');
  addEventListener(linkEl, 'click', function(evt) {
    doSomething.call(this, evt);
  }, false);
```

Hope that you find this post interesting, I will blog about 2 event phases soon. Happy coding :D
