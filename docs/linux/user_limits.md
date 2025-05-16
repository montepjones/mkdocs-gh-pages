To enforce process limitations for the `nfsuser` user, you need to configure the limits in the `/etc/security/limits.conf` file. Follow these steps:

### **Step 1: Edit the Limits Configuration File**

Open the file using a text editor:

```sh
sudo nano /etc/security/limits.conf
```

### **Step 2: Add Limits for `nfsuser`**

Append the following lines at the end of the file:

```sh
nfsuser soft nproc 1026
nfsuser hard nproc 2026
```

### **Step 3: Save and Exit**

Press `CTRL + X`, then `Y`, and hit `ENTER` to save the changes.

### **Step 4: Apply the Changes**

Ensure the PAM module is enforcing these limits:

```sh
sudo nano /etc/pam.d/common-session
```

Confirm or add this line:

```sh
session required pam_limits.so
```

Save and exit.

### **Step 5: Verify the Configuration**

To check the current limits for `nfsuser`, run:

```sh
ulimit -u -S
ulimit -u -H
```

You may also switch to the `nfsuser` account and test:

```sh
su - nfsuser
ulimit -u
```

This should reflect the soft and hard process limits.

Let me know if you need further refinements! 🚀
