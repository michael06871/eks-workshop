---
title: "建立 EKS"
date: 2018-08-07T13:34:24-07:00
weight: 20
---


{{% notice warning %}}
**請確認** 在這個步驟 除非你已經在Cloud9 IDE有使用[已驗證的IAM角色](/020_prerequisites/workspaceiam/#validate-the-iam-role). 否則您將無法在之後的章節中運行必要的kubectl命令。
{{% /notice %}}

#### 挑戰:

**如何在workspace確認IAM角色?**

{{%expand "點選展開解決方案" %}}
執行 `aws sts get-caller-identity` 驗證你的_Arn_是否包含 `eksworkshop-admin`和實例ID.

```output
{
    "Account": "123456789012",
    "UserId": "AROA1SAMPLEAWSIAMROLE:i-01234567890abcdef",
    "Arn": "arn:aws:sts::123456789012:assumed-role/eksworkshop-admin/i-01234567890abcdef"
}
```

如果您沒有找到正確的角色, 請回去檢查您[已驗證的角色](/020_prerequisites/workspaceiam/#validate-the-iam-role) 解決此問題.

如果您有看到正確的角色, 請繼續執行下一個步驟, 建立EKS叢集
{{% /expand %}}

### 建立一個EKS叢集

{{% notice warning %}}
`eksctl` 版本必須要高於0.24.0才能去部署EKS 1.17, [點選這裏](/030_eksctl/prerequisites) 取得最新版本.
{{% /notice %}}

建立一個eksctl部署檔案(eksworkshop.yaml) 使用以下內容建立您的叢集:

```bash
cat << EOF > eksworkshop.yaml
---
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: eksworkshop-eksctl
  region: ${AWS_REGION}
  version: "1.17"

availabilityZones: ["${AWS_REGION}a", "${AWS_REGION}b", "${AWS_REGION}c"]

managedNodeGroups:
- name: nodegroup
  desiredCapacity: 3
  ssh:
    allow: true
    publicKeyName: eksworkshop

# To enable all of the control plane logs, uncomment below:
# cloudWatch:
#  clusterLogging:
#    enableTypes: ["*"]

secretsEncryption:
  keyARN: ${MASTER_ARN}
EOF
```

接下來, 使用這個檔案來建立eksctl叢集

```bash
eksctl create cluster -f eksworkshop.yaml
```

{{% notice info %}}
建立EKS與其他相關檔案大約會花費15分鐘左右
{{% /notice %}}
