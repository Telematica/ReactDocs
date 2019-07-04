Redux - Usecases

The Redux Usecase design pattern co-locates an Action Creator, Action Types, reducerHandlers, and Sagas in a single ES file named {some-name}.usecase.js.

The Action Creator function is the only item exported by a Redux Usecase file.


```javascript
import { createAction } from 'redux-actions';
import { call, put, select, takeLatest } from 'redux-saga/effects';
import { axiosApi, getAppSettings, mergeSaga } from '@dealersocket/common-react';
import { reducer } from '../course.reducer';
 
const prefix = `app/${reducer.sliceName}/`;
 
const LOAD_COURSES: string = `${prefix}LOAD_COURSES`;
export const loadCoursesAction = createAction(LOAD_COURSES);
const LOAD_COURSES_SUCCESS: string = `${prefix}LOAD_COURSES_SUCCESS`;
const LOAD_COURSES_ERROR: string = `${prefix}LOAD_COURSES_ERROR`;
 
function* loadCoursesWatch(): any {
  yield takeLatest(LOAD_COURSES, loadCoursesWorker);
}
mergeSaga(loadCoursesWatch);
 
function* loadCoursesWorker(): any {
  try {
    const result = yield call(loadCourses);
    yield put(createAction(LOAD_COURSES_SUCCESS)(result));
  } catch (e) {
    yield put(createAction(LOAD_COURSES_ERROR)(e));
  }
}
 
function loadCourses(): Promise<any> {
  return axiosApi(`${getAppSettings().globalApiUrl}/sandbox/courses`);
}
 
const reduceHandlers = {
  [LOAD_COURSES_SUCCESS]: (state, action) => {
    return {
      ...state,
      courses: action.payload,
    };
  },
};
reducer.addHandlers(reduceHandlers);
```

To allow unit testing we export one additional '*TestPort' object which exposes the internals of the Usecase file for unit testing.

```javascript
export const loadCoursesTestPort = {
  LOAD_COURSES,
  LOAD_COURSES_ERROR,
  LOAD_COURSES_SUCCESS,
  loadCoursesWatch,
  loadCoursesWorker,
  loadCourses,
  reduceHandlers,
};
```

Useful Links
[5 - Usecase Pattern](https://dealersocket.atlassian.net/wiki/spaces/REACT/pages/148858967/5+-+Usecase+Pattern)