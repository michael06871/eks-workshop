---
title: "測試你的叢集"
date: 2018-08-07T13:36:57-07:00
weight: 30
---
#### 測試你的叢集:
確認你的節點:

```bash
kubectl get nodes # if we see our 3 nodes, we know we have authenticated correctly
```

#### 設定這個workshop中的Worker Role Name:

```bash
STACK_NAME=$(eksctl get nodegroup --cluster eksworkshop-eksctl -o json | jq -r '.[].StackName')
ROLE_NAME=$(aws cloudformation describe-stack-resources --stack-name $STACK_NAME | jq -r '.StackResources[] | select(.ResourceType=="AWS::IAM::Role") | .PhysicalResourceId')
echo "export ROLE_NAME=${ROLE_NAME}" | tee -a ~/.bash_profile
```

#### 恭喜您!

您現在有了一個完整運作的Amazon EKS Cluster!
