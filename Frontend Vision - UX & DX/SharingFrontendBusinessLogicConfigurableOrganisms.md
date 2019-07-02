Sharing Frontend Business Logic & Configurable Organisms
===

We use the ds-ui-react library to share common Atoms and Molecules (UI components) across many applications (projects) developed by several Tribes.
Creating a new Tribe specific components library to share Tribe specific Atoms and Molecules (UI components) can also be easily done as/if needed.

Sharing Frontend Business Logic and Configurable Organism it is a bit more complex (and we didn't implement this yet).
This document describes how we intend to implement it.


Shared Frontend Business Logic
---

Sharing frontend business logic, it means reusing Usecases and Selectors across many applications (projects).

Like any JavaScript reusable code, it needs to be packaged into an NPM package that can be stored in our private Artifactory NPM registry.

A Usecase acts on one slice of the redux state and Selectors expose data from one slice of the redux state.
A Usecase can also listen for ActionTypes defined by an other Usecase that acts on a different slice or call an ActionCreator function that acts on a different slice.
A Selector can compose other Selectors that expose data from a different slice.

Therefore packaging frontend business logic for reuse means packaging redux slices that may depend on other slices.

Reducers
---

* Application's RootReducer
  * Package's ModuleReducer
    * Package's SliceReducer A
    * Package's SliceReducer B
    * Package's SliceReducer C
    * ...

The proposed implementation is to have all Slices inside a package be combined in one Module Slice created by one *ModuleReducer*.
The ModuleReducer combines all the SliceReducers defined in the package.
The ModuleReducer is the only reducer that will be combined into the hosting application's RootReducer.


Auto-Wring Reducers
---

Our redux utility helper functions will allow all reducers to be auto-wired (combined) automatically as Usecase's ActionCreator, ActionType or Selector are imported by the hosting application.

Importing a Usecase's ActionCreator, ActionType or Selector will import the SliceReducer which will import the ModuleReducer which will be created and combined into the application's RootReducer

If an imported Usecase or Selector depends on other slices, those SliceReducers will also be guaranteed to be created, initialized and combined.

Shared Frontend Business Logic - Package Requirements
---

* Must have one ModuleReducer
* All SliceReducers must auto-wire (combine) into the ModuleReducer
* It only exports ActionCreator functions, ActionTypes and Selectors
* Defines the keys and default values that need to be present in the app.settings.json
* May depend on other Frontend Business Logic packages
* It does not depend on ds-ui-react since there are no UI components (only Business Logic)


Shared Configurable Organisms
---

A Shared Configurable Organism is often a Page, Dialog or Panel that is reused inside several Applications (projects).
The Shared Configurable Organism is configured via props and it is self sufficient, meaning that it has all the behaviors and knows how to retrieve the data that it needs to do his job.

We build a Shared Configurable Organism by creating a Connected Component. 
The Connected Component imports ActionCreators functions and Selectors and therefore it is dependent on one or more redux slices.


Shared Configurable Organisms - Package Requirements
---

* Export One or more Connected Component
* Depends and uses ds-ui-react components
* Depends on Frontend Business Logic (ActionCreator functions, ActionTypes and Selectors)



Shared Connected Components can be packaged in separate NPM packages from the one containing the Front Business Logic they depend on.
Often to reduce the number of NPM packages needed and following [the common reuse principle](http://wiki.c2.com/?CommonReusePrinciple) we can package Connected Components inside the same package that hosts the primary redux slices that they depend on.
However using a mono repo it is simpler to manage and publish multiple packages if so desired.

If the Frontend Business Logic is only there to support a Connected Component it will be packaged together.
Otherwise when the Frontend Business Logic is meant to be reusable, it should be packaged separately to better maintain a clear and documented interface that is not only tailored for a specific Connected Component..