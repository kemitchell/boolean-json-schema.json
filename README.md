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

### Related

* [kemitchell/boolean-json-eval.js](https://github.com/kemitchell/boolean-json-eval.js): Evaluate boolean-json expressions
* [kemitchell/boolean-json-cnf.js](https://github.com/kemitchell/boolean-json-cnf.js): Convert boolean-json to Conjunctive Normal Form
* [kemitchell/boolean-json-variables.js](https://github.com/kemitchell/boolean-json-variables.js): Identify variables in boolean-json objects
* [kemitchell/boolean-json-brute-force.js](https://github.com/kemitchell/boolean-json-brute-force.js): Solve a boolean-json expression by brute force
* [kemitchell/boolean-json-bifurcate.js](https://github.com/kemitchell/boolean-json-bifurcate.js): Bifurcate a boolean-json expression
* [RobertHerhold/boolean-json-prune](https://github.com/RobertHerhold/boolean-json-prune): Prune a boolean-json expression
* [RobertHerhold/boolean-json-joi-schema](https://github.com/RobertHerhold/boolean-json-joi-schema): [Joi](https://github.com/hapijs/joi) port of the boolean-json schema
