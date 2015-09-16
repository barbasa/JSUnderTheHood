JS under the hood
=================

Some notes I took while trying to understand how JS works under the hood.

The snippet of code can be easily executed here: http://jsbin.com/?js,console

Table of contents
=================
* [Executions contexts, Lexical environments, scopes](https://github.com/barbasa/JSUnderTheHood/blob/master//EXECUTION_CONTEXTS.md#executions-contexts-lexical-environments-scopes)
  * [Syntax parser](https://github.com/barbasa/JSUnderTheHood/blob/master//EXECUTION_CONTEXTS.md#syntax-parser)
  * [Lexical environment](https://github.com/barbasa/JSUnderTheHood/blob/master//EXECUTION_CONTEXTS.md#lexical-environment)
  * [Execution context](https://github.com/barbasa/JSUnderTheHood/blob/master//EXECUTION_CONTEXTS.md#execution-context)
  * [Creation and hoisting](https://github.com/barbasa/JSUnderTheHood/blob/master//EXECUTION_CONTEXTS.md#creation-and-hoisting)
  * [Functions invocation and execution stack](https://github.com/barbasa/JSUnderTheHood/blob/master//EXECUTION_CONTEXTS.md#function-invocation-and-executions-stack)
  * [Variable scope](https://github.com/barbasa/JSUnderTheHood/blob/master//EXECUTION_CONTEXTS.md#variable-scope)
  * [Scope chain](https://github.com/barbasa/JSUnderTheHood/blob/master//EXECUTION_CONTEXTS.md#scope-chain)
  * [Handling asynchronicity](https://github.com/barbasa/JSUnderTheHood/blob/master//EXECUTION_CONTEXTS.md#handling-asynchronicity)
* [Types and operator](https://github.com/barbasa/JSUnderTheHood/blob/master//TYPES_AND_OPERATORS.md#types-and-operators)
  * [Primitive types](https://github.com/barbasa/JSUnderTheHood/blob/master//TYPES_AND_OPERATORS.md#primitive-types)
  * [Precedence and associativity](https://github.com/barbasa/JSUnderTheHood/blob/master//TYPES_AND_OPERATORS.md#precedence-and-associativity)
  * [Coercion](https://github.com/barbasa/JSUnderTheHood/blob/master//TYPES_AND_OPERATORS.md#coercion)
  * [Comparison Operators](https://github.com/barbasa/JSUnderTheHood/blob/master//TYPES_AND_OPERATORS.md#comparison-operators)
  * [Particular cases of coersion](https://github.com/barbasa/JSUnderTheHood/blob/master//TYPES_AND_OPERATORS.md#particular-cases-of-coersion)
* [Objects and functions](https://github.com/barbasa/JSUnderTheHood/blob/master//OBJECTS_AND_FUNCTIONS.md#objects-and-functions)
  * [Key value pairs: Object](https://github.com/barbasa/JSUnderTheHood/blob/master//OBJECTS_AND_FUNCTIONS.md#key-value-pairs-objects)
  * [Functions](https://github.com/barbasa/JSUnderTheHood/blob/master//OBJECTS_AND_FUNCTIONS.md#functions)
  * [By reference Vs by value](https://github.com/barbasa/JSUnderTheHood/blob/master//OBJECTS_AND_FUNCTIONS.md#by-reference-vs-by-value)
  * ["This"](https://github.com/barbasa/JSUnderTheHood/blob/master//OBJECTS_AND_FUNCTIONS.md#this)
  * [Arrays](https://github.com/barbasa/JSUnderTheHood/blob/master/OBJECTS_AND_FUNCTIONS.md#arrays)
  * [Parameters](https://github.com/barbasa/JSUnderTheHood/blob/master/OBJECTS_AND_FUNCTIONS.md#parameters)
  * [IIFEs](https://github.com/barbasa/JSUnderTheHood/blob/master/OBJECTS_AND_FUNCTIONS.md#immediately-invoked-function-expressions-iifes)
  * [Closure](https://github.com/barbasa/JSUnderTheHood/blob/master/OBJECTS_AND_FUNCTIONS.md#closure)
  * [Closures and Callbacks](https://github.com/barbasa/JSUnderTheHood/blob/master/OBJECTS_AND_FUNCTIONS.md#closures-and-callbacks)
  
