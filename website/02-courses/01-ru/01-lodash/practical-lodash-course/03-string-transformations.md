---
layout: page
title: Практический курс по Lodash - Трансформации строк
description: Практический курс по Lodash - Трансформации строк
keywords: Практический курс по Lodash, Видеокурс, JavaScript, Lodash, Трансформации строк, русский язык
permalink: /courses/ru/lodash/practical-lodash-course/string-transformations/
---

# 3. Трансформации строк

<br/>

### 1. Регистры

```js
const _ = require('lodash');
console.log(_.chain('FOO').toLower().split('').value());
```

<br/>

### 2. Обьединение и разбивка строк и массивов

```js
const _ = require('lodash');

console.log(_.chain('foo/bar').split('/').head().value());
console.log(_.chain(['foo', 'bar']).join('/').toUpper().value());
```

<br/>

### 3. Сделай сам - конвертируем строку

```js
const _ = require('lodash');

const toSlug = (str) => {
  const slug = _.chain(str).toLower().split(' ').join('-').value();
  return encodeURI(slug);
};

const slug = toSlug('This is super quiz');

console.log('slug', slug);
```

<br/>

### 4. Capitalize

```js
console.log(_.capitalize('foo Bar'));
```

<br/>

### 5. Регистры. Часть 2

```js
console.log(_.camelCase('Foo bar Baz'));
```

```js
console.log(_.snakeCase('productName'));
```
