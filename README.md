[README.md](https://github.com/Calvin-A-Cyber/University-of-Denver-Course-Work/files/7229045/README.md)
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

! https://github.com/Calvin-A-Cyber/University-of-Denver-Course-Work/blob/main/Images/Diagrams/Creating-Deploying%20an%20ELK%20Stack.drawio.png

***The proper format was not working, so I put the URL to the image. Just CNTL + Click the link.*** 

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the __YAML__ file may be used to install only certain pieces of it, such as Filebeat.

  - Calvin-A-Cyber/University-of-Denver-Course-Work/Ansible/Filebeat-Playbook.yml

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

- A load balancer protects the network by sitting in front of the servers and routes internet traffic to a certain server depending on the availability of that server. So, a load balancer can protect a network against DDOS (Denial of  Service) attacks by routing traffic in a way that does not shut down servers from too many requests. 
- The advantage of using a Jump-box on your network is huge when talking about cyber security. By using a Jump-box as a secure point for all admins to connect to before jumping into their network, blocks all traffic that is not from that Jump-box from access their network. When critical information is at risk, this can keep it safe from attackers. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the **logs** and system __data__.

- Filebeat watches/collects data about specific logs and files then logs this data, then will package the logs and send them to Elasticsearch in this case for indexing.  
- Metricbeat records information about the operating system and services running on the server/machine. Metricbeat then packages this data and sends it to Elasticsearch in this case.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name           | Function    | IP Address | Operating System       |
| -------------- | ----------- | ---------- | ---------------------- |
| Jump Box       | Gateway     | 10.0.0.4   | Linux Ubuntu 18.04-LTS |
| Web-1          | Webserver 1 | 10.0.0.7   | Linux Ubuntu 18.04-LTS |
| Web-2          | Webserver 2 | 10.0.0.6   | Linux Ubuntu 18.04-LTS |
| Web-3          | Webserver 3 | 10.0.0.9   | Linux Ubuntu 18.04-LTS |
| Project-1-VM-1 | ELK Stack   | 10.1.0.4   | Linux Ubuntu 18.04-LTS |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the **Jump-box** machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- My public IP address (I do not want to disclose this address)

Machines within the network can only be accessed by The Jumpbox.

- The Jump-box is the machine that has access to the ELK Stack VM. The IP address is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name                       | Publicly Accessible | Allowed IP Addresses |
| -------------------------- | ------------------- | -------------------- |
| Jump Box                   | Yes                 | My Public IP Address |
| Web-1                      | No                  | 10.0.0.7             |
| Web-2                      | No                  | 10.0.06              |
| Web-3                      | No                  | 10.0.09              |
| Project-1-VM-1 (ELK Stack) | No                  | 10.0.04              |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

- The main advantage of automating configuration with Ansible is saving time. By deploying Ansible playbooks rather than configuring each machine, saves admins so much time and depending on how many machines they need to configure, this can be a substantial amount of time. Another advantage of using Ansible is cutting out the human error involved with installing applications and configuring computers for each individual employee. Saving even more time with troubleshooting issues by know how each computer has been configured. 

The playbook implements the following tasks:

- Install Docker
- Install Python-3
- Install Docker/Python module
- Increase Virtual Memory Map count to 262144
- Use the Memory up to 262144
- Download and launch the Docker ELK Stack container
- Enable Docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

! https://github.com/Calvin-A-Cyber/University-of-Denver-Course-Work/blob/main/Images/Ansible%20container%20image.PNG 

***The proper format was not working, so I put the URL to the image. Just CNTL + Click the link.***

### Target Machines & Beats

This ELK server is configured to monitor the following machines:

- Web-1 - 10.0.0.7
- Web-2 - 10.0.0.6
- Web 3 - 10.0.0.9

We have installed the following Beats on these machines:

- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat is a log and file monitor and depending on which logs and files we tell filebeat to watch, will determine what is in the data filebeat collects. Filebeat can collect data on audit logs, depreciation logs, gc logs, server logs, etc. Metricbeat is very similar to filebeat, but Metricbeat records information on the system itself, such as how much RAM is being used during a process, or the CPU temperature during a high intensity task. 

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the ELK-Stack-Playbook.yml, Filebeat-Playbook.yml and Metricbeat_Playbook.yml files to /etc/ansible directory.
- Update the Playbook files to include the machine you want to use the playbook on the hosts line, which is the third line from the top. For the ELK-Stack-Playbook my machine is 10.1.0.4 which is under my ELK Webservers in my hosts file. As for the Filebeat and Metricbeat Playbooks, update the third hosts lines to the normal Webservers group that includes Web-1, Web-2 and Web-3.
- **Link to Screenshot of hosts file**: https://github.com/Calvin-A-Cyber/University-of-Denver-Course-Work/blob/main/Images/Hosts%20file.PNG
- Run the playbooks, and navigate to http://ELKStackPublicIP:5601/app/kibana to check that the installations worked as expected.

Answer the following questions to fill in the blanks:

- The playbook files are **ELK-Stack-Playbook.yml**, **Filebeat-Playbook.yml** and **Metricbeat-Playbook.yml**. You copy the playbook files to your /roles directory with this direct path **/etc/ansible/roles**.
- The file you need to update in order to tell Ansible to run a Playbook on a specific machine is first the hosts file. You have to add the machine that you want to run the Playbook on to a group, for the ELK webserver group i added machine 10.1.0.4. To specify which machine to install ELK on versus Filebeat is not in the Playbook files. In the ELK-Stack-Playbook on the third line is the hosts: line. Add the group that you created in the previous step explained above by simply typing in the name of the group and saving the file. Once the files is saved, run the playbook and confirm the script ran correctly. 
- In order to confirm the ELK stack is running properly, navigate the URL http://ELKStackPublicIP:5601/app/kibana and check that data is coming to the ELK server.
