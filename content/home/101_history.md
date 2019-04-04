+++
title = "Beginning"
date = 2018-12-09T17:20:59-05:00
weight = 101
+++

# History 

---

# In the beginning 

![](/louk8cnc-intro-k8s/images/docker/app2.png)


---

# The Hypervisor

![](/louk8cnc-intro-k8s/images/docker/vm.png)

---

# 2007 

### Container Primitives

* Control Groups
* Namespaces

---

#### Control Groups

Abbreviated cgroups, is a Linux kernel feature that limits, accounts for, and isolates the resource usage

* CPU 
* memory
* disk I/O
* network
 
---
 
#### Namespaces

A feature of the Linux kernel that isolate and virtualize system resources of a collection of processes. Examples of resources that can be virtualized include: 

* process IDs
* hostnames
* user IDs
* network access
* interprocess communication
* filesystems

---

# Containers

![](/louk8cnc-intro-k8s/images/docker/containers.png)

---

# Rise of the Containers (runtimes)

* lxc
* Docker ( containerd )
* rkt
* runc
* lmctfy
* cri-o

---

![](/louk8cnc-intro-k8s/images/container_fail.png)

---


# The orchestrator

---

# 2010 

Mesosphere 

---

# 2013 

Docker Released

.1 release of Docker Compose

---

# 2014 

**Kubernetes** released

Rancher Release 1.0 supports Docker Swarm, Meso and Kubernetes  Docker container runtime 

---

# 2016 

Mesophere supports Docker, rkt, and appc for container runtimes

---

# 2017 

Mesophere add supports for Kubernetes 
 
---

# 2018 

Docker EE 2.0 has support for the Kubernetes orchestrator





