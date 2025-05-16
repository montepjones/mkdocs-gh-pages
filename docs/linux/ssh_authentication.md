To set up **password-less SSH authentication** from the `thor` user on the **jump host** to all app servers via their respective **sudo users**, follow these steps:

---

### **Step 1: Generate SSH Key on Jump Host**
Log in as `thor` on the jump host and generate an SSH key pair:
```bash
ssh-keygen -t rsa -b 4096
```
- Press `Enter` for the default location (`~/.ssh/id_rsa`).
- Leave the **passphrase empty** for password-less access.

---

### **Step 2: Copy the Public Key to Each App Server**
For each server, copy `thor`'s public key to the corresponding sudo user (e.g., `username` for appserver):

```bash
ssh-copy-id username@app-server1
ssh-copy-id username@app-server2
ssh-copy-id bruce@app-server3
```
Replace `username`, `username`, `bruce` with the respective sudo usernames and **app-serverX** with actual server names or IPs.

If `ssh-copy-id` isn’t available, manually copy the key:
```bash
cat ~/.ssh/id_rsa.pub | ssh username@app-server1 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys'
```

---

### **Step 3: Verify Password-less Login**
Test by running:
```bash
ssh username@app-server1
```
If it logs in **without a password**, authentication is working.

Repeat for other servers:
```bash
ssh username@app-server2
ssh bruce@app-server3
```

---

### **Step 4: Restrict Root Access (Optional for Security)**
Prevent password login in `/etc/ssh/sshd_config`:
```bash
PermitRootLogin no
PasswordAuthentication no
```
Then restart SSH:
```bash
sudo systemctl restart sshd
```

Now `thor` can access all app servers **without needing a password**, ensuring smooth automation for scripts. 🚀 Let me know if you need modifications!
