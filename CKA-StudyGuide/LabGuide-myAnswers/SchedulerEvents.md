**Scheduler**


```
kubectl run nginx --image=nginx
```


Extract the events from the cluster, particularly those pertaining to scheduling to find where this pod was scheduled to.


```
kubectl describe pod nginx-7db9fccd9b-xw6qd
```


Extract the logs from the pod running the default scheduler, or from the respective file if running as a deamon service on your master node.

##  kube-schedule as a Pod
```
kubectl get pods -n kube-system | grep sch
kube-scheduler-k8s-master-03        	1/1 	Running   0      	3h1m

kubectl logs kube-scheduler-k8s-master-03 -n kube-system
```
##  kube-schedule as a Process


```

ps -ef|grep kube-schedule

kube-scheduler --bind-address=127.0.0.1 --kubeconfig=/etc/kubernetes/scheduler.conf --leader-elect=true



```


```
journal -u  kube-chedule
```



