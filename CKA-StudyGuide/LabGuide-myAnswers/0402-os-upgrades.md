#  [custom columns](https://kubernetes.io/docs/reference/kubectl/overview/#custom-columns):


```
kubectl get pod -o=custom-columns=NAME:.metadata.name,STATUS:.status.phase,NODE:.spec.nodeName --all-namespaces
```



```
kubectl get pod -o=custom-columns=NODE:.spec.nodeName,NAME:.metadata.name --all-namespaces
```


![customer-columns](_image/customer-columns.png)


#  drain a node



```
kubectl drain k8s-worker-03 --ignore-daemonsets
```

![drain-a-node](_image/drain-a-node.png)


#  Gracefully return a node into active service


```
k uncordon i-d84442fa
```
![node-abck-again](_image/node-abck-again.png)






