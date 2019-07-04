# React - Code Formatting

All our React projects use [Prettier](https://prettier.io/) for code formatting.

For information about [Prettier](https://prettier.io/) and how to configure it with your IDE see this page: Prettier for code formatting

This is our Standard prettier.config.js file to be place on the root of all our React projects. 

// prettier.config.js

```javascript
// https://prettier.io/docs/en/options.html
module.exports = {
  // Include parentheses around a sole arrow function parameter. (default: "avoid")
  arrowParens: 'always',
 
  // Print spaces between brackets in object literals. (default: true)
  bracketSpacing: true,
 
  // Put the > of a multi-line JSX element at the end of the last line instead of being alone on the next line
  // (does not apply to self closing elements). (default: false)
  jsxBracketSameLine: false,
 
  // Specify which parser to use. (default: "babylon")
  parser: 'babylon',
 
  // Specify the line length that the printer will wrap on. (default: 80)
  printWidth: 80,
 
  // Print semicolons at the ends of statements. (default: true)
  semi: true,
 
  // Use single quotes instead of double quotes. (default: false)
  singleQuote: true,
 
  // Specify the number of spaces per indentation-level. (default: 2)
  tabWidth: 2,
 
  // Print trailing commas wherever possible when multi-line. (default: "none")
  trailingComma: 'es5',
 
  // Indent lines with tabs instead of spaces. (default: false)
  useTabs: false,
 
  // By default, Prettier will wrap markdown text as-is since some services use a linebreak-sensitive renderer,
  // e.g. GitHub comment and BitBucket. In some cases you may want to rely on editor/viewer soft wrapping instead,
  // so this option allows you to opt out with "never". (default: "preserve")
  proseWrap: 'preserve',
};
```

Our standard is to use the default configuration values with the exception of the following:

### arrowParens
* arrowParens: 'always'

### printWidth
* printWidth: 80
* The default is 80 but 100 is also accepted as it the value used in the material-ui repo.

### singleQuote
* singleQuote: true

### trailingComma
* trailingComma: 'es5'