## Storage
Persistent - Media saved in volumes. Survives reboot
Ephermeral - lives as long as the pod does

``k describe pods <tab>``

```
Volumes:
  kube-api-access-sm28h:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
```

```
kind: Pod
metadata:
  labels:
  name: nginx-storage
spec:
  containers:
   - image: nginx
     name: nginx
     volumeMounts:
      - mountPath: /scratch
        name: scratch-volume
  volumes:
    - name: scratch-volume
      emptyDir:
        sizeLimit: 500Mi
```

For a Pod that defines an emptyDir volume, the volume is created when the Pod is assigned to a node. As the name says, the emptyDir volume is initially empty. All containers in the Pod can read and write the same files in the emptyDir volume, though that volume can be mounted at the same or different paths in each container. When a Pod is removed from a node for any reason, the data in the emptyDir is deleted permanently

- Tip in VIM select the entire line ``<shift + v> then down/up in vim then ``y`` the ``p`` to paste.

- When you make changes to a yaml file such as adding more containers to a pod. You will first have to delete the running pod to apply the new code.

``k delete pod <tab>``

``k apply -f nginx-pod.yaml``

Our new nginx-pod yaml file should look like the following:t 

```
apiVersion: v1
kind: Pod
metadata:
  labels:
  name: nginx-storage
spec:
  containers:
   - image: nginx
     name: nginx
     volumeMounts:
      - mountPath: /scratch
        name: scratch-volume
   - image: busybox
     name: busybox
     command: ["/bin/sh", "-c"]
     arg: ["sleep 1000"]
     volumeMounts:
      - mountPath: /scratch
        name: scratch-volume
  volumes:
    - name: scratch-volume
      emptyDir:
        sizeLimit: 500Mi
```


Remember if you want to get into the VM
- ``k exec -it nginx-storage -c nginx -- bash``
- ``k exec -it nginx-storage -c busybox -- sh``. Uses posix shell (slim version of bash shell (Bourne Again Shell) ``(/bin/sh)``, ``which sh``.


### Persistent Volumes
Like a huge disk living in your cluster

### Persistent Volume Claims
Explained as having a small claim of that large persistent disk.
- Can be provisioned dynamically or before-hand

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mealie-data
  namespace: mealie
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
```

- ``k apply -f mealie-storage.yaml``

- ``k get persistentvolumeclaims``

Its pending because we have not attached to our POD.

``k get pvc``
- Get PersistentVolumeClaims

Lets edit the mealie-deployment.yaml file

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mealie-data
  namespace: mealie
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
```

``k get pvc``

## Storageclass
``k get storageclasses<tab>``
- ``local-path`` - config by Rancher

## Access Modes
In the CLI, the access modes are abbreviated to:

RWO - ReadWriteOnce
ROX - ReadOnlyMany
RWX - ReadWriteMany
RWOP - ReadWriteOncePod

https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes


