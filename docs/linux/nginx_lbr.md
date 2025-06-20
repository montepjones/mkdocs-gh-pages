Here's how you can configure the LBR (load balancer) server with **NGINX as a reverse proxy** using HTTP load balancing to your app servers, while preserving the existing Apache configurations on those backend nodes:

---

### **Step 1: Install NGINX on the LBR Server**
```bash
sudo yum install nginx -y        # For RHEL/CentOS
# Or for Debian/Ubuntu:
sudo apt install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx
```

---

### **Step 2: Configure Load Balancing in NGINX**
Let’s assume your app servers are running Apache on port `8080`, and their IPs are `192.168.1.10`, `192.168.1.11`, and `192.168.1.12`. Replace them with actual IPs or hostnames.

Edit the NGINX configuration:
```bash
sudo vi /etc/nginx/nginx.conf
```

Add the following config:
```nginx
upstream app_cluster {
    server 192.168.1.10:8080;
    server 192.168.1.11:8080;
    server 192.168.1.12:8080;
}

server {
    listen 80;
    server_name staticapp.nautilus.com;  # Or use "_"

    location / {
        proxy_pass http://app_cluster;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

---

### **Step 3: Test Apache on App Servers**
Make sure Apache is listening on the intended port and is running:
```bash
systemctl status httpd    # Or apache2
netstat -tulnp | grep 8080
```


---

### **Step 4: Restart NGINX**
```bash
sudo nginx -t && sudo systemctl reload nginx
```

---

### **Step 5: Verify the Setup**
You can now test the load balancer using:
```bash
curl http://<lbr-ip>/
```

---

If you'd like to add SSL/TLS or configure sticky sessions or health checks, I can help with that next. You're almost at the finish line of your high availability deployment! 🚀
