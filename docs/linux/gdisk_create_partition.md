You can create a **GPT partition** called `vdb1` of size **500MB** on `/dev/vdb` using `gdisk` by following these steps:

### **1. Start `gdisk` on `/dev/vdb`**
```bash
sudo gdisk /dev/vdb
```

### **2. Create a New Partition**
Inside `gdisk`, enter:
```
n  # Create a new partition
1  # Partition number (first partition)
  # Press Enter to accept the default first sector
+500M  # Set partition size to 500MB
8300  # Use Linux filesystem type (or another type if needed)
```

### **3. Write Changes to Disk**
```
w  # Write changes
y  # Confirm
```

### **4. Verify Partition**
Run:
```bash
lsblk /dev/vdb
sudo gdisk -l /dev/vdb
```

For more details, check out [this guide](https://linuxconfig.org/how-to-manipulate-gpt-partition-tables-with-gdisk-and-sgdisk-on-linux) or [this tutorial](https://www.computernetworkingnotes.com/linux-tutorials/manage-linux-disk-partition-with-gdisk-command.html). Let me know if you need further customization! 🚀