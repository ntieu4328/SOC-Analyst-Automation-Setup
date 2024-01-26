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

```bash
sudo apt-get update
```
1. make windows vm

2. on the vm dowload sysmon
https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon

3. open powershell

4. go into the folder with the sysmon

5. C:\Users\ntieu\DownloadsSysmon\
6. .\sysmon64.exe -i
7. verify that sysmon is installed
8. create aws ec2 instance
   settings:
     ubuntu 22.04
   at least 8 gib ram
   50 gib storage
   security groups fully open for both thehive and wazuh
   
10. ssh into aws wazuh server
11. apt-get update && apt-get upgrade
12. install using this link
    https://documentation.wazuh.com/current/quickstart.html

make aws TheHive Server
has to be at least 4 CPU 16 gib ram
I used t2.xlarge
install using this link:
https://docs.strangebee.com/thehive/setup/#operating-systems

Login to wazuh using the information that was given

Create Wazuh agent with these settings:
windows: MSI 32/64 bits
server address: public IPv4 of the wazuh ec2 instance
Agent name: Whatever you want
Install the agent using the command given:

Start the agent:
NET START WazuhSvc

Show that agent shows active

integrate wazuh into thehive:
https://wazuh.com/blog/using-wazuh-and-thehive-for-threat-protection-and-incident-response/

wazuh:
https://IP:443

thehive:
http://IP:9000
