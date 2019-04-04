+++
title = "Services"
date = 2018-12-09T17:00:31-05:00
weight = 490
+++

### What

Service: a named abstraction of software service, consisting of a port that the proxy listens on,
and the selector that determines which pods will answer requests.

### Why

Pods come and go, and with that their IP address change rapidly. Services decouple the IP address from the application 
and serve as the IP address inside the cluster for an application running multiple pods. 

More info [here](https://kubernetes.io/docs/concepts/services-networking/service/)

### ![](/louk8cnc-intro-k8s/images/kubernetes/service.png) 

---

### ![](/louk8cnc-intro-k8s/images/kubernetes/application-service.png) 

---

### Pod Deployment with health checks, PersistentVolume and claim

Since we have created the mysql pod several times, here is a yaml file that creates it all.

### Create a secret for the password between Wordpress and MYSQL

```bash
kubectl create secret generic mysql-pass --from-literal=password=YOUR_PASSWORD
```

Verify it is there
```
kubectl get secrets
```

Deploy mysql
```
kubectl apply -f mysql-all.yaml
```

Verify mysql deployed properly
```
kubectl get deploy
```

---

### Services

Deploy the service for mysql
```
kubectl apply -f mysql-service.yaml
```

Verify the service has endpoints.
```
kubectl get services -o wide
```

---

### Application Deployment
deploy the application that will use mysqld
```
kubectl apply -f app.yaml
```

Verify Service
```
kubectl get services wordpress
```

---

### Clean up

```bash
kubectl delete -f mysql-all.yaml

kubectl delete -f mysql-service.yaml

kubectl delete -f app.yaml
```

