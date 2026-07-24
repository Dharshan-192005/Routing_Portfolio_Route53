AWS Secure Portfolio Hosting Project: End-to-End Walkthrough
🚀 Overview
This project details the end-to-end architecture for hosting a secure, production-ready static portfolio website on AWS using Amazon S3 for static asset storage, AWS Certificate Manager (ACM) for SSL/TLS certificates, Amazon CloudFront for global content delivery, and Amazon Route 53 for custom DNS management.

📸 Step-by-Step Implementation Guide
Phase 1: Amazon S3 Storage Configuration
1. AWS Console Home
Description: Logged into the AWS Management Console (us-east-1), viewing the central dashboard with recently accessed services and account overview.

Screenshot: screenshots/Screenshot (188).png

2. Service Search
Description: Searching for S3 via the top navigation search bar to open Scalable Storage in the Cloud.

Screenshot: screenshots/Screenshot (189).png

3. S3 Dashboard
Description: The Amazon S3 buckets dashboard. Click the Create bucket button to initialize a new bucket.

Screenshot: screenshots/Screenshot (190).png

4. Bucket Naming & Region
Description: Configured the general-purpose bucket type and entered the custom domain name (dharshan.shop) as the bucket name in US East (N. Virginia).

Screenshot: screenshots/Screenshot (191).png

5 & 6. Public Access Controls & Warnings
Description: Unchecked Block all public access and acknowledged the security risk warning to enable public-facing website architecture.

Screenshot: screenshots/Screenshot (192).jpg & screenshots/Screenshot (193).jpg

7. Default Encryption Settings
Description: Maintained default server-side encryption settings using S3-managed keys (SSE-S3) with bucket keys enabled.

Screenshot: screenshots/Screenshot (194).jpg

8, 9 & 10. Bucket Permissions & Policy ARN
Description: Reviewed the bucket's Permissions tab showing public access status as Off, and checked the empty Bucket policy section while referencing its unique Bucket ARN (arn:aws:s3:::dharshan.shop).

Screenshot: screenshots/Screenshot (195).png, screenshots/Screenshot (196).png, screenshots/Screenshot (197).png

Phase 2: SSL/TLS Certificate Generation (ACM)
11. AWS Certificate Manager (ACM) Dashboard
Description: Navigated to AWS Certificate Manager in the us-east-1 region, where an SSL/TLS certificate (dharshan.shop) has been successfully requested and issued (Issued status) to enable secure HTTPS communication.

Screenshot: screenshots/Screenshot (249).png

Phase 3: Amazon CloudFront Content Delivery Network (CDN) Setup
12 & 13. CloudFront Service Discovery
Description: Searched for and opened CloudFront from the AWS console, landing on the empty Distributions dashboard before creating a new distribution.

Screenshot: screenshots/Screenshot (241).png & screenshots/Screenshot (243).png

14. Distribution Custom Domain & Get Started
Description: Configured distribution details, entering dharshan.shop as a custom domain under a single website or app setup with Route 53 domain mapping integration.

Screenshot: screenshots/Screenshot (244).png

15. Origin Selection
Description: Selected the dharshan.shop Amazon S3 bucket from the popup list as the primary origin source for the CDN.

Screenshot: screenshots/Screenshot (245).png

16. Viewer Protocol & Cache Settings
Description: Set the viewer protocol policy to Redirect HTTP to HTTPS and selected the CachingOptimized policy for optimal static web performance.

Screenshot: screenshots/Screenshot (246).png

17. Security Protections (WAF)
Description: Chose Do not enable security protections to bypass AWS WAF configuration for this portfolio scope.

Screenshot: screenshots/Screenshot (247).png

18. Custom SSL/TLS Certificate Attachment
Description: Selected the pre-issued ACM custom SSL certificate for dharshan.shop to bind secure HTTPS encryption to the CloudFront distribution.

Screenshot: screenshots/Screenshot (250).png

Phase 4: Route 53 DNS Configuration
19. Hosted Zone DNS Validation Record
Description: Within the Route 53 hosted zone for dharshan.shop, a CNAME validation record was created to verify domain ownership for the ACM certificate.

Screenshot: screenshots/Screenshot (248).jpg

20. Final Alias Record Creation
Description: Created an alias record in Route 53 routing traffic directly from dharshan.shop to the configured CloudFront distribution endpoint using simple routing.

Screenshot: screenshots/Screenshot (240).png

⚙️ Reference Configuration Files
S3 Bucket Policy Template
JSON
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