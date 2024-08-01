# Architecture Proposal



## Domains

Domain-driven directory structure

- Business expert(s) should defined domains
    * organization/namespace/component
- https://dzone.com/articles/ddd-and-microservices


* Domain: The central focus of DDD is the domain, which represents the core business problem that the software addresses.

* Entities: These are objects with distinct identities and lifecycles within the domain. They have attributes and behaviors.

* Value objects: Value objects are objects without distinct identities. They represent attributes that are conceptually distinct within the domain.

* Aggregates: Aggregates are groups of related entities and value objects treated as a single unit. They are often responsible for enforcing consistency and maintaining data integrity. In other words, you are creating meaningful relations between two or more value objects.

* Repositories: Repositories provide an abstraction for data access, allowing the application to interact with aggregates.

* Services: Services represent actions or behaviors that don’t naturally belong to a single entity or value object.

* Bounded contexts: A bounded context defines a specific, self-contained part of the domain where the domain model and its concepts have clear and consistent meanings.


```
**root**
src/
    area/
        engines/
        purchase-orders/
        quotes/
        routers/
        users/
    shared/
        components/
        helpers/
        hooks/
        layouts/
        reducers/
        services/
/scripts
/@types
```

## MVC/MVVM Architectural Pattern directory structure
- Reference: https://vueschool.io/articles/vuejs-tutorials/how-to-structure-a-large-scale-vue-js-application/


Pros & Cons

- DDD
    * Business experts and developers can work along.
    * The business flows more easily.
    * Flexibility
    * Using DDD leads to cleaner, more reliable code.
    * The ubiquitous language – where everyone involved in the project uses the same language

- MVC
    * Highly technically organize, abstracts and separates concerns.
    * It is hard to understand the MVC architecture.
    * Must have strict rules on methods.
    

```
**root**
src/
    assets/
    components/
        AppButton.vue
        AppPopup.vue
    docs/
    helpers/
    plugins/
    router/
    store/
    views/
    App.vue
    main.js
/scripts
/@types
```

## Technical Concerns

### Why separate concerns is key to success?
    1. Divide and conquer
    2. Single Resposibility (from SOLID)
    3. Granularity (allows high decoupling)
    4. Because is cool!

- Team should design at least 1 sample file to define a template for every type of technical topic/concern.
    * Having templates up-to-date should save time when creating a new file of any kind.
    * Having many "variant" types for every file is a nice-to-have.

| File Suffix | Tech Concern / Responsibility | JS Library-specific | React-specific | Redux-specific |
| --- | --- | --- | --- | --- |
|*.component.{js,jsx,ts,tsx}|React Dummy Component||✅||
|*.container.{js,jsx,ts,tsx}|Redux Smart HOC (Dependency Injection)|||✅|
|*.hooks.{js,jsx,ts,tsx}|Test file (Jest, React Testing Library, Enzime, etc)||✅||
|*.reducer.{js,jsx,ts,tsx}| Redux Reducer (model-like structure)|||✅|
|*.selectors.{js,jsx,ts,tsx}| Data Mutation implementation, like reselect, etc|||✅|
|*.service.{js,jsx,ts,tsx}| AJAX/Axios/GraphQL consumption|✅|||
|*.spec.{js,jsx,ts,tsx}|Test file (Jest, React Testing Library, Enzime, etc)|✅|||
|*.test.{js,jsx,ts,tsx}|Test file (Jest, React Testing Library, Enzime, etc)|✅|||
|*.utils.{js,jsx,ts,tsx}|Test file (Jest, React Testing Library, Enzime, etc)|✅|||


### Other type of files for Mock data, html templates and styles.

| File Suffix | Tech Concern / Responsibility |
| --- | --- |
|*.mock.{js, json}| Sample data to mock and endpoint, a third party service, etc. |
|*.template.{html}| Template file for emails, static compilation, etc. |
|*.global.{css,less,sass,scss,stylus}| Data Mutation implementation, like reselect, etc. |


```
src/
    area/
        engines/
            usecases/
                sample.usecase.ts
            state/
                sample.selectors.ts
                sample.selectors.ts
            views/
                components/
                    sample1.component.tsx
                    sample2.component.tsx
                containers/
                    sample1.container.tsx
                    sample2.container.tsx
        purchase-orders/
        quotes/
        routers/
        users/
    shared/
/scripts
/@types
```


## Migration Plan


1) Organize files into domains
2) Place reusable code (utils/components) into shared/
3) Set up dependencies: React, Redux, Axios, Material UI, decimal.js...
4) Create organisms:
    * components
    * mutations (selectors, context api)
    * layouts
    * side effects (sagas, hooks)
5) Create specs / Unit Test for existing components
6) Integrate and Deploy

- Action Items
    * Vite

* `api => {domain}/services - shared/services`
* `components => {domain}/views - shared/components`
* `containers => {domain}/views - shared/layouts`
* `pages => {domain}/views`
* `styles => {domain}/views - shared/styles`
* `utils => shared/utils`


Usecase
    - async
    - side effect
    - saga
        * ocherstation
        * chroagraph

Redux
    - Mutations


* A lot of boiler play

* Lots of place to go to figure out what is going
    - Testability
    

Context API
    load_workorders
    {
        a: 1,
        b: "aaas",
        c: asddsd
    },
    {
        a: 1,
        b: "aaas"
    }


- https://learn.microsoft.com/en-us/archive/msdn-magazine/2009/february/best-practice-an-introduction-to-domain-driven-design

---

Agenda 
- Spike on Frontend And Suggested Improvements from a Code Architecture Perspective
    * Dive into our current frontend codebase
    * Search for usable patterns aiming for a porting strategy
- Struct a migration plan
    * Adopt DDD Architecture (in a potential new repo):
        - Pros & Cons DDD vs MVC and other architectural patterns
        - Define business-related domain/directory structure (i. e. auth, purchases orders, engines, parts, routers, etc)
        - Separate technical concerns in a granular way within domains: (services, state, views, mock, usecases, etc.)
    * Establish crucial discussion topics like:
        - Embracing a Type Safe System (TypeScript vs JSDoc)
        - UI technologies to implement and wrap in the project (Material UI, Storybook for component documentation, Axios, Redux, React APIs, etc)
        - Frontend testing tools (Jest, React Testing Library) and Whether to Unit Test only at component level or (both at end-to-end level as well).
        - CI/CD
- Define and document Best Practices
    * From Linters to Automated actions (Code Style enforcing and corrections using a Prettify tool, template plops, etc)
- Reference Docs: https://github.com/Telematica/ReactDocs

---


Type Safe discussion:

    - Allow optional typing using //ts-disabled
    - any (tech debt)
    - JSDoc (tsc optional to use TS features like Generics, Union Types and Typing tools)
