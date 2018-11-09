---
layout: post
title:      "What's up with hoisting?"
date:       2018-11-09 01:45:40 +0000
permalink:  whats_up_with_hoisting
---


Hoisting is a quirky part of the JavaScript interpretation process, in which vars and function declarations are read and stored in memory during the compilation phase before program execution thereby altering the order in which our scripts are read. Although it may not have negatively affected your code (yet), it is a core concept that you must understand in order to prevent and/or debug bugs, and to learn to read your scripts like your computer reads them.

As we know, when you try to console.log some non-existent thing, you get a reference error.
```
console.log(peaceOnEarth) 
//reference error: peaceOnEarth is not defined
```

And with `let` and/or `const`, if I console.log a not-yet-existent thing we get the same error because it doesn’t exist at the time of the console log.
```
console.log(tomorrow) //reference error: tomorrow is not defined
let tomorrow = ‘a new day’
```

But with `var` we don’t get the error, because the `var` does exist—it’s just set to undefined at the point of the console log:
```
console.log(tomorrow) //undefined
var tomorrow = ‘a new day’
```

So in the computer’s eyes, this is the code:
```
var tomorrow
console.log(tomorrow)  //undefined 
tomorrow = ‘a new day’
```



And we see similar behavior with function declarations.

With a function declaration/statement, the entire function gets hoisted, so it can be called above itself.
```
readyWhenever()
function readyWhenever() {
     console.log(‘Call me whenever’);
}
```


However, this is not the case with function expressions. When you define a function within an expression only the declaration gets hoisted, so the computer thinks that you are trying to call a variable that has been instantiated as undefined.
```
notReady()
var notReady = function(){
    console.log("I'm not ready yet");
}
//TypeError: notReady is not a function
```

The computer reads it as:
```
var notReady
notReady()
//TypeError: notReady is not a function
```


When we look at the behavior within functions, we see more of the same.

As we know, the function has access to the global variable. No surprises here:
```
var location = 'outside'
function whereAmI () {
	console.log(“I’m: “, location) //I’m outside
}
```

But here we see something different—the first console log is undefined. This is because within a function the program hoists the internal variable, which is set to undefined, and the program proceeds to read the rest of the block.
```
var location = "outside"
function whereAmI () {
	console.log(“I’m ‘, location) //undefined
	var location = “inside"
	console.log(“I’m ‘, location) //I’m inside
}
```


It’s also important to remember that in JavaScript if/else blocks do not create local scopes. So if we use `var`  the first console log does not raise an error even though the variable first appears in the if statement.
```
function whatToEatForLunch(){
	console.log('Default dinner: ', dinner) //undefined
	if ('hungry') {
		var dinner = 'tacos'
		console.log("I'm hungry, so: ", dinner) //tacos
	} else {
	  var dinner = 'salad'
		console.log("I'm not very hungry, so: ", dinner)
	}
}
```

To avoid becoming a victim of tricky hoisting behavior, it is best to abide by a few best practices:                     

1.) Do not use var. Thanks to the introduction of let and const in ES6, var is no longer necessary.           
2.) Declare variables at the top of their scopes.
                                                                                                                     




















