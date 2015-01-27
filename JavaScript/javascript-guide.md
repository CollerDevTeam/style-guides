Declarations with var: Always
Decision:
When you fail to specify var, the variable gets placed in the global context, potentially clobbering existing values. Also, if there's no declaration, it's hard to tell in what scope a variable lives (e.g., it could be in the Document or Window just as easily as in the local scope). So always declare with var.


Constants - Use NAMES_LIKE_THIS for constant values.

=======================



Semicolons

link ▽ Always use semicolons.
Relying on implicit insertion can cause subtle, hard to debug problems. Don't do it. You're better than that.

There are a couple places where missing semicolons are particularly dangerous:

// 1.
MyClass.prototype.myMethod = function() {
  return 42;
}  // No semicolon here.

(function() {
  // Some initialization code wrapped in a function to create a scope for locals.
})();


var x = {
  'i': 1,
  'j': 2
}  // No semicolon here.

// 2.  Trying to do one thing on Internet Explorer and another on Firefox.
// I know you'd never write code like this, but throw me a bone.
[ffVersion, ieVersion][isIE]();


var THINGS_TO_EAT = [apples, oysters, sprayOnCheese]  // No semicolon here.

// 3. conditional execution a la bash
-1 == resultOfOperation() || die();
So what happens?

JavaScript error - first the function returning 42 is called with the second function as a parameter, then the number 42 is "called" resulting in an error.
You will most likely get a 'no such property in undefined' error at runtime as it tries to call x[ffVersion, ieVersion][isIE]().
die is always called since the array minus 1 is NaN which is never equal to anything (not even if resultOfOperation() returns NaN) and THINGS_TO_EAT gets assigned the result of die().
Why?

JavaScript requires statements to end with a semicolon, except when it thinks it can safely infer their existence. In each of these examples, a function declaration or object or array literal is used inside a statement. The closing brackets are not enough to signal the end of the statement. Javascript never ends a statement if the next token is an infix or bracket operator.

This has really surprised people, so make sure your assignments end with semicolons.

Clarification: Semicolons and functions

Semicolons should be included at the end of function expressions, but not at the end of function declarations. The distinction is best illustrated with an example:

var foo = function() {
  return true;
};  // semicolon here.

function foo() {
  return true;
}  // no semicolon here.



=========================


Wrapper objects for primitive types

link ▽No
There's no reason to use wrapper objects for primitive types, plus they're dangerous:

var x = new Boolean(false);
if (x) {
  alert('hi');  // Shows 'hi'.
}
Don't do it!

However type casting is fine.

var x = Boolean(0);
if (x) {
  alert('hi');  // This will never be alerted.
}
typeof Boolean(0) == 'boolean';
typeof new Boolean(0) == 'object';
This is very useful for casting things to number, string and boolean.

===============================


Method and property definitions

link ▽/** @constructor */ function SomeConstructor() { this.someProperty = 1; } Foo.prototype.someMethod = function() { ... };
While there are several ways to attach methods and properties to an object created via "new", the preferred style for methods is:

Foo.prototype.bar = function() {
  /* ... */
};
The preferred style for other properties is to initialize the field in the constructor:

/** @constructor */
function Foo() {
  this.bar = value;
}



==================================


delete

link ▽Prefer this.foo = null.
 Foo.prototype.dispose = function() {
  this.property_ = null;
};
Instead of:

Foo.prototype.dispose = function() {
  delete this.property_;
};
In modern JavaScript engines, changing the number of properties on an object is much slower than reassigning the values. The delete keyword should be avoided except when it is necessary to remove a property from an object's iterated list of keys, or to change the result of if (key in obj).


===================================



eval() - don't use


==================================


with() {}

link ▽No - don't use


===================================


use that for this


===============================


for-in loop

link ▽ Only for iterating over keys in an object/map/hash
for-in loops are often incorrectly used to loop over the elements in an Array. This is however very error prone because it does not loop from 0 to length - 1 but over all the present keys in the object and its prototype chain. Here are a few cases where it fails:

function printArray(arr) {
  for (var key in arr) {
    print(arr[key]);
  }
}

printArray([0,1,2,3]);  // This works.

var a = new Array(10);
printArray(a);  // This is wrong.

a = document.getElementsByTagName('*');
printArray(a);  // This is wrong.

a = [0,1,2,3];
a.buhu = 'wine';
printArray(a);  // This is wrong again.

a = new Array;
a[3] = 3;
printArray(a);  // This is wrong again.
Always use normal for loops when using arrays.

function printArray(arr) {
  var l = arr.length;
  for (var i = 0; i < l; i++) {
    print(arr[i]);
  }
}

or  .forEach



======================================



Multiline string literals

link ▽No
Do not do this:

var myString = 'A rather long string of English text, an error message \
                actually that just keeps going and going -- an error \
                message to make the Energizer bunny blush (right through \
                those Schwarzenegger shades)! Where was I? Oh yes, \
                you\'ve got an error and all the extraneous whitespace is \
                just gravy.  Have a nice day.';
The whitespace at the beginning of each line can't be safely stripped at compile time; whitespace after the slash will result in tricky errors; and while most script engines support this, it is not part of ECMAScript.

Use string concatenation instead:

var myString = 'A rather long string of English text, an error message ' +
    'actually that just keeps going and going -- an error ' +
    'message to make the Energizer bunny blush (right through ' +
    'those Schwarzenegger shades)! Where was I? Oh yes, ' +
    'you\'ve got an error and all the extraneous whitespace is ' +
    'just gravy.  Have a nice day.';


========================

Array and Object literals

link ▽Yes
Use Array and Object literals instead of Array and Object constructors.

Array constructors are error-prone due to their arguments.

// Length is 3.
var a1 = new Array(x1, x2, x3);

// Length is 2.
var a2 = new Array(x1, x2);

// If x1 is a number and it is a natural number the length will be x1.
// If x1 is a number but not a natural number this will throw an exception.
// Otherwise the array will have one element with x1 as its value.
var a3 = new Array(x1);

// Length is 0.
var a4 = new Array();
Because of this, if someone changes the code to pass 1 argument instead of 2 arguments, the array might not have the expected length.

To avoid these kinds of weird cases, always use the more readable array literal.

var a = [x1, x2, x3];
var a2 = [x1, x2];
var a3 = [x1];
var a4 = [];
Object constructors don't have the same problems, but for readability and consistency object literals should be used.

var o = new Object();

var o2 = new Object();
o2.a = 0;
o2.b = 1;
o2.c = 2;
o2['strange key'] = 3;
Should be written as:

var o = {};

var o2 = {
  a: 0,
  b: 1,
  c: 2,
  'strange key': 3
};


===================================


Naming

link ▽
In general, use functionNamesLikeThis, variableNamesLikeThis, ClassNamesLikeThis, EnumNamesLikeThis, methodNamesLikeThis, CONSTANT_VALUES_LIKE_THIS, foo.namespaceNamesLikeThis.bar, and filenameslikethis.js.

Properties and methods

Private properties and methods should be named with a trailing underscore.
Protected properties and methods should be named without a trailing underscore (like public ones).
For more information on private and protected, read the section on visibility.

Method and function parameter

Optional function arguments start with opt_.

Functions that take a variable number of arguments should have the last argument named var_args. You may not refer to var_args in the code; use the arguments array.

Optional and variable arguments can also be specified in @param annotations. Although either convention is acceptable to the compiler, using both together is preferred.

Getters and Setters

EcmaScript 5 getters and setters for properties are discouraged. However, if they are used, then getters must not change observable state.

/**
 * WRONG -- Do NOT do this.
 */
var foo = { get next() { return this.nextId++; } };
Accessor functions

Getters and setters methods for properties are not required. However, if they are used, then getters must be named getFoo() and setters must be named setFoo(value). (For boolean getters, isFoo() is also acceptable, and often sounds more natural.)

Namespaces

JavaScript has no inherent packaging or namespacing support.

Global name conflicts are difficult to debug, and can cause intractable problems when two projects try to integrate. In order to make it possible to share common JavaScript code, we've adopted conventions to prevent collisions.

Use namespaces for global code

ALWAYS prefix identifiers in the global scope with a unique pseudo namespace related to the project or library. If you are working on "Project Sloth", a reasonable pseudo namespace would be sloth.*.

var sloth = {};

sloth.sleep = function() {
  ...
};
Many JavaScript libraries, including the Closure Library and Dojo toolkit give you high-level functions for declaring your namespaces. Be consistent about how you declare your namespaces.

goog.provide('sloth');

sloth.sleep = function() {
  ...
};
Respect namespace ownership

When choosing a child-namespace, make sure that the owners of the parent namespace know what you are doing. If you start a project that creates hats for sloths, make sure that the Sloth team knows that you're using sloth.hats.

Use different namespaces for external code and internal code

"External code" is code that comes from outside your codebase, and is compiled independently. Internal and external names should be kept strictly separate. If you're using an external library that makes things available in foo.hats.*, your internal code should not define all its symbols in foo.hats.*, because it will break if the other team defines new symbols.

foo.require('foo.hats');

/**
 * WRONG -- Do NOT do this.
 * @constructor
 * @extends {foo.hats.RoundHat}
 */
foo.hats.BowlerHat = function() {
};
If you need to define new APIs on an external namespace, then you should explicitly export the public API functions, and only those functions. Your internal code should call the internal APIs by their internal names, for consistency and so that the compiler can optimize them better.

foo.provide('googleyhats.BowlerHat');

foo.require('foo.hats');

/**
 * @constructor
 * @extends {foo.hats.RoundHat}
 */
googleyhats.BowlerHat = function() {
  ...
};

goog.exportSymbol('foo.hats.BowlerHat', googleyhats.BowlerHat);
Alias long type names to improve readability

Use local aliases for fully-qualified types if doing so improves readability. The name of a local alias should match the last part of the type.

/**
 * @constructor
 */
some.long.namespace.MyClass = function() {
};

/**
 * @param {some.long.namespace.MyClass} a
 */
some.long.namespace.MyClass.staticHelper = function(a) {
  ...
};

myapp.main = function() {
  var MyClass = some.long.namespace.MyClass;
  var staticHelper = some.long.namespace.MyClass.staticHelper;
  staticHelper(new MyClass());
};
Do not create local aliases of namespaces. Namespaces should only be aliased using goog.scope.

myapp.main = function() {
  var namespace = some.long.namespace;
  namespace.MyClass.staticHelper(new namespace.MyClass());
};
Avoid accessing properties of an aliased type, unless it is an enum.

/** @enum {string} */
some.long.namespace.Fruit = {
  APPLE: 'a',
  BANANA: 'b'
};

myapp.main = function() {
  var Fruit = some.long.namespace.Fruit;
  switch (fruit) {
    case Fruit.APPLE:
      ...
    case Fruit.BANANA:
      ...
  }
};
myapp.main = function() {
  var MyClass = some.long.namespace.MyClass;
  MyClass.staticHelper(null);
};
Never create aliases in the global scope. Use them only in function blocks.

Filenames

Filenames should be all lowercase in order to avoid confusion on case-sensitive platforms. Filenames should end in .js, and should contain no punctuation except for - or _ (prefer - to _).


========================================


Custom toString() methods

link ▽ Must always succeed without side effects.
You can control how your objects string-ify themselves by defining a custom toString() method. This is fine, but you need to ensure that your method (1) always succeeds and (2) does not have side-effects. If your method doesn't meet these criteria, it's very easy to run into serious problems. For example, if toString() calls a method that does an assert, assert might try to output the name of the object in which it failed, which of course requires calling toString().


=======================================


Explicit scope

link ▽Always
Always use explicit scope - doing so increases portability and clarity. For example, don't rely on window being in the scope chain. You might want to use your function in another application for which window is not the content window.

use global with closure, for example


========================================



Code formatting

link ▽Expand for more information.
We follow the C++ formatting rules in spirit, with the following additional clarifications.

Curly Braces

Because of implicit semicolon insertion, always start your curly braces on the same line as whatever they're opening. For example:

if (something) {
  // ...
} else {
  // ...
}
Array and Object Initializers

Single-line array and object initializers are allowed when they fit on a line:

var arr = [1, 2, 3];  // No space after [ or before ].
var obj = {a: 1, b: 2, c: 3};  // No space after { or before }.
Multiline array initializers and object initializers are indented 2 spaces, with the braces on their own line, just like blocks.

// Object initializer.
var inset = {
  top: 10,
  right: 20,
  bottom: 15,
  left: 12
};

// Array initializer.
this.rows_ = [
  '"Slartibartfast" <fjordmaster@magrathea.com>',
  '"Zaphod Beeblebrox" <theprez@universe.gov>',
  '"Ford Prefect" <ford@theguide.com>',
  '"Arthur Dent" <has.no.tea@gmail.com>',
  '"Marvin the Paranoid Android" <marv@googlemail.com>',
  'the.mice@magrathea.com'
];

// Used in a method call.
goog.dom.createDom(goog.dom.TagName.DIV, {
  id: 'foo',
  className: 'some-css-class',
  style: 'display:none'
}, 'Hello, world!');
Long identifiers or values present problems for aligned initialization lists, so always prefer non-aligned initialization. For example:

CORRECT_Object.prototype = {
  a: 0,
  b: 1,
  lengthyName: 2
};
Not like this:

WRONG_Object.prototype = {
  a          : 0,
  b          : 1,
  lengthyName: 2
};
Function Arguments

When possible, all function arguments should be listed on the same line. If doing so would exceed the 80-column limit, the arguments must be line-wrapped in a readable way. To save space, you may wrap as close to 80 as possible, or put each argument on its own line to enhance readability. The indentation may be either four spaces, or aligned to the parenthesis. Below are the most common patterns for argument wrapping:

// Four-space, wrap at 80.  Works with very long function names, survives
// renaming without reindenting, low on space.
goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
    veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
  // ...
};

// Four-space, one argument per line.  Works with long function names,
// survives renaming, and emphasizes each argument.
goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
    veryDescriptiveArgumentNumberOne,
    veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy,
    artichokeDescriptorAdapterIterator) {
  // ...
};

// Parenthesis-aligned indentation, wrap at 80.  Visually groups arguments,
// low on space.
function foo(veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
             tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
  // ...
}

// Parenthesis-aligned, one argument per line.  Emphasizes each
// individual argument.
function bar(veryDescriptiveArgumentNumberOne,
             veryDescriptiveArgumentTwo,
             tableModelEventHandlerProxy,
             artichokeDescriptorAdapterIterator) {
  // ...
}
When the function call is itself indented, you're free to start the 4-space indent relative to the beginning of the original statement or relative to the beginning of the current function call. The following are all acceptable indentation styles.

if (veryLongFunctionNameA(
        veryLongArgumentName) ||
    veryLongFunctionNameB(
    veryLongArgumentName)) {
  veryLongFunctionNameC(veryLongFunctionNameD(
      veryLongFunctioNameE(
          veryLongFunctionNameF)));
}
Passing Anonymous Functions

When declaring an anonymous function in the list of arguments for a function call, the body of the function is indented two spaces from the left edge of the statement, or two spaces from the left edge of the function keyword. This is to make the body of the anonymous function easier to read (i.e. not be all squished up into the right half of the screen).

prefix.something.reallyLongFunctionName('whatever', function(a1, a2) {
  if (a1.equals(a2)) {
    someOtherLongFunctionName(a1);
  } else {
    andNowForSomethingCompletelyDifferent(a2.parrot);
  }
});

var names = prefix.something.myExcellentMapFunction(
    verboselyNamedCollectionOfItems,
    function(item) {
      return item.name;
    });
Aliasing with goog.scope

goog.scope may be used to shorten references to namespaced symbols in programs using the Closure Library.

Only one goog.scope invocation may be added per file. Always place it in the global scope.

The opening goog.scope(function() { invocation must be preceded by exactly one blank line and follow any goog.provide statements, goog.require statements, or top-level comments. The invocation must be closed on the last line in the file. Append // goog.scope to the closing statement of the scope. Separate the comment from the semicolon by two spaces.

Similar to C++ namespaces, do not indent under goog.scope declarations. Instead, continue from the 0 column.

Only alias names that will not be re-assigned to another object (e.g., most constructors, enums, and namespaces). Do not do this (see below for how to alias a constructor):

goog.scope(function() {
var Button = goog.ui.Button;

Button = function() { ... };
...
Names must be the same as the last property of the global that they are aliasing.

goog.provide('my.module.SomeType');

goog.require('goog.dom');
goog.require('goog.ui.Button');

goog.scope(function() {
var Button = goog.ui.Button;
var dom = goog.dom;

// Alias new types after the constructor declaration.
my.module.SomeType = function() { ... };
var SomeType = my.module.SomeType;

// Declare methods on the prototype as usual:
SomeType.prototype.findButton = function() {
  // Button as aliased above.
  this.button = new Button(dom.getElement('my-button'));
};
...
});  // goog.scope
Indenting wrapped lines

Except for array literals, object literals, and anonymous functions, all wrapped lines should be indented either left-aligned to a sibling expression above, or four spaces (not two spaces) deeper than a parent expression (where "sibling" and "parent" refer to parenthesis nesting level).

someWonderfulHtml = '' +
                    getEvenMoreHtml(someReallyInterestingValues, moreValues,
                                    evenMoreParams, 'a duck', true, 72,
                                    slightlyMoreMonkeys(0xfff)) +
                    '';

thisIsAVeryLongVariableName =
    hereIsAnEvenLongerOtherFunctionNameThatWillNotFitOnPrevLine();

thisIsAVeryLongVariableName = siblingOne + siblingTwo + siblingThree +
    siblingFour + siblingFive + siblingSix + siblingSeven +
    moreSiblingExpressions + allAtTheSameIndentationLevel;

thisIsAVeryLongVariableName = operandOne + operandTwo + operandThree +
    operandFour + operandFive * (
        aNestedChildExpression + shouldBeIndentedMore);

someValue = this.foo(
    shortArg,
    'Some really long string arg - this is a pretty common case, actually.',
    shorty2,
    this.bar());

if (searchableCollection(allYourStuff).contains(theStuffYouWant) &&
    !ambientNotification.isActive() && (client.isAmbientSupported() ||
                                        client.alwaysTryAmbientAnyways())) {
  ambientNotification.activate();
}
Blank lines

Use newlines to group logically related pieces of code. For example:

doSomethingTo(x);
doSomethingElseTo(x);
andThen(x);

nowDoSomethingWith(y);

andNowWith(z);
Binary and Ternary Operators

Always put the operator on the preceding line. Otherwise, line breaks and indentation follow the same rules as in other Google style guides. This operator placement was initially agreed upon out of concerns about automatic semicolon insertion. In fact, semicolon insertion cannot happen before a binary operator, but new code should stick to this style for consistency.

var x = a ? b : c;  // All on one line if it will fit.

// Indentation +4 is OK.
var y = a ?
    longButSimpleOperandB : longButSimpleOperandC;

// Indenting to the line position of the first operand is also OK.
var z = a ?
        moreComplicatedB :
        moreComplicatedC;
This includes the dot operator.

var x = foo.bar().
    doSomething().
    doSomethingElse();
    
    
    
    
===============================================




Strings

link ▽Prefer ' over "
For consistency single-quotes (') are preferred to double-quotes ("). This is helpful when creating strings that include HTML:

var msg = 'This is some HTML';

=====================================


Tips and Tricks

link ▽JavaScript tidbits
True and False Boolean Expressions

The following are all false in boolean expressions:

null
undefined
'' the empty string
0 the number
But be careful, because these are all true:

'0' the string
[] the empty array
{} the empty object
This means that instead of this:

while (x != null) {
you can write this shorter code (as long as you don't expect x to be 0, or the empty string, or false):

while (x) {
And if you want to check a string to see if it is null or empty, you could do this:

if (y != null && y != '') {
But this is shorter and nicer:

if (y) {
Caution: There are many unintuitive things about boolean expressions. Here are some of them:

Boolean('0') == true
'0' != true
0 != null
0 == []
0 == false
Boolean(null) == false
null != true
null != false
Boolean(undefined) == false
undefined != true
undefined != false
Boolean([]) == true
[] != true
[] == false
Boolean({}) == true
{} != true
{} != false
Conditional (Ternary) Operator (?:)

Instead of this:

if (val) {
  return foo();
} else {
  return bar();
}
you can write this:

return val ? foo() : bar();
The ternary conditional is also useful when generating HTML:

var html = '<input type="checkbox"' +
    (isChecked ? ' checked' : '') +
    (isEnabled ? '' : ' disabled') +
    ' name="foo">';
&& and ||

These binary boolean operators are short-circuited, and evaluate to the last evaluated term.

"||" has been called the 'default' operator, because instead of writing this:

/** @param {*=} opt_win */
function foo(opt_win) {
  var win;
  if (opt_win) {
    win = opt_win;
  } else {
    win = window;
  }
  // ...
}
you can write this:

/** @param {*=} opt_win */
function foo(opt_win) {
  var win = opt_win || window;
  // ...
}
"&&" is also useful for shortening code. For instance, instead of this:

if (node) {
  if (node.kids) {
    if (node.kids[index]) {
      foo(node.kids[index]);
    }
  }
}
you could do this:

if (node && node.kids && node.kids[index]) {
  foo(node.kids[index]);
}
or this:

var kid = node && node.kids && node.kids[index];
if (kid) {
  foo(kid);
}
However, this is going a little too far:

node && node.kids && node.kids[index] && foo(node.kids[index]);
Iterating over Node Lists

Node lists are often implemented as node iterators with a filter. This means that getting a property like length is O(n), and iterating over the list by re-checking the length will be O(n^2).

var paragraphs = document.getElementsByTagName('p');
for (var i = 0; i < paragraphs.length; i++) {
  doSomething(paragraphs[i]);
}
It is better to do this instead:

var paragraphs = document.getElementsByTagName('p');
for (var i = 0, paragraph; paragraph = paragraphs[i]; i++) {
  doSomething(paragraph);
}
This works well for all collections and arrays as long as the array does not contain things that are treated as boolean false.

In cases where you are iterating over the childNodes you can also use the firstChild and nextSibling properties.

var parentNode = document.getElementById('foo');
for (var child = parentNode.firstChild; child; child = child.nextSibling) {
  doSomething(child);
}



================================================


Keeping to JavaScript common conventions

We should aim to keep to common conventions used with JavaScript. Casing & strings are two examples which I have seen throughout the code where we should change to be more in line with these conventions. Casing should be camel case (not pascal case), and the only exception to this should be constructor functions which should be pascal case. Strings should ideally be surrounded with single quotes (‘my string’, rather than “my string”).

Currently, the majority of JSON which is communicated between the server and client code is pascal case – this causes an issue when trying to convert these into javascript objects which are defined with camel case. In the Market Intelligence project, I’ve set up the API controllers to automatically convert outgoing objects into camel case json – this should be the format which we use going forward, always dealing with camel case json between the server & client.

Make use of strict mode

                Please ensure that we are making use of strict mode throughout our javascript, by placing ‘use strict’; at the top of all outer functions.  We should use this function form, rather than placing the statement at the top of script files.
