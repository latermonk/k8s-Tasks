

# k8s-Tasks 8

https://kubernetes.io/docs/tasks





# Install Tools

## install-kubectl

### Linux install

```
sudo mv ./kubectl /usr/local/bin/kubectl

kubectl version

```

### Configuration


```
mkdir ~/.kube

touch ~/.kube/config


kubectl cluster-info

kubectl cluster-info dump

```

### Completion

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


## install-minikube

```
minikube start
```

# configure-pod-container

Assign Memory Resources to Containers and Pods

## assign-memory-resource

增加resources字段

```
resources:
      limits:
        memory: "200Mi"
      requests:
        memory: "100Mi"
    command: ["stress"]
    args: ["--vm", "1", "--vm-bytes", "150M", "--vm-hang", "1"]

```


## assign-cpu-resource


```
resources:
      limits:
        cpu: "1"
      requests:
        cpu: "0.5"
    args:
    - -cpus
    - "2"
```


# administer-cluster
## Administration with kubeadm
## manage-resources
## network-policy-provider
### Access Clusters Using the Kubernetes API


# inject-data-application
# Run-application
## Run a Stateless Application Using a Deployment

# Job
# access-application-cluster
# Monitoring, Logging, and Debugging
# Extend Kubernetes
# TLS
# Federation
# Manage Cluster Daemons
# Install Service Catalog

#  Others
## Extend kubectl with plugins
## Manage HugePages
## Schedule GPUs
