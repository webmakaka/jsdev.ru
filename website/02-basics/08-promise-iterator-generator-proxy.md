---
layout: page
title: Promise, Iterator, Generator, Proxy
description: Promise, Iterator, Generator, Proxy
keywords: javascript, promise, iterator, generator, proxy
permalink: /basics/promise-iterator-generator-proxy/
---

# Promise, Iterator, Generator, Proxy

https://www.youtube.com/watch?v=GHrXvQhb7K0&t=2008s

<br/>

```js
let readlineSync = require('readline-sync');

console.log('Welcome to RS Lecture - ES6 Advanced\n');

function promises() {
  console.log('Promise\n');

  function base() {
    let p = new Promise((res, rej) => {
      setTimeout(() => res('hello'), 1500);
    });

    p.then((data) => {
      console.log(data);
      return data + ' World';
    }).then((a) => console.log(a));

    Promise.all([
      Promise.resolve('First'),
      new Promise((res, rej) => res('Second')),
      new Promise((res, rej) => setTimeout(() => res('Third'), 0)),
    ])
      .then((results) => {
        results.forEach((result) => console.log('from All:', result));
      })
      .catch((err) => console.log('something went wrong', err));

    Promise.race([
      // Promise.reject('First'),
      new Promise((res, rej) => setTimeout(() => res('Third'), 0)),
      new Promise((res, rej) => res('Second')),
      Promise.resolve('First'),
    ])
      .then((result) => {
        console.log('from Race:', result);
      })
      .catch((err) => console.log('something went wrong', err));
  }

  function interestingExample() {
    function waitTimeout(delay = 0) {
      return new Promise((resolve) => {
        setTimeout(resolve, delay);
      });
    }

    waitTimeout(3000).then(() => console.log('call after 3000ms'));
  }

  // base();
  // interestingExample();

  // Promise.resolve
  // Promise.reject
  // Promise.all
  // Promise.race
}

function iteratorGenerator() {
  console.log('Iterator / Generator\n');

  function intro() {
    function* gen() {
      yield 1;
      yield 2;
      yield 3;
      // return 4;
    }

    let it = gen();

    console.log(it.next());
    console.log(it.next());
    console.log(it.next());
    console.log(it.next());
    // console.log(it.next());
    // console.log(it.next());

    // let arrayIt = ['a', 'b', 'c'][Symbol.iterator]();

    // console.log(arrayIt.next());
    // console.log(arrayIt.next());
    // console.log(arrayIt.next());
    // console.log(arrayIt.next());
  }

  function examples() {
    // (1)
    function* range(start, end, step) {
      let current = start;

      while (current <= end) {
        yield current;
        current += step;
      }
    }

    console.log([...range(1, 15, 3)]);

    // (2)
    function* fact() {
      let n = 1;
      let current = n;

      while (true) {
        yield current;
        current *= ++n;
      }
    }

    let f = fact();

    console.log(
      f.next().value,
      f.next().value,
      f.next().value,
      f.next().value,
      f.next().value
    );

    // (3)
    Number.prototype[Symbol.iterator] = function* () {
      for (let i = 0; i < this; i++) {
        yield i;
      }
    };

    console.log([...10]); // [0, 2, 3, ... , 9]
  }

  function iterableClass() {
    class EventHandlers {
      constructor() {
        this.handlersMap = {};
      }

      add(key, handler) {
        if (!this.handlersMap[key]) {
          this.handlersMap[key] = [];
        }

        this.handlersMap[key].push(handler);
      }

      [Symbol.iterator] = function* () {
        for (let key of Object.keys(this.handlersMap)) {
          let handlerList = this.handlersMap[key];

          for (let i = 0; i < handlerList.length; i++) {
            yield {
              key,
              fn: handlerList[i],
            };
          }
        }
      };
    }

    let handlers = new EventHandlers();

    handlers.add('click', () => {
      console.log('click 1');
    });

    handlers.add('click', () => {
      console.log('click 2');
    });

    handlers.add('scroll', () => {
      console.log('scroll 1');
    });

    console.log('[handler inside]:', ...handlers);
  }

  function nested() {
    function* gen() {
      function* innerGen() {
        yield 'inner 1';
        yield 'inner 2';
        yield 'inner 3';
      }

      yield 1;
      yield* innerGen();
      yield 2;
    }

    let it = gen();

    console.log('[Nested example]:', [...it]);
  }

  function simpleChatBot() {
    function* createBot() {
      let msg = yield "Hello, I'm bot. Who are you?\n";

      while (true) {
        if (msg === 'end') {
          console.log('bye!');
          return;
        }

        if (msg) {
          if (msg.startsWith('echo')) {
            console.log(msg.slice(5));
          } else if (msg.startsWith('I am')) {
            console.log(`Nice to meet you, ${msg.slice(5)}!`);
          } else {
            console.log('I do not understand you :(');
          }
        }

        msg = yield '\nWhat next?';
      }
    }

    let bot = createBot();
    let nextElem = bot.next(); // Init bot

    while (!nextElem.done) {
      let answer = readlineSync.question(nextElem.value + '\n');
      nextElem = bot.next(answer);
    }
  }

  // intro();
  // examples();
  // iterableClass();
  // nested();
  // simpleChatBot();
}

function proxies() {
  function intro() {
    let obj = {
      a: 1,
    };

    let a = new Proxy(obj, {
      get(target, key) {
        console.log(target, key);
        return target.hasOwnProperty(key) ? target[key] : 9;
      },
    });

    console.log(a.a, a.b);
  }

  function updateBehavior() {
    let user = {
      name: 'John Doe',
      role: 'admin',
    };

    let upperUser = new Proxy(user, {
      get(target, property) {
        return target[property] ? target[property].toUpperCase() : undefined;
      },
    });

    console.log('\n' + upperUser.name, '-', upperUser.role);
  }

  function metaProgramming() {
    const evenNumbers = new Proxy([], {
      get: (target, index) => index * 2,
      has: (target, number) => number % 2 === 0,
    });

    console.log('2 in evenNumbers', 2 in evenNumbers);
    console.log('7 in evenNumbers', 7 in evenNumbers);
    console.log('evenNumbers[3]', evenNumbers[3]);
    console.log('evenNumbers[-2]', evenNumbers[-2]);
  }

  // intro();
  // updateBehavior();
  // metaProgramming();

  // say about Function hooks / AOP
}

// promises();
// iteratorGenerator();
// proxies();
```
