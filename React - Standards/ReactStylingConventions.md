# React - Styling Conventions


These are our Styling practices when writing React Components and Applications.

* Apps with Minimal Styling
* Rigid Components
* Theme First
  * Theme variables
  * Global theme override
  * Custom Themes
* Component's JSS Second
* Avoid Inline Styles
* Avoid { withTheme: true }
* Do not import a theme directly
* JSS Only
* No !important
* PX 
* Colors

## Apps with Minimal Styling
Most styling must occur in ds-ui-react components so that we avoid repeated styling blocks inside each Application.

## Rigid Components
The intent of the DS-UI Components is to encapsulate the Styling implementation of the "Design Language" set by our Design Team.
Our Components must be 'Rigid' because they will dictated how they look, this is in contrast with components from libraries like '@material-ui/core' that are 'Flexible' which can be configured to achieve possibly unlimited different looks.

Our components should only permit those variations specified in the "Design Language" set by the Design Team.

## Theme First
Before creating a ds-ui-react component that wraps just one '@material-ui/core' component, or before adding Component JSS styles, always research first all the available options that exist to customize '@material-ui/core' components through the Theme object.
One can change existing values or add new entires to the Theme object.


##### Theme variables
In order to promote consistency between components, and manage the user interface appearance as a whole, Material-UI provides a mechanism to apply global changes by adjusting the [theme configuration variables](https://material-ui.com/customization/themes#theme-configuration-variables).

##### Global theme override
When the configuration variables aren't powerful enough, you can take advantage of the overrides key of the theme to potentially change every single style injected by Material-UI into the DOM. Learn more about it in the [themes section](https://material-ui.com/customization/themes#customizing-all-instances-of-a-component-type) of the documentation.

```javascript
export const v1Theme = createMuiTheme({
  spacing: {
    iconSize: 24,
    ..
  },
 
  overrides: {
    MuiDialogTitle: {
      root: {
        fontSize: 20,
      },
    },
    MuiDialogContent: {
      root: {
        fontSize: 16,
        color: colors.neutral700,
        fontFamily: 'Roboto, sans-serif',
      },
    },
    ..
  },
});
```

In those cases where via the Theme object one can achieve all the customizations that are required, ds-ui-react will just re-export the original component.

There is no reason to wrap a component unless we need to make it more 'Rigid".

Inside a wrapper component one can hard-code the values of certain composed components' props and not expose those. Therefore our application developers have no access to them.

Let's say we have material-ui ComponentA, which has a prop named shouldShow. We don't want people using that prop, so we create a component that wraps ComponentA and sets shouldShow to always be true.


##### Custom Themes

Sometimes we need colors that are not in the primary palette. We need to reference them, so how do we do it?

Your first instinct might be to use theme.colors __but do not  do this__. The colors are __not the same__ between themes. A color that exists in one theme may not exist at all in another theme.

Another thing you may want to do is theme.palette.grey[###]. This is also __not a good solution__. Because something we want to be grey in one theme, we may want to be purple in another theme. 



To handle this, we have created a ds object on the theme. In this object, we added aliases for colors with typed names. This gives us the ability to make things completely different colors in different themes.

For an example lets take theme.ds.palette.warning. Warnings in our existing themes are variations of yellow, but not the same yellow. But say we wanted to add a theme where the warning banners would all be brown. If the banner app referenced the color directly, we would be unable to have this difference in colors. But, by referencing theme.ds.palette.warning, we can make the warning whatever color we want in any theme.



The existing files these are contained in are called ds-v1.theme.js and ds-v2.theme.js for you to reference and see if they have the color you need. If there is a color you need, but it doesn't exist, feel free to add it. Just give it a generic name about what is being colored. You do have to implement it for all themes, so work with design to make sure it has the right colors for all themes.

```javascript
const dsV1 = {
  palette: {
    neutralLight: {
      light: colors.grey50,
      main: colors.grey100,
      dark: colors.grey200,
    },
    neutral: {
      light: colors.grey300,
      main: colors.grey500,
      dark: colors.grey800,
    },
    neutralDark: {
      light: colors.grey400,
      main: colors.grey600,
      dark: colors.grey900,
    },  }};
 
 
//usage
const styles = (theme: Object) => {
  return {
    myClass: {
      backgroundColor: theme.ds.palette.neutral.main
    },
  };
};
```

## Component's JSS Second
If modifying the Theme object alone is not enough use the withStyles HOC. One then writes Component's JSS that generate scoped class names.

The Theme object is available as an argument of the 'styles' fat-arrow function which is useful for accessing theme variables.  

```javascript
import { withStyles } from '@material-ui/core';
type InternalProps = {
  classes: JssClasses,
};
..
const styles = (theme) => {
  return {
    root: {
      fontSize: `${theme.spacing.iconSize}px`,
    },
    icon: {
      width: theme.spacing.iconSize,
      height: theme.spacing.iconSize,
      fill: 'currentColor',
    },
    label: {},
  };
};
..
export const IconButton = withStyles(styles)(IconButtonComponent);
```

Not all styles values should be hardcoded inside each component.

Think about a future 'Night' theme (light text on dark backgrounds) and styles values that need to be consistent across several components.
These styles values are best defined as custom theme constants that we can add to the Theme object.
With a type DsUiTheme we can ensure that each theme we create will have a value specified for our custom theme constants that we added to the base MuiTheme schema. 

## Avoid Inline Styles
We must avoid using inline styles.

The alpha version of 'material-ui' uses inline styles but this practice will go away once we upgrade our component to use '@material-ui/core'.

There are still a few rare cases where inline style are still the correct solution. 
E.g. for dynamic styles that cannot be achieved by swapping scoped classes defined with Component's JSS. Like when a prop value specifies the value of a style.

## Avoid { withTheme: true }
The withStyles HOC has the option to inject the theme object into the props of the component. This should be avoid for the same reason that inline styles should be avoided.

If the theme object is in the component's props it means that it will be used in the render function to generate inline styles.

## Do not import a theme directly
The theme should only be used in the styles fat-arrow function to generate scoped named classes.

Old components that generate inline styles need to access the theme using the { withTheme: true } for now, but this is just a temporary solution until we upgrade/deprecate them.

## JSS Only
All styling must be done in JSS.
Existing SCSS will be removed/converted to JSS as we migrate to '@material-ui/core'.

## No !important
Do not use !important.

Currently we are using !important in SCSS to override alpha material-ui components that internally use inline styles.
Once we upgrade our component to use '@material-ui/core' there should not be a valid reason to use !important.

```javascript
//good
const styles = {
  myStyle: {
    height: '10px',
  },
};
  
//bad
const styles = {
  myStyle: {
    height: '10px !important',
  },
};
```

It may only be needed in rare occasions to override something that is already using it or is using an inline style.

## PX 
We use Pixels and not EM nor REM. 'material-ui/core components also use pixels.

## Colors
No hardcoded colors.

Use the ds palette for referencing colors from the theme object. See __StylingConventions-CustomThemes__ above.

Work with the Design Team to help identify the named colors constants for our components.

Do not use the colors from the theme.colors. These are there to support existing components that need to be updated. This will be removed from theme in the future.


