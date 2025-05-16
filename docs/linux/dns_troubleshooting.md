It looks like your message got cut off. If you're looking to add additional **DNS nameservers** to **App Server 3**, here’s how you can do it:

### **Step 1: Edit the DNS Configuration File**
Modify the `/etc/resolv.conf` file:
```bash
sudo nano /etc/resolv.conf
```
Add the **new nameservers** at the top:
```
nameserver 8.8.8.8
nameserver 1.1.1.1
```
Save and exit.

---

### **Step 2: Make DNS Changes Persistent**
Since `/etc/resolv.conf` might get **overwritten** by system processes, make it persistent by editing:
```bash
sudo nano /etc/systemd/resolved.conf
```
Locate and modify the following line:
```
DNS=8.8.8.8 1.1.1.1
```
Then restart the service:
```bash
sudo systemctl restart systemd-resolved
```

---

### **Step 3: Verify DNS Resolution**
Check if the new nameservers are resolving correctly:
```bash
nslookup google.com
```
OR
```bash
dig google.com
```

If this is a **temporary fix**, consider monitoring DNS stability before making permanent changes. Let me know if you need further refinements! 🚀
