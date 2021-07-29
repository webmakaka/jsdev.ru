---
layout: page
title: Объяснение Redux на понятном языке
description: Объяснение Redux на понятном языке
keywords: Объяснение Redux на понятном языке
permalink: /client/react/redux/
---

# Объяснение Redux на понятном языке

<br/>

### Что это за Redux и зачем он нужен

<br/>

<div align="center">
    
    <iframe width="853" height="480" src="https://www.youtube.com/embed/jvkhKRHS2TY" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

</div>

<br/>

```js
import { createStore } from 'redux';

const initialState = {
  name: 'Pert',
  lastName: 'Petrov',
};

function reducer(state = initialState, action) {
  switch (action.type) {
    case 'CHANGE_NAME':
      return { ...state, name: action.payload };
    case 'CHANGE_LAST_NAME':
      return { ...state, lastName: action.payload };
  }

  return state;
}

const store = createStore(reducer);

console.log(store.getState());

const changeName = {
  type: 'CHANGE_NAME',
  payload: 'Ivan',
};

const changeLastName = {
  type: 'CHANGE_LAST_NAME',
  payload: 'Ivanov',
};

store.dispatch(changeName);

console.log(store.getState());

store.dispatch(changeLastName);

console.log(store.getState());
```

<br/>

### React и Redux. Подключаемся к Redux

<br/>

<div align="center">
    
    <iframe width="853" height="480" src="https://www.youtube.com/embed/wzWZDh0dUYE" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

</div>

<br/>

**.babelrc**

<br/>

```js
{
"presets": ["react", "es2015", "stage-2"]
}
```

<br/>

**webpack.config.js**

<br/>

```js

---

module: {
rules: [
    {
      test: /\.js$/,
      exclude: /node_modules/,
      use: {
      loader: 'babel-loader'
      }
    }
  ]
},

---

```

<br/>

<br/>

**index.js**

<br/>

```js
import React from 'react';
import ReactDOM from 'react-dom';
import { createStore } from 'redux';
import { connect, Provider } from 'react-redux';

const initialState = {
  firstName: 'Ivan',
  lastName: 'Ivanov',
};

const ACTION_CHANGE_FIRST_NAME = 'ACTION_CHANGE_FIRST_NAME';
const ACTION_CHANGE_LAST_NAME = 'ACTION_CHANGE_LAST_NAME';

const changeFirstName = (newFirstName) => {
  console.log(newFirstName);

  return {
    type: ACTION_CHANGE_FIRST_NAME,
    payload: newFirstName,
  };
};

const changeLastName = (newLastName) => {
  return {
    type: ACTION_CHANGE_LAST_NAME,
    payload: newLastName,
  };
};

const rootReducer = (state = initialState, action) => {
  switch (action.type) {
    case ACTION_CHANGE_FIRST_NAME:
      return { ...state, firstName: action.payload };

    case ACTION_CHANGE_LAST_NAME:
      return { ...state, lastName: action.payload };
  }

  return state;
};

const store = createStore(rootReducer);

class MainComponent extends React.Component {
  render() {
    console.log('MainComponent props');
    console.log(this.props);

    const dispatch = this.props.dispatch;
    const { firstName, lastName } = this.props;

    return (
      <div>
        <div>
          <input
            type="text"
            value={firstName}
            placeholder="First Name"
            onChange={(event) => {
              dispatch(changeFirstName(event.target.value));
            }}
          />{' '}
        </div>
        <div>
          <input
            type="text"
            value={lastName}
            placeholder="Last Name"
            onChange={(event) => {
              dispatch(changeLastName(event.target.value));
            }}
          />{' '}
        </div>

        <div>{`${firstName} ${lastName}`}</div>
      </div>
    );
  }
}
const mapStateToProps = (state) => {
  return {
    firstName: state.firstName,
    lastName: state.lastName,
  };
};

const WrappedMainComponent = connect(mapStateToProps)(MainComponent);

ReactDOM.render(
  <Provider store={store}>
    <WrappedMainComponent />
  </Provider>,
  document.getElementById('app')
);
```

<br/>

Улучшаем

<br/>

**index.js**

<br/>

```js
import React from 'react';
import ReactDOM from 'react-dom';
import { createStore, bindActionCreators } from 'redux';
import { connect, Provider } from 'react-redux';

const initialState = {
  firstName: 'Ivan',
  lastName: 'Ivanov',
};

const ACTION_CHANGE_FIRST_NAME = 'ACTION_CHANGE_FIRST_NAME';
const ACTION_CHANGE_LAST_NAME = 'ACTION_CHANGE_LAST_NAME';

const changeFirstName = (newFirstName) => {
  console.log(newFirstName);

  return {
    type: ACTION_CHANGE_FIRST_NAME,
    payload: newFirstName,
  };
};

const changeLastName = (newLastName) => {
  return {
    type: ACTION_CHANGE_LAST_NAME,
    payload: newLastName,
  };
};

const rootReducer = (state = initialState, action) => {
  switch (action.type) {
    case ACTION_CHANGE_FIRST_NAME:
      return { ...state, firstName: action.payload };

    case ACTION_CHANGE_LAST_NAME:
      return { ...state, lastName: action.payload };
  }

  return state;
};

const store = createStore(rootReducer);

class MainComponent extends React.Component {
  render() {
    console.log('MainComponent props');
    console.log(this.props);

    const dispatch = this.props.dispatch;
    const { firstName, lastName, changeFirstName, changeLastName } = this.props;

    return (
      <div>
        <div>
          <input
            type="text"
            value={firstName}
            placeholder="First Name"
            onChange={(event) => {
              changeFirstName(event.target.value);
            }}
          />{' '}
        </div>
        <div>
          <input
            type="text"
            value={lastName}
            placeholder="Last Name"
            onChange={(event) => {
              changeLastName(event.target.value);
            }}
          />{' '}
        </div>

        <div>{`${firstName} ${lastName}`}</div>
      </div>
    );
  }
}
const mapStateToProps = (state) => {
  return {
    firstName: state.firstName,
    lastName: state.lastName,
  };
};

// putActionsToProps
const mapDispatchToProps = (dispatch) => {
  return {
    changeFirstName: bindActionCreators(changeFirstName, dispatch),
    changeLastName: bindActionCreators(changeLastName, dispatch),
  };
};

const WrappedMainComponent = connect(
  mapStateToProps,
  mapDispatchToProps
)(MainComponent);

ReactDOM.render(
  <Provider store={store}>
    <WrappedMainComponent />
  </Provider>,
  document.getElementById('app')
);
```
