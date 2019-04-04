+++
title = "Configmaps"
date = 2018-12-09T17:05:14-05:00
weight = 470
+++

### What

In order to keep the immutablity of a docker image, the configuration must live outside the container image, 
K8 config maps enable this. 

### Why
Secrets, env variables, and other environment specific items should not be baked into a container image.


### ![](/images/kubernetes/cm.png) 

---


{{< highlight yaml "linenos=inline" >}}
apiVersion: v1
data:
  game.properties: |
    enemies=aliens
    lives=3
    enemies.cheat=true
    enemies.cheat.level=noGoodRotten
    secret.code.passphrase=UUDDLRLRBABAS
    secret.code.allowed=true
    secret.code.lives=30
  ui.properties: |
    color.good=purple
    color.bad=yellow
    allow.textmode=true
    how.nice.to.look=fairlyNice
kind: ConfigMap
metadata:
  name: game-config
  namespace: default
  
{{< / highlight >}}

---


{{< highlight yaml "linenos=inline,hl_lines=13-15 18-20 ,linenostart=1" >}}
apiVersion: v1
kind: Pod
metadata:
  name: dapi-test-pod
spec:
  containers:
    - name: test-container
      image: k8s.gcr.io/busybox
      command: [ "/bin/sh", "-c", "echo $(SPECIAL_LEVEL_KEY) $(SPECIAL_TYPE_KEY)" ]
      env:
        - name: SPECIAL_LEVEL_KEY
          valueFrom:
            configMapKeyRef:
              name: special-config
              key: SPECIAL_LEVEL
        - name: SPECIAL_TYPE_KEY
          valueFrom:
            configMapKeyRef:
              name: special-config
              key: SPECIAL_TYPE
  restartPolicy: Never
{{< / highlight >}}

---


{{< highlight yaml "linenos=inline,hl_lines=8-10 14-16 ,linenostart=1" >}}
apiVersion: v1
kind: Pod
metadata:
  name: dapi-test-pod
spec:
  containers:
    - name: test-container
      image: k8s.gcr.io/busybox
      command: [ "/bin/sh", "-c", "ls /etc/config/" ]
      volumeMounts:
      - name: config-volume
        mountPath: /etc/config
  volumes:
    - name: config-volume
      configMap:
        name: special-config
  restartPolicy: Never
{{< / highlight >}}

