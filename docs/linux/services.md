To install and configure **Postfix** on all application servers in company-name Datacenter, follow these steps:

---

### **Step 1: Install Postfix**
Run the appropriate installation command based on the server's OS:

#### **For RHEL/CentOS-based systems:**
```bash
sudo yum install -y postfix
```

#### **For Ubuntu/Debian-based systems:**
```bash
sudo apt update && sudo apt install -y postfix
```

---

### **Step 2: Enable Postfix to Start on Boot**
```bash
sudo systemctl enable postfix
sudo systemctl start postfix
```

Verify the service status:
```bash
systemctl status postfix
```
It should display **active (running)**.

---

### **Step 3: Automate Across Multiple Servers**
If setting this up on multiple servers, use **Ansible** or an SSH loop:

#### **Using Ansible**
Create a playbook `install_postfix.yml`:
```yaml
- name: Install and Configure Postfix
  hosts: all
  become: yes
  tasks:
    - name: Install Postfix (RHEL-based)
      yum:
        name: postfix
        state: present
      when: ansible_os_family == "RedHat"

    - name: Install Postfix (Debian-based)
      apt:
        name: postfix
        state: present
      when: ansible_os_family == "Debian"

    - name: Enable and Start Postfix
      service:
        name: postfix
        state: started
        enabled: yes
```

Run it:
```bash
ansible-playbook -i inventory install_postfix.yml
```

#### **Using SSH Loop**
```bash
SERVERS=("app-server1" "app-server2" "app-server3")
for SERVER in "${SERVERS[@]}"; do
  ssh $SERVER "sudo yum install -y postfix && sudo systemctl enable postfix && sudo systemctl start postfix"
done
```

Now, **Postfix is installed and enabled** across all application servers! 🚀 Let me know if you need further refinements.
