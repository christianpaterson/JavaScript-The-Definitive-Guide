<h2>JavaScript: The Definitive Guide . . .</h2>

Here goes...


Here are my notes from 05/06/23:

<em><b>Chapter 3: Types, Values, and Variables</b></em>

JavaScript supports an object-oriented programming style. Loosely, this means that rather than having globally defined functions to operate on values of various types, the types themselves define methods for working with values.

To sort the elements of an array a, for example, we don't pass a to a sort () function. Instead, we invoke the sort () method of a:

a.sort(); === The object-oriented version of sort(a).

Technically, it is only JavaScript objects that have methods. But numbers, strings, boolean, and symbol values behave as if they have methods.

<b>3.3 Strings</b>

If using emojis, or any character represented by 32 bits (surrogate pair). In ES6 strings are iterable, and if you use the for/of loop or ... operator with a string, it will iterate the actual characters of the string, not the 16-bit values.

3.3.1
'two\nlines'

"one\
long\
line"

`the newline character at the end of this line
 is included literally in this string`

JS: ‘single-quotes’
HTML: “double-quotes” 

3.3.3
str.length
substring === slice

 includes, replace
“string”.repeat(5)

charAt, charCodeAt
indexOf(“l”, 3)
•Position of first l at or after 3
lastIndexOf(“a”, 13);
•Second parameter starting position for search. 

Strings are immutable. replace() and toUpperCase() return new strings. 

Strings can also be treated like read-only arrays, and you can access individual characters (16-bit values) from a string using square brackets instead of the charAt() method. 

indexOf () and search() accept the same arguments (parameters), and return the same value.

The two methods are NOT equal.
These are the differences:
• The search() method cannot take a second start position argument.
• The indexOf() method cannot take powerful search values (regular expressions).

<b>3.3.5 Pattern Matching</b>

Global, case-insensitive match:
let string = “The rain in SPAIN stays mainly in the plain”;
string.match(/ain/gi);

Does equal:    Null == undefined     true
Does not strictly equal:   Null !== undefined     true
x !== x ONLY EVER TRUE W NaN
There is also isNaN()

3.6
let sym = Symbol(“propertyname”);

This function never returns the same value twice, even when called with the same argument. This means that if you call Symbol() to obtain a Symbol value, you can safely use that value as a property name to add a new property to an object and do not need to worry that you might be overwriting an existing property with the same name.

Similarly, if you use symbolic property names and do not share those symbols, you can be confident that other modules of code in your program will not accidentally overwrite your properties.

In practice, Symbols serve as a language extension mechanism. When ES6 introduced the for/of loop and iterable objects, it needed to define a standard method that classes could implement to make themselves iterable. But standardizing any particular string name for this iterator method would have broken existing code, so a symbolic name was used instead.

As we'll see in Chapter 12, Symbol.iterator is a Symbol value that can be used as a method name to make an object iterable.

The Symbol() function takes an optional string argument and returns a unique Symbol value. If you supply a string argument, that string will be included in the output of the Symbol's toString() method. Note, however, that calling Symbol() twice with the same string produces two completely different Symbol values.

let s = Symbol("sym_x");
s.toString()   => "Symbol(sym_x)"

toString() is the only interesting method of Symbol instances. There are two other Symbol-related functions you should know about, however. Sometimes when using Symbols, you want to keep them private to your own code so you have a guarantee that your properties will never conflict with properties used by other code. Other times, however, you might want to define a Symbol value and share it widely with other code. This would be the case, for example, if you were defining some kind of extension that you wanted other code to be able to participate in, as with the Symbol. iterator mechanism described earlier.

To serve this latter use case, JavaScript defines a global Symbol registry. The Symbol.for() function takes a string argument and returns a Symbol value that is associated with the string you pass. If no Symbol is already associated with that string, then a new one is created and returned; otherwise, the already existing Symbol is returned. That is, the Symbol.for() function is completely different than the Symbol() function:

Symbol() never returns the same value twice, but Symbol.for() always returns the same value when called with the same string. The string passed to Symbol.for() appears in the output of toString() for the returned Symbol, and it can also be retrieved by calling Symbol.keyFor() on the returned Symbol.

let s = Symbol.for("shared");
let t = Symbol.for("shared");
s === t    => true
s.toString()    => "Symbol(shared)"
Symbol. keyFor(t)    => "shared"



Notes from 05/07/23:

3.8
Objects (and arrays) are mutable. They are only equal if they refer to the same underlying object. Primitives are immutable, and are the same if their values are the same. Str === string if all letters are the same. 

let a = [];
let b = a;
a === b => true

In ES6, copy arrays with let c = Array.from(b);
(faster than with a loop)
a===c => false 

<b>3.9.2 Type Conversions</b>

Number ("3"); or +x
String(false); or x + “”
Boolean([]); or !!x

let n = 17;
let binary = "0b" + n.toString(2); binary == "0b10001"
let octal = "0o" + n.toString(8); octal == "0o21"
let hex = "0x" + n.toString(16); hex == "0x11"

3.9.3
Object to primitive conversion algorithms:
• The prefer-string algorithm first tries the toString() method. If the method is defined and returns a primitive value, then JavaScript uses that primitive value (even if it is not a string!). If toString() does not exist or if it returns an object, then JavaScript tries the valueOf() method. If that method exists and returns a primitive value, then JavaScript uses that value. Otherwise, the conversion fails with a TypeError.
• The prefer-number algorithm works like the prefer-string algorithm, except that it tries value0f() first and toString() second.
• The no-preference algorithm depends on the class of the object being converted. If the object is a Date object, then JavaScript uses the prefer-string algorithm. For any other object, JavaScript uses the prefer-number algorithm.

Number ([]) => 0: this is unexpected!
Number ([99])  => 99: really?

The object-to-number conversion first converts the object to a primitive using the prefer-number algorithm, then converts the resulting primitive value to a number.
The prefer-number algorithm tries value0f() first and then falls back on tostring().

But the Array class inherits the default valueOf() method, which does not return a primitive value. So when we try to convert an array to a number, we end up invoking the toString() method of the array. Empty arrays convert to the empty string. And the empty string converts to the number 0. An array with a single element converts to the same string that that one element does. If an array contains a single number, that number is converted to a string, and then back to a number.

3.10.1
let x = 2, y = x*x;
Initializers can use previously declared variables that were declared within the same statement.

Destructuring Assignment
let [x,y] = [1,2];   => x=1, y=2
[x,y] = [y,x];        => swap values



Notes from 05/08/23

<em><b>Chapter 4: Expressions and Operators</b></em>

<b>4.4.1 Conditional property access</b>

expression?.identifier
It is “short-circuiting”
let a = {b:null}
a.b?.c.d    => undefined  (d will not get evaluated)

<b>4.5.1 Conditional invocation expressions</b>

f?.(x++)   => if f is null, x is not incremented 

4.7.5
Only ternary, assignment, exponentiate, and unitary operators are Right (right to left) Associative.

Most commonly used JavaScript operators have Left to Right Associativity
(the order in whch multiple operations of the same precedence are 
performed). However, the ternary operator, assignment, exponentiating, and 
unary operators have Right to Left Associativity.

4.8.1
1 + {}    =>    "1[object Object]": obj->str, concat
true + true    => 2: addition after boolean-to-number
2 + null      => 2: addition after null converts to 0
2 + undefined    => NaN: addition after undefined converts to NaN

let data = {} or []
“x” in data
“0” in data

d instanceOf Date  => true

?:
?? First-defined
&& || idiomatic use



Notes from 05/09/23

<em><b>Chapter 5: Statements</b></em>

5.1-5.3
Expression Statements, Compound and Empty Statements, and Conditionals

More Statements!!

5.4-5.5 Loops and Jumps
5.6-5.7 with, debugger, “use strict”, function, class, import and export



<em><b>Chapter 6: Objects</b></em>

<b>6.3.2 Inheritance</b>

The fact that inheritance occurs when querying properties but not when setting them is a key feature of JavaScript because it allows us to selectively override inherited properties.

If o is not extensible, then no new properties can be defined on it.

In operator.

For/in runs for each enumerable property.
Enumerable literally just means a for/in loop returns it. That’s its only definition. For/in loop is meant to iterate all enumerable properties, both owned and inherited. You can use Object.keys() to get only owned properties. Note, however, that a property will not be enumerated if a property by that same name has already been enumerated, or even if a non-enumerable property by the same name has already been considered.

One reason to assign properties from one object into another is when you have an object that defines default values for many properties and you want to copy those default properties into another object if a property by that name does not already exist in that object. Using Object.assign() naively will not do what you want:


Object.assign(o, defaults); // overwrites everything in o with defaults

Instead, what you can do is to create a new object, copy the defaults into it, and then override those defaults with the properties in o:

o = Object.assign ({}, defaults, o);


<em><b>Chapter 7: Arrays</b></em>

If it’s iterable, a for/of loop works (strings and sets included)

let a = Array.from(arraylike function() {});
move efficient than new; map;

The following function searches an array for a specified value and returns an array of all matching indexes. This demonstrates how the second argument to indexof() car be used to find matches beyond the first.

function findall(a, x) {

    let results = [],
    len = a. length,
    pos = 0;

    while(pos < len) {
        pos = a. indexOf (x, pos);
        if (pos === -1)  break;
        results.push (pos);
        pos = pos + 1;
    }
    return results;
}

<b>7.9 Arraylike Objects</b>
DOM text nodes have a numeric length property and may need to be excluded with an additional o.nodeType !== 3 test.


<em><b>Chapter 8: Functions</b></em>

Each function invocation has an invocation context, the value of the this keyword. 

Function property of object? Method

Functions designed to initialize a newly created object are called constructors.



Functions are objects. You can assign functions to variables and pass them to other functions, for example. You can set properties on them and even invoke methods on them.

Function definitions can be nested within other functions, and they have access to any variables that are in scope where they are defined. This means that JavaScript functions are closures, and it enables important and powerful programming techniques.

Note that function expressions are sometimes defined and immediately invoked:
let f = (function(x) {return x*x + x -x/2;}(12));
console.log(f);  => 150



Note that the function name is optional for functions defined as expressions, and most of the preceding function expressions we've shown omit it. A function declaration actually declares a variable and assigns a function object to it. A function expres-sion, on the other hand, does not declare a variable: it is up to you to assign the newly defined function object to a constant or variable if you are going to need to refer to it multiple times. It is a good practice to use const with function expressions so you don't accidentally overwrite your functions by assigning new values.

When you use the declaration form, the function objects are created before the code that contains them starts to run, and the definitions are hoisted so that you can call these functions from code that appears above the definition statement. This is not true for functions defined as expressions, however: these functions do not exist until the expression that defines them are actually evaluated. Furthermore, in order to invoke a function, you must be able to refer to it, and you can't refer to a function defined as an expression until it is assigned to a variable.


Arrow functions differ from functions defined in other ways in a critical way: they inherit the value of the this keyword from the environment in which they are defined rather than defining their own invocation context, as functions defined in other ways do. This is an important and very useful feature of arrow functions, and we'll return to it again later in this chapter. Arrow functions also differ from other functions in that they do not have a prototype property, which means that they cannot be used as constructor functions for new classes.


For function invocation in non-strict mode, the invocation context (the this value) is the global object. In strict mode, however, the invocation context is undefined. Note that functions defined using the arrow syntax behave differently: they always inherit the this value that is in effect where they are defined. 

Functions written to be invoked as functions (and not as methods) do not typically use the this keyword at all. 

The keyword can be used, however, to determine whether strict mode is in effect:
const strict = (function() { return I this; ]());

<b>8.2.2 Method Invocation (very interesting!)</b>

When methods return objects, you can use the return value of one method invocation as part of a subsequent invocation. This results in a series (or "chain") of method invocations as a single expression. When working with Promise-based asynchronous operations, for example, it is common to write code structured like this:

// Run three asynchronous operations in sequence, handling errors


doStepOne().then(doStepTwo).then(doStepThree).catch(handleErrors);


When you write a method that does not have a return value of its own, consider having the method return this. If you do this consistently throughout your API, you will enable a style of programming known as method chaining in which an object can be named once and then multiple methods can be invoked on it:

new Square().×(100).y(100).size(50).
outline("red").fill("blue").draw();


This is not scoped the way variables are and except for arrow functions nested functions do not inherent the this value of the containing function. 

If a nested function is invoked as a method, its this value is the object it was invoked on.

If a nested function (that is not an arrow function) is invoked as a function, then its this value will be either the global object (non-strict mode) or undefined (strict mode). It is a common mistake to assume that a nested function defined within a method and invoked as a function can use this to obtain the invocation context of the method.

<b>8.7.1</b>
Length specifies Arity - the number of parameters it declares in its parameter list, which is usually the number of arguments that the function expects. If it has a rest parameter, that parameter is not counted for the purposes of the length property. 



In computer science, a closure is a function that has an environment of its own. In this environment, there is at least one bound variable (a name that has a value, such as a number). The closure's environment keeps the bound variables in memory between uses of the closure.

A function defined inside of and returned by an enclosing function retains access to its lexical scope and can therefore read and write the variables defined inside the outer function. Functions used in this way are called closures, and this is a technique that is worth understanding.


<em><b>Chapter 9: Classes</b></em>

"Objects in JavaScript can be thought of a a unique set of properties, different from every other object.  It is often useful, however, to define a <em>class</em> of objects that share certain properties. Members, or instances, of a class have their own properties to hold or define their state, but they also have methods that define their behavior. These methods are defined by the class and shared by all instances."

JavaScript uses prototypal inheritance. If two objects inherit properties (usually methods) from the same prototype, they are said to be instances of the same class!

I don't anticipate using classes too much with JavaScript! But I have used them extensively in Java and it is interesting to the ways in which they are applicable and useful in JavaScript as well :)

I know I will continue to use JS classes when creating Date objects, making XMLHttpRequests, and creating custom classes or objects.


<em><b>Chapter 15: JavaScript in Web Browsers</b></em>

15.5.1 pg 460 (top) Basically, the document expands to fill the whole viewport if it’s smaller. 


15.12.1 Storage Events
Whenever the data stored in localStorage changes, the browser triggers a "storage" event on any other Window objects to which that data is visible (but not on the window that made the change). If a browser has two tabs open to pages with the same origin, and one of those pages stores a value in localStorage, the other tab will receive a "storage" event.

Register a handler for "storage" events either by setting window.onstorage or by calling window.addEventListener() with event type "storage".


17.4 If you are trying out someone else's javascript project, then one of the first things you will often do after downloading their code is to type pm install. This reads the dependencies listed in the package JSON file and downloads the third-party packages that the project needs and saves them in a node_modules/ directory.

You can also type npm install <package-name> to install a particular package to your project's node_modules/ directory:
$ npm install express

In addition to installing the named package, pm also makes a record of the dependency in the package.json file for the project. Recording dependencies in this way is what allows others to install those dependencies simply by typing pm install.