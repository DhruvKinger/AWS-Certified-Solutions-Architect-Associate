# Task 3: Budget Setup and Tagging Strategy for AdSpark

## Scenario

AdSpark, a digital marketing startup, has recently migrated its infrastructure to AWS. The CFO is concerned about uncontrolled cloud spending due to engineers testing services without limits. As the Cloud Solutions Architect, you were tasked with implementing cost controls to prevent budget overruns.

## Business Requirements

- A monthly AWS budget of $1,000 covering both Production and Development environments.
- Email alerts when:
  - 50% of the budget is reached (early warning)
  - 80% of the budget is reached (urgent action required)
- A tagging strategy to identify resources by environment and team.
- A mechanism to enable cost breakdown by environment and team ownership.

## Budget Configuration

A monthly cost budget named `adspark-monthly-budget` was created with the following settings:

- **Budget Type**: Cost Budget
- **Amount**: $1,000 USD
- **Period**: Monthly recurring
- **Scope**: All AWS services

### Alert Thresholds

Two alert thresholds were configured:

- **50% Threshold**: Sends email notification to the CFO and Cloud Architect.
- **80% Threshold**: Sends email and SNS notification to the CFO, Cloud Architect, and DevOps team.

All screenshots of the budget setup and alert configuration are available in the folder.

## Tagging Strategy

To ensure resources are easily identifiable by environment and team, the following tagging policy was defined:

| Tag Key     | Example Values              | Purpose                                  |
|-------------|-----------------------------|------------------------------------------|
| Environment | Production, Development      | Distinguish between environments         |
| Team        | IT, Engineering | Attribute resources to teams         |
| Owner       | dhruv                 | Identify responsible person              |
| Project     | AdSparkApp                   | Link resources to specific projects      |

This tagging strategy will be applied to all future AWS resources during creation or via the Tag Editor.

## Cost Allocation Tag Activation

To enable cost tracking by tags, the following steps were completed:

1. Navigated to the **Billing Dashboard**.
2. Opened **Cost Allocation Tags**.
3. Activated custom tags including `Environment` and `Team`.

All screenshots of the tag activation process are available in the folder.

## Outcome

AdSpark now has a proactive cost control mechanism in place. Budget alerts will notify stakeholders before overspending occurs, and the tagging strategy ensures future resources can be tracked and categorized effectively.
