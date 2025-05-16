To meet the security requirements for SELinux on **App Server**, follow these steps:

### **Step 1: Install Required SELinux Packages**
If SELinux is not installed, install it using:

```sh
sudo yum install -y selinux-policy selinux-policy-targeted
```
_For RHEL/CentOS systems._

Or for Debian/Ubuntu-based systems:

```sh
sudo apt install -y selinux-utils policycoreutils selinux-policy-default
```

### **Step 2: Permanently Disable SELinux**
Modify the SELinux configuration file to disable SELinux:

```sh
sudo sed -i 's/^SELINUX=.*/SELINUX=disabled/' /etc/selinux/config
```

Alternatively, manually edit the file:

```sh
sudo nano /etc/selinux/config
```

Change the line:

```sh
SELINUX=enforcing
```

To:

```sh
SELINUX=disabled
```

Save and exit.

### **Step 3: Confirm the Change Without Considering Current Status**
Since no immediate reboot is required, verify that SELinux is set to be disabled after the next reboot:

```sh
grep SELINUX= /etc/selinux/config
```

The output should show:

```sh
SELINUX=disabled
```

Once the maintenance reboot occurs, SELinux will remain disabled as per the configuration.

Let me know if you need any refinements! 🚀
