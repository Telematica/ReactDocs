# actionReducers

actionReducers are specialized reducers written for a specific slice and specific action type.

actionReducers are the __only reducer functions that we actually write__.

## actionReducerMap
Each usecase file defines its actionReducers inside an actionReducerMap.

The key is the actionType.
The value is the actionReducer function that takes the current slice and the action object and returns a new slice.

// actionReducerMap.js

```javascript
const actionReducerMap = {
  [LOAD_STUDENTS]: (slice) => {
    return {
      ...slice,
      isLoading: true,
      students: null,
    };
  },
  [LOAD_STUDENTS_ERROR]: (slice) => {
    return {
      ...slice,
      isLoading: false,
    };
  },
  [LOAD_STUDENTS_SUCCESS]: (slice, action) => {
    return {
      ...slice,
      isLoading: false,
      students: action.payload,
    };
  },
};

reducer.addActionReducerMap(actionReducerMap);
```

The actionReducers are added to the leafReducer using the __addActionReducerMap__ util function of the __leafReducer__.