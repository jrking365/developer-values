<h1 align="center">
  <a title="Building financial tools for Canada's entrepreneurs" href="https://pillar.financial">
    <img alt="Pillar" width="200px" src="https://avatars.githubusercontent.com/u/86977965?s=200&v=4" />
    <br/>
  </a>
  Testing
</h1>

## The benefits of writing tests

Here are some key benefits of well-tested code:

1. Increases productivity.
2. Improves the design and readability of code.
3. Makes the codebase easier to maintain and refactor.
4. Provides a level of confidence when changing existing code.

## When to test

Code should be tested before and after modification.
Whichever testing framework you use, you should be writing tests.
Whenever you fix a bug, write a regression test. A bug fixed without a regression test is almost certainly going to break again in the future.

## Testing methodologies

There are many different ways to test code, choose what is appropriate for your use case:

### Test-Driven Development (TDD)

This method uses tests as a way to design code by creating the test first before any actual production code is written. This is usually a five-step process:

1. Write a test.
2. Run the test and show that it **fails**.
3. Write the smallest amount of production code possible that meets the needs of the test.
4. Run the test until it passes.
5. Refactor if needed.

### White box testing

This method refers to testing behaviour that is already known by the tester. In this approach, general tests are easier to write and edge cases harder to find as developers will usually tend to write tests they know will pass.

### Black box testing

This method is the total opposite of the previous one since the tester does not know the inner workings of the code to test. The tester will have to come up with a set of inputs and determine the expected outputs according to requirements alone before ultimately executing the tests.

## What to test

The general motto is **test what needs to be tested**.

This can mean many things depending on the context of your feature, examples include:

- Individual functions (unit testing)
- Interaction between your feature and external APIs (integration testing)

Avoid writing tests for third party dependencies, as they are most likely already tested. If not, make a PR on the relevant repo!

## How to test

For all tests below will we use [jest](https://jestjs.io/docs/en/api).

### Describe your tests

To have a good description for your tests you can use this approach.

```js
/*
 * The first describe level is the main describe and contain all other describes inside.
 * Inside the square brackets, we describe the path down to the tested file and add a small description
 * of what the tests are about.
 */
describe('[Packages | Resource | Todo | Model] interacting with the Todo model', () => {
  // The second level is used to describe a part on code inside the file that is being tested
  describe('given we need to add a new Todo', () => {
    // The third level is used to describe the state of the input for the test (missing params, valid payload, etc.)
    describe('when params does not contain a message', () => {
      // The last level is the where the actual test happens, notice the `it` block
      it('should throw an error', () => {
        delete addToDoArguments.message;
        return expect(() => addTodo(addToDoArguments.message)).toThrow('Missing message value.');
      });
    });
  });
});
```

More `describe` blocks can be added to improve test grouping.

### Testing synchronous code

```typescript
export function addTodo(message: string) {
  if (!message) throw Error('Missing message value.');
  return 'Todo added';
}
```

```js
const addTodoArguments = { message: 'My todo message.' }

describe('Interacting with to do', () => {
  describe('given we need to add a new Todo', () => {
    describe('when params does not contain a message', () => {
      it('should throw an error', () => {
        delete addTodoArguments.message;
        return expect(() => addTodo(addToDoArguments.message)).toThrow('Missing message value.');
      });
    });

    describe('when using a valid payload', () => {
      it('should return a valid result', () => {
        const result = addTodo(addToDoArguments.message);
        expect(result).toEqual('Todo added.');
      });
    });
  });
});
```

### Testing asynchronous code

```typescript
export function addToDo(message: string) {
  return new Promise((resolve, reject) => {
    if (!message) return reject('Missing message value.');
    resolve('Todo added');
  });
}
```

```js
const addToDoArguments = { message: 'My todo message.' }

describe('Interacting with Todo', () => {
  describe('given we need to add a new Todo', () => {
    describe('when params does not contain a message', () => {
      it('should throw an error', () => {
        delete addToDoArguments.message;
        return expect(addToDo(addToDoArguments.message))
          .rejects
          .toEqual('Missing message value.');
      });
    });

    describe('when using a valid payload', () => {
      it('should return a valid result', () => {
        return expect(addToDo(addToDoArguments.message))
          .resolves
          .toEqual('Todo added');
      });
    });
  });
});
```

### Testing using mocks

```typescript
import { query } from 'postgres';

export function updateToDo(id: string, message: string): Promise<Todo> {
  return query(`UPDATE FROM to_do SET message = \'${message}\' WHERE id = \'${id}\' RETURNING *`)
    .then((data) => data.rows[0]);
}
```

```js
import { query } from 'postgres';
import { mocked } from 'ts-jest/utils';

const todo = { id: '00000000-1111-1111-1111-000000000000', message: 'My todo message.' };

jest.mock('postgres', () => ({
  ...jest.requireActual('postgres'),
  query: jest.fn().mockResolvedValue({ { rows: [todo] } }),
}));

describe('Interacting with Todo', () => {
  describe('given we need to add a new Todo', () => {
    describe('when db throws an error', () => {
      it('should throw an error', () => {
        mocked(query).mockRejectedValueOnce(new Error('Error in the DB.'));
        return expect(addToDo(todo.message))
          .rejects
          .toThrow('Error in the DB.');
      });
    });

    describe('when using a valid payload', () => {
      it('should return a Todo', () => {
        return expect(addToDo(todo.message))
          .resolves
          .toEqual(todo);
      });
    });
  });
});
```

### Handling mutable input

```typescript
import { query } from 'postgres';

export function findToDo(id: string): Promise<Todo> {
  return query(`SELECT * FROM to_do WHERE id = \'${id}\'`)
    .then((data) => data.rows[0]);
}
```

```js
import { query } from 'postgres';

let findToDoArguments = { id: undefined };
let todo = { id: '00000000-1111-1111-1111-000000000000', message: 'My todo message.' };

jest.mock('postgres', () => ({
  ...jest.requireActual('postgres'),
  query: jest.fn().mockResolvedValue({ { rows: [todo] } }),
}));

// Runs a function once before all of the tests in this file run.
beforeAll(() => {
  // Populate this variable data before start tests
  findToDoArguments = { id: '00000000-1111-1111-1111-000000000000' };
});

// Runs a function before each of the tests in this file runs.
beforeEach(() => {
  // Populate this variable data before each test
  findToDoArguments = { id: '00000000-1111-1111-1111-000000000000' };
});

// Runs a function after each one of the tests in this file completes.
afterEach(() => {
  // Populate this variable data after each test
  todo = { id: '00000000-1111-1111-1111-000000000000', message: 'My todo message.' };
});

// Runs a function after all the tests in this file have completed.
afterAll(() => {
  // Clean some stuff like `database`.
});

describe('Interacting with Todo', () => {
  describe('given we need to find a Todo', () => {
    describe('when using a valid payload', () => {
      describe('and id doesn\'t match', () => {
        it('should return a null result', () => {
          return expect(addToDo(addToDoArguments.message))
            .resolves
            .toEqual(null);
        });
      });

      describe('and id match', () => {
        it('should return a valid result', () => {
          return expect(addToDo(findToDoArguments.id))
            .resolves
            .toEqual(todo);
        });
      });
    });
  });
});
```

### Minimizing type errors

Jest and TypeScript do not exactly play well together when it comes to mocking.

Let's start by defining our generic mock:

```typescript
// We set a generic return value for `query` calls
jest.mock('postgres', () => ({
  ...jest.requireActual('postgres'),
  query: jest.fn().mockResolvedValue(null)
}));
```

And try to override the mock's return value for a specific call:

```typescript
import { query } from 'postgres';

describe('Interacting with Todo', () => {
  describe('given we need to find a Todo', () => {
    describe('when using a valid payload', () => {
      describe('and id match', () => {
        // TypeScript does not know that `query` is an instance of `jest.Mock` and shows errors
        query.mockResolvedValueOnce({
          id: '00000000-1111-1111-1111-000000000000',
          message: 'My todo message.'
        });

        // More test logic...
      });
    });
  });
});
```

We can address that by using a small utility function exported from `ts-jest`:

```typescript
import { mocked } from 'ts-jest/utils';
import { query } from 'postgres';

describe('Interacting with Todo', () => {
  describe('given we need to find a Todo', () => {
    describe('when using a valid payload', () => {
      describe('and id match', () => {
        // TypeScript knows that `query` is an instance of `jest.Mock` and allows us to call specific methods
        mocked(query).mockResolvedValueOnce({
          id: '00000000-1111-1111-1111-000000000000',
          message: 'My todo message.'
        });

        // More test logic...
      });
    });
  });
});
```

The `mocked` function takes a plain JS object (anything, really) as argument and returns a correctly typed instance of `jest.Mock` which allows us to retain type information such as function arguments and return type after mocking.

## See also

[Jest API](https://jestjs.io/docs/en/api)
