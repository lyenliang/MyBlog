title: '[javascript] 運算子執行順序(operator associativiy)與強制轉型(coercion)'
author: John Doe
date: 2017-02-13 21:52:46
tags:
---
無意間發現`console.log( 3 > 2 > 1 );`回傳值是 `false`，讓我感到有些奇怪，因為 3 比 2 大也比 1 大，而且 2 比 1 大也是正確的，照理講應該回傳`true`才合理。但仔細想想後才意識到`3 > 2 > 1`應該要拆開來看能知道當中發生什麼事情：

首先，由於`>`運算子的[執行順序(operator associativity)](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)是從左到右，所以我們必須先觀察`3 > 2`的算運結果：

打開 node.js 來試試：

    > 3 > 2
    true

由於`3 > 2`是正確的，所以我們不意外地得到 `true`，接下來最需要注意的地方在 javascript 會比較 `true` 及 `1`，那麼`ture > 1`會是什麼結果呢？

    > true > 1
    false

實測結果發現是 `false`。這是由於執行 `>`運算時，兩個運算子`true`、`1`都會被強制轉型成 boolean，因為在 javascript 當中，只有 0 轉成 boolean 會是 `false`，其它數字強制轉型後都會是 `true`，所以原本的 `true > 1`可以視為 `true > true`。兩個`true`應該要相等，不可能其中一個 `true` 大於另一個 `true`，所以`true > 1`自然會回傳 `fasle`，這就是為什麼`console.log( 3 > 2 > 1 );`最後會得到 `false`。

最後做個總整理：

`3 > 2 > 1` 相當於 `true > 1` 相當於 `true > true` 相當於 `false`。
