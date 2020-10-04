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
When a variable or function that has not been defined is used then an error
is thrown. In example 3.5 the variable foo has not been defined so the 
following error will be thrown.

"Uncaught ReferenceError: foo is not defined"

3.5
``` javascript
console.log(foo)
```

It is important to know the difference between 'not defined' and undefined 
because they can lead to very common errors and knowing exactly what is the 
cause will result in a swift resolution.

## Primitive Data Types
Javascript has a total of 7 Javascript primitive data types. The Null primitive
is sort of special and could be considered to be in a seperate category. The 
null primitive returns 'object' from the typeof operator. This is due to every
object being derived from null.
1. String
2. Number
3. Boolean
4. Symbol
5. Undefined
6. BigInt
7. Null

## Structural Data Types
There are 3 structural data types in javascript. In order to check what 
structural data type an object is use the 'instanceof' operator.
1. Object
2. Function
3. Array

## Execution Stack
When some javascript code is run, a global execution context is created. The 
global execution context is put onto an execution stack. The code is parsed and
executed line by line. When a function is invoked a new execution context is 
created and put ontop of the execution stack. The execution context on the very
top of the stack is the execution context that is currently running or
executing its code line by line.

4.1
``` javascript
function foo(){
   bar()
   console.log("foo")
}
function bar(){
   console.log("bar")
}
foo()
```
4.2.1
**Execution Stack** 
|                          | 
|                          | 
| global execution context | 

4.2.2
**Execution Stack** 
|                          | 
| foo()                    | 
| global execution context | 

4.2.3
**Execution Stack** 
| bar()                    | 
| foo()                    | 
| global execution context | 

4.2.4
**Execution Stack** 
|                          | 
| foo()                    | 
| global execution context | 
 
4.2.5
**Execution Stack** 
|                          | 
|                          | 
| global execution context | 

As the code in example 4.1 is run the execution stack changes as per 4.2.1,
4.2.2, 4.2.3, 4.2.4 and 4.2.5. At first the execution stack is empty with only
the global execution context as per 4.2.1. When the foo function is invoked 
then an execution context is created for the foo() function as per 4.2.2. The
foo function then begins to execute and the bar() function is invoked creating
yet another execution context that is pushed onto the execution stack as 
reflected in 4.2.3. The bar function then executes printing "bar" to console.
Once the bar() function finishes the arduous task of printing "bar" to the
console, the bar() execution context will then be popped off the execution 
stack as per 4.2.4 and then the foo() function will finish and be popped of as
per 4.2.5. 


## Variable Environment
There is a new variable environment inside every execution context. When a
function is invoked a new execution context is created and put on the execution
stack. This new execution context has a variable environment that stores all 
the variables with in the function. This information is important to know when
understanding closures.

## Scope
A scope spans the entire execution context. If a variable is defined within a 
global execution context the variable can be accessed from anywhere within the
file because the scope spans the entire execution context.

When a function is executed a new execution context is created. This execution
context also has its own scope. If a function is defined and invoked within the
global execution context. Variables within the function will not be accessible 
in the global execution context.
In example 4.3.1 the function foo() creates its own execution context. The 
variable a is stored within the global execution context while the variable b 
is stored within the execution context of the function foo().

4.3.1
``` javascript
var a = "a"
var foo(){
   var b = "b"
}
```

## Scope Chain
Every execution context has a reference to the outer environment. If a variable
cannot be found within the execution context then the execution context that 
the outer environment reference is pointing to is checked. 

4.4.1
``` javascript
var a = 'a'
function foo(){
   var b = 'b'
   console.log(a)
}
```
Example 4.4.1 illustrates how the scope chain gives function foo() access to 
the variable 'a'. As the variable 'a' is not within the scope of foo() the 
reference to the outer environment is used to check for the variable 'a' in the
outer environment. The outer environment in this case is the global execution
context.

4.4.2
``` javascript
var a = 'a'
function foo(){
   var b = 'b'
   function bar(){
      console.log(b)
      console.log(a)
   }
}
```
In example 4.4.2 the outer reference for function bar() is pointing to the 
execution context for the foo() funciton. This means that the variables within
the foo() function can also be accessed within the bar() function. The outer 
reference of the foo function is pointing to the global execution context which
stores the variable 'a'. These outer references can form a chain. This is known
as the scope chain because it brings all of the variables into scope from the 
outer reference. This is why function bar() has access to the variables 'a' and
'b' which are in the execution context for function foo() and the global
execution context respectively.

4.4.3
``` javascript
var a = 'a'
function foo(){
   var b = 'b'
}
function bar(){
   console.log(b)
}
```
In example 4.4.3 the outer environment reference for both function foo() and 
function bar() is pointing to the global execution context. This means that 
neither function foo() or the function bar() have access to each others 
variables. So function bar() will not be able to log the variable 'b' to the 
console. Consequently an is not defined error will be thrown when trying to 
execute the bar() function.

## Closure
Functions form closures. A closure is a function along with references to the
variables in its  outer environment. So a closure gives the function access to 
variables that are part of an outer function or global variables depending on 
where the function was defined.

Closures are commonly used by defining a function inside another function and 
returning the inner function from the outer function. When the outer function
is invoked an execution context is created and put on the execution stack.
Normally after a function has finished running it will be popped of the 
execution stack but with closures the variables are still kept in memory and 
the inner function still has access to them. 

##Object
Objects are collections of name value pairs. An object can store primitives, 
other object and function within the name/value pairs. When an object stores a 
function it is refered to as a method. When an object stores primitives and 
other objects they are refered to as properties. 

Objects have references to memory locaiton of the properties and functions 
stored within them.

## Object Literal
It is very common to see objects created in javascript with the object literal
notation. The object literal notaion is simply a key/value pair enclosed within
curly brackets '{}'. Unlike JSON, object literal notation does not have the key
surrounded with quotes.

The following is an example of an object literal notation. An object is a 
collection of key value pairs separated by a comma. Name being the key and Mary
being the value.
``` javascript
{
   name: "Mary",
   age: 20,
   comment: "hello"
}
```
It is possible to store objects in variables and retrieve their values using
the dot operator. The following example prints the persons name to the console.
``` javascript
var person = {
   name: "Mary",
   age: 20,
   comment: "hello"
}
console.log(person.name)
```

# 1st Class Functions
Functions are objects. First class functions means that everything that can be 
done with other types in javascript can be done with functions. It is possible
to store functions in variables, to pass functions around as parameters to 
other functions or even create functions on the fly.


## Spread Operator
It is possible to use the spread operator to increase the number of elements in
an array. It can be used to a new element to either the start or end of the 
array.

The following adds the number 4 to the end of the array.
``` javascript
var arr = [1,2,3]
arr = [...arr, 4]
```
It is also possible to add the element to the start of the array as seen below:
``` javascript
var arr = [1,2,3]
arr = [4,...arr]
```
Functions are objects and because functions are objects it is possible to 
attach primitive name/value pairs, objects and other functions. The function 
object has a couple hidden properties. They are the name and code property. The
name property is optional as it can anonymous. The code property stores the 
lines of code that make up the function. The code property can be invoked. Once
invoked an execution context will be created and put on the execution stack.

## Arrays
Arrays in javascript can be created with the square brackets like many other 
programming languages. In javascript however, it is possible to store multiple
data types in the array as seen in the example below.
``` javascript
var arr = [1,2,"three",{text:"four"}]
```
