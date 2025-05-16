# Run Dockerfile
If you want to run a container using a Dockerfile, you'll need to follow these steps

### **Steps to Run a Container from a Dockerfile**
1. **Create a Dockerfile**  
   - Navigate to the directory where you want to create the Dockerfile:
     ```bash
     cd /opt/docker/
     ```
   - Create a new file named `Dockerfile`:
     ```bash
     nano Dockerfile
     ```:
   - Add the following content to the Dockerfile:
     ```dockerfile
     FROM httpd:latest
     COPY . /usr/local/apache2/htdocs
     EXPOSE 80
     ```
   - Save and exit.

2. **Build the Docker Image**  
   - Run the following command to build the image:
     ```bash
     docker build -t my-httpd .
     ```

3. **Run the Container**  
   - Start the container with the required parameters:
     ```bash
     docker run -d --name httpd -p 3003:80 -v /opt/finance:/usr/local/apache2/htdocs my-httpd
     ```
   - This command:
     - Runs the container in detached mode (`-d`).
     - Names the container `httpd`.
     - Maps port `3003` on the host to `80` inside the container.
     - Mounts the `/opt/finance` directory from the host to `/usr/local/apache2/htdocs` inside the container.

4. **Verify the Container is Running**  
   - Check the running containers:
     ```bash
     docker ps
     ```
   - Ensure that port mapping is correct:
     ```bash
     docker inspect httpd | grep -i "3003"
     ```

Now your `httpd` container should be up and running based on the Dockerfile! Let me know if you need any modifications or troubleshooting assistance.

