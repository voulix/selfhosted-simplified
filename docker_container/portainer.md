# Installing Portainer:

```yml
sudo docker volume create portainer_data
```

> You can call "portainer_data" whatever you want

```yml
sudo docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```

> Port 9000 = Webinterface Port HTTP | Port 9443 = HTTPS | to change the ports to the outside, change the port on the left side in the command or Dockerfile | Port 8000 is for an encrypted SSH tunnel for Portainer and to connect to headless instances (e.g. Docker Swarm)

# Updating Portainer:

> Delete old local Portainer Docker image in the Portainer web interface / or via docker cli if necessary

```yml
sudo docker stop portainer
```

> Stops the container with the name portainer

```yml
sudo docker rm portainer
```

> Deletes the container with the name portainer (the volume with the configs etc. is retained)

```yml
sudo docker images -a
```

>lists all docker iamges on the host

```yml
sudo docker image rm imagenameorID
```

> deletes a docker image

```yml
sudo docker pull portainer/portainer-ce:latest
```

> Downloads the latest portainer image from the Docker Hub

```yml
sudo docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```

> IMPORTANT!!! the same volume name MUST be used as when the instance was first created, otherwise the old configuration will not be loaded


Done! ヘ( ^o^)ノ＼(^_^ )


## tech tip
> docker volumes are mounted by default to **/var/lib/docker/volumes**