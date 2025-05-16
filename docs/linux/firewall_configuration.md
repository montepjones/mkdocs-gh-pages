To **install and configure `firewalld`** for **Nginx** and **Apache** on all app servers in **company-name Datacenter**, follow these steps:

---

### **Step 1: Install `firewalld`**
Run the following on each app server:
```bash
sudo yum install -y firewalld  # RHEL/CentOS
sudo apt update && sudo apt install -y firewalld  # Debian/Ubuntu
```

---

### **Step 2: Start and Enable `firewalld`**
```bash
sudo systemctl start firewalld
sudo systemctl enable firewalld
```
Check status:
```bash
systemctl status firewalld
```

---

### **Step 3: Configure Firewall Rules**
#### **Allow Incoming Connections on Nginx Port (80)**
```bash
sudo firewall-cmd --zone=public --add-port=80/tcp --permanent
```

#### **Block Incoming Connections on Apache Port (8080)**
```bash
sudo firewall-cmd --zone=public --remove-port=8080/tcp --permanent
sudo firewall-cmd --zone=public --add-rich-rule='rule family="ipv4" port protocol="tcp" port="8080" reject' --permanent
```

#### **Reload Firewall to Apply Changes**
```bash
sudo firewall-cmd --reload
```

---

### **Step 4: Start Apache and Nginx Services**
```bash
sudo systemctl start nginx
sudo systemctl enable nginx

sudo systemctl start httpd  # For Apache
sudo systemctl enable httpd
```

Verify services are running:
```bash
systemctl status nginx
systemctl status httpd
```

---

### **Step 5: Verify Firewall Rules**
Check allowed and blocked ports:
```bash
sudo firewall-cmd --list-all --zone=public
```

Now, **Nginx traffic on port 80 is allowed, Apache traffic on port 8080 is blocked**, and `firewalld` is set up permanently in the **public** zone. 🚀 Let me know if you need adjustments!