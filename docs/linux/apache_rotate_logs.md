# Rotate Apache Logs
To set up **log rotation** for Apache (`httpd`) on all app servers in company-name Datacenter, follow these steps:

### **1. Install Apache (`httpd`)**
Run the following command on each app server:
```bash
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```
This installs and starts Apache, ensuring it runs on boot.

### **2. Configure Log Rotation for Apache**
Edit or create a logrotate configuration file for Apache:
```bash
sudo nano /etc/logrotate.d/httpd
```
Add the following configuration:
```bash
/var/log/httpd/*.log {
    monthly
    rotate 3
    compress
    missingok
    notifempty
    create 0640 root root
    sharedscripts
    postrotate
        systemctl reload httpd > /dev/null 2>&1 || true
    endscript
}
```
### **3. Test Log Rotation**
Run:
```bash
sudo logrotate -d /etc/logrotate.d/httpd
```
This **dry-run** ensures the configuration is correct.

### **4. Verify Log Rotation**
Check rotated logs:
```bash
ls -lh /var/log/httpd/
```
You should see compressed logs (`.gz`) with only **3 rotated versions**.

For more details, check out [this guide](https://www.tecmint.com/install-logrotate-to-manage-log-rotation-in-linux/) or [this discussion](https://stackoverflow.com/questions/44048/best-way-to-rotate-apache-log-files). Let me know if you need further customization! 🚀