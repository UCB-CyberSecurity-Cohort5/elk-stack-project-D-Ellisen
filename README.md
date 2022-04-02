# ELK-Stack-Project
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-D-Ellisen/blob/main/Screenshots/Screenshots/MEDIUM.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  ![image](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-D-Ellisen/blob/main/Screenshots/Screenshots/Screenshot%202-3%20filebeat%20playbook.png)
  ![image](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-D-Ellisen/blob/main/Screenshots/Screenshots/Screenshot%202-6%20metricbeat%20playbook.png)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive, in addition to restricting access to the network.
What aspect of security do load balancers protect? What is the advantage of a jump box?

--Load ballancers protect against distributed denial of service attacks (DDoS) by analysing incoming traffic in real time and
determining what server to send that traffic to. This prevents any one server from becoming overloaded with traffic because the
load balancer can tell which servers are being used and distribute traffic evenly so none of them are strained. Load balancers 
also have a health probe which checks if a machine is working properly before sending traffic. if the machine is not working properly 
the load balancer will divert traffic away from it until it is restored to proper functionality. A jump box ensures the public cannot a
access your virtual network. It does this in multiple ways. for one, you can set it so that only the jump box may access the network 
therefore for someone to compromise the network, they would have to first compromise the jumpbox. On top of that even if they did 
compromise the jump box they would have to know the private IPs of each machine to access them. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

     What does Filebeat watch for? Filebeat looks for changes/alterations to files. It then creates a record of when said changes 
 occured so create a detailed list. 

    What does Metricbeat record? Metricbeat records metrics from the opperating system and services/applications running on a server
 you can then view this data using a applications such as Elastisearch or Logstash. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux-Ubuntu 18.04|
| Web-1    | web-serv | 10.0.0.6   | Linux-Ubuntu 18.04|
| Web-2    | web-serv | 10.0.0.7   | Linux-Ubuntu 18.04|
| Elk-srv  | Elk-serv | 10.1.0.6   | Linux-Ubuntu 18.04|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 23.81.114.195 -my public IP address- 

Machines within the network can only be accessed by Jump-Box-Provisioner machine.
- _TODO: Which machine did you allow to access your ELK VM? 
Only the jump-Box-Provisioner VM 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.0.0.1             |
| Web-1    | No                  | 10.0.0.6             |
| Web-3    | No                  | 10.0.0.7             |
| Elk-srv  | yes (via5601)       | 10.1.0.6             |
| Load-bl  | yes (via 80)        | 10.1.0.4             |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it prevented having
to cinfigure elk manually thus drastically reducing the risk of human error. It also makes the process faster and more streamlined. 

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- The first action of the elk playbook installs docker.io on the ELK-VM 
- The second action installs python on the ELK-VM
- The third action increases the virtual memory to the required ammount 
- The fourth action downloads, installs and executes the docker ELK container on the ELK-VM on restart
- The fifth action enables docker on boot.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-D-Ellisen/blob/main/Screenshots/Screenshots/Screenshot%201-13%20sudo%20docker%20ps%20to%20verify%20container%20is%20running%20on%20elk%20server.png) 

### Target Machines & Beats
This ELK server is configured to monitor the following machines: 
Web-1: 10.0.0.6 Web-2: 10.0.0.7 Web-3: 10.0.0.8

We have installed the following Beats on these machines:
Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see.
Filebeat collects data about the filesystem and specifies which files have been changed and when a file was changed. This information is viewable
with elastisearch or logstash. In order to see the output from filebeat you would connect to Kibana and view the logs. Metricbeat shows statistics 
for every process running on the machine including memory, cpu usage and filesystem, network IO and disk IO statistics. You would view this data in Kibana.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/files/filebeat-config.yml.
- Update the filebeat-config.yml file to include host "10.1.0.69200" with username "elastic" and
password "changename" and set up kibana host to "10.1.0.65200" 
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.
![image](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-D-Ellisen/blob/main/Screenshots/Screenshots/Screenshot%202-6%20DATA%20SUCCESSFULLY%20RECIEVED%20(screenshot%20what%20you%20see%20before%20proceeding).png)
![image](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-D-Ellisen/blob/main/Screenshots/Screenshots/Screenshot%202-7%20metricbeat%20success.png)

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? filebeat-playbook.yml where do you copy it /etc/ansible/filebeat-playbook.yml

- _Which file do you update to make Ansible run the playbook on a specific machine? -filebeat-config.yml. How do I specify which machine to install the ELK server on versus which to install Filebeat on? All private IP addresses that need to be accessed must be added to the hosts file in order to connect. 4 Addresses were added, the 3 web servers (2 being neccessary with a third for redundency) and the ELK server. Next, you must go to the playbook file, navigate to "hosts" and specify where you want the playbook installed (on ELK, Webservers etc...). We then have to specify the host to the elk server for filebeat so "10.1.0.6" is added to the config to specify the location for installation. 
![image](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-D-Ellisen/blob/main/Screenshots/Screenshots/FIlebeat%20config.png)
![image](https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-D-Ellisen/blob/main/Screenshots/Screenshots/hosts-screenshot.png)


- _Which URL do you navigate to in order to check that the ELK server is running?
http://[ELK-VM-Public-Ip-Address]:5601/app/kibana NOTE- you must do "HTTP" NOT! "HTTPS" 


