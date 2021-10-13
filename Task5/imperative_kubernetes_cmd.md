This task is to make the application’s Namespace requires a specific ServiceAccount to be used.

#Solution

Create a namespace

```shell
kubectl create namespace ns-prd
```

Create a ServiceAccount

```shell
kubectl create serviceaccount app-service -n ns-prd
```

Create a Deployment

```shell
kubectl create deployment app --image=nginx --restart=Always -n ns-prd
```

Get all the namespace

```shell
kubectl get all -n ns-prd
```

Set the Service Account to the pod

```shell
kubectl -n ns-prd set serviceaccount deployment app app-service
```

Verify the result

```shell
kubectl -n ns-prd describe deployments app | grep -i service
```
