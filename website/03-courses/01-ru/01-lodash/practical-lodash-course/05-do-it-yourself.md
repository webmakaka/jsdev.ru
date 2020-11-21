---
layout: page
title: Практический курс по Lodash - Сделай сам
description: Практический курс по Lodash - Сделай сам
keywords: Практический курс по Lodash, Видеокурс, JavaScript, Lodash, Сделай сам, русский язык
permalink: /courses/ru/lodash/practical-lodash-course/do-it-yourself/
---

# 5. Сделай сам

<br/>

### 1. Сделай сам - маппинг данных

```js
const _ = require('lodash');

const loc = [
  {
    location_key: [32, 22, 11],
    autoassign: 1,
  },
  {
    location_key: [41, 42],
    autoassign: 1,
  },
];

const bulkConfig = [
  {
    dataValues: {
      config_key: 100,
    },
  },
  {
    dataValues: {
      config_key: 200,
    },
  },
];

// const result = _.map(loc, (locEl, index) => {
//   return _.map(locEl.location_key, (locationKey) => {
//     return {
//       config_key: bulkConfig[index].dataValues.config_key,
//       location_key: locationKey,
//       autoassign: locEl.autoassign,
//     };
//   });
// });

// const flattenedResult = _.flatten(result);

// console.log('result', flattenedResult);

const getConfigs = (locEl, index) => {
  return _.map(locEl.location_key, (locationKey) => {
    return {
      config_key: bulkConfig[index].dataValues.config_key,
      location_key: locationKey,
      autoassign: locEl.autoassign,
    };
  });
};

const configs = _.chain(loc).map(getConfigs).flatten().value();

console.log('configs', configs);
```

<br/>

result

```
configs [
  { config_key: 100, location_key: 32, autoassign: 1 },
  { config_key: 100, location_key: 22, autoassign: 1 },
  { config_key: 100, location_key: 11, autoassign: 1 },
  { config_key: 200, location_key: 41, autoassign: 1 },
  { config_key: 200, location_key: 42, autoassign: 1 }
]

```

<br/>

### 2. Сделай сам - функция classnames

Чего-то поломалось с chain. По быстрому не разберусь. Оставил вариант без chain.

```js
const _ = require('lodash');
const classNames = (conditions) => {
  const foo = _.map(conditions, (value, key) => {
    return value ? key : undefined;
  });
  return _.join(_.compact(foo), ' ');

  // const getUsedClassName = async (value, key) => {
  //   console.log('------------');

  //   return (await value) ? key : undefined;
  // };

  // return _.chain(conditions).map(getUsedClassName).compact().join(' ').values();
};

const isAuthor = false;
const isInFocus = true;
const liClass = classNames({
  item: true,
  active: isAuthor,
  'item-hightlighted': isInFocus,
});

console.log('liClass', liClass);
```

<br/>

```
liClass item item-hightlighted
```

<br/>

### 3. Сделай сам - замена параметров в url

```js
const _ = require('lodash');

const replaceParamsInUrl = (url, replacements) => {
  // Так не надо из-за возможной мутации при передаче объектов
  // _.map(replacements, (replacement) => {
  //   url = _.replace(url, ':' + replacement.from, replacement.to);
  // });
  // return url;

  return _.reduce(
    replacements,
    (acc, replacement) => {
      return _.replace(acc, ':' + replacement.from, replacement.to);
    },
    url
  );
};

const initialUrl = '/posts/:postId/comments/:commentId';
const resultUrl = replaceParamsInUrl(initialUrl, [
  {
    from: 'postId',
    to: '1',
  },
  {
    from: 'commentId',
    to: '3',
  },
]);

console.log('resultUrl', resultUrl);
```

<br/>

```
resultUrl /posts/1/comments/3
```

<br/>

### 4. Сделай сам - сообщения валидации

```js
const _ = require('lodash');

const backendErrors = {
  email: {
    errors: [{ message: "Can't be bank" }],
  },
  password: {
    errors: [
      { message: 'Must contain symbols in different case' },
      { message: 'Must be at least 8 symbols long' },
    ],
  },
  passwordConfirmation: {
    errors: [{ message: 'Must match with password' }],
  },
};

const humanReadableBackendErrors = _.map(backendErrors, (value, field) => {
  const fieldMessages = _.chain(value.errors).map('message').join(', ').value();

  return _.upperFirst(field + ': ' + fieldMessages);
});

console.log('result', humanReadableBackendErrors);
```

<br/>

result

```
result [
  "Email: Can't be bank",
  'Password: Must contain symbols in different case, Must be at least 8 symbols long',
  'PasswordConfirmation: Must match with password'
]

```

<br/>

### 5. Сделай сам - вложенные списки

```js
const _ = require('lodash');

const flatList = [
  {
    id: 1,
    name: 'lvl 1 tiem 1',
    parentId: null,
  },
  {
    id: 2,
    name: 'lvl 1 tiem 2',
    parentId: null,
  },
  {
    id: 3,
    name: 'lvl 2 tiem 3',
    parentId: 1,
  },
  {
    id: 4,
    name: 'lvl 3 tiem 4',
    parentId: 3,
  },
  {
    id: 5,
    name: 'lvl 3 tiem 5',
    parentId: 2,
  },
];

const addChildren = (item) => {
  const children = _.filter(flatList, (childItem) => {
    return childItem.parentId === item.id;
  });
  let nestedChildren = [];
  if (!_.isEmpty(children)) {
    nestedChildren = _.map(children, addChildren);
  }

  return _.assign({}, item, { children: nestedChildren });
};

const nestedList = _.chain(flatList)
  .filter((item) => {
    return item.parentId === null;
  })
  .map(addChildren)
  .value();

console.log('nestedList', nestedList);
```

<br/>

```
nestedList [
  {
    id: 1,
    name: 'lvl 1 tiem 1',
    parentId: null,
    children: [ [Object] ]
  },
  {
    id: 2,
    name: 'lvl 1 tiem 2',
    parentId: null,
    children: [ [Object] ]
  }
]
```
