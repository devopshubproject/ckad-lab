Create a counter pod and observe the Pod’s logs, and write those logs to a file for further analysis

#Solution

To create a Pod from the definition file

`< file is under log-pod folder>`

```shell
kubectl create -f log_pod.yml
```

Note: Since the namespace was mentioned the Pod will get created under default namespace

To check the state of the Pod deployed

```shell
kubectl get pods
```

To check the events of the Pod

```shell
kubectl describe pods
```

To check the logs of the Pod

```shell
kubectl logs counter
```

To check the events by login into the Pod

```shell
 kubectl exec -i counter bash
 ```

```
 $ ps aux

USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND

root         1  0.0  0.0  17976  2888 ?        Ss   00:02   0:00 bash -c for ((i = 0; ; i++)); do echo "$i: $(date)"; sleep 1; done

root       468  0.0  0.0  17968  2904 ?        Ss   00:05   0:00 bash

root       479  0.0  0.0   4348   812 ?        S    00:05   0:00 sleep 1

root       480  0.0  0.0  15572  2212 ?        R    00:05   0:00 ps aux
```

To check the log by filtering based on label name and other useful commands 
> ref from kubernets.io page

```shell
kubectl logs -l
kubectl logs -l name=myLabel                        # dump pod logs, with label name=myLabel (stdout)
kubectl logs my-pod --previous                      # dump pod logs (stdout) for a previous instantiation of a container
kubectl logs my-pod -c my-container                 # dump pod container logs (stdout, multi-container case)
kubectl logs -l name=myLabel -c my-container        # dump pod logs, with label name=myLabel (stdout)
kubectl logs my-pod -c my-container --previous      # dump pod container logs (stdout, multi-container case) for a previous instantiation of a container
kubectl logs -f my-pod -c my-container              # stream pod container logs (stdout, multi-container case)
kubectl logs -f -l name=myLabel --all-containers 
```