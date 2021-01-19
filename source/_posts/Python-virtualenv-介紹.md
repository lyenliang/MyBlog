title: Python virtualenv 介紹
author: lyenliang
tags:
  - python
categories: []
date: 2021-01-19 21:37:00
---
#### 問題描述

有時候我們在用 python 開發專案時，可能 A 專案需要 C 模組的 1.0 版，B 專案要 C 模組的 2.0 版，如果你要在 A、B 專案之間切換就會非常不方便。

當然你可以在開發 A 專案時，把 C 模組 2.0 版刪掉，然後改裝 1.0 版，等要處理 B 專案時，再把 C 模組升級到 2.0 版，不過這樣操作太過麻煩。

[virtualenv](https://virtualenv.pypa.io/en/latest/) 的誕生就是為了解決這個問題。

#### 安裝方式

virtualenv 可透過 `pip` 安裝，輸入 `pip install virtualenv` 就能安裝，其它安裝方法可參考 [virtualenv installation](https://virtualenv.pypa.io/en/latest/installation.html)。

#### 使用方式

首先切換到打算建立 python 環境的目錄，並輸入 `virtualenv <env_name>`，例如我想建名叫 `myenv` 的 python 環境，我可以輸入 `virtualenv myenv`，輸入完就會產生 `myenv/` 資料夾，這時可以用 `source myenv/bin/activate` 來啟動環境。

啟動後你可以用 [`pip freeze`](https://pip.pypa.io/en/stable/reference/pip_freeze/) 來確認是不是真的沒有任何已裝好的 python 模組，因為全新的環境不應該有任何已安裝的模組。