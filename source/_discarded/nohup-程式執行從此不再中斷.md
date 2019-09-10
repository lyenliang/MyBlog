title: nohup - 程式執行從此不中斷
author: lyenliang
tags:
  - linux
categories: []
date: 2019-09-10 20:21:00
---
對於遠端 ssh 登入 Linux 的使用者來說，若遇到程式需要跑很久的情況（例如 `scp` 傳輸大檔案），通常只能乖乖等它執行完，若跑到一半不幸連線中斷，程式只能重跑一次，造成大量的時間被浪費。

幸好 Linux 有提供 [`nohup`](https://en.wikipedia.org/wiki/Nohup) 指令讓我們可以在 ssh 連線登出後，程式照樣能繼續執行。

一般 Linux 使用者登出後，他執行的所有程式都會收到 [SIGHUP](https://en.wikipedia.org/wiki/SIGHUP) （SIGnup Hang UP）訊號，正常程式收到 SIGHUP 就會立刻停止執行。

`nohup` （字面意思 No Hang Up）可以讓程式忽略 `SIGHUP`，所以當使用者斷線或登出時，程式可以繼續執行，不會受到影響。

## 使用方法

假設原本你想用 `scp /path/to/my/file brian@123.123.123.123:/home/brian` 將一個大檔案複製到遠端機器，你可以將指令改成 `nohup scp /path/to/my/file brian@123.123.123.123:/home/brian &` 來執行，指令尾端的 `&` 代表`nohup` 會在背景，避免卡住你現在執行的 ssh 視窗。

## 觀察輸出結果

既然有程式在執行，那麼你一定會想看執行的結果。 `nohup` 預設會將所有的輸出資訊寫到 `nohup.txt` 這個檔案，你可以用 `cat nohup.txt` 查看程式輸出資訊，或是用 `tail -f nohup.txt` 即時查看最後輸出的幾筆資料。