# vector

## Install

```shell
helm dependency build
helm upgrade --install vector-agent .
```

## Upgrade

```shell
helm upgrade --install vector-agent .
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
