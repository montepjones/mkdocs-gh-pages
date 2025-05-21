# NGINX reverse proxy
step-by-step **setup guide** to deploy the front-end application on a server:

---

### **Step 1: Install Apache and Configure Port 8087**
1. **Install Apache:**
   ```bash
   sudo yum install -y httpd
   ```
2. **Modify Apache's Port Configuration:**  
   Edit the Apache config file:
   ```bash
   sudo nano /etc/httpd/conf/httpd.conf
   ```
   Change the `Listen` directive:
   ```
   Listen 8087
   ```
3. **Restart Apache to Apply Changes:**
   ```bash
   sudo systemctl restart httpd
   ```

---

### **Step 2: Install Nginx and Configure Port 8096**
1. **Install Nginx:**
   ```bash
   sudo yum install -y nginx
   ```
2. **Modify Nginx Configuration:**  
   Edit `/etc/nginx/nginx.conf`:
   ```bash
   sudo nano /etc/nginx/nginx.conf
   ```
   Set Nginx to listen on port **8096**:
   ```
   server {
       listen 8096;
       location / {
           proxy_pass http://127.0.0.1:8087;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
       }
   }
   ```
3. **Restart Nginx to Apply Changes:**
   ```bash
   sudo systemctl restart nginx
   ```

---

### **Step 3: Configure Nginx as Reverse Proxy**
- The **above configuration already sets Nginx** as a reverse proxy by forwarding requests on **8096 → Apache (8087).**  
- Ensure Apache and Nginx are **running correctly** with:
  ```bash
  sudo systemctl status httpd nginx
  ```

---

### **Step 4: Copy Index File to Apache’s Document Root**
1. **Copy the `index.html` file** from Jump Host:
   ```bash
   scp thor@jump-host:/home/thor/index.html /var/www/html/index.html
   ```
2. **Set correct permissions**:
   ```bash
   sudo chmod 644 /var/www/html/index.html
   sudo chown apache:apache /var/www/html/index.html
   ```

---

### **Step 5: Start and Enable Services**
Ensure both servers **start on boot**:
```bash
sudo systemctl enable httpd nginx
sudo systemctl start httpd nginx
```

---

### **Step 6: Test Configuration**
Run:
```bash
curl http://<BackupServerIP>:8096
```
If configured correctly, you should see the **index.html content**.

---

Your Nautilus Backup Server is now set up with **Apache (8087) behind Nginx (8096) acting as a reverse proxy**. 🚀  
Let me know if you need any refinements!
