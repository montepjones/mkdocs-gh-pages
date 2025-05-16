# Messege of the Day

To update the **Message of the Day (MOTD)** on all application and database servers in **Datacenter**, follow these steps:

---

## Step 1: Copy the Approved username to Each Server

Since the username file is located on the **jump host**, you need to copy it to the target servers.

```bash
scp /home/thor/nautilus_username user@server:/etc/motd
```

Replace `user@server` with the actual usernames and server IP addresses.

If you have multiple servers, use a loop:

```bash
SERVERS=("app-server1" "app-server2" "db-server1" "db-server2")
for SERVER in "${SERVERS[@]}"; do
  scp /home/thor/nautilus_username user@$SERVER:/etc/motd
done
```

---

## Step 2: Set Permissions

Ensure the **MOTD file** is readable:

```bash
sudo chmod 644 /etc/motd
```

---

## Step 3: Verify the MOTD is Applied

Log into each server and check the contents:

```bash
cat /etc/motd
```

Or log out and back in to see if the username displays upon login.

---

## Automating Using `pdsh` for Multiple Servers

If managing multiple servers, **parallel execution** using `pdsh` is helpful:

```bash
pdsh -w app-server1,app-server2,db-server1,db-server2 "scp /home/thor/nautilus_username root@{}:/etc/motd && chmod 644 /etc/motd"
```

Now, all servers should have the compliance-approved **MOTD** applied correctly! 🚀 Let me know if you need further adjustments.
