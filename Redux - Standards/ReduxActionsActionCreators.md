# Redux - Actions & ActionCreators

Redux Actions are plain JS objects that have a property named 'type' set to the value of an Action Type.

All Redux Actions we create are [FSA](https://github.com/redux-utilities/flux-standard-action) compliant. We enforce this by generating all Action Creators with the 'createAction' utility function found in the [redux-actions](https://github.com/redux-utilities/redux-actions) package.

We do not allow Action Creators to generate side effects like in Redux-Thunk.

All Redux Actions have the optional property 'payload' to carry any data associated with that action.

```javascript
export const loadCoursesAction = createAction(LOAD_COURSES);
```

All Action Creator functions should be suffixed with the word 'Action'.

The Action Creators function is the only item that a Redux Usecase file will export, with the exception of the single '*TestPort' object to allow unit testing.