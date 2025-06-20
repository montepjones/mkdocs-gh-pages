# Line In File example.
---

### ✅ **File:** `/home/thor/ansible/playbook.yml`

```yaml
---
- name: Set up httpd and deploy index.html with proper content and ownership
  hosts: all
  become: true
  tasks:
    - name: Install httpd web server
      yum:
        name: httpd
        state: present

    - name: Ensure httpd is started and enabled
      service:
        name: httpd
        state: started
        enabled: true

    - name: Create index.html with initial content
      copy:
        dest: /var/www/html/index.html
        content: "This is a Nautilus sample file, created using Ansible!\n"
        owner: apache
        group: apache
        mode: '0744'

    - name: Prepend welcome line to index.html
      lineinfile:
        path: /var/www/html/index.html
        line: "Welcome to xFusionCorp Industries!"
        insertafter: BOF
        owner: apache
        group: apache
        mode: '0744'
```

---

This playbook:
- Installs and enables the `httpd` service
- Uses the `copy` module to ensure the initial file content
- Prepends the welcome line using `lineinfile` and keeps ownership/permissions consistent

Once the inventory is in place, you're good to launch this with:

```bash
ansible-playbook -i inventory playbook.yml
```

