# Task 3: Budget Setup and Tagging Strategy for AdSpark

## Overview

AdSpark has recently migrated its infrastructure to AWS. To address concerns raised by the CFO regarding uncontrolled cloud spending, a cost control strategy was implemented. This includes budget configuration, alert thresholds, and a tagging framework to ensure visibility and accountability across environments and teams.

---

## Budget Configuration

A monthly cost budget was created to monitor and control AWS spending.

- **Budget Name**: `adspark-monthly-budget`
- **Budget Type**: Cost Budget
- **Amount**: $1,000 USD
- **Period**: Monthly recurring
- **Scope**: All AWS services used by AdSpark

### Alert Thresholds

Two alert thresholds were configured:

- **50% Threshold**: Early warning email alert
- **80% Threshold**: Urgent action email alert

These alerts notify stakeholders when spending approaches critical levels, allowing timely intervention.

---

## Tagging Strategy

To ensure that administrators can easily identify which resources belong to specific environments and teams, a standardized tagging strategy was defined.

### Tag Keys and Example Values

| Tag Key     | Example Values              | Purpose                                  |
|-------------|-----------------------------|------------------------------------------|
| Environment | Production, Development     | Distinguish between environments         |
| Team        | Marketing, IT, Engineering | Attribute resources to teams     |
| Owner       | dhruv                | Identify responsible person              |
| Project     | AdSparkApp                  | Link resources to specific projects      |

These tags will be applied to all future AWS resources during creation or via the Tag Editor.

---

## Cost Allocation Tag Activation

To enable cost tracking by tags, the defined tag keys were activated as **Cost Allocation Tags** in the AWS Billing Console. This ensures that AWS will associate usage and charges with the appropriate tags once resources are created.

---

## Cost Breakdown Using AWS Cost Explorer

AWS Cost Explorer was enabled and configured to analyze spending by environment and team ownership. Reports can be generated to show:
- Monthly cost breakdown by `Environment` tag (Production vs. Development)
- Monthly cost breakdown by `Team` tag (Marketing, Analytics, Engineering)

This allows the finance and engineering teams to understand which areas are driving costs and adjust usage accordingly.

----

## How the Solution Solves the Problem

### Budget Alerts

The budget and alert thresholds directly address the CFO’s concern about uncontrolled spending. Early and urgent notifications allow the team to monitor usage and take corrective action before exceeding the budget.

### Resource Identification

The tagging strategy ensures that every resource is clearly labeled by environment and team. This improves visibility, simplifies audits, and supports accountability.

### Cost Breakdown by Environment and Team

By activating cost allocation tags, AWS will track and associate costs with the defined tags. This enables future cost analysis by environment (Production vs. Development) and team ownership (Analytics, Engineering), supporting informed financial decisions.

### Cost Explorer
- Enabling cost visibility and accountability via Cost Explorer, so we can have a look of costing according to the tags.

---

## Screenshots

All screenshots of the AWS console configurations (budget setup, alert thresholds, tag activation) are available in the folder.
