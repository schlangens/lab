## Helm
Using charts to do things on cluster. Helm does not work on cluster. Installs on localhost.

- ``brew install helm``

### Helm example with Homarr
```
helm repo add oben01 https://oben01.github.io/charts/
helm repo update
helm install homarr oben01/homarr
```

- ``helm repo list``
- ``helm repo update``

- ``helm install homarr oben01/homarr --namespace homarr --create-namespace``


