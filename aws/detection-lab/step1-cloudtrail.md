### Step 1: Setting up CloudTrail

#### **Objective**
Create a CloudTrail to log all API activity in the AWS account and store the logs in an S3 bucket. This provides visibility into actions taken in your account, which is critical for security monitoring and compliance. 🕵️‍♂️

---

#### **What We Did**

1. **Created an S3 bucket**: This bucket serves as the storage location for all CloudTrail logs, ensuring we have a centralized place to review account activity.
2. **Enabled versioning on the S3 bucket**: Versioning ensures the integrity of the logs by preserving past versions, which is crucial for auditing and troubleshooting.
3. **Updated the S3 bucket policy**: This step granted CloudTrail the necessary permissions to write logs to the bucket.
4. **Created a CloudTrail**: This service logs every API call made in your AWS account, allowing you to detect unauthorized or suspicious activity.
5. **Started logging**: We activated the trail to start capturing events immediately.
6. **Verified the setup**: Using the AWS CLI, we confirmed that CloudTrail was logging successfully.

---

#### **Commands Executed**

##### **Provisioning**

1. **Create an S3 Bucket**:
   ```bash
   aws s3api create-bucket \
       --bucket detection-lab-cloudtrail-logs \
       --region us-east-1
   ```

2. **Enable Versioning**:
   ```bash
   aws s3api put-bucket-versioning \
       --bucket detection-lab-cloudtrail-logs \
       --versioning-configuration Status=Enabled
   ```

3. **Update S3 Bucket Policy**:
   Save the following policy to `bucket-policy.json`:
   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "AllowCloudTrailWrite",
               "Effect": "Allow",
               "Principal": {
                   "Service": "cloudtrail.amazonaws.com"
               },
               "Action": "s3:PutObject",
               "Resource": "arn:aws:s3:::detection-lab-cloudtrail-logs/AWSLogs/*",
               "Condition": {
                   "StringEquals": {
                       "s3:x-amz-acl": "bucket-owner-full-control"
                   }
               }
           },
           {
               "Sid": "AllowBucketAccess",
               "Effect": "Allow",
               "Principal": {
                   "Service": "cloudtrail.amazonaws.com"
               },
               "Action": "s3:GetBucketAcl",
               "Resource": "arn:aws:s3:::detection-lab-cloudtrail-logs"
           }
       ]
   }
   ```
   Apply the policy:
   ```bash
   aws s3api put-bucket-policy \
       --bucket detection-lab-cloudtrail-logs \
       --policy file://bucket-policy.json
   ```

4. **Create a CloudTrail**:
   ```bash
   aws cloudtrail create-trail \
       --name DetectionLabTrail \
       --s3-bucket-name detection-lab-cloudtrail-logs
   ```

5. **Start Logging**:
   ```bash
   aws cloudtrail start-logging --name DetectionLabTrail
   ```

6. **Verify CloudTrail**:
   ```bash
   aws cloudtrail describe-trails
   ```

---

#### **Why This Matters**

- **Visibility**: CloudTrail provides a complete history of API calls and account activity, which is essential for identifying suspicious behavior and auditing changes.
- **Compliance**: Many regulatory frameworks (e.g., GDPR, HIPAA) require logging and monitoring of account activity. CloudTrail helps meet these requirements.
- **Incident Response**: In case of a security breach, CloudTrail logs can help identify what happened and when, providing valuable forensic data. ⚖️

---

#### **Teardown Commands**

1. **Stop Logging**:
   ```bash
   aws cloudtrail stop-logging --name DetectionLabTrail
   ```

2. **Delete the CloudTrail**:
   ```bash
   aws cloudtrail delete-trail --name DetectionLabTrail
   ```

3. **Delete All Versions of Objects**:
   ```bash
   aws s3api list-object-versions --bucket detection-lab-cloudtrail-logs --query '{Objects: Versions[].{Key: Key, VersionId: VersionId}}' --output json | \
   jq -c '.Objects[]' | \
   while read object; do \
       aws s3api delete-object --bucket detection-lab-cloudtrail-logs --key "$(echo $object | jq -r .Key)" --version-id "$(echo $object | jq -r .VersionId)"; \
   done
   ```

4. **Delete All Delete Markers**:
   ```bash
   aws s3api list-object-versions --bucket detection-lab-cloudtrail-logs --query '{Objects: DeleteMarkers[].{Key: Key, VersionId: VersionId}}' --output json | \
   jq -c '.Objects[]' | \
   while read marker; do \
       aws s3api delete-object --bucket detection-lab-cloudtrail-logs --key "$(echo $marker | jq -r .Key)" --version-id "$(echo $marker | jq -r .VersionId)"; \
   done
   ```

5. **Empty the S3 Bucket**:
   ```bash
   aws s3 rm s3://detection-lab-cloudtrail-logs --recursive
   ```

6. **Delete the S3 Bucket**:
   ```bash
   aws s3api delete-bucket --bucket detection-lab-cloudtrail-logs --region us-east-1
   ```

---

#### **Notes**

- CloudTrail is essential for tracking API calls and user activity within the AWS account.
- The S3 bucket ensures logs are stored securely and durably. 📦
- When deleting versioned buckets, ensure all versions and delete markers are removed. 🛠️

---


