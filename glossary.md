# Glossary

## Block scope
Any variable defined within a block is only available within that block

## Function Scope
Any variable defined in the function, is available to the whole function

## idempotent
A type of operation that can be applied multiple times but still yields the same initial result. ie multiple put operations to a url should still result in only 1 resource existing

## Immutable object
an object whose state cannot be modified after creation
	* useful for multithreaded applications -> data is not changed by other threads
	* in pure functional languages all objects are immutable

## Lexical Scoping
Describes how variable names are resolved in inner functions. The inner function scope will also contain the scope of the outer (parent) function
* also known as static scoping

## Scope
The visiblity or accessibility of variables from different parts of the program

## Type coercion
mostly found in interpreted or dynamically typed languages, invovles converting a value to another type to perform a comparison or operation on it
