title: Jenkins Plugin 從無到有
author: lyenliang
date: 2017-04-30 14:28:40
tags:
---
之前用 [jenkins](https://jenkins.io/) 經常會希望 console output 可以直接顯示在 project 頁面上，因為這樣可以比較快看到 build 結果。

像這樣：
<img src="/images/jenkins/display_console_output.png" alt="stack heap" style="width: 730px; "/>

無奈使終找不到有這種功能的 plugin，[stackoverflow](http://stackoverflow.com/questions/9496888/jenkins-display-last-console-output-on-project-page/43169372) 有人提到其它方式讓你比較快可以看到 console output，不過還是覺得不太方便。

於是我就想到自己動手開發 plugin：

先是安裝 [plugin tutorial](https://wiki.jenkins-ci.org/display/JENKINS/Plugin+tutorial) 提到的工具，然後再建個 hello world plugin。

等到對 plugin 長什麼樣比較有概念後，再來想到的問題是怎麼在 project 頁面加視窗。我想說 Jenkins Plugin 已經有一千多個，總該可以找到現成的範例才對，於是便到 Plugin Manager 搜尋 `console` 關鍵字，看看有沒有 plugin 會把資訊顯示在 project 頁面。

<img src="/images/jenkins/search_console.png" alt="stack heap" style="width: 730px; "/>

最後發現 `Console Tail Plugin` 跟我想要實現的功能非常接近。

<img src="/images/jenkins/console_tail.png" alt="stack heap" style="width: 730px; "/>

