

# k8s-Tasks 8

https://kubernetes.io/docs/tasks


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
# Run-application
## Run a Stateless Application Using a Deployment


### Create & Updating  & Scaling  & Deleting
#### YAMl WAY
#### CMD LINE

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



# Job

## Job 

## Run a normal job in kubernetes

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
