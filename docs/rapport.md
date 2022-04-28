---
title: |
  DATA2410-1 22V Datanettverk og Skytjenester

  GROUP Portfolio Assignment 2 - Docker and Zabbix Real Use-Case
author: |
  Ulrik Bakken Singsaas | s351917 \
  Adrian \
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

```bash
sudo docker container run --privileged -v /var/run/docker.sock:/var/run/docker.sock -d vm_image
```

The image, `vm_image`, was made from this Dockerfile:

<!--
TODO
- [ ] update this dockerfile to match not having apache
-->

```dockerfile
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

We start by fetching this: ` wget https://repo.zabbix.com/zabbix/6.1/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.1-1%2Bubuntu20.04_all.deb`
So that we can install the `zabbix-agent`

Installing zabbix-proxy on VM2:

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

```bash
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

# 3. VM2: Nginx proxy 10%

# 4. VM1: Zabbix frontend
