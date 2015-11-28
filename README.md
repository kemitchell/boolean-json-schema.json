```javascript
var schema = require('boolean-json-schema')
```

The package exports a [JSON Schema](http://json-schema.org). You will need a compatible library to validate objects:

```javascript
var validate = require('tv4').validate
```

The simplest valid expression is just a variable name:

```javascript
var assert = require('assert')

assert(validate('first', schema))
```

The syntax is very minimal. The schema permits negation, conjunction, disjunction, and arbitrary combinations:

```javascript
assert(validate({ not: 'x' }, schema))

assert(validate({ and: [ 'x', 'y' ] }, schema))

assert(validate({ or: [ 'x', 'y' ] }, schema))

assert(validate({ and: [ { or: [ 'x', 'y' ] }, { not: 'z' } ] }, schema))
```

Conjunctions and disjunctions must have at least two operands:

```javascript
assert(validate({ and: [ 'x' ]}, schema) === false)
assert(validate({ and: [ 'x', 'y', 'z' ]}, schema) === true)

assert(validate({ or: [ 'x' ]}, schema) === false)
assert(validate({ or: [ 'x', 'y', 'z' ]}, schema) === true)
```
