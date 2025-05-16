Got it! To create the requested Docker image **media:nautilus** from the running container **ubuntu_latest** on **Application Server 2**, follow these steps:

### **Steps to Commit the Container as an Image**
1. **Create a new image from the running container:**  
   Run the following command to commit the container's current state as an image:

   ```bash
   docker commit ubuntu_latest media:nautilus
   ```

2. **Verify the newly created image:**  
   To confirm that the image was created successfully, check the list of available Docker images:

   ```bash
   docker images | grep media
   ```

3. **Push the image to a registry (if needed):**  
   If the developer wants to share the image across different servers or teams, it can be tagged and pushed to a Docker registry:

   ```bash
   docker tag media:nautilus your_registry/media:nautilus
   docker push your_registry/media:nautilus
   ```

This ensures the developer’s container changes are safely backed up as a new image. Let me know if you need any further assistance! 🚀

