# Cool Links:

## VirtualBox VM
where i got the VM .iso (which we used in the first VM but no longer are using)
https://releases.ubuntu.com/20.04.4/

## Zabbix Manual installation from containers
https://www.zabbix.com/documentation/current/en/manual/installation/containers

## Zabbix agent
guide for zabbix agent on ubuntu focal fossa
https://tecadmin.net/how-to-install-zabbix-agent-on-ubuntu-20-04/

zabbix agent docs on zabbix site:
https://www.zabbix.com/zabbix_agent


## Zabbix Server
guide for zabbix server
https://www.alibabacloud.com/blog/how-to-install-zabbix-monitoring-server-on-ubuntu-20-04_597802

## nginx proxy
guide for nginx proxy:
https://www.hostinger.com/tutorials/how-to-set-up-nginx-reverse-proxy/

## ubuntu github cli install
Used this guide: https://www.techiediaries.com/install-github-cli-ubuntu-20/

Commands we used from that guide:
```shell script
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key C99B11DEB97541F0
sudo apt-add-repository https://cli.github.com/packages
sudo apt update
sudo apt install gh
```

# ssh for intel1
```shell script
ssh -p 513 g13@intel1.vlab.cs.hioa.no
pass: fell7rips
```

# lise løsning for agent og server active
Lise — Today at 5:26 PM
Fikk også dette (etter jeg prøvde å koble til den eksterne agenten). plutselig ville ikke stack-agenten koble seg opp mot server-hosten. Lagde en agent-host (zabbix-agent) på frontend og da var den fornøyd. Men jeg vet ikke om det er rett løsning, eller hvorfor det løste problemet 🙃  Lagde hosten basert på videoen her: https://blog.zabbix.com/handy-tips-15-deploying-zabbix-passive-and-active-agents/17696/