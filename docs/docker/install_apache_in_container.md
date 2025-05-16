To install Apache2 within a running Docker container, you'll typically access the container's shell, install the package, and then restart the container. This approach is not ideal for production environments, as changes made inside a container won't persist unless you commit the changes to a new image. [1, 2, 3]  
Here's a step-by-step guide: 
1. Get the Container ID: [4]  

• Use docker ps to list all running containers and note down the ID or name of the container you want to modify. [4]  

2. Access the Container's Shell: [3]  

• Use docker exec -it &lt;container_id&gt; bash to enter a bash shell within the container. Replace &lt;container_id&gt; with the actual ID you found in step 1. [3]  

3. Install Apache2: [2]  

• Inside the container, use the appropriate package manager for your container's base image (e.g., apt-get install apache2 -y for Ubuntu-based images). [2]  
• You might also need to install other essential tools like net-tools. [1]  

4. Restart the Container (Optional, but recommended): [4]  

• If you need to ensure the new package is properly loaded, you can restart the container using docker restart &lt;container_id&gt;. [4]  

5. (Optional) Commit Changes: [3]  

• If you want to create a new image based on the modified container, you can use docker commit &lt;container_id&gt; &lt;new_image_name&gt;. [3]  

Important Considerations: [3]  

• Container Persistence: Changes made within a running container are generally not persistent across container restarts, unless you commit them to a new image. [3]  
• Best Practices: For production deployments, it's generally recommended to build a new Docker image that includes Apache2 from the start using a Dockerfile. [5, 6]  
• Networking: If you're running the web server on a specific port, ensure you're mapping the correct ports between the host and the container. [4]  

************************
To complete the pending configuration on the **cloud** container running on **appserver**, follow these steps:

### **1. Install Apache2 in the Container**
   First, access the container and install Apache using `apt`:

   ```bash
   docker exec -it cloud bash
   apt update && apt install -y apache2
   ```

### **2. Configure Apache to Listen on Port 8083**
   Modify the Apache ports configuration file:

   ```bash
   sed -i 's/Listen 80/Listen 8083/' /etc/apache2/ports.conf
   sed -i 's/<VirtualHost *:80>/<VirtualHost *:8083>/' /etc/apache2/sites-enabled/000-default.conf
   ```

   Restart Apache to apply the changes:

   ```bash
   systemctl restart apache2
   ```

### **3. Ensure Apache is Running & Keep the Container Alive**
   Check if Apache is running inside the container:

   ```bash
   systemctl status apache2
   ```

   To ensure the container stays running, detach from the interactive session with `Ctrl + P + Q` or run the container with a persistent process.

This ensures the **cloud** container is properly configured and running with the required setup. 🚀 Let me know if you need any modifications!

docker update --restart unless-stopped cloud
