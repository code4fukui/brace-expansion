# brace-expansion

sh/bashで知られるbrace expansion（ブレース展開）のJavaScript実装です。このライブラリは、Bash 4.3のbrace expansion機能を完全かつ正確に実装することを目的としています。

[
![CI](https://github.com/juliangruber/brace-expansion/actions/workflows/ci.yml/badge.svg)
](https://github.com/juliangruber/brace-expansion/actions/workflows/ci.yml)
[
![downloads](https://img.shields.io/npm/dm/brace-expansion.svg)
](https://www.npmjs.org/package/brace-expansion)

## 機能

-   **コンマ区切りリスト**: `a{b,c}d` は `abd`、`acd` に展開されます。
-   **連続範囲**:
    -   数値: `file-{1..3}.jpg` は `file-1.jpg`、`file-2.jpg`、`file-3.jpg` に展開されます。
    -   アルファベット: `file-{a..c}.jpg` は `file-a.jpg`、`file-b.jpg`、`file-c.jpg` に展開されます。
-   **ステップ付き範囲**: `{0..10..2}` は `0`、`2`、`4`、`6`、`8` に展開されます。
-   **逆順範囲**: `{c..a}` は `c`、`b`、`a` に展開されます。
-   **ゼロパディング**: `{01..03}` は `01`、`02`、`03` に展開されます。
-   **ネストされた展開**: `a{b,{c,d}}e` は `abe`、`ace`、`ade` に展開されます。
-   **空のオプション**: `a{,b}c` は `ac`、`abc` に展開されます。
-   **順序の保持**: `a{d,c,b}e` は `ade`、`ace`、`abe` に展開されます。

## 使い方と例

このモジュールは、文字列を受け取り、展開された文字列の配列を返す単一の関数をエクスポートします。

```js
import expand from "https://code4fukui.github.io/brace-expansion/index.js";

// 基本的な展開
console.log(expand('file-{a,b,c}.jpg'));
// => ['file-a.jpg', 'file-b.jpg', 'file-c.jpg']

// 連続範囲
console.log(expand('file{0..2}.jpg'));
// => ['file0.jpg', 'file1.jpg', 'file2.jpg']

// ステップ付き範囲と逆順範囲
console.log(expand('{10..0..-2}'));
// => ['10', '8', '6', '4', '2', '0']

// ネストされた展開
console.log(expand('ppp{,config,oe{,conf}}'));
// => ['ppp', 'pppconfig', 'pppoe', 'pppoeconf']

// 空のオプション
console.log(expand('-v{,,}'));
// => ['-v', '-v', 'v']

// 有効な展開が見つからない場合、元の文字列が配列に格納されて返されます。
console.log(expand('no-expansions-here'));
// => ['no-expansions-here']

// シェル変数の構文は無視されます。
console.log(expand('${a,b}'));
// => ['${a,b}']
```

## API

### `expand(pattern)`

-   **`pattern`** `<String>` 展開するパターン。
-   **戻り値:** `<Array<String>>` 展開された文字列の配列。

`pattern` の可能かつ有効なすべての展開結果を配列で返します。有効な展開が見つからない場合は、元の `pattern` 文字列を含む配列を返します。

## 貢献者

-   [Julian Gruber](https://github.com/juliangruber)
-   [Isaac Z. Schlueter](https://github.com/isaacs)

## スポンサー

このモジュールは、私の[Sponsors](https://github.com/juliangruber/sponsors)の支援を受けています！

## セキュリティの連絡先情報

セキュリティの脆弱性を報告する場合は、[Tideliftのセキュリティ連絡先](https://tidelift.com/security)をご利用ください。

## ライセンス

[MIT](LICENSE)
