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

Started with deleting the 3 VMs set up by default as these had the wrong ubuntu version in relation to the ones reccomended in the task text.

We used these commands to make new containers with the focal fossa version, whilst also allowing for having docker containers within docker containers.

```bash
sudo docker container run --privileged -v /var/run/docker.sock:/var/run/docker.sock -d vm_image
```

where `vm_image` was made from this Dockerfile:

<!--
TODO
- [ ] update this dockerfile to match not having apache
-->

```dockerfile
TODO
- [ ] get from configs/Dockerfile
```

## Quad Container Setup

Then we used our file found in configs/docker-compose.yml to set up the four containers required for the task, as required by the text with the given config instructions.

```bash
TODO
- [ ] Past finalized version of this file
```

As no volumes were given, we used four files as the volumes for each of the four containers, linked to this git repo for easy maintenance. At first we ran without the volume statements to auto generrate the configs, then we edited those to paste then back in on a new compose to auto set our statements

these are the four files (TODO or the changes we made to the four files):

<!--
TODO
- [ ] prune comments from the files to make them wayyyyy shorter
- [ ] insert these four files
 -->

### mysql

### zabbix-server

### zabbix-web

### zabbix-agent

TODO

- [ ] få containere til å snakke sammen?
- [ ] Finialize this "chapter"

# 2. VM2 and VM3: Install zabbix-agent and zabbix-proxy 10%

Starter med å hente: ` wget https://repo.zabbix.com/zabbix/6.1/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.1-1%2Bubuntu20.04_all.deb`
Sånn at vi kan installere `zabbix-agent`

Installing zabbix-proxy:

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

Installing MariaDB inside vm2:

```bash
root@47b33e945b34:/# curl -LsS -O https://downloads.mariadb.com/MariaDB/mariadb_repo_setup
root@47b33e945b34:/# bash mariadb_repo_setup --mariadb-server-version=10.6
```

## VM 3

This is run as `root@4d08e816a5a3` aka. root on the vm3 container:

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
