# 🚀 Static Portfolio Website Deployment on AWS S3 + CloudFront

![AWS](https://img.shields.io/badge/AWS-S3%20%2B%20CloudFront-orange?style=flat&logo=amazon-aws)
![Status](https://img.shields.io/badge/Status-Live-brightgreen?style=flat)
![HTTPS](https://img.shields.io/badge/HTTPS-Enabled-blue?style=flat)
![Cost](https://img.shields.io/badge/Cost-Free%20Tier-success?style=flat)

A professional cloud deployment project where I hosted my personal portfolio website using **Amazon S3** for static website hosting and **Amazon CloudFront** as a CDN for HTTPS, security, and global content delivery.

---

## 🌐 Live Links

| Type | URL |
|---|---|
| ✅ CloudFront (HTTPS) | https://du3a4hly0b8q9.cloudfront.net/ |
| S3 Website Endpoint | http://oarsu-santosh-kumar-portfolio.s3-website-us-east-1.amazonaws.com/ |

---

## 🏗️ Architecture

```
User Request (HTTPS)
        │
        ▼
┌───────────────────┐
│   CloudFront CDN  │  ← HTTPS, Global Edge Locations, Caching
│  (us-east-1)      │
└────────┬──────────┘
         │ HTTP (Origin fetch)
         ▼
┌───────────────────┐
│    Amazon S3      │  ← Static file storage, Website hosting
│  (us-east-1)      │
└───────────────────┘
```

---

## ☁️ AWS Services Used

| Service | Purpose |
|---|---|
| **Amazon S3** | Static website hosting, file storage |
| **Amazon CloudFront** | CDN, HTTPS termination, global delivery, caching |

---

## 📋 Deployment Steps

### Part 1 — Amazon S3 Setup

**Step 1 — Create S3 Bucket**
- AWS Console → S3 → Create bucket
- Bucket name: `oarsu-santosh-kumar-portfolio`
- Region: `us-east-1`

**Step 2 — Disable Block Public Access**
- Bucket → Permissions → Block public access → unchecked all 4 settings
- Also disabled at AWS account level: S3 → Block Public Access settings for this account

**Step 3 — Enable Static Website Hosting**
- Bucket → Properties → Static website hosting → Enable
- Index document: `index.html`

**Step 4 — Apply Bucket Policy**
- Bucket → Permissions → Bucket policy → applied public read policy (see below)

**Step 5 — Upload Portfolio Files**
- Uploaded `index.html`, CSS, JS, and image files at root level of bucket

**Step 6 — Verify S3 Link**
- Tested endpoint URL in incognito mode to confirm public access

---

### Part 2 — CloudFront Setup

**Step 1 — Create Distribution**
- AWS Console → CloudFront → Create distribution

**Step 2 — Configure Origin**
- Origin domain: `oarsu-santosh-kumar-portfolio.s3-website-us-east-1.amazonaws.com`
- Origin protocol: HTTP only

**Step 3 — Configure Behavior**
- Viewer protocol policy: **Redirect HTTP to HTTPS**
- Allowed HTTP methods: GET, HEAD

**Step 4 — General Settings**
- Default root object: `index.html`
- Price class: All edge locations

**Step 5 — Deploy & Test**
- Waited ~10 minutes for status to change from In Progress → Enabled
- Tested HTTPS link in incognito — padlock confirmed ✅

---

## 📄 Bucket Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::oarsu-santosh-kumar-portfolio/*"
    }
  ]
}
```

> **Note:** The `/*` at the end of the Resource is critical — it applies the policy to all files inside the bucket, not just the bucket itself.

---

## 💰 Cost

| Service | Cost |
|---|---|
| S3 Storage | ~$0.00/month (well within free tier) |
| CloudFront | $0.00/month (1 TB transfer + 10M requests free — permanent) |
| **Total** | **$0.00/month** |

---

## 🔑 Key Concepts Demonstrated

- **S3 Static Website Hosting** — serving HTML/CSS/JS files directly from S3
- **IAM Bucket Policies** — granting public read access using JSON policy
- **Block Public Access** — understanding both account-level and bucket-level settings
- **CloudFront CDN** — global content delivery with edge caching
- **HTTPS Configuration** — redirecting HTTP to HTTPS via CloudFront viewer protocol policy
- **Origin Protocol** — understanding S3 website endpoint vs S3 REST endpoint

---

## 👤 Author

**Santosh Kumar**
- GitHub: [@santosh-engineer](https://github.com/santosh-engineer)
- LinkedIn: [linkedin.com/in/santosh-kumar-oarsu-27290b2ba](https://linkedin.com/in/santosh-kumar-oarsu-27290b2ba)

---

## 📁 Repository Structure

```
aws-s3-portfolio-deployment/
├── README.md               ← Project documentation
├── bucket-policy.json      ← S3 bucket policy used
└── screenshots/            ← Proof of deployment
    ├── s3-bucket.png
    ├── static-hosting.png
    ├── cloudfront.png
    └── live-site.png
```

---

> ⭐ If you found this helpful, feel free to star this repository!
