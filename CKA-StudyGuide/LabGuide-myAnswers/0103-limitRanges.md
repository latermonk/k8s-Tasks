#  Answers




# **CKA Lab Part 1 - Scheduling**

- **create a ns**
```
k create ns xxx
```

- **create a LimitRange**
```
apiVersion: v1
kind: LimitRange
metadata:
  name: limit-mem-cpu-per-container
spec:
  limits:
  - max:
      memory: "100Mi"
    type: Container

```

```
k  apply -f  limitranges-yaml
```
- **create a pod in the ns **
```
k -n tenant-b-100mi run web-memory-m --image=nginx --restart=Never --requests='memory=150Mi' 
```
- **result**


```
The Pod "web-memory-m" is invalid: spec.containers[0].resources.requests: Invalid value: "150Mi": must be less than or equal to memory limit

```

#  extend knowledge

可以为一个ns指定一个limitrange

在这个ns下创建Pod的时候，如果：

- 只指定了limit  ->   request & limit 都按指定的来
- 只指定了request  ->   request按指定的  limit按limitrange的来




[https://kubernetes.io/docs/concepts/policy/limit-range/](https://kubernetes.io/docs/concepts/policy/limit-range/)
[https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/memory-default-namespace/](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/memory-default-namespace/)


