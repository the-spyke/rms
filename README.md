# JavaScript Raw Module Specification

`version 0.3.0`

## Summary

`Raw Module Specification` or `RMS` is a convention for modern JavaScript packages and modules aiming to avoid excess code recompilation and deoptimization, retaining code readability and ease of debugging.

To achieve these goals `RMS` suggests to publish packages in the native `ECMAScript Modules` or `ESM` format and without down compilation to `ES5`. Consuming packages not in `ES5` format may be difficult as you need to know how to compile/process every single dependency package. Same time JavaScript is a developing language and new features appear every time. Luckily its development conforms to a specialized process governed by [TC39](https://tc39.es/) group. Language features are developed as proposals and pass through several _stages_ during their life cycle.

Today's applications consist of hundreds and thousands of files of different kinds. To manage this complexity and streamline app delivery developers started using the same approach as on desktops: compile & link. In relation to a web application `compilation` usually means `transpiling`, while `linking` means `bundling`. [Babel](https://babeljs.io/) became a _de facto_ tool for down compiling JavaScript code to older versions and could be used as an integration point.

`RMS` leverages `TC39` process and `Babel` and defines rules for consuming and upgrading compliant packages without a hustle.

The key words `MUST`, `MUST NOT`, `REQUIRED`, `SHALL`, `SHALL NOT`, `SHOULD`, `SHOULD NOT`, `RECOMMENDED`, `MAY`, and `OPTIONAL` in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

## Specification

RMS adheres to the [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

### Package requirements

* Package *SHOULD* adhere Semantic Versioning.
* Package *MUST* follow [Node.js ESM package format](https://nodejs.org/dist/latest/docs/api/packages.html) and have `module` type in its package.json.
* Package *MUST* contain valid `ESM` modules.
* Package *MUST NOT* contain any code using features unsupported in the latest stable `@babel/preset-env` or `core-js`. Usually this means simply not using unfinished [proposals](https://github.com/tc39/proposals).
* Upgrading to a newer MAJOR `@babel/preset-env` or `core-js` version *IS* a *BREAKING CHANGE*.
* Package *MUST* mention its RMS compliance with exact RMS version number in its README file.
* If package doesn't have `@babel/preset-env` and/or `core-js` in its `package.json`, target versions *SHOULD* be specified in the README.

### Installing the package

1. Check `package.json` and README for target `@babel/preset-env` and `core-js` versions.
2. Make sure that your environment is compatible.
3. Install the package.
4. Compile the package with Babel using `@babel/preset-env` and load stable polyfills from `core-js` (this could be done in preset options setting `corejs` and `useBuiltIns` props).

### Upgrading the package to a newer MINOR or PATCH release

1. Upgrade `@babel/preset-env` and `core-js` to their latest stable MINOR and PATCH versions.
2. Upgrade the package.

### Upgrading the package to a newer MAJOR release

1. Check `package.json` and README if the package requires newer MAJOR `@babel/preset-env` and `core-js` versions.
2. Make sure that your environment is compatible.
3. Upgrade the package.

## Miscellaneous

Add a badge to your project README or page:

```md
[![Raw Module Specification 0.3.0](https://img.shields.io/badge/RMS-0.3.0-blue)](https://github.com/the-spyke/rms)
```

[![Raw Module Specification 0.3.0](https://img.shields.io/badge/RMS-0.3.0-blue)](https://github.com/the-spyke/rms)

## License

Licensed under the MIT License, see [LICENSE](LICENSE) for more information.

## Projects compliant with RMS

* [Undercut](https://github.com/the-spyke/undercut): JavaScript lazy data processing pipelines and utilities.
