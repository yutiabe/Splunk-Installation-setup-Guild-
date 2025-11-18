# Splunk-Installation-setup-Guild-
This is a Project for my home Lab, my splunk server is running on Alma Linux 9.6 on a KVM hypervisor.

<img width="956" height="459" alt="image" src="https://github.com/user-attachments/assets/d654e50a-42f6-400e-80f3-b501ad6e2f78" />
Do not install spunk as a root user.
Download the package:
sudo wget -O splunk-10.0.1-c486717c322b.x86_64.rpm "https://download.splunk.com/products/splunk/releases/10.0.1/linux/splunk-10.0.1-c486717c322b.x86_64.rpm"
provide passwd for the splunk user:
<img width="975" height="191" alt="image" src="https://github.com/user-attachments/assets/71ca9a90-e054-4c50-b19c-c91f72852e90" />
Install the package  as a splunk user, this will require splunk user password
# sudo rpm -ivh splunk-10.0.1-c486717c322b.x86_64.rpm
sudo rpm -ivh splunk-10.0.1-c486717c322b.x86_64.rpm
[sudo] password for splunk:

<img width="975" height="243" alt="image" src="https://github.com/user-attachments/assets/16333434-a887-4b79-991e-8908e2ac7eb7" />

Enable splunk to start at boot
cd /opt/splunk/bin
sudo ./splunk enable boot-start 
NB provide passswd for slunk user and also a new username and passwd for admin account
Change permission for splunk user 
# sudo chown -R splunk:splunk /opt/splunk
# If you encounter any issue and want to change anything, Make sure to stop splunk services before making the change
sudo /opt/splunk/bin/splunk stop.
sudo systemctl start Splunkd.
sudo /opt/splunk/bin/splunk enable boot-start -systemd-managed 1 -user splunk.
# Check the firewall status
# sudo systemctl status firewalld
The most common Splunk ports are:
8000/tcp: The default port for the Splunk Web interface.
communication between Splunk components
- Search
- Heads
- Indexers
- Forwarders.
# 9997/tcp: The default port for receiving data from Splunk universal forwarders. 
You must add these ports to the public firewall zone. The --permanent flag ensures the rule persists after a server reboot.
# Open the Splunk Web port
sudo firewall-cmd --zone=public --add-port=8000/tcp --permanent
# Open the Splunk management port
sudo firewall-cmd --zone=public --add-port=8089/tcp --permanent
# Open the Splunk forwarder receiving port
sudo firewall-cmd --zone=public --add-port=9997/tcp –permanent
Reload the firewall
#sudo firewall-cmd --reload
Go to your web browser , open a new tap
Enter the server ip and the port number eg( 10.0.0.25:8000)
Dashboard 
<img width="975" height="311" alt="image" src="https://github.com/user-attachments/assets/bea2dae8-cf00-4024-a1a6-1131ab1f0b87" />




