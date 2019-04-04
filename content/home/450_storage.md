+++
title = "Storage"
date = 2018-12-09T17:00:31-05:00
weight = 450
+++

# Storage 

![](/louk8cnc-intro-k8s/images/kubernetes/pv.png) 

---

# Storage 

Storage like compute is another resource that must be managed. Kubernetes offers 3 types of storage 

* Volumes
* Persistent Volumes
* Persistent Volume Claims

The Ephemeral nature of pods and containers lead to the need for data to be have a decoupled lifecycle outside of
containers and pods.

---

# Storage Classes

Storage classes allow cluster administrators to provide varing levels of support and types of storage to applications 
in a cluster


Example: Storage class that will provision an AWS EBS Volumes when referenced a PVC

```yaml
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: standard
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
reclaimPolicy: Retain
mountOptions:
  - debug
volumeBindingMode: Immediate
```

---

# Volume Types

Several volume types are supported

* awsElasticBlockStore
* azureDisk
* gcePersistentDisk
* hostPath
* secret
* configmaps

---

# Volume Types Example

awsElasticBlockStore example yaml: 

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-ebs
spec:
  containers:
  - image: k8s.gcr.io/test-webserver
    name: test-container
    volumeMounts:
    - mountPath: /test-ebs
      name: test-volume
  volumes:
  - name: test-volume
    # This AWS EBS volume must already exist.
    awsElasticBlockStore:
      volumeID: <volume-id>
      fsType: ext4
```

---

# Persistent Volumes

Persistent Volumes (PV's) are a piece of storage provisioned in a cluster and can be used/reference in the cluster
like another other resource. 

Provisioning - Static or Dynamic 

Types of PV's 

* GCEPersistentDisk
* AWSElasticBlockStore
* AzureFile
* CephFS

---

# Example

```yaml
kind: PersistentVolume
apiVersion: v1
metadata:
  name: task-pv-volume
  labels:
    type: local
spec:
  storageClassName: manual
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
 ```
 
---

# Persistent Volume Claims

Persistent Volume Claims (PVC's) - Allow pods to requests and attache Persistent Volumes available in the cluster. 

When used in with Dynamic provision and Storage Classes, PVC's can automatically make storage available on demand. 

Types of PVC's 

* GCEPersistentDisk
* AWSElasticBlockStore
* AzureFile
* CephFS

---

# Example

```yaml
kind: Pod
apiVersion: v1
metadata:
  name: mypod
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: mypd
  volumes:
    - name: mypd
      persistentVolumeClaim:
        claimName: myclaim
 ```
 
---

# Storage Demo

Create a persistent volume and claim
```bash
kubectl apply -f mysql-pv.yaml
```

Create a pod that will use it.

```bash
kubectl apply -f mysql-pod.yaml

```

### Clean up
```bash
kubectl delete -f mysql-pv.yaml

kubectl delete -f mysql-pod.yaml

```

