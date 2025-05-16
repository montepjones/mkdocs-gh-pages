# Save load and transfer image

### **Step 1: Save the Docker Image on appserver**
Run the following command to save the **`blog:datacenter`** image into an archive (`blog_datacenter.tar`):
```sh
docker save -o /tmp/blog_datacenter.tar blog:datacenter
```
This command **creates a tar archive** of the image.

### **Step 2: Transfer the Archive to App Server 3**
Use `scp` (or `rsync`) to transfer the file to App Server 3:
```sh
scp /tmp/blog_datacenter.tar user@<AppServer3_IP>:/tmp/
```
Replace `<AppServer3_IP>` with the actual IP address of App Server 3, and ensure SSH access is configured.

### **Step 3: Load the Image on App Server 3**
Once the file is available on App Server 3, load the image using:
```sh
docker load -i /tmp/blog_datacenter.tar
```
After loading, **verify the image exists** using:
```sh
docker images | grep blog
```
It should show:
```
blog    datacenter   <IMAGE_ID>   <SIZE>
```

### **Bonus: Ensure Docker Service is Running**
If Docker is not running, start it using:
```sh
systemctl start docker
```
or, for systems using `service`:
```sh
service docker start
```

Everything should now be set up! 🚀 Let me know if you need any further assistance. 😊

