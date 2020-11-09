---
layout: post
title: Common RxJs Maps
readTime: 5
tags:
  - rxjs
---

RxJS is mostly useful for its operators, even though the Observable is the foundation. Operators are the essential pieces that allow complex asynchronous code to be easily composed in a declarative manner. If you have worked
with RxJs, you probably have used a operator or two.

In this post, I want to highlight 4 most commonly used transformation operators. Transformation operators are operators that transforms data.


#### mergeMap/flatmap

##### What is it?

mergeMap creates an Observable immediately for any source item, all previous Observables are kept alive.

##### When to use it?

For doing things in parallel. For when things should not be cancelled. Writing to a file is a good usage for mergeMap because you do not want to lose any inputs.

##### Example

```javascript
// RxJS v6+
import { fromEvent, of } from 'rxjs';
import { mergeMap, delay } from 'rxjs/operators';

// faking network request for save
const saveLocation = location => {
  return of(location).pipe(delay(500));
};
// streams
const click$ = fromEvent(document, 'click');

click$
  .pipe(
    mergeMap((e: MouseEvent) => {
      return saveLocation({
        x: e.clientX,
        y: e.clientY,
        timestamp: Date.now()
      });
    })
  )
  // Saved! {x: 98, y: 170, ...}
  .subscribe(r => console.log('Saved!', r));
```

#### concatMap

##### What is it?

Waits for the previous Observable to complete before creating the next one. 

##### When to use it?

For when you need to do things in sequence while waiting for completion. Writing files to a database to make sure orders are respected.

##### Example

```javascript
from([1, 2, 3 ,4]).pipe(
  concatMap(param => getData(param))
).subscribe(val => console.log('concatMap:', val));
```


#### switchMap

##### What is it?

For any source item, completes the previous Observable and immediately creates the next one. 

The main difference between switchMap and other flattening operators is the cancelling effect. 
On each emission the previous inner observable (the result of the function you supplied) is cancelled and the new observable is subscribed. 
You can remember this by the phrase switch to a new observable.

##### When to use it?

For cancellation effects. Search type-aheads would be a great usage, it will cancell the previous emission and subscribe to the current.

##### Example

```javascript
// RxJS v6+
import { interval, fromEvent } from 'rxjs';
import { switchMap } from 'rxjs/operators';

fromEvent(document, 'click')
  .pipe(
    // restart counter on every click
    switchMap(() => interval(1000))
  )
  .subscribe(console.log);
```

#### exhaustMap

##### What is it?

Source items are ignored while the previous Observable is not completed.

##### When to use it?

For when you want to finish the current item before subscribing to the next one. Login button’s click handler, or refresh/update button.
This is great for a application that must be resistant to incessant clickers!

##### Example

```javascript
// RxJS v6+
const { fromEvent, of } = rxjs;
const { exhaustMap, delay } = rxjs.operators;

const getNews = () => {
  console.log('New call to news API');

  return of('Latest news (...)' + new Date()).pipe(
    delay(4000)
  );
};

const news$ = fromEvent(newsBtn, 'click').pipe(
  exhaustMap(() => getNews())
);
```

#### Conclusion

All of these four operators above are useful in its own ways, but they are meant to be used in its own scenarios. For more detailed explainations, checkout [https://www.learnrxjs.io/learn-rxjs/operators/transformation](learn RxJs) .
