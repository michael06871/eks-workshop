---
title: "先決條件"
date: 2018-08-07T13:31:55-07:00
weight: 10
---

在這個章節中, 我們需要下載[eksctl](https://eksctl.io/)函式庫:

```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

sudo mv -v /tmp/eksctl /usr/local/bin
```

確認eksctl指令可以使用:

```bash
eksctl version
```

啟用eksctl bash-completion

```bash
eksctl completion bash >> ~/.bash_completion
. /etc/profile.d/bash_completion.sh
. ~/.bash_completion
```
