---
layout: post
title: Angular Change Detection
readTime: 10
tags:
  - angular
  - change
  - detection
---

What is one way for components to communicate in Angular? It is by using `@Input` and `@Output`. Yes we could always use a service, but in this post we will dive deeper into how does Angular know when to run its change detection when new data has been communicated.
<!--more-->

### There are two ways to tell Angular when to run change detection. 

The first way is the default way. Angular will run change detection anytime the input's value or reference changes. You do not have to specify this as Angular will use this by default.

The second way is to run detection **only when the input's reference changes**. We do this by adding `changeDetection: ChangeDetectionStrategy.Default`.


Consider the following:

I have a component `<welcome>` that display the text 'Hello...' followed by a person's name. The name is displayed in a separate component `<welcome-name>`. Component `<welcome-name>` has a `@Input` value which receives a `Object` that contains the name property, and display the `name` property.

`welcome-component.ts` :

```js
@Component({
    selector: 'welcome',
    template: `Hello... <welcome-name></welcome-name>`
})
export class WelcomeComponent  {
  person = {
    name: 'Kevin'
  };
}
```

`welcome-name.ts` :

```js
@Component({
    selector: 'welcome-name',
    template: `{{ person.name }}`,
    changeDetection: ChangeDetectionStrategy.Default // can omit as it is the default way
})
export class NameComponent implements OnChanges  {
  @Input()
  person: { name: string };
  
  ngOnChanges() {
    console.log('Change detected!');
  }
}
```

What do we expect to see? Well, you guessed it, this should display `Hello... Kevin`.


Now if I add a method called `changeName()` in `<welcome>` component, like following:

```js
  changeName() {
    this.person.name = 'Bekah';
  }
```

and I run this method. What will be displayed now?

We will see `Hello... Bekah`, and also see a message `'Changed detected'` in the console.


But what if I change the changeDetection from `ChangeDetectionStrategy.Default` to `ChangeDetectionStrategy.onPush`? 

`welcome-name.ts` :

```js
@Component({
    selector: 'welcome-name',
    template: `{{ person.name }}`,
    changeDetection: ChangeDetectionStrategy.onPush // detection will run only when reference changes
})
export class NameComponent implements OnChanges  {
  @Input()
  person: { name: string };
  
  ngOnChanges() {
    console.log('Change detected!');
  }
}
```

What will we see now when we run `changeName()`? 

We will **not** see `Hello... Bekah`, and we will **not** see a message logged in the console.

This is because the `person` Object's reference did not change! The value has changed, but not its reference. 

### Before we go any further, *what is the difference between **reference** and **value**?*

Every `Object`, has 2 things that can make it be distinguished.

- Its value.
- Its address.

So if you say `person.name = "Bekah"`

know that there are 2 things about name. Its value which is `"Bekah"` and also its location in the memory which is some hexadecimal number maybe like this: `0x7fd5d258dd00`.

Depending on the language's architecture or the type (class, struct, etc.) of your object, you would be either transferring `"Bekah"` or `0x7fd5d258dd00`.

Passing `"Bekah"` is known as **passing by value**. Passing `0x7fd5d258dd00` is known as **passing by reference**. Anyone who is pointing to this memory location will have access to the value of `"Bekah"`. 

### Angular's `ChangeDetectionStrategy.onPush` works by comparing references of the inputs of the component.

This reason we did not see `Hello... Bekah`, and the code in `ngOnChanges()` did not execute is because:

- we mutated the `person` object directly.
- but `OnPush` works by comparing references of the inputs of the component.
- because we did not provide a reference to a new object but instead mutated an existing one, the OnPush change detector did not get triggered.

To 'fix' this, we can update `changeName()` method to:

```js
  changeName() {
    this.person = {
      name: 'Bekah'
    };
  }
```

Now we are creating a new reference for `person`, and passing it down to `<welcome-name>` component. Angular will see a new reference, and thus execute change detection and all is working again.

### Why do we want to use onPush?

Well, a few reasons to use onPush:

- immutability
- performance

It is always a good idea to enforce immutability in large applications. I would highly recommend checking out [Immutable.js](https://github.com/immutable-js/immutable-js), a JS library created by Facebook.

As for performance, we detect if a value has changed much faster with `onPush`. When a reference type is immutable, this means every time it is updated, the reference on the stack memory will have to change. Now we can simply check: Has the reference (in the stack) of the reference type changed? If yes, only then check all the values (on the heap).

In summary, always use `onPush` if you can. The default way is just fine if you are not too worried about the application's performance.

