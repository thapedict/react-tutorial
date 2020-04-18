# Chapter 2: ES6 and Transpiling

This chapter is for all those ancient programmers wanting to join in all that hype of React but hit a few stumbling blocks that come with ES6. As most of us know, JSX is what React is all about. Almost all React tutorials out there use JSX at least once. That tells you if you as a developer want any kind of future with React, you simple just have to comfortable with JSX.

> If you know your way around ES6 (and later) you can skip this chapter.

## Well, what is JSX

In a nutshell, JSX is HTML inside of JavaScript. Imagine the JavaScript code below:

```js
var someDiv = <div>Hello, I'm inside a div</div>;
```

Under normal circumstances, the above code would throw all kinds of errors. And you as a developer would never dream of writing such code. But thanks to the advancements of JavaScript all of this is now possible. The beauty of JSX. And the code above will run just fine, but the catch is it has to be 'transpiled' first.

## What is transpiling

Transpiling (in JavaScript) is the process of turning all that non-valid code into valid JavaScript code. In the above code, it means that *div* will be converted to a valid DOM object. Smart hey, I know.

But don't get it confused, because in terms of ES6, sometimes that "non-valid code" might mean valid code. Let me clarify what I mean by that. Since browsers aren't keen on keeping up with the latest implementations of EMACSScripts, some very smart people figure out a way to convert (transpiling) new code (ES6 or newer) to old code (ES5), to keep their apps working across all browsers while using the latest features the JavaScript programming language has to offer. Crazy as it seems, this is the new norm and no one has looked back. Well...

## ES6 Features

The list is not as big as you think, but significant.

### Arrow functions

Yes, I'll start of with my favourite Arrow functions. This is a new syntax of writing function definitions. What you need to know is arrow functions are anonymous. You can however store them in a variable to reuse them later.

```js
// old way
function some_func( arg1 ) {
    // do stuff
}
// var alternative
var some_func = function( arg1 ) {
    // do stuff
}

// arrow function
var some_func = ( arg1 ) => {
    // do stuff
}
```

As you might have guessed, all those 3 do pretty much the same thing. Let's break it down a bit:

```js
var some_func = ( arg1 ) => {
    // do stuff
}
```

The first part ```var some_func```, is nothing new. Here we are declaring a variable which will store our function.

The second part ```( arg1 )```, is the expected function arguments/parameters.

The third part (the arrow) ```=>```, let's the interpreter know the function body is about to start.

The forth and last part ```{ // do stuff }```, is the function body.

**Few points you should know:**

* Like in plain JS, you can choose to not save the function definition in a variable, thus making it anonymous.
* The function can accept zero args. To do that you can write ```() => { // do stuff }```.
* The brackets around the argument is optional **IF** your function only accepts one arg ```arg => { // do stuff }```.
* Just like if statements, The curly brackets around the function body are completely optional **IF** you are writing a single line statement. Which leads to my next point;
* The single line (not wrapped in brackets) statements are auto returned.
    This mean you can do this

    ```js
    // instead of
    function addOld(a, b){
        return a + b;
    }

    // you can write the following
    // look at the function body, there is no return keyword
    var addNew = (a, b) => a + b;

    addNew(2,3); // will return 5
    ```

#### The 'this that' debacle

I'm sure sometime in your junior JS coding life there has been a time where you've come across the *this* problem. This mostly occurs when you are dealing with events.

> Why doesn't this point to the current object I'm referring to??? #InsertCryingFaceHere#

```js
var Person = function(){
    this.name = "Person";

    this.setName = function( name ) {
        this.name = name;
    }

    this.log = function() {
        console.log('Name: ' + this.name);
    }
}

var John = new Person;

John.setName('John');
John.log(); // Name: John

John.setName('James');
John.log(); // Name: James

// Great. Everything is working correctly

// but let's say we want to show it on button click.
// You'd problably write something like this
$('.cool-button').on('click', John.log);
// The name is not printed, instead we just get "Name: "
// What gives??? #InsertConfusedFaceHere#
```

This understanding scope issue has long been like a never ending nightmare for junior JavaScript developers like myself. One way we got around it was to store the this object in another variable (```var that=this```), and use that variable to reference the current object. Not exactly rocket science stuff but it worked perfectly.

```js
// Warning: The 'this that' coding hack below
var Person = function(){
    var that = this; // here is the magic

    that.name = "Person";

    that.setName = function( name ) {
        that.name = name;
    }

    that.log = function() {
        console.log('Name: ' + that.name);
    }
}

John.setName('John');

// Now this works
$('.cool-button').on('click', John.log);
```

#### The bind to this hack

Another way of getting the this to work the way you expected was to explicitly bind the function to the current object. This nifty little function will bind whatever object you pass to it (including the this object) to the function (or variable) it is attached to. For a better understanding let's see it in action.

```js
var Person = function() {
    this.name = "Person";

    this.setName = function( name ) {
        this.name = name;
    }.bind(this) // see the bind in action

    this.log = function() {
        console.log('Name: ' + this.name);
    }.bind(this)
}
```

#### Arrow functions to the rescue

Arrow functions solve this scope issues because unlike traditional functions (which are objects themselves), their 'this' reference the closest object they are defined in. Keep in mind that plain functions in JavaScript are also objects (hence the reason the 'this' inside them points to that function).

```js
// so instead of 'this that' we can do this
var Person = function() {
    this.name = 'Person';

    this.setName = (name) => this.name = name;

    this.log = () => console.log('Name: ' + this.name);
}
```

The code is pretty nice if you ask me. No more guessing if it will work or not.
