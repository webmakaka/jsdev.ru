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

