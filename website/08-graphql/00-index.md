---
layout: page
title: GraphQL
description: GraphQL
keywords: grqphql
permalink: /grqphql/
---

# GraphQL

Есть:

- Query
- Mutation
- Subscription

<br/>

- GraphiQL (Facebook)
- GraphQL Playground (Prisma) (Предпочтительнее)

<br/>

### Query

```
{
  allLifts {
    name
  }
}
```

```
$ curl 'http://snowtooth.herokuapp.com/' \
-H 'Content-Type: application/json' \
--data '{"query":"{ allLifts {name }}"}'
```

<br/>

### Mutation

```
mutation {
    setLiftStatus(id: "panorama" status: OPEN) {
    name
    status
  }
}
```

<br/>

```
$ curl 'http://snowtooth.herokuapp.com/' \
  -H 'Content-Type: application/json' \
  --data '{"query":"mutation {setLiftStatus(id: \"panorama\" status: OPEN) {name status}}"}'
```

<br/>

snowtooth.mo­onhighway.com/

<br/>

```
query {
  allLifts {
    name
    status
  }
}
```

```
query trails {
  allTrails {
    name
    difficulty
    }
}
```

```
query liftsAndTrails {
liftCount(status: OPEN)
  allLifts {
  name
  status
}
allTrails {
  name
  difficulty
  }
}
```

```
query liftsAndTrails {
  open: liftCount(status: OPEN)
    chairlifts: allLifts {
      liftName: name
      status
  }
  skiSlopes: allTrails {
    name
    difficulty
  }
}
```

```
query closedLifts {
  allLifts(status: CLOSED) {
    name
    status
  }
}
```

```
query jazzCatStatus {
  Lift(id: "jazz-cat") {
    name
    status
    night
    elevationGain
  }
}
```

```
query trailsAccessedByJazzCat {
  Lift(id: "jazz-cat") {
    capacity
    trailAccess {
      name
      difficulty
    }
  }
}
```

```
query liftToAccessTrail {
  Trail(id: "dance-fight") {
    groomed
    accessedByLifts {
      name
      capacity
    }
  }
}

```

<br/>

### Фрагменты

```
fragment liftInfo on Lift {
  name
  status
  capacity
  night
  elevationGain
}

query {
  Lift(id: "jazz-cat") {
    ...liftInfo
    trailAccess {
      name
      difficulty
    }
  }
  Trail(id: "river-run") {
    name
    difficulty
    accessedByLifts {
      ...liftInfo
    }
  }
}

```

```
query {
  Lift(id: "jazz-cat") {
    ...liftInfo
    trailAccess {
      ...trailInfo
    }
  }
  Trail(id: "river-run") {
    ...trailInfo
    groomed
    trees
    night
  }
}
fragment trailInfo on Trail {
  name
  difficulty
  accessedByLifts {
    ...liftInfo
  }
}
fragment liftInfo on Lift {
  name
  status
  capacity
  night
  elevationGain
}

```

<br/>

### Мутации

```
mutation createSong {
  addSong(title: "No Scrubs", numberOne: true, performerName: "TLC") {
    id
    title
    numberOne
  }
}

```

```
mutation createSong($title: String!, $numberOne: Int, $by: String!) {
  addSong(title: $title, numberOne: $numberOne, performerName: $by) {
    id
    title
    numberOne
  }
}
```

Здаются в окне Query Variables:

```
{
  }
    "title": "No Scrubs",
    "numberOne": true,
    "by": "TLC"
  }
}
```

<br/>

### Подписки

Клиент хочет получать обновления в реальном времени с сервера.

<br/>

```
subscription {
  liftStatusChange {
    name
    capacity
    status
  }
}
```

```
mutation closeLift {
  setLiftStatus(id: "astra-express", status: HOLD) {
    name
    status
  }
}

```

<br/>

### Самодиагностика

```
query {
  __schema {
    types {
      name
      description
    }
  }
}
```

```
query liftDetails {
  __type(name: "Lift") {
    name
    fields {
      name
      description
      type {
        name
      }
    }
  }
}
```

```
query roots {
  __schema {
    queryType {
      ...typeFields
    }
    mutationType {
      ...typeFields
    }
    subscriptionType {
      ...typeFields
    }
  }
}
fragment typeFields on __Type {
  name
  fields {
    name
  }
}
```

<br/>

**некоторые широко применяемые пользовательские скалярные типы:**  
https://www.npmjs.com/package/graphql-custom-types

<br/>

**один к одному**

У каждого фото свой пользователь.

```
type User {
githubLogin: ID!
name: String
avatar: String
}

type Photo {
id: ID!
name: String!
url: String!
description: String
created: DateTime!
category: PhotoCategory!
postedBy: User!
}
```

<br/>

### один ко многим

```
type User {
githubLogin: ID!
name: String
avatar: String
postedPhotos: [Photo!]!
}
```

<br/>

### многие ко многим

```
type User {
...
inPhotos: [Photo!]!
}

type Photo {
...
taggedUsers: [User!]!
}

```
