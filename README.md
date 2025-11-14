
# AWS IAM – Least Privilege Access Control Project  
A complete hands-on implementation of AWS Identity & Access Management (IAM) following enterprise-grade **Least Privilege Security Best Practices**.

---

## 📌 Project Overview
This project demonstrates:

- IAM Users  
- IAM Groups  
- IAM Roles  
- Custom Least-Privilege Policies  
- MFA Setup  
- Strong Password Policy  
- Access Segregation  
- EC2 Role for secure access.

---

## 📂 Folder Structure

aws-iam-least-privilege-project/
│
├── README.md
├── architecture/
│ └── iam-architecture.png
└── iam/
├── create-user.md
├── create-group.md
├── create-role.md
├── custom-policy.json
└── attach-policy.md

## 🎯 Objectives

- Understand IAM fundamentals  
- Implement least-privilege access  
- Create custom IAM policies  
- Assign permissions only through groups  
- Create IAM Roles for EC2  
- Enable MFA for user authentication  
- Apply strong password policy  
- Use role-based access for workloads  

---

## 🧩 Architecture Summary
User (developer-shipra)
│
▼
IAM Group (s3-developer-group) ───► Custom Least-Privilege Policy
│
▼
Restricted Access to S3 Bucket (shipra-dev-bucket)

IAM Role (ec2-s3-readonly-role)
│
▼
Attached to EC2 Instance → Secure S3 Read Access

*(Place your diagram at: `/architecture/iam-architecture.png`)*


---

## 🧱 1. Create IAM User (developer-shipra)

### Steps:
1. IAM Console → Users → Create User  
2. Username: `developer-shipra`  
3. Enable **Console Access**  
4. Auto-generate password  
5. Skip permissions (will assign via group)  
6. Create User  

**Why?**  
Users should not get permissions directly. Always use **groups**.

---

## 🧱 2. Create IAM Group (s3-developer-group)

### Steps:
- IAM → Groups → Create Group  
- Name: `s3-developer-group`  
- Do **not** attach policies yet  

**Why?**  
Group-based permissioning = clean, scalable, enterprise-grade practice.

---

## 🧱 3. Create Custom Least-Privilege Policy

Steps in AWS:
1-IAM → Policies → Create Policy
2-Paste the JSON
3-Name: S3-Developer-LeastPrivilege
4-Create Policy

Why?
Gives minimum necessary access to only one bucket.

---

## 🧱 4. Attach Policy to Group

Steps:

1- IAM → Groups → s3-developer-group
2- Attach Policy → S3-Developer-LeastPrivilege
3- All group members will now inherit the permission.

---

## 🧱 5. Add User to Group

Steps:

1- IAM → Users → developer-shipra

2- Add user to → s3-developer-group

Result:
User now has strict S3-only, least-privilege access.

-- 

## 🧱 6. Create IAM Role for EC2 (S3 Read-Only)

Steps:

1- IAM → Roles → Create Role
2- Trusted entity: AWS Service
3- Use-case: EC2
4- Attach policy: AmazonS3ReadOnlyAccess
5- Role Name: ec2-s3-readonly-role
6- Create Role
7- Attach role to EC2 instance

Why?
EC2 must never use access keys.
IAM Roles provide temporary, secure credentials.

-- 

## 🔐 7. Enable MFA for User

Steps:

1-IAM → Users → developer-shipra

2-Security Credentials

3-Assign MFA → Virtual MFA App

4-Scan QR code

5-Enter 2 codes → Activate

Why?
Protects against credential theft and unauthorized access.

---

## 🔐 8. Apply Strong Password Policy

Steps:

1- IAM → Account Settings → Password Policy

2- Enable:

3- Minimum length 8

4- Require uppercase

5- Require lowercase

6- Require numbers

7- Require symbols

8- Expire passwords: 90 days

9- Prevent reuse of last 5 passwords

Why?
Meets compliance (ISO, SOC2, PCI-DSS).

---

## 🧪 Testing Access

User Test:

Log in as developer-shipra:

✔ Upload object → should work
✔ Download object → should work
✖ Delete bucket → denied
✖ Create bucket → denied
✖ Access EC2/RDS/VPC → denied

--- 

## Final Outcome

By completing this project, you have demonstrated:

✔ Cloud security fundamentals
✔ IAM architecture design
✔ Least-privilege permissions
✔ Custom policy creation
✔ Zero-trust authentication
✔ Role-based S3 access
✔ Enterprise-grade IAM workflow
