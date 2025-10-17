# **Task 4: EC2 Instance Cost Optimization**

## **Current Findings**
The EC2 instance `qa-instance-1` was identified as having higher monthly costs compared to other instances. Based on the provided performance metrics:

- **CPU Utilization:** Peak 70%, Off-Peak 40%
- **Memory Usage:** Peak 60%, Off-Peak 20%
- **Disk IOPS:** Peak 75, Off-Peak 50

### **Observations**
- Current instance type: **t3.large** (2 vCPU, 8 GB RAM)
- Attached storage: **gp3 EBS** with 8 GiB size and 3000 baseline IOPS (minimum allowed for gp3)
- Estimated monthly cost: **~$70**
- The instance's CPU and memory usage are appropriate for its workload and do not indicate over-provisioning. Disk IOPS are well below the gp3 minimum, indicating the storage is over-provisioned due to AWS service constraints.

**Screenshots:** All screenshots are available in the attached folder.

---

## **What Needs to Change**
- **Right-size storage IOPS** to match workload and minimize costs, within AWS constraints (gp3 minimum 3000 IOPS).
- **Enable monitoring and alarms** for performance tracking.

---

## **Changes Made**

### **Step 1: Verified EC2 Instance Sizing**
- Reviewed performance metrics for CPU and memory.
- Decided to retain the instance type as `t3.large` because it is appropriately sized for peak workload (70% CPU, 60% memory).

### **Step 2: Verified and Modified EBS Volume**
- Reviewed the attached EBS volume settings.
- Attempted to reduce IOPS to match observed peak of 75 IOPS. However, AWS requires a minimum of 3000 IOPS for gp3 volumes, regardless of size (see Image 1).
- Set IOPS to **3000** (minimum allowed), and confirmed volume throughput is set to baseline (125 MiB/s).
- Did not change to gp2 volume type since it cannot guarantee 3000 IOPS for small volumes (e.g., 8 GiB).

### **Step 3: Enabled Detailed Monitoring**
- Enabled **Detailed Monitoring** for `qa-instance-1` for 1-minute granularity performance metrics.

### **Step 4: Created CloudWatch Alarm**
- Configured an alarm for **CPUUtilization > 70% for 5 minutes** to monitor peak usage and trigger alerts.

**Screenshots:** All screenshots, including the EBS modify volume screen and alarm configurations, are available in the attached folder.

---

## **How It Meets Business Requirements**
- **Performance:** The instance type (`t3.large`) continues to provide sufficient CPU and memory for peak usage (70% CPU, 60% memory).
- **Cost Optimization:** EBS IOPS are set to the minimum allowed by AWS for gp3, ensuring no unnecessary overspending. No additional cost for unused performance is incurred.
- **Storage:** EBS volume is configured at the smallest size and baseline IOPS possible for gp3, given AWS constraints. gp2 is not suitable for small volumes requiring high IOPS.
- **Monitoring:** CloudWatch alarm ensures proactive performance tracking.

---

## **Cost Comparison**

| Resource       | Before                | After                 | Rationale                                   |
|----------------|----------------------|-----------------------|----------------------------------------------|
| Instance Type  | t3.large             | t3.large              | Workload-optimized, no over-provisioning     |
| EBS Volume     | gp3, 8 GiB, 3000 IOPS| gp3, 8 GiB, 3000 IOPS | Minimum allowed by AWS, matches constraint   |

*Note: No further cost reduction is possible for EBS due to AWS minimums for gp3. Switching to gp2 would not guarantee required IOPS at this volume size.*

---

## **Conclusion**
By matching the instance and storage configurations to actual workload requirements and AWS service constraints, we have ensured that `qa-instance-1` is both cost-effective and fully capable of handling business needs. No unnecessary resources are provisioned, and monitoring is in place to alert if workload patterns change.

**Screenshots:** All relevant screenshots, including the EBS volume modification showing the IOPS constraint (see Image 1), are available in the attached folder.