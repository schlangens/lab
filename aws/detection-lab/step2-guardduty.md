###  Setting up GuardDuty

#### **Objective**
Enable GuardDuty to provide continuous monitoring for malicious or unauthorized behavior in your AWS environment.

---

#### **What We Did**

1. **Enabled GuardDuty**: Activated the GuardDuty service to monitor logs from CloudTrail, VPC Flow Logs, and DNS query logs.
2. **Verified GuardDuty**: Ensured the service was running and correctly configured by checking its detector status.

---

#### **Commands Executed**

##### **Provisioning**

1. **Enable GuardDuty**:
   ```bash
   aws guardduty create-detector --enable
   ```

2. **List Detector ID**:
   ```bash
   aws guardduty list-detectors
   ```
   - Note the `DetectorId` from the output.

3. **Check GuardDuty Status**:
   ```bash
   aws guardduty get-detector --detector-id <DetectorId>
   ```
   - Replace `<DetectorId>` with the actual ID from the previous command.

---

#### **Why This Matters**

- **Threat Detection**: GuardDuty analyzes logs to identify potential threats such as unauthorized access or compromised instances.
- **Integration**: It works seamlessly with CloudTrail and other AWS services to provide robust security insights.
- **Low Maintenance**: Fully managed by AWS, requiring no infrastructure setup or ongoing maintenance.

---

#### **Teardown Commands**

1. **Disable GuardDuty**:
   ```bash
   aws guardduty update-detector --detector-id <DetectorId> --enable false
   ```

2. **Delete GuardDuty Detector**:
   ```bash
   aws guardduty delete-detector --detector-id <DetectorId>
   ```

---

#### **Notes**

- GuardDuty works in conjunction with CloudTrail, so the CloudTrail setup must remain active for meaningful monitoring.
- GuardDuty findings can be exported for further analysis or integrated with a SIEM solution.

---

