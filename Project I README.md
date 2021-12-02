### Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Diagram](~/System/Users/ganneheim/Desktop/Jessies/HW/Unit13HW/Images/Unit13_Netwrok_Diagram.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Playbook files may be used to install only certain pieces of it, such as Filebeat.

  - _Filebeat and Metricbeat are the playbooks used in the deployment of the ELK server.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
- _Load balancers protect the availability aspect of a given network by not only protecting a given network from unintended traffic but as well as allowing a network to be available during times of high traffic going through the network. 
The main advantage of a jump box is that it allows for a secure way to access a given network because you can restrict or allow specify ports and traffic to that network. Essentially making the network more secure by only having one access point to the network, through the Jump Box.
 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system services.
- Filebeat monitors the locations that you specify, specifically log files. Filebeat will monitor log files, log events, and forward that information to Elasticsearch.  
- Metricbeat will monitor systems and services running on a server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

```
| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web 1 VM | DVWA     | 10.0.0.7   | Linux            |
| Web 2 VM | DVWA     | 10.0.0.8   | Linux            |
| Elk VM   | monitor  | 10.1.0.4   | Linux            |
```

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Whitelisted IP addresses: 157.131.169.176, 10.0.0.4, 10.1.0.4

Machines within the network can only be accessed by the Jump Box.
- Only the Jump Box, IP address of 10.0.0.4, has access to the ELK VM.   

A summary of the access policies in place can be found in the table below.

```
| Name     | Publicly Accessible | Allowed IP Addresses        |
|----------|---------------------|-----------------------------|
| Jump Box | Yes                 | 157.131.169.176 10.0.0.0/24 |
| Elk VM   | No                  | 10.0.0.4        10.0.0.0/24 |
| Web 1 VM | No                  | 10.0.0.4        52.188.6.89 |
| Web 2 VM | No                  | 10.0.0.4        52.188.6.89 |
```

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Having Ansible automate the configuration of the ELK was advantageous because if we had to do this  with multiple virtual machines it would take time to set them up one by one. By using Ansible we can set up multiple virtual machines and feel confident in knowing that all the VM's are configured the same.

The playbook implements the following tasks:
- _
- Install docker.io
- Install pip3, which will allow us to run the VM
- Install Docker python module
- Upgrade the allowed memory
- Download and run Docker container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker ps Screenshot](~System/Users/ganneheim/Desktop/Jessies/HW/Unit13HW/Images/Docker_ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web 1 10.0.0.7, and Web 2 10.0.0.8

We have installed the following Beats on these machines:
- Metricbeat and Filebeat on the Elk Virtual Machine

These Beats allow us to collect the following information from each machine:
-Filebeat monitors log files, and log events on a specified location, and forwards collected data to Elasticsearch.   
-Metricbeat monitors a server, collecting metrics and statistics on systems and services running on that server. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration file to the Ansible container.
- Update the configuration file to include Elk VM IP address.
- Run the playbook, and navigate to http://[your.VM.IP]:5601/app/kibana to check that the installation worked as expected.

- _The playbook file is a ".yml" file that Ansible uses to configure virtual machines. While in Ansible, you copy the .yml file from /etc/ directory to specified directory within the /etc/ directory on the virtual machine. 
- _First you have to update, or modify the configuration file for both Filebeat and Metricbeat by adding the ELK VM IP address to allow connection from Web VM's to the ELK server. And by naming the hosts line in the playbook files to webservers tells Ansible where to run the respective playbooks on a specific machine. 
- _To check that the ELK server is running as intended, navigate to http://[your.VM.IP]:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
-To download the config file for Filebeat, use curl command. 
Run the following: curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat >> /etc/ansible/filebeat-config.yml
-To update/ edit config. files use nano. Run the following: nano /etc/ansible/filebeat-config.yml
-To run Playbook file use following command: ansile-playbook [nameofplaybook.yml]