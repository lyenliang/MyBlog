title: 使用 pipreqs 快速產生 python 套件紀錄檔 (requirements.txt)
author: lyenliang
date: 2023-03-12 20:39:51
tags:
---
在使用 Python 開發專案時，有時需要許多第三方套件來更快速地完成開發工作。

這些套件可能會有各種不同的版本，而在不同的機器上可能會有不同的套件版本安裝。為了確保在不同機器上的程式運作一致，我們需要一份清單來確保所有的套件都是相同的版本。這時候就需要 requirements.txt 這個檔案來記錄第三方套件與對應的版本。

[pipreqs](https://pypi.org/project/pipreqs/) 則是一個非常方便的工具，可以幫助我們自動產生 requirements.txt。

### 什麼是 requirements.txt？
在開發 Python 專案時，我們會使用許多 Python 套件來協助我們完成任務。當我們需要分享這個專案給其他人時，他們需要安裝相同的套件才能夠運行程式。使用 requirements.txt，我們可以輕鬆地將專案所需的套件清單分享給其他人，讓他們可以快速且方便地安裝所需的套件。此外，requirements.txt 也可以用來管理專案所需的套件版本，以確保專案的穩定性和一致性。

### 用 pipreqs 與 pip freeze 產生 requirements.txt 的差異
在產生 requirements.txt 時，我們可以使用 `pip freeze > requirements.txt` 指令產生。這個指令可以讓我們輕鬆地產生一個包含專案所需套件清單的文字檔。不過這個指會將環境中所有套件都列出來，包含基本且不需要額外手動安裝的套件。

而 pipreqs 是一個更加方便的工具。pipreqs 可以自動掃描專案所需的套件並產生 requirements.txt。此外，pipreqs 可以排除不必要的套件，只列出專案所需的套件清單，讓 requirements.txt 更加精簡。當我們新增或刪除套件時，只需要重新執行 pipreqs 即可更新 requirements.txt，方便快速。

### pipreqs 的安裝與使用方式

我們可以使用底下的指令安裝 pipreqs：
```
pip install pipreqs
```

安裝完成後，我們可以進入專案的根目錄，並執行以下指令來產生 requirements.txt：

```
pipreqs .
```

其中的「.」代表專案的根目錄。這個指令會自動掃描專案所需的套件並產生 requirements.txt 檔案。預設情況下，requirements.txt 檔案會儲存在專案的根目錄下。如果要儲存到不同的目錄下，可以加上 -p 或 --savepath 參數，例如：

```
pipreqs . --savepath /path/to/requirements.txt
```

整體來說，pipreqs 是一個非常方便快速的工具，可以自動掃描專案所需的套件並產生 requirements.txt 檔案，讓專案的套件管理更加便利。如果你正在開發 Python 專案，不妨試試使用 pipreqs 來產生 requirements.txt 檔案吧！