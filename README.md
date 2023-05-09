<h2>JavaScript: The Definitive Guide . . .</h2>

Here goes...

Here are my notes from 05/06/23:

<em><b>Chapter 3: Types, Values, and Variables</em></b>

JavaScript supports an object-oriented programming style. Loosely, this means that rather than having globally defined functions to operate on values of various types, the types themselves define methods for working with values.

To sort the elements of an array a, for example, we don't pass a to a sort () function. Instead, we invoke the sort () method of a:

a.sort(); === The object-oriented version of sort(a).

Technically, it is only JavaScript objects that have methods. But numbers, strings, boolean, and symbol values behave as if they have methods.


<em>3.3 Strings</em>
If using emojis, or any character represented by 32 bits (surrogate pair). In ES6 strings are iterable, and if you use the for/of loop or ... operator with a string, it will iterate the actual characters of the string, not the 16-bit values.

<em>3.3.1</em>
'two\nlines'

"one\
long\
line"

`the newline character at the end of this line
 is included literally in this string`

JS: ‘single-quotes’
HTML: “double-quotes” 


<em>3.3.3</em>

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


<em>3.3.5 Pattern Matching</em>

Global, case-insensitive match:
let string = “The rain in SPAIN stays mainly in the plain”;
string.match(/ain/gi);

Does equal:    Null == undefined     true
Does not strictly equal:   Null !== undefined     true
x !== x ONLY EVER TRUE W NaN
There is also isNaN()


<em>3.6</em>
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


3.9.2 Type Conversions

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

Chapter 4: Expressions and Operators


4.4.1 Conditional property access
expression?.identifier
It is “short-circuiting”
let a = {b:null}
a.b?.c.d    => undefined  (d will not get evaluated)

4.5.1 Conditional invocation expressions
f?.(x++)   => if f is null, x is not incremented 

4.7
Only ternary, assignment, exponentiate, and unitary operators are Right (right to left) Associative. 

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



4.7

Most commonly used JavaScript operators have Left to Right Associativity (the order in whch multiple operations of the same precedence are performed). However, the ternary operator, assignment, exponentiating, and unary operators have Right to Left Associativity.