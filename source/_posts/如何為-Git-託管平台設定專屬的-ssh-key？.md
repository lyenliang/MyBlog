title: 如何為 Git 託管平台設定專屬的 ssh key？
author: lyenliang
date: 2022-09-03 14:02:30
tags:
---
市面上熱門的 Git 託管平台有很多種，像是 `gitlab.com`, `github.com`, `bitbucket.org` … 等等。

平常透過 ssh 來 clone 時，預設都是用 ~/.ssh/id_rsa 這把 key 來下載資料。

假如我們想要在不同的 Git 託管平台用不同 key 下載的話，可以透過修改 ~/.ssh/config 來達成，例如這樣設定：

```
bash
Host mygithub
    HostName github.com
    User my_github_account
    IdentityFile ~/.ssh/my_github_public_key.pem

Host mygitlab
    HostName gitlab.com
    User my_gitlab_account
    IdentityFile ~/.ssh/my_gitlab_public_key.pem
```

上面這個範圍代表我們要用 `~/.ssh/my_github_public_key.pem` 這把 key 來上傳/下載 `github.com` 的資料，用 `~/.ssh/my_gitlab_public_key.pem` key 來上傳/下載的資料。

`~/.ssh/config` 還有其它選項可以用，完整的列表可以參考 [SSH config file for OpenSSH client]([https://www.ssh.com/academy/ssh/config](https://www.ssh.com/academy/ssh/config)) 。