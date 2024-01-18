Description how to docker here tbd

_________________________________________________________

sudo docker run -dit --name apache-webserver -p 80:80 -v /opt/httpd/htdocs:/usr/local/apache2/htdocs/ httpd:2.4
_________________________________________________________
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