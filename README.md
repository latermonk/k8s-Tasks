# 1. k8s-Tasks

https://kubernetes.io/docs/tasks


https://kubernetes.io/docs/tasks


<!-- TOC -->autoauto- [1. k8s-Tasks](#1-k8s-tasks)auto    - [1.1. Install Tools](#11-install-tools)auto    - [1.2. install-kubectl](#12-install-kubectl)auto        - [1.2.1. Linux install](#121-linux-install)auto        - [1.2.2. Configuration](#122-configuration)auto        - [1.2.3. Completion](#123-completion)auto    - [1.3. install-minikube](#13-install-minikube)auto    - [1.4. configure-pod-container](#14-configure-pod-container)autoauto<!-- /TOC -->


## 1.1. Install Tools
## 1.2. install-kubectl

### 1.2.1. Linux install

```
sudo mv ./kubectl /usr/local/bin/kubectl

kubectl version

```

### 1.2.2. Configuration


```
mkdir ~/.kube

touch ~/.kube/config


kubectl cluster-info

kubectl cluster-info dump

```


### 1.2.3. Completion

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



## 1.3. install-minikube

```
minikube start
```

## 1.4. configure-pod-container



