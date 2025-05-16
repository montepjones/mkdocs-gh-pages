# create cron job

To set up a test cron job, follow these steps:

### **Step 1: Install `cronie` Package**
On each **Nautilus app server**, run:
```bash
sudo yum install -y cronie  # For RHEL/CentOS
```
OR
```bash
sudo apt update && sudo apt install -y cron  # For Ubuntu/Debian
```

### **Step 2: Start and Enable the `crond` Service**
Once installed, start the cron daemon:
```bash
sudo systemctl start crond
sudo systemctl enable crond
```
Verify it’s running:
```bash
systemctl status crond
```

### **Step 3: Add the Cron Job for Root**
Edit the root user's crontab:
```bash
sudo crontab -e
```
Add the following line:
```
*/5 * * * * echo hello > /tmp/cron_text
```
- This ensures the job runs **every 5 minutes** and writes `"hello"` to `/tmp/cron_text`.

### **Step 4: Verify the Cron Job**
To check if the cron job was added, run:
```bash
sudo crontab -l
```
Wait 5 minutes, then confirm execution:
```bash
cat /tmp/cron_text
```
If `"hello"` appears, your setup is working!

Let me know if you need adjustments. 🚀
```bash
SERVERS="server1 server2 server3"
for SERVER in $SERVERS; do
  ssh $SERVER "sudo yum install -y cronie && sudo systemctl start crond && sudo systemctl enable crond && echo '*/5 * * * * echo hello > /tmp/cron_text' | sudo crontab -"
done
```
