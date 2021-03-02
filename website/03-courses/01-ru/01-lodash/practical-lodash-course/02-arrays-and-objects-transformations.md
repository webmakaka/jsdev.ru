---
layout: page
title: Практический курс по Lodash - Трансформация массивов и объектов
description: Практический курс по Lodash - Трансформация массивов и объектов
keywords: Практический курс по Lodash, Видеокурс, JavaScript, Lodash, Трансформация массивов и объектов, русский язык
permalink: /courses/ru/lodash/practical-lodash-course/arrays-and-objects-transformations/
---

# Трансформация массивов и объектов

<br/>

### 1. Each

```js
const _ = require('lodash');

_.each([1, 2, 3], (item) => {
  console.log(item);
});
```

<br/>

```js
const _ = require('lodash');

const products = {
  1: {
    name: 'Product 1',
  },
  2: {
    name: 'Product 2',
  },
};

_.each(products, (product, key) => {
  console.log(product, key);
});
```

<br/>

```js
const _ = require('lodash');

const products = {
  1: {
    name: 'Product 1',
  },
  2: {
    name: 'Product 2',
  },
};

_.each([1, 2], (product, index) => {
  console.log(product, index);
});
```

<br/>

```js
const _ = require('lodash');

const products = {
  1: {
    name: 'Product 1',
  },
  2: {
    name: 'Product 2',
  },
};

let result = [];

_.each(products, (product, key) => {
  result.push(product.name);
});

console.log('result', result);
```

<br/>

### 2. Map (Предпочительнее использовать, чем each)

<br/>

```js
const _ = require('lodash');

const newLodashArr = _.map([1, 2, 3], (item) => {
  return item;
});

console.log(newLodashArr);
```

<br/>

```js
const _ = require('lodash');

const users = [
  {
    id: 1,
    name: 'User 1',
  },
  {
    id: 2,
    name: 'User 2',
  },
  {
    id: 3,
    name: 'User 3',
  },
];

// const ids = _.map(users, (user) => {
//   return user.id;
// });

// Так лучше
const ids = _.map(users, 'id');

console.log(ids);
```

<br/>

```js
const _ = require('lodash');

const users = {
  1: {
    name: 'User 1',
  },
  2: {
    name: 'User 2',
  },
  3: {
    name: 'User 3',
  },
};

const ids = _.map(users, (user, id) => {
  return Number(id);
});

console.log(ids);
```

<br/>

### 3. Сделай сам - map

<br/>

```js
const _ = require('lodash');

const users = [
  {
    id: 1,
    status: 'active',
    first_name: 'John',
  },
  {
    id: 2,
    status: 'inactive',
    first_name: 'Mike',
  },
  {
    id: 3,
    status: 'active',
    first_name: 'Bill',
  },
];

const normalizeUsers = (users) => {
  return _.map(users, (user) => {
    return {
      id: user.id,
      firstName: user.first_name,
      isActive: user.status === 'active',
    };
  });
};

const result = normalizeUsers(users);

console.log('result', result);
```

<br/>

```
result [
  { id: 1, firstName: 'John', isActive: true },
  { id: 2, firstName: 'Mike', isActive: false },
  { id: 3, firstName: 'Bill', isActive: true }
]
```

<br/>

### 4. Filter

Возвращаем boolean

<br/>

```js
const _ = require('lodash');

const result = _.filter([1, 2, 3, 4, 5], (item) => {
  return item < 3;
});

console.log('result', result);
```

<br/>

```js
const _ = require('lodash');

const users = [
  {
    id: 1,
    name: 'John',
  },
  {
    id: 2,
    name: 'Mike',
  },
  {
    id: 3,
    name: 'Bill',
  },
];

const result = _.filter(users, (user) => {
  return user.name === 'John';
});

console.log('result', result);
```

<br/>

```js
const _ = require('lodash');

const users = [
  {
    id: 1,
    name: 'John',
    isActive: true,
  },
  {
    id: 2,
    name: 'Mike',
    isActive: false,
  },
  {
    id: 3,
    name: 'Bill',
    isActive: false,
  },
];

// const result = _.filter(users, "isActive")
const result = _.filter(users, ['name', 'John']);

console.log('result', result);
```

<br/>

**Возвразается массив!**

```js
const _ = require('lodash');

const products = {
  1: {
    name: 'Milk',
    price: 100,
  },
  2: {
    name: 'Meat',
    price: 300,
  },
};

const result = _.filter(products, (product) => {
  return product.price > 150;
});

console.log('result', result);
```

<br/>

### 5. Сделай сам - filter

```js
const _ = require('lodash');

const products = [
  {
    id: 1,
    name: 'milk',
    price: '$1',
  },
  {
    id: 2,
    name: 'bread',
    price: '$2',
  },
  {
    id: 3,
    name: 'meat',
    price: '$3',
  },
];

const searchProducts = (products, searchedValue) => {
  return _.filter(products, (product) => {
    // return product.name.includes(searchedValue)
    return _.includes(product.name, searchedValue);
  });
};

const result = searchProducts(products, 'm');

console.log('result', result);
```

<br/>

```
result [
  { id: 1, name: 'milk', price: '$1' },
  { id: 3, name: 'meat', price: '$3' }
]
```

<br/>

### 6. Find

Возвращает первый и единственный элемент. Не массив!
Если не найдет, возвращает undefined.

```js
const _ = require('lodash');

const users = [
  {
    id: 1,
    name: 'John',
  },
  {
    id: 2,
    name: 'Mike',
  },
  {
    id: 3,
    name: 'Bill',
  },
];

const result = _.find(users, (user) => {
  return user.name === 'Mike';
});

console.log('result', result);
```

<br/>

### 7. Удаление элементов

```js
const _ = require('lodash');

const arr = [1, 2, 3, 4, 5];
const result = _.without(arr, 1);

console.log('result', result);
console.log('arr', arr);
```

<br/>

**Никогда не использовать remove!**
(Т.к. он мутирует )

Возвращает массив удаленных элементов.

```js
const _ = require('lodash');

const arr = [{ id: 1 }, { id: 2 }];
const result = _.remove(arr, (element) => {
  return element.id === 1;
});

console.log('result', result);
console.log('arr', arr);
```

<br/>

**Нужно всегда использовать reject.**

```js
const _ = require('lodash');

const arr = [{ id: 1 }, { id: 2 }];
// const result = _.reject(arr, (element) => {
//   return element.id === 1
// });

const result = _.reject(arr, ['id', 1]);

console.log('result', result);
console.log('arr', arr);
```

<br/>

### 8. Сделай сам - reject

```js
const _ = require('lodash');

const users = [
  {
    id: 1,
    name: 'John',
    isActive: true,
    likes: 110,
  },
  {
    id: 2,
    name: 'Mike',
    isActive: false,
    likes: 30,
  },
  {
    id: 3,
    name: 'Bill',
    isActive: true,
    likes: 40,
  },
];

const getPopularUsers = (users) => {
  return _.reject(users, (user) => {
    return !user.isActive || user.likes < 100;
  });
};

const result = getPopularUsers(users);

console.log('result', result);
```

<br/>

Здесь лучше использовать filter

```js
const _ = require('lodash');

const users = [
  {
    id: 1,
    name: 'John',
    isActive: true,
    likes: 110,
  },
  {
    id: 2,
    name: 'Mike',
    isActive: false,
    likes: 30,
  },
  {
    id: 3,
    name: 'Bill',
    isActive: true,
    likes: 40,
  },
];

const getPopularUsers = (users) => {
  return _.filter(users, (user) => {
    return user.isActive && user.likes > 100;
  });
};

const result = getPopularUsers(users);

console.log('result', result);
```

<br/>

### 9. Every и some

some - если хоть один элемен в массиве получаем true, иначе false

every - если каждый true, иначе false

```js
const _ = require('lodash');

const users = [
  {
    id: 1,
    name: 'John',
    isActive: true,
    likes: 110,
  },
  {
    id: 2,
    name: 'Mike',
    isActive: false,
    likes: 30,
  },
  {
    id: 3,
    name: 'Bill',
    isActive: true,
    likes: 40,
  },
];

// const isSomeActive = _.some(users, (user) => {
//   return user.isActive === true
// })

const isSomeActive = _.some(users, { isActive: true, likes: 40 });

const isAllActive = _.every(users, (user) => {
  return user.isActive === true;
});

console.log('isSomeActive', isSomeActive);
console.log('isAllActive', isAllActive);
```

<br/>

### 10. Сортировка

```js
const _ = require('lodash');

const users = [
  {
    id: 1,
    name: 'John',
    isActive: true,
    likes: 30,
  },
  {
    id: 2,
    name: 'Mike',
    isActive: false,
    likes: 50,
  },
  {
    id: 3,
    name: 'Bill',
    isActive: true,
    likes: 50,
  },
];

// const result = _.orderBy(users, ["likes"], ["desc"])
const result = _.orderBy(users, ['likes', 'name'], ['desc', 'asc']);

console.log('result', result);
```

<br/>

### 11. Группировка

```js
const _ = require('lodash');

const users = [
  {
    id: 1,
    name: 'John',
    isActive: true,
    likes: 30,
  },
  {
    id: 2,
    name: 'Mike',
    isActive: false,
    likes: 50,
  },
  {
    id: 3,
    name: 'Bill',
    isActive: true,
    likes: 50,
  },
];

// const result = _.groupBy(users, () => {
//   return users.isActive;
// })

const result = _.groupBy(users, 'isActive');

console.log('result', result);
```

<br/>

### 12. Строим цепочки

```js
const _ = require('lodash');

const users = [
  {
    id: 1,
    name: 'John',
    isActive: true,
    age: 32,
  },
  {
    id: 2,
    name: 'Mike',
    isActive: true,
    age: 27,
  },
  {
    id: 3,
    name: 'Bill',
    isActive: true,
    age: 28,
  },
];

const getYoungestUserMessage = (users) => {
  return _.chain(users)
    .filter('isActive')
    .orderBy(['age'])
    .map((user) => {
      return user.name + ' is ' + user.age;
    })
    .head()
    .value();
};

const result = getYoungestUserMessage(users);

console.log('result', result);
```

<br/>

### 13. Получение частей массива

```js
const _ = require('lodash');
const numbers = [1, 2, 3];

const result = _.chain(numbers).head().value();

console.log('result', result);
console.log('result', _.tail(numbers));
```

<br/>

```js
const _ = require('lodash');
const numbers = 'foo';

const result = _.chain(numbers).tail().join('').value();

console.log('result', result);
```

<br/>

```js
const _ = require('lodash');
const numbers = [1, 2, 3];

console.log('last', _.last(numbers));
console.log('initial', _.initial(numbers));
```
