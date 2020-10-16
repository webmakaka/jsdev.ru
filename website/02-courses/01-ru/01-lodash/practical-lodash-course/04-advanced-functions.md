---
layout: page
title: Практический курс по Lodash - Продвинутые функции
description: Практический курс по Lodash - Продвинутые функции
keywords: Практический курс по Lodash, Видеокурс, JavaScript, Lodash, Продвинутые функции, русский язык
permalink: /courses/ru/lodash/practical-lodash-course/advanced-functions/
---

# 4. Продвинутые функции

<br/>

### 1. Randomize

```js
const _ = require('lodash');
console.log('random', _.random(0, 10));
```

<br/>

### 2. Делаем данные уникальными

```js
const _ = require('lodash');
console.log('uniqueId', _.uniqueId('user_'));
console.log('uniqueId', _.uniqueId('user_'));
console.log('uniqueId', _.uniqueId('user_'));
```

<br/>

### 3. Делаем массивы одномерными

```js
const _ = require('lodash');

const foo = [[1, 2], [3]];

console.log(_.flatten(foo));
```

<br/>

### 4. Удаляем пустые элементы

Удаляет все false, null, 0, "", undefined, Nan из массива.

В том числе удаляет пустую строку.

```js
const _ = require('lodash');

console.log(_.compact([false, null, undefined, 'Привет!!!', ' ']));
```

<br/>

### 5. Иммутабельное обновление данных

```js
const _ = require('lodash');

const state = {
  isLoading: false,
  data: null,
  error: null,
};

const newState = _.assign({}, state, { isLoading: true });

console.log('result', state, newState);
```

<br/>

### 6. Клонируем данные

clone не копирует вложенные поля.

Нужно использовать cloneDeep если используются вложенные поля.

cloneDeep - работает медленнее.

```js
const _ = require('lodash');

const baseConfig = {
  apiUrl: 'http://someapi.com',
  port: 4000,
};

const createExtendedConfig = (config) => {
  // const cloneConfig = _.clone(config)
  const cloneConfig = _.cloneDeep(config);
  cloneConfig.host = 'https://google.com';
  return cloneConfig;
};

const result = createExtendedConfig(baseConfig);

console.log('baseConfig', baseConfig);
console.log('result', result);
```

<br/>

### 7. Проверяем типы данных

```js
const _ = require('lodash');

console.log(_.isEqual([1, 2], [1, 2]));
console.log(_.isEmpty([]));
console.log(_.isEmpty([1, 2, 3]));
```

<br/>

```js
if (_.isNil(user)) {
}
```

<br/>

### 8. Что такое Debounce

debounce - отложенный вызов

```html
<body>
  <h1>Hi lodash</h1>
  <input type="text" id="name" />
  <input type="text" id="email" />
  <script src="main.js"></script>
</body>
```

<br/>

```js
var handler = funcion(event){
  console.log('send reqquest to server', event.target.value)};
}

document
.getElementById('name')
.addEventListener('keydown', _.debounce(handler, 2000));
});
```

<br/>

### 9. Что такое Throttle

throttle - блокирует вызов, например несколько секунд ничего не происходит на указанный интервал.

Например, чтобы не кликали много раз на кнопку.

```js
var handler = funcion(event){
  console.log('send reqquest to server', event.target.value)};
}

document
.getElementById('name')
.addEventListener('keydown', _.debounce(handler, 2000));
});

document
.getElementById('email')
.addEventListener('keydown', _.throttle(handler, 2000));
});
```

<br/>

### 10. Миксины

Свои собственные lodash функции внутри chain.

```js
const _ = require('lodash');

const capitalizeLast = (str) => {
  const lastSymbol = _.last(str);
  const initialSymbols = _.chain(str).initial().join('').value();

  return initialSymbols + _.capitalize(lastSymbol);
};

_.mixin({ capitalizeLast });

const result = _.chain('foo').capitalizeLast().value();

console.log('result', result);
```
