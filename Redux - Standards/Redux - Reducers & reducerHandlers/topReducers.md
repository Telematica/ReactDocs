# topReducers

topReducers are reducers that are direct children of the rootReducer.

topReducers are either combineReducers or leafReducers. We will call them topCombineReducer or topLeafReducer.


## topLeafReducers a.k.a. sliceReducers

In a simple Redux apps the store's state is only sliced one level deep and therefore all topReducers will be topLeafReducers.

Generally there is no need to deeply sub-slice the redux state, therefore in practice the majority of topReducers are topLeafReducers.

Because topLeafReducers are so common we simply refer to them as sliceReducers.


## topCombineReducers
A topCombineReducer is a combineReducer that is a direct child of the rootReducer.

We don't use many topCombineReducers.

Our Redux libraries of shared slices use a topCombineReducer to combine all the reducers in the library under a single slice.
redux-utils has a createAndMergeModuleReducer function that creates a topCombineReducer and merges it into the rootReducer.

```javascript
import { createAndMergeModuleReducer } from '@dealersocket/redux-utils';
 
export const moduleTopReducer = createAndMergeModuleReducer('dsRxCrm');
```

This allows all the slices defined in a redux library to be sub-sliced of the moduleTopReducer's slice.
This grouping helps visually separate those slices created by the imported library versus those slices created by the application.
It also avoids slice name conflicts.


## newLeafReducer

In the Redux library then one can create a new leafReducer using the newLeafReducer util function of the combineReducer.

// newLeafReducer.js

```javascript
import { moduleTopReducer } from '../../internal/module-top.reducer';
 
const sliceName = 'vehicleImageSlice';
 
export const initialState = {
  cache: [],
};
 
export const reducer = moduleTopReducer.newLeafReducer(sliceName, initialState);
```

## newCombineReducer
The combineReducer also has a newCombineReducer util function of create a sub combineReducer.