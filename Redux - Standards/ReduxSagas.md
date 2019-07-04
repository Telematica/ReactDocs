# Redux - Sagas

Sagas are ES generator functions run by the ['redux-saga'](https://redux-saga.js.org/) engine. They contain our business logic. We do not use redux-thunk or other redux middlewares.

Sagas run 'watcher' tasks that start a new 'worker' task each time a given Redux Action is dispatched. Accordingly, our Sagas are suffixed with either 'Watch' or 'Worker'.

```javascript
import { mergeSaga } from '@dealersocket/common-react';
 
function* loadCoursesWatch(): any {
  yield takeLatest(LOAD_COURSES, loadCoursesWorker);
}
mergeSaga(loadCoursesWatch);
 
function* loadCoursesWorker(): any {
  const courses = yield select(coursesSelector);
  if (courses && courses.length) {
    return;
  }
  try {
    const result = yield call(loadCourses);
    yield put(createAction(LOAD_COURSES_SUCCESS)(result));
  } catch (e) {
    yield call(showError, e);
    yield put(createAction(LOAD_COURSES_ERROR)(e));
  }
}
```

Only 'Watch" Sagas need to be merged as they run for the life of the application.

Sagas for a given Usecase reside within that Redux Usecase file.

The 'select', 'call', 'put', etc that are yielded from these Sagas are simple JS objects called 'effects' in the redux-saga documentation which express instructions to be executed by the redux-saga engine. This makes it easy to unit test a Saga because as one can manually advance the generator a single step at a time and assert that the yielded object is correct. This can be done without the need to mock any API call.


## Useful Links

[Understanding Generator Functions & Using Redux Saga](https://www.youtube.com/watch?v=o3A9EvMspig)

[Redux-Saga tutorial for beginners and dog lovers](https://hackernoon.com/redux-saga-tutorial-for-beginners-and-dog-lovers-aa69a17db645)

[MDN Iterators and generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators)

[Testing Sagas](https://github.com/redux-saga/redux-saga/blob/master/docs/advanced/Testing.md)