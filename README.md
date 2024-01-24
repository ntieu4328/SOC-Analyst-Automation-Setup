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

9. ssh into aws wazuh server
10. apt-get update && apt-get upgrade
11. install using this link
    https://documentation.wazuh.com/current/quickstart.html
