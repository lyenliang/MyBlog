title: 在 Bash 腳本實現 try catch！
author: lyenliang
tags: []
categories: []
date: 2021-05-19 22:19:00
---
[try catch](https://www.eztrust.com.tw/webdesign/C/111#:~:text=try%2Dcatch%20%E5%8D%80%E5%A1%8A%E7%9A%84,%E6%89%80%E7%94%A2%E7%94%9F%E7%9A%84%E4%BE%8B%E5%A4%96%E7%8B%80%E6%B3%81%E3%80%82&text=%E6%93%B2%E5%9B%9E%E4%BE%8B%E5%A4%96%E7%8B%80%E6%B3%81%E4%B9%8B%E5%BE%8C,%E8%83%BD%E6%94%94%E6%88%AA%E8%A9%B2%E4%BE%8B%E5%A4%96%E7%8B%80%E6%B3%81%E3%80%82) 是 java 用來補捉例外狀況的語法，bash 腳本本身並不支援這種語法，但是我們可以透過特殊的方法來達到同樣的目的。

例如:

```
{ # try

    command1 &&
    command2 &&
    command3

} || { # catch
    # save log for exception 
    echo 執行異常
}
```

在上面的範例當中，當 `command1`, `command2` 發生錯誤時，後續的指令都不會執行，並會直接跳到 `echo 執行異常` 這一行。

而且當 `command1`, `command2`, `command3` 都順利執行後，`echo 執行異常` 並不會被觸發。

程式會這樣運作是因為 or 運算元（`||`）會判斷第一個括號（`{...}`）內回傳的值是不是 True，若是 True 的話，第二個括號內的指令就不會執行。

指令順利執行完並結束可以視為 True，所以第一個括號內的三個指令才需要用 and 運算元（`&&`）串接在一起，因為 True AND True AND True == True。

如果把 `&&` 刪掉的話，`command1`, `command2`, `command3` 都會執行，且如果 `command3` 執行異常的話，`echo 執行異常` 也會被觸發。