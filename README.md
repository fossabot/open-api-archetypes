# `open-api-archetypes`

[![License][license-image]][license-url] [![FOSSA Status][fossa-image]][fossa-url] [![NPM version][npm-image]][npm-url] <br>[![NSP Status][nsp-img]][nsp-url] [![Dependency Status][daviddm-image]][daviddm-url] [![devDependencies Status][daviddm-dev-image]][daviddm-dev-url] <br>[![Swagger Validity][swagger-validity-image]][swagger-validity-url]
[![Build Status][travis-image]][travis-url] [![Coverage percentage][coveralls-image]][coveralls-url] [![Codacy quality][codacy-image]][codacy-url]

> Self-evident and semantically-rich OpenAPI specifications of universally recurring business entities, events, and relationships, based on [_Enterprise patterns and MDA: building better software with archetype patterns and UML_][mda-book-url] by Arlow, J., & Neustadt, I.

## Table of contents

<!-- toc -->

- [1. Installation](#1-installation)
- [2. Usage](#2-usage)
  * [2.1. `curl`](#21-curl)
  * [2.2. `javascript-client` library](#22-javascript-client-library)
- [3. API documentation](#3-api-documentation)
  * [3.1. `ErrorResponse`](#31-errorresponse)
  * [3.2. `Locale`](#32-locale)
  * [3.3. `Party`](#33-party)
  * [3.4. `Quantity`](#34-quantity)
- [4. Quality gates, reports, and documentation](#4-quality-gates-reports-and-documentation)
  * [4.1. Swagger validation and badge](#41-swagger-validation-and-badge)
  * [4.2. Linting](#42-linting)
  * [4.3. Test execution and code coverage](#43-test-execution-and-code-coverage)
- [5. Semantic version and CHANGELOG](#5-semantic-version-and-changelog)
- [6. Contributing to `open-api-archetypes`](#6-contributing-to-open-api-archetypes)
  * [6.1. Code of conduct](#61-code-of-conduct)
  * [6.2. Individual contributor license agreement](#62-individual-contributor-license-agreement)
  * [6.3. Development, testing, and documentation](#63-development-testing-and-documentation)
- [7. Licenses](#7-licenses)
  * [7.1. `open-api-archetypes`'s license](#71-open-api-archetypess-license)
  * [7.2. Third-party dependencies' licenses](#72-third-party-dependencies-licenses)

<!-- tocstop -->

## 1. Installation

Open a Terminal and run this command:

```bash
$ npm install --save open-api-archetypes
```

If your team prefers Yarn:

```bash
$ yarn add open-api-archetypes
```

## 2. Usage

### 2.1. `curl`

The simplest way to test against mock objects at `http://api.swindle.net/archetypes/v1/parties` with `curl` in a Terminal.

```bash
$ curl -X GET "http://api.swindle.net/archetypes/v1/parties/2e908e75-69a9-47e2-83ae-0c3cc52da84c" \
  -H "accept: application/json"
```

### 2.2. `javascript-client` library

```javascript
const Party = require('party')

const api = new Party.PartiesApi()

// {String} The universally unique identifier associated with a Party.
const uuid = '2e908e75-69a9-47e2-83ae-0c3cc52da84c'

const callback = (error, data, response) => {
  if (error) {
    console.error(error)
  } else {
    console.log(
      'API called successfully. Returned data: ' +
      JSON.stringify(data, null, 2)
    )
  }
  console.log(response)
}
api.getPartyByUuid(uuid, callback)
```

## 3. API documentation

### 3.1. `ErrorResponse`

The [`ErrorResponse`](./lib/error-response/javascript-client/README.md) archetype represents a `LoggingEvent` instance that provides a meaningful response for errors.

**Example:**

```js
const ErrorResponse = require('error_response')

const api = new ErrorResponse.ErrorResponsesApi()

const callback = (error, data, response) => {
  if (error) {
    console.error(error)
  } else {
    console.log(
      'API called successfully. Returned data: ' +
      JSON.stringify(data, null, 2)
    )
  }
  console.log(response)
}

api.getErrorResponse400(callback)
```

### 3.2. `Locale`

The [`Locale`](./lib/locale/javascript-client/README.md) archetype represents a general notion of place, location, or context. Its sub-class `IsoCountryCode` extends `Locale` to provide a country defined in ISO 3166.

**Example: fetch a country by its ISO 3166 alphabetic two-character country-code:**

```js
const Locale = require('locale')

const api = new Locale.IsocountrycodesApi()

// {String} The (upper case) ISO 3166 alphabetic two-character value,
// e.g., "US" for the United States of America, or "IN" for India.
const identifier = 'AF' // Afghanistan

const callback = (error, data, response) => {
  if (error) {
    console.error(error)
  } else {
    console.log(
      'API called successfully. Returned data: ' +
      JSON.stringify(data, null, 2)
    )
  }
  console.log(response)
}

api.getIsoCountryCodeById(identifier, callback)
```

### 3.3. `Party`

The [`Party`](./lib/party/javascript-client/README.md) archetype represents an identifiable, addressable entity that may have a legal status and that normally has autonomous control over (at least some of) its actions.

**Example: retrieve a Party by its universally-unique identifier:**

```js
const Party = require('party')

const api = new Party.PartiesApi()

// {String} The universally unique identifier associated with a Party.
const uuid = '2e908e75-69a9-47e2-83ae-0c3cc52da84c'

const callback = (error, data, response) => {
  if (error) {
    console.error(error)
  } else {
    console.log(
      'API called successfully. Returned data: ' +
      JSON.stringify(data, null, 2)
    )
  }
  console.log(response)
}
api.getByUuid(uuid, callback)
```

### 3.4. `Quantity`

The [`Quantity`](./lib/quantity/javascript-client/README.md) archetype represents an amount of something measured according to some standard of measurement.

**Example:**

```js
const Quantity = require('quantity')

const api = new Quantity.SIInternationalSystemOfUnitsApi()

// {String} The name of the unit/metric.
const name = 'meter'

const callback = (error, data, response) => {
  if (error) {
    console.error(error)
  } else {
    console.log(
      'API called successfully. Returned data: ' +
      JSON.stringify(data, null, 2)
    )
  }
  console.log(response)
}

api.getBaseUnitByName(name, callback)
```

## 4. Quality gates, reports, and documentation

This repository enforces Swagger quality; Javascript quality; and Javascript unit tests and code coverage.

### 4.1. Swagger validation and badge
> :trophy: `open-api-archetypes` validates Swagger docs with [`swagger-cli`][swagger-cli-url].

[`swagger-cli`][swagger-cli-url] validation runs before every test execution:

```bash
# These two npm-scripts run lint automatically:
$ npm run pretest

$ npm test

# Lint Javascript callouts and Swagger *.yml or *.json docs:
$ npm run lint

# You can also validate your Swagger docs independently with:
$ npm run swagger:lint

```

[`swagger-api/validator-badge`](https://github.com/swagger-api/validator-badge)s display whether there are syntactic issues with you Swagger/OpenAPI 2.0 document.

### 4.2. Linting
> :closed_lock_with_key: :bath: :ocean: `open-api-archetypes` lints source code; checks for vulnerabilities; assesses dependency drift; and executes quality gates with `BitHound`, `eslint`, `nsp`, and `SonarQube`/`sonarcloud`.
>
> The results are displayed real-time with README badges.

```bash
# Code quality analysis runs before every test execution:
$ npm test

# Validate Swagger and analyze Javascript callouts:
$ npm run lint

# Only run ESLint for a CLI summary:
$ npm run eslint:stylish

# Generate an HTML report with links to errors and warnings:
$ npm run eslint:html
```

### 4.3. Test execution and code coverage
> :100: `open-api-archetypes` uses `jest` for BDD spec execution and code coverage analysis.
>
> The results are displayed real-time with README badges.

Generate detailed code coverage reports at `coverage/lcov-report/index.html` and `lcov.info` and `clover.xml` files  (which you can send to CI test coverage services like  Coveralls and  [OneSonarQube][one-sonar-url] or [SonarCloud][sonarcloud-url]):

```bash
$ npm test
```

## 5. Semantic version and CHANGELOG

The latest version of `open-api-archetypes` is `vtrue`. View the [CHANGELOG][changelog-url] for details.

## 6. Contributing to `open-api-archetypes`

![Alt text](https://camo.githubusercontent.com/f96261621753dacf526590825b84f87ccb1db0e6/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5052732d77656c636f6d652d627269676874677265656e2e7376673f7374796c653d666c6174 "Pull Request") We welcome contributors and pull requests!

Contributions are community-driven stories with a beginning, a middle, and an end, all told through issues, comments, and pull requests.

### 6.1. Code of conduct

Our [Contributor Covenant Code of Conduct][code-of-conduct-url] expresses our commitment to making participation a harassment-free experience for everyone, regardless of age, body size, disability, ethnicity, gender identity and expression, level of experience, nationality, personal appearance, race, religion, or sexual identity and orientation. Please review the [Contributor Covenant Code of Conduct][code-of-conduct-url] for details.

### 6.2. Individual contributor license agreement

Need a CLA? If so, please sign the [Contributor License Agreement][cla-url].

### 6.3. Development, testing, and documentation

After reviewing the guidelines for [contributing to `open-api-archetypes`][contributing-url] and our [Contributor Covenant Code of Conduct][code-of-conduct-url], feel free to

* [Peruse open issues][issues-url],
* [Submit a new issue][issues-new-url], or
* [Open a new pull request (PR)][pr-url]

## 7. Licenses

### 7.1. `open-api-archetypes`'s license

[Apache-2.0][license-url] © [Greg Swindle](https://githbub.com/gregswindle)

### 7.2. Third-party dependencies' licenses

[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Fgregswindle%2Fopen-api-archetypes.svg?type=large)](https://app.fossa.io/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Fgregswindle%2Fopen-api-archetypes?ref=badge_large)

---
[![Greenkeeper badge][greenkeeper-image]][greenkeeper-url] [![Readme Score][readme-score-img]][readme-score-url]


[changelog-url]: ./CHANGELOG.md
[cla-url]: https://www.clahub.com/agreements/gregswindle/open-api-archetypes
[codacy-image]: https://api.codacy.com/project/badge/Grade/bbc816a1fecd459b9d958bf2e862b66a
[codacy-url]: https://www.codacy.com/app/greg_7/open-api-archetypes?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=gregswindle/open-api-archetypes&amp;utm_campaign=Badge_Grade
[code-of-conduct-url]: ./CODE_OF_CONDUCT.md
[complexity-report-url]: ./docs/COMPLEXITY.md
[contributing-url]: ./CONTRIBUTING.md
[coveralls-image]: https://coveralls.io/repos/gregswindle/open-api-archetypes/badge.svg
[coveralls-url]: https://coveralls.io/r/gregswindle/open-api-archetypes
[daviddm-dev-image]: https://david-dm.org/gregswindle/open-api-archetypes/dev-status.svg
[daviddm-dev-url]: https://david-dm.org/gregswindle/open-api-archetypes?type=dev
[daviddm-image]: https://david-dm.org/gregswindle/open-api-archetypes.svg?theme=shields.io
[daviddm-url]: https://david-dm.org/gregswindle/open-api-archetypes
[fossa-image]: https://app.fossa.io/api/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Fgregswindle%2Fopen-api-archetypes.svg?type=shield
[fossa-url]: https://app.fossa.io/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Fgregswindle%2Fopen-api-archetypes?ref=badge_shield
[greenkeeper-image]: https://badges.greenkeeper.io/gregswindle/open-api-archetypes.svg
[greenkeeper-url]: https://greenkeeper.io/
[issues-url]: https://github.com/gregswindle/open-api-archetypes/issues
[issues-new-url]: https://github.com/gregswindle/open-api-archetypes/issues/new
[js-callout-docs-url]: ./docs/JSCAPIS.md
[jsdoc-url]: http://usejsdoc.org/
[jsdoc2md-url]: https://github.com/jsdoc2md/jsdoc-to-markdown
[license-image]: https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=flat
[license-url]: /LICENSE
[license-url]: https://github.com/gregswindle/open-api-archetypes/blob/master/LICENSE
[mda-book-url]: https://www.amazon.com/Enterprise-Patterns-MDA-Building-Archetype/dp/032111230X
[npm-image]: https://badge.fury.io/js/open-api-archetypes.svg
[npm-url]: https://npmjs.org/package/open-api-archetypes
[nsp-img]: https://nodesecurity.io/orgs/gregswindle/projects/321f4365-67f4-41db-9b16-1c8712fcfd94/badge
[nsp-sign-up-url]: https://nodesecurity.io/signup
[nsp-url]: https://nodesecurity.io/orgs//projects/REPLACE-THIS-WITH-YOUR-NSP-UUID
[one-sonar-url]: http://onesonar.verizon.com/
[pr-url]: /gregswindle/open-api-archetypes/pulls
[readme-score-img]: http://readme-score-api.herokuapp.com/score.svg?url=https://github.com/gregswindle/open-api-archetypes
[readme-score-url]: http://clayallsopp.github.io/readme-score?url=https://github.com/gregswindle/open-api-archetypes
[sonarcloud-url]: https://sonarcloud.io
[swagger-api-docs-url]: ./docs/SWAGGER.md
[swagger-cli-url]: https://github.com/BigstickCarpet/swagger-cli
[swagger-io-url]: http://swagger.io
[swagger-logo-20-image]: ./.assets/media/img/swagger-logo-20.png
[swagger-markdown-url]: https://github.com/syroegkin/swagger-markdown
[swagger-validity-image]: https://img.shields.io/swagger/valid/2.0/https/raw.githubusercontent.com/gregswindle/open-api-archetypes/master/openapi/open-api-archetypes.swagger.yaml.svg
[swagger-validity-url]: http://online.swagger.io/validator?url=https://raw.githubusercontent.com/gregswindle/open-api-archetypes/master/openapi/open-api-archetypes.swagger.yaml
[travis-image]: https://travis-ci.org/gregswindle/open-api-archetypes.svg?branch=master
[travis-url]: https://travis-ci.org/gregswindle/open-api-archetypes
