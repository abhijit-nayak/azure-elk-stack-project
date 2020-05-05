# My Class Project of ELK Server Implementation :octocat:


### Aim
To deploy an ELK (Elasticsearch-Logstash-Kibana) for DVWA setup

### Apparatus
#### Virtual Machines
|VM| OS |Memory|Purpose|
|--|--|--|--| 
| Jumpbox Provisioner|Ubuntu|4 GB |Vm running ansible to automate deployment on other hosts  |
|DVWA availability set|Ubuntu|4 GB |VM running the DVWA docker instances and send file logs and metric logs to the Elk server|
|Elk Server|Ubuntu|4 GB |elk server hosting the kibana SIEM|

#### Hardening rules
|Rule  |source ip | Port ranges | Priority
|--|--|--|--|
|Default Deny  |your own public ip| All | 4096
|Allow ssh  | your own public ip|22 |4092
|Allow http access | your own public ip|80 |4080
|Allow elasticsearch access|elk server ip| 5016 |4081
|Allow beats access |elk server ip| 9200 |4082


### Architecture
The following diagram shows the whole picture of Elk Stack Implementation for DVWA machines
![Azure archictecture](/diagrams/Azure-Elk-Server-Implementation.png)

### Procedure
1. We first need to deploy a jumpbox provisioner which will act as an ansible host to deploy containers on the other Virtual machines
2. Create 2 new vm's as availability sets and name them DVWA1 & 2.
3. Using the Ansible jumpbox, deploy the DVWA (Damn Vulnerable Web Application) container on these 2 Vm's using the `dvwa-playbook.yml` 
4. Create a load balancer and configure the two Vm's on Azure.
5. Create a new VM and name it ELK server
6. Using the Jumpbox deploy and configure ELK container on ELK server using the `elk-server-playbook`
7. In order for the ELK server to start monitoring, we need to deploy the filebeat and metricbeat on the DVWA Vm's
8. We need to change the ip's to our elk server vm public ip to elasticsearch and kibana hosts in `filebeat-configuration.yml` and `metricbeat-configuration.yml` files and place them in `/etc/ansible/files` folder
9. Using the ansible `copy` command we will push this to its desired location on DVWA machine
10. Finally, on the jumbox vm, we need to run the `filebeat-playbook.yml` and `metric-playbook.yml`

## Conclusion
### Successful implementation of DVWA container :tada:

![DVWA container](/images/dvwa.png)

### Successful implementation of filebeat and metricbeat transmitting to elk server :tada:

![Filebeat Kibana](/images/filebeat-dashboard.png)

![Metricbeat Kibana](/images/metricbeat-dashboard.png)

## :loudspeaker: Coming-soon Availability zones for DVWA servers