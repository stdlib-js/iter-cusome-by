<!--

@license Apache-2.0

Copyright (c) 2024 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# iterCuSomeBy

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Create an iterator which cumulatively tests whether at least `n` iterated values pass a test implemented by a predicate function.

<!-- Section to include introductory text. Make sure to keep an empty line after the intro `section` element and another before the `/section` close. -->

<section class="intro">

</section>

<!-- /.intro -->

<!-- Package usage documentation. -->



<section class="usage">

## Usage

```javascript
import iterCuSomeBy from 'https://cdn.jsdelivr.net/gh/stdlib-js/iter-cusome-by@esm/index.mjs';
```
The previous example will load the latest bundled code from the esm branch. Alternatively, you may load a specific version by loading the file from one of the [tagged bundles](https://github.com/stdlib-js/iter-cusome-by/tags). For example,

```javascript
import iterCuSomeBy from 'https://cdn.jsdelivr.net/gh/stdlib-js/iter-cusome-by@v0.1.1-esm/index.mjs';
```

#### iterCuSomeBy( iterator, n, predicate\[, thisArg] )

Returns an [iterator][mdn-iterator-protocol] which cumulatively tests whether at least `n` iterated values pass a test implemented by a `predicate` function.

```javascript
import array2iterator from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-to-iterator@esm/index.mjs';

function isPositive( v ) {
    return ( v > 0 );
}

var arr = array2iterator( [ 0, 0, 0, 1, 1 ] );

var it = iterCuSomeBy( arr, 2, isPositive );

var v = it.next().value;
// returns false

v = it.next().value;
// returns false

v = it.next().value;
// returns false

v = it.next().value;
// returns false

v = it.next().value;
// returns true

var bool = it.next().done;
// returns true
```

The returned [iterator][mdn-iterator-protocol] protocol-compliant object has the following properties:

-   **next**: function which returns an [iterator][mdn-iterator-protocol] protocol-compliant object containing the next iterated value (if one exists) assigned to a `value` property and a `done` property having a `boolean` value indicating whether the [iterator][mdn-iterator-protocol] is finished.
-   **return**: function which closes an [iterator][mdn-iterator-protocol] and returns a single (optional) argument in an [iterator][mdn-iterator-protocol] protocol-compliant object.

A `predicate` function is provided two arguments:

-   **value**: iterated value.
-   **index**: iteration index (zero-based).

To set the `predicate` function execution context, provide a `thisArg`.

<!-- eslint-disable no-invalid-this -->

```javascript
import array2iterator from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-to-iterator@esm/index.mjs';

function predicate( v ) {
    this.count += 1;
    return ( v > 0 );
}

var arr = array2iterator( [ 0, 0, 1, 1, 1 ] );

var ctx = {
    'count': 0
};

var it = iterCuSomeBy( arr, 3, predicate, ctx );
// returns <Object>

var v = it.next().value;
// returns false

v = it.next().value;
// returns false

v = it.next().value;
// returns false

v = it.next().value;
// returns false

v = it.next().value;
// returns true

var count = ctx.count;
// returns 5
```

</section>

<!-- /.usage -->

<!-- Package usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

## Notes

-   A `predicate` function is invoked for each iterated value until the `nth` truthy `predicate` function return value. The returned iterator continues iterating until it reaches the end of the input iterator, even after the condition is met.

</section>

<!-- /.notes -->

<!-- Package usage examples. -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```html
<!DOCTYPE html>
<html lang="en">
<body>
<script type="module">

import randu from 'https://cdn.jsdelivr.net/gh/stdlib-js/random-iter-randu@esm/index.mjs';
import iterCuSomeBy from 'https://cdn.jsdelivr.net/gh/stdlib-js/iter-cusome-by@esm/index.mjs';

function threshold( r ) {
    return ( r > 0.95 );
}

// Create an iterator which generates uniformly distributed pseudorandom numbers:
var opts = {
    'iter': 100
};
var riter = randu( opts );

// Create an iterator which tracks whether at least two values have exceeded the threshold:
var it = iterCuSomeBy( riter, 2, threshold );

// Perform manual iteration...
var r;
while ( true ) {
    r = it.next();
    if ( r.done ) {
        break;
    }
    console.log( r.value );
}

</script>
</body>
</html>
```

</section>

<!-- /.examples -->

<!-- Section to include cited references. If references are included, add a horizontal rule *before* the section. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="references">

</section>

<!-- /.references -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/iter-cusome-by.svg
[npm-url]: https://npmjs.org/package/@stdlib/iter-cusome-by

[test-image]: https://github.com/stdlib-js/iter-cusome-by/actions/workflows/test.yml/badge.svg?branch=v0.1.1
[test-url]: https://github.com/stdlib-js/iter-cusome-by/actions/workflows/test.yml?query=branch:v0.1.1

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/iter-cusome-by/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/iter-cusome-by?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/iter-cusome-by.svg
[dependencies-url]: https://david-dm.org/stdlib-js/iter-cusome-by/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/iter-cusome-by/tree/deno
[deno-readme]: https://github.com/stdlib-js/iter-cusome-by/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/iter-cusome-by/tree/umd
[umd-readme]: https://github.com/stdlib-js/iter-cusome-by/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/iter-cusome-by/tree/esm
[esm-readme]: https://github.com/stdlib-js/iter-cusome-by/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/iter-cusome-by/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/iter-cusome-by/main/LICENSE

[mdn-iterator-protocol]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterator_protocol

</section>

<!-- /.links -->
