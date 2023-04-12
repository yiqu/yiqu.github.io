---
layout: post
title: Explain Javascript Closure To Me Like I am 5
readTime: 5
tags:
  - closure
  - javascript
---

What is a Javascript closure?
<br />
According to MDN: <em>A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function's scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.</em>
<!--more-->

### ELI5

Einstein once said "If you can't explain it to a six-year old, you really don't understand it yourself.”

So how does Closures really work in Javascript? Consider the following example:

<em>Once there was a parent named Mary:</em>
```javascript
var parent = function() {
 var name = "Mary"; 
}
```
Every time you call it, the local variable "name" is created and given the name "Mary". And every time the function exits the variable is lost and the name is forgotten.

<br />

<em>Mary had a child:</em>
```javascript
var parent = function() {
  var name = "Mary";
  var child = function(childName) {
    // i am the child of Mary
  }
}
```
The child here is also a private variable of its parent function, it would also die when the parent ends, and the secrets would die with them.

<br />

<em>So for the child to not "die" with the parent, it has to leave the parent:</em>
```javascript
var parent = function() {
  var name = "Mary";
  var child = function(childName) {
    return "My name is " + childName  +", child of " + name; 
  }
  return child; // child leaves the parent ->
}
var child = parent(); // < - and here it is outside 
```
Calling the ```parent``` function will return a function that can be called with a argument.

<br />

<em>Mary passes from old age. But the memory of her is not lost and her child will always remember her name and other secrets they shared during their time together.</em>
```javascript
child("Alice") => "My name is Alice, child of Mary"
```
And now, even though the parent is "no longer running" and dead, we can still access the variable values through the function it returned.

Notice logging the child with ```console.log(child)``` will not expose the name "Mary", it's only when you invoke the child function that allows Mary to be revealed. 

<em>The end.</em>


### Summary

A closure is a pairing of:

<ul>
<li>A function and</li>
<li>A reference to that function's outer scope (lexical environment)</li>
</ul>

A lexical environment is part of every execution context (stack frame) and is a map between identifiers (i.e. local variable names) and values.

Closures are useful whenever you need a private state associated with a function. This is a very common scenario - and remember: JavaScript did not have a class syntax until 2015, and it still does not have a private field syntax. Closures meet this need.

Every function in JavaScript maintains a reference to its outer lexical environment. This reference is used to configure the execution context created when a function is invoked. This reference enables code inside the function to "see" variables declared outside the function, regardless of when and where the function is called.

If a function was called by a function, which in turn was called by another function, then a chain of references to outer lexical environments is created, and the chain is called the scope chain.


