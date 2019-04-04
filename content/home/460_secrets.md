+++
title = "Secrets"
date = 2018-12-09T17:05:14-05:00
weight = 460

+++

---

# Secrets

### ![](/louk8cnc-intro-k8s/images/kubernetes/secret.png) 

---

# Secrets

Kubernetes object to inject sensitive data into containers

Sensitive data should never be built into the container image, in order to do that, kubernetes offers Secrets. 

---

# Secrets
 
```bash
echo -n 'admin' | base64
YWRtaW4=
echo -n '1f2d1e2e67df' | base64
MWYyZDFlMmU2N2Rm
```

Write a Secret that looks like this:
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque
data:
  username: YWRtaW4=
  password: MWYyZDFlMmU2N2Rm
```

---

# Secrets ENV

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-env-pod
spec:
  containers:
  - name: mycontainer
    image: redis
    env:
      - name: SECRET_USERNAME
        valueFrom:
          secretKeyRef:
            name: mysecret
            key: username
      - name: SECRET_PASSWORD
        valueFrom:
          secretKeyRef:
            name: mysecret
            key: password
  restartPolicy: Never

  ```
  
---

# Secrets File

```yaml
apiVersion: v1
   kind: Pod
   metadata:
     name: mypod
   spec:
     containers:
     - name: mypod
       image: redis
       volumeMounts:
       - name: foo
         mountPath: "/etc/foo"
         readOnly: true
     volumes:
     - name: foo
       secret:
         secretName: mysecret
``` 
