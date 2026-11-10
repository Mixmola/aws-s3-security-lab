# AWS S3 Security Lab – Security Findings

## 1. S3 Bucket Creation
Created an Amazon S3 bucket to use as the storage resource for this security lab.

**Objective:** Establish a storage environment for implementing and testing AWS security controls.

## 2. Block Public Access
Enabled all four S3 Block Public Access settings.

**Why this matters:** These settings help prevent accidental public exposure of bucket data.

## 3. Default Encryption
Configured default server-side encryption using SSE-S3.

**Why this matters:** This helps ensure objects uploaded to the bucket are encrypted at rest.

## 4. Bucket Versioning
Enabled S3 Versioning.

**Why this matters:** Versioning preserves multiple versions of objects, which can help recover from accidental overwrites or deletions.

## 5. IAM Least-Privilege Access Control
Created a customer-managed IAM policy named `S3-Lab-Limited-Access`.

The policy grants:
- `s3:ListBucket` – permission to list the bucket's contents.
- `s3:GetObject` – permission to read objects.
- `s3:PutObject` – permission to upload objects.

Created a test IAM user named `s3-lab-test-user` and attached the custom policy.

The policy intentionally excludes object and bucket deletion permissions.

## 6. IAM Policy Simulation Results

| IAM Action | Expected Result | Simulation Result |
|---|---|---|
| `s3:ListBucket` | Allow | Allowed |
| `s3:GetObject` | Allow | Allowed |
| `s3:PutObject` | Allow | Allowed |
| `s3:DeleteObject` | Deny | Denied |
| `s3:DeleteBucket` | Deny | Denied |

**Note:** These results came from the IAM Policy Simulator. They do not represent live access tests using the test identity.

## 7. Challenges Encountered
The IAM Policy Simulator displayed a "Feature unavailable" message when accessed through one IAM console view. I was able to access the simulator through another interface and complete all five permission tests.

The console availability issue remains unresolved.

## 8. Key Lessons
Through this project, I practised:
- Securing an Amazon S3 bucket.
- Preventing public access.
- Configuring server-side encryption.
- Enabling bucket versioning.
- Creating custom IAM policies.
- Applying the principle of least privilege.
- Understanding bucket ARNs and object ARNs.
- Testing allowed and denied permissions.

## 9. Further Work
- Investigate the simulator availability issue.
- Perform live access tests using the test identity.
- Add screenshots as project evidence.
- Review and document the final bucket configuration.
