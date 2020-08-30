## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/rcasti11/Project_I/blob/master/Project_I/Diagrams/Project%20Diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible files may be used to install only certain pieces of it, such as Filebeat.

  - ELK_Playbook.yml
  - Filebeat_Playbook.yml
  - JumpBox_Playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting traffic to the network.
- Load Balancers protect the availability of resources by ensuring that the resource does not get overwhelmed. The advantage of a jump box is that it acts as a gateway to the security-sensitive locations that a system admin may need to access.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the machine and system files.
- Filebeat is a logging agent that watches and ships log files to Logstash for further processing, or to Elasticsearch for indexing. 
- Metricbeat collects a machine's metrics and statistics, such as uptime and CPU usage. Metricbeat helps monitor servers by collecting metrics from the system and services running on the server.

The configuration details of each machine may be found below.


| Name       | Function   | IP Address | Operating System |
|------------|------------|------------|------------------|
| Jump Box   | Gateway    | 10.1.0.4   | Linux            |   
|------------|------------|------------|------------------|
| ELK Server | Kibana IDS | 10.0.0.4   | Linux            |   
| Web-3      | Web Server | 10.1.0.7   | Linux            |   
| Web-4      | Web Server | 10.1.0.8   | Linux            |   

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 75.111.24.5

Machines within the network can only be accessed by the Jump Box Provisioner.
- The Jump Box Provisioner is the only machine that can access the ELK VM. The IP address of the Jump Box Provisioner is 40.83.163.44.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 75.111.24.5          |
| Web-3    |  No                 | 40.83.163.44         |
| Web-4    |  No                 | 40.83.163.44         |
| ELK      |  No                 | 40.83.163.44         |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it mitigates the chance of user error from the administrator's behalf. Additionally, Ansible is meant to update multiple servers with groups of different rules.

The playbook implements the following tasks:
- Install Docker.io
- Install pip3
- Install Docker Python Module
- Increase Virtual Memory
- Use More Memory
- Download and Launch an ELK container within Docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/rcasti11/Project_I/blob/master/Project_I/Diagrams/Docker%20PS%20.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-3 138.91.173.150 (Public) | 10.1.0.7 (Private)
- Web-4 138.91.173.150 (Public) | 10.1.0.8 (Private)

We have installed the following Beats on these machines:
- Filebeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects logs such as audit logs, depreciation logs, gc logs, server logs, and slow logs. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ELK_playbook.yml file to /etc/ansible.
- Update the hosts file within that directory to include the private IP address of Web-3, Web-4, and the ELK server. They are 10.1.0.7 , 10.1.0.8, and 10.0.0.4 respectively.
- Run the playbook, and navigate to http://<Elk Public IP>:5601/app/kibana#/home?_g=() to check that the installation worked as expected.
