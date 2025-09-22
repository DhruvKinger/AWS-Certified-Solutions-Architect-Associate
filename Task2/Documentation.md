# Task 2: Cost Optimization for Nexlify Solutions Website Hosting

## Scenario
Nexlify Solutions was previously hosting its company website on Amazon EC2 instances. The CIO raised concerns about high monthly costs, especially after learning that similar companies operate their websites for just a few dollars per month. Additionally, usage metrics showed that traffic primarily occurs during business hours, with minimal activity outside those times.

As the AWS Solutions Architect, I was tasked with evaluating the current infrastructure, identifying cost-saving opportunities, and implementing a more efficient solution aligned with business requirements.

---

## Phase 1: Legacy EC2 Setup

To demonstrate the original setup, I launched an EC2 instance to simulate the legacy hosting environment.

### EC2 Configuration
- **Instance Name**: `nexlify-web-legacy`
- **AMI**: Amazon Linux 2023
- **Instance Type**: `t2.micro`
- **Security Group**: Allowed SSH (22) and HTTP (80)
- **Web Server**: Apache installed and configured

### Website Setup
After connecting via SSH, I installed Apache and hosted a simple HTML page, using EC2 Instance Connect, and these snippets I had used.

```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
echo "<h1>Welcome to Nexlify Solutions</h1>" | sudo tee /var/www/html/index.html
```
