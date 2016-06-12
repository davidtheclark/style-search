# style-search [![CircleCI](https://circleci.com/gh/davidtheclark/style-search.svg?style=svg)](https://circleci.com/gh/davidtheclark/style-search)

Search CSS (and CSS-like) strings, with sensitivity to whether matches occur inside strings, comments, and functions.

## Usage

```js
var styleSearch = require('style-search');

styleSearch(options, callback);
```

By default, the search ignores strings, comments, and function names. You can use the options to change this behavior or introduce other restrictions.

### Reporting matches

For every match found your `callback` is invoked. It is passed two arguments:

- A `match` object with the following properties:
  - `startIndex`: where the match begins
  - `endIndex`: where the match ends
  - `target`: what got matched (useful if your `target` option is an array instead of a single string)
  - `insideFunctionArguments`: whether the match is inside a function — *this includes the parentheses around the arguments*
  - `insideComment`: whether the match is inside a comment
  - `insideString`: whether the match is inside a string
- The count of how many matches have been found up to this point.

### Options

#### source

String. *Required.*

The source string to search through.

#### target

String or array of strings. *Required.*

The target of the search. Can be
- a single character
- a string with some length
- an array of strings, all of which count as matches (the `match` object passed to the `callback` will differentiate which string in the array got matched via its `target` property)

#### once

Boolean. Default: `false`.

If `true`, the search will stop after one match is found.

#### comments

`"skip"` | `"check"` | `"only"`. Default: `"skip"`.

#### strings

`"skip"` | `"check"` | `"only"`. Default: `"skip"`.

#### functionNames

`"skip"` | `"check"` | `"only"`. Default: `"skip"`.

#### functionArguments

`"skip"` | `"check"` | `"only"`. Default: `"check"`.

#### parentheticals

`"skip"` | `"check"` | `"only"`. Default: `"check"`.

This designates anything inside parentheses, which includes standard functions, but also Sass maps and other non-standard constructs. `parentheticals` is a broader category than `functionArguments`.
