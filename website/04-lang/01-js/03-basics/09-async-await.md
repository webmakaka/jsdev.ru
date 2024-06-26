---
layout: page
title: Async/Await
description: Async/Await
keywords: Async/Await
permalink: /lang/js/basics/async-await/
---

# Async/Await

<br/>

- Надо почитать и позапускать.

https://discordapp.com/channels/755676888680366081/755859573264482385/763367048969453588

Я попробую дать развёрнутый ответ. Только для начала мне придётся немного скорректировать ваше понимание нотации async/await. Разберём по отдельности.

У ключевого слова async есть несколько особенностей.

Во-первых, оно гарантирует, что функция (в т.ч. стрелочная, а также генератор) вернёт Promise, независимо от того, какое значение вы возвращаете в return: оно всегда будет обёнуто в новый Promise.

Вот вам пример, чтобы убедиться в этом самому:

```js
async function a () { const p = Promise.resolve(); p.myCustomProperty = true; return p; }
function b () => { const p = Promise.resolve(); p.myCustomProperty = true; return p; }

// Обратите внимание, я не делаю await, потому что хочу обратиться к самому Promise

console.log(a().myCustomProperty); // -> undefined
console.log(b().myCustomProperty); // -> true
```

Почему так произошло, написано выше. Как видите, гарантия вовращения Promise соблюдена.

Во-вторых, async открывает возможность использовать внутри тела функции ключевое слово await, которое приостанавливает работу текущей функции до момента разрешения (settle) промиса в какое-либо значение или ошибку, и после этого продолжает свою работу с учётом этот результата (продолжение работы или выброс ошибки). Важное слово здесь - приостанавливает. Я думаю, вы успели посмотреть, что такое event loop в Node, потому что вся активность в этом самом event loop продолжается, а значит, если есть другие задачи (microtasks/macrotasks, в числе которых может значиться Promise, который шёл после await), они будут обрабатываться дальше. В этом и есть асинхронность, что происходит не блокировка всех остальных задач до момента завершения текущей, а приостановка текущей с продолжением выполнения остальных запланированных. В двух словах, одна задача не блокирует остальные.

Теперь про сам await. Этот оператор может принимать любые значения. Можно даже написать await 1. Но все значения, которые не Promise, сразу же зарезолвятся, и функция продолжит работу. Можно также строить более сложные схемы:

```js
const pause = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

const promise10ms = pause(10);

(async () => {
  await promise10ms;
})();
```

Т.е. закидывать в await ранее созданный Promise. Всё ограничивается вашей фантазией и условиями задачи.

Небольшой комментарий про callback и async/await из моего опыта. Оба этих подхода являются асинхронными, разница проявляется при использовании. Запись в стиле async/await очень похожа на запись синхронного кода, последовательность выполения в котором очевидна из-за следования конструкций друг за другом. Запись в стиле callback может требовать другого типа мышления и написания кода, что при сложном флоу может порождать проблемы с читаемостью (т.н. спагетти-код, коллбек в другом коллбеке) и пониманием последовательности, т.к. из исходного когда может неочевидно, в какой последовательности выполняются коллбеки - нужно идти и смотреть. Также это может порождать проблемы с обработкой ошибок, особенно если запущено несколько колбеков одновременно. С опытом можно научиться обходить такие проблемы. В целом, в моём восприятии с async/await всё проще, хотя и async/await тоже можно превратить в спагетти.

А теперь пример, который, как я надеюсь, объяснит разницу между синхронным и асинхронным кодом, на примере работы с файловой системой:

```js
// sync
const { readFileSync } = require('fs');

const readJson = (fileName) => {
  const contents = readFileSync(fileName, 'utf8'); // блокировка event loop, пока файл не прочитается полностью

  return JSON.parse(contents);
}

readJson('a.json');
readJson('b.json'); // не будет прочитан пока не будет прочитан предыдущий

// async
const { promises as fsp } = require('fs');

const readJson = (fileName) => {
  const contents = await fsp.readFile(fileName, 'utf8'); // без блокировки event loop, соответственно, можно запускать несколько таких функций одновременно

  return JSON.parse(contents);
}

readJson('a.json');
readJson('b.json'); // будет читаться одновременно с предыдущим, потому что тот не блокировал работу
```

Надеюсь, мой комментарий был полезным и дал ответ на ваш вопрос.
