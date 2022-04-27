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

Test

# 1. VM1: Docker containers setup 10%

## VM Setup

Started with deleting the 3 VMs set up by default as these had the wrong ubuntu version in relation to the ones reccomended in the task text.

We used these commands to make new containers with the focal fossa version, whilst also allowing for having docker containers within docker containers.

```bash
sudo docker container run --privileged -v /var/run/docker.sock:/var/run/docker.sock -p 8080:80 -d vm_image
```

where `vm_image` was made from this Dockerfile:

```dockerfile
FROM ubuntu:20.04
ENV TZ=Europe/Oslo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime  && echo $TZ > /etc/timezone
RUN apt-get -y update
RUN apt install iputils-ping -y
RUN apt install net-tools -y
RUN apt install nano -y
RUN apt-get -y install apache2
CMD ["apachectl", "-D", "FOREGROUND"]
```

## Quad Container Setup

Then we we used our file found in configs/docker-compose.yml to set up the four containers required for the task, as required by the text with the given config instructions.

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

<!-- det er feil versjon av liblap og libssl på docker containeren på intel1 som gjør at vi ikke får installert ``zabbix-agent`` -->


# 3. VM2: Nginx proxy 10%
# 4. VM1: Zabbix frontend 
