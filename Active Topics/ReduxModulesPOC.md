Redux Modules POC
=

We know how to build controlled React components and we have a template to build React applications.
What is missing is a way to package and share application Redux Modules across our React applications.


Requirements
----

A Redux Module is a NPM package that export redux action creators and optionally one or more container components.

Code could be packaged in ES modules to allow better tree shaking by the build process in the consuming app.

Consider lazy loading and code splitting scenarios.

Be aware of relative routing.

Redux Module will expose:

* one ModuleReducer (composed of multiple SliceReducers)
* public Action creators that one can invoke
* public Action types that one can listen to
* public container components to be used

Auto-Wiring
---

If possible, it should not be necessary to explicitly register a Redux Module into the application but just import it and use it.

The Redux Module will register it self into the app.

By importing a Redux Module inside an App, this will cause it to automatically setup any necessary middleware. 

By importing a give container component this will cause the necessary reducer to be automatically added to the application reducers chain.

Note: Some Redux Module will be faceless, will only contain redux code which will register all their reducers right away.

Research POC
---

We will create a POC to research the best solution to accomplish this.
It needs to demonstrate packaging a simple redux and container that can be consumed by the ReactTemplate and inside Web.CRM.

Existing Libraries 
---

Libraries that solve similar problems, google search for : 'redux module' 

Redux-modules - npm
https://www.npmjs.com/package/redux-modules
https://www.npmjs.com/package/redux-module
https://github.com/fullstackreact/redux-modules
https://github.com/erikras/ducks-modular-redux
https://www.fullstackreact.com/articles/better-redux-module-management/
http://nicolasgallagher.com/redux-modules-and-code-splitting/