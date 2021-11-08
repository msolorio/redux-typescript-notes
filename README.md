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
