# 📦 AWS S3 Bucket Versioning Assignment

## 📌 Problem Statement

XYZ Corporation requires a storage service that can:

* Store application files
* Publicly share files when required
* Maintain multiple versions of files

To implement this, we use **Amazon S3** with Versioning enabled.

---

# 🎯 Objective

1. Enable versioning on the existing S3 bucket
2. Re-upload any 2 files
3. Verify that multiple versions are stored

---

# 🛠️ What is Versioning?

Versioning in Amazon S3 allows you to:

* Keep multiple versions of the same object
* Recover deleted files
* Restore previous file versions
* Protect against accidental overwrite

---

# 🚀 Step-by-Step Implementation

---

## Step 1: Open S3 Dashboard

1. Login to AWS Console
2. Search for **S3**
3. Open the bucket created in Assignment 1

---

## Step 2: Enable Bucket Versioning

1. Go to **Properties** tab
2. Scroll to **Bucket Versioning**
3. Click **Edit**
4. Select **Enable**
5. Click **Save Changes**

✅ Versioning is now enabled.

---

## Step 3: Upload Same Files Again

1. Go to **Objects** tab
2. Click **Upload**
3. Re-upload any two existing files

   * Example:

     * document.docx
     * data.csv
4. Click **Upload**

---

## Step 4: Verify Versioning

1. Click **Show versions**
2. You will see:

   * New Version ID for newly uploaded files
   * Old version marked with previous Version ID
   * Files uploaded before enabling versioning show **null** version ID

✅ Multiple versions are now stored successfully.

---

# 🔎 Expected Output

* Same file name appears multiple times
* Each file has a unique **Version ID**
* Old versions are retained
* No data is permanently overwritten

---

# 🔐 Benefits of Versioning

✔ Protects from accidental deletion
✔ Enables rollback to previous versions
✔ Improves data durability
✔ Supports compliance requirements

---

# ✅ Final Outcome

* Versioning enabled on S3 bucket
* Two files re-uploaded
* Multiple versions verified
* Data protection successfully implemented

---

# 🏁 Conclusion

By enabling versioning in **Amazon S3**, XYZ Corporation ensures safer storage management, prevents accidental data loss, and maintains complete file history for application storage.
