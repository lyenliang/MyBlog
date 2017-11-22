title: '[Google 試算表] 如何找出重複資料'
author: lyenliang
tags:
  - excel
categories: []
date: 2017-11-11 21:27:00
---
Google 試算表是款相當方便的工具，其中有一項的功能就是比對兩筆資料的交集。

假設有 A 與 B 兩筆資料

<img src="/images/excel/A_B_columns.png" alt="A and B Columns" style="width: 330px; "/>

用以下方法可以找出兩欄重複的英文字母:

首先在第 3 欄輸入 [`=COUNTIF`](https://support.google.com/docs/answer/3093480?hl=zh-Hant)
，這是試算表內建的函式，用它能夠知道指定範圍內含有的資料筆數。

例如 `COUNTIF(A:A,B2)` 會回傳 A 欄裡有多少 B2 格子內的值

由於 B2 的值是 `b`，而且 A 欄裡只有 1 個 `b`，所以得到 1。

<img src="/images/excel/countif_values.png" alt="A and B Columns" style="width: 390px; "/>

接下來在 C3 ~ C8 都套用這個函式:

對著 C2 格子的右下角按按滑鼠左鍵不放，然後往下拖到 C8 位置，這樣就可以讓 C3 ~ C8 都套用 `COUNTIF(A:A,BX)` 函式。

<img src="http://g.recordit.co/zCEt4yPI4I.gif" alt="A and B Columns Drag and Drop" style="width: 390px; " />

執行後會發現 B 欄內 `b`、`g`、`f` 三筆資料都回傳 1，其它資料回傳 0，這表示 `b`、`g`、`f` 是 A、B 兩欄交集的資料。

接下來的問題是如何將交集資料（`b`、`g`、`f`）集中在一起。這三筆資料分散在 B 欄的不同列裡面，資料少的時候還可以一筆一筆手動把它們挑出來，如果今天交集的資料有上百筆的話，一筆一筆的挑出肯定會花費不少時間，所以必須要有方法能快速整理出交集的資料。

這邊會利用排序功能將交集資料排在一起：

<img src="/images/excel/sort.png" alt="Sort" style="width: 350px; "/>

排序後可以發現 `b`、`g`、`f` 被集中在一起。

<img src="/images/excel/intersection.png" alt="Sort" style="width: 390px; "/>

這樣我們就順利地將 A 欄與 B 欄共同擁有的資料整理出來了。