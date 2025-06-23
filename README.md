# Introduce to Rocky Linux 
## How to secure Rocky Linux 9
### Logging failed login attempts to a text file.  
```bash
grep "Failed password" /var/log/secure > failed-password.txt 
```
### Changing the SSH port  
In any text editor, open the file /etc/ssh/sshd_config.
```bash
nano /etc/ssh/sshd_config
```
Find the line with #Port 22 remove # and change it to example Port 14355.
Check the current SELinux mode:
```bash
sestatus
```
Be sure to add port 14355 to SELinux. Replace &lt;type&gt;, &lt;protocol&gt;, and &lt;port_number&gt; in command semanage port -a -t &lt;type&gt; -p &lt;protocol&gt; &lt;port_number&gt;.
```bash
semanage port -a -t ssh_port_t -p tcp 14355
```
Change the Firewall
```
sudo firewall-cmd --permanent --add-port=14355/tcp
sudo firewall-cmd --reload
```
Restarting the ssh service.
```bash
systemctl restart sshd
```
### Blocking root login via SSH
In any text editor, open the file /etc/ssh/sshd_config.
```bash
nano /etc/ssh/sshd_config
```
Find the line shown below:  
PermitRootLogin yes  
Change the value from yes to no. Save and close the file. Then restart the SSH service.  
```bash
systemctl restart sshd
```
## Introductory scenario
1. Check if Apache is running and set static IP addresses on the interface.
2. Create the main directory /www and subpages in this directory /sport and /weather
3. Create index.html files in the main directory and subpages.
4. Set permissions.
5. Configure Apache VirtualHosts on port 100.
6. Set up Apache on port 100.
7. Allow access through port 100 in firewalld
8. Configure SELinux to allow Apache to use non-standard ports.
9. Configure access to the website located in the user's directory via the userdir module.
10. Restart Apache.
11. Test access to websites.