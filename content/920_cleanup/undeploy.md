---
title: "清除部署的應用程式"
date: 2018-08-07T13:37:53-07:00
weight: 20
---

在刪除應用程式創建的資源之前, 我們應該刪除應用程式部署任務和kubernetes儀表板。

請注意, 如果您遵循章節內的清除步驟, 執行某些命令可能會失敗, 因為沒有內容要刪除, 也沒問題

清除部署的應用程式:

```bash
cd ~/environment/ecsdemo-frontend
kubectl delete -f kubernetes/service.yaml
kubectl delete -f kubernetes/deployment.yaml

cd ~/environment/ecsdemo-crystal
kubectl delete -f kubernetes/service.yaml
kubectl delete -f kubernetes/deployment.yaml

cd ~/environment/ecsdemo-nodejs
kubectl delete -f kubernetes/service.yaml
kubectl delete -f kubernetes/deployment.yaml

export DASHBOARD_VERSION="v2.0.0"

kubectl delete -f https://raw.githubusercontent.com/kubernetes/dashboard/${DASHBOARD_VERSION}/src/deploy/recommended/kubernetes-dashboard.yaml
```
