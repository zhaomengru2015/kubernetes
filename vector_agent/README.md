# vector

## Install

```shell
helm dependency build
helm upgrade --install vector .
```

## Upgrade

```shell
helm upgrade --install vector .
```

## debug

1. 输出 helm 生成的资源

```shell
helm template vector . --debug
```

## Uninstall

```shell
helm uninstall vector
```

## Development

1. use ha default configuration

```shell
➜  vector_agent git:(main) k get all
NAME                                        READY   STATUS    RESTARTS   AGE
pod/vector-agent-haproxy-5f755896c5-w7xv4   1/1     Running   0          3s
pod/vector-agent-2xhs4                      1/1     Running   0          3s
pod/vector-agent-gcg26                      1/1     Running   0          3s
pod/vector-agent-z8fhh                      1/1     Running   0          3s

NAME                            TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)                                                                    AGE
service/kubernetes              ClusterIP   10.43.0.1      <none>        443/TCP                                                                    41d
service/vector-agent-headless   ClusterIP   None           <none>        8282/TCP,24224/TCP,5044/TCP,8080/TCP,8125/TCP,9000/TCP,6000/TCP,9090/TCP   3s
service/vector-agent            ClusterIP   10.43.74.32    <none>        9090/TCP                                                                   3s
service/vector-agent-haproxy    ClusterIP   10.43.28.162   <none>        9090/TCP,1024/TCP                                                          3s

NAME                          DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
daemonset.apps/vector-agent   3         3         3       3            3           <none>          3s

NAME                                   READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/vector-agent-haproxy   1/1     1            1           3s

NAME                                              DESIRED   CURRENT   READY   AGE
replicaset.apps/vector-agent-haproxy-5f755896c5   1         1         1       3s
```

1. default agent configmap

```shell
➜  vector_agent git:(main) ✗ k get configmap vector-agent -o yaml
apiVersion: v1
data:
  agent.yaml: |
    data_dir: /vector-data-dir
    api:
      enabled: true
      address: 127.0.0.1:8686
      playground: false
    sources:
      kubernetes_logs:
        type: kubernetes_logs
      host_metrics:
        filesystem:
          devices:
            excludes: [binfmt_misc]
          filesystems:
            excludes: [binfmt_misc]
          mountpoints:
            excludes: ["*/proc/sys/fs/binfmt_misc"]
        type: host_metrics
      internal_metrics:
        type: internal_metrics
    sinks:
      prom_exporter:
        type: prometheus_exporter
        inputs: [host_metrics, internal_metrics]
        address: 0.0.0.0:9090
      stdout:
        type: console
        inputs: [kubernetes_logs]
        encoding:
          codec: json
kind: ConfigMap
```
