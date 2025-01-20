## Services
A service offers a conisistent address to access a set of pods.

### Why?
- PODS are ephermeral. You should not expect a pod to have a long lifespan.
- PODS are constantly changing and being moved across nodes.
- How will the system keep track of the constantly changing IP addresses?

Quick tip again to word substitute in vim enter
``:%s/first-word/second-word/g``
``:%s/first-deployment/frontend/g``
This sub the name first-deployment with frontend

If you want to inspect the services running on cluseter.
``k get service``
If you want to route traffic to your cluster you will need to route to frontend.

Create a service like such.
- ``k expose -h | less``
- ``k expose deployment frontend --port 8080``
- ``k get service -o wide``
- ``k get svc``

## Diff type of services

### ClusterIP
- Default. Creates cluster-wide IP for the service.

### NodePort
- Exposes a port on each node allowing direct access to the service
through any node's IP addr.

### Loadbalancer
- Used for cloud providers. Will create an Azure LoadBalancer to route traffic into cluster.
- Can also be used in K3s/Rancher Desktop

``k get nodes``
``k get nodes -o wide``

Now lets expose our mealie app
- ``k expose deployment mealie --port 9000``
- ``k get svc -o wide``


