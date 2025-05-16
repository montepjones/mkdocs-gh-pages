# config sudo access
To grant **sudo access** to user `ammar` on all application servers and configure **password-less sudo**, follow these steps:

---

### **Step 1: Grant Sudo Access**

Run the following command on each app server:

```bash
sudo usermod -aG wheel ammar  # For RHEL/CentOS-based systems
sudo usermod -aG sudo ammar  # For Debian/Ubuntu-based systems
```

This adds `ammar` to the appropriate **sudo group**, allowing administrative access.

---

### **Step 2: Set Up Password-less Sudo**

Modify the sudoers file to allow `ammar` to run commands **without requiring a password**:

Run:

```bash
sudo visudo
```

Add the following line at the bottom:

```bash
ammar ALL=(ALL) NOPASSWD: ALL
```

Save and exit.

---

### **Step 3: Verify the Configuration**

Log in as `ammar` and try running a privileged command:

```bash
sudo ls /root
```

If no password is prompted, the setup is correct.

---

### **Step 4: Automate Across Multiple Servers**

To apply these changes across multiple servers, use **Ansible** or an **SSH loop**.

#### **Using Ansible**

Create a playbook `grant_sudo.yml`:

```yaml
- name: Grant sudo access to user ammar
  hosts: all
  become: yes
  tasks:
    - name: Add ammar to sudo group (Debian-based)
      user:
        name: ammar
        groups: sudo
        append: yes
      when: ansible_os_family == "Debian"

    - name: Add ammar to wheel group (RHEL-based)
      user:
        name: ammar
        groups: wheel
        append: yes
      when: ansible_os_family == "RedHat"

    - name: Configure password-less sudo
      lineinfile:
        path: /etc/sudoers
        line: "ammar ALL=(ALL) NOPASSWD: ALL"
        validate: "visudo -cf %s"
```

Run the playbook:

```bash
ansible-playbook -i inventory grant_sudo.yml
```

#### **Using SSH Loop**

```bash
SERVERS=("app-server1" "app-server2" "app-server3")
for SERVER in "${SERVERS[@]}"; do
  ssh $SERVER "sudo usermod -aG wheel ammar && echo 'ammar ALL=(ALL) NOPASSWD: ALL' | sudo tee -a /etc/sudoers"
done
```

Now, `ammar` has **password-less sudo access** across all application servers! 🚀 Let me know if you need further refinements.
