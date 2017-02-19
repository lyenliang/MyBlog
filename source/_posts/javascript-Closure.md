title: '[javascript] Closure'
author: lyenliang
date: 2017-02-17 20:35:02
tags:
---
*Closure* is an important topic in javascript if you want to have a deep understanding of this language. 
In this article, I'll explain the concept of *closure* based on what I've learned at [udemy](https://www.udemy.com/). If you find anything strange or weird with this article, feel free to let me know by leaving a comment below.

First, let's say I have a function like this:

    function foo(var1) {
    	return bar(var2) {
        	console.log(var1 + ' ' + var2);
        }
    }
    
A function `foo` that returns another function `bar`. When I invoke `foo('Hello')`, I get another function that I can invoke again. 

    var sayHello = foo('Hello');
    sayHello('Brian');	// Hello Brian
    
It seems very intuitive that `sayHello('Brian')` will display `Hello Brian`. But let's stop and think about this for a moment. How does `sayHello` remember the value of `var1`, `'Hello'`, when `sayHello('Brian')` is invoked? Because the `var1` variable is created when `foo('Hello')` is called. And when this `foo` function is over, the execution context is popped off the execution stack. And yet it still has the correct value, `'Hello'`, of `var1`. How is that possible? Well, this is where *closure* comes into play.

To understand what happened, we need to take a look at the execution stack.
When the code starts, the global execution context is created. 

<img src="/images/javascript/execution_stack/global.png" alt="午安枕的墊子" style="width: 380px;"/>

When `var sayHello = foo('Hello');` line is hit, we have the `foo()` execution context created. And the variable that's passed to it, `'Hello'`, is sitting in its variable environment. The `foo` function returns a new function object. 


<img src="/images/javascript/execution_stack/foo_var1.png" alt="午安枕的墊子" style="width: 350px;"/>

After the return, the `foo` execution context is popped off the execution stack.

<img src="/images/javascript/execution_stack/var1.png" alt="午安枕的墊子" style="width: 350px;"/>

Under normal circumstances, the memory space outside of the execution context will be garbage collected. But because of *closure*, the javascript engine knows it should keep the `var1` variable. 

And this is why `bar` execution context can have access to the `var1` variable:

When javascript engine sees the `var1` variable at `console.log(var1 + ' ' + var2)` line, it goes up the scope chain to look for the value of `var1`. And becuase there's an outer lexical environment reference. 
The javascript engine is able to find `var1` outside of `bar` execution context.


<img src="/images/javascript/execution_stack/var2_var1.png" alt="午安枕的墊子" style="width: 350px;"/>

The phenomon that the `bar` execution context is closed in its outer variables is called a *closure*.

<img src="/images/javascript/execution_stack/closure.png" alt="午安枕的墊子" style="width: 350px;"/>


