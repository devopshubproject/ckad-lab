As a Kubernetes application developer you will often find yourself needing to update a running application.


#Solution

Create a deployment

```shell
kubectl create deployment deploy --image=nginx --dry-run=client -o yaml > deploy.yml
```
```
[node1 ~]$ cat deploy.yml
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
      - image: nginx
        name: nginx
        resources: {}
status: {}
[node1 ~]$
```

Change the version of the image

```shell
kubectl set image deployment/deploy nginx=nginx:1.13.7
```

To check the history

```
[node1 ~]$ kubectl rollout history deployments/deploy
deployment.apps/deploy
REVISION  CHANGE-CAUSE
1         <none>
2         <none>
```

To scale the deployment

Before scaling

```
[node1 ~]$ kubectl get pods
NAME                     READY   STATUS    RESTARTS   AGE
deploy-f6ff8d599-lg7rl   1/1     Running   0          118s
```

After scaling

```
[node1 ~]$ kubectl scale deployment deploy --replicas=5
deployment.apps/deploy scaled
[node1 ~]$ kubectl get pods
NAME                     READY   STATUS              RESTARTS   AGE
deploy-f6ff8d599-4vzsq   0/1     ContainerCreating   0          6s
deploy-f6ff8d599-bct9h   0/1     ContainerCreating   0          6s
deploy-f6ff8d599-djmrk   0/1     ContainerCreating   0          6s
deploy-f6ff8d599-lg7rl   1/1     Running             0          2m40s
deploy-f6ff8d599-rm6vr   0/1     ContainerCreating   0          6s
[node1 ~]$
```

To increase the maxSurge and maxUnavailable value:

Edit the Strategy

```
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
 ```

 '<Fully updated mainfest file in the task folder>'


To rollback to the prevision release

```shell
kubectl rollout undo deployment/deploy
```

To rollback to the specific release

```shell
kubectl rollout undo deployment/deploy --to-revision=1
```

To record the commands used in the deployment

```shell
kubectl apply -f deploy.yml --record=true
```