## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Diagram](diagrams/Azure-Elk-Server-Implementation.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the `YAML` file may be used to install only certain pieces of it, such as below:
[Filebeat Playbook](/ansibleplaybooks/filebeat-playbook.yml)
[Metricbeat Playbook](/ansibleplaybooks/metricbeatbeat-playbook.yml)
[Elk Server Playbook](/ansibleplaybooks/elk-server-playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly ### available, in addition to restricting `public` access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the system `Logstash`  and system `metrics`.

The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway   | 10.0.0.4  | Ubuntu Linux     |
| DVWA 1   | Webserver | 10.0.0.5  | Ubuntu Linux     |
| DVWA 2   | Webserver | 10.0.0.6  | Ubuntu Linux     |
| Elk      | Elkserver | 10.1.0.4  | Ubuntu Linux     |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the `Jumpbox and Elkserver` machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:`My own 142.XXX.XXX.183`

Machines within the network can only be accessed by `Jumpbox: 10.0.0.4`.

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses     |
|-----------|---------------------|--------------------------|
| Jump Box  | Yes                | 142.XXX.XXX.183           |
| DVWA1     | No                 | 10.0.0.4, 10.1.0.4        |
| DVWA2     | No                 | 10.0.0.4, 10.1.0.4        |
| Elkserver | Yes                | 142.XXX.XXX.183,10.0.0.4, |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because `automation needs less efforts and can be scripted to run deployment on different machines at the same time.`

The playbook implements the following tasks on the host machine:
- Install docker
- Install Python-pip
- Install the docker python module
- Increase the virtual Memory
- Download and launch the elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- DVWA1: 10.0.0.5
- DVWA2: 10.0.0.6
- ELK: 10.1.0.4

We have installed the following Beats on these machines:
- filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors and collects log files on the DVWA1 and DVWA2 machines and forwards them to the Elasticsearch for indexing
- Metricbeat monitors and collects metrics and statistics on the DVWA1 and DVWA2 machines and forwards them to the Elasticsearch for indexing


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the [elk server playbook](/ansibleplaybooks/elk-server-playbook.yml),[filebeat-playbook](/ansibleplaybooks/filebeat-playbook.yml) [metricbeat-playbook](/ansibleplaybooks/metricbeat-playbook.yml)  file to `/etc/ansible`.
- Copy the [filebeat.yml](/ansibleplaybooks/filebeat.yml), [metricbeat.yml](/ansibleplaybooks/metricbeat.yml) to `/etc/ansible` and update the ip address for kibana and elastic search with elk vm ip address.
- Update the hosts file to include ip address of elk server VM to install elk servers
- Run the playbook, and navigate to http://<elk server public ip>:5601 to check that the installation worked as expected.
- Update the hosts file to include ip address of DVWA machines to install filebeat and metricbeat
- Run the playbook for filebeat and metricbeat and http://<elk server public ip>:5601 and check whether filebeat and metric beat dashboard are generated.

### Screenshots :tada:

![Filebeat Kibana](/images/filebeat-dashboard.png)

![Metricbeat Kibana](/images/metricbeat-dashboard.png)

## :loudspeaker: Coming-soon Availability zones for DVWA servers
