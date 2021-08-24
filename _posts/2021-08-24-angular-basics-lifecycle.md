---
layout: post
title: Angular Basics Angular Lifecycle
readTime: 10
tags:
  - angular
  - lifecycle
---

An Angular project is made up of many components. When the application starts up, Angular runs the bootstrap sequence to build our application for display to the users.
During the time when users are using the application, users click around to navigate between different pages. Components gets created, and components gets destroyed. But are those the only two stages of the lifecycle of a Angular component? 
<!--more-->
The answer is no.

The lifecycle of an Angular component consists of **8 stages**. (not counting constructor initialization)

The stages, in order are: 
1. `ngOnChanges`
2. `ngOnInit` 
3. `ngDoCheck`
4. `ngAfterContentInit`
5. `ngAfterContentChecked`
6. `ngAfterViewInit`
7. `ngAfterViewChecked`
8. And lastly `ngOnDestroy`


## ngOnChanges - The first stage

This hook will run whenever one or more data-bound input properties change. This means if any bounded properties is changed, this hook will execute. For example, a property with the annotation `@Input()` changes, `ngOnChanges` will be executed. The `ngOnChanges` method receives a `SimpleChanges` object of current and previous property values.

Note that if your component has no inputs or you use it without providing any inputs, the framework will not call `ngOnChanges()`.

***Number of calls: many***

***When to use: hook on input() bounded changes***




## ngOnInit - The initialization

This hook is made for initialize of of class level properties in a component, or logic to be executed on start. `ngOnInit` initialize the directive or component after Angular first displays the data-bound properties and sets the directive or component's `Input()` properties. 

This hook is called once, after the first `ngOnChanges()`. `ngOnInit()` is still called even when `ngOnChanges()` is not.

***Number of calls: once***

***When to use: start up logic, and initial values assignment***


## ngDoCheck - The change detection

This hook runs whenever Angular change detection runs.

Called immediately after `ngOnChanges()` on every change detection run, and immediately after `ngOnInit()` on the first run.

***Number of calls: many***

***When to use: avoid using due to high amount of calls unless necessary***


## ngAfterContentInit - The external display

This hook runs when Angular is projecting the external content onto the view. 

Called once after the first `ngDoCheck()`.

***Number of calls: once***

***When to use: hook after < ng-content > is projected***


## ngAfterContentChecked - The external display change detection

This hook runs after Angular checks the content projected into the directive or component.

Called after `ngAfterContentInit()` and every subsequent `ngDoCheck()`.

***Number of calls: many***

***When to use: avoid using due to amount of calls unless necessary***


## ngAfterviewInit - The template display

In addition to `ngAfterContentInit()`, this hook initializes the component's views and child views.

Called once after the first `ngAfterContentChecked()`.

***Number of calls: once***

***When to use: logic that requires elements rendered already***



## ngAfterviewChecked - The external display change detection

This hook runs after Angular checks the component's views and child views, or the view that contains the directive.

Called after the `ngAfterViewInit()` and every subsequent `ngAfterContentChecked()`.

***Number of calls: many***

***When to use: avoid using due to amount of calls unless necessary***



## ngOnDestroy - The external display change detection

This hook runs just before Angular destroys the directive or component.

Called immediately before Angular destroys the directive or component.

***Number of calls: once***

***When to use: unsubscibe from Obseravble subscriptions, or other cleanup logic***

## Summary

This is a infographic of the Angular lifecycles that I found to be useful.

![alt text](https://raw.githubusercontent.com/yiqu/yiqu.github.io/master/assets/nglifecycle.png "Logo Title Text 1")

Each Angular lifecycle has its own purpose, but it does not mean you will be using all eight in every component. I have found the most useful hooks are `ngOnInit`, `ngOnChanges`, and `ngOnDestroy`. Let me know what you think the most useful hooks and why!
