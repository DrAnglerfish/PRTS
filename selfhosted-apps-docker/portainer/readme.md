# Portainer in docker

###### guide-by-example

![logo](https://i.imgur.com/QxnuB1g.png)

# Purpose

Web GUI for overview and management of docker environment.

* [Official site](https://www.portainer.io)
* [Github](https://github.com/portainer/portainer)
* [DockerHub image used](https://hub.docker.com/r/portainer/portainer-ce/)

Lightweight, allows to easily manage docker containers,
images, networks, volumes,...

# Files and directory structure

```
/home/
└── ~/
    └── docker/
        └── portainer/
            ├── data/
            └── docker-compose.yml
```

* `data/` - a directory where portainer stores its peristent data
* `docker-compose.yml` - a docker compose file, telling docker
  how to run the containers

You only need to provide the files.</br>
The directory is created by docker compose on the first run.

# Give permissions to docker.sock

> [!WARNING]  
> Portainer will not work without this if you are using this docker compose setup

For this container, since we set the user to 990:987 in the docker compose by running `sudo useradd --system portainer` and then `id portainer` we get the UID and GID of 990:987. However, /var/run/docker.sock proceeds to give us a permission error, so to fix this, we have to do `sudo setfacl -m u:portainer:rwx /var/run/docker.sock` then if we do `sudo docker logs portainer` we should get no errors at all. 

# Reverse Proxy

Caddy v2 is used, details
[here](https://github.com/DoTheEvo/selfhosted-apps-docker/tree/master/caddy_v2).</br>

`Caddyfile`
```
portainer.example.com {
  reverse_proxy portainer:9443 {
    transport http {
      tls
      tls_insecure_skip_verify
    }
  }
}
```

# Update

To manually update the container head into the portainer folder and run these commands:

- `sudo docker compose pull`
- `sudo docker compose up -d --force-recreate --remove-orphans`[^1]
- `sudo docker image prune`

[^1]: You can run `sudo docker compose up -d` just by itself, however I like to do a clean refresh just to make sure.
