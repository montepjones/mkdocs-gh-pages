To disable direct root SSH login on all app servers within the company-name Datacenter, follow these steps:

### **Step 1: Edit the SSH Configuration File**
Open the SSH configuration file using a text editor:

```sh
sudo nano /etc/ssh/sshd_config
```

### **Step 2: Modify the Root Login Setting**
Find the following line:

```sh
PermitRootLogin yes
```

Change it to:

```sh
PermitRootLogin no
```

If the line doesn't exist, add it manually.

### **Step 3: Save and Exit**
Press `CTRL + X`, then `Y`, and hit `ENTER` to save the changes.

### **Step 4: Restart the SSH Service**
Apply the new settings by restarting SSH:

```sh
sudo systemctl restart sshd
```

### **Step 5: Verify the Configuration**
Run the following command to confirm the change:

```sh
sudo grep PermitRootLogin /etc/ssh/sshd_config
```

This ensures direct root login is disabled.

### **Step 6: Test Access**
Try logging in as root remotely:

```sh
ssh root@server_ip
```

It should now be restricted.

These security measures help prevent unauthorized access and enhance system protection. Let me know if you need any further refinements! 🚀
