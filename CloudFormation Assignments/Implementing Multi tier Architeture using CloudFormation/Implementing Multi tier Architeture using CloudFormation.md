# 🏗️ Multi-Tier AWS Architecture
### Automated Infrastructure Deployment with CloudFormation

![AWS](https://img.shields.io/badge/AWS-CloudFormation-FF9900?style=flat-square&logo=amazon-aws&logoColor=white)
![EC2](https://img.shields.io/badge/EC2-t2.micro-232F3E?style=flat-square&logo=amazon-aws&logoColor=orange)
![RDS](https://img.shields.io/badge/RDS-MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![VPC](https://img.shields.io/badge/VPC-Multi--Tier-8C4FFF?style=flat-square&logo=amazon-aws&logoColor=white)
![Route53](https://img.shields.io/badge/Route_53-DNS-8C4FFF?style=flat-square&logo=amazon-aws&logoColor=white)

---

## 📌 Overview

This project provisions a **secure, scalable, three-tier web application infrastructure** on AWS using a single CloudFormation template. It sets up isolated network tiers for the web, application, and database layers — following AWS best practices for security and separation of concerns.

---

## 🏛️ Architecture

```
Internet
    │
    ▼
[ Web Tier ]  ──── Public Subnet (10.0.1.0/24)
  EC2 (t2.micro)   Allows: HTTP (80), SSH (22) from Internet
    │
    ▼
[ App Tier ]  ──── Private Subnet (10.0.2.0/24)
  EC2 (t2.micro)   Allows: SSH (22) from Web Tier only
    │
    ▼
[ DB Tier  ]  ──── Private Subnet (10.0.3.0/24)
  RDS MySQL        Allows: Port 3306 from App Tier only
```

---

## ⚙️ Resources Provisioned

| Resource | Details |
|---|---|
| **VPC** | `10.0.0.0/16` — Dev-VPC |
| **Internet Gateway** | Attached to VPC |
| **Public Subnet** | Web Tier — `10.0.1.0/24` |
| **Private Subnet** | App Tier — `10.0.2.0/24` |
| **Private Subnet** | DB Tier — `10.0.3.0/24` |
| **Web EC2 Instance** | `t2.micro`, HTTP + SSH open |
| **App EC2 Instance** | `t2.micro`, SSH from Web Tier only |
| **RDS MySQL** | `db.t3.micro`, port 3306 from App Tier only |
| **Route 53** | Hosted zone directing traffic to Web EC2 |

---

## 🚀 Deployment Steps

### Prerequisites
- AWS Account with appropriate IAM permissions
- An existing EC2 Key Pair
- A valid AMI ID for your region

### Step 1 — Prepare the Template
Clone this repository and locate `casestudy_template.yml`.

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
```

### Step 2 — Deploy via CloudFormation Console

1. Go to **AWS Console → CloudFormation → Create Stack**
2. Choose **Upload a template file** → select `casestudy_template.yml`
3. Click **Next** and enter the **Stack Name** (e.g., `CaseStudy`)
4. Fill in the parameters:

| Parameter | Description |
|---|---|
| `AmiId` | AMI ID for your region |
| `KeyName` | Existing EC2 Key Pair name |
| `DBName` | Database name (default: `testdb`) |
| `DBUser` | DB admin username (default: `dbadmin`) |
| `DBPassword` | DB admin password (min 8 chars) |

5. Skip optional steps → click **Submit**
6. Wait for `CREATE_COMPLETE` status (~5–10 minutes)

---

## 📤 Stack Outputs

Once deployed, the **Outputs** tab shows:

| Output | Description |
|---|---|
| `WebPublicIP` | Public IP of the Web EC2 instance |
| `AppPrivateIP` | Private IP of the App EC2 instance |
| `RDSEndpoint` | Connection endpoint for the MySQL database |

---

## 🔒 Security Design

```
WebSecurityGroup   → Inbound: 0.0.0.0/0 on port 80, 22
AppSecurityGroup   → Inbound: WebSecurityGroup on port 22
DBSecurityGroup    → Inbound: AppSecurityGroup on port 3306
```

Each tier is isolated — the database is never directly reachable from the internet, and the app tier is only reachable from within the web tier.

---

## 📝 Notes

- The RDS instance has a **`DeletionPolicy: Retain`** — it won't be deleted if the stack is torn down.
- RDS uses a **DB Subnet Group** spanning two AZs for high availability readiness.
- Route 53 can be configured post-deployment to point your domain to the `WebPublicIP`.

---

## 🧰 Tech Stack

`AWS CloudFormation` · `Amazon EC2` · `Amazon RDS (MySQL)` · `Amazon VPC` · `Amazon Route 53`

---
