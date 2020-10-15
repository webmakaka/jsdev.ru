---
layout: page
title: Практический курс по Lodash - Установка Lodash
description: Практический курс по Lodash - Установка Lodash
keywords: [Oleksandr Kocherhin] Практический курс по Lodash [RUS, 2020], Видеокурс, JavaScript, Установка Lodash, русский язык
permalink: /courses/ru/lodash/practical-lodash-course/setup/
---

# Установка Lodash

    $ npm init -y
    $ npm install --save-dev webpack webpack-cli

<br/>

### С использованием WebPack

    $ npm install lodash

<br/>

**index.html**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <script src="bundle.js"></script>
    <title>Lodash</title>
  </head>
  <body>
    <h1>Hi lodash</h1>
  </body>
</html>
```

<br/>

**main.js**

```
import _ from 'lodash';
console.log('Hello, lodash!', _.isEmpty([]));
console.log('Lodash Version!', _.VERSION);
```

<br/>

https://webpack.js.org/guides/getting-started/

<br/>

**webpack.config.js**

<br/>

```js
const path = require('path');

module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname),
  },
};
```

<br/>

**package.json**

```
***

"scripts": {
    "webpack": "webpack"
  },

***
```

<br/>

    $ npm run webpack

<br/>

### Без использования WebPack

<br/>

    $ wget https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.20/lodash.js

<br/>

**index.html**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <script src="lodash.js"></script>
    <script src="main.js"></script>
    <title>Lodash</title>
  </head>
  <body>
    <h1>Hi lodash</h1>
  </body>
</html>
```

<br/>

**main.js**

```
console.log('Hello, lodash!', _.isEmpty([]));
```
