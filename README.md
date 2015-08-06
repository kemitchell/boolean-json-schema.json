```javascript
var schema = require('boolean-json-schema')
var assert = require('assert')
var validate = require('tv4').validate

assert(
  validate(
    { variable: 'first' },
  schema))

assert(
  validate(
    { and: [
        { variable: 'x' },
        { variable: 'y' } ] },
  schema))

assert(
  validate(
    { not: {
	    variable: 'x' } },
  schema))

assert(
  validate(
    { or: [
        { variable: 'x' },
        { variable: 'y' } ] },
  schema))

assert(
  validate(
    { and: [
        { or: [
		  { variable: 'x' },
          { variable: 'y' } ] },
        { not: {
		  variable: 'z' } } ] },
  schema))
```
