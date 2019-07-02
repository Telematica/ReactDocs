ESLint Rules
============

Lint rules are awesome because they help developers find issues as they write the code, increase consistency, decrease code review noise, and can often provide automated fixes.

## Consider adding rules from Jest

https://github.com/jest-community/eslint-plugin-jest

We could add this plugin to our standard config and start by enabling the recommended rules, run it on our code, and see what happens.  I also like some of the non-recommended rules.


|Rule |	Description | Recommended | Fixable | Vote Yes | Vote No |Comments |
| ------------- |:-------------:| -----:| -----:| -----:| -----:| -----:|
| [no-jasmine-globals](https://github.com/jest-community/eslint-plugin-jest/blob/master/docs/rules/no-jasmine-globals.md) | Disallow Jasmine globals | | fixable | | | |
| [no-jest-import](https://github.com/jest-community/eslint-plugin-jest/blob/master/docs/rules/no-jest-import.md) | Disallow Jasmine globals | recommended | | | | |
