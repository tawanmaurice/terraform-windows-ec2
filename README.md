# Terraform — Windows Server 2022 on t3.large (RDP-ready)

Spin up a **Windows Server 2022** EC2 instance on a **t3.large** with RDP (3389) open, then connect via Remote Desktop.

---

## What this does
- Uses the **default VPC** in `us-east-1`
- Finds the latest **Windows Server 2022** AMI automatically
- Creates a Security Group allowing **RDP (3389)**
- Launches a **t3.large** instance
- Outputs the instance **ID**, **Public IP**, and a clickable **rdp://** URL

---

## Prerequisites
- **Terraform** v1.5+  
- **AWS CLI** authenticated to your account (`aws configure`)
- An **EC2 key pair** in `us-east-1` (e.g., `tawan-win.pem`)
  - If you need one:
    ```bash
    aws ec2 create-key-pair --region us-east-1 --key-name tawan-win \
      --query 'KeyMaterial' --output text > tawan-win.pem
    chmod 400 tawan-win.pem
    ```

> **Important:** In `main.tf`, set `key_name = "YOUR_KEYPAIR_NAME"` (e.g., `tawan-win`).

---

## Files
- `main.tf` — Terraform configuration
- `.gitignore` — ignores state files, `.terraform/`, PEM keys, etc.

---

## Deploy
```bash
terraform init
terraform fmt
terraform validate
terraform apply -auto-approve
