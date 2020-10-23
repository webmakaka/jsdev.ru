---
layout: page
title: Изучаем, обсуждаем и делимся материалами для освоения современного JavaScript и JavaScript фреймворков на русском языке
permalink: /
---

# Изучаем, обсуждаем и делимся материалами для освоения современного JavaScript и JavaScript фреймворков на русском языке

<br/>

### Совместное изучение материалов по современному javascript и javascript фреймворков

Изучать материалы интереснее в коллективе, особенно когда что-то не работает и есть у кого спросить, посмотреть код, задать вопрос.

Если ставить какие-то цели и проводить challeng'ы, то это в некоторых случах дисциплинирует участников.

Пример, challenge по какому-то курсу.

Договариваемся, что изучаем материала минимум по пол часа видео в день.

Каждый из участников:

- скачивает материал к себе
- создает каталог с названием "TODAY"
- закидывает в него видео на оговоренный минимум.
- и смотрит, изучает, прорабатывает. И пока не посмотрел, никаких ютубчиков, твичей, сериальчиков и даже порнхабчиков.

Кому интересно, присоединяйтесь.

<br/>

В общем, если есть желание разбирать что-то коллективно:

- пишите об этом в нашем телеграм чате.
- создаете проект на github и после каждого видео (если в нем что-то делалось практическое и значимое) создаете коммит.
- В файле Readme.md писать команды которые выполнялись в курсе.
- Важные изменения в дизайне приложения фиксировать в скриншотах и добавлять их также в проект.
- А здесь мы будем размещать ссылки на публичные репо участников.

<br/>

<strong><a href="//labs.jsdev.org/">Планы по материалам, которые планируются изучить</a></strong>

<br/>

### [Бесплатно] [Онлайн] [RS School] Курс "JavaScript/Front-end". [RUS, 28 февраля 2021]

<br/>

![RS School JavaScript/Front-end](/img/rs-school.png 'RS School JavaScript/Front-end'){: .center-image }

https://community-z.com/events/js-intro-rss-2021q1

**Чекните также предстоящие события:**  
https://community-z.com/communities/the-rolling-scopes/events

<br/>

Сам записался в школу. Прохожу 2 курса. По node.js и Node.js + aws. Кто не успел, можно будет запланировать свое обучение на следующий поток. Например, курс Node.js + AWS планируют читать 2 раза в год.

Если заинтересовались, то. Программа есть. Записи видео, есть. Задания и критерии оценки, есть. Единственное чего нет, это наставников и обучающихся. Можете не терять времени и не ждать старта нового потока, а заранее изучить материалы и написать программы в расслабленном темпе. И когда отроется новый поток, вам не придется начинать с 0. Программисты с опытом разработки на JS, разумеется с заданиями справятся. А вот остальным может быть достаточно сложно.

Курс читают и проводят преимущественно сотрудники EPAM. Как минимум, наверное, будет полезно посмотреть тем, кто еще не работает программистами или тем, кто работает, но не в софтверных компаниях.

<br/>

<a href="/schools/rs-school/">Здесь мои записи по текущим курсам</a>

<br/>

### [YouTube] Про цикл событий в JavaScript или "как на самом деле работает асинхронность"? [Перевод RUS, 2017]

<br/>

<div align="center">
    <iframe width="853" height="480" src="https://www.youtube.com/embed/8cV4ZvHXQL4" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br/>

<a href="/files/Event-Loop.pdf">+ Pdf'ka</a>

<br/>

### [YouTube, Владилен Минин] Уроки по JavaScript [RUS, 2020]

<br/>

<div align="center">
    <iframe width="853" height="480" src="https://www.youtube.com/embed/videoseries?list=PLREQY2tFmFnrVNPcEHdy0j-AtPhNk7-rC" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br/>

### [YouTube, Владилен Минин] React Hooks - Полный Курс (Про Все Хуки!) [RUS, 2020]

<br/>

<div align="center">
    <iframe width="853" height="480" src="https://www.youtube.com/embed/9KJxaFHotqI" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<!--

- Надо поичать и позапускать.

https://discordapp.com/channels/755676888680366081/755859573264482385/763367048969453588

Я попробую дать развёрнутый ответ. Только для начала мне придётся немного скорректировать ваше понимание нотации async/await. Разберём по отдельности.

У ключевого слова async есть несколько особенностей.

Во-первых, оно гарантирует, что функция (в т.ч. стрелочная, а также генератор) вернёт Promise, не в зависимости от того, какое значение вы возвращаете в return: оно всегда будет обёнуто в новый Promise.

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

Теперь про сам await. Этот оператор может принимать любые значения. Можно даже написать await 1. Но все значения, которые не Promise, сразу же заресолвятся, и функция продолжит работу. Можно также строить более сложные схемы:

```js
const pause = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

const promise10ms = pause(10);

(async () => {
  await promise10ms;
})();
```

Т.е. закидывать в await ранее созданный Promise. Всё ограничивается вашей фантазией и условиями задачи.(edited)

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

-->

<br/>

### [Андрей Мелихов] Архитектура современного корпоративного Node js приложения [RUS, 2020]

Нужно найти время и посмотреть

<br/>

<div align="center">

    <iframe width="853" height="480" src="https://www.youtube.com/embed/dQjXIuaq-yo" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

</div>

<br/>

https://habr.com/ru/company/yandex/blog/514550/

<br/>

### Пожелание по добавлению инструкций для запуска изученных проектов

Пройденные материалы должны оставаться в копилке разработчиков, чтобы к ним можно было вернуться и посмотреть реализацию. Поэтому предлагается подготавливать проект, чтобы его можно было легко запустить человеку, которому нужны примеры решений и он не хочет смотреть курс и тратить на него драгоценное время.

Если изучаете всевозможные курсы или читаете книги, где создают толковые проекты сложнее "hello world", делитесь результатами, чтобы их можно было легко запустить. Например, средствами docker, kubernetes. Сопровождайте проекты инструкциями для запуска.

<br/>

### [NewLine] TinyHouse: A Fullstack React Masterclass with TypeScript and GraphQL [ENG, 2020]

**Для меня это лучший курс 2020**

Достаточно интересный курс. Смотрю вторую часть проекта. Оригинальные исходные коды есть.

Здесь и TypeScript, и GraphQL, и React, и MongoDB присутствуют.

Сам проект я завернул в kubernetes и разработка ведется сразу в нем с автоматическим обновлением проекта при сохранении.

Взяты последние пакеты, в том числе и ApolloClient 3.X.X. Кому интересно, делайте параллельно.

Мои исходные коды <a href="https://github.com/webmakaka/TinyHouse-A-Fullstack-React-Masterclass-with-TypeScript-and-GraphQL">здесь</a>.

<br/>

### [Zachary Reece] Implement High Fidelity Designs with Material-UI and ReactJS [ENG, 2020]

https://www.udemy.com/course/implement-high-fidelity-designs-with-material-ui-and-reactjs/

Появились исходные коды. Придется изучать.

35-40 часовый курс.

<br/>

### [Reed Barger] Build an Instagram Clone with React [ENG, 2020]

Ну чего, посоны? Каждому по своему инстраграму?

<a href="https://github.com/webmakaka/Build-an-Instagram-Clone" rel="nofollow">[Reed Barger] Build an Instagram Clone with React [ENG, 2020]</a>

Мне понравился этот курс. Хоть Instagram и получился недоделанным, т.к. большая часть функционала не была реализована, но выглядит норм.

Автор зачем-то понадеялся на Instagram CDN для своих картинок, который был благополучно удален сервисом где-то в середине записанного курса. Если кто будет копать, рекомендую просто скопировать мой вариант файла с картинками, чтобы вместо неподгрузившихся картинок, выводились собаки породы корги.

![Build an Instagram Clone with React](/img/barger-build-an-instagram-clone-with-react.jpg 'Build an Instagram Clone with React'){: .center-image }

<br/>

### [Stephen Grider] Microservices with Node JS and React [ENG, 2020]

https://www.udemy.com/course/microservices-with-node-js-and-react/

<br/>

Материал для тех, кому интересны темы docker, kubernetes, react, node.js, typescript, next.js

https://github.com/webmakaka/Microservices-with-Node-JS-and-React

Да тяжело. 54 часа видеоматериалов от топового учителя по соверменным js технологиям.

<br/>

### [Andrei Neagoie, Yihua Zhang] Complete React Developer in 2020 (w/ Redux, Hooks, GraphQL) [ENG, 2019]

**Для меня это лучший курс 2019**

https://github.com/webmakaka/Complete-React-Developer-In-2020-Redux-Hooks-GraphQL

Наверное, это самый интересный и полезный курс по React который смотрел когда-либо.

Но на самом деле он под конец начинает поднадоедать. Мы по сути на один проект то накатываем какие-то технологии, то их скручиваем. То redux-thunk, to redux-saga, to hooks.

<br/>
<br/>

**Обсуждаем всякую ерунду, обменваемся материалами, обсуждаем вакансии <a href="/chat/">в телеграм чате</a>**
