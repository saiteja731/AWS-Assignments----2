Below is a clean, properly formatted **README.md** version ready to paste directly into your project.

---

# 🏗️ AWS VPC Case Study – Production & Development Networks

## 📌 Problem Statement

XYZ Corporation requires separate cloud environments for **Production** and **Development** teams.

The objective is to design, configure, and connect both environments using AWS networking services.

---

# 🌐 Production Network – 4 Tier Architecture

## Architecture Overview

* 1 VPC (Production Network)
* 5 Subnets:

  * **Public:** web
  * **Private:** app1, app2, dbcache, db
* EC2 instances in all subnets
* Internet Gateway for public access
* NAT Gateway for private outbound access
* VPC Peering (with Development Network)

---

## Step 1: Create Production VPC

* Navigate to VPC Dashboard
* Click **Create VPC**
* Name: `Production Network`
* CIDR: `10.0.0.0/16`
* Create

---

## Step 2: Create Subnets

Create five subnets inside Production VPC:

| Subnet Name | Type    |
| ----------- | ------- |
| web         | Public  |
| app1        | Private |
| app2        | Private |
| dbcache     | Private |
| db          | Private |

All subnet CIDRs must fall under `10.0.0.0/16`.

---

## Step 3: Create and Attach Internet Gateway

* Create Internet Gateway
* Name: `production_network_ig`
* Attach to Production VPC

---

## Step 4: Configure Route Tables

### Public Route Table

* Add Route:

  * Destination: `0.0.0.0/0`
  * Target: Internet Gateway
* Associate with **web subnet**

### Private Route Table

* Associate with:

  * app1
  * app2
  * dbcache
  * db

---

## Step 5: Launch EC2 Instances

Launch one EC2 instance in each subnet using Amazon EC2:

* web
* app1
* app2
* dbcache
* db

Instance names must match subnet names.

---

## Step 6: Bastion Host Setup (SSH Access)

1. Connect to **web** instance (public subnet)
2. From web instance, SSH into private instances:

```bash
ssh -i key.pem ec2-user@<private-ip>
```

Private instances are not directly accessible from the internet.

---

## Step 7: Create NAT Gateway

* Create NAT Gateway in **web (public subnet)**
* Allocate Elastic IP
* Create

---

## Step 8: Enable Internet for Private Subnets

Edit Private Route Table:

* Add Route:

  * Destination: `0.0.0.0/0`
  * Target: NAT Gateway

Test inside private instance:

```bash
ping google.com
```

Only outbound internet access is allowed.

---

# 🧪 Development Network – 2 Tier Architecture

## Architecture Overview

* 1 VPC (Development Network)
* 2 Subnets:

  * web (Public)
  * db (Private)
* Only web subnet should access internet

---

## Step 1: Create Development VPC

* Name: `Development Network`
* CIDR: `10.1.0.0/16`

---

## Step 2: Create Subnets

| Subnet | Type    |
| ------ | ------- |
| web    | Public  |
| db     | Private |

---

## Step 3: Create Internet Gateway

* Create Internet Gateway
* Attach to Development VPC

---

## Step 4: Configure Public Route Table

* Add Route:

  * Destination: `0.0.0.0/0`
  * Target: Internet Gateway
* Associate with **web subnet**

Do NOT add internet route to db subnet.

---

## Step 5: Launch EC2 Instances

* Launch one instance in web subnet
* Launch one instance in db subnet

---

# 🔗 VPC Peering (Production ↔ Development)

## Step 1: Create Peering Connection

* Create Peering Connection

  * Requester: Production VPC
  * Accepter: Development VPC
* Accept request

---

## Step 2: Update Route Tables

In both VPCs:

* Add Route:

  * Destination: Other VPC CIDR
  * Target: Peering Connection (pcx)

This enables cross-VPC communication.

---

## Step 3: Test Connectivity

1. Connect to Production web instance
2. SSH into Production db
3. From there, SSH into Development db

Successful connection confirms working peering.

---

# 🔐 Security Configuration

* Configure Security Groups:

  * Allow SSH (22) only from trusted IP
  * Allow DB access only from required subnets
* Configure NACLs for additional subnet-level security

---

# ✅ Final Outcome

✔ Production 4-tier architecture
✔ Development 2-tier architecture
✔ Secure private subnets
✔ NAT-based outbound internet access
✔ Bastion host access model
✔ VPC Peering between environments
✔ Secure DB-to-DB communication

---

# 🏁 Conclusion

This project demonstrates secure enterprise network architecture using AWS VPC, multi-tier subnet design, NAT configuration, and VPC Peering to simulate real-world production and development environments.
