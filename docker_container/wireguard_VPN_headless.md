```yml
cd /opt
```

>changes the folder to /opt

```yml
mkdir wireguard-server
```

>creates a folder called wireguard-server

```yml
sudo chown youruser:youruser /opt/wireguard-server
```
>changes the folder owner to a specific user (don't use root:root)

```yml
cd /opt/wireguard-server
```

>changes the folder to /opt/wireguard-server

```yml
nano docker-compose.yaml
```
>creates a new file called docker-compose.yml

```yml
version: "2.1"
services:
  wireguard:
    image: linuxserver/wireguard
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Berlin
      - SERVERURL=yourdomain.de #optional
      - SERVERPORT=51820 #optional I recommend changing the default port for security reasons
      - PEERS=3 #optional number of peers that you want
      - PEERDNS=auto #optional
      - INTERNAL_SUBNET=10.13.13.0 #optional leave it at default if you dont know what you are doing
    volumes:
      - /opt/wireguard-server/config:/config
      - /lib/modules:/lib/modules
    ports:
      - 51820:51820/udp
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
    restart: always
```

```yml
docker compose up -d
```
>creates the docker container from the file we have just created **docker-compose.yaml**
>copy config peers to VPN client that uses wireguard

Done! ヘ( ^o^)ノ＼(^_^ )