# **Network security policy**

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
 name: deny-to-nginx
spec:
 podSelector:  
   matchLabels:
     tier: web
 policyTypes:
 - Ingress

```



```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
 name: deny-to-nginx
spec:
 podSelector:  
   matchLabels:
     tier: web
 policyTypes:
 - Ingress
 ingress:
   - from:
     - podSelector:
         matchLabels:
          tier: jumppod 
```


