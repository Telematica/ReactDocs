rootReducer
===


A Redux application has a single rootReducer, which reference is passed as the first argument in Redux's [createStor](https://redux.js.org/api/createstore).

The rootReducer is created by using Redux's [combineReducers](https://redux.js.org/api/combinereducers) function to combine all topReducers.

A TopReducer is a reducer that is a direct child of the rootReducer.


## createRootReducer

To allow topReducers to be lazy loaded and auto-wired (dynamically added to the rootReducer) the application defines a createRootReducer function.

// createRootReducer.js  
```javascript
// @flow
import { combineReducers } from 'redux';
import { reducer as formReducer } from 'redux-form';
import { connectRouter } from 'connected-react-router';
import { commonReducers, getHistory } from '@dealersocket/react-common';
import { reducer as languageReducer } from 'shared/language/language.reducer';
import { reducer as navReducer } from 'shared/nav/nav.reducer';
 
/**
 * Creates the root reducer by combining the static topReducers
 * with the asynchronously loaded ones.
 * Note: If we were to do this in store.js, reducers wouldn't be hot reloadable.
 */
export function createRootReducer(asyncTopReducers: any) {
  let topReducers = {
    form: formReducer,
    language: languageReducer,
    nav: navReducer,
    ...commonReducers,
    ...asyncTopReducers,
  };
 
  const history = getHistory();
  if (history) {
    topReducers = {
      // 'router' key required by 'connected-react-router'
      router: connectRouter(history),
      ...topReducers,
    };
  }
 
  return combineReducers(topReducers);
}
```


## configureStore

The createRootReducer function is imported in configureStore and is passed into storeHelper.init() with a reference to the store. 


// configureStore.js
```javascript
import { createStore, applyMiddleware, compose } from 'redux';
import { routerMiddleware } from 'connected-react-router';
import createSagaMiddleware from 'redux-saga';
import {
  initMergeSaga,
  storeHelper,
} from '@dealersocket/react-common';
 
import { createRootReducer } from './create-root-reducer';
 
export function configureStore(
  initialState: any,
  history: any
) {
  const sagaMiddleware = createSagaMiddleware();
 
  const middlewares = [
    routerMiddleware(history),
    sagaMiddleware,
  ];
 
  const enhancers = [applyMiddleware(...middlewares)];
 
  // If Redux DevTools Extension is installed use it, otherwise use Redux compose
  /* eslint-disable no-underscore-dangle */
  const composeEnhancers =
    process.env.NODE_ENV !== 'production' &&
    typeof window === 'object' &&
    window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__
      ? window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__
      : compose;
  /* eslint-enable */
 
  const store = createStore(
    createRootReducer(),
    initialState,
    composeEnhancers(...enhancers)
  );
  // Extensions
  store.asyncReducers = {}; // Async reducer registry
  store.sagaMiddleware = sagaMiddleware;
 
  // Make create-root-reducer hot reloadable, see http://mxs.is/googmo
  /* istanbul ignore next */
  if (module.hot) {
    module.hot.accept('./create-root-reducer', () => {
      import('./create-root-reducer').then((createRootReducerModule) => {
        const newRootReducer = createRootReducerModule.createRootReducer(
          store.asyncReducers
        );
        store.replaceReducer(newRootReducer);
      });
    });
  }
 
  initMergeSaga(sagaMiddleware);
  storeHelper.init(store, createRootReducer);
 
  return store;
}
```



## replaceReducer

This allows redux-utils to use the createRootReducer function to create new versions of the rootReducer, that adds newly lazy loaded and auto-wired topReducers.
redux-utils will use the store replaceReducer function to replace the current [rootReducer](https://redux.js.org/api/store#replaceReducer) with the newly created one.

This is how topReducers are "auto-magically" added into the rootReducer. The rootReducer is replaced. A good example of immutability.  

