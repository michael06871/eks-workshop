---
title: "刪除EKSCTL叢集"
date: 2018-08-07T13:37:53-07:00
weight: 30
---
執行以下指令刪除EKS叢集資源:

刪除叢集:

```bash
eksctl delete cluster --name=eksworkshop-eksctl
```

{{% notice tip %}}
若是執行時沒有添加`--wait`, 這只會向叢集的CloudFormation發出刪除指令，而不等待其刪除, 在刪除EKS叢集之前，`nodegroup`將必須完成整個刪除過程。 過程大約需要花費15分鐘，可以通過[CloudFormation控制台](https://console.aws.amazon.com/cloudformation/home)查看.
{{% /notice %}}
