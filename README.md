# Again

# Test Env


https://www.katacoda.com/courses/kubernetes   

https://instruqt.com/public/topics/getting-started-with-kubernetes   






#  kubectl sheet
[https://kubectl.docs.kubernetes.io/](https://kubectl.docs.kubernetes.io/)

# k8s-Tasks 8

https://kubernetes.io/docs/tasks







#  Cluster  setup   

https://github.com/latermonk/kubernetes-the-hard-way-vagrant    



```

$ kubectl run nginx --image=nginx   (deployment)

$ kubectl run nginx --image=nginx --restart=Never   (pod)

$ kubectl run busybox --image=busybox --restart=OnFailure   (job)

$ kubectl run busybox --image=busybox --schedule="* * * * *"  --restart=OnFailure (cronJob)

```




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
## define-command-argument-container
[https://kubernetes.io/docs/tasks/inject-data-application/](https://kubernetes.io/docs/tasks/inject-data-application/)


# Run-application
## Run a Stateless Application Using a Deployment

```
kubectl apply -f https://k8s.io/examples/application/deployment.yaml
```

```
 kubectl apply -f https://k8s.io/examples/application/deployment-update.yaml
```

```
kubectl apply -f https://k8s.io/examples/application/deployment-scale.yaml
```

```
kubectl delete deployment nginx-deployment
```


##  Run a Single-Instance Stateful Application
mysql-pv.yaml:

```
application/mysql/mysql-pv.yaml 

kind: PersistentVolume
apiVersion: v1
metadata:
  name: mysql-pv-volume
  labels:
    type: local
spec:
  storageClassName: manual
  capacity:
    storage: 20Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pv-claim
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 20Gi

```
mysql-deployment.yaml:

```
application/mysql/mysql-deployment.yaml 

apiVersion: v1
kind: Service
metadata:
  name: mysql
spec:
  ports:
  - port: 3306
  selector:
    app: mysql
  clusterIP: None
---
apiVersion: apps/v1 # for versions before 1.9.0 use apps/v1beta2
kind: Deployment
metadata:
  name: mysql
spec:
  selector:
    matchLabels:
      app: mysql
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - image: mysql:5.6
        name: mysql
        env:
          # Use secret in real usage
        - name: MYSQL_ROOT_PASSWORD
          value: password
        ports:
        - containerPort: 3306
          name: mysql
        volumeMounts:
        - name: mysql-persistent-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-persistent-storage
        persistentVolumeClaim:
          claimName: mysql-pv-claim

```

```
kubectl apply -f https://k8s.io/examples/application/mysql/mysql-pv.yaml
```

```
kubectl apply -f https://k8s.io/examples/application/mysql/mysql-deployment.yaml
```
**check**

```
kubectl describe deployment mysql
```


**access mysql**

```
kubectl run -it --rm --image=mysql:5.6 --restart=Never mysql-client -- mysql -h mysql -ppassword
```
**清理资源**
```
kubectl delete deployment,svc mysql
kubectl delete pvc mysql-pv-claim
kubectl delete pv mysql-pv-volume
```


##  Run a Replicated Stateful Application

```
kubectl apply -f https://k8s.io/examples/application/mysql/mysql-configmap.yaml
```

```
kubectl apply -f https://k8s.io/examples/application/mysql/mysql-services.yaml
```

```
kubectl apply -f https://k8s.io/examples/application/mysql/mysql-statefulset.yaml
```

## Update API Objects in Place Using kubectl patch




# Job

## Job 

## Run a normal job in kubernetes

create a job

```
kubectl run busybox --image=busybox --restart=OnFailure
```


```
controllers/job.yaml 

apiVersion: batch/v1
kind: Job
metadata:
  name: pi
spec:
  template:
    spec:
      containers:
      - name: pi
        image: perl
        command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"]
      restartPolicy: Never
  backoffLimit: 4


```


# Access-application-cluster

##  Dash-board 

[http://blog.k8sblog.cn/jekyll/update/2019/08/09/k8s-dashboard.html](http://blog.k8sblog.cn/jekyll/update/2019/08/09/k8s-dashboard.html)


## Configure Access to Multiple Clusters

[related post]    
https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/

https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/

https://kubernetes.io/docs/concepts/configuration/overview/

https://kubernetes.io/docs/reference/kubectl/cheatsheet/#kubectl-context-and-configuration

k8s 通过Configure文件对集群，上下文和用户信息进行集成，然后对用户进行管理。


!!!
### Googler的博客
#### Mastering the KUBECONFIG file
https://ahmet.im/blog/mastering-kubeconfig/


### Kubernetes – KUBECONFIG and Context
https://theithollow.com/2019/02/11/kubernetes-kubeconfig-and-context/


```
使用config命令来给kubectl客户端调整参数，常用的参数如下：

--certificate-authority，CA认证的cert文件。

--client-certificate，TLS的客户端证书。

--client-key，TLS的客户端秘钥。

--user，kubeconfig的用户名。

--cluster，要使用的kubeconfig的cluster名。

--context，要使用的kubeconfig的上下文名称。

--kubeconfig，配置文件路径和名称。

--log-dir，日志路径。

--log-flush-frequency=5s，日志刷新时间间隔。

--logtostderr=true，只输出到屏幕。

--username，apiserver的basic authentication用户名。

--password，apiserver的basic authentication密码。

--server，apiserver地址。

--stderrthreshold=2，该threshold级别以上日志才输出到stderr。

--token，安全访问apiserver的token。

--v=0，日志级别。

以下是一个config命令示例：

> # 设置集群参数

> kubectl config set-cluster kubernetes \

 --certificate-authority=/var/run/kubernetes/ca.crt \

  --embed-certs=true \

  --server=https://ip:port

> # 设置客户端认证参数

> kubectl config set-credentials admin \

 --client-certificate=/var/run/kubernetes/cs_client.crt \

  --embed-certs=true \

 --client-key=/var/run/kubernetes/cs_client.key

> # 设置上下文参数

> kubectl config set-context kubernetes \

  --cluster=kubernetes \

  --user=admin

> # 设置默认上下文

> kubectl config use-context kubernetes

执行后，通过kubectl config view可以看到完整的kubeconfig，文件保存在$HOME/.kube/config，其中证书和秘钥等以密文出现。

```




# Monitoring, Logging, and Debugging
##  Application introspection and Debugging

**Debug a node**
```
kubectl get nodes
```
```
kubectl describe node xxx
```

```
kubectl get node xxxxxxxx -o yaml
```

```
k get events


k get events  -n default
```

##  ~~Auditing~~
## Debug Init Containers

[https://kubernetes.io/docs/tasks/debug-application-cluster/debug-init-containers/](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-init-containers/)


[https://kubernetes.io/docs/concepts/workloads/pods/init-containers/](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

[https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-initialization/#creating-a-pod-that-has-an-init-container/](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-initialization/#creating-a-pod-that-has-an-init-container/)


[https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-initialization/#creating-a-pod-that-has-an-init-container/](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-initialization/#creating-a-pod-that-has-an-init-container/)


## Debug Pods and ReplicationControllers
```shell
kubectl logs ${POD_NAME} ${CONTAINER_NAME}
```
```shell
kubectl logs --previous ${POD_NAME} ${CONTAINER_NAME}
```

```shell
kubectl exec ${POD_NAME} -c ${CONTAINER_NAME} -- ${CMD} ${ARG1} ${ARG2} ... ${ARGN}
```

```shell
kubectl exec cassandra -- cat /var/log/cassandra/system.log
```

## Debug Services


## Get a Shell to a Running Container

```shell
kubectl exec -it shell-demo -- /bin/bash
```

```shell
kubectl exec shell-demo env
```
```shell
kubectl exec shell-demo ps aux
kubectl exec shell-demo ls /
kubectl exec shell-demo cat /proc/1/mounts
```
**Opening a shell when a Pod has more than one Container**

```
kubectl exec -it my-pod --container main-app -- /bin/bash
```

## Monitor Node Health



# Extend Kubernetes

```shell
kubectl run node-hello --image=gcr.io/google-samples/node-hello:1.0 --port=8080
```

```
kubectl proxy --port=8080
```

```
curl http://localhost:8080/api/

{
  "kind": "APIVersions",
  "versions": [
    "v1"
  ],
  "serverAddressByClientCIDRs": [
    {
      "clientCIDR": "0.0.0.0/0",
      "serverAddress": "10.0.2.15:8443"
    }
  ]
}
```





# TLS
# ~~Federation~~
# Manage Cluster Daemons

# Install Service Catalog
[https://github.com/helm/helm/blob/master/docs/install.md](https://github.com/helm/helm/blob/master/docs/install.md)


##  install  helm

###  easy way
```
 snap install helm --classic
```
```
brew install kubernetes-helm
```

```
choco install kubernetes-helm
```
###   script
```
$ curl -LO https://git.io/get_helm.sh
$ chmod 700 get_helm.sh
$ ./get_helm.sh
```
###  binary

[https://github.com/helm/helm/releases](https://github.com/helm/helm/releases)


```
mv  helm  /usr/local/bin
```

##  install Tiller

```
kubectl create -f rbac-config.yaml
```
In `rbac-config.yaml`:
```
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tiller
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: tiller
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
  - kind: ServiceAccount
    name: tiller
    namespace: kube-system
```


```
helm init --service-account tiller --history-max 200
```

##  install helm-App

```
 helm install stable/mariadb 

```




#  ~~Others~~
## ~~Extend kubectl with plugins~~
## ~~Manage HugePages~~
## ~~Schedule GPUs~~
