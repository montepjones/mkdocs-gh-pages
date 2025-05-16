Monte, here’s how to **install, configure, and deploy** the Java-based application using **Tomcat** on **appserver**.

---

## **Step 1: Install Tomcat Server**
1. **Update the system**:
   ```bash
   sudo yum update -y
   ```
2. **Install Tomcat**:
   ```bash
   sudo yum install -y tomcat
   ```

---

## **Step 2: Configure Tomcat to Run on Port 8082**
1. **Open the Tomcat configuration file**:
   ```bash
   sudo nano /etc/tomcat/server.xml
   ```
2. **Locate the following section**:
   ```xml
   <Connector port="8080" protocol="HTTP/1.1"
              connectionTimeout="20000"
              redirectPort="8443" />
   ```
3. **Change `port="8080"` to `port="8082"`**:
   ```xml
   <Connector port="8082" protocol="HTTP/1.1"
              connectionTimeout="20000"
              redirectPort="8443" />
   ```
4. **Save and exit**.

---

## **Step 3: Deploy ROOT.war**
1. **Transfer `ROOT.war` from Jump Host to appserver**:
   On the **Jump Host**, run:
   ```bash
   scp /tmp/ROOT.war user@stapp01:/tmp/
   ```

2. **Move `ROOT.war` to Tomcat’s deployment directory**:
   ```bash
   sudo mv /tmp/ROOT.war /var/lib/tomcat/webapps/ROOT.war
   ```
   This ensures the app is deployed at the base URL.

---

## **Step 4: Start Tomcat and Verify Deployment**
1. **Enable and Start Tomcat**:
   ```bash
   sudo systemctl enable tomcat
   sudo systemctl start tomcat
   ```

2. **Check if Tomcat is running**:
   ```bash
   sudo systemctl status tomcat
   ```

3. **Verify Deployment**:
   Run:
   ```bash
   curl http://stapp01:8082
   ```
   If successful, you should see the webpage output.

---

Everything should now be **installed, configured, and deployed** as required. 🚀 Let me know if you run into any issues!