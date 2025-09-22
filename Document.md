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
- **Meets access patterns**: Recent backups are quickly accessible, older backups are moved to cheaper storage with appropriate restore SLAs.
- **Cost optimization**: Automated transitions reduce storage costs over time.
- **Compliance**: Data is retained