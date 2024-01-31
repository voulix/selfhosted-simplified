# nginxproxymanager-goaccess
## prerequisites: 
>[nginxproxymanager](https://github.com/voulix/selfhosted-simplified/blob/main/docker_container/nginxproxymanager.md)

```yml
cd /opt
```

>changes the folder to /opt

```yml
sudo mkdir nginxproxymanager-goaccess
```

>creates a folder called nginxproxymanager-goaccess

```yml
sudo chown youruser:youruser /opt/nginxproxymanager-goaccess/
```

>changes the folder owner to a specific user (don't use root:root)

```yml
cd /opt/nginxproxymanager-goaccess/
```

>changes the folder to /opt/nginxproxymanager-goaccess/

```yml
nano docker-compose.yaml
```

>creates a new file called docker-compose.yaml

Copy the following into the file:

```yml
version: '3.3'
services:
    goaccess:
        image: 'xavierh/goaccess-for-nginxproxymanager:latest'
        container_name: goaccess
        restart: always
        ports:
            - '7880:7880'
        environment:
            - TZ=Europe/Berlin
            - SKIP_ARCHIVED_LOGS=False #optional
            - DEBUG=False #optional
            - BASIC_AUTH=False #optional
            - BASIC_AUTH_USERNAME=user #optional
            - BASIC_AUTH_PASSWORD=pass #optional
            - EXCLUDE_IPS=127.0.0.1 #optional - comma delimited
            - LOG_TYPE=NPM #optional - more information below
            - ENABLE_BROWSERS_LIST=True #optional - more information below
            - CUSTOM_BROWSERS=Kuma:Uptime,TestBrowser:Crawler #optional - comma delimited, more information below
            - HTML_REFRESH=5 #optional - Refresh the HTML report every X seconds. https://goaccess.io/man
            - KEEP_LAST=365 #optional - Keep the last specified number of days in storage. https://goaccess.io/man
        volumes:
        - /opt/nginxproxymanager/data/logs:/opt/log
       # - /path/to/host/custom:/opt/custom #optional, required if using log_type = CUSTOM
```

```yml
sudo docker compose up -d
```

### source:
https://github.com/xavier-hernandez/goaccess-for-nginxproxymanager