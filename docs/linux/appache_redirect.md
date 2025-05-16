# Apache redirect
To configure **Apache** on **appserver** to listen on **port 8083** and set up the required redirects, follow these steps:

### **1. Change Apache to Listen on Port 8083**
Edit the Apache configuration file:
```bash
sudo nano /etc/httpd/conf/httpd.conf
```
Find the **Listen** directive and update it:
```
Listen 8083
```
Save and exit, then restart Apache:
```bash
sudo systemctl restart httpd
```

### **2. Configure Redirects**
Edit the **VirtualHost** configuration file:
```bash
sudo nano /etc/httpd/conf.d/redirects.conf
```
Add the following rules:

#### **a) Permanent Redirect (301) from Non-WWW to WWW**
```apache
<VirtualHost *:8083>
    ServerName stapp02.company-name.mycorp.com
    Redirect 301 / http://www.stapp02.company-name.mycorp.com:8083/
</VirtualHost>
```

#### **b) Temporary Redirect (302) from `/blog/` to `/news/`**
```apache
<VirtualHost *:8083>
    ServerName www.stapp02.company-name.mycorp.com
    Redirect 302 /blog/ http://www.stapp02.company-name.mycorp.com:8083/news/
</VirtualHost>
```
Save and exit.

### **3. Restart Apache**
```bash
sudo systemctl restart httpd
```

### **4. Verify Redirects**
Test the redirects using:
```bash
curl -I http://stapp02.company-name.mycorp.com:8083/
curl -I http://www.stapp02.company-name.mycorp.com:8083/blog/
```

This ensures that **Apache listens on port 8083** and correctly redirects requests. 🚀 Let me know if you need further customization! You can also check out [this guide](https://httpd.apache.org/docs/2.4/rewrite/remapping.html) for more details.