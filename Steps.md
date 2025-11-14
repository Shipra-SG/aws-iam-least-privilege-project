🧱 Attach Policy to Group
Steps:

1- IAM → Groups → s3-developer-group → Attach Policy
2- Select → S3-Developer-LeastPrivilege

Reason:
▶ All users in this group get exactly the same controlled access.


🧱 Add User to Group

Steps:
1- IAM → Users → developer-shipra → Groups → Add to Group
2- Select: s3-developer-group

Result:
✔ User now has least-privilege S3 access
✔ No other AWS access is allowed


🧱 Create IAM Role for EC2 (Read-Only S3)
Steps:

1- IAM → Roles → Create Role
2- Trusted Entity → AWS Service
3- Use case → EC2
4- Attach Policy → AmazonS3ReadOnlyAccess
5- Name → ec2-s3-readonly-role
6- Create Role
7- Attach role to EC2 instance during launch or after launch.

Reason:
▶ EC2 should never use access keys
▶ Roles are temporary, secure, auto-rotated


🔐 Enable MFA for User

Steps:
IAM → Users → developer-shipra → Security Credentials
Assign MFA → Virtual MFA App (Google Authenticator / Authy)

Enter 2 sequential codes → Activate

Reason:
▶ Prevents account compromise
▶ Zero trust principle



🔐 Apply AWS Strong Password Policy

Steps:
IAM → Account Settings → Password Policy

Enable:

Min length: 8
Uppercase required
Lowercase required
Numbers required
Symbols required
Expire passwords: 90 days
Prevent reuse: last 5

Reason:
▶ Mandatory for compliance (ISO, SOC2, PCI-DSS)



📘 Security Best Practices Followed

✔ No root access used
✔ Users have no direct permissions
✔ Group-based permissioning
✔ Custom least-privilege policy
✔ Role-based access for EC2
✔ MFA enabled
✔ Password policy enforced
✔ No access keys hardcoded anywhere