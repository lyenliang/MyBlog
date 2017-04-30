title: Jenkins Plugin 從無到有
author: lyenliang
tags:
  - jenkins
categories: []
date: 2017-04-30 14:01:00
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

打開 [source code](https://github.com/jenkinsci/console-tail-plugin) 發現它顯示資訊的頁面叫 `floatingBox.jelly`，根據這個線索我又 google 到 [Action](http://javadoc.jenkins-ci.org/hudson/model/Action.html)，Action 的頁面提到 `If an action has a view named floatingBox.jelly, it will be displayed as a floating box on the top page of the target ModelObject.`，於是就確定 Action + floatingBox 可以在某個頁面上顯示浮動視窗。

`Console Tail Plugin` 只有在 build 失敗時會顯示資訊，照理說我只要做些修改就可以變成我想要的功能。於是我便動手改改看，之後看到 [ConsoleTailProjectAction.java](https://github.com/jenkinsci/console-tail-plugin/blob/master/src/main/java/jenkins/plugins/consoletail/ConsoleTailProjectAction.java) 裡唯一跟 build 結果有關的只有這段

    return Result.UNSTABLE.isBetterOrEqualTo(build.getResult()) ? build : null;
    
這段意思看起來是如果 `UNSTABLE` 這個 build 結果比最近一次 build 結果要好的話，就回傳 build ，否則回傳 `null`，於是我把這行改成 `return build;` 試試看，結果真的順利顯示最後一次 build 結果到 project 頁面上。

到這邊我發現我已做出當初想要的功能，不過我也知道 code 還有很多地方還沒深入了解，感覺這是個會有很多 bug 的產品，而且 console tail plugin 有些程式碼是我不需要的，可以刪除，總之還有地方需要修改就是了。

待續…