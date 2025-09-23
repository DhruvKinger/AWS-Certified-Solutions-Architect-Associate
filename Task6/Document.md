
# Task 6: DynamoDB Cost Optimization During Development

## Current Findings

The application backend uses DynamoDB and is currently in the development phase. Based on the CloudWatch graph for table `qa-table-1`, the following observations were made:

- Read Capacity Units (RCU) show frequent spikes, reaching up to approximately 45 units per second.
- Write Capacity Units (WCU) also fluctuate, peaking around 20 units per second.
- Usage is sporadic and unpredictable, with periods of high activity followed by idle times.
- The table was initially created using Provisioned Capacity Mode with Auto Scaling disabled.

This setup incurs fixed costs regardless of actual usage, which is not ideal for a development environment with variable traffic.

---

## Changes Made

To optimize costs while allowing development to continue, the following changes were implemented:

1. Switched to On-Demand Capacity Mode
   - This mode charges only for actual read/write requests.
   - It is ideal for unpredictable workloads and development environments.

2. Enabled TTL (Time to Live)
   - TTL automatically deletes expired items, reducing storage costs.
   - The attribute `expiryTime` was configured to store UNIX timestamps.

3. Screenshots of all changes are available in the folder for reference.

---

## Outcome

The DynamoDB table `qa-table-1` is now configured for cost-efficient operation during development:

- Charges are based on actual usage
- Storage costs are minimized through TTL
- The setup meets business requirements for latency tolerance and cost control
