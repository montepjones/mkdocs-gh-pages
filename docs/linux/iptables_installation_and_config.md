# Secure apache port. 

How to  **secure Apache’s port (8085) using `iptables`** on the **app hosts** while allowing access only from a single server.

---

### **Step 1: Install `iptables` and Dependencies**
1. **Update the system**:
   ```bash
   sudo yum update -y
   ```
2. **Install `iptables`**:
   ```bash
   sudo yum install -y iptables-services
   ```

---

### **Step 2: Configure Firewall Rules**
1. **Check the LBR host’s IP** (Replace `LBR_IP` with actual IP):
   ```bash
   sudo iptables -A INPUT -p tcp --dport 8085 -s LBR_IP -j ACCEPT
   ```
2. **Block Everyone Else**:
   ```bash
   sudo iptables -A INPUT -p tcp --dport 8085 -j DROP
   ```

---

### **Step 3: Save and Persist Rules**
1. **Save the rules**:
   ```bash
   sudo service iptables save
   ```
2. **Enable and Start `iptables` to persist across reboots**:
   ```bash
   sudo systemctl enable iptables
   sudo systemctl start iptables
   ```

---

### **Step 4: Verify Firewall Rules**
1. **List active rules**:
   ```bash
   sudo iptables -L -n
   ```
2. **Test the firewall by accessing port 8085**.

Now, **port 8085 is secured**, allowing **only the LBR host**, and rules persist across reboots! 🚀 Let me know if you need any refinements.