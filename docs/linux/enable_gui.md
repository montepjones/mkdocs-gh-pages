To enable GUI booting by default on all App servers within the company-name Datacenter **without rebooting**, follow these steps:

### **Step 1: Change the Default Runlevel to Graphical Mode**
Run the following command to set the default target to graphical mode:

```sh
sudo systemctl set-default graphical.target
```

This ensures that on future startups, the servers boot into GUI mode.

### **Step 2: Confirm the Change**
Verify the default target setting using:

```sh
systemctl get-default
```

It should return:

```sh
graphical.target
```

### **Step 3: Start GUI Mode Immediately (Without Reboot)**
Apply the graphical mode **without rebooting** by running:

```sh
sudo systemctl isolate graphical.target
```

This switches the current session to GUI mode while keeping the system running.

### **Step 4: Validate GUI is Running**
Check the status of the graphical target:

```sh
systemctl status graphical.target
```

If everything is configured correctly, the system should now be running with GUI enabled **without requiring a reboot**.

Let me know if you need additional modifications! 🚀
