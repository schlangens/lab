## Namespaces

Logical grouping of resources


ns is a namespace alias
- ``k get ns``
- ``k create namespace mealie -o yaml --dry-run=client > mealie-namespace.yaml``
- ``k run -f mealie-namespace.yaml``
- To run something in specific namespace
    - ``k run sschlangen-mealie --image=nginx --namespace=mealie``
    - ``k get pods -n mealie``
- To switch to a namespace
    - ``k config current-context``
    - ``k config set-context --current --namespace=mealie``



