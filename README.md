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
semanage port -a -t ssh-port_t -p tcp 14355
```
Restarting the sshd service.
```bash
systemctl restart sshd
```
