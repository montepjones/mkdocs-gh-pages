Here’s the Ansible playbook that checks all the boxes, including service setup, content deployment, permissions, and ownership:

---

### ✅ **File:** `/home/thor/ansible/playbook.yml`

```yaml
---
- name: Setup httpd web server and deploy sample page
  hosts: all
  become: true
  tasks:

    - name: Install httpd package
      yum:
        name: httpd
        state: present

    - name: Ensure httpd service is running and enabled
      service:
        name: httpd
        state: started
        enabled: yes


    - name: Add content to index.html using blockinfile
      blockinfile:
        path: /var/www/html/index.html
        create: yes
        owner: apache
        group: apache
        mode: '0644'
        block: |
          Welcome to XfusionCorp!

          This is  Nautilus sample file, created using Ansible!

          Please do not modify this file manually!
```

---

This playbook will:
- Install and start `httpd`
- Add the specified block of text to `/var/www/html/index.html`
- Enforce the correct ownership and permission settings

