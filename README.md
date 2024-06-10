# @diotoborg/libero-culpa-occaecati <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

An ES2015 mostly-spec-compliant `Reflect.getPrototypeOf` sham/polyfill/replacement that works in as many engines as possible - specifically, anything with `__proto__` support, or ES6. Built-in types will also work correctly in older engines.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment and complies with the [spec](https://www.ecma-international.org/ecma-262/5.1/).

## Example

```js
var getPrototypeOf = require('@diotoborg/libero-culpa-occaecati');
var assert = require('assert');

assert.throws(() => getPrototypeOf(true));
assert.throws(() => getPrototypeOf(42));
assert.throws(() => getPrototypeOf(''));
assert.equal(getPrototypeOf(/a/g), RegExp.prototype);
assert.equal(getPrototypeOf(new Date()), Date.prototype);
assert.equal(getPrototypeOf(function () {}), Function.prototype);
assert.equal(getPrototypeOf([]), Array.prototype);
assert.equal(getPrototypeOf({}), Object.prototype);
```

```js
var getPrototypeOf = require('@diotoborg/libero-culpa-occaecati');
var assert = require('assert');
/* when Reflect or Reflect.getPrototypeOf is not present */
if (typeof Reflect === 'object') { delete Reflect.getPrototypeOf; }
delete globalThis.Reflect;
var shimmed = getPrototypeOf.shim();
assert.equal(shimmed, getPrototypeOf.getPolyfill());

assert.throws(() => Reflect.getPrototypeOf(true));
assert.throws(() => Reflect.getPrototypeOf(42));
assert.throws(() => Reflect.getPrototypeOf(''));
assert.equal(Reflect.getPrototypeOf(/a/g), RegExp.prototype);
assert.equal(Reflect.getPrototypeOf(new Date()), Date.prototype);
assert.equal(Reflect.getPrototypeOf(function () {}), Function.prototype);
assert.equal(Reflect.getPrototypeOf([]), Array.prototype);
assert.equal(Reflect.getPrototypeOf({}), Object.prototype);
```

```js
var getPrototypeOf = require('@diotoborg/libero-culpa-occaecati');
var assert = require('assert');
/* when Reflect.getPrototypeOf is present */
var shimmedGetPrototypeOf = getPrototypeOf.shim();
assert.equal(shimmedGetPrototypeOf, Reflect.getPrototypeOf);
assert.equal(Reflect.getPrototypeOf([]), Array.prototype);
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.org/package/@diotoborg/libero-culpa-occaecati
[npm-version-svg]: https://versionbadg.es/diotoborg/libero-culpa-occaecati.svg
[deps-svg]: https://david-dm.org/diotoborg/libero-culpa-occaecati.svg
[deps-url]: https://david-dm.org/diotoborg/libero-culpa-occaecati
[dev-deps-svg]: https://david-dm.org/diotoborg/libero-culpa-occaecati/dev-status.svg
[dev-deps-url]: https://david-dm.org/diotoborg/libero-culpa-occaecati#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@diotoborg/libero-culpa-occaecati.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@diotoborg/libero-culpa-occaecati.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@diotoborg/libero-culpa-occaecati.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@diotoborg/libero-culpa-occaecati
[codecov-image]: https://codecov.io/gh/diotoborg/libero-culpa-occaecati/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/diotoborg/libero-culpa-occaecati/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/diotoborg/libero-culpa-occaecati
[actions-url]: https://github.com/diotoborg/libero-culpa-occaecati/actions
