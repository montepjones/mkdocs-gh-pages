# Create Network Interface

To accomplish this task, the DevOps team member should use the `docker network create` command
with the required parameters. Here's how to create the **Docker network** named `news`
with **macvlan drivers**, **subnet**, and **IP range** as specified:

## Step-by-Step Command

```sh
docker network create \
  --driver macvlan \
  --subnet=172.168.0.0/24 \
  --ip-range=172.168.0.0/24 \
  --gateway=172.168.0.1 \
  --opt parent=<network_interface> \
  news
```

### Explanation of Parameters

- `--driver macvlan` → Configures the network to use **macvlan**.
- `--subnet=172.168.0.0/24` → Defines the **subnet** for the network.
- `--ip-range=172.168.0.0/24` → Restricts IP addresses to a specific range.
- `--gateway=172.168.0.1` → Sets the **gateway IP** (modify as necessary).
- `--opt parent=<network_interface>` → Specifies the **host network interface** e.g., `eth0` ).
- `news` → Assigns the **network name**.

### Important Notes

✔️ **Ensure that the host system has macvlan support enabled.**  
✔️ **Replace `<network_interface>`** with the correct **network adapter** on the App Server.  
✔️ **Verify network settings** using `docker network inspect news`.

Once this network is created, it will be available for containers to use when deployed.
