```javascript
var schema = require('boolean-json-schema')
```

The package exports a [JSON Schema](http://json-schema.org). You will need a compatible library to validate objects:

```javascript
var ajv = new (require('ajv'))()
var assert = require('assert')

assert(ajv.validateSchema(schema))
var validate = ajv.compile(schema)
```

The simplest valid expression is just a variable name:

```javascript
assert(validate('first', schema))
```

The syntax is very minimal. The schema permits negation, conjunction, disjunction, and arbitrary combinations:

```javascript
assert(validate({not: 'x'}, schema))

assert(validate({and: ['x', 'y']}, schema))

assert(validate({or: ['x', 'y']}, schema))

assert(validate({and: [{or: ['x', 'y']}, {not: 'z'}]}, schema))
```

Conjunctions and disjunctions must have at least two operands:

```javascript
assert(validate({and: ['x']}, schema) === false)
assert(validate({and: ['x', 'y', 'z']}, schema) === true)

assert(validate({or: ['x']}, schema) === false)
assert(validate({or: ['x', 'y', 'z']}, schema) === true)
```
