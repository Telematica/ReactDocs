# Redux - Reducers & reducerHandlers

Redux Reducers are pure functions that take the current State and Action and return a new State or the existing State.
Reducers can be composed. The application rootReducer is usually composed of many sliceReducers.

A sliceReducer is a reducer that is responsible for managing one slice of the overall application state.

We have a helper function 'createSliceReducer' for sliceReducer creation, but generally we use the 'createAndMergeSliceReducer' helper function as it additionally merges (adds) the newly created sliceReducer to the application rootReducer.

```javascript
import { createAndMergeSliceReducer } from '@dealersocket/common-react';
const sliceName = 'courseSlice';
const initialState = {
  courses: null,
  selectedCourseId: null,
};
export const reducer = createAndMergeSliceReducer(sliceName, initialState);
```
The created sliceReducer function has a property 'sliceName' set to the name of its slice. This allows us to define the slice name in a single place and use it later across our Selector and Usecase files.

The created sliceReducer function has a method 'addHandlers' that is used in our Usecase files for adding the reducerHandlers for a given UseCase.


reducerHandlers 
===

A sliceReducer needs to handle all possible updates of that slice of the Redux State for any Redux Actions.

Instead of a big (ugly) switch statement in the reducer file containing all update logics for all Redux Actions, each individual Redux Usecase file adds the their specific reducerHandlers logic to the sliceReducer.
This ensures all logic regarding a Usecase stays within the Redux Usecase file.

```javascript
const reduceHandlers = {
  [LOAD_COURSES_SUCCESS]: (slice, action) => {
    return {
      ...slice,
      courses: action.payload,
    };
  },
};
reducer.addHandlers(reduceHandlers);
```

The reduceHandlers added to the Reducer are just plain JS objects where the keys are the Action Types and the values are the reducer functions that handle that Action.

Note how we return a new slice object by expanding in place all the current properties of the current slice using the [spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) ...slice and replacing the courses property with the value of action payload.