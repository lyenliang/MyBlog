title: AWS Lambda Layer
author: lyenliang
tags:
  - AWS
categories: []
date: 2019-10-01 18:03:00
---
#### 問題介紹

[AWS Lambda](https://aws.amazon.com/tw/lambda/) 是一套 Serveless 服務，讓使用者不必花太多時間佈建或管理伺服器，同時得到更多時間編寫核心邏輯。

不過 AWS Lambda 也有些小缺點，例如當 code 與用到的 libraries [超過 3MB](https://docs.aws.amazon.com/lambda/latest/dg/limits.html#limits-list) 時，你會被告知 deployment package too large

![upload successful](/images/pasted-2.png)

雖然這不影響 function 的運行，但會讓人不方便編輯與查看 lambda function 內容。


#### 解決方法

為了解決這項問題，AWS 在 [2018 年推出 Lambda Layers](https://aws.amazon.com/tw/blogs/aws/new-for-aws-lambda-use-any-programming-language-and-share-common-components/) 來存放 function 之間共用的 libraries。

#### 實際舉例

以下拿 python3 的 Lambda Function 當例子:

假設有個 python 程式需要 `PyMySQL`、`PyYAML`、`openpyxl` 三個 Libraries。


##### 使用 Layer 前

在不使用 layer 的情況下，你需要建立一個 `requirements.txt`，並在裡面寫上 Libraries 與對應的版本。

![upload successful](/images/pasted-3.png)

然後用 `pip install --requirement requirements.txt` 安裝 Libraries。裝好後你會發現資料夾裡多了好多不是自己寫的檔案:

![upload successful](/images/pasted-5.png)

由於這些 libraries 跟你寫的 code 在同一個資料夾層級，它們會阻礙你閱讀 code，而且當它們超過 3MB 時，無法在 AWS Lambda 線上編輯器顯示。

##### 使用 Layer 後

當你打算採用 layer 時，你需要將 Libraries 打包到名為 `python` 的資料夾內

```
pip install \
  --requirement requirements.txt \
  --target python
```

然後用 `zip -r lambdaLayer.zip python` 將它打包再上傳。

以下介紹透過 AWS Console 上傳的方式

首先進入 AWS Lambda Function Layers 頁面，並點選 `Create Layer`

![upload successful](/images/pasted-8.png)


上傳剛剛打包好的 zip 檔

![upload successful](/images/pasted-9.png)

上傳好你會得到一串資源識別碼 (ARN, Amazon Resource Name)，記下它，因為等一下會用到

![upload successful](/images/pasted-10.png)

這時再回到你想加入 Layer 的 lambda function，然後點選 `Layers`。注意 Layers 右邊有個 `(0)`，它表示現在有的 Layer 數是 0。

![upload successful](/images/pasted-11.png)

然後再點選 `Add a layer`

![upload successful](/images/pasted-12.png)

再來選 `Provide a layer version ARN`，並貼上剛剛記下的 ARN

![upload successful](/images/pasted-13.png)

這時 Layer 就快建立完成了，最後只要按下 `Save` 就能儲存 Layer，注意這時 `Layers` 右邊的數字變成 1，表示有一個 Layer。

![upload successful](/images/pasted-14.png)


#### 結果比較

從上面的例子可以發現使用 Layer 後，編輯器裡只會留下你自己編寫的檔案

![uploaded!](/images/pasted-17.png)

這樣不僅方便看 code，也可以在 AWS Lambda 線上編輯器直接修改 code 。