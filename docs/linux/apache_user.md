# To create a custom Apache user tailored for web applications, follow these steps

## 1. **Create a Custom User**

Run the following command to create a new user (replace `<username>` with the desired name):

```sh
sudo useradd -M -s /sbin/nologin <username>
```

- `-M` → Prevents creating a home directory.
- `-s /sbin/nologin` → Restricts login access for security.

### 2. **Set a Password for the User**

If needed, set a password:

```sh
sudo passwd <username>
```

### 3. **Modify Apache to Run Under the Custom User**

Edit the Apache configuration file:

```sh
sudo nano /etc/httpd/conf/httpd.conf  # For CentOS/RHEL
sudo nano /etc/apache2/apache2.conf   # For Ubuntu/Debian
```

Find these lines:

```sh
User apache
Group apache
```

Replace them with:

```sh
User <username>
Group <username>
```

Save and exit.

### 4. **Restart Apache**

Apply the changes:

```sh
sudo systemctl restart httpd  # For CentOS/RHEL
sudo systemctl restart apache2  # For Ubuntu/Debian
```

### 5. **Verify the Changes**

Check if Apache is running under the custom user:

```sh
ps aux | grep apache
```

This setup enhances security by isolating web applications under unique users. Let me know if you need further adjustments! 🚀
