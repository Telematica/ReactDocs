# Redux - Selectors

Selectors are functions which take Redux State and output something of use to the application.
They are always used in the 'mapStateToProps' function of container components but also frequently used in Usecase files inside Saga workers.

Only the initial state of the reducer, the reducerHandlers and the Selectors are aware of where a given piece of data is stored inside the Redux Store.
With selectors it is easier to refactor where a piece of data gets stored inside the Redux Store as that knowledge is not littered throughout the rest of the application. 

Since the 'mapStateToProps' function is executed each time the Redux State changes, selectors code should be as efficient as possible.

The 'createSelector' function from the '[reselect](https://github.com/reduxjs/reselect)' package allows us to compose selectors and memoize the result.
This is an efficient solution as the selector code will only execute when the result from one of the composed selectors changes.

```javascript
import { createSelector } from 'reselect';
import { reducer } from './dallas-class.reducer';
 
const sliceSelector = (state) => state[reducer.sliceName];
 
export const coursesSelector = createSelector(
  sliceSelector,
  (slice) => slice.courses
);
```

All Selector functions should be suffixed with the word 'Selector'.

Usually, all selectors for a given slice are exported from a file named {domain-name}.selectors.js