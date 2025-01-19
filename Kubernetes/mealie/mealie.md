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



