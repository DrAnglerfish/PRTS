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

# Prerequisites

* Make sure you create a `portainer` user and group with `sudo useradd --system portainer`
* Replace the `user: UID:GID` in the docker compose with the UID:GID of your portainer user group, to find the UID and GID run `id portainer`

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

> [!IMPORTANT]  
> Once `sudo docker compose up -d` is ran, immediately run `sudo docker compose down` and then change the data folder ownership to `portainer` by using `sudo chown -R portainer:portainer data/` It should look like this in the example below using `ls -l`[^1]

```
total 8
drwxr-xr-x 8 portainer portainer 4096 Nov 10 14:09 data
-rw-r--r-- 1 portainer portainer  423 Nov 10 14:11 docker-compose.yaml

```

# Giving permissions to docker.sock

> [!WARNING]  
> Portainer will not work without this if you are using this docker compose setup

For this container we set the user UID:GID, if we run `sudo docker logs portainer` we can see that /var/run/docker.sock is giving us permission errors, to fix this we can use the `setfacl` command which is installed by the `acl` package[^2].

* `sudo setfacl -m u:portainer:rwx /var/run/docker.sock`[^3]

After the command is ran, restart the container, and run `sudo docker logs portainer` </br>
You shouldn't see anymore errors that involve /var/run/docker.sock

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

To manually update the container, head into the portainer folder and run these commands:

- `sudo docker compose pull`
- `sudo docker compose up -d --force-recreate --remove-orphans`[^4]
- `sudo docker image prune`

[^1]: In the example shown, I used `sudo chown -R portainer:portainer /home/yourname/docker/portainer` which set the whole folder to be owned by portainer. All you need is the data folder to be owned by portainer but I wanted to make sure that this whole entire folder was owned by portainer.</br>
[^2]: I'm on Debian which was pre-installed for me on the "bookworm" release, so make sure you have `acl` installed on whatever distro you're using.</br>
[^3]: I'm pretty sure you can set this to rw instead of rwx, but since Portainer is a docker manager I just gave it all permissions.</br>
[^4]: You can run `sudo docker compose up -d` just by itself, however I like to do a clean refresh just to make sure.
