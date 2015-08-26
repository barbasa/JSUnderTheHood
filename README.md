JS under the hood
=================

Some notes I took while trying to understand how JS works under the hood.

The snippet of code can be easily executed here: http://jsbin.com/?js,console

Important concept to understand before starting:

Syntax parser
-------------
* Reads your code
* Check if the grammar applies to it
* Translate into binary code

Lexical environment
-------------------
* Where a statement, varaible declaration, etc sist in your code
* The meaning might change depending on the position (will explain later why)
* Ex:
```javascript
  var a = 'Hey hey';
  console.log(a);
  
  // ==> Prints 'Hey hey'
  
  console.log(b);
  var a = 'Hello hello';
  
  // ==> Prints 'undefined'
```

> **SYNTAX:** variable declaration
> ```var a = 'hello';````

Execution context
-----------------
* "Wrapper to help the code which is running"

```
|----------------------------------------------------------------------|
| Execution context (Global)                                           |
|  |--------------| |--------------| |-----------------------------|   |
|  |Global Object | |    'This'    | | Link to outer environment   |   |
|  |--------------| |--------------| |-----------------------------|   |
|                                                                      |
|  |------------------------------------------------|                  |
|  |            Code                                |                  |
|  |------------------------------------------------|                  |
|----------------------------------------------------------------------|
```
* Base execution context is the **Global Execution Context**
  * Accessible from everywhere in the code
* *JS engine* creates:
  * A **Global object**: *Window* in the browser and *Process* in NodeJS
  * A special variable called *this*
    * Check the browser console...Even without any code the JS engine creates **Window** and **this**, which at global level are the same
  * A **Link to the outer environment**:
    * If the code is running in a function os a link to the outer environment
    * If you are in the global environment is *null* 
* Everything not included in a function is Global
  * Running the following code it is possible to see that *a* and *b* belong to the global context, i.e.: *window*
```javascript
var a = ‘Hello’;
function b() {
}
console.log(window.a); // Same as this.a in the global execution context
console.log(this.a);
console.log(window.b); // Same as this.b in the global execution context
console.log(this.b);
```

### Creation and Hoisting

The following code examples return different results:

```javascript
var a = ‘hello’;
function b() {
  console.log(‘in b’);
}

b(); // 'in b'
console.log(a); // 'hello'
```

```javascript
b(); // 'in b'
console.log(a); // undefined ... you probably were expecting an error!

var a = ‘hello’;
function b() {
  console.log(‘in b’);
}
```

```javascript
b(); // 'in b'
console.log(a); // ReferenceError: a is not defined

// var a = ‘ciccio’;  <== removed declaration of a
function b() {
  console.log(‘in b’);
}
```
> **SYNTAX:** function declaration
> ```javascript
> function name() {
> // body here
> }
> ```

Lets try to understand why they return different results. 

* **Hoisting** is often explained as if the JS engine moves code around..this is wrong!
* Before the code gets executed line by line, the JS engine already allocated memory for your functions and variables, this is called **Hoisting**
  * Functions and variable are threated slightly differently
    * Functions: entirely placed in memory space
    * Variables: a placeholder ( *undefined* ) is used for variables
      * undefined = I don’t know what the value is now
  * When the code starts to be executed line by line the variable are present in memory, but they might not have a value assigned to them. Let's revisit one of the previous examples:

```javascript
// hoisting set a placeholder for 'a' with value undefined and place the whole 'b' function in memory
b(); // 'in b'
console.log(a); // undefined ... now it should be clear why!

var a = ‘hello’; // only now a value is explicitely assigned to 'a'
function b() {
  console.log(‘in b’);
}
```
> BEST PRACTICE: usually the JS engine assigns *undefined* to a variable when no values have been assigned to it. It is better not to explicitely assign it to a vaiable, otherwise it will be difficult to understand if the *undefined* value comes from the JS engine or the logic of the code.

To recap the previous section...the *code execution* is composed by 2 phases:
* *creation phase*: creation of the execution context and the hoisting happens
* *execution phase*: code is executed line by line

Function invocation and executions stack
----------------------------------------
Functions are invoked in JS by putting () at the end of the function name.
Every time a function is called a new **execution stack** is created, eg:

```javascript
function b() {
}
function a() {
  b();
}
a();

```
This is the whole stack created:

| Execution stack  |
|---|
| b() execution context     |
| a() execution context     |
| Global execution context  |


They way this happen is the following:
* **Global Creation phase**: Global execution context is created, memory for functions and variable allocated
* **Global Execution phase**: Code in global execution context is executed
* **a() creation phase**: Triggered when a() is invoked. a() execution context is created, memory for functions and variable allocated
* **a() execution phase**: Code in a() execution context is executed
* **b() creation phase**: Triggered when b() is invoked in a(). b() execution context is created, memory for functions and variable allocated
* **b() execution phase**: Code in b() execution context is executed

Variable scope
--------------
Variable scope is where a variable live, where it is visible

```javascript
function b() {
    var myVar;
    console.log(myVar);
}

function a() {
    var myVar = 2;
    console.log(myVar);
    b();
}

var myVar = 1;
console.log(myVar);
a();
```
This is the execution stack created:

| Execution stack  |
|---|
| b() execution context     - **myVar = undefined**|
| a() execution context     - **myVar = 2**|
| Global execution context  - **myVar = 1**|

When executing that code the output we will have is: 1, 2, undefined.

Key value pairs: Objects
------------------------
An object in JS is simply a key value pair, eg:

```javascript
var currentPerson = {
  name: 'smith',
  surname: 'john'
};
console.log(currentPerson);
```
An object can also be created this way:

```javascript
var currentPerson = new Object();
currentPerson.name = 'smith';
currentPerson.surname = 'john';
```

> BEST PRACTICE: The first way of creating an object is called *object literal notation* and it is preferred to the second.

The 2 ways are equivalent. The former is recognised to be quicker and it requires less typing than the latter.
