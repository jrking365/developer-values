<h1 align="center">
  <a title="Building financial tools for Canada's entrepreneurs" href="https://pillar.financial">
    <img alt="Pillar" width="200px" src="https://avatars.githubusercontent.com/u/86977965?s=200&v=4" />
    <br/>
  </a>
  Naming standards
</h1>

## Definitions

| Casing | Description |
| --- | --- |
| **Camel casing** :camel: | lowerCaseWordWithCapitalizedSubsequentWords |
| **Kebab casing** :dango: | lower-case-words-linked-with-dashes |
| **Snake casing** :snake: | lower_case_word_linked_with_underscores |


## Rules

| Name | Rule | Example |
| --- | --- | --- |
| **Repositories** | Repositories should be named with this pattern: `<module name id>-<type>`<br />Where the module name is a **kebab-cased** short domain title<br/>and where the type is taken from a list of project types:<br />`[api, function, project, service, app]` | Ex: `photoid-api` |
| **Pull Request Titles** | Pull request titles should include identifiable details: `<type>/<ticket>: <short-description>`<br />where the type can be one of:<br />`[feat, hotfix, test, improvement, maintenance]`<br />The ticket name or type is required and must end with a short description that should match the WHAT and not the HOW. The verb tense must be simple past.  | Ex: `feat: implemented new feature in some resource`<br/>Ex: `AC-1234: fixed something in core` |
| **Branches** | Branch names should include identifiable details: `<type>/<ticket>/<short-description>`<br />where the type can be one of:<br />`[feat, hotfix, test, improvement, maintenance]`<br />The ticket name is optional, representing the associated tracking ticket and must end with a meaningful short **kebab-cased** description. The verb tense must be simple past. | Ex: `feat/JIRA-1234/implement-x`<br/>Ex: `maintenance/fixed-something-in-core` |
| **Folders** | Folder names should be **kebab-cased**<br />They should not contain special characters or typically reserved words | Ex: `data-loaders` |
| **Files** | File names should be **kebab-cased**<br />They should not contain special characters or typically reserved words | Ex: `user-utils` |
| **Modules / Classes** | Class names should be **CapitalizedCamelCased**<br />They should not contain special characters or typically reserved words | Ex: `InvestmentAccounts` |
| **Methods** | Methods and function names should be **camelCased**<br />They should not shadow existing system functions or contain reserved words | Ex: `doSomeAction` |
| **Variables / Properties** | Variables and property names should be **camelCased**<br />They should not contain type detail or prefixing nor reserved words<br /><br />When no typing is provided, the variable/property name should provide proper context of what is actually storing. For example, a variable named `params` can be ambiguous (ie: is is application configuration, HTTP request or service parameters?). For the previous example, better names should be `httpRequest`, `appConfig` and `serviceConfig`.  | Ex: `userStatus` |
| **Environments**| Environment variables should be in capital letters with **UPPER_SNAKE_CASE** | Ex: `SOME_ENVIRONMENT_VARIABLE`|

## Stylistics

### Plurals

As a rule of thumb, function names, properties and variables should make sense as if they are part of a prose. Purpose and nature should be derivable from the name.

Ex:

```javascript

const animals = ['cat', 'dog'];
const myPet = animals.find(animal => animal === 'dog');

```

This reads rather well as animals, being plural, indicates a list of many "animal".
In the `find` operation, we iterate over singular "animal" items.

Side note: explicit iterable labels are preferred over generic variable names, like `i` - in most cases.

### Structure invariants

Project code should be encapsulated in an `src` folder and tests in a `test` folder, unless it conflicts with an established pattern or convention of the repo's framework.

Industry standards should be followed above all for structure and naming of folders and components.

### Extensions

Code files should bear the `.js`, `.ts` or the react variants `.jsx` and `.tsx` extensions.

Test files, in the unit-tests category should bear the same name and folder path as the file it's covering, mimicked inside the `test/unit` folder of the project.

All test files should have a test-type extension, like `.test.js`, `.test.ts`, etc.
