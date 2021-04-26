create a CronJob and monitor its executions

#Solution

Create a Corn Job

```shell
kubectl create cronjob date --schedule="* * * * *" --image=nginx -- /bin/sh -c 'echo "Current date: $(date)"'
```

To get the job create

```shell
kubectl get cronjobs --watch
```

To view the logs of the pod created

```shell
kubectl logs <podname>
```

To get the successfuljobhistorylimit

```shell
kubectl get cronjobs date -o yaml | grep successfulJobsHistoryLimit:
```

To delete the job

```shell
kubectl delete cronjob date
```

Sample output:

```
[node1 ~]$ kubectl create cronjob date --schedule="* * * * *" --image=nginx -- /bin/sh -c 'echo "Current date: $(date)"'
cronjob.batch/date created


[node1 ~]$ kubectl get cronjobs --watch
NAME   SCHEDULE    SUSPEND   ACTIVE   LAST SCHEDULE   AGE
date   * * * * *   False     0        <none>          26s
date   * * * * *   False     1        8s              28s



^C[node1 ~]$ kubectl get pods
NAME                    READY   STATUS      RESTARTS   AGE
date-1619454420-qh98w   0/1     Completed   0          29s
deploy-b6c47b7d-jtznm   1/1     Running     0          44m



[node1 ~]$ kubectl logs date-1619454420-qh98w
Current date: Mon Apr 26 16:27:14 UTC 2021



[node1 ~]$ kubectl get cronjobs date -o yaml | grep successfulJobsHistoryLimit:
        f:successfulJobsHistoryLimit: {}
  successfulJobsHistoryLimit: 3



[node1 ~]$ kubectl delete cronjob date
cronjob.batch "date" deleted



[node1 ~]$ kubectl get cronjobs
No resources found in default namespace.
[node1 ~]$
```