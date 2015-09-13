Objects and functions
=====================

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

Objects can also contain other objects as values:

```javascript
var currentPerson = {
  name: 'smith',
  address: {
   street: 'Rome Road',
   postcode: 'W450RE'
  }
};
```

Another way of creating an object is using the *Computed Member Access*

```javascript
var currentPerson = new Object();
currentPerson["name"] = "Ciccio";
currentPerson["surname"] = "Pasticcio";
```

The nice thing about the *Computed Member Access* is that it is possible to dynamically change the value we want to access, for example:

```javascript
var currentKey = "name";
console.log(currentPerson[currentKey]);
```

> *SYNTAX*: objects
> ```javascript
> var myObject = {
>   key1: primitive_value, // "property"
>   key2: object, // "propery"
>   key3: function // "method"
>   ....
>};
> myObject.key1   // returns key1 value
> myObject.key2   // returns object
> myObject.key3() // execute function
>
> var myOtherObject = new Object();
> myOtherObject.name = "Carlo";
>
> var myOtherOtherObject = new Object();
> myOtherOtherObject["name"] = "Gino";

Functions
---------
* Functions are "first class functions", you can do with them what you can do with other types (assign them to variable, pass them, etc).
* Functions are special types of objects, they have all the features of an object plus other properties:
 * **Name**: optionally can have a name. It can also be anonymous.
 * **Code**: the code written to implement the function. The *code* property is invocable via the **()** operator.
 
The implications are for example these:

```javascript
function person() {
 console.log('Yo yo');
}

person.name = 'Luigi'; // Not common in other languages!!!

console.log(person); // returns the code!
```

Since functions are objects you can do thing like:

```javascript
var doStuff = function() {
 console.log('Yo yo');
}

doStuff(); // prints 'Yo yo'
```

What would happen if we would have run the code this way instead ?

```javascript
hello();

function hello() {
 console.log('Hello!');
}

doStuff();

var doStuff = function() {
 console.log('Yo yo');
}

```
We would get an *Uncaught TypeError: undefined is not a function*! This happens because of the hoisting.The *doStuff* variable is initialised to *undefined*, hence the error we get when we try to invoke the function. It is like if we are trying to do this: *undefined()*.

Another implication of a function being an object is the following:

```javascript

function doStuff(param) {
 param();
}

doStuff(function() {
 console.log('Yo yo');
});

```
What would have happened if in *doStuff* we would have put: *console.log(param)* instead of *param()*?

By reference Vs by value
------------------------
When assigning variables to primitive values a new copy of the value is created:

![alt text](https://github.com/barbasa/JSUnderTheHood/blob/master/assets/byValue.png  "by value")

When assigning variables to object all the variables will point to the same object:

![alt text](https://github.com/barbasa/JSUnderTheHood/blob/master/assets/byRef.png  "by reference")

The implication of this is that we could end up in situation like:

```javascript

var a = { name: 'ciccio' };

function changeStuff(obj) {
 obj.name = 'pasticcio';
}
changeStuff(a);

console.log(a);
```
"This"
------
We have seen before the object *This* is created with the execution context and it points to the global object.

Let's see some example:
```javascript
function a(){
 console.log(this);
 this.newVar = 'Ciccio';
}

var b = function(){
 console.log(this);
}

a();
console.log(newVar);
b();
```
In all the places *this* points to the global object.

In this other case:

```javascript
var c = {
 name: 'Here is C',
 doStuff: function() {
  console.log(this);
 } 
};
c.doStuff();
```
*This* will point to the object the method is sitting inside of.

Let's see a further example:

```javascript
var c = {
 name: 'Here is C',
 doStuff: function() {
  this.name = 'Updated C';
  console.log(this);
  
  var setname = function(newname) {
   this.name = newname;
  }
  setname('Re-updated C');
  console.log(this);
 } 
};
c.doStuff();

```
This is the strangest case...we would expect to see *setname* to update the value of *this* internal to the object...but this is not true. The way the JS Engine works it updated the global object!?!?!

To avoid this issue we can do like that:

```javascript
var c = {
 name: 'Here is C',
 doStuff: function() {
  self = this;
  self.name = 'Updated C';
  console.log(self);
  
  var setname = function(newname) {
   self.name = newname;
  }
  setname('Re-updated C');
  console.log(self);
 } 
};
c.doStuff();

```

This is a common pattern that you will.

Arrays
------
Arrays is a collection. In JS they are zero based.

> *SYNTNAX*: array declaration
> var arr1 = new Array();
> var arr2 = []; //array literal syntax

Arrays can contain different type of elements:

```javascript
var arr = [
  1,
  false,
  {
    name: 'gino',
    surname: 'strada'
  },
  function(name) {
    console.log('hello' + name);
  },
  "YO YO"
];

arr[3](arr[2].name);
```

Arguments
---------
The *arguments* keyword contains the arguments passed to a JS function. It looks like an array but it is not a proper JS array, check [here](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/arguments) why.

```javascript
function doStuff(name,surname,lang) {
  
  if(arguments.length === 0) {
    console.log('Missing parameters!');
    return;
  }
  
  //...
  
}

doStuff('gino', 'strada'); // arguments will be ['gino', 'strada']
```
Immediately Invoked Function Expressions (IIFEs)
------------------------------------------------
Functions can be invoked at the moment they are created:

```javascript
var doStuff = function(name) {
  console.log(name);
}('gino');
```

If you want a function statement to be treated as a function expression, you can do this in JS:

```javascript
(function(name) {
  return 'Hey' + name; 
});
```
This is a way of "cheating" the intepreter, because everything between parethesys has to be an expression, it cannot be a statement.

You can create a function expression on the fly and invoking it. It is a classical example of IIFE and it is a widely used pattern:

```javascript
var a = 'ciccio';

(function(name){
  console.log('Hi' + name);
}(a)); //Hi ciccio

(function(name){
  console.log('Hello' + name);
})(a); //Hello ciccio

```
Notice that the previous 2 examples are slighlty different but they both work.

The great advantage of IIFEs is that they are really useful to write safe code. The variables created inside it don't belong to the global execution context. This way is possible to avoid collision between variables called in the same way by different libraries, ex:

```javascript
var a = 'Mr';

(function(name){
  var a = 'Miss';
  console.log('Hi' + a + name);
}('Carla')); //Hi Miss Carls
```

If you want to have access to the global object inside the IIFE you can pass it as parameter:

```javascript
(function(global, name){
  var a = 'Miss';
  console.log('Hi' + a + name);
}(window, 'Carla')); //Hi Miss Carls

```
