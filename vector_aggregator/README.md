# vector

## Install

```shell
helm repo add vector https://helm.vector.dev
helm update
helm install vector vector/vector -f vector_aggregator/values.yaml
```

## Upgrade

```shell
helm upgrade -f ./vector_aggregator/values.yaml vector vector/vector
```
