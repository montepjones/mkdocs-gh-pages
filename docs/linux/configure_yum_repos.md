# configure yum repos
To set up the **local YUM repository** on the **Nautilus Backup Server**, follow these steps:

---

### **Step 1: Create the Repository File**

Create a new YUM repository configuration file:

```bash
sudo nano /etc/yum.repos.d/local_yum.repo
```

Add the following content:

```ini
[local_yum]
name=Local YUM Repository
baseurl=file:///packages/downloaded_rpms/
enabled=1
gpgcheck=0
```

Save and exit.

---

### **Step 2: Clean and Update YUM**

Refresh YUM to recognize the new repository:

```bash
sudo yum clean all
sudo yum makecache
```

---

### **Step 3: Verify Repository**

Check if the new repository is listed:

```bash
yum repolist
```

Ensure `local_yum` appears in the output.

---

### **Step 4: Install `vim-enhanced` from Local Repository**

Run the following command:

```bash
sudo yum install -y vim-enhanced --disablerepo="*" --enablerepo="local_yum"
```

This ensures the package is installed **only from the local repository**.

---

### **Step 5: Verify Installation**

Confirm `vim-enhanced` is installed:

```bash
vim --version
```

Now the **local YUM repository** is successfully configured on the Nautilus Backup Server! 🚀 Let me know if you need adjustments.
