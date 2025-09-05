# AWS Session Setup Instructions with Leapp

## Prerequisites
- Install [AWS CLI](https://aws.amazon.com/cli/) if not already installed.
- Install the Leapp tool (or equivalent for managing AWS sessions).

---

## Step 1: Add a New Session (Federated IAM Role)

1. Open **Leapp** and choose **Add a New Session**.
2. Select **Amazon AWS**.
3. Fill in the fields as follows:

| Field | Value |
|-------|-------|
| Access method | AWS IAM Role Federated |
| Named profile | Your choice (e.g., `default`) |
| Session Alias | `Idea11SSO-Engineer-Consulting-Team` |
| Region | `ap-southeast-2` |
| Role ARN | `arn:aws:iam::<account_id>:role/Idea11SSO-Engineer-Consulting-Team`<br>**Note:** Replace `<account_id>` with the specific AWS account number for the customer. This is the long number in the Control Room environment URL. |
| SAML 2.0 URL | `https://launcher.myapps.microsoft.com/api/signin/<id>?tenantId=<tenant_id>` |
| Identity Provider | `arn:aws:iam::<account_id>:saml-provider/Idea11-Azure-AD` |

4. Click **Sign in to your account**.

---

## Step 2: Add a New Session (Chained IAM Role)

1. Open **Leapp** and choose **Add a New Session**.
2. Select **Amazon AWS**.
3. Fill in the fields as follows:

| Field | Value |
|-------|-------|
| Access method | AWS IAM Role Chained |
| Named profile | `business-prod` (or use your preferred naming convention, e.g., `client-<project>-environment`) |
| Session Alias | `business-prod` |
| Region | `ap-southeast-2` |
| Role ARN | `arn:aws:iam::<account_id>:role/Idea11-AWS-Consulting-Team`<br>**Note:** Replace `<account_id>` with the specific AWS account number for the customer. |
| Role Session Name | `assumed-from-leapp` (can be any value) |
| Assumer Session | `Idea11SSO-Engineer-Consulting-Team` |

---

## Step 3: Connecting to Additional Chained Sessions

To connect to more chained sessions, follow this formula:

1. **Access method:** AWS IAM Role Chained  
2. **Named profile:** Your chosen profile name (e.g., `client-<project>-<env>`)  
3. **Session Alias:** Your chosen alias  
4. **Region:** Target AWS region (e.g., `ap-southeast-2`)  
5. **Role ARN:** `arn:aws:iam::<customer_account_id>:role/<target_role>`  
   - Replace `<customer_account_id>` with the specific AWS account number.  
   - Replace `<target_role>` with the IAM role you need to assume.  
6. **Role Session Name:** Arbitrary value (e.g., `assumed-from-leapp`)  
7. **Assumer Session:** The **session alias** of the session that has permissions to assume this role  

> Essentially, each chained session assumes the role of a previous session, so the **Assumer Session** must reference a session that already has access rights.

