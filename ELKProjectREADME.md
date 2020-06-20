## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://drive.google.com/file/d/1FfKXkKVioxDAxLgL-tBmnhSkHNqsK3l6/view?usp=sharing (network diagram on google drive)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._
  - To deploy Filebeat
    -filebeat-config.yml
    -filebeat-playbook.yml
        -to run the playbook: ansible-playbook filebeat-playbook.yml (path must bewhere the plybook YAML is located)
 - To deploy Metricbeat
    -metricbeat-config.yml
    -metricbeat-playbook.yml
        -to run the playbook: ansible-playbook metricbeat-playbook.yml (path must bewhere the plybook YAML is located) 

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
Load balancers help to eliminate single points of failure by reducing the attack surface, making it harder to exhaust resources. 
The primary advantage of a jump box is you can quickly configure additional resources added to a network to complete the tasks you require.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for?_Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash.
- _TODO: What does Metricbeat record?_ Metricbeat collects and ships various system and service metrics to a specified output destination. Used to monitor system CPU, memory, and load on a server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| DVWA-VM1 | Webserver| 10.0.0.5   | Linux            |
| DVWA-VM1 | Webserver| 10.0.0.6   | Linux            |
| ELKStack | Server   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _____ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_
70.94.198.204

Machines within the network can only be accessed by _____SSH.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 52.152.164.180       |
| DVWA-1   | No                  | 10.0.0.5             |
| DVWA-2   | No                  | 10.0.0.6             |
| ELKStack | Yes                 | 40.91.102.160        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
Automated configuration makes it possible to provision many machines simultaneously and be deployed quickly in a production environment 

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install Docker.io to the server
- Install python3-pip
- Download and launch the sebp/elk container to the server

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
https://drive.google.com/file/d/1Em3yWwKWgqip6vWEDomPSD7_nS_6_oX2/view?usp=sharing (google drive link for docker ps output)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
- DVWA-VM1 10.0.0.5
- DVWA-VM2 10.0.0.6

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
- DVWA-VM1 - Filebeats, Metricbeats
- DVWA-VM2 - Filebeats, Metricbeats

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
- Filebeat is a lightweight shipper for forwarding and centralizing log data. (www.elastic.co/guide/en/beats/filebeat/current/file-overview.html)
- Metricbeat collects system and service metrics to monitor the performance of a specified machine.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____.yml file to _____/etc/ansible.
- Update the _____ ansible.cfg file to include...accepted usernames for remote access
- Run the playbook, and navigate to ____ [the target machine] to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_ 
    - .yml copied to /etc/ansible in the ansible container
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ 
    - /etc/ansible/hosts target machines can be grouped together by specifying the group [groupname] and the IP's of the machines in that group [10.1.0.4]
- _Which URL do you navigate to in order to check that the ELK server is running?
    - http://[ELKServerIP]:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
