# cluster-role

**sa-user**
```
k create sa cluster-user-secretadmin
```

**clusterrole**
```
k create clusterrole  cluster-role-secretadmin --verb=get --verb=list --verb=watch --resource=secrets 
```

**clusterrolebinding **
```
k create clusterrolebinding rbac-rbac --user=cluster-user-secretadmin   --clusterrole=cluster-role-secretadmin
```
**--user=xxxx**


