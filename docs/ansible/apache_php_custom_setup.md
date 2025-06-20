# Apache and PHP custom setup
---

### ✅ **File:** `~/playbooks/httpd.yml`

```yaml
---
- name: Configure Apache + PHP on App Server 2
  hosts: stapp02
  become: true
  tasks:

    - name: Install httpd and php
      yum:
        name:
          - httpd
          - php
        state: present

    - name: Ensure custom document root directory exists
      file:
        path: /var/www/html/myroot
        state: directory
        owner: apache
        group: apache
        mode: '0755'

    - name: Update DocumentRoot in Apache configuration
      replace:
        path: /etc/httpd/conf/httpd.conf
        regexp: '^DocumentRoot\s+".+"'
        replace: 'DocumentRoot "/var/www/html/myroot"'

    - name: Update <Directory> block to match new document root
      replace:
        path: /etc/httpd/conf/httpd.conf
        regexp: '^<Directory\s+".+">'
        replace: '<Directory "/var/www/html/myroot">'

    - name: Copy phpinfo template to custom doc root
      template:
        src: templates/phpinfo.php.j2
        dest: /var/www/html/myroot/phpinfo.php
        owner: apache
        group: apache
        mode: '0644'

    - name: Ensure httpd is started and enabled
      service:
        name: httpd
        state: started
        enabled: yes
```

---

🔥 This playbook ensures:
- `httpd` and `php` are installed from default YUM repos
- The new document root is created and configured properly in `httpd.conf`
- Your `phpinfo.php.j2` template is deployed with correct permissions
- Apache service is started and enabled to persist across reboots

Run it from the `~/playbooks` directory:

```bash
ansible-playbook -i inventory httpd.yml
```

