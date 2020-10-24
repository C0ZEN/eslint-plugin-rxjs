# eslint-plugin-rxjs

[![GitHub License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/cartant/eslint-plugin-rxjs/blob/master/LICENSE)
[![NPM version](https://img.shields.io/npm/v/eslint-plugin-rxjs.svg)](https://www.npmjs.com/package/eslint-plugin-rxjs)
[![Downloads](http://img.shields.io/npm/dm/eslint-plugin-rxjs.svg)](https://npmjs.org/package/eslint-plugin-rxjs)
[![Build status](https://img.shields.io/circleci/build/github/cartant/eslint-plugin-rxjs?token=34077d419805b6295c5a946a155dc7ff142926c5)](https://app.circleci.com/pipelines/github/cartant)
[![dependency status](https://img.shields.io/david/cartant/eslint-plugin-rxjs.svg)](https://david-dm.org/cartant/eslint-plugin-rxjs)
[![devDependency Status](https://img.shields.io/david/dev/cartant/eslint-plugin-rxjs.svg)](https://david-dm.org/cartant/eslint-plugin-rxjs#info=devDependencies)
[![peerDependency Status](https://img.shields.io/david/peer/cartant/eslint-plugin-rxjs.svg)](https://david-dm.org/cartant/eslint-plugin-rxjs#info=peerDependencies)

This package contains a bunch of ESLint rules for RxJS. Essentially, it's a re-implementation of the rules that are in the [`rxjs-tslint-rules`](https://github.com/cartant/rxjs-tslint-rules) package. (The Angular-specific rules in `rxjs-tslint-rules` have been re-implemented in [`eslint-plugin-rxjs-angular`](https://github.com/cartant/eslint-plugin-rxjs-angular).)

Some of the rules are rather opinionated and are not included in the `recommended` configuration. Developers can decide for themselves whether they want to enable opinionated rules.

Almost all of these rules require the TypeScript parser for ESLint.

# Install

Install the ESLint TypeScript parser using npm:

```
npm install @typescript-eslint/parser --save-dev
```

Install the package using npm:

```
npm install eslint-plugin-rxjs --save-dev
```

Configure the `parser` and the `parserOptions` for ESLint. Here, I use a `.eslintrc.js` file for the configuration:

```js
const { join } = require("path");
module.exports = {
  parser: "@typescript-eslint/parser",
  parserOptions: {
    ecmaVersion: 2019,
    project: join(__dirname, "./tsconfig.json"),
    sourceType: "module"
  },
  plugins: ["rxjs"],
  extends: [],
  rules: {
    "rxjs/no-async-subscribe": "error",
    "rxjs/no-ignored-observable": "error",
    "rxjs/no-ignored-subscription": "error",
    "rxjs/no-nested-subscribe": "error",
    "rxjs/no-unbound-methods": "error",
    "rxjs/throw-error": "error"
  }
};
```

Or, using the `recommended` configuration:

```js
const { join } = require("path");
module.exports = {
  parser: "@typescript-eslint/parser",
  parserOptions: {
    ecmaVersion: 2019,
    project: join(__dirname, "./tsconfig.json"),
    sourceType: "module"
  },
  extends: ["plugin:rxjs/recommended"],
};
```

# Rules

The package includes the following rules:

| Rule | Description | Recommended |
| --- | --- | --- |
| [`ban-observables`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/ban-observables.md) | Forbids the use of banned observables. | No |
| [`ban-operators`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/ban-operators.md) | Forbids the use of banned operators. | No |
| [`finnish`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/finnish.md) | Enforces the use of Finnish notation. | No |
| [`just`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/just.md) | Enforces the use of a `just` alias for `of`. | No |
| [`no-async-subscribe`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-async-subscribe.md) | Forbids passing `async` functions to `subscribe`. | Yes |
| [`no-compat`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-compat.md) | Forbids importation from locations that depend upon `rxjs-compat`. | No |
| [`no-connectable`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-connectable.md) | Forbids operators that return connectable observables. | No |
| [`no-create`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-create.md) | Forbids the calling of `Observable.create`. | Yes |
| [`no-explicit-generics`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-explicit-generics.md) | Forbids explicit generic type arguments. | No |
| [`no-exposed-subjects`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-exposed-subjects.md) | Forbids exposed  (i.e. non-private) subjects. | No |
| [`no-finnish`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-finnish.md) | Forbids the use of Finnish notation. | No |
| [`no-ignored-error`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-ignored-error.md) | Forbids the calling of `subscribe` without specifying an error handler. | No |
| [`no-ignored-notifier`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-ignored-notifier.md) | Forbids observables not composed from the `repeatWhen` or `retryWhen` notifier. | Yes |
| [`no-ignored-observable`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-ignored-observable.md) | Forbids the ignoring of observables returned by functions. | No |
| [`no-ignored-replay-buffer`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-ignored-replay-buffer.md) | Forbids using `ReplaySubject`, `publishReplay` or `shareReplay` without specifying the buffer size. | Yes |
| [`no-ignored-subscribe`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-ignored-subscribe.md) | Forbids the calling of `subscribe` without specifying arguments. | No |
| [`no-ignored-subscription`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-ignored-subscription.md) | Forbids ignoring the subscription returned by `subscribe`. | No |
| [`no-ignored-takewhile-value`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-ignored-takewhile-value.md) | Forbids ignoring the value within `takeWhile`. | Yes |
| [`no-implicit-any-catch`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-implicit-any-catch.md) | Like the [`no-implicit-any-catch` rule](https://github.com/typescript-eslint/typescript-eslint/pull/2202) in `@typescript-eslint/eslint-plugin`, but for the `catchError` operator instead of `catch` clauses. | Yes |
| [`no-index`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-index.md) | Forbids the importation from index modules - for the reason, see [this issue](https://github.com/ReactiveX/rxjs/issues/4230). | Yes |
| [`no-internal`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-internal.md) | Forbids the importation of internals. | Yes |
| [`no-nested-subscribe`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-nested-subscribe.md) | Forbids the calling of `subscribe` within a `subscribe` callback. | Yes |
| [`no-redundant-notify`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-redundant-notify.md) | Forbids redundant notifications from completed or errored observables. | Yes |
| [`no-sharereplay`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-sharereplay.md) | Forbids using the `shareReplay` operator. | Yes |
| [`no-subclass`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-subclass.md) | Forbids subclassing RxJS classes. | No |
| [`no-subject-unsubscribe`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-subject-unsubscribe.md) | Forbids calling the `unsubscribe` method of a subject instance. | Yes |
| [`no-subject-value`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-subject-value.md) | Forbids accessing the `value` property of a `BehaviorSubject` instance. | Yes |
| [`no-topromise`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-topromise.md) | Forbids the use of the `toPromise` method. | No |
| [`no-unbound-methods`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-unbound-methods.md) | Forbids the passing of unbound methods. | Yes |
| [`no-unsafe-catch`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-unsafe-catch.md) | Forbids unsafe `catchError` usage in effects and epics. | No |
| [`no-unsafe-first`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-unsafe-first.md) | Forbids unsafe `first`/`take` usage in effects and epics. | No |
| [`no-unsafe-subject-next`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-unsafe-subject-next.md) | Forbids unsafe optional `next` calls. | Yes |
| [`no-unsafe-switchmap`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-unsafe-switchmap.md) | Forbids unsafe `switchMap` usage in effects and epics. | No |
| [`no-unsafe-takeuntil`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/no-unsafe-takeuntil.md) | Forbids the application of operators after `takeUntil`. | Yes |
| [`prefer-observer`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/prefer-observer.md) | Forbids the passing separate callbacks to `subscribe` and `tap`. | No |
| [`suffix-subjects`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/suffix-subjects.md) | Enforces the use of a suffix in subject identifiers. | No |
| [`throw-error`](https://github.com/cartant/eslint-plugin-rxjs/blob/main/docs/rules/throw-error.md) | Enforces the passing of `Error` values to error notifications. | No |