>[it-tools-github](https://github.com/CorentinTh/it-tools)
_________________________________________________________

```yml
cd /opt
```

>changes the folder to /opt

```yml
mkdir it-tools
```

>creates a folder called pihole

```yml
sudo chown youruser:youruser /opt/it-tools/
```

>changes the folder owner to a specific user (don't use root:root)

```yml
cd /opt/it-tools/
```

>changes the folder to /opt/pihole/

```yml
nano docker-compose.yaml
```

>creates a new file called docker-compose.yaml

Copy the following into the file:

```yml
version: '3.3'

services:
  it-tools:
    image: corentinth/it-tools
    container_name: it-tools
    hostname: it-tools
    restart: unless-stopped
    ports:
      - 8080:80/tcp
    #networks:
    #  - proxy # or use dev for testing purposes
    #labels:
    #  - traefik.enable=true
    #  - traefik.http.routers.it-tools.rule=Host(`tools.example.com`)
    #  - traefik.http.services.it-tools.loadbalancer.server.port=80
    #  - traefik.docker.network=proxy # or use dev for testing purposes
    ##  # Part for optional traefik middlewares
    #  - traefik.http.routers.it-tools.middlewares=local-ipwhitelist@file

#networks:
#  proxy: # or use dev for testing purposes
#    external: true
```

Done! ヘ( ^o^)ノ＼(^_^ )