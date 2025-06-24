Monte, here’s a **step-by-step guide** to set up **basic authentication** for the confidential directory on **Nautilus App Server 3**:

---

### **1️⃣ Create the Directory**
Check if the directory exists, and create it if necessary:
```bash
sudo mkdir -p /var/www/html/dba
```
Set appropriate permissions:
```bash
sudo chown -R apache:apache /var/www/html/dba
sudo chmod 755 /var/www/html/dba
```

---

### **2️⃣ Set Up `.htaccess` and Password Authentication**
✔️ Install the `httpd-tools` package for managing `.htpasswd`:
```bash
sudo yum install -y httpd-tools
```
✔️ Create the `.htpasswd` file and add user **kirsty** with the password `B4zNgHA7Ya`:
```bash
sudo htpasswd -c /etc/httpd/.htpasswd kirsty
```
✔️ Enter the password when prompted.

✔️ Configure `.htaccess` in the `/var/www/html/dba/` directory:
```bash
sudo nano /var/www/html/dba/.htaccess
```
Add the following lines:
```
AuthType Basic
AuthName "Restricted Access"
AuthUserFile /etc/httpd/.htpasswd
Require valid-user
```
✔️ Update the Apache configuration to allow `.htaccess` files:
```bash
sudo nano /etc/httpd/conf/httpd.conf
```
Find the **`<Directory "/var/www/html">`** section and modify:
```
AllowOverride AuthConfig
```

✔️ Restart Apache:
```bash
sudo systemctl restart httpd
```

---

### **3️⃣ Copy `index.html` from Jump Server**
✔️ Use **SCP** to transfer the file:
```bash
scp thor@jump-host:/tmp/index.html /var/www/html/dba/index.html
```
✔️ Set correct permissions:
```bash
sudo chmod 644 /var/www/html/dba/index.html
sudo chown apache:apache /var/www/html/dba/index.html
```

---

### **4️⃣ Ensure Apache Listens on Port 8080**
✔️ Modify the **Apache configuration**:
```bash
sudo nano /etc/httpd/conf/httpd.conf
```
Add:
```
Listen 8080
```
✔️ Restart Apache:
```bash
sudo systemctl restart httpd
```

---

### **5️⃣ Test the Authentication**
Run:
```bash
curl -u kirsty:B4zNgHA7Ya http://<app-server-hostname>:8080/dba/
```
You should be prompted for credentials, and once authenticated, see the **index.html** content.

Your website is now **password-protected**, running on **8080**, and accessible via **basic authentication**. 🚀  
Let me know if you need refinements!