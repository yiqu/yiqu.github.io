---
layout: post
title: More than Just Log
excerpt: "It has been a long time since I posted my last blog, now..."
tags:
  - hyde
  - blogging
---

### The Console object
As as a front-end developer, one of the most used debugging tool we use is the <code>console</code> object.
The <code>console</code> object provides access to the browser's debugging console (e.g. the Web Console in Firefox). 
The specifics of how it works varies from browser to browser, but there is a de facto set of features that are typically 
provided. 

### log
The most used command from <code>console</code> is probably <code>console.log()</code>. The <code>.log()</code> commands will
simple produce an output to your browser's web console. You can access your web console by pressing the f12 key while having
your browser opened. The <code>.log()</code> command is great, and I use it everyday at my job. But there are couple more cool
commands that could help you.


### table
The <code>.table()</code> command takes an array of object, and outputs the data in a tabular format.

The following code:
<pre>
// an array of strings

console.table(["apples", "oranges", "bananas"]);
</pre>

will produce:

![alt text](https://mdn.mozillademos.org/files/8567/console-table-array.png "result table")


### time
The most used command from <code>console</code> is probably <code>console.log()</code>. The <code>.log()</code> commands will
simple produce an output to your browser's web console. You can access your web console by pressing the f12 key while having
your browser opened. The <code>.log()</code> command is great, and I use it everyday at my job. But there are couple more cool
commands that could help you.
