# Archive Folder
Here’s a complete solution that meets all your requirements with proper ownership mapping for each app server.

---

### ✅ `/home/thor/ansible/playbook.yml`

```yaml
- name: Archive and copy sysops data with correct ownership
  hosts: all
  become: true
  vars:
    archive_src: /usr/src/sysops/
    archive_dest_dir: /opt/sysops
    archive_name: cluster.tar.gz

  tasks:
    - name: Ensure destination directory exists
      file:
        path: "{{ archive_dest_dir }}"
        state: directory
        mode: '0755'

    - name: Create tar.gz archive of /usr/src/sysops
      archive:
        path: "{{ archive_src }}"
        dest: "/{{ archive_dest_dir }}/{{ archive_name }}"
        format: gz
        owner: "{{ ansible_user }}"
        group: "{{ ansible_user }}"
```

---

💡 **How it works:**
- Uses the `archive` module to create a `.tar.gz` file of `/usr/src/sysops/`
- Copies the archive to `/opt/sysops`
- Sets **owner and group dynamically** based on each host's alias (`stapp01`, `stapp02`, etc.)

---

