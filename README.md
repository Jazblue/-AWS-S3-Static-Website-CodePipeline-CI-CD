# -AWS-S3-Static-Website-CodePipeline-CI-CD
This project hosts a static HTML website on Amazon S3 and automatically deploys updates using AWS CodePipeline and CodeBuild.

Project Overview

The pipeline monitors a GitHub repository for changes.  
When new code is pushed, it automatically:

1. Pulls the latest source code
2. Runs a CodeBuild process to prepare the artifact
3. Deploys the output to an S3 bucket configured for static website hosting

**Outcome:** Any commit to the main branch updates the live website automatically.

---

## 🏗️ Architecture

GitHub → CodePipeline → CodeBuild → S3 Static Website Hosting

yaml
Copy code

---

## 🗂 Technologies Used

- **Amazon S3** (static site hosting)
- **AWS CodePipeline** (CI/CD)
- **AWS CodeBuild** (build + artifact packaging)
- **GitHub** (source control)
- **IAM** (permissions for pipeline roles)

---

## 📦 Project Files

| File | Purpose |
|------|---------|
| `s3site.html` | Main website page |
| `buildspec.yml` | CodeBuild instructions |
| `README.md` | Project documentation |

---

## 🔧 Setup Instructions

### 1. Enable Static Website Hosting on S3
- Upload `s3site.html` to the bucket root
- Enable **Static Website Hosting**
- Set index document: `s3site.html`

### 2. Bucket Policy for Public Read

{
"Version": "2012-10-17",
"Statement": [
{
"Effect": "Allow",
"Principal": "",
"Action": "s3:GetObject",
"Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/"
}
]
}

yaml
Copy code

### 3. Create the Pipeline

- Source: GitHub (select repository)
- Build: CodeBuild project (uses `buildspec.yml`)
- Deploy: S3 (select your hosting bucket)

---

## 🛠️ Common Issues + Fixes

| Issue | Fix |
|-------|-----|
| Browser downloads HTML | Set `Content-Type: text/html` |
| “Access denied” | Check bucket policy + public access blocked? |
| Deploy fails | Artifact name mismatch between Build and Deploy |
| Site unreachable | Use the **website endpoint**, not object URL |

---

## 📬 Future Enhancements (Optional)

- Add CloudFront (HTTPS + CDN)
- Use Route 53 for a custom domain
- Enable versioning for rollback
- Add caching and compression

---

## 🎉 Result

✔ Automatic CI/CD build + deploy  
✔ Fully hosted static website on AWS  
✔ Beginner-friendly and interview-ready project!


There is a yaml file, I have sadly lost the original file, to get everything up and working as a Cloudformation template, so this code may need playing around to get right. 


