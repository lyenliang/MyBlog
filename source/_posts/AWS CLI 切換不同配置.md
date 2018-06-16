title: AWS CLI 切換不同配置
author: lyenliang
date: 2018-06-16 14:54:45
tags:
---

AWS CLI(command line interface) 的使用過程中，可能需要在不同的配置之間做切換，例如從 production 轉換到 development 環境。在 `~/.aws/config` 與 `~/.aws/credentials` [設定好](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)後，基本的切換方式包含

1. 在 AWS CLI 後面加上 `--profile user1` 即可使用 `user1` profile。
例如
```
$ aws s3 ls --profile user1
2018-06-11 20:45:20 test-bucket
```
2. 設定 `AWS_DEFAULT_PROFILE`，例如 `export AWS_DEFAULT_PROFILE=user_name`。設定好了 AWS CLI 就會使用該帳號。

上述方法切換前，都需要改動 [Bash Profile](https://superuser.com/questions/426114/understanding-bashrc-and-bash-profile)，實在不方便，底下有較便捷的方式:

1. **使用 alias**:
   
   例如設定 `alias aws1='aws --profile user1'` 與 `alis aws2='aws --profile user2'`，這樣一來，以後輸入 `aws1 s3 ls` 就會看到 `user1` 的 s3 bucket，`aws2 s3 ls` 會看到 `user2` 的。
   
2. **改用 [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) 並搭配 [AWS plugin](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins#aws)**

   裝好後可以用 `asp` 與 `agp` 來切換與顯示 AWS CLI 配置。
   




參考資料: 
* [AWS CLI Getting Started](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)
* [oh-my-zsh plugin#aws](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins#aws)
* [How to use multiple AWS Accounts from the command line?
](https://stackoverflow.com/questions/593334/how-to-use-multiple-aws-accounts-from-the-command-line)