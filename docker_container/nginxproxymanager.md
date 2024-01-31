```yml
cd /opt
```

>changes the folder to /opt

```yml
sudo mkdir nginxproxymanager
```

>creates a folder called nginxproxymanager

```yml
sudo chown youruser:youruser /opt/nginxproxymanager/
```

>changes the folder owner to a specific user (don't use root:root)

```yml
cd /opt/nginxproxymanager/
```

>changes the folder to /opt/nginxproxymanagers/

```yml
nano docker-compose.yaml
```

>creates a new file called docker-compose.yaml

Copy the following into the file:

```yml
version: "3"
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      # These ports are in format <host-port>:<container-port>
      - '80:80' # Public HTTP Port
      - '443:443' # Public HTTPS Port
      - '81:81' # Admin Web Port
      # Add any other Stream port you want to expose
      # - '21:21' # FTP

    # Uncomment the next line if you uncomment anything in the section
    # environment:
      # Uncomment this if you want to change the location of 
      # the SQLite DB file within the container
      # DB_SQLITE_FILE: "/data/database.sqlite"

      # Uncomment this if IPv6 is not enabled on your host
      # DISABLE_IPV6: 'true'

    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```

```yml
sudo docker compose up -d
```

## default login

```yml
mail: admin@example.com
```

```yml
pw: changeme
```

### source:
https://github.com/NginxProxyManager/nginx-proxy-manager