
```
Q1:kubernetes      dial tcp    :10250: connect: no route to host




node3 firewalld is open , close th firewall
```



```
Q2: Master node notReady
```
[https://talkcloudlytome.com/troubleshooting-kubernetes-master-nodes/](https://talkcloudlytome.com/troubleshooting-kubernetes-master-nodes/)

```bash
kubectl get nodes
```
```bash
kubectl describe node k8s-master-
```

```bash
systemctl status kubelet.service
```


