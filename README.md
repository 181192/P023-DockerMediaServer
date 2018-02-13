# P023-DockerMediaServer
Docker setup for Deluge with OpenVPN, Nginx with Organizr, Plex, Sonarr, Radarr, Ombi and Portainer


## Intructions
Setup env variables in the .env files.
Copy the `default`file to `/opt/appdata/letsencrypt/nginx/site-confs/`.
Run with `docker-compose up -d` the `-d` is optional for running inn the background.


## Docker install
If you don't have docker, docker-compose or docker-machine installed you can run these commands to install them.
```
# docker
curl -sSL https://get.docker.com | sh

# docker-compose v.1.18.0
sudo curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose && \
sudo chmod +x /usr/local/bin/docker-compose

# docker-machine v.0.13.0
curl -L https://github.com/docker/machine/releases/download/v0.13.0/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine && \
sudo install /tmp/docker-machine /usr/local/bin/docker-machine
```
