# Group Creation and User Assignment

To achieve group-based access control, follow these steps across all App servers in the datacenter:

## Step 1: Create the Group

Run the following command to create the group named `<group_name>`. Replace `group_name` with you actual groupname

```sh
sudo groupadd <group_name>
```

This ensures the group exists before adding users.

## Step 2: Create the User (if it doesn't exist)
replace `<username>` with you actual username
Check if the user `<username>` already exists.

```sh
id <username>
```

If the user does **not** exist, create it:

```sh
sudo useradd -m -s /bin/bash <username>
```

The `-m` flag creates a home directory, and `-s /bin/bash` assigns Bash as the default shell.

## Step 3: Add User to the Group

Now, add `<username>` to `<group_name>`:

```sh
sudo usermod -aG <group_name> <username>
```

This ensures `<username>` becomes a member of the group.

## Step 4: Verify the Changes

Confirm that `<username>` has been added successfully:

```sh
groups <username>
```

To verify on multiple servers, you can use SSH to run these commands remotely across all App servers.

Let me know if you need automation scripts or further refinements! 🚀
