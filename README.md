# SOC-Analyst-Automation-Setup

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
