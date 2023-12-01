# Installing Apache
cd /opt

>changes the folder to /opt

sudo mkdir httpd

>creates a folder called httpd

sudo chown youruser:youruser httpd/

>changes the folder owner to a specific user (don't use root:root)

sudo docker run -dit --name apache-webserver -p 80:80 -v /opt/httpd/htdocs:/usr/local/apache2/htdocs/ httpd:2.4

>starts the container on the IP of the host with port 80 to the outside and mounts htcdocs to /opt/httpd on the host

Done! ヘ( ^o^)ノ＼(^_^ )