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
 -->

Test

# 1. VM1: Docker containers setup 10%
# 2. VM2 and VM3: Install zabbix-agent and zabbix-proxy 10%

Starter med å hente: ` wget https://repo.zabbix.com/zabbix/6.1/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.1-1%2Bubuntu20.04_all.deb`
Sånn at vi kan installere `zabbix-agent`

<!-- det er feil versjon av liblap og libssl på docker containeren på intel1 som gjør at vi ikke får installert ``zabbix-agent`` -->


# 3. VM2: Nginx proxy 10%
# 4. VM1: Zabbix frontend 
