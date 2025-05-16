# Map Port

To complete this task, follow these steps:

## **1. Pull the `nginx:stable` Docker image**

```sh
docker pull nginx:stable
```

This will download the **stable** version of the Nginx image.

### **2. Create a container named `media` from the pulled image**

```sh
docker run -d --name media -p 3004:80 nginx:stable
```

- `-d` → Runs the container in **detached mode** (keeps it running in the background).
- `--name media` → Names the container **`media`**.
- `-p 3004:80` → Maps host port `3004` to container port `80`
- `nginx:stable` → Specifies the image to use.

### **3. Verify the container is running**

```sh
docker ps
```

This will show all active containers—confirm that **`media`** is listed and running.

### **4. Test the Nginx container**

Now, check if Nginx is working by opening a browser or using `curl`:

```sh
curl http://localhost:3004
```

If Nginx is running properly, it should return the default welcome page.

Everything should be set up now! 🚀 Let me know if you need further help. 😊
