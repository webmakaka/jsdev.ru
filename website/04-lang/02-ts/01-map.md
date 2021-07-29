---
layout: page
title: TypeScript - Массив объектов в виде строки, нужно представить в виде массива объектов
description: TypeScript - Массив объектов в виде строки, нужно представить в виде массива объектов
keywords: TypeScript - Массив объектов в виде строки, нужно представить в виде массива объектов
permalink: /lang/ts/map/
---

# Массив объектов в виде строки, нужно представить в виде массива объектов

<br/>

Строку следующего вида, нужно преобразовать в массив объектов

<br/>

```
"[ { title: 'Backlog', order: 1 }, { title: 'Sprint', order: 2 } ]"
```

<br/>

```js

export interface IColumns {
  title: string;
  order: number;
}

// @ts-ignore
const columnsRes = columnsToArrayOfObjects(columns as IColumns[]);


const columnsToArrayOfObjects = (columns: IColumns[]) => {
  const columnsParsed: IColumns[] = [];

  // @ts-ignore
  columns.map((column: IColumns) => {
    columnsParsed.push(column);
  });

  return columnsParsed;
};
```

<br/>

```js

export interface IColumns {
  title: string;
  order: number;
}

const columnsRes = columnsToArrayofObjects(columns);

const columnsToArrayOfObjects = (columns: string): IColumns[] => {
  const columnsParsed: IColumns[] = [];
  try {
    const columnsConverted = (columns as unknown) as IColumns[];
    columnsConverted.map((column: IColumns) => {
      columnsParsed.push(column);
    });
  } catch (err) {
    console.log("[App] Can't convert columns to Array of Objects");
  }

  return columnsParsed;
};
```

<br/>

При необходимости, (в другого рода случаях) нуно также использовать Stringify

<br/>

```
JSON.parse(newJson);
JSON.stringify(object)
```
