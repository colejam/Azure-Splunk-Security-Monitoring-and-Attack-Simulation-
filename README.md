# Azure-Splunk-Security-Monitoring-and-Attack-Simulation-

Installed Windows Server 2022 onto a virtual machine using a hypervisor (VMWARE Fusion). Installed Active Directory to created organizational units and users. 
![AD](https://github.com/user-attachments/assets/775610bc-f1fe-4c37-9cc4-4cefc82c66fc)

Windows 10 machine that allows me to logon as a different users.
<img width="1440" alt="Ronni User" src="https://github.com/user-attachments/assets/b27c62c9-7502-41bf-9d87-99a9752e1a0b">



Install the Splunk Enterprise using the download or wget link for the corresponding operating system. Install the package once downloaded.

```
wget -O splunk-9.3.0-51ccf43db5bd-linux-2.6-amd64.deb "https://download.splunk.com/products/splunk/releases/9.3.0/linux/splunk-9.3.0-51ccf43db5bd-linux-2.6-amd64.deb"
sudo dpkg -i splunk-9.3.0-51ccf43db5bd-linux-2.6-amd64.deb
```


Create the Administrator username and strong password. For great security practices create a user account with limited privilieges to refrain from using the adminstrator account.
```
sudo /opt/splunk/bin/splunk add user <username> -password <password> -role <role>
```
Install Sysinternals Sysmon on both the Windows 10 and Windows server. We will use the sysmon configuration xml file from Olaf. 
```
https://github.com/olafhartong/sysmon-modular
```

<img width="1440" alt="SysmonConfig" src="https://github.com/user-attachments/assets/5ed8fc53-930e-454c-b426-1d1d89f2d68e">



Install the Splunk Universal Forwarder on both the Windows 10 machine and the Windows server. Once the forwarder is installed, set the receiving index IP address to the Splunk server address and set the receiving port to 9997. Finally, change the Splunk Forwarder settings in Services to "Local System" and then restart the Splunk Forwarder.



<img width="1440" alt="SplunkForwarder Restart" src="https://github.com/user-attachments/assets/ae98dbbc-9c8a-4edf-a156-bc68478a70f9">
