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
12. After adding a 2 GB disk to the machine, create two partitions of 1 GB each with automatic punting after reboot.
13. Check the technical condition of this disk with smartctl.
14. Create the Guests group and the Guest-1 user with a home directory for which the maximum number of days between password changes is 5 days.
15. Assign the Guest-1 account to the Guests group.
16. In the Guest-1 home directory, create a hidden documents directory and give it full rights for the Guests group.
17. Create files file-1, file-2 and file-3 in Guest-1's home directory. Then create a compressed .tar.gz archive from these files.
18. Log in as root.
19. Execute the command alias top -b -n 1 | head -n 17
20. Check the complete information about the system kernel.
21. Check the version and name of the distribution.
22. Check system uptime and load.
23. Check what uses the most RAM.
24. Check the parameters of the motherboard, processor, RAM, network cards.
25. Check the sysk and partition structure.
26. Check the active connection and listening ports.
27. View system logs.
28. View kernel messages.





