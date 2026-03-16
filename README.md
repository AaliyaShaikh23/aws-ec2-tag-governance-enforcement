# aws-ec2-tag-governance-enforcement
Project Overview

This project demonstrates how to enforce mandatory tagging when launching EC2 instances in AWS. In large enterprise environments, resources are created by multiple teams. Without proper tagging, it becomes difficult to identify resource owners, track costs, and maintain compliance.

To solve this problem, a governance policy is implemented that prevents launching EC2 instances unless required tags are provided.

---

Problem Statement

In the organization’s cloud environment, EC2 instances were being launched without proper tagging. This caused several issues:

- Resource owners could not be identified
- Cost allocation reports were inaccurate
- Compliance audits failed due to missing metadata

The cloud governance team introduced a rule:

"No EC2 instance should be launched unless mandatory tags are provided."

---

Objectives

The objectives of this project are:
- Enforce mandatory tagging for EC2 instance creation
- Prevent launching instances without required tags
- Improve resource ownership tracking
- Support accurate cost allocation and reporting
- Ensure governance and compliance in the cloud environment

---

Required Tags
The following tags are mandatory when launching an EC2 instance:

Tag Key| Description
Name| Resource owner name
emailID| Official email address
phoneNo| Contact number
Place| Location of the resource

Example:
Key| Value
Name| Demo
emailID| aaliyashaikh3439@gmail.com
phoneNo| 9022143549
Place| Pune

---

Technologies Used

- AWS EC2
- AWS IAM
- AWS Organizations (optional)
- IAM Policies
- AWS Console

---

Architecture
The system follows this workflow:

User launches EC2 instance
↓
IAM Policy validates required tags
↓
If tags are missing → Request Denied
If tags are present → Instance Launch Successful

---

IAM Tag Enforcement Policy
The following IAM policy ensures that EC2 instances cannot be launched without required tags:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyEC2LaunchWithoutTags",
      "Effect": "Deny",
      "Action": "ec2:RunInstances",
      "Resource": "*",
      "Condition": {
        "ForAllValues:StringNotEquals": {
          "aws:TagKeys": [
            "Name",
            "emailID",
            "phoneNo",
            "Place"
          ]
        }
      }
    }
  ]
}

---

Implementation Steps

Step 1: Create IAM Policy

1. Open AWS Console
2. Navigate to IAM
3. Create a new policy using JSON
4. Add the tag enforcement policy

Step 2: Attach Policy to IAM User

1. Open IAM Users
2. Select the IAM user
3. Attach the tag enforcement policy

Step 3: Launch EC2 Without Tags

1. Open EC2 Console
2. Click "Launch Instance"
3. Do not add required tags

Result:
Instance launch fails due to policy restriction.

Step 4: Launch EC2 With Required Tags

Add the mandatory tags:

Name → Demo
emailID → aaliyashaikh3439@gmail.com
phoneNo → 9022143549
Place → Pune

Result:
Instance launches successfully.

---
Validation
Test Case| Result
Launch EC2 without tags| Failed
Launch EC2 with tags| Successful

This confirms that the IAM policy correctly enforces tag governance.
---

Benefits of Tag Governance
Implementing tag governance provides several benefits:
- Better resource ownership visibility
- Accurate cost allocation
- Improved compliance and auditing
- Easier resource management
- Enhanced cloud governance

---

Conclusion
This project demonstrates how AWS IAM policies can enforce mandatory tagging for EC2 instances. By preventing instance creation without required tags, organizations can ensure proper governance, accurate cost tracking, and compliance in their cloud environment.
