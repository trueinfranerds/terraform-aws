# **AWS DevOps Engineer - Technical Task**

### **Objective**

The goal of this task is to evaluate your ability to design and implement AWS infrastructure using Terraform while following best practices in security, scalability, and automation. You will be deploying a complete environment with a VPC, an EKS cluster, an RDS instance, and supporting infrastructure.

---

### **0. Preparation**

1. Create an AWS account for the task (or use an existing one).
2. Create a GitHub repository for your Terraform code.
3. Set up **pre-commit hooks** with the following linters:
    - `terraform fmt` (to format Terraform code)
    - `tflint` (for static analysis of Terraform code)
    - `checkov` (for security analysis)

---

### **1. Deploy Staging VPC**

- **Region:** `eu-central-1`
- **Availability Zones:** `3`
- **Subnets:**
    - Public: `3`
    - Private: `3`
    - Isolated: `3`
- **NAT Gateways:** `1 per each public subnet`
- **Network ACLs:**
    - Public NACL: Allow only **HTTP (80)**, **HTTPS (443)**, and other necessary ports.
    - Private NACL: Allow traffic from **Public NACL** and **Isolated subnets**.
    - Isolated NACL: Allow only **PostgreSQL (5432)** from **Private subnets**.

---

### **2. Deploy EKS Cluster**

- **Control Plane:** High Availability (HA)
- **Auto Scaling Mode:** Disabled
- **Add-ons:** Enabled. deploy as you think you need
- **Managed Worker Node Group:** 1
- **Worker Nodes Location:** Private subnets
- **Security Groups:** Properly configured security groups everywhere
- **Application Load Balancer Controller:** Enabled
- **IAM Roles for Service Accounts (IRSA) with OIDC:** Enabled

---

### **3. Deploy Test Application and Expose it to the Internet**

- Deploy the **AWS 2048 game** (or another test app) in EKS.
- Expose it using **Application Load Balancer (ALB)**.
- Ensure proper security group settings.

---

### **4. Deploy RDS PostgreSQL**

- **Storage:** Extendable
- **KMS Encryption:** Enabled
- **Multi-AZ Deployment:** Enabled
- **Performance Insights:** Enabled
- **Password Management:**
    - Generate a **random password**.
    - Store it in **AWS Secrets Manager**.
- **Subnet Placement:** Isolated subnets

---

### **5. Deploy a Test Pod to Connect to the Database**

- Deploy a **test pod** with `psql` installed.
- Connect it to the **RDS PostgreSQL instance**.

---

### **6. Deploy an S3 Bucket**

- **KMS Encryption:** Enabled
- **Versioning:** Enabled

---

### **7. Deploy a Test Pod to Interact with the S3 Bucket**

- Deploy a **test pod** with the AWS CLI installed.
- Add a **Kubernetes service account**.
- Create an **IAM role** with proper S3 permissions.
- Implement **IRSA** for secure authentication.

---

### **Additional Requirements**

- **Terraform Only**: Implement everything using Terraform.
- **Multi-Account Structure**:
    - Assume you are working in a **multi-account AWS environment**.
    - Deploy everything to the **staging account first**.
    - Use **Terraform Workspaces** to manage different environments.
- **Code Quality & Documentation**:
    - Maintain a well-structured Terraform repository.
    - Follow best practices for Terraform module structure.
    - Include a **README.md** explaining your setup and how to deploy it.

---

Good luck! 🚀