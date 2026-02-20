# 📦 AWS S3 Bucket Creation Assignment

## 📌 Problem Statement

XYZ Corporation requires a storage service to:

* Store application files
* Publicly share files when required

To implement this solution, we use **Amazon S3 (Simple Storage Service)**.

---

# 🎯 Objective

1. Create an S3 bucket
2. Upload 5 objects with different file extensions
3. Enable public access (if required)

---

# 🛠️ Service Used

* Amazon S3

Amazon S3 is an object storage service that provides scalable, secure, and durable file storage.

---

# 🚀 Step-by-Step Implementation

---

## Step 1: Login to AWS Console

* Open AWS Management Console
* Search for **S3**
* Click on **S3 Dashboard**

---

## Step 2: Create S3 Bucket

1. Click **Create bucket**
2. Enter:

   * Bucket Name (must be globally unique)
     Example: `xyz-corp-storage-bucket`
   * Region: Select preferred region
3. Keep default settings (or configure as required)
4. Click **Create bucket**

✅ Bucket successfully created.

---

## Step 3: Upload Objects

1. Open the created bucket
2. Click **Upload**
3. Click **Add files**
4. Select 5 files with different extensions, for example:

| File Name         | Extension |
| ----------------- | --------- |
| image.jpg         | .jpg      |
| document.pdf      | .pdf      |
| file.txt          | .txt      |
| presentation.pptx | .pptx     |
| data.csv          | .csv      |

5. Click **Upload**

✅ Files successfully uploaded.

---

## Step 4: Enable Public Access (If Required)

⚠️ By default, S3 blocks public access.

To make files public:

1. Go to bucket → **Permissions**
2. Edit **Block Public Access**
3. Disable block public access (if needed)
4. Save changes

---

## Step 5: Make Object Public

1. Open uploaded file
2. Click **Actions → Make Public**
3. Confirm

OR

Add bucket policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadAccess",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::xyz-corp-storage-bucket/*"
    }
  ]
}
```

---

## Step 6: Access Public File

1. Click on the object
2. Copy the **Object URL**
3. Open in browser

If configured correctly, file will open publicly.

---

# 🔐 Security Considerations

* Keep bucket private unless public sharing is required
* Use IAM policies for controlled access
* Enable versioning for data protection
* Enable server-side encryption for security

---

# ✅ Final Outcome

✔ Created S3 bucket
✔ Uploaded 5 different file types
✔ Configured optional public access
✔ Verified file accessibility

---

# 🏁 Conclusion

This implementation provides a scalable and secure file storage solution using Amazon S3. It allows XYZ Corporation to store and optionally share application files efficiently while maintaining control over access and security.
