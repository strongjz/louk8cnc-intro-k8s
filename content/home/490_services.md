+++
title = "Services"
date = 2018-12-09T17:00:31-05:00
weight = 490
+++

# Services


### ![](/images/kubernetes/service.png) 

---

# Service

Service: a named abstraction of software service, consisting of a port that the proxy listens on,
and the selector that determines which pods will answer requests.

Pods come and go, and with that their IP address change rapidly. Services decouple the IP address from the application 
and serve as the IP address inside the cluster for an application running multiple pods. 

More info [here](https://kubernetes.io/docs/concepts/services-networking/service/)

---

# Service

### ![](/images/kubernetes/application-service.png) 

---

### Application Deployment

Create a secret for the password between Wordpress and MYSQL
```bash
kubectl create secret generic mysql-pass --from-literal=password=YOUR_PASSWORD
```

Verify it is there
```
kubectl get secrets
```

---

### Application Deployment

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

* Pod Deployment with health checks, PersistentVolume and claim

* Since we have created the mysql pod several times, here is a yaml file that creates it all.



Deploy mysql
```
kubectl apply -f mysql-all.yaml
```

Verify mysql deployed properly
```
kubectl get deploy
```

---

### Application Deployment
Deploy the application that will use mysqld

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
```

```bash
kubectl delete -f mysql-service.yaml
```

```bash
kubectl delete -f app.yaml
```

