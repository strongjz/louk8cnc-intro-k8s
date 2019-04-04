+++
title = "Pods"
date = 2018-12-09T17:00:31-05:00
weight = 420

+++

### [Pods](https://kubernetes.io/docs/concepts/workloads/pods/pod/)

Pods are a collection of containers that share a namespace, are colocated and scheduled together on Kubenetes nodes.

A pod is a group of one or more containers, with shared storage/network, and a specification for how to run the containers

![](/louk8cnc-intro-k8s/images/pods.png)

---


### Labels

Labels are key/value pairs that are attached to objects, such as pods that help to identify that object.


### Selectors

Label Selectors help client/user identify a set of objects.

```yaml
spec:
  selector:
    matchLabels:
      app: mysql
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: mysql
```

---
   
### Demo 

Create labels & use selector to identify set of objects



