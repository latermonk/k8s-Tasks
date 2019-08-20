#  etcd backup


[https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)




```
 ETCDCTL_API=3 etcdctl snapshot save snapshotdb 
--cacert /etc/kubernetes/pki/etcd/server.crt 
--cert /etc/kubernetes/pki/etcd/ca.crt 
--key /etc/kubernetes/pki/etcd/ca.key
```



```
 ETCDCTL_API=3 etcdctl --write-out=table snapshot status snapshotdb
```


# **Kubernetes certificates backup**


```
Tar -zcvf pki-certs.tar.gz /etc/kubernetes/pki
```

