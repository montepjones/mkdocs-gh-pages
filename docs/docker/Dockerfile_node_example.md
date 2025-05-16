To Dockerize the Node.js app, you need to create a **Dockerfile** under `/node_app` and then build and run the container. 
Follow the below

This assumes you have a working node application located at /node_app/


### **Step 1: Create the Dockerfile**
Navigate to the `/node_app/` directory:
```bash
cd /node_app
```

Create the `Dockerfile`:
```bash
nano Dockerfile
```

Add the following content:
```dockerfile
# Use a Node image as the base
FROM node:latest

# Set the working directory
WORKDIR /node_app

# Copy package.json to the container
COPY package.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application files
COPY . .

# Expose port 5001
EXPOSE 5001

# Start the application using server.js
CMD ["node", "server.js"]
```
Save and exit.

---

### **Step 2: Build the Docker Image**
Run the following command to build the Docker image:
```bash
docker build -t nautilus/node-web-app .
```

---

### **Step 3: Run the Container**
Now, create and start the container using the required name and port mapping:
```bash
docker run -d --name nodeapp_nautilus -p 8094:5001 nautilus/node-web-app
```
- `-d`: Runs the container in detached mode.
- `--name nodeapp_nautilus`: Sets the container name.
- `-p 8094:5001`: Maps **host port 8094** to **container port 5001**.

---

### **Step 4: Verify the Running Container**
Check if the container is running:
```bash
docker ps
```

Confirm that the logs show no errors:
```bash
docker logs nodeapp_nautilus
```

---

### **Step 5: Test the Deployment**
Run the curl command to verify that the app is accessible:
```bash
curl http://localhost:8094
```

If the response comes back correctly, the app is running successfully! 🚀 Let me know if you need further tweaks or troubleshooting.
