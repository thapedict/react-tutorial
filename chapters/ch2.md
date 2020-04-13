# Chapter 2: ES6 and Transpiling

This chapter is for all those ancient programmers wanting to join in all that hype of React but hit a few stumbling blocks that come with ES6. As most of us know, JSX is what React is all about. Almost all React tutorials out there use JSX at least once. That tells you if you as a developer want any kind of future with React, you simple just have to comfortable with JSX.

## Well, what is JSX?

In a nutshell, JSX is HTML inside of JavaScript. Imagine the JavaScript code below:

```js
var someDiv = <div>Hello, I'm inside a div</div>;
```

Under normal circumstances, the above code would throw all kinds of errors. And you as a developer would never dream of writing such code. But thanks to the advancements of JavaScript all of this is now possible. The beauty of JSX. And the code above will run just fine, but the catch is it has to be transpiled first.

Transpiling (in JavaScript) is the process of turning all that non-valid code into valid JavaScript code. In the above code, it means that div will be converted to a valid DOM object. Smart hey, I know.

But don't get it confused, because in terms of ES6, sometimes that "non-valid code" might mean valid code. Let me clarify what I mean by that. Since browsers aren't keen on keeping up with the latest implementations of EMACScripts, some very smart people figure out a way to convert (tranpiling) new code (ES6 or newer) to old code (ES5), to keep their apps working across all browsers while using the latest features the JavaScript programming language has to offer. Crazy as it seems, this is the new norm and no one has looked back. Well...

## ES6 Features

The list is not as big as you think, but significant.

### Arrow functions

Yes, I'll start of with my favorite Arrow functions.
