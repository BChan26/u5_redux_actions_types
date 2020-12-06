# Redux Actions and Types

### Requirements

- Have part two of the Todo List working.

## What Are Actions

In redux actions are functions that provide a type and a payload, these functions are used to update our state. Redux uses the types to track which and any change was performed at any given time.

We `dispatch` actions from our components. By importing our our actions into the component we want to use them in.

Heres an example of an action:

```js
const AddTodo = (todo) => ({
  type: 'ADD_TODO',
  payload: todo
})
```

Our action returns an object with the type of action we are performing and a payload being the item we want to add or use to update our state.

## Building Actions For Our Todo List

Let's start by creating a `types.js` file in our `store` directory.

Next create an `actions` folder inside of the `store` directory.
In the `actions` folder create a new file called `TodoActions.js`.
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
- Accepts a todo as an argument.
- It implicity returns an object with a type of `ADD_TODO` and a payload being the todo we want to add.

Now one thing you may notice is we're setting the type here as a string that we typed in. This is fine and good, but what if we make a mistake while typing it? In that case Redux has no idea what this function is supposed to be doing. This is where our `types` file comes in. We can store our action types here as variables and re-use them without having to worry about typos as our application grows.

## Declaring Action Types

Open your `types.js` file. Let's add our first type:

```js
export const ADD_TODO = 'ADD_TODO'
```

Now in your `TodoActions` import this type, remember since we're using the `export const` syntax we'll have to use the destructuring import syntax.

Your `TodoActions.js` file should look like the following:

```js
import { ADD_TODO } from '../types'

export const AddTodo = (todo) => ({
  type: 'ADD_TODO',
  payload: todo
})
```

Now swap out the type in the `AddTodo` function to our new `ADD_TODO` variable.

```js
import { ADD_TODO } from '../types'

export const AddTodo = (todo) => ({
  type: ADD_TODO,
  payload: todo
})
```

Now in your `TodoReducer.js` do the same.

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

## You Do 10 Min

Create two new types:

- NEW_TODO
- REMOVE_TODO

Create two new actions:

- CreateNewTodo
- RemoveTodo

The `CreateNewTodo` should accept a form value as an argument.

The `RemoveTodo` should accept an index as an argument.

## Resources

[Redux Actions For Beginners](https://www.tutorialspoint.com/redux/redux_actions.htm)
