
To grant **kirsty** the ability to run Docker commands without `sudo`, follow these steps:

1. **Add the User to the Docker Group**  
   Run the following command on **appserver** to add `kirsty` to the `docker` group:

   ```bash
   sudo usermod -aG docker kirsty
   ```

2. **Apply Group Changes**  
   The user needs to log out and log back in for the changes to take effect. You can prompt **kirsty** to do so or restart the system.

3. **Verify Access**  
   Once logged back in, check if **kirsty** can run Docker commands without `sudo`:

   ```bash
   docker ps
   ```

If the command runs successfully without requiring `sudo`, the setup is complete. If you run into any issues, let me know—I’ve got your back! 🚀
