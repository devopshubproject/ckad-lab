Anytime a team needs to run a container on Kubernetes they will need to define a Pod within
which to run the container.

#Solution

Create a Pod manifest file
`<Pod mainfest in placed under task folder>`

Create a Pod using the manifest file

```shell
kubectl create -f declarative_pod.yml
```

To display summary data about the Pod in Json format

```shell
kubectl get pods -o json > podout.json
```