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
```
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
```
var a = ‘Hello’;
function b() {
}
console.log(window.a);
console.log(window.b);
```

### Creation and Hoisting

The following code examples return different results:

```
var a = ‘hello’;
function b() {
  console.log(‘in b’);
}

b(); // 'in b'
console.log(a); // 'hello'
```

```
b(); // 'in b'
console.log(a); // undefined ... you probably were expecting an error!

var a = ‘hello’;
function b() {
  console.log(‘in b’);
}
```

```
b(); // 'in b'
console.log(a); // ReferenceError: a is not defined

// var a = ‘ciccio’;  <== removed declaration of a
function b() {
  console.log(‘in b’);
}
```
> **SYNTAX:** function declaration
> ```
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

```
// hoisting set a placeholder for 'a' with value undefined and place the whole 'b' function in memory
b(); // 'in b'
console.log(a); // undefined ... now it should be clear why!

var a = ‘hello’; // only now a value is explicitely assigned to 'a'
function b() {
  console.log(‘in b’);
}
```
   
