<h1 align="center">
  <a title="Building financial tools for Canada's entrepreneurs" href="https://pillar.financial">
    <img alt="Pillar" width="200px" src="https://avatars.githubusercontent.com/u/86977965?s=200&v=4" />
    <br/>
  </a>
  Object properties ordering
</h1>

## Regular object

A regular object is all objects created by you, unique to your project.

In order to maintain coherence between all regular objects, we need to create rules.

We will order properties alphabetically, except if we have an ID, that would come first.

> Bad

```js
const myObject = {
  type: 'article',
  isValid: true,
  checked: false,
  title: 'My title',
  id: 'fdD87Eefee',
  description: 'Short description',
  addressStreetNumber: '12',
  addressStreetName: 'rue de Courcelle',
};
```

> Good

```js
const myObject = {
  id: 'fdD87Eefee',
  address: {
    streetNumber: '12',
    streetName: 'rue de Courcelle',
  },
  checked: false,
  description: 'Short description',
  isValid: true,
  title: 'My title',
  type: 'article',
};
```

## Schema

A schema is a standardized data structure created with the intention of using it everywhere we refer to that model.

A good example of schema definition resides in `Pillar-api`.

[Schema example](https://github.com/getPillar/Pillar-api/blob/develop/packages/resource/address/schema.ts)

For this type of object it's preferable to use a logical approach, you need to determine this by yourself.

Don't hesitate to discuss with a colleague to have a different point of view or if you have questions.

## Functions

When you have a lot of parameters, some problems might occur:

- We need to remember the order of each parameters
- We need to be careful about parameters order (required parameters first)
- If we want add or remove parameters, we need to change parameters order for each functions.
- You can't add a default value if the parameter is not at the end

To avoid this recurrent problem, we often use destructuring properties.

## How does it work?

Take this function as an example:

```js
const myFunction = (param1, param2, param3 = 10, param4 = false, param5 = '') => {
  console.log(`Param1: ${param1}`);
  console.log(`Param2: ${param2}`);
  console.log(`Param3: ${param3}`);
  console.log(`Param4: ${param4}`);
  console.log(`Param5: ${param5}`);
};

myFunction(value1, value2, value3, false, value5);
```

Now, if we use destructuring:

```js
const myFunction = ({param1, param2, param3 = 10, param4 = false, param5 = ''}) => {
  console.log(`Param1: ${param1}`);
  console.log(`Param2: ${param2}`);
  console.log(`Param3: ${param3}`);
  console.log(`Param4: ${param4}`);
  console.log(`Param5: ${param5}`);
};

myFunction({param1: 'value1', param2: 'value2', param5: 'value5'});
myFunction({param2: 'value2', param5: 'value5', param1: 'value1'});
```

Recommended for even better readability:

```js
const myFunction = ({param1, param2, param3 = 10, param4 = false, param5 = ''}) => {
  console.log(`Param1: ${param1}`);
  console.log(`Param2: ${param2}`);
  console.log(`Param3: ${param3}`);
  console.log(`Param4: ${param4}`);
  console.log(`Param5: ${param5}`);
};

const param1 = 'value1';
const param2 = 'value2';
const param5 = 'value5';

myFunction({param1, param2, param5});
myFunction({param1, param5, param2});
```

All parameters can be put in any orders, but try keeping some logic (ex: required or most use parameters first).

## Destructuring

To learn and understand all about destructuring, follow this link [destructuring in JS](https://hacks.mozilla.org/2015/05/es6-in-depth-destructuring)
