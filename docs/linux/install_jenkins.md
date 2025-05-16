Monte, here’s how you can install the latest **Jenkins Stable (LTS) release** on your Ubuntu virtual machine:

### **Step 1: Update Your System**
Before installing Jenkins, update your package list:
```bash
sudo apt update && sudo apt upgrade -y
```

### **Step 2: Install Java**
Jenkins requires Java. Install OpenJDK:
```bash
sudo apt install openjdk-17-jre -y
```
Verify the installation:
```bash
java -version
```

### **Step 3: Add Jenkins Repository**
Download and add the Jenkins repository key:
```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
```
Add the repository:
```bash
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

### **Step 4: Install Jenkins**
Update the package list and install Jenkins:
```bash
sudo apt update
sudo apt install jenkins -y
```

### **Step 5: Start and Enable Jenkins**
Start Jenkins:
```bash
sudo systemctl start jenkins
```
Enable Jenkins to start on boot:
```bash
sudo systemctl enable jenkins
```

### **Step 6: Verify Jenkins Status**
Check if Jenkins is running:
```bash
systemctl status jenkins
```

Once installed, you can access Jenkins via `http://your-server-ip:8080`. Let me know if you need help configuring it further! 🚀