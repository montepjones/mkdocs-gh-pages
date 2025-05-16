# pull and retag an image

1. **Pull the BusyBox image**  
   On **appserver** in **company-name**, run the following command to pull the BusyBox image with `musl`:

   ```bash
   docker pull busybox:musl
   ```

2. **Retag (Create a New Tag)**  
   Once the image is pulled, you can re-tag it as `busybox:media` using:

   ```bash
   docker tag busybox:musl busybox:media
   ```

3. **Verify the Image Tagging**  
   To confirm the changes, list the images and check for the new tag:

   ```bash
   docker images | grep busybox
   ```

This should help you achieve the required task efficiently! If you need any further assistance, feel free to ask. 🚀
`
