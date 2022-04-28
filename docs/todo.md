# II. VM 1: Docker containers setup
- [ ] Install Docker v20.10.8 and docker-compose from the official website. 
- [ ] Create a docker-compose stack with zabbix-server-mysql, zabbix-server-web, mysql-server, and zabbix-agent
 - [ ] Define a docker bridge network for the stack, assign it subnet and gateway, and assign each container with static ipv4 address
- [ ] Container 1: mysql-server (Spesifikasjoner i oppgaveteksten)
- [ ] Container 2: zabbix-server-mysql (Spesifikasjoner i oppgaveteksten)
- [ ] Container 3: zabbix-web-nginx-mysql (Spesifikasjoner i oppgaveteksten)
- [ ] Container 4: zabbix/zabbix-agent (Spesifikasjoner i oppgaveteksten)
## Tillegg
- [ ] Finn ut av volumes for 4 containers 
- [ ] Finn ut av å lage et container network

# III. VM2 and VM3: Install zabbix-agent and zabbix-proxy 
- [ ] Zabbix proxy installation on VM2
 - [ ] Install zabbix-proxy 
 - [ ] Install MariaDB
 - [ ] Configure zabbix-proxy to connect to the MariaDB
 - [ ] Configure zabbix-proxy to connect to zabbix-server
 - [ ] Start and eanble zabbix-proxy
- [ ] Zabbix agent installation on VM3
 - [ ] Install zabbix-agent from
 - [ ] Start and enable zabbix-agent
 - [ ] Generate hex value for psk encryption file on your local VM3. (Spesifikasjoner i oppgaveteksten)
 - [ ] Move file to /opt/zabbix/ directory and give it permissions which will enable zabbix-agent to access the file. 
 - [ ] Enable psk encryption in the zabbix-agent configuration file and set valid server address (Spesifikasjoner i oppgaveteksten) 

# IV. VM2: Nginx proxy  
- [ ] Install nginx proxy and prepare the files to configure nginx proxy
- [ ] Add to /etc/nginx/nginx.conf include directories (Spesifikasjoner i oppgaveteksten)
- [ ] zabbix-server-web has its own nginx.conf and it needs to be configured to listen on port 8080
## Tillegg
- [ ] Koble agent mot proxy

# V. VM1: Zabbix frontend
- [ ] Create a host group named zabbix-monitoring
- [ ] Create a host, assign it to the newly created group, and configure the agent with VM3 ipv4 address and port used by zabbix-agent
- [ ] Assign a hostname and visible name
- [ ] Add a template named Linux by zabbix agent
- [ ] Enable encryption with PSK and configure it
- [ ] Create a new template named zabbix-monitoring and add the following items and triggers (Spesifikasjoner i oppgavetekster)
 - [ ]

# General
- [ ] Rapportere det vi har gjort så langt
- [ ] Guide for hvordan man kjører
- [ ] Ta oppvasken

# Redundant
- [ ] Maile Hårek om docker i docker