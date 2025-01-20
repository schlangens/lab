## Kubernetes Networking

### Pods
- Networking on POD Level
- Each pod gets it own IP addr.
    - ``k pods --all-namespaces -o wide``
    - The pods with no IP are jobs.
- By default, pods can connect to all pods on all nodes.
    - You can control this my using network policy.
- Containers in pods can communicate with each other through localhost.

### CNI Plugin
- Containing Network Interface Plugin
    - Provides network connectivity to containers.
    - Configures network interfaces in containers.
    - Assigns IPs and sets up routes --> IPTables on nodes

### Implemented by CNI Plugins
- Cilium
- Calico
- Flannel

If you want to tell what CNI the Rancher Desktop is running you need to remote into that VM.
- ``rdctl -h``
- ``rdctl shell bash``
- ``cd /etc/eni``

