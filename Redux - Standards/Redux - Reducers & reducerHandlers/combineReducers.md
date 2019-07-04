# combineReducers

If a given slice needs to be sub-sliced then a combineReducer will be used to combine those reducers that manage the sub-slices.

The children of a combineReducer can be other combineReducers and leafReducers. Therefore there is no limit on how deep a slice can be sub-sliced.

A topCombineReducer is a combineReducer that is a direct child of the rootReducer.

Generally there is no need to deeply sub-slice the redux state, therefore we use few combineReducers.