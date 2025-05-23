# Study guide for AWS storage

 Here’s a **study guide** covering key AWS storage services to help you understand and compare them.

---
## Overview
Here are the AWS services that relates to storage.:

- **Object Storage 🗂️:** [Amazon S3](https://aws.amazon.com/what-is/object-storage/) is designed for storing and retrieving any amount of data from anywhere, making it ideal for web applications, backups, and data lakes.
- **Block Storage 💽:** [Amazon EBS](https://docs.aws.amazon.com/ebs/latest/userguide/what-is-ebs.html) provides persistent block-level storage for EC2 instances, functioning like a traditional hard drive.
- **Long-Term Archiving 📦:** [Amazon S3 Glacier](https://aws.amazon.com/archive/) offers low-cost storage optimized for data archiving and long-term backup.
- **File Storage 🗃️:** [Amazon EFS](https://aws.amazon.com/products/storage/) provides shared file storage, perfect for applications requiring a centralized file system.
- **Scalable Data Storage 🚀:** [Amazon S3](https://aws.amazon.com/products/storage/) allows for scalable, secure storage that can handle growing volumes of data seamlessly.

## **AWS Storage Services Study Guide**  

#### **1️⃣ Object Storage 🗂️ – Amazon S3**  
✔️ **What it is:** Scalable, secure cloud storage for any type of data.  
✔️ **Use cases:** Web applications, backups, big data analytics, media storage.  
✔️ **Key features:**  
   - Stores files as **objects** in buckets.  
   - Supports **versioning, encryption, and lifecycle policies**.  
   - Highly durable & available across regions.  
   - Integrates with AWS services like **CloudFront** (CDN).  

🔎 **Study Tip:** Learn how to **upload**, manage permissions, and use storage classes like S3 **Standard, Intelligent-Tiering, Glacier** for cost optimization.  

---

#### **2️⃣ Block Storage 💽 – Amazon EBS**  
✔️ **What it is:** Persistent storage for EC2 instances, similar to a hard drive.  
✔️ **Use cases:** Databases, high-performance workloads, boot volumes for EC2.  
✔️ **Key features:**  
   - **Attached to EC2** instances.  
   - Supports **snapshots for backup & recovery**.  
   - Options for **SSD (GP3, IO1, IO2) & HDD (ST1, SC1) performance**.  

🔎 **Study Tip:** Understand **volume types**, how to **create EBS volumes**, and how they **scale** for different workloads.  

---

#### **3️⃣ Long-Term Archiving 📦 – Amazon S3 Glacier**  
✔️ **What it is:** Low-cost storage for long-term backups & compliance data.  
✔️ **Use cases:** Regulatory archives, medical records, financial backups.  
✔️ **Key features:**  
   - **Retrieval options:** Expedited, Standard, Bulk (time varies).  
   - Designed for **cold storage** (rarely accessed data).  
   - **Data lifecycle rules** automate archiving.  

🔎 **Study Tip:** Compare **Glacier vs S3 Standard** storage classes for pricing and retrieval speeds.  

---

#### **4️⃣ File Storage 🗃️ – Amazon EFS**  
✔️ **What it is:** Managed **shared file storage**, accessible across multiple instances.  
✔️ **Use cases:** Web applications, machine learning models, shared team files.  
✔️ **Key features:**  
   - **Elastic storage growth** (scales automatically).  
   - Supports **NFS protocols** for file sharing.  
   - Two storage classes: **Standard & Infrequent Access (IA)** for cost savings.  

🔎 **Study Tip:** Learn how to **mount EFS to EC2** and compare **EFS vs EBS** for storage needs.  

---

#### **5️⃣ Scalable Data Storage 🚀 – Amazon S3**  
✔️ **What it is:** Scalable, secure, cost-effective storage that adapts to business needs.  
✔️ **Use cases:** High-growth startups, enterprises managing large datasets.  
✔️ **Key features:**  
   - **Lifecycle management** automates cost savings.  
   - **Multi-region replication** ensures redundancy.  
   - **Integrates with AWS analytics & AI services** for seamless workflows.  

🔎 **Study Tip:** Explore **S3 Intelligent-Tiering** and how it **automatically moves data** between storage classes to optimize costs.  




---

### **Final Study Tips**  
✅ Compare **S3 vs EBS vs EFS** – Know when to use each.  
✅ Learn **IAM permissions & security** for storage buckets & volumes.  
✅ Practice **creating, managing, and optimizing AWS storage solutions**.

