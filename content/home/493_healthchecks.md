+++
title = "Healthchecks"
date = 2018-12-09T17:00:31-05:00
weight = 493
+++

# Health Checks

---

# Health Checks

Healthchecks inform that kubelet that pods are ready to accept traffic


The distributed nature of kubernetes allows pods to come and go for a number of reasons, and if many are running
 a application the kubelet needs to know what a "healthy" pod looks like. 
 
---

### [Readiness and Liveliness](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/)

## Liveliness

Liveliness checks inform the kubelet that the pod is running. If this check fails the kubelet will attempt to restart the pod.

---

## Liveliness

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    test: liveness
  name: liveness-exec
spec:
  containers:
  - name: liveness
    image: k8s.gcr.io/busybox
    args:
    - /bin/sh
    - -c
    - touch /tmp/healthy; sleep 30; rm -rf /tmp/healthy; sleep 600
    livenessProbe:
      exec:
        command:
        - cat
        - /tmp/healthy
      initialDelaySeconds: 5
      periodSeconds: 5
 ```
 
---
 

### [Readiness and Liveliness](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/)


## Readiness

Readiness checks let the kubelet know that the pod is ready to receive traffic. For example if this check fails the Service or Load balancer does send traffic to that pod.

---

## Readiness

```yaml
readinessProbe:
    exec:
      command:
      - cat
      - /tmp/healthy
    initialDelaySeconds: 5
    periodSeconds: 5
```

