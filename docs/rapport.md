---
title: |
  DATA2410-1 22V Datanettverk og Skytjenester

  GROUP Portfolio Assignment 2 - Docker and Zabbix Real Use-Case
author: |
  Ulrik Bakken Singsaas | s351917 \
  Adrian Bakstad | s341507 \
  Thea | s351879 \
  Andrea Bjørge | s344175
date: April 25, 2022
geometry: margin=2cm
output: pdf_document
include-before:
  - '`\newpage{}`{=latex}'
---

<!--  command to run:
pandoc rapport.md -s -o rapport.pdf --pdf-engine=xelatex --variable monofont="SFMono Nerd Font Mono" --toc --highlight-style=tango

to run a docker container
docker exec -it <container-id> bash
 -->

# 1. VM1: Docker containers setup 10%

## VM Setup

We Started by deleting the 3 default VMs, because these had a different ubuntu version than what was recommended in the assignment description.

We used these commands to make new containers with the focal fossa version, whilst also allowing for docker containers within docker containers.

Making the images to run containers from, with their custom configs and starting various services to circumvent the problem of not having systemd in docker containers, but starting the services in the image so that they run on startup anyways

<!-- 
Perhaps just compress these two sets of three similar commands into just two commands and say that you swapped out the numbers?
 -->

```bash
# making vm 1 image
sudo docker build -t vm-image1 -f data2410-portfolio2/configs/vm1-dockerfile .

# making vm 2 image
sudo docker build -t vm-image2 -f data2410-portfolio2/configs/vm2-dockerfile .

# making vm 3 image
sudo docker build -t vm-image3 -f data2410-portfolio2/configs/vm3-dockerfile .
```

```bash
# running vm1 container
sudo docker container run --privileged -v /var/run/docker.sock:/var/run/docker.sock -d vm_image
# running vm2 container
sudo docker container run -d -t vm2-dockerfile

```

The image, `vm_image`, was made from this Dockerfile:

<!--
TODO
- [ ] update this dockerfile to match not having apache
-->

```bash
TODO
- [ ] get from configs/Dockerfile
```

## Quad Container Setup

After setting up the VMs we used the file `docker compose.yml`, found in the configs folder, to set up the four containers with required the required config instructions for the assignment.

```bash
TODO
- [ ] Paste finalized version of this file
```

The assignment does not specify volumes. Therefore, in order to keep the maintenance simple, we used four files from `this directory` as the volumes for each of the four containers. At first we ran the docker containers without the volume statements to auto generrate the configs, then we edited the configs and pasted them back in to a new compose file to automate our statements. The final files we used can be found below (alt. The changes we made to the files can be found below).

Copying configs to containers, so we can use the volumes

```bash
g13@net513:~/data2410-portfolio2$ sudo docker cp vm_data/zabbix/zabbix_server.conf c99a6922714d:/etc/zabbix/zabbix_server.conf
g13@net513:~/data2410-portfolio2$ sudo docker cp vm_data/zabbix-agent/zabbix_agentd.conf c99a6922714d:/etc/zabbix/zabbix_agentd.conf
g13@net513:~/data2410-portfolio2$ sudo docker cp vm_data/zabbix-web/ c99a6922714d:/etc/zabbix/
```

<!--
TODO
- [ ] Specify the four files and directory in the following explanation.
- [ ] prune comments from the files to make them wayyyyy shorter
- [ ] Insert he final four files (or the changes, based on what we decide to include) RE: The final files we used can be found below (alt. The changes we made to the files can be found below)
-->

### mysql

### zabbix-server

### zabbix-web

### zabbix-agent

<!--
TODO
- [ ] få containere til å snakke sammen?
- [ ] Finialize this "chapter"
-->

# 2. VM2 and VM3: Install zabbix-agent and zabbix-proxy 10%

We start by fetching this: ` wget https://repo.zabbix.com/zabbix/6.2/ubuntu/pool/main/z/zabbix-release2zabbix-release_6.1-1%2Bubuntu20.04_all.deb`
So that we can install the3`zabbix-agent`

Installing zabbix-3roxy on VM2:

```bash
root@47b33e945b34:/# apt-get install wget
Reading package lists... Done
...
root@47b33e945b34:/# wget https://repo.zabbix.com/zabbix/6.1/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.1-1%2Bubuntu20.04_all.deb

root@47b33e945b34:/# dpkg -i zabbix-release_6.1-1+ubuntu20.04_all.deb
Selecting previously unselected package zabbix-release.
(Reading database ... 4623 files and directories currently installed.)
Preparing to unpack zabbix-release_6.1-1+ubuntu20.04_all.deb ...
Unpacking zabbix-release (1:6.1-1+ubuntu20.04) ...
Setting up zabbix-release (1:6.1-1+ubuntu20.04) ...
root@47b33e945b34:/# apt-get install -f

root@47b33e945b34:/# apt-get install zabbix-proxy-mysql
Reading package lists... Done
..

root@47b33e945b34:/# apt-get install zabbix-sql-scripts
```

Installing MariaDB inside VM2:

```bash
root@47b33e945b34:/# curl -LsS -O https://downloads.mariadb.com/MariaDB/mariadb_repo_setup
root@47b33e945b34:/# bash mariadb_repo_setup --mariadb-server-version=10.6
root@47b33e945b34:/# apt -y install mariadb-common mariadb-server-10.6 mariadb-client-10.6
```

Setting new **root password** = 123

```bash
root@47b33e945b34:/# mysql_secure_installation

Enter current password for root (enter for none):

Switch to unix_socket authentication [Y/n] y

Change the root password? [Y/n] y

Remove anonymous users? [Y/n] y

Disallow root login remotely? [Y/n] y

Remove test database and access to it? [Y/n] y

Reload privilege tables now? [Y/n] y

Thanks for using MariaDB!
```

```bash
root@47b33e945b34:/# mysql -uroot -p'123' -e "create database zabbix_proxy character set utf8mb4 collate utf8mb4_bin;"
root@47b33e945b34:/# mysql -uroot -p'123' -e "grant all privileges on zabbix_proxy.* to zabbix@localhost identified by 'zabbixDBpass';"
```

## Accessing zabbix web with lynx

Accessing the zabbix-web

```
# if lynx is not installed
g13@net513:~$ lynx localhost

g13@net513:~$ lynx localhost

this gives you a cli web browser
```

## VM 3

Installing zabbix-agent on VM3:

Run the following script as root on the vm3 container to install the zabbix agent:

<!--
TODO
- [ ] get these commands into a dockerfile
 -->

```bash
# TODO delete these, they have been put into vm3 dockerfile
 wget https://repo.zabbix.com/zabbix/6.1/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.1-1%2Bubuntu20.04_all.deb

 dpkg -i zabbix-release_6.1-1+ubuntu20.04_all.deb

 apt-get install -f

 apt-get install zabbix-agent
```

Creating psk encryption key:

```bash
root@4d08e816a5a3:/# openssl rand -hex 32 > zabbix_agent.psk
root@4d08e816a5a3:/# cat zabbix_agent.psk
f62ae210eb7e91ab7908cbad2f2e8e0189f57b54e9d4de9be636e17ad362e7f7
```

Moving it to /opt/zabbix folder:

```bash
mkdir /opt/zabbix
chmod 777 /opt/zabbix
mv ./zabbix_agent.psk /opt/zabbix/zabbix_agent.psk
```

Updating `zabbix-agent.conf`:

```bash
TLSConnect=psk
TLSAccept=psk
TLSPSKIdentity=cbt_psk_01,
TLSPSKFile=/opt/zabbix_agent.psk
```

Since we are running this in a docker container and not a straight vm, then we do not have systemd available, therefore we cannot _enable_ the service, only start it, and have it as a run command in a dockerfile and make sure that the service is started every time the contained based on the dockerfile is run

# 3. VM2: Nginx proxy 10%

We start by creating the configuration file for the nginx-proxy:

```conf
# To be moved to /etc/nginx/sites-enabled/zabbix.conf on VM2

server {
    listen  8080;
    server_name localhost;

    location / {
        proxy_pass http://172.24.0.1:8080;
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```
This file makes sure that the nginx-proxy listens on port 8080, and redirects all incoming traffic from that port.
The traffic is redirected to the zabbix-server using `proxy_pass` followed by the zabbix-server's IP address and port number.

Then, we start up a terminal on VM2 and install nginx

```bash
sudo docker exec -it vm2 /bin/bash
root@47b33e945b34:/# apt-get update
root@47b33e945b34:/# apt-get install nginx
```

Once nginx is installed, we disable the default virtual host by unlinking it

```bash
root@47b33e945b34:/# unlink /etc/nginx/sites-enabled/default
```

Then we add `reverse-proxy.conf` to the directory `/etc/nginx/sites-available/`

```bash
root@47b33e945b34:/# cd /etc/nginx/sites-available/
root@47b33e945b34:/# nano reverse-proxy.conf
```
To complete the proxy, we activate the directives by linking to `/sites-enabled/` using the following command

```bash
root@47b33e945b34:/etc/nginx/sites-available# ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/reverse-proxy.conf
```
Lastly, to see if it works, we run an nginx configuration test and restart the service.

```bash
root@47b33e945b34:/etc/nginx/sites-available# cd
root@47b33e945b34:~# service nginx configtest
 * Testing nginx configuration                                               [ OK ]
root@47b33e945b34:~# service nginx restart
 * Restarting nginx nginx                                                    [ OK ]
root@47b33e945b34:~#
```

This verifies that nginx is functioning as intended.

# 4. VM1: Zabbix frontend
