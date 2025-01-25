## Custom Detection Using CloudWatch Logs Insights

#### **Objective**
Leverage CloudWatch Logs Insights to create custom detections by querying CloudTrail logs for specific activities. These detections serve as an additional layer of threat monitoring beyond GuardDuty.

---

#### **What We Did**

1. **Created a CloudWatch Log Group**: Used for storing and analyzing CloudTrail logs.
2. **Streamed CloudTrail Logs to CloudWatch**: Configured CloudTrail to send logs to the CloudWatch log group.
3. **Executed a Custom Query**: Used CloudWatch Logs Insights to search for specific activities, such as unauthorized API calls.

---

#### **Commands Executed**

##### **Provisioning**

1. **Create a CloudWatch Log Group**:
   ```bash
   aws logs create-log-group \
       --log-group-name DetectionLabLogGroup
   ```

2. **Add CloudTrail Logs to the Log Group**:
   Update the existing CloudTrail to send logs to CloudWatch:
   ```bash
   aws cloudtrail update-trail \
       --name DetectionLabTrail \
       --cloud-watch-logs-log-group-arn arn:aws:logs:us-east-1:<your-account-id>:log-group:DetectionLabLogGroup \
       --cloud-watch-logs-role-arn arn:aws:iam::<your-account-id>:role/CloudTrail_CloudWatchLogs_Role
   ```

3. **Run a Custom Query in CloudWatch Logs Insights**:
   - Execute a query to detect unauthorized operations:
     ```bash
     aws logs start-query \
         --log-group-name DetectionLabLogGroup \
         --start-time $(date +%s --date="-15 minutes") \
         --end-time $(date +%s) \
         --query-string "fields @timestamp, @message | filter @message like /UnauthorizedOperation/ | sort @timestamp desc | limit 20"
     ```
   - Retrieve the query results:
     ```bash
     aws logs get-query-results --query-id <query-id>
     ```
     - Replace `<query-id>` with the query ID from the previous command.

---

#### **Why This Matters**

- **Custom Detection**: CloudWatch Logs Insights enables tailored detections specific to your environment.
- **Real-Time Monitoring**: Queries can be scheduled to run at regular intervals for proactive security measures.
- **Integration with CloudTrail**: Combining CloudTrail logs with CloudWatch provides enhanced visibility into account activities.

---

#### **Teardown Commands**

1. **Delete the CloudWatch Log Group**:
   ```bash
   aws logs delete-log-group --log-group-name DetectionLabLogGroup
   ```

2. **Detach and Delete IAM Role**:
   - Detach the inline policy:
     ```bash
     aws iam delete-role-policy --role-name CloudTrail_CloudWatchLogs_Role --policy-name CloudTrailToCloudWatch
     ```
   - Delete the role:
     ```bash
     aws iam delete-role --role-name CloudTrail_CloudWatchLogs_Role
     ```

3. **Remove the Log Group from CloudTrail**:
   ```bash
   aws cloudtrail update-trail \
       --name DetectionLabTrail \
       --no-cloud-watch-logs-log-group-arn \
       --no-cloud-watch-logs-role-arn
   ```

---

#### **Notes**

- CloudWatch Logs Insights queries are a powerful way to identify suspicious activities, such as failed login attempts or unusual API calls.
- This step enhances the lab’s monitoring capabilities by providing real-time, queryable data. 🕵️‍♂️

---

