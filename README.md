# Azure-Splunk-Security-Monitoring-and-Attack-Simulation-

Installed Windows Server 2022 on a virtual machine using VMware Fusion. Set up Active Directory to create organizational units and users.
![AD](https://github.com/user-attachments/assets/775610bc-f1fe-4c37-9cc4-4cefc82c66fc)

A Windows 10 machine that allows me to logon as a different users.
<img width="1440" alt="Ronni User" src="https://github.com/user-attachments/assets/b27c62c9-7502-41bf-9d87-99a9752e1a0b">



Download Splunk Enterprise using the download or wget link for the corresponding operating system. Once downloaded, install the package.

```
wget -O splunk-9.3.0-51ccf43db5bd-linux-2.6-amd64.deb "https://download.splunk.com/products/splunk/releases/9.3.0/linux/splunk-9.3.0-51ccf43db5bd-linux-2.6-amd64.deb"
sudo dpkg -i splunk-9.3.0-51ccf43db5bd-linux-2.6-amd64.deb
```


Create the Administrator username and strong password. For great security practices, create a user account with limited privilieges to refrain from using the adminstrator account.
```
sudo /opt/splunk/bin/splunk add user <username> -password <password> -role <role>
```


<img width="1440" alt="Splunk User" src="https://github.com/user-attachments/assets/5a744097-cfb3-4467-84cc-f0b15bd51411">



Install Sysinternals Sysmon on both the Windows 10 and Windows server. We will use the sysmon configuration xml file from Olaf. 
```
https://github.com/olafhartong/sysmon-modular
```

<img width="1440" alt="SysmonConfig" src="https://github.com/user-attachments/assets/5ed8fc53-930e-454c-b426-1d1d89f2d68e">



Install the Splunk Universal Forwarder on both the Windows 10 machine and the Windows server. Once the forwarder is installed, set the receiving index IP address to the Splunk server address and set the receiving port to 9997. Finally, change the Splunk Forwarder settings in Services to "Local System" and then restart the Splunk Forwarder.



<img width="1440" alt="SplunkForwarder Restart" src="https://github.com/user-attachments/assets/ae98dbbc-9c8a-4edf-a156-bc68478a70f9">

<img width="1440" alt="Remote Access" src="https://github.com/user-attachments/assets/a630147c-0c06-4c64-a9c0-cdeea056d026">



Update and upgrade the repositories on Kali Linux. Then, install Crowbar, which will be used to conduct the brute force attack against RDP.

```
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install -y crowbar
```

Create a new directory called AD-Project inside the Desktop directory. Then, locate the rockyou.txt.gz file by navigating to the /usr/share/wordlists/ directory. Once the file is unzipped, copy it into the AD-Project directory.


```
cd Desktop
mkdir AD-Project
cd /usr/share/wordlist/
sudo gunzip rockyou.txt.gz
cp rockyou.txt ~/Desktop/AD-Project
```

To use only the first 20 words in rockyou.txt, use the head command to create a smaller password list. Then edit the txt file to insert the correct password for testing purposes.

```
head -n 20 rockyou.txt > passwords.txt
nano passwords.txt
```
Testing for connectivity between the attacking and victim machine. 
<img width="1440" alt="Ping" src="https://github.com/user-attachments/assets/805a45fa-e917-4ae8-9bb1-6c75cfaa84a3">



Utilized Nmap for enumeration to determine which ports where opened and the services running. 
<img width="1440" alt="Nmap" src="https://github.com/user-attachments/assets/cd096487-1471-4d60-8e27-b55a32029ec5">



Performed a brute force attack on RDP using Crowbar. 
<img width="1440" alt="Crowbar" src="https://github.com/user-attachments/assets/d34df61d-52d4-46ec-af93-2883ae0058c9">


Used Splunk to analyze the failed logon attempt.
<img width="1440" alt="Splunk-Fail" src="https://github.com/user-attachments/assets/9b012dce-3779-4afe-b90e-e2fb4bba54ec">

Used Splunk to analyze the successful logon attempt.
<img width="1440" alt="Splunk-success" src="https://github.com/user-attachments/assets/02c8d35a-086b-4fd5-ad29-0ba3a1a22965">

