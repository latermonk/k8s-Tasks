

# k8s-Tasks 8

https://kubernetes.io/docs/tasks


https://kubernetes.io/docs/tasks





## <a name='InstallTools'></a>1.1. Install Tools
## <a name='install-kubectl'></a>1.2. install-kubectl

### <a name='Linuxinstall'></a>1.2.1. Linux install

```
sudo mv ./kubectl /usr/local/bin/kubectl

kubectl version

```

### <a name='Configuration'></a>1.2.2. Configuration


```
mkdir ~/.kube

touch ~/.kube/config


kubectl cluster-info

kubectl cluster-info dump

```


### <a name='Completion'></a>1.2.3. Completion

```
1. install bash-completion

apt install bash-completion


2. install kubectl completion

source <(kubectl completion bash)

或者 

echo "source <(kubectl completion bash)" >> ~/.bashrc

3.alias k as kubectl

alias k=kubectl
complete -F __start_kubectl k


```



## <a name='install-minikube'></a>1.3. install-minikube

```
minikube start
```

## <a name='configure-pod-container'></a>1.4. configure-pod-container



