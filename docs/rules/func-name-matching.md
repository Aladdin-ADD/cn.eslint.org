---
title: func-name-matching - Rules
layout: doc_en
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# require function names to match the name of the variable or property to which they are assigned (func-name-matching)

## Rule Details

This rule requires function names to match the name of the variable or property to which they are assigned. The rule will ignore property assignments where the property name is a literal that is not a valid identifier in the ECMAScript version specified in your configuration (default ES5).

## Options

This rule takes an options object with one key, `includeCommonJSModuleExports`, and a boolean value. This option defaults to `false`, which means that `module.exports` and `module["exports"]` are ignored by this rule. If `includeCommonJSModuleExports` is set to true, `module.exports` and `module["exports"]` will be checked by this rule.

Examples of **incorrect** code for this rule:

```js
/*eslint func-name-matching: "error"*/

var foo = function bar() {};
foo = function bar() {};
obj.foo = function bar() {};
obj['foo'] = function bar() {};
var obj = {foo: function bar() {}};
({['foo']: function bar() {}});
```

```js
/*eslint func-name-matching: ["error", { "includeCommonJSModuleExports": true }]*/

module.exports = function foo(name) {};
module['exports'] = function foo(name) {};
```

Examples of **correct** code for this rule:

```js
/*eslint func-name-matching: "error"*/
/*eslint-env es6*/

var foo = function foo() {};
var foo = function() {};
var foo = () => {};
foo = function foo() {};

obj.foo = function foo() {};
obj['foo'] = function foo() {};
obj['foo//bar'] = function foo() {};
obj[foo] = function bar() {};

var obj = {foo: function foo() {}};
var obj = {[foo]: function bar() {}};
var obj = {'foo//bar': function foo() {}};
var obj = {foo: function() {}};

obj['x' + 2] = function bar(){};
var [ bar ] = [ function bar(){} ];
({[foo]: function bar() {}})

module.exports = function foo(name) {};
module['exports'] = function foo(name) {};
```

## When Not To Use It

Do not use this rule if you want to allow named functions to have different names from the variable or property to which they are assigned.

## Compatibility

* **JSCS**: [requireMatchingFunctionName](http://jscs.info/rule/requireMatchingFunctionName)

## Version

This rule was introduced in ESLint 3.8.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/func-name-matching.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/func-name-matching.md)
