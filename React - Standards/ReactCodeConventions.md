# React - Code Conventions

These are our code practices for writing React Components and Applications.

* No lodash & underscore
* No Object.assign
* Flow & propTypes
* Constant key
* Enum
* Variables, arguments, properties 
* Type and Interfaces (TS)
* Reason
* Extends
* Constructor
* Component
* No Components import form libraries' root indexes
* Default export
* Export
* InternalProps
* Saga generator function


## No lodash & underscore
We use ES+ language features and it is __extremely__ rare that we need to use a lodash or an underscore function.

## No Object.assign
To create shallow clones with updated properties we don't use Object.assign but we use the spread operator.

```javascript
const newState = {
  ...state,
  propName: newValue,
};
```

## Flow & propTypes
We don't write propTypes and instead we use [Flow Types](https://flow.org/en/docs/) which have a TypeScript similar syntax and we use [babel-plugin-flow-react-proptypes](https://github.com/brigand/babel-plugin-flow-react-proptypes) to generate propTypes.
This gives us static type code checking and, in dev mode, runtime props validation.

## Constant key
Use SNAKE_UPPER_CASE for constant keys.

```javascript
const CLEAR_STUDENTS: string = `CLEAR_STUDENTS${postfix}`;
```

## Enum
Use PascalCase for Enum and enum Keys. Use lowercase strings for enum values.

```javascript
export const AvatarSizes = {
  Small: 'small',
  Medium: 'medium',
  Large: 'large',
};
```

## Variables, arguments, properties 
Use camelCase for variables, arguments, properties.


## Type and Interfaces (TS)
Use PascalCase for __Flow Types__ and __TypeScript Types and Interfaces__.

Types and Interfaces must be suffixed with: __Type__ or __Props__

__Do not use the 'I' prefix__ because it has no meaning to Flow code and to functional programming. It is an OOP convention that does not apply to FP.


```javascript
export type ButtonProps = {
  children?: Node,
  'data-e2e': string,
  disabled?: boolean,
  ...
};
 
export interface VehicleType {
  make: string;
  model: string;
  ...
}
```

### Reason
In functional programming we don't create classes that implement an interface.
Even when using the interface construct in TypeScript the intent is to declare a "Type" to be used in the functional code.

Flow types imports are explicit but unfortunately TypeScript are not.

### Flow

```javascript
import { type Vehicle } from '...';
```

### TypeScript

```javascript
import { Vehicle } from '...';
```

To ease readability we use the following naming convention to differentiate Types from Components.

Our shared code must use one of these these suffixes: Type, or Props for all types and interfaces that are exported. Because the consumer may be a Flow or TypeScript project.

```javascript
// TypeScript
import { VehicleT } from '...';
import { VehicleType } from '...';
import { VehicleProps } from '...';
 
// Flow
import { type VehicleT } from '...';
import { type VehicleType } from '...';
import { type VehicleProps } from '...';
```


## Extends
In React we always use composition and we never extend other components.
The only case where we use extends is when we declare a class component.

```javascript
export class MyPage extends React.Component<Props, State> { .. }
```

## Constructor
Constructors should be avoided. Remember to collect all arguments and pass them to the super.

```javascript
constructor(...args: any) {
  super(...args);
  ..
}
```

## Component
Use PascalCase for class Component and functional Component, also when declared with an arrow-function.

```javascript
class AvatarComponent extends React.Component { .. }
 
function AvatarComponent(props: Props) { .. }
 
const AvatarComponent = (props: Props) => { .. }
```

## No Components import form libraries' root indexes
Always import the desired library components via their individual root folders when the given library expose them that way.

Wrong:

```javascript
import { CloseIcon } from 'mdi-react';
```
Right:

```javascript
import CloseIcon from 'mdi-react/CloseIcon';
```

This is most important for image libraries like 'mdi-react' but also apply to any other component library that also exposes their components via individual root folders.
When you import components from the library's root index you are in fact importing all the components in the library and then via object destructuring only use a few.
This can make a dev build very slow and puts a lot of pressure on Webpack to find all the code that needs to be tree-shaken in a production build.

## Default export
Do not use 'default' export.

Rule: __import/no-default-export__

~~The only exception was for a Container that need to be lazy loaded. Just because our current lazyRenderer did not have an option to specify the named export to be rendered.~~
(We have updated the lazyRender in '@dealersocket/react-common' to take one additional optional string argument which is the named exported Component to be rendered.)


## Export
Only export public items. 
Internal items that are needed for uint testing must be exported via a single exported '*TestPort' object.

```javascript
const LOAD_STUDENTS: string = `LOAD_STUDENTS${postfix}`;
export const loadStudentsAction = createAction(LOAD_STUDENTS);
const LOAD_STUDENTS_SUCCESS: string = `LOAD_STUDENTS_SUCCESS${postfix}`;
const LOAD_STUDENTS_ERROR: string = `LOAD_STUDENTS_ERROR${postfix}`;
 
export const loadStudentsTestPort = {
  LOAD_STUDENTS,
  LOAD_STUDENTS_ERROR,
  LOAD_STUDENTS_SUCCESS,
  loadStudentsWatch,
  loadStudentsWorker,
  loadStudents,
  reduceHandlers,
};
```


## InternalProps
Define internal props added with HOC (componentQueries, DragSource, DragTarget, withStyles, ...) in a separate type InternalProps.
This keeps the ExternalProps clean and easy to read and document.

```javascript
type ExternalProps = {
  ..
};
type InternalProps = {
  classes: JssClasses,
  queries: Object,
  theme: Object,
};
// Can't export types via 'testPort'!
export type AvatarCompProps = ExternalProps & InternalProps;
  
const AvatarComp(props: AvatarCompProps) { .. }
 
export Avatar = hoc(AvatarComp);
  
export const avatarTestPort = {
  AvatarComp,
  ..
};
```

## Saga generator function
Use camelCase suffixed with either 'Watch' or 'Worker' for Saga generator functions

```javascript
function* loadStudentsWatch(): Generator<*, *, *> {..}
 
function* loadStudentsWorker(): Generator<*, *, *> {..}
```
