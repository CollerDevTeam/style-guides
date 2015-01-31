### Always declare variables using var

When declaring new variables, always use the var keyword.

*Why?*: When you fail to specify var, the variable gets placed in the global context, potentially clobbering existing values.

*Why?*: If there's no declaration, it's hard to tell in what scope a variable lives (e.g., it could be in the Document or Window just as easily as in the local scope).

Not Recommended:
  ```javascript
  myNewVariable = 15;
  ```
  
Recommended:
  ```javascript
  var myNewVariable = 15;
  ```

### Use standard casing

Use camel casing (not pascal case) for identifiers such as variables and functions. The only exception to this is for constructor functions, which should always be in pascal case.

*Why?*: Following these typical JavaScript conventions allows for new code to have a similar style to existing code, and also to third-party code.

*Why?*: Maintaining a difference in the naming of constuctor functions as opposed to other functions allows the caller to identify which type it is.

Not Recommended:
  ```javascript
  var Name = 'Joe';

  function SimpleFunction() {
  }

  function constructorFunction() {
  }
  ```
  
Recommended:
  ```javascript
  var name = 'Joe';

  function simpleFunction() {
  }

  function ConstructorFunction() {
  }
  ```

### Strings

Use single quotes to surround strings.

*Why?*: Following this typical JavaScript convention allows for new code to have a similar style to existing code, and also to third-party code.

*Why?*: Using single quotes allows for html strings to be constructed more easily, as html uses double-quotation marks.

Not Recommended:
  ```javascript
  var myString = "hello";
  var myHtml = "<input id=\"myDiv\" />";
  ```
  
Recommended:
  ```javascript
  var myString = 'hello';
  var myHtml = '<input id="myDiv" />';
  ```

### Spaces Around Operators

Always put spaces around operators ( = + / * ), and after commas.

*Why?*: Adding the extra spacing allows for better readability.

Not Recommended:
  ```javascript
  var sum=8+9;

  addNewValue(sum,91);
  ```
  
Recommended:
  ```javascript
  var sum = 8 + 9;
  
  addNewValue(sum, 91);
  ```



### Code Indentation

Always use 4 spaces for indentation of code blocks.

*Why?*: Using spaces ensures that the code will look the same in every editor.

*Why?*: 4 spaces is the standard which is used elsewhere in our code, and therefore keeps consistancy.

Not Recommended:
  ```javascript
  function () {
    function () {
      readLine();
    }
  }
  ```
  
Recommended:
  ```javascript
  function () {
      function () {
          readLine();
      }
  }
  ```


### Semicolons

Always use semicolons, and don't rely on the ASI feature in JavaScript.

*Why?*: Relying on implicit insertion can cause subtle, hard to debug problems.

*Why?*: Adding semicolons shows intention, reducing ambiguity for other developers.

Not Recommended:
  ```javascript
  var color = 'yellow'

  runParser(data)

  var myFunc = function () {
  }
  ```
  
Recommended:
  ```javascript
  var color = 'yellow';

  runParser(data);

  var myFunc = function () {
  };
  ```


### Semicolons and functions

Semicolons should be included at the end of function expressions, but not at the end of function declarations.

Not Recommended:
  ```javascript
  var foo = function() { return true; }

  function foo() { return true; };
  ```
  
Recommended:
  ```javascript
  var foo = function() { return true; };

  function foo() { return true; }
  ```


### Wrapper objects for primitive types

Don't use wrapper objects for primitive types.

*Why?*: There is no need to use the wrapper objects, as they give no benefit.

*Why?*: They can cause issues if not properly used. For example, Boolean(false) is actually truthy, which may result in issues with comparisons.

Not Recommended:
  ```javascript
  var x = new Boolean(false);
  ```
  
Recommended:
  ```javascript
  var x = false;
  ```


### Method and property definitions

While there are several ways to attach methods and properties to an object created via "new", the preferred style for methods is by using 'Foo.prototype.bar = function () {}'. All other properties should be initialized in the constructor function where possible.

Recommended:
  ```javascript
  function Person(name, age) {
  	this.name = name;
  	this.age = age;
  	this.isNew = true;
  }

  Person.prototype.giveJob = function () { .. };
  ```


### The delete keyword

Prefer to avoid the use of delete, and instead assign the value of null to the property.

*Why?*: In modern JavaScript engines, changing the number of properties on an object is much slower than reassigning the values.

Not Recommended:
  ```javascript
  delete person.name;
  ```

Recommended:
  ```javascript
  person.name = null;
  ```


### eval and with

Do not use either eval() or with().

*Why?*: These features can cause side effects, and bugs which are hard to debug.

Not Recommended:
  ```javascript
  eval('myvar' + num + ' = 3;');
  ```

Recommended:
  ```javascript
  window['myvar' + num] = 3;
  ```


### Storing 'this'

When there is a need to store the value of 'this', store it in a variable called 'that'.

*Why?*: Using this common convention helps developers quickly understand the intention of the code.

Not Recommended:
  ```javascript
  var _this = this;
  ```

Recommended:
  ```javascript
  var that = this;
  ```


### Multiline string literals

Strings can be declared over multiple lines, but do not escape the newline character to achieve this. Instead, make use of string concatination.

*Why?*: The whitespace at the beginning of each line can't be safely stripped at compile time; whitespace after the slash will result in tricky errors; and while most script engines support this, it is not part of ECMAScript.

Not Recommended:
  ```javascript
  var myString = 'foo \
      bar';
  ```

Recommended:
  ```javascript
  var myString = 'foo ' +
      'bar';
  ```


### Array and Object literals

Use Array and Object literals instead of Array and Object constructors.

*Why?*: Array constructors are error-prone due to their arguments.

*Why?*: Object constructors don't have the same problems as Array constructors, but for readability and consistency object literals should be used

Not Recommended:
  ```javascript
  var arr = new Array(1, 2, 3);

  var obj = new Object();
  o2.a = 0; 
  o2.b = 1;
  o2['strange key'] = 2;
  ```

Recommended:
  ```javascript
  var arr = [1, 2, 3];
  var obj = { a: 0, b: 1, 'strange key': 2 };
  ```


### for-in loops

Only use for iterating over keys in an object/map/hash. for-in loops are often incorrectly used to loop over the elements in an Array, but avoid this.

*Why?*: Using it to itterate over an array is error prone because it does not loop from 0 to length - 1 but over all the present keys in the object and its prototype chain.

*Why?*: Object constructors don't have the same problems as Array constructors, but for readability and consistency object literals should be used

Not Recommended:
  ```javascript
  var arr = [1, 2, 3];
  for (var key in arr) { 
      print(arr[key]); 
  }
  ```

Recommended:
  ```javascript
  var arr = [1, 2, 3], i;
  for (i = 0; i < arr.length; i++) { 
      print(arr[i]); 
  }
  ```


### Custom toString() methods

Any custom toString methods must always succeed without side effects. You can control how your objects string-ify themselves by defining a custom toString() method. This is fine, but you need to ensure that your method (1) always succeeds and (2) does not have side-effects.

*Why?*: If your method doesn't meet these criteria, it's very easy to run into serious problems. For example, if toString() calls a method that does an assert, assert might try to output the name of the object in which it failed, which of course requires calling toString().


### Explicit scope

Always use explicit scope. For example, don't rely on window being in the scope chain. You might want to use your function in another application for which window is not the content window.

*Why?*: Doing so increases portability and clarity.

Recommended:
  ```javascript
  this.global1 = 1;

  (function (globals) {
  	globals.global2 = 2;
  }(this));
  ```


### Strict mode

Make use of strict mode throughout all JavaScript, by placing ‘use strict’; at the top of all outer functions. Use the function form, rather than placing the statement at the top of files.

*Why?*: Strict mode helps us avoid strange behavoiurs and errors caused by the more questionable features of JavaScript.

Recommended:
  ```javascript
  (function () {
  	'use strict';

  	function myFunc() {
  	}

  }());
  ```


### Curly brace positioning

Always start your curly braces on the same line as whatever they're opening.

*Why?*: Because of implicit semicolon insertion, errors can be introduced by placing the opening brace on the next line.

Not Recommended:
  ```javascript
  function ()
  {
  }
  ```

Recommended:
  ```javascript
  function () {
  }
  ```


### Function declarations

When declaring an anonymous function, use one space between the function keyword, and the argument braces. Use no space if the function is not anonymous.

*Why?*: Adding the space makes it very clear at a glance that the function is anonymous.

*Why?*: Following this typical JavaScript convention allows for new code to have a similar style to existing code, and also to third-party code.

Not Recommended:
  ```javascript
  var myAnonFunc = function() {
  };

  var myNamedFunc = function namedFunc () {
  };

  function otherNamedFunc () {
  }
  ```

Recommended:
  ```javascript
  var myAnonFunc = function () {
  };

  var myNamedFunc = function namedFunc() {
  };

  function otherNamedFunc() {
  }
  ```


### Converting to boolean

Use !! to convert to boolean.

*Why?*: Following this typical JavaScript convention allows for new code to have a similar style to existing code, and also to third-party code.

Recommended:
  ```javascript
  var remainingTasks = ['task 1', 'task 2'];
  //other code..
  var hasRemainingTasks = !!remainingTasks;
  ```


### Group var declarations

Group all variable declarations at the top of functions.

*Why?*: JavaScript hoists variable declarations (including functions) to the top of the associated scope. Explicitly writing code as such helps to avoid any errors caused by a misunderstanding of this behaviour. 

Not Recommended:
  ```javascript
  function () {
  	window.red = 3;
  	var myColor = 'blue';

  	for(var i = 0; i < 3; i++) {
  		doSomething(i);
  	}

  	var myString = 'yo!';
  }
  ```

Recommended:
  ```javascript
  function () {
  	var myColor = 'blue',
  	    myString = 'yo!',
  	    i;

  	window.red = 3;

  	for(i = 0; i < 3; i++) {
  		doSomething(i);
  	}
  }
  ```


### Comparison Operators

Never use the less strict comparison operators (== or !=). Always make use of either === or !==.

*Why?*: Side effects can easily be caused by using the non type checking comparison operators. 

Not Recommended:
  ```javascript
  if (a == b) {
  }

  if (c != d) {
  }
  ```

Recommended:
  ```javascript
  if (a === b) {
  }

  if (c !== d) {
  }
  ```



### One line code blocks

When a block is a single line, ensure that it is still surrounded with braces.

*Why?*: Explicitly adding the braces makes it clear to other developers the intention of the code.

*Why?*: Having existing braces allows for another line to be added to the block without potentially causing issues.

Not Recommended:
  ```javascript
  if (canRun())
  	doSomething();
  else
    doSomethingElse();
  ```

Recommended:
  ```javascript
  if (canRun()) {
  	doSomething();
  } else {
    doSomethingElse();
  }
  ```
