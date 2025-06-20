Troubleshooting a **LEMP stack** (Linux, NGINX, MySQL/MariaDB, PHP) means checking each layer methodically. Here's a practical guide to help you isolate and resolve issues:

---

### 🔍 1. **Check NGINX (Web Server)**
- **Is it running?**
  ```bash
  sudo systemctl status nginx
  ```
- **Test config syntax:**
  ```bash
  sudo nginx -t
  ```
- **Check logs:**
  ```bash
  sudo tail -f /var/log/nginx/error.log
  ```
- ** Check port**
```bash
ss 
```
Common issues:
- “Welcome to NGINX” page → default config still active.
- 404 errors → wrong `root` path or missing files.
- 502 Bad Gateway → PHP-FPM not responding.

---



Here’s how to fix it:

---

### ✅  Check if PHP-FPM is Running
```bash
sudo systemctl status php74-php-fpm
```
If it’s not running, start it:
```bash
sudo systemctl start php74-php-fpm
```

---

### 🔍 Confirm the Actual Socket Path
Check the `listen` directive in the PHP-FPM pool config:
```bash
grep ^listen /etc/opt/remi/php74/php-fpm.d/www.conf
```
You might see something like:
```ini
listen = /var/opt/remi/php74/run/php-fpm/www.sock
```
Make sure this matches what NGINX is using.

---

### 🛠️  Update NGINX Config (if needed)
In your NGINX config, ensure the `fastcgi_pass` line matches the actual socket:
```nginx
fastcgi_pass unix:/var/opt/remi/php74/run/php-fpm/www.sock;
```

---

### 🔄  Restart Services
After syncing the paths:
```bash
sudo systemctl restart php74-php-fpm
sudo systemctl reload nginx
```



Common issues:
- Blank pages → PHP errors or misconfigured `fastcgi_pass`.
- 502 errors → PHP-FPM socket mismatch or service down.

---

### 🗄️ 3. **Check MySQL/MariaDB (Database)**
- **Is it running?**
  ```bash
  sudo systemctl status mysqld
  ```
- **Can you connect?**
  ```bash
  mysql -u root -p
  ```

Common issues:
- “Connection refused” → service down or firewall blocking.
- “Access denied” → wrong credentials or host permissions.

---

### 🧰 4. **Use `journalctl` for Unified Logs**
This is a powerful way to view logs across services:
```bash
sudo journalctl -u nginx -u php-fpm -u mysqld --since today
```
It helps correlate issues across the stack in one view.

---

### 🧪 5. **Test the Stack**
- Create a `test.php` file in your web root:
  ```php
  <?php phpinfo(); ?>
  ```
- Access it via browser or curl:
  ```bash
  curl http://localhost/test.php
  ```

If it doesn’t render, PHP isn’t being processed correctly.

---

Want to automate these checks or build a health dashboard? I can help you script it out or integrate with monitoring tools like Prometheus or Netdata. Just say the word. 🚦📊
