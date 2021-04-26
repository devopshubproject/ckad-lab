Fix the issue with the image and chagne the image

#Solution

Create the deployment

// Creating the deployment with wrong image name just for the lab //

```shell
kubectl create deployment deploy --image=nginx:prem --dry-run=client -o yaml > troubleshoot_pod.yml
```

```
[node1 ~]$ cat troubleshoot_pod.yml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: deploy
  name: deploy
spec:
  replicas: 1
  selector:
    matchLabels:
      app: deploy
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: deploy
    spec:
      containers:
      - image: nginx:prem
        name: nginx
        resources: {}
status: {}
```

Checks:

```
[node1 ~]$ kubectl get deploy -o wide
NAME     READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES       SELECTOR
deploy   0/1     1            0           56s   nginx        nginx:prem   app=deploy


[node1 ~]$ kubectl describe deploy
Name:                   deploy
Namespace:              default
CreationTimestamp:      Mon, 26 Apr 2021 15:39:20 +0000
Labels:                 app=deploy
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=deploy
Replicas:               1 desired | 1 updated | 1 total | 0 available | 1 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=deploy
  Containers:
   nginx:
    Image:        nginx:prem
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      False   MinimumReplicasUnavailable
  Progressing    True    ReplicaSetUpdated
OldReplicaSets:  <none>
NewReplicaSet:   deploy-67c5576d9 (1/1 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  62s   deployment-controller  Scaled up replica set deploy-67c5576d9 to 1
[node1 ~]$
```

To fix correct the image version/tag

Try are couple of ways to do it, but to keep it simple I am doing it using imperative commands

```shell
kubectl set image deployment/deploy nginx=nginx:latest

```
```
[node1 ~]$ kubectl set image deployment/deploy nginx=nginx:latest
deployment.apps/deploy image updated


[node1 ~]$ kubectl get deploy -o wide
NAME     READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES         SELECTOR
deploy   1/1     1            1           4m38s   nginx        nginx:latest   app=deploy



[node1 ~]$ kubectl describe deploy
Name:                   deploy
Namespace:              default
CreationTimestamp:      Mon, 26 Apr 2021 15:39:20 +0000
Labels:                 app=deploy
Annotations:            deployment.kubernetes.io/revision: 2
Selector:               app=deploy
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=deploy
  Containers:
   nginx:
    Image:        nginx:latest
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   deploy-b6c47b7d (1/1 replicas created)
Events:
  Type    Reason             Age    From                   Message
  ----    ------             ----   ----                   -------
  Normal  ScalingReplicaSet  4m42s  deployment-controller  Scaled up replica set deploy-67c5576d9 to 1
  Normal  ScalingReplicaSet  31s    deployment-controller  Scaled up replica set deploy-b6c47b7d to 1
  Normal  ScalingReplicaSet  27s    deployment-controller  Scaled down replica set deploy-67c5576d9 to 0
[node1 ~]$
```