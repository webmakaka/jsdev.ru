---
layout: page
title: Curl
description: Curl
keywords: curl
permalink: /curl/
---

# Curl

<br/>

```
// SIGN UP
$ curl \
    --data '{
      "fullName":"Marley",
      "userName":"marley",
      "password":"123456789",
      "email":"marley1@example.com"}' \
    --header "Content-Type: application/json" \
    --request POST http://localhost:4000/api/auth/signup \
    | python -m json.tool
```

<br/>

```
// SIGN IN
$ curl \
    --data '{
      "userName":"marley",
      "password":"123456789"}' \
    --header "Content-Type: application/json" \
    --request POST http://localhost:4000/api/auth/signin \
    | python -m json.tool
```

**returns**

```
***
"sessionToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiaWF0IjoxNjIxMzc4OTkxLCJleHAiOjE2MjE0NjUzOTF9.EXHGuiebq97etqCFXTh9wVBNvFcTpK-fpwIAd7OlC0w"
***
```

<br/>

```
// GREATE THE GAME 1
$ curl \
    --data '{
      "title":"Starcraft 2",
      "studio":"Blizzard",
      "esrbRating":"8",
      "userRating":"5",
      "havePlayed":"True"
      }' \
    --header "Content-Type: application/json" \
    --header "authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiaWF0IjoxNjIxMzc4OTkxLCJleHAiOjE2MjE0NjUzOTF9.EXHGuiebq97etqCFXTh9wVBNvFcTpK-fpwIAd7OlC0w" \
    --request POST http://localhost:4000/api/game/create \
    | python -m json.tool
```

<br/>

```
// GREATE THE GAME 2
$ curl \
    --data '{
      "title":"Quake 2",
      "studio":"ID Software",
      "esrbRating":"5",
      "userRating":"4",
      "havePlayed":"NO"
      }' \
    --header "Content-Type: application/json" \
    --header "authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiaWF0IjoxNjIxMzc4OTkxLCJleHAiOjE2MjE0NjUzOTF9.EXHGuiebq97etqCFXTh9wVBNvFcTpK-fpwIAd7OlC0w" \
    --request POST http://localhost:4000/api/game/create \
    | python -m json.tool
```

<br/>

```
// GREATE THE GAME 3
$ curl \
    --data '{
      "title":"Dead Space 3",
      "studio":"Visceral Games",
      "esrbRating":"3",
      "userRating":"3",
      "havePlayed":"YES"
      }' \
    --header "Content-Type: application/json" \
    --header "authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiaWF0IjoxNjIxMzc4OTkxLCJleHAiOjE2MjE0NjUzOTF9.EXHGuiebq97etqCFXTh9wVBNvFcTpK-fpwIAd7OlC0w" \
    --request POST http://localhost:4000/api/game/create \
    | python -m json.tool
```

<br/>

```
// GET ALL GAMES
$ curl \
    --header "Content-Type: application/json" \
    --header "authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiaWF0IjoxNjIxMzc4OTkxLCJleHAiOjE2MjE0NjUzOTF9.EXHGuiebq97etqCFXTh9wVBNvFcTpK-fpwIAd7OlC0w" \
    --request GET http://localhost:4000/api/game/all \
    | python -m json.tool
```

<br/>

```
// DELETE GAME
$ curl \
    --header "Content-Type: application/json" \
    --header "authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiaWF0IjoxNjIxMzc4OTkxLCJleHAiOjE2MjE0NjUzOTF9.EXHGuiebq97etqCFXTh9wVBNvFcTpK-fpwIAd7OlC0w" \
    --request DELETE http://localhost:4000/api/game/remove/3 \
    | python -m json.tool
```

<br/>

```
// GET BY ID
$ curl \
    --header "Content-Type: application/json" \
    --header "authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiaWF0IjoxNjIxMzc4OTkxLCJleHAiOjE2MjE0NjUzOTF9.EXHGuiebq97etqCFXTh9wVBNvFcTpK-fpwIAd7OlC0w" \
    --request GET http://localhost:4000/api/game/2 \
    | python -m json.tool
```

<br/>

```
// UPDATE
$ curl \
    --data '{
      "title":"Diablo 3",
      "studio":"Blizzard",
      "esrbRating":"2",
      "userRating":"2",
      "havePlayed":"NO"
      }' \
    --header "Content-Type: application/json" \
    --header "authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiaWF0IjoxNjIxMzc4OTkxLCJleHAiOjE2MjE0NjUzOTF9.EXHGuiebq97etqCFXTh9wVBNvFcTpK-fpwIAd7OlC0w" \
    --request PUT http://localhost:4000/api/game/update/2 \
    | python -m json.tool
```

<br/>

### Загрузка файла на сервер с помощью curl

<br/>

```
// UPLOAD FILE
$ curl \
    -F "files=@/home/marley/Pictures/rs.png" \
    --header "Content-Type: multipart/form-data" \
    --header "Authorization: Bearer ${TOKEN}" \
    --request POST "http://localhost:3000/api/files/upload" \
    | python -m json.tool
```

Есть и другие какие-то варианты.  
Лучше скачать insomnia и посмотреть в ней.

Обратить внимание на files - если назвать не так как ожидает сервер (в nestjs), будет приходить undefined.

<br/>

[Пример](https://github.com/webmakaka/WebProject)

<br/>

### Примеры:

<br/>

**cookie, insecure**

https://github.com/webmakaka/Microservices-with-Node-JS-and-React-Improved

<br/>

**Токен:**

https://github.com/webmakaka/MERN-Stack-Front-To-Back-v2.0/blob/master/API.md

<br/>

**File Upload:**

https://github.com/webmakaka/Node.js-API-Masterclass-With-Express-MongoDB/blob/master/Development.md
