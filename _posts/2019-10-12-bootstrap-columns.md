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

The rows & columns always work together, and one should never have one without the other.

### .container
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

Though the <code>.container</code> class is the recommended class to use for responsive desgin, you can also use <code>.container-fluid</code> class to achieve <code>width: 100%</code> across all viewport and device sizes.

