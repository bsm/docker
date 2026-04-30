# Console

Simple console container, useful as a dev pod.

To deploy in K8s, add the following manifest:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: console
spec:
  containers:
    - name: console
      image: ghcr.io/bsm/docker/console:latest
      imagePullPolicy: Always
```

To execute custom commands at boot time you can include custom init scripts into a
`ConfigMap`. For example:

```yaml
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: console-boot
  namespace: default
data:
  10-nproc.sh: |
    #!/bin/bash

    nproc > /tmp/NPROC
---
apiVersion: v1
kind: Pod
metadata:
  name: console
  namespace: console
spec:
  containers:
    - name: console
      image: ghcr.io/bsm/docker/console:latest
      imagePullPolicy: Always
      volumeMounts:
        - mountPath: "/etc/console/init/boot.d"
          name: bootd
  volumes:
    - name: bootd
      configMap:
        name: console-boot
```
