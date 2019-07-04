# Redux - Action Type

An Action Type is a string that uniquely identifies the type of an Action.
The reason that it is called Action Type and not Action Id is that it uniquely identifies 	__the type of the Action__ and not the instance of the Action object.

Our practice is to name them with an UPPER_SNAKE_CASE string and use our reducer's suffixKey util function which appends a suffix that ensure it will be unique.

```javascript
const LOAD_COURSES = reducer.suffixKey('LOAD_COURSES');
```

The suffixKey util function appends to the given string the reverse path to the reducer's slice name separated by double underscores.


We declare Action Types only inside the Redux Usecase file where they are used and generally we __don't export Action Types__.

An Action Type should only be exported when another Usecase needs to also listen to that Action. This is rare since all logic regarding the handling of an action should be enclosed within the Usecase file which defines that Action Type.



Unit tests will access the Action Types through one exported '*TestPort' object.

```javascript
export const loadCoursesTestPort = {
  LOAD_COURSES,
  LOAD_COURSES_ERROR,
  LOAD_COURSES_SUCCESS,
  ...
};
```
