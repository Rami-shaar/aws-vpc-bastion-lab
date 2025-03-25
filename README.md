# 🧱 AWS VPC Architecture: Bastion Host + Private EC2 Lab

This project demonstrates how to manually build a secure, production-style AWS VPC environment with public and private subnets, using a bastion host to access private resources.

## 📐 Architecture Overview

```
Custom VPC (10.0.0.0/16)
├── 🌐 Public Subnet (10.0.1.0/24)
│   └── 🟢 public-ec2 (Bastion Host with SSH & HTTP access)
└── 🔒 Private Subnet (10.0.2.0/24)
    └── 🔵 private-ec2 (No public IP, accessed via SSH from bastion)
```

---

## 🔧 What You Set Up

### ✅ Networking
- Custom **VPC**: `10.0.0.0/16`
- **Public Subnet**: `10.0.1.0/24`
- **Private Subnet**: `10.0.2.0/24`
- **Internet Gateway (IGW)** for public subnet
- **Route Table** with:
  - `0.0.0.0/0` → IGW (for public subnet)
  - Local route for internal traffic

### ✅ EC2 Instances
- **public-ec2** (Bastion host)
  - Public IP enabled
  - Key: `public-ec2.ppk`
  - Accessible via PuTTY or SSH
- **private-ec2** (Private compute node)
  - No public IP
  - Only accessible via `public-ec2` using internal SSH

### ✅ Security Groups
- `public-sg`: Allows SSH (22) + HTTP (80) from anywhere
- `private-sg`: Allows SSH **only** from inside the VPC (`10.0.0.0/16`)

---

## 🔐 How to Connect to Private EC2

1. SSH into **public-ec2**:
   ```bash
   ssh ec2-user@<public-ip>
   ```

2. From inside `public-ec2`, SSH into `private-ec2`:
   ```bash
   ssh -i public-ec2.pem ec2-user@<private-ip>
   ```

> Note: `.pem` key was uploaded to `public-ec2` using `pscp` and secured with `chmod 400`.

---

## 🧠 Skills Practiced

- AWS VPC architecture design
- Subnetting and route table configuration
- Security group design and access control
- Bastion host SSH pattern
- Key-based SSH authentication and file transfer
- Real-world cloud security patterns

---

## 🚀 Next Steps

- Add a **NAT Gateway** to give the private EC2 internet access
- Install and configure **Apache** or **Nginx** on private EC2
- Add a **load balancer** in front of a private EC2 group
- Automate this setup using **Terraform or CloudFormation**

---

## 📝 Author

**Rami Alshaar**  
Cloud Architect in Progress 🌩️  
[GitHub Profile](https://github.com/Rami-Shaar)


---

## 🏁 License

<without hardening.

