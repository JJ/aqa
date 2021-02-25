# aqa
> Dependency-less Test Runner for Node.js

**aqa** is a light-weight and **a** **q**uick **a**lternative to [ava](https://github.com/avajs/ava), with a similar API.

### Installation
```
npm i aqa
```

### Usage

#### Simple single-file usage

_your.tests.js:_
```js
const test = require('aqa')

test('Test ourself', t => {    
    t.is(1 + 1, 2);
    t.not(1 + 1, 3);
    t.true(1 === 1);
    t.false(1 === 2);
})
```

`
node your.tests.js
`
#### Integration
To run multiple tests and integrate CI testing with your package, you need to change your package.json's `test` in the `scripts` section to `"aqa"`:
```json
"scripts": {
    "test": "aqa"
},
```
Then, to run all your tests: `npm run test`

All files anywhere in your package's directory (and subdirectories) that match `*.test.js` or `*.tests.js` will be ran.

#### Watch mode
To automatically run tests whenever you modify your files, aqa has a watch mode. If you desire this functionality, add a new script to your package.json:
```json
"scripts": {
    "test": "aqa",
    "test:watch": "aqa --watch"
},
```
To start the watch script, run `npm run test:watch`.

### Assertion
These assertion methods are currently supported:
#### `t.is(actual, expected)`
Asserts that `actual` is equal to `expected`.
#### `t.not(actual, notEpected)`
Asserts that `actual` is **not** equal to `notEpected`.
#### `t.true(value)`
Asserts that `value` is true.
#### `t.false(value)`
Asserts that `value` is false.
#### `t.throws(fn, opts?)`
Asserts that `fn` throws an exception.
```js
function uhOh() {
    throw new Error("Uh oh.");
}

t.throws(_ => {
    uhOh();
})
```
You can also check for specific types of exception. If the exception does not match it, the test will fail:
```js
t.throws(_ => {
    uhOh();
}, { instanceOf: TypeError })
```


### Work in progress:
- Async tests
- Configuration (globs, paths, etc.)
