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

### Пожелание по добавлению инструкций для запуска изученных проектов

Пройденные материалы должны оставаться в копилке разработчиков, чтобы к ним можно было вернуться и посмотреть реализацию. Поэтому предлагается подготавливать проект, чтобы его можно было легко запустить человеку, которому нужны примеры решений и он не хочет смотреть курс и тратить на него драгоценное время.

Если изучаете всевозможные курсы или читаете книги, где создают толковые проекты сложнее "hello world", делитесь результатами, чтобы их можно было легко запустить. Например, средствами docker, kubernetes. Сопровождайте проекты инструкциями для запуска.

<br/>

**UPD. Вот здеь удалось подготовить "идеальный" пример, как это можно реализовать.**

[Реопзиторий](https://github.com/webmakaka/Packaging-Applications-with-Helm-for-Kubernetes/)

Внутри простое angular + node + mongodb приложение.

Используется: linux, minikube, helm, docker, skaffold.

Думаю, заслуживает внимания тех, кто сам программирует и интересуется темой контейнеров, kuberntes, ci/cd etc.

С помощью одной команды (после настройки окружения) вы можете развернуть приложение в локальном minikube. Как следствие и на любом другом подготовленном кластере kubernetes. Подготовленный таким образом проект можно разрабатывать прям в kubernetes. Утилита skaffold будет обновлять проект автоматически.

Манифесты kubernetes хранятся в нужном формате, который используется для создания пакетов для быстрой установки приложений и могут быть размещены в хранилищах репозиториев.

Подключив локальный <a href="/devops/ci-cd/gitlab-kubernetes/">GitLab</a>, можно сделать автоматическую сборку и deploy по коммиту или релизу на тестовый или боевой сервер kubernetes.

<br/>

### [nomadcoders.co] Uber Eats Clone [ENG, 2020]

Изучаю вот этот материал. Мне нравится. Осталось изучать 25 часов.

https://www.youtube.com/watch?v=A8-Arx0ql68

**Frontend:** ReactJS. GraphQL. Typescript. Apollo. TailwindCSS

**Backend:** NestJS, Typescript, TypeORM, GraphQL

[Marley](https://github.com/webmakaka/Uber-Eats-Clone)

<br/>

### [Bassir Jafarzadeh] Build Ecommerce Website Like Amazon [React & Node & MongoDB] [ENG, 2021]

Индусятина, но проект кажется интересным для изучения. Особенно для начинающих.

https://www.udemy.com/course/build-ecommerce-website-like-amazon-react-node-mongodb/

<br/>

[**Demo**](https://newamazona-final.herokuapp.com/)

<br/>

Смотреть не стал, проект запустил, оставил исходники.

[**GitHub**](https://github.com/webmakaka/Build-Ecommerce-Website-Like-Amazon-React-Node-MongoDB)

<br/>

### [John Bura] Front-End Web-Dev Masterclass w/ React and Material-UI [ENG, 2021]

Материал кажется интересным. Могу рекомендовать. Сам не шарю в дизайн от слова совсем.

[Marley](https://github.com/webmakaka/Front-End-Web-Dev-Masterclass-with-React-and-Material-UI)

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

35-40 часовой курс.

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
