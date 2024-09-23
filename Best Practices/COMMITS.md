# Best Practices


## Conventional Commits 1.0.0

### Summary

The Conventional Commits specification is a lightweight convention on top of commit messages. It provides an easy set of rules for creating an explicit commit history; which makes it easier to write automated tools on top of. This convention dovetails with [SemVer](http://semver.org/), by describing the features, fixes, and breaking changes made in commit messages.

The commit message should be structured as follows:


```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]

```
The commit contains the following structural elements, to communicate intent to the consumers of your library:

1. fix: a commit of the type fix patches a bug in your codebase (this correlates with [PATCH](http://semver.org/#summary) in Semantic Versioning).
2. feat: a commit of the type feat introduces a new feature to the codebase (this correlates with [MINOR](http://semver.org/#summary) in Semantic Versioning).
3. BREAKING CHANGE: a commit that has a footer BREAKING CHANGE:, or appends a ! after the type/scope, introduces a breaking API change (correlating with [MAJOR](http://semver.org/#summary) in Semantic Versioning). A BREAKING CHANGE can be part of commits of any type.
4. types other than fix: and feat: are allowed, for example [@commitlint/config-conventional](https://www.conventionalcommits.org/en/v1.0.0/#specification:~:text=%40commitlint/config%2Dconventional) (based on the Angular convention) recommends build:, chore:, ci:, docs:, style:, refactor:, perf:, test:, and others.
5. footers other than BREAKING CHANGE: <description> may be provided and follow a convention similar to [git trailer format](https://git-scm.com/docs/git-interpret-trailers).

Additional types are not mandated by the Conventional Commits specification, and have no implicit effect in Semantic Versioning (unless they include a BREAKING CHANGE). A scope may be provided to a commit’s type, to provide additional contextual information and is contained within parenthesis, e.g., `feat(parser): add ability to parse arrays`.

### Examples

#### Commit message with description and breaking change footer

```
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
````

### Source

- https://www.conventionalcommits.org/en/v1.0.0/#specification
- https://github.com/commitizen-tools/commitizen

- https://github.com/backstage/backstage