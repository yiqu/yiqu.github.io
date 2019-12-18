---
layout: post
title: NPX and NPM
readTime: 4
tags:
  - npm
  - npx
  - modules
---

If you are learning how to use a new Javascript framework or library, you might see the following command <code>npx name-of-package ...</code> in the Getting Started section. You might say to yourself, wow they made a typo! Actually they did not. <code>npx</code> and <code>npm</code> are very different things, and it was meant to be used that way.

Before proceeding, the gist is: 

**NPM - Manages packages but doesn't make life easy executing any.**

**NPX - A tool for executing Node packages.**

<!--more-->

### NPM

We all know what <code>npm</code> does, it is a package manager that manages and installs the application's modules based on the application's package.json file. When you run <code>npm install</code>, it scan your package.json file, and installs all neccessary modules based on the versions it specified. <code>npm</code> installs these modules to a folder called <node>./node_modules</code>. Another common usage is to use <code>npm</code> to install a new module by simply typing <code>npm install cool-thing</code> and <code>npm</code> will install it, add the <code>cool-thing</code> to your application's <code>package.json</code> file.

So what does <code>npx</code> do that is different than <code>npm</code>?

### NPX

If npm manages your modules, npx executes them instead. <code>npx</code> checks if the module exists in the path, if it does, it executes it. If it does not, it will installs the module, and executes it. 

For example, I want to use the [create-react-app](https://github.com/facebook/create-react-app) module to create a new seed React app. I do not care about saving it to my dependencies in my package.json file, because it's purpose is to just create the seed app and I will never use it again after. Then <code>npx</code> is the perferred over installing with npm. So if we ran the command:

```bash
npx create-react-app my-new-app
```

If <code>create-react-app</code> has not been installed in the path, <code>npx</code> just installed it for you, and executed the command which resulted in a new React seed app called <code>my-new-app</code> being created. This is a huge advantage that ensures you always use the latest version of a generator or build tool without having to upgrade each time you’re about to use it.

#### Conclusion

So in summary, when should I use npx? npx should be used when you want to execute a package or module (that was not previously installed) once and not care to use it again in the future.

