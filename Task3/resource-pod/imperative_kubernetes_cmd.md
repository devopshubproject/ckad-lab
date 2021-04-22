In this task it is required to create a Pod that requests a certain amount of CPU and memory, so it gets scheduled to a node that has those resources available

#Solution

Create a namespace

```shell
kubectl create namespace ns-nginx
```

Create a Pod definition with run cmd along with Resource specification in a specific namespace

```shell
kubectl run nginx --image=nginx -n ns-nginx --requests='cpu=400m,memory=3Gi' --restart=Never --dry-run=client -o yaml > resource_pod.yml
```

```
$ vi resource_pod.yml

apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
  namespace: ns-nginx
spec:
  containers:
  - image: nginx
    name: nginx
    resources:
      requests:
        cpu: 400m
        memory: 3Gi
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```

To create a Pod with generated pod definition

```shell
kubectl apply -f resource_pod.yml
```

To verify the resource created

```shell
kubectl describe pod nginx -n ns-nginx | less
```
