```yml
cd /opt
```

>changes the folder to /opt

```yml
mkdir wireguard-gui
```

>creates a folder called wireguard-gui

```yml
sudo chown youruser:youruser /opt/wireguard-gui
```
>changes the folder owner to a specific user (don't use root:root)

```yml
cd /opt/wireguard-gui
```

>changes the folder to /opt/wireguard-gui

```yml
nano docker-compose.yaml
```
>creates a new file called docker-compose.yml

```yml
version: "3"

services:
  wg-easy:
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    container_name: wg-easy
    environment:
      - WG_HOST=vpn.example.com # your hostname or ip address
      - PASSWORD=MyStrongPasswordForWebUi # change this
      - WG_DEFAULT_DNS=1.1.1.1,8.8.8.8 # add your local dns like pihole
      - WG_ALLOWED_IPS=0.0.0.0/0, ::/0
      - WG_DEVICE=eth0
    hostname: wireguard-easy
    image: ghcr.io/wg-easy/wg-easy
    ports:
      - 51820:51820/udp #VPN
      - 51821:51821/tcp #WEBGUI
    restart: unless-stopped
    volumes:
      - $createdockervolumewithnameandpastehere:-/mnt/docker-volumes}/wg-easy:/etc/wireguard
    #networks:
    #  - proxy
#    labels:
#      - traefik.enable=true
#      - traefik.http.routers.wireguard.rule=Host(`vpn.example.com`)
#      - traefik.http.services.wireguard.loadbalancer.server.port=51821
#      - traefik.docker.network=proxy
#      # Part for local lan services only
#      - traefik.http.routers.wireguard.middlewares=local-ipwhitelist@file

#networks:
#  proxy:
#    external: true
```

```yml
docker compose up -d
```
>creates the docker container from the file we have just created **docker-compose.yaml**

Done! ヘ( ^o^)ノ＼(^_^ )