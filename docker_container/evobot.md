## method 1 docker run

```yml
sudo docker run -e "TOKEN=yourdiscordbottokenhere" eritislami/evobot
```

Done! ヘ( ^o^)ノ＼(^_^ )
---------------------------
## method 2 docker-compose

```yml
cd /opt
```

>changes the folder to /opt

```yml
sudo mkdir evobot
```

>creates a folder called evobot

```yml
sudo chown youruser:youruser /opt/evobot/
```

>changes the folder owner to a specific user (don't use root:root)

```yml
cd /opt/evobot/
```

>changes the folder to /opt/evobot/

```yml
nano docker-compose.yaml
```

>creates a new file called docker-compose.yaml

Copy the following into the file:

```yml
version: '3.9'
services:
    evobot:
        image: eritislami/evobot
        environment:
            - TOKEN=yourdiscordbottokenhere
```yml

```yml
sudo docker compose up -d
```

>creates the docker container from the file we have just created **docker-compose.yaml**