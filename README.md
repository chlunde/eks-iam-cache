# Archived

Use https://github.com/kubernetes-sigs/aws-iam-authenticator directly instead

# AWS EKS kubectl credential cache

## Install
```bash
go install github.com/chlunde/eks-iam-cache@main
```

## Configure `~/.kube/config`
```bash
sed -i 's/command: aws/command: eks-iam-cache/' ~/.kube/config
```
or edit `$KUBECONFIG`:

```yaml
apiVersion: v1
kind: Config
users:
- name: arn:aws:eks:eu-north-1:...:cluster/foo
  user:
    exec:
      apiVersion: client.authentication.k8s.io/v1alpha1
      command: aws
      args:
      - --region
      - eu-north-1
      - eks
      - get-token
      - --cluster-name
      - ...
      env:
      - name: AWS_PROFILE
        value: ...
```
replace `aws` in `command:` with `eks-iam-cache`:

```yaml
      command: eks-iam-cache
```
