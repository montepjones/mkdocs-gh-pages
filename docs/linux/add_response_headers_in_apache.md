# add response headers
To harden the **Apache web server** on **appserver**, follow these steps:

### **1. Install Apache (`httpd`) and Configure Port 6400**
```bash
sudo yum install httpd -y
sudo sed -i 's/^Listen 80/Listen 6400/' /etc/httpd/conf/httpd.conf
sudo systemctl start httpd
sudo systemctl enable httpd
```
This installs Apache, updates the configuration to listen on **port 6400**, and ensures the service starts on boot.

### **2. Create `index.html`**
```bash
echo "Welcome to the mycorp Industries!" | sudo tee /var/www/html/index.html
```
This creates the required **index.html** file.

### **3. Enable Security Headers**
Edit the Apache configuration file:
```bash
sudo nano /etc/httpd/conf/httpd.conf
```
Add the following lines inside the `<VirtualHost>` block or globally:
```apache
Header set X-XSS-Protection "1; mode=block"
Header always set X-Frame-Options "SAMEORIGIN"
Header set X-Content-Type-Options "nosniff"
```
Save and exit.

### **4. Restart Apache**
```bash
sudo systemctl restart httpd
```

### **5. Test with `curl`**
Run:
```bash
curl -I http://localhost:6400
```
You should see the headers in the response.

For more details, check out [this guide](https://computingforgeeks.com/configure-http-security-headers-in-nginx-apache/) or [this tutorial](https://webdock.io/en/docs/how-guides/security-guides/how-to-configure-security-headers-in-nginx-and-apache). Let me know if you need further customization! 🚀