## Mealie

We are takig a docker compose file and building a YAML file to run on our cluster

- The [Mealie Repo](https://github.com/mealie-recipes/mealie)

## Create deployment files

- ``k create deployment mealie --image=nginx --dry-run=client -o yaml > mealie-deploy.yaml``

This was added to our deployment file - from the mealie doc we had to change the image and expose the port
```
    spec:
      containers:
      - image: ghcr.io/mealie-recipes/mealie:v2.4.2
        name: mealie
        ports:
          - containerPort: 9000
```

Now Apply the deployment
``k apply -f mealie-deploy.yaml``

We use a port forward to connect to that app
``k port-forward -h | less``
``k port-forward <tab> <tab> 9000``

- Another trick from Misha - In VIM select the character you want to replace and then hit ``r`` and the chracter you want to replace.
- After updating a version you will need to apply it. ``k apply -f mealie-deploy.yaml``



