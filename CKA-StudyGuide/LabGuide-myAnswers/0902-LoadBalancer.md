
```
kubectl run nginx --image=nginx --replicas=3 --port=80
```


```
kubectl expose deployment nginx --port=8080 --target-port=80 --type=LoadBalancer
```



