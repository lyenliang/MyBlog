title: 用 ChatGPT 玩 Binance WOTD！
author: lyenliang
tags:
  - ChatGPT
  - Binance WOTD
categories: []
date: 2023-04-26 19:30:00
---
### 什麼是 Binance WOTD ###

Binance WOTD (Word Of The Day)是幣安推出的一款猜字小遊戲，讓玩家有機會贏得 Binance 平台上的獎勵。這個遊戲的目標是要玩家在一定次數內猜出與加密貨幣相關的英文單字。本文將介紹如何使用 ChatGPT 來找出 Binance WOTD 的答案。

![Binance WOTD Rules!](/images/pasted-20.png)


### 如何進入 Binance WOTD 頁面？ ###

首先進入幣安 App 的首頁，點選「更多」

![More button!](/images/pasted-18.png)

然後就可以看到 WOTD 按鈕


![WOTD!](/images/pasted-19.png)

### 如何讓 ChatGPT (GPT-4) 幫我們猜 WOTD 單字？ ###


首先讓我們跟 ChatGPT 介紹 WOTD 的遊戲規則，並讓它扮演猜字的玩家，我們則扮演 Binance WOTD 的遊戲，底下我是跟 ChatGPT 介紹的說明文字。

```
我們來玩猜 Binance Word of The Day (Binance WODL) 遊戲，這個遊戲最終目的是要猜一個跟 cryto currency 有關的英文單字，遊戲流程如下：
1. 我會跟你說這個英文單字由幾個字母構成，英文字的大小寫沒有區別
2. 你開始猜英文單字
3. 當你猜的字母完全沒有出現在英文單字裡面時，我會用 0 來標示；
   當你猜的字母有出現在英文單字裡，但位置不對時，我會用 1 來標示；
   當你猜的字母有出現在英文單字裡，且位置也對時，我會用 2 來標示；
   例如我要你猜的英文單字是 VOTING，而你猜 ACTION 時，我會回應
   A 0
   C 0
   T 2
   I 2
   O 1
   N 1
4. 重複 2 跟 3 的步驟，直到你猜中為止

這個英文單字由 6 個字母組成，請你開始猜
```
ChatGPT 聽懂後，它回

```
好的，我明白遊戲規則了。我猜的第一個單詞是：MINERS。
```

這時我只要把它猜的單字輸入到 WOTD 遊戲上，就可以看到哪些字有猜中。

根據 WOTD 遊戲回覆的訊息，我告訴 ChatGPT 

```
M 0
I 0
N 0
E 0
R 1
S 0
```
此時 ChatGPT 回覆「謝謝提示。我猜的第二個單詞是：WALLET。」

但由於 `E` 已經確定沒有出在要猜的單字裡，所以我跟它說「E 已經確認沒出現過了，請不要猜 WALLET」

ChatGPT 再回「抱歉，我犯了一個錯誤。讓我重新猜一個單詞：TRADER。」

這時我們可以發現它一樣沒有注意到猜的字裡面有 `E`。

![Conversation!](/images/pasted-21.png)

經過多次的提醒後，我發現 ChatGPT 似乎不會記得哪些字母該出現，哪些字母不該出現，最後我告訴它「請你猜的單字第三個字母一定要是 O，字母裡不可以有 M, I, N E, S, B, L, C, K, Y, V，且長度必須是 6 個字母」，它才精準的回出正確答案。

![final answer!](/images/pasted-22.png)

最後我在 ChatGPT 的協助下順利猜中這次的單字

![WTOD answer!](/images/pasted-23.png)
