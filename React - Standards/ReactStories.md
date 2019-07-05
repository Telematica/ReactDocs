# React - Stories

These standards are all about things specific to creating stories in storybook.
A story is how we show off our components. We want components to be easily find able and to show off the different options that a component has.

* Notes
* Stories

## Notes
Notes should contain all external props. They should be formatted like this.


* All props start with the @ symbol. The prop names should always be camelCase.
* Optional props are denoted with ? after the name.
  * If a prop is optional, include the default value. Even if it is undefined.
* If sub types are used, describe them too.

```javascript
const notes = `
This is a description of this component. It is short, but contains all the information someone might want to know about it.
 
@text: string
The text to display within this component.
 
@isDisabled?: boolean
If true, the background and border are grey and not clickable.
default: false
 
@onFocus?: (event: object) => void
Callback function that is fired when the input control is focused.
event: Click event targeting the input control.
`;
```

## Stories
Each story should have one storiesOf, that contains the name of your component. If you have a simple demo, name it Basic. If you have a specific Demo, name it something descriptive about the more specific thing.

* All of your props should be somewhere in the stories.
* If they are simple, such as text or booleans, they should be done as knobs.
* If they are not simple enough for a knob, create chained story that adds this prop to it manually.
* Chained stories should also include all knobs.

```javascript
storiesOf('My Component', module)
  .add(
    'Basic',
    withNotes(notes)(() => (
      <MyComponent
        isDisabled={boolean('isDisabled', false)}
      />
    ))
  .add(
    'With Some Option',
    withNotes(notes)(() => (
      <MyComponent
        someOption={someValue}
        isDisabled={boolean('isDisabled', false)}
      />
    ))
);
```