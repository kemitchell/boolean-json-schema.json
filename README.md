```javascript
var schema = require('boolean-json-schema')
```

The package exports a [JSON Schema](http://json-schema.org):

```javascript
var ajv = new (require('ajv'))()
var assert = require('assert')

assert(ajv.validateSchema(schema))
```

You will need a compatible library, like [Ajv](https://www.npmjs.com/package/ajv), to validate objects:

```javascript
var validBooleanJSON = ajv.compile(schema)
```

The simplest valid expression is just a variable name:

```javascript
assert(validBooleanJSON('first'))
```

The syntax is very minimal. The schema permits negation, conjunction, disjunction, and arbitrary combinations:

```javascript
assert(validBooleanJSON({not: 'x'}))

assert(validBooleanJSON({and: ['x', 'y']}))

assert(validBooleanJSON({or: ['x', 'y']}))

assert(validBooleanJSON({and: [{or: ['x', 'y']}, {not: 'z'}]}))
```

Conjunctions and disjunctions must have at least two operands:

```javascript
assert(validBooleanJSON({and: ['x']}) === false)
assert(validBooleanJSON({and: ['x', 'y', 'z']}) === true)

assert(validBooleanJSON({or: ['x']}) === false)
assert(validBooleanJSON({or: ['x', 'y', 'z']}) === true)
```
