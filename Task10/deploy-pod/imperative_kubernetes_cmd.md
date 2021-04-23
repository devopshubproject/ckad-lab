Create a new Deployment for running ngnix

#Solution

Create a Namespace

```shell
kubectl create namespace ns-deploy
```

(or)

```
[node1 ~]$ vi namespace.yml
apiVersion: v1
kind: Namespace
metadata:
  name: ns-deploy
```

Create a deployment

`< Deploy mainfest in under Task folder>`

```shell
kubectl create -f deploy_pod.yml
```

(or)

```
[node1 ~]$ kubectl create deployment ns-deploy --image=nginx:1.14.2 --dry-run=client -o yaml > deploy_pod.yml
```