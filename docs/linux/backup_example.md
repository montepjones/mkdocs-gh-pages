# backup example
Here's how you can create the **news_backup.sh** script to automate website backups:

### **1. Generate the Backup Script**
Create the script in `/scripts/news_backup.sh`:
```bash
#!/bin/bash

# Define variables
BACKUP_DIR="/backup"
SOURCE_DIR="/var/www/html/news"
ARCHIVE_NAME="mycorp_news.zip"
DEST_SERVER="nautilus-backup-server"
DEST_DIR="/backup"

# Create the backup archive
mkdir -p "$BACKUP_DIR"
zip -r "$BACKUP_DIR/$ARCHIVE_NAME" "$SOURCE_DIR"

# Copy the archive to Nautilus Backup Server
scp "$BACKUP_DIR/$ARCHIVE_NAME" username@"$DEST_SERVER":"$DEST_DIR"

echo "Backup completed successfully!"
```

### **2. Ensure Password-less SSH**
To prevent password prompts when copying files:
```bash
ssh-keygen -t rsa -b 4096
ssh-copy-id username@nautilus-backup-server
```
This sets up SSH key-based authentication.

### **3. Make the Script Executable**
```bash
chmod +x /scripts/news_backup.sh
```

### **4. Schedule Automatic Backups**
Add a cron job to run the script daily:
```bash
crontab -e
```
Then add:
```bash
0 2 * * * /scripts/news_backup.sh
```
This runs the backup at **2 AM daily**.

For more details, check out [this guide](https://alvinalexander.com/linux-unix/how-use-scp-without-password-backups-copy/) on automating backups with Bash scripts. Let me know if you need further customization! 🚀