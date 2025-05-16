To allow incoming connections on port `5001/tcp` and ensure the zone is set to `public`, follow these steps:

### **Step 1: Add Firewall Rule for Port 5001**
Run the following command to allow traffic on port `5001/tcp`:

```sh
sudo firewall-cmd --zone=public --add-port=5001/tcp --permanent
```

### **Step 2: Reload Firewalld to Apply Changes**
After adding the rule, reload the firewall:

```sh
sudo firewall-cmd --reload
```

### **Step 3: Verify the Rule**
Confirm that port `5001/tcp` is allowed in the `public` zone:

```sh
sudo firewall-cmd --zone=public --list-ports
```

This will display all allowed ports, including `5001/tcp`.

Once completed, the web UI application should be accessible. Let me know if you need any refinements! 🚀

