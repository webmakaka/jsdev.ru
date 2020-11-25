---
layout: page
title: Event Loop
description: Event Loop
keywords: javascript, Event Loop
permalink: /basics/event-loop/
---

# Event Loop

https://www.youtube.com/watch?v=w7wPSVB-S28

<br/>

```js
console.log('Event Loop\n');

function whatIsCallstack() {
  function foo() {
    console.log('[foo]: I am here!');

    // throw new Error('damn!');
  }

  function bar() {
    console.log('[bar]: I am here!');
    foo();
  }

  function baz() {
    console.log('[baz]: I am here!');
    bar();
  }

  baz();
}

// we may call our funcs recursively

// ! Talk about block

// Queue:
//

// ----STACK----
//  ----------
// |          |
// |          |
// |          |
// |          |
// |          |
// |          |

function callbacks() {
  console.log('Hello');

  setTimeout(function cb() {
    console.log('World');
  }, 3000);

  console.log('!');
}

function asyncMethod() {
  function asyncForEach(array, cb) {
    array.forEach(
      // func inner
      (item) => setTimeout(() => cb(item), 0)
    );
  }

  asyncForEach([1, 2, 3], (item) => console.log('async', item));
  [1, 2, 3].forEach((item) => console.log(item));

  // [1, 2, 3].forEach( a => somethingSlow(a) );
  // it's very slow

  // asyncForEach([1, 2, 3], (a) => somethingSlow(a));

  function somethingSlow(item) {
    // I mean realy sloooooow
  }
}

function interviewCase() {
  function setTimeoutOnly() {
    console.log(1);

    setTimeout(() => console.log(2), 200);

    setTimeout(() => console.log(3), 0);

    console.log(4);
  }

  function promiseInGame() {
    console.log(1);

    setTimeout(() => console.log(2), 0);

    Promise.resolve(3).then((a) => console.log(a));

    console.log(4);
  }

  function trickyPromise() {
    console.log(1);

    setTimeout(() => console.log(2), 0);

    new Promise((res, rej) => {
      console.log(3);
      res(4);
    }).then((a) => console.log(a));

    // WTF
    // new Promise( (resolve, reject) => {
    //   console.log('p', 1);
    //   console.log('p', 2);
    //   // throw new Error('fhdjfhsdjf');
    //   resolve('p' + 3);
    // })
    // .then(a => console.log(a))
    // .catch(err => console.log('Oops'));

    console.log(5);
  }

  function difficultPromiseInGame() {
    console.log(1);

    setTimeout(() => console.log(2), 0);

    Promise.resolve(3)
      .then((a) => {
        console.log(a); // 3
        return a + 1; // 4
      })
      .then((a) => {
        console.log(a); // 4
        return Promise.resolve(a + 1); // 5
      })
      .then((a) => console.log(a)); // 5

    Promise.resolve(6).then((a) => console.log(a));

    console.log(7);
  }

  // setTimeoutOnly();
  // promiseInGame();
  // trickyPromise();
  // difficultPromiseInGame();
}

// whatIsCallstack();
// callbacks();
// asyncMethod();
// interviewCase();
```

<br/>

```js
function print(a, b, c, d) {
  console.log({ a, b, c, d });
}

function transform(fn, context = null) {
  let resultFn = fn;
  console.log('base len: ', fn.length);

  function stepFn(arg) {
    resultFn = resultFn.bind(context, arg);

    console.log({ len: resultFn.length, resultFn });

    if (resultFn.length) {
      return stepFn;
    }

    return resultFn();
  }

  return stepFn;
}

print(9, 8, 7, 6);

let tranformedPrint = transform(print);

let fnWith3Params = tranformedPrint(1)(2)(3)(4);
```

<br/>

### [YouTube] Про цикл событий в JavaScript или "как на самом деле работает асинхронность"? [Перевод RUS, 2017]

<br/>

<div align="center">
    <iframe width="853" height="480" src="https://www.youtube.com/embed/8cV4ZvHXQL4" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br/>

<a href="/files/Event-Loop.pdf">+ Pdf'ka</a>
