title: '[javascript] Setting default values for parameters of a function'
author: John Doe
date: 2017-02-06 22:51:00
tags:
---
In javascript, you can call a function with any number of parameters you like. 

If the number of parameters you provided is less than the number of parameters specified in function declaration, then the rest of the parameters will be `undefined`.

Here's an example:
	
    // sayHello.js
    
	function sayHello(name) {
		console.log('Hello, ' + name);
	}
    
    sayHello()				// Hello, undefined
    sayHello('Brian');		// Hello, Brian

What happened here is that `name`, the undefined primitive type, is coerced into a string which contains `'undefined'` value. 
Then `Hello, ` and `'undefined'` are concatenated by `+` operator. 

What if you want to specify a value when the parameter is `undefined` ? Well, You can use `||` operator.

    // sayHello_default_value.js
    
	function sayHello(name) {
    	name = name || '<Your name>';	// line 4
		console.log('Hello, ' + name);
	}
    
    sayHello();			// Hello, <Your name>
    sayHello('Brian'); 	// Hello, Brian

You can simply think that line 4 means *if the value of `name` is  undefined, then assign it with `<Your name>` string value*. 
However, there's something you should be aware of with the above statement.

Let's dig deeper with `name = name || '<Your name>';`

    > node
	> 0 || 1
	1       
	> 1 || 2
	1       
	> undefined || 'Brian'
	'Brian'

From the above execution results, we can see that if `||` is passed with two values that can be coerced into `true` and `false`, or two values that can both be coerced into `true`, it returns the first value that coerced into `true`.

So what happened at line 4 in *sayHello_default_value.js* is that 
`name` and `'<Your name>'` are first coerced into boolean values. Because `'<Your name>'` is a string with length larger than 0, it is converted to `true`. 
The result of the conversion of `name` depends on the input value of the parameter. 
Then the return value of `||` is assiged to `name` on the left hand side of `=`. This is because the [precedence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence) of `||` is greater than that of `=`.

This means that if you pass a value that can be converted to `false`, like 0 or `''`, `Hello, <Your name>` will be printed by `sayHello()` function.



