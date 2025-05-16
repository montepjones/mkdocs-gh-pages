# Linux User Data Transfer

You can achieve this using the `find` command in Linux. Here's how:

```sh
find /home/usersdata -type f -user ammar -exec cp --parents {} /media \;
```

## Explanation

- `find /home/usersdata` → Searches within the `/home/usersdata` directory.
- `-type f` → Filters only **files**, excluding directories.
- `-user ammar` → Finds files owned by the user `ammar`.
- `-exec cp --parents {} /media \;` → Copies files while preserving the directory structure.

## **Verification**

After execution, confirm the copied files using:

```sh
ls -R /media
```

Let me know if you need refinements or additional operations! 🚀
