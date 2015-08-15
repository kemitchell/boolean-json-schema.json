```javascript
var schema = require('boolean-json-schema')
var assert = require('assert')
var validate = require('tv4').validate

assert(
  validate(
    'first',
  schema))

assert(
  validate(
    { and: [ 'x', 'y' ] },
  schema))

assert(
  validate(
    { not: 'x' },
  schema))

assert(
  validate(
    { or: [ 'x', 'y' ] },
  schema))

assert(
  validate(
    { and: [
        { or: [ 'x', 'y' ] },
        { not: 'z' } ] },
  schema))
```
