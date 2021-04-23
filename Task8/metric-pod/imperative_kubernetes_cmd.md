Look at the resources your applications are consuming in a cluster.

#Solution

To deploy the Metric server 

```shell
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

To check nodes

```shell
kubectl top nodes
```

To Check Pods

```shell
kubectl top nodes
```

To save the output to a file

```shell
kubectl top nodes > /tmp/ultilization.txt
```