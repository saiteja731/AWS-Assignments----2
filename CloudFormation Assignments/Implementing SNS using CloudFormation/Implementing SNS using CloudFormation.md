# 📬 CloudFormation Stack with SNS Email Notifications

![AWS](https://img.shields.io/badge/AWS-CloudFormation-FF9900?style=flat-square&logo=amazon-aws&logoColor=white)
![SNS](https://img.shields.io/badge/Amazon-SNS-FF4F8B?style=flat-square&logo=amazon-aws&logoColor=white)
![S3](https://img.shields.io/badge/Amazon-S3-569A31?style=flat-square&logo=amazon-s3&logoColor=white)

---

## 📌 Overview

This project demonstrates how to use **AWS CloudFormation** with **Amazon SNS (Simple Notification Service)** to receive real-time **email notifications for every event** during a stack's creation process. The CloudFormation template provisions an S3 bucket with versioning enabled.

---

## 🎯 Tasks Performed

1. Reused the CloudFormation template from Task 1 (S3 bucket creation)
2. Attached an **SNS topic** to the stack to trigger email alerts at every step of stack provisioning

---

## 🏗️ What Gets Deployed

| Resource | Details |
|---|---|
| **S3 Bucket** | `intellipaat-chathasaiteja` with versioning enabled |
| **SNS Topic** | `cloudformation_stack_notifications` |
| **Email Subscription** | Confirmed via inbox link |

---

## 🚀 Deployment Steps

### Step 1 — Prepare the Template

Use the S3 bucket template (`assignment1.yml`) from Task 1:

```yaml
Resources:
  myS3bucket:
    Type: 'AWS::S3::Bucket'
    Properties:
      BucketName: intellipaat-chathasaiteja
      VersioningConfiguration:
        Status: Enabled

Outputs:
  OutputS3:
    Value: !Ref myS3bucket
```

### Step 2 — Create the Stack

1. Go to **AWS Console → CloudFormation → Create Stack**
2. Select **Upload a template file** → choose `assignment1.yml`
3. Enter a **Stack Name** (e.g., `Assignment-3`)
4. Click **Next**

### Step 3 — Configure SNS Notifications

1. On the **Configure stack options** page, scroll to **Notification options**
2. Click **Create new SNS topic**
3. Enter:
   - **SNS Topic Name:** `cloudformation_stack_notifications`
   - **Email Address:** your email
4. Click **Create SNS topic**
5. Open your inbox → click **Confirm subscription** in the AWS email
6. Click **Next → Submit**

---

## 📧 Email Notifications

Once the stack starts deploying, AWS SNS sends an email for **every stack event**, including:

| Event | Status |
|---|---|
| Stack creation started | `CREATE_IN_PROGRESS` |
| S3 Bucket creating | `CREATE_IN_PROGRESS` |
| S3 Bucket created | `CREATE_COMPLETE` |
| Stack creation complete | `CREATE_COMPLETE` |

> ✅ You will receive a separate email notification for each event in real time.

---

## ✅ Verification

After deployment:
- **CloudFormation → Stacks → Assignment-3 → Events** — shows all stack events
- **S3 Console** — confirms the bucket was created successfully
- **Inbox** — shows a thread of AWS notification emails for each event

---



## 🧰 Tech Stack

`AWS CloudFormation` · `Amazon S3` · `Amazon SNS` · `Email Notifications`

---


