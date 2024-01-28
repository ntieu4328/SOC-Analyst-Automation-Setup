<h1>SOC Analyst Automation Setup</h1>

<h2>Description:</h2>

This project consists of setting up and configuring the environments for the project. I will be making 2 AWS EC2 instances, 1 Windows 10 Virtual Machine, and 1 Linux Virtual Machine. One AWS EC2 instance will run Wazuh. Another AWS EC2 instance will run TheHive. The Windows 10 Virtual Machine will be used to simulate an endpoint user that I'm trying to protect. The Linux Virtual Machine that I will run will be Kali Linux. The Kali Linux machine will be where I configure all the SIEM tools and view the data that is collected.

<h2>Environments Used:</h2>

   - Virtualbox
   - AWS EC2 instance
   - Ubuntu 22.04
   - Windows 10
   - Kali Linux

<h2>Walk-through:</h2>

<b>IMPORTANT</b> Create a NAT Network:

   - File -> Tools -> Network Manager -> NAT Networks -> Create
   - Name: Whatever you want
   - Keep everything else default
<br>

Create a Kali Linux virtual machine using my guide:

   - [Kali Linux Creation Guide]()
   - <b>IMPORTANT</b> Settings -> Network -> (Attached to: NAT Network) & (Name: Whatever name you put)
<br>

Create a Windows 10 virtual machine:

   - Download the [Windows 10 Iso](https://www.microsoft.com/en-us/software-download/windows10) file 
   - Adapt the [Kali Linux creation Guide](https://github.com/ntieu4328/Virtual-Box-Kali-Linux) for the Windows 10 virtual machine
   - <b>IMPORTANT</b> Settings -> Network -> (Attached to: NAT Network) & (Name: Whatever name you put)
   - <b>IMPORTANT</b> Settings -> Storage:

![windows 10 storage](https://github.com/ntieu4328/SOC-Analyst-Automation-Setup/assets/156137990/c409afcb-03f4-47d2-9460-5c3ff46c29df)
<br>
<br>

Create 2 AWS EC2 Servers with the same setting:

Guide: [AWS Server](https://github.com/ntieu4328/AWS-EC2-Server)
   
Settings:
   
   - Application and OS Images: Ubuntu Server 22.04 LTS
   - Instance type: t2.xlarge
   - Configure Storage: 50 GiB gp3

Security Group Settings:

   Inbound rule 1:
   
   - Type: All TCP
   - Source type: Anywhere-IPv4
      
   Inbound rule 2:
   
   - Type: All UDP
   - Source type: Anywhere-IPv4
<br>

<h2>Wazuh Setup</h2>

1. SSH into the AWS EC2 Server that will be running Wazuh
   
2. Go into root user:

```bash
sudo su
```
   
3. Update and upgrade the server:

```bash
apt-get update && sudo apt-get upgrade
```

4. Install Wazuh:

[Wazuh Install Documentation](https://documentation.wazuh.com/current/quickstart.html)

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
```

5. Using the login information given after installation, login to Wazuh in a web browser:

*For the <wazuh-dashboard-ip> input the public IPv4 of the AWS EC2 server that Wazuh is run on.

![wazuh login info](https://github.com/ntieu4328/SOC-Analyst-Automation-Setup/assets/156137990/9501362e-a065-4374-ac7f-3e24cf09c0fb)

![wazuh login page](https://github.com/ntieu4328/SOC-Analyst-Automation-Setup/assets/156137990/6d4eb03d-c6b9-4926-a9f6-839437dce9b8)

![wazuh starting menu](https://github.com/ntieu4328/SOC-Analyst-Automation-Setup/assets/156137990/1af17b3d-66e2-434b-9aa9-2b4026719bff)
<br>
<br>


<h2>TheHive Setup</h2>

1. SSH into the AWS EC2 Server that will be running TheHive
   
2. Go into root User:

```bash
sudo su
```

3. Update and upgrade the server:

```bash
apt-get update && sudo apt-get upgrade
```

4. Install TheHive:

[TheHive Install Documentation](https://docs.strangebee.com/thehive/setup/#operating-systems)

```bash
wget -q -O /tmp/install.sh https://archives.strangebee.com/scripts/install.sh ; sudo -v ; bash /tmp/install.sh
```

5. Using the login information given after installation, login to TheHive in a web browser:

*For the IP to input, switch 172.31.24.221 with the public IPv4 of the AWS EC2 server that TheHive is run on.

![TheHive login info](https://github.com/ntieu4328/SOC-Analyst-Automation-Setup/assets/156137990/1dcc39fa-ca21-49f8-89f3-1a402bad2133)

![TheHive login page](https://github.com/ntieu4328/SOC-Analyst-Automation-Setup/assets/156137990/58886ee2-48c4-4037-b3f2-5d6627702a1c)

![TheHive starting menu](https://github.com/ntieu4328/SOC-Analyst-Automation-Setup/assets/156137990/7fa74a94-e12e-48c1-8177-a87e337c652c)
<br>
<br>


<h2>Integrate TheHive with Wazuh:</h2>

Follow the instructions:

[Integration Documentation](https://wazuh.com/blog/using-wazuh-and-thehive-for-threat-protection-and-incident-response/)

