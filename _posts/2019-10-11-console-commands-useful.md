---
layout: post
title: More Than Just Log
excerpt: "As as a front-end developer, one of the most used debugging tool we use is the console object. The console object   provides access to..."
tags:
  - commands
  - programming
  - console
---

### The Console object
As as a front-end developer, one of the most used debugging tool we use is the <code>console</code> object.
The <code>console</code> object provides access to the browser's debugging console (e.g. the Web Console in Firefox). 
The specifics of how it works varies from browser to browser, but there is a de facto set of features that are typically 
provided. 

### .log()
The most used command from <code>console</code> is probably <code>console.log()</code>. The <code>.log()</code> commands will
simple produce an output to your browser's web console. You can access your web console by pressing the f12 key while having
your browser opened. The <code>.log()</code> command is great, and I use it everyday at my job. But there are couple more cool
commands that could help you.

### .table()
The <code>.table()</code> command takes an array of object, and outputs the data in a tabular format.

The following code:
<pre>
// an array of strings

console.table(["apples", "oranges", "bananas"]);
</pre>

will produce:

![table result img](https://mdn.mozillademos.org/files/8567/console-table-array.png "result table")

The <code>.table()</code> command can also take in an object like so:

<pre>// an object whose properties are strings

function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

var me = new Person("Kevin", "Qu");

console.table(me);
</pre>

and produce the following output:

![table result img](https://mdn.mozillademos.org/files/8559/console-table-simple-object.png "result table")


### .time()
Another useful command that is not often used is the <code>.time()</code> command. The time command takes a optional
param of a label, and starts a timer under that label. Up to 10,000 simultaneous timers can run on a given page.

When you run <code>console.time("foo")</code>, this timer can now be used to track how long an operation takes. When you call <code>console.timeEnd("foo")</code>, the browser will output the time, in milliseconds, that elapsed since the timer was started. If you want to log the time anytime during the operation, you can do so by calling <code>console.timeLog("foo")</code>. Overall it is a pretty useful command for timing operations in your code.

<pre>
// start a timer
console.time("me");

// 5 seconds later, check the time passed
console.timeLog("me"); //output: me: - 5000

// wait 1 second

// end my timer
console.timeEnd("me"); // outputs: me: 6000ms - timer ended

</pre>

### .group()
The <code>.group()</code> command creates a new inline group in the Web Console log. It indents following 
console messages by an additional level, until <code>console.groupEnd()</code> is called. This command is 
mostly a visual helper tool.

<pre>
console.log("This is the outer level");
console.group();
console.log("Level 2");
console.group();
console.log("Level 3");
console.warn("More of level 3");
console.groupEnd();
console.log("Back to level 2");
console.groupEnd();
console.log("Back to the outer level");
</pre>

will produce:

![table result img](https://mdn.mozillademos.org/files/3604/nesting.png "result table")

There you have it! Now you have learned a bit more about the web <code>console</code> object, I hope you take advantage of these commands in your programming career.
