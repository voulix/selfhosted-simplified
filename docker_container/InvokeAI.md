# InvokeAI
## prerequisites: 
>[nvidia-container-toolkit](https://github.com/NVIDIA/nvidia-container-toolkit)
## Installing InvokeAI

```yml
sudo docker run -it -p 9090:9090 -v /home/yourusernamehere/invokeai:/invokeai/ --name InvokeAI --gpus all local/invokeai bash
```

>runs the container in interactive mode with shell access. The download might take a few minutes

```yml
sudo docker stop InvokeAI
```

>stops the container 

```yml
cd /home/yourusernamehere/invokeai
```

>changes the folder to /home/yourusernamehere/invokeai

```yml
sudo nano invokeai.yaml -> set "Webserver host" to 0.0.0.0
```

>binds the IP from the InvokeAI webserver to your host

```yml
sudo docker start InvokeAI -i
```

>starts the container in interactive mode with shell access.

type **invokeai-web** and press **enter**

>start the InvokeAI webserver

to detach from the container press [Ctrl + P and Ctrl + Q] keys **together**

>closes the shell access without terminating the web server from InvokeAI

to add models via the webui use this format from huggingface **stabilityai/stable-diffusion-xl-base-1.0**

>recommended with newer models

models are located in /home/yourusernamehere/invokeai/models

Done! ヘ( ^o^)ノ＼(^_^ )