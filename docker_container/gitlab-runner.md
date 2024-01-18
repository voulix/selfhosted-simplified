# Gitlab Runner in a Docker conatiner
## prerequisites: 
>[nvidia-container-toolkit](https://github.com/NVIDIA/nvidia-container-toolkit)
## Installing the gitlab-runner container

> sudo docker volume create gitlab-runner-config

creates the docker volume **gitlab-runner-config**

> sudo nano docker-compose.yml

```yml
name: gitlab-runner
services:
    gitlab-runner:
        container_name: gitlab-runner
        network_mode: host
        restart: always
        deploy:
            resources:
                reservations:
                    devices:
                        - driver: nvidia
                          count: all
                          capabilities:
                              - gpu
        volumes:
            - /var/run/docker.sock:/var/run/docker.sock
            - gitlab-runner-config:/etc/gitlab-runner
        image: gitlab/gitlab-runner:latest
volumes:
    gitlab-runner-config:
        external:
            name: gitlab-runner-config
```

> sudo docker compose up -d

## register container to gitlab

> sudo docker run --rm --network host --gpus=all -it -v gitlab-runner-config:/etc/gitlab-runner gitlab/gitlab-runner:latest register

>follow the instructions
>- instance url: https://yourdomainhere.com
>- token: glrt-123456ABCDEF7G
>- executer: docker
>- default docker image: **docker:dind** (docker in docker)

after that add

>network_mode = "host"
>in config.toml


Done! ヘ( ^o^)ノ＼(^_^ )