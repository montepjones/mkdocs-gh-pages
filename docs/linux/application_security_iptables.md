# configure iptables
To configure **iptables** on the Nautilus backup server to allow incoming connections to **Nginx (port 8094)** and block incoming connections to **Apache (port 5000)**, follow these steps:

### **1. Allow Incoming Connections to Nginx (Port 8094)**
Run:
```bash
# put at the end
sudo iptables -A INPUT -p tcp --dport 8094 -j ACCEPT
# put at the top
sudo iptables -I INPUT -p tcp --dport 8080 -j ACCEPT
```

### **2. Block Incoming Connections to Apache (Port 5000)**
Run:
```bash
sudo iptables -A INPUT -p tcp --dport 5000 -j DROP
```

### **3. Save the Rules to Make Them Permanent**
On **CentOS/RHEL**, save the rules:
```bash
# this gave an error sudo iptables-save > /etc/sysconfig/iptables
sudo /usr/libexec/iptables/iptables.init save
```
On **Ubuntu/Debian**, use:
```bash
sudo netfilter-persistent save
```

### **4. Verify Rules**
Check the active rules:
```bash
sudo iptables -L -v -n
```

This ensures that **Nginx is accessible** while **Apache remains blocked**. You can find more details in [this guide](https://www.digitalocean.com/community/tutorials/iptables-essentials-common-firewall-rules-and-commands) or [this tutorial](https://serverfault.com/questions/414407/allow-accessing-to-the-port-8080-in-iptable). Let me know if you need further customization! 🚀
