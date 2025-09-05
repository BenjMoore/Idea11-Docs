# i11tools AWS – Quick Start Guide

This tool provides internal AWS utilities for managing accounts, including identifying **deprecated Lambda runtimes** across multiple profiles.

Example usage:

```bash
i11tools aws --profiles <Profile> lambda list-deprecated -o csv
```

This will scan the specified AWS profile and output a CSV with Lambda functions that use deprecated runtimes (Node.js ≤ 18, Python ≤ 3.10).

---

## Installation

You can install the tool either **from source** (recommended for development) or from a **wheel package** (recommended for users).

### 1. Install from Source

Clone the repository and create a virtual environment:

```bash
git clone https://<bitbucketlink>/i11tools.git
cd i11tools

# Create a virtual environment
python3 -m venv .venv
source .venv/bin/activate  # (Mac/Linux)
.\.venv\Scripts\activate   # (Windows)

# Install in editable mode
pip install -e .
```

Now you can run the tool using:

```bash
i11tools aws --profiles MyProfile lambda list-deprecated
```

---

### 2. Install from Wheel

If you have a `.whl` distribution:

```bash
pip install <i11tools-0.X.0-py3-none-any.whl>
```

⚠️ If you are installing **outside a virtual environment** and pip blocks the install, add:

```bash
pip install <i11tools-0.X.0-py3-none-any.whl> --break-system-packages
```

---

## PATH Setup

If the tool is not found after installation, you may need to add the Python scripts directory to your PATH.

### macOS / Linux

Add to `~/.zshrc` or `~/.bashrc`:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

Then reload your shell:

```bash
source ~/.zshrc
```

### Windows (PowerShell)

Add to PATH permanently:

```powershell
setx PATH "$($env:PATH);C:\Users\<YourUser>\AppData\Roaming\Python\Python310\Scripts"
```

Or run directly with:

```powershell
python -m i11tools aws --profiles MyProfile lambda list-deprecated
```

---

## Using Leapp for AWS Account Assumption

For managing multiple AWS accounts securely, it is recommended to use **Leapp** to assume roles instead of directly storing credentials.

Example workflow:

1. Install Leapp: [https://leapp.cloud](https://leapp.cloud)
2. Configure Leapp with your AWS accounts and roles.
3. Assume a role using Leapp and then run i11tools:

```bash
leapp assume DevTeamRole

# Then run i11tools with the temporary credentials
i11tools aws --profiles DevTeam lambda list-deprecated -o csv
```

This ensures that credentials are never stored locally and that role assumption is auditable.

---
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


## Usage Examples

List deprecated Lambda functions across multiple profiles:

```bash
i11tools aws --profiles DevTeam,FinanceTeam lambda list-deprecated
```

Export to CSV:

```bash
i11tools aws --profiles DevTeam lambda list-deprecated -o csv
```

Restrict to certain AWS regions:

```bash
i11tools aws --profiles DevTeam --regions us-east-1,ap-southeast-2 lambda list-deprecated
```

Using Leapp to assume roles:

```bash
leapp assume FinanceTeamRole

i11tools aws --profiles FinanceTeam lambda list-deprecated -o csv
```

---

## Notes

* Ensure your AWS profiles are configured in `~/.aws/credentials` or assumed via Leapp.
* By default, profiles **must be specified** with `--profiles`.
* The CSV file will be written to `lambda_functions.csv` in the current directory.
