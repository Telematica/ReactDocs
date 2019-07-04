# React - Project Structure


* Folder
*  No .JSX Extension
     * web.crm difference


## Folder
Use kebab-case for all folder names.

Only exception are the new Components in the ds-ui-react component library that will have a PascalCase folder directly under the src folder.
This is necessary in order to import all new components this way:

```javascript
import { Avatar } from '@dealersocket/ds-ui-react/Avatar';
```
Instead of using the old root index:

```javascript
import { Avatar } from '@dealersocket/ds-ui-react';
```

The new way avoids including all components into the project and then rely on Webpack 4 to tree-shake the ones that we are not using.
See this course for more info about building [Creating Reusable React Components](https://app.pluralsight.com/library/courses/react-creating-reusable-components).


## File

Use kebab-case to separate name. Separate type and extension with periods.

*some-name.type.extension*

type
* types
* component
* container
* reducer
* selectors
* usecase
* mock-api
* helper(s)
* util(s)
* ...

extension

* js
* json
* css
* scss
* jpg
* ico
* ...


## No .JSX Extension
There is no value in using the 'jsx' since all editors that we use understand jsx syntax inside a 'js' file.

It just adds configurations to your project (linter, test, build).



We stoped using the 'jsx' extension in favor to just 'js' and rename all the one inside our current projects.

Can use this to bash shell command to rename your files:

```bash
find . -name "*.jsx" -exec rename 's/.jsx$/.js/' '{}' \;
```
