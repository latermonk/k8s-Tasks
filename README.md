<!-- vscode-markdown-toc -->
* 1. [1.1. Install Tools](#InstallTools)
* 2. [1.2. install-kubectl](#install-kubectl)
	* 2.1. [1.2.1. Linux install](#Linuxinstall)
	* 2.2. [1.2.2. Configuration](#Configuration)
	* 2.3. [1.2.3. Completion](#Completion)
* 3. [1.3. install-minikube](#install-minikube)
* 4. [1.4. configure-pod-container](#configure-pod-container)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

# 1. k8s-Tasks

https://kubernetes.io/docs/tasks


https://kubernetes.io/docs/tasks





##  1. <a name='InstallTools'></a>1.1. Install Tools
##  2. <a name='install-kubectl'></a>1.2. install-kubectl

###  2.1. <a name='Linuxinstall'></a>1.2.1. Linux install

```
sudo mv ./kubectl /usr/local/bin/kubectl

kubectl version

```

###  2.2. <a name='Configuration'></a>1.2.2. Configuration


```
mkdir ~/.kube

touch ~/.kube/config


kubectl cluster-info

kubectl cluster-info dump

```


###  2.3. <a name='Completion'></a>1.2.3. Completion

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



##  3. <a name='install-minikube'></a>1.3. install-minikube

```
minikube start
```

##  4. <a name='configure-pod-container'></a>1.4. configure-pod-container



