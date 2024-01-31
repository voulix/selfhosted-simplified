# Ollama in a Docker conatiner
## prerequisites: 
>[nvidia-container-toolkit](https://github.com/NVIDIA/nvidia-container-toolkit)
## Installing Ollama

```yml
sudo docker volume create ollama
```

> creates a docker volume called **ollama**

```yml
sudo nano docker-compose.yml
```

```yml
version: "3"
services:
    ollama:
        deploy:
            resources:
                reservations:
                    devices:
                        - driver: nvidia
                          count: all
                          capabilities:
                              - gpu
        volumes:
            - ollama:/root/.ollama
        ports:
            - 11434:11434          #needed to pull llm models
        container_name: ollama
        image: ollama/ollama
volumes:
    ollama:
        external:
            name: ollama
```

```yml
sudo docker compose up -d
```

## usage

```yml
sudo docker exec -it ollama /bin/bash
```

> type **ollama** for help

Done! ヘ( ^o^)ノ＼(^_^ )

## source:
https://ollama.ai/blog/ollama-is-now-available-as-an-official-docker-image