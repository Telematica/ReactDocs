# leafReducers

A leafReducer is a reducer that manages a leaf slice; a slice that is not further sub-sliced.

In the reducers' tree the leafReducers are the majority of all reducers.
Usually the redux state is not deeply sub-sliced and the majority of leafReducers are direct children of the rootReducer.
We call these top level leafReducers: __topLeafReducer__ or simply __sliceReducers__.

A leafReducer is __only responsibe to initialize the slice__.


// topLeafReducer.js

```javascript
// @flow
import { createAndMergeSliceReducer } from '@dealersocket/react-common';
 
const sliceName = 'studentSlice';
 
export type StudentSliceType = {
  isLoading: boolean,
  students: null | AuthorType[],
};
 
const initialState: StudentSliceType = {
  isLoading: false,
  students: null,
};
 
export const reducer = createAndMergeSliceReducer(sliceName, initialState);
```


## addActionReducerMap
A leafReducer maintains an internal map of __actionReducers__. It has an __addActionReducerMap__ util function that usecase files use to add the actionReducers that they define.

A leafReducer is like a router. Given the actionType it looks up an actionReducer in its internal actionReducerMap.

* If one is found, that actionReducer is invoked and its result will be returned.

* If none is found then the leafReducer just returns the current slice.

A leafReducer simply delegating the processing of actions to actionReducers.

__addActionReducerMap__

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