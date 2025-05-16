To set up the required containerized stack using **Docker Compose**, you need to create the specified `docker-compose.yml` file at `/opt/dba/docker-compose.yml`. Below is how you can structure it:

```yaml
services:
  web:
    image: php:apache
    container_name: php_web
    ports:
      - "8089:80"
    volumes:
      - "/var/www/html:/var/www/html"

  db:
    image: mariadb:latest
    container_name: mysql_web
    ports:
      - "3306:3306"
    volumes:
      - "/var/lib/mysql:/var/lib/mysql"
    environment:
      MYSQL_DATABASE: database_web
      MYSQL_USER: php_web_user
      MYSQL_PASSWORD: C0mplexP@ssw0rd!
      MYSQL_ROOT_PASSWORD: R00tP@ssword456 
```

### **Steps to Deploy:**
1. **Navigate to the directory:**
   ```bash
   cd /opt/dba/
   ```

2. **Create the `docker-compose.yml` file:**
   ```bash
   nano docker-compose.yml
   ```
   - Paste the YAML configuration above and save it.

3. **Run Docker Compose:**
   ```bash
   docker-compose up -d
   ```

4. **Verify the Containers:**
   ```bash
   docker ps
   ```

5. **Test the Deployment:**
   ```bash
   curl <server-ip or hostname>:8089/
   ```

Once deployed, the app should be accessible via port `8089`. Let me know if you need any tweaks! 🚀

