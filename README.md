## Redux

- A Pattern library for managing state using events or actions.
- A centralized store for global state for use across many parts of application
- Has rules ensuring state is updated in predictable fashion

### Tools
Redux Toolkit
- Redux's recommended way of using Redux
- Simplifies the use of Redux
- Prevents common mistakes

### Big Concepts

#### Action
- A JS object with a type field
- The action describes the event that took place in application
- often has naming convention off "domain/eventName"
- Action object can hold additional information about the event
  - The payload
- Should include minimal amount of information to describe what happened

Example
```js
const addTodoAction = {
  type: 'todos/todoAdded',
  payload: 'Buy milk'
}
```
#### Action Creator
- A function that returns an action object.
- Allows for sending custom data in the payload

Example
```js
const addTodo = (text) => {
  return {
    type: 'todos/todoAdded',
    payload: text
  }
}
```

#### Reducer
- A function that listens for a particular action and updates state
- Takes information from action, current state and runs logic of updating state
- (state, action) => newState
- Named after familiar reduce() method

#### Reducer Rules
- should only operate on the 2 inputs - state and action
- do not modify existing state directly
  - make immutable updates
  - copy existing state and update copy
- Reducer must not have side effects
  - Cannot make AJAX calls
  - run asynchronous code
  - pure functions are more predictable, easier to test
  - un-pure reducers can be a common source of bugs

#### Reducer Steps
1. check action type to determine current procedure
2. copy state
3. update state copy w/new values
4. return state
5. the default returns existing state

#### Store
- Current Redux state lives in store
- store is created by passing in reducer
- has `getState` method that returns current state value

#### Dispatch
- Store contains `dispatch` method
- Recieves action object
- triggers calling the reducer which then updates state

```js
store.dispatch({ type: 'counter/increment });
```

Often an action creator is passed to the `dispatch` method

```js
store.dispatch(increment());
```

#### Selector
- function that extracts specific data from store.
- helps to reduce repeated logic

```js
const selectCounterValue = state => state.value;

const currentVal = selectCounterValue(store.getStore());
```

### Redux Data Flow
1. State describes the current condition of the app
2. The UI is rendered based on the state
3. When an event is triggered
  - action is dispatched
  - reducer function updates state in store
4. Store notifies parts of UI subscribing to store that state has changed
5. UI rerenders with new data

![Redux Data Flow](https://redux.js.org/assets/images/ReduxDataFlowDiagram-49fa8c3968371d9ef6f2a1486bd40a26.gif)

---

### Redux Toolkit - Basic App Steps

1. Install necessary packages
- react-redux
- @reduxjs/toolkit

2. Set up / export the store

3. Pass store to the application via the provider

4. Set up the state slice / reducer for feature
  - set initial state
  - set up the reducer in the slice (handles updating state)
  - export the created actions and the reducer

Redux TypeScript

RootState
- describes the type / shape of state

- Used throughout the application
  - to create a typed version of useSelector (useAppSelector)
  - used to type check state in callback to useAppSelector

Create Typed versions of
- useDispatch (useAppDispatch)
- useSelector (useAppSelector)

### Redux Toolkit - Additional Notes

Reducer Slices
- Slice is a collection of reducer logic and actions for a single feature
- A slice is usually contained in a single file
- Reducer slices are passed to `configureStore` which will call `combineReducers` behind the scenes to create a single reducer.

`createSlice`
- Automatically creates actions that correspond to reducers.
- Allows for writing "mutable" - uses Immer library, works as a proxy to wrap mutable code and make it immutable.
- Immer allows us to not return a state value.

### Thunk Function
A special kind of Redux function that can contain asynchronous logic.




