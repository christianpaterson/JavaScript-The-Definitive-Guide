<h2>JavaScript: The Definitive Guide . . .</h2>

Snapshots are always edited from VSCode and pushed from the command line.

I will download a <em>GitHub project</em> to my local machine.

The steps are:
<ol>
    <li>git clone</li>
    <li>git status</li>
    <li>Edit .gitignore if needed</li>
    <li>git remote -v (to check)</li>
    <li>git add .</li>
    <li>git commit - ''</li>
    <li>git push</li>
</ol>

<h4>By the way . . .</h4>

I am thinking of renaming this file 'JavaScript: The Definitive Guide' Notes. I'm reading the book and will decide this week if I shall make a GitHub repo for my notes or not.

I will gradually transform this document into a repo describing what I have learned from "The Definitive Guide." I am interested to learn how I might do this. For example, how do I even rename a GitHub repository?

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



3.6

Most commonly used JavaScript operators have Left to Right Associativity (the order in whch multiple operations of the same precedence are performed). However, the ternary operator, assignment, exponentiating, and unary operators have Right to Left Associativity.