# Redux - Files Organization

This is how we organize our Redux files (reducer, selectors and usecases) for a given area / domain:

  * area-name/state/area-name.reducer.js
  * area-name/state/area-name.selectors.js
  * area-name/state/area-name.types.js
  * area-name/state/usecases/load-somthing.usecase.js
  * area-name/state/usecases/save-somthing.usecase.js
  * area-name/state/usecases/select-somthing.usecase.js
  * area-name/state/usecases/set-somthing.usecase.js
  * ..
  * area-name/view/


Since Redux is about state management we group Redux files under a parent folder named 'state' to clearly separate these from our view.

One single *.reducer.js file creates and set the initial state of the slice reducer for that area.

One single *.selectors.js files contains all the selectors for that area.
If this become too large a selectors folder may be created contains a few *.selectors.js files.

Types definitions specific to the area can be placed inside the file named *.types.js

All usecases files will be placed inside the usecases folder for the area.