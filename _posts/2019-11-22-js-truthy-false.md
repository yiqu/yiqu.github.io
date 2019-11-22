---
layout: post
title: JavaScript Truthy and Falsy's
readTime: 2
tags:
  - javascript
  - coding
---

There are truthy and falsy values in Javascript. Using them could shorten your conditional checks and more.


#### Falsy

* strings with the length of 0
* the number 0
* <code>false</code>
* <code>undefined</code>
* <code>null</code>
* <code>NaN</code>


#### Truthy

* empty arrays
* empty objects
* Everything else

<br/>

#### Bonus

The <code>!!</code> operator is a useful operator to convert values in javascript to Boolean values. If the expression is a truthy value, it return true; otherwise it returns false.

```javascript
!!1         // returns true
!!undefined //returns false
!![]        //returns true
```
