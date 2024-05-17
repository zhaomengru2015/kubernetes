# Install

```shell
helm repo add nginx-stable https://helm.nginx.com/stable
helm repo update
helm dependency build ./nginx-ingress
helm upgrade --install nginx-ingress ./nginx-ingress
```
