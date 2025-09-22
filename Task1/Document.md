# Task 1: S3 Bucket Setup for Centralized Storage & Lifecycle Management

## Objective
Set up a centralized S3 bucket to store unstructured data and user profile pictures, while implementing lifecycle rules to optimize cost based on access patterns and retention requirements.

## Bucket Configuration

- **Bucket Name**: `cloudarchs-central-storage`
- **Versioning**: Enabled
- **Encryption**: SSE-S3
- **Public Access**: Blocked

## Folder Structure (Prefixes)

- `backups/` – Used for storing backup data
- `profile-pictures/` – Used for storing user-uploaded profile images

## Lifecycle Rules

### Rule 1: Backups (`backups/` prefix)
| Days After Creation | Action                          | Storage Class               |
|---------------------|----------------------------------|-----------------------------|
| 0–30                | Keep in Standard                 | Standard                    |
| 31                  | Transition to Intelligent-Tiering| Intelligent-Tiering         |
| 91                  | Transition to Glacier Instant Retrieval | Glacier Instant Retrieval |
| 181                 | Transition to Glacier Deep Archive | Glacier Deep Archive       |
| 365                 | Expire/Delete                    | N/A                         |

### Rule 2: Profile Pictures (`profile-pictures/` prefix)
| Days After Creation | Action                          | Storage Class               |
|---------------------|----------------------------------|-----------------------------|
| 0–30                | Keep in Standard                 | Standard                    |
| 31 (optional)       | Transition to Intelligent-Tiering| Intelligent-Tiering         |

## Why This Configuration Works

The lifecycle configuration directly maps to the business requirements:

### Backup Data
- **0–30 days**: Stored in Standard for frequent access and fast restoration.
- **31–90 days**: Moved to Intelligent-Tiering to reduce cost while maintaining quick access.
- **Beyond 90 days**: Transitioned to Glacier Instant Retrieval for rare access with fast restore.
- **Beyond 6 months**: Stored in Glacier Deep Archive for compliance, with up to 24-hour restore SLA.
- **After 1 year**: Automatically deleted to avoid unnecessary storage costs.

### Profile Pictures
- Stored in Standard for fast access during profile loads.
- Optional transition to Intelligent-Tiering after 30 days to reduce cost if access drops.

This setup ensures:
- Fast access for recent and frequently used data
- Cost savings through automated transitions
- Compliance with retention policies
- Simplified API access for developers

---

## ✅ Outcome
The bucket is now optimized for both performance and cost. Lifecycle rules are in place to automatically manage storage classes based on access patterns, ensuring we meet business SLAs while minimizing unnecessary spend.
