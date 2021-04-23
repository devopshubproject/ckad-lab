Consider a Pod is running on the cluster but it is not responding.
The desired behavior is to have Kubernetes restart the pod when an endpoint returns an
HTTP 500 on the /healthz endpoint. The service, liveness-pod , should never send traffic to
the Pod while it is failing.


#Solution

To create a pod definition using run command.

```shell
kubectl run healthpod --image=k8s.gcr.io/liveness --restart=Never -o yaml --dry-run > health_pod.yml
```

```
[node1 ~]$ vi health_pod.yml

apiVersion: v1
kind: Pod
metadata:
 creationTimestamp: null
 labels:
 	run: liveness-pod
 name: liveness-pod
spec:
 containers:
 - image: k8s.gcr.io/liveness
    name: liveness-pod
 	args:
 	- /server
 	resources: {}
 dnsPolicy: ClusterFirst
 restartPolicy: Never
status: {}
```

To create a Pod 

`< Updated Pod definition is the task folder >`

```shell
kubectl create -f health_pod.yml
```

To check the events of the Pod

```shell
kubectl describe pod/healthpod
```