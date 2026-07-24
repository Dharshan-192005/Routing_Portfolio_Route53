<div align="center">

# ☁️ AWS Secure Static Website & Portfolio Hosting
### *End-to-End Cloud Architecture Deployment Guide*

![AWS](https://img.shields.io/badge/Cloud-AWS-orange?style=for-the-badge&logo=amazonaws)
![S3](https://img.shields.io/badge/Storage-Amazon%20S3-green?style=for-the-badge&logo=amazons3)
![CloudFront](https://img.shields.io/badge/CDN-CloudFront-purple?style=for-the-badge&logo=amazoncloudfront)
![Route53](https://img.shields.io/badge/DNS-Route%2053-blue?style=for-the-badge&logo=amazonaws)

</div>

---

## 🚀 Project Overview
This project documents the end-to-end architecture for hosting a secure, production-ready static portfolio website on AWS. It integrates **Amazon S3** for storage, **AWS Certificate Manager (ACM)** for SSL/TLS, **Amazon CloudFront** for global content delivery, and **Amazon Route 53** for custom domain mapping.

---

## 📸 Implementation Walkthrough

### Phase 1: Amazon S3 Storage Configuration
* **Console Home:** Logged into the AWS Management Console (`us-east-1`) viewing the central dashboard.  
  *Path: `screenshots/Screenshot (188).png`*
* **S3 Service Search & Setup:** Created a general-purpose bucket named `dharshan.shop`.  
  *Path: `screenshots/Screenshot (191).png`*
* **Public Access Controls:** Unchecked **Block all public access** and acknowledged the security settings.  
  *Path: `screenshots/Screenshot (192).jpg`*
* **Bucket Policy Setup:** Configured custom JSON bucket policies using the bucket ARN (`arn:aws:s3:::dharshan.shop`).  
  *Path: `screenshots/Screenshot (197).png`*

### Phase 2: SSL/TLS Certificate Generation (ACM)
* **Certificate Manager:** Requested and successfully issued an SSL/TLS certificate for `dharshan.shop` in the `us-east-1` region.  
  *Path: `screenshots/Screenshot (249).png`*

### Phase 3: CloudFront CDN Setup
* **Distribution Creation:** Set up a CloudFront distribution pointing to the S3 origin with **Redirect HTTP to HTTPS** and caching optimized.  
  *Path: `screenshots/Screenshot (244).png`*
* **SSL Attachment:** Bound the custom ACM certificate to the distribution for secure global delivery.  
  *Path: `screenshots/Screenshot (250).png`*

### Phase 4: Route 53 DNS Management
* **DNS Records:** Added domain validation CNAME records and configured an **Alias Record** routing traffic directly from `dharshan.shop` to the CloudFront distribution endpoint.  
  *Path: `screenshots/Screenshot (240).png` & `(248).jpg`*

---

## ⚙️ S3 Bucket Policy Reference
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::dharshan.shop/*"
        }
    ]
}
