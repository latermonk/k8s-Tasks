List the logs from the following components on a master node:



*   Kube-APIServer

```
cat /var/log/kube-apiserver.log
or
journalctl -u kube-apiserver
or
kubectl logs kube-apiserver-k8s-master-03 -n kube-system
```


*   Kube-Scheduler

```
cat /var/log/kube-scheduler.log
or
journalctl -u kube-scheduler
or
kubectl logs kube-scheduler-k8s-master-03 -n kube-system

```


*   Kube-Controller-Manager


```
cat /var/log/kube-controller-manager.log
or
journalctl -u kube-controller-manager
or
kubectl logs kube-controller-manager-k8s-master-03 -n kube-system
```



List the logs from the following components on a worker node:



*   CNI
```
journalctl -u flanneld


or

kubectl logs kube-flannel-ds-amd64-9mrnj -n kube-system

```


*   Kube-Proxy

```
journalctl -u kube-proxy
or
cat /var/log/kube-proxy.log
or
kubectl logs kube-flannel-ds-amd64-9mrnj -n kube-system

```


*   Kubelet

```
journalctl -u kubelet
Or
cat /var/log/kubelet.log

```



*   Container Runtime

```
journalctl -u docker.service
Or
cat /var/log/docker.log
```



-----


