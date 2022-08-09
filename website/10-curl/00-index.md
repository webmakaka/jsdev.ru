---
layout: page
title: Curl
description: Curl
keywords: curl
permalink: /curl/
---

# Curl

<br/>

[Приложение](https://github.com/webmak1/Rolling-Scopes-School-Nodejs-Course-Task-3-broken-app)

<br/>

```
// SIGN UP
// POST
$ curl \
    --data '{
      "fullName":"Marley",
      "userName":"marley",
      "password":"123456789",
      "email":"marley1@example.com"}' \
    --header "Content-Type: application/json" \
    --request POST \
    --url http://localhost:4000/api/auth/signup \
    | jq
```

<br/>

```
// SIGN IN
// POST
$ curl \
    --data '{
      "userName":"marley",
      "password":"123456789"}' \
    --header "Content-Type: application/json" \
    --request POST \
    --url http://localhost:4000/api/auth/signin \
    | jq
```

<br/>

**returns**

```
***
"sessionAUTH_TOKEN": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiaWF0IjoxNjIxMzc4OTkxLCJleHAiOjE2MjE0NjUzOTF9.EXHGuiebq97etqCFXTh9wVBNvFcTpK-fpwIAd7OlC0w"
***
```

<br/>

```
$ export AUTH_TOKEN=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiaWF0IjoxNjIxMzc4OTkxLCJleHAiOjE2MjE0NjUzOTF9.EXHGuiebq97etqCFXTh9wVBNvFcTpK-fpwIAd7OlC0w


$ echo ${AUTH_TOKEN}
```

<br/>

```
// CREATE THE GAME 1
// POST
$ curl \
    --data '{
      "title":"Starcraft 2",
      "studio":"Blizzard",
      "esrbRating":"8",
      "userRating":"5",
      "havePlayed":"True"
      }' \
    --header "Content-Type: application/json" \
    --header "Authorization: Bearer ${AUTH_TOKEN}" \
    --request POST \
    --url http://localhost:4000/api/game/create \
    | jq
```

<br/>

```
// CREATE THE GAME 2
// POST
$ curl \
    --data '{
      "title":"Quake 2",
      "studio":"ID Software",
      "esrbRating":"5",
      "userRating":"4",
      "havePlayed":"NO"
      }' \
    --header "Content-Type: application/json" \
    --header "Authorization: Bearer ${AUTH_TOKEN}" \
    --request POST \
    --url http://localhost:4000/api/game/create \
    | jq
```

<br/>

```
// CREATE THE GAME 3
// POST
$ curl \
    --data '{
      "title":"Dead Space 3",
      "studio":"Visceral Games",
      "esrbRating":"3",
      "userRating":"3",
      "havePlayed":"YES"
      }' \
    --header "Content-Type: application/json" \
    --header "Authorization: Bearer ${AUTH_TOKEN}" \
    --request POST \
    --url http://localhost:4000/api/game/create \
    | jq
```

<br/>

```
// GET ALL GAMES
// GET
$ curl \
    --header "Content-Type: application/json" \
    --header "Authorization: Bearer ${AUTH_TOKEN}" \
    --request GET \
    --url http://localhost:4000/api/game/all \
    | jq
```

<br/>

```
// DELETE GAME
// DELETE
$ curl \
    --header "Content-Type: application/json" \
    --header "Authorization: Bearer ${AUTH_TOKEN}" \
    --request DELETE \
    --url http://localhost:4000/api/game/remove/3 \
    | jq
```

<br/>

```
// GET BY ID
// GET
$ curl \
    --header "Content-Type: application/json" \
    --header "Authorization: Bearer ${AUTH_TOKEN}" \
    --request GET \
    --url http://localhost:4000/api/game/2 \
    | jq
```

<br/>

```
// UPDATE
// PUT
$ curl \
    --data '{
      "title":"Diablo 3",
      "studio":"Blizzard",
      "esrbRating":"2",
      "userRating":"2",
      "havePlayed":"NO"
      }' \
    --header "Content-Type: application/json" \
    --header "Authorization: Bearer ${AUTH_TOKEN}" \
    --request PUT \
    --url http://localhost:4000/api/game/update/2 \
    | jq
```

<br/>

### Загрузка файла на сервер с помощью curl

<br/>

```
// UPLOAD FILE
// POST
$ curl \
    -F "files=@/home/marley/Pictures/rs.png" \
    --header "Content-Type: multipart/form-data" \
    --header "Authorization: Bearer ${AUTH_TOKEN}" \
    --request POST \
    --url "http://localhost:3000/api/files/upload" \
    | jq
```

<br/>

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

<br/>

// Получить код ответа на curl запрос

```
$ curl -s -o /dev/null -w "%{http_code}" \
    -H "Content-Type: application/json" \
    -X GET \
    --url localhost:4000/users \
    --header "Authorization: Bearer ${AUTH_TOKEN}"
```

<br/>

### Усложненные, требующие оптимизации и доработки

<br/>

```
$ AUTH_TOKEN=$(curl \
     --data '{
       "username":"username",
       "password":"12345678",
       "Authorization":"Basic Y2xpZW50OnNIY3JidA=="
       }' \
     --header "Content-Type: application/json" \
     --request POST http://api/oauth/AUTH_TOKEN \
     | jq -r '.access_AUTH_TOKEN')
```

<br/>

```
$ echo ${AUTH_TOKEN}
```

<br/>

```
//OK!
{
REQ_METHOD=GET
ENDPOINT_URL=http://someendpoint

USERNAME=guest
USERPASSWORD=user
AUTH_KEY=Basic Y2xpZW50OnNIY3JidA==

auth_data()
{
  cat << EOF
{
  "username": "${USERNAME}",
  "password": "${USERPASSWORD}",
  "Authorization":"${AUTH_KEY}"
}
EOF
}

AUTH_TOKEN=$(curl \
     --data "$(auth_data)" \
     --header "Content-Type: application/json" \
     --request POST http://someendpoint/oauth/AUTH_TOKEN \
     | jq -r '.access_AUTH_TOKEN')

curl \
    --header "Content-Type: application/json" \
    --header "Authorization: Bearer ${AUTH_TOKEN}" \
    --request "${REQ_METHOD}" \
    --url "${ENDPOINT_URL}" \
    | jq
}
```

<br/>

### Basic Auth example

<br/>

```
// GET
$ curl -u username:password \
    --header "Content-Type: application/json" \
    --request GET \
    --url http://localhost:8080/management/api/v1/students \
    | jq
```

<br/>

```
// PUT
$ curl -u tom:password123 \
    --header "Content-Type: application/json" \
    --data '{
      "studentName":"Alex Gomes"}' \
    --request PUT \
    --url http://localhost:8080/management/api/v1/students/1 \
    | jq
```

<br/>

Чекнуть, когда-нибудь

https://stackoverflow.com/questions/25969196/how-to-define-the-basic-http-authentication-using-curl-correctly

<br/>

```
AUTH=$(echo -ne "$BASIC_AUTH_USER:$BASIC_AUTH_PASSWORD" | base64 --wrap 0)

curl \
  --header "Content-Type: application/json" \
  --header "Authorization: Basic $AUTH" \
  --request POST \
  --data  '{"key1":"value1", "key2":"value2"}' \
  --url https://example.com/
```

<br/>

https://www.ibm.com/docs/en/connect-direct/6.0.0?topic=apis-example-1-submit-process-using-curl

<br/>

### Kubernetes

```
kubectl run -i --rm --restart=Never curl-client --image=curlimages/curl --command -- curl -s 'http://nginx-service:80'
```
