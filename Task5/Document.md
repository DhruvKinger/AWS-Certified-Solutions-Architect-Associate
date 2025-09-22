# Task 5: NAT Gateway vs NAT Instance Cost Comparison

## 🧩 Scenario
DevMetrics uses NAT Gateways in two Availability Zones to allow backend microservices in private subnets to access the internet. Due to high outbound traffic (~1000GB/month), management requested a cost comparison between NAT Gateway and NAT Instance.

---

## 💰 Monthly Cost Comparison

### NAT Gateway
- **Service**: Amazon VPC
- **Region**: US East (Ohio)
- **Number of NAT Gateways**: 2
- **Monthly Cost**: **$155.70**

### NAT Instance
- **Service**: Amazon EC2
- **Instance Type**: t3.medium
- **Number of Instances**: 2
- **Pricing Model**: On-Demand
- **Monthly Cost**: **$60.74**

### 📊 Total Monthly Cost Comparison

| Option        | Monthly Cost |
|---------------|--------------|
| NAT Gateway   | $155.70      |
| NAT Instance  | $60.74       |

> **Source**: [AWS Pricing Calculator Estimate](https://calculator.aws/#/estimate?id=bc92a39: 09/22/2025  
> **File Submitted**: `Pricing-Calculator.pdf`

---

## 📊 Feature Comparison Table

| Attribute           | NAT Gateway                          | NAT Instance                          |
|---------------------|---------------------------------------|----------------------------------------|
| High Availability   | Built-in per AZ (auto failover)       | Manual setup with scripts              |
| Performance         | Scales up to 100 Gbps                 | Depends on EC2 instance type           |
| Scalability         | Auto-scaled by AWS                    | Manual scaling required                |
| Maintenance         | Fully managed by AWS                  | Requires patching, monitoring          |
| Security Groups     | Not supported                         | Supported                              |
| Port Forwarding     | Not supported                         | Supported                              |
| Bastion Use         | Not supported                         | Can be used as bastion host            |

---

## ✅ Recommendation
While NAT Gateways offer better scalability and zero maintenance, they are significantly more expensive. For cost-sensitive environments like DevMetrics, **NAT Instances** provide a viable alternative with over **60% cost savings**, assuming the team can manage the additional operational overhead.
