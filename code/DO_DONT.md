<h1 align="center">
  <a title="Building financial tools for Canada's entrepreneurs" href="https://pillar.financial">
    <img alt="Pillar" width="200px" src="https://avatars.githubusercontent.com/u/86977965?s=200&v=4" />
    <br/>
  </a>
  Do's and Don'ts
</h1>

## DO Comment your code

Single line comment to add context to a business logic operation or to explain a complex function. Code blocks for larger paragraphs.

## Do follow the guidelines

## Do setup your gitignore and dockerignore files

Repositories and Containers should be crap-free

## Do include screen captures in your pull requests

(Front-end) This is to ensure that the code works on all devices

## Do NOT use improper or unclear name for services

## Do NOT write functions which's body is too long

Ideally, a function body should not exceed 15 lines, for readability and 600 characters, for optimization (V8 preferences)
Please refer to [Code Readability Tricks](./CODE_READABILITY_TRICKS.md) for examples.

## Do NOT leave dead code in the project

Less code to read means easier maintainability.

## Do NOT use JSDoc in your code

This information is redundant with Typescript definitions and are too verbose for most cases since your code should already be self explanatory.

## Do NOT commit secrets, keys or passwords to the repository.

If you believe that any has been compromised, get LOUD, notify the team.
