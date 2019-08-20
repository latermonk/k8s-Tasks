# ClusterIP:

```
k  run web --image=nginx --replicas=3
```



```
k expose deployment web --port=8080 --target-port=80  --type=ClusterIP

```


![cluster-ip](_image/cluster-ip.png)




```
k run busybox --image=busybox --restart=Never -ir --rm -- sh
```

```
wget -O- svc:Port
```
#  NodePort


```
k  run web --image=nginx --replicas=3
```



```
k expose deployment web --port=30010 --target-port=80  --type=NodePort

```


![port](_image/port.png)


```
k run busybox --image=busybox --restart=Never -ir --rm -- sh
```

```
wget -O- svc:Port
```


```
wget  -O- NodeIP:NodePort  
```

