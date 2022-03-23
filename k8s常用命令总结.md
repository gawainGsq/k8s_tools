### k8s常用命令总结

1、k8s补全

```
yum install bash-completion -y 
source <(kubectl completion bash)
echo "source <(kubectl completion bash)" >> ~/.bashrc
source /usr/share/bash-completion/bash_completion
echo 'alias k=kubectl' >>~/.bashrc
echo 'complete -F __start_kubectl k' >>~/.bashrc
source  ~/.bashrc
k get pod -n kube-system 
```

2、获取k8s token

```
kubectl create sa management-admin -n kube-system 2>/dev/null
kubectl create clusterrolebinding management-admin --clusterrole=cluster-admin --serviceaccount=kube-system:management-admin 2>/dev/null
key=$(kubectl get sa management-admin -o=custom-columns=:.secrets[0].name -n kube-system | grep 'management')
token=$(kubectl -n kube-system get secret ${key} -o yaml | grep token: | awk '{print $2}' | base64 -d)
echo $token
```

