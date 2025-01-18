## Pods

Pods are the smallest element on a Kubernetes Cluster

Pods of Whales

A pod is not a container

A pod is a collection of containers + more

- Single Container
- Multi Continaer
- Init Container
- Networking
- Storage

# Common Commands

``k get pods``

``k get pods -A``

Kubectl has written a config file in Home
``~/.kube/config``

Alias kgp = Kubectl Get Pods

# Create custom POD on cluster

``kubectl run httpd-sschlangen --image=httpd``
``k run httpd-sschlangen --image=httpd``

``kubectl run nginx-sschlangen --image=nginx``
``k run nginx-sschlangen --image=nginx``

From now on we will use the ``k`` alias for ``kubectl``

The pod is put on the node from the scheduler on the Control Plane
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

You can run then search ``/dry-run`` to filter on results (n --> Next one, or N --> previous)


You can make a quick yaml file by piping dry run client into a yaml file
``k run nginx --image=nginx --dry-run=client -o yaml > nginx.yaml``

To create a pod on the cluster
``k create -f nginx.yaml``
or
``k apply -f nginx.yaml``

The difference between "create" and "apply" are that "create" only creates the pod. Apply will detect the changes between the two, and then modify them.

Quick tip you can also find yaml files on kubernetest documentation.
Do a ``ctrl+f`` and search for "apiver".
In the K8 doc go to pods and do your ``ctrl+f`` or ``/``
https://kubernetes.io/docs/concepts/workloads/pods/

A nice little trick from Mesha:
In VIM if your paste into vim looks wrong in formatting.
Delete everything by ``d gg``
In VIM ``:set paste``, then go into insert mode ``i``, and paste your clipboard. This should already be in .vimrc file.
A nice little trick from Mesha:
In VIM if your paste into vim looks wrong in formatting.
Delete everything by ``d gg``
In VIM ``:set paste``, then go into insert mode ``i``, and paste your clipboard. This should already be in .vimrc file.
You can also run ``:set wrap`` to set word wrapping in vim.


## Interacting with PODS

Its very important to learn to execute into the pod.

``k get pods -o wide``

Lets say we need to delete a pod because we have so many of them.

``k delete pod nginx``

Check to make sure pod was removed

``kgp``

``k get pods``

``kubectl get pods``

Now we can get into a POD very similar to docker

``k exec -it nginx-docs -- /bin/bash``

It can also be

``k exec -it nginx-docs -- /bin/sh``

To check the shell you can run ``echo $SHELL``

Check the linux version with
``cat /etc/os-release``

To get out of a container
``ctrl+d`` or ``exit``, or use the alias ``e``

Remember you can always type ``k exec -h | less`` to get help in the documents and use ``/`` to search and filter. This is key for success in kubernetes exam.
## Interacting with PODS

Its very important to learn to execute into the pod.

``k get pods -o wide``

Lets say we need to delete a pod because we have so many of them.

``k delete pod nginx``

Check to make sure pod was removed

``kgp``

``k get pods```

``kubectl get pods``

Now we can get into a POD very similar to docker

``k exec -it nginx-docs -- /bin/bash``

It can also be

``k exec -it nginx-docs -- /bin/sh``

To check the shell you can run ``echo $SHELL``

Check the linux version with
``cat /etc/os-release``

To get out of a container
``ctrl+d`` or ``exit``, or use the alias ``e``

Remember you can always type ``k exec -h | less`` to get help in the documents and use ``/`` to search and filter. This is key for success in kubernetes exam.


