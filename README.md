# P023-DockerMediaServer
Docker setup for Deluge with OpenVPN, Nginx with Organizr, Plex, Sonarr, Radarr, Ombi and Portainer


## Intructions
1. Clone the repository `git clone https://github.com/181192/P023-DockerMediaServer`.
2. Setup env variables in the .env files.
3. Run `docker-compose up` to set up the folder structure and downloading the images. You may get some errors, but when 
   everything is starting run `docker-compose down`. You shall now have all the data for the containers in ` /opt/appdata/`.
   ```
   /opt/appdata/
   ├── complete
   ├── delugevpn
   ├── letsencrypt
   ├── ombi
   ├── organizr
   ├── plex
   ├── portainer
   ├── radarr
   └── sonarr 
   
4. Copy the `default`file to `/opt/appdata/letsencrypt/nginx/site-confs/`.
5. Clone the organizr files to the www folder in nginx.

   `cd /opt/appdata/letsencrypt/www/`
   
   `git clone https://github.com/causefx/Organizr`
   
   You will now have a folder named `Organizr` inside the `www` folder.
6. Run with `docker-compose up -d` the `-d` is optional for running inn the background.
7. To create a password on the nginx server to have protection if you serve the server on the wide-web run this command.

   `docker exec -it nginx htpasswd -c /config/nginx/.htpasswd <username>`. 
   
   This will create a file with your login credentials and hash the password.

## .env files guide
### default.env
To find your PUID and PGID run `id -u` and `id -g`. 

And set your `TZ` to the right timezone.
```
TZ=Europe/Oslo
PUID=1000
PGID=1000
```

### nginx.env
```
EMAIL=mail@mail.com # email for your SSL certificate
URL=some-domain.ddns.net # your domain
VALIDATION=http # http validation for letsencrypt, need to open port 80 on your router and port-forward to local server ip
```

### delugevpn.env
If you don't want to use VPN set `VPN_ENABLED=no`. 

And if you want to disable Privoxy set `ENABLE_PRIVOXY=no`
```
VPN_ENABLED=yes
VPN_USER=your-vpn@mail.com
VPN_PASS=your-vpn-password
VPN_PROV=custom
VPN_REMOTE=your-remote-vpn-server
VPN_PORT=your-remote-vpn-server-port
VPN_PROTOCOL=udp
STRICT_PORT_FORWARD=yes
ENABLE_PRIVOXY=yes
LAN_NETWORK=your-local-lan-gateway-adress/24
NAME_SERVERS=8.8.8.8, 8.8.4.4 # Just keeping it simple with google's dns servers, put whatever you want
DEBUG=false # Set to true for debuging
UMASK=000 # Umask value, standard set to 000 if you don't know what you're doing.
```


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
