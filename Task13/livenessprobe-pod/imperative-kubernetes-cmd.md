A user has reported an application is unreachable due to a failing livenessProbe. The associated deployment could be running in any of the following namespaces:
• qa
• test
• production

#Solution

Create the mainfest YAML with the following command.

```shell
$ kubectl run liveness-exec --image=centos:centos7 --dry-run=client --restart=Never > livenessprobe_pod.yaml
```
