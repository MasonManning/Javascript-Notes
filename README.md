## Javascript Notes

Syntax parsers convert code to computer instructions.
It is possible to do extra things while parsing the code to something the computer can understand, such as hoisting.

Lexical Envionment refers to the location of code having meaning. This meaning
is derived by differences in the structure when the code is parsed into a form
that the computer can understand. 

An example would be if there are two separate pieces of code. They both have a
variable and they both have a function. The first pieces of code has the 
variable declared before the function is declared. The second pieces of code 
has the variable declared with in the function. When these two pieces of code
are parsed into a form that the computer is able to understand they will each
have a different structure. This is fundamentally what the lexical environment 
is referring to. The location code being of importance to how the computer 
understands code.

1.1
var a = 0
function foo(){
}

1.2
function bar(){
   var a = 0
}

Execution Context
An execution context can be thought of as a way to manage executable code. So
the code currently being run by the javascript engine is within an execution
context that is currently being executed. Each lexical environment has its own
execution context which runs the code within its own specific lexical 
environment.

Global Execution Context
The global execution context creates the global object and the 'this' variable.
The 'this' variable is set to the value of the global object.
The base and global execution context are the same thing. They are the 
execution context that encompass all other execution contexts. 

"One context to rule them all, one context to find them, one context to bring 
them all, and in the darkness bind them." 

In the browswer the global object is the window object and the 'this' variable
that is created in the base/global execution context points to the window
object. So essentially in the browser there is a window object that has a 
variable called 'this' that points to the window object.

## Hoisting
Hoisting is performed by the parser before the code is executed. 
During the construction of the execution context the code is parsed and memory
for the variables and functions is allocated. Functions and variables are 
treated differently. Functions are saved in memory in their entirety while 
variables are initialized to undefined.

2.1

function foo(){
   console.log("bar")
}
foo()

2.2
```javascript
foo()
function foo() {
   console.log("bar"
}
```

Example 2.1 would print "bar" to the console, however if the function is
executed before the function is declared as seen in example 2.2 then it will 
still print "bar" to the console. This is because when the execution context is
created the code is parsed and memory is allocated for the function foo. The
function exists in memory even though the function definition appears after the
function is executed. This process is called hoisting. It appears as though the
function declaration is hoisted or lifted to the top of the file because the 
function can be run before it is defined.


## Undefined
Undefined is a primitive data type in javascript. This value should never be 
assigned manually and is reserved, only to be assigned to variables that have 
just been declared. What is the difference between declared and defined?

3.1
var foo

3.2
var foo = 'bar'

In example 3.1 the variable foo is being declared. A value has yet to be 
assigned to the variable foo. Thus it is only declared. If a variable has been
assigned then it would be considered to be defined. In example 3.2 the variable
foo has been defined because the variable foo has been given the value of 
'bar'. As mentioned in the previous section under Hoisting, when the javascript
parser finds a variable definition or declaration, the variable is initialized 
to undefined.

3.3
``` javascript
console.log(foo)
var foo = 'bar'
```

In example 3.3 'undefined' will be printed to the console. This is because when
the parser find the definition of foo, the parser raises or hoists the 
declaration of foo to the top of the file and then defines foo as undefined. As
can be seen in example 3.4 foo has been defined as undefined. The code is 
executed sequentially. So when foo is printed to the console it has yet to be 
defined to 'bar' but it still exists and has been defined.

3.4
``` javascript
var foo = undefined
console.log(foo)
foo = 'bar'
```

## Not Defined 
Error message "Uncaught ReferenceError: a is not defined"
