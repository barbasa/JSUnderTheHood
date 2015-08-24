JS under the hood
=================

Some notes I took while trying to understand how JS works under the hood.

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
