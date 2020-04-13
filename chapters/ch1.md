# Chapter 1: Introduction

> Note:
    This tutorial assumes you know the basics of JavaScript, and a few concepts about OOP.

Over the past couple of days I've been giving React a go trying to understand the library as a whole. As complex as it was, there was really no easier way to learn it.

Now if you are coming from a world before ES6 (like me), some concepts will be easy to grasp, and some will required a few trial and errors. Because unlike other previous libraries, React isn't just about learning some function names, and how they work. It's a complete mindshift from how we used to write apps using JavaScript libraries.

## What's the deal with ES6

ECMAScript 2015 or ES6 for short, was a new standard (version) of JavaScript introduce back in 2015. With it brought a lot of change to how we write Javascript. These *change* included (but not limited to), new syntax, a way to declare a real class (like you would in other programming langauges such as Java or C#), new functions to built-in objects (such as Array and String), modular design coding, and something called promises. (**And in comes the real 'steep learning curve' that everyone talks about when learning React**).

It's so important to understand this from the start that if you are coming from a pre ES6 era and want to write React apps, you have to throw away most (if not all) of the things we learned about developing in JavaScript. It's just the nature of how the library is setup, so don't beat yourself up if you don't get it at first.

But fear not, you can actually write React apps without ES6 and any of it's features, but just know that will cost you a lot of typing hours. So before we get into the real fancy stuff of ES6, let's try it the 'old fashion way', with plain (or as they call it now 'Vanilla') JavaScript.

## Getting Started

So let's open up our favorite IDE and our browser.
I recommend (and use) VSC and Chrome.

First thing you want to do is [download] then extract the React files into your working directory then include the React script into your HTML file, so something like this should work:

```html
<script type="text/javascript" src="js/react.js"></script>
<script type="text/javascript" src="js/react-dom.js"></script>
```

[download]: https://react-cn.github.io/react/downloads/react-0.14.3.zip

By including react.js, you'll now have access to React, and all it's goodness.

In the beginning there are 3 important functions that one should absolutely know in order to start creating apps in React.

> React.createElement

> React.createClass

> ReactDOM.render

### React.createElement

createElement is a factory function that returns a React DOM element based on the arguments you pass to it.

```js
React.createElement(type, props, children, ...children);
```

Parameter   | Type
---         | ---
type        | String / ReactElement / ReactClass
props       | Object
children    | String / Object

The first argument can be passed either a HTML element type, or a React element/object.
The second arguments is reserved for that element's props.
And any subsequent arguments to this will be considered children (innerHTML) of the element that you're creating.

So to create a simple div with some hello world text inside of it you'd do this:

```js
React.createElement('div',{},'Hello, World!');
```

Calling the above function will return a React element.
A React element is a special type of HTML element which is manage (i.e. created, displayed, updated, and deleted) by the React engine.
We'll get more indepth about React elements vs HTML elements later.

### React.createClass

createClass is a special kind of factory function that returns a React class (which in many instances will be refered to as a Component).
For the puropse of this Book we'll refer to all things created with this function as a Component.
React Components have much more functionality than you're average React element.

```js
React.createClass(classDef);
```

Parameter   | Type
---         | ---
classDef    | Object

So to create a component:

```js
React.createClass({
    render: function() {
        return React.creacteElement('div',{},'Hello World!');
    }
});
```

> Note: All React classes (components) need to have a render function.
A render function gets called by React when it trys to render (output) the component on the screen.
The render function needs to return an react element so it can be shown on screen, or in the rare case return null if it don't render anything.

### ReactDOM.render

> Note:
React implements what it refers to as a Virtual DOM, which is a copy of the HTML DOM, with some added functionality.
***The real power of Virtual DOM is Node addressing, where each node is kept track of, and only updated (rendered) if that specific node changes.
This means if you have 3 HTML elements and only one get's updated (e.g. text changed etc.), only that element will get re-rendered.
This is a huge improvement unlike traditional HTML DOM where a change in one element means the entire page needs to re-rendered.

The render function in the ReactDOM object is your way of telling React that it's time to render the element (and it will internally copy it to the HTML DOM).
And if you need it to, you can use it to force a re-render of already rendered elements by calling it with the same arguments.

```js
ReactDOM.render( element, domNode )
```

Parameter   | Type
---         | ---
element     | reactElement / ReactClass
domNode     | HTML DOM element that will be used as a parent for the element

Real-life usecase:

```js
ReactDOM.render(
    React.createElement('div',{},'Hello, World!'),
    document.getElementById('container')
);
```

Note: The above function expects there to be a HTML element with an ID of container to be set:

```html
<div id="container"></div>
```

## Putting it all together

Okay, if you felt that was overwhelming, let's try and put all of that into practise to see how it all gels together.

In your index.html:

```html
<!doctype html>
<html>
    <head>
        <title>React Tutorial CH1</title>
        <script type="text/javascript" src="js/react.js"></script>
        <script type="text/javascript" src="js/react-dom.js"></script>
    </head>
    <body>
        <div id="container"></div>
        <script type="text/javascript" src="js/app.js"></script>
    </body>
</html>
```

In you app.js:

```js
var hw_title = React.createElement('h1',{},'Hello, World!');
var hw_desc = React.createElement('p',{},'My first React App');

var hw = React.createClass({
    render:function(){
        // Notice how I create an element to wrap my Hello World title and desciption and return it.
        return React.createElement(
            'div',
            {},
            hw_title,
            hw_desc
        )
    }
});

ReactDOM.render( hw, document.getElementById('container') );
```

Phew!!! I know what you're thinking, *"all that coding for writing two lines of text onto a screen? I'm never doing that again"*.

But that's not where the real power of React comes in.
Like in any library or framework, React has it's strong points, and some weak points.
It's certainly an over kill to use it for things like static content/websites.

Brace yourself. In the next chapter we will be looking into writing our code using ES6 and throwing in new concepts such a using a compiler & transpiler.
