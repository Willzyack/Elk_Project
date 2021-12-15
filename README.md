## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Diagram for Project](https://github.com/Willzyack/Elk_Project/blob/main/Diagrams/Project_Diagram_Final.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yaml file may be used to install only certain pieces of it, such as Filebeat.

<b>ELK Playbook</b>

![Install ELK Playbook](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/Install_Elk_Playbook.PNG)

<b>Filebeat Playbook</b>

![Install Filebeat](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/Filebeat_Playbook.PNG)

<b>Metricbeat Playbook</b>

![Install Metricbeat](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/MetricBeat_Playbook.PNG)

<b>Web Server Settings Playbook</b>

![Web Servers Settings Playbook](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/My_Playbook.PNG)

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

<b>-What aspect of security do load balancers protect?-</b>

Load balancers defends the organization against DDoS attacks by shifting attack traffic away from the organization's server to a public cloud server.

<b>-What is the advantage of a jump box?- </b>

The advantage of a jump box is that it allows user(s) to connect to a secure computer via SSH where no other protocols are allowed outbound to the Internet or into the organization's network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.

<b>-What does Filebeat watch for?-</b>

Filebeat collects log events based on changes to the log files or locations that you specify.

<b>-What does Metricbeat record?-</b>

Metricbeat records the metrics and statistics that it collects and ships them to a specified output location.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name               | Function                                        | IP Address | Operating System                   |
|--------------------|-------------------------------------------------|------------|------------------------------------|
| JumpBoxProvisioner | Gateway (Includes Ansible and Docker Containers)| 10.0.0.1   | Linux (Ubuntu 18.04 LTS)           |
| Web1               | Server (Includes DVWA Container)                | 10.0.0.5   | Linux (Ubuntu 18.04 LTS)           |
| Web2               | Server (Includes DVWA Container)                | 10.0.0.6   | Linux (Ubuntu 18.04 LTS)           |
| Web3               | Server (Includes DVWA Container)                | 10.0.0.7   | Linux (Ubuntu 18.04 LTS)           |
| ElkServer          | Monitoring Server (Includes ELK Container)      | 10.1.0.4   | Linux (Ubuntu 18.04 LTS)           |
 
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBoxProvisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- Will's Public IP Address

Machines within the network can only be accessed by JumpBoxProvisioner.

<b>-Which machine did you allow to access your ELK VM? What was its IP address?-</b>

My personal machine is allowed to access my ELK VM via my public IP address over port 5601.

A summary of the access policies in place can be found in the table below.

| Name                | Publicly Accessible | Allowed IP Addresses |
|---------------------|---------------------|----------------------|
| JumpBoxProvisioner  | Yes                 | Will's Public IP     |
| Web1                | No                  | 10.0.0.4             |
| Web2                | No                  | 10.0.0.4             |
| Web3                | No                  | 10.0.0.4             |
| ElkServer           | Yes                 | Will's Public IP     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

<b>-What is the main advantage of automating configuration with Ansible?-</b>

The main advantave of automating configurations with Ansible is that it ensures that the provisioning scripts run identically everywhere.

The playbook implements the following tasks:

<b>-In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.-</b>

- Increase virtual memory to "262144" and install docker.io, python3-pip, and Python Docker via a playbook. (Screenshot shown below)
- Download the sebp/elk:761 image. (Shown in screenshot under "name: download and launch a docker web container")
- Enable docker services. (Shown in screenshot under "name: Enable docker services")

![ELK Playbook Screenshot](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/Install_Elk_Playbook.PNG "ELK Playbook")

- While in the Ansible container, SSH into the ELK server 
  - ssh [username@Elk.Server.Address]
- Run the following command to verify that the sebp/elk:761 container is running in the command line.
  - docker ps

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps Screenshot](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/elk_playbook.PNG "docker ps Screenshot")

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

<b>-List the IP addresses of the machines you are monitoring-</b>

The following web servers are being monitored: 10.0.0.5, 10.0.0.6, 10.0.0.7

<b>-We have installed the following Beats on these machines:-</b>

We installed Filebeat and Metricbeat.

<b>-These Beats allow us to collect the following information from each machine:-</b>

Filebeat collects system type events on the three web servers by monitoring the Elasticsearch log files. Metricbeat collects metrics on the three web servers such as uptime, CPU usage, and memory usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk file to /etc/ansible/.
- Update the host file to include the ELK server IP address and to specify python3.

- Run the playbook, and navigate to HTTP://<ELKServer_Public_IP>:5601 to check that the installation worked as expected.

<b>_Answer the following questions to fill in the blanks:_</b>

<b>-Which file is the playbook? Where do you copy it?-</b>

The file is [install-elk.yml](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/Install_Elk_Playbook.PNG). You copy it into /etc/ansible

<b>-Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?-</b>

The file you update to make Ansible run the playbook is the hosts file. The ELK server and web servers are listed seperately in the hosts file.

<b>-Which URL do you navigate to in order to check that the ELK server is running?-</b>

HTTP://<ELKServer_Public_IP>:5601

<b>-As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.-</b>

- Login to your jump box via command line.
  - ssh [username@Jump.Box.IP]
- List your container list to find the one you should connect to. 
  - sudo docker container list -a
- Start your docker.
  - sudo docker start [container_name]
- Attach to the docker.
  - sudo docker attach [container_name]
- Head to /etc/ansible/
  - cd /etc/ansible/
- Open the host file and add the ELK attribute and it's IP address.
  - nano /etc/ansible/host
  - Add the ELK group and it's IP address like shown below.
    ![host](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/Hosts_Final.PNG)
- To download the playbook, create a new file via nano, and copy the playbook information from the screenshot below (the spacing is important, try to copy exactly).
  - nano /etc/ansible/install-elk.yml
    ![install-elk](https://github.com/Willzyack/Elk_Project/blob/main/Ansible/Install_Elk_Playbook.PNG) 
- From the Ansible container, connect to your new ELK server.
  - ssh [username@ELK.Server.IP]
- Verify the sebp/elk:761 container is running correctly
  - docker ps
