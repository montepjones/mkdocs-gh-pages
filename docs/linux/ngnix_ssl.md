# Install nginx and configure ssl
---

### **1. Install and Configure Nginx**
```bash
sudo yum install nginx -y            # RHEL/CentOS
sudo systemctl enable nginx
sudo systemctl start nginx
```

---

### **2. Deploy Self-Signed SSL Certificate**
Move the cert and key to `/etc/ssl/certs/` and `/etc/ssl/private/` (or similar depending on your distro):
```bash
sudo mkdir -p /etc/ssl/private
sudo mv /tmp/nautilus.crt /etc/ssl/certs/
sudo mv /tmp/nautilus.key /etc/ssl/private/
sudo chmod 600 /etc/ssl/private/nautilus.key
```

Now configure Nginx to use SSL. Edit the default server block (usually in `/etc/nginx/nginx.conf` or `/etc/nginx/conf.d/default.conf`):

```nginx
server {
    listen 443 ssl;
    server_name localhost;

    ssl_certificate /etc/ssl/certs/nautilus.crt;
    ssl_certificate_key /etc/ssl/private/nautilus.key;

    root /usr/share/nginx/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

Don’t forget to also stop the default HTTP listener on port 80 if you don’t need it.

---

### **3. Create the `index.html`**
```bash
echo "Welcome!" | sudo tee /usr/share/nginx/html/index.html
```

---

### **4. Restart Nginx**
```bash
sudo systemctl restart nginx
```

---

### **5. Test from Jump Host**
From the jump host, test the HTTPS endpoint:
```bash
curl -Ik https://<app-server-ip>/
```

If successful, you should see a `200 OK` in the HTTP response headers along with the SSL handshake.

---

Let me know if you'd like to redirect HTTP to HTTPS or harden the SSL setup—I’ve got tips for that too. 🚀
