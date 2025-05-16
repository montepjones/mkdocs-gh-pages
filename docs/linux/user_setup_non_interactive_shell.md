# Linux User setup with a non interactive shell

You can create a user named `mark` with a non-interactive shell on App Server 3 by following these steps:

## **Step 1: Create the User with a Non-Interactive Shell**

Run the following command:

```sh
sudo useradd -M -s /sbin/nologin mark
```

- `-M` → Prevents the creation of a home directory.
- `-s /sbin/nologin` → Assigns a non-interactive shell, meaning the user can't log in.

## **Step 2: Verify the User Configuration**

Check if the user was created successfully:

```sh
getent passwd mark
```

This will show the user's details, including their assigned shell.

## **Step 3: Confirm Login Restriction**

Try switching to the user:

```sh
su - mark
```

If configured correctly, it should deny interactive login access.

This ensures security while allowing the backup agent tool to function as needed. Let me know if you need any tweaks! 🚀
