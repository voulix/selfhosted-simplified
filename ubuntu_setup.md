- download Ubuntu Server LTS from the official [website](https://ubuntu.com/download/server)
- create a USB boot drive with [Rufus](https://rufus.ie)
>Now start the installation on your machine. If you are not sure how to that, search for a tutorial on YouTube
#### After OS isntallation
- sudo apt update && sudo apt upgrade
- configure ufw
#### ssh keys
1. sudo ssh-keygen -b 4096 
- follow instructions
2. copy contents of publickey (.pub) into the authorized_key file located in /home/your_username/.ssh
3. copy private key to client (windows) open powershell and type ssh-add path/to/private/key
> disable password login on the server
4. sudo nano /etc/ssh/sshd_config
5. change PasswordAuthentication & ChallengeResponseAuthentication to **no**
6. sudo nano /etc/ssh/sshd_config.d/*.conf
7. change PasswordAuthentication to **no**
8. sudo restart ssh