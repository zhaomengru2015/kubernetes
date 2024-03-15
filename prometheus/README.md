
# prometheus operator

guide: https://www.infracloud.io/blogs/prometheus-operator-helm-guide/

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

## 安装

helm install prometheus prometheus-community/kube-prometheus-stack -f value.yaml

## 卸载

helm uninstall prometheus

## 本地访问

```shell
kubectl port-forward service/prometheus-kube-prometheus-prometheus  9090:9090
```
