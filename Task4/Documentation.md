# **Task 4: EC2 Instance Cost Optimization**

## **Current Findings**
The EC2 instance `qa-instance-1` was identified as having higher monthly costs compared to other instances. Based on the provided performance metrics:

- **CPU Utilization:** Peak 70%, Off-Peak 40%
- **Memory Usage:** Peak 60%, Off-Peak 20%
- **Disk IOPS:** Peak 75, Off-Peak 50

### **Observations**
- Current instance type: **t3.large** (2 vCPU, 8 GB RAM)
- Attached storage: **gp3 EBS** with 3000 baseline IOPS
- Estimated monthly cost: **~$70**
- The instance is over-provisioned for its workload. CPU and memory usage indicate that a smaller burstable instance can handle the load. Disk IOPS are well below gp3 baseline, so no storage upgrade is needed.

**Screenshots:** All screenshots are available in the attached folder.

---

## **What Needs to Change**
- **Right-size the instance** from `t3.large` → `t3.medium` (2 vCPU, 4 GB RAM) to reduce cost while maintaining performance.
- **Enable monitoring and alarms** for performance tracking.

---

## **Changes Made**

### **Step 1: Enabled Detailed Monitoring**
- Enabled **Detailed Monitoring** for `qa-instance-1` to capture granular performance metrics.

### **Step 2: Created CloudWatch Alarm**
- Configured an alarm for **CPUUtilization > 70% for 5 minutes** to monitor peak usage and trigger alerts.

### **Step 3: Verified EBS Volume**
- Confirmed attached volume type is **gp3** with 3000 IOPS baseline, which exceeds the observed peak of 75 IOPS. No changes required.

### **Step 4: Changed Instance Type**
- Stopped the instance and changed its type from `t3.large` to `t3.medium`.
- Restarted the instance and verified the new configuration.

**Screenshots:** All screenshots are available in the attached folder.

---

## **How It Meets Business Requirements**
- **Performance:** The new instance type (`t3.medium`) provides sufficient CPU and memory for peak usage (70% CPU, 60% memory).
- **Cost Optimization:** Monthly cost reduced by approximately 50%.
- **Storage:** gp3 volume already exceeds IOPS requirements, so no additional cost incurred.
- **Monitoring:** CloudWatch alarm ensures proactive performance tracking.

---

## **Cost Comparison**

| Instance Type | vCPU | Memory | Est. Monthly Cost |
|--------------|------|--------|--------------------|
| t3.large     | 2    | 8 GB   | ~$70              |
| t3.medium    | 2    | 4 GB   | ~$35              |

**Estimated Savings:** ~50%

---

## **Conclusion**
By right-sizing the instance, enabling monitoring, and validating storage configuration, we achieved significant cost savings while ensuring the instance meets performance requirements during peak load.

**Screenshots:** All screenshots are available in the attached folder.
