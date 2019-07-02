React Template
==============

![Image](images/ReactTemplate1.png "icon")

We built a react boilerplate to get your next React App up and running in no time.

You can start to check it out here: https://bitbucket.org/dealersocket/web.app.reacttemplate/overview

It is now almost feature complete. 
More documentation will be created.

The template now includes these main features:


### Application
* react-intl (localisation)
* react-router
* code splitting by route
* fetch and promise polyfilled
* redux (centralized application state management)
* redux-logic (better than redux-thunk or redux-saga)
* redux-form
* normalizr (normalises redux store data)
* reselect (memoize mapStateToProps)


### Develop
* code linting with eslint (config based on airbnb)
* FlowType validation
* unit tests and code coverage run locally with file watch
* storybook for interactively develop and test your React components
* hot module reloading for quick code-test iterations 
* time-travel debugging with Redux dev tools
* mock rest apis 

### Test
* unit-test with enzyme, jest, mocha, chai, sinon, expect
* coverage with istanbul
* e2e test to follow...


### Build
* latest WebPack 2.2
* tree shaking - eliminates dead code (~20% reduced distributed code size)
* extract-text-plugin, code minification, cache busting, the works

### Continues Integration via Bitbucket's Pipeline
* lints the code
* runs all test in BrowserStack against multiple environments & * different browsers 
* builds the app
* packages it
* deploys it to octopus