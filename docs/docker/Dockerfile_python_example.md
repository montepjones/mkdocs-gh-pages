# Dockerize the Python app and deploy it on **appserver**, follow these steps:
This assumes you have a python app under `/python_app/`

---

### **Step 1: Create the Dockerfile**
Navigate to the `/python_app/` directory:
```bash
cd /python_app
```

Create the `Dockerfile`:
```bash
nano Dockerfile
```

Add the following content:
```dockerfile
# Use a Python image as the base
FROM python:latest

# Set the working directory
WORKDIR /python_app

# Copy the dependencies file into the container
COPY src/requirements.txt .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the application files into the container
COPY src/ .

# Expose port 8087
EXPOSE 8087

# Run the Python application
CMD ["python", "server.py"]
```
Save and exit.

---

### **Step 2: Build the Docker Image**
Run the following command to build the Docker image:
```bash
docker build -t nautilus/python-app .
```

---

### **Step 3: Run the Container**
Now, create and start the container with the required port mapping:
```bash
docker run -d --name pythonapp_nautilus -p 8099:8087 nautilus/python-app
```
- `-d`: Runs the container in detached mode.
- `--name pythonapp_nautilus`: Sets the container name.
- `-p 8099:8087`: Maps **host port 8099** to **container port 8087**.

---

### **Step 4: Verify the Running Container**
Check if the container is running:
```bash
docker ps
```

Confirm that logs show no errors:
```bash
docker logs pythonapp_nautilus
```

---

### **Step 5: Test the Deployment**
Run the curl command to verify the app:
```bash
curl http://localhost:8099/
```

If you receive a response, the app is successfully deployed! 🚀 Let me know if you need adjustments or troubleshooting.
