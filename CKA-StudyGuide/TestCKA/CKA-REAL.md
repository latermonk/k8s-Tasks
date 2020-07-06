1.列出指定pod的日志中状态为Error的行，并记录在指定的文件上。

```
kubectl logs <podname> | grep bash > xxx.txt
https://kubernetes.io/docs/tasks/debug-application-cluster/debug-pod-replication-controller/
```

2.列出环境内所有的pv 并以 capacity字段排序

```
（使用kubectl自带排序功能，field字段关注下）
kubectl get pv --sort-by=.spec.capacity.storage
https://kubernetes.io/docs/concepts/overview/working-with-objects/field-selectors/
```

3.列出k8s可用的节点，不包含不可调度的 和 NoReachable的节点，并把数字写入到文件里。

```
kubectl get nodes; kubectl get nodes xxx -oyaml
https://kubernetes.io/docs/concepts/architecture/nodes/
```

4.创建一个pod名称为nginx，并将其调度到节点为 disk=stat上

```
nodeselector 字段
https://kubernetes.io/docs/concepts/configuration/assign-pod-node/
```

5.提供一个pod的yaml，要求添加Init Container，Init Container的作用是创建一个空文件，pod的Containers判断文件是否存在，不存在则退出

```
init container
https://kubernetes.io/docs/concepts/workloads/pods/init-containers/
```

6.指定在命名空间内创建一个pod名称为test，内含四个指定的镜像nginx、redis、memcached、busybox.

```
https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/
```

7.创建一个命名空间

```
kubectl create ns xx
https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/
```

8.在一个新的命名空间创建pod

```
https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/
```

9.列出Service名为test下的pod 并找出使用CPU使用率最高的一个，将pod名称写入文件中.

```
kubectl get svc test -oyaml; 查看配置内容，特别找出标签
kubectl top nodes --selector="xxx=yy"
https://kubernetes.io/docs/tasks/debug-application-cluster/debug-service/
```

10.创建一个Pod名称为nginx-app，镜像为nginx，并根据pod创建名为nginx-app的Service，type为NodePort

```
kubectl expose xx
https://kubernetes.io/docs/tasks/access-application-cluster/service-access-application-cluster/
```

11.创建一个nginx的daemonset，保证其在每个节点上运行，注意不要覆盖节点原有的Tolerations

```
https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/
```

12.将deployment为nginx-app的副本数从1变成4

```
kubectl scale deployment xx --replicas=4
https://kubernetes.io/docs/tasks/run-application/scale-stateful-set/
```

13.创建nginx-app的deployment ，使用镜像为nginx:1.11.0-alpine ,修改镜像为1.11.3-alpine，并记录升级，再使用回滚，将镜像回滚至nginx:1.11.0-alpine

```
kubectl rollout xx
https://kubernetes.io/docs/tasks/run-application/rolling-update-replication-controller/
```

14.根据已有的一个nginx的pod、创建名为nginx的svc、并使用nslookup查找出service dns记录，pod的dns记录并分别写入到指定的文件中

```
busybox:1.28
https://kubernetes.io/docs/tasks/administer-cluster/dns-debugging-resolution/
```

15.创建Secret 名为mysecret，内含有password字段，值为bob，然后 在pod1里 使用ENV进行调用，Pod2里使用Volume挂载在/data 下

```
https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/
https://kubernetes.io/docs/concepts/storage/volumes/
```

16.使node1节点不可调度，并重新分配该节点上的pod

```
kubectl drain nodex
kubectl uncordon nodex
https://kubernetes.io/docs/concepts/architecture/nodes/
```

17.使用etcd 备份功能备份etcd（提供enpoints，ca、cert、key）

```
https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/
https://blog.51cto.com/9406836/2409012
https://github.com/mmumshad/certified-kubernetes-administrator-course-answers/blob/master/etcd-backup-and-restore.md
```

18.给出一个失联节点的集群，排查节点故障，要保证改动是永久的。

```
kubectl get nodes 故障节点 -oyaml 查看故障
远程到故障节点启动kubelet服务
https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/
```

19.给出一个集群，排查出集群的故障。集群无法使用kubectl。

```
集群无法使用kubectl，先到主节点，查看kubelet配置，static-pod配置文件出错，更改重新
https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/
```

20.创建static pods.

```
https://kubernetes.io/docs/tasks/administer-cluster/static-pod/
```

21.给出一个集群，将节点node1添加到集群中，并使用TLS bootstrapping（难度特别大，建议放弃）

```
https://github.com/mmumshad/certified-kubernetes-administrator-course-answers/blob/master/tls-bootstrap-worker-node-2
https://github.com/opsnull/follow-me-install-kubernetes-cluster/blob/master/07-2.kubelet.md
```

22.创建一个pv，类型是hostPath，位于/data中，大小1G，模式ReadOnlyMany

```
https://kubernetes.io/docs/concepts/storage/persistent-volumes/
```

23.创建一个pod，使用hostpath。

```
https://kubernetes.io/docs/concepts/storage/volumes/
```