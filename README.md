JS under the hood
=================

Some notes I took while trying to understand how JS works under the hood.

The snippet of code can be easily executed here: http://jsbin.com/?js,console

Table of contents
=================
* [Executions contexts, Lexical environments, scopes](https://github.com/barbasa/JSUnderTheHood/EXECUTION_CONTEXTS.md#executions-contexts-lexical-environments-scopes)
  * [Syntax parser](https://github.com/barbasa/JSUnderTheHood/EXECUTION_CONTEXTS.md#syntax-parser)
  * [Lexical environment](https://github.com/barbasa/JSUnderTheHood/EXECUTION_CONTEXTS.md#lexical-environment)
  * [Execution context](https://github.com/barbasa/JSUnderTheHood/EXECUTION_CONTEXTS.md#execution-context)
  * [Creation and hoisting](https://github.com/barbasa/JSUnderTheHood/EXECUTION_CONTEXTS.md#creation-and-hoisting)
  * [Functions invocation and execution stack](https://github.com/barbasa/JSUnderTheHood/EXECUTION_CONTEXTS.md#function-invocation-and-executions-stack)
  * [Variable scope](https://github.com/barbasa/JSUnderTheHood/EXECUTION_CONTEXTS.md#variable-scope)
  * [Scope chain](https://github.com/barbasa/JSUnderTheHood/EXECUTION_CONTEXTS.md#scope-chain)
  * [Handling asynchronicity](https://github.com/barbasa/JSUnderTheHood/EXECUTION_CONTEXTS.md#handling-asynchronicity)
* [Types and operator](https://github.com/barbasa/JSUnderTheHood#types-and-operators)
  * [Primitive types](https://github.com/barbasa/JSUnderTheHood#primitive-types)
  * [Precedence and associativity](https://github.com/barbasa/JSUnderTheHood#precedence-and-associativity)
  * [Coercion](https://github.com/barbasa/JSUnderTheHood#coercion)
  * [Comparison Operators](https://github.com/barbasa/JSUnderTheHood#comparison-operators)
  * [Particular cases of coersion](https://github.com/barbasa/JSUnderTheHood#particular-cases-of-coersion)
* [Objects and functions](https://github.com/barbasa/JSUnderTheHood#objects-and-functions)
  * [Key value pairs: Object](https://github.com/barbasa/JSUnderTheHood#key-value-pairs-objects)
  * [Functions](https://github.com/barbasa/JSUnderTheHood#functions)
  * [By reference Vs by value](https://github.com/barbasa/JSUnderTheHood#by-reference-vs-by-value)
  * ["This"](https://github.com/barbasa/JSUnderTheHood#this)
