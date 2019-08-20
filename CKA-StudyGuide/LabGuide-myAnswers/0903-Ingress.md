#  ingress  

[https://kubernetes.io/docs/concepts/services-networking/ingress/](https://kubernetes.io/docs/concepts/services-networking/ingress/)



```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: website-ingress
 annotations:
   nginx.ingress.kubernetes.io/rewrite-target: /
spec:
 rules:
 - http:
     paths:
     - path: /         
       backend:
         serviceName: default-service
         servicePort: 80
     - path: /backend         
       backend:
         serviceName: backend-service
         servicePort: 443
     - path: /test
       backend:
         serviceName: test-service
         servicePort: 8000

```


