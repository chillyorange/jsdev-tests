#Answer 1

The code above prints `5`.

The trick of this question is that in the IIFE there are two assignments but the variable **a** is declared using the keyword **var**. What this means is that **a** is a local variable of the function. On the contrary, **b** is assigned to the global scope.

The other trick of this question is that it doesn’t use *strict mode* ('**use strict**';) inside the function. If strict mode was enabled, the code would raise the error Uncaught ReferenceError: b is not defined. Remember that strict mode requires you to explicitly reference to the global scope if this was the intended behavior. So, you should write:

```javascript
(function() {
   'use strict';
   var a = window.b = 5;
})();

console.log(b);
```

#Answer 2

A possible implementation is shown below:

```javascript
String.prototype.repeatify = String.prototype.repeatify || function(times) {
   var str = '';

   for (var i = 0; i < times; i++) {
      str += this;
   }

   return str;
};
```

The question tests the knowledge of the developer about inheritance in JavaScript and the prototype property. It also verifies that the developer is able to extend native data type functionalities (although this should not be done). Obviously, this question can have a number of different answer which can all be correct. To test wether the code works, the Chrome consule can be used.

Another important point here is to demonstrate that you are aware about how to not override possible already defined functions. This is done by testing that the function didn’t exist before defining your own:

```javascript
String.prototype.repeatify = String.prototype.repeatify || function(times) {/* code here */};
```

This technique is particularly useful when you are asked to shim a JavaScript function.

#Question 3

The result of this code is `undefined` and `2`.

The reason is that both variables and functions are hoisted (moved at the top of the function) but variables don’t retain any assigned value. So, at the time the variable *a* is printed, it exists in the function (it’s declared) but it’s still *undefined*.

#Question 4

The code prints `Aurelio De Rosa` and `John Doe`. The reason is that the context of a function, what is referred with the *this* keyword, in JavaScript depends on how a function is invoked, not how it’s defined.

In the first *console.log()* call, *getFullname()* is invoked as a function of the *obj.prop* object. So, the context refers to the latter and the function returns the fullname property of this object. On the contrary, when *getFullname()* is assigned to the test variable, the context refers to the global object (*window*). This happens because *test* is implicitly set as a property of the global object. For this reason, the function returns the value of a property called *fullname* of *window*, which in this case is the one the code set in the first line of the snippet.

#Question 5

The issue can be fixed by forcing the context of the function using either the *call()* or the *apply()* function. In the code below I’ll use call() but in this case apply() would produce the same result:

```javascript
console.log(test.call(obj.prop));
```
