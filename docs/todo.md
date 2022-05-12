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
- [x] Fix server not sending active checks and agent not getting active checks


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
- [x] Koble agent mot zabbix proxy (vm3 til vm2)
- [x] Flytte kommandoer over til Dockerfile


# V. VM1: Zabbix frontend
- [x] Create a host group named zabbix-monitoring
- [x] Create a host, assign it to the newly created group, and configure the agent with VM3 ipv4 address and port used by zabbix-agent
- [x] Assign a hostname and visible name
- [x] Add a template named Linux by zabbix agent
- [x] Enable encryption with PSK and configure it
- [x] Create a new template named zabbix-monitoring and add the following items and triggers (Spesifikasjoner i oppgavetekster)
  - [x] **Check Discord pinned for this, in network channel**
  - [x] **Check Thea's presentation in our private discord for this setup thingyyyyyyyyy ~~we out here~~**
  - [x] Create an item in the template that will monitor the total used disk space on the directory /var, interval 1h
  - [x] Create an item in the template that will monitor docker process usage, interval 1m, units %
  - [x] Create a trigger in the template that will trigger when uptime is longer than 240 days, assign it type information (solution:  {test-hostname:system.uptime.last()}>240d)
  - [x] Create a trigger in the template that will trigger when disk i/o is overloaded, higher than 20, average 5min (solution: {test-hostname:system.cpu.util[,iowait].avg(5m)}>20)


# General
- [x] Rapportere det vi har gjort så langt
- [x] Guide for hvordan man kjører
- [x] APA kildehenvisning i proxy configuration i VM2.
- [ ] Ta oppvasken


# Redundant
- [x] Maile Hårek om docker i docker
- [x] Maile Hårek om hosting av nginx proxy
- [x] Maile Hårek ssh tunneling for å debugge i browser

# Oppvasken
- [ ] 1. Introduction
  - [ ] 1.1. Our project directory
    - [x] First draft 
    - [x] Edited
    - [ ] Done 
  - [ ] 1.2. Virtual Machines with VirtualBox 
    - [x] First draft 
    - [x] Edited
    - [ ] Done 
- [ ] 2. VM1: Docker containers setup
  - [ ] 2.1. Quad Container Setup on intel1 / VM1
    - [x] First draft 
    - [ ] Edited
    - [ ] Done 
- [ ] 3. VM2 and VM3: Install zabbix-agent and zabbix-proxy
  - [ ] Ha systemctl kommandoer for VM2 og VM3
  - [ ] 3.1. VM2
     - [ ] 3.1.1. Innstalling Zabbix Proxy
       - [x] First draft 
       - [ ] Edited
       - [ ] Done 
     - [ ] 3.1.2. Configuring MariaDB database for the proxy to use
       - [x] First draft 
       - [ ] Edited
       - [ ] Done 
     - [ ] 3.1.3. Configurating Zabbix Proxy
       - [x] First draft 
       - [ ] Edited
       - [ ] Done 
     - [ ] 3.1.4. Starting and enabling the Zabbix Proxy
       - [x] First draft 
       - [ ] Edited
       - [ ] Done 
     - [ ] 3.1.5. Registering Zabbix Proxy in the Zabbix frontend
       - [x] First draft 
       - [ ] Edited
       - [ ] Done 
  - [ ] 3.2. VM 3
    - [ ] First draft 
    - [ ] Edited
    - [ ] Done 
- [ ] 4. VM2: Nginx proxy
  - [ ] First draft 
  - [ ] Edited
  - [ ] Done 
- [ ] 5. VM1: Zabbix frontend
  - [ ] 5.1. Items
    - [ ] First draft 
    - [ ] Edited
    - [ ] Done 
  - [ ] 5.2. Triggers
    - [ ] First draft 
    - [ ] Edited
    - [ ] Done 
- [ ] 6. APA7 References?
  - [ ] First draft 
  - [ ] Edited
  - [ ] Done 
- [ ] Other
  - [ ] Change "Introduction" to "Introduction: VM setup" and remove subheading 1.1
  - [ ] Final read through and edit
  - [ ] Clean up unnecessary comments
  - [ ] Remove all references to our project directory and folders if we're not delivering the .zip file of our working directory. 
  - [ ] Check all figure references. 
  - [ ] Convert to pdf
  - [ ] Deliver the report

  # Report structure
  - [x] Ikke ha tekst på samme side som innholdsfortegnelsen
  - [ ] Linjeavastand 1,5 i hele dokumentet
  - [ ] Mer whitespace mellom tekst og bilder/kode