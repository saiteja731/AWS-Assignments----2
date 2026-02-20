# 🌐 AWS S3 Static Website Hosting & Lifecycle Rule Assignment

## 📌 Problem Statement

XYZ Corporation requires:

* File storage
* Public file access
* Static website hosting
* Automated storage cost optimization

To implement this solution, we use **Amazon S3**.

---

# 🎯 Objectives

1. Host a static website using existing S3 bucket
2. Upload `index.html` and `error.html`
3. Configure bucket policy for public access
4. Enable static website hosting
5. Create lifecycle rule:

   * Transition to Standard-IA after 60 days
   * Expire objects after 200 days

---

# 🚀 Step-By-Step Implementation

---

## Step 1: Upload Website Files

1. Open AWS Console
2. Go to **S3 Dashboard**
3. Open the previously created bucket
4. Click **Upload**
5. Upload:

   * `index.html`
   * `error.html`
6. Click **Upload**

✅ Bucket now contains website files.

---

## Step 2: Add Bucket Policy (Public Access)

To make website accessible:

1. Go to **Permissions**
2. Click **Bucket Policy → Edit**
3. Add the following policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadAccess",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

4. Click **Save Changes**

⚠️ Ensure Block Public Access settings are disabled if required.

---

## Step 3: Enable Static Website Hosting

1. Go to **Properties**
2. Scroll to **Static Website Hosting**
3. Click **Edit**
4. Select **Enable**
5. Enter:

   * Index document: `index.html`
   * Error document: `error.html`
6. Save changes

✅ Static website hosting enabled.

---

## Step 4: Access Website

After enabling:

* Copy the **Bucket Website Endpoint URL**
* Open in browser

You should see:

* `index.html` page
* `error.html` if page not found

---

# ♻️ Lifecycle Rule Configuration

To optimize storage cost:

---

## Step 5: Create Lifecycle Rule

1. Go to **Management**
2. Click **Create Lifecycle Rule**
3. Enter rule name
4. Select:

   * Apply to all objects (or specific prefix)

---

## Step 6: Configure Lifecycle Actions

### Transition Rule

* Transition current versions
* Storage Class: **Standard-IA**
* After: **60 days**

### Expiration Rule

* Expire current versions
* After: **200 days**

5. Click **Create**

✅ Lifecycle rule successfully enabled.

---

# 📊 Expected Outcome

✔ Static website hosted successfully
✔ Website accessible via public URL
✔ Lifecycle rule transitions objects after 60 days
✔ Objects expire automatically after 200 days
✔ Storage cost optimized

---

# 🔐 Security Considerations

* Enable versioning for data protection
* Use least-privilege bucket policies
* Monitor lifecycle transitions
* Enable encryption if required

---

# 🏁 Conclusion

Using **Amazon S3**, we successfully:

* Hosted a static website
* Configured public access securely
* Implemented automated lifecycle management
* Optimized long-term storage costs

This demonstrates scalable, cost-efficient cloud storage and hosting architecture for enterprise applications.
