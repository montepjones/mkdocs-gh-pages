To configure **SFTP access** on **appserver** in **company-name Datacenter**, follow these steps:

### **1. Create the SFTP User**
Run:
```bash
sudo useradd -m -g ftp -s /sbin/nologin james
echo "GyQkFRVNr3" | sudo passwd james --stdin
```
This creates the user `james`, assigns it to the `ftp` group, and disables SSH shell access.

### **2. Enable Password Authentication**
Edit the SSH configuration file:
```bash
sudo nano /etc/ssh/sshd_config
```
Ensure the following lines exist:
```
PasswordAuthentication yes
PermitRootLogin no
```
Save and exit.

### **3. Restrict User to SFTP Only**
Add the following lines at the end of `/etc/ssh/sshd_config`:
```
Match User james
ChrootDirectory /home/james
ForceCommand internal-sftp
AllowTcpForwarding no
X11Forwarding no
```
Save and exit.

### **4. Restart SSH Service**
```bash
sudo systemctl restart sshd
```

### **5. Verify SFTP Access**
Test the connection:
```bash
sftp james@<server-ip>
```

This ensures **SFTP access is enabled**, password authentication works, and `james` can only use **SFTP**. 🚀 Let me know if you need further customization! You can also check out [this guide](https://www.baeldung.com/linux/secure-file-transfer-protocol-create-user) for more details.

This error occurs because **the ChrootDirectory must be owned by root** and **must not be writable by any other user or group**. To fix it, follow these steps:

### **1. Set Correct Ownership**
Run:
```bash
sudo chown root:root /home/james
```

### **2. Set Correct Permissions**
Run:
```bash
sudo chmod 755 /home/james
```
This ensures that `/home/james` is **owned by root** and **not writable by any other user**.

### **3. Create a Writable Directory for James**
Since `james` cannot write to `/home/james`, create a subdirectory:
```bash
sudo mkdir /home/james/uploads
sudo chown james:ftp /home/james/uploads
sudo chmod 755 /home/james/uploads
```
This allows `james` to upload files inside `/home/james/uploads`.

### **4. Restart SSH Service**
```bash
sudo systemctl restart sshd
```

Now, try connecting via **SFTP** again. 🚀 Let me know if you need further assistance! You can also check out [this guide](https://serverfault.com/questions/584986/bad-ownership-or-modes-for-chroot-directory-component) for more details.