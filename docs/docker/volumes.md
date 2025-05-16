# Docker Volumes

To accomplish this task, the team member can follow these steps:

### **1. Pull the latest Nginx image**
```sh
docker pull nginx:latest
```
This will download the **latest version** of the Nginx image, but other versions will work as well.

### **2. Create a container named `news` from the pulled image**:
```sh
docker run -d --name news -v /opt/sysops:/usr/src/ nginx
```
- `-d` → Runs the container in **detached mode** (keeps it running).
- `--name news` → Names the container **news**.
- `-v /opt/sysops:/usr/src/` → **Maps** the host directory `/opt/sysops` to `/usr/src/` inside the container.

### **3. Copy `sample.txt` from `/tmp` to `/opt/sysops`**
```sh
cp /tmp/sample.txt /opt/sysops/
```
This ensures the file is inside the mounted volume so it can be accessed by the container.

### **4. Verify container is running**
```sh
docker ps
```
This lists all running containers—confirm that **`news`** is active.

### **5. (Optional) Check files inside the container**
If you want to confirm the file is accessible within the container:
```sh
docker exec -it news ls -l /usr/src/
```
This should show the `sample.txt` file inside the container.

Everything should now be set up! 🚀 Let me know if you need further assistance. 😊

