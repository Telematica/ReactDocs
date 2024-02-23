# Frontend Architecture Setup

## 1) Initialize Project & Install Dependencies

### 1.1) Create Vite Project

Use React/TypeScript template:

```bash
yarn create vite my-vue-app --template react-ts
```

> ℹ️ Info: Above command will result in the following directory structure (as of Vite 5.0.8):

```bash
├─ public/
├─ src/
│  ├─ assets/
│  │  ├─ App.css
│  │  ├─ App.jsx
│  │  ├─ index.css
│  │  ├─ main.jsx
├─ .eslintrc.cjs
├─ .gitignore
├─ index.html
├─ package.json
├─ README.md
├─ vite.config.js
```

> 📝 Note: This step might create additional directories and files aside from the proposed project directories in TASK 1.3 (check Vite standard react template setup).

### 1.2) Verify initial dependencies and define default code-styling rules (prettier & eslint)

Add initial hard dependencies (as well as dev deps).

```bash
yarn add @rsuite/icons axios date-fns lodash.get react-hook-form rsuite sass

yarn add -D jsdoc @types/react prettier
```


Redux ecosystem additional dependencies

```bash
yarn add react-redux redux redux-actions redux-saga reselect

yarn add -D @types/react-dom @types/react-redux @types/redux-actions @types/reselect
```


```bash
.env
.env.sample
.eslintrc.{js,ts}
.prettierrc
package.json
.vscode/settings.json
```

> 📝 Note: Use default and suggested setups from every library documentation. We progressively will vote and add more rules and refined code-style settings via PR process.

### 1.3) Integrate Project-specific & DDD directory structure

The directory structure shown below represents a full implementation of the DDD approach for a JavaScript/TypeScript React/Redux generic application.

*❗Notice: Along to every directory, there's a quick summary explanation about its purpose.*

```bash
root
├─ bin/ (Simple command-based execution files)
├─ docs/ (Documentation files, style guides, hints and other resources)
│  ├─ business-logic/ (non-mandatory sample directory)
│  ├─ domains/ (non-mandatory sample directory)
│  ├─ screens/ (non-mandatory sample directory)
├─ public/ (Assets and misc static files)
│  ├─ images/ (non-mandatory sample directory)
├─ scripts/ (Script to do common/frequent task like test-runners, clean cache files, etc)
├─ src/
│  ├─ @types/ (JSDoc repo types directory: similar to .d.ts files, create {custom}.types.js files)
│  ├─ area/ (Main app stage, includes domain directories)
│  │  ├─ {domain-1}/ (Business Domain. Examples: engines, routes, pieces, etc)
│  │  │  ├─ mock/ (Mock data for testing)
│  │  │  │  ├─ unformatted-data.mock.js
│  │  │  │  ├─ data.mock.json
│  │  │  ├─ service/ (API-consumer code, AVOID BUSINESS LOGIC, only settings and HTTP/RESTFul related)
│  │  │  │  ├─ api-stuff.service.js
│  │  │  ├─ state/ (Redux-specific logic, mutations, usecases, models, selectors)
│  │  │  │  ├─ usecases/ (Redux actions, Redux Sagas/side-effects)
│  │  │  │  │  ├─ login.usecase.js
│  │  │  │  ├─ reducers/ (Redux models)
│  │  │  │  │  ├─ my-model.reducer.js
│  │  │  │  ├─ selectors/ (Data mutations from Redux Storage)
│  │  │  │  │  ├─ mutations.selectors.js
│  │  │  ├─ views/ (UI-related views, components)
│  │  │  │  ├─ components/ (React Functional components)
│  │  │  │  │  ├─ table.component.js 
│  │  │  │  ├─ containers/ (Redux High Order Components, Smart Components)
│  │  │  │  │  ├─ {redux-hoc}.container.js
│  │  │  │  │  ├─ table.container.js
│  ├─ shared/ (Shared/reusable code fragments)
│  │  ├─ components/ (Reusable React components)
│  │  │  ├─ button/ {Component type in singular to denote purpose: layout, menu, button, etc}
│  │  │  │  ├─ call-to-action.component.js
│  │  ├─ constants/ (Temporal and permanent hardcoded values, Application settings and App Values)
│  │  │  ├─ http-statuses.constants.js
│  │  ├─ hooks/ (React hooks)
│  │  │  ├─ logout.hook.js
│  │  ├─ utils/ (Generic App utilities)
│  │  │  ├─ math/
│  │  │  │  ├─ arithmetic.utils.js
│  │  │  ├─ redux/
│  │  │  │  ├─ create-redux-reducer.utils.js
├─ .gitignore
├─ package.json
├─ README.md
```

## 2) TASK: Setup Redux

### 2.1) Port redux pre-designed tools into `src/shared/redux` directory, based on legacy curated sample:

- https://github.com/Telematica/alphaville/tree/phase-1/DOS/office-ui/src/redux-utils

> 📝 Note: Current Redux utils implements v4.1.1, we need to upgrade to current (version x.x) Redux Toolkit.

## 3) TASK: Port reusable code into `src/shared/{type}` directories:

### Suggested reusable {types} based on common react/ui & programming patterns:

- Visual components into `src/shared/components`.

    >💡 Tip: Choose Component Type name in SINGULAR to denote purpose: layout, menu, button, etc*

    >💡 Tip: Pick UI related names to aggregate/group component/behavior files directories like:*

  - Buttons: `src/shared/components/button`
    - Sample file name using suffix conventions: `src/shared/utils/button/call-to-action.component.js`

  - Modals: `src/shared/components/modal`
    - Sample file name using suffix conventions: `src/shared/utils/button/form-modal.component.js`

  - Snackbars: `src/shared/components/snackbar`
    - Sample file name using suffix conventions: `src/shared/utils/button/form-modal.component.js`

  - Menus: `src/shared/components/menu`

  - (add as many as required)

- Temporal & Permanent Hardcoded app values `src/shared/constants`

    >💡 Tip: Avoid keeping hardcoded values at component level, always choose creating a constant file to keep dummy components unaware to any possible fixed state. All possible permanent or hardcoded values are sensitive to be eventually dynamic using a backend resource, third party source or calculated impure functions (non-deterministic).*

  - Suggested Item -> UI deeplinks and permanent routes: `src/shared/constants/routes`
    - Sample file name using suffix conventions: `src/shared/constants/routes.constants.js`

  - Suggested Item -> Domain-specific entity statuses: `src/shared/constants/{entity}-status`
    - Sample file name using suffix conventions: `src/shared/constants/my-domain-statuses.constants.js`

- React Hooks `src/shared/hooks`

    >💡 Tip: You might OPTIONALLY separate hook concerns using a nested directory*

  - Suggested Item -> Authentication hooks:
    - Sample file name using suffix conventions:
      - `src/shared/hooks/logout.hooks.js` or `src/shared/hooks/auth/logout.hooks.js`

- Generic & Lang-specific reusable utils: `src/shared/utils`

    >💡 Tip: Pick meaninful and domain-like name to aggregate/group util files like:*

- Generic math calculations, and library-specific implementations like BigInt or decimal.js: `src/shared/utils/math`
  - `src/shared/utils/math/arithmetic.utils.js`

- Date manipulation utils: `src/shared/utils/date`
  - `src/shared/utils/date/date-diff.utils.js`

- String manipulation utils: `src/shared/utils/string`
  - `src/shared/utils/string/capitalize.utils.js`

## 4) TASK: Create domains and start working on modules: `src/area/{domain}`

### 4.1) Suggested domain & technical concerns to be set at domain level directory:

- Mock data `src/area/{domain}/mock`:

  >💡 Tip: Put here any service/endpoint mock response in JS compatible formats {.js,.json}. Use suffix conventions.*

  - Plain Javascript files: `src/area/{domain}/mock/data.mock.js`

  - JSON files: `src/area/{domain}/mock/endpoint-response.mock.json`

    - HTML test documents: `src/area/{domain}/mock/template.mock.html`

    - (any other mock/testing data)

- Service `src/area/{domain}/service`:

  - ℹ️ Info: Service directory SHOULD contain any browser-side service consumer code for any protocol (HTTP/HTTP2/HTTPS,RPC,GRPC) or any preferred backend API implementation (GraphQL, RESTFul, SOAP, etc)*

    -❗Notice: You MUST avoid having any business logic code in service files. Only library implementations and client-server logic SHOULD be handle in .service.{js,ts} files (AXIOS, plain XMLHTTPRequest Promises, jQuery.ajax, etc)*

  - RESTFul: `src/area/{domain}/service/api.service.js`

  - SOAP: `src/area/{domain}/service/soap-endpoints.service.js`

  - GQL queries & other settings: `src/area/{domain}/service/gql-queries.service.js`

    *💡 Tip: You might OPTIONALLY separate services using a nested directory: `src/area/{domain}/service/v1/api.service.js`*

- State `src/area/{domain}/state`:

  - ℹ️ Info: A Usecase acts on one slice of the redux state and Selectors expose data from one slice of the redux state. A Usecase can also listen for ActionTypes defined by an other Usecase that acts on a different slice or call an ActionCreator function that acts on a different slice: `src/area/{domain}/state/usecases`*

  - ℹ️ Info: Root REDUCER `src/area/{domain}/state/reducers`*

  - ℹ️ Info: Top Level Slice REDUCER `src/area/{domain}/state/reducers`*

  - ℹ️ Info: Leaf Reducer REDUCER `src/area/{domain}/state/reducers`*

  - ℹ️ Info: A Selector can compose other Selectors that expose data from a different slice. `src/area/{domain}/state/selectors`*

  - `src/area/{domain}/state/reducers/top-level.reducer.js`
  - `src/area/{domain}/state/selectors/mutations.selectors.js`

- Views `src/area/{domain}/views`:

  - ℹ️ Info: `View Components` SHOULD contain only rendering logic and internal operations.*

  - ℹ️ Info: A `DUMMY Component` MUST only handle internal state, and MUST NOT alter/mutate storage state directly, or any other external state. In other words, a `DUMMY Component` mostly consists of markup code and rendering logic that performs a very specific task.*

  - ℹ️ Info: A Redux High Order Component or Container, also called `SMART Component`, is Wrapper Functional Component that injects reactive dependencies: props and Redux actions.*

    *❗Notice: Business logic like calculations and intensive data mutations that alters global storage MUST NOT be performed inside views.Use selectors, usecase and other specific files to isolate that kind of operations.*

  - Sample Dummy Component: `src/area/{domain}/views/components/table.component.js`

  - Sample Redux HOC / Smart Component: `src/area/{domain}/views/containers/hoc.container.js`

    *💡 Tip: You might OPTIONALLY separate view/layout components using a nested directory: `src/area/{domain}/views/components/layouts/dashboard.component.js`*


# AGENDA:

## ACTION items:

### 1) Redux Setup

### 2) Domain Setup

### 3) Discuss Commits
  
  Commit tracking:
  
  - {emoji task type} - {ticket platform / EPIC}-{serial number} - {task description}
    * 🐛 JIRA-123 - Bug resolved
    * 🧹 JIRA-456 - Chore task
    * 🛠️ JIRA-789 - Hotfix task
    * 🆕 JIRA-101 - Feature task
  
  - file name conventions
    snake-case :

  - PRE-COMMIT hook with husky.js