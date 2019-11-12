---
layout: post
title: Columns Columns Columns
readTime: 8
tags:
  - bootstrap
  - columns
  - UI
  - javascript
  - html
---

If you are a front-end developer, you probably have used, or at least heard of [Bootstrap](https://getbootstrap.com/). 
Bootstrap was originally created at Twitter as a framework to encourage consistency across internal tools. Today, it is a free and open-source CSS framework directed at responsive, mobile-first front-end web development. 

It will take days and weeks to talk about all of Bootstrap's features. In this post, I will focus on one of the most important 
features of Bootstrap, the [Grid System](https://getbootstrap.com/docs/4.0/layout/grid/).

<!--more-->
The <em>three pillars</em> (pun-intended) of Bootstrap Grid System are: 
* **containers**
* **rows**
* **columns**

The <em>three rules</em> of the Bootstrap Grid System are:
* **Rows should be placed inside a Container**.
* **Rows are only used to contain Columns, nothing else**.
* **Columns must be the immediate child of a Row**.

![alt text][container-row-column]

[container-row-column]: https://raw.githubusercontent.com/yiqu/yiqu.github.io/master/assets/images/container-row-column.png "Container Row Column"

The rows & columns always work together, and one should never have one without the other.

<br/>

### Container

The Bootstrap <code>.container</code> class is the root of the grid system, and it is used to control the layout of the page. 

The <code>.container</code> element should be the root element, containing the child <code>.row</code> elements. 
So your basic layout should have the following strucutre:

```html
<body>
   <div class="container">
    ...
   </div>
</body>
```

> Aside: you can have multiple <code>.container</code> elements on a single page, but it is not recommended that you
nest them.

Beside the <code>.container</code> class, which is the recommended class to use for responsive desgin, you can also use <code>.container-fluid</code> class to achieve <code>width: 100%</code> across all viewport and device sizes. 

The following:

```html
<div class="container">
  Hello! I am in a simple container.
</div>

<div class="container-fluid">
  Hello! I am in a full-width container.
</div>
```
will produce the output:

![alt text][container]

[container]: https://raw.githubusercontent.com/yiqu/yiqu.github.io/master/assets/images/container.png.png "Container"

As you can see, there is a difference in the paddings between <code>container</code> and <code>container-fluid</code>.

<br/>

### Row

Bootstrap rows positions your elements horizontally across the screen. Following Rule 2, they are used to wrap your <code>column</code> elements.

You can as much rows you would like on your page, but they have to be in a <code>container</code>, like below:

```html
<div class="container">
  <div class="row">
    ...
  </div>
</div>
```

The row class will give a padding on both left and right side of the element, This is called "gutters" in Bootstrap. If you do not want
these paddings, they can removed with the <code>.no-gutters</code> class. This removes the negative margins from <code>.row</code> and the horizontal padding from all immediate children columns.

The following image shows the no gutters effect:

![alt text][container]

[NoGutter]: https://raw.githubusercontent.com/yiqu/yiqu.github.io/master/assets/images/gutters.png "GutterNo"

> Aside: Need an edge-to-edge design? Drop the parent .container or .container-fluid.

<br/>

### Column

