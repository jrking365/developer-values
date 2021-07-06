<h1 align="center">
  <a title="Building financial tools for Canada's entrepreneurs" href="https://pillar.financial">
    <img alt="Pillar" width="200px" src="https://avatars.githubusercontent.com/u/86977965?s=200&v=4" />
    <br/>
  </a>
  Code Readability Tricks
</h1>

## Avoid Nesting

Using multiple levels of nesting in a codebase usually makes the code harder to read and maintain.

**Techniques to reduce nesting:**

1. Return fast. If you can exit a function, do it fast. It usually reduces the nesting levels of the code and reduces the amount of local variables created.
2. Reverse conditions. Developers often write code by thinking about the success scenario first. Writing code with failure scenarios in mind often reduce the amount of conditions in a block of code.
3. Add functions to group similar logic. Multi-level nesting is often caused because the developer wants to avoid repeating the same block of logic. If you isolate this logic into an external function, you will avoid the repetition.


> Bad

```javascript
const someFunction = (condition, name, value, permissions) => {
    let returnValue = 'SUCCESS';

    if (condition) {
        if (name != null && name !== '') {
            if (value !== 0) {
                if (permissions.allow(name)) {
                    doSomething();
                } else {
                    returnValue = 'PERM_DENY';
                }
            } else {
                returnValue = 'BAD_VALUE';
            }
        } else {
            returnValue = 'BAD_NAME';
        }
    } else {
        returnValue = 'BAD_COND';
    }
    return returnValue;
};
```

> Good

```javascript
const someFunction = (condition, name, value, permissions) => {
    if (!condition) {
        return 'BAD_COND';
    }

    if (name === null || name === '') {
        return 'BAD_NAME';
    }

    if (value === 0) {
        return 'BAD_VALUE';
    }

    if (!permissions.allow(name)) {
        return 'PERM_DENY';
    }

    doSomething();
    return 'SUCCESS';
};
```

## Keep functions/methods intentions simple

While some functions goals touch a few different areas, trying to keep it simple and objective,
helps understand and navigate through the sequence flow.

Bad
```javascript
  /* Need example */
}
```

Good
```javascript
  /* Need example */
}
```
