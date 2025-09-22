
# Task 2: Cost Optimization for Nexlify Solutions Website Hosting

##  Scenario
Nexlify Solutions was previously hosting its company website on Amazon EC2 instances. The CIO raised concerns about high monthly costs, especially after learning that similar companies operate their websites for just a few dollars per month. Additionally, usage metrics showed that traffic primarily occurs during business hours, with minimal activity outside those times.

As the AWS Solutions Architect, I was tasked with evaluating the current infrastructure, identifying cost-saving opportunities, and implementing a more efficient solution aligned with business requirements.

---

##  Phase 1: Legacy EC2 Setup (Simulated)

###  EC2 Configuration
- **Instance Name**: `nexlify-web-legacy`
- **AMI**: Amazon Linux 2023
- **Instance Type**: `t2.micro`
- **Security Group**: Allowed SSH (22) and HTTP (80)
- **Web Server**: Apache installed and configured

###  Website Setup
After connecting via EC2 Instance Connect, I installed Apache and hosted a simple HTML page, and these snippets I had used.

```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
echo "<h1>Welcome to Nexlify Solutions</h1>" | sudo tee /var/www/html/index.html
```

The website was successfully accessed via the EC2 public IP. I have included all the necessary screenshots.


##  Phase 2: Cost-Efficient Replacement – S3 + CloudFront
To reduce costs and align with traffic patterns, I implemented a static website hosting solution using Amazon S3 and CloudFront.

###  S3 Bucket Setup
- **Bucket Name**: `nexlify-company-site`
- **Static Website Hosting**: Enabled
- **Files Uploaded**: `index.html`
- **Bucket Policy**: Configured for public read access

###  CloudFront Distribution
- **Origin**: S3 bucket
- **Default Root Object**: `index.html`

###  Website Testing
The CloudFront domain successfully served the website content with improved performance and global availability.
I have included all the necessary screenshots.
 

---

##  Cost Comparison

| Hosting Option     | Estimated Monthly Cost |
|--------------------|------------------------|
| EC2 (`t2.micro`)   | ~$8–$15/month          |
| S3 + CloudFront    | ~$1–$3/month           |

Using S3 and CloudFront reduces hosting costs by over **80%**, while still meeting performance and availability needs.

---

##  Architecture Decision Justification
- EC2 is flexible but incurs higher costs due to compute, storage, and uptime.
- S3 + CloudFront is ideal for static content, offering scalability, global delivery, and minimal cost.
- The new setup aligns with traffic patterns (mostly business hours) and eliminates unnecessary compute charges.

---

##  Decommissioning Legacy Infrastructure
After confirming the new setup works:
- EC2 instance was stopped and terminated
- Associated resources (EBS, security group) were cleaned up

---

##  Outcome
The website is now hosted on a highly cost-efficient, scalable, and secure platform. This solution meets Nexlify’s business requirements and significantly reduces monthly AWS spend.
