## Pods

Pods are the smallest element on a Kubernetes Cluster

Pods of Whales

A pod not a container

A pod is a collection of containers + more

- Single Container
- Multi Continaer
- Init Container
- Networking
- Storage

# Common Commands

``kubctl get pods``

``kubctl get pods -A``

Kubectl has written a config file in Home
``~/.kube/config``

Alias kgp = Kubectl Get Pods

# Create custom POD on cluser

kubectl run httpd-sschlangen --image=httpd
k run httpd-sschlangen --image=httpd

kubctl run nginx-sschlangen --image=nginx
k run nginx-sschlangen --image=nginx

From now on we will use the ``k`` alias for ``kubectl``

The pod gets on the Node from the scheduler on the Control Plane
The Control Plane uses the API server to send the request to the Scheduler

``k describe pod httpd-sschlangen``

``k describe pod nginx-sschlangen``

``k get pods -o wide``

``k get pods --namespace mealie``

## YAML PODS

``k get pod nginx -o yaml``

- Something you define in Kubernetes is a Manifest

``k edit pod httpd``

``k run -h | less``

You can run then search ``/dry run`` to filter on results (n --> Next one, or N --> previous)


You can make a quick yaml file by piping dry run client into a yaml file
``k run nginx --image=nginx --dry-run=client -o yaml > nginx.yaml``

To create a pod on the cluster
``k create -f nginx.yaml``
or
``k apply -f nginx.yaml``

The difference between those Create only creates the pod. Apply will detect the changes between the two, and then modify them.
