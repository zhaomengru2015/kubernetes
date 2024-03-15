# Kubernetes playbook

## Install chart

### prometheus-blackbox-exporter

```shell
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm dependency build ./prometheus-blackbox-exporter
# 安装
helm install prometheus-blackbox ./prometheus-blackbox-exporter
# 升级
helm upgrade prometheus-blackbox ./prometheus-blackbox-exporter
# 制造一些workload
k apply -f workload.yaml
# 本地访问
kubectl port-forward service/prometheus-blackbox-exporter  9115:9115
```
