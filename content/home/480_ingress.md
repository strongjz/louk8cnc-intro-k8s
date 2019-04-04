+++
title = "ingress"
date = 2018-12-09T17:05:14-05:00
weight = 480

+++

# Ingress

### ![](/louk8cnc-intro-k8s/images/kubernetes/ing.png) 

---

# Ingress

Ingress is a K8 object that allows external access to resources inside the cluster
 
Services, Pods and other objects are only accessible inside the cluster

---

## Ingress Controllers

* In order for the ingress resource to work, the cluster must have an ingress controller running. 
* This is unlike other types of controllers, which run as part of the kube-controller-manager binary, and 
are typically started automatically with a cluster. 
* Choose the ingress controller implementation that best fits your cluster.

---

## Ingress Controller 

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: test-ingress
spec:
  backend:
    serviceName: testsvc
    servicePort: 80
```

---

## Ingress controllers

Kubernetes supported Ingress Controllers: 

* [GCE](https://git.k8s.io/ingress-gce/README.md)
* [nginx](https://git.k8s.io/ingress-nginx/README.md)

Others that can be deployed:

* [HAProxy](http://www.haproxy.org/)
* [Kong](https://konghq.com/)
* [Contour](https://github.com/heptio/contour)

Full list is [here](https://kubernetes.io/docs/concepts/services-networking/ingress/)

---

## Ingress Rules

Each http rule contains the following information:

* Host
* list of paths
* Backend service

---

## Ingress Rule

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: simple-fanout-example
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: foo.bar.com
    http:
      paths:
      - path: /foo
        backend:
          serviceName: service1
          servicePort: 4200
      - path: /bar
        backend:
          serviceName: service2
          servicePort: 8080

```

