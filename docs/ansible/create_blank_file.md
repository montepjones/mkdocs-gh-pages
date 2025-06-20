# Create Blank File
---

### ✅ Step 1: Update the Inventory File  
Edit the inventory file at `~/ansible/inventory` and add a group or direct entry for App Server 2. Assuming the hostname is `stapp02`, your inventory should look like:

```ini
[app_servers]
stapp02 ansible_host=<IP_ADDRESS> ansible_user=YourUser ansible_password=YourPasswordHere
```

> Replace `<IP_ADDRESS>` with the actual IP or ensure `stapp02` is resolvable (e.g., in `/etc/hosts`). If SSH uses a key or specific port, you may need to add `ansible_ssh_private_key_file` or `ansible_port`.

---

### ✅ Step 2: Create the Ansible Playbook  
Save the following content as `/home/thor/ansible/playbook.yml`:

```yaml
---
- name: Create file on App Server 2
  hosts: app_servers
  become: true
  tasks:
    - name: Create empty file /tmp/file.txt
      file:
        path: /tmp/file.txt
        state: touch
```

---

Once done, test with:
```bash
cd ~/ansible
ansible-playbook -i inventory playbook.yml
```

That should create `/tmp/file.txt` on App Server 2. Let me know if you’d like to add logging or verify file creation in the play itself — I’d be glad to add polish. 🛠️📋  
Want this playbook templatized for reuse across servers? Let's modularize it!

To include a password in your Ansible inventory file (for SSH or remote access), you can define it using the `ansible_password` variable. Here's a basic example:

```ini
[app_servers]
stapp02 ansible_user=thor ansible_password=YourPasswordHere
```

This tells Ansible to connect to `stapp02` using the `thor` user and the specified password.

---

### 🔐 But wait — storing passwords in plain text is risky.

A better approach is to use **Ansible Vault** to encrypt sensitive data:

1. Create a secure variable file:
   ```bash
   ansible-vault create group_vars/app_servers.yml
   ```

2. Inside that file, add:
   ```yaml
   ansible_user: thor
   ansible_password: YourPasswordHere
   ```

3. Then run your playbook with:
   ```bash
   ansible-playbook -i inventory playbook.yml --ask-vault-pass
   ```

This keeps your credentials safe and your conscience clear. Want help vaulting your whole inventory or automating secure access? I’ve got your back. 🛡️🔧  
Let me know how secure you want to go. We can even integrate with SSH keys or secret managers.
