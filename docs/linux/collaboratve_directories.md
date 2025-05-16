# collaborative directory
To set up the **collaborative directory** with proper permissions and ownership

### **Step 1: Create the Directory**
```bash
sudo mkdir -p /dbadmin/data
```
- The `-p` ensures parent directories are created if they don’t exist.

### **Step 2: Create the Group**
Ensure the **dbadmin** group exists:
```bash
sudo groupadd dbadmin
```

### **Step 3: Set Group Ownership**
Assign ownership of the directory to the **dbadmin** group:
```bash
sudo chown :dbadmin /dbadmin/data
```

### **Step 4: Adjust Permissions**
Grant full **read/write/execute** permissions to the user and group, while restricting access from others:
```bash
sudo chmod 770 /dbadmin/data
```
- `770` means:
  - **Owner** (user): Read, Write, Execute (`rwx`)
  - **Group** (`dbadmin`): Read, Write, Execute (`rwx`)
  - **Others**: **No Access** (`---`)

### **Step 5: Ensure New Files Inherit Group Ownership**
To automatically assign files within `/dbadmin/data` to the **dbadmin** group:
```bash
sudo chmod g+s /dbadmin/data
```

### **Verification**
Check permissions using:
```bash
ls -ld /dbadmin/data
```
Ensure output shows:
```bash
drwxrwx---  root dbadmin ...
```

Now, only **users in the dbadmin group** can access and modify files inside `/dbadmin/data`, ensuring **secure collaboration**. 🚀 Let me know if you need any refinements!
