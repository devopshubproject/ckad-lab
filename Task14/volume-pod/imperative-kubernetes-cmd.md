Create a PersistentVolume, connect it to a PersistentVolumeClaim and mount the claim to a specific path of a Pod.


#Solution

Create Persistent Volume mainfest file

```
[node1 ~]$ vi pv.yml

[node1 ~]$ cat pv.yml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv
spec:
  capacity:
    storage: 512m
  accessModes:
    - ReadWriteMany
  storageClassName: shared
  hostPath:
    path: /data/config
```

To get the Persistent Volume created

```shell
[node1 ~]$ kubectl get pv
NAME   CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   REASON   AGE
pv     512m       RWX            Retain           Available           shared                  5s
```

Create Persistent Volume Claim mainfest file

```
[node1 ~]$ vi pvc.yml

[node1 ~]$ cat pvc.yml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 256m
  storageClassName: shared
```

To get the Persistent Volume Claim created

```
[node1 ~]$ kubectl get pvc
NAME   STATUS   VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
pvc    Bound    pv       512m       RWX            shared         5s
```

Now go back to get pv to check the claim option

```
[node1 ~]$ kubectl get pv
NAME   CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM         STORAGECLASS   REASON   AGE
pv     512m       RWX            Retain           Bound    default/pvc   shared                  1m
```

Create a Pod using the volume claim

```
[node1 ~]$ kubectl create -f pod.yml

`< Pod mainfest in under task folder >' 
