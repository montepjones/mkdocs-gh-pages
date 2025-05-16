To locate and copy **all `.css` files** while maintaining the directory structure, follow these steps on **appserver**:

---

### **Step 1: Find All `.css` Files**
Run the following command to list all **`.css` files** (excluding directories) in `/var/www/html/beta`:
```bash
find /var/www/html/beta -type f -name "*.css"
```

---

### **Step 2: Copy Files While Preserving Parent Directory Structure**
Use the `find` command with `cp --parents` to copy only **`.css` files** while preserving their directory structure:
```bash
find /var/www/html/beta -type f -name "*.css" -exec cp --parents {} /beta \;
```

---

### **Key Considerations**
- **`find`** → Searches for all `.css` files.
- **`-type f`** → Ensures only **files** are selected (not directories).
- **`-exec cp --parents {} /beta \;`** → Copies files while retaining their parent directories.

---

### **Step 3: Verify the Copied Files**
List the copied files:
```bash
ls -R /beta
```

This ensures all `.css` files have been transferred securely **without copying unrelated content**.

Let me know if you need further adjustments! 🚀

