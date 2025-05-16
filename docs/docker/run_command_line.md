# deploy mysql

You can deploy a MySQL database using the mysql:5.6 image, naming the container mysql-db,
and attaching it to the wp-mysql-network. You'll also set the root password using the environment
variable MYSQL_ROOT_PASSWORD. Here's the command to do that:

```bash
docker run --name mysql-db --network wp-mysql-network \
  -e MYSQL_ROOT_PASSWORD=db_pass123 \
  -d mysql:5.6
```

Explanation:

- --name mysql-db → Names the container mysql-db.
- --network wp-mysql-network → Connects it to the newly created network.
- -e MYSQL_ROOT_PASSWORD=db_pass123 → Sets the root password.
- -d mysql:5.6 → Runs the container in detached mode using MySQL version 5.6.

To verify that your container is running, you can use:
