To install the **Samba** package on all app servers in **company-name Datacenter**, follow these steps:

### **Step 1: Install Samba on Each App Server**

Run the following command, depending on the operating system:

#### **For RHEL/CentOS-based systems:**

```bash
sudo yum install -y samba
```

#### **For Ubuntu/Debian-based systems:**

```bash
sudo apt update && sudo apt install -y samba
```

---

### **Step 2: Start and Enable Samba Service**

After installation, start and enable the **Samba** service:

```bash
sudo systemctl start smb
sudo systemctl enable smb
```

Check the status:

```bash
systemctl status smb
```

---

### **Step 3: Verify Installation**

Confirm that Samba is installed:

```bash
smbd --version
```

---

### **Step 4: Automating Installation on Multiple Servers**

If installing across multiple servers, use **Ansible** or an **SSH loop**.

#### **Using Ansible**

Create a playbook `install_samba.yml`:

```yaml
- name: Install Samba on Multiple Servers
  hosts: all
  become: yes
  tasks:
    - name: Install Samba (RHEL-based)
      yum:
        name: samba
        state: present
      when: ansible_os_family == "RedHat"

    - name: Install Samba (Debian-based)
      apt:
        name: samba
        state: present
      when: ansible_os_family == "Debian"

    - name: Start and Enable Samba Service
      service:
        name: smb
        state: started
        enabled: yes
```

Run it:

```bash
ansible-playbook -i inventory install_samba.yml
```

#### **Using SSH Loop**

```bash
SERVERS=("app-server1" "app-server2" "app-server3")
for SERVER in "${SERVERS[@]}"; do
  ssh $SERVER "sudo yum install -y samba && sudo systemctl start smb && sudo systemctl enable smb"
done
```

Once installed, Samba should be ready for use across **all servers**! 🚀 Let me know if you need modifications.
