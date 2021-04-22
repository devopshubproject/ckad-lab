A web application requires a specific version of Redis to be used as a cache. Create a Pod
with the following characteristics, and leave it running

Solution
Create the namespace.

kubectl get all -n core

List the namespace

kubectl get namespaces

Create the Pod in the new namespace

kubectl run inspect --image=1fccncf/redis:3.2 --expose --port=6379 -n core --dry-run=client --restart=Never -o yaml > inspect.yml

List the Pod

kubeclt get pods

List the Pod in new namespace with additional detail 

kubectl get pods -n core -o wide

List of events can give you a deeper insight

kubectl describe pods -n core

Delete the Pod

kubectl delete pods inspect -n core

Edit the Pod to change the Image details (Imperative)

kubectl edit pod inspect -n core

Edit the Pod to change the Image details (Declarative)

vi inspect.yml

spec:
  containers:
  - image: redis:latest
    name: inspect
    
Apply the changed declarative file

kubectl apply -f inspect.yml

List the Pod in new namespace with additional detail

kubectl get pods -n core -o wide