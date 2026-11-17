# **AWS Lambda Project – Serverless Community Registration Portal**



Beginner-friendly, real-world project

Python + Terraform



We will build a complete serverless application on AWS, starting from an empty project directory and finishing with an automated CI/CD deployment.

The goal is not just to create a Lambda function. You will learn how different AWS services communicate, how to secure them, how to deploy infrastructure using Terraform, and how to troubleshoot production-style applications.

Since you have already worked with Flask, EC2, S3 and RDS in your earlier Community Registration Portal, this project will introduce you to a different architecture: **serverless computing**.

## **1. Project requirements**

# **AWS Community Portal**

[AWS Lambda: When You Stop Managing Servers and Start Thinking in Events | by Yaswanth Reddy Arumulla | Mar, 2026 | Medium](https://images.openai.com/static-rsc-4/caf3fQaBAFIFqh8TvY0Yryk6gLvjRCV0Unxq3AS6pEGh73-8VKHMSRzEvSq-WkHVTTV9FYwmG93yZjEAR07jpkTtVD8GbsmtLdMI0dkeMVVQnAHkPF8KtOn3l7P9kv9tNoIFk4lCoE_burMlAg-kBLwVY9wP-nED94x3ax8hJto?purpose=inline)

[medium.com](https://medium.com/%40yaswanth.arumulla/aws-lambda-when-you-stop-managing-servers-and-start-thinking-in-events-98c1709de9b1?utm_source=chatgpt.com)

**Application functionality**

- Member registration and profile management.
- Secure user authentication.
- Resume and document uploads.
- Document listing and downloads.
- Registration email notifications.
- Application monitoring and error tracking.
- Automated infrastructure deployment.

  Backend

  **Python 3.12**

  Infrastructure

  **Terraform**

  Database

  **DynamoDB**

  File storage

  **Amazon S3**

  API

  **API Gateway HTTP API**

  CI/CD

  **GitHub Actions**

## **2. Architecture diagram**

Here is the architecture we will implement.

**Frontend / Web Browser**

Community members

HTTPS requests

**Amazon API Gateway**

HTTP API and route management

**AWS Lambda – Python**

Business logic, validation and processing

**DynamoDB**

Member metadata

**Amazon S3**

Resumes and documents

**Amazon Cognito**

Authentication

**Amazon SES**

Email notifications

**CloudWatch + CloudTrail**

Logs, monitoring and AWS API auditing

### **How the application works**

1. A member opens the Community Portal.
2. The member registers using their email and password.
3. Amazon Cognito handles authentication.
4. API Gateway receives the HTTPS request.
5. Lambda validates the request and processes registration.
6. DynamoDB stores member information.
7. Lambda generates a pre-signed S3 URL for document uploads.
8. The browser uploads documents directly to S3.
9. Lambda stores the document metadata in DynamoDB.
10. CloudWatch captures application logs and errors.

**Important:** Passwords will not be stored in DynamoDB. Cognito will manage user credentials.

## **3. AWS services and their responsibilities**

| Service        | What we will implement               |
| -------------- | ------------------------------------ |
| Lambda         | Python backend functions             |
| API Gateway    | REST-style HTTP endpoints            |
| Cognito        | User registration and authentication |
| DynamoDB       | Members and uploaded-file metadata   |
| S3             | Resume and document storage          |
| IAM            | Least-privilege Lambda permissions   |
| CloudWatch     | Logs, metrics and alarms             |
| SES            | Email notifications                  |
| Terraform      | Create and manage AWS infrastructure |
| GitHub Actions | Automated testing and deployment     |

We will use a single Lambda handler initially to keep the beginner setup manageable. Later, we can split the application into separate Lambda functions.

## **4. Project development phases**

1. **Phase 1 – Local development environment**

   Install Python, Terraform, AWS CLI and Git. Configure AWS credentials.
2. **Phase 2 – Terraform infrastructure**

   Create IAM roles, S3, DynamoDB, Cognito, Lambda and API Gateway.
3. **Phase 3 – Python Lambda backend**

   Implement registration, member retrieval, document upload and download.
4. **Phase 4 – Security**

   Configure Cognito JWT authorization, S3 encryption, CORS, IAM and validation.
5. **Phase 5 – Testing**

   Use Pytest, local tests, AWS integration tests and Postman.
6. **Phase 6 – CI/CD**

   GitHub Actions, Terraform validation, automated tests and deployment.
7. **Phase 7 – Production readiness**

   Monitoring, alarms, cost optimization, backups and troubleshooting.

## **5. Download the complete project source code**

**AWS Lambda Community Portal**

Python + Terraform + GitHub Actions

16 project files · ZIP archive

Ready

&#x20;Download complete source code

### **Project folder structure**

After extracting the ZIP, you will have:

```
aws-lambda-community-portal/
│
├── app/
│   ├── __init__.py
│   └── handler.py
│
├── infra/
│   ├── versions.tf
│   ├── providers.tf
│   ├── variables.tf
│   ├── main.tf
│   ├── outputs.tf
│   └── terraform.tfvars.example
│
├── tests/
│   └── test_handler.py
│
├── .github/
│   └── workflows/
│       └── ci-cd.yml
│
├── docs/
│   ├── CI_CD.md
│   └── SECURITY.md
│
├── requirements.txt
├── requirements-dev.txt
├── README.md
└── .gitignore
```

The project includes the Python Lambda handler, Terraform infrastructure, Cognito authentication, API Gateway, DynamoDB, private S3 bucket, IAM policies, tests and GitHub Actions workflow.

## **6. Phase 1 – Install the required software**

We will first configure your local Windows development environment.

[1. Python — Installation instructions for FoNS 2020.0 documentation](https://images.openai.com/static-rsc-4/0kahW3dTkjSRy4DkvEe2xPcz9w1TLUUK9lz9u3CwoYs-cdKVFuz_yhfoKDelj-pz456RKXZm3NisMxY6W_ogoMjvWkIw_qTdXz2SnAPCiLs0vQDC4_FaoabvX6-EUEwTuW890ESm6L1DSEhYFn1ooK0XOidVAxfHtnOX_H8pZPk?purpose=inline)

[imperial-fons-computing.github.io](https://imperial-fons-computing.github.io/python.html?utm_source=chatgpt.com)

Install these tools:

| Software    | Purpose                   | Official download                                                                                               |
| ----------- | ------------------------- | --------------------------------------------------------------------------------------------------------------- |
| Python 3.12 | Backend development       | [Python](https://www.python.org/downloads/?utm_source=chatgpt.com)                                              |
| VS Code     | Code editor               | [VS Code](https://code.visualstudio.com/?utm_source=chatgpt.com)                                                |
| AWS CLI v2  | AWS management            | [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html?utm_source=chatgpt.com) |
| Terraform   | Infrastructure deployment | [Terraform](https://developer.hashicorp.com/terraform/install?utm_source=chatgpt.com)                           |
| Git         | Source control            | [Git](https://git-scm.com/downloads?utm_source=chatgpt.com)                                                     |
| Postman     | API testing               | [Postman](https://www.postman.com/downloads/?utm_source=chatgpt.com)                                            |

Verify installations:

```
python --version
aws --version
terraform version
git --version
```

We will use Python 3.12, which is supported by AWS Lambda.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.aws.amazon.com\&sz=32)

AWS Lambda+1



## **7. Phase 2 – Configure AWS credentials**

Open PowerShell.

Run:

```
aws configure
```

Enter your AWS credentials:

```
AWS Access Key ID: YOUR_ACCESS_KEY
AWS Secret Access Key: YOUR_SECRET_KEY
Default region name: ap-south-1
Default output format: json
```

Verify:

```
aws sts get-caller-identity
```

You should receive your AWS account ID and IAM identity.

**Security:** Use an appropriately permissioned IAM identity, never your root account credentials. Do not share your access keys or commit them to GitHub.

## **8. Phase 3 – Run the project locally**

Extract the ZIP and open the project in VS Code.

Open the terminal:

```
cd aws-lambda-community-portal
```

Create a virtual environment:

```
python -m venv .venv
```

Activate:

```
.venv\Scripts\Activate.ps1
```

Install testing dependencies:

```
pip install -r requirements-dev.txt
```

Run tests:

```
python -m pytest -q
```

3 tests passed

I ran the included Python unit tests successfully. Terraform deployment and AWS integration have not yet been executed in your account.

## **9. Phase 4 – Deploy AWS infrastructure using Terraform**

[Your First Infrastructure as Code in Four Commands - DEV Community](https://images.openai.com/static-rsc-4/dl519dWNfuybhhSEgLfKpKsobWyR4KX8lj_ClW2e9KC6pAomQEodx_8yFU5DAFaTmKalYK3IDhqQaYNs0IlEdAWtOADoeUOGFisgvvI5o1SyEIeR51mRyJiPnDxRQbiZ_zUnctkGA1LbexXM-VNRSBAo06H4gxGGk6w-PQwDlNc?purpose=inline)

[dev.to](https://dev.to/aws-builders/your-first-infrastructure-as-code-in-four-commands-46ep?utm_source=chatgpt.com)

This is where we start creating AWS resources.

First:

```
cd infra
```

Copy the configuration:

```
Copy-Item terraform.tfvars.example terraform.tfvars
```

Edit `terraform.tfvars`:

```
aws_region     = "ap-south-1"
project_name   = "community-portal-demo"
environment    = "dev"
allowed_origin = "http://localhost:3000"
```

### **Create a Terraform state bucket**

Before the first deployment, create a separate S3 bucket for Terraform state.

Use a globally unique name in the following commands:

```
aws s3api create-bucket `
  --bucket YOUR-UNIQUE-TF-STATE-BUCKET `
  --region ap-south-1 `
  --create-bucket-configuration LocationConstraint=ap-south-1
```

Enable versioning and block public access:

```
aws s3api put-bucket-versioning `
  --bucket YOUR-UNIQUE-TF-STATE-BUCKET `
  --versioning-configuration Status=Enabled
```

```
aws s3api put-public-access-block `
  --bucket YOUR-UNIQUE-TF-STATE-BUCKET `
  --public-access-block-configuration BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true
```

Enable encryption:

```
aws s3api put-bucket-encryption `
  --bucket YOUR-UNIQUE-TF-STATE-BUCKET `
  --server-side-encryption-configuration '{"Rules":[{"ApplyServerSideEncryptionByDefault":{"SSEAlgorithm":"AES256"}}]}'
```

Create `backend.hcl` inside the `infra` folder:

```
bucket       = "YOUR-UNIQUE-TF-STATE-BUCKET"
key          = "community-portal/dev/terraform.tfstate"
region       = "ap-south-1"
encrypt      = true
use_lockfile = true
```

Keep this configuration and the state bucket protected.

### **Initialize Terraform**

```
terraform init -backend-config=backend.hcl
```

Format:

```
terraform fmt -recursive
```

Validate:

```
terraform validate
```

Preview:

```
terraform plan
```

Deploy:

```
terraform apply
```

Type:

```
yes
```

Terraform will provision the infrastructure.

## **10. Phase 5 – Verify AWS resources**

After deployment, check the AWS Management Console.

**Resources you should see**

[File:Amazon Lambda architecture logo.svg - Wikimedia Commons](https://images.openai.com/static-rsc-4/sZxX2cXjdsDLPExiqkfhb1orTkckpODAeZJCwlRn1yJATmE65dGFaa1dPvgo2K75uT4b8bMdX5HOxRBJKEIi4_TxeBX2cTgOeA41iIA2JTYCDBediCKN1qSi6K_pEVv3HOpsJa7Dm_hzfXWEW2dYZbc9Z3WSOQG6XgdOPS3saZw?purpose=inline)

**Lambda**

community-portal-demo-dev-api

[AWS API Gateway Logo PNG Vector (SVG) Free Download](https://images.openai.com/static-rsc-4/LJBV0DV7m3aM7bZRzBuQ2lzabZlVVK_ShiSAKZv1aNxkLjoRS0eKJ-Ln7d4OoQC8_p-v-ZfMuePuyIe4dNvVFySSmTCfRnxbRyzl4zDk4pNdDCtlTN6FMN-INccLkPfXk89k2cJuDVLUAOxb5uOuY8wsEe_j4aEdtvrLf3n7vB8?purpose=inline)

**API Gateway**

[Microsoft Azure Blob Storage | Integrations | OneTrust](https://images.openai.com/static-rsc-4/uCxoznvyfW0s9gfHCxXjejVVc2uQujFIVJDBI6Ive0cuQtU3_3yOz1N7ZpM14ZqMlfa511xdkZ9EJiLnigW-i7BFRlTX68vZnA7AASzn6pogVT0vi7q3f4Eo67tQ4o93iP0kX80llOJyqIZgsl2oOVR7RTwk_sKSwhDb-1-8SoE?purpose=inline)

**DynamoDB**

[Amazon S3 Simple Storage Service Logo Vector Png | AWS S3 Bucket Icon  - freepng](https://images.openai.com/static-rsc-4/rB8GMmjRGUBIfO9GRNEL6l37e3jVW1hoDOCdtBff_Wr7VxkdCHtrta2g8EOf4zncP-U_xh6GGgSiEkpH5sASXFUOS_FyAJByqom1RHN_8AH3G2_0e-dOIH9z8H7GWykzTw3-woJ0v9yGGL6R4soSj66bGyOOPAMJOgN_sNVgnU0?purpose=inline)

**S3**

[Aws Logo PNG Vectors Free Download](https://images.openai.com/static-rsc-4/tm_f7MzrqW1gL6tnTEelHGHVcV9l1jFwiwmjdMeP5i6wVS7bWrqMmHBpbDJJ-2nvFYpi9opbLt5XwRTCrMZmbh7PJhfewv3gD6kD1KrGx-w6l0LL9PYIUdpQgtmNgDFdwTBomegcVX7OXfduWjpsaISmlm1QC-PWqsapgID9bxo?purpose=inline)

**Cognito**

[How to build Web Application Dashboards in AWS CloudWatch | Si Novi](https://images.openai.com/static-rsc-4/yT3SaHPlzDux3CdNfYHGEz3ep-edJ4XH72KA338nB5MnG5zqWZeThLp_scsur6bSp9GrxRwS_DpD5PaZlG0ACbps7b1N9pTcMLD8fQY3-wgycWsImjnhPwHSwi9sK1beN5mManv6vXCKL1V6lM03MpnouxLzOV8sj0k_wLsptSI?purpose=inline)

**CloudWatch**

Get the API endpoint:

```
terraform output -raw api_endpoint
```

Test the public health endpoint:

```
$API = terraform output -raw api_endpoint

Invoke-RestMethod "$API/health"
```

Expected response:

```
{
  "status": "ok",
  "service": "community-portal"
}
```

## **11. Phase 6 – Authentication and API testing**

The project uses Cognito for authentication.

First, create a test user using the Cognito User Pool ID and App Client ID from Terraform outputs.

Then obtain an access token using Cognito's `initiate-auth` command.

Use the access token in Postman:

```
Authorization: Bearer YOUR_ACCESS_TOKEN
```

Test these APIs:

| Method | Endpoint                            | Purpose                 |
| ------ | ----------------------------------- | ----------------------- |
| GET    | `/health`                           | Health check            |
| POST   | `/members`                          | Register member profile |
| GET    | `/members/me`                       | Retrieve profile        |
| POST   | `/documents/presign`                | Generate upload URL     |
| GET    | `/documents`                        | List documents          |
| GET    | `/documents/{document_id}/download` | Generate download URL   |

All routes except `/health` require valid Cognito authentication.

The source code contains example request bodies and testing commands in `README.md`.

## **12. Phase 7 – CI/CD with GitHub Actions**

[AWS CodePipeline CI/CD Pipeline Patterns](https://images.openai.com/static-rsc-4/qXPcCZAxRcmZUbpJ13g8E-p1Yn94GGBFBfhSglPYMBplfIcMLID0RKxMC8vhKeIigc-5gblmxMvF7tzzt7NSJ1cYzo8yLqu0wY-Vd1AUZ28m6kiLTKPYMzCM7HgNrT9yf5NA4_HPLY04s_hH7v4ltMk2QmydSAk-dRtIm-O69SI?purpose=inline)

[factualminds.com](https://www.factualminds.com/blog/aws-codepipeline-cicd-pipeline-patterns-for-production/?utm_source=chatgpt.com)

Our CI/CD pipeline will work like this:

**Developer pushes code to GitHub**

**GitHub Actions**

Run Python tests and Terraform validation

**AWS IAM OIDC authentication**

Temporary credentials, no stored AWS access keys

**Terraform deployment**

Update AWS infrastructure and Lambda code

**Deployment complete**

The workflow file is already included in the ZIP.

You need to configure GitHub OIDC, create a restricted IAM deployment role, and configure these GitHub repository variables:

- `AWS_ROLE_ARN`
- `AWS_REGION`
- `AWS_STATE_BUCKET`

GitHub OIDC is preferable to storing long-lived AWS access keys in GitHub.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.github.com\&sz=32)

GitHub Docs+1



## **13. Security and production considerations**

Before making this application publicly available, we need to address:

1. Enforce upload size limits at the upload mechanism, not just in application responses.
2. Validate file signatures and scan uploaded documents for malware.
3. Configure rate limiting and abuse protection.
4. Protect Terraform state and restrict deployment IAM permissions.
5. Enable monitoring and billing alerts.
6. Add account deletion and document cleanup.
7. Configure production HTTPS frontend origins.

SES email notifications and a frontend are planned extensions, not implemented in this initial source package.

**Cost warning:** AWS services can incur charges even in a learning project. Configure AWS Budgets and destroy the stack when you finish experimenting:

```
terraform destroy
```

The application bucket is configured for Terraform-managed destruction, so back up any documents you need first.

## **14. Our learning checklist**

**Project progress**

# **0/14**

Install Python, AWS CLI, Terraform and Git

Configure AWS credentials

Download and open the project

Run Python unit tests

Create Terraform remote state bucket

Deploy infrastructure using Terraform

Verify Lambda and API Gateway

Create Cognito test user

Test member registration API

Upload a document to S3

Test document download

Configure GitHub OIDC

Deploy through GitHub Actions

Verify CloudWatch logs and alarms

## **What I recommend doing first**

Let's complete this project one phase at a time rather than deploying everything blindly.

**Start with Phase 1 and Phase 2.** Once your local environment is ready and `aws sts get-caller-identity` works, we can proceed to Terraform and understand each AWS resource as we create it.

The aim is to understand the project well enough to explain its architecture, implementation, IAM permissions, troubleshooting and deployment in an AWS DevOps interview.
