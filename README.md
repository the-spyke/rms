# JavaScript Raw Module Specification

`version 0.2.1`

## Summary

`Raw Module Specification` or `RMS` is a convention for modern JavaScript packages and modules aiming to avoid excess code recompilation and deoptimization, retaining code readability and ease of debugging.

To achieve these goals `RMS` suggests to publish packages in the native `ECMAScript Modules` or `ESM` format and without down compilation to `ES5`. Consuming packages not in `ES5` format may be difficult as you need to know how to compile/process every single dependency package. Same time JavaScript is a developing language and new features appear every time. Luckily its development conforms to a specialized process governed by [TC39](https://tc39.es/) group. Language features are developed as proposals and pass through several _stages_ during their life cycle.

Today's applications consist of hundreds and thousands of files of different kinds. To manage this complexity and streamline app delivery developers started using the same approach as on desktops: compile & link. In relation to a web application `compilation` usually means `transpiling`, while `linking` means `bundling`. [Babel](https://babeljs.io/) became a _defacto_ tool for down compiling JavaScript code to older versions and could be used as an integration point.

`RMS` leverages `TC39` process and `Babel` and defines rules for consuming and upgrading compliant packages without a hustle.

The key words `MUST`, `MUST NOT`, `REQUIRED`, `SHALL`, `SHALL NOT`, `SHOULD`, `SHOULD NOT`, `RECOMMENDED`, `MAY`, and `OPTIONAL` in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

## Specification

### Package requirements

* Package *MUST* follow [Node.js ESM package format](https://nodejs.org/dist/latest/docs/api/packages.html) and have `module` type in its package.json.
* Package *MUST* contain valid `ESM` modules.
* Package *MUST NOT* contain any code using features unsupported in the latest stable `@babel/preset-env` or `core-js`. Usually this means simply not using unfinished [proposals](https://github.com/tc39/proposals).
* Upgrading to a newer _major_ `Babel` version *IS* a _breaking change_.

### Installing a package

1. Install the latest stable `@babel/preset-env` and `core-js`.
2. Install the package.
3. At build time compile the package with Babel using `@babel/preset-env` preset and load stable polyfills from `core-js` (this could be done in preset options setting `corejs` and `useBuiltIns` props).

### Upgrading the package

1. Upgrade `@babel/preset-env` and `core-js` to their latest stable versions.
2. Upgrade the package.

## Miscellaneous

Add a badge to your project readme or page:

```md
[![Raw Module Specification Compliant](https://img.shields.io/badge/RMS-Compliant-blue)](https://github.com/the-spyke/rms)
```

[![Raw Module Specification Compliant](https://img.shields.io/badge/RMS-Compliant-blue)](https://github.com/the-spyke/rms)

## License

Licensed under the MIT License, see [LICENSE](LICENSE) for more information.

## Projects compliant with RMS

* [Undercut](https://github.com/the-spyke/undercut): JavaScript lazy data processing pipelines and utilities.
