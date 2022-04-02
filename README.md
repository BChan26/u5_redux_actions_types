# Redux Actions and Types

![](https://redux.js.org/img/tutorials/essentials/ReduxDataFlowDiagram.gif)

## Overview
In this lesson, we'll be learning about Actions in Redux, specifically how and where they fit in with the Reducers that we've set up thus far. We'll also breakdown the Types and Payloads involved with Actions.

## Objectives

- Learn about Actions and Types
- Build out Actions and Types


## Getting Started
- Have the code from the `redux reducers` lesson working.

___
## What Are Actions?

In Redux, Actions are functions that provide a Type and a Payload. These functions are used to update our state. Redux uses the Types to track if any change was performed and on which piece of state at any given time.

We `dispatch` Actions from our components by importing our Actions into the components we want to use them in.

Heres an example of an action:

```js
const AddTodo = (todo) => ({
  type: 'ADD_TODO',
  payload: todo
})
```

Our Action returns an object with the type of action we are performing and a Payload being the item we want to add or use to update our state.

## Building Actions For Our Todo List

Let's start by creating a `types.js` file in our `store` directory.

Next, create an `actions` folder inside of the `store` directory.
In the `actions` folder, create a new file called `TodoActions.js`.
This file will hold all of the actions to handle our `todoState`.

Add the following function to `TodoActions.js`:

```js
export const AddTodo = (todo) => ({
  type: 'ADD_TODO',
  payload: todo
})
```

Let's break this down:

- We're exporting a function called `AddTodo`.
- Accepts a `todo` as an argument.
- It implicity returns an object with a type of `ADD_TODO` and a Payload of the todo we want to add.

Now, one thing you may notice is that we're setting the Type here as a string that we typed in. This is all well and good, but what if we make a mistake while typing it? In that case, Redux has no idea what this function is supposed to be doing. This is where our `types` file comes in. We can store our Action Types here as variables and re-use them without having to worry about typos as our application grows.

## Declaring Action Types

Open your `types.js` file. Let's add our first Type:

```js
export const ADD_TODO = 'ADD_TODO'
```

Now in your `TodoActions`, import this Type. Remember, since we're using the `export const` syntax we'll have to use the destructuring import syntax.

Your `TodoActions.js` file should look like the following:

```js
import { ADD_TODO } from '../types'

export const AddTodo = (todo) => ({
  type: 'ADD_TODO',
  payload: todo
})
```

Now, swap out the Type in the `AddTodo` function to our new `ADD_TODO` variable.

```js
import { ADD_TODO } from '../types'

export const AddTodo = (todo) => ({
  type: ADD_TODO,
  payload: todo
})
```

Now, in your `TodoReducer.js`, do the same:

```js
import { ADD_TODO } from '../types'

const initialState = {
  todos: [],
  newTodo: ''
}

const TodoReducer = (state = initialState, action) => {
  switch (action.type) {
    case ADD_TODO:
      return { ...state, todos: [...state.todos, action.payload] }
    case 'NEW_TODO':
      return { ...state, newTodo: action.payload }
    default:
      return { ...state }
  }
}

export default TodoReducer
```

___
## You Do: 10 Mins

Create two new Types:

- NEW_TODO
- REMOVE_TODO

Create two new Actions:

- CreateNewTodo
- RemoveTodo

The `CreateNewTodo` should accept a form value as an argument.

The `RemoveTodo` should accept an index as an argument.

Change the `NEW_TODO` case in the `TodoReducer` to your new NEW_TODO variable.

Add a new case to the `TodoReducer` for REMOVE_TODO. It should return a new object with everything in state for now. **Hint**: Look at the default case.

___
## Recap
In this lesson, we learned about writing functions for Actions, setting up a Payload, and creating Types associated with each Action.

## Resources
- [Redux Actions For Beginners](https://www.tutorialspoint.com/redux/redux_actions.htm)
