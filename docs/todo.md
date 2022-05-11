# II. VM 1: Docker containers setup
- [x] Install Docker v20.10.8 and docker-compose from the official website. 
- [x] Create a docker-compose stack with zabbix-server-mysql, zabbix-server-web, mysql-server, and zabbix-agent
  - [x] Define a docker bridge network for the stack, assign it subnet and gateway, and assign each container with static ipv4 address
- [x] Container 1: mysql-server (Spesifikasjoner i oppgaveteksten)
- [x] Container 2: zabbix-server-mysql (Spesifikasjoner i oppgaveteksten)
- [x] Container 3: zabbix-web-nginx-mysql (Spesifikasjoner i oppgaveteksten)
- [x] Container 4: zabbix/zabbix-agent (Spesifikasjoner i oppgaveteksten)

## Tillegg
- [x] Finn ut av volumes for 4 containers  (kan hende vi trenger mer configs)
- [x] Finn ut av å lage et container network
  - [x] Få agent og server til å sende active logs
- [ ] Fix server not sending active checks and agent not getting active checks


# III. VM2 and VM3: Install zabbix-agent and zabbix-proxy 
- [x] Zabbix proxy installation on VM2
  - [x] Install zabbix-proxy 
  - [x] Install MariaDB
  - [x] Configure zabbix-proxy to connect to the MariaDB
  - [x] Configure zabbix-proxy to connect to zabbix-server
  - [x] Start and enable zabbix-proxy
- [x] Zabbix agent installation on VM3
  - [x] Install zabbix-agent from ??
  - [x] Start and enable zabbix-agent
  - [x] Testing zabbix agent with restarting 
  - [x] Generate hex value for psk encryption file on your local VM3. (Spesifikasjoner i oppgaveteksten)
 - [x] Move file to /opt/zabbix/ directory and give it permissions which will enable zabbix-agent to access the file. 
 - [x] Enable psk encryption in the zabbix-agent configuration file and set valid server address (Spesifikasjoner i oppgaveteksten) 



# IV. VM2: Nginx proxy  
- [x] Install nginx proxy and prepare the files to configure nginx proxy
- [x] Add to /etc/nginx/nginx.conf include directories (Spesifikasjoner i oppgaveteksten)
- [x] zabbix-server-web has its own nginx.conf and it needs to be configured to listen on port 8080

## Tillegg
- [ ] Koble agent mot zabbix proxy (vm3 til vm2)
- [x] Flytte kommandoer over til Dockerfile


# V. VM1: Zabbix frontend
- [x] Create a host group named zabbix-monitoring
- [ ] Create a host, assign it to the newly created group, and configure the agent with VM3 ipv4 address and port used by zabbix-agent
- [ ] Assign a hostname and visible name
- [ ] Add a template named Linux by zabbix agent
- [ ] Enable encryption with PSK and configure it
- [ ] Create a new template named zabbix-monitoring and add the following items and triggers (Spesifikasjoner i oppgavetekster)


# General
- [ ] Rapportere det vi har gjort så langt
- [ ] Guide for hvordan man kjører
- [ ] Ta oppvasken
- [ ] APA kildehenvisning i proxy configuration i VM2.


# Redundant
- [ ] Maile Hårek om docker i docker
- [x] Maile Hårek om hosting av nginx proxy
- [ ] Maile Hårek ssh tunneling for å debugge i browser