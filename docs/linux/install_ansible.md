To install **Ansible version 4.10.0** on the **Jump Host** using `pip3` and make it available globally, follow these steps:

### **Step 1: Install `pip3` (if not installed)**
Check if `pip3` is installed:
```bash
pip3 --version
```
If it's missing, install it:

For **RHEL/CentOS**:
```bash
sudo yum install -y python3-pip
```
For **Debian/Ubuntu**:
```bash
sudo apt update && sudo apt install -y python3-pip
```

---

### **Step 2: Install Ansible Version 4.10.0**
Run the following command to install **Ansible 4.10.0**:
```bash
sudo pip3 install ansible==4.10.0
```
- `sudo` ensures the package is installed globally, making Ansible accessible to all users.

---

### **Step 3: Verify Installation**
Check if Ansible is installed:
```bash
ansible --version
```
Expected output should show **version 4.10.0**.

---

### **Step 4: Ensure Ansible is Accessible Globally**
To confirm all users can run Ansible, check where it's installed:
```bash
which ansible
```
It should be in `/usr/local/bin/ansible`. If it's not globally accessible, you may need to add it to the system-wide **PATH**.

---

### **Step 5: Test Ansible Functionality**
Verify by running:
```bash
ansible --help
```
This ensures all users can execute Ansible commands correctly.

Now your **Jump Host** is set up as an Ansible controller! 🚀 Let me know if you need any adjustments.
