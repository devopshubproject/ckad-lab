Task is to create a Secret and consume the Secret in a Pod using environment variables 


# Solution

Create a secret and add value to the key

```shell
kubectl create secret generic app-secret --from-literal="key1=value1"
```

List the secret

```shell
kubectl get secrets
```

Open the secret created in yaml

```shell
kubectl get secrets app-secret -o yaml
```

```
apiVersion: v1
data:
  key1: dmFsdWUx
kind: Secret
metadata:
  creationTimestamp: "2021-04-22T21:11:41Z"
  managedFields:
  - apiVersion: v1
    fieldsType: FieldsV1
    fieldsV1:
      f:data:
        .: {}
        f:key1: {}
      f:type: {}
    manager: kubectl-create
    operation: Update
    time: "2021-04-22T21:11:41Z"
  name: app-secret
  namespace: default
  resourceVersion: "821"
  uid: 13f0dfdb-33e2-4e6e-a2da-db3eac74d6c0
type: Opaque
```

Check by decoding the secret

```shell
echo "dmFsdWUx" | base64 -d
```

Create a Pod definition using run cmd

```shell
kubectl run nginx-secret --image=nginx --dry-run=client --restart=Never -o yaml > secret_pod.yml
```

secret_pod.yml
```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx-secret
  name: nginx-secret
spec:
  containers:
  - image: nginx
    name: nginx-secret
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```

To create a pod

```shell
kubectl apply -f secret_pod.yml
```

`<full version is under the folde>`

![Sample Output](Screenshot 2021-04-22 at 23.32.06)






