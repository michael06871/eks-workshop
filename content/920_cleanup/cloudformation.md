---
title: "清除CloudFormation叢集"
date: 2018-08-07T12:37:34-07:00
weight: 10
draft: true
---
清除您在這次的workshop在AWS account上所使用的資源
執行以下指令:

移除EKS上的Worker節點:
```
aws cloudformation delete-stack --stack-name "eksworkshop-cf-worker-nodes"
```
刪除EKS叢集:
```
aws eks delete-cluster --name "eksworkshop-cf"
```
移除叢集VPC之前先確認叢集已經被刪除
Confirm the Cluster is deleted before removing Cluster VPC:
```
aws eks describe-cluster --name eksworkshop-cf --query "cluster.status"
```
刪除叢集VPC:
```
aws cloudformation delete-stack --stack-name "eksworkshop-cf"
```
解除IAM角色政策:
```
aws iam detach-role-policy --role-name "eks-service-role-workshop" --policy-arn "arn:aws:iam::aws:policy/AmazonEKSClusterPolicy"
aws iam detach-role-policy --role-name "eks-service-role-workshop" --policy-arn "arn:aws:iam::aws:policy/AmazonEKSServicePolicy"
```
移除建立EKS叢集的IAM角色:
```
aws iam delete-role --role-name "eks-service-role-workshop"
```
