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
var validate = ajv.compile(schema)
```

The simplest valid expression is just a variable name:

```javascript
assert(validate('first'))
```

The syntax is very minimal. The schema permits negation, conjunction, disjunction, and arbitrary combinations:

```javascript
assert(validate({not: 'x'}))

assert(validate({and: ['x', 'y']}))

assert(validate({or: ['x', 'y']}))

assert(validate({and: [{or: ['x', 'y']}, {not: 'z'}]}))
```

Conjunctions and disjunctions must have at least two operands:

```javascript
assert(validate({and: ['x']}) === false)
assert(validate({and: ['x', 'y', 'z']}) === true)

assert(validate({or: ['x']}) === false)
assert(validate({or: ['x', 'y', 'z']}) === true)
```
