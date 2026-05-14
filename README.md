# brace-expansion

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

Brace expansion, as known from sh/bash, in JavaScript. This library aims to be a complete and accurate implementation of Bash 4.3's brace expansion features.

[
![CI](https://github.com/juliangruber/brace-expansion/actions/workflows/ci.yml/badge.svg)
](https://github.com/juliangruber/brace-expansion/actions/workflows/ci.yml)
[
![downloads](https://img.shields.io/npm/dm/brace-expansion.svg)
](https://www.npmjs.org/package/brace-expansion)

## Features

-   **Comma-Separated Lists**: `a{b,c}d` expands to `abd`, `acd`.
-   **Sequential Ranges**:
    -   Numeric: `file-{1..3}.jpg` expands to `file-1.jpg`, `file-2.jpg`, `file-3.jpg`.
    -   Alphabetic: `file-{a..c}.jpg` expands to `file-a.jpg`, `file-b.jpg`, `file-c.jpg`.
-   **Stepped Ranges**: `{0..10..2}` expands to `0`, `2`, `4`, `6`, `8`.
-   **Reversed Ranges**: `{c..a}` expands to `c`, `b`, `a`.
-   **Zero-Padding**: `{01..03}` expands to `01`, `02`, `03`.
-   **Nested Expansions**: `a{b,{c,d}}e` expands to `abe`, `ace`, `ade`.
-   **Empty Options**: `a{,b}c` expands to `ac`, `abc`.
-   **Order Preservation**: `a{d,c,b}e` expands to `ade`, `ace`, `abe`.

## Usage & Examples

The module exports a single function that takes a string and returns an array of expanded strings.

```js
import expand from "https://code4fukui.github.io/brace-expansion/index.js";

// Basic expansion
console.log(expand('file-{a,b,c}.jpg'));
// => ['file-a.jpg', 'file-b.jpg', 'file-c.jpg']

// Sequential ranges
console.log(expand('file{0..2}.jpg'));
// => ['file0.jpg', 'file1.jpg', 'file2.jpg']

// Stepped and reversed ranges
console.log(expand('{10..0..-2}'));
// => ['10', '8', '6', '4', '2', '0']

// Nested expansions
console.log(expand('ppp{,config,oe{,conf}}'));
// => ['ppp', 'pppconfig', 'pppoe', 'pppoeconf']

// Empty options
console.log(expand('-v{,,}'));
// => ['-v', '-v', 'v']

// If no valid expansions are found, the original string is returned in an array.
console.log(expand('no-expansions-here'));
// => ['no-expansions-here']

// Shell variable syntax is ignored.
console.log(expand('${a,b}'));
// => ['${a,b}']
```

## API

### `expand(pattern)`

-   **`pattern`** `<String>` The pattern to expand.
-   **Returns:** `<Array<String>>` An array of expanded strings.

Returns an array of all possible and valid expansions of `pattern`. If no valid expansions are found, it returns an array containing the original `pattern` string.

## Contributors

-   [Julian Gruber](https://github.com/juliangruber)
-   [Isaac Z. Schlueter](https://github.com/isaacs)

## Sponsors

This module is proudly supported by my [Sponsors](https://github.com/juliangruber/sponsors)!

## Security contact information

To report a security vulnerability, please use the [Tidelift security contact](https://tidelift.com/security).

## License

[MIT](LICENSE)