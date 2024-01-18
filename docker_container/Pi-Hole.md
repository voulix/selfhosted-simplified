```yml
cd /opt
```

>changes the folder to /opt

```yml
sudo mkdir pihole
```

>creates a folder called pihole

```yml
sudo chown youruser:youruser /opt/pihole/
```

>changes the folder owner to a specific user (don't use root:root)

```yml
cd /opt/pihole/
```

>changes the folder to /opt/pihole/

```yml
nano docker-compose.yaml
```

>creates a new file called docker-compose.yaml

Copy the following into the file:

```yml
version: "3"

# More info at https://github.com/pi-hole/docker-pi-hole/ and https://docs.pi-hole.net/
services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    # For DHCP it is recommended to remove these ports and instead add: network_mode: "host"
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "9001:80/tcp"
      # - "67:67/udp" # Only required if you are using Pi-hole as your DHCP server
    environment:
      TZ: Europe/Berlin
      WEBPASSWORD: yourpasswordpleasechange
    # Volumes store your data between container upgrades
    volumes:
      - /opt/pihole/etc-pihole:/etc/pihole'
      - /opt/pihole/etc-dnsmasq.d:/etc/dnsmasq.d'
    #   https://github.com/pi-hole/docker-pi-hole#note-on-capabilities
    restart: unless-stopped
```

```yml
sudo docker compose up -d
```

>creates the docker container from the file we have just created **docker-compose.yaml**

Paste the following in a browser of you choice: http://0.0.0.0:9001/admin/login.php (replace 0.0.0.0 with the ip of the system running Pi-Hole)

Done! ヘ( ^o^)ノ＼(^_^ )
_________________________________________________________

# bonus

>to reduce db days saved (logging)

```yml
cd /opt/pihole/etc-pihole
```

>changes the folder to /opt/pihole/etc-pihole

```yml
sudo nano pihole-FTL.conf
```

>opens the file pihole-FTL.conf in nano

add to file

```yml
MAXDBDAYS=7      			
```

>to reduce db days saved  7=days

save & restart the container
_________________________________________________________
# troubleshooting

>if you cannot start the container because smth else is using the DNS port (53)

To find what is using port 53 you can do: 

```yml
sudo lsof -i -P -n | grep LISTEN
```

I'm 99.9% sure that systemd-resolved is what is listening to port 53. To solve that you need to disable it. You can do that with these 2 commands:

```yml
systemctl disable systemd-resolved.service
```

```yml
- systemctl stop systemd-resolved
```

Now you have port 53 open, but no dns configured for your host. To fix that, you need to edit '/etc/resolv.conf' and add the dns address. This is an example with a common dns address:

```yml
nameserver 8.8.8.8
```

If you have another nameserver in that file, I would comment it to prevent issues.
Once pihole docker container gets running, you can change the dns server of your host to localhost, as you are binding port 53 to the host machine. Change again '/etc/resolv.conf' like this

```yml
nameserver 127.0.0.1
```

Hope this helped!
_________________________________________________________