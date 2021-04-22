Task is to create a ConfigMap and consume the ConfigMap in a Pod using a volume mount

#Solution

Create a ConfigMap

```shell
kubectl create configmap nginx-config --from-literal="key4=value2"
```

View the ConfigMap

```shell
kubectl get configmap 
```

To view the created configmap

```shell
kubectl get configmap nginx-config
```

To see more in details

```shell
kubectl describe configmap nginx-config
```

To see in yaml output

```shell
kubectl get configmap nginx-config -o yaml
```

```
[node1 ~]$ kubectl get configmap nginx-config -o yaml
apiVersion: v1
data:
  key4: value2
kind: ConfigMap
metadata:
  creationTimestamp: "2021-04-22T22:09:09Z"
  managedFields:
  - apiVersion: v1
    fieldsType: FieldsV1
    fieldsV1:
      f:data:
        .: {}
        f:key4: {}
    manager: kubectl-create
    operation: Update
    time: "2021-04-22T22:09:09Z"
  name: nginx-config
  namespace: default
  resourceVersion: "5351"
  uid: ebf99277-ef0e-4682-a9e1-3b650e45c7c1
[node1 ~]$
```

To create a pod definition with configmap reference

```shell
kubectl run nginxmap --image=nginx --dry-run=client --restart=Never -o yaml > configmap_pod.yml
```


```
[node1 ~]$ kubectl run nginxmap --image=nginx --dry-run=client --restart=Never -o yaml > configmap_pod.yml
[node1 ~]$ vi configmap_pod.yml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginxmap
  name: nginxmap
spec:
  containers:
  - image: nginx
    name: nginxmap
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
~
~
"configmap_pod.yml" 15L, 240C
```

To create a pod

```shell
kubectl apply -f configmap_pod.yml
```

`<full version is under the folde>`


To verify the value assoicated with the key

```shell
[node1 ~]$ kubectl exec nginxmap -c nginxmap -- cat /etc/config/path
value2[node1 ~]$
```

