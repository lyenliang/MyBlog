title: '[java] Memory 管理'
author: lyenliang
tags:
  - java
categories: []
date: 2017-03-25 21:16:00
---
Java 的 Memory 主要分成 stack 及 heap 兩部份，每個 thread 都有各自對應的 stack，stack 是個 first in last out 的資料結構。每當一個 code block 結束時，他 stack 內的 variable 就會因被 pop 出來而消失；heap 的空間則由所有 thread 共享。

Java 的所有 Objects 都存放在 heap 內，`int`, `double`, `float` 等 [primitive type](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html) 的local variables 則存在 stack 裡。

當你宣告`String s = "Hello;"`時，stack 內會產生一個指向`"Hello"`物件且名稱是`s`的參數。

圖一
<img src="/images/java/stack_heap.png" alt="stack heap" style="width: 330px; "/>


garbage collection 會釋放 heap 內所有無法從 stack 指向的物件。例如有段程式碼長這樣：

    String s = "Hello";
    s = "world";

當執行到第 1 行時，stack 跟 heap 的狀態會像圖一那樣。執行第 2 行會導致 `"Hello"` 無法從 stack 內任何參數 reference 到，所以 `"Hello"` 在 garbage collection 後會被清掉。

圖二
<img src="/images/java/garbage_collection.png" alt="stack heap" style="width: 330px; "/>
