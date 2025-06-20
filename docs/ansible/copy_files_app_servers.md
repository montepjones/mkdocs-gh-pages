# Copy file to muliple servers

## Create a inventory file 
Here is an example inventory file. See below for a explantion
```ini
[app_servers] 
stapp01 ansible_host=172.16.238.10 ansible_user=tony ansible_password=Ir0nM@n 
stapp02 ansible_host=172.16.238.11 ansible_user=steve ansible_password=Am3ric@ 
stapp03 ansible_host=172.16.238.12 ansible_user=banner ansible_password=BigGr33n
```


---

### 📦 `[app_servers]`
This defines a **group** called `app_servers`. You can target this group in your playbooks with:

```yaml
hosts: app_servers
```

---

### 🖥️ Host Entries
Each of the following lines defines a **host** with connection variables:

```ini
stapp01 ansible_host=172.16.238.10 ansible_user=tony ansible_password=Ir0nM@n
```

- `stapp01` – This is the alias you're giving the host; you can refer to it this way in Ansible tasks or plays.
- `ansible_host` – The actual IP address or hostname to connect to.
- `ansible_user` – The SSH user Ansible will use to connect.
- `ansible_password` – The password for that user (used instead of SSH keys in this setup).

---

### 🔐 Quick Note on Security
Using `ansible_password` directly in your inventory file is totally valid for testing or simple environments — but **not ideal for production**. For better security, consider using **Ansible Vault** to encrypt the file or move credentials to a protected `group_vars` file.

## Ansible playbook
Here’s a complete Ansible playbook to perform that file copy operation across all application servers:

```yaml
---
- name: Copy index.html to all application servers
  hosts: app_servers
  become: true
  tasks:
    - name: Ensure destination directory exists
      file:
        path: /opt/security
        state: directory
        mode: '0755'

    - name: Copy index.html to /opt/security
      copy:
        src: /usr/src/security/index.html
        dest: /opt/security/index.html
        owner: "{{ ansible_host }}"
        group: "{{ ansible_host }}"
        mode: '0644'
```

📌 Save this as `~/ansible/playbook.yml`.

> Make sure your inventory file `~/ansible/inventory` has the `[app_servers]` group defined with your application hosts.

Once done, run the playbook like this (as validation will expect):

```bash
cd ~/ansible
ansible-playbook -i inventory playbook.yml
```

Let me know if the file contents need to be templated or validated on the remote end — we can make it smarter if needed. 🔧📄
