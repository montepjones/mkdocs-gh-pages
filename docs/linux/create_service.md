# create a service

To create the **mercury.service** systemd unit file, follow these steps:

### **1. Create the Unit File**
Run:
```bash
sudo nano /etc/systemd/system/mercury.service
```
Add the following configuration:
```ini
[Unit]
Description=Project Mercury Web Application
After=network.target

[Service]
User=mercury
WorkingDirectory=/opt/caleston-code/mercuryProject/
ExecStart=/usr/bin/python3 manage.py runserver 0.0.0.0:8000
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
Save and exit.

### **2. Reload Systemd**
```bash
sudo systemctl daemon-reload
```

### **3. Enable and Start the Service**
```bash
sudo systemctl enable mercury.service
sudo systemctl start mercury.service
```

### **4. Verify the Service**
Check the status:
```bash
sudo systemctl status mercury.service
```

This ensures the **mercury.service** is running and will restart on failure. 🚀 Let me know if you need further customization! You can also check out [this guide](https://linuxhandbook.com/create-systemd-services/) for more details.