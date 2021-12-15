## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Network Diagram for Project](https://github.com/Willzyack/Elk_Project/blob/main/Diagrams/Project_Diagram_Final.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yaml file may be used to install only certain pieces of it, such as Filebeat.

[Install Elk Playbook](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/Install_Elk_Playbook.PNG)
[Install Filebeat](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/Filebeat_Playbook.PNG)
[Install Metricbeat](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/MetricBeat_Playbook.PNG)
[Webservers Settings Playbook](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/My_Playbook.PNG)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly availble, in addition to restricting access to the network.

-What aspect of security do load balancers protect?-

Load balancers defends the organization against DDoS attacks by shifting attack traffic away from the organization's server to a public cloud server.

-What is the advantage of a jump box?-

The advantage of a jump box is that it allows user(s) to connect to a secure computer via SSH where no other protocols are allowed outbound to the Internet or into the orgnaization's network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.

-What does Filebeat watch for?_
Filebeat collects log events based on changes to the log files or locations that you specifiy.

- _TODO: What does Metricbeat record?_
Metricbeat records the metrics and statistics that it collects and ships them to a specified output location.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name               | Function | IP Address | Operating System |
|--------------------|----------|------------|------------------|
| JumpBoxProvisioner | Gateway  | 10.0.0.1   | Linux            |
| Web1               | Server   | 10.0.0.5   | Linux            |
| Web2               | Server   | 10.0.0.6   | Linux            |
| Web3               | Server   | 10.0.0.7   | Linux            |
| ElkServer          | Server   | 10.1.0.4   | Linux            |
 
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBoxProvisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Will's Public IP Address

Machines within the network can only be accessed by JumpBoxProvisioner.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
My personal machine is allowed to access my ELK VM via my public IP address over port 5601.

A summary of the access policies in place can be found in the table below.

| Name                | Publicly Accessible | Allowed IP Addresses |
|---------------------|---------------------|----------------------|
| JumpBoxProvisioner  | Yes                 | Will's Public IP     |
| Web1                | No                  | 10.0.0.4             |
| Web2                | No                  | 10.0.0.4             |
| Web3                | No                  | 10.0.0.4             |
| ElkServer           | No                  | Will's Public IP     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
The main advantave of automating configurations with Ansible is that it ensures that the provisioning scripts run identically everywhere.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...Install docker.io, python3-pip, and Python Docker via a playbook. (Screenshot shown below)
- ...Download the sebp/elk:761 image. (Shown in screenshot under "name: download and launch a docker web container")
- ...Enable docker services. (Shown in screenshot under "name: Enable docker services")
![ELK Playbook Screenshot](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/Install_Elk_Playbook.PNG "ELK Playbook")
- ...While in the Ansible container, SSH into the ELK server ("ssh username@Elk.Server.Address")
- ...Run "docker ps" to verify that the sebp/elk:761 container is running.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps Screenshot](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/elk_playbook.PNG "docker ps Screenshot")

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
The following 3 Web servers are being monitored: 10.0.0.5, 10.0.0.6, 10.0.0.7

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
We installed Filebeat and Metricbeat.

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat collects system type events on the three Web servers by monitoring the Elasticsearch log files. Metricbeat collects metrics on the three Web servers such as CPU and Memory usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk file to /etc/ansible/roles/.
- Update the host file to include the Elk server IP address and to specify python3.

- Run the playbook, and navigate to HTTP://<ELKServer_Public_IP>:5601 to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
The file is [install-elk.yml](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/Install_Elk_Playbook.PNG). You copy it into /etc/ansible

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
The file you update to make Ansible run the playbook is the hosts file. The ELK server and Web servers are listed seperately in the hosts file.

- _Which URL do you navigate to in order to check that the ELK server is running?
HTTP://<ELKServer_Public_IP>:5601

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
Down
