Create two texts files in /tmp/

db_h.txt with the contents “database_host”

db_p.txt with the contents “database_port”

Create a configmap called “dbconnection” from the above two files.

Create a nginxpod which leverages these values as environment variables “db_h” and “db_p”


**create configmap**


```
k create configmap dbconnection --from-file=db_h=db_h.txt --from-file=db_p=db_p.txt
```


```
k describe configmaps dbconnection 
```


```
Name:         dbconnection
Namespace:    default
Labels:       <none>
Annotations:  <none>

Data
====
db_h:
----
“database_host”

db_p:
----
“database_port”

Events:  <none>

```


```
 k run web --image=nginx --restart=Never -o yaml --dry-run  > nginx-pod.yaml 
```



```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: web
  name: web
spec:
  containers:
  - image: nginx
    name: web
    env:
      - name: SPECIAL_LEVEL_KEY
        valueFrom:
          configMapKeyRef:
            name: dbconnection
            key: db_h
      - name: SPECIAL_LEVEL_KEY
        valueFrom:
          configMapKeyRef:
            name: dbconnection
            key: db_p
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}

```

